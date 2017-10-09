---
redirect_url: /azure/sql-data-warehouse/sql-data-warehouse-load-with-data-factory
title: armazenamento de BLOBs de dados de aaaLoad do Azure para o Azure SQL Data Warehouse (Azure Data Factory) | Microsoft Docs
description: Saiba mais dados tooload com o Azure Data Factory
services: sql-data-warehouse
documentationcenter: NA
author: barbkess
manager: jhubbard
editor: 
tags: azure-sql-data-warehouse
ms.assetid: 689fb02e-eb98-4f7c-81e6-6c1d22d53901
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.date: 11/22/2016
ms.author: barbkess
ms.custom: loading
ms.openlocfilehash: 29a220679a11cedefb0dfd06c0a6838f81a90447
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-from-azure-blob-storage-into-azure-sql-data-warehouse-azure-data-factory"></a>Carregar dados do armazenamento de blobs para o Azure SQL Data Warehouse (Azure Data Factory)
> [!div class="op_single_selector"]
> * [Data Factory](sql-data-warehouse-load-from-azure-blob-storage-with-data-factory.md)
> * [PolyBase](sql-data-warehouse-load-from-azure-blob-storage-with-polybase.md)
> 
> 

 Este tutorial mostra como toocreate um pipeline de dados do Azure Data Factory toomove tooSQL de Blob de armazenamento do Azure do armazém de dados. Com Olá os passos seguintes, irá:

* Configurar dados de exemplo num Blob de Armazenamento do Azure.
* Ligar recursos tooAzure fábrica de dados.
* Crie dados de toomove um pipeline de Blobs de armazenamento tooSQL do armazém de dados.

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Loading-Azure-SQL-Data-Warehouse-with-Azure-Data-Factory/player]
> 
> 

## <a name="before-you-begin"></a>Antes de começar
toofamiliarize por si com o Azure Data Factory, consulte [introdução tooAzure Data Factory][Introduction tooAzure Data Factory].

### <a name="create-or-identify-resources"></a>Criar ou identificar recursos
Antes de começar este tutorial, terá de Olá toohave os seguintes recursos.

* **Blob de armazenamento do Azure**: Este tutorial utiliza o Blob de armazenamento do Azure como origem de dados de Olá do pipeline de Azure Data Factory Olá e, por isso, terá de dados de exemplo de Olá toohave um toostore disponíveis. Se ainda não tiver um, saiba como demasiado[criar uma conta de armazenamento][Create a storage account].
* **O SQL Data Warehouse**: estes tutorial move Olá dados de Blob de armazenamento do Azure demasiado do armazém de dados do SQL Server e, têm de toohave um armazém de dados online carregado com Olá dados de exemplo AdventureWorksDW. Se ainda não tiver um armazém de dados, saiba como demasiado[aprovisionar um][Create a SQL Data Warehouse]. Se tiver um armazém de dados, mas não o tiver aprovisionado com dados de exemplo de Olá, pode [carregá-los manualmente][Load sample data into SQL Data Warehouse].
* **O Azure Data Factory**: Azure Data Factory irá concluir o carregamento atual Olá e, por isso, terá de toohave um que pode utilizar o pipeline de movimento de dados de Olá toobuild. Se ainda não tiver um, saiba como toocreate um no passo 1 de [introdução ao Azure Data Factory (Data Factory Editor)][Get started with Azure Data Factory (Data Factory Editor)].
* **AZCopy**: terá de dados de exemplo do AZCopy toocopy Olá da sua tooyour do cliente local Blob de armazenamento do Azure. Para obter instruções de instalação, consulte Olá [documentação do AZCopy][AZCopy documentation].

## <a name="step-1-copy-sample-data-tooazure-storage-blob"></a>Passo 1: Copiar dados de exemplo tooAzure Blob de armazenamento
Assim que tiver tudo Olá pronto, está pronto toocopy exemplo dados tooyour Blob de armazenamento do Azure.

