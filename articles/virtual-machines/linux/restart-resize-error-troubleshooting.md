---
title: aaaVM reiniciar ou redimensionar problemas no Azure | Microsoft Docs
description: "Resolver problemas de implementação do Resource Manager com reiniciar ou redimensionar uma Máquina Virtual de Linux existente no Azure"
services: virtual-machines-linux, azure-resource-manager
documentationcenter: 
author: Deland-Han
manager: felixwu
editor: 
tags: top-support-issue
ms.assetid: 51f1610c-0290-464a-97d4-c2e485c7ae7f
ms.service: virtual-machines-linux
ms.topic: support-article
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.workload: required
ms.date: 01/10/2017
ms.author: delhan
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d9ff76b64b6646b04565eb93110759c4ebc858e2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-deployment-issues-with-restarting-or-resizing-an-existing-linux-vm-in-azure"></a><span data-ttu-id="04d9b-103">Resolver problemas de implementação com reiniciar ou redimensionar uma VM com Linux existente no Azure</span><span class="sxs-lookup"><span data-stu-id="04d9b-103">Troubleshoot deployment issues with restarting or resizing an existing Linux VM in Azure</span></span>
<span data-ttu-id="04d9b-104">Quando tentar toostart uma Máquina Virtual do Azure (VM) parada ou redimensionar uma VM do Azure existente, o erro comum de Olá que ocorrerem é uma falha de alocação.</span><span class="sxs-lookup"><span data-stu-id="04d9b-104">When you try toostart a stopped Azure Virtual Machine (VM), or resize an existing Azure VM, hello common error you encounter is an allocation failure.</span></span> <span data-ttu-id="04d9b-105">Este erro resulta quando cluster Olá ou a região não ter recursos disponíveis ou não é suporte Olá pedir o tamanho da VM.</span><span class="sxs-lookup"><span data-stu-id="04d9b-105">This error results when hello cluster or region either does not have resources available or cannot support hello requested VM size.</span></span>

[!INCLUDE [support-disclaimer](../../../includes/support-disclaimer.md)]

## <a name="collect-activity-logs"></a><span data-ttu-id="04d9b-106">Regista a atividade de recolha</span><span class="sxs-lookup"><span data-stu-id="04d9b-106">Collect activity logs</span></span>
<span data-ttu-id="04d9b-107">toostart de resolução de problemas, atividade Olá recolher os registos erro de Olá tooidentify associado ao problema Olá.</span><span class="sxs-lookup"><span data-stu-id="04d9b-107">toostart troubleshooting, collect hello activity logs tooidentify hello error associated with hello issue.</span></span> <span data-ttu-id="04d9b-108">Olá seguintes ligações contém informações detalhadas sobre o processo de Olá:</span><span class="sxs-lookup"><span data-stu-id="04d9b-108">hello following links contain detailed information on hello process:</span></span>

[<span data-ttu-id="04d9b-109">Ver as operações de implementação</span><span class="sxs-lookup"><span data-stu-id="04d9b-109">View deployment operations</span></span>](../../azure-resource-manager/resource-manager-deployment-operations.md)

[<span data-ttu-id="04d9b-110">Ver registos de atividade toomanage Azure recursos</span><span class="sxs-lookup"><span data-stu-id="04d9b-110">View activity logs toomanage Azure resources</span></span>](../../resource-group-audit.md)

## <a name="issue-error-when-starting-a-stopped-vm"></a><span data-ttu-id="04d9b-111">Problema: Erro ao iniciar uma VM parada</span><span class="sxs-lookup"><span data-stu-id="04d9b-111">Issue: Error when starting a stopped VM</span></span>
<span data-ttu-id="04d9b-112">Tente toostart uma VM parada mas obtêm uma falha de alocação.</span><span class="sxs-lookup"><span data-stu-id="04d9b-112">You try toostart a stopped VM but get an allocation failure.</span></span>

### <a name="cause"></a><span data-ttu-id="04d9b-113">Causa</span><span class="sxs-lookup"><span data-stu-id="04d9b-113">Cause</span></span>
<span data-ttu-id="04d9b-114">pedido de Olá toostart Olá parado VM tem toobe tentada no cluster original Olá que aloja o serviço em nuvem Olá.</span><span class="sxs-lookup"><span data-stu-id="04d9b-114">hello request toostart hello stopped VM has toobe attempted at hello original cluster that hosts hello cloud service.</span></span> <span data-ttu-id="04d9b-115">No entanto, o cluster de Olá não tem o pedido de Olá toofulfill disponíveis de espaço livre.</span><span class="sxs-lookup"><span data-stu-id="04d9b-115">However, hello cluster does not have free space available toofulfill hello request.</span></span>

