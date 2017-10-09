---
title: "aaaBuild a primeira fábrica de dados (modelo do Resource Manager) | Microsoft Docs"
description: Neste tutorial, vai criar um exemplo de pipeline do Azure Data Factory com um modelo do Azure Resource Manager.
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: eb9e70b9-a13a-4a27-8256-2759496be470
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: fa08cd1ac3a0e5c5bf4bd4c6bd9dfa6dba9f4319
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-build-your-first-azure-data-factory-using-azure-resource-manager-template"></a>Tutorial: Criar a primeira fábrica de dados do Azure com o modelo Azure Resource Manager
> [!div class="op_single_selector"]
> * [Descrição geral e pré-requisitos](data-factory-build-your-first-pipeline.md)
> * [Portal do Azure](data-factory-build-your-first-pipeline-using-editor.md)
> * [Visual Studio](data-factory-build-your-first-pipeline-using-vs.md)
> * [PowerShell](data-factory-build-your-first-pipeline-using-powershell.md)
> * [Modelo do Resource Manager](data-factory-build-your-first-pipeline-using-arm.md)
> * [API REST](data-factory-build-your-first-pipeline-using-rest-api.md)
> 
> 

Neste artigo, utilize um toocreate de modelo Azure Resource Manager a primeira fábrica de dados do Azure. toodo Olá tutorial, utilizando outras ferramentas/SDKs, selecione uma das opções de Olá Olá na lista pendente.

pipeline de Olá neste tutorial tem uma atividade: **atividade do ramo de registo do HDInsight**. Esta atividade executa um script de ramo de registo num cluster do Azure HDInsight transformações dados de saída de tooproduce de dados de entrada. pipeline de Olá é agendada toorun depois de um mês entre Olá especificado tempos de início e de fim. 

> [!NOTE]
> pipeline de dados de Olá neste tutorial transforma dados de saída de tooproduce de dados de entrada. Para um tutorial sobre como os dados de toocopy utilizando o Azure Data Factory, consulte [Tutorial: copiar dados do Blob Storage tooSQL da base de dados](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).
> 
> pipeline de Olá neste tutorial tem apenas uma atividade do tipo: HDInsightHive. Um pipeline pode ter mais de uma atividade. Além disso, pode encadeiam duas atividades (executadas uma atividade após outro) definindo o conjunto de dados de saída de Olá de uma atividade como Olá de entrada de conjunto de dados de Olá outra atividade. Para obter mais informações, veja [scheduling and execution in Data Factory](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline) (agendamento e execução no Data Factory). 

## <a name="prerequisites"></a>Pré-requisitos
* Leia [descrição geral do Tutorial](data-factory-build-your-first-pipeline.md) artigo e Olá concluída **pré-requisito** passos.
* Siga as instruções em [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview) artigo tooinstall versão mais recente do Azure PowerShell no seu computador.
* Consulte [criação de modelos do Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md) toolearn sobre modelos Azure Resource Manager. 

## <a name="in-this-tutorial"></a>Neste tutorial
| Entidade | Descrição |
| --- | --- |
| Serviço ligado do Storage do Azure |Liga a fábrica de dados de toohello de conta do Storage do Azure. Olá contém Olá dados de entrada e de saída do pipeline de Olá neste exemplo de conta de armazenamento do Azure. |
| Serviço ligado do HDInsight a pedido |Uma fábrica de dados a pedido HDInsight cluster toohello ligações. cluster de Olá é criado automaticamente para si tooprocess dados e é eliminado após o processamento de Olá terminar. |
| Conjunto de dados de entrada de Blobs do Azure |Refere-se o serviço ligado do Storage do Azure de toohello. Olá serviço ligado refere-se conta de armazenamento do Azure tooan e conjunto de dados de Blobs do Azure de Olá Especifica contentor Olá, pasta e nome de ficheiro no armazenamento de Olá que contém dados de entrada Olá. |
| Conjunto de dados de saída do Blob do Azure |Refere-se o serviço ligado do Storage do Azure de toohello. Olá serviço ligado refere-se conta de armazenamento do Azure tooan e conjunto de dados de Blobs do Azure de Olá Especifica contentor Olá, pasta e nome de ficheiro no armazenamento de Olá que contém dados de saída Olá. |
| Pipeline de dados |pipeline de Olá tem uma atividade do tipo HDInsightHive, o que consome Olá conjunto de dados de entrada e produz o conjunto de dados de saída de Olá. |