1. [Transferir dados de exemplo][Download sample data]. Estes dados irão adicionar mais três anos de dados de vendas tooyour dados de exemplo AdventureWorksDW.
2. Utilize este Olá de toocopy de comandos do AZCopy três anos de dados tooyour Blob de armazenamento do Azure.

````
AzCopy /Source:<Sample Data Location>  /Dest:https://<storage account>.blob.core.windows.net/<container name> /DestKey:<storage key> /Pattern:FactInternetSales.csv
````


## <a name="step-2-connect-resources-tooazure-data-factory"></a>Passo 2: Ligar recursos tooAzure fábrica de dados
Agora que Olá dados estão no local podemos criar dados de Olá de toomove de pipeline do Azure Data Factory Olá do armazenamento de Blobs do Azure para o SQL Data Warehouse.

tooget iniciado, abra Olá [portal do Azure] [ Azure portal] e selecione a fábrica de dados a partir do menu da esquerda Olá.

### <a name="step-21-create-linked-service"></a>Passo 2.1: Criar o Serviço Ligado
Ligue a sua conta de armazenamento do Azure e a fábrica de dados do SQL Data Warehouse tooyour.  

1. Em primeiro lugar, iniciar o processo de registo de Olá clicando a secção "Serviços ligados" Olá a fábrica de dados e, em seguida, clique em 'Novo arquivo de dados'. Escolha um nome tooregister o armazenamento no azure, selecione armazenamento do Azure como o tipo e, em seguida, introduza o nome de conta e chave de conta.
2. tooregister SQL Data Warehouse navegue toohello "Criar e implementar" secção, selecione 'Novo arquivo de dados' e, em seguida, "Azure SQL Data Warehouse". Copie e cole neste modelo e, em seguida, preencha as suas informações específicas.

```JSON
{
    "name": "<Linked Service Name>",
    "properties": {
        "description": "",
        "type": "AzureSqlDW",
        "typeProperties": {
             "connectionString": "Data Source=tcp:<server name>.database.windows.net,1433;Initial Catalog=<server name>;Integrated Security=False;User ID=<user>@<servername>;Password=<password>;Connect Timeout=30;Encrypt=True"
         }
    }
}
```

### <a name="step-22-define-hello-dataset"></a>Passo 2.2: Definir Olá conjunto de dados
Depois de criar Olá serviços ligados, temos conjuntos de dados de Olá toodefine.  Neste caso, significa definir a estrutura de Olá dos dados de Olá que estão a ser movidos do seu armazém de dados de tooyour de armazenamento.  Pode ler mais sobre como criar

1. Inicie este processo, navegando a secção 'Criar e implementar' toohello da fábrica de dados.
2. Clique em 'Novo conjunto de dados' e, em seguida, 'Blob storage do Azure' toolink a fábrica de dados de tooyour de armazenamento.  Pode utilizar Olá abaixo script toodefine os dados no Blob storage do Azure:

