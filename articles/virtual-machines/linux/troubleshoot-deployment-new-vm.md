---
title: "aaaTroubleshoot implementação-RM de VM com Linux | Microsoft Docs"
description: "Resolver problemas de implementação do Resource Manager, quando criar uma nova máquina virtual de Linux no Azure"
services: virtual-machines-linux, azure-resource-manager
documentationcenter: 
author: JiangChen79
manager: felixwu
editor: 
tags: top-support-issue, azure-resource-manager
ms.assetid: 906a9c89-6866-496b-b4a4-f07fb39f990c
ms.service: virtual-machines-linux
ms.workload: na
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 09/09/2016
ms.author: cjiang
ms.openlocfilehash: 2dd7f1855bba75d86eb90f88e6d573cd42fd8d87
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-resource-manager-deployment-issues-with-creating-a-new-linux-virtual-machine-in-azure"></a><span data-ttu-id="e2c33-103">Resolver problemas de implementação do Resource Manager com a criação de uma nova máquina virtual de Linux no Azure</span><span class="sxs-lookup"><span data-stu-id="e2c33-103">Troubleshoot Resource Manager deployment issues with creating a new Linux virtual machine in Azure</span></span>
[!INCLUDE [virtual-machines-troubleshoot-deployment-new-vm-opening](../../../includes/virtual-machines-troubleshoot-deployment-new-vm-opening-include.md)]

[!INCLUDE [support-disclaimer](../../../includes/support-disclaimer.md)]

## <a name="top-issues"></a><span data-ttu-id="e2c33-104">Problemas principais</span><span class="sxs-lookup"><span data-stu-id="e2c33-104">Top issues</span></span>
[!INCLUDE [support-disclaimer](../../../includes/virtual-machines-linux-troubleshoot-deploy-vm-top.md)]

<span data-ttu-id="e2c33-105">Para outros problemas de implementação da VM e perguntas, consulte [resolver problemas de máquina virtual Linux implementar no Azure](troubleshoot-deploy-vm.md).</span><span class="sxs-lookup"><span data-stu-id="e2c33-105">For other VM deployment issues and questions, see [Troubleshoot deploying Linux virtual machine issues in Azure](troubleshoot-deploy-vm.md).</span></span>
## <a name="collect-activity-logs"></a><span data-ttu-id="e2c33-106">Regista a atividade de recolha</span><span class="sxs-lookup"><span data-stu-id="e2c33-106">Collect activity logs</span></span>
<span data-ttu-id="e2c33-107">toostart de resolução de problemas, atividade Olá recolher os registos erro de Olá tooidentify associado ao problema Olá.</span><span class="sxs-lookup"><span data-stu-id="e2c33-107">toostart troubleshooting, collect hello activity logs tooidentify hello error associated with hello issue.</span></span> <span data-ttu-id="e2c33-108">Olá ligações seguintes contêm informações detalhadas sobre Olá toofollow de processo.</span><span class="sxs-lookup"><span data-stu-id="e2c33-108">hello following links contain detailed information on hello process toofollow.</span></span>

[<span data-ttu-id="e2c33-109">Ver as operações de implementação</span><span class="sxs-lookup"><span data-stu-id="e2c33-109">View deployment operations</span></span>](../../azure-resource-manager/resource-manager-deployment-operations.md)

[<span data-ttu-id="e2c33-110">Ver registos de atividade toomanage Azure recursos</span><span class="sxs-lookup"><span data-stu-id="e2c33-110">View activity logs toomanage Azure resources</span></span>](../../resource-group-audit.md)

[!INCLUDE [virtual-machines-troubleshoot-deployment-new-vm-issue1](../../../includes/virtual-machines-troubleshoot-deployment-new-vm-issue1-include.md)]

[!INCLUDE [virtual-machines-linux-troubleshoot-deployment-new-vm-table](../../../includes/virtual-machines-linux-troubleshoot-deployment-new-vm-table.md)]

<span data-ttu-id="e2c33-111">**Y:** se Olá SO é Linux generalizado e é carregado e/ou capturado com Olá generalizado definição, em seguida, haverá quaisquer erros.</span><span class="sxs-lookup"><span data-stu-id="e2c33-111">**Y:** If hello OS is Linux generalized, and it is uploaded and/or captured with hello generalized setting, then there won’t be any errors.</span></span> <span data-ttu-id="e2c33-112">Da mesma forma, se Olá SO é especializada do Linux, e é carregado e/ou capturado com Olá especializada definição, em seguida, haverá quaisquer erros.</span><span class="sxs-lookup"><span data-stu-id="e2c33-112">Similarly, if hello OS is Linux specialized, and it is uploaded and/or captured with hello specialized setting, then there won’t be any errors.</span></span>

