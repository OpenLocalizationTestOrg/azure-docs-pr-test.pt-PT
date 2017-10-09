---
title: aaaCall, acionador ou aninhar fluxos de trabalho com pontos finais HTTP - Azure Logic Apps | Microsoft Docs
description: Configurar pontos finais toocall HTTP, acionador ou nest fluxos de trabalho para o Azure Logic Apps
services: logic-apps
keywords: fluxos de trabalho, pontos finais de HTTP
author: jeffhollan
manager: anneta
editor: 
documentationcenter: 
ms.assetid: 73ba2a70-03e9-4982-bfc8-ebfaad798bc2
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.custom: H1Hack27Feb2017
ms.date: 03/31/2017
ms.author: LADocs; jehollan
ms.openlocfilehash: 072a314c3bff75ab7696f86bb063bb7c03c4ae89
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="call-trigger-or-nest-workflows-with-http-endpoints-in-logic-apps"></a>Chamar, acionador, ou aninhar fluxos de trabalho com pontos finais HTTP nas logic apps

Nativamente pode expor os pontos finais de HTTP síncronos como os acionadores nas logic apps para que possa acionar ou chamar as logic apps através de um URL. Também pode aninhar fluxos de trabalho nas suas logic apps utilizando um padrão de possível chamar EndRead pontos finais.

pontos finais HTTP toocreate, pode adicionar estes acionadores para que as logic apps podem receber pedidos de entrada:

* [Pedido](../connectors/connectors-native-reqres.md)

