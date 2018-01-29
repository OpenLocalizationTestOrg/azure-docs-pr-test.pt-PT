---
title: Mover dados do Salesforce ao utilizar o Data Factory | Microsoft Docs
description: Saiba mais sobre como mover dados do Salesforce ao utilizar o Azure Data Factory.
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: dbe3bfd6-fa6a-491a-9638-3a9a10d396d1
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/10/2018
ms.author: jingwang
robots: noindex
ms.openlocfilehash: 9e678e947a686b5a672af13cb0f0e60b4a272de9
ms.sourcegitcommit: 9cc3d9b9c36e4c973dd9c9028361af1ec5d29910
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 01/23/2018
---
# <a name="move-data-from-salesforce-by-using-azure-data-factory"></a>Mover dados do Salesforce ao utilizar o Azure Data Factory
> [!div class="op_single_selector" title1="Select the version of Data Factory service you are using:"]
> * [Versão 1 - GA](data-factory-salesforce-connector.md)
> * [Versão 2 - Pré-visualização](../connector-salesforce.md)

> [!NOTE]
> Este artigo aplica-se à versão 1 do Data Factory, que está geralmente disponível (GA). Se estiver a utilizar a versão 2 do serviço do Data Factory, o que está em pré-visualização, consulte [conector do Salesforce no V2](../connector-salesforce.md).


