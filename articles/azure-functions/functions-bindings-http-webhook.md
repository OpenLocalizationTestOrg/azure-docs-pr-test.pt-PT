---
title: "enlaces de funções de HTTP e webhook aaaAzure | Microsoft Docs"
description: "Compreender a forma como toouse HTTP e webhook aciona e os enlaces de funções do Azure."
services: functions
documentationcenter: na
author: mattchenderson
manager: erikre
editor: 
tags: 
keywords: "das funções do Azure, funções, eventos de processamento, webhooks, dinâmicos de computação, arquitetura sem servidor, HTTP, API, REST"
ms.assetid: 2b12200d-63d8-4ec1-9da8-39831d5a51b1
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 11/18/2016
ms.author: mahender
ms.openlocfilehash: c23b7a1443d492ed78c595e97d1d778a7ab12416
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-http-and-webhook-bindings"></a><span data-ttu-id="9c365-104">Enlaces de funções de HTTP e webhook do Azure</span><span class="sxs-lookup"><span data-stu-id="9c365-104">Azure Functions HTTP and webhook bindings</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="9c365-105">Este artigo explica como aciona tooconfigure e trabalhar com HTTP e os enlaces de funções do Azure.</span><span class="sxs-lookup"><span data-stu-id="9c365-105">This article explains how tooconfigure and work with HTTP triggers and bindings in Azure Functions.</span></span>
<span data-ttu-id="9c365-106">Com estas, pode utilizar as funções do Azure toobuild sem servidor APIs e respondeu toowebhooks.</span><span class="sxs-lookup"><span data-stu-id="9c365-106">With these, you can use Azure Functions toobuild serverless APIs and respond toowebhooks.</span></span>