Uma fábrica de dados pode ter um ou mais pipelines. Um pipeline pode conter uma atividade ou mais. Existem dois tipos de atividades: [atividades de movimento de dados](data-factory-data-movement-activities.md) e [atividades de transformação de dados](data-factory-data-transformation-activities.md). Neste tutorial, pode criar um pipeline com uma atividade (atividade do Hive).

Olá seguinte secção fornece modelo de Gestor de recursos completo Olá para definir as entidades do Data Factory para que pode percorrer Olá tutorial e teste Olá modelo rapidamente. toounderstand a cada entidade de fábrica de dados estiver definida, consulte [entidades do Data Factory no modelo de Olá](#data-factory-entities-in-the-template) secção.

## <a name="data-factory-json-template"></a>Modelo JSON do Data Factory
modelo do Resource Manager de nível superior do Olá para definir uma fábrica de dados é: 

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": { ...
    },
    "variables": { ...
    },
    "resources": [
        {
            "name": "[parameters('dataFactoryName')]",
            "apiVersion": "[variables('apiVersion')]",
            "type": "Microsoft.DataFactory/datafactories",
            "location": "westus",
            "resources": [
                { ... },
                { ... },
                { ... },
                { ... }
            ]
        }
    ]
}
```
Crie um ficheiro JSON com o nome **adftutorialarm. JSON** no **C:\ADFGetStarted** pasta com Olá seguinte conteúdo:

```json
{
    "contentVersion": "1.0.0.0",
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "parameters": {
        "storageAccountName": { "type": "string", "metadata": { "description": "Name of hello Azure storage account that contains hello input/output data." } },
          "storageAccountKey": { "type": "securestring", "metadata": { "description": "Key for hello Azure storage account." } },
          "blobContainer": { "type": "string", "metadata": { "description": "Name of hello blob container in hello Azure Storage account." } },
          "inputBlobFolder": { "type": "string", "metadata": { "description": "hello folder in hello blob container that has hello input file." } },
          "inputBlobName": { "type": "string", "metadata": { "description": "Name of hello input file/blob." } },
          "outputBlobFolder": { "type": "string", "metadata": { "description": "hello folder in hello blob container that will hold hello transformed data." } },
          "hiveScriptFolder": { "type": "string", "metadata": { "description": "hello folder in hello blob container that contains hello Hive query file." } },
          "hiveScriptFile": { "type": "string", "metadata": { "description": "Name of hello hive query (HQL) file." } }
    },
    "variables": {
          "dataFactoryName": "[concat('HiveTransformDF', uniqueString(resourceGroup().id))]",
          "azureStorageLinkedServiceName": "AzureStorageLinkedService",
          "hdInsightOnDemandLinkedServiceName": "HDInsightOnDemandLinkedService",
          "blobInputDatasetName": "AzureBlobInput",
          "blobOutputDatasetName": "AzureBlobOutput",
          "pipelineName": "HiveTransformPipeline"
    },
    "resources": [
      {
        "name": "[variables('dataFactoryName')]",
        "apiVersion": "2015-10-01",
        "type": "Microsoft.DataFactory/datafactories",
        "location": "West US",
        "resources": [
          {
            "type": "linkedservices",
            "name": "[variables('azureStorageLinkedServiceName')]",
            "dependsOn": [
                  "[variables('dataFactoryName')]"
            ],
            "apiVersion": "2015-10-01",
            "properties": {
                  "type": "AzureStorage",
                  "description": "Azure Storage linked service",
                  "typeProperties": {
                    "connectionString": "[concat('DefaultEndpointsProtocol=https;AccountName=',parameters('storageAccountName'),';AccountKey=',parameters('storageAccountKey'))]"
                  }
            }
          },
          {
            "type": "linkedservices",
            "name": "[variables('hdInsightOnDemandLinkedServiceName')]",
            "dependsOn": [
                  "[variables('dataFactoryName')]",
                  "[variables('azureStorageLinkedServiceName')]"
            ],
            "apiVersion": "2015-10-01",
            "properties": {
                  "type": "HDInsightOnDemand",
                  "typeProperties": {
                    "version": "3.5",
                    "clusterSize": 1,
                    "timeToLive": "00:05:00",
                    "osType": "Linux",
                    "linkedServiceName": "[variables('azureStorageLinkedServiceName')]"
                  }
            }
          },
          {
            "type": "datasets",
            "name": "[variables('blobInputDatasetName')]",
            "dependsOn": [
                  "[variables('dataFactoryName')]",
                  "[variables('azureStorageLinkedServiceName')]"
            ],
            "apiVersion": "2015-10-01",
            "properties": {
                  "type": "AzureBlob",
                  "linkedServiceName": "[variables('azureStorageLinkedServiceName')]",
                  "typeProperties": {
                    "fileName": "[parameters('inputBlobName')]",
                    "folderPath": "[concat(parameters('blobContainer'), '/', parameters('inputBlobFolder'))]",
                    "format": {
                          "type": "TextFormat",
                          "columnDelimiter": ","
                    }
                  },
                  "availability": {
                    "frequency": "Month",
                    "interval": 1
                  },
                  "external": true
            }
          },
          {
            "type": "datasets",
            "name": "[variables('blobOutputDatasetName')]",
            "dependsOn": [
                  "[variables('dataFactoryName')]",
                  "[variables('azureStorageLinkedServiceName')]"
            ],
            "apiVersion": "2015-10-01",
            "properties": {
                  "type": "AzureBlob",
                  "linkedServiceName": "[variables('azureStorageLinkedServiceName')]",
                  "typeProperties": {
                    "folderPath": "[concat(parameters('blobContainer'), '/', parameters('outputBlobFolder'))]",
                    "format": {
                          "type": "TextFormat",
                          "columnDelimiter": ","
                    }
                  },
                  "availability": {
                    "frequency": "Month",
                    "interval": 1
                  }
            }
          },
          {
            "type": "datapipelines",
            "name": "[variables('pipelineName')]",
            "dependsOn": [
                  "[variables('dataFactoryName')]",
                  "[variables('azureStorageLinkedServiceName')]",
                  "[variables('hdInsightOnDemandLinkedServiceName')]",
                  "[variables('blobInputDatasetName')]",
                  "[variables('blobOutputDatasetName')]"
            ],
            "apiVersion": "2015-10-01",
            "properties": {
                  "description": "Pipeline that transforms data using Hive script.",
                  "activities": [
                {
                      "type": "HDInsightHive",
                      "typeProperties": {
                        "scriptPath": "[concat(parameters('blobContainer'), '/', parameters('hiveScriptFolder'), '/', parameters('hiveScriptFile'))]",
                        "scriptLinkedService": "[variables('azureStorageLinkedServiceName')]",
                        "defines": {
                              "inputtable": "[concat('wasb://', parameters('blobContainer'), '@', parameters('storageAccountName'), '.blob.core.windows.net/', parameters('inputBlobFolder'))]",
                              "partitionedtable": "[concat('wasb://', parameters('blobContainer'), '@', parameters('storageAccountName'), '.blob.core.windows.net/', parameters('outputBlobFolder'))]"
                        }
                      },
                      "inputs": [
                        {
                              "name": "[variables('blobInputDatasetName')]"
                        }
                      ],
                      "outputs": [
                        {
                              "name": "[variables('blobOutputDatasetName')]"
                        }
                      ],
                      "policy": {
                        "concurrency": 1,
                        "retry": 3
                      },
                      "scheduler": {
                        "frequency": "Month",
                        "interval": 1
                      },
                      "name": "RunSampleHiveActivity",
                      "linkedServiceName": "[variables('hdInsightOnDemandLinkedServiceName')]"
                }
                  ],
                  "start": "2017-07-01T00:00:00Z",
                  "end": "2017-07-02T00:00:00Z",
                  "isPaused": false
              }
          }
        ]
      }
    ]
}
```

> [!NOTE]
> Pode encontrar outro exemplo do modelo do Resource Manager para criar uma fábrica de dados do Azure no [Tutorial: criar um pipeline com a Atividade de Cópia utilizando um modelo do Azure Resource Manager](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md).  
> 
> 

## <a name="parameters-json"></a>Parâmetros JSON
Crie um ficheiro JSON com o nome **ADFTutorialARM-Parameters. JSON** que contém os parâmetros de modelo do Azure Resource Manager Olá.  

> [!IMPORTANT]
> Especifique o nome de Olá e a chave da sua conta do Storage do Azure para Olá **storageAccountName** e **storageAccountKey** parâmetros neste ficheiro de parâmetros. 
> 
> 

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "storageAccountName": {
            "value": "<Name of your Azure Storage account>"
        },
        "storageAccountKey": {
            "value": "<Key of your Azure Storage account>"
        },
        "blobContainer": {
            "value": "adfgetstarted"
        },
        "inputBlobFolder": {
            "value": "inputdata"
        },
        "inputBlobName": {
            "value": "input.log"
        },
        "outputBlobFolder": {
            "value": "partitioneddata"
        },
        "hiveScriptFolder": {
              "value": "script"
        },
        "hiveScriptFile": {
              "value": "partitionweblogs.hql"
        }
    }
}
```

