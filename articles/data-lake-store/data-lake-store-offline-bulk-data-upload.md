---
title: "grandes quantidades de aaaUpload dos dados no Data Lake Store utilizando métodos offline | Microsoft Docs"
description: "Olá utilizar dados de toocopy ferramenta AdlCopy do armazenamento do Azure blobs tooData Lake Store"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 45321f6a-179f-4ee4-b8aa-efa7745b8eb6
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 42ef75142a26ebfab05d89614782a54c244c4bcb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-azure-importexport-service-for-offline-copy-of-data-toodata-lake-store"></a><span data-ttu-id="4d2f7-103">Utilizar o serviço do Azure para importar/exportar Olá para cópia offline tooData Lake do arquivo de dados</span><span class="sxs-lookup"><span data-stu-id="4d2f7-103">Use hello Azure Import/Export service for offline copy of data tooData Lake Store</span></span>
<span data-ttu-id="4d2f7-104">Neste artigo, irá aprender como dados de grande toocopy define (> 200 GB) para um Azure Data Lake Store utilizando métodos de cópia offline, como Olá [serviço importar/exportar do Azure](../storage/common/storage-import-export-service.md).</span><span class="sxs-lookup"><span data-stu-id="4d2f7-104">In this article, you'll learn how toocopy huge data sets (>200 GB) into an Azure Data Lake Store by using offline copy methods, like hello [Azure Import/Export service](../storage/common/storage-import-export-service.md).</span></span> <span data-ttu-id="4d2f7-105">Especificamente, o ficheiro de Olá utilizado como exemplo neste artigo é 339,420,860,416 bytes ou cerca de 319 GB no disco.</span><span class="sxs-lookup"><span data-stu-id="4d2f7-105">Specifically, hello file used as an example in this article is 339,420,860,416 bytes, or about 319 GB on disk.</span></span> <span data-ttu-id="4d2f7-106">Vamos chamar 319GB.tsv este ficheiro.</span><span class="sxs-lookup"><span data-stu-id="4d2f7-106">Let's call this file 319GB.tsv.</span></span>

<span data-ttu-id="4d2f7-107">Olá serviço importar/exportar do Azure ajuda-o a tootransfer grandes quantidades de dados mais segura tooAzure armazenamento de BLOBs de disco rígido de envio de unidades tooan datacenter do Azure.</span><span class="sxs-lookup"><span data-stu-id="4d2f7-107">hello Azure Import/Export service helps you tootransfer large amounts of data more securely tooAzure Blob storage by shipping hard disk drives tooan Azure datacenter.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4d2f7-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="4d2f7-108">Prerequisites</span></span>
<span data-ttu-id="4d2f7-109">Antes de começar, tem de ter o seguinte Olá:</span><span class="sxs-lookup"><span data-stu-id="4d2f7-109">Before you begin, you must have hello following:</span></span>

