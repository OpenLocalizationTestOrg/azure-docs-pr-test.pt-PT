---
title: "Ligar uma rede virtual de tooan circuito do ExpressRoute: PowerShell: clássico: Azure | Microsoft Docs"
description: "Este documento fornece uma descrição geral de como toolink virtual redes (VNets) tooExpressRoute circuitos utilizando o modelo de implementação clássica Olá e o PowerShell."
services: expressroute
documentationcenter: na
author: ganesr
manager: carmonm
editor: 
tags: azure-service-management
ms.assetid: 9b53fd72-9b6b-4844-80b9-4e1d54fd0c17
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/28/2017
ms.author: ganesr
ms.openlocfilehash: 6b8a01dcd4bbb9618ec3dd438cf0107538fb2a7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="connect-a-virtual-network-tooan-expressroute-circuit-using-powershell-classic"></a>Ligar um circuito de ExpressRoute de tooan de rede virtual com o PowerShell (clássica)
> [!div class="op_single_selector"]
> * [Portal do Azure](expressroute-howto-linkvnet-portal-resource-manager.md)
> * [PowerShell](expressroute-howto-linkvnet-arm.md)
> * [CLI do Azure](howto-linkvnet-cli.md)
> * [Vídeo - portal do Azure](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-connection-between-your-vpn-gateway-and-expressroute-circuit)
> * [PowerShell (clássico)](expressroute-howto-linkvnet-classic.md)
>

Este artigo ajuda-o ligação circuitos do ExpressRoute redes virtuais (VNets) tooAzure utilizando o modelo de implementação clássica Olá e o PowerShell. Redes virtuais podem ser na Olá mesma subscrição ou pode fazer parte de outra subscrição.

[!INCLUDE [expressroute-classic-end-include](../../includes/expressroute-classic-end-include.md)]

**Acerca dos modelos de implementação do Azure**

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

