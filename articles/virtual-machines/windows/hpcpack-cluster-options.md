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
# <a name="options-with-hpc-pack-toocreate-and-manage-a-windows-hpc-cluster-in-azure"></a>Opções com HPC Pack toocreate e gerir um cluster Windows HPC no Azure
[!INCLUDE [virtual-machines-common-hpcpack-cluster-options](../../../includes/virtual-machines-common-hpcpack-cluster-options.md)]

Este artigo incida no opções toocreate HPC Pack cargas de trabalho do clusters toorun Windows. Também existem opções para criar pacote HPC clusters toorun [cargas de trabalho Linux HPC](../linux/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).


## <a name="run-an-hpc-pack-cluster-in-azure-vms"></a>Executar um cluster HPC Pack em VMs do Azure
### <a name="azure-templates"></a>Modelos do Azure
* (GitHub) [Modelos de cluster HPC Pack 2016](https://github.com/MsHpcPack/HPCPack2016)
* (Marketplace) [Cluster HPC Pack para cargas de trabalho do Windows](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterwindowscn/)
* (Marketplace) [Cluster HPC Pack para cargas de trabalho do Excel](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterexcelcn/)
* (Início rápido) [Criar um cluster HPC](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster)
* (Início rápido) [Criar um cluster HPC com a imagem do nó de computação personalizada](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster-custom-image)

### <a name="azure-vm-images"></a>Imagens VM do Azure
* [Nó principal do HPC Pack 2016 no Windows Server 2016](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.HPCPack2016HeadNodeonWindowsServer2016?tab=Overview)
* [Nó de computação de HPC Pack 2016 no Windows Server 2016](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.HPCPack2016ComputeNodeonWindowsServer2016?tab=Overview)
* [Nó principal do HPC Pack 2016 no Windows Server 2012 R2](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.HPCPack2016HeadNodeonWindowsServer2012R2?tab=Overview)
* [Nó de computação de HPC Pack 2016 no Windows Server 2012 R2](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.HPCPack2016ComputeNodeonWindowsServer2012R2?tab=Overview)
* [Nó principal do HPC Pack 2012 R2 no Windows Server 2012 R2](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2onwindowsserver2012r2/)
* [Nó de computação de HPC Pack 2012 R2 no Windows Server 2012 R2](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2computenodeonwindowsserver2012r2/)
* [Pacote HPC computação nó com o Excel no Windows Server 2012 R2](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2computenodewithexcelonwindowsserver2012r2/)

### <a name="powershell-deployment-script"></a>Script de implementação do PowerShell
* [Criar um cluster HPC com Olá script de implementação do IaaS do HPC Pack](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

### <a name="tutorials"></a>Tutoriais
* [Tutorial: Implementar um cluster HPC Pack 2016 no Azure](hpcpack-2016-cluster.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Tutorial: Introdução com um cluster HPC Pack no Azure toorun Excel e cargas de trabalho SOA](excel-cluster-hpcpack.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

### <a name="manual-deployment-with-hello-azure-portal"></a>Implementação manual com Olá portal do Azure
* [Configurar o nó principal do Olá de um cluster HPC Pack numa VM do Azure](hpcpack-cluster-headnode.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

### <a name="cluster-management"></a>Gestão de clusters
* [Gerir os nós de computação de um cluster HPC Pack no Azure](classic/hpcpack-cluster-node-manage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
* [Aumentar e diminuir a recursos de computação do Azure num cluster HPC Pack](classic/hpcpack-cluster-node-autogrowshrink.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
* [Submeter cluster HPC Pack de tooan de tarefas no Azure](hpcpack-cluster-submit-jobs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Gestão de tarefas no HPC Pack](https://technet.microsoft.com/library/jj899585.aspx)
* [Gerir um cluster HPC Pack no Azure com o Azure Active Directory](hpcpack-cluster-active-directory.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

## <a name="add-worker-role-nodes-tooan-hpc-pack-cluster"></a>Adicionar o cluster de HPC Pack de tooan de nós de função de trabalho
* [Impulsar tooAzure instâncias de trabalho com o HPC Pack](https://technet.microsoft.com/library/gg481749.aspx)
* [Tutorial: Configurar um cluster de híbrido com o HPC Pack no Azure](../../cloud-services/cloud-services-setup-hybrid-hpcpack-cluster.md)
* [Adicionar do Azure "impulsar" nós tooan HPC Pack nó principal no Azure](classic/hpcpack-cluster-node-burst.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

## <a name="integrate-with-azure-batch"></a>Integrar com o Azure Batch
* [Impulsar tooAzure Batch com o HPC Pack](https://technet.microsoft.com/library/mt612877.aspx)

## <a name="create-rdma-clusters-for-mpi-workloads"></a>Criar clusters RDMA para cargas de trabalho MPI
* [Configurar um cluster do Windows RDMA com aplicações de MPI toorun HPC Pack](classic/hpcpack-rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

