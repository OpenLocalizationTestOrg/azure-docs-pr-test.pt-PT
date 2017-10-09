---
title: "aaaCommunicate com qualquer ponto final através de HTTP - Azure Logic Apps | Microsoft Docs"
description: "Criar as logic apps que podem comunicar com qualquer ponto final através de HTTP"
services: logic-apps
author: jeffhollan
manager: anneta
editor: 
documentationcenter: 
tags: connectors
ms.assetid: e11c6b4d-65a5-4d2d-8e13-38150db09c0b
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/15/2016
ms.author: jehollan; LADocs
ms.openlocfilehash: 9793601839437a2b880bdb81e15881270cacc963
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-http-action"></a><span data-ttu-id="9b5b7-103">Introdução ao hello ação de HTTP</span><span class="sxs-lookup"><span data-stu-id="9b5b7-103">Get started with hello HTTP action</span></span>

<span data-ttu-id="9b5b7-104">Com a ação de HTTP Olá, pode expandir fluxos de trabalho para a sua organização e comunicar o ponto final de tooany através de HTTP.</span><span class="sxs-lookup"><span data-stu-id="9b5b7-104">With hello HTTP action, you can extend workflows for your organization and communicate tooany endpoint over HTTP.</span></span>

<span data-ttu-id="9b5b7-105">Pode:</span><span class="sxs-lookup"><span data-stu-id="9b5b7-105">You can:</span></span>

* <span data-ttu-id="9b5b7-106">Crie lógica fluxos de trabalho da aplicação que ativar (acionador) quando um site que gere fica inativo.</span><span class="sxs-lookup"><span data-stu-id="9b5b7-106">Create logic app workflows that activate (trigger) when a website that you manage goes down.</span></span>
* <span data-ttu-id="9b5b7-107">Comunicar tooany endpoint através de HTTP tooextend os fluxos de trabalho noutros serviços.</span><span class="sxs-lookup"><span data-stu-id="9b5b7-107">Communicate tooany endpoint over HTTP tooextend your workflows into other services.</span></span>

