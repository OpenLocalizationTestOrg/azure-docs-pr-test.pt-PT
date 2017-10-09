---
title: "aaaManage VMs num conjunto de dimensionamento de Máquina Virtual | Microsoft Docs"
description: "Gerir máquinas virtuais num conjunto com o Azure PowerShell de dimensionamento de máquina virtual."
services: virtual-machine-scale-sets
documentationcenter: 
author: Thraka
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: d35fa77a-de96-4ccd-a332-eb181d1f4273
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/27/2016
ms.author: adegeo
ms.openlocfilehash: 7d848729c0fc708bd596b61feb528cf4bf4bafd4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-virtual-machines-in-a-virtual-machine-scale-set"></a><span data-ttu-id="da2f9-103">Gerir máquinas virtuais num conjunto de dimensionamento de máquina virtual</span><span class="sxs-lookup"><span data-stu-id="da2f9-103">Manage virtual machines in a virtual machine scale set</span></span>
<span data-ttu-id="da2f9-104">Utilize tarefas de Olá nas máquinas virtuais de toomanage artigo no seu conjunto de dimensionamento de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="da2f9-104">Use hello tasks in this article toomanage virtual machines in your virtual machine scale set.</span></span>

<span data-ttu-id="da2f9-105">Na maioria das tarefas de Olá que envolvam a gerir uma máquina virtual num conjunto de dimensionamento necessita que sabe o ID de instância de Olá da máquina de Olá que pretende que o toomanage.</span><span class="sxs-lookup"><span data-stu-id="da2f9-105">Most of hello tasks that involve managing a virtual machine in a scale set require that you know hello instance ID of hello machine that you want toomanage.</span></span> <span data-ttu-id="da2f9-106">Pode utilizar [Explorador de recursos do Azure](https://resources.azure.com) toofind Olá ID de instância de uma máquina virtual num conjunto de dimensionamento.</span><span class="sxs-lookup"><span data-stu-id="da2f9-106">You can use [Azure Resource Explorer](https://resources.azure.com) toofind hello instance ID of a virtual machine in a scale set.</span></span> <span data-ttu-id="da2f9-107">Também é utilizar o Explorador de recursos tooverify Olá Estado Olá tarefas que termina.</span><span class="sxs-lookup"><span data-stu-id="da2f9-107">You also use Resource Explorer tooverify hello status of hello tasks that you finish.</span></span>

<span data-ttu-id="da2f9-108">Consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview) para obter informações sobre instalar Olá a versão mais recente do Azure PowerShell, selecionar a sua subscrição e início de sessão na conta tooyour.</span><span class="sxs-lookup"><span data-stu-id="da2f9-108">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for information about installing hello latest version of Azure PowerShell, selecting your subscription, and signing in tooyour account.</span></span>

## <a name="display-information-about-a-scale-set"></a><span data-ttu-id="da2f9-109">Apresentar informações sobre um conjunto de dimensionamento</span><span class="sxs-lookup"><span data-stu-id="da2f9-109">Display information about a scale set</span></span>
<span data-ttu-id="da2f9-110">Pode obter informações gerais sobre um conjunto de dimensionamento, que também seja vista de instância de Olá tooas referenciado.</span><span class="sxs-lookup"><span data-stu-id="da2f9-110">You can get general information about a scale set, which is also referred tooas hello instance view.</span></span> <span data-ttu-id="da2f9-111">Em alternativa, pode obter informações mais específicas, tais como informações sobre recursos de Olá no conjunto de dimensionamento de Olá.</span><span class="sxs-lookup"><span data-stu-id="da2f9-111">Or, you can get more specific information, such as information about hello resources in hello scale set.</span></span>

<span data-ttu-id="da2f9-112">Substitua Olá entre aspas valores com o nome de Olá ou o grupo de recursos e a escala definido e, em seguida, execute o comando de Olá:</span><span class="sxs-lookup"><span data-stu-id="da2f9-112">Replace hello quoted values with hello name or your resource group and scale set and then run hello command:</span></span>

    Get-AzureRmVmss -ResourceGroupName "resource group name" -VMScaleSetName "scale set name"

