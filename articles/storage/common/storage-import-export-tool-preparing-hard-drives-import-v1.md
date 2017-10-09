---
title: "unidades de disco rígido aaaPreparing para um Azure para importar/exportar importar tarefa - v1 | Microsoft Docs"
description: "Saiba como unidades de disco rígido tooprepare utilizando Olá WAImportExport v1 ferramenta toocreate uma tarefa de importação para o serviço de importação/exportação do Azure Olá."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 3d818245-8b1b-4435-a41f-8e5ec1f194b2
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/15/2017
ms.author: muralikk
ms.openlocfilehash: 1eb0c3c51e984e2869b5268254f468d4b43e9d85
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="preparing-hard-drives-for-an-import-job"></a>Preparar as unidades de disco rígido para uma tarefa de importação
tooprepare um ou mais unidades de disco rígido para uma tarefa de importação, siga estes passos:

-   Identificar Olá dados tooimport para Olá serviço Blob

-   Identificar os diretórios virtuais do destino e os blobs no Olá serviço Blob

-   Determinar quantos unidades, terá de

-   Copiar dados de Olá tooeach das suas unidades de disco rígidas

 Para um fluxo de trabalho de exemplo, consulte [tooPrepare de fluxo de trabalho de exemplo, discos rígidos de uma tarefa de importação](storage-import-export-tool-sample-preparing-hard-drives-import-job-workflow-v1.md).

## <a name="identify-hello-data-toobe-imported"></a>Identificar Olá dados toobe importado
 Olá primeiro passo toocreating uma tarefa de importação é toodetermine os diretórios e ficheiros vão tooimport. Isto pode ser uma lista de diretórios, uma lista dos ficheiros exclusivos ou uma combinação desses dois. Quando um diretório estiver incluído, todos os ficheiros no diretório de Olá e nos seus subdiretórios irão fazer parte da tarefa de importação de Olá.

> [!NOTE]
>  Uma vez que subdiretórios recursivamente incluída quando um diretório principal está incluído, especifique apenas o diretório principal Olá. Não também especificar qualquer um dos seus subdiretórios.
>
>  Atualmente, Olá ferramenta de importação/exportação do Microsoft Azure tem Olá seguir limitação: se um diretório contém mais dados do que pode conter um disco rígido, em seguida, Olá directory precisar de toobe dividido em diretórios mais pequenos. Por exemplo, se um diretório contém 2,5 TB de dados e Olá a capacidade de disco rígido é apenas 2TB, em seguida, terá de diretório do toobreak Olá 2,5 TB para diretórios mais pequenos. Esta limitação será resolvida numa versão posterior da ferramenta de Olá.

## <a name="identify-hello-destination-locations-in-hello-blob-service"></a>Identificar as localizações de destino Olá no serviço de blob Olá
 Para cada diretório ou o ficheiro que será importado, terá de tooidentify um diretório virtual de destino ou um blob no Olá serviço Blob do Azure. Irá utilizar nestes destinos como entradas toohello ferramenta de importação/exportação do Azure. Tenha em atenção que os diretórios devem ser delimitados com caráter de barra Olá "/".

 Olá, a tabela seguinte mostra alguns exemplos de destinos de blob:

|Ficheiro de origem ou diretório|Blob de destino ou diretório virtual|
|------------------------------|-------------------------------------------|
|H:\Video|https://mystorageaccount.blob.Core.Windows.NET/Video|
|H:\Photo|https://mystorageaccount.blob.Core.Windows.NET/Photo|
|K:\Temp\FavoriteVideo.ISO|https://mystorageaccount.blob.Core.Windows.NET/Favorite/FavoriteVideo.ISO|
|\\\myshare\john\music|https://mystorageaccount.blob.Core.Windows.NET/Music|

## <a name="determine-how-many-drives-are-needed"></a>Determinar quantos unidades são necessárias
 Em seguida, terá de toodetermine:

-   número de Olá de unidades de disco rígido necessário dados de Olá toostore.

-   diretórios de Olá e/ou os ficheiros de autónomo que serão copiado tooeach da sua unidade de disco rígida.

 Certifique-se de que tem o número de Olá de unidades de disco rígido, terá de dados de Olá toostore que estiver a transferir.

