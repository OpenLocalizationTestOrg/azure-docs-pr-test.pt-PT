---
title: aaaDesign e implementar uma Oracle da base de dados no Azure | Microsoft Docs
description: Conceber e implementar uma base de dados Oracle no seu ambiente do Azure.
services: virtual-machines-linux
documentationcenter: virtual-machines
author: v-shiuma
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 6/22/2017
ms.author: rclaus
ms.openlocfilehash: 8fa1207458695df1c7330ec626888b1b6b8d8939
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="design-and-implement-an-oracle-database-in-azure"></a><span data-ttu-id="b87c5-103">Conceber e implementar uma base de dados Oracle no Azure</span><span class="sxs-lookup"><span data-stu-id="b87c5-103">Design and implement an Oracle database in Azure</span></span>

## <a name="assumptions"></a><span data-ttu-id="b87c5-104">Pressupostos</span><span class="sxs-lookup"><span data-stu-id="b87c5-104">Assumptions</span></span>

- <span data-ttu-id="b87c5-105">Está a planear toomigrate uma base de dados Oracle de tooAzure no local.</span><span class="sxs-lookup"><span data-stu-id="b87c5-105">You're planning toomigrate an Oracle database from on-premises tooAzure.</span></span>
- <span data-ttu-id="b87c5-106">Ter uma compreensão dos Olá várias métricas nos relatórios de Oracle AWR.</span><span class="sxs-lookup"><span data-stu-id="b87c5-106">You have an understanding of hello various metrics in Oracle AWR reports.</span></span>
- <span data-ttu-id="b87c5-107">Ter uma compreensão de linha de base de desempenho da aplicação e a utilização de plataforma.</span><span class="sxs-lookup"><span data-stu-id="b87c5-107">You have a baseline understanding of application performance and platform utilization.</span></span>

## <a name="goals"></a><span data-ttu-id="b87c5-108">Objetivos</span><span class="sxs-lookup"><span data-stu-id="b87c5-108">Goals</span></span>

- <span data-ttu-id="b87c5-109">Compreender como toooptimize a implementação da Oracle no Azure.</span><span class="sxs-lookup"><span data-stu-id="b87c5-109">Understand how toooptimize your Oracle deployment in Azure.</span></span>
- <span data-ttu-id="b87c5-110">Explore as opções para uma base de dados Oracle num ambiente do Azure de otimização do desempenho.</span><span class="sxs-lookup"><span data-stu-id="b87c5-110">Explore performance tuning options for an Oracle database in an Azure environment.</span></span>

## <a name="hello-differences-between-an-on-premises-and-azure-implementation"></a><span data-ttu-id="b87c5-111">Olá diferenças entre no local e a implementação do Azure</span><span class="sxs-lookup"><span data-stu-id="b87c5-111">hello differences between an on-premises and Azure implementation</span></span> 

<span data-ttu-id="b87c5-112">Seguem-se algumas importante coisas tookeep em mente quando estiver a migrar no local tooAzure de aplicações.</span><span class="sxs-lookup"><span data-stu-id="b87c5-112">Following are some important things tookeep in mind when you're migrating on-premises applications tooAzure.</span></span> 

<span data-ttu-id="b87c5-113">Uma diferença importante é que uma implementação do Azure, recursos, tais como VMs, discos e redes virtuais são partilhados entre os outros clientes.</span><span class="sxs-lookup"><span data-stu-id="b87c5-113">One important difference is that in an Azure implementation, resources such as VMs, disks, and virtual networks are shared among other clients.</span></span> <span data-ttu-id="b87c5-114">Além disso, os recursos podem ser limitados com base nos requisitos de Olá.</span><span class="sxs-lookup"><span data-stu-id="b87c5-114">In addition, resources can be throttled based on hello requirements.</span></span> <span data-ttu-id="b87c5-115">Em vez de concentrar-se no evitando (MTBF) a falhar, Azure mais concentra-se no reiniciadas falha Olá (MTTR).</span><span class="sxs-lookup"><span data-stu-id="b87c5-115">Instead of focusing on avoiding failing (MTBF), Azure is more focused on surviving hello failure (MTTR).</span></span>

<span data-ttu-id="b87c5-116">Olá tabela seguinte lista algumas das diferenças de Olá entre uma implementação no local e uma implementação do Azure de uma base de dados Oracle.</span><span class="sxs-lookup"><span data-stu-id="b87c5-116">hello following table lists some of hello differences between an on-premises implementation and an Azure implementation of an Oracle database.</span></span>

