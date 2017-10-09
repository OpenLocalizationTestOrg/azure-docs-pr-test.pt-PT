---
title: "Opções de cluster HPC Pack aaaLinux na nuvem de Olá | Microsoft Docs"
description: "Saiba mais sobre as opções de com o Microsoft HPC Pack toocreate e gerir um Linux elevado desempenho computação em cluster (HPC) Olá em nuvem do Azure"
services: virtual-machines-linux,cloud-services
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management,hpc-pack
ms.assetid: ac60624e-aefa-40c3-8bc1-ef6d5c0ef1a2
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: big-compute
ms.date: 02/06/2017
ms.author: danlep
ms.openlocfilehash: 60d093b466f44a0391815842c421c328e8c7a0d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="options-with-hpc-pack-toocreate-and-manage-an-hpc-cluster-in-azure-for-linux-workloads"></a>Opções com HPC Pack toocreate e gerir um cluster HPC no Azure para cargas de trabalho do Linux
[!INCLUDE [virtual-machines-common-hpcpack-cluster-options](../../../includes/virtual-machines-common-hpcpack-cluster-options.md)]

Este artigo incida no opções toouse HPC Pack toorun Linux as cargas de trabalho. Também existem opções para executar [cargas de trabalho do Windows HPC com o HPC Pack](../windows/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

## <a name="run-an-hpc-pack-cluster-in-azure-vms"></a>Executar um cluster HPC Pack em VMs do Azure
### <a name="azure-templates"></a>Modelos do Azure
* (GitHub) [Modelos de cluster HPC Pack 2016](https://github.com/MsHpcPack/HPCPack2016)
* (Marketplace) [Cluster HPC Pack para cargas de trabalho do Linux](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/)
* (Início rápido) [Criar um cluster HPC connosco de computação do Linux](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster-linux-cn)

### <a name="powershell-deployment-script"></a>Script de implementação do PowerShell
* [Criar um cluster Linux HPC com Olá script de implementação do IaaS do HPC Pack](../windows/classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)

### <a name="tutorials"></a>Tutoriais
* [Tutorial: Introdução a nós de computação do Linux num cluster HPC Pack no Azure](classic/hpcpack-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [Tutorial: Executar NAMD com o Microsoft HPC Pack no Linux nós de computação em do Azure](classic/hpcpack-cluster-namd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [Tutorial: Executar OpenFOAM com o Microsoft HPC Pack num cluster Linux RDMA no Azure](classic/hpcpack-cluster-openfoam.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [Tutorial: Executar ESTRELA-CCM + com o Microsoft HPC Pack num RDMA Linux cluster no Azure](classic/hpcpack-cluster-starccm.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)

### <a name="cluster-management"></a>Gestão de clusters
* [Submeter cluster HPC Pack de tooan de tarefas no Azure](../windows/hpcpack-cluster-submit-jobs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Gestão de tarefas no HPC Pack](https://technet.microsoft.com/library/jj899585.aspx)

## <a name="create-rdma-clusters-for-mpi-workloads"></a>Criar clusters RDMA para cargas de trabalho MPI
* [Tutorial: Executar OpenFOAM com o Microsoft HPC Pack num cluster Linux RDMA no Azure](classic/hpcpack-cluster-openfoam.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [Configurar um Linux RDMA cluster toorun MPI aplicações](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)

