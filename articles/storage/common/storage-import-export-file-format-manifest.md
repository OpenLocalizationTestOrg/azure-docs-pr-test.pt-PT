---
title: "formato de ficheiro de manifesto de importação/exportação aaaAzure | Microsoft Docs"
description: "Saiba mais sobre o formato de Olá do ficheiro de manifesto de unidade de Olá que descreve o mapeamento de Olá entre os blobs no armazenamento de Blobs do Azure e os ficheiros numa unidade de uma tarefa de importação ou exportação no serviço de importação/exportação Olá."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: f3119e1c-2c25-48ad-8752-a6ed4adadbb0
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: d7e5e1990482916f7ff5f891c97343b52e82b2f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-importexport-service-manifest-file-format"></a>Formato de ficheiro de manifesto de serviço de importação/exportação do Azure
ficheiro de manifesto de unidade de Olá descreve o mapeamento de Olá entre os blobs no armazenamento de Blobs do Azure e os ficheiros numa unidade que inclui uma tarefa de importação ou exportação. Para uma operação de importação, o ficheiro de manifesto Olá é criado como parte do processo de preparação de unidade de Olá e é armazenado na unidade de Olá antes do envio de unidade de Olá toohello Datacenter do Azure. Durante uma operação de exportação, o manifesto de Olá é criado e armazenado numa unidade de Olá por Olá serviço importar/exportar do Azure.  
  
Para ambos importar e exportar tarefas, o ficheiro de manifesto do Olá unidade é armazenado no Olá importar ou exportar unidade; Não é transmitido toohello serviço através de todas as operações de API.  
  
seguinte Olá descreve formato geral de Olá de um ficheiro de manifesto de unidade:  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<DriveManifest Version="2014-11-01">  
  <Drive>  
    <DriveId>drive-id</DriveId>  
    import-export-credential  
  
    <!-- First Blob List -->  
    <BlobList>  
      <!-- Global properties and metadata that applies tooall blobs -->  
      [<MetadataPath Hash="md5-hash">global-metadata-file-path</MetadataPath>]  
      [<PropertiesPath   
        Hash="md5-hash">global-properties-file-path</PropertiesPath>]  
  
      <!-- First Blob -->  
      <Blob>  
        <BlobPath>blob-path-relative-to-account</BlobPath>  
        <FilePath>file-path-relative-to-transfer-disk</FilePath>  
        [<ClientData>client-data</ClientData>]  
        [<Snapshot>snapshot</Snapshot>]  
        <Length>content-length</Length>  
        [<ImportDisposition>import-disposition</ImportDisposition>]  
        page-range-list-or-block-list          
        [<MetadataPath Hash="md5-hash">metadata-file-path</MetadataPath>]  
        [<PropertiesPath Hash="md5-hash">properties-file-path</PropertiesPath>]  
      </Blob>  
  
      <!-- Second Blob -->  
      <Blob>  
      . . .  
      </Blob>  
    </BlobList>  
  
    <!-- Second Blob List -->  
    <BlobList>  
    . . .  
    </BlobList>  
  </Drive>  
</DriveManifest>  
  
import-export-credential ::=   
  <StorageAccountKey>storage-account-key</StorageAccountKey> | <ContainerSas>container-sas</ContainerSas>  
  
page-range-list-or-block-list ::=   
  page-range-list | block-list  
  
page-range-list ::=   
    <PageRangeList>  
      [<PageRange Offset="page-range-offset" Length="page-range-length"   
       Hash="md5-hash"/>]  
      [<PageRange Offset="page-range-offset" Length="page-range-length"   
       Hash="md5-hash"/>]  
    </PageRangeList>  
  
block-list ::=  
    <BlockList>  
      [<Block Offset="block-offset" Length="block-length" [Id="block-id"]  
       Hash="md5-hash"/>]  
      [<Block Offset="block-offset" Length="block-length" [Id="block-id"]   
       Hash="md5-hash"/>]  
    </BlockList>  

