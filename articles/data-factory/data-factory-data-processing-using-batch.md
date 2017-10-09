---
title: aaaProcess conjuntos de dados em grande escala com o Data Factory e Batch | Microsoft Docs
description: Descreve como o pipeline de tooprocess quantidades enormes de dados de um Azure Data Factory, utilizando a capacidade de processamento paralelo de lote do Azure.
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 688b964b-51d0-4faa-91a7-26c7e3150868
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: spelluru
ms.openlocfilehash: 6788f02de555d2e9d6588cc990a39043866d7e97
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="process-large-scale-datasets-using-data-factory-and-batch"></a><span data-ttu-id="5d06c-103">Processar grandes conjuntos de dados com o Data Factory e o Batch</span><span class="sxs-lookup"><span data-stu-id="5d06c-103">Process large-scale datasets using Data Factory and Batch</span></span>
<span data-ttu-id="5d06c-104">Este artigo descreve uma arquitetura de uma solução de exemplo que se move e processa os conjuntos de dados em grande escala de forma automática e agendada.</span><span class="sxs-lookup"><span data-stu-id="5d06c-104">This article describes an architecture of a sample solution that moves and processes large-scale datasets in an automatic and scheduled manner.</span></span> <span data-ttu-id="5d06c-105">Também fornece uma solução de Olá instruções ponto a ponto tooimplement através do Azure Data Factory e do Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="5d06c-105">It also provides an end-to-end walkthrough tooimplement hello solution using Azure Data Factory and Azure Batch.</span></span>

