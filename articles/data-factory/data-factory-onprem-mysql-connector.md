---
title: dados aaaMove MySQL utilizando o Azure Data Factory | Microsoft Docs
description: Saiba mais sobre como dados toomove MySQL da base de dados utilizando o Azure Data Factory.
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 452f4fce-9eb5-40a0-92f8-1e98691bea4c
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: jingwang
ms.openlocfilehash: 3ffe969e42ce1a54b265c4739df43fdc594ea891
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-mysql-using-azure-data-factory"></a>Mover dados de MySQL utilizando o Azure Data Factory
Este artigo explica como toouse Olá atividade de cópia em dados do Azure Data Factory toomove a partir de uma base de dados MySQL no local. Baseia-se no Olá [atividades de movimentos de dados](data-factory-data-movement-activities.md) artigo, que apresenta uma descrição geral do movimento de dados com a atividade de cópia de Olá.

Pode copiar dados de um arquivo de dados do local MySQL dados arquivo tooany suportado sink. Para obter uma lista dos dados arquivos suportados como sinks pela atividade de cópia de Olá, consulte Olá [arquivos de dados suportados](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabela. Fábrica de dados atualmente suporta apenas mover tooother arquivos de dados de arquivo de dados de um de dados MySQL, mas não para mover dados de noutro arquivo de dados MySQL de tooan de arquivos de dados. 

## <a name="prerequisites"></a>Pré-requisitos
Serviço de fábrica de dados suporta origens de MySQL tooon local ao ligar utilizando Olá Data Management Gateway. Consulte [mover dados entre localizações no local e nuvem](data-factory-move-data-between-onprem-and-cloud.md) toolearn artigo sobre o Data Management Gateway e instruções passo a passo sobre como configurar o gateway de Olá.

É necessário gateway, mesmo se a base de dados MySQL Olá estiver alojada numa máquina virtual IaaS do Azure (VM). Pode instalar o gateway de Olá num Olá mesma VM como dados de Olá armazenar ou numa VM diferente desde como gateway Olá pode ligar toohello base de dados.

> [!NOTE]
> Consulte [resolver problemas de gateway](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) para dicas sobre/gateway de ligação de resolução de problemas relacionados com problemas.

## <a name="supported-versions-and-installation"></a>Versões suportadas e instalação
Para o Data Management Gateway tooconnect toohello base de dados MySQL, terá de tooinstall Olá [MySQL conector/Net para Microsoft Windows](https://dev.mysql.com/downloads/connector/net/) (versão 6.6.5 ou superior) Olá no mesmo sistema como Olá Data Management Gateway. O MySQL versão 5.1 e posterior é suportado.

> [!TIP]
> Se clicar em erro "Autenticação falhou porque a parte remota de Olá fechou fluxo de transporte Olá.", considere tooupgrade Olá versão de toohigher MySQL conector/Net.

## <a name="getting-started"></a>Introdução
Pode criar um pipeline com uma atividade de cópia move os dados de um arquivo de dados no local Cassandra utilizando ferramentas diferentes/APIs. 

- Olá toocreate da forma mais fácil um pipeline está toouse Olá **Assistente para copiar**. Consulte [Tutorial: criar um pipeline com o Assistente para copiar](data-factory-copy-data-wizard-tutorial.md) para obter instruções sobre como criar um pipeline com o Assistente de cópia de dados Olá rápida. 
- Também pode utilizar Olá seguintes ferramentas toocreate um pipeline: **portal do Azure**, **Visual Studio**, **Azure PowerShell**, **modelo Azure Resource Manager** , **.NET API**, e **REST API**. Consulte [tutorial de atividade de cópia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para instruções passo a passo toocreate um pipeline com uma atividade de cópia. 

Se utilizar ferramentas de Olá ou APIs, execute Olá os seguintes passos toocreate um pipeline que move o arquivo de dados do tooa sink do arquivo de dados de uma origem de dados:

1. Criar **serviços ligados** fábrica de dados de tooyour de arquivos de dados de entrada e saída de toolink.
2. Criar **conjuntos de dados** toorepresent de entrada e saída de operação de cópia de dados para Olá. 
3. Criar um **pipeline** com uma atividade de cópia executa um conjunto de dados como entrada e um conjunto de dados como resultado. 

Quando utiliza o Assistente de Olá, definições de JSON para estas entidades do Data Factory (serviços ligados, conjuntos de dados e pipeline Olá) são criadas automaticamente para si. Ao utilizar ferramentas/APIs (exceto .NET API), é possível definir estas entidades do Data Factory utilizando o formato JSON Olá.  Para um exemplo com definições de JSON para entidades do Data Factory que são utilizados toocopy dados a partir de um arquivo de dados MySQL no local, consulte [exemplo JSON: copiar dados de MySQL tooAzure Blob](#json-example-copy-data-from-mysql-to-azure-blob) secção deste artigo. 

Olá seguintes secções fornece detalhes sobre as propriedades JSON que são utilizados toodefine arquivo de dados do Data Factory entidades tooa específico MySQL:

## <a name="linked-service-properties"></a>Propriedades de serviço ligado
Olá, a tabela seguinte fornece uma descrição do serviço do JSON elementos específicos tooMySQL ligado.

| Propriedade | Descrição | Necessário |
| --- | --- | --- |
| tipo |a propriedade de tipo Olá tem de ser definida: **OnPremisesMySql** |Sim |
| servidor |Nome do servidor do Olá MySQL. |Sim |
| base de dados |Nome da base de dados MySQL Olá. |Sim |
| Esquema |Nome do esquema de Olá na base de dados de Olá. |Não |
| authenticationType |Tipo de autenticação utilizado toohello tooconnect de dados MySQL. Os valores possíveis são: `Basic`. |Sim |
| o nome de utilizador |Especifique a base de dados do utilizador nome tooconnect toohello MySQL. |Sim |
| palavra-passe |Especifique a palavra-passe da conta de utilizador de Olá que especificou. |Sim |
| gatewayName |Nome do gateway de Olá que Olá serviço Data Factory deve utilizar tooconnect toohello no local de dados MySQL. |Sim |

## <a name="dataset-properties"></a>Propriedades do conjunto de dados
Para uma lista completa das secções & Propriedades disponíveis para definir os conjuntos de dados, consulte Olá [criar conjuntos de dados](data-factory-create-datasets.md) artigo. As secções, tais como a estrutura, a disponibilidade e a política de um conjunto de dados JSON são semelhantes para todos os tipos de conjunto de dados (SQL do Azure, Azure blob, tabela do Azure, etc.).

Olá **typeProperties** secção é diferente para cada tipo de conjunto de dados e fornece informações sobre a localização de Olá dos dados de Olá no arquivo de dados de Olá. Olá typeProperties secção para o conjunto de dados do tipo **RelationalTable** (que inclui o conjunto de dados MySQL) tem Olá seguintes propriedades

| Propriedade | Descrição | Necessário |
| --- | --- | --- |
| tableName |Nome da tabela de Olá na instância de base de dados MySQL que o serviço ligado de Olá referenciada. |Não (se **consulta** de **RelationalSource** especificado) |

## <a name="copy-activity-properties"></a>Propriedades da atividade de cópia
Para uma lista completa das secções & Propriedades disponíveis para definir as atividades, consulte Olá [criar Pipelines](data-factory-create-pipelines.md) artigo. Propriedades, tais como o nome, descrição, tabelas de entrada e de saída, são as políticas estão disponíveis para todos os tipos de atividades.

Enquanto, propriedades disponíveis nos Olá **typeProperties** secção da atividade de Olá variar de acordo com cada tipo de atividade. Para a atividade de cópia, podem variam consoante os tipos de origens e sinks Olá.

Quando a origem de atividade de cópia é do tipo **RelationalSource** (que inclui o MySQL), na secção typeProperties, estão disponível Olá seguintes propriedades:

| Propriedade | Descrição | Valores permitidos | Necessário |
| --- | --- | --- | --- |
| consulta |Utilize Olá consulta personalizada tooread dados. |Cadeia de consulta SQL. Por exemplo: selecionar * de MyTable. |Não (se **tableName** de **dataset** especificado) |


## <a name="json-example-copy-data-from-mysql-tooazure-blob"></a>Exemplo JSON: copiar dados de MySQL tooAzure Blob
Neste exemplo fornece definições JSON de exemplo que pode utilizar toocreate um pipeline utilizando [portal do Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) ou [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) ou [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md). Mostra como toocopy dados a partir de um MySQL no local da base de dados tooan Blob Storage do Azure. No entanto, os dados podem ser copiado tooany de Olá sinks indicado [aqui](data-factory-data-movement-activities.md#supported-data-stores-and-formats) utilizando Olá atividade de cópia no Azure Data Factory.

> [!IMPORTANT]
> Este exemplo fornece fragmentos JSON. Não inclui instruções passo a passo para criar a fábrica de dados de Olá. Consulte [mover dados entre localizações no local e nuvem](data-factory-move-data-between-onprem-and-cloud.md) artigo para obter instruções passo a passo.

exemplo de Olá tem Olá seguintes entidades da fábrica de dados:

1. Um serviço ligado do tipo [OnPremisesMySql](data-factory-onprem-mysql-connector.md#linked-service-properties).
2. Um serviço ligado do tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
3. Uma entrada [dataset](data-factory-create-datasets.md) do tipo [RelationalTable](data-factory-onprem-mysql-connector.md#dataset-properties).
4. Uma saída [dataset](data-factory-create-datasets.md) do tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
5. A [pipeline](data-factory-create-pipelines.md) com atividade de cópia que utiliza [RelationalSource](data-factory-onprem-mysql-connector.md#copy-activity-properties) e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).

exemplo de Olá copia dados a partir de um resultado da consulta num blob de tooa de base de dados MySQL hora a hora. Propriedades JSON de Olá utilizadas nestes exemplos são descritas nas secções seguintes exemplos de Olá.

Como primeiro passo, o programa de configuração Olá o data management gateway. instruções de Olá estão em Olá [mover dados entre localizações no local e nuvem](data-factory-move-data-between-onprem-and-cloud.md) artigo.

**Serviço ligado do MySQL:**

```JSON
    {
      "name": "OnPremMySqlLinkedService",
      "properties": {
        "type": "OnPremisesMySql",
        "typeProperties": {
          "server": "<server name>",
          "database": "<database name>",
          "schema": "<schema name>",
          "authenticationType": "<authentication type>",
          "userName": "<user name>",
          "password": "<password>",
          "gatewayName": "<gateway>"
        }
      }
    }
```

**Serviço ligado do Storage do Azure:**

```JSON
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

**Conjunto de dados entrado de MySQL:**

exemplo de Olá pressupõe que criou uma tabela "MyTable" MySQL e contém uma coluna chamada "timestampcolumn" para dados de séries de tempo.

A definição "external": "true" informa serviço do Data Factory Olá nessa tabela Olá é toohello externo fábrica de dados e não é produzida por uma atividade no factory de dados de Olá.

```JSON
    {
        "name": "MySqlDataSet",
        "properties": {
            "published": false,
            "type": "RelationalTable",
            "linkedServiceName": "OnPremMySqlLinkedService",
            "typeProperties": {},
            "availability": {
                "frequency": "Hour",
                "interval": 1
            },
            "external": true,
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

**Conjunto de dados de saída do Blob do Azure:**

São escritos dados no blob tooa de novo a cada hora (frequência: hora, intervalo: 1). caminho da pasta Olá para BLOBs Olá dinamicamente é avaliado com base na hora de início de Olá do setor de Olá que está a ser processado. caminho da pasta Olá utiliza ano, mês, dia e horas partes Olá da hora de início.

```JSON
    {
        "name": "AzureBlobMySqlDataSet",
        "properties": {
            "type": "AzureBlob",
            "linkedServiceName": "AzureStorageLinkedService",
            "typeProperties": {
                "folderPath": "mycontainer/mysql/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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

**Pipeline com atividade de cópia:**

Olá pipeline contém uma atividade de cópia é configurado toouse Olá conjuntos de dados de entrada e de saída e é agendada toorun a cada hora. No pipeline de Olá definição JSON, Olá **origem** tipo está definido demasiado**RelationalSource** e **sink** tipo está definido demasiado**BlobSink**. consulta SQL Olá especificada para Olá **consulta** propriedade seleciona dados Olá Olá passado toocopy de hora.

```JSON
    {
        "name": "CopyMySqlToBlob",
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
                            "name": "MySqlDataSet"
                        }
                    ],
                    "outputs": [
                        {
                            "name": "AzureBlobMySqlDataSet"
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
                    "name": "MySqlToBlob"
                }
            ],
            "start": "2014-06-01T18:00:00Z",
            "end": "2014-06-01T19:00:00Z"
        }
    }
```


### <a name="type-mapping-for-mysql"></a>Mapeamento de tipo para o MySQL
Tal como mencionado na Olá [atividades de movimentos de dados](data-factory-data-movement-activities.md) artigo, a atividade de cópia realiza conversões de tipo automática dos tipos de toosink de tipos de origem com Olá abordagem de dois passos a seguir:

1. Converter do tipo de too.NET de tipos de origem nativo
2. Converter do tipo de sink de toonative de tipo .NET

Quando move dados tooMySQL, Olá mapeamentos seguintes são utilizados dos tipos de too.NET de tipos de MySQL.

| Tipo de base de dados MySQL | Tipo de .NET framework |
| --- | --- |
| bigint não assinado |Decimal |
| bigint |Int64 |
| bits |Decimal |
| blob |Byte] |
| bool |Valor booleano |
| char |Cadeia |
| Data |DateTime |
| DateTime |DateTime |
| Decimal |Decimal |
| precisão dupla |duplo |
| duplo |duplo |
| Enum |Cadeia |
| Número de vírgula flutuante |Único |
| Int não assinado |Int64 |
| Int |Int32 |
| número inteiro sem sinal |Int64 |
| número inteiro |Int32 |
| varbinary longo |Byte] |
| varchar longo |Cadeia |
| longblob |Byte] |
| LONGTEXT |Cadeia |
| mediumblob |Byte] |
| mediumint não assinado |Int64 |
| mediumint |Int32 |
| mediumtext |Cadeia |
| um valor numérico |Decimal |
| real |duplo |
| definir |Cadeia |
| smallint não assinado |Int32 |
| smallint |Int16 |
| Texto |Cadeia |
| hora |TimeSpan |
| carimbo de data/hora |DateTime |
| tinyblob |Byte] |
| tinyint não assinado |Int16 |
| tinyint |Int16 |
| tinytext |Cadeia |
| varchar |Cadeia |
| ano |Int |

## <a name="map-source-toosink-columns"></a>Mapear colunas toosink de origem
toolearn sobre mapeamento as colunas na origem toocolumns de conjunto de dados no conjunto de dados dependente, consulte [mapeamento de colunas do conjunto de dados no Azure Data Factory](data-factory-map-columns.md).

## <a name="repeatable-read-from-relational-sources"></a>Repetíveis leitura a partir de origens relacionais
Quando copiar dados de arquivos de dados relacional, manter a repetibilidade em mente tooavoid resultados inesperados. No Azure Data Factory, pode voltar a executar um setor manualmente. Também pode configurar a política de repetição para um conjunto de dados para que um setor será novamente executado quando ocorre uma falha. Quando um setor é voltar a executar qualquer forma, terá de toomake certificar-se de que Olá mesmos dados é de leitura como não independentemente do número de vezes que um setor é executado. Consulte [Repeatable ler a partir de origens relacionais](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).

## <a name="performance-and-tuning"></a>Desempenho e a otimização
Consulte [desempenho de atividade de cópia & otimização guia](data-factory-copy-activity-performance.md) toolearn sobre chave factors desse desempenho impacto de movimento de dados (atividade de cópia) no Azure Data Factory e várias formas toooptimize-lo.
