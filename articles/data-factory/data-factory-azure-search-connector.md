---
title: "índice de tooSearch aaaPush dados utilizando o Data Factory | Microsoft Docs"
description: "Saiba mais sobre como toopush dados tooAzure índice de pesquisa através do Azure Data Factory."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: f8d46e1e-5c37-4408-80fb-c54be532a4ab
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/04/2017
ms.author: jingwang
ms.openlocfilehash: f2d973d0a2c24d6448e2d59e37e24503aa433018
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="push-data-tooan-azure-search-index-by-using-azure-data-factory"></a>Push de índice de pesquisa do Azure tooan dados através da utilização do Azure Data Factory
Este artigo descreve como o índice de pesquisa de tooAzure de arquivo de dados de toopush do toouse Olá atividade de cópia de dados de origem suportada. Arquivos de dados de origem suportada estão listados na coluna de origem de Olá de Olá [suportados origens e sinks](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabela. Este artigo baseia-se Olá [atividades de movimentos de dados](data-factory-data-movement-activities.md) artigo, que apresenta uma descrição geral do movimento de dados com a atividade de cópia e combinações de arquivo de dados suportada.

## <a name="enabling-connectivity"></a>Ativar a conectividade
tooallow serviço Data Factory ligar o arquivo de dados no local tooan, instalar o Data Management Gateway no seu ambiente no local. Pode instalar o gateway num Olá mesmo computador que aloja os dados de origem Olá armazenar ou em tooavoid um computador separado competir para recursos com dados Olá arquivo.

Gateway de gestão de dados liga-se os serviços de toocloud de origens de dados no local de forma segura e gerida. Consulte [mover dados entre no local e na nuvem](data-factory-move-data-between-onprem-and-cloud.md) artigo para obter detalhes sobre o Data Management Gateway.

## <a name="getting-started"></a>Introdução
Pode criar um pipeline com uma atividade de cópia que envia dados a partir de um índice de pesquisa de tooAzure de arquivo de dados de origem utilizando ferramentas diferentes/APIs.

Olá toocreate da forma mais fácil um pipeline está toouse Olá **Assistente para copiar**. Consulte [Tutorial: criar um pipeline com o Assistente para copiar](data-factory-copy-data-wizard-tutorial.md) para obter instruções sobre como criar um pipeline com o Assistente de cópia de dados Olá rápida.

Também pode utilizar Olá seguintes ferramentas toocreate um pipeline: **portal do Azure**, **Visual Studio**, **Azure PowerShell**, **modelo Azure Resource Manager** , **.NET API**, e **REST API**. Consulte [tutorial de atividade de cópia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para instruções passo a passo toocreate um pipeline com uma atividade de cópia. 

Se utilizar ferramentas de Olá ou APIs, execute Olá os seguintes passos toocreate um pipeline que move o arquivo de dados do tooa sink do arquivo de dados de uma origem de dados: 

1. Criar **serviços ligados** fábrica de dados de tooyour de arquivos de dados de entrada e saída de toolink.
2. Criar **conjuntos de dados** toorepresent de entrada e saída de operação de cópia de dados para Olá. 
3. Criar um **pipeline** com uma atividade de cópia executa um conjunto de dados como entrada e um conjunto de dados como resultado. 

Quando utiliza o Assistente de Olá, definições de JSON para estas entidades do Data Factory (serviços ligados, conjuntos de dados e pipeline Olá) são criadas automaticamente para si. Ao utilizar ferramentas/APIs (exceto .NET API), é possível definir estas entidades do Data Factory utilizando o formato JSON Olá.  Para um exemplo com definições de JSON para entidades do Data Factory do índice de pesquisa utilizados toocopy dados tooAzure, consulte [exemplo JSON: copiar dados de índice de pesquisa no local do SQL Server tooAzure](#json-example-copy-data-from-on-premises-sql-server-to-azure-search-index) secção deste artigo. 

Olá seguintes secções fornece detalhes sobre as propriedades JSON que são utilizados toodefine Data Factory entidades específica tooAzure índice de pesquisa:

## <a name="linked-service-properties"></a>Propriedades de serviço ligado

Olá, a tabela seguinte fornece descrições para os elementos JSON que são o serviço de pesquisa do Azure ligado toohello específico.

| Propriedade | Descrição | Necessário |
| -------- | ----------- | -------- |
| tipo | a propriedade de tipo Olá tem de ser definida: **azuresearch, uma vez**. | Sim |
| URL | URL para Olá serviço da Azure Search. | Sim |
| key | Chave de administrador para Olá serviço da Azure Search. | Sim |

## <a name="dataset-properties"></a>Propriedades do conjunto de dados

Para uma lista completa das secções e as propriedades disponíveis para definir os conjuntos de dados, consulte Olá [criar conjuntos de dados](data-factory-create-datasets.md) artigo. As secções, tais como a estrutura, a disponibilidade e a política de um conjunto de dados JSON são semelhantes para todos os tipos de conjunto de dados. Olá **typeProperties** secção é diferente para cada tipo de conjunto de dados. secção Olá typeProperties para um conjunto de dados do tipo de Olá **AzureSearchIndex** tem Olá seguintes propriedades:

| Propriedade | Descrição | Necessário |
| -------- | ----------- | -------- |
| tipo | a propriedade de tipo Olá tem de ser definida demasiado**AzureSearchIndex**.| Sim |
| indexName | Nome do índice de pesquisa do Azure Olá. Fábrica de dados não criar o índice de Olá. índice de Olá tem de existir na Azure Search. | Sim |


## <a name="copy-activity-properties"></a>Propriedades da atividade de cópia
Para uma lista completa das secções e as propriedades disponíveis para definir as atividades, consulte Olá [Criar pipelines](data-factory-create-pipelines.md) artigo. Propriedades, tais como o nome, descrição, entrada e tabelas de saída e várias políticas estão disponíveis para todos os tipos de atividades. Enquanto, propriedades disponíveis na secção de typeProperties Olá variar de acordo com cada tipo de atividade. Para a atividade de cópia, podem variam consoante os tipos de origens e sinks Olá.

Para a atividade de cópia, quando o sink de Olá é do tipo de Olá **AzureSearchIndexSink**, na secção typeProperties, estão disponível Olá seguintes propriedades:

| Propriedade | Descrição | Valores permitidos | Necessário |
| -------- | ----------- | -------------- | -------- |
| WriteBehavior | Especifica se toomerge ou substituir quando um documento já existe no índice Olá. Consulte Olá [WriteBehavior propriedade](#writebehavior-property).| Intercalar (predefinição)<br/>Carregar| Não |
| WriteBatchSize | Carrega dados para o índice de pesquisa do Azure Olá quando o tamanho de memória intermédia de Olá atingir writeBatchSize. Consulte Olá [WriteBatchSize propriedade](#writebatchsize-property) para obter mais detalhes. | 1 too1, 000. Valor predefinido é 1000. | Não |

### <a name="writebehavior-property"></a>Propriedade de WriteBehavior
AzureSearchSink upserts ao escrever dados. Por outras palavras, ao escrever um documento, se a chave do documento Olá já existe no índice de pesquisa do Azure Olá, Azure Search atualizações documento existente Olá, em vez de gerar uma exceção de conflito.

Olá AzureSearchSink fornece Olá seguir dois upsert comportamentos (utilizando o SDK azuresearch, uma vez):

- **Intercalar**: combinar todas as colunas de Olá documento novo Olá com Olá um existente. Para colunas com um valor nulo no documento novo Olá, valor Olá Olá existente um é preservada.
- **Carregar**: substitui o documento novo Olá Olá já existente. Para colunas não especificadas no documento novo Olá, o valor de Olá é definido toonull se houver um valor não nulo documento existente Olá, ou não.

comportamento predefinido de Olá é **intercalar**.

### <a name="writebatchsize-property"></a>Propriedade de WriteBatchSize
Serviço de pesquisa do Azure suporta documentos de escrita como um lote. Um lote pode conter 1 too1, 000 ações. Uma ação processa uma operação de intercalação/carregamento do documento tooperform Olá.

### <a name="data-type-support"></a>Suporte de tipo de dados
Olá seguinte tabela especifica se um tipo de dados de pesquisa do Azure é suportado ou não.

| Tipo de dados de pesquisa do Azure | Suportado no receptor de pesquisa do Azure |
| ---------------------- | ------------------------------ |
| Cadeia | S |
| Int32 | S |
| Int64 | S |
| duplo | S |
| Valor booleano | S |
| DataTimeOffset | S |
| Matriz de cadeia | N |
| GeographyPoint | N |

## <a name="json-example-copy-data-from-on-premises-sql-server-tooazure-search-index"></a>Exemplo JSON: copiar dados de índice de pesquisa de tooAzure de SQL Server no local

Olá seguinte exemplo mostra:

1.  Um serviço ligado do tipo [azuresearch, uma vez](#linked-service-properties).
2.  Um serviço ligado do tipo [OnPremisesSqlServer](data-factory-sqlserver-connector.md#linked-service-properties).
3.  Uma entrada [dataset](data-factory-create-datasets.md) do tipo [SqlServerTable](data-factory-sqlserver-connector.md#dataset-properties).
4.  Uma saída [dataset](data-factory-create-datasets.md) do tipo [AzureSearchIndex](#dataset-properties).
4.  A [pipeline](data-factory-create-pipelines.md) com uma atividade de cópia que utiliza [SqlSource](data-factory-sqlserver-connector.md#copy-activity-properties) e [AzureSearchIndexSink](#copy-activity-properties).

exemplo de Olá copia dados de séries de tempo hora a hora de um índice de pesquisa do Azure do tooan no local do SQL Server da base de dados. as propriedades de JSON Olá utilizadas neste exemplo são descritas nas secções seguintes exemplos de Olá.

Como primeiro passo, configure o gateway de gestão de dados de Olá no seu computador local. instruções de Olá estão em Olá [mover dados entre localizações no local e nuvem](data-factory-move-data-between-onprem-and-cloud.md) artigo.

**Serviço ligado de pesquisa do Azure:**

```JSON
{
    "name": "AzureSearchLinkedService",
    "properties": {
        "type": "AzureSearch",
        "typeProperties": {
            "url": "https://<service>.search.windows.net",
            "key": "<AdminKey>"
        }
    }
}
```

**Serviço ligado do SQL Server**

```JSON
{
  "Name": "SqlServerLinkedService",
  "properties": {
    "type": "OnPremisesSqlServer",
    "typeProperties": {
      "connectionString": "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=False;User ID=<username>;Password=<password>;",
      "gatewayName": "<gatewayname>"
    }
  }
}
```

**Conjunto de dados de entrada do SQL Server**

exemplo de Olá pressupõe que criou uma tabela "MyTable" no SQL Server e contém uma coluna chamada "timestampcolumn" para dados de séries de tempo. Pode consultar através de várias tabelas na Olá mesma base de dados com um único conjunto de dados, mas uma única tabela tem de ser utilizado para typeProperty tableName de Olá conjunto de dados.

A definição "external": "true" informa serviço Data Factory esse conjunto de dados de Olá é toohello externo fábrica de dados e não é produzido por uma atividade no factory de dados de Olá.

```JSON
{
  "name": "SqlServerDataset",
  "properties": {
    "type": "SqlServerTable",
    "linkedServiceName": "SqlServerLinkedService",
    "typeProperties": {
      "tableName": "MyTable"
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

**Conjunto de dados de saída de pesquisa do Azure:**

Olá exemplo cópias dados tooan índice da Azure Search com o nome **produtos**. Fábrica de dados não criar o índice de Olá. Olá tootest de exemplo, crie um índice com este nome. Criar o índice da Azure Search de Olá com Olá mesmo número de colunas que no conjunto de dados de entrada Olá. Novas entradas são adicionadas toohello o índice da Azure Search a cada hora.

```JSON
{
    "name": "AzureSearchIndexDataset",
    "properties": {
        "type": "AzureSearchIndex",
        "linkedServiceName": "AzureSearchLinkedService",
        "typeProperties" : {
            "indexName": "products",
        },
        "availability": {
            "frequency": "Minute",
            "interval": 15
        }
   }
}
```

**Atividade de cópia de um pipeline com a origem SQL e o sink de índice da Azure Search:**

Olá pipeline contém uma atividade de cópia é configurado toouse Olá conjuntos de dados de entrada e de saída e é agendada toorun a cada hora. No pipeline de Olá definição JSON, Olá **origem** tipo está definido demasiado**SqlSource** e **sink** tipo está definido demasiado**AzureSearchIndexSink**. consulta SQL Olá especificada para Olá **SqlReaderQuery** propriedade seleciona dados Olá Olá passado toocopy de hora.

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline for copy activity",
    "activities":[  
      {
        "name": "SqlServertoAzureSearchIndex",
        "description": "copy activity",
        "type": "Copy",
        "inputs": [
          {
            "name": " SqlServerInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureSearchIndexDataset"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "SqlSource",
            "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
          },
          "sink": {
            "type": "AzureSearchIndexSink"
          }
        },
       "scheduler": {
          "frequency": "Hour",
          "interval": 1
        },
        "policy": {
          "concurrency": 1,
          "executionPriorityOrder": "OldestFirst",
          "retry": 0,
          "timeout": "01:00:00"
        }
      }
     ]
   }
}
```

Se estiver a copiar dados de um arquivo de dados em nuvem na Azure Search, `executionLocation` propriedade é necessária. Olá fragmento JSON seguinte mostra as alterações de Olá necessária na atividade de cópia `typeProperties` como exemplo. Verifique [copiar dados entre os arquivos de dados de nuvem](data-factory-data-movement-activities.md#global) secção para os valores suportados e obter mais detalhes.

```JSON
"typeProperties": {
  "source": {
    "type": "BlobSource"
  },
  "sink": {
    "type": "AzureSearchIndexSink"
  },
  "executionLocation": "West US"
}
```


## <a name="copy-from-a-cloud-source"></a>Copiar de uma origem de nuvem
Se estiver a copiar dados de um arquivo de dados em nuvem na Azure Search, `executionLocation` propriedade é necessária. Olá fragmento JSON seguinte mostra as alterações de Olá necessária na atividade de cópia `typeProperties` como exemplo. Verifique [copiar dados entre os arquivos de dados de nuvem](data-factory-data-movement-activities.md#global) secção para os valores suportados e obter mais detalhes.

```JSON
"typeProperties": {
  "source": {
    "type": "BlobSource"
  },
  "sink": {
    "type": "AzureSearchIndexSink"
  },
  "executionLocation": "West US"
}
```

Também pode mapear colunas do conjunto de dados de origem toocolumns do conjunto de dados dependente na definição de atividade de cópia de Olá. Para obter mais informações, consulte [mapeamento de colunas do conjunto de dados no Azure Data Factory](data-factory-map-columns.md).

## <a name="performance-and-tuning"></a>Desempenho e otimização  
Consulte Olá [guia Otimização e de desempenho de atividade de cópia](data-factory-copy-activity-performance.md) toolearn sobre chave factors desse desempenho impacto de movimento de dados (atividade de cópia) e de várias formas toooptimize-lo.

## <a name="next-steps"></a>Passos seguintes
Consulte Olá seguintes artigos:

* [Tutorial de atividade de cópia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para obter instruções passo a passo para criar um pipeline com uma atividade de cópia.
