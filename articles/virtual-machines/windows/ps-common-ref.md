---
title: "aaaCommon PowerShell comandos para máquinas virtuais do Azure | Microsoft Docs"
description: Comuns tooget de comandos do PowerShell que iniciou a criar e gerir as VMs do Windows no Azure.
services: virtual-machines-windows
documentationcenter: 
author: davidmu1
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: ba3839a2-f3d5-4e19-a5de-95bfb1c0e61e
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 07/17/2017
ms.author: davidmu
ms.openlocfilehash: 3de9bd4d20259ced2c0aa8ef7a3f7d9520a071d0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="common-powershell-commands-for-creating-and-managing-azure-virtual-machines"></a>Comandos do PowerShell comuns para criar e gerir máquinas virtuais do Azure

Este artigo aborda alguns dos Olá que comandos do Azure PowerShell que pode utilizar toocreate e gerir máquinas virtuais na sua subscrição do Azure.  Para obter mais ajuda com comutadores de linha de comandos específicos e as opções, pode utilizar **Get-Help** *comando*.

Consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview) para obter informações sobre instalar Olá a versão mais recente do Azure PowerShell, selecionar a sua subscrição e início de sessão na conta tooyour.

Estas variáveis poderão ser útil se com mais do que um dos comandos Olá neste artigo:

- $location - localização Olá da máquina virtual de Olá. Pode utilizar [Get-AzureRmLocation](https://docs.microsoft.com/powershell/module/azurerm.resources/get-azurermlocation) toofind um [região geográfica](https://azure.microsoft.com/regions/) que funciona para si.
- $myResourceGroup - nome Olá Olá do grupo de recursos que contém a máquina virtual de Olá.
- $myVM - nome Olá da máquina virtual de Olá.

## <a name="create-a-vm"></a>Criar uma VM

| Tarefa | Comando |
| ---- | ------- |
| Criar uma configuração de VM |$vm = [New-AzureRmVMConfig](https://docs.microsoft.com/powershell/module/azurerm.compute/new-azurermvmconfig) - VMName $myVM - VMSize "Standard_D1_v1"<BR></BR><BR></BR>a configuração de VM Olá é utilizadas toodefine ou atualização definições Olá VM. configuração de Olá foi inicializada com o nome Olá Olá VM e a respetiva [tamanho](sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). |
| Adicionar as definições de configuração |$vm = [conjunto AzureRmVMOperatingSystem](https://docs.microsoft.com/powershell/module/azurerm.compute/set-azurermvmoperatingsystem) - VM $vm-Windows - ComputerName $myVM-Credential $cred - ProvisionVMAgent - EnableAutoUpdate<BR></BR><BR></BR>Definições do sistema operativo, incluindo [credenciais](https://technet.microsoft.com/library/hh849815.aspx) são adicionados toohello objeto de configuração que criou anteriormente com AzureRmVMConfig de novo. |
| Adicione uma interface de rede |$vm = [adicionar AzureRmVMNetworkInterface](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.5.0/Add-AzureRmVMNetworkInterface) - VM $vm-NIC de $Id. ID<BR></BR><BR></BR>Uma VM tem de ter um [interface de rede](../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) toocommunicate numa rede virtual. Também pode utilizar [Get-AzureRmNetworkInterface](https://docs.microsoft.com/powershell/module/azurerm.compute/add-azurermvmnetworkinterface) tooretrieve um objeto de interface de rede existente. |
| Especifique uma imagem de plataforma |$vm = [conjunto AzureRmVMSourceImage](https://docs.microsoft.com/powershell/module/azurerm.compute/set-azurermvmsourceimage) - VM $vm - PublisherName "publisher_name"-oferecem "publisher_offer" - Skus "product_sku"-versão "mais recente"<BR></BR><BR></BR>[Informações de imagem](cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) é adicionado o objeto de configuração de toohello que criou anteriormente com AzureRmVMConfig de novo. objeto de Olá devolvido por este comando só é utilizado quando definir Olá SO disco toouse uma imagem de plataforma. |
| Definir toouse de disco de SO uma imagem de plataforma |$vm = [conjunto AzureRmVMOSDisk](https://docs.microsoft.com/powershell/module/azurerm.compute/set-azurermvmosdisk) - VM $vm-Name "myOSDisk" - VhdUri "http://mystore1.blob.core.windows.net/vhds/myOSDisk.vhd" - CreateOption FromImage<BR></BR><BR></BR>nome de Olá do disco do sistema operativo Olá e a respetiva localização no [armazenamento](../../storage/common/storage-powershell-guide-full.md) é adicionado o objeto de configuração de toohello que criou anteriormente. |
| Uma imagem generalizada do conjunto de toouse de disco do SO |$vm = set AzureRmVMOSDisk - VM $vm-Name "myOSDisk" - SourceImageUri "https://mystore1.blob.core.windows.net/system/Microsoft.Compute/Images/myimages/myprefix-osDisk. {guid}.. vhd"- VhdUri"https://mystore1.blob.core.windows.net/vhds/disk_name.vhd"- CreateOption FromImage-Windows<BR></BR><BR></BR>nome de Olá do disco do sistema operativo Olá, a localização de Olá Olá da imagem de origem e a localização do disco Olá [armazenamento](../../storage/common/storage-powershell-guide-full.md) é adicionada toohello objeto de configuração. |
| Uma imagem especializada do conjunto de toouse de disco do SO |$vm = set AzureRmVMOSDisk - VM $vm-Name "myOSDisk" - VhdUri "http://mystore1.blob.core.windows.net/vhds/" - CreateOption anexar - Windows |
| Criar uma VM |[Novo-AzureRmVM]() - ResourceGroupName $myResourceGroup-localização $location - VM $vm<BR></BR><BR></BR>Todos os recursos são criados num [grupo de recursos](../../azure-resource-manager/powershell-azure-resource-manager.md). Antes de executar este comando, execute New-AzureRmVMConfig, AzureRmVMOperatingSystem conjunto, AzureRmVMSourceImage conjunto, AzureRmVMNetworkInterface adicionar e AzureRmVMOSDisk de conjunto. |

## <a name="get-information-about-vms"></a>Obter informações sobre as VMs

| Tarefa | Comando |
| ---- | ------- |
| Lista de VMs de uma subscrição |[Get-AzureRmVM](https://docs.microsoft.com/powershell/module/azurerm.compute/get-azurermvm) |
| Lista de VMs num grupo de recursos |Get-AzureRmVM - ResourceGroupName $myResourceGroup<BR></BR><BR></BR>uma lista de recursos de tooget grupos na sua subscrição, utilize [Get-AzureRmResourceGroup](https://docs.microsoft.com/powershell/module/azurerm.resources/get-azurermresourcegroup). |
| Obter informações sobre uma VM |Get-AzureRmVM - ResourceGroupName $myResourceGroup-nome $myVM |

## <a name="manage-vms"></a>Gerir VMs
| Tarefa | Comando |
| --- | --- |
| Iniciar uma VM |[Start-AzureRmVM](https://docs.microsoft.com/powershell/module/azurerm.compute/start-azurermvm) - ResourceGroupName $myResourceGroup-nome $myVM |
| Parar uma VM |[Stop-AzureRmVM](https://docs.microsoft.com/powershell/module/azurerm.compute/stop-azurermvm) - ResourceGroupName $myResourceGroup-nome $myVM |
| Reiniciar uma VM em execução |[Reinício-AzureRmVM](https://docs.microsoft.com/powershell/module/azurerm.compute/restart-azurermvm) - ResourceGroupName $myResourceGroup-nome $myVM |
| Eliminar uma VM |[Remove-AzureRmVM](https://docs.microsoft.com/powershell/module/azurerm.compute/remove-azurermvm) - ResourceGroupName $myResourceGroup-nome $myVM |
| Generalize uma VM |[Set-AzureRmVm](https://docs.microsoft.com/powershell/module/azurerm.compute/set-azurermvm) - ResourceGroupName $myResourceGroup-nome $myVM-generalizado<BR></BR><BR></BR>Execute este comando antes de executar AzureRmVMImage guardar. |
| Capturar uma VM |[Guardar AzureRmVMImage](https://docs.microsoft.com/powershell/module/azurerm.compute/save-azurermvmimage) - ResourceGroupName $myResourceGroup - VMName $myVM - DestinationContainerName "myImageContainer" - VHDNamePrefix "myImagePrefix"-"C:\filepath\filename.json" do caminho<BR></BR><BR></BR>Uma máquina virtual tem de ser [preparado, encerre e generalizado](prepare-for-upload-vhd-image.md) toocreate toobe utilizada uma imagem. Antes de executar este comando, execute Set-AzureRmVm. |
| Atualizar uma VM |[Update-AzureRmVM](https://docs.microsoft.com/powershell/module/azurerm.compute/update-azurermvm) - ResourceGroupName $myResourceGroup - VM $vm<BR></BR><BR></BR>Obter Olá configuração atual da VM utilizando o Get-AzureRmVM, alterar definições de configuração no objeto VM Olá e, em seguida, execute este comando. |
| Adicionar um tooa de disco de dados VM |[AzureRmVMDataDisk adicionar](https://docs.microsoft.com/powershell/module/azurerm.compute/add-azurermvmdatadisk) - VM $vm-Name "myDataDisk" - VhdUri "https://mystore1.blob.core.windows.net/vhds/myDataDisk.vhd" - LUN #-colocação em cache ReadWrite - DiskSizeinGB # CreateOption - vazio<BR></BR><BR></BR>Utilize Get-AzureRmVM tooget Olá VM objeto. Especifique o número LUN Olá e o tamanho de Olá do disco de Olá. Execute atualização-AzureRmVM tooapply Olá configuração alterações toohello VM. disco Olá que adiciona não está inicializado. |
| Remover um disco de dados de uma VM |[Remover AzureRmVMDataDisk](https://docs.microsoft.com/powershell/module/azurerm.compute/remove-azurermvmdatadisk) - VM $vm-Name "myDataDisk"<BR></BR><BR></BR>Utilize Get-AzureRmVM tooget Olá VM objeto. Execute atualização-AzureRmVM tooapply Olá configuração alterações toohello VM. |
| Adicionar uma extensão tooa VM |[Conjunto AzureRmVMExtension](https://docs.microsoft.com/powershell/module/azurerm.compute/set-azurermvmextension) - ResourceGroupName $myResourceGroup-localização $location - VMName $myVM-extensionName"nome"-publicador "publisherName"-"extensionType" de tipo - TypeHandlerVersion "#. #"-definições $Settings - ProtectedSettings $ProtectedSettings<BR></BR><BR></BR>Execute este comando com Olá adequado [informações de configuração](template-description.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json#extensions) para extensão Olá que pretende que o tooinstall. |
| Remover uma extensão de VM |[Remover AzureRmVMExtension](https://docs.microsoft.com/powershell/module/azurerm.compute/remove-azurermvmextension) - ResourceGroupName $myResourceGroup-Name "extensionName" - VMName $myVM |

## <a name="next-steps"></a>Passos seguintes
* Consulte os passos básicos Olá para criar uma máquina virtual no [criar uma VM do Windows utilizando o Gestor de recursos e o PowerShell](../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

