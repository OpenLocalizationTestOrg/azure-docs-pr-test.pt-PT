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
# <a name="transfer-data-with-hello-azcopy-on-windows"></a><span data-ttu-id="8d81e-105">Transferência de dados com Olá AzCopy no Windows</span><span class="sxs-lookup"><span data-stu-id="8d81e-105">Transfer data with hello AzCopy on Windows</span></span>
<span data-ttu-id="8d81e-106">O AzCopy é um utilitário da linha de comandos concebido para copiar dados tooand do armazenamento de Blobs do Microsoft Azure, ficheiros e tabela utilizando comandos simples com um desempenho ideal.</span><span class="sxs-lookup"><span data-stu-id="8d81e-106">AzCopy is a command-line utility designed for copying data tooand from Microsoft Azure Blob, File, and Table storage using simple commands with optimal performance.</span></span> <span data-ttu-id="8d81e-107">Pode copiar dados de um objeto tooanother dentro da sua conta de armazenamento, ou entre contas de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="8d81e-107">You can copy data from one object tooanother within your storage account, or between storage accounts.</span></span>

<span data-ttu-id="8d81e-108">Existem duas versões do AzCopy que pode transferir.</span><span class="sxs-lookup"><span data-stu-id="8d81e-108">There are two versions of AzCopy that you can download.</span></span> <span data-ttu-id="8d81e-109">AzCopy no Windows baseia-se com o .NET Framework e o estilo de Windows esta oferece opções de linha de comandos.</span><span class="sxs-lookup"><span data-stu-id="8d81e-109">AzCopy on Windows is built with .NET Framework, and offers Windows style command-line options.</span></span> <span data-ttu-id="8d81e-110">[AzCopy no Linux](storage-use-azcopy-linux.md) baseia-se com o .NET Core Framework que está direcionada para plataformas Linux oferta estilo POSIX opções da linha de comandos.</span><span class="sxs-lookup"><span data-stu-id="8d81e-110">[AzCopy on Linux](storage-use-azcopy-linux.md) is built with .NET Core Framework which targets Linux platforms offering POSIX style command-line options.</span></span> <span data-ttu-id="8d81e-111">Este artigo abrange AzCopy no Windows.</span><span class="sxs-lookup"><span data-stu-id="8d81e-111">This article covers AzCopy on Windows.</span></span>

