---
title: "aaaCreate a sua primeira função do Olá Portal do Azure | Microsoft Docs"
description: "Saiba como toocreate a sua primeira Azure funcionar para a utilização de execução sem servidor Olá portal do Azure."
services: functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
ms.assetid: 96cf87b9-8db6-41a8-863a-abb828e3d06d
ms.service: functions
ms.devlang: multiple
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 08/07/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 84283d7d4bc6015061946af4589f9a70ae61f36b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-function-in-hello-azure-portal"></a><span data-ttu-id="74cae-103">Criar a sua primeira função no Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="74cae-103">Create your first function in hello Azure portal</span></span>

<span data-ttu-id="74cae-104">As funções do Azure permite-lhe executar o seu código num ambiente sem servidor sem ter toofirst criar uma VM ou publicar uma aplicação web.</span><span class="sxs-lookup"><span data-stu-id="74cae-104">Azure Functions lets you execute your code in a serverless environment without having toofirst create a VM or publish a web application.</span></span> <span data-ttu-id="74cae-105">Neste tópico, saiba como toouse funciona toocreate uma função de "Olá mundo" Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="74cae-105">In this topic, learn how toouse Functions toocreate a "hello world" function in hello Azure portal.</span></span>

![Criar aplicação de função no Olá portal do Azure](./media/functions-create-first-azure-function/function-app-in-portal-editor.png)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="log-in-tooazure"></a><span data-ttu-id="74cae-107">Inicie sessão no tooAzure</span><span class="sxs-lookup"><span data-stu-id="74cae-107">Log in tooAzure</span></span>

