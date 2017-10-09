---
title: "tarefa de importar aaaSample fluxo de trabalho tooprep unidades de disco rígido para um Azure para importar/exportar | Microsoft Docs"
description: "Consulte as instruções para o processo de conclusão de Olá da preparação unidades para uma tarefa de importação Olá serviço importar/exportar do Azure."
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
ms.date: 04/07/2017
ms.author: muralikk
ms.openlocfilehash: 560220b7dc9f87416f1fec1ff30fa5cd65812ce5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="sample-workflow-tooprepare-hard-drives-for-an-import-job"></a>Discos rígidos do tooprepare de fluxo de trabalho de exemplo para uma tarefa de importação

Este artigo orienta-o através do processo completo de Olá da preparação unidades para uma tarefa de importação.

## <a name="sample-data"></a>Dados de exemplo

Neste exemplo importa os seguintes dados para uma conta do storage do Azure com o nome de Olá `mystorageaccount`:

|Localização|Descrição|Tamanho dos dados|
|--------------|-----------------|-----|
|H:\Video\ |Uma coleção de vídeos|12 TB|
|H:\Photo\ |Uma coleção de fotografias|30 GB|
|K:\Temp\FavoriteMovie.ISO|Imagem de disco A Blu-ray™|25 GB|
|\\\bigshare\john\music\|Uma coleção de ficheiros de música numa partilha de rede|10 GB|

## <a name="storage-account-destinations"></a>Destinos de conta de armazenamento

tarefa de importação de Olá irá importar dados de Olá para Olá destinos na conta do storage Olá os seguintes:

|Origem|Diretório virtual de destino ou blob|
|------------|-------------------------------------------|
|H:\Video\ |vídeo /|
|H:\Photo\ |fotografia /|
|K:\Temp\FavoriteMovie.ISO|favorite/FavoriteMovies.ISO|
|\\\bigshare\john\music\ |música|

Com este mapeamento Olá ficheiro `H:\Video\Drama\GreatMovie.mov` serão importados toohello blob `https://mystorageaccount.blob.core.windows.net/video/Drama/GreatMovie.mov`.

## <a name="determine-hard-drive-requirements"></a>Determinar os requisitos de disco rígido

Toodetermine seguinte, o número de unidades de disco rígido forem necessárias, computação Olá tamanho dos dados de Olá:

`12TB + 30GB + 25GB + 10GB = 12TB + 65GB`

Neste exemplo, dois discos rígidos de 8TB devem ser suficientes. No entanto, dado que o diretório de origem Olá `H:\Video` tem 12TB de dados e a capacidade do disco rígido único é apenas de 8TB, será capaz de toospecify isto em Olá seguintes forma no Olá **driveset.csv** ficheiro:

```
DriveLetter,FormatOption,SilentOrPromptOnFormat,Encryption,ExistingBitLockerKey
X,Format,SilentMode,Encrypt,
Y,Format,SilentMode,Encrypt,
```
ferramenta de Olá será distribuem dados em duas unidades de disco rígidas uma forma otimizada.

## <a name="attach-drives-and-configure-hello-job"></a>Anexar unidades e configurar a tarefa de Olá
Irá ligar a máquina de toohello ambos os discos e crie volumes. Em seguida, criar **dataset.csv** ficheiro:
```
BasePath,DstBlobPathOrPrefix,BlobType,Disposition,MetadataFile,PropertiesFile
H:\Video\,video/,BlockBlob,rename,None,H:\mydirectory\properties.xml
H:\Photo\,photo/,BlockBlob,rename,None,H:\mydirectory\properties.xml
K:\Temp\FavoriteVideo.ISO,favorite/FavoriteVideo.ISO,BlockBlob,rename,None,H:\mydirectory\properties.xml
\\myshare\john\music\,music/,BlockBlob,rename,None,H:\mydirectory\properties.xml
```

Além disso, pode definir Olá metadados para todos os ficheiros a seguir:

* **UploadMethod:** serviço de importação/exportação do Windows Azure
* **DataSetName:** SampleData
* **CreationDate:** 1/10/2013

tooset metadados para ficheiros de Olá importado, crie um ficheiro de texto, `c:\WAImportExport\SampleMetadata.txt`, com Olá seguinte conteúdo:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<Metadata>
    <UploadMethod>Windows Azure Import/Export service</UploadMethod>
    <DataSetName>SampleData</DataSetName>
    <CreationDate>10/1/2013</CreationDate>
</Metadata>
```

Também pode definir algumas propriedades para Olá `FavoriteMovie.ISO` blob:

* **Tipo de conteúdo:** application/octet-stream.
* **Content-MD5:** Q2hlY2sgSW50ZWdyaXR5IQ = =
* **Cache-Control:** não cache

tooset estas propriedades, crie um ficheiro de texto, `c:\WAImportExport\SampleProperties.txt`:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<Properties>
    <Content-Type>application/octet-stream</Content-Type>
    <Content-MD5>Q2hlY2sgSW50ZWdyaXR5IQ==</Content-MD5>
    <Cache-Control>no-cache</Cache-Control>
</Properties>
```

## <a name="run-hello-azure-importexport-tool-waimportexportexe"></a>Execute Olá ferramenta de importação/exportação do Azure (WAImportExport.exe)

Agora, está pronto toorun Olá ferramenta de importação/exportação do Azure tooprepare Olá duas unidades de disco rígido.

**Para Olá primeira sessão:**

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#1  /sk:************* /InitialDriveSet:driveset-1.csv /DataSet:dataset-1.csv /logdir:F:\logs
```

Se precisar de mais dados toobe adicionado, crie outro ficheiro de conjunto de dados (mesmo formato que Initialdataset).

**Para Olá segunda sessão:**

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#2  /DataSet:dataset-2.csv
```

Depois de concluíram as sessões de cópia de Olá, pode desligar duas unidades de Olá do computador de cópia de Olá e envie-los toohello adequado Datacenter do Azure. Deverá carregar os ficheiros do diário de alterações de Olá dois, `<FirstDriveSerialNumber>.xml` e `<SecondDriveSerialNumber>.xml`, quando criar tarefa de importação de Olá no Olá portal do Azure.

## <a name="next-steps"></a>Passos seguintes

* [Preparar as unidades de disco rígido para uma tarefa de importação](storage-import-export-tool-preparing-hard-drives-import.md)
* [Referência rápida para comandos utilizados com frequência](storage-import-export-tool-quick-reference.md)
