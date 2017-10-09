---
title: "aaaManage Azure discos com Olá CLI do Azure | Microsoft Docs"
description: "Tutorial - Gerir discos do Azure com Olá CLI do Azure"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/02/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: ad29cfbec5f9738f47705b19d0450c9a2f555492
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-disks-with-hello-azure-cli"></a><span data-ttu-id="e28b4-103">Gerir discos do Azure com Olá CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="e28b4-103">Manage Azure disks with hello Azure CLI</span></span>

<span data-ttu-id="e28b4-104">Máquinas virtuais do Azure utilizar sistema de operativo discos toostore Olá VMs, aplicações e dados.</span><span class="sxs-lookup"><span data-stu-id="e28b4-104">Azure virtual machines use disks toostore hello VMs operating system, applications, and data.</span></span> <span data-ttu-id="e28b4-105">Quando cria uma VM é importante toochoose um tamanho de disco e a carga de trabalho de toohello adequado esperado de configuração.</span><span class="sxs-lookup"><span data-stu-id="e28b4-105">When creating a VM it is important toochoose a disk size and configuration appropriate toohello expected workload.</span></span> <span data-ttu-id="e28b4-106">Este tutorial abrange a implementação e gestão de discos VM.</span><span class="sxs-lookup"><span data-stu-id="e28b4-106">This tutorial covers deploying and managing VM disks.</span></span> <span data-ttu-id="e28b4-107">Pode obter informações sobre:</span><span class="sxs-lookup"><span data-stu-id="e28b4-107">You learn about:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="e28b4-108">Discos de SO e discos temporários</span><span class="sxs-lookup"><span data-stu-id="e28b4-108">OS disks and temporary disks</span></span>
> * <span data-ttu-id="e28b4-109">discos de dados</span><span class="sxs-lookup"><span data-stu-id="e28b4-109">Data disks</span></span>
> * <span data-ttu-id="e28b4-110">Standard e discos Premium</span><span class="sxs-lookup"><span data-stu-id="e28b4-110">Standard and Premium disks</span></span>
> * <span data-ttu-id="e28b4-111">Desempenho de disco</span><span class="sxs-lookup"><span data-stu-id="e28b4-111">Disk performance</span></span>
> * <span data-ttu-id="e28b4-112">Anexar e preparar os discos de dados</span><span class="sxs-lookup"><span data-stu-id="e28b4-112">Attaching and preparing data disks</span></span>
> * <span data-ttu-id="e28b4-113">O redimensionamento de discos</span><span class="sxs-lookup"><span data-stu-id="e28b4-113">Resizing disks</span></span>
> * <span data-ttu-id="e28b4-114">Instantâneos de disco</span><span class="sxs-lookup"><span data-stu-id="e28b4-114">Disk snapshots</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="e28b4-115">Se escolher tooinstall e utilizar Olá CLI localmente, este tutorial, necessita que está a executar versão CLI do Azure de Olá 2.0.4 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="e28b4-115">If you choose tooinstall and use hello CLI locally, this tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="e28b4-116">Executar `az --version` versão de Olá toofind.</span><span class="sxs-lookup"><span data-stu-id="e28b4-116">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="e28b4-117">Se precisar de tooinstall ou atualização, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="e28b4-117">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="default-azure-disks"></a><span data-ttu-id="e28b4-118">Predefinição discos do Azure</span><span class="sxs-lookup"><span data-stu-id="e28b4-118">Default Azure disks</span></span>

<span data-ttu-id="e28b4-119">Quando é criada uma máquina virtual do Azure, dois discos são automaticamente anexados toohello máquina.</span><span class="sxs-lookup"><span data-stu-id="e28b4-119">When an Azure virtual machine is created, two disks are automatically attached toohello virtual machine.</span></span> 

<span data-ttu-id="e28b4-120">**Disco do sistema operativo** - discos de sistema operativo podem ser dimensionados de forma segurança too1 terabyte e anfitriões Olá sistema de operativo VMs.</span><span class="sxs-lookup"><span data-stu-id="e28b4-120">**Operating system disk** - Operating system disks can be sized up too1 terabyte, and hosts hello VMs operating system.</span></span> <span data-ttu-id="e28b4-121">etiqueta do disco de SO de Olá */dev/sda* por predefinição.</span><span class="sxs-lookup"><span data-stu-id="e28b4-121">hello OS disk is labeled */dev/sda* by default.</span></span> <span data-ttu-id="e28b4-122">disco Olá colocação em cache de configuração do disco do SO Olá está otimizado para desempenho do SO.</span><span class="sxs-lookup"><span data-stu-id="e28b4-122">hello disk caching configuration of hello OS disk is optimized for OS performance.</span></span> <span data-ttu-id="e28b4-123">Devido a esta configuração, Olá disco do SO **não devem** alojar aplicações ou dados.</span><span class="sxs-lookup"><span data-stu-id="e28b4-123">Because of this configuration, hello OS disk **should not** host applications or data.</span></span> <span data-ttu-id="e28b4-124">Para aplicações e dados, utilize os discos de dados, que estão descritos neste artigo.</span><span class="sxs-lookup"><span data-stu-id="e28b4-124">For applications and data, use data disks, which are detailed later in this article.</span></span> 

