---
title: aaaCopy ou mover dados tooAzure armazenamento com o AzCopy no Linux | Microsoft Docs
description: "Utilize Olá AzCopy no Linux utilitário toomove ou copiar dados tooor do conteúdo de blob e o ficheiro. Copiar dados tooAzure armazenamento de ficheiros locais ou copie os dados dentro ou entre contas de armazenamento. Migre facilmente a sua tooAzure dados de armazenamento."
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
ms.date: 05/11/2017
ms.author: seguler
ms.openlocfilehash: dccb03c9e8cc3ea661494e7834f307b0e3e30cb9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="transfer-data-with-azcopy-on-linux"></a>Transferência de dados com o AzCopy no Linux
O AzCopy no Linux é um utilitário da linha de comandos concebido para copiar dados tooand do armazenamento de Blobs do Microsoft Azure e o ficheiro de utilização de comandos simples com um desempenho ideal. Pode copiar dados de um objeto tooanother dentro da sua conta de armazenamento, ou entre contas de armazenamento.

Existem duas versões do AzCopy que pode transferir. AzCopy no Linux é criado com o .NET Core Framework, que está direcionada para plataformas Linux oferta estilo POSIX opções da linha de comandos. [AzCopy no Windows](storage-use-azcopy.md) baseia-se com o .NET Framework e oferece opções de linha de comandos de estilo do Windows. Este artigo abrange AzCopy no Linux.

## <a name="download-and-install-azcopy"></a>Transfira e instale o AzCopy
### <a name="installation-on-linux"></a>Instalação no Linux

