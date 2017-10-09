---
title: "aaaConvert uma máquina virtual do Windows de não discos discos toomanaged - discos gerida do Azure | Microsoft Docs"
description: "Como tooconvert uma VM do Windows de discos não gerido toomanaged discos utilizando o PowerShell no modelo de implementação do Resource Manager Olá"
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: cynthn
ms.openlocfilehash: e8ed8694b0e776d22df26261e2fc8340bfe5cafa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="convert-a-windows-virtual-machine-from-unmanaged-disks-toomanaged-disks"></a><span data-ttu-id="fdb9f-103">Converter uma máquina virtual do Windows de discos de toomanaged discos não gerido</span><span class="sxs-lookup"><span data-stu-id="fdb9f-103">Convert a Windows virtual machine from unmanaged disks toomanaged disks</span></span>

<span data-ttu-id="fdb9f-104">Se tiver existentes máquinas virtuais (VMs Windows) que utilizam discos não geridos, pode converter Olá VMs toouse gerido discos através de Olá [Azure geridos discos](managed-disks-overview.md) serviço.</span><span class="sxs-lookup"><span data-stu-id="fdb9f-104">If you have existing Windows virtual machines (VMs) that use unmanaged disks, you can convert hello VMs toouse managed disks through hello [Azure Managed Disks](managed-disks-overview.md) service.</span></span> <span data-ttu-id="fdb9f-105">Este processo converte o disco de Olá SO e discos de dados anexados.</span><span class="sxs-lookup"><span data-stu-id="fdb9f-105">This process converts both hello OS disk and any attached data disks.</span></span>

