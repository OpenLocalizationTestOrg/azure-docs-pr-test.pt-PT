---
title: "aaaCreate uma função que é executada com base numa agenda no Azure | Microsoft Docs"
description: "Saiba como toocreate uma função no Azure que é executada com base numa agenda que definir."
services: functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
ms.assetid: ba50ee47-58e0-4972-b67b-828f2dc48701
ms.service: functions
ms.devlang: multiple
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/31/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 793b06a65a154466dfd4c121bcc88082227cd597
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-function-in-azure-that-is-triggered-by-a-timer"></a><span data-ttu-id="02c1a-103">Criar uma função no Azure que é acionada por um temporizador</span><span class="sxs-lookup"><span data-stu-id="02c1a-103">Create a function in Azure that is triggered by a timer</span></span>

<span data-ttu-id="02c1a-104">Saiba como toouse das funções do Azure toocreate uma função que executa com base numa agenda que definir.</span><span class="sxs-lookup"><span data-stu-id="02c1a-104">Learn how toouse Azure Functions toocreate a function that runs based a schedule that you define.</span></span>

![Criar aplicação de função no Olá portal do Azure](./media/functions-create-scheduled-function/function-app-in-portal-editor.png)

## <a name="prerequisites"></a><span data-ttu-id="02c1a-106">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="02c1a-106">Prerequisites</span></span>

<span data-ttu-id="02c1a-107">toocomplete neste tutorial:</span><span class="sxs-lookup"><span data-stu-id="02c1a-107">toocomplete this tutorial:</span></span>

+ <span data-ttu-id="02c1a-108">Se não tiver uma subscrição do Azure, crie uma [conta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) antes de começar.</span><span class="sxs-lookup"><span data-stu-id="02c1a-108">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [functions-portal-favorite-function-apps](../../includes/functions-portal-favorite-function-apps.md)]

## <a name="create-an-azure-function-app"></a><span data-ttu-id="02c1a-109">Criar uma aplicação de Funções do Azure</span><span class="sxs-lookup"><span data-stu-id="02c1a-109">Create an Azure Function app</span></span>

[!INCLUDE [Create function app Azure portal](../../includes/functions-create-function-app-portal.md)]

![Aplicação Function App criada com êxito.](./media/functions-create-first-azure-function/function-app-create-success.png)

<span data-ttu-id="02c1a-111">Em seguida, crie uma função na nova aplicação de função Olá.</span><span class="sxs-lookup"><span data-stu-id="02c1a-111">Next, you create a function in hello new function app.</span></span>

<a name="create-function"></a>

## <a name="create-a-timer-triggered-function"></a><span data-ttu-id="02c1a-112">Criar uma função acionada por temporizador</span><span class="sxs-lookup"><span data-stu-id="02c1a-112">Create a timer triggered function</span></span>

1. <span data-ttu-id="02c1a-113">Expanda a sua aplicação de função e clique em Olá  **+**  no botão seguinte demasiado**funções**.</span><span class="sxs-lookup"><span data-stu-id="02c1a-113">Expand your function app and click hello **+** button next too**Functions**.</span></span> <span data-ttu-id="02c1a-114">Se esta for a primeira função de Olá na sua aplicação de função, selecione **função personalizada**.</span><span class="sxs-lookup"><span data-stu-id="02c1a-114">If this is hello first function in your function app, select **Custom function**.</span></span> <span data-ttu-id="02c1a-115">Esta ação apresenta o conjunto completo de Olá dos modelos de função.</span><span class="sxs-lookup"><span data-stu-id="02c1a-115">This displays hello complete set of function templates.</span></span>

    ![Página de início rápido de funções no Olá portal do Azure](./media/functions-create-scheduled-function/add-first-function.png)

