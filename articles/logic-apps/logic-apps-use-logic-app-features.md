---
title: "aaaAdd condições e iniciar os fluxos de trabalho - Azure Logic Apps | Microsoft Docs"
description: "Controla a forma como fluxos de trabalho são executados no Azure Logic Apps adicionando lógica condicional, acionadores, ações e parâmetros."
author: stepsic-microsoft-com
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: e4e24de4-049a-4b3a-a14c-3bf3163287a8
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/28/2017
ms.author: LADocs; stepsic
ms.openlocfilehash: 76d5e44590ffa14cf70d7a93b99a241d286d555b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="use-logic-apps-features"></a><span data-ttu-id="48525-103">Utilizar funcionalidades das Logic Apps</span><span class="sxs-lookup"><span data-stu-id="48525-103">Use Logic Apps features</span></span>

<span data-ttu-id="48525-104">Num [tópico anterior](../logic-apps/logic-apps-create-a-logic-app.md), que criou a sua primeira aplicação lógica.</span><span class="sxs-lookup"><span data-stu-id="48525-104">In a [previous topic](../logic-apps/logic-apps-create-a-logic-app.md), you created your first logic app.</span></span> <span data-ttu-id="48525-105">toocontrol fluxo de trabalho da sua aplicação lógica, pode especificar diferentes caminhos para sua toorun de aplicação lógica e demasiado como processar os dados em matrizes, coleções e lotes.</span><span class="sxs-lookup"><span data-stu-id="48525-105">toocontrol your logic app's workflow, you can specify different paths for your logic app toorun and how too process data in arrays, collections, and batches.</span></span> <span data-ttu-id="48525-106">Pode incluir estes elementos no seu fluxo de trabalho de aplicação lógica:</span><span class="sxs-lookup"><span data-stu-id="48525-106">You can include these elements in your logic app workflow:</span></span>

* <span data-ttu-id="48525-107">Condições e [comutador instruções](../logic-apps/logic-apps-switch-case.md) permitem a sua aplicação lógica executar ações diferentes com base em se forem cumpridas condições específicas.</span><span class="sxs-lookup"><span data-stu-id="48525-107">Conditions and [switch statements](../logic-apps/logic-apps-switch-case.md) let your logic app run different actions based on whether specific conditions are met.</span></span>

* <span data-ttu-id="48525-108">[Ciclos](../logic-apps/logic-apps-loops-and-scopes.md) permitem a sua aplicação lógica executar passos repetidamente.</span><span class="sxs-lookup"><span data-stu-id="48525-108">[Loops](../logic-apps/logic-apps-loops-and-scopes.md) let your logic app run steps repeatedly.</span></span> <span data-ttu-id="48525-109">Por exemplo, pode repetir ações através de uma matriz ao utilizar um **For_each** ciclo.</span><span class="sxs-lookup"><span data-stu-id="48525-109">For example, you can repeat actions over an array when you use a **For_each** loop.</span></span> <span data-ttu-id="48525-110">Ou pode repetir ações até que a condição é cumprida quando utiliza um **até** ciclo.</span><span class="sxs-lookup"><span data-stu-id="48525-110">Or you can repeat actions until a condition is met when you use an **Until** loop.</span></span>

* <span data-ttu-id="48525-111">[Âmbitos](../logic-apps/logic-apps-loops-and-scopes.md) permitem agrupar série de ações em conjunto, por exemplo, o processamento de exceções tooimplement.</span><span class="sxs-lookup"><span data-stu-id="48525-111">[Scopes](../logic-apps/logic-apps-loops-and-scopes.md) let you group series of actions together, for example, tooimplement exception handling.</span></span>

* <span data-ttu-id="48525-112">[Debatching](../logic-apps/logic-apps-loops-and-scopes.md) permite que a sua aplicação lógica iniciar os fluxos de trabalho separados para os itens numa matriz quando utilizar Olá **SplitOn** comando.</span><span class="sxs-lookup"><span data-stu-id="48525-112">[Debatching](../logic-apps/logic-apps-loops-and-scopes.md) lets your logic app start separate workflows for items in an array when you use hello **SplitOn** command.</span></span>

