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
# <a name="call-trigger-or-nest-workflows-with-http-endpoints-in-logic-apps"></a><span data-ttu-id="2934b-104">Chamar, acionador, ou aninhar fluxos de trabalho com pontos finais HTTP nas logic apps</span><span class="sxs-lookup"><span data-stu-id="2934b-104">Call, trigger, or nest workflows with HTTP endpoints in logic apps</span></span>

<span data-ttu-id="2934b-105">Nativamente pode expor os pontos finais de HTTP síncronos como os acionadores nas logic apps para que possa acionar ou chamar as logic apps através de um URL.</span><span class="sxs-lookup"><span data-stu-id="2934b-105">You can natively expose synchronous HTTP endpoints as triggers on logic apps so that you can trigger or call your logic apps through a URL.</span></span> <span data-ttu-id="2934b-106">Também pode aninhar fluxos de trabalho nas suas logic apps utilizando um padrão de possível chamar EndRead pontos finais.</span><span class="sxs-lookup"><span data-stu-id="2934b-106">You can also nest workflows in your logic apps by using a pattern of callable endpoints.</span></span>

<span data-ttu-id="2934b-107">pontos finais HTTP toocreate, pode adicionar estes acionadores para que as logic apps podem receber pedidos de entrada:</span><span class="sxs-lookup"><span data-stu-id="2934b-107">toocreate HTTP endpoints, you can add these triggers so that your logic apps can receive incoming requests:</span></span>

* [<span data-ttu-id="2934b-108">Pedido</span><span class="sxs-lookup"><span data-stu-id="2934b-108">Request</span></span>](../connectors/connectors-native-reqres.md)