* [Webhook de ligação de API](logic-apps-workflow-actions-triggers.md#api-connection-trigger)

* [Webhook de HTTP](../connectors/connectors-native-webhook.md)

   > [!NOTE]
   > Apesar dos nossos exemplos utilizam Olá **pedido** acionador, pode utilizar qualquer um dos Olá listados acionadores HTTP e todos os princípios de forma idêntica aplicam toohello dos outros tipos de Acionador.

## <a name="set-up-an-http-endpoint-for-your-logic-app"></a>Configurar um ponto final HTTP para a sua aplicação lógica

toocreate um ponto final de HTTP, adicionar um acionador que pode receber pedidos recebidos.

1. Inicie sessão no toohello [portal do Azure](https://portal.azure.com "portal do Azure"). Aceda a aplicação de lógica de tooyour e abra o Designer de aplicação lógica.

2. Adicione um acionador que permite que a sua aplicação lógica receber pedidos recebidos. Por exemplo, adicionar Olá **pedido** aplicação de lógica de tooyour de Acionador.

3.  Em **esquema de JSON de corpo do pedido**, opcionalmente, pode introduzir um esquema JSON para o que esperar Olá acionador tooreceive payload de Olá (dados).

    designer de Olá utiliza este esquema para gerar tokens que a sua aplicação lógica pode utilizar tooconsume, parse e transmita dados de Acionador de Olá através do seu fluxo de trabalho. 
    Mais informações sobre como [tokens gerados a partir de esquemas JSON](#generated-tokens).

    Neste exemplo, introduza o esquema de Olá mostrada no designer de Olá:

    ```json
    {
      "type": "object",
      "properties": {
        "address": {
          "type": "string"
        }
      },
      "required": [
        "address"
      ]
    }
    ```

    ![Adicionar Olá pedido de ação][1]

    > [!TIP]
    > 
    > Pode gerar um esquema para um payload JSON de exemplo a partir de uma ferramenta como o [jsonschema.net](http://jsonschema.net/), ou no Olá **pedido** acionador escolhendo **esquema de toogenerate de payload de exemplo de utilização**. 
    > Introduza o payload de exemplo e escolha **feito**.

    Por exemplo, este payload de exemplo:

    ```json
    {
       "address": "21 2nd Street, New York, New York"
    }
    ```

    gera neste esquema:

    ```json
    }
       "type": "object",
       "properties": {
          "address": {
             "type": "string" 
          }
       }
    }
    ```

4.  Guarde a sua aplicação lógica. Em **HTTP POST toothis URL**, agora deve encontrar um URL de chamada de retorno gerado, tal como neste exemplo:

    ![URL de chamada de retorno gerado para o ponto final](./media/logic-apps-http-endpoint/generated-endpoint-url.png)

    Este URL contém uma chave de assinatura de acesso partilhado (SAS) nos parâmetros de consulta de Olá que são utilizados para autenticação. 
    Também pode obter o URL de ponto final HTTP Olá da sua descrição geral da aplicação lógica em Olá portal do Azure. Em **histórico de Acionador**, selecione o acionador:

    ![Obter o URL de ponto final HTTP a partir do portal do Azure][2]

    Ou pode obter o URL de Olá ao efetuar esta chamada:

    ```
    POST https://management.azure.com/{logic-app-resourceID}/triggers/{myendpointtrigger}/listCallbackURL?api-version=2016-06-01
    ```

## <a name="change-hello-http-method-for-your-trigger"></a>Alterar o método HTTP Olá para o acionador

Por predefinição, Olá **pedido** acionador espera um pedido POST de HTTP, mas pode utilizar um método HTTP diferente. 

> [!NOTE]
> Pode especificar o tipo de apenas um método.

1. No seu **pedido** acionar, escolha **Mostrar opções avançadas**.

2. Abra Olá **método** lista. Para este exemplo, selecione **obter** , para que possa testar URL do ponto final de HTTP mais tarde.

    > [!NOTE]
    > Pode selecionar qualquer outro método HTTP ou especificar um método personalizado para a sua própria aplicação lógica.

    ![Alterar o método HTTP](./media/logic-apps-http-endpoint/change-method.png)

## <a name="accept-parameters-through-your-http-endpoint-url"></a>Aceitar parâmetros através do seu URL de ponto final HTTP

Quando pretender que os parâmetros de tooaccept de URL de ponto final HTTP, personalize o caminho relativo do acionador.

1. No seu **pedido** acionar, escolha **Mostrar opções avançadas**. 

2. Em **método**, especifique o método de Olá HTTP que pretende que o seu toouse de pedido. Para este exemplo, selecione Olá **obter** método, se ainda não o fez, para que possa testar URL do ponto final de HTTP.

      > [!NOTE]
      > Quando especificar um caminho relativo para o acionador, tem de especificar também explicitamente um método HTTP para o acionador.

3. Em **caminho relativo**, especifique Olá caminho relativo para o parâmetro de Olá que deve aceitar o URL, por exemplo, `customers/{customerID}`.

    ![Especifique o método HTTP Olá e o caminho relativo para o parâmetro](./media/logic-apps-http-endpoint/relativeurl.png)

4. toouse Olá parâmetro, adicione um **resposta** aplicação de lógica de tooyour de ação. (Sob o acionador, escolha **novo passo** > **adicionar uma ação** > **resposta**) 

5. Na sua resposta **corpo**, inclui Olá o token para o parâmetro de Olá que especificou no caminho relativo do acionador.

    Por exemplo, tooreturn `Hello {customerID}`, atualize a sua resposta **corpo** com `Hello {customerID token}`. 
    lista de conteúdo dinâmico Olá deve aparecer e Mostrar Olá `customerID` token para tooselect.

    ![Adicionar o corpo do parâmetro tooresponse](./media/logic-apps-http-endpoint/relativeurlresponse.png)

    O **corpo** deverá ser semelhante neste exemplo:

    ![Corpo de resposta com o parâmetro](./media/logic-apps-http-endpoint/relative-url-with-parameter.png)

6. Guarde a sua aplicação lógica. 

    O URL de ponto final HTTP inclui agora o caminho relativo Olá, por exemplo: 

    https & # 58;//prod-00.southcentralus.logic.azure.com/workflows/f90cb66c52ea4e9cabe0abf4e197deff/triggers/manual/paths/invoke/customers/{customerID}...

7. tootest o ponto final de HTTP, cópia e colagem Olá URL atualizado na outra janela do browser, mas substituem `{customerID}` com `123456`, e prima Enter.

    O browser deve mostrar este texto: 

    `Hello 123456`

<a name="generated-tokens"></a>
### <a name="tokens-generated-from-json-schemas-for-your-logic-app"></a>Tokens gerados a partir de esquemas JSON para a sua aplicação lógica

Quando fornecer o esquema JSON na sua **pedido** acionar, hello Designer de aplicação lógica gera tokens para propriedades que esquema. Em seguida, pode utilizar esses tokens para transmitir dados através do seu fluxo de trabalho de aplicação lógica.

Neste exemplo, se adicionar Olá `title` e `name` esquema JSON tooyour de propriedades, os seus tokens estão agora disponível toouse em passos posteriores do fluxo de trabalho. 

Segue-se o esquema JSON concluída Olá:

```json
{
   "type": "object",
   "properties": {
      "address": {
         "type": "string"
      },
      "title": {
         "type": "string"
      },
      "name": {
         "type": "string"
      }
   },
   "required": [
      "address",
      "title",
      "name"
   ]
}
```

## <a name="create-nested-workflows-for-logic-apps"></a>Criar fluxos de trabalho aninhados para aplicações lógicas

Pode ser aninhado fluxos de trabalho na sua aplicação lógica adicionando outras as logic apps que podem receber pedidos. tooinclude estes logic apps, adicionar Olá **Azure Logic Apps - escolha um fluxo de trabalho Logic Apps** acionador tooyour de ação. Em seguida, pode selecionar a partir de aplicações lógicas elegível.

![Adicionar outra aplicação lógica](./media/logic-apps-http-endpoint/choose-logic-apps-workflow.png)

## <a name="call-or-trigger-logic-apps-through-http-endpoints"></a>Chamar ou acionar as logic apps através de pontos finais HTTP

Depois de criar o ponto final de HTTP, pode acionar a sua aplicação lógica através de um `POST` URL completo do método toohello. As Logic apps têm suporte incorporado para pontos finais de acesso direto.

## <a name="reference-content-from-an-incoming-request"></a>Conteúdo de referência de um pedido recebido

Olá conteúdo type do estiver `application/json`, pode referenciar propriedades do pedido de entrada Olá. Caso contrário, conteúdo é tratado como uma única unidade binária, que pode decorrer tooother APIs. tooreference este conteúdo no interior do fluxo de trabalho Olá, tem de converter esse conteúdo. Por exemplo, se passa `application/xml` conteúdo, pode utilizar `@xpath()` para extração um XPath, ou `@json()` para a conversão XML tooJSON. Saiba mais sobre [trabalhar com os tipos de conteúdo](../logic-apps/logic-apps-content-type.md).

Olá tooget de saída de um pedido de entrada, pode utilizar Olá `@triggerOutputs()` função. saída de Olá aspeto que poderá ter neste exemplo:

```json
{
    "headers": {
        "content-type" : "application/json"
    },
    "body": {
        "myProperty" : "property value"
    }
}
```

Olá tooaccess `body` propriedade especificamente, pode utilizar Olá `@triggerBody()` atalho. 

## <a name="respond-toorequests"></a>Responder toorequests

Pode querer toorespond toocertain pedidos que iniciar uma aplicação lógica devolvendo toohello conteúdo autor da chamada. código de estado de Olá tooconstruct, o cabeçalho e o corpo da sua resposta, pode utilizar Olá **resposta** ação. Esta ação pode aparecer em qualquer local na sua aplicação lógica, não apenas no final de Olá do fluxo de trabalho.

> [!NOTE] 
> Se a sua aplicação lógica não inclui um **resposta**, ponto final de Olá HTTP responde *imediatamente* com um **aceites 202** estado. Além disso, para original pedido tooget Olá resposta Olá, todos os passos necessários para resposta Olá devem ser concluído dentro do Olá [limite de tempo limite do pedido](./logic-apps-limits-and-config.md) , exceto se chamar o fluxo de trabalho Olá como uma aplicação lógica aninhada. Se nenhuma resposta acontece este limite, o pedido recebido Olá exceder o tempo limite e recebe a resposta HTTP de Olá **tempo limite de cliente 408**. Para aplicações lógicas aninhados, a aplicação de lógica de principal de Olá continua toowait para uma resposta até à conclusão, independentemente da quanto tempo é necessário.

### <a name="construct-hello-response"></a>Construir a resposta Olá

Pode incluir mais do que um cabeçalho e qualquer tipo de conteúdo no corpo de resposta de Olá. No nosso exemplo de resposta, o cabeçalho de Olá Especifica que resposta Olá tem o tipo de conteúdo `application/json`. e Olá corpo contém `title` e `name`, com base no esquema JSON Olá anteriormente atualizado para incluir Olá **pedido** acionador.

![Ação de resposta de HTTP][3]

As respostas têm estas propriedades:

| Propriedade | Descrição |
| --- | --- |
| statusCode |Especifica o código de estado de Olá HTTP para o pedido de entrada toohello está a responder. Este código pode ser qualquer código de estado válido que comece com 2xx, 4xx ou 5xx. No entanto, os códigos de estado de 3xx não são permitidos. |
| Cabeçalhos |Define a qualquer número de cabeçalhos tooinclude na resposta Olá. |
| Corpo |Especifica um objeto de corpo pode ser uma cadeia, um objeto JSON ou mesmo binário conteúdo referenciado a partir de um passo anterior. |

Eis o esquema JSON Olá parece agora para Olá **resposta** ação:

``` json
"Response": {
   "inputs": {
      "body": {
         "title": "@{triggerBody()?['title']}",
         "name": "@{triggerBody()?['name']}"
      },
      "headers": {
           "content-type": "application/json"
      },
      "statusCode": 200
   },
   "runAfter": {},
   "type": "Response"
}
```

> [!TIP]
> Escolha a definição de JSON de conclua de Olá do tooview para a sua aplicação lógica, no Olá Designer de aplicação lógica, **Code vista**.

## <a name="q--a"></a>P&R

#### <a name="q-what-about-url-security"></a>P: E sobre segurança URL?

R: azure gera em segurança URLs da chamada de retorno de aplicação de lógica com uma assinatura de acesso partilhado (SAS). Esta assinatura atravessa como um parâmetro de consulta e tem de ser validada antes da aplicação lógica pode acionados. O Azure gera assinatura Olá utilizando uma combinação exclusiva de uma chave secreta por aplicação lógica, o nome do acionador Olá e operação Olá que é executada. Por isso, a menos que alguém tenha a chave de acesso toohello lógica segredo aplicação, não é possível gerar uma assinatura válida.

   > [!IMPORTANT]
   > Para produção e sistemas seguros, Desaconselhamos vivamente a sua aplicação lógica ao chamar diretamente a partir do browser Olá porque:
   > 
   > * chave de acesso partilhado Olá é apresentado no URL Olá.
   > * Não é possível gerir políticas de conteúdo seguras devido tooshared domínios em clientes de aplicação lógica.

#### <a name="q-can-i-configure-http-endpoints-further"></a>P: posso configurar pontos finais de HTTP mais?

R: Sim, pontos finais de HTTP suportam a configuração mais avançada através de [ **API Management**](../api-management/api-management-key-concepts.md). Este serviço também oferece a capacidade de Olá para tooconsistently faça a gestão de todas as suas APIs, incluindo as logic apps, configurar os nomes de domínio personalizado, utilize mais métodos de autenticação e muito mais, por exemplo:

* [Alterar método de pedido de Olá](https://docs.microsoft.com/azure/api-management/api-management-advanced-policies#SetRequestMethod)
* [Alterar os segmentos de URL de pedido de Olá Olá](https://docs.microsoft.com/azure/api-management/api-management-transformation-policies#RewriteURL)
* Configurar os domínios de gestão de API no Olá [portal do Azure](https://portal.azure.com/ "portal do Azure")
* Configurar a política toocheck para a autenticação básica

#### <a name="q-what-changed-when-hello-schema-migrated-from-hello-december-1-2014-preview"></a>P: o que foi alterado quando esquema Olá migrado a partir da pré-visualização de 1 de Dezembro de 2014 Olá?

R: Eis um resumo sobre estas alterações:

| Pré-visualização de 1 de Dezembro de 2014 | 1 de Junho de 2016 |
| --- | --- |
| Clique em **serviço de escuta HTTP** aplicação API |Clique em **acionador Manual** (não existe nenhuma aplicação de API obrigatório) |
| Definição de serviço de escuta de HTTP "*envia automaticamente resposta*" |Quer incluir um **resposta** ação ou não se encontra na definição de fluxo de trabalho de Olá |
| Configurar a autenticação básica ou OAuth |através da gestão de API |
| Configurar o método de HTTP |Em **Mostrar opções avançadas**, escolha um método HTTP |
| Configurar o caminho relativo |Em **Mostrar opções avançadas**, adicione um caminho relativo |
| Corpo de entrada de Olá de referência através da`@triggerOutputs().body.Content` |Referência através da`@triggerOutputs().body` |
| **Enviar uma resposta HTTP** ação no Olá serviço de escuta de HTTP |Clique em **respondeu tooHTTP pedido** (não existe nenhuma aplicação de API obrigatório) |

## <a name="get-help"></a>Obter ajuda

perguntas tooask, responda às perguntas e saiba que outras Azure Logic Apps os utilizadores estão a fazer, visite Olá [fórum de Azure Logic Apps](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).

toohelp melhorar Azure Logic Apps e conectores, votar em ou submeter ideias em Olá [site de comentários do utilizador do Azure Logic Apps](http://aka.ms/logicapps-wish).

## <a name="next-steps"></a>Passos seguintes

* [Criar definições de aplicação lógica](./logic-apps-author-definitions.md)
* [Lidar com erros e exceções](./logic-apps-exception-handling.md)

[1]: ./media/logic-apps-http-endpoint/manualtrigger.png
[2]: ./media/logic-apps-http-endpoint/manualtriggerurl.png
[3]: ./media/logic-apps-http-endpoint/response.png
