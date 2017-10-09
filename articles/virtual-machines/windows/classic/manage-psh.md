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
# <a name="manage-your-virtual-machines-by-using-azure-powershell"></a><span data-ttu-id="e9e44-103">Gerir máquinas virtuais utilizando o Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="e9e44-103">Manage your virtual machines by using Azure PowerShell</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="e9e44-104">O Azure tem dois modelos de implementação diferentes para criar e trabalhar com recursos: [Resource Manager e clássico](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="e9e44-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="e9e44-105">Este artigo abrange utilizando o modelo de implementação clássica Olá.</span><span class="sxs-lookup"><span data-stu-id="e9e44-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="e9e44-106">A Microsoft recomenda que as implementações mais novas utilizem o modelo de Gestor de recursos de Olá.</span><span class="sxs-lookup"><span data-stu-id="e9e44-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="e9e44-107">Para utilizar o modelo do Resource Manager Olá comuns comandos do PowerShell, consulte [aqui](../../virtual-machines-windows-ps-common-ref.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e9e44-107">For common PowerShell commands using hello Resource Manager model, see [here](../../virtual-machines-windows-ps-common-ref.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="e9e44-108">Muitas tarefas, fazê-lo toomanage cada dia as suas VMs podem ser automatizadas utilizando cmdlets do PowerShell do Azure.</span><span class="sxs-lookup"><span data-stu-id="e9e44-108">Many tasks you do each day toomanage your VMs can be automated by using Azure PowerShell cmdlets.</span></span> <span data-ttu-id="e9e44-109">Este artigo dá-lhe comandos de exemplo para tarefas mais simples e tooarticles de ligações que mostram os comandos de Olá para as tarefas mais complexas.</span><span class="sxs-lookup"><span data-stu-id="e9e44-109">This article gives you example commands for simpler tasks, and links tooarticles that show hello commands for more complex tasks.</span></span>