* <span data-ttu-id="4d2f7-110">**Uma subscrição do Azure**.</span><span class="sxs-lookup"><span data-stu-id="4d2f7-110">**An Azure subscription**.</span></span> <span data-ttu-id="4d2f7-111">Consulte [Obter uma avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4d2f7-111">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="4d2f7-112">**Uma conta de armazenamento do Azure**.</span><span class="sxs-lookup"><span data-stu-id="4d2f7-112">**An Azure storage account**.</span></span>
* <span data-ttu-id="4d2f7-113">**Uma conta do Azure Data Lake Store**.</span><span class="sxs-lookup"><span data-stu-id="4d2f7-113">**An Azure Data Lake Store account**.</span></span> <span data-ttu-id="4d2f7-114">Para obter instruções sobre como um, ver toocreate [introdução ao Azure Data Lake Store](data-lake-store-get-started-portal.md)</span><span class="sxs-lookup"><span data-stu-id="4d2f7-114">For instructions on how toocreate one, see [Get started with Azure Data Lake Store](data-lake-store-get-started-portal.md)</span></span>

## <a name="preparing-hello-data"></a><span data-ttu-id="4d2f7-115">A preparar os dados de Olá</span><span class="sxs-lookup"><span data-stu-id="4d2f7-115">Preparing hello data</span></span>
<span data-ttu-id="4d2f7-116">Antes de utilizar o serviço de importação/exportação Olá, quebra Olá dados ficheiro toobe transferidos **em cópias são menos 200 GB** de tamanho.</span><span class="sxs-lookup"><span data-stu-id="4d2f7-116">Before using hello Import/Export service, break hello data file toobe transferred **into copies that are less than 200 GB** in size.</span></span> <span data-ttu-id="4d2f7-117">ferramenta de importação de Olá não funciona com ficheiros maiores do que 200 GB.</span><span class="sxs-lookup"><span data-stu-id="4d2f7-117">hello import tool does not work with files greater than 200 GB.</span></span> <span data-ttu-id="4d2f7-118">Neste tutorial, iremos dividir os ficheiros de Olá em segmentos de 100 GB cada.</span><span class="sxs-lookup"><span data-stu-id="4d2f7-118">In this tutorial, we split hello file into chunks of 100 GB each.</span></span> <span data-ttu-id="4d2f7-119">Pode fazê-lo utilizando [Cygwin](https://cygwin.com/install.html).</span><span class="sxs-lookup"><span data-stu-id="4d2f7-119">You can do this by using [Cygwin](https://cygwin.com/install.html).</span></span> <span data-ttu-id="4d2f7-120">Cygwin suporta comandos de Linux.</span><span class="sxs-lookup"><span data-stu-id="4d2f7-120">Cygwin supports Linux commands.</span></span> <span data-ttu-id="4d2f7-121">Neste caso, utilize Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="4d2f7-121">In this case, use hello following command:</span></span>

    split -b 100m 319GB.tsv

<span data-ttu-id="4d2f7-122">operação de divisão de Olá cria ficheiros com os seguintes nomes de Olá.</span><span class="sxs-lookup"><span data-stu-id="4d2f7-122">hello split operation creates files with hello following names.</span></span>

    319GB.tsv-part-aa

    319GB.tsv-part-ab

    319GB.tsv-part-ac

    319GB.tsv-part-ad

## <a name="get-disks-ready-with-data"></a><span data-ttu-id="4d2f7-123">Preparar os discos com os dados</span><span class="sxs-lookup"><span data-stu-id="4d2f7-123">Get disks ready with data</span></span>
<span data-ttu-id="4d2f7-124">Siga as instruções de Olá em [utilizando o serviço de importação/exportação do Azure Olá](../storage/common/storage-import-export-service.md) (em Olá **preparar as suas unidades** secção) tooprepare unidades de disco rígido.</span><span class="sxs-lookup"><span data-stu-id="4d2f7-124">Follow hello instructions in [Using hello Azure Import/Export service](../storage/common/storage-import-export-service.md) (under hello **Prepare your drives** section) tooprepare your hard drives.</span></span> <span data-ttu-id="4d2f7-125">Eis Olá sequência geral:</span><span class="sxs-lookup"><span data-stu-id="4d2f7-125">Here's hello overall sequence:</span></span>

1. <span data-ttu-id="4d2f7-126">Obter um disco rígido que cumpra Olá requisito toobe utilizado para Olá serviço importar/exportar do Azure.</span><span class="sxs-lookup"><span data-stu-id="4d2f7-126">Procure a hard disk that meets hello requirement toobe used for hello Azure Import/Export service.</span></span>
2. <span data-ttu-id="4d2f7-127">Identifique uma conta de armazenamento do Azure onde serão copiados os dados de Olá depois-é enviada toohello do datacenter do Azure.</span><span class="sxs-lookup"><span data-stu-id="4d2f7-127">Identify an Azure storage account where hello data will be copied after it is shipped toohello Azure datacenter.</span></span>
3. <span data-ttu-id="4d2f7-128">Olá utilize [ferramenta de importação/exportação do Azure](http://go.microsoft.com/fwlink/?LinkID=301900&clcid=0x409), um utilitário da linha de comandos.</span><span class="sxs-lookup"><span data-stu-id="4d2f7-128">Use hello [Azure Import/Export Tool](http://go.microsoft.com/fwlink/?LinkID=301900&clcid=0x409), a command-line utility.</span></span> <span data-ttu-id="4d2f7-129">Eis um fragmento de exemplo que mostra como toouse Olá ferramenta.</span><span class="sxs-lookup"><span data-stu-id="4d2f7-129">Here's a sample snippet that shows how toouse hello tool.</span></span>

    ````
    WAImportExport PrepImport /sk:<StorageAccountKey> /t: <TargetDriveLetter> /format /encrypt /logdir:e:\myexportimportjob\logdir /j:e:\myexportimportjob\journal1.jrn /id:myexportimportjob /srcdir:F:\demo\ExImContainer /dstdir:importcontainer/vf1/
    ````
    <span data-ttu-id="4d2f7-130">Consulte [utilizando o serviço de importação/exportação do Azure Olá](../storage/common/storage-import-export-service.md) para obter mais fragmentos de exemplo.</span><span class="sxs-lookup"><span data-stu-id="4d2f7-130">See [Using hello Azure Import/Export service](../storage/common/storage-import-export-service.md) for more sample snippets.</span></span>
4. <span data-ttu-id="4d2f7-131">Olá comando anterior cria um diário de alterações ficheiro Olá especificada a localização.</span><span class="sxs-lookup"><span data-stu-id="4d2f7-131">hello preceding command creates a journal file at hello specified location.</span></span> <span data-ttu-id="4d2f7-132">Utilize este toocreate de ficheiros do diário de alterações uma tarefa de importação de Olá [portal clássico do Azure](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="4d2f7-132">Use this journal file toocreate an import job from hello [Azure classic portal](https://manage.windowsazure.com).</span></span>

## <a name="create-an-import-job"></a><span data-ttu-id="4d2f7-133">Criar uma tarefa de importação</span><span class="sxs-lookup"><span data-stu-id="4d2f7-133">Create an import job</span></span>
<span data-ttu-id="4d2f7-134">Agora, pode criar uma tarefa de importação, utilizando instruções Olá [utilizando o serviço de importação/exportação do Azure Olá](../storage/common/storage-import-export-service.md) (em Olá **criar tarefa de importação de Olá** secção).</span><span class="sxs-lookup"><span data-stu-id="4d2f7-134">You can now create an import job by using hello instructions in [Using hello Azure Import/Export service](../storage/common/storage-import-export-service.md) (under hello **Create hello Import job** section).</span></span> <span data-ttu-id="4d2f7-135">Para esta tarefa de importação com outros detalhes também fornece Olá diário ficheiro criado durante a preparação Olá unidades de disco.</span><span class="sxs-lookup"><span data-stu-id="4d2f7-135">For this import job, with other details, also provide hello journal file created while preparing hello disk drives.</span></span>

## <a name="physically-ship-hello-disks"></a><span data-ttu-id="4d2f7-136">Fisicamente são enviados discos Olá</span><span class="sxs-lookup"><span data-stu-id="4d2f7-136">Physically ship hello disks</span></span>
<span data-ttu-id="4d2f7-137">Agora pode enviar fisicamente Olá discos tooan datacenter do Azure.</span><span class="sxs-lookup"><span data-stu-id="4d2f7-137">You can now physically ship hello disks tooan Azure datacenter.</span></span> <span data-ttu-id="4d2f7-138">Não existe, são copiados dados Olá toohello BLOBs de armazenamento do Azure que forneceu ao criar a tarefa de importação de Olá.</span><span class="sxs-lookup"><span data-stu-id="4d2f7-138">There, hello data is copied over toohello Azure Storage blobs you provided while creating hello import job.</span></span> <span data-ttu-id="4d2f7-139">Além disso, ao criar a tarefa de Olá, se tiver optado por Olá tooprovide mais tarde, as informações de controlo pode agora voltar atrás tooyour importar tarefa e atualização Olá controlo número.</span><span class="sxs-lookup"><span data-stu-id="4d2f7-139">Also, while creating hello job, if you opted tooprovide hello tracking information later, you can now go back tooyour import job and update hello tracking number.</span></span>

## <a name="copy-data-from-azure-storage-blobs-tooazure-data-lake-store"></a><span data-ttu-id="4d2f7-140">Copiar dados de armazenamento do Azure blobs tooAzure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="4d2f7-140">Copy data from Azure Storage blobs tooAzure Data Lake Store</span></span>
<span data-ttu-id="4d2f7-141">Depois de estado de Olá de Olá a tarefa de importação mostra que for concluído, pode verificar se os dados de Olá estão disponíveis em blobs de armazenamento do Azure Olá que tivesse especificado.</span><span class="sxs-lookup"><span data-stu-id="4d2f7-141">After hello status of hello import job shows that it's completed, you can verify whether hello data is available in hello Azure Storage blobs you had specified.</span></span> <span data-ttu-id="4d2f7-142">Em seguida, pode utilizar uma variedade de toomove métodos que os dados a partir de Olá blobs tooAzure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="4d2f7-142">You can then use a variety of methods toomove that data from hello blobs tooAzure Data Lake Store.</span></span> <span data-ttu-id="4d2f7-143">Para todos os hello as opções disponíveis para carregar dados, consulte [ingestão de dados no Data Lake Store](data-lake-store-data-scenarios.md#ingest-data-into-data-lake-store).</span><span class="sxs-lookup"><span data-stu-id="4d2f7-143">For all hello available options for uploading data, see [Ingesting data into Data Lake Store](data-lake-store-data-scenarios.md#ingest-data-into-data-lake-store).</span></span>

<span data-ttu-id="4d2f7-144">Nesta secção, iremos fornecer definições JSON de Olá que pode utilizar toocreate um pipeline do Azure Data Factory para copiar dados.</span><span class="sxs-lookup"><span data-stu-id="4d2f7-144">In this section, we provide you with hello JSON definitions that you can use toocreate an Azure Data Factory pipeline for copying data.</span></span> <span data-ttu-id="4d2f7-145">Pode utilizar estas definições JSON de Olá [portal do Azure](../data-factory/data-factory-copy-activity-tutorial-using-azure-portal.md), ou [Visual Studio](../data-factory/data-factory-copy-activity-tutorial-using-visual-studio.md), ou [Azure PowerShell](../data-factory/data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="4d2f7-145">You can use these JSON definitions from hello [Azure portal](../data-factory/data-factory-copy-activity-tutorial-using-azure-portal.md), or [Visual Studio](../data-factory/data-factory-copy-activity-tutorial-using-visual-studio.md), or [Azure PowerShell](../data-factory/data-factory-copy-activity-tutorial-using-powershell.md).</span></span>

### <a name="source-linked-service-azure-storage-blob"></a><span data-ttu-id="4d2f7-146">Serviço ligado de origem (blob Storage do Azure)</span><span class="sxs-lookup"><span data-stu-id="4d2f7-146">Source linked service (Azure Storage blob)</span></span>
````
{
    "name": "AzureStorageLinkedService",
    "properties": {
        "type": "AzureStorage",
        "description": "",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
        }
    }
}
````

### <a name="target-linked-service-azure-data-lake-store"></a><span data-ttu-id="4d2f7-147">Serviço ligado (Azure Data Lake Store) de destino</span><span class="sxs-lookup"><span data-stu-id="4d2f7-147">Target linked service (Azure Data Lake Store)</span></span>
````
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "description": "",
        "typeProperties": {
            "authorization": "<Click 'Authorize' tooallow this data factory and hello activities it runs tooaccess this Data Lake Store with your access rights>",
            "dataLakeStoreUri": "https://<adls_account_name>.azuredatalakestore.net/webhdfs/v1",
            "sessionId": "<OAuth session id from hello OAuth authorization session. Each session id is unique and may only be used once>"
        }
    }
}
````
### <a name="input-data-set"></a><span data-ttu-id="4d2f7-148">Conjunto de dados de entrada</span><span class="sxs-lookup"><span data-stu-id="4d2f7-148">Input data set</span></span>
````
{
    "name": "InputDataSet",
    "properties": {
        "published": false,
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "importcontainer/vf1/"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {}
    }
}
````
### <a name="output-data-set"></a><span data-ttu-id="4d2f7-149">Conjunto de dados de saída</span><span class="sxs-lookup"><span data-stu-id="4d2f7-149">Output data set</span></span>
````
{
"name": "OutputDataSet",
"properties": {
  "published": false,
  "type": "AzureDataLakeStore",
  "linkedServiceName": "AzureDataLakeStoreLinkedService",
  "typeProperties": {
    "folderPath": "/importeddatafeb8job/"
    },
  "availability": {
    "frequency": "Hour",
    "interval": 1
    }
  }
}
````
### <a name="pipeline-copy-activity"></a><span data-ttu-id="4d2f7-150">Pipeline (atividade de cópia)</span><span class="sxs-lookup"><span data-stu-id="4d2f7-150">Pipeline (copy activity)</span></span>
````
{
    "name": "CopyImportedData",
    "properties": {
        "description": "Pipeline with copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "BlobSource"
                    },
                    "sink": {
                        "type": "AzureDataLakeStoreSink",
                        "copyBehavior": "PreserveHierarchy",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "InputDataSet"
                    }
                ],
                "outputs": [
                    {
                        "name": "OutputDataSet"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1
                },
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "AzureBlobtoDataLake",
                "description": "Copy Activity"
            }
        ],
        "start": "2016-02-08T22:00:00Z",
        "end": "2016-02-08T23:00:00Z",
        "isPaused": false,
        "pipelineMode": "Scheduled"
    }
}
````
<span data-ttu-id="4d2f7-151">Para obter mais informações, consulte [mover dados de armazenamento do Azure blob tooAzure Data Lake Store utilizando o Azure Data Factory](../data-factory/data-factory-azure-datalake-connector.md).</span><span class="sxs-lookup"><span data-stu-id="4d2f7-151">For more information, see [Move data from Azure Storage blob tooAzure Data Lake Store using Azure Data Factory](../data-factory/data-factory-azure-datalake-connector.md).</span></span>

