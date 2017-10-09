---
title: "aaaLinux computação VMs num cluster HPC Pack | Microsoft Docs"
description: "Saiba como toocreate e utilizar um pacote HPC cluster no Azure para Linux elevado desempenho informática cargas de trabalho (HPC)"
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager,hpc-pack
ms.assetid: 4d080fdd-5ffe-4f54-a78d-4c818f6eb3fb
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: big-compute
ms.date: 10/12/2016
ms.author: danlep
ms.openlocfilehash: 9ed20d6cd69a6472a00666caf8965e9d022698a6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-linux-compute-nodes-in-an-hpc-pack-cluster-in-azure"></a><span data-ttu-id="7e0b6-103">Introdução aos nós de computação do Linux num cluster HPC Pack no Azure</span><span class="sxs-lookup"><span data-stu-id="7e0b6-103">Get started with Linux compute nodes in an HPC Pack cluster in Azure</span></span>
<span data-ttu-id="7e0b6-104">Configurar um [Microsoft HPC Pack](https://technet.microsoft.com/library/cc514029.aspx) com uma distribuição Linux suportada de nós de computação de cluster no Azure que contém um nó principal com o Windows Server e várias.</span><span class="sxs-lookup"><span data-stu-id="7e0b6-104">Set up a [Microsoft HPC Pack](https://technet.microsoft.com/library/cc514029.aspx) cluster in Azure that contains a head node running Windows Server and several compute nodes running a supported Linux distribution.</span></span> <span data-ttu-id="7e0b6-105">Explore os dados de toomove de opções entre os nós do Linux Olá e nó principal de Windows hello do cluster de Olá.</span><span class="sxs-lookup"><span data-stu-id="7e0b6-105">Explore options toomove data among hello Linux nodes and hello Windows head node of hello cluster.</span></span> <span data-ttu-id="7e0b6-106">Saiba como toosubmit Linux HPC tarefas toohello cluster.</span><span class="sxs-lookup"><span data-stu-id="7e0b6-106">Learn how toosubmit Linux HPC jobs toohello cluster.</span></span>

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="7e0b6-107">Um nível elevado, hello diagrama seguinte mostra cluster HPC Pack de Olá criar e trabalhar com.</span><span class="sxs-lookup"><span data-stu-id="7e0b6-107">At a high level, hello following diagram shows hello HPC Pack cluster you create and work with.</span></span>

![Cluster de pacote HPC connosco do Linux][scenario]

<span data-ttu-id="7e0b6-109">Para outra opções toorun Linux HPC cargas de trabalho no Azure, consulte [recursos técnicos para batch e computação de alto desempenho](../../../batch/big-compute-resources.md).</span><span class="sxs-lookup"><span data-stu-id="7e0b6-109">For other options toorun Linux HPC workloads in Azure, see [Technical resources for batch and high-performance computing](../../../batch/big-compute-resources.md).</span></span>

## <a name="deploy-an-hpc-pack-cluster-with-linux-compute-nodes"></a><span data-ttu-id="7e0b6-110">Implementar um cluster de pacote HPC connosco de computação do Linux</span><span class="sxs-lookup"><span data-stu-id="7e0b6-110">Deploy an HPC Pack cluster with Linux compute nodes</span></span>
<span data-ttu-id="7e0b6-111">Este artigo mostra duas opções toodeploy um cluster HPC Pack no Azure connosco de computação do Linux.</span><span class="sxs-lookup"><span data-stu-id="7e0b6-111">This article shows you two options toodeploy an HPC Pack cluster in Azure with Linux compute nodes.</span></span> <span data-ttu-id="7e0b6-112">Ambos os métodos de utilizam uma imagem do Marketplace do Windows Server com o nó principal do HPC Pack toocreate Olá.</span><span class="sxs-lookup"><span data-stu-id="7e0b6-112">Both methods use a Marketplace image of Windows Server with HPC Pack toocreate hello head node.</span></span> 

* <span data-ttu-id="7e0b6-113">**Modelo Azure Resource Manager** -utilizar um modelo a partir do Olá Azure Marketplace ou um modelo de início rápido da Comunidade Olá, tooautomate a criação do cluster de Olá no modelo de implementação do Resource Manager Olá.</span><span class="sxs-lookup"><span data-stu-id="7e0b6-113">**Azure Resource Manager template** - Use a template from hello Azure Marketplace, or a quickstart template from hello community, tooautomate creation of hello cluster in hello Resource Manager deployment model.</span></span> <span data-ttu-id="7e0b6-114">Por exemplo, Olá [cluster HPC Pack para cargas de trabalho do Linux](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/) modelo no Olá Azure Marketplace cria uma infraestrutura de cluster HPC Pack concluída para o Linux HPC cargas de trabalho.</span><span class="sxs-lookup"><span data-stu-id="7e0b6-114">For example, hello [HPC Pack cluster for Linux workloads](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/) template in hello Azure Marketplace creates a complete HPC Pack cluster infrastructure for Linux HPC workloads.</span></span>
* <span data-ttu-id="7e0b6-115">**Script do PowerShell** -Olá utilize [script de implementação do Microsoft HPC Pack IaaS](../../windows/classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) (**New-HpcIaaSCluster.ps1**) tooautomate uma implementação completa do cluster no modelo de implementação clássica Olá.</span><span class="sxs-lookup"><span data-stu-id="7e0b6-115">**PowerShell script** - Use hello [Microsoft HPC Pack IaaS deployment script](../../windows/classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) (**New-HpcIaaSCluster.ps1**) tooautomate a complete cluster deployment in hello classic deployment model.</span></span> <span data-ttu-id="7e0b6-116">Este script do PowerShell do Azure utiliza uma imagem de VM de pacote HPC no Olá Azure Marketplace para a implementação rápida e fornece um conjunto abrangente de toodeploy de parâmetros de configuração de nós de computação do Linux.</span><span class="sxs-lookup"><span data-stu-id="7e0b6-116">This Azure PowerShell script uses an HPC Pack VM image in hello Azure Marketplace for fast deployment and provides a comprehensive set of configuration parameters toodeploy Linux compute nodes.</span></span>

<span data-ttu-id="7e0b6-117">Para obter mais informações sobre as opções de implementação de cluster HPC Pack no Azure, consulte [opções toocreate e gerir um cluster de computação de alto desempenho (HPC) no Azure com o Microsoft HPC Pack](../hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="7e0b6-117">For more information about HPC Pack cluster deployment options in Azure, see [Options toocreate and manage a high-performance computing (HPC) cluster in Azure with Microsoft HPC Pack](../hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

### <a name="prerequisites"></a><span data-ttu-id="7e0b6-118">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="7e0b6-118">Prerequisites</span></span>
* <span data-ttu-id="7e0b6-119">**Subscrição do Azure** -pode utilizar uma subscrição em qualquer um dos Olá serviço Global do Azure ou do Azure China.</span><span class="sxs-lookup"><span data-stu-id="7e0b6-119">**Azure subscription** - You can use a subscription in either hello Azure Global or Azure China service.</span></span> <span data-ttu-id="7e0b6-120">Se não tiver uma conta, pode criar um [conta gratuita](https://azure.microsoft.com/pricing/free-trial/) em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="7e0b6-120">If you don't have an account, you can create a [free account](https://azure.microsoft.com/pricing/free-trial/) in just a couple of minutes.</span></span>
* <span data-ttu-id="7e0b6-121">**Quota de núcleos** -poderá ter de quota de Olá tooincrease de núcleos, especialmente se optar por toodeploy vários nós do cluster sem especializados tamanhos de VM.</span><span class="sxs-lookup"><span data-stu-id="7e0b6-121">**Cores quota** - You might need tooincrease hello quota of cores, especially if you choose toodeploy several cluster nodes with multicore VM sizes.</span></span> <span data-ttu-id="7e0b6-122">tooincrease uma quota, abra um pedido de suporte online do cliente, sem encargos.</span><span class="sxs-lookup"><span data-stu-id="7e0b6-122">tooincrease a quota, open an online customer support request at no charge.</span></span>
* <span data-ttu-id="7e0b6-123">**As distribuições do Linux** -atualmente HPC Pack suporta Olá seguir as distribuições do Linux para nós de computação.</span><span class="sxs-lookup"><span data-stu-id="7e0b6-123">**Linux distributions** - Currently HPC Pack supports hello following Linux distributions for compute nodes.</span></span> <span data-ttu-id="7e0b6-124">Pode utilizar Marketplace as versões destes distribuições, quando disponíveis, ou forneça o seu próprio.</span><span class="sxs-lookup"><span data-stu-id="7e0b6-124">You can use Marketplace versions of these distributions where available, or supply your own.</span></span>
  
  * <span data-ttu-id="7e0b6-125">**Com base em centOS**: 6.5 6.6, 6.7, 7.0, 7.1, 7.2, 6.5 HPC, 7.1 HPC</span><span class="sxs-lookup"><span data-stu-id="7e0b6-125">**CentOS-based**: 6.5, 6.6, 6.7, 7.0, 7.1, 7.2, 6.5 HPC, 7.1 HPC</span></span>
  * <span data-ttu-id="7e0b6-126">**Red Hat Enterprise Linux**: 6.7, 6.8, 7.2</span><span class="sxs-lookup"><span data-stu-id="7e0b6-126">**Red Hat Enterprise Linux**: 6.7, 6.8, 7.2</span></span>
  * <span data-ttu-id="7e0b6-127">**SUSE Linux Enterprise Server**: SLES 12 SLES 12 (Premium), SLES 12 SP1, SLES 12 SP1 (Premium), SLES 12 para HPC, SLES 12 para HPC (Premium)</span><span class="sxs-lookup"><span data-stu-id="7e0b6-127">**SUSE Linux Enterprise Server**: SLES 12, SLES 12 (Premium), SLES 12 SP1, SLES 12 SP1 (Premium), SLES 12 for HPC, SLES 12 for HPC (Premium)</span></span>
  * <span data-ttu-id="7e0b6-128">**Ubuntu Server**: 14.04 LTS, 16.04 LTS</span><span class="sxs-lookup"><span data-stu-id="7e0b6-128">**Ubuntu Server**: 14.04 LTS, 16.04 LTS</span></span>
    
    > [!TIP]
    > <span data-ttu-id="7e0b6-129">rede de Azure RDMA Olá toouse com um dos tamanhos de VM Olá com capacidade RDMA, especifique uma imagem do SUSE Linux Enterprise Server 12 HPC ou baseada em CentOS HPC de Olá Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="7e0b6-129">toouse hello Azure RDMA network with one of hello RDMA-capable VM sizes, specify a SUSE Linux Enterprise Server 12 HPC or CentOS-based HPC image from hello Azure Marketplace.</span></span> <span data-ttu-id="7e0b6-130">Para obter mais informações, consulte [tamanhos de VM de computação de elevado desempenho](../sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="7e0b6-130">For more information, see [High performance compute VM sizes](../sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
    > 
    > 

<span data-ttu-id="7e0b6-131">Pré-requisitos adicionais toodeploy Olá cluster utilizando o script de implementação de HPC Pack IaaS Olá:</span><span class="sxs-lookup"><span data-stu-id="7e0b6-131">Additional prerequisites toodeploy hello cluster by using hello HPC Pack IaaS deployment script:</span></span>

* <span data-ttu-id="7e0b6-132">**Computador cliente** -precisa de um script de implementação do cliente baseada em Windows computador toorun Olá cluster.</span><span class="sxs-lookup"><span data-stu-id="7e0b6-132">**Client computer** - You need a Windows-based client computer toorun hello cluster deployment script.</span></span>
* <span data-ttu-id="7e0b6-133">**O Azure PowerShell** - [instalar e configurar o Azure PowerShell](/powershell/azure/overview) (versão 0.8.10 ou posterior) no computador cliente.</span><span class="sxs-lookup"><span data-stu-id="7e0b6-133">**Azure PowerShell** - [Install and configure Azure PowerShell](/powershell/azure/overview) (version 0.8.10 or later) on your client computer.</span></span>
* <span data-ttu-id="7e0b6-134">**Script de implementação de HPC Pack IaaS** - transferir e Descompacte a versão mais recente do Olá do script de Olá no Olá [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=44949).</span><span class="sxs-lookup"><span data-stu-id="7e0b6-134">**HPC Pack IaaS deployment script** - Download and unpack hello latest version of hello script from hello [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=44949).</span></span> <span data-ttu-id="7e0b6-135">Pode verificar a versão de Olá do script Olá executando `.\New-HPCIaaSCluster.ps1 –Version`.</span><span class="sxs-lookup"><span data-stu-id="7e0b6-135">You can check hello version of hello script by running `.\New-HPCIaaSCluster.ps1 –Version`.</span></span> <span data-ttu-id="7e0b6-136">Este artigo baseia-se numa versão 4.4.1 ou posterior do script de Olá.</span><span class="sxs-lookup"><span data-stu-id="7e0b6-136">This article is based on version 4.4.1 or later of hello script.</span></span>

### <a name="deployment-option-1-use-a-resource-manager-template"></a><span data-ttu-id="7e0b6-137">Opção de implementação 1.</span><span class="sxs-lookup"><span data-stu-id="7e0b6-137">Deployment option 1.</span></span> <span data-ttu-id="7e0b6-138">Utilizar um modelo do Resource Manager</span><span class="sxs-lookup"><span data-stu-id="7e0b6-138">Use a Resource Manager template</span></span>
1. <span data-ttu-id="7e0b6-139">Aceda toohello [cluster HPC Pack para cargas de trabalho do Linux](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/) modelo no Olá Azure Marketplace e clique em **implementar**.</span><span class="sxs-lookup"><span data-stu-id="7e0b6-139">Go toohello [HPC Pack cluster for Linux workloads](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/) template in hello Azure Marketplace, and click **Deploy**.</span></span>
2. <span data-ttu-id="7e0b6-140">No Olá portal do Azure, reveja as informações de Olá e, em seguida, clique em **criar**.</span><span class="sxs-lookup"><span data-stu-id="7e0b6-140">In hello Azure portal, review hello information and then click **Create**.</span></span>
   
    ![Criação do portal][portal]
3. <span data-ttu-id="7e0b6-142">No Olá **Noções básicas** painel, introduza um nome para o cluster Olá, que também os nomes de nó principal do Olá VM.</span><span class="sxs-lookup"><span data-stu-id="7e0b6-142">On hello **Basics** blade, enter a name for hello cluster, which also names hello head node VM.</span></span> <span data-ttu-id="7e0b6-143">Pode escolher um grupo de recursos existente ou crie um grupo para implementação de Olá numa localização que seja tooyou disponível.</span><span class="sxs-lookup"><span data-stu-id="7e0b6-143">You can choose an existing resource group or create a group for hello deployment in a location that's available tooyou.</span></span> <span data-ttu-id="7e0b6-144">Olá localização afeta a disponibilidade de Olá de determinados tamanhos de VM e outros serviços do Azure (consulte [produtos disponíveis por região](https://azure.microsoft.com/regions/services/)).</span><span class="sxs-lookup"><span data-stu-id="7e0b6-144">hello location affects hello availability of certain VM sizes and other Azure services (see [Products available by region](https://azure.microsoft.com/regions/services/)).</span></span>
4. <span data-ttu-id="7e0b6-145">No Olá **aceda a definições de nó** painel, para uma primeira implementação, pode aceitar geralmente as predefinições de Olá.</span><span class="sxs-lookup"><span data-stu-id="7e0b6-145">On hello **Head node settings** blade, for a first deployment, you can generally accept hello default settings.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="7e0b6-146">Olá **URL de scripts pós-configuração** é opcional definição toospecify um script do Windows PowerShell publicamente disponível que pretende que toorun no nó principal do Olá VM depois de se encontra em execução.</span><span class="sxs-lookup"><span data-stu-id="7e0b6-146">hello **Post-configuration script URL** is an optional setting toospecify a publicly available Windows PowerShell script that you want toorun on hello head node VM after it is running.</span></span> 
   > 
   > 
5. <span data-ttu-id="7e0b6-147">No Olá **definições de nó de computação** painel, selecione um padrão de nomenclatura para nós de Olá, o número de Olá e o tamanho de nós de Olá e Olá toodeploy de distribuição de Linux.</span><span class="sxs-lookup"><span data-stu-id="7e0b6-147">On hello **Compute node settings** blade, select a naming pattern for hello nodes, hello number and size of hello nodes, and hello Linux distribution toodeploy.</span></span>
6. <span data-ttu-id="7e0b6-148">No Olá **as definições de infraestrutura** painel, introduza os nomes de rede virtual Olá e do Active Directory domínio, domínio e credenciais de administrador da VM e um padrão de nomenclatura Olá contas do storage.</span><span class="sxs-lookup"><span data-stu-id="7e0b6-148">On hello **Infrastructure settings** blade, enter names for hello virtual network and Active Directory domain, domain and VM administrator credentials, and a naming pattern for hello storage accounts.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="7e0b6-149">Pacote HPC utiliza Olá do Active Directory tooauthenticate cluster aos utilizadores de domínio.</span><span class="sxs-lookup"><span data-stu-id="7e0b6-149">HPC Pack uses hello Active Directory domain tooauthenticate cluster users.</span></span> 
   > 
   > 
7. <span data-ttu-id="7e0b6-150">Depois de executar testes de validação de Olá e reveja os termos de Olá de utilização, clique em **Compra**.</span><span class="sxs-lookup"><span data-stu-id="7e0b6-150">After hello validation tests run and you review hello terms of use, click **Purchase**.</span></span>

### <a name="deployment-option-2-use-hello-iaas-deployment-script"></a><span data-ttu-id="7e0b6-151">Opção de implementação 2.</span><span class="sxs-lookup"><span data-stu-id="7e0b6-151">Deployment option 2.</span></span> <span data-ttu-id="7e0b6-152">Utilizar script de implementação de IaaS Olá</span><span class="sxs-lookup"><span data-stu-id="7e0b6-152">Use hello IaaS deployment script</span></span>
<span data-ttu-id="7e0b6-153">Seguem-se cluster de Olá toodeploy de pré-requisitos adicionais utilizando o script de implementação de HPC Pack IaaS Olá:</span><span class="sxs-lookup"><span data-stu-id="7e0b6-153">Following are additional prerequisites toodeploy hello cluster by using hello HPC Pack IaaS deployment script:</span></span>

* <span data-ttu-id="7e0b6-154">**Computador cliente** -precisa de um script de implementação do cliente baseada em Windows computador toorun Olá cluster.</span><span class="sxs-lookup"><span data-stu-id="7e0b6-154">**Client computer** - You need a Windows-based client computer toorun hello cluster deployment script.</span></span>
* <span data-ttu-id="7e0b6-155">**O Azure PowerShell** - [instalar e configurar o Azure PowerShell](/powershell/azure/overview) (versão 0.8.10 ou posterior) no computador cliente.</span><span class="sxs-lookup"><span data-stu-id="7e0b6-155">**Azure PowerShell** - [Install and configure Azure PowerShell](/powershell/azure/overview) (version 0.8.10 or later) on your client computer.</span></span>
* <span data-ttu-id="7e0b6-156">**Script de implementação de HPC Pack IaaS** - transferir e Descompacte a versão mais recente do Olá do script de Olá no Olá [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=44949).</span><span class="sxs-lookup"><span data-stu-id="7e0b6-156">**HPC Pack IaaS deployment script** - Download and unpack hello latest version of hello script from hello [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=44949).</span></span> <span data-ttu-id="7e0b6-157">Pode verificar a versão de Olá do script Olá executando `.\New-HPCIaaSCluster.ps1 –Version`.</span><span class="sxs-lookup"><span data-stu-id="7e0b6-157">You can check hello version of hello script by running `.\New-HPCIaaSCluster.ps1 –Version`.</span></span> <span data-ttu-id="7e0b6-158">Este artigo baseia-se numa versão 4.4.1 ou posterior do script de Olá.</span><span class="sxs-lookup"><span data-stu-id="7e0b6-158">This article is based on version 4.4.1 or later of hello script.</span></span>

<span data-ttu-id="7e0b6-159">**Ficheiro de configuração XML**</span><span class="sxs-lookup"><span data-stu-id="7e0b6-159">**XML configuration file**</span></span>

<span data-ttu-id="7e0b6-160">Olá HPC Pack IaaS script de implementação utiliza um ficheiro de configuração XML, como cluster HPC Olá toodescribe de entrada.</span><span class="sxs-lookup"><span data-stu-id="7e0b6-160">hello HPC Pack IaaS deployment script uses an XML configuration file as input toodescribe hello  HPC cluster.</span></span> <span data-ttu-id="7e0b6-161">Olá seguinte ficheiro de configuração de exemplo Especifica um cluster pequeno constituída por um nó principal do HPC Pack e dois nós de computação do Linux do A7 CentOS 7.0 de tamanho.</span><span class="sxs-lookup"><span data-stu-id="7e0b6-161">hello following sample configuration file specifies a small cluster consisting of an HPC Pack head node and two size A7 CentOS 7.0 Linux compute nodes.</span></span> 

<span data-ttu-id="7e0b6-162">Modificar o ficheiro de Olá conforme necessário para o seu ambiente e a configuração de cluster pretendido e guarde-o com um nome, como HPCDemoConfig.xml.</span><span class="sxs-lookup"><span data-stu-id="7e0b6-162">Modify hello file as needed for your environment and desired cluster configuration, and save it with a name such as HPCDemoConfig.xml.</span></span> <span data-ttu-id="7e0b6-163">Por exemplo, terá de toosupply nome da sua subscrição e um nome de conta de armazenamento exclusivas e o nome do serviço em nuvem.</span><span class="sxs-lookup"><span data-stu-id="7e0b6-163">For example, you need toosupply your subscription name and a unique storage account name and cloud service name.</span></span> <span data-ttu-id="7e0b6-164">Além disso, poderá toochoose outro suportado Linux imagem Olá nós de computação.</span><span class="sxs-lookup"><span data-stu-id="7e0b6-164">Additionally, you might want toochoose a different supported Linux image for hello compute nodes.</span></span> <span data-ttu-id="7e0b6-165">Para obter mais informações sobre elementos Olá no ficheiro de configuração de Olá, consulte o ficheiro de Manual.rtf de Olá na pasta de script de Olá e [criar um cluster HPC com Olá script de implementação de HPC Pack IaaS](../../windows/classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="7e0b6-165">For more information about hello elements in hello configuration file, see hello Manual.rtf file in hello script folder and [Create an HPC cluster with hello HPC Pack IaaS deployment script](../../windows/classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

```
<?xml version="1.0" encoding="utf-8" ?>
<IaaSClusterConfig>
  <Subscription>
    <SubscriptionName>Subscription-1</SubscriptionName>
    <StorageAccount>allvhdsje</StorageAccount>
  </Subscription>
  <Location>Japan East</Location>  
  <VNet>
    <VNetName>centos7rdmavnetje</VNetName>
    <SubnetName>CentOS7RDMACluster</SubnetName>
  </VNet>
  <Domain>
    <DCOption>HeadNodeAsDC</DCOption>
    <DomainFQDN>hpc.local</DomainFQDN>
  </Domain>
  <Database>
    <DBOption>LocalDB</DBOption>
  </Database>
  <HeadNode>
    <VMName>CentOS7RDMA-HN</VMName>
    <ServiceName>centos7rdma-je</ServiceName>
  <VMSize>ExtraLarge</VMSize>
  <EnableRESTAPI />
  <EnableWebPortal />
  </HeadNode>
  <LinuxComputeNodes>
    <VMNamePattern>CentOS7RDMA-LN%1%</VMNamePattern>
    <ServiceName>centos7rdma-je</ServiceName>
    <VMSize>A7</VMSize>
    <NodeCount>2</NodeCount>
    <ImageName>5112500ae3b842c8b9c604889f8753c3__OpenLogic-CentOS-70-20150325</ImageName>
  </LinuxComputeNodes>
</IaaSClusterConfig>
```

<span data-ttu-id="7e0b6-166">**Olá toorun script de implementação do IaaS do HPC Pack**</span><span class="sxs-lookup"><span data-stu-id="7e0b6-166">**toorun hello HPC Pack IaaS deployment script**</span></span>

1. <span data-ttu-id="7e0b6-167">Abra o Windows PowerShell no computador de cliente Olá como administrador.</span><span class="sxs-lookup"><span data-stu-id="7e0b6-167">Open Windows PowerShell on hello client computer as an administrator.</span></span>
2. <span data-ttu-id="7e0b6-168">Alterar pasta do toohello diretório onde está o script de Olá instalado (E:\IaaSClusterScript neste exemplo).</span><span class="sxs-lookup"><span data-stu-id="7e0b6-168">Change directory toohello folder where hello script is installed (E:\IaaSClusterScript in this example).</span></span>
   
    ```powershell
    cd E:\IaaSClusterScript
    ```
3. <span data-ttu-id="7e0b6-169">Execute Olá cluster HPC Pack do comando toodeploy Olá a seguir.</span><span class="sxs-lookup"><span data-stu-id="7e0b6-169">Run hello following command toodeploy hello HPC Pack cluster.</span></span> <span data-ttu-id="7e0b6-170">Este exemplo assume que o ficheiro configuração Olá está localizado na E:\HPCDemoConfig.xml</span><span class="sxs-lookup"><span data-stu-id="7e0b6-170">This example assumes that hello configuration file is located in E:\HPCDemoConfig.xml</span></span>
   
    ```powershell
    .\New-HpcIaaSCluster.ps1 –ConfigFile E:\HPCDemoConfig.xml –AdminUserName MyAdminName
    ```
   
    <span data-ttu-id="7e0b6-171">a.</span><span class="sxs-lookup"><span data-stu-id="7e0b6-171">a.</span></span> <span data-ttu-id="7e0b6-172">Porque Olá **AdminPassword** não está especificado no Olá precedente comandos, é pedido tooenter Olá palavra-passe utilizador *MyAdminName*.</span><span class="sxs-lookup"><span data-stu-id="7e0b6-172">Because hello **AdminPassword** is not specified in hello preceding command, you are prompted tooenter hello password for user *MyAdminName*.</span></span>
   
    <span data-ttu-id="7e0b6-173">b.</span><span class="sxs-lookup"><span data-stu-id="7e0b6-173">b.</span></span> <span data-ttu-id="7e0b6-174">script de Olá, em seguida, inicia o ficheiro de configuração de Olá toovalidate.</span><span class="sxs-lookup"><span data-stu-id="7e0b6-174">hello script then starts toovalidate hello configuration file.</span></span> <span data-ttu-id="7e0b6-175">Pode demorar até tooseveral minutos dependendo da ligação de rede Olá.</span><span class="sxs-lookup"><span data-stu-id="7e0b6-175">It can take up tooseveral minutes depending on hello network connection.</span></span>
   
    ![Validação][validate]
   
    <span data-ttu-id="7e0b6-177">c.</span><span class="sxs-lookup"><span data-stu-id="7e0b6-177">c.</span></span> <span data-ttu-id="7e0b6-178">Depois de passaram validações, o script Olá lista toocreate de recursos de cluster Olá.</span><span class="sxs-lookup"><span data-stu-id="7e0b6-178">After validations pass, hello script lists hello cluster resources toocreate.</span></span> <span data-ttu-id="7e0b6-179">Introduza *Y* toocontinue.</span><span class="sxs-lookup"><span data-stu-id="7e0b6-179">Enter *Y* toocontinue.</span></span>
   
    ![Recursos][resources]
   
    <span data-ttu-id="7e0b6-181">d.</span><span class="sxs-lookup"><span data-stu-id="7e0b6-181">d.</span></span> <span data-ttu-id="7e0b6-182">script de Olá inicia toodeploy Olá HPC Pack cluster e concluir a configuração de Olá sem mais passos manuais.</span><span class="sxs-lookup"><span data-stu-id="7e0b6-182">hello script starts toodeploy hello HPC Pack cluster and completes hello configuration without further manual steps.</span></span> <span data-ttu-id="7e0b6-183">Pode executar o script de Olá durante vários minutos.</span><span class="sxs-lookup"><span data-stu-id="7e0b6-183">hello script can run for several minutes.</span></span>
   
    ![Implementação][deploy]
   
   > [!NOTE]
   > <span data-ttu-id="7e0b6-185">Neste exemplo, o script de Olá gera um ficheiro de registo automaticamente o desde Olá **- LogFile** parâmetro não está especificado.</span><span class="sxs-lookup"><span data-stu-id="7e0b6-185">In this example, hello script generates a log file automatically since hello **-LogFile** parameter isn't specified.</span></span> <span data-ttu-id="7e0b6-186">Olá registos não são escritos em tempo real, mas são recolhidos no fim de Olá de validação de Olá e implementação de Olá.</span><span class="sxs-lookup"><span data-stu-id="7e0b6-186">hello logs aren't written in real time, but are collected at hello end of hello validation and hello deployment.</span></span> <span data-ttu-id="7e0b6-187">Se Olá PowerShell processo for interrompido enquanto está a executar o script de Olá, alguns registos serão perdidos.</span><span class="sxs-lookup"><span data-stu-id="7e0b6-187">If hello PowerShell process is stopped while hello script is running, some logs are lost.</span></span>
   > 
   > 

## <a name="connect-toohello-head-node"></a><span data-ttu-id="7e0b6-188">Ligar o nó principal toohello</span><span class="sxs-lookup"><span data-stu-id="7e0b6-188">Connect toohello head node</span></span>
<span data-ttu-id="7e0b6-189">Depois de implementar um cluster HPC Pack de Olá no Azure, [estabelecer ligação ao ambiente de trabalho remoto](../../windows/connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) através de VM de nó principal do toohello Olá credenciais de domínio que forneceu quando implementou o cluster de Olá (por exemplo, *hpc\\ clusteradmin*).</span><span class="sxs-lookup"><span data-stu-id="7e0b6-189">After you deploy hello HPC Pack cluster in Azure, [connect by Remote Desktop](../../windows/connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) toohello head node VM using hello domain credentials you provided when you deployed hello cluster (for example, *hpc\\clusteradmin*).</span></span> <span data-ttu-id="7e0b6-190">Gerir o cluster de Olá do nó principal Olá.</span><span class="sxs-lookup"><span data-stu-id="7e0b6-190">You manage hello cluster from hello head node.</span></span>

<span data-ttu-id="7e0b6-191">No nó principal Olá, inicie o Gestor de clusters HPC toocheck Estado Olá cluster HPC Pack de Olá.</span><span class="sxs-lookup"><span data-stu-id="7e0b6-191">On hello head node, start HPC Cluster Manager toocheck hello status of hello HPC Pack cluster.</span></span> <span data-ttu-id="7e0b6-192">Pode gerir e monitorizar nós de computação do Linux hello mesma forma que trabalha com o Windows nós de computação.</span><span class="sxs-lookup"><span data-stu-id="7e0b6-192">You can manage and monitor Linux compute nodes hello same way you work with Windows compute nodes.</span></span> <span data-ttu-id="7e0b6-193">Por exemplo, consulte nós do Linux Olá listados no **gestão de recursos** (estes nós são implementados com Olá **LinuxNode** modelo).</span><span class="sxs-lookup"><span data-stu-id="7e0b6-193">For example, you see hello Linux nodes listed in **Resource Management** (these nodes are deployed with hello **LinuxNode** template).</span></span>

![Gestão de nó][management]

<span data-ttu-id="7e0b6-195">Consulte também nós Linux Olá Olá **mapa térmico** vista.</span><span class="sxs-lookup"><span data-stu-id="7e0b6-195">You also see hello Linux nodes in hello **Heat Map** view.</span></span>

![Mapa térmico][heatmap]

## <a name="how-toomove-data-in-a-cluster-with-linux-nodes"></a><span data-ttu-id="7e0b6-197">Como toomove dados num cluster connosco do Linux</span><span class="sxs-lookup"><span data-stu-id="7e0b6-197">How toomove data in a cluster with Linux nodes</span></span>
<span data-ttu-id="7e0b6-198">Tem vários dados de toomove escolhas entre os nós do Linux e o nó principal de Windows hello do cluster de Olá.</span><span class="sxs-lookup"><span data-stu-id="7e0b6-198">You have several choices toomove data among Linux nodes and hello Windows head node of hello cluster.</span></span> <span data-ttu-id="7e0b6-199">Seguem-se três métodos comuns, descritos com maior detalhe em Olá seguintes secções:</span><span class="sxs-lookup"><span data-stu-id="7e0b6-199">Here are three common methods, described in more detail in hello following sections:</span></span>

* <span data-ttu-id="7e0b6-200">**Ficheiros do Azure** -expõe um gerido toostore dados do SMB ficheiro partilha de ficheiros no armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="7e0b6-200">**Azure File** - Exposes a managed SMB file share toostore data files in Azure storage.</span></span> <span data-ttu-id="7e0b6-201">Nós do Windows e nós do Linux podem montar uma partilha de ficheiros do Azure como uma unidade ou pasta no Olá mesmo tempo, mesmo que está a ser implementados em redes virtuais diferentes.</span><span class="sxs-lookup"><span data-stu-id="7e0b6-201">Windows nodes and Linux nodes can mount an Azure File share as a drive or folder at hello same time, even if they're deployed in different virtual networks.</span></span>
* <span data-ttu-id="7e0b6-202">**Nó principal SMB partilhar** -monta uma pasta partilhada de Windows padrão de nó principal Olá em nós do Linux.</span><span class="sxs-lookup"><span data-stu-id="7e0b6-202">**Head node SMB share** - Mounts a standard Windows shared folder of hello head node on Linux nodes.</span></span>
* <span data-ttu-id="7e0b6-203">**O servidor NFS do head nó** -fornece uma solução de partilha de ficheiros para um ambiente misto do Windows e Linux.</span><span class="sxs-lookup"><span data-stu-id="7e0b6-203">**Head node NFS server**  - Provides a file-sharing solution for a mixed Windows and Linux environment.</span></span>

### <a name="azure-file-storage"></a><span data-ttu-id="7e0b6-204">File storage do Azure</span><span class="sxs-lookup"><span data-stu-id="7e0b6-204">Azure File storage</span></span>
<span data-ttu-id="7e0b6-205">Olá [ficheiros do Azure](https://azure.microsoft.com/services/storage/files/) serviço expõe partilhas de ficheiros utilizando o protocolo SMB 2.1 padrão do Olá.</span><span class="sxs-lookup"><span data-stu-id="7e0b6-205">hello [Azure File](https://azure.microsoft.com/services/storage/files/) service exposes file shares using hello standard SMB 2.1 protocol.</span></span> <span data-ttu-id="7e0b6-206">Serviços de nuvem e as VMs do Azure podem partilhar dados de ficheiros entre componentes da aplicação através de partilhas montadas e as aplicações no local podem aceder a dados de ficheiros numa partilha através de Olá API do armazenamento de ficheiros.</span><span class="sxs-lookup"><span data-stu-id="7e0b6-206">Azure VMs and cloud services can share file data across application components via mounted shares, and on-premises applications can access file data in a share through hello File storage API.</span></span> 

<span data-ttu-id="7e0b6-207">Para obter passos detalhados toocreate um ficheiro de Azure partilhar e montá-la no nó principal Olá, consulte [introdução ao File storage do Azure no Windows](../../../storage/files/storage-how-to-use-files-windows.md).</span><span class="sxs-lookup"><span data-stu-id="7e0b6-207">For detailed steps toocreate an Azure File share and mount it on hello head node, see [Get started with Azure File storage on Windows](../../../storage/files/storage-how-to-use-files-windows.md).</span></span> <span data-ttu-id="7e0b6-208">partilha de ficheiros de Azure Olá toomount nós do Linux Olá, consulte [como toouse File storage do Azure com o Linux](../../../storage/files/storage-how-to-use-files-linux.md).</span><span class="sxs-lookup"><span data-stu-id="7e0b6-208">toomount hello Azure File share on hello Linux nodes, see [How toouse Azure File storage with Linux](../../../storage/files/storage-how-to-use-files-linux.md).</span></span> <span data-ttu-id="7e0b6-209">tooset cópias de segurança persistentes ligações, consulte [Persisting ligações tooMicrosoft ficheiros do Azure](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/27/persisting-connections-to-microsoft-azure-files.aspx).</span><span class="sxs-lookup"><span data-stu-id="7e0b6-209">tooset up persisting connections, see [Persisting connections tooMicrosoft Azure Files](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/27/persisting-connections-to-microsoft-azure-files.aspx).</span></span>

<span data-ttu-id="7e0b6-210">No seguinte exemplo de Olá, crie uma partilha de ficheiros do Azure numa conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="7e0b6-210">In hello following example, create an Azure File share on a storage account.</span></span> <span data-ttu-id="7e0b6-211">Olá toomount partilha em Olá nó principal, abra uma linha de comandos e introduza Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="7e0b6-211">toomount hello share on hello head node, open a Command Prompt and enter hello following commands:</span></span>

```command
cmdkey /add:allvhdsje.file.core.windows.net /user:allvhdsje /pass:<storageaccountkey>

net use Z: \\allvhdje.file.core.windows.net\rdma /persistent:yes
```

<span data-ttu-id="7e0b6-212">Neste exemplo, allvhdsje é o nome da sua conta de armazenamento, storageaccountkey é a chave de conta de armazenamento e rdma é Olá nome da partilha de ficheiros do Azure.</span><span class="sxs-lookup"><span data-stu-id="7e0b6-212">In this example, allvhdsje is your storage account name, storageaccountkey is your storage account key, and rdma is hello Azure File share name.</span></span> <span data-ttu-id="7e0b6-213">partilha de ficheiros do Azure Olá está montada como z no nó principal Olá.</span><span class="sxs-lookup"><span data-stu-id="7e0b6-213">hello Azure File share is mounted as Z: on hello head node.</span></span>

<span data-ttu-id="7e0b6-214">partilha de ficheiros de Azure Olá toomount nós do Linux, execute um **clusrun** comando no nó principal Olá.</span><span class="sxs-lookup"><span data-stu-id="7e0b6-214">toomount hello Azure File share on Linux nodes, run a **clusrun** command on hello head node.</span></span> <span data-ttu-id="7e0b6-215">**[Clusrun](https://technet.microsoft.com/library/cc947685.aspx)**  é uma ferramenta toocarry útil do HPC Pack realizar tarefas administrativas em vários nós.</span><span class="sxs-lookup"><span data-stu-id="7e0b6-215">**[Clusrun](https://technet.microsoft.com/library/cc947685.aspx)** is a useful HPC Pack tool toocarry out administrative tasks on multiple nodes.</span></span> <span data-ttu-id="7e0b6-216">(Consulte também [Clusrun para nós do Linux](#Clusrun-for-Linux-nodes) neste artigo.)</span><span class="sxs-lookup"><span data-stu-id="7e0b6-216">(See also [Clusrun for Linux nodes](#Clusrun-for-Linux-nodes) in this article.)</span></span>

<span data-ttu-id="7e0b6-217">Abra uma janela do Windows PowerShell e introduza Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="7e0b6-217">Open a Windows PowerShell window and enter hello following commands:</span></span>

```powershell
clusrun /nodegroup:LinuxNodes mkdir -p /rdma

clusrun /nodegroup:LinuxNodes mount -t cifs //allvhdsje.file.core.windows.net/rdma /rdma -o vers=2.1`,username=allvhdsje`,password=<storageaccountkey>'`,dir_mode=0777`,file_mode=0777
```

<span data-ttu-id="7e0b6-218">comando primeiro Olá cria uma pasta denominada /rdma em todos os nós no grupo de LinuxNodes Olá.</span><span class="sxs-lookup"><span data-stu-id="7e0b6-218">hello first command creates a folder named /rdma on all nodes in hello LinuxNodes group.</span></span> <span data-ttu-id="7e0b6-219">segundo comando de Olá monta Olá ficheiros do Azure partilha allvhdsjw.file.core.windows.net/rdma numa pasta de /rdma Olá com dir e ficheiro too777 de conjunto de bits de modo.</span><span class="sxs-lookup"><span data-stu-id="7e0b6-219">hello second command mounts hello Azure File share allvhdsjw.file.core.windows.net/rdma onto hello /rdma folder with dir and file mode bits set too777.</span></span> <span data-ttu-id="7e0b6-220">No segundo comando Olá, allvhdsje é o nome da sua conta de armazenamento e storageaccountkey é a chave de conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="7e0b6-220">In hello second command, allvhdsje is your storage account name and storageaccountkey is your storage account key.</span></span>

> [!NOTE]
> <span data-ttu-id="7e0b6-221">Olá "\\`" símbolo segundo comando de Olá é um símbolo de escape para o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7e0b6-221">hello “\\`” symbol in hello second command is an escape symbol for PowerShell.</span></span> <span data-ttu-id="7e0b6-222">"\\`,"significa que Olá"," (vírgulas caráter) é uma parte do comando de Olá.</span><span class="sxs-lookup"><span data-stu-id="7e0b6-222">“\\`,” means that hello “,” (comma character) is a part of hello command.</span></span>
> 
> 

### <a name="head-node-share"></a><span data-ttu-id="7e0b6-223">Partilha de nó principal</span><span class="sxs-lookup"><span data-stu-id="7e0b6-223">Head node share</span></span>
<span data-ttu-id="7e0b6-224">Em alternativa, monte uma pasta partilhada de nó principal Olá em nós do Linux.</span><span class="sxs-lookup"><span data-stu-id="7e0b6-224">Alternatively, mount a shared folder of hello head node on Linux nodes.</span></span> <span data-ttu-id="7e0b6-225">Fornece de uma partilha de ficheiros de tooshare de forma mais simples Olá, mas o nó principal Olá e todos os nós do Linux tem de ser implementados numa Olá mesma rede virtual.</span><span class="sxs-lookup"><span data-stu-id="7e0b6-225">A share provides hello simplest way tooshare files, but hello head node and all Linux nodes must be deployed in hello same virtual network.</span></span> <span data-ttu-id="7e0b6-226">Seguem-se passos de Olá.</span><span class="sxs-lookup"><span data-stu-id="7e0b6-226">Here are hello steps.</span></span>

1. <span data-ttu-id="7e0b6-227">Crie uma pasta no nó principal Olá e partilhe-tooEveryone com permissões de leitura/escrita.</span><span class="sxs-lookup"><span data-stu-id="7e0b6-227">Create a folder on hello head node and share it tooEveryone with Read/Write permissions.</span></span> <span data-ttu-id="7e0b6-228">Por exemplo, partilhar D:\OpenFOAM no nó principal do Olá como \\CentOS7RDMA HN\OpenFOAM.</span><span class="sxs-lookup"><span data-stu-id="7e0b6-228">For example, share D:\OpenFOAM on hello head node as \\CentOS7RDMA-HN\OpenFOAM.</span></span> <span data-ttu-id="7e0b6-229">Aqui CentOS7RDMA HN é Olá nome de anfitrião do nó principal Olá.</span><span class="sxs-lookup"><span data-stu-id="7e0b6-229">Here CentOS7RDMA-HN is hello hostname of hello head node.</span></span>
   
    ![Permissões de partilha de ficheiros][fileshareperms]
   
    ![Partilha de ficheiros][filesharing]
2. <span data-ttu-id="7e0b6-232">Abra uma janela do Windows PowerShell e execute Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="7e0b6-232">Open a Windows PowerShell window and run hello following commands:</span></span>
   
    ```powershell
    clusrun /nodegroup:LinuxNodes mkdir -p /openfoam
   
    clusrun /nodegroup:LinuxNodes mount -t cifs //CentOS7RDMA-HN/OpenFOAM /openfoam -o vers=2.1`,username=<username>`,password='<password>'`,dir_mode=0777`,file_mode=0777
    ```

<span data-ttu-id="7e0b6-233">comando primeiro Olá cria uma pasta denominada /openfoam em todos os nós no grupo de LinuxNodes Olá.</span><span class="sxs-lookup"><span data-stu-id="7e0b6-233">hello first command creates a folder named /openfoam on all nodes in hello LinuxNodes group.</span></span> <span data-ttu-id="7e0b6-234">segundo comando de Olá monta Olá partilhado pasta //CentOS7RDMA-HN/OpenFOAM numa pasta Olá com dir e ficheiro too777 de conjunto de bits de modo.</span><span class="sxs-lookup"><span data-stu-id="7e0b6-234">hello second command mounts hello shared folder //CentOS7RDMA-HN/OpenFOAM onto hello folder with dir and file mode bits set too777.</span></span> <span data-ttu-id="7e0b6-235">Olá nome de utilizador e palavra-passe no comando Olá devem ser Olá nome de utilizador e palavra-passe de um utilizador de cluster no nó principal Olá.</span><span class="sxs-lookup"><span data-stu-id="7e0b6-235">hello username and password in hello command should be hello username and password of a cluster user on hello head node.</span></span> <span data-ttu-id="7e0b6-236">(Consulte [adicionar ou remover utilizadores de cluster](https://technet.microsoft.com/library/ff919330.aspx).)</span><span class="sxs-lookup"><span data-stu-id="7e0b6-236">(See [Add or remove cluster users](https://technet.microsoft.com/library/ff919330.aspx).)</span></span>

> [!NOTE]
> <span data-ttu-id="7e0b6-237">Olá "\\`" símbolo segundo comando de Olá é um símbolo de escape para o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7e0b6-237">hello “\\`” symbol in hello second command is an escape symbol for PowerShell.</span></span> <span data-ttu-id="7e0b6-238">"\\`,"significa que Olá"," (vírgulas caráter) é uma parte do comando de Olá.</span><span class="sxs-lookup"><span data-stu-id="7e0b6-238">“\\`,” means that hello “,” (comma character) is a part of hello command.</span></span>
> 
> 

### <a name="nfs-server"></a><span data-ttu-id="7e0b6-239">Servidor NFS</span><span class="sxs-lookup"><span data-stu-id="7e0b6-239">NFS server</span></span>
<span data-ttu-id="7e0b6-240">Olá serviço NFS permite-lhe tooshare e migra ficheiros entre computadores que executam o sistema de operativo Olá Windows Server 2012 utilizando o protocolo SMB de Olá e os computadores baseados em Linux através do protocolo NFS de Olá.</span><span class="sxs-lookup"><span data-stu-id="7e0b6-240">hello NFS service enables you tooshare and migrate files between computers running hello Windows Server 2012 operating system using hello SMB protocol and Linux-based computers using hello NFS protocol.</span></span> <span data-ttu-id="7e0b6-241">Olá servidor NFS e todos os outros nós têm toobe implementado na Olá mesma rede virtual.</span><span class="sxs-lookup"><span data-stu-id="7e0b6-241">hello NFS server and all other nodes have toobe deployed in hello same virtual network.</span></span> <span data-ttu-id="7e0b6-242">Proporciona uma melhoria da compatibilidade com os nós do Linux comparada a uma partilha SMB.</span><span class="sxs-lookup"><span data-stu-id="7e0b6-242">It provides better compatibility with Linux nodes compared with an SMB share.</span></span> <span data-ttu-id="7e0b6-243">Por exemplo, suporta ligações de ficheiro.</span><span class="sxs-lookup"><span data-stu-id="7e0b6-243">For example, it supports file links.</span></span>

1. <span data-ttu-id="7e0b6-244">tooinstall e configurar um servidor NFS, siga os passos Olá [servidor para a partilha primeiro do sistema de ficheiros de rede ponto a ponto](http://blogs.technet.com/b/filecab/archive/2012/10/08/server-for-network-file-system-first-share-end-to-end.aspx).</span><span class="sxs-lookup"><span data-stu-id="7e0b6-244">tooinstall and set up an NFS server, follow hello steps in [Server for Network File System First Share End-to-End](http://blogs.technet.com/b/filecab/archive/2012/10/08/server-for-network-file-system-first-share-end-to-end.aspx).</span></span>
   
    <span data-ttu-id="7e0b6-245">Por exemplo, crie uma partilha NFS com o nome nfs com Olá seguintes propriedades:</span><span class="sxs-lookup"><span data-stu-id="7e0b6-245">For example, create an NFS share named nfs with hello following properties:</span></span>
   
    ![Autorização de NFS][nfsauth]
   
    ![Permissões de partilha NFS][nfsshare]
   
    ![Permissões NTFS de NFS][nfsperm]
   
    ![Propriedades de gestão de NFS][nfsmanage]
2. <span data-ttu-id="7e0b6-250">Abra uma janela do Windows PowerShell e execute Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="7e0b6-250">Open a Windows PowerShell window and run hello following commands:</span></span>
   
    ```powershell
    clusrun /nodegroup:LinuxNodes mkdir -p /nfsshare
   
    clusrun /nodegroup:LinuxNodes mount CentOS7RDMA-HN:/nfs /nfsshared
    ```
   
   <span data-ttu-id="7e0b6-251">comando primeiro Olá cria uma pasta denominada /nfsshared em todos os nós no grupo de LinuxNodes Olá.</span><span class="sxs-lookup"><span data-stu-id="7e0b6-251">hello first command creates a folder named /nfsshared on all nodes in hello LinuxNodes group.</span></span> <span data-ttu-id="7e0b6-252">Olá segundo comando monta Olá NFS partilhar CentOS7RDMA HN: / nfs para Olá pasta.</span><span class="sxs-lookup"><span data-stu-id="7e0b6-252">hello second command mounts hello NFS share CentOS7RDMA-HN:/nfs onto hello folder.</span></span> <span data-ttu-id="7e0b6-253">Aqui CentOS7RDMA HN: / nfs é o caminho de remoto Olá da sua partilha NFS.</span><span class="sxs-lookup"><span data-stu-id="7e0b6-253">Here CentOS7RDMA-HN:/nfs is hello remote path of your NFS share.</span></span>

## <a name="how-toosubmit-jobs"></a><span data-ttu-id="7e0b6-254">Como toosubmit tarefas</span><span class="sxs-lookup"><span data-stu-id="7e0b6-254">How toosubmit jobs</span></span>
<span data-ttu-id="7e0b6-255">Existem várias formas toosubmit tarefas toohello HPC Pack cluster:</span><span class="sxs-lookup"><span data-stu-id="7e0b6-255">There are several ways toosubmit jobs toohello HPC Pack cluster:</span></span>

* <span data-ttu-id="7e0b6-256">Gestor de clusters HPC ou GUI de Gestor de tarefas HPC</span><span class="sxs-lookup"><span data-stu-id="7e0b6-256">HPC Cluster Manager or HPC Job Manager GUI</span></span>
* <span data-ttu-id="7e0b6-257">HPC web portal</span><span class="sxs-lookup"><span data-stu-id="7e0b6-257">HPC web portal</span></span>
* <span data-ttu-id="7e0b6-258">API REST</span><span class="sxs-lookup"><span data-stu-id="7e0b6-258">REST API</span></span>

<span data-ttu-id="7e0b6-259">Submissão de tarefa toohello cluster no Azure através do portal web do Olá HPC e ferramentas de HPC Pack GUI são Olá iguais a nós de computação do Windows.</span><span class="sxs-lookup"><span data-stu-id="7e0b6-259">Job submission toohello cluster in Azure via HPC Pack GUI tools and hello HPC web portal are hello same as for Windows compute nodes.</span></span> <span data-ttu-id="7e0b6-260">Consulte [Gestor de tarefas HPC Pack](https://technet.microsoft.com/library/ff919691.aspx) e [como toosubmit tarefas a partir de um computador de cliente no local](../../windows/hpcpack-cluster-submit-jobs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="7e0b6-260">See [HPC Pack Job Manager](https://technet.microsoft.com/library/ff919691.aspx) and [How toosubmit jobs from an on-premises client computer](../../windows/hpcpack-cluster-submit-jobs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="7e0b6-261">tarefas de toosubmit através de Olá REST API, consulte demasiado[criar e submeter tarefas ao utilizar Olá API de REST no Microsoft HPC Pack](http://social.technet.microsoft.com/wiki/contents/articles/7737.creating-and-submitting-jobs-by-using-the-rest-api-in-microsoft-hpc-pack-windows-hpc-server.aspx).</span><span class="sxs-lookup"><span data-stu-id="7e0b6-261">toosubmit jobs via hello REST API, refer too[Creating and Submitting Jobs by Using hello REST API in Microsoft HPC Pack](http://social.technet.microsoft.com/wiki/contents/articles/7737.creating-and-submitting-jobs-by-using-the-rest-api-in-microsoft-hpc-pack-windows-hpc-server.aspx).</span></span> <span data-ttu-id="7e0b6-262">toosubmit tarefas de um cliente Linux, consulte também o exemplo de Python toohello no Olá [HPC Pack SDK](https://www.microsoft.com/download/details.aspx?id=47756).</span><span class="sxs-lookup"><span data-stu-id="7e0b6-262">toosubmit jobs from a Linux client, also refer toohello Python sample in hello [HPC Pack SDK](https://www.microsoft.com/download/details.aspx?id=47756).</span></span>

## <a name="clusrun-for-linux-nodes"></a><span data-ttu-id="7e0b6-263">Clusrun para nós do Linux</span><span class="sxs-lookup"><span data-stu-id="7e0b6-263">Clusrun for Linux nodes</span></span>
<span data-ttu-id="7e0b6-264">Olá HPC Pack [clusrun](https://technet.microsoft.com/library/cc947685.aspx) ferramenta pode ser utilizado tooexecute comandos em nós do Linux ou através de uma linha de comandos ou o Gestor de clusters HPC.</span><span class="sxs-lookup"><span data-stu-id="7e0b6-264">hello HPC Pack [clusrun](https://technet.microsoft.com/library/cc947685.aspx) tool can be used tooexecute commands on Linux nodes either through a Command Prompt or HPC Cluster Manager.</span></span> <span data-ttu-id="7e0b6-265">Seguem-se alguns exemplos básicos.</span><span class="sxs-lookup"><span data-stu-id="7e0b6-265">Following are some basic examples.</span></span>

* <span data-ttu-id="7e0b6-266">Mostra os nomes de utilizador atual em todos os nós no cluster de Olá.</span><span class="sxs-lookup"><span data-stu-id="7e0b6-266">Show current user names on all nodes in hello cluster.</span></span>
  
    ```command
    clusrun whoami
    ```
* <span data-ttu-id="7e0b6-267">Instalar Olá **gdb** ferramenta de depurador com **yum** em todos os nós Olá linuxnodes grupo e, em seguida, reinicie nós Olá após 10 minutos.</span><span class="sxs-lookup"><span data-stu-id="7e0b6-267">Install hello **gdb** debugger tool with **yum** on all nodes in hello linuxnodes group and then restart hello nodes after 10 minutes.</span></span>
  
    ```command
    clusrun /nodegroup:linuxnodes yum install gdb –y; shutdown –r 10
    ```
* <span data-ttu-id="7e0b6-268">Criar um script de shell que apresenta cada número entre 1 e 10 para um segundo em cada nó de Linux num cluster de Olá, executá-la e mostrar um resultado de nós de Olá imediatamente.</span><span class="sxs-lookup"><span data-stu-id="7e0b6-268">Create a shell script displaying each number 1 through 10 for one second on each Linux node in hello cluster, run it, and show output from hello nodes immediately.</span></span>
  
    ```command
    clusrun /interleaved /nodegroup:linuxnodes echo \"for i in {1..10}; do echo \\\"\$i\\\"; sleep 1; done\" ^> script.sh; chmod +x script.sh; ./script.sh
    ```

> [!NOTE]
> <span data-ttu-id="7e0b6-269">Poderá ser necessário toouse determinados carateres de escape **clusrun** comandos.</span><span class="sxs-lookup"><span data-stu-id="7e0b6-269">You might need toouse certain escape characters in **clusrun** commands.</span></span> <span data-ttu-id="7e0b6-270">Como é mostrado neste exemplo, utilize ^ no Olá de tooescape linha de comandos ">" símbolo.</span><span class="sxs-lookup"><span data-stu-id="7e0b6-270">As shown in this example, use ^ in a Command Prompt tooescape hello ">" symbol.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="7e0b6-271">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="7e0b6-271">Next steps</span></span>
* <span data-ttu-id="7e0b6-272">Tente como aumentar verticalmente Olá cluster tooa grande número de nós, ou tentar executar uma carga de trabalho do Linux no cluster de Olá.</span><span class="sxs-lookup"><span data-stu-id="7e0b6-272">Try scaling up hello cluster tooa larger number of nodes, or try running a Linux workload on hello cluster.</span></span> <span data-ttu-id="7e0b6-273">Por exemplo, consulte [NAMD executar com o Microsoft HPC Pack no Linux nós de computação em Azure](hpcpack-cluster-namd.md).</span><span class="sxs-lookup"><span data-stu-id="7e0b6-273">For an example, see [Run NAMD with Microsoft HPC Pack on Linux compute nodes in Azure](hpcpack-cluster-namd.md).</span></span>
* <span data-ttu-id="7e0b6-274">Tente um cluster com [VMs com capacidade RDMA, de computação intensiva](../../windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) toorun MPI as cargas de trabalho.</span><span class="sxs-lookup"><span data-stu-id="7e0b6-274">Try a cluster with [RDMA-capable, compute-intensive VMs](../../windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) toorun MPI workloads.</span></span> <span data-ttu-id="7e0b6-275">Por exemplo, consulte [cluster OpenFOAM executar com o Microsoft HPC Pack num RDMA Linux no Azure](hpcpack-cluster-openfoam.md).</span><span class="sxs-lookup"><span data-stu-id="7e0b6-275">For an example, see [Run OpenFOAM with Microsoft HPC Pack on a Linux RDMA cluster in Azure](hpcpack-cluster-openfoam.md).</span></span>
* <span data-ttu-id="7e0b6-276">Se estiver interessado em trabalhar com Linux nós num cluster HPC Pack no local, consulte Olá [TechNet orientações](https://technet.microsoft.com/library/mt595803.aspx).</span><span class="sxs-lookup"><span data-stu-id="7e0b6-276">If you are interested in working with Linux nodes in an on-premises HPC Pack cluster, see hello [TechNet guidance](https://technet.microsoft.com/library/mt595803.aspx).</span></span>

<!--Image references-->
[scenario]:media/hpcpack-cluster/scenario.png
[portal]:media/hpcpack-cluster/portal.png
[validate]:media/hpcpack-cluster/validate.png
[resources]:media/hpcpack-cluster/resources.png
[deploy]:media/hpcpack-cluster/deploy.png
[management]:media/hpcpack-cluster/management.png
[heatmap]:media/hpcpack-cluster/heatmap.png
[fileshareperms]:media/hpcpack-cluster/fileshare1.png
[filesharing]:media/hpcpack-cluster/fileshare2.png
[nfsauth]:media/hpcpack-cluster/nfsauth.png
[nfsshare]:media/hpcpack-cluster/nfsshare.png
[nfsperm]:media/hpcpack-cluster/nfsperm.png
[nfsmanage]:media/hpcpack-cluster/nfsmanage.png
