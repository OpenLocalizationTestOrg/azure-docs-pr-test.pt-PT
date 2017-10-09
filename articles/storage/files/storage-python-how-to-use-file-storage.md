---
title: aaaDevelop para o File storage do Azure com o Python | Microsoft Docs
description: "Saiba como aplicações de Python toodevelop e serviços que utilizam toostore de armazenamento de ficheiros do Azure de ficheiros de dados."
services: storage
documentationcenter: python
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 297f3a14-6b3a-48b0-9da4-db5907827fb5
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 12/08/2016
ms.author: robinsh
ms.openlocfilehash: 2adc5aac2765b98a8022ab1f706c1fcdbca1b43c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="develop-for-azure-file-storage-with-python"></a><span data-ttu-id="83a55-103">Desenvolver para o File storage do Azure com o Python</span><span class="sxs-lookup"><span data-stu-id="83a55-103">Develop for Azure File storage with Python</span></span>
[!INCLUDE [storage-selector-file-include](../../../includes/storage-selector-file-include.md)]

[!INCLUDE [storage-try-azure-tools-files](../../../includes/storage-try-azure-tools-files.md)]

## <a name="about-this-tutorial"></a><span data-ttu-id="83a55-104">Acerca deste tutorial</span><span class="sxs-lookup"><span data-stu-id="83a55-104">About this tutorial</span></span>
<span data-ttu-id="83a55-105">Este tutorial demonstrar Noções básicas de Olá da utilização de aplicações do Python toodevelop ou serviços que utilizam dados de ficheiros de toostore de armazenamento de ficheiros do Azure.</span><span class="sxs-lookup"><span data-stu-id="83a55-105">This tutorial will demonstrate hello basics of using Python toodevelop applications or services that use Azure File storage toostore file data.</span></span> <span data-ttu-id="83a55-106">Neste tutorial, iremos criar uma aplicação de consola simples e Mostrar como tooperform ações básicas com o storage do Python e ficheiros do Azure:</span><span class="sxs-lookup"><span data-stu-id="83a55-106">In this tutorial, we will create a simple console application and show how tooperform basic actions with Python and Azure File storage:</span></span>

* <span data-ttu-id="83a55-107">Criar partilhas de ficheiros do Azure</span><span class="sxs-lookup"><span data-stu-id="83a55-107">Create Azure File shares</span></span>
* <span data-ttu-id="83a55-108">Criar diretórios</span><span class="sxs-lookup"><span data-stu-id="83a55-108">Create directories</span></span>
* <span data-ttu-id="83a55-109">Enumerar ficheiros e diretórios numa partilha de ficheiros do Azure</span><span class="sxs-lookup"><span data-stu-id="83a55-109">Enumerate files and directories in an Azure File share</span></span>
* <span data-ttu-id="83a55-110">Carregar, transferir e eliminar um ficheiro</span><span class="sxs-lookup"><span data-stu-id="83a55-110">Upload, download, and delete a file</span></span>

