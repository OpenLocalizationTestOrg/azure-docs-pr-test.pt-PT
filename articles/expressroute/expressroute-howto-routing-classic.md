---
title: "Como tooconfigure encaminhamento (peering) para um circuito ExpressRoute: Azure: clássica | Microsoft Docs"
description: "Este artigo explica Olá passos para criar e aprovisionar Olá privado, público e peering da Microsoft de um circuito ExpressRoute. Este artigo mostra também como estado de Olá toocheck, atualizar ou eliminar peerings no seu circuito."
documentationcenter: na
services: expressroute
author: ganesr
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: a4bd39d2-373a-467a-8b06-36cfcc1027d2
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/21/2017
ms.author: ganesr;cherylmc
ms.openlocfilehash: dc5bcc4b86c3bc965a88281b6c2a660f3bc58eb1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-modify-peering-for-an-expressroute-circuit-classic"></a>Criar e modificar o peering de um circuito de ExpressRoute (clássica)
> [!div class="op_single_selector"]
> * [Portal do Azure](expressroute-howto-routing-portal-resource-manager.md)
> * [PowerShell](expressroute-howto-routing-arm.md)
> * [CLI do Azure](howto-routing-cli.md)
> * [Vídeo - privada peering](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-azure-private-peering-for-your-expressroute-circuit)
> * [Vídeo - peering público](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-azure-public-peering-for-your-expressroute-circuit)
> * [Vídeo - peering da Microsoft](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-microsoft-peering-for-your-expressroute-circuit)
> * [PowerShell (clássico)](expressroute-howto-routing-classic.md)
> 

Este artigo explica-lhe Olá passos toocreate e gerir a configuração de encaminhamento para um circuito ExpressRoute com o PowerShell e Olá modelo de implementação clássica. passos de Olá abaixo também irão mostrar como toocheck Olá Estado, atualizar, ou eliminar e retirar o aprovisionamento do peerings para um circuito ExpressRoute.

[!INCLUDE [expressroute-classic-end-include](../../includes/expressroute-classic-end-include.md)]

**Acerca dos modelos de implementação do Azure**

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]


## <a name="configuration-prerequisites"></a>Pré-requisitos da configuração
* Terá a versão mais recente do Olá do Olá cmdlets do PowerShell de gestão de serviço do Azure (SM). Para obter mais informações, consulte [introdução aos cmdlets do Azure PowerShell](/powershell/azure/overview).  
* Certifique-se de que reviu Olá [pré-requisitos](expressroute-prerequisites.md) página Olá [requisitos de encaminhamento](expressroute-routing.md) página e Olá [fluxos de trabalho](expressroute-workflows.md) página antes de iniciar a configuração.
* Deve ter um circuito ExpressRoute ativo. Siga as instruções de Olá demasiado[criar um circuito ExpressRoute](expressroute-howto-circuit-classic.md) e ter circuito Olá ativado pelo seu fornecedor de conectividade antes de continuar. Olá circuito ExpressRoute tem de ser num Estado aprovisionado e ativado para si toobe toorun capaz de Olá cmdlets descritos abaixo.

> [!IMPORTANT]
> Estas instruções aplicam-se apenas toocircuits criados com fornecedores de serviços de oferta de serviços de conectividade de camada 2. Se estiver a utilizar um fornecedor de serviço que oferece serviços geridos de Camada 3 (normalmente, um VPN de IP, como MPLS), o seu fornecedor de conectividade irá configurar e gerir encaminhamento por si.
> 
> 

Pode configurar um, dois ou todos os três peerings (Azure privado, Azure público e Microsoft) para um circuito ExpressRoute. Pode configurar peerings em qualquer ordem que escolha. No entanto, tem de se certificar de que concluir configuração Olá cada peering, um de cada vez.


### <a name="log-in-tooyour-azure-account-and-select-a-subscription"></a>Inicie sessão no tooyour conta do Azure e selecionar uma subscrição
1. Abra a consola do PowerShell com direitos elevados e ligue tooyour conta. Utilize Olá toohelp de exemplo, ligar os seguintes:

        Login-AzureRmAccount

2. Verifique Olá subscrições para a conta de Olá.

        Get-AzureRmSubscription

3. Se tiver mais do que uma subscrição, selecione a subscrição de Olá que pretende que o toouse.

        Select-AzureRmSubscription -SubscriptionName "Replace_with_your_subscription_name"

4. Em seguida, utilize Olá seguintes cmdlet tooadd tooPowerShell sua subscrição do Azure para o modelo de implementação clássica Olá.

        Add-AzureAccount