<span data-ttu-id="da2f9-113">Devolve algo semelhante ao seguinte:</span><span class="sxs-lookup"><span data-stu-id="da2f9-113">It returns something like this:</span></span>

    Id                                          : /subscriptions/{sub-id}/resourceGroups/myrg1/providers/Microsoft.Compute/virtualMachineScaleSets/myvmss1
    Name                                        : myvmss1
    Type                                        : Microsoft.Compute/virtualMachineScaleSets
    Location                                    : centralus
    Sku                                         :
      Name                                      : Standard_A0
      Tier                                      : Standard
      Capacity                                  : 3
    UpgradePolicy                               :
      Mode                                      : Manual
    VirtualMachineProfile                       :
      OsProfile                                 :
        ComputerNamePrefix                      : vmss1
        AdminUsername                           : admin1
        WindowsConfiguration                    :
          ProvisionVMAgent                      : True
          EnableAutomaticUpdates                : True
    StorageProfile                              :
      ImageReference                            :
        Publisher                               : MicrosoftWindowsServer
        Offer                                   : WindowsServer
        Sku                                     : 2012-R2-Datacenter
        Version                                 : latest
      OsDisk                                    :
        Name                                    : vmssosdisk
        Caching                                 : ReadOnly
        CreateOption                            : FromImage
        VhdContainers[0]                        : https://astore.blob.core.windows.net/vmss
        VhdContainers[1]                        : https://gstore.blob.core.windows.net/vmss
        VhdContainers[2]                        : https://mstore.blob.core.windows.net/vmss
        VhdContainers[3]                        : https://sstore.blob.core.windows.net/vmss
        VhdContainers[4]                        : https://ystore.blob.core.windows.net/vmss
    NetworkProfile                              :
      NetworkInterfaceConfigurations[0]         :
        Name                                    : mync1
        Primary                                 : True
        IpConfigurations[0]                     :
          Name                                  : ip1
          Subnet                                :
            Id                                  : /subscriptions/{sub-id}/resourceGroups/myrg1/providers/Microsoft.Network/virtualNetworks/myvn1/subnets/mysn1
          LoadBalancerBackendAddressPools[0]    :
            Id                                  : /subscriptions/{sub-id}/resourceGroups/myrg1/providers/Microsoft.Network/loadBalancers/mylb1/backendAddressPools/bepool1
        LoadBalancerInboundNatPools[0]          :
            Id                                  : /subscriptions/{sub-id}/resourceGroups/myrg1/providers/Microsoft.Network/loadBalancers/mylb1/inboundNatPools/natpool1
    ExtensionProfile                            :
      Extensions[0]                             :
        Name                                    : Microsoft.Insights.VMDiagnosticsSettings
        Publisher                               : Microsoft.Azure.Diagnostics
        Type                                    : IaaSDiagnostics
        TypeHandlerVersion                      : 1.5
        AutoUpgradeMinorVersion                 : True
        Settings                                : {"xmlCfg":"...","storageAccount":"astore"}
    ProvisioningState                           : Succeeded

<span data-ttu-id="da2f9-114">Substitua Olá entre aspas valores com o nome de Olá do seu conjunto de grupo e o dimensionamento do recurso.</span><span class="sxs-lookup"><span data-stu-id="da2f9-114">Replace hello quoted values with hello name of your resource group and scale set.</span></span> <span data-ttu-id="da2f9-115">Substitua  *#*  com o identificador de instância de Olá da máquina virtual de Olá que pretende tooget informações sobre e, em seguida, executá-lo:</span><span class="sxs-lookup"><span data-stu-id="da2f9-115">Replace *#* with hello instance identifier of hello virtual machine that you want tooget information about and then run it:</span></span>

    Get-AzureRmVmssVM -ResourceGroupName "resource group name" -VMScaleSetName "scale set name" -InstanceId #