```JSON
{
    "name": "<Dataset Name>",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "<linked storage name>",
        "typeProperties": {
            "folderPath": "<containter name>",
            "fileName": "FactInternetSales.csv",
            "format": {
            "type": "TextFormat",
            "columnDelimiter": ",",
            "rowDelimiter": "\n"
            }
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
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


1. Agora, iremos também definir o nosso conjunto de dados para o SQL Data Warehouse.  Vamos começar Olá mesma forma, ao clicar em 'Novo conjunto de dados' e, em seguida, "Azure SQL Data Warehouse".

```JSON
{
    "name": "DWDataset",
    "properties": {
        "type": "AzureSqlDWTable",
        "linkedServiceName": "AzureSqlDWLinkedService",
        "typeProperties": {
            "tableName": "FactInternetSales"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

## <a name="step-3-create-and-run-your-pipeline"></a>Passo 3: criar e executar o pipeline
Por último, iremos configurar e executar pipeline Olá no Azure Data Factory.  Esta operação Olá que irá concluir o movimento de dados de Olá é.  Pode encontrar uma visão completa de operações de Olá que pode realizar com o armazém de dados do SQL Server e do Azure Data Factory [aqui][Move data tooand from Azure SQL Data Warehouse using Azure Data Factory].

Na secção 'Criar e implementar' de Olá agora, clique em "Mais comandos" e, em seguida, "Novo Pipeline".  Depois de criar o pipeline de Olá, pode utilizar Olá abaixo código tootransfer Olá tooyour dados do armazém de dados:

```JSON
{
    "name": "<Pipeline Name>",
    "properties": {
        "description": "<Description>",
        "activities": [
          {
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "BlobSource",
                    "skipHeaderLineCount": 1
                },
                "sink": {
                    "type": "SqlDWSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:10"
                }
            },
            "inputs": [
              {
                "name": "<Storage Dataset>"
              }
            ],
            "outputs": [
              {
                "name": "<Data Warehouse Dataset>"
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
            "name": "Sample Copy",
            "description": "Copy Activity"
          }
        ],
        "start": "<Date YYYY-MM-DD>",
        "end": "<Date YYYY-MM-DD>",
        "isPaused": false
    }
}
```

## <a name="next-steps"></a>Passos seguintes
toolearn mais, comece por visualizar:

* [Percurso de aprendizagem do Azure Data Factory][Azure Data Factory learning path].
* [Conector do Azure SQL Data Warehouse][Azure SQL Data Warehouse Connector]. Este é o tópico de referência principal Olá para utilizar o Azure Data Factory com o Azure SQL Data Warehouse.

Estes tópicos fornecem informações detalhadas sobre o Azure Data Factory. Abrangem a SQL Database do Azure ou o HDinsight, mas as informações de Olá também se aplica tooAzure SQL Data Warehouse.

* [Tutorial: Introdução ao Azure Data Factory] [ Tutorial: Get started with Azure Data Factory] este é Olá tutorial de núcleo para processamento de dados com o Azure Data Factory. Este tutorial irá criar o seu primeiro pipeline, que utiliza o HDInsight tootransform e analisar registos web mensalmente. Tenha em atenção que não existe nenhuma atividade de cópia neste tutorial.
* [Tutorial: Copiar dados de BLOBs de armazenamento do Azure tooAzure base de dados SQL][Tutorial: Copy data from Azure Storage Blob tooAzure SQL Database]. Neste tutorial, irá criar um pipeline de dados do Azure Data Factory toocopy do Blob de armazenamento do Azure tooAzure base de dados SQL.

<!--Image references-->

<!--Article references-->
[AZCopy documentation]: ../storage/storage-use-azcopy.md
[Azure SQL Data Warehouse Connector]: ../data-factory/data-factory-azure-sql-data-warehouse-connector.md
[BCP]: sql-data-warehouse-load-with-bcp.md
[Create a SQL Data Warehouse]: sql-data-warehouse-get-started-provision.md
[Create a storage account]: ../storage/storage-create-storage-account.md#create-a-storage-account
[Data Factory]: sql-data-warehouse-get-started-load-with-azure-data-factory.md
[Get started with Azure Data Factory (Data Factory Editor)]: ../data-factory/data-factory-build-your-first-pipeline-using-editor.md
[Introduction tooAzure Data Factory]: ../data-factory/data-factory-introduction.md
[Load sample data into SQL Data Warehouse]: sql-data-warehouse-load-sample-databases.md
[Move data tooand from Azure SQL Data Warehouse using Azure Data Factory]: ../data-factory/data-factory-azure-sql-data-warehouse-connector.md
[PolyBase]: sql-data-warehouse-get-started-load-with-polybase.md
[Tutorial: Copy data from Azure Storage Blob tooAzure SQL Database]: ../data-factory/data-factory-copy-data-from-azure-blob-storage-to-sql-database.md
[Tutorial: Get started with Azure Data Factory]: ../data-factory/data-factory-build-your-first-pipeline.md

<!--MSDN references-->

<!--Other Web references-->
[Azure Data Factory learning path]: https://azure.microsoft.com/documentation/learning-paths/data-factory
[Azure portal]: https://portal.azure.com
[Download sample data]: https://migrhoststorage.blob.core.windows.net/adfsample/FactInternetSales.csv