AzCopy no Linux requer o framework .NET Core na plataforma de Olá. Consulte as instruções de instalação de Olá no Olá [.NET Core](https://www.microsoft.com/net/core#linuxubuntu) página.

Por exemplo, vamos a instalar o .NET Core no Ubuntu 16.10. Guia de instalação mais recente Olá, visite [.NET Core no Linux](https://www.microsoft.com/net/core#linuxubuntu) página de instalação.


```bash
sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ yakkety main" > /etc/apt/sources.list.d/dotnetdev.list' 
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 417A0893
sudo apt-get update
sudo apt-get install dotnet-dev-1.0.3
```

Depois de ter instalado o .NET Core, transfira e instale o AzCopy.

```bash
wget -O azcopy.tar.gz https://aka.ms/downloadazcopyprlinux
tar -xf azcopy.tar.gz
sudo ./install.sh
```

Pode remover ficheiros de Olá extraído assim que estiver instalado AzCopy no Linux. Em alternativa se não tiver privilégios de Superutilizador, também pode executar AzCopy utilizando o script de shell Olá 'azcopy' na pasta extraída Olá. 

### <a name="alternative-installation-on-ubuntu"></a>Instalação alternativa no Ubuntu

**Ubuntu 14.04**

Adicionar origem apt para .net Core:

```bash
sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ trusty main" > /etc/apt/sources.list.d/dotnetdev.list' 
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 417A0893
```

Adicione apt origem para o repositório de produto do Microsoft Linux e instale o AzCopy:

```bash
curl https://packages.microsoft.com/config/ubuntu/14.04/prod.list > ./microsoft-prod.list
sudo cp ./microsoft-prod.list /etc/apt/sources.list.d/
curl https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > microsoft.gpg
sudo cp ./microsoft.gpg /etc/apt/trusted.gpg.d/
```

```bash
sudo apt-get update
sudo apt-get install azcopy
```

**Ubuntu 16.04**

Adicionar origem apt para .net Core:

```bash
sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ xenial main" > /etc/apt/sources.list.d/dotnetdev.list' 
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 417A0893
```

Adicione apt origem para o repositório de produto do Microsoft Linux e instale o AzCopy:

```bash
curl https://packages.microsoft.com/config/ubuntu/16.04/prod.list > ./microsoft-prod.list
sudo cp ./microsoft-prod.list /etc/apt/sources.list.d/
curl https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > microsoft.gpg
sudo cp ./microsoft.gpg /etc/apt/trusted.gpg.d/
```

```bash
sudo apt-get update
sudo apt-get install azcopy
```

**Ubuntu 16.10**

Adicionar origem apt para .net Core:

```bash
sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ yakkety main" > /etc/apt/sources.list.d/dotnetdev.list' 
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 417A0893
```

Adicione apt origem para o repositório de produto do Microsoft Linux e instale o AzCopy:

```bash
curl https://packages.microsoft.com/config/ubuntu/16.10/prod.list > ./microsoft-prod.list
sudo cp ./microsoft-prod.list /etc/apt/sources.list.d/
curl https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > microsoft.gpg
sudo cp ./microsoft.gpg /etc/apt/trusted.gpg.d/
```

```bash
sudo apt-get update
sudo apt-get install azcopy
```

## <a name="writing-your-first-azcopy-command"></a>Escrever o seu primeiro comando do AzCopy
sintaxe de básico Olá para comandos do AzCopy é:

```azcopy
azcopy --source <source> --destination <destination> [Options]
```

Olá seguir exemplos demonstram vários cenários para copiar tooand de dados de Blobs do Microsoft Azure e os ficheiros. Consulte toohello `azcopy --help` menu para uma explicação detalhada de parâmetros de Olá utilizados em cada amostra.

## <a name="blob-download"></a>Blob: Transferir
### <a name="download-single-blob"></a>Transferir BLOBs único

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --include "abc.txt"
```

Se a pasta de Olá `/mnt/myfiles` não existir, AzCopy criá-lo e transfere `abc.txt ` na nova pasta de Olá.

### <a name="download-single-blob-from-secondary-region"></a>Transferir BLOBs único da região secundária

```azcopy
azcopy \
    --source https://myaccount-secondary.blob.core.windows.net/mynewcontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --include "abc.txt"
```

Tenha em atenção que tem de ter o armazenamento georredundante com acesso de leitura ativado.

### <a name="download-all-blobs"></a>Transferir todos os blobs

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --recursive
```

Partem do princípio de seguinte Olá residem os blobs no contentor especificado Olá:  

```
abc.txt
abc1.txt
abc2.txt
vd1/a.txt
vd1/abcd.txt
```

Após a operação de transferência Olá, Olá diretório `/mnt/myfiles` inclui Olá os seguintes ficheiros:

```
/mnt/myfiles/abc.txt
/mnt/myfiles/abc1.txt
/mnt/myfiles/abc2.txt
/mnt/myfiles/vd1/a.txt
/mnt/myfiles/vd1/abcd.txt
```

Se não especificar opção `--recursive`, não existem BLOBs não serão transferidos.

### <a name="download-blobs-with-specified-prefix"></a>Transferir blobs com o prefixo especificado

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --include "a" \
    --recursive
```

Partem do princípio de seguinte Olá residem os blobs no contentor especificado Olá. Todos os blobs a partir do prefixo de Olá `a` são transferidas.

```
abc.txt
abc1.txt
abc2.txt
xyz.txt
vd1\a.txt
vd1\abcd.txt
```

Após a operação de transferência Olá, Olá pasta `/mnt/myfiles` inclui Olá os seguintes ficheiros:

```
/mnt/myfiles/abc.txt
/mnt/myfiles/abc1.txt
/mnt/myfiles/abc2.txt
```

prefixo de Olá aplica-se o diretório virtual de toohello, o que faz parte de primeiro Olá do nome do blob Olá. Exemplo de Olá mostrado acima, diretório virtual Olá não corresponde ao prefixo especificado Olá, pelo que não existem BLOBs é transferido. Além disso, se hello opção `--recursive` não for especificado, AzCopy não transferir blobs.

### <a name="set-hello-last-modified-time-of-exported-files-toobe-same-as-hello-source-blobs"></a>Definir a hora de Olá última modificação de ficheiros exportados toobe igual ao hello blobs de origem

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination "/mnt/myfiles" \
    --source-key <key> \
    --preserve-last-modified-time
```

Também pode excluir os blobs de operação de transferência de Olá com base na respetiva tempo last-modified. Por exemplo, se pretender que os blobs tooexclude cuja hora da última modificação é Olá igual ou mais recente do que o ficheiro de destino Olá, adicionar Olá `--exclude-newer` opção:

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --preserve-last-modified-time \
    --exclude-newer
```

Ou se pretender que os blobs tooexclude cuja hora da última modificação é Olá igual ou mais antiga do que o ficheiro de destino Olá, adicione Olá `--exclude-older` opção:

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --preserve-last-modified-time \
    --exclude-older
```

## <a name="blob-upload"></a>Blob: carregar
### <a name="upload-single-file"></a>Carregar ficheiro único

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --include "abc.txt"
```

Se Olá o contentor de destino especificado não existe, o AzCopy criá-lo e carregamentos Olá ficheiro para a mesma.

### <a name="upload-single-file-toovirtual-directory"></a>Carregar ficheiro único diretório toovirtual

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --include "abc.txt"
```

Se Olá especificado diretório virtual não existe, o AzCopy carrega Olá tooinclude Olá virtual diretório do ficheiro no nome do blob Olá (*por exemplo,*, `vd/abc.txt` no exemplo Olá acima).

### <a name="upload-all-files"></a>Carregar todos os ficheiros

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --recursive
```

Especificar a opção `--recursive` carregamentos Olá conteúdo Olá especificado diretório tooBlob armazenamento recursiva, o que significa que todas as subpastas e os ficheiros são carregados bem. Por exemplo, suponha o seguinte Olá residem os ficheiros na pasta `/mnt/myfiles`:

```
/mnt/myfiles/abc.txt
/mnt/myfiles/abc1.txt
/mnt/myfiles/abc2.txt
/mnt/myfiles/subfolder/a.txt
/mnt/myfiles/subfolder/abcd.txt
```

Após a operação de carregamento de Olá, o contentor de Olá inclui Olá os seguintes ficheiros:

```
abc.txt
abc1.txt
abc2.txt
subfolder/a.txt
subfolder/abcd.txt
```

Quando Olá opção `--recursive` não for especificado, só hello seguintes três ficheiros são carregados:

```
abc.txt
abc1.txt
abc2.txt
```

### <a name="upload-files-matching-specified-pattern"></a>Carregar ficheiros correspondentes ao padrão especificado

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --include "a*" \
    --recursive
```

Partem do princípio de seguinte Olá residem os ficheiros na pasta `/mnt/myfiles`:

```
/mnt/myfiles/abc.txt
/mnt/myfiles/abc1.txt
/mnt/myfiles/abc2.txt
/mnt/myfiles/xyz.txt
/mnt/myfiles/subfolder/a.txt
/mnt/myfiles/subfolder/abcd.txt
```

Após a operação de carregamento de Olá, o contentor de Olá inclui Olá os seguintes ficheiros:

```
abc.txt
abc1.txt
abc2.txt
subfolder/a.txt
subfolder/abcd.txt
```

Quando Olá opção `--recursive` não for especificado, AzCopy ignora os ficheiros que estão em diretórios secundárias:

```
abc.txt
abc1.txt
abc2.txt
```

### <a name="specify-hello-mime-content-type-of-a-destination-blob"></a>Especifique o tipo de conteúdo de MIME de Olá de um blob de destino
Por predefinição, AzCopy define o tipo de conteúdo de Olá de um blob de destino demasiado`application/octet-stream`. No entanto, pode especificar explicitamente tipo de conteúdo de Olá através da opção de Olá `--set-content-type [content-type]`. Esta sintaxe define o tipo de conteúdo de Olá para todos os blobs numa operação de carregamento.

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/myContainer/ \
    --dest-key <key> \
    --include "ab" \
    --set-content-type "video/mp4"
```

Se hello opção `--set-content-type` for especificado sem um valor, em seguida, o AzCopy define cada blob ou um ficheiro do tipo de conteúdo de acordo com tooits extensão de ficheiro.

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/myContainer/ \
    --dest-key <key> \
    --include "ab" \
    --set-content-type
```

## <a name="blob-copy"></a>Blob: cópia
### <a name="copy-single-blob-within-storage-account"></a>Copiar blob único na conta de armazenamento

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer1 \
    --destination https://myaccount.blob.core.windows.net/mycontainer2 \
    --source-key <key> \
    --dest-key <key> \
    --include "abc.txt"
```

Quando copiar um blob sem - opção de cópia de sincronização, um [cópia do lado do servidor](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) é efetuar a operação.

### <a name="copy-single-blob-across-storage-accounts"></a>Copiar blob único em contas de armazenamento

```azcopy
azcopy \
    --source https://sourceaccount.blob.core.windows.net/mycontainer1 \
    --destination https://destaccount.blob.core.windows.net/mycontainer2 \
    --source-key <key1> \
    --dest-key <key2> \
    --include "abc.txt"
```

Quando copiar um blob sem - opção de cópia de sincronização, um [cópia do lado do servidor](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) é efetuar a operação.

### <a name="copy-single-blob-from-secondary-region-tooprimary-region"></a>Copiar blob único da região de tooprimary região secundária

```azcopy
azcopy \
    --source https://myaccount1-secondary.blob.core.windows.net/mynewcontainer1 \
    --destination https://myaccount2.blob.core.windows.net/mynewcontainer2 \
    --source-key <key1> \
    --dest-key <key2> \
    --include "abc.txt"
```

Tenha em atenção que tem de ter o armazenamento georredundante com acesso de leitura ativado.

### <a name="copy-single-blob-and-its-snapshots-across-storage-accounts"></a>Copiar blob único e o respetivos instantâneos em contas de armazenamento

```azcopy
azcopy \
    --source https://sourceaccount.blob.core.windows.net/mycontainer1 \
    --destination https://destaccount.blob.core.windows.net/mycontainer2 \
    --source-key <key1> \
    --dest-key <key2> \
    --include "abc.txt" \
    --include-snapshot
```

Após a operação de cópia de Olá, um contentor de destino Olá inclui blob Olá e respetivos instantâneos. Olá contentor inclui Olá seguinte blob e o respetivos instantâneos:

```
abc.txt
abc (2013-02-25 080757).txt
abc (2014-02-21 150331).txt
```

### <a name="synchronously-copy-blobs-across-storage-accounts"></a>Em sincronia copiar os blobs em contas de armazenamento
AzCopy por predefinição copia dados entre dois pontos finais de armazenamento de forma assíncrona. Por conseguinte, é copiado Olá execuções de operação de cópia em segundo plano Olá utilizando a capacidade de reserva de largura de banda que não tenha nenhum SLA em termos de rápido como um blob. 

Olá `--sync-copy` opção garante que a operação de cópia de Olá obtém velocidade consistente. AzCopy efetua a cópia síncrona Olá transferindo blobs Olá toocopy de Olá especificada de memória de toolocal de origem e, em seguida, carregá-los toohello destino de armazenamento de Blobs.

```azcopy
azcopy \
    --source https://myaccount1.blob.core.windows.net/myContainer/ \
    --destination https://myaccount2.blob.core.windows.net/myContainer/ \
    --source-key <key1> \
    --dest-key <key2> \
    --include "ab" \
    --sync-copy
```

`--sync-copy`pode gerar a saída adicionais custos comparadas tooasynchronous cópia. Olá abordagem recomendada é toouse esta opção na VM do Azure, que está a ser Olá mesma região que o custo de saída tooavoid de conta de armazenamento de origem.

## <a name="file-download"></a>Ficheiro: Transferir
### <a name="download-single-file"></a>Transferência de ficheiro único

```azcopy
azcopy \
    --source https://myaccount.file.core.windows.net/myfileshare/myfolder1/ \
    --destination /mnt/myfiles \
    --source-key <key> \
    --include "abc.txt"
```

Se Olá especificado origem é uma partilha de ficheiros do Azure, tem de especificar se o nome de ficheiro exato de Olá, (*por exemplo,* `abc.txt`) toodownload um ficheiro único, ou especificar a opção `--recursive` toodownload todos os ficheiros numa partilha de Olá em modo recursivo. Tentativa de toospecify um padrão de ficheiro e a opção `--recursive` resultados em conjunto num erro.

### <a name="download-all-files"></a>Transferir todos os ficheiros

```azcopy
azcopy \
    --source https://myaccount.file.core.windows.net/myfileshare/ \
    --destination /mnt/myfiles \
    --source-key <key> \
    --recursive
```

Tenha em atenção que não são transferidas quaisquer pastas vazias.

## <a name="file-upload"></a>Ficheiro: carregar
### <a name="upload-single-file"></a>Carregar ficheiro único

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.file.core.windows.net/myfileshare/ \
    --dest-key <key> \
    --include abc.txt
```

### <a name="upload-all-files"></a>Carregar todos os ficheiros

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.file.core.windows.net/myfileshare/ \
    --dest-key <key> \
    --recursive
```

Tenha em atenção que quaisquer pastas vazias não são carregadas.

### <a name="upload-files-matching-specified-pattern"></a>Carregar ficheiros correspondentes ao padrão especificado

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.file.core.windows.net/myfileshare/ \
    --dest-key <key> \
    --include "ab*" \
    --recursive
```

## <a name="file-copy"></a>Ficheiro: cópia
### <a name="copy-across-file-shares"></a>Copiar em partilhas de ficheiros

```azcopy
azcopy \
    --source https://myaccount1.file.core.windows.net/myfileshare1/ \
    --destination https://myaccount2.file.core.windows.net/myfileshare2/ \
    --source-key <key1> \
    --dest-key <key2> \
    --recursive
```
Quando copiar um ficheiro através de partilhas de ficheiros, um [cópia do lado do servidor](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) é efetuar a operação.

### <a name="copy-from-file-share-tooblob"></a>Copiar do tooblob de partilha de ficheiros

```azcopy
azcopy \ 
    --source https://myaccount1.file.core.windows.net/myfileshare/ \
    --destination https://myaccount2.blob.core.windows.net/mycontainer/ \
    --source-key <key1> \
    --dest-key <key2> \
    --recursive
```
Quando copiar um ficheiro de tooblob de partilha de ficheiros, um [cópia do lado do servidor](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) é efetuar a operação.

### <a name="copy-from-blob-toofile-share"></a>Copiar de blob toofile partilha

```azcopy
azcopy \
    --source https://myaccount1.blob.core.windows.net/mycontainer/ \
    --destination https://myaccount2.file.core.windows.net/myfileshare/ \
    --source-key <key1> \
    --dest-key <key2> \
    --recursive
```
Quando copiar um ficheiro de partilha de toofile de blob, um [cópia do lado do servidor](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) é efetuar a operação.

### <a name="synchronously-copy-files"></a>Em sincronia copiar ficheiros
Pode especificar Olá `--sync-copy` opção toocopy dados tooFile de armazenamento de ficheiros armazenamento, do armazenamento de ficheiros tooBlob armazenamento e de armazenamento de BLOBs tooFile armazenamento de forma síncrona. AzCopy executa esta operação ao descarregar Olá origem dados toolocal de memória e, em seguida, carregá-lo toodestination. Neste caso, o custo de saída padrão se aplica.

```azcopy
azcopy \
    --source https://myaccount1.file.core.windows.net/myfileshare1/ \
    --destination https://myaccount2.file.core.windows.net/myfileshare2/ \
    --source-key <key1> \
    --dest-key <key2> \
    --recursive \
    --sync-copy
```

Quando copiar do File Storage tooBlob armazenamento, é de tipo de blob predefinido Olá BLOBs de blocos, o utilizador pode especificar a opção `/BlobType:page` toochange Olá tipo de blob de destino.

Tenha em atenção que `--sync-copy` poderá gerar a saída adicional custo compara tooasynchronous cópia. Olá abordagem recomendada é toouse esta opção na VM do Azure, que está a ser Olá mesma região que o custo de saída tooavoid de conta de armazenamento de origem.

## <a name="other-azcopy-features"></a>Outras funcionalidades do AzCopy
### <a name="only-copy-data-that-doesnt-exist-in-hello-destination"></a>Apenas os dados de cópia que não existem no destino Olá
Olá `--exclude-older` e `--exclude-newer` parâmetros permitem tooexclude recursos de origem de anterior ou mais recente de ser copiado, respetivamente. Se pretender apenas toocopy recursos de origem que não existem no destino Olá, pode especificar os dois parâmetros na Olá comandos do AzCopy:

    --source http://myaccount.blob.core.windows.net/mycontainer --destination /mnt/myfiles --source-key <sourcekey> --recursive --exclude-older --exclude-newer

    --source /mnt/myfiles --destination http://myaccount.file.core.windows.net/myfileshare --dest-key <destkey> --recursive --exclude-older --exclude-newer

    --source http://myaccount.blob.core.windows.net/mycontainer --destination http://myaccount.blob.core.windows.net/mycontainer1 --source-key <sourcekey> --dest-key <destkey> --recursive --exclude-older --exclude-newer

### <a name="use-a-configuration-file-toospecify-command-line-parameters"></a>Utilizar um toospecify de ficheiro de configuração para parâmetros de linha de comandos

```azcopy
azcopy --config-file "azcopy-config.ini"
```

Pode incluir quaisquer parâmetros de linha de comandos do AzCopy num ficheiro de configuração. Processos do AzCopy Olá parâmetros no ficheiro de Olá como se tivesse sido especificados na linha de comandos Olá, efetuar uma substituição direta com conteúdo Olá do ficheiro de Olá.

Partem do princípio de um ficheiro de configuração com o nome `copyoperation`, que contém Olá seguintes linhas. Cada parâmetro do AzCopy pode ser especificado numa única linha.

    --source http://myaccount.blob.core.windows.net/mycontainer --destination /mnt/myfiles --source-key <sourcekey> --recursive --quiet

ou, no separar linhas:

    --source http://myaccount.blob.core.windows.net/mycontainer
    --destination /mnt/myfiles
    --source-key<sourcekey>
    --recursive
    --quiet

AzCopy falha se dividir parâmetro Olá por duas linhas, conforme mostrado aqui para Olá `--source-key` parâmetro:

    http://myaccount.blob.core.windows.net/mycontainer
    /mnt/myfiles
    --sourcekey
    <sourcekey>
    --recursive
    --quiet

### <a name="specify-a-shared-access-signature-sas"></a>Especifique uma assinatura de acesso partilhado (SAS)

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer1 \
    --destination https://myaccount.blob.core.windows.net/mycontainer2 \
    --source-sas <SAS1> \
    --dest-sas <SAS2> \
    --include abc.txt
```

Também pode especificar uma SAS no contentor de Olá URI:

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer1/?SourceSASToken \
    --destination /mnt/myfiles \
    --recursive
```

Tenha em atenção que AzCopy atualmente suporta apenas Olá [conta SAS](https://docs.microsoft.com/en-us/azure/storage/storage-dotnet-shared-access-signature-part-1).

### <a name="journal-file-folder"></a>Pasta de ficheiros do diário de alterações
Sempre que emitir um comando tooAzCopy, este verifica se existe um ficheiro de diário de alterações na pasta predefinida de hello, ou se existe uma pasta que especificou através desta opção. Se não existir um ficheiro do diário de alterações de Olá em qualquer local, o AzCopy trata operação Olá como novo e gera um novo ficheiro de diário de alterações.

Se existirem ficheiros do diário de alterações de Olá, o AzCopy verifica se linha de comandos de Olá introduzido corresponde a linha de comandos Olá no ficheiro de diário Olá. Se duas linhas de comando Olá corresponderem, o AzCopy retoma operação incompleta Olá. Se não corresponderem, o AzCopy pede ao utilizador tooeither substituir Olá diário ficheiro toostart uma operação de novo ou a operação atual do toocancel Olá.

Se pretender que a localização predefinida de Olá de toouse para o ficheiro do diário de alterações de Olá:

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --resume
```

Se omitir opção `--resume`, ou especificar a opção `--resume` sem o caminho da pasta Olá, conforme mostrado acima, o AzCopy cria Olá diário ficheiro na localização predefinida de Olá, que é `~\Microsoft\Azure\AzCopy`. Se já existir um ficheiro do diário de alterações de Olá, o AzCopy retoma operação Olá com base num ficheiro do diário de alterações de Olá.

Se quiser toospecify numa localização personalizada para o ficheiro do diário de alterações de Olá:

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key key \
    --resume "/mnt/myjournal"
```

Este exemplo cria ficheiros do diário de alterações de Olá se já existir. Se existir, o AzCopy retoma operação Olá com base num ficheiro do diário de alterações de Olá.

Se quiser tooresume uma operação do AzCopy, repetir Olá mesmo comando. AzCopy no Linux, em seguida, irá pedir confirmação:

```azcopy
Incomplete operation with same command line detected at hello journal directory "/home/myaccount/Microsoft/Azure/AzCopy", do you want tooresume hello operation? Choose Yes tooresume, choose No toooverwrite hello journal toostart a new operation. (Yes/No)
```

### <a name="output-verbose-logs"></a>Registos verbosos de saída

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --verbose
```

### <a name="specify-hello-number-of-concurrent-operations-toostart"></a>Especifique o número de Olá de operações simultâneas toostart
Opção `--parallel-level` Especifica o número de Olá de operações de cópia em simultâneo. Por predefinição, o AzCopy é iniciado um determinado número de débito de transferência de dados de Olá tooincrease operações simultâneas. número de Olá de operações simultâneas de é igual Olá, número de processadores tiver oito horas. Se estiver a executar o AzCopy através de uma rede de largura de banda reduzida, pode especificar um número inferior de - falha de tooavoid de nível de paralelo provocada por concorrência de recursos.

[!TIP]
>lista completa de Olá tooview dos parâmetros do AzCopy, consulte 'azcopy – Ajuda' menu.

## <a name="known-issues-and-best-practices"></a>Problemas conhecidos e melhores práticas
### <a name="error-net-core-is-not-found-in-hello-system"></a>Erro: .NET Core não foi encontrado no sistema de Olá.
Se ocorrer um erro a indicar que o .NET Core não está instalado no sistema de Olá, Olá binário do caminho toohello .NET Core `dotnet` poderá estar em falta.

Na ordem tooaddress este problema, localizar binário de .NET Core Olá no sistema de Olá:
```bash
sudo find / -name dotnet
```

Esta ação devolve Olá caminho toohello dotnet binário. 

    /opt/rh/rh-dotnetcore11/root/usr/bin/dotnet
    /opt/rh/rh-dotnetcore11/root/usr/lib64/dotnetcore/dotnet
    /opt/rh/rh-dotnetcore11/root/usr/lib64/dotnetcore/shared/Microsoft.NETCore.App/1.1.2/dotnet

Agora, adicione esta variável de caminho de toohello do caminho. Para o sudo, edição secure_path toocontain Olá caminho toohello dotnet binário:
```bash 
sudo visudo
### Append hello path found in hello preceding example too'secure_path' variable
```

Neste exemplo, a variável de secure_path lê como:

```
secure_path = /sbin:/bin:/usr/sbin:/usr/bin:/opt/rh/rh-dotnetcore11/root/usr/bin/
```

Para o utilizador atual Olá, editar.bash_profile/.profile tooinclude Olá caminho toohello dotnet binário na variável de caminho 
```bash
vi ~/.bash_profile
### Append hello path found in hello preceding example too'PATH' variable
```

Certifique-se de que o .NET Core está agora no caminho:
```bash
which dotnet
sudo which dotnet
```

### <a name="error-installing-azcopy"></a>Erro ao instalar o AzCopy
Se ocorrerem problemas com a instalação do AzCopy, tente toorun AzCopy utilizando scripts de bash Olá no Olá extraído `azcopy` pasta.

```bash
cd azcopy
./azcopy
```

### <a name="limit-concurrent-writes-while-copying-data"></a>Limitar escritas em simultâneo ao copiar dados
Quando copia blobs ou ficheiros com o AzCopy, tenha em atenção que outra aplicação pode ser modificar Olá dados enquanto estiver a copiar. Se for possível, certifique-se de que os dados de Olá que estiver a copiar não está a ser modificados durante a operação de cópia de Olá. Por exemplo, quando copiar um VHD associado uma máquina virtual do Azure, certifique-se de que não existem outras aplicações atualmente estiver a escrever toohello VHD. Uma boa forma toodo trata por leasing Olá recursos toobe copiado. Em alternativa, pode criar um instantâneo do VHD de Olá primeiro e, em seguida, copiar o instantâneo de Olá.

Se não podem impedir outras aplicações de escrever tooblobs ou ficheiros, enquanto que estão a ser copiados, em seguida, tenha em atenção que, pela tarefa de Olá Olá tempo é concluída, hello recursos copiados podem já não ter paridade completa com recursos de origem Olá.

### <a name="run-one-azcopy-instance-on-one-machine"></a>Execute uma instância do AzCopy num computador.
O AzCopy é concebida toomaximize Olá utilização sua máquina recursos tooaccelerate Olá da transferência de dados, recomendamos que execute apenas uma instância do AzCopy num computador e especificar a opção de Olá `--parallel-level` se precisar de mais simultâneas operações. Para obter mais detalhes, escreva `AzCopy --help parallel-level` na linha de comandos Olá.

## <a name="next-steps"></a>Passos seguintes
Para obter mais informações sobre o Storage do Azure e AzCopy, consulte Olá os seguintes recursos:

### <a name="azure-storage-documentation"></a>Documentação do Storage do Azure:
* [Introdução tooAzure armazenamento](storage-introduction.md)
* [Criar uma conta de armazenamento](storage-create-storage-account.md)
* [Gerir a blobs com o Explorador de armazenamento](https://docs.microsoft.com/en-us/azure/vs-azure-tools-storage-explorer-blobs)
* [Utilizar Olá 2.0 de CLI do Azure com o Storage do Azure](storage-azure-cli.md)
* [Como toouse Blob storage do C++](storage-c-plus-plus-how-to-use-blobs.md)
* [Como toouse Blob storage do Java](storage-java-how-to-use-blob-storage.md)
* [Como toouse Blob storage do Node.js](storage-nodejs-how-to-use-blob-storage.md)
* [Como toouse Blob storage do Python](storage-python-how-to-use-blob-storage.md)

### <a name="azure-storage-blog-posts"></a>Mensagens de blogue de armazenamento do Azure:
* [Anunciar AzCopy na pré-visualização do Linux](https://azure.microsoft.com/en-in/blog/announcing-azcopy-on-linux-preview/)
* [Introdução ao pré-visualização de biblioteca de movimento de dados de armazenamento do Azure](https://azure.microsoft.com/blog/introducing-azure-storage-data-movement-library-preview-2/)
* [AzCopy: Introdução ao copiar síncrona e tipo de conteúdo personalizado](http://blogs.msdn.com/b/windowsazurestorage/archive/2015/01/13/azcopy-introducing-synchronous-copy-and-customized-content-type.aspx)
* [AzCopy: Anunciar disponibilidade geral do 3.0 AzCopy plus versão de pré-visualização do AzCopy 4.0 com suporte de tabela e ficheiro](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/10/29/azcopy-announcing-general-availability-of-azcopy-3-0-plus-preview-release-of-azcopy-4-0-with-table-and-file-support.aspx)
* [AzCopy: Otimizado para cenários de cópia em grande escala](http://go.microsoft.com/fwlink/?LinkId=507682)
* [AzCopy: Suporte para o armazenamento georredundante com acesso de leitura](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/04/07/azcopy-support-for-read-access-geo-redundant-account.aspx)
* [AzCopy: Transferir dados com o SAS token e o modo reiniciável](http://blogs.msdn.com/b/windowsazurestorage/archive/2013/09/07/azcopy-transfer-data-with-re-startable-mode-and-sas-token.aspx)
* [AzCopy: Utilizando o Blob de cópia de conta em vários locais](http://blogs.msdn.com/b/windowsazurestorage/archive/2013/04/01/azcopy-using-cross-account-copy-blob.aspx)
* [AzCopy: Carregar/transferência de ficheiros para Blobs do Azure](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/12/03/azcopy-uploading-downloading-files-for-windows-azure-blobs.aspx)

