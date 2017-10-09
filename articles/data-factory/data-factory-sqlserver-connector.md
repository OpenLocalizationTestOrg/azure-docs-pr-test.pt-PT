---
title: aaaMove tooand de dados do SQL Server | Microsoft Docs
description: "Saiba mais sobre como dados toomove da SQL Server da base de dados que está no local ou numa VM do Azure utilizando o Azure Data Factory."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 864ece28-93b5-4309-9873-b095bbe6fedd
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jingwang
ms.openlocfilehash: f0cccf56a670e62ec893d75052a81eb26d562050
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-tooand-from-sql-server-on-premises-or-on-iaas-azure-vm-using-azure-data-factory"></a>Mover tooand de dados do SQL Server no local ou no IaaS (VM do Azure) utilizando o Azure Data Factory
Este artigo explica como toouse Olá atividade de cópia de dados de toomove do Azure Data Factory para/de uma base de dados do SQL Server no local. Baseia-se no Olá [atividades de movimentos de dados](data-factory-data-movement-activities.md) artigo, que apresenta uma descrição geral do movimento de dados com a atividade de cópia de Olá. 

## <a name="supported-scenarios"></a>Cenários suportados
Pode copiar dados **de uma base de dados do SQL Server** toohello seguir arquivos de dados:

[!INCLUDE [data-factory-supported-sink](../../includes/data-factory-supported-sinks.md)]

Pode copiar dados de Olá seguir arquivos de dados **base de dados do SQL Server tooa**:

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

## <a name="supported-sql-server-versions"></a>Versões suportadas do SQL Server
Este suporte de conector do SQL Server copiar dados a partir de / toohello seguintes versões de instância alojado no local ou no IaaS do Azure utilizando a autenticação do SQL Server e a autenticação do Windows: SQL Server 2016, o SQL Server 2014, o SQL Server 2012, o SQL Server 2008 R2, o SQL Server Server 2008, o SQL Server 2005

## <a name="enabling-connectivity"></a>Ativar a conectividade
conceitos de Olá e passos necessários para estabelecer a ligação com SQL Server alojado no local ou no IaaS do Azure VMs (infraestrutura-como-um-serviço) são Olá mesmo. Em ambos os casos, terá de toouse Data Management Gateway para a conectividade.

Consulte [mover dados entre localizações no local e nuvem](data-factory-move-data-between-onprem-and-cloud.md) toolearn artigo sobre o Data Management Gateway e instruções passo a passo sobre como configurar o gateway de Olá. Configurar uma instância de gateway é um pré-requisito para a ligação com o SQL Server.

Enquanto pode instalar o gateway no Olá mesmo no local instância VM de nuvem ou máquina como hello do SQL Server para um melhor desempenho, recomendamos que instalar em computadores separados. A existência de gateway Olá e o SQL Server em máquinas separadas reduz a contenção de recursos.

## <a name="getting-started"></a>Introdução
Pode criar um pipeline com uma atividade de cópia move os dados de/para uma base de dados do SQL Server no local utilizando ferramentas diferentes/APIs.

Olá toocreate da forma mais fácil um pipeline está toouse Olá **Assistente para copiar**. Consulte [Tutorial: criar um pipeline com o Assistente para copiar](data-factory-copy-data-wizard-tutorial.md) para obter instruções sobre como criar um pipeline com o Assistente de cópia de dados Olá rápida.

