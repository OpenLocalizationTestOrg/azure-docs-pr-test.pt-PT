---
title: "aaaGeo escala distribuídas com ambientes do App Service"
description: "Saiba como toohorizontally dimensionar aplicações ao utilizar a georreplicação distribuição com ambientes do App Service e o Traffic Manager."
services: app-service
documentationcenter: 
author: stefsch
manager: erikre
editor: 
ms.assetid: c1b05ca8-3703-4d87-a9ae-819d741787fb
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/07/2016
ms.author: stefsch
ms.openlocfilehash: 9b441f637d8b7f679b3d83240baf99b8ee57e8f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="geo-distributed-scale-with-app-service-environments"></a>Escala Distribuída Geograficamente com Ambientes de Serviço de Aplicações
## <a name="overview"></a>Descrição geral
Cenários de aplicações que requerem muito grande escala podem exceder Olá computação capacidade disponível tooa única implementação de recursos de uma aplicação.  Aplicações de voto, sporting eventos e os eventos de entretenimento televised são todos os exemplos de cenários que necessitam de escala extremamente elevada. Requisitos de grande escala podem ser cumpridos ao aumentar horizontalmente horizontalmente aplicações, com várias implementações de aplicação que está a ser efetuadas numa única região, bem como em regiões, requisitos de carga Alpine toohandle.

Os ambientes de serviço de aplicações são uma plataforma ideal para Escalamento horizontal.  Assim que tiver sido selecionada uma configuração de ambiente de serviço de aplicações que pode suportar uma taxa de pedidos conhecido, os programadores podem implementar ambientes de serviço de aplicações adicionais no "cookie cutter" forma tooattain uma capacidade de carregamento das horas de ponta pretendido.

Por exemplo, suponha uma aplicação em execução numa configuração de ambiente de serviço de aplicações foi testada toohandle K de 20 pedidos por segundo (RPS).  Se carregar das horas de ponta pretendido Olá capacidade é 100 mil RPS, cinco (5) ambientes do App Service pode ser criados e configurado tooensure Olá aplicação pode processar carga prevista máximo de Olá.

Uma vez que os clientes, normalmente, aceder a aplicações ao utilizar um domínio personalizado (ou intuitivos), a necessidade dos programadores uma aplicação de toodistribute forma pedidos em todas as instâncias de ambiente de serviço de aplicações de Olá.  Tooaccomplish uma excelente forma trata tooresolve Olá domínio personalizado utilizando um [perfil do Traffic Manager do Azure][AzureTrafficManagerProfile].  Olá Gestor de tráfego perfil pode ser configurado toopoint em todas as Olá individuais ambientes do App Service.  Gestor de tráfego processará automaticamente distribui os clientes em todos os ambientes do App Service, com base nas definições do perfil do Gestor de tráfego de Olá de balanceamento de carga Olá de Olá.  Esta abordagem funciona independentemente se todos os ambientes de serviço de aplicação Olá são implementados numa única região do Azure ou em todo o mundo implementados em várias regiões do Azure.

Além disso, uma vez que os clientes aceder a aplicações através do domínio de intuitivos Olá, os clientes são tem conhecimento do número de Olá de ambientes de serviço de aplicações em execução uma aplicação.  Como resultado os programadores podem rápida e facilmente adicionar e remover, ambientes do App Service, com base na carga de tráfego observado.

diagrama conceptual Olá abaixo ilustra uma aplicação horizontalmente ampliada em três ambientes do App Service numa única região.

![Arquitetura conceptual][ConceptualArchitecture] 

resto Olá deste tópico explica os passos de Olá envolvidos configurar uma topologia distribuída para a aplicação de exemplo de Olá com vários ambientes do App Service.

## <a name="planning-hello-topology"></a>Planear a topologia de Olá
Antes de conceção de requisitos de espaço de aplicação distribuída, ajuda a toohave algumas informações de peças antecedência.

