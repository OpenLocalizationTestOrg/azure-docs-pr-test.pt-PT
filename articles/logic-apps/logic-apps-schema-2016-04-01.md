---
title: "aaaSchema de atualizações de Junho-1-2016 - Azure Logic Apps | Microsoft Docs"
description: "Criar definições de JSON para o Azure Logic Apps com a versão de esquema 2016-06-01"
author: jeffhollan
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: 349d57e8-f62b-4ec6-a92f-a6e0242d6c0e
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: H1Hack27Feb2017
ms.date: 07/25/2016
ms.author: LADocs; jehollan
ms.openlocfilehash: b0347fbbd692a93b63a2f8b741402a225450b35a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="schema-updates-for-azure-logic-apps---june-1-2016"></a><span data-ttu-id="54a1b-103">Atualizações do esquema para o Azure Logic Apps - 1 de Junho de 2016</span><span class="sxs-lookup"><span data-stu-id="54a1b-103">Schema updates for Azure Logic Apps - June 1, 2016</span></span>

<span data-ttu-id="54a1b-104">Este novo esquema e a API versão para o Azure Logic Apps inclui melhoramentos essenciais que tornam as logic apps mais toouse mais fácil e fiável:</span><span class="sxs-lookup"><span data-stu-id="54a1b-104">This new schema and API version for Azure Logic Apps includes key improvements that make logic apps more reliable and easier toouse:</span></span>

