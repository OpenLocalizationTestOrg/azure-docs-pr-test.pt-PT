---
title: aaaHPC pacote do cluster para o Excel e SOA | Microsoft Docs
description: "Começar a executar cargas de trabalho em grande escala Excel e SOA num cluster HPC Pack no Azure"
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager,hpc-pack
ms.assetid: cb6a9abe-caf3-44da-b911-849a50f6cfb3
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 06/01/2017
ms.author: danlep
ms.openlocfilehash: 55b4b2c25fe65d06b75025cc23c3c13b8b764238
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-running-excel-and-soa-workloads-on-an-hpc-pack-cluster-in-azure"></a><span data-ttu-id="d1bc6-103">Introdução ao executar cargas de trabalho do Excel e SOA num cluster HPC Pack no Azure</span><span class="sxs-lookup"><span data-stu-id="d1bc6-103">Get started running Excel and SOA workloads on an HPC Pack cluster in Azure</span></span>
<span data-ttu-id="d1bc6-104">Este artigo mostra como toodeploy Microsoft HPC Pack 2012 R2 do cluster em máquinas virtuais do Azure, utilizando um modelo de início rápido do Azure ou, opcionalmente, um script de implementação do Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d1bc6-104">This article shows you how toodeploy a Microsoft HPC Pack 2012 R2 cluster on Azure virtual machines by using an Azure quickstart template, or optionally an Azure PowerShell deployment script.</span></span> <span data-ttu-id="d1bc6-105">cluster de Olá utiliza VM do Azure Marketplace imagens concebidas toorun Microsoft Excel ou cargas de trabalho de arquitetura orientada para serviços (SOA) com o HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="d1bc6-105">hello cluster uses Azure Marketplace VM images designed toorun Microsoft Excel or service-oriented architecture (SOA) workloads with HPC Pack.</span></span> <span data-ttu-id="d1bc6-106">Pode utilizar serviços SOA partir de um computador de cliente no local e Olá toorun de cluster HPC de Excel.</span><span class="sxs-lookup"><span data-stu-id="d1bc6-106">You can use hello cluster toorun Excel HPC and SOA services from an on-premises client computer.</span></span> <span data-ttu-id="d1bc6-107">os serviços de Excel HPC Olá incluem descarregamento de livros do Excel e funções definidas pelo utilizador do Excel ou UDFs.</span><span class="sxs-lookup"><span data-stu-id="d1bc6-107">hello Excel HPC services include Excel workbook offloading and Excel user-defined functions, or UDFs.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="d1bc6-108">Este artigo baseia-se nas funcionalidades, modelos e scripts para HPC Pack 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="d1bc6-108">This article is based on features, templates, and scripts for HPC Pack 2012 R2.</span></span> <span data-ttu-id="d1bc6-109">Este cenário não é atualmente suportado HPC Pack 2016.</span><span class="sxs-lookup"><span data-stu-id="d1bc6-109">This scenario is not currently supported in HPC Pack 2016.</span></span>
>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="d1bc6-110">Um nível elevado, hello diagrama seguinte mostra cluster HPC Pack de Olá que cria.</span><span class="sxs-lookup"><span data-stu-id="d1bc6-110">At a high level, hello following diagram shows hello HPC Pack cluster you create.</span></span>

![Cluster HPC connosco executar cargas de trabalho do Excel][scenario]

