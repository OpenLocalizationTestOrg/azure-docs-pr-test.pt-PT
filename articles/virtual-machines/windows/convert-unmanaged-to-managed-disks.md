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
# <a name="convert-a-windows-virtual-machine-from-unmanaged-disks-toomanaged-disks"></a>Converter uma máquina virtual do Windows de discos de toomanaged discos não gerido

Se tiver existentes máquinas virtuais (VMs Windows) que utilizam discos não geridos, pode converter Olá VMs toouse gerido discos através de Olá [Azure geridos discos](managed-disks-overview.md) serviço. Este processo converte o disco de Olá SO e discos de dados anexados.

Este artigo mostra como tooconvert VMs com o Azure PowerShell. Se precisar de tooinstall ou atualizá-lo, consulte [instalar e configurar o Azure PowerShell](/powershell/azure/install-azurerm-ps.md).

## <a name="before-you-begin"></a>Antes de começar


* Reveja [planear a migração de Olá tooManaged discos](on-prem-to-azure.md#plan-for-the-migration-to-managed-disks).

[!INCLUDE [virtual-machines-common-convert-disks-considerations](../../../includes/virtual-machines-common-convert-disks-considerations.md)]




## <a name="convert-single-instance-vms"></a>Converter a VMs de instância única
Esta secção abrange como tooconvert single-instance as VMs do Azure de não discos toomanaged discos. (Se as suas VMs num conjunto de disponibilidade, consulte o secção seguinte Olá.) 

1. Desalocar Olá VM utilizando Olá [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm) cmdlet. Olá exemplo seguinte deallocates Olá VM com o nome `myVM` no grupo de recursos de Olá designado `myResourceGroup`: 

  ```powershell
  $rgName = "myResourceGroup"
  $vmName = "myVM"
  Stop-AzureRmVM -ResourceGroupName $rgName -Name $vmName -Force
  ```

2. Converta os discos de toomanaged VM de Olá utilizando Olá [ConvertTo-AzureRmVMManagedDisk](/powershell/module/azurerm.compute/convertto-azurermvmmanageddisk) cmdlet. Olá seguir o processo converte Olá VM anterior, incluindo disco Olá SO e discos de dados:

  ```powershell
  ConvertTo-AzureRmVMManagedDisk -ResourceGroupName $rgName -VMName $vmName
  ```

3. Iniciar Olá VM após a discos de toomanaged de conversão de Olá utilizando [Start-AzureRmVM](/powershell/module/azurerm.compute/start-azurermvm). Olá reinícios de exemplo a seguir Olá VM anterior:

  ```powershell
  Start-AzureRmVM -ResourceGroupName $rgName -Name $vmName
  ```


## <a name="convert-vms-in-an-availability-set"></a>Converter VMs num conjunto de disponibilidade

Se Olá VMs que pretende que sejam tooconvert toomanaged discos estão num conjunto de disponibilidade, terá primeiro tooconvert Olá disponibilidade conjunto tooa gerido conjunto de disponibilidade.

1. Converter o conjunto, utilizando Olá de disponibilidade de Olá [atualização AzureRmAvailabilitySet](/powershell/module/azurerm.compute/update-azurermavailabilityset) cmdlet. Olá seguinte o exemplo de atualizações Olá conjunto nomeada de disponibilidade `myAvailabilitySet` no grupo de recursos de Olá designado `myResourceGroup`:

  ```powershell
  $rgName = 'myResourceGroup'
  $avSetName = 'myAvailabilitySet'

  $avSet = Get-AzureRmAvailabilitySet -ResourceGroupName $rgName -Name $avSetName
  Update-AzureRmAvailabilitySet -AvailabilitySet $avSet -Sku Aligned 
  ```

  Se a região de olá onde está localizado o conjunto de disponibilidade tem apenas 2 domínios de falhas gerido, mas Olá número de domínios de falhas não gerido 3, este comando apresenta um erro semelhante demasiado "Olá especificado o número de domínios de falhas 3 tem de pertencer Olá intervalo 1 too2." tooresolve Olá erro, too2 de domínio de falhas de Olá de atualização e atualização `Sku` demasiado`Aligned` da seguinte forma:

  ```powershell
  $avSet.PlatformFaultDomainCount = 2
  Update-AzureRmAvailabilitySet -AvailabilitySet $avSet -Sku Aligned
  ```

2. Desalocar e converter Olá VMs no conjunto de disponibilidade de Olá. Olá seguinte script deallocates cada VM utilizando Olá [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm) cmdlet, converte-o utilizando [ConvertTo-AzureRmVMManagedDisk](/powershell/module/azurerm.compute/convertto-azurermvmmanageddisk)e reinicia-lo utilizando [Start-AzureRmVM ](/powershell/module/azurerm.compute/start-azurermvm):

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


## <a name="troubleshooting"></a>Resolução de problemas

Se ocorrer um erro durante a conversão, ou se uma VM está em estado de falha devido a problemas de uma conversão anterior, execute Olá `ConvertTo-AzureRmVMManagedDisk` cmdlet novamente. Uma repetição simple normalmente unblocks situação Olá.


## <a name="next-steps"></a>Passos seguintes

[Converter discos geridos padrão toopremium](convert-disk-storage.md)

Efetuar uma cópia só de leitura de uma VM utilizando [instantâneos](snapshot-copy-managed-disk.md).

