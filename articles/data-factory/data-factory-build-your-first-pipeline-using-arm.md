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
# <a name="tutorial-build-your-first-azure-data-factory-using-azure-resource-manager-template"></a><span data-ttu-id="a8e3b-103">Tutorial: Criar a primeira fábrica de dados do Azure com o modelo Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="a8e3b-103">Tutorial: Build your first Azure data factory using Azure Resource Manager template</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a8e3b-104">Descrição geral e pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="a8e3b-104">Overview and prerequisites</span></span>](data-factory-build-your-first-pipeline.md)
> * [<span data-ttu-id="a8e3b-105">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="a8e3b-105">Azure portal</span></span>](data-factory-build-your-first-pipeline-using-editor.md)
> * [<span data-ttu-id="a8e3b-106">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="a8e3b-106">Visual Studio</span></span>](data-factory-build-your-first-pipeline-using-vs.md)
> * [<span data-ttu-id="a8e3b-107">PowerShell</span><span class="sxs-lookup"><span data-stu-id="a8e3b-107">PowerShell</span></span>](data-factory-build-your-first-pipeline-using-powershell.md)
> * [<span data-ttu-id="a8e3b-108">Modelo do Resource Manager</span><span class="sxs-lookup"><span data-stu-id="a8e3b-108">Resource Manager Template</span></span>](data-factory-build-your-first-pipeline-using-arm.md)
> * [<span data-ttu-id="a8e3b-109">API REST</span><span class="sxs-lookup"><span data-stu-id="a8e3b-109">REST API</span></span>](data-factory-build-your-first-pipeline-using-rest-api.md)
> 
> 

<span data-ttu-id="a8e3b-110">Neste artigo, utilize um toocreate de modelo Azure Resource Manager a primeira fábrica de dados do Azure.</span><span class="sxs-lookup"><span data-stu-id="a8e3b-110">In this article, you use an Azure Resource Manager template toocreate your first Azure data factory.</span></span> <span data-ttu-id="a8e3b-111">toodo Olá tutorial, utilizando outras ferramentas/SDKs, selecione uma das opções de Olá Olá na lista pendente.</span><span class="sxs-lookup"><span data-stu-id="a8e3b-111">toodo hello tutorial using other tools/SDKs, select one of hello options from hello drop-down list.</span></span>

<span data-ttu-id="a8e3b-112">pipeline de Olá neste tutorial tem uma atividade: **atividade do ramo de registo do HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="a8e3b-112">hello pipeline in this tutorial has one activity: **HDInsight Hive activity**.</span></span> <span data-ttu-id="a8e3b-113">Esta atividade executa um script de ramo de registo num cluster do Azure HDInsight transformações dados de saída de tooproduce de dados de entrada.</span><span class="sxs-lookup"><span data-stu-id="a8e3b-113">This activity runs a hive script on an Azure HDInsight cluster that transforms input data tooproduce output data.</span></span> <span data-ttu-id="a8e3b-114">pipeline de Olá é agendada toorun depois de um mês entre Olá especificado tempos de início e de fim.</span><span class="sxs-lookup"><span data-stu-id="a8e3b-114">hello pipeline is scheduled toorun once a month between hello specified start and end times.</span></span> 

