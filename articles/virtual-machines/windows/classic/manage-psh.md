---
title: "aaaManage as máquinas virtuais utilizando o Azure PowerShell | Microsoft Docs"
description: "Saiba mais comandos que pode utilizar tarefas de tooautomate na gestão de máquinas virtuais."
services: virtual-machines-windows
documentationcenter: windows
author: singhkays
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 7cdf9bd3-6578-4069-8a95-e8585f04a394
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 10/12/2016
ms.author: kasing
ms.openlocfilehash: e4ca6f098519243a321eac98b6692790fe18c22c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-your-virtual-machines-by-using-azure-powershell"></a>Gerir máquinas virtuais utilizando o Azure PowerShell
> [!IMPORTANT] 
> O Azure tem dois modelos de implementação diferentes para criar e trabalhar com recursos: [Resource Manager e clássico](../../../resource-manager-deployment-model.md). Este artigo abrange utilizando o modelo de implementação clássica Olá. A Microsoft recomenda que as implementações mais novas utilizem o modelo de Gestor de recursos de Olá. Para utilizar o modelo do Resource Manager Olá comuns comandos do PowerShell, consulte [aqui](../../virtual-machines-windows-ps-common-ref.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

Muitas tarefas, fazê-lo toomanage cada dia as suas VMs podem ser automatizadas utilizando cmdlets do PowerShell do Azure. Este artigo dá-lhe comandos de exemplo para tarefas mais simples e tooarticles de ligações que mostram os comandos de Olá para as tarefas mais complexas.

> [!NOTE]
> Se ainda não instalado e configurado o Azure PowerShell ainda, pode obter as instruções no artigo Olá [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview).
> 
> 

## <a name="how-toouse-hello-example-commands"></a>Como toouse Olá comandos de exemplo
Irá precisar de tooreplace algumas das texto Olá Olá comandos com o texto que é adequado para o seu ambiente. Olá < e > símbolos indicar que precisa de tooreplace de texto. Quando a substituir o texto de Olá, remover símbolos Olá, mas deixe Olá aspa marcas no local.

## <a name="get-a-vm"></a>Obter uma VM
Esta é uma tarefa de básica que irá utilizar com frequência. Utilizá-lo tooget informações sobre uma VM, efetuar tarefas numa VM ou obter toostore de resultado numa variável.

informações de tooget sobre Olá VM, execute este comando, substituindo tudo aspas Olá, incluindo Olá < e > carateres:

     Get-AzureVM -ServiceName "<cloud service name>" -Name "<virtual machine name>"

Olá toostore resultado numa variável $vm, execute:

    $vm = Get-AzureVM -ServiceName "<cloud service name>" -Name "<virtual machine name>"

## <a name="log-on-tooa-windows-based-vm"></a>Inicie sessão tooa VM baseadas em Windows
Execute estes comandos:

> [!NOTE]
> Pode obter Olá máquina e nome do serviço de nuvem a partir de apresentação Olá de Olá **Get-AzureVM** comando.
> 
> $svcName = "<cloud service name>" $vmName = "<virtual machine name>" $localPath = "< unidade e a pasta ficheiros RDP localização toostore Olá transferido, exemplo: c:\temp >" $localFile = $localPath + "\" + $vmname +". rdp"Get-AzureRemoteDesktopFile - ServiceName $svcName-nome $vmName - LocalPath $localFile-iniciar
> 
> 

## <a name="stop-a-vm"></a>Parar uma VM
Execute este comando:

    Stop-AzureVM -ServiceName "<cloud service name>" -Name "<virtual machine name>"

> [!IMPORTANT]
> Utilize este Olá tookeep de parâmetro IP virtual (VIP) da nuvem Olá service caso seja Olá última VM em que o serviço de nuvem. <br><br> Se utilizar o parâmetro de StayProvisioned Olá, irá ainda ser-lhe faturado Olá VM.
> 
> 

## <a name="start-a-vm"></a>Iniciar uma VM
Execute este comando:

    Start-AzureVM -ServiceName "<cloud service name>" -Name "<virtual machine name>"

## <a name="attach-a-data-disk"></a>Anexar um disco de dados
Esta tarefa requer alguns passos. Em primeiro lugar, utilize o Olá *** Add-AzureDataDisk *** cmdlet tooadd Olá toohello $vm objeto de disco. Em seguida, utilize **Update-AzureVM** cmdlet tooupdate Olá configuração Olá VM.

Também terá de toodecide se tooattach um novo disco ou um que contenha dados. Para um novo disco, o comando Olá cria o ficheiro. vhd Olá e anexa-lo.

tooattach um novo disco, execute este comando:

    Add-AzureDataDisk -CreateNew -DiskSizeInGB 128 -DiskLabel "<main>" -LUN <0> -VM $vm | Update-AzureVM

tooattach um disco de dados existente, execute este comando:

    Add-AzureDataDisk -Import -DiskName "<MyExistingDisk>" -LUN <0> | Update-AzureVM

tooattach discos de dados de um ficheiro. vhd existente no armazenamento de BLOBs, execute este comando:

    Add-AzureDataDisk -ImportFrom -MediaLocation `
              "<https://mystorage.blob.core.windows.net/mycontainer/MyExistingDisk.vhd>" `
              -DiskLabel "<main>" -LUN <0> |
              Update-AzureVM

## <a name="create-a-windows-based-vm"></a>Criar uma VM com base no Windows
toocreate uma nova baseados em Windows máquina virtual no Azure, utilize Olá instruções [toocreate de utilizar o Azure PowerShell e pré-configurar máquinas virtuais baseadas em Windows](create-powershell.md). Passos neste tópico, através da criação de Olá de um conjunto de comandos do Azure PowerShell cria uma VM baseada em Windows que pode ser pré-configurados:

* Com a associação de domínio do Active Directory.
* Com discos adicionais.
* Definir o membro de um existente com balanceamento de carga.
* Com um endereço IP estático.

