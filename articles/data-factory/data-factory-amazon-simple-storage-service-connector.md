---
title: "dados aaaMove do serviço de armazenamento simples Amazon utilizando o Data Factory | Microsoft Docs"
description: "Saiba mais sobre como dados toomove a partir do serviço de armazenamento simples (S3) do Amazon através da utilização do Azure Data Factory."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 636d3179-eba8-4841-bcb4-3563f6822a26
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jingwang
ms.openlocfilehash: 8a8cd2845fd1de74413bd0372f3aabfb4817549b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-amazon-simple-storage-service-by-using-azure-data-factory"></a>Mover dados do serviço de armazenamento simples Amazon através da utilização do Azure Data Factory
Este artigo explica como toouse Olá atividade de cópia de dados do Azure Data Factory toomove do serviço de armazenamento simples (S3) do Amazon. Baseia-se no Olá [atividades de movimentos de dados](data-factory-data-movement-activities.md) artigo, que apresenta uma descrição geral do movimento de dados com a atividade de cópia de Olá.

Pode copiar dados do arquivo de dados do Amazon S3 tooany suportado sink. Para obter uma lista dos dados arquivos suportados como sinks pela atividade de cópia de Olá, consulte Olá [arquivos de dados suportados](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabela. Fábrica de dados atualmente suporta apenas dados mover de arquivos de dados do Amazon S3 tooother, mas não mover dados de outros dados armazena tooAmazon S3.

## <a name="required-permissions"></a>Permissões necessárias
toocopy dados do Amazon S3, certifique-se de que lhe foram concedidas Olá as seguintes permissões:

* `s3:GetObject`e `s3:GetObjectVersion` para operações de objeto do Amazon S3.
* `s3:ListBucket`para operações de registo do Amazon S3. Se estiver a utilizar o Assistente de cópia do Data Factory, de Olá `s3:ListAllMyBuckets` também é necessário.

Para obter detalhes sobre a lista completa de Olá Amazon S3 permissões, consulte [especificar permissões numa política](http://docs.aws.amazon.com/AmazonS3/latest/dev/using-with-s3-actions.html).

## <a name="getting-started"></a>Introdução
Pode criar um pipeline com uma atividade de cópia move dados a partir de uma origem de Amazon S3, utilizando ferramentas diferentes ou APIs.

Olá toocreate da forma mais fácil um pipeline está toouse Olá **Assistente para copiar**. Para instruções rápidas, consulte [Tutorial: criar um pipeline com o Assistente para copiar](data-factory-copy-data-wizard-tutorial.md).

Também pode utilizar Olá seguintes ferramentas toocreate um pipeline: **portal do Azure**, **Visual Studio**, **Azure PowerShell**, **modelo Azure Resource Manager** , **.NET API**, e **REST API**. Para instruções passo a passo toocreate um pipeline com uma atividade de cópia, consulte Olá [tutorial de atividade de cópia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).

Se utilizar ferramentas ou APIs, execute Olá os seguintes passos toocreate um pipeline que move o arquivo de dados do tooa sink do arquivo de dados de uma origem de dados:

1. Criar **serviços ligados** fábrica de dados de tooyour de arquivos de dados de entrada e saída de toolink.
2. Criar **conjuntos de dados** toorepresent de entrada e saída de operação de cópia de dados para Olá.
3. Criar um **pipeline** com uma atividade de cópia executa um conjunto de dados como entrada e um conjunto de dados como resultado.

Quando utiliza o Assistente de Olá, definições de JSON para estas entidades do Data Factory (serviços ligados, conjuntos de dados e pipeline Olá) são criadas automaticamente para si. Quando utilizar APIs (exceto .NET API) ou ferramentas, é possível definir estas entidades do Data Factory utilizando o formato JSON Olá. Para um exemplo com definições de JSON para entidades do Data Factory que são utilizados toocopy dados de um arquivo de dados do Amazon S3, consulte Olá [exemplo JSON: copiar dados do Amazon S3 tooAzure Blob](#json-example-copy-data-from-amazon-s3-to-azure-blob) secção deste artigo.

> [!NOTE]
> Para obter detalhes sobre os formatos de ficheiro e compressão suportados para uma atividade de cópia, consulte [formatos de ficheiro e compressão no Azure Data Factory](data-factory-supported-file-and-compression-formats.md).

Olá seguintes secções fornece detalhes sobre as propriedades JSON que são utilizados toodefine Data Factory entidades específica tooAmazon S3.

## <a name="linked-service-properties"></a>Propriedades de serviço ligado
Um serviço ligado liga uma fábrica de dados de tooa de arquivo de dados. Criar um serviço ligado do tipo **AwsAccessKey** toolink tooyour fábrica de dados de arquivo de dados do Amazon S3. Olá, a tabela seguinte fornece um serviço descrição JSON elementos específico tooAmazon S3 (AwsAccessKey) ligado.

| Propriedade | Descrição | Valores permitidos | Necessário |
| --- | --- | --- | --- |
| accessKeyID |ID da chave de acesso secreta Olá. |Cadeia |Sim |
| secretAccessKey |chave de acesso secreta Olá próprio. |Cadeia secreta encriptada |Sim |

Segue-se um exemplo:

```json
{
    "name": "AmazonS3LinkedService",
    "properties": {
        "type": "AwsAccessKey",
        "typeProperties": {
            "accessKeyId": "<access key id>",
            "secretAccessKey": "<secret access key>"
        }
    }
}
```

## <a name="dataset-properties"></a>Propriedades do conjunto de dados
toospecify toorepresent um conjunto de dados de entrada os dados no Blob storage do Azure, defina a propriedade de tipo de Olá de conjunto de dados de Olá demasiado**AmazonS3**. Conjunto Olá **linkedServiceName** propriedade do Olá dataset toohello nome Olá Amazon S3 serviço ligado. Para uma lista completa das secções e propriedades disponíveis para definir os conjuntos de dados, consulte [criar conjuntos de dados](data-factory-create-datasets.md). 

As secções, tais como a estrutura, a disponibilidade e a política são semelhantes para todos os tipos de conjunto de dados (por exemplo, SQL database, blob do Azure e tabela do Azure). Olá **typeProperties** secção é diferente para cada tipo de conjunto de dados e fornece informações sobre a localização de Olá dos dados de Olá no arquivo de dados de Olá. Olá **typeProperties** secção para um conjunto de dados do tipo **AmazonS3** (que inclui o conjunto de dados de Olá Amazon S3) tem Olá seguintes propriedades:

| Propriedade | Descrição | Valores permitidos | Necessário |
| --- | --- | --- | --- |
| bucketName |nome do registo de Olá S3. |Cadeia |Sim |
| key |chave do objeto de Olá S3. |Cadeia |Não |
| prefixo |Prefixo para a chave de objeto Olá S3. Objetos cujas chaves começar a utilizar este prefixo estão selecionados. Aplica-se apenas quando o chave está vazia. |Cadeia |Não |
| Versão |versão de Olá do objeto de Olá S3, se o controlo de versões de S3 estiver ativado. |Cadeia |Não |
| formato | é suportado os seguintes tipos de formato de Olá: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**. Conjunto Olá **tipo** propriedade em formato tooone destes valores. Para obter mais informações, consulte Olá [formato de texto](data-factory-supported-file-and-compression-formats.md#text-format), [formato JSON](data-factory-supported-file-and-compression-formats.md#json-format), [formato Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc formato](data-factory-supported-file-and-compression-formats.md#orc-format), e [formato Parquet ](data-factory-supported-file-and-compression-formats.md#parquet-format) secções. <br><br> Se pretender que os ficheiros de toocopy como-entre baseados em ficheiros arquivos de (cópia binário), ignorar Olá formato secção ambas as definições do conjunto de dados de entrada e de saída. |Não | |
| Compressão | Especifique o tipo de Olá e nível de compressão de dados de Olá. os tipos de Olá suportado são: **GZip**, **Deflate**, **BZip2**, e **ZipDeflate**. níveis de Olá suportado são: **Optimal** e **Fastest**. Para obter mais informações, consulte [formatos de ficheiro e compressão no Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support). |Não | |


> [!NOTE]
> **bucketName + chave** Especifica a localização de Olá do objeto de Olá S3, em que o registo é recipiente-raiz Olá para objetos de S3, e chave é o objeto de toohello S3 Olá caminho completo.

### <a name="sample-dataset-with-prefix"></a>Conjunto de dados de exemplo com prefixo

```json
{
    "name": "dataset-s3",
    "properties": {
        "type": "AmazonS3",
        "linkedServiceName": "link- testS3",
        "typeProperties": {
            "prefix": "testFolder/test",
            "bucketName": "testbucket",
            "format": {
                "type": "OrcFormat"
            }
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```
### <a name="sample-dataset-with-version"></a>Conjunto de dados de exemplo (com a versão)

```json
{
    "name": "dataset-s3",
    "properties": {
        "type": "AmazonS3",
        "linkedServiceName": "link- testS3",
        "typeProperties": {
            "key": "testFolder/test.orc",
            "bucketName": "testbucket",
            "version": "XXXXXXXXXczm0CJajYkHf0_k6LhBmkcL",
            "format": {
                "type": "OrcFormat"
            }
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```

### <a name="dynamic-paths-for-s3"></a>Caminhos de dinâmicos para S3
Olá anterior exemplo utiliza valores fixos para Olá **chave** e **bucketName** propriedades no conjunto de dados de Olá Amazon S3.

```json
"key": "testFolder/test.orc",
"bucketName": "testbucket",
```

Pode ter o Data Factory calcular estas propriedades dinamicamente em runtime, utilizando variáveis de sistema, tais como SliceStart.

```json
"key": "$$Text.Format('{0:MM}/{0:dd}/test.orc', SliceStart)"
"bucketName": "$$Text.Format('{0:yyyy}', SliceStart)"
```

Pode fazê-lo hello mesmo para Olá **prefixo** propriedade de um conjunto de dados do Amazon S3. Para obter uma lista de funções suportadas e as variáveis, consulte [funções de Data Factory e variáveis do sistema](data-factory-functions-variables.md).

## <a name="copy-activity-properties"></a>Propriedades da atividade de cópia
Para uma lista completa das secções e propriedades disponíveis para definir as atividades, consulte [Criar pipelines](data-factory-create-pipelines.md). Propriedades, tais como o nome, descrição e de saída, tabelas e as políticas estão disponíveis para todos os tipos de atividades. Propriedades disponíveis nos Olá **typeProperties** secção da atividade de Olá variar de acordo com cada tipo de atividade. Para a atividade de cópia de Olá, propriedades variam consoante os tipos de origens e sinks Olá. Quando uma origem de atividade de cópia de Olá é do tipo **FileSystemSource** (que inclui o Amazon S3), Olá seguinte propriedade está disponível no **typeProperties** secção:

| Propriedade | Descrição | Valores permitidos | Necessário |
| --- | --- | --- | --- |
| Recursiva |Especifica se a lista de toorecursively S3 objetos no diretório de Olá. |Verdadeiro/Falso |Não |

## <a name="json-example-copy-data-from-amazon-s3-tooazure-blob-storage"></a>Exemplo JSON: copiar dados do Amazon S3 tooAzure armazenamento de BLOBs
Este exemplo mostra como toocopy dados do Amazon S3 tooan Blob storage do Azure. No entanto, dados podem ser copiados diretamente demasiado[qualquer um dos Olá sinks que são suportados](data-factory-data-movement-activities.md#supported-data-stores-and-formats) utilizando a atividade de cópia de Olá na fábrica de dados.

exemplo de Olá fornece definições de JSON para Olá seguintes entidades do Data Factory. Pode utilizar estes toocreate definições dados de toocopy um pipeline do armazenamento de tooBlob Amazon S3, utilizando Olá [portal do Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), ou [PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).   

* Um serviço ligado do tipo [AwsAccessKey](#linked-service-properties).
* Um serviço ligado do tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
* Uma entrada [dataset](data-factory-create-datasets.md) do tipo [AmazonS3](#dataset-properties).
* Uma saída [dataset](data-factory-create-datasets.md) do tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
* A [pipeline](data-factory-create-pipelines.md) com atividade de cópia que utiliza [FileSystemSource](#copy-activity-properties) e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).

exemplo de Olá copia dados da Amazon S3 tooan BLOBs do Azure a cada hora. Propriedades JSON de Olá utilizadas nestes exemplos são descritas nas secções seguintes exemplos de Olá.

### <a name="amazon-s3-linked-service"></a>Serviço ligado do Amazon S3

```json
{
    "name": "AmazonS3LinkedService",
    "properties": {
        "type": "AwsAccessKey",
        "typeProperties": {
            "accessKeyId": "<access key id>",
            "secretAccessKey": "<secret access key>"
        }
    }
}
```

### <a name="azure-storage-linked-service"></a>Serviço ligado do Storage do Azure

```json
{
  "name": "AzureStorageLinkedService",
  "properties": {
    "type": "AzureStorage",
    "typeProperties": {
      "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
    }
  }
}
```

### <a name="amazon-s3-input-dataset"></a>Conjunto de dados de entrada Amazon S3

Definição **"external": true** informa o serviço do Data Factory Olá esse conjunto de dados de Olá é toohello externo fábrica de dados. Defina um conjunto de dados de entrada que não é produzido por uma atividade no pipeline de Olá tootrue esta propriedade.

```json
    {
        "name": "AmazonS3InputDataset",
        "properties": {
            "type": "AmazonS3",
            "linkedServiceName": "AmazonS3LinkedService",
            "typeProperties": {
                "key": "testFolder/test.orc",
                "bucketName": "testbucket",
                "format": {
                    "type": "OrcFormat"
                }
            },
            "availability": {
                "frequency": "Hour",
                "interval": 1
            },
            "external": true
        }
    }
```


### <a name="azure-blob-output-dataset"></a>Conjunto de dados de saída do Blob do Azure

São escritos dados no blob tooa de novo a cada hora (frequência: hora, intervalo: 1). caminho da pasta Olá para BLOBs Olá dinamicamente é avaliado com base na hora de início de Olá do setor de Olá que está a ser processado. caminho da pasta Olá utiliza as partes de ano, mês, dia e horas Olá Olá da hora de início.

```json
{
    "name": "AzureBlobOutputDataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/fromamazons3/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
            "format": {
                "type": "TextFormat",
                "rowDelimiter": "\n",
                "columnDelimiter": "\t"
            },
            "partitionedBy": [
                {
                    "name": "Year",
                    "value": {
                        "type": "DateTime",
                        "date": "SliceStart",
                        "format": "yyyy"
                    }
                },
                {
                    "name": "Month",
                    "value": {
                        "type": "DateTime",
                        "date": "SliceStart",
                        "format": "MM"
                    }
                },
                {
                    "name": "Day",
                    "value": {
                        "type": "DateTime",
                        "date": "SliceStart",
                        "format": "dd"
                    }
                },
                {
                    "name": "Hour",
                    "value": {
                        "type": "DateTime",
                        "date": "SliceStart",
                        "format": "HH"
                    }
                }
            ]
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```


### <a name="copy-activity-in-a-pipeline-with-an-amazon-s3-source-and-a-blob-sink"></a>Atividade de cópia de um pipeline com uma origem de Amazon S3 e um receptor de blob

Olá pipeline contém uma atividade de cópia é configurado toouse Olá conjuntos de dados de entrada e de saída, não sendo toorun agendada a cada hora. No pipeline de Olá definição JSON, Olá **origem** tipo está definido demasiado**FileSystemSource**, e **sink** tipo está definido demasiado**BlobSink**.

```json
{
    "name": "CopyAmazonS3ToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "FileSystemSource",
                        "recursive": true
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "AmazonS3InputDataset"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobOutputDataSet"
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
                "name": "AmazonS3ToBlob"
            }
        ],
        "start": "2014-08-08T18:00:00Z",
        "end": "2014-08-08T19:00:00Z"
    }
}
```
> [!NOTE]
> colunas de toomap um toocolumns de conjunto de dados de origem de um conjunto de dados dependente, consulte [mapeamento de colunas do conjunto de dados no Azure Data Factory](data-factory-map-columns.md).


## <a name="next-steps"></a>Passos seguintes
Consulte Olá seguintes artigos:

* toolearn sobre chave factors desse desempenho impacto de movimento de dados (atividade de cópia) no Factory de dados e várias formas toooptimize-lo, consulte Olá [copiar guia Otimização e de desempenho de atividade](data-factory-copy-activity-performance.md).

* Para obter instruções passo a passo para criar um pipeline com uma atividade de cópia, consulte Olá [tutorial de atividade de cópia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).
