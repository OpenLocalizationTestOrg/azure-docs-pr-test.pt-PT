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
# <a name="transfer-data-with-azcopy-on-linux"></a><span data-ttu-id="7b1da-105">Transferência de dados com o AzCopy no Linux</span><span class="sxs-lookup"><span data-stu-id="7b1da-105">Transfer data with AzCopy on Linux</span></span>
<span data-ttu-id="7b1da-106">O AzCopy no Linux é um utilitário da linha de comandos concebido para copiar dados tooand do armazenamento de Blobs do Microsoft Azure e o ficheiro de utilização de comandos simples com um desempenho ideal.</span><span class="sxs-lookup"><span data-stu-id="7b1da-106">AzCopy on Linux is a command-line utility designed for copying data tooand from Microsoft Azure Blob and File storage using simple commands with optimal performance.</span></span> <span data-ttu-id="7b1da-107">Pode copiar dados de um objeto tooanother dentro da sua conta de armazenamento, ou entre contas de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="7b1da-107">You can copy data from one object tooanother within your storage account, or between storage accounts.</span></span>

<span data-ttu-id="7b1da-108">Existem duas versões do AzCopy que pode transferir.</span><span class="sxs-lookup"><span data-stu-id="7b1da-108">There are two versions of AzCopy that you can download.</span></span> <span data-ttu-id="7b1da-109">AzCopy no Linux é criado com o .NET Core Framework, que está direcionada para plataformas Linux oferta estilo POSIX opções da linha de comandos.</span><span class="sxs-lookup"><span data-stu-id="7b1da-109">AzCopy on Linux is built with .NET Core Framework, which targets Linux platforms offering POSIX style command-line options.</span></span> <span data-ttu-id="7b1da-110">[AzCopy no Windows](storage-use-azcopy.md) baseia-se com o .NET Framework e oferece opções de linha de comandos de estilo do Windows.</span><span class="sxs-lookup"><span data-stu-id="7b1da-110">[AzCopy on Windows](storage-use-azcopy.md) is built with .NET Framework, and offers Windows style command-line options.</span></span> <span data-ttu-id="7b1da-111">Este artigo abrange AzCopy no Linux.</span><span class="sxs-lookup"><span data-stu-id="7b1da-111">This article covers AzCopy on Linux.</span></span>

## <a name="download-and-install-azcopy"></a><span data-ttu-id="7b1da-112">Transfira e instale o AzCopy</span><span class="sxs-lookup"><span data-stu-id="7b1da-112">Download and install AzCopy</span></span>
### <a name="installation-on-linux"></a><span data-ttu-id="7b1da-113">Instalação no Linux</span><span class="sxs-lookup"><span data-stu-id="7b1da-113">Installation on Linux</span></span>