> [!IMPORTANT]
> Pode ter ficheiros JSON do parâmetro separado para o desenvolvimento, teste e ambientes de produção que pode utilizar com Olá mesmo modelo JSON de fábrica de dados. Ao utilizar um script do Power Shell, pode automatizar a implementação de entidades do Data Factory nestes ambientes. 
> 
> 

## <a name="create-data-factory"></a>Criar fábrica de dados
1. Iniciar **Azure PowerShell** e Olá execute os seguintes comandos: 
   * Execute Olá os seguintes comandos e introduza o nome de utilizador de Olá e a palavra-passe que utilizam toosign no toohello portal do Azure.
    ```PowerShell
    Login-AzureRmAccount
    ```  
   * Execute Olá tooview de comando a seguir todas as subscrições de Olá para esta conta.
    ```PowerShell
    Get-AzureRmSubscription
    ``` 
   * Execute Olá comando tooselect Olá subscrição que pretende que toowork com os seguintes. Esta subscrição deve ser Olá igual à Olá utilizada no Olá portal do Azure.
    ```
    Get-AzureRmSubscription -SubscriptionName <SUBSCRIPTION NAME> | Set-AzureRmContext
    ```   
2. Execute Olá seguintes entidades do Data Factory comando toodeploy utilizando o modelo do Resource Manager Olá que criou no passo 1. 

    ```PowerShell
    New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile C:\ADFGetStarted\ADFTutorialARM.json -TemplateParameterFile C:\ADFGetStarted\ADFTutorialARM-Parameters.json
    ```

