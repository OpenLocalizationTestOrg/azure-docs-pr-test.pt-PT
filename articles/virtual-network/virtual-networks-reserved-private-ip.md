---
title: "aaaStatic clássico IP - VM do Azure - privado interno"
description: "Noções sobre IPs interno estático (DIPs) e como toomanage-las"
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
ms.assetid: 93444c6f-af1b-41f8-a035-77f5c0302bf0
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/22/2016
ms.author: jdial
ms.openlocfilehash: 5abe1c59f2f3ed19bcf56c269dfe57ac32d4f601
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooset-a-static-internal-private-ip-address-using-powershell-classic"></a><span data-ttu-id="6dc66-103">Como tooset um IP estático de privada interno endereços através do PowerShell (clássica)</span><span class="sxs-lookup"><span data-stu-id="6dc66-103">How tooset a static internal private IP address using PowerShell (Classic)</span></span>
<span data-ttu-id="6dc66-104">Na maioria dos casos, não terá toospecify um endereço IP estático interno para a máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="6dc66-104">In most cases, you won’t need toospecify a static internal IP address for your virtual machine.</span></span> <span data-ttu-id="6dc66-105">As VMs numa rede virtual serão recebem automaticamente um endereço IP de um intervalo que especificou.</span><span class="sxs-lookup"><span data-stu-id="6dc66-105">VMs in a virtual network will automatically receive an internal IP address from a range that you specify.</span></span> <span data-ttu-id="6dc66-106">Mas em certos casos, a especificação de um endereço IP estático para uma VM específica faz sentido.</span><span class="sxs-lookup"><span data-stu-id="6dc66-106">But in certain cases, specifying a static IP address for a particular VM makes sense.</span></span> <span data-ttu-id="6dc66-107">Por exemplo, se a VM está curso toorun DNS ou será um controlador de domínio.</span><span class="sxs-lookup"><span data-stu-id="6dc66-107">For example, if your VM is going toorun DNS or will be a domain controller.</span></span> <span data-ttu-id="6dc66-108">Um endereço IP estático interno permanece com Olá VM mesmo através de um Estado de paragem/desaprovisionamento.</span><span class="sxs-lookup"><span data-stu-id="6dc66-108">A static internal IP address stays with hello VM even through a stop/deprovision state.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="6dc66-109">O Azure tem dois modelos de implementação diferentes para criar e trabalhar com os recursos: [Resource Manager e clássico](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="6dc66-109">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="6dc66-110">Este artigo abrange utilizando o modelo de implementação clássica Olá.</span><span class="sxs-lookup"><span data-stu-id="6dc66-110">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="6dc66-111">A Microsoft recomenda que a maioria das implementações novas utilizem Olá [modelo de implementação do Resource Manager](virtual-networks-static-private-ip-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="6dc66-111">Microsoft recommends that most new deployments use hello [Resource Manager deployment model](virtual-networks-static-private-ip-arm-ps.md).</span></span>
> 
> 

## <a name="how-tooverify-if-a-specific-ip-address-is-available"></a><span data-ttu-id="6dc66-112">Como tooverify esteja disponível um endereço IP específico</span><span class="sxs-lookup"><span data-stu-id="6dc66-112">How tooverify if a specific IP address is available</span></span>
<span data-ttu-id="6dc66-113">tooverify se hello endereço IP *10.0.0.7* está disponível numa vnet com o nome *TestVnet*, execute o seguinte comando do PowerShell de Olá e verifique o valor de Olá para *IsAvailable*:</span><span class="sxs-lookup"><span data-stu-id="6dc66-113">tooverify if hello IP address *10.0.0.7* is available in a vnet named *TestVnet*, run hello following PowerShell command and verify hello value for *IsAvailable*:</span></span>

    Test-AzureStaticVNetIP –VNetName TestVNet –IPAddress 10.0.0.7 

    IsAvailable          : True
    AvailableAddresses   : {}
    OperationDescription : Test-AzureStaticVNetIP
    OperationId          : fd3097e1-5f4b-9cac-8afa-bba1e3492609
    OperationStatus      : Succeeded

> [!NOTE]
> <span data-ttu-id="6dc66-114">Se pretender que o comando de Olá tootest acima num ambiente seguro, siga as diretrizes de Olá no [criar uma rede virtual (clássica)](virtual-networks-create-vnet-classic-pportal.md) toocreate uma vnet com o nome *TestVnet* e certifique-se de que utiliza Olá  *10.0.0.0/8* espaço de endereços.</span><span class="sxs-lookup"><span data-stu-id="6dc66-114">If you want tootest hello command above in a safe environment follow hello guidelines in [Create a virtual network (classic)](virtual-networks-create-vnet-classic-pportal.md) toocreate a vnet named *TestVnet* and ensure it uses hello *10.0.0.0/8* address space.</span></span>
> 
> 

## <a name="how-toospecify-a-static-internal-ip-when-creating-a-vm"></a><span data-ttu-id="6dc66-115">Como toospecify um IP internos estático ao criar uma VM</span><span class="sxs-lookup"><span data-stu-id="6dc66-115">How toospecify a static internal IP when creating a VM</span></span>
<span data-ttu-id="6dc66-116">Olá script do PowerShell abaixo cria um novo serviço em nuvem com o nome *TestService*, em seguida, obtém uma imagem do Azure, em seguida, cria uma VM chamada *TestVM* no Olá novo serviço em nuvem utilizando a imagem Olá obtido, conjuntos de Olá toobe VM numa sub-rede com o nome *sub-rede 1*e define *10.0.0.7* como um IP estático interno para Olá VM:</span><span class="sxs-lookup"><span data-stu-id="6dc66-116">hello PowerShell script below creates a new cloud service named *TestService*, then retrieves an image from Azure, then creates a VM named *TestVM* in hello new cloud service using hello retrieved image, sets hello VM toobe in a subnet named *Subnet-1*, and sets *10.0.0.7* as a static internal IP for hello VM:</span></span>

    New-AzureService -ServiceName TestService -Location "Central US"
    $image = Get-AzureVMImage|?{$_.ImageName -like "*RightImage-Windows-2012R2-x64*"}
    New-AzureVMConfig -Name TestVM -InstanceSize Small -ImageName $image.ImageName `
    | Add-AzureProvisioningConfig -Windows -AdminUsername adminuser -Password MyP@ssw0rd!! `
    | Set-AzureSubnet –SubnetNames Subnet-1 `
    | Set-AzureStaticVNetIP -IPAddress 10.0.0.7 `
    | New-AzureVM -ServiceName "TestService" –VNetName TestVnet

## <a name="how-tooretrieve-static-internal-ip-information-for-a-vm"></a><span data-ttu-id="6dc66-117">Como tooretrieve estáticas internas informações de IP para uma VM</span><span class="sxs-lookup"><span data-stu-id="6dc66-117">How tooretrieve static internal IP information for a VM</span></span>
<span data-ttu-id="6dc66-118">tooview Olá estáticas internas informações de IP para Olá criada a VM com o script de Olá acima, execute o seguinte comando do PowerShell de Olá e observar os valores de Olá para *IpAddress*:</span><span class="sxs-lookup"><span data-stu-id="6dc66-118">tooview hello static internal IP information for hello VM created with hello script above, run hello following PowerShell command and observe hello values for *IpAddress*:</span></span>

    Get-AzureVM -Name TestVM -ServiceName TestService

    DeploymentName              : TestService
    Name                        : TestVM
    Label                       : 
    VM                          : Microsoft.WindowsAzure.Commands.ServiceManagement.Model.PersistentVM
    InstanceStatus              : Provisioning
    IpAddress                   : 10.0.0.7
    InstanceStateDetails        : Windows is preparing your computer for first use...
    PowerState                  : Started
    InstanceErrorCode           : 
    InstanceFaultDomain         : 0
    InstanceName                : TestVM
    InstanceUpgradeDomain       : 0
    InstanceSize                : Small
    HostName                    : rsR2-797
    AvailabilitySetName         : 
    DNSName                     : http://testservice000.cloudapp.net/
    Status                      : Provisioning
    GuestAgentStatus            : Microsoft.WindowsAzure.Commands.ServiceManagement.Model.GuestAgentStatus
    ResourceExtensionStatusList : {Microsoft.Compute.BGInfo}
    PublicIPAddress             : 
    PublicIPName                : 
    NetworkInterfaces           : {}
    ServiceName                 : TestService
    OperationDescription        : Get-AzureVM
    OperationId                 : 34c1560a62f0901ab75cde4fed8e8bd1
    OperationStatus             : OK

## <a name="how-tooremove-a-static-internal-ip-from-a-vm"></a><span data-ttu-id="6dc66-119">Como tooremove um IP estático interno de uma VM</span><span class="sxs-lookup"><span data-stu-id="6dc66-119">How tooremove a static internal IP from a VM</span></span>
<span data-ttu-id="6dc66-120">IP internos estáticos tooremove Olá adicionado toohello VM no script de Olá acima, execute Olá seguinte comando do PowerShell:</span><span class="sxs-lookup"><span data-stu-id="6dc66-120">tooremove hello static internal IP added toohello VM in hello script above, run hello following PowerShell command:</span></span>

    Get-AzureVM -ServiceName TestService -Name TestVM `
    | Remove-AzureStaticVNetIP `
    | Update-AzureVM

## <a name="how-tooadd-a-static-internal-ip-tooan-existing-vm"></a><span data-ttu-id="6dc66-121">Como tooadd um tooan IP estático interno VM existente</span><span class="sxs-lookup"><span data-stu-id="6dc66-121">How tooadd a static internal IP tooan existing VM</span></span>
<span data-ttu-id="6dc66-122">tooadd um toohello IP interno estático VM criada utilizando o script de Olá acima, runt tados os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="6dc66-122">tooadd a static internal IP toohello VM created using hello script above, runt he following command:</span></span>

    Get-AzureVM -ServiceName TestService000 -Name TestVM `
    | Set-AzureStaticVNetIP -IPAddress 10.10.0.7 `
    | Update-AzureVM

## <a name="next-steps"></a><span data-ttu-id="6dc66-123">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="6dc66-123">Next steps</span></span>
[<span data-ttu-id="6dc66-124">IP reservado</span><span class="sxs-lookup"><span data-stu-id="6dc66-124">Reserved IP</span></span>](virtual-networks-reserved-public-ip.md)

[<span data-ttu-id="6dc66-125">IP público de nível de instância (ILPIP)</span><span class="sxs-lookup"><span data-stu-id="6dc66-125">Instance-Level Public IP (ILPIP)</span></span>](virtual-networks-instance-level-public-ip.md)

[<span data-ttu-id="6dc66-126">APIs REST do IP reservado</span><span class="sxs-lookup"><span data-stu-id="6dc66-126">Reserved IP REST APIs</span></span>](https://msdn.microsoft.com/library/azure/dn722420.aspx)