<span data-ttu-id="5d06c-106">Este artigo é maior do que o nosso artigo típico porque contém uma explicação passo a passo de uma solução de exemplo completo.</span><span class="sxs-lookup"><span data-stu-id="5d06c-106">This article is longer than our typical article because it contains a walkthrough of an entire sample solution.</span></span> <span data-ttu-id="5d06c-107">Se for novo tooBatch e fábrica de dados, pode saber sobre estes serviços e como funcionam em conjunto.</span><span class="sxs-lookup"><span data-stu-id="5d06c-107">If you are new tooBatch and Data Factory, you can learn about these services and how they work together.</span></span> <span data-ttu-id="5d06c-108">Se souber algo sobre os serviços de Olá e são estruturar/arquitetar uma solução, pode concentrar-se apenas nos Olá [secção de arquitetura](#architecture-of-sample-solution) do artigo Olá e se estiver a desenvolver um protótipo ou uma solução, também poderá tootry instruções passo a passo Olá [instruções](#implementation-of-sample-solution).</span><span class="sxs-lookup"><span data-stu-id="5d06c-108">If you know something about hello services and are designing/architecting a solution, you may focus just on hello [architecture section](#architecture-of-sample-solution) of hello article and if you are developing a prototype or a solution, you may also want tootry out step-by-step instructions in hello [walkthrough](#implementation-of-sample-solution).</span></span> <span data-ttu-id="5d06c-109">Convidamo-os seus comentários sobre este conteúdo e como utilizá-lo.</span><span class="sxs-lookup"><span data-stu-id="5d06c-109">We invite your comments about this content and how you use it.</span></span>

<span data-ttu-id="5d06c-110">Em primeiro lugar, vamos ver como podem ajudar a fábrica de dados e Batch serviços com grandes conjuntos de dados na nuvem de Olá de processamento.</span><span class="sxs-lookup"><span data-stu-id="5d06c-110">First, let's look at how Data Factory and Batch services can help with processing large datasets in hello cloud.</span></span>     

## <a name="why-azure-batch"></a><span data-ttu-id="5d06c-111">Por que motivo o Azure Batch?</span><span class="sxs-lookup"><span data-stu-id="5d06c-111">Why Azure Batch?</span></span>
<span data-ttu-id="5d06c-112">O Azure Batch permite-lhe toorun em grande escala paralelas e elevado desempenho aplicações de computação (HPC) e forma eficiente na nuvem de Olá.</span><span class="sxs-lookup"><span data-stu-id="5d06c-112">Azure Batch enables you toorun large-scale parallel and high-performance computing (HPC) applications efficiently in hello cloud.</span></span> <span data-ttu-id="5d06c-113">É um serviço de plataforma que agenda trabalho de computação intensiva toorun numa coleção gerida de máquinas virtuais e pode dimensionar automaticamente de computação necessidades de Olá toomeet recursos das suas tarefas.</span><span class="sxs-lookup"><span data-stu-id="5d06c-113">It's a platform service that schedules compute-intensive work toorun on a managed collection of virtual machines, and can automatically scale compute resources toomeet hello needs of your jobs.</span></span>

<span data-ttu-id="5d06c-114">Com o serviço Batch Olá, é possível definir tooexecute de recursos de computação do Azure as suas aplicações em paralelo e com dimensionamento.</span><span class="sxs-lookup"><span data-stu-id="5d06c-114">With hello Batch service, you define Azure compute resources tooexecute your applications in parallel, and at scale.</span></span> <span data-ttu-id="5d06c-115">Pode executar a pedido ou agendadas tarefas e não precisa de toomanually criar, configurar e gerir um cluster HPC, máquinas virtuais individuais, redes virtuais ou uma tarefa complexa e infraestrutura de agendamento de tarefas.</span><span class="sxs-lookup"><span data-stu-id="5d06c-115">You can run on-demand or scheduled jobs, and you don't need toomanually create, configure, and manage an HPC cluster, individual virtual machines, virtual networks, or a complex job and task scheduling infrastructure.</span></span>

<span data-ttu-id="5d06c-116">Consulte Olá seguintes artigos se não estiver familiarizado com o Azure Batch como ajuda com compreender Olá arquitetura/implementação da solução de Olá descrita neste artigo.</span><span class="sxs-lookup"><span data-stu-id="5d06c-116">See hello following articles if you are not familiar with Azure Batch as it helps with understanding hello architecture/implementation of hello solution described in this article.</span></span>   

* [<span data-ttu-id="5d06c-117">Noções básicas do Azure Batch</span><span class="sxs-lookup"><span data-stu-id="5d06c-117">Basics of Azure Batch</span></span>](../batch/batch-technical-overview.md)
* [<span data-ttu-id="5d06c-118">Descrição geral da funcionalidade do Batch</span><span class="sxs-lookup"><span data-stu-id="5d06c-118">Batch feature overview</span></span>](../batch/batch-api-basics.md)

<span data-ttu-id="5d06c-119">(opcional) toolearn mais informações sobre o Azure Batch, consulte Olá [percurso de aprendizagem para o Azure Batch](https://azure.microsoft.com/documentation/learning-paths/batch/).</span><span class="sxs-lookup"><span data-stu-id="5d06c-119">(optional) toolearn more about Azure Batch, see hello [Learning path for Azure Batch](https://azure.microsoft.com/documentation/learning-paths/batch/).</span></span>

## <a name="why-azure-data-factory"></a><span data-ttu-id="5d06c-120">Por que motivo fábrica de dados do Azure?</span><span class="sxs-lookup"><span data-stu-id="5d06c-120">Why Azure Data Factory?</span></span>
<span data-ttu-id="5d06c-121">Data Factory é um serviço de integração de dados baseado na nuvem que orquestra e automatiza o movimento de Olá e a transformação de dados.</span><span class="sxs-lookup"><span data-stu-id="5d06c-121">Data Factory is a cloud-based data integration service that orchestrates and automates hello movement and transformation of data.</span></span> <span data-ttu-id="5d06c-122">Utilizar o serviço do Data Factory Olá, pode criar pipelines de dados geridos que movem os dados no local e na nuvem arquivo de dados centralizada de tooa de arquivos de dados (por exemplo: Blob Storage do Azure) e o processo/transformação dados através de serviços como o Azure HDInsight e do Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="5d06c-122">Using hello Data Factory service, you can create managed data pipelines that move data from on-premises and cloud data stores tooa centralized data store (for example: Azure Blob Storage), and process/transform data using services such as Azure HDInsight and Azure Machine Learning.</span></span> <span data-ttu-id="5d06c-123">Também pode agendar toorun de pipelines de dados no monitor e forma agendada (hora a hora, diária, semanal, etc.) e geri-los em problemas de tooidentify um rapidamente e tomar medidas.</span><span class="sxs-lookup"><span data-stu-id="5d06c-123">You can also schedule data pipelines toorun in a scheduled manner (hourly, daily, weekly, etc.) and monitor and manage them at a glance tooidentify issues and take action.</span></span>

<span data-ttu-id="5d06c-124">Consulte Olá seguintes artigos se não estiver familiarizado com o Azure Data Factory como ajuda com compreender Olá arquitetura/implementação da solução de Olá descrita neste artigo.</span><span class="sxs-lookup"><span data-stu-id="5d06c-124">See hello following articles if you are not familiar with Azure Data Factory as it helps with understanding hello architecture/implementation of hello solution described in this article.</span></span>  

* [<span data-ttu-id="5d06c-125">Introdução ao Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="5d06c-125">Introduction of Azure Data Factory</span></span>](data-factory-introduction.md)
* [<span data-ttu-id="5d06c-126">Criar o seu primeiro pipeline de dados</span><span class="sxs-lookup"><span data-stu-id="5d06c-126">Build your first data pipeline</span></span>](data-factory-build-your-first-pipeline.md)   

<span data-ttu-id="5d06c-127">(opcional) toolearn mais informações sobre o Azure Data Factory, consulte Olá [percurso de aprendizagem do Azure Data Factory](https://azure.microsoft.com/documentation/learning-paths/data-factory/).</span><span class="sxs-lookup"><span data-stu-id="5d06c-127">(optional) toolearn more about Azure Data Factory, see hello [Learning path for Azure Data Factory](https://azure.microsoft.com/documentation/learning-paths/data-factory/).</span></span>

## <a name="data-factory-and-batch-together"></a><span data-ttu-id="5d06c-128">Fábrica de dados e em conjunto do Batch</span><span class="sxs-lookup"><span data-stu-id="5d06c-128">Data Factory and Batch together</span></span>
<span data-ttu-id="5d06c-129">Fábrica de dados inclui atividades incorporadas, como o arquivo de dados de destino tooa e dados de tooprocess de atividade do ramo de registo utilizando clusters do Hadoop (HDInsight) no Azure do arquivo de dados de toocopy/mover de atividade de cópia de uma origem de dados.</span><span class="sxs-lookup"><span data-stu-id="5d06c-129">Data Factory includes built-in activities such as Copy Activity toocopy/move data from a source data store tooa destination data store and Hive Activity tooprocess data using Hadoop clusters (HDInsight) on Azure.</span></span> <span data-ttu-id="5d06c-130">Consulte [atividades de transformação de dados](data-factory-data-transformation-activities.md) para uma lista de atividades de transformação suportados.</span><span class="sxs-lookup"><span data-stu-id="5d06c-130">See [Data Transformation Activities](data-factory-data-transformation-activities.md) for a list of supported transformation activities.</span></span>

<span data-ttu-id="5d06c-131">Também permite toocreate .NET atividades personalizadas toomove ou processo de dados com a sua própria lógica e executar estas atividades num cluster do HDInsight do Azure ou num conjunto de VMs do Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="5d06c-131">It also allows you toocreate custom .NET activities toomove or process data with your own logic and run these activities on an Azure HDInsight cluster or on an Azure Batch pool of VMs.</span></span> <span data-ttu-id="5d06c-132">Quando utilizar o Azure Batch, pode configurar o conjunto de Olá tooauto hiper escala (adicionar ou remover VMs com base na carga de trabalho Olá) com base numa fórmula que fornecer.</span><span class="sxs-lookup"><span data-stu-id="5d06c-132">When you use Azure Batch, you can configure hello pool tooauto-scale (add or remove VMs based on hello workload) based on a formula you provide.</span></span>     

## <a name="architecture-of-sample-solution"></a><span data-ttu-id="5d06c-133">Arquitetura de solução de exemplo</span><span class="sxs-lookup"><span data-stu-id="5d06c-133">Architecture of sample solution</span></span>
<span data-ttu-id="5d06c-134">Apesar de arquitetura de Olá descrita neste artigo destina-se uma solução simples, é toocomplex relevantes cenários tais como a modelação de serviços financeiros, processamento de imagem e composição e análise genomic riscos.</span><span class="sxs-lookup"><span data-stu-id="5d06c-134">Even though hello architecture described in this article is for a simple solution, it is relevant toocomplex scenarios such as risk modeling by financial services, image processing and rendering, and genomic analysis.</span></span>

<span data-ttu-id="5d06c-135">Diagrama de Olá ilustra 1) como o Data Factory orquestra movimento de dados e processamento e 2) como o Azure Batch processa Olá dados de forma paralela.</span><span class="sxs-lookup"><span data-stu-id="5d06c-135">hello diagram illustrates 1) how Data Factory orchestrates data movement and processing and 2) how Azure Batch processes hello data in a parallel manner.</span></span> <span data-ttu-id="5d06c-136">Transferir e diagrama de impressão Olá para fácil referência (11 x 17 pol.</span><span class="sxs-lookup"><span data-stu-id="5d06c-136">Download and print hello diagram for easy reference (11 x 17 in.</span></span> <span data-ttu-id="5d06c-137">ou tamanho A3): [HPC e de dados orchestration através do Azure Batch e do Data Factory](http://go.microsoft.com/fwlink/?LinkId=717686).</span><span class="sxs-lookup"><span data-stu-id="5d06c-137">or A3 size): [HPC and data orchestration using Azure Batch and Data Factory](http://go.microsoft.com/fwlink/?LinkId=717686).</span></span>

<span data-ttu-id="5d06c-138">[![Diagrama de processamento de dados em grande escala](./media/data-factory-data-processing-using-batch/image1.png)](http://go.microsoft.com/fwlink/?LinkId=717686)</span><span class="sxs-lookup"><span data-stu-id="5d06c-138">[![Large-scale data processing diagram](./media/data-factory-data-processing-using-batch/image1.png)](http://go.microsoft.com/fwlink/?LinkId=717686)</span></span>

<span data-ttu-id="5d06c-139">Olá lista seguinte fornece os passos básicos Olá do processo de Olá.</span><span class="sxs-lookup"><span data-stu-id="5d06c-139">hello following list provides hello basic steps of hello process.</span></span> <span data-ttu-id="5d06c-140">Olá inclui código de solução e de explicações toobuild Olá ponto-a-ponto.</span><span class="sxs-lookup"><span data-stu-id="5d06c-140">hello solution includes code and explanations toobuild hello end-to-end solution.</span></span>

1. <span data-ttu-id="5d06c-141">**Configurar o Azure Batch com um conjunto de nós de computação (VMs)**.</span><span class="sxs-lookup"><span data-stu-id="5d06c-141">**Configure Azure Batch with a pool of compute nodes (VMs)**.</span></span> <span data-ttu-id="5d06c-142">Pode especificar o número de Olá de nós e o tamanho de cada nó.</span><span class="sxs-lookup"><span data-stu-id="5d06c-142">You can specify hello number of nodes and size of each node.</span></span>
2. <span data-ttu-id="5d06c-143">**Criar uma instância do Azure Data Factory** que está configurado com entidades que representam o blob storage do Azure, serviço de computação do Azure Batch, dados de entrada/saída e um fluxo de trabalho pipeline com atividades que mover e transforme dados.</span><span class="sxs-lookup"><span data-stu-id="5d06c-143">**Create an Azure Data Factory instance** that is configured with entities that represent Azure blob storage, Azure Batch compute service, input/output data, and a workflow/pipeline with activities that move and transform data.</span></span>
3. <span data-ttu-id="5d06c-144">**Criar uma atividade personalizada do .NET no pipeline do Data Factory Olá**.</span><span class="sxs-lookup"><span data-stu-id="5d06c-144">**Create a custom .NET activity in hello Data Factory pipeline**.</span></span> <span data-ttu-id="5d06c-145">atividade de Olá é o código de utilizador que é executado no Olá conjunto do Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="5d06c-145">hello activity is your user code that runs on hello Azure Batch pool.</span></span>
4. <span data-ttu-id="5d06c-146">**Armazenar grandes quantidades de dados de entrada que os blobs no armazenamento do Azure**.</span><span class="sxs-lookup"><span data-stu-id="5d06c-146">**Store large amounts of input data as blobs in Azure storage**.</span></span> <span data-ttu-id="5d06c-147">Dados estão divididos em setores lógicas (normalmente por hora).</span><span class="sxs-lookup"><span data-stu-id="5d06c-147">Data is divided into logical slices (usually by time).</span></span>
5. <span data-ttu-id="5d06c-148">**Fábrica de dados copia os dados que estão a ser processados em paralelo** toohello de localização secundária.</span><span class="sxs-lookup"><span data-stu-id="5d06c-148">**Data Factory copies data that is processed in parallel** toohello secondary location.</span></span>
6. <span data-ttu-id="5d06c-149">**Fábrica de dados executa atividades personalizadas Olá utilizar agrupamento Olá atribuído pelo Batch**.</span><span class="sxs-lookup"><span data-stu-id="5d06c-149">**Data Factory runs hello custom activity using hello pool allocated by Batch**.</span></span> <span data-ttu-id="5d06c-150">Fábrica de dados pode ser executados atividades em simultâneo.</span><span class="sxs-lookup"><span data-stu-id="5d06c-150">Data Factory can run activities concurrently.</span></span> <span data-ttu-id="5d06c-151">Cada atividade processa um setor de dados.</span><span class="sxs-lookup"><span data-stu-id="5d06c-151">Each activity processes a slice of data.</span></span> <span data-ttu-id="5d06c-152">resultados de Olá são armazenados no armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="5d06c-152">hello results are stored in Azure storage.</span></span>
7. <span data-ttu-id="5d06c-153">**Fábrica de dados move a localização de terceira Olá resultados final tooa**, para distribuição através de uma aplicação ou para processamento adicional por outras ferramentas.</span><span class="sxs-lookup"><span data-stu-id="5d06c-153">**Data Factory moves hello final results tooa third location**, either for distribution via an app, or for further processing by other tools.</span></span>

## <a name="implementation-of-sample-solution"></a><span data-ttu-id="5d06c-154">Implementação da solução de exemplo</span><span class="sxs-lookup"><span data-stu-id="5d06c-154">Implementation of sample solution</span></span>
<span data-ttu-id="5d06c-155">solução de exemplo de Olá é intencionalmente simple e é tooshow como toouse fábrica de dados e Batch tooprocess em conjunto os conjuntos de dados.</span><span class="sxs-lookup"><span data-stu-id="5d06c-155">hello sample solution is intentionally simple and is tooshow you how toouse Data Factory and Batch together tooprocess datasets.</span></span> <span data-ttu-id="5d06c-156">solução Olá conta simplesmente o número de Olá de ocorrências de um termo de pesquisa ("Microsoft") nos ficheiros de entrada organizados de uma série de tempo.</span><span class="sxs-lookup"><span data-stu-id="5d06c-156">hello solution simply counts hello number of occurrences of a search term (“Microsoft”) in input files organized in a time series.</span></span> <span data-ttu-id="5d06c-157">-Produz os ficheiros de toooutput Olá contagem.</span><span class="sxs-lookup"><span data-stu-id="5d06c-157">It outputs hello count toooutput files.</span></span>

<span data-ttu-id="5d06c-158">**Tempo**: Se estiver familiarizado com as noções básicas do Azure, a fábrica de dados e o Batch e tem os pré-requisitos de Olá concluída listados abaixo, iremos fazer a estimativa esta solução assume toocomplete 1-2 horas.</span><span class="sxs-lookup"><span data-stu-id="5d06c-158">**Time**: If you are familiar with basics of Azure, Data Factory, and Batch, and have completed hello prerequisites listed below, we estimate this solution takes 1-2 hours toocomplete.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="5d06c-159">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="5d06c-159">Prerequisites</span></span>
#### <a name="azure-subscription"></a><span data-ttu-id="5d06c-160">Subscrição do Azure</span><span class="sxs-lookup"><span data-stu-id="5d06c-160">Azure subscription</span></span>
<span data-ttu-id="5d06c-161">Se não tiver uma subscrição do Azure, pode criar uma conta de avaliação gratuita em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="5d06c-161">If you don't have an Azure subscription, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="5d06c-162">Consulte [avaliação gratuita](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5d06c-162">See [Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

#### <a name="azure-storage-account"></a><span data-ttu-id="5d06c-163">Conta de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="5d06c-163">Azure storage account</span></span>
<span data-ttu-id="5d06c-164">Utilize uma conta de armazenamento do Azure para armazenar dados de Olá neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="5d06c-164">You use an Azure storage account for storing hello data in this tutorial.</span></span> <span data-ttu-id="5d06c-165">Se não tiver uma conta de armazenamento do Azure, consulte o artigo [criar uma conta de armazenamento](../storage/common/storage-create-storage-account.md#create-a-storage-account).</span><span class="sxs-lookup"><span data-stu-id="5d06c-165">If you don't have an Azure storage account, see [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account).</span></span> <span data-ttu-id="5d06c-166">solução de exemplo de Olá utiliza o armazenamento de Blobs.</span><span class="sxs-lookup"><span data-stu-id="5d06c-166">hello sample solution uses blob storage.</span></span>

#### <a name="azure-batch-account"></a><span data-ttu-id="5d06c-167">Conta de Batch do Azure</span><span class="sxs-lookup"><span data-stu-id="5d06c-167">Azure Batch account</span></span>
<span data-ttu-id="5d06c-168">Criar uma conta do Azure Batch com Olá [portal do Azure](http://manage.windowsazure.com/).</span><span class="sxs-lookup"><span data-stu-id="5d06c-168">Create an Azure Batch account using hello [Azure portal](http://manage.windowsazure.com/).</span></span> <span data-ttu-id="5d06c-169">Consulte [criar e gerir uma conta do Azure Batch](../batch/batch-account-create-portal.md).</span><span class="sxs-lookup"><span data-stu-id="5d06c-169">See [Create and manage an Azure Batch account](../batch/batch-account-create-portal.md).</span></span> <span data-ttu-id="5d06c-170">Tenha em atenção Olá do Azure Batch e conta de nome de chave da conta.</span><span class="sxs-lookup"><span data-stu-id="5d06c-170">Note hello Azure Batch account name and account key.</span></span> <span data-ttu-id="5d06c-171">Também pode utilizar [New-AzureRmBatchAccount](https://msdn.microsoft.com/library/mt603749.aspx) cmdlet toocreate uma conta do Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="5d06c-171">You can also use [New-AzureRmBatchAccount](https://msdn.microsoft.com/library/mt603749.aspx) cmdlet toocreate an Azure Batch account.</span></span> <span data-ttu-id="5d06c-172">Consulte [introdução aos cmdlets do Azure Batch PowerShell](../batch/batch-powershell-cmdlets-get-started.md) para obter instruções detalhadas sobre como utilizar este cmdlet.</span><span class="sxs-lookup"><span data-stu-id="5d06c-172">See [Get started with Azure Batch PowerShell cmdlets](../batch/batch-powershell-cmdlets-get-started.md) for detailed instructions on using this cmdlet.</span></span>

<span data-ttu-id="5d06c-173">solução de exemplo de Olá utiliza dados do Azure Batch (indiretamente através de um pipeline do Azure Data Factory) tooprocess de forma parallel num conjunto de nós de computação (coleção gerida de máquinas virtuais).</span><span class="sxs-lookup"><span data-stu-id="5d06c-173">hello sample solution uses Azure Batch (indirectly via an Azure Data Factory pipeline) tooprocess data in a parallel manner on a pool of compute nodes (a managed collection of virtual machines).</span></span>

#### <a name="azure-batch-pool-of-virtual-machines-vms"></a><span data-ttu-id="5d06c-174">Conjunto do Batch do Azure de máquinas virtuais (VMs)</span><span class="sxs-lookup"><span data-stu-id="5d06c-174">Azure Batch pool of virtual machines (VMs)</span></span>
<span data-ttu-id="5d06c-175">Criar um **conjunto do Azure Batch** com, pelo menos, 2 nós de computação.</span><span class="sxs-lookup"><span data-stu-id="5d06c-175">Create an **Azure Batch pool** with at least 2 compute nodes.</span></span>

1. <span data-ttu-id="5d06c-176">No Olá [portal do Azure](https://portal.azure.com), clique em **procurar** no Olá menu à esquerda e clique em **contas do Batch**.</span><span class="sxs-lookup"><span data-stu-id="5d06c-176">In hello [Azure portal](https://portal.azure.com), click **Browse** in hello left menu, and click **Batch Accounts**.</span></span>
2. <span data-ttu-id="5d06c-177">Selecione o seu Olá de tooopen de conta do Azure Batch **conta do Batch** painel.</span><span class="sxs-lookup"><span data-stu-id="5d06c-177">Select your Azure Batch account tooopen hello **Batch Account** blade.</span></span>
3. <span data-ttu-id="5d06c-178">Clique em **agrupamentos** mosaico.</span><span class="sxs-lookup"><span data-stu-id="5d06c-178">Click **Pools** tile.</span></span>
4. <span data-ttu-id="5d06c-179">No Olá **agrupamentos** painel, clique em Adicionar botão na barra de ferramentas de Olá tooadd um conjunto.</span><span class="sxs-lookup"><span data-stu-id="5d06c-179">In hello **Pools** blade, click Add button on hello toolbar tooadd a pool.</span></span>
   1. <span data-ttu-id="5d06c-180">Introduza um ID para o conjunto de Olá (**ID do conjunto**).</span><span class="sxs-lookup"><span data-stu-id="5d06c-180">Enter an ID for hello pool (**Pool ID**).</span></span> <span data-ttu-id="5d06c-181">Olá nota **ID do conjunto de Olá**; apenas quando criar a solução de fábrica de dados de Olá.</span><span class="sxs-lookup"><span data-stu-id="5d06c-181">Note hello **ID of hello pool**; you need it when creating hello Data Factory solution.</span></span>
   2. <span data-ttu-id="5d06c-182">Especifique **Windows Server 2012 R2** para definição do Olá família do sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="5d06c-182">Specify **Windows Server 2012 R2** for hello Operating System Family setting.</span></span>
   3. <span data-ttu-id="5d06c-183">Selecione um **escalão de preço de nó**.</span><span class="sxs-lookup"><span data-stu-id="5d06c-183">Select a **node pricing tier**.</span></span>
   4. <span data-ttu-id="5d06c-184">Introduza **2** como valor de Olá **destino dedicado** definição.</span><span class="sxs-lookup"><span data-stu-id="5d06c-184">Enter **2** as value for hello **Target Dedicated** setting.</span></span>
   5. <span data-ttu-id="5d06c-185">Introduza **2** como valor de Olá **máx. tarefas por nó** definição.</span><span class="sxs-lookup"><span data-stu-id="5d06c-185">Enter **2** as value for hello **Max tasks per node** setting.</span></span>
   6. <span data-ttu-id="5d06c-186">Clique em **OK** conjunto de Olá toocreate.</span><span class="sxs-lookup"><span data-stu-id="5d06c-186">Click **OK** toocreate hello pool.</span></span>

#### <a name="azure-storage-explorer"></a><span data-ttu-id="5d06c-187">Explorador do Storage do Azure</span><span class="sxs-lookup"><span data-stu-id="5d06c-187">Azure Storage Explorer</span></span>
<span data-ttu-id="5d06c-188">[6 do Explorador de armazenamento do Azure (ferramenta)](https://azurestorageexplorer.codeplex.com/) ou [CloudXplorer](http://clumsyleaf.com/products/cloudxplorer) (a partir do ClumsyLeaf Software).</span><span class="sxs-lookup"><span data-stu-id="5d06c-188">[Azure Storage Explorer 6 (tool)](https://azurestorageexplorer.codeplex.com/) or [CloudXplorer](http://clumsyleaf.com/products/cloudxplorer) (from ClumsyLeaf Software).</span></span> <span data-ttu-id="5d06c-189">Utilizar estas ferramentas para inspecionar e alteração de dados de Olá nos seus projetos de armazenamento do Azure, incluindo Olá os registos das suas aplicações alojadas na nuvem.</span><span class="sxs-lookup"><span data-stu-id="5d06c-189">You use these tools for inspecting and altering hello data in your Azure Storage projects including hello logs of your cloud-hosted applications.</span></span>

1. <span data-ttu-id="5d06c-190">Criar um contentor com o nome **mycontainer** com acesso privado (sem acesso anónimo)</span><span class="sxs-lookup"><span data-stu-id="5d06c-190">Create a container named **mycontainer** with private access (no anonymous access)</span></span>
2. <span data-ttu-id="5d06c-191">Se estiver a utilizar **CloudXplorer**, criar pastas e subpastas com Olá a seguir a estrutura:</span><span class="sxs-lookup"><span data-stu-id="5d06c-191">If you are using **CloudXplorer**, create folders and subfolders with hello following structure:</span></span>

   ![](./media/data-factory-data-processing-using-batch/image3.png)

   <span data-ttu-id="5d06c-192">`Inputfolder`e `outputfolder` são pastas de nível superior no `mycontainer`.</span><span class="sxs-lookup"><span data-stu-id="5d06c-192">`Inputfolder` and `outputfolder` are top-level folders in `mycontainer`.</span></span> <span data-ttu-id="5d06c-193">Olá `inputfolder` tem subpastas com carimbos de data / hora (AAAA-MM-DD-HH).</span><span class="sxs-lookup"><span data-stu-id="5d06c-193">hello `inputfolder` has subfolders with date-time stamps (YYYY-MM-DD-HH).</span></span>

   <span data-ttu-id="5d06c-194">Se estiver a utilizar **Explorador de armazenamento do Azure**, no próximo passo Olá, terá de tooupload os ficheiros com nomes: `inputfolder/2015-11-16-00/file.txt`, `inputfolder/2015-11-16-01/file.txt` e assim sucessivamente.</span><span class="sxs-lookup"><span data-stu-id="5d06c-194">If you are using **Azure Storage Explorer**, in hello next step, you need tooupload files with names: `inputfolder/2015-11-16-00/file.txt`, `inputfolder/2015-11-16-01/file.txt` and so on.</span></span> <span data-ttu-id="5d06c-195">Este passo cria automaticamente a pastas Olá.</span><span class="sxs-lookup"><span data-stu-id="5d06c-195">This step automatically creates hello folders.</span></span>
3. <span data-ttu-id="5d06c-196">Criar um ficheiro de texto **file.txt** no seu computador com o conteúdo que tenha a palavra-chave de Olá **Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="5d06c-196">Create a text file **file.txt** on your machine with content that has hello keyword **Microsoft**.</span></span> <span data-ttu-id="5d06c-197">Por exemplo: "atividades personalizadas do atividade personalizada Microsoft teste Microsoft de teste".</span><span class="sxs-lookup"><span data-stu-id="5d06c-197">For example: “test custom activity Microsoft test custom activity Microsoft”.</span></span>
4. <span data-ttu-id="5d06c-198">Carregar Olá ficheiro toohello seguir entradas pastas no armazenamento de Blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="5d06c-198">Upload hello file toohello following input folders in Azure blob storage.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image4.png)

   <span data-ttu-id="5d06c-199">Se estiver a utilizar **Explorador de armazenamento do Azure**, carregue o ficheiro de Olá **file.txt** demasiado**mycontainer**.</span><span class="sxs-lookup"><span data-stu-id="5d06c-199">If you are using **Azure Storage Explorer**, upload hello file **file.txt** too**mycontainer**.</span></span> <span data-ttu-id="5d06c-200">Clique em **cópia** na barra de ferramentas de Olá toocreate uma cópia do blob Olá.</span><span class="sxs-lookup"><span data-stu-id="5d06c-200">Click **Copy** on hello toolbar toocreate a copy of hello blob.</span></span> <span data-ttu-id="5d06c-201">No Olá **copiar Blob** caixa de diálogo, a alteração Olá **nome do blob de destino** demasiado`inputfolder/2015-11-16-00/file.txt`.</span><span class="sxs-lookup"><span data-stu-id="5d06c-201">In hello **Copy Blob** dialog box, change hello **destination blob name** too`inputfolder/2015-11-16-00/file.txt`.</span></span> <span data-ttu-id="5d06c-202">Repita este passo toocreate `inputfolder/2015-11-16-01/file.txt`, `inputfolder/2015-11-16-02/file.txt`, `inputfolder/2015-11-16-03/file.txt`, `inputfolder/2015-11-16-04/file.txt` e assim sucessivamente.</span><span class="sxs-lookup"><span data-stu-id="5d06c-202">Repeat this step toocreate `inputfolder/2015-11-16-01/file.txt`, `inputfolder/2015-11-16-02/file.txt`, `inputfolder/2015-11-16-03/file.txt`, `inputfolder/2015-11-16-04/file.txt` and so on.</span></span> <span data-ttu-id="5d06c-203">Esta ação cria automaticamente a pastas Olá.</span><span class="sxs-lookup"><span data-stu-id="5d06c-203">This action automatically creates hello folders.</span></span>
5. <span data-ttu-id="5d06c-204">Criar outro contentor com o nome: `customactivitycontainer`.</span><span class="sxs-lookup"><span data-stu-id="5d06c-204">Create another container named: `customactivitycontainer`.</span></span> <span data-ttu-id="5d06c-205">Carregue o contentor de toothis Olá atividade personalizada zip ficheiros.</span><span class="sxs-lookup"><span data-stu-id="5d06c-205">You upload hello custom activity zip file toothis container.</span></span>

#### <a name="visual-studio"></a><span data-ttu-id="5d06c-206">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="5d06c-206">Visual Studio</span></span>
<span data-ttu-id="5d06c-207">Instale o Microsoft Visual Studio 2012 ou posterior toocreate Olá personalizado Batch atividade toobe utilizado no Olá solução Data Factory.</span><span class="sxs-lookup"><span data-stu-id="5d06c-207">Install Microsoft Visual Studio 2012 or later toocreate hello custom Batch activity toobe used in hello Data Factory solution.</span></span>

### <a name="high-level-steps-toocreate-hello-solution"></a><span data-ttu-id="5d06c-208">Solução de Olá toocreate de passos de alto nível</span><span class="sxs-lookup"><span data-stu-id="5d06c-208">High-level steps toocreate hello solution</span></span>
1. <span data-ttu-id="5d06c-209">Crie uma atividade personalizada que contém a lógica de processamento de dados de Olá.</span><span class="sxs-lookup"><span data-stu-id="5d06c-209">Create a custom activity that contains hello data processing logic.</span></span>
2. <span data-ttu-id="5d06c-210">Crie um Azure data factory que utiliza a atividade personalizada Olá:</span><span class="sxs-lookup"><span data-stu-id="5d06c-210">Create an Azure data factory that uses hello custom activity:</span></span>

### <a name="create-hello-custom-activity"></a><span data-ttu-id="5d06c-211">Criar atividades personalizadas Olá</span><span class="sxs-lookup"><span data-stu-id="5d06c-211">Create hello custom activity</span></span>
<span data-ttu-id="5d06c-212">Olá atividade personalizada da fábrica de dados é heart Olá desta solução de exemplo.</span><span class="sxs-lookup"><span data-stu-id="5d06c-212">hello Data Factory custom activity is hello heart of this sample solution.</span></span> <span data-ttu-id="5d06c-213">solução de exemplo de Olá utiliza a atividade personalizada do Azure Batch toorun Olá.</span><span class="sxs-lookup"><span data-stu-id="5d06c-213">hello sample solution uses Azure Batch toorun hello custom activity.</span></span> <span data-ttu-id="5d06c-214">Consulte [utilizar atividades personalizadas num pipeline do Azure Data Factory](data-factory-use-custom-activities.md) para Olá informações básicas toodevelop atividades e utilize-las no Azure Data Factory pipelines.</span><span class="sxs-lookup"><span data-stu-id="5d06c-214">See [Use custom activities in an Azure Data Factory pipeline](data-factory-use-custom-activities.md) for hello basic information toodevelop custom activities and use them in Azure Data Factory pipelines.</span></span>

<span data-ttu-id="5d06c-215">toocreate uma atividade personalizada do .NET que pode utilizar um pipeline do Azure Data Factory, tem de toocreate um **biblioteca de classe de .NET** projeto com uma classe que implementa que **IDotNetActivity** interface.</span><span class="sxs-lookup"><span data-stu-id="5d06c-215">toocreate a .NET custom activity that you can use in an Azure Data Factory pipeline, you need toocreate a **.NET Class Library** project with a class that implements that **IDotNetActivity** interface.</span></span> <span data-ttu-id="5d06c-216">Esta interface tem apenas um método: **executar**.</span><span class="sxs-lookup"><span data-stu-id="5d06c-216">This interface has only one method: **Execute**.</span></span> <span data-ttu-id="5d06c-217">Segue-se a assinatura do método Olá Olá:</span><span class="sxs-lookup"><span data-stu-id="5d06c-217">Here is hello signature of hello method:</span></span>

```csharp
public IDictionary<string, string> Execute(
            IEnumerable<LinkedService> linkedServices,
            IEnumerable<Dataset> datasets,
            Activity activity,
            IActivityLogger logger)
```

<span data-ttu-id="5d06c-218">o método de Olá tem alguns componentes principais que terá de toounderstand.</span><span class="sxs-lookup"><span data-stu-id="5d06c-218">hello method has a few key components that you need toounderstand.</span></span>

* <span data-ttu-id="5d06c-219">método de Olá aceita quatro parâmetros:</span><span class="sxs-lookup"><span data-stu-id="5d06c-219">hello method takes four parameters:</span></span>

  1. <span data-ttu-id="5d06c-220">**linkedServices**.</span><span class="sxs-lookup"><span data-stu-id="5d06c-220">**linkedServices**.</span></span> <span data-ttu-id="5d06c-221">Uma lista enumeráveis de serviços ligados para ligar a origens de dados de entrada/saída (por exemplo: Blob Storage do Azure) toohello fábrica de dados.</span><span class="sxs-lookup"><span data-stu-id="5d06c-221">An enumerable list of linked services that link input/output data sources (for example: Azure Blob Storage) toohello data factory.</span></span> <span data-ttu-id="5d06c-222">Neste exemplo, não há apenas um serviço ligado do tipo de armazenamento do Azure utilizados para a entrada e saída.</span><span class="sxs-lookup"><span data-stu-id="5d06c-222">In this sample, there is only one linked service of type Azure Storage used for both input and output.</span></span>
  2. <span data-ttu-id="5d06c-223">**conjuntos de dados**.</span><span class="sxs-lookup"><span data-stu-id="5d06c-223">**datasets**.</span></span> <span data-ttu-id="5d06c-224">Esta é uma lista enumeráveis de conjuntos de dados.</span><span class="sxs-lookup"><span data-stu-id="5d06c-224">This is an enumerable list of datasets.</span></span> <span data-ttu-id="5d06c-225">Pode utilizar este localizações do parâmetro tooget Olá e esquemas definidas conjuntos de dados de entrada e de saída.</span><span class="sxs-lookup"><span data-stu-id="5d06c-225">You can use this parameter tooget hello locations and schemas defined by input and output datasets.</span></span>
  3. <span data-ttu-id="5d06c-226">**atividade**.</span><span class="sxs-lookup"><span data-stu-id="5d06c-226">**activity**.</span></span> <span data-ttu-id="5d06c-227">Este parâmetro representa Olá atual computação entidade - neste caso, um serviço Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="5d06c-227">This parameter represents hello current compute entity - in this case, an Azure Batch service.</span></span>
  4. <span data-ttu-id="5d06c-228">**registo**.</span><span class="sxs-lookup"><span data-stu-id="5d06c-228">**logger**.</span></span> <span data-ttu-id="5d06c-229">permite de registo de Olá que escrever comentários de depuração esse superfície como Olá "Utilizador" iniciar sessão para Olá pipeline.</span><span class="sxs-lookup"><span data-stu-id="5d06c-229">hello logger lets you write debug comments that surface as hello “User” log for hello pipeline.</span></span>
* <span data-ttu-id="5d06c-230">método de Olá devolve um dicionário que pode ser utilizados toochain de atividades personalizadas em conjunto no futuro Olá.</span><span class="sxs-lookup"><span data-stu-id="5d06c-230">hello method returns a dictionary that can be used toochain custom activities together in hello future.</span></span> <span data-ttu-id="5d06c-231">Esta funcionalidade ainda não está implementada, por isso, devolver um dicionário vazio do método Olá.</span><span class="sxs-lookup"><span data-stu-id="5d06c-231">This feature is not implemented yet, so return an empty dictionary from hello method.</span></span>

#### <a name="procedure-create-hello-custom-activity"></a><span data-ttu-id="5d06c-232">Procedimento: Criar atividades personalizadas Olá</span><span class="sxs-lookup"><span data-stu-id="5d06c-232">Procedure: Create hello custom activity</span></span>
1. <span data-ttu-id="5d06c-233">Crie um projeto da biblioteca de classe de .NET no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="5d06c-233">Create a .NET Class Library project in Visual Studio.</span></span>

   1. <span data-ttu-id="5d06c-234">Iniciar **Visual Studio 2012**/**2013/2015**.</span><span class="sxs-lookup"><span data-stu-id="5d06c-234">Launch **Visual Studio 2012**/**2013/2015**.</span></span>
   2. <span data-ttu-id="5d06c-235">Clique em **ficheiro**, ponto demasiado**novo**e clique em **projeto**.</span><span class="sxs-lookup"><span data-stu-id="5d06c-235">Click **File**, point too**New**, and click **Project**.</span></span>
   3. <span data-ttu-id="5d06c-236">Expanda **modelos**e selecione **Visual C\#**.</span><span class="sxs-lookup"><span data-stu-id="5d06c-236">Expand **Templates**, and select **Visual C\#**.</span></span> <span data-ttu-id="5d06c-237">Nestas instruções, utilizar o C\#, mas pode utilizar qualquer .NET idioma toodevelop Olá atividade personalizada.</span><span class="sxs-lookup"><span data-stu-id="5d06c-237">In this walkthrough, you use C\#, but you can use any .NET language toodevelop hello custom activity.</span></span>
   4. <span data-ttu-id="5d06c-238">Selecione **biblioteca de classes** da lista de Olá dos tipos de projeto no Olá à direita.</span><span class="sxs-lookup"><span data-stu-id="5d06c-238">Select **Class Library** from hello list of project types on hello right.</span></span>
   5. <span data-ttu-id="5d06c-239">Introduza **MyDotNetActivity** para Olá **nome**.</span><span class="sxs-lookup"><span data-stu-id="5d06c-239">Enter **MyDotNetActivity** for hello **Name**.</span></span>
   6. <span data-ttu-id="5d06c-240">Selecione **c:\\ADF** para Olá **localização**.</span><span class="sxs-lookup"><span data-stu-id="5d06c-240">Select **C:\\ADF** for hello **Location**.</span></span> <span data-ttu-id="5d06c-241">Criar a pasta de Olá **ADF** se não existir.</span><span class="sxs-lookup"><span data-stu-id="5d06c-241">Create hello folder **ADF** if it does not exist.</span></span>
   7. <span data-ttu-id="5d06c-242">Clique em **OK** projeto de Olá toocreate.</span><span class="sxs-lookup"><span data-stu-id="5d06c-242">Click **OK** toocreate hello project.</span></span>
2. <span data-ttu-id="5d06c-243">Clique em **ferramentas**, ponto demasiado**Gestor de pacotes NuGet**e clique em **consola do Gestor de pacotes**.</span><span class="sxs-lookup"><span data-stu-id="5d06c-243">Click **Tools**, point too**NuGet Package Manager**, and click **Package Manager Console**.</span></span>
3. <span data-ttu-id="5d06c-244">No Olá **consola do Gestor de pacotes**, executar Olá os seguintes comandos tooimport **Microsoft.Azure.Management.DataFactories**.</span><span class="sxs-lookup"><span data-stu-id="5d06c-244">In hello **Package Manager Console**, execute hello following command tooimport **Microsoft.Azure.Management.DataFactories**.</span></span>

    ```powershell
    Install-Package Microsoft.Azure.Management.DataFactories
    ```
4. <span data-ttu-id="5d06c-245">Olá importação **Storage do Azure** pacote NuGet no projeto toohello.</span><span class="sxs-lookup"><span data-stu-id="5d06c-245">Import hello **Azure Storage** NuGet package in toohello project.</span></span> <span data-ttu-id="5d06c-246">Este pacote tem porque utiliza a API de armazenamento de BLOBs de Olá neste exemplo.</span><span class="sxs-lookup"><span data-stu-id="5d06c-246">You need this package because you use hello Blob storage API in this sample.</span></span>

    ```powershell
    Install-Package Azure.Storage
    ```
5. <span data-ttu-id="5d06c-247">Adicione Olá seguinte **utilizando** ficheiro de origem toohello diretivas no projeto Olá.</span><span class="sxs-lookup"><span data-stu-id="5d06c-247">Add hello following **using** directives toohello source file in hello project.</span></span>

    ```csharp
    using System.IO;
    using System.Globalization;
    using System.Diagnostics;
    using System.Linq;
    
    using Microsoft.Azure.Management.DataFactories.Models;
    using Microsoft.Azure.Management.DataFactories.Runtime;
    
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Blob;
    ```
6. <span data-ttu-id="5d06c-248">Nome de Olá de alteração de Olá **espaço de nomes** demasiado**MyDotNetActivityNS**.</span><span class="sxs-lookup"><span data-stu-id="5d06c-248">Change hello name of hello **namespace** too**MyDotNetActivityNS**.</span></span>

    ```csharp
    namespace MyDotNetActivityNS
    ```
7. <span data-ttu-id="5d06c-249">Alterar o nome de Olá da classe de Olá demasiado**MyDotNetActivity** e derivar-Olá **IDotNetActivity** interface conforme mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="5d06c-249">Change hello name of hello class too**MyDotNetActivity** and derive it from hello **IDotNetActivity** interface as shown below.</span></span>

    ```csharp
    public class MyDotNetActivity : IDotNetActivity
    ```
8. <span data-ttu-id="5d06c-250">Olá implementar (adicionar) **executar** método de Olá **IDotNetActivity** interface toohello **MyDotNetActivity** Olá classe e copie o método de toohello do código de exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="5d06c-250">Implement (Add) hello **Execute** method of hello **IDotNetActivity** interface toohello **MyDotNetActivity** class and copy hello following sample code toohello method.</span></span> <span data-ttu-id="5d06c-251">Consulte Olá [executar o método](#execute-method) secção para obter explicações para a lógica de Olá utilizada este método.</span><span class="sxs-lookup"><span data-stu-id="5d06c-251">See hello [Execute Method](#execute-method) section for explanation for hello logic used in this method.</span></span>

    ```csharp
    /// <summary>
    /// Execute method is hello only method of IDotNetActivity interface you must implement.
    /// In this sample, hello method invokes hello Calculate method tooperform hello core logic.  
    /// </summary>
    public IDictionary<string, string> Execute(
       IEnumerable<LinkedService> linkedServices,
       IEnumerable<Dataset> datasets,
       Activity activity,
       IActivityLogger logger)
    {
    
       // declare types for input and output data stores
       AzureStorageLinkedService inputLinkedService;
    
       Dataset inputDataset = datasets.Single(dataset => dataset.Name == activity.Inputs.Single().Name);
    
       foreach (LinkedService ls in linkedServices)
           logger.Write("linkedService.Name {0}", ls.Name);
    
       // using First method instead of Single since we are using hello same
       // Azure Storage linked service for input and output.
       inputLinkedService = linkedServices.First(
           linkedService =>
           linkedService.Name ==
           inputDataset.Properties.LinkedServiceName).Properties.TypeProperties
           as AzureStorageLinkedService;
    
       string connectionString = inputLinkedService.ConnectionString; // toocreate an input storage client.
       string folderPath = GetFolderPath(inputDataset);
       string output = string.Empty; // for use later.
    
       // create storage client for input. Pass hello connection string.
       CloudStorageAccount inputStorageAccount = CloudStorageAccount.Parse(connectionString);
       CloudBlobClient inputClient = inputStorageAccount.CreateCloudBlobClient();
    
       // initialize hello continuation token before using it in hello do-while loop.
       BlobContinuationToken continuationToken = null;
       do
       {   // get hello list of input blobs from hello input storage client object.
           BlobResultSegment blobList = inputClient.ListBlobsSegmented(folderPath,
                                    true,
                                    BlobListingDetails.Metadata,
                                    null,
                                    continuationToken,
                                    null,
                                    null);
    
           // Calculate method returns hello number of occurrences of
           // hello search term (“Microsoft”) in each blob associated
           // with hello data slice.
           //
           // definition of hello method is shown in hello next step.
           output = Calculate(blobList, logger, folderPath, ref continuationToken, "Microsoft");
    
       } while (continuationToken != null);
    
       // get hello output dataset using hello name of hello dataset matched tooa name in hello Activity output collection.
       Dataset outputDataset = datasets.Single(dataset => dataset.Name == activity.Outputs.Single().Name);
    
       folderPath = GetFolderPath(outputDataset);
    
       logger.Write("Writing blob toohello folder: {0}", folderPath);
    
       // create a storage object for hello output blob.
       CloudStorageAccount outputStorageAccount = CloudStorageAccount.Parse(connectionString);
       // write hello name of hello file.
       Uri outputBlobUri = new Uri(outputStorageAccount.BlobEndpoint, folderPath + "/" + GetFileName(outputDataset));
    
       logger.Write("output blob URI: {0}", outputBlobUri.ToString());
       // create a blob and upload hello output text.
       CloudBlockBlob outputBlob = new CloudBlockBlob(outputBlobUri, outputStorageAccount.Credentials);
       logger.Write("Writing {0} toohello output blob", output);
       outputBlob.UploadText(output);
    
       // hello dictionary can be used toochain custom activities together in hello future.
       // This feature is not implemented yet, so just return an empty dictionary.
       return new Dictionary<string, string>();
    }
    ```
9. <span data-ttu-id="5d06c-252">Adicione a seguinte classe de toohello de métodos de programa auxiliar de Olá.</span><span class="sxs-lookup"><span data-stu-id="5d06c-252">Add hello following helper methods toohello class.</span></span> <span data-ttu-id="5d06c-253">Estes métodos são invocados pelo Olá **executar** método.</span><span class="sxs-lookup"><span data-stu-id="5d06c-253">These methods are invoked by hello **Execute** method.</span></span> <span data-ttu-id="5d06c-254">Mais importante ainda, Olá **Calculate** método isola código Olá itera através de cada blob.</span><span class="sxs-lookup"><span data-stu-id="5d06c-254">Most importantly, hello **Calculate** method isolates hello code that iterates through each blob.</span></span>

    ```csharp
    /// <summary>
    /// Gets hello folderPath value from hello input/output dataset.
    /// </summary>
    private static string GetFolderPath(Dataset dataArtifact)
    {
       if (dataArtifact == null || dataArtifact.Properties == null)
       {
           return null;
       }
    
       AzureBlobDataset blobDataset = dataArtifact.Properties.TypeProperties as AzureBlobDataset;
       if (blobDataset == null)
       {
           return null;
       }
    
       return blobDataset.FolderPath;
    }
    
    /// <summary>
    /// Gets hello fileName value from hello input/output dataset.
    /// </summary>
    
    private static string GetFileName(Dataset dataArtifact)
    {
       if (dataArtifact == null || dataArtifact.Properties == null)
       {
           return null;
       }
    
       AzureBlobDataset blobDataset = dataArtifact.Properties.TypeProperties as AzureBlobDataset;
       if (blobDataset == null)
       {
           return null;
       }
    
       return blobDataset.FileName;
    }
    
    /// <summary>
    /// Iterates through each blob (file) in hello folder, counts hello number of instances of search term in hello file,
    /// and prepares hello output text that is written toohello output blob.
    /// </summary>
    
    public static string Calculate(BlobResultSegment Bresult, IActivityLogger logger, string folderPath, ref BlobContinuationToken token, string searchTerm)
    {
       string output = string.Empty;
       logger.Write("number of blobs found: {0}", Bresult.Results.Count<IListBlobItem>());
       foreach (IListBlobItem listBlobItem in Bresult.Results)
       {
           CloudBlockBlob inputBlob = listBlobItem as CloudBlockBlob;
           if ((inputBlob != null) && (inputBlob.Name.IndexOf("$$$.$$$") == -1))
           {
               string blobText = inputBlob.DownloadText(Encoding.ASCII, null, null, null);
               logger.Write("input blob text: {0}", blobText);
               string[] source = blobText.Split(new char[] { '.', '?', '!', ' ', ';', ':', ',' }, StringSplitOptions.RemoveEmptyEntries);
               var matchQuery = from word in source
                                where word.ToLowerInvariant() == searchTerm.ToLowerInvariant()
                                select word;
               int wordCount = matchQuery.Count();
               output += string.Format("{0} occurrences(s) of hello search term \"{1}\" were found in hello file {2}.\r\n", wordCount, searchTerm, inputBlob.Name);
           }
       }
       return output;
    }
    ```
    <span data-ttu-id="5d06c-255">Olá **GetFolderPath** método devolve pasta do Olá caminho toohello esse Olá de tooand de pontos de conjunto de dados de Olá **GetFileName** método devolve o nome de Olá de Olá/ficheiro blob que Olá pontos de conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="5d06c-255">hello **GetFolderPath** method returns hello path toohello folder that hello dataset points tooand hello **GetFileName** method returns hello name of hello blob/file that hello dataset points to.</span></span>

    ```csharp

    "name": "InputDataset",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "fileName": "file.txt",
            "folderPath": "mycontainer/inputfolder/{Year}-{Month}-{Day}-{Hour}",
    ```

    <span data-ttu-id="5d06c-256">Olá **Calculate** método calcula o número de Olá de instâncias de palavra-chave **Microsoft** no Olá os ficheiros de entrada (blobs na pasta Olá).</span><span class="sxs-lookup"><span data-stu-id="5d06c-256">hello **Calculate** method calculates hello number of instances of keyword **Microsoft** in hello input files (blobs in hello folder).</span></span> <span data-ttu-id="5d06c-257">o termo de pesquisa de Olá ("Microsoft") é "hard-coded" no código Olá.</span><span class="sxs-lookup"><span data-stu-id="5d06c-257">hello search term (“Microsoft”) is hard-coded in hello code.</span></span>

1. <span data-ttu-id="5d06c-258">Compile o projeto de Olá.</span><span class="sxs-lookup"><span data-stu-id="5d06c-258">Compile hello project.</span></span> <span data-ttu-id="5d06c-259">Clique em **criar** no menu de Olá e clique em **compilar solução**.</span><span class="sxs-lookup"><span data-stu-id="5d06c-259">Click **Build** from hello menu and click **Build Solution**.</span></span>
2. <span data-ttu-id="5d06c-260">Iniciar **Explorador do Windows**e navegue demasiado**bin\\depurar** ou **bin\\versão** pasta, dependendo do tipo de Olá de compilação.</span><span class="sxs-lookup"><span data-stu-id="5d06c-260">Launch **Windows Explorer**, and navigate too**bin\\debug** or **bin\\release** folder depending on hello type of build.</span></span>
3. <span data-ttu-id="5d06c-261">Criar um ficheiro zip **MyDotNetActivity.zip** que contém todos os binários de Olá no Olá  **\\bin\\depurar** pasta.</span><span class="sxs-lookup"><span data-stu-id="5d06c-261">Create a zip file **MyDotNetActivity.zip** that contains all hello binaries in hello **\\bin\\Debug** folder.</span></span> <span data-ttu-id="5d06c-262">Poderá pretender tooinclude Olá MyDotNetActivity. **pdb** para que obtenha detalhes adicionais, tais como o número de linha no código fonte Olá que causou o problema de Olá quando ocorre uma falha de ficheiros.</span><span class="sxs-lookup"><span data-stu-id="5d06c-262">You may want tooinclude hello MyDotNetActivity.**pdb** file so that you get additional details such as line number in hello source code that caused hello issue when a failure occurs.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image5.png)
4. <span data-ttu-id="5d06c-263">Carregar **MyDotNetActivity.zip** como um contentor de blob do blob toohello: `customactivitycontainer` no Olá Azure armazenamento de BLOBs que Olá **StorageLinkedService** serviço no Olá ligado  **ADFTutorialDataFactory** utiliza.</span><span class="sxs-lookup"><span data-stu-id="5d06c-263">Upload **MyDotNetActivity.zip** as a blob toohello blob container: `customactivitycontainer` in hello Azure blob storage that hello **StorageLinkedService** linked service in hello **ADFTutorialDataFactory** uses.</span></span> <span data-ttu-id="5d06c-264">Criar contentor de blob Olá `customactivitycontainer` se já existir.</span><span class="sxs-lookup"><span data-stu-id="5d06c-264">Create hello blob container `customactivitycontainer` if it does not already exist.</span></span>

#### <a name="execute-method"></a><span data-ttu-id="5d06c-265">Executar o método</span><span class="sxs-lookup"><span data-stu-id="5d06c-265">Execute method</span></span>
<span data-ttu-id="5d06c-266">Esta secção fornece mais detalhes e notas sobre o código de Olá no Olá método de execução.</span><span class="sxs-lookup"><span data-stu-id="5d06c-266">This section provides more details and notes about hello code in hello Execute method.</span></span>

1. <span data-ttu-id="5d06c-267">os membros de Olá para repetir a coleção de entrada Olá encontram Olá [Microsoft.WindowsAzure.Storage.Blob](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.aspx) espaço de nomes.</span><span class="sxs-lookup"><span data-stu-id="5d06c-267">hello members for iterating through hello input collection are found in hello [Microsoft.WindowsAzure.Storage.Blob](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.aspx) namespace.</span></span> <span data-ttu-id="5d06c-268">Repetir a coleção de blob Olá requer a utilização Olá **BlobContinuationToken** classe.</span><span class="sxs-lookup"><span data-stu-id="5d06c-268">Iterating through hello blob collection requires using hello **BlobContinuationToken** class.</span></span> <span data-ttu-id="5d06c-269">Essencialmente, tem de utilizar um efetue-ao ciclo com token Olá como mecanismo de Olá para sair do ciclo de Olá.</span><span class="sxs-lookup"><span data-stu-id="5d06c-269">In essence, you must use a do-while loop with hello token as hello mechanism for exiting hello loop.</span></span> <span data-ttu-id="5d06c-270">Para obter mais informações, consulte [como toouse Blob storage do .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="5d06c-270">For more information, see [How toouse Blob storage from .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span> <span data-ttu-id="5d06c-271">Um ciclo básico é mostrado aqui:</span><span class="sxs-lookup"><span data-stu-id="5d06c-271">A basic loop is shown here:</span></span>

    ```csharp
    // Initialize hello continuation token.
    BlobContinuationToken continuationToken = null;
    do
    {
    // Get hello list of input blobs from hello input storage client object.
    BlobResultSegment blobList = inputClient.ListBlobsSegmented(folderPath,
    
                         true,
                                   BlobListingDetails.Metadata,
                                   null,
                                   continuationToken,
                                   null,
                                   null);
    // Return a string derived from parsing each blob.
    
     output = Calculate(blobList, logger, folderPath, ref continuationToken, "Microsoft");
    
    } while (continuationToken != null);

    ```
   <span data-ttu-id="5d06c-272">Consulte a documentação de Olá para Olá [ListBlobsSegmented](https://msdn.microsoft.com/library/jj717596.aspx) método para obter mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="5d06c-272">See hello documentation for hello [ListBlobsSegmented](https://msdn.microsoft.com/library/jj717596.aspx) method for details.</span></span>
2. <span data-ttu-id="5d06c-273">Olá código para funcionar através de conjunto de Olá de blobs logicamente fica dentro Olá fazer-ao ciclo.</span><span class="sxs-lookup"><span data-stu-id="5d06c-273">hello code for working through hello set of blobs logically goes within hello do-while loop.</span></span> <span data-ttu-id="5d06c-274">No Olá **executar** método, efetue de Olá-enquanto ciclo transmite lista Olá de blobs com o nome de método de tooa **Calculate**.</span><span class="sxs-lookup"><span data-stu-id="5d06c-274">In hello **Execute** method, hello do-while loop passes hello list of blobs tooa method named **Calculate**.</span></span> <span data-ttu-id="5d06c-275">método de Olá devolve uma variável de cadeia denominada **saída** que Olá resultado ter iterated através de todos os blobs Olá no segmento Olá.</span><span class="sxs-lookup"><span data-stu-id="5d06c-275">hello method returns a string variable named **output** that is hello result of having iterated through all hello blobs in hello segment.</span></span>

   <span data-ttu-id="5d06c-276">-Devolve o número de Olá de ocorrências do termo de pesquisa de Olá (**Microsoft**) num blob Olá transmitido toohello **Calculate** método.</span><span class="sxs-lookup"><span data-stu-id="5d06c-276">It returns hello number of occurrences of hello search term (**Microsoft**) in hello blob passed toohello **Calculate** method.</span></span>

    ```csharp
    output += string.Format("{0} occurrences of hello search term \"{1}\" were found in hello file {2}.\r\n", wordCount, searchTerm, inputBlob.Name);
    ```
3. <span data-ttu-id="5d06c-277">Uma vez Olá **Calculate** método tem de terminar o trabalho de Olá, têm de ser escrito tooa blob de novo.</span><span class="sxs-lookup"><span data-stu-id="5d06c-277">Once hello **Calculate** method has done hello work, it must be written tooa new blob.</span></span> <span data-ttu-id="5d06c-278">Por isso, para cada conjunto de blobs processados, um novo blob pode ser escrito com resultados de Olá.</span><span class="sxs-lookup"><span data-stu-id="5d06c-278">So for every set of blobs processed, a new blob can be written with hello results.</span></span> <span data-ttu-id="5d06c-279">toowrite tooa novos BLOBs, primeiro localizar o Olá saída dataset.</span><span class="sxs-lookup"><span data-stu-id="5d06c-279">toowrite tooa new blob, first find hello output dataset.</span></span>

    ```csharp
    // Get hello output dataset using hello name of hello dataset matched tooa name in hello Activity output collection.
    Dataset outputDataset = datasets.Single(dataset => dataset.Name == activity.Outputs.Single().Name);
    ```
4. <span data-ttu-id="5d06c-280">Olá também chama um método de programa auxiliar: **GetFolderPath** caminho da pasta tooretrieve Olá (nome do contentor de armazenamento de Olá).</span><span class="sxs-lookup"><span data-stu-id="5d06c-280">hello code also calls a helper method: **GetFolderPath** tooretrieve hello folder path (hello storage container name).</span></span>

    ```csharp
    folderPath = GetFolderPath(outputDataset);
    ```
   <span data-ttu-id="5d06c-281">Olá **GetFolderPath** casts Olá tooan de objeto do conjunto de dados AzureBlobDataSet, que tem uma propriedade chamada FolderPath.</span><span class="sxs-lookup"><span data-stu-id="5d06c-281">hello **GetFolderPath** casts hello DataSet object tooan AzureBlobDataSet, which has a property named FolderPath.</span></span>

    ```csharp
    AzureBlobDataset blobDataset = dataArtifact.Properties.TypeProperties as AzureBlobDataset;
    
    return blobDataset.FolderPath;
    ```
5. <span data-ttu-id="5d06c-282">Olá código chamadas Olá **GetFileName** nome do ficheiro do método tooretrieve Olá (nome do blob).</span><span class="sxs-lookup"><span data-stu-id="5d06c-282">hello code calls hello **GetFileName** method tooretrieve hello file name (blob name).</span></span> <span data-ttu-id="5d06c-283">código de Olá é semelhante toohello acima caminho da pasta do código tooget Olá.</span><span class="sxs-lookup"><span data-stu-id="5d06c-283">hello code is similar toohello above code tooget hello folder path.</span></span>

    ```csharp
    AzureBlobDataset blobDataset = dataArtifact.Properties.TypeProperties as AzureBlobDataset;
    
    return blobDataset.FileName;
    ```
6. <span data-ttu-id="5d06c-284">Olá o nome do ficheiro de Olá é escrito através da criação de um objeto URI.</span><span class="sxs-lookup"><span data-stu-id="5d06c-284">hello name of hello file is written by creating a URI object.</span></span> <span data-ttu-id="5d06c-285">o construtor URI Olá utiliza Olá **BlobEndpoint** nome da propriedade tooreturn Olá contentor.</span><span class="sxs-lookup"><span data-stu-id="5d06c-285">hello URI constructor uses hello **BlobEndpoint** property tooreturn hello container name.</span></span> <span data-ttu-id="5d06c-286">nome de ficheiro e caminho da pasta Olá são adicionados URI de blob tooconstruct Olá saída.</span><span class="sxs-lookup"><span data-stu-id="5d06c-286">hello folder path and file name are added tooconstruct hello output blob URI.</span></span>  

    ```csharp
    // Write hello name of hello file.
    Uri outputBlobUri = new Uri(outputStorageAccount.BlobEndpoint, folderPath + "/" + GetFileName(outputDataset));
    ```
7. <span data-ttu-id="5d06c-287">nome de Olá do ficheiro de Olá foi escrito e agora pode escrever Olá cadeia da saída de Olá **Calculate** blob novo do método tooa:</span><span class="sxs-lookup"><span data-stu-id="5d06c-287">hello name of hello file has been written and now you can write hello output string from hello **Calculate** method tooa new blob:</span></span>

    ```csharp
    // Create a blob and upload hello output text.
    CloudBlockBlob outputBlob = new CloudBlockBlob(outputBlobUri, outputStorageAccount.Credentials);
    logger.Write("Writing {0} toohello output blob", output);
    outputBlob.UploadText(output);
    ```

### <a name="create-hello-data-factory"></a><span data-ttu-id="5d06c-288">Criar fábrica de dados de Olá</span><span class="sxs-lookup"><span data-stu-id="5d06c-288">Create hello data factory</span></span>
<span data-ttu-id="5d06c-289">No Olá [criar atividades personalizadas Olá](#create-the-custom-activity) secção, criou uma atividade personalizada e o ficheiro zip Olá carregado com os binários e Olá PDB ficheiros tooan contentor de Blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="5d06c-289">In hello [Create hello custom activity](#create-the-custom-activity) section, you created a custom activity and uploaded hello zip file with binaries and hello PDB file tooan Azure blob container.</span></span> <span data-ttu-id="5d06c-290">Nesta secção, vai criar um Azure **fábrica de dados** com um **pipeline** que utiliza Olá **atividade personalizada**.</span><span class="sxs-lookup"><span data-stu-id="5d06c-290">In this section, you create an Azure **data factory** with a **pipeline** that uses hello **custom activity**.</span></span>

<span data-ttu-id="5d06c-291">Olá o conjunto de dados de entrada para a atividade personalizada Olá representa blobs Olá (ficheiros) na pasta de entrada Olá (`mycontainer\\inputfolder`) no armazenamento de Blobs.</span><span class="sxs-lookup"><span data-stu-id="5d06c-291">hello input dataset for hello custom activity represents hello blobs (files) in hello input folder (`mycontainer\\inputfolder`) in blob storage.</span></span> <span data-ttu-id="5d06c-292">Olá conjunto de dados de saída para a atividade de Olá representa Olá saída blobs na pasta de saída Olá (`mycontainer\\outputfolder`) no armazenamento de Blobs.</span><span class="sxs-lookup"><span data-stu-id="5d06c-292">hello output dataset for hello activity represents hello output blobs in hello output folder (`mycontainer\\outputfolder`) in blob storage.</span></span>

<span data-ttu-id="5d06c-293">Remova um ou mais ficheiros em pastas de entrada Olá:</span><span class="sxs-lookup"><span data-stu-id="5d06c-293">Drop one or more files in hello input folders:</span></span>

```
mycontainer -\> inputfolder
    2015-11-16-00
    2015-11-16-01
    2015-11-16-02
    2015-11-16-03
    2015-11-16-04
```

<span data-ttu-id="5d06c-294">Por exemplo, remova um ficheiro (file.txt) com Olá seguir o conteúdo para cada uma das pastas de Olá.</span><span class="sxs-lookup"><span data-stu-id="5d06c-294">For example, drop one file (file.txt) with hello following content into each of hello folders.</span></span>

```
test custom activity Microsoft test custom activity Microsoft
```

<span data-ttu-id="5d06c-295">Cada pasta de entrada corresponde setor tooa no Azure Data Factory, mesmo se tiver de pasta Olá 2 ou mais ficheiros.</span><span class="sxs-lookup"><span data-stu-id="5d06c-295">Each input folder corresponds tooa slice in Azure Data Factory even if hello folder has 2 or more files.</span></span> <span data-ttu-id="5d06c-296">Quando cada setor é processado pelo pipeline Olá, atividade personalizada Olá itera através de todos os blobs Olá na pasta de entrada Olá para esse setor.</span><span class="sxs-lookup"><span data-stu-id="5d06c-296">When each slice is processed by hello pipeline, hello custom activity iterates through all hello blobs in hello input folder for that slice.</span></span>

<span data-ttu-id="5d06c-297">Consulte a saída cinco ficheiros com Olá mesmo conteúdo.</span><span class="sxs-lookup"><span data-stu-id="5d06c-297">You see five output files with hello same content.</span></span> <span data-ttu-id="5d06c-298">Por exemplo, o ficheiro de saída de Olá de processar o ficheiro de Olá na pasta de Olá 2015-11-16-00 tem Olá seguinte conteúdo:</span><span class="sxs-lookup"><span data-stu-id="5d06c-298">For example, hello output file from processing hello file in hello 2015-11-16-00 folder has hello following content:</span></span>

```
2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-00/file.txt.
```

<span data-ttu-id="5d06c-299">Se remover vários ficheiros (file.txt file2.txt, file3.txt) com Olá de pasta de entrada toohello mesmo conteúdo, consulte Olá seguir o conteúdo no ficheiro de saída Olá.</span><span class="sxs-lookup"><span data-stu-id="5d06c-299">If you drop multiple files (file.txt, file2.txt, file3.txt) with hello same content toohello input folder, you see hello following content in hello output file.</span></span> <span data-ttu-id="5d06c-300">Cada pasta (2015-11-16-00, etc.) corresponde tooa setor neste exemplo, apesar de pasta de Olá tem vários ficheiros de entrada.</span><span class="sxs-lookup"><span data-stu-id="5d06c-300">Each folder (2015-11-16-00, etc.) corresponds tooa slice in this sample even though hello folder has multiple input files.</span></span>

```csharp
2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-00/file.txt.
2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-00/file2.txt.
2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-00/file3.txt.
```

<span data-ttu-id="5d06c-301">ficheiro de saída de Olá tem três linhas agora, um para cada ficheiro de entrada (blob) na pasta Olá associado setor Olá (2015-11-16-00).</span><span class="sxs-lookup"><span data-stu-id="5d06c-301">hello output file has three lines now, one for each input file (blob) in hello folder associated with hello slice (2015-11-16-00).</span></span>

<span data-ttu-id="5d06c-302">Uma tarefa é criada para cada execução da atividade.</span><span class="sxs-lookup"><span data-stu-id="5d06c-302">A task is created for each activity run.</span></span> <span data-ttu-id="5d06c-303">Neste exemplo, não há apenas uma atividade no pipeline de Olá.</span><span class="sxs-lookup"><span data-stu-id="5d06c-303">In this sample, there is only one activity in hello pipeline.</span></span> <span data-ttu-id="5d06c-304">Quando um setor é processado pelo pipeline Olá, atividade personalizada Olá é executado no setor da Olá tooprocess do Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="5d06c-304">When a slice is processed by hello pipeline, hello custom activity runs on Azure Batch tooprocess hello slice.</span></span> <span data-ttu-id="5d06c-305">Uma vez que existem cinco setores (cada setor pode ter vários blobs ou ficheiro), existem cinco tarefas criadas no Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="5d06c-305">Since there are five slices (each slice can have multiple blobs or file), there are five tasks created in Azure Batch.</span></span> <span data-ttu-id="5d06c-306">Quando é executada uma tarefa do batch, está efetivamente Olá atividade personalizada que está em execução.</span><span class="sxs-lookup"><span data-stu-id="5d06c-306">When a task runs on Batch, it is actually hello custom activity that is running.</span></span>

<span data-ttu-id="5d06c-307">Olá instruções a seguir fornece detalhes adicionais.</span><span class="sxs-lookup"><span data-stu-id="5d06c-307">hello following walkthrough provides additional details.</span></span>

#### <a name="step-1-create-hello-data-factory"></a><span data-ttu-id="5d06c-308">Passo 1: Criar a fábrica de dados de Olá</span><span class="sxs-lookup"><span data-stu-id="5d06c-308">Step 1: Create hello data factory</span></span>
1. <span data-ttu-id="5d06c-309">Após iniciar sessão toohello [portal do Azure](https://portal.azure.com/), Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="5d06c-309">After logging in toohello [Azure portal](https://portal.azure.com/), do hello following steps:</span></span>

   1. <span data-ttu-id="5d06c-310">Clique em **novo** no menu à esquerda Olá.</span><span class="sxs-lookup"><span data-stu-id="5d06c-310">Click **NEW** on hello left menu.</span></span>
   2. <span data-ttu-id="5d06c-311">Clique em **dados + análise** no Olá **novo** painel.</span><span class="sxs-lookup"><span data-stu-id="5d06c-311">Click **Data + Analytics** in hello **New** blade.</span></span>
   3. <span data-ttu-id="5d06c-312">Clique em **Data Factory** no Olá **análise de dados** painel.</span><span class="sxs-lookup"><span data-stu-id="5d06c-312">Click **Data Factory** on hello **Data analytics** blade.</span></span>
2. <span data-ttu-id="5d06c-313">No Olá **nova fábrica de dados** painel, introduza **CustomActivityFactory** para Olá nome.</span><span class="sxs-lookup"><span data-stu-id="5d06c-313">In hello **New data factory** blade, enter **CustomActivityFactory** for hello Name.</span></span> <span data-ttu-id="5d06c-314">nome de Olá do Olá do Azure data factory deve ser globalmente exclusivo.</span><span class="sxs-lookup"><span data-stu-id="5d06c-314">hello name of hello Azure data factory must be globally unique.</span></span> <span data-ttu-id="5d06c-315">Se receber o erro de Olá: **nome da fábrica de dados "CustomActivityFactory" não está disponível**, altere Olá nome da fábrica de dados de Olá (por exemplo, **yournameCustomActivityFactory**) e tente criar novamente.</span><span class="sxs-lookup"><span data-stu-id="5d06c-315">If you receive hello error: **Data factory name “CustomActivityFactory” is not available**, change hello name of hello data factory (for example, **yournameCustomActivityFactory**) and try creating again.</span></span>
3. <span data-ttu-id="5d06c-316">Clique em **nome do grupo de recursos**e selecione um grupo de recursos existente ou crie um grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="5d06c-316">Click **RESOURCE GROUP NAME**, and select an existing resource group or create a resource group.</span></span>
4. <span data-ttu-id="5d06c-317">Certifique-se de que está a utilizar a subscrição correta Olá e região onde pretende toobe de fábrica de dados de Olá criado.</span><span class="sxs-lookup"><span data-stu-id="5d06c-317">Verify that you are using hello correct subscription and region where you want hello data factory toobe created.</span></span>
5. <span data-ttu-id="5d06c-318">Clique em **criar** no Olá **nova fábrica de dados** painel.</span><span class="sxs-lookup"><span data-stu-id="5d06c-318">Click **Create** on hello **New data factory** blade.</span></span>
6. <span data-ttu-id="5d06c-319">Consulte a fábrica de dados de Olá a ser criada no Olá **Dashboard** de Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="5d06c-319">You see hello data factory being created in hello **Dashboard** of hello Azure portal.</span></span>
7. <span data-ttu-id="5d06c-320">Depois de Olá a fábrica de dados foi criada com êxito, será apresentada a página de fábrica do Olá dados, que mostra-lhe Olá conteúdos da fábrica de dados de Olá.</span><span class="sxs-lookup"><span data-stu-id="5d06c-320">After hello data factory has been created successfully, you see hello data factory page, which shows you hello contents of hello data factory.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image6.png)

#### <a name="step-2-create-linked-services"></a><span data-ttu-id="5d06c-321">Passo 2: Criar serviços ligados</span><span class="sxs-lookup"><span data-stu-id="5d06c-321">Step 2: Create linked services</span></span>
<span data-ttu-id="5d06c-322">Os serviços ligados ligam os arquivos de dados ou fábrica de dados do Azure tooan de serviços de computação.</span><span class="sxs-lookup"><span data-stu-id="5d06c-322">Linked services link data stores or compute services tooan Azure data factory.</span></span> <span data-ttu-id="5d06c-323">Neste passo, ligue o **Storage do Azure** conta e **do Azure Batch** fábrica de dados de tooyour de conta.</span><span class="sxs-lookup"><span data-stu-id="5d06c-323">In this step, you link your **Azure Storage** account and **Azure Batch** account tooyour data factory.</span></span>

#### <a name="create-azure-storage-linked-service"></a><span data-ttu-id="5d06c-324">Criar o serviço ligado do Storage do Azure</span><span class="sxs-lookup"><span data-stu-id="5d06c-324">Create Azure Storage linked service</span></span>
1. <span data-ttu-id="5d06c-325">Clique em Olá **autor e implementar** mosaico Olá **DATA FACTORY** painel **CustomActivityFactory**.</span><span class="sxs-lookup"><span data-stu-id="5d06c-325">Click hello **Author and deploy** tile on hello **DATA FACTORY** blade for **CustomActivityFactory**.</span></span> <span data-ttu-id="5d06c-326">Consulte Olá Editor do Data Factory.</span><span class="sxs-lookup"><span data-stu-id="5d06c-326">You see hello Data Factory Editor.</span></span>
2. <span data-ttu-id="5d06c-327">Clique em **novo arquivo de dados** na barra de comando de Olá e escolha **storage do Azure.**</span><span class="sxs-lookup"><span data-stu-id="5d06c-327">Click **New data store** on hello command bar and choose **Azure storage.**</span></span> <span data-ttu-id="5d06c-328">Deverá ver Olá script JSON para criar um Storage do Azure ligado serviço num editor de Olá.</span><span class="sxs-lookup"><span data-stu-id="5d06c-328">You should see hello JSON script for creating an Azure Storage linked service in hello editor.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image7.png)

3. <span data-ttu-id="5d06c-329">Substitua **nome da conta** com o nome de Olá da sua conta de armazenamento do Azure e **chave da conta** com a chave de acesso de Olá de Olá conta do storage do Azure.</span><span class="sxs-lookup"><span data-stu-id="5d06c-329">Replace **account name** with hello name of your Azure storage account and **account key** with hello access key of hello Azure storage account.</span></span> <span data-ttu-id="5d06c-330">toolearn como tooget seu armazenamento aceder à chave, consulte [chaves de acesso de ver, copiar e voltar a gerar armazenamento](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span><span class="sxs-lookup"><span data-stu-id="5d06c-330">toolearn how tooget your storage access key, see [View, copy and regenerate storage access keys](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span>

4. <span data-ttu-id="5d06c-331">Clique em **implementar** no comando Olá barra toodeploy Olá ligado serviço.</span><span class="sxs-lookup"><span data-stu-id="5d06c-331">Click **Deploy** on hello command bar toodeploy hello linked service.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image8.png)

#### <a name="create-azure-batch-linked-service"></a><span data-ttu-id="5d06c-332">Criar o serviço ligado do Azure Batch</span><span class="sxs-lookup"><span data-stu-id="5d06c-332">Create Azure Batch linked service</span></span>
<span data-ttu-id="5d06c-333">Neste passo, vai criar um serviço ligado para sua **do Azure Batch** conta que seja utilizado toorun fábrica de dados de Olá atividade personalizada.</span><span class="sxs-lookup"><span data-stu-id="5d06c-333">In this step, you create a linked service for your **Azure Batch** account that is used toorun hello Data Factory custom activity.</span></span>

1. <span data-ttu-id="5d06c-334">Clique em **nova computação** na barra de comando de Olá e escolha **do Azure Batch.**</span><span class="sxs-lookup"><span data-stu-id="5d06c-334">Click **New compute** on hello command bar and choose **Azure Batch.**</span></span> <span data-ttu-id="5d06c-335">Deverá ver Olá script JSON para criar um Azure Batch ligado serviço num editor de Olá.</span><span class="sxs-lookup"><span data-stu-id="5d06c-335">You should see hello JSON script for creating an Azure Batch linked service in hello editor.</span></span>
2. <span data-ttu-id="5d06c-336">No Olá script JSON:</span><span class="sxs-lookup"><span data-stu-id="5d06c-336">In hello JSON script:</span></span>

   1. <span data-ttu-id="5d06c-337">Substitua **nome da conta** com o nome de Olá da sua conta do Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="5d06c-337">Replace **account name** with hello name of your Azure Batch account.</span></span>
   2. <span data-ttu-id="5d06c-338">Substitua **chave de acesso** com a chave de acesso de Olá de Olá conta do Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="5d06c-338">Replace **access key** with hello access key of hello Azure Batch account.</span></span>
   3. <span data-ttu-id="5d06c-339">Introduza o ID de Olá do conjunto de Olá para Olá **poolName** propriedade**.**</span><span class="sxs-lookup"><span data-stu-id="5d06c-339">Enter hello ID of hello pool for hello **poolName** property**.**</span></span> <span data-ttu-id="5d06c-340">Para esta propriedade, pode especificar o nome do conjunto ou agrupamento ID.</span><span class="sxs-lookup"><span data-stu-id="5d06c-340">For this property, you can specify either pool name or pool ID.</span></span>
   4. <span data-ttu-id="5d06c-341">Introduza o lote de Olá URI para Olá **batchUri** propriedade JSON.</span><span class="sxs-lookup"><span data-stu-id="5d06c-341">Enter hello batch URI for hello **batchUri** JSON property.</span></span>

      > [!IMPORTANT]
      > <span data-ttu-id="5d06c-342">Olá **URL** de Olá **painel de conta do Azure Batch** está a ser Olá seguinte formato: \<accountname\>.\< região\>. batch.azure.com. Para Olá **batchUri** propriedade no Olá JSON, terá de demasiado**remover "accountname."**</span><span class="sxs-lookup"><span data-stu-id="5d06c-342">hello **URL** from hello **Azure Batch account blade** is in hello following format: \<accountname\>.\<region\>.batch.azure.com. For hello **batchUri** property in hello JSON, you need too**remove "accountname."**</span></span> <span data-ttu-id="5d06c-343">do URL de Olá.</span><span class="sxs-lookup"><span data-stu-id="5d06c-343">from hello URL.</span></span> <span data-ttu-id="5d06c-344">Exemplo: `"batchUri": "https://eastus.batch.azure.com"`.</span><span class="sxs-lookup"><span data-stu-id="5d06c-344">Example: `"batchUri": "https://eastus.batch.azure.com"`.</span></span>
      >
      >

      ![](./media/data-factory-data-processing-using-batch/image9.png)

      <span data-ttu-id="5d06c-345">Para Olá **poolName** propriedade, também pode especificar Olá ID do conjunto de Olá em vez do nome de Olá do conjunto de Olá.</span><span class="sxs-lookup"><span data-stu-id="5d06c-345">For hello **poolName** property, you can also specify hello ID of hello pool instead of hello name of hello pool.</span></span>

      > [!NOTE]
      > <span data-ttu-id="5d06c-346">Olá serviço fábrica de dados não suporta uma opção a pedido para o Azure Batch como para o HDInsight.</span><span class="sxs-lookup"><span data-stu-id="5d06c-346">hello Data Factory service does not support an on-demand option for Azure Batch as it does for HDInsight.</span></span> <span data-ttu-id="5d06c-347">Só pode utilizar o seu próprio conjunto do Azure Batch num Azure data factory.</span><span class="sxs-lookup"><span data-stu-id="5d06c-347">You can only use your own Azure Batch pool in an Azure data factory.</span></span>
      >
      >
   5. <span data-ttu-id="5d06c-348">Especifique **StorageLinkedService** para Olá **linkedServiceName** propriedade.</span><span class="sxs-lookup"><span data-stu-id="5d06c-348">Specify **StorageLinkedService** for hello **linkedServiceName** property.</span></span> <span data-ttu-id="5d06c-349">Este serviço ligado que criou no passo anterior Olá.</span><span class="sxs-lookup"><span data-stu-id="5d06c-349">You created this linked service in hello previous step.</span></span> <span data-ttu-id="5d06c-350">Este tipo de armazenamento é utilizado como uma área de transição para ficheiros e registos.</span><span class="sxs-lookup"><span data-stu-id="5d06c-350">This storage is used as a staging area for files and logs.</span></span>
3. <span data-ttu-id="5d06c-351">Clique em **implementar** no comando Olá barra toodeploy Olá ligado serviço.</span><span class="sxs-lookup"><span data-stu-id="5d06c-351">Click **Deploy** on hello command bar toodeploy hello linked service.</span></span>

#### <a name="step-3-create-datasets"></a><span data-ttu-id="5d06c-352">Passo 3: Criar conjuntos de dados</span><span class="sxs-lookup"><span data-stu-id="5d06c-352">Step 3: Create datasets</span></span>
<span data-ttu-id="5d06c-353">Neste passo, criar toorepresent de conjuntos de dados de entrada e saída de dados.</span><span class="sxs-lookup"><span data-stu-id="5d06c-353">In this step, you create datasets toorepresent input and output data.</span></span>

#### <a name="create-input-dataset"></a><span data-ttu-id="5d06c-354">Criar conjunto de dados de entrada</span><span class="sxs-lookup"><span data-stu-id="5d06c-354">Create input dataset</span></span>
1. <span data-ttu-id="5d06c-355">No Olá **Editor** para Olá Data Factory, clique em **novo conjunto de dados** botão na toolbar Olá e clique em **Blob storage do Azure** no menu de Olá pendente.</span><span class="sxs-lookup"><span data-stu-id="5d06c-355">In hello **Editor** for hello Data Factory, click **New dataset** button on hello toolbar and click **Azure Blob storage** from hello drop-down menu.</span></span>
2. <span data-ttu-id="5d06c-356">Substitua Olá JSON no painel direito Olá Olá seguinte fragmento JSON:</span><span class="sxs-lookup"><span data-stu-id="5d06c-356">Replace hello JSON in hello right pane with hello following JSON snippet:</span></span>

    ```json
    {
       "name": "InputDataset",
       "properties": {
           "type": "AzureBlob",
           "linkedServiceName": "AzureStorageLinkedService",
           "typeProperties": {
               "folderPath": "mycontainer/inputfolder/{Year}-{Month}-{Day}-{Hour}",
               "format": {
                   "type": "TextFormat"
               },
               "partitionedBy": [
                   {
                       "name": "Year",
                       "value": {
                           "type": "DateTime",
                           "date": "SliceStart",
                           "format": "yyyy"
                       }
                   },
                   {
                       "name": "Month",
                       "value": {
                           "type": "DateTime",
                           "date": "SliceStart",
                           "format": "MM"
                       }
                   },
                   {
                       "name": "Day",
                       "value": {
                           "type": "DateTime",
                           "date": "SliceStart",
                           "format": "dd"
                       }
                   },
                   {
                       "name": "Hour",
                       "value": {
                           "type": "DateTime",
                           "date": "SliceStart",
                           "format": "HH"
                       }
                   }
               ]
           },
           "availability": {
               "frequency": "Hour",
               "interval": 1
           },
           "external": true,
           "policy": {}
       }
    }
    ```

    <span data-ttu-id="5d06c-357">Pode cria um pipeline mais tarde esta explicação passo a passo com a hora de início: 2015-11-tempo 16T00:00:00Z e de fim: 2015-11-16T05:00:00Z.</span><span class="sxs-lookup"><span data-stu-id="5d06c-357">You create a pipeline later in this walkthrough with start time: 2015-11-16T00:00:00Z and end time: 2015-11-16T05:00:00Z.</span></span> <span data-ttu-id="5d06c-358">É agendada tooproduce dados **hora a hora**, pelo que existem 5 setores de entrada/saída (entre **00**: 00:00 -\> **05**: 00:00).</span><span class="sxs-lookup"><span data-stu-id="5d06c-358">It is scheduled tooproduce data **hourly**, so there are 5 input/output slices (between **00**:00:00 -\> **05**:00:00).</span></span>

    <span data-ttu-id="5d06c-359">Olá **frequência** e **intervalo** para o conjunto de dados de entrada Olá estiver definido demasiado**hora** e **1**, que significa que Olá entrada setor está disponível hora a hora.</span><span class="sxs-lookup"><span data-stu-id="5d06c-359">hello **frequency** and **interval** for hello input dataset is set too**Hour** and **1**, which means that hello input slice is available hourly.</span></span>

    <span data-ttu-id="5d06c-360">Seguem-se Olá horas de início cada setor, que são representadas por **SliceStart** variável de sistema no Olá acima fragmento JSON.</span><span class="sxs-lookup"><span data-stu-id="5d06c-360">Here are hello start times for each slice, which is represented by **SliceStart** system variable in hello above JSON snippet.</span></span>

    | <span data-ttu-id="5d06c-361">**Setor**</span><span class="sxs-lookup"><span data-stu-id="5d06c-361">**Slice**</span></span> | <span data-ttu-id="5d06c-362">**Hora de início**</span><span class="sxs-lookup"><span data-stu-id="5d06c-362">**Start time**</span></span>          |
    |-----------|-------------------------|
    | <span data-ttu-id="5d06c-363">1</span><span class="sxs-lookup"><span data-stu-id="5d06c-363">1</span></span>         | <span data-ttu-id="5d06c-364">2015-11-16T**00**: 00:00</span><span class="sxs-lookup"><span data-stu-id="5d06c-364">2015-11-16T**00**:00:00</span></span> |
    | <span data-ttu-id="5d06c-365">2</span><span class="sxs-lookup"><span data-stu-id="5d06c-365">2</span></span>         | <span data-ttu-id="5d06c-366">2015-11-16T**01**: 00:00</span><span class="sxs-lookup"><span data-stu-id="5d06c-366">2015-11-16T**01**:00:00</span></span> |
    | <span data-ttu-id="5d06c-367">3</span><span class="sxs-lookup"><span data-stu-id="5d06c-367">3</span></span>         | <span data-ttu-id="5d06c-368">2015-11-16T**02**: 00:00</span><span class="sxs-lookup"><span data-stu-id="5d06c-368">2015-11-16T**02**:00:00</span></span> |
    | <span data-ttu-id="5d06c-369">4</span><span class="sxs-lookup"><span data-stu-id="5d06c-369">4</span></span>         | <span data-ttu-id="5d06c-370">2015-11-16T**03**: 00:00</span><span class="sxs-lookup"><span data-stu-id="5d06c-370">2015-11-16T**03**:00:00</span></span> |
    | <span data-ttu-id="5d06c-371">5</span><span class="sxs-lookup"><span data-stu-id="5d06c-371">5</span></span>         | <span data-ttu-id="5d06c-372">2015-11-16T**04**: 00:00</span><span class="sxs-lookup"><span data-stu-id="5d06c-372">2015-11-16T**04**:00:00</span></span> |

    <span data-ttu-id="5d06c-373">Olá **folderPath** é calculado utilizando a parte ano, mês, dia e hora Olá Olá setor da hora de início (**SliceStart**).</span><span class="sxs-lookup"><span data-stu-id="5d06c-373">hello **folderPath** is calculated by using hello year, month, day, and hour part of hello slice start time (**SliceStart**).</span></span> <span data-ttu-id="5d06c-374">Por conseguinte, aqui é a forma como uma pasta de entrada setor tooa mapeada.</span><span class="sxs-lookup"><span data-stu-id="5d06c-374">Therefore, here is how an input folder is mapped tooa slice.</span></span>

    | <span data-ttu-id="5d06c-375">**Setor**</span><span class="sxs-lookup"><span data-stu-id="5d06c-375">**Slice**</span></span> | <span data-ttu-id="5d06c-376">**Hora de início**</span><span class="sxs-lookup"><span data-stu-id="5d06c-376">**Start time**</span></span>          | <span data-ttu-id="5d06c-377">**Pasta de entrada**</span><span class="sxs-lookup"><span data-stu-id="5d06c-377">**Input folder**</span></span>  |
    |-----------|-------------------------|-------------------|
    | <span data-ttu-id="5d06c-378">1</span><span class="sxs-lookup"><span data-stu-id="5d06c-378">1</span></span>         | <span data-ttu-id="5d06c-379">2015-11-16T**00**: 00:00</span><span class="sxs-lookup"><span data-stu-id="5d06c-379">2015-11-16T**00**:00:00</span></span> | <span data-ttu-id="5d06c-380">2015-11-16-**00**</span><span class="sxs-lookup"><span data-stu-id="5d06c-380">2015-11-16-**00**</span></span> |
    | <span data-ttu-id="5d06c-381">2</span><span class="sxs-lookup"><span data-stu-id="5d06c-381">2</span></span>         | <span data-ttu-id="5d06c-382">2015-11-16T**01**: 00:00</span><span class="sxs-lookup"><span data-stu-id="5d06c-382">2015-11-16T**01**:00:00</span></span> | <span data-ttu-id="5d06c-383">2015-11-16-**01**</span><span class="sxs-lookup"><span data-stu-id="5d06c-383">2015-11-16-**01**</span></span> |
    | <span data-ttu-id="5d06c-384">3</span><span class="sxs-lookup"><span data-stu-id="5d06c-384">3</span></span>         | <span data-ttu-id="5d06c-385">2015-11-16T**02**: 00:00</span><span class="sxs-lookup"><span data-stu-id="5d06c-385">2015-11-16T**02**:00:00</span></span> | <span data-ttu-id="5d06c-386">2015-11-16-**02**</span><span class="sxs-lookup"><span data-stu-id="5d06c-386">2015-11-16-**02**</span></span> |
    | <span data-ttu-id="5d06c-387">4</span><span class="sxs-lookup"><span data-stu-id="5d06c-387">4</span></span>         | <span data-ttu-id="5d06c-388">2015-11-16T**03**: 00:00</span><span class="sxs-lookup"><span data-stu-id="5d06c-388">2015-11-16T**03**:00:00</span></span> | <span data-ttu-id="5d06c-389">2015-11-16-**03**</span><span class="sxs-lookup"><span data-stu-id="5d06c-389">2015-11-16-**03**</span></span> |
    | <span data-ttu-id="5d06c-390">5</span><span class="sxs-lookup"><span data-stu-id="5d06c-390">5</span></span>         | <span data-ttu-id="5d06c-391">2015-11-16T**04**: 00:00</span><span class="sxs-lookup"><span data-stu-id="5d06c-391">2015-11-16T**04**:00:00</span></span> | <span data-ttu-id="5d06c-392">2015-11-16-**04**</span><span class="sxs-lookup"><span data-stu-id="5d06c-392">2015-11-16-**04**</span></span> |

1. <span data-ttu-id="5d06c-393">Clique em **implementar** no Olá toocreate da barra de ferramentas e implementar Olá **InputDataset** tabela.</span><span class="sxs-lookup"><span data-stu-id="5d06c-393">Click **Deploy** on hello toolbar toocreate and deploy hello **InputDataset** table.</span></span>

#### <a name="create-output-dataset"></a><span data-ttu-id="5d06c-394">Criar conjunto de dados de saída</span><span class="sxs-lookup"><span data-stu-id="5d06c-394">Create output dataset</span></span>
<span data-ttu-id="5d06c-395">Neste passo, crie outro conjunto de dados do tipo AzureBlob toorepresent Olá dados de saída.</span><span class="sxs-lookup"><span data-stu-id="5d06c-395">In this step, you create another dataset of type AzureBlob toorepresent hello output data.</span></span>

1. <span data-ttu-id="5d06c-396">No Olá **Editor** para Olá Data Factory, clique em **novo conjunto de dados** botão na toolbar Olá e clique em **Blob storage do Azure** no menu de Olá pendente.</span><span class="sxs-lookup"><span data-stu-id="5d06c-396">In hello **Editor** for hello Data Factory, click **New dataset** button on hello toolbar and click **Azure Blob storage** from hello drop-down menu.</span></span>
2. <span data-ttu-id="5d06c-397">Substitua Olá JSON no painel direito Olá Olá seguinte fragmento JSON:</span><span class="sxs-lookup"><span data-stu-id="5d06c-397">Replace hello JSON in hello right pane with hello following JSON snippet:</span></span>

    ```json
    {
       "name": "OutputDataset",
       "properties": {
           "type": "AzureBlob",
           "linkedServiceName": "AzureStorageLinkedService",
           "typeProperties": {
               "fileName": "{slice}.txt",
               "folderPath": "mycontainer/outputfolder",
               "partitionedBy": [
                   {
                       "name": "slice",
                       "value": {
                           "type": "DateTime",
                           "date": "SliceStart",
                           "format": "yyyy-MM-dd-HH"
                       }
                   }
               ]
           },
           "availability": {
               "frequency": "Hour",
               "interval": 1
           }
       }
    }
    ```

    <span data-ttu-id="5d06c-398">Um ficheiro/blob de saída é gerado para cada setor de entrada.</span><span class="sxs-lookup"><span data-stu-id="5d06c-398">An output blob/file is generated for each input slice.</span></span> <span data-ttu-id="5d06c-399">Eis como um ficheiro de saída é designado para cada setor.</span><span class="sxs-lookup"><span data-stu-id="5d06c-399">Here is how an output file is named for each slice.</span></span> <span data-ttu-id="5d06c-400">Todos os ficheiros de saída de Olá são gerados por uma pasta de saída: `mycontainer\\outputfolder`.</span><span class="sxs-lookup"><span data-stu-id="5d06c-400">All hello output files are generated in one output folder: `mycontainer\\outputfolder`.</span></span>

    | <span data-ttu-id="5d06c-401">**Setor**</span><span class="sxs-lookup"><span data-stu-id="5d06c-401">**Slice**</span></span> | <span data-ttu-id="5d06c-402">**Hora de início**</span><span class="sxs-lookup"><span data-stu-id="5d06c-402">**Start time**</span></span>          | <span data-ttu-id="5d06c-403">**Ficheiro de saída**</span><span class="sxs-lookup"><span data-stu-id="5d06c-403">**Output file**</span></span>       |
    |-----------|-------------------------|-----------------------|
    | <span data-ttu-id="5d06c-404">1</span><span class="sxs-lookup"><span data-stu-id="5d06c-404">1</span></span>         | <span data-ttu-id="5d06c-405">2015-11-16T**00**: 00:00</span><span class="sxs-lookup"><span data-stu-id="5d06c-405">2015-11-16T**00**:00:00</span></span> | <span data-ttu-id="5d06c-406">2015-11-16 -**00. txt**</span><span class="sxs-lookup"><span data-stu-id="5d06c-406">2015-11-16-**00.txt**</span></span> |
    | <span data-ttu-id="5d06c-407">2</span><span class="sxs-lookup"><span data-stu-id="5d06c-407">2</span></span>         | <span data-ttu-id="5d06c-408">2015-11-16T**01**: 00:00</span><span class="sxs-lookup"><span data-stu-id="5d06c-408">2015-11-16T**01**:00:00</span></span> | <span data-ttu-id="5d06c-409">2015-11-16 -**01. txt**</span><span class="sxs-lookup"><span data-stu-id="5d06c-409">2015-11-16-**01.txt**</span></span> |
    | <span data-ttu-id="5d06c-410">3</span><span class="sxs-lookup"><span data-stu-id="5d06c-410">3</span></span>         | <span data-ttu-id="5d06c-411">2015-11-16T**02**: 00:00</span><span class="sxs-lookup"><span data-stu-id="5d06c-411">2015-11-16T**02**:00:00</span></span> | <span data-ttu-id="5d06c-412">2015-11-16 -**02. txt**</span><span class="sxs-lookup"><span data-stu-id="5d06c-412">2015-11-16-**02.txt**</span></span> |
    | <span data-ttu-id="5d06c-413">4</span><span class="sxs-lookup"><span data-stu-id="5d06c-413">4</span></span>         | <span data-ttu-id="5d06c-414">2015-11-16T**03**: 00:00</span><span class="sxs-lookup"><span data-stu-id="5d06c-414">2015-11-16T**03**:00:00</span></span> | <span data-ttu-id="5d06c-415">2015-11-16 -**03. txt**</span><span class="sxs-lookup"><span data-stu-id="5d06c-415">2015-11-16-**03.txt**</span></span> |
    | <span data-ttu-id="5d06c-416">5</span><span class="sxs-lookup"><span data-stu-id="5d06c-416">5</span></span>         | <span data-ttu-id="5d06c-417">2015-11-16T**04**: 00:00</span><span class="sxs-lookup"><span data-stu-id="5d06c-417">2015-11-16T**04**:00:00</span></span> | <span data-ttu-id="5d06c-418">2015-11-16 -**04. txt**</span><span class="sxs-lookup"><span data-stu-id="5d06c-418">2015-11-16-**04.txt**</span></span> |

    <span data-ttu-id="5d06c-419">Lembre-se de que todos os ficheiros numa pasta entrada de Olá (por exemplo: 2015-11-16-00) fazem parte de um setor com a hora de início Olá: 2015-11-16-00.</span><span class="sxs-lookup"><span data-stu-id="5d06c-419">Remember that all hello files in an input folder (for example: 2015-11-16-00) are part of a slice with hello start time: 2015-11-16-00.</span></span> <span data-ttu-id="5d06c-420">Quando este setor é processado, atividade personalizada Olá analisa através de cada ficheiro e produz uma linha no ficheiro de saída de Olá com o número de Olá de ocorrências do termo de pesquisa ("Microsoft").</span><span class="sxs-lookup"><span data-stu-id="5d06c-420">When this slice is processed, hello custom activity scans through each file and produces a line in hello output file with hello number of occurrences of search term (“Microsoft”).</span></span> <span data-ttu-id="5d06c-421">Se existirem três ficheiros na pasta Olá 2015-11-16-00, existem três linhas no ficheiro de saída Olá: 2015-11-16-00.txt.</span><span class="sxs-lookup"><span data-stu-id="5d06c-421">If there are three files in hello folder 2015-11-16-00, there are three lines in hello output file: 2015-11-16-00.txt.</span></span>

1. <span data-ttu-id="5d06c-422">Clique em **implementar** no Olá toocreate da barra de ferramentas e implementar Olá **OutputDataset**.</span><span class="sxs-lookup"><span data-stu-id="5d06c-422">Click **Deploy** on hello toolbar toocreate and deploy hello **OutputDataset**.</span></span>

#### <a name="step-4-create-and-run-hello-pipeline-with-custom-activity"></a><span data-ttu-id="5d06c-423">Passo 4: Criar e executar o pipeline de Olá com atividade personalizada</span><span class="sxs-lookup"><span data-stu-id="5d06c-423">Step 4: Create and run hello pipeline with custom activity</span></span>
<span data-ttu-id="5d06c-424">Neste passo, vai criar um pipeline com uma atividade, atividade personalizada Olá que criou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="5d06c-424">In this step, you create a pipeline with one activity, hello custom activity you created earlier.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5d06c-425">Se ainda não adicionou Olá **file.txt** tooinput pastas no contentor de blob Olá, fazê-lo antes de criar o pipeline de Olá.</span><span class="sxs-lookup"><span data-stu-id="5d06c-425">If you haven't uploaded hello **file.txt** tooinput folders in hello blob container, do so before creating hello pipeline.</span></span> <span data-ttu-id="5d06c-426">Olá **isPaused** propriedade é definida toofalse na Olá JSON do pipeline, para o pipeline de Olá seja executada imediatamente como Olá **iniciar** data está no passado Olá.</span><span class="sxs-lookup"><span data-stu-id="5d06c-426">hello **isPaused** property is set toofalse in hello pipeline JSON, so hello pipeline runs immediately as hello **start** date is in hello past.</span></span>
>
>

1. <span data-ttu-id="5d06c-427">No Editor do Data Factory Olá, clique em **novo pipeline** na barra de comandos Olá.</span><span class="sxs-lookup"><span data-stu-id="5d06c-427">In hello Data Factory Editor, click **New pipeline** on hello command bar.</span></span> <span data-ttu-id="5d06c-428">Se não vir comando Olá, clique em **... (Reticências)**  toosee-lo.</span><span class="sxs-lookup"><span data-stu-id="5d06c-428">If you do not see hello command, click **... (Ellipsis)** toosee it.</span></span>
2. <span data-ttu-id="5d06c-429">Substitua Olá JSON no painel direito Olá Olá seguinte script JSON:</span><span class="sxs-lookup"><span data-stu-id="5d06c-429">Replace hello JSON in hello right pane with hello following JSON script:</span></span>

    ```json
    {
       "name": "PipelineCustom",
       "properties": {
           "description": "Use custom activity",
           "activities": [
               {
                   "type": "DotNetActivity",
                   "typeProperties": {
                       "assemblyName": "MyDotNetActivity.dll",
                       "entryPoint": "MyDotNetActivityNS.MyDotNetActivity",
                       "packageLinkedService": "AzureStorageLinkedService",
                       "packageFile": "customactivitycontainer/MyDotNetActivity.zip"
                   },
                   "inputs": [
                       {
                           "name": "InputDataset"
                       }
                   ],
                   "outputs": [
                       {
                           "name": "OutputDataset"
                       }
                   ],
                   "policy": {
                       "timeout": "00:30:00",
                       "concurrency": 5,
                       "retry": 3
                   },
                   "scheduler": {
                       "frequency": "Hour",
                       "interval": 1
                   },
                   "name": "MyDotNetActivity",
                   "linkedServiceName": "AzureBatchLinkedService"
               }
           ],
           "start": "2015-11-16T00:00:00Z",
           "end": "2015-11-16T05:00:00Z",
           "isPaused": false
      }
    }
    ```
   <span data-ttu-id="5d06c-430">Tenha em atenção Olá seguintes pontos:</span><span class="sxs-lookup"><span data-stu-id="5d06c-430">Note hello following points:</span></span>

   * <span data-ttu-id="5d06c-431">Não existe apenas uma atividade no pipeline de Olá e que é do tipo: **DotNetActivity**.</span><span class="sxs-lookup"><span data-stu-id="5d06c-431">There is only one activity in hello pipeline and that is of type: **DotNetActivity**.</span></span>
   * <span data-ttu-id="5d06c-432">**AssemblyName** é definir nome toohello Olá DLL: **MyDotNetActivity.dll**.</span><span class="sxs-lookup"><span data-stu-id="5d06c-432">**AssemblyName** is set toohello name of hello DLL: **MyDotNetActivity.dll**.</span></span>
   * <span data-ttu-id="5d06c-433">**EntryPoint** estiver definido demasiado**MyDotNetActivityNS.MyDotNetActivity**.</span><span class="sxs-lookup"><span data-stu-id="5d06c-433">**EntryPoint** is set too**MyDotNetActivityNS.MyDotNetActivity**.</span></span> <span data-ttu-id="5d06c-434">É basicamente \<espaço de nomes\>.\< ClassName\> no seu código.</span><span class="sxs-lookup"><span data-stu-id="5d06c-434">It is basically \<namespace\>.\<classname\> in your code.</span></span>
   * <span data-ttu-id="5d06c-435">**PackageLinkedService** estiver definido demasiado**StorageLinkedService** que aponta de armazenamento de BLOBs de toohello que contém o ficheiro zip do Olá atividade personalizada.</span><span class="sxs-lookup"><span data-stu-id="5d06c-435">**PackageLinkedService** is set too**StorageLinkedService** that points toohello blob storage that contains hello custom activity zip file.</span></span> <span data-ttu-id="5d06c-436">Se estiver a utilizar diferentes contas de armazenamento do Azure para ficheiros de entrada/saída e o ficheiro zip do Olá atividade personalizada, terá de toocreate outro armazenamento do Azure serviço ligado.</span><span class="sxs-lookup"><span data-stu-id="5d06c-436">If you are using different Azure Storage accounts for input/output files and hello custom activity zip file, you have toocreate another Azure Storage linked service.</span></span> <span data-ttu-id="5d06c-437">Este artigo assume que está a utilizar Olá a mesma conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="5d06c-437">This article assumes that you are using hello same Azure Storage account.</span></span>
   * <span data-ttu-id="5d06c-438">**PackageFile** estiver definido demasiado**customactivitycontainer/MyDotNetActivity.zip**.</span><span class="sxs-lookup"><span data-stu-id="5d06c-438">**PackageFile** is set too**customactivitycontainer/MyDotNetActivity.zip**.</span></span> <span data-ttu-id="5d06c-439">Está no formato de Olá: \<containerforthezip\>/\<nameofthezip.zip\>.</span><span class="sxs-lookup"><span data-stu-id="5d06c-439">It is in hello format: \<containerforthezip\>/\<nameofthezip.zip\>.</span></span>
   * <span data-ttu-id="5d06c-440">atividade personalizada Olá demora **InputDataset** como entrada e **OutputDataset** como saída.</span><span class="sxs-lookup"><span data-stu-id="5d06c-440">hello custom activity takes **InputDataset** as input and **OutputDataset** as output.</span></span>
   * <span data-ttu-id="5d06c-441">Olá **linkedServiceName** propriedade de atividade personalizado Olá aponta toohello **AzureBatchLinkedService**, que informa a Azure Data Factory dessa atividade personalizada Olá tem toorun do Azure batch.</span><span class="sxs-lookup"><span data-stu-id="5d06c-441">hello **linkedServiceName** property of hello custom activity points toohello **AzureBatchLinkedService**, which tells Azure Data Factory that hello custom activity needs toorun on Azure Batch.</span></span>
   * <span data-ttu-id="5d06c-442">Olá **simultaneidade** definição é importante.</span><span class="sxs-lookup"><span data-stu-id="5d06c-442">hello **concurrency** setting is important.</span></span> <span data-ttu-id="5d06c-443">Se utilizar o valor predefinido de Olá, que é 1, mesmo se tiver de 2 ou mais nós de computação num conjunto do Azure Batch de Olá, são processados de setores de Olá umas a seguir.</span><span class="sxs-lookup"><span data-stu-id="5d06c-443">If you use hello default value, which is 1, even if you have 2 or more compute nodes in hello Azure Batch pool, hello slices are processed one after another.</span></span> <span data-ttu-id="5d06c-444">Por conseguinte, não são tirar partido da capacidade de processamento paralelo de Olá do Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="5d06c-444">Therefore, you are not taking advantage of hello parallel processing capability of Azure Batch.</span></span> <span data-ttu-id="5d06c-445">Se definir **simultaneidade** tooa valor mais alto, diga 2, significa que dois setores (corresponde tootwo tarefas no Azure Batch) podem ser processados em Olá mesmo tempo, caso em que ambas as VMs de Olá no Olá do Azure Batch são utilizados de agrupamento.</span><span class="sxs-lookup"><span data-stu-id="5d06c-445">If you set **concurrency** tooa higher value, say 2, it means that two slices (corresponds tootwo tasks in Azure Batch) can be processed at hello same time, in which case, both hello VMs in hello Azure Batch pool are utilized.</span></span> <span data-ttu-id="5d06c-446">Por conseguinte, defina a propriedade de simultaneidade de Olá adequadamente.</span><span class="sxs-lookup"><span data-stu-id="5d06c-446">Therefore, set hello concurrency property appropriately.</span></span>
   * <span data-ttu-id="5d06c-447">Por predefinição, apenas uma tarefa (setor) é executada numa VM em qualquer momento.</span><span class="sxs-lookup"><span data-stu-id="5d06c-447">Only one task (slice) is executed on a VM at any point by default.</span></span> <span data-ttu-id="5d06c-448">Olá razão é que, por predefinição, hello **máximo de tarefas por VM** está definido too1 para um conjunto do Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="5d06c-448">hello reason is that, by default, hello **Maximum tasks per VM** is set too1 for an Azure Batch pool.</span></span> <span data-ttu-id="5d06c-449">Como parte da pré-requisitos, criou um conjunto com este too2 de conjunto de propriedade para duas setores de fábrica de dados podem estar em execução numa VM em Olá mesmo tempo.</span><span class="sxs-lookup"><span data-stu-id="5d06c-449">As part of prerequisites, you created a pool with this property set too2, so two Data Factory slices can be running on a VM at hello same time.</span></span>

    -   <span data-ttu-id="5d06c-450">**isPaused** propriedade está definida toofalse por predefinição.</span><span class="sxs-lookup"><span data-stu-id="5d06c-450">**isPaused** property is set toofalse by default.</span></span> <span data-ttu-id="5d06c-451">pipeline de Olá executa imediatamente neste exemplo, porque setores Olá iniciar no Olá passado.</span><span class="sxs-lookup"><span data-stu-id="5d06c-451">hello pipeline runs immediately in this example because hello slices start in hello past.</span></span> <span data-ttu-id="5d06c-452">Pode definir o pipeline do Olá tootrue toopause esta propriedade e defini-lo toorestart toofalse anterior.</span><span class="sxs-lookup"><span data-stu-id="5d06c-452">You can set this property tootrue toopause hello pipeline and set it back toofalse toorestart.</span></span>

    -   <span data-ttu-id="5d06c-453">Olá **iniciar** tempo e **final** vezes são, à excepção de cinco horas e setores são produzidos de hora a hora, pelo que os cinco setores são produzidos pelo pipeline Olá.</span><span class="sxs-lookup"><span data-stu-id="5d06c-453">hello **start** time and **end** times are five hours apart and slices are produced hourly, so five slices are produced by hello pipeline.</span></span>

1. <span data-ttu-id="5d06c-454">Clique em **implementar** no comando Olá barra pipeline de Olá toodeploy.</span><span class="sxs-lookup"><span data-stu-id="5d06c-454">Click **Deploy** on hello command bar toodeploy hello pipeline.</span></span>

#### <a name="step-5-test-hello-pipeline"></a><span data-ttu-id="5d06c-455">Passo 5: Testar o pipeline de Olá</span><span class="sxs-lookup"><span data-stu-id="5d06c-455">Step 5: Test hello pipeline</span></span>
<span data-ttu-id="5d06c-456">Neste passo, teste pipeline Olá, arrastando ficheiros em pastas Olá de entrada.</span><span class="sxs-lookup"><span data-stu-id="5d06c-456">In this step, you test hello pipeline by dropping files into hello input folders.</span></span> <span data-ttu-id="5d06c-457">Vamos começar com o pipeline de Olá teste com um ficheiro por uma pasta de entrada.</span><span class="sxs-lookup"><span data-stu-id="5d06c-457">Let’s start with testing hello pipeline with one file per one input folder.</span></span>

1. <span data-ttu-id="5d06c-458">No painel de fábrica de dados de Olá no Olá portal do Azure, clique em **diagrama**.</span><span class="sxs-lookup"><span data-stu-id="5d06c-458">In hello Data Factory blade in hello Azure portal, click **Diagram**.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image10.png)
2. <span data-ttu-id="5d06c-459">Na vista de diagrama Olá, faça duplo clique em conjunto de dados de entrada: **InputDataset**.</span><span class="sxs-lookup"><span data-stu-id="5d06c-459">In hello diagram view, double-click input dataset: **InputDataset**.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image11.png)
3. <span data-ttu-id="5d06c-460">Deverá ver Olá **InputDataset** painel com todos os cinco setores pronto.</span><span class="sxs-lookup"><span data-stu-id="5d06c-460">You should see hello **InputDataset** blade with all five slices ready.</span></span> <span data-ttu-id="5d06c-461">Olá aviso **hora de início do SETOR** e **hora de fim de SETOR** para cada setor.</span><span class="sxs-lookup"><span data-stu-id="5d06c-461">Notice hello **SLICE START TIME** and **SLICE END TIME** for each slice.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image12.png)
4. <span data-ttu-id="5d06c-462">No Olá **vista de diagrama**, agora, clique em **OutputDataset**.</span><span class="sxs-lookup"><span data-stu-id="5d06c-462">In hello **Diagram View**, now click **OutputDataset**.</span></span>
5. <span data-ttu-id="5d06c-463">Deverá ver que os setores de saída cinco Olá estão no estado pronto Olá se que já foram produzidos.</span><span class="sxs-lookup"><span data-stu-id="5d06c-463">You should see that hello five output slices are in hello Ready state if they have already been produced.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image13.png)
6. <span data-ttu-id="5d06c-464">Olá tooview portal do Azure de utilização **tarefas** associado Olá **setores** e ver que VM cada setor é executado no.</span><span class="sxs-lookup"><span data-stu-id="5d06c-464">Use Azure portal tooview hello **tasks** associated with hello **slices** and see what VM each slice ran on.</span></span> <span data-ttu-id="5d06c-465">Consulte [integração com o Data Factory e Batch](#data-factory-and-batch-integration) secção para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="5d06c-465">See [Data Factory and Batch integration](#data-factory-and-batch-integration) section for details.</span></span>
7. <span data-ttu-id="5d06c-466">Deverá ver ficheiros de saída de Olá no Olá `outputfolder` de `mycontainer` no seu Azure armazenamento de Blobs.</span><span class="sxs-lookup"><span data-stu-id="5d06c-466">You should see hello output files in hello `outputfolder` of `mycontainer` in your Azure blob storage.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image15.png)

   <span data-ttu-id="5d06c-467">Deverá ver cinco ficheiros de saída, uma para cada setor de entrada.</span><span class="sxs-lookup"><span data-stu-id="5d06c-467">You should see five output files, one for each input slice.</span></span> <span data-ttu-id="5d06c-468">Cada um dos Olá de saída do ficheiro deve ter conteúdo toohello semelhante seguinte saída:</span><span class="sxs-lookup"><span data-stu-id="5d06c-468">Each of hello output file should have content similar toohello following output:</span></span>

    ```
    2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-00/file.txt.
    ```
   <span data-ttu-id="5d06c-469">Olá diagrama seguinte ilustra como setores de fábrica de dados de Olá mapeiam tootasks no Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="5d06c-469">hello following diagram illustrates how hello Data Factory slices map tootasks in Azure Batch.</span></span> <span data-ttu-id="5d06c-470">Neste exemplo, um setor tem apenas uma execução.</span><span class="sxs-lookup"><span data-stu-id="5d06c-470">In this example, a slice has only one run.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image16.png)
8. <span data-ttu-id="5d06c-471">Agora, vamos tentar com vários ficheiros numa pasta.</span><span class="sxs-lookup"><span data-stu-id="5d06c-471">Now, let’s try with multiple files in a folder.</span></span> <span data-ttu-id="5d06c-472">Criar ficheiros: **file2.txt**, **file3.txt**, **file4.txt**, e **file5.txt** com Olá mesmo conteúdo, tal como em file.txt na pasta Olá: **2015-11-06-01**.</span><span class="sxs-lookup"><span data-stu-id="5d06c-472">Create files: **file2.txt**, **file3.txt**, **file4.txt**, and **file5.txt** with hello same content as in file.txt in hello folder: **2015-11-06-01**.</span></span>
9. <span data-ttu-id="5d06c-473">Na pasta de saída Olá, **eliminar** Olá o ficheiro de saída: **2015-11-16-01.txt**.</span><span class="sxs-lookup"><span data-stu-id="5d06c-473">In hello output folder, **delete** hello output file: **2015-11-16-01.txt**.</span></span>
10. <span data-ttu-id="5d06c-474">Agora, no Olá **OutputDataset** painel, o setor de Olá contexto com **hora de início do SETOR** definido demasiado**11/16/2015 01:00:00 AM**e clique em **executar**setor Olá toorerun/re-process.</span><span class="sxs-lookup"><span data-stu-id="5d06c-474">Now, in hello **OutputDataset** blade, right-click hello slice with **SLICE START TIME** set too**11/16/2015 01:00:00 AM**, and click **Run** toorerun/re-process hello slice.</span></span> <span data-ttu-id="5d06c-475">Agora, o setor de Olá tem cinco ficheiros em vez de um ficheiro.</span><span class="sxs-lookup"><span data-stu-id="5d06c-475">Now, hello slice has five files instead of one file.</span></span>

    ![](./media/data-factory-data-processing-using-batch/image17.png)
11. <span data-ttu-id="5d06c-476">Depois de setor de Olá é executado e o respetivo estado é **pronto**, verifique o conteúdo de Olá no ficheiro de saída de Olá neste setor (**2015-11-16-01.txt**) no Olá `outputfolder` de `mycontainer` no seu armazenamento de Blobs.</span><span class="sxs-lookup"><span data-stu-id="5d06c-476">After hello slice runs and its status is **Ready**, verify hello content in hello output file for this slice (**2015-11-16-01.txt**) in hello `outputfolder` of `mycontainer` in your blob storage.</span></span> <span data-ttu-id="5d06c-477">Deve ser uma linha para cada ficheiro de setor de Olá.</span><span class="sxs-lookup"><span data-stu-id="5d06c-477">There should be a line for each file of hello slice.</span></span>

    ```
    2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-01/file.txt.
    2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-01/file2.txt.
    2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-01/file3.txt.
    2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-01/file4.txt.
    2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-01/file5.txt.
    ```

> [!NOTE]
> <span data-ttu-id="5d06c-478">Se não eliminou o 2015 de ficheiro da saída Olá-11-16-01.txt antes de tentar com cinco ficheiros de entrada, verá uma linha de setor anterior Olá executar e cinco linhas de setor atual Olá executar.</span><span class="sxs-lookup"><span data-stu-id="5d06c-478">If you did not delete hello output file 2015-11-16-01.txt before trying with five input files, you see one line from hello previous slice run and five lines from hello current slice run.</span></span> <span data-ttu-id="5d06c-479">Por predefinição, o conteúdo de Olá é anexado toooutput ficheiro se já existir.</span><span class="sxs-lookup"><span data-stu-id="5d06c-479">By default, hello content is appended toooutput file if it already exists.</span></span>
>
>

#### <a name="data-factory-and-batch-integration"></a><span data-ttu-id="5d06c-480">Integração de fábrica de dados e de Batch</span><span class="sxs-lookup"><span data-stu-id="5d06c-480">Data Factory and Batch integration</span></span>
<span data-ttu-id="5d06c-481">Olá serviço Data Factory cria uma tarefa no Azure Batch com o nome de Olá: `adf-poolname:job-xxx`.</span><span class="sxs-lookup"><span data-stu-id="5d06c-481">hello Data Factory service creates a job in Azure Batch with hello name: `adf-poolname:job-xxx`.</span></span>

![O Azure Data Factory - tarefas do Batch](media/data-factory-data-processing-using-batch/data-factory-batch-jobs.png)

<span data-ttu-id="5d06c-483">É criada uma tarefa na tarefa de Olá para cada execução de atividade de um setor.</span><span class="sxs-lookup"><span data-stu-id="5d06c-483">A task in hello job is created for each activity run of a slice.</span></span> <span data-ttu-id="5d06c-484">Se existirem toobe pronto 10 do setores, processados, são criadas 10 tarefas na tarefa de Olá.</span><span class="sxs-lookup"><span data-stu-id="5d06c-484">If there are 10 slices ready toobe processed, 10 tasks are created in hello job.</span></span> <span data-ttu-id="5d06c-485">Pode ter mais do que um setor ser executado em paralelo se tiver vários nós de computação no conjunto de Olá.</span><span class="sxs-lookup"><span data-stu-id="5d06c-485">You can have more than one slice running in parallel if you have multiple compute nodes in hello pool.</span></span> <span data-ttu-id="5d06c-486">Se Olá máximo por computação nó estiver definido demasiado > 1, podem existir mais do que um setor a ser executado no Olá computação mesma.</span><span class="sxs-lookup"><span data-stu-id="5d06c-486">If hello maximum tasks per compute node is set too> 1, there can be more than one slice running on hello same compute.</span></span>

<span data-ttu-id="5d06c-487">Neste exemplo, existem cinco setores, por isso, cinco tarefas no Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="5d06c-487">In this example, there are five slices, so five tasks in Azure Batch.</span></span> <span data-ttu-id="5d06c-488">Com Olá **simultaneidade** definido demasiado**5** no Olá pipeline JSON no Azure Data Factory e **máximo de tarefas por VM** definido demasiado**2** no Azure Batch conjunto com **2** VMs, Olá tarefas é executado rápida (Verifique os tempos de início e de fim para tarefas).</span><span class="sxs-lookup"><span data-stu-id="5d06c-488">With hello **concurrency** set too**5** in hello pipeline JSON in Azure Data Factory and **Maximum tasks per VM** set too**2** in Azure Batch pool with **2** VMs, hello tasks runs fast (check start and end times for tasks).</span></span>

<span data-ttu-id="5d06c-489">Utilize a tarefa de lote do Olá portal tooview Olá e as respetivas tarefas associadas Olá **setores** e ver que VM cada setor é executado no.</span><span class="sxs-lookup"><span data-stu-id="5d06c-489">Use hello portal tooview hello Batch job and its tasks that are associated with hello **slices** and see what VM each slice ran on.</span></span>

![O Azure Data Factory - tarefas de lote](media/data-factory-data-processing-using-batch/data-factory-batch-job-tasks.png)

### <a name="debug-hello-pipeline"></a><span data-ttu-id="5d06c-491">Depurar o pipeline de Olá</span><span class="sxs-lookup"><span data-stu-id="5d06c-491">Debug hello pipeline</span></span>
<span data-ttu-id="5d06c-492">A depuração inclui algumas técnicas básicas:</span><span class="sxs-lookup"><span data-stu-id="5d06c-492">Debugging consists of a few basic techniques:</span></span>

1. <span data-ttu-id="5d06c-493">Se o setor de entrada Olá não estiver definido demasiado**pronto**, confirmar que a estrutura de entrada de pasta Olá está correta e file.txt existe nas pastas de entrada Olá.</span><span class="sxs-lookup"><span data-stu-id="5d06c-493">If hello input slice is not set too**Ready**, confirm that hello input folder structure is correct and file.txt exists in hello input folders.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image3.png)
2. <span data-ttu-id="5d06c-494">No Olá **executar** método da atividade personalizada, utilize Olá **IActivityLogger** informações do objeto toolog que o ajuda a resolver problemas.</span><span class="sxs-lookup"><span data-stu-id="5d06c-494">In hello **Execute** method of your custom activity, use hello **IActivityLogger** object toolog information that helps you troubleshoot issues.</span></span> <span data-ttu-id="5d06c-495">mensagens Hello registado apareçam no utilizador Olá\_0. ficheiro de registo.</span><span class="sxs-lookup"><span data-stu-id="5d06c-495">hello logged messages show up in hello user\_0.log file.</span></span>

   <span data-ttu-id="5d06c-496">No Olá **OutputDataset** painel, clique em Olá do Olá setor toosee **SETOR de dados** painel para essa setor.</span><span class="sxs-lookup"><span data-stu-id="5d06c-496">In hello **OutputDataset** blade, click hello slice toosee hello **DATA SLICE** blade for that slice.</span></span> <span data-ttu-id="5d06c-497">Verá **execuções de atividade** para esse setor.</span><span class="sxs-lookup"><span data-stu-id="5d06c-497">You see **activity runs** for that slice.</span></span> <span data-ttu-id="5d06c-498">Deverá ver uma atividade executar o setor de Olá.</span><span class="sxs-lookup"><span data-stu-id="5d06c-498">You should see one activity run for hello slice.</span></span> <span data-ttu-id="5d06c-499">Se clicar em **executar** na barra de comando Olá, pode começar a outra atividade executada para Olá setor mesmo.</span><span class="sxs-lookup"><span data-stu-id="5d06c-499">If you click **Run** in hello command bar, you can start another activity run for hello same slice.</span></span>

   <span data-ttu-id="5d06c-500">Ao clicar em execução da atividade Olá, consulte Olá **detalhes da execução da ATIVIDADE** painel com uma lista de ficheiros de registo.</span><span class="sxs-lookup"><span data-stu-id="5d06c-500">When you click hello activity run, you see hello **ACTIVITY RUN DETAILS** blade with a list of log files.</span></span> <span data-ttu-id="5d06c-501">Consulte as mensagens anteriormente registadas no Olá **utilizador\_0. registo** ficheiro.</span><span class="sxs-lookup"><span data-stu-id="5d06c-501">You see logged messages in hello **user\_0.log** file.</span></span> <span data-ttu-id="5d06c-502">Quando ocorre um erro, consulte três execuções de atividade porque Olá contagem de repetições está definida too3 Olá pipeline/atividade JSON.</span><span class="sxs-lookup"><span data-stu-id="5d06c-502">When an error occurs, you see three activity runs because hello retry count is set too3 in hello pipeline/activity JSON.</span></span> <span data-ttu-id="5d06c-503">Ao clicar em execução da atividade Olá, consulte os ficheiros de registo Olá que pode rever o erro de Olá tootroubleshoot.</span><span class="sxs-lookup"><span data-stu-id="5d06c-503">When you click hello activity run, you see hello log files that you can review tootroubleshoot hello error.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image18.png)

   <span data-ttu-id="5d06c-504">Na lista de Olá dos ficheiros de registo, clique em Olá **utilizador 0.log**.</span><span class="sxs-lookup"><span data-stu-id="5d06c-504">In hello list of log files, click hello **user-0.log**.</span></span> <span data-ttu-id="5d06c-505">No painel à direita Olá são Olá os resultados da utilizando Olá **IActivityLogger.Write** método.</span><span class="sxs-lookup"><span data-stu-id="5d06c-505">In hello right panel are hello results of using hello **IActivityLogger.Write** method.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image19.png)

   <span data-ttu-id="5d06c-506">Verifique o sistema-0.log para quaisquer mensagens de erro de sistema e exceções.</span><span class="sxs-lookup"><span data-stu-id="5d06c-506">Check system-0.log for any system error messages and exceptions.</span></span>

    ```
    Trace\_T\_D\_12/6/2015 1:43:35 AM\_T\_D\_\_T\_D\_Verbose\_T\_D\_0\_T\_D\_Loading assembly file MyDotNetActivity...
    
    Trace\_T\_D\_12/6/2015 1:43:35 AM\_T\_D\_\_T\_D\_Verbose\_T\_D\_0\_T\_D\_Creating an instance of MyDotNetActivityNS.MyDotNetActivity from assembly file MyDotNetActivity...
    
    Trace\_T\_D\_12/6/2015 1:43:35 AM\_T\_D\_\_T\_D\_Verbose\_T\_D\_0\_T\_D\_Executing Module
    
    Trace\_T\_D\_12/6/2015 1:43:38 AM\_T\_D\_\_T\_D\_Information\_T\_D\_0\_T\_D\_Activity e3817da0-d843-4c5c-85c6-40ba7424dce2 finished successfully
    ```
3. <span data-ttu-id="5d06c-507">Incluir Olá **PDB** ficheiro no ficheiro zip de Olá, para que os detalhes do erro Olá tem informações como **pilha de chamadas** quando ocorre um erro.</span><span class="sxs-lookup"><span data-stu-id="5d06c-507">Include hello **PDB** file in hello zip file so that hello error details have information such as **call stack** when an error occurs.</span></span>
4. <span data-ttu-id="5d06c-508">Todos os Olá ficheiros no ficheiro zip de Olá para a atividade personalizada Olá tem de estar no Olá **principais nível** com sem subpastas.</span><span class="sxs-lookup"><span data-stu-id="5d06c-508">All hello files in hello zip file for hello custom activity must be at hello **top level** with no subfolders.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image20.png)
5. <span data-ttu-id="5d06c-509">Certifique-se de que Olá **assemblyName** (MyDotNetActivity.dll), **entryPoint** (MyDotNetActivityNS.MyDotNetActivity), **packageFile** (customactivitycontainer / MyDotNetActivity.zip), e **packageLinkedService** (deve Azure toohello de ponto de armazenamento de BLOBs que contém o ficheiro zip Olá) estão definidos valores toocorrect.</span><span class="sxs-lookup"><span data-stu-id="5d06c-509">Ensure that hello **assemblyName** (MyDotNetActivity.dll), **entryPoint** (MyDotNetActivityNS.MyDotNetActivity), **packageFile** (customactivitycontainer/MyDotNetActivity.zip), and **packageLinkedService** (should point toohello Azure blob storage that contains hello zip file) are set toocorrect values.</span></span>
6. <span data-ttu-id="5d06c-510">Se corrigido um erro e pretender setor de Olá tooreprocess, faça duplo clique setor de Olá no Olá **OutputDataset** painel e clique em **executar**.</span><span class="sxs-lookup"><span data-stu-id="5d06c-510">If you fixed an error and want tooreprocess hello slice, right-click hello slice in hello **OutputDataset** blade and click **Run**.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image21.png)

   > [!NOTE]
   > <span data-ttu-id="5d06c-511">Verá um **contentor** no seu armazenamento de Blobs do Azure com o nome: `adfjobs`.</span><span class="sxs-lookup"><span data-stu-id="5d06c-511">You see a **container** in your Azure Blob storage named: `adfjobs`.</span></span> <span data-ttu-id="5d06c-512">Este contentor não é eliminado automaticamente, mas pode eliminar em segurança depois de terminar a solução de Olá teste.</span><span class="sxs-lookup"><span data-stu-id="5d06c-512">This container is not automatically deleted, but you can safely delete it after you are done testing hello solution.</span></span> <span data-ttu-id="5d06c-513">Da mesma forma, Olá solução Data Factory cria um Azure Batch **tarefa** com o nome: `adf-\<pool ID/name\>:job-0000000001`.</span><span class="sxs-lookup"><span data-stu-id="5d06c-513">Similarly, hello Data Factory solution creates an Azure Batch **job** named: `adf-\<pool ID/name\>:job-0000000001`.</span></span> <span data-ttu-id="5d06c-514">É possível eliminar esta tarefa depois de testar solução Olá se assim o desejar.</span><span class="sxs-lookup"><span data-stu-id="5d06c-514">You can delete this job after you test hello solution if you like.</span></span>
   >
   >