2. <span data-ttu-id="02c1a-117">Selecione Olá **TimerTrigger** modelo para o idioma pretendido.</span><span class="sxs-lookup"><span data-stu-id="02c1a-117">Select hello **TimerTrigger** template for your desired language.</span></span> <span data-ttu-id="02c1a-118">Em seguida, utilize definições de Olá conforme especificado na tabela de Olá:</span><span class="sxs-lookup"><span data-stu-id="02c1a-118">Then use hello settings as specified in hello table:</span></span>

    ![Crie uma função de temporizador acionada Olá portal do Azure.](./media/functions-create-scheduled-function/functions-create-timer-trigger.png)

    | <span data-ttu-id="02c1a-120">Definição</span><span class="sxs-lookup"><span data-stu-id="02c1a-120">Setting</span></span> | <span data-ttu-id="02c1a-121">Valor sugerido</span><span class="sxs-lookup"><span data-stu-id="02c1a-121">Suggested value</span></span> | <span data-ttu-id="02c1a-122">Descrição</span><span class="sxs-lookup"><span data-stu-id="02c1a-122">Description</span></span> |
    |---|---|---|
    | <span data-ttu-id="02c1a-123">**Dar um nome à função**</span><span class="sxs-lookup"><span data-stu-id="02c1a-123">**Name your function**</span></span> | <span data-ttu-id="02c1a-124">TimerTriggerCSharp1</span><span class="sxs-lookup"><span data-stu-id="02c1a-124">TimerTriggerCSharp1</span></span> | <span data-ttu-id="02c1a-125">Define o nome de Olá da sua função de temporizador acionado.</span><span class="sxs-lookup"><span data-stu-id="02c1a-125">Defines hello name of your timer triggered function.</span></span> |
    | <span data-ttu-id="02c1a-126">**[Agenda](http://en.wikipedia.org/wiki/Cron#CRON_expression)**</span><span class="sxs-lookup"><span data-stu-id="02c1a-126">**[Schedule](http://en.wikipedia.org/wiki/Cron#CRON_expression)**</span></span> | <span data-ttu-id="02c1a-127">0 \*/1 \* \* \* \*</span><span class="sxs-lookup"><span data-stu-id="02c1a-127">0 \*/1 \* \* \* \*</span></span> | <span data-ttu-id="02c1a-128">Um campo seis [expressão CRON](http://en.wikipedia.org/wiki/Cron#CRON_expression) que agendas toorun sua função de cada minuto.</span><span class="sxs-lookup"><span data-stu-id="02c1a-128">A six field [CRON expression](http://en.wikipedia.org/wiki/Cron#CRON_expression) that schedules your function toorun every minute.</span></span> |

2. <span data-ttu-id="02c1a-129">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="02c1a-129">Click **Create**.</span></span> <span data-ttu-id="02c1a-130">É criada uma função na linguagem que escolheu e que é executada todos os minutos.</span><span class="sxs-lookup"><span data-stu-id="02c1a-130">A function is created in your chosen language that runs every minute.</span></span>

3. <span data-ttu-id="02c1a-131">Certifique-se a execução através da visualização de informações de rastreio escritas toohello registos.</span><span class="sxs-lookup"><span data-stu-id="02c1a-131">Verify execution by viewing trace information written toohello logs.</span></span>

    ![As funções de início de sessão Visualizador Olá portal do Azure.](./media/functions-create-scheduled-function/functions-timer-trigger-view-logs2.png)

<span data-ttu-id="02c1a-133">Agora, pode alterar a agenda da função de Olá para que seja executado com menos frequência, por exemplo, uma vez a cada hora.</span><span class="sxs-lookup"><span data-stu-id="02c1a-133">Now, you can change hello function's schedule so that it runs less often, such as once every hour.</span></span> 

## <a name="update-hello-timer-schedule"></a><span data-ttu-id="02c1a-134">Atualizar o agendamento de temporizador Olá</span><span class="sxs-lookup"><span data-stu-id="02c1a-134">Update hello timer schedule</span></span>

1. <span data-ttu-id="02c1a-135">Expanda a função e clique em **Integrar**.</span><span class="sxs-lookup"><span data-stu-id="02c1a-135">Expand your function and click **Integrate**.</span></span> <span data-ttu-id="02c1a-136">Este é onde definir entrada e saída enlaces para a sua função e também definir agenda Olá.</span><span class="sxs-lookup"><span data-stu-id="02c1a-136">This is where you define input and output bindings for your function and also set hello schedule.</span></span> 

2. <span data-ttu-id="02c1a-137">Introduza um valor para **Agenda** novo de `0 0 */1 * * *` e clique em **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="02c1a-137">Enter a new **Schedule** value of `0 0 */1 * * *`, and then click **Save**.</span></span>  

![As funções de atualizar o agendamento de temporizador no Olá portal do Azure.](./media/functions-create-scheduled-function/functions-timer-trigger-change-schedule.png)

<span data-ttu-id="02c1a-139">Tem agora uma função que é executada uma vez por hora.</span><span class="sxs-lookup"><span data-stu-id="02c1a-139">You now have a function that runs once every hour.</span></span> 

## <a name="clean-up-resources"></a><span data-ttu-id="02c1a-140">Limpar recursos</span><span class="sxs-lookup"><span data-stu-id="02c1a-140">Clean up resources</span></span>

[!INCLUDE [Next steps note](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a><span data-ttu-id="02c1a-141">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="02c1a-141">Next steps</span></span>

<span data-ttu-id="02c1a-142">Criou uma função que é executada com base numa agenda.</span><span class="sxs-lookup"><span data-stu-id="02c1a-142">You have created a function that runs based on a schedule.</span></span>

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

<span data-ttu-id="02c1a-143">Para obter mais informações sobre os acionadores de temporizadores, veja [Schedule code execution with Azure Functions](functions-bindings-timer.md) (Agendar a execução de código com as Funções do Azure).</span><span class="sxs-lookup"><span data-stu-id="02c1a-143">For more information timer triggers, see [Schedule code execution with Azure Functions](functions-bindings-timer.md).</span></span>