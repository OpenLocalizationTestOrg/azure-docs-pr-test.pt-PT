---
title: "aaaSecurely ligação tooBackEnd recursos a partir de um ambiente de serviço de aplicações"
description: "Saiba mais sobre como o toosecurely ligar toobackend recursos a partir de um ambiente de serviço de aplicações."
services: app-service
documentationcenter: 
author: stefsch
manager: erikre
editor: 
ms.assetid: f82eb283-a6e7-4923-a00b-4b4ccf7c4b5b
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/04/2016
ms.author: stefsch
ms.openlocfilehash: 6311d3fc301512ea3c4ed8f14f268f75755aa415
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="securely-connecting-toobackend-resources-from-an-app-service-environment"></a>Em segurança ligar tooBackend recursos a partir de um ambiente de serviço de aplicações
## <a name="overview"></a>Descrição geral
Uma vez que um ambiente de serviço de aplicações é sempre criado no **ou** uma rede virtual do Azure Resource Manager, **ou** um modelo de implementação clássica [rede virtual] [ virtualnetwork], ligações de saída a partir dos recursos de back-end de tooother ambiente de serviço de aplicações possam circular exclusivamente através de rede virtual Olá.  Com uma alteração recente efetuada em Junho de 2016, ASEs também podem ser implementados em redes virtuais que utilizam os intervalos de endereços público ou espaços de endereços RFC1918 (ou seja, endereços privados).  

Por exemplo, poderá ser um SQL Server em execução num cluster de máquinas virtuais com a porta 1433 bloqueados.  ponto final de Olá poderá ACLd tooonly permitir o acesso a partir de outros recursos em Olá a mesma rede virtual.  

Outro exemplo, pontos finais confidenciais podem executar no local e ser tooAzure ligado através de um [Site a Site] [ SiteToSite] ou [Azure ExpressRoute] [ ExpressRoute] ligações.  Como resultado, apenas recursos nas redes virtuais ligadas toohello Site para Site ou ExpressRoute túneis serão pontos finais do tooaccess consegue no local.

Para todos estes cenários, as aplicações em execução no ambiente de serviço de aplicações irá ser toosecurely capaz de ligar toohello vários servidores e recursos.  Tráfego de saída de aplicações em execução num pontos finais tooprivate de ambiente de serviço de aplicações no Olá mesma rede virtual (ou ligado toohello mesma rede virtual), será apenas fluxo através de rede virtual Olá.  Pontos finais não irão fluir através de tooprivate de tráfego de saída Olá Internet pública.

