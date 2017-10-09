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
# <a name="use-hello-azure-importexport-service-for-offline-copy-of-data-toodata-lake-store"></a>Utilizar o serviço do Azure para importar/exportar Olá para cópia offline tooData Lake do arquivo de dados
Neste artigo, irá aprender como dados de grande toocopy define (> 200 GB) para um Azure Data Lake Store utilizando métodos de cópia offline, como Olá [serviço importar/exportar do Azure](../storage/common/storage-import-export-service.md). Especificamente, o ficheiro de Olá utilizado como exemplo neste artigo é 339,420,860,416 bytes ou cerca de 319 GB no disco. Vamos chamar 319GB.tsv este ficheiro.

Olá serviço importar/exportar do Azure ajuda-o a tootransfer grandes quantidades de dados mais segura tooAzure armazenamento de BLOBs de disco rígido de envio de unidades tooan datacenter do Azure.

## <a name="prerequisites"></a>Pré-requisitos
Antes de começar, tem de ter o seguinte Olá:

* **Uma subscrição do Azure**. Consulte [Obter uma avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/).
* **Uma conta de armazenamento do Azure**.
* **Uma conta do Azure Data Lake Store**. Para obter instruções sobre como um, ver toocreate [introdução ao Azure Data Lake Store](data-lake-store-get-started-portal.md)

## <a name="preparing-hello-data"></a>A preparar os dados de Olá
Antes de utilizar o serviço de importação/exportação Olá, quebra Olá dados ficheiro toobe transferidos **em cópias são menos 200 GB** de tamanho. ferramenta de importação de Olá não funciona com ficheiros maiores do que 200 GB. Neste tutorial, iremos dividir os ficheiros de Olá em segmentos de 100 GB cada. Pode fazê-lo utilizando [Cygwin](https://cygwin.com/install.html). Cygwin suporta comandos de Linux. Neste caso, utilize Olá os seguintes comandos:

    split -b 100m 319GB.tsv

operação de divisão de Olá cria ficheiros com os seguintes nomes de Olá.

    319GB.tsv-part-aa

    319GB.tsv-part-ab

    319GB.tsv-part-ac

    319GB.tsv-part-ad

## <a name="get-disks-ready-with-data"></a>Preparar os discos com os dados
Siga as instruções de Olá em [utilizando o serviço de importação/exportação do Azure Olá](../storage/common/storage-import-export-service.md) (em Olá **preparar as suas unidades** secção) tooprepare unidades de disco rígido. Eis Olá sequência geral:

1. Obter um disco rígido que cumpra Olá requisito toobe utilizado para Olá serviço importar/exportar do Azure.
2. Identifique uma conta de armazenamento do Azure onde serão copiados os dados de Olá depois-é enviada toohello do datacenter do Azure.
3. Olá utilize [ferramenta de importação/exportação do Azure](http://go.microsoft.com/fwlink/?LinkID=301900&clcid=0x409), um utilitário da linha de comandos. Eis um fragmento de exemplo que mostra como toouse Olá ferramenta.

    ````
    WAImportExport PrepImport /sk:<StorageAccountKey> /t: <TargetDriveLetter> /format /encrypt /logdir:e:\myexportimportjob\logdir /j:e:\myexportimportjob\journal1.jrn /id:myexportimportjob /srcdir:F:\demo\ExImContainer /dstdir:importcontainer/vf1/
    ````
    Consulte [utilizando o serviço de importação/exportação do Azure Olá](../storage/common/storage-import-export-service.md) para obter mais fragmentos de exemplo.
4. Olá comando anterior cria um diário de alterações ficheiro Olá especificada a localização. Utilize este toocreate de ficheiros do diário de alterações uma tarefa de importação de Olá [portal clássico do Azure](https://manage.windowsazure.com).

## <a name="create-an-import-job"></a>Criar uma tarefa de importação
Agora, pode criar uma tarefa de importação, utilizando instruções Olá [utilizando o serviço de importação/exportação do Azure Olá](../storage/common/storage-import-export-service.md) (em Olá **criar tarefa de importação de Olá** secção). Para esta tarefa de importação com outros detalhes também fornece Olá diário ficheiro criado durante a preparação Olá unidades de disco.

## <a name="physically-ship-hello-disks"></a>Fisicamente são enviados discos Olá
Agora pode enviar fisicamente Olá discos tooan datacenter do Azure. Não existe, são copiados dados Olá toohello BLOBs de armazenamento do Azure que forneceu ao criar a tarefa de importação de Olá. Além disso, ao criar a tarefa de Olá, se tiver optado por Olá tooprovide mais tarde, as informações de controlo pode agora voltar atrás tooyour importar tarefa e atualização Olá controlo número.

## <a name="copy-data-from-azure-storage-blobs-tooazure-data-lake-store"></a>Copiar dados de armazenamento do Azure blobs tooAzure Data Lake Store
Depois de estado de Olá de Olá a tarefa de importação mostra que for concluído, pode verificar se os dados de Olá estão disponíveis em blobs de armazenamento do Azure Olá que tivesse especificado. Em seguida, pode utilizar uma variedade de toomove métodos que os dados a partir de Olá blobs tooAzure Data Lake Store. Para todos os hello as opções disponíveis para carregar dados, consulte [ingestão de dados no Data Lake Store](data-lake-store-data-scenarios.md#ingest-data-into-data-lake-store).

Nesta secção, iremos fornecer definições JSON de Olá que pode utilizar toocreate um pipeline do Azure Data Factory para copiar dados. Pode utilizar estas definições JSON de Olá [portal do Azure](../data-factory/data-factory-copy-activity-tutorial-using-azure-portal.md), ou [Visual Studio](../data-factory/data-factory-copy-activity-tutorial-using-visual-studio.md), ou [Azure PowerShell](../data-factory/data-factory-copy-activity-tutorial-using-powershell.md).

### <a name="source-linked-service-azure-storage-blob"></a>Serviço ligado de origem (blob Storage do Azure)
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

### <a name="target-linked-service-azure-data-lake-store"></a>Serviço ligado (Azure Data Lake Store) de destino
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
### <a name="input-data-set"></a>Conjunto de dados de entrada
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
### <a name="output-data-set"></a>Conjunto de dados de saída
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
### <a name="pipeline-copy-activity"></a>Pipeline (atividade de cópia)
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
Para obter mais informações, consulte [mover dados de armazenamento do Azure blob tooAzure Data Lake Store utilizando o Azure Data Factory](../data-factory/data-factory-azure-datalake-connector.md).

## <a name="reconstruct-hello-data-files-in-azure-data-lake-store"></a>Reconstrua ficheiros de dados de Olá no Azure Data Lake Store
Vamos começar a utilizar um ficheiro que foi 319 GB e quebrou-a para baixo para ficheiros de tamanho mais pequeno, de modo a que pode ser transferida através do serviço do Azure para importar/exportar Olá. Agora que Olá dados no Azure Data Lake Store, iremos pode reconstrua Olá tooits original tamanho. Pode utilizar Olá seguintes, por isso, o Azure PowerShell cmldts toodo.

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

## <a name="next-steps"></a>Passos seguintes
* [Secure data in Data Lake Store (Proteger dados no Data Lake Store)](data-lake-store-secure-data.md)
* [Utilizar o Azure Data Lake Analytics com o Data Lake Store](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [Use Azure HDInsight with Data Lake Store (Utilizar o Azure HDInsight com o Data Lake Store)](data-lake-store-hdinsight-hadoop-use-portal.md)
