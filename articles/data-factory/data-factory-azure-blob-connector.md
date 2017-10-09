---
title: dados aaaCopy para/de Blob Storage do Azure | Microsoft Docs
description: 'Saiba como toocopy blob dados no Azure Data Factory. Utilizar o nosso exemplo: como toocopy tooand de dados do Blob Storage do Azure e SQL Database do Azure.'
keywords: "dados de BLOBs, cópia de Blobs do azure"
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: bec8160f-5e07-47e4-8ee1-ebb14cfb805d
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jingwang
ms.openlocfilehash: 8428c64e8e8b1084b3f2f680c4e1819559e4ffa3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="copy-data-tooor-from-azure-blob-storage-using-azure-data-factory"></a>Copiar dados tooor do armazenamento de Blobs do Azure utilizando o Azure Data Factory
Este artigo explica como toouse Olá atividade de cópia no Azure Data Factory toocopy dados tooand do Blob Storage do Azure. Baseia-se no Olá [atividades de movimentos de dados](data-factory-data-movement-activities.md) artigo, que apresenta uma descrição geral do movimento de dados com a atividade de cópia de Olá.

## <a name="overview"></a>Descrição geral
Pode copiar dados de qualquer origem suportada armazenam tooAzure armazenamento de BLOBs ou a partir dos dados do Blob Storage do Azure tooany suportado sink armazenam dados. Olá tabela seguinte fornece uma lista de arquivos de dados suportada como origens ou sinks pela atividade de cópia de Olá. Por exemplo, pode mover dados **de** uma base de dados do SQL Server ou uma base de dados SQL do Azure **para** um armazenamento de Blobs do Azure. E, pode copiar dados **de** blob storage do Azure **para** um Azure SQL Data Warehouse ou uma coleção de BD do Cosmos do Azure. 

## <a name="supported-scenarios"></a>Cenários suportados
Pode copiar dados **do Blob Storage do Azure** toohello seguir arquivos de dados:

[!INCLUDE [data-factory-supported-sink](../../includes/data-factory-supported-sinks.md)]

Pode copiar dados de Olá seguir arquivos de dados **tooAzure Blob Storage**:

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]
 
> [!IMPORTANT]
> Atividade de cópia suporta a cópia de dados de / tooboth Storage do Azure para fins gerais contas de acesso frequente e/esporádico armazenamento de Blobs. atividade de Olá suporta **ler a partir de blocos, acrescentar ou blobs de páginas**, mas suporta **escrita de blobs de blocos tooonly**. Armazenamento Premium do Azure não é suportado como um sink porque esteja associada a blobs de páginas.
> 
> Atividade de cópia não elimina dados de origem Olá após Olá dados com êxito são copiada toohello destino. Se precisar de dados de origem toodelete depois de uma cópia com êxito, crie um [atividade personalizada](data-factory-use-custom-activities.md) toodelete Olá dados e utilize a atividade de Olá no pipeline de Olá. Por exemplo, consulte Olá [eliminar BLOBs ou pasta de exemplo no GitHub](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/DeleteBlobFileFolderCustomActivity). 

## <a name="get-started"></a>Introdução
Pode criar um pipeline com uma atividade de cópia move os dados de/para um armazenamento de Blobs do Azure utilizando ferramentas diferentes/APIs.