## <a name="prerequisites"></a><span data-ttu-id="d1bc6-112">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="d1bc6-112">Prerequisites</span></span>
* <span data-ttu-id="d1bc6-113">**Computador cliente** -precisa de um cliente baseado no Windows computador toosubmit exemplo Excel e SOA tarefas toohello cluster.</span><span class="sxs-lookup"><span data-stu-id="d1bc6-113">**Client computer** - You need a Windows-based client computer toosubmit sample Excel and SOA jobs toohello cluster.</span></span> <span data-ttu-id="d1bc6-114">Também precisa de um Olá de toorun de computador Windows script de implementação de cluster do Azure PowerShell (se escolher que método de implementação).</span><span class="sxs-lookup"><span data-stu-id="d1bc6-114">You also need a Windows computer toorun hello Azure PowerShell cluster deployment script (if you choose that deployment method).</span></span>
* <span data-ttu-id="d1bc6-115">**Subscrição do Azure** -se não tiver uma subscrição do Azure, pode criar um [conta gratuita](https://azure.microsoft.com/pricing/free-trial/) em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="d1bc6-115">**Azure subscription** - If you don't have an Azure subscription, you can create a [free account](https://azure.microsoft.com/pricing/free-trial/) in just a couple of minutes.</span></span>
* <span data-ttu-id="d1bc6-116">**Quota de núcleos** -poderá ter de quota de Olá tooincrease de núcleos, especialmente se implementar vários nós do cluster sem especializados tamanhos de VM.</span><span class="sxs-lookup"><span data-stu-id="d1bc6-116">**Cores quota** - You might need tooincrease hello quota of cores, especially if you deploy several cluster nodes with multicore VM sizes.</span></span> <span data-ttu-id="d1bc6-117">Se estiver a utilizar um modelo de início rápido do Azure, a quota de núcleos de Olá no Gestor de recursos é por região do Azure.</span><span class="sxs-lookup"><span data-stu-id="d1bc6-117">If you are using an Azure quickstart template, hello cores quota in Resource Manager is per Azure region.</span></span> <span data-ttu-id="d1bc6-118">Nesse caso, poderá ter de quota de Olá tooincrease numa região específica.</span><span class="sxs-lookup"><span data-stu-id="d1bc6-118">In that case, you might need tooincrease hello quota in a specific region.</span></span> <span data-ttu-id="d1bc6-119">Consulte [limites de subscrição do Azure, quotas e restrições](../../azure-subscription-service-limits.md).</span><span class="sxs-lookup"><span data-stu-id="d1bc6-119">See [Azure subscription limits, quotas, and constraints](../../azure-subscription-service-limits.md).</span></span> <span data-ttu-id="d1bc6-120">tooincrease uma quota [abrir um pedido de suporte ao cliente online](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/) , sem encargos.</span><span class="sxs-lookup"><span data-stu-id="d1bc6-120">tooincrease a quota, [open an online customer support request](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/) at no charge.</span></span>
* <span data-ttu-id="d1bc6-121">**Licença do Microsoft Office** - se implementar computação nós utilizando uma imagem de VM do Marketplace HPC Pack 2012 R2 com o Microsoft Excel, está instalada uma versão de avaliação de 30 dias do Microsoft Excel Professional Plus 2013.</span><span class="sxs-lookup"><span data-stu-id="d1bc6-121">**Microsoft Office license** - If you deploy compute nodes using a Marketplace HPC Pack 2012 R2 VM image with Microsoft Excel, a 30-day evaluation version of Microsoft Excel Professional Plus 2013 is installed.</span></span> <span data-ttu-id="d1bc6-122">Após o período de avaliação de Olá, terá de tooprovide uma válido Microsoft Office licença tooactivate Excel toocontinue toorun cargas de trabalho.</span><span class="sxs-lookup"><span data-stu-id="d1bc6-122">After hello evaluation period, you need tooprovide a valid Microsoft Office license tooactivate Excel toocontinue toorun workloads.</span></span> <span data-ttu-id="d1bc6-123">Consulte [Excel ativação](#excel-activation) posteriormente neste artigo.</span><span class="sxs-lookup"><span data-stu-id="d1bc6-123">See [Excel activation](#excel-activation) later in this article.</span></span> 

## <a name="step-1-set-up-an-hpc-pack-cluster-in-azure"></a><span data-ttu-id="d1bc6-124">Passo 1.</span><span class="sxs-lookup"><span data-stu-id="d1bc6-124">Step 1.</span></span> <span data-ttu-id="d1bc6-125">Configurar um cluster HPC Pack no Azure</span><span class="sxs-lookup"><span data-stu-id="d1bc6-125">Set up an HPC Pack cluster in Azure</span></span>
<span data-ttu-id="d1bc6-126">Vamos mostrar duas opções tooset segurança cluster HPC Pack 2012 R2 de Olá: primeiro, utilizando um modelo de início rápido do Azure e Olá portal do Azure; e o segundo, utilizando um script de implementação do Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d1bc6-126">We show two options tooset up hello HPC Pack 2012 R2 cluster: first, using an Azure quickstart template and hello Azure portal; and second, using an Azure PowerShell deployment script.</span></span>

### <a name="option-1-use-a-quickstart-template"></a><span data-ttu-id="d1bc6-127">Opção 1.</span><span class="sxs-lookup"><span data-stu-id="d1bc6-127">Option 1.</span></span> <span data-ttu-id="d1bc6-128">Utilize um modelo de início rápido</span><span class="sxs-lookup"><span data-stu-id="d1bc6-128">Use a quickstart template</span></span>
<span data-ttu-id="d1bc6-129">Utilize um tooquickly de modelo de início rápido do Azure implementar um cluster HPC Pack Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="d1bc6-129">Use an Azure quickstart template tooquickly deploy an HPC Pack cluster in hello Azure portal.</span></span> <span data-ttu-id="d1bc6-130">Quando abrir o modelo de Olá no portal de Olá, obtenha uma IU simple em que introduza as definições de Olá para o cluster.</span><span class="sxs-lookup"><span data-stu-id="d1bc6-130">When you open hello template in hello portal, you get a simple UI where you enter hello settings for your cluster.</span></span> <span data-ttu-id="d1bc6-131">Seguem-se passos de Olá.</span><span class="sxs-lookup"><span data-stu-id="d1bc6-131">Here are hello steps.</span></span> 

> [!TIP]
> <span data-ttu-id="d1bc6-132">Se quiser, utilize um [modelo do Azure Marketplace](https://portal.azure.com/?feature.relex=*%2CHubsExtension#create/microsofthpc.newclusterexcelcn) que cria um cluster semelhante especificamente para cargas de trabalho do Excel.</span><span class="sxs-lookup"><span data-stu-id="d1bc6-132">If you want, use an [Azure Marketplace template](https://portal.azure.com/?feature.relex=*%2CHubsExtension#create/microsofthpc.newclusterexcelcn) that creates a similar cluster specifically for Excel workloads.</span></span> <span data-ttu-id="d1bc6-133">passos de Olá diferirem ligeiramente do seguinte Olá.</span><span class="sxs-lookup"><span data-stu-id="d1bc6-133">hello steps differ slightly from hello following.</span></span>
> 
> 

1. <span data-ttu-id="d1bc6-134">Visite Olá [página do modelo criar Cluster HPC no GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster).</span><span class="sxs-lookup"><span data-stu-id="d1bc6-134">Visit hello [Create HPC Cluster template page on GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster).</span></span> <span data-ttu-id="d1bc6-135">Se quiser, rever as informações sobre o modelo de Olá e código de origem Olá.</span><span class="sxs-lookup"><span data-stu-id="d1bc6-135">If you want, review information about hello template and hello source code.</span></span>
2. <span data-ttu-id="d1bc6-136">Clique em **implementar tooAzure** toostart uma implementação com modelo Olá Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="d1bc6-136">Click **Deploy tooAzure** toostart a deployment with hello template in hello Azure portal.</span></span>
   
   ![Implementar a modelo tooAzure][github]
3. <span data-ttu-id="d1bc6-138">No portal de Olá, siga estes passos tooenter Olá parâmetros modelo de cluster HPC Olá.</span><span class="sxs-lookup"><span data-stu-id="d1bc6-138">In hello portal, follow these steps tooenter hello parameters for hello HPC cluster template.</span></span>
   
   <span data-ttu-id="d1bc6-139">a.</span><span class="sxs-lookup"><span data-stu-id="d1bc6-139">a.</span></span> <span data-ttu-id="d1bc6-140">No Olá **parâmetros** página, introduza ou modificar os valores de parâmetros de modelo Olá.</span><span class="sxs-lookup"><span data-stu-id="d1bc6-140">On hello **Parameters** page, enter or modify values for hello template parameters.</span></span> <span data-ttu-id="d1bc6-141">(Clique Olá ícone tooeach as definições seguintes para obter informações de ajuda.) Valores de exemplo são apresentados na Olá ecrã a seguir.</span><span class="sxs-lookup"><span data-stu-id="d1bc6-141">(Click hello icon next tooeach setting for help information.) Sample values are shown in hello following screen.</span></span> <span data-ttu-id="d1bc6-142">Este exemplo cria um cluster com o nome *hpc01* no Olá *hpc.local* nós de computação de domínio constituída por um nó principal e 2.</span><span class="sxs-lookup"><span data-stu-id="d1bc6-142">This example creates a cluster named *hpc01* in hello *hpc.local* domain consisting of a head node and 2 compute nodes.</span></span> <span data-ttu-id="d1bc6-143">nós de computação Olá são criados a partir de uma imagem de VM de pacote HPC inclui o Microsoft Excel.</span><span class="sxs-lookup"><span data-stu-id="d1bc6-143">hello compute nodes are created from an HPC Pack VM image that includes Microsoft Excel.</span></span>
   
   ![Introduza os parâmetros][parameters-new-portal]
   
   > [!NOTE]
   > <span data-ttu-id="d1bc6-145">nó principal Olá VM é criada automaticamente a partir Olá [mais recente imagem do Marketplace](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2onwindowsserver2012r2/) do HPC Pack 2012 R2 no Windows Server 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="d1bc6-145">hello head node VM is created automatically from hello [latest Marketplace image](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2onwindowsserver2012r2/) of HPC Pack 2012 R2 on Windows Server 2012 R2.</span></span> <span data-ttu-id="d1bc6-146">Atualmente imagem Olá baseia-se no HPC Pack 2012 R2 Update 3.</span><span class="sxs-lookup"><span data-stu-id="d1bc6-146">Currently hello image is based on HPC Pack 2012 R2 Update 3.</span></span>
   > 
   > <span data-ttu-id="d1bc6-147">VMs de nó de computação são criadas a partir da imagem mais recente do Olá da família de nó de computação Olá selecionado.</span><span class="sxs-lookup"><span data-stu-id="d1bc6-147">Compute node VMs are created from hello latest image of hello selected compute node family.</span></span> <span data-ttu-id="d1bc6-148">Selecione Olá **ComputeNodeWithExcel** opção Olá mais recente HPC Pack computação nó imagem que inclui uma versão de avaliação do Microsoft Excel Professional Plus 2013.</span><span class="sxs-lookup"><span data-stu-id="d1bc6-148">Select hello **ComputeNodeWithExcel** option for hello latest HPC Pack compute node image that includes an evaluation version of Microsoft Excel Professional Plus 2013.</span></span> <span data-ttu-id="d1bc6-149">toodeploy um cluster para sessões SOA gerais ou para descarregamento de UDF do Excel, escolha Olá **ComputeNode** opção (sem Excel instalado).</span><span class="sxs-lookup"><span data-stu-id="d1bc6-149">toodeploy a cluster for general SOA sessions or for Excel UDF offloading, choose hello **ComputeNode** option (without Excel installed).</span></span>
   > 
   > 
   
   <span data-ttu-id="d1bc6-150">b.</span><span class="sxs-lookup"><span data-stu-id="d1bc6-150">b.</span></span> <span data-ttu-id="d1bc6-151">Escolha Olá subscrição.</span><span class="sxs-lookup"><span data-stu-id="d1bc6-151">Choose hello subscription.</span></span>
   
   <span data-ttu-id="d1bc6-152">c.</span><span class="sxs-lookup"><span data-stu-id="d1bc6-152">c.</span></span> <span data-ttu-id="d1bc6-153">Criar um grupo de recursos do cluster de Olá, tais como *hpc01RG*.</span><span class="sxs-lookup"><span data-stu-id="d1bc6-153">Create a resource group for hello cluster, such as *hpc01RG*.</span></span>
   
   <span data-ttu-id="d1bc6-154">d.</span><span class="sxs-lookup"><span data-stu-id="d1bc6-154">d.</span></span> <span data-ttu-id="d1bc6-155">Escolha uma localização para o grupo de recursos de Olá, como EUA Central.</span><span class="sxs-lookup"><span data-stu-id="d1bc6-155">Choose a location for hello resource group, such as Central US.</span></span>
   
   <span data-ttu-id="d1bc6-156">e.</span><span class="sxs-lookup"><span data-stu-id="d1bc6-156">e.</span></span> <span data-ttu-id="d1bc6-157">No Olá **termos legais** , reveja os termos de Olá.</span><span class="sxs-lookup"><span data-stu-id="d1bc6-157">On hello **Legal terms** page, review hello terms.</span></span> <span data-ttu-id="d1bc6-158">Se concordar, clique em **Compra**.</span><span class="sxs-lookup"><span data-stu-id="d1bc6-158">If you agree, click **Purchase**.</span></span> <span data-ttu-id="d1bc6-159">Quando tiver terminado a definir valores de Olá para o modelo de Olá, clique em **criar**.</span><span class="sxs-lookup"><span data-stu-id="d1bc6-159">Then, when you are finished setting hello values for hello template, click **Create**.</span></span>
4. <span data-ttu-id="d1bc6-160">Quando concluir a implementação de Olá (que normalmente demora cerca de 30 minutos), Exportar ficheiro de certificado de cluster Olá Olá principal do nó do cluster.</span><span class="sxs-lookup"><span data-stu-id="d1bc6-160">When hello deployment completes (it typically takes around 30 minutes), export hello cluster certificate file from hello cluster head node.</span></span> <span data-ttu-id="d1bc6-161">Num passo posterior, pode importa este certificado público no Olá tooprovide Olá do lado do servidor autenticação do computador cliente para enlace de HTTP seguro.</span><span class="sxs-lookup"><span data-stu-id="d1bc6-161">In a later step, you import this public certificate on hello client computer tooprovide hello server-side authentication for secure HTTP binding.</span></span>
   
   <span data-ttu-id="d1bc6-162">a.</span><span class="sxs-lookup"><span data-stu-id="d1bc6-162">a.</span></span> <span data-ttu-id="d1bc6-163">No portal do Azure Olá, aceda toohello dashboard, o nó principal selecione Olá e clique em **Connect** , Olá parte superior do Olá página tooconnect utilizando o ambiente de trabalho remoto.</span><span class="sxs-lookup"><span data-stu-id="d1bc6-163">In hello Azure portal, go toohello dashboard, select hello head node, and click **Connect** at hello top of hello page tooconnect using Remote Desktop.</span></span>
   
    <!-- ![Connect toohello head node][connect] -->
   
   <span data-ttu-id="d1bc6-164">b.</span><span class="sxs-lookup"><span data-stu-id="d1bc6-164">b.</span></span> <span data-ttu-id="d1bc6-165">Utilize procedimentos padrão no certificado de nó principal do Gestor de certificados tooexport Olá (localizado em Cert: \LocalMachine\My) sem chave privada Olá.</span><span class="sxs-lookup"><span data-stu-id="d1bc6-165">Use standard procedures in Certificate Manager tooexport hello head node certificate (located under Cert:\LocalMachine\My) without hello private key.</span></span> <span data-ttu-id="d1bc6-166">Neste exemplo, exportar *CN = hpc01.eastus.cloudapp.azure.com*.</span><span class="sxs-lookup"><span data-stu-id="d1bc6-166">In this example, export *CN = hpc01.eastus.cloudapp.azure.com*.</span></span>
   
   ![Exportar o certificado de Olá][cert]

### <a name="option-2-use-hello-hpc-pack-iaas-deployment-script"></a><span data-ttu-id="d1bc6-168">Opção 2.</span><span class="sxs-lookup"><span data-stu-id="d1bc6-168">Option 2.</span></span> <span data-ttu-id="d1bc6-169">Utilizar script de implementação de IaaS do pacote HPC Olá</span><span class="sxs-lookup"><span data-stu-id="d1bc6-169">Use hello HPC Pack IaaS Deployment script</span></span>
<span data-ttu-id="d1bc6-170">Olá script de implementação de HPC Pack IaaS proporciona outra forma versátil toodeploy um cluster HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="d1bc6-170">hello HPC Pack IaaS deployment script provides another versatile way toodeploy an HPC Pack cluster.</span></span> <span data-ttu-id="d1bc6-171">Cria um cluster no modelo de implementação clássica Olá, enquanto que o modelo de Olá utiliza o modelo de implementação Azure Resource Manager Olá.</span><span class="sxs-lookup"><span data-stu-id="d1bc6-171">It creates a cluster in hello classic deployment model, whereas hello template uses hello Azure Resource Manager deployment model.</span></span> <span data-ttu-id="d1bc6-172">Além disso, o script de Olá é compatível com uma subscrição no Olá Global do Azure ou o serviço de Azure China.</span><span class="sxs-lookup"><span data-stu-id="d1bc6-172">Also, hello script is compatible with a subscription in either hello Azure Global or Azure China service.</span></span>

<span data-ttu-id="d1bc6-173">**Pré-requisitos adicionais**</span><span class="sxs-lookup"><span data-stu-id="d1bc6-173">**Additional prerequisites**</span></span>

* <span data-ttu-id="d1bc6-174">**O Azure PowerShell** - [instalar e configurar o Azure PowerShell](/powershell/azure/overview) (versão 0.8.10 ou posterior) no computador cliente.</span><span class="sxs-lookup"><span data-stu-id="d1bc6-174">**Azure PowerShell** - [Install and configure Azure PowerShell](/powershell/azure/overview) (version 0.8.10 or later) on your client computer.</span></span>
* <span data-ttu-id="d1bc6-175">**Script de implementação de HPC Pack IaaS** - transferir e Descompacte a versão mais recente do Olá do script de Olá no Olá [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=44949).</span><span class="sxs-lookup"><span data-stu-id="d1bc6-175">**HPC Pack IaaS deployment script** - Download and unpack hello latest version of hello script from hello [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=44949).</span></span> <span data-ttu-id="d1bc6-176">Verificar a versão de Olá do script Olá executando `New-HPCIaaSCluster.ps1 –Version`.</span><span class="sxs-lookup"><span data-stu-id="d1bc6-176">Check hello version of hello script by running `New-HPCIaaSCluster.ps1 –Version`.</span></span> <span data-ttu-id="d1bc6-177">Este artigo baseia-se numa versão 4.5.0 ou posterior do script de Olá.</span><span class="sxs-lookup"><span data-stu-id="d1bc6-177">This article is based on version 4.5.0 or later of hello script.</span></span>

<span data-ttu-id="d1bc6-178">**Criar ficheiro de configuração de Olá**</span><span class="sxs-lookup"><span data-stu-id="d1bc6-178">**Create hello configuration file**</span></span>

 <span data-ttu-id="d1bc6-179">Olá HPC Pack IaaS script de implementação utiliza um ficheiro de configuração XML, como entrada descreve Olá da infraestrutura de cluster HPC de Olá.</span><span class="sxs-lookup"><span data-stu-id="d1bc6-179">hello HPC Pack IaaS deployment script uses an XML configuration file as input that describes hello infrastructure of hello HPC cluster.</span></span> <span data-ttu-id="d1bc6-180">toodeploy nós criados a partir da imagem do nó de computação Olá que inclui o Microsoft Excel, de computação de um cluster constituída por um nó principal e 18 substitua os valores para o seu ambiente para o seguinte ficheiro de configuração de exemplo de Olá.</span><span class="sxs-lookup"><span data-stu-id="d1bc6-180">toodeploy a cluster consisting of a head node and 18 compute nodes created from hello compute node image that includes Microsoft Excel, substitute values for your environment into hello following sample configuration file.</span></span> <span data-ttu-id="d1bc6-181">Para mais informações sobre o ficheiro de configuração de Olá, consulte o ficheiro de Manual.rtf de Olá na pasta de script de Olá e [criar um cluster HPC com Olá script de implementação de HPC Pack IaaS](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d1bc6-181">For more information about hello configuration file, see hello Manual.rtf file in hello script folder and [Create an HPC cluster with hello HPC Pack IaaS deployment script](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

```
<?xml version="1.0" encoding="utf-8"?>
<IaaSClusterConfig>
  <Subscription>
    <SubscriptionName>MySubscription</SubscriptionName>
    <StorageAccount>hpc01</StorageAccount>
  </Subscription>
  <Location>West US</Location>
  <VNet>
    <VNetName>hpc-vnet01</VNetName>
    <SubnetName>Subnet-1</SubnetName>
  </VNet>
  <Domain>
    <DCOption>NewDC</DCOption>
    <DomainFQDN>hpc.local</DomainFQDN>
    <DomainController>
      <VMName>HPCExcelDC01</VMName>
      <ServiceName>HPCExcelDC01</ServiceName>
      <VMSize>Medium</VMSize>
    </DomainController>
  </Domain>
   <Database>
    <DBOption>LocalDB</DBOption>
  </Database>
  <HeadNode>
    <VMName>HPCExcelHN01</VMName>
    <ServiceName>HPCExcelHN01</ServiceName>
    <VMSize>Large</VMSize>
    <EnableRESTAPI/>
    <EnableWebPortal/>
    <PostConfigScript>C:\tests\PostConfig.ps1</PostConfigScript>
  </HeadNode>
  <ComputeNodes>
    <VMNamePattern>HPCExcelCN%00%</VMNamePattern>
    <ServiceName>HPCExcelCN01</ServiceName>
    <VMSize>Medium</VMSize>
    <NodeCount>18</NodeCount>
    <ImageName>HPCPack2012R2_ComputeNodeWithExcel</ImageName>
  </ComputeNodes>
</IaaSClusterConfig>
```

<span data-ttu-id="d1bc6-182">**Notas sobre o ficheiro de configuração de Olá**</span><span class="sxs-lookup"><span data-stu-id="d1bc6-182">**Notes about hello configuration file**</span></span>

* <span data-ttu-id="d1bc6-183">Olá **VMName** de nó principal Olá **tem** ser Olá mesmo como Olá **ServiceName**, ou tarefas SOA falharem toorun.</span><span class="sxs-lookup"><span data-stu-id="d1bc6-183">hello **VMName** of hello head node **MUST** be hello same as hello **ServiceName**, or SOA jobs fail toorun.</span></span>
* <span data-ttu-id="d1bc6-184">Certifique-se de que especifica **EnableWebPortal** para que hello certificado do nó principal é gerado e exportado.</span><span class="sxs-lookup"><span data-stu-id="d1bc6-184">Make sure you specify **EnableWebPortal** so that hello head node certificate is generated and exported.</span></span>
* <span data-ttu-id="d1bc6-185">ficheiro de Olá Especifica um script do PowerShell pós-configuração PostConfig.ps1 que é executado no nó principal Olá.</span><span class="sxs-lookup"><span data-stu-id="d1bc6-185">hello file specifies a post-configuration PowerShell script PostConfig.ps1 that runs on hello head node.</span></span> <span data-ttu-id="d1bc6-186">Olá script de exemplo a seguir configura a cadeia de ligação de armazenamento do Azure Olá, remove a função de nó de computação Olá do nó principal Olá e coloca todos os nós online quando estão implementadas.</span><span class="sxs-lookup"><span data-stu-id="d1bc6-186">hello following sample script configures hello Azure storage connection string, removes hello compute node role from hello head node, and brings all nodes online when they are deployed.</span></span> 

```
    # add hello HPC Pack powershell cmdlets
        Add-PSSnapin Microsoft.HPC

    # set hello Azure storage connection string for hello cluster
        Set-HpcClusterProperty -AzureStorageConnectionString 'DefaultEndpointsProtocol=https;AccountName=<yourstorageaccountname>;AccountKey=<yourstorageaccountkey>'

    # remove hello compute node role for head node toomake sure hello Excel workbook won’t run on head node
        Get-HpcNode -GroupName HeadNodes | Set-HpcNodeState -State offline | Set-HpcNode -Role BrokerNode

    # total number of nodes in hello deployment including hello head node and compute nodes, which should match hello number specified in hello XML configuration file
        $TotalNumOfNodes = 19

        $ErrorActionPreference = 'SilentlyContinue'

    # bring nodes online when they are deployed until all nodes are online
        while ($true)
        {
          Get-HpcNode -State Offline | Set-HpcNodeState -State Online -Confirm:$false
          $OnlineNodes = @(Get-HpcNode -State Online)
          if ($OnlineNodes.Count -eq $TotalNumOfNodes)
          {
             break
          }
          sleep 60
        }
```

<span data-ttu-id="d1bc6-187">**Executar script de Olá**</span><span class="sxs-lookup"><span data-stu-id="d1bc6-187">**Run hello script**</span></span>

1. <span data-ttu-id="d1bc6-188">Abra a consola do PowerShell de Olá no computador de cliente Olá como administrador.</span><span class="sxs-lookup"><span data-stu-id="d1bc6-188">Open hello PowerShell console on hello client computer as an administrator.</span></span>
2. <span data-ttu-id="d1bc6-189">Alterar pasta do script do diretório toohello (E:\IaaSClusterScript neste exemplo).</span><span class="sxs-lookup"><span data-stu-id="d1bc6-189">Change directory toohello script folder (E:\IaaSClusterScript in this example).</span></span>
   
   ```
   cd E:\IaaSClusterScript
   ```
3. <span data-ttu-id="d1bc6-190">toodeploy Olá HPC Pack cluster, execute Olá os seguintes comandos.</span><span class="sxs-lookup"><span data-stu-id="d1bc6-190">toodeploy hello HPC Pack cluster, run hello following command.</span></span> <span data-ttu-id="d1bc6-191">Este exemplo assume que esse ficheiro de configuração Olá está localizado na E:\HPCDemoConfig.xml.</span><span class="sxs-lookup"><span data-stu-id="d1bc6-191">This example assumes that hello configuration file is located in E:\HPCDemoConfig.xml.</span></span>
   
   ```
   .\New-HpcIaaSCluster.ps1 –ConfigFile E:\HPCDemoConfig.xml –AdminUserName MyAdminName
   ```

<span data-ttu-id="d1bc6-192">Olá script de implementação de pacote HPC estiver em execução durante algum tempo.</span><span class="sxs-lookup"><span data-stu-id="d1bc6-192">hello HPC Pack deployment script runs for some time.</span></span> <span data-ttu-id="d1bc6-193">Um script de Olá coisa que faz é tooexport e transferir o certificado de cluster Olá e guardá-lo na pasta de documentos do utilizador atual Olá no computador de cliente Olá.</span><span class="sxs-lookup"><span data-stu-id="d1bc6-193">One thing hello script does is tooexport and download hello cluster certificate and save it in hello current user’s Documents folder on hello client computer.</span></span> <span data-ttu-id="d1bc6-194">script de Olá gera um mensagem semelhante toohello seguintes procedimentos.</span><span class="sxs-lookup"><span data-stu-id="d1bc6-194">hello script generates a message similar toohello following.</span></span> <span data-ttu-id="d1bc6-195">Um passo seguinte, importar o certificado de Olá no arquivo de certificados adequada de Olá.</span><span class="sxs-lookup"><span data-stu-id="d1bc6-195">In a following step, you import hello certificate in hello appropriate certificate store.</span></span>    

    You have enabled REST API or web portal on HPC Pack head node. Please import hello following certificate in hello Trusted Root Certification Authorities certificate store on hello computer where you are submitting job or accessing hello HPC web portal:
    C:\Users\hpcuser\Documents\HPCWebComponent_HPCExcelHN004_20150707162011.cer

## <a name="step-2-offload-excel-workbooks-and-run-udfs-from-an-on-premises-client"></a><span data-ttu-id="d1bc6-196">Passo 2.</span><span class="sxs-lookup"><span data-stu-id="d1bc6-196">Step 2.</span></span> <span data-ttu-id="d1bc6-197">Descarregamento de livros do Excel e executar UDFs a partir de um cliente no local</span><span class="sxs-lookup"><span data-stu-id="d1bc6-197">Offload Excel workbooks and run UDFs from an on-premises client</span></span>
### <a name="excel-activation"></a><span data-ttu-id="d1bc6-198">Ativação do Excel</span><span class="sxs-lookup"><span data-stu-id="d1bc6-198">Excel activation</span></span>
<span data-ttu-id="d1bc6-199">Quando utilizar Olá imagem de ComputeNodeWithExcel VM para cargas de trabalho de produção, terá de tooprovide uma válido Microsoft Office licença chave tooactivate Excel em nós de computação Olá.</span><span class="sxs-lookup"><span data-stu-id="d1bc6-199">When using hello ComputeNodeWithExcel VM image for production workloads, you need tooprovide a valid Microsoft Office license key tooactivate Excel on hello compute nodes.</span></span> <span data-ttu-id="d1bc6-200">Caso contrário, versão de avaliação de Olá do Excel expira após 30 dias e em execução livros do Excel irá falhar com Olá COMException (0x800AC472).</span><span class="sxs-lookup"><span data-stu-id="d1bc6-200">Otherwise, hello evaluation version of Excel expires after 30 days, and running Excel workbooks will fail with hello COMException (0x800AC472).</span></span> 

<span data-ttu-id="d1bc6-201">Pode rearmamento Excel por mais 30 dias da hora de avaliação: Inicie sessão no nó principal toohello e clusrun `%ProgramFiles(x86)%\Microsoft Office\Office15\OSPPREARM.exe` no Excel todos os nós através do Gestor de Cluster HPC de computação.</span><span class="sxs-lookup"><span data-stu-id="d1bc6-201">You can rearm Excel for another 30 days of evaluation time: Log on toohello head node and clusrun `%ProgramFiles(x86)%\Microsoft Office\Office15\OSPPREARM.exe` on all Excel compute nodes via HPC Cluster Manager.</span></span> <span data-ttu-id="d1bc6-202">Pode rearmamento um máximo de duas vezes.</span><span class="sxs-lookup"><span data-stu-id="d1bc6-202">You can rearm a maximum of two times.</span></span> <span data-ttu-id="d1bc6-203">Depois disso, tem de fornecer uma chave de licenciamento do Office válida.</span><span class="sxs-lookup"><span data-stu-id="d1bc6-203">After that, you must provide a valid Office license key.</span></span>

<span data-ttu-id="d1bc6-204">Olá Office Professional Plus 2013 instalado numa imagem VM Olá é uma edição de volume com uma chave de licença do genérico Volume (GVLK).</span><span class="sxs-lookup"><span data-stu-id="d1bc6-204">hello Office Professional Plus 2013 installed on hello VM image is a volume edition with a Generic Volume License Key (GVLK).</span></span> <span data-ttu-id="d1bc6-205">Pode ativá-lo através do serviço de gestão de chaves (KMS) / ativação baseada no Active Directory (AD BA) ou chave de ativação múltipla (MAK).</span><span class="sxs-lookup"><span data-stu-id="d1bc6-205">You can activate it via Key Management Service (KMS)/Active Directory-Based Activation (AD-BA) or Multiple Activation Key (MAK).</span></span> 

    * <span data-ttu-id="d1bc6-206">toouse KMS/AD-BA, utilizar um servidor KMS existente ou configure um novo utilizando Olá pacote de licença de Volume do Microsoft Office 2013.</span><span class="sxs-lookup"><span data-stu-id="d1bc6-206">toouse KMS/AD-BA, use an existing KMS server or set up a new one by using hello Microsoft Office 2013 Volume License Pack.</span></span> <span data-ttu-id="d1bc6-207">(Se pretender, configurar Olá servidor no nó principal Olá.) Em seguida, ative chave de anfitrião KMS Olá através de Olá Internet ou por telefone.</span><span class="sxs-lookup"><span data-stu-id="d1bc6-207">(If you want to, set up hello server on hello head node.) Then, activate hello KMS host key via hello Internet or telephone.</span></span> <span data-ttu-id="d1bc6-208">Em seguida, clusrun `ospp.vbs` tooset Olá e porta do servidor KMS e ativar o Office em todos os nós de computação de Excel Olá.</span><span class="sxs-lookup"><span data-stu-id="d1bc6-208">Then clusrun `ospp.vbs` tooset hello KMS server and port and activate Office on all hello Excel compute nodes.</span></span> 

    * <span data-ttu-id="d1bc6-209">toouse MAK, primeiro clusrun `ospp.vbs` tooinput Olá chave e, em seguida, ative todos os nós de computação de Excel Olá através de Olá Internet ou telefone.</span><span class="sxs-lookup"><span data-stu-id="d1bc6-209">toouse MAK, first clusrun `ospp.vbs` tooinput hello key and then activate all hello Excel compute nodes via hello Internet or telephone.</span></span> 

> [!NOTE]
> <span data-ttu-id="d1bc6-210">Não não possível utilizar chaves de produto de revenda para o Office Professional Plus 2013 com esta imagem de VM.</span><span class="sxs-lookup"><span data-stu-id="d1bc6-210">Retail product keys for Office Professional Plus 2013 cannot be used with this VM image.</span></span> <span data-ttu-id="d1bc6-211">Se tiver chaves válidas e de suporte de dados de instalação para o Office ou Excel edições que não sejam nesta edição de volume do Office Professional Plus 2013, pode utilizá-los em vez disso.</span><span class="sxs-lookup"><span data-stu-id="d1bc6-211">If you have valid keys and installation media for Office or Excel editions other than this Office Professional Plus 2013 volume edition, you can use them instead.</span></span> <span data-ttu-id="d1bc6-212">Primeiro, desinstale nesta edição de volume e instalar a edição de Olá que tiver.</span><span class="sxs-lookup"><span data-stu-id="d1bc6-212">First uninstall this volume edition and install hello edition that you have.</span></span> <span data-ttu-id="d1bc6-213">Olá reinstalado Excel nó de computação pode ser capturada como um toouse de imagem VM personalizada numa implementação à escala.</span><span class="sxs-lookup"><span data-stu-id="d1bc6-213">hello reinstalled Excel compute node can be captured as a customized VM image toouse in a deployment at scale.</span></span>
> 
> 

### <a name="offload-excel-workbooks"></a><span data-ttu-id="d1bc6-214">Descarregamento de livros do Excel</span><span class="sxs-lookup"><span data-stu-id="d1bc6-214">Offload Excel workbooks</span></span>
<span data-ttu-id="d1bc6-215">Siga estes toooffload passos um livro do Excel para que seja executado no cluster HPC Pack de Olá no Azure.</span><span class="sxs-lookup"><span data-stu-id="d1bc6-215">Follow these steps toooffload an Excel workbook so that it runs on hello HPC Pack cluster in Azure.</span></span> <span data-ttu-id="d1bc6-216">toodo, tem de ter o Excel 2010 ou 2013 já instalado no computador de cliente Olá.</span><span class="sxs-lookup"><span data-stu-id="d1bc6-216">toodo this, you must have Excel 2010 or 2013 already installed on hello client computer.</span></span>

1. <span data-ttu-id="d1bc6-217">Utilize uma das opções de Olá no passo 1 toodeploy um cluster HPC Pack com Olá Excel imagem do nó de computação.</span><span class="sxs-lookup"><span data-stu-id="d1bc6-217">Use one of hello options in Step 1 toodeploy an HPC Pack cluster with hello Excel compute node image.</span></span> <span data-ttu-id="d1bc6-218">Obter o ficheiro de certificado de cluster Olá (. cer) e cluster nome de utilizador e palavra-passe.</span><span class="sxs-lookup"><span data-stu-id="d1bc6-218">Obtain hello cluster certificate file (.cer) and cluster username and password.</span></span>
2. <span data-ttu-id="d1bc6-219">No computador de cliente Olá, importe o certificado de cluster de Olá em Cert: \CurrentUser\Root.</span><span class="sxs-lookup"><span data-stu-id="d1bc6-219">On hello client computer, import hello cluster certificate under Cert:\CurrentUser\Root.</span></span>
3. <span data-ttu-id="d1bc6-220">Certifique-se de que o Excel está instalado.</span><span class="sxs-lookup"><span data-stu-id="d1bc6-220">Make sure Excel is installed.</span></span> <span data-ttu-id="d1bc6-221">Crie um ficheiro de Excel.exe.config com Olá seguir o conteúdo no Olá mesma pasta que Excel.exe no computador de cliente Olá.</span><span class="sxs-lookup"><span data-stu-id="d1bc6-221">Create an Excel.exe.config file with hello following contents in hello same folder as Excel.exe on hello client computer.</span></span> <span data-ttu-id="d1bc6-222">Este passo garante que Olá suplemento HPC Pack 2012 R2 Excel COM é carregado com êxito.</span><span class="sxs-lookup"><span data-stu-id="d1bc6-222">This step ensures that hello HPC Pack 2012 R2 Excel COM add-in loads successfully.</span></span>
   
    ```
    <?xml version="1.0"?>
    <configuration>
        <startup useLegacyV2RuntimeActivationPolicy="true">
            <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.0"/>
        </startup>
    </configuration>
    ```
4. <span data-ttu-id="d1bc6-223">Configure Olá cliente toosubmit tarefas toohello HPC Pack cluster.</span><span class="sxs-lookup"><span data-stu-id="d1bc6-223">Set up hello client toosubmit jobs toohello HPC Pack cluster.</span></span> <span data-ttu-id="d1bc6-224">Uma das alternativas consiste Olá toodownload completa [instalação do HPC Pack 2012 R2 Update 3](http://www.microsoft.com/download/details.aspx?id=49922) e instalar o cliente de HPC Pack Olá.</span><span class="sxs-lookup"><span data-stu-id="d1bc6-224">One option is toodownload hello full [HPC Pack 2012 R2 Update 3 installation](http://www.microsoft.com/download/details.aspx?id=49922) and install hello HPC Pack client.</span></span> <span data-ttu-id="d1bc6-225">Em alternativa, transfira e instale Olá [utilitários de cliente do Microsoft HPC Pack 2012 R2 Update 3](https://www.microsoft.com/download/details.aspx?id=49923) e Olá adequado Visual C++ 2010 redistributable para o seu computador ([x64](http://www.microsoft.com/download/details.aspx?id=14632), [x86](https://www.microsoft.com/download/details.aspx?id=5555)).</span><span class="sxs-lookup"><span data-stu-id="d1bc6-225">Alternatively, download and install hello [HPC Pack 2012 R2 Update 3 client utilities](https://www.microsoft.com/download/details.aspx?id=49923) and hello appropriate Visual C++ 2010 redistributable for your computer ([x64](http://www.microsoft.com/download/details.aspx?id=14632), [x86](https://www.microsoft.com/download/details.aspx?id=5555)).</span></span>
5. <span data-ttu-id="d1bc6-226">Neste exemplo, utilizamos um livro do Excel de exemplo com o nome ConvertiblePricing_Complete.xlsb.</span><span class="sxs-lookup"><span data-stu-id="d1bc6-226">In this example, we use a sample Excel workbook named ConvertiblePricing_Complete.xlsb.</span></span> <span data-ttu-id="d1bc6-227">Poderá transferi-lo [aqui](https://www.microsoft.com/en-us/download/details.aspx?id=2939).</span><span class="sxs-lookup"><span data-stu-id="d1bc6-227">You can download it [here](https://www.microsoft.com/en-us/download/details.aspx?id=2939).</span></span>
6. <span data-ttu-id="d1bc6-228">Copie Olá Excel livro tooa a pasta de trabalho, tais como D:\Excel\Run.</span><span class="sxs-lookup"><span data-stu-id="d1bc6-228">Copy hello Excel workbook tooa working folder such as D:\Excel\Run.</span></span>
7. <span data-ttu-id="d1bc6-229">Abra o livro do Excel Olá.</span><span class="sxs-lookup"><span data-stu-id="d1bc6-229">Open hello Excel workbook.</span></span> <span data-ttu-id="d1bc6-230">No Olá **desenvolver** do Friso, clique em **suplementos COM** e confirme que Olá suplemento HPC Pack Excel COM carregada com êxito.</span><span class="sxs-lookup"><span data-stu-id="d1bc6-230">On hello **Develop** ribbon, click **COM Add-Ins** and confirm that hello HPC Pack Excel COM add-in is loaded successfully.</span></span>
   
   ![Excel suplemento para HPC Pack][addin]
8. <span data-ttu-id="d1bc6-232">Editar Olá VBA macro HPCControlMacros no Excel alterando Olá comentado linhas, conforme mostrado no seguinte script de Olá.</span><span class="sxs-lookup"><span data-stu-id="d1bc6-232">Edit hello VBA macro HPCControlMacros in Excel by changing hello commented lines as shown in hello following script.</span></span> <span data-ttu-id="d1bc6-233">Substitua os valores apropriados para o seu ambiente.</span><span class="sxs-lookup"><span data-stu-id="d1bc6-233">Substitute appropriate values for your environment.</span></span>
   
   ![Macro Excel para HPC Pack][macro]
   
   ```
   'Private Const HPC_ClusterScheduler = "HEADNODE_NAME"
   Private Const HPC_ClusterScheduler = "hpc01.eastus.cloudapp.azure.com"
   
   'Private Const HPC_NetworkShare = "\\PATH\TO\SHARE\DIRECTORY"
   Private Const HPC_DependFiles = "D:\Excel\Upload\ConvertiblePricing_Complete.xlsb=ConvertiblePricing_Complete.xlsb"
   
   'HPCExcelClient.Initialize ActiveWorkbook
   HPCExcelClient.Initialize ActiveWorkbook, HPC_DependFiles
   
   'HPCWorkbookPath = HPC_NetworkShare & Application.PathSeparator & ActiveWorkbook.name
   HPCWorkbookPath = "ConvertiblePricing_Complete.xlsb"
   
   'HPCExcelClient.OpenSession headNode:=HPC_ClusterScheduler, remoteWorkbookPath:=HPCWorkbookPath
   HPCExcelClient.OpenSession headNode:=HPC_ClusterScheduler, remoteWorkbookPath:=HPCWorkbookPath, UserName:="hpc\azureuser", Password:="<YourPassword>"
   ```
9. <span data-ttu-id="d1bc6-235">Copie Olá Excel livro tooan carregamento diretório, tais como D:\Excel\Upload.</span><span class="sxs-lookup"><span data-stu-id="d1bc6-235">Copy hello Excel workbook tooan upload directory such as D:\Excel\Upload.</span></span> <span data-ttu-id="d1bc6-236">Este diretório é especificado em constante de HPC_DependsFiles Olá na macro VBA Olá.</span><span class="sxs-lookup"><span data-stu-id="d1bc6-236">This directory is specified in hello HPC_DependsFiles constant in hello VBA macro.</span></span>
10. <span data-ttu-id="d1bc6-237">livro de Olá toorun no cluster de Olá no Azure, clique em Olá **Cluster** botão na folha de cálculo de Olá.</span><span class="sxs-lookup"><span data-stu-id="d1bc6-237">toorun hello workbook on hello cluster in Azure, click hello **Cluster** button on hello worksheet.</span></span>

### <a name="run-excel-udfs"></a><span data-ttu-id="d1bc6-238">Executar UDFs do Excel</span><span class="sxs-lookup"><span data-stu-id="d1bc6-238">Run Excel UDFs</span></span>
<span data-ttu-id="d1bc6-239">toorun UDFs do Excel, siga Olá precedente passos 1 – 3 tooset. o computador de cliente Olá.</span><span class="sxs-lookup"><span data-stu-id="d1bc6-239">toorun Excel UDFs, follow hello preceding steps 1 – 3 tooset up hello client computer.</span></span> <span data-ttu-id="d1bc6-240">Para UDFs do Excel, não precisa de aplicação de Excel toohave Olá instalada em nós de computação.</span><span class="sxs-lookup"><span data-stu-id="d1bc6-240">For Excel UDFs, you don't need toohave hello Excel application installed on compute nodes.</span></span> <span data-ttu-id="d1bc6-241">Para que, quando criar o cluster de nós de computação, que pode escolher uma imagem do nó de computação normal em vez de Olá computação imagens de nó com o Excel.</span><span class="sxs-lookup"><span data-stu-id="d1bc6-241">So, when creating your cluster compute nodes, you could choose a normal compute node image instead of hello compute node image with Excel.</span></span>

> [!NOTE]
> <span data-ttu-id="d1bc6-242">Não há um limite de 34 caracteres no Olá Excel 2010 e a caixa de diálogo de conector de cluster de 2013.</span><span class="sxs-lookup"><span data-stu-id="d1bc6-242">There is a 34 character limit in hello Excel 2010 and 2013 cluster connector dialog box.</span></span> <span data-ttu-id="d1bc6-243">Utilize este cluster de Olá de toospecify da caixa de diálogo que é executado Olá UDFs.</span><span class="sxs-lookup"><span data-stu-id="d1bc6-243">You use this dialog box toospecify hello cluster that runs hello UDFs.</span></span> <span data-ttu-id="d1bc6-244">Se o nome do cluster completo de Olá é maior (por exemplo, hpcexcelhn01.southeastasia.cloudapp.azure.com), não se ajustar na caixa de diálogo Olá.</span><span class="sxs-lookup"><span data-stu-id="d1bc6-244">If hello full cluster name is longer (for example, hpcexcelhn01.southeastasia.cloudapp.azure.com), it does not fit in hello dialog box.</span></span> <span data-ttu-id="d1bc6-245">Olá solução é tooset uma variável de toda a máquina como *CCP_IAASHN* com o valor de Olá do nome de cluster longo Olá.</span><span class="sxs-lookup"><span data-stu-id="d1bc6-245">hello workaround is tooset a machine-wide variable such as *CCP_IAASHN* with hello value of hello long cluster name.</span></span> <span data-ttu-id="d1bc6-246">Em seguida, introduza *% CCP_IAASHN %* na caixa de diálogo de Olá como nome de nó principal do cluster Olá.</span><span class="sxs-lookup"><span data-stu-id="d1bc6-246">Then, enter *%CCP_IAASHN%* in hello dialog box as hello cluster head node name.</span></span> 
> 
> 

<span data-ttu-id="d1bc6-247">Depois do cluster de Olá é implementado com êxito, prosseguir Olá toorun passos a seguir um incorporado de exemplo UDF do Excel.</span><span class="sxs-lookup"><span data-stu-id="d1bc6-247">After hello cluster is successfully deployed, continue with hello following steps toorun a sample built-in Excel UDF.</span></span> <span data-ttu-id="d1bc6-248">Para personalizado UDFs do Excel, consulte estes [recursos](http://social.technet.microsoft.com/wiki/contents/articles/1198.windows-hpc-and-microsoft-excel-resources-for-building-cluster-ready-workbooks.aspx) toobuild Olá XLLs e implementá-los num cluster de IaaS Olá.</span><span class="sxs-lookup"><span data-stu-id="d1bc6-248">For customized Excel UDFs, see these [resources](http://social.technet.microsoft.com/wiki/contents/articles/1198.windows-hpc-and-microsoft-excel-resources-for-building-cluster-ready-workbooks.aspx) toobuild hello XLLs and deploy them on hello IaaS cluster.</span></span>

1. <span data-ttu-id="d1bc6-249">Abra um novo livro do Excel.</span><span class="sxs-lookup"><span data-stu-id="d1bc6-249">Open a new Excel workbook.</span></span> <span data-ttu-id="d1bc6-250">No Olá **desenvolver** do Friso, clique em **suplementos**. Em seguida, na caixa de diálogo Olá, clique em **procurar**, navegue toohello %CCP_HOME%Bin\XLL32 pastas e selecione o exemplo de Olá ClusterUDF32.xll.</span><span class="sxs-lookup"><span data-stu-id="d1bc6-250">On hello **Develop** ribbon, click **Add-Ins**. Then, in hello dialog box, click **Browse**, navigate toohello %CCP_HOME%Bin\XLL32 folder, and select hello sample ClusterUDF32.xll.</span></span> <span data-ttu-id="d1bc6-251">Se hello ClusterUDF32 não existe no computador de cliente Olá, copie-a partir da pasta %CCP_HOME%Bin\XLL32 Olá nó principal Olá.</span><span class="sxs-lookup"><span data-stu-id="d1bc6-251">If hello ClusterUDF32 doesn't exist on hello client machine, copy it from hello %CCP_HOME%Bin\XLL32 folder on hello head node.</span></span>
   
   ![Selecione Olá UDF][udf]
2. <span data-ttu-id="d1bc6-253">Clique em **ficheiro** > **opções** > **avançadas**.</span><span class="sxs-lookup"><span data-stu-id="d1bc6-253">Click **File** > **Options** > **Advanced**.</span></span> <span data-ttu-id="d1bc6-254">Em **fórmulas**, verifique **permitir toorun de funções XLL definido pelo utilizador a um cluster de cálculo**.</span><span class="sxs-lookup"><span data-stu-id="d1bc6-254">Under **Formulas**, check **Allow user-defined XLL functions toorun a compute cluster**.</span></span> <span data-ttu-id="d1bc6-255">Em seguida, clique em **opções** e introduza o nome do cluster completo Olá no **nome de nó principal do Cluster**.</span><span class="sxs-lookup"><span data-stu-id="d1bc6-255">Then click **Options** and enter hello full cluster name in **Cluster head node name**.</span></span> <span data-ttu-id="d1bc6-256">(Que foram anotados anteriormente esta caixa de entrada está limitada too34 carateres, para que um nome de cluster longo não pode caber.</span><span class="sxs-lookup"><span data-stu-id="d1bc6-256">(As noted previously this input box is limited too34 characters, so a long cluster name may not fit.</span></span> <span data-ttu-id="d1bc6-257">É possível utilizar uma variável de toda a máquina aqui para um nome de cluster longo.)</span><span class="sxs-lookup"><span data-stu-id="d1bc6-257">You may use a machine-wide variable here for a long cluster name.)</span></span>
   
   ![Configurar Olá UDF][options]
3. <span data-ttu-id="d1bc6-259">Olá toorun cálculo de UDF num cluster de Olá, clique em Olá célula com o valor =XllGetComputerNameC() e prima Enter.</span><span class="sxs-lookup"><span data-stu-id="d1bc6-259">toorun hello UDF calculation on hello cluster, click hello cell with value =XllGetComputerNameC() and press Enter.</span></span> <span data-ttu-id="d1bc6-260">função de Olá apenas obtém Olá nome de nó de computação de Olá no qual Olá UDF é executada.</span><span class="sxs-lookup"><span data-stu-id="d1bc6-260">hello function simply retrieves hello name of hello compute node on which hello UDF runs.</span></span> <span data-ttu-id="d1bc6-261">Para Olá executar pela primeira vez, uma caixa de diálogo de credenciais pede-lhe Olá nome de utilizador e palavra-passe tooconnect toohello IaaS cluster.</span><span class="sxs-lookup"><span data-stu-id="d1bc6-261">For hello first run, a credentials dialog box prompts for hello username and password tooconnect toohello IaaS cluster.</span></span>
   
   ![Executar UDF][run]
   
   <span data-ttu-id="d1bc6-263">Quando existem demasiadas células toocalculate, prima Alt-Shift-Ctrl + o cálculo de Olá F9 toorun em todas as células.</span><span class="sxs-lookup"><span data-stu-id="d1bc6-263">When there are many cells toocalculate, press Alt-Shift-Ctrl + F9 toorun hello calculation on all cells.</span></span>

## <a name="step-3-run-a-soa-workload-from-an-on-premises-client"></a><span data-ttu-id="d1bc6-264">Passo 3.</span><span class="sxs-lookup"><span data-stu-id="d1bc6-264">Step 3.</span></span> <span data-ttu-id="d1bc6-265">Executar uma carga de trabalho SOA a partir de um cliente no local</span><span class="sxs-lookup"><span data-stu-id="d1bc6-265">Run a SOA workload from an on-premises client</span></span>
<span data-ttu-id="d1bc6-266">aplicações SOA gerais toorun no cluster de HPC Pack IaaS Olá, utilize um dos métodos de Olá pela primeira vez no cluster do passo 1 toodeploy Olá.</span><span class="sxs-lookup"><span data-stu-id="d1bc6-266">toorun general SOA applications on hello HPC Pack IaaS cluster, first use one of hello methods in Step 1 toodeploy hello cluster.</span></span> <span data-ttu-id="d1bc6-267">Especifique uma imagem do nó de computação genérico neste caso, porque não é necessário o Excel em nós de computação Olá.</span><span class="sxs-lookup"><span data-stu-id="d1bc6-267">Specify a generic compute node image in this case, because you do not need Excel on hello compute nodes.</span></span> <span data-ttu-id="d1bc6-268">Em seguida, siga estes passos.</span><span class="sxs-lookup"><span data-stu-id="d1bc6-268">Then follow these steps.</span></span>

1. <span data-ttu-id="d1bc6-269">Após a obtenção de certificado de cluster Olá, importe-o no computador de cliente Olá em Cert: \CurrentUser\Root.</span><span class="sxs-lookup"><span data-stu-id="d1bc6-269">After retrieving hello cluster certificate, import it on hello client computer under Cert:\CurrentUser\Root.</span></span>
2. <span data-ttu-id="d1bc6-270">Instalar Olá [HPC Pack 2012 R2 Update 3 SDK](http://www.microsoft.com/download/details.aspx?id=49921) e [utilitários de cliente do Microsoft HPC Pack 2012 R2 Update 3](https://www.microsoft.com/download/details.aspx?id=49923).</span><span class="sxs-lookup"><span data-stu-id="d1bc6-270">Install hello [HPC Pack 2012 R2 Update 3 SDK](http://www.microsoft.com/download/details.aspx?id=49921) and [HPC Pack 2012 R2 Update 3 client utilities](https://www.microsoft.com/download/details.aspx?id=49923).</span></span> <span data-ttu-id="d1bc6-271">Estas ferramentas permitem-lhe toodevelop e executem aplicações de cliente SOA.</span><span class="sxs-lookup"><span data-stu-id="d1bc6-271">These tools enable you toodevelop and run SOA client applications.</span></span>
3. <span data-ttu-id="d1bc6-272">Transferir Olá HelloWorldR2 [código de exemplo](https://www.microsoft.com/download/details.aspx?id=41633).</span><span class="sxs-lookup"><span data-stu-id="d1bc6-272">Download hello HelloWorldR2 [sample code](https://www.microsoft.com/download/details.aspx?id=41633).</span></span> <span data-ttu-id="d1bc6-273">Abra Olá HelloWorldR2.sln no Visual Studio 2010 ou 2012.</span><span class="sxs-lookup"><span data-stu-id="d1bc6-273">Open hello HelloWorldR2.sln in Visual Studio 2010 or 2012.</span></span> <span data-ttu-id="d1bc6-274">(Este exemplo não é atualmente compatível com versões mais recentes do Visual Studio).</span><span class="sxs-lookup"><span data-stu-id="d1bc6-274">(This sample is not currently compatible with more recent versions of Visual Studio.)</span></span>
4. <span data-ttu-id="d1bc6-275">Compilar o projeto de EchoService Olá primeiro.</span><span class="sxs-lookup"><span data-stu-id="d1bc6-275">Build hello EchoService project first.</span></span> <span data-ttu-id="d1bc6-276">Em seguida, implemente o cluster de IaaS do Olá serviço toohello no Olá mesma forma que implementa tooan-local no cluster.</span><span class="sxs-lookup"><span data-stu-id="d1bc6-276">Then, deploy hello service toohello IaaS cluster in hello same way you deploy tooan on-premises cluster.</span></span> <span data-ttu-id="d1bc6-277">Para obter passos detalhados, consulte Olá Readme.doc no HelloWordR2.</span><span class="sxs-lookup"><span data-stu-id="d1bc6-277">For detailed steps, see hello Readme.doc in HelloWordR2.</span></span> <span data-ttu-id="d1bc6-278">Modificar e criar Olá HellWorldR2 e outros projetos, conforme descrito em Olá seguinte secção toogenerate Olá SOA aplicações cliente que são executados num cluster do IaaS do Azure.</span><span class="sxs-lookup"><span data-stu-id="d1bc6-278">Modify and build hello HellWorldR2 and other projects as described in hello following section toogenerate hello SOA client applications that run on an Azure IaaS cluster.</span></span>

### <a name="use-http-binding-with-azure-storage-queue"></a><span data-ttu-id="d1bc6-279">Utilizar o enlace de Http com a fila de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="d1bc6-279">Use Http binding with Azure storage queue</span></span>
<span data-ttu-id="d1bc6-280">enlace de Http toouse com uma fila de armazenamento do Azure, efetue alterações alguns toohello código de exemplo.</span><span class="sxs-lookup"><span data-stu-id="d1bc6-280">toouse Http binding with an Azure storage queue, make a few changes toohello sample code.</span></span>

* <span data-ttu-id="d1bc6-281">Nome do cluster de Olá de atualização.</span><span class="sxs-lookup"><span data-stu-id="d1bc6-281">Update hello cluster name.</span></span>
  
    ```
  // Before
  const string headnode = "[headnode]";
  // After e.g.
  const string headnode = "hpc01.eastus.cloudapp.azure.com";
  or
  const string headnode = "hpc01.cloudapp.net";
  ```
* <span data-ttu-id="d1bc6-282">Opcionalmente, utilize a predefinição de Olá TransportScheme SessionStartInfo ou explicitamente definido tooHttp.</span><span class="sxs-lookup"><span data-stu-id="d1bc6-282">Optionally, use hello default TransportScheme in SessionStartInfo or explicitly set it tooHttp.</span></span>

```
    info.TransportScheme = TransportScheme.Http;
```

* <span data-ttu-id="d1bc6-283">Utilize o enlace predefinido para Olá BrokerClient.</span><span class="sxs-lookup"><span data-stu-id="d1bc6-283">Use default binding for hello BrokerClient.</span></span>
  
    ```
  // Before
  using (BrokerClient<IService1> client = new BrokerClient<IService1>(session, binding))
  // After
  using (BrokerClient<IService1> client = new BrokerClient<IService1>(session))
  ```
  
    <span data-ttu-id="d1bc6-284">Ou defina explicitamente com Olá basicHttpBinding.</span><span class="sxs-lookup"><span data-stu-id="d1bc6-284">Or set explicitly using hello basicHttpBinding.</span></span>
  
    ```
  BasicHttpBinding binding = new BasicHttpBinding(BasicHttpSecurityMode.TransportWithMessageCredential);
  binding.Security.Message.ClientCredentialType = BasicHttpMessageCredentialType.UserName;    binding.Security.Transport.ClientCredentialType = HttpClientCredentialType.None;
  ```
* <span data-ttu-id="d1bc6-285">Opcionalmente, defina Olá UseAzureQueue sinalizador tootrue no SessionStartInfo.</span><span class="sxs-lookup"><span data-stu-id="d1bc6-285">Optionally, set hello UseAzureQueue flag tootrue in SessionStartInfo.</span></span> <span data-ttu-id="d1bc6-286">Se não for definido, será definido tootrue por predefinição quando o nome do cluster Olá tem sufixos de domínio do Azure e Olá TransportScheme é Http.</span><span class="sxs-lookup"><span data-stu-id="d1bc6-286">If not set, it will be set tootrue by default when hello cluster name has Azure domain suffixes and hello TransportScheme is Http.</span></span>
  
    ```
    info.UseAzureQueue = true;
  ```

### <a name="use-http-binding-without-azure-storage-queue"></a><span data-ttu-id="d1bc6-287">Utilizar o enlace de Http sem fila de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="d1bc6-287">Use Http binding without Azure storage queue</span></span>
<span data-ttu-id="d1bc6-288">enlace de Http toouse sem uma fila de armazenamento do Azure, explicitamente conjunto Olá UseAzureQueue sinalizador toofalse no Olá SessionStartInfo.</span><span class="sxs-lookup"><span data-stu-id="d1bc6-288">toouse Http binding without an Azure storage queue, explicitly set hello UseAzureQueue flag toofalse in hello SessionStartInfo.</span></span>

```
    info.UseAzureQueue = false;
```

### <a name="use-nettcp-binding"></a><span data-ttu-id="d1bc6-289">Utilizar o enlace de NetTcp</span><span class="sxs-lookup"><span data-stu-id="d1bc6-289">Use NetTcp binding</span></span>
<span data-ttu-id="d1bc6-290">toouse NetTcp enlace, a configuração de Olá é cluster de no local de tooan tooconnecting semelhantes.</span><span class="sxs-lookup"><span data-stu-id="d1bc6-290">toouse NetTcp binding, hello configuration is similar tooconnecting tooan on-premises cluster.</span></span> <span data-ttu-id="d1bc6-291">É necessário tooopen alguns pontos finais no nó principal do Olá VM.</span><span class="sxs-lookup"><span data-stu-id="d1bc6-291">You need tooopen a few endpoints on hello head node VM.</span></span> <span data-ttu-id="d1bc6-292">Se utilizou o cluster de Olá de toocreate implementação script Olá HPC Pack IaaS, por exemplo, pontos finais de Olá do conjunto no Olá portal do Azure da seguinte forma.</span><span class="sxs-lookup"><span data-stu-id="d1bc6-292">If you used hello HPC Pack IaaS deployment script toocreate hello cluster, for example, set hello endpoints in hello Azure portal as follows.</span></span>

1. <span data-ttu-id="d1bc6-293">Pare Olá VM.</span><span class="sxs-lookup"><span data-stu-id="d1bc6-293">Stop hello VM.</span></span>
2. <span data-ttu-id="d1bc6-294">Adicionar portas TCP de Olá 9090, 9087, 9091, 9094 para Olá sessão, mediador, Mediador de trabalho e os serviços de dados, respetivamente</span><span class="sxs-lookup"><span data-stu-id="d1bc6-294">Add hello TCP ports 9090, 9087, 9091, 9094 for hello Session, Broker, Broker worker, and Data services, respectively</span></span>
   
    ![Configurar pontos finais][endpoint-new-portal]
3. <span data-ttu-id="d1bc6-296">Inicie Olá VM.</span><span class="sxs-lookup"><span data-stu-id="d1bc6-296">Start hello VM.</span></span>

<span data-ttu-id="d1bc6-297">Olá aplicação de cliente SOA não necessita de alterações, exceto alterar Olá nome head toohello IaaS completa nome do cluster.</span><span class="sxs-lookup"><span data-stu-id="d1bc6-297">hello SOA client application requires no changes except altering hello head name toohello IaaS cluster full name.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d1bc6-298">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="d1bc6-298">Next steps</span></span>
* <span data-ttu-id="d1bc6-299">Consulte [estes recursos](http://social.technet.microsoft.com/wiki/contents/articles/1198.windows-hpc-and-microsoft-excel-resources-for-building-cluster-ready-workbooks.aspx) para obter mais informações sobre como executar cargas de trabalho do Excel com o HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="d1bc6-299">See [these resources](http://social.technet.microsoft.com/wiki/contents/articles/1198.windows-hpc-and-microsoft-excel-resources-for-building-cluster-ready-workbooks.aspx) for more information about running Excel workloads with HPC Pack.</span></span>
* <span data-ttu-id="d1bc6-300">Consulte [gerir serviços SOA no Microsoft HPC Pack](https://technet.microsoft.com/library/ff919412.aspx) para obter mais informações sobre como implementar e gerir serviços SOA com o HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="d1bc6-300">See [Managing SOA Services in Microsoft HPC Pack](https://technet.microsoft.com/library/ff919412.aspx) for more about deploying and managing SOA services with HPC Pack.</span></span>

<!--Image references-->
[scenario]: ./media/excel-cluster-hpcpack/scenario.png
[github]: ./media/excel-cluster-hpcpack/github.png
[template]: ./media/excel-cluster-hpcpack/template.png
[parameters]: ./media/excel-cluster-hpcpack/parameters.png
[parameters-new-portal]: ./media/excel-cluster-hpcpack/parameters-new-portal.png
[create]: ./media/excel-cluster-hpcpack/create.png
[connect]: ./media/excel-cluster-hpcpack/connect.png
[cert]: ./media/excel-cluster-hpcpack/cert.png
[addin]: ./media/excel-cluster-hpcpack/addin.png
[macro]: ./media/excel-cluster-hpcpack/macro.png
[options]: ./media/excel-cluster-hpcpack/options.png
[run]: ./media/excel-cluster-hpcpack/run.png
[endpoint]: ./media/excel-cluster-hpcpack/endpoint.png
[endpoint-new-portal]: ./media/excel-cluster-hpcpack/endpoint-new-portal.png
[udf]: ./media/excel-cluster-hpcpack/udf.png
