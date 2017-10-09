---
title: aaaCopy ou mover dados tooAzure armazenamento com o AzCopy no Windows | Microsoft Docs
description: "Utilize Olá AzCopy no Windows utilitário toomove ou copiar dados tooor de blob, tabela e o conteúdo do ficheiro. Copiar dados tooAzure armazenamento de ficheiros locais ou copie os dados dentro ou entre contas de armazenamento. Migre facilmente a sua tooAzure dados de armazenamento."
services: storage
documentationcenter: 
author: seguler
manager: jahogg
editor: tysonn
ms.assetid: aa155738-7c69-4a83-94f8-b97af4461274
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/14/2017
ms.author: seguler
ms.openlocfilehash: a77db84c3a3e06f0ad4e87d02b14a5c62ed8d9ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="transfer-data-with-hello-azcopy-on-windows"></a>Transferência de dados com Olá AzCopy no Windows
O AzCopy é um utilitário da linha de comandos concebido para copiar dados tooand do armazenamento de Blobs do Microsoft Azure, ficheiros e tabela utilizando comandos simples com um desempenho ideal. Pode copiar dados de um objeto tooanother dentro da sua conta de armazenamento, ou entre contas de armazenamento.

Existem duas versões do AzCopy que pode transferir. AzCopy no Windows baseia-se com o .NET Framework e o estilo de Windows esta oferece opções de linha de comandos. [AzCopy no Linux](storage-use-azcopy-linux.md) baseia-se com o .NET Core Framework que está direcionada para plataformas Linux oferta estilo POSIX opções da linha de comandos. Este artigo abrange AzCopy no Windows.

