---
title: aaaOpen portas tooa VM com o Azure PowerShell | Microsoft Docs
description: "Saiba como tooopen uma porta / criar um ponto final tooyour VM do Windows utilizando o modo de implementação do Olá do Azure resource manager e o Azure PowerShell"
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: cf45f7d8-451a-48ab-8419-730366d54f1e
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 08/21/2017
ms.author: iainfou
ms.openlocfilehash: c1817a0c447ae4ce7a1ce2a1fc6927bedf2dacb5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooopen-ports-and-endpoints-tooa-vm-in-azure-using-powershell"></a><span data-ttu-id="8ea1f-103">Como tooopen portas e os pontos finais tooa VM no Azure utilizando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="8ea1f-103">How tooopen ports and endpoints tooa VM in Azure using PowerShell</span></span>
[!INCLUDE [virtual-machines-common-nsg-quickstart](../../../includes/virtual-machines-common-nsg-quickstart.md)]

## <a name="quick-commands"></a><span data-ttu-id="8ea1f-104">Comandos rápidos</span><span class="sxs-lookup"><span data-stu-id="8ea1f-104">Quick commands</span></span>
<span data-ttu-id="8ea1f-105">Grupo de segurança de rede toocreate e precisa de regras de ACL [versão mais recente do Olá do Azure PowerShell instalada](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="8ea1f-105">toocreate a Network Security Group and ACL rules you need [hello latest version of Azure PowerShell installed](/powershell/azureps-cmdlets-docs).</span></span> <span data-ttu-id="8ea1f-106">Também pode [executar estes passos, utilizando o portal do Azure de Olá](nsg-quickstart-portal.md).</span><span class="sxs-lookup"><span data-stu-id="8ea1f-106">You can also [perform these steps using hello Azure portal](nsg-quickstart-portal.md).</span></span>

<span data-ttu-id="8ea1f-107">Inicie sessão no tooyour conta do Azure:</span><span class="sxs-lookup"><span data-stu-id="8ea1f-107">Log in tooyour Azure account:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="8ea1f-108">No Olá exemplos a seguir, substitua os nomes dos parâmetros de exemplo com os seus próprios valores.</span><span class="sxs-lookup"><span data-stu-id="8ea1f-108">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="8ea1f-109">Os nomes de parâmetros de exemplo incluídos *myResourceGroup*, *myNetworkSecurityGroup*, e *myVnet*.</span><span class="sxs-lookup"><span data-stu-id="8ea1f-109">Example parameter names included *myResourceGroup*, *myNetworkSecurityGroup*, and *myVnet*.</span></span>

<span data-ttu-id="8ea1f-110">Criar uma regra com [New-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig).</span><span class="sxs-lookup"><span data-stu-id="8ea1f-110">Create a rule with [New-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig).</span></span> <span data-ttu-id="8ea1f-111">Olá exemplo seguinte cria uma regra com o nome *myNetworkSecurityGroupRule* tooallow *tcp* tráfego na porta *80*:</span><span class="sxs-lookup"><span data-stu-id="8ea1f-111">hello following example creates a rule named *myNetworkSecurityGroupRule* tooallow *tcp* traffic on port *80*:</span></span>

```powershell
$httprule = New-AzureRmNetworkSecurityRuleConfig `
    -Name "myNetworkSecurityGroupRule" `
    -Description "Allow HTTP" `
    -Access "Allow" `
    -Protocol "Tcp" `
    -Direction "Inbound" `
    -Priority "100" `
    -SourceAddressPrefix "Internet" `
    -SourcePortRange * `
    -DestinationAddressPrefix * `
    -DestinationPortRange 80
```

<span data-ttu-id="8ea1f-112">Em seguida, crie o grupo de segurança de rede com [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) e atribuir Olá HTTP regra que acabou de criar da seguinte forma.</span><span class="sxs-lookup"><span data-stu-id="8ea1f-112">Next, create your Network Security group with [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) and assign hello HTTP rule you just created as follows.</span></span> <span data-ttu-id="8ea1f-113">Olá exemplo seguinte cria um grupo de segurança de rede com o nome *myNetworkSecurityGroup*:</span><span class="sxs-lookup"><span data-stu-id="8ea1f-113">hello following example creates a Network Security Group named *myNetworkSecurityGroup*:</span></span>

```powershell
$nsg = New-AzureRmNetworkSecurityGroup `
    -ResourceGroupName "myResourceGroup" `
    -Location "EastUS" `
    -Name "myNetworkSecurityGroup" `
    -SecurityRules $httprule
```

<span data-ttu-id="8ea1f-114">Agora vamos atribuir a sub-rede de tooa do grupo de segurança de rede.</span><span class="sxs-lookup"><span data-stu-id="8ea1f-114">Now let's assign your Network Security Group tooa subnet.</span></span> <span data-ttu-id="8ea1f-115">Olá seguinte exemplo atribui uma rede virtual existente denominada *myVnet* toohello variável *$vnet* com [Get-AzureRmVirtualNetwork](/powershell/module/azurerm.network/get-azurermvirtualnetwork):</span><span class="sxs-lookup"><span data-stu-id="8ea1f-115">hello following example assigns an existing virtual network named *myVnet* toohello variable *$vnet* with [Get-AzureRmVirtualNetwork](/powershell/module/azurerm.network/get-azurermvirtualnetwork):</span></span>

```powershell
$vnet = Get-AzureRmVirtualNetwork `
    -ResourceGroupName "myResourceGroup" `
    -Name "myVnet"
```

<span data-ttu-id="8ea1f-116">Associar o seu grupo de segurança de rede com a sub-rede com [conjunto AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig).</span><span class="sxs-lookup"><span data-stu-id="8ea1f-116">Associate your Network Security Group with your subnet with [Set-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig).</span></span> <span data-ttu-id="8ea1f-117">Olá exemplo seguinte associa sub-rede Olá designada *mySubnet* com o grupo de segurança de rede:</span><span class="sxs-lookup"><span data-stu-id="8ea1f-117">hello following example associates hello subnet named *mySubnet* with your Network Security Group:</span></span>

```powershell
$subnetPrefix = $vnet.Subnets|?{$_.Name -eq 'mySubnet'}

Set-AzureRmVirtualNetworkSubnetConfig `
    -VirtualNetwork $vnet `
    -Name "mySubnet" `
    -AddressPrefix $subnetPrefix.AddressPrefix `
    -NetworkSecurityGroup $nsg
```

<span data-ttu-id="8ea1f-118">Por fim, atualize a rede virtual com [Set-AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork) por ordem para o efeito de tootake alterações:</span><span class="sxs-lookup"><span data-stu-id="8ea1f-118">Finally, update your virtual network with [Set-AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork) in order for your changes tootake effect:</span></span>

```powershell
Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
```


## <a name="more-information-on-network-security-groups"></a><span data-ttu-id="8ea1f-119">Obter mais informações sobre grupos de segurança de rede</span><span class="sxs-lookup"><span data-stu-id="8ea1f-119">More information on Network Security Groups</span></span>
<span data-ttu-id="8ea1f-120">comandos rápidos Olá aqui permitem-lhe tooget cópias de segurança e em execução com tooyour de fluxo de tráfego VM.</span><span class="sxs-lookup"><span data-stu-id="8ea1f-120">hello quick commands here allow you tooget up and running with traffic flowing tooyour VM.</span></span> <span data-ttu-id="8ea1f-121">Grupos de segurança de rede fornecem várias funcionalidades excelentes e granularidade para controlar aceder a recursos tooyour.</span><span class="sxs-lookup"><span data-stu-id="8ea1f-121">Network Security Groups provide many great features and granularity for controlling access tooyour resources.</span></span> <span data-ttu-id="8ea1f-122">Pode ler mais sobre [criar um grupo de segurança de rede e a ACL regras aqui](tutorial-virtual-network.md#manage-internal-traffic).</span><span class="sxs-lookup"><span data-stu-id="8ea1f-122">You can read more about [creating a Network Security Group and ACL rules here](tutorial-virtual-network.md#manage-internal-traffic).</span></span>

<span data-ttu-id="8ea1f-123">Para aplicações web de elevada disponibilidade, deve colocar as VMs por trás de um balanceador de carga do Azure.</span><span class="sxs-lookup"><span data-stu-id="8ea1f-123">For highly available web applications, you should place your VMs behind an Azure Load Balancer.</span></span> <span data-ttu-id="8ea1f-124">Balanceador de carga Olá distribui o tráfego tooVMs, com um grupo de segurança de rede que fornece a filtragem de tráfego.</span><span class="sxs-lookup"><span data-stu-id="8ea1f-124">hello load balancer distributes traffic tooVMs, with a Network Security Group that provides traffic filtering.</span></span> <span data-ttu-id="8ea1f-125">Para obter mais informações, consulte [como balancear tooload Linux virtual máquinas na toocreate do Azure, uma aplicação altamente disponível](tutorial-load-balancer.md).</span><span class="sxs-lookup"><span data-stu-id="8ea1f-125">For more information, see [How tooload balance Linux virtual machines in Azure toocreate a highly available application](tutorial-load-balancer.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="8ea1f-126">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="8ea1f-126">Next steps</span></span>
<span data-ttu-id="8ea1f-127">Neste exemplo, criou um tráfego de tooallow HTTP regra simples.</span><span class="sxs-lookup"><span data-stu-id="8ea1f-127">In this example, you created a simple rule tooallow HTTP traffic.</span></span> <span data-ttu-id="8ea1f-128">Pode encontrar informações sobre como criar ambientes mais detalhados no Olá seguintes artigos:</span><span class="sxs-lookup"><span data-stu-id="8ea1f-128">You can find information on creating more detailed environments in hello following articles:</span></span>

* [<span data-ttu-id="8ea1f-129">Descrição geral do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="8ea1f-129">Azure Resource Manager overview</span></span>](../../azure-resource-manager/resource-group-overview.md)
* [<span data-ttu-id="8ea1f-130">O que é um Grupo de Segurança de Rede (NSG)? (What is a Network Security Group (NSG)?)</span><span class="sxs-lookup"><span data-stu-id="8ea1f-130">What is a Network Security Group (NSG)?</span></span>](../../virtual-network/virtual-networks-nsg.md)
* [<span data-ttu-id="8ea1f-131">Descrição geral do Gestor de recursos do Azure para balanceadores de carga</span><span class="sxs-lookup"><span data-stu-id="8ea1f-131">Azure Resource Manager Overview for Load Balancers</span></span>](../../load-balancer/load-balancer-arm.md)

