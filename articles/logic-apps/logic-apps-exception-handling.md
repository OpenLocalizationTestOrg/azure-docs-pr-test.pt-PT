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
# <a name="handle-errors-and-exceptions-in-azure-logic-apps"></a>Processar os erros e exceções no Azure Logic Apps

Aplicações lógicas do Azure fornece ferramentas avançadas e padrões toohelp, certificar-se que a integrações são resilientes contra falhas e robusto. Qualquer arquitetura de integração pode representar um desafio de Olá de efetuar o período de indisponibilidade do tooappropriately se identificador ou problemas de sistemas dependentes. Logic Apps torna processamento de erros de uma experiência de primeira classe, dando-lhe Olá ferramentas terá tooact em exceções e erros nos seus fluxos de trabalho.

## <a name="retry-policies"></a>Repita políticas

Uma política de repetição é tipo mais básico do Olá de exceção e processamento de erros. Se um pedido inicial foi excedido ou falha (qualquer pedido que resulte num 429 ou resposta 5xx), esta política define se a ação de Olá deve repetir. Por predefinição, todas as ações repetir 4 vezes adicionais sobre os intervalos de 20 segundo. Por isso, caso o primeiro pedido efetuado Olá recebe um `500 Internal Server Error` resposta, o motor de fluxo de trabalho de Olá interrompe para 20 segundos e tentativas Olá pedido novamente. Se depois de todas as tentativas, resposta Olá ainda é uma exceção ou falha, o fluxo de trabalho Olá continua e marcas de escala Olá estado da ação como `Failed`.

Pode configurar as políticas de repetição no Olá **entradas** para uma ação específica. Por exemplo, pode configurar um tootry de política de repetição máximo de 4 horas através de intervalos de 1 hora. Para obter detalhes completos sobre as propriedades de entrada, consulte [ações de fluxo de trabalho e é acionado][retryPolicyMSDN].

```json
"retryPolicy" : {
      "type": "<type-of-retry-policy>",
      "interval": <retry-interval>,
      "count": <number-of-retry-attempts>
    }
```

Se pretendia sua tooretry de ação de HTTP 4 vezes e aguarde 10 minutos entre cada tentativa, utilizaria Olá definição os seguintes:

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

Para obter mais informações sobre a sintaxe suportado, consulte Olá [secção política de repetição ações de fluxo de trabalho e é acionado][retryPolicyMSDN].

## <a name="catch-failures-with-hello-runafter-property"></a>Detetar falhas com Olá RunAfter propriedade

Cada ação de aplicação lógica declara que ações devem ser concluído antes de iniciado o ação Olá, como a ordenação passos Olá no fluxo de trabalho. Na definição de ação de Olá, esta ordem é conhecido como Olá `runAfter` propriedade. Esta propriedade é um objeto que descreve quais as ações e Estados de ação executar a ação de Olá. Por predefinição, todas as ações adicionadas através do Designer de aplicação de lógica de Olá estiverem definidas demasiado`runAfter` passo anterior de Olá se hello passo anterior `Succeeded`. No entanto, pode personalizar esta ações de toofire valor quando têm ações anteriores `Failed`, `Skipped`, ou um conjunto possíveis destes valores. Se pretendesse tooadd tooa um item designado tópico do Service Bus após uma ação específica `Insert_Row` falhar, pode utilizar Olá seguir `runAfter` configuração:

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

Olá aviso `runAfter` é definir a propriedade toofire se hello `Insert_Row` é ação `Failed`. ação de Olá toorun se for o estado da ação Olá `Succeeded`, `Failed`, ou `Skipped`, utilizam esta sintaxe:

```json
"runAfter": {
        "Insert_Row": [
            "Failed", "Succeeded", "Skipped"
        ]
    }
```

> [!TIP]
> Ações que executaram e concluir com êxito após ter uma ação anterior tenha falhado, estão marcados como `Succeeded`. Isto significa de comportamento se a com êxito catch todas as falhas no fluxo de trabalho, Olá ser executado automaticamente está marcada como `Succeeded`.

## <a name="scopes-and-results-tooevaluate-actions"></a>Ações de tooevaluate âmbitos e resultados

Toohow semelhante pode executar após ações individuais, pode também agrupar ações em conjunto no interior de um [âmbito](../logic-apps/logic-apps-loops-and-scopes.md), que atua como um agrupamento lógico das ações. Âmbitos são úteis para organizar as suas ações de aplicação lógica tanto para efetuar avaliações do agregado num Estado de Olá de um âmbito. âmbito de Olá próprio recebe um Estado depois de terminar todas as ações de um âmbito. Estado de âmbito de Olá é determinado com Olá mesmos critérios como uma execução. Se é Olá ação final um ramo de execução `Failed` ou `Aborted`, estado de Olá é `Failed`.

toofire ações específicas para quaisquer falhas que tenham acontecido dentro do âmbito de Olá, pode utilizar `runAfter` com um âmbito que está marcado como `Failed`. Se *qualquer* ações no âmbito de Olá falharem, executar após a falha de um âmbito permite criar uma única ação toocatch falhas.

### <a name="getting-hello-context-of-failures-with-results"></a>Obter Olá contexto de falhas com resultados

