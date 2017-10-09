---
title: dados aaaCopy para/de um sistema de ficheiros utilizando o Azure Data Factory | Microsoft Docs
description: Saiba como toocopy tooand de dados de um sistema de ficheiros no local utilizando o Azure Data Factory.
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: ce19f1ae-358e-4ffc-8a80-d802505c9c84
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: jingwang
ms.openlocfilehash: 201b8bc3ffa639df781443aa0c3f95c975d280be
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="copy-data-tooand-from-an-on-premises-file-system-by-using-azure-data-factory"></a>Copiar tooand de dados a partir de um sistema de ficheiros no local utilizando o Azure Data Factory
Este artigo explica como toouse Olá atividade de cópia de dados de toocopy do Azure Data Factory para/de um sistema de ficheiros no local. Baseia-se no Olá [atividades de movimentos de dados](data-factory-data-movement-activities.md) artigo, que apresenta uma descrição geral do movimento de dados com a atividade de cópia de Olá.

## <a name="supported-scenarios"></a>Cenários suportados
Pode copiar dados **de um sistema de ficheiros no local** toohello seguir arquivos de dados:

[!INCLUDE [data-factory-supported-sink](../../includes/data-factory-supported-sinks.md)]

Pode copiar dados de Olá seguir arquivos de dados **tooan no local o sistema de ficheiros**:

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

> [!NOTE]
> Atividade de cópia não eliminar o ficheiro de origem Olá depois de estes destino toohello copiados com êxito. Se precisar de ficheiro de origem do toodelete Olá depois de uma cópia com êxito, crie um ficheiro de Olá toodelete atividade personalizada e utilize a atividade Olá no pipeline de Olá. 

## <a name="enabling-connectivity"></a>Ativar a conectividade
Fábrica de dados suporta tooand ligação de um sistema de ficheiros no local através de **Data Management Gateway**. Tem de instalar Olá Data Management Gateway no seu ambiente no local para Olá Data Factory service tooconnect tooany suportados no local arquivo de dados, incluindo o sistema de ficheiros. toolearn sobre o Data Management Gateway e para obter instruções passo a passo sobre como configurar o gateway de Olá, consulte [mover dados entre origens no local e nuvem de Olá com o Data Management Gateway](data-factory-move-data-between-onprem-and-cloud.md). Para além do Data Management Gateway, não existem outros ficheiros binários tem toobe instalado toocommunicate tooand de um sistema de ficheiros no local. Tem de instalar e utilizar Olá Data Management Gateway, mesmo que esteja sistema de ficheiros de Olá na VM do IaaS do Azure. Para obter informações detalhadas sobre o gateway de Olá, consulte [Data Management Gateway](data-factory-data-management-gateway.md).