Olá toocreate da forma mais fácil um pipeline está toouse Olá **Assistente para copiar**. Este artigo tem um [instruções](#walkthrough-use-copy-wizard-to-copy-data-tofrom-blob-storage) para criar um dados toocopy do pipeline de um tooanother de localização de armazenamento de Blobs do Azure a localização de armazenamento de Blobs do Azure. Para um tutorial sobre a criação de um dado de toocopy do pipeline de uma base de dados SQL de tooAzure do Blob Storage do Azure, consulte [Tutorial: criar um pipeline com o Assistente para copiar](data-factory-copy-data-wizard-tutorial.md).

Também pode utilizar Olá seguintes ferramentas toocreate um pipeline: **portal do Azure**, **Visual Studio**, **Azure PowerShell**, **modelo Azure Resource Manager** , **.NET API**, e **REST API**. Consulte [tutorial de atividade de cópia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para instruções passo a passo toocreate um pipeline com uma atividade de cópia.

Se utilizar ferramentas de Olá ou APIs, execute Olá os seguintes passos toocreate um pipeline que move o arquivo de dados do tooa sink do arquivo de dados de uma origem de dados:

1. Criar um **fábrica de dados**. Uma fábrica de dados pode conter um ou mais pipelines. 
2. Criar **serviços ligados** fábrica de dados de tooyour de arquivos de dados de entrada e saída de toolink. Por exemplo, se estiver a copiar dados de uma base de dados de SQL do Azure de tooan de armazenamento do BLOBs do Azure, pode cria dois serviços ligados toolink a conta de armazenamento do Azure e a fábrica de dados de tooyour de base de dados SQL do Azure. As propriedades de serviço ligado que são específica tooAzure Blob Storage, consulte [ligado propriedades do serviço](#linked-service-properties) secção. 
2. Criar **conjuntos de dados** toorepresent de entrada e saída de operação de cópia de dados para Olá. Exemplo de Olá mencionado no passo último Olá, criar um contentor de blob do conjunto de dados toospecify Olá e a pasta que contém dados de entrada Olá. Além disso, crie outra tabela do conjunto de dados toospecify Olá SQL na base de dados do SQL do Azure Olá que contém dados Olá copiados Olá do armazenamento de Blobs. As propriedades do conjunto de dados que são específica tooAzure Blob Storage, consulte [propriedades do dataset](#dataset-properties) secção.
3. Criar um **pipeline** com uma atividade de cópia executa um conjunto de dados como entrada e um conjunto de dados como resultado. Exemplo de Olá mencionado anteriormente, que utilizar BlobSource como uma origem e SqlSink como um sink para atividade de cópia de Olá. Da mesma forma, se estiver a copiar a partir da base de dados do Azure SQL tooAzure armazenamento de BLOBs, utilizar SqlSource e BlobSink na atividade de cópia de Olá. Para as propriedades da atividade de cópia que são específica tooAzure Blob Storage, consulte [copiar propriedades da atividade](#copy-activity-properties) secção. Para obter detalhes sobre como toouse um arquivo de dados como uma origem ou de um receptor de mensagens em fila, clique em ligação Olá na secção anterior do Olá para o arquivo de dados.  

Quando utiliza o Assistente de Olá, definições de JSON para estas entidades do Data Factory (serviços ligados, conjuntos de dados e pipeline Olá) são criadas automaticamente para si. Ao utilizar ferramentas/APIs (exceto .NET API), é possível definir estas entidades do Data Factory utilizando o formato JSON Olá.  Para exemplos com definições de JSON para entidades do Data Factory que são utilizados toocopy dados para/de um Blob Storage do Azure, consulte [exemplos JSON](#json-examples-for-copying-data-to-and-from-blob-storage  ) secção deste artigo.

Olá seguintes secções fornece detalhes sobre as propriedades JSON que são utilizados toodefine Data Factory entidades específica tooAzure Blob Storage.

## <a name="linked-service-properties"></a>Propriedades de serviço ligado
Existem dois tipos de serviços ligados, pode utilizar toolink um Azure data factory de tooan do Storage do Azure. São: **AzureStorage** serviço ligado e **AzureStorageSas** serviço ligado. Olá serviço ligado do Storage do Azure fornece fábrica de dados de Olá com acesso global toohello Storage do Azure. Enquanto, Olá Azure armazenamento SAS (assinatura de acesso partilhado) ligado serviço fornece fábrica de dados de Olá com acesso restrito/vínculo de tempo toohello Storage do Azure. Não existem não existem outras diferenças entre esses dois serviços ligados. Escolha um serviço Olá ligado que se adapta às suas necessidades. Olá secções seguintes fornecem mais detalhes sobre estes dois serviços ligados.

[!INCLUDE [data-factory-azure-storage-linked-services](../../includes/data-factory-azure-storage-linked-services.md)]

## <a name="dataset-properties"></a>Propriedades do conjunto de dados
toospecify toorepresent um conjunto de dados dados de entrada ou saídos num armazenamento de Blobs do Azure, pode definir a propriedade de tipo Olá de Olá conjunto de dados: **AzureBlob**. Conjunto Olá **linkedServiceName** serviço ligado de propriedade do Olá dataset toohello nome Olá Storage do Azure ou SAS de armazenamento do Azure.  Propriedades de tipo Olá do conjunto de dados de Olá especificar Olá **contentor do blob** e Olá **pasta** no armazenamento de BLOBs de Olá.

Para obter uma lista completa de secções JSON & Propriedades disponíveis para definir os conjuntos de dados, consulte Olá [criar conjuntos de dados](data-factory-create-datasets.md) artigo. As secções, tais como a estrutura, a disponibilidade e a política de um conjunto de dados JSON são semelhantes para todos os tipos de conjunto de dados (SQL do Azure, Azure blob, tabela do Azure, etc.).

Fábrica de dados suporta Olá os seguintes valores do tipo compatível com CLS .NET com base para fornecer informações sobre o tipo de "estrutura" para origens de dados de esquema no leitura como BLOBs do Azure: Int16, Int32, Int64, único, Double, Decimal, Byte [] e String, booleano, Datetime, e Guid Datetimeoffset, Timespan. Fábrica de dados efetua automaticamente conversões de tipo ao mover o arquivo de dados do tooa sink do arquivo de dados de uma origem de dados.

Olá **typeProperties** secção é diferente para cada tipo de conjunto de dados e fornece informações sobre a localização de Olá, etc., formato de dados de Olá no arquivo de dados de Olá. Olá typeProperties secção para o conjunto de dados do tipo **AzureBlob** dataset tem Olá seguintes propriedades:

| Propriedade | Descrição | Necessário |
| --- | --- | --- |
| folderPath |Contentor de toohello caminho e a pasta no armazenamento de BLOBs de Olá. Exemplo: myblobcontainer\myblobfolder\ |Sim |
| fileName |Nome do blob Olá. nome de ficheiro é opcional e maiúsculas e minúsculas.<br/><br/>Se especificar um nome de ficheiro, Olá atividade (incluindo cópia) funciona no Olá Blob específico.<br/><br/>Quando o nome de ficheiro não for especificado, cópia inclui todos os Blobs no folderPath Olá para conjunto de dados de entrada.<br/><br/>Quando **fileName** não está especificado para um conjunto de dados de saída e **preserveHierarchy** não foram especificadas no receptor de atividade, nome de Olá do ficheiro de Olá gerado seria no Olá segue este formato: Data.<Guid>. txt (por exemplo:: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt |Não |
| partitionedBy |partitionedBy propriedade é opcional. Pode utilizar-toospecify um folderPath dinâmica e nome de ficheiro de dados de séries de tempo. Por exemplo, folderPath pode ser parametrizada para cada hora dos dados. Consulte Olá [utilizando a secção de propriedade partitionedBy](#using-partitionedBy-property) para obter detalhes e exemplos. |Não |
| formato | é suportado os seguintes tipos de formato de Olá: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**. Conjunto Olá **tipo** propriedade em formato tooone destes valores. Para obter mais informações, consulte [formato de texto](data-factory-supported-file-and-compression-formats.md#text-format), [formato Json](data-factory-supported-file-and-compression-formats.md#json-format), [formato Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc formato](data-factory-supported-file-and-compression-formats.md#orc-format), e [Parquet formato](data-factory-supported-file-and-compression-formats.md#parquet-format) secções. <br><br> Se quiser demasiado**copiar ficheiros como-é** entre arquivos baseados em ficheiros (cópia binário), ignorar a secção de formato Olá em ambas as definições do conjunto de dados de entrada e de saída. |Não |
| Compressão | Especifique o tipo de Olá e nível de compressão de dados de Olá. Tipos suportados são: **GZip**, **Deflate**, **BZip2**, e **ZipDeflate**. Níveis suportados são: **Optimal** e **Fastest**. Para obter mais informações, consulte [formatos de ficheiro e compressão no Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support). |Não |

### <a name="using-partitionedby-property"></a>Utilizar a propriedade partitionedBy
Tal como mencionado na secção anterior Olá, pode especificar um folderPath dinâmica e o nome de ficheiro de dados de séries de tempo com Olá **partitionedBy** propriedade, [funções de Data Factory e variáveis do sistema Olá](data-factory-functions-variables.md).

Para obter mais informações sobre conjuntos de dados de séries de tempo, agendar e setores, consulte [criar conjuntos de dados](data-factory-create-datasets.md) e [agendamento e execução](data-factory-scheduling-and-execution.md) artigos.

#### <a name="sample-1"></a>Exemplo 1

```json
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```

Neste exemplo, {setor} é substituído pelo valor da Olá da variável de sistema do Data Factory SliceStart no formato de Olá (YYYYMMDDHH) especificado. Olá SliceStart refere-se a hora de toostart do setor Olá. Olá folderPath é diferente para cada setor. Por exemplo: wikidatagateway/wikisampledataout/2014100103 ou wikidatagateway/wikisampledataout/2014100104

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

Neste exemplo, ano, mês, dia e hora do SliceStart são extraídos em separado variáveis que são utilizadas pelas propriedades folderPath e nome de ficheiro.

## <a name="copy-activity-properties"></a>Propriedades da atividade de cópia
Para uma lista completa das secções & Propriedades disponíveis para definir as atividades, consulte Olá [criar Pipelines](data-factory-create-pipelines.md) artigo. Propriedades, tais como o nome, descrição e de saída, conjuntos de dados e as políticas estão disponíveis para todos os tipos de atividades. Enquanto, propriedades disponíveis nos Olá **typeProperties** secção da atividade de Olá variar de acordo com cada tipo de atividade. Para a atividade de cópia, podem variam consoante os tipos de origens e sinks Olá. Se estiver a mover dados de um Blob Storage do Azure, definir o tipo de origem Olá na atividade de cópia de Olá demasiado**BlobSource**. Da mesma forma, se estiver a mover dados tooan Blob Storage do Azure, definir o tipo de sink Olá na atividade de cópia de Olá demasiado**BlobSink**. Esta secção fornece uma lista de propriedades suportadas por BlobSource e BlobSink.

**BlobSource** suporta Olá seguintes propriedades no Olá **typeProperties** secção:

| Propriedade | Descrição | Valores permitidos | Necessário |
| --- | --- | --- | --- |
| Recursiva |Indica se Olá é ler dados recursivamente subpastas Olá ou apenas a pasta especificada Olá. |TRUE (valor predefinido), False |Não |

**BlobSink** suporta as seguintes propriedades de Olá **typeProperties** secção:

| Propriedade | Descrição | Valores permitidos | Necessário |
| --- | --- | --- | --- |
| copyBehavior |Define o comportamento de cópia de Olá quando a origem de Olá é BlobSource ou sistema de ficheiros. |<b>PreserveHierarchy</b>: preserva Olá hierarquia de ficheiros na pasta de destino Olá. o caminho relativo Olá da pasta de toosource do ficheiro de origem é idêntico toohello caminho relativo de tootarget da pasta do ficheiro de destino.<br/><br/><b>FlattenHierarchy</b>: todos os ficheiros da pasta de origem Olá estão em Olá primeiro níveis da pasta de destino. os ficheiros de destino Olá ter nome automaticamente gerado. <br/><br/><b>MergeFiles</b>: une todos os ficheiros a partir do ficheiro de tooone da pasta de origem de Olá. Se Olá nome de ficheiro/Blob for especificado, o nome de ficheiro intercalada de Olá seria o nome especificado Olá; caso contrário, seria nome de ficheiro gerada automaticamente. |Não |

**BlobSource** também suporta estas duas propriedades para compatibilidade com versões anteriores.

* **treatEmptyAsNull**: Especifica se uma cadeia nula ou vazia tootreat como um valor nulo.
* **skipHeaderLineCount** -Especifica o número de linhas tem de ser ignoradas. É aplicável apenas ao conjunto de dados de entrada está a utilizar TextFormat.

Da mesma forma, **BlobSink** suporta Olá seguinte propriedade para compatibilidade com versões anteriores.

* **blobWriterAddHeader**: Especifica se tooadd um cabeçalho de definições da coluna ao escrever tooan conjunto de dados de saída.

Olá suporte agora de conjuntos de dados seguintes propriedades que implementam Olá a mesma funcionalidade: **treatEmptyAsNull**, **skipLineCount**, **firstRowAsHeader**.

Olá tabela seguinte fornece orientações sobre como utilizar propriedades de novo conjunto de dados Olá em vez destas propriedades de origem/sink do blob.

| Propriedade da atividade de cópia | Propriedade de conjunto de dados |
|:--- |:--- |
| skipHeaderLineCount no BlobSource |skipLineCount e firstRowAsHeader. As linhas são ignoradas pela primeira vez e, em seguida, a primeira linha de Olá é lido como um cabeçalho. |
| treatEmptyAsNull no BlobSource |treatEmptyAsNull no conjunto de dados de entrada |
| blobWriterAddHeader no BlobSink |firstRowAsHeader no conjunto de dados de saída |

Consulte [especificando TextFormat](data-factory-supported-file-and-compression-formats.md#text-format) secção para obter informações detalhadas sobre estas propriedades.    

### <a name="recursive-and-copybehavior-examples"></a>Exemplos de recursiva e copyBehavior
Esta secção descreve o comportamento resultante de Olá de operação de cópia de Olá para diferentes combinações de valores recursiva e copyBehavior.

| Recursiva | copyBehavior | Comportamento resultante |
| --- | --- | --- |
| VERDADEIRO |preserveHierarchy |Para uma pasta de origem Pasta1 com Olá seguir a estrutura: <br/><br/>Pasta1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5<br/><br/>pasta de destino Olá Pasta1 é criada com Olá mesmo estrutura como origem Olá<br/><br/>Pasta1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5. |
| VERDADEIRO |flattenHierarchy |Para uma pasta de origem Pasta1 com Olá seguir a estrutura: <br/><br/>Pasta1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5<br/><br/>destino de Olá Pasta1 é criado com Olá seguir a estrutura: <br/><br/>Pasta1<br/>&nbsp;&nbsp;&nbsp;&nbsp;nome gerado automaticamente para File1<br/>&nbsp;&nbsp;&nbsp;&nbsp;nome gerado automaticamente para File2<br/>&nbsp;&nbsp;&nbsp;&nbsp;nome gerado automaticamente para File3<br/>&nbsp;&nbsp;&nbsp;&nbsp;nome gerado automaticamente para File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;nome gerado automaticamente para File5 |
| VERDADEIRO |mergeFiles |Para uma pasta de origem Pasta1 com Olá seguir a estrutura: <br/><br/>Pasta1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5<br/><br/>destino de Olá Pasta1 é criado com Olá seguir a estrutura: <br/><br/>Pasta1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1 + File2 + File3 + File4 + ficheiro 5 é intercalado conteúdo para um ficheiro com nome de ficheiro gerado automaticamente |
| FALSO |preserveHierarchy |Para uma pasta de origem Pasta1 com Olá seguir a estrutura: <br/><br/>Pasta1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5<br/><br/>pasta de destino Olá Pasta1 é criada com Olá seguir a estrutura<br/><br/>Pasta1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File2<br/><br/><br/>Não Subfolder1 com File3, File4 e File5 captado. |
| FALSO |flattenHierarchy |Para uma pasta de origem Pasta1 com Olá seguir a estrutura:<br/><br/>Pasta1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5<br/><br/>pasta de destino Olá Pasta1 é criada com Olá seguir a estrutura<br/><br/>Pasta1<br/>&nbsp;&nbsp;&nbsp;&nbsp;nome gerado automaticamente para File1<br/>&nbsp;&nbsp;&nbsp;&nbsp;nome gerado automaticamente para File2<br/><br/><br/>Não Subfolder1 com File3, File4 e File5 captado. |
| FALSO |mergeFiles |Para uma pasta de origem Pasta1 com Olá seguir a estrutura:<br/><br/>Pasta1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5<br/><br/>pasta de destino Olá Pasta1 é criada com Olá seguir a estrutura<br/><br/>Pasta1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1 + File2 conteúdos são intercalados para um ficheiro com nome de ficheiro gerada automaticamente. nome gerado automaticamente para File1<br/><br/>Não Subfolder1 com File3, File4 e File5 captado. |

## <a name="walkthrough-use-copy-wizard-toocopy-data-tofrom-blob-storage"></a>EXPLICAÇÃO passo a passo: Dados Assistente de cópia de utilização toocopy para/de armazenamento de BLOBs
Vamos ver como o armazenamento de BLOBs de tooquickly copiar dados para / do Azure. Nestas instruções, armazena os dados de origem e destino do tipo: Blob Storage do Azure. Olá pipeline nestas instruções copia dados a partir de uma pasta de tooanother nas Olá mesmo contentor de blob. Estas instruções se tooshow intencionalmente simple que as definições ou propriedades quando utilizar o armazenamento de Blob como uma origem ou o sink. 

### <a name="prerequisites"></a>Pré-requisitos
1. Criar um para fins gerais **conta do Storage do Azure** se ainda não tiver um. Utilizar o armazenamento de BLOBs de Olá como ambos **origem** e **destino** armazenam dados nestas instruções. Se não tiver uma conta de armazenamento do Azure, consulte Olá [criar uma conta de armazenamento](../storage/common/storage-create-storage-account.md#create-a-storage-account) artigo para passos toocreate um.
2. Criar um contentor do blob denominado **adfblobconnector** na conta do storage Olá. 
4. Crie uma pasta denominada **entrada** no Olá **adfblobconnector** contentor.
5. Crie um ficheiro denominado **emp.txt** com Olá seguir conteúdo e carregá-la toohello **entrada** pasta utilizando ferramentas como [Explorador de armazenamento do Azure](https://azurestorageexplorer.codeplex.com/)
    ```json
    John, Doe
    Jane, Doe
    ```
### <a name="create-hello-data-factory"></a>Criar fábrica de dados de Olá
1. Inicie sessão no toohello [portal do Azure](https://portal.azure.com).
2. Clique em **+ novo** no canto superior esquerdo de Olá, clique em **Intelligence + análise**e clique em **Data Factory**.
3. No Olá **nova fábrica de dados** painel:   
    1. Introduza **ADFBlobConnectorDF** para Olá **nome**. nome de Olá do Olá do Azure data factory deve ser globalmente exclusivo. Se receber o erro de Olá: `*Data factory name “ADFBlobConnectorDF” is not available`, altere o nome de Olá do Olá data factory (por exemplo, yournameADFBlobConnectorDF) e tente criar novamente. Veja o tópico [Data Factory – Naming Rules (Data Factory – Regras de Nomenclatura)](data-factory-naming-rules.md) para obter as regras de nomenclatura dos artefactos do Data Factory.
    2. Selecione a sua **subscrição** do Azure.
    3. Para o grupo de recursos, selecione **utilização existente** tooselect um recurso grupo (ou existente) selecione **criar nova** tooenter um nome para um grupo de recursos.
    4. Selecione um **localização** Olá fábrica de dados.
    5. Selecione **Pin toodashboard** caixa de verificação na parte inferior de Olá do painel de Olá.
    6. Clique em **Criar**.
3. Depois de concluída a criação de Olá, consulte Olá **Data Factory** painel conforme mostrado no Olá seguinte imagem: ![home page da fábrica de dados](./media/data-factory-azure-blob-connector/data-factory-home-page.png)

### <a name="copy-wizard"></a>Assistente de Cópia
1. Na home page da Olá fábrica de dados, clique em Olá **copiar dados [pré-visualização]** mosaico toolaunch **Assistente de cópia de dados** num separador separado.    
    
    > [!NOTE]
    >    Se vir esse browser da web Olá é bloqueada no "A autorizar …", desative/desmarque **bloquear cookies de terceiros e dados do site** definição (ou) mantenha-a ativada e crie uma exceção para **login.microsoftonline.com**e, em seguida, tente iniciar novamente o Assistente de Olá.
2. No Olá **propriedades** página:
    1. Introduza **CopyPipeline** para **nome da tarefa**. nome da tarefa Olá é o nome de Olá do pipeline de Olá na fábrica de dados.
    2. Introduza um **Descrição** tarefa Olá (opcional).
    3. Para **cadência de tarefas ou agenda de tarefas**, manter Olá **regularmente executado numa agenda** opção. Se pretender toorun esta tarefa apenas uma vez em vez de ser executado repetidamente numa agenda, selecione **executar agora uma vez**. Se selecionar, **executar agora uma vez** opção, uma [pipeline Monouso](data-factory-create-pipelines.md#onetime-pipeline) é criado. 
    4. Manter Olá para **periódica padrão**. Esta tarefa é executada diariamente entre Olá começar e termina horas especificar no passo seguinte Olá.
    5. Olá alteração **data hora de início** demasiado**21/04/2017**. 
    6. Olá alteração **data hora de fim** demasiado**25/04/2017**. Poderá pretender data de Olá tootype em vez de navegar pelas calendário Olá.     
    8. Clique em **Seguinte**.
      ![Ferramenta copiar – página de propriedades](./media/data-factory-azure-blob-connector/copy-tool-properties-page.png) 
3. No Olá **arquivo de dados de origem** página, clique em **Blob Storage do Azure** mosaico. Utiliza este arquivo de dados de origem do página toospecify Olá Olá tarefa de cópia. Pode utilizar um serviço ligado do arquivo de dados existente (ou) especificar um novo arquivo de dados. serviço ligado de toouse existente, deverá selecionar **de serviços ligados existentes** e selecione Olá serviço ligado correto. 
    ![Ferramenta copiar – página do arquivo de dados de origem](./media/data-factory-azure-blob-connector/copy-tool-source-data-store-page.png)
4. No Olá **especificar conta de armazenamento de Blobs do Azure Olá** página:
   1. Mantenha o nome de Olá gerado automaticamente para **nome da ligação**. nome da ligação Olá é o nome de Olá do serviço de Olá ligado do tipo: armazenamento do Azure. 
   2. Confirme que a opção **A partir de subscrições do Azure** está selecionada para o **Método de seleção de contas**.
   3. Selecione a sua subscrição do Azure ou manter **Selecionar tudo** para **subscrição do Azure**.   
   4. Selecione um **conta do storage do Azure** de Olá contas disponível na subscrição Olá selecionado de lista de armazenamento do Azure. Pode também escolher tooenter as definições de conta de armazenamento manualmente selecionando **introduzir manualmente** opção para Olá **método de seleção de contas**.
   5. Clique em **Seguinte**. 
      ![Ferramenta copiar – especificar a conta de armazenamento de Blobs do Azure Olá](./media/data-factory-azure-blob-connector/copy-tool-specify-azure-blob-storage-account.png)
5. No **pasta ou ficheiro de entrada escolha Olá** página:
   1. Faça duplo clique em **adfblobcontainer**.
   2. Selecione **entrada**e clique em **escolha**. Nestas instruções, selecionar pasta de entrada Olá. Pode também selecionar Olá emp.txt ficheiro na pasta Olá em vez disso. 
      ![Ferramenta copiar – escolha a pasta ou ficheiro de entrada Olá](./media/data-factory-azure-blob-connector/copy-tool-choose-input-file-or-folder.png)
6. No Olá **pasta ou ficheiro de entrada escolha Olá** página:
    1. Confirme que Olá **ficheiro ou pasta** estiver definido demasiado**adfblobconnector/entrada**. Se forem ficheiros Olá em subpastas, por exemplo, 2017/04/01, 2017/04/02 e assim sucessivamente, introduza adfblobconnector/valor / {year} / {month} / {day} para o ficheiro ou pasta. Quando prime SEPARADOR fora de caixa de texto Olá, será apresentada três formatos de tooselect na lista pendente (AAAA) de ano, mês (MM) e dia (dd). 
    2. Não defina **copiar recursivamente ficheiro**. Selecione este passam de toorecursively opção através de pastas para ficheiros toobe toohello copiados de destino. 
    3. Não Olá **cópia binária** opção. Selecione esta opção tooperform uma cópia binária do destino de toohello do ficheiro de origem. Não selecione para estas instruções para que possa ver mais opções em páginas seguintes Olá. 
    4. Confirme que Olá **tipo de compressão** estiver definido demasiado**nenhum**. Selecione um valor para esta opção se os ficheiros de origem são comprimidos dos formatos de Olá suportado. 
    5. Clique em **Seguinte**.
    ![Ferramenta copiar – escolha a pasta ou ficheiro de entrada Olá](./media/data-factory-azure-blob-connector/chose-input-file-folder.png) 
7. No Olá **definições do formato de ficheiro** página, verá os delimitadores Olá e esquema de Olá que é detetada automaticamente pelo Assistente de Olá ao analisar o ficheiro de Olá. 
    1. Confirmar Olá seguintes opções: uma. Olá **formato de ficheiro** estiver definido demasiado**formato de texto**. Pode ver todos os formatos de Olá suportado Olá na lista pendente. Por exemplo: JSON, Avro, ORC, Parquet.
        b. Olá **delimitador de coluna** estiver definido demasiado`Comma (,)`. Pode ver Olá outros delimitadores de coluna suportados pela fábrica de dados no Olá na lista pendente. Também pode especificar um delimitador personalizado.
        c. Olá **delimitador de linha** estiver definido demasiado`Carriage Return + Line feed (\r\n)`. Pode ver Olá outros delimitadores de linha suportados pela fábrica de dados no Olá na lista pendente. Também pode especificar um delimitador personalizado.
        d. Olá **ignorar a contagem de linha** estiver definido demasiado**0**. Se pretender que alguns toobe de linhas ignorado, Olá parte superior do ficheiro de Olá, introduza o número de Olá aqui.
        e.  Olá **primeira linha de dados contém nomes de colunas** não está definido. Se os ficheiros de origem Olá contém nomes de colunas na primeira linha de Olá, selecione esta opção.
        f. Olá **tratar o valor de coluna vazia como null** opção estiver definida.
    2. Expanda **definições avançadas** toosee avançadas opção disponível.
    3. Em Olá parte inferior da página Olá, consulte Olá **pré-visualização** dos dados a partir do ficheiro de emp.txt Olá.
    4. Clique em **esquema** separador no esquema do Olá inferior toosee Olá nesse assistente de cópia de Olá inferido observando dados Olá no ficheiro de origem Olá.
    5. Clique em **seguinte** depois de analisar os delimitadores Olá e pré-visualizar os dados.
    ![Ferramenta copiar – definições do formato de ficheiro](./media/data-factory-azure-blob-connector/copy-tool-file-format-settings.png)  
8. No Olá **página do arquivo de dados de destino**, selecione **Blob Storage do Azure**e clique em **seguinte**. Olá Blob Storage do Azure está a utilizar como ambos os arquivos de dados de Olá origem e de destino, esta explicação passo a passo.    
    ![Ferramenta copiar – arquivo de dados de destino selecione](media/data-factory-azure-blob-connector/select-destination-data-store.png)
9. No **especificar conta de armazenamento de Blobs do Azure Olá** página:
   1. Introduza **AzureStorageLinkedService** para Olá **nome da ligação** campo.
   2. Confirme que a opção **A partir de subscrições do Azure** está selecionada para o **Método de seleção de contas**.
   3. Selecione a sua **subscrição** do Azure.  
   4. Selecione a sua conta de armazenamento do Azure. 
   5. Clique em **Seguinte**.     
10. No Olá **Olá de escolha de saída do ficheiro ou pasta** página: 
    6. Especifique **caminho da pasta** como **adfblobconnector/saída / {year} / {month} / {day}**. Introduza **SEPARADOR**.
    7. Para Olá **ano**, selecione **aaaa**.
    8. Para Olá **mês**, confirme que está definido demasiado**MM**.
    9. Para Olá **dia**, confirme que está definido demasiado**dd**.
    10. Confirme que Olá **tipo de compressão** estiver definido demasiado**nenhum**.
    11. Confirme que Olá **copiar comportamento** estiver definido demasiado**intercalar ficheiros**. Se o ficheiro com Olá já existe mesmo nome de saída Olá, hello novo conteúdo é adicionado toohello mesmo ficheiro no fim de Olá.
    12. Clique em **Seguinte**.
    ![Ferramenta copiar – escolha a pasta ou ficheiro de saída](media/data-factory-azure-blob-connector/choose-the-output-file-or-folder.png)
11. No Olá **definições do formato de ficheiro** , reveja as definições de Olá e, em **seguinte**. Uma das opções adicionais Olá aqui é tooadd um ficheiro de saída de toohello do cabeçalho. Se selecionar esta opção, uma linha de cabeçalho é adicionada com nomes de colunas de Olá do esquema de Olá da origem de Olá. Pode mudar o nome de Olá nomes predefinidos das colunas ao visualizar o esquema de Olá para a origem de Olá. Por exemplo, pode alterar Olá primeira coluna tooFirst nome e a segunda coluna tooLast nome. Em seguida, o ficheiro de saída Olá é gerado com um cabeçalho com estes nomes como nomes de colunas. 
    ![Ferramenta copiar – definições do formato de ficheiro de destino](media/data-factory-azure-blob-connector/file-format-destination.png)
12. No Olá **definições de desempenho** página, confirme que **nuvem unidades** e **paralela cópias** estão definidas demasiado**automática**e clique em seguinte. Para obter detalhes sobre estas definições, consulte [copiar guia Otimização e de desempenho de atividade](data-factory-copy-activity-performance.md#parallel-copy).
    ![Ferramenta copiar – definições de desempenho](media/data-factory-azure-blob-connector/copy-performance-settings.png) 
14. No Olá **resumo** página, reveja as definições de todos os (propriedades da tarefa, as definições de origem e de destino e as definições de cópia) e clique em **seguinte**.
    ![Ferramenta copiar – página de resumo](media/data-factory-azure-blob-connector/copy-tool-summary-page.png)
15. Reveja as informações na Olá **resumo** página e clique em **concluir**. Assistente de Olá cria dois serviços ligados, dois conjuntos de dados (entrada e saída) e um pipeline na fábrica de dados de Olá (a partir de onde foi iniciado Olá Assistente para copiar).
    ![Ferramenta copiar – página de implementação](media/data-factory-azure-blob-connector/copy-tool-deployment-page.png)

### <a name="monitor-hello-pipeline-copy-task"></a>Monitorizar o pipeline Olá (tarefa de cópia)

1. Clique em ligação Olá `Click here toomonitor copy pipeline` no Olá **implementação** página. 
2. Deverá ver Olá **monitorizar e gerir aplicações** num separador separado.  ![Monitorizar e gerir aplicações](media/data-factory-azure-blob-connector/monitor-manage-app.png)
3. Olá alteração **iniciar** tempo na parte superior do Olá demasiado`04/19/2017` e **final** demasiado tempo`04/27/2017`e, em seguida, clique em **aplicar**. 
4. Deverá ver cinco janelas de atividade do Olá **ATIVIDADE WINDOWS** lista. Olá **WindowStart** vezes devem abranger todos os dias da hora de fim do pipeline início toopipeline. 
5. Clique em **atualizar** botão para Olá **ATIVIDADE WINDOWS** lista algumas horas até ver estado Olá de todas as janelas de atividade de Olá está definida tooReady. 
6. Agora, certifique-se de que os ficheiros de saída Olá são gerados na pasta de saída de Olá do contentor de adfblobconnector. Deverá ver Olá seguir a estrutura de pastas na pasta de saída Olá: 
    ```
    2017/04/21
    2017/04/22
    2017/04/23
    2017/04/24
    2017/04/25    
    ```
Para obter informações detalhadas sobre como monitorizar e gerir as fábricas de dados, consulte [monitorizar e gerir o pipeline do Data Factory](data-factory-monitor-manage-app.md) artigo. 
 
### <a name="data-factory-entities"></a>Entidades da fábrica de dados
Agora, mude o separador de back-toohello com Olá home page da fábrica de dados. Tenha em atenção que existem dois serviços ligados, dois conjuntos de dados e um pipeline na fábrica de dados agora. 

![Página inicial de fábrica de dados com entidades](media/data-factory-azure-blob-connector/data-factory-home-page-with-numbers.png)

Clique em **autor e implementar** toolaunch Editor do Data Factory. 

![Editor do Data Factory](media/data-factory-azure-blob-connector/data-factory-editor.png)

Deverá ver Olá seguintes entidades do Data Factory na fábrica de dados: 

 - Dois serviços ligados. Uma para a origem de Olá e Olá outro para o destino de Olá. Ambos os serviços de Olá ligado Consulte toohello mesma conta de armazenamento do Azure esta explicação passo a passo. 
 - Dois conjuntos de dados. Um conjunto de dados de entrada e um conjunto de dados de saída. Nestas instruções, ambos utilizam Olá mesmo contentor de blob mas Consulte toodifferent pastas (entrada e saída).
 - Um pipeline. pipeline de Olá contém uma atividade de cópia que utiliza uma origem de blob e um blob sink toocopy de dados de um tooanother de localização de blob do Azure a localização de blob do Azure. 

Olá secções seguintes fornecem mais informações sobre estas entidades. 

#### <a name="linked-services"></a>Serviços ligados
Deverá ver dois serviços ligados. Uma para a origem de Olá e Olá outro para o destino de Olá. Esta explicação passo a passo, o aspeto ambas as definições Olá mesmo, exceto para os nomes de Olá. Olá **tipo** de Olá serviço ligado está definido demasiado**AzureStorage**. A propriedade mais importante da definição de serviço ligado de Olá está Olá **connectionString**, que é utilizado pelo Data Factory tooconnect tooyour conta de armazenamento do Azure no tempo de execução. Ignore a propriedade de hubName Olá na definição de Olá. 

##### <a name="source-blob-storage-linked-service"></a>Serviço de ligado do armazenamento de BLOBs de origem
```json
{
    "name": "Source-BlobStorage-z4y",
    "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=mystorageaccount;AccountKey=**********"
        }
    }
}
```

##### <a name="destination-blob-storage-linked-service"></a>Serviço de ligado do armazenamento de BLOBs de destino

```json
{
    "name": "Destination-BlobStorage-z4y",
    "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=mystorageaccount;AccountKey=**********"
        }
    }
}
```

Para mais informações sobre o serviço ligado do Storage do Azure, consulte [ligado propriedades do serviço](#linked-service-properties) secção. 

#### <a name="datasets"></a>Conjuntos de dados
Existem dois conjuntos de dados: um conjunto de dados de entrada e um conjunto de dados de saída. tipo de Olá de Olá conjunto de dados está definido demasiado**AzureBlob** para ambos. 

conjunto de dados de entrada Olá pontos toohello **entrada** pasta de Olá **adfblobconnector** contentor do blob. Olá **externo** for definida demasiado**verdadeiro** deste conjunto de dados como Olá dados não é produzidos pelo pipeline Olá com atividade de cópia de Olá que demora este conjunto de dados como entrada. 

Olá toohello de pontos de conjunto de dados de saída **saída** pasta de Olá mesmo contentor de blob. Olá conjunto de dados de saída também utiliza Olá ano, mês e dia Olá **SliceStart** toodynamically variável sistema avaliar caminho Olá para o ficheiro de saída Olá. Para obter uma lista de funções e variáveis do sistema suportadas pela fábrica de dados, consulte [funções de Data Factory e variáveis do sistema](data-factory-functions-variables.md). Olá **externo** for definida demasiado**falso** (valor predefinido) porque este conjunto de dados é produzido pelo pipeline Olá. 

Para obter mais informações sobre as propriedades suportadas pelo conjunto de dados de Blobs do Azure, consulte [propriedades do Dataset](#dataset-properties) secção.

##### <a name="input-dataset"></a>Conjunto de dados de entrada

```json
{
    "name": "InputDataset-z4y",
    "properties": {
        "structure": [
            { "name": "Prop_0", "type": "String" },
            { "name": "Prop_1", "type": "String" }
        ],
        "type": "AzureBlob",
        "linkedServiceName": "Source-BlobStorage-z4y",
        "typeProperties": {
            "folderPath": "adfblobconnector/input/",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ","
            }
        },
        "availability": {
            "frequency": "Day",
            "interval": 1
        },
        "external": true,
        "policy": {}
    }
}
```

##### <a name="output-dataset"></a>Conjunto de dados de saída

```json
{
    "name": "OutputDataset-z4y",
    "properties": {
        "structure": [
            { "name": "Prop_0", "type": "String" },
            { "name": "Prop_1", "type": "String" }
        ],
        "type": "AzureBlob",
        "linkedServiceName": "Destination-BlobStorage-z4y",
        "typeProperties": {
            "folderPath": "adfblobconnector/output/{year}/{month}/{day}",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ","
            },
            "partitionedBy": [
                { "name": "year", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyy" } },
                { "name": "month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
                { "name": "day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } }
            ]
        },
        "availability": {
            "frequency": "Day",
            "interval": 1
        },
        "external": false,
        "policy": {}
    }
}
```

#### <a name="pipeline"></a>Pipeline
pipeline de Olá tem apenas uma atividade. Olá **tipo** de Olá atividade está definida demasiado**cópia**.  Nas propriedades do tipo de Olá para a atividade de Olá, existem duas secções, um para a origem e Olá outro para sink. tipo de origem Olá estiver definido demasiado**BlobSource** como atividade Olá copia dados do armazenamento de Blobs. Olá o tipo de sink estiver definido demasiado**BlobSink** como atividade Olá copiar o blob storage tooa dados. atividade de cópia de Olá aceita InputDataset z4y como comentários de Olá e OutputDataset-z4y como saída Olá. 

Para obter mais informações sobre propriedades suportadas por BlobSource e BlobSink, consulte [copiar propriedades da atividade](#copy-activity-properties) secção. 

```json
{
    "name": "CopyPipeline",
    "properties": {
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "BlobSource",
                        "recursive": false
                    },
                    "sink": {
                        "type": "BlobSink",
                        "copyBehavior": "MergeFiles",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "InputDataset-z4y"
                    }
                ],
                "outputs": [
                    {
                        "name": "OutputDataset-z4y"
                    }
                ],
                "policy": {
                    "timeout": "1.00:00:00",
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "style": "StartOfInterval",
                    "retry": 3,
                    "longRetry": 0,
                    "longRetryInterval": "00:00:00"
                },
                "scheduler": {
                    "frequency": "Day",
                    "interval": 1
                },
                "name": "Activity-0-Blob path_ adfblobconnector_input_->OutputDataset-z4y"
            }
        ],
        "start": "2017-04-21T22:34:00Z",
        "end": "2017-04-25T05:00:00Z",
        "isPaused": false,
        "pipelineMode": "Scheduled"
    }
}
```

## <a name="json-examples-for-copying-data-tooand-from-blob-storage"></a>Exemplos JSON para copiar dados tooand do armazenamento de BLOBs  
Olá exemplos seguintes fornecem definições JSON de exemplo que pode utilizar toocreate um pipeline utilizando [portal do Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) ou [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) ou [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md). Estes mostram como toocopy tooand de dados do Blob Storage do Azure e SQL Database do Azure. No entanto, os dados podem ser copiados **diretamente** de qualquer uma das origens tooany de Olá sinks indicado [aqui](data-factory-data-movement-activities.md#supported-data-stores-and-formats) utilizando Olá atividade de cópia no Azure Data Factory.

### <a name="json-example-copy-data-from-blob-storage-toosql-database"></a>Exemplo JSON: Copiar dados de armazenamento de BLOBs tooSQL da base de dados
Olá seguinte exemplo mostra:

1. Um serviço ligado do tipo [AzureSqlDatabase](data-factory-azure-sql-connector.md#linked-service-properties).
2. Um serviço ligado do tipo [AzureStorage](#linked-service-properties).
3. Uma entrada [dataset](data-factory-create-datasets.md) do tipo [AzureBlob](#dataset-properties).
4. Uma saída [dataset](data-factory-create-datasets.md) do tipo [AzureSqlTable](data-factory-azure-sql-connector.md#dataset-properties).
5. A [pipeline](data-factory-create-pipelines.md) com uma atividade de cópia que utiliza [BlobSource](#copy-activity-properties) e [SqlSink](data-factory-azure-sql-connector.md#copy-activity-properties).

exemplo de Olá copia dados de séries de tempo de uma tabela de SQL do Azure do blob do Azure tooan hora a hora. Propriedades JSON de Olá utilizadas nestes exemplos são descritas nas secções seguintes exemplos de Olá.

**Serviço ligado SQL do Azure:**

```json
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
**Serviço ligado do Storage do Azure:**

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
O Azure Data Factory suportam dois tipos de serviços de armazenamento do Azure ligado: **AzureStorage** e **AzureStorageSas**. Para Olá primeiro, especifique a cadeia de ligação de Olá que incluem a chave de conta Olá e para Olá posteriormente, um, especificar Olá Uri de assinatura de acesso partilhado (SAS). Consulte [serviços ligados](#linked-service-properties) secção para obter detalhes.  

**Conjunto de dados de entrada Blob do Azure:**

Dados são captados um blob de novo a cada hora (frequência: hora, intervalo: 1). Olá pasta caminho e nome de ficheiro para o blob Olá dinamicamente são avaliados com base na hora de início de Olá do setor de Olá que está a ser processado. caminho da pasta Olá utiliza ano, mês e parte de dia da hora de início de Olá e nome de ficheiro utiliza a parte de hora Olá Olá da hora de início. "external": "true" definição informa fábrica de dados nessa tabela Olá é toohello externo fábrica de dados e não é produzida por uma atividade no factory de dados de Olá.

```json
{
  "name": "AzureBlobInput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}/",
      "fileName": "{Hour}.csv",
      "partitionedBy": [
        { "name": "Year", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyy" } },
        { "name": "Month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
        { "name": "Day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } },
        { "name": "Hour", "value": { "type": "DateTime", "date": "SliceStart", "format": "HH" } }
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
**Conjunto de dados de saída do SQL do Azure:**

exemplo de Olá copia a tabela de tooa de dados com o nome "MyTable" numa base de dados SQL do Azure. Criar tabela Olá na base de dados SQL do Azure com Olá o mesmo número de colunas como esperado Olá Blob CSV ficheiro toocontain. Novas linhas são adicionadas toohello tabela cada hora.

```json
{
  "name": "AzureSqlOutput",
  "properties": {
    "type": "AzureSqlTable",
    "linkedServiceName": "AzureSqlLinkedService",
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
**Uma atividade de cópia num pipeline com a origem de Blob e o sink do SQL Server:**

Olá pipeline contém uma atividade de cópia é configurado toouse Olá conjuntos de dados de entrada e de saída e é agendada toorun a cada hora. No pipeline de Olá definição JSON, Olá **origem** tipo está definido demasiado**BlobSource** e **sink** tipo está definido demasiado**SqlSink**.

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
            "name": "AzureSqlOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "BlobSource"
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
### <a name="json-example-copy-data-from-azure-sql-tooazure-blob"></a>Exemplo JSON: Copiar dados de SQL do Azure tooAzure Blob
Olá seguinte exemplo mostra:

1. Um serviço ligado do tipo [AzureSqlDatabase](data-factory-azure-sql-connector.md#linked-service-properties).
2. Um serviço ligado do tipo [AzureStorage](#linked-service-properties).
3. Uma entrada [dataset](data-factory-create-datasets.md) do tipo [AzureSqlTable](data-factory-azure-sql-connector.md#dataset-properties).
4. Uma saída [dataset](data-factory-create-datasets.md) do tipo [AzureBlob](#dataset-properties).
5. A [pipeline](data-factory-create-pipelines.md) com atividade de cópia que utiliza [SqlSource](data-factory-azure-sql-connector.md#copy-activity-properties) e [BlobSink](#copy-activity-properties).

exemplo de Olá copia dados de séries de tempo de um tooan de tabela SQL do Azure blob do Azure numa base horária. Propriedades JSON de Olá utilizadas nestes exemplos são descritas nas secções seguintes exemplos de Olá.

**Serviço ligado SQL do Azure:**

```json
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
**Serviço ligado do Storage do Azure:**

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
O Azure Data Factory suportam dois tipos de serviços de armazenamento do Azure ligado: **AzureStorage** e **AzureStorageSas**. Para Olá primeiro, especifique a cadeia de ligação de Olá que incluem a chave de conta Olá e para Olá posteriormente, um, especificar Olá Uri de assinatura de acesso partilhado (SAS). Consulte [serviços ligados](#linked-service-properties) secção para obter detalhes.  

**Conjunto de dados de entrada SQL do Azure:**

exemplo de Olá pressupõe que criou uma tabela "MyTable" SQL do Azure e contém uma coluna chamada "timestampcolumn" para dados de séries de tempo.

A definição "external": "true" informa serviço Data Factory nessa tabela Olá é toohello externo fábrica de dados e não é produzida por uma atividade no factory de dados de Olá.

```json
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

**Conjunto de dados de saída do Blob do Azure:**

São escritos dados no blob tooa de novo a cada hora (frequência: hora, intervalo: 1). caminho da pasta Olá para BLOBs Olá dinamicamente é avaliado com base na hora de início de Olá do setor de Olá que está a ser processado. caminho da pasta Olá utiliza ano, mês, dia e horas partes Olá da hora de início.

```json
{
  "name": "AzureBlobOutput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}/",
      "partitionedBy": [
        {
          "name": "Year",
          "value": { "type": "DateTime",  "date": "SliceStart", "format": "yyyy" } },
        { "name": "Month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
        { "name": "Day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } },
        { "name": "Hour", "value": { "type": "DateTime", "date": "SliceStart", "format": "HH" } }
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

**Uma atividade de cópia num pipeline com a origem SQL e o sink de Blob:**

Olá pipeline contém uma atividade de cópia é configurado toouse Olá conjuntos de dados de entrada e de saída e é agendada toorun a cada hora. No pipeline de Olá definição JSON, Olá **origem** tipo está definido demasiado**SqlSource** e **sink** tipo está definido demasiado**BlobSink**. consulta SQL Olá especificada para Olá **SqlReaderQuery** propriedade seleciona dados Olá Olá passado toocopy de hora.

```json
{  
    "name":"SamplePipeline",
    "properties":{  
        "start":"2014-06-01T18:00:00",
        "end":"2014-06-01T19:00:00",
        "description":"pipeline for copy activity",
        "activities":[  
              {
                "name": "AzureSQLtoBlob",
                "description": "copy activity",
                "type": "Copy",
                "inputs": [
                  {
                    "name": "AzureSQLInput"
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

> [!NOTE]
> colunas de toomap toocolumns de conjunto de dados de origem do conjunto de dados dependente, consulte [mapeamento de colunas do conjunto de dados no Azure Data Factory](data-factory-map-columns.md).

## <a name="performance-and-tuning"></a>Desempenho e a otimização
Consulte [desempenho de atividade de cópia & otimização guia](data-factory-copy-activity-performance.md) toolearn sobre chave factors desse desempenho impacto de movimento de dados (atividade de cópia) no Azure Data Factory e várias formas toooptimize-lo.