<span data-ttu-id="e28b4-125">**Disco temporário** -temporários discos utilizam uma unidade de estado sólido que está localizada em Olá mesmo anfitrião do Azure como Olá VM.</span><span class="sxs-lookup"><span data-stu-id="e28b4-125">**Temporary disk** - Temporary disks use a solid-state drive that is located on hello same Azure host as hello VM.</span></span> <span data-ttu-id="e28b4-126">Discos temporários são altamente performant e podem ser utilizados para operações, tais como o processamento de dados temporária.</span><span class="sxs-lookup"><span data-stu-id="e28b4-126">Temp disks are highly performant and may be used for operations such as temporary data processing.</span></span> <span data-ttu-id="e28b4-127">No entanto, se Olá VM for movido tooa novo anfitrião, todos os dados armazenados num disco temporário são removidos.</span><span class="sxs-lookup"><span data-stu-id="e28b4-127">However, if hello VM is moved tooa new host, any data stored on a temporary disk is removed.</span></span> <span data-ttu-id="e28b4-128">o tamanho do disco temporário Olá Olá é determinado pelo Olá tamanho da VM.</span><span class="sxs-lookup"><span data-stu-id="e28b4-128">hello size of hello temporary disk is determined by hello VM size.</span></span> <span data-ttu-id="e28b4-129">Discos temporários são etiquetados */dev/sdb* e ter uma pontodemontagem de */mnt*.</span><span class="sxs-lookup"><span data-stu-id="e28b4-129">Temporary disks are labeled */dev/sdb* and have a mountpoint of */mnt*.</span></span>

### <a name="temporary-disk-sizes"></a><span data-ttu-id="e28b4-130">Tamanhos de disco temporário</span><span class="sxs-lookup"><span data-stu-id="e28b4-130">Temporary disk sizes</span></span>

| <span data-ttu-id="e28b4-131">Tipo</span><span class="sxs-lookup"><span data-stu-id="e28b4-131">Type</span></span> | <span data-ttu-id="e28b4-132">Tamanho da VM</span><span class="sxs-lookup"><span data-stu-id="e28b4-132">VM Size</span></span> | <span data-ttu-id="e28b4-133">Tamanho máximo de disco temporário (GB)</span><span class="sxs-lookup"><span data-stu-id="e28b4-133">Max temp disk size (GB)</span></span> |
|----|----|----|
| [<span data-ttu-id="e28b4-134">Fins gerais</span><span class="sxs-lookup"><span data-stu-id="e28b4-134">General purpose</span></span>](sizes-general.md) | <span data-ttu-id="e28b4-135">A e a série de D</span><span class="sxs-lookup"><span data-stu-id="e28b4-135">A and D series</span></span> | <span data-ttu-id="e28b4-136">800</span><span class="sxs-lookup"><span data-stu-id="e28b4-136">800</span></span> |
| [<span data-ttu-id="e28b4-137">Com otimização de computação</span><span class="sxs-lookup"><span data-stu-id="e28b4-137">Compute optimized</span></span>](sizes-compute.md) | <span data-ttu-id="e28b4-138">Série F</span><span class="sxs-lookup"><span data-stu-id="e28b4-138">F series</span></span> | <span data-ttu-id="e28b4-139">800</span><span class="sxs-lookup"><span data-stu-id="e28b4-139">800</span></span> |
| [<span data-ttu-id="e28b4-140">Com otimização de memória</span><span class="sxs-lookup"><span data-stu-id="e28b4-140">Memory optimized</span></span>](../virtual-machines-windows-sizes-memory.md) | <span data-ttu-id="e28b4-141">Série de D e G</span><span class="sxs-lookup"><span data-stu-id="e28b4-141">D and G series</span></span> | <span data-ttu-id="e28b4-142">6144</span><span class="sxs-lookup"><span data-stu-id="e28b4-142">6144</span></span> |
| [<span data-ttu-id="e28b4-143">Com otimização de armazenamento</span><span class="sxs-lookup"><span data-stu-id="e28b4-143">Storage optimized</span></span>](../virtual-machines-windows-sizes-storage.md) | <span data-ttu-id="e28b4-144">Série de L</span><span class="sxs-lookup"><span data-stu-id="e28b4-144">L series</span></span> | <span data-ttu-id="e28b4-145">5630</span><span class="sxs-lookup"><span data-stu-id="e28b4-145">5630</span></span> |
| [<span data-ttu-id="e28b4-146">GPU</span><span class="sxs-lookup"><span data-stu-id="e28b4-146">GPU</span></span>](sizes-gpu.md) | <span data-ttu-id="e28b4-147">Série N</span><span class="sxs-lookup"><span data-stu-id="e28b4-147">N series</span></span> | <span data-ttu-id="e28b4-148">1440</span><span class="sxs-lookup"><span data-stu-id="e28b4-148">1440</span></span> |
| [<span data-ttu-id="e28b4-149">Elevado desempenho</span><span class="sxs-lookup"><span data-stu-id="e28b4-149">High performance</span></span>](sizes-hpc.md) | <span data-ttu-id="e28b4-150">A e a série de H</span><span class="sxs-lookup"><span data-stu-id="e28b4-150">A and H series</span></span> | <span data-ttu-id="e28b4-151">2000</span><span class="sxs-lookup"><span data-stu-id="e28b4-151">2000</span></span> |

## <a name="azure-data-disks"></a><span data-ttu-id="e28b4-152">Discos de dados do Azure</span><span class="sxs-lookup"><span data-stu-id="e28b4-152">Azure data disks</span></span>

<span data-ttu-id="e28b4-153">Discos de dados adicionais podem ser adicionados para instalar aplicações e armazenar dados.</span><span class="sxs-lookup"><span data-stu-id="e28b4-153">Additional data disks can be added for installing applications and storing data.</span></span> <span data-ttu-id="e28b4-154">Os discos de dados devem ser utilizados em qualquer situação em que o armazenamento de dados durável e reativa for pretendido.</span><span class="sxs-lookup"><span data-stu-id="e28b4-154">Data disks should be used in any situation where durable and responsive data storage is desired.</span></span> <span data-ttu-id="e28b4-155">Cada disco de dados tem uma capacidade máxima de 1 terabyte.</span><span class="sxs-lookup"><span data-stu-id="e28b4-155">Each data disk has a maximum capacity of 1 terabyte.</span></span> <span data-ttu-id="e28b4-156">o tamanho da máquina virtual de Olá Olá determina quantos discos de dados podem ser anexado tooa VM.</span><span class="sxs-lookup"><span data-stu-id="e28b4-156">hello size of hello virtual machine determines how many data disks can be attached tooa VM.</span></span> <span data-ttu-id="e28b4-157">Para cada núcleo VM, podem ser anexados a discos de dados de dois.</span><span class="sxs-lookup"><span data-stu-id="e28b4-157">For each VM core, two data disks can be attached.</span></span> 