instalar toouse uma partilha de ficheiros do Linux, [Samba](https://www.samba.org/) no seu servidor Linux e instalar o Data Management Gateway num servidor do Windows. Instalar o Data Management Gateway num servidor Linux não é suportada.

## <a name="getting-started"></a>Introdução
Pode criar um pipeline com uma atividade de cópia move os dados do sistema de ficheiros utilizando ferramentas diferentes/APIs.

Olá toocreate da forma mais fácil um pipeline está toouse Olá **Assistente para copiar**. Consulte [Tutorial: criar um pipeline com o Assistente para copiar](data-factory-copy-data-wizard-tutorial.md) para obter instruções sobre como criar um pipeline com o Assistente de cópia de dados Olá rápida.

Também pode utilizar Olá seguintes ferramentas toocreate um pipeline: **portal do Azure**, **Visual Studio**, **Azure PowerShell**, **modelo Azure Resource Manager** , **.NET API**, e **REST API**. Consulte [tutorial de atividade de cópia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para instruções passo a passo toocreate um pipeline com uma atividade de cópia.

Se utilizar ferramentas de Olá ou APIs, execute Olá os seguintes passos toocreate um pipeline que move o arquivo de dados do tooa sink do arquivo de dados de uma origem de dados:

1. Criar um **fábrica de dados**. Uma fábrica de dados pode conter um ou mais pipelines. 
2. Criar **serviços ligados** fábrica de dados de tooyour de arquivos de dados de entrada e saída de toolink. Por exemplo, se estiver a copiar dados de um sistema de ficheiros no local de tooan de armazenamento de Blobs do Azure, pode cria dois serviços ligados toolink o sistema de ficheiros no local e a fábrica de dados de tooyour de conta de armazenamento do Azure. As propriedades de serviço ligado que são de sistema de ficheiros no local tooan específicos, consulte [ligado propriedades do serviço](#linked-service-properties) secção.
3. Criar **conjuntos de dados** toorepresent de entrada e saída de operação de cópia de dados para Olá. Exemplo de Olá mencionado no passo último Olá, criar um contentor de blob do conjunto de dados toospecify Olá e a pasta que contém dados de entrada Olá. Além disso, crie outro conjunto de dados toospecify Olá ficheiros e pastas nome (opcional) no seu sistema de ficheiros. Para obter propriedades de conjunto de dados que são específico tooon local o sistema de ficheiros, consulte [propriedades do dataset](#dataset-properties) secção.
4. Criar um **pipeline** com uma atividade de cópia executa um conjunto de dados como entrada e um conjunto de dados como resultado. Exemplo de Olá mencionado anteriormente, que utilizar BlobSource como uma origem e FileSystemSink como um sink para atividade de cópia de Olá. Da mesma forma, se estiver a copiar tooAzure de sistema de ficheiros no local o Blob Storage, utilizar FileSystemSource e BlobSink na atividade de cópia de Olá. Para obter as propriedades da atividade de cópia são específico tooon local o sistema de ficheiros, consulte [copiar propriedades da atividade](#copy-activity-properties) secção. Para obter detalhes sobre como toouse um arquivo de dados como uma origem ou de um receptor de mensagens em fila, clique em ligação Olá na secção anterior do Olá para o arquivo de dados.

Quando utiliza o Assistente de Olá, definições de JSON para estas entidades do Data Factory (serviços ligados, conjuntos de dados e pipeline Olá) são criadas automaticamente para si. Ao utilizar ferramentas/APIs (exceto .NET API), é possível definir estas entidades do Data Factory utilizando o formato JSON Olá.  Para exemplos com definições de JSON para entidades do Data Factory que são utilizados toocopy dados para/de um sistema de ficheiros, consulte [exemplos JSON](#json-examples-for-copying-data-to-and-from-file-system) secção deste artigo.

Olá seguintes secções fornece detalhes sobre as propriedades JSON que são utilizados toodefine Data Factory entidades toofile específico sistema:

## <a name="linked-service-properties"></a>Propriedades de serviço ligado
Pode ligar uma fábrica de dados do Azure de tooan de sistema de ficheiros no local com Olá **local no servidor de ficheiros** serviço ligado. Olá, a tabela seguinte fornece descrições para os elementos JSON que são específica toohello serviço servidor de ficheiros no local ligada.

| Propriedade | Descrição | Necessário |
| --- | --- | --- |
| tipo |Certifique-se de que a propriedade de tipo Olá está definida demasiado**OnPremisesFileServer**. |Sim |
| anfitrião |Especifica o caminho da raiz da pasta de Olá que pretende que o toocopy Olá. Utilize o caráter de escape Olá ' \ ' para carateres especiais na cadeia de Olá. Consulte [exemplo ligado definições de serviço e o conjunto de dados](#sample-linked-service-and-dataset-definitions) para obter exemplos. |Sim |
| ID de utilizador |Especificar Olá ID de utilizador de Olá que tem acesso toohello servidor. |Não (se optar por encryptedCredential) |
| palavra-passe |Especifique Olá palavra-passe do utilizador Olá (userid). |Não (se optar por encryptedCredential |
| encryptedCredential |Especifique as credenciais de Olá encriptado que pode obter executando o cmdlet Olá AzureRmDataFactoryEncryptValue de novo. |Não (se optar por toospecify ID de utilizador e palavra-passe em texto simples) |
| gatewayName |Especifica o nome de Olá do gateway de Olá que fábrica de dados deve utilizar o servidor de ficheiros do tooconnect toohello no local. |Sim |


### <a name="sample-linked-service-and-dataset-definitions"></a>Serviço ligado e definições do conjunto de dados de exemplo
| Cenário | Na definição de serviço ligado do anfitrião | folderPath na definição do conjunto de dados |
| --- | --- | --- |
| Pasta local no computador do Data Management Gateway: <br/><br/>Exemplos: D:\\ \* ou D:\folder\subfolder\\* |D:\\ \\ (para o Data Management Gateway 2.0 e versões posteriores) <br/><br/> localhost (para versões anteriores a 2.0 do Data Management Gateway) |. \\ \\ ou pasta\\\\subpasta (para o Data Management Gateway 2.0 e versões posteriores) <br/><br/>D:\\ \\ ou d:\\\\pasta\\\\subpasta (para a versão do gateway abaixo 2.0) |
| Pasta partilhada remota: <br/><br/>Exemplos: \\ \\myserver\\partilhar\\ \* ou \\ \\myserver\\partilhar\\pasta\\subpasta\\* |\\\\\\\\MyServer\\\\partilhar |. \\ \\ ou pasta\\\\subpasta |


### <a name="example-using-username-and-password-in-plain-text"></a>Exemplo: Utilizar o nome de utilizador e palavra-passe em texto simples

```JSON
{
  "Name": "OnPremisesFileServerLinkedService",
  "properties": {
    "type": "OnPremisesFileServer",
    "typeProperties": {
      "host": "\\\\Contosogame-Asia",
      "userid": "Admin",
      "password": "123456",
      "gatewayName": "mygateway"
    }
  }
}
```

### <a name="example-using-encryptedcredential"></a>Exemplo: Utilizar encryptedcredential

```JSON
{
  "Name": " OnPremisesFileServerLinkedService ",
  "properties": {
    "type": "OnPremisesFileServer",
    "typeProperties": {
      "host": "D:\\",
      "encryptedCredential": "WFuIGlzIGRpc3Rpbmd1aXNoZWQsIG5vdCBvbmx5IGJ5xxxxxxxxxxxxxxxxx",
      "gatewayName": "mygateway"
    }
  }
}
```

## <a name="dataset-properties"></a>Propriedades do conjunto de dados
Para uma lista completa das secções e as propriedades disponíveis para definir os conjuntos de dados, consulte [criar conjuntos de dados](data-factory-create-datasets.md). As secções, tais como a estrutura, a disponibilidade e a política de um conjunto de dados JSON são semelhantes para todos os tipos de conjunto de dados.

secção de typeProperties Olá é diferente para cada tipo de conjunto de dados. Fornece informações como localização de Olá e o formato dos dados de Olá no arquivo de dados de Olá. Olá typeProperties secção Olá conjunto de dados do tipo **FileShare** tem Olá seguintes propriedades:

| Propriedade | Descrição | Necessário |
| --- | --- | --- |
| folderPath |Especifica Olá Subcaminho toohello pasta. Utilize o caráter de escape Olá ' \' para carateres especiais na cadeia de Olá. Consulte [exemplo ligado definições de serviço e o conjunto de dados](#sample-linked-service-and-dataset-definitions) para obter exemplos.<br/><br/>Pode combinar esta propriedade com **partitionBy** toohave caminhos de pastas com base no setor início/fim tempos de data. |Sim |
| fileName |Especifique o nome de Olá do ficheiro de Olá no Olá **folderPath** se quiser Olá tabela toorefer tooa específico ficheiro na pasta Olá. Se não for especificado qualquer valor para esta propriedade, tabela Olá pontos tooall ficheiros na pasta Olá.<br/><br/>Quando **fileName** não está especificado para um conjunto de dados de saída e **preserveHierarchy** não foram especificadas no receptor de atividade, Olá do ficheiro de Olá gerado está a ser Olá seguinte formato: <br/><br/>`Data.<Guid>.txt`(Exemplo: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt) |Não |
| fileFilter |Especifique um filtro toobe utilizada tooselect um subconjunto de ficheiros em folderPath Olá em vez de todos os ficheiros. <br/><br/>Valores permitidos são: `*` (vários carateres) e `?` (único caráter).<br/><br/>Exemplo 1: "fileFilter": "*. log"<br/>Exemplo 2: "fileFilter": 2014 - 1-?. txt"<br/><br/>Tenha em atenção que fileFilter se aplica a um conjunto de dados de partilha de ficheiros de entrada. |Não |
| partitionedBy |Pode utilizar partitionedBy toospecify folderPath/fileName dinâmico para dados de séries de tempo. Um exemplo é folderPath parametrizada para cada hora dos dados. |Não |
| formato | é suportado os seguintes tipos de formato de Olá: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**. Conjunto Olá **tipo** propriedade em formato tooone destes valores. Para obter mais informações, consulte [formato de texto](data-factory-supported-file-and-compression-formats.md#text-format), [formato Json](data-factory-supported-file-and-compression-formats.md#json-format), [formato Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc formato](data-factory-supported-file-and-compression-formats.md#orc-format), e [Parquet formato](data-factory-supported-file-and-compression-formats.md#parquet-format) secções. <br><br> Se quiser demasiado**copiar ficheiros como-é** entre arquivos baseados em ficheiros (cópia binário), ignorar a secção de formato Olá em ambas as definições do conjunto de dados de entrada e de saída. |Não |
| Compressão | Especifique o tipo de Olá e nível de compressão de dados de Olá. Tipos suportados são: **GZip**, **Deflate**, **BZip2**, e **ZipDeflate**. Níveis suportados são: **Optimal** e **Fastest**. consulte [formatos de ficheiro e compressão no Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support). |Não |

> [!NOTE]
> Não é possível utilizar fileName e fileFilter em simultâneo.

### <a name="using-partitionedby-property"></a>Utilizar a propriedade partitionedBy
Tal como mencionado na secção anterior Olá, pode especificar um folderPath dinâmica e o nome de ficheiro de dados de séries de tempo com Olá **partitionedBy** propriedade, [funções de Data Factory e variáveis do sistema Olá](data-factory-functions-variables.md).

Consulte mais detalhes em conjuntos de dados de séries de tempo, agendar e setores, de toounderstand [criar conjuntos de dados](data-factory-create-datasets.md), [agendamento e execução](data-factory-scheduling-and-execution.md), e [Criar pipelines](data-factory-create-pipelines.md).

#### <a name="sample-1"></a>Exemplo 1:

```JSON
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```

Neste exemplo, {setor} é substituído pelo valor Olá de Olá fábrica de dados de variável de sistema SliceStart no formato de Olá (YYYYMMDDHH). SliceStart refere-se a hora de toostart do setor Olá. Olá folderPath é diferente para cada setor. Por exemplo: wikidatagateway/wikisampledataout/2014100103 ou wikidatagateway/wikisampledataout/2014100104.

#### <a name="sample-2"></a>Exemplo 2:

```JSON
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

Neste exemplo, ano, mês, dia e hora do SliceStart são extraídos para variáveis separadas que utilizam propriedades de Olá folderPath e nome de ficheiro.

## <a name="copy-activity-properties"></a>Propriedades da atividade de cópia
Para uma lista completa das secções & Propriedades disponíveis para definir as atividades, consulte Olá [criar Pipelines](data-factory-create-pipelines.md) artigo. Propriedades, tais como o nome, descrição e de saída, conjuntos de dados e as políticas estão disponíveis para todos os tipos de atividades. Enquanto, propriedades disponíveis nos Olá **typeProperties** secção da atividade de Olá variar de acordo com cada tipo de atividade.

Para a atividade de cópia, podem variam consoante os tipos de origens e sinks Olá. Se estiver a mover dados de um sistema de ficheiros no local, definir o tipo de origem Olá na atividade de cópia de Olá demasiado**FileSystemSource**. Da mesma forma, se estiver a mover dados tooan sistema de ficheiros no local, defina o tipo de sink Olá na atividade de cópia de Olá demasiado**FileSystemSink**. Esta secção fornece uma lista de propriedades suportadas por FileSystemSource e FileSystemSink.

**FileSystemSource** suporta Olá seguintes propriedades:

| Propriedade | Descrição | Valores permitidos | Necessário |
| --- | --- | --- | --- |
| Recursiva |Indica se Olá é ler dados recursivamente subpastas Olá ou apenas a pasta especificada Olá. |TRUE, False (predefinição) |Não |

**FileSystemSink** suporta Olá seguintes propriedades:

| Propriedade | Descrição | Valores permitidos | Necessário |
| --- | --- | --- | --- |
| copyBehavior |Define o comportamento de cópia de Olá quando a origem de Olá é BlobSource ou sistema de ficheiros. |**PreserveHierarchy:** preserva a hierarquia de ficheiros de Olá na pasta de destino Olá. Ou seja, o caminho da pasta de origem do Olá origem ficheiro toohello relativo Olá é Olá, mesmo que o caminho da pasta de destino do toohello no ficheiro de destino do Olá relativo Olá.<br/><br/>**FlattenHierarchy:** todos os ficheiros da pasta de origem Olá são criados no nível de primeiro Olá da pasta de destino. ficheiros do destino de Olá são criados com um nome gerado automaticamente.<br/><br/>**MergeFiles:** une todos os ficheiros a partir do ficheiro de tooone da pasta de origem de Olá. Se for especificado o nome de blob/nome de ficheiro Olá, Olá ficheiro intercalado é Olá especificado nome. Caso contrário, é um nome de ficheiro gerada automaticamente. |Não |

### <a name="recursive-and-copybehavior-examples"></a>Exemplos de recursiva e copyBehavior
Esta secção descreve o comportamento resultante de Olá de operação de cópia de Olá para diferentes combinações de valores para Olá recursiva e copyBehavior propriedades.

| valor de recursiva | valor de copyBehavior | Comportamento resultante |
| --- | --- | --- |
| VERDADEIRO |preserveHierarchy |Para uma pasta de origem Pasta1 com Olá seguir a estrutura de<br/><br/>Pasta1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5<br/><br/>pasta de destino Olá Pasta1 é criada com Olá mesmo estrutura como origem Olá:<br/><br/>Pasta1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5 |
| VERDADEIRO |flattenHierarchy |Para uma pasta de origem Pasta1 com Olá seguir a estrutura de<br/><br/>Pasta1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5<br/><br/>destino de Olá Pasta1 é criado com Olá seguir a estrutura: <br/><br/>Pasta1<br/>&nbsp;&nbsp;&nbsp;&nbsp;nome gerado automaticamente para File1<br/>&nbsp;&nbsp;&nbsp;&nbsp;nome gerado automaticamente para File2<br/>&nbsp;&nbsp;&nbsp;&nbsp;nome gerado automaticamente para File3<br/>&nbsp;&nbsp;&nbsp;&nbsp;nome gerado automaticamente para File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;nome gerado automaticamente para File5 |
| VERDADEIRO |mergeFiles |Para uma pasta de origem Pasta1 com Olá seguir a estrutura de<br/><br/>Pasta1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5<br/><br/>destino de Olá Pasta1 é criado com Olá seguir a estrutura: <br/><br/>Pasta1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1 + File2 + File3 + File4 + ficheiro 5 é intercalado conteúdo para um ficheiro com um nome de ficheiro gerada automaticamente. |
| FALSO |preserveHierarchy |Para uma pasta de origem Pasta1 com Olá seguir a estrutura de<br/><br/>Pasta1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5<br/><br/>pasta de destino Olá Pasta1 é criada com Olá seguir a estrutura:<br/><br/>Pasta1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File2<br/><br/>Não é escolhido Subfolder1 com File3, File4 e File5. |
| FALSO |flattenHierarchy |Para uma pasta de origem Pasta1 com Olá seguir a estrutura de<br/><br/>Pasta1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5<br/><br/>pasta de destino Olá Pasta1 é criada com Olá seguir a estrutura:<br/><br/>Pasta1<br/>&nbsp;&nbsp;&nbsp;&nbsp;nome gerado automaticamente para File1<br/>&nbsp;&nbsp;&nbsp;&nbsp;nome gerado automaticamente para File2<br/><br/>Não é escolhido Subfolder1 com File3, File4 e File5. |
| FALSO |mergeFiles |Para uma pasta de origem Pasta1 com Olá seguir a estrutura de<br/><br/>Pasta1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5<br/><br/>pasta de destino Olá Pasta1 é criada com Olá seguir a estrutura:<br/><br/>Pasta1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1 + File2 conteúdos são intercalados para um ficheiro com um nome de ficheiro gerada automaticamente.<br/>&nbsp;&nbsp;&nbsp;&nbsp;Nome gerado automaticamente para File1<br/><br/>Não é escolhido Subfolder1 com File3, File4 e File5. |

## <a name="supported-file-and-compression-formats"></a>Formatos de ficheiro e compressão suportados
Consulte [formatos de ficheiro e compressão no Azure Data Factory](data-factory-supported-file-and-compression-formats.md) artigo em detalhes.

## <a name="json-examples-for-copying-data-tooand-from-file-system"></a>Exemplos JSON para copiar dados tooand do sistema de ficheiros
Olá exemplos seguintes fornecem definições JSON de exemplo que pode utilizar toocreate um pipeline utilizando Olá [portal do Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), ou [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md). Estes mostram como toocopy tooand de dados de um sistema de ficheiros no local e o armazenamento de Blobs do Azure. No entanto, pode copiar dados *diretamente* de qualquer um dos Olá origens tooany de Olá sinks listado no [suportados origens e sinks](data-factory-data-movement-activities.md#supported-data-stores-and-formats) utilizando a atividade de cópia no Azure Data Factory.

### <a name="example-copy-data-from-an-on-premises-file-system-tooazure-blob-storage"></a>Exemplo: Copiar dados de um tooAzure de sistema de ficheiros local no armazenamento de BLOBs
Este exemplo mostra como toocopy dados a partir de um tooAzure de sistema de ficheiros local no armazenamento de Blobs. exemplo de Olá tem Olá seguintes entidades do Data Factory:

* Um serviço ligado do tipo [OnPremisesFileServer](#linked-service-properties).
* Um serviço ligado do tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
* Uma entrada [dataset](data-factory-create-datasets.md) do tipo [FileShare](#dataset-properties).
* Uma saída [dataset](data-factory-create-datasets.md) do tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
* A [pipeline](data-factory-create-pipelines.md) com atividade de cópia que utiliza [FileSystemSource](#copy-activity-properties) e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).

Olá exemplo a seguir copia dados de séries de tempo de um tooAzure de sistema de ficheiros local no armazenamento de BLOBs a cada hora. Propriedades JSON Olá que são utilizadas nestes exemplos são descritas nas secções de Olá após amostras Olá.

Como primeiro passo, configurar o Data Management Gateway de acordo com as instruções de Olá em [mover dados entre origens no local e nuvem de Olá com o Data Management Gateway](data-factory-move-data-between-onprem-and-cloud.md).

**Serviço ligado do servidor de ficheiros no local:**

```JSON
{
  "Name": "OnPremisesFileServerLinkedService",
  "properties": {
    "type": "OnPremisesFileServer",
    "typeProperties": {
      "host": "\\\\Contosogame-Asia.<region>.corp.<company>.com",
      "userid": "Admin",
      "password": "123456",
      "gatewayName": "mygateway"
    }
  }
}
```

Recomendamos que utilize Olá **encryptedCredential** propriedade em vez disso, Olá **userid** e **palavra-passe** propriedades. Consulte [serviço ligado do servidor de ficheiros](#linked-service-properties) para obter detalhes sobre este serviço ligado.

**Serviço ligado do Storage do Azure:**

```JSON
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

**Conjunto de dados de entrada de sistema de ficheiros no local:**

Dados são captados um novo ficheiro de cada hora. Olá folderPath e propriedades de nome de ficheiro são determinadas com base na hora de início de Olá do setor Olá.  

Definição `"external": "true"` informa fábrica de dados, esse conjunto de dados de Olá é toohello externo fábrica de dados e não é produzido por uma atividade no factory de dados de Olá.

```JSON
{
  "name": "OnpremisesFileSystemInput",
  "properties": {
    "type": " FileShare",
    "linkedServiceName": " OnPremisesFileServerLinkedService ",
    "typeProperties": {
      "folderPath": "mysharedfolder/yearno={Year}/monthno={Month}/dayno={Day}",
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
      ]
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

**Conjunto de dados de saída do Blob storage do Azure:**

São escritos dados no blob tooa de novo a cada hora (frequência: hora, intervalo: 1). caminho da pasta Olá para BLOBs Olá dinamicamente é avaliado com base na hora de início de Olá do setor de Olá que está a ser processado. caminho da pasta Olá utiliza as partes de ano, mês, dia e hora Olá Olá da hora de início.

```JSON
{
  "name": "AzureBlobOutput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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

**Uma atividade de cópia num pipeline com a origem de sistema de ficheiros e o sink de Blob:**

Olá pipeline contém uma atividade de cópia é configurado toouse Olá conjuntos de dados de entrada e de saída, não sendo toorun agendada a cada hora. No pipeline de Olá definição JSON, Olá **origem** tipo está definido demasiado**FileSystemSource**, e **sink** tipo está definido demasiado**BlobSink**.

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2015-06-01T18:00:00",
    "end":"2015-06-01T19:00:00",
    "description":"Pipeline for copy activity",
    "activities":[  
      {
        "name": "OnpremisesFileSystemtoBlob",
        "description": "copy activity",
        "type": "Copy",
        "inputs": [
          {
            "name": "OnpremisesFileSystemInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureBlobOutput"
          }
        ],
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
          "executionPriorityOrder": "OldestFirst",
          "retry": 0,
          "timeout": "01:00:00"
        }
      }
     ]
   }
}
```

### <a name="example-copy-data-from-azure-sql-database-tooan-on-premises-file-system"></a>Exemplo: Copiar dados de sistema de ficheiros no local do SQL Database do Azure tooan
Olá seguinte exemplo mostra:

* Um serviço ligado do tipo [AzureSqlDatabase.](data-factory-azure-sql-connector.md#linked-service-properties)
* Um serviço ligado do tipo [OnPremisesFileServer](#linked-service-properties).
* Um conjunto de dados de entrada do tipo [AzureSqlTable](data-factory-azure-sql-connector.md#dataset-properties).
* Um conjunto de dados de saída do tipo [FileShare](#dataset-properties).
* Um pipeline com uma atividade de cópia que utiliza [SqlSource](data-factory-azure-sql-connector.md##copy-activity-properties) e [FileSystemSink](#copy-activity-properties).

exemplo de Olá copia dados de séries de tempo de um sistema de ficheiros no local do SQL do Azure tabela tooan a cada hora. Propriedades JSON Olá que são utilizadas nestes exemplos são descritas nas secções após amostras Olá.

**Serviço ligado do SQL Database do Azure:**

```JSON
{
  "name": "AzureSqlLinkedService",
  "properties": {
    "type": "AzureSqlDatabase",
    "typeProperties": {
      "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
    }
  }
}
```

**Serviço ligado do servidor de ficheiros no local:**

```JSON
{
  "Name": "OnPremisesFileServerLinkedService",
  "properties": {
    "type": "OnPremisesFileServer",
    "typeProperties": {
      "host": "\\\\Contosogame-Asia.<region>.corp.<company>.com",
      "userid": "Admin",
      "password": "123456",
      "gatewayName": "mygateway"
    }
  }
}
```

Recomendamos que utilize Olá **encryptedCredential** propriedade em vez de utilizar Olá **userid** e **palavra-passe** propriedades. Consulte [serviço ligado do sistema de ficheiros](#linked-service-properties) para obter detalhes sobre este serviço ligado.

**Conjunto de dados de entrada SQL do Azure:**

exemplo de Olá pressupõe que criou uma tabela "MyTable" no SQL do Azure e contém uma coluna chamada "timestampcolumn" para dados de séries de tempo.

Definição ``“external”: ”true”`` informa fábrica de dados, esse conjunto de dados de Olá é toohello externo fábrica de dados e não é produzido por uma atividade no factory de dados de Olá.

```JSON
{
  "name": "AzureSqlInput",
  "properties": {
    "type": "AzureSqlTable",
    "linkedServiceName": "AzureSqlLinkedService",
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

**Conjunto de dados de saída de sistema de ficheiros no local:**

Os dados são copiados tooa novo ficheiro a cada hora. Olá folderPath e nome de ficheiro de blob Olá são determinados com base na hora de início de Olá do setor Olá.

```JSON
{
  "name": "OnpremisesFileSystemOutput",
  "properties": {
    "type": "FileShare",
    "linkedServiceName": " OnPremisesFileServerLinkedService ",
    "typeProperties": {
      "folderPath": "mysharedfolder/yearno={Year}/monthno={Month}/dayno={Day}",
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
      ]
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

**Uma atividade de cópia num pipeline com a origem SQL e o sink de sistema de ficheiros:**

Olá pipeline contém uma atividade de cópia é configurado toouse Olá conjuntos de dados de entrada e de saída, não sendo toorun agendada a cada hora. No pipeline de Olá definição JSON, Olá **origem** tipo está definido demasiado**SqlSource**e Olá **sink** tipo está definido demasiado**FileSystemSink**. consulta SQL Olá especificado para Olá **SqlReaderQuery** propriedade seleciona dados Olá Olá passado toocopy de hora.

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2015-06-01T18:00:00",
    "end":"2015-06-01T20:00:00",
    "description":"pipeline for copy activity",
    "activities":[  
      {
        "name": "AzureSQLtoOnPremisesFile",
        "description": "copy activity",
        "type": "Copy",
        "inputs": [
          {
            "name": "AzureSQLInput"
          }
        ],
        "outputs": [
          {
            "name": "OnpremisesFileSystemOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "SqlSource",
            "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd}\\'', WindowStart, WindowEnd)"
          },
          "sink": {
            "type": "FileSystemSink"
          }
        },
       "scheduler": {
          "frequency": "Hour",
          "interval": 1
        },
        "policy": {
          "concurrency": 1,
          "executionPriorityOrder": "OldestFirst",
          "retry": 3,
          "timeout": "01:00:00"
        }
      }
     ]
   }
}
```


Também pode mapear colunas do conjunto de dados de origem toocolumns do conjunto de dados dependente na definição de atividade de cópia de Olá. Para obter mais informações, consulte [mapeamento de colunas do conjunto de dados no Azure Data Factory](data-factory-map-columns.md).

## <a name="performance-and-tuning"></a>Desempenho e otimização
 toolearn sobre chave factors desse desempenho de Olá impacto de movimento de dados (atividade de cópia) no Azure Data Factory e várias formas toooptimize-lo, consulte Olá [guia Otimização e de desempenho de atividade de cópia](data-factory-copy-activity-performance.md).
