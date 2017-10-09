---
title: "aaaCreate uma função de acionada por mensagens de filas do Azure | Microsoft Docs"
description: "Utilize as funções do Azure toocreate uma função sem servidor que é invocada por um mensagens submetido tooan fila de armazenamento do Azure."
services: azure-functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
ms.assetid: 361da2a4-15d1-4903-bdc4-cc4b27fc3ff4
ms.service: functions
ms.devlang: multiple
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/31/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: e9501ed336b502eaeee3fa62ec4ae085c76de0ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-function-triggered-by-azure-queue-storage"></a><span data-ttu-id="fe940-103">Criar uma função acionada pelo Armazenamento de filas do Azure</span><span class="sxs-lookup"><span data-stu-id="fe940-103">Create a function triggered by Azure Queue storage</span></span>

<span data-ttu-id="fe940-104">Saiba como toocreate uma função acionada quando as mensagens são submetidos tooan fila de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="fe940-104">Learn how toocreate a function triggered when messages are submitted tooan Azure Storage queue.</span></span>

![Mensagem de vista nos registos de Olá.](./media/functions-create-storage-queue-triggered-function/function-app-in-portal-editor.png)

## <a name="prerequisites"></a><span data-ttu-id="fe940-106">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="fe940-106">Prerequisites</span></span>