<span data-ttu-id="7b1da-114">AzCopy no Linux requer o framework .NET Core na plataforma de Olá.</span><span class="sxs-lookup"><span data-stu-id="7b1da-114">AzCopy on Linux requires .NET Core framework on hello platform.</span></span> <span data-ttu-id="7b1da-115">Consulte as instruções de instalação de Olá no Olá [.NET Core](https://www.microsoft.com/net/core#linuxubuntu) página.</span><span class="sxs-lookup"><span data-stu-id="7b1da-115">See hello installation instructions on hello [.NET Core](https://www.microsoft.com/net/core#linuxubuntu) page.</span></span>

<span data-ttu-id="7b1da-116">Por exemplo, vamos a instalar o .NET Core no Ubuntu 16.10.</span><span class="sxs-lookup"><span data-stu-id="7b1da-116">As an example, let's install .NET Core on Ubuntu 16.10.</span></span> <span data-ttu-id="7b1da-117">Guia de instalação mais recente Olá, visite [.NET Core no Linux](https://www.microsoft.com/net/core#linuxubuntu) página de instalação.</span><span class="sxs-lookup"><span data-stu-id="7b1da-117">For hello latest installation guide, visit [.NET Core on Linux](https://www.microsoft.com/net/core#linuxubuntu) installation page.</span></span>


```bash
sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ yakkety main" > /etc/apt/sources.list.d/dotnetdev.list' 
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 417A0893
sudo apt-get update
sudo apt-get install dotnet-dev-1.0.3
```

<span data-ttu-id="7b1da-118">Depois de ter instalado o .NET Core, transfira e instale o AzCopy.</span><span class="sxs-lookup"><span data-stu-id="7b1da-118">Once you have installed .NET Core, download and install AzCopy.</span></span>

```bash
wget -O azcopy.tar.gz https://aka.ms/downloadazcopyprlinux
tar -xf azcopy.tar.gz
sudo ./install.sh
```

<span data-ttu-id="7b1da-119">Pode remover ficheiros de Olá extraído assim que estiver instalado AzCopy no Linux.</span><span class="sxs-lookup"><span data-stu-id="7b1da-119">You can remove hello extracted files once AzCopy on Linux is installed.</span></span> <span data-ttu-id="7b1da-120">Em alternativa se não tiver privilégios de Superutilizador, também pode executar AzCopy utilizando o script de shell Olá 'azcopy' na pasta extraída Olá.</span><span class="sxs-lookup"><span data-stu-id="7b1da-120">Alternatively if you do not have superuser privileges, you can also run AzCopy using hello shell script 'azcopy' in hello extracted folder.</span></span> 

### <a name="alternative-installation-on-ubuntu"></a><span data-ttu-id="7b1da-121">Instalação alternativa no Ubuntu</span><span class="sxs-lookup"><span data-stu-id="7b1da-121">Alternative Installation on Ubuntu</span></span>

<span data-ttu-id="7b1da-122">**Ubuntu 14.04**</span><span class="sxs-lookup"><span data-stu-id="7b1da-122">**Ubuntu 14.04**</span></span>

<span data-ttu-id="7b1da-123">Adicionar origem apt para .net Core:</span><span class="sxs-lookup"><span data-stu-id="7b1da-123">Add apt source for .Net Core:</span></span>

```bash
sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ trusty main" > /etc/apt/sources.list.d/dotnetdev.list' 
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 417A0893
```

<span data-ttu-id="7b1da-124">Adicione apt origem para o repositório de produto do Microsoft Linux e instale o AzCopy:</span><span class="sxs-lookup"><span data-stu-id="7b1da-124">Add apt source for Microsoft Linux product repository and install AzCopy:</span></span>

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

<span data-ttu-id="7b1da-125">**Ubuntu 16.04**</span><span class="sxs-lookup"><span data-stu-id="7b1da-125">**Ubuntu 16.04**</span></span>

<span data-ttu-id="7b1da-126">Adicionar origem apt para .net Core:</span><span class="sxs-lookup"><span data-stu-id="7b1da-126">Add apt source for .Net Core:</span></span>

```bash
sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ xenial main" > /etc/apt/sources.list.d/dotnetdev.list' 
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 417A0893
```

<span data-ttu-id="7b1da-127">Adicione apt origem para o repositório de produto do Microsoft Linux e instale o AzCopy:</span><span class="sxs-lookup"><span data-stu-id="7b1da-127">Add apt source for Microsoft Linux product repository and install AzCopy:</span></span>

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

<span data-ttu-id="7b1da-128">**Ubuntu 16.10**</span><span class="sxs-lookup"><span data-stu-id="7b1da-128">**Ubuntu 16.10**</span></span>

<span data-ttu-id="7b1da-129">Adicionar origem apt para .net Core:</span><span class="sxs-lookup"><span data-stu-id="7b1da-129">Add apt source for .Net Core:</span></span>

```bash
sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ yakkety main" > /etc/apt/sources.list.d/dotnetdev.list' 
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 417A0893
```

<span data-ttu-id="7b1da-130">Adicione apt origem para o repositório de produto do Microsoft Linux e instale o AzCopy:</span><span class="sxs-lookup"><span data-stu-id="7b1da-130">Add apt source for Microsoft Linux product repository and install AzCopy:</span></span>

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

## <a name="writing-your-first-azcopy-command"></a><span data-ttu-id="7b1da-131">Escrever o seu primeiro comando do AzCopy</span><span class="sxs-lookup"><span data-stu-id="7b1da-131">Writing your first AzCopy command</span></span>
<span data-ttu-id="7b1da-132">sintaxe de básico Olá para comandos do AzCopy é:</span><span class="sxs-lookup"><span data-stu-id="7b1da-132">hello basic syntax for AzCopy commands is:</span></span>

```azcopy
azcopy --source <source> --destination <destination> [Options]
```

<span data-ttu-id="7b1da-133">Olá seguir exemplos demonstram vários cenários para copiar tooand de dados de Blobs do Microsoft Azure e os ficheiros.</span><span class="sxs-lookup"><span data-stu-id="7b1da-133">hello following examples demonstrate various scenarios for copying data tooand from Microsoft Azure Blobs and Files.</span></span> <span data-ttu-id="7b1da-134">Consulte toohello `azcopy --help` menu para uma explicação detalhada de parâmetros de Olá utilizados em cada amostra.</span><span class="sxs-lookup"><span data-stu-id="7b1da-134">Refer toohello `azcopy --help` menu for a detailed explanation of hello parameters used in each sample.</span></span>

## <a name="blob-download"></a><span data-ttu-id="7b1da-135">Blob: Transferir</span><span class="sxs-lookup"><span data-stu-id="7b1da-135">Blob: Download</span></span>
### <a name="download-single-blob"></a><span data-ttu-id="7b1da-136">Transferir BLOBs único</span><span class="sxs-lookup"><span data-stu-id="7b1da-136">Download single blob</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --include "abc.txt"
```

<span data-ttu-id="7b1da-137">Se a pasta de Olá `/mnt/myfiles` não existir, AzCopy criá-lo e transfere `abc.txt ` na nova pasta de Olá.</span><span class="sxs-lookup"><span data-stu-id="7b1da-137">If hello folder `/mnt/myfiles` does not exist, AzCopy creates it and downloads `abc.txt ` into hello new folder.</span></span>

### <a name="download-single-blob-from-secondary-region"></a><span data-ttu-id="7b1da-138">Transferir BLOBs único da região secundária</span><span class="sxs-lookup"><span data-stu-id="7b1da-138">Download single blob from secondary region</span></span>

```azcopy
azcopy \
    --source https://myaccount-secondary.blob.core.windows.net/mynewcontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --include "abc.txt"
```

<span data-ttu-id="7b1da-139">Tenha em atenção que tem de ter o armazenamento georredundante com acesso de leitura ativado.</span><span class="sxs-lookup"><span data-stu-id="7b1da-139">Note that you must have read-access geo-redundant storage enabled.</span></span>

### <a name="download-all-blobs"></a><span data-ttu-id="7b1da-140">Transferir todos os blobs</span><span class="sxs-lookup"><span data-stu-id="7b1da-140">Download all blobs</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --recursive
```

<span data-ttu-id="7b1da-141">Partem do princípio de seguinte Olá residem os blobs no contentor especificado Olá:</span><span class="sxs-lookup"><span data-stu-id="7b1da-141">Assume hello following blobs reside in hello specified container:</span></span>  

```
abc.txt
abc1.txt
abc2.txt
vd1/a.txt
vd1/abcd.txt
```

<span data-ttu-id="7b1da-142">Após a operação de transferência Olá, Olá diretório `/mnt/myfiles` inclui Olá os seguintes ficheiros:</span><span class="sxs-lookup"><span data-stu-id="7b1da-142">After hello download operation, hello directory `/mnt/myfiles` includes hello following files:</span></span>

```
/mnt/myfiles/abc.txt
/mnt/myfiles/abc1.txt
/mnt/myfiles/abc2.txt
/mnt/myfiles/vd1/a.txt
/mnt/myfiles/vd1/abcd.txt
```

<span data-ttu-id="7b1da-143">Se não especificar opção `--recursive`, não existem BLOBs não serão transferidos.</span><span class="sxs-lookup"><span data-stu-id="7b1da-143">If you do not specify option `--recursive`, no blob will be downloaded.</span></span>

### <a name="download-blobs-with-specified-prefix"></a><span data-ttu-id="7b1da-144">Transferir blobs com o prefixo especificado</span><span class="sxs-lookup"><span data-stu-id="7b1da-144">Download blobs with specified prefix</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --include "a" \
    --recursive
```

<span data-ttu-id="7b1da-145">Partem do princípio de seguinte Olá residem os blobs no contentor especificado Olá.</span><span class="sxs-lookup"><span data-stu-id="7b1da-145">Assume hello following blobs reside in hello specified container.</span></span> <span data-ttu-id="7b1da-146">Todos os blobs a partir do prefixo de Olá `a` são transferidas.</span><span class="sxs-lookup"><span data-stu-id="7b1da-146">All blobs beginning with hello prefix `a` are downloaded.</span></span>

```
abc.txt
abc1.txt
abc2.txt
xyz.txt
vd1\a.txt
vd1\abcd.txt
```

<span data-ttu-id="7b1da-147">Após a operação de transferência Olá, Olá pasta `/mnt/myfiles` inclui Olá os seguintes ficheiros:</span><span class="sxs-lookup"><span data-stu-id="7b1da-147">After hello download operation, hello folder `/mnt/myfiles` includes hello following files:</span></span>

```
/mnt/myfiles/abc.txt
/mnt/myfiles/abc1.txt
/mnt/myfiles/abc2.txt
```

<span data-ttu-id="7b1da-148">prefixo de Olá aplica-se o diretório virtual de toohello, o que faz parte de primeiro Olá do nome do blob Olá.</span><span class="sxs-lookup"><span data-stu-id="7b1da-148">hello prefix applies toohello virtual directory, which forms hello first part of hello blob name.</span></span> <span data-ttu-id="7b1da-149">Exemplo de Olá mostrado acima, diretório virtual Olá não corresponde ao prefixo especificado Olá, pelo que não existem BLOBs é transferido.</span><span class="sxs-lookup"><span data-stu-id="7b1da-149">In hello example shown above, hello virtual directory does not match hello specified prefix, so no blob is downloaded.</span></span> <span data-ttu-id="7b1da-150">Além disso, se hello opção `--recursive` não for especificado, AzCopy não transferir blobs.</span><span class="sxs-lookup"><span data-stu-id="7b1da-150">In addition, if hello option `--recursive` is not specified, AzCopy does not download any blobs.</span></span>

### <a name="set-hello-last-modified-time-of-exported-files-toobe-same-as-hello-source-blobs"></a><span data-ttu-id="7b1da-151">Definir a hora de Olá última modificação de ficheiros exportados toobe igual ao hello blobs de origem</span><span class="sxs-lookup"><span data-stu-id="7b1da-151">Set hello last-modified time of exported files toobe same as hello source blobs</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination "/mnt/myfiles" \
    --source-key <key> \
    --preserve-last-modified-time
```

<span data-ttu-id="7b1da-152">Também pode excluir os blobs de operação de transferência de Olá com base na respetiva tempo last-modified.</span><span class="sxs-lookup"><span data-stu-id="7b1da-152">You can also exclude blobs from hello download operation based on their last-modified time.</span></span> <span data-ttu-id="7b1da-153">Por exemplo, se pretender que os blobs tooexclude cuja hora da última modificação é Olá igual ou mais recente do que o ficheiro de destino Olá, adicionar Olá `--exclude-newer` opção:</span><span class="sxs-lookup"><span data-stu-id="7b1da-153">For example, if you want tooexclude blobs whose last modified time is hello same or newer than hello destination file, add hello `--exclude-newer` option:</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --preserve-last-modified-time \
    --exclude-newer
```

<span data-ttu-id="7b1da-154">Ou se pretender que os blobs tooexclude cuja hora da última modificação é Olá igual ou mais antiga do que o ficheiro de destino Olá, adicione Olá `--exclude-older` opção:</span><span class="sxs-lookup"><span data-stu-id="7b1da-154">Or if you want tooexclude blobs whose last modified time is hello same or older than hello destination file, add hello `--exclude-older` option:</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --preserve-last-modified-time \
    --exclude-older
```

## <a name="blob-upload"></a><span data-ttu-id="7b1da-155">Blob: carregar</span><span class="sxs-lookup"><span data-stu-id="7b1da-155">Blob: Upload</span></span>
### <a name="upload-single-file"></a><span data-ttu-id="7b1da-156">Carregar ficheiro único</span><span class="sxs-lookup"><span data-stu-id="7b1da-156">Upload single file</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --include "abc.txt"
```

<span data-ttu-id="7b1da-157">Se Olá o contentor de destino especificado não existe, o AzCopy criá-lo e carregamentos Olá ficheiro para a mesma.</span><span class="sxs-lookup"><span data-stu-id="7b1da-157">If hello specified destination container does not exist, AzCopy creates it and uploads hello file into it.</span></span>

### <a name="upload-single-file-toovirtual-directory"></a><span data-ttu-id="7b1da-158">Carregar ficheiro único diretório toovirtual</span><span class="sxs-lookup"><span data-stu-id="7b1da-158">Upload single file toovirtual directory</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --include "abc.txt"
```

<span data-ttu-id="7b1da-159">Se Olá especificado diretório virtual não existe, o AzCopy carrega Olá tooinclude Olá virtual diretório do ficheiro no nome do blob Olá (*por exemplo,*, `vd/abc.txt` no exemplo Olá acima).</span><span class="sxs-lookup"><span data-stu-id="7b1da-159">If hello specified virtual directory does not exist, AzCopy uploads hello file tooinclude hello virtual directory in hello blob name (*e.g.*, `vd/abc.txt` in hello example above).</span></span>

### <a name="upload-all-files"></a><span data-ttu-id="7b1da-160">Carregar todos os ficheiros</span><span class="sxs-lookup"><span data-stu-id="7b1da-160">Upload all files</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --recursive
```

<span data-ttu-id="7b1da-161">Especificar a opção `--recursive` carregamentos Olá conteúdo Olá especificado diretório tooBlob armazenamento recursiva, o que significa que todas as subpastas e os ficheiros são carregados bem.</span><span class="sxs-lookup"><span data-stu-id="7b1da-161">Specifying option `--recursive` uploads hello contents of hello specified directory tooBlob storage recursively, meaning that all subfolders and their files are uploaded as well.</span></span> <span data-ttu-id="7b1da-162">Por exemplo, suponha o seguinte Olá residem os ficheiros na pasta `/mnt/myfiles`:</span><span class="sxs-lookup"><span data-stu-id="7b1da-162">For instance, assume hello following files reside in folder `/mnt/myfiles`:</span></span>

```
/mnt/myfiles/abc.txt
/mnt/myfiles/abc1.txt
/mnt/myfiles/abc2.txt
/mnt/myfiles/subfolder/a.txt
/mnt/myfiles/subfolder/abcd.txt
```

<span data-ttu-id="7b1da-163">Após a operação de carregamento de Olá, o contentor de Olá inclui Olá os seguintes ficheiros:</span><span class="sxs-lookup"><span data-stu-id="7b1da-163">After hello upload operation, hello container includes hello following files:</span></span>

```
abc.txt
abc1.txt
abc2.txt
subfolder/a.txt
subfolder/abcd.txt
```

<span data-ttu-id="7b1da-164">Quando Olá opção `--recursive` não for especificado, só hello seguintes três ficheiros são carregados:</span><span class="sxs-lookup"><span data-stu-id="7b1da-164">When hello option `--recursive` is not specified, only hello following three files are uploaded:</span></span>

```
abc.txt
abc1.txt
abc2.txt
```

### <a name="upload-files-matching-specified-pattern"></a><span data-ttu-id="7b1da-165">Carregar ficheiros correspondentes ao padrão especificado</span><span class="sxs-lookup"><span data-stu-id="7b1da-165">Upload files matching specified pattern</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --include "a*" \
    --recursive
```

<span data-ttu-id="7b1da-166">Partem do princípio de seguinte Olá residem os ficheiros na pasta `/mnt/myfiles`:</span><span class="sxs-lookup"><span data-stu-id="7b1da-166">Assume hello following files reside in folder `/mnt/myfiles`:</span></span>

```
/mnt/myfiles/abc.txt
/mnt/myfiles/abc1.txt
/mnt/myfiles/abc2.txt
/mnt/myfiles/xyz.txt
/mnt/myfiles/subfolder/a.txt
/mnt/myfiles/subfolder/abcd.txt
```

<span data-ttu-id="7b1da-167">Após a operação de carregamento de Olá, o contentor de Olá inclui Olá os seguintes ficheiros:</span><span class="sxs-lookup"><span data-stu-id="7b1da-167">After hello upload operation, hello container includes hello following files:</span></span>

```
abc.txt
abc1.txt
abc2.txt
subfolder/a.txt
subfolder/abcd.txt
```

<span data-ttu-id="7b1da-168">Quando Olá opção `--recursive` não for especificado, AzCopy ignora os ficheiros que estão em diretórios secundárias:</span><span class="sxs-lookup"><span data-stu-id="7b1da-168">When hello option `--recursive` is not specified, AzCopy skips files that are in sub-directories:</span></span>

```
abc.txt
abc1.txt
abc2.txt
```

### <a name="specify-hello-mime-content-type-of-a-destination-blob"></a><span data-ttu-id="7b1da-169">Especifique o tipo de conteúdo de MIME de Olá de um blob de destino</span><span class="sxs-lookup"><span data-stu-id="7b1da-169">Specify hello MIME content type of a destination blob</span></span>
<span data-ttu-id="7b1da-170">Por predefinição, AzCopy define o tipo de conteúdo de Olá de um blob de destino demasiado`application/octet-stream`.</span><span class="sxs-lookup"><span data-stu-id="7b1da-170">By default, AzCopy sets hello content type of a destination blob too`application/octet-stream`.</span></span> <span data-ttu-id="7b1da-171">No entanto, pode especificar explicitamente tipo de conteúdo de Olá através da opção de Olá `--set-content-type [content-type]`.</span><span class="sxs-lookup"><span data-stu-id="7b1da-171">However, you can explicitly specify hello content type via hello option `--set-content-type [content-type]`.</span></span> <span data-ttu-id="7b1da-172">Esta sintaxe define o tipo de conteúdo de Olá para todos os blobs numa operação de carregamento.</span><span class="sxs-lookup"><span data-stu-id="7b1da-172">This syntax sets hello content type for all blobs in an upload operation.</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/myContainer/ \
    --dest-key <key> \
    --include "ab" \
    --set-content-type "video/mp4"
```

<span data-ttu-id="7b1da-173">Se hello opção `--set-content-type` for especificado sem um valor, em seguida, o AzCopy define cada blob ou um ficheiro do tipo de conteúdo de acordo com tooits extensão de ficheiro.</span><span class="sxs-lookup"><span data-stu-id="7b1da-173">If hello option `--set-content-type` is specified without a value, then AzCopy sets each blob or file's content type according tooits file extension.</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/myContainer/ \
    --dest-key <key> \
    --include "ab" \
    --set-content-type
```

## <a name="blob-copy"></a><span data-ttu-id="7b1da-174">Blob: cópia</span><span class="sxs-lookup"><span data-stu-id="7b1da-174">Blob: Copy</span></span>
### <a name="copy-single-blob-within-storage-account"></a><span data-ttu-id="7b1da-175">Copiar blob único na conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="7b1da-175">Copy single blob within Storage account</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer1 \
    --destination https://myaccount.blob.core.windows.net/mycontainer2 \
    --source-key <key> \
    --dest-key <key> \
    --include "abc.txt"
```

<span data-ttu-id="7b1da-176">Quando copiar um blob sem - opção de cópia de sincronização, um [cópia do lado do servidor](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) é efetuar a operação.</span><span class="sxs-lookup"><span data-stu-id="7b1da-176">When you copy a blob without --sync-copy option, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="copy-single-blob-across-storage-accounts"></a><span data-ttu-id="7b1da-177">Copiar blob único em contas de armazenamento</span><span class="sxs-lookup"><span data-stu-id="7b1da-177">Copy single blob across Storage accounts</span></span>

```azcopy
azcopy \
    --source https://sourceaccount.blob.core.windows.net/mycontainer1 \
    --destination https://destaccount.blob.core.windows.net/mycontainer2 \
    --source-key <key1> \
    --dest-key <key2> \
    --include "abc.txt"
```

<span data-ttu-id="7b1da-178">Quando copiar um blob sem - opção de cópia de sincronização, um [cópia do lado do servidor](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) é efetuar a operação.</span><span class="sxs-lookup"><span data-stu-id="7b1da-178">When you copy a blob without --sync-copy option, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="copy-single-blob-from-secondary-region-tooprimary-region"></a><span data-ttu-id="7b1da-179">Copiar blob único da região de tooprimary região secundária</span><span class="sxs-lookup"><span data-stu-id="7b1da-179">Copy single blob from secondary region tooprimary region</span></span>

```azcopy
azcopy \
    --source https://myaccount1-secondary.blob.core.windows.net/mynewcontainer1 \
    --destination https://myaccount2.blob.core.windows.net/mynewcontainer2 \
    --source-key <key1> \
    --dest-key <key2> \
    --include "abc.txt"
```

<span data-ttu-id="7b1da-180">Tenha em atenção que tem de ter o armazenamento georredundante com acesso de leitura ativado.</span><span class="sxs-lookup"><span data-stu-id="7b1da-180">Note that you must have read-access geo-redundant storage enabled.</span></span>

### <a name="copy-single-blob-and-its-snapshots-across-storage-accounts"></a><span data-ttu-id="7b1da-181">Copiar blob único e o respetivos instantâneos em contas de armazenamento</span><span class="sxs-lookup"><span data-stu-id="7b1da-181">Copy single blob and its snapshots across Storage accounts</span></span>

```azcopy
azcopy \
    --source https://sourceaccount.blob.core.windows.net/mycontainer1 \
    --destination https://destaccount.blob.core.windows.net/mycontainer2 \
    --source-key <key1> \
    --dest-key <key2> \
    --include "abc.txt" \
    --include-snapshot
```

<span data-ttu-id="7b1da-182">Após a operação de cópia de Olá, um contentor de destino Olá inclui blob Olá e respetivos instantâneos.</span><span class="sxs-lookup"><span data-stu-id="7b1da-182">After hello copy operation, hello target container includes hello blob and its snapshots.</span></span> <span data-ttu-id="7b1da-183">Olá contentor inclui Olá seguinte blob e o respetivos instantâneos:</span><span class="sxs-lookup"><span data-stu-id="7b1da-183">hello container includes hello following blob and its snapshots:</span></span>

```
abc.txt
abc (2013-02-25 080757).txt
abc (2014-02-21 150331).txt
```

### <a name="synchronously-copy-blobs-across-storage-accounts"></a><span data-ttu-id="7b1da-184">Em sincronia copiar os blobs em contas de armazenamento</span><span class="sxs-lookup"><span data-stu-id="7b1da-184">Synchronously copy blobs across Storage accounts</span></span>
<span data-ttu-id="7b1da-185">AzCopy por predefinição copia dados entre dois pontos finais de armazenamento de forma assíncrona.</span><span class="sxs-lookup"><span data-stu-id="7b1da-185">AzCopy by default copies data between two storage endpoints asynchronously.</span></span> <span data-ttu-id="7b1da-186">Por conseguinte, é copiado Olá execuções de operação de cópia em segundo plano Olá utilizando a capacidade de reserva de largura de banda que não tenha nenhum SLA em termos de rápido como um blob.</span><span class="sxs-lookup"><span data-stu-id="7b1da-186">Therefore, hello copy operation runs in hello background using spare bandwidth capacity that has no SLA in terms of how fast a blob is copied.</span></span> 

<span data-ttu-id="7b1da-187">Olá `--sync-copy` opção garante que a operação de cópia de Olá obtém velocidade consistente.</span><span class="sxs-lookup"><span data-stu-id="7b1da-187">hello `--sync-copy` option ensures that hello copy operation gets consistent speed.</span></span> <span data-ttu-id="7b1da-188">AzCopy efetua a cópia síncrona Olá transferindo blobs Olá toocopy de Olá especificada de memória de toolocal de origem e, em seguida, carregá-los toohello destino de armazenamento de Blobs.</span><span class="sxs-lookup"><span data-stu-id="7b1da-188">AzCopy performs hello synchronous copy by downloading hello blobs toocopy from hello specified source toolocal memory, and then uploading them toohello Blob storage destination.</span></span>

```azcopy
azcopy \
    --source https://myaccount1.blob.core.windows.net/myContainer/ \
    --destination https://myaccount2.blob.core.windows.net/myContainer/ \
    --source-key <key1> \
    --dest-key <key2> \
    --include "ab" \
    --sync-copy
```

<span data-ttu-id="7b1da-189">`--sync-copy`pode gerar a saída adicionais custos comparadas tooasynchronous cópia.</span><span class="sxs-lookup"><span data-stu-id="7b1da-189">`--sync-copy` might generate additional egress cost compared tooasynchronous copy.</span></span> <span data-ttu-id="7b1da-190">Olá abordagem recomendada é toouse esta opção na VM do Azure, que está a ser Olá mesma região que o custo de saída tooavoid de conta de armazenamento de origem.</span><span class="sxs-lookup"><span data-stu-id="7b1da-190">hello recommended approach is toouse this option in an Azure VM, that is in hello same region as your source storage account tooavoid egress cost.</span></span>

## <a name="file-download"></a><span data-ttu-id="7b1da-191">Ficheiro: Transferir</span><span class="sxs-lookup"><span data-stu-id="7b1da-191">File: Download</span></span>
### <a name="download-single-file"></a><span data-ttu-id="7b1da-192">Transferência de ficheiro único</span><span class="sxs-lookup"><span data-stu-id="7b1da-192">Download single file</span></span>

```azcopy
azcopy \
    --source https://myaccount.file.core.windows.net/myfileshare/myfolder1/ \
    --destination /mnt/myfiles \
    --source-key <key> \
    --include "abc.txt"
```

<span data-ttu-id="7b1da-193">Se Olá especificado origem é uma partilha de ficheiros do Azure, tem de especificar se o nome de ficheiro exato de Olá, (*por exemplo,* `abc.txt`) toodownload um ficheiro único, ou especificar a opção `--recursive` toodownload todos os ficheiros numa partilha de Olá em modo recursivo.</span><span class="sxs-lookup"><span data-stu-id="7b1da-193">If hello specified source is an Azure file share, then you must either specify hello exact file name, (*e.g.* `abc.txt`) toodownload a single file, or specify option `--recursive` toodownload all files in hello share recursively.</span></span> <span data-ttu-id="7b1da-194">Tentativa de toospecify um padrão de ficheiro e a opção `--recursive` resultados em conjunto num erro.</span><span class="sxs-lookup"><span data-stu-id="7b1da-194">Attempting toospecify both a file pattern and option `--recursive` together results in an error.</span></span>

### <a name="download-all-files"></a><span data-ttu-id="7b1da-195">Transferir todos os ficheiros</span><span class="sxs-lookup"><span data-stu-id="7b1da-195">Download all files</span></span>

```azcopy
azcopy \
    --source https://myaccount.file.core.windows.net/myfileshare/ \
    --destination /mnt/myfiles \
    --source-key <key> \
    --recursive
```

<span data-ttu-id="7b1da-196">Tenha em atenção que não são transferidas quaisquer pastas vazias.</span><span class="sxs-lookup"><span data-stu-id="7b1da-196">Note that any empty folders are not downloaded.</span></span>

## <a name="file-upload"></a><span data-ttu-id="7b1da-197">Ficheiro: carregar</span><span class="sxs-lookup"><span data-stu-id="7b1da-197">File: Upload</span></span>
### <a name="upload-single-file"></a><span data-ttu-id="7b1da-198">Carregar ficheiro único</span><span class="sxs-lookup"><span data-stu-id="7b1da-198">Upload single file</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.file.core.windows.net/myfileshare/ \
    --dest-key <key> \
    --include abc.txt
```

### <a name="upload-all-files"></a><span data-ttu-id="7b1da-199">Carregar todos os ficheiros</span><span class="sxs-lookup"><span data-stu-id="7b1da-199">Upload all files</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.file.core.windows.net/myfileshare/ \
    --dest-key <key> \
    --recursive
```

<span data-ttu-id="7b1da-200">Tenha em atenção que quaisquer pastas vazias não são carregadas.</span><span class="sxs-lookup"><span data-stu-id="7b1da-200">Note that any empty folders are not uploaded.</span></span>

### <a name="upload-files-matching-specified-pattern"></a><span data-ttu-id="7b1da-201">Carregar ficheiros correspondentes ao padrão especificado</span><span class="sxs-lookup"><span data-stu-id="7b1da-201">Upload files matching specified pattern</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.file.core.windows.net/myfileshare/ \
    --dest-key <key> \
    --include "ab*" \
    --recursive
```

## <a name="file-copy"></a><span data-ttu-id="7b1da-202">Ficheiro: cópia</span><span class="sxs-lookup"><span data-stu-id="7b1da-202">File: Copy</span></span>
### <a name="copy-across-file-shares"></a><span data-ttu-id="7b1da-203">Copiar em partilhas de ficheiros</span><span class="sxs-lookup"><span data-stu-id="7b1da-203">Copy across file shares</span></span>

```azcopy
azcopy \
    --source https://myaccount1.file.core.windows.net/myfileshare1/ \
    --destination https://myaccount2.file.core.windows.net/myfileshare2/ \
    --source-key <key1> \
    --dest-key <key2> \
    --recursive
```
<span data-ttu-id="7b1da-204">Quando copiar um ficheiro através de partilhas de ficheiros, um [cópia do lado do servidor](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) é efetuar a operação.</span><span class="sxs-lookup"><span data-stu-id="7b1da-204">When you copy a file across file shares, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="copy-from-file-share-tooblob"></a><span data-ttu-id="7b1da-205">Copiar do tooblob de partilha de ficheiros</span><span class="sxs-lookup"><span data-stu-id="7b1da-205">Copy from file share tooblob</span></span>

```azcopy
azcopy \ 
    --source https://myaccount1.file.core.windows.net/myfileshare/ \
    --destination https://myaccount2.blob.core.windows.net/mycontainer/ \
    --source-key <key1> \
    --dest-key <key2> \
    --recursive
```
<span data-ttu-id="7b1da-206">Quando copiar um ficheiro de tooblob de partilha de ficheiros, um [cópia do lado do servidor](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) é efetuar a operação.</span><span class="sxs-lookup"><span data-stu-id="7b1da-206">When you copy a file from file share tooblob, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="copy-from-blob-toofile-share"></a><span data-ttu-id="7b1da-207">Copiar de blob toofile partilha</span><span class="sxs-lookup"><span data-stu-id="7b1da-207">Copy from blob toofile share</span></span>

```azcopy
azcopy \
    --source https://myaccount1.blob.core.windows.net/mycontainer/ \
    --destination https://myaccount2.file.core.windows.net/myfileshare/ \
    --source-key <key1> \
    --dest-key <key2> \
    --recursive
```
<span data-ttu-id="7b1da-208">Quando copiar um ficheiro de partilha de toofile de blob, um [cópia do lado do servidor](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) é efetuar a operação.</span><span class="sxs-lookup"><span data-stu-id="7b1da-208">When you copy a file from blob toofile share, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="synchronously-copy-files"></a><span data-ttu-id="7b1da-209">Em sincronia copiar ficheiros</span><span class="sxs-lookup"><span data-stu-id="7b1da-209">Synchronously copy files</span></span>
<span data-ttu-id="7b1da-210">Pode especificar Olá `--sync-copy` opção toocopy dados tooFile de armazenamento de ficheiros armazenamento, do armazenamento de ficheiros tooBlob armazenamento e de armazenamento de BLOBs tooFile armazenamento de forma síncrona.</span><span class="sxs-lookup"><span data-stu-id="7b1da-210">You can specify hello `--sync-copy` option toocopy data from File Storage tooFile Storage, from File Storage tooBlob Storage and from Blob Storage tooFile Storage synchronously.</span></span> <span data-ttu-id="7b1da-211">AzCopy executa esta operação ao descarregar Olá origem dados toolocal de memória e, em seguida, carregá-lo toodestination.</span><span class="sxs-lookup"><span data-stu-id="7b1da-211">AzCopy runs this operation by downloading hello source data toolocal memory, and then uploading it toodestination.</span></span> <span data-ttu-id="7b1da-212">Neste caso, o custo de saída padrão se aplica.</span><span class="sxs-lookup"><span data-stu-id="7b1da-212">In this case, standard egress cost applies.</span></span>

```azcopy
azcopy \
    --source https://myaccount1.file.core.windows.net/myfileshare1/ \
    --destination https://myaccount2.file.core.windows.net/myfileshare2/ \
    --source-key <key1> \
    --dest-key <key2> \
    --recursive \
    --sync-copy
```

<span data-ttu-id="7b1da-213">Quando copiar do File Storage tooBlob armazenamento, é de tipo de blob predefinido Olá BLOBs de blocos, o utilizador pode especificar a opção `/BlobType:page` toochange Olá tipo de blob de destino.</span><span class="sxs-lookup"><span data-stu-id="7b1da-213">When copying from File Storage tooBlob Storage, hello default blob type is block blob, user can specify option `/BlobType:page` toochange hello destination blob type.</span></span>

<span data-ttu-id="7b1da-214">Tenha em atenção que `--sync-copy` poderá gerar a saída adicional custo compara tooasynchronous cópia.</span><span class="sxs-lookup"><span data-stu-id="7b1da-214">Note that `--sync-copy` might generate additional egress cost comparing tooasynchronous copy.</span></span> <span data-ttu-id="7b1da-215">Olá abordagem recomendada é toouse esta opção na VM do Azure, que está a ser Olá mesma região que o custo de saída tooavoid de conta de armazenamento de origem.</span><span class="sxs-lookup"><span data-stu-id="7b1da-215">hello recommended approach is toouse this option in an Azure VM, that is in hello same region as your source storage account tooavoid egress cost.</span></span>

## <a name="other-azcopy-features"></a><span data-ttu-id="7b1da-216">Outras funcionalidades do AzCopy</span><span class="sxs-lookup"><span data-stu-id="7b1da-216">Other AzCopy features</span></span>
### <a name="only-copy-data-that-doesnt-exist-in-hello-destination"></a><span data-ttu-id="7b1da-217">Apenas os dados de cópia que não existem no destino Olá</span><span class="sxs-lookup"><span data-stu-id="7b1da-217">Only copy data that doesn't exist in hello destination</span></span>
<span data-ttu-id="7b1da-218">Olá `--exclude-older` e `--exclude-newer` parâmetros permitem tooexclude recursos de origem de anterior ou mais recente de ser copiado, respetivamente.</span><span class="sxs-lookup"><span data-stu-id="7b1da-218">hello `--exclude-older` and `--exclude-newer` parameters allow you tooexclude older or newer source resources from being copied, respectively.</span></span> <span data-ttu-id="7b1da-219">Se pretender apenas toocopy recursos de origem que não existem no destino Olá, pode especificar os dois parâmetros na Olá comandos do AzCopy:</span><span class="sxs-lookup"><span data-stu-id="7b1da-219">If you only want toocopy source resources that don't exist in hello destination, you can specify both parameters in hello AzCopy command:</span></span>

    --source http://myaccount.blob.core.windows.net/mycontainer --destination /mnt/myfiles --source-key <sourcekey> --recursive --exclude-older --exclude-newer

    --source /mnt/myfiles --destination http://myaccount.file.core.windows.net/myfileshare --dest-key <destkey> --recursive --exclude-older --exclude-newer

    --source http://myaccount.blob.core.windows.net/mycontainer --destination http://myaccount.blob.core.windows.net/mycontainer1 --source-key <sourcekey> --dest-key <destkey> --recursive --exclude-older --exclude-newer

### <a name="use-a-configuration-file-toospecify-command-line-parameters"></a><span data-ttu-id="7b1da-220">Utilizar um toospecify de ficheiro de configuração para parâmetros de linha de comandos</span><span class="sxs-lookup"><span data-stu-id="7b1da-220">Use a configuration file toospecify command-line parameters</span></span>

```azcopy
azcopy --config-file "azcopy-config.ini"
```

<span data-ttu-id="7b1da-221">Pode incluir quaisquer parâmetros de linha de comandos do AzCopy num ficheiro de configuração.</span><span class="sxs-lookup"><span data-stu-id="7b1da-221">You can include any AzCopy command-line parameters in a configuration file.</span></span> <span data-ttu-id="7b1da-222">Processos do AzCopy Olá parâmetros no ficheiro de Olá como se tivesse sido especificados na linha de comandos Olá, efetuar uma substituição direta com conteúdo Olá do ficheiro de Olá.</span><span class="sxs-lookup"><span data-stu-id="7b1da-222">AzCopy processes hello parameters in hello file as if they had been specified on hello command line, performing a direct substitution with hello contents of hello file.</span></span>

<span data-ttu-id="7b1da-223">Partem do princípio de um ficheiro de configuração com o nome `copyoperation`, que contém Olá seguintes linhas.</span><span class="sxs-lookup"><span data-stu-id="7b1da-223">Assume a configuration file named `copyoperation`, that contains hello following lines.</span></span> <span data-ttu-id="7b1da-224">Cada parâmetro do AzCopy pode ser especificado numa única linha.</span><span class="sxs-lookup"><span data-stu-id="7b1da-224">Each AzCopy parameter can be specified on a single line.</span></span>

    --source http://myaccount.blob.core.windows.net/mycontainer --destination /mnt/myfiles --source-key <sourcekey> --recursive --quiet

<span data-ttu-id="7b1da-225">ou, no separar linhas:</span><span class="sxs-lookup"><span data-stu-id="7b1da-225">or on separate lines:</span></span>

    --source http://myaccount.blob.core.windows.net/mycontainer
    --destination /mnt/myfiles
    --source-key<sourcekey>
    --recursive
    --quiet

<span data-ttu-id="7b1da-226">AzCopy falha se dividir parâmetro Olá por duas linhas, conforme mostrado aqui para Olá `--source-key` parâmetro:</span><span class="sxs-lookup"><span data-stu-id="7b1da-226">AzCopy fails if you split hello parameter across two lines, as shown here for hello `--source-key` parameter:</span></span>

    http://myaccount.blob.core.windows.net/mycontainer
    /mnt/myfiles
    --sourcekey
    <sourcekey>
    --recursive
    --quiet

### <a name="specify-a-shared-access-signature-sas"></a><span data-ttu-id="7b1da-227">Especifique uma assinatura de acesso partilhado (SAS)</span><span class="sxs-lookup"><span data-stu-id="7b1da-227">Specify a shared access signature (SAS)</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer1 \
    --destination https://myaccount.blob.core.windows.net/mycontainer2 \
    --source-sas <SAS1> \
    --dest-sas <SAS2> \
    --include abc.txt
```

<span data-ttu-id="7b1da-228">Também pode especificar uma SAS no contentor de Olá URI:</span><span class="sxs-lookup"><span data-stu-id="7b1da-228">You can also specify a SAS on hello container URI:</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer1/?SourceSASToken \
    --destination /mnt/myfiles \
    --recursive
```

<span data-ttu-id="7b1da-229">Tenha em atenção que AzCopy atualmente suporta apenas Olá [conta SAS](https://docs.microsoft.com/en-us/azure/storage/storage-dotnet-shared-access-signature-part-1).</span><span class="sxs-lookup"><span data-stu-id="7b1da-229">Note that AzCopy currently only supports hello [Account SAS](https://docs.microsoft.com/en-us/azure/storage/storage-dotnet-shared-access-signature-part-1).</span></span>

### <a name="journal-file-folder"></a><span data-ttu-id="7b1da-230">Pasta de ficheiros do diário de alterações</span><span class="sxs-lookup"><span data-stu-id="7b1da-230">Journal file folder</span></span>
<span data-ttu-id="7b1da-231">Sempre que emitir um comando tooAzCopy, este verifica se existe um ficheiro de diário de alterações na pasta predefinida de hello, ou se existe uma pasta que especificou através desta opção.</span><span class="sxs-lookup"><span data-stu-id="7b1da-231">Each time you issue a command tooAzCopy, it checks whether a journal file exists in hello default folder, or whether it exists in a folder that you specified via this option.</span></span> <span data-ttu-id="7b1da-232">Se não existir um ficheiro do diário de alterações de Olá em qualquer local, o AzCopy trata operação Olá como novo e gera um novo ficheiro de diário de alterações.</span><span class="sxs-lookup"><span data-stu-id="7b1da-232">If hello journal file does not exist in either place, AzCopy treats hello operation as new and generates a new journal file.</span></span>

<span data-ttu-id="7b1da-233">Se existirem ficheiros do diário de alterações de Olá, o AzCopy verifica se linha de comandos de Olá introduzido corresponde a linha de comandos Olá no ficheiro de diário Olá.</span><span class="sxs-lookup"><span data-stu-id="7b1da-233">If hello journal file does exist, AzCopy checks whether hello command line that you input matches hello command line in hello journal file.</span></span> <span data-ttu-id="7b1da-234">Se duas linhas de comando Olá corresponderem, o AzCopy retoma operação incompleta Olá.</span><span class="sxs-lookup"><span data-stu-id="7b1da-234">If hello two command lines match, AzCopy resumes hello incomplete operation.</span></span> <span data-ttu-id="7b1da-235">Se não corresponderem, o AzCopy pede ao utilizador tooeither substituir Olá diário ficheiro toostart uma operação de novo ou a operação atual do toocancel Olá.</span><span class="sxs-lookup"><span data-stu-id="7b1da-235">If they do not match, AzCopy prompts user tooeither overwrite hello journal file toostart a new operation, or toocancel hello current operation.</span></span>

<span data-ttu-id="7b1da-236">Se pretender que a localização predefinida de Olá de toouse para o ficheiro do diário de alterações de Olá:</span><span class="sxs-lookup"><span data-stu-id="7b1da-236">If you want toouse hello default location for hello journal file:</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --resume
```

<span data-ttu-id="7b1da-237">Se omitir opção `--resume`, ou especificar a opção `--resume` sem o caminho da pasta Olá, conforme mostrado acima, o AzCopy cria Olá diário ficheiro na localização predefinida de Olá, que é `~\Microsoft\Azure\AzCopy`.</span><span class="sxs-lookup"><span data-stu-id="7b1da-237">If you omit option `--resume`, or specify option `--resume` without hello folder path, as shown above, AzCopy creates hello journal file in hello default location, which is `~\Microsoft\Azure\AzCopy`.</span></span> <span data-ttu-id="7b1da-238">Se já existir um ficheiro do diário de alterações de Olá, o AzCopy retoma operação Olá com base num ficheiro do diário de alterações de Olá.</span><span class="sxs-lookup"><span data-stu-id="7b1da-238">If hello journal file already exists, then AzCopy resumes hello operation based on hello journal file.</span></span>

<span data-ttu-id="7b1da-239">Se quiser toospecify numa localização personalizada para o ficheiro do diário de alterações de Olá:</span><span class="sxs-lookup"><span data-stu-id="7b1da-239">If you want toospecify a custom location for hello journal file:</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key key \
    --resume "/mnt/myjournal"
```

<span data-ttu-id="7b1da-240">Este exemplo cria ficheiros do diário de alterações de Olá se já existir.</span><span class="sxs-lookup"><span data-stu-id="7b1da-240">This example creates hello journal file if it does not already exist.</span></span> <span data-ttu-id="7b1da-241">Se existir, o AzCopy retoma operação Olá com base num ficheiro do diário de alterações de Olá.</span><span class="sxs-lookup"><span data-stu-id="7b1da-241">If it does exist, then AzCopy resumes hello operation based on hello journal file.</span></span>

<span data-ttu-id="7b1da-242">Se quiser tooresume uma operação do AzCopy, repetir Olá mesmo comando.</span><span class="sxs-lookup"><span data-stu-id="7b1da-242">If you want tooresume an AzCopy operation, repeat hello same command.</span></span> <span data-ttu-id="7b1da-243">AzCopy no Linux, em seguida, irá pedir confirmação:</span><span class="sxs-lookup"><span data-stu-id="7b1da-243">AzCopy on Linux then will prompt for confirmation:</span></span>

```azcopy
Incomplete operation with same command line detected at hello journal directory "/home/myaccount/Microsoft/Azure/AzCopy", do you want tooresume hello operation? Choose Yes tooresume, choose No toooverwrite hello journal toostart a new operation. (Yes/No)
```

### <a name="output-verbose-logs"></a><span data-ttu-id="7b1da-244">Registos verbosos de saída</span><span class="sxs-lookup"><span data-stu-id="7b1da-244">Output verbose logs</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --verbose
```

### <a name="specify-hello-number-of-concurrent-operations-toostart"></a><span data-ttu-id="7b1da-245">Especifique o número de Olá de operações simultâneas toostart</span><span class="sxs-lookup"><span data-stu-id="7b1da-245">Specify hello number of concurrent operations toostart</span></span>
<span data-ttu-id="7b1da-246">Opção `--parallel-level` Especifica o número de Olá de operações de cópia em simultâneo.</span><span class="sxs-lookup"><span data-stu-id="7b1da-246">Option `--parallel-level` specifies hello number of concurrent copy operations.</span></span> <span data-ttu-id="7b1da-247">Por predefinição, o AzCopy é iniciado um determinado número de débito de transferência de dados de Olá tooincrease operações simultâneas.</span><span class="sxs-lookup"><span data-stu-id="7b1da-247">By default, AzCopy starts a certain number of concurrent operations tooincrease hello data transfer throughput.</span></span> <span data-ttu-id="7b1da-248">número de Olá de operações simultâneas de é igual Olá, número de processadores tiver oito horas.</span><span class="sxs-lookup"><span data-stu-id="7b1da-248">hello number of concurrent operations is equal eight times hello number of processors you have.</span></span> <span data-ttu-id="7b1da-249">Se estiver a executar o AzCopy através de uma rede de largura de banda reduzida, pode especificar um número inferior de - falha de tooavoid de nível de paralelo provocada por concorrência de recursos.</span><span class="sxs-lookup"><span data-stu-id="7b1da-249">If you are running AzCopy across a low-bandwidth network, you can specify a lower number for --parallel-level tooavoid failure caused by resource competition.</span></span>

[!TIP]
><span data-ttu-id="7b1da-250">lista completa de Olá tooview dos parâmetros do AzCopy, consulte 'azcopy – Ajuda' menu.</span><span class="sxs-lookup"><span data-stu-id="7b1da-250">tooview hello complete list of AzCopy parameters, check out 'azcopy --help' menu.</span></span>

## <a name="known-issues-and-best-practices"></a><span data-ttu-id="7b1da-251">Problemas conhecidos e melhores práticas</span><span class="sxs-lookup"><span data-stu-id="7b1da-251">Known issues and best practices</span></span>
### <a name="error-net-core-is-not-found-in-hello-system"></a><span data-ttu-id="7b1da-252">Erro: .NET Core não foi encontrado no sistema de Olá.</span><span class="sxs-lookup"><span data-stu-id="7b1da-252">Error: .NET Core is not found in hello system.</span></span>
<span data-ttu-id="7b1da-253">Se ocorrer um erro a indicar que o .NET Core não está instalado no sistema de Olá, Olá binário do caminho toohello .NET Core `dotnet` poderá estar em falta.</span><span class="sxs-lookup"><span data-stu-id="7b1da-253">If you encounter an error stating that .NET Core is not installed in hello system, hello PATH toohello .NET Core binary `dotnet` may be missing.</span></span>

<span data-ttu-id="7b1da-254">Na ordem tooaddress este problema, localizar binário de .NET Core Olá no sistema de Olá:</span><span class="sxs-lookup"><span data-stu-id="7b1da-254">In order tooaddress this issue, find hello .NET Core binary in hello system:</span></span>
```bash
sudo find / -name dotnet
```

<span data-ttu-id="7b1da-255">Esta ação devolve Olá caminho toohello dotnet binário.</span><span class="sxs-lookup"><span data-stu-id="7b1da-255">This returns hello path toohello dotnet binary.</span></span> 

    /opt/rh/rh-dotnetcore11/root/usr/bin/dotnet
    /opt/rh/rh-dotnetcore11/root/usr/lib64/dotnetcore/dotnet
    /opt/rh/rh-dotnetcore11/root/usr/lib64/dotnetcore/shared/Microsoft.NETCore.App/1.1.2/dotnet

<span data-ttu-id="7b1da-256">Agora, adicione esta variável de caminho de toohello do caminho.</span><span class="sxs-lookup"><span data-stu-id="7b1da-256">Now add this path toohello PATH variable.</span></span> <span data-ttu-id="7b1da-257">Para o sudo, edição secure_path toocontain Olá caminho toohello dotnet binário:</span><span class="sxs-lookup"><span data-stu-id="7b1da-257">For sudo, edit secure_path toocontain hello path toohello dotnet binary:</span></span>
```bash 
sudo visudo
### Append hello path found in hello preceding example too'secure_path' variable
```

<span data-ttu-id="7b1da-258">Neste exemplo, a variável de secure_path lê como:</span><span class="sxs-lookup"><span data-stu-id="7b1da-258">In this example, secure_path variable reads as:</span></span>

```
secure_path = /sbin:/bin:/usr/sbin:/usr/bin:/opt/rh/rh-dotnetcore11/root/usr/bin/
```

<span data-ttu-id="7b1da-259">Para o utilizador atual Olá, editar.bash_profile/.profile tooinclude Olá caminho toohello dotnet binário na variável de caminho</span><span class="sxs-lookup"><span data-stu-id="7b1da-259">For hello current user, edit .bash_profile/.profile tooinclude hello path toohello dotnet binary in PATH variable</span></span> 
```bash
vi ~/.bash_profile
### Append hello path found in hello preceding example too'PATH' variable
```

<span data-ttu-id="7b1da-260">Certifique-se de que o .NET Core está agora no caminho:</span><span class="sxs-lookup"><span data-stu-id="7b1da-260">Verify that .NET Core is now in PATH:</span></span>
```bash
which dotnet
sudo which dotnet
```

### <a name="error-installing-azcopy"></a><span data-ttu-id="7b1da-261">Erro ao instalar o AzCopy</span><span class="sxs-lookup"><span data-stu-id="7b1da-261">Error Installing AzCopy</span></span>
<span data-ttu-id="7b1da-262">Se ocorrerem problemas com a instalação do AzCopy, tente toorun AzCopy utilizando scripts de bash Olá no Olá extraído `azcopy` pasta.</span><span class="sxs-lookup"><span data-stu-id="7b1da-262">If you encounter issues with AzCopy installation, you may try toorun AzCopy using hello bash script in hello extracted `azcopy` folder.</span></span>

```bash
cd azcopy
./azcopy
```

### <a name="limit-concurrent-writes-while-copying-data"></a><span data-ttu-id="7b1da-263">Limitar escritas em simultâneo ao copiar dados</span><span class="sxs-lookup"><span data-stu-id="7b1da-263">Limit concurrent writes while copying data</span></span>
<span data-ttu-id="7b1da-264">Quando copia blobs ou ficheiros com o AzCopy, tenha em atenção que outra aplicação pode ser modificar Olá dados enquanto estiver a copiar.</span><span class="sxs-lookup"><span data-stu-id="7b1da-264">When you copy blobs or files with AzCopy, keep in mind that another application may be modifying hello data while you are copying it.</span></span> <span data-ttu-id="7b1da-265">Se for possível, certifique-se de que os dados de Olá que estiver a copiar não está a ser modificados durante a operação de cópia de Olá.</span><span class="sxs-lookup"><span data-stu-id="7b1da-265">If possible, ensure that hello data you are copying is not being modified during hello copy operation.</span></span> <span data-ttu-id="7b1da-266">Por exemplo, quando copiar um VHD associado uma máquina virtual do Azure, certifique-se de que não existem outras aplicações atualmente estiver a escrever toohello VHD.</span><span class="sxs-lookup"><span data-stu-id="7b1da-266">For example, when copying a VHD associated with an Azure virtual machine, make sure that no other applications are currently writing toohello VHD.</span></span> <span data-ttu-id="7b1da-267">Uma boa forma toodo trata por leasing Olá recursos toobe copiado.</span><span class="sxs-lookup"><span data-stu-id="7b1da-267">A good way toodo this is by leasing hello resource toobe copied.</span></span> <span data-ttu-id="7b1da-268">Em alternativa, pode criar um instantâneo do VHD de Olá primeiro e, em seguida, copiar o instantâneo de Olá.</span><span class="sxs-lookup"><span data-stu-id="7b1da-268">Alternately, you can create a snapshot of hello VHD first and then copy hello snapshot.</span></span>

<span data-ttu-id="7b1da-269">Se não podem impedir outras aplicações de escrever tooblobs ou ficheiros, enquanto que estão a ser copiados, em seguida, tenha em atenção que, pela tarefa de Olá Olá tempo é concluída, hello recursos copiados podem já não ter paridade completa com recursos de origem Olá.</span><span class="sxs-lookup"><span data-stu-id="7b1da-269">If you cannot prevent other applications from writing tooblobs or files while they are being copied, then keep in mind that by hello time hello job finishes, hello copied resources may no longer have full parity with hello source resources.</span></span>

### <a name="run-one-azcopy-instance-on-one-machine"></a><span data-ttu-id="7b1da-270">Execute uma instância do AzCopy num computador.</span><span class="sxs-lookup"><span data-stu-id="7b1da-270">Run one AzCopy instance on one machine.</span></span>
<span data-ttu-id="7b1da-271">O AzCopy é concebida toomaximize Olá utilização sua máquina recursos tooaccelerate Olá da transferência de dados, recomendamos que execute apenas uma instância do AzCopy num computador e especificar a opção de Olá `--parallel-level` se precisar de mais simultâneas operações.</span><span class="sxs-lookup"><span data-stu-id="7b1da-271">AzCopy is designed toomaximize hello utilization of your machine resource tooaccelerate hello data transfer, we recommend you run only one AzCopy instance on one machine, and specify hello option `--parallel-level` if you need more concurrent operations.</span></span> <span data-ttu-id="7b1da-272">Para obter mais detalhes, escreva `AzCopy --help parallel-level` na linha de comandos Olá.</span><span class="sxs-lookup"><span data-stu-id="7b1da-272">For more details, type `AzCopy --help parallel-level` at hello command line.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7b1da-273">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="7b1da-273">Next steps</span></span>
<span data-ttu-id="7b1da-274">Para obter mais informações sobre o Storage do Azure e AzCopy, consulte Olá os seguintes recursos:</span><span class="sxs-lookup"><span data-stu-id="7b1da-274">For more information about Azure Storage and AzCopy, see hello following resources:</span></span>

### <a name="azure-storage-documentation"></a><span data-ttu-id="7b1da-275">Documentação do Storage do Azure:</span><span class="sxs-lookup"><span data-stu-id="7b1da-275">Azure Storage documentation:</span></span>
* [<span data-ttu-id="7b1da-276">Introdução tooAzure armazenamento</span><span class="sxs-lookup"><span data-stu-id="7b1da-276">Introduction tooAzure Storage</span></span>](storage-introduction.md)
* [<span data-ttu-id="7b1da-277">Criar uma conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="7b1da-277">Create a storage account</span></span>](storage-create-storage-account.md)
* [<span data-ttu-id="7b1da-278">Gerir a blobs com o Explorador de armazenamento</span><span class="sxs-lookup"><span data-stu-id="7b1da-278">Manage blobs with Storage Explorer</span></span>](https://docs.microsoft.com/en-us/azure/vs-azure-tools-storage-explorer-blobs)
* [<span data-ttu-id="7b1da-279">Utilizar Olá 2.0 de CLI do Azure com o Storage do Azure</span><span class="sxs-lookup"><span data-stu-id="7b1da-279">Using hello Azure CLI 2.0 with Azure Storage</span></span>](storage-azure-cli.md)
* [<span data-ttu-id="7b1da-280">Como toouse Blob storage do C++</span><span class="sxs-lookup"><span data-stu-id="7b1da-280">How toouse Blob storage from C++</span></span>](storage-c-plus-plus-how-to-use-blobs.md)
* [<span data-ttu-id="7b1da-281">Como toouse Blob storage do Java</span><span class="sxs-lookup"><span data-stu-id="7b1da-281">How toouse Blob storage from Java</span></span>](storage-java-how-to-use-blob-storage.md)
* [<span data-ttu-id="7b1da-282">Como toouse Blob storage do Node.js</span><span class="sxs-lookup"><span data-stu-id="7b1da-282">How toouse Blob storage from Node.js</span></span>](storage-nodejs-how-to-use-blob-storage.md)
* [<span data-ttu-id="7b1da-283">Como toouse Blob storage do Python</span><span class="sxs-lookup"><span data-stu-id="7b1da-283">How toouse Blob storage from Python</span></span>](storage-python-how-to-use-blob-storage.md)

### <a name="azure-storage-blog-posts"></a><span data-ttu-id="7b1da-284">Mensagens de blogue de armazenamento do Azure:</span><span class="sxs-lookup"><span data-stu-id="7b1da-284">Azure Storage blog posts:</span></span>
* [<span data-ttu-id="7b1da-285">Anunciar AzCopy na pré-visualização do Linux</span><span class="sxs-lookup"><span data-stu-id="7b1da-285">Announcing AzCopy on Linux Preview</span></span>](https://azure.microsoft.com/en-in/blog/announcing-azcopy-on-linux-preview/)
* [<span data-ttu-id="7b1da-286">Introdução ao pré-visualização de biblioteca de movimento de dados de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="7b1da-286">Introducing Azure Storage Data Movement Library Preview</span></span>](https://azure.microsoft.com/blog/introducing-azure-storage-data-movement-library-preview-2/)
* [<span data-ttu-id="7b1da-287">AzCopy: Introdução ao copiar síncrona e tipo de conteúdo personalizado</span><span class="sxs-lookup"><span data-stu-id="7b1da-287">AzCopy: Introducing synchronous copy and customized content type</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2015/01/13/azcopy-introducing-synchronous-copy-and-customized-content-type.aspx)
* [<span data-ttu-id="7b1da-288">AzCopy: Anunciar disponibilidade geral do 3.0 AzCopy plus versão de pré-visualização do AzCopy 4.0 com suporte de tabela e ficheiro</span><span class="sxs-lookup"><span data-stu-id="7b1da-288">AzCopy: Announcing General Availability of AzCopy 3.0 plus preview release of AzCopy 4.0 with Table and File support</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/10/29/azcopy-announcing-general-availability-of-azcopy-3-0-plus-preview-release-of-azcopy-4-0-with-table-and-file-support.aspx)
* [<span data-ttu-id="7b1da-289">AzCopy: Otimizado para cenários de cópia em grande escala</span><span class="sxs-lookup"><span data-stu-id="7b1da-289">AzCopy: Optimized for Large-Scale Copy Scenarios</span></span>](http://go.microsoft.com/fwlink/?LinkId=507682)
* [<span data-ttu-id="7b1da-290">AzCopy: Suporte para o armazenamento georredundante com acesso de leitura</span><span class="sxs-lookup"><span data-stu-id="7b1da-290">AzCopy: Support for read-access geo-redundant storage</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/04/07/azcopy-support-for-read-access-geo-redundant-account.aspx)
* [<span data-ttu-id="7b1da-291">AzCopy: Transferir dados com o SAS token e o modo reiniciável</span><span class="sxs-lookup"><span data-stu-id="7b1da-291">AzCopy: Transfer data with restartable mode and SAS token</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2013/09/07/azcopy-transfer-data-with-re-startable-mode-and-sas-token.aspx)
* [<span data-ttu-id="7b1da-292">AzCopy: Utilizando o Blob de cópia de conta em vários locais</span><span class="sxs-lookup"><span data-stu-id="7b1da-292">AzCopy: Using cross-account Copy Blob</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2013/04/01/azcopy-using-cross-account-copy-blob.aspx)
* [<span data-ttu-id="7b1da-293">AzCopy: Carregar/transferência de ficheiros para Blobs do Azure</span><span class="sxs-lookup"><span data-stu-id="7b1da-293">AzCopy: Uploading/downloading files for Azure Blobs</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/12/03/azcopy-uploading-downloading-files-for-windows-azure-blobs.aspx)

