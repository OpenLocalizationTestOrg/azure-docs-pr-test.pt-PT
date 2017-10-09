---
title: "aaaError & processamento de exceções - Azure Logic Apps | Microsoft Docs"
description: "Padrões de erro e excepção a processar no Azure Logic Apps"
services: logic-apps
documentationcenter: .net,nodejs,java
author: jeffhollan
manager: anneta
editor: 
ms.assetid: e50ab2f2-1fdc-4d2a-be40-995a6cc5a0d4
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 10/18/2016
ms.author: LADocs; jehollan
ms.openlocfilehash: 326a252310c8dfb154e583f91c9421675e448d1f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="handle-errors-and-exceptions-in-azure-logic-apps"></a><span data-ttu-id="a1fe5-103">Processar os erros e exceções no Azure Logic Apps</span><span class="sxs-lookup"><span data-stu-id="a1fe5-103">Handle errors and exceptions in Azure Logic Apps</span></span>

<span data-ttu-id="a1fe5-104">Aplicações lógicas do Azure fornece ferramentas avançadas e padrões toohelp, certificar-se que a integrações são resilientes contra falhas e robusto.</span><span class="sxs-lookup"><span data-stu-id="a1fe5-104">Azure Logic Apps provides rich tools and patterns toohelp you make sure your integrations are robust and resilient against failures.</span></span> <span data-ttu-id="a1fe5-105">Qualquer arquitetura de integração pode representar um desafio de Olá de efetuar o período de indisponibilidade do tooappropriately se identificador ou problemas de sistemas dependentes.</span><span class="sxs-lookup"><span data-stu-id="a1fe5-105">Any integration architecture poses hello challenge of making sure tooappropriately handle downtime or issues from dependent systems.</span></span> <span data-ttu-id="a1fe5-106">Logic Apps torna processamento de erros de uma experiência de primeira classe, dando-lhe Olá ferramentas terá tooact em exceções e erros nos seus fluxos de trabalho.</span><span class="sxs-lookup"><span data-stu-id="a1fe5-106">Logic Apps makes handling errors a first-class experience, giving you hello tools you need tooact on exceptions and errors in your workflows.</span></span>

## <a name="retry-policies"></a><span data-ttu-id="a1fe5-107">Repita políticas</span><span class="sxs-lookup"><span data-stu-id="a1fe5-107">Retry policies</span></span>

<span data-ttu-id="a1fe5-108">Uma política de repetição é tipo mais básico do Olá de exceção e processamento de erros.</span><span class="sxs-lookup"><span data-stu-id="a1fe5-108">A retry policy is hello most basic type of exception and error handling.</span></span> <span data-ttu-id="a1fe5-109">Se um pedido inicial foi excedido ou falha (qualquer pedido que resulte num 429 ou resposta 5xx), esta política define se a ação de Olá deve repetir.</span><span class="sxs-lookup"><span data-stu-id="a1fe5-109">If an initial request timed out or failed (any request that results in a 429 or 5xx response), this policy defines whether hello action should retry.</span></span> <span data-ttu-id="a1fe5-110">Por predefinição, todas as ações repetir 4 vezes adicionais sobre os intervalos de 20 segundo.</span><span class="sxs-lookup"><span data-stu-id="a1fe5-110">By default, all actions retry 4 additional times over 20-second intervals.</span></span> <span data-ttu-id="a1fe5-111">Por isso, caso o primeiro pedido efetuado Olá recebe um `500 Internal Server Error` resposta, o motor de fluxo de trabalho de Olá interrompe para 20 segundos e tentativas Olá pedido novamente.</span><span class="sxs-lookup"><span data-stu-id="a1fe5-111">So if hello first request receives a `500 Internal Server Error` response, hello workflow engine pauses for 20 seconds, and attempts hello request again.</span></span> <span data-ttu-id="a1fe5-112">Se depois de todas as tentativas, resposta Olá ainda é uma exceção ou falha, o fluxo de trabalho Olá continua e marcas de escala Olá estado da ação como `Failed`.</span><span class="sxs-lookup"><span data-stu-id="a1fe5-112">If after all retries, hello response is still an exception or failure, hello workflow continues and marks hello action status as `Failed`.</span></span>