> [!NOTE]
> <span data-ttu-id="e9e44-110">Se ainda não instalado e configurado o Azure PowerShell ainda, pode obter as instruções no artigo Olá [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="e9e44-110">If you haven't installed and configured Azure PowerShell yet, you can get instructions in hello article [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>
> 
> 

## <a name="how-toouse-hello-example-commands"></a><span data-ttu-id="e9e44-111">Como toouse Olá comandos de exemplo</span><span class="sxs-lookup"><span data-stu-id="e9e44-111">How toouse hello example commands</span></span>
<span data-ttu-id="e9e44-112">Irá precisar de tooreplace algumas das texto Olá Olá comandos com o texto que é adequado para o seu ambiente.</span><span class="sxs-lookup"><span data-stu-id="e9e44-112">You'll need tooreplace some of hello text in hello commands with text that's appropriate for your environment.</span></span> <span data-ttu-id="e9e44-113">Olá < e > símbolos indicar que precisa de tooreplace de texto.</span><span class="sxs-lookup"><span data-stu-id="e9e44-113">hello < and > symbols indicate text you need tooreplace.</span></span> <span data-ttu-id="e9e44-114">Quando a substituir o texto de Olá, remover símbolos Olá, mas deixe Olá aspa marcas no local.</span><span class="sxs-lookup"><span data-stu-id="e9e44-114">When you replace hello text, remove hello symbols but leave hello quote marks in place.</span></span>

## <a name="get-a-vm"></a><span data-ttu-id="e9e44-115">Obter uma VM</span><span class="sxs-lookup"><span data-stu-id="e9e44-115">Get a VM</span></span>
<span data-ttu-id="e9e44-116">Esta é uma tarefa de básica que irá utilizar com frequência.</span><span class="sxs-lookup"><span data-stu-id="e9e44-116">This is a basic task you'll use often.</span></span> <span data-ttu-id="e9e44-117">Utilizá-lo tooget informações sobre uma VM, efetuar tarefas numa VM ou obter toostore de resultado numa variável.</span><span class="sxs-lookup"><span data-stu-id="e9e44-117">Use it tooget information about a VM, perform tasks on a VM, or get output toostore in a variable.</span></span>

<span data-ttu-id="e9e44-118">informações de tooget sobre Olá VM, execute este comando, substituindo tudo aspas Olá, incluindo Olá < e > carateres:</span><span class="sxs-lookup"><span data-stu-id="e9e44-118">tooget information about hello VM, run this command, replacing everything in hello quotes, including hello < and > characters:</span></span>

     Get-AzureVM -ServiceName "<cloud service name>" -Name "<virtual machine name>"

<span data-ttu-id="e9e44-119">Olá toostore resultado numa variável $vm, execute:</span><span class="sxs-lookup"><span data-stu-id="e9e44-119">toostore hello output in a $vm variable, run:</span></span>

    $vm = Get-AzureVM -ServiceName "<cloud service name>" -Name "<virtual machine name>"

## <a name="log-on-tooa-windows-based-vm"></a><span data-ttu-id="e9e44-120">Inicie sessão tooa VM baseadas em Windows</span><span class="sxs-lookup"><span data-stu-id="e9e44-120">Log on tooa Windows-based VM</span></span>
<span data-ttu-id="e9e44-121">Execute estes comandos:</span><span class="sxs-lookup"><span data-stu-id="e9e44-121">Run these commands:</span></span>

> [!NOTE]
> <span data-ttu-id="e9e44-122">Pode obter Olá máquina e nome do serviço de nuvem a partir de apresentação Olá de Olá **Get-AzureVM** comando.</span><span class="sxs-lookup"><span data-stu-id="e9e44-122">You can get hello virtual machine and cloud service name from hello display of hello **Get-AzureVM** command.</span></span>
> 
> <span data-ttu-id="e9e44-123">$svcName = "<cloud service name>" $vmName = "<virtual machine name>" $localPath = "< unidade e a pasta ficheiros RDP localização toostore Olá transferido, exemplo: c:\temp >" $localFile = $localPath + "\" + $vmname +". rdp"Get-AzureRemoteDesktopFile - ServiceName $svcName-nome $vmName - LocalPath $localFile-iniciar</span><span class="sxs-lookup"><span data-stu-id="e9e44-123">$svcName = "<cloud service name>" $vmName = "<virtual machine name>" $localPath = "<drive and folder location toostore hello downloaded RDP file, example: c:\temp >" $localFile = $localPath + "\" + $vmname + ".rdp" Get-AzureRemoteDesktopFile -ServiceName $svcName -Name $vmName -LocalPath $localFile -Launch</span></span>
> 
> 

## <a name="stop-a-vm"></a><span data-ttu-id="e9e44-124">Parar uma VM</span><span class="sxs-lookup"><span data-stu-id="e9e44-124">Stop a VM</span></span>
<span data-ttu-id="e9e44-125">Execute este comando:</span><span class="sxs-lookup"><span data-stu-id="e9e44-125">Run this command:</span></span>

    Stop-AzureVM -ServiceName "<cloud service name>" -Name "<virtual machine name>"

> [!IMPORTANT]
> <span data-ttu-id="e9e44-126">Utilize este Olá tookeep de parâmetro IP virtual (VIP) da nuvem Olá service caso seja Olá última VM em que o serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="e9e44-126">Use this parameter tookeep hello virtual IP (VIP) of hello cloud service in case it's hello last VM in that cloud service.</span></span> <br><br> <span data-ttu-id="e9e44-127">Se utilizar o parâmetro de StayProvisioned Olá, irá ainda ser-lhe faturado Olá VM.</span><span class="sxs-lookup"><span data-stu-id="e9e44-127">If you use hello StayProvisioned parameter, you'll still be billed for hello VM.</span></span>
> 
> 

## <a name="start-a-vm"></a><span data-ttu-id="e9e44-128">Iniciar uma VM</span><span class="sxs-lookup"><span data-stu-id="e9e44-128">Start a VM</span></span>
<span data-ttu-id="e9e44-129">Execute este comando:</span><span class="sxs-lookup"><span data-stu-id="e9e44-129">Run this command:</span></span>

    Start-AzureVM -ServiceName "<cloud service name>" -Name "<virtual machine name>"

## <a name="attach-a-data-disk"></a><span data-ttu-id="e9e44-130">Anexar um disco de dados</span><span class="sxs-lookup"><span data-stu-id="e9e44-130">Attach a data disk</span></span>
<span data-ttu-id="e9e44-131">Esta tarefa requer alguns passos.</span><span class="sxs-lookup"><span data-stu-id="e9e44-131">This task requires a few steps.</span></span> <span data-ttu-id="e9e44-132">Em primeiro lugar, utilize o Olá *** Add-AzureDataDisk *** cmdlet tooadd Olá toohello $vm objeto de disco.</span><span class="sxs-lookup"><span data-stu-id="e9e44-132">First, you use hello ****Add-AzureDataDisk**** cmdlet tooadd hello disk toohello $vm object.</span></span> <span data-ttu-id="e9e44-133">Em seguida, utilize **Update-AzureVM** cmdlet tooupdate Olá configuração Olá VM.</span><span class="sxs-lookup"><span data-stu-id="e9e44-133">Then, you use **Update-AzureVM** cmdlet tooupdate hello configuration of hello VM.</span></span>

<span data-ttu-id="e9e44-134">Também terá de toodecide se tooattach um novo disco ou um que contenha dados.</span><span class="sxs-lookup"><span data-stu-id="e9e44-134">You'll also need toodecide whether tooattach a new disk or one that contains data.</span></span> <span data-ttu-id="e9e44-135">Para um novo disco, o comando Olá cria o ficheiro. vhd Olá e anexa-lo.</span><span class="sxs-lookup"><span data-stu-id="e9e44-135">For a new disk, hello command creates hello .vhd file and attaches it.</span></span>

<span data-ttu-id="e9e44-136">tooattach um novo disco, execute este comando:</span><span class="sxs-lookup"><span data-stu-id="e9e44-136">tooattach a new disk, run this command:</span></span>

    Add-AzureDataDisk -CreateNew -DiskSizeInGB 128 -DiskLabel "<main>" -LUN <0> -VM $vm | Update-AzureVM

<span data-ttu-id="e9e44-137">tooattach um disco de dados existente, execute este comando:</span><span class="sxs-lookup"><span data-stu-id="e9e44-137">tooattach an existing data disk, run this command:</span></span>

    Add-AzureDataDisk -Import -DiskName "<MyExistingDisk>" -LUN <0> | Update-AzureVM

<span data-ttu-id="e9e44-138">tooattach discos de dados de um ficheiro. vhd existente no armazenamento de BLOBs, execute este comando:</span><span class="sxs-lookup"><span data-stu-id="e9e44-138">tooattach data disks from an existing .vhd file in blob storage, run this command:</span></span>

    Add-AzureDataDisk -ImportFrom -MediaLocation `
              "<https://mystorage.blob.core.windows.net/mycontainer/MyExistingDisk.vhd>" `
              -DiskLabel "<main>" -LUN <0> |
              Update-AzureVM

## <a name="create-a-windows-based-vm"></a><span data-ttu-id="e9e44-139">Criar uma VM com base no Windows</span><span class="sxs-lookup"><span data-stu-id="e9e44-139">Create a Windows-based VM</span></span>
<span data-ttu-id="e9e44-140">toocreate uma nova baseados em Windows máquina virtual no Azure, utilize Olá instruções [toocreate de utilizar o Azure PowerShell e pré-configurar máquinas virtuais baseadas em Windows](create-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="e9e44-140">toocreate a new Windows-based virtual machine in Azure, use hello instructions in [Use Azure PowerShell toocreate and preconfigure Windows-based virtual machines](create-powershell.md).</span></span> <span data-ttu-id="e9e44-141">Passos neste tópico, através da criação de Olá de um conjunto de comandos do Azure PowerShell cria uma VM baseada em Windows que pode ser pré-configurados:</span><span class="sxs-lookup"><span data-stu-id="e9e44-141">This topic steps you through hello creation of an Azure PowerShell command set that creates a Windows-based VM that can be preconfigured:</span></span>

* <span data-ttu-id="e9e44-142">Com a associação de domínio do Active Directory.</span><span class="sxs-lookup"><span data-stu-id="e9e44-142">With Active Directory domain membership.</span></span>
* <span data-ttu-id="e9e44-143">Com discos adicionais.</span><span class="sxs-lookup"><span data-stu-id="e9e44-143">With additional disks.</span></span>
* <span data-ttu-id="e9e44-144">Definir o membro de um existente com balanceamento de carga.</span><span class="sxs-lookup"><span data-stu-id="e9e44-144">As a member of an existing load-balanced set.</span></span>
* <span data-ttu-id="e9e44-145">Com um endereço IP estático.</span><span class="sxs-lookup"><span data-stu-id="e9e44-145">With a static IP address.</span></span>

