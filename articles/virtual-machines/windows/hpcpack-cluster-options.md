---
title: "aaaWindows HPC Pack cluster opções na nuvem de Olá | Microsoft Docs"
description: "Saiba mais sobre as opções de com o Microsoft HPC Pack toocreate e gerir um desempenho elevado do Windows computação em cluster (HPC) Olá em nuvem do Azure"
services: virtual-machines-windows,cloud-services,batch
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management,hpc-pack
ms.assetid: 02c5566d-2129-483c-9ecf-0d61030442d7
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 02/06/2017
ms.author: danlep
ms.openlocfilehash: 6158d9dd0cecda38b14f85a2b2080163f18e8cf8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="options-with-hpc-pack-toocreate-and-manage-a-windows-hpc-cluster-in-azure"></a><span data-ttu-id="3f7e0-103">Opções com HPC Pack toocreate e gerir um cluster Windows HPC no Azure</span><span class="sxs-lookup"><span data-stu-id="3f7e0-103">Options with HPC Pack toocreate and manage a Windows HPC cluster in Azure</span></span>
[!INCLUDE [virtual-machines-common-hpcpack-cluster-options](../../../includes/virtual-machines-common-hpcpack-cluster-options.md)]

<span data-ttu-id="3f7e0-104">Este artigo incida no opções toocreate HPC Pack cargas de trabalho do clusters toorun Windows.</span><span class="sxs-lookup"><span data-stu-id="3f7e0-104">This article focuses on options toocreate HPC Pack clusters toorun Windows workloads.</span></span> <span data-ttu-id="3f7e0-105">Também existem opções para criar pacote HPC clusters toorun [cargas de trabalho Linux HPC](../linux/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="3f7e0-105">There are also options for creating HPC Pack clusters toorun [Linux HPC workloads](../linux/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>


## <a name="run-an-hpc-pack-cluster-in-azure-vms"></a><span data-ttu-id="3f7e0-106">Executar um cluster HPC Pack em VMs do Azure</span><span class="sxs-lookup"><span data-stu-id="3f7e0-106">Run an HPC Pack cluster in Azure VMs</span></span>
### <a name="azure-templates"></a><span data-ttu-id="3f7e0-107">Modelos do Azure</span><span class="sxs-lookup"><span data-stu-id="3f7e0-107">Azure templates</span></span>
* <span data-ttu-id="3f7e0-108">(GitHub) [Modelos de cluster HPC Pack 2016](https://github.com/MsHpcPack/HPCPack2016)</span><span class="sxs-lookup"><span data-stu-id="3f7e0-108">(GitHub) [HPC Pack 2016 cluster templates](https://github.com/MsHpcPack/HPCPack2016)</span></span>
* <span data-ttu-id="3f7e0-109">(Marketplace) [Cluster HPC Pack para cargas de trabalho do Windows](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterwindowscn/)</span><span class="sxs-lookup"><span data-stu-id="3f7e0-109">(Marketplace) [HPC Pack cluster for Windows workloads](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterwindowscn/)</span></span>
* <span data-ttu-id="3f7e0-110">(Marketplace) [Cluster HPC Pack para cargas de trabalho do Excel](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterexcelcn/)</span><span class="sxs-lookup"><span data-stu-id="3f7e0-110">(Marketplace) [HPC Pack cluster for Excel workloads](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterexcelcn/)</span></span>
* <span data-ttu-id="3f7e0-111">(Início rápido) [Criar um cluster HPC](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster)</span><span class="sxs-lookup"><span data-stu-id="3f7e0-111">(Quickstart) [Create an HPC cluster](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster)</span></span>
* <span data-ttu-id="3f7e0-112">(Início rápido) [Criar um cluster HPC com a imagem do nó de computação personalizada](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster-custom-image)</span><span class="sxs-lookup"><span data-stu-id="3f7e0-112">(Quickstart) [Create an HPC cluster with custom compute node image](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster-custom-image)</span></span>

### <a name="azure-vm-images"></a><span data-ttu-id="3f7e0-113">Imagens VM do Azure</span><span class="sxs-lookup"><span data-stu-id="3f7e0-113">Azure VM images</span></span>
* [<span data-ttu-id="3f7e0-114">Nó principal do HPC Pack 2016 no Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="3f7e0-114">HPC Pack 2016 head node on Windows Server 2016</span></span>](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.HPCPack2016HeadNodeonWindowsServer2016?tab=Overview)
* [<span data-ttu-id="3f7e0-115">Nó de computação de HPC Pack 2016 no Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="3f7e0-115">HPC Pack 2016 compute node on Windows Server 2016</span></span>](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.HPCPack2016ComputeNodeonWindowsServer2016?tab=Overview)
* [<span data-ttu-id="3f7e0-116">Nó principal do HPC Pack 2016 no Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="3f7e0-116">HPC Pack 2016 head node on Windows Server 2012 R2</span></span>](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.HPCPack2016HeadNodeonWindowsServer2012R2?tab=Overview)
* [<span data-ttu-id="3f7e0-117">Nó de computação de HPC Pack 2016 no Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="3f7e0-117">HPC Pack 2016 compute node on Windows Server 2012 R2</span></span>](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.HPCPack2016ComputeNodeonWindowsServer2012R2?tab=Overview)
* [<span data-ttu-id="3f7e0-118">Nó principal do HPC Pack 2012 R2 no Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="3f7e0-118">HPC Pack 2012 R2 head node on Windows Server 2012 R2</span></span>](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2onwindowsserver2012r2/)
* [<span data-ttu-id="3f7e0-119">Nó de computação de HPC Pack 2012 R2 no Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="3f7e0-119">HPC Pack 2012 R2 compute node on Windows Server 2012 R2</span></span>](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2computenodeonwindowsserver2012r2/)
* [<span data-ttu-id="3f7e0-120">Pacote HPC computação nó com o Excel no Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="3f7e0-120">HPC Pack compute node with Excel on Windows Server 2012 R2</span></span>](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2computenodewithexcelonwindowsserver2012r2/)

### <a name="powershell-deployment-script"></a><span data-ttu-id="3f7e0-121">Script de implementação do PowerShell</span><span class="sxs-lookup"><span data-stu-id="3f7e0-121">PowerShell deployment script</span></span>
* [<span data-ttu-id="3f7e0-122">Criar um cluster HPC com Olá script de implementação do IaaS do HPC Pack</span><span class="sxs-lookup"><span data-stu-id="3f7e0-122">Create an HPC cluster with hello HPC Pack IaaS deployment script</span></span>](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

### <a name="tutorials"></a><span data-ttu-id="3f7e0-123">Tutoriais</span><span class="sxs-lookup"><span data-stu-id="3f7e0-123">Tutorials</span></span>
* [<span data-ttu-id="3f7e0-124">Tutorial: Implementar um cluster HPC Pack 2016 no Azure</span><span class="sxs-lookup"><span data-stu-id="3f7e0-124">Tutorial: Deploy an HPC Pack 2016 cluster in Azure</span></span>](hpcpack-2016-cluster.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="3f7e0-125">Tutorial: Introdução com um cluster HPC Pack no Azure toorun Excel e cargas de trabalho SOA</span><span class="sxs-lookup"><span data-stu-id="3f7e0-125">Tutorial: Get started with an HPC Pack cluster in Azure toorun Excel and SOA workloads</span></span>](excel-cluster-hpcpack.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

### <a name="manual-deployment-with-hello-azure-portal"></a><span data-ttu-id="3f7e0-126">Implementação manual com Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="3f7e0-126">Manual deployment with hello Azure portal</span></span>
* [<span data-ttu-id="3f7e0-127">Configurar o nó principal do Olá de um cluster HPC Pack numa VM do Azure</span><span class="sxs-lookup"><span data-stu-id="3f7e0-127">Set up hello head node of an HPC Pack cluster in an Azure VM</span></span>](hpcpack-cluster-headnode.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

### <a name="cluster-management"></a><span data-ttu-id="3f7e0-128">Gestão de clusters</span><span class="sxs-lookup"><span data-stu-id="3f7e0-128">Cluster management</span></span>
* [<span data-ttu-id="3f7e0-129">Gerir os nós de computação de um cluster HPC Pack no Azure</span><span class="sxs-lookup"><span data-stu-id="3f7e0-129">Manage compute nodes in an HPC Pack cluster in Azure</span></span>](classic/hpcpack-cluster-node-manage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
* [<span data-ttu-id="3f7e0-130">Aumentar e diminuir a recursos de computação do Azure num cluster HPC Pack</span><span class="sxs-lookup"><span data-stu-id="3f7e0-130">Grow and shrink Azure compute resources in an HPC Pack cluster</span></span>](classic/hpcpack-cluster-node-autogrowshrink.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
* [<span data-ttu-id="3f7e0-131">Submeter cluster HPC Pack de tooan de tarefas no Azure</span><span class="sxs-lookup"><span data-stu-id="3f7e0-131">Submit jobs tooan HPC Pack cluster in Azure</span></span>](hpcpack-cluster-submit-jobs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="3f7e0-132">Gestão de tarefas no HPC Pack</span><span class="sxs-lookup"><span data-stu-id="3f7e0-132">Job management in HPC Pack</span></span>](https://technet.microsoft.com/library/jj899585.aspx)
* [<span data-ttu-id="3f7e0-133">Gerir um cluster HPC Pack no Azure com o Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3f7e0-133">Manage an HPC Pack cluster in Azure with Azure Active Directory</span></span>](hpcpack-cluster-active-directory.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

## <a name="add-worker-role-nodes-tooan-hpc-pack-cluster"></a><span data-ttu-id="3f7e0-134">Adicionar o cluster de HPC Pack de tooan de nós de função de trabalho</span><span class="sxs-lookup"><span data-stu-id="3f7e0-134">Add worker role nodes tooan HPC Pack cluster</span></span>
* [<span data-ttu-id="3f7e0-135">Impulsar tooAzure instâncias de trabalho com o HPC Pack</span><span class="sxs-lookup"><span data-stu-id="3f7e0-135">Burst tooAzure worker instances with HPC Pack</span></span>](https://technet.microsoft.com/library/gg481749.aspx)
* [<span data-ttu-id="3f7e0-136">Tutorial: Configurar um cluster de híbrido com o HPC Pack no Azure</span><span class="sxs-lookup"><span data-stu-id="3f7e0-136">Tutorial: Set up a hybrid cluster with HPC Pack in Azure</span></span>](../../cloud-services/cloud-services-setup-hybrid-hpcpack-cluster.md)
* [<span data-ttu-id="3f7e0-137">Adicionar do Azure "impulsar" nós tooan HPC Pack nó principal no Azure</span><span class="sxs-lookup"><span data-stu-id="3f7e0-137">Add Azure "burst" nodes tooan HPC Pack head node in Azure</span></span>](classic/hpcpack-cluster-node-burst.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

## <a name="integrate-with-azure-batch"></a><span data-ttu-id="3f7e0-138">Integrar com o Azure Batch</span><span class="sxs-lookup"><span data-stu-id="3f7e0-138">Integrate with Azure Batch</span></span>
* [<span data-ttu-id="3f7e0-139">Impulsar tooAzure Batch com o HPC Pack</span><span class="sxs-lookup"><span data-stu-id="3f7e0-139">Burst tooAzure Batch with HPC Pack</span></span>](https://technet.microsoft.com/library/mt612877.aspx)

## <a name="create-rdma-clusters-for-mpi-workloads"></a><span data-ttu-id="3f7e0-140">Criar clusters RDMA para cargas de trabalho MPI</span><span class="sxs-lookup"><span data-stu-id="3f7e0-140">Create RDMA clusters for MPI workloads</span></span>
* [<span data-ttu-id="3f7e0-141">Configurar um cluster do Windows RDMA com aplicações de MPI toorun HPC Pack</span><span class="sxs-lookup"><span data-stu-id="3f7e0-141">Set up a Windows RDMA cluster with HPC Pack toorun MPI applications</span></span>](classic/hpcpack-rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

