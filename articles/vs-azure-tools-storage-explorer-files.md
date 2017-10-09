---
title: "aaaUsing Explorador de armazenamento (pré-visualização) com o File storage do Azure | Microsoft Docs"
description: "Saiba como saber como toouse Explorador de armazenamento (pré-visualização) toowork com o ficheiro de partilhas e os ficheiros."
services: storage
documentationcenter: na
author: cawaMS
manager: paulyuk
editor: 
ms.assetid: 
ms.service: storage
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/09/2017
ms.author: cawa
ms.openlocfilehash: 98eb3cde711ae3dbfdb6ffaec23ae24f822370e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="using-storage-explorer-preview-with-azure-file-storage"></a><span data-ttu-id="0f172-103">Utilizar o Explorador de Armazenamento (Pré-visualização) com o Armazenamento de ficheiros do Azure</span><span class="sxs-lookup"><span data-stu-id="0f172-103">Using Storage Explorer (Preview) with Azure File storage</span></span>

<span data-ttu-id="0f172-104">Ficheiros do Azure storage é um serviço que oferece ficheiro partilhas na utilização de nuvem Olá Olá protocolo Server Message Block (SMB) padrão.</span><span class="sxs-lookup"><span data-stu-id="0f172-104">Azure File storage is a service that offers file shares in hello cloud using hello standard Server Message Block (SMB) Protocol.</span></span> <span data-ttu-id="0f172-105">O SMB 2.1 e o SMB 3.0 são suportados.</span><span class="sxs-lookup"><span data-stu-id="0f172-105">Both SMB 2.1 and SMB 3.0 are supported.</span></span> <span data-ttu-id="0f172-106">Com o File storage do Azure, é possível migrar aplicações antigas que se baseiam em tooAzure de partilhas de ficheiros rapidamente e sem reescritas dispendiosas.</span><span class="sxs-lookup"><span data-stu-id="0f172-106">With Azure File storage, you can migrate legacy applications that rely on file shares tooAzure quickly and without costly rewrites.</span></span> <span data-ttu-id="0f172-107">Pode utilizar os dados de ficheiros armazenamento tooexpose publicamente toohello mundo ou toostore dados da aplicação em privado.</span><span class="sxs-lookup"><span data-stu-id="0f172-107">You can use File storage tooexpose data publicly toohello world, or toostore application data privately.</span></span> <span data-ttu-id="0f172-108">Neste artigo, irá aprender como toouse Explorador de armazenamento (pré-visualização) toowork com o ficheiro de partilhas e os ficheiros.</span><span class="sxs-lookup"><span data-stu-id="0f172-108">In this article, you'll learn how toouse Storage Explorer (Preview) toowork with file shares and files.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0f172-109">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="0f172-109">Prerequisites</span></span>

<span data-ttu-id="0f172-110">toocomplete Olá passos descritos neste artigo, irá precisar seguinte Olá:</span><span class="sxs-lookup"><span data-stu-id="0f172-110">toocomplete hello steps in this article, you'll need hello following:</span></span>