<span data-ttu-id="da2f9-116">Devolve algo semelhante a este exemplo:</span><span class="sxs-lookup"><span data-stu-id="da2f9-116">It returns something like this example:</span></span>

    Id                            : /subscriptions/{sub-id}/resourceGroups/myrg1/providers/Microsoft.Compute/
                                    virtualMachineScaleSets/myvmss1/virtualMachines/0
    Name                          : myvmss1_0
    Type                          : Microsoft.Compute/virtualMachineScaleSets/virtualMachines
    Location                      : centralus
    InstanceId                    : 0
    Sku                           :
      Name                        : Standard_A0
      Tier                        : Standard
    LatestModelApplied            : True
    StorageProfile                :
      ImageReference              :
        Publisher                 : MicrosoftWindowsServer
        Offer                     : WindowsServer
        Sku                       : 2012-R2-Datacenter
        Version                   : 4.0.20160617
      OsDisk                      :
        OsType                    : Windows
        Name                      : vmssosdisk-os-0-e11cad52959b4b76a8d9f26c5190c4f8
        Vhd                       :
          Uri                     : https://astore.blob.core.windows.net/vmss/vmssosdisk-os-0-e11cad52959b4b76a8d9f26c5190c4f8.vhd
        Caching                   : ReadOnly
        CreateOption              : FromImage
    OsProfile                     :
      ComputerName                : myvmss1-0
      AdminUsername               : admin1
      WindowsConfiguration        :
        ProvisionVMAgent          : True
        EnableAutomaticUpdates    : True
    NetworkProfile                :
      NetworkInterfaces[0]        :
        Id                        : /subscriptions/{sub-id}/resourceGroups/myrg1/providers/Microsoft.Compute/virtualMachineScaleSets/
                                    myvmss1/virtualMachines/0/networkInterfaces/mync1
    ProvisioningState             : Succeeded
    Resources[0]                  :
      Id                          : /subscriptions/{sub-id}/resourceGroups/myrg1/providers/Microsoft.Compute/virtualMachines/
                                    myvmss1_0/extensions/Microsoft.Insights.VMDiagnosticsSettings
      Name                        : Microsoft.Insights.VMDiagnosticsSettings
      Type                        : Microsoft.Compute/virtualMachines/extensions
      Location                    : centralus
      Publisher                   : Microsoft.Azure.Diagnostics
      VirtualMachineExtensionType : IaaSDiagnostics
      TypeHandlerVersion          : 1.5
      AutoUpgradeMinorVersion     : True
      Settings                    : {"xmlCfg":"...","storageAccount":"astore"}
      ProvisioningState           : Succeeded

## <a name="start-a-virtual-machine-in-a-scale-set"></a><span data-ttu-id="da2f9-117">Iniciar uma máquina virtual num conjunto de dimensionamento</span><span class="sxs-lookup"><span data-stu-id="da2f9-117">Start a virtual machine in a scale set</span></span>
<span data-ttu-id="da2f9-118">Substitua Olá entre aspas valores com o nome de Olá do seu conjunto de grupo e o dimensionamento do recurso.</span><span class="sxs-lookup"><span data-stu-id="da2f9-118">Replace hello quoted values with hello name of your resource group and scale set.</span></span> <span data-ttu-id="da2f9-119">Substitua  *#*  com o identificador de Olá da máquina virtual de Olá que pretende toostart e, em seguida, executá-lo:</span><span class="sxs-lookup"><span data-stu-id="da2f9-119">Replace *#* with hello identifier of hello virtual machine that you want toostart and then run it:</span></span>

    Start-AzureRmVmss -ResourceGroupName "resource group name" -VMScaleSetName "scale set name" -InstanceId #

<span data-ttu-id="da2f9-120">No Explorador de recursos, é possível ver que Olá estado da instância de Olá é **executar**:</span><span class="sxs-lookup"><span data-stu-id="da2f9-120">In Resource Explorer, we can see that hello status of hello instance is **running**:</span></span>

    "statuses": [
      {
        "code": "ProvisioningState/succeeded",
        "level": "Info",
        "displayStatus": "Provisioning succeeded",
        "time": "2016-03-15T02:10:08.0730839+00:00"
      },
      {
        "code": "PowerState/running",
        "level": "Info",
        "displayStatus": "VM running"
      }
    ]