<span data-ttu-id="48525-113">Este tópico apresenta alguns outros conceitos para criar uma aplicação lógica:</span><span class="sxs-lookup"><span data-stu-id="48525-113">This topic introduces other concepts for building your logic app:</span></span>

* <span data-ttu-id="48525-114">Código de vista tooedit uma aplicação lógica existente</span><span class="sxs-lookup"><span data-stu-id="48525-114">Code view tooedit an existing logic app</span></span>
* <span data-ttu-id="48525-115">Opções de início de um fluxo de trabalho</span><span class="sxs-lookup"><span data-stu-id="48525-115">Options for starting a workflow</span></span>

## <a name="conditions-run-steps-only-after-meeting-a-condition"></a><span data-ttu-id="48525-116">Condições: Passos de execução apenas depois de reunião, uma condição</span><span class="sxs-lookup"><span data-stu-id="48525-116">Conditions: Run steps only after meeting a condition</span></span>

<span data-ttu-id="48525-117">toohave a sua aplicação lógica executar passos apenas quando os dados satisfazem critérios específicos, pode adicionar uma condição que compara os dados no fluxo de trabalho Olá contra campos específicos ou valores.</span><span class="sxs-lookup"><span data-stu-id="48525-117">toohave your logic app run steps only when data meets specific criteria, you can add a condition that compares data in hello workflow against specific fields or values.</span></span>

<span data-ttu-id="48525-118">Por exemplo, suponha que tem uma aplicação lógica que envia demasiadas mensagens de correio eletrónico para publicações no feed RSS de um Web site.</span><span class="sxs-lookup"><span data-stu-id="48525-118">For example, suppose you have a logic app that sends you too many emails for posts on a website's RSS feed.</span></span> <span data-ttu-id="48525-119">Pode adicionar uma condição para que a sua aplicação lógica envia correio eletrónico apenas quando publicar Olá nova categoria específica de tooa pertence.</span><span class="sxs-lookup"><span data-stu-id="48525-119">You can add a condition so that your logic app sends email only when hello new post belongs tooa specific category.</span></span>