* <span data-ttu-id="54a1b-105">[Âmbitos](#scopes) permitem-lhe agrupar ou aninhar ações como uma coleção de ações.</span><span class="sxs-lookup"><span data-stu-id="54a1b-105">[Scopes](#scopes) let you group or nest actions as a collection of actions.</span></span>
* <span data-ttu-id="54a1b-106">[Condições e ciclos](#conditions-loops) estão agora ações de primeira classe.</span><span class="sxs-lookup"><span data-stu-id="54a1b-106">[Conditions and loops](#conditions-loops) are now first-class actions.</span></span>
* <span data-ttu-id="54a1b-107">A ordenação mais precisas para executar ações com Olá `runAfter` propriedade, substituindo`dependsOn`</span><span class="sxs-lookup"><span data-stu-id="54a1b-107">More precise ordering for running actions with hello `runAfter` property, replacing `dependsOn`</span></span>

<span data-ttu-id="54a1b-108">esquema do esquema toohello 1 de Junho de 2016, de pré-visualização tooupgrade as logic apps do Olá 1 de Agosto de 2015 [veja a secção atualizar Olá](##upgrade-your-schema).</span><span class="sxs-lookup"><span data-stu-id="54a1b-108">tooupgrade your logic apps from hello August 1, 2015 preview schema toohello June 1, 2016 schema, [check out hello upgrade section](##upgrade-your-schema).</span></span>

<a name="scopes"></a>
## <a name="scopes"></a><span data-ttu-id="54a1b-109">âmbitos</span><span class="sxs-lookup"><span data-stu-id="54a1b-109">Scopes</span></span>

<span data-ttu-id="54a1b-110">Este esquema inclui âmbitos, que lhe permitem ações de grupo em conjunto, ou ações de aninhamento dentro entre si.</span><span class="sxs-lookup"><span data-stu-id="54a1b-110">This schema includes scopes, which let you group actions together, or nest actions inside each other.</span></span> <span data-ttu-id="54a1b-111">Por exemplo, uma condição pode conter outra condição.</span><span class="sxs-lookup"><span data-stu-id="54a1b-111">For example, a condition can contain another condition.</span></span> <span data-ttu-id="54a1b-112">Saiba mais sobre [âmbito sintaxe](../logic-apps/logic-apps-loops-and-scopes.md), ou consulte neste exemplo de âmbito básico:</span><span class="sxs-lookup"><span data-stu-id="54a1b-112">Learn more about [scope syntax](../logic-apps/logic-apps-loops-and-scopes.md), or review this basic scope example:</span></span>

```
{
    "actions": {
        "My_Scope": {
            "type": "scope",
            "actions": {                
                "Http": {
                    "inputs": {
                        "method": "GET",
                        "uri": "http://www.bing.com"
                    },
                    "runAfter": {},
                    "type": "Http"
                }
            }
        }
    }
}
```

<a name="conditions-loops"></a>
## <a name="conditions-and-loops-changes"></a><span data-ttu-id="54a1b-113">Condições e ciclos de alterações</span><span class="sxs-lookup"><span data-stu-id="54a1b-113">Conditions and loops changes</span></span>

<span data-ttu-id="54a1b-114">No esquema anterior versões, condições e ciclos foram parâmetros associados uma única ação.</span><span class="sxs-lookup"><span data-stu-id="54a1b-114">In previous schema versions, conditions and loops were parameters associated with a single action.</span></span> <span data-ttu-id="54a1b-115">Este esquema lifts esta limitação, pelo que as condições e ciclos são agora apresentadas como tipos de ação.</span><span class="sxs-lookup"><span data-stu-id="54a1b-115">This schema lifts this limitation, so conditions and loops now appear as action types.</span></span> <span data-ttu-id="54a1b-116">Saiba mais sobre [ciclos e âmbitos](../logic-apps/logic-apps-loops-and-scopes.md), ou consulte neste exemplo básico de uma ação de condição:</span><span class="sxs-lookup"><span data-stu-id="54a1b-116">Learn more about [loops and scopes](../logic-apps/logic-apps-loops-and-scopes.md), or review this basic example for a condition action:</span></span>

```
{
    "If_trigger_is_some-trigger": {
        "type": "If",
        "expression": "@equals(triggerBody(), 'some-trigger')",
        "runAfter": { },
        "actions": {
            "Http_2": {
                "inputs": {
                    "method": "GET",
                    "uri": "http://www.bing.com"
                },
                "runAfter": {},
                "type": "Http"
            }
        },
        "else": 
        {
            "if_trigger_is_another-trigger": "..."
        }      
    }
}
```

<a name="run-after"></a>
## <a name="runafter-property"></a><span data-ttu-id="54a1b-117">propriedade de 'runAfter'</span><span class="sxs-lookup"><span data-stu-id="54a1b-117">'runAfter' property</span></span>

<span data-ttu-id="54a1b-118">Olá `runAfter` propriedade substitui `dependsOn`, fornecer mais precisão quando especificar a ordem de Olá executar ações com base no estado de Olá das ações anteriores.</span><span class="sxs-lookup"><span data-stu-id="54a1b-118">hello `runAfter` property replaces `dependsOn`, providing more precision when you specify hello run order for actions based on hello status of previous actions.</span></span>

<span data-ttu-id="54a1b-119">Olá `dependsOn` propriedade foi synonymous com "ação Olá foi executada e foi concluída com êxito", independentemente do número de vezes que pretendia tooexecute uma ação, com base em se ação anterior Olá foi bem sucedida, falhou ou foi ignorada.</span><span class="sxs-lookup"><span data-stu-id="54a1b-119">hello `dependsOn` property was synonymous with "hello action ran and was successful", no matter how many times you wanted tooexecute an action, based on whether hello previous action was successful, failed, or skipped.</span></span> <span data-ttu-id="54a1b-120">Olá `runAfter` propriedade fornece dessa flexibilidade como um objeto que especifica Olá todos os nomes de ação após o qual hello objeto é executado.</span><span class="sxs-lookup"><span data-stu-id="54a1b-120">hello `runAfter` property provides that flexibility as an object that specifies all hello action names after which hello object runs.</span></span> <span data-ttu-id="54a1b-121">Esta propriedade também define uma matriz de Estados que são aceitáveis como acionadores.</span><span class="sxs-lookup"><span data-stu-id="54a1b-121">This property also defines an array of statuses that are acceptable as triggers.</span></span> <span data-ttu-id="54a1b-122">Por exemplo, se pretendesse toorun depois for bem sucedida do passo um e também após passo B com êxito ou falha, pode construir esta `runAfter` propriedade:</span><span class="sxs-lookup"><span data-stu-id="54a1b-122">For example, if you wanted toorun after step A succeeds and also after step B succeeds or fails, you construct this `runAfter` property:</span></span>

```
{
    "...",
    "runAfter": {
        "A": ["Succeeded"],
        "B": ["Succeeded", "Failed"]
    }
}
```

## <a name="upgrade-your-schema"></a><span data-ttu-id="54a1b-123">Atualizar o esquema</span><span class="sxs-lookup"><span data-stu-id="54a1b-123">Upgrade your schema</span></span>

<span data-ttu-id="54a1b-124">Atualizar toohello novo esquema demora apenas alguns passos.</span><span class="sxs-lookup"><span data-stu-id="54a1b-124">Upgrading toohello new schema only takes a few steps.</span></span> <span data-ttu-id="54a1b-125">Olá processo de atualização inclui a executar o script de actualização Olá, guardar como uma nova aplicação lógica e, se quiser, possivelmente substituir a aplicação de lógica anterior Olá.</span><span class="sxs-lookup"><span data-stu-id="54a1b-125">hello upgrade process includes running hello upgrade script, saving as a new logic app, and if you want, possibly overwriting hello previous logic app.</span></span>

1. <span data-ttu-id="54a1b-126">No portal do Azure Olá, abra a aplicação lógica.</span><span class="sxs-lookup"><span data-stu-id="54a1b-126">In hello Azure portal, open your logic app.</span></span>

2. <span data-ttu-id="54a1b-127">Aceda demasiado**descrição geral**.</span><span class="sxs-lookup"><span data-stu-id="54a1b-127">Go too**Overview**.</span></span> <span data-ttu-id="54a1b-128">Na barra de aplicação de lógica de Olá, escolha **atualizar esquema**.</span><span class="sxs-lookup"><span data-stu-id="54a1b-128">On hello logic app toolbar, choose **Update Schema**.</span></span>
   
    ![Escolha atualizar esquema][1]
   
    <span data-ttu-id="54a1b-130">Olá definição atualizada é devolvida, que pode copiar e colar para uma definição do recurso, se necessário.</span><span class="sxs-lookup"><span data-stu-id="54a1b-130">hello upgraded definition is returned, which you can copy and paste into a resource definition if necessary.</span></span> 
    <span data-ttu-id="54a1b-131">No entanto, iremos **vivamente recomendável** escolher **guardar como** toomake se de que todas as referências de ligação são válidas em Olá atualizado aplicação lógica.</span><span class="sxs-lookup"><span data-stu-id="54a1b-131">However, we **strongly recommend** you choose **Save As** toomake sure that all connection references are valid in hello upgraded logic app.</span></span>

3. <span data-ttu-id="54a1b-132">Na barra de ferramentas de atualização do painel Olá, escolha **guardar como**.</span><span class="sxs-lookup"><span data-stu-id="54a1b-132">In hello upgrade blade toolbar, choose **Save As**.</span></span>

4. <span data-ttu-id="54a1b-133">Introduza o nome de lógica de Olá e o estado.</span><span class="sxs-lookup"><span data-stu-id="54a1b-133">Enter hello logic name and status.</span></span> <span data-ttu-id="54a1b-134">toodeploy a aplicação de lógica atualizado, escolha **criar**.</span><span class="sxs-lookup"><span data-stu-id="54a1b-134">toodeploy your upgraded logic app, choose **Create**.</span></span>

5. <span data-ttu-id="54a1b-135">Certifique-se de que a sua aplicação lógica atualizado funciona conforme esperado.</span><span class="sxs-lookup"><span data-stu-id="54a1b-135">Confirm that your upgraded logic app works as expected.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="54a1b-136">Se estiver a utilizar um acionador manual ou a pedido, o URL de chamada de retorno de Olá alterações na sua nova aplicação lógica.</span><span class="sxs-lookup"><span data-stu-id="54a1b-136">If you are using a manual or request trigger, hello callback URL changes in your new logic app.</span></span> <span data-ttu-id="54a1b-137">Teste Olá novo URL toomake se Olá ponto-a-ponto experiência funciona.</span><span class="sxs-lookup"><span data-stu-id="54a1b-137">Test hello new URL toomake sure hello end-to-end experience works.</span></span> <span data-ttu-id="54a1b-138">os URLs anterior toopreserve, pode clonar ao longo da sua aplicação lógica existente.</span><span class="sxs-lookup"><span data-stu-id="54a1b-138">toopreserve previous URLs, you can clone over your existing logic app.</span></span>

6. <span data-ttu-id="54a1b-139">*Opcional* toooverwrite anterior aplicação lógica com Olá nova versão do esquema, na barra de ferramentas Olá, escolha **Clone**, seguinte demasiado**atualizar esquema**.</span><span class="sxs-lookup"><span data-stu-id="54a1b-139">*Optional* toooverwrite your previous logic app with hello new schema version, on hello toolbar, choose **Clone**, next too**Update Schema**.</span></span> <span data-ttu-id="54a1b-140">Este passo é necessário apenas se pretender tookeep Olá mesmo ID ou pedido de Acionador URL de recurso da sua aplicação lógica.</span><span class="sxs-lookup"><span data-stu-id="54a1b-140">This step is necessary only if you want tookeep hello same resource ID or request trigger URL of your logic app.</span></span>

### <a name="upgrade-tool-notes"></a><span data-ttu-id="54a1b-141">Notas de ferramenta de atualização</span><span class="sxs-lookup"><span data-stu-id="54a1b-141">Upgrade tool notes</span></span>

#### <a name="mapping-conditions"></a><span data-ttu-id="54a1b-142">Condições de mapeamento</span><span class="sxs-lookup"><span data-stu-id="54a1b-142">Mapping conditions</span></span>

<span data-ttu-id="54a1b-143">Na definição de Olá atualizado, ferramenta Olá permite um melhor esforço, em conjunto como um âmbito de agrupamento ações ramo true e false.</span><span class="sxs-lookup"><span data-stu-id="54a1b-143">In hello upgraded definition, hello tool makes a best effort at grouping true and false branch actions together as a scope.</span></span> <span data-ttu-id="54a1b-144">Especificamente, Olá estruturador padrão de `@equals(actions('a').status, 'Skipped')` devem ser apresentadas como um `else` ação.</span><span class="sxs-lookup"><span data-stu-id="54a1b-144">Specifically, hello designer pattern of `@equals(actions('a').status, 'Skipped')` should appear as an `else` action.</span></span> <span data-ttu-id="54a1b-145">No entanto, se a ferramenta de Olá detetar padrões irreconhecível, ferramenta Olá poderá criar condições separadas para verdadeiro Olá e ramo false Olá.</span><span class="sxs-lookup"><span data-stu-id="54a1b-145">However, if hello tool detects unrecognizable patterns, hello tool might create separate conditions for both hello true and hello false branch.</span></span> <span data-ttu-id="54a1b-146">É possível remapear ações após a atualização, se necessário.</span><span class="sxs-lookup"><span data-stu-id="54a1b-146">You can remap actions after upgrading, if necessary.</span></span>

#### <a name="foreach-loop-with-condition"></a><span data-ttu-id="54a1b-147">ciclo de 'foreach' com a condição</span><span class="sxs-lookup"><span data-stu-id="54a1b-147">'foreach' loop with condition</span></span>

<span data-ttu-id="54a1b-148">No novo esquema de Olá, pode utilizar Olá filtro ação tooreplicate Olá padrão um `foreach` ciclo com uma condição por item, mas esta alteração automaticamente deverá ocorrer durante a atualização.</span><span class="sxs-lookup"><span data-stu-id="54a1b-148">In hello new schema, you can use hello filter action tooreplicate hello pattern of a `foreach` loop with a condition per item, but this change should automatically happen when you upgrade.</span></span> <span data-ttu-id="54a1b-149">condição de Olá torna-se uma ação de filtro antes de ciclo de foreach Olá para devolver apenas uma matriz de itens que correspondem à condição Olá e essa matriz é transmitida para a ação de foreach Olá.</span><span class="sxs-lookup"><span data-stu-id="54a1b-149">hello condition becomes a filter action before hello foreach loop for returning only an array of items that match hello condition, and that array is passed into hello foreach action.</span></span> <span data-ttu-id="54a1b-150">Por exemplo, consulte [ciclos e âmbitos](../logic-apps/logic-apps-loops-and-scopes.md).</span><span class="sxs-lookup"><span data-stu-id="54a1b-150">For an example, see [Loops and scopes](../logic-apps/logic-apps-loops-and-scopes.md).</span></span>

#### <a name="resource-tags"></a><span data-ttu-id="54a1b-151">Sinalizadores de recursos</span><span class="sxs-lookup"><span data-stu-id="54a1b-151">Resource tags</span></span>

<span data-ttu-id="54a1b-152">Depois de atualizar, os sinalizadores de recursos são removidos, pelo que tem de repor-los para o fluxo de trabalho Olá atualizado.</span><span class="sxs-lookup"><span data-stu-id="54a1b-152">After you upgrade, resource tags are removed, so you must reset them for hello upgraded workflow.</span></span>

## <a name="other-changes"></a><span data-ttu-id="54a1b-153">Outras alterações</span><span class="sxs-lookup"><span data-stu-id="54a1b-153">Other changes</span></span>

### <a name="renamed-manual-trigger-toorequest-trigger"></a><span data-ttu-id="54a1b-154">Mudar o nome do acionador 'manual' too'request' acionador</span><span class="sxs-lookup"><span data-stu-id="54a1b-154">Renamed 'manual' trigger too'request' trigger</span></span>

<span data-ttu-id="54a1b-155">Olá `manual` tipo acionador foi preterido e mudar o nome demasiado`request` com tipo `http`.</span><span class="sxs-lookup"><span data-stu-id="54a1b-155">hello `manual` trigger type was deprecated and renamed too`request` with type `http`.</span></span> <span data-ttu-id="54a1b-156">Esta alteração cria mais consistência para o tipo de Olá padrão Olá acionador é toobuild utilizado.</span><span class="sxs-lookup"><span data-stu-id="54a1b-156">This change creates more consistency for hello kind of pattern that hello trigger is used toobuild.</span></span>

### <a name="new-filter-action"></a><span data-ttu-id="54a1b-157">Nova ação 'filter'</span><span class="sxs-lookup"><span data-stu-id="54a1b-157">New 'filter' action</span></span>

<span data-ttu-id="54a1b-158">toofilter uma grande matriz para baixo do conjunto de itens, Olá novos mais pequeno tooa `filter` tipo aceita uma matriz e uma condição, avalia condição Olá para cada item e devolve uma matriz com itens de condição de Olá a cumprir.</span><span class="sxs-lookup"><span data-stu-id="54a1b-158">toofilter a large array down tooa smaller set of items, hello new `filter` type accepts an array and a condition, evaluates hello condition for each item, and returns an array with items meeting hello condition.</span></span>

### <a name="restrictions-for-foreach-and-until-actions"></a><span data-ttu-id="54a1b-159">Restrições para 'foreach' e 'até' ações</span><span class="sxs-lookup"><span data-stu-id="54a1b-159">Restrictions for 'foreach' and 'until' actions</span></span>

<span data-ttu-id="54a1b-160">Olá `foreach` e `until` ciclo são tooa restrito única ação.</span><span class="sxs-lookup"><span data-stu-id="54a1b-160">hello `foreach` and `until` loop are restricted tooa single action.</span></span>

### <a name="new-trackedproperties-for-actions"></a><span data-ttu-id="54a1b-161">Novo 'trackedProperties' para ações</span><span class="sxs-lookup"><span data-stu-id="54a1b-161">New 'trackedProperties' for actions</span></span>

<span data-ttu-id="54a1b-162">Ações agora podem ter uma propriedade adicional denominada `trackedProperties`, que é colateral toohello `runAfter` e `type` propriedades.</span><span class="sxs-lookup"><span data-stu-id="54a1b-162">Actions can now have an additional property called `trackedProperties`, which is sibling toohello `runAfter` and `type` properties.</span></span> <span data-ttu-id="54a1b-163">Este objeto especifica determinadas entradas de ação ou produz que pretende que o tooinclude na telemetria de diagnóstico do Azure Olá, emitida como parte de um fluxo de trabalho.</span><span class="sxs-lookup"><span data-stu-id="54a1b-163">This object specifies certain action inputs or outputs that you want tooinclude in hello Azure Diagnostic telemetry, emitted as part of a workflow.</span></span> <span data-ttu-id="54a1b-164">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="54a1b-164">For example:</span></span>

```
{                
    "Http": {
        "inputs": {
            "method": "GET",
            "uri": "http://www.bing.com"
        },
        "runAfter": {},
        "type": "Http",
        "trackedProperties": {
            "responseCode": "@action().outputs.statusCode",
            "uri": "@action().inputs.uri"
        }
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="54a1b-165">Passos Seguintes</span><span class="sxs-lookup"><span data-stu-id="54a1b-165">Next Steps</span></span>
* [<span data-ttu-id="54a1b-166">Criar definições de fluxo de trabalho para aplicações lógicas</span><span class="sxs-lookup"><span data-stu-id="54a1b-166">Create workflow definitions for logic apps</span></span>](../logic-apps/logic-apps-author-definitions.md)
* [<span data-ttu-id="54a1b-167">Criar modelos de implementação para aplicações lógicas</span><span class="sxs-lookup"><span data-stu-id="54a1b-167">Create deployment templates for logic apps</span></span>](../logic-apps/logic-apps-create-deploy-template.md)

<!-- Image references -->
[1]: ./media/logic-apps-schema-2016-04-01/upgradeButton.png
