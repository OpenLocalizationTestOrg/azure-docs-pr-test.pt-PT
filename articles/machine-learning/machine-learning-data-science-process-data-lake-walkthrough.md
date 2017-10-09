---
title: "Dimensionável ciência de dados com o Azure Data Lake: uma instruções ponto a ponto | Microsoft Docs"
description: "Como as tarefas toouse do Azure Data Lake toodo exploração e binary classificação de dados num conjunto de dados."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 91a8207f-1e57-4570-b7fc-7c5fa858ffeb
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/30/2017
ms.author: bradsev;weig
ms.openlocfilehash: 8b05457ae7045a7aaed350a7502469f2247161e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="scalable-data-science-with-azure-data-lake-an-end-to-end-walkthrough"></a><span data-ttu-id="0b1aa-103">Dimensionável ciência de dados com o Azure Data Lake: uma instruções ponto a ponto</span><span class="sxs-lookup"><span data-stu-id="0b1aa-103">Scalable Data Science with Azure Data Lake: An end-to-end Walkthrough</span></span>
<span data-ttu-id="0b1aa-104">Estas instruções mostram como tarefas de classificação binária de uma amostra de Olá NYC e exploração de dados do toouse do Azure Data Lake toodo taxi viagem e fare toopredict de conjunto de dados ou não uma sugestão será paga por um fare.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-104">This walkthrough shows how toouse Azure Data Lake toodo data exploration and binary classification tasks on a sample of hello NYC taxi trip and fare dataset toopredict whether or not a tip will be paid by a fare.</span></span> <span data-ttu-id="0b1aa-105">-Orienta-o pelos passos de Olá da Olá [o processo de ciência de dados de equipa](http://aka.ms/datascienceprocess)ponto-a- ponto, formação de toomodel de aquisição de dados e, em seguida, toohello implementação de um serviço web que publica modelo Olá.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-105">It walks you through hello steps of hello [Team Data Science Process](http://aka.ms/datascienceprocess), end-to-end, from data acquisition toomodel training, and then toohello deployment of a web service that publishes hello model.</span></span>

### <a name="azure-data-lake-analytics"></a><span data-ttu-id="0b1aa-106">Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="0b1aa-106">Azure Data Lake Analytics</span></span>
<span data-ttu-id="0b1aa-107">Olá [Microsoft Azure Data Lake](https://azure.microsoft.com/solutions/data-lake/) tem todos os Olá capacidades necessárias toomake-lo mais fácil para os dados de toostore cientistas de dados de qualquer tamanho, forma e velocidade e tooconduct o processamento de dados, análise e modelação de aprendizagem máquina avançadas com elevada escalabilidade de forma económica.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-107">hello [Microsoft Azure Data Lake](https://azure.microsoft.com/solutions/data-lake/) has all hello capabilities required toomake it easy for data scientists toostore data of any size, shape and speed, and tooconduct data processing, advanced analytics, and machine learning modeling with high scalability in a cost-effective way.</span></span>   <span data-ttu-id="0b1aa-108">Paga numa base por tarefa, apenas quando os dados, na verdade, está a ser processados.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-108">You pay on a per-job basis, only when data is actually being processed.</span></span> <span data-ttu-id="0b1aa-109">Azure Data Lake Analytics inclui U-SQL, uma linguagem que blends Olá natureza declarativa do SQL Server com Olá poder expressivo do c# tooprovide escalável distribuído a capacidade de consulta.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-109">Azure Data Lake Analytics includes U-SQL, a language that blends hello declarative nature of SQL with hello expressive power of C# tooprovide scalable distributed query capability.</span></span> <span data-ttu-id="0b1aa-110">Permite-lhe tooprocess lógica personalizada de inserção de dados não estruturados aplicando esquema na leitura, e definidos pelo utilizador (UDFs) de funções e inclui extensibilidade tooenable bem detalhada controlo sobre como tooexecute à escala.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-110">It enables you tooprocess unstructured data by applying schema on read, insert custom logic and user defined functions (UDFs), and includes extensibility tooenable fine grained control over how tooexecute at scale.</span></span> <span data-ttu-id="0b1aa-111">toolearn mais informações sobre philosophy de estrutura de Olá atrás U-SQL, consulte [mensagem de blogue do Visual Studio](https://blogs.msdn.microsoft.com/visualstudio/2015/09/28/introducing-u-sql-a-language-that-makes-big-data-processing-easy/).</span><span class="sxs-lookup"><span data-stu-id="0b1aa-111">toolearn more about hello design philosophy behind U-SQL, see [Visual Studio blog post](https://blogs.msdn.microsoft.com/visualstudio/2015/09/28/introducing-u-sql-a-language-that-makes-big-data-processing-easy/).</span></span>

<span data-ttu-id="0b1aa-112">O Data Lake Analytics também é uma parte essencial do Cortana Analytics Suite e funciona com o Azure SQL Data Warehouse, o Power BI e o Data Factory.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-112">Data Lake Analytics is also a key part of Cortana Analytics Suite and works with Azure SQL Data Warehouse, Power BI, and Data Factory.</span></span> <span data-ttu-id="0b1aa-113">Isto dá-lhe uma plataforma de análise avançada e macrodados completa de nuvem.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-113">This gives you a complete cloud big data and advanced analytics platform.</span></span>

<span data-ttu-id="0b1aa-114">Estas instruções começa por que descrevem os pré-requisitos de Olá e recursos que são necessários toocomplete Olá tarefas de Data Lake Analytics que formam o processo de ciência de dados de Olá e como tooinstall-los.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-114">This walkthrough begins by describing hello prerequisites and resources that are needed toocomplete hello tasks with Data Lake Analytics that form hello data science process and how tooinstall them.</span></span> <span data-ttu-id="0b1aa-115">Em seguida, que descreve os passos de processamento de dados de Olá utilizando U-SQL e conclui mostrando como toouse Python e o Hive com o Azure Machine Learning Studio toobuild e implementar modelos preditivos Olá.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-115">Then it outlines hello data processing steps using U-SQL and concludes by showing how toouse Python and Hive with Azure Machine Learning Studio toobuild and deploy hello predictive models.</span></span> 

### <a name="u-sql-and-visual-studio"></a><span data-ttu-id="0b1aa-116">U-SQL e o Visual Studio</span><span class="sxs-lookup"><span data-stu-id="0b1aa-116">U-SQL and Visual Studio</span></span>
<span data-ttu-id="0b1aa-117">Estas instruções recomenda a utilização de conjunto de dados do Visual Studio tooedit U-SQL scripts tooprocess Olá.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-117">This walkthrough recommends using Visual Studio tooedit U-SQL scripts tooprocess hello dataset.</span></span> <span data-ttu-id="0b1aa-118">Olá scripts U-SQL são descritas aqui e fornecidos num ficheiro separado.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-118">hello U-SQL scripts are described here and provided in a separate file.</span></span> <span data-ttu-id="0b1aa-119">processo de Olá inclui ingestão relacionadas, explorar e fazendo a amostragem de dados de Olá.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-119">hello process includes ingesting, exploring, and sampling hello data.</span></span> <span data-ttu-id="0b1aa-120">Também mostra como criar tarefa a partir do portal do Azure de Olá um script toorun U-SQL.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-120">It also shows how toorun a U-SQL scripted job from hello Azure portal.</span></span> <span data-ttu-id="0b1aa-121">As tabelas do Hive são criadas para os dados de Olá num associados edifício de Olá do toofacilitate de cluster do HDInsight e uma implementação de um modelo de classificação binária no Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-121">Hive tables are created for hello data in an associated HDInsight cluster toofacilitate hello building and deployment of a binary classification model in Azure Machine Learning Studio.</span></span>  

### <a name="python"></a><span data-ttu-id="0b1aa-122">Python</span><span class="sxs-lookup"><span data-stu-id="0b1aa-122">Python</span></span>
<span data-ttu-id="0b1aa-123">Estas instruções também contém uma secção que mostra como toobuild e implementar um modelo preditivo com o Python no Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-123">This walkthrough also contains a section that shows how toobuild and deploy a predictive model using Python with Azure Machine Learning Studio.</span></span>  <span data-ttu-id="0b1aa-124">Fornecemos um bloco de notas do Jupyter com scripts do Python Olá para estes passos neste processo.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-124">We provide a Jupyter notebook with hello Python scripts for these steps in this process.</span></span> <span data-ttu-id="0b1aa-125">Bloco de notas do Olá inclui código para alguns passos engenharia da funcionalidade adicional e a construção de modelos, tais como a classificação de várias classes e regressão modelação, além disso, modelo de classificação binária toohello aqui descrito.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-125">hello notebook includes code for some additional feature engineering steps and models construction such as multiclass classification and regression modeling in addition toohello binary classification model outlined here.</span></span> <span data-ttu-id="0b1aa-126">tarefa de regressão Olá é a quantidade de Olá de toopredict de sugestão de Olá com base nas outras funcionalidades de sugestão.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-126">hello regression task is toopredict hello amount of hello tip based on other tip features.</span></span> 

### <a name="azure-machine-learning"></a><span data-ttu-id="0b1aa-127">Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="0b1aa-127">Azure Machine Learning</span></span>
<span data-ttu-id="0b1aa-128">Azure Machine Learning Studio é toobuild utilizado e implementar modelos preditivos Olá.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-128">Azure Machine Learning Studio is used toobuild and deploy hello predictive models.</span></span> <span data-ttu-id="0b1aa-129">Isto é feito utilizando duas abordagens: primeiro com Python scripts e, em seguida, com as tabelas do Hive num cluster do HDInsight (Hadoop).</span><span class="sxs-lookup"><span data-stu-id="0b1aa-129">This is done using two approaches: first with Python scripts and then with Hive tables on an HDInsight (Hadoop) cluster.</span></span>

### <a name="scripts"></a><span data-ttu-id="0b1aa-130">Scripts</span><span class="sxs-lookup"><span data-stu-id="0b1aa-130">Scripts</span></span>
<span data-ttu-id="0b1aa-131">Apenas Olá principal passos descritos nesta explicação passo a passo.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-131">Only hello principal steps are outlined in this walkthrough.</span></span> <span data-ttu-id="0b1aa-132">Pode transferir Olá completa **script U-SQL** e **bloco de notas do Jupyter** de [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/AzureDataLakeWalkthrough).</span><span class="sxs-lookup"><span data-stu-id="0b1aa-132">You can download hello full **U-SQL script** and **Jupyter Notebook** from [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/AzureDataLakeWalkthrough).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0b1aa-133">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="0b1aa-133">Prerequisites</span></span>
<span data-ttu-id="0b1aa-134">Antes de iniciar estes tópicos, tem de ter o seguinte Olá:</span><span class="sxs-lookup"><span data-stu-id="0b1aa-134">Before you begin these topics, you must have hello following:</span></span>

* <span data-ttu-id="0b1aa-135">Uma subscrição do Azure.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-135">An Azure subscription.</span></span> <span data-ttu-id="0b1aa-136">Se já tiver uma, consulte [avaliação gratuita do Azure obter](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="0b1aa-136">If you do not already have one, see [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="0b1aa-137">[Recomendado] Visual Studio 2013 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-137">[Recommended] Visual Studio 2013 or later.</span></span> <span data-ttu-id="0b1aa-138">Se já tiver um estas versões instaladas, pode transferir uma versão de Comunidade gratuita de [Visual Studio Community](https://www.visualstudio.com/vs/community/).</span><span class="sxs-lookup"><span data-stu-id="0b1aa-138">If you do not already have one of these versions installed, you can download a free Community version from [Visual Studio Community](https://www.visualstudio.com/vs/community/).</span></span>

> [!NOTE]
> <span data-ttu-id="0b1aa-139">Em vez do Visual Studio, também pode utilizar consultas de Azure Data Lake toosubmit do Olá Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-139">Instead of Visual Studio, you can also use hello Azure Portal toosubmit Azure Data Lake queries.</span></span> <span data-ttu-id="0b1aa-140">Iremos irá fornecer instruções sobre como toodo, por isso, com o Visual Studio e no portal de Olá na secção de Olá intitulada **processar os dados com o U-SQL**.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-140">We will provide instructions on how toodo so both with Visual Studio and on hello portal in hello section titled **Process data with U-SQL**.</span></span> 
> 
> 


## <a name="prepare-data-science-environment-for-azure-data-lake"></a><span data-ttu-id="0b1aa-141">Preparar o ambiente de ciência de dados para o Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="0b1aa-141">Prepare data science environment for Azure Data Lake</span></span>
<span data-ttu-id="0b1aa-142">ambiente de ciência de tooprepare Olá dados nestas instruções, criar Olá os seguintes recursos:</span><span class="sxs-lookup"><span data-stu-id="0b1aa-142">tooprepare hello data science environment for this walkthrough, create hello following resources:</span></span>

* <span data-ttu-id="0b1aa-143">O Azure Data Lake Store (ADLS)</span><span class="sxs-lookup"><span data-stu-id="0b1aa-143">Azure Data Lake Store (ADLS)</span></span> 
* <span data-ttu-id="0b1aa-144">Análise do Azure Data Lake (ADLA)</span><span class="sxs-lookup"><span data-stu-id="0b1aa-144">Azure Data Lake Analytics (ADLA)</span></span>
* <span data-ttu-id="0b1aa-145">Conta de armazenamento de Blobs do Azure</span><span class="sxs-lookup"><span data-stu-id="0b1aa-145">Azure Blob storage account</span></span>
* <span data-ttu-id="0b1aa-146">Conta do Azure Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="0b1aa-146">Azure Machine Learning Studio account</span></span>
* <span data-ttu-id="0b1aa-147">Ferramentas do Azure Data Lake para Visual Studio (recomendado)</span><span class="sxs-lookup"><span data-stu-id="0b1aa-147">Azure Data Lake Tools for Visual Studio (Recommended)</span></span>

<span data-ttu-id="0b1aa-148">Esta secção fornece instruções sobre como toocreate destes recursos.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-148">This section provides instructions on how toocreate each of these resources.</span></span> <span data-ttu-id="0b1aa-149">Se optar por toouse as tabelas do Hive com o Azure Machine Learning, em vez de Python, toobuild um modelo, terá também de tooprovision um cluster do HDInsight (Hadoop).</span><span class="sxs-lookup"><span data-stu-id="0b1aa-149">If you choose toouse Hive tables with Azure Machine Learning, instead of Python, toobuild a model,you will also need tooprovision an HDInsight (Hadoop) cluster.</span></span> <span data-ttu-id="0b1aa-150">Este procedimento alternativo descritos na secção adequada Olá abaixo.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-150">This alternative procedure in described in hello appropriate section below.</span></span>


> [!NOTE]
> <span data-ttu-id="0b1aa-151">Olá **Azure Data Lake Store** pode ser criado em separado ou quando criar Olá **Azure Data Lake Analytics** como armazenamento de predefinido Olá.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-151">hello **Azure Data Lake Store** can be created either separately or when you create hello **Azure Data Lake Analytics** as hello default storage.</span></span> <span data-ttu-id="0b1aa-152">São referenciadas instruções para criar cada um destes recursos separadamente abaixo, mas Olá conta de armazenamento do Data Lake não precisa de ser criada em separado.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-152">Instructions are referenced for creating each of these resources separately below, but hello Data Lake storage account need not be created separately.</span></span>
>
> 

### <a name="create-an-azure-data-lake-store"></a><span data-ttu-id="0b1aa-153">Criar um Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="0b1aa-153">Create an Azure Data Lake Store</span></span>


<span data-ttu-id="0b1aa-154">Criar um ADLS de Olá [Portal do Azure](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="0b1aa-154">Create an ADLS from hello [Azure Portal](http://portal.azure.com).</span></span> <span data-ttu-id="0b1aa-155">Para obter mais informações, consulte [criar um cluster do HDInsight com o Data Lake Store utilizando o Portal do Azure](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="0b1aa-155">For details, see [Create an HDInsight cluster with Data Lake Store using Azure Portal](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span></span> <span data-ttu-id="0b1aa-156">Ser tooset se segurança Olá identidade AAD do Cluster no Olá **DataSource** painel de Olá **configuração opcional** painel descrito não existe.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-156">Be sure tooset up hello Cluster AAD Identity in hello **DataSource** blade of hello **Optional Configuration** blade described there.</span></span> 

 ![3](./media/machine-learning-data-science-process-data-lake-walkthrough/3-create-ADLS.PNG)

### <a name="create-an-azure-data-lake-analytics-account"></a><span data-ttu-id="0b1aa-158">Criar uma conta do Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="0b1aa-158">Create an Azure Data Lake Analytics account</span></span>
<span data-ttu-id="0b1aa-159">Criar uma conta ADLA de Olá [Portal do Azure](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="0b1aa-159">Create an ADLA account from hello [Azure Portal](http://portal.azure.com).</span></span> <span data-ttu-id="0b1aa-160">Para obter mais informações, consulte [Tutorial: introdução ao Azure Data Lake Analytics com o Portal do Azure](../data-lake-analytics/data-lake-analytics-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="0b1aa-160">For details, see [Tutorial: get started with Azure Data Lake Analytics using Azure Portal](../data-lake-analytics/data-lake-analytics-get-started-portal.md).</span></span> 

 ![4](./media/machine-learning-data-science-process-data-lake-walkthrough/4-create-ADLA-new.PNG)

### <a name="create-an-azure-blob-storage-account"></a><span data-ttu-id="0b1aa-162">Criar uma conta de armazenamento de Blobs do Azure</span><span class="sxs-lookup"><span data-stu-id="0b1aa-162">Create an Azure Blob storage account</span></span>
<span data-ttu-id="0b1aa-163">Criar uma conta de armazenamento de Blobs do Azure a partir de Olá [Portal do Azure](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="0b1aa-163">Create an Azure Blob storage account from hello [Azure Portal](http://portal.azure.com).</span></span> <span data-ttu-id="0b1aa-164">Para obter mais informações, consulte Olá criar uma conta de armazenamento secção [contas do storage do Azure sobre](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="0b1aa-164">For details, see hello Create a storage account section in [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span>

 ![5](./media/machine-learning-data-science-process-data-lake-walkthrough/5-Create-Azure-Blob.PNG)

### <a name="set-up-an-azure-machine-learning-studio-account"></a><span data-ttu-id="0b1aa-166">Configure uma conta do Azure Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="0b1aa-166">Set up an Azure Machine Learning Studio account</span></span>
<span data-ttu-id="0b1aa-167">A sessão de cópia de segurança/no Azure Machine Learning Studio a partir de Olá [Azure Machine Learning](https://azure.microsoft.com/services/machine-learning/) página.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-167">Sign up/into Azure Machine Learning Studio from hello [Azure Machine Learning](https://azure.microsoft.com/services/machine-learning/) page.</span></span> <span data-ttu-id="0b1aa-168">Clique em Olá **começar agora** botão e, em seguida, escolha um "Área de trabalho gratuita" ou "Área de trabalho Standard".</span><span class="sxs-lookup"><span data-stu-id="0b1aa-168">Click on hello **Get started now** button and then choose a "Free Workspace" or "Standard Workspace".</span></span> <span data-ttu-id="0b1aa-169">Após este será capaz de toocreate experimentações no Azure ML Studio.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-169">After this you will be able toocreate experiments in Azure ML Studio.</span></span>  

### <a name="install-azure-data-lake-tools-recommended"></a><span data-ttu-id="0b1aa-170">Instale o ferramentas do Azure Data Lake [Recomendado]</span><span class="sxs-lookup"><span data-stu-id="0b1aa-170">Install Azure Data Lake Tools [Recommended]</span></span>
<span data-ttu-id="0b1aa-171">Instalar o Azure Data Lake Tools para a sua versão do Visual Studio do [ferramentas do Azure Data Lake para Visual Studio](https://www.microsoft.com/download/details.aspx?id=49504).</span><span class="sxs-lookup"><span data-stu-id="0b1aa-171">Install Azure Data Lake Tools for your version of Visual Studio from [Azure Data Lake Tools for Visual Studio](https://www.microsoft.com/download/details.aspx?id=49504).</span></span>

 ![6](./media/machine-learning-data-science-process-data-lake-walkthrough/6-install-ADL-tools-VS.PNG)

<span data-ttu-id="0b1aa-173">Após a conclusão com êxito da instalação de Olá, abra Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-173">After hello installation finishes successfully, open up Visual Studio.</span></span> <span data-ttu-id="0b1aa-174">Deverá ver o menu Olá de separador de Data Lake do Olá na parte superior do Olá.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-174">You should see hello Data Lake tab hello menu at hello top.</span></span> <span data-ttu-id="0b1aa-175">Os recursos do Azure devem aparecer no painel esquerdo Olá ao iniciar sessão na sua conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-175">Your Azure resources should appear in hello left panel when you sign into your Azure account.</span></span>

 ![7](./media/machine-learning-data-science-process-data-lake-walkthrough/7-install-ADL-tools-VS-done.PNG)

## <a name="hello-nyc-taxi-trips-dataset"></a><span data-ttu-id="0b1aa-177">o conjunto de dados do Olá NYC Taxi viagens</span><span class="sxs-lookup"><span data-stu-id="0b1aa-177">hello NYC Taxi Trips dataset</span></span>
<span data-ttu-id="0b1aa-178">Olá conjunto de dados é utilizado aqui é um conjunto de dados publicamente disponível – hello [NYC Taxi viagens dataset](http://www.andresmh.com/nyctaxitrips/).</span><span class="sxs-lookup"><span data-stu-id="0b1aa-178">hello data set we used here is a publicly available dataset -- hello [NYC Taxi Trips dataset](http://www.andresmh.com/nyctaxitrips/).</span></span> <span data-ttu-id="0b1aa-179">Olá dados NYC Taxi viagem consiste em cerca de 20GB de ficheiros CSV comprimidos (GB de ~ 48 descomprimido), mais de 173 milhões de gravação viagens individuais e Olá fares paga para cada viagem.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-179">hello NYC Taxi Trip data consists of about 20GB of compressed CSV files (~48GB uncompressed), recording more than 173 million individual trips and hello fares paid for each trip.</span></span> <span data-ttu-id="0b1aa-180">Cada registo viagem inclui localizações de recolha e drop-off Olá e vezes, são anónimos hack número de licença (controlador) e Olá número medallion (id exclusivo do taxi).</span><span class="sxs-lookup"><span data-stu-id="0b1aa-180">Each trip record includes hello pickup and drop-off locations and times, anonymized hack (driver's) license number, and hello medallion (taxi’s unique id) number.</span></span> <span data-ttu-id="0b1aa-181">dados Olá abrange todos os viagens no ano de Olá 2013 e são fornecidos na Olá seguir dois conjuntos de dados de cada mês:</span><span class="sxs-lookup"><span data-stu-id="0b1aa-181">hello data covers all trips in hello year 2013 and is provided in hello following two datasets for each month:</span></span>

* <span data-ttu-id="0b1aa-182">Olá 'trip_data' CSV contém detalhes viagem, tais como o número de passageiros, recolha e dropoff pontos, duração de viagem e comprimento viagem.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-182">hello 'trip_data' CSV contains trip details, such as number of passengers, pickup and dropoff points, trip duration, and trip length.</span></span> <span data-ttu-id="0b1aa-183">Seguem-se alguns registos de exemplo:</span><span class="sxs-lookup"><span data-stu-id="0b1aa-183">Here are a few sample records:</span></span>
  
       medallion,hack_license,vendor_id,rate_code,store_and_fwd_flag,pickup_datetime,dropoff_datetime,passenger_count, trip_time_in_secs,trip_distance,pickup_longitude,pickup_latitude,dropoff_longitude,dropoff_latitude
       89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,1,N,2013-01-01 15:11:48,2013-01-01 15:18:10,4,382,1.00,-73.978165,40.757977,-73.989838,40.751171
       0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-06 00:18:35,2013-01-06 00:22:54,1,259,1.50,-74.006683,40.731781,-73.994499,40.75066
       0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-05 18:49:41,2013-01-05 18:54:23,1,282,1.10,-74.004707,40.73777,-74.009834,40.726002
       DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:54:15,2013-01-07 23:58:20,2,244,.70,-73.974602,40.759945,-73.984734,40.759388
       DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:25:03,2013-01-07 23:34:24,1,560,2.10,-73.97625,40.748528,-74.002586,40.747868
* <span data-ttu-id="0b1aa-184">Olá 'trip_fare' CSV contém detalhes de fare Olá paga para cada viagem, tais como o tipo de pagamento, a quantidade de fare, surcharge e taxas, sugestões e tolls e quantidade total de Olá paga.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-184">hello 'trip_fare' CSV contains details of hello fare paid for each trip, such as payment type, fare amount, surcharge and taxes, tips and tolls, and hello total amount paid.</span></span> <span data-ttu-id="0b1aa-185">Seguem-se alguns registos de exemplo:</span><span class="sxs-lookup"><span data-stu-id="0b1aa-185">Here are a few sample records:</span></span>
  
       medallion, hack_license, vendor_id, pickup_datetime, payment_type, fare_amount, surcharge, mta_tax, tip_amount, tolls_amount, total_amount
       89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,2013-01-01 15:11:48,CSH,6.5,0,0.5,0,0,7
       0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-06 00:18:35,CSH,6,0.5,0.5,0,0,7
       0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-05 18:49:41,CSH,5.5,1,0.5,0,0,7
       DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:54:15,CSH,5,0.5,0.5,0,0,6
       DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:25:03,CSH,9.5,0.5,0.5,0,0,10.5

<span data-ttu-id="0b1aa-186">viagem de toojoin de chave exclusivo Olá\_dados e viagem\_fare é composto por Olá seguintes três campos: medallion, acesso\_licença e recolha\_datetime.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-186">hello unique key toojoin trip\_data and trip\_fare is composed of hello following three fields: medallion, hack\_license and pickup\_datetime.</span></span> <span data-ttu-id="0b1aa-187">ficheiros CSV em bruto Olá podem ser acedidos a partir de um blob de armazenamento do Azure público.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-187">hello raw CSV files can be accessed from a public Azure storage blob.</span></span> <span data-ttu-id="0b1aa-188">Olá script U-SQL para esta associação é no Olá [associar tabelas viagem e fare](#join) secção.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-188">hello U-SQL script for this join is in hello [Join trip and fare tables](#join) section.</span></span>

## <a name="process-data-with-u-sql"></a><span data-ttu-id="0b1aa-189">Processar os dados com o U-SQL</span><span class="sxs-lookup"><span data-stu-id="0b1aa-189">Process data with U-SQL</span></span>
<span data-ttu-id="0b1aa-190">as tarefas de processamento de dados de Olá ilustradas nesta secção incluem ingestão relacionadas, verificar a qualidade, a explorar e a amostragem de dados de Olá.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-190">hello data processing tasks illustrated in this section include ingesting, checking quality, exploring, and sampling hello data.</span></span> <span data-ttu-id="0b1aa-191">Também vamos mostrar como toojoin viagem e fare tabelas.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-191">We also show how toojoin trip and fare tables.</span></span> <span data-ttu-id="0b1aa-192">secção final Olá mostra executar uma tarefa de script U-SQL de Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-192">hello final section shows run a U-SQL scripted job from hello Azure portal.</span></span> <span data-ttu-id="0b1aa-193">Seguem-se ligações tooeach subsecção:</span><span class="sxs-lookup"><span data-stu-id="0b1aa-193">Here are links tooeach subsection:</span></span>

* [<span data-ttu-id="0b1aa-194">Ingestão de dados: ler dados a partir do blob público</span><span class="sxs-lookup"><span data-stu-id="0b1aa-194">Data ingestion: read in data from public blob</span></span>](#ingest)
* [<span data-ttu-id="0b1aa-195">Verificações de qualidade de dados</span><span class="sxs-lookup"><span data-stu-id="0b1aa-195">Data quality checks</span></span>](#quality)
* [<span data-ttu-id="0b1aa-196">Exploração de dados</span><span class="sxs-lookup"><span data-stu-id="0b1aa-196">Data exploration</span></span>](#explore)
* [<span data-ttu-id="0b1aa-197">Associar viagem e fare tabelas</span><span class="sxs-lookup"><span data-stu-id="0b1aa-197">Join trip and fare tables</span></span>](#join)
* [<span data-ttu-id="0b1aa-198">Amostragem de dados</span><span class="sxs-lookup"><span data-stu-id="0b1aa-198">Data sampling</span></span>](#sample)
* [<span data-ttu-id="0b1aa-199">Executar tarefas U-SQL</span><span class="sxs-lookup"><span data-stu-id="0b1aa-199">Run U-SQL jobs</span></span>](#run)

<span data-ttu-id="0b1aa-200">Olá scripts U-SQL são descritas aqui e fornecidos num ficheiro separado.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-200">hello U-SQL scripts are described here and provided in a separate file.</span></span> <span data-ttu-id="0b1aa-201">Pode transferir Olá completa **scripts U-SQL** de [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/AzureDataLakeWalkthrough).</span><span class="sxs-lookup"><span data-stu-id="0b1aa-201">You can download hello full **U-SQL scripts** from [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/AzureDataLakeWalkthrough).</span></span>

<span data-ttu-id="0b1aa-202">tooexecute U-SQL, abra Visual Studio, clique em **ficheiro--> novo--> projeto**, escolha **projeto U-SQL**, atribua um nome e guardá-lo tooa pasta.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-202">tooexecute U-SQL, Open Visual Studio, click **File --> New --> Project**, choose **U-SQL Project**, name and save it tooa folder.</span></span>

![8](./media/machine-learning-data-science-process-data-lake-walkthrough/8-create-USQL-project.PNG)

> [!NOTE]
> <span data-ttu-id="0b1aa-204">É possível toouse Olá Portal do Azure tooexecute U-SQL em vez do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-204">It is possible toouse hello Azure Portal tooexecute U-SQL instead of Visual Studio.</span></span> <span data-ttu-id="0b1aa-205">Pode navegar recursos do Azure Data Lake Analytics toohello no portal de Olá e submeter consultas diretamente como ilustradas na Olá figura a seguir.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-205">You can navigate toohello Azure Data Lake Analytics resource on hello portal and submit queries directly as illustrated in hello following figure.</span></span>
> 
> 

![9](./media/machine-learning-data-science-process-data-lake-walkthrough/9-portal-submit-job.PNG)

### <span data-ttu-id="0b1aa-207"><a name="ingest"></a>Ingestão de dados: Ler dados a partir do blob público</span><span class="sxs-lookup"><span data-stu-id="0b1aa-207"><a name="ingest"></a>Data Ingestion: Read in data from public blob</span></span>
<span data-ttu-id="0b1aa-208">localização de Olá dos dados de Olá no Olá BLOBs do Azure é referenciada como  **wasb://container_name@blob_storage_account_name.blob.core.windows.net/blob_name**  e pode ser extraída utilizando **Extractors.Csv()**.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-208">hello location of hello data in hello Azure blob is referenced as **wasb://container_name@blob_storage_account_name.blob.core.windows.net/blob_name** and can be extracted using **Extractors.Csv()**.</span></span> <span data-ttu-id="0b1aa-209">Substitua o seu nome de contentor e um nome de conta do storage em scripts seguintes para container_name@blob_storage_account_name no endereço de wasb Olá.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-209">Substitute your own container name and storage account name in following scripts for container_name@blob_storage_account_name in hello wasb address.</span></span> <span data-ttu-id="0b1aa-210">Uma vez que os nomes de ficheiro Olá estão no mesmo formato, podemos utilizar **viagem\_data_ {\*\}. csv** tooread em todos os ficheiros de 12 viagem.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-210">Since hello file names are in same format, we can use **trip\_data_{\*\}.csv** tooread in all 12 trip files.</span></span> 

    ///Read in Trip data
    @trip0 =
        EXTRACT 
        medallion string,
        hack_license string,
        vendor_id string,
        rate_code string,
        store_and_fwd_flag string,
        pickup_datetime string,
        dropoff_datetime string,
        passenger_count string,
        trip_time_in_secs string,
        trip_distance string,
        pickup_longitude string,
        pickup_latitude string,
        dropoff_longitude string,
        dropoff_latitude string
    // This is reading 12 trip data from blob
    FROM "wasb://container_name@blob_storage_account_name.blob.core.windows.net/nyctaxitrip/trip_data_{*}.csv"
    USING Extractors.Csv();

<span data-ttu-id="0b1aa-211">Uma vez que existem cabeçalhos na primeira linha de Olá, iremos tem cabeçalhos de Olá tooremove e alterar tipos de coluna para aqueles adequado.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-211">Since there are headers in hello first row, we need tooremove hello headers and change column types into appropriate ones.</span></span> <span data-ttu-id="0b1aa-212">É possível guardar Olá processado dados tooAzure armazenamento do Data Lake, utilizando **swebhdfs://data_lake_storage_name.azuredatalakestorage.net/folder_name/file_name**conta de armazenamento de BLOBs de _ ou tooAzure através de  **wasb://container_name@blob_storage_account_name.blob.core.windows.net/blob_name** .</span><span class="sxs-lookup"><span data-stu-id="0b1aa-212">We can either save hello processed data tooAzure Data Lake Storage using **swebhdfs://data_lake_storage_name.azuredatalakestorage.net/folder_name/file_name**_ or tooAzure Blob storage account using  **wasb://container_name@blob_storage_account_name.blob.core.windows.net/blob_name**.</span></span> 

    // change data types
    @trip =
        SELECT 
        medallion,
        hack_license,
        vendor_id,
        rate_code,
        store_and_fwd_flag,
        DateTime.Parse(pickup_datetime) AS pickup_datetime,
        DateTime.Parse(dropoff_datetime) AS dropoff_datetime,
        Int32.Parse(passenger_count) AS passenger_count,
        Double.Parse(trip_time_in_secs) AS trip_time_in_secs,
        Double.Parse(trip_distance) AS trip_distance,
        (pickup_longitude==string.Empty ? 0: float.Parse(pickup_longitude)) AS pickup_longitude,
        (pickup_latitude==string.Empty ? 0: float.Parse(pickup_latitude)) AS pickup_latitude,
        (dropoff_longitude==string.Empty ? 0: float.Parse(dropoff_longitude)) AS dropoff_longitude,
        (dropoff_latitude==string.Empty ? 0: float.Parse(dropoff_latitude)) AS dropoff_latitude
    FROM @trip0
    WHERE medallion != "medallion";

    ////output data tooADL
    OUTPUT @trip   
    too"swebhdfs://data_lake_storage_name.azuredatalakestore.net/nyctaxi_folder/demo_trip.csv"
    USING Outputters.Csv(); 

    ////Output data tooblob
    OUTPUT @trip   
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_trip.csv"
    USING Outputters.Csv();  

<span data-ttu-id="0b1aa-213">Da mesma forma, pode ler conjuntos de dados de fare Olá.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-213">Similarly we can read in hello fare data sets.</span></span> <span data-ttu-id="0b1aa-214">Clique com o botão direito do rato em Azure Data Lake Store, pode escolher toolook os dados no **Portal do Azure--> Explorador de dados** ou **Explorador de ficheiros** no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-214">Right click Azure Data Lake Store, you can choose toolook at your data in **Azure Portal --> Data Explorer** or **File Explorer** within Visual Studio.</span></span> 

 ![10](./media/machine-learning-data-science-process-data-lake-walkthrough/10-data-in-ADL-VS.PNG)

 ![11](./media/machine-learning-data-science-process-data-lake-walkthrough/11-data-in-ADL.PNG)

### <span data-ttu-id="0b1aa-217"><a name="quality"></a>Verificações de qualidade de dados</span><span class="sxs-lookup"><span data-stu-id="0b1aa-217"><a name="quality"></a>Data quality checks</span></span>
<span data-ttu-id="0b1aa-218">Depois de tem sido lida viagem e fare tabelas, as verificações de qualidade de dados podem ser feitas no Olá seguinte forma.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-218">After trip and fare tables have been read in, data quality checks can be done in hello following way.</span></span> <span data-ttu-id="0b1aa-219">Olá resultante ficheiros CSV pode ser armazenamento de BLOBs de tooAzure de saída ou do Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-219">hello resulting CSV files can be output tooAzure Blob storage or Azure Data Lake Store.</span></span> 

<span data-ttu-id="0b1aa-220">Encontrar o número de Olá de medallions e o número exclusivo de medallions:</span><span class="sxs-lookup"><span data-stu-id="0b1aa-220">Find hello number of medallions and unique number of medallions:</span></span>

    ///check hello number of medallions and unique number of medallions
    @trip2 =
        SELECT
        medallion,
        vendor_id,
        pickup_datetime.Month AS pickup_month
        FROM @trip;

    @ex_1 =
        SELECT
        pickup_month, 
        COUNT(medallion) AS cnt_medallion,
        COUNT(DISTINCT(medallion)) AS unique_medallion
        FROM @trip2
        GROUP BY pickup_month;
        OUTPUT @ex_1   
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_1.csv"
    USING Outputters.Csv(); 

<span data-ttu-id="0b1aa-221">Localize esses medallions que tinha mais do que 100 viagens:</span><span class="sxs-lookup"><span data-stu-id="0b1aa-221">Find those medallions that had more than 100 trips:</span></span>

    ///find those medallions that had more than 100 trips
    @ex_2 =
        SELECT medallion,
               COUNT(medallion) AS cnt_medallion
        FROM @trip2
        //where pickup_datetime >= "2013-01-01t00:00:00.0000000" and pickup_datetime <= "2013-04-01t00:00:00.0000000"
        GROUP BY medallion
        HAVING COUNT(medallion) > 100;
        OUTPUT @ex_2   
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_2.csv"
    USING Outputters.Csv(); 

<span data-ttu-id="0b1aa-222">Localize os registos inválidos em termos de pickup_longitude:</span><span class="sxs-lookup"><span data-stu-id="0b1aa-222">Find those invalid records in terms of pickup_longitude:</span></span>

    ///find those invalid records in terms of pickup_longitude
    @ex_3 =
        SELECT COUNT(medallion) AS cnt_invalid_pickup_longitude
        FROM @trip
        WHERE
        pickup_longitude <- 90 OR pickup_longitude > 90;
        OUTPUT @ex_3   
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_3.csv"
    USING Outputters.Csv(); 

<span data-ttu-id="0b1aa-223">Localize os valores em falta para algumas variáveis:</span><span class="sxs-lookup"><span data-stu-id="0b1aa-223">Find missing values for some variables:</span></span>

    //check missing values
    @res =
        SELECT *,
               (medallion == null? 1 : 0) AS missing_medallion
        FROM @trip;

    @trip_summary6 =
        SELECT 
            vendor_id,
        SUM(missing_medallion) AS medallion_empty, 
        COUNT(medallion) AS medallion_total,
        COUNT(DISTINCT(medallion)) AS medallion_total_unique  
        FROM @res
        GROUP BY vendor_id;
    OUTPUT @trip_summary6
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_16.csv"
    USING Outputters.Csv();



### <span data-ttu-id="0b1aa-224"><a name="explore"></a>Exploração de dados</span><span class="sxs-lookup"><span data-stu-id="0b1aa-224"><a name="explore"></a>Data exploration</span></span>
<span data-ttu-id="0b1aa-225">Podemos fazer algumas tooget de exploração de dados uma melhor compreensão dos dados de Olá.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-225">We can do some data exploration tooget a better understanding of hello data.</span></span>

<span data-ttu-id="0b1aa-226">Localize distribuição Olá viagens tipped e não tipped:</span><span class="sxs-lookup"><span data-stu-id="0b1aa-226">Find hello distribution of tipped and non-tipped trips:</span></span>

    ///tipped vs. not tipped distribution
    @tip_or_not =
        SELECT *,
               (tip_amount > 0 ? 1: 0) AS tipped
        FROM @fare;

    @ex_4 =
        SELECT tipped,
               COUNT(*) AS tip_freq
        FROM @tip_or_not
        GROUP BY tipped;
        OUTPUT @ex_4   
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_4.csv"
    USING Outputters.Csv(); 

<span data-ttu-id="0b1aa-227">Localizar distribuição Olá da quantidade de sugestão com valores de truncado: 0,5,10 e utilizados no compromisso 20.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-227">Find hello distribution of tip amount with cut-off values: 0,5,10,and 20 dollars.</span></span>

    //tip class/range distribution
    @tip_class =
        SELECT *,
               (tip_amount >20? 4: (tip_amount >10? 3:(tip_amount >5 ? 2:(tip_amount > 0 ? 1: 0)))) AS tip_class
        FROM @fare;
    @ex_5 =
        SELECT tip_class,
               COUNT(*) AS tip_freq
        FROM @tip_class
        GROUP BY tip_class;
        OUTPUT @ex_5   
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_5.csv"
    USING Outputters.Csv(); 

<span data-ttu-id="0b1aa-228">Localize estatísticas básicas de distância viagem:</span><span class="sxs-lookup"><span data-stu-id="0b1aa-228">Find basic statistics of trip distance:</span></span>

    // find basic statistics for trip_distance
    @trip_summary4 =
        SELECT 
            vendor_id,
            COUNT(*) AS cnt_row,
            MIN(trip_distance) AS min_trip_distance,
            MAX(trip_distance) AS max_trip_distance,
            AVG(trip_distance) AS avg_trip_distance 
        FROM @trip
        GROUP BY vendor_id;
    OUTPUT @trip_summary4
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_14.csv"
    USING Outputters.Csv();

<span data-ttu-id="0b1aa-229">Localize percentiles Olá de distância viagem:</span><span class="sxs-lookup"><span data-stu-id="0b1aa-229">Find hello percentiles of trip distance:</span></span>

    // find percentiles of trip_distance
    @trip_summary3 =
        SELECT DISTINCT vendor_id AS vendor,
                        PERCENTILE_DISC(0.25) WITHIN GROUP(ORDER BY trip_distance) OVER(PARTITION BY vendor_id) AS median_trip_distance_disc,
                        PERCENTILE_DISC(0.5) WITHIN GROUP(ORDER BY trip_distance) OVER(PARTITION BY vendor_id) AS median_trip_distance_disc,
                        PERCENTILE_DISC(0.75) WITHIN GROUP(ORDER BY trip_distance) OVER(PARTITION BY vendor_id) AS median_trip_distance_disc
        FROM @trip;
       // group by vendor_id;
    OUTPUT @trip_summary3
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_13.csv"
    USING Outputters.Csv(); 


### <span data-ttu-id="0b1aa-230"><a name="join"></a>Associar viagem e fare tabelas</span><span class="sxs-lookup"><span data-stu-id="0b1aa-230"><a name="join"></a>Join trip and fare tables</span></span>
<span data-ttu-id="0b1aa-231">As tabelas viagem e fare podem ser associadas ao medallion, hack_license e pickup_time.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-231">Trip and fare tables can be joined by medallion, hack_license, and pickup_time.</span></span>

    //join trip and fare table

    @model_data_full =
    SELECT t.*, 
    f.payment_type, f.fare_amount, f.surcharge, f.mta_tax, f.tolls_amount,  f.total_amount, f.tip_amount,
    (f.tip_amount > 0 ? 1: 0) AS tipped,
    (f.tip_amount >20? 4: (f.tip_amount >10? 3:(f.tip_amount >5 ? 2:(f.tip_amount > 0 ? 1: 0)))) AS tip_class
    FROM @trip AS t JOIN  @fare AS f
    ON   (t.medallion == f.medallion AND t.hack_license == f.hack_license AND t.pickup_datetime == f.pickup_datetime)
    WHERE   (pickup_longitude != 0 AND dropoff_longitude != 0 );

    //// output tooblob
    OUTPUT @model_data_full   
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_7_full_data.csv"
    USING Outputters.Csv(); 

    ////output data tooADL
    OUTPUT @model_data_full   
    too"swebhdfs://data_lake_storage_name.azuredatalakestore.net/nyctaxi_folder/demo_ex_7_full_data.csv"
    USING Outputters.Csv(); 


<span data-ttu-id="0b1aa-232">Para cada nível de contagem de passenger, calcule o número de Olá de registos, a quantidade de sugestão média, a variância a partir da quantidade de sugestão, percentagem de viagens tipped.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-232">For each level of passenger count, calculate hello number of records, average tip amount, variance of tip amount, percentage of tipped trips.</span></span>

    // contigency table
    @trip_summary8 =
        SELECT passenger_count,
               COUNT(*) AS cnt,
               AVG(tip_amount) AS avg_tip_amount,
               VAR(tip_amount) AS var_tip_amount,
               SUM(tipped) AS cnt_tipped,
               (float)SUM(tipped)/COUNT(*) AS pct_tipped
        FROM @model_data_full
        GROUP BY passenger_count;
        OUTPUT @trip_summary8
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_17.csv"
    USING Outputters.Csv();


### <span data-ttu-id="0b1aa-233"><a name="sample"></a>Amostragem de dados</span><span class="sxs-lookup"><span data-stu-id="0b1aa-233"><a name="sample"></a>Data sampling</span></span>
<span data-ttu-id="0b1aa-234">Primeiro vamos aleatoriamente selecione 0.1% dos dados de Olá da tabela associada ao hello:</span><span class="sxs-lookup"><span data-stu-id="0b1aa-234">First we randomly select 0.1% of hello data from hello joined table:</span></span>

    //random select 1/1000 data for modeling purpose
    @addrownumberres_randomsample =
    SELECT *,
            ROW_NUMBER() OVER() AS rownum
    FROM @model_data_full;

    @model_data_random_sample_1_1000 =
    SELECT *
    FROM @addrownumberres_randomsample
    WHERE rownum % 1000 == 0;

    OUTPUT @model_data_random_sample_1_1000   
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_7_random_1_1000.csv"
    USING Outputters.Csv(); 

<span data-ttu-id="0b1aa-235">Em seguida, iremos fazer a amostragem stratified binário tip_class variável:</span><span class="sxs-lookup"><span data-stu-id="0b1aa-235">Then we do stratified sampling by binary variable tip_class:</span></span>

    //stratified random select 1/1000 data for modeling purpose
    @addrownumberres_stratifiedsample =
    SELECT *,
            ROW_NUMBER() OVER(PARTITION BY tip_class) AS rownum
    FROM @model_data_full;

    @model_data_stratified_sample_1_1000 =
    SELECT *
    FROM @addrownumberres_stratifiedsample
    WHERE rownum % 1000 == 0;
    //// output tooblob
    OUTPUT @model_data_stratified_sample_1_1000   
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_9_stratified_1_1000.csv"
    USING Outputters.Csv(); 
    ////output data tooADL
    OUTPUT @model_data_stratified_sample_1_1000   
    too"swebhdfs://data_lake_storage_name.azuredatalakestore.net/nyctaxi_folder/demo_ex_9_stratified_1_1000.csv"
    USING Outputters.Csv(); 


### <span data-ttu-id="0b1aa-236"><a name="run"></a>Executar tarefas U-SQL</span><span class="sxs-lookup"><span data-stu-id="0b1aa-236"><a name="run"></a>Run U-SQL jobs</span></span>
<span data-ttu-id="0b1aa-237">Quando concluir a edição scripts U-SQL, pode submetê-las servidor toohello utilizando a sua conta do Azure Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-237">When you finish editing U-SQL scripts, you can submit them toohello server using your Azure Data Lake Analytics account.</span></span> <span data-ttu-id="0b1aa-238">Clique em **Data Lake**, **submeter tarefa**, selecione o **conta Analytics**, escolha **paralelismo**e clique em **submeter** botão.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-238">Click **Data Lake**, **Submit Job**, select your **Analytics Account**, choose **Parallelism**, and click **Submit** button.</span></span>  

 ![12](./media/machine-learning-data-science-process-data-lake-walkthrough/12-submit-USQL.PNG)

<span data-ttu-id="0b1aa-240">Quando a tarefa de Olá é complied com êxito, estado de Olá da tarefa será apresentado no Visual Studio para monitorização.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-240">When hello job is complied successfully, hello status of your job will be displayed in Visual Studio for monitoring.</span></span> <span data-ttu-id="0b1aa-241">Após a conclusão da tarefa de Olá em execução, pode mesmo reprodução Olá tarefa processo de execução e descobrir Olá bottleneck passos tooimprove a eficiência da tarefa.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-241">After hello job finishes running, you can even replay hello job execution process and find out hello bottleneck steps tooimprove your job efficiency.</span></span> <span data-ttu-id="0b1aa-242">Pode também aceder tooAzure Portal toocheck Olá Estado as tarefas U-SQL.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-242">You can also go tooAzure Portal toocheck hello status of your U-SQL jobs.</span></span>

 ![13](./media/machine-learning-data-science-process-data-lake-walkthrough/13-USQL-running-v2.PNG)

 ![14](./media/machine-learning-data-science-process-data-lake-walkthrough/14-USQL-jobs-portal.PNG)

<span data-ttu-id="0b1aa-245">Agora pode verificar os ficheiros de saída de Olá no Blob storage do Azure ou no Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-245">Now you can check hello output files in either Azure Blob storage or Azure Portal.</span></span> <span data-ttu-id="0b1aa-246">Utilizaremos os dados de exemplo de Olá stratified para a nossa modelação no passo seguinte Olá.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-246">We will use hello stratified sample data for our modeling in hello next step.</span></span>

 ![15](./media/machine-learning-data-science-process-data-lake-walkthrough/15-U-SQL-output-csv.PNG)

 ![16](./media/machine-learning-data-science-process-data-lake-walkthrough/16-U-SQL-output-csv-portal.PNG)

## <a name="build-and-deploy-models-in-azure-machine-learning"></a><span data-ttu-id="0b1aa-249">Criar e implementar modelos no Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="0b1aa-249">Build and deploy models in Azure Machine Learning</span></span>
<span data-ttu-id="0b1aa-250">Iremos demonstrar duas opções disponíveis para si toopull dados no Azure Machine Learning toobuild e</span><span class="sxs-lookup"><span data-stu-id="0b1aa-250">We demonstrate two options available for you toopull data into Azure Machine Learning toobuild and</span></span> 

* <span data-ttu-id="0b1aa-251">Na primeira opção Olá, utilize dados Olá amostragem que foi escritos tooan Blob do Azure (no Olá **amostragem de dados** passo acima) e utilizar o Python toobuild e implementar modelos do Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-251">In hello first option, you use hello sampled data that has been written tooan Azure Blob (in hello **Data sampling** step above) and use Python toobuild and deploy models from Azure Machine Learning.</span></span> 
* <span data-ttu-id="0b1aa-252">Na segunda opção Olá, consultar dados Olá no Azure Data Lake diretamente utilizando uma consulta do Hive.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-252">In hello second option, you query hello data in Azure Data Lake directly using a Hive query.</span></span> <span data-ttu-id="0b1aa-253">Esta opção exige que crie um novo cluster de HDInsight ou utilize um cluster do HDInsight existente onde Olá Hive tabelas toohello de ponto de dados de NY Taxi no armazenamento do Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-253">This option requires that you create a new HDInsight cluster or use an existing HDInsight cluster where hello Hive tables point toohello NY Taxi data in Azure Data Lake Storage.</span></span>  <span data-ttu-id="0b1aa-254">Vamos discutir ambas estas opções abaixo.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-254">We discuss both these options below.</span></span> 

## <a name="option-1-use-python-toobuild-and-deploy-machine-learning-models"></a><span data-ttu-id="0b1aa-255">Opção 1: Utilizar Python toobuild e implementar modelos de machine learning</span><span class="sxs-lookup"><span data-stu-id="0b1aa-255">Option 1: Use Python toobuild and deploy machine learning models</span></span>
<span data-ttu-id="0b1aa-256">toobuild e implementar modelos de machine learning com o Python, criar um bloco de notas do Jupyter no seu computador local ou no Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-256">toobuild and deploy machine learning models using Python, create a Jupyter Notebook on your local machine or in Azure Machine Learning Studio.</span></span> <span data-ttu-id="0b1aa-257">Olá bloco de notas do Jupyter fornecido no [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/AzureDataLakeWalkthrough) contém Olá tooexplore código completo, visualizar dados, engenharia da funcionalidade, modelação e a implementação.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-257">hello Jupyter Notebook  provided on [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/AzureDataLakeWalkthrough) contains hello full code tooexplore, visualize data, feature engineering, modeling and deployment.</span></span> <span data-ttu-id="0b1aa-258">Neste artigo, vamos mostrar apenas a modelação de Olá e a implementação.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-258">In this article, we show just hello modeling and deployment.</span></span> 

### <a name="import-python-libraries"></a><span data-ttu-id="0b1aa-259">Importar bibliotecas de Python</span><span class="sxs-lookup"><span data-stu-id="0b1aa-259">Import Python libraries</span></span>
<span data-ttu-id="0b1aa-260">No Olá toorun de ordem de exemplo o bloco de notas do Jupyter ou Olá o ficheiro de script de Python, hello seguintes pacotes de Python são necessários.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-260">In order toorun hello sample Jupyter Notebook or hello Python script file, hello following Python packages are needed.</span></span> <span data-ttu-id="0b1aa-261">Se estiver a utilizar Olá serviço AzureML bloco de notas, estes pacotes tem sido previamente instalados.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-261">If you are using hello AzureML Notebook service, these packages have been pre-installed.</span></span>

    import pandas as pd
    from pandas import Series, DataFrame
    import numpy as np
    import matplotlib.pyplot as plt
    from time import time
    import pyodbc
    import os
    from azure.storage.blob import BlobService
    import tables
    import time
    import zipfile
    import random
    import sklearn
    from sklearn.linear_model import LogisticRegression
    from sklearn.cross_validation import train_test_split
    from sklearn import metrics
    from __future__ import division
    from sklearn import linear_model
    from azureml import services


### <a name="read-in-hello-data-from-blob"></a><span data-ttu-id="0b1aa-262">Ler dados Olá a partir do blob</span><span class="sxs-lookup"><span data-stu-id="0b1aa-262">Read in hello data from blob</span></span>
* <span data-ttu-id="0b1aa-263">Cadeia de ligação</span><span class="sxs-lookup"><span data-stu-id="0b1aa-263">Connection String</span></span>   
  
        CONTAINERNAME = 'test1'
        STORAGEACCOUNTNAME = 'XXXXXXXXX'
        STORAGEACCOUNTKEY = 'YYYYYYYYYYYYYYYYYYYYYYYYYYYY'
        BLOBNAME = 'demo_ex_9_stratified_1_1000_copy.csv'
        blob_service = BlobService(account_name=STORAGEACCOUNTNAME,account_key=STORAGEACCOUNTKEY)
* <span data-ttu-id="0b1aa-264">Lida como texto</span><span class="sxs-lookup"><span data-stu-id="0b1aa-264">Read in as text</span></span>
  
        t1 = time.time()
        data = blob_service.get_blob_to_text(CONTAINERNAME,BLOBNAME).split("\n")
        t2 = time.time()
        print(("It takes %s seconds tooread in "+BLOBNAME) % (t2 - t1))
  
  ![17](./media/machine-learning-data-science-process-data-lake-walkthrough/17-python_readin_csv.PNG)    
* <span data-ttu-id="0b1aa-266">Adicionar nomes de coluna e separe colunas</span><span class="sxs-lookup"><span data-stu-id="0b1aa-266">Add column names and separate columns</span></span>
  
        colnames = ['medallion','hack_license','vendor_id','rate_code','store_and_fwd_flag','pickup_datetime','dropoff_datetime',
        'passenger_count','trip_time_in_secs','trip_distance','pickup_longitude','pickup_latitude','dropoff_longitude','dropoff_latitude',
        'payment_type', 'fare_amount', 'surcharge', 'mta_tax', 'tolls_amount',  'total_amount', 'tip_amount', 'tipped', 'tip_class', 'rownum']
        df1 = pd.DataFrame([sub.split(",") for sub in data], columns = colnames)
* <span data-ttu-id="0b1aa-267">Alterar algumas toonumeric de colunas</span><span class="sxs-lookup"><span data-stu-id="0b1aa-267">Change some columns toonumeric</span></span>
  
        cols_2_float = ['trip_time_in_secs','pickup_longitude','pickup_latitude','dropoff_longitude','dropoff_latitude',
        'fare_amount', 'surcharge','mta_tax','tolls_amount','total_amount','tip_amount', 'passenger_count','trip_distance'
        ,'tipped','tip_class','rownum']
        for col in cols_2_float:
            df1[col] = df1[col].astype(float)

### <a name="build-machine-learning-models"></a><span data-ttu-id="0b1aa-268">Criar modelos de machine learning</span><span class="sxs-lookup"><span data-stu-id="0b1aa-268">Build machine learning models</span></span>
<span data-ttu-id="0b1aa-269">Aqui vamos construir um toopredict de modelo de classificação binária se um viagem é tipped ou não.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-269">Here we build a binary classification model toopredict whether a trip is tipped or not.</span></span> <span data-ttu-id="0b1aa-270">Olá bloco de notas do Jupyter pode encontrar outros dois modelos: classificação várias classes e modelos de regressão.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-270">In hello Jupyter Notebook you can find other two models: multiclass classification, and regression models.</span></span>

* <span data-ttu-id="0b1aa-271">Primeiro é preciso toocreate variáveis fictício que podem ser utilizadas em scikit-saiba modelos</span><span class="sxs-lookup"><span data-stu-id="0b1aa-271">First we need toocreate dummy variables that can be used in scikit-learn models</span></span>
  
        df1_payment_type_dummy = pd.get_dummies(df1['payment_type'], prefix='payment_type_dummy')
        df1_vendor_id_dummy = pd.get_dummies(df1['vendor_id'], prefix='vendor_id_dummy')
* <span data-ttu-id="0b1aa-272">Criar moldura de dados para a modelação de Olá</span><span class="sxs-lookup"><span data-stu-id="0b1aa-272">Create data frame for hello modeling</span></span>
  
        cols_to_keep = ['tipped', 'trip_distance', 'passenger_count']
        data = df1[cols_to_keep].join([df1_payment_type_dummy,df1_vendor_id_dummy])
  
        X = data.iloc[:,1:]
        Y = data.tipped
* <span data-ttu-id="0b1aa-273">Formação e testar 60 40 dividido</span><span class="sxs-lookup"><span data-stu-id="0b1aa-273">Training and testing 60-40 split</span></span>
  
        X_train, X_test, Y_train, Y_test = train_test_split(X, Y, test_size=0.4, random_state=0)
* <span data-ttu-id="0b1aa-274">Regressão logística no conjunto de preparação</span><span class="sxs-lookup"><span data-stu-id="0b1aa-274">Logistic Regression in training set</span></span>
  
        model = LogisticRegression()
        logit_fit = model.fit(X_train, Y_train)
        print ('Coefficients: \n', logit_fit.coef_)
        Y_train_pred = logit_fit.predict(X_train)
  
       ![c1](./media/machine-learning-data-science-process-data-lake-walkthrough/c1-py-logit-coefficient.PNG)
* <span data-ttu-id="0b1aa-275">Pontuar o conjunto de dados de teste</span><span class="sxs-lookup"><span data-stu-id="0b1aa-275">Score testing data set</span></span>
  
        Y_test_pred = logit_fit.predict(X_test)
* <span data-ttu-id="0b1aa-276">Calcular as métricas de avaliação</span><span class="sxs-lookup"><span data-stu-id="0b1aa-276">Calculate Evaluation metrics</span></span>
  
        fpr_train, tpr_train, thresholds_train = metrics.roc_curve(Y_train, Y_train_pred)
        print fpr_train, tpr_train, thresholds_train
  
        fpr_test, tpr_test, thresholds_test = metrics.roc_curve(Y_test, Y_test_pred) 
        print fpr_test, tpr_test, thresholds_test
  
        #AUC
        print metrics.auc(fpr_train,tpr_train)
        print metrics.auc(fpr_test,tpr_test)
  
        #Confusion Matrix
        print metrics.confusion_matrix(Y_train,Y_train_pred)
        print metrics.confusion_matrix(Y_test,Y_test_pred)
  
       ![c2](./media/machine-learning-data-science-process-data-lake-walkthrough/c2-py-logit-evaluation.PNG)

### <a name="build-web-service-api-and-consume-it-in-python"></a><span data-ttu-id="0b1aa-277">Criar API Web do serviço e consumi-lo no Python</span><span class="sxs-lookup"><span data-stu-id="0b1aa-277">Build Web Service API and consume it in Python</span></span>
<span data-ttu-id="0b1aa-278">Queremos toooperationalize Olá modelo de machine learning depois de ter sido concebido.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-278">We want toooperationalize hello machine learning model after it has been built.</span></span> <span data-ttu-id="0b1aa-279">Aqui, utilizamos modelo logística da binário de Olá como exemplo.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-279">Here we use hello binary logistic model as an example.</span></span> <span data-ttu-id="0b1aa-280">Certifique-se de que Olá scikit-saber versão no seu computador local é 0.15.1.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-280">Make sure hello scikit-learn version in your local machine is 0.15.1.</span></span> <span data-ttu-id="0b1aa-281">Não tem tooworry sobre esta se utilizar o serviço do Azure ML studio.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-281">You don't have tooworry about this if you use Azure ML studio service.</span></span>

* <span data-ttu-id="0b1aa-282">Localize as credenciais da sua área de trabalho do Azure ML studio de definições.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-282">Find your workspace credentials from Azure ML studio settings.</span></span> <span data-ttu-id="0b1aa-283">No Azure Machine Learning Studio, clique em **definições** --> **nome** --> **Tokens de autorização**.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-283">In Azure Machine Learning Studio, click **Settings** --> **Name** --> **Authorization Tokens**.</span></span> 
  
    ![C3](./media/machine-learning-data-science-process-data-lake-walkthrough/c3-workspace-id.PNG)

        workspaceid = 'xxxxxxxxxxxxxxxxxxxxxxxxxxx'
        auth_token = 'xxxxxxxxxxxxxxxxxxxxxxxxxxx'

* <span data-ttu-id="0b1aa-285">Criar o serviço Web</span><span class="sxs-lookup"><span data-stu-id="0b1aa-285">Create Web Service</span></span>
  
        @services.publish(workspaceid, auth_token) 
        @services.types(trip_distance = float, passenger_count = float, payment_type_dummy_CRD = float, payment_type_dummy_CSH=float, payment_type_dummy_DIS = float, payment_type_dummy_NOC = float, payment_type_dummy_UNK = float, vendor_id_dummy_CMT = float, vendor_id_dummy_VTS = float)
        @services.returns(int) #0, or 1
        def predictNYCTAXI(trip_distance, passenger_count, payment_type_dummy_CRD, payment_type_dummy_CSH,payment_type_dummy_DIS, payment_type_dummy_NOC, payment_type_dummy_UNK, vendor_id_dummy_CMT, vendor_id_dummy_VTS ):
            inputArray = [trip_distance, passenger_count, payment_type_dummy_CRD, payment_type_dummy_CSH, payment_type_dummy_DIS, payment_type_dummy_NOC, payment_type_dummy_UNK, vendor_id_dummy_CMT, vendor_id_dummy_VTS]
            return logit_fit.predict(inputArray)
* <span data-ttu-id="0b1aa-286">Obter credenciais do serviço web</span><span class="sxs-lookup"><span data-stu-id="0b1aa-286">Get web service credentials</span></span>
  
        url = predictNYCTAXI.service.url
        api_key =  predictNYCTAXI.service.api_key
  
        print url
        print api_key
  
        @services.service(url, api_key)
        @services.types(trip_distance = float, passenger_count = float, payment_type_dummy_CRD = float, payment_type_dummy_CSH=float,payment_type_dummy_DIS = float, payment_type_dummy_NOC = float, payment_type_dummy_UNK = float, vendor_id_dummy_CMT = float, vendor_id_dummy_VTS = float)
        @services.returns(float)
        def NYCTAXIPredictor(trip_distance, passenger_count, payment_type_dummy_CRD, payment_type_dummy_CSH,payment_type_dummy_DIS, payment_type_dummy_NOC, payment_type_dummy_UNK, vendor_id_dummy_CMT, vendor_id_dummy_VTS ):
            pass
* <span data-ttu-id="0b1aa-287">Chame a API do serviço Web.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-287">Call Web service API.</span></span> <span data-ttu-id="0b1aa-288">Ter toowait 5-10 segundos após o passo anterior Olá.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-288">You have toowait 5-10 seconds after hello previous step.</span></span>
  
        NYCTAXIPredictor(1,2,1,0,0,0,0,0,1)
  
       ![c4](./media/machine-learning-data-science-process-data-lake-walkthrough/c4-call-API.PNG)

## <a name="option-2-create-and-deploy-models-directly-in-azure-machine-learning"></a><span data-ttu-id="0b1aa-289">Opção 2: Criar e implementar modelos diretamente no Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="0b1aa-289">Option 2: Create and deploy models directly in Azure Machine Learning</span></span>
<span data-ttu-id="0b1aa-290">Azure Machine Learning Studio pode ler os dados diretamente a partir do Azure Data Lake Store e, em seguida, ser toocreate utilizado e implementar modelos.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-290">Azure Machine Learning Studio can read data directly from Azure Data Lake Store and then be used toocreate and deploy models.</span></span> <span data-ttu-id="0b1aa-291">Esta abordagem utiliza uma tabela de Hive que aponta ao hello do Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-291">This approach uses a Hive table that points at hello Azure Data Lake Store.</span></span> <span data-ttu-id="0b1aa-292">Isto requer que um cluster separado do Azure HDInsight ser aprovisionado, em que Olá Hive tabela foi criada.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-292">This requires that a separate Azure HDInsight cluster be provisioned, on which hello Hive table is created.</span></span> <span data-ttu-id="0b1aa-293">Olá seguintes secções mostram como toodo isto.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-293">hello following sections show how toodo this.</span></span> 

### <a name="create-an-hdinsight-linux-cluster"></a><span data-ttu-id="0b1aa-294">Criar um Cluster do HDInsight com Linux</span><span class="sxs-lookup"><span data-stu-id="0b1aa-294">Create an HDInsight Linux Cluster</span></span>
<span data-ttu-id="0b1aa-295">Criar um Cluster do HDInsight (Linux) a partir de Olá [Portal do Azure](http://portal.azure.com). Para obter mais informações, consulte Olá **criar um cluster do HDInsight com acesso tooAzure Data Lake Store** secção [criar um cluster do HDInsight com o Data Lake Store utilizando o Portal do Azure](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="0b1aa-295">Create an HDInsight Cluster (Linux) from hello [Azure Portal](http://portal.azure.com).For details, see hello **Create an HDInsight cluster with access tooAzure Data Lake Store** section in [Create an HDInsight cluster with Data Lake Store using Azure Portal](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span></span>

 ![18](./media/machine-learning-data-science-process-data-lake-walkthrough/18-create_HDI_cluster.PNG)

### <a name="create-hive-table-in-hdinsight"></a><span data-ttu-id="0b1aa-297">Criar tabela do Hive no HDInsight</span><span class="sxs-lookup"><span data-stu-id="0b1aa-297">Create Hive table in HDInsight</span></span>
<span data-ttu-id="0b1aa-298">Agora vamos criar toobe de tabelas do Hive utilizado no Azure Machine Learning Studio no cluster do HDInsight Olá utilizando dados de Olá armazenados no Azure Data Lake Store no passo anterior Olá.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-298">Now we create Hive tables toobe used in Azure Machine Learning Studio in hello HDInsight cluster using hello data stored in Azure Data Lake Store in hello previous step.</span></span> <span data-ttu-id="0b1aa-299">Aceda toohello acabou de criar cluster do HDInsight.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-299">Go toohello HDInsight cluster just created.</span></span> <span data-ttu-id="0b1aa-300">Clique em **definições** --> **propriedades** --> **identidade do AAD do Cluster** --> **acesso ADLS**, Certifique-se a sua conta do Azure Data Lake Store é adicionada na lista de Olá com leitura, escrita e direitos de execução.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-300">Click **Settings** --> **Properties** --> **Cluster AAD Identity** --> **ADLS Access**, make sure your Azure Data Lake Store account is added in hello list with read, write and execute rights.</span></span> 

 ![19](./media/machine-learning-data-science-process-data-lake-walkthrough/19-HDI-cluster-add-ADLS.PNG)

<span data-ttu-id="0b1aa-302">Em seguida, clique em **Dashboard** toohello seguinte **definições** botão e uma janela irão aparecer.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-302">Then click **Dashboard** next toohello **Settings** button and a window will pop up.</span></span> <span data-ttu-id="0b1aa-303">Clique em **vista do Hive** Olá canto superior direito da página Olá e verá Olá **Editor de consultas**.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-303">Click **Hive View** in hello upper right corner of hello page and you will see hello **Query Editor**.</span></span>

 ![20](./media/machine-learning-data-science-process-data-lake-walkthrough/20-HDI-dashboard.PNG)

 ![21](./media/machine-learning-data-science-process-data-lake-walkthrough/21-Hive-Query-Editor-v2.PNG)

<span data-ttu-id="0b1aa-306">Cole no Olá seguir toocreate de scripts Hive uma tabela.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-306">Paste in hello following Hive scripts toocreate a table.</span></span> <span data-ttu-id="0b1aa-307">localização de Olá da origem de dados está numa referência de Azure Data Lake Store desta forma: **adl://data_lake_store_name.azuredatalakestore.net:443/nome_da_pasta/file_name**.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-307">hello location of data source is in Azure Data Lake Store reference in this way: **adl://data_lake_store_name.azuredatalakestore.net:443/folder_name/file_name**.</span></span>

    CREATE EXTERNAL TABLE nyc_stratified_sample
    (
        medallion string,
        hack_license string,
        vendor_id string,
        rate_code string,
        store_and_fwd_flag string,
        pickup_datetime string,
        dropoff_datetime string,
        passenger_count string,
        trip_time_in_secs string,
        trip_distance string,
        pickup_longitude string,
        pickup_latitude string,
        dropoff_longitude string,
        dropoff_latitude string,
      payment_type string,
      fare_amount string,
      surcharge string,
      mta_tax string,
      tolls_amount string,
      total_amount string,
      tip_amount string,
      tipped string,
      tip_class string,
      rownum string
      )
    ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' lines terminated by '\n'
    LOCATION 'adl://data_lake_storage_name.azuredatalakestore.net:443/nyctaxi_folder/demo_ex_9_stratified_1_1000_copy.csv';


<span data-ttu-id="0b1aa-308">Quando a consulta de Olá termina em execução, verá os resultados de Olá como esta:</span><span class="sxs-lookup"><span data-stu-id="0b1aa-308">When hello query finishes running, you will see hello results like this:</span></span>

 ![22](./media/machine-learning-data-science-process-data-lake-walkthrough/22-Hive-Query-results.PNG)

### <a name="build-and-deploy-models-in-azure-machine-learning-studio"></a><span data-ttu-id="0b1aa-310">Criar e implementar modelos no Azure Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="0b1aa-310">Build and deploy models in Azure Machine Learning Studio</span></span>
<span data-ttu-id="0b1aa-311">Iremos agora está pronto toobuild e implementar um modelo que prevê ou não uma sugestão é paga com o Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-311">We are now ready toobuild and deploy a model that predicts whether or not a tip is paid with Azure Machine Learning.</span></span> <span data-ttu-id="0b1aa-312">Olá dados de exemplo stratified estão pronto toobe utilizado nesta classificação binária (sugestão ou não) problema.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-312">hello stratified sample data is ready toobe used in this binary classification (tip or not) problem.</span></span> <span data-ttu-id="0b1aa-313">Olá modelos preditivos utiliza a classificação de várias classes (tip_class) e regressão (tip_amount) também pode ser criado e implementado com o Azure Machine Learning Studio, mas aqui vamos mostrar apenas como toohandle Olá maiúsculas utilizando Olá modelo de classificação binária.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-313">hello predictive models using multiclass classification (tip_class) and regression (tip_amount) can also be built and deployed with Azure Machine Learning Studio, but here we only show how toohandle hello case using hello binary classification model.</span></span>

1. <span data-ttu-id="0b1aa-314">Obter dados Olá do Azure ML com Olá **importar dados** módulo, disponível no Olá **dados de entrada e saída** secção.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-314">Get hello data into Azure ML using hello **Import Data** module, available in hello **Data Input and Output** section.</span></span> <span data-ttu-id="0b1aa-315">Para obter mais informações, consulte Olá [módulo importar dados](https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/) página de referência.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-315">For more information, see hello [Import Data module](https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/) reference page.</span></span>
2. <span data-ttu-id="0b1aa-316">Selecione **consulta do Hive** como Olá **origem de dados** no Olá **propriedades** painel.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-316">Select **Hive Query** as hello **Data source** in hello **Properties** panel.</span></span>
3. <span data-ttu-id="0b1aa-317">Olá colar seguinte script de ramo de registo no Olá **consulta de base de dados do Hive** editor</span><span class="sxs-lookup"><span data-stu-id="0b1aa-317">Paste hello following Hive script in hello **Hive database query** editor</span></span>
   
        select * from nyc_stratified_sample;
4. <span data-ttu-id="0b1aa-318">Introduza o cluster de URI do HDInsight Olá (Isto pode ser encontrado no Portal do Azure), as credenciais do Hadoop, localização de dados de saída e o nome de nome / / contentor da chave de conta do storage do Azure.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-318">Enter hello URI of HDInsight cluster (this can be found in Azure Portal), Hadoop credentials, location of output data, and Azure storage account name/key/container name.</span></span>
   
   ![23](./media/machine-learning-data-science-process-data-lake-walkthrough/23-reader-module-v3.PNG)  

<span data-ttu-id="0b1aa-320">Um exemplo de uma experimentação de classificação binária ler os dados da tabela do Hive é apresentado na figura Olá abaixo.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-320">An example of a binary classification experiment reading data from Hive table is shown in hello figure below.</span></span>

 ![24](./media/machine-learning-data-science-process-data-lake-walkthrough/24-AML-exp.PNG)

<span data-ttu-id="0b1aa-322">Depois de criada a experimentação Olá, clique em **segurança serviço Web** --> **preditiva serviço Web**</span><span class="sxs-lookup"><span data-stu-id="0b1aa-322">After hello experiment is created, click  **Set Up Web Service** --> **Predictive Web Service**</span></span>

 ![25](./media/machine-learning-data-science-process-data-lake-walkthrough/25-AML-exp-deploy.PNG)

<span data-ttu-id="0b1aa-324">Execute Olá criado automaticamente classificação experimentação, quando terminar, clique em **implementar serviço Web**</span><span class="sxs-lookup"><span data-stu-id="0b1aa-324">Run hello automatically created scoring experiment, when it finishes, click **Deploy Web Service**</span></span>

 ![26](./media/machine-learning-data-science-process-data-lake-walkthrough/26-AML-exp-deploy-web.PNG)

<span data-ttu-id="0b1aa-326">dashboard de serviço web de Olá será apresentado em breve:</span><span class="sxs-lookup"><span data-stu-id="0b1aa-326">hello web service dashboard will be displayed shortly:</span></span>

 ![27](./media/machine-learning-data-science-process-data-lake-walkthrough/27-AML-web-api.PNG)

## <a name="summary"></a><span data-ttu-id="0b1aa-328">Resumo</span><span class="sxs-lookup"><span data-stu-id="0b1aa-328">Summary</span></span>
<span data-ttu-id="0b1aa-329">Por concluir estas instruções criou um ambiente de ciência de dados para criar soluções de ponto a ponto dimensionáveis no Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-329">By completing this walkthrough you have created a data science environment for building scalable end-to-end solutions in Azure Data Lake.</span></span> <span data-ttu-id="0b1aa-330">Este ambiente foi tooanalyze utilizado um conjunto de dados público grande, colocar-ajudá Olá canónico Olá o processo de ciência de dados, de aquisição de dados através de formação do modelo, e, em seguida, o modelo de implementação toohello Olá, como um serviço web.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-330">This environment was used tooanalyze a large public dataset, taking it through hello canonical steps of hello Data Science Process, from data acquisition through model training, and then toohello deployment of hello model as a web service.</span></span> <span data-ttu-id="0b1aa-331">U-SQL foi tooprocess utilizado, explore e dados Olá de exemplo.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-331">U-SQL was used tooprocess, explore and sample hello data.</span></span> <span data-ttu-id="0b1aa-332">Python e o ramo de registo foram utilizados com o Azure Machine Learning Studio toobuild implementar modelos preditivos.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-332">Python and Hive were used with Azure Machine Learning Studio toobuild and deploy predictive models.</span></span>

## <a name="whats-next"></a><span data-ttu-id="0b1aa-333">Passos seguintes?</span><span class="sxs-lookup"><span data-stu-id="0b1aa-333">What's next?</span></span>
<span data-ttu-id="0b1aa-334">Olá learning caminho para o [processo de ciência de dados de equipa (TDSP)](http://aka.ms/datascienceprocess) fornece tootopics ligações que descrevem cada passo na Olá avançadas o processo de análise.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-334">hello learning path for the [Team Data Science Process (TDSP)](http://aka.ms/datascienceprocess) provides links tootopics describing each step in hello advanced analytics process.</span></span> <span data-ttu-id="0b1aa-335">Há uma série de instruções descritas em Olá [instruções do processo de ciência de dados de equipa](data-science-process-walkthroughs.md) como a página que demonstração toouse recursos e serviços em vários cenários de Análise Preditiva:</span><span class="sxs-lookup"><span data-stu-id="0b1aa-335">There are a series of walkthroughs itemized on hello [Team Data Science Process walkthroughs](data-science-process-walkthroughs.md) page that showcase how toouse resources and services in various predictive analytics scenarios:</span></span>

* [<span data-ttu-id="0b1aa-336">Olá o processo de ciência de dados de equipa em ação: utilizar o SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="0b1aa-336">hello Team Data Science Process in action: using SQL Data Warehouse</span></span>](machine-learning-data-science-process-sqldw-walkthrough.md)
* [<span data-ttu-id="0b1aa-337">Olá o processo de ciência de dados de equipa em ação: com clusters do HDInsight Hadoop</span><span class="sxs-lookup"><span data-stu-id="0b1aa-337">hello Team Data Science Process in action: using HDInsight Hadoop clusters</span></span>](machine-learning-data-science-process-hive-walkthrough.md)
* [<span data-ttu-id="0b1aa-338">Olá o processo de ciência de dados de equipa: utilizar o SQL Server</span><span class="sxs-lookup"><span data-stu-id="0b1aa-338">hello Team Data Science Process: using SQL Server</span></span>](machine-learning-data-science-process-sql-walkthrough.md)
* [<span data-ttu-id="0b1aa-339">Descrição geral da utilização do processo de ciência de dados de Olá Spark no Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="0b1aa-339">Overview of hello Data Science Process using Spark on Azure HDInsight</span></span>](machine-learning-data-science-spark-overview.md)

