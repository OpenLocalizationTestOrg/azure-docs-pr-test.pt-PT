---
title: dados de aaaMove de arquivos de dados ODBC | Microsoft Docs
description: Saiba mais sobre como dados de toomove dos dados ODBC armazena utilizando o Azure Data Factory.
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: ad70a598-c031-4339-a883-c6125403cb76
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: jingwang
ms.openlocfilehash: bf96e71da449313b6144bb194205c572d2ca2030
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-odbc-data-stores-using-azure-data-factory"></a>Mover dados de ODBC os arquivos de dados utilizando o Azure Data Factory
Este artigo explica como armazenar toouse Olá atividade de cópia de dados de toomove do Azure Data Factory de dados ODBC no local. Baseia-se no Olá [atividades de movimentos de dados](data-factory-data-movement-activities.md) artigo, que apresenta uma descrição geral do movimento de dados com a atividade de cópia de Olá.

Pode copiar dados de um arquivo de dados do ODBC dados arquivo tooany suportado sink. Para obter uma lista dos dados arquivos suportados como sinks pela atividade de cópia de Olá, consulte Olá [arquivos de dados suportados](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabela. Fábrica de dados atualmente suporta apenas mover tooother arquivos de dados de arquivo de dados de dados de ODBC, mas não para mover dados do arquivo de dados ODBC outros dados arquivos tooan. 

## <a name="enabling-connectivity"></a>Ativar a conectividade
Serviço de fábrica de dados suporta origens ODBC tooon local ao ligar utilizando Olá Data Management Gateway. Consulte [mover dados entre localizações no local e nuvem](data-factory-move-data-between-onprem-and-cloud.md) toolearn artigo sobre o Data Management Gateway e instruções passo a passo sobre como configurar o gateway de Olá. Utilize o arquivo de dados ODBC tooconnect tooan Olá gateway mesmo esteja alojado numa VM do IaaS do Azure.

Pode instalar o gateway de Olá num Olá mesmo no local do computador ou Olá VM do Azure como arquivo de dados ODBC Olá. No entanto, recomendamos que instale o gateway de Olá num máquina/Azure separado IaaS VM tooavoid contenção de recursos e para um melhor desempenho. Quando instalar o gateway de Olá num computador separado, máquina Olá deve ser capaz de tooaccess máquina de Olá com o arquivo de dados ODBC Olá.

Para além dos Olá Data Management Gateway, tem também o controlador ODBC do tooinstall Olá Olá arquivo de dados no computador do gateway de Olá.

> [!NOTE]
> Consulte [resolver problemas de gateway](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) para dicas sobre/gateway de ligação de resolução de problemas relacionados com problemas.

## <a name="getting-started"></a>Introdução
Pode criar um pipeline com uma atividade de cópia move os dados de um arquivo de dados ODBC utilizando ferramentas diferentes/APIs.

Olá toocreate da forma mais fácil um pipeline está toouse Olá **Assistente para copiar**. Consulte [Tutorial: criar um pipeline com o Assistente para copiar](data-factory-copy-data-wizard-tutorial.md) para obter instruções sobre como criar um pipeline com o Assistente de cópia de dados Olá rápida.

Também pode utilizar Olá seguintes ferramentas toocreate um pipeline: **portal do Azure**, **Visual Studio**, **Azure PowerShell**, **modelo Azure Resource Manager** , **.NET API**, e **REST API**. Consulte [tutorial de atividade de cópia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para instruções passo a passo toocreate um pipeline com uma atividade de cópia. 

Se utilizar ferramentas de Olá ou APIs, execute Olá os seguintes passos toocreate um pipeline que move o arquivo de dados do tooa sink do arquivo de dados de uma origem de dados: 

1. Criar **serviços ligados** fábrica de dados de tooyour de arquivos de dados de entrada e saída de toolink.
2. Criar **conjuntos de dados** toorepresent de entrada e saída de operação de cópia de dados para Olá. 
3. Criar um **pipeline** com uma atividade de cópia executa um conjunto de dados como entrada e um conjunto de dados como resultado. 

Quando utiliza o Assistente de Olá, definições de JSON para estas entidades do Data Factory (serviços ligados, conjuntos de dados e pipeline Olá) são criadas automaticamente para si. Ao utilizar ferramentas/APIs (exceto .NET API), é possível definir estas entidades do Data Factory utilizando o formato JSON Olá.  Para um exemplo com definições de JSON para entidades do Data Factory que são utilizados toocopy dados de um arquivo de dados ODBC, consulte [exemplo JSON: arquivo de dados de cópia de dados de ODBC tooAzure Blob](#json-example-copy-data-from-odbc-data-store-to-azure-blob) secção deste artigo. 

Olá seguintes secções fornece detalhes sobre as propriedades JSON que são o arquivo de dados do toodefine utilizados Data Factory entidades tooODBC específico:

## <a name="linked-service-properties"></a>Propriedades de serviço ligado
Olá, a tabela seguinte fornece uma descrição do serviço do JSON elementos específicos tooODBC ligado.

| Propriedade | Descrição | Necessário |
| --- | --- | --- |
| tipo |a propriedade de tipo Olá tem de ser definida: **OnPremisesOdbc** |Sim |
| connectionString |parte de credencial de acesso não de Olá da cadeia de ligação de Olá e opcional encriptada credencial. Veja exemplos na Olá seguintes secções: |Sim |
| credencial |parte de credencial de acesso de Olá Olá da cadeia de ligação especificada no formato do valor da propriedade do controlador específico. Exemplo: "Uid =<user ID>; Pwd =<password>; RefreshToken =<secret refresh token>; ". |Não |
| authenticationType |Tipo de autenticação utilizado tooconnect toohello arquivo de dados ODBC. Os valores possíveis são: básico e anónimos. |Sim |
| o nome de utilizador |Especifique o nome de utilizador se estiver a utilizar autenticação básica. |Não |
| palavra-passe |Especifique a palavra-passe da conta de utilizador de Olá especificado para nome de utilizador Olá. |Não |
| gatewayName |Nome do gateway de Olá que Olá serviço Data Factory deve utilizar o arquivo de dados ODBC do tooconnect toohello. |Sim |

### <a name="using-basic-authentication"></a>Utilizar a autenticação básica

```json
{
    "name": "odbc",
    "properties":
    {
        "type": "OnPremisesOdbc",
        "typeProperties":
        {
            "authenticationType": "Basic",
            "connectionString": "Driver={SQL Server};Server=Server.database.windows.net; Database=TestDatabase;",
            "userName": "username",
            "password": "password",
            "gatewayName": "mygateway"
        }
    }
}
```
### <a name="using-basic-authentication-with-encrypted-credentials"></a>Utilizar a autenticação básica com credenciais encriptado
Pode encriptar as credenciais de Olá utilizando Olá [New-AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) cmdlet (1.0 versão do Azure PowerShell) ou [New-AzureDataFactoryEncryptValue](https://msdn.microsoft.com/library/dn834940.aspx) (0.9 ou anterior versão da Olá O Azure PowerShell).  

```json
{
    "name": "odbc",
    "properties":
    {
        "type": "OnPremisesOdbc",
        "typeProperties":
        {
            "authenticationType": "Basic",
            "connectionString": "Driver={SQL Server};Server=myserver.database.windows.net; Database=TestDatabase;;EncryptedCredential=eyJDb25uZWN0...........................",
            "gatewayName": "mygateway"
        }
    }
}
```

### <a name="using-anonymous-authentication"></a>Autenticação anónima

```json
{
    "name": "odbc",
    "properties":
    {
        "type": "OnPremisesOdbc",
        "typeProperties":
        {
            "authenticationType": "Anonymous",
            "connectionString": "Driver={SQL Server};Server={servername}.database.windows.net; Database=TestDatabase;",
            "credential": "UID={uid};PWD={pwd}",
            "gatewayName": "mygateway"
        }
    }
}
```


## <a name="dataset-properties"></a>Propriedades do conjunto de dados
Para uma lista completa das secções & Propriedades disponíveis para definir os conjuntos de dados, consulte Olá [criar conjuntos de dados](data-factory-create-datasets.md) artigo. As secções, tais como a estrutura, a disponibilidade e a política de um conjunto de dados JSON são semelhantes para todos os tipos de conjunto de dados (SQL do Azure, Azure blob, tabela do Azure, etc.).

Olá **typeProperties** secção é diferente para cada tipo de conjunto de dados e fornece informações sobre a localização de Olá dos dados de Olá no arquivo de dados de Olá. Olá typeProperties secção para o conjunto de dados do tipo **RelationalTable** (que inclui o conjunto de dados ODBC) tem Olá seguintes propriedades

| Propriedade | Descrição | Necessário |
| --- | --- | --- |
| tableName |Nome da tabela de Olá no arquivo de dados ODBC Olá. |Sim |

## <a name="copy-activity-properties"></a>Propriedades da atividade de cópia
Para uma lista completa das secções & Propriedades disponíveis para definir as atividades, consulte Olá [criar Pipelines](data-factory-create-pipelines.md) artigo. Propriedades, tais como o nome, descrição e de saída, tabelas e as políticas estão disponíveis para todos os tipos de atividades.

Propriedades disponíveis nos Olá **typeProperties** secção de atividades de Olá em Olá por outro lado variar de acordo com cada tipo de atividade. Para a atividade de cópia, podem variam consoante os tipos de origens e sinks Olá.

Na atividade de cópia, quando a origem é do tipo **RelationalSource** (que inclui ODBC), na secção typeProperties, estão disponível Olá seguintes propriedades:

| Propriedade | Descrição | Valores permitidos | Necessário |
| --- | --- | --- | --- |
| consulta |Utilize Olá consulta personalizada tooread dados. |Cadeia de consulta SQL. Por exemplo: selecionar * de MyTable. |Sim |


## <a name="json-example-copy-data-from-odbc-data-store-tooazure-blob"></a>Exemplo JSON: arquivo de dados de cópia de dados de ODBC tooAzure Blob
Neste exemplo fornece definições de JSON que pode utilizar toocreate um pipeline utilizando [portal do Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) ou [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) ou [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md). Mostra como tooan Blob Storage do Azure da origem de dados de toocopy de um ODBC. No entanto, os dados podem ser copiado tooany de Olá sinks indicado [aqui](data-factory-data-movement-activities.md#supported-data-stores-and-formats) utilizando Olá atividade de cópia no Azure Data Factory.

exemplo de Olá tem Olá seguintes entidades da fábrica de dados:

1. Um serviço ligado do tipo [OnPremisesOdbc](#linked-service-properties).
2. Um serviço ligado do tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
3. Uma entrada [dataset](data-factory-create-datasets.md) do tipo [RelationalTable](#dataset-properties).
4. Uma saída [dataset](data-factory-create-datasets.md) do tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
5. A [pipeline](data-factory-create-pipelines.md) com atividade de cópia que utiliza [RelationalSource](#copy-activity-properties) e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).

exemplo de Olá copia dados a partir num resultado de consulta um blob de tooa do arquivo de dados ODBC a cada hora. Propriedades JSON de Olá utilizadas nestes exemplos são descritas nas secções seguintes exemplos de Olá.

Como primeiro passo, configure Olá o data management gateway. instruções de Olá estão em Olá [mover dados entre localizações no local e nuvem](data-factory-move-data-between-onprem-and-cloud.md) artigo.

**Serviço ligado de ODBC** este exemplo utiliza Olá autenticação básica. Consulte [serviço ligado de ODBC](#linked-service-properties) secção para diferentes tipos de autenticação, pode utilizar.

```json
{
    "name": "OnPremOdbcLinkedService",
    "properties":
    {
        "type": "OnPremisesOdbc",
        "typeProperties":
        {
            "authenticationType": "Basic",
            "connectionString": "Driver={SQL Server};Server=Server.database.windows.net; Database=TestDatabase;",
            "userName": "username",
            "password": "password",
            "gatewayName": "mygateway"
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

**Conjunto de dados de entrada de ODBC**

exemplo de Olá pressupõe que criou uma tabela "MyTable" numa base de dados ODBC e contém uma coluna chamada "timestampcolumn" para dados de séries de tempo.

A definição "external": "true" informa serviço do Data Factory Olá esse conjunto de dados de Olá é toohello externo fábrica de dados e não é produzido por uma atividade no factory de dados de Olá.

```json
{
    "name": "ODBCDataSet",
    "properties": {
        "published": false,
        "type": "RelationalTable",
        "linkedServiceName": "OnPremOdbcLinkedService",
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

**Conjunto de dados de saída de Blobs do Azure**

São escritos dados no blob tooa de novo a cada hora (frequência: hora, intervalo: 1). caminho da pasta Olá para BLOBs Olá dinamicamente é avaliado com base na hora de início de Olá do setor de Olá que está a ser processado. caminho da pasta Olá utiliza ano, mês, dia e horas partes Olá da hora de início.

```json
{
    "name": "AzureBlobOdbcDataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/odbc/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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


**Atividade de cópia de um pipeline com a origem ODBC (RelationalSource) e o sink de Blob (BlobSink)**

pipeline de Olá contém uma atividade de cópia que está configurado toouse estes conjuntos de dados de entrada e de saída e toorun agendada a cada hora. No pipeline de Olá definição JSON, Olá **origem** tipo está definido demasiado**RelationalSource** e **sink** tipo está definido demasiado**BlobSink**. consulta SQL Olá especificada para Olá **consulta** propriedade seleciona dados Olá Olá passado toocopy de hora.

```json
{
    "name": "CopyODBCToBlob",
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
                        "name": "OdbcDataSet"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobOdbcDataSet"
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
                "name": "OdbcToBlob"
            }
        ],
        "start": "2016-06-01T18:00:00Z",
        "end": "2016-06-01T19:00:00Z"
    }
}
```
### <a name="type-mapping-for-odbc"></a>Mapeamento de tipos para ODBC
Tal como mencionado na Olá [atividades de movimentos de dados](data-factory-data-movement-activities.md) artigo, a atividade de cópia realiza conversões de tipo automática dos tipos de toosink de tipos de origem com Olá abordagem de dois passos a seguir:

1. Converter do tipo de too.NET de tipos de origem nativo
2. Converter do tipo de sink de toonative de tipo .NET

Quando mover dados de arquivos de dados ODBC, tipos de dados ODBC são tipos de too.NET mapeada tal como mencionado na Olá [mapeamentos de tipos de dados de ODBC](https://msdn.microsoft.com/library/cc668763.aspx) tópico.

## <a name="map-source-toosink-columns"></a>Mapear colunas toosink de origem
toolearn sobre mapeamento as colunas na origem toocolumns de conjunto de dados no conjunto de dados dependente, consulte [mapeamento de colunas do conjunto de dados no Azure Data Factory](data-factory-map-columns.md).

## <a name="repeatable-read-from-relational-sources"></a>Repetíveis leitura a partir de origens relacionais
Quando copiar dados de arquivos de dados relacional, manter a repetibilidade em mente tooavoid resultados inesperados. No Azure Data Factory, pode voltar a executar um setor manualmente. Também pode configurar a política de repetição para um conjunto de dados para que um setor será novamente executado quando ocorre uma falha. Quando um setor é voltar a executar qualquer forma, terá de toomake certificar-se de que Olá mesmos dados é de leitura como não independentemente do número de vezes que um setor é executado. Consulte [Repeatable ler a partir de origens relacionais](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).

## <a name="ge-historian-store"></a>Arquivo de GE Historian
Criar um toolink de serviço ligado de ODBC um [GE Proficy Historian (agora GE Historian)](http://www.geautomation.com/products/proficy-historian) tooan fábrica de dados do Azure do arquivo de dados conforme mostrado no seguinte exemplo de Olá:

```json
{
    "name": "HistorianLinkedService",
    "properties":
    {
        "type": "OnPremisesOdbc",
        "typeProperties":
        {
            "connectionString": "DSN=<name of hello GE Historian store>",
            "gatewayName": "<gateway name>",
            "authenticationType": "Basic",
            "userName": "<user name>",
            "password": "<password>"
        }
    }
}
```

Instalar o Data Management Gateway numa máquina no local e registar o gateway de Olá com o portal de Olá. gateway de Olá instalado no seu computador no local utiliza o controlador ODBC Olá para GE Historian tooconnect toohello arquivo de dados de GE Historian. Por conseguinte, instale o controlador de Olá se não estiver já instalado no computador do gateway de Olá. Consulte [ativar conectividade](#enabling-connectivity) secção para obter detalhes.

Antes de utilizar Olá GE Historian armazenar numa solução de fábrica de dados, verifique se o gateway de Olá pode ligar toohello arquivo de dados com as instruções na secção seguinte Olá.

Artigo de Olá de leitura a partir do início de Olá para uma descrição geral detalhada da utilização de dados de ODBC armazena como arquivos de dados de origem de uma operação de cópia.  

## <a name="troubleshoot-connectivity-issues"></a>Resolver problemas de conectividade
problemas de ligação de tootroubleshoot, utilize Olá **diagnóstico** separador de **Gestor de configuração do Data Management Gateway**.

1. Iniciar **Gestor de configuração do Data Management Gateway**. Pode optar por executar "C:\Program Files\Microsoft Data gestão Gateway\1.0\Shared\ConfigManager.exe" diretamente (ou) pesquisa para **Gateway** toofind uma ligação demasiado**Microsoft Data Management Gateway** aplicação conforme mostrado no Olá seguinte imagem.

    ![Gateway de pesquisa](./media/data-factory-odbc-connector/search-gateway.png)
2. Comutador toohello **diagnóstico** separador.

    ![Diagnóstico do gateway](./media/data-factory-odbc-connector/data-factory-gateway-diagnostics.png)
3. Selecione Olá **tipo** de dados armazenar (serviço ligado).
4. Especifique **autenticação** e introduza **credenciais** (ou) introduza **cadeia de ligação** que é o arquivo de dados de toohello tooconnect utilizados.
5. Clique em **Testar ligação** o arquivo de dados do tootest Olá ligação toohello.

## <a name="performance-and-tuning"></a>Desempenho e a otimização
Consulte [desempenho de atividade de cópia & otimização guia](data-factory-copy-activity-performance.md) toolearn sobre chave factors desse desempenho impacto de movimento de dados (atividade de cópia) no Azure Data Factory e várias formas toooptimize-lo.