Também pode utilizar Olá seguintes ferramentas toocreate um pipeline: **portal do Azure**, **Visual Studio**, **Azure PowerShell**, **modelo Azure Resource Manager** , **.NET API**, e **REST API**. Consulte [tutorial de atividade de cópia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para instruções passo a passo toocreate um pipeline com uma atividade de cópia. 

Se utilizar ferramentas de Olá ou APIs, execute Olá os seguintes passos toocreate um pipeline que move o arquivo de dados do tooa sink do arquivo de dados de uma origem de dados: 

1. Criar um **fábrica de dados**. Uma fábrica de dados pode conter um ou mais pipelines. 
2. Criar **serviços ligados** fábrica de dados de tooyour de arquivos de dados de entrada e saída de toolink. Por exemplo, se estiver a copiar dados de um tooan de base de dados do SQL Server blob storage do Azure, pode cria dois serviços ligados toolink a base de dados do SQL Server e a fábrica de dados de tooyour de conta de armazenamento do Azure. Para o serviço ligado as propriedades da base de dados de servidor de tooSQL específico, consulte [ligado propriedades do serviço](#linked-service-properties) secção. 
3. Criar **conjuntos de dados** toorepresent de entrada e saída de operação de cópia de dados para Olá. Exemplo de Olá mencionado no passo último Olá, crie uma tabela SQL do conjunto de dados toospecify Olá na base de dados do SQL Server que contém dados de entrada Olá. Crie outro conjunto de dados toospecify Olá o contentor de BLOBs e pasta de Olá que contém dados Olá copiados Olá base de dados do SQL Server. Para o conjunto de dados as propriedades da base de dados de servidor de tooSQL específico, consulte [propriedades do dataset](#dataset-properties) secção.
4. Criar um **pipeline** com uma atividade de cópia executa um conjunto de dados como entrada e um conjunto de dados como resultado. Exemplo de Olá mencionado anteriormente, que utilizar SqlSource como uma origem e BlobSink como um sink para atividade de cópia de Olá. Da mesma forma, se estiver a copiar a partir do Blob Storage do Azure tooSQL base de dados do servidor, utilizar BlobSource e SqlSink na atividade de cópia de Olá. Para copiar atividade propriedades tooSQL específica da base de dados do servidor, consulte [copiar propriedades da atividade](#copy-activity-properties) secção. Para obter detalhes sobre como toouse um arquivo de dados como uma origem ou de um receptor de mensagens em fila, clique em ligação Olá na secção anterior do Olá para o arquivo de dados. 

Quando utiliza o Assistente de Olá, definições de JSON para estas entidades do Data Factory (serviços ligados, conjuntos de dados e pipeline Olá) são criadas automaticamente para si. Ao utilizar ferramentas/APIs (exceto .NET API), é possível definir estas entidades do Data Factory utilizando o formato JSON Olá.  Para exemplos com definições de JSON para entidades do Data Factory que são utilizados toocopy dados para/de uma base de dados do SQL Server no local, consulte [exemplos JSON](#json-examples-for-copying-data-from-and-to-sql-server) secção deste artigo. 

Olá seguintes secções fornece detalhes sobre as propriedades JSON que são utilizados toodefine Data Factory entidades específica tooSQL servidor: 

## <a name="linked-service-properties"></a>Propriedades de serviço ligado
Criar um serviço ligado do tipo **OnPremisesSqlServer** toolink uma fábrica de dados no local do SQL Server da base de dados tooa. Olá, a tabela seguinte fornece uma descrição do serviço ligado do SQL Server do JSON elementos local tooon específico.

Olá, a tabela seguinte fornece uma descrição para JSON elementos específico tooSQL serviço de servidor ligado.

| Propriedade | Descrição | Necessário |
| --- | --- | --- |
| tipo |a propriedade de tipo Olá deve ser definida como: **OnPremisesSqlServer**. |Sim |
| connectionString |Especifique as informações de connectionString necessárias tooconnect toohello no local do SQL Server da base de dados utilizando a autenticação SQL ou autenticação do Windows. |Sim |
| gatewayName |Nome do gateway de Olá que Olá serviço Data Factory deve utilizar tooconnect toohello no local do SQL Server da base de dados. |Sim |
| o nome de utilizador |Especifique o nome de utilizador se estiver a utilizar a autenticação do Windows. Exemplo: **domainname\\username**. |Não |
| palavra-passe |Especifique a palavra-passe da conta de utilizador de Olá especificado para nome de utilizador Olá. |Não |

Pode encriptar as credenciais utilizando Olá **New-AzureRmDataFactoryEncryptValue** cmdlet e utilizá-los na cadeia de ligação de Olá, conforme mostrado no seguinte exemplo de Olá (**EncryptedCredential** propriedade):  

```JSON
"connectionString": "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=True;EncryptedCredential=<encrypted credential>",
```

### <a name="samples"></a>Amostras
**JSON para utilizar a autenticação do SQL Server**

```json
{
    "name": "MyOnPremisesSQLDB",
    "properties":
    {
        "type": "OnPremisesSqlServer",
        "typeProperties": {
            "connectionString": "Data Source=<servername>;Initial Catalog=MarketingCampaigns;Integrated Security=False;User ID=<username>;Password=<password>;",
            "gatewayName": "<gateway name>"
        }
    }
}
```
**JSON para utilizar a autenticação do Windows**

O Data Management Gateway será representar Olá especificado utilizador conta tooconnect toohello no local do SQL Server base de dados. 

```json
{
     "Name": " MyOnPremisesSQLDB",
     "Properties":
     {
         "type": "OnPremisesSqlServer",
         "typeProperties": {
             "ConnectionString": "Data Source=<servername>;Initial Catalog=MarketingCampaigns;Integrated Security=True;",
             "username": "<domain\\username>",
             "password": "<password>",
             "gatewayName": "<gateway name>"
        }
     }
}
```

## <a name="dataset-properties"></a>Propriedades do conjunto de dados
Nos exemplos de Olá, utilizou um conjunto de dados do tipo **SqlServerTable** toorepresent uma tabela numa base de dados do SQL Server.  

Para uma lista completa das secções & Propriedades disponíveis para definir os conjuntos de dados, consulte Olá [criar conjuntos de dados](data-factory-create-datasets.md) artigo. As secções, tais como a estrutura, a disponibilidade e a política de um conjunto de dados JSON são semelhantes para todos os tipos de conjunto de dados (SQL Server, BLOBs do Azure, a tabela do Azure, etc.).

secção de typeProperties Olá é diferente para cada tipo de conjunto de dados e fornece informações sobre a localização de Olá dos dados de Olá no arquivo de dados de Olá. Olá **typeProperties** secção Olá conjunto de dados do tipo **SqlServerTable** tem Olá seguintes propriedades:

| Propriedade | Descrição | Necessário |
| --- | --- | --- |
| tableName |Nome da tabela de Olá ou vista na instância de base de dados do SQL Server Olá pelo serviço ligado referenciada. |Sim |

## <a name="copy-activity-properties"></a>Propriedades da atividade de cópia
Se estiver a mover dados de uma base de dados do SQL Server, definir o tipo de origem Olá na atividade de cópia de Olá demasiado**SqlSource**. Da mesma forma, se estiver a mover dados tooa do SQL Server da base de dados, definir o tipo de sink Olá na atividade de cópia de Olá demasiado**SqlSink**. Esta secção fornece uma lista de propriedades suportadas por SqlSource e SqlSink.

Para uma lista completa das secções & Propriedades disponíveis para definir as atividades, consulte Olá [criar Pipelines](data-factory-create-pipelines.md) artigo. Propriedades, tais como o nome, descrição e de saída, tabelas e as políticas estão disponíveis para todos os tipos de atividades.

> [!NOTE]
> Olá atividade de cópia demora apenas uma entrada e produz saída de apenas um.

Enquanto, propriedades disponíveis na secção de typeProperties Olá da atividade de Olá variar de acordo com cada tipo de atividade. Para a atividade de cópia, podem variam consoante os tipos de origens e sinks Olá.

### <a name="sqlsource"></a>SqlSource
Quando a origem de uma atividade de cópia é do tipo **SqlSource**, Olá seguintes propriedades está disponível no **typeProperties** secção:

| Propriedade | Descrição | Valores permitidos | Necessário |
| --- | --- | --- | --- |
| sqlReaderQuery |Utilize Olá consulta personalizada tooread dados. |Cadeia de consulta SQL. Por exemplo: selecionar * de MyTable. Pode referenciar várias tabelas da base de dados de Olá referenciada pelo conjunto de dados de entrada Olá. Se não for especificado, Olá instrução de SQL que é executada: selecione a partir de MyTable. |Não |
| sqlReaderStoredProcedureName |Nome da Olá armazenado procedimento que lê dados a partir da tabela de origem Olá. |Nome do Olá procedimento armazenado. Olá última instrução de SQL tem de ser uma instrução SELECT no procedimento de Olá armazenado. |Não |
| storedProcedureParameters |Parâmetros para Olá procedimento armazenado. |Pares nome/valor. Nomes e maiúsculas e minúsculas de parâmetros têm de corresponder nomes Olá e maiúsculas e minúsculas de parâmetros de procedimento armazenado de Olá. |Não |

Se hello **sqlReaderQuery** especificado para Olá SqlSource, hello atividade de cópia executa esta consulta contra Olá base de dados do SQL Server origem tooget Olá de dados.

Em alternativa, pode especificar um procedimento armazenado especificando Olá **sqlReaderStoredProcedureName** e **storedProcedureParameters** (se hello procedimento armazenado recebe parâmetros).

Se não especificar sqlReaderQuery ou sqlReaderStoredProcedureName, colunas Olá definidas na secção de estrutura de Olá são utilizado toobuild toorun uma consulta select contra Olá base de dados do SQL Server. Se a definição do conjunto de dados de Olá não tem uma estrutura de Olá, todas as colunas são selecionadas da tabela de Olá.

> [!NOTE]
> Quando utiliza **sqlReaderStoredProcedureName**, terá ainda de toospecify um valor para Olá **tableName** propriedade no conjunto de dados Olá JSON. Não existem nenhum validações executadas apesar desta tabela.

### <a name="sqlsink"></a>SqlSink
**SqlSink** suporta Olá seguintes propriedades:

| Propriedade | Descrição | Valores permitidos | Necessário |
| --- | --- | --- | --- |
| writeBatchTimeout |De tempo de espera para toocomplete de operação de inserção de lote Olá antes de atingir o tempo limite. |TimeSpan<br/><br/> Exemplo: "00: 30:00" (30 minutos). |Não |
| WriteBatchSize |Insere dados na tabela SQL Olá quando o tamanho de memória intermédia de Olá atingir writeBatchSize. |Número inteiro (número de linhas) |Não (predefinição: 10000) |
| sqlWriterCleanupScript |Especifique a consulta para a atividade de cópia tooexecute, de modo a que os dados de um setor específico é limpa. Para obter mais informações, consulte [cópia repetíveis](#repeatable-copy) secção. |Uma instrução de consulta. |Não |
| sliceIdentifierColumnName |Especifique o nome de coluna para toofill de atividade de cópia com o identificador de setor automaticamente gerado, que é utilizado tooclean dos dados de um setor específico quando voltar a executar. Para obter mais informações, consulte [cópia repetíveis](#repeatable-copy) secção. |Nome da coluna de uma coluna com o tipo de dados de binary(32). |Não |
| sqlWriterStoredProcedureName |Nome do Olá procedimento armazenado dados upserts (inserções/atualizações) na tabela de destino Olá. |Nome do Olá procedimento armazenado. |Não |
| storedProcedureParameters |Parâmetros para Olá procedimento armazenado. |Pares nome/valor. Nomes e maiúsculas e minúsculas de parâmetros têm de corresponder nomes Olá e maiúsculas e minúsculas de parâmetros de procedimento armazenado de Olá. |Não |
| sqlWriterTableType |Especifique toobe de nome de tipo de tabela utilizado no procedimento de Olá armazenado. Atividade de cópia disponibiliza uma dados Olá a ser movidos numa tabela temporária com este tipo de tabela. Código do procedimento armazenado, em seguida, pode intercalar dados de Olá a ser copiados com dados existentes. |Um nome de tipo de tabela. |Não |


## <a name="json-examples-for-copying-data-from-and-toosql-server"></a>Exemplos JSON para copiar dados e tooSQL servidor
Olá exemplos seguintes fornecem definições JSON de exemplo que pode utilizar toocreate um pipeline utilizando [portal do Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) ou [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) ou [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md). Olá, os seguintes exemplos mostram como toocopy tooand de dados do SQL Server e o armazenamento de Blobs do Azure. No entanto, os dados podem ser copiados **diretamente** de qualquer uma das origens tooany de Olá sinks indicado [aqui](data-factory-data-movement-activities.md#supported-data-stores-and-formats) utilizando Olá atividade de cópia no Azure Data Factory.     

## <a name="example-copy-data-from-sql-server-tooazure-blob"></a>Exemplo: Copiar dados do SQL Server tooAzure Blob
Olá seguinte exemplo mostra:

1. Um serviço ligado do tipo [OnPremisesSqlServer](#linked-service-properties).
2. Um serviço ligado do tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
3. Uma entrada [dataset](data-factory-create-datasets.md) do tipo [SqlServerTable](#dataset-properties).
4. Uma saída [dataset](data-factory-create-datasets.md) do tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
5. Olá [pipeline](data-factory-create-pipelines.md) com atividade de cópia que utiliza [SqlSource](#copy-activity-properties) e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).

exemplo de Olá copia dados de séries de tempo de um tooan de tabela do SQL Server BLOBs do Azure a cada hora. Propriedades JSON de Olá utilizadas nestes exemplos são descritas nas secções seguintes exemplos de Olá.

Como primeiro passo, o programa de configuração Olá o data management gateway. instruções de Olá estão em Olá [mover dados entre localizações no local e nuvem](data-factory-move-data-between-onprem-and-cloud.md) artigo.

**Serviço ligado do SQL Server**
```json
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
**Serviço de ligado do armazenamento de Blobs do Azure**

```json
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
**Conjunto de dados de entrada do SQL Server**

exemplo de Olá pressupõe que criou uma tabela "MyTable" no SQL Server e contém uma coluna chamada "timestampcolumn" para dados de séries de tempo. Pode consultar através de várias tabelas na Olá mesma base de dados com um único conjunto de dados, mas uma única tabela tem de ser utilizado para typeProperty tableName de Olá conjunto de dados.

A definição "external": "true" informa serviço Data Factory esse conjunto de dados de Olá é toohello externo fábrica de dados e não é produzido por uma atividade no factory de dados de Olá.

```json
{
  "name": "SqlServerInput",
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
**Conjunto de dados de saída de Blobs do Azure**

São escritos dados no blob tooa de novo a cada hora (frequência: hora, intervalo: 1). caminho da pasta Olá para BLOBs Olá dinamicamente é avaliado com base na hora de início de Olá do setor de Olá que está a ser processado. caminho da pasta Olá utiliza ano, mês, dia e horas partes Olá da hora de início.

```json
{
  "name": "AzureBlobOutput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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
      "format": {
        "type": "TextFormat",
        "columnDelimiter": "\t",
        "rowDelimiter": "\n"
      }
    },
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```
**Pipeline com atividade de cópia**

pipeline de Olá contém uma atividade de cópia que está configurado toouse estes conjuntos de dados de entrada e de saída e toorun agendada a cada hora. No pipeline de Olá definição JSON, Olá **origem** tipo está definido demasiado**SqlSource** e **sink** tipo está definido demasiado**BlobSink**. consulta SQL Olá especificada para Olá **SqlReaderQuery** propriedade seleciona dados Olá Olá passado toocopy de hora.

```json
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2016-06-01T18:00:00",
    "end":"2016-06-01T19:00:00",
    "description":"pipeline for copy activity",
    "activities":[  
      {
        "name": "SqlServertoBlob",
        "description": "copy activity",
        "type": "Copy",
        "inputs": [
          {
            "name": " SqlServerInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureBlobOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "SqlSource",
            "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
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
Neste exemplo, **sqlReaderQuery** especificado para Olá SqlSource. Olá atividade de cópia executa esta consulta contra Olá base de dados do SQL Server origem tooget Olá de dados. Em alternativa, pode especificar um procedimento armazenado especificando Olá **sqlReaderStoredProcedureName** e **storedProcedureParameters** (se hello procedimento armazenado recebe parâmetros). Olá sqlReaderQuery pode fazer referência a várias tabelas na base de dados de Olá referenciada pelo conjunto de dados de entrada Olá. Não é limitado tooonly tabela de Olá definida como Olá typeProperty tableName de conjunto de dados.

Se não especificar sqlReaderQuery ou sqlReaderStoredProcedureName, colunas Olá definidas na secção de estrutura de Olá são utilizado toobuild toorun uma consulta select contra Olá base de dados do SQL Server. Se a definição do conjunto de dados de Olá não tem uma estrutura de Olá, todas as colunas são selecionadas da tabela de Olá.

Consulte Olá [origem Sql](#sqlsource) secção e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) para Olá obter lista de propriedades suportadas por SqlSource e BlobSink.

## <a name="example-copy-data-from-azure-blob-toosql-server"></a>Exemplo: Copiar dados de Blobs do Azure tooSQL servidor
Olá seguinte exemplo mostra:

1. serviço do tipo de ligado a Olá [OnPremisesSqlServer](#linked-service-properties).
2. serviço do tipo de ligado a Olá [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
3. Uma entrada [dataset](data-factory-create-datasets.md) do tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
4. Uma saída [dataset](data-factory-create-datasets.md) do tipo [SqlServerTable](data-factory-sqlserver-connector.md#dataset-properties).
5. Olá [pipeline](data-factory-create-pipelines.md) com atividade de cópia que utiliza [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) e [SqlSink](#sql-server-copy-activity-type-properties).

exemplo de Olá copia dados de séries de tempo de uma tabela de SQL Server do blob do Azure tooa a cada hora. Propriedades JSON de Olá utilizadas nestes exemplos são descritas nas secções seguintes exemplos de Olá.

**Serviço ligado do SQL Server**

```json
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
**Serviço de ligado do armazenamento de Blobs do Azure**

```json
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
**Conjunto de dados de entrada Blob do Azure**

Dados são captados um blob de novo a cada hora (frequência: hora, intervalo: 1). Olá pasta caminho e nome de ficheiro para o blob Olá dinamicamente são avaliados com base na hora de início de Olá do setor de Olá que está a ser processado. caminho da pasta Olá utiliza ano, mês e parte de dia da hora de início de Olá e nome de ficheiro utiliza a parte de hora Olá Olá da hora de início. "external": "true" definição informa o serviço do Data Factory Olá, esse conjunto de dados de Olá é toohello externo fábrica de dados e não é produzido por uma atividade no factory de dados de Olá.

```json
{
  "name": "AzureBlobInput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}",
      "fileName": "{Hour}.csv",
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
**Conjunto de dados de saída de SQL Server**

exemplo de Olá copia a tabela de tooa de dados com o nome "MyTable" no SQL Server. Criar tabela Olá no SQL Server com Olá o mesmo número de colunas como esperado Olá Blob CSV ficheiro toocontain. Novas linhas são adicionadas toohello tabela cada hora.

```json
{
  "name": "SqlServerOutput",
  "properties": {
    "type": "SqlServerTable",
    "linkedServiceName": "SqlServerLinkedService",
    "typeProperties": {
      "tableName": "MyOutputTable"
    },
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```
**Pipeline com atividade de cópia**

pipeline de Olá contém uma atividade de cópia que está configurado toouse estes conjuntos de dados de entrada e de saída e toorun agendada a cada hora. No pipeline de Olá definição JSON, Olá **origem** tipo está definido demasiado**BlobSource** e **sink** tipo está definido demasiado**SqlSink**.

```json
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline with copy activity",
    "activities":[  
      {
        "name": "AzureBlobtoSQL",
        "description": "Copy Activity",
        "type": "Copy",
        "inputs": [
          {
            "name": "AzureBlobInput"
          }
        ],
        "outputs": [
          {
            "name": " SqlServerOutput "
          }
        ],
        "typeProperties": {
          "source": {
            "type": "BlobSource",
            "blobColumnSeparators": ","
          },
          "sink": {
            "type": "SqlSink"
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

## <a name="troubleshooting-connection-issues"></a>Resolução de problemas de ligação
1. Configure as ligações remotas de tooaccept do SQL Server. Iniciar **SQL Server Management Studio**, faça duplo clique **servidor**e clique em **propriedades**. Selecione **ligações** partir da lista de Olá e verificação **servidor do permitir ligações remotas toohello**.

    ![Ativar ligações remotas](./media/data-factory-sqlserver-connector/AllowRemoteConnections.png)

    Consulte [configurar o acesso remoto de Olá opção de configuração do servidor](https://msdn.microsoft.com/library/ms191464.aspx) para obter passos detalhados.
2. Iniciar **Gestor de configuração do SQL Server**. Expanda **configuração de rede do SQL Server** para Olá instância pretende e selecione **protocolos para MSSQLSERVER**. Deverá ver protocolos no painel direito Olá. Ative TCP/IP clicando **TCP/IP** e clicando em **ativar**.

    ![Ative TCP/IP](./media/data-factory-sqlserver-connector/EnableTCPProptocol.png)

    Consulte [ativar ou desativar um protocolo de rede do servidor](https://msdn.microsoft.com/library/ms191294.aspx) para obter detalhes e alternativas formas de ativar o protocolo TCP/IP.
3. Na mesma janela de Olá, faça duplo clique **TCP/IP** toolaunch **propriedades de TCP/IP** janela.
4. Comutador toohello **endereços IP** separador. Desloque para baixo toosee **IPAll** secção. Tome nota dos Olá * * a porta TCP * * (predefinição é **1433**).
5. Criar um **regra de Firewall do Windows de Olá** no Olá máquina tooallow tráfego de entrada através desta porta.  
6. **Verificar ligação**: tooconnect toohello SQL Server com o nome completamente qualificado, utilize o SQL Server Management Studio de um computador diferente. Por exemplo: "<machine>.<domain>. Corp.<company>empresa>.com, 1433. "

   > [!IMPORTANT]

   > Consulte [mover dados entre origens no local e nuvem de Olá com o Data Management Gateway](data-factory-move-data-between-onprem-and-cloud.md) para obter informações detalhadas.
   >
   > Consulte [resolver problemas de gateway](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) para dicas sobre/gateway de ligação de resolução de problemas relacionados com problemas.
   >
   >


## <a name="identity-columns-in-hello-target-database"></a>Colunas de identidade na base de dados de destino de Olá
Esta secção fornece um exemplo que copia dados a partir de uma tabela de origem com a tabela de destino não identidade coluna tooa com uma coluna de identidade.

**Tabela de origem:**

```sql
create table dbo.SourceTbl
(
       name varchar(100),
       age int
)
```
**Tabela de destino:**

```sql
create table dbo.TargetTbl
(
       identifier int identity(1,1),
       name varchar(100),
       age int
)
```

Tenha em atenção de que a tabela de destino que Olá tem uma coluna de identidade.

**Definição de JSON do conjunto de dados de origem**

```json
{
    "name": "SampleSource",
    "properties": {
        "published": false,
        "type": " SqlServerTable",
        "linkedServiceName": "TestIdentitySQL",
        "typeProperties": {
            "tableName": "SourceTbl"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {}
    }
}
```
**Definição de JSON do conjunto de dados de destino**

```json
{
    "name": "SampleTarget",
    "properties": {
        "structure": [
            { "name": "name" },
            { "name": "age" }
        ],
        "published": false,
        "type": "AzureSqlTable",
        "linkedServiceName": "TestIdentitySQLSource",
        "typeProperties": {
            "tableName": "TargetTbl"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": false,
        "policy": {}
    }
}
```

Tenha em atenção que, como a tabela de origem e destino têm esquemas diferentes (o destino tem uma coluna adicional com a identidade). Neste cenário, terá de toospecify **estrutura** propriedade na definição do conjunto de dados de Olá destino, que não inclui a coluna de identidade Olá.

## <a name="invoke-stored-procedure-from-sql-sink"></a>Invocar um procedimento armazenado do sink do SQL Server
Consulte [invocar um procedimento armazenado para sink do SQL Server na atividade de cópia](data-factory-invoke-stored-procedure-from-copy-activity.md) artigo para obter um exemplo de invocar um procedimento armazenado do sink do SQL Server numa atividade de cópia de um pipeline.

## <a name="type-mapping-for-sql-server"></a>Mapeamento de tipos para o SQL server
Tal como mencionado na Olá [atividades de movimentos de dados](data-factory-data-movement-activities.md) artigo, Olá atividade de cópia executa conversões de tipo automática dos tipos de toosink de tipos de origem com Olá seguir abordagem de passo 2:

1. Converter do tipo de too.NET de tipos de origem nativo
2. Converter do tipo de sink de toonative de tipo .NET

Quando mover dados demasiado & do SQL server, Olá mapeamentos seguintes são utilizados do tipo de too.NET do tipo SQL e vice-versa.

o mapeamento de Olá é igual ao hello mapeamento do tipo de dados do SQL Server para ADO.NET.

| Tipo de motor de base de dados do SQL Server | Tipo de .NET framework |
| --- | --- |
| bigint |Int64 |
| Binário |Byte] |
| bits |Valor booleano |
| char |Cadeia, Char [] |
| Data |DateTime |
| DateTime |DateTime |
| datetime2 |DateTime |
| Datetimeoffset |DateTimeOffset |
| Decimal |Decimal |
| Atributo FILESTREAM (varbinary(max)) |Byte] |
| Número de vírgula flutuante |duplo |
| Imagem |Byte] |
| Int |Int32 |
| dinheiro |Decimal |
| nchar |Cadeia, Char [] |
| ntext |Cadeia, Char [] |
| um valor numérico |Decimal |
| nvarchar |Cadeia, Char [] |
| real |Único |
| ROWVERSION |Byte] |
| smalldatetime |DateTime |
| smallint |Int16 |
| em smallmoney |Decimal |
| sql_variant |Objeto * |
| Texto |Cadeia, Char [] |
| hora |TimeSpan |
| carimbo de data/hora |Byte] |
| tinyint |Bytes |
| uniqueidentifier |GUID |
| varbinary |Byte] |
| varchar |Cadeia, Char [] |
| xml |XML |

## <a name="mapping-source-toosink-columns"></a>Mapeamento de colunas de toosink de origem
colunas de toomap toocolumns de conjunto de dados de origem do conjunto de dados dependente, consulte [mapeamento de colunas do conjunto de dados no Azure Data Factory](data-factory-map-columns.md).

## <a name="repeatable-copy"></a>Cópia repetíveis
Quando copiar dados tooSQL base de dados do servidor, a atividade de cópia de Olá acrescenta tabela do sink de toohello de dados por predefinição. em vez disso, consulte tooperform um UPSERT [escrita repetíveis tooSqlSink](data-factory-repeatable-copy.md#repeatable-write-to-sqlsink) artigo. 

Quando copiar dados de arquivos de dados relacional, manter a repetibilidade em mente tooavoid resultados inesperados. No Azure Data Factory, pode voltar a executar um setor manualmente. Também pode configurar a política de repetição para um conjunto de dados para que um setor será novamente executado quando ocorre uma falha. Quando um setor é voltar a executar qualquer forma, terá de toomake certificar-se de que Olá mesmos dados é de leitura como não independentemente do número de vezes que um setor é executado. Consulte [Repeatable ler a partir de origens relacionais](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).

## <a name="performance-and-tuning"></a>Desempenho e a otimização
Consulte [desempenho de atividade de cópia & otimização guia](data-factory-copy-activity-performance.md) toolearn sobre chave factors desse desempenho impacto de movimento de dados (atividade de cópia) no Azure Data Factory e várias formas toooptimize-lo.
