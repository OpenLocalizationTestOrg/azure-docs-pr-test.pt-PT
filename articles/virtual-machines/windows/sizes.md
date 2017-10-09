---
title: tamanhos aaaWindows VM no Azure | Microsoft Docs
description: "Apresenta uma lista de tamanhos diferentes Olá disponíveis para máquinas virtuais do Windows no Azure."
services: virtual-machines-windows
documentationcenter: 
author: jonbeck7
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: aabf0d30-04eb-4d34-b44a-69f8bfb84f22
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 07/28/2017
ms.author: jonbeck
ms.openlocfilehash: 80bd8241b134031c41b56224e841c7557c4845cf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="sizes-for-windows-virtual-machines-in-azure"></a><span data-ttu-id="34c13-103">Tamanhos de máquinas virtuais do Windows no Azure</span><span class="sxs-lookup"><span data-stu-id="34c13-103">Sizes for Windows virtual machines in Azure</span></span>

<span data-ttu-id="34c13-104">Este artigo descreve os tamanhos disponíveis Olá e opções para Olá máquinas virtuais do Azure, pode utilizar toorun as suas aplicações do Windows e cargas de trabalho.</span><span class="sxs-lookup"><span data-stu-id="34c13-104">This article describes hello available sizes and options for hello Azure virtual machines you can use toorun your Windows apps and workloads.</span></span> <span data-ttu-id="34c13-105">Também fornece toobe de considerações de implementação em consideração quando está a planear toouse estes recursos.</span><span class="sxs-lookup"><span data-stu-id="34c13-105">It also provides deployment considerations toobe aware of when you're planning toouse these resources.</span></span>  <span data-ttu-id="34c13-106">Este artigo também está disponível para [máquinas virtuais do Linux](../linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="34c13-106">This article is also available for [Linux virtual machines](../linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>