<span data-ttu-id="74cae-108">Inicie sessão no toohello [portal do Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="74cae-108">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>

## <a name="create-a-function-app"></a><span data-ttu-id="74cae-109">Criar uma aplicação de função</span><span class="sxs-lookup"><span data-stu-id="74cae-109">Create a function app</span></span>

<span data-ttu-id="74cae-110">Tem de ter uma execução de Olá do função aplicação toohost das suas funções.</span><span class="sxs-lookup"><span data-stu-id="74cae-110">You must have a function app toohost hello execution of your functions.</span></span> <span data-ttu-id="74cae-111">As aplicações App Function permitem-lhe agrupar funções como unidades lógicas para uma gestão, implementação e partilha de recursos mais fácil.</span><span class="sxs-lookup"><span data-stu-id="74cae-111">A function app lets you group functions as a logic unit for easier management, deployment, and sharing of resources.</span></span> 

[!INCLUDE [Create function app Azure portal](../../includes/functions-create-function-app-portal.md)]

[!INCLUDE [functions-portal-favorite-function-apps](../../includes/functions-portal-favorite-function-apps.md)]

<span data-ttu-id="74cae-112">Em seguida, crie uma função na nova aplicação de função Olá.</span><span class="sxs-lookup"><span data-stu-id="74cae-112">Next, you create a function in hello new function app.</span></span>

## <span data-ttu-id="74cae-113"><a name="create-function"></a>Criar uma função acionada por HTTP</span><span class="sxs-lookup"><span data-stu-id="74cae-113"><a name="create-function"></a>Create an HTTP triggered function</span></span>

1. <span data-ttu-id="74cae-114">Expanda a nova aplicação de função, em seguida, clique em Olá  **+**  no botão seguinte demasiado**funções**.</span><span class="sxs-lookup"><span data-stu-id="74cae-114">Expand your new function app, then click hello **+** button next too**Functions**.</span></span>

2.  <span data-ttu-id="74cae-115">No Olá **começar rapidamente** página, selecione **WebHook + API**, **escolher um idioma** para a função e clique em **criar esta função** .</span><span class="sxs-lookup"><span data-stu-id="74cae-115">In hello **Get started quickly** page, select **WebHook + API**, **Choose a language** for your function, and click **Create this function**.</span></span> 
   
    ![Guia de introdução de funções no Olá portal do Azure.](./media/functions-create-first-azure-function/function-app-quickstart-node-webhook.png)

<span data-ttu-id="74cae-117">Uma função é criada no idioma que escolheu utilizando o modelo de Olá para uma função de acionada de HTTP.</span><span class="sxs-lookup"><span data-stu-id="74cae-117">A function is created in your chosen language using hello template for an HTTP triggered function.</span></span> <span data-ttu-id="74cae-118">Pode executar a nova função de Olá ao enviar um pedido HTTP.</span><span class="sxs-lookup"><span data-stu-id="74cae-118">You can run hello new function by sending an HTTP request.</span></span>

## <a name="test-hello-function"></a><span data-ttu-id="74cae-119">Testar a função de Olá</span><span class="sxs-lookup"><span data-stu-id="74cae-119">Test hello function</span></span>

1. <span data-ttu-id="74cae-120">Na sua nova função, clique em **</> Obter URL da função**, selecione **predefinição (tecla de função)** e, em seguida, clique em **Copiar**.</span><span class="sxs-lookup"><span data-stu-id="74cae-120">In your new function, click **</> Get function URL**, select **default (Function key)**, and then click **Copy**.</span></span> 

    ![Copie o URL da função Olá do Olá portal do Azure](./media/functions-create-first-azure-function/function-app-develop-tab-testing.png)

2. <span data-ttu-id="74cae-122">Colar Olá função URL na barra de endereço do browser.</span><span class="sxs-lookup"><span data-stu-id="74cae-122">Paste hello function URL into your browser's address bar.</span></span> <span data-ttu-id="74cae-123">Acrescentar a cadeia de consulta Olá `&name=<yourname>` toothis URL e prima Olá `Enter` chave no seu pedido de Olá tooexecute teclado.</span><span class="sxs-lookup"><span data-stu-id="74cae-123">Append hello query string `&name=<yourname>` toothis URL and press hello `Enter` key on your keyboard tooexecute hello request.</span></span> <span data-ttu-id="74cae-124">Olá segue-se um exemplo de resposta de Olá devolvida pela função Olá no browser Edge de Olá:</span><span class="sxs-lookup"><span data-stu-id="74cae-124">hello following is an example of hello response returned by hello function in hello Edge browser:</span></span>

    ![Resposta de função no browser Olá.](./media/functions-create-first-azure-function/function-app-browser-testing.png)

    <span data-ttu-id="74cae-126">pedido de Olá URL inclui uma chave que é necessário, por predefinição, tooaccess a função através de HTTP.</span><span class="sxs-lookup"><span data-stu-id="74cae-126">hello request URL includes a key that is required, by default, tooaccess your function over HTTP.</span></span>   

3. <span data-ttu-id="74cae-127">Quando a função é executada, informações de rastreio são escritas toohello registos.</span><span class="sxs-lookup"><span data-stu-id="74cae-127">When your function runs, trace information is written toohello logs.</span></span> <span data-ttu-id="74cae-128">resultados de rastreio de Olá toosee da execução anterior do Olá, regresse a função tooyour no portal de Olá e clique em Olá segurança seta na parte inferior de Olá de Olá ecrã tooexpand **registos**.</span><span class="sxs-lookup"><span data-stu-id="74cae-128">toosee hello trace output from hello previous execution, return tooyour function in hello portal and click hello up arrow at hello bottom of hello screen tooexpand **Logs**.</span></span> 

   ![As funções de início de sessão Visualizador Olá portal do Azure.](./media/functions-create-first-azure-function/function-view-logs.png)

## <a name="clean-up-resources"></a><span data-ttu-id="74cae-130">Limpar recursos</span><span class="sxs-lookup"><span data-stu-id="74cae-130">Clean up resources</span></span>

[!INCLUDE [Clean up resources](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a><span data-ttu-id="74cae-131">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="74cae-131">Next steps</span></span>

<span data-ttu-id="74cae-132">Criou uma aplicação App Function com uma função acionada por HTTP simples.</span><span class="sxs-lookup"><span data-stu-id="74cae-132">You have created a function app with a simple HTTP triggered function.</span></span>  

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

<span data-ttu-id="74cae-133">Para obter mais informações, veja [Azure Functions HTTP and webhook bindings](functions-bindings-http-webhook.md) (Enlaces de HTTP e webhook das Funções do Azure).</span><span class="sxs-lookup"><span data-stu-id="74cae-133">For more information, see [Azure Functions HTTP and webhook bindings](functions-bindings-http-webhook.md).</span></span>