## <a name="copy-data-tooyour-hard-drive"></a>Copiar a unidade de disco rígido de tooyour de dados
 Esta secção descreve como toocall Olá toocopy da ferramenta de importação/exportação do Azure a tooone de dados ou mais unidades de disco rígido. Sempre que chamar Olá ferramenta de importação/exportação do Azure, criar um novo *copiar sessão*. Criar a sessão de cópia, pelo menos, um para cada unidade toowhich copiar dados; em alguns casos, poderá ser necessário mais do que um toocopy de sessão de cópia todos da sua unidade de toosingle de dados. Seguem-se algumas razões que poderá ter várias sessões de cópia:

-   Tem de criar uma sessão de cópia separada para cada unidade que copiar para.

-   Uma sessão de cópia pode copiar um único diretório ou unidade de toohello um blob único. Se estiver a copiar vários diretórios, vários blobs ou uma combinação de ambos, terá de toocreate várias sessões de cópia.

-   Pode especificar propriedades e os metadados que serão definidos em blobs Olá importados como parte de uma tarefa de importação. Propriedades de Olá ou metadados que especificou para uma sessão de cópia irão aplicar blobs tooall especificados nessa sessão de cópia. Se pretender que propriedades diferentes toospecify ou metadados para alguns blobs, terá de toocreate um separado copiar sessão. Consulte [propriedades de definição e de metadados durante o processo de importação de Olá](storage-import-export-tool-setting-properties-metadata-import-v1.md)para obter mais informações.

> [!NOTE]
>  Se tiver várias máquinas que cumprem os requisitos de Olá descritos na [Olá definição cópias de segurança do Azure para importar/exportar ferramenta](storage-import-export-tool-setup-v1.md), pode copiar os discos rígidos toomultiple dados em paralelo ao executar uma instância desta ferramenta em cada máquina.

 Para cada unidade de disco rígida preparar com Olá ferramenta de importação/exportação do Azure, ferramenta Olá irá criar um ficheiro único diário de alterações. Precisa de ficheiros do diário Olá todos os a tarefa de importação do unidades toocreate Olá. ficheiros do diário de alterações de Olá também podem ser utilizado tooresume unidade preparação se ferramenta Olá for interrompida.

### <a name="azure-importexport-tool-syntax-for-an-import-job"></a>Sintaxe da ferramenta de importação/exportação do Azure para uma tarefa de importação
 unidades de tooprepare para uma tarefa de importação, chamar Olá ferramenta de importação/exportação do Azure com Olá **PrepImport** comando. Os parâmetros que incluir depende se isto é Olá primeira cópia sessão ou uma sessão de cópia subsequentes.

 Olá primeira sessão de cópia para uma unidade requer alguns parâmetros adicionais toospecify Olá conta de armazenamento chave; letra de unidade de destino Olá; Indica se deve ser formatada unidade Olá; Se a unidade de Olá tem de estar encriptada e se assim for, Olá chave do BitLocker; e o diretório de registo Olá. Segue-se a sintaxe de Olá para um toocopy de sessão de cópia inicial um diretório ou um único ficheiro:

 **Primeiro de copiar toocopy de sessão único diretório**

 `WAImportExport PrepImport /sk:<StorageAccountKey> /csas:<ContainerSas> /t: <TargetDriveLetter> [/format] [/silentmode] [/encrypt] [/bk:<BitLockerKey>] [/logdir:<LogDirectory>] /j:<JournalFile> /id:<SessionId> /srcdir:<SourceDirectory> /dstdir:<DestinationBlobVirtualDirectory> [/Disposition:<Disposition>] [/BlobType:<BlockBlob|PageBlob>] [/PropertyFile:<PropertyFile>] [/MetadataFile:<MetadataFile>]`

 **Primeiro de copiar toocopy de sessão único ficheiro**

 `WAImportExport PrepImport /sk:<StorageAccountKey> /csas:<ContainerSas> /t: <TargetDriveLetter> [/format] [/silentmode] [/encrypt] [/bk:<BitLockerKey>] [/logdir:<LogDirectory>] /j:<JournalFile> /id:<SessionId> /srcfile:<SourceFile> /dstblob:<DestinationBlobPath> [/Disposition:<Disposition>] [/BlobType:<BlockBlob|PageBlob>] [/PropertyFile:<PropertyFile>] [/MetadataFile:<MetadataFile>]`

 Nas sessões subsequentes cópia, não terá de parâmetros do toospecify Olá iniciais. Segue-se a sintaxe de Olá para um toocopy de sessão subsequentes cópia um diretório ou um único ficheiro:

 **Cópia subsequentes sessões toocopy único diretório**

 `WAImportExport PrepImport /j:<JournalFile> /id:<SessionId> /srcdir:<SourceDirectory> /dstdir:<DestinationBlobVirtualDirectory> [/Disposition:<Disposition>] [/BlobType:<BlockBlob|PageBlob>] [/PropertyFile:<PropertyFile>] [/MetadataFile:<MetadataFile>]`

 **Toocopy de sessões subsequentes copiar um ficheiro único**

 `WAImportExport PrepImport /j:<JournalFile> /id:<SessionId> /srcfile:<SourceFile> /dstblob:<DestinationBlobPath> [/Disposition:<Disposition>] [/BlobType:<BlockBlob|PageBlob>] [/PropertyFile:<PropertyFile>] [/MetadataFile:<MetadataFile>]`