| <span data-ttu-id="34c13-107">Tipo</span><span class="sxs-lookup"><span data-stu-id="34c13-107">Type</span></span>                     | <span data-ttu-id="34c13-108">Tamanhos</span><span class="sxs-lookup"><span data-stu-id="34c13-108">Sizes</span></span>           |    <span data-ttu-id="34c13-109">Descrição</span><span class="sxs-lookup"><span data-stu-id="34c13-109">Description</span></span>       |
|--------------------------|-------------------|------------------------------------------------------------------------------------------------------------------------------------|
| [<span data-ttu-id="34c13-110">Fins gerais</span><span class="sxs-lookup"><span data-stu-id="34c13-110">General purpose</span></span>](sizes-general.md)          | <span data-ttu-id="34c13-111">Dsv3, Dv3, série DSv2, Dv2, DS, D, Av2, A0 7</span><span class="sxs-lookup"><span data-stu-id="34c13-111">Dsv3, Dv3, DSv2, Dv2, DS, D, Av2, A0-7</span></span> | <span data-ttu-id="34c13-112">Relação CPU/memória equilibrada.</span><span class="sxs-lookup"><span data-stu-id="34c13-112">Balanced CPU-to-memory ratio.</span></span> <span data-ttu-id="34c13-113">Ideal para teste e desenvolvimento, toomedium pequeno bases de dados e servidores de web de tráfego toomedium baixa.</span><span class="sxs-lookup"><span data-stu-id="34c13-113">Ideal for testing and development, small toomedium databases, and low toomedium traffic web servers.</span></span> |
| [<span data-ttu-id="34c13-114">Com otimização de computação</span><span class="sxs-lookup"><span data-stu-id="34c13-114">Compute optimized</span></span>](sizes-compute.md)        | <span data-ttu-id="34c13-115">FS, F</span><span class="sxs-lookup"><span data-stu-id="34c13-115">Fs, F</span></span>             | <span data-ttu-id="34c13-116">Relação CPU/memória elevada.</span><span class="sxs-lookup"><span data-stu-id="34c13-116">High CPU-to-memory ratio.</span></span> <span data-ttu-id="34c13-117">Ideal para servidores Web com tráfego médio, aplicações de rede, processos em lote e servidores de aplicações.</span><span class="sxs-lookup"><span data-stu-id="34c13-117">Good for medium traffic web servers, network appliances, batch processes, and application servers.</span></span>        |
| [<span data-ttu-id="34c13-118">Com otimização de memória</span><span class="sxs-lookup"><span data-stu-id="34c13-118">Memory optimized</span></span>](../virtual-machines-windows-sizes-memory.md)         | <span data-ttu-id="34c13-119">Esv3, Ev3, M, GS, G, série DSv2, DS, Dv2, D</span><span class="sxs-lookup"><span data-stu-id="34c13-119">Esv3, Ev3, M, GS, G, DSv2, DS, Dv2, D</span></span>   | <span data-ttu-id="34c13-120">Rácio de memória a CPU elevado.</span><span class="sxs-lookup"><span data-stu-id="34c13-120">High memory-to-CPU ratio.</span></span> <span data-ttu-id="34c13-121">Excelente para servidores de base de dados relacional, caches de toolarge média e análise de memória.</span><span class="sxs-lookup"><span data-stu-id="34c13-121">Great for relational database servers, medium toolarge caches, and in-memory analytics.</span></span>                 |
| [<span data-ttu-id="34c13-122">Com otimização de armazenamento</span><span class="sxs-lookup"><span data-stu-id="34c13-122">Storage optimized</span></span>](../virtual-machines-windows-sizes-storage.md)        | <span data-ttu-id="34c13-123">Ls</span><span class="sxs-lookup"><span data-stu-id="34c13-123">Ls</span></span>                | <span data-ttu-id="34c13-124">Débito e E/S de disco elevados.</span><span class="sxs-lookup"><span data-stu-id="34c13-124">High disk throughput and IO.</span></span> <span data-ttu-id="34c13-125">Ideal para bases de dados de Macrodados, SQL e NoSQL.</span><span class="sxs-lookup"><span data-stu-id="34c13-125">Ideal for Big Data, SQL, and NoSQL databases.</span></span>                                                         |
| [<span data-ttu-id="34c13-126">GPU</span><span class="sxs-lookup"><span data-stu-id="34c13-126">GPU</span></span>](sizes-gpu.md)            | <span data-ttu-id="34c13-127">NV, NC</span><span class="sxs-lookup"><span data-stu-id="34c13-127">NV, NC</span></span>            | <span data-ttu-id="34c13-128">Especializadas máquinas virtuais de destino para composição de gráfico pesada e edição de vídeo.</span><span class="sxs-lookup"><span data-stu-id="34c13-128">Specialized virtual machines targeted for heavy graphic rendering and video editing.</span></span> <span data-ttu-id="34c13-129">Disponível com GPUs único ou vários.</span><span class="sxs-lookup"><span data-stu-id="34c13-129">Available with single or multiple GPUs.</span></span>       |
| [<span data-ttu-id="34c13-130">Computação de elevado desempenho</span><span class="sxs-lookup"><span data-stu-id="34c13-130">High performance compute</span></span>](sizes-hpc.md) | <span data-ttu-id="34c13-131">H, A8-11</span><span class="sxs-lookup"><span data-stu-id="34c13-131">H, A8-11</span></span>          | <span data-ttu-id="34c13-132">As nossas máquinas virtuais com CPU mais rápidas e poderosas com interfaces de rede de alto débito (RDMA) opcionais.</span><span class="sxs-lookup"><span data-stu-id="34c13-132">Our fastest and most powerful CPU virtual machines with optional high-throughput network interfaces (RDMA).</span></span> 

<br> 