### <a name="max-data-disks-per-vm"></a><span data-ttu-id="e28b4-158">Discos de dados de máx. por VM</span><span class="sxs-lookup"><span data-stu-id="e28b4-158">Max data disks per VM</span></span>

| <span data-ttu-id="e28b4-159">Tipo</span><span class="sxs-lookup"><span data-stu-id="e28b4-159">Type</span></span> | <span data-ttu-id="e28b4-160">Tamanho da VM</span><span class="sxs-lookup"><span data-stu-id="e28b4-160">VM Size</span></span> | <span data-ttu-id="e28b4-161">Discos de dados de máx. por VM</span><span class="sxs-lookup"><span data-stu-id="e28b4-161">Max data disks per VM</span></span> |
|----|----|----|
| [<span data-ttu-id="e28b4-162">Fins gerais</span><span class="sxs-lookup"><span data-stu-id="e28b4-162">General purpose</span></span>](sizes-general.md) | <span data-ttu-id="e28b4-163">A e a série de D</span><span class="sxs-lookup"><span data-stu-id="e28b4-163">A and D series</span></span> | <span data-ttu-id="e28b4-164">32</span><span class="sxs-lookup"><span data-stu-id="e28b4-164">32</span></span> |
| [<span data-ttu-id="e28b4-165">Com otimização de computação</span><span class="sxs-lookup"><span data-stu-id="e28b4-165">Compute optimized</span></span>](sizes-compute.md) | <span data-ttu-id="e28b4-166">Série F</span><span class="sxs-lookup"><span data-stu-id="e28b4-166">F series</span></span> | <span data-ttu-id="e28b4-167">32</span><span class="sxs-lookup"><span data-stu-id="e28b4-167">32</span></span> |
| [<span data-ttu-id="e28b4-168">Com otimização de memória</span><span class="sxs-lookup"><span data-stu-id="e28b4-168">Memory optimized</span></span>](../virtual-machines-windows-sizes-memory.md) | <span data-ttu-id="e28b4-169">Série de D e G</span><span class="sxs-lookup"><span data-stu-id="e28b4-169">D and G series</span></span> | <span data-ttu-id="e28b4-170">64</span><span class="sxs-lookup"><span data-stu-id="e28b4-170">64</span></span> |
| [<span data-ttu-id="e28b4-171">Com otimização de armazenamento</span><span class="sxs-lookup"><span data-stu-id="e28b4-171">Storage optimized</span></span>](../virtual-machines-windows-sizes-storage.md) | <span data-ttu-id="e28b4-172">Série de L</span><span class="sxs-lookup"><span data-stu-id="e28b4-172">L series</span></span> | <span data-ttu-id="e28b4-173">64</span><span class="sxs-lookup"><span data-stu-id="e28b4-173">64</span></span> |
| [<span data-ttu-id="e28b4-174">GPU</span><span class="sxs-lookup"><span data-stu-id="e28b4-174">GPU</span></span>](sizes-gpu.md) | <span data-ttu-id="e28b4-175">Série N</span><span class="sxs-lookup"><span data-stu-id="e28b4-175">N series</span></span> | <span data-ttu-id="e28b4-176">48</span><span class="sxs-lookup"><span data-stu-id="e28b4-176">48</span></span> |
| [<span data-ttu-id="e28b4-177">Elevado desempenho</span><span class="sxs-lookup"><span data-stu-id="e28b4-177">High performance</span></span>](sizes-hpc.md) | <span data-ttu-id="e28b4-178">A e a série de H</span><span class="sxs-lookup"><span data-stu-id="e28b4-178">A and H series</span></span> | <span data-ttu-id="e28b4-179">32</span><span class="sxs-lookup"><span data-stu-id="e28b4-179">32</span></span> |

## <a name="vm-disk-types"></a><span data-ttu-id="e28b4-180">Tipos de disco da VM</span><span class="sxs-lookup"><span data-stu-id="e28b4-180">VM disk types</span></span>

<span data-ttu-id="e28b4-181">O Azure oferece dois tipos de disco.</span><span class="sxs-lookup"><span data-stu-id="e28b4-181">Azure provides two types of disk.</span></span>

### <a name="standard-disk"></a><span data-ttu-id="e28b4-182">Disco Standard</span><span class="sxs-lookup"><span data-stu-id="e28b4-182">Standard disk</span></span>

<span data-ttu-id="e28b4-183">O Armazenamento Standard está protegido por HDDs e fornece armazenamento económico, mantendo o desempenho.</span><span class="sxs-lookup"><span data-stu-id="e28b4-183">Standard Storage is backed by HDDs, and delivers cost-effective storage while still being performant.</span></span> <span data-ttu-id="e28b4-184">Discos padrão são ideais para um dev económica e teste de carga de trabalho.</span><span class="sxs-lookup"><span data-stu-id="e28b4-184">Standard disks are ideal for a cost effective dev and test workload.</span></span>

### <a name="premium-disk"></a><span data-ttu-id="e28b4-185">Disco Premium</span><span class="sxs-lookup"><span data-stu-id="e28b4-185">Premium disk</span></span>

