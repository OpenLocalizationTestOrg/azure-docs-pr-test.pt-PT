---
title: "partilha de ficheiros do Azure aaaMount através de SMB com macOS | Microsoft Docs"
description: "Saiba como partilhar toomount um ficheiro do Azure através de SMB com macOS."
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
ms.openlocfilehash: 71aaec8a77b770fe147b783c0ab9f86830176bec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="mount-azure-file-share-over-smb-with-macos"></a><span data-ttu-id="a0a6b-103">Montar uma partilha de Ficheiros do Azure através de SMB com macOS</span><span class="sxs-lookup"><span data-stu-id="a0a6b-103">Mount Azure File share over SMB with macOS</span></span>
<span data-ttu-id="a0a6b-104">[File storage do Azure](../storage-dotnet-how-to-use-files.md) é serviço da Microsoft que lhe permite toocreate e utilizar partilhas de ficheiros de rede no Olá do Azure utilizando o padrão da indústria de Olá.</span><span class="sxs-lookup"><span data-stu-id="a0a6b-104">[Azure File storage](../storage-dotnet-how-to-use-files.md) is Microsoft's service that enables you toocreate and use network file shares in hello Azure using hello industry standard.</span></span> <span data-ttu-id="a0a6b-105">As partilhas de Ficheiros do Azure podem ser montadas no macOS Sierra (10.12) e El Capitan (10.11).</span><span class="sxs-lookup"><span data-stu-id="a0a6b-105">Azure File shares can be mounted in macOS Sierra (10.12) and El Capitan (10.11).</span></span> <span data-ttu-id="a0a6b-106">Este artigo mostra duas formas diferentes toomount uma partilha de ficheiros do Azure no macOS com Olá LCA IU e utilizando Olá Terminal.</span><span class="sxs-lookup"><span data-stu-id="a0a6b-106">This article shows two different ways toomount an Azure File share on macOS with hello Finder UI and using hello Terminal.</span></span>