## <a name="azure-private-peering"></a>Peering privado do Azure
Esta secção fornece instruções sobre como toocreate, obter, atualizar e eliminar Olá configuração do peering privado do Azure para um circuito ExpressRoute. 

### <a name="toocreate-azure-private-peering"></a>toocreate peering privado do Azure
1. **Importe o módulo do PowerShell de Olá para o ExpressRoute.**
   
    Tem de importar módulos do Azure e ExpressRoute Olá para a sessão do PowerShell Olá no toostart ordem utilizando cmdlets do ExpressRoute Olá. Seguinte Olá executar comandos tooimport Olá do Azure e ExpressRoute os módulos para a sessão de PowerShell Olá.  
   
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\Azure.psd1'
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\ExpressRoute\ExpressRoute.psd1'
2. **Crie um circuito ExpressRoute.**
   
    Siga Olá instruções toocreate um [circuito ExpressRoute](expressroute-howto-circuit-classic.md) e solicite ao fornecedor de conectividade Olá. Se o seu fornecedor de conectividade oferecer serviços geridos de camada 3, pode pedir o tooenable de fornecedor de conectividade para si de peering privado do Azure. Nesse caso, não terá das instruções de toofollow indicadas nas secções seguintes Olá. No entanto, se o seu fornecedor de conectividade não gerir encaminhamento por si, depois de criar o seu circuito, siga as instruções de Olá abaixo. 
3. **Verifique tooensure de circuito de ExpressRoute Olá que está aprovisionado.**
   
    Verifique primeiro toosee se Olá circuito ExpressRoute está aprovisionado e também ativado. Veja o exemplo de Olá abaixo.
   
        PS C:\> Get-AzureDedicatedCircuit -ServiceKey "*********************************"
   
        Bandwidth                        : 200
        CircuitName                      : MyTestCircuit
        Location                         : Silicon Valley
        ServiceKey                       : *********************************
        ServiceProviderName              : equinix
        ServiceProviderProvisioningState : Provisioned
        Sku                              : Standard
        Status                           : Enabled
   
    Certifique-se de que o circuito Olá mostra como aprovisionado e ativado. Se não, funciona com a sua tooget do fornecedor de conectividade do Estado do circuito toohello necessário e o estado.
   
        ServiceProviderProvisioningState : Provisioned
        Status                           : Enabled
4. **Configure o peering privado do Azure para o circuito Olá.**
   
    Certifique-se de que tem Olá seguintes itens antes de continuar com os passos seguintes Olá:
   
   * Um /30 sub-rede para a ligação primária Olá. Esta não pode fazer parte de qualquer espaço de endereço reservado para redes virtuais.
   * Um /30 sub-rede para a ligação secundária Olá. Esta não pode fazer parte de qualquer espaço de endereço reservado para redes virtuais.
   * Um tooestablish de ID de VLAN válido este peering. Certifique-se de que nenhum outro peering no circuito de Olá utiliza Olá mesmo ID de VLAN.
   * Número AS para peering. Pode utilizar números AS de 2 e 4 bytes. Pode utilizar um número AS privado para este peering. Assegure que não está a utilizar 65515.
   * Um hash MD5 se optar por toouse um. **Isto é opcional**.
     
    Pode executar Olá seguir tooconfigure cmdlet peering privado do Azure para o seu circuito.
     
        Novo AzureBGPPeering - AccessType privada - ServiceKey "***" - PrimaryPeerSubnet "10.0.0.0/30" - SecondaryPeerSubnet "10.0.0.4/30" - PeerAsn 1234 - VlanId 100
     
    Pode utilizar o cmdlet Olá abaixo se optar por toouse um hash MD5.
     
        Novo AzureBGPPeering - AccessType privada - ServiceKey "***" - PrimaryPeerSubnet "10.0.0.0/30" - SecondaryPeerSubnet "10.0.0.4/30" - PeerAsn 1234 - VlanId 100 - SharedKey "A1B2C3D4"
     
     > [!IMPORTANT]
     > Assegure que especifica o seu número AS como ASN de peering, não cliente ASN.
     > 
     > 

