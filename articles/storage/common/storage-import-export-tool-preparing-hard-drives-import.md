---
title: "unidades de disco rígido aaaPreparing para um Azure para importar/exportar importar tarefa | Microsoft Docs"
description: "Saiba como unidades de disco rígido tooprepare utilizando Olá WAImportExport ferramenta toocreate uma tarefa de importação para Olá serviço importar/exportar do Azure."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: muralikk
ms.openlocfilehash: dc4f4f580f70dbd504317f59df142b3e4c48cb66
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="preparing-hard-drives-for-an-import-job"></a>Preparar os discos rígidos de uma tarefa de importação

Olá WAImportExport ferramenta é preparação de unidade de Olá e a ferramenta de reparação que pode utilizar com Olá [serviço de importação/exportação do Microsoft Azure](../storage-import-export-service.md). Pode utilizar esta ferramenta toocopy dados toohello unidades de disco rígido que vai tooship tooan datacenter do Azure. Depois de uma tarefa de importação foi concluída, que pode utilizar esta ferramenta toorepair blobs que foram corrompidos, foram em falta ou em conflito com outros blobs. Depois de receber Olá unidades de uma tarefa de exportação foi concluída, pode utilizar esta ferramenta toorepair todos os ficheiros que foram danificados ou em falta no Olá unidades. Neste artigo, vamos abordar utilize Olá desta ferramenta.

## <a name="prerequisites"></a>Pré-requisitos

### <a name="requirements-for-waimportexportexe"></a>Requisitos para WAImportExport.exe

