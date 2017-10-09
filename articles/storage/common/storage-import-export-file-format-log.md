---
title: "formato de ficheiro de registo de importação/exportação aaaAzure | Microsoft Docs"
description: "Saiba mais sobre o formato de Olá Olá dos ficheiros de registo criado quando são executados os passos para uma tarefa de serviço de importação/exportação."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 38cc16bd-ad55-4625-9a85-e1726c35fd1b
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: 15a652455aa947922af0aa39ccefe68811a3db19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-importexport-service-log-file-format"></a>Formato do ficheiro de registo de serviço do Azure para importar/exportar
Quando Olá serviço de importação/exportação do Microsoft Azure efetua uma ação num disco como parte de uma tarefa de importação ou uma tarefa de exportação, os registos são escritos tooblock blobs na conta do storage Olá associada com essa tarefa.  
  
Existem dois registos que podem ser escritos pelo Olá serviço importar/exportar:  
  
-   registo de erros de Olá sempre é gerado no evento Olá de um erro.  
  
-   Olá registo verboso não está ativado por predefinição, mas pode ser ativado por definição Olá `EnableVerboseLog` propriedade um [colocar tarefa](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) ou [propriedades da tarefa de atualização](/rest/api/storageimportexport/jobs#Jobs_Update) operação.  
  
## <a name="log-file-location"></a>Localização do ficheiro de registo  
Olá registos são escritos tooblock blobs no contentor de Olá ou diretório virtual especificado pelo Olá `ImportExportStatesPath` definição, que podem ser definidas num `Put Job` operação. Olá localização toowhich Olá registos são escritos depende de como a autenticação é especificada para a tarefa de Olá, juntamente com o valor de Olá especificado para `ImportExportStatesPath`. Autenticação para a tarefa de Olá pode ser especificada através de uma chave de conta de armazenamento ou de um contentor SAS (assinatura de acesso partilhado).  
  
nome de Olá do contentor de Olá ou diretório virtual poderá a ser Olá predefinido nome de `waimportexport`, ou outro contentor ou nome do diretório virtual que especificou.  
  
tabela de Olá abaixo mostra as opções de possíveis Olá:  
  
|Método de Autenticação|O valor de `ImportExportStatesPath`elemento|Localização de Blobs de registo|  
|---------------------------|----------------------------------------------|---------------------------|  
|Chave de conta de armazenamento|Valor predefinido|Um contentor com o nome `waimportexport`, que é o contentor do Olá predefinido. Por exemplo:<br /><br /> `https://myaccount.blob.core.windows.net/waimportexport`|  
|Chave de conta de armazenamento|Valor de utilizador especificado|Um contentor designado por utilizador Olá. Por exemplo:<br /><br /> `https://myaccount.blob.core.windows.net/mylogcontainer`|  
|Contentor SAS|Valor predefinido|Um diretório virtual com o nome `waimportexport`, que é o nome predefinido de Olá, por baixo do contentor de Olá especificado na Olá SAS.<br /><br /> Por exemplo, se Olá SAS especificado para a tarefa de Olá é `https://myaccount.blob.core.windows.net/mylogcontainer?sv=2012-02-12&se=2015-05-22T06%3A54%3A55Z&sr=c&sp=wl&sig=sigvalue`, em seguida, a localização de registo Olá seria`https://myaccount.blob.core.windows.net/mylogcontainer/waimportexport`|  
|Contentor SAS|Valor de utilizador especificado|Um diretório virtual com o nome pelo utilizador Olá, por baixo do contentor de Olá especificado na Olá SAS.<br /><br /> Por exemplo, se Olá SAS especificado para a tarefa de Olá é `https://myaccount.blob.core.windows.net/mylogcontainer?sv=2012-02-12&se=2015-05-22T06%3A54%3A55Z&sr=c&sp=wl&sig=sigvalue`, e Olá especificado diretório virtual é denominado `mylogblobs`, em seguida, a localização de registo Olá seria `https://myaccount.blob.core.windows.net/mylogcontainer/waimportexport/mylogblobs`.|  
  
Pode obter URL Olá para registos de verbosos e erro Olá ao chamar Olá [Get Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operação. estão disponíveis registos de Olá após a conclusão do processamento da unidade de Olá.  
  
## <a name="log-file-format"></a>Formato de ficheiro de registo  
Olá formato para ambos os registos é Olá mesmo: um blob que contém XML as descrições dos eventos de Olá que ocorreram durante a cópia de blobs entre o disco rígido Olá e conta hello do cliente.  
  
registo verboso Olá contém informações sobre o estado de Olá de operação de cópia de Olá para cada blob (para uma tarefa de importação) ou o ficheiro (para uma tarefa de exportação), enquanto que o registo de erros de Olá contém apenas informações de Olá para blobs ou ficheiros que encontrou erros durante a Olá importar ou exportar a tarefa.  
  
formato de registo verboso Olá é mostrado abaixo. registo de erros de Olá tem Olá mesmo estrutura, mas filtra operações com êxito.  

```xml
<DriveLog Version="2014-11-01">  
  <DriveId>drive-id</DriveId>  
  [<Blob Status="blob-status">  
   <BlobPath>blob-path</BlobPath>  
   <FilePath>file-path</FilePath>  
   [<Snapshot>snapshot</Snapshot>]  
   <Length>length</Length>  
   [<LastModified>last-modified</LastModified>]  
   [<ImportDisposition Status="import-disposition-status">import-disposition</ImportDisposition>]  
   [page-range-list-or-block-list]  
   [metadata-status]  
   [properties-status]  
  </Blob>]  
  [<Blob>  
    . . .  
  </Blob>]  
  <Status>drive-status</Status>  
</DriveLog>  
  
page-range-list-or-block-list ::= 
  page-range-list | block-list  
  
page-range-list ::=   
<PageRangeList>  
      [<PageRange Offset="page-range-offset" Length="page-range-length"   
       [Hash="md5-hash"] Status="page-range-status"/>]  
      [<PageRange Offset="page-range-offset" Length="page-range-length"   
       [Hash="md5-hash"] Status="page-range-status"/>]  
</PageRangeList>  
  
block-list ::=  
<BlockList>  
      [<Block Offset="block-offset" Length="block-length" [Id="block-id"]  
       [Hash="md5-hash"] Status="block-status"/>]  
      [<Block Offset="block-offset" Length="block-length" [Id="block-id"]   
       [Hash="md5-hash"] Status="block-status"/>]  
</BlockList>  
  
metadata-status ::=  
<Metadata Status="metadata-status">  
   [<GlobalPath Hash="md5-hash">global-metadata-file-path</GlobalPath>]  
   [<Path Hash="md5-hash">metadata-file-path</Path>]  
</Metadata>  
  
properties-status ::=  
<Properties Status="properties-status">  
   [<GlobalPath Hash="md5-hash">global-properties-file-path</GlobalPath>]  
   [<Path Hash="md5-hash">properties-file-path</Path>]  
</Properties>  
```

Olá seguinte tabela descreve os elementos de Olá Olá do ficheiro de registo.  
  
|Elemento XML|Tipo|Descrição|  
|-----------------|----------|-----------------|  
|`DriveLog`|Elemento XML|Representa um registo de unidade.|  
|`Version`|Atributo, cadeia|versão de Olá do formato de registo Olá.|  
|`DriveId`|Cadeia|Olá, número de série de hardware da unidade.|  
|`Status`|Cadeia|Estado de processamento de unidade de Olá. Consulte Olá `Drive Status Codes` tabela abaixo para obter mais informações.|  
|`Blob`|Aninhada elemento XML|Representa um blob.|  
|`Blob/BlobPath`|Cadeia|URI de blob Olá Olá.|  
|`Blob/FilePath`|Cadeia|Olá caminho relativo toohello o ficheiro na unidade de Olá.|  
|`Blob/Snapshot`|DateTime|versão de instantâneo de Olá do blob Olá, para apenas uma tarefa de exportação.|  
|`Blob/Length`|Número inteiro|comprimento total Olá dos BLOBs Olá em bytes.|  
|`Blob/LastModified`|DateTime|Olá data/hora esse blob Olá foi modificado pela última vez, para apenas uma tarefa de exportação.|  
|`Blob/ImportDisposition`|Cadeia|Olá importar disposição de blob Olá, apenas uma tarefa de importação.|  
|`Blob/ImportDisposition/@Status`|Atributo, cadeia|Estado de Olá de Olá importar disposição.|  
|`PageRangeList`|Aninhada elemento XML|Representa uma lista de intervalos de página para um blob de página.|  
|`PageRange`|Elemento XML|Representa um intervalo de páginas.|  
|`PageRange/@Offset`|Atributo de número inteiro|A partir de deslocamento do intervalo de páginas de Olá blob Olá.|  
|`PageRange/@Length`|Atributo de número inteiro|Comprimento em bytes do intervalo de páginas de Olá.|  
|`PageRange/@Hash`|Atributo, cadeia|Com codificação Base16 hash MD5 do intervalo de páginas de Olá.|  
|`PageRange/@Status`|Atributo, cadeia|Estado do processamento de intervalo de páginas de Olá.|  
|`BlockList`|Aninhada elemento XML|Representa uma lista de blocos para um blob de blocos.|  
|`Block`|Elemento XML|Representa um bloco.|  
|`Block/@Offset`|Atributo de número inteiro|Desvio inicial de Olá bloco num blob Olá.|  
|`Block/@Length`|Atributo de número inteiro|Comprimento em bytes do bloco de Olá.|  
|`Block/@Id`|Atributo, cadeia|ID do bloco de Olá.|  
|`Block/@Hash`|Atributo, cadeia|Com codificação Base16 hash MD5 do bloco de Olá.|  
|`Block/@Status`|Atributo, cadeia|Estado do bloco de Olá de processamento.|  
|`Metadata`|Aninhada elemento XML|Representa os metadados do blob Olá.|  
|`Metadata/@Status`|Atributo, cadeia|Estado de processamento de metadados do blob Olá.|  
|`Metadata/GlobalPath`|Cadeia|Ficheiro de metadados globais do caminho relativo toohello.|  
|`Metadata/GlobalPath/@Hash`|Atributo, cadeia|Com codificação Base16 hash MD5 do ficheiro de metadados globais Olá.|  
|`Metadata/Path`|Cadeia|Ficheiro de metadados do caminho relativo toohello.|  
|`Metadata/Path/@Hash`|Atributo, cadeia|Com codificação Base16 MD5 hash de ficheiro de metadados de Olá.|  
|`Properties`|Aninhada elemento XML|Representa as propriedades de blob Olá.|  
|`Properties/@Status`|Atributo, cadeia|Estado do processamento de propriedades de blob Olá, por exemplo, ficheiro não encontrado; foi concluída.|  
|`Properties/GlobalPath`|Cadeia|Ficheiros do caminho relativo toohello propriedades globais.|  
|`Properties/GlobalPath/@Hash`|Atributo, cadeia|Com codificação Base16 hash MD5 do ficheiro de propriedades globais Olá.|  
|`Properties/Path`|Cadeia|Ficheiro de propriedades do caminho relativo toohello.|  
|`Properties/Path/@Hash`|Atributo, cadeia|Com codificação Base16 hash MD5 do ficheiro de propriedades de Olá.|  
|`Blob/Status`|Cadeia|Estado do processamento de blob Olá.|  
  
# <a name="drive-status-codes"></a>Códigos de estado de unidade  
Olá tabela seguinte lista os códigos de estado de Olá para uma unidade de processamento.  
  
|Código de estado|Descrição|  
|-----------------|-----------------|  
|`Completed`|unidade de Olá concluiu o processamento sem erros.|  
|`CompletedWithWarnings`|unidade de Olá concluiu o processamento com avisos num ou mais blobs por dispositions de importação de Olá especificados para o blobs Olá.|  
|`CompletedWithErrors`|unidade de Olá foi concluída com erros de um ou mais blobs ou segmentos.|  
|`DiskNotFound`|Está localizado nenhum disco na unidade de Olá.|  
|`VolumeNotNtfs`|Olá primeiro dados volume num disco Olá não está no formato NTFS.|  
|`DiskOperationFailed`|Ocorreu uma falha desconhecida ao realizar operações na unidade de Olá.|  
|`BitLockerVolumeNotFound`|Não foi encontrado nenhum volume encryptable do BitLocker.|  
|`BitLockerNotActivated`|O BitLocker não estiver ativado num volume de Olá.|  
|`BitLockerProtectorNotFound`|protetor de chave de palavra-passe numérica Olá não existe no volume de Olá.|  
|`BitLockerKeyInvalid`|Olá numérica palavra-passe fornecida não é possível desbloquear o volume de Olá.|  
|`BitLockerUnlockVolumeFailed`|Falha desconhecida tiver ocorrido durante a tentativa de volume de Olá toounlock.|  
|`BitLockerFailed`|Ocorreu uma falha desconhecida ao executar operações de BitLocker.|  
|`ManifestNameInvalid`|nome de ficheiro de manifesto Olá é inválido.|  
|`ManifestNameTooLong`|nome de ficheiro de manifesto Olá é demasiado longo.|  
|`ManifestNotFound`|o ficheiro de manifesto Olá não foi encontrado.|  
|`ManifestAccessDenied`|Ficheiro de manifesto de toohello de acesso é negado.|  
|`ManifestCorrupted`|Olá ficheiro de manifesto está danificado (conteúdo Olá não corresponde ao respetivo hash).|  
|`ManifestFormatInvalid`|conteúdo de manifesto Olá não está em conformidade com formato necessário toohello.|  
|`ManifestDriveIdMismatch`|unidade de Olá não corresponde ao ID de ficheiro de manifesto Olá Olá uma leitura do disco de Olá.|  
|`ReadManifestFailed`|Ocorreu um falha de e/s de disco ao ler o manifesto Olá.|  
|`BlobListFormatInvalid`|blob de lista de BLOBs de exportação de Olá não está em conformidade com formato necessário toohello.|  
|`BlobRequestForbidden`|Aceder a blobs toohello na conta do storage Olá é proibido. Esta situação pode ser devido a chave de conta do storage tooinvalid ou contentor SAS.|  
|`InternalError`|E, Ocorreu um erro interno ao processar a unidade de Olá.|  
  
## <a name="blob-status-codes"></a>Códigos de estado de blob  
Olá tabela seguinte lista os códigos de estado de Olá para o processamento de um blob.  
  
|Código de estado|Descrição|  
|-----------------|-----------------|  
|`Completed`|blob Olá concluiu o processamento sem erros.|  
|`CompletedWithErrors`|blob Olá concluiu o processamento de erros em um ou mais intervalos de página ou blocos, os metadados ou propriedades.|  
|`FileNameInvalid`|nome de ficheiro Olá é inválido.|  
|`FileNameTooLong`|nome de ficheiro Olá é demasiado longo.|  
|`FileNotFound`|Olá ficheiro não encontrado.|  
|`FileAccessDenied`|Ficheiro de toohello de acesso é negado.|  
|`BlobRequestFailed`|Falha no pedido de serviço Blob Olá tooaccess Olá blob.|  
|`BlobRequestForbidden`|pedido de serviço Blob Olá tooaccess Olá blob é proibido. Esta situação pode ser devido a chave de conta do storage tooinvalid ou contentor SAS.|  
|`RenameFailed`|Falha ao blob do Olá toorename (para uma tarefa de importação) ou ficheiro Olá (para uma tarefa de exportação).|  
|`BlobUnexpectedChange`|Tiver ocorrido uma alteração inesperada com BLOBs Olá (para uma tarefa de exportação).|  
|`LeasePresent`|Há uma concessão presente no blob Olá.|  
|`IOFailed`|Um disco ou a falha de e/s de rede ocorreu ao processar o blob Olá.|  
|`Failed`|Ocorreu uma falha desconhecida ao processar o blob Olá.|  
  
## <a name="import-disposition-status-codes"></a>Códigos de estado de disposição de importação  
Olá tabela seguinte lista os códigos de estado de Olá para resolver uma disposição de importação.  
  
|Código de estado|Descrição|  
|-----------------|-----------------|  
|`Created`|blob Olá foi criado.|  
|`Renamed`|blob Olá foi alterado por disposição de importação de mudança de nome. Olá `Blob/BlobPath` elemento contém Olá URI de blob Olá mudado.|  
|`Skipped`|blob Olá foi ignorado por `no-overwrite` importar disposição.|  
|`Overwritten`|blob Olá substituíram um blob existente por `overwrite` importar disposição.|  
|`Cancelled`|Uma falha anterior foi parado o processamento disposição de importação de Olá.|  
  
## <a name="page-rangeblock-status-codes"></a>Códigos de estado de intervalo/bloco de página  
Olá tabela seguinte lista os códigos de estado de Olá para o processamento de um intervalo de página ou um bloco.  
  
|Código de estado|Descrição|  
|-----------------|-----------------|  
|`Completed`|intervalo de páginas de Olá ou bloco concluiu o processamento sem erros.|  
|`Committed`|Bloco de Olá tiver sido consolidado, mas não no Olá lista de bloqueios completa porque outros blocos tem falha ou coloque a lista de bloqueios completa próprio tem falhou.|  
|`Uncommitted`|Bloco de Olá é carregado, mas não consolidado.|  
|`Corrupted`|intervalo de páginas de Olá ou de bloqueios está danificado (conteúdo Olá não corresponde ao respetivo hash).|  
|`FileUnexpectedEnd`|Foi detetado um fim inesperado do ficheiro.|  
|`BlobUnexpectedEnd`|Foi detetado um fim inesperado do blob.|  
|`BlobRequestFailed`|Falha ao bloco ou Olá pedido de serviço Blob tooaccess Olá intervalo de páginas.|  
|`IOFailed`|Um disco ou a falha de e/s de rede ocorreu ao processar o intervalo de páginas de Olá ou de bloqueios.|  
|`Failed`|Ocorreu uma falha desconhecida ao processar o intervalo de páginas de Olá ou de bloqueios.|  
|`Cancelled`|Uma falha anterior foi parado o processamento adicional do intervalo de páginas de Olá ou de bloqueios.|  
  
## <a name="metadata-status-codes"></a>Códigos de estado de metadados  
Olá tabela seguinte lista os códigos de estado de Olá para metadados do blob de processamento.  
  
|Código de estado|Descrição|  
|-----------------|-----------------|  
|`Completed`|metadados de Olá concluiu o processamento sem erros.|  
|`FileNameInvalid`|nome de ficheiro de metadados de Olá é inválido.|  
|`FileNameTooLong`|nome de ficheiro de metadados de Olá é demasiado longo.|  
|`FileNotFound`|ficheiro de metadados de Olá não foi encontrado.|  
|`FileAccessDenied`|Ficheiro de metadados de toohello de acesso é negado.|  
|`Corrupted`|ficheiro de metadados de Olá está danificado (conteúdo Olá não corresponde ao respetivo hash).|  
|`XmlReadFailed`|conteúdo de metadados de Olá não está em conformidade com formato necessário toohello.|  
|`XmlWriteFailed`|Escrever metadados Olá que XML falhou.|  
|`BlobRequestFailed`|Falha no pedido de serviço Blob Olá tooaccess Olá metadados.|  
|`IOFailed`|Ocorreu uma falha de e/s de disco ou de rede durante o processamento de metadados de Olá.|  
|`Failed`|Ocorreu uma falha desconhecida ao processar Olá metadados.|  
|`Cancelled`|Uma falha anterior foi parado o processamento Olá metadados.|  
  
## <a name="properties-status-codes"></a>Códigos de estado de propriedades  
Olá tabela seguinte lista os códigos de estado de Olá para o processamento de propriedades de blob.  
  
|Código de estado|Descrição|  
|-----------------|-----------------|  
|`Completed`|Propriedades de Olá tem concluído o processamento sem erros.|  
|`FileNameInvalid`|nome de ficheiro de propriedades de Olá é inválido.|  
|`FileNameTooLong`|nome de ficheiro de propriedades de Olá é demasiado longo.|  
|`FileNotFound`|ficheiro de propriedades de Olá não encontrado.|  
|`FileAccessDenied`|Ficheiro de propriedades de toohello de acesso é negado.|  
|`Corrupted`|Olá propriedades ficheiro está corrompido (conteúdo Olá não corresponde ao respetivo hash).|  
|`XmlReadFailed`|conteúdo de propriedades de Olá não está em conformidade com formato necessário toohello.|  
|`XmlWriteFailed`|Escrever propriedades Olá que XML falhou.|  
|`BlobRequestFailed`|Falha no pedido de serviço Blob Olá tooaccess Olá propriedades.|  
|`IOFailed`|Ocorreu uma falha de e/s de disco ou de rede durante o processamento de propriedades de Olá.|  
|`Failed`|Ocorreu uma falha desconhecida ao processar propriedades Olá.|  
|`Cancelled`|Uma falha anterior foi parado o processamento adicional de propriedades de Olá.|  
  
## <a name="sample-logs"></a>Registos de exemplo  
Olá segue-se um exemplo de registo verboso.  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<DriveLog Version="2014-11-01">  
    <DriveId>WD-WMATV123456</DriveId>  
    <Blob Status="Completed">  
       <BlobPath>pictures/bob/wild/desert.jpg</BlobPath>  
       <FilePath>\Users\bob\Pictures\wild\desert.jpg</FilePath>  
       <Length>98304</Length>  
       <ImportDisposition Status="Created">overwrite</ImportDisposition>  
       <BlockList>  
          <Block Offset="0" Length="65536" Id="AAAAAA==" Hash=" 9C8AE14A55241F98533C4D80D85CDC68" Status="Completed"/>  
          <Block Offset="65536" Length="32768" Id="AQAAAA==" Hash=" DF54C531C9B3CA2570FDDDB3BCD0E27D" Status="Completed"/>  
       </BlockList>  
       <Metadata Status="Completed">  
          <GlobalPath Hash=" E34F54B7086BCF4EC1601D056F4C7E37">\Users\bob\Pictures\wild\metadata.xml</GlobalPath>  
       </Metadata>  
    </Blob>  
    <Blob Status="CompletedWithErrors">  
       <BlobPath>pictures/bob/animals/koala.jpg</BlobPath>  
       <FilePath>\Users\bob\Pictures\animals\koala.jpg</FilePath>  
       <Length>163840</Length>  
       <ImportDisposition Status="Overwritten">overwrite</ImportDisposition>  
       <PageRangeList>  
          <PageRange Offset="0" Length="65536" Hash="19701B8877418393CB3CB567F53EE225" Status="Completed"/>  
          <PageRange Offset="65536" Length="65536" Hash="AA2585F6F6FD01C4AD4256E018240CD4" Status="Corrupted"/>  
          <PageRange Offset="131072" Length="4096" Hash="9BA552E1C3EEAFFC91B42B979900A996" Status="Completed"/>  
       </PageRangeList>  
       <Properties Status="Completed">  
          <Path Hash="38D7AE80653F47F63C0222FEE90EC4E7">\Users\bob\Pictures\animals\koala.jpg.properties</Path>  
       </Properties>  
    </Blob>  
    <Status>CompletedWithErrors</Status>  
</DriveLog>  
```  
  
registo de erro correspondente Olá é mostrado abaixo.  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<DriveLog Version="2014-11-01">  
    <DriveId>WD-WMATV6965824</DriveId>  
    <Blob Status="CompletedWithErrors">  
       <BlobPath>pictures/bob/animals/koala.jpg</BlobPath>  
       <FilePath>\Users\bob\Pictures\animals\koala.jpg</FilePath>  
       <Length>163840</Length>  
       <ImportDisposition Status="Overwritten">overwrite</ImportDisposition>  
       <PageRangeList>  
          <PageRange Offset="65536" Length="65536" Hash="AA2585F6F6FD01C4AD4256E018240CD4" Status="Corrupted"/>  
       </PageRangeList>  
    </Blob>  
    <Status>CompletedWithErrors</Status>  
</DriveLog>  
```

 registo de erros de siga Olá para uma tarefa de importação contém um erro sobre um ficheiro não encontrado na unidade de importação de Olá. Tenha em atenção que o estado de Olá dos componentes subsequentes é `Cancelled`.  
  
```xml
<?xml version="1.0" encoding="utf-8"?>  
<DriveLog Version="2014-11-01">  
  <DriveId>9WM35C2V</DriveId>  
  <Blob Status="FileNotFound">  
    <BlobPath>pictures/animals/koala.jpg</BlobPath>  
    <FilePath>\animals\koala.jpg</FilePath>  
    <Length>30310</Length>  
    <ImportDisposition Status="Cancelled">rename</ImportDisposition>  
    <BlockList>  
      <Block Offset="0" Length="6062" Id="MD5/cAzn4h7VVSWXf696qp5Uaw==" Hash="700CE7E21ED55525977FAF7AAA9E546B" Status="Cancelled" />  
      <Block Offset="6062" Length="6062" Id="MD5/PEnGwYOI8LPLNYdfKr7kAg==" Hash="3C49C6C18388F0B3CB35875F2ABEE402" Status="Cancelled" />  
      <Block Offset="12124" Length="6062" Id="MD5/FG4WxqfZKuUWZ2nGTU2qVA==" Hash="146E16C6A7D92AE5166769C64D4DAA54" Status="Cancelled" />  
      <Block Offset="18186" Length="6062" Id="MD5/ZzibNDzr3IRBQENRyegeXQ==" Hash="67389B343CEBDC8441404351C9E81E5D" Status="Cancelled" />  
      <Block Offset="24248" Length="6062" Id="MD5/ZzibNDzr3IRBQENRyegeXQ==" Hash="67389B343CEBDC8441404351C9E81E5D" Status="Cancelled" />  
    </BlockList>  
  </Blob>  
  <Status>CompletedWithErrors</Status>  
</DriveLog>  
```

Olá seguinte registo de erros para uma tarefa de exportação indica que conteúdo de blob Olá tem foi escrita com êxito na unidade de toohello, mas que ocorreu um erro ao exportar as propriedades de blob Olá.  
  
```xml
<?xml version="1.0" encoding="utf-8"?>  
<DriveLog Version="2014-11-01">  
  <DriveId>9WM35C3U</DriveId>  
  <Blob Status="CompletedWithErrors">  
    <BlobPath>pictures/wild/canyon.jpg</BlobPath>  
    <FilePath>\pictures\wild\canyon.jpg</FilePath>  
    <LastModified>2012-09-18T23:47:08Z</LastModified>  
    <Length>163840</Length>  
    <BlockList />  
    <Properties Status="Failed" />  
  </Blob>  
  <Status>CompletedWithErrors</Status>  
</DriveLog>  
```
  
## <a name="next-steps"></a>Passos seguintes
 
* [API de REST do Storage para importar/exportar](/rest/api/storageimportexport/)
