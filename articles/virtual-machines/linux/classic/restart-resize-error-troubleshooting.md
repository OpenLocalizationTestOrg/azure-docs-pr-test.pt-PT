---
title: aaaVM reiniciar ou redimensionar problemas | Microsoft Docs
description: "Resolver problemas de implementação clássica com reiniciar ou redimensionar uma Máquina Virtual de Linux existente no Azure"
services: virtual-machines-linux
documentationcenter: 
author: Deland-Han
manager: felixwu
editor: 
tags: top-support-issue
ms.assetid: 73f2672c-602e-4766-8948-2b180115d299
ms.service: virtual-machines-linux
ms.topic: support-article
ms.tgt_pltfrm: vm-linux
ms.workload: required
ms.date: 01/10/2017
ms.devlang: na
ms.author: delhan
ms.openlocfilehash: fb1dc88bb1b83043c434590118bc8810ad402872
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-classic-deployment-issues-with-restarting-or-resizing-an-existing-linux-virtual-machine-in-azure"></a><span data-ttu-id="3d0dc-103">Resolver problemas de implementação clássica com reiniciar ou redimensionar uma Máquina Virtual de Linux existente no Azure</span><span class="sxs-lookup"><span data-stu-id="3d0dc-103">Troubleshoot classic deployment issues with restarting or resizing an existing Linux Virtual Machine in Azure</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="3d0dc-104">Clássico</span><span class="sxs-lookup"><span data-stu-id="3d0dc-104">Classic</span></span>](restart-resize-error-troubleshooting.md)
> * [<span data-ttu-id="3d0dc-105">Resource Manager</span><span class="sxs-lookup"><span data-stu-id="3d0dc-105">Resource Manager</span></span>](../restart-resize-error-troubleshooting.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
> 
> 

<span data-ttu-id="3d0dc-106">Quando tentar toostart uma Máquina Virtual do Azure (VM) parada ou redimensionar uma VM do Azure existente, o erro comum de Olá que ocorrerem é uma falha de alocação.</span><span class="sxs-lookup"><span data-stu-id="3d0dc-106">When you try toostart a stopped Azure Virtual Machine (VM), or resize an existing Azure VM, hello common error you encounter is an allocation failure.</span></span> <span data-ttu-id="3d0dc-107">Este erro resulta quando cluster Olá ou a região não ter recursos disponíveis ou não é suporte Olá pedir o tamanho da VM.</span><span class="sxs-lookup"><span data-stu-id="3d0dc-107">This error results when hello cluster or region either does not have resources available or cannot support hello requested VM size.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="3d0dc-108">O Azure tem dois modelos de implementação diferentes para criar e trabalhar com recursos: [Resource Manager e clássico](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="3d0dc-108">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="3d0dc-109">Este artigo abrange utilizando o modelo de implementação clássica Olá.</span><span class="sxs-lookup"><span data-stu-id="3d0dc-109">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="3d0dc-110">A Microsoft recomenda que as implementações mais novas utilizem o modelo de Gestor de recursos de Olá.</span><span class="sxs-lookup"><span data-stu-id="3d0dc-110">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="3d0dc-111">Para a versão do Gestor de recursos de Olá, consulte [aqui](../restart-resize-error-troubleshooting.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="3d0dc-111">For hello Resource Manager version, see [here](../restart-resize-error-troubleshooting.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

[!INCLUDE [support-disclaimer](../../../../includes/support-disclaimer.md)]

## <a name="collect-audit-logs"></a><span data-ttu-id="3d0dc-112">Os registos de auditoria de recolha</span><span class="sxs-lookup"><span data-stu-id="3d0dc-112">Collect audit logs</span></span>
<span data-ttu-id="3d0dc-113">toostart de resolução de problemas, auditoria Olá recolher os registos erro de Olá tooidentify associado ao problema Olá.</span><span class="sxs-lookup"><span data-stu-id="3d0dc-113">toostart troubleshooting, collect hello audit logs tooidentify hello error associated with hello issue.</span></span>

<span data-ttu-id="3d0dc-114">No portal do Azure Olá, clique em **procurar** > **máquinas virtuais** > *a máquina virtual do Linux*  >   **Definições** > **registos de auditoria**.</span><span class="sxs-lookup"><span data-stu-id="3d0dc-114">In hello Azure portal, click **Browse** > **Virtual machines** > *your Linux virtual machine* > **Settings** > **Audit logs**.</span></span>

## <a name="issue-error-when-starting-a-stopped-vm"></a><span data-ttu-id="3d0dc-115">Problema: Erro ao iniciar uma VM parada</span><span class="sxs-lookup"><span data-stu-id="3d0dc-115">Issue: Error when starting a stopped VM</span></span>
<span data-ttu-id="3d0dc-116">Tente toostart uma VM parada mas obtêm uma falha de alocação.</span><span class="sxs-lookup"><span data-stu-id="3d0dc-116">You try toostart a stopped VM but get an allocation failure.</span></span>

### <a name="cause"></a><span data-ttu-id="3d0dc-117">Causa</span><span class="sxs-lookup"><span data-stu-id="3d0dc-117">Cause</span></span>
<span data-ttu-id="3d0dc-118">pedido de Olá toostart Olá parado VM tem toobe tentada no cluster original Olá que aloja o serviço em nuvem Olá.</span><span class="sxs-lookup"><span data-stu-id="3d0dc-118">hello request toostart hello stopped VM has toobe attempted at hello original cluster that hosts hello cloud service.</span></span> <span data-ttu-id="3d0dc-119">No entanto, o cluster de Olá não tem o pedido de Olá toofulfill disponíveis de espaço livre.</span><span class="sxs-lookup"><span data-stu-id="3d0dc-119">However, hello cluster does not have free space available toofulfill hello request.</span></span>

### <a name="resolution"></a><span data-ttu-id="3d0dc-120">Resolução</span><span class="sxs-lookup"><span data-stu-id="3d0dc-120">Resolution</span></span>
* <span data-ttu-id="3d0dc-121">Criar um novo serviço de nuvem e associá-la a uma região ou uma rede virtual com base na região, mas não é um grupo de afinidade.</span><span class="sxs-lookup"><span data-stu-id="3d0dc-121">Create a new cloud service and associate it with either a region or a region-based virtual network, but not an affinity group.</span></span>
* <span data-ttu-id="3d0dc-122">Eliminar Olá parado VM.</span><span class="sxs-lookup"><span data-stu-id="3d0dc-122">Delete hello stopped VM.</span></span>
* <span data-ttu-id="3d0dc-123">Recrie Olá VM no novo serviço de nuvem Olá utilizando discos de Olá.</span><span class="sxs-lookup"><span data-stu-id="3d0dc-123">Recreate hello VM in hello new cloud service by using hello disks.</span></span>
* <span data-ttu-id="3d0dc-124">Iniciar Olá recriada VM.</span><span class="sxs-lookup"><span data-stu-id="3d0dc-124">Start hello re-created VM.</span></span>

<span data-ttu-id="3d0dc-125">Se obtiver um erro quando tenta toocreate um novo serviço em nuvem, tente novamente mais tarde ou alterar a região de Olá para o serviço em nuvem Olá.</span><span class="sxs-lookup"><span data-stu-id="3d0dc-125">If you get an error when trying toocreate a new cloud service, either retry at a later time or change hello region for hello cloud service.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3d0dc-126">novo serviço de nuvem Olá terá um novo nome e VIP, pelo que terá toochange essas informações para todas as dependências de Olá utilizam essas informações para o serviço em nuvem existente Olá.</span><span class="sxs-lookup"><span data-stu-id="3d0dc-126">hello new cloud service will have a new name and VIP, so you will need toochange that information for all hello dependencies that use that information for hello existing cloud service.</span></span>
> 
> 

## <a name="issue-error-when-resizing-an-existing-vm"></a><span data-ttu-id="3d0dc-127">Problema: Ocorreu um erro ao redimensionar uma VM existente</span><span class="sxs-lookup"><span data-stu-id="3d0dc-127">Issue: Error when resizing an existing VM</span></span>
<span data-ttu-id="3d0dc-128">Tente tooresize uma VM existente mas obtêm uma falha de alocação.</span><span class="sxs-lookup"><span data-stu-id="3d0dc-128">You try tooresize an existing VM but get an allocation failure.</span></span>

### <a name="cause"></a><span data-ttu-id="3d0dc-129">Causa</span><span class="sxs-lookup"><span data-stu-id="3d0dc-129">Cause</span></span>
<span data-ttu-id="3d0dc-130">pedido de Olá tooresize Olá VM tem toobe tentativa no cluster original Olá referido serviço em nuvem Olá anfitriões.</span><span class="sxs-lookup"><span data-stu-id="3d0dc-130">hello request tooresize hello VM has toobe attempted at hello original cluster that hosts hello cloud service.</span></span> <span data-ttu-id="3d0dc-131">No entanto, o cluster de Olá não suporta Olá solicitado o tamanho da VM.</span><span class="sxs-lookup"><span data-stu-id="3d0dc-131">However, hello cluster does not support hello requested VM size.</span></span>

### <a name="resolution"></a><span data-ttu-id="3d0dc-132">Resolução</span><span class="sxs-lookup"><span data-stu-id="3d0dc-132">Resolution</span></span>
<span data-ttu-id="3d0dc-133">Reduzir Olá solicitado o tamanho da VM e repita Olá redimensionar pedido.</span><span class="sxs-lookup"><span data-stu-id="3d0dc-133">Reduce hello requested VM size, and retry hello resize request.</span></span>

* <span data-ttu-id="3d0dc-134">Clique em **Procurar tudo** > **máquinas virtuais (clássicas)** > *a máquina virtual* > **definições** > **tamanho**.</span><span class="sxs-lookup"><span data-stu-id="3d0dc-134">Click **Browse all** > **Virtual machines (classic)** > *your virtual machine* > **Settings** > **Size**.</span></span> <span data-ttu-id="3d0dc-135">Para obter passos detalhados, consulte [redimensionar a máquina virtual de Olá](https://msdn.microsoft.com/library/dn168976.aspx).</span><span class="sxs-lookup"><span data-stu-id="3d0dc-135">For detailed steps, see [Resize hello virtual machine](https://msdn.microsoft.com/library/dn168976.aspx).</span></span>

<span data-ttu-id="3d0dc-136">Se não for possível tooreduce Olá tamanho da VM, siga estes passos:</span><span class="sxs-lookup"><span data-stu-id="3d0dc-136">If it is not possible tooreduce hello VM size, follow these steps:</span></span>

* <span data-ttu-id="3d0dc-137">Crie um novo serviço de nuvem, assegurar que não se trata de grupo de afinidade tooan ligado e não associados a uma rede virtual que é o grupo de afinidade tooan ligado.</span><span class="sxs-lookup"><span data-stu-id="3d0dc-137">Create a new cloud service, ensuring it is not linked tooan affinity group and not associated with a virtual network that is linked tooan affinity group.</span></span>
* <span data-ttu-id="3d0dc-138">Crie uma VM nova, maior dimensão no mesmo.</span><span class="sxs-lookup"><span data-stu-id="3d0dc-138">Create a new, larger-sized VM in it.</span></span>

<span data-ttu-id="3d0dc-139">Pode consolidar todas as suas VMs no Olá mesmo serviço em nuvem.</span><span class="sxs-lookup"><span data-stu-id="3d0dc-139">You can consolidate all your VMs in hello same cloud service.</span></span> <span data-ttu-id="3d0dc-140">Se o serviço em nuvem existente está associado uma rede virtual com base na região, pode ligar Olá novo nuvem serviço toohello rede virtual existente.</span><span class="sxs-lookup"><span data-stu-id="3d0dc-140">If your existing cloud service is associated with a region-based virtual network, you can connect hello new cloud service toohello existing virtual network.</span></span>

<span data-ttu-id="3d0dc-141">Se o serviço em nuvem existente Olá não estiver associado uma rede virtual com base na região, em seguida, pode ter toodelete Olá VMs num serviço em nuvem existente do Olá e recriá-los no Olá novo serviço em nuvem dos respetivos discos.</span><span class="sxs-lookup"><span data-stu-id="3d0dc-141">If hello existing cloud service is not associated with a region-based virtual network, then you have toodelete hello VMs in hello existing cloud service, and recreate them in hello new cloud service from their disks.</span></span> <span data-ttu-id="3d0dc-142">No entanto, é importante tooremember que novo serviço de nuvem Olá terá um novo nome e VIP, pelo que terá tooupdate estes para todas as dependências de Olá que a utilizam atualmente estas informações para o serviço em nuvem existente Olá.</span><span class="sxs-lookup"><span data-stu-id="3d0dc-142">However, it is important tooremember that hello new cloud service will have a new name and VIP, so you will need tooupdate these for all hello dependencies that currently use this information for hello existing cloud service.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3d0dc-143">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="3d0dc-143">Next steps</span></span>
<span data-ttu-id="3d0dc-144">Se ocorrerem problemas ao criar uma nova VM com Linux no Azure, consulte o artigo [resolver problemas de implementação com a criação de uma nova máquina virtual de Linux no Azure](../troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="3d0dc-144">If you encounter issues when you create a new Linux VM in Azure, see [Troubleshoot deployment issues with creating a new Linux virtual machine in Azure](../troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

