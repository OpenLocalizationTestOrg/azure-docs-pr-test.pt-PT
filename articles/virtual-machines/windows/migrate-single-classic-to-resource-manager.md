---
title: "aaaMigrate um tooan VMS clássicas VM de disco gerido ARM | Microsoft Docs"
description: "Migrar uma única VM do Azure de implementação clássica Olá tooManaged discos no modelo de implementação do Resource Manager Olá de modelo."
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
ms.date: 06/15/2017
ms.author: cynthn
ms.openlocfilehash: d8c4b9431f5dd8a071fcbc2ee36581a33f76ba62
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="manually-migrate-a-classic-vm-tooa-new-arm-managed-disk-vm-from-hello-vhd"></a><span data-ttu-id="29b39-103">Migrar manualmente um tooa VMS clássicas novo ARM geridos disco VM a partir do Olá VHD</span><span class="sxs-lookup"><span data-stu-id="29b39-103">Manually migrate a Classic VM tooa new ARM Managed Disk VM from hello VHD</span></span> 


<span data-ttu-id="29b39-104">Esta secção ajuda-toomigrate as suas VMs do Azure existente do modelo de implementação clássica Olá demasiado[discos geridos](managed-disks-overview.md) no modelo de implementação do Resource Manager Olá.</span><span class="sxs-lookup"><span data-stu-id="29b39-104">This section helps you toomigrate your existing Azure VMs from hello classic deployment model too[Managed Disks](managed-disks-overview.md) in hello Resource Manager deployment model.</span></span>


## <a name="plan-for-hello-migration-toomanaged-disks"></a><span data-ttu-id="29b39-105">Planear a migração de Olá tooManaged discos</span><span class="sxs-lookup"><span data-stu-id="29b39-105">Plan for hello migration tooManaged Disks</span></span>

<span data-ttu-id="29b39-106">Esta secção ajuda-o a decisão de melhor Olá toomake em tipos de disco e de VM.</span><span class="sxs-lookup"><span data-stu-id="29b39-106">This section helps you toomake hello best decision on VM and disk types.</span></span>


### <a name="location"></a><span data-ttu-id="29b39-107">Localização</span><span class="sxs-lookup"><span data-stu-id="29b39-107">Location</span></span>

