---
title: dados aaaMove Teradata utilizando o Azure Data Factory | Microsoft Docs
description: "Saiba mais sobre o conector Teradata para Olá serviço fábrica de dados que lhe permite mover dados de base de dados Teradata"
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 98eb76d8-5f3d-4667-b76e-e59ed3eea3ae
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jingwang
ms.openlocfilehash: 79153476157666463b499edaa7585adaf8ad3bee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-teradata-using-azure-data-factory"></a>Mover dados de Teradata utilizando o Azure Data Factory
Este artigo explica como toouse Olá atividade de cópia no Azure Data Factory toomove da base de dados um local Teradata. Baseia-se no Olá [atividades de movimentos de dados](data-factory-data-movement-activities.md) artigo, que apresenta uma descrição geral do movimento de dados com a atividade de cópia de Olá.

Pode copiar dados de um arquivo de dados do local Teradata dados arquivo tooany suportado sink. Para obter uma lista dos dados arquivos suportados como sinks pela atividade de cópia de Olá, consulte Olá [arquivos de dados suportados](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabela. Fábrica de dados atualmente suporta apenas mover tooother arquivos de dados de arquivo de dados de um de dados Teradata, mas não para mover dados de noutro arquivo de dados Teradata de tooa de arquivos de dados. 

## <a name="prerequisites"></a>Pré-requisitos
Fábrica de dados suporta a ligação origens de Teradata tooon local através de Olá Data Management Gateway. Consulte [mover dados entre localizações no local e nuvem](data-factory-move-data-between-onprem-and-cloud.md) toolearn artigo sobre o Data Management Gateway e instruções passo a passo sobre como configurar o gateway de Olá.

É necessário gateway, mesmo se hello Teradata estiver alojada numa VM do IaaS do Azure. Pode instalar o gateway de Olá num Olá mesma VM do IaaS como dados de Olá armazenar ou numa VM diferente desde como gateway Olá pode ligar toohello base de dados.

> [!NOTE]
> Consulte [resolver problemas de gateway](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) para dicas sobre/gateway de ligação de resolução de problemas relacionados com problemas.

## <a name="supported-versions-and-installation"></a>Versões suportadas e instalação
Para o Data Management Gateway tooconnect toohello base de dados Teradata, terá de tooinstall Olá [fornecedor de dados .NET para Teradata](http://go.microsoft.com/fwlink/?LinkId=278886) versão 14 ou acima no Olá mesmo sistema como Olá Data Management Gateway. Teradata versão 12 e posterior é suportado.

## <a name="getting-started"></a>Introdução
Pode criar um pipeline com uma atividade de cópia move os dados de um arquivo de dados no local Cassandra utilizando ferramentas diferentes/APIs. 

- Olá toocreate da forma mais fácil um pipeline está toouse Olá **Assistente para copiar**. Consulte [Tutorial: criar um pipeline com o Assistente para copiar](data-factory-copy-data-wizard-tutorial.md) para obter instruções sobre como criar um pipeline com o Assistente de cópia de dados Olá rápida. 
- Também pode utilizar Olá seguintes ferramentas toocreate um pipeline: **portal do Azure**, **Visual Studio**, **Azure PowerShell**, **modelo Azure Resource Manager** , **.NET API**, e **REST API**. Consulte [tutorial de atividade de cópia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para instruções passo a passo toocreate um pipeline com uma atividade de cópia. 

Se utilizar ferramentas de Olá ou APIs, execute Olá os seguintes passos toocreate um pipeline que move o arquivo de dados do tooa sink do arquivo de dados de uma origem de dados:

1. Criar **serviços ligados** fábrica de dados de tooyour de arquivos de dados de entrada e saída de toolink.
2. Criar **conjuntos de dados** toorepresent de entrada e saída de operação de cópia de dados para Olá. 
3. Criar um **pipeline** com uma atividade de cópia executa um conjunto de dados como entrada e um conjunto de dados como resultado. 

Quando utiliza o Assistente de Olá, definições de JSON para estas entidades do Data Factory (serviços ligados, conjuntos de dados e pipeline Olá) são criadas automaticamente para si. Ao utilizar ferramentas/APIs (exceto .NET API), é possível definir estas entidades do Data Factory utilizando o formato JSON Olá.  Para um exemplo com definições de JSON para entidades do Data Factory que são utilizados toocopy dados a partir de um arquivo de dados Teradata no local, consulte [exemplo JSON: copiar dados de Teradata tooAzure Blob](#json-example-copy-data-from-teradata-to-azure-blob) secção deste artigo. 

Olá seguintes secções fornece detalhes sobre as propriedades JSON que são utilizados toodefine arquivo de dados do Data Factory entidades tooa específico Teradata:

## <a name="linked-service-properties"></a>Propriedades de serviço ligado
Olá, a tabela seguinte fornece uma descrição do serviço do JSON elementos específicos tooTeradata ligado.

| Propriedade | Descrição | Necessário |
| --- | --- | --- |
| tipo |a propriedade de tipo Olá tem de ser definida: **OnPremisesTeradata** |Sim |
| servidor |Nome do servidor de Teradata Olá. |Sim |
| authenticationType |Tipo de autenticação utilizado a base de dados Teradata de toohello tooconnect. Os valores possíveis são: anónimo, básico e Windows. |Sim |
| o nome de utilizador |Especifique o nome de utilizador se estiver a utilizar autenticação básica ou do Windows. |Não |
| palavra-passe |Especifique a palavra-passe da conta de utilizador de Olá especificado para nome de utilizador Olá. |Não |
| gatewayName |Nome do gateway de Olá que Olá serviço Data Factory deve utilizar a base de dados do tooconnect toohello no local Teradata. |Sim |

## <a name="dataset-properties"></a>Propriedades do conjunto de dados
Para uma lista completa das secções & Propriedades disponíveis para definir os conjuntos de dados, consulte Olá [criar conjuntos de dados](data-factory-create-datasets.md) artigo. As secções, tais como a estrutura, a disponibilidade e a política de um conjunto de dados JSON são semelhantes para todos os tipos de conjunto de dados (SQL do Azure, Azure blob, tabela do Azure, etc.).

Olá **typeProperties** secção é diferente para cada tipo de conjunto de dados e fornece informações sobre a localização de Olá dos dados de Olá no arquivo de dados de Olá. Atualmente, existem sem propriedades de tipo suportadas para o conjunto de dados do Olá Teradata.

## <a name="copy-activity-properties"></a>Propriedades da atividade de cópia
Para uma lista completa das secções & Propriedades disponíveis para definir as atividades, consulte Olá [criar Pipelines](data-factory-create-pipelines.md) artigo. Propriedades, tais como o nome, descrição e de saída, tabelas e as políticas estão disponíveis para todos os tipos de atividades.

Enquanto, propriedades disponíveis na secção de typeProperties Olá da atividade de Olá variar de acordo com cada tipo de atividade. Para a atividade de cópia, podem variam consoante os tipos de origens e sinks Olá.

Quando a origem de Olá é do tipo **RelationalSource** (que inclui Teradata), Olá seguintes propriedades está disponível no **typeProperties** secção:

| Propriedade | Descrição | Valores permitidos | Necessário |
| --- | --- | --- | --- |
| consulta |Utilize Olá consulta personalizada tooread dados. |Cadeia de consulta SQL. Por exemplo: selecionar * de MyTable. |Sim |

### <a name="json-example-copy-data-from-teradata-tooazure-blob"></a>Exemplo JSON: copiar dados de Teradata tooAzure Blob
Olá exemplo a seguir fornece definições JSON de exemplo que pode utilizar toocreate um pipeline utilizando [portal do Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) ou [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) ou [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md). Estes mostram como toocopy dados Teradata tooAzure Blob Storage. No entanto, os dados podem ser copiado tooany de Olá sinks indicado [aqui](data-factory-data-movement-activities.md#supported-data-stores-and-formats) utilizando Olá atividade de cópia no Azure Data Factory.   

exemplo de Olá tem Olá seguintes entidades da fábrica de dados:

1. Um serviço ligado do tipo [OnPremisesTeradata](#linked-service-properties).
2. Um serviço ligado do tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
3. Uma entrada [dataset](data-factory-create-datasets.md) do tipo [RelationalTable](#dataset-properties).
4. Uma saída [dataset](data-factory-create-datasets.md) do tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
5. Olá [pipeline](data-factory-create-pipelines.md) com atividade de cópia que utiliza [RelationalSource](#copy-activity-properties) e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).

exemplo de Olá copia dados a partir de um resultado da consulta num blob de tooa de base de dados Teradata a cada hora. Propriedades JSON de Olá utilizadas nestes exemplos são descritas nas secções seguintes exemplos de Olá.

Como primeiro passo, o programa de configuração Olá o data management gateway. instruções de Olá estão em Olá [mover dados entre localizações no local e nuvem](data-factory-move-data-between-onprem-and-cloud.md) artigo.

**Teradata serviço ligado:**

```json
{
    "name": "OnPremTeradataLinkedService",
    "properties": {
        "type": "OnPremisesTeradata",
        "typeProperties": {
            "server": "<server>",
            "authenticationType": "<authentication type>",
            "username": "<username>",
            "password": "<password>",
            "gatewayName": "<gatewayName>"
        }
    }
}
```

**Serviço ligado do armazenamento de Blobs do Azure:**

```json
{
    "name": "AzureStorageLinkedService",
    "properties": {
        "type": "AzureStorageLinkedService",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<AccountName>;AccountKey=<AccountKey>"
        }
    }
}
```

**Conjunto de dados entrado de Teradata:**

exemplo de Olá pressupõe que criou uma tabela "MyTable" Teradata e contém uma coluna chamada "timestamp" para dados de séries de tempo.

A definição "external": true informa o serviço do Data Factory Olá nessa tabela Olá é toohello externo fábrica de dados e não é produzida por uma atividade no factory de dados de Olá.

```json
{
    "name": "TeradataDataSet",
    "properties": {
        "published": false,
        "type": "RelationalTable",
        "linkedServiceName": "OnPremTeradataLinkedService",
        "typeProperties": {
        },
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

```json
{
    "name": "AzureBlobTeradataDataSet",
    "properties": {
        "published": false,
        "location": {
            "type": "AzureBlobLocation",
            "folderPath": "mycontainer/teradata/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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
            ],
            "linkedServiceName": "AzureStorageLinkedService"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```
**Pipeline com atividade de cópia:**

Olá pipeline contém uma atividade de cópia é configurado toouse Olá conjuntos de dados de entrada e de saída e é agendada toorun hora a hora. No pipeline de Olá definição JSON, Olá **origem** tipo está definido demasiado**RelationalSource** e **sink** tipo está definido demasiado**BlobSink**. consulta SQL Olá especificada para Olá **consulta** propriedade seleciona dados Olá Olá passado toocopy de hora.

```json
{
    "name": "CopyTeradataToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "RelationalSource",
                        "query": "$$Text.Format('select * from MyTable where timestamp >= \\'{0:yyyy-MM-ddTHH:mm:ss}\\' AND timestamp < \\'{1:yyyy-MM-ddTHH:mm:ss}\\'', SliceStart, SliceEnd)"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "TeradataDataSet"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobTeradataDataSet"
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
                "name": "TeradataToBlob"
            }
        ],
        "start": "2014-06-01T18:00:00Z",
        "end": "2014-06-01T19:00:00Z",
        "isPaused": false
    }
}
```
## <a name="type-mapping-for-teradata"></a>Mapeamento de tipos para Teradata
Tal como mencionado na Olá [atividades de movimentos de dados](data-factory-data-movement-activities.md) artigo, Olá atividade de cópia executa conversões de tipo automática dos tipos de toosink de tipos de origem com Olá seguir abordagem de passo 2:

1. Converter do tipo de too.NET de tipos de origem nativo
2. Converter do tipo de sink de toonative de tipo .NET

Quando move dados tooTeradata, hello mapeamentos seguintes são utilizados nas Teradata tipo too.NET tipo.

| Tipo de base de dados Teradata | Tipo de .NET framework |
| --- | --- |
| char |Cadeia |
| CLOB |Cadeia |
| Gráfico |Cadeia |
| VarChar |Cadeia |
| VarGraphic |Cadeia |
| Blobs |Byte] |
| Bytes |Byte] |
| VarByte |Byte] |
| BigInt |Int64 |
| ByteInt |Int16 |
| Decimal |Decimal |
| duplo |duplo |
| Número inteiro |Int32 |
| Número |duplo |
| SmallInt |Int16 |
| Data |DateTime |
| Hora |TimeSpan |
| Período de tempo com fuso horário |Cadeia |
| Timestamp |DateTime |
| Timestamp com o fuso horário |DateTimeOffset |
| Dia de intervalo |TimeSpan |
| Intervalo dia tooHour |TimeSpan |
| Intervalo dia tooMinute |TimeSpan |
| Intervalo dia tooSecond |TimeSpan |
| Hora de intervalo |TimeSpan |
| Intervalo hora tooMinute |TimeSpan |
| Intervalo hora tooSecond |TimeSpan |
| Minuto do intervalo |TimeSpan |
| TooSecond minuto do intervalo |TimeSpan |
| Intervalo segundo |TimeSpan |
| Intervalo ano |Cadeia |
| Intervalo ano tooMonth |Cadeia |
| Mês do intervalo |Cadeia |
| Period(Date) |Cadeia |
| Period(Time) |Cadeia |
| Período (Time com fuso horário) |Cadeia |
| Period(Timestamp) |Cadeia |
| Período (Timestamp com o fuso horário) |Cadeia |
| XML |Cadeia |

## <a name="map-source-toosink-columns"></a>Mapear colunas toosink de origem
toolearn sobre mapeamento as colunas na origem toocolumns de conjunto de dados no conjunto de dados dependente, consulte [mapeamento de colunas do conjunto de dados no Azure Data Factory](data-factory-map-columns.md).

## <a name="repeatable-read-from-relational-sources"></a>Repetíveis leitura a partir de origens relacionais
Quando copiar dados de arquivos de dados relacional, manter a repetibilidade em mente tooavoid resultados inesperados. No Azure Data Factory, pode voltar a executar um setor manualmente. Também pode configurar a política de repetição para um conjunto de dados para que um setor será novamente executado quando ocorre uma falha. Quando um setor é voltar a executar qualquer forma, terá de toomake certificar-se de que Olá mesmos dados é de leitura como não independentemente do número de vezes que um setor é executado. Consulte [Repeatable ler a partir de origens relacionais](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).

## <a name="performance-and-tuning"></a>Desempenho e a otimização
Consulte [desempenho de atividade de cópia & otimização guia](data-factory-copy-activity-performance.md) toolearn sobre chave factors desse desempenho impacto de movimento de dados (atividade de cópia) no Azure Data Factory e várias formas toooptimize-lo.