### <a name="tooview-azure-private-peering-details"></a>tooview detalhes de peering privado do Azure
Pode obter os detalhes de configuração utilizando o seguinte cmdlet de Olá

    Get-AzureBGPPeering -AccessType Private -ServiceKey "*********************************"

    AdvertisedPublicPrefixes       : 
    AdvertisedPublicPrefixesState  : Configured
    AzureAsn                       : 12076
    CustomerAutonomousSystemNumber : 
    PeerAsn                        : 1234
    PrimaryAzurePort               : 
    PrimaryPeerSubnet              : 10.0.0.0/30
    RoutingRegistryName            : 
    SecondaryAzurePort             : 
    SecondaryPeerSubnet            : 10.0.0.4/30
    State                          : Enabled
    VlanId                         : 100


### <a name="tooupdate-azure-private-peering-configuration"></a>tooupdate configuração do peering privado do Azure
Pode atualizar qualquer parte da configuração de Olá utilizando Olá seguinte cmdlet. Exemplo de Olá abaixo, Olá ID de VLAN do circuito Olá está a ser atualizado de 100 too500.

    Set-AzureBGPPeering -AccessType Private -ServiceKey "*********************************" -PrimaryPeerSubnet "10.0.0.0/30" -SecondaryPeerSubnet "10.0.0.4/30" -PeerAsn 1234 -VlanId 500 -SharedKey "A1B2C3D4"

### <a name="toodelete-azure-private-peering"></a>toodelete peering privado do Azure
Pode remover a configuração de peering executando o seguinte cmdlet de Olá.

> [!WARNING]
> Tem de se certificar de que todas as redes virtuais são desassociadas do Olá circuito ExpressRoute antes de executar este cmdlet. 
> 
> 

    Remove-AzureBGPPeering -AccessType Private -ServiceKey "*********************************"


## <a name="azure-public-peering"></a>Peering público do Azure
Esta secção fornece instruções sobre como toocreate, obter, atualizar e eliminar Olá configuração do peering público do Azure para um circuito ExpressRoute.

### <a name="toocreate-azure-public-peering"></a>toocreate peering público do Azure
1. **Importe o módulo do PowerShell de Olá para o ExpressRoute.**
   
    Tem de importar módulos do Azure e ExpressRoute Olá para a sessão do PowerShell Olá no toostart ordem utilizando cmdlets do ExpressRoute Olá. Seguinte Olá executar comandos tooimport Olá do Azure e ExpressRoute os módulos para a sessão de PowerShell Olá. 
   
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\Azure.psd1'
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\ExpressRoute\ExpressRoute.psd1'
2. **Crie um circuito do ExpressRoute**
   
    Siga Olá instruções toocreate um [circuito ExpressRoute](expressroute-howto-circuit-classic.md) e solicite ao fornecedor de conectividade Olá. Se o seu fornecedor de conectividade oferecer serviços geridos de camada 3, pode pedir o tooenable de fornecedor de conectividade para si de peering público do Azure. Nesse caso, não terá das instruções de toofollow indicadas nas secções seguintes Olá. No entanto, se o seu fornecedor de conectividade não gerir encaminhamento por si, depois de criar o seu circuito, siga as instruções de Olá abaixo.
3. **Verifique tooensure do circuito ExpressRoute que está aprovisionado**
   
    Verifique primeiro toosee se Olá circuito ExpressRoute está aprovisionado e também ativado. Veja o exemplo de Olá abaixo.
   
        PS C:\> Get-AzureDedicatedCircuit -ServiceKey "*********************************"
   
        Bandwidth                        : 200
        CircuitName                      : MyTestCircuit
        Location                         : Silicon Valley
        ServiceKey                       : *********************************
        ServiceProviderName              : equinix
        ServiceProviderProvisioningState : Provisioned
        Sku                              : Standard
        Status                           : Enabled
   
    Certifique-se de que o circuito Olá mostra como aprovisionado e ativado. Se não, funciona com a sua tooget do fornecedor de conectividade do Estado do circuito toohello necessário e o estado.
   
        ServiceProviderProvisioningState : Provisioned
        Status                           : Enabled