<span data-ttu-id="a1fe5-113">Pode configurar as políticas de repetição no Olá **entradas** para uma ação específica.</span><span class="sxs-lookup"><span data-stu-id="a1fe5-113">You can configure retry policies in hello **inputs** for a particular action.</span></span> <span data-ttu-id="a1fe5-114">Por exemplo, pode configurar um tootry de política de repetição máximo de 4 horas através de intervalos de 1 hora.</span><span class="sxs-lookup"><span data-stu-id="a1fe5-114">For example, you can configure a retry policy tootry as many as 4 times over 1-hour intervals.</span></span> <span data-ttu-id="a1fe5-115">Para obter detalhes completos sobre as propriedades de entrada, consulte [ações de fluxo de trabalho e é acionado][retryPolicyMSDN].</span><span class="sxs-lookup"><span data-stu-id="a1fe5-115">For full details about input properties, see [Workflow Actions and Triggers][retryPolicyMSDN].</span></span>

```json
"retryPolicy" : {
      "type": "<type-of-retry-policy>",
      "interval": <retry-interval>,
      "count": <number-of-retry-attempts>
    }
```

<span data-ttu-id="a1fe5-116">Se pretendia sua tooretry de ação de HTTP 4 vezes e aguarde 10 minutos entre cada tentativa, utilizaria Olá definição os seguintes:</span><span class="sxs-lookup"><span data-stu-id="a1fe5-116">If you wanted your HTTP action tooretry 4 times and wait 10 minutes between each attempt, you would use hello following definition:</span></span>

```json
"HTTP": 
{
    "inputs": {
        "method": "GET",
        "uri": "http://myAPIendpoint/api/action",
        "retryPolicy" : {
            "type": "fixed",
            "interval": "PT10M",
            "count": 4
        }
    },
    "runAfter": {},
    "type": "Http"
}
```

<span data-ttu-id="a1fe5-117">Para obter mais informações sobre a sintaxe suportado, consulte Olá [secção política de repetição ações de fluxo de trabalho e é acionado][retryPolicyMSDN].</span><span class="sxs-lookup"><span data-stu-id="a1fe5-117">For more information on supported syntax, see hello [retry-policy section in Workflow Actions and Triggers][retryPolicyMSDN].</span></span>

## <a name="catch-failures-with-hello-runafter-property"></a><span data-ttu-id="a1fe5-118">Detetar falhas com Olá RunAfter propriedade</span><span class="sxs-lookup"><span data-stu-id="a1fe5-118">Catch failures with hello RunAfter property</span></span>

<span data-ttu-id="a1fe5-119">Cada ação de aplicação lógica declara que ações devem ser concluído antes de iniciado o ação Olá, como a ordenação passos Olá no fluxo de trabalho.</span><span class="sxs-lookup"><span data-stu-id="a1fe5-119">Each logic app action declares which actions must finish before hello action starts, like ordering hello steps in your workflow.</span></span> <span data-ttu-id="a1fe5-120">Na definição de ação de Olá, esta ordem é conhecido como Olá `runAfter` propriedade.</span><span class="sxs-lookup"><span data-stu-id="a1fe5-120">In hello action definition, this ordering is known as hello `runAfter` property.</span></span> <span data-ttu-id="a1fe5-121">Esta propriedade é um objeto que descreve quais as ações e Estados de ação executar a ação de Olá.</span><span class="sxs-lookup"><span data-stu-id="a1fe5-121">This property is an object that describes which actions and action statuses execute hello action.</span></span> <span data-ttu-id="a1fe5-122">Por predefinição, todas as ações adicionadas através do Designer de aplicação de lógica de Olá estiverem definidas demasiado`runAfter` passo anterior de Olá se hello passo anterior `Succeeded`.</span><span class="sxs-lookup"><span data-stu-id="a1fe5-122">By default, all actions added through hello Logic App Designer are set too`runAfter` hello previous step if hello previous step `Succeeded`.</span></span> <span data-ttu-id="a1fe5-123">No entanto, pode personalizar esta ações de toofire valor quando têm ações anteriores `Failed`, `Skipped`, ou um conjunto possíveis destes valores.</span><span class="sxs-lookup"><span data-stu-id="a1fe5-123">However, you can customize this value toofire actions when previous actions have `Failed`, `Skipped`, or a possible set of these values.</span></span> <span data-ttu-id="a1fe5-124">Se pretendesse tooadd tooa um item designado tópico do Service Bus após uma ação específica `Insert_Row` falhar, pode utilizar Olá seguir `runAfter` configuração:</span><span class="sxs-lookup"><span data-stu-id="a1fe5-124">If you wanted tooadd an item tooa designated Service Bus topic after a specific action `Insert_Row` fails, you could use hello following `runAfter` configuration:</span></span>

