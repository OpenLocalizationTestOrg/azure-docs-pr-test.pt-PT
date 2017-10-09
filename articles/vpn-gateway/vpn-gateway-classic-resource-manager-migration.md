---
title: "aaaVPN Gateway clássico tooResource Gestor de migração | Microsoft Docs"
description: "Esta página fornece uma descrição geral de Olá VPN Gateway clássico tooResource migração do gestor."
documentationcenter: na
services: vpn-gateway
author: amsriva
manager: rossort
editor: amsriva
ms.assetid: caa8eb19-825a-4031-8b49-18fbf3ebc04e
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/02/2017
ms.author: amsriva
ms.openlocfilehash: c1d84bf5315224c5c8faac53d7957b496ed205ed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="vpn-gateway-classic-tooresource-manager-migration"></a>Gateway de VPN clássico tooResource Gestor de migração
Gateways de VPN agora podem ser migrados do modelo de implementação do Gestor de tooResource clássico. Pode ler mais sobre o Azure Resource Manager [funcionalidades e vantagens](../azure-resource-manager/resource-group-overview.md). Neste artigo, vamos detalhe como toomigrate de implementações clássicas toonewer Gestor de recursos com base em modelo. 

Gateways de VPN são migrados como parte da migração de VNet do Gestor de tooResource clássico. Esta migração é efetuada uma VNet a uma hora. Não há nenhum requisito adicional em termos de toomigration ferramentas ou de pré-requisitos. Passos de migração são idênticos tooexisting VNet migração e estão documentados em [página de migração de recursos IaaS](../virtual-machines/windows/migration-classic-resource-manager-ps.md). Não há nenhum período de indisponibilidade do caminho de dados durante a migração e, por conseguinte, cargas de trabalho existentes continuaria toofunction sem perda de conectividade no local durante a migração. endereço IP público Olá associado ao gateway de VPN Olá não altera durante o processo de migração de Olá. Isto implica que não terá tooreconfigure o router no local depois de concluída a migração de Olá.  

modelo de Olá no Gestor de recursos é diferente do modelo clássico e é composto de gateways de rede virtual, de gateways de rede local e de recursos de ligação. Estes representam Olá próprio gateway de VPN, Olá site local representando no espaço de endereços no local, a conectividade entre Olá dois, respetivamente. Depois de concluída a migração não seria disponíveis no modelo clássico seus gateways e todas as operações de gestão em gateways de rede virtual, gateways de rede local e objetos de ligação tem de ser efetuadas utilizando o modelo do Resource Manager.

## <a name="supported-scenarios"></a>Cenários suportados
Cenários mais comuns de conectividade VPN estão abrangidos pelos tooResource clássico migração do gestor. os cenários de Olá suportado incluem-

* Conectividade toosite ponto
* Conectividade de toosite de site com o Gateway de VPN ligado tooon localização de local
* VNet tooVNet conectividade entre duas VNets com gateways de VPN
* Várias VNets ligado toosame na localização no local
* Conetividade multilocal
* Imposição do túnel ativada VNets

Os cenários que não são suportados incluem-  

* VNet com o Gateway do ExpressRoute e o Gateway de VPN não é atualmente suportada.
* Cenários de trânsito onde as extensões de VM são servidores ligados tooon local. Limitações de conectividade VPN de trânsito detalhadas abaixo.

> [!NOTE]
> Validação de CIDR no modelo do Resource Manager é mais estrita de Olá um no modelo clássico. Antes de migrar Certifique-se de que os intervalos de endereços clássico fornecidos está em conformidade com formato CIDR toovalid antes de iniciar a migração de Olá. CIDR possa ser validada utilizando qualquer validações CIDR comuns. VNet ou sites locais com intervalos CIDR inválidos quando migrada resultaria num Estado com falhas.
> 
> 

## <a name="vnet-toovnet-connectivity-migration"></a>Migração de conectividade de tooVNet VNet
VNet tooVNet conectividade no clássico foi alcançada através da criação de um site local representação de Olá ligado VNet. Os clientes foram toocreate necessário dois sites locais que representado Olá duas VNets que necessários toobe ligadas em conjunto. Estes foram, em seguida, toohello ligado correspondente VNets com conectividade de tooestablish de túnel IPsec entre Olá duas VNets. Este modelo tem desafios de capacidade de gestão, uma vez que as alterações de intervalo de endereços na um VNet também têm de ser mantidas em representação de local site correspondente Olá. No modelo do Resource Manager esta solução já não é necessária. ligação de Olá entre duas VNets podem ser diretamente de Olá conseguido utilizando o tipo de ligação 'Vnet2Vnet' no recurso de ligação. 

![Captura de ecrã da VNet tooVNet migração.](./media/vpn-gateway-migration/migration1.png)

Durante a migração de VNet detectarmos que Olá entidade ligada o gateway de VPN da VNet toocurrent é outra VNet e certifique-se de que depois de concluída a migração de ambas as VNets, já não verá dois sites locais que representa Olá outra VNet. Olá o modelo clássico de dois gateways de VPN, os dois sites locais e duas ligações entre eles é transformada tooResource modelo Manager com dois gateways de VPN e duas ligações do tipo Vnet2Vnet.

## <a name="transit-vpn-connectivity"></a>Conectividade VPN de trânsito
Pode configurar gateways de VPN numa topologia de forma a que conectividade no local para uma VNet é conseguida através da ligação tooanother VNet que está diretamente ligado tooon local. Este é o trânsito conectividade VPN onde instâncias na primeira VNet são recursos ligados tooon local através do gateway de VPN do trânsito toohello na VNet ligado que está diretamente ligado tooon local. tooachieve esta configuração no modelo de implementação clássica, terá de toocreate num site local que foi agregada prefixos que representa o espaço de endereços ambas Olá ligado VNet e no local. Este site local representational é então ligado toohello VNet tooachieve trânsito conectividade. Este modelo clássico tem também semelhante desafios de capacidade de gestão, uma vez que qualquer alteração no intervalo de endereços no local também têm de ser mantida no site local Olá que representa a agregação de Olá de VNet e no local. Introdução de suporte BGP nos gateways de Gestor de recursos suportados simplifica a capacidade de gestão, uma vez que hello gateways ligados podem aprendem rotas no local sem tooprefixes modificação manual.

![Captura de ecrã do cenário de encaminhamento de trânsito.](./media/vpn-gateway-migration/migration2.png)

Uma vez que vamos transformar VNet tooVNet conectividade sem necessidade de sites locais, cenário de trânsito Olá perde a conectividade de no local para a VNet que está local tooon indiretamente ligado. Olá perda de conectividade pode ser mitigada no Olá seguintes duas formas, depois de concluída a migração - 

* Ative o BGP nos gateways de VPN estiverem ligados em conjunto e tooon local. Ativar o BGP restaura a conectividade sem qualquer alteração de configuração desde rotas aprendidas e anunciadas entre os gateways de VNet. Tenha em atenção que a opção de BGP só está disponível no SKUs padrão e planos superiores.
* Estabelece uma ligação explícita do gateway de rede local toohello afetado VNet que representa a localização no local. Isto seria também exigir a alteração da configuração no toocreate de router no local de Olá e configurar o túnel IPsec de Olá.

## <a name="next-steps"></a>Passos seguintes
Depois de aprender mais sobre o suporte de migração de gateway VPN, aceda demasiado[plataforma suportada a migração de recursos IaaS do clássico tooResource Manager](../virtual-machines/windows/migration-classic-resource-manager-ps.md) tooget foi iniciado.