* **Domínio personalizado para a aplicação Olá:** que é o nome de domínio personalizado de Olá que os clientes utilizarão tooaccess Olá aplicação?  Para o domínio personalizado de Olá aplicação de exemplo Olá nome é *www.scalableasedemo.com*
* **Domínio do Traffic Manager:** necessita de um nome de domínio toobe escolhido durante a criação de um [perfil do Traffic Manager do Azure][AzureTrafficManagerProfile].  Este nome será ser combinado com Olá *trafficmanager.net* sufixo tooregister uma entrada de domínio que é gerida pelo Gestor de tráfego.  Para a aplicação de exemplo de Olá, é escolhido de nome de Olá *demonstração dimensionável ase*.  Como resultado o nome de domínio completo de Olá geridas pelo Gestor de tráfego é *demo.trafficmanager.net dimensionável ase*.
* **Estratégia de dimensionamento Olá aplicação os requisitos de espaço:** Olá aplicação os requisitos de espaço serem distribuídos pelos vários ambientes do App Service numa única região?  Várias regiões?  Uma combinação-e-correspondência de ambas as abordagens?  Decisão de Olá deve ser baseada no onde o tráfego de cliente será têm origem, bem como rest Olá bem de uma aplicação que suporta a infraestrutura de back-end pode dimensionar as expectativas.  Por exemplo, com uma aplicação sem monitorização de estado de 100%, uma aplicação pode ser extremamente escalada utilizando uma combinação de vários ambientes do App Service por região do Azure, multiplicado pelo ambientes do App Service implementado em várias regiões do Azure.  Com 15 + pública regiões do Azure toochoose disponíveis do, os clientes verdadeiramente podem criar requisitos de espaço de aplicação de hiper escala em todo o mundo.  Para a aplicação de exemplo de Olá utilizada para este artigo, três ambientes do App Service foram criados numa única região do Azure (Sul Central US).
* **Convenção de nomenclatura para Olá ambientes do App Service:** cada ambiente de serviço de aplicações requer um nome exclusivo.  Para além de um ou dois ambientes do App Service é útil toohave uma convenção de nomenclatura toohelp identificar cada ambiente de serviço de aplicações.  Para a aplicação de exemplo de Olá foi utilizada uma convenção de nomenclatura simple.  Olá os nomes dos ambientes de serviço de aplicação Olá três são *fe1ase*, *fe2ase*, e *fe3ase*.
* **Convenção de nomenclatura para aplicações de Olá:** uma vez que serão implementadas várias instâncias da aplicação Olá, um nome é necessária para cada instância da aplicação Olá implementado.  Uma funcionalidade reduzida conhecido mas muito conveniente de ambientes do App Service é essa Olá mesmo nome de aplicação pode ser utilizado em vários ambientes do App Service.  Uma vez que cada ambiente de serviço de aplicações têm um sufixo de domínio único, os programadores podem escolher toore utilize Olá exato mesmo nome de aplicação em cada ambiente.  Por exemplo um programador pode ter aplicações com o nome da seguinte forma: *myapp.foo1.p.azurewebsites.net*, *myapp.foo2.p.azurewebsites.net*, *myapp.foo3.p.azurewebsites.net*, etc.  Apesar da aplicação de exemplo de Olá cada instância da aplicação também tem um nome exclusivo.  Olá os nomes de instâncias da aplicação utilizados são *webfrontend1*, *webfrontend2*, e *webfrontend3*.

## <a name="setting-up-hello-traffic-manager-profile"></a>Configurar Olá perfil do Traffic Manager
Assim que forem implementadas várias instâncias de uma aplicação em vários ambientes do App Service, instâncias de aplicações individuais Olá podem ser registadas com o Gestor de tráfego.  Para a aplicação de exemplo de Olá um Gestor de tráfego de perfil é necessária para *demo.trafficmanager.net dimensionável ase* que pode encaminhar clientes tooany de Olá seguir implementado aplicação instâncias:

* **webfrontend1.fe1ase.p.azurewebsites.NET:** Olá, uma instância da aplicação de exemplo de Olá implementada num ambiente de serviço de aplicações primeiro.
* **webfrontend2.fe2ase.p.azurewebsites.NET:** Olá, uma instância da aplicação de exemplo de Olá implementada num ambiente de serviço de aplicações segundo.
* **webfrontend3.fe3ase.p.azurewebsites.NET:** Olá, uma instância da aplicação de exemplo de Olá implementada num ambiente de serviço de aplicações terceiro.