<span data-ttu-id="da2f9-121">Pode começar a todas as máquinas de virtuais Olá na escala de Olá definida por não utilizar o parâmetro - InstanceId de Olá.</span><span class="sxs-lookup"><span data-stu-id="da2f9-121">You can start all hello virtual machines in hello scale set by not using hello -InstanceId parameter.</span></span>

## <a name="stop-a-virtual-machine-in-a-scale-set"></a><span data-ttu-id="da2f9-122">Parar uma máquina virtual num conjunto de dimensionamento</span><span class="sxs-lookup"><span data-stu-id="da2f9-122">Stop a virtual machine in a scale set</span></span>
<span data-ttu-id="da2f9-123">Substitua Olá entre aspas valores com o nome de Olá do seu conjunto de grupo e o dimensionamento do recurso.</span><span class="sxs-lookup"><span data-stu-id="da2f9-123">Replace hello quoted values with hello name of your resource group and scale set.</span></span> <span data-ttu-id="da2f9-124">Substitua  *#*  com o identificador de Olá da máquina virtual de Olá que pretende toostop e, em seguida, executá-lo:</span><span class="sxs-lookup"><span data-stu-id="da2f9-124">Replace *#* with hello identifier of hello virtual machine that you want toostop and then run it:</span></span>

    Stop-AzureRmVmss -ResourceGroupName "resource group name" -VMScaleSetName "scale set name" -InstanceId #

<span data-ttu-id="da2f9-125">No Explorador de recursos, é possível ver que Olá estado da instância de Olá é **desalocada**:</span><span class="sxs-lookup"><span data-stu-id="da2f9-125">In Resource Explorer, we can see that hello status of hello instance is **deallocated**:</span></span>

    "statuses": [
      {
        "code": "ProvisioningState/succeeded",
        "level": "Info",
        "displayStatus": "Provisioning succeeded",
        "time": "2016-03-15T01:25:17.8792929+00:00"
      },
      {
        "code": "PowerState/deallocated",
        "level": "Info",
        "displayStatus": "VM deallocated"
      }
    ]

<span data-ttu-id="da2f9-126">toostop uma máquina virtual e não desalocá-lo, utilize o parâmetro - StayProvisioned de Olá.</span><span class="sxs-lookup"><span data-stu-id="da2f9-126">toostop a virtual machine and not deallocate it, use hello -StayProvisioned parameter.</span></span> <span data-ttu-id="da2f9-127">Pode parar todas as máquinas de virtuais de Olá Olá definido por não utilizar o parâmetro - InstanceId de Olá.</span><span class="sxs-lookup"><span data-stu-id="da2f9-127">You can stop all hello virtual machines in hello set by not using hello -InstanceId parameter.</span></span>

## <a name="restart-a-virtual-machine-in-a-scale-set"></a><span data-ttu-id="da2f9-128">Reiniciar uma máquina virtual num conjunto de dimensionamento</span><span class="sxs-lookup"><span data-stu-id="da2f9-128">Restart a virtual machine in a scale set</span></span>
<span data-ttu-id="da2f9-129">Substitua Olá entre aspas valores com o nome de Olá do seu conjunto de dimensionamento de grupo e Olá recursos.</span><span class="sxs-lookup"><span data-stu-id="da2f9-129">Replace hello quoted values with hello name of your resource group and hello scale set.</span></span> <span data-ttu-id="da2f9-130">Substitua  *#*  com o identificador de Olá da máquina virtual de Olá que pretende toorestart e, em seguida, executá-lo:</span><span class="sxs-lookup"><span data-stu-id="da2f9-130">Replace *#* with hello identifier of hello virtual machine that you want toorestart and then run it:</span></span>

    Restart-AzureRmVmss -ResourceGroupName "resource group name" -VMScaleSetName "scale set name" -InstanceId #