1. <span data-ttu-id="48525-120">No Olá [portal do Azure](https://portal.azure.com), localize e abra a sua aplicação lógica no Designer de aplicação lógica.</span><span class="sxs-lookup"><span data-stu-id="48525-120">In hello [Azure portal](https://portal.azure.com), find and open your logic app in Logic App Designer.</span></span>

2. <span data-ttu-id="48525-121">Adicione uma localização de fluxo de trabalho do toohello a condição que pretende.</span><span class="sxs-lookup"><span data-stu-id="48525-121">Add a condition toohello workflow location that you want.</span></span> 

   <span data-ttu-id="48525-122">condição de Olá tooadd entre passos existentes no fluxo de trabalho do app do lógica de Olá, mova o ponteiro de Olá através de seta de olá onde pretende que a condição de Olá tooadd.</span><span class="sxs-lookup"><span data-stu-id="48525-122">tooadd hello condition between existing steps in hello logic app workflow, move hello pointer over hello arrow where you want tooadd hello condition.</span></span> 
   <span data-ttu-id="48525-123">Escolha Olá **sinal** (**+**), em seguida, escolha **adicionar uma condição**.</span><span class="sxs-lookup"><span data-stu-id="48525-123">Choose hello **plus sign** (**+**), then choose **Add a condition**.</span></span> <span data-ttu-id="48525-124">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="48525-124">For example:</span></span>

   ![Adicionar condição toologic aplicação](./media/logic-apps-use-logic-app-features/add-condition.png)

   > [!NOTE]
   > <span data-ttu-id="48525-126">Se quiser tooadd uma condição no fim de Olá do seu fluxo de trabalho atual, aceda toohello inferior da sua aplicação lógica e escolha **+ novo passo**.</span><span class="sxs-lookup"><span data-stu-id="48525-126">If you want tooadd a condition at hello end of your current workflow, go toohello bottom of your logic app, and choose **+ New step**.</span></span>

3. <span data-ttu-id="48525-127">Agora defina condição Olá.</span><span class="sxs-lookup"><span data-stu-id="48525-127">Now define hello condition.</span></span> <span data-ttu-id="48525-128">Especificar o campo de origem de Olá que pretende que o tooevaluate, Olá operação tooperform e o valor de destino Olá ou campo.</span><span class="sxs-lookup"><span data-stu-id="48525-128">Specify hello source field that you want tooevaluate, hello operation tooperform, and hello target value or field.</span></span> <span data-ttu-id="48525-129">tooadd existente campos tooyour condição, escolha Olá **lista de conteúdo dinâmica adicionar**.</span><span class="sxs-lookup"><span data-stu-id="48525-129">tooadd existing fields tooyour condition, choose from hello **Add dynamic content list**.</span></span>

   <span data-ttu-id="48525-130">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="48525-130">For example:</span></span>

   ![Editar condição no modo básico](./media/logic-apps-use-logic-app-features/edit-condition-basic-mode.png)

   <span data-ttu-id="48525-132">Segue-se a condição concluída Olá:</span><span class="sxs-lookup"><span data-stu-id="48525-132">Here's hello complete condition:</span></span>

   ![Condição concluída](./media/logic-apps-use-logic-app-features/edit-condition-basic-mode-2.png)

   > [!TIP]
   > <span data-ttu-id="48525-134">condição de Olá toodefine no código, escolha **editar no modo avançado**.</span><span class="sxs-lookup"><span data-stu-id="48525-134">toodefine hello condition in code, choose **Edit in advanced mode**.</span></span> <span data-ttu-id="48525-135">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="48525-135">For example:</span></span>
   > 
   > ![Editar condição no código](./media/logic-apps-use-logic-app-features/edit-condition-advanced-mode.png)

4. <span data-ttu-id="48525-137">Em **se Sim** e **não se**, adicionar Olá passos tooperform com base em se Olá condição é cumprida.</span><span class="sxs-lookup"><span data-stu-id="48525-137">Under **IF YES** and **IF NO**, add hello steps tooperform based on whether hello condition is met.</span></span>

   <span data-ttu-id="48525-138">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="48525-138">For example:</span></span>

   ![Condição com Sim e não existem caminhos](./media/logic-apps-use-logic-app-features/condition-yes-no-path.png)

   > [!TIP]
   > <span data-ttu-id="48525-140">Pode arrastar ações existentes para Olá **se Sim** e **não se** caminhos.</span><span class="sxs-lookup"><span data-stu-id="48525-140">You can drag existing actions into hello **IF YES** and **IF NO** paths.</span></span>

5. <span data-ttu-id="48525-141">Quando tiver terminado, guarde a aplicação lógica.</span><span class="sxs-lookup"><span data-stu-id="48525-141">When you're done, save your logic app.</span></span>

<span data-ttu-id="48525-142">Agora receber e-mails apenas quando Olá cronologia satisfaz a condição.</span><span class="sxs-lookup"><span data-stu-id="48525-142">Now you get emails only when hello posts meet your condition.</span></span>

## <a name="repeat-actions-over-a-list-with-foreach"></a><span data-ttu-id="48525-143">Repetir ações através de uma lista com forEach</span><span class="sxs-lookup"><span data-stu-id="48525-143">Repeat actions over a list with forEach</span></span>

<span data-ttu-id="48525-144">ciclo de forEach Olá Especifica um toorepeat de matriz uma ação ao longo.</span><span class="sxs-lookup"><span data-stu-id="48525-144">hello forEach loop specifies an array toorepeat an action over.</span></span> <span data-ttu-id="48525-145">Se não for uma matriz, o fluxo de Olá falha.</span><span class="sxs-lookup"><span data-stu-id="48525-145">If it is not an array, hello flow fails.</span></span> <span data-ttu-id="48525-146">Por exemplo, se tiver action1 devolve uma matriz de mensagens e quiser toosend cada mensagem, pode incluir esta declaração de forEach nas propriedades de Olá a ação:`forEach : "@action('action1').outputs.messages"`</span><span class="sxs-lookup"><span data-stu-id="48525-146">For example, if you have action1 that outputs an array of messages, and you want toosend each message, you can include this forEach statement in hello properties of your action: `forEach : "@action('action1').outputs.messages"`</span></span>

## <a name="edit-hello-code-definition-for-a-logic-app"></a><span data-ttu-id="48525-147">Editar definição de código Olá para uma aplicação lógica</span><span class="sxs-lookup"><span data-stu-id="48525-147">Edit hello code definition for a logic app</span></span>

<span data-ttu-id="48525-148">Embora tenham Olá Designer de aplicação lógica, pode editar diretamente o código de Olá que define uma aplicação lógica.</span><span class="sxs-lookup"><span data-stu-id="48525-148">Although you have hello Logic App Designer, you can directly edit hello code that defines a logic app.</span></span>

1. <span data-ttu-id="48525-149">Na barra de comando Olá, escolha **Code vista**.</span><span class="sxs-lookup"><span data-stu-id="48525-149">On hello command bar, choose **Code view**.</span></span>

    <span data-ttu-id="48525-150">Um editor de completo abre-se e mostra a definição de Olá editasse.</span><span class="sxs-lookup"><span data-stu-id="48525-150">A full editor opens and shows hello definition you edited.</span></span>

    ![Vista de código](media/logic-apps-use-logic-app-features/codeview.png)

    <span data-ttu-id="48525-152">No editor de texto Olá, pode copiar e colar qualquer número de ações na Olá mesma aplicação de lógica ou entre as logic apps.</span><span class="sxs-lookup"><span data-stu-id="48525-152">In hello text editor, you can copy and paste any number of actions within hello same logic app or between logic apps.</span></span> 
    <span data-ttu-id="48525-153">Pode também facilmente adicionar ou remover secções todos a definição de Olá, e também pode partilhar as definições com outras pessoas.</span><span class="sxs-lookup"><span data-stu-id="48525-153">You can also easily add or remove entire sections from hello definition, and you can also share definitions with others.</span></span>

2. <span data-ttu-id="48525-154">Escolha as edições de toosave **guardar**.</span><span class="sxs-lookup"><span data-stu-id="48525-154">toosave your edits, choose **Save**.</span></span>

## <a name="parameters"></a><span data-ttu-id="48525-155">Parâmetros</span><span class="sxs-lookup"><span data-stu-id="48525-155">Parameters</span></span>

<span data-ttu-id="48525-156">Algumas capacidades de Logic Apps estão disponíveis apenas na vista de código, por exemplo, os parâmetros.</span><span class="sxs-lookup"><span data-stu-id="48525-156">Some Logic Apps capabilities are available only in code view, for example, parameters.</span></span> <span data-ttu-id="48525-157">Os parâmetros tornam mais fácil tooreuse valores em toda a sua aplicação lógica.</span><span class="sxs-lookup"><span data-stu-id="48525-157">Parameters make it easy tooreuse values throughout your logic app.</span></span> <span data-ttu-id="48525-158">Por exemplo, se tiver um endereço de e-mail que pretende utilizar nas várias ações, deve definir esse endereço de e-mail como um parâmetro.</span><span class="sxs-lookup"><span data-stu-id="48525-158">For example, if you have an email address that you want use in several actions, you should define that email address as a parameter.</span></span>

<span data-ttu-id="48525-159">Os parâmetros são ideais para extrair os valores que são muito provavelmente toochange.</span><span class="sxs-lookup"><span data-stu-id="48525-159">Parameters are good for pulling out values that you are likely toochange a lot.</span></span> <span data-ttu-id="48525-160">São particularmente úteis quando necessitar de parâmetros de toooverride em ambientes diferentes.</span><span class="sxs-lookup"><span data-stu-id="48525-160">They are especially useful when you need toooverride parameters in different environments.</span></span> <span data-ttu-id="48525-161">toolearn como parâmetros de toooverride com base no ambiente, consulte [criar definições da aplicação lógica](../logic-apps/logic-apps-author-definitions.md) e [documentação da REST API](https://docs.microsoft.com/rest/api/logic).</span><span class="sxs-lookup"><span data-stu-id="48525-161">toolearn how toooverride parameters based on environment, see [Author logic app definitions](../logic-apps/logic-apps-author-definitions.md) and [REST API documentation](https://docs.microsoft.com/rest/api/logic).</span></span>

<span data-ttu-id="48525-162">Este exemplo mostra como tooupdate sua aplicação lógica existente para que possa utilizar os parâmetros de termo de consulta Olá.</span><span class="sxs-lookup"><span data-stu-id="48525-162">This example shows how tooupdate your existing logic app so that you can use parameters for hello query term.</span></span>

1. <span data-ttu-id="48525-163">Na vista de código, determinar Olá `parameters : {}` de objeto e adicionar um `currentFeedUrl` objeto:</span><span class="sxs-lookup"><span data-stu-id="48525-163">In code view, find hello `parameters : {}` object, and add a `currentFeedUrl` object:</span></span>

        "currentFeedUrl" : {
            "type" : "string",
            "defaultValue" : "http://rss.cnn.com/rss/cnn_topstories.rss"
        }

2. <span data-ttu-id="48525-164">Aceda toohello `When_a_feed-item_is_published` ação, localizar Olá `queries` secção e substitua o valor de consulta Olá com:`"feedUrl": "#@{parameters('currentFeedUrl')}"`</span><span class="sxs-lookup"><span data-stu-id="48525-164">Go toohello `When_a_feed-item_is_published` action, find hello `queries` section, and replace hello query value with : `"feedUrl": "#@{parameters('currentFeedUrl')}"`</span></span> 

    <span data-ttu-id="48525-165">toojoin dois ou mais cadeias, também pode utilizar Olá `concat` função.</span><span class="sxs-lookup"><span data-stu-id="48525-165">toojoin two or more strings, you can also use hello `concat` function.</span></span> 
    <span data-ttu-id="48525-166">Por exemplo, `"@concat('#',parameters('currentFeedUrl'))"` funciona Olá mesmo como Olá acima.</span><span class="sxs-lookup"><span data-stu-id="48525-166">For example, `"@concat('#',parameters('currentFeedUrl'))"` works hello same as hello above.</span></span>

3.  <span data-ttu-id="48525-167">Quando tiver terminado, escolha **guardar**.</span><span class="sxs-lookup"><span data-stu-id="48525-167">When you're done, choose **Save**.</span></span> 

    <span data-ttu-id="48525-168">Agora pode alterar o feed através da transmissão de um URL diferente através de Olá RSS do Web site Olá `currentFeedURL` objeto.</span><span class="sxs-lookup"><span data-stu-id="48525-168">Now you can change hello website's RSS feed by passing a different URL through hello `currentFeedURL` object.</span></span>

<span data-ttu-id="48525-169">Saiba mais sobre [como definições da aplicação lógica tooauthor](../logic-apps/logic-apps-author-definitions.md).</span><span class="sxs-lookup"><span data-stu-id="48525-169">Learn more about [how tooauthor logic app definitions](../logic-apps/logic-apps-author-definitions.md).</span></span>

## <a name="start-logic-app-workflows"></a><span data-ttu-id="48525-170">Iniciar os fluxos de trabalho de aplicação de lógica</span><span class="sxs-lookup"><span data-stu-id="48525-170">Start logic app workflows</span></span>

<span data-ttu-id="48525-171">Ter diferentes opções para iniciar o fluxo de trabalho Olá definido na sua aplicação lógica.</span><span class="sxs-lookup"><span data-stu-id="48525-171">You have different options for starting hello workflow defined in your logic app.</span></span> <span data-ttu-id="48525-172">Pode sempre iniciar uma fluxo de trabalho a pedido no Olá [portal do Azure].</span><span class="sxs-lookup"><span data-stu-id="48525-172">You can always start a workflow on-demand in hello [Azure portal].</span></span>

### <a name="recurrence-triggers"></a><span data-ttu-id="48525-173">Acionadores de periodicidade</span><span class="sxs-lookup"><span data-stu-id="48525-173">Recurrence triggers</span></span>

<span data-ttu-id="48525-174">Um acionador de recorrência é executada com intervalo que especificou.</span><span class="sxs-lookup"><span data-stu-id="48525-174">A recurrence trigger runs at an interval that you specify.</span></span> <span data-ttu-id="48525-175">Quando o acionador de Olá tem lógica condicional, acionador Olá determina se o fluxo de trabalho Olá tem toorun.</span><span class="sxs-lookup"><span data-stu-id="48525-175">When hello trigger has conditional logic, hello trigger determines whether hello workflow needs toorun.</span></span> <span data-ttu-id="48525-176">Um acionador indica deve executar o fluxo de trabalho Olá devolvendo um `200` código de estado.</span><span class="sxs-lookup"><span data-stu-id="48525-176">A trigger indicates hello workflow should run by returning a `200` status code.</span></span> <span data-ttu-id="48525-177">Quando o fluxo de trabalho Olá não necessita de toorun, acionador Olá devolve um `202` código de estado.</span><span class="sxs-lookup"><span data-stu-id="48525-177">When hello workflow doesn't need toorun, hello trigger returns a `202` status code.</span></span>

### <a name="callback-using-rest-apis"></a><span data-ttu-id="48525-178">Chamada de retorno com REST APIs</span><span class="sxs-lookup"><span data-stu-id="48525-178">Callback using REST APIs</span></span>

<span data-ttu-id="48525-179">toostart um fluxo de trabalho, os serviços podem chamar um ponto final da aplicação lógica.</span><span class="sxs-lookup"><span data-stu-id="48525-179">toostart a workflow, services can call a logic app endpoint.</span></span> <span data-ttu-id="48525-180">toostart este tipo de lógica aplicação a pedido, escolha **executar agora** na barra de comandos Olá.</span><span class="sxs-lookup"><span data-stu-id="48525-180">toostart this kind of logic app on-demand, choose **Run now** on hello command bar.</span></span> <span data-ttu-id="48525-181">Consulte [iniciar os fluxos de trabalho chamando lógica pontos finais de aplicação como acionadores](../logic-apps/logic-apps-http-endpoint.md).</span><span class="sxs-lookup"><span data-stu-id="48525-181">See [Start workflows by calling logic app endpoints as triggers](../logic-apps/logic-apps-http-endpoint.md).</span></span> 

<!-- Shared links -->
[portal do Azure]: https://portal.azure.com

## <a name="next-steps"></a><span data-ttu-id="48525-183">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="48525-183">Next steps</span></span>

* [<span data-ttu-id="48525-184">Instruções de comutador</span><span class="sxs-lookup"><span data-stu-id="48525-184">Switch statements</span></span>](../logic-apps/logic-apps-switch-case.md) 
* [<span data-ttu-id="48525-185">Ciclos, âmbitos e divisões</span><span class="sxs-lookup"><span data-stu-id="48525-185">Loops, scopes, and debatching</span></span>](../logic-apps/logic-apps-loops-and-scopes.md)
* [<span data-ttu-id="48525-186">Criar definições de aplicação lógica</span><span class="sxs-lookup"><span data-stu-id="48525-186">Author logic app definitions</span></span>](../logic-apps/logic-apps-author-definitions.md)