---
title: aaaHow toouse PowerShell toomanage File storage do Azure | Microsoft Docs
description: Saiba toouse PowerShell toomanage File storage do Azure.
services: storage
documentationcenter: 
author: RenaShahMSFT
manager: aungoo
editor: tysonn
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/27/2017
ms.author: renash
ms.openlocfilehash: 7bd84c9cfa31782aedf4a209cb15d4b8d92e2737
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-powershell-toomanage-azure-file-storage"></a><span data-ttu-id="22c1d-103">Como toouse PowerShell toomanage File storage do Azure</span><span class="sxs-lookup"><span data-stu-id="22c1d-103">How toouse PowerShell toomanage Azure File storage</span></span>
<span data-ttu-id="22c1d-104">Pode utilizar o Azure PowerShell toocreate e gerir partilhas de ficheiros.</span><span class="sxs-lookup"><span data-stu-id="22c1d-104">You can use Azure PowerShell toocreate and manage file shares.</span></span>

## <a name="install-hello-powershell-cmdlets-for-azure-storage"></a><span data-ttu-id="22c1d-105">Instalar os cmdlets do PowerShell Olá para o Storage do Azure</span><span class="sxs-lookup"><span data-stu-id="22c1d-105">Install hello PowerShell cmdlets for Azure Storage</span></span>
<span data-ttu-id="22c1d-106">tooprepare toouse PowerShell, transfira e instale os cmdlets do PowerShell do Azure de Olá.</span><span class="sxs-lookup"><span data-stu-id="22c1d-106">tooprepare toouse PowerShell, download and install hello Azure PowerShell cmdlets.</span></span> <span data-ttu-id="22c1d-107">Consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azureps-cmdlets-docs) para Olá instalar instruções de instalação e do ponto.</span><span class="sxs-lookup"><span data-stu-id="22c1d-107">See [How tooinstall and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) for hello install point and installation instructions.</span></span>

> [!NOTE]
> <span data-ttu-id="22c1d-108">Recomenda-se transferir e instalar ou atualizar o módulo Azure PowerShell mais recente do toohello.</span><span class="sxs-lookup"><span data-stu-id="22c1d-108">It's recommended that you download and install or upgrade toohello latest Azure PowerShell module.</span></span>
> 
> 

<span data-ttu-id="22c1d-109">Abra uma janela do Azure PowerShell ao clicar em **Iniciar** e escrever **Windows PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="22c1d-109">Open an Azure PowerShell window by clicking **Start** and typing **Windows PowerShell**.</span></span> <span data-ttu-id="22c1d-110">janela do PowerShell Olá carrega o módulo do Azure Powershell Olá por si.</span><span class="sxs-lookup"><span data-stu-id="22c1d-110">hello PowerShell window loads hello Azure Powershell module for you.</span></span>