<span data-ttu-id="29b39-108">Escolha uma localização onde discos gerida do Azure estão disponíveis.</span><span class="sxs-lookup"><span data-stu-id="29b39-108">Pick a location where Azure Managed Disks are available.</span></span> <span data-ttu-id="29b39-109">Se estiver a migrar discos geridos de tooPremium, certifique-se também que armazenamento Premium está disponível na região de olá onde estiver a planear toomigrate para.</span><span class="sxs-lookup"><span data-stu-id="29b39-109">If you are migrating tooPremium Managed Disks, also ensure that Premium storage is available in hello region where you are planning toomigrate to.</span></span> <span data-ttu-id="29b39-110">Consulte [byRegion de serviços do Azure](https://azure.microsoft.com/regions/#services) para obter informações atualizadas em localizações disponíveis.</span><span class="sxs-lookup"><span data-stu-id="29b39-110">See [Azure Services byRegion](https://azure.microsoft.com/regions/#services) for up-to-date information on available locations.</span></span>

### <a name="vm-sizes"></a><span data-ttu-id="29b39-111">Tamanhos de VM</span><span class="sxs-lookup"><span data-stu-id="29b39-111">VM sizes</span></span>

<span data-ttu-id="29b39-112">Se estiver a migrar discos geridos de tooPremium, tem de tamanho de Olá tooupdate de Olá VM tooPremium tamanho com capacidade de armazenamento disponível na região de olá onde está localizada a VM.</span><span class="sxs-lookup"><span data-stu-id="29b39-112">If you are migrating tooPremium Managed Disks, you have tooupdate hello size of hello VM tooPremium Storage capable size available in hello region where VM is located.</span></span> <span data-ttu-id="29b39-113">Reveja os tamanhos de VM Olá que são compatíveis com o Premium Storage.</span><span class="sxs-lookup"><span data-stu-id="29b39-113">Review hello VM sizes that are Premium Storage capable.</span></span> <span data-ttu-id="29b39-114">as especificações de tamanho de VM do Azure Olá constam [tamanhos das virtual machines](sizes.md).</span><span class="sxs-lookup"><span data-stu-id="29b39-114">hello Azure VM size specifications are listed in [Sizes for virtual machines](sizes.md).</span></span>
<span data-ttu-id="29b39-115">Reveja as características de desempenho de Olá de máquinas virtuais que funcionam com o Premium Storage e escolha Olá mais adequado tamanho da VM que melhor se adapta às sua carga de trabalho.</span><span class="sxs-lookup"><span data-stu-id="29b39-115">Review hello performance characteristics of virtual machines that work with Premium Storage and choose hello most appropriate VM size that best suits your workload.</span></span> <span data-ttu-id="29b39-116">Certifique-se de que existe largura de banda suficiente disponível no seu tráfego de disco do VM toodrive Olá.</span><span class="sxs-lookup"><span data-stu-id="29b39-116">Make sure that there is sufficient bandwidth available on your VM toodrive hello disk traffic.</span></span>

### <a name="disk-sizes"></a><span data-ttu-id="29b39-117">Tamanhos de disco</span><span class="sxs-lookup"><span data-stu-id="29b39-117">Disk sizes</span></span>

<span data-ttu-id="29b39-118">**Premium discos geridos**</span><span class="sxs-lookup"><span data-stu-id="29b39-118">**Premium Managed Disks**</span></span>

<span data-ttu-id="29b39-119">Existem sete tipos de discos de gerido premium que podem ser utilizados com a VM e cada um tem IOPs específicos e débito limites.</span><span class="sxs-lookup"><span data-stu-id="29b39-119">There are seven types of premium Managed disks that can be used with your VM and each has specific IOPs and throughput limits.</span></span> <span data-ttu-id="29b39-120">Quando escolher Olá tipo de disco Premium para VM com base nas necessidades de Olá da sua aplicação em termos de capacidade, desempenho, escalabilidade e carrega das horas de ponta, considere estes limites.</span><span class="sxs-lookup"><span data-stu-id="29b39-120">Consider these limits when choosing hello Premium disk type for your VM based on hello needs of your application in terms of capacity, performance, scalability, and peak loads.</span></span>

| <span data-ttu-id="29b39-121">Tipo de discos Premium</span><span class="sxs-lookup"><span data-stu-id="29b39-121">Premium Disks Type</span></span>  | <span data-ttu-id="29b39-122">P4</span><span class="sxs-lookup"><span data-stu-id="29b39-122">P4</span></span>    | <span data-ttu-id="29b39-123">P6</span><span class="sxs-lookup"><span data-stu-id="29b39-123">P6</span></span>    | <span data-ttu-id="29b39-124">P10</span><span class="sxs-lookup"><span data-stu-id="29b39-124">P10</span></span>   | <span data-ttu-id="29b39-125">P20</span><span class="sxs-lookup"><span data-stu-id="29b39-125">P20</span></span>   | <span data-ttu-id="29b39-126">P30</span><span class="sxs-lookup"><span data-stu-id="29b39-126">P30</span></span>   | <span data-ttu-id="29b39-127">P40</span><span class="sxs-lookup"><span data-stu-id="29b39-127">P40</span></span>   | <span data-ttu-id="29b39-128">P50</span><span class="sxs-lookup"><span data-stu-id="29b39-128">P50</span></span>   | 
|---------------------|-------|-------|-------|-------|-------|-------|-------|
| <span data-ttu-id="29b39-129">Tamanho do disco</span><span class="sxs-lookup"><span data-stu-id="29b39-129">Disk size</span></span>           | <span data-ttu-id="29b39-130">128 GB</span><span class="sxs-lookup"><span data-stu-id="29b39-130">128 GB</span></span>| <span data-ttu-id="29b39-131">512 GB</span><span class="sxs-lookup"><span data-stu-id="29b39-131">512 GB</span></span>| <span data-ttu-id="29b39-132">128 GB</span><span class="sxs-lookup"><span data-stu-id="29b39-132">128 GB</span></span>| <span data-ttu-id="29b39-133">512 GB</span><span class="sxs-lookup"><span data-stu-id="29b39-133">512 GB</span></span>            | <span data-ttu-id="29b39-134">1024 GB (1 TB)</span><span class="sxs-lookup"><span data-stu-id="29b39-134">1024 GB (1 TB)</span></span>    | <span data-ttu-id="29b39-135">2048 GB (2 TB)</span><span class="sxs-lookup"><span data-stu-id="29b39-135">2048 GB (2 TB)</span></span>    | <span data-ttu-id="29b39-136">4095 GB (4 TB)</span><span class="sxs-lookup"><span data-stu-id="29b39-136">4095 GB (4 TB)</span></span>    | 
| <span data-ttu-id="29b39-137">IOPs por disco</span><span class="sxs-lookup"><span data-stu-id="29b39-137">IOPS per disk</span></span>       | <span data-ttu-id="29b39-138">120</span><span class="sxs-lookup"><span data-stu-id="29b39-138">120</span></span>   | <span data-ttu-id="29b39-139">240</span><span class="sxs-lookup"><span data-stu-id="29b39-139">240</span></span>   | <span data-ttu-id="29b39-140">500</span><span class="sxs-lookup"><span data-stu-id="29b39-140">500</span></span>   | <span data-ttu-id="29b39-141">2300</span><span class="sxs-lookup"><span data-stu-id="29b39-141">2300</span></span>              | <span data-ttu-id="29b39-142">5000</span><span class="sxs-lookup"><span data-stu-id="29b39-142">5000</span></span>              | <span data-ttu-id="29b39-143">7500</span><span class="sxs-lookup"><span data-stu-id="29b39-143">7500</span></span>              | <span data-ttu-id="29b39-144">7500</span><span class="sxs-lookup"><span data-stu-id="29b39-144">7500</span></span>              | 
| <span data-ttu-id="29b39-145">Débito por disco</span><span class="sxs-lookup"><span data-stu-id="29b39-145">Throughput per disk</span></span> | <span data-ttu-id="29b39-146">25 MB por segundo</span><span class="sxs-lookup"><span data-stu-id="29b39-146">25 MB per second</span></span>  | <span data-ttu-id="29b39-147">50 MB por segundo</span><span class="sxs-lookup"><span data-stu-id="29b39-147">50 MB per second</span></span>  | <span data-ttu-id="29b39-148">100 MB por segundo</span><span class="sxs-lookup"><span data-stu-id="29b39-148">100 MB per second</span></span> | <span data-ttu-id="29b39-149">150 MB por segundo</span><span class="sxs-lookup"><span data-stu-id="29b39-149">150 MB per second</span></span> | <span data-ttu-id="29b39-150">200 MB por segundo</span><span class="sxs-lookup"><span data-stu-id="29b39-150">200 MB per second</span></span> | <span data-ttu-id="29b39-151">250 MB por segundo</span><span class="sxs-lookup"><span data-stu-id="29b39-151">250 MB per second</span></span> | <span data-ttu-id="29b39-152">250 MB por segundo</span><span class="sxs-lookup"><span data-stu-id="29b39-152">250 MB per second</span></span> | 

<span data-ttu-id="29b39-153">**Discos geridos padrão**</span><span class="sxs-lookup"><span data-stu-id="29b39-153">**Standard Managed Disks**</span></span>

<span data-ttu-id="29b39-154">Existem sete tipos de discos padrão gerido que podem ser utilizados com a VM.</span><span class="sxs-lookup"><span data-stu-id="29b39-154">There are seven types of Standard Managed disks that can be used with your VM.</span></span> <span data-ttu-id="29b39-155">Cada um deles tem capacidade de diferentes, mas tem o mesmo IOPS e limites de débito.</span><span class="sxs-lookup"><span data-stu-id="29b39-155">Each of them have different capacity but have same IOPS and throughput limits.</span></span> <span data-ttu-id="29b39-156">Escolha o tipo de Olá de gerido padrão discos com base nas necessidades de capacidade de Olá da sua aplicação.</span><span class="sxs-lookup"><span data-stu-id="29b39-156">Choose hello type of Standard Managed disks based on hello capacity needs of your application.</span></span>

| <span data-ttu-id="29b39-157">Tipo de Disco Standard</span><span class="sxs-lookup"><span data-stu-id="29b39-157">Standard Disk Type</span></span>  | <span data-ttu-id="29b39-158">S4</span><span class="sxs-lookup"><span data-stu-id="29b39-158">S4</span></span>               | <span data-ttu-id="29b39-159">S6</span><span class="sxs-lookup"><span data-stu-id="29b39-159">S6</span></span>               | <span data-ttu-id="29b39-160">S10</span><span class="sxs-lookup"><span data-stu-id="29b39-160">S10</span></span>              | <span data-ttu-id="29b39-161">S20</span><span class="sxs-lookup"><span data-stu-id="29b39-161">S20</span></span>              | <span data-ttu-id="29b39-162">S30</span><span class="sxs-lookup"><span data-stu-id="29b39-162">S30</span></span>              | <span data-ttu-id="29b39-163">S40</span><span class="sxs-lookup"><span data-stu-id="29b39-163">S40</span></span>              | <span data-ttu-id="29b39-164">S50</span><span class="sxs-lookup"><span data-stu-id="29b39-164">S50</span></span>              | 
|---------------------|---------------------|---------------------|------------------|------------------|------------------|------------------|------------------| 
| <span data-ttu-id="29b39-165">Tamanho do disco</span><span class="sxs-lookup"><span data-stu-id="29b39-165">Disk size</span></span>           | <span data-ttu-id="29b39-166">30 GB</span><span class="sxs-lookup"><span data-stu-id="29b39-166">30 GB</span></span>            | <span data-ttu-id="29b39-167">64 GB</span><span class="sxs-lookup"><span data-stu-id="29b39-167">64 GB</span></span>            | <span data-ttu-id="29b39-168">128 GB</span><span class="sxs-lookup"><span data-stu-id="29b39-168">128 GB</span></span>           | <span data-ttu-id="29b39-169">512 GB</span><span class="sxs-lookup"><span data-stu-id="29b39-169">512 GB</span></span>           | <span data-ttu-id="29b39-170">1024 GB (1 TB)</span><span class="sxs-lookup"><span data-stu-id="29b39-170">1024 GB (1 TB)</span></span>   | <span data-ttu-id="29b39-171">2048 GB (2TB)</span><span class="sxs-lookup"><span data-stu-id="29b39-171">2048 GB (2TB)</span></span>    | <span data-ttu-id="29b39-172">4095 GB (4 TB)</span><span class="sxs-lookup"><span data-stu-id="29b39-172">4095 GB (4 TB)</span></span>   | 
| <span data-ttu-id="29b39-173">IOPs por disco</span><span class="sxs-lookup"><span data-stu-id="29b39-173">IOPS per disk</span></span>       | <span data-ttu-id="29b39-174">500</span><span class="sxs-lookup"><span data-stu-id="29b39-174">500</span></span>              | <span data-ttu-id="29b39-175">500</span><span class="sxs-lookup"><span data-stu-id="29b39-175">500</span></span>              | <span data-ttu-id="29b39-176">500</span><span class="sxs-lookup"><span data-stu-id="29b39-176">500</span></span>              | <span data-ttu-id="29b39-177">500</span><span class="sxs-lookup"><span data-stu-id="29b39-177">500</span></span>              | <span data-ttu-id="29b39-178">500</span><span class="sxs-lookup"><span data-stu-id="29b39-178">500</span></span>              | <span data-ttu-id="29b39-179">500</span><span class="sxs-lookup"><span data-stu-id="29b39-179">500</span></span>             | <span data-ttu-id="29b39-180">500</span><span class="sxs-lookup"><span data-stu-id="29b39-180">500</span></span>              | 
| <span data-ttu-id="29b39-181">Débito por disco</span><span class="sxs-lookup"><span data-stu-id="29b39-181">Throughput per disk</span></span> | <span data-ttu-id="29b39-182">60 MB por segundo</span><span class="sxs-lookup"><span data-stu-id="29b39-182">60 MB per second</span></span> | <span data-ttu-id="29b39-183">60 MB por segundo</span><span class="sxs-lookup"><span data-stu-id="29b39-183">60 MB per second</span></span> | <span data-ttu-id="29b39-184">60 MB por segundo</span><span class="sxs-lookup"><span data-stu-id="29b39-184">60 MB per second</span></span> | <span data-ttu-id="29b39-185">60 MB por segundo</span><span class="sxs-lookup"><span data-stu-id="29b39-185">60 MB per second</span></span> | <span data-ttu-id="29b39-186">60 MB por segundo</span><span class="sxs-lookup"><span data-stu-id="29b39-186">60 MB per second</span></span> | <span data-ttu-id="29b39-187">60 MB por segundo</span><span class="sxs-lookup"><span data-stu-id="29b39-187">60 MB per second</span></span> | <span data-ttu-id="29b39-188">60 MB por segundo</span><span class="sxs-lookup"><span data-stu-id="29b39-188">60 MB per second</span></span> | 


### <a name="disk-caching-policy"></a><span data-ttu-id="29b39-189">Política de colocação em cache em disco</span><span class="sxs-lookup"><span data-stu-id="29b39-189">Disk caching policy</span></span> 

<span data-ttu-id="29b39-190">**Premium discos geridos**</span><span class="sxs-lookup"><span data-stu-id="29b39-190">**Premium Managed Disks**</span></span>

<span data-ttu-id="29b39-191">Por predefinição, o disco de política de colocação em cache é *só de leitura* para Olá todos os discos de dados Premium, e *leitura e escrita* para disco do sistema operativo Olá Premium ligados toohello VM.</span><span class="sxs-lookup"><span data-stu-id="29b39-191">By default, disk caching policy is *Read-Only* for all hello Premium data disks, and *Read-Write* for hello Premium operating system disk attached toohello VM.</span></span> <span data-ttu-id="29b39-192">Esta definição de configuração é recomendada tooachieve Olá um desempenho ideal para IOs a aplicação.</span><span class="sxs-lookup"><span data-stu-id="29b39-192">This configuration setting is recommended tooachieve hello optimal performance for your application’s IOs.</span></span> <span data-ttu-id="29b39-193">Pesado de escrita ou só de escrita para discos de dados (por exemplo, ficheiros de registo do SQL Server), desative a colocação em cache no disco, de modo a que pode alcançar um melhor desempenho de aplicações.</span><span class="sxs-lookup"><span data-stu-id="29b39-193">For write-heavy or write-only data disks (such as SQL Server log files), disable disk caching so that you can achieve better application performance.</span></span>

### <a name="pricing"></a><span data-ttu-id="29b39-194">Preços</span><span class="sxs-lookup"><span data-stu-id="29b39-194">Pricing</span></span>

<span data-ttu-id="29b39-195">Olá revisão [preços para discos geridos](https://azure.microsoft.com/en-us/pricing/details/managed-disks/).</span><span class="sxs-lookup"><span data-stu-id="29b39-195">Review hello [pricing for Managed Disks](https://azure.microsoft.com/en-us/pricing/details/managed-disks/).</span></span> <span data-ttu-id="29b39-196">Preços dos discos de geridos Premium é a mesmo Olá os discos Premium não gerido.</span><span class="sxs-lookup"><span data-stu-id="29b39-196">Pricing of Premium Managed Disks is same as hello Premium Unmanaged Disks.</span></span> <span data-ttu-id="29b39-197">Mas preços para os discos padrão geridos são diferente de discos padrão de não gerido.</span><span class="sxs-lookup"><span data-stu-id="29b39-197">But pricing for Standard Managed Disks is different than Standard Unmanaged Disks.</span></span>


## <a name="checklist"></a><span data-ttu-id="29b39-198">Lista de verificação</span><span class="sxs-lookup"><span data-stu-id="29b39-198">Checklist</span></span>

1.  <span data-ttu-id="29b39-199">Se estiver a migrar discos geridos de tooPremium, certifique-se de que está disponível na região de Olá que estiver a migrar para.</span><span class="sxs-lookup"><span data-stu-id="29b39-199">If you are migrating tooPremium Managed Disks, make sure it is available in hello region you are migrating to.</span></span>

2.  <span data-ttu-id="29b39-200">Decida Olá novo série de VM que irá utilizar.</span><span class="sxs-lookup"><span data-stu-id="29b39-200">Decide hello new VM series you will be using.</span></span> <span data-ttu-id="29b39-201">Deve ser um com capacidade de armazenamento Premium se estiver a migrar discos geridos de tooPremium.</span><span class="sxs-lookup"><span data-stu-id="29b39-201">It should be a Premium Storage capable if you are migrating tooPremium Managed Disks.</span></span>

3.  <span data-ttu-id="29b39-202">Decida Olá exato tamanho da VM que irá utilizar que estão disponíveis na região de Olá que estiver a migrar.</span><span class="sxs-lookup"><span data-stu-id="29b39-202">Decide hello exact VM size you will use which are available in hello region you are migrating to.</span></span> <span data-ttu-id="29b39-203">Tamanho da VM tem de número de Olá toobe toosupport grandes o suficiente de discos de dados que tiver.</span><span class="sxs-lookup"><span data-stu-id="29b39-203">VM size needs toobe large enough toosupport hello number of data disks you have.</span></span> <span data-ttu-id="29b39-204">Por exemplo, se tiver quatro discos de dados, Olá VM tem de ter dois ou mais núcleos.</span><span class="sxs-lookup"><span data-stu-id="29b39-204">For example, if you have four data disks, hello VM must have two or more cores.</span></span> <span data-ttu-id="29b39-205">Além disso, considere o processamento de energia, memória e as necessidades de largura de banda de rede.</span><span class="sxs-lookup"><span data-stu-id="29b39-205">Also, consider processing power, memory and network bandwidth needs.</span></span>

4.  <span data-ttu-id="29b39-206">Ter Olá VM detalhes atuais à mão, incluindo Olá lista de discos e blobs VHD correspondentes.</span><span class="sxs-lookup"><span data-stu-id="29b39-206">Have hello current VM details handy, including hello list of disks and corresponding VHD blobs.</span></span>

<span data-ttu-id="29b39-207">Prepare a sua aplicação para o período de indisponibilidade.</span><span class="sxs-lookup"><span data-stu-id="29b39-207">Prepare your application for downtime.</span></span> <span data-ttu-id="29b39-208">uma migração limpa toodo, tiver toostop todo o processamento Olá no sistema atual Olá.</span><span class="sxs-lookup"><span data-stu-id="29b39-208">toodo a clean migration, you have toostop all hello processing in hello current system.</span></span> <span data-ttu-id="29b39-209">Só então, pode obtê-lo tooconsistent Estado, o que pode migrar toohello nova plataforma.</span><span class="sxs-lookup"><span data-stu-id="29b39-209">Only then you can get it tooconsistent state which you can migrate toohello new platform.</span></span> <span data-ttu-id="29b39-210">Duração do período de indisponibilidade depende da quantidade de Olá de dados no Olá toomigrate de discos.</span><span class="sxs-lookup"><span data-stu-id="29b39-210">Downtime duration depends on hello amount of data in hello disks toomigrate.</span></span>


## <a name="migrate-hello-vm"></a><span data-ttu-id="29b39-211">Migrar Olá VM</span><span class="sxs-lookup"><span data-stu-id="29b39-211">Migrate hello VM</span></span>

<span data-ttu-id="29b39-212">Prepare a sua aplicação para o período de indisponibilidade.</span><span class="sxs-lookup"><span data-stu-id="29b39-212">Prepare your application for downtime.</span></span> <span data-ttu-id="29b39-213">uma migração limpa toodo, tiver toostop todo o processamento Olá no sistema atual Olá.</span><span class="sxs-lookup"><span data-stu-id="29b39-213">toodo a clean migration, you have toostop all hello processing in hello current system.</span></span> <span data-ttu-id="29b39-214">Só então, pode obtê-lo tooconsistent Estado, o que pode migrar toohello nova plataforma.</span><span class="sxs-lookup"><span data-stu-id="29b39-214">Only then you can get it tooconsistent state which you can migrate toohello new platform.</span></span> <span data-ttu-id="29b39-215">Duração do período de indisponibilidade depende da quantidade de Olá de dados no Olá toomigrate de discos.</span><span class="sxs-lookup"><span data-stu-id="29b39-215">Downtime duration depends hello amount of data in hello disks toomigrate.</span></span>


1.  <span data-ttu-id="29b39-216">Em primeiro lugar, defina os parâmetros comuns de Olá:</span><span class="sxs-lookup"><span data-stu-id="29b39-216">First, set hello common parameters:</span></span>

    ```powershell
    $resourceGroupName = 'yourResourceGroupName'
    
    $location = 'your location' 
    
    $virtualNetworkName = 'yourExistingVirtualNetworkName'
    
    $virtualMachineName = 'yourVMName'
    
    $virtualMachineSize = 'Standard_DS3'
    
    $adminUserName = "youradminusername"
    
    $adminPassword = "yourpassword" | ConvertTo-SecureString -AsPlainText -Force
    
    $imageName = 'yourImageName'
    
    $osVhdUri = 'https://storageaccount.blob.core.windows.net/vhdcontainer/osdisk.vhd'
    
    $dataVhdUri = 'https://storageaccount.blob.core.windows.net/vhdcontainer/datadisk1.vhd'
    
    $dataDiskName = 'dataDisk1'
    ```

2.  <span data-ttu-id="29b39-217">Criar um disco de SO gerido com Olá VHD de Olá VMS clássicas.</span><span class="sxs-lookup"><span data-stu-id="29b39-217">Create a managed OS disk using hello VHD from hello classic VM.</span></span>

    <span data-ttu-id="29b39-218">Certifique-se de que lhe forneceu Olá concluir URI de Olá parâmetro toohello $osVhdUri de VHD de SO.</span><span class="sxs-lookup"><span data-stu-id="29b39-218">Ensure that you have provided hello complete URI of hello OS VHD toohello $osVhdUri parameter.</span></span> <span data-ttu-id="29b39-219">Além disso, introduza **- AccountType** como **PremiumLRS** ou **StandardLRS** com base no tipo de discos (Premium ou Standard) estiver a migrar para.</span><span class="sxs-lookup"><span data-stu-id="29b39-219">Also, enter **-AccountType** as **PremiumLRS** or **StandardLRS** based on type of disks (Premium or Standard) you are migrating to.</span></span>

    ```powershell
    $osDisk = New-AzureRmDisk -DiskName $osDiskName -Disk (New-AzureRmDiskConfig '
    -AccountType PremiumLRS -Location $location -CreateOption Import -SourceUri $osVhdUri) '
    -ResourceGroupName $resourceGroupName
    ```

3.  <span data-ttu-id="29b39-220">Anexar Olá SO disco toohello nova VM.</span><span class="sxs-lookup"><span data-stu-id="29b39-220">Attach hello OS disk toohello new VM.</span></span>

    ```powershell
    $VirtualMachine = New-AzureRmVMConfig -VMName $virtualMachineName -VMSize $virtualMachineSize
    $VirtualMachine = Set-AzureRmVMOSDisk -VM $VirtualMachine -ManagedDiskId $osDisk.Id '
    -StorageAccountType PremiumLRS -DiskSizeInGB 128 -CreateOption Attach -Windows
    ```

4.  <span data-ttu-id="29b39-221">Criar um disco de dados geridos a partir do ficheiro VHD de dados de Olá e adicioná-la toohello nova VM.</span><span class="sxs-lookup"><span data-stu-id="29b39-221">Create a managed data disk from hello data VHD file and add it toohello new VM.</span></span>

    ```powershell
    $dataDisk1 = New-AzureRmDisk -DiskName $dataDiskName -Disk (New-AzureRmDiskConfig '
    -AccountType PremiumLRS -Location $location -CreationDataCreateOption Import '
    -SourceUri $dataVhdUri ) -ResourceGroupName $resourceGroupName
    
    $VirtualMachine = Add-AzureRmVMDataDisk -VM $VirtualMachine -Name $dataDiskName '
    -CreateOption Attach -ManagedDiskId $dataDisk1.Id -Lun 1
    ```

5.  <span data-ttu-id="29b39-222">Criar Olá nova VM ao definir o IP público, rede Virtual e a NIC.</span><span class="sxs-lookup"><span data-stu-id="29b39-222">Create hello new VM by setting public IP, Virtual Network and NIC.</span></span>

    ```powershell
    $publicIp = New-AzureRmPublicIpAddress -Name ($VirtualMachineName.ToLower()+'_ip') '
    -ResourceGroupName $resourceGroupName -Location $location -AllocationMethod Dynamic
    
    $vnet = Get-AzureRmVirtualNetwork -Name $virtualNetworkName -ResourceGroupName $resourceGroupName
    
    $nic = New-AzureRmNetworkInterface -Name ($VirtualMachineName.ToLower()+'_nic') '
    -ResourceGroupName $resourceGroupName -Location $location -SubnetId $vnet.Subnets[0].Id '
    -PublicIpAddressId $publicIp.Id
    
    $VirtualMachine = Add-AzureRmVMNetworkInterface -VM $VirtualMachine -Id $nic.Id
    
    New-AzureRmVM -VM $VirtualMachine -ResourceGroupName $resourceGroupName -Location $location
    ```

> [!NOTE]
><span data-ttu-id="29b39-223">Poderão existir toosupport necessários passos adicionais a aplicação que não é ser abrangida neste guia.</span><span class="sxs-lookup"><span data-stu-id="29b39-223">There may be additional steps necessary toosupport your application that is not be covered by this guide.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="29b39-224">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="29b39-224">Next steps</span></span>

- <span data-ttu-id="29b39-225">Ligar a máquina virtual de toohello.</span><span class="sxs-lookup"><span data-stu-id="29b39-225">Connect toohello virtual machine.</span></span> <span data-ttu-id="29b39-226">Para obter instruções, consulte [como tooconnect e início de sessão tooan virtual do Azure máquina com o Windows](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="29b39-226">For instructions, see [How tooconnect and log on tooan Azure virtual machine running Windows](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