## <a name="download-and-install-azcopy"></a><span data-ttu-id="8d81e-112">Transfira e instale o AzCopy</span><span class="sxs-lookup"><span data-stu-id="8d81e-112">Download and install AzCopy</span></span>
### <a name="azcopy-on-windows"></a><span data-ttu-id="8d81e-113">AzCopy no Windows</span><span class="sxs-lookup"><span data-stu-id="8d81e-113">AzCopy on Windows</span></span>
<span data-ttu-id="8d81e-114">Transferir Olá [versão mais recente do AzCopy no Windows](http://aka.ms/downloadazcopy).</span><span class="sxs-lookup"><span data-stu-id="8d81e-114">Download hello [latest version of AzCopy on Windows](http://aka.ms/downloadazcopy).</span></span>

#### <a name="installation-on-windows"></a><span data-ttu-id="8d81e-115">Instalação no Windows</span><span class="sxs-lookup"><span data-stu-id="8d81e-115">Installation on Windows</span></span>
<span data-ttu-id="8d81e-116">Depois de instalar o AzCopy no Windows utilizando o instalador Olá, abra uma janela de comandos e navegue diretório de instalação do AzCopy toohello no seu computador - onde hello `AzCopy.exe` executável está localizado.</span><span class="sxs-lookup"><span data-stu-id="8d81e-116">After installing AzCopy on Windows using hello installer, open a command window and navigate toohello AzCopy installation directory on your computer - where hello `AzCopy.exe` executable is located.</span></span> <span data-ttu-id="8d81e-117">Se assim o desejar, pode adicionar o caminho do sistema de tooyour instalação localização Olá AzCopy.</span><span class="sxs-lookup"><span data-stu-id="8d81e-117">If desired, you can add hello AzCopy installation location tooyour system path.</span></span> <span data-ttu-id="8d81e-118">Por predefinição, AzCopy é instalado demasiado`%ProgramFiles(x86)%\Microsoft SDKs\Azure\AzCopy` ou `%ProgramFiles%\Microsoft SDKs\Azure\AzCopy`.</span><span class="sxs-lookup"><span data-stu-id="8d81e-118">By default, AzCopy is installed too`%ProgramFiles(x86)%\Microsoft SDKs\Azure\AzCopy` or `%ProgramFiles%\Microsoft SDKs\Azure\AzCopy`.</span></span>

## <a name="writing-your-first-azcopy-command"></a><span data-ttu-id="8d81e-119">Escrever o seu primeiro comando do AzCopy</span><span class="sxs-lookup"><span data-stu-id="8d81e-119">Writing your first AzCopy command</span></span>
<span data-ttu-id="8d81e-120">sintaxe de básico Olá para comandos do AzCopy é:</span><span class="sxs-lookup"><span data-stu-id="8d81e-120">hello basic syntax for AzCopy commands is:</span></span>

```azcopy
AzCopy /Source:<source> /Dest:<destination> [Options]
```

<span data-ttu-id="8d81e-121">Olá seguir exemplos demonstram uma variedade de cenários para copiar dados tooand do Microsoft Azure, ficheiros, tabelas e Blobs.</span><span class="sxs-lookup"><span data-stu-id="8d81e-121">hello following examples demonstrate a variety of scenarios for copying data tooand from Microsoft Azure Blobs, Files, and Tables.</span></span> <span data-ttu-id="8d81e-122">Consulte toohello [AzCopy parâmetros](#azcopy-parameters) secção para obter uma explicação detalhada de parâmetros de Olá utilizados em cada amostra.</span><span class="sxs-lookup"><span data-stu-id="8d81e-122">Refer toohello [AzCopy Parameters](#azcopy-parameters) section for a detailed explanation of hello parameters used in each sample.</span></span>

## <a name="blob-download"></a><span data-ttu-id="8d81e-123">Blob: Transferir</span><span class="sxs-lookup"><span data-stu-id="8d81e-123">Blob: Download</span></span>
### <a name="download-single-blob"></a><span data-ttu-id="8d81e-124">Transferir BLOBs único</span><span class="sxs-lookup"><span data-stu-id="8d81e-124">Download single blob</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /Pattern:"abc.txt"
```

<span data-ttu-id="8d81e-125">Tenha em atenção que, se a pasta de Olá `C:\myfolder` não existir, AzCopy irá criá-la e transferir `abc.txt ` na nova pasta de Olá.</span><span class="sxs-lookup"><span data-stu-id="8d81e-125">Note that if hello folder `C:\myfolder` does not exist, AzCopy will create it and download `abc.txt ` into hello new folder.</span></span>

### <a name="download-single-blob-from-secondary-region"></a><span data-ttu-id="8d81e-126">Transferir BLOBs único da região secundária</span><span class="sxs-lookup"><span data-stu-id="8d81e-126">Download single blob from secondary region</span></span>

```azcopy
AzCopy /Source:https://myaccount-secondary.blob.core.windows.net/mynewcontainer /Dest:C:\myfolder /SourceKey:key /Pattern:abc.txt
```

<span data-ttu-id="8d81e-127">Tenha em atenção que tem de ter o armazenamento georredundante com acesso de leitura ativado.</span><span class="sxs-lookup"><span data-stu-id="8d81e-127">Note that you must have read-access geo-redundant storage enabled.</span></span>

### <a name="download-all-blobs"></a><span data-ttu-id="8d81e-128">Transferir todos os blobs</span><span class="sxs-lookup"><span data-stu-id="8d81e-128">Download all blobs</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /S
```

<span data-ttu-id="8d81e-129">Partem do princípio de seguinte Olá residem os blobs no contentor especificado Olá:</span><span class="sxs-lookup"><span data-stu-id="8d81e-129">Assume hello following blobs reside in hello specified container:</span></span>  

    abc.txt
    abc1.txt
    abc2.txt
    vd1\a.txt
    vd1\abcd.txt

<span data-ttu-id="8d81e-130">Após a operação de transferência Olá, Olá diretório `C:\myfolder` incluirá Olá os seguintes ficheiros:</span><span class="sxs-lookup"><span data-stu-id="8d81e-130">After hello download operation, hello directory `C:\myfolder` will include hello following files:</span></span>

    C:\myfolder\abc.txt
    C:\myfolder\abc1.txt
    C:\myfolder\abc2.txt
    C:\myfolder\vd1\a.txt
    C:\myfolder\vd1\abcd.txt

<span data-ttu-id="8d81e-131">Se não especificar opção `/S`, não existem blobs não serão transferidos.</span><span class="sxs-lookup"><span data-stu-id="8d81e-131">If you do not specify option `/S`, no blobs will be downloaded.</span></span>

### <a name="download-blobs-with-specified-prefix"></a><span data-ttu-id="8d81e-132">Transferir blobs com o prefixo especificado</span><span class="sxs-lookup"><span data-stu-id="8d81e-132">Download blobs with specified prefix</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /Pattern:a /S
```

<span data-ttu-id="8d81e-133">Partem do princípio de seguinte Olá residem os blobs no contentor especificado Olá.</span><span class="sxs-lookup"><span data-stu-id="8d81e-133">Assume hello following blobs reside in hello specified container.</span></span> <span data-ttu-id="8d81e-134">Todos os blobs a partir do prefixo de Olá `a` serão transferidos:</span><span class="sxs-lookup"><span data-stu-id="8d81e-134">All blobs beginning with hello prefix `a` will be downloaded:</span></span>

    abc.txt
    abc1.txt
    abc2.txt
    xyz.txt
    vd1\a.txt
    vd1\abcd.txt

<span data-ttu-id="8d81e-135">Após a operação de transferência Olá, Olá pasta `C:\myfolder` incluirá Olá os seguintes ficheiros:</span><span class="sxs-lookup"><span data-stu-id="8d81e-135">After hello download operation, hello folder `C:\myfolder` will include hello following files:</span></span>

    C:\myfolder\abc.txt
    C:\myfolder\abc1.txt
    C:\myfolder\abc2.txt

<span data-ttu-id="8d81e-136">prefixo de Olá aplica-se o diretório virtual de toohello, o que faz parte de primeiro Olá do nome do blob Olá.</span><span class="sxs-lookup"><span data-stu-id="8d81e-136">hello prefix applies toohello virtual directory, which forms hello first part of hello blob name.</span></span> <span data-ttu-id="8d81e-137">Exemplo de Olá mostrado acima, o diretório virtual Olá não corresponde a prefixo especificado Olá, pelo que não está a ser transferido.</span><span class="sxs-lookup"><span data-stu-id="8d81e-137">In hello example shown above, hello virtual directory does not match hello specified prefix, so it is not downloaded.</span></span> <span data-ttu-id="8d81e-138">Além disso, se hello opção `\S` não for especificado, AzCopy não poderão transferir os blobs.</span><span class="sxs-lookup"><span data-stu-id="8d81e-138">In addition, if hello option `\S` is not specified, AzCopy will not download any blobs.</span></span>

### <a name="set-hello-last-modified-time-of-exported-files-toobe-same-as-hello-source-blobs"></a><span data-ttu-id="8d81e-139">Definir a hora de Olá última modificação de ficheiros exportados toobe igual ao hello blobs de origem</span><span class="sxs-lookup"><span data-stu-id="8d81e-139">Set hello last-modified time of exported files toobe same as hello source blobs</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /MT
```

<span data-ttu-id="8d81e-140">Também pode excluir os blobs de operação de transferência de Olá com base na respetiva tempo last-modified.</span><span class="sxs-lookup"><span data-stu-id="8d81e-140">You can also exclude blobs from hello download operation based on their last-modified time.</span></span> <span data-ttu-id="8d81e-141">Por exemplo, se pretender que os blobs tooexclude cuja hora da última modificação é Olá igual ou mais recente do que o ficheiro de destino Olá, adicionar Olá `/XN` opção:</span><span class="sxs-lookup"><span data-stu-id="8d81e-141">For example, if you want tooexclude blobs whose last modified time is hello same or newer than hello destination file, add hello `/XN` option:</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /MT /XN
```

<span data-ttu-id="8d81e-142">Ou se pretender que os blobs tooexclude cuja hora da última modificação é Olá igual ou mais antiga do que o ficheiro de destino Olá, adicione Olá `/XO` opção:</span><span class="sxs-lookup"><span data-stu-id="8d81e-142">Or if you want tooexclude blobs whose last modified time is hello same or older than hello destination file, add hello `/XO` option:</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /MT /XO
```

## <a name="blob-upload"></a><span data-ttu-id="8d81e-143">Blob: carregar</span><span class="sxs-lookup"><span data-stu-id="8d81e-143">Blob: Upload</span></span>
### <a name="upload-single-file"></a><span data-ttu-id="8d81e-144">Carregar ficheiro único</span><span class="sxs-lookup"><span data-stu-id="8d81e-144">Upload single file</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /Pattern:"abc.txt"
```

<span data-ttu-id="8d81e-145">Se Olá o contentor de destino especificado não existe, o AzCopy irá criá-lo e carregar o ficheiro de Olá para a mesma.</span><span class="sxs-lookup"><span data-stu-id="8d81e-145">If hello specified destination container does not exist, AzCopy will create it and upload hello file into it.</span></span>

### <a name="upload-single-file-toovirtual-directory"></a><span data-ttu-id="8d81e-146">Carregar ficheiro único diretório toovirtual</span><span class="sxs-lookup"><span data-stu-id="8d81e-146">Upload single file toovirtual directory</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer/vd /DestKey:key /Pattern:abc.txt
```

<span data-ttu-id="8d81e-147">Se Olá especificado diretório virtual não existe, o AzCopy carregará Olá tooinclude Olá virtual diretório do ficheiro no respetivo nome (*por exemplo,*, `vd/abc.txt` no exemplo Olá acima).</span><span class="sxs-lookup"><span data-stu-id="8d81e-147">If hello specified virtual directory does not exist, AzCopy will upload hello file tooinclude hello virtual directory in its name (*e.g.*, `vd/abc.txt` in hello example above).</span></span>

### <a name="upload-all-files"></a><span data-ttu-id="8d81e-148">Carregar todos os ficheiros</span><span class="sxs-lookup"><span data-stu-id="8d81e-148">Upload all files</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /S
```

<span data-ttu-id="8d81e-149">Especificar a opção `/S` carregamentos Olá conteúdo Olá especificado diretório tooBlob armazenamento recursiva, o que significa que todas as subpastas e os ficheiros e serão carregados bem.</span><span class="sxs-lookup"><span data-stu-id="8d81e-149">Specifying option `/S` uploads hello contents of hello specified directory tooBlob storage recursively, meaning that all subfolders and their files will be uploaded as well.</span></span> <span data-ttu-id="8d81e-150">Por exemplo, suponha o seguinte Olá residem os ficheiros na pasta `C:\myfolder`:</span><span class="sxs-lookup"><span data-stu-id="8d81e-150">For instance, assume hello following files reside in folder `C:\myfolder`:</span></span>

    C:\myfolder\abc.txt
    C:\myfolder\abc1.txt
    C:\myfolder\abc2.txt
    C:\myfolder\subfolder\a.txt
    C:\myfolder\subfolder\abcd.txt

<span data-ttu-id="8d81e-151">Após a operação de carregamento de Olá, contentor Olá irá incluir Olá os seguintes ficheiros:</span><span class="sxs-lookup"><span data-stu-id="8d81e-151">After hello upload operation, hello container will include hello following files:</span></span>

    abc.txt
    abc1.txt
    abc2.txt
    subfolder\a.txt
    subfolder\abcd.txt

<span data-ttu-id="8d81e-152">Se não especificar opção `/S`, AzCopy não irá carregar em modo recursivo.</span><span class="sxs-lookup"><span data-stu-id="8d81e-152">If you do not specify option `/S`, AzCopy will not upload recursively.</span></span> <span data-ttu-id="8d81e-153">Após a operação de carregamento de Olá, contentor Olá irá incluir Olá os seguintes ficheiros:</span><span class="sxs-lookup"><span data-stu-id="8d81e-153">After hello upload operation, hello container will include hello following files:</span></span>

    abc.txt
    abc1.txt
    abc2.txt

### <a name="upload-files-matching-specified-pattern"></a><span data-ttu-id="8d81e-154">Carregar ficheiros correspondentes ao padrão especificado</span><span class="sxs-lookup"><span data-stu-id="8d81e-154">Upload files matching specified pattern</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /Pattern:a* /S
```

<span data-ttu-id="8d81e-155">Partem do princípio de seguinte Olá residem os ficheiros na pasta `C:\myfolder`:</span><span class="sxs-lookup"><span data-stu-id="8d81e-155">Assume hello following files reside in folder `C:\myfolder`:</span></span>

    C:\myfolder\abc.txt
    C:\myfolder\abc1.txt
    C:\myfolder\abc2.txt
    C:\myfolder\xyz.txt
    C:\myfolder\subfolder\a.txt
    C:\myfolder\subfolder\abcd.txt

<span data-ttu-id="8d81e-156">Após a operação de carregamento de Olá, contentor Olá irá incluir Olá os seguintes ficheiros:</span><span class="sxs-lookup"><span data-stu-id="8d81e-156">After hello upload operation, hello container will include hello following files:</span></span>

    abc.txt
    abc1.txt
    abc2.txt
    subfolder\a.txt
    subfolder\abcd.txt

<span data-ttu-id="8d81e-157">Se não especificar opção `/S`, AzCopy só irá carregar blobs que não residem num diretório virtual:</span><span class="sxs-lookup"><span data-stu-id="8d81e-157">If you do not specify option `/S`, AzCopy will only upload blobs that don't reside in a virtual directory:</span></span>

    C:\myfolder\abc.txt
    C:\myfolder\abc1.txt
    C:\myfolder\abc2.txt

### <a name="specify-hello-mime-content-type-of-a-destination-blob"></a><span data-ttu-id="8d81e-158">Especifique o tipo de conteúdo de MIME de Olá de um blob de destino</span><span class="sxs-lookup"><span data-stu-id="8d81e-158">Specify hello MIME content type of a destination blob</span></span>
<span data-ttu-id="8d81e-159">Por predefinição, AzCopy define o tipo de conteúdo de Olá de um blob de destino demasiado`application/octet-stream`.</span><span class="sxs-lookup"><span data-stu-id="8d81e-159">By default, AzCopy sets hello content type of a destination blob too`application/octet-stream`.</span></span> <span data-ttu-id="8d81e-160">A partir da versão 3.1.0, pode explicitamente especificar tipo de conteúdo de Olá através da opção de Olá `/SetContentType:[content-type]`.</span><span class="sxs-lookup"><span data-stu-id="8d81e-160">Beginning with version 3.1.0, you can explicitly specify hello content type via hello option `/SetContentType:[content-type]`.</span></span> <span data-ttu-id="8d81e-161">Esta sintaxe define o tipo de conteúdo de Olá para todos os blobs numa operação de carregamento.</span><span class="sxs-lookup"><span data-stu-id="8d81e-161">This syntax sets hello content type for all blobs in an upload operation.</span></span>

```azcopy
AzCopy /Source:C:\myfolder\ /Dest:https://myaccount.blob.core.windows.net/myContainer/ /DestKey:key /Pattern:ab /SetContentType:video/mp4
```

<span data-ttu-id="8d81e-162">Se especificar `/SetContentType` sem um valor, em seguida, AzCopy definirá cada blob ou tipo de conteúdo do ficheiro de acordo com tooits extensão de ficheiro.</span><span class="sxs-lookup"><span data-stu-id="8d81e-162">If you specify `/SetContentType` without a value, then AzCopy will set each blob or file's content type according tooits file extension.</span></span>

```azcopy
AzCopy /Source:C:\myfolder\ /Dest:https://myaccount.blob.core.windows.net/myContainer/ /DestKey:key /Pattern:ab /SetContentType
```

## <a name="blob-copy"></a><span data-ttu-id="8d81e-163">Blob: cópia</span><span class="sxs-lookup"><span data-stu-id="8d81e-163">Blob: Copy</span></span>
### <a name="copy-single-blob-within-storage-account"></a><span data-ttu-id="8d81e-164">Copiar blob único na conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="8d81e-164">Copy single blob within Storage account</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer1 /Dest:https://myaccount.blob.core.windows.net/mycontainer2 /SourceKey:key /DestKey:key /Pattern:abc.txt
```

<span data-ttu-id="8d81e-165">Quando copiar um blob dentro de uma conta de armazenamento, um [cópia do lado do servidor](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) é efetuar a operação.</span><span class="sxs-lookup"><span data-stu-id="8d81e-165">When you copy a blob within a Storage account, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="copy-single-blob-across-storage-accounts"></a><span data-ttu-id="8d81e-166">Copiar blob único em contas de armazenamento</span><span class="sxs-lookup"><span data-stu-id="8d81e-166">Copy single blob across Storage accounts</span></span>

```azcopy
AzCopy /Source:https://sourceaccount.blob.core.windows.net/mycontainer1 /Dest:https://destaccount.blob.core.windows.net/mycontainer2 /SourceKey:key1 /DestKey:key2 /Pattern:abc.txt
```

<span data-ttu-id="8d81e-167">Quando copiar um blob em contas de armazenamento, um [cópia do lado do servidor](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) é efetuar a operação.</span><span class="sxs-lookup"><span data-stu-id="8d81e-167">When you copy a blob across Storage accounts, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="copy-single-blob-from-secondary-region-tooprimary-region"></a><span data-ttu-id="8d81e-168">Copiar blob único da região de tooprimary região secundária</span><span class="sxs-lookup"><span data-stu-id="8d81e-168">Copy single blob from secondary region tooprimary region</span></span>

```azcopy
AzCopy /Source:https://myaccount1-secondary.blob.core.windows.net/mynewcontainer1 /Dest:https://myaccount2.blob.core.windows.net/mynewcontainer2 /SourceKey:key1 /DestKey:key2 /Pattern:abc.txt
```

<span data-ttu-id="8d81e-169">Tenha em atenção que tem de ter o armazenamento georredundante com acesso de leitura ativado.</span><span class="sxs-lookup"><span data-stu-id="8d81e-169">Note that you must have read-access geo-redundant storage enabled.</span></span>

### <a name="copy-single-blob-and-its-snapshots-across-storage-accounts"></a><span data-ttu-id="8d81e-170">Copiar blob único e o respetivos instantâneos em contas de armazenamento</span><span class="sxs-lookup"><span data-stu-id="8d81e-170">Copy single blob and its snapshots across Storage accounts</span></span>

```azcopy
    AzCopy /Source:https://sourceaccount.blob.core.windows.net/mycontainer1 /Dest:https://destaccount.blob.core.windows.net/mycontainer2 /SourceKey:key1 /DestKey:key2 /Pattern:abc.txt /Snapshot
```

<span data-ttu-id="8d81e-171">Após a operação de cópia de Olá, um contentor de destino Olá incluirá blob Olá e respetivos instantâneos.</span><span class="sxs-lookup"><span data-stu-id="8d81e-171">After hello copy operation, hello target container will include hello blob and its snapshots.</span></span> <span data-ttu-id="8d81e-172">Partindo do princípio de blob Olá no exemplo Olá acima tem dois instantâneos, contentor Olá incluirá seguinte Olá e instantâneos do blob:</span><span class="sxs-lookup"><span data-stu-id="8d81e-172">Assuming hello blob in hello example above has two snapshots, hello container will include hello following blob and snapshots:</span></span>

    abc.txt
    abc (2013-02-25 080757).txt
    abc (2014-02-21 150331).txt

### <a name="synchronously-copy-blobs-across-storage-accounts"></a><span data-ttu-id="8d81e-173">Em sincronia copiar os blobs em contas de armazenamento</span><span class="sxs-lookup"><span data-stu-id="8d81e-173">Synchronously copy blobs across Storage accounts</span></span>
<span data-ttu-id="8d81e-174">AzCopy por predefinição copia dados entre dois pontos finais de armazenamento de forma assíncrona.</span><span class="sxs-lookup"><span data-stu-id="8d81e-174">AzCopy by default copies data between two storage endpoints asynchronously.</span></span> <span data-ttu-id="8d81e-175">Por conseguinte, a operação de cópia de Olá será executado em segundo plano Olá utilizando a capacidade de reserva de largura de banda que não tenha nenhum SLA em termos de forma rápida um blob será copiado e AzCopy irá verificar periodicamente o estado da cópia Olá até Olá copiar está concluída ou falhada.</span><span class="sxs-lookup"><span data-stu-id="8d81e-175">Therefore, hello copy operation will run in hello background using spare bandwidth capacity that has no SLA in terms of how fast a blob will be copied, and AzCopy will periodically check hello copy status until hello copying is completed or failed.</span></span>

<span data-ttu-id="8d81e-176">Olá `/SyncCopy` opção garante que a operação de cópia de Olá obterá velocidade consistente.</span><span class="sxs-lookup"><span data-stu-id="8d81e-176">hello `/SyncCopy` option ensures that hello copy operation will get consistent speed.</span></span> <span data-ttu-id="8d81e-177">AzCopy efetua a cópia síncrona Olá transferindo blobs Olá toocopy de Olá especificada de memória de toolocal de origem e, em seguida, carregá-los toohello destino de armazenamento de Blobs.</span><span class="sxs-lookup"><span data-stu-id="8d81e-177">AzCopy performs hello synchronous copy by downloading hello blobs toocopy from hello specified source toolocal memory, and then uploading them toohello Blob storage destination.</span></span>

```azcopy
AzCopy /Source:https://myaccount1.blob.core.windows.net/myContainer/ /Dest:https://myaccount2.blob.core.windows.net/myContainer/ /SourceKey:key1 /DestKey:key2 /Pattern:ab /SyncCopy
```

<span data-ttu-id="8d81e-178">`/SyncCopy`pode gerar saída adicional de custos comparadas tooasynchronous cópia, hello abordagem recomendada é toouse esta opção na VM do Azure que está a ser Olá mesma região que o custo de saída tooavoid de conta de armazenamento de origem.</span><span class="sxs-lookup"><span data-stu-id="8d81e-178">`/SyncCopy` might generate additional egress cost compared tooasynchronous copy, hello recommended approach is toouse this option in an Azure VM that is in hello same region as your source storage account tooavoid egress cost.</span></span>

## <a name="file-download"></a><span data-ttu-id="8d81e-179">Ficheiro: Transferir</span><span class="sxs-lookup"><span data-stu-id="8d81e-179">File: Download</span></span>
### <a name="download-single-file"></a><span data-ttu-id="8d81e-180">Transferência de ficheiro único</span><span class="sxs-lookup"><span data-stu-id="8d81e-180">Download single file</span></span>

```azcopy
AzCopy /Source:https://myaccount.file.core.windows.net/myfileshare/myfolder1/ /Dest:C:\myfolder /SourceKey:key /Pattern:abc.txt
```

<span data-ttu-id="8d81e-181">Se Olá especificado origem é uma partilha de ficheiros do Azure, tem de especificar se o nome de ficheiro exato de Olá, (*por exemplo,* `abc.txt`) toodownload um ficheiro único, ou especificar a opção `/S` toodownload todos os ficheiros numa partilha de Olá em modo recursivo.</span><span class="sxs-lookup"><span data-stu-id="8d81e-181">If hello specified source is an Azure file share, then you must either specify hello exact file name, (*e.g.* `abc.txt`) toodownload a single file, or specify option `/S` toodownload all files in hello share recursively.</span></span> <span data-ttu-id="8d81e-182">Tentativa de toospecify um padrão de ficheiro e a opção `/S` em conjunto resultará num erro.</span><span class="sxs-lookup"><span data-stu-id="8d81e-182">Attempting toospecify both a file pattern and option `/S` together will result in an error.</span></span>

### <a name="download-all-files"></a><span data-ttu-id="8d81e-183">Transferir todos os ficheiros</span><span class="sxs-lookup"><span data-stu-id="8d81e-183">Download all files</span></span>

```azcopy
AzCopy /Source:https://myaccount.file.core.windows.net/myfileshare/ /Dest:C:\myfolder /SourceKey:key /S
```

<span data-ttu-id="8d81e-184">Tenha em atenção que não serão transferidas quaisquer pastas vazias.</span><span class="sxs-lookup"><span data-stu-id="8d81e-184">Note that any empty folders will not be downloaded.</span></span>

## <a name="file-upload"></a><span data-ttu-id="8d81e-185">Ficheiro: carregar</span><span class="sxs-lookup"><span data-stu-id="8d81e-185">File: Upload</span></span>
### <a name="upload-single-file"></a><span data-ttu-id="8d81e-186">Carregar ficheiro único</span><span class="sxs-lookup"><span data-stu-id="8d81e-186">Upload single file</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.file.core.windows.net/myfileshare/ /DestKey:key /Pattern:abc.txt
```

### <a name="upload-all-files"></a><span data-ttu-id="8d81e-187">Carregar todos os ficheiros</span><span class="sxs-lookup"><span data-stu-id="8d81e-187">Upload all files</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.file.core.windows.net/myfileshare/ /DestKey:key /S
```

<span data-ttu-id="8d81e-188">Tenha em atenção que não serão carregadas qualquer pastas vazias.</span><span class="sxs-lookup"><span data-stu-id="8d81e-188">Note that any empty folders will not be uploaded.</span></span>

### <a name="upload-files-matching-specified-pattern"></a><span data-ttu-id="8d81e-189">Carregar ficheiros correspondentes ao padrão especificado</span><span class="sxs-lookup"><span data-stu-id="8d81e-189">Upload files matching specified pattern</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.file.core.windows.net/myfileshare/ /DestKey:key /Pattern:ab* /S
```

## <a name="file-copy"></a><span data-ttu-id="8d81e-190">Ficheiro: cópia</span><span class="sxs-lookup"><span data-stu-id="8d81e-190">File: Copy</span></span>
### <a name="copy-across-file-shares"></a><span data-ttu-id="8d81e-191">Copiar em partilhas de ficheiros</span><span class="sxs-lookup"><span data-stu-id="8d81e-191">Copy across file shares</span></span>

```azcopy
AzCopy /Source:https://myaccount1.file.core.windows.net/myfileshare1/ /Dest:https://myaccount2.file.core.windows.net/myfileshare2/ /SourceKey:key1 /DestKey:key2 /S
```
<span data-ttu-id="8d81e-192">Quando copiar um ficheiro através de partilhas de ficheiros, um [cópia do lado do servidor](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) é efetuar a operação.</span><span class="sxs-lookup"><span data-stu-id="8d81e-192">When you copy a file across file shares, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="copy-from-file-share-tooblob"></a><span data-ttu-id="8d81e-193">Copiar do tooblob de partilha de ficheiros</span><span class="sxs-lookup"><span data-stu-id="8d81e-193">Copy from file share tooblob</span></span>

```azcopy
AzCopy /Source:https://myaccount1.file.core.windows.net/myfileshare/ /Dest:https://myaccount2.blob.core.windows.net/mycontainer/ /SourceKey:key1 /DestKey:key2 /S
```
<span data-ttu-id="8d81e-194">Quando copiar um ficheiro de tooblob de partilha de ficheiros, um [cópia do lado do servidor](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) é efetuar a operação.</span><span class="sxs-lookup"><span data-stu-id="8d81e-194">When you copy a file from file share tooblob, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>


### <a name="copy-from-blob-toofile-share"></a><span data-ttu-id="8d81e-195">Copiar de blob toofile partilha</span><span class="sxs-lookup"><span data-stu-id="8d81e-195">Copy from blob toofile share</span></span>

```azcopy
AzCopy /Source:https://myaccount1.blob.core.windows.net/mycontainer/ /Dest:https://myaccount2.file.core.windows.net/myfileshare/ /SourceKey:key1 /DestKey:key2 /S
```
<span data-ttu-id="8d81e-196">Quando copiar um ficheiro de partilha de toofile de blob, um [cópia do lado do servidor](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) é efetuar a operação.</span><span class="sxs-lookup"><span data-stu-id="8d81e-196">When you copy a file from blob toofile share, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="synchronously-copy-files"></a><span data-ttu-id="8d81e-197">Em sincronia copiar ficheiros</span><span class="sxs-lookup"><span data-stu-id="8d81e-197">Synchronously copy files</span></span>
<span data-ttu-id="8d81e-198">Pode especificar Olá `/SyncCopy` opção toocopy dados de armazenamento de ficheiros tooFile armazenamento, de armazenamento de ficheiros tooBlob armazenamento e de armazenamento de BLOBs tooFile armazenamento de forma síncrona, AzCopy efetua este procedimento, transferindo Olá origem dados toolocal de memória e carregá-la toodestination novamente.</span><span class="sxs-lookup"><span data-stu-id="8d81e-198">You can specify hello `/SyncCopy` option toocopy data from File Storage tooFile Storage, from File Storage tooBlob Storage and from Blob Storage tooFile Storage synchronously, AzCopy does this by downloading hello source data toolocal memory and upload it again toodestination.</span></span> <span data-ttu-id="8d81e-199">Custo de saída padrão será aplicada.</span><span class="sxs-lookup"><span data-stu-id="8d81e-199">Standard egress cost will apply.</span></span>

```azcopy
AzCopy /Source:https://myaccount1.file.core.windows.net/myfileshare1/ /Dest:https://myaccount2.file.core.windows.net/myfileshare2/ /SourceKey:key1 /DestKey:key2 /S /SyncCopy
```

<span data-ttu-id="8d81e-200">Quando copiar do File Storage tooBlob armazenamento, é de tipo de blob predefinido Olá BLOBs de blocos, o utilizador pode especificar a opção `/BlobType:page` toochange Olá tipo de blob de destino.</span><span class="sxs-lookup"><span data-stu-id="8d81e-200">When copying from File Storage tooBlob Storage, hello default blob type is block blob, user can specify option `/BlobType:page` toochange hello destination blob type.</span></span>

<span data-ttu-id="8d81e-201">Tenha em atenção que `/SyncCopy` poderá gerar a saída adicional custo compara tooasynchronous cópia, hello abordagem recomendada é toouse VM do Azure que está a ser Olá Olá, esta opção na mesma região que o custo de saída tooavoid de conta de armazenamento de origem.</span><span class="sxs-lookup"><span data-stu-id="8d81e-201">Note that `/SyncCopy` might generate additional egress cost comparing tooasynchronous copy, hello recommended approach is toouse this option in hello Azure VM which is in hello same region as your source storage account tooavoid egress cost.</span></span>

## <a name="table-export"></a><span data-ttu-id="8d81e-202">Tabela: Exportar</span><span class="sxs-lookup"><span data-stu-id="8d81e-202">Table: Export</span></span>
### <a name="export-table"></a><span data-ttu-id="8d81e-203">Tabela de exportação</span><span class="sxs-lookup"><span data-stu-id="8d81e-203">Export table</span></span>

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/myTable/ /Dest:C:\myfolder\ /SourceKey:key
```

<span data-ttu-id="8d81e-204">AzCopy escreve uma pasta de destino especificada do ficheiro de manifesto toohello.</span><span class="sxs-lookup"><span data-stu-id="8d81e-204">AzCopy writes a manifest file toohello specified destination folder.</span></span> <span data-ttu-id="8d81e-205">o ficheiro de manifesto Olá é utilizada nos ficheiros de dados necessários do Olá importação processo toolocate Olá e efetuar a validação de dados.</span><span class="sxs-lookup"><span data-stu-id="8d81e-205">hello manifest file is used in hello import process toolocate hello necessary data files and perform data validation.</span></span> <span data-ttu-id="8d81e-206">o ficheiro de manifesto Olá utiliza Olá seguinte convenção de nomenclatura por predefinição:</span><span class="sxs-lookup"><span data-stu-id="8d81e-206">hello manifest file uses hello following naming convention by default:</span></span>

    <account name>_<table name>_<timestamp>.manifest

<span data-ttu-id="8d81e-207">Utilizador também é possível especificar a opção de Olá `/Manifest:<manifest file name>` nome de ficheiro de manifesto tooset Olá.</span><span class="sxs-lookup"><span data-stu-id="8d81e-207">User can also specify hello option `/Manifest:<manifest file name>` tooset hello manifest file name.</span></span>

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/myTable/ /Dest:C:\myfolder\ /SourceKey:key /Manifest:abc.manifest
```

### <a name="split-export-into-multiple-files"></a><span data-ttu-id="8d81e-208">Exportação de divisão em vários ficheiros</span><span class="sxs-lookup"><span data-stu-id="8d81e-208">Split export into multiple files</span></span>

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/mytable/ /Dest:C:\myfolder /SourceKey:key /S /SplitSize:100
```

<span data-ttu-id="8d81e-209">AzCopy utiliza um *índice volume* no Olá dividir dados nomes do ficheiro toodistinguish vários ficheiros.</span><span class="sxs-lookup"><span data-stu-id="8d81e-209">AzCopy uses a *volume index* in hello split data file names toodistinguish multiple files.</span></span> <span data-ttu-id="8d81e-210">índice de volume Olá consiste em duas partes: um *índice de intervalos de chave de partição* e um *divisão ficheiro índice*.</span><span class="sxs-lookup"><span data-stu-id="8d81e-210">hello volume index consists of two parts, a *partition key range index* and a *split file index*.</span></span> <span data-ttu-id="8d81e-211">Ambos os índices são baseado em zero.</span><span class="sxs-lookup"><span data-stu-id="8d81e-211">Both indexes are zero-based.</span></span>

<span data-ttu-id="8d81e-212">índice de intervalos de chave de partição de Olá será 0 se o utilizador especificar a opção `/PKRS`.</span><span class="sxs-lookup"><span data-stu-id="8d81e-212">hello partition key range index will be 0 if user does not specify option `/PKRS`.</span></span>

<span data-ttu-id="8d81e-213">Por exemplo, suponha que AzCopy gera dois ficheiros de dados depois do utilizador de Olá Especifica opção `/SplitSize`.</span><span class="sxs-lookup"><span data-stu-id="8d81e-213">For instance, suppose AzCopy generates two data files after hello user specifies option `/SplitSize`.</span></span> <span data-ttu-id="8d81e-214">poderá ser Olá resultante nomes de ficheiro de dados:</span><span class="sxs-lookup"><span data-stu-id="8d81e-214">hello resulting data file names might be:</span></span>

    myaccount_mytable_20140903T051850.8128447Z_0_0_C3040FE8.json
    myaccount_mytable_20140903T051850.8128447Z_0_1_0AB9AC20.json

<span data-ttu-id="8d81e-215">Tenha em atenção que Olá valor mínimo possível para a opção `/SplitSize` é 32 MB.</span><span class="sxs-lookup"><span data-stu-id="8d81e-215">Note that hello minimum possible value for option `/SplitSize` is 32MB.</span></span> <span data-ttu-id="8d81e-216">Se Olá especificado destino for o Blob storage, o AzCopy irá dividir o ficheiro de dados de Olá uma vez a limitação de tamanho de blob na Olá de atingir tamanhos (200GB), independentemente da opção se `/SplitSize` foi especificado pelo utilizador Olá.</span><span class="sxs-lookup"><span data-stu-id="8d81e-216">If hello specified destination is Blob storage, AzCopy will split hello data file once its sizes reaches hello blob size limitation (200GB), regardless of whether option `/SplitSize` has been specified by hello user.</span></span>

### <a name="export-table-toojson-or-csv-data-file-format"></a><span data-ttu-id="8d81e-217">Exportar tooJSON de tabela ou o formato de ficheiro de dados CSV</span><span class="sxs-lookup"><span data-stu-id="8d81e-217">Export table tooJSON or CSV data file format</span></span>
<span data-ttu-id="8d81e-218">AzCopy por predefinição exporta os ficheiros de dados de tooJSON tabelas.</span><span class="sxs-lookup"><span data-stu-id="8d81e-218">AzCopy by default exports tables tooJSON data files.</span></span> <span data-ttu-id="8d81e-219">Pode especificar a opção de Olá `/PayloadFormat:JSON|CSV` tabelas de Olá tooexport como JSON ou CSV.</span><span class="sxs-lookup"><span data-stu-id="8d81e-219">You can specify hello option `/PayloadFormat:JSON|CSV` tooexport hello tables as JSON or CSV.</span></span>

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/myTable/ /Dest:C:\myfolder\ /SourceKey:key /PayloadFormat:CSV
```

<span data-ttu-id="8d81e-220">Durante a especificação de formato de payload Olá CSV, o AzCopy também irá gerar um ficheiro de esquema com a extensão de ficheiro `.schema.csv` para cada ficheiro de dados.</span><span class="sxs-lookup"><span data-stu-id="8d81e-220">When specifying hello CSV payload format, AzCopy will also generate a schema file with file extension `.schema.csv` for each data file.</span></span>

### <a name="export-table-entities-concurrently"></a><span data-ttu-id="8d81e-221">Exportar as entidades da tabela em simultâneo</span><span class="sxs-lookup"><span data-stu-id="8d81e-221">Export table entities concurrently</span></span>

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/myTable/ /Dest:C:\myfolder\ /SourceKey:key /PKRS:"aa#bb"
```

<span data-ttu-id="8d81e-222">AzCopy iniciará entidades de tooexport operações simultâneas, quando o utilizador de Olá Especifica opção `/PKRS`.</span><span class="sxs-lookup"><span data-stu-id="8d81e-222">AzCopy will start concurrent operations tooexport entities when hello user specifies option `/PKRS`.</span></span> <span data-ttu-id="8d81e-223">Cada operação exporta um intervalo de chave de partição.</span><span class="sxs-lookup"><span data-stu-id="8d81e-223">Each operation exports one partition key range.</span></span>

<span data-ttu-id="8d81e-224">Tenha em atenção que o número de Olá de operações simultâneas também é controlado pela opção `/NC`.</span><span class="sxs-lookup"><span data-stu-id="8d81e-224">Note that hello number of concurrent operations is also controlled by option `/NC`.</span></span> <span data-ttu-id="8d81e-225">AzCopy utiliza o número de Olá de processadores de núcleo como valor predefinido Olá `/NC` quando copiar as entidades da tabela, mesmo se `/NC` não foi especificado.</span><span class="sxs-lookup"><span data-stu-id="8d81e-225">AzCopy uses hello number of core processors as hello default value of `/NC` when copying table entities, even if `/NC` was not specified.</span></span> <span data-ttu-id="8d81e-226">Quando o utilizador Olá Especifica opção `/PKRS`, AzCopy utiliza Olá mais pequenos de Olá dois valores - partição intervalos de chaves versus operações simultâneas implícita ou explicitamente especificados - toodetermine Olá número toostart operações simultâneas.</span><span class="sxs-lookup"><span data-stu-id="8d81e-226">When hello user specifies option `/PKRS`, AzCopy uses hello smaller of hello two values - partition key ranges versus implicitly or explicitly specified concurrent operations - toodetermine hello number of concurrent operations toostart.</span></span> <span data-ttu-id="8d81e-227">Para obter mais detalhes, escreva `AzCopy /?:NC` na linha de comandos Olá.</span><span class="sxs-lookup"><span data-stu-id="8d81e-227">For more details, type `AzCopy /?:NC` at hello command line.</span></span>

### <a name="export-table-tooblob"></a><span data-ttu-id="8d81e-228">Exportar a tabela tooblob</span><span class="sxs-lookup"><span data-stu-id="8d81e-228">Export table tooblob</span></span>

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/myTable/ /Dest:https://myaccount.blob.core.windows.net/mycontainer/ /SourceKey:key1 /Destkey:key2
```

<span data-ttu-id="8d81e-229">AzCopy irá gerar um ficheiro de dados JSON no contentor de BLOBs de Olá com a seguinte convenção de nomenclatura:</span><span class="sxs-lookup"><span data-stu-id="8d81e-229">AzCopy will generate a JSON data file into hello blob container with following naming convention:</span></span>

    <account name>_<table name>_<timestamp>_<volume index>_<CRC>.json

<span data-ttu-id="8d81e-230">ficheiro de dados JSON Olá gerado segue o formato de payload Olá para metadados mínimo.</span><span class="sxs-lookup"><span data-stu-id="8d81e-230">hello generated JSON data file follows hello payload format for minimal metadata.</span></span> <span data-ttu-id="8d81e-231">Para obter detalhes sobre este formato de payload, consulte [formato de Payload para operações de serviço tabela](http://msdn.microsoft.com/library/azure/dn535600.aspx).</span><span class="sxs-lookup"><span data-stu-id="8d81e-231">For details on this payload format, see [Payload Format for Table Service Operations](http://msdn.microsoft.com/library/azure/dn535600.aspx).</span></span>

<span data-ttu-id="8d81e-232">Tenha em atenção que ao exportar tooblobs de tabelas, AzCopy irá transferir Olá tabela entidades toolocal temporário os ficheiros de dados e, em seguida, carregue os BLOBs de toohello entidades.</span><span class="sxs-lookup"><span data-stu-id="8d81e-232">Note that when exporting tables tooblobs, AzCopy will download hello Table entities toolocal temporary data files and then upload those entities toohello blob.</span></span> <span data-ttu-id="8d81e-233">Estes ficheiros de dados temporária são colocados de pasta do ficheiro de Olá diário de alterações com o caminho predefinido de Olá "<code>%LocalAppData%\Microsoft\Azure\AzCopy</code>", pode especificar a opção/z [pasta de ficheiros de diário] toochange Olá localização de pasta de ficheiros do diário de alterações e, por conseguinte, altere a localização de ficheiros de dados temporária de Olá.</span><span class="sxs-lookup"><span data-stu-id="8d81e-233">These temporary data files are put into hello journal file folder with hello default path "<code>%LocalAppData%\Microsoft\Azure\AzCopy</code>", you can specify option /Z:[journal-file-folder] toochange hello journal file folder location and thus change hello temporary data files location.</span></span> <span data-ttu-id="8d81e-234">Olá dados temporários tamanho dos ficheiros é decidido ao tamanho e tamanho de Olá que especificou com Olá opção /SplitSize, as entidades da tabela, apesar do ficheiro de dados temporária de Olá no disco local será eliminado de forma instantânea depois de ter sido carregado toohello blob, certifique-se antes de ter suficiente toostore de espaço em disco local estes ficheiros de dados temporária estes sejam eliminados.</span><span class="sxs-lookup"><span data-stu-id="8d81e-234">hello temporary data files' size is decided by your table entities' size and hello size you specified with hello option /SplitSize, although hello temporary data file in local disk will be deleted instantly once it has been uploaded toohello blob, please make sure you have enough local disk space toostore these temporary data files before they are deleted.</span></span>

## <a name="table-import"></a><span data-ttu-id="8d81e-235">Tabela: importação</span><span class="sxs-lookup"><span data-stu-id="8d81e-235">Table: Import</span></span>
### <a name="import-table"></a><span data-ttu-id="8d81e-236">Tabela importar</span><span class="sxs-lookup"><span data-stu-id="8d81e-236">Import table</span></span>

```azcopy
AzCopy /Source:C:\myfolder\ /Dest:https://myaccount.table.core.windows.net/mytable1/ /DestKey:key /Manifest:"myaccount_mytable_20140103T112020.manifest" /EntityOperation:InsertOrReplace
```

<span data-ttu-id="8d81e-237">Olá opção `/EntityOperation` indica como tooinsert entidades para Olá tabela.</span><span class="sxs-lookup"><span data-stu-id="8d81e-237">hello option `/EntityOperation` indicates how tooinsert entities into hello table.</span></span> <span data-ttu-id="8d81e-238">Os valores possíveis são:</span><span class="sxs-lookup"><span data-stu-id="8d81e-238">Possible values are:</span></span>

* <span data-ttu-id="8d81e-239">`InsertOrSkip`: Ignora a uma entidade existente ou introduza uma nova entidade se não existir na tabela de Olá.</span><span class="sxs-lookup"><span data-stu-id="8d81e-239">`InsertOrSkip`: Skips an existing entity or inserts a new entity if it does not exist in hello table.</span></span>
* <span data-ttu-id="8d81e-240">`InsertOrMerge`: Intercala uma entidade existente ou introduza uma nova entidade se não existir na tabela de Olá.</span><span class="sxs-lookup"><span data-stu-id="8d81e-240">`InsertOrMerge`: Merges an existing entity or inserts a new entity if it does not exist in hello table.</span></span>
* <span data-ttu-id="8d81e-241">`InsertOrReplace`: Substitui uma entidade existente ou introduza uma nova entidade se não existir na tabela de Olá.</span><span class="sxs-lookup"><span data-stu-id="8d81e-241">`InsertOrReplace`: Replaces an existing entity or inserts a new entity if it does not exist in hello table.</span></span>

<span data-ttu-id="8d81e-242">Tenha em atenção que não é possível especificar a opção `/PKRS` num cenário de importação de Olá.</span><span class="sxs-lookup"><span data-stu-id="8d81e-242">Note that you cannot specify option `/PKRS` in hello import scenario.</span></span> <span data-ttu-id="8d81e-243">Ao contrário do cenário de exportação de Olá, na qual tem de especificar a opção `/PKRS` toostart de operações simultâneas, AzCopy por predefinição iniciará operações simultâneas quando importar uma tabela.</span><span class="sxs-lookup"><span data-stu-id="8d81e-243">Unlike hello export scenario, in which you must specify option `/PKRS` toostart concurrent operations, AzCopy will by default start concurrent operations when you import a table.</span></span> <span data-ttu-id="8d81e-244">Olá predefinição o número de operações simultâneas iniciado é toohello igual número de processadores de núcleo No entanto, pode especificar um número diferente de em simultâneo com a opção `/NC`.</span><span class="sxs-lookup"><span data-stu-id="8d81e-244">hello default number of concurrent operations started is equal toohello number of core processors; however, you can specify a different number of concurrent with option `/NC`.</span></span> <span data-ttu-id="8d81e-245">Para obter mais detalhes, escreva `AzCopy /?:NC` na linha de comandos Olá.</span><span class="sxs-lookup"><span data-stu-id="8d81e-245">For more details, type `AzCopy /?:NC` at hello command line.</span></span>

<span data-ttu-id="8d81e-246">Tenha em atenção que AzCopy só suporta a importação para JSON, CSV não.</span><span class="sxs-lookup"><span data-stu-id="8d81e-246">Note that AzCopy only supports importing for JSON, not CSV.</span></span> <span data-ttu-id="8d81e-247">AzCopy não suporta importações de tabela JSON criados pelo utilizador e os ficheiros de manifesto.</span><span class="sxs-lookup"><span data-stu-id="8d81e-247">AzCopy does not support table imports from user-created JSON and manifest files.</span></span> <span data-ttu-id="8d81e-248">Ambos estes ficheiros têm de ser provenientes uma exportação de tabela do AzCopy.</span><span class="sxs-lookup"><span data-stu-id="8d81e-248">Both of these files must come from an AzCopy table export.</span></span> <span data-ttu-id="8d81e-249">erros de tooavoid, não modifique Olá exportado JSON ou o ficheiro de manifesto.</span><span class="sxs-lookup"><span data-stu-id="8d81e-249">tooavoid errors, please do not modify hello exported JSON or manifest file.</span></span>

### <a name="import-entities-tootable-using-blobs"></a><span data-ttu-id="8d81e-250">Entidades de importação tootable utilizar blobs</span><span class="sxs-lookup"><span data-stu-id="8d81e-250">Import entities tootable using blobs</span></span>
<span data-ttu-id="8d81e-251">Assuma um contentor do Blob contém seguinte Olá: ficheiro de um JSON que representam uma tabela do Azure e o respetivo ficheiro de manifesto associado.</span><span class="sxs-lookup"><span data-stu-id="8d81e-251">Assume a Blob container contains hello following: A JSON file representing an Azure Table and its accompanying manifest file.</span></span>

    myaccount_mytable_20140103T112020.manifest
    myaccount_mytable_20140103T112020_0_0_0AF395F1DC42E952.json

<span data-ttu-id="8d81e-252">Pode executar Olá seguintes entidades do comando tooimport para uma tabela com o ficheiro de manifesto Olá nesse contentor de blob:</span><span class="sxs-lookup"><span data-stu-id="8d81e-252">You can run hello following command tooimport entities into a table using hello manifest file in that blob container:</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:https://myaccount.table.core.windows.net/mytable /SourceKey:key1 /DestKey:key2 /Manifest:"myaccount_mytable_20140103T112020.manifest" /EntityOperation:"InsertOrReplace"
```

## <a name="other-azcopy-features"></a><span data-ttu-id="8d81e-253">Outras funcionalidades do AzCopy</span><span class="sxs-lookup"><span data-stu-id="8d81e-253">Other AzCopy features</span></span>
### <a name="only-copy-data-that-doesnt-exist-in-hello-destination"></a><span data-ttu-id="8d81e-254">Apenas os dados de cópia que não existem no destino Olá</span><span class="sxs-lookup"><span data-stu-id="8d81e-254">Only copy data that doesn't exist in hello destination</span></span>
<span data-ttu-id="8d81e-255">Olá `/XO` e `/XN` parâmetros permitem tooexclude recursos de origem de anterior ou mais recente de ser copiado, respetivamente.</span><span class="sxs-lookup"><span data-stu-id="8d81e-255">hello `/XO` and `/XN` parameters allow you tooexclude older or newer source resources from being copied, respectively.</span></span> <span data-ttu-id="8d81e-256">Se pretender apenas toocopy recursos de origem que não existem no destino Olá, pode especificar os dois parâmetros na Olá comandos do AzCopy:</span><span class="sxs-lookup"><span data-stu-id="8d81e-256">If you only want toocopy source resources that don't exist in hello destination, you can specify both parameters in hello AzCopy command:</span></span>

    /Source:http://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:<sourcekey> /S /XO /XN

    /Source:C:\myfolder /Dest:http://myaccount.file.core.windows.net/myfileshare /DestKey:<destkey> /S /XO /XN

    /Source:http://myaccount.blob.core.windows.net/mycontainer /Dest:http://myaccount.blob.core.windows.net/mycontainer1 /SourceKey:<sourcekey> /DestKey:<destkey> /S /XO /XN

<span data-ttu-id="8d81e-257">Tenha em atenção que isto não é suportado quando Olá origem ou de destino é uma tabela.</span><span class="sxs-lookup"><span data-stu-id="8d81e-257">Note that this is not supported when either hello source or destination is a table.</span></span>

### <a name="use-a-response-file-toospecify-command-line-parameters"></a><span data-ttu-id="8d81e-258">Utilize um toospecify de ficheiro de resposta para parâmetros de linha de comandos</span><span class="sxs-lookup"><span data-stu-id="8d81e-258">Use a response file toospecify command-line parameters</span></span>

```azcopy
AzCopy /@:"C:\responsefiles\copyoperation.txt"
```

<span data-ttu-id="8d81e-259">Pode incluir quaisquer parâmetros de linha de comandos do AzCopy num ficheiro de resposta.</span><span class="sxs-lookup"><span data-stu-id="8d81e-259">You can include any AzCopy command-line parameters in a response file.</span></span> <span data-ttu-id="8d81e-260">Processos do AzCopy Olá parâmetros no ficheiro de Olá como se tivesse sido especificados na linha de comandos Olá, efetuar uma substituição direta com conteúdo Olá do ficheiro de Olá.</span><span class="sxs-lookup"><span data-stu-id="8d81e-260">AzCopy processes hello parameters in hello file as if they had been specified on hello command line, performing a direct substitution with hello contents of hello file.</span></span>

<span data-ttu-id="8d81e-261">Partem do princípio de um ficheiro de resposta com o nome `copyoperation.txt`, que contém Olá seguintes linhas.</span><span class="sxs-lookup"><span data-stu-id="8d81e-261">Assume a response file named `copyoperation.txt`, that contains hello following lines.</span></span> <span data-ttu-id="8d81e-262">Cada parâmetro do AzCopy pode ser especificado numa única linha</span><span class="sxs-lookup"><span data-stu-id="8d81e-262">Each AzCopy parameter can be specified on a single line</span></span>

    /Source:http://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:<sourcekey> /S /Y

<span data-ttu-id="8d81e-263">ou, no separar linhas:</span><span class="sxs-lookup"><span data-stu-id="8d81e-263">or on separate lines:</span></span>

    /Source:http://myaccount.blob.core.windows.net/mycontainer
    /Dest:C:\myfolder
    /SourceKey:<sourcekey>
    /S
    /Y

<span data-ttu-id="8d81e-264">AzCopy irá falhar se dividir parâmetro Olá por duas linhas, conforme mostrado aqui para Olá `/sourcekey` parâmetro:</span><span class="sxs-lookup"><span data-stu-id="8d81e-264">AzCopy will fail if you split hello parameter across two lines, as shown here for hello `/sourcekey` parameter:</span></span>

    http://myaccount.blob.core.windows.net/mycontainer
     C:\myfolder
    /sourcekey:
    <sourcekey>
    /S
    /Y

### <a name="use-multiple-response-files-toospecify-command-line-parameters"></a><span data-ttu-id="8d81e-265">Utilizar vários ficheiros toospecify da linha de comandos parâmetros de resposta</span><span class="sxs-lookup"><span data-stu-id="8d81e-265">Use multiple response files toospecify command-line parameters</span></span>
<span data-ttu-id="8d81e-266">Partem do princípio de um ficheiro de resposta com o nome `source.txt` que especifica um contentor de origem:</span><span class="sxs-lookup"><span data-stu-id="8d81e-266">Assume a response file named `source.txt` that specifies a source container:</span></span>

    /Source:http://myaccount.blob.core.windows.net/mycontainer

<span data-ttu-id="8d81e-267">E um ficheiro de resposta com o nome `dest.txt` que especifica uma pasta de destino no sistema de ficheiros de Olá:</span><span class="sxs-lookup"><span data-stu-id="8d81e-267">And a response file named `dest.txt` that specifies a destination folder in hello file system:</span></span>

    /Dest:C:\myfolder

<span data-ttu-id="8d81e-268">E um ficheiro de resposta com o nome `options.txt` que especifica as opções para AzCopy:</span><span class="sxs-lookup"><span data-stu-id="8d81e-268">And a response file named `options.txt` that specifies options for AzCopy:</span></span>

    /S /Y

<span data-ttu-id="8d81e-269">toocall AzCopy com estes ficheiros de resposta, todos os que residem num diretório `C:\responsefiles`, utilize este comando:</span><span class="sxs-lookup"><span data-stu-id="8d81e-269">toocall AzCopy with these response files, all of which reside in a directory `C:\responsefiles`, use this command:</span></span>

```azcopy
AzCopy /@:"C:\responsefiles\source.txt" /@:"C:\responsefiles\dest.txt" /SourceKey:<sourcekey> /@:"C:\responsefiles\options.txt"   
```

<span data-ttu-id="8d81e-270">AzCopy processa este comando, tal como se de que incluiu todos os parâmetros de individuais Olá na linha de comandos Olá:</span><span class="sxs-lookup"><span data-stu-id="8d81e-270">AzCopy processes this command just as it would if you included all of hello individual parameters on hello command line:</span></span>

```azcopy
AzCopy /Source:http://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:<sourcekey> /S /Y
```

### <a name="specify-a-shared-access-signature-sas"></a><span data-ttu-id="8d81e-271">Especifique uma assinatura de acesso partilhado (SAS)</span><span class="sxs-lookup"><span data-stu-id="8d81e-271">Specify a shared access signature (SAS)</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer1 /Dest:https://myaccount.blob.core.windows.net/mycontainer2 /SourceSAS:SAS1 /DestSAS:SAS2 /Pattern:abc.txt
```

<span data-ttu-id="8d81e-272">Também pode especificar uma SAS no contentor de Olá URI:</span><span class="sxs-lookup"><span data-stu-id="8d81e-272">You can also specify a SAS on hello container URI:</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer1/?SourceSASToken /Dest:C:\myfolder /S
```

### <a name="journal-file-folder"></a><span data-ttu-id="8d81e-273">Pasta de ficheiros do diário de alterações</span><span class="sxs-lookup"><span data-stu-id="8d81e-273">Journal file folder</span></span>
<span data-ttu-id="8d81e-274">Sempre que emitir um comando tooAzCopy, este verifica se existe um ficheiro de diário de alterações na pasta predefinida de hello, ou se existe uma pasta que especificou através desta opção.</span><span class="sxs-lookup"><span data-stu-id="8d81e-274">Each time you issue a command tooAzCopy, it checks whether a journal file exists in hello default folder, or whether it exists in a folder that you specified via this option.</span></span> <span data-ttu-id="8d81e-275">Se não existir um ficheiro do diário de alterações de Olá em qualquer local, o AzCopy trata operação Olá como novo e gera um novo ficheiro de diário de alterações.</span><span class="sxs-lookup"><span data-stu-id="8d81e-275">If hello journal file does not exist in either place, AzCopy treats hello operation as new and generates a new journal file.</span></span>

<span data-ttu-id="8d81e-276">Se existirem ficheiros do diário de alterações de Olá, AzCopy irá verificar se linha de comandos de Olá introduzido corresponde a linha de comandos Olá no ficheiro de diário Olá.</span><span class="sxs-lookup"><span data-stu-id="8d81e-276">If hello journal file does exist, AzCopy will check whether hello command line that you input matches hello command line in hello journal file.</span></span> <span data-ttu-id="8d81e-277">Se duas linhas de comando Olá corresponderem, o AzCopy retoma operação incompleta Olá.</span><span class="sxs-lookup"><span data-stu-id="8d81e-277">If hello two command lines match, AzCopy resumes hello incomplete operation.</span></span> <span data-ttu-id="8d81e-278">Se não corresponderem, será pedido tooeither substituir Olá diário ficheiro toostart uma operação de novo ou toocancel Olá operação atual.</span><span class="sxs-lookup"><span data-stu-id="8d81e-278">If they do not match, you will be prompted tooeither overwrite hello journal file toostart a new operation, or toocancel hello current operation.</span></span>

<span data-ttu-id="8d81e-279">Se pretender que a localização predefinida de Olá de toouse para o ficheiro do diário de alterações de Olá:</span><span class="sxs-lookup"><span data-stu-id="8d81e-279">If you want toouse hello default location for hello journal file:</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /Z
```

<span data-ttu-id="8d81e-280">Se omitir opção `/Z`, ou especificar a opção `/Z` sem o caminho da pasta Olá, conforme mostrado acima, o AzCopy cria Olá diário ficheiro na localização predefinida de Olá, que é `%SystemDrive%\Users\%username%\AppData\Local\Microsoft\Azure\AzCopy`.</span><span class="sxs-lookup"><span data-stu-id="8d81e-280">If you omit option `/Z`, or specify option `/Z` without hello folder path, as shown above, AzCopy creates hello journal file in hello default location, which is `%SystemDrive%\Users\%username%\AppData\Local\Microsoft\Azure\AzCopy`.</span></span> <span data-ttu-id="8d81e-281">Se já existir um ficheiro do diário de alterações de Olá, o AzCopy retoma operação Olá com base num ficheiro do diário de alterações de Olá.</span><span class="sxs-lookup"><span data-stu-id="8d81e-281">If hello journal file already exists, then AzCopy resumes hello operation based on hello journal file.</span></span>

<span data-ttu-id="8d81e-282">Se quiser toospecify numa localização personalizada para o ficheiro do diário de alterações de Olá:</span><span class="sxs-lookup"><span data-stu-id="8d81e-282">If you want toospecify a custom location for hello journal file:</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /Z:C:\journalfolder\
```

<span data-ttu-id="8d81e-283">Este exemplo cria ficheiros do diário de alterações de Olá se já existir.</span><span class="sxs-lookup"><span data-stu-id="8d81e-283">This example creates hello journal file if it does not already exist.</span></span> <span data-ttu-id="8d81e-284">Se existir, o AzCopy retoma operação Olá com base num ficheiro do diário de alterações de Olá.</span><span class="sxs-lookup"><span data-stu-id="8d81e-284">If it does exist, then AzCopy resumes hello operation based on hello journal file.</span></span>

<span data-ttu-id="8d81e-285">Se quiser tooresume uma operação do AzCopy:</span><span class="sxs-lookup"><span data-stu-id="8d81e-285">If you want tooresume an AzCopy operation:</span></span>

```azcopy
AzCopy /Z:C:\journalfolder\
```

<span data-ttu-id="8d81e-286">Neste exemplo retoma Olá última operação, que pode não ter conseguido toocomplete.</span><span class="sxs-lookup"><span data-stu-id="8d81e-286">This example resumes hello last operation, which may have failed toocomplete.</span></span>

### <a name="generate-a-log-file"></a><span data-ttu-id="8d81e-287">Gerar um ficheiro de registo</span><span class="sxs-lookup"><span data-stu-id="8d81e-287">Generate a log file</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /V
```

<span data-ttu-id="8d81e-288">Se especificar a opção `/V` sem fornecer um registo verboso do caminho toohello de ficheiros, em seguida, AzCopy cria Olá ficheiro de registo na localização predefinida de Olá, que é `%SystemDrive%\Users\%username%\AppData\Local\Microsoft\Azure\AzCopy`.</span><span class="sxs-lookup"><span data-stu-id="8d81e-288">If you specify option `/V` without providing a file path toohello verbose log, then AzCopy creates hello log file in hello default location, which is `%SystemDrive%\Users\%username%\AppData\Local\Microsoft\Azure\AzCopy`.</span></span>

<span data-ttu-id="8d81e-289">Caso contrário, pode criar um ficheiro de registo numa localização personalizada:</span><span class="sxs-lookup"><span data-stu-id="8d81e-289">Otherwise, you can create an log file in a custom location:</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /V:C:\myfolder\azcopy1.log
```

<span data-ttu-id="8d81e-290">Tenha em atenção que se especificar um caminho relativo a seguinte opção `/V`, tais como `/V:test/azcopy1.log`, em seguida, o registo verboso Olá é criado na Olá atual diretório de trabalho dentro de uma subpasta denominada `test`.</span><span class="sxs-lookup"><span data-stu-id="8d81e-290">Note that if you specify a relative path following option `/V`, such as `/V:test/azcopy1.log`, then hello verbose log is created in hello current working directory within a subfolder named `test`.</span></span>

### <a name="specify-hello-number-of-concurrent-operations-toostart"></a><span data-ttu-id="8d81e-291">Especifique o número de Olá de operações simultâneas toostart</span><span class="sxs-lookup"><span data-stu-id="8d81e-291">Specify hello number of concurrent operations toostart</span></span>
<span data-ttu-id="8d81e-292">Opção `/NC` Especifica o número de Olá de operações de cópia em simultâneo.</span><span class="sxs-lookup"><span data-stu-id="8d81e-292">Option `/NC` specifies hello number of concurrent copy operations.</span></span> <span data-ttu-id="8d81e-293">Por predefinição, o AzCopy é iniciado um determinado número de débito de transferência de dados de Olá tooincrease operações simultâneas.</span><span class="sxs-lookup"><span data-stu-id="8d81e-293">By default, AzCopy starts a certain number of concurrent operations tooincrease hello data transfer throughput.</span></span> <span data-ttu-id="8d81e-294">Para operações de tabela, o número de Olá de operações simultâneas é toohello igual número de processadores que tem.</span><span class="sxs-lookup"><span data-stu-id="8d81e-294">For Table operations, hello number of concurrent operations is equal toohello number of processors you have.</span></span> <span data-ttu-id="8d81e-295">Para operações de Blob e o ficheiro, número de Olá de operações simultâneas de é igual número de Olá de 8 horas de processadores que tem.</span><span class="sxs-lookup"><span data-stu-id="8d81e-295">For Blob and File operations, hello number of concurrent operations is equal 8 times hello number of processors you have.</span></span> <span data-ttu-id="8d81e-296">Se estiver a executar o AzCopy através de uma rede de largura de banda reduzida, pode especificar um número inferior de falha de tooavoid /NC causado por concorrência de recursos.</span><span class="sxs-lookup"><span data-stu-id="8d81e-296">If you are running AzCopy across a low-bandwidth network, you can specify a lower number for /NC tooavoid failure caused by resource competition.</span></span>

### <a name="run-azcopy-against-azure-storage-emulator"></a><span data-ttu-id="8d81e-297">Executar o AzCopy no emulador do Storage do Azure</span><span class="sxs-lookup"><span data-stu-id="8d81e-297">Run AzCopy against Azure Storage Emulator</span></span>
<span data-ttu-id="8d81e-298">Pode executar o AzCopy contra Olá [emulador do Storage do Azure](storage-use-emulator.md) para Blobs:</span><span class="sxs-lookup"><span data-stu-id="8d81e-298">You can run AzCopy against hello [Azure Storage Emulator](storage-use-emulator.md) for Blobs:</span></span>

```azcopy
AzCopy /Source:https://127.0.0.1:10000/myaccount/mycontainer/ /Dest:C:\myfolder /SourceKey:key /SourceType:Blob /S
```

<span data-ttu-id="8d81e-299">e tabelas:</span><span class="sxs-lookup"><span data-stu-id="8d81e-299">and Tables:</span></span>

```azcopy
AzCopy /Source:https://127.0.0.1:10002/myaccount/mytable/ /Dest:C:\myfolder /SourceKey:key /SourceType:Table
```

## <a name="azcopy-parameters"></a><span data-ttu-id="8d81e-300">Parâmetros do AzCopy</span><span class="sxs-lookup"><span data-stu-id="8d81e-300">AzCopy Parameters</span></span>
<span data-ttu-id="8d81e-301">Parâmetros para AzCopy são descritos abaixo.</span><span class="sxs-lookup"><span data-stu-id="8d81e-301">Parameters for AzCopy are described below.</span></span> <span data-ttu-id="8d81e-302">Também pode escrever um dos Olá Olá linha de comandos para obter ajuda utilizando o AzCopy para os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="8d81e-302">You can also type one of hello following commands from hello command line for help in using AzCopy:</span></span>

* <span data-ttu-id="8d81e-303">Para obter ajuda detalhada da linha de comandos do AzCopy:`AzCopy /?`</span><span class="sxs-lookup"><span data-stu-id="8d81e-303">For detailed command-line help for AzCopy: `AzCopy /?`</span></span>
* <span data-ttu-id="8d81e-304">Para obter ajuda detalhada com quaisquer parâmetros de AzCopy:`AzCopy /?:SourceKey`</span><span class="sxs-lookup"><span data-stu-id="8d81e-304">For detailed help with any AzCopy parameter: `AzCopy /?:SourceKey`</span></span>
* <span data-ttu-id="8d81e-305">Para obter exemplos da linha de comandos:`AzCopy /?:Samples`</span><span class="sxs-lookup"><span data-stu-id="8d81e-305">For command-line examples: `AzCopy /?:Samples`</span></span>

### <a name="sourcesource"></a><span data-ttu-id="8d81e-306">/ De origem: "origem"</span><span class="sxs-lookup"><span data-stu-id="8d81e-306">/Source:"source"</span></span>
<span data-ttu-id="8d81e-307">Especifica a origem de dados Olá do qual toocopy.</span><span class="sxs-lookup"><span data-stu-id="8d81e-307">Specifies hello source data from which toocopy.</span></span> <span data-ttu-id="8d81e-308">origem de Olá pode ser um diretório do sistema de ficheiros, um contentor de blob, um diretório virtual de blob, uma partilha de ficheiros de armazenamento, um diretório do ficheiro de armazenamento ou uma tabela do Azure.</span><span class="sxs-lookup"><span data-stu-id="8d81e-308">hello source can be a file system directory, a blob container, a blob virtual directory, a storage file share, a storage file directory, or an Azure table.</span></span>

<span data-ttu-id="8d81e-309">**Aplica-se a:** Blobs, ficheiros, tabelas</span><span class="sxs-lookup"><span data-stu-id="8d81e-309">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="destdestination"></a><span data-ttu-id="8d81e-310">/ Dest: "destino"</span><span class="sxs-lookup"><span data-stu-id="8d81e-310">/Dest:"destination"</span></span>
<span data-ttu-id="8d81e-311">Especifica Olá toocopy de destino para.</span><span class="sxs-lookup"><span data-stu-id="8d81e-311">Specifies hello destination toocopy to.</span></span> <span data-ttu-id="8d81e-312">destino de Olá pode ser um diretório do sistema de ficheiros, um contentor de blob, um diretório virtual de blob, uma partilha de ficheiros de armazenamento, um diretório do ficheiro de armazenamento ou uma tabela do Azure.</span><span class="sxs-lookup"><span data-stu-id="8d81e-312">hello destination can be a file system directory, a blob container, a blob virtual directory, a storage file share, a storage file directory, or an Azure table.</span></span>

<span data-ttu-id="8d81e-313">**Aplica-se a:** Blobs, ficheiros, tabelas</span><span class="sxs-lookup"><span data-stu-id="8d81e-313">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="patternfile-pattern"></a><span data-ttu-id="8d81e-314">/ Padrão: "-padrão de ficheiros"</span><span class="sxs-lookup"><span data-stu-id="8d81e-314">/Pattern:"file-pattern"</span></span>
<span data-ttu-id="8d81e-315">Especifica um padrão de ficheiro que indica que toocopy de ficheiros.</span><span class="sxs-lookup"><span data-stu-id="8d81e-315">Specifies a file pattern that indicates which files toocopy.</span></span> <span data-ttu-id="8d81e-316">comportamento de Olá do parâmetro de /Pattern Olá é determinado por localização Olá Olá de dados de origem e a presença de Olá da opção de modo recursivo Olá.</span><span class="sxs-lookup"><span data-stu-id="8d81e-316">hello behavior of hello /Pattern parameter is determined by hello location of hello source data, and hello presence of hello recursive mode option.</span></span> <span data-ttu-id="8d81e-317">Modo recursivo é especificado através da opção /S.</span><span class="sxs-lookup"><span data-stu-id="8d81e-317">Recursive mode is specified via option /S.</span></span>

<span data-ttu-id="8d81e-318">Se origem especificada Olá for um diretório no sistema de ficheiros de Olá, carateres universais padrão estão em vigor e especificar um padrão de ficheiro Olá é comparado com ficheiros dentro do diretório de Olá.</span><span class="sxs-lookup"><span data-stu-id="8d81e-318">If hello specified source is a directory in hello file system, then standard wildcards are in effect, and hello file pattern provided is matched against files within hello directory.</span></span> <span data-ttu-id="8d81e-319">Se a opção que /s for especificado, em seguida, AzCopy também corresponde ao padrão especificado de Olá contra todos os ficheiros em subpastas abaixo diretório Olá.</span><span class="sxs-lookup"><span data-stu-id="8d81e-319">If option /S is specified, then AzCopy also matches hello specified pattern against all files in any subfolders beneath hello directory.</span></span>

<span data-ttu-id="8d81e-320">Se a origem especificada Olá é um contentor de blob ou um diretório virtual, caracteres universais não são aplicadas.</span><span class="sxs-lookup"><span data-stu-id="8d81e-320">If hello specified source is a blob container or virtual directory, then wildcards are not applied.</span></span> <span data-ttu-id="8d81e-321">Se a opção que /s for especificado, em seguida, AzCopy interpreta padrão de ficheiro especificado Olá como um prefixo de blob.</span><span class="sxs-lookup"><span data-stu-id="8d81e-321">If option /S is specified, then AzCopy interprets hello specified file pattern as a blob prefix.</span></span> <span data-ttu-id="8d81e-322">Se a opção que /s não for especificado, em seguida, AzCopy corresponde ao padrão de ficheiro Olá contra dos nomes blob exato.</span><span class="sxs-lookup"><span data-stu-id="8d81e-322">If option /S is not specified, then AzCopy matches hello file pattern against exact blob names.</span></span>

<span data-ttu-id="8d81e-323">Se Olá especificado origem é uma partilha de ficheiros do Azure, tem de especificar ou nome de ficheiro exato de Olá, (por exemplo, abc.txt) toocopy um ficheiro único, ou especificar a opção /S toocopy todos os ficheiros na partilha de Olá em modo recursivo.</span><span class="sxs-lookup"><span data-stu-id="8d81e-323">If hello specified source is an Azure file share, then you must either specify hello exact file name, (e.g. abc.txt) toocopy a single file, or specify option /S toocopy all files in hello share recursively.</span></span> <span data-ttu-id="8d81e-324">Tentativa de toospecify um padrão de ficheiro e a opção /S em conjunto resultará num erro.</span><span class="sxs-lookup"><span data-stu-id="8d81e-324">Attempting toospecify both a file pattern and option /S together will result in an error.</span></span>

<span data-ttu-id="8d81e-325">AzCopy utiliza a correspondência de maiúsculas e minúsculas quando Olá /Source é um contentor de blob ou um diretório virtual de blob e Olá, utiliza sensível correspondentes em todos os outros casos.</span><span class="sxs-lookup"><span data-stu-id="8d81e-325">AzCopy uses case-sensitive matching when hello /Source is a blob container or blob virtual directory, and uses case-insensitive matching in all hello other cases.</span></span>

<span data-ttu-id="8d81e-326">Olá ficheiro padrão predefinido utilizado quando não é especificada nenhuma padrão de ficheiro é *.*</span><span class="sxs-lookup"><span data-stu-id="8d81e-326">hello default file pattern used when no file pattern is specified is *.*</span></span> <span data-ttu-id="8d81e-327">para uma localização de ficheiros de sistema ou um prefixo vazio para uma localização de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="8d81e-327">for a file system location or an empty prefix for an Azure Storage location.</span></span> <span data-ttu-id="8d81e-328">Especificar vários padrões de ficheiro não é suportada.</span><span class="sxs-lookup"><span data-stu-id="8d81e-328">Specifying multiple file patterns is not supported.</span></span>

<span data-ttu-id="8d81e-329">**Aplica-se a:** Blobs, ficheiros</span><span class="sxs-lookup"><span data-stu-id="8d81e-329">**Applicable to:** Blobs, Files</span></span>

### <a name="destkeystorage-key"></a><span data-ttu-id="8d81e-330">/ DestKey: "chave de armazenamento"</span><span class="sxs-lookup"><span data-stu-id="8d81e-330">/DestKey:"storage-key"</span></span>
<span data-ttu-id="8d81e-331">Especifica a chave de conta do storage Olá para o recurso de destino Olá.</span><span class="sxs-lookup"><span data-stu-id="8d81e-331">Specifies hello storage account key for hello destination resource.</span></span>

<span data-ttu-id="8d81e-332">**Aplica-se a:** Blobs, ficheiros, tabelas</span><span class="sxs-lookup"><span data-stu-id="8d81e-332">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="destsassas-token"></a><span data-ttu-id="8d81e-333">/ DestSAS: "sas token"</span><span class="sxs-lookup"><span data-stu-id="8d81e-333">/DestSAS:"sas-token"</span></span>
<span data-ttu-id="8d81e-334">Especifica uma assinatura de acesso partilhado (SAS) com permissões de leitura e escrita para o destino de Olá (se aplicável).</span><span class="sxs-lookup"><span data-stu-id="8d81e-334">Specifies a Shared Access Signature (SAS) with READ and WRITE permissions for hello destination (if applicable).</span></span> <span data-ttu-id="8d81e-335">Coloque Olá SAS com aspas, como pode contém carateres especiais de linha de comandos.</span><span class="sxs-lookup"><span data-stu-id="8d81e-335">Surround hello SAS with double quotes, as it may contains special command-line characters.</span></span>

<span data-ttu-id="8d81e-336">Se o recurso de destino de Olá for um contentor de blob, a partilha de ficheiros ou a tabela, pode especificar esta opção seguida de token SAS de hello, ou pode especificar Olá SAS como parte do contentor de blob de destino Olá, partilha de ficheiros ou URI da tabela, sem esta opção.</span><span class="sxs-lookup"><span data-stu-id="8d81e-336">If hello destination resource is a blob container, file share or table, you can either specify this option followed by hello SAS token, or you can specify hello SAS as part of hello destination blob container, file share or table's URI, without this option.</span></span>

<span data-ttu-id="8d81e-337">Se Olá origem e destino estão ambos os blobs e BLOBs de destino Olá têm de residir no Olá mesmo a conta de armazenamento como blob de origem Olá.</span><span class="sxs-lookup"><span data-stu-id="8d81e-337">If hello source and destination are both blobs, then hello destination blob must reside within hello same storage account as hello source blob.</span></span>

<span data-ttu-id="8d81e-338">**Aplica-se a:** Blobs, ficheiros, tabelas</span><span class="sxs-lookup"><span data-stu-id="8d81e-338">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="sourcekeystorage-key"></a><span data-ttu-id="8d81e-339">/ SourceKey: "chave de armazenamento"</span><span class="sxs-lookup"><span data-stu-id="8d81e-339">/SourceKey:"storage-key"</span></span>
<span data-ttu-id="8d81e-340">Especifica a chave de conta do storage Olá para o recurso de origem Olá.</span><span class="sxs-lookup"><span data-stu-id="8d81e-340">Specifies hello storage account key for hello source resource.</span></span>

<span data-ttu-id="8d81e-341">**Aplica-se a:** Blobs, ficheiros, tabelas</span><span class="sxs-lookup"><span data-stu-id="8d81e-341">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="sourcesassas-token"></a><span data-ttu-id="8d81e-342">/ SourceSAS: "sas token"</span><span class="sxs-lookup"><span data-stu-id="8d81e-342">/SourceSAS:"sas-token"</span></span>
<span data-ttu-id="8d81e-343">Especifica uma assinatura de acesso partilhado com permissões de leitura e de lista para a origem de Olá (se aplicável).</span><span class="sxs-lookup"><span data-stu-id="8d81e-343">Specifies a Shared Access Signature with READ and LIST permissions for hello source (if applicable).</span></span> <span data-ttu-id="8d81e-344">Coloque Olá SAS com aspas, como pode contém carateres especiais de linha de comandos.</span><span class="sxs-lookup"><span data-stu-id="8d81e-344">Surround hello SAS with double quotes, as it may contains special command-line characters.</span></span>

<span data-ttu-id="8d81e-345">Se recursos de origem Olá é um contentor de blob e não uma chave nem uma SAS é fornecida, será possível ler o contentor do blob Olá através do acesso anónimo.</span><span class="sxs-lookup"><span data-stu-id="8d81e-345">If hello source resource is a blob container, and neither a key nor a SAS is provided, then hello blob container will be read via anonymous access.</span></span>

<span data-ttu-id="8d81e-346">Se a origem Olá é uma partilha de ficheiros ou tabela, tem de ser fornecida uma chave ou uma SAS.</span><span class="sxs-lookup"><span data-stu-id="8d81e-346">If hello source is a file share or table, a key or a SAS must be provided.</span></span>

<span data-ttu-id="8d81e-347">**Aplica-se a:** Blobs, ficheiros, tabelas</span><span class="sxs-lookup"><span data-stu-id="8d81e-347">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="s"></a><span data-ttu-id="8d81e-348">/S</span><span class="sxs-lookup"><span data-stu-id="8d81e-348">/S</span></span>
<span data-ttu-id="8d81e-349">Especifica o modo recursivo para operações de cópia.</span><span class="sxs-lookup"><span data-stu-id="8d81e-349">Specifies recursive mode for copy operations.</span></span> <span data-ttu-id="8d81e-350">No modo de recursiva, o AzCopy vai copiar todos os blobs ou ficheiros que correspondam ao padrão de ficheiro especificado Olá, incluindo as existentes na subpastas.</span><span class="sxs-lookup"><span data-stu-id="8d81e-350">In recursive mode, AzCopy will copy all blobs or files that match hello specified file pattern, including those in subfolders.</span></span>

<span data-ttu-id="8d81e-351">**Aplica-se a:** Blobs, ficheiros</span><span class="sxs-lookup"><span data-stu-id="8d81e-351">**Applicable to:** Blobs, Files</span></span>

### <a name="blobtypeblock--page--append"></a><span data-ttu-id="8d81e-352">/ BlobType: "bloquear" | "página" | "acrescentar"</span><span class="sxs-lookup"><span data-stu-id="8d81e-352">/BlobType:"block" | "page" | "append"</span></span>
<span data-ttu-id="8d81e-353">Especifica se o blob de destino Olá é um blob de blocos, um blob de página ou um blob de acréscimo.</span><span class="sxs-lookup"><span data-stu-id="8d81e-353">Specifies whether hello destination blob is a block blob, a page blob, or an append blob.</span></span> <span data-ttu-id="8d81e-354">Esta opção é aplicável apenas quando estiver a carregar um blob.</span><span class="sxs-lookup"><span data-stu-id="8d81e-354">This option is applicable only when you are uploading a blob.</span></span> <span data-ttu-id="8d81e-355">Caso contrário, é gerado um erro.</span><span class="sxs-lookup"><span data-stu-id="8d81e-355">Otherwise, an error is generated.</span></span> <span data-ttu-id="8d81e-356">Se o destino de Olá é um blob e esta opção não for especificada, por predefinição, o AzCopy cria um blob de blocos.</span><span class="sxs-lookup"><span data-stu-id="8d81e-356">If hello destination is a blob and this option is not specified, by default, AzCopy creates a block blob.</span></span>

<span data-ttu-id="8d81e-357">**Aplica-se a:** Blobs</span><span class="sxs-lookup"><span data-stu-id="8d81e-357">**Applicable to:** Blobs</span></span>

### <a name="checkmd5"></a><span data-ttu-id="8d81e-358">/ CheckMD5</span><span class="sxs-lookup"><span data-stu-id="8d81e-358">/CheckMD5</span></span>
<span data-ttu-id="8d81e-359">Calcula um hash MD5 para dados transferidos e verifica se o hash MD5 de Olá armazenados no blob Olá ou propriedade de conteúdo-MD5 do ficheiro corresponda ao hash de Olá calculado.</span><span class="sxs-lookup"><span data-stu-id="8d81e-359">Calculates an MD5 hash for downloaded data and verifies that hello MD5 hash stored in hello blob or file's Content-MD5 property matches hello calculated hash.</span></span> <span data-ttu-id="8d81e-360">verificação de Olá MD5 está desativada por predefinição, pelo que tem de especificar esta verificação de MD5 opção tooperform Olá quando a transferência de dados.</span><span class="sxs-lookup"><span data-stu-id="8d81e-360">hello MD5 check is turned off by default, so you must specify this option tooperform hello MD5 check when downloading data.</span></span>

<span data-ttu-id="8d81e-361">Tenha em atenção que o armazenamento do Azure não garante que Olá hash MD5 para BLOBs Olá ou o ficheiro está atualizado.</span><span class="sxs-lookup"><span data-stu-id="8d81e-361">Note that Azure Storage doesn't guarantee that hello MD5 hash stored for hello blob or file is up-to-date.</span></span> <span data-ttu-id="8d81e-362">É Olá de tooupdate de responsabilidade do cliente MD5 sempre que o blob Olá ou o ficheiro é modificado.</span><span class="sxs-lookup"><span data-stu-id="8d81e-362">It is client's responsibility tooupdate hello MD5 whenever hello blob or file is modified.</span></span>

<span data-ttu-id="8d81e-363">AzCopy sempre define Olá Content-MD5 propriedade para um blob do Azure ou o ficheiro após carregá-lo toohello serviço.</span><span class="sxs-lookup"><span data-stu-id="8d81e-363">AzCopy always sets hello Content-MD5 property for an Azure blob or file after uploading it toohello service.</span></span>  

<span data-ttu-id="8d81e-364">**Aplica-se a:** Blobs, ficheiros</span><span class="sxs-lookup"><span data-stu-id="8d81e-364">**Applicable to:** Blobs, Files</span></span>

### <a name="snapshot"></a><span data-ttu-id="8d81e-365">/ Instantâneo de</span><span class="sxs-lookup"><span data-stu-id="8d81e-365">/Snapshot</span></span>
<span data-ttu-id="8d81e-366">Indica se tootransfer instantâneos.</span><span class="sxs-lookup"><span data-stu-id="8d81e-366">Indicates whether tootransfer snapshots.</span></span> <span data-ttu-id="8d81e-367">Esta opção só é válida quando a origem de Olá é um blob.</span><span class="sxs-lookup"><span data-stu-id="8d81e-367">This option is only valid when hello source is a blob.</span></span>

<span data-ttu-id="8d81e-368">Olá instantâneos do blob transferidos são mudados neste formato: nome do blob (hora de instantâneo) .extension</span><span class="sxs-lookup"><span data-stu-id="8d81e-368">hello transferred blob snapshots are renamed in this format: blob-name (snapshot-time).extension</span></span>

<span data-ttu-id="8d81e-369">Por predefinição, os instantâneos não são copiados.</span><span class="sxs-lookup"><span data-stu-id="8d81e-369">By default, snapshots are not copied.</span></span>

<span data-ttu-id="8d81e-370">**Aplica-se a:** Blobs</span><span class="sxs-lookup"><span data-stu-id="8d81e-370">**Applicable to:** Blobs</span></span>

### <a name="vverbose-log-file"></a><span data-ttu-id="8d81e-371">/ V: [verboso--ficheiro de registo]</span><span class="sxs-lookup"><span data-stu-id="8d81e-371">/V:[verbose-log-file]</span></span>
<span data-ttu-id="8d81e-372">Saídas verboso as mensagens de estado para um ficheiro de registo.</span><span class="sxs-lookup"><span data-stu-id="8d81e-372">Outputs verbose status messages into a log file.</span></span>

<span data-ttu-id="8d81e-373">Por predefinição, o ficheiro de registo verboso Olá é denominado AzCopyVerbose.log no `%LocalAppData%\Microsoft\Azure\AzCopy`.</span><span class="sxs-lookup"><span data-stu-id="8d81e-373">By default, hello verbose log file is named AzCopyVerbose.log in `%LocalAppData%\Microsoft\Azure\AzCopy`.</span></span> <span data-ttu-id="8d81e-374">Se especificar uma localização de ficheiros existentes para esta opção, o registo verboso Olá será anexado toothat ficheiro.</span><span class="sxs-lookup"><span data-stu-id="8d81e-374">If you specify an existing file location for this option, hello verbose log will be appended toothat file.</span></span>  

<span data-ttu-id="8d81e-375">**Aplica-se a:** Blobs, ficheiros, tabelas</span><span class="sxs-lookup"><span data-stu-id="8d81e-375">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="zjournal-file-folder"></a><span data-ttu-id="8d81e-376">/ Z [pasta de ficheiros de diário]</span><span class="sxs-lookup"><span data-stu-id="8d81e-376">/Z:[journal-file-folder]</span></span>
<span data-ttu-id="8d81e-377">Especifica uma pasta de ficheiros do diário de alterações para retomar uma operação.</span><span class="sxs-lookup"><span data-stu-id="8d81e-377">Specifies a journal file folder for resuming an operation.</span></span>

<span data-ttu-id="8d81e-378">AzCopy suporta sempre retomar se uma operação foi interrompida.</span><span class="sxs-lookup"><span data-stu-id="8d81e-378">AzCopy always supports resuming if an operation has been interrupted.</span></span>

<span data-ttu-id="8d81e-379">Se esta opção não for especificada, ou se for especificado sem um caminho de pasta, o AzCopy criar ficheiros do diário de alterações de Olá na localização predefinida de Olá, que é % LocalAppData%\Microsoft\Azure\AzCopy.</span><span class="sxs-lookup"><span data-stu-id="8d81e-379">If this option is not specified, or it is specified without a folder path, then AzCopy will create hello journal file in hello default location, which is %LocalAppData%\Microsoft\Azure\AzCopy.</span></span>

<span data-ttu-id="8d81e-380">Sempre que emitir um comando tooAzCopy, este verifica se existe um ficheiro de diário de alterações na pasta predefinida de hello, ou se existe uma pasta que especificou através desta opção.</span><span class="sxs-lookup"><span data-stu-id="8d81e-380">Each time you issue a command tooAzCopy, it checks whether a journal file exists in hello default folder, or whether it exists in a folder that you specified via this option.</span></span> <span data-ttu-id="8d81e-381">Se não existir um ficheiro do diário de alterações de Olá em qualquer local, o AzCopy trata operação Olá como novo e gera um novo ficheiro de diário de alterações.</span><span class="sxs-lookup"><span data-stu-id="8d81e-381">If hello journal file does not exist in either place, AzCopy treats hello operation as new and generates a new journal file.</span></span>

<span data-ttu-id="8d81e-382">Se existirem ficheiros do diário de alterações de Olá, AzCopy irá verificar se linha de comandos de Olá introduzido corresponde a linha de comandos Olá no ficheiro de diário Olá.</span><span class="sxs-lookup"><span data-stu-id="8d81e-382">If hello journal file does exist, AzCopy will check whether hello command line that you input matches hello command line in hello journal file.</span></span> <span data-ttu-id="8d81e-383">Se duas linhas de comando Olá corresponderem, o AzCopy retoma operação incompleta Olá.</span><span class="sxs-lookup"><span data-stu-id="8d81e-383">If hello two command lines match, AzCopy resumes hello incomplete operation.</span></span> <span data-ttu-id="8d81e-384">Se não corresponderem, será pedido tooeither substituir Olá diário ficheiro toostart uma operação de novo ou toocancel Olá operação atual.</span><span class="sxs-lookup"><span data-stu-id="8d81e-384">If they do not match, you will be prompted tooeither overwrite hello journal file toostart a new operation, or toocancel hello current operation.</span></span>

<span data-ttu-id="8d81e-385">ficheiros do diário de alterações de Olá é eliminado após a conclusão com êxito da operação de Olá.</span><span class="sxs-lookup"><span data-stu-id="8d81e-385">hello journal file is deleted upon successful completion of hello operation.</span></span>

<span data-ttu-id="8d81e-386">Tenha em atenção que a retomar a uma operação a partir de um ficheiro de diário criada por uma versão anterior do AzCopy não é suportada.</span><span class="sxs-lookup"><span data-stu-id="8d81e-386">Note that resuming an operation from a journal file created by a previous version of AzCopy is not supported.</span></span>

<span data-ttu-id="8d81e-387">**Aplica-se a:** Blobs, ficheiros, tabelas</span><span class="sxs-lookup"><span data-stu-id="8d81e-387">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="parameter-file"></a><span data-ttu-id="8d81e-388">/@:"Parameter-File"</span><span class="sxs-lookup"><span data-stu-id="8d81e-388">/@:"parameter-file"</span></span>
<span data-ttu-id="8d81e-389">Especifica um ficheiro que contém os parâmetros.</span><span class="sxs-lookup"><span data-stu-id="8d81e-389">Specifies a file that contains parameters.</span></span> <span data-ttu-id="8d81e-390">Processos do AzCopy Olá parâmetros no ficheiro de Olá como se tivesse sido especificados na linha de comandos Olá.</span><span class="sxs-lookup"><span data-stu-id="8d81e-390">AzCopy processes hello parameters in hello file just as if they had been specified on hello command line.</span></span>

<span data-ttu-id="8d81e-391">No ficheiro de resposta, pode especificar vários parâmetros numa única linha, ou especifique cada parâmetro na sua própria linha.</span><span class="sxs-lookup"><span data-stu-id="8d81e-391">In a response file, you can either specify multiple parameters on a single line, or specify each parameter on its own line.</span></span> <span data-ttu-id="8d81e-392">Tenha em atenção que um parâmetro individuais não pode abranger várias linhas.</span><span class="sxs-lookup"><span data-stu-id="8d81e-392">Note that an individual parameter cannot span multiple lines.</span></span>

<span data-ttu-id="8d81e-393">Ficheiros de resposta podem incluir as linhas de comentários que começam com o símbolo de # Olá.</span><span class="sxs-lookup"><span data-stu-id="8d81e-393">Response files can include comments lines that begin with hello # symbol.</span></span>

<span data-ttu-id="8d81e-394">Pode especificar vários ficheiros de resposta.</span><span class="sxs-lookup"><span data-stu-id="8d81e-394">You can specify multiple response files.</span></span> <span data-ttu-id="8d81e-395">No entanto, tenha em atenção que não suporta o AzCopy aninhadas ficheiros de resposta.</span><span class="sxs-lookup"><span data-stu-id="8d81e-395">However, note that AzCopy does not support nested response files.</span></span>

<span data-ttu-id="8d81e-396">**Aplica-se a:** Blobs, ficheiros, tabelas</span><span class="sxs-lookup"><span data-stu-id="8d81e-396">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="y"></a><span data-ttu-id="8d81e-397">/Y</span><span class="sxs-lookup"><span data-stu-id="8d81e-397">/Y</span></span>
<span data-ttu-id="8d81e-398">Suprime todos os pedidos de confirmação do AzCopy.</span><span class="sxs-lookup"><span data-stu-id="8d81e-398">Suppresses all AzCopy confirmation prompts.</span></span>

<span data-ttu-id="8d81e-399">**Aplica-se a:** Blobs, ficheiros, tabelas</span><span class="sxs-lookup"><span data-stu-id="8d81e-399">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="l"></a><span data-ttu-id="8d81e-400">/L</span><span class="sxs-lookup"><span data-stu-id="8d81e-400">/L</span></span>
<span data-ttu-id="8d81e-401">Especifica uma operação de listagem apenas; Não existem dados são copiados.</span><span class="sxs-lookup"><span data-stu-id="8d81e-401">Specifies a listing operation only; no data is copied.</span></span>

<span data-ttu-id="8d81e-402">AzCopy será interpretar Olá utilizando esta opção como uma simulação de linha de comandos Olá em execução sem esta opção /L e contagem de objetos quantos serão copiados, pode especificar a opção /V em Olá mesmo toocheck quais os objetos que serão copiados no registo verboso Olá de tempo.</span><span class="sxs-lookup"><span data-stu-id="8d81e-402">AzCopy will interpret hello using of this option as a simulation for running hello command line without this option /L and count how many objects will be copied, you can specify option /V at hello same time toocheck which objects will be copied in hello verbose log.</span></span>

<span data-ttu-id="8d81e-403">comportamento de Olá desta opção também é determinado por localização Olá Olá de dados de origem e de presença Olá Olá recursiva modo opção /S e de ficheiros padrão opção /Pattern.</span><span class="sxs-lookup"><span data-stu-id="8d81e-403">hello behavior of this option is also determined by hello location of hello source data and hello presence of hello recursive mode option /S and file pattern option /Pattern.</span></span>

<span data-ttu-id="8d81e-404">AzCopy necessita da permissão de LISTAGEM e de leitura desta localização de origem ao utilizar esta opção.</span><span class="sxs-lookup"><span data-stu-id="8d81e-404">AzCopy requires LIST and READ permission of this source location when using this option.</span></span>

<span data-ttu-id="8d81e-405">**Aplica-se a:** Blobs, ficheiros</span><span class="sxs-lookup"><span data-stu-id="8d81e-405">**Applicable to:** Blobs, Files</span></span>

### <a name="mt"></a><span data-ttu-id="8d81e-406">/MT</span><span class="sxs-lookup"><span data-stu-id="8d81e-406">/MT</span></span>
<span data-ttu-id="8d81e-407">Define toobe Olá mesmo como blob de origem hello ou do ficheiro da hora da última modificação do ficheiro Olá transferido.</span><span class="sxs-lookup"><span data-stu-id="8d81e-407">Sets hello downloaded file's last-modified time toobe hello same as hello source blob or file's.</span></span>

<span data-ttu-id="8d81e-408">**Aplica-se a:** Blobs, ficheiros</span><span class="sxs-lookup"><span data-stu-id="8d81e-408">**Applicable to:** Blobs, Files</span></span>

### <a name="xn"></a><span data-ttu-id="8d81e-409">/XN</span><span class="sxs-lookup"><span data-stu-id="8d81e-409">/XN</span></span>
<span data-ttu-id="8d81e-410">Exclui um recurso de origem mais recente.</span><span class="sxs-lookup"><span data-stu-id="8d81e-410">Excludes a newer source resource.</span></span> <span data-ttu-id="8d81e-411">recurso de Olá não será copiado esteja hello hora da última modificação da origem de Olá Olá igual ou mais recente do que o destino.</span><span class="sxs-lookup"><span data-stu-id="8d81e-411">hello resource will not be copied if hello last modified time of hello source is hello same or newer than destination.</span></span>

<span data-ttu-id="8d81e-412">**Aplica-se a:** Blobs, ficheiros</span><span class="sxs-lookup"><span data-stu-id="8d81e-412">**Applicable to:** Blobs, Files</span></span>

### <a name="xo"></a><span data-ttu-id="8d81e-413">/XO</span><span class="sxs-lookup"><span data-stu-id="8d81e-413">/XO</span></span>
<span data-ttu-id="8d81e-414">Exclui um recurso de origem de anterior.</span><span class="sxs-lookup"><span data-stu-id="8d81e-414">Excludes an older source resource.</span></span> <span data-ttu-id="8d81e-415">recurso de Olá não será copiado esteja hello hora da última modificação da origem de Olá Olá igual ou anterior ao destino.</span><span class="sxs-lookup"><span data-stu-id="8d81e-415">hello resource will not be copied if hello last modified time of hello source is hello same or older than destination.</span></span>

<span data-ttu-id="8d81e-416">**Aplica-se a:** Blobs, ficheiros</span><span class="sxs-lookup"><span data-stu-id="8d81e-416">**Applicable to:** Blobs, Files</span></span>

### <a name="a"></a><span data-ttu-id="8d81e-417">/A</span><span class="sxs-lookup"><span data-stu-id="8d81e-417">/A</span></span>
<span data-ttu-id="8d81e-418">Carrega apenas os ficheiros que têm o atributo de arquivo de Olá definido.</span><span class="sxs-lookup"><span data-stu-id="8d81e-418">Uploads only files that have hello Archive attribute set.</span></span>

<span data-ttu-id="8d81e-419">**Aplica-se a:** Blobs, ficheiros</span><span class="sxs-lookup"><span data-stu-id="8d81e-419">**Applicable to:** Blobs, Files</span></span>

### <a name="iarashcnetoi"></a><span data-ttu-id="8d81e-420">/ IA: [RASHCNETOI]</span><span class="sxs-lookup"><span data-stu-id="8d81e-420">/IA:[RASHCNETOI]</span></span>
<span data-ttu-id="8d81e-421">Carrega apenas os ficheiros com qualquer um dos Olá especificar o conjunto de atributos.</span><span class="sxs-lookup"><span data-stu-id="8d81e-421">Uploads only files that have any of hello specified attributes set.</span></span>

<span data-ttu-id="8d81e-422">Os atributos disponíveis incluem:</span><span class="sxs-lookup"><span data-stu-id="8d81e-422">Available attributes include:</span></span>

* <span data-ttu-id="8d81e-423">R = ficheiros só de leitura</span><span class="sxs-lookup"><span data-stu-id="8d81e-423">R = Read-only files</span></span>
* <span data-ttu-id="8d81e-424">A = ficheiros prontos para arquivar</span><span class="sxs-lookup"><span data-stu-id="8d81e-424">A = Files ready for archiving</span></span>
* <span data-ttu-id="8d81e-425">S = ficheiros de sistema</span><span class="sxs-lookup"><span data-stu-id="8d81e-425">S = System files</span></span>
* <span data-ttu-id="8d81e-426">H = Hidden ficheiros</span><span class="sxs-lookup"><span data-stu-id="8d81e-426">H = Hidden files</span></span>
* <span data-ttu-id="8d81e-427">C = Compressed ficheiros</span><span class="sxs-lookup"><span data-stu-id="8d81e-427">C = Compressed files</span></span>
* <span data-ttu-id="8d81e-428">N = ficheiros Normal</span><span class="sxs-lookup"><span data-stu-id="8d81e-428">N = Normal files</span></span>
* <span data-ttu-id="8d81e-429">I = ficheiros encriptados</span><span class="sxs-lookup"><span data-stu-id="8d81e-429">E = Encrypted files</span></span>
* <span data-ttu-id="8d81e-430">T = ficheiros temporários</span><span class="sxs-lookup"><span data-stu-id="8d81e-430">T = Temporary files</span></span>
* <span data-ttu-id="8d81e-431">O = ficheiros Offline</span><span class="sxs-lookup"><span data-stu-id="8d81e-431">O = Offline files</span></span>
* <span data-ttu-id="8d81e-432">Posso = indexado não ficheiros</span><span class="sxs-lookup"><span data-stu-id="8d81e-432">I = Non-indexed files</span></span>

<span data-ttu-id="8d81e-433">**Aplica-se a:** Blobs, ficheiros</span><span class="sxs-lookup"><span data-stu-id="8d81e-433">**Applicable to:** Blobs, Files</span></span>

### <a name="xarashcnetoi"></a><span data-ttu-id="8d81e-434">/ XA: [RASHCNETOI]</span><span class="sxs-lookup"><span data-stu-id="8d81e-434">/XA:[RASHCNETOI]</span></span>
<span data-ttu-id="8d81e-435">Exclui ficheiros com qualquer um dos Olá especificado conjunto de atributos.</span><span class="sxs-lookup"><span data-stu-id="8d81e-435">Excludes files that have any of hello specified attributes set.</span></span>

<span data-ttu-id="8d81e-436">Os atributos disponíveis incluem:</span><span class="sxs-lookup"><span data-stu-id="8d81e-436">Available attributes include:</span></span>

* <span data-ttu-id="8d81e-437">R = ficheiros só de leitura</span><span class="sxs-lookup"><span data-stu-id="8d81e-437">R = Read-only files</span></span>
* <span data-ttu-id="8d81e-438">A = ficheiros prontos para arquivar</span><span class="sxs-lookup"><span data-stu-id="8d81e-438">A = Files ready for archiving</span></span>
* <span data-ttu-id="8d81e-439">S = ficheiros de sistema</span><span class="sxs-lookup"><span data-stu-id="8d81e-439">S = System files</span></span>
* <span data-ttu-id="8d81e-440">H = Hidden ficheiros</span><span class="sxs-lookup"><span data-stu-id="8d81e-440">H = Hidden files</span></span>
* <span data-ttu-id="8d81e-441">C = Compressed ficheiros</span><span class="sxs-lookup"><span data-stu-id="8d81e-441">C = Compressed files</span></span>
* <span data-ttu-id="8d81e-442">N = ficheiros Normal</span><span class="sxs-lookup"><span data-stu-id="8d81e-442">N = Normal files</span></span>
* <span data-ttu-id="8d81e-443">I = ficheiros encriptados</span><span class="sxs-lookup"><span data-stu-id="8d81e-443">E = Encrypted files</span></span>
* <span data-ttu-id="8d81e-444">T = ficheiros temporários</span><span class="sxs-lookup"><span data-stu-id="8d81e-444">T = Temporary files</span></span>
* <span data-ttu-id="8d81e-445">O = ficheiros Offline</span><span class="sxs-lookup"><span data-stu-id="8d81e-445">O = Offline files</span></span>
* <span data-ttu-id="8d81e-446">Posso = indexado não ficheiros</span><span class="sxs-lookup"><span data-stu-id="8d81e-446">I = Non-indexed files</span></span>

<span data-ttu-id="8d81e-447">**Aplica-se a:** Blobs, ficheiros</span><span class="sxs-lookup"><span data-stu-id="8d81e-447">**Applicable to:** Blobs, Files</span></span>

### <a name="delimiterdelimiter"></a><span data-ttu-id="8d81e-448">/ Delimitador: "delimiter"</span><span class="sxs-lookup"><span data-stu-id="8d81e-448">/Delimiter:"delimiter"</span></span>
<span data-ttu-id="8d81e-449">Indica o caráter delimitador de Olá utilizado toodelimit de diretórios virtuais num nome de blob.</span><span class="sxs-lookup"><span data-stu-id="8d81e-449">Indicates hello delimiter character used toodelimit virtual directories in a blob name.</span></span>

<span data-ttu-id="8d81e-450">Por predefinição, utiliza AzCopy / como caráter de delimitador Olá.</span><span class="sxs-lookup"><span data-stu-id="8d81e-450">By default, AzCopy uses / as hello delimiter character.</span></span> <span data-ttu-id="8d81e-451">No entanto, o AzCopy suporta a utilização de qualquer caráter comuns (por exemplo, @, # ou %) como um delimitador.</span><span class="sxs-lookup"><span data-stu-id="8d81e-451">However, AzCopy supports using any common character (such as @, #, or %) as a delimiter.</span></span> <span data-ttu-id="8d81e-452">Se precisar de tooinclude um destes carateres especiais na linha de comandos Olá, coloque o nome de ficheiro Olá com aspas duplas.</span><span class="sxs-lookup"><span data-stu-id="8d81e-452">If you need tooinclude one of these special characters on hello command line, enclose hello file name with double quotes.</span></span>

<span data-ttu-id="8d81e-453">Esta opção só é aplicável para transferir blobs.</span><span class="sxs-lookup"><span data-stu-id="8d81e-453">This option is only applicable for downloading blobs.</span></span>

<span data-ttu-id="8d81e-454">**Aplica-se a:** Blobs</span><span class="sxs-lookup"><span data-stu-id="8d81e-454">**Applicable to:** Blobs</span></span>

### <a name="ncnumber-of-concurrent-operations"></a><span data-ttu-id="8d81e-455">/ NC: "número-de-em simultâneo-operações de"</span><span class="sxs-lookup"><span data-stu-id="8d81e-455">/NC:"number-of-concurrent-operations"</span></span>
<span data-ttu-id="8d81e-456">Especifica o número de Olá de operações simultâneas.</span><span class="sxs-lookup"><span data-stu-id="8d81e-456">Specifies hello number of concurrent operations.</span></span>

<span data-ttu-id="8d81e-457">AzCopy por predefinição é iniciado um determinado número de débito de transferência de dados de Olá tooincrease operações simultâneas.</span><span class="sxs-lookup"><span data-stu-id="8d81e-457">AzCopy by default starts a certain number of concurrent operations tooincrease hello data transfer throughput.</span></span> <span data-ttu-id="8d81e-458">Tenha em atenção que grande número de operações simultâneas num ambiente de largura de banda baixa pode sobrecarregar a ligação de rede Olá e impedir operações Olá totalmente conclusão.</span><span class="sxs-lookup"><span data-stu-id="8d81e-458">Note that large number of concurrent operations in a low-bandwidth environment may overwhelm hello network connection and prevent hello operations from fully completing.</span></span> <span data-ttu-id="8d81e-459">Limitar operações simultâneas com base na largura de banda disponível real.</span><span class="sxs-lookup"><span data-stu-id="8d81e-459">Throttle concurrent operations based on actual available network bandwidth.</span></span>

<span data-ttu-id="8d81e-460">limite superior de Olá para operações simultâneas é 512.</span><span class="sxs-lookup"><span data-stu-id="8d81e-460">hello upper limit for concurrent operations is 512.</span></span>

<span data-ttu-id="8d81e-461">**Aplica-se a:** Blobs, ficheiros, tabelas</span><span class="sxs-lookup"><span data-stu-id="8d81e-461">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="sourcetypeblob--table"></a><span data-ttu-id="8d81e-462">/ SourceType: "Blob" | "Tabela"</span><span class="sxs-lookup"><span data-stu-id="8d81e-462">/SourceType:"Blob" | "Table"</span></span>
<span data-ttu-id="8d81e-463">Especifica que Olá `source` recursos é um blob disponível no ambiente de desenvolvimento local Olá, em execução no emulador do storage Olá.</span><span class="sxs-lookup"><span data-stu-id="8d81e-463">Specifies that hello `source` resource is a blob available in hello local development environment, running in hello storage emulator.</span></span>

<span data-ttu-id="8d81e-464">**Aplica-se a:** Blobs, tabelas</span><span class="sxs-lookup"><span data-stu-id="8d81e-464">**Applicable to:** Blobs, Tables</span></span>

### <a name="desttypeblob--table"></a><span data-ttu-id="8d81e-465">/ DestType: "Blob" | "Tabela"</span><span class="sxs-lookup"><span data-stu-id="8d81e-465">/DestType:"Blob" | "Table"</span></span>
<span data-ttu-id="8d81e-466">Especifica que Olá `destination` recursos é um blob disponível no ambiente de desenvolvimento local Olá, em execução no emulador do storage Olá.</span><span class="sxs-lookup"><span data-stu-id="8d81e-466">Specifies that hello `destination` resource is a blob available in hello local development environment, running in hello storage emulator.</span></span>

<span data-ttu-id="8d81e-467">**Aplica-se a:** Blobs, tabelas</span><span class="sxs-lookup"><span data-stu-id="8d81e-467">**Applicable to:** Blobs, Tables</span></span>

### <a name="pkrskey1key2key3"></a><span data-ttu-id="8d81e-468">/ PKRS: "key&#1;key&#2;key&#3;..."</span><span class="sxs-lookup"><span data-stu-id="8d81e-468">/PKRS:"key1#key2#key3#..."</span></span>
<span data-ttu-id="8d81e-469">Divisões Olá tooenable de intervalo de chaves de partição exportar dados de tabela em paralelo, o que aumenta a velocidade de Olá Olá da operação de exportação.</span><span class="sxs-lookup"><span data-stu-id="8d81e-469">Splits hello partition key range tooenable exporting table data in parallel, which increases hello speed of hello export operation.</span></span>

<span data-ttu-id="8d81e-470">Se esta opção não for especificada, o AzCopy utiliza entidades de tabela de tooexport um único thread.</span><span class="sxs-lookup"><span data-stu-id="8d81e-470">If this option is not specified, then AzCopy uses a single thread tooexport table entities.</span></span> <span data-ttu-id="8d81e-471">Por exemplo, se hello o utilizador Especifica /PKRS: "aa #bb", em seguida, AzCopy inicia três operações simultâneas.</span><span class="sxs-lookup"><span data-stu-id="8d81e-471">For example, if hello user specifies /PKRS:"aa#bb", then AzCopy starts three concurrent operations.</span></span>

<span data-ttu-id="8d81e-472">Cada operação exporta um dos três intervalos de chaves de partição, conforme mostrado abaixo:</span><span class="sxs-lookup"><span data-stu-id="8d81e-472">Each operation exports one of three partition key ranges, as shown below:</span></span>

  <span data-ttu-id="8d81e-473">[chave de partição primeiro, aa)</span><span class="sxs-lookup"><span data-stu-id="8d81e-473">[first-partition-key, aa)</span></span>

  <span data-ttu-id="8d81e-474">[aa, bb)</span><span class="sxs-lookup"><span data-stu-id="8d81e-474">[aa, bb)</span></span>

  <span data-ttu-id="8d81e-475">[bb, chave de partição último]</span><span class="sxs-lookup"><span data-stu-id="8d81e-475">[bb, last-partition-key]</span></span>

<span data-ttu-id="8d81e-476">**Aplica-se a:** tabelas</span><span class="sxs-lookup"><span data-stu-id="8d81e-476">**Applicable to:** Tables</span></span>

### <a name="splitsizefile-size"></a><span data-ttu-id="8d81e-477">/ SplitSize: "tamanho de ficheiro"</span><span class="sxs-lookup"><span data-stu-id="8d81e-477">/SplitSize:"file-size"</span></span>
<span data-ttu-id="8d81e-478">Especifica Olá ficheiro exportado dividir tamanho em MB, valor mínimo de Olá permitido é 32.</span><span class="sxs-lookup"><span data-stu-id="8d81e-478">Specifies hello exported file split size in MB, hello minimal value allowed is 32.</span></span>

<span data-ttu-id="8d81e-479">Se esta opção não for especificada, o AzCopy irá exportar ficheiro de toosingle de dados de tabela.</span><span class="sxs-lookup"><span data-stu-id="8d81e-479">If this option is not specified, AzCopy will export table data toosingle file.</span></span>

<span data-ttu-id="8d81e-480">Se os dados da tabela Olá são exportado tooa blob e hello tamanho do ficheiro exportado atinge Olá 200 GB limite de tamanho do blob, em seguida, AzCopy dividir ficheiro exportado Olá, mesmo se esta opção não está especificada.</span><span class="sxs-lookup"><span data-stu-id="8d81e-480">If hello table data is exported tooa blob, and hello exported file size reaches hello 200 GB limit for blob size, then AzCopy will split hello exported file, even if this option is not specified.</span></span>

<span data-ttu-id="8d81e-481">**Aplica-se a:** tabelas</span><span class="sxs-lookup"><span data-stu-id="8d81e-481">**Applicable to:** Tables</span></span>

### <a name="entityoperationinsertorskip--insertormerge--insertorreplace"></a><span data-ttu-id="8d81e-482">/ EntityOperation: "InsertOrSkip" | "InsertOrMerge" | "InsertOrReplace"</span><span class="sxs-lookup"><span data-stu-id="8d81e-482">/EntityOperation:"InsertOrSkip" | "InsertOrMerge" | "InsertOrReplace"</span></span>
<span data-ttu-id="8d81e-483">Especifica o comportamento Olá da importação de dados de tabela.</span><span class="sxs-lookup"><span data-stu-id="8d81e-483">Specifies hello table data import behavior.</span></span>

* <span data-ttu-id="8d81e-484">InsertOrSkip - ignora a uma entidade existente ou introduza uma nova entidade se não existir na tabela de Olá.</span><span class="sxs-lookup"><span data-stu-id="8d81e-484">InsertOrSkip - Skips an existing entity or inserts a new entity if it does not exist in hello table.</span></span>
* <span data-ttu-id="8d81e-485">InsertOrMerge - intercala uma entidade existente ou introduza uma nova entidade se não existir na tabela de Olá.</span><span class="sxs-lookup"><span data-stu-id="8d81e-485">InsertOrMerge - Merges an existing entity or inserts a new entity if it does not exist in hello table.</span></span>
* <span data-ttu-id="8d81e-486">InsertOrReplace - substitui uma entidade existente ou introduza uma nova entidade se não existir na tabela de Olá.</span><span class="sxs-lookup"><span data-stu-id="8d81e-486">InsertOrReplace - Replaces an existing entity or inserts a new entity if it does not exist in hello table.</span></span>

<span data-ttu-id="8d81e-487">**Aplica-se a:** tabelas</span><span class="sxs-lookup"><span data-stu-id="8d81e-487">**Applicable to:** Tables</span></span>

### <a name="manifestmanifest-file"></a><span data-ttu-id="8d81e-488">/ Manifesto: "ficheiro de manifesto"</span><span class="sxs-lookup"><span data-stu-id="8d81e-488">/Manifest:"manifest-file"</span></span>
<span data-ttu-id="8d81e-489">Especifica o ficheiro de manifesto Olá de tabela Olá exportar e importar a operação.</span><span class="sxs-lookup"><span data-stu-id="8d81e-489">Specifies hello manifest file for hello table export and import operation.</span></span>

<span data-ttu-id="8d81e-490">Esta opção é opcional durante a operação de exportação de Olá, AzCopy irá gerar um ficheiro de manifesto com o nome predefinido se esta opção não for especificada.</span><span class="sxs-lookup"><span data-stu-id="8d81e-490">This option is optional during hello export operation, AzCopy will generate a manifest file with predefined name if this option is not specified.</span></span>

<span data-ttu-id="8d81e-491">Esta opção é necessária durante a operação de importação de Olá para localizar ficheiros de dados de Olá.</span><span class="sxs-lookup"><span data-stu-id="8d81e-491">This option is required during hello import operation for locating hello data files.</span></span>

<span data-ttu-id="8d81e-492">**Aplica-se a:** tabelas</span><span class="sxs-lookup"><span data-stu-id="8d81e-492">**Applicable to:** Tables</span></span>

### <a name="synccopy"></a><span data-ttu-id="8d81e-493">/ SyncCopy</span><span class="sxs-lookup"><span data-stu-id="8d81e-493">/SyncCopy</span></span>
<span data-ttu-id="8d81e-494">Indica se toosynchronously copiar blobs ou ficheiros entre dois pontos finais de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="8d81e-494">Indicates whether toosynchronously copy blobs or files between two Azure Storage endpoints.</span></span>

<span data-ttu-id="8d81e-495">AzCopy por predefinição utiliza cópia assíncrona do lado do servidor.</span><span class="sxs-lookup"><span data-stu-id="8d81e-495">AzCopy by default uses server-side asynchronous copy.</span></span> <span data-ttu-id="8d81e-496">Especifique este tooperform opção um síncrona copiar, que transfere os blobs ou ficheiros toolocal memória e, em seguida, carrega-os tooAzure armazenamento.</span><span class="sxs-lookup"><span data-stu-id="8d81e-496">Specify this option tooperform a synchronous copy, which downloads blobs or files toolocal memory and then uploads them tooAzure Storage.</span></span>

<span data-ttu-id="8d81e-497">Pode utilizar esta opção quando copiar os ficheiros dentro do armazenamento de BLOBs no armazenamento de ficheiros ou a partir do Blob storage tooFile armazenamento ou vice-versa se.</span><span class="sxs-lookup"><span data-stu-id="8d81e-497">You can use this option when copying files within Blob storage, within File storage, or from Blob storage tooFile storage or vice versa.</span></span>

<span data-ttu-id="8d81e-498">**Aplica-se a:** Blobs, ficheiros</span><span class="sxs-lookup"><span data-stu-id="8d81e-498">**Applicable to:** Blobs, Files</span></span>

### <a name="setcontenttypecontent-type"></a><span data-ttu-id="8d81e-499">/ SetContentType: "content-type"</span><span class="sxs-lookup"><span data-stu-id="8d81e-499">/SetContentType:"content-type"</span></span>
<span data-ttu-id="8d81e-500">Especifica o tipo de conteúdo de MIME de Olá para blobs de destino ou os ficheiros.</span><span class="sxs-lookup"><span data-stu-id="8d81e-500">Specifies hello MIME content type for destination blobs or files.</span></span>

<span data-ttu-id="8d81e-501">Conjuntos de AzCopy Olá o tipo de conteúdo para um blob ou ficheiro tooapplication/octet-stream por predefinição.</span><span class="sxs-lookup"><span data-stu-id="8d81e-501">AzCopy sets hello content type for a blob or file tooapplication/octet-stream by default.</span></span> <span data-ttu-id="8d81e-502">Pode definir o tipo de conteúdo de Olá para todos os blobs ou ficheiros especificando explicitamente um valor para esta opção.</span><span class="sxs-lookup"><span data-stu-id="8d81e-502">You can set hello content type for all blobs or files by explicitly specifying a value for this option.</span></span>

<span data-ttu-id="8d81e-503">Se especificar esta opção sem um valor, em seguida, AzCopy definirá cada blob ou tipo de conteúdo do ficheiro de acordo com tooits extensão de ficheiro.</span><span class="sxs-lookup"><span data-stu-id="8d81e-503">If you specify this option without a value, then AzCopy will set each blob or file's content type according tooits file extension.</span></span>

<span data-ttu-id="8d81e-504">**Aplica-se a:** Blobs, ficheiros</span><span class="sxs-lookup"><span data-stu-id="8d81e-504">**Applicable to:** Blobs, Files</span></span>

### <a name="payloadformatjson--csv"></a><span data-ttu-id="8d81e-505">/ PayloadFormat: "JSON" | "CSV"</span><span class="sxs-lookup"><span data-stu-id="8d81e-505">/PayloadFormat:"JSON" | "CSV"</span></span>
<span data-ttu-id="8d81e-506">Especifica o formato de Olá do ficheiro de dados exportados Olá tabela.</span><span class="sxs-lookup"><span data-stu-id="8d81e-506">Specifies hello format of hello table exported data file.</span></span>

<span data-ttu-id="8d81e-507">Se esta opção não for especificada, por predefinição, AzCopy exporta ficheiro de dados de tabela no formato JSON.</span><span class="sxs-lookup"><span data-stu-id="8d81e-507">If this option is not specified, by default AzCopy exports table data file in JSON format.</span></span>

<span data-ttu-id="8d81e-508">**Aplica-se a:** tabelas</span><span class="sxs-lookup"><span data-stu-id="8d81e-508">**Applicable to:** Tables</span></span>

## <a name="known-issues-and-best-practices"></a><span data-ttu-id="8d81e-509">Problemas conhecidos e melhores práticas</span><span class="sxs-lookup"><span data-stu-id="8d81e-509">Known Issues and Best Practices</span></span>
### <a name="limit-concurrent-writes-while-copying-data"></a><span data-ttu-id="8d81e-510">Limitar escritas em simultâneo ao copiar dados</span><span class="sxs-lookup"><span data-stu-id="8d81e-510">Limit concurrent writes while copying data</span></span>
<span data-ttu-id="8d81e-511">Quando copia blobs ou ficheiros com o AzCopy, tenha em atenção que outra aplicação pode ser modificar Olá dados enquanto estiver a copiar.</span><span class="sxs-lookup"><span data-stu-id="8d81e-511">When you copy blobs or files with AzCopy, keep in mind that another application may be modifying hello data while you are copying it.</span></span> <span data-ttu-id="8d81e-512">Se for possível, certifique-se de que os dados de Olá que estiver a copiar não está a ser modificados durante a operação de cópia de Olá.</span><span class="sxs-lookup"><span data-stu-id="8d81e-512">If possible, ensure that hello data you are copying is not being modified during hello copy operation.</span></span> <span data-ttu-id="8d81e-513">Por exemplo, quando copiar um VHD associado uma máquina virtual do Azure, certifique-se de que não existem outras aplicações atualmente estiver a escrever toohello VHD.</span><span class="sxs-lookup"><span data-stu-id="8d81e-513">For example, when copying a VHD associated with an Azure virtual machine, make sure that no other applications are currently writing toohello VHD.</span></span> <span data-ttu-id="8d81e-514">Uma boa forma toodo trata por leasing Olá recursos toobe copiado.</span><span class="sxs-lookup"><span data-stu-id="8d81e-514">A good way toodo this is by leasing hello resource toobe copied.</span></span> <span data-ttu-id="8d81e-515">Em alternativa, pode criar um instantâneo do VHD de Olá primeiro e, em seguida, copiar o instantâneo de Olá.</span><span class="sxs-lookup"><span data-stu-id="8d81e-515">Alternately, you can create a snapshot of hello VHD first and then copy hello snapshot.</span></span>

<span data-ttu-id="8d81e-516">Se não podem impedir outras aplicações de escrever tooblobs ou ficheiros, enquanto que estão a ser copiados, em seguida, tenha em atenção que, pela tarefa de Olá Olá tempo é concluída, hello recursos copiados podem já não ter paridade completa com recursos de origem Olá.</span><span class="sxs-lookup"><span data-stu-id="8d81e-516">If you cannot prevent other applications from writing tooblobs or files while they are being copied, then keep in mind that by hello time hello job finishes, hello copied resources may no longer have full parity with hello source resources.</span></span>

### <a name="run-one-azcopy-instance-on-one-machine"></a><span data-ttu-id="8d81e-517">Execute uma instância do AzCopy num computador.</span><span class="sxs-lookup"><span data-stu-id="8d81e-517">Run one AzCopy instance on one machine.</span></span>
<span data-ttu-id="8d81e-518">O AzCopy é concebida toomaximize Olá utilização sua máquina recursos tooaccelerate Olá da transferência de dados, recomendamos que execute apenas uma instância do AzCopy num computador e especificar a opção de Olá `/NC` se precisar de mais simultâneas operações.</span><span class="sxs-lookup"><span data-stu-id="8d81e-518">AzCopy is designed toomaximize hello utilization of your machine resource tooaccelerate hello data transfer, we recommend you run only one AzCopy instance on one machine, and specify hello option `/NC` if you need more concurrent operations.</span></span> <span data-ttu-id="8d81e-519">Para obter mais detalhes, escreva `AzCopy /?:NC` na linha de comandos Olá.</span><span class="sxs-lookup"><span data-stu-id="8d81e-519">For more details, type `AzCopy /?:NC` at hello command line.</span></span>

### <a name="enable-fips-compliant-md5-algorithms-for-azcopy-when-you-use-fips-compliant-algorithms-for-encryption-hashing-and-signing"></a><span data-ttu-id="8d81e-520">Ativar os algoritmos de MD5 compatíveis com FIPS para AzCopy quando a "utilização FIPS algoritmos compatíveis com para encriptação, hashing e iniciar sessão".</span><span class="sxs-lookup"><span data-stu-id="8d81e-520">Enable FIPS compliant MD5 algorithms for AzCopy when you "Use FIPS compliant algorithms for encryption, hashing and signing".</span></span>
<span data-ttu-id="8d81e-521">AzCopy por predefinição utiliza Olá de toocalculate de implementação do .NET MD5 MD5 quando copiar objetos, mas existem alguns requisitos de segurança que precisam de definição de MD5 AzCopy tooenable FIPS em conformidade.</span><span class="sxs-lookup"><span data-stu-id="8d81e-521">AzCopy by default uses .NET MD5 implementation toocalculate hello MD5 when copying objects, but there are some security requirements that need AzCopy tooenable FIPS compliant MD5 setting.</span></span>

<span data-ttu-id="8d81e-522">Pode criar um ficheiro App. config `AzCopy.exe.config` com a propriedade `AzureStorageUseV1MD5` e colocá-la reserve com AzCopy.exe.</span><span class="sxs-lookup"><span data-stu-id="8d81e-522">You can create an app.config file `AzCopy.exe.config` with property `AzureStorageUseV1MD5` and put it aside with AzCopy.exe.</span></span>

    <?xml version="1.0" encoding="utf-8" ?>
    <configuration>
      <appSettings>
        <add key="AzureStorageUseV1MD5" value="false"/>
      </appSettings>
    </configuration>

<span data-ttu-id="8d81e-523">Para a propriedade "AzureStorageUseV1MD5" • verdadeiro - valor predefinido de Olá, AzCopy utilizará .NET MD5 implementação.</span><span class="sxs-lookup"><span data-stu-id="8d81e-523">For property "AzureStorageUseV1MD5" • True - hello default value, AzCopy will use .NET MD5 implementation.</span></span>
<span data-ttu-id="8d81e-524">• False – AzCopy utilizará MD5 algoritmo de conformidade FIPS.</span><span class="sxs-lookup"><span data-stu-id="8d81e-524">• False – AzCopy will use FIPS compliant MD5 algorithm.</span></span>

<span data-ttu-id="8d81e-525">Tenha em atenção que algoritmos compatíveis com FIPS está desativada por predefinição no seu computador Windows, pode escrever secpol.msc a janela de execução e verifique este comutador na definição de segurança -> Políticas locais -> segurança Opções -> criptografia de sistema: algoritmos compatíveis com utilização FIPS para encriptação, hashing e iniciar sessão.</span><span class="sxs-lookup"><span data-stu-id="8d81e-525">Note that FIPS compliant algorithms is disabled by default on your Windows machine, you can type secpol.msc in your Run window and check this switch at Security Setting->Local Policy->Security Options->System cryptography: Use FIPS compliant algorithms for encryption, hashing and signing.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8d81e-526">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="8d81e-526">Next steps</span></span>
<span data-ttu-id="8d81e-527">Para obter mais informações sobre o Storage do Azure e AzCopy, consulte toohello os seguintes recursos.</span><span class="sxs-lookup"><span data-stu-id="8d81e-527">For more information about Azure Storage and AzCopy, refer toohello following resources.</span></span>

### <a name="azure-storage-documentation"></a><span data-ttu-id="8d81e-528">Documentação do Storage do Azure:</span><span class="sxs-lookup"><span data-stu-id="8d81e-528">Azure Storage documentation:</span></span>
* [<span data-ttu-id="8d81e-529">Introdução tooAzure armazenamento</span><span class="sxs-lookup"><span data-stu-id="8d81e-529">Introduction tooAzure Storage</span></span>](storage-introduction.md)
* [<span data-ttu-id="8d81e-530">Como toouse Blob storage do .NET</span><span class="sxs-lookup"><span data-stu-id="8d81e-530">How toouse Blob storage from .NET</span></span>](storage-dotnet-how-to-use-blobs.md)
* [<span data-ttu-id="8d81e-531">Como toouse File storage do .NET</span><span class="sxs-lookup"><span data-stu-id="8d81e-531">How toouse File storage from .NET</span></span>](storage-dotnet-how-to-use-files.md)
* [<span data-ttu-id="8d81e-532">Como toouse Table storage do .NET</span><span class="sxs-lookup"><span data-stu-id="8d81e-532">How toouse Table storage from .NET</span></span>](storage-dotnet-how-to-use-tables.md)
* [<span data-ttu-id="8d81e-533">Como toocreate, gerir ou eliminar uma conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="8d81e-533">How toocreate, manage, or delete a storage account</span></span>](storage-create-storage-account.md)
* [<span data-ttu-id="8d81e-534">Transferência de dados com o AzCopy no Linux</span><span class="sxs-lookup"><span data-stu-id="8d81e-534">Transfer data with AzCopy on Linux</span></span>](storage-use-azcopy-linux.md)

### <a name="azure-storage-blog-posts"></a><span data-ttu-id="8d81e-535">Mensagens de blogue de armazenamento do Azure:</span><span class="sxs-lookup"><span data-stu-id="8d81e-535">Azure Storage blog posts:</span></span>
* [<span data-ttu-id="8d81e-536">Introdução ao pré-visualização de biblioteca de movimento de dados de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="8d81e-536">Introducing Azure Storage Data Movement Library Preview</span></span>](https://azure.microsoft.com/blog/introducing-azure-storage-data-movement-library-preview-2/)
* [<span data-ttu-id="8d81e-537">AzCopy: Introdução ao copiar síncrona e tipo de conteúdo personalizado</span><span class="sxs-lookup"><span data-stu-id="8d81e-537">AzCopy: Introducing synchronous copy and customized content type</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2015/01/13/azcopy-introducing-synchronous-copy-and-customized-content-type.aspx)
* [<span data-ttu-id="8d81e-538">AzCopy: Anunciar disponibilidade geral do 3.0 AzCopy plus versão de pré-visualização do AzCopy 4.0 com suporte de tabela e ficheiro</span><span class="sxs-lookup"><span data-stu-id="8d81e-538">AzCopy: Announcing General Availability of AzCopy 3.0 plus preview release of AzCopy 4.0 with Table and File support</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/10/29/azcopy-announcing-general-availability-of-azcopy-3-0-plus-preview-release-of-azcopy-4-0-with-table-and-file-support.aspx)
* [<span data-ttu-id="8d81e-539">AzCopy: Otimizado para cenários de cópia em grande escala</span><span class="sxs-lookup"><span data-stu-id="8d81e-539">AzCopy: Optimized for Large-Scale Copy Scenarios</span></span>](http://go.microsoft.com/fwlink/?LinkId=507682)
* [<span data-ttu-id="8d81e-540">AzCopy: Suporte para o armazenamento georredundante com acesso de leitura</span><span class="sxs-lookup"><span data-stu-id="8d81e-540">AzCopy: Support for read-access geo-redundant storage</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/04/07/azcopy-support-for-read-access-geo-redundant-account.aspx)
* [<span data-ttu-id="8d81e-541">AzCopy: Transferir dados com o modo novamente iniciável e o SAS token</span><span class="sxs-lookup"><span data-stu-id="8d81e-541">AzCopy: Transfer data with re-startable mode and SAS token</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2013/09/07/azcopy-transfer-data-with-re-startable-mode-and-sas-token.aspx)
* [<span data-ttu-id="8d81e-542">AzCopy: Utilizando o Blob de cópia de conta em vários locais</span><span class="sxs-lookup"><span data-stu-id="8d81e-542">AzCopy: Using cross-account Copy Blob</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2013/04/01/azcopy-using-cross-account-copy-blob.aspx)
* [<span data-ttu-id="8d81e-543">AzCopy: Carregar/transferência de ficheiros para Blobs do Azure</span><span class="sxs-lookup"><span data-stu-id="8d81e-543">AzCopy: Uploading/downloading files for Azure Blobs</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/12/03/azcopy-uploading-downloading-files-for-windows-azure-blobs.aspx)