> [!Note]  
> <span data-ttu-id="83a55-111">Porque o File storage do Azure pode ser acedido através de SMB, é possível toowrite aplicações simples que aceder à partilha de ficheiros do Azure Olá utilizando Olá padrão e/s de Python classes e funções.</span><span class="sxs-lookup"><span data-stu-id="83a55-111">Because Azure File storage may be accessed over SMB, it is possible toowrite simple applications that access hello Azure File share using hello standard Python I/O classes and functions.</span></span> <span data-ttu-id="83a55-112">Este artigo descreve como toowrite aplicações que utilizam Olá Azure armazenamento Python SDK, que utiliza Olá [File storage do Azure REST API](https://docs.microsoft.com/en-us/rest/api/storageservices/fileservices/file-service-rest-api) tootalk tooAzure armazenamento de ficheiros.</span><span class="sxs-lookup"><span data-stu-id="83a55-112">This article will describe how toowrite applications that use hello Azure Storage Python SDK, which uses hello [Azure File storage REST API](https://docs.microsoft.com/en-us/rest/api/storageservices/fileservices/file-service-rest-api) tootalk tooAzure File storage.</span></span>

### <a name="set-up-your-application-toouse-azure-file-storage"></a><span data-ttu-id="83a55-113">Configurar a sua aplicação toouse File storage do Azure</span><span class="sxs-lookup"><span data-stu-id="83a55-113">Set up your application toouse Azure File storage</span></span>
<span data-ttu-id="83a55-114">Adicione o seguinte de Olá perto Olá parte superior do ficheiro de origem qualquer Python no qual pretende tooprogrammatically acesso Storage do Azure.</span><span class="sxs-lookup"><span data-stu-id="83a55-114">Add hello following near hello top of any Python source file in which you wish tooprogrammatically access Azure Storage.</span></span>

```python
from azure.storage.file import FileService
```

### <a name="set-up-a-connection-tooazure-file-storage"></a><span data-ttu-id="83a55-115">Configurar uma ligação tooAzure armazenamento de ficheiros</span><span class="sxs-lookup"><span data-stu-id="83a55-115">Set up a connection tooAzure File storage</span></span> 
<span data-ttu-id="83a55-116">Olá `FileService` objeto permite-lhe trabalhar com partilhas, diretórios e ficheiros.</span><span class="sxs-lookup"><span data-stu-id="83a55-116">hello `FileService` object lets you work with shares, directories and files.</span></span> <span data-ttu-id="83a55-117">Olá código seguinte cria um `FileService` utilizando Olá chave conta do storage conta e o nome do objeto.</span><span class="sxs-lookup"><span data-stu-id="83a55-117">hello following code creates a `FileService` object using hello storage account name and account key.</span></span> <span data-ttu-id="83a55-118">Substitua `<myaccount>` e `<mykey>` com o nome da conta e a chave.</span><span class="sxs-lookup"><span data-stu-id="83a55-118">Replace `<myaccount>` and `<mykey>` with your account name and key.</span></span>

```python
file_service = FileService(account_name='myaccount', account_key='mykey')
```

### <a name="create-an-azure-file-share"></a><span data-ttu-id="83a55-119">Criar uma partilha de ficheiros do Azure</span><span class="sxs-lookup"><span data-stu-id="83a55-119">Create an Azure File share</span></span>
<span data-ttu-id="83a55-120">No seguinte exemplo de código de Olá, pode utilizar um `FileService` partilha de Olá de toocreate objeto se não existir.</span><span class="sxs-lookup"><span data-stu-id="83a55-120">In hello following code example, you can use a `FileService` object toocreate hello share if it doesn't exist.</span></span>

```python
file_service.create_share('myshare')
```

### <a name="create-a-directory"></a><span data-ttu-id="83a55-121">Criar um diretório</span><span class="sxs-lookup"><span data-stu-id="83a55-121">Create a directory</span></span>
<span data-ttu-id="83a55-122">Também pode organizar armazenamento colocando os ficheiros secundárias diretórios em vez de ter todos eles no diretório de raiz de Olá.</span><span class="sxs-lookup"><span data-stu-id="83a55-122">You can also organize storage by putting files inside sub-directories instead of having all of them in hello root directory.</span></span> <span data-ttu-id="83a55-123">File storage do Azure permite-lhe toocreate como muitos diretórios como a sua conta irá permitem.</span><span class="sxs-lookup"><span data-stu-id="83a55-123">Azure File storage allows you toocreate as many directories as your account will allow.</span></span> <span data-ttu-id="83a55-124">código de Olá abaixo irá criar um subdiretório com o nome **sampledir** no diretório de raiz de Olá.</span><span class="sxs-lookup"><span data-stu-id="83a55-124">hello code below will create a sub-directory named **sampledir** under hello root directory.</span></span>

```python
file_service.create_directory('myshare', 'sampledir')
```

### <a name="enumerate-files-and-directories-in-an-azure-file-share"></a><span data-ttu-id="83a55-125">Enumerar ficheiros e diretórios numa partilha de ficheiros do Azure</span><span class="sxs-lookup"><span data-stu-id="83a55-125">Enumerate files and directories in an Azure File share</span></span>
<span data-ttu-id="83a55-126">ficheiros de Olá toolist e diretórios numa partilha, utilize Olá **lista\_diretórios\_e\_ficheiros** método.</span><span class="sxs-lookup"><span data-stu-id="83a55-126">toolist hello files and directories in a share, use hello **list\_directories\_and\_files** method.</span></span> <span data-ttu-id="83a55-127">Este método devolve um gerador de dimensões.</span><span class="sxs-lookup"><span data-stu-id="83a55-127">This method returns a generator.</span></span> <span data-ttu-id="83a55-128">Olá seguinte código produz Olá **nome** de cada ficheiro e diretório numa partilha toohello consola.</span><span class="sxs-lookup"><span data-stu-id="83a55-128">hello following code outputs hello **name** of each file and directory in a share toohello console.</span></span>

```python
generator = file_service.list_directories_and_files('myshare')
for file_or_dir in generator:
    print(file_or_dir.name)
```

### <a name="upload-a-file"></a><span data-ttu-id="83a55-129">Carregar um ficheiro</span><span class="sxs-lookup"><span data-stu-id="83a55-129">Upload a file</span></span> 
<span data-ttu-id="83a55-130">Ficheiros do Azure partilha contém em Olá muito menos, um diretório de raiz, onde podem residir os ficheiros.</span><span class="sxs-lookup"><span data-stu-id="83a55-130">Azure File share contains at hello very least, a root directory where files can reside.</span></span> <span data-ttu-id="83a55-131">Nesta secção, irá aprender como tooupload um ficheiro a partir do armazenamento local para Olá raiz do diretório de uma partilha.</span><span class="sxs-lookup"><span data-stu-id="83a55-131">In this section, you'll learn how tooupload a file from local storage onto hello root directory of a share.</span></span>

<span data-ttu-id="83a55-132">toocreate um ficheiro e os dados de carregamento, utilize Olá `create_file_from_path`, `create_file_from_stream`, `create_file_from_bytes` ou `create_file_from_text` métodos.</span><span class="sxs-lookup"><span data-stu-id="83a55-132">toocreate a file and upload data, use hello `create_file_from_path`, `create_file_from_stream`, `create_file_from_bytes` or `create_file_from_text` methods.</span></span> <span data-ttu-id="83a55-133">Estes são os métodos de alto nível que executam Olá necessário segmentação quando o tamanho de Olá dos dados de Olá exceder 64 MB.</span><span class="sxs-lookup"><span data-stu-id="83a55-133">They are high-level methods that perform hello necessary chunking when hello size of hello data exceeds 64 MB.</span></span>

<span data-ttu-id="83a55-134">`create_file_from_path`carregamentos Olá conteúdos de um ficheiro do caminho especificado Olá e `create_file_from_stream` carregamentos Olá conteúdo a partir de um fluxo/ficheiro já está aberto.</span><span class="sxs-lookup"><span data-stu-id="83a55-134">`create_file_from_path` uploads hello contents of a file from hello specified path, and `create_file_from_stream` uploads hello contents from an already opened file/stream.</span></span> <span data-ttu-id="83a55-135">`create_file_from_bytes`carrega uma matriz de bytes, e `create_file_from_text` carregamentos Olá especificado de valor de texto utilizando Olá especificado codificação (as predefinições tooUTF-8).</span><span class="sxs-lookup"><span data-stu-id="83a55-135">`create_file_from_bytes` uploads an array of bytes, and `create_file_from_text` uploads hello specified text value using hello specified encoding (defaults tooUTF-8).</span></span>

<span data-ttu-id="83a55-136">Olá exemplo seguinte carrega conteúdo Olá Olá **sunset.png** ficheiro para Olá **myfile** ficheiro.</span><span class="sxs-lookup"><span data-stu-id="83a55-136">hello following example uploads hello contents of hello **sunset.png** file into hello **myfile** file.</span></span>

```python
from azure.storage.file import ContentSettings
file_service.create_file_from_path(
    'myshare',
    None, # We want toocreate this blob in hello root directory, so we specify None for hello directory_name
    'myfile',
    'sunset.png',
    content_settings=ContentSettings(content_type='image/png'))
```

### <a name="download-a-file"></a><span data-ttu-id="83a55-137">Transferir um ficheiro</span><span class="sxs-lookup"><span data-stu-id="83a55-137">Download a file</span></span>
<span data-ttu-id="83a55-138">utilizar dados toodownload partir de um ficheiro `get_file_to_path`, `get_file_to_stream`, `get_file_to_bytes`, ou `get_file_to_text`.</span><span class="sxs-lookup"><span data-stu-id="83a55-138">toodownload data from a file, use `get_file_to_path`, `get_file_to_stream`, `get_file_to_bytes`, or `get_file_to_text`.</span></span> <span data-ttu-id="83a55-139">Estes são os métodos de alto nível que executam Olá necessário segmentação quando o tamanho de Olá dos dados de Olá exceder 64 MB.</span><span class="sxs-lookup"><span data-stu-id="83a55-139">They are high-level methods that perform hello necessary chunking when hello size of hello data exceeds 64 MB.</span></span>

<span data-ttu-id="83a55-140">Olá exemplo seguinte demonstra utilizando `get_file_to_path` conteúdo Olá toodownload Olá **myfile** de ficheiros e armazená-las toohello **fora sunset.png** ficheiro.</span><span class="sxs-lookup"><span data-stu-id="83a55-140">hello following example demonstrates using `get_file_to_path` toodownload hello contents of hello **myfile** file and store it toohello **out-sunset.png** file.</span></span>

```python
file_service.get_file_to_path('myshare', None, 'myfile', 'out-sunset.png')
```

### <a name="delete-a-file"></a><span data-ttu-id="83a55-141">Eliminar um ficheiro</span><span class="sxs-lookup"><span data-stu-id="83a55-141">Delete a file</span></span>
<span data-ttu-id="83a55-142">Por fim, toodelete um ficheiro, chamar `delete_file`.</span><span class="sxs-lookup"><span data-stu-id="83a55-142">Finally, toodelete a file, call `delete_file`.</span></span>

```python
file_service.delete_file('myshare', None, 'myfile')
```

## <a name="next-steps"></a><span data-ttu-id="83a55-143">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="83a55-143">Next steps</span></span>
<span data-ttu-id="83a55-144">Agora que aprendeu como toomanipulate File storage do Azure com o Python, siga estas toolearn ligações mais.</span><span class="sxs-lookup"><span data-stu-id="83a55-144">Now that you've learned how toomanipulate Azure File storage with Python, follow these links toolearn more.</span></span>

* [<span data-ttu-id="83a55-145">Centro para Programadores do Python</span><span class="sxs-lookup"><span data-stu-id="83a55-145">Python Developer Center</span></span>](/develop/python/)
* [<span data-ttu-id="83a55-146">API REST dos Serviços do Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="83a55-146">Azure Storage Services REST API</span></span>](http://msdn.microsoft.com/library/azure/dd179355)
* [<span data-ttu-id="83a55-147">Armazenamento do Microsoft Azure SDK para Python</span><span class="sxs-lookup"><span data-stu-id="83a55-147">Microsoft Azure Storage SDK for Python</span></span>](https://github.com/Azure/azure-storage-python)