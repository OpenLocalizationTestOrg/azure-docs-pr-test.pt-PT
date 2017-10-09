---
title: dados de aaaMove de origens de OData | Microsoft Docs
description: Saiba mais sobre como origens utilizando o Azure Data Factory de dados de toomove de OData.
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: de28fa56-3204-4546-a4df-21a21de43ed7
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/04/2017
ms.author: jingwang
ms.openlocfilehash: 328efe4fd274fb3e54c1d2f209e4614c77c1ff37
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-a-odata-source-using-azure-data-factory"></a>Mover dados de origem do OData utilizando o Azure Data Factory
Este artigo explica como toouse Olá atividade de cópia em dados do Azure Data Factory toomove a partir de uma origem de OData. Baseia-se no Olá [atividades de movimentos de dados](data-factory-data-movement-activities.md) artigo, que apresenta uma descrição geral do movimento de dados com a atividade de cópia de Olá.

Pode copiar dados de um arquivo de dados do OData origem tooany suportado sink. Para obter uma lista dos dados arquivos suportados como sinks pela atividade de cópia de Olá, consulte Olá [arquivos de dados suportados](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabela. Fábrica de dados atualmente suporta apenas mover armazena os dados a partir de uma origem de OData tooother dados, mas não para mover dados de outros dados armazena tooan OData origem. 

## <a name="supported-versions-and-authentication-types"></a>Versões suportadas e tipos de autenticação
Este conector de OData suporta a versão de OData 3.0 e 4.0 e pode copiar dados a partir de ambos os cloud OData e origens de OData no local. Para Olá esta última opção, terá de tooinstall Olá Data Management Gateway. Consulte [mover dados entre no local e na nuvem](data-factory-move-data-between-onprem-and-cloud.md) artigo para obter detalhes sobre o Data Management Gateway.

Abaixo autenticação são suportados tipos:

* tooaccess **nuvem** feed de OData, pode utilizar anónimo, básico (nome de utilizador e palavra-passe), ou do Azure Active Directory baseado em autenticação OAuth.
* tooaccess **no local** feed de OData, pode utilizar anónimo, básico (nome de utilizador e palavra-passe), ou a autenticação do Windows.

## <a name="getting-started"></a>Introdução
Pode criar um pipeline com uma atividade de cópia move dados a partir de uma origem de OData utilizando ferramentas diferentes/APIs.

Olá toocreate da forma mais fácil um pipeline está toouse Olá **Assistente para copiar**. Consulte [Tutorial: criar um pipeline com o Assistente para copiar](data-factory-copy-data-wizard-tutorial.md) para obter instruções sobre como criar um pipeline com o Assistente de cópia de dados Olá rápida.

Também pode utilizar Olá seguintes ferramentas toocreate um pipeline: **portal do Azure**, **Visual Studio**, **Azure PowerShell**, **modelo Azure Resource Manager** , **.NET API**, e **REST API**. Consulte [tutorial de atividade de cópia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para instruções passo a passo toocreate um pipeline com uma atividade de cópia. 

Se utilizar ferramentas de Olá ou APIs, execute Olá os seguintes passos toocreate um pipeline que move o arquivo de dados do tooa sink do arquivo de dados de uma origem de dados: 

1. Criar **serviços ligados** fábrica de dados de tooyour de arquivos de dados de entrada e saída de toolink.
2. Criar **conjuntos de dados** toorepresent de entrada e saída de operação de cópia de dados para Olá. 
3. Criar um **pipeline** com uma atividade de cópia executa um conjunto de dados como entrada e um conjunto de dados como resultado. 

Quando utiliza o Assistente de Olá, definições de JSON para estas entidades do Data Factory (serviços ligados, conjuntos de dados e pipeline Olá) são criadas automaticamente para si. Ao utilizar ferramentas/APIs (exceto .NET API), é possível definir estas entidades do Data Factory utilizando o formato JSON Olá.  Para um exemplo com definições de JSON para entidades do Data Factory que são utilizados toocopy dados de uma origem de OData, consulte [exemplo JSON: copiar dados de OData origem tooAzure Blob](#json-example-copy-data-from-odata-source-to-azure-blob) secção deste artigo. 

Olá seguintes secções fornece detalhes sobre as propriedades JSON que são utilizados toodefine Data Factory entidades tooOData específico origem:

## <a name="linked-service-properties"></a>Propriedades do serviço ligadas
Olá, a tabela seguinte fornece uma descrição do serviço do JSON elementos específicos tooOData ligado.

| Propriedade | Descrição | Necessário |
| --- | --- | --- |
| tipo |a propriedade de tipo Olá tem de ser definida: **OData** |Sim |
| URL |URL de Olá serviço OData. |Sim |
| authenticationType |Tipo de autenticação utilizado tooconnect toohello OData origem. <br/><br/> Para a nuvem OData, os valores possíveis são anónimo, básico e OAuth (tenha em atenção o suporte do Azure Data Factory atualmente, apenas do Azure Active Directory com base em OAuth). <br/><br/> De OData no local, os valores possíveis são anónimo, básico e Windows. |Sim |
| o nome de utilizador |Especifique o nome de utilizador se estiver a utilizar autenticação básica. |Sim (apenas se estiver a utilizar autenticação básica) |
| palavra-passe |Especifique a palavra-passe da conta de utilizador de Olá especificado para nome de utilizador Olá. |Sim (apenas se estiver a utilizar autenticação básica) |
| authorizedCredential |Se estiver a utilizar o OAuth, clique em **autorizar** button hello Assistente de cópia do Data Factory ou Editor e introduza as credenciais, em seguida, o valor desta propriedade Olá será gerado automaticamente. |Sim (apenas se estiver a utilizar autenticação OAuth) |
| gatewayName |Nome do gateway de Olá que Olá serviço Data Factory deve utilizar o serviço OData do tooconnect toohello no local. Especifique apenas se estiver a copiar dados a partir da origem de OData no local. |Não |

### <a name="using-basic-authentication"></a>Utilizar a autenticação básica
```json
{
    "name": "inputLinkedService",
    "properties":
    {
        "type": "OData",
            "typeProperties":
        {
            "url": "http://services.odata.org/OData/OData.svc",
            "authenticationType": "Basic",
            "username": "username",
            "password": "password"
        }
    }
}
```

### <a name="using-anonymous-authentication"></a>Autenticação anónima
```json
{
    "name": "ODataLinkedService",
        "properties":
    {
        "type": "OData",
        "typeProperties":
        {
            "url": "http://services.odata.org/OData/OData.svc",
            "authenticationType": "Anonymous"
        }
    }
}
```

### <a name="using-windows-authentication-accessing-on-premises-odata-source"></a>Através da autenticação do Windows aceder à origem de OData no local
```json
{
    "name": "inputLinkedService",
    "properties":
    {
        "type": "OData",
            "typeProperties":
        {
            "url": "<endpoint of on-premises OData source e.g. Dynamics CRM>",
            "authenticationType": "Windows",
            "username": "domain\\user",
            "password": "password",
            "gatewayName": "mygateway"
        }
    }
}
```

### <a name="using-oauth-authentication-accessing-cloud-odata-source"></a>Utilizando a autenticação do OAuth de nuvem ao aceder à origem de OData
```json
{
    "name": "inputLinkedService",
    "properties":
    {
        "type": "OData",
            "typeProperties":
        {
            "url": "<endpoint of cloud OData source e.g. https://<tenant>.crm.dynamics.com/XRMServices/2011/OrganizationData.svc>",
            "authenticationType": "OAuth",
            "authorizedCredential": "<auto generated by clicking hello Authorize button on UI>"
        }
    }
}
```

## <a name="dataset-properties"></a>Propriedades do conjunto de dados
Para uma lista completa das secções & Propriedades disponíveis para definir os conjuntos de dados, consulte Olá [criar conjuntos de dados](data-factory-create-datasets.md) artigo. As secções, tais como a estrutura, a disponibilidade e a política de um conjunto de dados JSON são semelhantes para todos os tipos de conjunto de dados (SQL do Azure, Azure blob, tabela do Azure, etc.).

Olá **typeProperties** secção é diferente para cada tipo de conjunto de dados e fornece informações sobre a localização de Olá dos dados de Olá no arquivo de dados de Olá. Olá typeProperties secção para o conjunto de dados do tipo **ODataResource** (que inclui o conjunto de dados do OData) tem Olá seguintes propriedades

| Propriedade | Descrição | Necessário |
| --- | --- | --- |
| Caminho |Caminho toohello recursos de OData |Não |

## <a name="copy-activity-properties"></a>Propriedades da atividade de cópia
Para uma lista completa das secções & Propriedades disponíveis para definir as atividades, consulte Olá [criar Pipelines](data-factory-create-pipelines.md) artigo. Propriedades, tais como o nome, descrição e de saída, tabelas e política estão disponíveis para todos os tipos de atividades.

As propriedades disponíveis na secção de typeProperties Olá da atividade de Olá no Olá por outro lado variar de acordo com cada tipo de atividade. Para a atividade de cópia, podem variam consoante os tipos de origens e sinks Olá.

Quando a origem é do tipo **RelationalSource** (que inclui OData) na secção typeProperties, estão disponível Olá seguintes propriedades:

| Propriedade | Descrição | Exemplo | Necessário |
| --- | --- | --- | --- |
| consulta |Utilize Olá consulta personalizada tooread dados. |"? $select = o nome, descrição & $top = 5" |Não |

## <a name="type-mapping-for-odata"></a>Mapeamento de tipos de OData
Tal como mencionado na Olá [atividades de movimentos de dados](data-factory-data-movement-activities.md) artigo, a atividade de cópia realiza conversões de tipo automática dos tipos de toosink de tipos de origem com Olá abordagem de dois passos a seguir.

1. Converter do tipo de too.NET de tipos de origem nativo
2. Converter do tipo de sink de toonative de tipo .NET

Quando mover dados de OData, hello mapeamentos seguintes são utilizados do tipo de too.NET de tipos de OData.

| Tipo de dados de OData | Tipo .NET |
| --- | --- |
| Edm.Binary |Byte] |
| Edm.Boolean |bool |
| Edm.Byte |Byte] |
| Edm.DateTime |DateTime |
| Edm.Decimal |Decimal |
| Edm.Double |duplo |
| Edm.Single |Único |
| Edm.Guid |GUID |
| Edm.Int16 |Int16 |
| Edm.Int32 |Int32 |
| Edm.Int64 |Int64 |
| Edm.SByte |Int16 |
| Edm.String |Cadeia |
| Edm.Time |TimeSpan |
| Edm.DateTimeOffset |DateTimeOffset |

> [!Note]
> Por exemplo, tipos de dados complexos de OData objeto não são suportadas.

## <a name="json-example-copy-data-from-odata-source-tooazure-blob"></a>Exemplo JSON: copiar dados de OData origem tooAzure Blob
Neste exemplo fornece definições JSON de exemplo que pode utilizar toocreate um pipeline utilizando [portal do Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) ou [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) ou [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md). Estes mostram como tooan Blob Storage do Azure da origem de dados de toocopy de OData. No entanto, os dados podem ser copiado tooany de Olá sinks indicado [aqui](data-factory-data-movement-activities.md#supported-data-stores-and-formats) utilizando Olá atividade de cópia no Azure Data Factory. exemplo de Olá tem Olá seguintes entidades do Data Factory:

1. Um serviço ligado do tipo [OData](#linked-service-properties).
2. Um serviço ligado do tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
3. Uma entrada [dataset](data-factory-create-datasets.md) do tipo [ODataResource](#dataset-properties).
4. Uma saída [dataset](data-factory-create-datasets.md) do tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
5. A [pipeline](data-factory-create-pipelines.md) com atividade de cópia que utiliza [RelationalSource](#copy-activity-properties) e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).

exemplo de Olá copia dados da consulta em relação a um tooan de origem OData BLOBs do Azure a cada hora. Propriedades JSON de Olá utilizadas nestes exemplos são descritas nas secções seguintes exemplos de Olá.

**Serviço ligado de OData:** neste exemplo Olá, utiliza a autenticação anónima. Consulte [serviço ligado de OData](#linked-service-properties) secção para diferentes tipos de autenticação, pode utilizar.

```json
{
    "name": "ODataLinkedService",
        "properties":
    {
        "type": "OData",
            "typeProperties":
        {
            "url": "http://services.odata.org/OData/OData.svc",
            "authenticationType": "Anonymous"
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

**Conjunto de dados entrado de OData:**

A definição "external": "true" informa serviço do Data Factory Olá esse conjunto de dados de Olá é toohello externo fábrica de dados e não é produzido por uma atividade no factory de dados de Olá.

```json
{
    "name": "ODataDataset",
    "properties":
    {
        "type": "ODataResource",
        "typeProperties":
        {
                "path": "Products"
        },
        "linkedServiceName": "ODataLinkedService",
        "structure": [],
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "retryInterval": "00:01:00",
            "retryTimeout": "00:10:00",
            "maximumRetry": 3                
        }
    }
}
```

Especificar **caminho** no conjunto de dados de Olá definição é opcional.

**Conjunto de dados de saída do Blob do Azure:**

São escritos dados no blob tooa de novo a cada hora (frequência: hora, intervalo: 1). caminho da pasta Olá para BLOBs Olá dinamicamente é avaliado com base na hora de início de Olá do setor de Olá que está a ser processado. caminho da pasta Olá utiliza ano, mês, dia e horas partes Olá da hora de início.

```json
{
    "name": "AzureBlobODataDataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/odata/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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


**Atividade de cópia num pipeline com a origem de OData e o sink de Blob:**

Olá pipeline contém uma atividade de cópia é configurado toouse Olá conjuntos de dados de entrada e de saída e é agendada toorun a cada hora. No pipeline de Olá definição JSON, Olá **origem** tipo está definido demasiado**RelationalSource** e **sink** tipo está definido demasiado**BlobSink**. consulta SQL Olá especificada para Olá **consulta** propriedade seleciona os dados (mais recentes) mais recentes de Olá a partir da origem de OData Olá.

```json
{
    "name": "CopyODataToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "RelationalSource",
                        "query": "?$select=Name, Description&$top=5",
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "ODataDataSet"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobODataDataSet"
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
                "name": "ODataToBlob"
            }
        ],
        "start": "2017-02-01T18:00:00Z",
        "end": "2017-02-03T19:00:00Z"
    }
}
```

Especificar **consulta** no pipeline de Olá definição é opcional. Olá **URL** é que o serviço do Data Factory Olá utiliza dados tooretrieve: URL especificado no Olá serviço ligado (obrigatório) + caminho especificado no conjunto de dados Olá (opcional) + consultar no pipeline de Olá (opcional).


### <a name="type-mapping-for-odata"></a>Mapeamento de tipos de OData
Tal como mencionado na Olá [atividades de movimentos de dados](data-factory-data-movement-activities.md) artigo, a atividade de cópia realiza conversões de tipo automática dos tipos de toosink de tipos de origem com Olá seguir abordagem de passo 2:

1. Converter do tipo de too.NET de tipos de origem nativo
2. Converter do tipo de sink de toonative de tipo .NET

Quando mover dados de arquivos de dados de OData, tipos de dados de OData são tipos de too.NET mapeada.

## <a name="map-source-toosink-columns"></a>Mapear colunas toosink de origem
toolearn sobre mapeamento as colunas na origem toocolumns de conjunto de dados no conjunto de dados dependente, consulte [mapeamento de colunas do conjunto de dados no Azure Data Factory](data-factory-map-columns.md).

## <a name="repeatable-read-from-relational-sources"></a>Repetíveis leitura a partir de origens relacionais
Quando copiar dados de arquivos de dados relacional, manter a repetibilidade em mente tooavoid resultados inesperados. No Azure Data Factory, pode voltar a executar um setor manualmente. Também pode configurar a política de repetição para um conjunto de dados para que um setor será novamente executado quando ocorre uma falha. Quando um setor é voltar a executar qualquer forma, terá de toomake certificar-se de que Olá mesmos dados é de leitura como não independentemente do número de vezes que um setor é executado. Consulte [Repeatable ler a partir de origens relacionais](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).

## <a name="performance-and-tuning"></a>Desempenho e a otimização
Consulte [desempenho de atividade de cópia & otimização guia](data-factory-copy-activity-performance.md) toolearn sobre chave factors desse desempenho impacto de movimento de dados (atividade de cópia) no Azure Data Factory e várias formas toooptimize-lo.