* [<span data-ttu-id="2934b-109">Webhook de ligação de API</span><span class="sxs-lookup"><span data-stu-id="2934b-109">API Connection Webhook</span></span>](logic-apps-workflow-actions-triggers.md#api-connection-trigger)

* [<span data-ttu-id="2934b-110">Webhook de HTTP</span><span class="sxs-lookup"><span data-stu-id="2934b-110">HTTP Webhook</span></span>](../connectors/connectors-native-webhook.md)

   > [!NOTE]
   > <span data-ttu-id="2934b-111">Apesar dos nossos exemplos utilizam Olá **pedido** acionador, pode utilizar qualquer um dos Olá listados acionadores HTTP e todos os princípios de forma idêntica aplicam toohello dos outros tipos de Acionador.</span><span class="sxs-lookup"><span data-stu-id="2934b-111">Although our examples use hello **Request** trigger, you can use any of hello listed HTTP triggers, and all principles identically apply toohello other trigger types.</span></span>

## <a name="set-up-an-http-endpoint-for-your-logic-app"></a><span data-ttu-id="2934b-112">Configurar um ponto final HTTP para a sua aplicação lógica</span><span class="sxs-lookup"><span data-stu-id="2934b-112">Set up an HTTP endpoint for your logic app</span></span>

<span data-ttu-id="2934b-113">toocreate um ponto final de HTTP, adicionar um acionador que pode receber pedidos recebidos.</span><span class="sxs-lookup"><span data-stu-id="2934b-113">toocreate an HTTP endpoint, add a trigger that can receive incoming requests.</span></span>

1. <span data-ttu-id="2934b-114">Inicie sessão no toohello [portal do Azure](https://portal.azure.com "portal do Azure").</span><span class="sxs-lookup"><span data-stu-id="2934b-114">Sign in toohello [Azure portal](https://portal.azure.com "Azure portal").</span></span> <span data-ttu-id="2934b-115">Aceda a aplicação de lógica de tooyour e abra o Designer de aplicação lógica.</span><span class="sxs-lookup"><span data-stu-id="2934b-115">Go tooyour logic app, and open Logic App Designer.</span></span>

2. <span data-ttu-id="2934b-116">Adicione um acionador que permite que a sua aplicação lógica receber pedidos recebidos.</span><span class="sxs-lookup"><span data-stu-id="2934b-116">Add a trigger that lets your logic app receive incoming requests.</span></span> <span data-ttu-id="2934b-117">Por exemplo, adicionar Olá **pedido** aplicação de lógica de tooyour de Acionador.</span><span class="sxs-lookup"><span data-stu-id="2934b-117">For example, add hello **Request** trigger tooyour logic app.</span></span>

3.  <span data-ttu-id="2934b-118">Em **esquema de JSON de corpo do pedido**, opcionalmente, pode introduzir um esquema JSON para o que esperar Olá acionador tooreceive payload de Olá (dados).</span><span class="sxs-lookup"><span data-stu-id="2934b-118">Under **Request Body JSON Schema**, you can optionally enter a JSON schema for hello payload (data) that you expect hello trigger tooreceive.</span></span>

    <span data-ttu-id="2934b-119">designer de Olá utiliza este esquema para gerar tokens que a sua aplicação lógica pode utilizar tooconsume, parse e transmita dados de Acionador de Olá através do seu fluxo de trabalho.</span><span class="sxs-lookup"><span data-stu-id="2934b-119">hello designer uses this schema for generating tokens that your logic app can use tooconsume, parse, and pass data from hello trigger through your workflow.</span></span> 
    <span data-ttu-id="2934b-120">Mais informações sobre como [tokens gerados a partir de esquemas JSON](#generated-tokens).</span><span class="sxs-lookup"><span data-stu-id="2934b-120">More about [tokens generated from JSON schemas](#generated-tokens).</span></span>

    <span data-ttu-id="2934b-121">Neste exemplo, introduza o esquema de Olá mostrada no designer de Olá:</span><span class="sxs-lookup"><span data-stu-id="2934b-121">For this example, enter hello schema shown in hello designer:</span></span>

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
    > <span data-ttu-id="2934b-123">Pode gerar um esquema para um payload JSON de exemplo a partir de uma ferramenta como o [jsonschema.net](http://jsonschema.net/), ou no Olá **pedido** acionador escolhendo **esquema de toogenerate de payload de exemplo de utilização**.</span><span class="sxs-lookup"><span data-stu-id="2934b-123">You can generate a schema for a sample JSON payload from a tool like [jsonschema.net](http://jsonschema.net/), or in hello **Request** trigger by choosing **Use sample payload toogenerate schema**.</span></span> 
    > <span data-ttu-id="2934b-124">Introduza o payload de exemplo e escolha **feito**.</span><span class="sxs-lookup"><span data-stu-id="2934b-124">Enter your sample payload, and choose **Done**.</span></span>

    <span data-ttu-id="2934b-125">Por exemplo, este payload de exemplo:</span><span class="sxs-lookup"><span data-stu-id="2934b-125">For example, this sample payload:</span></span>

    ```json
    {
       "address": "21 2nd Street, New York, New York"
    }
    ```

    <span data-ttu-id="2934b-126">gera neste esquema:</span><span class="sxs-lookup"><span data-stu-id="2934b-126">generates this schema:</span></span>

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

4.  <span data-ttu-id="2934b-127">Guarde a sua aplicação lógica.</span><span class="sxs-lookup"><span data-stu-id="2934b-127">Save your logic app.</span></span> <span data-ttu-id="2934b-128">Em **HTTP POST toothis URL**, agora deve encontrar um URL de chamada de retorno gerado, tal como neste exemplo:</span><span class="sxs-lookup"><span data-stu-id="2934b-128">Under **HTTP POST toothis URL**, you should now find a generated callback URL, like this example:</span></span>

    ![URL de chamada de retorno gerado para o ponto final](./media/logic-apps-http-endpoint/generated-endpoint-url.png)

    <span data-ttu-id="2934b-130">Este URL contém uma chave de assinatura de acesso partilhado (SAS) nos parâmetros de consulta de Olá que são utilizados para autenticação.</span><span class="sxs-lookup"><span data-stu-id="2934b-130">This URL contains a Shared Access Signature (SAS) key in hello query parameters that are used for authentication.</span></span> 
    <span data-ttu-id="2934b-131">Também pode obter o URL de ponto final HTTP Olá da sua descrição geral da aplicação lógica em Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="2934b-131">You can also get hello HTTP endpoint URL from your logic app overview in hello Azure portal.</span></span> <span data-ttu-id="2934b-132">Em **histórico de Acionador**, selecione o acionador:</span><span class="sxs-lookup"><span data-stu-id="2934b-132">Under **Trigger History**, select your trigger:</span></span>

    ![Obter o URL de ponto final HTTP a partir do portal do Azure][2]

    <span data-ttu-id="2934b-134">Ou pode obter o URL de Olá ao efetuar esta chamada:</span><span class="sxs-lookup"><span data-stu-id="2934b-134">Or you can get hello URL by making this call:</span></span>

    ```
    POST https://management.azure.com/{logic-app-resourceID}/triggers/{myendpointtrigger}/listCallbackURL?api-version=2016-06-01
    ```

## <a name="change-hello-http-method-for-your-trigger"></a><span data-ttu-id="2934b-135">Alterar o método HTTP Olá para o acionador</span><span class="sxs-lookup"><span data-stu-id="2934b-135">Change hello HTTP method for your trigger</span></span>

<span data-ttu-id="2934b-136">Por predefinição, Olá **pedido** acionador espera um pedido POST de HTTP, mas pode utilizar um método HTTP diferente.</span><span class="sxs-lookup"><span data-stu-id="2934b-136">By default, hello **Request** trigger expects an HTTP POST request, but you can use a different HTTP method.</span></span> 

> [!NOTE]
> <span data-ttu-id="2934b-137">Pode especificar o tipo de apenas um método.</span><span class="sxs-lookup"><span data-stu-id="2934b-137">You can specify only one method type.</span></span>

1. <span data-ttu-id="2934b-138">No seu **pedido** acionar, escolha **Mostrar opções avançadas**.</span><span class="sxs-lookup"><span data-stu-id="2934b-138">On your **Request** trigger, choose **Show advanced options**.</span></span>

2. <span data-ttu-id="2934b-139">Abra Olá **método** lista.</span><span class="sxs-lookup"><span data-stu-id="2934b-139">Open hello **Method** list.</span></span> <span data-ttu-id="2934b-140">Para este exemplo, selecione **obter** , para que possa testar URL do ponto final de HTTP mais tarde.</span><span class="sxs-lookup"><span data-stu-id="2934b-140">For this example, select **GET** so that you can test your HTTP endpoint's URL later.</span></span>

    > [!NOTE]
    > <span data-ttu-id="2934b-141">Pode selecionar qualquer outro método HTTP ou especificar um método personalizado para a sua própria aplicação lógica.</span><span class="sxs-lookup"><span data-stu-id="2934b-141">You can select any other HTTP method, or specify a custom method for your own logic app.</span></span>

    ![Alterar o método HTTP](./media/logic-apps-http-endpoint/change-method.png)

## <a name="accept-parameters-through-your-http-endpoint-url"></a><span data-ttu-id="2934b-143">Aceitar parâmetros através do seu URL de ponto final HTTP</span><span class="sxs-lookup"><span data-stu-id="2934b-143">Accept parameters through your HTTP endpoint URL</span></span>

<span data-ttu-id="2934b-144">Quando pretender que os parâmetros de tooaccept de URL de ponto final HTTP, personalize o caminho relativo do acionador.</span><span class="sxs-lookup"><span data-stu-id="2934b-144">When you want your HTTP endpoint URL tooaccept parameters, customize your trigger's relative path.</span></span>

1. <span data-ttu-id="2934b-145">No seu **pedido** acionar, escolha **Mostrar opções avançadas**.</span><span class="sxs-lookup"><span data-stu-id="2934b-145">On your **Request** trigger, choose **Show advanced options**.</span></span> 

2. <span data-ttu-id="2934b-146">Em **método**, especifique o método de Olá HTTP que pretende que o seu toouse de pedido.</span><span class="sxs-lookup"><span data-stu-id="2934b-146">Under **Method**, specify hello HTTP method that you want your request toouse.</span></span> <span data-ttu-id="2934b-147">Para este exemplo, selecione Olá **obter** método, se ainda não o fez, para que possa testar URL do ponto final de HTTP.</span><span class="sxs-lookup"><span data-stu-id="2934b-147">For this example, select hello **GET** method, if you haven't already, so that you can test your HTTP endpoint's URL.</span></span>

      > [!NOTE]
      > <span data-ttu-id="2934b-148">Quando especificar um caminho relativo para o acionador, tem de especificar também explicitamente um método HTTP para o acionador.</span><span class="sxs-lookup"><span data-stu-id="2934b-148">When you specify a relative path for your trigger, you must also explicitly specify an HTTP method for your trigger.</span></span>

3. <span data-ttu-id="2934b-149">Em **caminho relativo**, especifique Olá caminho relativo para o parâmetro de Olá que deve aceitar o URL, por exemplo, `customers/{customerID}`.</span><span class="sxs-lookup"><span data-stu-id="2934b-149">Under **Relative path**, specify hello relative path for hello parameter that your URL should accept, for example, `customers/{customerID}`.</span></span>

    ![Especifique o método HTTP Olá e o caminho relativo para o parâmetro](./media/logic-apps-http-endpoint/relativeurl.png)

4. <span data-ttu-id="2934b-151">toouse Olá parâmetro, adicione um **resposta** aplicação de lógica de tooyour de ação.</span><span class="sxs-lookup"><span data-stu-id="2934b-151">toouse hello parameter, add a **Response** action tooyour logic app.</span></span> <span data-ttu-id="2934b-152">(Sob o acionador, escolha **novo passo** > **adicionar uma ação** > **resposta**)</span><span class="sxs-lookup"><span data-stu-id="2934b-152">(Under your trigger, choose **New step** > **Add an action** > **Response**)</span></span> 

5. <span data-ttu-id="2934b-153">Na sua resposta **corpo**, inclui Olá o token para o parâmetro de Olá que especificou no caminho relativo do acionador.</span><span class="sxs-lookup"><span data-stu-id="2934b-153">In your response's **Body**, include hello token for hello parameter that you specified in your trigger's relative path.</span></span>

    <span data-ttu-id="2934b-154">Por exemplo, tooreturn `Hello {customerID}`, atualize a sua resposta **corpo** com `Hello {customerID token}`.</span><span class="sxs-lookup"><span data-stu-id="2934b-154">For example, tooreturn `Hello {customerID}`, update your response's **Body** with `Hello {customerID token}`.</span></span> 
    <span data-ttu-id="2934b-155">lista de conteúdo dinâmico Olá deve aparecer e Mostrar Olá `customerID` token para tooselect.</span><span class="sxs-lookup"><span data-stu-id="2934b-155">hello dynamic content list should appear and show hello `customerID` token for you tooselect.</span></span>

    ![Adicionar o corpo do parâmetro tooresponse](./media/logic-apps-http-endpoint/relativeurlresponse.png)

    <span data-ttu-id="2934b-157">O **corpo** deverá ser semelhante neste exemplo:</span><span class="sxs-lookup"><span data-stu-id="2934b-157">Your **Body** should look like this example:</span></span>

    ![Corpo de resposta com o parâmetro](./media/logic-apps-http-endpoint/relative-url-with-parameter.png)

6. <span data-ttu-id="2934b-159">Guarde a sua aplicação lógica.</span><span class="sxs-lookup"><span data-stu-id="2934b-159">Save your logic app.</span></span> 

    <span data-ttu-id="2934b-160">O URL de ponto final HTTP inclui agora o caminho relativo Olá, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="2934b-160">Your HTTP endpoint URL now includes hello relative path, for example:</span></span> 

    <span data-ttu-id="2934b-161">https & # 58;//prod-00.southcentralus.logic.azure.com/workflows/f90cb66c52ea4e9cabe0abf4e197deff/triggers/manual/paths/invoke/customers/{customerID}...</span><span class="sxs-lookup"><span data-stu-id="2934b-161">https&#58;//prod-00.southcentralus.logic.azure.com/workflows/f90cb66c52ea4e9cabe0abf4e197deff/triggers/manual/paths/invoke/customers/{customerID}...</span></span>

7. <span data-ttu-id="2934b-162">tootest o ponto final de HTTP, cópia e colagem Olá URL atualizado na outra janela do browser, mas substituem `{customerID}` com `123456`, e prima Enter.</span><span class="sxs-lookup"><span data-stu-id="2934b-162">tootest your HTTP endpoint, copy and paste hello updated URL into another browser window, but replace `{customerID}` with `123456`, and press Enter.</span></span>

    <span data-ttu-id="2934b-163">O browser deve mostrar este texto:</span><span class="sxs-lookup"><span data-stu-id="2934b-163">Your browser should show this text:</span></span> 

    `Hello 123456`

<a name="generated-tokens"></a>
### <a name="tokens-generated-from-json-schemas-for-your-logic-app"></a><span data-ttu-id="2934b-164">Tokens gerados a partir de esquemas JSON para a sua aplicação lógica</span><span class="sxs-lookup"><span data-stu-id="2934b-164">Tokens generated from JSON schemas for your logic app</span></span>

<span data-ttu-id="2934b-165">Quando fornecer o esquema JSON na sua **pedido** acionar, hello Designer de aplicação lógica gera tokens para propriedades que esquema.</span><span class="sxs-lookup"><span data-stu-id="2934b-165">When you provide a JSON schema in your **Request** trigger, hello Logic App Designer generates tokens for properties in that schema.</span></span> <span data-ttu-id="2934b-166">Em seguida, pode utilizar esses tokens para transmitir dados através do seu fluxo de trabalho de aplicação lógica.</span><span class="sxs-lookup"><span data-stu-id="2934b-166">You can then use those tokens for passing data through your logic app workflow.</span></span>

<span data-ttu-id="2934b-167">Neste exemplo, se adicionar Olá `title` e `name` esquema JSON tooyour de propriedades, os seus tokens estão agora disponível toouse em passos posteriores do fluxo de trabalho.</span><span class="sxs-lookup"><span data-stu-id="2934b-167">For this example, if you add hello `title` and `name` properties tooyour JSON schema, their tokens are now available toouse in later workflow steps.</span></span> 

<span data-ttu-id="2934b-168">Segue-se o esquema JSON concluída Olá:</span><span class="sxs-lookup"><span data-stu-id="2934b-168">Here is hello complete JSON schema:</span></span>

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

## <a name="create-nested-workflows-for-logic-apps"></a><span data-ttu-id="2934b-169">Criar fluxos de trabalho aninhados para aplicações lógicas</span><span class="sxs-lookup"><span data-stu-id="2934b-169">Create nested workflows for logic apps</span></span>

<span data-ttu-id="2934b-170">Pode ser aninhado fluxos de trabalho na sua aplicação lógica adicionando outras as logic apps que podem receber pedidos.</span><span class="sxs-lookup"><span data-stu-id="2934b-170">You can nest workflows in your logic app by adding other logic apps that can receive requests.</span></span> <span data-ttu-id="2934b-171">tooinclude estes logic apps, adicionar Olá **Azure Logic Apps - escolha um fluxo de trabalho Logic Apps** acionador tooyour de ação.</span><span class="sxs-lookup"><span data-stu-id="2934b-171">tooinclude these logic apps, add hello **Azure Logic Apps - Choose a Logic Apps workflow** action tooyour trigger.</span></span> <span data-ttu-id="2934b-172">Em seguida, pode selecionar a partir de aplicações lógicas elegível.</span><span class="sxs-lookup"><span data-stu-id="2934b-172">You can then select from eligible logic apps.</span></span>

![Adicionar outra aplicação lógica](./media/logic-apps-http-endpoint/choose-logic-apps-workflow.png)

## <a name="call-or-trigger-logic-apps-through-http-endpoints"></a><span data-ttu-id="2934b-174">Chamar ou acionar as logic apps através de pontos finais HTTP</span><span class="sxs-lookup"><span data-stu-id="2934b-174">Call or trigger logic apps through HTTP endpoints</span></span>

<span data-ttu-id="2934b-175">Depois de criar o ponto final de HTTP, pode acionar a sua aplicação lógica através de um `POST` URL completo do método toohello.</span><span class="sxs-lookup"><span data-stu-id="2934b-175">After you create your HTTP endpoint, you can trigger your logic app through a `POST` method toohello full URL.</span></span> <span data-ttu-id="2934b-176">As Logic apps têm suporte incorporado para pontos finais de acesso direto.</span><span class="sxs-lookup"><span data-stu-id="2934b-176">Logic apps have built-in support for direct-access endpoints.</span></span>

## <a name="reference-content-from-an-incoming-request"></a><span data-ttu-id="2934b-177">Conteúdo de referência de um pedido recebido</span><span class="sxs-lookup"><span data-stu-id="2934b-177">Reference content from an incoming request</span></span>

<span data-ttu-id="2934b-178">Olá conteúdo type do estiver `application/json`, pode referenciar propriedades do pedido de entrada Olá.</span><span class="sxs-lookup"><span data-stu-id="2934b-178">If hello content's type is `application/json`, you can reference properties from hello incoming request.</span></span> <span data-ttu-id="2934b-179">Caso contrário, conteúdo é tratado como uma única unidade binária, que pode decorrer tooother APIs.</span><span class="sxs-lookup"><span data-stu-id="2934b-179">Otherwise, content is treated as a single binary unit that you can pass tooother APIs.</span></span> <span data-ttu-id="2934b-180">tooreference este conteúdo no interior do fluxo de trabalho Olá, tem de converter esse conteúdo.</span><span class="sxs-lookup"><span data-stu-id="2934b-180">tooreference this content inside hello workflow, you must convert that content.</span></span> <span data-ttu-id="2934b-181">Por exemplo, se passa `application/xml` conteúdo, pode utilizar `@xpath()` para extração um XPath, ou `@json()` para a conversão XML tooJSON.</span><span class="sxs-lookup"><span data-stu-id="2934b-181">For example, if you pass `application/xml` content, you can use `@xpath()` for an XPath extraction, or `@json()` for converting XML tooJSON.</span></span> <span data-ttu-id="2934b-182">Saiba mais sobre [trabalhar com os tipos de conteúdo](../logic-apps/logic-apps-content-type.md).</span><span class="sxs-lookup"><span data-stu-id="2934b-182">Learn about [working with content types](../logic-apps/logic-apps-content-type.md).</span></span>

<span data-ttu-id="2934b-183">Olá tooget de saída de um pedido de entrada, pode utilizar Olá `@triggerOutputs()` função.</span><span class="sxs-lookup"><span data-stu-id="2934b-183">tooget hello output from an incoming request, you can use hello `@triggerOutputs()` function.</span></span> <span data-ttu-id="2934b-184">saída de Olá aspeto que poderá ter neste exemplo:</span><span class="sxs-lookup"><span data-stu-id="2934b-184">hello output might look like this example:</span></span>

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

<span data-ttu-id="2934b-185">Olá tooaccess `body` propriedade especificamente, pode utilizar Olá `@triggerBody()` atalho.</span><span class="sxs-lookup"><span data-stu-id="2934b-185">tooaccess hello `body` property specifically, you can use hello `@triggerBody()` shortcut.</span></span> 

## <a name="respond-toorequests"></a><span data-ttu-id="2934b-186">Responder toorequests</span><span class="sxs-lookup"><span data-stu-id="2934b-186">Respond toorequests</span></span>

<span data-ttu-id="2934b-187">Pode querer toorespond toocertain pedidos que iniciar uma aplicação lógica devolvendo toohello conteúdo autor da chamada.</span><span class="sxs-lookup"><span data-stu-id="2934b-187">You might want toorespond toocertain requests that start a logic app by returning content toohello caller.</span></span> <span data-ttu-id="2934b-188">código de estado de Olá tooconstruct, o cabeçalho e o corpo da sua resposta, pode utilizar Olá **resposta** ação.</span><span class="sxs-lookup"><span data-stu-id="2934b-188">tooconstruct hello status code, header, and body for your response, you can use hello **Response** action.</span></span> <span data-ttu-id="2934b-189">Esta ação pode aparecer em qualquer local na sua aplicação lógica, não apenas no final de Olá do fluxo de trabalho.</span><span class="sxs-lookup"><span data-stu-id="2934b-189">This action can appear anywhere in your logic app, not just at hello end of your workflow.</span></span>

> [!NOTE] 
> <span data-ttu-id="2934b-190">Se a sua aplicação lógica não inclui um **resposta**, ponto final de Olá HTTP responde *imediatamente* com um **aceites 202** estado.</span><span class="sxs-lookup"><span data-stu-id="2934b-190">If your logic app doesn't include a **Response**, hello HTTP endpoint responds *immediately* with a **202 Accepted** status.</span></span> <span data-ttu-id="2934b-191">Além disso, para original pedido tooget Olá resposta Olá, todos os passos necessários para resposta Olá devem ser concluído dentro do Olá [limite de tempo limite do pedido](./logic-apps-limits-and-config.md) , exceto se chamar o fluxo de trabalho Olá como uma aplicação lógica aninhada.</span><span class="sxs-lookup"><span data-stu-id="2934b-191">Also, for hello original request tooget hello response, all steps required for hello response must finish within hello [request timeout limit](./logic-apps-limits-and-config.md) unless you call hello workflow as a nested logic app.</span></span> <span data-ttu-id="2934b-192">Se nenhuma resposta acontece este limite, o pedido recebido Olá exceder o tempo limite e recebe a resposta HTTP de Olá **tempo limite de cliente 408**.</span><span class="sxs-lookup"><span data-stu-id="2934b-192">If no response happens within this limit, hello incoming request times out and receives hello HTTP response **408 Client timeout**.</span></span> <span data-ttu-id="2934b-193">Para aplicações lógicas aninhados, a aplicação de lógica de principal de Olá continua toowait para uma resposta até à conclusão, independentemente da quanto tempo é necessário.</span><span class="sxs-lookup"><span data-stu-id="2934b-193">For nested logic apps, hello parent logic app continues toowait for a response until completed, regardless of how much time is required.</span></span>

### <a name="construct-hello-response"></a><span data-ttu-id="2934b-194">Construir a resposta Olá</span><span class="sxs-lookup"><span data-stu-id="2934b-194">Construct hello response</span></span>

<span data-ttu-id="2934b-195">Pode incluir mais do que um cabeçalho e qualquer tipo de conteúdo no corpo de resposta de Olá.</span><span class="sxs-lookup"><span data-stu-id="2934b-195">You can include more than one header and any type of content in hello response body.</span></span> <span data-ttu-id="2934b-196">No nosso exemplo de resposta, o cabeçalho de Olá Especifica que resposta Olá tem o tipo de conteúdo `application/json`.</span><span class="sxs-lookup"><span data-stu-id="2934b-196">In our example response, hello header specifies that hello response has content type `application/json`.</span></span> <span data-ttu-id="2934b-197">e Olá corpo contém `title` e `name`, com base no esquema JSON Olá anteriormente atualizado para incluir Olá **pedido** acionador.</span><span class="sxs-lookup"><span data-stu-id="2934b-197">and hello body contains `title` and `name`, based on hello JSON schema updated previously for hello **Request** trigger.</span></span>

![Ação de resposta de HTTP][3]

<span data-ttu-id="2934b-199">As respostas têm estas propriedades:</span><span class="sxs-lookup"><span data-stu-id="2934b-199">Responses have these properties:</span></span>

| <span data-ttu-id="2934b-200">Propriedade</span><span class="sxs-lookup"><span data-stu-id="2934b-200">Property</span></span> | <span data-ttu-id="2934b-201">Descrição</span><span class="sxs-lookup"><span data-stu-id="2934b-201">Description</span></span> |
| --- | --- |
| <span data-ttu-id="2934b-202">statusCode</span><span class="sxs-lookup"><span data-stu-id="2934b-202">statusCode</span></span> |<span data-ttu-id="2934b-203">Especifica o código de estado de Olá HTTP para o pedido de entrada toohello está a responder.</span><span class="sxs-lookup"><span data-stu-id="2934b-203">Specifies hello HTTP status code for responding toohello incoming request.</span></span> <span data-ttu-id="2934b-204">Este código pode ser qualquer código de estado válido que comece com 2xx, 4xx ou 5xx.</span><span class="sxs-lookup"><span data-stu-id="2934b-204">This code can be any valid status code that starts with 2xx, 4xx, or 5xx.</span></span> <span data-ttu-id="2934b-205">No entanto, os códigos de estado de 3xx não são permitidos.</span><span class="sxs-lookup"><span data-stu-id="2934b-205">However, 3xx status codes are not permitted.</span></span> |
| <span data-ttu-id="2934b-206">Cabeçalhos</span><span class="sxs-lookup"><span data-stu-id="2934b-206">headers</span></span> |<span data-ttu-id="2934b-207">Define a qualquer número de cabeçalhos tooinclude na resposta Olá.</span><span class="sxs-lookup"><span data-stu-id="2934b-207">Defines any number of headers tooinclude in hello response.</span></span> |
| <span data-ttu-id="2934b-208">Corpo</span><span class="sxs-lookup"><span data-stu-id="2934b-208">body</span></span> |<span data-ttu-id="2934b-209">Especifica um objeto de corpo pode ser uma cadeia, um objeto JSON ou mesmo binário conteúdo referenciado a partir de um passo anterior.</span><span class="sxs-lookup"><span data-stu-id="2934b-209">Specifies a body object that can be a string, a JSON object, or even binary content referenced from a previous step.</span></span> |

<span data-ttu-id="2934b-210">Eis o esquema JSON Olá parece agora para Olá **resposta** ação:</span><span class="sxs-lookup"><span data-stu-id="2934b-210">Here's what hello JSON schema looks like now for hello **Response** action:</span></span>

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
> <span data-ttu-id="2934b-211">Escolha a definição de JSON de conclua de Olá do tooview para a sua aplicação lógica, no Olá Designer de aplicação lógica, **Code vista**.</span><span class="sxs-lookup"><span data-stu-id="2934b-211">tooview hello complete JSON definition for your logic app, on hello Logic App Designer, choose **Code view**.</span></span>

## <a name="q--a"></a><span data-ttu-id="2934b-212">P&R</span><span class="sxs-lookup"><span data-stu-id="2934b-212">Q & A</span></span>

#### <a name="q-what-about-url-security"></a><span data-ttu-id="2934b-213">P: E sobre segurança URL?</span><span class="sxs-lookup"><span data-stu-id="2934b-213">Q: What about URL security?</span></span>

<span data-ttu-id="2934b-214">R: azure gera em segurança URLs da chamada de retorno de aplicação de lógica com uma assinatura de acesso partilhado (SAS).</span><span class="sxs-lookup"><span data-stu-id="2934b-214">A: Azure securely generates logic app callback URLs using a Shared Access Signature (SAS).</span></span> <span data-ttu-id="2934b-215">Esta assinatura atravessa como um parâmetro de consulta e tem de ser validada antes da aplicação lógica pode acionados.</span><span class="sxs-lookup"><span data-stu-id="2934b-215">This signature passes through as a query parameter and must be validated before your logic app can fire.</span></span> <span data-ttu-id="2934b-216">O Azure gera assinatura Olá utilizando uma combinação exclusiva de uma chave secreta por aplicação lógica, o nome do acionador Olá e operação Olá que é executada.</span><span class="sxs-lookup"><span data-stu-id="2934b-216">Azure generates hello signature using a unique combination of a secret key per logic app, hello trigger name, and hello operation that's performed.</span></span> <span data-ttu-id="2934b-217">Por isso, a menos que alguém tenha a chave de acesso toohello lógica segredo aplicação, não é possível gerar uma assinatura válida.</span><span class="sxs-lookup"><span data-stu-id="2934b-217">So unless someone has access toohello secret logic app key, they cannot generate a valid signature.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="2934b-218">Para produção e sistemas seguros, Desaconselhamos vivamente a sua aplicação lógica ao chamar diretamente a partir do browser Olá porque:</span><span class="sxs-lookup"><span data-stu-id="2934b-218">For production and secure systems, we strongly recommend against calling your logic app directly from hello browser because:</span></span>
   > 
   > * <span data-ttu-id="2934b-219">chave de acesso partilhado Olá é apresentado no URL Olá.</span><span class="sxs-lookup"><span data-stu-id="2934b-219">hello shared access key appears in hello URL.</span></span>
   > * <span data-ttu-id="2934b-220">Não é possível gerir políticas de conteúdo seguras devido tooshared domínios em clientes de aplicação lógica.</span><span class="sxs-lookup"><span data-stu-id="2934b-220">You can't manage secure content policies due tooshared domains across Logic App customers.</span></span>

#### <a name="q-can-i-configure-http-endpoints-further"></a><span data-ttu-id="2934b-221">P: posso configurar pontos finais de HTTP mais?</span><span class="sxs-lookup"><span data-stu-id="2934b-221">Q: Can I configure HTTP endpoints further?</span></span>

<span data-ttu-id="2934b-222">R: Sim, pontos finais de HTTP suportam a configuração mais avançada através de [ **API Management**](../api-management/api-management-key-concepts.md).</span><span class="sxs-lookup"><span data-stu-id="2934b-222">A: Yes, HTTP endpoints support more advanced configuration through [**API Management**](../api-management/api-management-key-concepts.md).</span></span> <span data-ttu-id="2934b-223">Este serviço também oferece a capacidade de Olá para tooconsistently faça a gestão de todas as suas APIs, incluindo as logic apps, configurar os nomes de domínio personalizado, utilize mais métodos de autenticação e muito mais, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="2934b-223">This service also offers hello capability for you tooconsistently manage all your APIs, including logic apps, set up custom domain names, use more authentication methods, and more, for example:</span></span>

* [<span data-ttu-id="2934b-224">Alterar método de pedido de Olá</span><span class="sxs-lookup"><span data-stu-id="2934b-224">Change hello request method</span></span>](https://docs.microsoft.com/azure/api-management/api-management-advanced-policies#SetRequestMethod)
* [<span data-ttu-id="2934b-225">Alterar os segmentos de URL de pedido de Olá Olá</span><span class="sxs-lookup"><span data-stu-id="2934b-225">Change hello URL segments of hello request</span></span>](https://docs.microsoft.com/azure/api-management/api-management-transformation-policies#RewriteURL)
* <span data-ttu-id="2934b-226">Configurar os domínios de gestão de API no Olá [portal do Azure](https://portal.azure.com/ "portal do Azure")</span><span class="sxs-lookup"><span data-stu-id="2934b-226">Set up your API Management domains in hello [Azure portal](https://portal.azure.com/ "Azure portal")</span></span>
* <span data-ttu-id="2934b-227">Configurar a política toocheck para a autenticação básica</span><span class="sxs-lookup"><span data-stu-id="2934b-227">Set up policy toocheck for Basic authentication</span></span>

#### <a name="q-what-changed-when-hello-schema-migrated-from-hello-december-1-2014-preview"></a><span data-ttu-id="2934b-228">P: o que foi alterado quando esquema Olá migrado a partir da pré-visualização de 1 de Dezembro de 2014 Olá?</span><span class="sxs-lookup"><span data-stu-id="2934b-228">Q: What changed when hello schema migrated from hello December 1, 2014 preview?</span></span>

<span data-ttu-id="2934b-229">R: Eis um resumo sobre estas alterações:</span><span class="sxs-lookup"><span data-stu-id="2934b-229">A: Here's a summary about these changes:</span></span>

| <span data-ttu-id="2934b-230">Pré-visualização de 1 de Dezembro de 2014</span><span class="sxs-lookup"><span data-stu-id="2934b-230">December 1, 2014 preview</span></span> | <span data-ttu-id="2934b-231">1 de Junho de 2016</span><span class="sxs-lookup"><span data-stu-id="2934b-231">June 1, 2016</span></span> |
| --- | --- |
| <span data-ttu-id="2934b-232">Clique em **serviço de escuta HTTP** aplicação API</span><span class="sxs-lookup"><span data-stu-id="2934b-232">Click **HTTP Listener** API App</span></span> |<span data-ttu-id="2934b-233">Clique em **acionador Manual** (não existe nenhuma aplicação de API obrigatório)</span><span class="sxs-lookup"><span data-stu-id="2934b-233">Click **Manual trigger** (no API App required)</span></span> |
| <span data-ttu-id="2934b-234">Definição de serviço de escuta de HTTP "*envia automaticamente resposta*"</span><span class="sxs-lookup"><span data-stu-id="2934b-234">HTTP Listener setting "*Sends response automatically*"</span></span> |<span data-ttu-id="2934b-235">Quer incluir um **resposta** ação ou não se encontra na definição de fluxo de trabalho de Olá</span><span class="sxs-lookup"><span data-stu-id="2934b-235">Either include a **Response** action or not in hello workflow definition</span></span> |
| <span data-ttu-id="2934b-236">Configurar a autenticação básica ou OAuth</span><span class="sxs-lookup"><span data-stu-id="2934b-236">Configure Basic or OAuth authentication</span></span> |<span data-ttu-id="2934b-237">através da gestão de API</span><span class="sxs-lookup"><span data-stu-id="2934b-237">via API Management</span></span> |
| <span data-ttu-id="2934b-238">Configurar o método de HTTP</span><span class="sxs-lookup"><span data-stu-id="2934b-238">Configure HTTP method</span></span> |<span data-ttu-id="2934b-239">Em **Mostrar opções avançadas**, escolha um método HTTP</span><span class="sxs-lookup"><span data-stu-id="2934b-239">Under **Show advanced options**, choose an HTTP method</span></span> |
| <span data-ttu-id="2934b-240">Configurar o caminho relativo</span><span class="sxs-lookup"><span data-stu-id="2934b-240">Configure relative path</span></span> |<span data-ttu-id="2934b-241">Em **Mostrar opções avançadas**, adicione um caminho relativo</span><span class="sxs-lookup"><span data-stu-id="2934b-241">Under **Show advanced options**, add a relative path</span></span> |
| <span data-ttu-id="2934b-242">Corpo de entrada de Olá de referência através da`@triggerOutputs().body.Content`</span><span class="sxs-lookup"><span data-stu-id="2934b-242">Reference hello incoming body through `@triggerOutputs().body.Content`</span></span> |<span data-ttu-id="2934b-243">Referência através da`@triggerOutputs().body`</span><span class="sxs-lookup"><span data-stu-id="2934b-243">Reference through `@triggerOutputs().body`</span></span> |
| <span data-ttu-id="2934b-244">**Enviar uma resposta HTTP** ação no Olá serviço de escuta de HTTP</span><span class="sxs-lookup"><span data-stu-id="2934b-244">**Send HTTP response** action on hello HTTP Listener</span></span> |<span data-ttu-id="2934b-245">Clique em **respondeu tooHTTP pedido** (não existe nenhuma aplicação de API obrigatório)</span><span class="sxs-lookup"><span data-stu-id="2934b-245">Click **Respond tooHTTP request** (no API App required)</span></span> |

## <a name="get-help"></a><span data-ttu-id="2934b-246">Obter ajuda</span><span class="sxs-lookup"><span data-stu-id="2934b-246">Get help</span></span>

<span data-ttu-id="2934b-247">perguntas tooask, responda às perguntas e saiba que outras Azure Logic Apps os utilizadores estão a fazer, visite Olá [fórum de Azure Logic Apps](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span><span class="sxs-lookup"><span data-stu-id="2934b-247">tooask questions, answer questions, and learn what other Azure Logic Apps users are doing, visit hello [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span></span>

<span data-ttu-id="2934b-248">toohelp melhorar Azure Logic Apps e conectores, votar em ou submeter ideias em Olá [site de comentários do utilizador do Azure Logic Apps](http://aka.ms/logicapps-wish).</span><span class="sxs-lookup"><span data-stu-id="2934b-248">toohelp improve Azure Logic Apps and connectors, vote on or submit ideas at hello [Azure Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span></span>

## <a name="next-steps"></a><span data-ttu-id="2934b-249">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="2934b-249">Next steps</span></span>

* [<span data-ttu-id="2934b-250">Criar definições de aplicação lógica</span><span class="sxs-lookup"><span data-stu-id="2934b-250">Author logic app definitions</span></span>](./logic-apps-author-definitions.md)
* [<span data-ttu-id="2934b-251">Lidar com erros e exceções</span><span class="sxs-lookup"><span data-stu-id="2934b-251">Handle errors and exceptions</span></span>](./logic-apps-exception-handling.md)

[1]: ./media/logic-apps-http-endpoint/manualtrigger.png
[2]: ./media/logic-apps-http-endpoint/manualtriggerurl.png
[3]: ./media/logic-apps-http-endpoint/response.png