<span data-ttu-id="e2c33-113">**Carregar erros:**</span><span class="sxs-lookup"><span data-stu-id="e2c33-113">**Upload Errors:**</span></span>

<span data-ttu-id="e2c33-114">**N<sup>1</sup>:** se Olá SO Linux generalizado, e ser carregada como especializada, obterá um erro de tempo limite de aprovisionamento porque Olá VM é bloqueada no Olá fase de aprovisionamento.</span><span class="sxs-lookup"><span data-stu-id="e2c33-114">**N<sup>1</sup>:** If hello OS is Linux generalized, and it is uploaded as specialized, you will get a provisioning timeout error because hello VM is stuck at hello provisioning stage.</span></span>

<span data-ttu-id="e2c33-115">**N<sup>2</sup>:** esteja Olá SO Linux especializada e ser carregada como generalizado, obterá um erro de falha de aprovisionamento porque hello nova VM está em execução com o nome do computador original Olá, nome de utilizador e palavra-passe.</span><span class="sxs-lookup"><span data-stu-id="e2c33-115">**N<sup>2</sup>:** If hello OS is Linux specialized, and it is uploaded as generalized, you will get a provisioning failure error because hello new VM is running with hello original computer name, username and password.</span></span>

<span data-ttu-id="e2c33-116">**Resolução:**</span><span class="sxs-lookup"><span data-stu-id="e2c33-116">**Resolution:**</span></span>

<span data-ttu-id="e2c33-117">tooresolve ambos estes erros, carregar Olá VHD original, disponível no local, com Olá, mesmo que a definição Olá SO (generalizado/especializado).</span><span class="sxs-lookup"><span data-stu-id="e2c33-117">tooresolve both these errors, upload hello original VHD, available on-prem, with hello same setting as that for hello OS (generalized/specialized).</span></span> <span data-ttu-id="e2c33-118">tooupload como generalizado, lembre-se toorun-desaprovisionar primeiro.</span><span class="sxs-lookup"><span data-stu-id="e2c33-118">tooupload as generalized, remember toorun -deprovision first.</span></span>

<span data-ttu-id="e2c33-119">**Captura de erros:**</span><span class="sxs-lookup"><span data-stu-id="e2c33-119">**Capture Errors:**</span></span>

<span data-ttu-id="e2c33-120">**N<sup>3</sup>:** se Olá SO Linux generalizado, e é capturado como especializada, obterá um erro de tempo limite de aprovisionamento porque Olá original VM não é utilizável está marcado como generalizado.</span><span class="sxs-lookup"><span data-stu-id="e2c33-120">**N<sup>3</sup>:** If hello OS is Linux generalized, and it is captured as specialized, you will get a provisioning timeout error because hello original VM is not usable as it is marked as generalized.</span></span>

<span data-ttu-id="e2c33-121">**N<sup>4</sup>:** esteja Olá SO Linux especializada e é capturado como generalizado, obterá um erro de falha de aprovisionamento porque hello nova VM está em execução com o nome do computador original Olá, nome de utilizador e palavra-passe.</span><span class="sxs-lookup"><span data-stu-id="e2c33-121">**N<sup>4</sup>:** If hello OS is Linux specialized, and it is captured as generalized, you will get a provisioning failure error because hello new VM is running with hello original computer name, username and password.</span></span> <span data-ttu-id="e2c33-122">Além disso, Olá original VM não é utilizável porque está marcado como especializado.</span><span class="sxs-lookup"><span data-stu-id="e2c33-122">Also, hello original VM is not usable because it is marked as specialized.</span></span>

<span data-ttu-id="e2c33-123">**Resolução:**</span><span class="sxs-lookup"><span data-stu-id="e2c33-123">**Resolution:**</span></span>

<span data-ttu-id="e2c33-124">tooresolve ambos estes erros, eliminar imagem atual Olá do portal de Olá, e [recapturá-lo a partir de Olá VHDs atuais](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) com Olá, mesmo que a definição Olá SO (generalizado/especializado).</span><span class="sxs-lookup"><span data-stu-id="e2c33-124">tooresolve both these errors, delete hello current image from hello portal, and [recapture it from hello current VHDs](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) with hello same setting as that for hello OS (generalized/specialized).</span></span>

## <a name="issue-custom-gallery-marketplace-image-allocation-failure"></a><span data-ttu-id="e2c33-125">Problema: Personalizada / Galeria / imagem do marketplace; Falha de alocação</span><span class="sxs-lookup"><span data-stu-id="e2c33-125">Issue: Custom/ gallery/ marketplace image; allocation failure</span></span>
<span data-ttu-id="e2c33-126">Este erro for em situações quando novo pedido de VM Olá é afixado tooa de cluster que não suporta o tamanho da VM Olá que está a ser solicitado, ou não têm o pedido de Olá tooaccommodate de espaço livre disponível.</span><span class="sxs-lookup"><span data-stu-id="e2c33-126">This error arises in situations when hello new VM request is pinned tooa cluster that either cannot support hello VM size being requested, or does not have available free space tooaccommodate hello request.</span></span>