> [!NOTE]
> <span data-ttu-id="a8e3b-115">pipeline de dados de Olá neste tutorial transforma dados de saída de tooproduce de dados de entrada.</span><span class="sxs-lookup"><span data-stu-id="a8e3b-115">hello data pipeline in this tutorial transforms input data tooproduce output data.</span></span> <span data-ttu-id="a8e3b-116">Para um tutorial sobre como os dados de toocopy utilizando o Azure Data Factory, consulte [Tutorial: copiar dados do Blob Storage tooSQL da base de dados](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="a8e3b-116">For a tutorial on how toocopy data using Azure Data Factory, see [Tutorial: Copy data from Blob Storage tooSQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>
> 
> <span data-ttu-id="a8e3b-117">pipeline de Olá neste tutorial tem apenas uma atividade do tipo: HDInsightHive.</span><span class="sxs-lookup"><span data-stu-id="a8e3b-117">hello pipeline in this tutorial has only one activity of type: HDInsightHive.</span></span> <span data-ttu-id="a8e3b-118">Um pipeline pode ter mais de uma atividade.</span><span class="sxs-lookup"><span data-stu-id="a8e3b-118">A pipeline can have more than one activity.</span></span> <span data-ttu-id="a8e3b-119">Além disso, pode encadeiam duas atividades (executadas uma atividade após outro) definindo o conjunto de dados de saída de Olá de uma atividade como Olá de entrada de conjunto de dados de Olá outra atividade.</span><span class="sxs-lookup"><span data-stu-id="a8e3b-119">And, you can chain two activities (run one activity after another) by setting hello output dataset of one activity as hello input dataset of hello other activity.</span></span> <span data-ttu-id="a8e3b-120">Para obter mais informações, veja [scheduling and execution in Data Factory](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline) (agendamento e execução no Data Factory).</span><span class="sxs-lookup"><span data-stu-id="a8e3b-120">For more information, see [scheduling and execution in Data Factory](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="a8e3b-121">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="a8e3b-121">Prerequisites</span></span>
* <span data-ttu-id="a8e3b-122">Leia [descrição geral do Tutorial](data-factory-build-your-first-pipeline.md) artigo e Olá concluída **pré-requisito** passos.</span><span class="sxs-lookup"><span data-stu-id="a8e3b-122">Read through [Tutorial Overview](data-factory-build-your-first-pipeline.md) article and complete hello **prerequisite** steps.</span></span>
* <span data-ttu-id="a8e3b-123">Siga as instruções em [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview) artigo tooinstall versão mais recente do Azure PowerShell no seu computador.</span><span class="sxs-lookup"><span data-stu-id="a8e3b-123">Follow instructions in [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) article tooinstall latest version of Azure PowerShell on your computer.</span></span>
* <span data-ttu-id="a8e3b-124">Consulte [criação de modelos do Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md) toolearn sobre modelos Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="a8e3b-124">See [Authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md) toolearn about Azure Resource Manager templates.</span></span> 

## <a name="in-this-tutorial"></a><span data-ttu-id="a8e3b-125">Neste tutorial</span><span class="sxs-lookup"><span data-stu-id="a8e3b-125">In this tutorial</span></span>
| <span data-ttu-id="a8e3b-126">Entidade</span><span class="sxs-lookup"><span data-stu-id="a8e3b-126">Entity</span></span> | <span data-ttu-id="a8e3b-127">Descrição</span><span class="sxs-lookup"><span data-stu-id="a8e3b-127">Description</span></span> |
| --- | --- |
| <span data-ttu-id="a8e3b-128">Serviço ligado do Storage do Azure</span><span class="sxs-lookup"><span data-stu-id="a8e3b-128">Azure Storage linked service</span></span> |<span data-ttu-id="a8e3b-129">Liga a fábrica de dados de toohello de conta do Storage do Azure.</span><span class="sxs-lookup"><span data-stu-id="a8e3b-129">Links your Azure Storage account toohello data factory.</span></span> <span data-ttu-id="a8e3b-130">Olá contém Olá dados de entrada e de saída do pipeline de Olá neste exemplo de conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="a8e3b-130">hello Azure Storage account holds hello input and output data for hello pipeline in this sample.</span></span> |
| <span data-ttu-id="a8e3b-131">Serviço ligado do HDInsight a pedido</span><span class="sxs-lookup"><span data-stu-id="a8e3b-131">HDInsight on-demand linked service</span></span> |<span data-ttu-id="a8e3b-132">Uma fábrica de dados a pedido HDInsight cluster toohello ligações.</span><span class="sxs-lookup"><span data-stu-id="a8e3b-132">Links an on-demand HDInsight cluster toohello data factory.</span></span> <span data-ttu-id="a8e3b-133">cluster de Olá é criado automaticamente para si tooprocess dados e é eliminado após o processamento de Olá terminar.</span><span class="sxs-lookup"><span data-stu-id="a8e3b-133">hello cluster is automatically created for you tooprocess data and is deleted after hello processing is done.</span></span> |
| <span data-ttu-id="a8e3b-134">Conjunto de dados de entrada de Blobs do Azure</span><span class="sxs-lookup"><span data-stu-id="a8e3b-134">Azure Blob input dataset</span></span> |<span data-ttu-id="a8e3b-135">Refere-se o serviço ligado do Storage do Azure de toohello.</span><span class="sxs-lookup"><span data-stu-id="a8e3b-135">Refers toohello Azure Storage linked service.</span></span> <span data-ttu-id="a8e3b-136">Olá serviço ligado refere-se conta de armazenamento do Azure tooan e conjunto de dados de Blobs do Azure de Olá Especifica contentor Olá, pasta e nome de ficheiro no armazenamento de Olá que contém dados de entrada Olá.</span><span class="sxs-lookup"><span data-stu-id="a8e3b-136">hello linked service refers tooan Azure Storage account and hello Azure Blob dataset specifies hello container, folder, and file name in hello storage that holds hello input data.</span></span> |
| <span data-ttu-id="a8e3b-137">Conjunto de dados de saída do Blob do Azure</span><span class="sxs-lookup"><span data-stu-id="a8e3b-137">Azure Blob output dataset</span></span> |<span data-ttu-id="a8e3b-138">Refere-se o serviço ligado do Storage do Azure de toohello.</span><span class="sxs-lookup"><span data-stu-id="a8e3b-138">Refers toohello Azure Storage linked service.</span></span> <span data-ttu-id="a8e3b-139">Olá serviço ligado refere-se conta de armazenamento do Azure tooan e conjunto de dados de Blobs do Azure de Olá Especifica contentor Olá, pasta e nome de ficheiro no armazenamento de Olá que contém dados de saída Olá.</span><span class="sxs-lookup"><span data-stu-id="a8e3b-139">hello linked service refers tooan Azure Storage account and hello Azure Blob dataset specifies hello container, folder, and file name in hello storage that holds hello output data.</span></span> |
| <span data-ttu-id="a8e3b-140">Pipeline de dados</span><span class="sxs-lookup"><span data-stu-id="a8e3b-140">Data pipeline</span></span> |<span data-ttu-id="a8e3b-141">pipeline de Olá tem uma atividade do tipo HDInsightHive, o que consome Olá conjunto de dados de entrada e produz o conjunto de dados de saída de Olá.</span><span class="sxs-lookup"><span data-stu-id="a8e3b-141">hello pipeline has one activity of type HDInsightHive, which consumes hello input dataset and produces hello output dataset.</span></span> |

<span data-ttu-id="a8e3b-142">Uma fábrica de dados pode ter um ou mais pipelines.</span><span class="sxs-lookup"><span data-stu-id="a8e3b-142">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="a8e3b-143">Um pipeline pode conter uma atividade ou mais.</span><span class="sxs-lookup"><span data-stu-id="a8e3b-143">A pipeline can have one or more activities in it.</span></span> <span data-ttu-id="a8e3b-144">Existem dois tipos de atividades: [atividades de movimento de dados](data-factory-data-movement-activities.md) e [atividades de transformação de dados](data-factory-data-transformation-activities.md).</span><span class="sxs-lookup"><span data-stu-id="a8e3b-144">There are two types of activities: [data movement activities](data-factory-data-movement-activities.md) and [data transformation activities](data-factory-data-transformation-activities.md).</span></span> <span data-ttu-id="a8e3b-145">Neste tutorial, pode criar um pipeline com uma atividade (atividade do Hive).</span><span class="sxs-lookup"><span data-stu-id="a8e3b-145">In this tutorial, you create a pipeline with one activity (Hive activity).</span></span>

<span data-ttu-id="a8e3b-146">Olá seguinte secção fornece modelo de Gestor de recursos completo Olá para definir as entidades do Data Factory para que pode percorrer Olá tutorial e teste Olá modelo rapidamente.</span><span class="sxs-lookup"><span data-stu-id="a8e3b-146">hello following section provides hello complete Resource Manager template for defining Data Factory entities so that you can quickly run through hello tutorial and test hello template.</span></span> <span data-ttu-id="a8e3b-147">toounderstand a cada entidade de fábrica de dados estiver definida, consulte [entidades do Data Factory no modelo de Olá](#data-factory-entities-in-the-template) secção.</span><span class="sxs-lookup"><span data-stu-id="a8e3b-147">toounderstand how each Data Factory entity is defined, see [Data Factory entities in hello template](#data-factory-entities-in-the-template) section.</span></span>

## <a name="data-factory-json-template"></a><span data-ttu-id="a8e3b-148">Modelo JSON do Data Factory</span><span class="sxs-lookup"><span data-stu-id="a8e3b-148">Data Factory JSON template</span></span>
<span data-ttu-id="a8e3b-149">modelo do Resource Manager de nível superior do Olá para definir uma fábrica de dados é:</span><span class="sxs-lookup"><span data-stu-id="a8e3b-149">hello top-level Resource Manager template for defining a data factory is:</span></span> 

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
<span data-ttu-id="a8e3b-150">Crie um ficheiro JSON com o nome **adftutorialarm. JSON** no **C:\ADFGetStarted** pasta com Olá seguinte conteúdo:</span><span class="sxs-lookup"><span data-stu-id="a8e3b-150">Create a JSON file named **ADFTutorialARM.json** in **C:\ADFGetStarted** folder with hello following content:</span></span>

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
> <span data-ttu-id="a8e3b-151">Pode encontrar outro exemplo do modelo do Resource Manager para criar uma fábrica de dados do Azure no [Tutorial: criar um pipeline com a Atividade de Cópia utilizando um modelo do Azure Resource Manager](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md).</span><span class="sxs-lookup"><span data-stu-id="a8e3b-151">You can find another example of Resource Manager template for creating an Azure data factory on [Tutorial: Create a pipeline with Copy Activity using an Azure Resource Manager template](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md).</span></span>  
> 
> 

## <a name="parameters-json"></a><span data-ttu-id="a8e3b-152">Parâmetros JSON</span><span class="sxs-lookup"><span data-stu-id="a8e3b-152">Parameters JSON</span></span>
<span data-ttu-id="a8e3b-153">Crie um ficheiro JSON com o nome **ADFTutorialARM-Parameters. JSON** que contém os parâmetros de modelo do Azure Resource Manager Olá.</span><span class="sxs-lookup"><span data-stu-id="a8e3b-153">Create a JSON file named **ADFTutorialARM-Parameters.json** that contains parameters for hello Azure Resource Manager template.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="a8e3b-154">Especifique o nome de Olá e a chave da sua conta do Storage do Azure para Olá **storageAccountName** e **storageAccountKey** parâmetros neste ficheiro de parâmetros.</span><span class="sxs-lookup"><span data-stu-id="a8e3b-154">Specify hello name and key of your Azure Storage account for hello **storageAccountName** and **storageAccountKey** parameters in this parameter file.</span></span> 
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
> <span data-ttu-id="a8e3b-155">Pode ter ficheiros JSON do parâmetro separado para o desenvolvimento, teste e ambientes de produção que pode utilizar com Olá mesmo modelo JSON de fábrica de dados.</span><span class="sxs-lookup"><span data-stu-id="a8e3b-155">You may have separate parameter JSON files for development, testing, and production environments that you can use with hello same Data Factory JSON template.</span></span> <span data-ttu-id="a8e3b-156">Ao utilizar um script do Power Shell, pode automatizar a implementação de entidades do Data Factory nestes ambientes.</span><span class="sxs-lookup"><span data-stu-id="a8e3b-156">By using a Power Shell script, you can automate deploying Data Factory entities in these environments.</span></span> 
> 
> 

## <a name="create-data-factory"></a><span data-ttu-id="a8e3b-157">Criar fábrica de dados</span><span class="sxs-lookup"><span data-stu-id="a8e3b-157">Create data factory</span></span>
1. <span data-ttu-id="a8e3b-158">Iniciar **Azure PowerShell** e Olá execute os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="a8e3b-158">Start **Azure PowerShell** and run hello following command:</span></span> 
   * <span data-ttu-id="a8e3b-159">Execute Olá os seguintes comandos e introduza o nome de utilizador de Olá e a palavra-passe que utilizam toosign no toohello portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="a8e3b-159">Run hello following command and enter hello user name and password that you use toosign in toohello Azure portal.</span></span>
    ```PowerShell
    Login-AzureRmAccount
    ```  
   * <span data-ttu-id="a8e3b-160">Execute Olá tooview de comando a seguir todas as subscrições de Olá para esta conta.</span><span class="sxs-lookup"><span data-stu-id="a8e3b-160">Run hello following command tooview all hello subscriptions for this account.</span></span>
    ```PowerShell
    Get-AzureRmSubscription
    ``` 
   * <span data-ttu-id="a8e3b-161">Execute Olá comando tooselect Olá subscrição que pretende que toowork com os seguintes.</span><span class="sxs-lookup"><span data-stu-id="a8e3b-161">Run hello following command tooselect hello subscription that you want toowork with.</span></span> <span data-ttu-id="a8e3b-162">Esta subscrição deve ser Olá igual à Olá utilizada no Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="a8e3b-162">This subscription should be hello same as hello one you used in hello Azure portal.</span></span>
    ```
    Get-AzureRmSubscription -SubscriptionName <SUBSCRIPTION NAME> | Set-AzureRmContext
    ```   
2. <span data-ttu-id="a8e3b-163">Execute Olá seguintes entidades do Data Factory comando toodeploy utilizando o modelo do Resource Manager Olá que criou no passo 1.</span><span class="sxs-lookup"><span data-stu-id="a8e3b-163">Run hello following command toodeploy Data Factory entities using hello Resource Manager template you created in Step 1.</span></span> 

    ```PowerShell
    New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile C:\ADFGetStarted\ADFTutorialARM.json -TemplateParameterFile C:\ADFGetStarted\ADFTutorialARM-Parameters.json
    ```

## <a name="monitor-pipeline"></a><span data-ttu-id="a8e3b-164">Monitorizar o pipeline</span><span class="sxs-lookup"><span data-stu-id="a8e3b-164">Monitor pipeline</span></span>
1. <span data-ttu-id="a8e3b-165">Após iniciar sessão toohello [portal do Azure](https://portal.azure.com/), clique em **procurar** e selecione **fábricas de dados**.</span><span class="sxs-lookup"><span data-stu-id="a8e3b-165">After logging in toohello [Azure portal](https://portal.azure.com/), Click **Browse** and select **Data factories**.</span></span>
     <span data-ttu-id="a8e3b-166">![Procurar->Fábricas de dados](./media/data-factory-build-your-first-pipeline-using-arm/BrowseDataFactories.png)</span><span class="sxs-lookup"><span data-stu-id="a8e3b-166">![Browse->Data factories](./media/data-factory-build-your-first-pipeline-using-arm/BrowseDataFactories.png)</span></span>
2. <span data-ttu-id="a8e3b-167">No Olá **fábricas de dados** painel, clique em fábrica de dados de Olá (**TutorialFactoryARM**) que criou.</span><span class="sxs-lookup"><span data-stu-id="a8e3b-167">In hello **Data Factories** blade, click hello data factory (**TutorialFactoryARM**) you created.</span></span>    
3. <span data-ttu-id="a8e3b-168">No Olá **Data Factory** painel para a fábrica de dados, clique em **diagrama**.</span><span class="sxs-lookup"><span data-stu-id="a8e3b-168">In hello **Data Factory** blade for your data factory, click **Diagram**.</span></span>

     ![Mosaico do Diagrama](./media/data-factory-build-your-first-pipeline-using-arm/DiagramTile.png)
4. <span data-ttu-id="a8e3b-170">No Olá **vista de diagrama**, verá uma descrição geral dos pipelines Olá e conjuntos de dados utilizado neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="a8e3b-170">In hello **Diagram View**, you see an overview of hello pipelines, and datasets used in this tutorial.</span></span>
   
   ![Vista de Diagrama](./media/data-factory-build-your-first-pipeline-using-arm/DiagramView.png) 
5. <span data-ttu-id="a8e3b-172">Na vista de diagrama Olá, faça duplo clique em dataset Olá **AzureBlobOutput**.</span><span class="sxs-lookup"><span data-stu-id="a8e3b-172">In hello Diagram View, double-click hello dataset **AzureBlobOutput**.</span></span> <span data-ttu-id="a8e3b-173">Verá o setor que Olá que está atualmente a ser processado.</span><span class="sxs-lookup"><span data-stu-id="a8e3b-173">You see that hello slice that is currently being processed.</span></span>
   
    ![Conjunto de dados](./media/data-factory-build-your-first-pipeline-using-arm/AzureBlobOutput.png)
6. <span data-ttu-id="a8e3b-175">Quando o processamento terminar, verá o setor de Olá no **pronto** estado.</span><span class="sxs-lookup"><span data-stu-id="a8e3b-175">When processing is done, you see hello slice in **Ready** state.</span></span> <span data-ttu-id="a8e3b-176">A criação de um cluster do HDInsight a pedido demora, por norma, algum tempo (cerca de 20 minutos).</span><span class="sxs-lookup"><span data-stu-id="a8e3b-176">Creation of an on-demand HDInsight cluster usually takes sometime (approximately 20 minutes).</span></span> <span data-ttu-id="a8e3b-177">Por conseguinte, esperar Olá pipeline tootake **aproximadamente 30 minutos** tooprocess Olá setor.</span><span class="sxs-lookup"><span data-stu-id="a8e3b-177">Therefore, expect hello pipeline tootake **approximately 30 minutes** tooprocess hello slice.</span></span>
   
    ![Conjunto de dados](./media/data-factory-build-your-first-pipeline-using-arm/SliceReady.png)    
7. <span data-ttu-id="a8e3b-179">Quando Olá setor estiver no **pronto** de estado, verifique Olá **partitioneddata** pasta Olá **adfgetstarted** dados de saída do contentor de armazenamento de BLOBs para Olá.</span><span class="sxs-lookup"><span data-stu-id="a8e3b-179">When hello slice is in **Ready** state, check hello **partitioneddata** folder in hello **adfgetstarted** container in your blob storage for hello output data.</span></span>  

<span data-ttu-id="a8e3b-180">Consulte [monitorizar os conjuntos de dados e pipeline](data-factory-monitor-manage-pipelines.md) para obter instruções sobre como o pipeline de Olá do toouse Olá os painéis do portal do Azure toomonitor e conjuntos de dados que criou neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="a8e3b-180">See [Monitor datasets and pipeline](data-factory-monitor-manage-pipelines.md) for instructions on how toouse hello Azure portal blades toomonitor hello pipeline and datasets you have created in this tutorial.</span></span>

<span data-ttu-id="a8e3b-181">Também pode utilizar toomonitor monitorizar e gerir aplicações seus pipelines de dados.</span><span class="sxs-lookup"><span data-stu-id="a8e3b-181">You can also use Monitor and Manage App toomonitor your data pipelines.</span></span> <span data-ttu-id="a8e3b-182">Consulte [monitorizar e gerir pipelines do Azure Data Factory com a aplicação de monitorização](data-factory-monitor-manage-app.md) para obter detalhes sobre como utilizar a aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="a8e3b-182">See [Monitor and manage Azure Data Factory pipelines using Monitoring App](data-factory-monitor-manage-app.md) for details about using hello application.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="a8e3b-183">ficheiro de entrada Olá é eliminado quando o setor de Olá é processado com êxito.</span><span class="sxs-lookup"><span data-stu-id="a8e3b-183">hello input file gets deleted when hello slice is processed successfully.</span></span> <span data-ttu-id="a8e3b-184">Por conseguinte, se pretender setor de Olá toorerun ou Olá novamente o tutorial, carregue Olá ficheiro de entrada (input.log) toohello na pasta inputdata do contentor adfgetstarted de Olá.</span><span class="sxs-lookup"><span data-stu-id="a8e3b-184">Therefore, if you want toorerun hello slice or do hello tutorial again, upload hello input file (input.log) toohello inputdata folder of hello adfgetstarted container.</span></span>
> 
> 

## <a name="data-factory-entities-in-hello-template"></a><span data-ttu-id="a8e3b-185">Entidades da fábrica de dados no modelo de Olá</span><span class="sxs-lookup"><span data-stu-id="a8e3b-185">Data Factory entities in hello template</span></span>
### <a name="define-data-factory"></a><span data-ttu-id="a8e3b-186">Definir fábrica de dados</span><span class="sxs-lookup"><span data-stu-id="a8e3b-186">Define data factory</span></span>
<span data-ttu-id="a8e3b-187">Definir uma fábrica de dados no modelo do Resource Manager Olá, conforme mostrado no seguinte exemplo de Olá:</span><span class="sxs-lookup"><span data-stu-id="a8e3b-187">You define a data factory in hello Resource Manager template as shown in hello following sample:</span></span>  

```json
"resources": [
{
    "name": "[variables('dataFactoryName')]",
    "apiVersion": "2015-10-01",
    "type": "Microsoft.DataFactory/datafactories",
    "location": "West US"
}
```
<span data-ttu-id="a8e3b-188">Olá dataFactoryName está definida como:</span><span class="sxs-lookup"><span data-stu-id="a8e3b-188">hello dataFactoryName is defined as:</span></span> 

```json
"dataFactoryName": "[concat('HiveTransformDF', uniqueString(resourceGroup().id))]",
```
<span data-ttu-id="a8e3b-189">É uma cadeia exclusiva com base no ID de grupo de recursos para Olá.</span><span class="sxs-lookup"><span data-stu-id="a8e3b-189">It is a unique string based on hello resource group ID.</span></span>  

### <a name="defining-data-factory-entities"></a><span data-ttu-id="a8e3b-190">Definir entidades do Data Factory</span><span class="sxs-lookup"><span data-stu-id="a8e3b-190">Defining Data Factory entities</span></span>
<span data-ttu-id="a8e3b-191">Olá seguintes entidades do Data Factory estão definidas no modelo JSON Olá:</span><span class="sxs-lookup"><span data-stu-id="a8e3b-191">hello following Data Factory entities are defined in hello JSON template:</span></span> 

* [<span data-ttu-id="a8e3b-192">Serviço ligado do Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="a8e3b-192">Azure Storage linked service</span></span>](#azure-storage-linked-service)
* [<span data-ttu-id="a8e3b-193">Serviço ligado do HDInsight a pedido</span><span class="sxs-lookup"><span data-stu-id="a8e3b-193">HDInsight on-demand linked service</span></span>](#hdinsight-on-demand-linked-service)
* [<span data-ttu-id="a8e3b-194">Conjunto de dados de entrada do blobs do Azure</span><span class="sxs-lookup"><span data-stu-id="a8e3b-194">Azure blob input dataset</span></span>](#azure-blob-input-dataset)
* [<span data-ttu-id="a8e3b-195">Conjunto de dados de saída do blob do Azure</span><span class="sxs-lookup"><span data-stu-id="a8e3b-195">Azure blob output dataset</span></span>](#azure-blob-output-dataset)
* [<span data-ttu-id="a8e3b-196">Pipeline de dados com uma atividade de cópia</span><span class="sxs-lookup"><span data-stu-id="a8e3b-196">Data pipeline with a copy activity</span></span>](#data-pipeline)

#### <a name="azure-storage-linked-service"></a><span data-ttu-id="a8e3b-197">Serviço ligado do Storage do Azure</span><span class="sxs-lookup"><span data-stu-id="a8e3b-197">Azure Storage linked service</span></span>
<span data-ttu-id="a8e3b-198">Especifique o nome de Olá e a chave da sua conta de armazenamento do Azure nesta secção.</span><span class="sxs-lookup"><span data-stu-id="a8e3b-198">You specify hello name and key of your Azure storage account in this section.</span></span> <span data-ttu-id="a8e3b-199">Consulte [serviço ligado do Storage do Azure](data-factory-azure-blob-connector.md#azure-storage-linked-service) para obter detalhes sobre JSON as propriedades utilizadas toodefine um Azure serviço ligado do Storage.</span><span class="sxs-lookup"><span data-stu-id="a8e3b-199">See [Azure Storage linked service](data-factory-azure-blob-connector.md#azure-storage-linked-service) for details about JSON properties used toodefine an Azure Storage linked service.</span></span> 

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
<span data-ttu-id="a8e3b-200">Olá **connectionString** utiliza Olá storageAccountName e storageAccountKey parâmetros.</span><span class="sxs-lookup"><span data-stu-id="a8e3b-200">hello **connectionString** uses hello storageAccountName and storageAccountKey parameters.</span></span> <span data-ttu-id="a8e3b-201">Olá os valores para estes parâmetros transmitidos através da utilização de um ficheiro de configuração.</span><span class="sxs-lookup"><span data-stu-id="a8e3b-201">hello values for these parameters passed by using a configuration file.</span></span> <span data-ttu-id="a8e3b-202">definição de Olá também utiliza as variáveis: azureStroageLinkedService e dataFactoryName definido no modelo de Olá.</span><span class="sxs-lookup"><span data-stu-id="a8e3b-202">hello definition also uses variables: azureStroageLinkedService and dataFactoryName defined in hello template.</span></span> 

#### <a name="hdinsight-on-demand-linked-service"></a><span data-ttu-id="a8e3b-203">Serviço ligado do HDInsight a pedido</span><span class="sxs-lookup"><span data-stu-id="a8e3b-203">HDInsight on-demand linked service</span></span>
<span data-ttu-id="a8e3b-204">Consulte [serviços ligados de computação](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) artigo para obter detalhes sobre JSON as propriedades utilizadas toodefine um serviço ligado do HDInsight a pedido.</span><span class="sxs-lookup"><span data-stu-id="a8e3b-204">See [Compute linked services](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) article for details about JSON properties used toodefine an HDInsight on-demand linked service.</span></span>  

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
<span data-ttu-id="a8e3b-205">Tenha em atenção Olá seguintes pontos:</span><span class="sxs-lookup"><span data-stu-id="a8e3b-205">Note hello following points:</span></span> 

* <span data-ttu-id="a8e3b-206">Olá Data Factory cria um **baseado em Linux** cluster do HDInsight com Olá acima JSON.</span><span class="sxs-lookup"><span data-stu-id="a8e3b-206">hello Data Factory creates a **Linux-based** HDInsight cluster for you with hello above JSON.</span></span> <span data-ttu-id="a8e3b-207">Veja [On-demand HDInsight Linked Service (Serviço Ligado do HDInsight a Pedido)](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="a8e3b-207">See [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span></span> 
* <span data-ttu-id="a8e3b-208">Também pode utilizar o **seu próprio cluster do HDInsight** em vez de utilizar um cluster do HDInsight a pedido.</span><span class="sxs-lookup"><span data-stu-id="a8e3b-208">You could use **your own HDInsight cluster** instead of using an on-demand HDInsight cluster.</span></span> <span data-ttu-id="a8e3b-209">Veja [HDInsight Linked Service (Serviço Ligado do HDInsight)](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="a8e3b-209">See [HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) for details.</span></span>
* <span data-ttu-id="a8e3b-210">cluster do HDInsight Olá cria um **contentor predefinido** no armazenamento de BLOBs de Olá especificado na Olá JSON (**linkedServiceName**).</span><span class="sxs-lookup"><span data-stu-id="a8e3b-210">hello HDInsight cluster creates a **default container** in hello blob storage you specified in hello JSON (**linkedServiceName**).</span></span> <span data-ttu-id="a8e3b-211">HDInsight não é eliminado deste contentor quando cluster Olá é eliminado.</span><span class="sxs-lookup"><span data-stu-id="a8e3b-211">HDInsight does not delete this container when hello cluster is deleted.</span></span> <span data-ttu-id="a8e3b-212">Este comportamento é propositado.</span><span class="sxs-lookup"><span data-stu-id="a8e3b-212">This behavior is by design.</span></span> <span data-ttu-id="a8e3b-213">Com o serviço de ligado de HDInsight a pedido, é criado um cluster de HDInsight sempre que um setor tiver toobe processado, exceto se houver um cluster existente em direto (**timeToLive**) e é eliminado quando o processamento de Olá terminar.</span><span class="sxs-lookup"><span data-stu-id="a8e3b-213">With on-demand HDInsight linked service, a HDInsight cluster is created every time a slice needs toobe processed unless there is an existing live cluster (**timeToLive**) and is deleted when hello processing is done.</span></span>
  
    <span data-ttu-id="a8e3b-214">À medida que são processados mais setores, verá muitos contentores no armazenamento de blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="a8e3b-214">As more slices are processed, you see many containers in your Azure blob storage.</span></span> <span data-ttu-id="a8e3b-215">Se não precisar deles para resolução de problemas de tarefas Olá, poderá ser útil toodelete-los armazenamento de Olá tooreduce custo.</span><span class="sxs-lookup"><span data-stu-id="a8e3b-215">If you do not need them for troubleshooting of hello jobs, you may want toodelete them tooreduce hello storage cost.</span></span> <span data-ttu-id="a8e3b-216">os nomes de Olá destes contentores seguem um padrão: "adf**nomedafábricadedados**-**linkedservicename**- datetimestamp".</span><span class="sxs-lookup"><span data-stu-id="a8e3b-216">hello names of these containers follow a pattern: "adf**yourdatafactoryname**-**linkedservicename**-datetimestamp".</span></span> <span data-ttu-id="a8e3b-217">Utilize ferramentas como [Explorador de armazenamento do Microsoft](http://storageexplorer.com/) toodelete contentores no seu Azure armazenamento de Blobs.</span><span class="sxs-lookup"><span data-stu-id="a8e3b-217">Use tools such as [Microsoft Storage Explorer](http://storageexplorer.com/) toodelete containers in your Azure blob storage.</span></span>

<span data-ttu-id="a8e3b-218">Veja [On-demand HDInsight Linked Service (Serviço Ligado do HDInsight a Pedido)](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="a8e3b-218">See [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span></span>

#### <a name="azure-blob-input-dataset"></a><span data-ttu-id="a8e3b-219">Conjunto de dados de entrada de blobs do Azure</span><span class="sxs-lookup"><span data-stu-id="a8e3b-219">Azure blob input dataset</span></span>
<span data-ttu-id="a8e3b-220">Especifique nomes de Olá do contentor de blob, pasta e ficheiro que contém dados de entrada Olá.</span><span class="sxs-lookup"><span data-stu-id="a8e3b-220">You specify hello names of blob container, folder, and file that contains hello input data.</span></span> <span data-ttu-id="a8e3b-221">Consulte [propriedades do conjunto de dados de Blobs do Azure](data-factory-azure-blob-connector.md#dataset-properties) para obter detalhes sobre as propriedades utilizadas de JSON toodefine um conjunto de dados de Blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="a8e3b-221">See [Azure Blob dataset properties](data-factory-azure-blob-connector.md#dataset-properties) for details about JSON properties used toodefine an Azure Blob dataset.</span></span> 

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
<span data-ttu-id="a8e3b-222">Esta definição utiliza os seguintes parâmetros definidos no modelo de parâmetro de Olá: blobContainer, inputBlobFolder e inputBlobName.</span><span class="sxs-lookup"><span data-stu-id="a8e3b-222">This definition uses hello following parameters defined in parameter template: blobContainer, inputBlobFolder, and inputBlobName.</span></span> 

#### <a name="azure-blob-output-dataset"></a><span data-ttu-id="a8e3b-223">Conjunto de dados de saída do Blob do Azure</span><span class="sxs-lookup"><span data-stu-id="a8e3b-223">Azure Blob output dataset</span></span>
<span data-ttu-id="a8e3b-224">Especifique nomes de Olá da pasta que contém dados de saída Olá e contentor de blob.</span><span class="sxs-lookup"><span data-stu-id="a8e3b-224">You specify hello names of blob container and folder that holds hello output data.</span></span> <span data-ttu-id="a8e3b-225">Consulte [propriedades do conjunto de dados de Blobs do Azure](data-factory-azure-blob-connector.md#dataset-properties) para obter detalhes sobre as propriedades utilizadas de JSON toodefine um conjunto de dados de Blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="a8e3b-225">See [Azure Blob dataset properties](data-factory-azure-blob-connector.md#dataset-properties) for details about JSON properties used toodefine an Azure Blob dataset.</span></span>  

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

<span data-ttu-id="a8e3b-226">Esta definição utiliza Olá seguir os parâmetros definidos no modelo de parâmetro de Olá: blobContainer e outputBlobFolder.</span><span class="sxs-lookup"><span data-stu-id="a8e3b-226">This definition uses hello following parameters defined in hello parameter template: blobContainer and outputBlobFolder.</span></span> 

#### <a name="data-pipeline"></a><span data-ttu-id="a8e3b-227">Pipeline de dados</span><span class="sxs-lookup"><span data-stu-id="a8e3b-227">Data pipeline</span></span>
<span data-ttu-id="a8e3b-228">Defina um pipeline que transforme dados executando o script de ramo de registo num cluster HDInsight a pedido do Azure.</span><span class="sxs-lookup"><span data-stu-id="a8e3b-228">You define a pipeline that transform data by running Hive script on an on-demand Azure HDInsight cluster.</span></span> <span data-ttu-id="a8e3b-229">Consulte [JSON do Pipeline](data-factory-create-pipelines.md#pipeline-json) para obter descrições JSON elementos utilizados toodefine um pipeline neste exemplo.</span><span class="sxs-lookup"><span data-stu-id="a8e3b-229">See [Pipeline JSON](data-factory-create-pipelines.md#pipeline-json) for descriptions of JSON elements used toodefine a pipeline in this example.</span></span> 

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

## <a name="reuse-hello-template"></a><span data-ttu-id="a8e3b-230">Reutilizar o modelo de Olá</span><span class="sxs-lookup"><span data-stu-id="a8e3b-230">Reuse hello template</span></span>
<span data-ttu-id="a8e3b-231">Olá tutorial, vai criar um modelo para definir entidades do Data Factory e um modelo para passar os valores de parâmetros.</span><span class="sxs-lookup"><span data-stu-id="a8e3b-231">In hello tutorial, you created a template for defining Data Factory entities and a template for passing values for parameters.</span></span> <span data-ttu-id="a8e3b-232">toouse Olá mesmos modelo toodeploy Data Factory entidades toodifferent ambientes, crie um ficheiro de parâmetro para cada ambiente e utilizá-lo quando implementar toothat ambiente.</span><span class="sxs-lookup"><span data-stu-id="a8e3b-232">toouse hello same template toodeploy Data Factory entities toodifferent environments, you create a parameter file for each environment and use it when deploying toothat environment.</span></span>     

<span data-ttu-id="a8e3b-233">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="a8e3b-233">Example:</span></span>  

```PowerShell
New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFTutorialARM.json -TemplateParameterFile ADFTutorialARM-Parameters-Dev.json

New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFTutorialARM.json -TemplateParameterFile ADFTutorialARM-Parameters-Test.json

New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFTutorialARM.json -TemplateParameterFile ADFTutorialARM-Parameters-Production.json
```
<span data-ttu-id="a8e3b-234">Tenha em atenção que Olá primeiro parâmetro do comando utiliza o ficheiro para o ambiente de desenvolvimento de Olá, um segundo para o ambiente de teste de Olá e Olá uma terceira para ambiente de produção Olá.</span><span class="sxs-lookup"><span data-stu-id="a8e3b-234">Notice that hello first command uses parameter file for hello development environment, second one for hello test environment, and hello third one for hello production environment.</span></span>  

<span data-ttu-id="a8e3b-235">Também pode reutilizar Olá modelo tooperform repetido tarefas.</span><span class="sxs-lookup"><span data-stu-id="a8e3b-235">You can also reuse hello template tooperform repeated tasks.</span></span> <span data-ttu-id="a8e3b-236">Por exemplo, terá de toocreate várias fábricas de dados com um ou mais pipelines que implementam Olá mesma lógica, mas cada data factory utiliza diferentes storage do Azure e contas de SQL Database do Azure.</span><span class="sxs-lookup"><span data-stu-id="a8e3b-236">For example, you need toocreate many data factories with one or more pipelines that implement hello same logic but each data factory uses different Azure storage and Azure SQL Database accounts.</span></span> <span data-ttu-id="a8e3b-237">Neste cenário, utilize Olá mesmo modelo no Olá mesmo ambiente (desenvolvimento, teste ou de produção) com o parâmetro diferentes ficheiros toocreate fábricas de dados.</span><span class="sxs-lookup"><span data-stu-id="a8e3b-237">In this scenario, you use hello same template in hello same environment (dev, test, or production) with different parameter files toocreate data factories.</span></span> 

## <a name="resource-manager-template-for-creating-a-gateway"></a><span data-ttu-id="a8e3b-238">Modelo do Resource Manager para criar um gateway</span><span class="sxs-lookup"><span data-stu-id="a8e3b-238">Resource Manager template for creating a gateway</span></span>
<span data-ttu-id="a8e3b-239">Segue-se um modelo de Gestor de recursos de exemplo para criar um gateway lógico no Olá novamente.</span><span class="sxs-lookup"><span data-stu-id="a8e3b-239">Here is a sample Resource Manager template for creating a logical gateway in hello back.</span></span> <span data-ttu-id="a8e3b-240">Instalar um gateway no computador local ou VM do IaaS do Azure e registar o gateway de Olá com o serviço Data Factory com uma chave.</span><span class="sxs-lookup"><span data-stu-id="a8e3b-240">Install a gateway on your on-premises computer or Azure IaaS VM and register hello gateway with Data Factory service using a key.</span></span> <span data-ttu-id="a8e3b-241">Veja [Move data between on-premises and cloud (Mover dados entre o local e a nuvem)](data-factory-move-data-between-onprem-and-cloud.md) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="a8e3b-241">See [Move data between on-premises and cloud](data-factory-move-data-between-onprem-and-cloud.md) for details.</span></span>

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
<span data-ttu-id="a8e3b-242">Este modelo cria uma fábrica de dados com o nome GatewayUsingArmDF com um gateway designado: GatewayUsingARM.</span><span class="sxs-lookup"><span data-stu-id="a8e3b-242">This template creates a data factory named GatewayUsingArmDF with a gateway named: GatewayUsingARM.</span></span> 

## <a name="see-also"></a><span data-ttu-id="a8e3b-243">Veja também</span><span class="sxs-lookup"><span data-stu-id="a8e3b-243">See Also</span></span>
| <span data-ttu-id="a8e3b-244">Tópico</span><span class="sxs-lookup"><span data-stu-id="a8e3b-244">Topic</span></span> | <span data-ttu-id="a8e3b-245">Descrição</span><span class="sxs-lookup"><span data-stu-id="a8e3b-245">Description</span></span> |
|:--- |:--- |
| [<span data-ttu-id="a8e3b-246">Pipelines</span><span class="sxs-lookup"><span data-stu-id="a8e3b-246">Pipelines</span></span>](data-factory-create-pipelines.md) |<span data-ttu-id="a8e3b-247">Este artigo ajuda-o a compreender os pipelines e atividades no Azure Data Factory e como toouse-los tooconstruct ponto a ponto condicionados por dados fluxos de trabalho para o seu cenário ou empresa.</span><span class="sxs-lookup"><span data-stu-id="a8e3b-247">This article helps you understand pipelines and activities in Azure Data Factory and how toouse them tooconstruct end-to-end data-driven workflows for your scenario or business.</span></span> |
| [<span data-ttu-id="a8e3b-248">Conjuntos de dados</span><span class="sxs-lookup"><span data-stu-id="a8e3b-248">Datasets</span></span>](data-factory-create-datasets.md) |<span data-ttu-id="a8e3b-249">Este artigo ajuda-o a compreender os conjuntos de dados no Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="a8e3b-249">This article helps you understand datasets in Azure Data Factory.</span></span> |
| [<span data-ttu-id="a8e3b-250">Agendamento e execução</span><span class="sxs-lookup"><span data-stu-id="a8e3b-250">Scheduling and execution</span></span>](data-factory-scheduling-and-execution.md) |<span data-ttu-id="a8e3b-251">Este artigo explica os aspetos de agendamento e execução de Olá do modelo de aplicação do Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="a8e3b-251">This article explains hello scheduling and execution aspects of Azure Data Factory application model.</span></span> |
| [<span data-ttu-id="a8e3b-252">Monitorizar e gerir pipelines com a Aplicação de Monitorização</span><span class="sxs-lookup"><span data-stu-id="a8e3b-252">Monitor and manage pipelines using Monitoring App</span></span>](data-factory-monitor-manage-app.md) |<span data-ttu-id="a8e3b-253">Este artigo descreve como toomonitor, gerir e depurar pipelines utilizando Olá de monitorização e gestão de aplicações.</span><span class="sxs-lookup"><span data-stu-id="a8e3b-253">This article describes how toomonitor, manage, and debug pipelines using hello Monitoring & Management App.</span></span> |