### <a name="parameters-for-hello-first-copy-session-for-a-hard-drive"></a>Parâmetros para Olá primeiro de copiar sessão para uma unidade de disco rígido
 Sempre que executar ficheiros do Olá ferramenta de importação/exportação do Azure toocopy toohello de disco rígido, a ferramenta de Olá cria uma sessão de cópia. Cada sessão de cópia copia um único diretório ou unidade de disco rígido de tooa um único ficheiro. Estado de Olá da sessão de cópia de Olá é escrito toohello ficheiros de diário de alterações. Se uma sessão de cópia é interrompida (por exemplo, devido a falha de energia do sistema de tooa), é possível retomar executar novamente a ferramenta de Olá e especificar os ficheiros do diário de alterações de Olá na linha de comandos Olá.

> [!WARNING]
>  Se especificar Olá **/Formatar** parâmetro Olá primeira sessão de cópia, unidade de Olá será formatada e todos os dados na unidade de Olá serão eliminados. Recomenda-se a utilização de pens em branco apenas para a sua sessão de cópia.

 comando de Olá utilizado para Olá primeira sessão de cópia para cada unidade requer diferentes parâmetros que comandos Olá para sessões de cópia subsequentes. Olá tabela seguinte lista Olá parâmetros adicionais que estão disponíveis para Olá primeira sessão de cópia:

|Parâmetro da linha de comandos|Descrição|
|-----------------------------|-----------------|
|**/SK:**< StorageAccountKey\>|`Optional.`chave de conta do storage Olá para Olá armazenamento toowhich Olá os dados da conta será importado. Tem de incluir um **/sk:**< StorageAccountKey\> ou **/csas:**< ContainerSas\> no comando Olá.|
|**/csas:**< ContainerSas\>|`Optional`. contentor de Olá conta de armazenamento do SAS toouse tooimport dados toohello. Tem de incluir um **/sk:**< StorageAccountKey\> ou **/csas:**< ContainerSas\> no comando Olá.<br /><br /> valor de Olá para este parâmetro tem de começar com o nome do contentor Olá, seguido de um ponto de interrogação (?) e o token SAS de Olá. Por exemplo:<br /><br /> `mycontainer?sv=2014-02-14&sr=c&si=abcde&sig=LiqEmV%2Fs1LF4loC%2FJs9ZM91%2FkqfqHKhnz0JM6bqIqN0%3D&se=2014-11-20T23%3A54%3A14Z&sp=rwdl`<br /><br /> permissões de Olá, se especificado no URL Olá ou numa política de acesso armazenada, tem de incluir leitura, escrita e eliminação para tarefas de importação e leitura, escrita e lista para as tarefas de exportação.<br /><br /> Quando este parâmetro for especificado, todos os blobs toobe, importado ou exportado tem de estar dentro do contentor de Olá especificado na assinatura de acesso partilhado Olá.|
|**/t:**< TargetDriveLetter\>|`Required.`letra de unidade de Olá da unidade de disco rígido de destino de Olá Olá cópia sessão atual, sem Olá à direita dois pontos.|
|**/Format**|`Optional.`Especificar este parâmetro quando precisa de unidade de Olá toobe formatado; caso contrário, omita-lo. Antes de ferramenta Olá formatos unidade Olá, irá solicitar uma confirmação da consola. toosuppress Olá confirmação, especifique o parâmetro de /silentmode Olá.|
|**/silentmode**|`Optional.`Especifique esta confirmação de Olá toosuppress de parâmetro para a unidade de targert Olá de formatação.|
|**/ encriptar**|`Optional.`Especificar este parâmetro quando unidade Olá ainda não foi encriptada com BitLocker e as suas necessidades toobe encriptado pela ferramenta de Olá. Se a unidade de Olá já foi encriptada com BitLocker, em seguida, omita este parâmetro e especifique Olá `/bk` parâmetro, fornecendo a chave do BitLocker existente Olá.<br /><br /> Se especificar Olá `/format` parâmetro, então, também tem de especificar Olá `/encrypt` parâmetro.|
|**/BK:**< BitLockerKey\>|`Optional.`Se `/encrypt` é especificado, omita este parâmetro. Se `/encrypt` for omitido, é necessário toohave já encriptou unidade Olá com o BitLocker. Utilize este parâmetro toospecify Olá BitLocker chave. A encriptação BitLocker é necessária para todos os discos rígidos para tarefas de importação.|
|**/LOGDIR:**< LogDirectory\>|`Optional.`diretório de registo de Olá Especifica que um diretório toobe utilizada registos verboso toostore, bem como os ficheiros de manifesto temporários. Se não for especificado, será utilizado como o diretório de registo de Olá diretório atual Olá.|

### <a name="parameters-required-for-all-copy-sessions"></a>Parâmetros necessários para todas as sessões de cópia
 ficheiros do diário de alterações de Olá contém Estado Olá todas as sessões de cópia para uma unidade de disco rígida. Também contém informações de Olá necessário toocreate Olá importar tarefa. Tem de especificar sempre um ficheiro de diário quando em execução Olá ferramenta de importação/exportação do Azure, bem como um ID de sessão de cópia:

|||
|-|-|
|Parâmetro de linha de comandos|Descrição|
|**/j:**< JournalFile\>|`Required.`Olá caminho toohello diário de alterações o ficheiro. Cada unidade tem de ter exatamente um ficheiro de diário de alterações. Tenha em atenção que o ficheiro diário Olá não têm de residir na unidade de destino Olá. extensão de ficheiro do diário de alterações de Olá é `.jrn`.|
|**formado:**< SessionId\>|`Required.`ID de sessão de Olá identifica uma sessão de cópia. É utilizado tooensure recuperação exata de uma sessão de cópia interrompida. Os ficheiros que são copiados numa sessão de cópia são armazenados num diretório com o nome após o ID de sessão de Olá na unidade de destino Olá.|

### <a name="parameters-for-copying-a-single-directory"></a>Parâmetros para copiar um único diretório
 Quando copiar um único diretório, a seguir Olá necessário e parâmetros opcionais aplicam-se:

|Parâmetro de linha de comandos|Descrição|
|----------------------------|-----------------|
|**/srcdir:**< SourceDirectory\>|`Required.`diretório de origem Olá que contém ficheiros toobe copiados toohello unidade de destino. caminho do diretório Olá tem de ser um caminho absoluto (não um caminho relativo).|
|**/dstdir:**< DestinationBlobVirtualDirectory\>|`Required.`Olá caminho toohello destino diretório virtual na sua conta de armazenamento do Windows Azure. diretório virtual Olá pode ou não pode já existir.<br /><br /> Pode especificar um contentor ou como um prefixo de blob `music/70s/`. Olá diretório de destino tem de começar com o nome do contentor Olá, seguido por uma barra "/" e, opcionalmente, pode incluir um diretório virtual blob que termina com "/".<br /><br /> Quando o contentor de destino Olá recipiente-raiz Olá, tem de especificar explicitamente recipiente-raiz Olá, incluindo a barra de Olá, como `$root/`. Uma vez que não podem incluir os blobs no contentor de raiz de Olá "/" nos respetivos nomes, não serão copiados todos os subdiretórios no diretório de origem Olá ao diretório de destino Olá é recipiente-raiz Olá.<br /><br /> Ser toouse se os nomes dos contentores válidos quando especificar diretórios virtuais de destino ou blobs. Tenha em atenção que os nomes dos contentores têm de estar em minúsculas. Para regras de nomenclatura de contentor, consulte [nomenclatura e referência de contentores, Blobs e metadados](/rest/api/storageservices/naming-and-referencing-containers--blobs--and-metadata).|
|**/ Disposição:**< mudar o nome de &#124; substituir o não &#124; substituir >|`Optional.`Especifica o comportamento de Olá quando um blob com Olá especificado o endereço já existe. Os valores válidos para este parâmetro são: `rename`, `no-overwrite` e `overwrite`. Tenha em atenção que estes valores são maiúsculas e minúsculas. Se for especificado nenhum valor, a predefinição de Olá é `rename`.<br /><br /> Olá o valor especificado para este parâmetro afeta todos os ficheiros de Olá no diretório de Olá especificado pelo Olá `/srcdir` parâmetro.|
|**/ BlobType:**< BlockBlob &#124; PageBlob >|`Optional.`Especifica o tipo de blob Olá para blobs de destino Olá. Os valores válidos são: `BlockBlob` e `PageBlob`. Tenha em atenção que estes valores são maiúsculas e minúsculas. Se for especificado nenhum valor, a predefinição de Olá é `BlockBlob`.<br /><br /> Na maioria dos casos, `BlockBlob` é recomendada. Se especificar `PageBlob`, comprimento de Olá de cada ficheiro no diretório de Olá tem de ser um múltiplo de 512, Olá tamanho de uma página para blobs de páginas.|
|**/ PropertyFile:**< PropertyFile\>|`Optional.`Ficheiro de propriedade de toohello de caminho para os blobs de destino Olá. Consulte [metadados e o formato de ficheiro de propriedades de serviço de importação/exportação](../storage-import-export-file-format-metadata-and-properties.md) para obter mais informações.|
|**/ MetadataFile:**< MetadataFile\>|`Optional.`Ficheiro de metadados de toohello de caminho para os blobs de destino Olá. Consulte [metadados e o formato de ficheiro de propriedades de serviço de importação/exportação](../storage-import-export-file-format-metadata-and-properties.md) para obter mais informações.|

### <a name="parameters-for-copying-a-single-file"></a>Parâmetros para copiar um ficheiro único
 Quando copiar um ficheiro único, hello parâmetros obrigatórios e opcionais seguintes aplicam-se:

