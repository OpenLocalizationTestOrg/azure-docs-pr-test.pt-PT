---
title: "aaaCreate uma conta do Batch no portal do Azure de Olá | Microsoft Docs"
description: "Saiba como toocreate um Azure Batch conta no Olá toorun portal do Azure, cargas de trabalho paralelas em grande escala na nuvem de Olá"
services: batch
documentationcenter: 
author: tamram
manager: timlt
editor: 
ms.assetid: 3fbae545-245f-4c66-aee2-e25d7d5d36db
ms.service: batch
ms.workload: big-compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/20/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 2176f88ba0a1a3298023de8f520d46ef28a664b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-batch-account-with-hello-azure-portal"></a><span data-ttu-id="3c419-103">Criar uma conta do Batch com Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="3c419-103">Create a Batch account with hello Azure portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="3c419-104">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="3c419-104">Azure portal</span></span>](batch-account-create-portal.md)
> * [<span data-ttu-id="3c419-105">Gestão de Batch .NET</span><span class="sxs-lookup"><span data-stu-id="3c419-105">Batch Management .NET</span></span>](batch-management-dotnet.md)
>
>

<span data-ttu-id="3c419-106">Saiba como toocreate um Azure Batch conta no Olá [portal do Azure][azure_portal]e escolha as propriedades da conta de Olá que se adeque ao seu cenário de computação.</span><span class="sxs-lookup"><span data-stu-id="3c419-106">Learn how toocreate an Azure Batch account in hello [Azure portal][azure_portal], and choose hello account properties that fit your compute scenario.</span></span> <span data-ttu-id="3c419-107">Saiba onde toofind propriedades da conta de importante que as chaves de acesso e os URLs de conta.</span><span class="sxs-lookup"><span data-stu-id="3c419-107">Learn where toofind important account properties like access keys and account URLs.</span></span>

<span data-ttu-id="3c419-108">Para fundo sobre cenários e de contas do Batch, consulte Olá [descrição geral da funcionalidade](batch-api-basics.md).</span><span class="sxs-lookup"><span data-stu-id="3c419-108">For background about Batch accounts and scenarios, see hello [feature overview](batch-api-basics.md).</span></span>



## <a name="create-a-batch-account"></a><span data-ttu-id="3c419-109">Criar uma conta do Batch</span><span class="sxs-lookup"><span data-stu-id="3c419-109">Create a Batch account</span></span>

