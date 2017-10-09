---
title: "Descrição geral do agente de Máquina Virtual de aaaAzure | Microsoft Docs"
description: "Descrição geral do agente de Máquina Virtual do Azure"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 0a1f212e-053e-4a39-9910-8d622959f594
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 03/28/2017
ms.author: nepeters
ms.openlocfilehash: 178766925673419cd661dbb460b8427bbfaf54e7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-virtual-machine-agent-overview"></a><span data-ttu-id="64b04-103">Descrição geral do agente da Máquina Virtual do Azure</span><span class="sxs-lookup"><span data-stu-id="64b04-103">Azure Virtual Machine Agent overview</span></span>

<span data-ttu-id="64b04-104">Olá agente de Máquina Virtual do Microsoft Azure (agente da VM) é um processo seguro e simples que gere a interação de VM com Olá controlador de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="64b04-104">hello Microsoft Azure Virtual Machine Agent (VM Agent) is a secured, lightweight process that manages VM interaction with hello Azure Fabric Controller.</span></span> <span data-ttu-id="64b04-105">Olá agente da VM tem uma função primária em ativar e executar as extensões de máquina virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="64b04-105">hello VM Agent has a primary role in enabling and executing Azure virtual machine extensions.</span></span> <span data-ttu-id="64b04-106">Ativar as extensões de VM após a configuração de implementação de máquinas virtuais, tais como instalar e configurar o software.</span><span class="sxs-lookup"><span data-stu-id="64b04-106">VM Extensions enabling post deployment configuration of virtual machines, such as installing and configuring software.</span></span> <span data-ttu-id="64b04-107">Extensões de máquina virtual também ativar as funcionalidades de recuperação, tal como repor Olá palavra-passe administrativa de uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="64b04-107">Virtual machine extensions also enable recovery features such as resetting hello administrative password of a virtual machine.</span></span> <span data-ttu-id="64b04-108">Sem Olá agente da VM do Azure, não não possível executar as extensões de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="64b04-108">Without hello Azure VM Agent, virtual machine extensions cannot be run.</span></span>

<span data-ttu-id="64b04-109">Este documento fornece detalhes sobre a instalação, a deteção e a remoção de Olá agente da Máquina Virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="64b04-109">This document details installation, detection, and removal of hello Azure Virtual Machine Agent.</span></span>

## <a name="install-hello-vm-agent"></a><span data-ttu-id="64b04-110">Instalar Olá agente da VM</span><span class="sxs-lookup"><span data-stu-id="64b04-110">Install hello VM Agent</span></span>

### <a name="azure-gallery-image"></a><span data-ttu-id="64b04-111">Imagem da galeria do Azure</span><span class="sxs-lookup"><span data-stu-id="64b04-111">Azure gallery image</span></span>

<span data-ttu-id="64b04-112">Olá agente da VM do Azure está instalado por predefinição em qualquer máquina virtual do Windows implementada a partir de uma imagem de galeria do Azure.</span><span class="sxs-lookup"><span data-stu-id="64b04-112">hello Azure VM Agent is installed by default on any Windows virtual machine deployed from an Azure Gallery image.</span></span> <span data-ttu-id="64b04-113">Quando implementar uma imagem de galeria do Azure a partir de Olá Portal, o PowerShell, Interface de linha de comandos ou um modelo Azure Resource Manager, Olá que agente da VM do Azure é também instalada.</span><span class="sxs-lookup"><span data-stu-id="64b04-113">When deploying an Azure gallery image from hello Portal, PowerShell, Command Line Interface, or an Azure Resource Manager template, hello Azure VM Agent is also be installed.</span></span> 

### <a name="manual-installation"></a><span data-ttu-id="64b04-114">Instalação manual</span><span class="sxs-lookup"><span data-stu-id="64b04-114">Manual installation</span></span>