<span data-ttu-id="e28b4-186">Os discos Premium são apoiados por disco de elevado desempenho, baixa latência baseadas em SSD.</span><span class="sxs-lookup"><span data-stu-id="e28b4-186">Premium disks are backed by SSD-based high-performance, low-latency disk.</span></span> <span data-ttu-id="e28b4-187">Perfeita para as VMs com a carga de trabalho de produção.</span><span class="sxs-lookup"><span data-stu-id="e28b4-187">Perfect for VMs running production workload.</span></span> <span data-ttu-id="e28b4-188">Armazenamento Premium suporta-série DS, série DSv2-série, série GS e série FS VMs.</span><span class="sxs-lookup"><span data-stu-id="e28b4-188">Premium Storage supports DS-series, DSv2-series, GS-series, and FS-series VMs.</span></span> <span data-ttu-id="e28b4-189">Os discos Premium são fornecidos em três tipos (P10, P20, P30), o tamanho do disco de Olá Olá determina o tipo de disco Olá.</span><span class="sxs-lookup"><span data-stu-id="e28b4-189">Premium disks come in three types (P10, P20, P30), hello size of hello disk determines hello disk type.</span></span> <span data-ttu-id="e28b4-190">Quando selecionar, um valor de Olá de tamanho de disco é arredondado toohello tipo do próximo.</span><span class="sxs-lookup"><span data-stu-id="e28b4-190">When selecting, a disk size hello value is rounded up toohello next type.</span></span> <span data-ttu-id="e28b4-191">Por exemplo, se o tamanho do disco de Olá for inferior a 128 GB, o tipo de disco Olá é P10.</span><span class="sxs-lookup"><span data-stu-id="e28b4-191">For example, if hello disk size is less than 128 GB, hello disk type is P10.</span></span> <span data-ttu-id="e28b4-192">Se o tamanho do disco Olá entre 129 GB e 512 GB, o tamanho de Olá é um P20.</span><span class="sxs-lookup"><span data-stu-id="e28b4-192">If hello disk size is between 129 GB and 512 GB, hello size is a P20.</span></span> <span data-ttu-id="e28b4-193">Nada mais 512 GB, o tamanho de Olá é um P30.</span><span class="sxs-lookup"><span data-stu-id="e28b4-193">Anything over 512 GB, hello size is a P30.</span></span>

### <a name="premium-disk-performance"></a><span data-ttu-id="e28b4-194">Desempenho do disco Premium</span><span class="sxs-lookup"><span data-stu-id="e28b4-194">Premium disk performance</span></span>

|<span data-ttu-id="e28b4-195">Tipo de disco de armazenamento Premium</span><span class="sxs-lookup"><span data-stu-id="e28b4-195">Premium storage disk type</span></span> | <span data-ttu-id="e28b4-196">P10</span><span class="sxs-lookup"><span data-stu-id="e28b4-196">P10</span></span> | <span data-ttu-id="e28b4-197">P20</span><span class="sxs-lookup"><span data-stu-id="e28b4-197">P20</span></span> | <span data-ttu-id="e28b4-198">P30</span><span class="sxs-lookup"><span data-stu-id="e28b4-198">P30</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="e28b4-199">Tamanho do disco (arredondar)</span><span class="sxs-lookup"><span data-stu-id="e28b4-199">Disk size (round up)</span></span> | <span data-ttu-id="e28b4-200">128 GB</span><span class="sxs-lookup"><span data-stu-id="e28b4-200">128 GB</span></span> | <span data-ttu-id="e28b4-201">512 GB</span><span class="sxs-lookup"><span data-stu-id="e28b4-201">512 GB</span></span> | <span data-ttu-id="e28b4-202">1.024 GB (1 TB)</span><span class="sxs-lookup"><span data-stu-id="e28b4-202">1,024 GB (1 TB)</span></span> |
| <span data-ttu-id="e28b4-203">IOPs Máx por disco</span><span class="sxs-lookup"><span data-stu-id="e28b4-203">Max IOPS per disk</span></span> | <span data-ttu-id="e28b4-204">500</span><span class="sxs-lookup"><span data-stu-id="e28b4-204">500</span></span> | <span data-ttu-id="e28b4-205">2,300</span><span class="sxs-lookup"><span data-stu-id="e28b4-205">2,300</span></span> | <span data-ttu-id="e28b4-206">5,000</span><span class="sxs-lookup"><span data-stu-id="e28b4-206">5,000</span></span> |
<span data-ttu-id="e28b4-207">Débito por disco</span><span class="sxs-lookup"><span data-stu-id="e28b4-207">Throughput per disk</span></span> | <span data-ttu-id="e28b4-208">100 MB/s</span><span class="sxs-lookup"><span data-stu-id="e28b4-208">100 MB/s</span></span> | <span data-ttu-id="e28b4-209">150 MB/s</span><span class="sxs-lookup"><span data-stu-id="e28b4-209">150 MB/s</span></span> | <span data-ttu-id="e28b4-210">200 MB/s</span><span class="sxs-lookup"><span data-stu-id="e28b4-210">200 MB/s</span></span> |

<span data-ttu-id="e28b4-211">Enquanto Olá acima tabela identifica os IOPS máximo por disco, um nível mais elevado de desempenho pode ser alcançado ao striping vários discos de dados.</span><span class="sxs-lookup"><span data-stu-id="e28b4-211">While hello above table identifies max IOPS per disk, a higher level of performance can be achieved by striping multiple data disks.</span></span> <span data-ttu-id="e28b4-212">Por exemplo, uma VM Standard_GS5 pode alcançar um máximo de 80.000 IOPS.</span><span class="sxs-lookup"><span data-stu-id="e28b4-212">For instance, a Standard_GS5 VM can achieve a maximum of 80,000 IOPS.</span></span> <span data-ttu-id="e28b4-213">Para obter informações detalhadas sobre o IOPS máximo por VM, consulte [tamanhos de VM com Linux](sizes.md).</span><span class="sxs-lookup"><span data-stu-id="e28b4-213">For detailed information on max IOPS per VM, see [Linux VM sizes](sizes.md).</span></span>

## <a name="create-and-attach-disks"></a><span data-ttu-id="e28b4-214">Criar e anexar discos</span><span class="sxs-lookup"><span data-stu-id="e28b4-214">Create and attach disks</span></span>

<span data-ttu-id="e28b4-215">Os discos de dados podem ser criados e ligados ao tempo de criação de VM ou tooan existente VM.</span><span class="sxs-lookup"><span data-stu-id="e28b4-215">Data disks can be created and attached at VM creation time or tooan existing VM.</span></span>