> 
> |  | <span data-ttu-id="b87c5-117">**Implementação no local**</span><span class="sxs-lookup"><span data-stu-id="b87c5-117">**On-premises implementation**</span></span> | <span data-ttu-id="b87c5-118">**Implementação do Azure**</span><span class="sxs-lookup"><span data-stu-id="b87c5-118">**Azure implementation**</span></span> |
> | --- | --- | --- |
> | <span data-ttu-id="b87c5-119">**Redes**</span><span class="sxs-lookup"><span data-stu-id="b87c5-119">**Networking**</span></span> |<span data-ttu-id="b87c5-120">LAN/WAN</span><span class="sxs-lookup"><span data-stu-id="b87c5-120">LAN/WAN</span></span>  |<span data-ttu-id="b87c5-121">SDN (redes definidas por software)</span><span class="sxs-lookup"><span data-stu-id="b87c5-121">SDN (software-defined networking)</span></span>|
> | <span data-ttu-id="b87c5-122">**Grupo de segurança**</span><span class="sxs-lookup"><span data-stu-id="b87c5-122">**Security group**</span></span> |<span data-ttu-id="b87c5-123">Ferramentas de restrição de IP/porta</span><span class="sxs-lookup"><span data-stu-id="b87c5-123">IP/port restriction tools</span></span> |[<span data-ttu-id="b87c5-124">Grupo de segurança de rede (NSG)</span><span class="sxs-lookup"><span data-stu-id="b87c5-124">Network Security Group (NSG)</span></span>](https://azure.microsoft.com/blog/network-security-groups) |
> | <span data-ttu-id="b87c5-125">**Resiliência**</span><span class="sxs-lookup"><span data-stu-id="b87c5-125">**Resilience**</span></span> |<span data-ttu-id="b87c5-126">MTBF (tempo médio entre falhas)</span><span class="sxs-lookup"><span data-stu-id="b87c5-126">MTBF (mean time between failures)</span></span> |<span data-ttu-id="b87c5-127">MTTR (toorecovery de Greenwich)</span><span class="sxs-lookup"><span data-stu-id="b87c5-127">MTTR (mean time toorecovery)</span></span>|
> | <span data-ttu-id="b87c5-128">**Manutenção planeada**</span><span class="sxs-lookup"><span data-stu-id="b87c5-128">**Planned maintenance**</span></span> |<span data-ttu-id="b87c5-129">Aplicação de patches/atualizações</span><span class="sxs-lookup"><span data-stu-id="b87c5-129">Patching/upgrades</span></span>|<span data-ttu-id="b87c5-130">[Conjuntos de disponibilidade](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-availability-sets-guidelines) (aplicação de patches/atualizações geridas pelo Azure)</span><span class="sxs-lookup"><span data-stu-id="b87c5-130">[Availability sets](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-availability-sets-guidelines) (patching/upgrades managed by Azure)</span></span> |
> | <span data-ttu-id="b87c5-131">**Recurso**</span><span class="sxs-lookup"><span data-stu-id="b87c5-131">**Resource**</span></span> |<span data-ttu-id="b87c5-132">Dedicado</span><span class="sxs-lookup"><span data-stu-id="b87c5-132">Dedicated</span></span>  |<span data-ttu-id="b87c5-133">Partilhada com outros clientes</span><span class="sxs-lookup"><span data-stu-id="b87c5-133">Shared with other clients</span></span>|
> | <span data-ttu-id="b87c5-134">**Regiões**</span><span class="sxs-lookup"><span data-stu-id="b87c5-134">**Regions**</span></span> |<span data-ttu-id="b87c5-135">Datacenters</span><span class="sxs-lookup"><span data-stu-id="b87c5-135">Datacenters</span></span> |[<span data-ttu-id="b87c5-136">Pares de região</span><span class="sxs-lookup"><span data-stu-id="b87c5-136">Region pairs</span></span>](https://docs.microsoft.com/azure/virtual-machines/windows/regions-and-availability)|
> | <span data-ttu-id="b87c5-137">**Armazenamento**</span><span class="sxs-lookup"><span data-stu-id="b87c5-137">**Storage**</span></span> |<span data-ttu-id="b87c5-138">Discos físicos/SAN</span><span class="sxs-lookup"><span data-stu-id="b87c5-138">SAN/physical disks</span></span> |[<span data-ttu-id="b87c5-139">Armazenamento gerido pelo Azure</span><span class="sxs-lookup"><span data-stu-id="b87c5-139">Azure-managed storage</span></span>](https://azure.microsoft.com/pricing/details/managed-disks/?v=17.23h)|
> | <span data-ttu-id="b87c5-140">**Dimensionamento**</span><span class="sxs-lookup"><span data-stu-id="b87c5-140">**Scale**</span></span> |<span data-ttu-id="b87c5-141">Escala vertical</span><span class="sxs-lookup"><span data-stu-id="b87c5-141">Vertical scale</span></span> |<span data-ttu-id="b87c5-142">Dimensionamento horizontal</span><span class="sxs-lookup"><span data-stu-id="b87c5-142">Horizontal scale</span></span>|


### <a name="requirements"></a><span data-ttu-id="b87c5-143">Requisitos</span><span class="sxs-lookup"><span data-stu-id="b87c5-143">Requirements</span></span>

- <span data-ttu-id="b87c5-144">Determine a taxa de tamanho e crescimento da base de dados Olá.</span><span class="sxs-lookup"><span data-stu-id="b87c5-144">Determine hello database size and growth rate.</span></span>
- <span data-ttu-id="b87c5-145">Determine os requisitos de IOPS Olá, o que pode fazer a estimativa baseada em relatórios Oracle AWR ou outra ferramentas de monitorização de rede.</span><span class="sxs-lookup"><span data-stu-id="b87c5-145">Determine hello IOPS requirements, which you can estimate based on Oracle AWR reports or other network monitoring tools.</span></span>

## <a name="configuration-options"></a><span data-ttu-id="b87c5-146">Opções de configuração</span><span class="sxs-lookup"><span data-stu-id="b87c5-146">Configuration options</span></span>

<span data-ttu-id="b87c5-147">Existem quatro áreas potenciais que pode otimizar o desempenho de tooimprove num ambiente do Azure:</span><span class="sxs-lookup"><span data-stu-id="b87c5-147">There are four potential areas that you can tune tooimprove performance in an Azure environment:</span></span>

- <span data-ttu-id="b87c5-148">Tamanho da máquina virtual</span><span class="sxs-lookup"><span data-stu-id="b87c5-148">Virtual machine size</span></span>
- <span data-ttu-id="b87c5-149">Débito de rede</span><span class="sxs-lookup"><span data-stu-id="b87c5-149">Network throughput</span></span>
- <span data-ttu-id="b87c5-150">Configurações e os tipos de disco</span><span class="sxs-lookup"><span data-stu-id="b87c5-150">Disk types and configurations</span></span>
- <span data-ttu-id="b87c5-151">Definições de cache do disco</span><span class="sxs-lookup"><span data-stu-id="b87c5-151">Disk cache settings</span></span>

### <a name="generate-an-awr-report"></a><span data-ttu-id="b87c5-152">Gerar um relatório AWR</span><span class="sxs-lookup"><span data-stu-id="b87c5-152">Generate an AWR report</span></span>

<span data-ttu-id="b87c5-153">Se tiver uma base de dados Oracle existente e estiver a planear toomigrate tooAzure, tem várias opções.</span><span class="sxs-lookup"><span data-stu-id="b87c5-153">If you have an existing an Oracle database and are planning toomigrate tooAzure, you have several options.</span></span> <span data-ttu-id="b87c5-154">Pode executar Olá Oracle AWR relatório tooget Olá métricas (IOPS, Mbps, GiBs e assim sucessivamente).</span><span class="sxs-lookup"><span data-stu-id="b87c5-154">You can run hello Oracle AWR report tooget hello metrics (IOPS, Mbps, GiBs, and so on).</span></span> <span data-ttu-id="b87c5-155">Em seguida, escolha Olá que VM com base nas métricas Olá que recolheu.</span><span class="sxs-lookup"><span data-stu-id="b87c5-155">Then choose hello VM based on hello metrics that you collected.</span></span> <span data-ttu-id="b87c5-156">Ou pode contactar a sua infraestrutura equipa tooget semelhante as informações.</span><span class="sxs-lookup"><span data-stu-id="b87c5-156">Or you can contact your infrastructure team tooget similar information.</span></span>

<span data-ttu-id="b87c5-157">Poderá considerar executar relatório AWR durante regulares e pico cargas de trabalho, pelo que pode comparar.</span><span class="sxs-lookup"><span data-stu-id="b87c5-157">You might consider running your AWR report during both regular and peak workloads, so you can compare.</span></span> <span data-ttu-id="b87c5-158">Com base nestes relatórios, pode tamanho Olá VMs com base na carga de trabalho médio Olá ou carga de trabalho máximo Olá.</span><span class="sxs-lookup"><span data-stu-id="b87c5-158">Based on these reports, you can size hello VMs based on either hello average workload or hello maximum workload.</span></span>

<span data-ttu-id="b87c5-159">Segue-se um exemplo de como toogenerate um relatório AWR:</span><span class="sxs-lookup"><span data-stu-id="b87c5-159">Following is an example of how toogenerate an AWR report:</span></span>

```bash
$ sqlplus / as sysdba
SQL> EXEC DBMS_WORKLOAD_REPOSITORY.CREATE_SNAPSHOT;
SQL> @?/rdbms/admin/awrrpt.sql
```

### <a name="key-metrics"></a><span data-ttu-id="b87c5-160">Métricas-chave</span><span class="sxs-lookup"><span data-stu-id="b87c5-160">Key metrics</span></span>

<span data-ttu-id="b87c5-161">Seguem-se as métricas de Olá que pode obter de Olá relatório AWR:</span><span class="sxs-lookup"><span data-stu-id="b87c5-161">Following are hello metrics that you can obtain from hello AWR report:</span></span>

- <span data-ttu-id="b87c5-162">Número total de núcleos</span><span class="sxs-lookup"><span data-stu-id="b87c5-162">Total number of cores</span></span>
- <span data-ttu-id="b87c5-163">Velocidade de relógio de CPU</span><span class="sxs-lookup"><span data-stu-id="b87c5-163">CPU clock speed</span></span>
- <span data-ttu-id="b87c5-164">Total de memória em GB</span><span class="sxs-lookup"><span data-stu-id="b87c5-164">Total memory in GB</span></span>
- <span data-ttu-id="b87c5-165">Utilização da CPU</span><span class="sxs-lookup"><span data-stu-id="b87c5-165">CPU utilization</span></span>
- <span data-ttu-id="b87c5-166">Velocidade de transferência de dados das horas de ponta</span><span class="sxs-lookup"><span data-stu-id="b87c5-166">Peak data transfer rate</span></span>
- <span data-ttu-id="b87c5-167">Taxa de alterações de e/s (leitura/escrita)</span><span class="sxs-lookup"><span data-stu-id="b87c5-167">Rate of I/O changes (read/write)</span></span>
- <span data-ttu-id="b87c5-168">Refazer a taxa de registo (MBPs)</span><span class="sxs-lookup"><span data-stu-id="b87c5-168">Redo log rate (MBPs)</span></span>
- <span data-ttu-id="b87c5-169">Débito de rede</span><span class="sxs-lookup"><span data-stu-id="b87c5-169">Network throughput</span></span>
- <span data-ttu-id="b87c5-170">Taxa de latência de rede (baixa/alta)</span><span class="sxs-lookup"><span data-stu-id="b87c5-170">Network latency rate (low/high)</span></span>
- <span data-ttu-id="b87c5-171">Tamanho de base de dados em GB</span><span class="sxs-lookup"><span data-stu-id="b87c5-171">Database size in GB</span></span>
- <span data-ttu-id="b87c5-172">Bytes recebidos através de SQL * Net da / tooclient</span><span class="sxs-lookup"><span data-stu-id="b87c5-172">Bytes received via SQL*Net from/tooclient</span></span>

### <a name="virtual-machine-size"></a><span data-ttu-id="b87c5-173">Tamanho da máquina virtual</span><span class="sxs-lookup"><span data-stu-id="b87c5-173">Virtual machine size</span></span>

#### <a name="1-estimate-vm-size-based-on-cpu-memory-and-io-usage-from-hello-awr-report"></a><span data-ttu-id="b87c5-174">1. Estimar o tamanho da VM com base na utilização da CPU, memória e e/s de Olá relatório AWR</span><span class="sxs-lookup"><span data-stu-id="b87c5-174">1. Estimate VM size based on CPU, memory, and I/O usage from hello AWR report</span></span>

<span data-ttu-id="b87c5-175">Um aspeto que poderá ver é Olá superior cinco excedeu o tempo limite em primeiro plano eventos que indicam onde são congestionamentos de sistema Olá.</span><span class="sxs-lookup"><span data-stu-id="b87c5-175">One thing you might look at is hello top five timed foreground events that indicate where hello system bottlenecks are.</span></span>

<span data-ttu-id="b87c5-176">Por exemplo, Olá diagrama a seguir, sincronização de ficheiros de registo Olá é na parte superior do Olá.</span><span class="sxs-lookup"><span data-stu-id="b87c5-176">For example, in hello following diagram, hello log file sync is at hello top.</span></span> <span data-ttu-id="b87c5-177">Indica número de Olá de aguarda que sejam necessários antes de Olá LGWR escreve o ficheiro de registo de Refazer da memória intermédia toohello Olá registo.</span><span class="sxs-lookup"><span data-stu-id="b87c5-177">It indicates hello number of waits that are required before hello LGWR writes hello log buffer toohello redo log file.</span></span> <span data-ttu-id="b87c5-178">Estes resultados indicam que o melhor desempenho de armazenamento ou discos são necessários.</span><span class="sxs-lookup"><span data-stu-id="b87c5-178">These results indicate that better performing storage or disks are required.</span></span> <span data-ttu-id="b87c5-179">Além disso, Olá diagrama também mostra o número de Olá de CPU (núcleos) e quantidade Olá de memória.</span><span class="sxs-lookup"><span data-stu-id="b87c5-179">In addition, hello diagram also shows hello number of CPU (cores) and hello amount of memory.</span></span>

![Captura de ecrã da página do relatório Olá AWR](./media/oracle-design/cpu_memory_info.png)

<span data-ttu-id="b87c5-181">Olá diagrama seguinte mostra Olá e/s total de leitura e escrita.</span><span class="sxs-lookup"><span data-stu-id="b87c5-181">hello following diagram shows hello total I/O of read and write.</span></span> <span data-ttu-id="b87c5-182">Ocorreram GB 59 ler e GB 247.3 escritos durante a hora de Olá do relatório de Olá.</span><span class="sxs-lookup"><span data-stu-id="b87c5-182">There were 59 GB read and 247.3 GB written during hello time of hello report.</span></span>

![Captura de ecrã da página do relatório Olá AWR](./media/oracle-design/io_info.png)

#### <a name="2-choose-a-vm"></a><span data-ttu-id="b87c5-184">2. Escolha uma VM</span><span class="sxs-lookup"><span data-stu-id="b87c5-184">2. Choose a VM</span></span>

<span data-ttu-id="b87c5-185">Com base nas informações de Olá recolhidos a partir de Olá relatório AWR, o passo seguinte Olá é toochoose uma VM de um tamanho semelhante aos seus requisitos.</span><span class="sxs-lookup"><span data-stu-id="b87c5-185">Based on hello information that you collected from hello AWR report, hello next step is toochoose a VM of a similar size that meets your requirements.</span></span> <span data-ttu-id="b87c5-186">Pode encontrar uma lista de VMs disponíveis no artigo Olá [com otimização de memória](https://docs.microsoft.com/azure/virtual-machinFine tune es/virtual-machines-windows-sizes-memory).</span><span class="sxs-lookup"><span data-stu-id="b87c5-186">You can find a list of available VMs in hello article [Memory optimized](https://docs.microsoft.com/azure/virtual-machinFine tune es/virtual-machines-windows-sizes-memory).</span></span>

#### <a name="3-fine-tune-hello-vm-sizing-with-a-similar-vm-series-based-on-hello-acu"></a><span data-ttu-id="b87c5-187">3. Otimizar o dimensionamento de VM Olá com uma série VM semelhante com base no Olá ACU</span><span class="sxs-lookup"><span data-stu-id="b87c5-187">3. Fine-tune hello VM sizing with a similar VM series based on hello ACU</span></span>

<span data-ttu-id="b87c5-188">Depois que escolheu Olá VM, preste atenção toohello ACU para Olá VM.</span><span class="sxs-lookup"><span data-stu-id="b87c5-188">After you've chosen hello VM, pay attention toohello ACU for hello VM.</span></span> <span data-ttu-id="b87c5-189">Pode optar por utilizar uma VM diferente com base no Olá valor ACU que melhor se adequa aos seus requisitos.</span><span class="sxs-lookup"><span data-stu-id="b87c5-189">You might choose a different VM based on hello ACU value that better suits your requirements.</span></span> <span data-ttu-id="b87c5-190">Para obter mais informações, consulte [unidade de computação do Azure](https://docs.microsoft.com/azure/virtual-machines/windows/acu).</span><span class="sxs-lookup"><span data-stu-id="b87c5-190">For more information, see [Azure compute unit](https://docs.microsoft.com/azure/virtual-machines/windows/acu).</span></span>

![Captura de ecrã da página de unidades ACU Olá](./media/oracle-design/acu_units.png)

### <a name="network-throughput"></a><span data-ttu-id="b87c5-192">Débito de rede</span><span class="sxs-lookup"><span data-stu-id="b87c5-192">Network throughput</span></span>

<span data-ttu-id="b87c5-193">Olá seguinte diagrama mostra a relação de Olá entre débito e IOPS:</span><span class="sxs-lookup"><span data-stu-id="b87c5-193">hello following diagram shows hello relation between throughput and IOPS:</span></span>

![Captura de ecrã de débito](./media/oracle-design/throughput.png)

<span data-ttu-id="b87c5-195">débito de rede total Olá é estimado com base no Olá seguintes informações:</span><span class="sxs-lookup"><span data-stu-id="b87c5-195">hello total network throughput is estimated based on hello following information:</span></span>
- <span data-ttu-id="b87c5-196">SQL * tráfego de rede</span><span class="sxs-lookup"><span data-stu-id="b87c5-196">SQL*Net traffic</span></span>
- <span data-ttu-id="b87c5-197">MBps x o número de servidores (sequência de saída, tais como o Oracle Data Guard)</span><span class="sxs-lookup"><span data-stu-id="b87c5-197">MBps x number of servers (outbound stream such as Oracle Data Guard)</span></span>
- <span data-ttu-id="b87c5-198">Outros fatores, tais como replicação de aplicação</span><span class="sxs-lookup"><span data-stu-id="b87c5-198">Other factors, such as application replication</span></span>

![Captura de ecrã do Olá SQL * débito Net](./media/oracle-design/sqlnet_info.png)

<span data-ttu-id="b87c5-200">Com base nos seus requisitos de largura de banda de rede, existem vários tipos de gateway para toochoose do.</span><span class="sxs-lookup"><span data-stu-id="b87c5-200">Based on your network bandwidth requirements, there are various gateway types for you toochoose from.</span></span> <span data-ttu-id="b87c5-201">Estes incluem basic VpnGw e Azure ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="b87c5-201">These include basic, VpnGw, and Azure ExpressRoute.</span></span> <span data-ttu-id="b87c5-202">Para obter mais informações, consulte Olá [página de preços de gateway VPN](https://azure.microsoft.com/en-us/pricing/details/vpn-gateway/?v=17.23h).</span><span class="sxs-lookup"><span data-stu-id="b87c5-202">For more information, see hello [VPN gateway pricing page](https://azure.microsoft.com/en-us/pricing/details/vpn-gateway/?v=17.23h).</span></span>

<span data-ttu-id="b87c5-203">**Recommendations (Recomendações)**</span><span class="sxs-lookup"><span data-stu-id="b87c5-203">**Recommendations**</span></span>

- <span data-ttu-id="b87c5-204">Latência de rede é a implementação de local de tooan em comparação com superior.</span><span class="sxs-lookup"><span data-stu-id="b87c5-204">Network latency is higher compared tooan on-premises deployment.</span></span> <span data-ttu-id="b87c5-205">Reduzir rede arredondar viagens pode significativamente melhorar o desempenho.</span><span class="sxs-lookup"><span data-stu-id="b87c5-205">Reducing network round trips can greatly improve performance.</span></span>
- <span data-ttu-id="b87c5-206">consolidar de ida e volta de tooreduce, as aplicações que têm aplicações "chatty" ou de transações elevadas em Olá mesma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="b87c5-206">tooreduce round-trips, consolidate applications that have high transactions or “chatty” apps on hello same virtual machine.</span></span>

### <a name="disk-types-and-configurations"></a><span data-ttu-id="b87c5-207">Configurações e os tipos de disco</span><span class="sxs-lookup"><span data-stu-id="b87c5-207">Disk types and configurations</span></span>

- <span data-ttu-id="b87c5-208">*Predefinição discos de SO*: estes tipos de disco oferecem dados persistentes e colocação em cache.</span><span class="sxs-lookup"><span data-stu-id="b87c5-208">*Default OS disks*: These disk types offer persistent data and caching.</span></span> <span data-ttu-id="b87c5-209">Estes estão otimizados para acesso de SO no arranque e não são concebidos para um transacional ou cargas de trabalho (analíticas) do armazém de dados.</span><span class="sxs-lookup"><span data-stu-id="b87c5-209">They are optimized for OS access at startup, and aren't designed for either transactional or data warehouse (analytical) workloads.</span></span>

- <span data-ttu-id="b87c5-210">*Não gerido discos*: com estes tipos de disco, gere contas de armazenamento de Olá que armazenam ficheiros de disco rígido virtual (VHD) de Olá que correspondem tooyour discos da VM.</span><span class="sxs-lookup"><span data-stu-id="b87c5-210">*Unmanaged disks*: With these disk types, you manage hello storage accounts that store hello virtual hard disk (VHD) files that correspond tooyour VM disks.</span></span> <span data-ttu-id="b87c5-211">Ficheiros VHD são armazenados como blobs de páginas em contas do storage do Azure.</span><span class="sxs-lookup"><span data-stu-id="b87c5-211">VHD files are stored as page blobs in Azure storage accounts.</span></span>

- <span data-ttu-id="b87c5-212">*Discos geridos pelo*: Azure gere contas de armazenamento de Olá que utilizar para os discos VM.</span><span class="sxs-lookup"><span data-stu-id="b87c5-212">*Managed disks*: Azure manages hello storage accounts that you use for your VM disks.</span></span> <span data-ttu-id="b87c5-213">Especifique o tipo de disco Olá (standard ou premium) e o tamanho de Olá do disco de Olá que precisa.</span><span class="sxs-lookup"><span data-stu-id="b87c5-213">You specify hello disk type (premium or standard) and hello size of hello disk that you need.</span></span> <span data-ttu-id="b87c5-214">Azure cria e gere o disco de Olá por si.</span><span class="sxs-lookup"><span data-stu-id="b87c5-214">Azure creates and manages hello disk for you.</span></span>

- <span data-ttu-id="b87c5-215">*Discos de armazenamento Premium*: estes tipos de disco são mais adequados para cargas de trabalho de produção.</span><span class="sxs-lookup"><span data-stu-id="b87c5-215">*Premium storage disks*: These disk types are best suited for production workloads.</span></span> <span data-ttu-id="b87c5-216">Premium storage suporta discos de VM que podem ser anexados a série de tamanho toospecific VMs, tais como série DS, série DSv2, GS e F VMs.</span><span class="sxs-lookup"><span data-stu-id="b87c5-216">Premium storage supports VM disks that can be attached toospecific size-series VMs, such as DS, DSv2, GS, and F series VMs.</span></span> <span data-ttu-id="b87c5-217">disco de premium Olá vem com tamanhos diferentes e pode escolher entre discos de 32 GB too4, 096 GB.</span><span class="sxs-lookup"><span data-stu-id="b87c5-217">hello premium disk comes with different sizes, and you can choose between disks ranging from 32 GB too4,096 GB.</span></span> <span data-ttu-id="b87c5-218">Cada tamanho do disco tem as suas próprias especificações de desempenho.</span><span class="sxs-lookup"><span data-stu-id="b87c5-218">Each disk size has its own performance specifications.</span></span> <span data-ttu-id="b87c5-219">Dependendo dos requisitos de aplicação, poderá anexar um ou mais discos tooyour VM.</span><span class="sxs-lookup"><span data-stu-id="b87c5-219">Depending on your application requirements, you can attach one or more disks tooyour VM.</span></span>

<span data-ttu-id="b87c5-220">Quando criar um novo disco gerido a partir do portal de Olá, pode escolher Olá **tipo de conta** para o tipo de Olá de disco que pretende toouse.</span><span class="sxs-lookup"><span data-stu-id="b87c5-220">When you create a new managed disk from hello portal, you can choose hello **Account type** for hello type of disk you want toouse.</span></span> <span data-ttu-id="b87c5-221">Tenha em atenção que nem todos os discos disponíveis são apresentados no menu pendente de Olá.</span><span class="sxs-lookup"><span data-stu-id="b87c5-221">Keep in mind that not all available disks are shown in hello drop-down menu.</span></span> <span data-ttu-id="b87c5-222">Depois de escolher um tamanho VM específico, o menu Olá mostra apenas Olá disponível armazenamento premium SKUs que se baseiam nesse tamanho VM.</span><span class="sxs-lookup"><span data-stu-id="b87c5-222">After you choose a particular VM size, hello menu shows only hello available premium storage SKUs that are based on that VM size.</span></span>

![Captura de ecrã da página de disco gerido Olá](./media/oracle-design/premium_disk01.png)

<span data-ttu-id="b87c5-224">Para obter mais informações, consulte [elevado desempenho Premium Storage e discos geridos para VMs](https://docs.microsoft.com/azure/storage/storage-premium-storage).</span><span class="sxs-lookup"><span data-stu-id="b87c5-224">For more information, see [High-performance Premium Storage and managed disks for VMs](https://docs.microsoft.com/azure/storage/storage-premium-storage).</span></span>

<span data-ttu-id="b87c5-225">Depois de configurar o armazenamento numa VM, pode querer discos de Olá tooload teste antes de criar uma base de dados.</span><span class="sxs-lookup"><span data-stu-id="b87c5-225">After you configure your storage on a VM, you might want tooload test hello disks before creating a database.</span></span> <span data-ttu-id="b87c5-226">Saber a taxa de e/s de Olá em termos de latência e débito pode ajudar a determinar se Olá VMs suportam Olá esperado débito com destinos de latência.</span><span class="sxs-lookup"><span data-stu-id="b87c5-226">Knowing hello I/O rate in terms of both latency and throughput can help you determine if hello VMs support hello expected throughput with latency targets.</span></span>

<span data-ttu-id="b87c5-227">Existem várias ferramentas para a aplicação teste de carga, como Oracle Orion, Sysbench e Fio.</span><span class="sxs-lookup"><span data-stu-id="b87c5-227">There are a number of tools for application load testing, such as Oracle Orion, Sysbench, and Fio.</span></span>

<span data-ttu-id="b87c5-228">Execute o teste de carga Olá novamente depois de implementar uma base de dados Oracle.</span><span class="sxs-lookup"><span data-stu-id="b87c5-228">Run hello load test again after you've deployed an Oracle database.</span></span> <span data-ttu-id="b87c5-229">Iniciar as cargas de trabalho normais e utilização máxima e Olá Mostrar resultados Olá da linha de base do seu ambiente.</span><span class="sxs-lookup"><span data-stu-id="b87c5-229">Start your regular and peak workloads, and hello results show you hello baseline of your environment.</span></span>

<span data-ttu-id="b87c5-230">Poderá ser mais importante toosize Olá no armazenamento baseado em taxa IOPS Olá em vez de tamanho de armazenamento Olá.</span><span class="sxs-lookup"><span data-stu-id="b87c5-230">It might be more important toosize hello storage based on hello IOPS rate rather than hello storage size.</span></span> <span data-ttu-id="b87c5-231">Por exemplo, se necessário Olá IOPS é 5.000, mas só precisa de 200 GB, poderá obter disco premium do Olá P30 classe, apesar de este inclui mais de 200 GB de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="b87c5-231">For example, if hello required IOPS is 5,000, but you only need 200 GB, you might still get hello P30 class premium disk even though it comes with more than 200 GB of storage.</span></span>

<span data-ttu-id="b87c5-232">taxa IOPS Olá pode ser obtida a partir Olá relatório AWR.</span><span class="sxs-lookup"><span data-stu-id="b87c5-232">hello IOPS rate can be obtained from hello AWR report.</span></span> <span data-ttu-id="b87c5-233">Este é determinado pelo registo de Refazer Olá, leituras físicas e velocidade de escritas.</span><span class="sxs-lookup"><span data-stu-id="b87c5-233">It's determined by hello redo log, physical reads, and writes rate.</span></span>

![Captura de ecrã da página do relatório Olá AWR](./media/oracle-design/awr_report.png)

<span data-ttu-id="b87c5-235">Por exemplo, o tamanho de Refazer Olá é 12,200,000 bytes por segundo, que é igual too11.63 MBPs.</span><span class="sxs-lookup"><span data-stu-id="b87c5-235">For example, hello redo size is 12,200,000 bytes per second, which is equal too11.63 MBPs.</span></span>
<span data-ttu-id="b87c5-236">Olá IOPS é 12,200,000 / 2,358 = 5,174.</span><span class="sxs-lookup"><span data-stu-id="b87c5-236">hello IOPS is 12,200,000 / 2,358 = 5,174.</span></span>

<span data-ttu-id="b87c5-237">Depois de ter uma visão clara dos requisitos de e/s de Olá, pode escolher uma combinação de unidades que melhor se adequam toomeet esses requisitos.</span><span class="sxs-lookup"><span data-stu-id="b87c5-237">After you have a clear picture of hello I/O requirements, you can choose a combination of drives that are best suited toomeet those requirements.</span></span>

<span data-ttu-id="b87c5-238">**Recommendations (Recomendações)**</span><span class="sxs-lookup"><span data-stu-id="b87c5-238">**Recommendations**</span></span>

- <span data-ttu-id="b87c5-239">Para o espaço de tabelas de dados, distribuídos carga de trabalho de e/s de Olá por um número de discos utilizando o armazenamento gerido ou Oracle ASM.</span><span class="sxs-lookup"><span data-stu-id="b87c5-239">For data tablespace, spread hello I/O workload across a number of disks by using managed storage or Oracle ASM.</span></span>
- <span data-ttu-id="b87c5-240">À medida que aumenta o tamanho do bloco Olá e/s para operações que exigem muita leitura e escrita intensivas, adicione mais discos de dados.</span><span class="sxs-lookup"><span data-stu-id="b87c5-240">As hello I/O block size increases for read-intensive and write-intensive operations, add more data disks.</span></span>
- <span data-ttu-id="b87c5-241">Aumente o tamanho do bloco Olá para processos sequenciais grandes.</span><span class="sxs-lookup"><span data-stu-id="b87c5-241">Increase hello block size for large sequential processes.</span></span>
- <span data-ttu-id="b87c5-242">Utilize a e/s tooreduce de compressão de dados (para dados e índices).</span><span class="sxs-lookup"><span data-stu-id="b87c5-242">Use data compression tooreduce I/O (for both data and indexes).</span></span>
- <span data-ttu-id="b87c5-243">Separe os registos de Refazer, sistema e temps e anular TS em discos de dados separada.</span><span class="sxs-lookup"><span data-stu-id="b87c5-243">Separate redo logs, system, and temps, and undo TS on separate data disks.</span></span>
- <span data-ttu-id="b87c5-244">Não coloque os ficheiros de aplicação em discos de SO predefinido (dev/sda).</span><span class="sxs-lookup"><span data-stu-id="b87c5-244">Don't put any application files on default OS disks (/dev/sda).</span></span> <span data-ttu-id="b87c5-245">Estes discos não estão otimizados para a VM rápida tempos de arranque e poderá não fornecer um bom desempenho para a sua aplicação.</span><span class="sxs-lookup"><span data-stu-id="b87c5-245">These disks aren't optimized for fast VM boot times, and they might not provide good performance for your application.</span></span>

### <a name="disk-cache-settings"></a><span data-ttu-id="b87c5-246">Definições de cache do disco</span><span class="sxs-lookup"><span data-stu-id="b87c5-246">Disk cache settings</span></span>

<span data-ttu-id="b87c5-247">Existem três opções para a colocação em cache do anfitrião:</span><span class="sxs-lookup"><span data-stu-id="b87c5-247">There are three options for host caching:</span></span>

- <span data-ttu-id="b87c5-248">*Só de leitura*: todos os pedidos são colocados em cache para leituras futuras.</span><span class="sxs-lookup"><span data-stu-id="b87c5-248">*Read-only*: All requests are cached for future reads.</span></span> <span data-ttu-id="b87c5-249">Todas as escritas são mantidas diretamente tooAzure armazenamento de Blobs.</span><span class="sxs-lookup"><span data-stu-id="b87c5-249">All writes are persisted directly tooAzure Blob storage.</span></span>

- <span data-ttu-id="b87c5-250">*Leitura e escrita*: Este é um algoritmo "antecipadas".</span><span class="sxs-lookup"><span data-stu-id="b87c5-250">*Read-write*: This is a “read-ahead” algorithm.</span></span> <span data-ttu-id="b87c5-251">Olá lê e escreve é colocadas em cache para leituras futuras.</span><span class="sxs-lookup"><span data-stu-id="b87c5-251">hello reads and writes are cached for future reads.</span></span> <span data-ttu-id="b87c5-252">Não-escrita-through escreve são persistente toohello local cache primeiro.</span><span class="sxs-lookup"><span data-stu-id="b87c5-252">Non-write-through writes are persisted toohello local cache first.</span></span> <span data-ttu-id="b87c5-253">Para o SQL Server, escreve são tooAzure persistente armazenamento porque utiliza através de escrita.</span><span class="sxs-lookup"><span data-stu-id="b87c5-253">For SQL Server, writes are persisted tooAzure Storage because it uses write-through.</span></span> <span data-ttu-id="b87c5-254">Também fornece mais baixa latência de disco Olá para cargas de trabalho leves.</span><span class="sxs-lookup"><span data-stu-id="b87c5-254">It also provides hello lowest disk latency for light workloads.</span></span>

- <span data-ttu-id="b87c5-255">*Nenhum* (desativada): ao utilizar esta opção, pode ignorar a cache de Olá.</span><span class="sxs-lookup"><span data-stu-id="b87c5-255">*None* (disabled): By using this option, you can bypass hello cache.</span></span> <span data-ttu-id="b87c5-256">Todos os dados de Olá é toodisk transferido e persistente tooAzure armazenamento.</span><span class="sxs-lookup"><span data-stu-id="b87c5-256">All hello data is transferred toodisk and persisted tooAzure Storage.</span></span> <span data-ttu-id="b87c5-257">Este oferece método hello mais elevada taxa de e/s para cargas de trabalho exigente em termos de e/s.</span><span class="sxs-lookup"><span data-stu-id="b87c5-257">This method gives you hello highest I/O rate for I/O intensive workloads.</span></span> <span data-ttu-id="b87c5-258">Também precisa de tootake "custos de transação" em consideração.</span><span class="sxs-lookup"><span data-stu-id="b87c5-258">You also need tootake “transaction cost” into consideration.</span></span>

<span data-ttu-id="b87c5-259">**Recommendations (Recomendações)**</span><span class="sxs-lookup"><span data-stu-id="b87c5-259">**Recommendations**</span></span>

<span data-ttu-id="b87c5-260">débito do toomaximize Olá, recomendamos que comece com **nenhum** para a colocação em cache do anfitrião.</span><span class="sxs-lookup"><span data-stu-id="b87c5-260">toomaximize hello throughput, we recommend that you  start with **None** for host caching.</span></span> <span data-ttu-id="b87c5-261">Para o Premium Storage, tenha em atenção que tem de desativar Olá "barreiras as eficazes" ao montar o sistema de ficheiros de Olá com Olá **ReadOnly** ou **nenhum** opções.</span><span class="sxs-lookup"><span data-stu-id="b87c5-261">For Premium Storage, keep in mind that you must disable hello "barriers" when you mount hello file system with hello **ReadOnly** or **None** options.</span></span> <span data-ttu-id="b87c5-262">Atualize ficheiro de /etc/fstab Olá com discos de toohello Olá UUID.</span><span class="sxs-lookup"><span data-stu-id="b87c5-262">Update hello /etc/fstab file with hello UUID toohello disks.</span></span>

<span data-ttu-id="b87c5-263">Para obter mais informações, consulte [Premium Storage para VMs com Linux](https://docs.microsoft.com/azure/storage/storage-premium-storage#premium-storage-for-linux-vms).</span><span class="sxs-lookup"><span data-stu-id="b87c5-263">For more information, see [Premium Storage for Linux VMs](https://docs.microsoft.com/azure/storage/storage-premium-storage#premium-storage-for-linux-vms).</span></span>

![Captura de ecrã da página de disco gerido Olá](./media/oracle-design/premium_disk02.png)

- <span data-ttu-id="b87c5-265">Para discos de SO, utilizar a predefinição **leitura/escrita** colocação em cache.</span><span class="sxs-lookup"><span data-stu-id="b87c5-265">For OS disks, use default **Read/Write** caching.</span></span>
- <span data-ttu-id="b87c5-266">Para o sistema, TEMP e anulação utilizar **nenhum** para colocar em cache.</span><span class="sxs-lookup"><span data-stu-id="b87c5-266">For SYSTEM, TEMP, and UNDO use **None** for caching.</span></span>
- <span data-ttu-id="b87c5-267">Para os dados, utilize **nenhum** para colocar em cache.</span><span class="sxs-lookup"><span data-stu-id="b87c5-267">For DATA, use **None** for caching.</span></span> <span data-ttu-id="b87c5-268">Mas se a base de dados é só de leitura ou de leitura intensiva, utilize **só de leitura** colocação em cache.</span><span class="sxs-lookup"><span data-stu-id="b87c5-268">But if your database is read-only or read-intensive, use **Read-only** caching.</span></span>

<span data-ttu-id="b87c5-269">Depois da definição de disco de dados é guardada, não é possível alterar a definição de cache do anfitrião de Olá, a menos que desmonte a unidade de Olá em Olá ao nível do SO e, em seguida, voltar a montá-lo Depois de efetuadas Olá alterar.</span><span class="sxs-lookup"><span data-stu-id="b87c5-269">After your data disk setting is saved, you can't change hello host cache setting unless you unmount hello drive at hello OS level and then remount it after you've made hello change.</span></span>


## <a name="security"></a><span data-ttu-id="b87c5-270">Segurança</span><span class="sxs-lookup"><span data-stu-id="b87c5-270">Security</span></span>

<span data-ttu-id="b87c5-271">Depois de configurar e configurar o seu ambiente do Azure, o passo seguinte Olá é toosecure sua rede.</span><span class="sxs-lookup"><span data-stu-id="b87c5-271">After you have set up and configured your Azure environment, hello next step is toosecure your network.</span></span> <span data-ttu-id="b87c5-272">Seguem-se algumas recomendações:</span><span class="sxs-lookup"><span data-stu-id="b87c5-272">Here are some recommendations:</span></span>

- <span data-ttu-id="b87c5-273">*Política NSG*: NSG pode ser definido por uma sub-rede ou NIC.</span><span class="sxs-lookup"><span data-stu-id="b87c5-273">*NSG policy*: NSG can be defined by a subnet or NIC.</span></span> <span data-ttu-id="b87c5-274">É mais simples toocontrol acesso ao nível de sub-rede Olá para segurança e a imposição de encaminhamento para coisas como firewalls de aplicação.</span><span class="sxs-lookup"><span data-stu-id="b87c5-274">It's simpler toocontrol access at hello subnet level both for security and force routing for things like application firewalls.</span></span>

- <span data-ttu-id="b87c5-275">*Jumpbox*: para um acesso mais seguro, os administradores devem não ligar diretamente toohello serviço de aplicações ou a base de dados.</span><span class="sxs-lookup"><span data-stu-id="b87c5-275">*Jumpbox*: For more secure access, administrators should not directly connect toohello application service or database.</span></span> <span data-ttu-id="b87c5-276">Um jumpbox é utilizado como um suporte de dados entre a máquina de administrador de Olá e de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="b87c5-276">A jumpbox is used as a media between hello administrator machine and Azure resources.</span></span>
<span data-ttu-id="b87c5-277">![Captura de ecrã da página de topologia de Jumpbox Olá](./media/oracle-design/jumpbox.png)</span><span class="sxs-lookup"><span data-stu-id="b87c5-277">![Screenshot of hello Jumpbox topology page](./media/oracle-design/jumpbox.png)</span></span>

    <span data-ttu-id="b87c5-278">máquina de administrador Olá deve oferecer apenas o acesso restrito de IP toohello jumpbox.</span><span class="sxs-lookup"><span data-stu-id="b87c5-278">hello administrator machine should offer IP-restricted access toohello jumpbox only.</span></span> <span data-ttu-id="b87c5-279">Olá jumpbox deve ter acesso toohello aplicação e a base de dados.</span><span class="sxs-lookup"><span data-stu-id="b87c5-279">hello jumpbox should have access toohello application and database.</span></span>

- <span data-ttu-id="b87c5-280">*Rede privada* (sub-redes): Recomendamos que tenha o serviço de aplicações de Olá e base de dados em sub-redes diferentes, para melhorar o controlo pode ser definido pela política NSG.</span><span class="sxs-lookup"><span data-stu-id="b87c5-280">*Private network* (subnets): We recommend that you have hello application service and database on separate subnets, so better control can be set by NSG policy.</span></span>


## <a name="additional-reading"></a><span data-ttu-id="b87c5-281">Leitura adicional</span><span class="sxs-lookup"><span data-stu-id="b87c5-281">Additional reading</span></span>

- [<span data-ttu-id="b87c5-282">Configurar Oracle ASM</span><span class="sxs-lookup"><span data-stu-id="b87c5-282">Configure Oracle ASM</span></span>](configure-oracle-asm.md)
- [<span data-ttu-id="b87c5-283">Configurar a proteção de dados Oracle</span><span class="sxs-lookup"><span data-stu-id="b87c5-283">Configure Oracle Data Guard</span></span>](configure-oracle-dataguard.md)
- [<span data-ttu-id="b87c5-284">Configurar a porta de Golden Oracle</span><span class="sxs-lookup"><span data-stu-id="b87c5-284">Configure Oracle Golden Gate</span></span>](configure-oracle-golden-gate.md)
- [<span data-ttu-id="b87c5-285">Cópia de segurança do Oracle e recuperação</span><span class="sxs-lookup"><span data-stu-id="b87c5-285">Oracle backup and recovery</span></span>](oracle-backup-recovery.md)

## <a name="next-steps"></a><span data-ttu-id="b87c5-286">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="b87c5-286">Next steps</span></span>

- [<span data-ttu-id="b87c5-287">Tutorial: Criar as VMs de elevada disponibilidade</span><span class="sxs-lookup"><span data-stu-id="b87c5-287">Tutorial: Create highly available VMs</span></span>](../../linux/create-cli-complete.md)
- [<span data-ttu-id="b87c5-288">Explorar amostras de CLI do Azure de implementação de VM</span><span class="sxs-lookup"><span data-stu-id="b87c5-288">Explore VM deployment Azure CLI samples</span></span>](../../linux/cli-samples.md)