```json
"Send_message": {
    "inputs": {
        "body": {
            "ContentData": "@{encodeBase64(body('Insert_Row'))}",
            "ContentType": "{ \"content-type\" : \"application/json\" }"
        },
        "host": {
            "api": {
                "runtimeUrl": "https://logic-apis-westus.azure-apim.net/apim/servicebus"
            },
            "connection": {
                "name": "@parameters('$connections')['servicebus']['connectionId']"
            }
        },
        "method": "post",
        "path": "/@{encodeURIComponent('failures')}/messages"
    },
    "runAfter": {
        "Insert_Row": [
            "Failed"
        ]
    }
}
```

<span data-ttu-id="a1fe5-125">Olá aviso `runAfter` é definir a propriedade toofire se hello `Insert_Row` é ação `Failed`.</span><span class="sxs-lookup"><span data-stu-id="a1fe5-125">Notice hello `runAfter` property is set toofire if hello `Insert_Row` action is `Failed`.</span></span> <span data-ttu-id="a1fe5-126">ação de Olá toorun se for o estado da ação Olá `Succeeded`, `Failed`, ou `Skipped`, utilizam esta sintaxe:</span><span class="sxs-lookup"><span data-stu-id="a1fe5-126">toorun hello action if hello action status is `Succeeded`, `Failed`, or `Skipped`, use this syntax:</span></span>

```json
"runAfter": {
        "Insert_Row": [
            "Failed", "Succeeded", "Skipped"
        ]
    }
```

> [!TIP]
> <span data-ttu-id="a1fe5-127">Ações que executaram e concluir com êxito após ter uma ação anterior tenha falhado, estão marcados como `Succeeded`.</span><span class="sxs-lookup"><span data-stu-id="a1fe5-127">Actions that run and complete successfully after a preceding action has failed, are marked as `Succeeded`.</span></span> <span data-ttu-id="a1fe5-128">Isto significa de comportamento se a com êxito catch todas as falhas no fluxo de trabalho, Olá ser executado automaticamente está marcada como `Succeeded`.</span><span class="sxs-lookup"><span data-stu-id="a1fe5-128">This behavior means that if you successfully catch all failures in a workflow, hello run itself is marked as `Succeeded`.</span></span>

## <a name="scopes-and-results-tooevaluate-actions"></a><span data-ttu-id="a1fe5-129">Ações de tooevaluate âmbitos e resultados</span><span class="sxs-lookup"><span data-stu-id="a1fe5-129">Scopes and results tooevaluate actions</span></span>

<span data-ttu-id="a1fe5-130">Toohow semelhante pode executar após ações individuais, pode também agrupar ações em conjunto no interior de um [âmbito](../logic-apps/logic-apps-loops-and-scopes.md), que atua como um agrupamento lógico das ações.</span><span class="sxs-lookup"><span data-stu-id="a1fe5-130">Similar toohow you can run after individual actions, you can also group actions together inside a [scope](../logic-apps/logic-apps-loops-and-scopes.md), which act as a logical grouping of actions.</span></span> <span data-ttu-id="a1fe5-131">Âmbitos são úteis para organizar as suas ações de aplicação lógica tanto para efetuar avaliações do agregado num Estado de Olá de um âmbito.</span><span class="sxs-lookup"><span data-stu-id="a1fe5-131">Scopes are useful both for organizing your logic app actions, and for performing aggregate evaluations on hello status of a scope.</span></span> <span data-ttu-id="a1fe5-132">âmbito de Olá próprio recebe um Estado depois de terminar todas as ações de um âmbito.</span><span class="sxs-lookup"><span data-stu-id="a1fe5-132">hello scope itself receives a status after all actions in a scope have finished.</span></span> <span data-ttu-id="a1fe5-133">Estado de âmbito de Olá é determinado com Olá mesmos critérios como uma execução.</span><span class="sxs-lookup"><span data-stu-id="a1fe5-133">hello scope status is determined with hello same criteria as a run.</span></span> <span data-ttu-id="a1fe5-134">Se é Olá ação final um ramo de execução `Failed` ou `Aborted`, estado de Olá é `Failed`.</span><span class="sxs-lookup"><span data-stu-id="a1fe5-134">If hello final action in an execution branch is `Failed` or `Aborted`, hello status is `Failed`.</span></span>