<span data-ttu-id="9c365-107">As funções do Azure fornece Olá enlaces a seguir:</span><span class="sxs-lookup"><span data-stu-id="9c365-107">Azure Functions provides hello following bindings:</span></span>
- <span data-ttu-id="9c365-108">Um [acionador HTTP](#httptrigger) permite invocar uma função com um pedido de HTTP.</span><span class="sxs-lookup"><span data-stu-id="9c365-108">An [HTTP trigger](#httptrigger) lets you invoke a function with an HTTP request.</span></span> <span data-ttu-id="9c365-109">Isto pode ser personalizado toorespond[webhooks](#hooktrigger).</span><span class="sxs-lookup"><span data-stu-id="9c365-109">This can be customized toorespond too[webhooks](#hooktrigger).</span></span>
- <span data-ttu-id="9c365-110">Um [vínculo de saída HTTP](#output) permite-lhe toorespond toohello pedido.</span><span class="sxs-lookup"><span data-stu-id="9c365-110">An [HTTP output binding](#output) allows you toorespond toohello request.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

[!INCLUDE [HTTP client best practices](../../includes/functions-http-client-best-practices.md)]

<a name="httptrigger"></a>

## <a name="http-trigger"></a><span data-ttu-id="9c365-111">Acionador HTTP</span><span class="sxs-lookup"><span data-stu-id="9c365-111">HTTP trigger</span></span>
<span data-ttu-id="9c365-112">acionador HTTP Olá executará a função no pedido HTTP de tooan de resposta.</span><span class="sxs-lookup"><span data-stu-id="9c365-112">hello HTTP trigger will execute your function in response tooan HTTP request.</span></span> <span data-ttu-id="9c365-113">Pode personalizar toorespond tooa determinado URL ou um conjunto de métodos de HTTP.</span><span class="sxs-lookup"><span data-stu-id="9c365-113">You can customize it toorespond tooa particular URL or set of HTTP methods.</span></span> <span data-ttu-id="9c365-114">Um acionador HTTP, também pode ser configurado toorespond toowebhooks.</span><span class="sxs-lookup"><span data-stu-id="9c365-114">An HTTP trigger can also be configured toorespond toowebhooks.</span></span> 

<span data-ttu-id="9c365-115">Se utilizar o portal de funções de Olá, pode também começar a utilizar imediato utilizando um modelo de pré-efetuado.</span><span class="sxs-lookup"><span data-stu-id="9c365-115">If using hello Functions portal, you can also get started right away using a pre-made template.</span></span> <span data-ttu-id="9c365-116">Selecione **nova função** e escolher "API e Webhooks" Olá **cenário** pendente.</span><span class="sxs-lookup"><span data-stu-id="9c365-116">Select **New function** and choose "API & Webhooks" from hello **Scenario** dropdown.</span></span> <span data-ttu-id="9c365-117">Selecione um dos modelos de Olá e clique em **criar**.</span><span class="sxs-lookup"><span data-stu-id="9c365-117">Select one of hello templates and click **Create**.</span></span>

<span data-ttu-id="9c365-118">Por predefinição, um acionador HTTP responderá toohello pedido com um código de estado HTTP 200 OK e um corpo vazio.</span><span class="sxs-lookup"><span data-stu-id="9c365-118">By default, an HTTP trigger will respond toohello request with an HTTP 200 OK status code and an empty body.</span></span> <span data-ttu-id="9c365-119">toomodify Olá resposta, configure um [enlace HTTP de saída](#output)</span><span class="sxs-lookup"><span data-stu-id="9c365-119">toomodify hello response, configure an [HTTP output binding](#output)</span></span>

### <a name="configuring-an-http-trigger"></a><span data-ttu-id="9c365-120">Configurar um acionador HTTP</span><span class="sxs-lookup"><span data-stu-id="9c365-120">Configuring an HTTP trigger</span></span>
<span data-ttu-id="9c365-121">Um acionador HTTP está definido, incluindo um toohello semelhante de objeto JSON a seguir no Olá `bindings` matriz de function.json:</span><span class="sxs-lookup"><span data-stu-id="9c365-121">An HTTP trigger is defined by including a JSON object similar toohello following in hello `bindings` array of function.json:</span></span>

```json
{
    "name": "req",
    "type": "httpTrigger",
    "direction": "in",
    "authLevel": "function",
    "methods": [ "get" ],
    "route": "values/{id}"
},
```
<span data-ttu-id="9c365-122">enlace de Olá suporta Olá seguintes propriedades:</span><span class="sxs-lookup"><span data-stu-id="9c365-122">hello binding supports hello following properties:</span></span>

* <span data-ttu-id="9c365-123">**nome** : necessária - o nome da variável Olá utilizado no código de função para o pedido de Olá ou corpo do pedido.</span><span class="sxs-lookup"><span data-stu-id="9c365-123">**name** : Required - hello variable name used in function code for hello request or request body.</span></span> <span data-ttu-id="9c365-124">Consulte [trabalhar com um acionador HTTP a partir do código](#httptriggerusage).</span><span class="sxs-lookup"><span data-stu-id="9c365-124">See [Working with an HTTP trigger from code](#httptriggerusage).</span></span>
* <span data-ttu-id="9c365-125">**tipo** : obrigatória - tem de ser definido demasiado "httpTrigger".</span><span class="sxs-lookup"><span data-stu-id="9c365-125">**type** : Required - must be set too"httpTrigger".</span></span>
* <span data-ttu-id="9c365-126">**direção** : obrigatória - tem de ser definido demasiado "em".</span><span class="sxs-lookup"><span data-stu-id="9c365-126">**direction** : Required - must be set too"in".</span></span>
* <span data-ttu-id="9c365-127">_authLevel_ : Isto determina as chaves, se existirem, precisam de toobe presente no pedido de Olá na função de Olá tooinvoke de ordem.</span><span class="sxs-lookup"><span data-stu-id="9c365-127">_authLevel_ : This determines what keys, if any, need toobe present on hello request in order tooinvoke hello function.</span></span> <span data-ttu-id="9c365-128">Consulte [trabalhar com as chaves](#keys) abaixo.</span><span class="sxs-lookup"><span data-stu-id="9c365-128">See [Working with keys](#keys) below.</span></span> <span data-ttu-id="9c365-129">valor de Olá pode ser um dos seguintes Olá:</span><span class="sxs-lookup"><span data-stu-id="9c365-129">hello value can be one of hello following:</span></span>
    * <span data-ttu-id="9c365-130">_anónimo_: a chave de API não é necessária.</span><span class="sxs-lookup"><span data-stu-id="9c365-130">_anonymous_: No API key is required.</span></span>
    * <span data-ttu-id="9c365-131">_função_: é necessária uma chave de API específicas.</span><span class="sxs-lookup"><span data-stu-id="9c365-131">_function_: A function-specific API key is required.</span></span> <span data-ttu-id="9c365-132">Este é o valor predefinido de Olá se não for fornecido nenhum.</span><span class="sxs-lookup"><span data-stu-id="9c365-132">This is hello default value if none is provided.</span></span>
    * <span data-ttu-id="9c365-133">_administração_ : Olá mestre chave é necessária.</span><span class="sxs-lookup"><span data-stu-id="9c365-133">_admin_ : hello master key is required.</span></span>
* <span data-ttu-id="9c365-134">**métodos** : Esta é uma matriz dos métodos de Olá HTTP a função de Olá toowhich responderá.</span><span class="sxs-lookup"><span data-stu-id="9c365-134">**methods** : This is an array of hello HTTP methods toowhich hello function will respond.</span></span> <span data-ttu-id="9c365-135">Se não for especificado, a função de Olá responderá métodos tooall HTTP.</span><span class="sxs-lookup"><span data-stu-id="9c365-135">If not specified, hello function will respond tooall HTTP methods.</span></span> <span data-ttu-id="9c365-136">Consulte [personalizar o ponto final de Olá HTTP](#url).</span><span class="sxs-lookup"><span data-stu-id="9c365-136">See [Customizing hello HTTP endpoint](#url).</span></span>
* <span data-ttu-id="9c365-137">**rota** : Isto define o modelo de rota Olá, controlar toowhich URLs responderá a função do pedido.</span><span class="sxs-lookup"><span data-stu-id="9c365-137">**route** : This defines hello route template, controlling toowhich request URLs your function will respond.</span></span> <span data-ttu-id="9c365-138">Olá valor predefinido se não for fornecido nenhum é `<functionname>`.</span><span class="sxs-lookup"><span data-stu-id="9c365-138">hello default value if none is provided is `<functionname>`.</span></span> <span data-ttu-id="9c365-139">Consulte [personalizar o ponto final de Olá HTTP](#url).</span><span class="sxs-lookup"><span data-stu-id="9c365-139">See [Customizing hello HTTP endpoint](#url).</span></span>
* <span data-ttu-id="9c365-140">**webHookType** : Esta ação configura Olá HTTP acionador tooact como reciever um webhook de fornecedor especificado Olá.</span><span class="sxs-lookup"><span data-stu-id="9c365-140">**webHookType** : This configures hello HTTP trigger tooact as a webhook reciever for hello specified provider.</span></span> <span data-ttu-id="9c365-141">Olá _métodos_ propriedade não deve ser definida se isto for escolhido.</span><span class="sxs-lookup"><span data-stu-id="9c365-141">hello _methods_ property should not be set if this is chosen.</span></span> <span data-ttu-id="9c365-142">Consulte [responder toowebhooks](#hooktrigger).</span><span class="sxs-lookup"><span data-stu-id="9c365-142">See [Responding toowebhooks](#hooktrigger).</span></span> <span data-ttu-id="9c365-143">valor de Olá pode ser um dos seguintes Olá:</span><span class="sxs-lookup"><span data-stu-id="9c365-143">hello value can be one of hello following:</span></span>
    * <span data-ttu-id="9c365-144">_genericJson_ : um ponto final de webhook fins gerais sem lógica para um fornecedor específico.</span><span class="sxs-lookup"><span data-stu-id="9c365-144">_genericJson_ : A general purpose webhook endpoint without logic for a specific provider.</span></span>
    * <span data-ttu-id="9c365-145">_github_ : função Olá responderá tooGitHub webhooks.</span><span class="sxs-lookup"><span data-stu-id="9c365-145">_github_ : hello function will respond tooGitHub webhooks.</span></span> <span data-ttu-id="9c365-146">Olá _authLevel_ propriedade não deve ser definida se isto for escolhido.</span><span class="sxs-lookup"><span data-stu-id="9c365-146">hello _authLevel_ property should not be set if this is chosen.</span></span>
    * <span data-ttu-id="9c365-147">_slack_ : função Olá responderá tooSlack webhooks.</span><span class="sxs-lookup"><span data-stu-id="9c365-147">_slack_ : hello function will respond tooSlack webhooks.</span></span> <span data-ttu-id="9c365-148">Olá _authLevel_ propriedade não deve ser definida se isto for escolhido.</span><span class="sxs-lookup"><span data-stu-id="9c365-148">hello _authLevel_ property should not be set if this is chosen.</span></span>

<a name="httptriggerusage"></a>
### <a name="working-with-an-http-trigger-from-code"></a><span data-ttu-id="9c365-149">Trabalhar com um acionador HTTP a partir do código</span><span class="sxs-lookup"><span data-stu-id="9c365-149">Working with an HTTP trigger from code</span></span>
<span data-ttu-id="9c365-150">Para as funções de c# e F #, podem declarar tipo Olá do seu toobe de entrada de Acionador ou `HttpRequestMessage` ou um tipo personalizado.</span><span class="sxs-lookup"><span data-stu-id="9c365-150">For C# and F# functions, you can declare hello type of your trigger input toobe either `HttpRequestMessage` or a custom type.</span></span> <span data-ttu-id="9c365-151">Se optar por `HttpRequestMessage`, em seguida, irá obter o objeto de pedido de toohello acesso total.</span><span class="sxs-lookup"><span data-stu-id="9c365-151">If you choose `HttpRequestMessage`, then you will get full access toohello request object.</span></span> <span data-ttu-id="9c365-152">Para um tipo personalizado (por exemplo, um POCO), funções tentará corpo do pedido tooparse Olá como as propriedades do objeto JSON toopopulate Olá.</span><span class="sxs-lookup"><span data-stu-id="9c365-152">For a custom type (such as a POCO), Functions will attempt tooparse hello request body as JSON toopopulate hello object properties.</span></span>

<span data-ttu-id="9c365-153">Para funções de Node.js, tempo de execução do Olá funções fornece o corpo do pedido Olá em vez de objecto de pedido de Olá.</span><span class="sxs-lookup"><span data-stu-id="9c365-153">For Node.js functions, hello Functions runtime provides hello request body instead of hello request object.</span></span>

<span data-ttu-id="9c365-154">Consulte [amostras de Acionador HTTP](#httptriggersample) utilizações por exemplo.</span><span class="sxs-lookup"><span data-stu-id="9c365-154">See [HTTP trigger samples](#httptriggersample) for example usages.</span></span>


<a name="output"></a>
## <a name="http-response-output-binding"></a><span data-ttu-id="9c365-155">Enlace de saída de resposta de HTTP</span><span class="sxs-lookup"><span data-stu-id="9c365-155">HTTP response output binding</span></span>
<span data-ttu-id="9c365-156">Utilize Olá HTTP saída enlace toorespond toohello HTTP pedido remetente.</span><span class="sxs-lookup"><span data-stu-id="9c365-156">Use hello HTTP output binding toorespond toohello HTTP request sender.</span></span> <span data-ttu-id="9c365-157">Este enlace necessita de um acionador HTTP e permite-lhe resposta de Olá toocustomize associada pedido trigger Olá.</span><span class="sxs-lookup"><span data-stu-id="9c365-157">This binding requires an HTTP trigger and allows you toocustomize hello response associated with hello trigger's request.</span></span> <span data-ttu-id="9c365-158">Se o enlace de saída de um HTTP não for fornecido, um acionador HTTP irá devolver HTTP 200 OK com uma mensagem vazia.</span><span class="sxs-lookup"><span data-stu-id="9c365-158">If an HTTP output binding is not provided, an HTTP trigger will return HTTP 200 OK with an empty body.</span></span> 

### <a name="configuring-an-http-output-binding"></a><span data-ttu-id="9c365-159">Configurar um HTTP de saída do enlace</span><span class="sxs-lookup"><span data-stu-id="9c365-159">Configuring an HTTP output binding</span></span>
<span data-ttu-id="9c365-160">Olá HTTP de saída do enlace está definido, incluindo um toohello semelhante de objeto JSON a seguir no Olá `bindings` matriz de function.json:</span><span class="sxs-lookup"><span data-stu-id="9c365-160">hello HTTP output binding is defined by including a JSON object similar toohello following in hello `bindings` array of function.json:</span></span>

```json
{
    "name": "res",
    "type": "http",
    "direction": "out"
}
```
<span data-ttu-id="9c365-161">o enlace de Olá contém Olá seguintes propriedades:</span><span class="sxs-lookup"><span data-stu-id="9c365-161">hello binding contains hello following properties:</span></span>

* <span data-ttu-id="9c365-162">**nome** : obrigatória - Olá utilizado no código de função para resposta Olá o nome da variável.</span><span class="sxs-lookup"><span data-stu-id="9c365-162">**name** : Required - hello variable name used in function code for hello response.</span></span> <span data-ttu-id="9c365-163">Consulte [enlace a partir do código de saída de trabalhar com um HTTP](#outputusage).</span><span class="sxs-lookup"><span data-stu-id="9c365-163">See [Working with an HTTP output binding from code](#outputusage).</span></span>
* <span data-ttu-id="9c365-164">**tipo** : obrigatória - tem de ser definido demasiado "http".</span><span class="sxs-lookup"><span data-stu-id="9c365-164">**type** : Required - must be set too"http".</span></span>
* <span data-ttu-id="9c365-165">**direção** : obrigatória - tem de ser definido demasiado "out".</span><span class="sxs-lookup"><span data-stu-id="9c365-165">**direction** : Required - must be set too"out".</span></span>

<a name="outputusage"></a>
### <a name="working-with-an-http-output-binding-from-code"></a><span data-ttu-id="9c365-166">Trabalhar com um HTTP enlace a partir do código de saída</span><span class="sxs-lookup"><span data-stu-id="9c365-166">Working with an HTTP output binding from code</span></span>
<span data-ttu-id="9c365-167">Pode utilizar Olá saída parâmetro (por exemplo, "res") toorespond toohello http ou webhook autor da chamada.</span><span class="sxs-lookup"><span data-stu-id="9c365-167">You can use hello output parameter (e.g., "res") toorespond toohello http or webhook caller.</span></span> <span data-ttu-id="9c365-168">Em alternativa, pode utilizar o padrão `Request.CreateResponse()` (c#) ou `context.res` (Node.JS) padrão tooreturn sua resposta.</span><span class="sxs-lookup"><span data-stu-id="9c365-168">Alternatively, you can use the standard `Request.CreateResponse()` (C#) or `context.res` (Node.JS) pattern tooreturn your response.</span></span> <span data-ttu-id="9c365-169">Para obter exemplos sobre como toouse Olá método última, consulte [amostras de Acionador HTTP](#httptriggersample) e [amostras de Acionador de Webhook](#hooktriggersample).</span><span class="sxs-lookup"><span data-stu-id="9c365-169">For examples on how toouse hello latter method, see [HTTP trigger samples](#httptriggersample) and [Webhook trigger samples](#hooktriggersample).</span></span>


<a name="hooktrigger"></a>
## <a name="responding-toowebhooks"></a><span data-ttu-id="9c365-170">Responder toowebhooks</span><span class="sxs-lookup"><span data-stu-id="9c365-170">Responding toowebhooks</span></span>
<span data-ttu-id="9c365-171">Um acionador HTTP com Olá _webHookType_ propriedade será configurado toorespond demasiado[webhooks](https://en.wikipedia.org/wiki/Webhook).</span><span class="sxs-lookup"><span data-stu-id="9c365-171">An HTTP trigger with hello _webHookType_ property will be configured toorespond too[webhooks](https://en.wikipedia.org/wiki/Webhook).</span></span> <span data-ttu-id="9c365-172">configuração básica Olá utiliza a definição de "genericJson" Olá.</span><span class="sxs-lookup"><span data-stu-id="9c365-172">hello basic configuration uses hello "genericJson" setting.</span></span> <span data-ttu-id="9c365-173">Restringe esta pedidos tooonly as utilizando o HTTP POST e com Olá `application/json` tipo de conteúdo.</span><span class="sxs-lookup"><span data-stu-id="9c365-173">This restricts requests tooonly those using HTTP POST and with hello `application/json` content type.</span></span>

<span data-ttu-id="9c365-174">Olá acionador pode ser tooa personalizáveis fornecedor de webhook específico (por exemplo, [GitHub](https://developer.github.com/webhooks/) e [Slack](https://api.slack.com/outgoing-webhooks)).</span><span class="sxs-lookup"><span data-stu-id="9c365-174">hello trigger can additionally be tailored tooa specific webhook provider (e.g., [GitHub](https://developer.github.com/webhooks/) and [Slack](https://api.slack.com/outgoing-webhooks)).</span></span> <span data-ttu-id="9c365-175">Se não for especificado um fornecedor, o tempo de execução do Olá funções pode asseguramos lógica de validação do fornecedor de Olá por si.</span><span class="sxs-lookup"><span data-stu-id="9c365-175">If a provider is specified, hello Functions runtime can take care of hello provider's validation logic for you.</span></span>  

### <a name="configuring-github-as-a-webhook-provider"></a><span data-ttu-id="9c365-176">Configuração de GitHub como um fornecedor de webhook</span><span class="sxs-lookup"><span data-stu-id="9c365-176">Configuring GitHub as a webhook provider</span></span>
<span data-ttu-id="9c365-177">toorespond tooGitHub webhooks, primeiro criar a sua função com um acionador de HTTP e defina Olá _webHookType_ propriedade demasiado "github".</span><span class="sxs-lookup"><span data-stu-id="9c365-177">toorespond tooGitHub webhooks, first create your function with an HTTP Trigger, and set hello _webHookType_ property too"github".</span></span> <span data-ttu-id="9c365-178">Em seguida, copie o [URL](#url) e [chave de API](#keys) no seu repositório GitHub **adicionar webhook** página.</span><span class="sxs-lookup"><span data-stu-id="9c365-178">Then copy its [URL](#url) and [API key](#keys) into your GitHub repository's **Add webhook** page.</span></span> <span data-ttu-id="9c365-179">Consulte o artigo do GitHub [criar Webhooks](http://go.microsoft.com/fwlink/?LinkID=761099&clcid=0x409) documentação para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="9c365-179">See GitHub's [Creating Webhooks](http://go.microsoft.com/fwlink/?LinkID=761099&clcid=0x409) documentation for more.</span></span>

![](./media/functions-bindings-http-webhook/github-add-webhook.png)

### <a name="configuring-slack-as-a-webhook-provider"></a><span data-ttu-id="9c365-180">Configurar Slack como um fornecedor de webhook</span><span class="sxs-lookup"><span data-stu-id="9c365-180">Configuring Slack as a webhook provider</span></span>
<span data-ttu-id="9c365-181">webhook Slack Olá gera um token para si em vez de permitindo-lhe especificar, pelo que tem de configurar uma chave de específicas com token Olá de Slack.</span><span class="sxs-lookup"><span data-stu-id="9c365-181">hello Slack webhook generates a token for you instead of letting you specify it, so you must configure a function-specific key with hello token from Slack.</span></span> <span data-ttu-id="9c365-182">Consulte [trabalhar com as chaves](#keys).</span><span class="sxs-lookup"><span data-stu-id="9c365-182">See [Working with keys](#keys).</span></span>

<a name="url"></a>
## <a name="customizing-hello-http-endpoint"></a><span data-ttu-id="9c365-183">Personalizar o ponto final de HTTP Olá</span><span class="sxs-lookup"><span data-stu-id="9c365-183">Customizing hello HTTP endpoint</span></span>
<span data-ttu-id="9c365-184">Por predefinição quando cria uma função de um acionador HTTP ou o WebHook, função Olá é endereçável com uma rota de formulário Olá:</span><span class="sxs-lookup"><span data-stu-id="9c365-184">By default when you create a function for an HTTP trigger, or WebHook, hello function is addressable with a route of hello form:</span></span>

    http://<yourapp>.azurewebsites.net/api/<funcname> 

<span data-ttu-id="9c365-185">Pode personalizar esta rota utilizando Olá opcional `route` propriedade no acionador Olá HTTP de entrada de enlace.</span><span class="sxs-lookup"><span data-stu-id="9c365-185">You can customize this route using hello optional `route` property on hello HTTP trigger's input binding.</span></span> <span data-ttu-id="9c365-186">Por exemplo, Olá seguir *function.json* ficheiro define um `route` propriedade para um acionador HTTP:</span><span class="sxs-lookup"><span data-stu-id="9c365-186">As an example, hello following *function.json* file defines a `route` property for an HTTP trigger:</span></span>

```json
    {
      "bindings": [
        {
          "type": "httpTrigger",
          "name": "req",
          "direction": "in",
          "methods": [ "get" ],
          "route": "products/{category:alpha}/{id:int?}"
        },
        {
          "type": "http",
          "name": "res",
          "direction": "out"
        }
      ]
    }
```

<span data-ttu-id="9c365-187">Utilizando esta configuração, Olá função é agora endereçável com Olá rota em vez de rota original Olá a seguir.</span><span class="sxs-lookup"><span data-stu-id="9c365-187">Using this configuration, hello function is now addressable with hello following route instead of hello original route.</span></span>

    http://<yourapp>.azurewebsites.net/api/products/electronics/357

<span data-ttu-id="9c365-188">Isto permite que o código de função Olá toosupport dois parâmetros no endereço Olá, "categoria" e "id".</span><span class="sxs-lookup"><span data-stu-id="9c365-188">This allows hello function code toosupport two parameters in hello address, "category" and "id".</span></span> <span data-ttu-id="9c365-189">Pode utilizar qualquer [Web API rota restrição](https://www.asp.net/web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2#constraints) com os parâmetros.</span><span class="sxs-lookup"><span data-stu-id="9c365-189">You can use any [Web API Route Constraint](https://www.asp.net/web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2#constraints) with your parameters.</span></span> <span data-ttu-id="9c365-190">Olá o seguinte código à função c# utilizam ambos os parâmetros.</span><span class="sxs-lookup"><span data-stu-id="9c365-190">hello following C# function code makes use of both parameters.</span></span>

```csharp
    public static Task<HttpResponseMessage> Run(HttpRequestMessage req, string category, int? id, 
                                                    TraceWriter log)
    {
        if (id == null)
           return  req.CreateResponse(HttpStatusCode.OK, $"All {category} items were requested.");
        else
           return  req.CreateResponse(HttpStatusCode.OK, $"{category} item with id = {id} has been requested.");
    }
```

<span data-ttu-id="9c365-191">Eis Olá do Node.js função código toouse mesmos parâmetros de rota.</span><span class="sxs-lookup"><span data-stu-id="9c365-191">Here is Node.js function code toouse hello same route parameters.</span></span>

```javascript
    module.exports = function (context, req) {

        var category = context.bindingData.category;
        var id = context.bindingData.id;

        if (!id) {
            context.res = {
                // status: 200, /* Defaults too200 */
                body: "All " + category + " items were requested."
            };
        }
        else {
            context.res = {
                // status: 200, /* Defaults too200 */
                body: category + " item with id = " + id + " was requested."
            };
        }

        context.done();
    } 
```

<span data-ttu-id="9c365-192">Por predefinição, todas as rotas de função são adicionado o prefixo *api*.</span><span class="sxs-lookup"><span data-stu-id="9c365-192">By default, all function routes are prefixed with *api*.</span></span> <span data-ttu-id="9c365-193">Também pode personalizar ou remover o prefixo de Olá utilizando Olá `http.routePrefix` propriedade no seu *host.json* ficheiro.</span><span class="sxs-lookup"><span data-stu-id="9c365-193">You can also customize or remove hello prefix using hello `http.routePrefix` property in your *host.json* file.</span></span> <span data-ttu-id="9c365-194">Olá exemplo a seguir remove Olá *api* prefixo de rota através da utilização de uma cadeia vazia para o prefixo de Olá no Olá *host.json* ficheiro.</span><span class="sxs-lookup"><span data-stu-id="9c365-194">hello following example removes hello *api* route prefix by using an empty string for hello prefix in hello *host.json* file.</span></span>

```json
    {
      "http": {
        "routePrefix": ""
      }
    }
```

<span data-ttu-id="9c365-195">Para obter informações detalhadas sobre como tooupdate Olá *host.json* ficheiro para a função, consulte [como ficheiros de aplicação de função tooupdate](functions-reference.md#fileupdate).</span><span class="sxs-lookup"><span data-stu-id="9c365-195">For detailed information on how tooupdate hello *host.json* file for your function, See, [How tooupdate function app files](functions-reference.md#fileupdate).</span></span> 

<span data-ttu-id="9c365-196">Para obter informações sobre outras propriedades que pode configurar na sua *host.json* de ficheiros, consulte [host.json referência](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json).</span><span class="sxs-lookup"><span data-stu-id="9c365-196">For information on other properties you can configure in your *host.json* file, see [host.json reference](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json).</span></span>


<a name="keys"></a>
## <a name="working-with-keys"></a><span data-ttu-id="9c365-197">Trabalhar com as chaves</span><span class="sxs-lookup"><span data-stu-id="9c365-197">Working with keys</span></span>
<span data-ttu-id="9c365-198">HttpTriggers pode tirar partido das chaves de segurança adicional.</span><span class="sxs-lookup"><span data-stu-id="9c365-198">HttpTriggers can leverage keys for added security.</span></span> <span data-ttu-id="9c365-199">Um padrão HttpTrigger pode utilizá-las como uma chave de API, exigindo Olá toobe chave presente no pedido de Olá.</span><span class="sxs-lookup"><span data-stu-id="9c365-199">A standard HttpTrigger can use these as an API key, requiring hello key toobe present on hello request.</span></span> <span data-ttu-id="9c365-200">Webhooks pode utilizar os pedidos de tooauthorize de chaves de diversas formas, consoante o fornecedor de Olá suporta.</span><span class="sxs-lookup"><span data-stu-id="9c365-200">Webhooks can use keys tooauthorize requests in a variety of ways, depending on what hello provider supports.</span></span>

<span data-ttu-id="9c365-201">As chaves são armazenadas como parte da sua aplicação de função no Azure e são encriptadas em pausa.</span><span class="sxs-lookup"><span data-stu-id="9c365-201">Keys are stored as part of your function app in Azure and are encrypted at rest.</span></span> <span data-ttu-id="9c365-202">tooview as chaves, criar novos ou toonew valores de chaves de agregação, navegue tooone das suas funções no portal de Olá e selecione "Gerir".</span><span class="sxs-lookup"><span data-stu-id="9c365-202">tooview your keys, create new ones, or roll keys toonew values, navigate tooone of your functions within hello portal and select "Manage."</span></span> 

<span data-ttu-id="9c365-203">Existem dois tipos de chaves:</span><span class="sxs-lookup"><span data-stu-id="9c365-203">There are two types of keys:</span></span>
- <span data-ttu-id="9c365-204">**Das chaves de anfitrião**: estas chaves são partilhadas por todas as funções dentro da aplicação de função Olá.</span><span class="sxs-lookup"><span data-stu-id="9c365-204">**Host keys**: These keys are shared by all functions within hello function app.</span></span> <span data-ttu-id="9c365-205">Quando utilizado como uma chave de API, estes cmdlets permitem a função de tooany de acesso à aplicação de função Olá.</span><span class="sxs-lookup"><span data-stu-id="9c365-205">When used as an API key, these allow access tooany function within hello function app.</span></span>
- <span data-ttu-id="9c365-206">**As chaves de função**: estas chaves aplicam-se apenas toohello funções específicas em que estão definidos.</span><span class="sxs-lookup"><span data-stu-id="9c365-206">**Function keys**: These keys apply only toohello specific functions under which they are defined.</span></span> <span data-ttu-id="9c365-207">Quando utilizado como uma chave de API, estes apenas permitem o acesso toothat função.</span><span class="sxs-lookup"><span data-stu-id="9c365-207">When used as an API key, these only allow access toothat function.</span></span>

<span data-ttu-id="9c365-208">Cada chave com o nome de referência e existe uma chave de predefinição (denominada "predefinido") ao nível de função e o anfitrião de Olá.</span><span class="sxs-lookup"><span data-stu-id="9c365-208">Each key is named for reference, and there is a default key (named "default") at hello function and host level.</span></span> <span data-ttu-id="9c365-209">Olá **chave mestra** uma chave de anfitrião predefinido com o nome "_master" que está definido para cada aplicação de função e não pode ser revogado.</span><span class="sxs-lookup"><span data-stu-id="9c365-209">hello **master key** is a default host key named "_master" that is defined for each function app and cannot be revoked.</span></span> <span data-ttu-id="9c365-210">Fornece acesso administrativo toohello runtime APIs.</span><span class="sxs-lookup"><span data-stu-id="9c365-210">It provides administrative access toohello runtime APIs.</span></span> <span data-ttu-id="9c365-211">Utilizar `"authLevel": "admin"` na Olá enlace JSON irá exigir esta chave toobe apresentada no pedido de Olá; qualquer outra chave ocorrerá uma falha de autorização.</span><span class="sxs-lookup"><span data-stu-id="9c365-211">Using `"authLevel": "admin"` in hello binding JSON will require this key toobe presented on hello request; any other key will result in a authorization failure.</span></span>

> [!NOTE]
> <span data-ttu-id="9c365-212">Devida toohello elevados permissões concedidas pela chave mestra de Olá, não deve partilhar esta chave com terceiros nem distribui-lo em aplicações de cliente nativo.</span><span class="sxs-lookup"><span data-stu-id="9c365-212">Due toohello elevated permissions granted by hello master key, you should not share this key with third parties or distribute it in native client applications.</span></span> <span data-ttu-id="9c365-213">Tenha cuidado quando escolher o nível de autorização de administrador Olá.</span><span class="sxs-lookup"><span data-stu-id="9c365-213">Exercise caution when choosing hello admin authorization level.</span></span>
> 
> 

### <a name="api-key-authorization"></a><span data-ttu-id="9c365-214">Autorização da chave de API</span><span class="sxs-lookup"><span data-stu-id="9c365-214">API key authorization</span></span>
<span data-ttu-id="9c365-215">Por predefinição, um HttpTrigger requer uma chave de API no pedido HTTP Olá.</span><span class="sxs-lookup"><span data-stu-id="9c365-215">By default, an HttpTrigger requires an API key in hello HTTP request.</span></span> <span data-ttu-id="9c365-216">Por isso, o pedido HTTP normalmente este aspeto:</span><span class="sxs-lookup"><span data-stu-id="9c365-216">So your HTTP request normally looks like this:</span></span>

    https://<yourapp>.azurewebsites.net/api/<function>?code=<ApiKey>

<span data-ttu-id="9c365-217">chave de Olá pode ser incluído numa variável de cadeia de consulta com o nome `code`, como acima, ou pode ser incluído num `x-functions-key` cabeçalho de HTTP.</span><span class="sxs-lookup"><span data-stu-id="9c365-217">hello key can be included in a query string variable named `code`, as above, or it can be included in an `x-functions-key` HTTP header.</span></span> <span data-ttu-id="9c365-218">valor de Olá da chave de Olá pode ser qualquer tecla de função definido para a função de Olá ou qualquer chave de anfitrião.</span><span class="sxs-lookup"><span data-stu-id="9c365-218">hello value of hello key can be any function key defined for hello function, or any host key.</span></span>

<span data-ttu-id="9c365-219">Pode escolher tooallow pedidos sem chaves ou especificar essa chave mestra de Olá tem de ser utilizado pela alteração Olá `authLevel` propriedade no Olá enlace JSON (consulte [acionador HTTP](#httptrigger)).</span><span class="sxs-lookup"><span data-stu-id="9c365-219">You can choose tooallow requests without keys or specify that hello master key must be used by changing hello `authLevel` property in hello binding JSON (see [HTTP trigger](#httptrigger)).</span></span>

### <a name="keys-and-webhooks"></a><span data-ttu-id="9c365-220">As chaves e webhooks</span><span class="sxs-lookup"><span data-stu-id="9c365-220">Keys and webhooks</span></span>
<span data-ttu-id="9c365-221">Autorização de Webhook é processada pelo componente de reciever de webhook Olá, parte Olá HttpTrigger e o mecanismo de Olá varia com base no tipo de webhook Olá.</span><span class="sxs-lookup"><span data-stu-id="9c365-221">Webhook authorization is handled by hello webhook reciever component, part of hello HttpTrigger, and hello mechanism varies based on hello webhook type.</span></span> <span data-ttu-id="9c365-222">Cada mecanismo, o Contudo dependem de uma chave.</span><span class="sxs-lookup"><span data-stu-id="9c365-222">Each mechanism does, however rely on a key.</span></span> <span data-ttu-id="9c365-223">Por predefinição, será utilizada a tecla de função de Olá com o nome "predefinida".</span><span class="sxs-lookup"><span data-stu-id="9c365-223">By default, hello function key named "default" will be used.</span></span> <span data-ttu-id="9c365-224">Se desejar toouse uma chave diferente, terá de tooconfigure Olá webhook fornecedor toosend Olá nome da chave com o pedido de Olá dos Olá seguintes formas:</span><span class="sxs-lookup"><span data-stu-id="9c365-224">If you wish toouse a different key, you will need tooconfigure hello webhook provider toosend hello key name with hello request in one of hello following ways:</span></span>

- <span data-ttu-id="9c365-225">**Cadeia de consulta**: fornecedor de Olá transmite o nome da chave Olá no Olá `clientid` parâmetro de cadeia de consulta (por exemplo, `https://<yourapp>.azurewebsites.net/api/<funcname>?clientid=<keyname>`).</span><span class="sxs-lookup"><span data-stu-id="9c365-225">**Query string**: hello provider passes hello key name in hello `clientid` query string parameter (e.g., `https://<yourapp>.azurewebsites.net/api/<funcname>?clientid=<keyname>`).</span></span>
- <span data-ttu-id="9c365-226">**Cabeçalho de pedido**: fornecedor de Olá transmite o nome da chave Olá no Olá `x-functions-clientid` cabeçalho.</span><span class="sxs-lookup"><span data-stu-id="9c365-226">**Request header**: hello provider passes hello key name in hello `x-functions-clientid` header.</span></span>

> [!NOTE]
> <span data-ttu-id="9c365-227">Teclas de função têm precedência sobre as chaves de anfitrião.</span><span class="sxs-lookup"><span data-stu-id="9c365-227">Function keys take precedence over host keys.</span></span> <span data-ttu-id="9c365-228">Se duas chaves são definidas com o mesmo nome, hello de Olá função chave será utilizada.</span><span class="sxs-lookup"><span data-stu-id="9c365-228">If two keys are defined with hello same name, hello function key will be used.</span></span>
> 
> 


<a name="httptriggersample"></a>
## <a name="http-trigger-samples"></a><span data-ttu-id="9c365-229">Exemplos de Acionador HTTP</span><span class="sxs-lookup"><span data-stu-id="9c365-229">HTTP trigger samples</span></span>
<span data-ttu-id="9c365-230">Suponhamos tiver Olá seguir acionador HTTP de Olá `bindings` matriz de function.json:</span><span class="sxs-lookup"><span data-stu-id="9c365-230">Suppose you have hello following HTTP trigger in hello `bindings` array of function.json:</span></span>

```json
{
    "name": "req",
    "type": "httpTrigger",
    "direction": "in",
    "authLevel": "function"
},
```

<span data-ttu-id="9c365-231">Consulte o exemplo de específicas do idioma Olá que procura um `name` parâmetro ou na cadeia de consulta Olá ou no corpo de Olá do pedido de Olá HTTP.</span><span class="sxs-lookup"><span data-stu-id="9c365-231">See hello language-specific sample that looks for a `name` parameter either in hello query string or hello body of hello HTTP request.</span></span>

* [<span data-ttu-id="9c365-232">C#</span><span class="sxs-lookup"><span data-stu-id="9c365-232">C#</span></span>](#httptriggercsharp)
* [<span data-ttu-id="9c365-233">F#</span><span class="sxs-lookup"><span data-stu-id="9c365-233">F#</span></span>](#httptriggerfsharp)
* [<span data-ttu-id="9c365-234">Node.js</span><span class="sxs-lookup"><span data-stu-id="9c365-234">Node.js</span></span>](#httptriggernodejs)


<a name="httptriggercsharp"></a>
### <a name="http-trigger-sample-in-c"></a><span data-ttu-id="9c365-235">Exemplo de Acionador HTTP em c#</span><span class="sxs-lookup"><span data-stu-id="9c365-235">HTTP trigger sample in C#</span></span> #
```csharp
using System.Net;
using System.Threading.Tasks;

public static async Task<HttpResponseMessage> Run(HttpRequestMessage req, TraceWriter log)
{
    log.Info($"C# HTTP trigger function processed a request. RequestUri={req.RequestUri}");

    // parse query parameter
    string name = req.GetQueryNameValuePairs()
        .FirstOrDefault(q => string.Compare(q.Key, "name", true) == 0)
        .Value;

    // Get request body
    dynamic data = await req.Content.ReadAsAsync<object>();

    // Set name tooquery string or body data
    name = name ?? data?.name;

    return name == null
        ? req.CreateResponse(HttpStatusCode.BadRequest, "Please pass a name on hello query string or in hello request body")
        : req.CreateResponse(HttpStatusCode.OK, "Hello " + name);
}
```

<span data-ttu-id="9c365-236">Também é possível vincular tooa POCO em vez de `HttpRequestMessage`.</span><span class="sxs-lookup"><span data-stu-id="9c365-236">You can also bind tooa POCO instead of `HttpRequestMessage`.</span></span> <span data-ttu-id="9c365-237">Isto irá ser hydrated do corpo de Olá de pedido de Olá, analisado como JSON.</span><span class="sxs-lookup"><span data-stu-id="9c365-237">This will be hydrated from hello body of hello request, parsed as JSON.</span></span> <span data-ttu-id="9c365-238">Da mesma forma, um tipo pode ser transmitido a saída de resposta HTTP de toohello enlace e este será devolvido como corpo da resposta Olá, com um código de 200 estado.</span><span class="sxs-lookup"><span data-stu-id="9c365-238">Similarly, a type can be passed toohello HTTP response output binding, and this will be returned as hello response body, with a 200 status code.</span></span>
```csharp
using System.Net;
using System.Threading.Tasks;

public static string Run(CustomObject req, TraceWriter log)
{
    return "Hello " + req?.name;
}

public class CustomObject {
     public String name {get; set;}
}
}
```

<a name="httptriggerfsharp"></a>
### <a name="http-trigger-sample-in-f"></a><span data-ttu-id="9c365-239">Exemplo de Acionador HTTP no F #</span><span class="sxs-lookup"><span data-stu-id="9c365-239">HTTP trigger sample in F#</span></span> #
```fsharp
open System.Net
open System.Net.Http
open FSharp.Interop.Dynamic

let Run(req: HttpRequestMessage) =
    async {
        let q =
            req.GetQueryNameValuePairs()
                |> Seq.tryFind (fun kv -> kv.Key = "name")
        match q with
        | Some kv ->
            return req.CreateResponse(HttpStatusCode.OK, "Hello " + kv.Value)
        | None ->
            let! data = Async.AwaitTask(req.Content.ReadAsAsync<obj>())
            try
                return req.CreateResponse(HttpStatusCode.OK, "Hello " + data?name)
            with e ->
                return req.CreateErrorResponse(HttpStatusCode.BadRequest, "Please pass a name on hello query string or in hello request body")
    } |> Async.StartAsTask
```

<span data-ttu-id="9c365-240">É necessário um `project.json` ficheiros que utilize NuGet tooreference Olá `FSharp.Interop.Dynamic` e `Dynamitey` assemblagens, como esta:</span><span class="sxs-lookup"><span data-stu-id="9c365-240">You need a `project.json` file that uses NuGet tooreference hello `FSharp.Interop.Dynamic` and `Dynamitey` assemblies, like this:</span></span>

```json
{
  "frameworks": {
    "net46": {
      "dependencies": {
        "Dynamitey": "1.0.2",
        "FSharp.Interop.Dynamic": "3.0.0"
      }
    }
  }
}
```

<span data-ttu-id="9c365-241">Isto irá utilizar as suas dependências NuGet toofetch e fará referência na seu script.</span><span class="sxs-lookup"><span data-stu-id="9c365-241">This will use NuGet toofetch your dependencies and will reference them in your script.</span></span>

<a name="httptriggernodejs"></a>
### <a name="http-trigger-sample-in-nodejs"></a><span data-ttu-id="9c365-242">Exemplo de Acionador HTTP no Node.JS</span><span class="sxs-lookup"><span data-stu-id="9c365-242">HTTP trigger sample in Node.JS</span></span>
```javascript
module.exports = function(context, req) {
    context.log('Node.js HTTP trigger function processed a request. RequestUri=%s', req.originalUrl);

    if (req.query.name || (req.body && req.body.name)) {
        context.res = {
            // status: 200, /* Defaults too200 */
            body: "Hello " + (req.query.name || req.body.name)
        };
    }
    else {
        context.res = {
            status: 400,
            body: "Please pass a name on hello query string or in hello request body"
        };
    }
    context.done();
};
```



<a name="hooktriggersample"></a>
## <a name="webhook-samples"></a><span data-ttu-id="9c365-243">Amostras do Webhook</span><span class="sxs-lookup"><span data-stu-id="9c365-243">Webhook samples</span></span>
<span data-ttu-id="9c365-244">Suponhamos tiver Olá seguir acionador de webhook no Olá `bindings` matriz de function.json:</span><span class="sxs-lookup"><span data-stu-id="9c365-244">Suppose you have hello following webhook trigger in hello `bindings` array of function.json:</span></span>

```json
{
    "webHookType": "github",
    "name": "req",
    "type": "httpTrigger",
    "direction": "in",
},
```

<span data-ttu-id="9c365-245">Consulte o exemplo do Olá específicas do idioma que os registos de comentários de problema do GitHub.</span><span class="sxs-lookup"><span data-stu-id="9c365-245">See hello language-specific sample that logs GitHub issue comments.</span></span>

* [<span data-ttu-id="9c365-246">C#</span><span class="sxs-lookup"><span data-stu-id="9c365-246">C#</span></span>](#hooktriggercsharp)
* [<span data-ttu-id="9c365-247">F#</span><span class="sxs-lookup"><span data-stu-id="9c365-247">F#</span></span>](#hooktriggerfsharp)
* [<span data-ttu-id="9c365-248">Node.js</span><span class="sxs-lookup"><span data-stu-id="9c365-248">Node.js</span></span>](#hooktriggernodejs)

<a name="hooktriggercsharp"></a>

### <a name="webhook-sample-in-c"></a><span data-ttu-id="9c365-249">Exemplo de Webhook em c#</span><span class="sxs-lookup"><span data-stu-id="9c365-249">Webhook sample in C#</span></span> #
```csharp
#r "Newtonsoft.Json"

using System;
using System.Net;
using System.Threading.Tasks;
using Newtonsoft.Json;

public static async Task<object> Run(HttpRequestMessage req, TraceWriter log)
{
    string jsonContent = await req.Content.ReadAsStringAsync();
    dynamic data = JsonConvert.DeserializeObject(jsonContent);

    log.Info($"WebHook was triggered! Comment: {data.comment.body}");

    return req.CreateResponse(HttpStatusCode.OK, new {
        body = $"New GitHub comment: {data.comment.body}"
    });
}
```

<a name="hooktriggerfsharp"></a>

### <a name="webhook-sample-in-f"></a><span data-ttu-id="9c365-250">Exemplo de Webhook no F #</span><span class="sxs-lookup"><span data-stu-id="9c365-250">Webhook sample in F#</span></span> #
```fsharp
open System.Net
open System.Net.Http
open FSharp.Interop.Dynamic
open Newtonsoft.Json

type Response = {
    body: string
}

let Run(req: HttpRequestMessage, log: TraceWriter) =
    async {
        let! content = req.Content.ReadAsStringAsync() |> Async.AwaitTask
        let data = content |> JsonConvert.DeserializeObject
        log.Info(sprintf "GitHub WebHook triggered! %s" data?comment?body)
        return req.CreateResponse(
            HttpStatusCode.OK,
            { body = sprintf "New GitHub comment: %s" data?comment?body })
    } |> Async.StartAsTask
```

<a name="hooktriggernodejs"></a>

### <a name="webhook-sample-in-nodejs"></a><span data-ttu-id="9c365-251">Exemplo de Webhook no Node.JS</span><span class="sxs-lookup"><span data-stu-id="9c365-251">Webhook sample in Node.JS</span></span>
```javascript
module.exports = function (context, data) {
    context.log('GitHub WebHook triggered!', data.comment.body);
    context.res = { body: 'New GitHub comment: ' + data.comment.body };
    context.done();
};
```


## <a name="next-steps"></a><span data-ttu-id="9c365-252">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="9c365-252">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

