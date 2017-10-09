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
# <a name="create-predictive-pipelines-using-azure-machine-learning-and-azure-data-factory"></a>Criar pipelines preditivos com o Azure Machine Learning e o Azure Data Factory

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

## <a name="introduction"></a>Introdução

### <a name="azure-machine-learning"></a>Azure Machine Learning
[O Azure Machine Learning](https://azure.microsoft.com/documentation/services/machine-learning/) permite toobuild, testar e implementar soluções de Análise Preditiva. Do ponto de vista alto nível, é efetuada em três passos:

1. **Criar uma experimentação de preparação**. Execute este passo utilizando Olá Azure ML Studio. studio de ML Olá é um ambiente de desenvolvimento de visual de colaboração que utilize tootrain e testar um modelo de Análise Preditiva utilizando dados de preparação.
2. **Converta-experimentação preditiva tooa**. Depois do seu modelo tem sido preparado com a dados existentes e estiver pronto toouse-tooscore novos dados, preparar e simplificar a sua experimentação para classificação.
3. **Implementá-lo como um serviço web**. Pode publicar a sua experimentação de classificação como um serviço web do Azure. Pode enviar o modelo de tooyour dados através deste ponto de final de serviço web e receber predições resultado fro modelo Olá.  

### <a name="azure-data-factory"></a>Azure Data Factory
Fábrica de dados é um serviço de integração de dados baseado na nuvem que orquestra e automatiza Olá **movimento** e **transformação** de dados. Pode criar soluções de integração de dados utilizando o Azure Data Factory que podem ingerir dados a partir de vários arquivos de dados, dados Olá/processo transformar e publicar Olá resultado dados toohello os arquivos de dados.

Serviço fábrica de dados permite-lhe toocreate pipelines de dados que moverem e transforme dados e, em seguida, execute pipelines Olá numa agenda especificada (hora a hora, diariamente, semanalmente, etc.). Também fornece linhagem de Olá visualizações otimizadas toodisplay e as dependências entre os seus pipelines de dados e monitorizar todos os seus pipelines de dados de um problemas de identificar tooeasily vista unificada única e alertas de monitorização de configuração.

Consulte [introdução tooAzure Data Factory](data-factory-introduction.md) e [construir o seu primeiro pipeline](data-factory-build-your-first-pipeline.md) artigos tooquickly introdução ao hello do serviço Azure Data Factory.

### <a name="data-factory-and-machine-learning-together"></a>Fábrica de dados e de Machine Learning em conjunto
Ativa a fábrica de dados do Azure tooeasily Criar pipelines que utilizam um publicados [Azure Machine Learning] [ azure-machine-learning] web service para Análise Preditiva. Utilizar Olá **atividade de execução de lote** um pipeline do Azure Data Factory, pode invocar um predições do toomake de serviço web do Azure ML em dados de Olá no batch. Consulte [invocar do Azure ML web service utilizar Olá atividade de execução de lote](#invoking-an-azure-ml-web-service-using-the-batch-execution-activity) secção para obter detalhes.

Ao longo do tempo, os modelos preditivos de Olá nas experimentações classificação do Azure ML Olá necessário toobe retrained utilizando conjuntos de dados de entrada novo. Pode a reparametrização de um modelo do Azure ML de um pipeline do Data Factory efetuando Olá os seguintes passos:

1. Publica a experimentação de preparação de Olá (experimentação preditiva não) como um serviço web. Efetue este passo na Olá Azure ML Studio tal como fez experimentação preditiva tooexpose como um serviço web no cenário anterior Olá.
2. Utilize Olá atividade de execução de lote do Azure ML tooinvoke Olá web serviço para experimentação de preparação de Olá. Basicamente, pode utilizar tooinvoke da atividade de execução de lote do Azure ML Olá o serviço web de preparação e a classificação de serviço web.

Depois de terminar com reparametrização, atualizar Olá a classificação do serviço web (experimentação preditiva exposta como um serviço web) com o modelo treinado recentemente Olá utilizando Olá **da atividade de recursos de atualização do Azure ML**. Consulte [atualizar modelos de atividade do recurso da atualização](data-factory-azure-ml-update-resource-activity.md) artigo para obter detalhes.

## <a name="invoking-a-web-service-using-batch-execution-activity"></a>Invocar um serviço web utilizando a atividade de execução de lote
Utilizar o movimento de dados do Azure Data Factory tooorchestrate e processamento e, em seguida, efetuar a execução de lote através do Azure Machine Learning. Seguem-se passos de nível superior de Olá:

1. Crie um serviço ligado do Azure Machine Learning. É necessário Olá os seguintes valores:

   1. **URI de pedido** para Olá API de execução do Batch. Pode encontrar Olá URI pedido clicando Olá **de execução de lote** ligação na página de serviços web Olá.
   2. **Chave de API** para Olá publicado serviço web Azure Machine Learning. Pode encontrar a chave de API de Olá, clicando em serviço web Olá que tiver publicado.
   3. Olá utilize **AzureMLBatchExecution** atividade.

      ![Dashboard do Machine Learning](./media/data-factory-azure-ml-batch-execution-activity/AzureMLDashboard.png)

      ![URI do batch](./media/data-factory-azure-ml-batch-execution-activity/batch-uri.png)

### <a name="scenario-experiments-using-web-service-inputsoutputs-that-refer-toodata-in-azure-blob-storage"></a>Cenário: Experimentações com o Web service entradas/saídas que se referem toodata no Blob Storage do Azure
Neste cenário, Olá serviço Web do Azure Machine Learning torna predições utilizando os dados de um ficheiro no armazenamento de Blobs do Azure e armazena os resultados de predição de Olá no armazenamento de BLOBs de Olá. Olá seguinte JSON define um pipeline do Data Factory com uma atividade AzureMLBatchExecution. atividade de Olá tem o conjunto de dados de Olá **DecisionTreeInputBlob** como entrada e **DecisionTreeResultBlob** como saída Olá. Olá **DecisionTreeInputBlob** é transmitida como um serviço web de entrada toohello por utilizando Olá **webServiceInput** propriedade JSON. Olá **DecisionTreeResultBlob** é transmitida como um serviço de Web de toohello de saída por utilizando Olá **webServiceOutputs** propriedade JSON.  

> [!IMPORTANT]
> Se o serviço web de Olá demora várias entradas, utilize Olá **webServiceInputs** propriedade em vez de utilizar **webServiceInput**. Consulte Olá [serviço Web requer várias entradas](#web-service-requires-multiple-inputs) secção para obter um exemplo de utilização Olá webServiceInputs propriedade.
>
> Conjuntos de dados que são referenciados por Olá **webServiceInput**/**webServiceInputs** e **webServiceOutputs** propriedades (no  **typeProperties**) também devem ser incluídas no Olá atividade **entradas** e **produz**.
>
> Na sua experimentação do Azure ML, entrada de serviço web e portas de saída e parâmetros globais têm nomes predefinidos ("input1", "input2") que pode personalizar. os nomes de Olá que utiliza para webServiceInputs, webServiceOutputs e globalParameters definições têm de corresponder exatamente nomes Olá nas experimentações Olá. Pode ver o payload de pedido do exemplo Olá na página de ajuda de execução de lote de Olá para o mapeamento de Olá esperado de tooverify de ponto final do Azure ML.
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
> Apenas entradas e saídas da atividade de AzureMLBatchExecution Olá podem ser transmitidas como parâmetros toohello serviço Web. Por exemplo, Olá acima fragmento JSON, DecisionTreeInputBlob é uma entrada toohello AzureMLBatchExecution atividade, que é transmitida como um serviço Web de entrada toohello através do parâmetro webServiceInput.   
>
>

### <a name="example"></a>Exemplo
Toohold de armazenamento do Azure este exemplo utiliza ambos Olá dados de entrada e de saída.

Recomendamos que leia Olá [construir o seu primeiro pipeline com o Data Factory] [ adf-build-1st-pipeline] tutorial antes de passar neste exemplo. Utilize artefactos de fábrica de dados de toocreate do Olá Editor do Data Factory (serviços ligados, conjuntos de dados, pipeline) neste exemplo.   

1. Criar um **serviço ligado** para sua **Storage do Azure**. Se hello ficheiros de entrada e saídos estão em contas de armazenamento diferente, terá dois serviços ligados. Eis um exemplo JSON:

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
2. Criar Olá **entrada** do Azure Data Factory **dataset**. Ao contrário de algumas outros Data Factory conjuntos de dados, estes conjuntos de dados tem de conter ambos **folderPath** e **fileName** valores. Pode utilizar partições toocause cada tooprocess (cada setor de dados) de execução do batch ou produzir entrada exclusiva e ficheiros de saída. Poderá ser necessário tooinclude algumas Olá tootransform de atividade a montante introduzir no formato de ficheiro CSV Olá e colocá-lo na conta de armazenamento Olá para cada setor. Nesse caso, não deverá incluir Olá **externo** e **externalData** definições mostradas na Olá seguinte exemplo e seu DecisionTreeInputBlob seria Olá conjunto de dados de saída de uma atividade diferente.

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

    O ficheiro csv de entrada tem de ter linha de cabeçalho de coluna Olá. Se estiver a utilizar Olá **atividade de cópia** toocreate/mover Olá csv para o armazenamento de BLOBs de Olá, deve definir a propriedade de receptores de Olá **blobWriterAddHeader** demasiado**verdadeiro**. Por exemplo:

    ```JSON
    sink:
    {
        "type": "BlobSink",     
        "blobWriterAddHeader": true
    }
    ```

    Se um ficheiro csv Olá não tem uma linha de cabeçalho de Olá, poderá ver Olá seguinte erro: **erro na atividade: erro ao ler a cadeia. Token inesperado: StartObject. Caminho ', linha 1, posição 1**.
3. Criar Olá **saída** do Azure Data Factory **dataset**. Este exemplo utiliza a criação de partições toocreate um caminho de saída exclusivo para cada execução do setor. Sem a criação de partições Olá, atividade Olá substituiria o ficheiro Olá.

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
4. Criar um **serviço ligado** do tipo: **AzureMLLinkedService**, fornecendo a chave de API de Olá e URL da execução de lote de modelo.

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
5. Por fim, criar um pipeline que contém um **AzureMLBatchExecution** atividade. Em runtime, o pipeline efetua Olá os seguintes passos:

   1. Obtém a localização de Olá do ficheiro de entrada Olá dos conjuntos de dados de entrada.
   2. Invoca a execução de lote do Azure Machine Learning Olá API
   3. Cópias Olá blob toohello batch execução saída fornecido no seu conjunto de dados de saída.

      > [!NOTE]
      > Atividade de AzureMLBatchExecution pode ter zero ou mais entradas e saídas de um ou mais.
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

      Ambos **iniciar** e **final** DateTime tem de constar [formato ISO](http://en.wikipedia.org/wiki/ISO_8601). Por exemplo: 2014-10-14T16:32:41Z. Olá **final** tempo é opcional. Se não especificar valor de Olá **final** propriedade, esta é calculada como "**início + 48 horas.**" pipeline de Olá toorun indefinidamente, especifique **9999-09-09** como valor de Olá para Olá **final** propriedade. Veja [Referência de Processamento de Scripts JSON](https://msdn.microsoft.com/library/dn835050.aspx) para obter mais detalhes sobre as propriedades de JSON.

      > [!NOTE]
      > A especificação de entrada para a atividade de AzureMLBatchExecution Olá é opcional.
      >
      >

### <a name="scenario-experiments-using-readerwriter-modules-toorefer-toodata-in-various-storages"></a>Cenário: Experimentações com módulos de leitor/escritor toorefer toodata no armazenamento de vários
Outro cenário típico possível quando criar experimentações do Azure ML é toouse leitor e escritor módulos. módulo leitor de Olá é utilizado tooload dados para uma experimentação e módulo de escritor Olá é toosave dados a partir das suas experimentações. Para obter detalhes sobre o leitor e escritor módulos, consulte [leitor](https://msdn.microsoft.com/library/azure/dn905997.aspx) e [escritor](https://msdn.microsoft.com/library/azure/dn905984.aspx) tópicos da biblioteca MSDN.     

Quando utilizar módulos de leitor e escritor Olá, é boa prática toouse um parâmetro de serviço Web para cada propriedade estes módulos de leitor/escritor. Estes parâmetros web permitem-lhe os valores de Olá tooconfigure durante o tempo de execução. Por exemplo, pode criar uma experimentação com um módulo leitor de que utiliza uma base de dados do SQL do Azure: XXX.database.windows.net. Depois de implementar o serviço web de Olá, quer tooenable consumidores Olá Olá web service toospecify outro servidor de SQL do Azure chamado YYY.database.windows.net. Pode utilizar um tooallow de parâmetro de serviço Web toobe este valor configurado.

> [!NOTE]
> Entrada de serviço Web e de saída são diferentes dos parâmetros de serviço Web. No primeiro cenário Olá, constatou como uma entrada e saída podem ser especificados para um serviço Web do Azure ML. Neste cenário, passar parâmetros para um serviço Web que correspondem tooproperties dos módulos de leitor/escritor.
>
>

Vamos ver um cenário de utilização de parâmetros de serviço Web. Tem um serviço implementado de web Azure Machine Learning que utiliza uma data de tooread do módulo leitor a partir de uma das origens de dados de Olá suportadas pelo Azure Machine Learning (por exemplo: SQL Database do Azure). Após a execução de lote Olá é efetuada, resultados de Olá são escritos utilizando um módulo de escritor (SQL Database do Azure).  Não existem entradas de serviço web e saídas são definidas nas experimentações Olá. Neste caso, recomendamos que configure parâmetros de serviço web relevantes para módulos de leitor e escritor Olá. Esta configuração permite Olá leitor/escritor toobe módulos configurada quando utilizando Olá AzureMLBatchExecution atividade. Especifique os parâmetros do serviço Web na Olá **globalParameters** secção JSON da atividade Olá da seguinte forma.

```JSON
"typeProperties": {
    "globalParameters": {
        "Param 1": "Value 1",
        "Param 2": "Value 2"
    }
}
```

Também pode utilizar [funções da fábrica de dados](data-factory-functions-variables.md) em transmitir parâmetros de serviço Web, conforme mostrado no seguinte exemplo de Olá de valores para Olá:

```JSON
"typeProperties": {
    "globalParameters": {
       "Database query": "$$Text.Format('SELECT * FROM myTable WHERE timeColumn = \\'{0:yyyy-MM-dd HH:mm:ss}\\'', Time.AddHours(WindowStart, 0))"
    }
}
```

> [!NOTE]
> parâmetros de serviço Web de Olá são maiúsculas e minúsculas, por isso, certifique-se de que os nomes de Olá que especificar na atividade de Olá JSON corresponde Olá aqueles exposta pelo Olá serviço Web.
>
>

### <a name="using-a-reader-module-tooread-data-from-multiple-files-in-azure-blob"></a>Utilizar uma data de tooread do módulo leitor de vários ficheiros no Blob do Azure
Macrodados pipelines com atividades, tais como o Pig e ramo de registo pode produzir uma ou mais ficheiros de saída com nenhuma extensão. Por exemplo, quando especificar uma tabela do Hive externa, dados de Olá para a tabela de Hive externo Olá podem ser armazenados no blob storage do Azure com Olá seguir 000000_0 de nome. Pode utilizar o módulo de leitor de Olá no tooread experimentação vários ficheiros e utilizá-los para as predições.

Quando o módulo de leitor de Olá numa experimentação do Azure Machine Learning, pode especificar o Blob do Azure como entrada. ficheiros de Olá no Olá blob storage do Azure podem ser ficheiros de saída Olá (exemplo: 000000_0) que são produzidos pelo script Pig e ramo de registo em execução no HDInsight. Olá módulo leitor permite-lhe ficheiros tooread (com nenhuma extensão) configurando Olá **toocontainer de caminho, diretório/blob**. Olá **caminho toocontainer** pontos toohello contentor e **diretório/blob** pontos toofolder que contém ficheiros de Olá, conforme mostrado no Olá seguinte imagem. ou seja, a asterisco Olá \*) **Especifica que todos os ficheiros no contentor de Olá/pasta de Olá (ou seja, dados/aggregateddata/ano = mês/2014-6 /\*)** sejam de leitura como parte da experimentação Olá.

![Propriedades de Blob do Azure](./media/data-factory-create-predictive-pipelines/azure-blob-properties.png)

### <a name="example"></a>Exemplo
#### <a name="pipeline-with-azuremlbatchexecution-activity-with-web-service-parameters"></a>Pipeline com atividade AzureMLBatchExecution com parâmetros de serviço Web

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

No Olá acima exemplo JSON:

* Olá implementado o Azure Machine Learning Web service utiliza um leitor e um escritor módulo tooread/escrita de dados do / tooan SQL Database do Azure. Este serviço Web expõe Olá seguintes quatro parâmetros: nome do servidor, nome de base de dados, nome de conta de utilizador do servidor e palavra-passe de conta de utilizador servidor de base de dados.  
* Ambos **iniciar** e **final** DateTime tem de constar [formato ISO](http://en.wikipedia.org/wiki/ISO_8601). Por exemplo: 2014-10-14T16:32:41Z. Olá **final** tempo é opcional. Se não especificar valor de Olá **final** propriedade, esta é calculada como "**início + 48 horas.**" pipeline de Olá toorun indefinidamente, especifique **9999-09-09** como valor de Olá para Olá **final** propriedade. Veja [Referência de Processamento de Scripts JSON](https://msdn.microsoft.com/library/dn835050.aspx) para obter mais detalhes sobre as propriedades de JSON.

### <a name="other-scenarios"></a>Outros cenários
#### <a name="web-service-requires-multiple-inputs"></a>Serviço Web requer várias entradas
Se o serviço web de Olá demora várias entradas, utilize Olá **webServiceInputs** propriedade em vez de utilizar **webServiceInput**. Conjuntos de dados que são referenciados por Olá **webServiceInputs** também devem ser incluídas no Olá atividade **entradas**.

Na sua experimentação do Azure ML, entrada de serviço web e portas de saída e parâmetros globais têm nomes predefinidos ("input1", "input2") que pode personalizar. os nomes de Olá que utiliza para webServiceInputs, webServiceOutputs e globalParameters definições têm de corresponder exatamente nomes Olá nas experimentações Olá. Pode ver o payload de pedido do exemplo Olá na página de ajuda de execução de lote de Olá para o mapeamento de Olá esperado de tooverify de ponto final do Azure ML.

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

#### <a name="web-service-does-not-require-an-input"></a>Serviço Web não necessita de uma entrada
Serviços do web de execução de lote do Azure ML pode ser utilizado toorun quaisquer fluxos de trabalho, por exemplo R ou scripts do Python, que pode não necessitar de quaisquer entradas. Em alternativa, experimentação Olá pode ser configurada com um módulo de leitor não expõe qualquer GlobalParameters. Nesse caso, Olá AzureMLBatchExecution atividade seria configurado da seguinte forma:

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

#### <a name="web-service-does-not-require-an-inputoutput"></a>Serviço Web não necessita de uma entrada/saída
Olá serviço de web de execução de lote do Azure ML poderá não ter qualquer saída de serviço Web configurada. Neste exemplo, não há nenhum serviço Web de entrada ou saída nem qualquer GlobalParameters configurados. Ainda há uma saída configurada na atividade de Olá próprio, mas não está a ser fornecido como um webServiceOutput.

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

#### <a name="web-service-uses-readers-and-writers-and-hello-activity-runs-only-when-other-activities-have-succeeded"></a>Leitores de utilizações de serviço Web e escritores e execuções de atividade Olá apenas quando outras atividades êxito
Olá do Azure ML web leitor e escritor módulos do serviço podem ser configurado toorun com ou sem quaisquer GlobalParameters. No entanto, poderá pretender que chama o serviço tooembed num pipeline que utiliza o serviço do conjunto de dados dependências tooinvoke Olá apenas quando concluir algumas processamento a montante. Também pode acionar qualquer outra ação após conclusão da execução de lote Olá através desta abordagem. Nesse caso, pode express dependências Olá com entradas de atividade e saídas, sem qualquer um deles de nomenclatura como serviço Web entradas ou saídas.

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

Olá **takeaways** são:

* Se o ponto final de experimentação utiliza um webServiceInput: Este é representada por um conjunto de dados de blob e está incluído no entradas de atividade Olá e a propriedade de webServiceInput Olá. Caso contrário, a propriedade de webServiceInput Olá for omitida.
* Se o ponto final de experimentação utiliza webServiceOutput(s): estes são representados por conjuntos de dados de blob e incluídas na saídas da atividade de Olá e na propriedade de webServiceOutputs Olá. Olá atividade produz e webServiceOutputs estão mapeados com nome Olá cada resultado na experimentação de Olá. Caso contrário, a propriedade de webServiceOutputs Olá for omitida.
* Se o ponto final de experimentação expõe globalParameter(s), são fornecidos na propriedade de globalParameters Olá atividade como chave, pares de valor. Caso contrário, a propriedade de globalParameters Olá for omitida. as chaves de Olá são maiúsculas e minúsculas. [Funções do Azure Data Factory](data-factory-functions-variables.md) podem ser utilizadas em valores de Olá.
* Conjuntos de dados adicionais podem ser incluídos Olá entradas e saídas propriedades da atividade, sem a ser referenciado em Olá typeProperties de atividade. Estes conjuntos de dados governem execução utilizando dependências de setor mas caso contrário, são ignorados pelos Olá AzureMLBatchExecution atividade.


## <a name="updating-models-using-update-resource-activity"></a>Atualizar Modelos de atividade do recurso da atualização
Depois de terminar com reparametrização, atualizar Olá a classificação do serviço web (experimentação preditiva exposta como um serviço web) com o modelo treinado recentemente Olá utilizando Olá **da atividade de recursos de atualização do Azure ML**. Consulte [atualizar modelos de atividade do recurso da atualização](data-factory-azure-ml-update-resource-activity.md) artigo para obter detalhes.

### <a name="reader-and-writer-modules"></a>Leitor e escritor módulos
Um cenário comum para utilizar os parâmetros do serviço Web é a utilização de Olá de leitores de SQL do Azure e escritores. módulo leitor de Olá é utilizado tooload dados para uma experimentação de serviços de gestão de dados fora do Azure Machine Learning Studio. módulo de escritor Olá é toosave dados a partir das suas experimentações para os serviços de gestão de dados fora do Azure Machine Learning Studio.  

Para obter detalhes sobre o Azure Blob/Azure SQL. o leitor/escritor, consulte [leitor](https://msdn.microsoft.com/library/azure/dn905997.aspx) e [escritor](https://msdn.microsoft.com/library/azure/dn905984.aspx) tópicos da biblioteca MSDN. exemplo de Olá na secção anterior Olá utilizado leitor de Blob do Azure de Olá e escritor de Blob do Azure. Esta secção explica como utilizar o leitor de SQL do Azure e o escritor SQL do Azure.

## <a name="frequently-asked-questions"></a>Perguntas mais frequentes
**P:** tiver vários ficheiros que foram gerados por meu pipelines de macrodados. Pode utilizar Olá AzureMLBatchExecution atividade toowork em todos os ficheiros de Olá?

**R:** Sim. Consulte Olá **utilizando uma data de tooread do módulo leitor de vários ficheiros no Blob do Azure** secção para obter detalhes.

## <a name="azure-ml-batch-scoring-activity"></a>Atividade de classificação de lote do Azure ML
Se estiver a utilizar Olá **AzureMLBatchScoring** toointegrate de atividade com o Azure Machine Learning, recomendamos que utilize Olá mais recente **AzureMLBatchExecution** atividade.

Olá AzureMLBatchExecution atividade é introduzida no Olá versão de Agosto de 2015 do SDK do Azure e o Azure PowerShell.

Se quiser toocontinue utilizando Olá AzureMLBatchScoring atividade, continue a ler através desta secção.  

### <a name="azure-ml-batch-scoring-activity-using-azure-storage-for-inputoutput"></a>Classificação de lote ML atividade do Azure utilizando o armazenamento do Azure para a entrada/saída

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

### <a name="web-service-parameters"></a>Parâmetros do serviço Web
toospecify valores para parâmetros de serviço Web, adicione um **typeProperties** secção toohello **AzureMLBatchScoringActivty** secção Olá JSON do pipeline conforme mostrado no seguinte exemplo de Olá:

```JSON
"typeProperties": {
    "webServiceParameters": {
        "Param 1": "Value 1",
        "Param 2": "Value 2"
    }
}
```
Também pode utilizar [funções da fábrica de dados](data-factory-functions-variables.md) em transmitir parâmetros de serviço Web, conforme mostrado no seguinte exemplo de Olá de valores para Olá:

```JSON
"typeProperties": {
    "webServiceParameters": {
       "Database query": "$$Text.Format('SELECT * FROM myTable WHERE timeColumn = \\'{0:yyyy-MM-dd HH:mm:ss}\\'', Time.AddHours(WindowStart, 0))"
    }
}
```

> [!NOTE]
> parâmetros de serviço Web de Olá são maiúsculas e minúsculas, por isso, certifique-se de que os nomes de Olá que especificar na atividade de Olá JSON corresponde Olá aqueles exposta pelo Olá serviço Web.
>
>

## <a name="see-also"></a>Veja Também
* [Mensagem de blogue do Azure: introdução ao Azure Data Factory e o Azure Machine Learning](https://azure.microsoft.com/blog/getting-started-with-azure-data-factory-and-azure-machine-learning-4/)

[adf-build-1st-pipeline]: data-factory-build-your-first-pipeline.md

[azure-machine-learning]: http://azure.microsoft.com/services/machine-learning/
