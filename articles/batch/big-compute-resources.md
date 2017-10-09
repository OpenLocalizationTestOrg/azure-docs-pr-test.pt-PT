---
title: "aaaResources para batch e HPC na Olá em nuvem do Azure | Microsoft Docs"
description: "Apresenta uma lista de toohelp recursos técnicos, execute o paralelo em grande escala, batch e cargas de trabalho (HPC) no Azure de computação de alto desempenho."
services: batch, cloud-services, virtual-machines
documentationcenter: 
author: dlepow
manager: timlt
editor: 
ms.assetid: 6f8be911-c841-41ae-88d3-3bcfc029eb7f
ms.service: multiple
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: big-compute
ms.date: 03/17/2017
ms.author: danlep
ms.openlocfilehash: ab8ba24678bd7ec090306b501d29ca63c4fb83ee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="big-compute-in-azure-technical-resources-for-batch-and-high-performance-computing"></a>Tamanho de computação no Azure: recursos técnicos para batch e computação de elevado desempenho
Este é um toohelp de recursos do guia tootechnical executar o paralelo em grande escala, batch e cargas de trabalho de computação de alto desempenho (HPC) no Azure. Expanda o batch existente ou toohello de cargas de trabalho HPC em nuvem do Azure ou criar novas soluções de Macrocomputação utilizando os serviços de um intervalo de Azure.

## <a name="solutions-options"></a>Opções de soluções
Saiba mais sobre as opções de Macrocomputação no Azure e escolha a abordagem de direito de Olá para a sua necessidade de carga de trabalho e o negócio.