4. **Configure o peering público do Azure para o circuito Olá**
   
    Certifique-se de que tem Olá seguintes informações antes de prosseguir.
   
   * Um /30 sub-rede para a ligação primária Olá. Esta tem de ser um prefixo IPv4 válido.
   * Um /30 sub-rede para a ligação secundária Olá. Esta tem de ser um prefixo IPv4 válido.
   * Um tooestablish de ID de VLAN válido este peering. Certifique-se de que nenhum outro peering no circuito de Olá utiliza Olá mesmo ID de VLAN.
   * Número AS para peering. Pode utilizar números AS de 2 e 4 bytes.
   * Um hash MD5 se optar por toouse um. **Isto é opcional**.
     
    Pode executar Olá seguir tooconfigure cmdlet peering público do Azure para o seu circuito
     
        Novo AzureBGPPeering - AccessType público - ServiceKey "***" - PrimaryPeerSubnet "131.107.0.0/30" - SecondaryPeerSubnet "131.107.0.4/30" - PeerAsn 1234 - VlanId 200
     
    Pode utilizar o cmdlet Olá abaixo se optar por toouse um hash MD5
     
        Novo AzureBGPPeering - AccessType público - ServiceKey "***" - PrimaryPeerSubnet "131.107.0.0/30" - SecondaryPeerSubnet "131.107.0.4/30" - PeerAsn 1234 - VlanId 200 - SharedKey "A1B2C3D4"
     
     > [!IMPORTANT]
     > Assegure que especifica o seu número AS como ASN de peering e não cliente ASN.
     > 
     > 

### <a name="tooview-azure-public-peering-details"></a>tooview detalhes de peering público do Azure
Pode obter os detalhes de configuração utilizando o seguinte cmdlet de Olá

    Get-AzureBGPPeering -AccessType Public -ServiceKey "*********************************"

    AdvertisedPublicPrefixes       : 
    AdvertisedPublicPrefixesState  : Configured
    AzureAsn                       : 12076
    CustomerAutonomousSystemNumber : 
    PeerAsn                        : 1234
    PrimaryAzurePort               : 
    PrimaryPeerSubnet              : 131.107.0.0/30
    RoutingRegistryName            : 
    SecondaryAzurePort             : 
    SecondaryPeerSubnet            : 131.107.0.4/30
    State                          : Enabled
    VlanId                         : 200


### <a name="tooupdate-azure-public-peering-configuration"></a>tooupdate configuração do peering público do Azure
Pode atualizar qualquer parte da configuração de Olá utilizando o seguinte cmdlet de Olá

    Set-AzureBGPPeering -AccessType Public -ServiceKey "*********************************" -PrimaryPeerSubnet "131.107.0.0/30" -SecondaryPeerSubnet "131.107.0.4/30" -PeerAsn 1234 -VlanId 600 -SharedKey "A1B2C3D4"

Olá ID de VLAN do circuito Olá está a ser atualizado de 200 too600 no Olá acima exemplo.

### <a name="toodelete-azure-public-peering"></a>toodelete peering público do Azure
Pode remover a configuração de peering executando o seguinte cmdlet de Olá

    Remove-AzureBGPPeering -AccessType Public -ServiceKey "*********************************"

## <a name="microsoft-peering"></a>Peering da Microsoft
Esta secção fornece instruções sobre como toocreate, obter, atualizar e eliminar Olá configuração peering da Microsoft para um circuito ExpressRoute. 

### <a name="toocreate-microsoft-peering"></a>toocreate peering da Microsoft
1. **Importe o módulo do PowerShell de Olá para o ExpressRoute.**
   
    Tem de importar módulos do Azure e ExpressRoute Olá para a sessão do PowerShell Olá no toostart ordem utilizando cmdlets do ExpressRoute Olá. Seguinte Olá executar comandos tooimport Olá do Azure e ExpressRoute os módulos para a sessão de PowerShell Olá.  
   
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\Azure.psd1'
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\ExpressRoute\ExpressRoute.psd1'
2. **Crie um circuito do ExpressRoute**
   
    Siga Olá instruções toocreate um [circuito ExpressRoute](expressroute-howto-circuit-classic.md) e solicite ao fornecedor de conectividade Olá. Se o seu fornecedor de conectividade oferecer serviços geridos de camada 3, pode pedir o tooenable de fornecedor de conectividade para si de peering privado do Azure. Nesse caso, não terá das instruções de toofollow indicadas nas secções seguintes Olá. No entanto, se o seu fornecedor de conectividade não gerir encaminhamento por si, depois de criar o seu circuito, siga as instruções de Olá abaixo.
3. **Verifique tooensure do circuito ExpressRoute que está aprovisionado**
   
    Verifique primeiro toosee se Olá circuito do ExpressRoute estiver num Estado aprovisionado e ativado.
   
        PS C:\> Get-AzureDedicatedCircuit -ServiceKey "*********************************"
   
        Bandwidth                        : 200
        CircuitName                      : MyTestCircuit
        Location                         : Silicon Valley
        ServiceKey                       : *********************************
        ServiceProviderName              : equinix
        ServiceProviderProvisioningState : Provisioned
        Sku                              : Standard
        Status                           : Enabled
   
    Certifique-se de que o circuito Olá mostra como aprovisionado e ativado. Se não, funciona com a sua tooget do fornecedor de conectividade do Estado do circuito toohello necessário e o estado.
   
        ServiceProviderProvisioningState : Provisioned
        Status                           : Enabled
