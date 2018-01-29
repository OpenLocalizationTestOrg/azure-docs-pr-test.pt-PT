---
title: Copiar dados de/para um sistema de ficheiros utilizando o Azure Data Factory | Microsoft Docs
description: Saiba como copiar dados de sistema de ficheiros para os arquivos de dados suportados sink (ou) de arquivos de dados de origem suportada para o sistema de ficheiros utilizando o Azure Data Factory.
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: spelluru
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 
ms.author: jingwang
ms.openlocfilehash: 8c8edc6e3d3c8330824c767f1bb02668a44e670e
ms.sourcegitcommit: 9cc3d9b9c36e4c973dd9c9028361af1ec5d29910
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 01/23/2018
---
# <a name="copy-data-to-or-from-a-file-system-by-using-azure-data-factory"></a>Copiar dados de ou para um sistema de ficheiros utilizando o Azure Data Factory
> [!div class="op_single_selector" title1="Select the version of Data Factory service you are using:"]
> * [Versão 1 - GA](v1/data-factory-onprem-file-system-connector.md)
> * [Versão 2 - Pré-visualização](connector-file-system.md)

Este artigo descreve como utilizar a atividade de cópia no Azure Data Factory para copiar dados de origem e de sistema de ficheiros. Baseia-se no [copiar descrição geral da atividade](copy-activity-overview.md) artigo que apresenta uma descrição geral da atividade de cópia.

> [!NOTE]
> Este artigo aplica-se à versão 2 do Data Factory, que está atualmente em pré-visualização. Se estiver a utilizar a versão 1 do serviço do Data Factory, o que é geralmente disponível (DG), consulte [conector sistema de ficheiros no V1](v1/data-factory-onprem-file-system-connector.md).

## <a name="supported-capabilities"></a>Capacidades suportadas

