---
title: "aaaManage recursos de armazenamento de Blobs do Azure com o Explorador de armazenamento (pré-visualização) | Microsoft Docs"
description: "Gerir os contentores de Blobs do Azure e Blobs com o Explorador de armazenamento (pré-visualização)"
services: storage
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 2f09e545-ec94-4d89-b96c-14783cc9d7a9
ms.service: storage
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/18/2016
ms.author: kraigb
ms.openlocfilehash: 503dd061b205875da127378ab48e8d465800fc09
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-blob-storage-resources-with-storage-explorer-preview"></a><span data-ttu-id="6c4ac-103">Gerir recursos de armazenamento de Blobs do Azure com o Explorador de armazenamento (pré-visualização)</span><span class="sxs-lookup"><span data-stu-id="6c4ac-103">Manage Azure Blob Storage resources with Storage Explorer (Preview)</span></span>
## <a name="overview"></a><span data-ttu-id="6c4ac-104">Descrição geral</span><span class="sxs-lookup"><span data-stu-id="6c4ac-104">Overview</span></span>
<span data-ttu-id="6c4ac-105">[Armazenamento de Blobs do Azure](storage/blobs/storage-dotnet-how-to-use-blobs.md) é um serviço para armazenar grandes quantidades de dados não estruturados, tais como texto ou dados binários, que podem ser acedidos de qualquer local no mundo Olá através de HTTP ou HTTPS.</span><span class="sxs-lookup"><span data-stu-id="6c4ac-105">[Azure Blob Storage](storage/blobs/storage-dotnet-how-to-use-blobs.md) is a service for storing large amounts of unstructured data, such as text or binary data, that can be accessed from anywhere in hello world via HTTP or HTTPS.</span></span>
<span data-ttu-id="6c4ac-106">Pode utilizar os dados do Blob storage tooexpose publicamente toohello mundo ou toostore dados da aplicação em privado.</span><span class="sxs-lookup"><span data-stu-id="6c4ac-106">You can use Blob storage tooexpose data publicly toohello world, or toostore application data privately.</span></span> <span data-ttu-id="6c4ac-107">Neste artigo, irá aprender como toouse Explorador de armazenamento (pré-visualização) toowork com blobs e contentores de Blobs.</span><span class="sxs-lookup"><span data-stu-id="6c4ac-107">In this article, you'll learn how toouse Storage Explorer (Preview) toowork with blob containers and blobs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6c4ac-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="6c4ac-108">Prerequisites</span></span>
<span data-ttu-id="6c4ac-109">toocomplete Olá passos descritos neste artigo, irá precisar seguinte Olá:</span><span class="sxs-lookup"><span data-stu-id="6c4ac-109">toocomplete hello steps in this article, you'll need hello following:</span></span>

