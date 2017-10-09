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
# <a name="create-a-virtual-network-using-powershell"></a><span data-ttu-id="f9f74-103">Criar uma rede virtual com o PowerShell</span><span class="sxs-lookup"><span data-stu-id="f9f74-103">Create a virtual network using PowerShell</span></span>

[!INCLUDE [virtual-networks-create-vnet-intro](../../includes/virtual-networks-create-vnet-intro-include.md)]

<span data-ttu-id="f9f74-104">O Azure tem dois modelos de implementação: a implementação do Azure Resource Manager e a implementação clássica.</span><span class="sxs-lookup"><span data-stu-id="f9f74-104">Azure has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="f9f74-105">A Microsoft recomenda a criação de recursos através do modelo de implementação do Resource Manager Olá.</span><span class="sxs-lookup"><span data-stu-id="f9f74-105">Microsoft recommends creating resources through hello Resource Manager deployment model.</span></span> <span data-ttu-id="f9f74-106">mais informações sobre como toolearn Olá diferenças entre os modelos de Olá dois ler Olá [modelos de implementação do Azure compreender](../azure-resource-manager/resource-manager-deployment-model.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="f9f74-106">toolearn more about hello differences between hello two models, read hello [Understand Azure deployment models](../azure-resource-manager/resource-manager-deployment-model.md) article.</span></span>
 
<span data-ttu-id="f9f74-107">Este artigo explica como toocreate uma VNet através da implementação do Resource Manager Olá modelo através do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f9f74-107">This article explains how toocreate a VNet through hello Resource Manager deployment model using PowerShell.</span></span> <span data-ttu-id="f9f74-108">Também pode criar uma VNet através do Resource Manager utilizando outras ferramentas ou criar uma VNet através do modelo de implementação clássica Olá selecionando uma opção diferente de Olá lista a seguir:</span><span class="sxs-lookup"><span data-stu-id="f9f74-108">You can also create a VNet through Resource Manager using other tools or create a VNet through hello classic deployment model by selecting a different option from hello following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="f9f74-109">Portal</span><span class="sxs-lookup"><span data-stu-id="f9f74-109">Portal</span></span>](virtual-networks-create-vnet-arm-pportal.md)
> * [<span data-ttu-id="f9f74-110">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f9f74-110">PowerShell</span></span>](virtual-networks-create-vnet-arm-ps.md)
> * [<span data-ttu-id="f9f74-111">CLI</span><span class="sxs-lookup"><span data-stu-id="f9f74-111">CLI</span></span>](virtual-networks-create-vnet-arm-cli.md)
> * [<span data-ttu-id="f9f74-112">Modelo</span><span class="sxs-lookup"><span data-stu-id="f9f74-112">Template</span></span>](virtual-networks-create-vnet-arm-template-click.md)
> * [<span data-ttu-id="f9f74-113">Portal (Clássico)</span><span class="sxs-lookup"><span data-stu-id="f9f74-113">Portal (Classic)</span></span>](virtual-networks-create-vnet-classic-pportal.md)
> * [<span data-ttu-id="f9f74-114">PowerShell (Clássico)</span><span class="sxs-lookup"><span data-stu-id="f9f74-114">PowerShell (Classic)</span></span>](virtual-networks-create-vnet-classic-netcfg-ps.md)
> * [<span data-ttu-id="f9f74-115">CLI (Clássica)</span><span class="sxs-lookup"><span data-stu-id="f9f74-115">CLI (Classic)</span></span>](virtual-networks-create-vnet-classic-cli.md)

[!INCLUDE [virtual-networks-create-vnet-scenario-include](../../includes/virtual-networks-create-vnet-scenario-include.md)]

## <a name="create-a-virtual-network"></a><span data-ttu-id="f9f74-116">Criar uma rede virtual</span><span class="sxs-lookup"><span data-stu-id="f9f74-116">Create a virtual network</span></span>

<span data-ttu-id="f9f74-117">toocreate uma rede virtual com o PowerShell, Olá concluir os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="f9f74-117">toocreate a virtual network using PowerShell, complete hello following steps:</span></span>

1. <span data-ttu-id="f9f74-118">Instalar e configurar o Azure PowerShell, seguindo os passos de Olá em Olá [como tooInstall e configurar o Azure PowerShell](/powershell/azure/overview) artigo.</span><span class="sxs-lookup"><span data-stu-id="f9f74-118">Install and configure Azure PowerShell, by following hello steps in hello [How tooInstall and Configure Azure PowerShell](/powershell/azure/overview) article.</span></span>

2. <span data-ttu-id="f9f74-119">Se necessário, crie um novo grupo de recursos, conforme mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="f9f74-119">If necessary, create a new resource group, as shown below.</span></span> <span data-ttu-id="f9f74-120">Para este cenário, crie um grupo de recursos denominado *TestRG*.</span><span class="sxs-lookup"><span data-stu-id="f9f74-120">For this scenario, create a resource group named *TestRG*.</span></span> <span data-ttu-id="f9f74-121">Para obter mais informações sobre os grupos de recursos, veja [Descrição Geral do Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f9f74-121">For more information about resource groups, visit [Azure Resource Manager Overview](../azure-resource-manager/resource-group-overview.md).</span></span>

    ```powershell   
    New-AzureRmResourceGroup -Name TestRG -Location centralus
    ```

    <span data-ttu-id="f9f74-122">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="f9f74-122">Expected output:</span></span>

        ResourceGroupName : TestRG
        Location          : centralus
        ProvisioningState : Succeeded
        Tags              :
        ResourceId        : /subscriptions/[Subscription Id]/resourceGroups/TestRG    
3. <span data-ttu-id="f9f74-123">Crie uma nova VNet com o nome *TestVNet*:</span><span class="sxs-lookup"><span data-stu-id="f9f74-123">Create a new VNet named *TestVNet*:</span></span>

    ```powershell
    New-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet `
    -AddressPrefix 192.168.0.0/16 -Location centralus
    ```

    <span data-ttu-id="f9f74-124">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="f9f74-124">Expected output:</span></span>

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
4. <span data-ttu-id="f9f74-125">Arquivo Olá objeto da rede virtual numa variável:</span><span class="sxs-lookup"><span data-stu-id="f9f74-125">Store hello virtual network object in a variable:</span></span>

    ```powershell
    $vnet = Get-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet
    ```

   > [!TIP]
   > <span data-ttu-id="f9f74-126">Pode combinar os passos 3 e 4 executando `$vnet = New-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet -AddressPrefix 192.168.0.0/16 -Location centralus`.</span><span class="sxs-lookup"><span data-stu-id="f9f74-126">You can combine steps 3 and 4 by running `$vnet = New-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet -AddressPrefix 192.168.0.0/16 -Location centralus`.</span></span>
   > 

5. <span data-ttu-id="f9f74-127">Adicione uma sub-rede toohello nova variável da VNet:</span><span class="sxs-lookup"><span data-stu-id="f9f74-127">Add a subnet toohello new VNet variable:</span></span>

    ```powershell
    Add-AzureRmVirtualNetworkSubnetConfig -Name FrontEnd `
    -VirtualNetwork $vnet -AddressPrefix 192.168.1.0/24
    ```

    <span data-ttu-id="f9f74-128">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="f9f74-128">Expected output:</span></span>
   
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

6. <span data-ttu-id="f9f74-129">Repita os passos 5 acima para cada sub-rede que pretende toocreate.</span><span class="sxs-lookup"><span data-stu-id="f9f74-129">Repeat step 5 above for each subnet you want toocreate.</span></span> <span data-ttu-id="f9f74-130">Olá comando seguinte cria Olá *back-end* sub-rede para o cenário de Olá:</span><span class="sxs-lookup"><span data-stu-id="f9f74-130">hello following command creates hello *BackEnd* subnet for hello scenario:</span></span>

    ```powershell
    Add-AzureRmVirtualNetworkSubnetConfig -Name BackEnd `
    -VirtualNetwork $vnet -AddressPrefix 192.168.2.0/24
    ```

7. <span data-ttu-id="f9f74-131">Embora crie sub-redes, elas atualmente só existem no Olá local tooretrieve utilizadas variáveis de Olá VNet que criou no passo 4 acima.</span><span class="sxs-lookup"><span data-stu-id="f9f74-131">Although you create subnets, they currently only exist in hello local variable used tooretrieve hello VNet you create in step 4 above.</span></span> <span data-ttu-id="f9f74-132">toosave Olá alterações tooAzure, execute Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="f9f74-132">toosave hello changes tooAzure, run hello following command:</span></span>

    ```powershell
    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
    ```
   
    <span data-ttu-id="f9f74-133">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="f9f74-133">Expected output:</span></span>
   
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

## <a name="next-steps"></a><span data-ttu-id="f9f74-134">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="f9f74-134">Next steps</span></span>

<span data-ttu-id="f9f74-135">Saiba como tooconnect:</span><span class="sxs-lookup"><span data-stu-id="f9f74-135">Learn how tooconnect:</span></span>

- <span data-ttu-id="f9f74-136">Uma rede virtual de tooa de máquina virtual (VM) através da leitura Olá [criar uma VM do Windows](../virtual-machines/virtual-machines-windows-ps-create.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="f9f74-136">A virtual machine (VM) tooa virtual network by reading hello [Create a Windows VM](../virtual-machines/virtual-machines-windows-ps-create.md) article.</span></span> <span data-ttu-id="f9f74-137">Em vez de criar uma VNet e sub-rede nos passos de Olá dos artigos Olá, pode selecionar uma VNet existente e sub-rede tooconnect uma VM.</span><span class="sxs-lookup"><span data-stu-id="f9f74-137">Instead of creating a VNet and subnet in hello steps of hello articles, you can select an existing VNet and subnet tooconnect a VM to.</span></span>
- <span data-ttu-id="f9f74-138">Olá, redes virtuais de tooother de rede virtual através da leitura Olá [ligar VNets](../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="f9f74-138">hello virtual network tooother virtual networks by reading hello [Connect VNets](../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md) article.</span></span>
- <span data-ttu-id="f9f74-139">Olá rede virtual tooan rede no local através de um site para site rede privada virtual (VPN) ou um circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="f9f74-139">hello virtual network tooan on-premises network using a site-to-site virtual private network (VPN) or ExpressRoute circuit.</span></span> <span data-ttu-id="f9f74-140">Saiba como. o lendo Olá [ligar uma rede no local do VNet tooan usando uma VPN de site para site](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md) e [ligação tooan uma VNet circuito ExpressRoute](../expressroute/expressroute-howto-linkvnet-arm.md) artigos.</span><span class="sxs-lookup"><span data-stu-id="f9f74-140">Learn how by reading hello [Connect a VNet tooan on-premises network using a site-to-site VPN](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md) and [Link a VNet tooan ExpressRoute circuit](../expressroute/expressroute-howto-linkvnet-arm.md) articles.</span></span>
