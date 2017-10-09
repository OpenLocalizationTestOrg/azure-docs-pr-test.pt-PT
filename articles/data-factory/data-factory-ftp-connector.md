---
title: dados de aaaMove de um servidor FTP utilizando o Azure Data Factory | Microsoft Docs
description: Saiba mais sobre como dados de toomove de um servidor FTP utilizando o Azure Data Factory.
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: eea3bab0-a6e4-4045-ad44-9ce06229c718
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: jingwang
ms.openlocfilehash: c707e29532b2a8a870603948cb6150ab857bd6ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-an-ftp-server-by-using-azure-data-factory"></a>Mover dados de um servidor de FTP utilizando o Azure Data Factory
Este artigo explica como toouse Olá atividade de cópia de dados do Azure Data Factory toomove de um servidor FTP. Baseia-se no Olá [atividades de movimentos de dados](data-factory-data-movement-activities.md) artigo, que apresenta uma descrição geral do movimento de dados com a atividade de cópia de Olá.

Pode copiar dados de um arquivo de dados de receptor de tooany suportado de servidor FTP. Para obter uma lista dos dados arquivos suportados como sinks pela atividade de cópia de Olá, consulte Olá [arquivos de dados suportados](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabela. Fábrica de dados suporta atualmente só armazena dados movimento de dados de tooother do servidor de FTP, mas não mover dados de outros dados armazena servidor tooan FTP. Suporta tanto no local e na nuvem servidores FTP.

> [!NOTE]
> atividade de cópia de Olá não eliminar o ficheiro de origem Olá depois de estes destino toohello copiados com êxito. Se precisar de ficheiro de origem do toodelete Olá depois de uma cópia com êxito, crie um ficheiro de Olá toodelete atividade personalizada e utilize a atividade de Olá no pipeline de Olá. 

## <a name="enable-connectivity"></a>Ativar a conectividade
Se estiver a mover dados a partir de um **no local** arquivo de dados na nuvem de tooa de servidor FTP (por exemplo, a tooAzure armazenamento de BLOBs), instalar e utilizar o Data Management Gateway. Olá Data Management Gateway é um agente de cliente que está instalado no seu computador local e permite recurso da nuvem serviços tooconnect tooan no local. Para obter mais informações, consulte [Data Management Gateway](data-factory-data-management-gateway.md). Para obter instruções passo a passo sobre como configurar o gateway de Olá e utilizá-lo, consulte [mover dados entre localizações no local e nuvem](data-factory-move-data-between-onprem-and-cloud.md). Utilizar Olá gateway tooconnect tooan FTP server, mesmo que esteja servidor Olá numa infraestrutura do Azure como uma máquina virtual (VM) do serviço (IaaS).

É possível tooinstall gateway de Olá Olá mesmo no local da máquina ou VM do IaaS como hello do servidor de FTP. No entanto, recomendamos que instale o gateway de Olá num computador separado ou contenção de recursos do VM do IaaS tooavoid e para um melhor desempenho. Quando instalar o gateway de Olá num computador separado, máquina Olá deve ser o servidor de FTP possam tooaccess Olá.

## <a name="get-started"></a>Introdução
Pode criar um pipeline com uma atividade de cópia move dados a partir de uma origem FTP utilizando ferramentas diferentes ou APIs.

Olá toocreate da forma mais fácil um pipeline está toouse Olá **Assistente de cópia do Data Factory**. Consulte [Tutorial: criar um pipeline com o Assistente para copiar](data-factory-copy-data-wizard-tutorial.md) para instruções rápidas.

Também pode utilizar Olá seguintes ferramentas toocreate um pipeline: **portal do Azure**, **Visual Studio**, **PowerShell**, **modelo Azure Resource Manager**, **.NET API**, e **REST API**. Consulte [tutorial de atividade de cópia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para instruções passo a passo toocreate um pipeline com uma atividade de cópia.

Se utilizar ferramentas de Olá ou APIs, execute Olá os seguintes passos toocreate um pipeline que move o arquivo de dados do tooa sink do arquivo de dados de uma origem de dados:

1. Criar **serviços ligados** fábrica de dados de tooyour de arquivos de dados de entrada e saída de toolink.
2. Criar **conjuntos de dados** toorepresent de entrada e saída de operação de cópia de dados para Olá.
3. Criar um **pipeline** com uma atividade de cópia executa um conjunto de dados como entrada e um conjunto de dados como resultado.

Quando utiliza o Assistente de Olá, definições de JSON para estas entidades do Data Factory (serviços ligados, conjuntos de dados e pipeline Olá) são criadas automaticamente para si. Quando utilizar APIs (exceto .NET API) ou ferramentas, é possível definir estas entidades do Data Factory utilizando o formato JSON Olá. Para um exemplo com definições de JSON para entidades do Data Factory que são utilizados toocopy dados de um arquivo de dados do FTP, consulte Olá [exemplo JSON: copiar dados de blob de tooAzure do servidor FTP](#json-example-copy-data-from-ftp-server-to-azure-blob) secção deste artigo.

> [!NOTE]
> Para obter detalhes sobre toouse de formatos de ficheiro e compressão suportado, consulte [formatos de ficheiro e compressão no Azure Data Factory](data-factory-supported-file-and-compression-formats.md).

Olá seguintes secções fornece detalhes sobre as propriedades JSON que são utilizados toodefine entidades de fábrica de dados tooFTP específico.

## <a name="linked-service-properties"></a>Propriedades de serviço ligado
Olá, a tabela seguinte descreve o serviço FTP ligado JSON elementos tooan específico.

| Propriedade | Descrição | Necessário | Predefinição |
| --- | --- | --- | --- |
| tipo |Defina este tooFtpServer. |Sim |&nbsp; |
| anfitrião |Especifique o nome de Olá ou endereço IP do servidor FTP Olá. |Sim |&nbsp; |
| authenticationType |Especifique o tipo de autenticação de Olá. |Sim |Anónimo, básico |
| o nome de utilizador |Especificar utilizador Olá com o servidor de FTP toohello de acesso. |Não |&nbsp; |
| palavra-passe |Especifique Olá palavra-passe do utilizador Olá (nome de utilizador). |Não |&nbsp; |
| encryptedCredential |Especifica Olá encriptado credencial tooaccess Olá FTP servidor. |Não |&nbsp; |
| gatewayName |Especifique o nome de Olá do gateway de Olá no servidor FTP do Data Management Gateway tooconnect tooan no local. |Não |&nbsp; |
| porta |Especifique a porta de Olá no qual Olá FTP servidor está a escutar. |Não |21 |
| enableSsl |Especifique se toouse FTP através de um canal SSL/TLS. |Não |VERDADEIRO |
| enableServerCertificateValidation |Especifique se o servidor tooenable SSL certificado validação quando estiver a utilizar FTP através do canal SSL/TLS. |Não |VERDADEIRO |

### <a name="use-anonymous-authentication"></a>Utilize a autenticação anónima

```JSON
{
    "name": "FTPLinkedService",
    "properties": {
        "type": "FtpServer",
        "typeProperties": {        
            "authenticationType": "Anonymous",
              "host": "myftpserver.com"
        }
    }
}
```

### <a name="use-username-and-password-in-plain-text-for-basic-authentication"></a>Utilize o nome de utilizador e palavra-passe em texto simples para a autenticação básica

```JSON
{
    "name": "FTPLinkedService",
      "properties": {
    "type": "FtpServer",
        "typeProperties": {
            "host": "myftpserver.com",
            "authenticationType": "Basic",
            "username": "Admin",
            "password": "123456"
        }
      }
}
```

### <a name="use-port-enablessl-enableservercertificatevalidation"></a>Utilizar porta, enableSsl, enableServerCertificateValidation

```JSON
{
    "name": "FTPLinkedService",
    "properties": {
        "type": "FtpServer",
        "typeProperties": {
            "host": "myftpserver.com",
            "authenticationType": "Basic",    
            "username": "Admin",
            "password": "123456",
            "port": "21",
            "enableSsl": true,
            "enableServerCertificateValidation": true
        }
    }
}
```

### <a name="use-encryptedcredential-for-authentication-and-gateway"></a>Utilizar encryptedCredential para autenticação e de gateway

```JSON
{
    "name": "FTPLinkedService",
    "properties": {
        "type": "FtpServer",
        "typeProperties": {
            "host": "myftpserver.com",
            "authenticationType": "Basic",
            "encryptedCredential": "xxxxxxxxxxxxxxxxx",
            "gatewayName": "mygateway"
        }
      }
}
```

## <a name="dataset-properties"></a>Propriedades do conjunto de dados
Para uma lista completa das secções e propriedades disponíveis para definir os conjuntos de dados, consulte [criar conjuntos de dados](data-factory-create-datasets.md). As secções, tais como a estrutura, a disponibilidade e a política de um conjunto de dados JSON são semelhantes para todos os tipos de conjunto de dados.

Olá **typeProperties** secção é diferente para cada tipo de conjunto de dados. Fornece informações que é o tipo de conjunto de toohello específico. Olá **typeProperties** secção para um conjunto de dados do tipo **FileShare** tem Olá seguintes propriedades:

| Propriedade | Descrição | Necessário |
| --- | --- | --- |
| folderPath |Pasta de toohello Subcaminho. Utilize o caráter de escape ' \ ' para carateres especiais na cadeia de Olá. Consulte [exemplo ligado definições de serviço e o conjunto de dados](#sample-linked-service-and-dataset-definitions) para obter exemplos.<br/><br/>Pode combinar esta propriedade com **partitionBy** toohave caminhos de pastas com base no setor começar e terminar tempos de data. |Sim |
| fileName |Especifique o nome de Olá do ficheiro de Olá no Olá **folderPath** se quiser Olá tabela toorefer tooa específico ficheiro na pasta Olá. Se não for especificado qualquer valor para esta propriedade, tabela Olá pontos tooall ficheiros na pasta Olá.<br/><br/>Quando **fileName** não está especificado para um conjunto de dados de saída, Olá do ficheiro de Olá gerado está a ser Olá seguinte formato: <br/><br/>Dados. <Guid>. txt (exemplo: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt) |Não |
| fileFilter |Especifique um tooselect toobe utilizado de filtro um subconjunto de ficheiros no Olá **folderPath**, em vez de todos os ficheiros.<br/><br/>Valores permitidos são: `*` (vários carateres) e `?` (único caráter).<br/><br/>Exemplo 1:`"fileFilter": "*.log"`<br/>Exemplo 2:`"fileFilter": 2014-1-?.txt"`<br/><br/> **fileFilter** se aplica a um conjunto de dados de partilha de ficheiros de entrada. Esta propriedade não é suportada com distribuído ficheiro sistema Hadoop (HDFS). |Não |
| partitionedBy |Utilizado toospecify um dinâmico **folderPath** e **fileName** para dados de séries de tempo. Por exemplo, pode especificar um **folderPath** que é parametrizada para cada hora dos dados. |Não |
| formato | é suportado os seguintes tipos de formato de Olá: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**. Conjunto Olá **tipo** propriedade em formato tooone destes valores. Para obter mais informações, consulte Olá [formato de texto](data-factory-supported-file-and-compression-formats.md#text-format), [formato Json](data-factory-supported-file-and-compression-formats.md#json-format), [formato Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc formato](data-factory-supported-file-and-compression-formats.md#orc-format), e [Parquet formato ](data-factory-supported-file-and-compression-formats.md#parquet-format) secções. <br><br> Se pretender que os ficheiros de toocopy conforme forem entre arquivos baseados em ficheiros (cópia binário), ignore a secção de formato de Olá em ambas as definições do conjunto de dados de entrada e de saída. |Não |
| Compressão | Especifique o tipo de Olá e nível de compressão de dados de Olá. Tipos suportados são **GZip**, **Deflate**, **BZip2**, e **ZipDeflate**, e níveis suportados são **Optimal** e **Fastest**. Para obter mais informações, consulte [formatos de ficheiro e compressão no Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support). |Não |
| useBinaryTransfer |Especifique se binário de Olá toouse modo de transferência. valores de Olá forem verdadeiros para o modo binário (este é o valor predefinido de Olá) ou FALSO para ASCII. Esta propriedade só pode ser utilizada quando hello tipo de serviço ligado associado é do tipo: FtpServer. |Não |

> [!NOTE]
> **nome de ficheiro** e **fileFilter** não podem ser utilizados em simultâneo.

### <a name="use-hello-partionedby-property"></a>Utilize a propriedade de partionedBy Olá
Tal como mencionado na secção anterior Olá, pode especificar um dinâmico **folderPath** e **fileName** para dados de séries de tempo com Olá **partitionedBy** propriedade.

toolearn sobre conjuntos de dados de séries de tempo, agendar e setores, consulte [criar conjuntos de dados](data-factory-create-datasets.md), [agendamento e execução](data-factory-scheduling-and-execution.md), e [Criar pipelines](data-factory-create-pipelines.md).

#### <a name="sample-1"></a>Exemplo 1

```json
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```
Neste exemplo, {setor} é substituído pelo valor Olá da variável de sistema do Data Factory SliceStart, no Olá Formatar especificado (YYYYMMDDHH). Olá SliceStart refere-se a hora de toostart do setor Olá. caminho da pasta Olá é diferente para cada setor. (Por exemplo, wikidatagateway/wikisampledataout/2014100103 ou wikidatagateway/wikisampledataout/2014100104)

#### <a name="sample-2"></a>Exemplo 2

```json
"folderPath": "wikidatagateway/wikisampledataout/{Year}/{Month}/{Day}",
"fileName": "{Hour}.csv",
"partitionedBy":
 [
    { "name": "Year", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyy" } },
    { "name": "Month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
    { "name": "Day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } },
    { "name": "Hour", "value": { "type": "DateTime", "date": "SliceStart", "format": "hh" } }
],
```
Neste exemplo, são extraídos Olá ano, mês, dia e hora do SliceStart em separado variáveis que são utilizadas por Olá **folderPath** e **fileName** propriedades.

## <a name="copy-activity-properties"></a>Propriedades da atividade de cópia
Para uma lista completa das secções e propriedades disponíveis para definir as atividades, consulte [Criar pipelines](data-factory-create-pipelines.md). Propriedades, tais como o nome, descrição e de saída, tabelas e as políticas estão disponíveis para todos os tipos de atividades.

Propriedades disponíveis nos Olá **typeProperties** secção Olá atividade, no Olá por outro lado, variar de acordo com cada tipo de atividade. Para a atividade de cópia de Olá, propriedades do tipo Olá variam consoante os tipos de origens e sinks Olá.

Na atividade de cópia, quando a origem de Olá é do tipo **FileSystemSource**, Olá seguinte propriedade está disponível no **typeProperties** secção:

| Propriedade | Descrição | Valores permitidos | Necessário |
| --- | --- | --- | --- |
| Recursiva |Indica se Olá é ler dados em modo recursivo de subpastas hello, ou apenas a partir da pasta especificada Olá. |TRUE, False (predefinição) |Não |

## <a name="json-example-copy-data-from-ftp-server-tooazure-blob"></a>Exemplo JSON: copiar dados do servidor FTP tooAzure Blob
Este exemplo mostra como toocopy dados a partir de um tooAzure de servidor FTP armazenamento de Blobs. No entanto, é possível copiar dados diretamente tooany de Olá sinks Olá declarado no [arquivos de dados e formatos suportados](data-factory-data-movement-activities.md#supported-data-stores-and-formats), utilizando a atividade de cópia de Olá na fábrica de dados.  

Olá exemplos seguintes fornecem definições JSON de exemplo que pode utilizar toocreate um pipeline utilizando [portal do Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), ou [PowerShell](data-factory-copy-activity-tutorial-using-powershell.md):

* Um serviço ligado do tipo [FtpServer](#linked-service-properties)
* Um serviço ligado do tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)
* Uma entrada [dataset](data-factory-create-datasets.md) do tipo [partilha de ficheiros](#dataset-properties)
* Uma saída [dataset](data-factory-create-datasets.md) do tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties)
* A [pipeline](data-factory-create-pipelines.md) com atividade de cópia que utiliza [FileSystemSource](#copy-activity-properties) e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties)

exemplo de Olá copia dados a partir de um tooan de servidor FTP BLOBs do Azure a cada hora. Propriedades JSON de Olá utilizadas nestes exemplos são descritas nas secções seguintes exemplos de Olá.

### <a name="ftp-linked-service"></a>Serviço ligado de FTP

Este exemplo utiliza a autenticação básica, com o nome de utilizador de Olá e a palavra-passe em texto simples. Também pode utilizar um dos Olá seguintes formas:

* Autenticação anónima
* Autenticação básica com credenciais encriptado
* FTP por SSL/TLS (FTPS)

Consulte Olá [serviço ligado de FTP](#linked-service-properties) secção para diferentes tipos de autenticação, pode utilizar.

```JSON
{
    "name": "FTPLinkedService",
    "properties": {
    "type": "FtpServer",
    "typeProperties": {
        "host": "myftpserver.com",           
        "authenticationType": "Basic",
        "username": "Admin",
        "password": "123456"
    }
  }
}
```
### <a name="azure-storage-linked-service"></a>Serviço ligado do Storage do Azure

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
### <a name="ftp-input-dataset"></a>Conjunto de dados de entrada de FTP

Este conjunto de dados refere-se a pasta de toohello FTP `mysharedfolder` e ficheiro `test.csv`. Olá pipeline cópias Olá toohello o destino de ficheiro.

Definição **externo** demasiado**verdadeiro** informa o serviço do Data Factory Olá esse conjunto de dados de Olá é toohello externo fábrica de dados e não é produzido por uma atividade no factory de dados de Olá.

```JSON
{
  "name": "FTPFileInput",
  "properties": {
    "type": "FileShare",
    "linkedServiceName": "FTPLinkedService",
    "typeProperties": {
      "folderPath": "mysharedfolder",
      "fileName": "test.csv",
      "useBinaryTransfer": true
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```

### <a name="azure-blob-output-dataset"></a>Conjunto de dados de saída do Blob do Azure

São escritos dados no blob tooa de novo a cada hora (frequência: hora, intervalo: 1). caminho da pasta Olá para BLOBs Olá é avaliado dinamicamente, com base na hora de início de Olá do setor de Olá que está a ser processado. caminho da pasta Olá utiliza as partes de ano, mês, dia e horas Olá Olá da hora de início.

```JSON
{
    "name": "AzureBlobOutput",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/ftp/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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


### <a name="a-copy-activity-in-a-pipeline-with-file-system-source-and-blob-sink"></a>Uma atividade de cópia num pipeline com o sink de origem e de blob do sistema de ficheiros

Olá pipeline contém uma atividade de cópia é configurado toouse Olá conjuntos de dados de entrada e de saída, não sendo toorun agendada a cada hora. No pipeline de Olá definição JSON, Olá **origem** tipo está definido demasiado**FileSystemSource**e Olá **sink** tipo está definido demasiado**BlobSink**.

```JSON
{
    "name": "pipeline",
    "properties": {
        "activities": [{
            "name": "FTPToBlobCopy",
            "inputs": [{
                "name": "FtpFileInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "FileSystemSource"
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
                "executionPriorityOrder": "NewestFirst",
                "retry": 1,
                "timeout": "00:05:00"
            }
        }],
        "start": "2016-08-24T18:00:00Z",
        "end": "2016-08-24T19:00:00Z"
    }
}
```
> [!NOTE]
> colunas de toomap toocolumns de conjunto de dados de origem do conjunto de dados dependente, consulte [mapeamento de colunas do conjunto de dados no Azure Data Factory](data-factory-map-columns.md).

## <a name="next-steps"></a>Passos seguintes
Consulte Olá seguintes artigos:

* toolearn sobre chave factors desse desempenho impacto de movimento de dados (atividade de cópia) no Factory de dados e várias formas toooptimize-lo, consulte Olá [copiar guia Otimização e de desempenho de atividade](data-factory-copy-activity-performance.md).

* Para obter instruções passo a passo para criar um pipeline com uma atividade de cópia, consulte Olá [tutorial de atividade de cópia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).
