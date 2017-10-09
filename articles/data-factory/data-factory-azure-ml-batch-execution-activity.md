---
title: aaaCreate pipelines de dados preditiva utilizando o Azure Data Factory | Microsoft Docs
description: Descreve como toocreate Criar pipelines preditivos com o Azure Data Factory e o Azure Machine Learning
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: 4fad8445-4e96-4ce0-aa23-9b88e5ec1965
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: shlo
ms.openlocfilehash: 943210c28b1696e299ff9b7cc96369b95f182354
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-predictive-pipelines-using-azure-machine-learning-and-azure-data-factory"></a><span data-ttu-id="caa08-103">Criar pipelines preditivos com o Azure Machine Learning e o Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="caa08-103">Create predictive pipelines using Azure Machine Learning and Azure Data Factory</span></span>

> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="caa08-104">Atividade do ramo de registo</span><span class="sxs-lookup"><span data-stu-id="caa08-104">Hive Activity</span></span>](data-factory-hive-activity.md) 
> * [<span data-ttu-id="caa08-105">Atividade do PIg</span><span class="sxs-lookup"><span data-stu-id="caa08-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="caa08-106">Atividade de MapReduce</span><span class="sxs-lookup"><span data-stu-id="caa08-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="caa08-107">Atividade de transmissão em fluxo do Hadoop</span><span class="sxs-lookup"><span data-stu-id="caa08-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="caa08-108">Atividade do Spark</span><span class="sxs-lookup"><span data-stu-id="caa08-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="caa08-109">Atividade de Execução em Lote do Machine Learning</span><span class="sxs-lookup"><span data-stu-id="caa08-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="caa08-110">Atividade de Recursos de Atualização de Machine Learning</span><span class="sxs-lookup"><span data-stu-id="caa08-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="caa08-111">Atividade de Procedimento Armazenado</span><span class="sxs-lookup"><span data-stu-id="caa08-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="caa08-112">Atividade de U-SQL do Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="caa08-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="caa08-113">Atividade personalizada do .NET</span><span class="sxs-lookup"><span data-stu-id="caa08-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

## <a name="introduction"></a><span data-ttu-id="caa08-114">Introdução</span><span class="sxs-lookup"><span data-stu-id="caa08-114">Introduction</span></span>

### <a name="azure-machine-learning"></a><span data-ttu-id="caa08-115">Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="caa08-115">Azure Machine Learning</span></span>
<span data-ttu-id="caa08-116">[O Azure Machine Learning](https://azure.microsoft.com/documentation/services/machine-learning/) permite toobuild, testar e implementar soluções de Análise Preditiva.</span><span class="sxs-lookup"><span data-stu-id="caa08-116">[Azure Machine Learning](https://azure.microsoft.com/documentation/services/machine-learning/) enables you toobuild, test, and deploy predictive analytics solutions.</span></span> <span data-ttu-id="caa08-117">Do ponto de vista alto nível, é efetuada em três passos:</span><span class="sxs-lookup"><span data-stu-id="caa08-117">From a high-level point of view, it is done in three steps:</span></span>

1. <span data-ttu-id="caa08-118">**Criar uma experimentação de preparação**.</span><span class="sxs-lookup"><span data-stu-id="caa08-118">**Create a training experiment**.</span></span> <span data-ttu-id="caa08-119">Execute este passo utilizando Olá Azure ML Studio.</span><span class="sxs-lookup"><span data-stu-id="caa08-119">You do this step by using hello Azure ML Studio.</span></span> <span data-ttu-id="caa08-120">studio de ML Olá é um ambiente de desenvolvimento de visual de colaboração que utilize tootrain e testar um modelo de Análise Preditiva utilizando dados de preparação.</span><span class="sxs-lookup"><span data-stu-id="caa08-120">hello ML studio is a collaborative visual development environment that you use tootrain and test a predictive analytics model using training data.</span></span>
2. <span data-ttu-id="caa08-121">**Converta-experimentação preditiva tooa**.</span><span class="sxs-lookup"><span data-stu-id="caa08-121">**Convert it tooa predictive experiment**.</span></span> <span data-ttu-id="caa08-122">Depois do seu modelo tem sido preparado com a dados existentes e estiver pronto toouse-tooscore novos dados, preparar e simplificar a sua experimentação para classificação.</span><span class="sxs-lookup"><span data-stu-id="caa08-122">Once your model has been trained with existing data and you are ready toouse it tooscore new data, you prepare and streamline your experiment for scoring.</span></span>
3. <span data-ttu-id="caa08-123">**Implementá-lo como um serviço web**.</span><span class="sxs-lookup"><span data-stu-id="caa08-123">**Deploy it as a web service**.</span></span> <span data-ttu-id="caa08-124">Pode publicar a sua experimentação de classificação como um serviço web do Azure.</span><span class="sxs-lookup"><span data-stu-id="caa08-124">You can publish your scoring experiment as an Azure web service.</span></span> <span data-ttu-id="caa08-125">Pode enviar o modelo de tooyour dados através deste ponto de final de serviço web e receber predições resultado fro modelo Olá.</span><span class="sxs-lookup"><span data-stu-id="caa08-125">You can send data tooyour model via this web service end point and receive result predictions fro hello model.</span></span>  

### <a name="azure-data-factory"></a><span data-ttu-id="caa08-126">Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="caa08-126">Azure Data Factory</span></span>
<span data-ttu-id="caa08-127">Fábrica de dados é um serviço de integração de dados baseado na nuvem que orquestra e automatiza Olá **movimento** e **transformação** de dados.</span><span class="sxs-lookup"><span data-stu-id="caa08-127">Data Factory is a cloud-based data integration service that orchestrates and automates hello **movement** and **transformation** of data.</span></span> <span data-ttu-id="caa08-128">Pode criar soluções de integração de dados utilizando o Azure Data Factory que podem ingerir dados a partir de vários arquivos de dados, dados Olá/processo transformar e publicar Olá resultado dados toohello os arquivos de dados.</span><span class="sxs-lookup"><span data-stu-id="caa08-128">You can create data integration solutions using Azure Data Factory that can ingest data from various data stores, transform/process hello data, and publish hello result data toohello data stores.</span></span>

<span data-ttu-id="caa08-129">Serviço fábrica de dados permite-lhe toocreate pipelines de dados que moverem e transforme dados e, em seguida, execute pipelines Olá numa agenda especificada (hora a hora, diariamente, semanalmente, etc.).</span><span class="sxs-lookup"><span data-stu-id="caa08-129">Data Factory service allows you toocreate data pipelines that move and transform data, and then run hello pipelines on a specified schedule (hourly, daily, weekly, etc.).</span></span> <span data-ttu-id="caa08-130">Também fornece linhagem de Olá visualizações otimizadas toodisplay e as dependências entre os seus pipelines de dados e monitorizar todos os seus pipelines de dados de um problemas de identificar tooeasily vista unificada única e alertas de monitorização de configuração.</span><span class="sxs-lookup"><span data-stu-id="caa08-130">It also provides rich visualizations toodisplay hello lineage and dependencies between your data pipelines, and monitor all your data pipelines from a single unified view tooeasily pinpoint issues and setup monitoring alerts.</span></span>

<span data-ttu-id="caa08-131">Consulte [introdução tooAzure Data Factory](data-factory-introduction.md) e [construir o seu primeiro pipeline](data-factory-build-your-first-pipeline.md) artigos tooquickly introdução ao hello do serviço Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="caa08-131">See [Introduction tooAzure Data Factory](data-factory-introduction.md) and [Build your first pipeline](data-factory-build-your-first-pipeline.md) articles tooquickly get started with hello Azure Data Factory service.</span></span>

### <a name="data-factory-and-machine-learning-together"></a><span data-ttu-id="caa08-132">Fábrica de dados e de Machine Learning em conjunto</span><span class="sxs-lookup"><span data-stu-id="caa08-132">Data Factory and Machine Learning together</span></span>
<span data-ttu-id="caa08-133">Ativa a fábrica de dados do Azure tooeasily Criar pipelines que utilizam um publicados [Azure Machine Learning] [ azure-machine-learning] web service para Análise Preditiva.</span><span class="sxs-lookup"><span data-stu-id="caa08-133">Azure Data Factory enables you tooeasily create pipelines that use a published [Azure Machine Learning][azure-machine-learning] web service for predictive analytics.</span></span> <span data-ttu-id="caa08-134">Utilizar Olá **atividade de execução de lote** um pipeline do Azure Data Factory, pode invocar um predições do toomake de serviço web do Azure ML em dados de Olá no batch.</span><span class="sxs-lookup"><span data-stu-id="caa08-134">Using hello **Batch Execution Activity** in an Azure Data Factory pipeline, you can invoke an Azure ML web service toomake predictions on hello data in batch.</span></span> <span data-ttu-id="caa08-135">Consulte [invocar do Azure ML web service utilizar Olá atividade de execução de lote](#invoking-an-azure-ml-web-service-using-the-batch-execution-activity) secção para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="caa08-135">See [Invoking an Azure ML web service using hello Batch Execution Activity](#invoking-an-azure-ml-web-service-using-the-batch-execution-activity) section for details.</span></span>

<span data-ttu-id="caa08-136">Ao longo do tempo, os modelos preditivos de Olá nas experimentações classificação do Azure ML Olá necessário toobe retrained utilizando conjuntos de dados de entrada novo.</span><span class="sxs-lookup"><span data-stu-id="caa08-136">Over time, hello predictive models in hello Azure ML scoring experiments need toobe retrained using new input datasets.</span></span> <span data-ttu-id="caa08-137">Pode a reparametrização de um modelo do Azure ML de um pipeline do Data Factory efetuando Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="caa08-137">You can retrain an Azure ML model from a Data Factory pipeline by doing hello following steps:</span></span>

1. <span data-ttu-id="caa08-138">Publica a experimentação de preparação de Olá (experimentação preditiva não) como um serviço web.</span><span class="sxs-lookup"><span data-stu-id="caa08-138">Publish hello training experiment (not predictive experiment) as a web service.</span></span> <span data-ttu-id="caa08-139">Efetue este passo na Olá Azure ML Studio tal como fez experimentação preditiva tooexpose como um serviço web no cenário anterior Olá.</span><span class="sxs-lookup"><span data-stu-id="caa08-139">You do this step in hello Azure ML Studio as you did tooexpose predictive experiment as a web service in hello previous scenario.</span></span>
2. <span data-ttu-id="caa08-140">Utilize Olá atividade de execução de lote do Azure ML tooinvoke Olá web serviço para experimentação de preparação de Olá.</span><span class="sxs-lookup"><span data-stu-id="caa08-140">Use hello Azure ML Batch Execution Activity tooinvoke hello web service for hello training experiment.</span></span> <span data-ttu-id="caa08-141">Basicamente, pode utilizar tooinvoke da atividade de execução de lote do Azure ML Olá o serviço web de preparação e a classificação de serviço web.</span><span class="sxs-lookup"><span data-stu-id="caa08-141">Basically, you can use hello Azure ML Batch Execution activity tooinvoke both training web service and scoring web service.</span></span>

<span data-ttu-id="caa08-142">Depois de terminar com reparametrização, atualizar Olá a classificação do serviço web (experimentação preditiva exposta como um serviço web) com o modelo treinado recentemente Olá utilizando Olá **da atividade de recursos de atualização do Azure ML**.</span><span class="sxs-lookup"><span data-stu-id="caa08-142">After you are done with retraining, update hello scoring web service (predictive experiment exposed as a web service) with hello newly trained model by using hello **Azure ML Update Resource Activity**.</span></span> <span data-ttu-id="caa08-143">Consulte [atualizar modelos de atividade do recurso da atualização](data-factory-azure-ml-update-resource-activity.md) artigo para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="caa08-143">See [Updating models using Update Resource Activity](data-factory-azure-ml-update-resource-activity.md) article for details.</span></span>

## <a name="invoking-a-web-service-using-batch-execution-activity"></a><span data-ttu-id="caa08-144">Invocar um serviço web utilizando a atividade de execução de lote</span><span class="sxs-lookup"><span data-stu-id="caa08-144">Invoking a web service using Batch Execution Activity</span></span>
<span data-ttu-id="caa08-145">Utilizar o movimento de dados do Azure Data Factory tooorchestrate e processamento e, em seguida, efetuar a execução de lote através do Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="caa08-145">You use Azure Data Factory tooorchestrate data movement and processing, and then perform batch execution using Azure Machine Learning.</span></span> <span data-ttu-id="caa08-146">Seguem-se passos de nível superior de Olá:</span><span class="sxs-lookup"><span data-stu-id="caa08-146">Here are hello top-level steps:</span></span>

1. <span data-ttu-id="caa08-147">Crie um serviço ligado do Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="caa08-147">Create an Azure Machine Learning linked service.</span></span> <span data-ttu-id="caa08-148">É necessário Olá os seguintes valores:</span><span class="sxs-lookup"><span data-stu-id="caa08-148">You need hello following values:</span></span>

   1. <span data-ttu-id="caa08-149">**URI de pedido** para Olá API de execução do Batch.</span><span class="sxs-lookup"><span data-stu-id="caa08-149">**Request URI** for hello Batch Execution API.</span></span> <span data-ttu-id="caa08-150">Pode encontrar Olá URI pedido clicando Olá **de execução de lote** ligação na página de serviços web Olá.</span><span class="sxs-lookup"><span data-stu-id="caa08-150">You can find hello Request URI by clicking hello **BATCH EXECUTION** link in hello web services page.</span></span>
   2. <span data-ttu-id="caa08-151">**Chave de API** para Olá publicado serviço web Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="caa08-151">**API key** for hello published Azure Machine Learning web service.</span></span> <span data-ttu-id="caa08-152">Pode encontrar a chave de API de Olá, clicando em serviço web Olá que tiver publicado.</span><span class="sxs-lookup"><span data-stu-id="caa08-152">You can find hello API key by clicking hello web service that you have published.</span></span>
   3. <span data-ttu-id="caa08-153">Olá utilize **AzureMLBatchExecution** atividade.</span><span class="sxs-lookup"><span data-stu-id="caa08-153">Use hello **AzureMLBatchExecution** activity.</span></span>

      ![Dashboard do Machine Learning](./media/data-factory-azure-ml-batch-execution-activity/AzureMLDashboard.png)

      ![URI do batch](./media/data-factory-azure-ml-batch-execution-activity/batch-uri.png)

### <a name="scenario-experiments-using-web-service-inputsoutputs-that-refer-toodata-in-azure-blob-storage"></a><span data-ttu-id="caa08-156">Cenário: Experimentações com o Web service entradas/saídas que se referem toodata no Blob Storage do Azure</span><span class="sxs-lookup"><span data-stu-id="caa08-156">Scenario: Experiments using Web service inputs/outputs that refer toodata in Azure Blob Storage</span></span>
<span data-ttu-id="caa08-157">Neste cenário, Olá serviço Web do Azure Machine Learning torna predições utilizando os dados de um ficheiro no armazenamento de Blobs do Azure e armazena os resultados de predição de Olá no armazenamento de BLOBs de Olá.</span><span class="sxs-lookup"><span data-stu-id="caa08-157">In this scenario, hello Azure Machine Learning Web service makes predictions using data from a file in an Azure blob storage and stores hello prediction results in hello blob storage.</span></span> <span data-ttu-id="caa08-158">Olá seguinte JSON define um pipeline do Data Factory com uma atividade AzureMLBatchExecution.</span><span class="sxs-lookup"><span data-stu-id="caa08-158">hello following JSON defines a Data Factory pipeline with an AzureMLBatchExecution activity.</span></span> <span data-ttu-id="caa08-159">atividade de Olá tem o conjunto de dados de Olá **DecisionTreeInputBlob** como entrada e **DecisionTreeResultBlob** como saída Olá.</span><span class="sxs-lookup"><span data-stu-id="caa08-159">hello activity has hello dataset **DecisionTreeInputBlob** as input and **DecisionTreeResultBlob** as hello output.</span></span> <span data-ttu-id="caa08-160">Olá **DecisionTreeInputBlob** é transmitida como um serviço web de entrada toohello por utilizando Olá **webServiceInput** propriedade JSON.</span><span class="sxs-lookup"><span data-stu-id="caa08-160">hello **DecisionTreeInputBlob** is passed as an input toohello web service by using hello **webServiceInput** JSON property.</span></span> <span data-ttu-id="caa08-161">Olá **DecisionTreeResultBlob** é transmitida como um serviço de Web de toohello de saída por utilizando Olá **webServiceOutputs** propriedade JSON.</span><span class="sxs-lookup"><span data-stu-id="caa08-161">hello **DecisionTreeResultBlob** is passed as an output toohello Web service by using hello **webServiceOutputs** JSON property.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="caa08-162">Se o serviço web de Olá demora várias entradas, utilize Olá **webServiceInputs** propriedade em vez de utilizar **webServiceInput**.</span><span class="sxs-lookup"><span data-stu-id="caa08-162">If hello web service takes multiple inputs, use hello **webServiceInputs** property instead of using **webServiceInput**.</span></span> <span data-ttu-id="caa08-163">Consulte Olá [serviço Web requer várias entradas](#web-service-requires-multiple-inputs) secção para obter um exemplo de utilização Olá webServiceInputs propriedade.</span><span class="sxs-lookup"><span data-stu-id="caa08-163">See hello [Web service requires multiple inputs](#web-service-requires-multiple-inputs) section for an example of using hello webServiceInputs property.</span></span>
>
> <span data-ttu-id="caa08-164">Conjuntos de dados que são referenciados por Olá **webServiceInput**/**webServiceInputs** e **webServiceOutputs** propriedades (no  **typeProperties**) também devem ser incluídas no Olá atividade **entradas** e **produz**.</span><span class="sxs-lookup"><span data-stu-id="caa08-164">Datasets that are referenced by hello **webServiceInput**/**webServiceInputs** and **webServiceOutputs** properties (in **typeProperties**) must also be included in hello Activity **inputs** and **outputs**.</span></span>
>
> <span data-ttu-id="caa08-165">Na sua experimentação do Azure ML, entrada de serviço web e portas de saída e parâmetros globais têm nomes predefinidos ("input1", "input2") que pode personalizar.</span><span class="sxs-lookup"><span data-stu-id="caa08-165">In your Azure ML experiment, web service input and output ports and global parameters have default names ("input1", "input2") that you can customize.</span></span> <span data-ttu-id="caa08-166">os nomes de Olá que utiliza para webServiceInputs, webServiceOutputs e globalParameters definições têm de corresponder exatamente nomes Olá nas experimentações Olá.</span><span class="sxs-lookup"><span data-stu-id="caa08-166">hello names you use for webServiceInputs, webServiceOutputs, and globalParameters settings must exactly match hello names in hello experiments.</span></span> <span data-ttu-id="caa08-167">Pode ver o payload de pedido do exemplo Olá na página de ajuda de execução de lote de Olá para o mapeamento de Olá esperado de tooverify de ponto final do Azure ML.</span><span class="sxs-lookup"><span data-stu-id="caa08-167">You can view hello sample request payload on hello Batch Execution Help page for your Azure ML endpoint tooverify hello expected mapping.</span></span>
>
>

```JSON
{
  "name": "PredictivePipeline",
  "properties": {
    "description": "use AzureML model",
    "activities": [
      {
        "name": "MLActivity",
        "type": "AzureMLBatchExecution",
        "description": "prediction analysis on batch input",
        "inputs": [
          {
            "name": "DecisionTreeInputBlob"
          }
        ],
        "outputs": [
          {
            "name": "DecisionTreeResultBlob"
          }
        ],
        "linkedServiceName": "MyAzureMLLinkedService",
        "typeProperties":
        {
            "webServiceInput": "DecisionTreeInputBlob",
            "webServiceOutputs": {
                "output1": "DecisionTreeResultBlob"
            }                
        },
        "policy": {
          "concurrency": 3,
          "executionPriorityOrder": "NewestFirst",
          "retry": 1,
          "timeout": "02:00:00"
        }
      }
    ],
    "start": "2016-02-13T00:00:00Z",
    "end": "2016-02-14T00:00:00Z"
  }
}
```
> [!NOTE]
> <span data-ttu-id="caa08-168">Apenas entradas e saídas da atividade de AzureMLBatchExecution Olá podem ser transmitidas como parâmetros toohello serviço Web.</span><span class="sxs-lookup"><span data-stu-id="caa08-168">Only inputs and outputs of hello AzureMLBatchExecution activity can be passed as parameters toohello Web service.</span></span> <span data-ttu-id="caa08-169">Por exemplo, Olá acima fragmento JSON, DecisionTreeInputBlob é uma entrada toohello AzureMLBatchExecution atividade, que é transmitida como um serviço Web de entrada toohello através do parâmetro webServiceInput.</span><span class="sxs-lookup"><span data-stu-id="caa08-169">For example, in hello above JSON snippet, DecisionTreeInputBlob is an input toohello AzureMLBatchExecution activity, which is passed as an input toohello Web service via webServiceInput parameter.</span></span>   
>
>

### <a name="example"></a><span data-ttu-id="caa08-170">Exemplo</span><span class="sxs-lookup"><span data-stu-id="caa08-170">Example</span></span>
<span data-ttu-id="caa08-171">Toohold de armazenamento do Azure este exemplo utiliza ambos Olá dados de entrada e de saída.</span><span class="sxs-lookup"><span data-stu-id="caa08-171">This example uses Azure Storage toohold both hello input and output data.</span></span>

<span data-ttu-id="caa08-172">Recomendamos que leia Olá [construir o seu primeiro pipeline com o Data Factory] [ adf-build-1st-pipeline] tutorial antes de passar neste exemplo.</span><span class="sxs-lookup"><span data-stu-id="caa08-172">We recommend that you go through hello [Build your first pipeline with Data Factory][adf-build-1st-pipeline] tutorial before going through this example.</span></span> <span data-ttu-id="caa08-173">Utilize artefactos de fábrica de dados de toocreate do Olá Editor do Data Factory (serviços ligados, conjuntos de dados, pipeline) neste exemplo.</span><span class="sxs-lookup"><span data-stu-id="caa08-173">Use hello Data Factory Editor toocreate Data Factory artifacts (linked services, datasets, pipeline) in this example.</span></span>   

1. <span data-ttu-id="caa08-174">Criar um **serviço ligado** para sua **Storage do Azure**.</span><span class="sxs-lookup"><span data-stu-id="caa08-174">Create a **linked service** for your **Azure Storage**.</span></span> <span data-ttu-id="caa08-175">Se hello ficheiros de entrada e saídos estão em contas de armazenamento diferente, terá dois serviços ligados.</span><span class="sxs-lookup"><span data-stu-id="caa08-175">If hello input and output files are in different storage accounts, you need two linked services.</span></span> <span data-ttu-id="caa08-176">Eis um exemplo JSON:</span><span class="sxs-lookup"><span data-stu-id="caa08-176">Here is a JSON example:</span></span>

    ```JSON
    {
      "name": "StorageLinkedService",
      "properties": {
        "type": "AzureStorage",
        "typeProperties": {
          "connectionString": "DefaultEndpointsProtocol=https;AccountName=[acctName];AccountKey=[acctKey]"
        }
      }
    }
    ```
2. <span data-ttu-id="caa08-177">Criar Olá **entrada** do Azure Data Factory **dataset**.</span><span class="sxs-lookup"><span data-stu-id="caa08-177">Create hello **input** Azure Data Factory **dataset**.</span></span> <span data-ttu-id="caa08-178">Ao contrário de algumas outros Data Factory conjuntos de dados, estes conjuntos de dados tem de conter ambos **folderPath** e **fileName** valores.</span><span class="sxs-lookup"><span data-stu-id="caa08-178">Unlike some other Data Factory datasets, these datasets must contain both **folderPath** and **fileName** values.</span></span> <span data-ttu-id="caa08-179">Pode utilizar partições toocause cada tooprocess (cada setor de dados) de execução do batch ou produzir entrada exclusiva e ficheiros de saída.</span><span class="sxs-lookup"><span data-stu-id="caa08-179">You can use partitioning toocause each batch execution (each data slice) tooprocess or produce unique input and output files.</span></span> <span data-ttu-id="caa08-180">Poderá ser necessário tooinclude algumas Olá tootransform de atividade a montante introduzir no formato de ficheiro CSV Olá e colocá-lo na conta de armazenamento Olá para cada setor.</span><span class="sxs-lookup"><span data-stu-id="caa08-180">You may need tooinclude some upstream activity tootransform hello input into hello CSV file format and place it in hello storage account for each slice.</span></span> <span data-ttu-id="caa08-181">Nesse caso, não deverá incluir Olá **externo** e **externalData** definições mostradas na Olá seguinte exemplo e seu DecisionTreeInputBlob seria Olá conjunto de dados de saída de uma atividade diferente.</span><span class="sxs-lookup"><span data-stu-id="caa08-181">In that case, you would not include hello **external** and **externalData** settings shown in hello following example, and your DecisionTreeInputBlob would be hello output dataset of a different Activity.</span></span>

    ```JSON
    {
      "name": "DecisionTreeInputBlob",
      "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
          "folderPath": "azuremltesting/input",
          "fileName": "in.csv",
          "format": {
            "type": "TextFormat",
            "columnDelimiter": ","
          }
        },
        "external": true,
        "availability": {
          "frequency": "Day",
          "interval": 1
        },
        "policy": {
          "externalData": {
            "retryInterval": "00:01:00",
            "retryTimeout": "00:10:00",
            "maximumRetry": 3
          }
        }
      }
    }
    ```

    <span data-ttu-id="caa08-182">O ficheiro csv de entrada tem de ter linha de cabeçalho de coluna Olá.</span><span class="sxs-lookup"><span data-stu-id="caa08-182">Your input csv file must have hello column header row.</span></span> <span data-ttu-id="caa08-183">Se estiver a utilizar Olá **atividade de cópia** toocreate/mover Olá csv para o armazenamento de BLOBs de Olá, deve definir a propriedade de receptores de Olá **blobWriterAddHeader** demasiado**verdadeiro**.</span><span class="sxs-lookup"><span data-stu-id="caa08-183">If you are using hello **Copy Activity** toocreate/move hello csv into hello blob storage, you should set hello sink property **blobWriterAddHeader** too**true**.</span></span> <span data-ttu-id="caa08-184">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="caa08-184">For example:</span></span>

    ```JSON
    sink:
    {
        "type": "BlobSink",     
        "blobWriterAddHeader": true
    }
    ```

    <span data-ttu-id="caa08-185">Se um ficheiro csv Olá não tem uma linha de cabeçalho de Olá, poderá ver Olá seguinte erro: **erro na atividade: erro ao ler a cadeia. Token inesperado: StartObject. Caminho ', linha 1, posição 1**.</span><span class="sxs-lookup"><span data-stu-id="caa08-185">If hello csv file does not have hello header row, you may see hello following error: **Error in Activity: Error reading string. Unexpected token: StartObject. Path '', line 1, position 1**.</span></span>
3. <span data-ttu-id="caa08-186">Criar Olá **saída** do Azure Data Factory **dataset**.</span><span class="sxs-lookup"><span data-stu-id="caa08-186">Create hello **output** Azure Data Factory **dataset**.</span></span> <span data-ttu-id="caa08-187">Este exemplo utiliza a criação de partições toocreate um caminho de saída exclusivo para cada execução do setor.</span><span class="sxs-lookup"><span data-stu-id="caa08-187">This example uses partitioning toocreate a unique output path for each slice execution.</span></span> <span data-ttu-id="caa08-188">Sem a criação de partições Olá, atividade Olá substituiria o ficheiro Olá.</span><span class="sxs-lookup"><span data-stu-id="caa08-188">Without hello partitioning, hello activity would overwrite hello file.</span></span>

    ```JSON
    {
      "name": "DecisionTreeResultBlob",
      "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
          "folderPath": "azuremltesting/scored/{folderpart}/",
          "fileName": "{filepart}result.csv",
          "partitionedBy": [
            {
              "name": "folderpart",
              "value": {
                "type": "DateTime",
                "date": "SliceStart",
                "format": "yyyyMMdd"
              }
            },
            {
              "name": "filepart",
              "value": {
                "type": "DateTime",
                "date": "SliceStart",
                "format": "HHmmss"
              }
            }
          ],
          "format": {
            "type": "TextFormat",
            "columnDelimiter": ","
          }
        },
        "availability": {
          "frequency": "Day",
          "interval": 15
        }
      }
    }
    ```
4. <span data-ttu-id="caa08-189">Criar um **serviço ligado** do tipo: **AzureMLLinkedService**, fornecendo a chave de API de Olá e URL da execução de lote de modelo.</span><span class="sxs-lookup"><span data-stu-id="caa08-189">Create a **linked service** of type: **AzureMLLinkedService**, providing hello API key and model batch execution URL.</span></span>

    ```JSON
    {
      "name": "MyAzureMLLinkedService",
      "properties": {
        "type": "AzureML",
        "typeProperties": {
          "mlEndpoint": "https://[batch execution endpoint]/jobs",
          "apiKey": "[apikey]"
        }
      }
    }
    ```
5. <span data-ttu-id="caa08-190">Por fim, criar um pipeline que contém um **AzureMLBatchExecution** atividade.</span><span class="sxs-lookup"><span data-stu-id="caa08-190">Finally, author a pipeline containing an **AzureMLBatchExecution** Activity.</span></span> <span data-ttu-id="caa08-191">Em runtime, o pipeline efetua Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="caa08-191">At runtime, pipeline performs hello following steps:</span></span>

   1. <span data-ttu-id="caa08-192">Obtém a localização de Olá do ficheiro de entrada Olá dos conjuntos de dados de entrada.</span><span class="sxs-lookup"><span data-stu-id="caa08-192">Gets hello location of hello input file from your input datasets.</span></span>
   2. <span data-ttu-id="caa08-193">Invoca a execução de lote do Azure Machine Learning Olá API</span><span class="sxs-lookup"><span data-stu-id="caa08-193">Invokes hello Azure Machine Learning batch execution API</span></span>
   3. <span data-ttu-id="caa08-194">Cópias Olá blob toohello batch execução saída fornecido no seu conjunto de dados de saída.</span><span class="sxs-lookup"><span data-stu-id="caa08-194">Copies hello batch execution output toohello blob given in your output dataset.</span></span>

      > [!NOTE]
      > <span data-ttu-id="caa08-195">Atividade de AzureMLBatchExecution pode ter zero ou mais entradas e saídas de um ou mais.</span><span class="sxs-lookup"><span data-stu-id="caa08-195">AzureMLBatchExecution activity can have zero or more inputs and one or more outputs.</span></span>
      >
      >

    ```JSON
    {
        "name": "PredictivePipeline",
        "properties": {
            "description": "use AzureML model",
            "activities": [
            {
                "name": "MLActivity",
                "type": "AzureMLBatchExecution",
                "description": "prediction analysis on batch input",
                "inputs": [
                {
                    "name": "DecisionTreeInputBlob"
                }
                ],
                "outputs": [
                {
                    "name": "DecisionTreeResultBlob"
                }
                ],
                "linkedServiceName": "MyAzureMLLinkedService",
                "typeProperties":
                {
                    "webServiceInput": "DecisionTreeInputBlob",
                    "webServiceOutputs": {
                        "output1": "DecisionTreeResultBlob"
                    }                
                },
                "policy": {
                    "concurrency": 3,
                    "executionPriorityOrder": "NewestFirst",
                    "retry": 1,
                    "timeout": "02:00:00"
                }
            }
            ],
            "start": "2016-02-13T00:00:00Z",
            "end": "2016-02-14T00:00:00Z"
        }
    }
    ```

      <span data-ttu-id="caa08-196">Ambos **iniciar** e **final** DateTime tem de constar [formato ISO](http://en.wikipedia.org/wiki/ISO_8601).</span><span class="sxs-lookup"><span data-stu-id="caa08-196">Both **start** and **end** datetimes must be in [ISO format](http://en.wikipedia.org/wiki/ISO_8601).</span></span> <span data-ttu-id="caa08-197">Por exemplo: 2014-10-14T16:32:41Z.</span><span class="sxs-lookup"><span data-stu-id="caa08-197">For example: 2014-10-14T16:32:41Z.</span></span> <span data-ttu-id="caa08-198">Olá **final** tempo é opcional.</span><span class="sxs-lookup"><span data-stu-id="caa08-198">hello **end** time is optional.</span></span> <span data-ttu-id="caa08-199">Se não especificar valor de Olá **final** propriedade, esta é calculada como "**início + 48 horas.**"</span><span class="sxs-lookup"><span data-stu-id="caa08-199">If you do not specify value for hello **end** property, it is calculated as "**start + 48 hours.**"</span></span> <span data-ttu-id="caa08-200">pipeline de Olá toorun indefinidamente, especifique **9999-09-09** como valor de Olá para Olá **final** propriedade.</span><span class="sxs-lookup"><span data-stu-id="caa08-200">toorun hello pipeline indefinitely, specify **9999-09-09** as hello value for hello **end** property.</span></span> <span data-ttu-id="caa08-201">Veja [Referência de Processamento de Scripts JSON](https://msdn.microsoft.com/library/dn835050.aspx) para obter mais detalhes sobre as propriedades de JSON.</span><span class="sxs-lookup"><span data-stu-id="caa08-201">See [JSON Scripting Reference](https://msdn.microsoft.com/library/dn835050.aspx) for details about JSON properties.</span></span>

      > [!NOTE]
      > <span data-ttu-id="caa08-202">A especificação de entrada para a atividade de AzureMLBatchExecution Olá é opcional.</span><span class="sxs-lookup"><span data-stu-id="caa08-202">Specifying input for hello AzureMLBatchExecution activity is optional.</span></span>
      >
      >

### <a name="scenario-experiments-using-readerwriter-modules-toorefer-toodata-in-various-storages"></a><span data-ttu-id="caa08-203">Cenário: Experimentações com módulos de leitor/escritor toorefer toodata no armazenamento de vários</span><span class="sxs-lookup"><span data-stu-id="caa08-203">Scenario: Experiments using Reader/Writer Modules toorefer toodata in various storages</span></span>
<span data-ttu-id="caa08-204">Outro cenário típico possível quando criar experimentações do Azure ML é toouse leitor e escritor módulos.</span><span class="sxs-lookup"><span data-stu-id="caa08-204">Another common scenario when creating Azure ML experiments is toouse Reader and Writer modules.</span></span> <span data-ttu-id="caa08-205">módulo leitor de Olá é utilizado tooload dados para uma experimentação e módulo de escritor Olá é toosave dados a partir das suas experimentações.</span><span class="sxs-lookup"><span data-stu-id="caa08-205">hello reader module is used tooload data into an experiment and hello writer module is toosave data from your experiments.</span></span> <span data-ttu-id="caa08-206">Para obter detalhes sobre o leitor e escritor módulos, consulte [leitor](https://msdn.microsoft.com/library/azure/dn905997.aspx) e [escritor](https://msdn.microsoft.com/library/azure/dn905984.aspx) tópicos da biblioteca MSDN.</span><span class="sxs-lookup"><span data-stu-id="caa08-206">For details about reader and writer modules, see [Reader](https://msdn.microsoft.com/library/azure/dn905997.aspx) and [Writer](https://msdn.microsoft.com/library/azure/dn905984.aspx) topics on MSDN Library.</span></span>     

<span data-ttu-id="caa08-207">Quando utilizar módulos de leitor e escritor Olá, é boa prática toouse um parâmetro de serviço Web para cada propriedade estes módulos de leitor/escritor.</span><span class="sxs-lookup"><span data-stu-id="caa08-207">When using hello reader and writer modules, it is good practice toouse a Web service parameter for each property of these reader/writer modules.</span></span> <span data-ttu-id="caa08-208">Estes parâmetros web permitem-lhe os valores de Olá tooconfigure durante o tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="caa08-208">These web parameters enable you tooconfigure hello values during runtime.</span></span> <span data-ttu-id="caa08-209">Por exemplo, pode criar uma experimentação com um módulo leitor de que utiliza uma base de dados do SQL do Azure: XXX.database.windows.net.</span><span class="sxs-lookup"><span data-stu-id="caa08-209">For example, you could create an experiment with a reader module that uses an Azure SQL Database: XXX.database.windows.net.</span></span> <span data-ttu-id="caa08-210">Depois de implementar o serviço web de Olá, quer tooenable consumidores Olá Olá web service toospecify outro servidor de SQL do Azure chamado YYY.database.windows.net.</span><span class="sxs-lookup"><span data-stu-id="caa08-210">After hello web service has been deployed, you want tooenable hello consumers of hello web service toospecify another Azure SQL Server called YYY.database.windows.net.</span></span> <span data-ttu-id="caa08-211">Pode utilizar um tooallow de parâmetro de serviço Web toobe este valor configurado.</span><span class="sxs-lookup"><span data-stu-id="caa08-211">You can use a Web service parameter tooallow this value toobe configured.</span></span>

> [!NOTE]
> <span data-ttu-id="caa08-212">Entrada de serviço Web e de saída são diferentes dos parâmetros de serviço Web.</span><span class="sxs-lookup"><span data-stu-id="caa08-212">Web service input and output are different from Web service parameters.</span></span> <span data-ttu-id="caa08-213">No primeiro cenário Olá, constatou como uma entrada e saída podem ser especificados para um serviço Web do Azure ML.</span><span class="sxs-lookup"><span data-stu-id="caa08-213">In hello first scenario, you have seen how an input and output can be specified for an Azure ML Web service.</span></span> <span data-ttu-id="caa08-214">Neste cenário, passar parâmetros para um serviço Web que correspondem tooproperties dos módulos de leitor/escritor.</span><span class="sxs-lookup"><span data-stu-id="caa08-214">In this scenario, you pass parameters for a Web service that correspond tooproperties of reader/writer modules.</span></span>
>
>

<span data-ttu-id="caa08-215">Vamos ver um cenário de utilização de parâmetros de serviço Web.</span><span class="sxs-lookup"><span data-stu-id="caa08-215">Let's look at a scenario for using Web service parameters.</span></span> <span data-ttu-id="caa08-216">Tem um serviço implementado de web Azure Machine Learning que utiliza uma data de tooread do módulo leitor a partir de uma das origens de dados de Olá suportadas pelo Azure Machine Learning (por exemplo: SQL Database do Azure).</span><span class="sxs-lookup"><span data-stu-id="caa08-216">You have a deployed Azure Machine Learning web service that uses a reader module tooread data from one of hello data sources supported by Azure Machine Learning (for example: Azure SQL Database).</span></span> <span data-ttu-id="caa08-217">Após a execução de lote Olá é efetuada, resultados de Olá são escritos utilizando um módulo de escritor (SQL Database do Azure).</span><span class="sxs-lookup"><span data-stu-id="caa08-217">After hello batch execution is performed, hello results are written using a Writer module (Azure SQL Database).</span></span>  <span data-ttu-id="caa08-218">Não existem entradas de serviço web e saídas são definidas nas experimentações Olá.</span><span class="sxs-lookup"><span data-stu-id="caa08-218">No web service inputs and outputs are defined in hello experiments.</span></span> <span data-ttu-id="caa08-219">Neste caso, recomendamos que configure parâmetros de serviço web relevantes para módulos de leitor e escritor Olá.</span><span class="sxs-lookup"><span data-stu-id="caa08-219">In this case, we recommend that you configure relevant web service parameters for hello reader and writer modules.</span></span> <span data-ttu-id="caa08-220">Esta configuração permite Olá leitor/escritor toobe módulos configurada quando utilizando Olá AzureMLBatchExecution atividade.</span><span class="sxs-lookup"><span data-stu-id="caa08-220">This configuration allows hello reader/writer modules toobe configured when using hello AzureMLBatchExecution activity.</span></span> <span data-ttu-id="caa08-221">Especifique os parâmetros do serviço Web na Olá **globalParameters** secção JSON da atividade Olá da seguinte forma.</span><span class="sxs-lookup"><span data-stu-id="caa08-221">You specify Web service parameters in hello **globalParameters** section in hello activity JSON as follows.</span></span>

```JSON
"typeProperties": {
    "globalParameters": {
        "Param 1": "Value 1",
        "Param 2": "Value 2"
    }
}
```

<span data-ttu-id="caa08-222">Também pode utilizar [funções da fábrica de dados](data-factory-functions-variables.md) em transmitir parâmetros de serviço Web, conforme mostrado no seguinte exemplo de Olá de valores para Olá:</span><span class="sxs-lookup"><span data-stu-id="caa08-222">You can also use [Data Factory Functions](data-factory-functions-variables.md) in passing values for hello Web service parameters as shown in hello following example:</span></span>

```JSON
"typeProperties": {
    "globalParameters": {
       "Database query": "$$Text.Format('SELECT * FROM myTable WHERE timeColumn = \\'{0:yyyy-MM-dd HH:mm:ss}\\'', Time.AddHours(WindowStart, 0))"
    }
}
```

> [!NOTE]
> <span data-ttu-id="caa08-223">parâmetros de serviço Web de Olá são maiúsculas e minúsculas, por isso, certifique-se de que os nomes de Olá que especificar na atividade de Olá JSON corresponde Olá aqueles exposta pelo Olá serviço Web.</span><span class="sxs-lookup"><span data-stu-id="caa08-223">hello Web service parameters are case-sensitive, so ensure that hello names you specify in hello activity JSON match hello ones exposed by hello Web service.</span></span>
>
>

### <a name="using-a-reader-module-tooread-data-from-multiple-files-in-azure-blob"></a><span data-ttu-id="caa08-224">Utilizar uma data de tooread do módulo leitor de vários ficheiros no Blob do Azure</span><span class="sxs-lookup"><span data-stu-id="caa08-224">Using a Reader module tooread data from multiple files in Azure Blob</span></span>
<span data-ttu-id="caa08-225">Macrodados pipelines com atividades, tais como o Pig e ramo de registo pode produzir uma ou mais ficheiros de saída com nenhuma extensão.</span><span class="sxs-lookup"><span data-stu-id="caa08-225">Big data pipelines with activities such as Pig and Hive can produce one or more output files with no extensions.</span></span> <span data-ttu-id="caa08-226">Por exemplo, quando especificar uma tabela do Hive externa, dados de Olá para a tabela de Hive externo Olá podem ser armazenados no blob storage do Azure com Olá seguir 000000_0 de nome.</span><span class="sxs-lookup"><span data-stu-id="caa08-226">For example, when you specify an external Hive table, hello data for hello external Hive table can be stored in Azure blob storage with hello following name 000000_0.</span></span> <span data-ttu-id="caa08-227">Pode utilizar o módulo de leitor de Olá no tooread experimentação vários ficheiros e utilizá-los para as predições.</span><span class="sxs-lookup"><span data-stu-id="caa08-227">You can use hello reader module in an experiment tooread multiple files, and use them for predictions.</span></span>

<span data-ttu-id="caa08-228">Quando o módulo de leitor de Olá numa experimentação do Azure Machine Learning, pode especificar o Blob do Azure como entrada.</span><span class="sxs-lookup"><span data-stu-id="caa08-228">When using hello reader module in an Azure Machine Learning experiment, you can specify Azure Blob as an input.</span></span> <span data-ttu-id="caa08-229">ficheiros de Olá no Olá blob storage do Azure podem ser ficheiros de saída Olá (exemplo: 000000_0) que são produzidos pelo script Pig e ramo de registo em execução no HDInsight.</span><span class="sxs-lookup"><span data-stu-id="caa08-229">hello files in hello Azure blob storage can be hello output files (Example: 000000_0) that are produced by a Pig and Hive script running on HDInsight.</span></span> <span data-ttu-id="caa08-230">Olá módulo leitor permite-lhe ficheiros tooread (com nenhuma extensão) configurando Olá **toocontainer de caminho, diretório/blob**.</span><span class="sxs-lookup"><span data-stu-id="caa08-230">hello reader module allows you tooread files (with no extensions) by configuring hello **Path toocontainer, directory/blob**.</span></span> <span data-ttu-id="caa08-231">Olá **caminho toocontainer** pontos toohello contentor e **diretório/blob** pontos toofolder que contém ficheiros de Olá, conforme mostrado no Olá seguinte imagem.</span><span class="sxs-lookup"><span data-stu-id="caa08-231">hello **Path toocontainer** points toohello container and **directory/blob** points toofolder that contains hello files as shown in hello following image.</span></span> <span data-ttu-id="caa08-232">ou seja, a asterisco Olá \*) **Especifica que todos os ficheiros no contentor de Olá/pasta de Olá (ou seja, dados/aggregateddata/ano = mês/2014-6 /\*)** sejam de leitura como parte da experimentação Olá.</span><span class="sxs-lookup"><span data-stu-id="caa08-232">hello asterisk that is, \*) **specifies that all hello files in hello container/folder (that is, data/aggregateddata/year=2014/month-6/\*)** are read as part of hello experiment.</span></span>

![Propriedades de Blob do Azure](./media/data-factory-create-predictive-pipelines/azure-blob-properties.png)

### <a name="example"></a><span data-ttu-id="caa08-234">Exemplo</span><span class="sxs-lookup"><span data-stu-id="caa08-234">Example</span></span>
#### <a name="pipeline-with-azuremlbatchexecution-activity-with-web-service-parameters"></a><span data-ttu-id="caa08-235">Pipeline com atividade AzureMLBatchExecution com parâmetros de serviço Web</span><span class="sxs-lookup"><span data-stu-id="caa08-235">Pipeline with AzureMLBatchExecution activity with Web Service Parameters</span></span>

```JSON
{
  "name": "MLWithSqlReaderSqlWriter",
  "properties": {
    "description": "Azure ML model with sql azure reader/writer",
    "activities": [
      {
        "name": "MLSqlReaderSqlWriterActivity",
        "type": "AzureMLBatchExecution",
        "description": "test",
        "inputs": [
          {
            "name": "MLSqlInput"
          }
        ],
        "outputs": [
          {
            "name": "MLSqlOutput"
          }
        ],
        "linkedServiceName": "MLSqlReaderSqlWriterDecisionTreeModel",
        "typeProperties":
        {
            "webServiceInput": "MLSqlInput",
            "webServiceOutputs": {
                "output1": "MLSqlOutput"
            }
              "globalParameters": {
                "Database server name": "<myserver>.database.windows.net",
                "Database name": "<database>",
                "Server user account name": "<user name>",
                "Server user account password": "<password>"
              }              
        },
        "policy": {
          "concurrency": 1,
          "executionPriorityOrder": "NewestFirst",
          "retry": 1,
          "timeout": "02:00:00"
        },
      }
    ],
    "start": "2016-02-13T00:00:00Z",
    "end": "2016-02-14T00:00:00Z"
  }
}
```

<span data-ttu-id="caa08-236">No Olá acima exemplo JSON:</span><span class="sxs-lookup"><span data-stu-id="caa08-236">In hello above JSON example:</span></span>

* <span data-ttu-id="caa08-237">Olá implementado o Azure Machine Learning Web service utiliza um leitor e um escritor módulo tooread/escrita de dados do / tooan SQL Database do Azure.</span><span class="sxs-lookup"><span data-stu-id="caa08-237">hello deployed Azure Machine Learning Web service uses a reader and a writer module tooread/write data from/tooan Azure SQL Database.</span></span> <span data-ttu-id="caa08-238">Este serviço Web expõe Olá seguintes quatro parâmetros: nome do servidor, nome de base de dados, nome de conta de utilizador do servidor e palavra-passe de conta de utilizador servidor de base de dados.</span><span class="sxs-lookup"><span data-stu-id="caa08-238">This Web service exposes hello following four parameters:  Database server name, Database name, Server user account name, and Server user account password.</span></span>  
* <span data-ttu-id="caa08-239">Ambos **iniciar** e **final** DateTime tem de constar [formato ISO](http://en.wikipedia.org/wiki/ISO_8601).</span><span class="sxs-lookup"><span data-stu-id="caa08-239">Both **start** and **end** datetimes must be in [ISO format](http://en.wikipedia.org/wiki/ISO_8601).</span></span> <span data-ttu-id="caa08-240">Por exemplo: 2014-10-14T16:32:41Z.</span><span class="sxs-lookup"><span data-stu-id="caa08-240">For example: 2014-10-14T16:32:41Z.</span></span> <span data-ttu-id="caa08-241">Olá **final** tempo é opcional.</span><span class="sxs-lookup"><span data-stu-id="caa08-241">hello **end** time is optional.</span></span> <span data-ttu-id="caa08-242">Se não especificar valor de Olá **final** propriedade, esta é calculada como "**início + 48 horas.**"</span><span class="sxs-lookup"><span data-stu-id="caa08-242">If you do not specify value for hello **end** property, it is calculated as "**start + 48 hours.**"</span></span> <span data-ttu-id="caa08-243">pipeline de Olá toorun indefinidamente, especifique **9999-09-09** como valor de Olá para Olá **final** propriedade.</span><span class="sxs-lookup"><span data-stu-id="caa08-243">toorun hello pipeline indefinitely, specify **9999-09-09** as hello value for hello **end** property.</span></span> <span data-ttu-id="caa08-244">Veja [Referência de Processamento de Scripts JSON](https://msdn.microsoft.com/library/dn835050.aspx) para obter mais detalhes sobre as propriedades de JSON.</span><span class="sxs-lookup"><span data-stu-id="caa08-244">See [JSON Scripting Reference](https://msdn.microsoft.com/library/dn835050.aspx) for details about JSON properties.</span></span>

### <a name="other-scenarios"></a><span data-ttu-id="caa08-245">Outros cenários</span><span class="sxs-lookup"><span data-stu-id="caa08-245">Other scenarios</span></span>
#### <a name="web-service-requires-multiple-inputs"></a><span data-ttu-id="caa08-246">Serviço Web requer várias entradas</span><span class="sxs-lookup"><span data-stu-id="caa08-246">Web service requires multiple inputs</span></span>
<span data-ttu-id="caa08-247">Se o serviço web de Olá demora várias entradas, utilize Olá **webServiceInputs** propriedade em vez de utilizar **webServiceInput**.</span><span class="sxs-lookup"><span data-stu-id="caa08-247">If hello web service takes multiple inputs, use hello **webServiceInputs** property instead of using **webServiceInput**.</span></span> <span data-ttu-id="caa08-248">Conjuntos de dados que são referenciados por Olá **webServiceInputs** também devem ser incluídas no Olá atividade **entradas**.</span><span class="sxs-lookup"><span data-stu-id="caa08-248">Datasets that are referenced by hello **webServiceInputs** must also be included in hello Activity **inputs**.</span></span>

<span data-ttu-id="caa08-249">Na sua experimentação do Azure ML, entrada de serviço web e portas de saída e parâmetros globais têm nomes predefinidos ("input1", "input2") que pode personalizar.</span><span class="sxs-lookup"><span data-stu-id="caa08-249">In your Azure ML experiment, web service input and output ports and global parameters have default names ("input1", "input2") that you can customize.</span></span> <span data-ttu-id="caa08-250">os nomes de Olá que utiliza para webServiceInputs, webServiceOutputs e globalParameters definições têm de corresponder exatamente nomes Olá nas experimentações Olá.</span><span class="sxs-lookup"><span data-stu-id="caa08-250">hello names you use for webServiceInputs, webServiceOutputs, and globalParameters settings must exactly match hello names in hello experiments.</span></span> <span data-ttu-id="caa08-251">Pode ver o payload de pedido do exemplo Olá na página de ajuda de execução de lote de Olá para o mapeamento de Olá esperado de tooverify de ponto final do Azure ML.</span><span class="sxs-lookup"><span data-stu-id="caa08-251">You can view hello sample request payload on hello Batch Execution Help page for your Azure ML endpoint tooverify hello expected mapping.</span></span>

```JSON
{
    "name": "PredictivePipeline",
    "properties": {
        "description": "use AzureML model",
        "activities": [{
            "name": "MLActivity",
            "type": "AzureMLBatchExecution",
            "description": "prediction analysis on batch input",
            "inputs": [{
                "name": "inputDataset1"
            }, {
                "name": "inputDataset2"
            }],
            "outputs": [{
                "name": "outputDataset"
            }],
            "linkedServiceName": "MyAzureMLLinkedService",
            "typeProperties": {
                "webServiceInputs": {
                    "input1": "inputDataset1",
                    "input2": "inputDataset2"
                },
                "webServiceOutputs": {
                    "output1": "outputDataset"
                }
            },
            "policy": {
                "concurrency": 3,
                "executionPriorityOrder": "NewestFirst",
                "retry": 1,
                "timeout": "02:00:00"
            }
        }],
        "start": "2016-02-13T00:00:00Z",
        "end": "2016-02-14T00:00:00Z"
    }
}
```

#### <a name="web-service-does-not-require-an-input"></a><span data-ttu-id="caa08-252">Serviço Web não necessita de uma entrada</span><span class="sxs-lookup"><span data-stu-id="caa08-252">Web Service does not require an input</span></span>
<span data-ttu-id="caa08-253">Serviços do web de execução de lote do Azure ML pode ser utilizado toorun quaisquer fluxos de trabalho, por exemplo R ou scripts do Python, que pode não necessitar de quaisquer entradas.</span><span class="sxs-lookup"><span data-stu-id="caa08-253">Azure ML batch execution web services can be used toorun any workflows, for example R or Python scripts, that may not require any inputs.</span></span> <span data-ttu-id="caa08-254">Em alternativa, experimentação Olá pode ser configurada com um módulo de leitor não expõe qualquer GlobalParameters.</span><span class="sxs-lookup"><span data-stu-id="caa08-254">Or, hello experiment might be configured with a Reader module that does not expose any GlobalParameters.</span></span> <span data-ttu-id="caa08-255">Nesse caso, Olá AzureMLBatchExecution atividade seria configurado da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="caa08-255">In that case, hello AzureMLBatchExecution Activity would be configured as follows:</span></span>

```JSON
{
    "name": "scoring service",
    "type": "AzureMLBatchExecution",
    "outputs": [
        {
            "name": "myBlob"
        }
    ],
    "typeProperties": {
        "webServiceOutputs": {
            "output1": "myBlob"
        }              
     },
    "linkedServiceName": "mlEndpoint",
    "policy": {
        "concurrency": 1,
        "executionPriorityOrder": "NewestFirst",
        "retry": 1,
        "timeout": "02:00:00"
    }
},
```

#### <a name="web-service-does-not-require-an-inputoutput"></a><span data-ttu-id="caa08-256">Serviço Web não necessita de uma entrada/saída</span><span class="sxs-lookup"><span data-stu-id="caa08-256">Web Service does not require an input/output</span></span>
<span data-ttu-id="caa08-257">Olá serviço de web de execução de lote do Azure ML poderá não ter qualquer saída de serviço Web configurada.</span><span class="sxs-lookup"><span data-stu-id="caa08-257">hello Azure ML batch execution web service might not have any Web Service output configured.</span></span> <span data-ttu-id="caa08-258">Neste exemplo, não há nenhum serviço Web de entrada ou saída nem qualquer GlobalParameters configurados.</span><span class="sxs-lookup"><span data-stu-id="caa08-258">In this example, there is no Web Service input or output, nor are any GlobalParameters configured.</span></span> <span data-ttu-id="caa08-259">Ainda há uma saída configurada na atividade de Olá próprio, mas não está a ser fornecido como um webServiceOutput.</span><span class="sxs-lookup"><span data-stu-id="caa08-259">There is still an output configured on hello activity itself, but it is not given as a webServiceOutput.</span></span>

```JSON
{
    "name": "retraining",
    "type": "AzureMLBatchExecution",
    "outputs": [
        {
            "name": "placeholderOutputDataset"
        }
    ],
    "typeProperties": {
     },
    "linkedServiceName": "mlEndpoint",
    "policy": {
        "concurrency": 1,
        "executionPriorityOrder": "NewestFirst",
        "retry": 1,
        "timeout": "02:00:00"
    }
},
```

#### <a name="web-service-uses-readers-and-writers-and-hello-activity-runs-only-when-other-activities-have-succeeded"></a><span data-ttu-id="caa08-260">Leitores de utilizações de serviço Web e escritores e execuções de atividade Olá apenas quando outras atividades êxito</span><span class="sxs-lookup"><span data-stu-id="caa08-260">Web Service uses readers and writers, and hello activity runs only when other activities have succeeded</span></span>
<span data-ttu-id="caa08-261">Olá do Azure ML web leitor e escritor módulos do serviço podem ser configurado toorun com ou sem quaisquer GlobalParameters.</span><span class="sxs-lookup"><span data-stu-id="caa08-261">hello Azure ML web service reader and writer modules might be configured toorun with or without any GlobalParameters.</span></span> <span data-ttu-id="caa08-262">No entanto, poderá pretender que chama o serviço tooembed num pipeline que utiliza o serviço do conjunto de dados dependências tooinvoke Olá apenas quando concluir algumas processamento a montante.</span><span class="sxs-lookup"><span data-stu-id="caa08-262">However, you may want tooembed service calls in a pipeline that uses dataset dependencies tooinvoke hello service only when some upstream processing has completed.</span></span> <span data-ttu-id="caa08-263">Também pode acionar qualquer outra ação após conclusão da execução de lote Olá através desta abordagem.</span><span class="sxs-lookup"><span data-stu-id="caa08-263">You can also trigger some other action after hello batch execution has completed using this approach.</span></span> <span data-ttu-id="caa08-264">Nesse caso, pode express dependências Olá com entradas de atividade e saídas, sem qualquer um deles de nomenclatura como serviço Web entradas ou saídas.</span><span class="sxs-lookup"><span data-stu-id="caa08-264">In that case, you can express hello dependencies using activity inputs and outputs, without naming any of them as Web Service inputs or outputs.</span></span>

```JSON
{
    "name": "retraining",
    "type": "AzureMLBatchExecution",
    "inputs": [
        {
            "name": "upstreamData1"
        },
        {
            "name": "upstreamData2"
        }
    ],
    "outputs": [
        {
            "name": "downstreamData"
        }
    ],
    "typeProperties": {
     },
    "linkedServiceName": "mlEndpoint",
    "policy": {
        "concurrency": 1,
        "executionPriorityOrder": "NewestFirst",
        "retry": 1,
        "timeout": "02:00:00"
    }
},
```

<span data-ttu-id="caa08-265">Olá **takeaways** são:</span><span class="sxs-lookup"><span data-stu-id="caa08-265">hello **takeaways** are:</span></span>

* <span data-ttu-id="caa08-266">Se o ponto final de experimentação utiliza um webServiceInput: Este é representada por um conjunto de dados de blob e está incluído no entradas de atividade Olá e a propriedade de webServiceInput Olá.</span><span class="sxs-lookup"><span data-stu-id="caa08-266">If your experiment endpoint uses a webServiceInput: it is represented by a blob dataset and is included in hello activity inputs and hello webServiceInput property.</span></span> <span data-ttu-id="caa08-267">Caso contrário, a propriedade de webServiceInput Olá for omitida.</span><span class="sxs-lookup"><span data-stu-id="caa08-267">Otherwise, hello webServiceInput property is omitted.</span></span>
* <span data-ttu-id="caa08-268">Se o ponto final de experimentação utiliza webServiceOutput(s): estes são representados por conjuntos de dados de blob e incluídas na saídas da atividade de Olá e na propriedade de webServiceOutputs Olá.</span><span class="sxs-lookup"><span data-stu-id="caa08-268">If your experiment endpoint uses webServiceOutput(s): they are represented by blob datasets and are included in hello activity outputs and in hello webServiceOutputs property.</span></span> <span data-ttu-id="caa08-269">Olá atividade produz e webServiceOutputs estão mapeados com nome Olá cada resultado na experimentação de Olá.</span><span class="sxs-lookup"><span data-stu-id="caa08-269">hello activity outputs and webServiceOutputs are mapped by hello name of each output in hello experiment.</span></span> <span data-ttu-id="caa08-270">Caso contrário, a propriedade de webServiceOutputs Olá for omitida.</span><span class="sxs-lookup"><span data-stu-id="caa08-270">Otherwise, hello webServiceOutputs property is omitted.</span></span>
* <span data-ttu-id="caa08-271">Se o ponto final de experimentação expõe globalParameter(s), são fornecidos na propriedade de globalParameters Olá atividade como chave, pares de valor.</span><span class="sxs-lookup"><span data-stu-id="caa08-271">If your experiment endpoint exposes globalParameter(s), they are given in hello activity globalParameters property as key, value pairs.</span></span> <span data-ttu-id="caa08-272">Caso contrário, a propriedade de globalParameters Olá for omitida.</span><span class="sxs-lookup"><span data-stu-id="caa08-272">Otherwise, hello globalParameters property is omitted.</span></span> <span data-ttu-id="caa08-273">as chaves de Olá são maiúsculas e minúsculas.</span><span class="sxs-lookup"><span data-stu-id="caa08-273">hello keys are case-sensitive.</span></span> <span data-ttu-id="caa08-274">[Funções do Azure Data Factory](data-factory-functions-variables.md) podem ser utilizadas em valores de Olá.</span><span class="sxs-lookup"><span data-stu-id="caa08-274">[Azure Data Factory functions](data-factory-functions-variables.md) may be used in hello values.</span></span>
* <span data-ttu-id="caa08-275">Conjuntos de dados adicionais podem ser incluídos Olá entradas e saídas propriedades da atividade, sem a ser referenciado em Olá typeProperties de atividade.</span><span class="sxs-lookup"><span data-stu-id="caa08-275">Additional datasets may be included in hello Activity inputs and outputs properties, without being referenced in hello Activity typeProperties.</span></span> <span data-ttu-id="caa08-276">Estes conjuntos de dados governem execução utilizando dependências de setor mas caso contrário, são ignorados pelos Olá AzureMLBatchExecution atividade.</span><span class="sxs-lookup"><span data-stu-id="caa08-276">These datasets govern execution using slice dependencies but are otherwise ignored by hello AzureMLBatchExecution Activity.</span></span>


## <a name="updating-models-using-update-resource-activity"></a><span data-ttu-id="caa08-277">Atualizar Modelos de atividade do recurso da atualização</span><span class="sxs-lookup"><span data-stu-id="caa08-277">Updating models using Update Resource Activity</span></span>
<span data-ttu-id="caa08-278">Depois de terminar com reparametrização, atualizar Olá a classificação do serviço web (experimentação preditiva exposta como um serviço web) com o modelo treinado recentemente Olá utilizando Olá **da atividade de recursos de atualização do Azure ML**.</span><span class="sxs-lookup"><span data-stu-id="caa08-278">After you are done with retraining, update hello scoring web service (predictive experiment exposed as a web service) with hello newly trained model by using hello **Azure ML Update Resource Activity**.</span></span> <span data-ttu-id="caa08-279">Consulte [atualizar modelos de atividade do recurso da atualização](data-factory-azure-ml-update-resource-activity.md) artigo para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="caa08-279">See [Updating models using Update Resource Activity](data-factory-azure-ml-update-resource-activity.md) article for details.</span></span>

### <a name="reader-and-writer-modules"></a><span data-ttu-id="caa08-280">Leitor e escritor módulos</span><span class="sxs-lookup"><span data-stu-id="caa08-280">Reader and Writer Modules</span></span>
<span data-ttu-id="caa08-281">Um cenário comum para utilizar os parâmetros do serviço Web é a utilização de Olá de leitores de SQL do Azure e escritores.</span><span class="sxs-lookup"><span data-stu-id="caa08-281">A common scenario for using Web service parameters is hello use of Azure SQL Readers and Writers.</span></span> <span data-ttu-id="caa08-282">módulo leitor de Olá é utilizado tooload dados para uma experimentação de serviços de gestão de dados fora do Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="caa08-282">hello reader module is used tooload data into an experiment from data management services outside Azure Machine Learning Studio.</span></span> <span data-ttu-id="caa08-283">módulo de escritor Olá é toosave dados a partir das suas experimentações para os serviços de gestão de dados fora do Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="caa08-283">hello writer module is toosave data from your experiments into data management services outside Azure Machine Learning Studio.</span></span>  

<span data-ttu-id="caa08-284">Para obter detalhes sobre o Azure Blob/Azure SQL. o leitor/escritor, consulte [leitor](https://msdn.microsoft.com/library/azure/dn905997.aspx) e [escritor](https://msdn.microsoft.com/library/azure/dn905984.aspx) tópicos da biblioteca MSDN.</span><span class="sxs-lookup"><span data-stu-id="caa08-284">For details about Azure Blob/Azure SQL reader/writer, see [Reader](https://msdn.microsoft.com/library/azure/dn905997.aspx) and [Writer](https://msdn.microsoft.com/library/azure/dn905984.aspx) topics on MSDN Library.</span></span> <span data-ttu-id="caa08-285">exemplo de Olá na secção anterior Olá utilizado leitor de Blob do Azure de Olá e escritor de Blob do Azure.</span><span class="sxs-lookup"><span data-stu-id="caa08-285">hello example in hello previous section used hello Azure Blob reader and Azure Blob writer.</span></span> <span data-ttu-id="caa08-286">Esta secção explica como utilizar o leitor de SQL do Azure e o escritor SQL do Azure.</span><span class="sxs-lookup"><span data-stu-id="caa08-286">This section discusses using Azure SQL reader and Azure SQL writer.</span></span>

## <a name="frequently-asked-questions"></a><span data-ttu-id="caa08-287">Perguntas mais frequentes</span><span class="sxs-lookup"><span data-stu-id="caa08-287">Frequently asked questions</span></span>
<span data-ttu-id="caa08-288">**P:** tiver vários ficheiros que foram gerados por meu pipelines de macrodados.</span><span class="sxs-lookup"><span data-stu-id="caa08-288">**Q:** I have multiple files that are generated by my big data pipelines.</span></span> <span data-ttu-id="caa08-289">Pode utilizar Olá AzureMLBatchExecution atividade toowork em todos os ficheiros de Olá?</span><span class="sxs-lookup"><span data-stu-id="caa08-289">Can I use hello AzureMLBatchExecution Activity toowork on all hello files?</span></span>

<span data-ttu-id="caa08-290">**R:** Sim.</span><span class="sxs-lookup"><span data-stu-id="caa08-290">**A:** Yes.</span></span> <span data-ttu-id="caa08-291">Consulte Olá **utilizando uma data de tooread do módulo leitor de vários ficheiros no Blob do Azure** secção para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="caa08-291">See hello **Using a Reader module tooread data from multiple files in Azure Blob** section for details.</span></span>

## <a name="azure-ml-batch-scoring-activity"></a><span data-ttu-id="caa08-292">Atividade de classificação de lote do Azure ML</span><span class="sxs-lookup"><span data-stu-id="caa08-292">Azure ML Batch Scoring Activity</span></span>
<span data-ttu-id="caa08-293">Se estiver a utilizar Olá **AzureMLBatchScoring** toointegrate de atividade com o Azure Machine Learning, recomendamos que utilize Olá mais recente **AzureMLBatchExecution** atividade.</span><span class="sxs-lookup"><span data-stu-id="caa08-293">If you are using hello **AzureMLBatchScoring** activity toointegrate with Azure Machine Learning, we recommend that you use hello latest **AzureMLBatchExecution** activity.</span></span>

<span data-ttu-id="caa08-294">Olá AzureMLBatchExecution atividade é introduzida no Olá versão de Agosto de 2015 do SDK do Azure e o Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="caa08-294">hello AzureMLBatchExecution activity is introduced in hello August 2015 release of Azure SDK and Azure PowerShell.</span></span>

<span data-ttu-id="caa08-295">Se quiser toocontinue utilizando Olá AzureMLBatchScoring atividade, continue a ler através desta secção.</span><span class="sxs-lookup"><span data-stu-id="caa08-295">If you want toocontinue using hello AzureMLBatchScoring activity, continue reading through this section.</span></span>  

### <a name="azure-ml-batch-scoring-activity-using-azure-storage-for-inputoutput"></a><span data-ttu-id="caa08-296">Classificação de lote ML atividade do Azure utilizando o armazenamento do Azure para a entrada/saída</span><span class="sxs-lookup"><span data-stu-id="caa08-296">Azure ML Batch Scoring activity using Azure Storage for input/output</span></span>

```JSON
{
  "name": "PredictivePipeline",
  "properties": {
    "description": "use AzureML model",
    "activities": [
      {
        "name": "MLActivity",
        "type": "AzureMLBatchScoring",
        "description": "prediction analysis on batch input",
        "inputs": [
          {
            "name": "ScoringInputBlob"
          }
        ],
        "outputs": [
          {
            "name": "ScoringResultBlob"
          }
        ],
        "linkedServiceName": "MyAzureMLLinkedService",
        "policy": {
          "concurrency": 3,
          "executionPriorityOrder": "NewestFirst",
          "retry": 1,
          "timeout": "02:00:00"
        }
      }
    ],
    "start": "2016-02-13T00:00:00Z",
    "end": "2016-02-14T00:00:00Z"
  }
}
```

### <a name="web-service-parameters"></a><span data-ttu-id="caa08-297">Parâmetros do serviço Web</span><span class="sxs-lookup"><span data-stu-id="caa08-297">Web Service Parameters</span></span>
<span data-ttu-id="caa08-298">toospecify valores para parâmetros de serviço Web, adicione um **typeProperties** secção toohello **AzureMLBatchScoringActivty** secção Olá JSON do pipeline conforme mostrado no seguinte exemplo de Olá:</span><span class="sxs-lookup"><span data-stu-id="caa08-298">toospecify values for Web service parameters, add a **typeProperties** section toohello **AzureMLBatchScoringActivty** section in hello pipeline JSON as shown in hello following example:</span></span>

```JSON
"typeProperties": {
    "webServiceParameters": {
        "Param 1": "Value 1",
        "Param 2": "Value 2"
    }
}
```
<span data-ttu-id="caa08-299">Também pode utilizar [funções da fábrica de dados](data-factory-functions-variables.md) em transmitir parâmetros de serviço Web, conforme mostrado no seguinte exemplo de Olá de valores para Olá:</span><span class="sxs-lookup"><span data-stu-id="caa08-299">You can also use [Data Factory Functions](data-factory-functions-variables.md) in passing values for hello Web service parameters as shown in hello following example:</span></span>

```JSON
"typeProperties": {
    "webServiceParameters": {
       "Database query": "$$Text.Format('SELECT * FROM myTable WHERE timeColumn = \\'{0:yyyy-MM-dd HH:mm:ss}\\'', Time.AddHours(WindowStart, 0))"
    }
}
```

> [!NOTE]
> <span data-ttu-id="caa08-300">parâmetros de serviço Web de Olá são maiúsculas e minúsculas, por isso, certifique-se de que os nomes de Olá que especificar na atividade de Olá JSON corresponde Olá aqueles exposta pelo Olá serviço Web.</span><span class="sxs-lookup"><span data-stu-id="caa08-300">hello Web service parameters are case-sensitive, so ensure that hello names you specify in hello activity JSON match hello ones exposed by hello Web service.</span></span>
>
>

## <a name="see-also"></a><span data-ttu-id="caa08-301">Veja Também</span><span class="sxs-lookup"><span data-stu-id="caa08-301">See Also</span></span>
* [<span data-ttu-id="caa08-302">Mensagem de blogue do Azure: introdução ao Azure Data Factory e o Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="caa08-302">Azure blog post: Getting started with Azure Data Factory and Azure Machine Learning</span></span>](https://azure.microsoft.com/blog/getting-started-with-azure-data-factory-and-azure-machine-learning-4/)

[adf-build-1st-pipeline]: data-factory-build-your-first-pipeline.md

[azure-machine-learning]: http://azure.microsoft.com/services/machine-learning/