### <a name="resolution"></a><span data-ttu-id="04d9b-116">Resolução</span><span class="sxs-lookup"><span data-stu-id="04d9b-116">Resolution</span></span>
* <span data-ttu-id="04d9b-117">Pare Olá todas as VMs na disponibilidade de Olá definido e, em seguida, reiniciar cada VM.</span><span class="sxs-lookup"><span data-stu-id="04d9b-117">Stop all hello VMs in hello availability set, and then restart each VM.</span></span>
  
  1. <span data-ttu-id="04d9b-118">Clique em **grupos de recursos** > *o grupo de recursos* > **recursos** > *o conjunto de disponibilidade* > **máquinas virtuais** > *a máquina virtual* > **parar**.</span><span class="sxs-lookup"><span data-stu-id="04d9b-118">Click **Resource groups** > *your resource group* > **Resources** > *your availability set* > **Virtual Machines** > *your virtual machine* > **Stop**.</span></span>
  2. <span data-ttu-id="04d9b-119">Após todos os Olá parar de VMs, selecione cada uma das VMs Olá parado e clique em Iniciar.</span><span class="sxs-lookup"><span data-stu-id="04d9b-119">After all hello VMs stop, select each of hello stopped VMs and click Start.</span></span>
* <span data-ttu-id="04d9b-120">Repetir o pedido de reinício de Olá numa altura posterior.</span><span class="sxs-lookup"><span data-stu-id="04d9b-120">Retry hello restart request at a later time.</span></span>

## <a name="issue-error-when-resizing-an-existing-vm"></a><span data-ttu-id="04d9b-121">Problema: Ocorreu um erro ao redimensionar uma VM existente</span><span class="sxs-lookup"><span data-stu-id="04d9b-121">Issue: Error when resizing an existing VM</span></span>
<span data-ttu-id="04d9b-122">Tente tooresize uma VM existente mas obtêm uma falha de alocação.</span><span class="sxs-lookup"><span data-stu-id="04d9b-122">You try tooresize an existing VM but get an allocation failure.</span></span>

### <a name="cause"></a><span data-ttu-id="04d9b-123">Causa</span><span class="sxs-lookup"><span data-stu-id="04d9b-123">Cause</span></span>
<span data-ttu-id="04d9b-124">pedido de Olá tooresize Olá VM tem toobe tentativa no cluster original Olá referido serviço em nuvem Olá anfitriões.</span><span class="sxs-lookup"><span data-stu-id="04d9b-124">hello request tooresize hello VM has toobe attempted at hello original cluster that hosts hello cloud service.</span></span> <span data-ttu-id="04d9b-125">No entanto, o cluster de Olá não suporta Olá solicitado o tamanho da VM.</span><span class="sxs-lookup"><span data-stu-id="04d9b-125">However, hello cluster does not support hello requested VM size.</span></span>

### <a name="resolution"></a><span data-ttu-id="04d9b-126">Resolução</span><span class="sxs-lookup"><span data-stu-id="04d9b-126">Resolution</span></span>
* <span data-ttu-id="04d9b-127">Repita o pedido de Olá utilizando um tamanho mais pequeno da VM.</span><span class="sxs-lookup"><span data-stu-id="04d9b-127">Retry hello request using a smaller VM size.</span></span>
* <span data-ttu-id="04d9b-128">Se hello o tamanho do Olá pedido que não é possível alterar a VM:</span><span class="sxs-lookup"><span data-stu-id="04d9b-128">If hello size of hello requested VM cannot be changed：</span></span>
  
  1. <span data-ttu-id="04d9b-129">Pare todas as VMs de Olá no conjunto de disponibilidade de Olá.</span><span class="sxs-lookup"><span data-stu-id="04d9b-129">Stop all hello VMs in hello availability set.</span></span>
     
     * <span data-ttu-id="04d9b-130">Clique em **grupos de recursos** > *o grupo de recursos* > **recursos** > *o conjunto de disponibilidade* > **máquinas virtuais** > *a máquina virtual* > **parar**.</span><span class="sxs-lookup"><span data-stu-id="04d9b-130">Click **Resource groups** > *your resource group* > **Resources** > *your availability set* > **Virtual Machines** > *your virtual machine* > **Stop**.</span></span>
  2. <span data-ttu-id="04d9b-131">Após todos os hello VMs parar, redimensionar Olá pretendido tooa VM tamanho maior.</span><span class="sxs-lookup"><span data-stu-id="04d9b-131">After all hello VMs stop, resize hello desired VM tooa larger size.</span></span>
  3. <span data-ttu-id="04d9b-132">Selecione Olá redimensionado VM e clique em **iniciar**, e, em seguida, inicie cada Olá parado VMs.</span><span class="sxs-lookup"><span data-stu-id="04d9b-132">Select hello resized VM and click **Start**, and then start each of hello stopped VMs.</span></span>

## <a name="next-steps"></a><span data-ttu-id="04d9b-133">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="04d9b-133">Next steps</span></span>
<span data-ttu-id="04d9b-134">Se ocorrerem problemas ao criar uma nova VM com Linux no Azure, consulte o artigo [resolver problemas de implementação com a criação de uma nova máquina virtual de Linux no Azure](troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="04d9b-134">If you encounter issues when you create a new Linux VM in Azure, see [Troubleshoot deployment issues with creating a new Linux virtual machine in Azure](troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