- <span data-ttu-id="34c13-133">Para obter informações sobre os preços de Olá tamanhos diversos, consulte [preços das Virtual Machines](https://azure.microsoft.com/pricing/details/virtual-machines/#Windows).</span><span class="sxs-lookup"><span data-stu-id="34c13-133">For information about pricing of hello various sizes, see [Virtual Machines Pricing](https://azure.microsoft.com/pricing/details/virtual-machines/#Windows).</span></span> 
- <span data-ttu-id="34c13-134">toosee limites geral em VMs do Azure, consulte [subscrição do Azure e limites de serviço, quotas e restrições](../../azure-subscription-service-limits.md).</span><span class="sxs-lookup"><span data-stu-id="34c13-134">toosee general limits on Azure VMs, see [Azure subscription and service limits, quotas, and constraints](../../azure-subscription-service-limits.md).</span></span>
- <span data-ttu-id="34c13-135">Os custos de armazenamento são calculados separadamente com base nas páginas utilizadas na conta do storage Olá.</span><span class="sxs-lookup"><span data-stu-id="34c13-135">Storage costs are calculated separately based on used pages in hello storage account.</span></span> <span data-ttu-id="34c13-136">Para obter detalhes, [preços do Storage do Azure](https://azure.microsoft.com/pricing/details/storage/).</span><span class="sxs-lookup"><span data-stu-id="34c13-136">For details, [Azure Storage Pricing](https://azure.microsoft.com/pricing/details/storage/).</span></span>
- <span data-ttu-id="34c13-137">Saiba mais sobre como [unidades (ACU) de computação do Azure](acu.md) podem ajudar a comparar o desempenho de computação em SKUs do Azure.</span><span class="sxs-lookup"><span data-stu-id="34c13-137">Learn more about how [Azure compute units (ACU)](acu.md) can help you compare compute performance across Azure SKUs.</span></span>



## <a name="rest-api"></a><span data-ttu-id="34c13-138">REST API</span><span class="sxs-lookup"><span data-stu-id="34c13-138">Rest API</span></span>

<span data-ttu-id="34c13-139">Para informações sobre como utilizar Olá tooquery de REST API para tamanhos de VM, consulte o seguinte Olá:</span><span class="sxs-lookup"><span data-stu-id="34c13-139">For information on using hello REST API tooquery for VM sizes, see hello following:</span></span>

- [<span data-ttu-id="34c13-140">Listar tamanhos de máquina virtual disponíveis para redimensionar</span><span class="sxs-lookup"><span data-stu-id="34c13-140">List available virtual machine sizes for resizing</span></span>](https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-list-sizes-for-resizing)
- [<span data-ttu-id="34c13-141">Listar tamanhos de máquina virtual disponíveis para uma subscrição</span><span class="sxs-lookup"><span data-stu-id="34c13-141">List available virtual machine sizes for a subscription</span></span>](https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-list-sizes-region)
- [<span data-ttu-id="34c13-142">Listar tamanhos de máquina virtual disponíveis num conjunto de disponibilidade</span><span class="sxs-lookup"><span data-stu-id="34c13-142">List available virtual machine sizes in an availability set</span></span>](
https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-list-sizes-availability-set)

## <a name="acu"></a><span data-ttu-id="34c13-143">ACU</span><span class="sxs-lookup"><span data-stu-id="34c13-143">ACU</span></span>

<span data-ttu-id="34c13-144">Saiba mais sobre como [unidades (ACU) de computação do Azure](acu.md) podem ajudar a comparar o desempenho de computação em SKUs do Azure.</span><span class="sxs-lookup"><span data-stu-id="34c13-144">Learn more about how [Azure compute units (ACU)](acu.md) can help you compare compute performance across Azure SKUs.</span></span>

## <a name="next-steps"></a><span data-ttu-id="34c13-145">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="34c13-145">Next steps</span></span>

<span data-ttu-id="34c13-146">Saiba mais sobre Olá diferentes tamanhos de VM que estão disponíveis:</span><span class="sxs-lookup"><span data-stu-id="34c13-146">Learn more about hello different VM sizes that are available:</span></span>
- [<span data-ttu-id="34c13-147">Fins gerais</span><span class="sxs-lookup"><span data-stu-id="34c13-147">General purpose</span></span>](sizes-general.md)
- [<span data-ttu-id="34c13-148">Com otimização de computação</span><span class="sxs-lookup"><span data-stu-id="34c13-148">Compute optimized</span></span>](sizes-compute.md)
- [<span data-ttu-id="34c13-149">Com otimização de memória</span><span class="sxs-lookup"><span data-stu-id="34c13-149">Memory optimized</span></span>](../virtual-machines-windows-sizes-memory.md)
- [<span data-ttu-id="34c13-150">Com otimização de armazenamento</span><span class="sxs-lookup"><span data-stu-id="34c13-150">Storage optimized</span></span>](../virtual-machines-windows-sizes-storage.md)
- [<span data-ttu-id="34c13-151">Com otimização de GPU</span><span class="sxs-lookup"><span data-stu-id="34c13-151">GPU optimized</span></span>](sizes-gpu.md)
- [<span data-ttu-id="34c13-152">Computação de elevado desempenho</span><span class="sxs-lookup"><span data-stu-id="34c13-152">High performance compute</span></span>](sizes-hpc.md)