## <a name="download-and-install-azcopy"></a>Transfira e instale o AzCopy
### <a name="azcopy-on-windows"></a>AzCopy no Windows
Transferir Olá [versão mais recente do AzCopy no Windows](http://aka.ms/downloadazcopy).

#### <a name="installation-on-windows"></a>Instalação no Windows
Depois de instalar o AzCopy no Windows utilizando o instalador Olá, abra uma janela de comandos e navegue diretório de instalação do AzCopy toohello no seu computador - onde hello `AzCopy.exe` executável está localizado. Se assim o desejar, pode adicionar o caminho do sistema de tooyour instalação localização Olá AzCopy. Por predefinição, AzCopy é instalado demasiado`%ProgramFiles(x86)%\Microsoft SDKs\Azure\AzCopy` ou `%ProgramFiles%\Microsoft SDKs\Azure\AzCopy`.

## <a name="writing-your-first-azcopy-command"></a>Escrever o seu primeiro comando do AzCopy
sintaxe de básico Olá para comandos do AzCopy é:

```azcopy
AzCopy /Source:<source> /Dest:<destination> [Options]
```

Olá seguir exemplos demonstram uma variedade de cenários para copiar dados tooand do Microsoft Azure, ficheiros, tabelas e Blobs. Consulte toohello [AzCopy parâmetros](#azcopy-parameters) secção para obter uma explicação detalhada de parâmetros de Olá utilizados em cada amostra.

## <a name="blob-download"></a>Blob: Transferir
### <a name="download-single-blob"></a>Transferir BLOBs único

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /Pattern:"abc.txt"
```

Tenha em atenção que, se a pasta de Olá `C:\myfolder` não existir, AzCopy irá criá-la e transferir `abc.txt ` na nova pasta de Olá.

### <a name="download-single-blob-from-secondary-region"></a>Transferir BLOBs único da região secundária

```azcopy
AzCopy /Source:https://myaccount-secondary.blob.core.windows.net/mynewcontainer /Dest:C:\myfolder /SourceKey:key /Pattern:abc.txt
```

Tenha em atenção que tem de ter o armazenamento georredundante com acesso de leitura ativado.

### <a name="download-all-blobs"></a>Transferir todos os blobs

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /S
```

Partem do princípio de seguinte Olá residem os blobs no contentor especificado Olá:  

    abc.txt
    abc1.txt
    abc2.txt
    vd1\a.txt
    vd1\abcd.txt

Após a operação de transferência Olá, Olá diretório `C:\myfolder` incluirá Olá os seguintes ficheiros:

    C:\myfolder\abc.txt
    C:\myfolder\abc1.txt
    C:\myfolder\abc2.txt
    C:\myfolder\vd1\a.txt
    C:\myfolder\vd1\abcd.txt

Se não especificar opção `/S`, não existem blobs não serão transferidos.

### <a name="download-blobs-with-specified-prefix"></a>Transferir blobs com o prefixo especificado

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /Pattern:a /S
```

Partem do princípio de seguinte Olá residem os blobs no contentor especificado Olá. Todos os blobs a partir do prefixo de Olá `a` serão transferidos:

    abc.txt
    abc1.txt
    abc2.txt
    xyz.txt
    vd1\a.txt
    vd1\abcd.txt

Após a operação de transferência Olá, Olá pasta `C:\myfolder` incluirá Olá os seguintes ficheiros:

    C:\myfolder\abc.txt
    C:\myfolder\abc1.txt
    C:\myfolder\abc2.txt

prefixo de Olá aplica-se o diretório virtual de toohello, o que faz parte de primeiro Olá do nome do blob Olá. Exemplo de Olá mostrado acima, o diretório virtual Olá não corresponde a prefixo especificado Olá, pelo que não está a ser transferido. Além disso, se hello opção `\S` não for especificado, AzCopy não poderão transferir os blobs.

### <a name="set-hello-last-modified-time-of-exported-files-toobe-same-as-hello-source-blobs"></a>Definir a hora de Olá última modificação de ficheiros exportados toobe igual ao hello blobs de origem

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /MT
```

Também pode excluir os blobs de operação de transferência de Olá com base na respetiva tempo last-modified. Por exemplo, se pretender que os blobs tooexclude cuja hora da última modificação é Olá igual ou mais recente do que o ficheiro de destino Olá, adicionar Olá `/XN` opção:

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /MT /XN
```

Ou se pretender que os blobs tooexclude cuja hora da última modificação é Olá igual ou mais antiga do que o ficheiro de destino Olá, adicione Olá `/XO` opção:

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /MT /XO
```

## <a name="blob-upload"></a>Blob: carregar
### <a name="upload-single-file"></a>Carregar ficheiro único

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /Pattern:"abc.txt"
```

Se Olá o contentor de destino especificado não existe, o AzCopy irá criá-lo e carregar o ficheiro de Olá para a mesma.

### <a name="upload-single-file-toovirtual-directory"></a>Carregar ficheiro único diretório toovirtual

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer/vd /DestKey:key /Pattern:abc.txt
```

Se Olá especificado diretório virtual não existe, o AzCopy carregará Olá tooinclude Olá virtual diretório do ficheiro no respetivo nome (*por exemplo,*, `vd/abc.txt` no exemplo Olá acima).

### <a name="upload-all-files"></a>Carregar todos os ficheiros

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /S
```

Especificar a opção `/S` carregamentos Olá conteúdo Olá especificado diretório tooBlob armazenamento recursiva, o que significa que todas as subpastas e os ficheiros e serão carregados bem. Por exemplo, suponha o seguinte Olá residem os ficheiros na pasta `C:\myfolder`:

    C:\myfolder\abc.txt
    C:\myfolder\abc1.txt
    C:\myfolder\abc2.txt
    C:\myfolder\subfolder\a.txt
    C:\myfolder\subfolder\abcd.txt

Após a operação de carregamento de Olá, contentor Olá irá incluir Olá os seguintes ficheiros:

    abc.txt
    abc1.txt
    abc2.txt
    subfolder\a.txt
    subfolder\abcd.txt

Se não especificar opção `/S`, AzCopy não irá carregar em modo recursivo. Após a operação de carregamento de Olá, contentor Olá irá incluir Olá os seguintes ficheiros:

    abc.txt
    abc1.txt
    abc2.txt

### <a name="upload-files-matching-specified-pattern"></a>Carregar ficheiros correspondentes ao padrão especificado

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /Pattern:a* /S
```

Partem do princípio de seguinte Olá residem os ficheiros na pasta `C:\myfolder`:

    C:\myfolder\abc.txt
    C:\myfolder\abc1.txt
    C:\myfolder\abc2.txt
    C:\myfolder\xyz.txt
    C:\myfolder\subfolder\a.txt
    C:\myfolder\subfolder\abcd.txt

Após a operação de carregamento de Olá, contentor Olá irá incluir Olá os seguintes ficheiros:

    abc.txt
    abc1.txt
    abc2.txt
    subfolder\a.txt
    subfolder\abcd.txt

Se não especificar opção `/S`, AzCopy só irá carregar blobs que não residem num diretório virtual:

    C:\myfolder\abc.txt
    C:\myfolder\abc1.txt
    C:\myfolder\abc2.txt

### <a name="specify-hello-mime-content-type-of-a-destination-blob"></a>Especifique o tipo de conteúdo de MIME de Olá de um blob de destino
Por predefinição, AzCopy define o tipo de conteúdo de Olá de um blob de destino demasiado`application/octet-stream`. A partir da versão 3.1.0, pode explicitamente especificar tipo de conteúdo de Olá através da opção de Olá `/SetContentType:[content-type]`. Esta sintaxe define o tipo de conteúdo de Olá para todos os blobs numa operação de carregamento.

```azcopy
AzCopy /Source:C:\myfolder\ /Dest:https://myaccount.blob.core.windows.net/myContainer/ /DestKey:key /Pattern:ab /SetContentType:video/mp4
```

Se especificar `/SetContentType` sem um valor, em seguida, AzCopy definirá cada blob ou tipo de conteúdo do ficheiro de acordo com tooits extensão de ficheiro.

```azcopy
AzCopy /Source:C:\myfolder\ /Dest:https://myaccount.blob.core.windows.net/myContainer/ /DestKey:key /Pattern:ab /SetContentType
```

## <a name="blob-copy"></a>Blob: cópia
### <a name="copy-single-blob-within-storage-account"></a>Copiar blob único na conta de armazenamento

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer1 /Dest:https://myaccount.blob.core.windows.net/mycontainer2 /SourceKey:key /DestKey:key /Pattern:abc.txt
```

Quando copiar um blob dentro de uma conta de armazenamento, um [cópia do lado do servidor](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) é efetuar a operação.

### <a name="copy-single-blob-across-storage-accounts"></a>Copiar blob único em contas de armazenamento

```azcopy
AzCopy /Source:https://sourceaccount.blob.core.windows.net/mycontainer1 /Dest:https://destaccount.blob.core.windows.net/mycontainer2 /SourceKey:key1 /DestKey:key2 /Pattern:abc.txt
```

Quando copiar um blob em contas de armazenamento, um [cópia do lado do servidor](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) é efetuar a operação.

### <a name="copy-single-blob-from-secondary-region-tooprimary-region"></a>Copiar blob único da região de tooprimary região secundária

```azcopy
AzCopy /Source:https://myaccount1-secondary.blob.core.windows.net/mynewcontainer1 /Dest:https://myaccount2.blob.core.windows.net/mynewcontainer2 /SourceKey:key1 /DestKey:key2 /Pattern:abc.txt
```

Tenha em atenção que tem de ter o armazenamento georredundante com acesso de leitura ativado.

### <a name="copy-single-blob-and-its-snapshots-across-storage-accounts"></a>Copiar blob único e o respetivos instantâneos em contas de armazenamento

```azcopy
    AzCopy /Source:https://sourceaccount.blob.core.windows.net/mycontainer1 /Dest:https://destaccount.blob.core.windows.net/mycontainer2 /SourceKey:key1 /DestKey:key2 /Pattern:abc.txt /Snapshot
```

Após a operação de cópia de Olá, um contentor de destino Olá incluirá blob Olá e respetivos instantâneos. Partindo do princípio de blob Olá no exemplo Olá acima tem dois instantâneos, contentor Olá incluirá seguinte Olá e instantâneos do blob:

    abc.txt
    abc (2013-02-25 080757).txt
    abc (2014-02-21 150331).txt

### <a name="synchronously-copy-blobs-across-storage-accounts"></a>Em sincronia copiar os blobs em contas de armazenamento
AzCopy por predefinição copia dados entre dois pontos finais de armazenamento de forma assíncrona. Por conseguinte, a operação de cópia de Olá será executado em segundo plano Olá utilizando a capacidade de reserva de largura de banda que não tenha nenhum SLA em termos de forma rápida um blob será copiado e AzCopy irá verificar periodicamente o estado da cópia Olá até Olá copiar está concluída ou falhada.

Olá `/SyncCopy` opção garante que a operação de cópia de Olá obterá velocidade consistente. AzCopy efetua a cópia síncrona Olá transferindo blobs Olá toocopy de Olá especificada de memória de toolocal de origem e, em seguida, carregá-los toohello destino de armazenamento de Blobs.

```azcopy
AzCopy /Source:https://myaccount1.blob.core.windows.net/myContainer/ /Dest:https://myaccount2.blob.core.windows.net/myContainer/ /SourceKey:key1 /DestKey:key2 /Pattern:ab /SyncCopy
```

`/SyncCopy`pode gerar saída adicional de custos comparadas tooasynchronous cópia, hello abordagem recomendada é toouse esta opção na VM do Azure que está a ser Olá mesma região que o custo de saída tooavoid de conta de armazenamento de origem.

## <a name="file-download"></a>Ficheiro: Transferir
### <a name="download-single-file"></a>Transferência de ficheiro único

```azcopy
AzCopy /Source:https://myaccount.file.core.windows.net/myfileshare/myfolder1/ /Dest:C:\myfolder /SourceKey:key /Pattern:abc.txt
```

Se Olá especificado origem é uma partilha de ficheiros do Azure, tem de especificar se o nome de ficheiro exato de Olá, (*por exemplo,* `abc.txt`) toodownload um ficheiro único, ou especificar a opção `/S` toodownload todos os ficheiros numa partilha de Olá em modo recursivo. Tentativa de toospecify um padrão de ficheiro e a opção `/S` em conjunto resultará num erro.

### <a name="download-all-files"></a>Transferir todos os ficheiros

```azcopy
AzCopy /Source:https://myaccount.file.core.windows.net/myfileshare/ /Dest:C:\myfolder /SourceKey:key /S
```

Tenha em atenção que não serão transferidas quaisquer pastas vazias.

## <a name="file-upload"></a>Ficheiro: carregar
### <a name="upload-single-file"></a>Carregar ficheiro único

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.file.core.windows.net/myfileshare/ /DestKey:key /Pattern:abc.txt
```

### <a name="upload-all-files"></a>Carregar todos os ficheiros

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.file.core.windows.net/myfileshare/ /DestKey:key /S
```

Tenha em atenção que não serão carregadas qualquer pastas vazias.

### <a name="upload-files-matching-specified-pattern"></a>Carregar ficheiros correspondentes ao padrão especificado

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.file.core.windows.net/myfileshare/ /DestKey:key /Pattern:ab* /S
```

## <a name="file-copy"></a>Ficheiro: cópia
### <a name="copy-across-file-shares"></a>Copiar em partilhas de ficheiros

```azcopy
AzCopy /Source:https://myaccount1.file.core.windows.net/myfileshare1/ /Dest:https://myaccount2.file.core.windows.net/myfileshare2/ /SourceKey:key1 /DestKey:key2 /S
```
Quando copiar um ficheiro através de partilhas de ficheiros, um [cópia do lado do servidor](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) é efetuar a operação.

### <a name="copy-from-file-share-tooblob"></a>Copiar do tooblob de partilha de ficheiros

```azcopy
AzCopy /Source:https://myaccount1.file.core.windows.net/myfileshare/ /Dest:https://myaccount2.blob.core.windows.net/mycontainer/ /SourceKey:key1 /DestKey:key2 /S
```
Quando copiar um ficheiro de tooblob de partilha de ficheiros, um [cópia do lado do servidor](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) é efetuar a operação.


### <a name="copy-from-blob-toofile-share"></a>Copiar de blob toofile partilha

```azcopy
AzCopy /Source:https://myaccount1.blob.core.windows.net/mycontainer/ /Dest:https://myaccount2.file.core.windows.net/myfileshare/ /SourceKey:key1 /DestKey:key2 /S
```
Quando copiar um ficheiro de partilha de toofile de blob, um [cópia do lado do servidor](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) é efetuar a operação.

### <a name="synchronously-copy-files"></a>Em sincronia copiar ficheiros
Pode especificar Olá `/SyncCopy` opção toocopy dados de armazenamento de ficheiros tooFile armazenamento, de armazenamento de ficheiros tooBlob armazenamento e de armazenamento de BLOBs tooFile armazenamento de forma síncrona, AzCopy efetua este procedimento, transferindo Olá origem dados toolocal de memória e carregá-la toodestination novamente. Custo de saída padrão será aplicada.

```azcopy
AzCopy /Source:https://myaccount1.file.core.windows.net/myfileshare1/ /Dest:https://myaccount2.file.core.windows.net/myfileshare2/ /SourceKey:key1 /DestKey:key2 /S /SyncCopy
```

Quando copiar do File Storage tooBlob armazenamento, é de tipo de blob predefinido Olá BLOBs de blocos, o utilizador pode especificar a opção `/BlobType:page` toochange Olá tipo de blob de destino.

Tenha em atenção que `/SyncCopy` poderá gerar a saída adicional custo compara tooasynchronous cópia, hello abordagem recomendada é toouse VM do Azure que está a ser Olá Olá, esta opção na mesma região que o custo de saída tooavoid de conta de armazenamento de origem.

## <a name="table-export"></a>Tabela: Exportar
### <a name="export-table"></a>Tabela de exportação

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/myTable/ /Dest:C:\myfolder\ /SourceKey:key
```

AzCopy escreve uma pasta de destino especificada do ficheiro de manifesto toohello. o ficheiro de manifesto Olá é utilizada nos ficheiros de dados necessários do Olá importação processo toolocate Olá e efetuar a validação de dados. o ficheiro de manifesto Olá utiliza Olá seguinte convenção de nomenclatura por predefinição:

    <account name>_<table name>_<timestamp>.manifest

Utilizador também é possível especificar a opção de Olá `/Manifest:<manifest file name>` nome de ficheiro de manifesto tooset Olá.

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/myTable/ /Dest:C:\myfolder\ /SourceKey:key /Manifest:abc.manifest
```

### <a name="split-export-into-multiple-files"></a>Exportação de divisão em vários ficheiros

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/mytable/ /Dest:C:\myfolder /SourceKey:key /S /SplitSize:100
```

AzCopy utiliza um *índice volume* no Olá dividir dados nomes do ficheiro toodistinguish vários ficheiros. índice de volume Olá consiste em duas partes: um *índice de intervalos de chave de partição* e um *divisão ficheiro índice*. Ambos os índices são baseado em zero.

índice de intervalos de chave de partição de Olá será 0 se o utilizador especificar a opção `/PKRS`.

Por exemplo, suponha que AzCopy gera dois ficheiros de dados depois do utilizador de Olá Especifica opção `/SplitSize`. poderá ser Olá resultante nomes de ficheiro de dados:

    myaccount_mytable_20140903T051850.8128447Z_0_0_C3040FE8.json
    myaccount_mytable_20140903T051850.8128447Z_0_1_0AB9AC20.json

Tenha em atenção que Olá valor mínimo possível para a opção `/SplitSize` é 32 MB. Se Olá especificado destino for o Blob storage, o AzCopy irá dividir o ficheiro de dados de Olá uma vez a limitação de tamanho de blob na Olá de atingir tamanhos (200GB), independentemente da opção se `/SplitSize` foi especificado pelo utilizador Olá.

### <a name="export-table-toojson-or-csv-data-file-format"></a>Exportar tooJSON de tabela ou o formato de ficheiro de dados CSV
AzCopy por predefinição exporta os ficheiros de dados de tooJSON tabelas. Pode especificar a opção de Olá `/PayloadFormat:JSON|CSV` tabelas de Olá tooexport como JSON ou CSV.

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/myTable/ /Dest:C:\myfolder\ /SourceKey:key /PayloadFormat:CSV
```

Durante a especificação de formato de payload Olá CSV, o AzCopy também irá gerar um ficheiro de esquema com a extensão de ficheiro `.schema.csv` para cada ficheiro de dados.

### <a name="export-table-entities-concurrently"></a>Exportar as entidades da tabela em simultâneo

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/myTable/ /Dest:C:\myfolder\ /SourceKey:key /PKRS:"aa#bb"
```

AzCopy iniciará entidades de tooexport operações simultâneas, quando o utilizador de Olá Especifica opção `/PKRS`. Cada operação exporta um intervalo de chave de partição.

Tenha em atenção que o número de Olá de operações simultâneas também é controlado pela opção `/NC`. AzCopy utiliza o número de Olá de processadores de núcleo como valor predefinido Olá `/NC` quando copiar as entidades da tabela, mesmo se `/NC` não foi especificado. Quando o utilizador Olá Especifica opção `/PKRS`, AzCopy utiliza Olá mais pequenos de Olá dois valores - partição intervalos de chaves versus operações simultâneas implícita ou explicitamente especificados - toodetermine Olá número toostart operações simultâneas. Para obter mais detalhes, escreva `AzCopy /?:NC` na linha de comandos Olá.

### <a name="export-table-tooblob"></a>Exportar a tabela tooblob

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/myTable/ /Dest:https://myaccount.blob.core.windows.net/mycontainer/ /SourceKey:key1 /Destkey:key2
```

AzCopy irá gerar um ficheiro de dados JSON no contentor de BLOBs de Olá com a seguinte convenção de nomenclatura:

    <account name>_<table name>_<timestamp>_<volume index>_<CRC>.json

ficheiro de dados JSON Olá gerado segue o formato de payload Olá para metadados mínimo. Para obter detalhes sobre este formato de payload, consulte [formato de Payload para operações de serviço tabela](http://msdn.microsoft.com/library/azure/dn535600.aspx).

Tenha em atenção que ao exportar tooblobs de tabelas, AzCopy irá transferir Olá tabela entidades toolocal temporário os ficheiros de dados e, em seguida, carregue os BLOBs de toohello entidades. Estes ficheiros de dados temporária são colocados de pasta do ficheiro de Olá diário de alterações com o caminho predefinido de Olá "<code>%LocalAppData%\Microsoft\Azure\AzCopy</code>", pode especificar a opção/z [pasta de ficheiros de diário] toochange Olá localização de pasta de ficheiros do diário de alterações e, por conseguinte, altere a localização de ficheiros de dados temporária de Olá. Olá dados temporários tamanho dos ficheiros é decidido ao tamanho e tamanho de Olá que especificou com Olá opção /SplitSize, as entidades da tabela, apesar do ficheiro de dados temporária de Olá no disco local será eliminado de forma instantânea depois de ter sido carregado toohello blob, certifique-se antes de ter suficiente toostore de espaço em disco local estes ficheiros de dados temporária estes sejam eliminados.

## <a name="table-import"></a>Tabela: importação
### <a name="import-table"></a>Tabela importar

```azcopy
AzCopy /Source:C:\myfolder\ /Dest:https://myaccount.table.core.windows.net/mytable1/ /DestKey:key /Manifest:"myaccount_mytable_20140103T112020.manifest" /EntityOperation:InsertOrReplace
```

Olá opção `/EntityOperation` indica como tooinsert entidades para Olá tabela. Os valores possíveis são:

* `InsertOrSkip`: Ignora a uma entidade existente ou introduza uma nova entidade se não existir na tabela de Olá.
* `InsertOrMerge`: Intercala uma entidade existente ou introduza uma nova entidade se não existir na tabela de Olá.
* `InsertOrReplace`: Substitui uma entidade existente ou introduza uma nova entidade se não existir na tabela de Olá.

Tenha em atenção que não é possível especificar a opção `/PKRS` num cenário de importação de Olá. Ao contrário do cenário de exportação de Olá, na qual tem de especificar a opção `/PKRS` toostart de operações simultâneas, AzCopy por predefinição iniciará operações simultâneas quando importar uma tabela. Olá predefinição o número de operações simultâneas iniciado é toohello igual número de processadores de núcleo No entanto, pode especificar um número diferente de em simultâneo com a opção `/NC`. Para obter mais detalhes, escreva `AzCopy /?:NC` na linha de comandos Olá.

Tenha em atenção que AzCopy só suporta a importação para JSON, CSV não. AzCopy não suporta importações de tabela JSON criados pelo utilizador e os ficheiros de manifesto. Ambos estes ficheiros têm de ser provenientes uma exportação de tabela do AzCopy. erros de tooavoid, não modifique Olá exportado JSON ou o ficheiro de manifesto.

### <a name="import-entities-tootable-using-blobs"></a>Entidades de importação tootable utilizar blobs
Assuma um contentor do Blob contém seguinte Olá: ficheiro de um JSON que representam uma tabela do Azure e o respetivo ficheiro de manifesto associado.

    myaccount_mytable_20140103T112020.manifest
    myaccount_mytable_20140103T112020_0_0_0AF395F1DC42E952.json

Pode executar Olá seguintes entidades do comando tooimport para uma tabela com o ficheiro de manifesto Olá nesse contentor de blob:

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:https://myaccount.table.core.windows.net/mytable /SourceKey:key1 /DestKey:key2 /Manifest:"myaccount_mytable_20140103T112020.manifest" /EntityOperation:"InsertOrReplace"
```

## <a name="other-azcopy-features"></a>Outras funcionalidades do AzCopy
### <a name="only-copy-data-that-doesnt-exist-in-hello-destination"></a>Apenas os dados de cópia que não existem no destino Olá
Olá `/XO` e `/XN` parâmetros permitem tooexclude recursos de origem de anterior ou mais recente de ser copiado, respetivamente. Se pretender apenas toocopy recursos de origem que não existem no destino Olá, pode especificar os dois parâmetros na Olá comandos do AzCopy:

    /Source:http://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:<sourcekey> /S /XO /XN

    /Source:C:\myfolder /Dest:http://myaccount.file.core.windows.net/myfileshare /DestKey:<destkey> /S /XO /XN

    /Source:http://myaccount.blob.core.windows.net/mycontainer /Dest:http://myaccount.blob.core.windows.net/mycontainer1 /SourceKey:<sourcekey> /DestKey:<destkey> /S /XO /XN

Tenha em atenção que isto não é suportado quando Olá origem ou de destino é uma tabela.

### <a name="use-a-response-file-toospecify-command-line-parameters"></a>Utilize um toospecify de ficheiro de resposta para parâmetros de linha de comandos

```azcopy
AzCopy /@:"C:\responsefiles\copyoperation.txt"
```

Pode incluir quaisquer parâmetros de linha de comandos do AzCopy num ficheiro de resposta. Processos do AzCopy Olá parâmetros no ficheiro de Olá como se tivesse sido especificados na linha de comandos Olá, efetuar uma substituição direta com conteúdo Olá do ficheiro de Olá.

Partem do princípio de um ficheiro de resposta com o nome `copyoperation.txt`, que contém Olá seguintes linhas. Cada parâmetro do AzCopy pode ser especificado numa única linha

    /Source:http://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:<sourcekey> /S /Y

ou, no separar linhas:

    /Source:http://myaccount.blob.core.windows.net/mycontainer
    /Dest:C:\myfolder
    /SourceKey:<sourcekey>
    /S
    /Y

AzCopy irá falhar se dividir parâmetro Olá por duas linhas, conforme mostrado aqui para Olá `/sourcekey` parâmetro:

    http://myaccount.blob.core.windows.net/mycontainer
     C:\myfolder
    /sourcekey:
    <sourcekey>
    /S
    /Y

### <a name="use-multiple-response-files-toospecify-command-line-parameters"></a>Utilizar vários ficheiros toospecify da linha de comandos parâmetros de resposta
Partem do princípio de um ficheiro de resposta com o nome `source.txt` que especifica um contentor de origem:

    /Source:http://myaccount.blob.core.windows.net/mycontainer

E um ficheiro de resposta com o nome `dest.txt` que especifica uma pasta de destino no sistema de ficheiros de Olá:

    /Dest:C:\myfolder

E um ficheiro de resposta com o nome `options.txt` que especifica as opções para AzCopy:

    /S /Y

toocall AzCopy com estes ficheiros de resposta, todos os que residem num diretório `C:\responsefiles`, utilize este comando:

```azcopy
AzCopy /@:"C:\responsefiles\source.txt" /@:"C:\responsefiles\dest.txt" /SourceKey:<sourcekey> /@:"C:\responsefiles\options.txt"   
```

AzCopy processa este comando, tal como se de que incluiu todos os parâmetros de individuais Olá na linha de comandos Olá:

```azcopy
AzCopy /Source:http://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:<sourcekey> /S /Y
```

### <a name="specify-a-shared-access-signature-sas"></a>Especifique uma assinatura de acesso partilhado (SAS)

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer1 /Dest:https://myaccount.blob.core.windows.net/mycontainer2 /SourceSAS:SAS1 /DestSAS:SAS2 /Pattern:abc.txt
```

Também pode especificar uma SAS no contentor de Olá URI:

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer1/?SourceSASToken /Dest:C:\myfolder /S
```

### <a name="journal-file-folder"></a>Pasta de ficheiros do diário de alterações
Sempre que emitir um comando tooAzCopy, este verifica se existe um ficheiro de diário de alterações na pasta predefinida de hello, ou se existe uma pasta que especificou através desta opção. Se não existir um ficheiro do diário de alterações de Olá em qualquer local, o AzCopy trata operação Olá como novo e gera um novo ficheiro de diário de alterações.

Se existirem ficheiros do diário de alterações de Olá, AzCopy irá verificar se linha de comandos de Olá introduzido corresponde a linha de comandos Olá no ficheiro de diário Olá. Se duas linhas de comando Olá corresponderem, o AzCopy retoma operação incompleta Olá. Se não corresponderem, será pedido tooeither substituir Olá diário ficheiro toostart uma operação de novo ou toocancel Olá operação atual.

Se pretender que a localização predefinida de Olá de toouse para o ficheiro do diário de alterações de Olá:

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /Z
```

Se omitir opção `/Z`, ou especificar a opção `/Z` sem o caminho da pasta Olá, conforme mostrado acima, o AzCopy cria Olá diário ficheiro na localização predefinida de Olá, que é `%SystemDrive%\Users\%username%\AppData\Local\Microsoft\Azure\AzCopy`. Se já existir um ficheiro do diário de alterações de Olá, o AzCopy retoma operação Olá com base num ficheiro do diário de alterações de Olá.

Se quiser toospecify numa localização personalizada para o ficheiro do diário de alterações de Olá:

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /Z:C:\journalfolder\
```

Este exemplo cria ficheiros do diário de alterações de Olá se já existir. Se existir, o AzCopy retoma operação Olá com base num ficheiro do diário de alterações de Olá.

Se quiser tooresume uma operação do AzCopy:

```azcopy
AzCopy /Z:C:\journalfolder\
```

Neste exemplo retoma Olá última operação, que pode não ter conseguido toocomplete.

### <a name="generate-a-log-file"></a>Gerar um ficheiro de registo

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /V
```

Se especificar a opção `/V` sem fornecer um registo verboso do caminho toohello de ficheiros, em seguida, AzCopy cria Olá ficheiro de registo na localização predefinida de Olá, que é `%SystemDrive%\Users\%username%\AppData\Local\Microsoft\Azure\AzCopy`.

Caso contrário, pode criar um ficheiro de registo numa localização personalizada:

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /V:C:\myfolder\azcopy1.log
```

Tenha em atenção que se especificar um caminho relativo a seguinte opção `/V`, tais como `/V:test/azcopy1.log`, em seguida, o registo verboso Olá é criado na Olá atual diretório de trabalho dentro de uma subpasta denominada `test`.

### <a name="specify-hello-number-of-concurrent-operations-toostart"></a>Especifique o número de Olá de operações simultâneas toostart
Opção `/NC` Especifica o número de Olá de operações de cópia em simultâneo. Por predefinição, o AzCopy é iniciado um determinado número de débito de transferência de dados de Olá tooincrease operações simultâneas. Para operações de tabela, o número de Olá de operações simultâneas é toohello igual número de processadores que tem. Para operações de Blob e o ficheiro, número de Olá de operações simultâneas de é igual número de Olá de 8 horas de processadores que tem. Se estiver a executar o AzCopy através de uma rede de largura de banda reduzida, pode especificar um número inferior de falha de tooavoid /NC causado por concorrência de recursos.

### <a name="run-azcopy-against-azure-storage-emulator"></a>Executar o AzCopy no emulador do Storage do Azure
Pode executar o AzCopy contra Olá [emulador do Storage do Azure](storage-use-emulator.md) para Blobs:

```azcopy
AzCopy /Source:https://127.0.0.1:10000/myaccount/mycontainer/ /Dest:C:\myfolder /SourceKey:key /SourceType:Blob /S
```

e tabelas:

```azcopy
AzCopy /Source:https://127.0.0.1:10002/myaccount/mytable/ /Dest:C:\myfolder /SourceKey:key /SourceType:Table
```

## <a name="azcopy-parameters"></a>Parâmetros do AzCopy
Parâmetros para AzCopy são descritos abaixo. Também pode escrever um dos Olá Olá linha de comandos para obter ajuda utilizando o AzCopy para os seguintes comandos:

* Para obter ajuda detalhada da linha de comandos do AzCopy:`AzCopy /?`
* Para obter ajuda detalhada com quaisquer parâmetros de AzCopy:`AzCopy /?:SourceKey`
* Para obter exemplos da linha de comandos:`AzCopy /?:Samples`

### <a name="sourcesource"></a>/ De origem: "origem"
Especifica a origem de dados Olá do qual toocopy. origem de Olá pode ser um diretório do sistema de ficheiros, um contentor de blob, um diretório virtual de blob, uma partilha de ficheiros de armazenamento, um diretório do ficheiro de armazenamento ou uma tabela do Azure.

**Aplica-se a:** Blobs, ficheiros, tabelas

### <a name="destdestination"></a>/ Dest: "destino"
Especifica Olá toocopy de destino para. destino de Olá pode ser um diretório do sistema de ficheiros, um contentor de blob, um diretório virtual de blob, uma partilha de ficheiros de armazenamento, um diretório do ficheiro de armazenamento ou uma tabela do Azure.

**Aplica-se a:** Blobs, ficheiros, tabelas

### <a name="patternfile-pattern"></a>/ Padrão: "-padrão de ficheiros"
Especifica um padrão de ficheiro que indica que toocopy de ficheiros. comportamento de Olá do parâmetro de /Pattern Olá é determinado por localização Olá Olá de dados de origem e a presença de Olá da opção de modo recursivo Olá. Modo recursivo é especificado através da opção /S.

Se origem especificada Olá for um diretório no sistema de ficheiros de Olá, carateres universais padrão estão em vigor e especificar um padrão de ficheiro Olá é comparado com ficheiros dentro do diretório de Olá. Se a opção que /s for especificado, em seguida, AzCopy também corresponde ao padrão especificado de Olá contra todos os ficheiros em subpastas abaixo diretório Olá.

Se a origem especificada Olá é um contentor de blob ou um diretório virtual, caracteres universais não são aplicadas. Se a opção que /s for especificado, em seguida, AzCopy interpreta padrão de ficheiro especificado Olá como um prefixo de blob. Se a opção que /s não for especificado, em seguida, AzCopy corresponde ao padrão de ficheiro Olá contra dos nomes blob exato.

Se Olá especificado origem é uma partilha de ficheiros do Azure, tem de especificar ou nome de ficheiro exato de Olá, (por exemplo, abc.txt) toocopy um ficheiro único, ou especificar a opção /S toocopy todos os ficheiros na partilha de Olá em modo recursivo. Tentativa de toospecify um padrão de ficheiro e a opção /S em conjunto resultará num erro.

AzCopy utiliza a correspondência de maiúsculas e minúsculas quando Olá /Source é um contentor de blob ou um diretório virtual de blob e Olá, utiliza sensível correspondentes em todos os outros casos.

Olá ficheiro padrão predefinido utilizado quando não é especificada nenhuma padrão de ficheiro é *.* para uma localização de ficheiros de sistema ou um prefixo vazio para uma localização de armazenamento do Azure. Especificar vários padrões de ficheiro não é suportada.

**Aplica-se a:** Blobs, ficheiros

### <a name="destkeystorage-key"></a>/ DestKey: "chave de armazenamento"
Especifica a chave de conta do storage Olá para o recurso de destino Olá.

**Aplica-se a:** Blobs, ficheiros, tabelas

### <a name="destsassas-token"></a>/ DestSAS: "sas token"
Especifica uma assinatura de acesso partilhado (SAS) com permissões de leitura e escrita para o destino de Olá (se aplicável). Coloque Olá SAS com aspas, como pode contém carateres especiais de linha de comandos.

Se o recurso de destino de Olá for um contentor de blob, a partilha de ficheiros ou a tabela, pode especificar esta opção seguida de token SAS de hello, ou pode especificar Olá SAS como parte do contentor de blob de destino Olá, partilha de ficheiros ou URI da tabela, sem esta opção.

Se Olá origem e destino estão ambos os blobs e BLOBs de destino Olá têm de residir no Olá mesmo a conta de armazenamento como blob de origem Olá.

**Aplica-se a:** Blobs, ficheiros, tabelas

### <a name="sourcekeystorage-key"></a>/ SourceKey: "chave de armazenamento"
Especifica a chave de conta do storage Olá para o recurso de origem Olá.

**Aplica-se a:** Blobs, ficheiros, tabelas

### <a name="sourcesassas-token"></a>/ SourceSAS: "sas token"
Especifica uma assinatura de acesso partilhado com permissões de leitura e de lista para a origem de Olá (se aplicável). Coloque Olá SAS com aspas, como pode contém carateres especiais de linha de comandos.

Se recursos de origem Olá é um contentor de blob e não uma chave nem uma SAS é fornecida, será possível ler o contentor do blob Olá através do acesso anónimo.

Se a origem Olá é uma partilha de ficheiros ou tabela, tem de ser fornecida uma chave ou uma SAS.

**Aplica-se a:** Blobs, ficheiros, tabelas

### <a name="s"></a>/S
Especifica o modo recursivo para operações de cópia. No modo de recursiva, o AzCopy vai copiar todos os blobs ou ficheiros que correspondam ao padrão de ficheiro especificado Olá, incluindo as existentes na subpastas.

**Aplica-se a:** Blobs, ficheiros

### <a name="blobtypeblock--page--append"></a>/ BlobType: "bloquear" | "página" | "acrescentar"
Especifica se o blob de destino Olá é um blob de blocos, um blob de página ou um blob de acréscimo. Esta opção é aplicável apenas quando estiver a carregar um blob. Caso contrário, é gerado um erro. Se o destino de Olá é um blob e esta opção não for especificada, por predefinição, o AzCopy cria um blob de blocos.

**Aplica-se a:** Blobs

### <a name="checkmd5"></a>/ CheckMD5
Calcula um hash MD5 para dados transferidos e verifica se o hash MD5 de Olá armazenados no blob Olá ou propriedade de conteúdo-MD5 do ficheiro corresponda ao hash de Olá calculado. verificação de Olá MD5 está desativada por predefinição, pelo que tem de especificar esta verificação de MD5 opção tooperform Olá quando a transferência de dados.

Tenha em atenção que o armazenamento do Azure não garante que Olá hash MD5 para BLOBs Olá ou o ficheiro está atualizado. É Olá de tooupdate de responsabilidade do cliente MD5 sempre que o blob Olá ou o ficheiro é modificado.

AzCopy sempre define Olá Content-MD5 propriedade para um blob do Azure ou o ficheiro após carregá-lo toohello serviço.  

**Aplica-se a:** Blobs, ficheiros

### <a name="snapshot"></a>/ Instantâneo de
Indica se tootransfer instantâneos. Esta opção só é válida quando a origem de Olá é um blob.

Olá instantâneos do blob transferidos são mudados neste formato: nome do blob (hora de instantâneo) .extension

Por predefinição, os instantâneos não são copiados.

**Aplica-se a:** Blobs

### <a name="vverbose-log-file"></a>/ V: [verboso--ficheiro de registo]
Saídas verboso as mensagens de estado para um ficheiro de registo.

Por predefinição, o ficheiro de registo verboso Olá é denominado AzCopyVerbose.log no `%LocalAppData%\Microsoft\Azure\AzCopy`. Se especificar uma localização de ficheiros existentes para esta opção, o registo verboso Olá será anexado toothat ficheiro.  

**Aplica-se a:** Blobs, ficheiros, tabelas

### <a name="zjournal-file-folder"></a>/ Z [pasta de ficheiros de diário]
Especifica uma pasta de ficheiros do diário de alterações para retomar uma operação.

AzCopy suporta sempre retomar se uma operação foi interrompida.

Se esta opção não for especificada, ou se for especificado sem um caminho de pasta, o AzCopy criar ficheiros do diário de alterações de Olá na localização predefinida de Olá, que é % LocalAppData%\Microsoft\Azure\AzCopy.

Sempre que emitir um comando tooAzCopy, este verifica se existe um ficheiro de diário de alterações na pasta predefinida de hello, ou se existe uma pasta que especificou através desta opção. Se não existir um ficheiro do diário de alterações de Olá em qualquer local, o AzCopy trata operação Olá como novo e gera um novo ficheiro de diário de alterações.

Se existirem ficheiros do diário de alterações de Olá, AzCopy irá verificar se linha de comandos de Olá introduzido corresponde a linha de comandos Olá no ficheiro de diário Olá. Se duas linhas de comando Olá corresponderem, o AzCopy retoma operação incompleta Olá. Se não corresponderem, será pedido tooeither substituir Olá diário ficheiro toostart uma operação de novo ou toocancel Olá operação atual.

ficheiros do diário de alterações de Olá é eliminado após a conclusão com êxito da operação de Olá.

Tenha em atenção que a retomar a uma operação a partir de um ficheiro de diário criada por uma versão anterior do AzCopy não é suportada.

**Aplica-se a:** Blobs, ficheiros, tabelas

### <a name="parameter-file"></a>/@:"Parameter-File"
Especifica um ficheiro que contém os parâmetros. Processos do AzCopy Olá parâmetros no ficheiro de Olá como se tivesse sido especificados na linha de comandos Olá.

No ficheiro de resposta, pode especificar vários parâmetros numa única linha, ou especifique cada parâmetro na sua própria linha. Tenha em atenção que um parâmetro individuais não pode abranger várias linhas.

Ficheiros de resposta podem incluir as linhas de comentários que começam com o símbolo de # Olá.

Pode especificar vários ficheiros de resposta. No entanto, tenha em atenção que não suporta o AzCopy aninhadas ficheiros de resposta.

**Aplica-se a:** Blobs, ficheiros, tabelas

### <a name="y"></a>/Y
Suprime todos os pedidos de confirmação do AzCopy.

**Aplica-se a:** Blobs, ficheiros, tabelas

### <a name="l"></a>/L
Especifica uma operação de listagem apenas; Não existem dados são copiados.

AzCopy será interpretar Olá utilizando esta opção como uma simulação de linha de comandos Olá em execução sem esta opção /L e contagem de objetos quantos serão copiados, pode especificar a opção /V em Olá mesmo toocheck quais os objetos que serão copiados no registo verboso Olá de tempo.

comportamento de Olá desta opção também é determinado por localização Olá Olá de dados de origem e de presença Olá Olá recursiva modo opção /S e de ficheiros padrão opção /Pattern.

AzCopy necessita da permissão de LISTAGEM e de leitura desta localização de origem ao utilizar esta opção.

**Aplica-se a:** Blobs, ficheiros

### <a name="mt"></a>/MT
Define toobe Olá mesmo como blob de origem hello ou do ficheiro da hora da última modificação do ficheiro Olá transferido.

**Aplica-se a:** Blobs, ficheiros

### <a name="xn"></a>/XN
Exclui um recurso de origem mais recente. recurso de Olá não será copiado esteja hello hora da última modificação da origem de Olá Olá igual ou mais recente do que o destino.

**Aplica-se a:** Blobs, ficheiros

### <a name="xo"></a>/XO
Exclui um recurso de origem de anterior. recurso de Olá não será copiado esteja hello hora da última modificação da origem de Olá Olá igual ou anterior ao destino.

**Aplica-se a:** Blobs, ficheiros

### <a name="a"></a>/A
Carrega apenas os ficheiros que têm o atributo de arquivo de Olá definido.

**Aplica-se a:** Blobs, ficheiros

### <a name="iarashcnetoi"></a>/ IA: [RASHCNETOI]
Carrega apenas os ficheiros com qualquer um dos Olá especificar o conjunto de atributos.

Os atributos disponíveis incluem:

* R = ficheiros só de leitura
* A = ficheiros prontos para arquivar
* S = ficheiros de sistema
* H = Hidden ficheiros
* C = Compressed ficheiros
* N = ficheiros Normal
* I = ficheiros encriptados
* T = ficheiros temporários
* O = ficheiros Offline
* Posso = indexado não ficheiros

**Aplica-se a:** Blobs, ficheiros

### <a name="xarashcnetoi"></a>/ XA: [RASHCNETOI]
Exclui ficheiros com qualquer um dos Olá especificado conjunto de atributos.

Os atributos disponíveis incluem:

* R = ficheiros só de leitura
* A = ficheiros prontos para arquivar
* S = ficheiros de sistema
* H = Hidden ficheiros
* C = Compressed ficheiros
* N = ficheiros Normal
* I = ficheiros encriptados
* T = ficheiros temporários
* O = ficheiros Offline
* Posso = indexado não ficheiros

**Aplica-se a:** Blobs, ficheiros

### <a name="delimiterdelimiter"></a>/ Delimitador: "delimiter"
Indica o caráter delimitador de Olá utilizado toodelimit de diretórios virtuais num nome de blob.

Por predefinição, utiliza AzCopy / como caráter de delimitador Olá. No entanto, o AzCopy suporta a utilização de qualquer caráter comuns (por exemplo, @, # ou %) como um delimitador. Se precisar de tooinclude um destes carateres especiais na linha de comandos Olá, coloque o nome de ficheiro Olá com aspas duplas.

Esta opção só é aplicável para transferir blobs.

**Aplica-se a:** Blobs

### <a name="ncnumber-of-concurrent-operations"></a>/ NC: "número-de-em simultâneo-operações de"
Especifica o número de Olá de operações simultâneas.

AzCopy por predefinição é iniciado um determinado número de débito de transferência de dados de Olá tooincrease operações simultâneas. Tenha em atenção que grande número de operações simultâneas num ambiente de largura de banda baixa pode sobrecarregar a ligação de rede Olá e impedir operações Olá totalmente conclusão. Limitar operações simultâneas com base na largura de banda disponível real.

limite superior de Olá para operações simultâneas é 512.

**Aplica-se a:** Blobs, ficheiros, tabelas

### <a name="sourcetypeblob--table"></a>/ SourceType: "Blob" | "Tabela"
Especifica que Olá `source` recursos é um blob disponível no ambiente de desenvolvimento local Olá, em execução no emulador do storage Olá.

**Aplica-se a:** Blobs, tabelas

### <a name="desttypeblob--table"></a>/ DestType: "Blob" | "Tabela"
Especifica que Olá `destination` recursos é um blob disponível no ambiente de desenvolvimento local Olá, em execução no emulador do storage Olá.

**Aplica-se a:** Blobs, tabelas

### <a name="pkrskey1key2key3"></a>/ PKRS: "key&#1;key&#2;key&#3;..."
Divisões Olá tooenable de intervalo de chaves de partição exportar dados de tabela em paralelo, o que aumenta a velocidade de Olá Olá da operação de exportação.

Se esta opção não for especificada, o AzCopy utiliza entidades de tabela de tooexport um único thread. Por exemplo, se hello o utilizador Especifica /PKRS: "aa #bb", em seguida, AzCopy inicia três operações simultâneas.

Cada operação exporta um dos três intervalos de chaves de partição, conforme mostrado abaixo:

  [chave de partição primeiro, aa)

  [aa, bb)

  [bb, chave de partição último]

**Aplica-se a:** tabelas

### <a name="splitsizefile-size"></a>/ SplitSize: "tamanho de ficheiro"
Especifica Olá ficheiro exportado dividir tamanho em MB, valor mínimo de Olá permitido é 32.

Se esta opção não for especificada, o AzCopy irá exportar ficheiro de toosingle de dados de tabela.

Se os dados da tabela Olá são exportado tooa blob e hello tamanho do ficheiro exportado atinge Olá 200 GB limite de tamanho do blob, em seguida, AzCopy dividir ficheiro exportado Olá, mesmo se esta opção não está especificada.

**Aplica-se a:** tabelas

### <a name="entityoperationinsertorskip--insertormerge--insertorreplace"></a>/ EntityOperation: "InsertOrSkip" | "InsertOrMerge" | "InsertOrReplace"
Especifica o comportamento Olá da importação de dados de tabela.

* InsertOrSkip - ignora a uma entidade existente ou introduza uma nova entidade se não existir na tabela de Olá.
* InsertOrMerge - intercala uma entidade existente ou introduza uma nova entidade se não existir na tabela de Olá.
* InsertOrReplace - substitui uma entidade existente ou introduza uma nova entidade se não existir na tabela de Olá.

**Aplica-se a:** tabelas

### <a name="manifestmanifest-file"></a>/ Manifesto: "ficheiro de manifesto"
Especifica o ficheiro de manifesto Olá de tabela Olá exportar e importar a operação.

Esta opção é opcional durante a operação de exportação de Olá, AzCopy irá gerar um ficheiro de manifesto com o nome predefinido se esta opção não for especificada.

Esta opção é necessária durante a operação de importação de Olá para localizar ficheiros de dados de Olá.

**Aplica-se a:** tabelas

### <a name="synccopy"></a>/ SyncCopy
Indica se toosynchronously copiar blobs ou ficheiros entre dois pontos finais de armazenamento do Azure.

AzCopy por predefinição utiliza cópia assíncrona do lado do servidor. Especifique este tooperform opção um síncrona copiar, que transfere os blobs ou ficheiros toolocal memória e, em seguida, carrega-os tooAzure armazenamento.

Pode utilizar esta opção quando copiar os ficheiros dentro do armazenamento de BLOBs no armazenamento de ficheiros ou a partir do Blob storage tooFile armazenamento ou vice-versa se.

**Aplica-se a:** Blobs, ficheiros

### <a name="setcontenttypecontent-type"></a>/ SetContentType: "content-type"
Especifica o tipo de conteúdo de MIME de Olá para blobs de destino ou os ficheiros.

Conjuntos de AzCopy Olá o tipo de conteúdo para um blob ou ficheiro tooapplication/octet-stream por predefinição. Pode definir o tipo de conteúdo de Olá para todos os blobs ou ficheiros especificando explicitamente um valor para esta opção.

Se especificar esta opção sem um valor, em seguida, AzCopy definirá cada blob ou tipo de conteúdo do ficheiro de acordo com tooits extensão de ficheiro.

**Aplica-se a:** Blobs, ficheiros

### <a name="payloadformatjson--csv"></a>/ PayloadFormat: "JSON" | "CSV"
Especifica o formato de Olá do ficheiro de dados exportados Olá tabela.

Se esta opção não for especificada, por predefinição, AzCopy exporta ficheiro de dados de tabela no formato JSON.

**Aplica-se a:** tabelas

## <a name="known-issues-and-best-practices"></a>Problemas conhecidos e melhores práticas
### <a name="limit-concurrent-writes-while-copying-data"></a>Limitar escritas em simultâneo ao copiar dados
Quando copia blobs ou ficheiros com o AzCopy, tenha em atenção que outra aplicação pode ser modificar Olá dados enquanto estiver a copiar. Se for possível, certifique-se de que os dados de Olá que estiver a copiar não está a ser modificados durante a operação de cópia de Olá. Por exemplo, quando copiar um VHD associado uma máquina virtual do Azure, certifique-se de que não existem outras aplicações atualmente estiver a escrever toohello VHD. Uma boa forma toodo trata por leasing Olá recursos toobe copiado. Em alternativa, pode criar um instantâneo do VHD de Olá primeiro e, em seguida, copiar o instantâneo de Olá.

Se não podem impedir outras aplicações de escrever tooblobs ou ficheiros, enquanto que estão a ser copiados, em seguida, tenha em atenção que, pela tarefa de Olá Olá tempo é concluída, hello recursos copiados podem já não ter paridade completa com recursos de origem Olá.

### <a name="run-one-azcopy-instance-on-one-machine"></a>Execute uma instância do AzCopy num computador.
O AzCopy é concebida toomaximize Olá utilização sua máquina recursos tooaccelerate Olá da transferência de dados, recomendamos que execute apenas uma instância do AzCopy num computador e especificar a opção de Olá `/NC` se precisar de mais simultâneas operações. Para obter mais detalhes, escreva `AzCopy /?:NC` na linha de comandos Olá.

### <a name="enable-fips-compliant-md5-algorithms-for-azcopy-when-you-use-fips-compliant-algorithms-for-encryption-hashing-and-signing"></a>Ativar os algoritmos de MD5 compatíveis com FIPS para AzCopy quando a "utilização FIPS algoritmos compatíveis com para encriptação, hashing e iniciar sessão".
AzCopy por predefinição utiliza Olá de toocalculate de implementação do .NET MD5 MD5 quando copiar objetos, mas existem alguns requisitos de segurança que precisam de definição de MD5 AzCopy tooenable FIPS em conformidade.

Pode criar um ficheiro App. config `AzCopy.exe.config` com a propriedade `AzureStorageUseV1MD5` e colocá-la reserve com AzCopy.exe.

    <?xml version="1.0" encoding="utf-8" ?>
    <configuration>
      <appSettings>
        <add key="AzureStorageUseV1MD5" value="false"/>
      </appSettings>
    </configuration>

Para a propriedade "AzureStorageUseV1MD5" • verdadeiro - valor predefinido de Olá, AzCopy utilizará .NET MD5 implementação.
• False – AzCopy utilizará MD5 algoritmo de conformidade FIPS.

Tenha em atenção que algoritmos compatíveis com FIPS está desativada por predefinição no seu computador Windows, pode escrever secpol.msc a janela de execução e verifique este comutador na definição de segurança -> Políticas locais -> segurança Opções -> criptografia de sistema: algoritmos compatíveis com utilização FIPS para encriptação, hashing e iniciar sessão.

## <a name="next-steps"></a>Passos seguintes
Para obter mais informações sobre o Storage do Azure e AzCopy, consulte toohello os seguintes recursos.

### <a name="azure-storage-documentation"></a>Documentação do Storage do Azure:
* [Introdução tooAzure armazenamento](storage-introduction.md)
* [Como toouse Blob storage do .NET](storage-dotnet-how-to-use-blobs.md)
* [Como toouse File storage do .NET](storage-dotnet-how-to-use-files.md)
* [Como toouse Table storage do .NET](storage-dotnet-how-to-use-tables.md)
* [Como toocreate, gerir ou eliminar uma conta de armazenamento](storage-create-storage-account.md)
* [Transferência de dados com o AzCopy no Linux](storage-use-azcopy-linux.md)

### <a name="azure-storage-blog-posts"></a>Mensagens de blogue de armazenamento do Azure:
* [Introdução ao pré-visualização de biblioteca de movimento de dados de armazenamento do Azure](https://azure.microsoft.com/blog/introducing-azure-storage-data-movement-library-preview-2/)
* [AzCopy: Introdução ao copiar síncrona e tipo de conteúdo personalizado](http://blogs.msdn.com/b/windowsazurestorage/archive/2015/01/13/azcopy-introducing-synchronous-copy-and-customized-content-type.aspx)
* [AzCopy: Anunciar disponibilidade geral do 3.0 AzCopy plus versão de pré-visualização do AzCopy 4.0 com suporte de tabela e ficheiro](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/10/29/azcopy-announcing-general-availability-of-azcopy-3-0-plus-preview-release-of-azcopy-4-0-with-table-and-file-support.aspx)
* [AzCopy: Otimizado para cenários de cópia em grande escala](http://go.microsoft.com/fwlink/?LinkId=507682)
* [AzCopy: Suporte para o armazenamento georredundante com acesso de leitura](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/04/07/azcopy-support-for-read-access-geo-redundant-account.aspx)
* [AzCopy: Transferir dados com o modo novamente iniciável e o SAS token](http://blogs.msdn.com/b/windowsazurestorage/archive/2013/09/07/azcopy-transfer-data-with-re-startable-mode-and-sas-token.aspx)
* [AzCopy: Utilizando o Blob de cópia de conta em vários locais](http://blogs.msdn.com/b/windowsazurestorage/archive/2013/04/01/azcopy-using-cross-account-copy-blob.aspx)
* [AzCopy: Carregar/transferência de ficheiros para Blobs do Azure](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/12/03/azcopy-uploading-downloading-files-for-windows-azure-blobs.aspx)