7. <span data-ttu-id="5d06c-515">atividade personalizada Olá não utiliza Olá **App. config** ficheiro a partir do seu pacote.</span><span class="sxs-lookup"><span data-stu-id="5d06c-515">hello custom activity does not use hello **app.config** file from your package.</span></span> <span data-ttu-id="5d06c-516">Por conseguinte, se o seu código lê quaisquer cadeias de ligação do ficheiro de configuração de Olá, não funciona no tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="5d06c-516">Therefore, if your code reads any connection strings from hello configuration file, it does not work at runtime.</span></span> <span data-ttu-id="5d06c-517">Olá melhor prática quando utilizar o Azure Batch é toohold qualquer segredos num **Azure KeyVault**, utilize um keyvault de Olá de principal tooprotect de serviço baseada em certificado e distribuir conjunto do Batch Olá certificado tooAzure.</span><span class="sxs-lookup"><span data-stu-id="5d06c-517">hello best practice when using Azure Batch is toohold any secrets in an **Azure KeyVault**, use a certificate-based service principal tooprotect hello keyvault, and distribute hello certificate tooAzure Batch pool.</span></span> <span data-ttu-id="5d06c-518">Olá atividade personalizada do .NET, em seguida, pode aceder a segredos do Olá KeyVault no tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="5d06c-518">hello .NET custom activity then can access secrets from hello KeyVault at runtime.</span></span> <span data-ttu-id="5d06c-519">Esta solução é um genérico e pode dimensionar o tipo de tooany do segredo, não apenas a cadeia de ligação.</span><span class="sxs-lookup"><span data-stu-id="5d06c-519">This solution is a generic one and can scale tooany type of secret, not just connection string.</span></span>

    <span data-ttu-id="5d06c-520">Há uma solução mais fácil (mas não uma boa prática): pode criar um **serviço ligado de SQL do Azure** com as definições de cadeia de ligação, criar um conjunto de dados que utiliza Olá serviço ligado e o conjunto de dados de cadeia Olá como um conjunto de dados de entrada fictício atividade de .NET personalizada toohello.</span><span class="sxs-lookup"><span data-stu-id="5d06c-520">There is an easier workaround (but not a best practice): you can create an **Azure SQL linked service** with connection string settings, create a dataset that uses hello linked service, and chain hello dataset as a dummy input dataset toohello custom .NET activity.</span></span> <span data-ttu-id="5d06c-521">Pode, em seguida, Olá de acesso associados a cadeia de ligação do serviço no código de atividade personalizado Olá e deverão funcionar ajustar no tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="5d06c-521">You can then access hello linked service's connection string in hello custom activity code and it should work fine at runtime.</span></span>  