<span data-ttu-id="a1fe5-135">toofire ações específicas para quaisquer falhas que tenham acontecido dentro do âmbito de Olá, pode utilizar `runAfter` com um âmbito que está marcado como `Failed`.</span><span class="sxs-lookup"><span data-stu-id="a1fe5-135">toofire specific actions for any failures that happened within hello scope, you can use `runAfter` with a scope that is marked `Failed`.</span></span> <span data-ttu-id="a1fe5-136">Se *qualquer* ações no âmbito de Olá falharem, executar após a falha de um âmbito permite criar uma única ação toocatch falhas.</span><span class="sxs-lookup"><span data-stu-id="a1fe5-136">If *any* actions in hello scope fail, running after a scope fails lets you create a single action toocatch failures.</span></span>

### <a name="getting-hello-context-of-failures-with-results"></a><span data-ttu-id="a1fe5-137">Obter Olá contexto de falhas com resultados</span><span class="sxs-lookup"><span data-stu-id="a1fe5-137">Getting hello context of failures with results</span></span>

<span data-ttu-id="a1fe5-138">Embora a deteção de falhas de um âmbito é útil, pode também querer toohelp contexto que compreender exatamente as ações de falha, e quaisquer erros ou códigos de estado que foram devolvidos.</span><span class="sxs-lookup"><span data-stu-id="a1fe5-138">Although catching failures from a scope is useful, you might also want context toohelp you understand exactly which actions failed, and any errors or status codes that were returned.</span></span> <span data-ttu-id="a1fe5-139">Olá `@result()` função de fluxo de trabalho fornece o contexto sobre resultado Olá de todas as ações de um âmbito.</span><span class="sxs-lookup"><span data-stu-id="a1fe5-139">hello `@result()` workflow function provides context about hello result of all actions in a scope.</span></span>

<span data-ttu-id="a1fe5-140">`@result()`assume um parâmetro único, o nome de âmbito e devolve uma matriz de todos os resultados de ação de Olá do dentro esse âmbito.</span><span class="sxs-lookup"><span data-stu-id="a1fe5-140">`@result()` takes a single parameter, scope name, and returns an array of all hello action results from within that scope.</span></span> <span data-ttu-id="a1fe5-141">Estes objetos de ação incluem Olá mesmo atributos como Olá `@actions()` produz de objeto, incluindo a hora de início de ação, hora de fim de ação, estado da ação, entradas de ação, correlação da ação IDs e ação.</span><span class="sxs-lookup"><span data-stu-id="a1fe5-141">These action objects include hello same attributes as hello `@actions()` object, including action start time, action end time, action status, action inputs, action correlation IDs, and action outputs.</span></span> <span data-ttu-id="a1fe5-142">contexto toosend todas as ações que falha dentro de um âmbito, emparelhar facilmente um `@result()` funcionar com uma `runAfter`.</span><span class="sxs-lookup"><span data-stu-id="a1fe5-142">toosend context of any actions that failed within a scope, you can easily pair an `@result()` function with a `runAfter`.</span></span>