Pode copiar dados de sistema de ficheiros para qualquer arquivo de dados suportados sink ou copiar dados a partir de qualquer arquivo de dados de origem suportada para o sistema de ficheiros. Para obter uma lista dos arquivos de dados que são suportados como origens/sinks pela atividade de cópia, consulte o [arquivos de dados suportados](copy-activity-overview.md#supported-data-stores-and-formats) tabela.

Especificamente, este conector sistema de ficheiros suporta:

- Copiar ficheiros de/para partilha de ficheiros de rede ou de máquina local. Para utilizar uma partilha de ficheiros do Linux, instalar [Samba](https://www.samba.org/) no seu servidor Linux.
- Copiar ficheiros utilizando **Windows** autenticação.
- Copiar ficheiros como-está ou ficheiros com a análise/gerar o [suportado os formatos de ficheiro e compressão codecs](supported-file-formats-and-compression-codecs.md).

## <a name="prerequisites"></a>Pré-requisitos

Para copiar dados de/para um sistema de ficheiros que não está acessível publicamente, terá de configurar um tempo de execução de integração Self-hosted. Consulte [Self-hosted integração Runtime](create-self-hosted-integration-runtime.md) artigo para obter detalhes.

## <a name="getting-started"></a>Introdução

[!INCLUDE [data-factory-v2-connector-get-started](../../includes/data-factory-v2-connector-get-started.md)]

As secções seguintes fornecem detalhes sobre as propriedades que são utilizados para definir entidades do Data Factory específicas ao sistema de ficheiros.

## <a name="linked-service-properties"></a>Propriedades de serviço ligado

As seguintes propriedades são suportadas para o serviço ligado do sistema de ficheiros:

| Propriedade | Descrição | Necessário |
|:--- |:--- |:--- |
| tipo | A propriedade de tipo tem de ser definida: **servidor de ficheiros**. | Sim |
| anfitrião | Especifica o caminho da raiz da pasta que pretende copiar. Utilizar o caráter de escape "\" caracteres especiais na cadeia. Consulte [exemplo ligado definições de serviço e o conjunto de dados](#sample-linked-service-and-dataset-definitions) para obter exemplos. | Sim |
| ID de utilizador | Especifique o ID do utilizador que tem acesso ao servidor. | Sim |
| palavra-passe | Especifique a palavra-passe para o utilizador (ID de utilizador). Marcar este campo como SecureString. | Sim |
| connectVia | O [integração Runtime](concepts-integration-runtime.md) para ser utilizado para ligar ao arquivo de dados. Pode utilizar o Runtime de integração Self-hosted ou Runtime de integração do Azure (se o arquivo de dados acessível publicamente). Se não for especificado, utiliza a predefinição de Runtime de integração do Azure. |Não |

### <a name="sample-linked-service-and-dataset-definitions"></a>Serviço ligado e definições do conjunto de dados de exemplo

| Cenário | "anfitrião" na definição de serviço ligado | "folderPath" na definição do conjunto de dados |
|:--- |:--- |:--- |
| Pasta local na máquina de tempo de execução de integração: <br/><br/>Exemplos: D:\\ \* ou D:\folder\subfolder\\* |D:\\\\ |. \\ \\ ou pasta\\\\subpasta |
| Pasta partilhada remota: <br/><br/>Exemplos: \\ \\myserver\\partilhar\\ \* ou \\ \\myserver\\partilhar\\pasta\\subpasta\\* |\\\\\\\\myserver\\\\share |. \\ \\ ou pasta\\\\subpasta |

**Exemplo:**

```json
{
    "name": "FileLinkedService",
    "properties": {
        "type": "FileServer",
        "typeProperties": {
            "host": "<host>",
            "userid": "<domain>\\<user>",
            "password": {
                "type": "SecureString",
                "value": "<password>"
            }
        },
        "connectVia": {
            "referenceName": "<name of Integration Runtime>",
            "type": "IntegrationRuntimeReference"
        }
    }
}
```

## <a name="dataset-properties"></a>Propriedades do conjunto de dados

Para uma lista completa das secções e propriedades disponíveis para definir os conjuntos de dados, consulte o artigo de conjuntos de dados. Esta secção fornece uma lista de propriedades suportadas por conjunto de dados de sistema de ficheiros.

Para copiar dados de/para o sistema de ficheiros, defina a propriedade de tipo do conjunto de dados para **FileShare**. São suportadas as seguintes propriedades:

| Propriedade | Descrição | Necessário |
|:--- |:--- |:--- |
| tipo | A propriedade de tipo do conjunto de dados tem de ser definida: **partilha de ficheiros** |Sim |
| folderPath | Caminho para a pasta. Consulte [exemplo ligado definições de serviço e o conjunto de dados](#sample-linked-service-and-dataset-definitions) para obter exemplos. |Sim |
| fileName | Especifique o nome do ficheiro no **folderPath** se pretende copiar para/de um ficheiro específico. Se não for especificado qualquer valor para esta propriedade, o conjunto de dados aponta para todos os ficheiros na pasta como origem e gera automaticamente o nome de ficheiro.<br/><br/>**geração de automática de nome de ficheiro para sink:** quando o nome de ficheiro não está especificado para um conjunto de dados de saída e **preserveHierarchy** não foram especificadas no receptor de atividade, atividade de cópia gera o nome de ficheiro com o padrão do seguinte: <br/>- `Data_[activity run id]_[GUID].[format].[compression if configured]`. Por exemplo: `Data_0a405f8a-93ff-4c6f-b3be-f69616f1df7a_0d143eda-d5b8-44df-82ec-95c50895ff80.txt.gz` <br/>- ou `[Table name].[format].[compression if configured]` para origem relacional quando consulta não está especificada. Por exemplo: MySourceTable.orc. |Não |
| fileFilter | Especifique um filtro para ser utilizado para selecionar um subconjunto de ficheiros em folderPath em vez de todos os ficheiros. Aplica-se apenas ao nome de ficheiro não está especificado. <br/><br/>Permitidos carateres universais são: `*` (vários carateres) e `?` (único caráter).<br/>-Exemplo 1:`"fileFilter": "*.log"`<br/>-Exemplo 2:`"fileFilter": 2017-09-??.txt"` |Não |
| formato | Se pretender **copiar ficheiros como-é** entre arquivos baseados em ficheiros (cópia binário), ignorar a secção de formato em ambas as definições do conjunto de dados de entrada e de saída.<br/><br/>Se pretender analisar ou gerar ficheiros com um formato específico, são suportados os seguintes tipos de formato de ficheiro: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**. Definir o **tipo** propriedade de formato para um destes valores. Para obter mais informações, consulte [formato de texto](supported-file-formats-and-compression-codecs.md#text-format), [formato Json](supported-file-formats-and-compression-codecs.md#json-format), [formato Avro](supported-file-formats-and-compression-codecs.md#avro-format), [Orc formato](supported-file-formats-and-compression-codecs.md#orc-format), e [Parquet formato](supported-file-formats-and-compression-codecs.md#parquet-format) secções. |Nenhum (apenas para cenário de cópia binário) |
| Compressão | Especifique o tipo e o nível de compressão de dados. Para obter mais informações, consulte [suportado os formatos de ficheiro e compressão codecs](supported-file-formats-and-compression-codecs.md#compression-support).<br/>Tipos suportados são: **GZip**, **Deflate**, **BZip2**, e **ZipDeflate**.<br/>Níveis suportados são: **Optimal** e **Fastest**. |Não |


**Exemplo:**

```json
{
    "name": "FileSystemDataset",
    "properties": {
        "type": "FileShare",
        "linkedServiceName":{
            "referenceName": "<file system linked service name>",
            "type": "LinkedServiceReference"
        },
        "typeProperties": {
            "folderPath": "folder/subfolder/",
            "fileName": "myfile.csv.gz",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ",",
                "rowDelimiter": "\n"
            },
            "compression": {
                "type": "GZip",
                "level": "Optimal"
            }
        }
    }
}
```

## <a name="copy-activity-properties"></a>Propriedades da atividade Copy

Para uma lista completa das secções e propriedades disponíveis para definir as atividades, consulte o [Pipelines](concepts-pipelines-activities.md) artigo. Esta secção fornece uma lista de propriedades suportadas por origem de sistema de ficheiros e o sink.

### <a name="file-system-as-source"></a>Sistema de ficheiros como origem

Para copiar dados de sistema de ficheiros, defina o tipo de origem na atividade de cópia para **FileSystemSource**. As seguintes propriedades são suportadas na atividade de cópia **origem** secção:

| Propriedade | Descrição | Necessário |
|:--- |:--- |:--- |
| tipo | A propriedade de tipo da origem de atividade de cópia tem de ser definida: **FileSystemSource** |Sim |
| Recursiva | Indica se os dados é leitura recursivamente as subpastas ou apenas a pasta especificada. Nota Quando recursiva está definida como VERDADEIRO e o sink é baseado em ficheiros de arquivo, vazia pasta/sub-folder não serão copiados/criado no sink.<br/>Valores permitidos são: **verdadeiro** (predefinição), **false** | Não |

**Exemplo:**

```json
"activities":[
    {
        "name": "CopyFromFileSystem",
        "type": "Copy",
        "inputs": [
            {
                "referenceName": "<file system input dataset name>",
                "type": "DatasetReference"
            }
        ],
        "outputs": [
            {
                "referenceName": "<output dataset name>",
                "type": "DatasetReference"
            }
        ],
        "typeProperties": {
            "source": {
                "type": "FileSystemSource",
                "recursive": true
            },
            "sink": {
                "type": "<sink type>"
            }
        }
    }
]
```

### <a name="file-system-as-sink"></a>Sistema de ficheiros como sink

Para copiar dados para o sistema de ficheiros, defina o tipo de sink na atividade de cópia para **FileSystemSink**. São suportadas as seguintes propriedades no **sink** secção:

| Propriedade | Descrição | Necessário |
|:--- |:--- |:--- |
| tipo | A propriedade de tipo de sink de atividade de cópia tem de ser definida: **FileSystemSink** |Sim |
| copyBehavior | Define o comportamento de cópia quando a origem é ficheiros de arquivo de dados baseada em ficheiros.<br/><br/>Valores permitidos são:<br/><b>-PreserveHierarchy (predefinição)</b>: preserva a hierarquia de ficheiros na pasta de destino. O caminho relativo do ficheiro de origem para a pasta de origem é idêntico ao caminho relativo do ficheiro de destino para a pasta de destino.<br/><b>-FlattenHierarchy</b>: todos os ficheiros da pasta de origem estão no primeiro nível da pasta de destino. Os ficheiros de destino tem o nome de automaticamente gerado. <br/><b>-MergeFiles</b>: une todos os ficheiros da pasta de origem para um ficheiro. Se não for especificado o nome de ficheiro/Blob, o nome de ficheiro intercalado seria o nome especificado; caso contrário, seria nome de ficheiro gerada automaticamente. | Não |

**Exemplo:**

```json
"activities":[
    {
        "name": "CopyToFileSystem",
        "type": "Copy",
        "inputs": [
            {
                "referenceName": "<input dataset name>",
                "type": "DatasetReference"
            }
        ],
        "outputs": [
            {
                "referenceName": "<file system output dataset name>",
                "type": "DatasetReference"
            }
        ],
        "typeProperties": {
            "source": {
                "type": "<source type>"
            },
            "sink": {
                "type": "FileSystemSink",
                "copyBehavior": "PreserveHierarchy"
            }
        }
    }
]
```

### <a name="recursive-and-copybehavior-examples"></a>Exemplos de recursiva e copyBehavior

Esta secção descreve o comportamento resultante da operação de cópia para diferentes combinações de valores recursiva e copyBehavior.

| Recursiva | copyBehavior | Estrutura de pasta de origem | Destino resultante |
|:--- |:--- |:--- |:--- |
| true |preserveHierarchy | Pasta1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5 | a pasta de destino Pasta1 é criada com a mesma estrutura de origem:<br/><br/>Pasta1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5. |
| true |flattenHierarchy | Pasta1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5 | o destino Pasta1 é criado com a estrutura seguinte: <br/><br/>Pasta1<br/>&nbsp;&nbsp;&nbsp;&nbsp;nome gerado automaticamente para File1<br/>&nbsp;&nbsp;&nbsp;&nbsp;nome gerado automaticamente para File2<br/>&nbsp;&nbsp;&nbsp;&nbsp;nome gerado automaticamente para File3<br/>&nbsp;&nbsp;&nbsp;&nbsp;nome gerado automaticamente para File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;nome gerado automaticamente para File5 |
| true |mergeFiles | Pasta1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5 | o destino Pasta1 é criado com a estrutura seguinte: <br/><br/>Pasta1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1 + File2 + File3 + File4 + ficheiro 5 é intercalado conteúdo para um ficheiro com nome de ficheiro gerado automaticamente |
| falso |preserveHierarchy | Pasta1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5 | a pasta de destino Pasta1 é criada com a seguinte estrutura<br/><br/>Pasta1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File2<br/><br/>Não Subfolder1 com File3, File4 e File5 captado. |
| falso |flattenHierarchy | Pasta1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5 | a pasta de destino Pasta1 é criada com a seguinte estrutura<br/><br/>Pasta1<br/>&nbsp;&nbsp;&nbsp;&nbsp;nome gerado automaticamente para File1<br/>&nbsp;&nbsp;&nbsp;&nbsp;nome gerado automaticamente para File2<br/><br/>Não Subfolder1 com File3, File4 e File5 captado. |
| falso |mergeFiles | Pasta1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5 | a pasta de destino Pasta1 é criada com a seguinte estrutura<br/><br/>Pasta1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1 + File2 conteúdos são intercalados para um ficheiro com nome de ficheiro gerada automaticamente. nome gerado automaticamente para File1<br/><br/>Não Subfolder1 com File3, File4 e File5 captado. |

## <a name="next-steps"></a>Passos Seguintes
Para obter uma lista dos arquivos de dados suportados como origens e sinks pela atividade de cópia no Azure Data Factory, consulte [arquivos de dados suportados](copy-activity-overview.md##supported-data-stores-and-formats).