4. **Configurar o peering da Microsoft para o circuito Olá**
   
    Certifique-se de que tem Olá seguintes informações antes de continuar.
   
   * Um /30 sub-rede para a ligação primária Olá. Esta tem de ser um prefixo IPv4 público válido detido por si e registado num RIR/TIR.
   * Um /30 sub-rede para a ligação secundária Olá. Esta tem de ser um prefixo IPv4 público válido detido por si e registado num RIR/TIR.
   * Um tooestablish de ID de VLAN válido este peering. Certifique-se de que nenhum outro peering no circuito de Olá utiliza Olá mesmo ID de VLAN.
   * Número AS para peering. Pode utilizar números AS de 2 e 4 bytes.
   * Prefixos anunciados: tem de fornecer uma lista de todos os prefixos planear tooadvertise através de sessão de BGP Olá. São aceites apenas prefixos de endereços IP públicos. Pode enviar uma lista separada por vírgulas se planear toosend um conjunto de prefixos. Estes prefixos têm de ser registado tooyou num RIR / TIR.
   * Cliente ASN: Se estiver a anunciar prefixos que não são registado toohello número AS de peering, pode especificar Olá como número toowhich que estão registados. **Isto é opcional**.
   * Nome do registo de encaminhamento: Pode especificar Olá RIR / IRR em relação a que Olá como número e prefixos são registados.
   * Um hash MD5, se escolher toouse um. **Isto é opcional.**
     
    Pode executar Olá seguir pering de Microsoft tooconfigure cmdlet para o seu circuito
     
        Novo AzureBGPPeering - AccessType Microsoft - ServiceKey "***" - PrimaryPeerSubnet "131.107.0.0/30" - SecondaryPeerSubnet "131.107.0.4/30" - VlanId 300 - PeerAsn 1234 - CustomerAsn 2245 - AdvertisedPublicPrefixes "123.0.0.0/30" - RoutingRegistryName "ARIN" - SharedKey "A1B2C3D4"

### <a name="tooview-microsoft-peering-details"></a>Detalhes do tooview Microsoft peering
Pode obter os detalhes de configuração com Olá seguinte cmdlet.

    Get-AzureBGPPeering -AccessType Microsoft -ServiceKey "*********************************"

    AdvertisedPublicPrefixes       : 123.0.0.0/30
    AdvertisedPublicPrefixesState  : Configured
    AzureAsn                       : 12076
    CustomerAutonomousSystemNumber : 2245
    PeerAsn                        : 1234
    PrimaryAzurePort               : 
    PrimaryPeerSubnet              : 10.0.0.0/30
    RoutingRegistryName            : ARIN
    SecondaryAzurePort             : 
    SecondaryPeerSubnet            : 10.0.0.4/30
    State                          : Enabled
    VlanId                         : 300


### <a name="tooupdate-microsoft-peering-configuration"></a>configuração do peering da Microsoft tooupdate
Pode atualizar qualquer parte da configuração de Olá utilizando Olá seguinte cmdlet.

    Set-AzureBGPPeering -AccessType Microsoft -ServiceKey "*********************************" -PrimaryPeerSubnet "131.107.0.0/30" -SecondaryPeerSubnet "131.107.0.4/30" -VlanId 300 -PeerAsn 1234 -CustomerAsn 2245 -AdvertisedPublicPrefixes "123.0.0.0/30" -RoutingRegistryName "ARIN" -SharedKey "A1B2C3D4"

### <a name="toodelete-microsoft-peering"></a>toodelete peering da Microsoft
Pode remover a configuração de peering executando o seguinte cmdlet de Olá.

    Remove-AzureBGPPeering -AccessType Microsoft -ServiceKey "*********************************"

## <a name="next-steps"></a>Passos seguintes
Em seguida, [ligação tooan uma VNet circuito ExpressRoute](expressroute-howto-linkvnet-classic.md).

* Para obter mais informações sobre fluxos de trabalho, consulte [fluxos de trabalho do ExpressRoute](expressroute-workflows.md).
* Para obter mais informações sobre peering do circuito, veja [Circuitos ExpressRoute e domínios de encaminhamento](expressroute-circuit-peerings.md).

