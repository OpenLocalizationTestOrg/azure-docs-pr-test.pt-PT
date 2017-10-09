---
title: aaaSQL FCI Servidor - Virtual Machines do Azure | Microsoft Docs
description: "Este artigo explica como toocreate instância de Cluster de ativação pós-falha do SQL Server em Azure Virtual Machines."
services: virtual-machines
documentationCenter: na
authors: MikeRayMSFT
manager: jhubbard
editor: monicar
tags: azure-service-management
ms.assetid: 9fc761b1-21ad-4d79-bebc-a2f094ec214d
ms.service: virtual-machines-sql
ms.devlang: na
ms.custom: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 03/17/2017
ms.author: mikeray
ms.openlocfilehash: bee3b27805c5f6cc02a43b25d480c129c254cb90
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-sql-server-failover-cluster-instance-on-azure-virtual-machines"></a><span data-ttu-id="a3671-103">Configurar a instância de Cluster de ativação pós-falha do SQL Server em Virtual Machines do Azure</span><span class="sxs-lookup"><span data-stu-id="a3671-103">Configure SQL Server Failover Cluster Instance on Azure Virtual Machines</span></span>

<span data-ttu-id="a3671-104">Este artigo explica como toocreate uma SQL Server Cluster de ativação pós-falha (FCI) de instância em máquinas virtuais do Azure no modelo do Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="a3671-104">This article explains how toocreate a SQL Server Failover Cluster Instance (FCI) on Azure virtual machines in Resource Manager model.</span></span> <span data-ttu-id="a3671-105">Esta solução usa [edição Datacenter do Windows Server 2016 espaços de armazenamento direto \(S2D\) ](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/storage-spaces-direct-overview) como uma SAN de virtual baseado em software que sincroniza o armazenamento de Olá (discos de dados) entre Olá nós (as VMs do Azure) um Cluster do Windows.</span><span class="sxs-lookup"><span data-stu-id="a3671-105">This solution uses [Windows Server 2016 Datacenter edition Storage Spaces Direct \(S2D\)](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/storage-spaces-direct-overview) as a software-based virtual SAN that synchronizes hello storage (data disks) between hello nodes (Azure VMs) in a Windows Cluster.</span></span> <span data-ttu-id="a3671-106">S2D é nova no Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="a3671-106">S2D is new in Windows Server 2016.</span></span>

<span data-ttu-id="a3671-107">Olá diagrama seguinte mostra solução completa de Olá em máquinas virtuais do Azure:</span><span class="sxs-lookup"><span data-stu-id="a3671-107">hello following diagram shows hello complete solution on Azure virtual machines:</span></span>

![Grupo de disponibilidade](./media/virtual-machines-windows-portal-sql-create-failover-cluster/00-sql-fci-s2d-complete-solution.png)

<span data-ttu-id="a3671-109">Olá precedente diagrama mostra:</span><span class="sxs-lookup"><span data-stu-id="a3671-109">hello preceding diagram shows:</span></span>

- <span data-ttu-id="a3671-110">Dois virtual machines do Azure num cluster de ativação pós-falha do Windows.</span><span class="sxs-lookup"><span data-stu-id="a3671-110">Two Azure virtual machines in a Windows Failover Cluster.</span></span> <span data-ttu-id="a3671-111">Quando uma máquina virtual está num cluster de ativação pós-falha também é denominado um *o nó de cluster*, ou *nós*.</span><span class="sxs-lookup"><span data-stu-id="a3671-111">When a virtual machine is in a failover cluster it is also called a *cluster node*, or *nodes*.</span></span>
- <span data-ttu-id="a3671-112">Cada máquina virtual tem dois ou mais discos de dados.</span><span class="sxs-lookup"><span data-stu-id="a3671-112">Each virtual machine has two or more data disks.</span></span>
- <span data-ttu-id="a3671-113">S2D sincroniza os dados de Olá no disco de dados de Olá e apresenta Olá sincronizado armazenamento como um agrupamento de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="a3671-113">S2D synchronizes hello data on hello data disk and presents hello synchronized storage as a storage pool.</span></span>
- <span data-ttu-id="a3671-114">agrupamento de armazenamento Olá apresenta um cluster de ativação pós-falha do cluster (CSV) de volume partilhado toohello.</span><span class="sxs-lookup"><span data-stu-id="a3671-114">hello storage pool presents a cluster shared volume (CSV) toohello failover cluster.</span></span>
- <span data-ttu-id="a3671-115">função de cluster do SQL Server FCI Olá utiliza Olá CSV para Olá unidades de dados.</span><span class="sxs-lookup"><span data-stu-id="a3671-115">hello SQL Server FCI cluster role uses hello CSV for hello data drives.</span></span>
- <span data-ttu-id="a3671-116">Um carga do Azure balanceador toohold Olá endereço IP para Olá SQL Server FCI.</span><span class="sxs-lookup"><span data-stu-id="a3671-116">An Azure load balancer toohold hello IP address for hello SQL Server FCI.</span></span>
- <span data-ttu-id="a3671-117">Um conjunto de disponibilidade do Azure retém todos os recursos de Olá.</span><span class="sxs-lookup"><span data-stu-id="a3671-117">An Azure availability set holds all hello resources.</span></span>

   >[!NOTE]
   ><span data-ttu-id="a3671-118">Todos os recursos do Azure estão no diagrama de Olá em Olá mesmo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="a3671-118">All Azure resources are in hello diagram are in hello same resource group.</span></span>

<span data-ttu-id="a3671-119">Para obter detalhes sobre S2D, consulte [edição Datacenter do Windows Server 2016 espaços de armazenamento direto \(S2D\)](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/storage-spaces-direct-overview).</span><span class="sxs-lookup"><span data-stu-id="a3671-119">For details about S2D, see [Windows Server 2016 Datacenter edition Storage Spaces Direct \(S2D\)](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/storage-spaces-direct-overview).</span></span>

<span data-ttu-id="a3671-120">S2D suportam dois tipos de arquiteturas - convergidas e hiperconvergida.</span><span class="sxs-lookup"><span data-stu-id="a3671-120">S2D supports two types of architectures - converged and hyper-converged.</span></span> <span data-ttu-id="a3671-121">arquitetura de Olá neste documento é hiperconvergida.</span><span class="sxs-lookup"><span data-stu-id="a3671-121">hello architecture in this document is hyper-converged.</span></span> <span data-ttu-id="a3671-122">Um infraestrutura hiperconvergida locais Olá armazenamento Olá mesmos servidores essa aplicação Olá em cluster do anfitrião.</span><span class="sxs-lookup"><span data-stu-id="a3671-122">A hyper-converged infrastructure places hello storage on hello same servers that host hello clustered application.</span></span> <span data-ttu-id="a3671-123">Nesta arquitetura, o armazenamento de Olá é em cada nó do SQL Server FCI.</span><span class="sxs-lookup"><span data-stu-id="a3671-123">In this architecture, hello storage is on each SQL Server FCI node.</span></span>

### <a name="example-azure-template"></a><span data-ttu-id="a3671-124">Exemplo modelo do Azure</span><span class="sxs-lookup"><span data-stu-id="a3671-124">Example Azure template</span></span>

