---
title: aaaPowerShell script toodeploy cluster HPC do Linux | Microsoft Docs
description: "Executar um toodeploy de script do PowerShell de um cluster do Linux HPC Pack 2012 R2 em máquinas virtuais do Azure"
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-service-management,hpc-pack
ms.assetid: 73041960-58d3-4ecf-9540-d7e1a612c467
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: big-compute
ms.date: 12/29/2016
ms.author: danlep
ms.openlocfilehash: 885b03fa2fd604827dc388803fc21debab730979
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-linux-high-performance-computing-hpc-cluster-with-hello-hpc-pack-iaas-deployment-script"></a><span data-ttu-id="72556-103">Criar um cluster de computação de alto desempenho (HPC) do Linux com script de implementação de HPC Pack IaaS Olá</span><span class="sxs-lookup"><span data-stu-id="72556-103">Create a Linux high-performance computing (HPC) cluster with hello HPC Pack IaaS deployment script</span></span>
<span data-ttu-id="72556-104">Execute toodeploy de script do PowerShell de implementação do Olá HPC Pack IaaS um cluster HPC Pack 2012 R2 completado para cargas de trabalho do Linux em máquinas virtuais do Azure.</span><span class="sxs-lookup"><span data-stu-id="72556-104">Run hello HPC Pack IaaS deployment PowerShell script toodeploy a complete HPC Pack 2012 R2 cluster for Linux workloads in Azure virtual machines.</span></span> <span data-ttu-id="72556-105">cluster de Olá é composta por um nó principal associados ao Active Directory com o Windows Server e o Microsoft HPC Pack e nós de computação que execute um dos Olá distribuições Linux suportadas pelo pacote HPC.</span><span class="sxs-lookup"><span data-stu-id="72556-105">hello cluster consists of an Active Directory-joined head node running Windows Server and Microsoft HPC Pack, and compute nodes that run one of hello Linux distributions supported by HPC Pack.</span></span> <span data-ttu-id="72556-106">Se quiser toodeploy um cluster HPC Pack em cargas de trabalho do Azure para Windows, consulte [criar um cluster Windows HPC com Olá script de implementação de HPC Pack IaaS](../../windows/classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="72556-106">If you want toodeploy an HPC Pack cluster in Azure for Windows workloads, see [Create a Windows HPC cluster with hello HPC Pack IaaS deployment script](../../windows/classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span> <span data-ttu-id="72556-107">Também pode utilizar um toodeploy de modelo do Azure Resource Manager um cluster HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="72556-107">You can also use an Azure Resource Manager template toodeploy an HPC Pack cluster.</span></span> <span data-ttu-id="72556-108">Por exemplo, consulte [criar um cluster HPC connosco de computação do Linux](https://azure.microsoft.com/documentation/templates/create-hpc-cluster-linux-cn/).</span><span class="sxs-lookup"><span data-stu-id="72556-108">For an example, see [Create an HPC cluster with Linux compute nodes](https://azure.microsoft.com/documentation/templates/create-hpc-cluster-linux-cn/).</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="72556-109">Olá script do PowerShell descrito neste artigo cria um cluster do Microsoft HPC Pack 2012 R2 no Azure utilizando o modelo de implementação clássica Olá.</span><span class="sxs-lookup"><span data-stu-id="72556-109">hello PowerShell script described in this article creates a Microsoft HPC Pack 2012 R2 cluster in Azure using hello classic deployment model.</span></span> <span data-ttu-id="72556-110">A Microsoft recomenda que as implementações mais novas utilizem o modelo de Gestor de recursos de Olá.</span><span class="sxs-lookup"><span data-stu-id="72556-110">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>
> <span data-ttu-id="72556-111">Além disso, o script Olá descrito neste artigo não suporta o HPC Pack 2016.</span><span class="sxs-lookup"><span data-stu-id="72556-111">In addition, hello script described in this article does not support HPC Pack 2016.</span></span>

[!INCLUDE [virtual-machines-common-classic-hpcpack-cluster-powershell-script](../../../../includes/virtual-machines-common-classic-hpcpack-cluster-powershell-script.md)]

## <a name="example-configuration-file"></a><span data-ttu-id="72556-112">Ficheiro de configuração de exemplo</span><span class="sxs-lookup"><span data-stu-id="72556-112">Example configuration file</span></span>
<span data-ttu-id="72556-113">Olá seguinte ficheiro de configuração cria um controlador de domínio e floresta de domínio e implementa um cluster HPC Pack que tem um nó principal com bases de dados locais e 10 nós de computação do Linux.</span><span class="sxs-lookup"><span data-stu-id="72556-113">hello following configuration file creates a domain controller and domain forest and deploys an HPC Pack cluster which has one head node with local databases and 10 Linux compute nodes.</span></span> <span data-ttu-id="72556-114">Todos os serviços de cloud Olá são criados diretamente no Oriental como localização Olá.</span><span class="sxs-lookup"><span data-stu-id="72556-114">All hello cloud services are created directly in hello East Asia location.</span></span> <span data-ttu-id="72556-115">Olá nós de computação do Linux são criados em dois serviços de nuvem e duas contas de armazenamento (ou seja, *MyLnxCN-0001 e* para *MyLnxCN 0005* no *MyLnxCNService01* e *mylnxstorage01*, e *MyLnxCN 0006* para *MyLnxCN 0010* no *MyLnxCNService02* e *mylnxstorage02* ).</span><span class="sxs-lookup"><span data-stu-id="72556-115">hello Linux compute nodes are created in two cloud services and two storage accounts (that is, *MyLnxCN-0001* to *MyLnxCN-0005* in *MyLnxCNService01* and *mylnxstorage01*, and *MyLnxCN-0006* to *MyLnxCN-0010* in *MyLnxCNService02* and *mylnxstorage02*).</span></span> <span data-ttu-id="72556-116">nós de computação Olá são criados a partir de uma imagem de Linux do OpenLogic CentOS versão 7.0.</span><span class="sxs-lookup"><span data-stu-id="72556-116">hello compute nodes are created from an OpenLogic CentOS version 7.0 Linux image.</span></span> 

<span data-ttu-id="72556-117">Substitua os seus próprios valores para o nome da subscrição e os nomes de conta e o serviço de Olá.</span><span class="sxs-lookup"><span data-stu-id="72556-117">Substitute your own values for your subscription name and hello account and service names.</span></span>

```Xml
<?xml version="1.0" encoding="utf-8" ?>
<IaaSClusterConfig>
  <Subscription>
    <SubscriptionName>Subscription-1</SubscriptionName>
    <StorageAccount>mystorageaccount</StorageAccount>
  </Subscription>
  <Location>East Asia</Location>  
  <VNet>
    <VNetName>MyVNet</VNetName>
    <SubnetName>Subnet-1</SubnetName>
  </VNet>
  <Domain>
    <DCOption>NewDC</DCOption>
    <DomainFQDN>hpc.local</DomainFQDN>
    <DomainController>
      <VMName>MyDCServer</VMName>
      <ServiceName>MyHPCService</ServiceName>
      <VMSize>Large</VMSize>
    </DomainController>
  </Domain>
  <Database>
    <DBOption>LocalDB</DBOption>
  </Database>
  <HeadNode>
    <VMName>MyHeadNode</VMName>
    <ServiceName>MyHPCService</ServiceName>
    <VMSize>ExtraLarge</VMSize>
  </HeadNode>
  <LinuxComputeNodes>
    <VMNamePattern>MyLnxCN-%0001%</VMNamePattern>
    <ServiceNamePattern>MyLnxCNService%01%</ServiceNamePattern>
    <MaxNodeCountPerService>5</MaxNodeCountPerService>
    <StorageAccountNamePattern>mylnxstorage%01%</StorageAccountNamePattern>
    <VMSize>Medium</VMSize>
    <NodeCount>10</NodeCount>
    <ImageName>5112500ae3b842c8b9c604889f8753c3__OpenLogic-CentOS-70-20150325 </ImageName>
  </LinuxComputeNodes>
</IaaSClusterConfig>
```
## <a name="troubleshooting"></a><span data-ttu-id="72556-118">Resolução de problemas</span><span class="sxs-lookup"><span data-stu-id="72556-118">Troubleshooting</span></span>
* <span data-ttu-id="72556-119">**Erro "Não existe VNet"**.</span><span class="sxs-lookup"><span data-stu-id="72556-119">**“VNet doesn’t exist” error**.</span></span> <span data-ttu-id="72556-120">Se executar toodeploy de script de implementação de HPC Pack IaaS Olá vários clusters no Azure em simultâneo com uma subscrição, uma ou mais implementações podem falhar com o erro de Olá "VNet *VNet\_nome* não existe".</span><span class="sxs-lookup"><span data-stu-id="72556-120">If you run hello HPC Pack IaaS deployment script toodeploy multiple clusters in Azure concurrently under one subscription, one or more deployments may fail with hello error “VNet *VNet\_Name* doesn't exist”.</span></span>
  <span data-ttu-id="72556-121">Se este erro ocorrer, volte a executar script de Olá Olá falha na implementação.</span><span class="sxs-lookup"><span data-stu-id="72556-121">If this error occurs, rerun hello script for hello failed deployment.</span></span>
* <span data-ttu-id="72556-122">**Problema ao aceder ao hello Internet da rede virtual do Azure de Olá**.</span><span class="sxs-lookup"><span data-stu-id="72556-122">**Problem accessing hello Internet from hello Azure virtual network**.</span></span> <span data-ttu-id="72556-123">Se criar um cluster HPC Pack com um novo controlador de domínio utilizando o script de implementação hello, ou manualmente promover um controlador de toodomain VM de nó principal, podem ocorrer problemas de ligação Olá VMs na rede virtual do Azure de Olá toohello Internet.</span><span class="sxs-lookup"><span data-stu-id="72556-123">If you create an HPC Pack cluster with a new domain controller by using hello deployment script, or you manually promote a head node VM toodomain controller, you may experience problems connecting hello VMs in hello Azure virtual network toohello Internet.</span></span> <span data-ttu-id="72556-124">Isto pode ocorrer se um servidor DNS do reencaminhador é automaticamente configurado no controlador de domínio Olá, e este servidor DNS do reencaminhador não resolve corretamente.</span><span class="sxs-lookup"><span data-stu-id="72556-124">This can occur if a forwarder DNS server is automatically configured on hello domain controller, and this forwarder DNS server doesn’t resolve properly.</span></span>
  
    <span data-ttu-id="72556-125">toowork em torno este problema, inicie sessão no controlador de domínio de toohello e a definição de configuração do reencaminhador de Olá remover ou configurar um servidor DNS do reencaminhador válido.</span><span class="sxs-lookup"><span data-stu-id="72556-125">toowork around this problem, log on toohello domain controller and either remove hello forwarder configuration setting or configure a valid forwarder DNS server.</span></span> <span data-ttu-id="72556-126">toodo, clique no Gestor de servidor **ferramentas** > **DNS** tooopen Gestor de DNS e, em seguida, faça duplo clique **reencaminhadores**.</span><span class="sxs-lookup"><span data-stu-id="72556-126">toodo this, in Server Manager click **Tools** > **DNS** tooopen DNS Manager, and then double-click **Forwarders**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="72556-127">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="72556-127">Next steps</span></span>
* <span data-ttu-id="72556-128">Consulte [começar connosco de computação do Linux num cluster HPC Pack no Azure](hpcpack-cluster.md) para obter informações sobre as distribuições Linux suportadas, mover dados e a submissão de cluster HPC Pack de tooan de tarefas com o Linux nós de computação.</span><span class="sxs-lookup"><span data-stu-id="72556-128">See [Get started with Linux compute nodes in an HPC Pack cluster in Azure](hpcpack-cluster.md) for information about supported Linux distributions, moving data, and submitting jobs tooan HPC Pack cluster with Linux compute nodes.</span></span>
* <span data-ttu-id="72556-129">Para tutoriais que utilizam Olá script toocreate um cluster e executam uma carga de trabalho do Linux HPC, consulte:</span><span class="sxs-lookup"><span data-stu-id="72556-129">For tutorials that use hello script toocreate a cluster and run a Linux HPC workload, see:</span></span>
  * [<span data-ttu-id="72556-130">Executar NAMD com o Microsoft HPC Pack em nós de computação do Linux no Azure</span><span class="sxs-lookup"><span data-stu-id="72556-130">Run NAMD with Microsoft HPC Pack on Linux compute nodes in Azure</span></span>](hpcpack-cluster-namd.md)
  * [<span data-ttu-id="72556-131">Executar OpenFOAM com o Microsoft HPC Pack em nós de computação do Linux no Azure</span><span class="sxs-lookup"><span data-stu-id="72556-131">Run OpenFOAM with Microsoft HPC Pack on Linux compute nodes in Azure</span></span>](hpcpack-cluster-openfoam.md)
  * [<span data-ttu-id="72556-132">Executar ESTRELA-CCM + com o Microsoft HPC Pack no Linux nós de computação no Azure</span><span class="sxs-lookup"><span data-stu-id="72556-132">Run STAR-CCM+ with Microsoft HPC Pack on Linux compute nodes in Azure</span></span>](hpcpack-cluster-starccm.md)