<span data-ttu-id="a1fe5-143">tooexecute uma ação *para cada* ação num âmbito que `Failed`, a matriz de Olá de filtro de resultados tooactions que falharam, pode ser emparelhado `@result()` com um  **[filtro matriz](../connectors/connectors-native-query.md)**  ação e um  **[ForEach](../logic-apps/logic-apps-loops-and-scopes.md)**  ciclo.</span><span class="sxs-lookup"><span data-stu-id="a1fe5-143">tooexecute an action *for each* action in a scope that `Failed`, filter hello array of results tooactions that failed, you can pair `@result()` with a **[Filter Array](../connectors/connectors-native-query.md)** action and a **[ForEach](../logic-apps/logic-apps-loops-and-scopes.md)** loop.</span></span> <span data-ttu-id="a1fe5-144">Pode colocar a matriz de resultado filtrado Olá e efetuar uma ação para cada falha utilizando Olá **ForEach** ciclo.</span><span class="sxs-lookup"><span data-stu-id="a1fe5-144">You can take hello filtered result array and perform an action for each failure using hello **ForEach** loop.</span></span> <span data-ttu-id="a1fe5-145">Eis um exemplo, seguido por uma explicação detalhada, que envia um pedido POST de HTTP com o corpo da resposta Olá de todas as ações que falhou no âmbito de Olá `My_Scope`.</span><span class="sxs-lookup"><span data-stu-id="a1fe5-145">Here's an example, followed by a detailed explanation, that sends an HTTP POST request with hello response body of any actions that failed within hello scope `My_Scope`.</span></span>

```json
"Filter_array": {
    "inputs": {
        "from": "@result('My_Scope')",
        "where": "@equals(item()['status'], 'Failed')"
    },
    "runAfter": {
        "My_Scope": [
            "Failed"
        ]
    },
    "type": "Query"
},
"For_each": {
    "actions": {
        "Log_Exception": {
            "inputs": {
                "body": "@item()['outputs']['body']",
                "method": "POST",
                "headers": {
                    "x-failed-action-name": "@item()['name']",
                    "x-failed-tracking-id": "@item()['clientTrackingId']"
                },
                "uri": "http://requestb.in/"
            },
            "runAfter": {},
            "type": "Http"
        }
    },
    "foreach": "@body('Filter_array')",
    "runAfter": {
        "Filter_array": [
            "Succeeded"
        ]
    },
    "type": "Foreach"
}
```

<span data-ttu-id="a1fe5-146">Eis um toodescribe instruções detalhadas sobre o que acontece:</span><span class="sxs-lookup"><span data-stu-id="a1fe5-146">Here's a detailed walkthrough toodescribe what happens:</span></span>

1. <span data-ttu-id="a1fe5-147">resultado de Olá tooget de todas as ações dentro `My_Scope`, Olá **filtro matriz** filtros de ação `@result('My_Scope')`.</span><span class="sxs-lookup"><span data-stu-id="a1fe5-147">tooget hello result of all actions within `My_Scope`, hello **Filter Array** action filters `@result('My_Scope')`.</span></span>

2. <span data-ttu-id="a1fe5-148">Olá condição para **filtro matriz** alguma `@result()` item que tem o Estado igual demasiado`Failed`.</span><span class="sxs-lookup"><span data-stu-id="a1fe5-148">hello condition for **Filter Array** is any `@result()` item that has status equal too`Failed`.</span></span> <span data-ttu-id="a1fe5-149">Esta condição filtra matriz Olá com todos os resultados de ação de `My_Scope` tooan matriz com apenas os resultados de ação de falha.</span><span class="sxs-lookup"><span data-stu-id="a1fe5-149">This condition filters hello array with all action results from `My_Scope` tooan array with only failed action results.</span></span>

3. <span data-ttu-id="a1fe5-150">Efetuar uma **para cada** ação no Olá **filtrado matriz** produz.</span><span class="sxs-lookup"><span data-stu-id="a1fe5-150">Perform a **For Each** action on hello **Filtered Array** outputs.</span></span> <span data-ttu-id="a1fe5-151">Este passo executa uma ação *para cada* falhou o resultado da ação que foi filtrado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="a1fe5-151">This step performs an action *for each* failed action result that was previously filtered.</span></span>

    <span data-ttu-id="a1fe5-152">Se uma única ação no âmbito de Olá falhou, Olá ações no Olá `foreach` execute apenas uma vez.</span><span class="sxs-lookup"><span data-stu-id="a1fe5-152">If a single action in hello scope failed, hello actions in hello `foreach` run only once.</span></span> 
    <span data-ttu-id="a1fe5-153">Muitas ações falhadas causam uma ação por falha.</span><span class="sxs-lookup"><span data-stu-id="a1fe5-153">Many failed actions cause one action per failure.</span></span>