<span data-ttu-id="da2f9-131">Todas as máquinas de virtuais Olá pode ser reiniciado no Olá definido por não utilizar o parâmetro - InstanceId de Olá.</span><span class="sxs-lookup"><span data-stu-id="da2f9-131">You can restart all hello virtual machines in hello set by not using hello -InstanceId parameter.</span></span>

## <a name="remove-a-virtual-machine-from-a-scale-set"></a><span data-ttu-id="da2f9-132">Remover uma máquina virtual a partir de um conjunto de dimensionamento</span><span class="sxs-lookup"><span data-stu-id="da2f9-132">Remove a virtual machine from a scale set</span></span>
<span data-ttu-id="da2f9-133">Substitua Olá entre aspas valores com o nome de Olá do seu conjunto de dimensionamento de grupo e Olá recursos.</span><span class="sxs-lookup"><span data-stu-id="da2f9-133">Replace hello quoted values with hello name of your resource group and hello scale set.</span></span> <span data-ttu-id="da2f9-134">Substitua  *#*  com o identificador de Olá da máquina virtual de Olá que pretende tooremove e, em seguida, executá-lo:</span><span class="sxs-lookup"><span data-stu-id="da2f9-134">Replace *#* with hello identifier of hello virtual machine that you want tooremove and then run it:</span></span>  

    Remove-AzureRmVmss -ResourceGroupName "resource group name" –VMScaleSetName "scale set name" -InstanceId #

<span data-ttu-id="da2f9-135">Pode remover o conjunto de dimensionamento de máquina virtual de Olá, uma vez por não utilizar o parâmetro - InstanceId de Olá.</span><span class="sxs-lookup"><span data-stu-id="da2f9-135">You can remove hello virtual machine scale set all at once by not using hello -InstanceId parameter.</span></span>

## <a name="change-hello-capacity-of-a-scale-set"></a><span data-ttu-id="da2f9-136">Capacidade de Olá de alteração de um conjunto de dimensionamento</span><span class="sxs-lookup"><span data-stu-id="da2f9-136">Change hello capacity of a scale set</span></span>
<span data-ttu-id="da2f9-137">Pode adicionar ou remover máquinas virtuais alterando a capacidade de Olá do conjunto de Olá.</span><span class="sxs-lookup"><span data-stu-id="da2f9-137">You can add or remove virtual machines by changing hello capacity of hello set.</span></span> <span data-ttu-id="da2f9-138">Obter conjunto de dimensionamento de Olá que pretende que sejam toochange, conjunto Olá capacidade toowhat querer toobe e, em seguida, atualizar o conjunto de dimensionamento de Olá com a nova capacidade de Olá.</span><span class="sxs-lookup"><span data-stu-id="da2f9-138">Get hello scale set that you want toochange, set hello capacity toowhat you want it toobe, and then update hello scale set with hello new capacity.</span></span> <span data-ttu-id="da2f9-139">Nestes comandos, substitua Olá entre aspas valores com o nome de Olá do seu conjunto de dimensionamento de grupo e Olá recursos.</span><span class="sxs-lookup"><span data-stu-id="da2f9-139">In these commands, replace hello quoted values with hello name of your resource group and hello scale set.</span></span>

    $vmss = Get-AzureRmVmss -ResourceGroupName "resource group name" -VMScaleSetName "scale set name"
    $vmss.sku.capacity = 5
    Update-AzureRmVmss -ResourceGroupName "resource group name" -Name "scale set name" -VirtualMachineScaleSet $vmss 

<span data-ttu-id="da2f9-140">Se estiver a remover máquinas virtuais do conjunto de dimensionamento de Olá, máquinas virtuais Olá com ids mais elevados de Olá são removidas pela primeira vez.</span><span class="sxs-lookup"><span data-stu-id="da2f9-140">If you are removing virtual machines from hello scale set, hello virtual machines with hello highest ids are removed first.</span></span>

