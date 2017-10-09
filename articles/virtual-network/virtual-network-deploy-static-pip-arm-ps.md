---
title: "aaaCreate uma VM com um endereço IP público estático - Azure PowerShell | Microsoft Docs"
description: "Saiba como toocreate uma VM com um IP público estático endereço com o PowerShell."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: ad975ab9-d69f-45c1-9e45-0d3f0f51e87e
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 0d2b88319cb114b8616f60dbee41e8fdc6d8b1b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-a-static-public-ip-address-using-powershell"></a><span data-ttu-id="d8473-103">Criar uma VM com um endereço IP público estático através do PowerShell</span><span class="sxs-lookup"><span data-stu-id="d8473-103">Create a VM with a static public IP address using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="d8473-104">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="d8473-104">Azure portal</span></span>](virtual-network-deploy-static-pip-arm-portal.md)
> * [<span data-ttu-id="d8473-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d8473-105">PowerShell</span></span>](virtual-network-deploy-static-pip-arm-ps.md)
> * [<span data-ttu-id="d8473-106">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="d8473-106">Azure CLI</span></span>](virtual-network-deploy-static-pip-arm-cli.md)
> * [<span data-ttu-id="d8473-107">Modelo</span><span class="sxs-lookup"><span data-stu-id="d8473-107">Template</span></span>](virtual-network-deploy-static-pip-arm-template.md)
> * [<span data-ttu-id="d8473-108">PowerShell (Clássico)</span><span class="sxs-lookup"><span data-stu-id="d8473-108">PowerShell (Classic)</span></span>](virtual-networks-reserved-public-ip.md)