<span data-ttu-id="3c419-110">Utilize um dos Olá dois Olá portal toocreate uma conta do Batch *modos de alocação de conjunto*: **serviço Batch** modo ou Olá mais recente **subscrição de utilizador** modo, o que requer mais configuração.</span><span class="sxs-lookup"><span data-stu-id="3c419-110">Use hello portal toocreate a Batch account in one of hello two *pool allocation modes*: **Batch service** mode or hello newer **user subscription** mode, which requires more configuration.</span></span> <span data-ttu-id="3c419-111">Para obter informações sobre estes dois modos, consulte Olá [descrição geral da funcionalidade](batch-api-basics.md#account).</span><span class="sxs-lookup"><span data-stu-id="3c419-111">For information about these two modes, see hello [feature overview](batch-api-basics.md#account).</span></span> <span data-ttu-id="3c419-112">Para funcionalidades do modo de subscrição de utilizador Olá, consulte também Olá [blogue](https://blogs.technet.microsoft.com/windowshpc/2017/03/17/azure-batch-vnet-and-custom-image-support-for-virtual-machine-pools/).</span><span class="sxs-lookup"><span data-stu-id="3c419-112">For features of hello user subscription mode, see also hello [blog post](https://blogs.technet.microsoft.com/windowshpc/2017/03/17/azure-batch-vnet-and-custom-image-support-for-virtual-machine-pools/).</span></span>

## <a name="batch-service-mode"></a><span data-ttu-id="3c419-113">Modo de serviço do Batch</span><span class="sxs-lookup"><span data-stu-id="3c419-113">Batch service mode</span></span>



1. <span data-ttu-id="3c419-114">Inicie sessão no toohello [portal do Azure][azure_portal].</span><span class="sxs-lookup"><span data-stu-id="3c419-114">Sign in toohello [Azure portal][azure_portal].</span></span>
2. <span data-ttu-id="3c419-115">Clique em **Novo** > **Computação** > **Serviço Batch**.</span><span class="sxs-lookup"><span data-stu-id="3c419-115">Click **New** > **Compute** > **Batch Service**.</span></span>

    ![Batch no Olá Marketplace][marketplace_portal]
3. <span data-ttu-id="3c419-117">Olá **nova conta do Batch** é apresentado o painel.</span><span class="sxs-lookup"><span data-stu-id="3c419-117">hello **New Batch Account** blade is displayed.</span></span> <span data-ttu-id="3c419-118">Consulte as descrições de Olá abaixo de cada elemento do painel.</span><span class="sxs-lookup"><span data-stu-id="3c419-118">See hello descriptions below of each blade element.</span></span>

    ![Criar uma conta do Batch][account_portal]

    <span data-ttu-id="3c419-120">a.</span><span class="sxs-lookup"><span data-stu-id="3c419-120">a.</span></span> <span data-ttu-id="3c419-121">**Nome da conta**: nome da conta de Batch de Olá que escolher tem de ser exclusivo num Olá região do Azure onde será criada a conta de Olá (consulte **localização** abaixo).</span><span class="sxs-lookup"><span data-stu-id="3c419-121">**Account name**: hello Batch account name you choose must be unique within hello Azure region where hello account is created (see **Location** below).</span></span> <span data-ttu-id="3c419-122">o nome de conta Olá pode conter apenas carateres em minúsculas ou números e tem de ser 3 e 24 carateres de comprimento.</span><span class="sxs-lookup"><span data-stu-id="3c419-122">hello account name may contain only lowercase characters or numbers, and must be 3-24 characters in length.</span></span>

    <span data-ttu-id="3c419-123">b.</span><span class="sxs-lookup"><span data-stu-id="3c419-123">b.</span></span> <span data-ttu-id="3c419-124">**Subscrição**: Olá subscrição na qual Olá toocreate conta do Batch.</span><span class="sxs-lookup"><span data-stu-id="3c419-124">**Subscription**: hello subscription in which toocreate hello Batch account.</span></span> <span data-ttu-id="3c419-125">Se tiver apenas uma subscrição, está selecionada por predefinição.</span><span class="sxs-lookup"><span data-stu-id="3c419-125">If you have only one subscription, it is selected by default.</span></span>

    <span data-ttu-id="3c419-126">c.</span><span class="sxs-lookup"><span data-stu-id="3c419-126">c.</span></span> <span data-ttu-id="3c419-127">**Modo de alocação do conjunto**: selecione **serviço do Batch**.</span><span class="sxs-lookup"><span data-stu-id="3c419-127">**Pool allocation mode**: Select **Batch service**.</span></span>

    <span data-ttu-id="3c419-128">c.</span><span class="sxs-lookup"><span data-stu-id="3c419-128">c.</span></span> <span data-ttu-id="3c419-129">**Grupo de recursos**: selecione um grupo de recursos existente para a sua nova conta do Batch ou, opcionalmente, para criar um novo.</span><span class="sxs-lookup"><span data-stu-id="3c419-129">**Resource group**: Select an existing resource group for your new Batch account, or optionally create a new one.</span></span>

    <span data-ttu-id="3c419-130">d.</span><span class="sxs-lookup"><span data-stu-id="3c419-130">d.</span></span> <span data-ttu-id="3c419-131">**Localização**: Olá região do Azure na qual Olá toocreate conta do Batch.</span><span class="sxs-lookup"><span data-stu-id="3c419-131">**Location**: hello Azure region in which toocreate hello Batch account.</span></span> <span data-ttu-id="3c419-132">Apenas as regiões Olá suportadas pela sua subscrição e o grupo de recursos são apresentadas como opções.</span><span class="sxs-lookup"><span data-stu-id="3c419-132">Only hello regions supported by your subscription and resource group are displayed as options.</span></span>

    <span data-ttu-id="3c419-133">e.</span><span class="sxs-lookup"><span data-stu-id="3c419-133">e.</span></span> <span data-ttu-id="3c419-134">**Conta de armazenamento** (opcional): uma conta de Armazenamento do Azure para fins gerais que associa à conta do Batch.</span><span class="sxs-lookup"><span data-stu-id="3c419-134">**Storage account** (optional): A general-purpose Azure Storage account that you associate with your Batch account.</span></span> <span data-ttu-id="3c419-135">Esta opção é recomendada para a maioria das contas do Batch.</span><span class="sxs-lookup"><span data-stu-id="3c419-135">This is recommended for most Batch accounts.</span></span> <span data-ttu-id="3c419-136">Veja [Linked Azure Storage account (Conta do Armazenamento do Azure Ligada)](#linked-azure-storage-account) mais tarde neste artigo para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="3c419-136">See [Linked Azure Storage account](#linked-azure-storage-account) later in this article for more details.</span></span>

4. <span data-ttu-id="3c419-137">Clique em **criar** conta de Olá toocreate.</span><span class="sxs-lookup"><span data-stu-id="3c419-137">Click **Create** toocreate hello account.</span></span>

   <span data-ttu-id="3c419-138">portal de Olá indica a implementação está em curso.</span><span class="sxs-lookup"><span data-stu-id="3c419-138">hello portal indicates deployment is in progress.</span></span> <span data-ttu-id="3c419-139">Após a conclusão, aparece a notificação **Implementações concluídas com êxito** em **Notificações**.</span><span class="sxs-lookup"><span data-stu-id="3c419-139">Upon completion, a **Deployments succeeded** notification appears in **Notifications**.</span></span>

## <a name="user-subscription-mode"></a><span data-ttu-id="3c419-140">Modo de subscrição do utilizador</span><span class="sxs-lookup"><span data-stu-id="3c419-140">User subscription mode</span></span>

### <a name="allow-azure-batch-tooaccess-hello-subscription-one-time-operation"></a><span data-ttu-id="3c419-141">Permitir que o Azure Batch tooaccess subscrição Olá (operação única)</span><span class="sxs-lookup"><span data-stu-id="3c419-141">Allow Azure Batch tooaccess hello subscription (one-time operation)</span></span>
<span data-ttu-id="3c419-142">Ao criar a sua conta do Batch primeiro no modo de subscrição de utilizador, efetue Olá tooregister passos a seguir a sua subscrição com o Batch.</span><span class="sxs-lookup"><span data-stu-id="3c419-142">When creating your first Batch account in user subscription mode, perform hello following steps tooregister your subscription with Batch.</span></span> <span data-ttu-id="3c419-143">(Se fez anteriormente isto, ignorar a secção seguinte toohello.)</span><span class="sxs-lookup"><span data-stu-id="3c419-143">(If you previously did this, skip toohello next section.)</span></span>

1. <span data-ttu-id="3c419-144">Inicie sessão no toohello [portal do Azure][azure_portal].</span><span class="sxs-lookup"><span data-stu-id="3c419-144">Sign in toohello [Azure portal][azure_portal].</span></span>

2. <span data-ttu-id="3c419-145">Clique em **mais serviços** > **subscrições**e clique em subscrição Olá pretende toouse para Olá conta do Batch.</span><span class="sxs-lookup"><span data-stu-id="3c419-145">Click **More Services** > **Subscriptions**, and click hello subscription you want toouse for hello Batch account.</span></span>

3. <span data-ttu-id="3c419-146">No Olá **subscrição** painel, clique em **(IAM) do controlo de acesso** > **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="3c419-146">In hello **Subscription** blade, click **Access control (IAM)** > **Add**.</span></span>

    ![Controlo de acesso da subscrição][subscription_access]

4. <span data-ttu-id="3c419-148">No Olá **adicionar permissões** painel, selecione de Olá **contribuinte** função, procure Olá API do Batch.</span><span class="sxs-lookup"><span data-stu-id="3c419-148">On hello **Add permissions** blade, select hello **Contributor** role, search for hello Batch API.</span></span> <span data-ttu-id="3c419-149">Pesquisa para cada um destas cadeias até encontrar Olá API:</span><span class="sxs-lookup"><span data-stu-id="3c419-149">Search for each of these strings until you find hello API:</span></span>
    1. <span data-ttu-id="3c419-150">**MicrosoftAzureBatch**.</span><span class="sxs-lookup"><span data-stu-id="3c419-150">**MicrosoftAzureBatch**.</span></span>
    2. <span data-ttu-id="3c419-151">**Batch do Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="3c419-151">**Microsoft Azure Batch**.</span></span> <span data-ttu-id="3c419-152">Os inquilinos mais recentes podem utilizar este nome.</span><span class="sxs-lookup"><span data-stu-id="3c419-152">Newer Azure AD tenants may use this name.</span></span>
    3. <span data-ttu-id="3c419-153">**ddbf3205-c6bd-46ae-8127-60eb93363864** Olá ID para Olá API do Batch.</span><span class="sxs-lookup"><span data-stu-id="3c419-153">**ddbf3205-c6bd-46ae-8127-60eb93363864** is hello ID for hello Batch API.</span></span> 

5. <span data-ttu-id="3c419-154">Depois de encontrar Olá API do Batch, selecione-o e clique em **guardar**.</span><span class="sxs-lookup"><span data-stu-id="3c419-154">Once you find hello Batch API, select it and click **Save**.</span></span>

    ![Adicionar permissões do Batch][add_permission]

### <a name="create-a-key-vault"></a><span data-ttu-id="3c419-156">Criar um cofre de chaves</span><span class="sxs-lookup"><span data-stu-id="3c419-156">Create a key vault</span></span>
<span data-ttu-id="3c419-157">No modo de subscrição de utilizador, é necessário um cofre de chaves do Azure que pertence toothe mesmo grupo de recursos como toobe de conta de Batch de Olá criado.</span><span class="sxs-lookup"><span data-stu-id="3c419-157">In user subscription mode, an Azure key vault is required that belongs toothe same resource group as hello Batch account toobe created.</span></span> <span data-ttu-id="3c419-158">Certifique-se de grupo de recursos de Olá numa região onde está o Batch [disponíveis](https://azure.microsoft.com/regions/services/) e que suporta a sua subscrição.</span><span class="sxs-lookup"><span data-stu-id="3c419-158">Make sure hello resource group is in a region where Batch is [available](https://azure.microsoft.com/regions/services/) and which your subscription supports.</span></span>

1. <span data-ttu-id="3c419-159">No Olá [portal do Azure][azure_portal], clique em **novo** > **segurança + identidade** > **Cofre de chaves** .</span><span class="sxs-lookup"><span data-stu-id="3c419-159">In hello [Azure portal][azure_portal], click **New** > **Security + Identity** > **Key Vault**.</span></span>

2. <span data-ttu-id="3c419-160">No Olá **criar Cofre de chaves** painel, introduza um nome para o Cofre de chaves Olá e criar um grupo de recursos na região de Olá que pretende para a sua conta do Batch.</span><span class="sxs-lookup"><span data-stu-id="3c419-160">In hello **Create Key Vault** blade, enter a name for hello key vault, and create a resource group in hello region you want for your Batch account.</span></span> <span data-ttu-id="3c419-161">Deixe Olá restantes definições em valores predefinidos, em seguida, clique em **criar**.</span><span class="sxs-lookup"><span data-stu-id="3c419-161">Leave hello remaining settings at default values, then click **Create**.</span></span>

### <a name="create-a-batch-account"></a><span data-ttu-id="3c419-162">Criar uma conta do Batch</span><span class="sxs-lookup"><span data-stu-id="3c419-162">Create a Batch account</span></span>

1. <span data-ttu-id="3c419-163">No Olá [portal do Azure][azure_portal], clique em **novo** > **computação** > **deserviçodeBatch**.</span><span class="sxs-lookup"><span data-stu-id="3c419-163">In hello [Azure portal][azure_portal], click **New** > **Compute** > **Batch Service**.</span></span>

    ![Batch no Olá Marketplace][marketplace_portal]
3. <span data-ttu-id="3c419-165">Olá **nova conta do Batch** é apresentado o painel.</span><span class="sxs-lookup"><span data-stu-id="3c419-165">hello **New Batch Account** blade is displayed.</span></span> <span data-ttu-id="3c419-166">Consulte as descrições de Olá abaixo de cada elemento do painel.</span><span class="sxs-lookup"><span data-stu-id="3c419-166">See hello descriptions below of each blade element.</span></span>

    ![Criar uma conta do Batch][account_portal_byos]

    <span data-ttu-id="3c419-168">a.</span><span class="sxs-lookup"><span data-stu-id="3c419-168">a.</span></span> <span data-ttu-id="3c419-169">**Nome da conta**: nome da conta de Batch de Olá que escolher tem de ser exclusivo num Olá região do Azure onde será criada a conta de Olá (consulte **localização** abaixo).</span><span class="sxs-lookup"><span data-stu-id="3c419-169">**Account name**: hello Batch account name you choose must be unique within hello Azure region where hello account is created (see **Location** below).</span></span> <span data-ttu-id="3c419-170">o nome de conta Olá pode conter apenas carateres em minúsculas ou números e tem de ser 3 e 24 carateres de comprimento.</span><span class="sxs-lookup"><span data-stu-id="3c419-170">hello account name may contain only lowercase characters or numbers, and must be 3-24 characters in length.</span></span>

    <span data-ttu-id="3c419-171">b.</span><span class="sxs-lookup"><span data-stu-id="3c419-171">b.</span></span> <span data-ttu-id="3c419-172">**Subscrição**: Se tiver mais do que uma subscrição, selecione a subscrição de Olá que registado Olá serviço Batch.</span><span class="sxs-lookup"><span data-stu-id="3c419-172">**Subscription**: If you have more than one subscription, select hello subscription that you registered with hello Batch service.</span></span>

    <span data-ttu-id="3c419-173">c.</span><span class="sxs-lookup"><span data-stu-id="3c419-173">c.</span></span> <span data-ttu-id="3c419-174">**Modo de alocação do conjunto**: selecione **Subscrição do utilizador**.</span><span class="sxs-lookup"><span data-stu-id="3c419-174">**Pool allocation mode**: Select **User subscription**.</span></span>

    <span data-ttu-id="3c419-175">d.</span><span class="sxs-lookup"><span data-stu-id="3c419-175">d.</span></span> <span data-ttu-id="3c419-176">**Cofre da chave**: o Cofre de chaves Olá selecione que criou para a sua conta do Batch na secção anterior Olá.</span><span class="sxs-lookup"><span data-stu-id="3c419-176">**Key vault**: Select hello key vault you created for your Batch account in hello previous section.</span></span> <span data-ttu-id="3c419-177">Opcionalmente, crie um novo cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="3c419-177">Optionally, create a new key vault.</span></span> <span data-ttu-id="3c419-178">Depois de selecionar o Cofre de Olá, selecione Olá caixa de verificação toogrant do Azure Batch acesso toohello Cofre de chave.</span><span class="sxs-lookup"><span data-stu-id="3c419-178">After selecting hello vault, select hello checkbox toogrant Azure Batch access toohello key vault.</span></span>

    <span data-ttu-id="3c419-179">c.</span><span class="sxs-lookup"><span data-stu-id="3c419-179">c.</span></span> <span data-ttu-id="3c419-180">**Grupo de recursos**: grupo de recursos de Olá selecione onde criou o Cofre de chaves Olá.</span><span class="sxs-lookup"><span data-stu-id="3c419-180">**Resource group**: Select hello resource group in which you  created hello key vault.</span></span>

    <span data-ttu-id="3c419-181">d.</span><span class="sxs-lookup"><span data-stu-id="3c419-181">d.</span></span> <span data-ttu-id="3c419-182">**Localização**: Olá região do Azure onde criou o Cofre de chaves Olá Olá conta de Batch.</span><span class="sxs-lookup"><span data-stu-id="3c419-182">**Location**: hello Azure region in which you created hello key vault for hello Batch account.</span></span>

    <span data-ttu-id="3c419-183">e.</span><span class="sxs-lookup"><span data-stu-id="3c419-183">e.</span></span> <span data-ttu-id="3c419-184">**Conta de armazenamento** (opcional): uma conta de Armazenamento do Azure para fins gerais que associa à conta do Batch.</span><span class="sxs-lookup"><span data-stu-id="3c419-184">**Storage account** (optional): A general-purpose Azure Storage account that you associate with your Batch account.</span></span> <span data-ttu-id="3c419-185">Esta opção é recomendada para a maioria das contas do Batch.</span><span class="sxs-lookup"><span data-stu-id="3c419-185">This is recommended for most Batch accounts.</span></span> <span data-ttu-id="3c419-186">Veja [Conta do Armazenamento do Azure Ligada](#linked-azure-storage-account), abaixo, para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="3c419-186">See [Linked Azure Storage account](#linked-azure-storage-account) below for more details.</span></span>

4. <span data-ttu-id="3c419-187">Clique em **criar** conta de Olá toocreate.</span><span class="sxs-lookup"><span data-stu-id="3c419-187">Click **Create** toocreate hello account.</span></span>

   <span data-ttu-id="3c419-188">portal de Olá indica a implementação está em curso.</span><span class="sxs-lookup"><span data-stu-id="3c419-188">hello portal indicates deployment is in progress.</span></span> <span data-ttu-id="3c419-189">Após a conclusão, aparece a notificação **Implementações concluídas com êxito** em **Notificações**.</span><span class="sxs-lookup"><span data-stu-id="3c419-189">Upon completion, a **Deployments succeeded** notification appears in **Notifications**.</span></span>



## <a name="view-batch-account-properties"></a><span data-ttu-id="3c419-190">Ver propriedades da conta do Batch</span><span class="sxs-lookup"><span data-stu-id="3c419-190">View Batch account properties</span></span>
<span data-ttu-id="3c419-191">Quando tiver sido criada a conta de Olá, pode abrir Olá **painel de conta do Batch** tooaccess respetivas propriedades e definições.</span><span class="sxs-lookup"><span data-stu-id="3c419-191">Once hello account has been created, you can open hello **Batch account blade** tooaccess its settings and properties.</span></span> <span data-ttu-id="3c419-192">Pode aceder a todas as definições de conta e as propriedades utilizando o menu à esquerda do Olá do painel de conta de Batch de Olá.</span><span class="sxs-lookup"><span data-stu-id="3c419-192">You can access all account settings and properties by using hello left menu of hello Batch account blade.</span></span>

![Painel Conta do Batch no portal do Azure][account_blade]

* <span data-ttu-id="3c419-194">**O URL da conta do batch**: quando desenvolver uma aplicação com Olá [APIs do Batch](batch-apis-tools.md#azure-accounts-for-batch-development), terá uma tooaccess de URL da conta os recursos do Batch.</span><span class="sxs-lookup"><span data-stu-id="3c419-194">**Batch account URL**: When you develop an application with hello [Batch APIs](batch-apis-tools.md#azure-accounts-for-batch-development), you'll need an account URL tooaccess your Batch resources.</span></span> <span data-ttu-id="3c419-195">Um URL de conta do Batch tem Olá seguinte formato:</span><span class="sxs-lookup"><span data-stu-id="3c419-195">A Batch account URL has hello following format:</span></span>

    `https://<account_name>.<region>.batch.azure.com`

![URL da conta do Batch no portal][account_url]

* <span data-ttu-id="3c419-197">**Chaves de acesso** (modo de serviço do Batch): tooauthenticate acesso tooyour conta do Batch da sua aplicação, terá de uma chave de acesso da conta.</span><span class="sxs-lookup"><span data-stu-id="3c419-197">**Access keys** (Batch service mode): tooauthenticate access tooyour Batch account from your application, you'll need an account access key.</span></span> <span data-ttu-id="3c419-198">(Esta definição não está disponível no modo de subscrição de utilizador, onde utiliza a autenticação do Azure Active Directory.)</span><span class="sxs-lookup"><span data-stu-id="3c419-198">(This setting is not available in user subscription mode, where you use Azure Active Directory authentication.)</span></span>

    <span data-ttu-id="3c419-199">tooview ou voltar a gerar chaves de acesso da sua conta do Batch, introduza `keys` no menu à esquerda Olá **pesquisa** caixa no painel de conta de Batch de Olá, em seguida, selecione **chaves**.</span><span class="sxs-lookup"><span data-stu-id="3c419-199">tooview or regenerate your Batch account's access keys, enter `keys` in hello left menu **Search** box on hello Batch account blade, then select **Keys**.</span></span>

    ![Chaves da conta do Batch no portal do Azure][account_keys]

[!INCLUDE [batch-pricing-include](../../includes/batch-pricing-include.md)]

## <a name="linked-azure-storage-account"></a><span data-ttu-id="3c419-201">Conta do Armazenamento do Azure Ligada</span><span class="sxs-lookup"><span data-stu-id="3c419-201">Linked Azure Storage account</span></span>

<span data-ttu-id="3c419-202">Opcionalmente, pode ligar um tooyour de conta de armazenamento do Azure conta do Batch para fins gerais.</span><span class="sxs-lookup"><span data-stu-id="3c419-202">You can optionally link a general-purpose Azure Storage account tooyour Batch account.</span></span> <span data-ttu-id="3c419-203">Olá [pacotes de aplicações](batch-application-packages.md) funcionalidade do Batch utiliza o Blob storage do Azure, como sucede Olá [.NET do Batch ficheiro convenções](batch-task-output.md) biblioteca.</span><span class="sxs-lookup"><span data-stu-id="3c419-203">hello [application packages](batch-application-packages.md) feature of Batch uses Azure Blob storage, as does hello [Batch File Conventions .NET](batch-task-output.md) library.</span></span> <span data-ttu-id="3c419-204">Estas funcionalidades opcionais ajudá-lo a implementar Olá com as suas tarefas Batch, dados e aplicações persistentes Olá produzem.</span><span class="sxs-lookup"><span data-stu-id="3c419-204">These optional features assist you in deploying hello applications that your Batch tasks run, and persisting hello data they produce.</span></span>

<span data-ttu-id="3c419-205">Recomendamos que crie uma nova conta de Armazenamento para utilização exclusiva por parte da sua conta do Batch.</span><span class="sxs-lookup"><span data-stu-id="3c419-205">We recommend that you create a new Storage account exclusively for use by your Batch account.</span></span>

![Criar uma conta de armazenamento para fins gerais][storage_account]

> [!NOTE]
> <span data-ttu-id="3c419-207">O Azure Batch atualmente suporta apenas Olá para fins gerais armazenamento tipo de conta.</span><span class="sxs-lookup"><span data-stu-id="3c419-207">Azure Batch currently supports only hello general-purpose Storage account type.</span></span> <span data-ttu-id="3c419-208">Este tipo de conta é descrito no passo 5, [Criar uma conta de armazenamento] (../storage/common/storage-create-storage-account.md#create-a-storage-account), em [Sobre as contas de armazenamento do Azure](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="3c419-208">This account type is described in step 5, [Create a storage account] (../storage/common/storage-create-storage-account.md#create-a-storage-account), in [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span>
>
>

> [!WARNING]
> <span data-ttu-id="3c419-209">Tenha cuidado quando regenerar chaves de acesso de Olá de uma conta de armazenamento ligada.</span><span class="sxs-lookup"><span data-stu-id="3c419-209">Be careful when regenerating hello access keys of a linked Storage account.</span></span> <span data-ttu-id="3c419-210">Voltar a gerar apenas uma chave de conta do Storage e clique em **sincronizar chaves** no Olá ligado painel de conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="3c419-210">Regenerate only one Storage account key and click **Sync Keys** on hello linked Storage account blade.</span></span> <span data-ttu-id="3c419-211">Aguardar cinco minutos tooallow Olá chaves toopropagate toohello nós de computação em seus conjuntos e, em seguida, voltar a gerar e sincronizar Olá outra chave se for necessário.</span><span class="sxs-lookup"><span data-stu-id="3c419-211">Wait five minutes tooallow hello keys toopropagate toohello compute nodes in your pools, then regenerate and synchronize hello other key if necessary.</span></span> <span data-ttu-id="3c419-212">Se voltar a gerar ambas as chaves em Olá mesmo tempo, os nós de computação não será capaz de toosynchronize nenhuma das chaves e estas perdem o acesso toohello armazenamento conta.</span><span class="sxs-lookup"><span data-stu-id="3c419-212">If you regenerate both keys at hello same time, your compute nodes will not be able toosynchronize either key, and they will lose access toohello Storage account.</span></span>
>
>

<span data-ttu-id="3c419-213">![Regenerar chaves de conta de armazenamento][4]</span><span class="sxs-lookup"><span data-stu-id="3c419-213">![Regenerating storage account keys][4]</span></span>

## <a name="batch-service-quotas-and-limits"></a><span data-ttu-id="3c419-214">Quotas e limites do serviço Batch</span><span class="sxs-lookup"><span data-stu-id="3c419-214">Batch service quotas and limits</span></span>
<span data-ttu-id="3c419-215">Tenha ser que como com a sua subscrição do Azure e outro Azure serviços, a determinados [quotas e limites](batch-quota-limit.md) aplicar tooBatch contas.</span><span class="sxs-lookup"><span data-stu-id="3c419-215">Please be aware that as with your Azure subscription and other Azure services, certain [quotas and limits](batch-quota-limit.md) apply tooBatch accounts.</span></span> <span data-ttu-id="3c419-216">As quotas atuais numa conta de Batch de aparecer no portal de Olá na conta de Olá **propriedades**.</span><span class="sxs-lookup"><span data-stu-id="3c419-216">Current quotas for a Batch account appear in hello portal in hello account **Properties**.</span></span>

![Quotas das contas do Batch no portal do Azure][quotas]



<span data-ttu-id="3c419-218">Além disso, muitas destas quotas podem ser aumentadas simplesmente com um pedido de suporte de produto livre submetido na Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="3c419-218">Additionally, many of these quotas can be increased simply with a free product support request submitted in hello Azure portal.</span></span> <span data-ttu-id="3c419-219">Consulte [Quotas e limites para Olá serviço Azure Batch](batch-quota-limit.md) para obter detalhes sobre a quota aumenta a pedir.</span><span class="sxs-lookup"><span data-stu-id="3c419-219">See [Quotas and limits for hello Azure Batch service](batch-quota-limit.md) for details on requesting quota increases.</span></span>

## <a name="other-batch-account-management-options"></a><span data-ttu-id="3c419-220">Outras opções de gestão de contas do Batch</span><span class="sxs-lookup"><span data-stu-id="3c419-220">Other Batch account management options</span></span>
<span data-ttu-id="3c419-221">Além disso toousing Olá portal do Azure, também pode criar e gerir contas do Batch com seguinte Olá:</span><span class="sxs-lookup"><span data-stu-id="3c419-221">In addition toousing hello Azure portal, you can also create and manage Batch accounts with hello following:</span></span>

* [<span data-ttu-id="3c419-222">Cmdlets do PowerShell do Batch</span><span class="sxs-lookup"><span data-stu-id="3c419-222">Batch PowerShell cmdlets</span></span>](batch-powershell-cmdlets-get-started.md)
* [<span data-ttu-id="3c419-223">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="3c419-223">Azure CLI</span></span>](batch-cli-get-started.md)
* [<span data-ttu-id="3c419-224">Gestão de Batch .NET</span><span class="sxs-lookup"><span data-stu-id="3c419-224">Batch Management .NET</span></span>](batch-management-dotnet.md)

## <a name="next-steps"></a><span data-ttu-id="3c419-225">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="3c419-225">Next steps</span></span>
* <span data-ttu-id="3c419-226">Consulte Olá [descrição geral da funcionalidade do Batch](batch-api-basics.md) toolearn mais sobre as funcionalidades e conceitos do serviço Batch.</span><span class="sxs-lookup"><span data-stu-id="3c419-226">See hello [Batch feature overview](batch-api-basics.md) toolearn more about Batch service concepts and features.</span></span> <span data-ttu-id="3c419-227">Olá artigo aborda Olá recursos do Batch principais como conjuntos, nós de computação, trabalhos e tarefas e fornece uma descrição geral de Olá funcionalidades do serviço que permitem a execução de cargas de trabalho de computação em grande escala.</span><span class="sxs-lookup"><span data-stu-id="3c419-227">hello article discusses hello primary Batch resources such as pools, compute nodes, jobs, and tasks, and provides an overview of hello service's features that enable large-scale compute workload execution.</span></span>
* <span data-ttu-id="3c419-228">Saiba Olá Noções básicas sobre desenvolver uma aplicação preparada para Batch utilizando Olá [biblioteca de cliente .NET do Batch](batch-dotnet-get-started.md) ou [Python](batch-python-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="3c419-228">Learn hello basics of developing a Batch-enabled application using hello [Batch .NET client library](batch-dotnet-get-started.md) or [Python](batch-python-tutorial.md).</span></span> <span data-ttu-id="3c419-229">Estes artigos introdutórias ajudá-lo através de uma aplicação de trabalho que utiliza Olá Batch serviço tooexecute uma carga de trabalho em vários nós de computação e inclui a utilização do armazenamento do Azure para teste de ficheiros da carga de trabalho e obtenção.</span><span class="sxs-lookup"><span data-stu-id="3c419-229">These introductory articles guide you through a working application that uses hello Batch service tooexecute a workload on multiple compute nodes, and includes using Azure Storage for workload file staging and retrieval.</span></span>

[api_net]: https://msdn.microsoft.com/library/azure/mt348682.aspx
[api_rest]: https://msdn.microsoft.com/library/azure/Dn820158.aspx

[azure_portal]: https://portal.azure.com
[batch_pricing]: https://azure.microsoft.com/pricing/details/batch/

[4]: ./media/batch-account-create-portal/batch_acct_04.png "Regenerar chaves de conta de armazenamento"
[marketplace_portal]: ./media/batch-account-create-portal/marketplace_batch.PNG
[account_blade]: ./media/batch-account-create-portal/batch_blade.png
[account_portal]: ./media/batch-account-create-portal/batch_acct_portal.png
[account_keys]: ./media/batch-account-create-portal/account_keys.PNG
[account_url]: ./media/batch-account-create-portal/account_url.png
[storage_account]: ./media/batch-account-create-portal/storage_account.png
[quotas]: ./media/batch-account-create-portal/quotas.png
[subscription_access]: ./media/batch-account-create-portal/subscription_iam.png
[add_permission]: ./media/batch-account-create-portal/add_permission.png
[account_portal_byos]: ./media/batch-account-create-portal/batch_acct_portal_byos.png