- <span data-ttu-id="fe940-107">Transfira e instale Olá [Explorador de armazenamento do Microsoft Azure](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="fe940-107">Download and install hello [Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span></span>

- <span data-ttu-id="fe940-108">Uma subscrição do Azure.</span><span class="sxs-lookup"><span data-stu-id="fe940-108">An Azure subscription.</span></span> <span data-ttu-id="fe940-109">Se não tiver uma, crie uma [conta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) antes de começar.</span><span class="sxs-lookup"><span data-stu-id="fe940-109">If you don't have one, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [functions-portal-favorite-function-apps](../../includes/functions-portal-favorite-function-apps.md)]

## <a name="create-an-azure-function-app"></a><span data-ttu-id="fe940-110">Criar uma aplicação de Funções do Azure</span><span class="sxs-lookup"><span data-stu-id="fe940-110">Create an Azure Function app</span></span>

[!INCLUDE [Create function app Azure portal](../../includes/functions-create-function-app-portal.md)]

![Aplicação Function App criada com êxito.](./media/functions-create-first-azure-function/function-app-create-success.png)

<span data-ttu-id="fe940-112">Em seguida, crie uma função na nova aplicação de função Olá.</span><span class="sxs-lookup"><span data-stu-id="fe940-112">Next, you create a function in hello new function app.</span></span>

<a name="create-function"></a>

## <a name="create-a-queue-triggered-function"></a><span data-ttu-id="fe940-113">Criar uma função acionada por Fila</span><span class="sxs-lookup"><span data-stu-id="fe940-113">Create a Queue triggered function</span></span>

1. <span data-ttu-id="fe940-114">Expanda a sua aplicação de função e clique em Olá  **+**  no botão seguinte demasiado**funções**.</span><span class="sxs-lookup"><span data-stu-id="fe940-114">Expand your function app and click hello **+** button next too**Functions**.</span></span> <span data-ttu-id="fe940-115">Se esta for a primeira função de Olá na sua aplicação de função, selecione **função personalizada**.</span><span class="sxs-lookup"><span data-stu-id="fe940-115">If this is hello first function in your function app, select **Custom function**.</span></span> <span data-ttu-id="fe940-116">Esta ação apresenta o conjunto completo de Olá dos modelos de função.</span><span class="sxs-lookup"><span data-stu-id="fe940-116">This displays hello complete set of function templates.</span></span>

    ![Página de início rápido de funções no Olá portal do Azure](./media/functions-create-storage-queue-triggered-function/add-first-function.png)

2. <span data-ttu-id="fe940-118">Selecione Olá **QueueTrigger** modelo para o idioma pretendido e utilize as definições de Olá conforme especificado na tabela de Olá.</span><span class="sxs-lookup"><span data-stu-id="fe940-118">Select hello **QueueTrigger** template for your desired language, and  use hello settings as specified in hello table.</span></span>

    ![Crie uma função de acionada de fila de armazenamento de Olá.](./media/functions-create-storage-queue-triggered-function/functions-create-queue-storage-trigger-portal.png)
    
    | <span data-ttu-id="fe940-120">Definição</span><span class="sxs-lookup"><span data-stu-id="fe940-120">Setting</span></span> | <span data-ttu-id="fe940-121">Valor sugerido</span><span class="sxs-lookup"><span data-stu-id="fe940-121">Suggested value</span></span> | <span data-ttu-id="fe940-122">Descrição</span><span class="sxs-lookup"><span data-stu-id="fe940-122">Description</span></span> |
    |---|---|---|
    | <span data-ttu-id="fe940-123">**Nome da fila**</span><span class="sxs-lookup"><span data-stu-id="fe940-123">**Queue name**</span></span>   | <span data-ttu-id="fe940-124">myqueue-items</span><span class="sxs-lookup"><span data-stu-id="fe940-124">myqueue-items</span></span>    | <span data-ttu-id="fe940-125">Nome do Olá fila tooconnect tooin sua conta do Storage.</span><span class="sxs-lookup"><span data-stu-id="fe940-125">Name of hello queue tooconnect tooin your Storage account.</span></span> |
    | <span data-ttu-id="fe940-126">**Ligação da conta de armazenamento**</span><span class="sxs-lookup"><span data-stu-id="fe940-126">**Storage account connection**</span></span> | <span data-ttu-id="fe940-127">AzureWebJobStorage</span><span class="sxs-lookup"><span data-stu-id="fe940-127">AzureWebJobStorage</span></span> | <span data-ttu-id="fe940-128">Pode utilizar a ligação de conta de armazenamento de Olá já a ser utilizada pela sua aplicação de função ou crie um novo.</span><span class="sxs-lookup"><span data-stu-id="fe940-128">You can use hello storage account connection already being used by your function app, or create a new one.</span></span>  |
    | <span data-ttu-id="fe940-129">**Dar um nome à função**</span><span class="sxs-lookup"><span data-stu-id="fe940-129">**Name your function**</span></span> | <span data-ttu-id="fe940-130">Exclusivo na aplicação Function App</span><span class="sxs-lookup"><span data-stu-id="fe940-130">Unique in your function app</span></span> | <span data-ttu-id="fe940-131">O nome desta função acionada por fila.</span><span class="sxs-lookup"><span data-stu-id="fe940-131">Name of this queue triggered function.</span></span> |

3. <span data-ttu-id="fe940-132">Clique em **criar** toocreate sua função.</span><span class="sxs-lookup"><span data-stu-id="fe940-132">Click **Create** toocreate your function.</span></span>

<span data-ttu-id="fe940-133">Em seguida, ligar a conta de armazenamento do Azure tooyour e criar Olá **myqueue itens** fila de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="fe940-133">Next, you connect tooyour Azure Storage account and create hello **myqueue-items** storage queue.</span></span>

## <a name="create-hello-queue"></a><span data-ttu-id="fe940-134">Criar fila Olá</span><span class="sxs-lookup"><span data-stu-id="fe940-134">Create hello queue</span></span>

1. <span data-ttu-id="fe940-135">Na sua função, clique em **Integrar**, expanda **Documentação** e copie **Nome da conta** e **Chave da conta**.</span><span class="sxs-lookup"><span data-stu-id="fe940-135">In your function, click **Integrate**, expand **Documentation**, and copy both **Account name** and **Account key**.</span></span> <span data-ttu-id="fe940-136">Pode utilizar estas credenciais tooconnect toohello armazenamento conta.</span><span class="sxs-lookup"><span data-stu-id="fe940-136">You use these credentials tooconnect toohello storage account.</span></span> <span data-ttu-id="fe940-137">Se já tiver estabelecido ligação a conta do storage, ignore toostep 4.</span><span class="sxs-lookup"><span data-stu-id="fe940-137">If you have already connected your storage account, skip toostep 4.</span></span>

    ![Obter a conta de armazenamento Olá credenciais de ligação.](./media/functions-create-storage-queue-triggered-function/functions-storage-account-connection.png)<span data-ttu-id="fe940-139">v</span><span class="sxs-lookup"><span data-stu-id="fe940-139">v</span></span>

1. <span data-ttu-id="fe940-140">Executar Olá [Explorador de armazenamento do Microsoft Azure](http://storageexplorer.com/) ferramenta, clique em Olá ligar ícone Olá esquerda, escolha **utilizar um nome de conta de armazenamento e a chave**e clique em **seguinte**.</span><span class="sxs-lookup"><span data-stu-id="fe940-140">Run hello [Microsoft Azure Storage Explorer](http://storageexplorer.com/) tool, click hello connect icon on hello left, choose **Use a storage account name and key**, and click **Next**.</span></span>

    ![Execute a ferramenta Explorador de conta de armazenamento de Olá.](./media/functions-create-storage-queue-triggered-function/functions-storage-manager-connect-1.png)

1. <span data-ttu-id="fe940-142">Introduza Olá **nome da conta** e **chave da conta** do passo 1, clique em **seguinte** e, em seguida, **Connect**.</span><span class="sxs-lookup"><span data-stu-id="fe940-142">Enter hello **Account name** and **Account key** from step 1, click **Next** and then **Connect**.</span></span>

    ![Introduza as credenciais do armazenamento de Olá e ligar.](./media/functions-create-storage-queue-triggered-function/functions-storage-manager-connect-2.png)

1. <span data-ttu-id="fe940-144">Expanda a conta de armazenamento de Olá anexado, com o botão direito **filas**, clique em **criar fila**, tipo `myqueue-items`, e, em seguida, prima enter.</span><span class="sxs-lookup"><span data-stu-id="fe940-144">Expand hello attached storage account, right-click **Queues**, click **Create queue**, type `myqueue-items`, and then press enter.</span></span>

    ![Crie uma fila de armazenamento.](./media/functions-create-storage-queue-triggered-function/functions-storage-manager-create-queue.png)

<span data-ttu-id="fe940-146">Agora que tem uma fila de armazenamento, pode testar a função Olá adicionando uma fila de toohello de mensagens.</span><span class="sxs-lookup"><span data-stu-id="fe940-146">Now that you have a storage queue, you can test hello function by adding a message toohello queue.</span></span>

## <a name="test-hello-function"></a><span data-ttu-id="fe940-147">Testar a função de Olá</span><span class="sxs-lookup"><span data-stu-id="fe940-147">Test hello function</span></span>

1. <span data-ttu-id="fe940-148">No portal do Azure Olá, procurar tooyour função expanda Olá **registos** em Olá parte inferior da página Olá e certifique-se de que registo de transmissão em fluxo não está em pausa.</span><span class="sxs-lookup"><span data-stu-id="fe940-148">Back in hello Azure portal, browse tooyour function expand hello **Logs** at hello bottom of hello page and make sure that log streaming isn't paused.</span></span>

1. <span data-ttu-id="fe940-149">No Storage Explorer, expanda a conta de armazenamento, **Filas** e **myqueue-items** e clique em **Adicionar mensagem**.</span><span class="sxs-lookup"><span data-stu-id="fe940-149">In Storage Explorer, expand your storage account, **Queues**, and **myqueue-items**, then click **Add message**.</span></span>

    ![Adicione uma fila de toohello de mensagens.](./media/functions-create-storage-queue-triggered-function/functions-storage-manager-add-message.png)

1. <span data-ttu-id="fe940-151">Escreva a sua mensagem “Hello World”</span><span class="sxs-lookup"><span data-stu-id="fe940-151">Type your "Hello World!"</span></span> <span data-ttu-id="fe940-152">em **Texto da mensagem** e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="fe940-152">message in **Message text** and click **OK**.</span></span>

1. <span data-ttu-id="fe940-153">Aguarde alguns segundos, em seguida, voltar atrás tooyour registos de funções e certifique-se de que essa nova mensagem de Olá lidas a partir do fila Olá.</span><span class="sxs-lookup"><span data-stu-id="fe940-153">Wait for a few seconds, then go back tooyour function logs and verify that hello new message has been read from hello queue.</span></span>

    ![Mensagem de vista nos registos de Olá.](./media/functions-create-storage-queue-triggered-function/functions-queue-storage-trigger-view-logs.png)

1. <span data-ttu-id="fe940-155">No Explorador de armazenamento, clique **atualizar** e verifique essa mensagem de saudação foi processada e já não se encontra na fila de Olá.</span><span class="sxs-lookup"><span data-stu-id="fe940-155">Back in Storage Explorer, click **Refresh** and verify that hello message has been processed and is no longer in hello queue.</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="fe940-156">Limpar recursos</span><span class="sxs-lookup"><span data-stu-id="fe940-156">Clean up resources</span></span>

[!INCLUDE [Next steps note](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a><span data-ttu-id="fe940-157">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="fe940-157">Next steps</span></span>

<span data-ttu-id="fe940-158">Foi criada com uma função que é executado quando uma mensagem é adicionada tooa fila de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="fe940-158">You have created a function that runs when a message is added tooa storage queue.</span></span>

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

<span data-ttu-id="fe940-159">Para obter mais informações sobre os acionadores do Armazenamento de filas, veja [Azure Functions Storage queue bindings](functions-bindings-storage-queue.md) (Enlaces da fila de Armazenamento das Funções do Azure).</span><span class="sxs-lookup"><span data-stu-id="fe940-159">For more information about Queue storage triggers, see [Azure Functions Storage queue bindings](functions-bindings-storage-queue.md).</span></span>