- **Configuração da máquina**
  - Windows 7, Windows Server 2008 R2 ou um sistema de operativo mais recente do Windows
  - .NET framework 4 tem de estar instalado. Consulte [FAQ](#faq) sobre toocheck se o .net Framework está instalado na máquina de Olá.
- **Chave de conta de armazenamento** -precisa de, pelo menos, uma das chaves de conta Olá Olá conta de armazenamento.

### <a name="preparing-disk-for-import-job"></a>Preparar o disco para a tarefa de importação

- **BitLocker -** BitLocker tem de estar ativado na ferramenta de WAImportExport de Olá em execução do Olá máquina. Consulte Olá [FAQ](#faq) como tooenable BitLocker.
- **Discos** acessível a partir do computador no qual a ferramenta de WAImportExport é executada. Consulte [FAQ](#faq) para a especificação de disco.
- **Ficheiros de origem** -os ficheiros de Olá planear tooimport têm de estar acessíveis a partir da máquina de cópia de Olá, quer estejam na partilha de rede ou uma unidade de disco rígida local.

### <a name="repairing-a-partially-failed-import-job"></a>Reparação de uma tarefa de importação parcialmente falhada

- **Ficheiro de registo de cópia** que é gerado quando o serviço importar/exportar do Azure copia dados entre a conta de armazenamento e de disco. Está localizado na sua conta de armazenamento de destino.

### <a name="repairing-a-partially-failed-export-job"></a>Reparação de uma tarefa de exportação parcialmente falhada

- **Ficheiro de registo de cópia** que é gerado quando o serviço importar/exportar do Azure copia dados entre a conta de armazenamento e de disco. Está localizado na sua conta de armazenamento de origem.
- **Ficheiro de manifesto** -Located [opcional] no disco exportado que foi devolvido pela Microsoft.

## <a name="download-and-install-waimportexport"></a>Transfira e instale WAImportExport

Transferir Olá [versão mais recente do WAImportExport.exe](https://www.microsoft.com/download/details.aspx?id=55280). Extrair Olá zipado tooa conteúdo de diretório no seu computador.

A próxima tarefa consiste toocreate ficheiros CSV.

## <a name="prepare-hello-dataset-csv-file"></a>Preparar o ficheiro CSV Olá conjunto de dados

### <a name="what-is-dataset-csv"></a>O que é o conjunto de dados CSV

Um ficheiro CSV de conjunto de dados é Olá o valor do sinalizador /dataset é um ficheiro CSV que contém uma lista de diretórios e/ou uma lista de ficheiros copiado de toobe tootarget unidades. Olá primeiro passo toocreating uma tarefa de importação é toodetermine os diretórios e ficheiros vão tooimport. Isto pode ser uma lista de diretórios, uma lista dos ficheiros exclusivos ou uma combinação desses dois. Quando um diretório estiver incluído, todos os ficheiros no diretório de Olá e nos seus subdiretórios irão fazer parte da tarefa de importação de Olá.

Para cada toobe diretório ou ficheiro importado, tem de identificar um diretório virtual de destino ou um blob na Olá serviço Blob do Azure. Irá utilizar nestes destinos como ferramenta de WAImportExport toohello de entradas. Diretórios devem ser delimitados com caráter de barra Olá "/".

Olá, a tabela seguinte mostra alguns exemplos de destinos de blob:

| Ficheiro de origem ou diretório | Blob de destino ou diretório virtual |
| --- | --- |
| H:\Video | https://mystorageaccount.blob.Core.Windows.NET/Video |
| H:\Photo | https://mystorageaccount.blob.Core.Windows.NET/Photo |
| K:\Temp\FavoriteVideo.ISO | https://mystorageaccount.blob.Core.Windows.NET/Favorite/FavoriteVideo.ISO |
| \\myshare\john\music | https://mystorageaccount.blob.Core.Windows.NET/Music |

### <a name="sample-datasetcsv"></a>Dataset.csv de exemplo

```
BasePath,DstBlobPathOrPrefix,BlobType,Disposition,MetadataFile,PropertiesFile
"F:\50M_original\100M_1.csv.txt","containername/100M_1.csv.txt",BlockBlob,rename,"None",None
"F:\50M_original\","containername/",BlockBlob,rename,"None",None
```

### <a name="dataset-csv-file-fields"></a>Campos de ficheiro CSV de conjunto de dados

| Campo | Descrição |
| --- | --- |
| BasePath | **[Necessário]**<br/>valor de Olá deste parâmetro representa origem olá onde está localizada a Olá dados toobe importado. ferramenta de Olá irá recursivamente copiar todos os dados localizados neste caminho.<br><br/>**Valores permitidos**: Isto tem toobe um caminho válido no computador local ou um caminho de partilha válido e devem estar acessível aos utilizadores Olá. caminho do diretório Olá tem de ser um caminho absoluto (não um caminho relativo). Se o caminho de Olá termina com "\\", representa um diretório pessoa um caminho final sem"\\" representa um ficheiro.<br/>Não existem regex é permitido neste campo. Se o caminho de Olá contiver espaços, coloque-o "".<br><br/>**Exemplo**: "c:\Directory\c\Directory\File.txt"<br>"\\\\FBaseFilesharePath.domain.net\sharename\directory\"  |
| DstBlobPathOrPrefix | **[Necessário]**<br/> Olá caminho toohello destino diretório virtual na sua conta de armazenamento do Windows Azure. diretório virtual Olá pode ou não pode já existir. Se não existir, irá criar um serviço de importação/exportação.<br/><br/>Ser toouse se os nomes dos contentores válidos quando especificar diretórios virtuais de destino ou blobs. Tenha em atenção que os nomes dos contentores têm de estar em minúsculas. Para regras de nomenclatura de contentor, consulte [nomenclatura e referência de contentores, Blobs e metadados](/rest/api/storageservices/naming-and-referencing-containers--blobs--and-metadata). Se apenas raiz for especificada, a estrutura de diretórios Olá da origem de Olá é replicada no contentor de blob de destino Olá. Se pretender que a estrutura de diretórios diferentes Olá um na origem, várias linhas de mapeamento de CSV<br/><br/>Pode especificar um contentor ou um prefixo de blob, como leitores de música/70s /. Olá diretório de destino tem de começar com o nome do contentor Olá, seguido por uma barra "/" e, opcionalmente, pode incluir um diretório virtual blob que termina com "/".<br/><br/>Quando o contentor de destino Olá recipiente-raiz Olá, tem de especificar explicitamente recipiente-raiz Olá, incluindo Olá barra, como $root /. Uma vez que não podem incluir os blobs no contentor de raiz de Olá "/" nos respetivos nomes, não serão copiados todos os subdiretórios no diretório de origem Olá ao diretório de destino Olá é recipiente-raiz Olá.<br/><br/>**Exemplo**<br/>Se o caminho de blob de destino Olá https://mystorageaccount.blob.core.windows.net/video, valor de Olá deste campo pode ser vídeo /  |
| BlobType | **[Opcional]**  Bloco &#124; página<br/>Atualmente, o serviço de importação/exportação suporta 2 tipos de Blobs. Página os blobs e bloco BlobsBy predefinição em todos os ficheiros serão importados como Blobs de blocos. E \*. vhd e \*importado. vhdx como BlobsThere de página é um limite Olá-BLOBs de blocos e BLOBs de páginas tamanho permitido. Consulte [metas de escalabilidade do armazenamento](storage-scalability-targets.md#scalability-targets-for-blobs-queues-tables-and-files) para obter mais informações.  |
| Disposição | **[Opcional]**  mudar o nome de &#124; substituir o não &#124; substituir <br/> Este campo especifica o comportamento de cópia Olá durante a importação revertidos Quando os dados estão a ser carregado toohello a conta de armazenamento do disco de Olá. Opções disponíveis são: mudar o nome &#124; Substituir &#124; não de substituição. As predefinições demasiado "mudar o nome" se nada especificado. <br/><br/>**Mudar o nome**: Se estiver presente um objeto com o mesmo nome, cria uma cópia no destino.<br/>Substituir: substitui o ficheiro de Olá com o ficheiro mais recente. ficheiro de Olá com last-modified wins.<br/>**Substituir o não**: ignora a escrever Olá ficheiro se já está presente.|
| MetadataFile | **[Opcional]** <br/>o campo de toothis do valor Olá é o ficheiro de metadados de Olá que pode ser fornecido se precisar de Olá um toopreserve Olá metadados de objetos de Olá ou forneça metadados personalizados. Ficheiro de metadados de toohello de caminho para os blobs de destino Olá. Consulte [metadados e o formato de ficheiro de propriedades de serviço de importação/exportação](../storage-import-export-file-format-metadata-and-properties.md) para obter mais informações |
| PropertiesFile | **[Opcional]** <br/>Ficheiro de propriedade de toohello de caminho para os blobs de destino Olá. Consulte [metadados e o formato de ficheiro de propriedades de serviço de importação/exportação](../storage-import-export-file-format-metadata-and-properties.md) para obter mais informações. |

## <a name="prepare-initialdriveset-or-additionaldriveset-csv-file"></a>Preparar ficheiro InitialDriveSet ou AdditionalDriveSet CSV

### <a name="what-is-driveset-csv"></a>O que é driveset CSV

Olá o valor do sinalizador de /InitialDriveSet ou /AdditionalDriveSet Olá é um ficheiro CSV que contém a lista de Olá dos discos letras de unidade de Olá toowhich estão mapeadas para que hello ferramenta pode corretamente escolher lista Olá de toobe discos preparado. Se o tamanho dos dados Olá for superior a um tamanho de disco único, o ferramenta de WAImportExport Olá distribuir dados Olá entre múltiplos discos inscritas neste ficheiro CSV de uma forma otimizada.

Não há nenhum limite do número de Olá dos dados de Olá discos pode ser escrito tooin uma única sessão. ferramenta de Olá será distribuir dados com base no tamanho do disco e o tamanho da pasta. Irá selecionar disco Olá que é a maioria das otimizadas para o tamanho de objeto Olá. Olá dados quando carregado toohello conta de armazenamento será convergida toohello back-estrutura de diretórios que foi especificada no ficheiro de conjunto de dados. Na ordem toocreate um driveset CSV, siga os passos de Olá abaixo.

### <a name="create-basic-volume-and-assign-drive-letter"></a>Criar o volume básico e atribua a letra de unidade

Na ordem toocreate um volume básico e atribuir uma letra de unidade, seguindo as instruções de Olá para "Criação de partições mais simples" fornecido durante a [descrição geral da gestão de discos](https://technet.microsoft.com/library/cc754936.aspx).

### <a name="sample-initialdriveset-and-additionaldriveset-csv-file"></a>Ficheiro de exemplo InitialDriveSet e AdditionalDriveSet CSV

```
DriveLetter,FormatOption,SilentOrPromptOnFormat,Encryption,ExistingBitLockerKey
G,AlreadyFormatted,SilentMode,AlreadyEncrypted,060456-014509-132033-080300-252615-584177-672089-411631
H,Format,SilentMode,Encrypt,
```

### <a name="driveset-csv-file-fields"></a>Campos dos ficheiros Driveset CSV

| Campos | Valor |
| --- | --- |
| Letradaunidade | **[Necessário]**<br/> Cada unidade que está a ser fornecida ferramenta toohello como destino de Olá tem de ter um volume NTFS simples no mesmo e uma letra de unidade atribuída tooit.<br/> <br/>**Exemplo**: R ou r |
| FormatOption | **[Necessário]**  Formato &#124; AlreadyFormatted<br/><br/> **Formato**: especificar Isto irá formatar todos os dados de Olá no disco Olá. <br/>**AlreadyFormatted**: ferramenta Olá irá ignorar a formatação quando este valor for especificado. |
| SilentOrPromptOnFormat | **[Necessário]**  SilentMode &#124; PromptOnFormat<br/><br/>**SilentMode**: fornecer este valor irá permitir a ferramenta de Olá toorun de utilizador no modo silencioso. <br/>**PromptOnFormat**: ferramenta Olá pedirá Olá utilizador tooconfirm se ação Olá destina-se realmente em cada formato.<br/><br/>Se não definir comando irá abortar e apresentar a mensagem de erro: "Valor incorreto para SilentOrPromptOnFormat: none" |
| Encriptação | **[Necessário]**  Encriptar &#124; AlreadyEncrypted<br/> valor de Olá deste campo decide que tooencrypt de disco e que não a. <br/><br/>**Encriptar**: ferramenta irá formatar a unidade de Olá. Se o valor do campo "FormatOption" for "Format", em seguida, este valor é necessário toobe "Encriptar". Se "AlreadyEncrypted" é especificado neste caso, irá resultar num erro "Quando é especificado o formato, encriptar deve ser também especificado".<br/>**AlreadyEncrypted**: ferramenta será desencripta a unidade de Olá utilizando Olá BitLockerKey fornecido no campo "ExistingBitLockerKey". Se o valor do campo "FormatOption" for "AlreadyFormatted", em seguida, este valor pode ser "Encriptar" ou "AlreadyEncrypted" |
| ExistingBitLockerKey | **[Necessário]**  Se o valor do campo "Encriptação" for "AlreadyEncrypted"<br/> o valor de Olá deste campo é a chave do BitLocker Olá que estão associado com disco específico Olá. <br/><br/>Este campo deve ser deixado em branco se o valor de Olá do campo "Encriptação" for "Encriptar".  Se a chave do BitLocker é especificado neste caso, irá resultar num erro "Chave do Bitlocker não deve ser especificado".<br/>  **Exemplo**: 060456-014509-132033-080300-252615-584177-672089-411631|

##  <a name="preparing-disk-for-import-job"></a>Preparar o disco para a tarefa de importação

unidades de tooprepare para uma tarefa de importação, chame a ferramenta de WAImportExport Olá com Olá **PrepImport** comando. Os parâmetros que incluir depende se isto é Olá primeira cópia sessão ou uma sessão de cópia subsequentes.

### <a name="first-session"></a>Primeira sessão

Primeira cópia sessão tooCopy uma ferramenta de WAImportExport de disco (consoante o que é especificado no ficheiro CSV) único/vários comandos PrepImport para Olá do diretório Single/Multiple tooa primeiro de copiar diretórios toocopy de sessão e/ou os ficheiros com uma nova sessão de cópia:

```
WAImportExport.exe PrepImport /j:<JournalFile> /id:<SessionId> [/logdir:<LogDirectory>] [/sk:<StorageAccountKey>] [/silentmode] [/InitialDriveSet:<driveset.csv>] DataSet:<dataset.csv>
```

**Exemplo:**

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#1  /sk:\*\*\*\*\*\*\*\*\*\*\*\*\* /InitialDriveSet:driveset-1.csv /DataSet:dataset-1.csv /logdir:F:\logs
```

### <a name="add-data-in-subsequent-session"></a>Adicionar dados de sessão subsequentes

Nas sessões subsequentes cópia, não terá de parâmetros do toospecify Olá iniciais. Terá de toouse Olá mesmo ficheiro diário por ordem para Olá ferramenta tooremember onde-lo à esquerda no Olá sessão anterior. Estado de Olá da sessão de cópia de Olá é escrito toohello ficheiros de diário de alterações. Segue-se a sintaxe de Olá para uma cópia subsequente diretórios adicionais de toocopy de sessão e ou ficheiros:

```
WAImportExport.exe PrepImport /j:<SameJournalFile> /id:<DifferentSessionId>  [DataSet:<differentdataset.csv>]
```

**Exemplo:**

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#2  /DataSet:dataset-2.csv
```

### <a name="add-drives-toolatest-session"></a>Adicione unidades toolatest sessão

Se os dados de Olá se enquadram em unidades especificadas no InitialDriveset, um pode utilizar a sessão de cópia de toosame tooadd unidades adicionais Olá ferramenta. 

>[!NOTE] 
>id de sessão de Olá deve corresponder ao id de sessão anterior Olá. Ficheiros do diário de alterações devem corresponder ao hello um especificado na sessão anterior.
>
```
WAImportExport.exe PrepImport /j:<SameJournalFile> /id:<SameSessionId> /AdditionalDriveSet:<newdriveset.csv>
```

**Exemplo:**

```
WAImportExport.exe PrepImport /j:SameJournalTest.jrn /id:session#2  /AdditionalDriveSet:driveset-2.csv
```

### <a name="abort-hello-latest-session"></a>Abortar Olá sessão mais recente:

Se uma sessão de cópia é interrompida e não é possível tooresume (por exemplo, se um diretório de origem foi tentativa inacessível), tem abortar Olá sessão atual para que este pode ser revertida back e novas sessões de cópia podem ser iniciadas:

```
WAImportExport.exe PrepImport /j:<SameJournalFile> /id:<SameSessionId> /AbortSession
```

**Exemplo:**

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#2  /AbortSession
```

Apenas Olá última de cópia de sessão, se terminou anormalmente, pode ser abortada. Tenha em atenção que não é possível a abortar Olá primeira sessão de cópia para uma unidade. Em vez disso, tem de reiniciar sessão de cópia de Olá com um novo ficheiro de diário de alterações.

### <a name="resume-a-latest-interrupted-session"></a>Retomar uma sessão interrompida mais recente

Se uma sessão de cópia é interrompida por qualquer motivo, pode retomá-lo ao executar a ferramenta de Olá com apenas o ficheiro de diário Olá especificado:

```
WAImportExport.exe PrepImport /j:<SameJournalFile> /id:<SameSessionId> /ResumeSession
```

**Exemplo:**

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#2 /ResumeSession
```

> [!IMPORTANT] 
> Quando retomar uma sessão de cópia, não modificar diretórios e ficheiros de dados de origem Olá adicionando ou removendo ficheiros.

## <a name="waimportexport-parameters"></a>Parâmetros de WAImportExport

| Parâmetros | Descrição |
| --- | --- |
|     /j:&lt;JournalFile&gt;  | **Necessário**<br/> Ficheiros do caminho toohello diário de alterações. Um ficheiro de diário controla um conjunto de unidades e registos Olá progresso na preparação destas unidades. ficheiros do diário de alterações de Olá sempre tem de ser especificado.  |
|     /LOGDIR:&lt;LogDirectory&gt;  | **Opcional**. diretório de registo de Olá.<br/> Ficheiros de registo verboso, bem como alguns ficheiros temporários serão escritos toothis diretório. Se não for especificado, o atual diretório será utilizado como diretório de registo Olá. Olá diretório de registo pode ser especificado apenas uma vez para Olá mesmo ficheiro de diário de alterações.  |
|     formado:&lt;SessionId&gt;  | **Necessário**<br/> Olá Id da sessão que é utilizada tooidentify uma sessão de cópia. É utilizado tooensure recuperação exata de uma sessão de cópia interrompida.  |
|     / ResumeSession  | Opcional. Se Olá última sessão de cópia foi anormalmente terminada, este parâmetro pode ser especificado tooresume Olá sessão.   |
|     / AbortSession  | Opcional. Se Olá última sessão de cópia foi anormalmente terminada, este parâmetro pode ser especificado tooabort Olá sessão.  |
|     /SN:&lt;StorageAccountName&gt;  | **Necessário**<br/> Só é aplicável para RepairImport e RepairExport. nome de Olá Olá da conta de armazenamento.  |
|     /SK:&lt;StorageAccountKey&gt;  | **Necessário**<br/> chave de Olá Olá da conta de armazenamento. |
|     / InitialDriveSet:&lt;driveset.csv&gt;  | **Necessário** quando em execução Olá primeira sessão de cópia<br/> Um ficheiro CSV que contém uma lista de unidades tooprepare.  |
|     / AdditionalDriveSet:&lt;driveset.csv&gt; | **Necessário**. Ao adicionar unidades toocurrent cópia sessão. <br/> Um ficheiro CSV que contém uma lista adicional de unidades toobe adicionado.  |
|      /r:&lt;RepairFile&gt; | **Necessário** apenas aplicável para RepairImport e RepairExport.<br/> Ficheiro de toohello de caminho para controlar o progresso de reparação. Cada unidade tem de ter um e apenas um ficheiro de reparação.  |
|     /d:&lt;TargetDirectories&gt; | **Necessário**. Só é aplicável para RepairImport e RepairExport. Para RepairImport, um ou mais toorepair de valores separados por ponto e vírgula diretórios; Para RepairExport, toorepair de um diretório, por exemplo, raiz do diretório da unidade de Olá.  |
|     / CopyLogFile:&lt;DriveCopyLogFile&gt; | **Necessário** apenas aplicável para RepairImport e RepairExport. O ficheiro de registo do caminho toohello unidade cópia (verboso ou de erros).  |
|     / ManifestFile:&lt;DriveManifestFile&gt; | **Necessário** apenas aplicável para RepairExport.<br/> Caminho toohello unidade ficheiro de manifesto.  |
|     / PathMapFile:&lt;DrivePathMapFile&gt; | **Opcional**. Só é aplicável para RepairImport.<br/> Ficheiro de toohello de caminho que contenha mapeamentos de ficheiro caminhos relativos toohello unidade raiz toolocations dos ficheiros reais (delimitado por separador). Quando especificado pela primeira vez, este será preenchido com caminhos de ficheiros com destinos vazios, que significa não se encontram no TargetDirectories, acesso negado com um nome inválido, ou existam vários diretórios. ficheiro de mapa de caminho Olá pode ser editado manualmente tooinclude caminhos de destino correto de Olá e novamente para caminhos de ficheiro do Olá ferramenta tooresolve Olá corretamente especificado.  |
|     / ExportBlobListFile:&lt;ExportBlobListFile&gt; | **Necessário**. Só é aplicável para PreviewExport.<br/> Caminho toohello XML do ficheiro que contém lista de caminhos de blob ou prefixos de caminho de Olá blobs toobe exportados do blob. formato de ficheiro Olá é Olá mesmo como Olá blob lista o formato de blob na Olá operação de colocar a tarefa de REST API do serviço de importação/exportação Olá.  |
|     / DriveSize:&lt;DriveSize&gt; | **Necessário**. Só é aplicável para PreviewExport.<br/>  Tamanho do toobe unidades utilizada para exportação. Por exemplo, 500 GB, 1,5 TB. Nota: 1 GB = 1,000,000,000 bytes1 TB = 1,000,000,000,000 bytes  |
|     / Conjunto de dados:&lt;dataset.csv&gt; | **Necessário**<br/> Um ficheiro CSV que contém uma lista de diretórios e/ou uma lista de ficheiros toobe copiados tootarget unidades.  |
|     /silentmode  | **Opcional**.<br/> Se não for especificado, irá lembrar-se ao hello requisito de unidades e tem o toocontinue de confirmação.  |

## <a name="tool-output"></a>Saída de ferramenta

### <a name="sample-drive-manifest-file"></a>Ficheiro de manifesto de unidade de exemplo

```xml
<?xml version="1.0" encoding="UTF-8"?>
<DriveManifest Version="2011-MM-DD">
   <Drive>
      <DriveId>drive-id</DriveId>
      <StorageAccountKey>storage-account-key</StorageAccountKey>
      <ClientCreator>client-creator</ClientCreator>
      <!-- First Blob List -->
      <BlobList Id="session#1-0">
         <!-- Global properties and metadata that applies tooall blobs -->
         <MetadataPath Hash="md5-hash">global-metadata-file-path</MetadataPath>
         <PropertiesPath Hash="md5-hash">global-properties-file-path</PropertiesPath>
         <!-- First Blob -->
         <Blob>
            <BlobPath>blob-path-relative-to-account</BlobPath>
            <FilePath>file-path-relative-to-transfer-disk</FilePath>
            <ClientData>client-data</ClientData>
            <Length>content-length</Length>
            <ImportDisposition>import-disposition</ImportDisposition>
            <!-- page-range-list-or-block-list -->
            <!-- page-range-list -->
            <PageRangeList>
               <PageRange Offset="1073741824" Length="512" Hash="md5-hash" />
               <PageRange Offset="1073741824" Length="512" Hash="md5-hash" />
            </PageRangeList>
            <!-- block-list -->
            <BlockList>
               <Block Offset="1073741824" Length="4194304" Id="block-id" Hash="md5-hash" />
               <Block Offset="1073741824" Length="4194304" Id="block-id" Hash="md5-hash" />
            </BlockList>
            <MetadataPath Hash="md5-hash">metadata-file-path</MetadataPath>
            <PropertiesPath Hash="md5-hash">properties-file-path</PropertiesPath>
         </Blob>
      </BlobList>
   </Drive>
</DriveManifest>
```

### <a name="sample-journal-file-xml-for-each-drive"></a>Ficheiro de diário de alterações de exemplo (XML) para cada unidade

```xml
[BeginUpdateRecord][2016/11/01 21:22:25.379][Type:ActivityRecord]
ActivityId: DriveInfo
DriveState: [BeginValue]
<?xml version="1.0" encoding="UTF-8"?>
<Drive>
   <DriveId>drive-id</DriveId>
   <BitLockerKey>*******</BitLockerKey>
   <ManifestFile>\DriveManifest.xml</ManifestFile>
   <ManifestHash>D863FE44F861AE0DA4DCEAEEFFCCCE68</ManifestHash> </Drive>
[EndValue]
SaveCommandOutput: Completed
[EndUpdateRecord]
```

### <a name="sample-journal-file-jrn-for-session-that-records-hello-trail-of-sessions"></a>Ficheiro de diário de alterações de exemplo (JRN) para a sessão que regista o registo de Olá de sessões

```
[BeginUpdateRecord][2016/11/02 18:24:14.735][Type:NewJournalFile]
VocabularyVersion: 2013-02-01
[EndUpdateRecord]
[BeginUpdateRecord][2016/11/02 18:24:14.749][Type:ActivityRecord]
ActivityId: PrepImportDriveCommandContext
LogDirectory: F:\logs
[EndUpdateRecord]
[BeginUpdateRecord][2016/11/02 18:24:14.754][Type:ActivityRecord]
ActivityId: PrepImportDriveCommandContext
StorageAccountKey: *******
[EndUpdateRecord]
```

## <a name="faq"></a>FAQ

### <a name="general"></a>Geral

#### <a name="what-is-waimportexport-tool"></a>O que é a ferramenta de WAImportExport?

a ferramenta de WAImportExport Olá está preparação de unidade de Olá e a ferramenta de reparação que pode utilizar com Olá serviço de importação/exportação do Microsoft Azure. Pode utilizar esta ferramenta toocopy dados toohello unidades de disco rígido que vai tooship tooan Datacenter do Azure. Depois de uma tarefa de importação foi concluída, que pode utilizar esta ferramenta toorepair blobs que foram corrompidos, foram em falta ou em conflito com outros blobs. Depois de receber Olá unidades de uma tarefa de exportação foi concluída, pode utilizar esta ferramenta toorepair todos os ficheiros que foram danificados ou em falta no Olá unidades.

#### <a name="how-does-hello-waimportexport-tool-work-on-multiple-source-dir-and-disks"></a>Como does Olá WAImportExport ferramenta funcionam em múltiplos dir de origem e discos?

Se o tamanho dos dados Olá é superior ao tamanho do disco Olá, ferramenta de WAImportExport Olá distribuir os dados de Olá entre discos Olá de uma forma otimizada. podem ser feitos Olá dados copiar toomultiple discos em paralelo ou sequencialmente. Não há nenhum limite do número de Olá dos dados de Olá discos pode ser escrito toosimultaneously. ferramenta de Olá será distribuir dados com base no tamanho do disco e o tamanho da pasta. Irá selecionar disco Olá que é a maioria das otimizadas para o tamanho de objeto Olá. Olá dados quando carregado toohello conta de armazenamento irá ser novamente convergida toohello especificado estrutura de diretórios.

#### <a name="where-can-i-find-previous-version-of-waimportexport-tool"></a>Onde posso encontrar a versão anterior da ferramenta de WAImportExport?

A ferramenta de WAImportExport tem todas as funcionalidades que tinha ferramenta WAImportExport V1. WAImportExport ferramenta permite que os utilizadores toospecify várias origens e escrita toomultiple unidades. Além disso, um pode gerir facilmente várias localizações de origem a partir da qual os dados de Olá necessitam toobe copiado num único ficheiro CSV. No entanto, no caso precisa de SAS suportar ou quiser toocopy único toosingle o disco de origem, que pode [Transferir WAImportExport V1 ferramenta] (http://go.microsoft.com/fwlink/? LinkID = 301900&amp;clcid = 0x409) e consulte demasiado[WAImportExport V1 referência](storage-import-export-tool-how-to-v1.md) para obter ajuda com a utilização de WAImportExport V1.

#### <a name="what-is-a-session-id"></a>O que é um ID de sessão?

ferramenta de Olá espera sessão de cópia de Olá (/ id) toobe parâmetro Olá mesmo se dados de Olá toospread intenção Olá entre vários discos. Manter Olá o mesmo nome da sessão de cópia de Olá irá ativar dados toocopy do utilizador a partir de uma ou várias localizações de origem para um ou vários discos/diretórios de destino. Manter o mesmo id de sessão permite Olá ferramenta toopick cópia Olá de ficheiros a partir de onde se foi deixada Olá última vez.

No entanto, a mesma sessão de cópia não pode ser utilizado tooimport dados toodifferent contas de armazenamento.

Quando o nome da sessão de cópia é mesmo em várias execuções de ferramenta Olá, Olá de logfile (/ logdir) e a chave de conta de armazenamento (/ sk) é também toobe esperado Olá mesmo.

SessionId pode ser composto por letras, 0 ~ understore 9, (\_), travessão (-) ou hash (#), e o seu comprimento deve ser 3 ~ 30.

Por exemplo, 1 de sessão ou sessão #1 ou sessão\_1

#### <a name="what-is-a-journal-file"></a>O que é um ficheiro do diário de alterações?

Sempre que executar Olá WAImportExport ferramenta toocopy ficheiros toohello unidade de disco rígido, a ferramenta de Olá cria uma sessão de cópia. Estado de Olá da sessão de cópia de Olá é escrito toohello ficheiros de diário de alterações. Se uma sessão de cópia é interrompida (por exemplo, devido a falha de energia do sistema de tooa), é possível retomar executar novamente a ferramenta de Olá e especificar os ficheiros do diário de alterações de Olá na linha de comandos Olá.

Para cada unidade de disco rígida preparar com Olá ferramenta de importação/exportação do Azure, ferramenta Olá irá criar um ficheiro único diário de alterações com o nome "&lt;DriveID&gt;. xml" em que a unidade Id é o número de série de Olá associado à unidade de toohello Olá ferramenta lê a partir do disco Olá. Precisa de ficheiros do diário Olá todos os a tarefa de importação do unidades toocreate Olá. ficheiros do diário de alterações de Olá também podem ser utilizado tooresume unidade preparação se ferramenta Olá for interrompida.

#### <a name="what-is-a-log-directory"></a>O que é um diretório de registo?

diretório de registo de Olá Especifica que um diretório toobe utilizada registos verboso toostore, bem como os ficheiros de manifesto temporários. Se não for especificado, será utilizado como o diretório de registo de Olá diretório atual Olá. Olá registos são registos verbosos.

### <a name="prerequisites"></a>Pré-requisitos

#### <a name="what-are-hello-specifications-of-my-disk"></a>Quais são as especificações de Olá do meu disco?

Uma ou mais SATAII 2.5 polegadas ou 3.5 polegadas vazio ou III ou disco rígido de SSD unidades máquina de cópia de toohello ligado.

#### <a name="how-can-i-enable-bitlocker-on-my-machine"></a>Como ativar o BitLocker no meu computador?

Toocheck de forma simples é clicando na unidade do sistema. Irá mostrar opções para o Bitlocker se a capacidade de Olá estiver ativada. Se estiver desligado, não irá vê-lo.

![Verifique o BitLocker](./media/storage-import-export-tool-preparing-hard-drives-import/BitLocker.png)

Eis um artigo no [como tooenable BitLocker](https://technet.microsoft.com/library/cc766295.aspx)

É possível que a máquina não tem TPM chip. Se não obtiver uma saída utilizando tpm.msc, observe FAQ seguinte Olá.

#### <a name="how-toodisable-trusted-platform-module-tpm-in-bitlocker"></a>Como toodisable fidedigna Platform Module (TPM) no BitLocker?
> [!NOTE]
> Apenas se não existir nenhum TPM nos respetivos servidores, terá de política TPM toodisable. Não é necessário toodisable TPM se houver um TPM fidedigno no servidor do utilizador. 
> 

Na ordem toodisable TPM no BitLocker, percorrer Olá os seguintes passos:<br/>
1. Iniciar **Editor de políticas de grupo** escrevendo gpedit.msc numa linha de comandos. Se **Editor de políticas de grupo** aparece toobe disponível, para ativar o BitLocker primeiro. Consulte as FAQ anterior.
2. Abra **política de computador Local &gt; configuração do computador &gt; modelos administrativos &gt; componentes do Windows&gt; encriptação de unidade BitLocker &gt; deunidadesdesistemaoperativo**.
3. Editar **requer autenticação adicional durante o arranque** política.
4. Definir a política de Olá demasiado**ativado** e certifique-se **permitir BitLocker sem um TPM compatível** está marcada.

####  <a name="how-toocheck-if-net-4-or-higher-version-is-installed-on-my-machine"></a>Como toocheck se .NET 4 ou versão posterior está instalada no meu computador?

Todas as versões do Microsoft .NET Framework estão instaladas no seguinte diretório: %windir%\Microsoft.NET\Framework\

Navegue toohello acima mencionado parte no seu computador de destino onde a ferramenta de Olá tem toorun. Procure o nome da pasta começados por "v4". Ausência de um diretório tal significa que .NET 4 não está instalado no seu computador. Pode transferir o .net 4 na sua máquina utilizando [o Microsoft .NET Framework 4 (programa de instalação Web)](https://www.microsoft.com/download/details.aspx?id=17851).

### <a name="limits"></a>Limites

#### <a name="how-many-drives-can-i-preparesend-at-hello-same-time"></a>O número de unidades pode posso preparar/envio em Olá mesmo tempo?

Não há nenhum limite do número de Olá de discos que Olá ferramenta pode preparar. No entanto, a ferramenta de Olá espera letras de unidade como entradas. Que limita-too25 preparação de disco em simultâneo. Uma única tarefa pode processar o máximo de 10 discos cada vez. Se a preparar-se mais de 10 discos filtragem Olá a mesma conta de armazenamento, discos Olá podem ser distribuídos por várias tarefas.

#### <a name="can-i-target-more-than-one-storage-account"></a>Pode visar mais do que uma conta de armazenamento?

Apenas uma conta de armazenamento pode ser submetida por tarefa e na sessão de cópia única.

### <a name="capabilities"></a>Capacidades

#### <a name="does-waimportexportexe-encrypt-my-data"></a>WAImportExport.exe encriptar os meus dados?

Sim. A encriptação BitLocker está ativada e necessárias para este processo.

#### <a name="what-will-be-hello-hierarchy-of-my-data-when-it-appears-in-hello-storage-account"></a>O que será hierarquia Olá dos meus dados quando é apresentado na conta do storage Olá?

Apesar de dados são distribuídos entre discos, Olá dados quando carregado conta de armazenamento toohello irá ser convergida fazer uma cópia de estrutura de diretórios toohello especificada no ficheiro CSV Olá conjunto de dados.

#### <a name="how-many-of-hello-input-disks-will-have-active-io-in-parallel-when-copy-is-in-progress"></a>Quantidade de Olá entrada discos terão Active Directory e/s em paralelo, quando copiar está em curso?

ferramenta de Olá distribui dados pelos discos de entrada Olá com base no tamanho Olá Olá de ficheiros de entrada. Dito isto, número de Olá de Active Directory discos em paralelo delends completamente na natureza Olá Olá de dados de entrada. Consoante o tamanho dos ficheiros individuais no conjunto de dados de entrada Olá Olá, um ou mais discos podem mostrar o Active Directory e/s em paralelo. Consulte a questão seguinte para obter mais detalhes.

#### <a name="how-does-hello-tool-distribute-hello-files-across-hello-disks"></a>Como ferramenta Olá distribuir os ficheiros de Olá entre discos Olá?

Ferramenta WAImportExport lê e escreve os ficheiros batch por lote, um batch contém o número máximo de 100000 ficheiros. Isto significa que os 100000 ficheiros máx. podem ser escritos paralelo. Vários discos são escritos toosimultaneously se estes 100000 ficheiros são distribuídas toomulti unidades. No entanto se ferramenta Olá escreve toomultiple discos em simultâneo ou um único disco depende do tamanho cumulativo de Olá do batch Olá. Por exemplo, em caso de ficheiros mais pequenos, se todos os ficheiros 10,0000 são capaz toofit numa única unidade, ferramenta irá escrever tooonly um disco durante o processamento Olá este lote.

### <a name="waimportexport-output"></a>Saída de WAImportExport

#### <a name="there-are-two-journal-files-which-one-should-i-upload-tooazure-portal"></a>Existem dois ficheiros do diário de alterações, que deve posso carregar tooAzure portal?

**. XML** -para cada unidade de disco rígida deve preparar-se com a ferramenta de WAImportExport Olá, ferramenta Olá irá criar um ficheiro único diário de alterações com o nome `<DriveID>.xml` onde DriveID é o número de série de Olá associado à unidade de toohello Olá ferramenta lê a partir do disco Olá. Precisa de ficheiros do diário Olá todos os a tarefa de importação de Olá toocreate unidades no Olá portal do Azure. Este ficheiro de diário também pode ser utilizado tooresume unidade preparação se ferramenta Olá for interrompida.

**.jrn** -ficheiro de diário de alterações de Olá com sufixo `.jrn` contém o estado de Olá todas as sessões de cópia para uma unidade de disco rígida. Também contém informações de Olá necessário toocreate Olá importar tarefa. Sempre tem de especificar um ficheiro do diário de alterações ao ID de ferramenta de WAImportExport Olá em execução, bem como uma sessão de cópia.

## <a name="next-steps"></a>Passos seguintes

* [Configurar a definição Olá ferramenta de importação/exportação do Azure](storage-import-export-tool-setup.md)
* [Processo de importar metadados durante Olá e propriedades da definição](storage-import-export-tool-setting-properties-metadata-import.md)
* [Discos rígidos do tooprepare de fluxo de trabalho de exemplo para uma tarefa de importação](storage-import-export-tool-sample-preparing-hard-drives-import-job-workflow.md)
* [Referência rápida para comandos utilizados com frequência](storage-import-export-tool-quick-reference.md) 
* [Revisão do estado da tarefa com ficheiros de registo de cópia](storage-import-export-tool-reviewing-job-status-v1.md)
* [Reparação de uma tarefa de importação](storage-import-export-tool-repairing-an-import-job-v1.md)
* [Reparação de uma tarefa de exportação](storage-import-export-tool-repairing-an-export-job-v1.md)
* [Resolução de problemas Olá ferramenta de importação/exportação do Azure](storage-import-export-tool-troubleshooting-v1.md)
