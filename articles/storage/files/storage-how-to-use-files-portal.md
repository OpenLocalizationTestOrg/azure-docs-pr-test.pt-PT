---
title: "aaaHow toomanage File storage do Azure de Olá portal do Azure | Microsoft Docs"
description: "Saiba toouse Olá toomanage portal do Azure File storage do Azure."
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
ms.openlocfilehash: 6ad2fbbf9ee2f86748b1b175d0f63274144dc5eb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-file-storage-from-hello-azure-portal"></a><span data-ttu-id="8e908-103">Como toouse File storage do Azure de Olá Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="8e908-103">How toouse Azure File storage from hello Azure Portal</span></span>
<span data-ttu-id="8e908-104">Olá [portal do Azure](https://portal.azure.com) fornece uma interface de utilizador para gerir o File storage do Azure.</span><span class="sxs-lookup"><span data-stu-id="8e908-104">hello [Azure portal](https://portal.azure.com) provides a user interface for managing Azure File storage.</span></span> <span data-ttu-id="8e908-105">Pode efetuar Olá seguintes ações a partir do seu browser web:</span><span class="sxs-lookup"><span data-stu-id="8e908-105">You can perform hello following actions from your web browser:</span></span>

* <span data-ttu-id="8e908-106">Criar Partilhas de Ficheiros</span><span class="sxs-lookup"><span data-stu-id="8e908-106">Create a File Share</span></span>
* <span data-ttu-id="8e908-107">Carregar e transferir ficheiros tooand da partilha de ficheiros.</span><span class="sxs-lookup"><span data-stu-id="8e908-107">Upload and download files tooand from your file share.</span></span>
* <span data-ttu-id="8e908-108">Monitorizar a utilização real do Olá de cada partilha de ficheiros.</span><span class="sxs-lookup"><span data-stu-id="8e908-108">Monitor hello actual usage of each file share.</span></span>
* <span data-ttu-id="8e908-109">Ajuste a quota de tamanho da partilha de ficheiros de Olá.</span><span class="sxs-lookup"><span data-stu-id="8e908-109">Adjust hello file share size quota.</span></span>
* <span data-ttu-id="8e908-110">Copie Olá montagem comandos toouse toomount partilhar o ficheiro de um cliente Windows ou Linux.</span><span class="sxs-lookup"><span data-stu-id="8e908-110">Copy hello mount commands toouse toomount your file share from a Windows or Linux client.</span></span>

## <a name="create-file-share"></a><span data-ttu-id="8e908-111">Criar a partilha de ficheiros</span><span class="sxs-lookup"><span data-stu-id="8e908-111">Create file share</span></span>
1. <span data-ttu-id="8e908-112">Inicie sessão no toohello portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="8e908-112">Sign in toohello Azure portal.</span></span>
2. <span data-ttu-id="8e908-113">No menu de navegação de Olá, clique em **contas do Storage** ou **contas do Storage (clássica)**.</span><span class="sxs-lookup"><span data-stu-id="8e908-113">On hello navigation menu, click **Storage accounts** or **Storage accounts (classic)**.</span></span>
    
    ![Captura de ecrã que mostra como de partilha de ficheiros de toocreate no portal de Olá](./media/storage-how-to-use-files-portal/use-files-portal-create-file-share1.png)

3. <span data-ttu-id="8e908-115">Escolha a sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="8e908-115">Choose your storage account.</span></span>

    ![Captura de ecrã que mostra como de partilha de ficheiros de toocreate no portal de Olá](./media/storage-how-to-use-files-portal/use-files-portal-create-file-share2.png)

4. <span data-ttu-id="8e908-117">Escolha o serviço “Ficheiros”.</span><span class="sxs-lookup"><span data-stu-id="8e908-117">Choose "Files" service.</span></span>

    ![Captura de ecrã que mostra como de partilha de ficheiros de toocreate no portal de Olá](./media/storage-how-to-use-files-portal/use-files-portal-create-file-share3.png)

5. <span data-ttu-id="8e908-119">Clique em "Partilhas de ficheiros" e seguir Olá ligação toocreate partilhar o seu primeiro ficheiro.</span><span class="sxs-lookup"><span data-stu-id="8e908-119">Click "File shares" and follow hello link toocreate your first file share.</span></span>

    ![Captura de ecrã que mostra como de partilha de ficheiros de toocreate no portal de Olá](./media/storage-how-to-use-files-portal/use-files-portal-create-file-share4.png)

6. <span data-ttu-id="8e908-121">Preencha nome Olá da partilha de ficheiros e o tamanho de Olá de Olá ficheiro partilha (cópia de segurança too5120 GB) toocreate sua primeira partilha de ficheiros.</span><span class="sxs-lookup"><span data-stu-id="8e908-121">Fill in hello file share name and hello size of hello file share (up too5120 GB) toocreate your first file share.</span></span> <span data-ttu-id="8e908-122">Quando tiver sido criada a partilha de ficheiros de Olá, possível montá-la a partir de qualquer sistema de ficheiros que suporta SMB 2.1 ou SMB 3.0.</span><span class="sxs-lookup"><span data-stu-id="8e908-122">Once hello file share has been created, you can mount it from any file system that supports SMB 2.1 or SMB 3.0.</span></span> <span data-ttu-id="8e908-123">Pode clicar em **Quota** no Olá ficheiro partilha toochange Olá tamanho Olá do ficheiro de cópia de segurança too5120 GB.</span><span class="sxs-lookup"><span data-stu-id="8e908-123">You could click on **Quota** on hello file share toochange hello size of hello file up too5120 GB.</span></span> <span data-ttu-id="8e908-124">Consulte demasiado[Calculadora de preços do Azure](https://azure.microsoft.com/pricing/calculator/) custo do armazenamento Olá tooestimate da utilização do File storage do Azure.</span><span class="sxs-lookup"><span data-stu-id="8e908-124">Please refer too[Azure Pricing Calculator](https://azure.microsoft.com/pricing/calculator/) tooestimate hello storage cost of using Azure File storage.</span></span>

    ![Captura de ecrã que mostra como de partilha de ficheiros de toocreate no portal de Olá](./media/storage-how-to-use-files-portal/use-files-portal-create-file-share5.png)

## <a name="upload-and-download-files"></a><span data-ttu-id="8e908-126">Carregar e transferir os ficheiros</span><span class="sxs-lookup"><span data-stu-id="8e908-126">Upload and download files</span></span>
1. <span data-ttu-id="8e908-127">Escolha uma partilha de ficheiros que já criou.</span><span class="sxs-lookup"><span data-stu-id="8e908-127">Choose one file share your have already created.</span></span>

    ![Captura de ecrã que mostra como ficheiros tooupload e transferências de Olá portal](./media/storage-how-to-use-files-portal/use-files-portal-upload-file1.png)

2. <span data-ttu-id="8e908-129">Clique em **carregar** para abrir a interface de utilizador de Olá para carregamento de ficheiros.</span><span class="sxs-lookup"><span data-stu-id="8e908-129">Click **Upload** to open hello user interface for files uploading.</span></span>

    ![Captura de ecrã que mostra como tooupload ficheiros a partir do portal de Olá](./media/storage-how-to-use-files-portal/use-files-portal-upload-file2.png)

## <a name="connect-toofile-share"></a><span data-ttu-id="8e908-131">Ligar toofile partilha</span><span class="sxs-lookup"><span data-stu-id="8e908-131">Connect toofile share</span></span>
-  <span data-ttu-id="8e908-132">Clique em **Connect** obter Olá linha de comandos para partilha de ficheiros de Olá a montagem do Windows e Linux.</span><span class="sxs-lookup"><span data-stu-id="8e908-132">Click **Connect** to get hello command line for mounting hello file share from Windows and Linux.</span></span> <span data-ttu-id="8e908-133">Para os utilizadores do Linux, pode também consultar demasiado[como toouse File storage do Azure com o Linux](../storage-how-to-use-files-linux.md) para obter mais instruções de montagem para outras as distribuições do Linux.</span><span class="sxs-lookup"><span data-stu-id="8e908-133">For Linux users, you can also refer too[How toouse Azure File storage with Linux](../storage-how-to-use-files-linux.md) for more mounting instructions for other Linux distributions.</span></span>

    ![Captura de ecrã que mostra como toomount Olá partilha de ficheiros](./media/storage-how-to-use-files-portal/use-files-portal-connect.png)
-  <span data-ttu-id="8e908-135">Pode copiar Olá comandos para montar ficheiros partilham no Windows ou Linux e execução-lo da máquina de VM do Azure ou no local.</span><span class="sxs-lookup"><span data-stu-id="8e908-135">You can copy hello commands for mounting file share on Windows or Linux and run it from you Azure VM or on-premises machine.</span></span>

    ![Captura de ecrã que mostra os comandos de montagem de Olá para o Windows e Linux](./media/storage-how-to-use-files-portal/use-files-portal-show-mount-commands.png)

<span data-ttu-id="8e908-137">**Sugestão:**</span><span class="sxs-lookup"><span data-stu-id="8e908-137">**Tip:**</span></span>  
<span data-ttu-id="8e908-138">toofind chave de acesso da conta de armazenamento de Olá de montagem, clique em **visualizar chaves de acesso para esta conta de armazenamento** na parte inferior de Olá de Olá ligar página.</span><span class="sxs-lookup"><span data-stu-id="8e908-138">toofind hello storage account access key for mounting, click on **View access keys for this storage account** at hello bottom of hello connect page.</span></span>

## <a name="see-also"></a><span data-ttu-id="8e908-139">Consultar também</span><span class="sxs-lookup"><span data-stu-id="8e908-139">See also</span></span>
<span data-ttu-id="8e908-140">Consulte as ligações para obter mais informações sobre o Armazenamento de ficheiros do Azure.</span><span class="sxs-lookup"><span data-stu-id="8e908-140">See these links for more information about Azure File storage.</span></span>

* [<span data-ttu-id="8e908-141">FAQ</span><span class="sxs-lookup"><span data-stu-id="8e908-141">FAQ</span></span>](../storage-files-faq.md)
* [<span data-ttu-id="8e908-142">Resolução de Problemas no Windows</span><span class="sxs-lookup"><span data-stu-id="8e908-142">Troubleshooting on Windows</span></span>](storage-troubleshoot-windows-file-connection-problems.md)      
* [<span data-ttu-id="8e908-143">Resolução de Problemas no Linux</span><span class="sxs-lookup"><span data-stu-id="8e908-143">Troubleshooting on Linux</span></span>](storage-troubleshoot-linux-file-connection-problems.md)    