## <a name="create-a-context-for-your-storage-account-and-key"></a><span data-ttu-id="22c1d-111">Criar um contexto para a conta de armazenamento e a chave</span><span class="sxs-lookup"><span data-stu-id="22c1d-111">Create a context for your storage account and key</span></span>
<span data-ttu-id="22c1d-112">Crie um contexto de conta de armazenamento Olá.</span><span class="sxs-lookup"><span data-stu-id="22c1d-112">Create hello storage account context.</span></span> <span data-ttu-id="22c1d-113">contexto de Olá encapsula Olá chave conta do storage nome e a conta.</span><span class="sxs-lookup"><span data-stu-id="22c1d-113">hello context encapsulates hello storage account name and account key.</span></span> <span data-ttu-id="22c1d-114">Para obter instruções sobre a cópia da sua chave de conta de Olá [portal do Azure](https://portal.azure.com), consulte [ver e copiar chaves de acesso de armazenamento](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json#view-and-copy-storage-access-keys).</span><span class="sxs-lookup"><span data-stu-id="22c1d-114">For instructions on copying your account key from hello [Azure portal](https://portal.azure.com), see [View and copy storage access keys](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json#view-and-copy-storage-access-keys).</span></span>

<span data-ttu-id="22c1d-115">Substitua `storage-account-name` e `storage-account-key` com o nome da conta de armazenamento e a chave no seguinte exemplo de Olá.</span><span class="sxs-lookup"><span data-stu-id="22c1d-115">Replace `storage-account-name` and `storage-account-key` with your storage account name and key in hello following example.</span></span>

```powershell
# create a context for account and key
$ctx=New-AzureStorageContext storage-account-name storage-account-key
```

## <a name="create-a-new-file-share"></a><span data-ttu-id="22c1d-116">Criar uma nova partilha de ficheiros</span><span class="sxs-lookup"><span data-stu-id="22c1d-116">Create a new file share</span></span>
<span data-ttu-id="22c1d-117">Criar Olá nova partilha, com o nome `logs`.</span><span class="sxs-lookup"><span data-stu-id="22c1d-117">Create hello new share, named `logs`.</span></span>

```powershell
# create a new share
$s = New-AzureStorageShare logs -Context $ctx
```

<span data-ttu-id="22c1d-118">Tem agora uma partilha de ficheiros no Armazenamento de ficheiros.</span><span class="sxs-lookup"><span data-stu-id="22c1d-118">You now have a file share in File storage.</span></span> <span data-ttu-id="22c1d-119">Em seguida, vamos adicionar um diretório e um ficheiro.</span><span class="sxs-lookup"><span data-stu-id="22c1d-119">Next we'll add a directory and a file.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="22c1d-120">Olá nome da partilha de ficheiros tem de ser todo em minúsculas.</span><span class="sxs-lookup"><span data-stu-id="22c1d-120">hello name of your file share must be all lowercase.</span></span> <span data-ttu-id="22c1d-121">Para obter detalhes completos sobre a nomenclatura de partilhas de ficheiros e ficheiros, veja [Naming and Referencing Shares, Directories, Files, and Metadata (Nomenclatura e Referência de Partilhas, Diretórios, Ficheiros e Metadados)](https://msdn.microsoft.com/library/azure/dn167011.aspx).</span><span class="sxs-lookup"><span data-stu-id="22c1d-121">For complete details about naming file shares and files, see [Naming and Referencing Shares, Directories, Files, and Metadata](https://msdn.microsoft.com/library/azure/dn167011.aspx).</span></span>
> 
> 

## <a name="create-a-directory-in-hello-file-share"></a><span data-ttu-id="22c1d-122">Crie um diretório na partilha de ficheiros de Olá</span><span class="sxs-lookup"><span data-stu-id="22c1d-122">Create a directory in hello file share</span></span>
<span data-ttu-id="22c1d-123">Crie um diretório na partilha de Olá.</span><span class="sxs-lookup"><span data-stu-id="22c1d-123">Create a directory in hello share.</span></span> <span data-ttu-id="22c1d-124">Diretório de Olá com o nome no seguinte exemplo de Olá, `CustomLogs`.</span><span class="sxs-lookup"><span data-stu-id="22c1d-124">In hello following example, hello directory is named `CustomLogs`.</span></span>

```powershell
# create a directory in hello share
New-AzureStorageDirectory -Share $s -Path CustomLogs
```

## <a name="upload-a-local-file-toohello-directory"></a><span data-ttu-id="22c1d-125">Carregar um diretório do ficheiro local toohello</span><span class="sxs-lookup"><span data-stu-id="22c1d-125">Upload a local file toohello directory</span></span>
<span data-ttu-id="22c1d-126">Agora carregue um diretório do ficheiro local toohello.</span><span class="sxs-lookup"><span data-stu-id="22c1d-126">Now upload a local file toohello directory.</span></span> <span data-ttu-id="22c1d-127">Olá exemplo seguinte carrega um ficheiro de `C:\temp\Log1.txt`.</span><span class="sxs-lookup"><span data-stu-id="22c1d-127">hello following example uploads a file from `C:\temp\Log1.txt`.</span></span> <span data-ttu-id="22c1d-128">Edite o caminho do ficheiro Olá para que aponte tooa ficheiro válido no seu computador local.</span><span class="sxs-lookup"><span data-stu-id="22c1d-128">Edit hello file path so that it points tooa valid file on your local machine.</span></span>

```powershell
# upload a local file toohello new directory
Set-AzureStorageFileContent -Share $s -Source C:\temp\Log1.txt -Path CustomLogs
```

## <a name="list-hello-files-in-hello-directory"></a><span data-ttu-id="22c1d-129">Listar Olá ficheiros no diretório de Olá</span><span class="sxs-lookup"><span data-stu-id="22c1d-129">List hello files in hello directory</span></span>
<span data-ttu-id="22c1d-130">ficheiro de Olá toosee no diretório de Olá, pode listar todos os ficheiros do diretório de Olá.</span><span class="sxs-lookup"><span data-stu-id="22c1d-130">toosee hello file in hello directory, you can list all of hello directory's files.</span></span> <span data-ttu-id="22c1d-131">Este comando devolve Olá ficheiros e subdiretórios (se existir alguma) no diretório do Olá CustomLogs.</span><span class="sxs-lookup"><span data-stu-id="22c1d-131">This command returns hello files and subdirectories (if there are any) in hello CustomLogs directory.</span></span>

```powershell
# list files in hello new directory
Get-AzureStorageFile -Share $s -Path CustomLogs | Get-AzureStorageFile
```

<span data-ttu-id="22c1d-132">Get-AzureStorageFile devolve uma lista de ficheiros e diretórios para qualquer diretório no qual o objeto passa.</span><span class="sxs-lookup"><span data-stu-id="22c1d-132">Get-AzureStorageFile returns a list of files and directories for whatever directory object is passed in.</span></span> <span data-ttu-id="22c1d-133">"Get-AzureStorageFile-partilhar $s" devolve uma lista de ficheiros e diretórios no diretório de raiz de Olá.</span><span class="sxs-lookup"><span data-stu-id="22c1d-133">"Get-AzureStorageFile -Share $s" returns a list of files and directories in hello root directory.</span></span> <span data-ttu-id="22c1d-134">tooget uma lista de ficheiros num subdiretório, tem de toopass Olá subdiretório tooGet-AzureStorageFile.</span><span class="sxs-lookup"><span data-stu-id="22c1d-134">tooget a list of files in a subdirectory, you have toopass hello subdirectory tooGet-AzureStorageFile.</span></span> <span data-ttu-id="22c1d-135">Que é que isto faz – Olá primeira parte comando Olá segurança toohello pipe devolve uma instância de diretório do subdiretório Olá CustomLogs.</span><span class="sxs-lookup"><span data-stu-id="22c1d-135">That's what this does -- hello first part of hello command up toohello pipe returns a directory instance of hello subdirectory CustomLogs.</span></span> <span data-ttu-id="22c1d-136">Em seguida, é passado para o Get-AzureStorageFile, que devolve Olá ficheiros e diretórios no CustomLogs.</span><span class="sxs-lookup"><span data-stu-id="22c1d-136">Then that is passed into Get-AzureStorageFile, which returns hello files and directories in CustomLogs.</span></span>

## <a name="copy-files"></a><span data-ttu-id="22c1d-137">Copiar ficheiros</span><span class="sxs-lookup"><span data-stu-id="22c1d-137">Copy files</span></span>
<span data-ttu-id="22c1d-138">A partir da versão 0.9.7 do Azure PowerShell, pode copiar um ficheiro do ficheiro tooanother, um ficheiro tooa blob ou um ficheiro de tooa de blob.</span><span class="sxs-lookup"><span data-stu-id="22c1d-138">Beginning with version 0.9.7 of Azure PowerShell, you can copy a file tooanother file, a file tooa blob, or a blob tooa file.</span></span> <span data-ttu-id="22c1d-139">Abaixo, demonstramos como tooperform estes copiar operações utilizando os cmdlets do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="22c1d-139">Below we demonstrate how tooperform these copy operations using PowerShell cmdlets.</span></span>

```powershell
# copy a file toohello new directory
Start-AzureStorageFileCopy -SrcShareName srcshare -SrcFilePath srcdir/hello.txt -DestShareName destshare -DestFilePath destdir/hellocopy.txt -Context $srcCtx -DestContext $destCtx

# copy a blob tooa file directory
Start-AzureStorageFileCopy -SrcContainerName srcctn -SrcBlobName hello2.txt -DestShareName hello -DestFilePath hellodir/hello2copy.txt -DestContext $ctx -Context $ctx
```
## <a name="next-steps"></a><span data-ttu-id="22c1d-140">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="22c1d-140">Next steps</span></span>
<span data-ttu-id="22c1d-141">Consulte as ligações para obter mais informações sobre o Armazenamento de ficheiros do Azure.</span><span class="sxs-lookup"><span data-stu-id="22c1d-141">See these links for more information about Azure File storage.</span></span>

* [<span data-ttu-id="22c1d-142">FAQ</span><span class="sxs-lookup"><span data-stu-id="22c1d-142">FAQ</span></span>](../storage-files-faq.md)
* [<span data-ttu-id="22c1d-143">Resolução de Problemas no Windows</span><span class="sxs-lookup"><span data-stu-id="22c1d-143">Troubleshooting on Windows</span></span>](storage-troubleshoot-windows-file-connection-problems.md)      
* [<span data-ttu-id="22c1d-144">Resolução de Problemas no Linux</span><span class="sxs-lookup"><span data-stu-id="22c1d-144">Troubleshooting on Linux</span></span>](storage-troubleshoot-linux-file-connection-problems.md)    