|Parâmetro de linha de comandos|Descrição|
|----------------------------|-----------------|
|**/srcfile:**< SourceFile\>|`Required.`caminho completo de Olá toohello ficheiro toobe copiado. caminho do diretório Olá tem de ser um caminho absoluto (não um caminho relativo).|
|**/dstblob:**< DestinationBlobPath\>|`Required.`Olá caminho toohello blob de destino na sua conta de armazenamento do Windows Azure. blob Olá pode ou não pode já existir.<br /><br /> Especifique Olá blob nome que começa com o nome do contentor Olá. nome do blob Olá não pode começar com "/" ou o nome de conta do storage Olá. Para regras de nomenclatura de BLOBs, consulte [nomenclatura e referência de contentores, Blobs e metadados](/rest/api/storageservices/naming-and-referencing-containers--blobs--and-metadata).<br /><br /> Quando o contentor de destino Olá recipiente-raiz Olá, explicitamente tem de especificar `$root` como Olá contentor, tais como `$root/sample.txt`. Tenha em atenção que os blobs no contentor de raiz de Olá não pode incluir "/" nos respetivos nomes.|
|**/ Disposição:**< mudar o nome de &#124; substituir o não &#124; substituir >|`Optional.`Especifica o comportamento de Olá quando um blob com Olá especificado o endereço já existe. Os valores válidos para este parâmetro são: `rename`, `no-overwrite` e `overwrite`. Tenha em atenção que estes valores são maiúsculas e minúsculas. Se for especificado nenhum valor, a predefinição de Olá é `rename`.|
|**/ BlobType:**< BlockBlob &#124; PageBlob >|`Optional.`Especifica o tipo de blob Olá para blobs de destino Olá. Os valores válidos são: `BlockBlob` e `PageBlob`. Tenha em atenção que estes valores são maiúsculas e minúsculas. Se for especificado nenhum valor, a predefinição de Olá é `BlockBlob`.<br /><br /> Na maioria dos casos, `BlockBlob` é recomendada. Se especificar `PageBlob`, comprimento de Olá de cada ficheiro no diretório de Olá tem de ser um múltiplo de 512, Olá tamanho de uma página para blobs de páginas.|
|**/ PropertyFile:**< PropertyFile\>|`Optional.`Ficheiro de propriedade de toohello de caminho para os blobs de destino Olá. Consulte [metadados e o formato de ficheiro de propriedades de serviço de importação/exportação](../storage-import-export-file-format-metadata-and-properties.md) para obter mais informações.|
|**/ MetadataFile:**< MetadataFile\>|`Optional.`Ficheiro de metadados de toohello de caminho para os blobs de destino Olá. Consulte [metadados e o formato de ficheiro de propriedades de serviço de importação/exportação](../storage-import-export-file-format-metadata-and-properties.md) para obter mais informações.|

### <a name="resuming-an-interrupted-copy-session"></a>A retomar a uma sessão de cópia interrompida
 Se uma sessão de cópia é interrompida por qualquer motivo, pode retomá-lo ao executar a ferramenta de Olá com apenas o ficheiro de diário Olá especificado:

```
WAImportExport.exe PrepImport /j:<JournalFile> /id:<SessionId> /ResumeSession
```

 Apenas Olá mais recente cópia sessão, se terminou anormalmente, pode ser retomada.

> [!IMPORTANT]
>  Quando retomar uma sessão de cópia, não modificar diretórios e ficheiros de dados de origem Olá adicionando ou removendo ficheiros.

### <a name="aborting-an-interrupted-copy-session"></a>Abortar uma sessão de cópia interrompida
 Se uma sessão de cópia é interrompida e não é possível tooresume (por exemplo, se um diretório de origem foi tentativa inacessível), tem abortar Olá sessão atual para que este pode ser revertida back e novas sessões de cópia podem ser iniciadas:

```
WAImportExport.exe PrepImport /j:<JournalFile> /id:<SessionId> /AbortSession
```

 Apenas Olá última de cópia de sessão, se terminou anormalmente, pode ser abortada. Tenha em atenção que não é possível a abortar Olá primeira sessão de cópia para uma unidade. Em vez disso, tem de reiniciar sessão de cópia de Olá com um novo ficheiro de diário de alterações.

## <a name="next-steps"></a>Passos seguintes

* [Configurar a definição Olá ferramenta de importação/exportação do Azure](storage-import-export-tool-setup-v1.md)
* [Processo de importar metadados durante Olá e propriedades da definição](storage-import-export-tool-setting-properties-metadata-import-v1.md)
* [Discos rígidos do tooprepare de fluxo de trabalho de exemplo para uma tarefa de importação](storage-import-export-tool-sample-preparing-hard-drives-import-job-workflow-v1.md)
* [Referência rápida para comandos utilizados com frequência](storage-import-export-tool-quick-reference-v1.md) 
* [Revisão do estado da tarefa com ficheiros de registo de cópia](storage-import-export-tool-reviewing-job-status-v1.md)
* [Reparação de uma tarefa de importação](storage-import-export-tool-repairing-an-import-job-v1.md)
* [Reparação de uma tarefa de exportação](storage-import-export-tool-repairing-an-export-job-v1.md)
* [Resolução de problemas Olá ferramenta de importação/exportação do Azure](storage-import-export-tool-troubleshooting-v1.md)
