---
title: "aaaManage de rede de grupos de segurança - CLI do Azure 1.0 | Microsoft Docs"
description: "Saiba como grupos de segurança de rede de toomanage utilizando Olá interface de linha de comandos do Azure (CLI) 1.0."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/21/2017
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 9a429f947abbcb5fa6adb40c84504f68efd5e20e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-network-security-groups-using-hello-azure-cli-10"></a><span data-ttu-id="fcce9-103">Gerir grupos de segurança de rede com Olá CLI do Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="fcce9-103">Manage network security groups using hello Azure CLI 1.0</span></span>

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="fcce9-104">Tarefas do CLI versões toocomplete Olá</span><span class="sxs-lookup"><span data-stu-id="fcce9-104">CLI versions toocomplete hello task</span></span> 

<span data-ttu-id="fcce9-105">Pode concluir tarefas Olá utilizando uma das seguintes versões do CLI de Olá:</span><span class="sxs-lookup"><span data-stu-id="fcce9-105">You can complete hello task using one of hello following CLI versions:</span></span> 

- <span data-ttu-id="fcce9-106">[Azure CLI 1.0](#View-existing-NSGs) – nosso CLI para Olá clássica e resource Gestão modelos de implementação</span><span class="sxs-lookup"><span data-stu-id="fcce9-106">[Azure CLI 1.0](#View-existing-NSGs) – our CLI for hello classic and resource management deployment models</span></span> 
- <span data-ttu-id="fcce9-107">[Azure CLI 2.0](virtual-network-manage-nsg-arm-cli.md) -nossa próxima geração CLI para o modelo de implementação da gestão de recursos de Olá (Este artigo)</span><span class="sxs-lookup"><span data-stu-id="fcce9-107">[Azure CLI 2.0](virtual-network-manage-nsg-arm-cli.md) - our next generation CLI for hello resource management deployment model (this article)</span></span>

[!INCLUDE [virtual-network-manage-nsg-intro-include.md](../../includes/virtual-network-manage-nsg-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="fcce9-108">O Azure tem dois modelos de implementação diferentes para criar e trabalhar com os recursos: [Resource Manager e clássico](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="fcce9-108">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="fcce9-109">Este artigo abrange utilizando o modelo de implementação Resource Manager de Olá, que a Microsoft recomenda-se para a maioria das implementações de novo em vez do modelo de implementação clássica Olá.</span><span class="sxs-lookup"><span data-stu-id="fcce9-109">This article covers using hello Resource Manager deployment model, which Microsoft recommends for most new deployments instead of hello classic deployment model.</span></span>
> 

[!INCLUDE [virtual-network-manage-nsg-arm-scenario-include.md](../../includes/virtual-network-manage-nsg-arm-scenario-include.md)]

[!INCLUDE [azure-cli-prerequisites-include.md](../../includes/azure-cli-prerequisites-include.md)]

## <a name="retrieve-information"></a><span data-ttu-id="fcce9-110">Obter as informações</span><span class="sxs-lookup"><span data-stu-id="fcce9-110">Retrieve Information</span></span>
<span data-ttu-id="fcce9-111">Pode ver os seus NSGs existentes, obter as regras para um NSG existente e descobrir os recursos que um NSG é associado a.</span><span class="sxs-lookup"><span data-stu-id="fcce9-111">You can view your existing NSGs, retrieve rules for an existing NSG, and find out what resources an NSG is associated to.</span></span>

### <a name="view-existing-nsgs"></a><span data-ttu-id="fcce9-112">Ver os NSGs existentes</span><span class="sxs-lookup"><span data-stu-id="fcce9-112">View existing NSGs</span></span>
<span data-ttu-id="fcce9-113">lista de Olá tooview de NSGs num grupo de recursos específico, execute Olá `azure network nsg list` comando conforme mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="fcce9-113">tooview hello list of NSGs in a specific resource group, run hello `azure network nsg list` command as shown below.</span></span>

```azurecli
azure network nsg list --resource-group RG-NSG
```

<span data-ttu-id="fcce9-114">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="fcce9-114">Expected output:</span></span>

    info:    Executing command network nsg list
    + Getting hello network security groups
    data:    Name          Location
    data:    ------------  --------
    data:    NSG-BackEnd   westus
    data:    NSG-FrontEnd  westus
    info:    network nsg list command OK

### <a name="list-all-rules-for-an-nsg"></a><span data-ttu-id="fcce9-115">Listar todas as regras para um NSG</span><span class="sxs-lookup"><span data-stu-id="fcce9-115">List all rules for an NSG</span></span>
<span data-ttu-id="fcce9-116">regras de Olá tooview de um NSG denominado **NSG-front-end**, hello execute `azure network nsg show` comando conforme mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="fcce9-116">tooview hello rules of an NSG named **NSG-FrontEnd**, run hello `azure network nsg show` command as shown below.</span></span> 

```azurecli
azure network nsg show --resource-group RG-NSG --name NSG-FrontEnd
```

<span data-ttu-id="fcce9-117">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="fcce9-117">Expected output:</span></span>

    info:    Executing command network nsg show
    + Looking up hello network security group "NSG-FrontEnd"
    data:    Id                              : /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd
    data:    Name                            : NSG-FrontEnd
    data:    Type                            : Microsoft.Network/networkSecurityGroups
    data:    Location                        : westus
    data:    Provisioning state              : Succeeded
    data:    Tags                            : displayName=NSG - Front End
    data:    Security group rules:
    data:    Name                           Source IP          Source Port  Destination IP  Destination Port  Protocol  Direction  Access  Priority
    data:    -----------------------------  -----------------  -----------  --------------  ----------------  --------  ---------  ------  --------
    data:    rdp-rule                       Internet           *            *               3389              Tcp       Inbound    Allow   100
    data:    web-rule                       Internet           *            *               80                Tcp       Inbound    Allow   101
    data:    AllowVnetInBound               VirtualNetwork     *            VirtualNetwork  *                 *         Inbound    Allow   65000
    data:    AllowAzureLoadBalancerInBound  AzureLoadBalancer  *            *               *                 *         Inbound    Allow   65001
    data:    DenyAllInBound                 *                  *            *               *                 *         Inbound    Deny    65500
    data:    AllowVnetOutBound              VirtualNetwork     *            VirtualNetwork  *                 *         Outbound   Allow   65000
    data:    AllowInternetOutBound          *                  *            Internet        *                 *         Outbound   Allow   65001
    data:    DenyAllOutBound                *                  *            *               *                 *         Outbound   Deny    65500
    info:    network nsg show command OK

> [!NOTE]
> <span data-ttu-id="fcce9-118">Também pode utilizar `azure network nsg rule list --resource-group RG-NSG --nsg-name NSG-FrontEnd` regras de Olá toolist dos Olá **NSG-front-end** NSG.</span><span class="sxs-lookup"><span data-stu-id="fcce9-118">You can also use `azure network nsg rule list --resource-group RG-NSG --nsg-name NSG-FrontEnd` toolist hello rules from hello **NSG-FrontEnd** NSG.</span></span>
>

### <a name="view-nsg-associations"></a><span data-ttu-id="fcce9-119">Associações de NSG de vista</span><span class="sxs-lookup"><span data-stu-id="fcce9-119">View NSG associations</span></span>

<span data-ttu-id="fcce9-120">tooview que Olá recursos **NSG-front-end** NSG é associado ao, execute Olá `azure network nsg show` comando conforme mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="fcce9-120">tooview what resources hello **NSG-FrontEnd** NSG is associate with, run hello `azure network nsg show` command as shown below.</span></span> <span data-ttu-id="fcce9-121">Tenha em atenção que Olá apenas diferença é a utilização de Olá de Olá **– json** parâmetro.</span><span class="sxs-lookup"><span data-stu-id="fcce9-121">Notice that hello only difference is hello use of hello **--json** parameter.</span></span>

```azurecli
azure network nsg show --resource-group RG-NSG --name NSG-FrontEnd --json
```

<span data-ttu-id="fcce9-122">Procure Olá **nomes de networkInterfaces** e **sub-redes** propriedades conforme mostrado abaixo:</span><span class="sxs-lookup"><span data-stu-id="fcce9-122">Look for hello **networkInterfaces** and **subnets** properties as shown below:</span></span>

    "networkInterfaces": [],
    ...
    "subnets": [
        {
            "id": "/subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd"
        }
    ],
    ...

<span data-ttu-id="fcce9-123">No exemplo de Olá acima, Olá NSG não está associado a tooany interfaces de rede (NICs) e é associado tooa sub-rede designada **front-end**.</span><span class="sxs-lookup"><span data-stu-id="fcce9-123">In hello example above, hello NSG is not associated tooany network interfaces (NICs), and it is associated tooa subnet named **FrontEnd**.</span></span>

## <a name="manage-rules"></a><span data-ttu-id="fcce9-124">Gerir as regras</span><span class="sxs-lookup"><span data-stu-id="fcce9-124">Manage rules</span></span>
<span data-ttu-id="fcce9-125">Pode adicionar tooan regras existentes NSG, editar regras existentes e remova regras.</span><span class="sxs-lookup"><span data-stu-id="fcce9-125">You can add rules tooan existing NSG, edit existing rules, and remove rules.</span></span>

### <a name="add-a-rule"></a><span data-ttu-id="fcce9-126">Adicionar uma regra</span><span class="sxs-lookup"><span data-stu-id="fcce9-126">Add a rule</span></span>
<span data-ttu-id="fcce9-127">tooadd uma regra que permite **entrada** tráfego tooport **443** de qualquer máquina toohello **NSG-front-end** NSG, introduza Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="fcce9-127">tooadd a rule allowing **inbound** traffic tooport **443** from any machine toohello **NSG-FrontEnd** NSG, enter hello following command:</span></span>

```azurecli
azure network nsg rule create --resource-group RG-NSG \
    --nsg-name NSG-FrontEnd \
    --name allow-https \
    --description "Allow access tooport 443 for HTTPS" \
    --protocol Tcp \
    --source-address-prefix * \
    --source-port-range * \
    --destination-address-prefix * \
    --destination-port-range 443 \
    --access Allow \
    --priority 102 \
    --direction Inbound
```

<span data-ttu-id="fcce9-128">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="fcce9-128">Expected output:</span></span>

    info:    Executing command network nsg rule create
    + Looking up hello network security rule "allow-https"
    + Creating a network security rule "allow-https"
    + Looking up hello network security group "NSG-FrontEnd"
    data:    Id                              : /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/allow-https
    data:    Name                            : allow-https
    data:    Type                            : Microsoft.Network/networkSecurityGroups/securityRules
    data:    Provisioning state              : Succeeded
    data:    Description                     : Allow access tooport 443 for HTTPS
    data:    Source IP                       : *
    data:    Source Port                     : *
    data:    Destination IP                  : *
    data:    Destination Port                : 443
    data:    Protocol                        : Tcp
    data:    Direction                       : Inbound
    data:    Access                          : Allow
    data:    Priority                        : 102
    info:    network nsg rule create command OK

### <a name="change-a-rule"></a><span data-ttu-id="fcce9-129">Alterar uma regra</span><span class="sxs-lookup"><span data-stu-id="fcce9-129">Change a rule</span></span>
<span data-ttu-id="fcce9-130">regra de Olá toochange criada acima tooallow de entrada do tráfego de Olá **Internet** apenas, execute hello os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="fcce9-130">toochange hello rule created above tooallow inbound traffic from hello **Internet** only, run hello following command:</span></span>

```azurecli
azure network nsg rule set --resource-group RG-NSG \
    --nsg-name NSG-FrontEnd \
    --name allow-https \
    --source-address-prefix Internet
```

<span data-ttu-id="fcce9-131">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="fcce9-131">Expected output:</span></span>

    info:    Executing command network nsg rule set
    + Looking up hello network security group "NSG-FrontEnd"
    + Setting a network security rule "allow-https"
    + Looking up hello network security group "NSG-FrontEnd"
    data:    Id                              : /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/allow-https
    data:    Name                            : allow-https
    data:    Type                            : Microsoft.Network/networkSecurityGroups/securityRules
    data:    Provisioning state              : Succeeded
    data:    Description                     : Allow access tooport 443 for HTTPS
    data:    Source IP                       : Internet
    data:    Source Port                     : *
    data:    Destination IP                  : *
    data:    Destination Port                : 443
    data:    Protocol                        : Tcp
    data:    Direction                       : Inbound
    data:    Access                          : Allow
    data:    Priority                        : 102
    info:    network nsg rule set command OK

### <a name="delete-a-rule"></a><span data-ttu-id="fcce9-132">Eliminar uma regra</span><span class="sxs-lookup"><span data-stu-id="fcce9-132">Delete a rule</span></span>
<span data-ttu-id="fcce9-133">regra de Olá toodelete criado acima, executar Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="fcce9-133">toodelete hello rule created above, run hello following command:</span></span>

```azurecli
azure network nsg rule delete --resource-group RG-NSG \
    --nsg-name NSG-FrontEnd \
    --name allow-https \
    --quiet
```

> [!NOTE]
> <span data-ttu-id="fcce9-134">Olá `--quiet` parâmetro garante que não precisa de eliminação de Olá tooconfirm.</span><span class="sxs-lookup"><span data-stu-id="fcce9-134">hello `--quiet` parameter ensures you don't need tooconfirm hello deletion.</span></span>
>

<span data-ttu-id="fcce9-135">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="fcce9-135">Expected output:</span></span>

    info:    Executing command network nsg rule delete
    + Looking up hello network security group "NSG-FrontEnd"
    + Deleting network security rule "allow-https"
    info:    network nsg rule delete command OK

## <a name="manage-associations"></a><span data-ttu-id="fcce9-136">Gerir as associações</span><span class="sxs-lookup"><span data-stu-id="fcce9-136">Manage associations</span></span>
<span data-ttu-id="fcce9-137">Pode associar um NSG toosubnets e NICs.</span><span class="sxs-lookup"><span data-stu-id="fcce9-137">You can associate an NSG toosubnets and NICs.</span></span> <span data-ttu-id="fcce9-138">Também pode desassociar um NSG a partir de qualquer recurso que está associado.</span><span class="sxs-lookup"><span data-stu-id="fcce9-138">You can also dissociate an NSG from any resource it's associated to.</span></span>

### <a name="associate-an-nsg-tooa-nic"></a><span data-ttu-id="fcce9-139">Associar um NSG tooa NIC</span><span class="sxs-lookup"><span data-stu-id="fcce9-139">Associate an NSG tooa NIC</span></span>
<span data-ttu-id="fcce9-140">Olá tooassociate **NSG-front-end** NSG toohello **TestNICWeb1** NIC, execute Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="fcce9-140">tooassociate hello **NSG-FrontEnd** NSG toohello **TestNICWeb1** NIC, run hello following command:</span></span>

```azurecli
azure network nic set --resource-group RG-NSG \
    --name TestNICWeb1 \
    --network-security-group-name NSG-FrontEnd
```

<span data-ttu-id="fcce9-141">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="fcce9-141">Expected output:</span></span>

    info:    Executing command network nic set
    + Looking up hello network interface "TestNICWeb1"
    + Looking up hello network security group "NSG-FrontEnd"
    + Updating network interface "TestNICWeb1"
    + Looking up hello network interface "TestNICWeb1"
    data:    Id                              : /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/RG-NSG/providers/Microsoft.Network/networkInterfaces/TestNICWeb1
    data:    Name                            : TestNICWeb1
    data:    Type                            : Microsoft.Network/networkInterfaces
    data:    Location                        : westus
    data:    Provisioning state              : Succeeded
    data:    MAC address                     : 00-0D-3A-30-A1-F8
    data:    Enable IP forwarding            : false
    data:    Tags                            : displayName=NetworkInterfaces - Web
    data:    Network security group          : /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd
    data:    Virtual machine                 : /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/RG-NSG/providers/Microsoft.Compute/virtualMachines/Web1
    data:    IP configurations:
    data:      Name                          : ipconfig1
    data:      Provisioning state            : Succeeded
    data:      Public IP address             : /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/RG-NSG/providers/Microsoft.Network/publicIPAddresses/TestPIPWeb1
    data:      Private IP address            : 192.168.1.5
    data:      Private IP Allocation Method  : Dynamic
    data:      Subnet                        : /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/RG-NSG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd
    data:
    info:    network nic set command OK

### <a name="dissociate-an-nsg-from-a-nic"></a><span data-ttu-id="fcce9-142">Desassociar um NSG a partir de uma NIC</span><span class="sxs-lookup"><span data-stu-id="fcce9-142">Dissociate an NSG from a NIC</span></span>

<span data-ttu-id="fcce9-143">Olá toodissociate **NSG-front-end** NSG de Olá **TestNICWeb1** NIC, execute Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="fcce9-143">toodissociate hello **NSG-FrontEnd** NSG from hello **TestNICWeb1** NIC, run hello following command:</span></span>

```azurecli
azure network nic set --resource-group RG-NSG --name TestNICWeb1 --network-security-group-id ""
```

> [!NOTE]
> <span data-ttu-id="fcce9-144">Olá de aviso "" valor (vazio) para Olá `network-security-group-id` parâmetro.</span><span class="sxs-lookup"><span data-stu-id="fcce9-144">Notice hello "" (empty) value for hello `network-security-group-id` parameter.</span></span> <span data-ttu-id="fcce9-145">É como remover uma associação tooan NSG.</span><span class="sxs-lookup"><span data-stu-id="fcce9-145">That is how you remove an association tooan NSG.</span></span> <span data-ttu-id="fcce9-146">Não é possível efetuar Olá mesmo com Olá `network-security-group-name` parâmetro.</span><span class="sxs-lookup"><span data-stu-id="fcce9-146">You can't do hello same with hello `network-security-group-name` parameter.</span></span>
> 

<span data-ttu-id="fcce9-147">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="fcce9-147">Expected result:</span></span>

    info:    Executing command network nic set
    + Looking up hello network interface "TestNICWeb1"
    + Updating network interface "TestNICWeb1"
    + Looking up hello network interface "TestNICWeb1"
    data:    Id                              : /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkInterfaces/TestNICWeb1
    data:    Name                            : TestNICWeb1
    data:    Type                            : Microsoft.Network/networkInterfaces
    data:    Location                        : westus
    data:    Provisioning state              : Succeeded
    data:    MAC address                     : 00-0D-3A-30-A1-F8
    data:    Enable IP forwarding            : false
    data:    Tags                            : displayName=NetworkInterfaces - Web
    data:    Virtual machine                 : /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Compute/virtualMachines/Web1
    data:    IP configurations:
    data:      Name                          : ipconfig1
    data:      Provisioning state            : Succeeded
    data:      Public IP address             : /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/publicIPAddresses/TestPIPWeb1
    data:      Private IP address            : 192.168.1.5
    data:      Private IP Allocation Method  : Dynamic
    data:      Subnet                        : /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd
    data:
    info:    network nic set command OK

### <a name="dissociate-an-nsg-from-a-subnet"></a><span data-ttu-id="fcce9-148">Desassociar um NSG de sub-rede</span><span class="sxs-lookup"><span data-stu-id="fcce9-148">Dissociate an NSG from a subnet</span></span>
<span data-ttu-id="fcce9-149">Olá toodissociate **NSG-front-end** NSG de Olá **front-end** sub-rede, execute Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="fcce9-149">toodissociate hello **NSG-FrontEnd** NSG from hello **FrontEnd** subnet, run hello following command:</span></span>

```azurecli
azure network vnet subnet set --resource-group RG-NSG \
    --vnet-name TestVNet \
    --name FrontEnd \
    --network-security-group-id ""
```

<span data-ttu-id="fcce9-150">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="fcce9-150">Expected output:</span></span>

    info:    Executing command network vnet subnet set
    + Looking up hello subnet "FrontEnd"
    + Setting subnet "FrontEnd"
    + Looking up hello subnet "FrontEnd"
    data:    Id                              : /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd
    data:    Type                            : Microsoft.Network/virtualNetworks/subnets
    data:    ProvisioningState               : Succeeded
    data:    Name                            : FrontEnd
    data:    Address prefix                  : 192.168.1.0/24
    data:    IP configurations:
    data:      /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkInterfaces/TestNICWeb2/ipConfigurations/ipconfig1
    data:      /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkInterfaces/TestNICWeb1/ipConfigurations/ipconfig1
    data:
    info:    network vnet subnet set command OK

### <a name="associate-an-nsg-tooa-subnet"></a><span data-ttu-id="fcce9-151">Associar uma sub-rede de tooa NSG</span><span class="sxs-lookup"><span data-stu-id="fcce9-151">Associate an NSG tooa subnet</span></span>
<span data-ttu-id="fcce9-152">Olá tooassociate **NSG-front-end** NSG toohello **FronEnd** sub-rede novamente, execute Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="fcce9-152">tooassociate hello **NSG-FrontEnd** NSG toohello **FronEnd** subnet again, run hello following command:</span></span>

```azurecli
azure network vnet subnet set --resource-group RG-NSG \
    --vnet-name TestVNet \
    --name FrontEnd \
    --network-security-group-name NSG-FronEnd
```

> [!NOTE]
> <span data-ttu-id="fcce9-153">Olá comando acima só funciona porque Olá **NSG-front-end** NSG está em Olá mesmo grupo de recursos à rede virtual Olá **TestVNet**.</span><span class="sxs-lookup"><span data-stu-id="fcce9-153">hello command above only works because hello **NSG-FrontEnd** NSG is in hello same resource group as hello virtual network **TestVNet**.</span></span> <span data-ttu-id="fcce9-154">Se Olá NSG está num grupo de recursos diferente, terá de toouse Olá `--network-security-group-id` parâmetro em vez disso e forneça o id completo de Olá para Olá NSG.</span><span class="sxs-lookup"><span data-stu-id="fcce9-154">If hello NSG is in a different resource group, you need toouse hello `--network-security-group-id` parameter instead, and provide hello full id for hello NSG.</span></span> <span data-ttu-id="fcce9-155">Pode obter o id de Olá executando `azure network nsg show --resource-group RG-NSG --name NSG-FrontEnd --json` e à procura de Olá **id** propriedade.</span><span class="sxs-lookup"><span data-stu-id="fcce9-155">You can retrieve hello id by running `azure network nsg show --resource-group RG-NSG --name NSG-FrontEnd --json` and looking for hello **id** property.</span></span> 
> 

<span data-ttu-id="fcce9-156">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="fcce9-156">Expected output:</span></span>

        info:    Executing command network vnet subnet set
        + Looking up hello subnet "FrontEnd"
        + Looking up hello network security group "NSG-FrontEnd"
        + Setting subnet "FrontEnd"
        + Looking up hello subnet "FrontEnd"
        data:    Id                              : /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd
        data:    Type                            : Microsoft.Network/virtualNetworks/subnets
        data:    ProvisioningState               : Succeeded
        data:    Name                            : FrontEnd
        data:    Address prefix                  : 192.168.1.0/24
        data:    Network security group          : [object Object]
        data:    IP configurations:
        data:      /subscriptions/[Subscription Id]resourceGroups/RG-NSG/providers/Microsoft.Network/networkInterfaces/TestNICWeb2/ipConfigurations/ipconfig1
        data:      /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkInterfaces/TestNICWeb1/ipConfigurations/ipconfig1
        data:
        info:    network vnet subnet set command OK

## <a name="delete-an-nsg"></a><span data-ttu-id="fcce9-157">Eliminar um NSG</span><span class="sxs-lookup"><span data-stu-id="fcce9-157">Delete an NSG</span></span>
<span data-ttu-id="fcce9-158">Só é possível eliminar um NSG se tooany recurso não está associado.</span><span class="sxs-lookup"><span data-stu-id="fcce9-158">You can only delete an NSG if it's not associated tooany resource.</span></span> <span data-ttu-id="fcce9-159">toodelete um NSG, siga os passos de Olá abaixo.</span><span class="sxs-lookup"><span data-stu-id="fcce9-159">toodelete an NSG, follow hello steps below.</span></span>

1. <span data-ttu-id="fcce9-160">recursos de Olá toocheck associados tooan NSG, execute Olá `azure network nsg show` conforme mostrado no [vista NSGs associações](#View-NSGs-associations).</span><span class="sxs-lookup"><span data-stu-id="fcce9-160">toocheck hello resources associated tooan NSG, run hello `azure network nsg show` as shown in [View NSGs associations](#View-NSGs-associations).</span></span>
2. <span data-ttu-id="fcce9-161">Se Olá NSG é associado tooany NICs, execute Olá `azure network nic set` conforme mostrado no [desassociar um NSG a partir de uma NIC](#Dissociate-an-NSG-from-a-NIC) para cada NIC.</span><span class="sxs-lookup"><span data-stu-id="fcce9-161">If hello NSG is associated tooany NICs, run hello `azure network nic set` as shown in [Dissociate an NSG from a NIC](#Dissociate-an-NSG-from-a-NIC) for each NIC.</span></span> 
3. <span data-ttu-id="fcce9-162">Se Olá NSG é associado tooany sub-rede, execute Olá `azure network vnet subnet set` conforme mostrado no [desassociar um NSG de sub-rede](#Dissociate-an-NSG-from-a-subnet) para cada sub-rede.</span><span class="sxs-lookup"><span data-stu-id="fcce9-162">If hello NSG is associated tooany subnet, run hello `azure network vnet subnet set` as shown in [Dissociate an NSG from a subnet](#Dissociate-an-NSG-from-a-subnet) for each subnet.</span></span>
4. <span data-ttu-id="fcce9-163">toodelete Olá NSG, execute Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="fcce9-163">toodelete hello NSG, run hello following command:</span></span>

    ```azurecli
    azure network nsg delete --resource-group RG-NSG --name NSG-FrontEnd --quiet
    ```

    <span data-ttu-id="fcce9-164">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="fcce9-164">Expected output:</span></span>

        info:    Executing command network nsg delete
        + Looking up hello network security group "NSG-FrontEnd"
        + Deleting network security group "NSG-FrontEnd"
        info:    network nsg delete command OK

## <a name="next-steps"></a><span data-ttu-id="fcce9-165">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="fcce9-165">Next steps</span></span>
* <span data-ttu-id="fcce9-166">[Ativar o registo](virtual-network-nsg-manage-log.md) para NSGs.</span><span class="sxs-lookup"><span data-stu-id="fcce9-166">[Enable logging](virtual-network-nsg-manage-log.md) for NSGs.</span></span>