Este artigo descreve como pode utilizar a atividade de cópia de um Azure data factory para copiar dados do Salesforce para qualquer arquivo de dados que está listado na coluna Sink no [suportados origens e sinks](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabela. Este artigo baseia-se a [atividades de movimentos de dados](data-factory-data-movement-activities.md) artigo, que apresenta uma descrição geral do movimento de dados com a atividade de cópia e combinações de arquivo de dados suportada.

O Azure Data Factory atualmente suporta apenas dados mover do Salesforce ao [sink arquivos de dados suportados](data-factory-data-movement-activities.md#supported-data-stores-and-formats), mas não suporte mover dados de outros dados armazena Salesforce.

## <a name="supported-versions"></a>Versões suportadas
Este conector suporta as seguintes edições do Salesforce: edição programador, edição Professional, Enterprise Edition ou edição ilimitado. E suporta a cópia de produção do Salesforce, sandbox e domínio personalizado.

## <a name="prerequisites"></a>Pré-requisitos
* Permissão de API tem de estar ativada. Consulte [como ativar o acesso à API no Salesforce pelo conjunto de permissões?](https://www.data2crm.com/migration/faqs/enable-api-access-salesforce-permission-set/)
* Para copiar dados do Salesforce aos arquivos de dados no local, tem de ter, pelo menos, 2.0 de Gateway de gestão de dados instalado no seu ambiente no local.

## <a name="salesforce-request-limits"></a>Limites de pedido do Salesforce
O Salesforce tem limites para o total de pedidos de API e pedidos de API em simultâneo. Tenha em atenção os seguintes pontos:

- Se o número de pedidos simultâneos excede o limite, limitação ocorre e verá falhas aleatórias.
- Se o número total de pedidos excede o limite, a conta do Salesforce será bloqueada durante 24 horas.

Também poderá receber o erro "REQUEST_LIMIT_EXCEEDED" em ambos os cenários. Consulte a secção "Limites de pedidos de API" o [limites de programador do Salesforce](http://resources.docs.salesforce.com/200/20/en-us/sfdc/pdf/salesforce_app_limits_cheatsheet.pdf) artigo para obter detalhes.

## <a name="getting-started"></a>Introdução
Pode criar um pipeline com uma atividade de cópia move os dados do Salesforce utilizando ferramentas diferentes/APIs.

A forma mais fácil de criar um pipeline que consiste em utilizar o **Assistente para copiar**. Consulte [Tutorial: criar um pipeline com o Assistente para copiar](data-factory-copy-data-wizard-tutorial.md) para instruções rápidas sobre como criar um pipeline com o Assistente de cópia de dados.

Também pode utilizar as ferramentas seguintes para criar um pipeline: **portal do Azure**, **Visual Studio**, **Azure PowerShell**, **modelo Azure Resource Manager**, **.NET API**, e **REST API**. Consulte [tutorial de atividade de cópia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para obter instruções passo a passo Criar um pipeline com uma atividade de cópia. 

Se utilizar as ferramentas ou APIs, execute os seguintes passos para criar um pipeline que move os dados de um arquivo de dados de origem para um arquivo de dados do sink: 

1. Criar **serviços ligados** associar dados de entrada e de saída armazena à fábrica de dados.
2. Criar **conjuntos de dados** para representar os dados de entrada e saídos da operação de cópia. 
3. Criar um **pipeline** com uma atividade de cópia executa um conjunto de dados como entrada e um conjunto de dados como resultado. 

Quando utilizar o assistente, definições de JSON para estas entidades do Data Factory (serviços ligados, conjuntos de dados e o pipeline) são criadas automaticamente para si. Ao utilizar ferramentas/APIs (exceto .NET API), é possível definir estas entidades do Data Factory, utilizando o formato JSON.  Para um exemplo com definições de JSON para entidades do Data Factory que são utilizadas para copiar dados do Salesforce, consulte [exemplo JSON: copiar dados do Salesforce ao Blob do Azure](#json-example-copy-data-from-salesforce-to-azure-blob) secção deste artigo. 

As secções seguintes fornecem detalhes sobre as propriedades JSON que são utilizados para definir o Salesforce entidades do Data Factory específicas: 

## <a name="linked-service-properties"></a>Propriedades de serviço ligado
A tabela seguinte fornece descrições para os elementos JSON que são específicas para o serviço ligado do Salesforce.

| Propriedade | Descrição | Necessário |
| --- | --- | --- |
| tipo |A propriedade de tipo tem de ser definida: **Salesforce**. |Sim |
| environmentUrl | Especifique a instância do URL do Salesforce. <br><br> -Predefinição é "https://login.salesforce.com". <br> -Para copiar dados a partir de sandbox, especifique "https://test.salesforce.com". <br> -Para copiar dados de domínio personalizado, especificar, por exemplo, "https://[domain].my.salesforce.com". |Não |
| o nome de utilizador |Especifique um nome de utilizador para a conta de utilizador. |Sim |
| palavra-passe |Especifique uma palavra-passe da conta de utilizador. |Sim |
| securityToken |Especifique um token de segurança para a conta de utilizador. Consulte [obtenha o token de segurança](https://help.salesforce.com/apex/HTViewHelpDoc?id=user_security_token.htm) para obter instruções sobre como repor/obter um token de segurança. Para saber mais sobre os tokens de segurança em geral, consulte [segurança e a API](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_concepts_security.htm). |Sim |

## <a name="dataset-properties"></a>Propriedades do conjunto de dados
Para uma lista completa das secções e as propriedades disponíveis para definir os conjuntos de dados, consulte o [criar conjuntos de dados](data-factory-create-datasets.md) artigo. As secções, tais como a estrutura, a disponibilidade e a política de um conjunto de dados JSON são semelhantes para todos os tipos de conjunto de dados (SQL do Azure, Azure blob, tabela do Azure e assim sucessivamente).

O **typeProperties** secção é diferente para cada tipo de conjunto de dados e fornece informações sobre a localização dos dados no arquivo de dados. Os typeProperties secção para um conjunto de dados do tipo **RelationalTable** tem as seguintes propriedades:

| Propriedade | Descrição | Necessário |
| --- | --- | --- |
| tableName |Nome da tabela no Salesforce. |Não (se um **consulta** de **RelationalSource** especificado) |

> [!IMPORTANT]
> A parte "__c" o nome da API é necessário para qualquer objeto personalizado.

![Nome do Data Factory - Salesforce ligação - API](media/data-factory-salesforce-connector/data-factory-salesforce-api-name.png)

## <a name="copy-activity-properties"></a>Propriedades da atividade Copy
Para uma lista completa das secções e as propriedades disponíveis para definir as atividades, consulte o [Criar pipelines](data-factory-create-pipelines.md) artigo. Propriedades como o nome, a descrição, a entrada e saída tabelas e várias políticas estão disponíveis para todos os tipos de atividades.

As propriedades que estão disponíveis na secção typeProperties da atividade, por outro lado, variar de acordo com cada tipo de atividade. Para a atividade de cópia, podem variam consoante os tipos de origens e sinks.

Na atividade de cópia, quando a origem é do tipo **RelationalSource** (que inclui o Salesforce), na secção typeProperties, estão disponíveis as seguintes propriedades:

| Propriedade | Descrição | Valores permitidos | Necessário |
| --- | --- | --- | --- |
| consulta |Utilize a consulta personalizada para ler os dados. |Uma consulta de SQL 92 ou [idioma de consulta de objeto do Salesforce (SOQL)](https://developer.salesforce.com/docs/atlas.en-us.soql_sosl.meta/soql_sosl/sforce_api_calls_soql.htm) consulta. Por exemplo: `select * from MyTable__c`. |Não (se o **tableName** do **dataset** especificado) |

> [!IMPORTANT]
> A parte "__c" o nome da API é necessário para qualquer objeto personalizado.

![Nome do Data Factory - Salesforce ligação - API](media/data-factory-salesforce-connector/data-factory-salesforce-api-name-2.png)

## <a name="query-tips"></a>Sugestões de consulta
### <a name="retrieving-data-using-where-clause-on-datetime-column"></a>Obter dados com onde cláusula na coluna de DateTime
Especifique quando a consulta SOQL ou SQL Server, preste atenção à diferença de formato DateTime. Por exemplo:

* **Exemplo SOQL**:`$$Text.Format('SELECT Id, Name, BillingCity FROM Account WHERE LastModifiedDate >= {0:yyyy-MM-ddTHH:mm:ssZ} AND LastModifiedDate < {1:yyyy-MM-ddTHH:mm:ssZ}', WindowStart, WindowEnd)`
* **Exemplo SQL**:
    * **Utilizando o Assistente para copiar para especificar a consulta:**`$$Text.Format('SELECT * FROM Account WHERE LastModifiedDate >= {{ts\'{0:yyyy-MM-dd HH:mm:ss}\'}} AND LastModifiedDate < {{ts\'{1:yyyy-MM-dd HH:mm:ss}\'}}', WindowStart, WindowEnd)`
    * **Utilizar o JSON de edição para especificar a consulta (como de escape char corretamente):**`$$Text.Format('SELECT * FROM Account WHERE LastModifiedDate >= {{ts\\'{0:yyyy-MM-dd HH:mm:ss}\\'}} AND LastModifiedDate < {{ts\\'{1:yyyy-MM-dd HH:mm:ss}\\'}}', WindowStart, WindowEnd)`

### <a name="retrieving-data-from-salesforce-report"></a>Obter dados de relatórios do Salesforce
Pode obter dados de relatórios do Salesforce, especificando a consulta como `{call "<report name>"}`, por exemplo,. `"query": "{call \"TestReport\"}"`.

### <a name="retrieving-deleted-records-from-salesforce-recycle-bin"></a>A obter eliminados registos da Reciclagem do Salesforce
Para consultar os registos eliminados recuperável da Reciclagem do Salesforce, pode especificar **"IsDeleted = 1"** na sua consulta. Por exemplo,

* Para consultar apenas os registos eliminados, especifique "selecionar * de MyTable__c **onde IsDeleted = 1**"
* Para consultar todos os registos, incluindo o existente e o eliminado, especifique "selecionar * de MyTable__c **onde IsDeleted = 0 ou IsDeleted = 1**"

## <a name="json-example-copy-data-from-salesforce-to-azure-blob"></a>Exemplo JSON: copiar dados do Salesforce ao Blob do Azure
O exemplo seguinte fornece definições de JSON de exemplo que pode utilizar para criar um pipeline com o [portal do Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), ou [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md). Estes mostram como copiar dados do Salesforce ao Blob Storage do Azure. No entanto, os dados podem ser copiados para qualquer um dos sinks indicados [aqui](data-factory-data-movement-activities.md#supported-data-stores-and-formats) utilizando a atividade de cópia no Azure Data Factory.   

Seguem-se os artefactos do Data Factory que terá de criar para implementar o cenário. As secções que se seguem lista fornecem detalhes sobre estes passos.

* Um serviço ligado do tipo [Salesforce](#linked-service-properties)
* Um serviço ligado do tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)
* Uma entrada [dataset](data-factory-create-datasets.md) do tipo [RelationalTable](#dataset-properties)
* Uma saída [dataset](data-factory-create-datasets.md) do tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties)
* A [pipeline](data-factory-create-pipelines.md) com atividade de cópia que utiliza [RelationalSource](#copy-activity-properties) e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties)

**Serviço ligado do Salesforce**

Este exemplo utiliza o **Salesforce** serviço ligado. Consulte o [serviço ligado do Salesforce](#linked-service-properties) secção para as propriedades que são suportados por este serviço ligado.  Consulte [obtenha o token de segurança](https://help.salesforce.com/apex/HTViewHelpDoc?id=user_security_token.htm) para obter instruções sobre como repor/obter o token de segurança.

```json
{
    "name": "SalesforceLinkedService",
    "properties":
    {
        "type": "Salesforce",
        "typeProperties":
        {
            "username": "<user name>",
            "password": "<password>",
            "securityToken": "<security token>"
        }
    }
}
```
**Serviço ligado do Armazenamento do Azure**

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
**Conjunto de dados de entrada Salesforce**

```json
{
    "name": "SalesforceInput",
    "properties": {
        "linkedServiceName": "SalesforceLinkedService",
        "type": "RelationalTable",
        "typeProperties": {
            "tableName": "AllDataType__c"  
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

Definição **externo** para **verdadeiro** informa o serviço fábrica de dados que o conjunto de dados é externo à fábrica de dados e não é produzido por uma atividade no factory de dados.

> [!IMPORTANT]
> A parte "__c" o nome da API é necessário para qualquer objeto personalizado.

![Nome do Data Factory - Salesforce ligação - API](media/data-factory-salesforce-connector/data-factory-salesforce-api-name.png)

**Conjunto de dados de saída do blob do Azure**

Dados são escritos num blob novo a cada hora (frequência: hora, intervalo: 1).

```json
{
    "name": "AzureBlobOutput",
    "properties":
    {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties":
        {
            "folderPath": "adfgetstarted/alltypes_c"
        },
        "availability":
        {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

**Pipeline com atividade de cópia**

O pipeline contém uma atividade de cópia, que está configurado para utilizar os conjuntos de dados de entrada e de saída e está agendada para execução a cada hora. No pipeline de definição de JSON, o **origem** tipo está definido como **RelationalSource**e o **sink** tipo está definido como **BlobSink**.

Consulte [propriedades do tipo RelationalSource](#copy-activity-properties) para a lista de propriedades que são suportadas pelo RelationalSource.

```json
{  
    "name":"SamplePipeline",
    "properties":{  
        "start":"2016-06-01T18:00:00",
        "end":"2016-06-01T19:00:00",
        "description":"pipeline with copy activity",
        "activities":[  
        {
            "name": "SalesforceToAzureBlob",
            "description": "Copy from Salesforce to an Azure blob",
            "type": "Copy",
            "inputs": [
            {
                "name": "SalesforceInput"
            }
            ],
            "outputs": [
            {
                "name": "AzureBlobOutput"
            }
            ],
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "SELECT Id, Col_AutoNumber__c, Col_Checkbox__c, Col_Currency__c, Col_Date__c, Col_DateTime__c, Col_Email__c, Col_Number__c, Col_Percent__c, Col_Phone__c, Col_Picklist__c, Col_Picklist_MultiSelect__c, Col_Text__c, Col_Text_Area__c, Col_Text_AreaLong__c, Col_Text_AreaRich__c, Col_URL__c, Col_Text_Encrypt__c, Col_Lookup__c FROM AllDataType__c"                
                },
                "sink": {
                    "type": "BlobSink"
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
> [!IMPORTANT]
> A parte "__c" o nome da API é necessário para qualquer objeto personalizado.

![Nome do Data Factory - Salesforce ligação - API](media/data-factory-salesforce-connector/data-factory-salesforce-api-name-2.png)


### <a name="type-mapping-for-salesforce"></a>Mapeamento de tipo para o Salesforce
| Tipo de Salesforce | . Tipo de rede |
| --- | --- |
| Número de automática |Cadeia |
| Caixa de verificação |Booleano |
| Moeda |Duplo |
| Data |DateTime |
| Data/Hora |DateTime |
| E-mail |Cadeia |
| Id |Cadeia |
| Relação de referência |Cadeia |
| Selecionar vários Picklist |Cadeia |
| Número |Duplo |
| Percentagem |Duplo |
| Telefone |Cadeia |
| Picklist |Cadeia |
| Texto |Cadeia |
| Área de texto |Cadeia |
| Área de texto (longa) |Cadeia |
| Área de texto (avançada) |Cadeia |
| Texto (encriptado) |Cadeia |
| URL |Cadeia |

> [!NOTE]
> Para mapear colunas do conjunto de dados de origem para colunas do conjunto de dados dependente, consulte [mapeamento de colunas do conjunto de dados no Azure Data Factory](data-factory-map-columns.md).

[!INCLUDE [data-factory-structure-for-rectangualr-datasets](../../../includes/data-factory-structure-for-rectangualr-datasets.md)]

## <a name="performance-and-tuning"></a>Desempenho e otimização
Consulte o [guia Otimização e de desempenho de atividade de cópia](data-factory-copy-activity-performance.md) para saber mais sobre fatores determinantes esse desempenho impacto de movimento de dados (atividade de cópia) no Azure Data Factory e várias formas para otimizar o mesmo.
