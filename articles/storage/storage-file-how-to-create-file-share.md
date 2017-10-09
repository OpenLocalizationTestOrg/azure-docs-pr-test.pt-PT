---
title: aaaHow toocreate uma partilha de ficheiros do Azure | Microsoft Docs
description: "Como toocreate um Azure partilha de ficheiros no File storage do Azure utilizando Olá portal do Azure, PowerShell e Olá CLI do Azure."
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
ms.openlocfilehash: c4c59966b82d743fb4ecf79f48c0c8e61295d03d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-file-share-in-azure-file-storage"></a><span data-ttu-id="8033c-103">Criar uma Partilha de Ficheiros no armazenamento de Ficheiros do Azure</span><span class="sxs-lookup"><span data-stu-id="8033c-103">Create a File Share in Azure File storage</span></span>
<span data-ttu-id="8033c-104">Pode criar partilhas de ficheiros do Azure utilizando [portal do Azure](https://portal.azure.com/), Olá cmdlets do PowerShell de armazenamento do Azure, Olá bibliotecas de cliente do Storage do Azure ou Olá API de REST do Storage do Azure. Neste tutorial, irá aprender:</span><span class="sxs-lookup"><span data-stu-id="8033c-104">You can create Azure File shares using [Azure portal](https://portal.azure.com/), hello Azure Storage PowerShell cmdlets, hello Azure Storage client libraries, or hello Azure Storage REST API.In this tutorial, you will learn:</span></span>
* [<span data-ttu-id="8033c-105">Como toocreate um ficheiro de Azure partilhar utilizando Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="8033c-105">How toocreate an Azure File share using hello Azure portal</span></span>](#Create file share through hello Portal)
* [<span data-ttu-id="8033c-106">Como toocreate um Azure partilha de ficheiros com o Powershell</span><span class="sxs-lookup"><span data-stu-id="8033c-106">How toocreate an Azure File share using Powershell</span></span>](#Create file share using PowerShell)
* [<span data-ttu-id="8033c-107">Como toocreate um Azure partilha de ficheiros ao utilizar a CLI</span><span class="sxs-lookup"><span data-stu-id="8033c-107">How toocreate an Azure File share using CLI</span></span>](#create-file-share-using-command-line-interface-cli)

## <a name="prerequisites"></a><span data-ttu-id="8033c-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="8033c-108">Prerequisites</span></span>
<span data-ttu-id="8033c-109">toocreate uma partilha de ficheiros do Azure, pode utilizar uma conta de armazenamento que já exista, ou [criar uma nova conta de armazenamento do Azure](storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="8033c-109">toocreate an Azure File share, you can use a storage account that already exists, or [create a new Azure storage account](storage-create-storage-account.md).</span></span> <span data-ttu-id="8033c-110">toocreate uma partilha de ficheiros do Azure com o PowerShell, terá de chave de conta de Olá e o nome da conta de armazenamento...</span><span class="sxs-lookup"><span data-stu-id="8033c-110">toocreate an Azure File share with PowerShell, you will need hello account key and name of your storage account..</span></span> <span data-ttu-id="8033c-111">Precisa de chave de conta de armazenamento se planear toouse Powershell ou a CLI.</span><span class="sxs-lookup"><span data-stu-id="8033c-111">You will need Storage account key if you plan toouse Powershell or CLI.</span></span>

## <a name="create-file-share-through-hello-portal"></a><span data-ttu-id="8033c-112">Criar partilha de ficheiros através de Olá Portal</span><span class="sxs-lookup"><span data-stu-id="8033c-112">Create file share through hello Portal</span></span>
1. <span data-ttu-id="8033c-113">**Aceda tooStorage painel de conta no Portal do Azure**:</span><span class="sxs-lookup"><span data-stu-id="8033c-113">**Go tooStorage Account blade on Azure Portal**:</span></span>    
    <span data-ttu-id="8033c-114">![Painel da Conta de Armazenamento](media/storage-file-how-to-create-file-share/create-file-share-portal1.png)</span><span class="sxs-lookup"><span data-stu-id="8033c-114">![Storage Account Blade](media/storage-file-how-to-create-file-share/create-file-share-portal1.png)</span></span>

2. <span data-ttu-id="8033c-115">**Clique no botão Adicionar Partilha de Ficheiros**:</span><span class="sxs-lookup"><span data-stu-id="8033c-115">**Click on add File Share button**:</span></span>    
    <span data-ttu-id="8033c-116">![Clique em Olá adicionar botão de partilha de ficheiros](media/storage-file-how-to-create-file-share/create-file-share-portal2.png)</span><span class="sxs-lookup"><span data-stu-id="8033c-116">![Click hello add file share button](media/storage-file-how-to-create-file-share/create-file-share-portal2.png)</span></span>

3. <span data-ttu-id="8033c-117">**Indique o Nome e a Quota. Atualmente, a quota pode ter um máximo de 5 TB**:</span><span class="sxs-lookup"><span data-stu-id="8033c-117">**Provide Name and Quota. Quota currently can be maximum 5TB**:</span></span>    
    <span data-ttu-id="8033c-118">![Forneça um nome e uma quota pretendida para a nova partilha de ficheiros Olá](media/storage-file-how-to-create-file-share/create-file-share-portal3.png)</span><span class="sxs-lookup"><span data-stu-id="8033c-118">![Provide a name and a desired quota for hello new file share](media/storage-file-how-to-create-file-share/create-file-share-portal3.png)</span></span>

4. <span data-ttu-id="8033c-119">**Veja a partilha de ficheiros nova**: ![Veja a partilha de ficheiros nova](media/storage-file-how-to-create-file-share/create-file-share-portal4.png)</span><span class="sxs-lookup"><span data-stu-id="8033c-119">**View your new file share**:  ![View your new file share](media/storage-file-how-to-create-file-share/create-file-share-portal4.png)</span></span>

5. <span data-ttu-id="8033c-120">**Carregue um ficheiro**: ![Carregue um ficheiro](media/storage-file-how-to-create-file-share/create-file-share-portal5.png)</span><span class="sxs-lookup"><span data-stu-id="8033c-120">**Upload a file**:  ![Upload a file](media/storage-file-how-to-create-file-share/create-file-share-portal5.png)</span></span>

6. <span data-ttu-id="8033c-121">**Navegue para a partilha de ficheiros e faça a gestão dos seus diretórios e ficheiros**: ![Navegar para a partilha de ficheiros](media/storage-file-how-to-create-file-share/create-file-share-portal6.png)</span><span class="sxs-lookup"><span data-stu-id="8033c-121">**Browse into your file share and manage your directories and files**:  ![Browse file share](media/storage-file-how-to-create-file-share/create-file-share-portal6.png)</span></span>


## <a name="create-file-share-through-powershell"></a><span data-ttu-id="8033c-122">Criar a partilha de Ficheiros através do PowerShell</span><span class="sxs-lookup"><span data-stu-id="8033c-122">Create file share through PowerShell</span></span>
<span data-ttu-id="8033c-123">tooprepare toouse PowerShell, transfira e instale os cmdlets do PowerShell do Azure de Olá.</span><span class="sxs-lookup"><span data-stu-id="8033c-123">tooprepare toouse PowerShell, download and install hello Azure PowerShell cmdlets.</span></span> <span data-ttu-id="8033c-124">Consulte [como tooinstall e configurar o Azure PowerShell](https://azure.microsoft.com/documentation/articles/powershell-install-configure/) para Olá instalar instruções de instalação e do ponto.</span><span class="sxs-lookup"><span data-stu-id="8033c-124">See [How tooinstall and configure Azure PowerShell](https://azure.microsoft.com/documentation/articles/powershell-install-configure/) for hello install point and installation instructions.</span></span>

> [!Note]  
> <span data-ttu-id="8033c-125">Recomenda-se transferir e instalar ou atualizar o módulo Azure PowerShell mais recente do toohello.</span><span class="sxs-lookup"><span data-stu-id="8033c-125">It's recommended that you download and install or upgrade toohello latest Azure PowerShell module.</span></span>

1. <span data-ttu-id="8033c-126">**Criar um contexto para a conta de armazenamento e a chave** contexto Olá encapsula Olá chave conta do storage nome e a conta.</span><span class="sxs-lookup"><span data-stu-id="8033c-126">**Create a context for your storage account and key** hello context encapsulates hello storage account name and account key.</span></span> <span data-ttu-id="8033c-127">Para obter instruções sobre a cópia da chave de conta a partir do [portal do Azure](https://portal.azure.com/), veja [View and copy storage access keys (Ver e copiar chaves de acesso de armazenamento)](storage-create-storage-account.md#view-and-copy-storage-access-keys).</span><span class="sxs-lookup"><span data-stu-id="8033c-127">For instructions on copying your account key from the [Azure portal](https://portal.azure.com/), see [View and copy storage access keys](storage-create-storage-account.md#view-and-copy-storage-access-keys).</span></span>

    ```powershell
    $storageContext = New-AzureStorageContext <storage-account-name> <storage-account-key>
    ```
    
2. <span data-ttu-id="8033c-128">**Criar uma partilha de ficheiros nova**:</span><span class="sxs-lookup"><span data-stu-id="8033c-128">**Create a new file share**:</span></span>    
    
    ```powershell
    $share = New-AzureStorageShare logs -Context $storageContext
    ```

> [!Note]  
> <span data-ttu-id="8033c-129">Olá nome da partilha de ficheiros tem de ser todo em minúsculas.</span><span class="sxs-lookup"><span data-stu-id="8033c-129">hello name of your file share must be all lowercase.</span></span> <span data-ttu-id="8033c-130">Para obter detalhes completos sobre a nomenclatura de partilhas de ficheiros e ficheiros, veja [Naming and Referencing Shares, Directories, Files, and Metadata (Nomenclatura e Referência de Partilhas, Diretórios, Ficheiros e Metadados)](https://msdn.microsoft.com/library/azure/dn167011.aspx).</span><span class="sxs-lookup"><span data-stu-id="8033c-130">For complete details about naming file shares and files, see [Naming and Referencing Shares, Directories, Files, and Metadata](https://msdn.microsoft.com/library/azure/dn167011.aspx).</span></span>

## <a name="create-file-share-through-command-line-interface-cli"></a><span data-ttu-id="8033c-131">Criar a partilha de Ficheiros através da Interface de Linha de Comandos (CLI)</span><span class="sxs-lookup"><span data-stu-id="8033c-131">Create file share through Command Line Interface (CLI)</span></span>
1. <span data-ttu-id="8033c-132">**tooprepare toouse uma Interface de linha de comandos (CLI), transfira e instale Olá CLI do Azure.**</span><span class="sxs-lookup"><span data-stu-id="8033c-132">**tooprepare toouse a Command Line Interface (CLI), download and install hello Azure CLI.**</span></span>  
    <span data-ttu-id="8033c-133">Veja [Instalar a CLI 2.0 do Azure](/cli/azure/install-az-cli2.md) e [Introdução à CLI 2.0 do Azure](/cli/azure/get-started-with-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="8033c-133">See [Install Azure CLI 2.0](/cli/azure/install-az-cli2.md) and [Get started with Azure CLI 2.0](/cli/azure/get-started-with-azure-cli.md).</span></span>

2. <span data-ttu-id="8033c-134">**Crie uma ligação cadeia toohello armazenamento onde pretende que a partilha de Olá toocreate.**</span><span class="sxs-lookup"><span data-stu-id="8033c-134">**Create a connection string toohello storage account where you want toocreate hello share.**</span></span>  
    <span data-ttu-id="8033c-135">Substitua ```<storage-account>``` e ```<resource_group>``` com o grupo de recursos e nome de conta de armazenamento no seguinte exemplo de Olá.</span><span class="sxs-lookup"><span data-stu-id="8033c-135">Replace ```<storage-account>``` and ```<resource_group>``` with your storage account name and resource group in hello following example.</span></span>

   ```azurecli
    current_env_conn_string = $(az storage account show-connection-string -n <storage-account> -g <resource-group> --query 'connectionString' -o tsv)

    if [[ $current_env_conn_string == "" ]]; then  
        echo "Couldn't retrieve hello connection string."
    fi
    ```

3. <span data-ttu-id="8033c-136">**Criar partilha de ficheiros**</span><span class="sxs-lookup"><span data-stu-id="8033c-136">**Create file share**</span></span>
    ```azurecli
    az storage share create --name files --quota 2048 --connection-string $current_env_conn_string 1 > /dev/null
    ```

## <a name="next-steps"></a><span data-ttu-id="8033c-137">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="8033c-137">Next steps</span></span>
* <span data-ttu-id="8033c-138">[Connect and Mount File Share - Windows](storage-file-how-to-use-files-windows.md) (Ligar e Montar Partilha de Ficheiros - Windows)</span><span class="sxs-lookup"><span data-stu-id="8033c-138">[Connect and Mount File Share - Windows](storage-file-how-to-use-files-windows.md)</span></span>
* <span data-ttu-id="8033c-139">[Connect and Mount File Share - Linux](storage-how-to-use-files-linux.md) (Ligar e Montar Partilha de Ficheiros - Linux)</span><span class="sxs-lookup"><span data-stu-id="8033c-139">[Connect and Mount File Share - Linux](storage-how-to-use-files-linux.md)</span></span>
* <span data-ttu-id="8033c-140">[Connect and Mount File Share - macOS](storage-file-how-to-use-files-mac.md) (Ligar e Montar Partilha de Ficheiros - macOS)</span><span class="sxs-lookup"><span data-stu-id="8033c-140">[Connect and Mount File Share - macOS](storage-file-how-to-use-files-mac.md)</span></span>

<span data-ttu-id="8033c-141">Consulte as ligações para obter mais informações sobre o Armazenamento de ficheiros do Azure.</span><span class="sxs-lookup"><span data-stu-id="8033c-141">See these links for more information about Azure File storage.</span></span>

* [<span data-ttu-id="8033c-142">FAQ</span><span class="sxs-lookup"><span data-stu-id="8033c-142">FAQ</span></span>](storage-files-faq.md)
* [<span data-ttu-id="8033c-143">Resolução de problemas</span><span class="sxs-lookup"><span data-stu-id="8033c-143">Troubleshooting</span></span>](storage-troubleshoot-file-connection-problems.md)