<span data-ttu-id="9b5b7-108">tooget iniciado utilizando a ação de Olá HTTP numa aplicação lógica, consulte [criar uma aplicação lógica](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="9b5b7-108">tooget started using hello HTTP action in a logic app, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="use-hello-http-trigger"></a><span data-ttu-id="9b5b7-109">Utilize o trigger de Olá HTTP</span><span class="sxs-lookup"><span data-stu-id="9b5b7-109">Use hello HTTP trigger</span></span>
<span data-ttu-id="9b5b7-110">Um acionador é um evento que pode ser o fluxo de trabalho do toostart utilizados Olá que está definido uma aplicação lógica.</span><span class="sxs-lookup"><span data-stu-id="9b5b7-110">A trigger is an event that can be used toostart hello workflow that is defined in a logic app.</span></span> <span data-ttu-id="9b5b7-111">[Saiba mais sobre acionadores](connectors-overview.md).</span><span class="sxs-lookup"><span data-stu-id="9b5b7-111">[Learn more about triggers](connectors-overview.md).</span></span>

<span data-ttu-id="9b5b7-112">Eis um exemplo de sequência de como tooset segurança Olá HTTP acionar no Olá Designer de aplicação lógica.</span><span class="sxs-lookup"><span data-stu-id="9b5b7-112">Here’s an example sequence of how tooset up hello HTTP trigger in hello Logic App Designer.</span></span>

1. <span data-ttu-id="9b5b7-113">Adicione o acionador HTTP Olá na sua aplicação lógica.</span><span class="sxs-lookup"><span data-stu-id="9b5b7-113">Add hello HTTP trigger in your logic app.</span></span>
2. <span data-ttu-id="9b5b7-114">Preencha os parâmetros de Olá para o ponto final de Olá HTTP que pretende que o toopoll.</span><span class="sxs-lookup"><span data-stu-id="9b5b7-114">Fill in hello parameters for hello HTTP endpoint that you want toopoll.</span></span>
3. <span data-ttu-id="9b5b7-115">Modificar o intervalo de periodicidade Olá na frequência deve consultar.</span><span class="sxs-lookup"><span data-stu-id="9b5b7-115">Modify hello recurrence interval on how frequently it should poll.</span></span>

   <span data-ttu-id="9b5b7-116">aplicação de lógica de Olá agora desencadeado com qualquer conteúdo que é devolvido durante a verificação de cada.</span><span class="sxs-lookup"><span data-stu-id="9b5b7-116">hello logic app now fires with any content that is returned during each check.</span></span>

   ![Acionador HTTP](./media/connectors-native-http/using-trigger.png)

### <a name="how-hello-http-trigger-works"></a><span data-ttu-id="9b5b7-118">Como funciona o acionador HTTP Olá</span><span class="sxs-lookup"><span data-stu-id="9b5b7-118">How hello HTTP trigger works</span></span>

<span data-ttu-id="9b5b7-119">acionador HTTP Olá envia um ponto final da chamada tooHTTP num intervalo periódico.</span><span class="sxs-lookup"><span data-stu-id="9b5b7-119">hello HTTP trigger sends a call tooHTTP endpoint on a recurring interval.</span></span> <span data-ttu-id="9b5b7-120">Por predefinição, os códigos de resposta HTTP são inferior a 300 faz com que um toorun de aplicação lógica.</span><span class="sxs-lookup"><span data-stu-id="9b5b7-120">By default, any HTTP response code that is lower than 300 causes a logic app toorun.</span></span> <span data-ttu-id="9b5b7-121">toospecify se a aplicação de lógica de Olá deve acionados, pode editar a aplicação de lógica de Olá na vista de código e adicionar uma condição que avalia após Olá chamada HTTP.</span><span class="sxs-lookup"><span data-stu-id="9b5b7-121">toospecify whether hello logic app should fire, you can edit hello logic app in code view, and add a condition that evaluates after hello HTTP call.</span></span> <span data-ttu-id="9b5b7-122">Eis um exemplo de um acionador HTTP que é acionado quando Olá devolveu o código de estado é maior que ou igual a demasiado`400`.</span><span class="sxs-lookup"><span data-stu-id="9b5b7-122">Here's an example of an HTTP trigger that fires when hello returned status code is greater than or equal too`400`.</span></span>

```javascript
"Http":
{
    "conditions": [
        {
            "expression": "@greaterOrEquals(triggerOutputs()['statusCode'], 400)"
        }
    ],
    "inputs": {
        "method": "GET",
        "uri": "https://blogs.msdn.microsoft.com/logicapps/",
        "headers": {
            "accept-language": "en"
        }
    },
    "recurrence": {
        "frequency": "Second",
        "interval": 15
    },
    "type": "Http"
}
```

<span data-ttu-id="9b5b7-123">Detalhes completos sobre os parâmetros de Acionador de Olá HTTP estão disponíveis no [MSDN](https://msdn.microsoft.com/library/azure/mt643939.aspx#HTTP-trigger).</span><span class="sxs-lookup"><span data-stu-id="9b5b7-123">Full details about hello HTTP trigger parameters are available on [MSDN](https://msdn.microsoft.com/library/azure/mt643939.aspx#HTTP-trigger).</span></span>

## <a name="use-hello-http-action"></a><span data-ttu-id="9b5b7-124">Utilize a ação de Olá HTTP</span><span class="sxs-lookup"><span data-stu-id="9b5b7-124">Use hello HTTP action</span></span>

<span data-ttu-id="9b5b7-125">Uma ação é uma operação que é efetuada pelo fluxo de trabalho de Olá que está definido uma aplicação lógica.</span><span class="sxs-lookup"><span data-stu-id="9b5b7-125">An action is an operation that is carried out by hello workflow that is defined in a logic app.</span></span> 
<span data-ttu-id="9b5b7-126">[Saiba mais sobre as ações](connectors-overview.md).</span><span class="sxs-lookup"><span data-stu-id="9b5b7-126">[Learn more about actions](connectors-overview.md).</span></span>

1. <span data-ttu-id="9b5b7-127">Escolha **novo passo** > **adicionar uma ação**.</span><span class="sxs-lookup"><span data-stu-id="9b5b7-127">Choose **New Step** > **Add an action**.</span></span>
3. <span data-ttu-id="9b5b7-128">Na caixa de pesquisa de ação de Olá, escreva **http** ações de Olá HTTP toolist.</span><span class="sxs-lookup"><span data-stu-id="9b5b7-128">In hello action search box, type **http** toolist hello HTTP actions.</span></span>
   
    ![Selecione a ação de Olá HTTP](./media/connectors-native-http/using-action-1.png)

4. <span data-ttu-id="9b5b7-130">Adicione os parâmetros necessários para a chamada de Olá HTTP.</span><span class="sxs-lookup"><span data-stu-id="9b5b7-130">Add any required parameters for hello HTTP call.</span></span>
   
    ![Olá concluída a ação de HTTP](./media/connectors-native-http/using-action-2.png)

5. <span data-ttu-id="9b5b7-132">Na barra de ferramentas estruturador de Olá, clique em **guardar**.</span><span class="sxs-lookup"><span data-stu-id="9b5b7-132">On hello designer toolbar, click **Save**.</span></span> <span data-ttu-id="9b5b7-133">A aplicação lógica é guardada e publicada (ativada) em Olá mesmo tempo.</span><span class="sxs-lookup"><span data-stu-id="9b5b7-133">Your logic app is saved and published (activated) at hello same time.</span></span>

## <a name="http-trigger"></a><span data-ttu-id="9b5b7-134">Acionador HTTP</span><span class="sxs-lookup"><span data-stu-id="9b5b7-134">HTTP trigger</span></span>
<span data-ttu-id="9b5b7-135">Seguem-se detalhes Olá para o acionador de Olá que suporte este conector.</span><span class="sxs-lookup"><span data-stu-id="9b5b7-135">Here are hello details for hello trigger that this connector supports.</span></span> <span data-ttu-id="9b5b7-136">conector HTTP Olá tem um acionador.</span><span class="sxs-lookup"><span data-stu-id="9b5b7-136">hello HTTP connector has one trigger.</span></span>

| <span data-ttu-id="9b5b7-137">Acionador</span><span class="sxs-lookup"><span data-stu-id="9b5b7-137">Trigger</span></span> | <span data-ttu-id="9b5b7-138">Descrição</span><span class="sxs-lookup"><span data-stu-id="9b5b7-138">Description</span></span> |
| --- | --- |
| <span data-ttu-id="9b5b7-139">HTTP</span><span class="sxs-lookup"><span data-stu-id="9b5b7-139">HTTP</span></span> |<span data-ttu-id="9b5b7-140">Faz uma chamada HTTP e devolve o conteúdo da resposta Olá.</span><span class="sxs-lookup"><span data-stu-id="9b5b7-140">Makes an HTTP call and returns hello response content.</span></span> |

## <a name="http-action"></a><span data-ttu-id="9b5b7-141">Ação de HTTP</span><span class="sxs-lookup"><span data-stu-id="9b5b7-141">HTTP action</span></span>
<span data-ttu-id="9b5b7-142">Seguem-se detalhes Olá para a ação de Olá que suporte este conector.</span><span class="sxs-lookup"><span data-stu-id="9b5b7-142">Here are hello details for hello action that this connector supports.</span></span> <span data-ttu-id="9b5b7-143">conector HTTP Olá tem uma ação possíveis.</span><span class="sxs-lookup"><span data-stu-id="9b5b7-143">hello HTTP connector has one possible action.</span></span>

| <span data-ttu-id="9b5b7-144">Ação</span><span class="sxs-lookup"><span data-stu-id="9b5b7-144">Action</span></span> | <span data-ttu-id="9b5b7-145">Descrição</span><span class="sxs-lookup"><span data-stu-id="9b5b7-145">Description</span></span> |
| --- | --- |
| <span data-ttu-id="9b5b7-146">HTTP</span><span class="sxs-lookup"><span data-stu-id="9b5b7-146">HTTP</span></span> |<span data-ttu-id="9b5b7-147">Faz uma chamada HTTP e devolve o conteúdo da resposta Olá.</span><span class="sxs-lookup"><span data-stu-id="9b5b7-147">Makes an HTTP call and returns hello response content.</span></span> |

## <a name="http-details"></a><span data-ttu-id="9b5b7-148">Detalhes HTTP</span><span class="sxs-lookup"><span data-stu-id="9b5b7-148">HTTP details</span></span>
<span data-ttu-id="9b5b7-149">Olá tabelas seguintes descrevem Olá necessários e opcionais campos de entrada para a ação de Olá e detalhes saída correspondente Olá associadas através da ação de Olá.</span><span class="sxs-lookup"><span data-stu-id="9b5b7-149">hello following tables describe hello required and optional input fields for hello action and hello corresponding output details that are associated with using hello action.</span></span>

#### <a name="http-request"></a><span data-ttu-id="9b5b7-150">Pedido de HTTP</span><span class="sxs-lookup"><span data-stu-id="9b5b7-150">HTTP request</span></span>
<span data-ttu-id="9b5b7-151">Olá seguem-se os campos de entrada para a ação de Olá, o que faz um pedido de saída de HTTP.</span><span class="sxs-lookup"><span data-stu-id="9b5b7-151">hello following are input fields for hello action, which makes an HTTP outbound request.</span></span>
<span data-ttu-id="9b5b7-152">A * significa que é um campo obrigatório.</span><span class="sxs-lookup"><span data-stu-id="9b5b7-152">A * means that it is a required field.</span></span>

| <span data-ttu-id="9b5b7-153">Nome a apresentar</span><span class="sxs-lookup"><span data-stu-id="9b5b7-153">Display name</span></span> | <span data-ttu-id="9b5b7-154">Nome da propriedade</span><span class="sxs-lookup"><span data-stu-id="9b5b7-154">Property name</span></span> | <span data-ttu-id="9b5b7-155">Descrição</span><span class="sxs-lookup"><span data-stu-id="9b5b7-155">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="9b5b7-156">Método *</span><span class="sxs-lookup"><span data-stu-id="9b5b7-156">Method*</span></span> |<span data-ttu-id="9b5b7-157">Método</span><span class="sxs-lookup"><span data-stu-id="9b5b7-157">method</span></span> |<span data-ttu-id="9b5b7-158">Olá HTTP verbo toouse</span><span class="sxs-lookup"><span data-stu-id="9b5b7-158">hello HTTP verb toouse</span></span> |
| <span data-ttu-id="9b5b7-159">URI *</span><span class="sxs-lookup"><span data-stu-id="9b5b7-159">URI*</span></span> |<span data-ttu-id="9b5b7-160">URI</span><span class="sxs-lookup"><span data-stu-id="9b5b7-160">uri</span></span> |<span data-ttu-id="9b5b7-161">Olá URI de pedido de Olá HTTP</span><span class="sxs-lookup"><span data-stu-id="9b5b7-161">hello URI for hello HTTP request</span></span> |
| <span data-ttu-id="9b5b7-162">Cabeçalhos</span><span class="sxs-lookup"><span data-stu-id="9b5b7-162">Headers</span></span> |<span data-ttu-id="9b5b7-163">Cabeçalhos</span><span class="sxs-lookup"><span data-stu-id="9b5b7-163">headers</span></span> |<span data-ttu-id="9b5b7-164">Um objeto JSON de tooinclude de cabeçalhos HTTP</span><span class="sxs-lookup"><span data-stu-id="9b5b7-164">A JSON object of HTTP headers tooinclude</span></span> |
| <span data-ttu-id="9b5b7-165">Corpo</span><span class="sxs-lookup"><span data-stu-id="9b5b7-165">Body</span></span> |<span data-ttu-id="9b5b7-166">Corpo</span><span class="sxs-lookup"><span data-stu-id="9b5b7-166">body</span></span> |<span data-ttu-id="9b5b7-167">Olá corpo do pedido HTTP</span><span class="sxs-lookup"><span data-stu-id="9b5b7-167">hello HTTP request body</span></span> |
| <span data-ttu-id="9b5b7-168">Autenticação</span><span class="sxs-lookup"><span data-stu-id="9b5b7-168">Authentication</span></span> |<span data-ttu-id="9b5b7-169">Autenticação</span><span class="sxs-lookup"><span data-stu-id="9b5b7-169">authentication</span></span> |<span data-ttu-id="9b5b7-170">Os detalhes na Olá [autenticação](#authentication) secção</span><span class="sxs-lookup"><span data-stu-id="9b5b7-170">Details in hello [Authentication](#authentication) section</span></span> |

<br>

#### <a name="output-details"></a><span data-ttu-id="9b5b7-171">Detalhes de saída</span><span class="sxs-lookup"><span data-stu-id="9b5b7-171">Output details</span></span>
<span data-ttu-id="9b5b7-172">Olá seguem-se detalhes de saída para Olá resposta de HTTP.</span><span class="sxs-lookup"><span data-stu-id="9b5b7-172">hello following are output details for hello HTTP response.</span></span>

| <span data-ttu-id="9b5b7-173">Nome da propriedade</span><span class="sxs-lookup"><span data-stu-id="9b5b7-173">Property name</span></span> | <span data-ttu-id="9b5b7-174">Tipo de dados</span><span class="sxs-lookup"><span data-stu-id="9b5b7-174">Data type</span></span> | <span data-ttu-id="9b5b7-175">Descrição</span><span class="sxs-lookup"><span data-stu-id="9b5b7-175">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="9b5b7-176">Cabeçalhos</span><span class="sxs-lookup"><span data-stu-id="9b5b7-176">Headers</span></span> |<span data-ttu-id="9b5b7-177">objeto</span><span class="sxs-lookup"><span data-stu-id="9b5b7-177">object</span></span> |<span data-ttu-id="9b5b7-178">Cabeçalhos de resposta</span><span class="sxs-lookup"><span data-stu-id="9b5b7-178">Response headers</span></span> |
| <span data-ttu-id="9b5b7-179">Corpo</span><span class="sxs-lookup"><span data-stu-id="9b5b7-179">Body</span></span> |<span data-ttu-id="9b5b7-180">objeto</span><span class="sxs-lookup"><span data-stu-id="9b5b7-180">object</span></span> |<span data-ttu-id="9b5b7-181">Objeto de resposta</span><span class="sxs-lookup"><span data-stu-id="9b5b7-181">Response object</span></span> |
| <span data-ttu-id="9b5b7-182">Código de estado</span><span class="sxs-lookup"><span data-stu-id="9b5b7-182">Status Code</span></span> |<span data-ttu-id="9b5b7-183">Int</span><span class="sxs-lookup"><span data-stu-id="9b5b7-183">int</span></span> |<span data-ttu-id="9b5b7-184">Código de estado HTTP</span><span class="sxs-lookup"><span data-stu-id="9b5b7-184">HTTP status code</span></span> |

## <a name="authentication"></a><span data-ttu-id="9b5b7-185">Autenticação</span><span class="sxs-lookup"><span data-stu-id="9b5b7-185">Authentication</span></span>
<span data-ttu-id="9b5b7-186">funcionalidade de Logic Apps Olá permite-lhe toouse diferentes tipos de autenticação nos pontos finais HTTP.</span><span class="sxs-lookup"><span data-stu-id="9b5b7-186">hello Logic Apps feature allows you toouse different types of authentication against HTTP endpoints.</span></span> <span data-ttu-id="9b5b7-187">Pode utilizar esta autenticação com Olá **HTTP**,  **[HTTP + Swagger](connectors-native-http-swagger.md)**, e  **[HTTP Webhook](connectors-native-webhook.md)**  conectores.</span><span class="sxs-lookup"><span data-stu-id="9b5b7-187">You can use this authentication with hello **HTTP**, **[HTTP + Swagger](connectors-native-http-swagger.md)**, and **[HTTP Webhook](connectors-native-webhook.md)** connectors.</span></span> <span data-ttu-id="9b5b7-188">Olá, os seguintes tipos de autenticação é configurável:</span><span class="sxs-lookup"><span data-stu-id="9b5b7-188">hello following types of authentication are configurable:</span></span>

* [<span data-ttu-id="9b5b7-189">Autenticação básica</span><span class="sxs-lookup"><span data-stu-id="9b5b7-189">Basic authentication</span></span>](#basic-authentication)
* [<span data-ttu-id="9b5b7-190">Autenticação de certificado de cliente</span><span class="sxs-lookup"><span data-stu-id="9b5b7-190">Client certificate authentication</span></span>](#client-certificate-authentication)
* [<span data-ttu-id="9b5b7-191">Autenticação do Azure Active Directory (Azure AD) OAuth</span><span class="sxs-lookup"><span data-stu-id="9b5b7-191">Azure Active Directory (Azure AD) OAuth authentication</span></span>](#azure-active-directory-oauth-authentication)

#### <a name="basic-authentication"></a><span data-ttu-id="9b5b7-192">Autenticação básica</span><span class="sxs-lookup"><span data-stu-id="9b5b7-192">Basic authentication</span></span>

<span data-ttu-id="9b5b7-193">Olá seguinte objeto de autenticação é necessária para a autenticação básica.</span><span class="sxs-lookup"><span data-stu-id="9b5b7-193">hello following authentication object is needed for basic authentication.</span></span>
<span data-ttu-id="9b5b7-194">A * significa que é um campo obrigatório.</span><span class="sxs-lookup"><span data-stu-id="9b5b7-194">A * means that it is a required field.</span></span>

| <span data-ttu-id="9b5b7-195">Nome da propriedade</span><span class="sxs-lookup"><span data-stu-id="9b5b7-195">Property name</span></span> | <span data-ttu-id="9b5b7-196">Tipo de dados</span><span class="sxs-lookup"><span data-stu-id="9b5b7-196">Data type</span></span> | <span data-ttu-id="9b5b7-197">Descrição</span><span class="sxs-lookup"><span data-stu-id="9b5b7-197">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="9b5b7-198">Tipo *</span><span class="sxs-lookup"><span data-stu-id="9b5b7-198">Type*</span></span> |<span data-ttu-id="9b5b7-199">tipo</span><span class="sxs-lookup"><span data-stu-id="9b5b7-199">type</span></span> |<span data-ttu-id="9b5b7-200">Tipo de autenticação (tem de ser `Basic` para a autenticação básica)</span><span class="sxs-lookup"><span data-stu-id="9b5b7-200">Type of authentication (must be `Basic` for basic authentication)</span></span> |
| <span data-ttu-id="9b5b7-201">Nome de utilizador *</span><span class="sxs-lookup"><span data-stu-id="9b5b7-201">Username*</span></span> |<span data-ttu-id="9b5b7-202">o nome de utilizador</span><span class="sxs-lookup"><span data-stu-id="9b5b7-202">username</span></span> |<span data-ttu-id="9b5b7-203">Tooauthenticate de nome de utilizador</span><span class="sxs-lookup"><span data-stu-id="9b5b7-203">User name tooauthenticate</span></span> |
| <span data-ttu-id="9b5b7-204">Palavra-passe *</span><span class="sxs-lookup"><span data-stu-id="9b5b7-204">Password*</span></span> |<span data-ttu-id="9b5b7-205">palavra-passe</span><span class="sxs-lookup"><span data-stu-id="9b5b7-205">password</span></span> |<span data-ttu-id="9b5b7-206">Palavra-passe tooauthenticate</span><span class="sxs-lookup"><span data-stu-id="9b5b7-206">Password tooauthenticate</span></span> |

> [!TIP]
> <span data-ttu-id="9b5b7-207">Se pretender toouse uma palavra-passe não pode ser obtida a partir da definição de Olá, utilize um `securestring` parâmetro e Olá `@parameters()`  
>  [função da definição de fluxo de trabalho](http://aka.ms/logicappdocs).</span><span class="sxs-lookup"><span data-stu-id="9b5b7-207">If you want toouse a password that cannot be retrieved from hello definition, use a `securestring` parameter and hello `@parameters()` 
> [workflow definition function](http://aka.ms/logicappdocs).</span></span>

<span data-ttu-id="9b5b7-208">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="9b5b7-208">For example:</span></span>

```javascript
{
    "type": "Basic",
    "username": "user",
    "password": "test"
}
```

#### <a name="client-certificate-authentication"></a><span data-ttu-id="9b5b7-209">Autenticação de certificados de cliente</span><span class="sxs-lookup"><span data-stu-id="9b5b7-209">Client certificate authentication</span></span>

<span data-ttu-id="9b5b7-210">Olá seguinte objeto de autenticação é necessário para autenticação de certificados de cliente.</span><span class="sxs-lookup"><span data-stu-id="9b5b7-210">hello following authentication object is needed for client certificate authentication.</span></span> <span data-ttu-id="9b5b7-211">A * significa que é um campo obrigatório.</span><span class="sxs-lookup"><span data-stu-id="9b5b7-211">A * means that it is a required field.</span></span>

| <span data-ttu-id="9b5b7-212">Nome da propriedade</span><span class="sxs-lookup"><span data-stu-id="9b5b7-212">Property name</span></span> | <span data-ttu-id="9b5b7-213">Tipo de dados</span><span class="sxs-lookup"><span data-stu-id="9b5b7-213">Data type</span></span> | <span data-ttu-id="9b5b7-214">Descrição</span><span class="sxs-lookup"><span data-stu-id="9b5b7-214">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="9b5b7-215">Tipo *</span><span class="sxs-lookup"><span data-stu-id="9b5b7-215">Type*</span></span> |<span data-ttu-id="9b5b7-216">tipo</span><span class="sxs-lookup"><span data-stu-id="9b5b7-216">type</span></span> |<span data-ttu-id="9b5b7-217">Olá, tipo de autenticação (tem de ser `ClientCertificate` para certificados de cliente SSL)</span><span class="sxs-lookup"><span data-stu-id="9b5b7-217">hello type of authentication (must be `ClientCertificate` for SSL client certificates)</span></span> |
| <span data-ttu-id="9b5b7-218">PFX *</span><span class="sxs-lookup"><span data-stu-id="9b5b7-218">PFX*</span></span> |<span data-ttu-id="9b5b7-219">PFX</span><span class="sxs-lookup"><span data-stu-id="9b5b7-219">pfx</span></span> |<span data-ttu-id="9b5b7-220">Olá com codificação Base64 conteúdo Olá Personal Information (Exchange PFX) ficheiro</span><span class="sxs-lookup"><span data-stu-id="9b5b7-220">hello Base64-encoded contents of hello Personal Information Exchange (PFX) file</span></span> |
| <span data-ttu-id="9b5b7-221">Palavra-passe *</span><span class="sxs-lookup"><span data-stu-id="9b5b7-221">Password*</span></span> |<span data-ttu-id="9b5b7-222">palavra-passe</span><span class="sxs-lookup"><span data-stu-id="9b5b7-222">password</span></span> |<span data-ttu-id="9b5b7-223">Olá palavra-passe tooaccess Olá ficheiro PFX</span><span class="sxs-lookup"><span data-stu-id="9b5b7-223">hello password tooaccess hello PFX file</span></span> |

> [!TIP]
> <span data-ttu-id="9b5b7-224">um parâmetro que não seja legível na definição de Olá depois de guardar a aplicação de lógica de Olá toouse, pode utilizar um `securestring` parâmetro e Olá `@parameters()`  
>  [função da definição de fluxo de trabalho](http://aka.ms/logicappdocs).</span><span class="sxs-lookup"><span data-stu-id="9b5b7-224">toouse a parameter that won't be readable in hello definition after saving hello logic app, you can use a `securestring` parameter and hello `@parameters()` 
> [workflow definition function](http://aka.ms/logicappdocs).</span></span>

<span data-ttu-id="9b5b7-225">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="9b5b7-225">For example:</span></span>

```javascript
{
    "type": "ClientCertificate",
    "pfx": "aGVsbG8g...d29ybGQ=",
    "password": "@parameters('myPassword')"
}
```

#### <a name="azure-ad-oauth-authentication"></a><span data-ttu-id="9b5b7-226">Autenticação do Azure AD OAuth</span><span class="sxs-lookup"><span data-stu-id="9b5b7-226">Azure AD OAuth authentication</span></span>
<span data-ttu-id="9b5b7-227">Olá seguinte objeto de autenticação é necessário para autenticação do Azure AD OAuth.</span><span class="sxs-lookup"><span data-stu-id="9b5b7-227">hello following authentication object is needed for Azure AD OAuth authentication.</span></span> <span data-ttu-id="9b5b7-228">A * significa que é um campo obrigatório.</span><span class="sxs-lookup"><span data-stu-id="9b5b7-228">A * means that it is a required field.</span></span>

| <span data-ttu-id="9b5b7-229">Nome da propriedade</span><span class="sxs-lookup"><span data-stu-id="9b5b7-229">Property name</span></span> | <span data-ttu-id="9b5b7-230">Tipo de dados</span><span class="sxs-lookup"><span data-stu-id="9b5b7-230">Data type</span></span> | <span data-ttu-id="9b5b7-231">Descrição</span><span class="sxs-lookup"><span data-stu-id="9b5b7-231">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="9b5b7-232">Tipo *</span><span class="sxs-lookup"><span data-stu-id="9b5b7-232">Type*</span></span> |<span data-ttu-id="9b5b7-233">tipo</span><span class="sxs-lookup"><span data-stu-id="9b5b7-233">type</span></span> |<span data-ttu-id="9b5b7-234">Olá, tipo de autenticação (tem de ser `ActiveDirectoryOAuth` para o Azure AD OAuth)</span><span class="sxs-lookup"><span data-stu-id="9b5b7-234">hello type of authentication (must be `ActiveDirectoryOAuth` for Azure AD OAuth)</span></span> |
| <span data-ttu-id="9b5b7-235">Inquilino *</span><span class="sxs-lookup"><span data-stu-id="9b5b7-235">Tenant*</span></span> |<span data-ttu-id="9b5b7-236">Inquilino</span><span class="sxs-lookup"><span data-stu-id="9b5b7-236">tenant</span></span> |<span data-ttu-id="9b5b7-237">Olá identificador de inquilino para o inquilino Olá do Azure AD</span><span class="sxs-lookup"><span data-stu-id="9b5b7-237">hello tenant identifier for hello Azure AD tenant</span></span> |
| <span data-ttu-id="9b5b7-238">Público-alvo *</span><span class="sxs-lookup"><span data-stu-id="9b5b7-238">Audience*</span></span> |<span data-ttu-id="9b5b7-239">público-alvo</span><span class="sxs-lookup"><span data-stu-id="9b5b7-239">audience</span></span> |<span data-ttu-id="9b5b7-240">recurso de Olá que está a pedir toouse de autorização.</span><span class="sxs-lookup"><span data-stu-id="9b5b7-240">hello resource you are requesting authorization toouse.</span></span> <span data-ttu-id="9b5b7-241">Por exemplo: `https://management.core.windows.net/`</span><span class="sxs-lookup"><span data-stu-id="9b5b7-241">For example: `https://management.core.windows.net/`</span></span> |
| <span data-ttu-id="9b5b7-242">Cliente ID *</span><span class="sxs-lookup"><span data-stu-id="9b5b7-242">Client ID*</span></span> |<span data-ttu-id="9b5b7-243">ID de cliente</span><span class="sxs-lookup"><span data-stu-id="9b5b7-243">clientId</span></span> |<span data-ttu-id="9b5b7-244">Olá identificador de cliente para a aplicação Olá do Azure AD</span><span class="sxs-lookup"><span data-stu-id="9b5b7-244">hello client identifier for hello Azure AD application</span></span> |
| <span data-ttu-id="9b5b7-245">Segredo *</span><span class="sxs-lookup"><span data-stu-id="9b5b7-245">Secret*</span></span> |<span data-ttu-id="9b5b7-246">segredo</span><span class="sxs-lookup"><span data-stu-id="9b5b7-246">secret</span></span> |<span data-ttu-id="9b5b7-247">segredo Olá hello do cliente de que está a solicitar o token de Olá</span><span class="sxs-lookup"><span data-stu-id="9b5b7-247">hello secret of hello client that is requesting hello token</span></span> |

> [!TIP]
> <span data-ttu-id="9b5b7-248">Pode utilizar um `securestring` parâmetro e Olá `@parameters()` [função da definição de fluxo de trabalho](http://aka.ms/logicappdocs) toouse um parâmetro que não seja legível na definição de Olá depois de guardar.</span><span class="sxs-lookup"><span data-stu-id="9b5b7-248">You can use a `securestring` parameter and hello `@parameters()` [workflow definition function](http://aka.ms/logicappdocs) toouse a parameter that won't be readable in hello definition after saving.</span></span>
> 
> 

<span data-ttu-id="9b5b7-249">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="9b5b7-249">For example:</span></span>

```javascript
{
    "type": "ActiveDirectoryOAuth",
    "tenant": "72f988bf-86f1-41af-91ab-2d7cd011db47",
    "audience": "https://management.core.windows.net/",
    "clientId": "34750e0b-72d1-4e4f-bbbe-664f6d04d411",
    "secret": "hcqgkYc9ebgNLA5c+GDg7xl9ZJMD88TmTJiJBgZ8dFo="
}
```

## <a name="next-steps"></a><span data-ttu-id="9b5b7-250">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="9b5b7-250">Next steps</span></span>
<span data-ttu-id="9b5b7-251">Agora, experimente a plataforma de Olá e [criar uma aplicação lógica](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="9b5b7-251">Now, try out hello platform and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="9b5b7-252">Pode explorar Olá outros conectores disponíveis em Logic Apps observando nosso [lista APIs](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="9b5b7-252">You can explore hello other available connectors in Logic Apps by looking at our [APIs list](apis-list.md).</span></span>