[!INCLUDE [virtual-network-deploy-static-pip-intro-include.md](../../includes/virtual-network-deploy-static-pip-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="d8473-109">O Azure tem dois modelos de implementação diferentes para criar e trabalhar com os recursos: [Resource Manager e clássico](../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="d8473-109">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="d8473-110">Este artigo abrange utilizando o modelo de implementação Resource Manager de Olá, que a Microsoft recomenda-se para a maioria das implementações de novo em vez do modelo de implementação clássica Olá.</span><span class="sxs-lookup"><span data-stu-id="d8473-110">This article covers using hello Resource Manager deployment model, which Microsoft recommends for most new deployments instead of hello classic deployment model.</span></span>

[!INCLUDE [virtual-network-deploy-static-pip-scenario-include.md](../../includes/virtual-network-deploy-static-pip-scenario-include.md)]

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="step-1---start-your-script"></a><span data-ttu-id="d8473-111">Passo 1 – iniciar o script</span><span class="sxs-lookup"><span data-stu-id="d8473-111">Step 1 - Start your script</span></span>
<span data-ttu-id="d8473-112">Pode transferir o script do PowerShell completa Olá utilizado [aqui](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/virtual-network-deploy-static-pip-arm-ps.ps1).</span><span class="sxs-lookup"><span data-stu-id="d8473-112">You can download hello full PowerShell script used [here](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/virtual-network-deploy-static-pip-arm-ps.ps1).</span></span> <span data-ttu-id="d8473-113">Siga os passos de Olá abaixo toochange Olá script toowork no seu ambiente.</span><span class="sxs-lookup"><span data-stu-id="d8473-113">Follow hello steps below toochange hello script toowork in your environment.</span></span>

<span data-ttu-id="d8473-114">Alterar Olá valores das variáveis de Olá abaixo com base nos valores de Olá pretende toouse para a sua implementação.</span><span class="sxs-lookup"><span data-stu-id="d8473-114">Change hello values of hello variables below based on hello values you want toouse for your deployment.</span></span> <span data-ttu-id="d8473-115">Olá seguir o cenário de toohello de mapa de valores utilizado neste artigo:</span><span class="sxs-lookup"><span data-stu-id="d8473-115">hello following values map toohello scenario used in this article:</span></span>

```powershell
# Set variables resource group
$rgName                = "IaaSStory"
$location              = "West US"

# Set variables for VNet
$vnetName              = "WTestVNet"
$vnetPrefix            = "192.168.0.0/16"
$subnetName            = "FrontEnd"
$subnetPrefix          = "192.168.1.0/24"

# Set variables for storage
$stdStorageAccountName = "iaasstorystorage"

# Set variables for VM
$vmSize                = "Standard_A1"
$diskSize              = 127
$publisher             = "MicrosoftWindowsServer"
$offer                 = "WindowsServer"
$sku                   = "2012-R2-Datacenter"
$version               = "latest"
$vmName                = "WEB1"
$osDiskName            = "osdisk"
$nicName               = "NICWEB1"
$privateIPAddress      = "192.168.1.101"
$pipName               = "PIPWEB1"
$dnsName               = "iaasstoryws1"
```

## <a name="step-2---create-hello-necessary-resources-for-your-vm"></a><span data-ttu-id="d8473-116">Passo 2 - Criar Olá recursos necessários para a VM</span><span class="sxs-lookup"><span data-stu-id="d8473-116">Step 2 - Create hello necessary resources for your VM</span></span>
<span data-ttu-id="d8473-117">Antes de criar uma VM, precisa de um grupo de recursos, VNet, pública IP e NIC toobe utilizado pelo Olá VM.</span><span class="sxs-lookup"><span data-stu-id="d8473-117">Before creating a VM, you need a resource group, VNet, public IP, and NIC toobe used by hello VM.</span></span>

1. <span data-ttu-id="d8473-118">Crie um novo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="d8473-118">Create a new resource group.</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name $rgName -Location $location
    ```

2. <span data-ttu-id="d8473-119">Criar Olá VNet e sub-rede.</span><span class="sxs-lookup"><span data-stu-id="d8473-119">Create hello VNet and subnet.</span></span>

    ```powershell
    $vnet = New-AzureRmVirtualNetwork -ResourceGroupName $rgName -Name $vnetName `
        -AddressPrefix $vnetPrefix -Location $location

    Add-AzureRmVirtualNetworkSubnetConfig -Name $subnetName `
        -VirtualNetwork $vnet -AddressPrefix $subnetPrefix

    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
    ```

3. <span data-ttu-id="d8473-120">Crie o recurso de IP público Olá.</span><span class="sxs-lookup"><span data-stu-id="d8473-120">Create hello public IP resource.</span></span> 

    ```powershell
    $pip = New-AzureRmPublicIpAddress -Name $pipName -ResourceGroupName $rgName `
        -AllocationMethod Static -DomainNameLabel $dnsName -Location $location
    ```

4. <span data-ttu-id="d8473-121">Crie a interface de rede (NIC) do Olá para Olá VM na sub-rede Olá criado acima, com o IP público Olá.</span><span class="sxs-lookup"><span data-stu-id="d8473-121">Create hello network interface (NIC) for hello VM in hello subnet created above, with hello public IP.</span></span> <span data-ttu-id="d8473-122">Repare Olá cmdlet primeiro obter Olá VNet do Azure, isto é necessário desde um `Set-AzureRmVirtualNetwork` foi executado toochange Olá VNet existente.</span><span class="sxs-lookup"><span data-stu-id="d8473-122">Notice hello first cmdlet retrieving hello VNet from Azure, this is necessary since a `Set-AzureRmVirtualNetwork` was executed toochange hello existing VNet.</span></span>

    ```powershell
    $vnet = Get-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $rgName
    $subnet = Get-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name $subnetName
    $nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $rgName `
        -Subnet $subnet -Location $location -PrivateIpAddress $privateIPAddress `
        -PublicIpAddress $pip
    ```

5. <span data-ttu-id="d8473-123">Crie um Olá de toohost de conta de armazenamento disco de SO de VM.</span><span class="sxs-lookup"><span data-stu-id="d8473-123">Create a storage account toohost hello VM OS drive.</span></span>

    ```powershell
    $stdStorageAccount = New-AzureRmStorageAccount -Name $stdStorageAccountName `
    -ResourceGroupName $rgName -Type Standard_LRS -Location $location
    ```

## <a name="step-3---create-hello-vm"></a><span data-ttu-id="d8473-124">Passo 3 – criar Olá VM</span><span class="sxs-lookup"><span data-stu-id="d8473-124">Step 3 - Create hello VM</span></span>
<span data-ttu-id="d8473-125">Agora que todos os recursos necessários estão em vigor, pode criar uma nova VM.</span><span class="sxs-lookup"><span data-stu-id="d8473-125">Now that all necessary resources are in place, you can create a new VM.</span></span>

1. <span data-ttu-id="d8473-126">Crie o objeto de configuração de Olá para Olá VM.</span><span class="sxs-lookup"><span data-stu-id="d8473-126">Create hello configuration object for hello VM.</span></span>

    ```powershell
    $vmConfig = New-AzureRmVMConfig -VMName $vmName -VMSize $vmSize
    ```

2. <span data-ttu-id="d8473-127">Obter credenciais para Olá conta de administrador local da VM.</span><span class="sxs-lookup"><span data-stu-id="d8473-127">Get credentials for hello VM local administrator account.</span></span>

    ```powershell
    $cred = Get-Credential -Message "Type hello name and password for hello local administrator account."
    ```

3. <span data-ttu-id="d8473-128">Crie um objeto de configuração de VM.</span><span class="sxs-lookup"><span data-stu-id="d8473-128">Create a VM configuration object.</span></span>

    ```powershell
    $vmConfig = Set-AzureRmVMOperatingSystem -VM $vmConfig -Windows -ComputerName $vmName `
        -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
    ```

4. <span data-ttu-id="d8473-129">Definir a imagem do sistema operativo Olá para Olá VM.</span><span class="sxs-lookup"><span data-stu-id="d8473-129">Set hello operating system image for hello VM.</span></span>

    ```powershell
    $vmConfig = Set-AzureRmVMSourceImage -VM $vmConfig -PublisherName $publisher `
        -Offer $offer -Skus $sku -Version $version
    ```

5. <span data-ttu-id="d8473-130">Configure o disco de Olá SO.</span><span class="sxs-lookup"><span data-stu-id="d8473-130">Configure hello OS disk.</span></span>

    ```powershell
    $osVhdUri = $stdStorageAccount.PrimaryEndpoints.Blob.ToString() + "vhds/" + $osDiskName + ".vhd"
    $vmConfig = Set-AzureRmVMOSDisk -VM $vmConfig -Name $osDiskName -VhdUri $osVhdUri -CreateOption fromImage
    ```

6. <span data-ttu-id="d8473-131">Adicione Olá NIC toohello VM.</span><span class="sxs-lookup"><span data-stu-id="d8473-131">Add hello NIC toohello VM.</span></span>

    ```powershell
    $vmConfig = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $nic.Id -Primary
    ```

7. <span data-ttu-id="d8473-132">Crie Olá VM.</span><span class="sxs-lookup"><span data-stu-id="d8473-132">Create hello VM.</span></span>

    ```powershell
    New-AzureRmVM -VM $vmConfig -ResourceGroupName $rgName -Location $location
    ```

8. <span data-ttu-id="d8473-133">Guarde o ficheiro de script de Olá.</span><span class="sxs-lookup"><span data-stu-id="d8473-133">Save hello script file.</span></span>

## <a name="step-4---run-hello-script"></a><span data-ttu-id="d8473-134">Passo 4 - executar Olá script</span><span class="sxs-lookup"><span data-stu-id="d8473-134">Step 4 - Run hello script</span></span>
<span data-ttu-id="d8473-135">Depois de efetuar as alterações necessárias e compreender o script de Olá Mostrar acima, execute o script de Olá.</span><span class="sxs-lookup"><span data-stu-id="d8473-135">After making any necessary changes, and understanding hello script show above, run hello script.</span></span> 

1. <span data-ttu-id="d8473-136">A partir de uma consola do PowerShell, ou o ISE do PowerShell, execute o script Olá acima.</span><span class="sxs-lookup"><span data-stu-id="d8473-136">From a PowerShell console, or PowerShell ISE, run hello script above.</span></span>
2. <span data-ttu-id="d8473-137">Olá seguinte resultado deverá ser apresentada após alguns minutos:</span><span class="sxs-lookup"><span data-stu-id="d8473-137">hello following output should be displayed after a few minutes:</span></span>
   
        ResourceGroupName : IaaSStory
        Location          : westus
        ProvisioningState : Succeeded
        Tags              : 
        ResourceId        : /subscriptions/[Subscription ID]/resourceGroups/IaaSStory
   
        AddressSpace      : Microsoft.Azure.Commands.Network.Models.PSAddressSpace
        DhcpOptions       : Microsoft.Azure.Commands.Network.Models.PSDhcpOptions
        Subnets           : {FrontEnd}
        ProvisioningState : Succeeded
        AddressSpaceText  : {
                              "AddressPrefixes": [
                                "192.168.0.0/16"
                              ]
                            }
        DhcpOptionsText   : {}
        SubnetsText       : [
                              {
                                "Name": "FrontEnd",
                                "AddressPrefix": "192.168.1.0/24"
                              }
                            ]
        ResourceGroupName : IaaSStory
        Location          : westus
        ResourceGuid      : [Id]
        Tag               : {}
        TagsTable         : 
        Name              : WTestVNet
        Etag              : W/"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
        Id                : /subscriptions/[Subscription ID]/resourceGroups/IaaSStory/providers/Microsoft.Network/virtualNetworks/WTestVNet
   
        AddressSpace      : Microsoft.Azure.Commands.Network.Models.PSAddressSpace
        DhcpOptions       : Microsoft.Azure.Commands.Network.Models.PSDhcpOptions
        Subnets           : {FrontEnd}
        ProvisioningState : Succeeded
        AddressSpaceText  : {
                              "AddressPrefixes": [
                                "192.168.0.0/16"
                              ]
                            }
        DhcpOptionsText   : {
                              "DnsServers": []
                            }
        SubnetsText       : [
                              {
                                "Name": "FrontEnd",
                                "Etag": [Id],
                                "Id": "/subscriptions/[Subscription ID]/resourceGroups/IaaSStory/providers/Microsoft.Network/virtualNetworks/WTestVNet/subnets/FrontEnd",
                                "AddressPrefix": "192.168.1.0/24",
                                "IpConfigurations": [],
                                "ProvisioningState": "Succeeded"
                              }
                            ]
        ResourceGroupName : IaaSStory
        Location          : westus
        ResourceGuid      : [Id]
        Tag               : {}
        TagsTable         : 
        Name              : WTestVNet
        Etag              : [Id]
        Id                : /subscriptions/[Subscription Id]/resourceGroups/IaaSStory/providers/Microsoft.Network/virtualNetworks/WTestVNet
   
        TrackingOperationId : [Id]
        RequestId           : [Id]
        Status              : Succeeded
        StatusCode          : OK
        Output              : 
        StartTime           : [Subscription Id]
        EndTime             : [Subscription Id]
        Error               : 
        ErrorText           : 