Olá tooregister de forma mais fácil múltiplos App Service do Azure pontos finais, todos os em execução no Olá **mesmo** região do Azure, é com Olá Powershell [suporte do Gestor de tráfego do Azure Resource Manager] [ ARMTrafficManager].  

Step-by-Olá primeiro passo é toocreate um perfil do Traffic Manager do Azure.  código de Olá abaixo mostra como o perfil de Olá foi criado para a aplicação de exemplo de Olá:

    $profile = New-AzureTrafficManagerProfile –Name scalableasedemo -ResourceGroupName yourRGNameHere -TrafficRoutingMethod Weighted -RelativeDnsName scalable-ase-demo -Ttl 30 -MonitorProtocol HTTP -MonitorPort 80 -MonitorPath "/"

Repare como Olá *RelativeDnsName* parâmetro foi definido demasiado*demonstração dimensionável ase*.  Isto é Olá como nome de domínio *demo.trafficmanager.net dimensionável ase* são criados e associados a um perfil do Traffic Manager.

Olá *TrafficRoutingMethod* parâmetro define a política do Traffic Manager irá utilizar toodetermine como cliente toospread carregar em todos os pontos finais de disponíveis Olá de balanceamento de carga Olá.  No Olá exemplo *Weighted* método escolhido.  Isto irá resultar em pedidos de cliente que está a ser distribuídos por todos os pontos finais de aplicação Olá registado com base em ponderações relativo Olá associadas a cada ponto final. 

Com o perfil de Olá criado, cada instância da aplicação é adicionada toohello perfil como um ponto final do Azure nativo.  código de Olá abaixo obtém uma aplicação de web de front-end de tooeach de referência e, em seguida, adiciona cada aplicação como um ponto final do Gestor de tráfego através de Olá *TargetResourceId* parâmetro.

    $webapp1 = Get-AzureRMWebApp -Name webfrontend1
    Add-AzureTrafficManagerEndpointConfig –EndpointName webfrontend1 –TrafficManagerProfile $profile –Type AzureEndpoints -TargetResourceId $webapp1.Id –EndpointStatus Enabled –Weight 10

    $webapp2 = Get-AzureRMWebApp -Name webfrontend2
    Add-AzureTrafficManagerEndpointConfig –EndpointName webfrontend2 –TrafficManagerProfile $profile –Type AzureEndpoints -TargetResourceId $webapp2.Id –EndpointStatus Enabled –Weight 10

    $webapp3 = Get-AzureRMWebApp -Name webfrontend3
    Add-AzureTrafficManagerEndpointConfig –EndpointName webfrontend3 –TrafficManagerProfile $profile –Type AzureEndpoints -TargetResourceId $webapp3.Id –EndpointStatus Enabled –Weight 10

    Set-AzureTrafficManagerProfile –TrafficManagerProfile $profile

Repare como há uma chamada de demasiado*adicionar AzureTrafficManagerEndpointConfig* para cada instância de aplicações individuais.  Olá *TargetResourceId* parâmetro em cada comando do Powershell faz referência a um dos três instâncias de aplicação implementada Olá.  Olá perfil do Traffic Manager serão distribuídos carga por todos os pontos três finais registados no perfil de Olá.

Olá todas Olá três pontos finais utilizam o mesmo valor (10) para Olá *ponderação* parâmetro.  Isto resulta no Gestor de tráfego pedidos de cliente propagando-se em todas as instâncias da aplicação de três relativamente uniformemente. 

## <a name="pointing-hello-apps-custom-domain-at-hello-traffic-manager-domain"></a>Domínio personalizado da aplicação Olá indo em Olá domínio do Traffic Manager
Olá último passo necessário é o domínio personalizado de Olá toopoint da aplicação Olá no domínio do Gestor de tráfego Olá.  Na aplicação de exemplo de Olá significa apontar *www.scalableasedemo.com* em *demo.trafficmanager.net dimensionável ase*.  Este passo necessita de toobe foi concluída com Olá de domínios que gere o domínio personalizado Olá.  