Uma advertência aplica-se a tráfego toooutbound de tooendpoints um ambiente de serviço de aplicações dentro de uma rede virtual.  Ambientes do App Service não é possível aceder a pontos finais de máquinas virtuais localizadas em Olá **mesmo** como Olá ambiente de serviço de aplicações.  Isto normalmente não deve ser um problema, desde que os ambientes de serviço de aplicações são implementados para uma sub-rede reservada para utilização exclusiva por Olá apenas ambiente de serviço de aplicações.

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="outbound-connectivity-and-dns-requirements"></a>Conectividade de saída e os requisitos de DNS
Para um ambiente de serviço de aplicações toofunction corretamente, requer pontos finais de toovarious de acesso de saída. Uma lista completa das Olá pontos finais externos utilizados pelo ASE consta Olá secção "Necessárias conectividade de rede" Olá [configuração de rede para o ExpressRoute](app-service-app-service-environment-network-configuration-expressroute.md#required-network-connectivity) artigo.

Ambientes do App Service necessitam de uma infraestrutura de DNS válida configurada para a rede virtual Olá.  Se para qualquer Olá razão a configuração de DNS é alterada depois de criar um ambiente de serviço de aplicações, os programadores de podem forçar toopick um ambiente de serviço de aplicações, a configuração de DNS novo Olá.  Acionar um reinício de ambiente graduais com ícone de "Restart" Olá, localizado em Olá parte superior do ambiente de serviço de aplicações de Olá painel de gestão no portal de Olá fará com que Olá ambiente toopick a configuração de DNS novo Olá.

Também é recomendável que todos os servidores DNS personalizados Olá vnet ser configurado antes da hora anterior toocreating um ambiente de serviço de aplicações.  Se a configuração de DNS de uma rede virtual é alterada durante a criação de um ambiente de serviço de aplicações, que resultará na falha de processo de criação de ambiente de serviço de aplicações de Olá.  Um vein semelhante, se existir um servidor DNS personalizado no Olá outra extremidade de um gateway de VPN e o servidor DNS Olá é Olá inacessível ou não está disponível, também irá falhar o processo de criação do ambiente de serviço de aplicações.

## <a name="connecting-tooa-sql-server"></a>Ligar tooa do SQL Server
Uma configuração comum do SQL Server tem um ponto final à escuta na porta 1433:

![Ponto final do SQL Server][SqlServerEndpoint]

Existem duas abordagens para restringir o ponto final de toothis de tráfego:

* [Listas de controlo de acesso de rede] [ NetworkAccessControlLists] (ACLs de rede)
* [Grupos de segurança de rede][NetworkSecurityGroups]

## <a name="restricting-access-with-a-network-acl"></a>Restringir o acesso com uma ACL de rede
A porta 1433 pode ser protegida utilizando uma lista de controlo de acesso de rede.  exemplo de Olá abaixo whitelists cliente endereços originadas a partir de dentro de uma rede virtual e bloquear o acesso tooall outros clientes.

![Exemplo de lista de controlo de acesso de rede][NetworkAccessControlListExample]

Olá, todas as aplicações em execução no ambiente de serviço de aplicações na mesma rede virtual como Olá do SQL Server será a instância do SQL Server toohello de tooconnect consegue utilizar Olá **VNet interno** endereço IP para a máquina de virtual Olá do SQL Server.  

cadeia de ligação de exemplo de Olá abaixo referências hello do SQL Server utilizando o respetivo endereço IP privado.

    Server=tcp:10.0.1.6;Database=MyDatabase;User ID=MyUser;Password=PasswordHere;provider=System.Data.SqlClient

Embora a máquina virtual de Olá tem um ponto de final público bem, as tentativas de ligação com o endereço IP público Olá serão rejeitadas devido a rede de Olá ACL. 

## <a name="restricting-access-with-a-network-security-group"></a>Restringir o acesso a um grupo de segurança de rede
É uma abordagem alternativa para proteger o acesso a um grupo de segurança de rede.  Grupos de segurança de rede podem ser aplicado tooindividual virtual machines ou sub-rede tooa que contêm máquinas virtuais.

Primeiro um grupo de segurança de rede necessita de toobe criada:

    New-AzureNetworkSecurityGroup -Name "testNSGexample" -Location "South Central US" -Label "Example network security group for an app service environment"

Restringir o acesso tooonly tráfego interno de VNet é muito simple com um grupo de segurança de rede.  regras de predefinidas Olá num grupo de segurança de rede permitem apenas o acesso a partir de outros clientes de rede no Olá mesma rede virtual.

Como resultado bloquear acesso tooSQL servidor é tão simple como aplicar um grupo de segurança de rede com as predefinição regras tooeither Olá máquinas virtuais em execução do SQL Server, ou a sub-rede de Olá contendo máquinas de virtuais Olá.

exemplo de Olá abaixo aplica-se uma segurança grupo toohello contentora sub-rede da rede:

    Get-AzureNetworkSecurityGroup -Name "testNSGExample" | Set-AzureNetworkSecurityGroupToSubnet -VirtualNetworkName 'testVNet' -SubnetName 'Subnet-1'

resultado final de Olá é um conjunto de regras de segurança que bloquear o acesso externo, ao permitir o acesso interno da VNet:

![Regras de segurança de rede predefinida][DefaultNetworkSecurityRules]

## <a name="getting-started"></a>Introdução
Todos os artigos e como-a para ambientes de serviço de aplicações estão disponíveis no Olá [Leia-me para ambientes de serviço de aplicações](../app-service/app-service-app-service-environments-readme.md).

tooget começar a utilizar ambientes do App Service, consulte [introdução tooApp ambiente de serviço][IntroToAppServiceEnvironment]

Para obter mais detalhes em torno de controlar o tráfego de entrada tooyour ambiente de serviço de aplicações, consulte [controlar o tráfego de entrada tooan ambiente de serviço de aplicações][ControlInboundASE]

Para obter mais informações sobre a plataforma do App Service do Azure de Olá, consulte [App Service do Azure][AzureAppService].

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- LINKS -->
[virtualnetwork]: https://azure.microsoft.com/documentation/articles/virtual-networks-faq/
[ControlInboundTraffic]:  http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-control-inbound-traffic/
[SiteToSite]: https://azure.microsoft.com/documentation/articles/vpn-gateway-site-to-site-create/
[ExpressRoute]: http://azure.microsoft.com/services/expressroute/
[NetworkAccessControlLists]: https://azure.microsoft.com/documentation/articles/virtual-networks-acl/
[NetworkSecurityGroups]: https://azure.microsoft.com/documentation/articles/virtual-networks-nsg/
[IntroToAppServiceEnvironment]:  http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-intro/
[AzureAppService]: http://azure.microsoft.com/documentation/articles/app-service-value-prop-what-is/ 
[ControlInboundASE]:  http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-control-inbound-traffic/ 

<!-- IMAGES -->
[SqlServerEndpoint]: ./media/app-service-app-service-environment-securely-connecting-to-backend-resources/SqlServerEndpoint01.png
[NetworkAccessControlListExample]: ./media/app-service-app-service-environment-securely-connecting-to-backend-resources/NetworkAcl01.png
[DefaultNetworkSecurityRules]: ./media/app-service-app-service-environment-securely-connecting-to-backend-resources/DefaultNetworkSecurityRules01.png 
