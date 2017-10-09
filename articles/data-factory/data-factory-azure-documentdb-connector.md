---
title: aaaMove dados da base de dados do Azure Cosmos | Microsoft Docs
description: "Saiba como mover dados da coleção de BD do Cosmos Azure utilizando o Azure Data Factory"
services: data-factory, cosmosdb
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: c9297b71-1bb4-4b29-ba3c-4cf1f5575fac
ms.service: multiple
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jingwang
ms.openlocfilehash: bd23ce4e004a972ce6f3e4165cfdea4f0c18fecc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-tooand-from-azure-cosmos-db-using-azure-data-factory"></a>Mover dados tooand da base de dados do Cosmos do Azure utilizando o Azure Data Factory
Este artigo explica como toouse Olá atividade de cópia de dados de toomove do Azure Data Factory para/da base de dados do Azure Cosmos (API do DocumentDB). Baseia-se no Olá [atividades de movimentos de dados](data-factory-data-movement-activities.md) artigo, que apresenta uma descrição geral do movimento de dados com a atividade de cópia de Olá. 

Pode copiar dados de qualquer origem suportada dados armazenam tooAzure Cosmos DB ou a partir dos dados do Azure Cosmos DB tooany suportado sink armazenam. Para obter uma lista dos arquivos de dados suportados como origens ou sinks pela atividade de cópia de Olá, consulte Olá [arquivos de dados suportados](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabela. 

> [!IMPORTANT]
> Conector Cosmos BD Azure suportam apenas a API do DocumentDB.

dados de toocopy como-é para/de ficheiros JSON ou de outra coleção Cosmos DB, consulte [documentos JSON de importação/exportação](#importexport-json-documents).

## <a name="getting-started"></a>Introdução
Pode criar um pipeline com uma atividade de cópia move os dados do Azure Cosmos DB utilizando ferramentas diferentes/APIs.

Olá toocreate da forma mais fácil um pipeline está toouse Olá **Assistente para copiar**. Consulte [Tutorial: criar um pipeline com o Assistente para copiar](data-factory-copy-data-wizard-tutorial.md) para obter instruções sobre como criar um pipeline com o Assistente de cópia de dados Olá rápida.

Também pode utilizar Olá seguintes ferramentas toocreate um pipeline: **portal do Azure**, **Visual Studio**, **Azure PowerShell**, **modelo Azure Resource Manager** , **.NET API**, e **REST API**. Consulte [tutorial de atividade de cópia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para instruções passo a passo toocreate um pipeline com uma atividade de cópia. 

Se utilizar ferramentas de Olá ou APIs, execute Olá os seguintes passos toocreate um pipeline que move o arquivo de dados do tooa sink do arquivo de dados de uma origem de dados: 

1. Criar **serviços ligados** fábrica de dados de tooyour de arquivos de dados de entrada e saída de toolink.
2. Criar **conjuntos de dados** toorepresent de entrada e saída de operação de cópia de dados para Olá. 
3. Criar um **pipeline** com uma atividade de cópia executa um conjunto de dados como entrada e um conjunto de dados como resultado. 

Quando utiliza o Assistente de Olá, definições de JSON para estas entidades do Data Factory (serviços ligados, conjuntos de dados e pipeline Olá) são criadas automaticamente para si. Ao utilizar ferramentas/APIs (exceto .NET API), é possível definir estas entidades do Data Factory utilizando o formato JSON Olá.  Para exemplos com definições de JSON para entidades do Data Factory que são utilizados toocopy dados da base de dados do Cosmos, consulte [exemplos JSON](#json-examples) secção deste artigo. 

Olá seguintes secções fornece detalhes sobre as propriedades JSON que são utilizados toodefine Data Factory entidades específicas tooCosmos DB: 

## <a name="linked-service-properties"></a>Propriedades de serviço ligado
Olá, a tabela seguinte fornece uma descrição para JSON elementos específico tooAzure serviço de base de dados do Cosmos ligado.

| **Propriedade** | **Descrição** | **Necessário** |
| --- | --- | --- |
| tipo |a propriedade de tipo Olá tem de ser definida: **DocumentDb** |Sim |
| connectionString |Especifique informações necessárias base de dados do tooconnect tooAzure BD do Cosmos. |Sim |

Exemplo:

```JSON
{
  "name": "CosmosDbLinkedService",
  "properties": {
    "type": "DocumentDb",
    "typeProperties": {
      "connectionString": "AccountEndpoint=<EndpointUrl>;AccountKey=<AccessKey>;Database=<Database>"
    }
  }
}
```

## <a name="dataset-properties"></a>Propriedades do conjunto de dados
Para obter uma lista completa das secções & Propriedades disponíveis para definir os conjuntos de dados Consulte toohello [criar conjuntos de dados](data-factory-create-datasets.md) artigo. As secções como estrutura, disponibilidade e a política de um conjunto de dados JSON são semelhantes para todos os tipos de conjunto de dados (SQL do Azure, Azure blob, tabela do Azure, etc.).

secção de typeProperties Olá é diferente para cada tipo de conjunto de dados e fornece informações sobre a localização de Olá dos dados de Olá no arquivo de dados de Olá. Olá typeProperties secção Olá conjunto de dados do tipo **DocumentDbCollection** tem Olá seguintes propriedades.

| **Propriedade** | **Descrição** | **Necessário** |
| --- | --- | --- |
| CollectionName |Nome da coleção de documentos do Cosmos DB de Olá. |Sim |

Exemplo:

```JSON
{
  "name": "PersonCosmosDbTable",
  "properties": {
    "type": "DocumentDbCollection",
    "linkedServiceName": "CosmosDbLinkedService",
    "typeProperties": {
      "collectionName": "Person"
    },
    "external": true,
    "availability": {
      "frequency": "Day",
      "interval": 1
    }
  }
}
```
### <a name="schema-by-data-factory"></a>Esquema pela fábrica de dados
Para os arquivos de dados sem esquema, tais como a base de dados do Azure Cosmos, Olá serviço Data Factory infere esquema Olá dos Olá seguintes formas:  

1. Se especificar a estrutura de Olá dos dados através da utilização de Olá **estrutura** propriedade na definição do conjunto de dados de Olá, Olá serviço Data Factory honra esta estrutura como esquema de Olá. Neste caso, se uma linha não contém um valor para uma coluna, irá ser fornecido um valor nulo para o mesmo.
2. Se não especificar a estrutura de Olá dos dados utilizando Olá **estrutura** propriedade na definição do conjunto de dados de Olá, Olá serviço Data Factory infere esquema Olá ao utilizar primeira linha de Olá nos dados de Olá. Neste caso, se a primeira linha de Olá não contém o esquema completa Olá, algumas colunas estará em falta no resultado de Olá da operação de cópia.

Por conseguinte, para origens de dados sem esquema, Olá procedimento recomendado é estrutura de Olá toospecify dos dados através de Olá **estrutura** propriedade.

## <a name="copy-activity-properties"></a>Propriedades da atividade de cópia
Para obter uma lista completa das secções & Propriedades disponíveis para definir atividades Consulte toohello [criar Pipelines](data-factory-create-pipelines.md) artigo. Propriedades, tais como o nome, descrição e de saída, tabelas e política estão disponíveis para todos os tipos de atividades.

> [!NOTE]
> Olá atividade de cópia demora apenas uma entrada e produz saída de apenas um.

As propriedades disponíveis na secção de typeProperties Olá da atividade de Olá no Olá por outro lado variar com cada tipo de atividade e, em caso de atividade de cópia que variam consoante os tipos de origens e sinks Olá.

Em caso de atividade de cópia quando a origem é do tipo **DocumentDbCollectionSource** Olá seguintes propriedades está disponível no **typeProperties** secção:

| **Propriedade** | **Descrição** | **Valores permitidos** | **Necessário** |
| --- | --- | --- | --- |
| consulta |Especifique Olá consulta tooread dados. |Suportado pelo Azure Cosmos DB de cadeia de consulta. <br/><br/>Exemplo:`SELECT c.BusinessEntityID, c.PersonType, c.NameStyle, c.Title, c.Name.First AS FirstName, c.Name.Last AS LastName, c.Suffix, c.EmailPromotion FROM c WHERE c.ModifiedDate > \"2009-01-01T00:00:00\"` |Não <br/><br/>Se não for especificado, Olá instrução de SQL que é executada:`select <columns defined in structure> from mycollection` |
| nestingSeparator |Caráter especial tooindicate que Olá documento está aninhado |Qualquer caráter. <br/><br/>BD do Cosmos do Azure é um arquivo de NoSQL para documentos JSON, onde são permitidas estruturas aninhadas. O Azure Data Factory permite que a hierarquia de toodenote do utilizador através de nestingSeparator, que é "." no Olá acima exemplos. Com separador Olá, atividade de cópia de Olá irá gerar o objeto de "Name" Olá com elementos três subordinados too"Name.First primeiro, média e última, de acordo com", "Name.Middle" e "Name.Last" Olá definição de tabela. |Não |

**DocumentDbCollectionSink** suporta Olá seguintes propriedades:

| **Propriedade** | **Descrição** | **Valores permitidos** | **Necessário** |
| --- | --- | --- | --- |
| nestingSeparator |É necessário um caráter especial no tooindicate nome de coluna de origem de Olá que aninhada documento. <br/><br/>Por exemplo acima: `Name.First` na saída de Olá tabela produz Olá estrutura JSON no documento de BD do Cosmos Olá os seguintes:<br/><br/>"Nome": {<br/>    "First": "João"<br/>}, |Caráter é utilizado tooseparate níveis de aninhamento.<br/><br/>Valor predefinido é `.` (ponto final). |Caráter é utilizado tooseparate níveis de aninhamento. <br/><br/>Valor predefinido é `.` (ponto final). |
| WriteBatchSize |Número de paralelo pedidos documentos de toocreate de serviço de base de dados do Cosmos tooAzure.<br/><br/>Pode otimizar o desempenho de Olá ao copiar dados do Cosmos DB utilizando esta propriedade. Pode esperar um desempenho melhor quando aumenta writeBatchSize porque mais pedidos paralelas tooCosmos DB são enviados. No entanto, terá de tooavoid limitação que pode acionar a mensagem de erro de saudação: "taxa é grande pedido".<br/><br/>Limitação é decidida por um número de fatores, incluindo o tamanho de documentos, número de termos de documentos, a indexação de política de coleção de destino, etc. Para operações de cópia, pode utilizar uma melhor toohave Olá da coleção (por exemplo, S3) a maioria das débito disponível (2,500 pedidos unidades por segundo). |Número inteiro |Não (predefinição: 5) |
| writeBatchTimeout |De tempo de espera para Olá operação toocomplete antes de atingir o tempo limite. |TimeSpan<br/><br/> Exemplo: "00: 30:00" (30 minutos). |Não |

## <a name="importexport-json-documents"></a>Documentos JSON para importar/exportar
Utilizar este conector Cosmos DB, pode facilmente

* Importe documentos JSON de várias origens para Cosmos DB, incluindo o Blob do Azure, Azure Data Lake, sistema de ficheiros no local ou outros arquivos de ficheiros suportados pelo Azure Data Factory.
* Exporte documentos JSON do Cosmos DB collecton em vários arquivos de ficheiros.
* Migrar dados entre duas coleções de BD do Cosmos como-é.

Copiar do tooachieve agnóstico esse esquema, 
* Ao utilizar o Assistente para copiar, verifique Olá **"Exportar como-é tooJSON ficheiros ou noutra coleção Cosmos BD"** opção.
* Quando utilizar a edição de JSON, não especifique secção de "estrutura" Olá dos DataSets de BD do Cosmos nem origem de propriedade de "nestingSeparator" na base de dados do Cosmos/sink na atividade de cópia. tooimport da / tooJSON ficheiros de exportação, no conjunto de dados de arquivo de ficheiros de Olá especificar tipo de formato como "JsonFormat", "filePattern" de configuração e ignorar as definições do formato de Olá rest, consulte [formato JSON](data-factory-supported-file-and-compression-formats.md#json-format) secção em detalhes.

## <a name="json-examples"></a>Exemplos JSON
Olá exemplos seguintes fornecem definições JSON de exemplo que pode utilizar toocreate um pipeline utilizando [portal do Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) ou [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) ou [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md). Estes mostram como toocopy tooand de dados da base de dados do Azure Cosmos e armazenamento de Blobs do Azure. No entanto, os dados podem ser copiados **diretamente** de qualquer uma das origens de Olá tooany de Olá sinks indicado [aqui](data-factory-data-movement-activities.md#supported-data-stores-and-formats) utilizando Olá atividade de cópia no Azure Data Factory.

## <a name="example-copy-data-from-azure-cosmos-db-tooazure-blob"></a>Exemplo: Copiar dados de base de dados do Azure Cosmos tooAzure Blob
exemplo de Olá abaixo mostra:

1. Um serviço ligado do tipo [DocumentDb](#linked-service-properties).
2. Um serviço ligado do tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
3. Uma entrada [dataset](data-factory-create-datasets.md) do tipo [DocumentDbCollection](#dataset-properties).
4. Uma saída [dataset](data-factory-create-datasets.md) do tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
5. A [pipeline](data-factory-create-pipelines.md) com atividade de cópia que utiliza [DocumentDbCollectionSource](#copy-activity-properties) e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).

exemplo de Olá copia os dados na base de dados do Azure Cosmos tooAzure Blob. Propriedades JSON de Olá utilizadas nestes exemplos são descritas nas secções seguintes exemplos de Olá.

**BD do Azure do Cosmos serviço ligado:**

```JSON
{
  "name": "CosmosDbLinkedService",
  "properties": {
    "type": "DocumentDb",
    "typeProperties": {
      "connectionString": "AccountEndpoint=<EndpointUrl>;AccountKey=<AccessKey>;Database=<Database>"
    }
  }
}
```
**Serviço ligado do armazenamento de Blobs do Azure:**

```JSON
{
  "name": "StorageLinkedService",
  "properties": {
    "type": "AzureStorage",
    "typeProperties": {
      "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
    }
  }
}
```
**Conjunto de dados de entrada Document DB do Azure:**

exemplo de Olá parte do princípio de que tem uma coleção designada **pessoa** numa base de dados do Azure Cosmos DB.

A definição "external": "true" e a especificação de externalData informações de política Olá do Azure Data Factory service nessa tabela Olá é toohello externo fábrica de dados e não são produzidos por uma atividade no factory de dados de Olá.

```JSON
{
  "name": "PersonCosmosDbTable",
  "properties": {
    "type": "DocumentDbCollection",
    "linkedServiceName": "CosmosDbLinkedService",
    "typeProperties": {
      "collectionName": "Person"
    },
    "external": true,
    "availability": {
      "frequency": "Day",
      "interval": 1
    }
  }
}
```

**Conjunto de dados de saída do Blob do Azure:**

Os dados são o blob tooa copiados de novo a cada hora com o caminho de Olá para BLOBs Olá ao refletir datetime específico Olá com granularidade de hora.

```JSON
{
  "name": "PersonBlobTableOut",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "docdb",
      "format": {
        "type": "TextFormat",
        "columnDelimiter": ",",
        "nullValue": "NULL"
      }
    },
    "availability": {
      "frequency": "Day",
      "interval": 1
    }
  }
}
```
Documento JSON de exemplo no Olá coleção pessoa numa base de dados do Cosmos DB:

```JSON
{
  "PersonId": 2,
  "Name": {
    "First": "Jane",
    "Middle": "",
    "Last": "Doe"
  }
}
```
BD do cosmos suporta a consulta de documentos utilizando um SQL Server como a sintaxe por hierárquicos documentos JSON.

Exemplo: 

```sql
SELECT Person.PersonId, Person.Name.First AS FirstName, Person.Name.Middle as MiddleName, Person.Name.Last AS LastName FROM Person
```

seguinte Olá pipeline copia dados a partir Olá coleção de pessoa em Olá tooan de base de dados de base de dados do Azure Cosmos BLOBs do Azure. Como parte da Olá de atividade de cópia de Olá foram especificados conjuntos de dados de entrada e de saída.  

```JSON
{
  "name": "DocDbToBlobPipeline",
  "properties": {
    "activities": [
      {
        "type": "Copy",
        "typeProperties": {
          "source": {
            "type": "DocumentDbCollectionSource",
            "query": "SELECT Person.Id, Person.Name.First AS FirstName, Person.Name.Middle as MiddleName, Person.Name.Last AS LastName FROM Person",
            "nestingSeparator": "."
          },
          "sink": {
            "type": "BlobSink",
            "blobWriterAddHeader": true,
            "writeBatchSize": 1000,
            "writeBatchTimeout": "00:00:59"
          }
        },
        "inputs": [
          {
            "name": "PersonCosmosDbTable"
          }
        ],
        "outputs": [
          {
            "name": "PersonBlobTableOut"
          }
        ],
        "policy": {
          "concurrency": 1
        },
        "name": "CopyFromDocDbToBlob"
      }
    ],
    "start": "2015-04-01T00:00:00Z",
    "end": "2015-04-02T00:00:00Z"
  }
}
```
## <a name="example-copy-data-from-azure-blob-tooazure-cosmos-db"></a>Exemplo: Copiar dados de Blobs do Azure tooAzure Cosmos DB 
exemplo de Olá abaixo mostra:

1. Um serviço ligado do tipo [DocumentDb](#azure-documentdb-linked-service-properties).
2. Um serviço ligado do tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
3. Uma entrada [dataset](data-factory-create-datasets.md) do tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
4. Uma saída [dataset](data-factory-create-datasets.md) do tipo [DocumentDbCollection](#azure-documentdb-dataset-type-properties).
5. A [pipeline](data-factory-create-pipelines.md) com atividade de cópia que utiliza [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) e [DocumentDbCollectionSink](#azure-documentdb-copy-activity-type-properties).

exemplo de Olá copia dados de Blobs do Azure tooAzure Cosmos DB. Propriedades JSON de Olá utilizadas nestes exemplos são descritas nas secções seguintes exemplos de Olá.

**Serviço ligado do armazenamento de Blobs do Azure:**

```JSON
{
  "name": "StorageLinkedService",
  "properties": {
    "type": "AzureStorage",
    "typeProperties": {
      "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
    }
  }
}
```
**BD do Azure do Cosmos serviço ligado:**

```JSON
{
  "name": "CosmosDbLinkedService",
  "properties": {
    "type": "DocumentDb",
    "typeProperties": {
      "connectionString": "AccountEndpoint=<EndpointUrl>;AccountKey=<AccessKey>;Database=<Database>"
    }
  }
}
```
**Conjunto de dados de entrada Blob do Azure:**

```JSON
{
  "name": "PersonBlobTableIn",
  "properties": {
    "structure": [
      {
        "name": "Id",
        "type": "Int"
      },
      {
        "name": "FirstName",
        "type": "String"
      },
      {
        "name": "MiddleName",
        "type": "String"
      },
      {
        "name": "LastName",
        "type": "String"
      }
    ],
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "fileName": "input.csv",
      "folderPath": "docdb",
      "format": {
        "type": "TextFormat",
        "columnDelimiter": ",",
        "nullValue": "NULL"
      }
    },
    "external": true,
    "availability": {
      "frequency": "Day",
      "interval": 1
    }
  }
}
```
**BD do Azure do Cosmos o conjunto de dados de saída:**

exemplo de Olá copia a recolha de dados tooa com o nome "Pessoa".

```JSON
{
  "name": "PersonCosmosDbTableOut",
  "properties": {
    "structure": [
      {
        "name": "Id",
        "type": "Int"
      },
      {
        "name": "Name.First",
        "type": "String"
      },
      {
        "name": "Name.Middle",
        "type": "String"
      },
      {
        "name": "Name.Last",
        "type": "String"
      }
    ],
    "type": "DocumentDbCollection",
    "linkedServiceName": "CosmosDbLinkedService",
    "typeProperties": {
      "collectionName": "Person"
    },
    "availability": {
      "frequency": "Day",
      "interval": 1
    }
  }
}
```
seguinte Olá pipeline copia dados de Blobs do Azure toohello coleção de pessoa em Olá BD do Cosmos. Como parte da Olá de atividade de cópia de Olá foram especificados conjuntos de dados de entrada e de saída.

```JSON
{
  "name": "BlobToDocDbPipeline",
  "properties": {
    "activities": [
      {
        "type": "Copy",
        "typeProperties": {
          "source": {
            "type": "BlobSource"
          },
          "sink": {
            "type": "DocumentDbCollectionSink",
            "nestingSeparator": ".",
            "writeBatchSize": 2,
            "writeBatchTimeout": "00:00:00"
          }
          "translator": {
              "type": "TabularTranslator",
              "ColumnMappings": "FirstName: Name.First, MiddleName: Name.Middle, LastName: Name.Last, BusinessEntityID: BusinessEntityID, PersonType: PersonType, NameStyle: NameStyle, title: aaaTitle, Suffix: Suffix, EmailPromotion: EmailPromotion, rowguid: rowguid, ModifiedDate: ModifiedDate"
          }
        },
        "inputs": [
          {
            "name": "PersonBlobTableIn"
          }
        ],
        "outputs": [
          {
            "name": "PersonCosmosDbTableOut"
          }
        ],
        "policy": {
          "concurrency": 1
        },
        "name": "CopyFromBlobToDocDb"
      }
    ],
    "start": "2015-04-14T00:00:00Z",
    "end": "2015-04-15T00:00:00Z"
  }
}
```
Se a entrada de BLOBs de exemplo de Olá é como

```
1,John,,Doe
```
Em seguida, Olá saída JSON na base de dados do Cosmos será como:

```JSON
{
  "Id": 1,
  "Name": {
    "First": "John",
    "Middle": null,
    "Last": "Doe"
  },
  "id": "a5e8595c-62ec-4554-a118-3940f4ff70b6"
}
```
BD do Cosmos do Azure é um arquivo de NoSQL para documentos JSON, onde são permitidas estruturas aninhadas. O Azure Data Factory permite que a hierarquia de toodenote do utilizador através de **nestingSeparator**, que é "." Neste exemplo. Com separador Olá, atividade de cópia de Olá irá gerar o objeto de "Name" Olá com elementos três subordinados too"Name.First primeiro, média e última, de acordo com", "Name.Middle" e "Name.Last" Olá definição de tabela.

## <a name="appendix"></a>Apêndice
1. **Pergunta:** Olá a atualização de suporte de atividade de cópia de registos existentes?

    **Resposta:** não.
2. **Pergunta:** como funciona uma repetição de um grau de BD do Cosmos tooAzure de cópia com já copiados registos?

    **Resposta:** se registos tem um campo de "ID" e a operação de cópia de Olá tenta tooinsert um registo com Olá mesmo ID de operação de cópia de Olá emite um erro.  
3. **Pergunta:** suporta Data Factory [intervalo ou criação de partições de dados com base em hash](../documentdb/documentdb-partition-data.md)?

    **Resposta:** não.
4. **Pergunta:** posso especificar mais do que uma coleção de BD do Cosmos do Azure para uma tabela?

    **Resposta:** não. Apenas uma coleção pode ser especificada neste momento.

## <a name="performance-and-tuning"></a>Desempenho e a otimização
Consulte [desempenho de atividade de cópia & otimização guia](data-factory-copy-activity-performance.md) toolearn sobre chave factors desse desempenho impacto de movimento de dados (atividade de cópia) no Azure Data Factory e várias formas toooptimize-lo.