## <a name="reconstruct-hello-data-files-in-azure-data-lake-store"></a><span data-ttu-id="4d2f7-152">Reconstrua ficheiros de dados de Olá no Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="4d2f7-152">Reconstruct hello data files in Azure Data Lake Store</span></span>
<span data-ttu-id="4d2f7-153">Vamos começar a utilizar um ficheiro que foi 319 GB e quebrou-a para baixo para ficheiros de tamanho mais pequeno, de modo a que pode ser transferida através do serviço do Azure para importar/exportar Olá.</span><span class="sxs-lookup"><span data-stu-id="4d2f7-153">We started with a file that was 319 GB, and broke it down into files of smaller size so that it could be transferred by using hello Azure Import/Export service.</span></span> <span data-ttu-id="4d2f7-154">Agora que Olá dados no Azure Data Lake Store, iremos pode reconstrua Olá tooits original tamanho.</span><span class="sxs-lookup"><span data-stu-id="4d2f7-154">Now that hello data is in Azure Data Lake Store, we can reconstruct hello file tooits original size.</span></span> <span data-ttu-id="4d2f7-155">Pode utilizar Olá seguintes, por isso, o Azure PowerShell cmldts toodo.</span><span class="sxs-lookup"><span data-stu-id="4d2f7-155">You can use hello following Azure PowerShell cmldts toodo so.</span></span>