* [Soluções batch e HPC](batch-hpc-solutions.md)
* [Vídeo: Macrocomputação na nuvem de Olá com o Azure e HPC](https://azure.microsoft.com/documentation/videos/teched-europe-2014-big-compute-in-the-cloud-with-high-performance-computing-on-azure/)

## <a name="azure-batch"></a>Azure Batch
[Batch](https://azure.microsoft.com/services/batch/) é um serviço de plataforma que torna mais fácil toocloud-ativar as suas aplicações de Linux e Windows e as tarefas de execução sem configurar e gerir um agendador de cluster e a tarefa. Utilizar aplicações de cliente do Olá SDK toointegrate com o Azure Batch através de vários idiomas, fase dados tooAzure e criar pipelines de execução da tarefa.

* [Documentação](https://azure.microsoft.com/documentation/services/batch/)
* [.NET](https://msdn.microsoft.com/library/azure/mt348682.aspx), [Python](http://azure-sdk-for-python.readthedocs.io/latest/), [Node.js](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/), [Java](http://azure.github.io/azure-sdk-for-java/), e [REST](https://msdn.microsoft.com/library/azure/dn820158.aspx) referência da API
* [Biblioteca de .NET do batch gestão](https://msdn.microsoft.com/library/mt463120.aspx) referência
* Tutoriais: Introdução ao [biblioteca do Azure Batch para .NET](batch-dotnet-get-started.md) e [cliente Batch Python](batch-python-tutorial.md)
* [Fórum do batch](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurebatch)
* [Vídeos do batch](https://azure.microsoft.com/documentation/videos/index/?services=batch)

## <a name="hpc-cluster-solutions"></a>Soluções de cluster HPC
Implementar ou expandir a sua existente Windows ou Linux HPC cluster tooAzure toorun as cargas de trabalho intensivas de computação.  

### <a name="microsoft-hpc-pack"></a>Pacote HPC da Microsoft
Pacote HPC é gratuita HPC solução da Microsoft incorporada no Microsoft Azure e o Windows Server tecnologias, capazes de executar o Windows e Linux HPC cargas de trabalho.  

* [Transferir o pacote HPC 2016](https://www.microsoft.com/download/details.aspx?id=54507)
* [Transferir o HPC Pack 2012 R2 Update 3](https://www.microsoft.com/download/details.aspx?id=49922)
* [Documentação](https://technet.microsoft.com/library/jj899572.aspx)
* Opções de cluster HPC Pack no Azure: [Linux](../virtual-machines/linux/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) e [Windows](../virtual-machines/windows/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) 
* [Impulsar tooAzure instâncias de trabalho com o HPC Pack](https://technet.microsoft.com/library/gg481749.aspx)
* [Impulsar tooAzure Batch com o HPC Pack](https://technet.microsoft.com/library/mt612877.aspx)
* [Fóruns do Windows HPC](https://social.microsoft.com/Forums/home?category=windowshpc)

### <a name="linux-and-oss-cluster-solutions"></a>Soluções de cluster do Linux e OSS
Utilize estas toodeploy de modelos do Azure clusters do Linux HPC.

* [Rotação de segurança de um cluster SLURM](https://azure.microsoft.com/documentation/templates/slurm/) e [mensagem de blogue](http://blogs.technet.com/b/windowshpc/archive/2015/06/06/deploy-a-slurm-cluster-on-azure.aspx)
* [Rotação de segurança de um cluster de Torque](https://azure.microsoft.com/documentation/templates/torque-cluster/)
* [Modelos de grelha de computação com PBS Professional](https://github.com/xpillons/azure-hpc/tree/master/Compute-Grid-Infra)

## <a name="hpc-storage"></a>Armazenamento HPC
* [Sistemas de ficheiros paralelas para armazenamento HPC no Azure](https://blogs.msdn.microsoft.com/azurecat/2017/03/17/parallel-file-systems-for-hpc-storage-on-azure/)
* [Edição de nuvem Intel para Software Lustre - aval](https://azure.microsoft.com/marketplace/partners/intel/lustre-cloud-edition-evaleval-lustre-2-7/)
* [BeeGFS no modelo de CentOS 7.2](https://github.com/smith1511/hpc/tree/master/beegfs-shared-on-centos7.2)




## <a name="microsoft-mpi"></a>Microsoft MPI
[Microsoft MPI](https://msdn.microsoft.com/library/bb524831.aspx) (MS-MPI) é uma implementação Microsoft da Olá Interface de passagem de mensagens standard para desenvolver e executar aplicações paralelas na plataforma do Windows hello.

* [Transferir MS MPI](http://go.microsoft.com/FWLink/p/?LinkID=389556)
* [Referência de MS MPI](https://msdn.microsoft.com/library/dn473458.aspx)
* [Fórum MPI](https://social.microsoft.com/Forums/en-us/home?forum=windowshpcmpi)

## <a name="compute-intensive-instances"></a>Instâncias de computação intensiva
Ofertas do Azure um [tamanhos de intervalo de VM](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json), incluindo [intensivas de computação H-série](../virtual-machines/windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) instâncias com capacidade para a ligação de rede RDMA de back-end tooa, toorun as cargas de trabalho de Linux e Windows HPC. 

* [Configurar um Linux RDMA cluster toorun MPI aplicações](../virtual-machines/linux/classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [Configurar um cluster do Windows RDMA com aplicações do Microsoft HPC Pack toorun MPI](../virtual-machines/windows/classic/hpcpack-rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

Para cargas de trabalho de GPU intensivas, veja [tamanhos de NC e NV](https://azure.microsoft.com/blog/azure-n-series-general-availability-on-december-1/).

## <a name="samples-and-demos"></a>Exemplos e demonstrações
* [Exemplos de código do Azure Batch c# e Python](https://github.com/Azure/azure-batch-samples)
* [Lote Shipyard](https://azure.github.io/batch-shipyard/) toolkit para facilitar a implementação de estilo batch Dockerized cargas de trabalho tooAzure Batch
* [doAzureParallel](http://www.github.com/Azure/doAzureParallel) pacote de R, desenvolvida do Azure Batch
* [Testar o SUSE Linux Enterprise Server para HPC](https://azure.microsoft.com/marketplace/partners/suse/suselinuxenterpriseserver12optimizedforhighperformancecompute/)

## <a name="related-azure-services"></a>Serviços relacionados do Azure
* [Data Factory](https://azure.microsoft.com/documentation/services/data-factory/)
* [Machine Learning](https://azure.microsoft.com/documentation/services/machine-learning/)
* [HDInsight](https://azure.microsoft.com/documentation/services/hdinsight/)
* [Máquinas Virtuais](https://azure.microsoft.com/documentation/services/virtual-machines/)
* [Conjuntos de Dimensionamento de Máquinas Virtuais](https://azure.microsoft.com/documentation/services/virtual-machine-scale-sets/)
* [Serviços Cloud](https://azure.microsoft.com/documentation/services/cloud-services/)
* [Serviço de Aplicações](https://azure.microsoft.com/documentation/services/app-service/)
* [Serviços de Multimédia](https://azure.microsoft.com/documentation/services/media-services/)
* [Funções](https://azure.microsoft.com/documentation/services/functions/)

## <a name="architecture-blueprints"></a>Esquemas de arquitetura
* [Orquestração HPC e dados utilizando o Azure Batch e do Azure Data Factory](http://go.microsoft.com/fwlink/?linkid=717686) (PDF) e [artigo](../data-factory/data-factory-data-processing-using-batch.md)

## <a name="industry-solutions"></a>Soluções de setor
* [Bancos e capital mercados](https://finance.azure.com/)
* [Simulações de engenharia](https://simulation.azure.com/) 

## <a name="customer-stories"></a>Histórias dos clientes
* [ANEO](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=4168) 
* [d3View](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=22088)
* [Ludwig Institute de Cancer Research](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=5830)
* [Microsoft Research](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=15634)
* [Milliman](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=14967)
* [Mitsubishi UFJ Securities internacional](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=26266)
* [Schlumberger](http://azure.microsoft.com/blog/big-compute-for-large-engineering-simulations)
* [Towers Watson](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=18222)
* [UberCloud](https://simulation.azure.com/casestudies/Team-182-ABB-UC-Final.pdf)

## <a name="next-steps"></a>Passos seguintes
* Para os anúncios mais recentes Olá, consulte o artigo Olá [blogue da equipa do Microsoft HPC e Batch](http://blogs.technet.com/b/windowshpc/) e Olá [blogue do Azure](https://azure.microsoft.com/blog/tag/hpc/).
* Consulte também [Novidades Batch](https://azure.microsoft.com/updates/?service=batch) ou subscrever toohello [RSS feed](https://azure.microsoft.com/updates/feed/?service=batch).

