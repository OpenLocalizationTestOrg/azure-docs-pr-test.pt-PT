---
title: aaaCreate uma rede virtual - Azure PowerShell | Microsoft Docs
description: "Saiba como toocreate a virtual rede através do PowerShell."
services: virtual-network
documentationcenter: 
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: a31f4f12-54ee-4339-b968-1a8097ca77d3
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/03/2017
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 8d6e395a77f71de9f94b6304b05450e46b47544f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-using-powershell"></a>Criar uma rede virtual com o PowerShell

[!INCLUDE [virtual-networks-create-vnet-intro](../../includes/virtual-networks-create-vnet-intro-include.md)]

O Azure tem dois modelos de implementação: a implementação do Azure Resource Manager e a implementação clássica. A Microsoft recomenda a criação de recursos através do modelo de implementação do Resource Manager Olá. mais informações sobre como toolearn Olá diferenças entre os modelos de Olá dois ler Olá [modelos de implementação do Azure compreender](../azure-resource-manager/resource-manager-deployment-model.md) artigo.
 
Este artigo explica como toocreate uma VNet através da implementação do Resource Manager Olá modelo através do PowerShell. Também pode criar uma VNet através do Resource Manager utilizando outras ferramentas ou criar uma VNet através do modelo de implementação clássica Olá selecionando uma opção diferente de Olá lista a seguir:

> [!div class="op_single_selector"]
> * [Portal](virtual-networks-create-vnet-arm-pportal.md)
> * [PowerShell](virtual-networks-create-vnet-arm-ps.md)
> * [CLI](virtual-networks-create-vnet-arm-cli.md)
> * [Modelo](virtual-networks-create-vnet-arm-template-click.md)
> * [Portal (Clássico)](virtual-networks-create-vnet-classic-pportal.md)
> * [PowerShell (Clássico)](virtual-networks-create-vnet-classic-netcfg-ps.md)
> * [CLI (Clássica)](virtual-networks-create-vnet-classic-cli.md)

[!INCLUDE [virtual-networks-create-vnet-scenario-include](../../includes/virtual-networks-create-vnet-scenario-include.md)]

## <a name="create-a-virtual-network"></a>Criar uma rede virtual

toocreate uma rede virtual com o PowerShell, Olá concluir os seguintes passos:

1. Instalar e configurar o Azure PowerShell, seguindo os passos de Olá em Olá [como tooInstall e configurar o Azure PowerShell](/powershell/azure/overview) artigo.

2. Se necessário, crie um novo grupo de recursos, conforme mostrado abaixo. Para este cenário, crie um grupo de recursos denominado *TestRG*. Para obter mais informações sobre os grupos de recursos, veja [Descrição Geral do Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).

    ```powershell   
    New-AzureRmResourceGroup -Name TestRG -Location centralus
    ```

    Resultado esperado:

        ResourceGroupName : TestRG
        Location          : centralus
        ProvisioningState : Succeeded
        Tags              :
        ResourceId        : /subscriptions/[Subscription Id]/resourceGroups/TestRG    
3. Crie uma nova VNet com o nome *TestVNet*:

    ```powershell
    New-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet `
    -AddressPrefix 192.168.0.0/16 -Location centralus
    ```

    Resultado esperado:

        Name                  : TestVNet
        ResourceGroupName     : TestRG
        Location              : centralus
        Id                    : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet
        Etag                   : W/"[Id]"
        ProvisioningState          : Succeeded
        Tags                       : 
        AddressSpace               : {
                                   "AddressPrefixes": [
                                     "192.168.0.0/16"
                                   ]
                                  }
        DhcpOptions                : {}
        Subnets                    : []
        VirtualNetworkPeerings     : []
4. Arquivo Olá objeto da rede virtual numa variável:

    ```powershell
    $vnet = Get-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet
    ```

   > [!TIP]
   > Pode combinar os passos 3 e 4 executando `$vnet = New-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet -AddressPrefix 192.168.0.0/16 -Location centralus`.
   > 

5. Adicione uma sub-rede toohello nova variável da VNet:

    ```powershell
    Add-AzureRmVirtualNetworkSubnetConfig -Name FrontEnd `
    -VirtualNetwork $vnet -AddressPrefix 192.168.1.0/24
    ```

    Resultado esperado:
   
        Name                  : TestVNet
        ResourceGroupName     : TestRG
        Location              : centralus
        Id                    : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet
        Etag                  : W/"[Id]"
        ProvisioningState     : Succeeded
        Tags                  :
        AddressSpace          : {
                                  "AddressPrefixes": [
                                    "192.168.0.0/16"
                                  ]
                                }
        DhcpOptions           : {}
        Subnets             : [
                                  {
                                    "Name": "FrontEnd",
                                    "AddressPrefix": "192.168.1.0/24"
                                  }
                                ]
        VirtualNetworkPeerings     : []

6. Repita os passos 5 acima para cada sub-rede que pretende toocreate. Olá comando seguinte cria Olá *back-end* sub-rede para o cenário de Olá:

    ```powershell
    Add-AzureRmVirtualNetworkSubnetConfig -Name BackEnd `
    -VirtualNetwork $vnet -AddressPrefix 192.168.2.0/24
    ```

7. Embora crie sub-redes, elas atualmente só existem no Olá local tooretrieve utilizadas variáveis de Olá VNet que criou no passo 4 acima. toosave Olá alterações tooAzure, execute Olá os seguintes comandos:

    ```powershell
    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
    ```
   
    Resultado esperado:
   
        Name                  : TestVNet
        ResourceGroupName     : TestRG
        Location              : centralus
        Id                    : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet
        Etag                  : W/"[Id]"
        ProvisioningState     : Succeeded
        Tags                  :
        AddressSpace          : {
                                  "AddressPrefixes": [
                                    "192.168.0.0/16"
                                  ]
                                }
        DhcpOptions           : {
                                  "DnsServers": []
                                }
        Subnets               : [
                                  {
                                    "Name": "FrontEnd",
                                    "Etag": "W/\"[Id]\"",
                                    "Id": "/subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                                    "AddressPrefix": "192.168.1.0/24",
                                    "IpConfigurations": [],
                                    "ProvisioningState": "Succeeded"
                                  },
                                  {
                                    "Name": "BackEnd",
                                    "Etag": "W/\"[Id]\"",
                                    "Id": "/subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/BackEnd",
                                    "AddressPrefix": "192.168.2.0/24",
                                    "IpConfigurations": [],
                                    "ProvisioningState": "Succeeded"
                                  }
                                ]
        VirtualNetworkPeerings : []

## <a name="next-steps"></a>Passos seguintes

Saiba como tooconnect:

- Uma rede virtual de tooa de máquina virtual (VM) através da leitura Olá [criar uma VM do Windows](../virtual-machines/virtual-machines-windows-ps-create.md) artigo. Em vez de criar uma VNet e sub-rede nos passos de Olá dos artigos Olá, pode selecionar uma VNet existente e sub-rede tooconnect uma VM.
- Olá, redes virtuais de tooother de rede virtual através da leitura Olá [ligar VNets](../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md) artigo.
- Olá rede virtual tooan rede no local através de um site para site rede privada virtual (VPN) ou um circuito ExpressRoute. Saiba como. o lendo Olá [ligar uma rede no local do VNet tooan usando uma VPN de site para site](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md) e [ligação tooan uma VNet circuito ExpressRoute](../expressroute/expressroute-howto-linkvnet-arm.md) artigos.