4. <span data-ttu-id="a1fe5-154">Enviar um HTTP POST em Olá `foreach` do item de corpo de resposta, ou `@item()['outputs']['body']`.</span><span class="sxs-lookup"><span data-stu-id="a1fe5-154">Send an HTTP POST on hello `foreach` item response body, or `@item()['outputs']['body']`.</span></span> <span data-ttu-id="a1fe5-155">Olá `@result()` forma item é Olá mesmo como Olá `@actions()` formam e pode ser analisado Olá mesma forma.</span><span class="sxs-lookup"><span data-stu-id="a1fe5-155">hello `@result()` item shape is hello same as hello `@actions()` shape, and can be parsed hello same way.</span></span>

5. <span data-ttu-id="a1fe5-156">Inclua dois cabeçalhos personalizados com o nome da ação falhada Olá `@item()['name']` e Olá falhou a execução cliente ID de controlo `@item()['clientTrackingId']`.</span><span class="sxs-lookup"><span data-stu-id="a1fe5-156">Include two custom headers with hello failed action name `@item()['name']` and hello failed run client tracking ID `@item()['clientTrackingId']`.</span></span>

<span data-ttu-id="a1fe5-157">Para referência, eis um exemplo de um único `@result()` item, que mostra Olá `name`, `body`, e `clientTrackingId` propriedades que são analisadas no exemplo anterior Olá.</span><span class="sxs-lookup"><span data-stu-id="a1fe5-157">For reference, here's an example of a single `@result()` item, showing hello `name`, `body`, and `clientTrackingId` properties that are parsed in hello previous example.</span></span> <span data-ttu-id="a1fe5-158">Fora de um `foreach`, `@result()` devolve uma matriz destes objetos.</span><span class="sxs-lookup"><span data-stu-id="a1fe5-158">Outside of a `foreach`, `@result()` returns an array of these objects.</span></span>

```json
{
    "name": "Example_Action_That_Failed",
    "inputs": {
        "uri": "https://myfailedaction.azurewebsites.net",
        "method": "POST"
    },
    "outputs": {
        "statusCode": 404,
        "headers": {
            "Date": "Thu, 11 Aug 2016 03:18:18 GMT",
            "Server": "Microsoft-IIS/8.0",
            "X-Powered-By": "ASP.NET",
            "Content-Length": "68",
            "Content-Type": "application/json"
        },
        "body": {
            "code": "ResourceNotFound",
            "message": "/docs/folder-name/resource-name does not exist"
        }
    },
    "startTime": "2016-08-11T03:18:19.7755341Z",
    "endTime": "2016-08-11T03:18:20.2598835Z",
    "trackingId": "bdd82e28-ba2c-4160-a700-e3a8f1a38e22",
    "clientTrackingId": "08587307213861835591296330354",
    "code": "NotFound",
    "status": "Failed"
}
```

<span data-ttu-id="a1fe5-159">padrões de processamento de exceções diferentes tooperform, pode utilizar expressões Olá apresentadas anteriormente.</span><span class="sxs-lookup"><span data-stu-id="a1fe5-159">tooperform different exception handling patterns, you can use hello expressions shown previously.</span></span> <span data-ttu-id="a1fe5-160">Poderá escolher tooexecute uma único excepção a processar a ação fora do âmbito de Olá que aceita matriz filtrado completo Olá de falhas e remover Olá `foreach`.</span><span class="sxs-lookup"><span data-stu-id="a1fe5-160">You might choose tooexecute a single exception handling action outside hello scope that accepts hello entire filtered array of failures, and remove hello `foreach`.</span></span> <span data-ttu-id="a1fe5-161">Também pode incluir outras propriedades útil de Olá `@result()` resposta apresentada anteriormente.</span><span class="sxs-lookup"><span data-stu-id="a1fe5-161">You can also include other useful properties from hello `@result()` response shown previously.</span></span>

## <a name="azure-diagnostics-and-telemetry"></a><span data-ttu-id="a1fe5-162">Telemetria e diagnóstico do Azure</span><span class="sxs-lookup"><span data-stu-id="a1fe5-162">Azure Diagnostics and telemetry</span></span>