<span data-ttu-id="e2c33-127">**Causa 1:** cluster Olá não pode suportar Olá solicitado o tamanho da VM.</span><span class="sxs-lookup"><span data-stu-id="e2c33-127">**Cause 1:** hello cluster cannot support hello requested VM size.</span></span>

<span data-ttu-id="e2c33-128">**Resolução 1:**</span><span class="sxs-lookup"><span data-stu-id="e2c33-128">**Resolution 1:**</span></span>

* <span data-ttu-id="e2c33-129">Repita o pedido de Olá utilizando um tamanho mais pequeno da VM.</span><span class="sxs-lookup"><span data-stu-id="e2c33-129">Retry hello request using a smaller VM size.</span></span>
* <span data-ttu-id="e2c33-130">Se hello o tamanho do Olá pedido que não é possível alterar a VM:</span><span class="sxs-lookup"><span data-stu-id="e2c33-130">If hello size of hello requested VM cannot be changed:</span></span>
  * <span data-ttu-id="e2c33-131">Pare todas as VMs de Olá no conjunto de disponibilidade de Olá.</span><span class="sxs-lookup"><span data-stu-id="e2c33-131">Stop all hello VMs in hello availability set.</span></span>
    <span data-ttu-id="e2c33-132">Clique em **grupos de recursos** > *o grupo de recursos* > **recursos** > *o conjunto de disponibilidade* > **máquinas virtuais** > *a máquina virtual* > **parar**.</span><span class="sxs-lookup"><span data-stu-id="e2c33-132">Click **Resource groups** > *your resource group* > **Resources** > *your availability set* > **Virtual Machines** > *your virtual machine* > **Stop**.</span></span>
  * <span data-ttu-id="e2c33-133">Depois de todos os hello parar de VMs, criar Olá nova VM na Olá pretendido tamanho.</span><span class="sxs-lookup"><span data-stu-id="e2c33-133">After all hello VMs stop, create hello new VM in hello desired size.</span></span>
  * <span data-ttu-id="e2c33-134">Iniciar Olá nova VM primeiro e, em seguida, selecione cada Olá parado VMs e clique em **iniciar**.</span><span class="sxs-lookup"><span data-stu-id="e2c33-134">Start hello new VM first, and then select each of hello stopped VMs and click **Start**.</span></span>

<span data-ttu-id="e2c33-135">**Causa 2:** Olá cluster não tem recursos gratuitos.</span><span class="sxs-lookup"><span data-stu-id="e2c33-135">**Cause 2:** hello cluster does not have free resources.</span></span>

<span data-ttu-id="e2c33-136">**Resolução de 2:**</span><span class="sxs-lookup"><span data-stu-id="e2c33-136">**Resolution 2:**</span></span>

* <span data-ttu-id="e2c33-137">Repita o pedido de Olá numa altura posterior.</span><span class="sxs-lookup"><span data-stu-id="e2c33-137">Retry hello request at a later time.</span></span>
* <span data-ttu-id="e2c33-138">Se hello nova VM pode ser faz parte de uma disponibilidade diferente conjunto</span><span class="sxs-lookup"><span data-stu-id="e2c33-138">If hello new VM can be part of a different availability set</span></span>
  * <span data-ttu-id="e2c33-139">Criar uma nova VM num conjunto de disponibilidade diferente (no Olá mesma região).</span><span class="sxs-lookup"><span data-stu-id="e2c33-139">Create a new VM in a different availability set (in hello same region).</span></span>
  * <span data-ttu-id="e2c33-140">Adicionar Olá nova VM toohello mesma rede virtual.</span><span class="sxs-lookup"><span data-stu-id="e2c33-140">Add hello new VM toohello same virtual network.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e2c33-141">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="e2c33-141">Next steps</span></span>
<span data-ttu-id="e2c33-142">Se ocorrerem problemas ao iniciar uma VM com Linux parada ou redimensionar uma VM com Linux existente no Azure, consulte o artigo [problemas de implementação do Gestor de recursos de resolução de problemas com reiniciar ou redimensionar uma Máquina Virtual de Linux existente no Azure](restart-resize-error-troubleshooting.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e2c33-142">If you encounter issues when you start a stopped Linux VM or resize an existing Linux VM in Azure, see [Troubleshoot Resource Manager deployment issues with restarting or resizing an existing Linux Virtual Machine in Azure](restart-resize-error-troubleshooting.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

