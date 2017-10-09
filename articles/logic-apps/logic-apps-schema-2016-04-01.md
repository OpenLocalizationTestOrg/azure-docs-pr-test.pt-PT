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
# <a name="schema-updates-for-azure-logic-apps---june-1-2016"></a>Atualizações do esquema para o Azure Logic Apps - 1 de Junho de 2016

Este novo esquema e a API versão para o Azure Logic Apps inclui melhoramentos essenciais que tornam as logic apps mais toouse mais fácil e fiável:

* [Âmbitos](#scopes) permitem-lhe agrupar ou aninhar ações como uma coleção de ações.
* [Condições e ciclos](#conditions-loops) estão agora ações de primeira classe.
* A ordenação mais precisas para executar ações com Olá `runAfter` propriedade, substituindo`dependsOn`

esquema do esquema toohello 1 de Junho de 2016, de pré-visualização tooupgrade as logic apps do Olá 1 de Agosto de 2015 [veja a secção atualizar Olá](##upgrade-your-schema).

<a name="scopes"></a>
## <a name="scopes"></a>âmbitos

Este esquema inclui âmbitos, que lhe permitem ações de grupo em conjunto, ou ações de aninhamento dentro entre si. Por exemplo, uma condição pode conter outra condição. Saiba mais sobre [âmbito sintaxe](../logic-apps/logic-apps-loops-and-scopes.md), ou consulte neste exemplo de âmbito básico:

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
## <a name="conditions-and-loops-changes"></a>Condições e ciclos de alterações

No esquema anterior versões, condições e ciclos foram parâmetros associados uma única ação. Este esquema lifts esta limitação, pelo que as condições e ciclos são agora apresentadas como tipos de ação. Saiba mais sobre [ciclos e âmbitos](../logic-apps/logic-apps-loops-and-scopes.md), ou consulte neste exemplo básico de uma ação de condição:

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
## <a name="runafter-property"></a>propriedade de 'runAfter'

Olá `runAfter` propriedade substitui `dependsOn`, fornecer mais precisão quando especificar a ordem de Olá executar ações com base no estado de Olá das ações anteriores.

Olá `dependsOn` propriedade foi synonymous com "ação Olá foi executada e foi concluída com êxito", independentemente do número de vezes que pretendia tooexecute uma ação, com base em se ação anterior Olá foi bem sucedida, falhou ou foi ignorada. Olá `runAfter` propriedade fornece dessa flexibilidade como um objeto que especifica Olá todos os nomes de ação após o qual hello objeto é executado. Esta propriedade também define uma matriz de Estados que são aceitáveis como acionadores. Por exemplo, se pretendesse toorun depois for bem sucedida do passo um e também após passo B com êxito ou falha, pode construir esta `runAfter` propriedade:

```
{
    "...",
    "runAfter": {
        "A": ["Succeeded"],
        "B": ["Succeeded", "Failed"]
    }
}
```

## <a name="upgrade-your-schema"></a>Atualizar o esquema

Atualizar toohello novo esquema demora apenas alguns passos. Olá processo de atualização inclui a executar o script de actualização Olá, guardar como uma nova aplicação lógica e, se quiser, possivelmente substituir a aplicação de lógica anterior Olá.

1. No portal do Azure Olá, abra a aplicação lógica.

2. Aceda demasiado**descrição geral**. Na barra de aplicação de lógica de Olá, escolha **atualizar esquema**.
   
    ![Escolha atualizar esquema][1]
   
    Olá definição atualizada é devolvida, que pode copiar e colar para uma definição do recurso, se necessário. 
    No entanto, iremos **vivamente recomendável** escolher **guardar como** toomake se de que todas as referências de ligação são válidas em Olá atualizado aplicação lógica.

3. Na barra de ferramentas de atualização do painel Olá, escolha **guardar como**.

4. Introduza o nome de lógica de Olá e o estado. toodeploy a aplicação de lógica atualizado, escolha **criar**.

5. Certifique-se de que a sua aplicação lógica atualizado funciona conforme esperado.
   
   > [!NOTE]
   > Se estiver a utilizar um acionador manual ou a pedido, o URL de chamada de retorno de Olá alterações na sua nova aplicação lógica. Teste Olá novo URL toomake se Olá ponto-a-ponto experiência funciona. os URLs anterior toopreserve, pode clonar ao longo da sua aplicação lógica existente.

6. *Opcional* toooverwrite anterior aplicação lógica com Olá nova versão do esquema, na barra de ferramentas Olá, escolha **Clone**, seguinte demasiado**atualizar esquema**. Este passo é necessário apenas se pretender tookeep Olá mesmo ID ou pedido de Acionador URL de recurso da sua aplicação lógica.

### <a name="upgrade-tool-notes"></a>Notas de ferramenta de atualização

#### <a name="mapping-conditions"></a>Condições de mapeamento

Na definição de Olá atualizado, ferramenta Olá permite um melhor esforço, em conjunto como um âmbito de agrupamento ações ramo true e false. Especificamente, Olá estruturador padrão de `@equals(actions('a').status, 'Skipped')` devem ser apresentadas como um `else` ação. No entanto, se a ferramenta de Olá detetar padrões irreconhecível, ferramenta Olá poderá criar condições separadas para verdadeiro Olá e ramo false Olá. É possível remapear ações após a atualização, se necessário.

#### <a name="foreach-loop-with-condition"></a>ciclo de 'foreach' com a condição

No novo esquema de Olá, pode utilizar Olá filtro ação tooreplicate Olá padrão um `foreach` ciclo com uma condição por item, mas esta alteração automaticamente deverá ocorrer durante a atualização. condição de Olá torna-se uma ação de filtro antes de ciclo de foreach Olá para devolver apenas uma matriz de itens que correspondem à condição Olá e essa matriz é transmitida para a ação de foreach Olá. Por exemplo, consulte [ciclos e âmbitos](../logic-apps/logic-apps-loops-and-scopes.md).

#### <a name="resource-tags"></a>Sinalizadores de recursos

Depois de atualizar, os sinalizadores de recursos são removidos, pelo que tem de repor-los para o fluxo de trabalho Olá atualizado.

## <a name="other-changes"></a>Outras alterações

### <a name="renamed-manual-trigger-toorequest-trigger"></a>Mudar o nome do acionador 'manual' too'request' acionador

Olá `manual` tipo acionador foi preterido e mudar o nome demasiado`request` com tipo `http`. Esta alteração cria mais consistência para o tipo de Olá padrão Olá acionador é toobuild utilizado.

### <a name="new-filter-action"></a>Nova ação 'filter'

toofilter uma grande matriz para baixo do conjunto de itens, Olá novos mais pequeno tooa `filter` tipo aceita uma matriz e uma condição, avalia condição Olá para cada item e devolve uma matriz com itens de condição de Olá a cumprir.

### <a name="restrictions-for-foreach-and-until-actions"></a>Restrições para 'foreach' e 'até' ações

Olá `foreach` e `until` ciclo são tooa restrito única ação.

### <a name="new-trackedproperties-for-actions"></a>Novo 'trackedProperties' para ações

Ações agora podem ter uma propriedade adicional denominada `trackedProperties`, que é colateral toohello `runAfter` e `type` propriedades. Este objeto especifica determinadas entradas de ação ou produz que pretende que o tooinclude na telemetria de diagnóstico do Azure Olá, emitida como parte de um fluxo de trabalho. Por exemplo:

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

## <a name="next-steps"></a>Passos Seguintes
* [Criar definições de fluxo de trabalho para aplicações lógicas](../logic-apps/logic-apps-author-definitions.md)
* [Criar modelos de implementação para aplicações lógicas](../logic-apps/logic-apps-create-deploy-template.md)

<!-- Image references -->
[1]: ./media/logic-apps-schema-2016-04-01/upgradeButton.png