* [<span data-ttu-id="6c4ac-110">Transfira e instale o Explorador de Armazenamento (pré-visualização)</span><span class="sxs-lookup"><span data-stu-id="6c4ac-110">Download and install Storage Explorer (preview)</span></span>](http://www.storageexplorer.com)
* [<span data-ttu-id="6c4ac-111">Ligar a conta de armazenamento do Azure tooa ou serviço</span><span class="sxs-lookup"><span data-stu-id="6c4ac-111">Connect tooa Azure storage account or service</span></span>](vs-azure-tools-storage-manage-with-storage-explorer.md#connect-to-a-storage-account-or-service)

## <a name="create-a-blob-container"></a><span data-ttu-id="6c4ac-112">Criar um contentor de blob</span><span class="sxs-lookup"><span data-stu-id="6c4ac-112">Create a blob container</span></span>
<span data-ttu-id="6c4ac-113">Todos os blobs tem de residir num contentor de blob, que é simplesmente um agrupamento lógico de blobs.</span><span class="sxs-lookup"><span data-stu-id="6c4ac-113">All blobs must reside in a blob container, which is simply a logical grouping of blobs.</span></span> <span data-ttu-id="6c4ac-114">Uma conta pode conter um número ilimitado de contentores, e cada contentor pode armazenar um número ilimitado de blobs.</span><span class="sxs-lookup"><span data-stu-id="6c4ac-114">An account can contain an unlimited number of containers, and each container can store an unlimited number of blobs.</span></span>

<span data-ttu-id="6c4ac-115">Olá passos seguintes mostram como toocreate um contentor do blob no Explorador de armazenamento (pré-visualização).</span><span class="sxs-lookup"><span data-stu-id="6c4ac-115">hello following steps illustrate how toocreate a blob container within Storage Explorer (Preview).</span></span>

1. <span data-ttu-id="6c4ac-116">Abrir o Explorador de Armazenamento (Pré-visualização).</span><span class="sxs-lookup"><span data-stu-id="6c4ac-116">Open Storage Explorer (Preview).</span></span>
2. <span data-ttu-id="6c4ac-117">No painel esquerdo Olá, expanda a conta de armazenamento de Olá no qual pretende o contentor de BLOBs de Olá toocreate.</span><span class="sxs-lookup"><span data-stu-id="6c4ac-117">In hello left pane, expand hello storage account within which you wish toocreate hello blob container.</span></span>
3. <span data-ttu-id="6c4ac-118">Clique com botão direito **contentores de BLOBs**e, no menu de contexto de Olá - selecione **criar contentor de Blob**.</span><span class="sxs-lookup"><span data-stu-id="6c4ac-118">Right-click **Blob Containers**, and - from hello context menu - select **Create Blob Container**.</span></span>

   ![Criar o menu de contexto de contentores de BLOBs][0]
4. <span data-ttu-id="6c4ac-120">Será apresentada uma caixa de texto abaixo Olá **contentores de BLOBs** pasta.</span><span class="sxs-lookup"><span data-stu-id="6c4ac-120">A text box will appear below hello **Blob Containers** folder.</span></span> <span data-ttu-id="6c4ac-121">Introduza o nome de Olá para o contentor do blob.</span><span class="sxs-lookup"><span data-stu-id="6c4ac-121">Enter hello name for your blob container.</span></span> <span data-ttu-id="6c4ac-122">Consulte Olá [regras de nomenclatura de contentor](storage/blobs/storage-dotnet-how-to-use-blobs.md#create-a-container) secção para obter uma lista de restrições em contentores de BLOBs de atribuição de nomes e regras.</span><span class="sxs-lookup"><span data-stu-id="6c4ac-122">See hello [Container naming rules](storage/blobs/storage-dotnet-how-to-use-blobs.md#create-a-container) section for a list of rules and restrictions on naming blob containers.</span></span>

   ![Criar caixa de texto de contentores de BLOBs][1]
5. <span data-ttu-id="6c4ac-124">Prima **Enter** concluída ao contentor do blob toocreate hello, ou **Esc** toocancel.</span><span class="sxs-lookup"><span data-stu-id="6c4ac-124">Press **Enter** when done toocreate hello blob container, or **Esc** toocancel.</span></span> <span data-ttu-id="6c4ac-125">Depois de contentor do blob Olá foi criado com êxito, será apresentado em Olá **contentores de BLOBs** pasta para Olá selecionado a conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="6c4ac-125">Once hello blob container has been successfully created, it will be displayed under hello **Blob Containers** folder for hello selected storage account.</span></span>

   ![Criada o contentor de BLOBs][2]

## <a name="view-a-blob-containers-contents"></a><span data-ttu-id="6c4ac-127">Ver os conteúdos de um contentor de BLOBs</span><span class="sxs-lookup"><span data-stu-id="6c4ac-127">View a blob container's contents</span></span>
<span data-ttu-id="6c4ac-128">Os contentores de blob contém os blobs e de pastas (que também podem conter os blobs).</span><span class="sxs-lookup"><span data-stu-id="6c4ac-128">Blob containers contain blobs and folders (that can also contain blobs).</span></span>

<span data-ttu-id="6c4ac-129">Olá passos seguintes mostram como conteúdo Olá tooview um contentor do blob no Explorador de armazenamento (pré-visualização):</span><span class="sxs-lookup"><span data-stu-id="6c4ac-129">hello following steps illustrate how tooview hello contents of a blob container within Storage Explorer (Preview):</span></span>

1. <span data-ttu-id="6c4ac-130">Abrir o Explorador de Armazenamento (Pré-visualização).</span><span class="sxs-lookup"><span data-stu-id="6c4ac-130">Open Storage Explorer (Preview).</span></span>
2. <span data-ttu-id="6c4ac-131">No painel esquerdo Olá, expanda a conta de armazenamento de Olá que contém o contentor de blob Olá desejar tooview.</span><span class="sxs-lookup"><span data-stu-id="6c4ac-131">In hello left pane, expand hello storage account containing hello blob container you wish tooview.</span></span>
3. <span data-ttu-id="6c4ac-132">Expanda a conta de armazenamento a Olá **contentores de BLOBs**.</span><span class="sxs-lookup"><span data-stu-id="6c4ac-132">Expand hello storage account's **Blob Containers**.</span></span>
4. <span data-ttu-id="6c4ac-133">Contentor de blob do contexto Olá que queira tooview e, no menu de contexto de Olá - selecione **abra Editor de contentor do Blob**.</span><span class="sxs-lookup"><span data-stu-id="6c4ac-133">Right-click hello blob container you wish tooview, and - from hello context menu - select **Open Blob Container Editor**.</span></span>
   <span data-ttu-id="6c4ac-134">Também pode fazer duplo clique contentor do blob Olá desejar tooview.</span><span class="sxs-lookup"><span data-stu-id="6c4ac-134">You can also double-click hello blob container you wish tooview.</span></span>

   ![Menu de contexto de editor de contentor de blob aberta][19]
5. <span data-ttu-id="6c4ac-136">painel principal Olá apresentará o conteúdo do contentor de blob Olá.</span><span class="sxs-lookup"><span data-stu-id="6c4ac-136">hello main pane will display hello blob container's contents.</span></span>

   ![Editor de contentor do blob][3]

## <a name="delete-a-blob-container"></a><span data-ttu-id="6c4ac-138">Eliminar um contentor do blob</span><span class="sxs-lookup"><span data-stu-id="6c4ac-138">Delete a blob container</span></span>
<span data-ttu-id="6c4ac-139">Contentores de blob podem ser facilmente criados e eliminadas, conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="6c4ac-139">Blob containers can be easily created and deleted as needed.</span></span> <span data-ttu-id="6c4ac-140">(toosee como blobs toodelete individuais, consulte a secção de toohello, [gerir os blobs num contentor de blob](#managing-blobs-in-a-blob-container).)</span><span class="sxs-lookup"><span data-stu-id="6c4ac-140">(toosee how toodelete individual blobs, refer toohello section, [Managing blobs in a blob container](#managing-blobs-in-a-blob-container).)</span></span>

<span data-ttu-id="6c4ac-141">Olá passos seguintes mostram como toodelete um contentor do blob no Explorador de armazenamento (pré-visualização):</span><span class="sxs-lookup"><span data-stu-id="6c4ac-141">hello following steps illustrate how toodelete a blob container within Storage Explorer (Preview):</span></span>

1. <span data-ttu-id="6c4ac-142">Abrir o Explorador de Armazenamento (Pré-visualização).</span><span class="sxs-lookup"><span data-stu-id="6c4ac-142">Open Storage Explorer (Preview).</span></span>
2. <span data-ttu-id="6c4ac-143">No painel esquerdo Olá, expanda a conta de armazenamento de Olá que contém o contentor de blob Olá desejar tooview.</span><span class="sxs-lookup"><span data-stu-id="6c4ac-143">In hello left pane, expand hello storage account containing hello blob container you wish tooview.</span></span>
3. <span data-ttu-id="6c4ac-144">Expanda a conta de armazenamento a Olá **contentores de BLOBs**.</span><span class="sxs-lookup"><span data-stu-id="6c4ac-144">Expand hello storage account's **Blob Containers**.</span></span>
4. <span data-ttu-id="6c4ac-145">Contentor de blob do contexto Olá que queira toodelete e, no menu de contexto de Olá - selecione **eliminar**.</span><span class="sxs-lookup"><span data-stu-id="6c4ac-145">Right-click hello blob container you wish toodelete, and - from hello context menu - select **Delete**.</span></span>
   <span data-ttu-id="6c4ac-146">Também pode premir **eliminar** contentor de blob atualmente selecionado toodelete Olá.</span><span class="sxs-lookup"><span data-stu-id="6c4ac-146">You can also press **Delete** toodelete hello currently selected blob container.</span></span>

   ![Eliminar o menu de contexto de contentor do blob][4]
5. <span data-ttu-id="6c4ac-148">Selecione **Sim** toohello diálogo de confirmação.</span><span class="sxs-lookup"><span data-stu-id="6c4ac-148">Select **Yes** toohello confirmation dialog.</span></span>

   ![Eliminar o blob confirmação do contentor][5]

## <a name="copy-a-blob-container"></a><span data-ttu-id="6c4ac-150">Copie um contentor do blob</span><span class="sxs-lookup"><span data-stu-id="6c4ac-150">Copy a blob container</span></span>
<span data-ttu-id="6c4ac-151">Explorador de armazenamento (pré-visualização) permite-lhe toocopy uma área de transferência do toohello de contentor do blob e, em seguida, colar que o contentor de blob para outra conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="6c4ac-151">Storage Explorer (Preview) enables you toocopy a blob container toohello clipboard, and then paste that blob container into another storage account.</span></span> <span data-ttu-id="6c4ac-152">(toosee como blobs toocopy individuais, consulte a secção de toohello, [gerir os blobs num contentor de blob](#managing-blobs-in-a-blob-container).)</span><span class="sxs-lookup"><span data-stu-id="6c4ac-152">(toosee how toocopy individual blobs, refer toohello section, [Managing blobs in a blob container](#managing-blobs-in-a-blob-container).)</span></span>

<span data-ttu-id="6c4ac-153">Olá, os passos seguintes mostram como toocopy um contentor de Blobs do armazenamento de uma conta tooanother.</span><span class="sxs-lookup"><span data-stu-id="6c4ac-153">hello following steps illustrate how toocopy a blob container from one storage account tooanother.</span></span>

1. <span data-ttu-id="6c4ac-154">Abrir o Explorador de Armazenamento (Pré-visualização).</span><span class="sxs-lookup"><span data-stu-id="6c4ac-154">Open Storage Explorer (Preview).</span></span>
2. <span data-ttu-id="6c4ac-155">No painel esquerdo Olá, expanda a conta de armazenamento de Olá que contém o contentor de blob Olá desejar toocopy.</span><span class="sxs-lookup"><span data-stu-id="6c4ac-155">In hello left pane, expand hello storage account containing hello blob container you wish toocopy.</span></span>
3. <span data-ttu-id="6c4ac-156">Expanda a conta de armazenamento a Olá **contentores de BLOBs**.</span><span class="sxs-lookup"><span data-stu-id="6c4ac-156">Expand hello storage account's **Blob Containers**.</span></span>
4. <span data-ttu-id="6c4ac-157">Contentor de blob do contexto Olá que queira toocopy e, no menu de contexto de Olá - selecione **contentor de BLOBs de cópia**.</span><span class="sxs-lookup"><span data-stu-id="6c4ac-157">Right-click hello blob container you wish toocopy, and - from hello context menu - select **Copy Blob Container**.</span></span>

   ![Copie o menu de contexto de contentor do blob][6]
5. <span data-ttu-id="6c4ac-159">Faça duplo clique de conta de armazenamento de destino"Olá pretendido" para o qual pretende contentor do blob toopaste Olá e - a partir do menu de contexto de Olá - selecione **contentor de BLOBs de colar**.</span><span class="sxs-lookup"><span data-stu-id="6c4ac-159">Right-click hello desired "target" storage account into which you want toopaste hello blob container, and - from hello context menu - select **Paste Blob Container**.</span></span>

   ![Menu de contexto de contentor de blob de colar][7]

## <a name="get-hello-sas-for-a-blob-container"></a><span data-ttu-id="6c4ac-161">Obter Olá SAS para um contentor de blob</span><span class="sxs-lookup"><span data-stu-id="6c4ac-161">Get hello SAS for a blob container</span></span>
<span data-ttu-id="6c4ac-162">A [assinatura de acesso partilhado (SAS)](storage/common/storage-dotnet-shared-access-signature-part-1.md) fornece acesso delegado tooresources na sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="6c4ac-162">A [shared access signature (SAS)](storage/common/storage-dotnet-shared-access-signature-part-1.md) provides delegated access tooresources in your storage account.</span></span>
<span data-ttu-id="6c4ac-163">Isto significa que pode conceder que um cliente limitada tooobjects de permissões na sua conta de armazenamento para um determinado período de tempo e com um conjunto especificado de permissões, sem ter de partilhar as chaves de acesso da conta.</span><span class="sxs-lookup"><span data-stu-id="6c4ac-163">This means that you can grant a client limited permissions tooobjects in your storage account for a specified period of time and with a specified set of permissions, without having to share your account access keys.</span></span>

<span data-ttu-id="6c4ac-164">Olá passos seguintes mostram como toocreate uma SAS para um contentor do blob:</span><span class="sxs-lookup"><span data-stu-id="6c4ac-164">hello following steps illustrate how toocreate a SAS for a blob container:</span></span>

1. <span data-ttu-id="6c4ac-165">Abrir o Explorador de Armazenamento (Pré-visualização).</span><span class="sxs-lookup"><span data-stu-id="6c4ac-165">Open Storage Explorer (Preview).</span></span>
2. <span data-ttu-id="6c4ac-166">No painel esquerdo Olá, expanda a conta de armazenamento de Olá que contém o contentor de blob Olá para o qual pretende tooget uma SAS.</span><span class="sxs-lookup"><span data-stu-id="6c4ac-166">In hello left pane, expand hello storage account containing hello blob container for which you wish tooget a SAS.</span></span>
3. <span data-ttu-id="6c4ac-167">Expanda a conta de armazenamento a Olá **contentores de BLOBs**.</span><span class="sxs-lookup"><span data-stu-id="6c4ac-167">Expand hello storage account's **Blob Containers**.</span></span>
4. <span data-ttu-id="6c4ac-168">Clique no contentor de blob pretendido Olá e, no menu de contexto de Olá - selecione **obter assinatura de acesso partilhado**.</span><span class="sxs-lookup"><span data-stu-id="6c4ac-168">Right-click hello desired blob container, and - from hello context menu - select **Get Shared Access Signature**.</span></span>

   ![Obter o menu de contexto SAS][8]
5. <span data-ttu-id="6c4ac-170">No Olá **assinatura de acesso partilhado** caixa de diálogo, especificar a política de Olá, datas de início e de expiração, fuso horário e níveis de que pretende para recursos de Olá de acesso.</span><span class="sxs-lookup"><span data-stu-id="6c4ac-170">In hello **Shared Access Signature** dialog, specify hello policy, start and expiration dates, time zone, and access levels you want for hello resource.</span></span>

   ![Obter as opções de SAS][9]
6. <span data-ttu-id="6c4ac-172">Quando tiver terminado de especificar opções de SAS Olá, selecione **criar**.</span><span class="sxs-lookup"><span data-stu-id="6c4ac-172">When you're finished specifying hello SAS options, select **Create**.</span></span>
7. <span data-ttu-id="6c4ac-173">Um segundo **assinatura de acesso partilhado** caixa de diálogo, em seguida, irá apresentar que apresenta uma lista de Olá contentor de blob, juntamente com o URL de Olá e QueryStrings pode utilizar tooaccess Olá recursos de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="6c4ac-173">A second **Shared Access Signature** dialog will then display that lists hello blob container along with hello URL and QueryStrings you can use tooaccess hello storage resource.</span></span>
   <span data-ttu-id="6c4ac-174">Selecione **cópia** seguinte URL de toohello desejar área de transferência do toocopy toohello.</span><span class="sxs-lookup"><span data-stu-id="6c4ac-174">Select **Copy** next toohello URL you wish toocopy toohello clipboard.</span></span>

   ![Copie o URL SAS][10]
8. <span data-ttu-id="6c4ac-176">Quando terminar, selecione **Close (Fechar)**.</span><span class="sxs-lookup"><span data-stu-id="6c4ac-176">When done, select **Close**.</span></span>

## <a name="manage-access-policies-for-a-blob-container"></a><span data-ttu-id="6c4ac-177">Gerir políticas de acesso para um contentor do blob</span><span class="sxs-lookup"><span data-stu-id="6c4ac-177">Manage Access Policies for a blob container</span></span>
<span data-ttu-id="6c4ac-178">Olá passos seguintes mostram como toomanage (adicionar e remover) políticas para um contentor de BLOBs de acesso:</span><span class="sxs-lookup"><span data-stu-id="6c4ac-178">hello following steps illustrate how toomanage (add and remove) access policies for a blob container:</span></span>

1. <span data-ttu-id="6c4ac-179">Abrir o Explorador de Armazenamento (Pré-visualização).</span><span class="sxs-lookup"><span data-stu-id="6c4ac-179">Open Storage Explorer (Preview).</span></span>
2. <span data-ttu-id="6c4ac-180">No painel esquerdo Olá, expanda a conta de armazenamento de Olá que contém o contentor de BLOBs de Olá cujas políticas de acesso pretende toomanage.</span><span class="sxs-lookup"><span data-stu-id="6c4ac-180">In hello left pane, expand hello storage account containing hello blob container whose access policies you wish toomanage.</span></span>
3. <span data-ttu-id="6c4ac-181">Expanda a conta de armazenamento a Olá **contentores de BLOBs**.</span><span class="sxs-lookup"><span data-stu-id="6c4ac-181">Expand hello storage account's **Blob Containers**.</span></span>
4. <span data-ttu-id="6c4ac-182">Selecione o contentor de blob pretendido Olá e, no menu de contexto de Olá - selecione **gerir políticas de acesso**.</span><span class="sxs-lookup"><span data-stu-id="6c4ac-182">Select hello desired blob container, and - from hello context menu - select **Manage Access Policies**.</span></span>

   ![Menu de Contexto Gerir políticas de acesso][11]
5. <span data-ttu-id="6c4ac-184">Olá **políticas de acesso** apresentará uma caixa de diálogo lista quaisquer políticas de acesso já criadas para o contentor de blob selecionado Olá.</span><span class="sxs-lookup"><span data-stu-id="6c4ac-184">hello **Access Policies** dialog will list any access policies already created for hello selected blob container.</span></span>

   ![Opções de política de acesso][12]        
6. <span data-ttu-id="6c4ac-186">Siga estes passos, dependendo da tarefa de gestão de política de acesso de Olá:</span><span class="sxs-lookup"><span data-stu-id="6c4ac-186">Follow these steps depending on hello access policy management task:</span></span>

   * <span data-ttu-id="6c4ac-187">**Adicionar uma política de acesso nova** - selecione **Add (Adicionar)**.</span><span class="sxs-lookup"><span data-stu-id="6c4ac-187">**Add a new access policy** - Select **Add**.</span></span> <span data-ttu-id="6c4ac-188">Depois de o gerado, Olá **políticas de acesso** diálogo apresentará Olá recém-adicionada política (com as predefinições) de acesso.</span><span class="sxs-lookup"><span data-stu-id="6c4ac-188">Once generated, hello **Access Policies** dialog will display hello newly added access policy (with default settings).</span></span>
   * <span data-ttu-id="6c4ac-189">**Editar uma política de acesso** - efetue as edições pretendidas e selecione **guardar**.</span><span class="sxs-lookup"><span data-stu-id="6c4ac-189">**Edit an access policy** -  Make any desired edits, and select **Save**.</span></span>
   * <span data-ttu-id="6c4ac-190">**Remover uma política de acesso** - selecione **remover** próxima política de acesso de toohello desejar tooremove.</span><span class="sxs-lookup"><span data-stu-id="6c4ac-190">**Remove an access policy** - Select **Remove** next toohello access policy you wish tooremove.</span></span>

## <a name="set-hello-public-access-level-for-a-blob-container"></a><span data-ttu-id="6c4ac-191">Definir Olá nível de acesso público para um contentor do blob</span><span class="sxs-lookup"><span data-stu-id="6c4ac-191">Set hello Public Access Level for a blob container</span></span>
<span data-ttu-id="6c4ac-192">Por predefinição, cada contentor de blob está definido demasiado "Sem acesso de público".</span><span class="sxs-lookup"><span data-stu-id="6c4ac-192">By default, every blob container is set too"No public access".</span></span>

<span data-ttu-id="6c4ac-193">Olá passos seguintes mostram como toospecify um público de acesso ao nível para um contentor do blob.</span><span class="sxs-lookup"><span data-stu-id="6c4ac-193">hello following steps illustrate how toospecify a public access level for a blob container.</span></span>

1. <span data-ttu-id="6c4ac-194">Abrir o Explorador de Armazenamento (Pré-visualização).</span><span class="sxs-lookup"><span data-stu-id="6c4ac-194">Open Storage Explorer (Preview).</span></span>
2. <span data-ttu-id="6c4ac-195">No painel esquerdo Olá, expanda a conta de armazenamento de Olá que contém o contentor de BLOBs de Olá cujas políticas de acesso pretende toomanage.</span><span class="sxs-lookup"><span data-stu-id="6c4ac-195">In hello left pane, expand hello storage account containing hello blob container whose access policies you wish toomanage.</span></span>
3. <span data-ttu-id="6c4ac-196">Expanda a conta de armazenamento a Olá **contentores de BLOBs**.</span><span class="sxs-lookup"><span data-stu-id="6c4ac-196">Expand hello storage account's **Blob Containers**.</span></span>
4. <span data-ttu-id="6c4ac-197">Selecione o contentor de blob pretendido Olá e, no menu de contexto de Olá - selecione **definir o nível de acesso público**.</span><span class="sxs-lookup"><span data-stu-id="6c4ac-197">Select hello desired blob container, and - from hello context menu - select **Set Public Access Level**.</span></span>

   ![Defina o menu de contexto de nível de acesso público][13]
5. <span data-ttu-id="6c4ac-199">No Olá **definido ao nível do contentor acesso público** caixa de diálogo, especifique o nível de acesso de Olá assim o desejar.</span><span class="sxs-lookup"><span data-stu-id="6c4ac-199">In hello **Set Container Public Access Level** dialog, specify hello desired access level.</span></span>

   ![Definir opções de nível de acesso público][14]
6. <span data-ttu-id="6c4ac-201">Selecione **Aplicar**.</span><span class="sxs-lookup"><span data-stu-id="6c4ac-201">Select **Apply**.</span></span>

## <a name="managing-blobs-in-a-blob-container"></a><span data-ttu-id="6c4ac-202">Gerir os blobs num contentor de blob</span><span class="sxs-lookup"><span data-stu-id="6c4ac-202">Managing blobs in a blob container</span></span>
<span data-ttu-id="6c4ac-203">Depois de criar um contentor de blob, pode carregar um contentor de blob do blob toothat, transferir um computador local do blob tooyour, abra um blob no seu computador local e muito mais.</span><span class="sxs-lookup"><span data-stu-id="6c4ac-203">Once you've created a blob container, you can upload a blob toothat blob container, download a blob tooyour local computer, open a blob on your local computer, and much more.</span></span>

<span data-ttu-id="6c4ac-204">Olá, os passos seguintes mostram como toomanage Olá blobs (e pastas) dentro de um contentor do blob.</span><span class="sxs-lookup"><span data-stu-id="6c4ac-204">hello following steps illustrate how toomanage hello blobs (and folders) within a blob container.</span></span>

1. <span data-ttu-id="6c4ac-205">Abrir o Explorador de Armazenamento (Pré-visualização).</span><span class="sxs-lookup"><span data-stu-id="6c4ac-205">Open Storage Explorer (Preview).</span></span>
2. <span data-ttu-id="6c4ac-206">No painel esquerdo Olá, expanda a conta de armazenamento de Olá que contém o contentor de blob Olá desejar toomanage.</span><span class="sxs-lookup"><span data-stu-id="6c4ac-206">In hello left pane, expand hello storage account containing hello blob container you wish toomanage.</span></span>
3. <span data-ttu-id="6c4ac-207">Expanda a conta de armazenamento a Olá **contentores de BLOBs**.</span><span class="sxs-lookup"><span data-stu-id="6c4ac-207">Expand hello storage account's **Blob Containers**.</span></span>
4. <span data-ttu-id="6c4ac-208">Faça duplo clique de contentor do blob Olá desejar tooview.</span><span class="sxs-lookup"><span data-stu-id="6c4ac-208">Double-click hello blob container you wish tooview.</span></span>
5. <span data-ttu-id="6c4ac-209">painel principal Olá apresentará o conteúdo do contentor de blob Olá.</span><span class="sxs-lookup"><span data-stu-id="6c4ac-209">hello main pane will display hello blob container's contents.</span></span>

   ![Contentor de BLOBs de vista][3]
6. <span data-ttu-id="6c4ac-211">painel principal Olá apresentará o conteúdo do contentor de blob Olá.</span><span class="sxs-lookup"><span data-stu-id="6c4ac-211">hello main pane will display hello blob container's contents.</span></span>
7. <span data-ttu-id="6c4ac-212">Siga estes que passos, dependendo das tarefas de Olá desejar tooperform:</span><span class="sxs-lookup"><span data-stu-id="6c4ac-212">Follow these steps depending on hello task you wish tooperform:</span></span>

   * <span data-ttu-id="6c4ac-213">**Carregar o contentor de BLOBs de tooa de ficheiros**</span><span class="sxs-lookup"><span data-stu-id="6c4ac-213">**Upload files tooa blob container**</span></span>

     1. <span data-ttu-id="6c4ac-214">Na barra de ferramentas do painel Olá principal, selecione **carregar**e, em seguida, **carregar ficheiros** no menu de Olá pendente.</span><span class="sxs-lookup"><span data-stu-id="6c4ac-214">On hello main pane's toolbar, select **Upload**, and then **Upload Files** from hello drop-down menu.</span></span>

        ![Carregar o menu de ficheiros][15]
     2. <span data-ttu-id="6c4ac-216">No Olá **carregar ficheiros** caixa de diálogo, reticências Olá selecione (**...** ) botão no lado direito de Olá de Olá **ficheiros** tooselect Olá ficheiros pretende tooupload de caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="6c4ac-216">In hello **Upload files** dialog, select hello ellipsis (**…**) button on hello right side of hello **Files** text box tooselect hello file(s) you wish tooupload.</span></span>

        ![Opções de ficheiros de carregamento][16]
     3. <span data-ttu-id="6c4ac-218">Especifique o tipo Olá de **Blob tipo**.</span><span class="sxs-lookup"><span data-stu-id="6c4ac-218">Specify hello type of **Blob type**.</span></span> <span data-ttu-id="6c4ac-219">artigo de Olá [introdução ao Blob storage do Azure através do .NET](storage/blobs/storage-dotnet-how-to-use-blobs.md#blob-service-concepts) explica Olá as diferenças entre Olá vários tipos de Blobs.</span><span class="sxs-lookup"><span data-stu-id="6c4ac-219">hello article [Get started with Azure Blob storage using .NET](storage/blobs/storage-dotnet-how-to-use-blobs.md#blob-service-concepts) explains hello differences between hello various blob types.</span></span>
     4. <span data-ttu-id="6c4ac-220">Opcionalmente, especifique uma pasta de destino no qual os ficheiros selecionados Olá serão carregados.</span><span class="sxs-lookup"><span data-stu-id="6c4ac-220">Optionally, specify a target folder into which hello selected file(s) will be uploaded.</span></span> <span data-ttu-id="6c4ac-221">Se a pasta de destino Olá não existir, será criado.</span><span class="sxs-lookup"><span data-stu-id="6c4ac-221">If hello target folder doesn’t exist, it will be created.</span></span>
     5. <span data-ttu-id="6c4ac-222">Selecione **Upload**.</span><span class="sxs-lookup"><span data-stu-id="6c4ac-222">Select **Upload**.</span></span>
   * <span data-ttu-id="6c4ac-223">**Carregar um contentor do blob tooa pasta**</span><span class="sxs-lookup"><span data-stu-id="6c4ac-223">**Upload a folder tooa blob container**</span></span>

     1. <span data-ttu-id="6c4ac-224">Na barra de ferramentas do painel Olá principal, selecione **carregar**e, em seguida, **carregar pasta** no menu de Olá pendente.</span><span class="sxs-lookup"><span data-stu-id="6c4ac-224">On hello main pane's toolbar, select **Upload**, and then **Upload Folder** from hello drop-down menu.</span></span>

        ![Menu Carregar pasta][17]
     2. <span data-ttu-id="6c4ac-226">No Olá **carregamento pasta** caixa de diálogo, reticências Olá selecione (**...** ) botão no lado direito de Olá de Olá **pasta** pasta de Olá de tooselect de caixa de texto cujo conteúdo pretende tooupload.</span><span class="sxs-lookup"><span data-stu-id="6c4ac-226">In hello **Upload folder** dialog, select hello ellipsis (**…**) button on hello right side of hello **Folder** text box tooselect hello folder whose contents you wish tooupload.</span></span>

        ![Carregue as opções de pastas][18]
     3. <span data-ttu-id="6c4ac-228">Especifique o tipo Olá de **Blob tipo**.</span><span class="sxs-lookup"><span data-stu-id="6c4ac-228">Specify hello type of **Blob type**.</span></span> <span data-ttu-id="6c4ac-229">artigo de Olá [introdução ao Blob storage do Azure através do .NET](storage/blobs/storage-dotnet-how-to-use-blobs.md#blob-service-concepts) explica Olá as diferenças entre Olá vários tipos de Blobs.</span><span class="sxs-lookup"><span data-stu-id="6c4ac-229">hello article [Get started with Azure Blob storage using .NET](storage/blobs/storage-dotnet-how-to-use-blobs.md#blob-service-concepts) explains hello differences between hello various blob types.</span></span>
     4. <span data-ttu-id="6c4ac-230">Opcionalmente, especifique uma pasta de destino no qual Olá conteúdo da pasta selecionado será carregado.</span><span class="sxs-lookup"><span data-stu-id="6c4ac-230">Optionally, specify a target folder into which hello selected folder's contents will be uploaded.</span></span> <span data-ttu-id="6c4ac-231">Se a pasta de destino Olá não existir, será criado.</span><span class="sxs-lookup"><span data-stu-id="6c4ac-231">If hello target folder doesn’t exist, it will be created.</span></span>
     5. <span data-ttu-id="6c4ac-232">Selecione **Upload**.</span><span class="sxs-lookup"><span data-stu-id="6c4ac-232">Select **Upload**.</span></span>
   * <span data-ttu-id="6c4ac-233">**Transferir o computador local blob tooyour**</span><span class="sxs-lookup"><span data-stu-id="6c4ac-233">**Download a blob tooyour local computer**</span></span>

     1. <span data-ttu-id="6c4ac-234">Selecione o blob Olá desejar toodownload.</span><span class="sxs-lookup"><span data-stu-id="6c4ac-234">Select hello blob you wish toodownload.</span></span>
     2. <span data-ttu-id="6c4ac-235">Na barra de ferramentas do painel Olá principal, selecione **transferir**.</span><span class="sxs-lookup"><span data-stu-id="6c4ac-235">On hello main pane's toolbar, select **Download**.</span></span>
     3. <span data-ttu-id="6c4ac-236">No Olá **Especifique qual toosave Olá transferidos blob** caixa de diálogo, especifique onde pretende que o blob Olá transferido de localização de Olá e Olá nome desejar toogive-lo.</span><span class="sxs-lookup"><span data-stu-id="6c4ac-236">In hello **Specify where toosave hello downloaded blob** dialog, specify hello location where you want hello blob downloaded, and hello name you wish toogive it.</span></span>  
     4. <span data-ttu-id="6c4ac-237">Selecione **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="6c4ac-237">Select **Save**.</span></span>
   * <span data-ttu-id="6c4ac-238">**Abra um blob no seu computador local**</span><span class="sxs-lookup"><span data-stu-id="6c4ac-238">**Open a blob on your local computer**</span></span>

     1. <span data-ttu-id="6c4ac-239">Selecione o blob Olá desejar tooopen.</span><span class="sxs-lookup"><span data-stu-id="6c4ac-239">Select hello blob you wish tooopen.</span></span>
     2. <span data-ttu-id="6c4ac-240">Na barra de ferramentas do painel Olá principal, selecione **abra**.</span><span class="sxs-lookup"><span data-stu-id="6c4ac-240">On hello main pane's toolbar, select **Open**.</span></span>
     3. <span data-ttu-id="6c4ac-241">blob Olá será transferida e aberta utilizando a aplicação Olá associada ao tipo de ficheiro do blob Olá subjacente.</span><span class="sxs-lookup"><span data-stu-id="6c4ac-241">hello blob will be downloaded and opened using hello application associated with hello blob's underlying file type.</span></span>
   * <span data-ttu-id="6c4ac-242">**Copiar uma área de transferência do blob toohello**</span><span class="sxs-lookup"><span data-stu-id="6c4ac-242">**Copy a blob toohello clipboard**</span></span>

     1. <span data-ttu-id="6c4ac-243">Selecione o blob Olá desejar toocopy.</span><span class="sxs-lookup"><span data-stu-id="6c4ac-243">Select hello blob you wish toocopy.</span></span>
     2. <span data-ttu-id="6c4ac-244">Na barra de ferramentas do painel Olá principal, selecione **cópia**.</span><span class="sxs-lookup"><span data-stu-id="6c4ac-244">On hello main pane's toolbar, select **Copy**.</span></span>
     3. <span data-ttu-id="6c4ac-245">No painel esquerdo Olá, navegue tooanother contentor de blob e faça duplo clique tooview-lo no painel principal Olá.</span><span class="sxs-lookup"><span data-stu-id="6c4ac-245">In hello left pane, navigate tooanother blob container, and double-click it tooview it in hello main pane.</span></span>
     4. <span data-ttu-id="6c4ac-246">Na barra de ferramentas do painel Olá principal, selecione **colar** toocreate uma cópia do blob Olá.</span><span class="sxs-lookup"><span data-stu-id="6c4ac-246">On hello main pane's toolbar, select **Paste** toocreate a copy of hello blob.</span></span>
   * <span data-ttu-id="6c4ac-247">**Eliminar um blob**</span><span class="sxs-lookup"><span data-stu-id="6c4ac-247">**Delete a blob**</span></span>

     1. <span data-ttu-id="6c4ac-248">Selecione o blob Olá desejar toodelete.</span><span class="sxs-lookup"><span data-stu-id="6c4ac-248">Select hello blob you wish toodelete.</span></span>
     2. <span data-ttu-id="6c4ac-249">Na barra de ferramentas do painel Olá principal, selecione **eliminar**.</span><span class="sxs-lookup"><span data-stu-id="6c4ac-249">On hello main pane's toolbar, select **Delete**.</span></span>
     3. <span data-ttu-id="6c4ac-250">Selecione **Sim** toohello diálogo de confirmação.</span><span class="sxs-lookup"><span data-stu-id="6c4ac-250">Select **Yes** toohello confirmation dialog.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6c4ac-251">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="6c4ac-251">Next steps</span></span>
* <span data-ttu-id="6c4ac-252">Olá vista [mais recente notas de versão do Explorador de armazenamento (pré-visualização) e vídeos](http://www.storageexplorer.com).</span><span class="sxs-lookup"><span data-stu-id="6c4ac-252">View hello [latest Storage Explorer (Preview) release notes and videos](http://www.storageexplorer.com).</span></span>
* <span data-ttu-id="6c4ac-253">Saiba como demasiado[criar aplicações utilizar blobs do Azure, tabelas, filas e os ficheiros](https://azure.microsoft.com/documentation/services/storage/).</span><span class="sxs-lookup"><span data-stu-id="6c4ac-253">Learn how too[create applications using Azure blobs, tables, queues, and files](https://azure.microsoft.com/documentation/services/storage/).</span></span>

[0]: ./media/vs-azure-tools-storage-explorer-blobs/blob-containers-create-context-menu.png
[1]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-create.png
[2]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-create-done.png
[3]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-editor.png
[4]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-delete-context-menu.png
[5]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-delete-confirmation.png
[6]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-copy-context-menu.png
[7]: ./media/vs-azure-tools-storage-explorer-blobs/blob-containers-paste-context-menu.png
[8]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-get-sas-context-menu.png
[9]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-get-sas-options.png
[10]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-get-sas-urls.png
[11]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-manage-access-policies-context-menu.png
[12]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-manage-access-policies-options.png
[13]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-set-public-access-level-context-menu.png
[14]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-set-public-access-level-options.png
[15]: ./media/vs-azure-tools-storage-explorer-blobs/blob-upload-files-menu.png
[16]: ./media/vs-azure-tools-storage-explorer-blobs/blob-upload-files-options.png
[17]: ./media/vs-azure-tools-storage-explorer-blobs/blob-upload-folder-menu.png
[18]: ./media/vs-azure-tools-storage-explorer-blobs/blob-upload-folder-options.png
[19]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-open-editor-context-menu.png
