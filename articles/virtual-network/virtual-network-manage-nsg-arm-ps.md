---
title: "aaaManage de rede de grupos de segurança - Azure PowerShell | Microsoft Docs"
description: "Saiba como toomanage rede grupos de segurança através do PowerShell."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 3706ce6c-d9ae-46cb-a048-f0a4e84dc5cc
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/14/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 930fe5e0827896ad67b24d84e41a5d3f898ba838
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-network-security-groups-using-powershell"></a><span data-ttu-id="458cf-103">Gerir grupos de segurança de rede com o PowerShell</span><span class="sxs-lookup"><span data-stu-id="458cf-103">Manage network security groups using PowerShell</span></span>

[!INCLUDE [virtual-network-manage-arm-selectors-include.md](../../includes/virtual-network-manage-nsg-arm-selectors-include.md)]

[!INCLUDE [virtual-network-manage-nsg-intro-include.md](../../includes/virtual-network-manage-nsg-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="458cf-104">O Azure tem dois modelos de implementação diferentes para criar e trabalhar com os recursos: [Resource Manager e clássico](../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="458cf-104">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="458cf-105">Este artigo abrange utilizando o modelo de implementação Resource Manager de Olá, que a Microsoft recomenda-se para a maioria das implementações de novo em vez do modelo de implementação clássica Olá.</span><span class="sxs-lookup"><span data-stu-id="458cf-105">This article covers using hello Resource Manager deployment model, which Microsoft recommends for most new deployments instead of hello classic deployment model.</span></span>
>

[!INCLUDE [virtual-network-manage-nsg-arm-scenario-include.md](../../includes/virtual-network-manage-nsg-arm-scenario-include.md)]

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="retrieve-information"></a><span data-ttu-id="458cf-106">Obter as informações</span><span class="sxs-lookup"><span data-stu-id="458cf-106">Retrieve Information</span></span>
<span data-ttu-id="458cf-107">Pode ver os seus NSGs existentes, obter as regras para um NSG existente e descobrir os recursos que um NSG é associado a.</span><span class="sxs-lookup"><span data-stu-id="458cf-107">You can view your existing NSGs, retrieve rules for an existing NSG, and find out what resources an NSG is associated to.</span></span>

### <a name="view-existing-nsgs"></a><span data-ttu-id="458cf-108">Ver os NSGs existentes</span><span class="sxs-lookup"><span data-stu-id="458cf-108">View existing NSGs</span></span>
<span data-ttu-id="458cf-109">tooview todos os NSGs existentes numa subscrição, execute Olá `Get-AzureRmNetworkSecurityGroup` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="458cf-109">tooview all existing NSGs in a subscription, run hello `Get-AzureRmNetworkSecurityGroup` cmdlet.</span></span>

<span data-ttu-id="458cf-110">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="458cf-110">Expected result:</span></span>

    Name                 : NSG-BackEnd
    ResourceGroupName    : RG-NSG
    Location             : westus
    Id                   : /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/
                           Microsoft.Network/networkSecurityGroups/NSG-BackEnd
    Etag                 : W/"[Id]"
    ResourceGuid         : [Id]
    ProvisioningState    : Succeeded
    Tags                 :                            
    SecurityRules        : [...]
    DefaultSecurityRules : [...]
    NetworkInterfaces    : [...]
    Subnets              : [...]

    Name                 : NSG-FrontEnd
    ResourceGroupName    : RG-NSG
    Location             : eastus
    Id                   : /subscriptions/[Subscription Id]/resourceGroups/NRP-RG/providers/
                           Microsoft.Network/networkSecurityGroups/NSG-FrontEnd
    Etag                 : W/"[Id]"
    ResourceGuid         : [Id]
    ProvisioningState    : Succeeded
    Tags                 : 
    SecurityRules        : [...]
    DefaultSecurityRules : [...]
    NetworkInterfaces    : [...]
    Subnets              : [...]

    Name                 : WEB1
    ResourceGroupName    : RG101
    Location             : eastus2
    Id                   : /subscriptions/[Subscription Id]/resourceGroups/RG101/providers/M
                           icrosoft.Network/networkSecurityGroups/WEB1
    Etag                 : W/"[Id]"
    ResourceGuid         : [Id]
    ProvisioningState    : Succeeded
    Tags                 : 
    SecurityRules        : [...]
    DefaultSecurityRules : [...]
    NetworkInterfaces    : [...]
    Subnets              : [...]


<span data-ttu-id="458cf-111">lista de Olá tooview de NSGs num grupo de recursos específico, execute Olá `Get-AzureRmNetworkSecurityGroup` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="458cf-111">tooview hello list of NSGs in a specific resource group, run hello `Get-AzureRmNetworkSecurityGroup` cmdlet.</span></span>

<span data-ttu-id="458cf-112">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="458cf-112">Expected output:</span></span>

    Name                 : NSG-BackEnd
    ResourceGroupName    : RG-NSG
    Location             : westus
    Id                   : /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/
                           Microsoft.Network/networkSecurityGroups/NSG-BackEnd
    Etag                 : W/"[Id]"
    ResourceGuid         : [Id]
    ProvisioningState    : Succeeded
    Tags                 :                            
    SecurityRules        : [...]
    DefaultSecurityRules : [...]
    NetworkInterfaces    : [...]
    Subnets              : [...]

    Name                 : NSG-FrontEnd
    ResourceGroupName    : RG-NSG
    Location             : eastus
    Id                   : /subscriptions/[Subscription Id]/resourceGroups/NRP-RG/providers/
                           Microsoft.Network/networkSecurityGroups/NSG-FrontEnd
    Etag                 : W/"[Id]"
    ResourceGuid         : [Id]
    ProvisioningState    : Succeeded
    Tags                 : 
    SecurityRules        : [...]
    DefaultSecurityRules : [...]
    NetworkInterfaces    : [...]
    Subnets              : [...]

### <a name="list-all-rules-for-an-nsg"></a><span data-ttu-id="458cf-113">Listar todas as regras para um NSG</span><span class="sxs-lookup"><span data-stu-id="458cf-113">List all rules for an NSG</span></span>
<span data-ttu-id="458cf-114">regras de Olá tooview de um NSG denominado **NSG-front-end**, introduza Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="458cf-114">tooview hello rules of an NSG named **NSG-FrontEnd**, enter hello following command:</span></span>

```powershell
Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd | Select SecurityRules -ExpandProperty SecurityRules
```

<span data-ttu-id="458cf-115">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="458cf-115">Expected output:</span></span>

    Name                     : rdp-rule
    Id                       : /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/                           Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/rdp-rule
    Etag                     : W/"[Id]"
    ProvisioningState        : Succeeded
    Description              : Allow RDP
    Protocol                 : Tcp
    SourcePortRange          : *
    DestinationPortRange     : 3389
    SourceAddressPrefix      : Internet
    DestinationAddressPrefix : *
    Access                   : Allow
    Priority                 : 100
    Direction                : Inbound

    Name                     : web-rule
    Id                       : /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/                           Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/web-rule
    Etag                     : W/"[Id]"
    ProvisioningState        : Succeeded
    Description              : Allow HTTP
    Protocol                 : Tcp
    SourcePortRange          : *
    DestinationPortRange     : 80
    SourceAddressPrefix      : Internet
    DestinationAddressPrefix : *
    Access                   : Allow
    Priority                 : 101
    Direction                : Inbound

> [!NOTE]
> <span data-ttu-id="458cf-116">Também pode utilizar `Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name "NSG-FrontEnd" | Select DefaultSecurityRules -ExpandProperty DefaultSecurityRules` regras de predefinidas Olá toolist de Olá **NSG-front-end** NSG.</span><span class="sxs-lookup"><span data-stu-id="458cf-116">You can also use `Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name "NSG-FrontEnd" | Select DefaultSecurityRules -ExpandProperty DefaultSecurityRules` toolist hello default rules from hello **NSG-FrontEnd** NSG.</span></span>
> 

### <a name="view-nsgs-associations"></a><span data-ttu-id="458cf-117">Ver as associações de NSGs</span><span class="sxs-lookup"><span data-stu-id="458cf-117">View NSGs associations</span></span>
<span data-ttu-id="458cf-118">tooview que Olá recursos **NSG-front-end** NSG é associado ao, hello executar seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="458cf-118">tooview what resources hello **NSG-FrontEnd** NSG is associate with, run hello following command:</span></span>

```powershell
Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd
```

<span data-ttu-id="458cf-119">Procure Olá **nomes de NetworkInterfaces** e **sub-redes** propriedades conforme mostrado abaixo:</span><span class="sxs-lookup"><span data-stu-id="458cf-119">Look for hello **NetworkInterfaces** and **Subnets** properties as shown below:</span></span>

    NetworkInterfaces    : []
    Subnets              : [
                             {
                               "Id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/RG-NSG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                               "IpConfigurations": []
                             }
                           ]

<span data-ttu-id="458cf-120">No exemplo anterior Olá, Olá NSG não está associado tooany interfaces de rede (NICs); é associado tooa sub-rede designada **front-end**.</span><span class="sxs-lookup"><span data-stu-id="458cf-120">In hello previous example, hello NSG is not associated tooany network interfaces (NICs); it is associated tooa subnet named **FrontEnd**.</span></span>

## <a name="manage-rules"></a><span data-ttu-id="458cf-121">Gerir as regras</span><span class="sxs-lookup"><span data-stu-id="458cf-121">Manage rules</span></span>
<span data-ttu-id="458cf-122">Pode adicionar tooan regras existentes NSG, editar regras existentes e remova regras.</span><span class="sxs-lookup"><span data-stu-id="458cf-122">You can add rules tooan existing NSG, edit existing rules, and remove rules.</span></span>

### <a name="add-a-rule"></a><span data-ttu-id="458cf-123">Adicionar uma regra</span><span class="sxs-lookup"><span data-stu-id="458cf-123">Add a rule</span></span>
<span data-ttu-id="458cf-124">tooadd uma regra que permite **entrada** tráfego tooport **443** de qualquer máquina toohello **NSG-front-end** NSG, Olá concluir os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="458cf-124">tooadd a rule allowing **inbound** traffic tooport **443** from any machine toohello **NSG-FrontEnd** NSG, complete hello following steps:</span></span>

1. <span data-ttu-id="458cf-125">Executar Olá seguir Olá do comando tooretrieve existente NSG e armazená-las numa variável:</span><span class="sxs-lookup"><span data-stu-id="458cf-125">Run hello following command tooretrieve hello existing NSG and store it in a variable:</span></span>

    ```powershell   
    $nsg = Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd
    ```

2. <span data-ttu-id="458cf-126">Execute Olá tooadd de comando a seguir um NSG de toohello de regra:</span><span class="sxs-lookup"><span data-stu-id="458cf-126">Run hello following command tooadd a rule toohello NSG:</span></span>

    ```powershell
    Add-AzureRmNetworkSecurityRuleConfig -NetworkSecurityGroup $nsg `
    -Name https-rule `
    -Description "Allow HTTPS" `
    -Access Allow `
    -Protocol Tcp `
    -Direction Inbound `
    -Priority 102 `
    -SourceAddressPrefix * `
    -SourcePortRange * `
    -DestinationAddressPrefix * `
    -DestinationPortRange 443
    ```

3. <span data-ttu-id="458cf-127">as alterações de Olá toosave efetuadas toohello NSG, execute Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="458cf-127">toosave hello changes made toohello NSG, run hello following command:</span></span>

    ```powershell
    Set-AzureRmNetworkSecurityGroup -NetworkSecurityGroup $nsg
    ```
    <span data-ttu-id="458cf-128">Resultado esperado Mostrar apenas Olá regras de segurança:</span><span class="sxs-lookup"><span data-stu-id="458cf-128">Expected output showing only hello security rules:</span></span>
   
        Name                 : NSG-FrontEnd
        ...
        SecurityRules        : [
                                 {
                                   "Name": "rdp-rule",
                                   ...
                                 },
                                 {
                                   "Name": "web-rule",
                                   ...
                                 },
                                 {
                                   "Name": "https-rule",
                                   "Etag": "W/\"[Id]\"",
                                   "Id": "/subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/https-rule",
                                   "Description": "Allow HTTPS",
                                   "Protocol": "Tcp",
                                   "SourcePortRange": "*",
                                   "DestinationPortRange": "443",
                                   "SourceAddressPrefix": "*",
                                   "DestinationAddressPrefix": "*",
                                   "Access": "Allow",
                                   "Priority": 102,
                                   "Direction": "Inbound",
                                   "ProvisioningState": "Succeeded"
                                 }
                               ]

### <a name="change-a-rule"></a><span data-ttu-id="458cf-129">Alterar uma regra</span><span class="sxs-lookup"><span data-stu-id="458cf-129">Change a rule</span></span>
<span data-ttu-id="458cf-130">regra de Olá toochange criada acima tooallow de entrada do tráfego de Olá **Internet** apenas, siga os passos de Olá abaixo.</span><span class="sxs-lookup"><span data-stu-id="458cf-130">toochange hello rule created above tooallow inbound traffic from hello **Internet** only, follow hello steps below.</span></span>

1. <span data-ttu-id="458cf-131">Executar Olá seguir Olá do comando tooretrieve existente NSG e armazená-las numa variável:</span><span class="sxs-lookup"><span data-stu-id="458cf-131">Run hello following command tooretrieve hello existing NSG and store it in a variable:</span></span>

    ```powershell 
    $nsg = Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd
    ```

2. <span data-ttu-id="458cf-132">Execute Olá comando com as definições da regra nova Olá os seguintes:</span><span class="sxs-lookup"><span data-stu-id="458cf-132">Run hello following command with hello new rule settings:</span></span>

    ```powershell
    Set-AzureRmNetworkSecurityRuleConfig -NetworkSecurityGroup $nsg `
    -Name https-rule `
    -Description "Allow HTTPS" `
    -Access Allow `
    -Protocol Tcp `
    -Direction Inbound `
    -Priority 102 `
    -SourceAddressPrefix Internet `
    -SourcePortRange * `
    -DestinationAddressPrefix * `
    -DestinationPortRange 443
    ```

3. <span data-ttu-id="458cf-133">as alterações de Olá toosave efetuadas toohello NSG, execute Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="458cf-133">toosave hello changes made toohello NSG, run hello following command:</span></span>

    ```powershell
    Set-AzureRmNetworkSecurityGroup -NetworkSecurityGroup $nsg
    ```

    <span data-ttu-id="458cf-134">Resultado esperado Mostrar apenas Olá regras de segurança:</span><span class="sxs-lookup"><span data-stu-id="458cf-134">Expected output showing only hello security rules:</span></span>
   
        Name                 : NSG-FrontEnd
        ...
        SecurityRules        : [
                                 {
                                   "Name": "rdp-rule",
                                   ...
                                 },
                                 {
                                   "Name": "web-rule",
                                   ...
                                 },
                                 {
                                   "Name": "https-rule",
                                   "Etag": "W/\"[Id]\"",
                                   "Id": "/subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/https-rule",
                                   "Description": "Allow HTTPS",
                                   "Protocol": "Tcp",
                                   "SourcePortRange": "*",
                                   "DestinationPortRange": "443",
                                   "SourceAddressPrefix": "Internet",
                                   "DestinationAddressPrefix": "*",
                                   "Access": "Allow",
                                   "Priority": 102,
                                   "Direction": "Inbound",
                                   "ProvisioningState": "Succeeded"
                                 }
                               ]

### <a name="delete-a-rule"></a><span data-ttu-id="458cf-135">Eliminar uma regra</span><span class="sxs-lookup"><span data-stu-id="458cf-135">Delete a rule</span></span>
1. <span data-ttu-id="458cf-136">Executar Olá seguir Olá do comando tooretrieve existente NSG e armazená-las numa variável:</span><span class="sxs-lookup"><span data-stu-id="458cf-136">Run hello following command tooretrieve hello existing NSG and store it in a variable:</span></span>

    ```powershell
    $nsg = Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd
    ```

2. <span data-ttu-id="458cf-137">Execute Olá seguintes regra do comando tooremove Olá de Olá NSG:</span><span class="sxs-lookup"><span data-stu-id="458cf-137">Run hello following command tooremove hello rule from hello NSG:</span></span>

    ```powershell
    Remove-AzureRmNetworkSecurityRuleConfig -NetworkSecurityGroup $nsg -Name https-rule
    ```

3. <span data-ttu-id="458cf-138">Guarde as alterações efetuadas de Olá toohello NSG, executando Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="458cf-138">Save hello changes made toohello NSG, by running hello following command:</span></span>

    ```powershell
    Set-AzureRmNetworkSecurityGroup -NetworkSecurityGroup $nsg
    ```

    <span data-ttu-id="458cf-139">O resultado esperado Mostrar apenas Olá regras de segurança, tenha em atenção Olá **regra https** já não está listado:</span><span class="sxs-lookup"><span data-stu-id="458cf-139">Expected output showing only hello security rules, notice hello **https-rule** is no longer listed:</span></span>
   
        Name                 : NSG-FrontEnd
        ...
        SecurityRules        : [
                                 {
                                   "Name": "rdp-rule",
                                   ...
                                 },
                                 {
                                   "Name": "web-rule",
                                   ...
                                 }
                               ]

## <a name="manage-associations"></a><span data-ttu-id="458cf-140">Gerir as associações</span><span class="sxs-lookup"><span data-stu-id="458cf-140">Manage associations</span></span>
<span data-ttu-id="458cf-141">Pode associar um NSG toosubnets e NICs.</span><span class="sxs-lookup"><span data-stu-id="458cf-141">You can associate an NSG toosubnets and NICs.</span></span> <span data-ttu-id="458cf-142">Também pode desassociar um NSG a partir de qualquer recurso que está associado.</span><span class="sxs-lookup"><span data-stu-id="458cf-142">You can also dissociate an NSG from any resource it's associated to.</span></span>

### <a name="associate-an-nsg-tooa-nic"></a><span data-ttu-id="458cf-143">Associar um NSG tooa NIC</span><span class="sxs-lookup"><span data-stu-id="458cf-143">Associate an NSG tooa NIC</span></span>
<span data-ttu-id="458cf-144">Olá tooassociate **NSG-front-end** NSG toohello **TestNICWeb1** NIC, Olá concluir os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="458cf-144">tooassociate hello **NSG-FrontEnd** NSG toohello **TestNICWeb1** NIC, complete hello following steps:</span></span>

1. <span data-ttu-id="458cf-145">Executar Olá seguir Olá do comando tooretrieve existente NSG e armazená-las numa variável:</span><span class="sxs-lookup"><span data-stu-id="458cf-145">Run hello following command tooretrieve hello existing NSG and store it in a variable:</span></span>

    ```powershell
    $nsg = Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd
    ```

2. <span data-ttu-id="458cf-146">Executar Olá seguir Olá do comando tooretrieve existente NIC e armazená-las numa variável:</span><span class="sxs-lookup"><span data-stu-id="458cf-146">Run hello following command tooretrieve hello existing NIC and store it in a variable:</span></span>

    ```powershell
    $nic = Get-AzureRmNetworkInterface -ResourceGroupName RG-NSG -Name TestNICWeb1
    ```

3. <span data-ttu-id="458cf-147">Conjunto Olá **NetworkSecurityGroup** propriedade Olá **NIC** valor variável toohello Olá **NSG** variável, introduzindo Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="458cf-147">Set hello **NetworkSecurityGroup** property of hello **NIC** variable toohello value of hello **NSG** variable, by entering hello following command:</span></span>

    ```powershell
    $nic.NetworkSecurityGroup = $nsg
    ```

4. <span data-ttu-id="458cf-148">as alterações de Olá toosave efetuadas toohello NIC, execute Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="458cf-148">toosave hello changes made toohello NIC, run hello following command:</span></span>

    ```powershell
    Set-AzureRmNetworkInterface -NetworkInterface $nic
    ```
   
    <span data-ttu-id="458cf-149">Olá apenas do que mostra o resultado esperado **NetworkSecurityGroup** propriedade:</span><span class="sxs-lookup"><span data-stu-id="458cf-149">Expected output showing only hello **NetworkSecurityGroup** property:</span></span>
   
        NetworkSecurityGroup : {
                                 "SecurityRules": [],
                                 "DefaultSecurityRules": [],
                                 "NetworkInterfaces": [],
                                 "Subnets": [],
                                 "Id": "/subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd"
                               }

### <a name="dissociate-an-nsg-from-a-nic"></a><span data-ttu-id="458cf-150">Desassociar um NSG a partir de uma NIC</span><span class="sxs-lookup"><span data-stu-id="458cf-150">Dissociate an NSG from a NIC</span></span>
<span data-ttu-id="458cf-151">Olá toodissociate **NSG-front-end** NSG de Olá **TestNICWeb1** NIC, Olá concluir os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="458cf-151">toodissociate hello **NSG-FrontEnd** NSG from hello **TestNICWeb1** NIC, complete hello following steps:</span></span>

1. <span data-ttu-id="458cf-152">Executar Olá seguir Olá do comando tooretrieve existente NIC e armazená-las numa variável:</span><span class="sxs-lookup"><span data-stu-id="458cf-152">Run hello following command tooretrieve hello existing NIC and store it in a variable:</span></span>

    ```powershell
    $nic = Get-AzureRmNetworkInterface -ResourceGroupName RG-NSG -Name TestNICWeb1
    ```

2. <span data-ttu-id="458cf-153">Conjunto Olá **NetworkSecurityGroup** propriedade Olá **NIC** variável demasiado**$null** executando Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="458cf-153">Set hello **NetworkSecurityGroup** property of hello **NIC** variable too**$null** by running hello following command:</span></span>

    ```powershell
    $nic.NetworkSecurityGroup = $null
    ```

3. <span data-ttu-id="458cf-154">as alterações de Olá toosave efetuadas toohello NIC, execute Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="458cf-154">toosave hello changes made toohello NIC, run hello following command:</span></span>

    ```powershell
    Set-AzureRmNetworkInterface -NetworkInterface $nic
    ```
   
    <span data-ttu-id="458cf-155">Olá apenas do que mostra o resultado esperado **NetworkSecurityGroup** propriedade:</span><span class="sxs-lookup"><span data-stu-id="458cf-155">Expected output showing only hello **NetworkSecurityGroup** property:</span></span>
   
        NetworkSecurityGroup : null

### <a name="dissociate-an-nsg-from-a-subnet"></a><span data-ttu-id="458cf-156">Desassociar um NSG de sub-rede</span><span class="sxs-lookup"><span data-stu-id="458cf-156">Dissociate an NSG from a subnet</span></span>
<span data-ttu-id="458cf-157">Olá toodissociate **NSG-front-end** NSG de Olá **front-end** sub-rede, Olá concluir os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="458cf-157">toodissociate hello **NSG-FrontEnd** NSG from hello **FrontEnd** subnet, complete hello following steps:</span></span>

1. <span data-ttu-id="458cf-158">Executar Olá seguir Olá do comando tooretrieve existente VNet e armazená-las numa variável:</span><span class="sxs-lookup"><span data-stu-id="458cf-158">Run hello following command tooretrieve hello existing VNet and store it in a variable:</span></span>

    ```powershell
    $vnet = Get-AzureRmVirtualNetwork -ResourceGroupName RG-NSG -Name TestVNet
    ```

2. <span data-ttu-id="458cf-159">Execute hello os seguintes comandos tooretrieve Olá **front-end** sub-rede e armazená-las numa variável:</span><span class="sxs-lookup"><span data-stu-id="458cf-159">Run hello following command tooretrieve hello **FrontEnd** subnet and store it in a variable:</span></span>

    ```powershell
    $subnet = Get-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name FrontEnd
    ```
 
3. <span data-ttu-id="458cf-160">Conjunto Olá **NetworkSecurityGroup** propriedade Olá **sub-rede** variável demasiado**$null** introduzindo Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="458cf-160">Set hello **NetworkSecurityGroup** property of hello **subnet** variable too**$null** by entering hello following command:</span></span>

    ```powershell
    $subnet.NetworkSecurityGroup = $null
    ```

4. <span data-ttu-id="458cf-161">as alterações de Olá toosave efetuadas toohello sub-rede, execute Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="458cf-161">toosave hello changes made toohello subnet, run hello following command:</span></span>

    ```powershell
    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
    ```

    <span data-ttu-id="458cf-162">O resultado esperado que apresenta apenas as propriedades de Olá de Olá **front-end** sub-rede.</span><span class="sxs-lookup"><span data-stu-id="458cf-162">Expected output showing only hello properties of hello **FrontEnd** subnet.</span></span> <span data-ttu-id="458cf-163">Observe que não é uma propriedade para **NetworkSecurityGroup**:</span><span class="sxs-lookup"><span data-stu-id="458cf-163">Notice there isn't a property for **NetworkSecurityGroup**:</span></span>
   
            ...
            Subnets           : [
                                  {
                                    "Name": "FrontEnd",
                                    "Etag": "W/\"[Id]\"",
                                    "Id": "/subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                                    "AddressPrefix": "192.168.1.0/24",
                                    "IpConfigurations": [
                                      {
                                        "Id": "/subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkInterfaces/TestNICWeb2/ipConfigurations/ipconfig1"
                                      },
                                      {
                                        "Id": "/subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkInterfaces/TestNICWeb1/ipConfigurations/ipconfig1"
                                      }
                                    ],
                                    "ProvisioningState": "Succeeded"
                                  },
                                    ...
                                ]

### <a name="associate-an-nsg-tooa-subnet"></a><span data-ttu-id="458cf-164">Associar uma sub-rede de tooa NSG</span><span class="sxs-lookup"><span data-stu-id="458cf-164">Associate an NSG tooa subnet</span></span>
<span data-ttu-id="458cf-165">Olá tooassociate **NSG-front-end** NSG toohello **FronEnd** sub-rede novamente, Olá concluir os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="458cf-165">tooassociate hello **NSG-FrontEnd** NSG toohello **FronEnd** subnet again, complete hello following steps:</span></span>

1. <span data-ttu-id="458cf-166">Executar Olá seguir Olá do comando tooretrieve existente VNet e armazená-las numa variável:</span><span class="sxs-lookup"><span data-stu-id="458cf-166">Run hello following command tooretrieve hello existing VNet and store it in a variable:</span></span>

    ```powershell
    $vnet = Get-AzureRmVirtualNetwork -ResourceGroupName RG-NSG -Name TestVNet
    ```

2. <span data-ttu-id="458cf-167">Execute hello os seguintes comandos tooretrieve Olá **front-end** sub-rede e armazená-las numa variável:</span><span class="sxs-lookup"><span data-stu-id="458cf-167">Run hello following command tooretrieve hello **FrontEnd** subnet and store it in a variable:</span></span>

    ```powershell
    $subnet = Get-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name FrontEnd
    ```
 
3. <span data-ttu-id="458cf-168">Executar Olá seguir Olá do comando tooretrieve existente NSG e armazená-las numa variável:</span><span class="sxs-lookup"><span data-stu-id="458cf-168">Run hello following command tooretrieve hello existing NSG and store it in a variable:</span></span>

    ```powershell
    $nsg = Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd
    ```

4. <span data-ttu-id="458cf-169">Conjunto Olá **NetworkSecurityGroup** propriedade Olá **sub-rede** variável demasiado**$null** executando Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="458cf-169">Set hello **NetworkSecurityGroup** property of hello **subnet** variable too**$null** by running hello following command:</span></span>

    ```powershell
    $subnet.NetworkSecurityGroup = $nsg
    ```

5. <span data-ttu-id="458cf-170">as alterações de Olá toosave efetuadas toohello sub-rede, execute Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="458cf-170">toosave hello changes made toohello subnet, run hello following command:</span></span>

    ```powershell
    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
    ```

    <span data-ttu-id="458cf-171">Olá apenas do que mostra o resultado esperado **NetworkSecurityGroup** propriedade Olá **front-end** sub-rede:</span><span class="sxs-lookup"><span data-stu-id="458cf-171">Expected output showing only hello **NetworkSecurityGroup** property of hello **FrontEnd** subnet:</span></span>
   
        ...
        "NetworkSecurityGroup": {
                                  "SecurityRules": [],
                                  "DefaultSecurityRules": [],
                                  "NetworkInterfaces": [],
                                  "Subnets": [],
                                  "Id": "/subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd"
                                }
        ...

## <a name="delete-an-nsg"></a><span data-ttu-id="458cf-172">Eliminar um NSG</span><span class="sxs-lookup"><span data-stu-id="458cf-172">Delete an NSG</span></span>
<span data-ttu-id="458cf-173">Só é possível eliminar um NSG se tooany recurso não está associado.</span><span class="sxs-lookup"><span data-stu-id="458cf-173">You can only delete an NSG if it's not associated tooany resource.</span></span> <span data-ttu-id="458cf-174">toodelete um NSG, siga os passos de Olá abaixo.</span><span class="sxs-lookup"><span data-stu-id="458cf-174">toodelete an NSG, follow hello steps below.</span></span>

1. <span data-ttu-id="458cf-175">recursos de Olá toocheck associados tooan NSG, execute Olá `azure network nsg show` conforme mostrado no [vista NSGs associações](#View-NSGs-associations).</span><span class="sxs-lookup"><span data-stu-id="458cf-175">toocheck hello resources associated tooan NSG, run hello `azure network nsg show` as shown in [View NSGs associations](#View-NSGs-associations).</span></span>
2. <span data-ttu-id="458cf-176">Se Olá NSG é associado tooany NICs, execute Olá `azure network nic set` conforme mostrado no [desassociar um NSG a partir de uma NIC](#Dissociate-an-NSG-from-a-NIC) para cada NIC.</span><span class="sxs-lookup"><span data-stu-id="458cf-176">If hello NSG is associated tooany NICs, run hello `azure network nic set` as shown in [Dissociate an NSG from a NIC](#Dissociate-an-NSG-from-a-NIC) for each NIC.</span></span> 
3. <span data-ttu-id="458cf-177">Se Olá NSG é associado tooany sub-rede, execute Olá `azure network vnet subnet set` conforme mostrado no [desassociar um NSG de sub-rede](#Dissociate-an-NSG-from-a-subnet) para cada sub-rede.</span><span class="sxs-lookup"><span data-stu-id="458cf-177">If hello NSG is associated tooany subnet, run hello `azure network vnet subnet set` as shown in [Dissociate an NSG from a subnet](#Dissociate-an-NSG-from-a-subnet) for each subnet.</span></span>
4. <span data-ttu-id="458cf-178">toodelete Olá NSG, execute Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="458cf-178">toodelete hello NSG, run hello following command:</span></span>

    ```powershell
    Remove-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd -Force
    ```
   
   > [!NOTE]
   > <span data-ttu-id="458cf-179">Olá `-Force` parâmetro garante que não precisa de eliminação de Olá tooconfirm.</span><span class="sxs-lookup"><span data-stu-id="458cf-179">hello `-Force` parameter ensures you don't need tooconfirm hello deletion.</span></span>
   > 

## <a name="next-steps"></a><span data-ttu-id="458cf-180">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="458cf-180">Next steps</span></span>
* <span data-ttu-id="458cf-181">[Ativar o registo](virtual-network-nsg-manage-log.md) para NSGs.</span><span class="sxs-lookup"><span data-stu-id="458cf-181">[Enable logging](virtual-network-nsg-manage-log.md) for NSGs.</span></span>

