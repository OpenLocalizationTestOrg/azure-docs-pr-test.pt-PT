---
title: dados aaaMove Redshift Amazon utilizando o Data Factory | Microsoft Docs
description: Saiba mais sobre como dados toomove Redshift Amazon utilizando o Azure Data Factory.
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 01d15078-58dc-455c-9d9d-98fbdf4ea51e
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jingwang
ms.openlocfilehash: 2a097320734ebdd57282d250f7fdba35741777f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-amazon-redshift-using-azure-data-factory"></a>Mover dados de Redshift de Amazon utilizando o Azure Data Factory
Este artigo explica como toouse Olá atividade de cópia em dados do Azure Data Factory toomove Amazon Redshift. artigo de Olá baseia-se Olá [atividades de movimentos de dados](data-factory-data-movement-activities.md) artigo, que apresenta uma descrição geral do movimento de dados com a atividade de cópia de Olá. 

Pode copiar dados do arquivo de dados do Amazon Redshift tooany suportado sink. Para obter uma lista dos arquivos de dados suportados como sinks pela atividade de cópia de Olá, consulte [arquivos de dados suportados](data-factory-data-movement-activities.md#supported-data-stores-and-formats). Atualmente, a fábrica de dados suporta mover dados de arquivos de dados do Amazon Redshift tooother, mas não para mover dados de outra tooAmazon de arquivos de dados Redshift.

## <a name="prerequisites"></a>Pré-requisitos
* Se estiver a mover dados tooan arquivo de dados no local, instale [Data Management Gateway](data-factory-data-management-gateway.md) numa máquina no local. Em seguida, conceder Data Management Gateway (endereço IP da utilização da máquina de Olá) Olá tooAmazon Redshift cluster de acesso. Consulte [cluster de toohello de acesso de autorizar](http://docs.aws.amazon.com/redshift/latest/gsg/rs-gsg-authorize-cluster-access.html) para obter instruções.
* Se estiver a mover o arquivo de dados do Azure de tooan de dados, consulte o artigo [intervalos de IP de centro de dados do Azure](https://www.microsoft.com/download/details.aspx?id=41653) para endereço de IP de computação de Olá e intervalos de SQL Server utilizados pelo Olá centros de dados do Azure.

## <a name="getting-started"></a>Introdução
Pode criar um pipeline com uma atividade de cópia move dados a partir de uma origem de Amazon Redshift utilizando ferramentas diferentes/APIs.

Olá toocreate da forma mais fácil um pipeline está toouse Olá **Assistente para copiar**. Consulte [Tutorial: criar um pipeline com o Assistente para copiar](data-factory-copy-data-wizard-tutorial.md) para obter instruções sobre como criar um pipeline com o Assistente de cópia de dados Olá rápida.

Também pode utilizar Olá seguintes ferramentas toocreate um pipeline: **portal do Azure**, **Visual Studio**, **Azure PowerShell**, **modelo Azure Resource Manager** , **.NET API**, e **REST API**. Consulte [tutorial de atividade de cópia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para instruções passo a passo toocreate um pipeline com uma atividade de cópia. 

Se utilizar ferramentas de Olá ou APIs, execute Olá os seguintes passos toocreate um pipeline que move o arquivo de dados do tooa sink do arquivo de dados de uma origem de dados: 

1. Criar **serviços ligados** fábrica de dados de tooyour de arquivos de dados de entrada e saída de toolink.
2. Criar **conjuntos de dados** toorepresent de entrada e saída de operação de cópia de dados para Olá. 
3. Criar um **pipeline** com uma atividade de cópia executa um conjunto de dados como entrada e um conjunto de dados como resultado. 

Quando utiliza o Assistente de Olá, definições de JSON para estas entidades do Data Factory (serviços ligados, conjuntos de dados e pipeline Olá) são criadas automaticamente para si. Ao utilizar ferramentas/APIs (exceto .NET API), é possível definir estas entidades do Data Factory utilizando o formato JSON Olá.  Para um exemplo com definições de JSON para entidades do Data Factory que os dados de um arquivo de dados do Amazon Redshift toocopy utilizadas, consulte [exemplo JSON: copiar dados do Amazon Redshift tooAzure Blob](#json-example-copy-data-from-amazon-redshift-to-azure-blob) secção deste artigo. 

Olá seguintes secções fornece detalhes sobre as propriedades JSON que são utilizados toodefine Data Factory entidades específica tooAmazon Redshift: 

## <a name="linked-service-properties"></a>Propriedades de serviço ligado
Olá, a tabela seguinte fornece uma descrição para JSON elementos específico tooAmazon serviço Redshift ligado.

| Propriedade | Descrição | Necessário |
| --- | --- | --- |
| tipo |a propriedade de tipo Olá tem de ser definida: **AmazonRedshift**. |Sim |
| servidor |Nome anfitrião ou endereço IP do servidor de Amazon Redshift Olá. |Sim |
| porta |número de Olá de porta TCP de Olá Olá Amazon Redshift servidor utiliza toolisten para ligações de cliente. |Valor predefinido não,: 5439 |
| base de dados |Nome da base de dados do Olá Amazon Redshift. |Sim |
| o nome de utilizador |Nome de utilizador que tenha a base de dados do access toohello. |Sim |
| palavra-passe |Palavra-passe da conta de utilizador Olá. |Sim |

## <a name="dataset-properties"></a>Propriedades do conjunto de dados
Para uma lista completa das secções & Propriedades disponíveis para definir os conjuntos de dados, consulte Olá [criar conjuntos de dados](data-factory-create-datasets.md) artigo. As secções, tais como a estrutura, a disponibilidade e a política são semelhantes para todos os tipos de conjunto de dados (SQL do Azure, Azure blob, tabela do Azure, etc.).

Olá **typeProperties** secção é diferente para cada tipo de conjunto de dados. Fornece informações sobre a localização de Olá dos dados de Olá no arquivo de dados de Olá. Olá typeProperties secção para o conjunto de dados do tipo **RelationalTable** (que inclui o conjunto de dados do Amazon Redshift) tem Olá seguintes propriedades

| Propriedade | Descrição | Necessário |
| --- | --- | --- |
| tableName |Nome da tabela de Olá na base de dados do Amazon Redshift Olá pelo serviço ligado refere-se. |Não (se **consulta** de **RelationalSource** especificado) |

## <a name="copy-activity-properties"></a>Propriedades da atividade de cópia
Para uma lista completa das secções & Propriedades disponíveis para definir as atividades, consulte Olá [criar Pipelines](data-factory-create-pipelines.md) artigo. Propriedades, tais como o nome, descrição e de saída, tabelas e as políticas estão disponíveis para todos os tipos de atividades.

Enquanto, propriedades disponíveis nos Olá **typeProperties** secção da atividade de Olá variar de acordo com cada tipo de atividade. Para a atividade de cópia, podem variam consoante os tipos de origens e sinks Olá.

Quando a origem da atividade de cópia é do tipo **RelationalSource** (que inclui o Amazon Redshift), na secção typeProperties, estão disponível Olá seguintes propriedades:

| Propriedade | Descrição | Valores permitidos | Necessário |
| --- | --- | --- | --- |
| consulta |Utilize Olá consulta personalizada tooread dados. |Cadeia de consulta SQL. Por exemplo: selecionar * de MyTable. |Não (se **tableName** de **dataset** especificado) |

## <a name="json-example-copy-data-from-amazon-redshift-tooazure-blob"></a>Exemplo JSON: copiar dados do Amazon Redshift tooAzure Blob
Este exemplo mostra como toocopy dados a partir de um Redshift Amazon da base de dados tooan Blob Storage do Azure. No entanto, os dados podem ser copiados **diretamente** tooany de Olá sinks indicado [aqui](data-factory-data-movement-activities.md#supported-data-stores-and-formats) utilizando Olá atividade de cópia no Azure Data Factory.  

exemplo de Olá tem Olá seguintes entidades da fábrica de dados:

* Um serviço ligado do tipo [AmazonRedshift](#linked-service-properties).
* Um serviço ligado do tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
* Uma entrada [dataset](data-factory-create-datasets.md) do tipo [RelationalTable](#dataset-properties).
* Uma saída [dataset](data-factory-create-datasets.md) do tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
* A [pipeline](data-factory-create-pipelines.md) com atividade de cópia que utiliza [RelationalSource](#copy-activity-properties) e [BlobSink](data-factory-azure-blob-connector.md##copy-activity-properties).

exemplo de Olá copia dados a partir num resultado de consulta Amazon Redshift tooa blob a cada hora. Propriedades JSON de Olá utilizadas nestes exemplos são descritas nas secções seguintes exemplos de Olá.

**Serviço ligado do Amazon Redshift:**

```json
{
    "name": "AmazonRedshiftLinkedService",
    "properties":
    {
        "type": "AmazonRedshift",
        "typeProperties":
        {
            "server": "< hello IP address or host name of hello Amazon Redshift server >",
            "port": <hello number of hello TCP port that hello Amazon Redshift server uses toolisten for client connections.>,
            "database": "<hello database name of hello Amazon Redshift database>",
            "username": "<username>",
            "password": "<password>"
        }
    }
}
```

**Serviço ligado do Storage do Azure:**

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
**Conjunto de dados entrado de Amazon Redshift:**

Definição `"external": true` informa o serviço do Data Factory Olá esse conjunto de dados de Olá é toohello externo fábrica de dados e não é produzido por uma atividade no factory de dados de Olá. Defina um conjunto de dados de entrada que não é produzido por uma atividade no pipeline de Olá tootrue esta propriedade.

```json
{
    "name": "AmazonRedshiftInputDataset",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "AmazonRedshiftLinkedService",
        "typeProperties": {
            "tableName": "<Table name>"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```

**Conjunto de dados de saída do Blob do Azure:**

São escritos dados no blob tooa de novo a cada hora (frequência: hora, intervalo: 1). caminho da pasta Olá para BLOBs Olá dinamicamente é avaliado com base na hora de início de Olá do setor de Olá que está a ser processado. caminho da pasta Olá utiliza ano, mês, dia e horas partes Olá da hora de início.

```json
{
    "name": "AzureBlobOutputDataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/fromamazonredshift/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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

**Atividade de cópia de um pipeline com a origem de Azure Redshift (RelationalSource) e o sink de Blob:**

Olá pipeline contém uma atividade de cópia é configurado toouse Olá conjuntos de dados de entrada e de saída e é agendada toorun a cada hora. No pipeline de Olá definição JSON, Olá **origem** tipo está definido demasiado**RelationalSource** e **sink** tipo está definido demasiado**BlobSink**. consulta SQL Olá especificada para Olá **consulta** propriedade seleciona dados Olá Olá passado toocopy de hora.

```json
{
    "name": "CopyAmazonRedshiftToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "RelationalSource",
                        "query": "$$Text.Format('select * from MyTable where timestamp >= \\'{0:yyyy-MM-ddTHH:mm:ss}\\' AND timestamp < \\'{1:yyyy-MM-ddTHH:mm:ss}\\'', WindowStart, WindowEnd)"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "AmazonRedshiftInputDataset"
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
                "name": "AmazonRedshiftToBlob"
            }
        ],
        "start": "2014-06-01T18:00:00Z",
        "end": "2014-06-01T19:00:00Z"
    }
}
```
### <a name="type-mapping-for-amazon-redshift"></a>Mapeamento de tipo para o Amazon Redshift
Tal como mencionado na Olá [atividades de movimentos de dados](data-factory-data-movement-activities.md) artigo, a atividade de cópia realiza conversões de tipo automática dos tipos de toosink de tipos de origem com Olá abordagem de dois passos a seguir:

1. Converter do tipo de too.NET de tipos de origem nativo
2. Converter do tipo de sink de toonative de tipo .NET

Quando move dados tooAmazon Redshift, Olá seguintes mapeamentos é utilizada de tipos de too.NET Amazon Redshift tipos.

| Tipo de Redshift Amazon | .NET com base em tipo |
| --- | --- |
| SMALLINT |Int16 |
| NÚMERO INTEIRO |Int32 |
| BIGINT |Int64 |
| DECIMAL |Decimal |
| REAL |Único |
| PRECISÃO DUPLA |duplo |
| VALOR BOOLEANO |Cadeia |
| CHAR |Cadeia |
| VARCHAR |Cadeia |
| DATA |DateTime |
| TIMESTAMP |DateTime |
| TEXTO |Cadeia |

## <a name="map-source-toosink-columns"></a>Mapear colunas toosink de origem
toolearn sobre mapeamento as colunas na origem toocolumns de conjunto de dados no conjunto de dados dependente, consulte [mapeamento de colunas do conjunto de dados no Azure Data Factory](data-factory-map-columns.md).

## <a name="repeatable-read-from-relational-sources"></a>Repetíveis leitura a partir de origens relacionais
Quando copiar dados de arquivos de dados relacional, manter a repetibilidade em mente tooavoid resultados inesperados. No Azure Data Factory, pode voltar a executar um setor manualmente. Também pode configurar a política de repetição para um conjunto de dados para que um setor será novamente executado quando ocorre uma falha. Quando um setor é voltar a executar qualquer forma, terá de toomake certificar-se de que Olá mesmos dados é de leitura como não independentemente do número de vezes que um setor é executado. Consulte [Repeatable ler a partir de origens relacionais](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)

## <a name="performance-and-tuning"></a>Desempenho e a otimização
Consulte [desempenho de atividade de cópia & otimização guia](data-factory-copy-activity-performance.md) toolearn sobre chave factors desse desempenho impacto de movimento de dados (atividade de cópia) no Azure Data Factory e várias formas toooptimize-lo.

## <a name="next-steps"></a>Passos Seguintes
Consulte Olá seguintes artigos:

* [Tutorial de atividade de cópia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para obter instruções passo a passo para criar um pipeline com uma atividade de cópia.