- [<span data-ttu-id="0f172-111">Transfira e instale o Explorador de Armazenamento (pré-visualização)</span><span class="sxs-lookup"><span data-stu-id="0f172-111">Download and install Storage Explorer (preview)</span></span>](http://www.storageexplorer.com/)

- [<span data-ttu-id="0f172-112">Ligar a conta de armazenamento do Azure tooa ou serviço</span><span class="sxs-lookup"><span data-stu-id="0f172-112">Connect tooa Azure storage account or service</span></span>](https://docs.microsoft.com//azure/vs-azure-tools-storage-manage-with-storage-explorer#connect-to-a-storage-account-or-service)

## <a name="create-a-file-share"></a><span data-ttu-id="0f172-113">Criar Partilhas de Ficheiros</span><span class="sxs-lookup"><span data-stu-id="0f172-113">Create a File Share</span></span>

<span data-ttu-id="0f172-114">Todos os ficheiros têm de residir numa partilha de ficheiros, que é simplesmente um agrupamento lógico de ficheiros.</span><span class="sxs-lookup"><span data-stu-id="0f172-114">All files must reside in a file share, which is simply a logical grouping of files.</span></span> <span data-ttu-id="0f172-115">Uma conta pode conter um número ilimitado de partilhas de ficheiros e cada partilha pode armazenar um número ilimitado de ficheiros.</span><span class="sxs-lookup"><span data-stu-id="0f172-115">An account can contain an unlimited number of file shares, and each share can store an unlimited number of files.</span></span>

<span data-ttu-id="0f172-116">Olá, os passos seguintes mostram como toocreate um partilha de ficheiros no Explorador de armazenamento (pré-visualização).</span><span class="sxs-lookup"><span data-stu-id="0f172-116">hello following steps illustrate how toocreate a file share within Storage Explorer (Preview).</span></span>

1. <span data-ttu-id="0f172-117">Abrir o Explorador de Armazenamento (Pré-visualização).</span><span class="sxs-lookup"><span data-stu-id="0f172-117">Open Storage Explorer (Preview).</span></span>

2. <span data-ttu-id="0f172-118">No painel esquerdo Olá, expanda a conta de armazenamento de Olá no qual pretende toocreate Olá partilha de ficheiros</span><span class="sxs-lookup"><span data-stu-id="0f172-118">In hello left pane, expand hello storage account within which you wish toocreate hello File Share</span></span>

3. <span data-ttu-id="0f172-119">Clique com botão direito **partilhas de ficheiros**e, no menu de contexto de Olá - selecione **criar partilha de ficheiros**.</span><span class="sxs-lookup"><span data-stu-id="0f172-119">Right-click **File Shares**, and - from hello context menu - select **Create File Share**.</span></span>

    ![Criar a Partilha de Ficheiros](media/vs-azure-tools-storage-explorer-files/image1.png)

4. <span data-ttu-id="0f172-121">Será apresentada uma caixa de texto abaixo Olá **partilhas de ficheiros** pasta.</span><span class="sxs-lookup"><span data-stu-id="0f172-121">A text box will appear below hello **File Shares** folder.</span></span> <span data-ttu-id="0f172-122">Introduza o nome de Olá para a partilha de ficheiros.</span><span class="sxs-lookup"><span data-stu-id="0f172-122">Enter hello name for your file share.</span></span> <span data-ttu-id="0f172-123">Consulte Olá [partilhar regras de nomenclatura](https://docs.microsoft.com//azure/storage/storage-dotnet-how-to-use-blobs#create-a-container) secção para obter uma lista de restrições em partilhas de ficheiros de atribuição de nomes e regras.</span><span class="sxs-lookup"><span data-stu-id="0f172-123">See hello [Share naming rules](https://docs.microsoft.com//azure/storage/storage-dotnet-how-to-use-blobs#create-a-container) section for a list of rules and restrictions on naming file shares.</span></span>

    ![Atribuição de nome de partilha de Olá](media/vs-azure-tools-storage-explorer-files/image2.png)

5. <span data-ttu-id="0f172-125">Prima **Enter** quando toocreate efectuada Olá partilha de ficheiros, ou **Esc** toocancel.</span><span class="sxs-lookup"><span data-stu-id="0f172-125">Press **Enter** when done toocreate hello file share, or **Esc** toocancel.</span></span> <span data-ttu-id="0f172-126">Assim que a partilha de ficheiros de Olá foi criada com êxito, será apresentado em Olá **partilhas de ficheiros** pasta para Olá selecionado a conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="0f172-126">Once hello file share has been successfully created, it will be displayed under hello **File Shares** folder for hello selected storage account.</span></span>

    ![nova partilha de Olá](media/vs-azure-tools-storage-explorer-files/image3.png)

## <a name="view-a-file-shares-contents"></a><span data-ttu-id="0f172-128">Ver os conteúdos de uma partilha de ficheiros</span><span class="sxs-lookup"><span data-stu-id="0f172-128">View a file share's contents</span></span>

<span data-ttu-id="0f172-129">As partilhas de ficheiros contêm ficheiros e pastas (que também podem conter ficheiros).</span><span class="sxs-lookup"><span data-stu-id="0f172-129">File shares contain files and folders (that can also contain files).</span></span>

<span data-ttu-id="0f172-130">Olá passos seguintes mostram como partilha de conteúdo de Olá tooview de um ficheiro no Explorador de armazenamento (pré-visualização): +</span><span class="sxs-lookup"><span data-stu-id="0f172-130">hello following steps illustrate how tooview hello contents of a file share within Storage Explorer (Preview):+</span></span>

1. <span data-ttu-id="0f172-131">Abrir o Explorador de Armazenamento (Pré-visualização).</span><span class="sxs-lookup"><span data-stu-id="0f172-131">Open Storage Explorer (Preview).</span></span>

2. <span data-ttu-id="0f172-132">No painel esquerdo Olá, expanda a conta de armazenamento de Olá com partilha de ficheiros de Olá desejar tooview.</span><span class="sxs-lookup"><span data-stu-id="0f172-132">In hello left pane, expand hello storage account containing hello file share you wish tooview.</span></span>

3. <span data-ttu-id="0f172-133">Expanda a conta de armazenamento a Olá **partilhas de ficheiros**.</span><span class="sxs-lookup"><span data-stu-id="0f172-133">Expand hello storage account's **File Shares**.</span></span>

4. <span data-ttu-id="0f172-134">Partilha de ficheiros do contexto Olá que queira tooview e, no menu de contexto de Olá - selecione **abra**.</span><span class="sxs-lookup"><span data-stu-id="0f172-134">Right-click hello file share you wish tooview, and - from hello context menu - select **Open**.</span></span> <span data-ttu-id="0f172-135">Também pode fazer duplo clique partilha de ficheiros de Olá desejar tooview.</span><span class="sxs-lookup"><span data-stu-id="0f172-135">You can also double-click hello file share you wish tooview.</span></span>

    ![Abrir a partilha](media/vs-azure-tools-storage-explorer-files/image4.png)

5. <span data-ttu-id="0f172-137">painel principal Olá apresentará o conteúdo da partilha de ficheiros Olá.</span><span class="sxs-lookup"><span data-stu-id="0f172-137">hello main pane will display hello file share's contents.</span></span>
    
    ![Olá conteúdos da partilha](media/vs-azure-tools-storage-explorer-files/image5.png)

## <a name="delete-a-file-share"></a><span data-ttu-id="0f172-139">Eliminar partilhas de ficheiros</span><span class="sxs-lookup"><span data-stu-id="0f172-139">Delete a file share</span></span>

<span data-ttu-id="0f172-140">É fácil criar e eliminar partilhas de ficheiros, conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="0f172-140">File shares can be easily created and deleted as needed.</span></span> <span data-ttu-id="0f172-141">(toosee como ficheiros individuais toodelete, consulte a secção de toohello, [gerir ficheiros numa partilha de ficheiros](https://docs.microsoft.com//azure/vs-azure-tools-storage-explorer-blobs#managing-blobs-in-a-blob-container).)</span><span class="sxs-lookup"><span data-stu-id="0f172-141">(toosee how toodelete individual files, refer toohello section, [Managing files in a file share](https://docs.microsoft.com//azure/vs-azure-tools-storage-explorer-blobs#managing-blobs-in-a-blob-container).)</span></span>

<span data-ttu-id="0f172-142">Olá, os passos seguintes ilustram como toodelete um partilha de ficheiros no Explorador de armazenamento (pré-visualização):</span><span class="sxs-lookup"><span data-stu-id="0f172-142">hello following steps illustrate how toodelete a file share within Storage Explorer (Preview):</span></span>

1. <span data-ttu-id="0f172-143">Abrir o Explorador de Armazenamento (Pré-visualização).</span><span class="sxs-lookup"><span data-stu-id="0f172-143">Open Storage Explorer (Preview).</span></span>

2. <span data-ttu-id="0f172-144">No painel esquerdo Olá, expanda a conta de armazenamento de Olá com partilha de ficheiros de Olá desejar tooview.</span><span class="sxs-lookup"><span data-stu-id="0f172-144">In hello left pane, expand hello storage account containing hello file share you wish tooview.</span></span>

3. <span data-ttu-id="0f172-145">Expanda a conta de armazenamento a Olá **partilhas de ficheiros**.</span><span class="sxs-lookup"><span data-stu-id="0f172-145">Expand hello storage account's **File Shares**.</span></span>

4. <span data-ttu-id="0f172-146">Partilha de ficheiros do contexto Olá que queira toodelete e, no menu de contexto de Olá - selecione **eliminar**.</span><span class="sxs-lookup"><span data-stu-id="0f172-146">Right-click hello file share you wish toodelete, and - from hello context menu - select **Delete**.</span></span> <span data-ttu-id="0f172-147">Também pode premir **eliminar** partilha do toodelete Olá ficheiro atualmente selecionado.</span><span class="sxs-lookup"><span data-stu-id="0f172-147">You can also press **Delete** toodelete hello currently selected file share.</span></span>

    ![Eliminar](media/vs-azure-tools-storage-explorer-files/image6.png)

5. <span data-ttu-id="0f172-149">Selecione **Sim** toohello diálogo de confirmação.</span><span class="sxs-lookup"><span data-stu-id="0f172-149">Select **Yes** toohello confirmation dialog.</span></span>
    
    ![Caixa de diálogo de confirmação](media/vs-azure-tools-storage-explorer-files/image7.png)

## <a name="copy-a-file-share"></a><span data-ttu-id="0f172-151">Copiar partilhas de ficheiros</span><span class="sxs-lookup"><span data-stu-id="0f172-151">Copy a file share</span></span>

<span data-ttu-id="0f172-152">Explorador de armazenamento (pré-visualização) permite-lhe toocopy uma área de transferência de toohello de partilha de ficheiros e, em seguida, cole que a partilha de ficheiros para outra conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="0f172-152">Storage Explorer (Preview) enables you toocopy a file share toohello clipboard, and then paste that file share into another storage account.</span></span> <span data-ttu-id="0f172-153">(toosee como ficheiros individuais toocopy, consulte a secção de toohello, [gerir ficheiros numa partilha de ficheiros](https://docs.microsoft.com//azure/vs-azure-tools-storage-explorer-blobs#managing-blobs-in-a-blob-container).)</span><span class="sxs-lookup"><span data-stu-id="0f172-153">(toosee how toocopy individual files, refer toohello section, [Managing files in a file share](https://docs.microsoft.com//azure/vs-azure-tools-storage-explorer-blobs#managing-blobs-in-a-blob-container).)</span></span>

<span data-ttu-id="0f172-154">Olá, os passos seguintes mostram como toocopy um ficheiro de partilha de um tooanother de conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="0f172-154">hello following steps illustrate how toocopy a file share from one storage account tooanother.</span></span>

1. <span data-ttu-id="0f172-155">Abrir o Explorador de Armazenamento (Pré-visualização).</span><span class="sxs-lookup"><span data-stu-id="0f172-155">Open Storage Explorer (Preview).</span></span>

2. <span data-ttu-id="0f172-156">No painel esquerdo Olá, expanda a conta de armazenamento de Olá com partilha de ficheiros de Olá desejar toocopy.</span><span class="sxs-lookup"><span data-stu-id="0f172-156">In hello left pane, expand hello storage account containing hello file share you wish toocopy.</span></span>

3. <span data-ttu-id="0f172-157">Expanda a conta de armazenamento a Olá **partilhas de ficheiros**.</span><span class="sxs-lookup"><span data-stu-id="0f172-157">Expand hello storage account's **File Shares**.</span></span>

4. <span data-ttu-id="0f172-158">Partilha de ficheiros do contexto Olá que queira toocopy e, no menu de contexto de Olá - selecione **partilha de ficheiros de cópia**.</span><span class="sxs-lookup"><span data-stu-id="0f172-158">Right-click hello file share you wish toocopy, and - from hello context menu - select **Copy File Share**.</span></span>

    ![Copiar Partilha de Ficheiros](media/vs-azure-tools-storage-explorer-files/image8.png)

5. <span data-ttu-id="0f172-160">Faça duplo clique de conta de armazenamento de destino"Olá pretendido" para o qual pretende partilha de ficheiros toopaste Olá e - a partir do menu de contexto de Olá - selecione **partilha de ficheiros de colar**.</span><span class="sxs-lookup"><span data-stu-id="0f172-160">Right-click hello desired "target" storage account into which you want toopaste hello file share, and - from hello context menu - select **Paste File Share**.</span></span>

    ![Criar Partilha de Ficheiros](media/vs-azure-tools-storage-explorer-files/image9.png)

## <a name="get-hello-sas-for-a-file-share"></a><span data-ttu-id="0f172-162">Obter Olá SAS para uma partilha de ficheiros</span><span class="sxs-lookup"><span data-stu-id="0f172-162">Get hello SAS for a file share</span></span>

<span data-ttu-id="0f172-163">A [assinatura de acesso partilhado (SAS)](https://docs.microsoft.com//azure/storage/storage-dotnet-shared-access-signature-part-1) fornece acesso delegado tooresources na sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="0f172-163">A [shared access signature (SAS)](https://docs.microsoft.com//azure/storage/storage-dotnet-shared-access-signature-part-1) provides delegated access tooresources in your storage account.</span></span> <span data-ttu-id="0f172-164">Isto significa que pode conceder que um cliente limitada tooobjects de permissões na sua conta de armazenamento para um determinado período de tempo e com um conjunto especificado de permissões, sem ter tooshare as chaves de acesso da conta.</span><span class="sxs-lookup"><span data-stu-id="0f172-164">This means that you can grant a client limited permissions tooobjects in your storage account for a specified period of time and with a specified set of permissions, without having tooshare your account access keys.</span></span>

<span data-ttu-id="0f172-165">Olá passos seguintes mostram como toocreate partilhar uma SAS para um ficheiro: +</span><span class="sxs-lookup"><span data-stu-id="0f172-165">hello following steps illustrate how toocreate a SAS for a file share:+</span></span>

1. <span data-ttu-id="0f172-166">Abrir o Explorador de Armazenamento (Pré-visualização).</span><span class="sxs-lookup"><span data-stu-id="0f172-166">Open Storage Explorer (Preview).</span></span>

2. <span data-ttu-id="0f172-167">No painel esquerdo Olá, expanda a conta de armazenamento de Olá com partilha de ficheiros de Olá para o qual pretende tooget uma SAS.</span><span class="sxs-lookup"><span data-stu-id="0f172-167">In hello left pane, expand hello storage account containing hello file share for which you wish tooget a SAS.</span></span>

3. <span data-ttu-id="0f172-168">Expanda a conta de armazenamento a Olá **partilhas de ficheiros**.</span><span class="sxs-lookup"><span data-stu-id="0f172-168">Expand hello storage account's **File Shares**.</span></span>

4. <span data-ttu-id="0f172-169">Partilha de ficheiros pretendido de Olá com o botão direito e, no menu de contexto de Olá - selecione **obter assinatura de acesso partilhado**.</span><span class="sxs-lookup"><span data-stu-id="0f172-169">Right-click hello desired file share, and - from hello context menu - select **Get Shared Access Signature**.</span></span>

    ![Obter Assinatura de Acesso Partilhado](media/vs-azure-tools-storage-explorer-files/image10.png)

5. <span data-ttu-id="0f172-171">No Olá **assinatura de acesso partilhado** caixa de diálogo, especificar a política de Olá, datas de início e de expiração, fuso horário e níveis de que pretende para recursos de Olá de acesso.</span><span class="sxs-lookup"><span data-stu-id="0f172-171">In hello **Shared Access Signature** dialog, specify hello policy, start and expiration dates, time zone, and access levels you want for hello resource.</span></span>

    ![Caixa de diálogo SAS](media/vs-azure-tools-storage-explorer-files/image11.png)

6. <span data-ttu-id="0f172-173">Quando tiver terminado de especificar opções de SAS Olá, selecione **criar**.</span><span class="sxs-lookup"><span data-stu-id="0f172-173">When you're finished specifying hello SAS options, select **Create**.</span></span>

7. <span data-ttu-id="0f172-174">Um segundo **assinatura de acesso partilhado** caixa de diálogo, em seguida, irá apresentar que apresenta uma lista de Olá partilha de ficheiros, juntamente com o URL de Olá e QueryStrings pode utilizar tooaccess Olá recursos de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="0f172-174">A second **Shared Access Signature** dialog will then display that lists hello file share along with hello URL and QueryStrings you can use tooaccess hello storage resource.</span></span> <span data-ttu-id="0f172-175">Selecione **cópia** seguinte URL de toohello desejar área de transferência do toocopy toohello.</span><span class="sxs-lookup"><span data-stu-id="0f172-175">Select **Copy** next toohello URL you wish toocopy toohello clipboard.</span></span>
    
    ![Segunda caixa de diálogo SAS](media/vs-azure-tools-storage-explorer-files/image12.png)

8. <span data-ttu-id="0f172-177">Quando terminar, selecione **Close (Fechar)**.</span><span class="sxs-lookup"><span data-stu-id="0f172-177">When done, select **Close**.</span></span>

## <a name="manage-access-policies-for-a-file-share"></a><span data-ttu-id="0f172-178">Gerir as Políticas de Acesso de uma partilha de ficheiros</span><span class="sxs-lookup"><span data-stu-id="0f172-178">Manage Access Policies for a file share</span></span>

<span data-ttu-id="0f172-179">Olá passos seguintes mostram como toomanage (adicionar e remover) políticas para uma partilha de ficheiros de acesso: +.</span><span class="sxs-lookup"><span data-stu-id="0f172-179">hello following steps illustrate how toomanage (add and remove) access policies for a file share:+ .</span></span> <span data-ttu-id="0f172-180">Políticas de acesso de Olá é utilizada para criar URLs de SAS através do qual as pessoas podem utilizar tooaccess Olá recurso do ficheiro de armazenamento durante um período de tempo definido.</span><span class="sxs-lookup"><span data-stu-id="0f172-180">hello Access Policies is used for creating SAS URLs through which people can use tooaccess hello Storage File resource during a defined period of time.</span></span>

1. <span data-ttu-id="0f172-181">Abrir o Explorador de Armazenamento (Pré-visualização).</span><span class="sxs-lookup"><span data-stu-id="0f172-181">Open Storage Explorer (Preview).</span></span>

2. <span data-ttu-id="0f172-182">No painel esquerdo Olá, expanda a conta de armazenamento de Olá com partilha de ficheiros de Olá cujas políticas de acesso pretende toomanage.</span><span class="sxs-lookup"><span data-stu-id="0f172-182">In hello left pane, expand hello storage account containing hello file share whose access policies you wish toomanage.</span></span>

3. <span data-ttu-id="0f172-183">Expanda a conta de armazenamento a Olá **partilhas de ficheiros**.</span><span class="sxs-lookup"><span data-stu-id="0f172-183">Expand hello storage account's **File Shares**.</span></span>

4. <span data-ttu-id="0f172-184">Selecione a partilha de ficheiros pretendido de Olá e, no menu de contexto de Olá - selecione **gerir políticas de acesso**.</span><span class="sxs-lookup"><span data-stu-id="0f172-184">Select hello desired file share, and - from hello context menu - select **Manage Access Policies**.</span></span>

    ![Menu de Contexto Gerir políticas de acesso](media/vs-azure-tools-storage-explorer-files/image13.png)

5. <span data-ttu-id="0f172-186">Olá **políticas de acesso** apresentará uma caixa de diálogo lista quaisquer políticas de acesso já criadas para a partilha de ficheiros selecionado Olá.</span><span class="sxs-lookup"><span data-stu-id="0f172-186">hello **Access Policies** dialog will list any access policies already created for hello selected file share.</span></span>
    
    ![Políticas de Acesso](media/vs-azure-tools-storage-explorer-files/image14.png)

6. <span data-ttu-id="0f172-188">Siga estes passos, dependendo da tarefa de gestão de política de acesso de Olá:</span><span class="sxs-lookup"><span data-stu-id="0f172-188">Follow these steps depending on hello access policy management task:</span></span>
    
    - <span data-ttu-id="0f172-189">**Adicionar uma política de acesso nova** - selecione **Add (Adicionar)**.</span><span class="sxs-lookup"><span data-stu-id="0f172-189">**Add a new access policy** - Select **Add**.</span></span> <span data-ttu-id="0f172-190">Depois de o gerado, Olá **políticas de acesso** diálogo apresentará Olá recém-adicionada política (com as predefinições) de acesso.</span><span class="sxs-lookup"><span data-stu-id="0f172-190">Once generated, hello **Access Policies** dialog will display hello newly added access policy (with default settings).</span></span>

    - <span data-ttu-id="0f172-191">**Editar uma política de acesso** - faça eventuais alterações que pretenda e selecione **Save (Guardar)**.</span><span class="sxs-lookup"><span data-stu-id="0f172-191">**Edit an access policy** - Make any desired edits, and select **Save**.</span></span>

    - <span data-ttu-id="0f172-192">**Remover uma política de acesso** - selecione **remover** próxima política de acesso de toohello desejar tooremove.</span><span class="sxs-lookup"><span data-stu-id="0f172-192">**Remove an access policy** - Select **Remove** next toohello access policy you wish tooremove.</span></span>

7. <span data-ttu-id="0f172-193">Crie um novo URL de SAS através de Olá política de acesso que criou anteriormente:</span><span class="sxs-lookup"><span data-stu-id="0f172-193">Create a new SAS URL using hello Access Policy you created earlier:</span></span>
    
    ![Obter SAS](media/vs-azure-tools-storage-explorer-files/image15.png)
    
    ![Nome e propriedades de SAS](media/vs-azure-tools-storage-explorer-files/image16.png)

## <a name="managing-files-in-a-file-share"></a><span data-ttu-id="0f172-196">Gerir ficheiros numa partilha de ficheiros</span><span class="sxs-lookup"><span data-stu-id="0f172-196">Managing files in a file share</span></span>

<span data-ttu-id="0f172-197">Assim que tiver criado uma partilha de ficheiros, pode carregar uma partilha de ficheiros do ficheiro toothat, transferir um computador local do ficheiro tooyour, abra um ficheiro no seu computador local e muito mais.</span><span class="sxs-lookup"><span data-stu-id="0f172-197">Once you've created a file share, you can upload a file toothat file share, download a file tooyour local computer, open a file on your local computer, and much more.</span></span>

<span data-ttu-id="0f172-198">Olá passos seguintes mostram como partilharem toomanage Olá ficheiros (e pastas) dentro de um ficheiro.</span><span class="sxs-lookup"><span data-stu-id="0f172-198">hello following steps illustrate how toomanage hello files (and folders) within a file share.</span></span>

1.  <span data-ttu-id="0f172-199">Abrir o Explorador de Armazenamento (Pré-visualização).</span><span class="sxs-lookup"><span data-stu-id="0f172-199">Open Storage Explorer (Preview).</span></span>

2.  <span data-ttu-id="0f172-200">No painel esquerdo Olá, expanda a conta de armazenamento de Olá com partilha de ficheiros de Olá desejar toomanage.</span><span class="sxs-lookup"><span data-stu-id="0f172-200">In hello left pane, expand hello storage account containing hello file share you wish toomanage.</span></span>

3.  <span data-ttu-id="0f172-201">Expanda a conta de armazenamento a Olá **partilhas de ficheiros**.</span><span class="sxs-lookup"><span data-stu-id="0f172-201">Expand hello storage account's **File Shares**.</span></span>

4.  <span data-ttu-id="0f172-202">Faça duplo clique em partilha de ficheiros de Olá desejar tooview.</span><span class="sxs-lookup"><span data-stu-id="0f172-202">Double-click hello file share you wish tooview.</span></span>

5.  <span data-ttu-id="0f172-203">painel principal Olá apresentará o conteúdo da partilha de ficheiros Olá.</span><span class="sxs-lookup"><span data-stu-id="0f172-203">hello main pane will display hello file share's contents.</span></span>

    ![Olá conteúdos da partilha](media/vs-azure-tools-storage-explorer-files/image17.png)

6.  <span data-ttu-id="0f172-205">painel principal Olá apresentará o conteúdo da partilha de ficheiros Olá.</span><span class="sxs-lookup"><span data-stu-id="0f172-205">hello main pane will display hello file share's contents.</span></span>

7.  <span data-ttu-id="0f172-206">Siga estes que passos, dependendo das tarefas de Olá desejar tooperform:</span><span class="sxs-lookup"><span data-stu-id="0f172-206">Follow these steps depending on hello task you wish tooperform:</span></span>

    - <span data-ttu-id="0f172-207">**Carregar a partilha de ficheiros de tooa de ficheiros**</span><span class="sxs-lookup"><span data-stu-id="0f172-207">**Upload files tooa file share**</span></span>

        <span data-ttu-id="0f172-208">a.</span><span class="sxs-lookup"><span data-stu-id="0f172-208">a.</span></span>  <span data-ttu-id="0f172-209">Na barra de ferramentas do painel Olá principal, selecione **carregar**e, em seguida, **carregar ficheiros** no menu de Olá pendente.</span><span class="sxs-lookup"><span data-stu-id="0f172-209">On hello main pane's toolbar, select **Upload**, and then **Upload Files** from hello drop-down menu.</span></span>

        ![Carregar ficheiros](media/vs-azure-tools-storage-explorer-files/image18.png)
        
        <span data-ttu-id="0f172-211">b.</span><span class="sxs-lookup"><span data-stu-id="0f172-211">b.</span></span> <span data-ttu-id="0f172-212">No Olá **carregar ficheiros** caixa de diálogo, reticências Olá selecione (**...** ) botão no lado direito de Olá de Olá **ficheiros** tooselect Olá ficheiros pretende tooupload de caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="0f172-212">In hello **Upload files** dialog, select hello ellipsis (**…**) button on hello right side of hello **Files** text box tooselect hello file(s) you wish tooupload.</span></span>

        ![Adição ficheiros](media/vs-azure-tools-storage-explorer-files/image19.png)

        <span data-ttu-id="0f172-214">c.</span><span class="sxs-lookup"><span data-stu-id="0f172-214">c.</span></span> <span data-ttu-id="0f172-215">Selecione **Upload**.</span><span class="sxs-lookup"><span data-stu-id="0f172-215">Select **Upload**.</span></span>

    - <span data-ttu-id="0f172-216">**Carregar uma partilha de ficheiros de tooa pasta**</span><span class="sxs-lookup"><span data-stu-id="0f172-216">**Upload a folder tooa file share**</span></span>
        
        <span data-ttu-id="0f172-217">a.</span><span class="sxs-lookup"><span data-stu-id="0f172-217">a.</span></span> <span data-ttu-id="0f172-218">Na barra de ferramentas do painel Olá principal, selecione **carregar**e, em seguida, **carregar pasta** no menu de Olá pendente.</span><span class="sxs-lookup"><span data-stu-id="0f172-218">On hello main pane's toolbar, select **Upload**, and then **Upload Folder** from hello drop-down menu.</span></span>

        ![Menu Carregar pasta](media/vs-azure-tools-storage-explorer-files/image20.png)

        <span data-ttu-id="0f172-220">b.</span><span class="sxs-lookup"><span data-stu-id="0f172-220">b.</span></span> <span data-ttu-id="0f172-221">No Olá **carregamento pasta** caixa de diálogo, reticências Olá selecione (**...** ) botão no lado direito de Olá de Olá **pasta** pasta de Olá de tooselect de caixa de texto cujo conteúdo pretende tooupload.</span><span class="sxs-lookup"><span data-stu-id="0f172-221">In hello **Upload folder** dialog, select hello ellipsis (**…**) button on hello right side of hello **Folder** text box tooselect hello folder whose contents you wish tooupload.</span></span>

        <span data-ttu-id="0f172-222">c.</span><span class="sxs-lookup"><span data-stu-id="0f172-222">c.</span></span> <span data-ttu-id="0f172-223">Opcionalmente, especifique uma pasta de destino no qual Olá conteúdo da pasta selecionado será carregado.</span><span class="sxs-lookup"><span data-stu-id="0f172-223">Optionally, specify a target folder into which hello selected folder's contents will be uploaded.</span></span> <span data-ttu-id="0f172-224">Se a pasta de destino Olá não existir, será criado.</span><span class="sxs-lookup"><span data-stu-id="0f172-224">If hello target folder doesn’t exist, it will be created.</span></span>

        <span data-ttu-id="0f172-225">d.</span><span class="sxs-lookup"><span data-stu-id="0f172-225">d.</span></span> <span data-ttu-id="0f172-226">Selecione **Upload**.</span><span class="sxs-lookup"><span data-stu-id="0f172-226">Select **Upload**.</span></span>

    - <span data-ttu-id="0f172-227">**Transferir um computador local do ficheiro tooyour**</span><span class="sxs-lookup"><span data-stu-id="0f172-227">**Download a file tooyour local computer**</span></span>
        
        <span data-ttu-id="0f172-228">a.</span><span class="sxs-lookup"><span data-stu-id="0f172-228">a.</span></span> <span data-ttu-id="0f172-229">Selecione o ficheiro de Olá desejar toodownload.</span><span class="sxs-lookup"><span data-stu-id="0f172-229">Select hello file you wish toodownload.</span></span>
        
        <span data-ttu-id="0f172-230">b.</span><span class="sxs-lookup"><span data-stu-id="0f172-230">b.</span></span> <span data-ttu-id="0f172-231">Na barra de ferramentas do painel Olá principal, selecione **transferir**.</span><span class="sxs-lookup"><span data-stu-id="0f172-231">On hello main pane's toolbar, select **Download**.</span></span>
        
        <span data-ttu-id="0f172-232">c.</span><span class="sxs-lookup"><span data-stu-id="0f172-232">c.</span></span> <span data-ttu-id="0f172-233">No Olá **Especifique qual toosave Olá transferidos ficheiros** caixa de diálogo, especifique onde pretende que o ficheiro de Olá transferido de localização de Olá e Olá nome desejar toogive-lo.</span><span class="sxs-lookup"><span data-stu-id="0f172-233">In hello **Specify where toosave hello downloaded file** dialog, specify hello location where you want hello file downloaded, and hello name you wish toogive it.</span></span>

        <span data-ttu-id="0f172-234">d.</span><span class="sxs-lookup"><span data-stu-id="0f172-234">d.</span></span> <span data-ttu-id="0f172-235">Selecione **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="0f172-235">Select **Save**.</span></span>

    - <span data-ttu-id="0f172-236">**Abrir um ficheiro no seu computador local**</span><span class="sxs-lookup"><span data-stu-id="0f172-236">**Open a file on your local computer**</span></span>
        
        <span data-ttu-id="0f172-237">a.</span><span class="sxs-lookup"><span data-stu-id="0f172-237">a.</span></span>  <span data-ttu-id="0f172-238">Selecione o ficheiro de Olá desejar tooopen.</span><span class="sxs-lookup"><span data-stu-id="0f172-238">Select hello file you wish tooopen.</span></span>
        
        <span data-ttu-id="0f172-239">b.</span><span class="sxs-lookup"><span data-stu-id="0f172-239">b.</span></span>  <span data-ttu-id="0f172-240">Na barra de ferramentas do painel Olá principal, selecione **abra**.</span><span class="sxs-lookup"><span data-stu-id="0f172-240">On hello main pane's toolbar, select **Open**.</span></span>
        
        <span data-ttu-id="0f172-241">c.</span><span class="sxs-lookup"><span data-stu-id="0f172-241">c.</span></span>  <span data-ttu-id="0f172-242">ficheiro de Olá será transferido e aberta utilizando a aplicação Olá associada ao tipo de ficheiro do ficheiro de Olá subjacente.</span><span class="sxs-lookup"><span data-stu-id="0f172-242">hello file will be downloaded and opened using hello application associated with hello file's underlying file type.</span></span>

    - <span data-ttu-id="0f172-243">**Copiar uma área de transferência do ficheiro toohello**</span><span class="sxs-lookup"><span data-stu-id="0f172-243">**Copy a file toohello clipboard**</span></span>

        <span data-ttu-id="0f172-244">a.</span><span class="sxs-lookup"><span data-stu-id="0f172-244">a.</span></span> <span data-ttu-id="0f172-245">Selecione o ficheiro de Olá desejar toocopy.</span><span class="sxs-lookup"><span data-stu-id="0f172-245">Select hello file you wish toocopy.</span></span>

        <span data-ttu-id="0f172-246">b.</span><span class="sxs-lookup"><span data-stu-id="0f172-246">b.</span></span> <span data-ttu-id="0f172-247">Na barra de ferramentas do painel Olá principal, selecione **cópia**.</span><span class="sxs-lookup"><span data-stu-id="0f172-247">On hello main pane's toolbar, select **Copy**.</span></span>

        <span data-ttu-id="0f172-248">c.</span><span class="sxs-lookup"><span data-stu-id="0f172-248">c.</span></span> <span data-ttu-id="0f172-249">No painel esquerdo Olá, navegue tooanother partilha de ficheiros e faça duplo clique tooview-lo no painel principal Olá.</span><span class="sxs-lookup"><span data-stu-id="0f172-249">In hello left pane, navigate tooanother file share, and double-click it tooview it in hello main pane.</span></span>

        <span data-ttu-id="0f172-250">d.</span><span class="sxs-lookup"><span data-stu-id="0f172-250">d.</span></span> <span data-ttu-id="0f172-251">Na barra de ferramentas do painel Olá principal, selecione **colar** toocreate uma cópia do ficheiro de Olá.</span><span class="sxs-lookup"><span data-stu-id="0f172-251">On hello main pane's toolbar, select **Paste** toocreate a copy of hello file.</span></span>

    - <span data-ttu-id="0f172-252">**Eliminar um ficheiro**</span><span class="sxs-lookup"><span data-stu-id="0f172-252">**Delete a file**</span></span>

        <span data-ttu-id="0f172-253">a.</span><span class="sxs-lookup"><span data-stu-id="0f172-253">a.</span></span> <span data-ttu-id="0f172-254">Selecione o ficheiro de Olá desejar toodelete.</span><span class="sxs-lookup"><span data-stu-id="0f172-254">Select hello file you wish toodelete.</span></span>

        <span data-ttu-id="0f172-255">b.</span><span class="sxs-lookup"><span data-stu-id="0f172-255">b.</span></span> <span data-ttu-id="0f172-256">Na barra de ferramentas do painel Olá principal, selecione **eliminar**.</span><span class="sxs-lookup"><span data-stu-id="0f172-256">On hello main pane's toolbar, select **Delete**.</span></span>

        <span data-ttu-id="0f172-257">c.</span><span class="sxs-lookup"><span data-stu-id="0f172-257">c.</span></span> <span data-ttu-id="0f172-258">Selecione **Sim** toohello diálogo de confirmação.</span><span class="sxs-lookup"><span data-stu-id="0f172-258">Select **Yes** toohello confirmation dialog.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0f172-259">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="0f172-259">Next steps</span></span>

- <span data-ttu-id="0f172-260">Olá vista [mais recente notas de versão do Explorador de armazenamento (pré-visualização) e vídeos](http://www.storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="0f172-260">View hello [latest Storage Explorer (Preview) release notes and videos](http://www.storageexplorer.com/).</span></span>

- <span data-ttu-id="0f172-261">Saiba como demasiado[criar aplicações utilizar blobs do Azure, tabelas, filas e os ficheiros](https://azure.microsoft.com/documentation/services/storage/).</span><span class="sxs-lookup"><span data-stu-id="0f172-261">Learn how too[create applications using Azure blobs, tables, queues, and files](https://azure.microsoft.com/documentation/services/storage/).</span></span>