Embora a deteção de falhas de um âmbito é útil, pode também querer toohelp contexto que compreender exatamente as ações de falha, e quaisquer erros ou códigos de estado que foram devolvidos. Olá `@result()` função de fluxo de trabalho fornece o contexto sobre resultado Olá de todas as ações de um âmbito.

`@result()`assume um parâmetro único, o nome de âmbito e devolve uma matriz de todos os resultados de ação de Olá do dentro esse âmbito. Estes objetos de ação incluem Olá mesmo atributos como Olá `@actions()` produz de objeto, incluindo a hora de início de ação, hora de fim de ação, estado da ação, entradas de ação, correlação da ação IDs e ação. contexto toosend todas as ações que falha dentro de um âmbito, emparelhar facilmente um `@result()` funcionar com uma `runAfter`.

tooexecute uma ação *para cada* ação num âmbito que `Failed`, a matriz de Olá de filtro de resultados tooactions que falharam, pode ser emparelhado `@result()` com um  **[filtro matriz](../connectors/connectors-native-query.md)**  ação e um  **[ForEach](../logic-apps/logic-apps-loops-and-scopes.md)**  ciclo. Pode colocar a matriz de resultado filtrado Olá e efetuar uma ação para cada falha utilizando Olá **ForEach** ciclo. Eis um exemplo, seguido por uma explicação detalhada, que envia um pedido POST de HTTP com o corpo da resposta Olá de todas as ações que falhou no âmbito de Olá `My_Scope`.

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

Eis um toodescribe instruções detalhadas sobre o que acontece:

1. resultado de Olá tooget de todas as ações dentro `My_Scope`, Olá **filtro matriz** filtros de ação `@result('My_Scope')`.

2. Olá condição para **filtro matriz** alguma `@result()` item que tem o Estado igual demasiado`Failed`. Esta condição filtra matriz Olá com todos os resultados de ação de `My_Scope` tooan matriz com apenas os resultados de ação de falha.

3. Efetuar uma **para cada** ação no Olá **filtrado matriz** produz. Este passo executa uma ação *para cada* falhou o resultado da ação que foi filtrado anteriormente.

    Se uma única ação no âmbito de Olá falhou, Olá ações no Olá `foreach` execute apenas uma vez. 
    Muitas ações falhadas causam uma ação por falha.

4. Enviar um HTTP POST em Olá `foreach` do item de corpo de resposta, ou `@item()['outputs']['body']`. Olá `@result()` forma item é Olá mesmo como Olá `@actions()` formam e pode ser analisado Olá mesma forma.

5. Inclua dois cabeçalhos personalizados com o nome da ação falhada Olá `@item()['name']` e Olá falhou a execução cliente ID de controlo `@item()['clientTrackingId']`.

Para referência, eis um exemplo de um único `@result()` item, que mostra Olá `name`, `body`, e `clientTrackingId` propriedades que são analisadas no exemplo anterior Olá. Fora de um `foreach`, `@result()` devolve uma matriz destes objetos.

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

padrões de processamento de exceções diferentes tooperform, pode utilizar expressões Olá apresentadas anteriormente. Poderá escolher tooexecute uma único excepção a processar a ação fora do âmbito de Olá que aceita matriz filtrado completo Olá de falhas e remover Olá `foreach`. Também pode incluir outras propriedades útil de Olá `@result()` resposta apresentada anteriormente.

## <a name="azure-diagnostics-and-telemetry"></a>Telemetria e diagnóstico do Azure

Olá padrões anteriores são erros de toohandle excelente forma e exceções dentro de uma execução, mas também pode identificar e responder tooerrors independente da Olá ser executado automaticamente. 
[Diagnóstico do Azure](../logic-apps/logic-apps-monitor-your-logic-apps.md) fornece uma forma simples toosend todos os conta de armazenamento do Azure do tooan de eventos (incluindo todos os Estados de execução e a ação) do fluxo de trabalho ou de um Hub de eventos do Azure. tooevaluate execute Estados, pode monitorizar as métricas e registos de Olá ou publicá-los em qualquer ferramenta monitorização que preferir. Uma opção de potencial é toostream todos os eventos de Olá através do Hub de eventos do Azure para [Stream Analytics](https://azure.microsoft.com/services/stream-analytics/). No Stream Analytics, é possível escrever consultas em direto fora de quaisquer anomalias, médias ou falhas de Olá os registos de diagnóstico. Do Stream Analytics pode facilmente saída tooother origens de dados como filas, tópicos, SQL Server, base de dados do Azure Cosmos e Power BI.

## <a name="next-steps"></a>Passos Seguintes

* [Veja como um cliente baseia-se com Azure Logic Apps de processamento de erros](../logic-apps/logic-apps-scenario-error-and-exception-handling.md)
* [Localizar mais cenários e exemplos de Logic Apps](../logic-apps/logic-apps-examples-and-scenarios.md)
* [Saiba como toocreate automatizada implementações para as logic apps](../logic-apps/logic-apps-create-deploy-template.md)
* [Criar e implementar aplicações lógicas com o Visual Studio](logic-apps-deploy-from-vs.md)

<!-- References -->
[retryPolicyMSDN]: https://docs.microsoft.com/rest/api/logic/actions-and-triggers#Anchor_9
