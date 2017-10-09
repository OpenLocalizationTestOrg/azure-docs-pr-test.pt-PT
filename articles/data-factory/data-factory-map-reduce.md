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
# <a name="invoke-mapreduce-programs-from-data-factory"></a>Invocar MapReduce programas da fábrica de dados
> [!div class="op_single_selector" title1="Transformation Activities"]
> * [Atividade do ramo de registo](data-factory-hive-activity.md) 
> * [Atividade do PIg](data-factory-pig-activity.md)
> * [Atividade de MapReduce](data-factory-map-reduce.md)
> * [Atividade de transmissão em fluxo do Hadoop](data-factory-hadoop-streaming-activity.md)
> * [Atividade do Spark](data-factory-spark.md)
> * [Atividade de Execução em Lote do Machine Learning](data-factory-azure-ml-batch-execution-activity.md)
> * [Atividade de Recursos de Atualização de Machine Learning](data-factory-azure-ml-update-resource-activity.md)
> * [Atividade de Procedimento Armazenado](data-factory-stored-proc-activity.md)
> * [Atividade de U-SQL do Data Lake Analytics](data-factory-usql-activity.md)
> * [Atividade personalizada do .NET](data-factory-use-custom-activities.md)

Olá atividade de HDInsight MapReduce numa fábrica de dados [pipeline](data-factory-create-pipelines.md) executa programas de MapReduce num [os seus próprios](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) ou [a pedido](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) cluster do HDInsight baseado em Windows/Linux. Este artigo baseia-se Olá [atividades de transformação de dados](data-factory-data-transformation-activities.md) artigo, que apresenta uma descrição geral de transformação de dados e atividades de transformação de Olá suportado.

> [!NOTE] 
> Se forem tooAzure nova fábrica de dados, leia [introdução tooAzure Data Factory](data-factory-introduction.md) e Olá tutorial: [construir o seu primeiro pipeline de dados](data-factory-build-your-first-pipeline.md) antes de ler este artigo.  

## <a name="introduction"></a>Introdução
Um pipeline de um Azure data factory processa dados nos serviços do storage ligadas utilizando os serviços ligados de computação. Contém uma sequência de atividades em que cada atividade executa uma operação de processamento específico. Este artigo descreve utilizando Olá atividade de MapReduce do HDInsight.

Consulte [Pig](data-factory-pig-activity.md) e [Hive](data-factory-hive-activity.md) para obter detalhes sobre como executar Pig/Hive scripts num HDInsight baseado em Windows/Linux cluster de um pipeline, utilizando as atividades de HDInsight Pig e do Hive. 

## <a name="json-for-hdinsight-mapreduce-activity"></a>JSON de atividade de HDInsight MapReduce
No Olá definição JSON para Olá atividade do HDInsight: 

1. Conjunto Olá **tipo** de Olá **atividade** demasiado**HDInsight**.
2. Especifique o nome de Olá classe Olá para **className** propriedade.
3. Especifique o ficheiro JAR Olá caminho toohello, incluindo o nome de ficheiro Olá para **jarFilePath** propriedade.
4. Especifique o serviço de Olá ligado que referencia toohello armazenamento de Blobs do Azure que contém o ficheiro JAR Olá **jarLinkedService** propriedade.   
5. Especifique os argumentos para o programa de MapReduce Olá no Olá **argumentos** secção. Em runtime, pode ver alguns argumentos adicionais (por exemplo: mapreduce.job.tags) da arquitetura do MapReduce Olá. toodifferentiate os argumentos com argumentos de MapReduce Olá, considere a utilização da opção e o valor como argumentos conforme mostrado no seguinte exemplo de Olá (- s, - entrada, - saída etc., são opções seguidas imediatamente pelos respetivos valores).

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
Pode utilizar Olá atividade de MapReduce HDInsight toorun qualquer ficheiro jar do MapReduce num cluster do HDInsight. Olá seguinte definição JSON de exemplo de um pipeline, Olá atividade do HDInsight é configurado toorun um ficheiro Mahout JAR.

## <a name="sample-on-github"></a>Exemplo no GitHub
Pode transferir um exemplo de utilização Olá atividade de MapReduce HDInsight do: [amostras do Data Factory no GitHub](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/JSON/MapReduce_Activity_Sample).  