> [!Note]  
> <span data-ttu-id="a0a6b-107">Antes de montar uma partilha de Ficheiros do Azure através de SMB, recomendamos desativar a assinatura de pacotes SMB.</span><span class="sxs-lookup"><span data-stu-id="a0a6b-107">Before mounting an Azure File share over SMB, we recommend disabling SMB packet signing.</span></span> <span data-ttu-id="a0a6b-108">Não se o fizer, poderá produzir fraco desempenho quando aceder à partilha de ficheiros do Azure Olá partir macOS.</span><span class="sxs-lookup"><span data-stu-id="a0a6b-108">Not doing so may yield poor performance when accessing hello Azure File share from macOS.</span></span> <span data-ttu-id="a0a6b-109">A ligação de SMB será encriptada, pelo que isto não afeta a segurança de Olá da sua ligação.</span><span class="sxs-lookup"><span data-stu-id="a0a6b-109">Your SMB connection will be encrypted, so this does not affect hello security of your connection.</span></span> <span data-ttu-id="a0a6b-110">De Olá terminal, Olá comandos seguintes irão desativar a assinatura do pacote SMB, conforme descrito por este [artigo de suporte da Apple no desativar a assinatura do pacote SMB](https://support.apple.com/HT205926):</span><span class="sxs-lookup"><span data-stu-id="a0a6b-110">From hello terminal, hello following commands will disable SMB packet signing, as described by this [Apple support article on disabling SMB packet signing](https://support.apple.com/HT205926):</span></span>  
>    ```
>    sudo -s
>    echo "[default]" >> /etc/nsmb.conf
>    echo "signing_required=no" >> /etc/nsmb.conf
>    exit
>    ```

## <a name="prerequisites-for-mounting-an-azure-file-share-on-macos"></a><span data-ttu-id="a0a6b-111">Pré-requisitos para montar uma partilha de Ficheiros do Azure em macOS</span><span class="sxs-lookup"><span data-stu-id="a0a6b-111">Prerequisites for mounting an Azure File share on macOS</span></span>
* <span data-ttu-id="a0a6b-112">**Nome da conta de armazenamento**: toomount partilha de um ficheiro do Azure, será necessário Olá nome Olá da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="a0a6b-112">**Storage account name**: toomount an Azure File share, you will need hello name of hello storage account.</span></span>

* <span data-ttu-id="a0a6b-113">**Chave de conta de armazenamento**: a partilha de um ficheiro de Azure toomount, será necessário Olá chave de armazenamento () principais ou secundários.</span><span class="sxs-lookup"><span data-stu-id="a0a6b-113">**Storage account key**: toomount an Azure File share, you will need hello primary (or secondary) storage key.</span></span> <span data-ttu-id="a0a6b-114">Atualmente, não são suportadas chaves SAS para a montagem.</span><span class="sxs-lookup"><span data-stu-id="a0a6b-114">SAS keys are not currently supported for mounting.</span></span>

* <span data-ttu-id="a0a6b-115">**Confirme que a porta 445 está aberta**: o SMB comunica através da porta TCP 445.</span><span class="sxs-lookup"><span data-stu-id="a0a6b-115">**Ensure port 445 is open**: SMB communicates over TCP port 445.</span></span> <span data-ttu-id="a0a6b-116">No computador de cliente (Olá Mac), verifique se que a firewall não está a bloquear a porta TCP 445 toomake.</span><span class="sxs-lookup"><span data-stu-id="a0a6b-116">On your client machine (hello Mac), check toomake sure your firewall is not blocking TCP port 445.</span></span>

## <a name="mount-an-azure-file-share-via-finder"></a><span data-ttu-id="a0a6b-117">Montar uma partilha de Ficheiros do Azure através do Finder</span><span class="sxs-lookup"><span data-stu-id="a0a6b-117">Mount an Azure File share via Finder</span></span>
1. <span data-ttu-id="a0a6b-118">**Abrir LCA**: LCA está aberta no macOS por predefinição, mas pode garantir é Olá selecionado atualmente no Olá ancoragem aplicação clicando Olá "o macOS enfrentam ícone":</span><span class="sxs-lookup"><span data-stu-id="a0a6b-118">**Open Finder**: Finder is open on macOS by default, but you can ensure it is hello currently selected application by clicking hello "macOS face icon" on hello dock:</span></span>  
    <span data-ttu-id="a0a6b-119">![Olá macOS enfrentam ícone](./media/storage-how-to-use-files-mac/mount-via-finder-1.png)</span><span class="sxs-lookup"><span data-stu-id="a0a6b-119">![hello macOS face icon](./media/storage-how-to-use-files-mac/mount-via-finder-1.png)</span></span>

2. <span data-ttu-id="a0a6b-120">**Selecione "Ligar tooServer" Olá "Ir" Menu**: utilizando o caminho UNC Olá de Olá [pré-requisitos](#preq), converter barra invertida duplo do Olá início (`\\`) demasiado`smb://` e todos os outras barras invertidas (`\`) barras tooforwards (`/`).</span><span class="sxs-lookup"><span data-stu-id="a0a6b-120">**Select "Connect tooServer" from hello "Go" Menu**: Using hello UNC path from hello [prerequisites](#preq), convert hello beginning double backslash (`\\`) too`smb://` and all other backslashes (`\`) tooforwards slashes (`/`).</span></span> <span data-ttu-id="a0a6b-121">A ligação deverá ter um aspeto semelhante Olá: ![caixa de diálogo de "Ligar tooServer" Olá](./media/storage-how-to-use-files-mac/mount-via-finder-2.png)</span><span class="sxs-lookup"><span data-stu-id="a0a6b-121">Your link should look like hello following: ![hello "Connect tooServer" dialog](./media/storage-how-to-use-files-mac/mount-via-finder-2.png)</span></span>

3. <span data-ttu-id="a0a6b-122">**Utilize Olá partilha de armazenamento e de nome de chave de conta quando lhe for pedido um nome de utilizador e palavra-passe**: quando clicar em "Ligar" da caixa de diálogo de "Ligar tooServer" Olá, será solicitado para Olá nome de utilizador e palavra-passe (tal será autopopulated com seu macOS nome de utilizador).</span><span class="sxs-lookup"><span data-stu-id="a0a6b-122">**Use hello share name and storage account key when prompted for a username and password**: When you click "Connect" on hello "Connect tooServer" dialog, you will be prompted for hello username and password (This will be autopopulated with your macOS username).</span></span> <span data-ttu-id="a0a6b-123">Tem a opção Olá de colocar a chave de conta de armazenamento/nome de partilha de Olá no seu macOS Keychain.</span><span class="sxs-lookup"><span data-stu-id="a0a6b-123">You have hello option of placing hello share name/storage account key in your macOS Keychain.</span></span>

4. <span data-ttu-id="a0a6b-124">**Partilha de ficheiros do Azure Olá utilização conforme o desejado**: após substituindo Olá partilha de armazenamento e o nome da chave de conta no Olá nome de utilizador e palavra-passe, será possível montar a partilha de Olá.</span><span class="sxs-lookup"><span data-stu-id="a0a6b-124">**Use hello Azure File share as desired**: After substituting hello share name and storage account key in for hello username and password, hello share will be mounted.</span></span> <span data-ttu-id="a0a6b-125">Pode utilizar este que normalmente utilizaria uma partilha de pasta/ficheiro local, incluindo, arrastar e largar os ficheiros numa partilha de ficheiros de Olá:</span><span class="sxs-lookup"><span data-stu-id="a0a6b-125">You may use this as you would normally use a local folder/file share, including dragging and dropping files into hello file share:</span></span>

    ![Instantâneo de uma partilha de Ficheiros do Azure montada](./media/storage-how-to-use-files-mac/mount-via-finder-3.png)

## <a name="mount-an-azure-file-share-via-terminal"></a><span data-ttu-id="a0a6b-127">Montar uma partilha de Ficheiros do Azure através do Terminal</span><span class="sxs-lookup"><span data-stu-id="a0a6b-127">Mount an Azure File share via Terminal</span></span>
1. <span data-ttu-id="a0a6b-128">Substitua `<storage-account-name>` com o nome de Olá da sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="a0a6b-128">Replace `<storage-account-name>` with hello name of your storage account.</span></span> <span data-ttu-id="a0a6b-129">Indique a Chave da Conta de Armazenamento como a palavra-passe, quando lhe for pedido.</span><span class="sxs-lookup"><span data-stu-id="a0a6b-129">Provide Storage Account Key as password when prompted.</span></span> 

    ```
    mount_smbfs //<storage-account-name>@<storage-account-name>.file.core.windows.net/<share-name> <desired-mount-point>
    ```

2. <span data-ttu-id="a0a6b-130">**Partilha de ficheiros do Azure Olá utilização conforme o desejado**: partilha de ficheiros do Azure Olá será montada no ponto de montagem Olá especificado pelo comando anterior Olá.</span><span class="sxs-lookup"><span data-stu-id="a0a6b-130">**Use hello Azure File share as desired**: hello Azure File share will be mounted at hello mount point specified by hello previous command.</span></span>  

    ![Um instantâneo de Olá montar a partilha de ficheiros do Azure](./media/storage-how-to-use-files-mac/mount-via-terminal-1.png)

## <a name="next-steps"></a><span data-ttu-id="a0a6b-132">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="a0a6b-132">Next steps</span></span>
<span data-ttu-id="a0a6b-133">Consulte as ligações para obter mais informações sobre o Armazenamento de ficheiros do Azure.</span><span class="sxs-lookup"><span data-stu-id="a0a6b-133">See these links for more information about Azure File storage.</span></span>

* [<span data-ttu-id="a0a6b-134">Artigo de suporte de Apple - como tooconnect com partilha de ficheiros no Mac</span><span class="sxs-lookup"><span data-stu-id="a0a6b-134">Apple Support Article - How tooconnect with File Sharing on your Mac</span></span>](https://support.apple.com/HT204445)
* [<span data-ttu-id="a0a6b-135">FAQ</span><span class="sxs-lookup"><span data-stu-id="a0a6b-135">FAQ</span></span>](../storage-files-faq.md)
* [<span data-ttu-id="a0a6b-136">Resolução de Problemas no Windows</span><span class="sxs-lookup"><span data-stu-id="a0a6b-136">Troubleshooting on Windows</span></span>](storage-troubleshoot-windows-file-connection-problems.md)      
* [<span data-ttu-id="a0a6b-137">Resolução de Problemas no Linux</span><span class="sxs-lookup"><span data-stu-id="a0a6b-137">Troubleshooting on Linux</span></span>](storage-troubleshoot-linux-file-connection-problems.md)    