<span data-ttu-id="a3671-125">Pode criar solução completa de Olá no Azure a partir de um modelo.</span><span class="sxs-lookup"><span data-stu-id="a3671-125">You can create hello entire solution in Azure from a template.</span></span> <span data-ttu-id="a3671-126">Um exemplo de um modelo está disponível no Olá GitHub [modelos de início rápido do Azure](https://github.com/MSBrett/azure-quickstart-templates/tree/master/sql-server-2016-fci-existing-vnet-and-ad).</span><span class="sxs-lookup"><span data-stu-id="a3671-126">An example of a template is available in hello GitHub [Azure Quickstart Templates](https://github.com/MSBrett/azure-quickstart-templates/tree/master/sql-server-2016-fci-existing-vnet-and-ad).</span></span> <span data-ttu-id="a3671-127">Este exemplo não concebido ou não está testado para qualquer carga de trabalho específica.</span><span class="sxs-lookup"><span data-stu-id="a3671-127">This example is not designed or tested for any specific workload.</span></span> <span data-ttu-id="a3671-128">Pode executar Olá modelo toocreate um FCI do SQL Server com o domínio de tooyour ligado de armazenamento S2D.</span><span class="sxs-lookup"><span data-stu-id="a3671-128">You can run hello template toocreate a SQL Server FCI with S2D storage connected tooyour domain.</span></span> <span data-ttu-id="a3671-129">Pode avaliar modelo Olá e modificá-lo para os fins pretendidos.</span><span class="sxs-lookup"><span data-stu-id="a3671-129">You can evaluate hello template, and modify it for your purposes.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="a3671-130">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="a3671-130">Before you begin</span></span>

<span data-ttu-id="a3671-131">Existem algumas coisas que precisa de tooknow e algumas coisas que precisa no local antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="a3671-131">There are a few things you need tooknow and a couple of things that you need in place before you proceed.</span></span>

### <a name="what-tooknow"></a><span data-ttu-id="a3671-132">Que tooknow</span><span class="sxs-lookup"><span data-stu-id="a3671-132">What tooknow</span></span>
<span data-ttu-id="a3671-133">Deve ter uma compreensão operacional das seguintes tecnologias de Olá:</span><span class="sxs-lookup"><span data-stu-id="a3671-133">You should have an operational understanding of hello following technologies:</span></span>

- [<span data-ttu-id="a3671-134">Tecnologias de cluster do Windows</span><span class="sxs-lookup"><span data-stu-id="a3671-134">Windows cluster technologies</span></span>](http://technet.microsoft.com/library/hh831579.aspx)
-  <span data-ttu-id="a3671-135">[Instâncias de Cluster de ativação pós-falha do SQL Server](http://msdn.microsoft.com/library/ms189134.aspx).</span><span class="sxs-lookup"><span data-stu-id="a3671-135">[SQL Server Failover Cluster Instances](http://msdn.microsoft.com/library/ms189134.aspx).</span></span>

<span data-ttu-id="a3671-136">Além disso, deve ter uma compreensão das seguintes tecnologias de Olá geral:</span><span class="sxs-lookup"><span data-stu-id="a3671-136">Also, you should have a general understanding of hello following technologies:</span></span>

- [<span data-ttu-id="a3671-137">Solução convergida Hyper utilizando direta de espaços de armazenamento no Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="a3671-137">Hyper-converged solution using Storage Spaces Direct in Windows Server 2016</span></span>](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct)
- [<span data-ttu-id="a3671-138">Grupos de recursos do Azure</span><span class="sxs-lookup"><span data-stu-id="a3671-138">Azure resource groups</span></span>](../../../azure-resource-manager/resource-group-portal.md)

### <a name="what-toohave"></a><span data-ttu-id="a3671-139">Que toohave</span><span class="sxs-lookup"><span data-stu-id="a3671-139">What toohave</span></span>

<span data-ttu-id="a3671-140">Antes de seguir as instruções de Olá neste artigo, já deverá ter:</span><span class="sxs-lookup"><span data-stu-id="a3671-140">Before following hello instructions in this article, you should already have:</span></span>

- <span data-ttu-id="a3671-141">Uma subscrição do Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="a3671-141">A Microsoft Azure subscription.</span></span>
- <span data-ttu-id="a3671-142">Um domínio do Windows em máquinas virtuais do Azure.</span><span class="sxs-lookup"><span data-stu-id="a3671-142">A Windows domain on Azure virtual machines.</span></span>
- <span data-ttu-id="a3671-143">Uma conta com objetos de toocreate permissão na Olá máquina virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="a3671-143">An account with permission toocreate objects in hello Azure virtual machine.</span></span>
- <span data-ttu-id="a3671-144">Uma rede virtual do Azure e a sub-rede com o espaço de endereços IP suficiente para Olá os seguintes componentes:</span><span class="sxs-lookup"><span data-stu-id="a3671-144">An Azure virtual network and subnet with sufficient IP address space for hello following components:</span></span>
   - <span data-ttu-id="a3671-145">Ambas as máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="a3671-145">Both virtual machines.</span></span>
   - <span data-ttu-id="a3671-146">endereço IP do cluster de ativação pós-falha do Olá.</span><span class="sxs-lookup"><span data-stu-id="a3671-146">hello failover cluster IP address.</span></span>
   - <span data-ttu-id="a3671-147">Um endereço IP para cada FCI.</span><span class="sxs-lookup"><span data-stu-id="a3671-147">An IP address for each FCI.</span></span>
- <span data-ttu-id="a3671-148">DNS configurado no Olá rede do Azure, os controladores de domínio toohello a apontar.</span><span class="sxs-lookup"><span data-stu-id="a3671-148">DNS configured on hello Azure Network, pointing toohello domain controllers.</span></span>

<span data-ttu-id="a3671-149">Com estas pré-requisitos no local, pode continuar com a criação do cluster de ativação pós-falha.</span><span class="sxs-lookup"><span data-stu-id="a3671-149">With these prerequisites in place, you can proceed with building your failover cluster.</span></span> <span data-ttu-id="a3671-150">Step-by-Olá primeiro passo é Olá toocreate máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="a3671-150">hello first step is toocreate hello virtual machines.</span></span>

## <a name="step-1-create-virtual-machines"></a><span data-ttu-id="a3671-151">Passo 1: Criar máquinas virtuais</span><span class="sxs-lookup"><span data-stu-id="a3671-151">Step 1: Create virtual machines</span></span>

1. <span data-ttu-id="a3671-152">Inicie sessão no toohello [portal do Azure](http://portal.azure.com) com a sua subscrição.</span><span class="sxs-lookup"><span data-stu-id="a3671-152">Log in toohello [Azure portal](http://portal.azure.com) with your subscription.</span></span>

1. <span data-ttu-id="a3671-153">[Criar um conjunto de disponibilidade do Azure](../tutorial-availability-sets.md).</span><span class="sxs-lookup"><span data-stu-id="a3671-153">[Create an Azure availability set](../tutorial-availability-sets.md).</span></span>

   <span data-ttu-id="a3671-154">disponibilidade de Olá definir grupos máquinas de virtuais em vários domínios de falhas e domínios de atualização.</span><span class="sxs-lookup"><span data-stu-id="a3671-154">hello availability set groups virtual machines across fault domains and update domains.</span></span> <span data-ttu-id="a3671-155">conjunto de disponibilidade de Olá certifica-se de que a aplicação não é afetada por pontos únicos de falha, como o comutador de rede Olá ou unidade de energia Olá de um bastidor de servidores.</span><span class="sxs-lookup"><span data-stu-id="a3671-155">hello availability set makes sure that your application is not affected by single points of failure, like hello network switch or hello power unit of a rack of servers.</span></span>

   <span data-ttu-id="a3671-156">Se não tiver criado o grupo de recursos de Olá para as máquinas virtuais, fazê-lo ao criar um conjunto de disponibilidade do Azure.</span><span class="sxs-lookup"><span data-stu-id="a3671-156">If you have not created hello resource group for your virtual machines, do it when you create an Azure availability set.</span></span> <span data-ttu-id="a3671-157">Se estiver a utilizar o conjunto de disponibilidade do Olá toocreate portal do Azure Olá, Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="a3671-157">If you're using hello Azure portal toocreate hello availability set, do hello following steps:</span></span>

   - <span data-ttu-id="a3671-158">No portal do Azure Olá, clique em  **+**  tooopen Olá Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="a3671-158">In hello Azure portal, click **+** tooopen hello Azure Marketplace.</span></span> <span data-ttu-id="a3671-159">Procurar **do conjunto de disponibilidade**.</span><span class="sxs-lookup"><span data-stu-id="a3671-159">Search for **Availability set**.</span></span>
   - <span data-ttu-id="a3671-160">Clique em **do conjunto de disponibilidade**.</span><span class="sxs-lookup"><span data-stu-id="a3671-160">Click **Availability set**.</span></span>
   - <span data-ttu-id="a3671-161">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="a3671-161">Click **Create**.</span></span>
   - <span data-ttu-id="a3671-162">No Olá **criar conjunto de disponibilidade** painel, Olá de conjunto de valores a seguir:</span><span class="sxs-lookup"><span data-stu-id="a3671-162">On hello **Create availability set** blade, set hello following values:</span></span>
      - <span data-ttu-id="a3671-163">**Nome**: um nome para o conjunto de disponibilidade de Olá.</span><span class="sxs-lookup"><span data-stu-id="a3671-163">**Name**: A name for hello availability set.</span></span>
      - <span data-ttu-id="a3671-164">**Subscrição**: subscrição do Azure.</span><span class="sxs-lookup"><span data-stu-id="a3671-164">**Subscription**: Your Azure subscription.</span></span>
      - <span data-ttu-id="a3671-165">**Grupo de recursos**: Se pretender toouse um grupo existente, clique em **utilizar existente** e selecione Olá grupo de Olá na lista pendente.</span><span class="sxs-lookup"><span data-stu-id="a3671-165">**Resource group**: If you want toouse an existing group, click **Use existing** and select hello group from hello drop-down list.</span></span> <span data-ttu-id="a3671-166">Caso contrário, escolha **criar novo** e escreva um nome para o grupo de Olá.</span><span class="sxs-lookup"><span data-stu-id="a3671-166">Otherwise choose **Create New** and type a name for hello group.</span></span>
      - <span data-ttu-id="a3671-167">**Localização**: Definir localização do olá onde planeia toocreate as máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="a3671-167">**Location**: Set hello location where you plan toocreate your virtual machines.</span></span>
      - <span data-ttu-id="a3671-168">**Domínios de falha**: utilizar a predefinição de Olá (3).</span><span class="sxs-lookup"><span data-stu-id="a3671-168">**Fault domains**: Use hello default (3).</span></span>
      - <span data-ttu-id="a3671-169">**Domínios de atualização**: utilizar a predefinição de Olá (5).</span><span class="sxs-lookup"><span data-stu-id="a3671-169">**Update domains**: Use hello default (5).</span></span>
   - <span data-ttu-id="a3671-170">Clique em **criar** conjunto de disponibilidade de Olá toocreate.</span><span class="sxs-lookup"><span data-stu-id="a3671-170">Click **Create** toocreate hello availability set.</span></span>

1. <span data-ttu-id="a3671-171">Crie máquinas virtuais Olá no conjunto de disponibilidade de Olá.</span><span class="sxs-lookup"><span data-stu-id="a3671-171">Create hello virtual machines in hello availability set.</span></span>

   <span data-ttu-id="a3671-172">Aprovisione duas máquinas virtuais do SQL Server no conjunto de disponibilidade do Azure Olá.</span><span class="sxs-lookup"><span data-stu-id="a3671-172">Provision two SQL Server virtual machines in hello Azure availability set.</span></span> <span data-ttu-id="a3671-173">Para obter instruções, consulte [aprovisionar uma máquina virtual do SQL Server no portal do Azure de Olá](virtual-machines-windows-portal-sql-server-provision.md).</span><span class="sxs-lookup"><span data-stu-id="a3671-173">For instructions, see [Provision a SQL Server virtual machine in hello Azure portal](virtual-machines-windows-portal-sql-server-provision.md).</span></span>

   <span data-ttu-id="a3671-174">Coloca as duas máquinas virtuais:</span><span class="sxs-lookup"><span data-stu-id="a3671-174">Place both virtual machines:</span></span>

   - <span data-ttu-id="a3671-175">Nas Olá mesmo grupo de recursos do Azure que definir a sua disponibilidade está a ser.</span><span class="sxs-lookup"><span data-stu-id="a3671-175">In hello same Azure resource group that your availability set is in.</span></span>
   - <span data-ttu-id="a3671-176">No Olá mesmo que o controlador de domínio de rede.</span><span class="sxs-lookup"><span data-stu-id="a3671-176">On hello same network as your domain controller.</span></span>
   - <span data-ttu-id="a3671-177">Numa sub-rede com suficiente espaço de endereços IP para máquinas virtuais e todas as FCIs que poderão, eventualmente, utilizar neste cluster.</span><span class="sxs-lookup"><span data-stu-id="a3671-177">On a subnet with sufficient IP address space for both virtual machines, and all FCIs that you may eventually use on this cluster.</span></span>
   - <span data-ttu-id="a3671-178">Olá conjunto de disponibilidade do Azure.</span><span class="sxs-lookup"><span data-stu-id="a3671-178">In hello Azure availability set.</span></span>   

      >[!IMPORTANT]
      ><span data-ttu-id="a3671-179">Não é possível definir ou alterar conjunto depois de criar uma máquina virtual de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="a3671-179">You cannot set or change availability set after a virtual machine has been created.</span></span>

   <span data-ttu-id="a3671-180">Escolha uma imagem do Olá Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="a3671-180">Choose an image from hello Azure Marketplace.</span></span> <span data-ttu-id="a3671-181">Pode utilizar um mercado imagem com o que inclui o Windows Server e SQL Server ou Olá apenas Windows Server.</span><span class="sxs-lookup"><span data-stu-id="a3671-181">You can use a Marketplace image with that includes Windows Server and SQL Server, or just hello Windows Server.</span></span> <span data-ttu-id="a3671-182">Para obter mais informações, consulte [descrição geral do SQL Server em Azure Virtual Machines](../../virtual-machines-windows-sql-server-iaas-overview.md)</span><span class="sxs-lookup"><span data-stu-id="a3671-182">For details, see [Overview of SQL Server on Azure Virtual Machines](../../virtual-machines-windows-sql-server-iaas-overview.md)</span></span>

   <span data-ttu-id="a3671-183">imagens do SQL Server oficiais Olá no Olá galeria do Azure incluem uma instância do SQL Server instalada, plus software de instalação do SQL Server Olá e Olá necessária uma chave.</span><span class="sxs-lookup"><span data-stu-id="a3671-183">hello official SQL Server images in hello Azure Gallery include an installed SQL Server instance, plus hello SQL Server installation software, and hello required key.</span></span>

   <span data-ttu-id="a3671-184">Escolha imagem direita Olá de acordo com toohow que pretende toopay de licença do SQL Server Olá:</span><span class="sxs-lookup"><span data-stu-id="a3671-184">Choose hello right image according toohow you want toopay for hello SQL Server license:</span></span>

   - <span data-ttu-id="a3671-185">**Pagar por utilização licenciamento**: um custo por minuto Olá destas imagens inclui Olá de licenciamento do SQL Server:</span><span class="sxs-lookup"><span data-stu-id="a3671-185">**Pay per usage licensing**: hello per-minute cost of these images includes hello SQL Server licensing:</span></span>
      - <span data-ttu-id="a3671-186">**SQL Server 2016 Enterprise no Datacenter do Windows Server 2016**</span><span class="sxs-lookup"><span data-stu-id="a3671-186">**SQL Server 2016 Enterprise on Windows Server Datacenter 2016**</span></span>
      - <span data-ttu-id="a3671-187">**SQL Server 2016 padrão no Datacenter do Windows Server 2016**</span><span class="sxs-lookup"><span data-stu-id="a3671-187">**SQL Server 2016 Standard on Windows Server Datacenter 2016**</span></span>
      - <span data-ttu-id="a3671-188">**SQL Server 2016 Programador no Datacenter do Windows Server 2016**</span><span class="sxs-lookup"><span data-stu-id="a3671-188">**SQL Server 2016 Developer on Windows Server Datacenter 2016**</span></span>

   - <span data-ttu-id="a3671-189">**Bring-your-proprietário-licença (BYOL)**</span><span class="sxs-lookup"><span data-stu-id="a3671-189">**Bring-your-own-license (BYOL)**</span></span>

      - <span data-ttu-id="a3671-190">**{BYOL} SQL Server 2016 Enterprise no Datacenter do Windows Server 2016**</span><span class="sxs-lookup"><span data-stu-id="a3671-190">**{BYOL} SQL Server 2016 Enterprise on Windows Server Datacenter 2016**</span></span>
      - <span data-ttu-id="a3671-191">**{BYOL} SQL Server 2016 padrão no Datacenter do Windows Server 2016**</span><span class="sxs-lookup"><span data-stu-id="a3671-191">**{BYOL} SQL Server 2016 Standard on Windows Server Datacenter 2016**</span></span>

   >[!IMPORTANT]
   ><span data-ttu-id="a3671-192">Depois de criar a máquina virtual de Olá, remova a instância de SQL Server do Olá autónomo pré-instaladas.</span><span class="sxs-lookup"><span data-stu-id="a3671-192">After you create hello virtual machine, remove hello pre-installed standalone SQL Server instance.</span></span> <span data-ttu-id="a3671-193">Irá utilizar Olá pré-instaladas SQL multimédia toocreate hello do servidor SQL Server FCI depois de configurar o cluster de ativação pós-falha Olá e S2D.</span><span class="sxs-lookup"><span data-stu-id="a3671-193">You will use hello pre-installed SQL Server media toocreate hello SQL Server FCI after you configure hello failover cluster and S2D.</span></span>

   <span data-ttu-id="a3671-194">Em alternativa, pode utilizar imagens do Azure Marketplace com sistema de operativo apenas Olá.</span><span class="sxs-lookup"><span data-stu-id="a3671-194">Alternatively, you can use Azure Marketplace images with just hello operating system.</span></span> <span data-ttu-id="a3671-195">Escolha um **Datacenter do Windows Server 2016** imagem e instalar Olá SQL Server FCI depois de configurar o cluster de ativação pós-falha Olá e S2D.</span><span class="sxs-lookup"><span data-stu-id="a3671-195">Choose a **Windows Server 2016 Datacenter** image and install hello SQL Server FCI after you configure hello failover cluster and S2D.</span></span> <span data-ttu-id="a3671-196">Esta imagem não contém suporte de instalação do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="a3671-196">This image does not contain SQL Server installation media.</span></span> <span data-ttu-id="a3671-197">Coloque o suporte de dados de instalação de Olá numa localização onde é possível executar a instalação do SQL Server Olá para cada servidor.</span><span class="sxs-lookup"><span data-stu-id="a3671-197">Place hello installation media in a location where you can run hello SQL Server installation for each server.</span></span>

1. <span data-ttu-id="a3671-198">Depois do Azure cria as máquinas virtuais, ligar máquinas de virtuais tooeach com RDP.</span><span class="sxs-lookup"><span data-stu-id="a3671-198">After Azure creates your virtual machines, connect tooeach virtual machine with RDP.</span></span>

   <span data-ttu-id="a3671-199">Quando liga pela primeira vez tooa máquinas com RDP, o computador de Olá pede-lhe se pretende tooallow toobe este PC detetável na rede de Olá.</span><span class="sxs-lookup"><span data-stu-id="a3671-199">When you first connect tooa virtual machine with RDP, hello computer asks if you want tooallow this PC toobe discoverable on hello network.</span></span> <span data-ttu-id="a3671-200">Clique em **Sim**.</span><span class="sxs-lookup"><span data-stu-id="a3671-200">Click **Yes**.</span></span>

1. <span data-ttu-id="a3671-201">Se estiver a utilizar uma das imagens da máquina virtual baseada no SQL Server de Olá, remova a instância do SQL Server de Olá.</span><span class="sxs-lookup"><span data-stu-id="a3671-201">If you are using one of hello SQL Server-based virtual machine images, remove hello SQL Server instance.</span></span>

   - <span data-ttu-id="a3671-202">No **programas e funcionalidades**, faça duplo clique **Microsoft SQL Server 2016 (64-bit)** e clique em **desinstalar/alterar**.</span><span class="sxs-lookup"><span data-stu-id="a3671-202">In **Programs and Features**, right-click **Microsoft SQL Server 2016 (64-bit)** and click **Uninstall/Change**.</span></span>
   - <span data-ttu-id="a3671-203">Clique em **remover**.</span><span class="sxs-lookup"><span data-stu-id="a3671-203">Click **Remove**.</span></span>
   - <span data-ttu-id="a3671-204">Selecione a instância predefinida de Olá.</span><span class="sxs-lookup"><span data-stu-id="a3671-204">Select hello default instance.</span></span>
   - <span data-ttu-id="a3671-205">Remova todas as funcionalidades em **serviços de motor de base de dados**.</span><span class="sxs-lookup"><span data-stu-id="a3671-205">Remove all features under **Database Engine Services**.</span></span> <span data-ttu-id="a3671-206">Não remova **partilhado funcionalidades**.</span><span class="sxs-lookup"><span data-stu-id="a3671-206">Do not remove **Shared Features**.</span></span> <span data-ttu-id="a3671-207">Consulte Olá seguinte imagem:</span><span class="sxs-lookup"><span data-stu-id="a3671-207">See hello following picture:</span></span>

      ![Remover funcionalidades](./media/virtual-machines-windows-portal-sql-create-failover-cluster/03-remove-features.png)

   - <span data-ttu-id="a3671-209">Clique em **seguinte**e, em seguida, clique em **remover**.</span><span class="sxs-lookup"><span data-stu-id="a3671-209">Click **Next**, and then click **Remove**.</span></span>

1. <span data-ttu-id="a3671-210"><a name="ports"></a>Abrir portas de firewall de Olá.</span><span class="sxs-lookup"><span data-stu-id="a3671-210"><a name="ports"></a>Open hello firewall ports.</span></span>

   <span data-ttu-id="a3671-211">Em cada máquina virtual, abra Olá seguindo as portas do Olá Firewall do Windows.</span><span class="sxs-lookup"><span data-stu-id="a3671-211">On each virtual machine, open hello following ports on hello Windows Firewall.</span></span>

   | <span data-ttu-id="a3671-212">Objetivo</span><span class="sxs-lookup"><span data-stu-id="a3671-212">Purpose</span></span> | <span data-ttu-id="a3671-213">A porta TCP</span><span class="sxs-lookup"><span data-stu-id="a3671-213">TCP Port</span></span> | <span data-ttu-id="a3671-214">Notas</span><span class="sxs-lookup"><span data-stu-id="a3671-214">Notes</span></span>
   | ------ | ------ | ------
   | <span data-ttu-id="a3671-215">SQL Server</span><span class="sxs-lookup"><span data-stu-id="a3671-215">SQL Server</span></span> | <span data-ttu-id="a3671-216">1433</span><span class="sxs-lookup"><span data-stu-id="a3671-216">1433</span></span> | <span data-ttu-id="a3671-217">Porta normal para instâncias predefinida do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="a3671-217">Normal port for default instances of SQL Server.</span></span> <span data-ttu-id="a3671-218">Se utilizou uma imagem da Galeria de Olá, esta porta é automaticamente aberta.</span><span class="sxs-lookup"><span data-stu-id="a3671-218">If you used an image from hello gallery, this port is automatically opened.</span></span>
   | <span data-ttu-id="a3671-219">Sonda de estado de funcionamento</span><span class="sxs-lookup"><span data-stu-id="a3671-219">Health probe</span></span> | <span data-ttu-id="a3671-220">59999</span><span class="sxs-lookup"><span data-stu-id="a3671-220">59999</span></span> | <span data-ttu-id="a3671-221">Abra qualquer porta TCP.</span><span class="sxs-lookup"><span data-stu-id="a3671-221">Any open TCP port.</span></span> <span data-ttu-id="a3671-222">Num passo posterior, configure o Balanceador de carga Olá [sonda do Estado de funcionamento](#probe) e Olá cluster toouse esta porta.</span><span class="sxs-lookup"><span data-stu-id="a3671-222">In a later step, configure hello load balancer [health probe](#probe) and hello cluster toouse this port.</span></span>  

1. <span data-ttu-id="a3671-223">Adicione armazenamento toohello máquina.</span><span class="sxs-lookup"><span data-stu-id="a3671-223">Add storage toohello virtual machine.</span></span> <span data-ttu-id="a3671-224">Para obter informações detalhadas, consulte [adicionar armazenamento](../../../storage/common/storage-premium-storage.md).</span><span class="sxs-lookup"><span data-stu-id="a3671-224">For detailed information, see [add storage](../../../storage/common/storage-premium-storage.md).</span></span>

   <span data-ttu-id="a3671-225">Ambas as máquinas virtuais precisa de discos de dados, pelo menos, dois.</span><span class="sxs-lookup"><span data-stu-id="a3671-225">Both virtual machines need at least two data disks.</span></span>

   <span data-ttu-id="a3671-226">Anexe discos em bruto - não NTFS formatado discos.</span><span class="sxs-lookup"><span data-stu-id="a3671-226">Attach raw disks - not NTFS formatted disks.</span></span>
      >[!NOTE]
      ><span data-ttu-id="a3671-227">Se anexar formatada com NTFS discos, só pode ativar S2D com verificação de elegibilidade sem disco.</span><span class="sxs-lookup"><span data-stu-id="a3671-227">If you attach NTFS-formatted disks, you can only enable S2D with no disk eligibility check.</span></span>  

   <span data-ttu-id="a3671-228">Anexe um mínimo de dois Premium Storage (discos SSD) tooeach VM.</span><span class="sxs-lookup"><span data-stu-id="a3671-228">Attach a minimum of two Premium Storage (SSD disks) tooeach VM.</span></span> <span data-ttu-id="a3671-229">Recomendamos que, pelo menos, P30 discos (1 TB).</span><span class="sxs-lookup"><span data-stu-id="a3671-229">We recommend at least P30 (1 TB) disks.</span></span>

   <span data-ttu-id="a3671-230">Anfitrião de conjunto de colocação em cache demasiado**só de leitura**.</span><span class="sxs-lookup"><span data-stu-id="a3671-230">Set host caching too**Read-only**.</span></span>

   <span data-ttu-id="a3671-231">capacidade de armazenamento de Olá que utilizar em ambientes de produção depende da sua carga de trabalho.</span><span class="sxs-lookup"><span data-stu-id="a3671-231">hello storage capacity you use in production environments depends on your workload.</span></span> <span data-ttu-id="a3671-232">os valores de Olá descritos neste artigo são de demonstração e teste.</span><span class="sxs-lookup"><span data-stu-id="a3671-232">hello values described in this article are for demonstration and testing.</span></span>

1. <span data-ttu-id="a3671-233">[Adicionar Olá máquinas virtuais tooyour pré-existente domínio](virtual-machines-windows-portal-sql-availability-group-prereq.md#joinDomain).</span><span class="sxs-lookup"><span data-stu-id="a3671-233">[Add hello virtual machines tooyour pre-existing domain](virtual-machines-windows-portal-sql-availability-group-prereq.md#joinDomain).</span></span>

<span data-ttu-id="a3671-234">Depois de Olá máquinas de virtuais são criadas e configuradas, pode configurar o cluster de ativação pós-falha Olá.</span><span class="sxs-lookup"><span data-stu-id="a3671-234">After hello virtual machines are created and configured, you can configure hello failover cluster.</span></span>

## <a name="step-2-configure-hello-windows-failover-cluster-with-s2d"></a><span data-ttu-id="a3671-235">Passo 2: Configurar Olá Cluster de ativação pós-falha do Windows com S2D</span><span class="sxs-lookup"><span data-stu-id="a3671-235">Step 2: Configure hello Windows Failover Cluster with S2D</span></span>

<span data-ttu-id="a3671-236">Olá passo seguinte consiste em cluster de ativação pós-falha de Olá tooconfigure com S2D.</span><span class="sxs-lookup"><span data-stu-id="a3671-236">hello next step is tooconfigure hello failover cluster with S2D.</span></span> <span data-ttu-id="a3671-237">Neste passo, irá fazer Olá seguintes substeps:</span><span class="sxs-lookup"><span data-stu-id="a3671-237">In this step, you will do hello following substeps:</span></span>

1. <span data-ttu-id="a3671-238">Adicionar a funcionalidade de Clustering de ativação pós-falha do Windows</span><span class="sxs-lookup"><span data-stu-id="a3671-238">Add Windows Failover Clustering feature</span></span>
1. <span data-ttu-id="a3671-239">Validar cluster Olá</span><span class="sxs-lookup"><span data-stu-id="a3671-239">Validate hello cluster</span></span>
1. <span data-ttu-id="a3671-240">Criar cluster de ativação pós-falha de Olá</span><span class="sxs-lookup"><span data-stu-id="a3671-240">Create hello failover cluster</span></span>
1. <span data-ttu-id="a3671-241">Criar o testemunho de nuvem Olá</span><span class="sxs-lookup"><span data-stu-id="a3671-241">Create hello cloud witness</span></span>
1. <span data-ttu-id="a3671-242">Adicionar armazenamento</span><span class="sxs-lookup"><span data-stu-id="a3671-242">Add storage</span></span>

### <a name="add-windows-failover-clustering-feature"></a><span data-ttu-id="a3671-243">Adicionar a funcionalidade de Clustering de ativação pós-falha do Windows</span><span class="sxs-lookup"><span data-stu-id="a3671-243">Add Windows Failover Clustering feature</span></span>

1. <span data-ttu-id="a3671-244">toobegin, ligar toohello primeira máquina de virtual com RDP utilizando uma conta de domínio que é um membro dos administradores locais e tem objetos de toocreate permissões no Active Directory.</span><span class="sxs-lookup"><span data-stu-id="a3671-244">toobegin, connect toohello first virtual machine with RDP using a domain account that is a member of local administrators, and has permissions toocreate objects in Active Directory.</span></span> <span data-ttu-id="a3671-245">Utilize esta conta para o resto Olá configuração Olá.</span><span class="sxs-lookup"><span data-stu-id="a3671-245">Use this account for hello rest of hello configuration.</span></span>

1. <span data-ttu-id="a3671-246">[Adicionar a máquina virtual do tooeach funcionalidade Clustering de ativação pós-falha](virtual-machines-windows-portal-sql-availability-group-prereq.md#add-failover-clustering-features-to-both-sql-server-vms).</span><span class="sxs-lookup"><span data-stu-id="a3671-246">[Add Failover Clustering feature tooeach virtual machine](virtual-machines-windows-portal-sql-availability-group-prereq.md#add-failover-clustering-features-to-both-sql-server-vms).</span></span>

   <span data-ttu-id="a3671-247">funcionalidade de Clustering de ativação pós-falha tooinstall de Olá IU, Olá os seguintes passos em ambas as máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="a3671-247">tooinstall Failover Clustering feature from hello UI, do hello following steps on both virtual machines.</span></span>
   - <span data-ttu-id="a3671-248">No **Gestor de servidor**, clique em **gerir**e, em seguida, clique em **para adicionar funções e funcionalidades**.</span><span class="sxs-lookup"><span data-stu-id="a3671-248">In **Server Manager**, click **Manage**, and then click **Add Roles and Features**.</span></span>
   - <span data-ttu-id="a3671-249">No **Assistente Adicionar funções e funcionalidades**, clique em **seguinte** quando obtiver demasiado**selecionar funcionalidades**.</span><span class="sxs-lookup"><span data-stu-id="a3671-249">In **Add Roles and Features Wizard**, click **Next** until you get too**Select Features**.</span></span>
   - <span data-ttu-id="a3671-250">No **selecionar funcionalidades**, clique em **Clustering de ativação pós-falha**.</span><span class="sxs-lookup"><span data-stu-id="a3671-250">In **Select Features**, click **Failover Clustering**.</span></span> <span data-ttu-id="a3671-251">Inclua todas as funcionalidades necessárias e ferramentas de gestão de Olá.</span><span class="sxs-lookup"><span data-stu-id="a3671-251">Include all required features and hello management tools.</span></span> <span data-ttu-id="a3671-252">Clique em **adicionar funcionalidades**.</span><span class="sxs-lookup"><span data-stu-id="a3671-252">Click **Add Features**.</span></span>
   - <span data-ttu-id="a3671-253">Clique em **seguinte** e, em seguida, clique em **concluir** funcionalidades de Olá tooinstall.</span><span class="sxs-lookup"><span data-stu-id="a3671-253">Click **Next** and then click **Finish** tooinstall hello features.</span></span>

   <span data-ttu-id="a3671-254">tooinstall Olá Clustering de ativação pós-falha funcionalidade com o PowerShell, execute Olá seguinte script a partir de uma sessão do PowerShell de administrador dos Olá máquinas de virtuais.</span><span class="sxs-lookup"><span data-stu-id="a3671-254">tooinstall hello Failover Clustering feature with PowerShell, run hello following script from an administrator PowerShell session on one of hello virtual machines.</span></span>

   ```PowerShell
   $nodes = ("<node1>","<node2>")
   Invoke-Command  $nodes {Install-WindowsFeature Failover-Clustering -IncludeAllSubFeature -IncludeManagementTools}
   ```

<span data-ttu-id="a3671-255">Para referência, passos Olá Siga instruções de Olá no passo 3 de [convergida Hyper solução utilizando direta de espaços de armazenamento no Windows Server 2016](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-3-configure-storage-spaces-direct).</span><span class="sxs-lookup"><span data-stu-id="a3671-255">For reference, hello next steps follow hello instructions under Step 3 of [Hyper-converged solution using Storage Spaces Direct in Windows Server 2016](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-3-configure-storage-spaces-direct).</span></span>

### <a name="validate-hello-cluster"></a><span data-ttu-id="a3671-256">Validar cluster Olá</span><span class="sxs-lookup"><span data-stu-id="a3671-256">Validate hello cluster</span></span>

<span data-ttu-id="a3671-257">Este guia refere-se tooinstructions em [validar cluster](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-31-run-cluster-validation).</span><span class="sxs-lookup"><span data-stu-id="a3671-257">This guide refers tooinstructions under [validate cluster](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-31-run-cluster-validation).</span></span>

<span data-ttu-id="a3671-258">Valide cluster Olá Olá IU ou com o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a3671-258">Validate hello cluster in hello UI or with PowerShell.</span></span>

<span data-ttu-id="a3671-259">cluster de Olá toovalidate com Olá IU, Olá seguindo os passos de uma das máquinas virtuais Olá.</span><span class="sxs-lookup"><span data-stu-id="a3671-259">toovalidate hello cluster with hello UI, do hello following steps from one of hello virtual machines.</span></span>

1. <span data-ttu-id="a3671-260">No **Gestor de servidor**, clique em **ferramentas**, em seguida, clique em **Gestor de clusters de ativação pós-falha**.</span><span class="sxs-lookup"><span data-stu-id="a3671-260">In **Server Manager**, click **Tools**, then click **Failover Cluster Manager**.</span></span>
1. <span data-ttu-id="a3671-261">No **Gestor de clusters de ativação pós-falha**, clique em **ação**, em seguida, clique em **validar configuração...** .</span><span class="sxs-lookup"><span data-stu-id="a3671-261">In **Failover Cluster Manager**, click **Action**, then click **Validate Configuration...**.</span></span>
1. <span data-ttu-id="a3671-262">Clique em **Seguinte**.</span><span class="sxs-lookup"><span data-stu-id="a3671-262">Click **Next**.</span></span>
1. <span data-ttu-id="a3671-263">No **selecionar servidores ou um Cluster**, nome do tipo Olá de ambas as máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="a3671-263">On **Select Servers or a Cluster**, type hello name of both virtual machines.</span></span>
1. <span data-ttu-id="a3671-264">No **opções de teste**, escolha **executar apenas os testes selecionados**.</span><span class="sxs-lookup"><span data-stu-id="a3671-264">On **Testing options**, choose **Run only tests I select**.</span></span> <span data-ttu-id="a3671-265">Clique em **Seguinte**.</span><span class="sxs-lookup"><span data-stu-id="a3671-265">Click **Next**.</span></span>
1. <span data-ttu-id="a3671-266">No **testar seleção**, incluir todos os testes, exceto **armazenamento**.</span><span class="sxs-lookup"><span data-stu-id="a3671-266">On **Test selection**, include all tests except **Storage**.</span></span> <span data-ttu-id="a3671-267">Consulte Olá seguinte imagem:</span><span class="sxs-lookup"><span data-stu-id="a3671-267">See hello following picture:</span></span>

   ![Validar testes](./media/virtual-machines-windows-portal-sql-create-failover-cluster/10-validate-cluster-test.png)

1. <span data-ttu-id="a3671-269">Clique em **Seguinte**.</span><span class="sxs-lookup"><span data-stu-id="a3671-269">Click **Next**.</span></span>
1. <span data-ttu-id="a3671-270">No **confirmação**, clique em **seguinte**.</span><span class="sxs-lookup"><span data-stu-id="a3671-270">On **Confirmation**, click **Next**.</span></span>

<span data-ttu-id="a3671-271">Olá **validar um Assistente de configuração** executa Olá testes de validação.</span><span class="sxs-lookup"><span data-stu-id="a3671-271">hello **Validate a Configuration Wizard** runs hello validation tests.</span></span>

<span data-ttu-id="a3671-272">cluster de Olá toovalidate com o PowerShell, execute Olá seguinte script a partir de uma sessão do PowerShell de administrador dos Olá máquinas de virtuais.</span><span class="sxs-lookup"><span data-stu-id="a3671-272">toovalidate hello cluster with PowerShell, run hello following script from an administrator PowerShell session on one of hello virtual machines.</span></span>

   ```PowerShell
   Test-Cluster –Node ("<node1>","<node2>") –Include "Storage Spaces Direct", "Inventory", "Network", "System Configuration"
   ```

<span data-ttu-id="a3671-273">Depois de validar cluster Olá, crie o cluster de ativação pós-falha de Olá.</span><span class="sxs-lookup"><span data-stu-id="a3671-273">After you validate hello cluster, create hello failover cluster.</span></span>

### <a name="create-hello-failover-cluster"></a><span data-ttu-id="a3671-274">Criar cluster de ativação pós-falha de Olá</span><span class="sxs-lookup"><span data-stu-id="a3671-274">Create hello failover cluster</span></span>

<span data-ttu-id="a3671-275">Este guia refere-se demasiado[Criar cluster de ativação pós-falha de Olá](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-32-create-a-cluster).</span><span class="sxs-lookup"><span data-stu-id="a3671-275">This guide refers too[Create hello failover cluster](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-32-create-a-cluster).</span></span>

<span data-ttu-id="a3671-276">cluster de ativação pós-falha do toocreate Olá, tem de:</span><span class="sxs-lookup"><span data-stu-id="a3671-276">toocreate hello failover cluster, you need:</span></span>
- <span data-ttu-id="a3671-277">nomes de Olá das máquinas virtuais Olá que fique Olá nós de cluster.</span><span class="sxs-lookup"><span data-stu-id="a3671-277">hello names of hello virtual machines that become hello cluster nodes.</span></span>
- <span data-ttu-id="a3671-278">Um nome para o cluster de ativação pós-falha Olá</span><span class="sxs-lookup"><span data-stu-id="a3671-278">A name for hello failover cluster</span></span>
- <span data-ttu-id="a3671-279">Um endereço IP para o cluster de ativação pós-falha de Olá.</span><span class="sxs-lookup"><span data-stu-id="a3671-279">An IP address for hello failover cluster.</span></span> <span data-ttu-id="a3671-280">Pode utilizar um endereço IP que não seja utilizado Olá mesma rede virtual do Azure e como Olá nós de cluster.</span><span class="sxs-lookup"><span data-stu-id="a3671-280">You can use an IP address that is not used on hello same Azure virtual network and subnet as hello cluster nodes.</span></span>

<span data-ttu-id="a3671-281">Olá PowerShell a seguir cria um cluster de ativação pós-falha.</span><span class="sxs-lookup"><span data-stu-id="a3671-281">hello following PowerShell creates a failover cluster.</span></span> <span data-ttu-id="a3671-282">Atualizar o script de Olá com nomes de Olá de nós de Olá (nomes de máquina virtual Olá) e um endereço IP disponível do Olá VNET do Azure:</span><span class="sxs-lookup"><span data-stu-id="a3671-282">Update hello script with hello names of hello nodes (hello virtual machine names) and an available IP address from hello Azure VNET:</span></span>

```PowerShell
New-Cluster -Name <FailoverCluster-Name> -Node ("<node1>","<node2>") –StaticAddress <n.n.n.n> -NoStorage
```   

### <a name="create-a-cloud-witness"></a><span data-ttu-id="a3671-283">Criar um testemunho de nuvem</span><span class="sxs-lookup"><span data-stu-id="a3671-283">Create a cloud witness</span></span>

<span data-ttu-id="a3671-284">Testemunho de nuvem é um novo tipo de testemunho de quórum do cluster armazenado num Blob de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="a3671-284">Cloud Witness is a new type of cluster quorum witness stored in an Azure Storage Blob.</span></span> <span data-ttu-id="a3671-285">Esta ação remove a necessidade de Olá de uma VM separada que aloja uma partilha de testemunho.</span><span class="sxs-lookup"><span data-stu-id="a3671-285">This removes hello need of a separate VM hosting a witness share.</span></span>

1. <span data-ttu-id="a3671-286">[Criar um testemunho de nuvem para o cluster de ativação pós-falha de Olá](http://technet.microsoft.com/windows-server-docs/failover-clustering/deploy-cloud-witness).</span><span class="sxs-lookup"><span data-stu-id="a3671-286">[Create a cloud witness for hello failover cluster](http://technet.microsoft.com/windows-server-docs/failover-clustering/deploy-cloud-witness).</span></span>

1. <span data-ttu-id="a3671-287">Crie um contentor de blob.</span><span class="sxs-lookup"><span data-stu-id="a3671-287">Create a blob container.</span></span>

1. <span data-ttu-id="a3671-288">Guarde as chaves de acesso de Olá e o URL do contentor Olá.</span><span class="sxs-lookup"><span data-stu-id="a3671-288">Save hello access keys and hello container URL.</span></span>

1. <span data-ttu-id="a3671-289">Configure o testemunho de quórum de cluster de cluster de ativação pós-falha de Olá.</span><span class="sxs-lookup"><span data-stu-id="a3671-289">Configure hello failover cluster cluster quorum witness.</span></span> <span data-ttu-id="a3671-290">Ver, [configurar testemunho de quórum de Olá na interface de utilizador Olá]. (http://technet.microsoft.com/windows-server-docs/failover-clustering/deploy-cloud-witness#to-configure-cloud-witness-as-a-quorum-witness) no Olá IU.</span><span class="sxs-lookup"><span data-stu-id="a3671-290">See, [Configure hello quorum witness in hello user interface].(http://technet.microsoft.com/windows-server-docs/failover-clustering/deploy-cloud-witness#to-configure-cloud-witness-as-a-quorum-witness) in hello UI.</span></span>

### <a name="add-storage"></a><span data-ttu-id="a3671-291">Adicionar armazenamento</span><span class="sxs-lookup"><span data-stu-id="a3671-291">Add storage</span></span>

<span data-ttu-id="a3671-292">discos Olá S2D necessário toobe vazio e sem partições ou outros dados.</span><span class="sxs-lookup"><span data-stu-id="a3671-292">hello disks for S2D need toobe empty and without partitions or other data.</span></span> <span data-ttu-id="a3671-293">Siga tooclean discos [Olá passos neste guia](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-34-clean-disks).</span><span class="sxs-lookup"><span data-stu-id="a3671-293">tooclean disks follow [hello steps in this guide](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-34-clean-disks).</span></span>

1. <span data-ttu-id="a3671-294">[Ativar loja direta de espaços \(S2D\)](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-35-enable-storage-spaces-direct).</span><span class="sxs-lookup"><span data-stu-id="a3671-294">[Enable Store Spaces Direct \(S2D\)](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-35-enable-storage-spaces-direct).</span></span>

   <span data-ttu-id="a3671-295">Olá seguir PowerShell permite direta de espaços de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="a3671-295">hello following PowerShell enables storage spaces direct.</span></span>  

   ```PowerShell
   Enable-ClusterS2D
   ```

   <span data-ttu-id="a3671-296">No **Gestor de clusters de ativação pós-falha**, agora, pode ver o agrupamento de armazenamento Olá.</span><span class="sxs-lookup"><span data-stu-id="a3671-296">In **Failover Cluster Manager**, you can now see hello storage pool.</span></span>

1. <span data-ttu-id="a3671-297">[Criar um volume](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-36-create-volumes).</span><span class="sxs-lookup"><span data-stu-id="a3671-297">[Create a volume](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-36-create-volumes).</span></span>

   <span data-ttu-id="a3671-298">Uma das funcionalidades de Olá de S2D é que este cria automaticamente um agrupamento de armazenamento se a ativar.</span><span class="sxs-lookup"><span data-stu-id="a3671-298">One of hello features of S2D is that it automatically creates a storage pool when you enable it.</span></span> <span data-ttu-id="a3671-299">Agora, está pronto toocreate um volume.</span><span class="sxs-lookup"><span data-stu-id="a3671-299">You are now ready toocreate a volume.</span></span> <span data-ttu-id="a3671-300">Olá PowerShell commandlet `New-Volume` automatiza o processo de criação do volume Olá, incluindo formatação, adicionar toohello cluster e criar um volume partilhado de cluster (CSV).</span><span class="sxs-lookup"><span data-stu-id="a3671-300">hello PowerShell commandlet `New-Volume` automates hello volume creation process, including formatting, adding toohello cluster, and creating a cluster shared volume (CSV).</span></span> <span data-ttu-id="a3671-301">Olá seguinte exemplo cria um 800 gigabyte (GB) CSV.</span><span class="sxs-lookup"><span data-stu-id="a3671-301">hello following example creates an 800 gigabyte (GB) CSV.</span></span>

   ```PowerShell
   New-Volume -StoragePoolFriendlyName S2D* -FriendlyName VDisk01 -FileSystem CSVFS_REFS -Size 800GB
   ```   

   <span data-ttu-id="a3671-302">Depois de concluída este comando, um volume de 800 GB está montado como um recurso de cluster.</span><span class="sxs-lookup"><span data-stu-id="a3671-302">After this command completes, an 800 GB volume is mounted as a cluster resource.</span></span> <span data-ttu-id="a3671-303">é volume Olá `C:\ClusterStorage\Volume1\`.</span><span class="sxs-lookup"><span data-stu-id="a3671-303">hello volume is at `C:\ClusterStorage\Volume1\`.</span></span>

   <span data-ttu-id="a3671-304">Olá diagrama a seguir mostra um volume partilhado de cluster com S2D:</span><span class="sxs-lookup"><span data-stu-id="a3671-304">hello following diagram shows a cluster shared volume with S2D:</span></span>

   ![ClusterSharedVolume](./media/virtual-machines-windows-portal-sql-create-failover-cluster/15-cluster-shared-volume.png)

## <a name="step-3-test-failover-cluster-failover"></a><span data-ttu-id="a3671-306">Passo 3: Testar a ativação pós-falha de cluster de ativação pós-falha</span><span class="sxs-lookup"><span data-stu-id="a3671-306">Step 3: Test failover cluster failover</span></span>

<span data-ttu-id="a3671-307">No Gestor de clusters de ativação pós-falha, certifique-se de que é possível mover toohello de recursos de armazenamento Olá outro nó de cluster.</span><span class="sxs-lookup"><span data-stu-id="a3671-307">In Failover Cluster Manager, verify that you can move hello storage resource toohello other cluster node.</span></span> <span data-ttu-id="a3671-308">Se pode ligar cluster de ativação pós-falha de toohello com **Gestor de clusters de ativação pós-falha** e mover o armazenamento de Olá de um nó toohello outros, está pronto tooconfigure Olá FCI.</span><span class="sxs-lookup"><span data-stu-id="a3671-308">If you can connect toohello failover cluster with **Failover Cluster Manager** and move hello storage from one node toohello other, you are ready tooconfigure hello FCI.</span></span>

## <a name="step-4-create-sql-server-fci"></a><span data-ttu-id="a3671-309">Passo 4: Criar do SQL Server FCI</span><span class="sxs-lookup"><span data-stu-id="a3671-309">Step 4: Create SQL Server FCI</span></span>

<span data-ttu-id="a3671-310">Depois de ter configurado o cluster de ativação pós-falha de Olá e todos os componentes de cluster, incluindo o armazenamento, pode criar Olá SQL Server FCI.</span><span class="sxs-lookup"><span data-stu-id="a3671-310">After you have configured hello failover cluster and all cluster components including storage, you can create hello SQL Server FCI.</span></span>

1. <span data-ttu-id="a3671-311">Ligar toohello primeira máquina de virtual com RDP.</span><span class="sxs-lookup"><span data-stu-id="a3671-311">Connect toohello first virtual machine with RDP.</span></span>

1. <span data-ttu-id="a3671-312">No **Gestor de clusters de ativação pós-falha**, certifique-se todos os recursos principais do cluster estão na máquina de virtual primeiro Olá.</span><span class="sxs-lookup"><span data-stu-id="a3671-312">In **Failover Cluster Manager**, make sure all cluster core resources are on hello first virtual machine.</span></span> <span data-ttu-id="a3671-313">Se necessário, mova todas as máquinas de toothis recursos.</span><span class="sxs-lookup"><span data-stu-id="a3671-313">If necessary, move all resources toothis virtual machine.</span></span>

1. <span data-ttu-id="a3671-314">Localize o suporte de dados de instalação de Olá.</span><span class="sxs-lookup"><span data-stu-id="a3671-314">Locate hello installation media.</span></span> <span data-ttu-id="a3671-315">Se a máquina virtual de Olá utiliza uma das imagens de Azure Marketplace Olá, suporte de dados de Olá está localizado em `C:\SQLServer_<version number>_Full`.</span><span class="sxs-lookup"><span data-stu-id="a3671-315">If hello virtual machine uses one of hello Azure Marketplace images, hello media is located at `C:\SQLServer_<version number>_Full`.</span></span> <span data-ttu-id="a3671-316">Clique em **configuração**.</span><span class="sxs-lookup"><span data-stu-id="a3671-316">Click **Setup**.</span></span>

1. <span data-ttu-id="a3671-317">No Olá **Centro de instalação do SQL Server**, clique em **instalação**.</span><span class="sxs-lookup"><span data-stu-id="a3671-317">In hello **SQL Server Installation Center**, click **Installation**.</span></span>

1. <span data-ttu-id="a3671-318">Clique em **instalação de cluster de ativação pós-falha do novo SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="a3671-318">Click **New SQL Server failover cluster installation**.</span></span> <span data-ttu-id="a3671-319">Siga as instruções de Olá Olá de tooinstall Olá assistente SQL Server FCI.</span><span class="sxs-lookup"><span data-stu-id="a3671-319">Follow hello instructions in hello wizard tooinstall hello SQL Server FCI.</span></span>

   <span data-ttu-id="a3671-320">diretórios de dados FCI Olá necessário toobe no armazenamento em cluster.</span><span class="sxs-lookup"><span data-stu-id="a3671-320">hello FCI data directories need toobe on clustered storage.</span></span> <span data-ttu-id="a3671-321">Com S2D, não é um disco partilhado, mas um volume de tooa de ponto de montagem em cada servidor.</span><span class="sxs-lookup"><span data-stu-id="a3671-321">With S2D, it's not a shared disk, but a mount point tooa volume on each server.</span></span> <span data-ttu-id="a3671-322">S2D sincroniza volume Olá entre ambos os nós.</span><span class="sxs-lookup"><span data-stu-id="a3671-322">S2D synchronizes hello volume between both nodes.</span></span> <span data-ttu-id="a3671-323">volume de Olá é apresentada toohello cluster como volume partilhado de cluster.</span><span class="sxs-lookup"><span data-stu-id="a3671-323">hello volume is presented toohello cluster as a cluster shared volume.</span></span> <span data-ttu-id="a3671-324">Utilize o ponto de montagem CSV Olá para diretórios de dados de Olá.</span><span class="sxs-lookup"><span data-stu-id="a3671-324">Use hello CSV mount point for hello data directories.</span></span>

   ![DataDirectories](./media/virtual-machines-windows-portal-sql-create-failover-cluster/20-data-dicrectories.png)

1. <span data-ttu-id="a3671-326">Depois de concluir o Assistente de Olá, a configuração irá instalar um FCI do SQL Server no primeiro nó de Olá.</span><span class="sxs-lookup"><span data-stu-id="a3671-326">After you complete hello wizard, Setup will install a SQL Server FCI on hello first node.</span></span>

1. <span data-ttu-id="a3671-327">Depois do programa de configuração instala com êxito Olá FCI no primeiro nó de Olá, ligar toohello segundo nó com RDP.</span><span class="sxs-lookup"><span data-stu-id="a3671-327">After Setup successfully installs hello FCI on hello first node, connect toohello second node with RDP.</span></span>

1. <span data-ttu-id="a3671-328">Abra Olá **Centro de instalação do SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="a3671-328">Open hello **SQL Server Installation Center**.</span></span> <span data-ttu-id="a3671-329">Clique em **instalação**.</span><span class="sxs-lookup"><span data-stu-id="a3671-329">Click **Installation**.</span></span>

1. <span data-ttu-id="a3671-330">Clique em **cluster de ativação pós-falha do SQL Server do adicionar nó tooa**.</span><span class="sxs-lookup"><span data-stu-id="a3671-330">Click **Add node tooa SQL Server failover cluster**.</span></span> <span data-ttu-id="a3671-331">Siga as instruções de Olá no SQL server do Olá assistente tooinstall e adicione toohello este servidor FCI.</span><span class="sxs-lookup"><span data-stu-id="a3671-331">Follow hello instructions in hello wizard tooinstall SQL server and add this server toohello FCI.</span></span>

   >[!NOTE]
   ><span data-ttu-id="a3671-332">Se utilizou uma imagem de galeria do Azure Marketplace com o SQL Server, ferramentas do SQL Server foram incluídas com Olá imagem.</span><span class="sxs-lookup"><span data-stu-id="a3671-332">If you used an Azure Marketplace gallery image with SQL Server, SQL Server tools were included with hello image.</span></span> <span data-ttu-id="a3671-333">Se não utilizou esta imagem, instale o ferramentas do SQL Server de Olá separadamente.</span><span class="sxs-lookup"><span data-stu-id="a3671-333">If you did not use this image, install hello SQL Server tools separately.</span></span> <span data-ttu-id="a3671-334">Consulte [transferir SQL Server Management Studio (SSMS)](http://msdn.microsoft.com/library/mt238290.aspx).</span><span class="sxs-lookup"><span data-stu-id="a3671-334">See [Download SQL Server Management Studio (SSMS)](http://msdn.microsoft.com/library/mt238290.aspx).</span></span>

## <a name="step-5-create-azure-load-balancer"></a><span data-ttu-id="a3671-335">Passo 5: Criar Balanceador de carga do Azure</span><span class="sxs-lookup"><span data-stu-id="a3671-335">Step 5: Create Azure load balancer</span></span>

<span data-ttu-id="a3671-336">Nas máquinas virtuais do Azure, clusters, utilize um toohold de Balanceador de carga um endereço IP que tem toobe num nó de cluster de cada vez.</span><span class="sxs-lookup"><span data-stu-id="a3671-336">On Azure virtual machines, clusters use a load balancer toohold an IP address that needs toobe on one cluster node at a time.</span></span> <span data-ttu-id="a3671-337">Nesta solução, o Balanceador de carga Olá detém do endereço IP Olá Olá SQL Server FCI.</span><span class="sxs-lookup"><span data-stu-id="a3671-337">In this solution, hello load balancer holds hello IP address for hello SQL Server FCI.</span></span>

<span data-ttu-id="a3671-338">[Criar e configurar um balanceador de carga do Azure](virtual-machines-windows-portal-sql-availability-group-tutorial.md#configure-internal-load-balancer).</span><span class="sxs-lookup"><span data-stu-id="a3671-338">[Create and configure an Azure load balancer](virtual-machines-windows-portal-sql-availability-group-tutorial.md#configure-internal-load-balancer).</span></span>

### <a name="create-hello-load-balancer-in-hello-azure-portal"></a><span data-ttu-id="a3671-339">Criar Balanceador de carga Olá no Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="a3671-339">Create hello load balancer in hello Azure portal</span></span>

<span data-ttu-id="a3671-340">Balanceador de carga de Olá toocreate:</span><span class="sxs-lookup"><span data-stu-id="a3671-340">toocreate hello load balancer:</span></span>

1. <span data-ttu-id="a3671-341">No portal do Azure Olá, visite toohello grupo de recursos com Olá máquinas de virtuais.</span><span class="sxs-lookup"><span data-stu-id="a3671-341">In hello Azure portal, go toohello Resource Group with hello virtual machines.</span></span>

1. <span data-ttu-id="a3671-342">Clique em **+ adicionar**.</span><span class="sxs-lookup"><span data-stu-id="a3671-342">Click **+ Add**.</span></span> <span data-ttu-id="a3671-343">Olá pesquisa Marketplace para **Balanceador de carga**.</span><span class="sxs-lookup"><span data-stu-id="a3671-343">Search hello Marketplace for **Load Balancer**.</span></span> <span data-ttu-id="a3671-344">Clique em **Balanceador de carga**.</span><span class="sxs-lookup"><span data-stu-id="a3671-344">Click **Load Balancer**.</span></span>

1. <span data-ttu-id="a3671-345">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="a3671-345">Click **Create**.</span></span>

1. <span data-ttu-id="a3671-346">Configure o Balanceador de carga Olá com:</span><span class="sxs-lookup"><span data-stu-id="a3671-346">Configure hello load balancer with:</span></span>

   - <span data-ttu-id="a3671-347">**Nome**: um nome que identifique o Balanceador de carga Olá.</span><span class="sxs-lookup"><span data-stu-id="a3671-347">**Name**: A name that identifies hello load balancer.</span></span>
   - <span data-ttu-id="a3671-348">**Tipo**: Balanceador de carga Olá pode ser públicas ou privadas.</span><span class="sxs-lookup"><span data-stu-id="a3671-348">**Type**: hello load balancer can be either public or private.</span></span> <span data-ttu-id="a3671-349">Um balanceador de carga privada pode ser acedido a partir do Olá mesma VNET.</span><span class="sxs-lookup"><span data-stu-id="a3671-349">A private load balancer can be accessed from within hello same VNET.</span></span> <span data-ttu-id="a3671-350">Aplicações mais Azure podem utilizar um balanceador de carga privada.</span><span class="sxs-lookup"><span data-stu-id="a3671-350">Most Azure applications can use a private load balancer.</span></span> <span data-ttu-id="a3671-351">Se a aplicação tem acesso tooSQL servidor diretamente através da Internet de Olá, utilize um balanceador de carga público.</span><span class="sxs-lookup"><span data-stu-id="a3671-351">If your application needs access tooSQL Server directly over hello Internet, use a public load balancer.</span></span>
   - <span data-ttu-id="a3671-352">**Rede virtual**: Olá mesmo como máquinas de virtuais Olá de rede.</span><span class="sxs-lookup"><span data-stu-id="a3671-352">**Virtual Network**: hello same network as hello virtual machines.</span></span>
   - <span data-ttu-id="a3671-353">**Sub-rede**: Olá mesma sub-rede que Olá máquinas de virtuais.</span><span class="sxs-lookup"><span data-stu-id="a3671-353">**Subnet**: hello same subnet as hello virtual machines.</span></span>
   - <span data-ttu-id="a3671-354">**Endereço IP privado**: Olá mesmo endereço IP que atribuídos recursos de rede de cluster do toohello SQL Server FCI.</span><span class="sxs-lookup"><span data-stu-id="a3671-354">**Private IP address**: hello same IP address that you assigned toohello SQL Server FCI cluster network resource.</span></span>
   - <span data-ttu-id="a3671-355">**subscrição**: subscrição do Azure.</span><span class="sxs-lookup"><span data-stu-id="a3671-355">**subscription**: Your Azure subscription.</span></span>
   - <span data-ttu-id="a3671-356">**Grupo de recursos**: Utilize Olá mesmo grupo de recursos como as máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="a3671-356">**Resource Group**: Use hello same resource group as your virtual machines.</span></span>
   - <span data-ttu-id="a3671-357">**Localização**: Utilize Olá mesma localização do Azure que as máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="a3671-357">**Location**: Use hello same Azure location as your virtual machines.</span></span>
   <span data-ttu-id="a3671-358">Consulte Olá seguinte imagem:</span><span class="sxs-lookup"><span data-stu-id="a3671-358">See hello following picture:</span></span>

   ![CreateLoadBalancer](./media/virtual-machines-windows-portal-sql-create-failover-cluster/30-load-balancer-create.png)

### <a name="configure-hello-load-balancer-backend-pool"></a><span data-ttu-id="a3671-360">Configurar o conjunto de back-end de Balanceador de carga Olá</span><span class="sxs-lookup"><span data-stu-id="a3671-360">Configure hello load balancer backend pool</span></span>

1. <span data-ttu-id="a3671-361">Devolver toohello grupo de recursos do Azure com as máquinas virtuais de Olá e localize o Balanceador de carga novo Olá.</span><span class="sxs-lookup"><span data-stu-id="a3671-361">Return toohello Azure Resource Group with hello virtual machines and locate hello new load balancer.</span></span> <span data-ttu-id="a3671-362">Poderá ter vista de Olá toorefresh no Olá grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="a3671-362">You may have toorefresh hello view on hello Resource Group.</span></span> <span data-ttu-id="a3671-363">Clique em Balanceador de carga Olá.</span><span class="sxs-lookup"><span data-stu-id="a3671-363">Click hello load balancer.</span></span>

1. <span data-ttu-id="a3671-364">No painel de Balanceador de carga Olá, clique em **conjuntos back-end**.</span><span class="sxs-lookup"><span data-stu-id="a3671-364">On hello load balancer blade, click **Backend pools**.</span></span>

1. <span data-ttu-id="a3671-365">Clique em **+ adicionar** tooadd um conjunto de back-end.</span><span class="sxs-lookup"><span data-stu-id="a3671-365">Click **+ Add** tooadd a backend pool.</span></span>

1. <span data-ttu-id="a3671-366">Escreva um nome para o conjunto de back-end Olá.</span><span class="sxs-lookup"><span data-stu-id="a3671-366">Type a name for hello backend pool.</span></span>

1. <span data-ttu-id="a3671-367">Clique em **adicionar uma máquina virtual**.</span><span class="sxs-lookup"><span data-stu-id="a3671-367">Click **Add a virtual machine**.</span></span>

1. <span data-ttu-id="a3671-368">No Olá **escolher as máquinas virtuais** painel, clique em **escolher um conjunto de disponibilidade**.</span><span class="sxs-lookup"><span data-stu-id="a3671-368">On hello **Choose virtual machines** blade, click **Choose an availability set**.</span></span>

1. <span data-ttu-id="a3671-369">Escolha o conjunto de disponibilidade de Olá que colocou Olá do SQL Server máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="a3671-369">Choose hello availability set that you placed hello SQL Server virtual machines in.</span></span>

1. <span data-ttu-id="a3671-370">No Olá **escolher as máquinas virtuais** painel, clique em **escolher máquinas de virtuais Olá**.</span><span class="sxs-lookup"><span data-stu-id="a3671-370">On hello **Choose virtual machines** blade, click **Choose hello virtual machines**.</span></span>

   <span data-ttu-id="a3671-371">O portal do Azure deve aspeto Olá seguinte imagem:</span><span class="sxs-lookup"><span data-stu-id="a3671-371">Your Azure portal should look like hello following picture:</span></span>

   ![CreateLoadBalancerBackEnd](./media/virtual-machines-windows-portal-sql-create-failover-cluster/33-load-balancer-back-end.png)

1. <span data-ttu-id="a3671-373">Clique em **selecione** no Olá **escolher as máquinas virtuais** painel.</span><span class="sxs-lookup"><span data-stu-id="a3671-373">Click **Select** on hello **Choose virtual machines** blade.</span></span>

1. <span data-ttu-id="a3671-374">Clique em **OK** duas vezes.</span><span class="sxs-lookup"><span data-stu-id="a3671-374">Click **OK** twice.</span></span>

### <a name="configure-a-load-balancer-health-probe"></a><span data-ttu-id="a3671-375">Configurar uma sonda de estado de funcionamento do Balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="a3671-375">Configure a load balancer health probe</span></span>

1. <span data-ttu-id="a3671-376">No painel de Balanceador de carga Olá, clique em **sondas de estado de funcionamento**.</span><span class="sxs-lookup"><span data-stu-id="a3671-376">On hello load balancer blade, click **Health probes**.</span></span>

1. <span data-ttu-id="a3671-377">Clique em **+ adicionar**.</span><span class="sxs-lookup"><span data-stu-id="a3671-377">Click **+ Add**.</span></span>

1. <span data-ttu-id="a3671-378">No Olá **sonda do Estado de funcionamento de adicionar** painel, <a name="probe"> </a>definir parâmetros de pesquisa de estado de funcionamento de Olá:</span><span class="sxs-lookup"><span data-stu-id="a3671-378">On hello **Add health probe** blade, <a name="probe"></a>Set hello health probe parameters:</span></span>

   - <span data-ttu-id="a3671-379">**Nome**: um nome para a sonda de estado de funcionamento de Olá.</span><span class="sxs-lookup"><span data-stu-id="a3671-379">**Name**: A name for hello health probe.</span></span>
   - <span data-ttu-id="a3671-380">**Protocolo**: TCP.</span><span class="sxs-lookup"><span data-stu-id="a3671-380">**Protocol**: TCP.</span></span>
   - <span data-ttu-id="a3671-381">**Porta**: Definir tooan porta TCP disponível.</span><span class="sxs-lookup"><span data-stu-id="a3671-381">**Port**: Set tooan available TCP port.</span></span> <span data-ttu-id="a3671-382">Esta porta necessita de uma porta de firewall aberta.</span><span class="sxs-lookup"><span data-stu-id="a3671-382">This port requires an open firewall port.</span></span> <span data-ttu-id="a3671-383">Olá utilize [mesma porta](#ports) definido para a sonda de estado de funcionamento de Olá na firewall de Olá.</span><span class="sxs-lookup"><span data-stu-id="a3671-383">Use hello [same port](#ports) you set for hello health probe at hello firewall.</span></span>
   - <span data-ttu-id="a3671-384">**Intervalo**: 5 segundos.</span><span class="sxs-lookup"><span data-stu-id="a3671-384">**Interval**: 5 Seconds.</span></span>
   - <span data-ttu-id="a3671-385">**Limiar de mau estado de funcionamento**: 2 falhas consecutivas.</span><span class="sxs-lookup"><span data-stu-id="a3671-385">**Unhealthy threshold**: 2 consecutive failures.</span></span>

1. <span data-ttu-id="a3671-386">Clique em OK.</span><span class="sxs-lookup"><span data-stu-id="a3671-386">Click OK.</span></span>

### <a name="set-load-balancing-rules"></a><span data-ttu-id="a3671-387">Definir regras de balanceamento de carga</span><span class="sxs-lookup"><span data-stu-id="a3671-387">Set load balancing rules</span></span>

1. <span data-ttu-id="a3671-388">No painel de Balanceador de carga Olá, clique em **as regras de balanceamento de carga**.</span><span class="sxs-lookup"><span data-stu-id="a3671-388">On hello load balancer blade, click **Load balancing rules**.</span></span>

1. <span data-ttu-id="a3671-389">Clique em **+ adicionar**.</span><span class="sxs-lookup"><span data-stu-id="a3671-389">Click **+ Add**.</span></span>

1. <span data-ttu-id="a3671-390">Definir os parâmetros de regras de balanceamento de carga de Olá:</span><span class="sxs-lookup"><span data-stu-id="a3671-390">Set hello load balancing rules parameters:</span></span>

   - <span data-ttu-id="a3671-391">**Nome**: um nome para as regras de balanceamento de carga de Olá.</span><span class="sxs-lookup"><span data-stu-id="a3671-391">**Name**: A name for hello load balancing rules.</span></span>
   - <span data-ttu-id="a3671-392">**Endereço IP de front-end**: Utilize um endereço IP Olá para Olá recurso de rede de cluster do SQL Server FCI.</span><span class="sxs-lookup"><span data-stu-id="a3671-392">**Frontend IP address**: Use hello IP address for hello SQL Server FCI cluster network resource.</span></span>
   - <span data-ttu-id="a3671-393">**Porta**: definir para Olá a porta TCP do SQL Server FCI.</span><span class="sxs-lookup"><span data-stu-id="a3671-393">**Port**: Set for hello SQL Server FCI TCP port.</span></span> <span data-ttu-id="a3671-394">porta de instância Olá predefinida é 1433.</span><span class="sxs-lookup"><span data-stu-id="a3671-394">hello default instance port is 1433.</span></span>
   - <span data-ttu-id="a3671-395">**Porta de back-end**: este valor utiliza Olá a mesma porta como Olá **porta** valor quando ativar **IP flutuante (devolução direta do servidor)**.</span><span class="sxs-lookup"><span data-stu-id="a3671-395">**Backend port**: This value uses hello same port as hello **Port** value when you enable **Floating IP (direct server return)**.</span></span>
   - <span data-ttu-id="a3671-396">**Conjunto back-end**: nome conjunto de back-end de Olá de utilização que configurou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="a3671-396">**Backend pool**: Use hello backend pool name that you configured earlier.</span></span>
   - <span data-ttu-id="a3671-397">**Sonda de estado de funcionamento**: sonda de estado de funcionamento de Olá utilização que configurou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="a3671-397">**Health probe**: Use hello health probe that you configured earlier.</span></span>
   - <span data-ttu-id="a3671-398">**Persistência da sessão**: nenhuma.</span><span class="sxs-lookup"><span data-stu-id="a3671-398">**Session persistence**: None.</span></span>
   - <span data-ttu-id="a3671-399">**Tempo limite (minutos) de inatividade**: 4.</span><span class="sxs-lookup"><span data-stu-id="a3671-399">**Idle timeout (minutes)**: 4.</span></span>
   - <span data-ttu-id="a3671-400">**Vírgula flutuante (devolução direta do servidor) de IP**: ativado</span><span class="sxs-lookup"><span data-stu-id="a3671-400">**Floating IP (direct server return)**: Enabled</span></span>

1. <span data-ttu-id="a3671-401">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="a3671-401">Click **OK**.</span></span>

## <a name="step-6-configure-cluster-for-probe"></a><span data-ttu-id="a3671-402">Passo 6: Configurar o cluster para a sonda</span><span class="sxs-lookup"><span data-stu-id="a3671-402">Step 6: Configure cluster for probe</span></span>

<span data-ttu-id="a3671-403">Definir o parâmetro de porta de sonda de cluster Olá no PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a3671-403">Set hello cluster probe port parameter in PowerShell.</span></span>

<span data-ttu-id="a3671-404">tooset Olá parâmetro de porta de sonda de cluster, Atualize as variáveis no Olá seguinte script do seu ambiente.</span><span class="sxs-lookup"><span data-stu-id="a3671-404">tooset hello cluster probe port parameter, update variables in hello following script from your environment.</span></span>

  ```PowerShell
   $ClusterNetworkName = "<Cluster Network Name>" # hello cluster network name (Use Get-ClusterNetwork on Windows Server 2012 of higher toofind hello name).
   $IPResourceName = "IP Address Resource Name" # hello IP Address cluster resource name.
   $ILBIP = "<10.0.0.x>" # hello IP Address of hello Internal Load Balancer (ILB). This is hello static IP address for hello load balancer you configured in hello Azure portal.
   [int]$ProbePort = <59999>

   Import-Module FailoverClusters

   Get-ClusterResource $IPResourceName | Set-ClusterParameter -Multiple @{"Address"="$ILBIP";"ProbePort"=$ProbePort;"SubnetMask"="255.255.255.255";"Network"="$ClusterNetworkName";"EnableDhcp"=0}
   ```


## <a name="step-7-test-fci-failover"></a><span data-ttu-id="a3671-405">Passo 7: Testar a ativação pós-falha da FCI</span><span class="sxs-lookup"><span data-stu-id="a3671-405">Step 7: Test FCI failover</span></span>

<span data-ttu-id="a3671-406">Testar a ativação pós-falha de Olá a funcionalidade de cluster toovalidate FCI.</span><span class="sxs-lookup"><span data-stu-id="a3671-406">Test failover of hello FCI toovalidate cluster functionality.</span></span> <span data-ttu-id="a3671-407">Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="a3671-407">Do hello following steps:</span></span>

1. <span data-ttu-id="a3671-408">Ligar tooone de nós de cluster do SQL Server FCI Olá com RDP.</span><span class="sxs-lookup"><span data-stu-id="a3671-408">Connect tooone of hello SQL Server FCI cluster nodes with RDP.</span></span>

1. <span data-ttu-id="a3671-409">Abra **Gestor de clusters de ativação pós-falha**.</span><span class="sxs-lookup"><span data-stu-id="a3671-409">Open **Failover Cluster Manager**.</span></span> <span data-ttu-id="a3671-410">Clique em **funções**.</span><span class="sxs-lookup"><span data-stu-id="a3671-410">Click **Roles**.</span></span> <span data-ttu-id="a3671-411">Aviso de nó que possui a função de SQL Server FCI Olá.</span><span class="sxs-lookup"><span data-stu-id="a3671-411">Notice which node owns hello SQL Server FCI role.</span></span>

1. <span data-ttu-id="a3671-412">Clique com botão direito função do SQL Server FCI Olá.</span><span class="sxs-lookup"><span data-stu-id="a3671-412">Right-click hello SQL Server FCI role.</span></span>

1. <span data-ttu-id="a3671-413">Clique em **mover** e clique em **melhor nó possível**.</span><span class="sxs-lookup"><span data-stu-id="a3671-413">Click **Move** and click **Best Possible Node**.</span></span>

<span data-ttu-id="a3671-414">**Gestor de clusters de ativação pós-falha** mostra Olá função e respetivos recursos fique offline.</span><span class="sxs-lookup"><span data-stu-id="a3671-414">**Failover Cluster Manager** shows hello role and its resources go offline.</span></span> <span data-ttu-id="a3671-415">Olá recursos, em seguida, mover e ficar online Olá no outro nó.</span><span class="sxs-lookup"><span data-stu-id="a3671-415">hello resources then move and come online on hello other node.</span></span>

### <a name="test-connectivity"></a><span data-ttu-id="a3671-416">Testar conectividade</span><span class="sxs-lookup"><span data-stu-id="a3671-416">Test connectivity</span></span>

<span data-ttu-id="a3671-417">conectividade tootest, registo na máquina virtual tooanother Olá mesma rede virtual.</span><span class="sxs-lookup"><span data-stu-id="a3671-417">tootest connectivity, log in tooanother virtual machine in hello same virtual network.</span></span> <span data-ttu-id="a3671-418">Abra **SQL Server Management Studio** e ligar o nome do SQL Server FCI toohello.</span><span class="sxs-lookup"><span data-stu-id="a3671-418">Open **SQL Server Management Studio** and connect toohello SQL Server FCI name.</span></span>

>[!NOTE]
><span data-ttu-id="a3671-419">Se necessário, pode [transferir SQL Server Management Studio](http://msdn.microsoft.com/library/mt238290.aspx).</span><span class="sxs-lookup"><span data-stu-id="a3671-419">If necessary, you can [download SQL Server Management Studio](http://msdn.microsoft.com/library/mt238290.aspx).</span></span>

## <a name="limitations"></a><span data-ttu-id="a3671-420">Limitações</span><span class="sxs-lookup"><span data-stu-id="a3671-420">Limitations</span></span>
<span data-ttu-id="a3671-421">Máquinas virtuais do Azure, coordenador de transações distribuídas ' (DTC) da Microsoft não é suportada em FCIs porque Olá porta RPC não é suportado pelo balanceador de carga Olá.</span><span class="sxs-lookup"><span data-stu-id="a3671-421">On Azure virtual machines, Microsoft Distributed Transaction Coordinator (DTC) is not supported on FCIs because hello RPC port is not supported by hello load balancer.</span></span>

## <a name="see-also"></a><span data-ttu-id="a3671-422">Veja Também</span><span class="sxs-lookup"><span data-stu-id="a3671-422">See Also</span></span>

[<span data-ttu-id="a3671-423">A configuração S2D com o ambiente de trabalho remoto (Azure)</span><span class="sxs-lookup"><span data-stu-id="a3671-423">Setup S2D with remote desktop (Azure)</span></span>](http://technet.microsoft.com/windows-server-docs/compute/remote-desktop-services/rds-storage-spaces-direct-deployment)

<span data-ttu-id="a3671-424">[Hyper-convergido solução com espaços de armazenamento diretos](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct).</span><span class="sxs-lookup"><span data-stu-id="a3671-424">[Hyper-converged solution with storage spaces direct](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct).</span></span>

[<span data-ttu-id="a3671-425">Descrição geral direta do espaço de armazenamento</span><span class="sxs-lookup"><span data-stu-id="a3671-425">Storage Space Direct Overview</span></span>](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/storage-spaces-direct-overview)

[<span data-ttu-id="a3671-426">Suporte do SQL Server para S2D</span><span class="sxs-lookup"><span data-stu-id="a3671-426">SQL Server support for S2D</span></span>](https://blogs.technet.microsoft.com/dataplatforminsider/2016/09/27/sql-server-2016-now-supports-windows-server-2016-storage-spaces-direct/)