## <a name="monitor-pipeline"></a>Monitorizar o pipeline
1. Após iniciar sessão toohello [portal do Azure](https://portal.azure.com/), clique em **procurar** e selecione **fábricas de dados**.
     ![Procurar->Fábricas de dados](./media/data-factory-build-your-first-pipeline-using-arm/BrowseDataFactories.png)
2. No Olá **fábricas de dados** painel, clique em fábrica de dados de Olá (**TutorialFactoryARM**) que criou.    
3. No Olá **Data Factory** painel para a fábrica de dados, clique em **diagrama**.

     ![Mosaico do Diagrama](./media/data-factory-build-your-first-pipeline-using-arm/DiagramTile.png)
4. No Olá **vista de diagrama**, verá uma descrição geral dos pipelines Olá e conjuntos de dados utilizado neste tutorial.
   
   ![Vista de Diagrama](./media/data-factory-build-your-first-pipeline-using-arm/DiagramView.png) 
5. Na vista de diagrama Olá, faça duplo clique em dataset Olá **AzureBlobOutput**. Verá o setor que Olá que está atualmente a ser processado.
   
    ![Conjunto de dados](./media/data-factory-build-your-first-pipeline-using-arm/AzureBlobOutput.png)
6. Quando o processamento terminar, verá o setor de Olá no **pronto** estado. A criação de um cluster do HDInsight a pedido demora, por norma, algum tempo (cerca de 20 minutos). Por conseguinte, esperar Olá pipeline tootake **aproximadamente 30 minutos** tooprocess Olá setor.
   
    ![Conjunto de dados](./media/data-factory-build-your-first-pipeline-using-arm/SliceReady.png)    
7. Quando Olá setor estiver no **pronto** de estado, verifique Olá **partitioneddata** pasta Olá **adfgetstarted** dados de saída do contentor de armazenamento de BLOBs para Olá.  

Consulte [monitorizar os conjuntos de dados e pipeline](data-factory-monitor-manage-pipelines.md) para obter instruções sobre como o pipeline de Olá do toouse Olá os painéis do portal do Azure toomonitor e conjuntos de dados que criou neste tutorial.

Também pode utilizar toomonitor monitorizar e gerir aplicações seus pipelines de dados. Consulte [monitorizar e gerir pipelines do Azure Data Factory com a aplicação de monitorização](data-factory-monitor-manage-app.md) para obter detalhes sobre como utilizar a aplicação Olá. 

> [!IMPORTANT]
> ficheiro de entrada Olá é eliminado quando o setor de Olá é processado com êxito. Por conseguinte, se pretender setor de Olá toorerun ou Olá novamente o tutorial, carregue Olá ficheiro de entrada (input.log) toohello na pasta inputdata do contentor adfgetstarted de Olá.
> 
> 

## <a name="data-factory-entities-in-hello-template"></a>Entidades da fábrica de dados no modelo de Olá
### <a name="define-data-factory"></a>Definir fábrica de dados
Definir uma fábrica de dados no modelo do Resource Manager Olá, conforme mostrado no seguinte exemplo de Olá:  

```json
"resources": [
{
    "name": "[variables('dataFactoryName')]",
    "apiVersion": "2015-10-01",
    "type": "Microsoft.DataFactory/datafactories",
    "location": "West US"
}
```
Olá dataFactoryName está definida como: 

```json
"dataFactoryName": "[concat('HiveTransformDF', uniqueString(resourceGroup().id))]",
```
É uma cadeia exclusiva com base no ID de grupo de recursos para Olá.  

### <a name="defining-data-factory-entities"></a>Definir entidades do Data Factory
Olá seguintes entidades do Data Factory estão definidas no modelo JSON Olá: 

* [Serviço ligado do Armazenamento do Azure](#azure-storage-linked-service)
* [Serviço ligado do HDInsight a pedido](#hdinsight-on-demand-linked-service)
* [Conjunto de dados de entrada do blobs do Azure](#azure-blob-input-dataset)
* [Conjunto de dados de saída do blob do Azure](#azure-blob-output-dataset)
* [Pipeline de dados com uma atividade de cópia](#data-pipeline)

#### <a name="azure-storage-linked-service"></a>Serviço ligado do Storage do Azure
Especifique o nome de Olá e a chave da sua conta de armazenamento do Azure nesta secção. Consulte [serviço ligado do Storage do Azure](data-factory-azure-blob-connector.md#azure-storage-linked-service) para obter detalhes sobre JSON as propriedades utilizadas toodefine um Azure serviço ligado do Storage. 

```json
{
    "type": "linkedservices",
    "name": "[variables('azureStorageLinkedServiceName')]",
    "dependsOn": [
        "[variables('dataFactoryName')]"
    ],
    "apiVersion": "2015-10-01",
    "properties": {
        "type": "AzureStorage",
        "description": "Azure Storage linked service",
        "typeProperties": {
            "connectionString": "[concat('DefaultEndpointsProtocol=https;AccountName=',parameters('storageAccountName'),';AccountKey=',parameters('storageAccountKey'))]"
        }
    }
}
```
Olá **connectionString** utiliza Olá storageAccountName e storageAccountKey parâmetros. Olá os valores para estes parâmetros transmitidos através da utilização de um ficheiro de configuração. definição de Olá também utiliza as variáveis: azureStroageLinkedService e dataFactoryName definido no modelo de Olá. 

#### <a name="hdinsight-on-demand-linked-service"></a>Serviço ligado do HDInsight a pedido
Consulte [serviços ligados de computação](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) artigo para obter detalhes sobre JSON as propriedades utilizadas toodefine um serviço ligado do HDInsight a pedido.  

```json
{
    "type": "linkedservices",
    "name": "[variables('hdInsightOnDemandLinkedServiceName')]",
    "dependsOn": [
        "[variables('dataFactoryName')]"
    ],
    "apiVersion": "2015-10-01",
    "properties": {
        "type": "HDInsightOnDemand",
        "typeProperties": {
            "version": "3.5",
            "clusterSize": 1,
            "timeToLive": "00:05:00",
            "osType": "Linux",
            "linkedServiceName": "[variables('azureStorageLinkedServiceName')]"
        }
    }
}
```
Tenha em atenção Olá seguintes pontos: 

* Olá Data Factory cria um **baseado em Linux** cluster do HDInsight com Olá acima JSON. Veja [On-demand HDInsight Linked Service (Serviço Ligado do HDInsight a Pedido)](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) para obter detalhes. 
* Também pode utilizar o **seu próprio cluster do HDInsight** em vez de utilizar um cluster do HDInsight a pedido. Veja [HDInsight Linked Service (Serviço Ligado do HDInsight)](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) para obter detalhes.
* cluster do HDInsight Olá cria um **contentor predefinido** no armazenamento de BLOBs de Olá especificado na Olá JSON (**linkedServiceName**). HDInsight não é eliminado deste contentor quando cluster Olá é eliminado. Este comportamento é propositado. Com o serviço de ligado de HDInsight a pedido, é criado um cluster de HDInsight sempre que um setor tiver toobe processado, exceto se houver um cluster existente em direto (**timeToLive**) e é eliminado quando o processamento de Olá terminar.
  
    À medida que são processados mais setores, verá muitos contentores no armazenamento de blobs do Azure. Se não precisar deles para resolução de problemas de tarefas Olá, poderá ser útil toodelete-los armazenamento de Olá tooreduce custo. os nomes de Olá destes contentores seguem um padrão: "adf**nomedafábricadedados**-**linkedservicename**- datetimestamp". Utilize ferramentas como [Explorador de armazenamento do Microsoft](http://storageexplorer.com/) toodelete contentores no seu Azure armazenamento de Blobs.

Veja [On-demand HDInsight Linked Service (Serviço Ligado do HDInsight a Pedido)](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) para obter detalhes.

#### <a name="azure-blob-input-dataset"></a>Conjunto de dados de entrada de blobs do Azure
Especifique nomes de Olá do contentor de blob, pasta e ficheiro que contém dados de entrada Olá. Consulte [propriedades do conjunto de dados de Blobs do Azure](data-factory-azure-blob-connector.md#dataset-properties) para obter detalhes sobre as propriedades utilizadas de JSON toodefine um conjunto de dados de Blobs do Azure. 

```json
{
    "type": "datasets",
    "name": "[variables('blobInputDatasetName')]",
    "dependsOn": [
        "[variables('dataFactoryName')]",
        "[variables('azureStorageLinkedServiceName')]"
    ],
    "apiVersion": "2015-10-01",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "[variables('azureStorageLinkedServiceName')]",
        "typeProperties": {
            "fileName": "[parameters('inputBlobName')]",
            "folderPath": "[concat(parameters('blobContainer'), '/', parameters('inputBlobFolder'))]",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ","
            }
        },
        "availability": {
            "frequency": "Month",
            "interval": 1
        },
        "external": true
    }
}
```
Esta definição utiliza os seguintes parâmetros definidos no modelo de parâmetro de Olá: blobContainer, inputBlobFolder e inputBlobName. 

#### <a name="azure-blob-output-dataset"></a>Conjunto de dados de saída do Blob do Azure
Especifique nomes de Olá da pasta que contém dados de saída Olá e contentor de blob. Consulte [propriedades do conjunto de dados de Blobs do Azure](data-factory-azure-blob-connector.md#dataset-properties) para obter detalhes sobre as propriedades utilizadas de JSON toodefine um conjunto de dados de Blobs do Azure.  

```json
{
    "type": "datasets",
    "name": "[variables('blobOutputDatasetName')]",
    "dependsOn": [
        "[variables('dataFactoryName')]",
        "[variables('azureStorageLinkedServiceName')]"
    ],
    "apiVersion": "2015-10-01",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "[variables('azureStorageLinkedServiceName')]",
        "typeProperties": {
            "folderPath": "[concat(parameters('blobContainer'), '/', parameters('outputBlobFolder'))]",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ","
            }
        },
        "availability": {
            "frequency": "Month",
            "interval": 1
        }
    }
}
```

Esta definição utiliza Olá seguir os parâmetros definidos no modelo de parâmetro de Olá: blobContainer e outputBlobFolder. 

#### <a name="data-pipeline"></a>Pipeline de dados
Defina um pipeline que transforme dados executando o script de ramo de registo num cluster HDInsight a pedido do Azure. Consulte [JSON do Pipeline](data-factory-create-pipelines.md#pipeline-json) para obter descrições JSON elementos utilizados toodefine um pipeline neste exemplo. 

```json
{
    "type": "datapipelines",
    "name": "[variables('pipelineName')]",
    "dependsOn": [
        "[variables('dataFactoryName')]",
        "[variables('azureStorageLinkedServiceName')]",
        "[variables('hdInsightOnDemandLinkedServiceName')]",
        "[variables('blobInputDatasetName')]",
        "[variables('blobOutputDatasetName')]"
    ],
    "apiVersion": "2015-10-01",
    "properties": {
        "description": "Pipeline that transforms data using Hive script.",
        "activities": [
        {
            "type": "HDInsightHive",
            "typeProperties": {
                "scriptPath": "[concat(parameters('blobContainer'), '/', parameters('hiveScriptFolder'), '/', parameters('hiveScriptFile'))]",
                "scriptLinkedService": "[variables('azureStorageLinkedServiceName')]",
                "defines": {
                    "inputtable": "[concat('wasb://', parameters('blobContainer'), '@', parameters('storageAccountName'), '.blob.core.windows.net/', parameters('inputBlobFolder'))]",
                    "partitionedtable": "[concat('wasb://', parameters('blobContainer'), '@', parameters('storageAccountName'), '.blob.core.windows.net/', parameters('outputBlobFolder'))]"
                }
            },
            "inputs": [
            {
                "name": "[variables('blobInputDatasetName')]"
            }
            ],
            "outputs": [
            {
                "name": "[variables('blobOutputDatasetName')]"
            }
            ],
            "policy": {
                "concurrency": 1,
                "retry": 3
            },
            "scheduler": {
                "frequency": "Month",
                "interval": 1
            },
            "name": "RunSampleHiveActivity",
            "linkedServiceName": "[variables('hdInsightOnDemandLinkedServiceName')]"
        }
        ],
        "start": "2017-07-01T00:00:00Z",
        "end": "2017-07-02T00:00:00Z",
        "isPaused": false
    }
}
```

## <a name="reuse-hello-template"></a>Reutilizar o modelo de Olá
Olá tutorial, vai criar um modelo para definir entidades do Data Factory e um modelo para passar os valores de parâmetros. toouse Olá mesmos modelo toodeploy Data Factory entidades toodifferent ambientes, crie um ficheiro de parâmetro para cada ambiente e utilizá-lo quando implementar toothat ambiente.     

Exemplo:  

```PowerShell
New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFTutorialARM.json -TemplateParameterFile ADFTutorialARM-Parameters-Dev.json

New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFTutorialARM.json -TemplateParameterFile ADFTutorialARM-Parameters-Test.json

New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFTutorialARM.json -TemplateParameterFile ADFTutorialARM-Parameters-Production.json
```
Tenha em atenção que Olá primeiro parâmetro do comando utiliza o ficheiro para o ambiente de desenvolvimento de Olá, um segundo para o ambiente de teste de Olá e Olá uma terceira para ambiente de produção Olá.  

Também pode reutilizar Olá modelo tooperform repetido tarefas. Por exemplo, terá de toocreate várias fábricas de dados com um ou mais pipelines que implementam Olá mesma lógica, mas cada data factory utiliza diferentes storage do Azure e contas de SQL Database do Azure. Neste cenário, utilize Olá mesmo modelo no Olá mesmo ambiente (desenvolvimento, teste ou de produção) com o parâmetro diferentes ficheiros toocreate fábricas de dados. 

## <a name="resource-manager-template-for-creating-a-gateway"></a>Modelo do Resource Manager para criar um gateway
Segue-se um modelo de Gestor de recursos de exemplo para criar um gateway lógico no Olá novamente. Instalar um gateway no computador local ou VM do IaaS do Azure e registar o gateway de Olá com o serviço Data Factory com uma chave. Veja [Move data between on-premises and cloud (Mover dados entre o local e a nuvem)](data-factory-move-data-between-onprem-and-cloud.md) para obter detalhes.

```json
{
    "contentVersion": "1.0.0.0",
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "parameters": {
    },
    "variables": {
        "dataFactoryName":  "GatewayUsingArmDF",
        "apiVersion": "2015-10-01",
        "singleQuote": "'"
    },
    "resources": [
        {
            "name": "[variables('dataFactoryName')]",
            "apiVersion": "[variables('apiVersion')]",
            "type": "Microsoft.DataFactory/datafactories",
            "location": "eastus",
            "resources": [
                {
                    "dependsOn": [ "[concat('Microsoft.DataFactory/dataFactories/', variables('dataFactoryName'))]" ],
                    "type": "gateways",
                    "apiVersion": "[variables('apiVersion')]",
                    "name": "GatewayUsingARM",
                    "properties": {
                        "description": "my gateway"
                    }
                }            
            ]
        }
    ]
}
```
Este modelo cria uma fábrica de dados com o nome GatewayUsingArmDF com um gateway designado: GatewayUsingARM. 

## <a name="see-also"></a>Veja também
| Tópico | Descrição |
|:--- |:--- |
| [Pipelines](data-factory-create-pipelines.md) |Este artigo ajuda-o a compreender os pipelines e atividades no Azure Data Factory e como toouse-los tooconstruct ponto a ponto condicionados por dados fluxos de trabalho para o seu cenário ou empresa. |
| [Conjuntos de dados](data-factory-create-datasets.md) |Este artigo ajuda-o a compreender os conjuntos de dados no Azure Data Factory. |
| [Agendamento e execução](data-factory-scheduling-and-execution.md) |Este artigo explica os aspetos de agendamento e execução de Olá do modelo de aplicação do Azure Data Factory. |
| [Monitorizar e gerir pipelines com a Aplicação de Monitorização](data-factory-monitor-manage-app.md) |Este artigo descreve como toomonitor, gerir e depurar pipelines utilizando Olá de monitorização e gestão de aplicações. |