## <a name="running-hello-word-count-program"></a>Executar programa de contagem de Word Olá
pipeline de Olá neste exemplo é executado Olá mapa/reduza a contagem de Word programa no seu cluster Azure HDInsight.   

### <a name="linked-services"></a>Serviços ligados
Em primeiro lugar, crie um Olá toolink de serviço ligado do armazenamento do Azure que é utilizado pela fábrica de dados do Azure do Olá Azure HDInsight cluster toohello. Se a copiar/colar Olá código a seguir, não se esqueça tooreplace **nome da conta** e **chave da conta** com nome Olá e a chave do seu armazenamento do Azure. 

#### <a name="azure-storage-linked-service"></a>Serviço ligado do Storage do Azure

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

#### <a name="azure-hdinsight-linked-service"></a>Serviço ligado de HDInsight do Azure
Em seguida, crie um serviço ligado toolink a fábrica de dados do Azure do Azure HDInsight cluster toohello. Se a copiar/colar Olá código a seguir, substitua **nome do cluster de HDInsight** com o nome de Olá do cluster do HDInsight e alteração de valores de nome e palavra-passe de utilizador.   

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

### <a name="datasets"></a>Conjuntos de dados
#### <a name="output-dataset"></a>Conjunto de dados de saída
pipeline de Olá neste exemplo não tem quaisquer entradas. Especifique um conjunto de dados de saída para Olá atividade de MapReduce do HDInsight. Este conjunto de dados é apenas um dataset fictício que é necessário toodrive Olá pipeline agenda.  

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

### <a name="pipeline"></a>Pipeline
pipeline de Olá neste exemplo tem apenas uma atividade que é do tipo: HDInsightMapReduce. Algumas das propriedades importantes Olá Olá JSON são: 

| Propriedade | Notas |
|:--- |:--- |
| tipo |tipo de Olá tem de ser definido demasiado**HDInsightMapReduce**. |
| className |Nome da classe de Olá é: **wordcount** |
| jarFilePath |Caminho toohello jar o ficheiro que contém a classe de Olá. Se a copiar/colar Olá código a seguir, não se esqueça de nome de Olá toochange do cluster de Olá. |
| jarLinkedService |Serviço ligado do Storage do Azure que contém o ficheiro jar de Olá. Este serviço ligado refere-se toohello armazenamento que está associado ao cluster do HDInsight Olá. |
| Argumentos |programa de wordcount Olá aceita dois argumentos, uma entrada e um resultado. ficheiro de entrada Olá é davinci.txt de Olá ficheiros. |
| frequência/intervalo |Olá os valores para estas propriedades de corresponder ao conjunto de dados de saída de Olá. |
| linkedServiceName |refere-se o serviço ligado de HDInsight de toohello criou anteriormente. |

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

## <a name="run-spark-programs"></a>Executar programas do Spark
Pode utilizar programas de Spark do MapReduce atividade toorun no seu cluster do HDInsight Spark. Veja [Invoke Spark programs from Azure Data Factory (Invocar programas do Spark a partir do Azure Data Factory)](data-factory-spark.md) para obter detalhes  

[developer-reference]: http://go.microsoft.com/fwlink/?LinkId=516908
[cmdlet-reference]: http://go.microsoft.com/fwlink/?LinkId=517456


[adfgetstarted]: data-factory-copy-data-from-azure-blob-storage-to-sql-database.md
[adfgetstartedmonitoring]:data-factory-copy-data-from-azure-blob-storage-to-sql-database.md#monitor-pipelines 

[Developer Reference]: http://go.microsoft.com/fwlink/?LinkId=516908
[Azure Portal]: http://portal.azure.com

## <a name="see-also"></a>Veja Também
* [Atividade do ramo de registo](data-factory-hive-activity.md)
* [Atividade do PIg](data-factory-pig-activity.md)
* [Atividade de transmissão em fluxo do Hadoop](data-factory-hadoop-streaming-activity.md)
* [Invocar programas do Spark](data-factory-spark.md)
* [Invocar scripts R](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample)