<span data-ttu-id="a1fe5-163">Olá padrões anteriores são erros de toohandle excelente forma e exceções dentro de uma execução, mas também pode identificar e responder tooerrors independente da Olá ser executado automaticamente.</span><span class="sxs-lookup"><span data-stu-id="a1fe5-163">hello previous patterns are great way toohandle errors and exceptions within a run, but you can also identify and respond tooerrors independent of hello run itself.</span></span> 
<span data-ttu-id="a1fe5-164">[Diagnóstico do Azure](../logic-apps/logic-apps-monitor-your-logic-apps.md) fornece uma forma simples toosend todos os conta de armazenamento do Azure do tooan de eventos (incluindo todos os Estados de execução e a ação) do fluxo de trabalho ou de um Hub de eventos do Azure.</span><span class="sxs-lookup"><span data-stu-id="a1fe5-164">[Azure Diagnostics](../logic-apps/logic-apps-monitor-your-logic-apps.md) provides a simple way toosend all workflow events (including all run and action statuses) tooan Azure Storage account or an Azure Event Hub.</span></span> <span data-ttu-id="a1fe5-165">tooevaluate execute Estados, pode monitorizar as métricas e registos de Olá ou publicá-los em qualquer ferramenta monitorização que preferir.</span><span class="sxs-lookup"><span data-stu-id="a1fe5-165">tooevaluate run statuses, you can monitor hello logs and metrics, or publish them into any monitoring tool you prefer.</span></span> <span data-ttu-id="a1fe5-166">Uma opção de potencial é toostream todos os eventos de Olá através do Hub de eventos do Azure para [Stream Analytics](https://azure.microsoft.com/services/stream-analytics/).</span><span class="sxs-lookup"><span data-stu-id="a1fe5-166">One potential option is toostream all hello events through Azure Event Hub into [Stream Analytics](https://azure.microsoft.com/services/stream-analytics/).</span></span> <span data-ttu-id="a1fe5-167">No Stream Analytics, é possível escrever consultas em direto fora de quaisquer anomalias, médias ou falhas de Olá os registos de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="a1fe5-167">In Stream Analytics, you can write live queries off any anomalies, averages, or failures from hello diagnostic logs.</span></span> <span data-ttu-id="a1fe5-168">Do Stream Analytics pode facilmente saída tooother origens de dados como filas, tópicos, SQL Server, base de dados do Azure Cosmos e Power BI.</span><span class="sxs-lookup"><span data-stu-id="a1fe5-168">Stream Analytics can easily output tooother data sources like queues, topics, SQL, Azure Cosmos DB, and Power BI.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a1fe5-169">Passos Seguintes</span><span class="sxs-lookup"><span data-stu-id="a1fe5-169">Next Steps</span></span>

* [<span data-ttu-id="a1fe5-170">Veja como um cliente baseia-se com Azure Logic Apps de processamento de erros</span><span class="sxs-lookup"><span data-stu-id="a1fe5-170">See how a customer builds error handling with Azure Logic Apps</span></span>](../logic-apps/logic-apps-scenario-error-and-exception-handling.md)
* [<span data-ttu-id="a1fe5-171">Localizar mais cenários e exemplos de Logic Apps</span><span class="sxs-lookup"><span data-stu-id="a1fe5-171">Find more Logic Apps examples and scenarios</span></span>](../logic-apps/logic-apps-examples-and-scenarios.md)
* [<span data-ttu-id="a1fe5-172">Saiba como toocreate automatizada implementações para as logic apps</span><span class="sxs-lookup"><span data-stu-id="a1fe5-172">Learn how toocreate automated deployments for logic apps</span></span>](../logic-apps/logic-apps-create-deploy-template.md)
* [<span data-ttu-id="a1fe5-173">Criar e implementar aplicações lógicas com o Visual Studio</span><span class="sxs-lookup"><span data-stu-id="a1fe5-173">Build and deploy logic apps with Visual Studio</span></span>](logic-apps-deploy-from-vs.md)

<!-- References -->
[retryPolicyMSDN]: https://docs.microsoft.com/rest/api/logic/actions-and-triggers#Anchor_9