````
# Login tooour account
Login-AzureRmAccount

# List your subscriptions
Get-AzureRmSubscription

# Switch toohello subscription you want toowork with
Set-AzureRmContext –SubscriptionId
Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.DataLakeStore"

# Join  hello files
Join-AzureRmDataLakeStoreItem -AccountName "<adls_account_name" -Paths "/importeddatafeb8job/319GB.tsv-part-aa","/importeddatafeb8job/319GB.tsv-part-ab", "/importeddatafeb8job/319GB.tsv-part-ac", "/importeddatafeb8job/319GB.tsv-part-ad" -Destination "/importeddatafeb8job/MergedFile.csv”
````

## <a name="next-steps"></a><span data-ttu-id="4d2f7-156">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="4d2f7-156">Next steps</span></span>
* [<span data-ttu-id="4d2f7-157">Secure data in Data Lake Store (Proteger dados no Data Lake Store)</span><span class="sxs-lookup"><span data-stu-id="4d2f7-157">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)
* [<span data-ttu-id="4d2f7-158">Utilizar o Azure Data Lake Analytics com o Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="4d2f7-158">Use Azure Data Lake Analytics with Data Lake Store</span></span>](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="4d2f7-159">Use Azure HDInsight with Data Lake Store (Utilizar o Azure HDInsight com o Data Lake Store)</span><span class="sxs-lookup"><span data-stu-id="4d2f7-159">Use Azure HDInsight with Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)