<span data-ttu-id="64b04-115">agente de VM do Windows Hello pode de ser instalado manualmente utilizando um pacote de instalador do Windows.</span><span class="sxs-lookup"><span data-stu-id="64b04-115">hello Windows VM agent can be manually installed using a Windows installer package.</span></span> <span data-ttu-id="64b04-116">Instalação manual pode ser necessária quando criar uma imagem de máquina virtual personalizada que será implementado no Azure.</span><span class="sxs-lookup"><span data-stu-id="64b04-116">Manual installation may be necessary when creating a custom virtual machine image that will be deployed in Azure.</span></span> <span data-ttu-id="64b04-117">toomanually Olá de instalar o agente de VM do Windows, transferir o instalador do agente de VM de Olá partir desta localização [transferir de agente do Windows Azure VM](http://go.microsoft.com/fwlink/?LinkID=394789).</span><span class="sxs-lookup"><span data-stu-id="64b04-117">toomanually install hello Windows VM Agent, download hello VM Agent installer from this location [Windows Azure VM Agent Download](http://go.microsoft.com/fwlink/?LinkID=394789).</span></span> 

<span data-ttu-id="64b04-118">Olá agente da VM pode ser instalado fazendo duplo clique em ficheiro de instalador do windows hello.</span><span class="sxs-lookup"><span data-stu-id="64b04-118">hello VM Agent can be installed by double-clicking hello windows installer file.</span></span> <span data-ttu-id="64b04-119">Para uma instalação automatizada ou automática do agente da VM Olá, execute Olá os seguintes comandos.</span><span class="sxs-lookup"><span data-stu-id="64b04-119">For an automated or unattended installation of hello VM agent, run hello following command.</span></span>

```cmd
msiexec.exe /i WindowsAzureVmAgent.2.7.1198.778.rd_art_stable.160617-1120.fre /quiet
```

## <a name="detect-hello-vm-agent"></a><span data-ttu-id="64b04-120">Detetar Olá agente da VM</span><span class="sxs-lookup"><span data-stu-id="64b04-120">Detect hello VM Agent</span></span>

### <a name="powershell"></a><span data-ttu-id="64b04-121">PowerShell</span><span class="sxs-lookup"><span data-stu-id="64b04-121">PowerShell</span></span>

<span data-ttu-id="64b04-122">módulo do Azure Resource Manager PowerShell de Olá pode ser utilizados tooretrieve informações sobre máquinas virtuais do Azure.</span><span class="sxs-lookup"><span data-stu-id="64b04-122">hello Azure Resource Manager PowerShell module can be used tooretrieve information about Azure Virtual Machines.</span></span> <span data-ttu-id="64b04-123">Executar `Get-AzureRmVM` devolve bastantes bits de informações, incluindo Olá para Olá agente da VM do Azure, o estado de aprovisionamento.</span><span class="sxs-lookup"><span data-stu-id="64b04-123">Running `Get-AzureRmVM` returns quite a bit of information including hello provisioning state for hello Azure VM Agent.</span></span>

```PowerShell
Get-AzureRmVM
```

<span data-ttu-id="64b04-124">Olá segue-se apenas um subconjunto de Olá `Get-AzureRmVM` saída.</span><span class="sxs-lookup"><span data-stu-id="64b04-124">hello following is just a subset of hello `Get-AzureRmVM` output.</span></span> <span data-ttu-id="64b04-125">Olá aviso `ProvisionVMAgent` propriedade aninhada `OSProfile`, esta propriedade pode ser utilizado toodetermine se o agente da VM Olá foi implementado toohello máquina.</span><span class="sxs-lookup"><span data-stu-id="64b04-125">Notice hello `ProvisionVMAgent` property nested inside `OSProfile`, this property can be used toodetermine if hello VM agent has been deployed toohello virtual machine.</span></span>

```PowerShell
OSProfile                  :
  ComputerName             : myVM
  AdminUsername            : muUserName
  WindowsConfiguration     :
    ProvisionVMAgent       : True
    EnableAutomaticUpdates : True
```

<span data-ttu-id="64b04-126">Olá script a seguir pode ser utilizado tooreturn concisa obter uma lista de nomes de máquina virtual e o estado de Olá de Olá agente da VM.</span><span class="sxs-lookup"><span data-stu-id="64b04-126">hello following script can be used tooreturn a concise list of virtual machine names and hello state of hello VM Agent.</span></span>

```PowerShell
$vms = Get-AzureRmVM

foreach ($vm in $vms) {
    $agent = $vm | Select -ExpandProperty OSProfile | Select -ExpandProperty Windowsconfiguration | Select ProvisionVMAgent
    Write-Host $vm.Name $agent.ProvisionVMAgent
}
```

### <a name="manual-detection"></a><span data-ttu-id="64b04-127">Deteção manual</span><span class="sxs-lookup"><span data-stu-id="64b04-127">Manual Detection</span></span>

<span data-ttu-id="64b04-128">Quando tem sessão iniciada no tooa VM do Windows Azure, o Gestor de tarefas pode ser utilizado tooexamine processos em execução.</span><span class="sxs-lookup"><span data-stu-id="64b04-128">When logged in tooa Windows Azure VM, task manager can be used tooexamine running processes.</span></span> <span data-ttu-id="64b04-129">toocheck para Olá agente da VM do Azure, abra o Gestor de tarefas > clique separador de detalhes de Olá e procure um nome de processo `WindowsAzureGuestAgent.exe`.</span><span class="sxs-lookup"><span data-stu-id="64b04-129">toocheck for hello Azure VM Agent, open Task Manager > click hello details tab, and look for a process name `WindowsAzureGuestAgent.exe`.</span></span> <span data-ttu-id="64b04-130">presença de Olá deste processo indica que o agente VM Olá está instalado.</span><span class="sxs-lookup"><span data-stu-id="64b04-130">hello presence of this process indicates that hello VM agent is installed.</span></span>

## <a name="upgrade-hello-vm-agent"></a><span data-ttu-id="64b04-131">Atualizar Olá agente da VM</span><span class="sxs-lookup"><span data-stu-id="64b04-131">Upgrade hello VM Agent</span></span>

<span data-ttu-id="64b04-132">Olá Azure VM agente para o Windows é atualizado automaticamente.</span><span class="sxs-lookup"><span data-stu-id="64b04-132">hello Azure VM Agent for Windows is automatically upgraded.</span></span> <span data-ttu-id="64b04-133">As novas máquinas virtuais implementada tooAzure, estes recebem agente da VM Olá mais recente.</span><span class="sxs-lookup"><span data-stu-id="64b04-133">As new virtual machines are deployed tooAzure, they receive hello latest VM agent.</span></span> <span data-ttu-id="64b04-134">Imagens VM personalizadas devem ser agente da VM nova Olá tooinclude atualizadas manualmente.</span><span class="sxs-lookup"><span data-stu-id="64b04-134">Custom VM images should be manually updated tooinclude hello new VM agent.</span></span>