Utilizar as ferramentas de gestão do domínio sua entidade de registo, um toobe de necessidades de registos CNAME que pontos Olá domínio personalizado criado no domínio do Gestor de tráfego Olá.  imagem de Olá abaixo mostra um exemplo do aspeto esta configuração de CNAME:

![CNAME para o domínio personalizado][CNAMEforCustomDomain] 

Apesar de não abrangidas neste tópico, lembre-se de que cada instância de aplicações individuais precisa de domínio do Olá de toohave personalizado registado com o mesmo assim.  Caso contrário, se um pedido faz com que instância de aplicação tooan e aplicação Olá não tem o domínio personalizado Olá registado com a aplicação Olá, pedido Olá irá falhar.  

Olá este exemplo domínio personalizado é *www.scalableasedemo.com*, e cada instância da aplicação tem o domínio personalizado Olá associado à mesma.

![Domínio Personalizado][CustomDomain] 

Para um resumo de registar um domínio personalizado com aplicações do App Service do Azure, consulte Olá seguinte artigo [registar domínios personalizados][RegisterCustomDomain].

## <a name="trying-out-hello-distributed-topology"></a>Experimentar Olá topologia distribuída
Olá resultado final da configuração de DNS e o Traffic Manager Olá é que os pedidos para *www.scalableasedemo.com* irá fluir pelo Olá seguinte sequência:

1. Um browser ou o dispositivo irá efetuar uma pesquisa de DNS *www.scalableasedemo.com*
2. Olá entrada CNAME no registo de domínios Olá faz com que Olá DNS pesquisa toobe redirecionado tooAzure Gestor de tráfego.
3. É efetuada uma pesquisa de DNS *demo.trafficmanager.net dimensionável ase* contra um dos servidores de DNS do Gestor de tráfego do Azure Olá.
4. Com base na política de balanceamento de carga Olá (Olá *TrafficRoutingMethod* parâmetro utilizado anteriormente durante a criação de perfil do Traffic Manager Olá), Gestor de tráfego irá selecionar uma das Olá configurados pontos finais e devolve Olá FQDN do que browser de toohello de ponto final ou dispositivo.
5. Uma vez que Olá FQDN do ponto final de Olá Olá Url de uma instância de aplicação em execução no ambiente de serviço de aplicações, hello browser ou o dispositivo irá perguntar-um servidor DNS do Microsoft Azure tooresolve Olá endereço IP tooan FQDN. 
6. browser de Olá ou dispositivo irá enviar o endereço IP do Olá HTTP/S pedido toohello.  
7. pedido de Olá conseguirá obter uma das instâncias de aplicação Olá em execução dos Olá ambientes do App Service.

Olá consola imagem abaixo mostra uma pesquisa de DNS domínio personalizado com êxito ao resolver tooan instância da aplicação da aplicação de exemplo Olá em execução dos exemplo Olá três ambientes do App Service (neste caso Olá segundo de Olá três ambientes do App Service):

![Pesquisa de DNS][DNSLookup] 

## <a name="additional-links-and-information"></a>Informações e hiperligações adicionais
Todos os artigos e como-a para ambientes de serviço de aplicações estão disponíveis no Olá [Leia-me para ambientes de serviço de aplicações](../app-service/app-service-app-service-environments-readme.md).

A documentação sobre Olá Powershell [suporte do Gestor de tráfego do Azure Resource Manager][ARMTrafficManager].  

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- LINKS -->
[AzureTrafficManagerProfile]: ../traffic-manager/traffic-manager-manage-profiles.md
[ARMTrafficManager]: ../traffic-manager/traffic-manager-powershell-arm.md
[RegisterCustomDomain]: app-service-web-tutorial-custom-domain.md


<!-- IMAGES -->
[ConceptualArchitecture]: ./media/app-service-app-service-environment-geo-distributed-scale/ConceptualArchitecture-1.png
[CNAMEforCustomDomain]:  ./media/app-service-app-service-environment-geo-distributed-scale/CNAMECustomDomain-1.png
[DNSLookup]:  ./media/app-service-app-service-environment-geo-distributed-scale/DNSLookup-1.png
[CustomDomain]:  ./media/app-service-app-service-environment-geo-distributed-scale/CustomDomain-1.png 