<span data-ttu-id="fdb9f-106">Este artigo mostra como tooconvert VMs com o Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="fdb9f-106">This article shows you how tooconvert VMs by using Azure PowerShell.</span></span> <span data-ttu-id="fdb9f-107">Se precisar de tooinstall ou atualizá-lo, consulte [instalar e configurar o Azure PowerShell](/powershell/azure/install-azurerm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="fdb9f-107">If you need tooinstall or upgrade it, see [Install and configure Azure PowerShell](/powershell/azure/install-azurerm-ps.md).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="fdb9f-108">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="fdb9f-108">Before you begin</span></span>


* <span data-ttu-id="fdb9f-109">Reveja [planear a migração de Olá tooManaged discos](on-prem-to-azure.md#plan-for-the-migration-to-managed-disks).</span><span class="sxs-lookup"><span data-stu-id="fdb9f-109">Review [Plan for hello migration tooManaged Disks](on-prem-to-azure.md#plan-for-the-migration-to-managed-disks).</span></span>

[!INCLUDE [virtual-machines-common-convert-disks-considerations](../../../includes/virtual-machines-common-convert-disks-considerations.md)]




## <a name="convert-single-instance-vms"></a><span data-ttu-id="fdb9f-110">Converter a VMs de instância única</span><span class="sxs-lookup"><span data-stu-id="fdb9f-110">Convert single-instance VMs</span></span>
<span data-ttu-id="fdb9f-111">Esta secção abrange como tooconvert single-instance as VMs do Azure de não discos toomanaged discos.</span><span class="sxs-lookup"><span data-stu-id="fdb9f-111">This section covers how tooconvert single-instance Azure VMs from unmanaged disks toomanaged disks.</span></span> <span data-ttu-id="fdb9f-112">(Se as suas VMs num conjunto de disponibilidade, consulte o secção seguinte Olá.)</span><span class="sxs-lookup"><span data-stu-id="fdb9f-112">(If your VMs are in an availability set, see hello next section.)</span></span> 

1. <span data-ttu-id="fdb9f-113">Desalocar Olá VM utilizando Olá [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="fdb9f-113">Deallocate hello VM by using hello [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm) cmdlet.</span></span> <span data-ttu-id="fdb9f-114">Olá exemplo seguinte deallocates Olá VM com o nome `myVM` no grupo de recursos de Olá designado `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="fdb9f-114">hello following example deallocates hello VM named `myVM` in hello resource group named `myResourceGroup`:</span></span> 

  ```powershell
  $rgName = "myResourceGroup"
  $vmName = "myVM"
  Stop-AzureRmVM -ResourceGroupName $rgName -Name $vmName -Force
  ```

2. <span data-ttu-id="fdb9f-115">Converta os discos de toomanaged VM de Olá utilizando Olá [ConvertTo-AzureRmVMManagedDisk](/powershell/module/azurerm.compute/convertto-azurermvmmanageddisk) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="fdb9f-115">Convert hello VM toomanaged disks by using hello [ConvertTo-AzureRmVMManagedDisk](/powershell/module/azurerm.compute/convertto-azurermvmmanageddisk) cmdlet.</span></span> <span data-ttu-id="fdb9f-116">Olá seguir o processo converte Olá VM anterior, incluindo disco Olá SO e discos de dados:</span><span class="sxs-lookup"><span data-stu-id="fdb9f-116">hello following process converts hello previous VM, including hello OS disk and any data disks:</span></span>

  ```powershell
  ConvertTo-AzureRmVMManagedDisk -ResourceGroupName $rgName -VMName $vmName
  ```

3. <span data-ttu-id="fdb9f-117">Iniciar Olá VM após a discos de toomanaged de conversão de Olá utilizando [Start-AzureRmVM](/powershell/module/azurerm.compute/start-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="fdb9f-117">Start hello VM after hello conversion toomanaged disks by using [Start-AzureRmVM](/powershell/module/azurerm.compute/start-azurermvm).</span></span> <span data-ttu-id="fdb9f-118">Olá reinícios de exemplo a seguir Olá VM anterior:</span><span class="sxs-lookup"><span data-stu-id="fdb9f-118">hello following example restarts hello previous VM:</span></span>

  ```powershell
  Start-AzureRmVM -ResourceGroupName $rgName -Name $vmName
  ```


## <a name="convert-vms-in-an-availability-set"></a><span data-ttu-id="fdb9f-119">Converter VMs num conjunto de disponibilidade</span><span class="sxs-lookup"><span data-stu-id="fdb9f-119">Convert VMs in an availability set</span></span>

<span data-ttu-id="fdb9f-120">Se Olá VMs que pretende que sejam tooconvert toomanaged discos estão num conjunto de disponibilidade, terá primeiro tooconvert Olá disponibilidade conjunto tooa gerido conjunto de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="fdb9f-120">If hello VMs that you want tooconvert toomanaged disks are in an availability set, you first need tooconvert hello availability set tooa managed availability set.</span></span>

1. <span data-ttu-id="fdb9f-121">Converter o conjunto, utilizando Olá de disponibilidade de Olá [atualização AzureRmAvailabilitySet](/powershell/module/azurerm.compute/update-azurermavailabilityset) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="fdb9f-121">Convert hello availability set by using hello [Update-AzureRmAvailabilitySet](/powershell/module/azurerm.compute/update-azurermavailabilityset) cmdlet.</span></span> <span data-ttu-id="fdb9f-122">Olá seguinte o exemplo de atualizações Olá conjunto nomeada de disponibilidade `myAvailabilitySet` no grupo de recursos de Olá designado `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="fdb9f-122">hello following example updates hello availability set named `myAvailabilitySet` in hello resource group named `myResourceGroup`:</span></span>

  ```powershell
  $rgName = 'myResourceGroup'
  $avSetName = 'myAvailabilitySet'

  $avSet = Get-AzureRmAvailabilitySet -ResourceGroupName $rgName -Name $avSetName
  Update-AzureRmAvailabilitySet -AvailabilitySet $avSet -Sku Aligned 
  ```

  <span data-ttu-id="fdb9f-123">Se a região de olá onde está localizado o conjunto de disponibilidade tem apenas 2 domínios de falhas gerido, mas Olá número de domínios de falhas não gerido 3, este comando apresenta um erro semelhante demasiado "Olá especificado o número de domínios de falhas 3 tem de pertencer Olá intervalo 1 too2."</span><span class="sxs-lookup"><span data-stu-id="fdb9f-123">If hello region where your availability set is located has only 2 managed fault domains but hello number of unmanaged fault domains is 3, this command shows an error similar too"hello specified fault domain count 3 must fall in hello range 1 too2."</span></span> <span data-ttu-id="fdb9f-124">tooresolve Olá erro, too2 de domínio de falhas de Olá de atualização e atualização `Sku` demasiado`Aligned` da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="fdb9f-124">tooresolve hello error, update hello fault domain too2 and update `Sku` too`Aligned` as follows:</span></span>

  ```powershell
  $avSet.PlatformFaultDomainCount = 2
  Update-AzureRmAvailabilitySet -AvailabilitySet $avSet -Sku Aligned
  ```

2. <span data-ttu-id="fdb9f-125">Desalocar e converter Olá VMs no conjunto de disponibilidade de Olá.</span><span class="sxs-lookup"><span data-stu-id="fdb9f-125">Deallocate and convert hello VMs in hello availability set.</span></span> <span data-ttu-id="fdb9f-126">Olá seguinte script deallocates cada VM utilizando Olá [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm) cmdlet, converte-o utilizando [ConvertTo-AzureRmVMManagedDisk](/powershell/module/azurerm.compute/convertto-azurermvmmanageddisk)e reinicia-lo utilizando [Start-AzureRmVM ](/powershell/module/azurerm.compute/start-azurermvm):</span><span class="sxs-lookup"><span data-stu-id="fdb9f-126">hello following script deallocates each VM by using hello [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm) cmdlet, converts it by using [ConvertTo-AzureRmVMManagedDisk](/powershell/module/azurerm.compute/convertto-azurermvmmanageddisk), and restarts it by using [Start-AzureRmVM](/powershell/module/azurerm.compute/start-azurermvm):</span></span>

  ```powershell
  $avSet = Get-AzureRmAvailabilitySet -ResourceGroupName $rgName -Name $avSetName

  foreach($vmInfo in $avSet.VirtualMachinesReferences)
  {
     $vm = Get-AzureRmVM -ResourceGroupName $rgName | Where-Object {$_.Id -eq $vmInfo.id}
     Stop-AzureRmVM -ResourceGroupName $rgName -Name $vm.Name -Force
     ConvertTo-AzureRmVMManagedDisk -ResourceGroupName $rgName -VMName $vm.Name
     Start-AzureRmVM -ResourceGroupName $rgName -Name $vmName
  }
  ```


## <a name="troubleshooting"></a><span data-ttu-id="fdb9f-127">Resolução de problemas</span><span class="sxs-lookup"><span data-stu-id="fdb9f-127">Troubleshooting</span></span>

<span data-ttu-id="fdb9f-128">Se ocorrer um erro durante a conversão, ou se uma VM está em estado de falha devido a problemas de uma conversão anterior, execute Olá `ConvertTo-AzureRmVMManagedDisk` cmdlet novamente.</span><span class="sxs-lookup"><span data-stu-id="fdb9f-128">If there is an error during conversion, or if a VM is in a failed state because of issues in a previous conversion, run hello `ConvertTo-AzureRmVMManagedDisk` cmdlet again.</span></span> <span data-ttu-id="fdb9f-129">Uma repetição simple normalmente unblocks situação Olá.</span><span class="sxs-lookup"><span data-stu-id="fdb9f-129">A simple retry usually unblocks hello situation.</span></span>


## <a name="next-steps"></a><span data-ttu-id="fdb9f-130">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="fdb9f-130">Next steps</span></span>

[<span data-ttu-id="fdb9f-131">Converter discos geridos padrão toopremium</span><span class="sxs-lookup"><span data-stu-id="fdb9f-131">Convert standard managed disks toopremium</span></span>](convert-disk-storage.md)

<span data-ttu-id="fdb9f-132">Efetuar uma cópia só de leitura de uma VM utilizando [instantâneos](snapshot-copy-managed-disk.md).</span><span class="sxs-lookup"><span data-stu-id="fdb9f-132">Take a read-only copy of a VM by using [snapshots](snapshot-copy-managed-disk.md).</span></span>