```

## <a name="manifest-xml-elements-and-attributes"></a>Atributos e elementos XML manifesto

elementos de dados de Olá e atributos Olá unidade manifesto XML no formato estão especificados na Olá a tabela seguinte.  
  
|Elemento XML|Tipo|Descrição|  
|-----------------|----------|-----------------|  
|`DriveManifest`|Elemento raiz|elemento de raiz de Olá do ficheiro de manifesto Olá. Todos os outros elementos no ficheiro de Olá são sob este elemento.|  
|`Version`|Atributo, cadeia|versão de Olá do ficheiro de manifesto Olá.|  
|`Drive`|Aninhada elemento XML|Contém o manifesto de Olá para cada unidade.|  
|`DriveId`|Cadeia|Olá Identificador exclusivo de unidade para a unidade de Olá. Identificador de unidade de Olá encontra-se ao consultar a unidade de Olá para o número de série. número de série de unidade de Olá está normalmente impresso no Olá fora da unidade de Olá bem. Olá `DriveID` elemento tem de aparecer antes de qualquer `BlobList` elemento no ficheiro de manifesto Olá.|  
|`StorageAccountKey`|Cadeia|É necessário para importar tarefas se apenas se `ContainerSas` não está especificado. chave da conta Olá para Olá conta do storage do Azure associada à tarefa Olá.<br /><br /> Este elemento é omitido do manifesto de Olá para uma operação de exportação.|  
|`ContainerSas`|Cadeia|É necessário para importar tarefas se apenas se `StorageAccountKey` não está especificado. Olá contentor SAS para aceder a blobs Olá associados à tarefa Olá. Consulte [colocar tarefa](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) para o seu formato. Este elemento é omitido do manifesto de Olá para uma operação de exportação.|  
|`ClientCreator`|Cadeia|Especifica o cliente de Olá que tiver criado o ficheiro XML de Olá. Este valor não é interpretado pelo Olá serviço de importação/exportação.|  
|`BlobList`|Aninhada elemento XML|Contém uma lista de blobs que fazem parte da importação de Olá ou tarefa de exportação. Cada blob numa lista de blob partilhas Olá mesmo metadados e as propriedades.|  
|`BlobList/MetadataPath`|Cadeia|Opcional. Especifica o caminho relativo de Olá de um ficheiro no disco Olá que contém os metadados da predefinição de Olá serão definidos nos blobs na lista de blob Olá para uma operação de importação. Estes metadados podem ser substituído, opcionalmente, de forma blob por BLOBs.<br /><br /> Este elemento é omitido do manifesto de Olá para uma operação de exportação.|  
|`BlobList/MetadataPath/@Hash`|Atributo, cadeia|Especifica o valor de hash MD5 codificado Base16 Olá para o ficheiro de metadados de Olá.|  
|`BlobList/PropertiesPath`|Cadeia|Opcional. Especifica o caminho relativo de Olá de um ficheiro no disco Olá que contém Olá predefinir as propriedades que serão definidas em blobs na lista de blob Olá para uma operação de importação. Estas propriedades podem ser substituídas, opcionalmente, de forma blob por BLOBs.<br /><br /> Este elemento é omitido do manifesto de Olá para uma operação de exportação.|  
|`BlobList/PropertiesPath/@Hash`|Atributo, cadeia|Especifica o valor de hash MD5 codificado Base16 Olá para o ficheiro de propriedades de Olá.|  
|`Blob`|Aninhada elemento XML|Contém informações sobre cada blob em cada lista de blob.|  
|`Blob/BlobPath`|Cadeia|Olá relativo URI toohello blob, começando com o nome do contentor Olá. Se tiver blob Olá recipiente-raiz, tem de começar com `$root`.|  
|`Blob/FilePath`|Cadeia|Especifica Olá caminho relativo toohello ficheiro na unidade de Olá. Para as tarefas de exportação, caminho do blob Olá será utilizado para o caminho do ficheiro de Olá se for possível; *por exemplo,*, `pictures/bob/wild/desert.jpg` serão exportados demasiado`\pictures\bob\wild\desert.jpg`. No entanto, devido a limitações de toohello dos nomes NTFS, um blob pode ser exportado tooa ficheiro com um caminho que não assemelhar-se o caminho do blob Olá.|  
|`Blob/ClientData`|Cadeia|Opcional. Contém os comentários do cliente de Olá. Este valor não é interpretado pelo Olá serviço de importação/exportação.|  
|`Blob/Snapshot`|DateTime|Opcional para as tarefas de exportação. Especifica o identificador de instantâneos de Olá para um instantâneo de blob exportado.|  
|`Blob/Length`|Número inteiro|Especifica o comprimento do blob Olá total Olá em bytes. valor de Olá poderá segurança too200 GB para um blob de bloco e cópia de segurança too1 TB para um blob de página. Para um blob de página, este valor tem de ser um múltiplo de 512.|  
|`Blob/ImportDisposition`|Cadeia|Opcional para tarefas de importação, omitidas para as tarefas de exportação. Esta ação Especifica a forma como Olá serviço importar/exportar deve processar caso Olá para uma tarefa de importação onde um blob com Olá mesmo nome já existe. Se este valor é omitido do manifesto de importação de Olá, o valor predefinido de Olá é `rename`.<br /><br /> os valores de Olá para este elemento incluem:<br /><br /> -   `no-overwrite`: Se um blob de destino já está presente Olá com o mesmo nome, uma operação de importação de Olá irá ignorar este ficheiro a importar.<br />-   `overwrite`: Quaisquer blob de destino existente está substituído completamente pelo ficheiro importado recentemente Olá.<br />-   `rename`: blob novo Olá será carregado com um nome de modificação.<br /><br /> Olá mudar o nome de regra é o seguinte:<br /><br /> -Se o nome do blob Olá não contém um ponto, um novo nome é gerado, acrescentando `(2)` toohello blob nome original; se este novo nome também está em conflito com um nome de blob existente, em seguida, `(3)` é acrescentada em vez de `(2)`; e assim sucessivamente.<br />-Se o nome do blob Olá contém um ponto, parte Olá seguir dot último Olá é considerado o nome da extensão Olá. Semelhante toohello acima procedimento, `(2)` é inserido antes Olá último ponto toogenerate um novo nome; se o novo nome de Olá ainda está em conflito com um nome de blob existente, em seguida, o serviço de Olá tenta `(3)`, `(4)`, e assim sucessivamente, até uma não esteja em conflito nome se encontra.<br /><br /> Alguns exemplos:<br /><br /> blob Olá `BlobNameWithoutDot` vai ser mudado para:<br /><br /> `BlobNameWithoutDot (2)  // if BlobNameWithoutDot exists`<br /><br /> `BlobNameWithoutDot (3)  // if both BlobNameWithoutDot and BlobNameWithoutDot (2) exist`<br /><br /> blob Olá `Seattle.jpg` vai ser mudado para:<br /><br /> `Seattle (2).jpg  // if Seattle.jpg exists`<br /><br /> `Seattle (3).jpg  // if both Seattle.jpg and Seattle (2).jpg exist`|  
|`PageRangeList`|Aninhada elemento XML|Necessário para um blob de página.<br /><br /> Para uma importação operação especifica uma lista de intervalos de bytes de toobe um ficheiro importado. Cada intervalo de páginas é descrito por um desvio e comprimento no ficheiro de origem Olá que descreve o intervalo de página Olá, juntamente com um hash MD5 da região de Olá. Olá `Hash` é necessário o atributo de um intervalo de página. serviço de Olá irá validar que hash Olá dos dados de Olá num blob Olá corresponde ao hash MD5 de Olá calculado do intervalo de páginas de Olá. Qualquer número de intervalos de página poderá toodescribe utilizado um ficheiro de importação, com o tamanho total do Olá segurança too1 TB. Todos os intervalos de página tem de ser ordenados por deslocamento e sem sobreposições são permitidas.<br /><br /> Para uma operação de exportação, especifica um conjunto de intervalos de byte de um blob que foram exportados toohello unidade.<br /><br /> intervalos de página Olá em conjunto podem abranger apenas secundárias intervalos de um blob ou um ficheiro.  parte restante do Olá do ficheiro de Olá não abrangido por qualquer intervalo de páginas é esperado e respetivo conteúdo pode ser definido.|  
|`PageRange`|Elemento XML|Representa um intervalo de páginas.|  
|`PageRange/@Offset`|Atributo de número inteiro|Especifica o deslocamento de Olá no ficheiro de transferência Olá e BLOBs Olá quando o intervalo de páginas especificado Olá começa. Este valor tem de ser um múltiplo de 512.|  
|`PageRange/@Length`|Atributo de número inteiro|Especifica o comprimento do intervalo de páginas de Olá Olá. Este valor tem de ser um múltiplo de 512 e não mais de 4 MB.|  
|`PageRange/@Hash`|Atributo, cadeia|Especifica o valor de hash MD5 codificado Base16 Olá para o intervalo de páginas de Olá.|  
|`BlockList`|Aninhada elemento XML|Necessário para um blob de blocos com blocos com nome.<br /><br /> Para uma operação de importação, a lista de bloqueios de Olá Especifica um conjunto de blocos que serão importados para o Storage do Azure. Para uma operação de exportação, a lista de bloqueios de Olá Especifica onde cada bloco tenha sido armazenado no ficheiro de Olá no disco de exportação de Olá. Cada bloco é descrito por um desvio nos ficheiros de Olá e um comprimento do bloco; cada bloco além disso é designado por um atributo de ID de bloco e contém um hash MD5 para bloco de Olá. Cópia de segurança too50, 000 blocos podem ser utilizado toodescribe um blob.  Todos os blocos têm de ser ordenados por deslocamento e em conjunto deve abranger o intervalo completo de Olá ficheiro Olá, *ou seja,*, não tem de existir nenhum intervalo entre blocos. Se Olá do blob é mais do que 64 MB, o bloco de Olá IDs para cada bloco tem de ser todos os não existe ou todas as apresentam. Os IDs de bloco são toobe necessário com codificação Base64 cadeias. Consulte [colocar bloco](/rest/api/storageservices/put-block) para obter os requisitos para IDs de bloco.|  
|`Block`|Elemento XML|Representa um bloco.|  
|`Block/@Offset`|Atributo de número inteiro|Especifica o deslocamento de olá onde o bloco especificado Olá começa.|  
|`Block/@Length`|Atributo de número inteiro|Especifica o número de Olá de bytes no bloco de Olá; Este valor tem de ser não mais de 4MB.|  
|`Block/@Id`|Atributo, cadeia|Especifica uma cadeia representando o ID do bloco Olá para bloco de Olá.|  
|`Block/@Hash`|Atributo, cadeia|Especifica Olá codificado Base16 MD5 hash de bloco de Olá.|  
|`Blob/MetadataPath`|Cadeia|Opcional. Especifica o caminho relativo de Olá de um ficheiro de metadados. Durante a importação, os metadados Olá está definido no blob de destino Olá. Durante uma operação de exportação, os metadados blob Olá são armazenados no ficheiro de metadados de Olá na unidade de Olá.|  
|`Blob/MetadataPath/@Hash`|Atributo, cadeia|Especifica Olá codificado Base16 MD5 hash de ficheiro de metadados do blob Olá.|  
|`Blob/PropertiesPath`|Cadeia|Opcional. Especifica o caminho relativo de Olá de um ficheiro de propriedades. Durante a importação, as propriedades de Olá estão definidas num blob de destino Olá. Durante uma operação de exportação, as propriedades de blob de Olá são armazenadas no ficheiro de propriedades de Olá na unidade de Olá.|  
|`Blob/PropertiesPath/@Hash`|Atributo, cadeia|Especifica Olá codificado Base16 MD5 hash do ficheiro de propriedades blob Olá.|  
  
## <a name="next-steps"></a>Passos seguintes
 
* [API de REST do Storage para importar/exportar](/rest/api/storageimportexport/)