#### <a name="extend-hello-sample"></a><span data-ttu-id="5d06c-522">Expandir o exemplo de Olá</span><span class="sxs-lookup"><span data-stu-id="5d06c-522">Extend hello sample</span></span>
<span data-ttu-id="5d06c-523">Pode expandir este exemplo toolearn mais informações sobre as funcionalidades do Azure Data Factory e do Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="5d06c-523">You can extend this sample toolearn more about Azure Data Factory and Azure Batch features.</span></span> <span data-ttu-id="5d06c-524">Por exemplo, Olá tooprocess setores um intervalo de hora diferente, os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="5d06c-524">For example, tooprocess slices in a different time range, do hello following steps:</span></span>

1. <span data-ttu-id="5d06c-525">Adicionar Olá seguir subpastas na Olá `inputfolder`: 2015-11-16-05, 2015-11-16-06 201-11-16-07, 2011-11-16-08, 2015-11-16-09 e coloque ficheiros de entrada nessas pastas.</span><span class="sxs-lookup"><span data-stu-id="5d06c-525">Add hello following subfolders in hello `inputfolder`: 2015-11-16-05, 2015-11-16-06, 201-11-16-07, 2011-11-16-08, 2015-11-16-09 and place input files in those folders.</span></span> <span data-ttu-id="5d06c-526">Alterar a hora de fim do pipeline de Olá do Olá `2015-11-16T05:00:00Z` demasiado`2015-11-16T10:00:00Z`.</span><span class="sxs-lookup"><span data-stu-id="5d06c-526">Change hello end time for hello pipeline from `2015-11-16T05:00:00Z` too`2015-11-16T10:00:00Z`.</span></span> <span data-ttu-id="5d06c-527">No Olá **vista de diagrama**, faça duplo clique em Olá **InputDataset**e confirme que os setores de entrada Olá estão prontos.</span><span class="sxs-lookup"><span data-stu-id="5d06c-527">In hello **Diagram View**, double-click hello **InputDataset**, and confirm that hello input slices are ready.</span></span> <span data-ttu-id="5d06c-528">Faça duplo clique em **OuptutDataset** toosee Estado Olá setores de saída.</span><span class="sxs-lookup"><span data-stu-id="5d06c-528">Double-click **OuptutDataset** toosee hello state of output slices.</span></span> <span data-ttu-id="5d06c-529">Se forem no estado pronto, verifique a pasta de saída de Olá para ficheiros de saída Olá.</span><span class="sxs-lookup"><span data-stu-id="5d06c-529">If they are in Ready state, check hello output folder for hello output files.</span></span>
2. <span data-ttu-id="5d06c-530">Aumentar ou diminuir Olá **simultaneidade** definição toounderstand a forma como os afeta o desempenho de Olá da sua solução, especialmente Olá processamento que ocorre no Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="5d06c-530">Increase or decrease hello **concurrency** setting toounderstand how it affects hello performance of your solution, especially hello processing that occurs on Azure Batch.</span></span> <span data-ttu-id="5d06c-531">(Consulte o passo 4: criar e executar o pipeline de Olá para obter mais informações sobre Olá **simultaneidade** definição.)</span><span class="sxs-lookup"><span data-stu-id="5d06c-531">(See Step 4: Create and run hello pipeline for more on hello **concurrency** setting.)</span></span>
3. <span data-ttu-id="5d06c-532">Criar um conjunto com maior/menor **máximo de tarefas por VM**.</span><span class="sxs-lookup"><span data-stu-id="5d06c-532">Create a pool with higher/lower **Maximum tasks per VM**.</span></span> <span data-ttu-id="5d06c-533">toouse Olá novo conjunto que criou, Olá de atualização de serviço ligado do Azure Batch na solução de fábrica de dados de Olá.</span><span class="sxs-lookup"><span data-stu-id="5d06c-533">toouse hello new pool you created, update hello Azure Batch linked service in hello Data Factory solution.</span></span> <span data-ttu-id="5d06c-534">(Consulte o passo 4: criar e executar o pipeline de Olá para obter mais informações sobre Olá **máximo de tarefas por VM** definição.)</span><span class="sxs-lookup"><span data-stu-id="5d06c-534">(See Step 4: Create and run hello pipeline for more on hello **Maximum tasks per VM** setting.)</span></span>
4. <span data-ttu-id="5d06c-535">Criar um conjunto do Azure Batch com **dimensionamento automático** funcionalidade.</span><span class="sxs-lookup"><span data-stu-id="5d06c-535">Create an Azure Batch pool with **autoscale** feature.</span></span> <span data-ttu-id="5d06c-536">Dimensionar automaticamente nós de computação num conjunto do Azure Batch é ajustamento dinâmico do Olá do processamento de energia utilizada pela sua aplicação.</span><span class="sxs-lookup"><span data-stu-id="5d06c-536">Automatically scaling compute nodes in an Azure Batch pool is hello dynamic adjustment of processing power used by your application.</span></span> 

    <span data-ttu-id="5d06c-537">fórmula de exemplo de Olá aqui distribui Olá seguinte comportamento: quando o conjunto de Olá for criado inicialmente, começa com 1 VM.</span><span class="sxs-lookup"><span data-stu-id="5d06c-537">hello sample formula here achieves hello following behavior: When hello pool is initially created, it starts with 1 VM.</span></span> <span data-ttu-id="5d06c-538">Métrica de $PendingTasks define o número de Olá das tarefas em execução + Active Directory (em fila) Estado.</span><span class="sxs-lookup"><span data-stu-id="5d06c-538">$PendingTasks metric defines hello number of tasks in running + active (queued) state.</span></span>  <span data-ttu-id="5d06c-539">a fórmula Olá localiza Olá o número médio de tarefas pendentes na Olá último segundos 180 e define TargetDedicated em conformidade.</span><span class="sxs-lookup"><span data-stu-id="5d06c-539">hello formula finds hello average number of pending tasks in hello last 180 seconds and sets TargetDedicated accordingly.</span></span> <span data-ttu-id="5d06c-540">Garante que nunca chegam TargetDedicated para além de 25 VMs.</span><span class="sxs-lookup"><span data-stu-id="5d06c-540">It ensures that TargetDedicated never goes beyond 25 VMs.</span></span> <span data-ttu-id="5d06c-541">Por isso, são submetidas novas tarefas, agrupamento automaticamente o crescimentos e as tarefas são concluídas, as VMs fiquem livre um a um e o dimensionamento automático de Olá diminui dessas VMs.</span><span class="sxs-lookup"><span data-stu-id="5d06c-541">So, as new tasks are submitted, pool automatically grows and as tasks complete, VMs become free one by one and hello autoscaling shrinks those VMs.</span></span> <span data-ttu-id="5d06c-542">startingNumberOfVMs e maxNumberofVMs podem ser ajustada tooyour necessidades.</span><span class="sxs-lookup"><span data-stu-id="5d06c-542">startingNumberOfVMs and maxNumberofVMs can be adjusted tooyour needs.</span></span>
 
    <span data-ttu-id="5d06c-543">Fórmula de dimensionamento automático:</span><span class="sxs-lookup"><span data-stu-id="5d06c-543">Autoscale formula:</span></span>

    ``` 
    startingNumberOfVMs = 1;
    maxNumberofVMs = 25;
    pendingTaskSamplePercent = $PendingTasks.GetSamplePercent(180 * TimeInterval_Second);
    pendingTaskSamples = pendingTaskSamplePercent < 70 ? startingNumberOfVMs : avg($PendingTasks.GetSample(180 * TimeInterval_Second));
    $TargetDedicated=min(maxNumberofVMs,pendingTaskSamples);
    ```

   <span data-ttu-id="5d06c-544">Consulte [automaticamente Dimensionar nós de computação num conjunto do Azure Batch](../batch/batch-automatic-scaling.md) para obter mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="5d06c-544">See [Automatically scale compute nodes in an Azure Batch pool](../batch/batch-automatic-scaling.md) for details.</span></span>

   <span data-ttu-id="5d06c-545">Se o conjunto de Olá estiver a utilizar predefinição de Olá [autoScaleEvaluationInterval](https://msdn.microsoft.com/library/azure/dn820173.aspx), Olá serviço Batch pode demorar 15-30 minutos tooprepare Olá VM antes de executar a atividade personalizada Olá.</span><span class="sxs-lookup"><span data-stu-id="5d06c-545">If hello pool is using hello default [autoScaleEvaluationInterval](https://msdn.microsoft.com/library/azure/dn820173.aspx), hello Batch service could take 15-30 minutes tooprepare hello VM before running hello custom activity.</span></span>  <span data-ttu-id="5d06c-546">Se o conjunto de Olá estiver a utilizar um autoScaleEvaluationInterval diferentes, Olá serviço Batch pode demorar autoScaleEvaluationInterval + 10 minutos.</span><span class="sxs-lookup"><span data-stu-id="5d06c-546">If hello pool is using a different autoScaleEvaluationInterval, hello Batch service could take autoScaleEvaluationInterval + 10 minutes.</span></span>
5. <span data-ttu-id="5d06c-547">Na solução de exemplo de Olá, Olá **executar** invoca o método Olá **Calculate** método que processe um tooproduce de setor de dados de entrada um setor de dados de saída.</span><span class="sxs-lookup"><span data-stu-id="5d06c-547">In hello sample solution, hello **Execute** method invokes hello **Calculate** method that processes an input data slice tooproduce an output data slice.</span></span> <span data-ttu-id="5d06c-548">Pode escrever o seu próprio método tooprocess dados de entrada e substitua chamada de método Calculate Olá no método de execução de Olá com um método de tooyour de chamada.</span><span class="sxs-lookup"><span data-stu-id="5d06c-548">You can write your own method tooprocess input data and replace hello Calculate method call in hello Execute method with a call tooyour method.</span></span>

### <a name="next-steps-consume-hello-data"></a><span data-ttu-id="5d06c-549">Próximos passos: consumir dados Olá</span><span class="sxs-lookup"><span data-stu-id="5d06c-549">Next steps: Consume hello data</span></span>
<span data-ttu-id="5d06c-550">Depois de processar dados, pode consumi-lo com ferramentas online como **Microsoft Power BI**.</span><span class="sxs-lookup"><span data-stu-id="5d06c-550">After you process data, you can consume it with online tools like **Microsoft Power BI**.</span></span> <span data-ttu-id="5d06c-551">Seguem-se toohelp ligações compreender o Power BI e como toouse-lo no Azure:</span><span class="sxs-lookup"><span data-stu-id="5d06c-551">Here are links toohelp you understand Power BI and how toouse it in Azure:</span></span>

* [<span data-ttu-id="5d06c-552">Explore um conjunto de dados no Power BI</span><span class="sxs-lookup"><span data-stu-id="5d06c-552">Explore a dataset in Power BI</span></span>](https://powerbi.microsoft.com/documentation/powerbi-service-get-data/)
* [<span data-ttu-id="5d06c-553">Introdução ao hello do Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="5d06c-553">Getting started with hello Power BI Desktop</span></span>](https://powerbi.microsoft.com/documentation/powerbi-desktop-getting-started/)
* [<span data-ttu-id="5d06c-554">Atualizar dados no Power BI</span><span class="sxs-lookup"><span data-stu-id="5d06c-554">Refresh data in Power BI</span></span>](https://powerbi.microsoft.com/documentation/powerbi-refresh-data/)
* [<span data-ttu-id="5d06c-555">Azure e o Power BI - descrição geral básica</span><span class="sxs-lookup"><span data-stu-id="5d06c-555">Azure and Power BI - basic overview</span></span>](https://powerbi.microsoft.com/documentation/powerbi-azure-and-power-bi/)

## <a name="references"></a><span data-ttu-id="5d06c-556">Referências</span><span class="sxs-lookup"><span data-stu-id="5d06c-556">References</span></span>
* [<span data-ttu-id="5d06c-557">Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="5d06c-557">Azure Data Factory</span></span>](https://azure.microsoft.com/documentation/services/data-factory/)

  * [<span data-ttu-id="5d06c-558">Introdução tooAzure serviço Data Factory</span><span class="sxs-lookup"><span data-stu-id="5d06c-558">Introduction tooAzure Data Factory service</span></span>](data-factory-introduction.md)
  * [<span data-ttu-id="5d06c-559">Introdução ao Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="5d06c-559">Get started with Azure Data Factory</span></span>](data-factory-build-your-first-pipeline.md)
  * [<span data-ttu-id="5d06c-560">Utilizar atividades personalizadas num pipeline do Azure Data Factory (Use custom activities in an Azure Data Factory pipeline)</span><span class="sxs-lookup"><span data-stu-id="5d06c-560">Use custom activities in an Azure Data Factory pipeline</span></span>](data-factory-use-custom-activities.md)
* [<span data-ttu-id="5d06c-561">O Azure Batch</span><span class="sxs-lookup"><span data-stu-id="5d06c-561">Azure Batch</span></span>](https://azure.microsoft.com/documentation/services/batch/)

  * [<span data-ttu-id="5d06c-562">Noções básicas do Azure Batch</span><span class="sxs-lookup"><span data-stu-id="5d06c-562">Basics of Azure Batch</span></span>](../batch/batch-technical-overview.md)
  * [<span data-ttu-id="5d06c-563">Descrição geral das funcionalidades do Azure Batch</span><span class="sxs-lookup"><span data-stu-id="5d06c-563">Overview of Azure Batch features</span></span>](../batch/batch-api-basics.md)
  * [<span data-ttu-id="5d06c-564">Criar e gerir a conta do Azure Batch no portal do Azure de Olá</span><span class="sxs-lookup"><span data-stu-id="5d06c-564">Create and manage Azure Batch account in hello Azure portal</span></span>](../batch/batch-account-create-portal.md)
  * [<span data-ttu-id="5d06c-565">Introdução à biblioteca .NET do Azure Batch</span><span class="sxs-lookup"><span data-stu-id="5d06c-565">Get started with Azure Batch Library .NET</span></span>](../batch/batch-dotnet-get-started.md)

[batch-explorer]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/BatchExplorer
[batch-explorer-walkthrough]: http://blogs.technet.com/b/windowshpc/archive/2015/01/20/azure-batch-explorer-sample-walkthrough.aspx