### <a name="attach-disk-at-vm-creation"></a><span data-ttu-id="e28b4-216">Anexar o disco durante a criação de VM</span><span class="sxs-lookup"><span data-stu-id="e28b4-216">Attach disk at VM creation</span></span>

<span data-ttu-id="e28b4-217">Criar um grupo de recursos com Olá [criar grupo az](https://docs.microsoft.com/cli/azure/group#create) comando.</span><span class="sxs-lookup"><span data-stu-id="e28b4-217">Create a resource group with hello [az group create](https://docs.microsoft.com/cli/azure/group#create) command.</span></span> 

```azurecli-interactive 
az group create --name myResourceGroupDisk --location eastus
```

<span data-ttu-id="e28b4-218">Criar uma VM utilizando Olá [az vm criar]( /cli/azure/vm#create) comando.</span><span class="sxs-lookup"><span data-stu-id="e28b4-218">Create a VM using hello [az vm create]( /cli/azure/vm#create) command.</span></span> <span data-ttu-id="e28b4-219">Olá `--datadisk-sizes-gb` argumento é utilizado toospecify que um disco adicional deve ser criado e ligados a máquina virtual de toohello.</span><span class="sxs-lookup"><span data-stu-id="e28b4-219">hello `--datadisk-sizes-gb` argument is used toospecify that an additional disk should be created and attached toohello virtual machine.</span></span> <span data-ttu-id="e28b4-220">toocreate e anexar mais de um disco, utilize uma lista delimitada por espaços de valores de tamanho de disco.</span><span class="sxs-lookup"><span data-stu-id="e28b4-220">toocreate and attach more than one disk, use a space-delimited list of disk size values.</span></span> <span data-ttu-id="e28b4-221">No seguinte exemplo de Olá, é criada uma VM com discos de dados de dois, ambos os 128 GB.</span><span class="sxs-lookup"><span data-stu-id="e28b4-221">In hello following example, a VM is created with two data disks, both 128 GB.</span></span> <span data-ttu-id="e28b4-222">Porque os tamanhos de disco Olá 128 GB, estes discos são configurados como P10s, que fornecem IOPS máximo de 500 por disco.</span><span class="sxs-lookup"><span data-stu-id="e28b4-222">Because hello disk sizes are 128 GB, these disks are both configured as P10s, which provide maximum 500 IOPS per disk.</span></span>

```azurecli-interactive 
az vm create \
  --resource-group myResourceGroupDisk \
  --name myVM \
  --image UbuntuLTS \
  --size Standard_DS2_v2 \
  --data-disk-sizes-gb 128 128 \
  --generate-ssh-keys
```

### <a name="attach-disk-tooexisting-vm"></a><span data-ttu-id="e28b4-223">Anexar o disco tooexisting VM</span><span class="sxs-lookup"><span data-stu-id="e28b4-223">Attach disk tooexisting VM</span></span>

<span data-ttu-id="e28b4-224">toocreate e anexar uma novo disco tooan máquina virtual existente, utilize Olá [anexar o disco da vm az](/cli/azure/vm/disk#attach) comando.</span><span class="sxs-lookup"><span data-stu-id="e28b4-224">toocreate and attach a new disk tooan existing virtual machine, use hello [az vm disk attach](/cli/azure/vm/disk#attach) command.</span></span> <span data-ttu-id="e28b4-225">Olá exemplo seguinte cria um disco premium, 128 gigabytes de tamanho e anexa-toohello que VM criada no último passo de Olá.</span><span class="sxs-lookup"><span data-stu-id="e28b4-225">hello following example creates a premium disk, 128 gigabytes in size, and attaches it toohello VM created in hello last step.</span></span>

```azurecli-interactive 
az vm disk attach --vm-name myVM --resource-group myResourceGroupDisk --disk myDataDisk --size-gb 128 --sku Premium_LRS --new 
```

## <a name="prepare-data-disks"></a><span data-ttu-id="e28b4-226">Preparar os discos de dados</span><span class="sxs-lookup"><span data-stu-id="e28b4-226">Prepare data disks</span></span>

<span data-ttu-id="e28b4-227">Depois de um disco foi anexado toohello máquina, sistema de operativo Olá tem toobe configurado toouse Olá disco.</span><span class="sxs-lookup"><span data-stu-id="e28b4-227">Once a disk has been attached toohello virtual machine, hello operating system needs toobe configured toouse hello disk.</span></span> <span data-ttu-id="e28b4-228">Olá seguinte exemplo mostra como toomanually configurar um disco.</span><span class="sxs-lookup"><span data-stu-id="e28b4-228">hello following example shows how toomanually configure a disk.</span></span> <span data-ttu-id="e28b4-229">Este processo também pode ser automatizado utilizando nuvem-init, que é abordada um [tutorial posterior](./tutorial-automate-vm-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="e28b4-229">This process can also be automated using cloud-init, which is covered in a [later tutorial](./tutorial-automate-vm-deployment.md).</span></span>

### <a name="manual-configuration"></a><span data-ttu-id="e28b4-230">Configuração manual</span><span class="sxs-lookup"><span data-stu-id="e28b4-230">Manual configuration</span></span>

<span data-ttu-id="e28b4-231">Crie uma ligação SSH com a máquina virtual de Olá.</span><span class="sxs-lookup"><span data-stu-id="e28b4-231">Create an SSH connection with hello virtual machine.</span></span> <span data-ttu-id="e28b4-232">Substitua os endereços IP do exemplo Olá Olá IP público de máquina virtual de Olá.</span><span class="sxs-lookup"><span data-stu-id="e28b4-232">Replace hello example IP address with hello public IP of hello virtual machine.</span></span>

```azurecli-interactive 
ssh 52.174.34.95
```

<span data-ttu-id="e28b4-233">Criar partições do disco Olá com `fdisk`.</span><span class="sxs-lookup"><span data-stu-id="e28b4-233">Partition hello disk with `fdisk`.</span></span>

```bash
(echo n; echo p; echo 1; echo ; echo ; echo w) | sudo fdisk /dev/sdc
```

<span data-ttu-id="e28b4-234">Escrever uma partição de toohello do sistema de ficheiros utilizando Olá `mkfs` comando.</span><span class="sxs-lookup"><span data-stu-id="e28b4-234">Write a file system toohello partition by using hello `mkfs` command.</span></span>

```bash
sudo mkfs -t ext4 /dev/sdc1
```

<span data-ttu-id="e28b4-235">Monte o disco novo Olá para que seja acessível no sistema de operativo Olá.</span><span class="sxs-lookup"><span data-stu-id="e28b4-235">Mount hello new disk so that it is accessible in hello operating system.</span></span>

```bash
sudo mkdir /datadrive && sudo mount /dev/sdc1 /datadrive
```

<span data-ttu-id="e28b4-236">disco Olá agora pode ser acedido através de Olá *datadrive* pontodemontagem, que pode ser verificada executando Olá `df -h` comando.</span><span class="sxs-lookup"><span data-stu-id="e28b4-236">hello disk can now be accessed through hello *datadrive* mountpoint, which can be verified by running hello `df -h` command.</span></span> 

```bash
df -h
```

<span data-ttu-id="e28b4-237">saída de Olá mostra unidade novo Olá montada em */datadrive*.</span><span class="sxs-lookup"><span data-stu-id="e28b4-237">hello output shows hello new drive mounted on */datadrive*.</span></span>

```bash
Filesystem      Size  Used Avail Use% Mounted on
/dev/sda1        30G  1.4G   28G   5% /
/dev/sdb1       6.8G   16M  6.4G   1% /mnt
/dev/sdc1        50G   52M   47G   1% /datadrive
```

<span data-ttu-id="e28b4-238">tooensure Olá unidade é remontadas da após um reinício, tem de ser adicionado toohello *etc/fstab* ficheiro.</span><span class="sxs-lookup"><span data-stu-id="e28b4-238">tooensure that hello drive is remounted after a reboot, it must be added toohello */etc/fstab* file.</span></span> <span data-ttu-id="e28b4-239">toodo por isso, obter Olá UUID de disco Olá com Olá `blkid` utilitário.</span><span class="sxs-lookup"><span data-stu-id="e28b4-239">toodo so, get hello UUID of hello disk with hello `blkid` utility.</span></span>

```bash
sudo -i blkid
```

<span data-ttu-id="e28b4-240">saída de Olá apresenta Olá UUID da unidade de Olá, `/dev/sdc1` neste caso.</span><span class="sxs-lookup"><span data-stu-id="e28b4-240">hello output displays hello UUID of hello drive, `/dev/sdc1` in this case.</span></span>

```bash
/dev/sdc1: UUID="33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e" TYPE="ext4"
```

<span data-ttu-id="e28b4-241">Adicionar uma linha de toohello semelhante seguir toohello *etc/fstab* ficheiro.</span><span class="sxs-lookup"><span data-stu-id="e28b4-241">Add a line similar toohello following toohello */etc/fstab* file.</span></span> <span data-ttu-id="e28b4-242">Também em atenção que escrever barreiras as eficazes pode ser desativada através de *barreira = 0*, esta configuração pode melhorar o desempenho de disco.</span><span class="sxs-lookup"><span data-stu-id="e28b4-242">Also note that write barriers can be disabled using *barrier=0*, this configuration can improve disk performance.</span></span> 

```bash
UUID=33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive  ext4    defaults,nofail,barrier=0   1  2
```

<span data-ttu-id="e28b4-243">Agora que hello disco tiver sido configurado, feche a sessão SSH Olá.</span><span class="sxs-lookup"><span data-stu-id="e28b4-243">Now that hello disk has been configured, close hello SSH session.</span></span>

```bash
exit
```

## <a name="resize-vm-disk"></a><span data-ttu-id="e28b4-244">Redimensionar disco da VM</span><span class="sxs-lookup"><span data-stu-id="e28b4-244">Resize VM disk</span></span>

<span data-ttu-id="e28b4-245">Assim que tiver sido implementada uma VM, disco de sistema operativo Olá ou qualquer discos de dados anexados podem ser aumentados de tamanho.</span><span class="sxs-lookup"><span data-stu-id="e28b4-245">Once a VM has been deployed, hello operating system disk or any attached data disks can be increased in size.</span></span> <span data-ttu-id="e28b4-246">Aumentar o tamanho de Olá de um disco é vantajoso quando necessitar de mais espaço de armazenamento ou de um nível mais elevado de desempenho (P10 P20, P30).</span><span class="sxs-lookup"><span data-stu-id="e28b4-246">Increasing hello size of a disk is beneficial when needing more storage space or a higher level of performance (P10, P20, P30).</span></span> <span data-ttu-id="e28b4-247">Tenha em atenção de que não podem ser diminuídos discos de tamanho.</span><span class="sxs-lookup"><span data-stu-id="e28b4-247">Note, disks cannot be decreased in size.</span></span>

<span data-ttu-id="e28b4-248">Antes de aumentar o tamanho do disco, Olá Id ou nome do disco de Olá é necessária.</span><span class="sxs-lookup"><span data-stu-id="e28b4-248">Before increasing disk size, hello Id or name of hello disk is needed.</span></span> <span data-ttu-id="e28b4-249">Olá utilize [lista de discos az](/cli/azure/vm/disk#list) comando tooreturn todos os discos num grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="e28b4-249">Use hello [az disk list](/cli/azure/vm/disk#list) command tooreturn all disks in a resource group.</span></span> <span data-ttu-id="e28b4-250">Tome nota do nome do disco Olá que gostaria de tooresize.</span><span class="sxs-lookup"><span data-stu-id="e28b4-250">Take note of hello disk name that you would like tooresize.</span></span>

```azurecli-interactive 
az disk list -g myResourceGroupDisk --query '[*].{Name:name,Gb:diskSizeGb,Tier:accountType}' --output table
```

<span data-ttu-id="e28b4-251">Olá VM também tem de ser desalocada.</span><span class="sxs-lookup"><span data-stu-id="e28b4-251">hello VM must also be deallocated.</span></span> <span data-ttu-id="e28b4-252">Olá utilize [az vm desalocar]( /cli/azure/vm#deallocate) toostop de comandos e desalocar Olá VM.</span><span class="sxs-lookup"><span data-stu-id="e28b4-252">Use hello [az vm deallocate]( /cli/azure/vm#deallocate) command toostop and deallocate hello VM.</span></span>

```azurecli-interactive 
az vm deallocate --resource-group myResourceGroupDisk --name myVM
```

<span data-ttu-id="e28b4-253">Olá utilize [atualização de disco az](/cli/azure/vm/disk#update) disco do comando tooresize Olá.</span><span class="sxs-lookup"><span data-stu-id="e28b4-253">Use hello [az disk update](/cli/azure/vm/disk#update) command tooresize hello disk.</span></span> <span data-ttu-id="e28b4-254">Neste exemplo redimensiona um disco chamado *myDataDisk* too1 terabyte.</span><span class="sxs-lookup"><span data-stu-id="e28b4-254">This example resizes a disk named *myDataDisk* too1 terabyte.</span></span>

```azurecli-interactive 
az disk update --name myDataDisk --resource-group myResourceGroupDisk --size-gb 1023
```

<span data-ttu-id="e28b4-255">Depois de concluída a operação de redimensionamento Olá, inicie Olá VM.</span><span class="sxs-lookup"><span data-stu-id="e28b4-255">Once hello resize operation has completed, start hello VM.</span></span>

```azurecli-interactive 
az vm start --resource-group myResourceGroupDisk --name myVM
```

<span data-ttu-id="e28b4-256">Se tiver redimensionado Olá disco do sistema de operativo, partição Olá é automaticamente expandido.</span><span class="sxs-lookup"><span data-stu-id="e28b4-256">If you’ve resized hello operating system disk, hello partition is automatically be expanded.</span></span> <span data-ttu-id="e28b4-257">Se tiver redimensionado um disco de dados, quaisquer partições atuais tem toobe expandido no sistema de operativo Olá VMs.</span><span class="sxs-lookup"><span data-stu-id="e28b4-257">If you have resized a data disk, any current partitions need toobe expanded in hello VMs operating system.</span></span>

## <a name="snapshot-azure-disks"></a><span data-ttu-id="e28b4-258">Instantâneos de discos do Azure</span><span class="sxs-lookup"><span data-stu-id="e28b4-258">Snapshot Azure disks</span></span>

<span data-ttu-id="e28b4-259">Criar um instantâneo de disco cria uma leitura cópia apenas, o ponto no tempo de disco Olá.</span><span class="sxs-lookup"><span data-stu-id="e28b4-259">Taking a disk snapshot creates a read only, point-in-time copy of hello disk.</span></span> <span data-ttu-id="e28b4-260">Instantâneos VM do Azure são úteis para guardar rapidamente o estado de Olá de uma VM antes de efetuar alterações de configuração.</span><span class="sxs-lookup"><span data-stu-id="e28b4-260">Azure VM snapshots are useful for quickly saving hello state of a VM before making configuration changes.</span></span> <span data-ttu-id="e28b4-261">O evento Olá hello alterações de configuração de provar toobe indesejado, estado de VM pode ser restaurado utilizando instantâneos de Olá.</span><span class="sxs-lookup"><span data-stu-id="e28b4-261">In hello event hello configuration changes prove toobe undesired, VM state can be restored using hello snapshot.</span></span> <span data-ttu-id="e28b4-262">Quando uma VM tem mais de um disco, é obtido um instantâneo de cada disco independentemente Olá outras pessoas.</span><span class="sxs-lookup"><span data-stu-id="e28b4-262">When a VM has more than one disk, a snapshot is taken of each disk independently of hello others.</span></span> <span data-ttu-id="e28b4-263">Para fazer cópias de segurança da aplicação, considere parar Olá VM antes de tirar instantâneos de disco.</span><span class="sxs-lookup"><span data-stu-id="e28b4-263">For taking application consistent backups, consider stopping hello VM before taking disk snapshots.</span></span> <span data-ttu-id="e28b4-264">Em alternativa, utilize Olá [serviço de cópia de segurança do Azure](/azure/backup/), que permite tooperform automatizada cópias de segurança ao hello VM está em execução.</span><span class="sxs-lookup"><span data-stu-id="e28b4-264">Alternatively, use hello [Azure Backup service](/azure/backup/), which enables you tooperform automated backups while hello VM is running.</span></span>

### <a name="create-snapshot"></a><span data-ttu-id="e28b4-265">Criar instantâneo</span><span class="sxs-lookup"><span data-stu-id="e28b4-265">Create snapshot</span></span>

<span data-ttu-id="e28b4-266">Antes de criar um instantâneo de disco da máquina virtual, hello Id ou nome do disco de Olá é necessária.</span><span class="sxs-lookup"><span data-stu-id="e28b4-266">Before creating a virtual machine disk snapshot, hello Id or name of hello disk is needed.</span></span> <span data-ttu-id="e28b4-267">Olá utilize [mostrar de vm az](https://docs.microsoft.com/en-us/cli/azure/vm#show) id de disco do comando tooreturn Olá. Neste exemplo, um id de disco Olá é armazenado numa variável, para que possa ser utilizado num passo posterior.</span><span class="sxs-lookup"><span data-stu-id="e28b4-267">Use hello [az vm show](https://docs.microsoft.com/en-us/cli/azure/vm#show) command tooreturn hello disk id. In this example, hello disk id is stored in a variable so that it can be used in a later step.</span></span>

```azurecli-interactive 
osdiskid=$(az vm show -g myResourceGroupDisk -n myVM --query "storageProfile.osDisk.managedDisk.id" -o tsv)
```

<span data-ttu-id="e28b4-268">Agora que tem o id de Olá do disco da máquina virtual Olá, hello comando seguinte cria um instantâneo do disco de Olá.</span><span class="sxs-lookup"><span data-stu-id="e28b4-268">Now that you have hello id of hello virtual machine disk, hello following command creates a snapshot of hello disk.</span></span>

```azurcli
az snapshot create -g myResourceGroupDisk --source "$osdiskid" --name osDisk-backup
```

### <a name="create-disk-from-snapshot"></a><span data-ttu-id="e28b4-269">Criar disco de instantâneo</span><span class="sxs-lookup"><span data-stu-id="e28b4-269">Create disk from snapshot</span></span>

<span data-ttu-id="e28b4-270">Este instantâneo, em seguida, pode ser convertido para um disco, o que pode ser utilizado toorecreate Olá máquina.</span><span class="sxs-lookup"><span data-stu-id="e28b4-270">This snapshot can then be converted into a disk, which can be used toorecreate hello virtual machine.</span></span>

```azurecli-interactive 
az disk create --resource-group myResourceGroupDisk --name mySnapshotDisk --source osDisk-backup
```

### <a name="restore-virtual-machine-from-snapshot"></a><span data-ttu-id="e28b4-271">Restauro do instantâneo de máquina virtual</span><span class="sxs-lookup"><span data-stu-id="e28b4-271">Restore virtual machine from snapshot</span></span>

<span data-ttu-id="e28b4-272">recuperação da máquina virtual toodemonstrate, eliminar Olá existente a máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="e28b4-272">toodemonstrate virtual machine recovery, delete hello existing virtual machine.</span></span> 

```azurecli-interactive 
az vm delete --resource-group myResourceGroupDisk --name myVM
```

<span data-ttu-id="e28b4-273">Crie uma nova máquina virtual a partir de discos de instantâneo Olá.</span><span class="sxs-lookup"><span data-stu-id="e28b4-273">Create a new virtual machine from hello snapshot disk.</span></span>

```azurecli-interactive 
az vm create --resource-group myResourceGroupDisk --name myVM --attach-os-disk mySnapshotDisk --os-type linux
```

### <a name="reattach-data-disk"></a><span data-ttu-id="e28b4-274">Reattach disco de dados</span><span class="sxs-lookup"><span data-stu-id="e28b4-274">Reattach data disk</span></span>

<span data-ttu-id="e28b4-275">Todos os discos de dados tem de máquina de virtual toohello toobe novamente ligado.</span><span class="sxs-lookup"><span data-stu-id="e28b4-275">All data disks need toobe reattached toohello virtual machine.</span></span>

<span data-ttu-id="e28b4-276">Localizar primeiro o nome de disco de dados de Olá utilizando Olá [lista de discos az](https://docs.microsoft.com/cli/azure/disk#list) comando.</span><span class="sxs-lookup"><span data-stu-id="e28b4-276">First find hello data disk name using hello [az disk list](https://docs.microsoft.com/cli/azure/disk#list) command.</span></span> <span data-ttu-id="e28b4-277">Neste exemplo locais Olá nome do disco de Olá numa variável designada *datadisk*, que é utilizada no passo seguinte Olá.</span><span class="sxs-lookup"><span data-stu-id="e28b4-277">This example places hello name of hello disk in a variable named *datadisk*, which is used in hello next step.</span></span>

```azurecli-interactive 
datadisk=$(az disk list -g myResourceGroupDisk --query "[?contains(name,'myVM')].[name]" -o tsv)
```

<span data-ttu-id="e28b4-278">Olá utilize [anexar o disco da vm az](https://docs.microsoft.com/cli/azure/vm/disk#attach) disco do comando tooattach Olá.</span><span class="sxs-lookup"><span data-stu-id="e28b4-278">Use hello [az vm disk attach](https://docs.microsoft.com/cli/azure/vm/disk#attach) command tooattach hello disk.</span></span>

```azurecli-interactive 
az vm disk attach –g myResourceGroupDisk –-vm-name myVM –-disk $datadisk
```

## <a name="next-steps"></a><span data-ttu-id="e28b4-279">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="e28b4-279">Next steps</span></span>

<span data-ttu-id="e28b4-280">Neste tutorial, aprendeu sobre os tópicos de discos VM, tais como:</span><span class="sxs-lookup"><span data-stu-id="e28b4-280">In this tutorial, you learned about VM disks topics such as:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="e28b4-281">Discos de SO e discos temporários</span><span class="sxs-lookup"><span data-stu-id="e28b4-281">OS disks and temporary disks</span></span>
> * <span data-ttu-id="e28b4-282">discos de dados</span><span class="sxs-lookup"><span data-stu-id="e28b4-282">Data disks</span></span>
> * <span data-ttu-id="e28b4-283">Standard e discos Premium</span><span class="sxs-lookup"><span data-stu-id="e28b4-283">Standard and Premium disks</span></span>
> * <span data-ttu-id="e28b4-284">Desempenho de disco</span><span class="sxs-lookup"><span data-stu-id="e28b4-284">Disk performance</span></span>
> * <span data-ttu-id="e28b4-285">Anexar e preparar os discos de dados</span><span class="sxs-lookup"><span data-stu-id="e28b4-285">Attaching and preparing data disks</span></span>
> * <span data-ttu-id="e28b4-286">O redimensionamento de discos</span><span class="sxs-lookup"><span data-stu-id="e28b4-286">Resizing disks</span></span>
> * <span data-ttu-id="e28b4-287">Instantâneos de disco</span><span class="sxs-lookup"><span data-stu-id="e28b4-287">Disk snapshots</span></span>

<span data-ttu-id="e28b4-288">Produzir toohello seguinte toolearn tutorial sobre automatizar a configuração de VM.</span><span class="sxs-lookup"><span data-stu-id="e28b4-288">Advance toohello next tutorial toolearn about automating VM configuration.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="e28b4-289">Automatizar a configuração da VM</span><span class="sxs-lookup"><span data-stu-id="e28b4-289">Automate VM configuration</span></span>](./tutorial-automate-vm-deployment.md)
