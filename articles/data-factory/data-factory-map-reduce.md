---
title: aaaInvoke MapReduce programa de Azure Data Factory
description: "Saiba como tooprocess dados através da execução de programas de MapReduce num Azure HDInsight cluster a partir de um Azure data factory."
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: c34db93f-570a-44f1-a7d6-00390f4dc0fa
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: shlo
ms.openlocfilehash: 448ef93a10bd97e7ecd4be4f04f88f8a05decc1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="invoke-mapreduce-programs-from-data-factory"></a><span data-ttu-id="b12eb-103">Invocar MapReduce programas da fábrica de dados</span><span class="sxs-lookup"><span data-stu-id="b12eb-103">Invoke MapReduce Programs from Data Factory</span></span>
> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="b12eb-104">Atividade do ramo de registo</span><span class="sxs-lookup"><span data-stu-id="b12eb-104">Hive Activity</span></span>](data-factory-hive-activity.md) 
> * [<span data-ttu-id="b12eb-105">Atividade do PIg</span><span class="sxs-lookup"><span data-stu-id="b12eb-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="b12eb-106">Atividade de MapReduce</span><span class="sxs-lookup"><span data-stu-id="b12eb-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="b12eb-107">Atividade de transmissão em fluxo do Hadoop</span><span class="sxs-lookup"><span data-stu-id="b12eb-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="b12eb-108">Atividade do Spark</span><span class="sxs-lookup"><span data-stu-id="b12eb-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="b12eb-109">Atividade de Execução em Lote do Machine Learning</span><span class="sxs-lookup"><span data-stu-id="b12eb-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="b12eb-110">Atividade de Recursos de Atualização de Machine Learning</span><span class="sxs-lookup"><span data-stu-id="b12eb-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="b12eb-111">Atividade de Procedimento Armazenado</span><span class="sxs-lookup"><span data-stu-id="b12eb-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="b12eb-112">Atividade de U-SQL do Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="b12eb-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="b12eb-113">Atividade personalizada do .NET</span><span class="sxs-lookup"><span data-stu-id="b12eb-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

<span data-ttu-id="b12eb-114">Olá atividade de HDInsight MapReduce numa fábrica de dados [pipeline](data-factory-create-pipelines.md) executa programas de MapReduce num [os seus próprios](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) ou [a pedido](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) cluster do HDInsight baseado em Windows/Linux.</span><span class="sxs-lookup"><span data-stu-id="b12eb-114">hello HDInsight MapReduce activity in a Data Factory [pipeline](data-factory-create-pipelines.md) executes MapReduce programs on [your own](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) or [on-demand](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) Windows/Linux-based HDInsight cluster.</span></span> <span data-ttu-id="b12eb-115">Este artigo baseia-se Olá [atividades de transformação de dados](data-factory-data-transformation-activities.md) artigo, que apresenta uma descrição geral de transformação de dados e atividades de transformação de Olá suportado.</span><span class="sxs-lookup"><span data-stu-id="b12eb-115">This article builds on hello [data transformation activities](data-factory-data-transformation-activities.md) article, which presents a general overview of data transformation and hello supported transformation activities.</span></span>

> [!NOTE] 
> <span data-ttu-id="b12eb-116">Se forem tooAzure nova fábrica de dados, leia [introdução tooAzure Data Factory](data-factory-introduction.md) e Olá tutorial: [construir o seu primeiro pipeline de dados](data-factory-build-your-first-pipeline.md) antes de ler este artigo.</span><span class="sxs-lookup"><span data-stu-id="b12eb-116">If you are new tooAzure Data Factory, read through [Introduction tooAzure Data Factory](data-factory-introduction.md) and do hello tutorial: [Build your first data pipeline](data-factory-build-your-first-pipeline.md) before reading this article.</span></span>  

## <a name="introduction"></a><span data-ttu-id="b12eb-117">Introdução</span><span class="sxs-lookup"><span data-stu-id="b12eb-117">Introduction</span></span>
<span data-ttu-id="b12eb-118">Um pipeline de um Azure data factory processa dados nos serviços do storage ligadas utilizando os serviços ligados de computação.</span><span class="sxs-lookup"><span data-stu-id="b12eb-118">A pipeline in an Azure data factory processes data in linked storage services by using linked compute services.</span></span> <span data-ttu-id="b12eb-119">Contém uma sequência de atividades em que cada atividade executa uma operação de processamento específico.</span><span class="sxs-lookup"><span data-stu-id="b12eb-119">It contains a sequence of activities where each activity performs a specific processing operation.</span></span> <span data-ttu-id="b12eb-120">Este artigo descreve utilizando Olá atividade de MapReduce do HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b12eb-120">This article describes using hello HDInsight MapReduce Activity.</span></span>

<span data-ttu-id="b12eb-121">Consulte [Pig](data-factory-pig-activity.md) e [Hive](data-factory-hive-activity.md) para obter detalhes sobre como executar Pig/Hive scripts num HDInsight baseado em Windows/Linux cluster de um pipeline, utilizando as atividades de HDInsight Pig e do Hive.</span><span class="sxs-lookup"><span data-stu-id="b12eb-121">See [Pig](data-factory-pig-activity.md) and [Hive](data-factory-hive-activity.md) for details about running Pig/Hive scripts on a Windows/Linux-based HDInsight cluster from a pipeline by using HDInsight Pig and Hive activities.</span></span> 

## <a name="json-for-hdinsight-mapreduce-activity"></a><span data-ttu-id="b12eb-122">JSON de atividade de HDInsight MapReduce</span><span class="sxs-lookup"><span data-stu-id="b12eb-122">JSON for HDInsight MapReduce Activity</span></span>
<span data-ttu-id="b12eb-123">No Olá definição JSON para Olá atividade do HDInsight:</span><span class="sxs-lookup"><span data-stu-id="b12eb-123">In hello JSON definition for hello HDInsight Activity:</span></span> 

1. <span data-ttu-id="b12eb-124">Conjunto Olá **tipo** de Olá **atividade** demasiado**HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="b12eb-124">Set hello **type** of hello **activity** too**HDInsight**.</span></span>
2. <span data-ttu-id="b12eb-125">Especifique o nome de Olá classe Olá para **className** propriedade.</span><span class="sxs-lookup"><span data-stu-id="b12eb-125">Specify hello name of hello class for **className** property.</span></span>
3. <span data-ttu-id="b12eb-126">Especifique o ficheiro JAR Olá caminho toohello, incluindo o nome de ficheiro Olá para **jarFilePath** propriedade.</span><span class="sxs-lookup"><span data-stu-id="b12eb-126">Specify hello path toohello JAR file including hello file name for **jarFilePath** property.</span></span>
4. <span data-ttu-id="b12eb-127">Especifique o serviço de Olá ligado que referencia toohello armazenamento de Blobs do Azure que contém o ficheiro JAR Olá **jarLinkedService** propriedade.</span><span class="sxs-lookup"><span data-stu-id="b12eb-127">Specify hello linked service that refers toohello Azure Blob Storage that contains hello JAR file for **jarLinkedService** property.</span></span>   
5. <span data-ttu-id="b12eb-128">Especifique os argumentos para o programa de MapReduce Olá no Olá **argumentos** secção.</span><span class="sxs-lookup"><span data-stu-id="b12eb-128">Specify any arguments for hello MapReduce program in hello **arguments** section.</span></span> <span data-ttu-id="b12eb-129">Em runtime, pode ver alguns argumentos adicionais (por exemplo: mapreduce.job.tags) da arquitetura do MapReduce Olá.</span><span class="sxs-lookup"><span data-stu-id="b12eb-129">At runtime, you see a few extra arguments (for example: mapreduce.job.tags) from hello MapReduce framework.</span></span> <span data-ttu-id="b12eb-130">toodifferentiate os argumentos com argumentos de MapReduce Olá, considere a utilização da opção e o valor como argumentos conforme mostrado no seguinte exemplo de Olá (- s, - entrada, - saída etc., são opções seguidas imediatamente pelos respetivos valores).</span><span class="sxs-lookup"><span data-stu-id="b12eb-130">toodifferentiate your arguments with hello MapReduce arguments, consider using both option and value as arguments as shown in hello following example (-s, --input, --output etc., are options immediately followed by their values).</span></span>

    ```JSON   
    {
        "name": "MahoutMapReduceSamplePipeline",
        "properties": {
            "description": "Sample Pipeline tooRun a Mahout Custom Map Reduce Jar. This job calcuates an Item Similarity Matrix toodetermine hello similarity between 2 items",
            "activities": [
                {
                    "type": "HDInsightMapReduce",
                    "typeProperties": {
                        "className": "org.apache.mahout.cf.taste.hadoop.similarity.item.ItemSimilarityJob",
                        "jarFilePath": "adfsamples/Mahout/jars/mahout-examples-0.9.0.2.2.7.1-34.jar",
                        "jarLinkedService": "StorageLinkedService",
                        "arguments": [
                            "-s",
                            "SIMILARITY_LOGLIKELIHOOD",
                            "--input",
                            "wasb://adfsamples@spestore.blob.core.windows.net/Mahout/input",
                            "--output",
                            "wasb://adfsamples@spestore.blob.core.windows.net/Mahout/output/",
                            "--maxSimilaritiesPerItem",
                            "500",
                            "--tempDir",
                            "wasb://adfsamples@spestore.blob.core.windows.net/Mahout/temp/mahout"
                        ]
                    },
                    "inputs": [
                        {
                            "name": "MahoutInput"
                        }
                    ],
                    "outputs": [
                        {
                            "name": "MahoutOutput"
                        }
                    ],
                    "policy": {
                        "timeout": "01:00:00",
                        "concurrency": 1,
                        "retry": 3
                    },
                    "scheduler": {
                        "frequency": "Hour",
                        "interval": 1
                    },
                    "name": "MahoutActivity",
                    "description": "Custom Map Reduce toogenerate Mahout result",
                    "linkedServiceName": "HDInsightLinkedService"
                }
            ],
            "start": "2017-01-03T00:00:00Z",
            "end": "2017-01-04T00:00:00Z"
        }
    }
    ```
<span data-ttu-id="b12eb-131">Pode utilizar Olá atividade de MapReduce HDInsight toorun qualquer ficheiro jar do MapReduce num cluster do HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b12eb-131">You can use hello HDInsight MapReduce Activity toorun any MapReduce jar file on an HDInsight cluster.</span></span> <span data-ttu-id="b12eb-132">Olá seguinte definição JSON de exemplo de um pipeline, Olá atividade do HDInsight é configurado toorun um ficheiro Mahout JAR.</span><span class="sxs-lookup"><span data-stu-id="b12eb-132">In hello following sample JSON definition of a pipeline, hello HDInsight Activity is configured toorun a Mahout JAR file.</span></span>

## <a name="sample-on-github"></a><span data-ttu-id="b12eb-133">Exemplo no GitHub</span><span class="sxs-lookup"><span data-stu-id="b12eb-133">Sample on GitHub</span></span>
<span data-ttu-id="b12eb-134">Pode transferir um exemplo de utilização Olá atividade de MapReduce HDInsight do: [amostras do Data Factory no GitHub](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/JSON/MapReduce_Activity_Sample).</span><span class="sxs-lookup"><span data-stu-id="b12eb-134">You can download a sample for using hello HDInsight MapReduce Activity from: [Data Factory Samples on GitHub](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/JSON/MapReduce_Activity_Sample).</span></span>  

## <a name="running-hello-word-count-program"></a><span data-ttu-id="b12eb-135">Executar programa de contagem de Word Olá</span><span class="sxs-lookup"><span data-stu-id="b12eb-135">Running hello Word Count program</span></span>
<span data-ttu-id="b12eb-136">pipeline de Olá neste exemplo é executado Olá mapa/reduza a contagem de Word programa no seu cluster Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b12eb-136">hello pipeline in this example runs hello Word Count Map/Reduce program on your Azure HDInsight cluster.</span></span>   

### <a name="linked-services"></a><span data-ttu-id="b12eb-137">Serviços ligados</span><span class="sxs-lookup"><span data-stu-id="b12eb-137">Linked Services</span></span>
<span data-ttu-id="b12eb-138">Em primeiro lugar, crie um Olá toolink de serviço ligado do armazenamento do Azure que é utilizado pela fábrica de dados do Azure do Olá Azure HDInsight cluster toohello.</span><span class="sxs-lookup"><span data-stu-id="b12eb-138">First, you create a linked service toolink hello Azure Storage that is used by hello Azure HDInsight cluster toohello Azure data factory.</span></span> <span data-ttu-id="b12eb-139">Se a copiar/colar Olá código a seguir, não se esqueça tooreplace **nome da conta** e **chave da conta** com nome Olá e a chave do seu armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="b12eb-139">If you copy/paste hello following code, do not forget tooreplace **account name** and **account key** with hello name and key of your Azure Storage.</span></span> 

#### <a name="azure-storage-linked-service"></a><span data-ttu-id="b12eb-140">Serviço ligado do Storage do Azure</span><span class="sxs-lookup"><span data-stu-id="b12eb-140">Azure Storage linked service</span></span>

```JSON
{
    "name": "StorageLinkedService",
    "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<account name>;AccountKey=<account key>"
        }
    }
}
```

#### <a name="azure-hdinsight-linked-service"></a><span data-ttu-id="b12eb-141">Serviço ligado de HDInsight do Azure</span><span class="sxs-lookup"><span data-stu-id="b12eb-141">Azure HDInsight linked service</span></span>
<span data-ttu-id="b12eb-142">Em seguida, crie um serviço ligado toolink a fábrica de dados do Azure do Azure HDInsight cluster toohello.</span><span class="sxs-lookup"><span data-stu-id="b12eb-142">Next, you create a linked service toolink your Azure HDInsight cluster toohello Azure data factory.</span></span> <span data-ttu-id="b12eb-143">Se a copiar/colar Olá código a seguir, substitua **nome do cluster de HDInsight** com o nome de Olá do cluster do HDInsight e alteração de valores de nome e palavra-passe de utilizador.</span><span class="sxs-lookup"><span data-stu-id="b12eb-143">If you copy/paste hello following code, replace **HDInsight cluster name** with hello name of your HDInsight cluster, and change user name and password values.</span></span>   

```JSON
{
    "name": "HDInsightLinkedService",
    "properties": {
        "type": "HDInsight",
        "typeProperties": {
            "clusterUri": "https://<HDInsight cluster name>.azurehdinsight.net",
            "userName": "admin",
            "password": "**********",
            "linkedServiceName": "StorageLinkedService"
        }
    }
}
```

### <a name="datasets"></a><span data-ttu-id="b12eb-144">Conjuntos de dados</span><span class="sxs-lookup"><span data-stu-id="b12eb-144">Datasets</span></span>
#### <a name="output-dataset"></a><span data-ttu-id="b12eb-145">Conjunto de dados de saída</span><span class="sxs-lookup"><span data-stu-id="b12eb-145">Output dataset</span></span>
<span data-ttu-id="b12eb-146">pipeline de Olá neste exemplo não tem quaisquer entradas.</span><span class="sxs-lookup"><span data-stu-id="b12eb-146">hello pipeline in this example does not take any inputs.</span></span> <span data-ttu-id="b12eb-147">Especifique um conjunto de dados de saída para Olá atividade de MapReduce do HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b12eb-147">You specify an output dataset for hello HDInsight MapReduce Activity.</span></span> <span data-ttu-id="b12eb-148">Este conjunto de dados é apenas um dataset fictício que é necessário toodrive Olá pipeline agenda.</span><span class="sxs-lookup"><span data-stu-id="b12eb-148">This dataset is just a dummy dataset that is required toodrive hello pipeline schedule.</span></span>  

```JSON
{
    "name": "MROutput",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "fileName": "WordCountOutput1.txt",
            "folderPath": "example/data/",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ","
            }
        },
        "availability": {
            "frequency": "Day",
            "interval": 1
        }
    }
}
```

### <a name="pipeline"></a><span data-ttu-id="b12eb-149">Pipeline</span><span class="sxs-lookup"><span data-stu-id="b12eb-149">Pipeline</span></span>
<span data-ttu-id="b12eb-150">pipeline de Olá neste exemplo tem apenas uma atividade que é do tipo: HDInsightMapReduce.</span><span class="sxs-lookup"><span data-stu-id="b12eb-150">hello pipeline in this example has only one activity that is of type: HDInsightMapReduce.</span></span> <span data-ttu-id="b12eb-151">Algumas das propriedades importantes Olá Olá JSON são:</span><span class="sxs-lookup"><span data-stu-id="b12eb-151">Some of hello important properties in hello JSON are:</span></span> 

| <span data-ttu-id="b12eb-152">Propriedade</span><span class="sxs-lookup"><span data-stu-id="b12eb-152">Property</span></span> | <span data-ttu-id="b12eb-153">Notas</span><span class="sxs-lookup"><span data-stu-id="b12eb-153">Notes</span></span> |
|:--- |:--- |
| <span data-ttu-id="b12eb-154">tipo</span><span class="sxs-lookup"><span data-stu-id="b12eb-154">type</span></span> |<span data-ttu-id="b12eb-155">tipo de Olá tem de ser definido demasiado**HDInsightMapReduce**.</span><span class="sxs-lookup"><span data-stu-id="b12eb-155">hello type must be set too**HDInsightMapReduce**.</span></span> |
| <span data-ttu-id="b12eb-156">className</span><span class="sxs-lookup"><span data-stu-id="b12eb-156">className</span></span> |<span data-ttu-id="b12eb-157">Nome da classe de Olá é: **wordcount**</span><span class="sxs-lookup"><span data-stu-id="b12eb-157">Name of hello class is: **wordcount**</span></span> |
| <span data-ttu-id="b12eb-158">jarFilePath</span><span class="sxs-lookup"><span data-stu-id="b12eb-158">jarFilePath</span></span> |<span data-ttu-id="b12eb-159">Caminho toohello jar o ficheiro que contém a classe de Olá.</span><span class="sxs-lookup"><span data-stu-id="b12eb-159">Path toohello jar file containing hello class.</span></span> <span data-ttu-id="b12eb-160">Se a copiar/colar Olá código a seguir, não se esqueça de nome de Olá toochange do cluster de Olá.</span><span class="sxs-lookup"><span data-stu-id="b12eb-160">If you copy/paste hello following code, don't forget toochange hello name of hello cluster.</span></span> |
| <span data-ttu-id="b12eb-161">jarLinkedService</span><span class="sxs-lookup"><span data-stu-id="b12eb-161">jarLinkedService</span></span> |<span data-ttu-id="b12eb-162">Serviço ligado do Storage do Azure que contém o ficheiro jar de Olá.</span><span class="sxs-lookup"><span data-stu-id="b12eb-162">Azure Storage linked service that contains hello jar file.</span></span> <span data-ttu-id="b12eb-163">Este serviço ligado refere-se toohello armazenamento que está associado ao cluster do HDInsight Olá.</span><span class="sxs-lookup"><span data-stu-id="b12eb-163">This linked service refers toohello storage that is associated with hello HDInsight cluster.</span></span> |
| <span data-ttu-id="b12eb-164">Argumentos</span><span class="sxs-lookup"><span data-stu-id="b12eb-164">arguments</span></span> |<span data-ttu-id="b12eb-165">programa de wordcount Olá aceita dois argumentos, uma entrada e um resultado.</span><span class="sxs-lookup"><span data-stu-id="b12eb-165">hello wordcount program takes two arguments, an input and an output.</span></span> <span data-ttu-id="b12eb-166">ficheiro de entrada Olá é davinci.txt de Olá ficheiros.</span><span class="sxs-lookup"><span data-stu-id="b12eb-166">hello input file is hello davinci.txt file.</span></span> |
| <span data-ttu-id="b12eb-167">frequência/intervalo</span><span class="sxs-lookup"><span data-stu-id="b12eb-167">frequency/interval</span></span> |<span data-ttu-id="b12eb-168">Olá os valores para estas propriedades de corresponder ao conjunto de dados de saída de Olá.</span><span class="sxs-lookup"><span data-stu-id="b12eb-168">hello values for these properties match hello output dataset.</span></span> |
| <span data-ttu-id="b12eb-169">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="b12eb-169">linkedServiceName</span></span> |<span data-ttu-id="b12eb-170">refere-se o serviço ligado de HDInsight de toohello criou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="b12eb-170">refers toohello HDInsight linked service you had created earlier.</span></span> |

```JSON
{
    "name": "MRSamplePipeline",
    "properties": {
        "description": "Sample Pipeline tooRun hello Word Count Program",
        "activities": [
            {
                "type": "HDInsightMapReduce",
                "typeProperties": {
                    "className": "wordcount",
                    "jarFilePath": "<HDInsight cluster name>/example/jars/hadoop-examples.jar",
                    "jarLinkedService": "StorageLinkedService",
                    "arguments": [
                        "/example/data/gutenberg/davinci.txt",
                        "/example/data/WordCountOutput1"
                    ]
                },
                "outputs": [
                    {
                        "name": "MROutput"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1,
                    "retry": 3
                },
                "scheduler": {
                    "frequency": "Day",
                    "interval": 1
                },
                "name": "MRActivity",
                "linkedServiceName": "HDInsightLinkedService"
            }
        ],
        "start": "2014-01-03T00:00:00Z",
        "end": "2014-01-04T00:00:00Z"
    }
}
```

## <a name="run-spark-programs"></a><span data-ttu-id="b12eb-171">Executar programas do Spark</span><span class="sxs-lookup"><span data-stu-id="b12eb-171">Run Spark programs</span></span>
<span data-ttu-id="b12eb-172">Pode utilizar programas de Spark do MapReduce atividade toorun no seu cluster do HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="b12eb-172">You can use MapReduce activity toorun Spark programs on your HDInsight Spark cluster.</span></span> <span data-ttu-id="b12eb-173">Veja [Invoke Spark programs from Azure Data Factory (Invocar programas do Spark a partir do Azure Data Factory)](data-factory-spark.md) para obter detalhes</span><span class="sxs-lookup"><span data-stu-id="b12eb-173">See [Invoke Spark programs from Azure Data Factory](data-factory-spark.md) for details.</span></span>  

[developer-reference]: http://go.microsoft.com/fwlink/?LinkId=516908
[cmdlet-reference]: http://go.microsoft.com/fwlink/?LinkId=517456


[adfgetstarted]: data-factory-copy-data-from-azure-blob-storage-to-sql-database.md
[adfgetstartedmonitoring]:data-factory-copy-data-from-azure-blob-storage-to-sql-database.md#monitor-pipelines 

[Developer Reference]: http://go.microsoft.com/fwlink/?LinkId=516908
[Azure Portal]: http://portal.azure.com

## <a name="see-also"></a><span data-ttu-id="b12eb-174">Veja Também</span><span class="sxs-lookup"><span data-stu-id="b12eb-174">See Also</span></span>
* [<span data-ttu-id="b12eb-175">Atividade do ramo de registo</span><span class="sxs-lookup"><span data-stu-id="b12eb-175">Hive Activity</span></span>](data-factory-hive-activity.md)
* [<span data-ttu-id="b12eb-176">Atividade do PIg</span><span class="sxs-lookup"><span data-stu-id="b12eb-176">Pig Activity</span></span>](data-factory-pig-activity.md)
* [<span data-ttu-id="b12eb-177">Atividade de transmissão em fluxo do Hadoop</span><span class="sxs-lookup"><span data-stu-id="b12eb-177">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
* [<span data-ttu-id="b12eb-178">Invocar programas do Spark</span><span class="sxs-lookup"><span data-stu-id="b12eb-178">Invoke Spark programs</span></span>](data-factory-spark.md)
* [<span data-ttu-id="b12eb-179">Invocar scripts R</span><span class="sxs-lookup"><span data-stu-id="b12eb-179">Invoke R scripts</span></span>](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample)