## <a name="configuration-prerequisites"></a>Pré-requisitos da configuração
1. Tem a versão mais recente do Olá de módulos do Azure PowerShell Olá. Pode transferir módulos do PowerShell mais recentes Olá da Olá secção PowerShell Olá [página de transferências do Azure](https://azure.microsoft.com/downloads/). Siga as instruções de Olá em [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview) para obter orientações passo a passo sobre como tooconfigure os módulos do PowerShell do Azure do computador toouse Olá.
2. Terá de tooreview Olá [pré-requisitos](expressroute-prerequisites.md), [requisitos de encaminhamento](expressroute-routing.md), e [fluxos de trabalho](expressroute-workflows.md) antes de iniciar a configuração.
3. Deve ter um circuito ExpressRoute ativo.
   * Siga as instruções de Olá demasiado[criar um circuito ExpressRoute](expressroute-howto-circuit-classic.md) e solicite ao seu fornecedor de conectividade ativar circuito Olá.
   * Certifique-se de que tem o peering privado do Azure configurada para o seu circuito. Consulte Olá [configurar encaminhamento](expressroute-howto-routing-classic.md) artigo para obter instruções de encaminhamento.
   * Certifique-se de que o peering privado do Azure está configurado e peering de BGP Olá entre a rede e a Microsoft está a funcionar, de modo a que pode ativar a conetividade de ponto a ponto.
   * Tem de ter uma rede virtual e um gateway de rede virtual criada e totalmente aprovisionado. Siga as instruções de Olá demasiado[configurar uma rede virtual para o ExpressRoute](expressroute-howto-vnet-portal-classic.md).

Pode ligar a cópia de segurança too10 redes virtuais tooan circuito ExpressRoute. Todas as redes virtuais tem de constar Olá mesma região geopolítica. Pode associar um grande número de redes virtuais tooyour circuito ExpressRoute ou ligar redes virtuais que se encontrem noutras regiões geopolíticas, se tiver ativado o suplemento premium do ExpressRoute de Olá. Verifique Olá [FAQ](expressroute-faqs.md) para obter mais detalhes sobre o suplemento do Olá premium.

## <a name="connect-a-virtual-network-in-hello-same-subscription-tooa-circuit"></a>Ligar uma rede virtual no Olá mesmo circuito tooa de subscrição
Pode ligar uma rede virtual de tooan circuito ExpressRoute utilizando o seguinte cmdlet de Olá. Certifique-se de que gateway de rede virtual Olá é criado e está pronta para a ligação antes de executar o cmdlet Olá.

    New-AzureDedicatedCircuitLink -ServiceKey "*****************************" -VNetName "MyVNet"
    Provisioned

## <a name="connect-a-virtual-network-in-a-different-subscription-tooa-circuit"></a>Ligar uma rede virtual no circuito de tooa subscrição diferente
Pode partilhar um circuito ExpressRoute entre várias subscrições. Olá figura a seguir mostra um simples schematic de funciona como partilha para circuitos do ExpressRoute entre várias subscrições.

Cada uma das nuvens mais pequenas de Olá na nuvem grande Olá é utilizado toorepresent subscrições que pertencem os departamentos de toodifferent dentro de uma organização. Cada um dos departamentos de Olá dentro da organização Olá pode utilizar as seus próprios subscrição para implementar os seus serviços - mas departamentos Olá pode partilhar uma única ExpressRoute circuito tooconnect back tooyour rede no local. Um único departamento (neste exemplo: IT) pode ter o circuito de ExpressRoute Olá. Outras subscrições dentro da organização Olá podem utilizar o circuito de ExpressRoute Olá.

> [!NOTE]
> Custos de largura de banda e conectividade de circuito dedicado de Olá será o proprietário de circuito de ExpressRoute toohello aplicados. Todas as redes virtuais partilham Olá mesma largura de banda.
> 
> 

![Conectividade entre subscrições](./media/expressroute-howto-linkvnet-classic/cross-subscription.png)

### <a name="administration"></a>Administração
Olá *proprietário do circuito* é Olá administrador/coadministrador da subscrição Olá que Olá ExpressRoute é criar circuito. Olá proprietário do circuito pode autorizar administradores/coadministrators de outras subscrições, referidos tooas *circuito utilizadores*, toouse Olá dedicado circuito que possuem. Circuito os utilizadores podem de circuito de ExpressRoute toouse autorizados Olá organização ligação de rede virtual do Olá no respetivo toohello subscrição circuito ExpressRoute depois estiverem autorizadas.

proprietário do circuito Olá tem as autorizações Olá energia toomodify e revogar em qualquer altura. Revogar uma autorização resultará em todas as ligações seja eliminadas da subscrição Olá cujo acesso foi revogado.

### <a name="circuit-owner-operations"></a>Operações de proprietário do circuito

**Criar uma autorização**

Olá proprietário do circuito autoriza Olá os administradores de outras subscrições toouse Olá especificado circuito. No seguinte exemplo de Olá, o administrador de Olá do circuito Olá (Contoso TI) permite ao administrador Olá de outra subscrição (Dev-teste) toolink segurança circuito de toohello tootwo redes virtuais. administrador de TI da Contoso Olá permite isto, especificando o ID de teste de desenvolvimento Microsoft Olá. cmdlet de Olá não enviar correio eletrónico toohello especificado ID da Microsoft. tem de proprietário do circuito Olá tooexplicitly notificar Olá outro proprietário da subscrição que Olá autorização está concluído.

    New-AzureDedicatedCircuitLinkAuthorization -ServiceKey "**************************" -Description "Dev-Test Links" -Limit 2 -MicrosoftIds 'devtest@contoso.com'

    Description         : Dev-Test Links
    Limit               : 2
    LinkAuthorizationId : **********************************
    MicrosoftIds        : devtest@contoso.com
    Used                : 0

**Rever autorizações**

proprietário do circuito Olá pode rever todas as autorizações que são emitidas sobre um determinado circuito executando Olá seguinte cmdlet:

    Get-AzureDedicatedCircuitLinkAuthorization -ServiceKey: "**************************"

    Description         : EngineeringTeam
    Limit               : 3
    LinkAuthorizationId : ####################################
    MicrosoftIds        : engadmin@contoso.com
    Used                : 1

    Description         : MarketingTeam
    Limit               : 1
    LinkAuthorizationId : @@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
    MicrosoftIds        : marketingadmin@contoso.com
    Used                : 0

    Description         : Dev-Test Links
    Limit               : 2
    LinkAuthorizationId : &&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&
    MicrosoftIds        : salesadmin@contoso.com
    Used                : 2


**Atualizar autorizações**

proprietário do circuito Olá pode modificar autorizações utilizando Olá seguinte cmdlet:

    Set-AzureDedicatedCircuitLinkAuthorization -ServiceKey "**************************" -AuthorizationId "&&&&&&&&&&&&&&&&&&&&&&&&&&&&"-Limit 5

    Description         : Dev-Test Links
    Limit               : 5
    LinkAuthorizationId : &&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&
    MicrosoftIds        : devtest@contoso.com
    Used                : 0


**Eliminar autorizações**

proprietário do circuito Olá pode revogar/eliminar utilizador de toohello autorizações executando Olá seguinte cmdlet:

    Remove-AzureDedicatedCircuitLinkAuthorization -ServiceKey "*****************************" -AuthorizationId "###############################"


### <a name="circuit-user-operations"></a>Operações de utilizador do circuito

**Rever autorizações**

utilizador do circuito Olá pode rever autorizações utilizando Olá seguinte cmdlet:

    Get-AzureAuthorizedDedicatedCircuit

    Bandwidth                        : 200
    CircuitName                      : ContosoIT
    Location                         : Washington DC
    MaximumAllowedLinks              : 2
    ServiceKey                       : &&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Status                           : Enabled
    UsedLinks                        : 0

**Resgatar autorizações de ligações**

utilizador do circuito Olá pode executar Olá seguintes cmdlet tooredeem uma autorização de ligação:

    New-AzureDedicatedCircuitLink –servicekey "&&&&&&&&&&&&&&&&&&&&&&&&&&" –VnetName 'SalesVNET1'

    State VnetName
    ----- --------
    Provisioned SalesVNET1

Execute este comando na subscrição Olá recentemente ligado para a rede virtual Olá:

    New-AzureDedicatedCircuitLink -ServiceKey "*****************************" -VNetName "MyVNet"

## <a name="next-steps"></a>Passos seguintes
Para obter mais informações sobre o ExpressRoute, consulte Olá [FAQ do ExpressRoute](expressroute-faqs.md).

