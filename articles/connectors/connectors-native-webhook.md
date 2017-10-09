---
title: conector aaaWebhook para Azure Logic Apps | Microsoft Docs
description: "As ações de webhook toouse e acionadores tooperform ações como o filtro de matriz partir das logic apps"
services: logic-apps
author: jeffhollan
manager: anneta
editor: 
documentationcenter: 
tags: connectors
ms.assetid: 71775384-6c3a-482c-a484-6624cbe4fcc7
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/21/2016
ms.author: jehollan; LADocs
ms.openlocfilehash: b2dee12750f3f20f10e7b257da05a79f28f90f43
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-webhook-connector"></a>Introdução ao conector do webhook Olá

Com o acionador e ação de webhook Olá, pode iniciar, colocar em pausa e retomar fluxos tooperform estas tarefas:

* Acionar a partir de um [Hub de eventos do Azure](https://github.com/logicappsio/EventHubAPI) quando é recebido um item
* Aguardar a aprovação antes de continuar o fluxo de trabalho

Saiba mais sobre [como toocreate APIs personalizadas que suportam um webhook](../logic-apps/logic-apps-create-api-app.md).

## <a name="use-hello-webhook-trigger"></a>Utilize o trigger de webhook Olá

A [ *acionador* ](connectors-overview.md) é um evento que inicia um fluxo de trabalho de aplicação lógica. Um acionador de webhook é baseada em eventos e não depende de consulta para novos itens. Como Olá [acionador pedido](connectors-native-reqres.md), aplicação de lógica de Olá desencadeado Olá instantânea que ocorre um evento. regista o acionador de webhook Olá um *URL de chamada de retorno* tooa serviço e utiliza essa aplicação de lógica do URL toofire Olá como necessário.

Eis um exemplo que mostra como tooset segurança um HTTP acionar no Olá Designer de aplicação lógica. Olá passos partem do princípio que já tiver implementado ou que estão a aceder a uma API que se segue Olá [webhook subscrever e anular a subscrição padrão nas aplicações lógicas](../logic-apps/logic-apps-create-api-app.md#webhook-triggers). Olá subscrever chamada é estabelecida sempre que uma aplicação lógica está guardada com um novo webhook ou mudou de tooenabled desativado. Olá anular a subscrição a chamada são efetuados quando um acionador de webhook de aplicação lógica é removido e guardado ou mudou de toodisabled ativado.

**acionador de webhook tooadd Olá**

1. Adicionar Olá **HTTP Webhook** acionador como Olá primeiro passo para uma aplicação lógica.
2. Preencha os parâmetros de Olá Olá webhook subscrever e anular a subscrição de chamadas.

   Este passo segue Olá mesmo padrão como Olá [ação HTTP](connectors-native-http.md) formato.

     ![Acionador de HTTP](./media/connectors-native-webhook/using-trigger.png)

3. Adicione pelo menos uma ação.
4. Clique em **guardar** aplicação de lógica de Olá toopublish. Este Olá de chamadas de passo subscrever o ponto final com Olá chamada de retorno URL necessário tootrigger esta aplicação lógica.
5. Olá sempre que o serviço torna um `HTTP POST` URL de chamada de retorno toohello, Olá desencadeado de aplicação de lógica e inclui todos os dados transmitidos para o pedido de Olá.

## <a name="use-hello-webhook-action"></a>Utilize a ação de webhook Olá

Um [ *ação* ](connectors-overview.md) é uma operação levada a cabo pelo fluxo de trabalho Olá definido numa aplicação lógica. Uma ação do webhook regista um *URL de chamada de retorno* com um serviço e aguarda até que o URL de Olá é chamado antes de a retomar. Olá ["Enviar correio eletrónico aprovação"](connectors-create-api-office365-outlook.md) é um exemplo de um conector que se segue este padrão. Pode expandir este padrão em qualquer serviço através da ação de webhook Olá. 

Eis um exemplo que mostra como tooset uma ação de webhook no Olá Designer de aplicação lógica. Estes passos partem do princípio de que já tiver implementado ou que estão a aceder a uma API que se segue Olá [webhook subscrever e anular a subscrição padrão utilizada em aplicações lógicas](../logic-apps/logic-apps-create-api-app.md#webhook-actions). Olá subscrever chamada são efetuados quando uma aplicação lógica executa a ação de webhook Olá. Olá anular a subscrição a chamada são efetuados quando uma execução foi cancelada ao aguardar uma resposta ou, antes de lógica de Olá aplicações de expirar.

**tooadd uma ação do webhook**

1. Escolha **novo passo** > **adicionar uma ação**.

2. Na caixa de pesquisa de Olá, escreva "webhook" toofind Olá **HTTP Webhook** ação.

    ![Selecione a ação de consulta](./media/connectors-native-webhook/using-action-1.png)

3. Preencha os parâmetros de Olá Olá webhook subscrever e anular a subscrição de chamadas

   Este passo segue Olá mesmo padrão como Olá [ação HTTP](connectors-native-http.md) formato.

     ![Ação de consulta concluída](./media/connectors-native-webhook/using-action-2.png)
   
   Em runtime, Olá chamadas de aplicação lógica Olá subscrever endpoint depois de atingir esse passo.

4. Clique em **guardar** aplicação de lógica de Olá toopublish.

## <a name="technical-details"></a>Detalhes técnicos

Eis mais detalhes sobre Olá acionadores e ações que webhook suporta.

## <a name="webhook-triggers"></a>Acionadores de Webhook

| Ação | Descrição |
| --- | --- |
| Webhook de HTTP |Subscreve um serviço de tooa do URL de chamada de retorno que pode chamar a aplicação de lógica de toofire do Olá URL conforme necessário. |

### <a name="trigger-details"></a>Detalhes de Acionador

#### <a name="http-webhook"></a>Webhook de HTTP

Subscreve um serviço de tooa do URL de chamada de retorno que pode chamar a aplicação de lógica de toofire do Olá URL conforme necessário.
Um * meios de campo obrigatório.

| Nome a apresentar | Nome da propriedade | Descrição |
| --- | --- | --- |
| Subscrever o método * |Método |Método de HTTP toouse para subscrever pedido |
| Subscrever URI * |URI |URI de HTTP toouse para subscrever pedido |
| Anular a subscrição método * |Método |Toouse de método HTTP para o pedido de anular a subscrição |
| Anular a subscrição URI * |URI |URI de HTTP toouse para anular a subscrição pedido |
| Subscrever o corpo |Corpo |Corpo do pedido HTTP para subscrever |
| Subscrever cabeçalhos |Cabeçalhos |Cabeçalhos de pedido HTTP para subscrever |
| Subscrever autenticação |Autenticação |Toouse de autenticação HTTP para subscrever. [Consulte o conetor HTTP](connectors-native-http.md#authentication) para obter detalhes |
| Anular a subscrição de corpo |Corpo |Corpo do pedido HTTP para anular a subscrição |
| Anular a subscrição cabeçalhos |Cabeçalhos |Cabeçalhos de pedido HTTP para anular a subscrição |
| Anular a subscrição de autenticação |Autenticação |Toouse de autenticação HTTP para anular a subscrição. [Consulte o conetor HTTP](connectors-native-http.md#authentication) para obter detalhes |

**Detalhes de saída**

Pedido de Webhook

| Nome da propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| Cabeçalhos |objeto |Cabeçalhos de pedido de Webhook |
| Corpo |objeto |Objeto de pedido de Webhook |
| Código de estado |Int |Código de estado de pedido de Webhook |

## <a name="webhook-actions"></a>Ações de Webhook

| Ação | Descrição |
| --- | --- |
| Webhook de HTTP |Subscreve um serviço de tooa do URL de chamada de retorno que pode chamar Olá URL tooresume um passo de fluxo de trabalho, conforme necessário. |

### <a name="action-details"></a>Detalhes de ação

#### <a name="http-webhook"></a>Webhook de HTTP

Subscreve um serviço de tooa do URL de chamada de retorno que pode chamar Olá URL tooresume um passo de fluxo de trabalho, conforme necessário.
Um * meios de campo obrigatório.

| Nome a apresentar | Nome da propriedade | Descrição |
| --- | --- | --- |
| Subscrever o método * |Método |Método de HTTP toouse para subscrever pedido |
| Subscrever URI * |URI |URI de HTTP toouse para subscrever pedido |
| Anular a subscrição método * |Método |Toouse de método HTTP para o pedido de anular a subscrição |
| Anular a subscrição URI * |URI |URI de HTTP toouse para anular a subscrição pedido |
| Subscrever o corpo |Corpo |Corpo do pedido HTTP para subscrever |
| Subscrever cabeçalhos |Cabeçalhos |Cabeçalhos de pedido HTTP para subscrever |
| Subscrever autenticação |Autenticação |Toouse de autenticação HTTP para subscrever. [Consulte o conetor HTTP](connectors-native-http.md#authentication) para obter detalhes |
| Anular a subscrição de corpo |Corpo |Corpo do pedido HTTP para anular a subscrição |
| Anular a subscrição cabeçalhos |Cabeçalhos |Cabeçalhos de pedido HTTP para anular a subscrição |
| Anular a subscrição de autenticação |Autenticação |Toouse de autenticação HTTP para anular a subscrição. [Consulte o conetor HTTP](connectors-native-http.md#authentication) para obter detalhes |

**Detalhes de saída**

Pedido de Webhook

| Nome da propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| Cabeçalhos |objeto |Cabeçalhos de pedido de Webhook |
| Corpo |objeto |Objeto de pedido de Webhook |
| Código de estado |Int |Código de estado de pedido de Webhook |

## <a name="next-steps"></a>Passos seguintes

* [Criar uma aplicação lógica](../logic-apps/logic-apps-create-a-logic-app.md)
* [Localizar outros conectores](apis-list.md)