---
title: "aaaCreate uma API sem servidor através das funções do Azure | Microsoft Docs"
description: "Como toocreate uma API sem servidor através das funções do Azure"
services: functions
author: mattchenderson
manager: erikre
ms.service: functions
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: tutorial
ms.date: 05/04/2017
ms.author: mahender
ms.custom: mvc
ms.openlocfilehash: 877e3b229d5477fc5fec594ccd284fb55d7f3c07
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-serverless-api-using-azure-functions"></a><span data-ttu-id="32b48-103">Criar uma API sem servidor através das funções do Azure</span><span class="sxs-lookup"><span data-stu-id="32b48-103">Create a serverless API using Azure Functions</span></span>

<span data-ttu-id="32b48-104">Neste tutorial, ficará a saber como as funções do Azure permite-lhe toobuild APIs altamente dimensionável.</span><span class="sxs-lookup"><span data-stu-id="32b48-104">In this tutorial you will learn how Azure Functions allows you toobuild highly-scalable APIs.</span></span> <span data-ttu-id="32b48-105">As funções do Azure é fornecido com uma coleção de incorporada HTTP acionadores e enlaces que tornam mais fácil tooauthor um ponto final numa variedade de idiomas, incluindo o Node.JS, c# e muito mais.</span><span class="sxs-lookup"><span data-stu-id="32b48-105">Azure Functions comes with a collection of built-in HTTP triggers and bindings which make it easy tooauthor an endpoint in a variety of languages, including Node.JS, C#, and more.</span></span> <span data-ttu-id="32b48-106">Neste tutorial, irá personalizar um HTTP acionador toohandle as ações específicas na sua conceção de API.</span><span class="sxs-lookup"><span data-stu-id="32b48-106">In this tutorial, you will customize an HTTP trigger toohandle specific actions in your API design.</span></span> <span data-ttu-id="32b48-107">Também irá preparar para a crescer a sua API, como o integrar com Proxies de funções do Azure e como configurar mock APIs.</span><span class="sxs-lookup"><span data-stu-id="32b48-107">You will also prepare for growing your API by integrating it with Azure Functions Proxies and setting up mock APIs.</span></span> <span data-ttu-id="32b48-108">Tudo isto é conseguido por cima Olá funções sem servidor ambiente de computação, pelo que não tem tooworry sobre dimensionamento recursos - apenas poder concentrar na sua lógica de API.</span><span class="sxs-lookup"><span data-stu-id="32b48-108">All of this is accomplished on top of hello Functions serverless compute environment, so you don't have tooworry about scaling resources - you can just focus on your API logic.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="32b48-109">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="32b48-109">Prerequisites</span></span> 

[!INCLUDE [Previous quickstart note](../../includes/functions-quickstart-previous-topics.md)]

<span data-ttu-id="32b48-110">função resultante Olá será utilizada para o resto Olá deste tutorial.</span><span class="sxs-lookup"><span data-stu-id="32b48-110">hello resulting function will be used for hello rest of this tutorial.</span></span>

### <a name="sign-in-tooazure"></a><span data-ttu-id="32b48-111">Inicie sessão no tooAzure</span><span class="sxs-lookup"><span data-stu-id="32b48-111">Sign in tooAzure</span></span>

<span data-ttu-id="32b48-112">Abra Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="32b48-112">Open hello Azure portal.</span></span> <span data-ttu-id="32b48-113">toodo, inicie sessão no demasiado[https://portal.azure.com](https://portal.azure.com) com a sua conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="32b48-113">toodo this, sign in too[https://portal.azure.com](https://portal.azure.com) with your Azure account.</span></span>

## <a name="customize-your-http-function"></a><span data-ttu-id="32b48-114">Personalizar a sua função HTTP</span><span class="sxs-lookup"><span data-stu-id="32b48-114">Customize your HTTP function</span></span>

<span data-ttu-id="32b48-115">Por predefinição, a função de acionada por HTTP é configurado tooaccept qualquer método HTTP.</span><span class="sxs-lookup"><span data-stu-id="32b48-115">By default, your HTTP-triggered function is configured tooaccept any HTTP method.</span></span> <span data-ttu-id="32b48-116">Também é um URL predefinido do formulário Olá `http://<yourapp>.azurewebsites.net/api/<funcname>?code=<functionkey>`.</span><span class="sxs-lookup"><span data-stu-id="32b48-116">There is also a default URL of hello form `http://<yourapp>.azurewebsites.net/api/<funcname>?code=<functionkey>`.</span></span> <span data-ttu-id="32b48-117">Se seguiu o guia de introdução Olá, em seguida, `<funcname>` provavelmente aspeto semelhante ao seguinte "HttpTriggerJS1".</span><span class="sxs-lookup"><span data-stu-id="32b48-117">If you followed hello quickstart, then `<funcname>` probably looks something like "HttpTriggerJS1".</span></span> <span data-ttu-id="32b48-118">Nesta secção, irá modificar pedidos de tooGET apenas do Olá função toorespond contra `/api/hello` encaminhar em vez disso.</span><span class="sxs-lookup"><span data-stu-id="32b48-118">In this section, you will modify hello function toorespond only tooGET requests against `/api/hello` route instead.</span></span> 

<span data-ttu-id="32b48-119">Navegue tooyour função no Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="32b48-119">Navigate tooyour function in hello Azure portal.</span></span> <span data-ttu-id="32b48-120">Selecione **integrar** no Olá deixado navegação.</span><span class="sxs-lookup"><span data-stu-id="32b48-120">Select **Integrate** in hello left navigation.</span></span>

![Personalizar uma função HTTP](./media/functions-create-serverless-api/customizing-http.png)

<span data-ttu-id="32b48-122">Utilize as definições de Acionador HTTP especificado na tabela de Olá.</span><span class="sxs-lookup"><span data-stu-id="32b48-122">Use the HTTP trigger settings as specified in hello table.</span></span>

| <span data-ttu-id="32b48-123">Campo</span><span class="sxs-lookup"><span data-stu-id="32b48-123">Field</span></span> | <span data-ttu-id="32b48-124">Valor da amostra</span><span class="sxs-lookup"><span data-stu-id="32b48-124">Sample value</span></span> | <span data-ttu-id="32b48-125">Descrição</span><span class="sxs-lookup"><span data-stu-id="32b48-125">Description</span></span> |
|---|---|---|
| <span data-ttu-id="32b48-126">Métodos de HTTP permitidos</span><span class="sxs-lookup"><span data-stu-id="32b48-126">Allowed HTTP methods</span></span> | <span data-ttu-id="32b48-127">Métodos selecionados</span><span class="sxs-lookup"><span data-stu-id="32b48-127">Selected methods</span></span> | <span data-ttu-id="32b48-128">Determinar que métodos HTTP podem ser utilizado tooinvoke esta função</span><span class="sxs-lookup"><span data-stu-id="32b48-128">Determines what HTTP methods may be used tooinvoke this function</span></span> |
| <span data-ttu-id="32b48-129">Métodos de HTTP selecionados</span><span class="sxs-lookup"><span data-stu-id="32b48-129">Selected HTTP methods</span></span> | <span data-ttu-id="32b48-130">INTRODUÇÃO</span><span class="sxs-lookup"><span data-stu-id="32b48-130">GET</span></span> | <span data-ttu-id="32b48-131">Permite que apenas toobe de métodos HTTP selecionado utilizado tooinvoke esta função</span><span class="sxs-lookup"><span data-stu-id="32b48-131">Allows only selected HTTP methods toobe used tooinvoke this function</span></span> |
| <span data-ttu-id="32b48-132">Modelo de rota</span><span class="sxs-lookup"><span data-stu-id="32b48-132">Route template</span></span> | <span data-ttu-id="32b48-133">/Hello</span><span class="sxs-lookup"><span data-stu-id="32b48-133">/hello</span></span> | <span data-ttu-id="32b48-134">Determina a rota de que é utilizado tooinvoke esta função</span><span class="sxs-lookup"><span data-stu-id="32b48-134">Determines what route is used tooinvoke this function</span></span> |

<span data-ttu-id="32b48-135">Tenha em atenção que não incluiu Olá `/api` base prefixo de caminho no modelo de rota Olá, como isto é processado por uma definição global.</span><span class="sxs-lookup"><span data-stu-id="32b48-135">Note that you did not include hello `/api` base path prefix in hello route template, as this is handled by a global setting.</span></span>

<span data-ttu-id="32b48-136">Clique em **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="32b48-136">Click **Save**.</span></span>

<span data-ttu-id="32b48-137">Pode saber mais sobre como personalizar funções HTTP no [enlaces HTTP de funções do Azure e webhook](https://docs.microsoft.com/azure/azure-functions/functions-bindings-http-webhook#customizing-the-http-endpoint).</span><span class="sxs-lookup"><span data-stu-id="32b48-137">You can learn more about customizing HTTP functions in [Azure Functions HTTP and webhook bindings](https://docs.microsoft.com/azure/azure-functions/functions-bindings-http-webhook#customizing-the-http-endpoint).</span></span>

### <a name="test-your-api"></a><span data-ttu-id="32b48-138">A API de teste</span><span class="sxs-lookup"><span data-stu-id="32b48-138">Test your API</span></span>

<span data-ttu-id="32b48-139">Em seguida, teste a função toosee-lo a trabalhar com a superfície de API novo Olá.</span><span class="sxs-lookup"><span data-stu-id="32b48-139">Next, test your function toosee it working with hello new API surface.</span></span>

<span data-ttu-id="32b48-140">Navegue página de desenvolvimento de back-toohello ao clicar no nome da função de Olá no Olá deixado navegação.</span><span class="sxs-lookup"><span data-stu-id="32b48-140">Navigate back toohello development page by clicking on hello function's name in hello left navigation.</span></span>

<span data-ttu-id="32b48-141">Clique em **obter URL de função** e copie o URL de Olá.</span><span class="sxs-lookup"><span data-stu-id="32b48-141">Click **Get function URL** and copy hello URL.</span></span> <span data-ttu-id="32b48-142">Deverá ver que utiliza Olá `/api/hello` encaminhar agora.</span><span class="sxs-lookup"><span data-stu-id="32b48-142">You should see that it uses hello `/api/hello` route now.</span></span>

<span data-ttu-id="32b48-143">Copie o URL de Olá para um novo separador do browser ou o cliente REST preferencial.</span><span class="sxs-lookup"><span data-stu-id="32b48-143">Copy hello URL into a new browser tab or your preferred REST client.</span></span> <span data-ttu-id="32b48-144">Browsers utilizará GET por predefinição.</span><span class="sxs-lookup"><span data-stu-id="32b48-144">Browsers will use GET by default.</span></span>

<span data-ttu-id="32b48-145">Execute a função Olá e confirme que está a funcionar.</span><span class="sxs-lookup"><span data-stu-id="32b48-145">Run hello function and confirm that it is working.</span></span> <span data-ttu-id="32b48-146">Poderá ter o parâmetro de "name" tooprovide Olá como um código de início rápido Olá de toosatisfy de cadeia de consulta.</span><span class="sxs-lookup"><span data-stu-id="32b48-146">You may need tooprovide hello "name" parameter as a query string toosatisfy hello quickstart code.</span></span>

<span data-ttu-id="32b48-147">Também pode tentar chamar Olá ponto final com outro tooconfirm de método HTTP que função Olá não foi executada.</span><span class="sxs-lookup"><span data-stu-id="32b48-147">You can also try calling hello endpoint with another HTTP method tooconfirm that hello function is not executed.</span></span> <span data-ttu-id="32b48-148">Para tal, terá de toouse um cliente REST, tais como cURL, Postman ou Fiddler.</span><span class="sxs-lookup"><span data-stu-id="32b48-148">For this, you will need toouse a REST client, such as cURL, Postman, or Fiddler.</span></span>

## <a name="proxies-overview"></a><span data-ttu-id="32b48-149">Descrição geral de proxies</span><span class="sxs-lookup"><span data-stu-id="32b48-149">Proxies overview</span></span>

<span data-ttu-id="32b48-150">Na secção seguinte, Olá, será de superfície da API através de um proxy.</span><span class="sxs-lookup"><span data-stu-id="32b48-150">In hello next section, you will surface your API through a proxy.</span></span> <span data-ttu-id="32b48-151">Proxies de funções do Azure é uma funcionalidade de pré-visualização permite-lhe tooforward pedidos tooother recursos.</span><span class="sxs-lookup"><span data-stu-id="32b48-151">Azure Functions Proxies is a preview feature that allows you tooforward requests tooother resources.</span></span> <span data-ttu-id="32b48-152">Definir um ponto final de HTTP tal como com o acionador de HTTP, mas em vez de escrever código tooexecute quando esse ponto final é chamado, terá de fornecer uma implementação de remota tooa URL.</span><span class="sxs-lookup"><span data-stu-id="32b48-152">You define an HTTP endpoint just like with HTTP trigger, but instead of writing code tooexecute when that endpoint is called, you provide a URL tooa remote implementation.</span></span> <span data-ttu-id="32b48-153">Isto permite-lhe toocompose API várias origens para uma único superfície de API que é mais fácil para os clientes tooconsume.</span><span class="sxs-lookup"><span data-stu-id="32b48-153">This allows you toocompose multiple API sources into a single API surface which is easy for clients tooconsume.</span></span> <span data-ttu-id="32b48-154">Isto é particularmente útil se quiser toobuild a API como micro-serviços.</span><span class="sxs-lookup"><span data-stu-id="32b48-154">This is particularly useful if you wish toobuild your API as microservices.</span></span>

<span data-ttu-id="32b48-155">Um ponto proxy de pode tooany HTTP recursos, tais como:</span><span class="sxs-lookup"><span data-stu-id="32b48-155">A proxy can point tooany HTTP resource, such as:</span></span>
- <span data-ttu-id="32b48-156">Funções do Azure</span><span class="sxs-lookup"><span data-stu-id="32b48-156">Azure Functions</span></span> 
- <span data-ttu-id="32b48-157">API apps no [App Service do Azure](https://docs.microsoft.com/azure/app-service/app-service-value-prop-what-is)</span><span class="sxs-lookup"><span data-stu-id="32b48-157">API apps in [Azure App Service](https://docs.microsoft.com/azure/app-service/app-service-value-prop-what-is)</span></span>
- <span data-ttu-id="32b48-158">Os contentores de docker no [do serviço de aplicações no Linux](https://docs.microsoft.com/azure/app-service/app-service-linux-readme)</span><span class="sxs-lookup"><span data-stu-id="32b48-158">Docker containers in [App Service on Linux](https://docs.microsoft.com/azure/app-service/app-service-linux-readme)</span></span>
- <span data-ttu-id="32b48-159">Quaisquer outro API alojada</span><span class="sxs-lookup"><span data-stu-id="32b48-159">Any other hosted API</span></span>

<span data-ttu-id="32b48-160">Consulte toolearn mais informações sobre proxies [trabalhar com os Proxies de funções do Azure (pré-visualização)].</span><span class="sxs-lookup"><span data-stu-id="32b48-160">toolearn more about proxies, see [Working with Azure Functions Proxies (preview)].</span></span>

## <a name="create-your-first-proxy"></a><span data-ttu-id="32b48-161">Criar o primeiro proxy</span><span class="sxs-lookup"><span data-stu-id="32b48-161">Create your first proxy</span></span>

<span data-ttu-id="32b48-162">Nesta secção, irá criar um novo proxy que funciona como um front-end tooyour API geral.</span><span class="sxs-lookup"><span data-stu-id="32b48-162">In this section, you will create a new proxy which serves as a frontend tooyour overall API.</span></span> 

### <a name="setting-up-hello-frontend-environment"></a><span data-ttu-id="32b48-163">Configurar o ambiente de front-end Olá</span><span class="sxs-lookup"><span data-stu-id="32b48-163">Setting up hello frontend environment</span></span>

<span data-ttu-id="32b48-164">Repita os passos de Olá demasiado[criar uma aplicação de função](https://docs.microsoft.com/azure/azure-functions/functions-create-first-azure-function#create-a-function-app) toocreate uma nova aplicação de função na qual irá criar o proxy.</span><span class="sxs-lookup"><span data-stu-id="32b48-164">Repeat hello steps too[Create a function app](https://docs.microsoft.com/azure/azure-functions/functions-create-first-azure-function#create-a-function-app) toocreate a new function app in which you will create your proxy.</span></span> <span data-ttu-id="32b48-165">Esta nova aplicação irá servir como front-end de Olá para a nossa API e aplicação de função Olá que foram anteriormente editar irá servir como um back-end.</span><span class="sxs-lookup"><span data-stu-id="32b48-165">This new app will serve as hello frontend for our API, and hello function app you were previously editing will serve as a backend.</span></span>

<span data-ttu-id="32b48-166">Navegue tooyour nova front-end aplicação de função no portal de Olá.</span><span class="sxs-lookup"><span data-stu-id="32b48-166">Navigate tooyour new frontend function app in hello portal.</span></span>

<span data-ttu-id="32b48-167">Selecione **definições**.</span><span class="sxs-lookup"><span data-stu-id="32b48-167">Select **Settings**.</span></span> <span data-ttu-id="32b48-168">Em seguida, ative **ativar Proxies de funções do Azure (pré-visualização)** demasiado "em".</span><span class="sxs-lookup"><span data-stu-id="32b48-168">Then toggle **Enable Azure Functions Proxies (preview)** too"On".</span></span>

<span data-ttu-id="32b48-169">Selecione **definições plataforma** e escolha **definições da aplicação**.</span><span class="sxs-lookup"><span data-stu-id="32b48-169">Select **Platform Settings** and choose **Application Settings**.</span></span>

<span data-ttu-id="32b48-170">Desloque para baixo demasiado**as definições de aplicação** e criar uma nova definição com a chave "HELLO_HOST".</span><span class="sxs-lookup"><span data-stu-id="32b48-170">Scroll down too**App settings** and create a new setting with key "HELLO_HOST".</span></span> <span data-ttu-id="32b48-171">Definir o respetivo anfitrião toohello do valor da sua aplicação de função de back-end, tal como `<YourApp>.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="32b48-171">Set its value toohello host of your backend function app, such as `<YourApp>.azurewebsites.net`.</span></span> <span data-ttu-id="32b48-172">Esta é a parte do URL de Olá que copiou anteriormente ao testar a sua função HTTP.</span><span class="sxs-lookup"><span data-stu-id="32b48-172">This is part of hello URL that you copied earlier when testing your HTTP function.</span></span> <span data-ttu-id="32b48-173">Irá referenciar esta definição na configuração de Olá mais tarde.</span><span class="sxs-lookup"><span data-stu-id="32b48-173">You'll reference this setting in hello configuration later.</span></span>

> [!NOTE] 
> <span data-ttu-id="32b48-174">As definições de aplicação são recomendadas para tooprevent de configuração de anfitrião Olá uma dependência de ambiente hard-coded para proxy de Olá.</span><span class="sxs-lookup"><span data-stu-id="32b48-174">App settings are recommended for hello host configuration tooprevent a hard-coded environment dependency for hello proxy.</span></span> <span data-ttu-id="32b48-175">Utilizar as definições de aplicação significa que pode mover a configuração de proxy Olá entre ambientes e definições de aplicação específico do ambiente de Olá serão aplicadas.</span><span class="sxs-lookup"><span data-stu-id="32b48-175">Using app settings means that you can move hello proxy configuration between environments, and hello environment-specific app settings will be applied.</span></span>

<span data-ttu-id="32b48-176">Clique em **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="32b48-176">Click **Save**.</span></span>

### <a name="creating-a-proxy-on-hello-frontend"></a><span data-ttu-id="32b48-177">Criar um proxy no front-end de Olá</span><span class="sxs-lookup"><span data-stu-id="32b48-177">Creating a proxy on hello frontend</span></span>

<span data-ttu-id="32b48-178">Navegue até a aplicação de função de front-end de back-tooyour no portal de Olá.</span><span class="sxs-lookup"><span data-stu-id="32b48-178">Navigate back tooyour frontend function app in hello portal.</span></span>

<span data-ttu-id="32b48-179">No painel navegação esquerda Olá, clique Olá juntamente com o início de sessão seguinte '+' demasiado "Proxies (pré-visualização)".</span><span class="sxs-lookup"><span data-stu-id="32b48-179">In hello left-hand navigation, click hello plus sign '+' next too"Proxies (preview)".</span></span>

![Criar um proxy](./media/functions-create-serverless-api/creating-proxy.png)

<span data-ttu-id="32b48-181">Utilize as definições de proxy conforme especificado na tabela de Olá.</span><span class="sxs-lookup"><span data-stu-id="32b48-181">Use proxy settings as specified in hello table.</span></span>

| <span data-ttu-id="32b48-182">Campo</span><span class="sxs-lookup"><span data-stu-id="32b48-182">Field</span></span> | <span data-ttu-id="32b48-183">Valor da amostra</span><span class="sxs-lookup"><span data-stu-id="32b48-183">Sample value</span></span> | <span data-ttu-id="32b48-184">Descrição</span><span class="sxs-lookup"><span data-stu-id="32b48-184">Description</span></span> |
|---|---|---|
| <span data-ttu-id="32b48-185">Nome</span><span class="sxs-lookup"><span data-stu-id="32b48-185">Name</span></span> | <span data-ttu-id="32b48-186">HelloProxy</span><span class="sxs-lookup"><span data-stu-id="32b48-186">HelloProxy</span></span> | <span data-ttu-id="32b48-187">Um nome amigável utilizado apenas para gestão</span><span class="sxs-lookup"><span data-stu-id="32b48-187">A friendly name used only for management</span></span> |
| <span data-ttu-id="32b48-188">Modelo de rota</span><span class="sxs-lookup"><span data-stu-id="32b48-188">Route template</span></span> | <span data-ttu-id="32b48-189">Olá/api /</span><span class="sxs-lookup"><span data-stu-id="32b48-189">/api/hello</span></span> | <span data-ttu-id="32b48-190">Determina a rota de que é utilizado tooinvoke este proxy</span><span class="sxs-lookup"><span data-stu-id="32b48-190">Determines what route is used tooinvoke this proxy</span></span> |
| <span data-ttu-id="32b48-191">URL de back-end</span><span class="sxs-lookup"><span data-stu-id="32b48-191">Backend URL</span></span> | <span data-ttu-id="32b48-192">https://%HELLO_HOST%/API/Hello</span><span class="sxs-lookup"><span data-stu-id="32b48-192">https://%HELLO_HOST%/api/hello</span></span> | <span data-ttu-id="32b48-193">Especifica o pedido de Olá Olá ponto final toowhich deve ser efetuado</span><span class="sxs-lookup"><span data-stu-id="32b48-193">Specifies hello endpoint toowhich hello request should be proxied</span></span> |

<span data-ttu-id="32b48-194">Tenha em atenção que Proxies fornecem Olá `/api` prefixo do caminho de base e este deve ser incluído no modelo de rota Olá.</span><span class="sxs-lookup"><span data-stu-id="32b48-194">Note that Proxies does not provide hello `/api` base path prefix, and this must be included in hello route template.</span></span>

<span data-ttu-id="32b48-195">Olá `%HELLO_HOST%` sintaxe fará referência a definição de aplicação Olá que criou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="32b48-195">hello `%HELLO_HOST%` syntax will reference hello app setting you created earlier.</span></span> <span data-ttu-id="32b48-196">Olá resolvido que URL irá apontar função original tooyour.</span><span class="sxs-lookup"><span data-stu-id="32b48-196">hello resolved URL will point tooyour original function.</span></span>

<span data-ttu-id="32b48-197">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="32b48-197">Click **Create**.</span></span>

<span data-ttu-id="32b48-198">Pode experimentar o seu novo proxy ao copiar Olá URL de Proxy e testá-lo no browser Olá ou com o cliente HTTP favorito.</span><span class="sxs-lookup"><span data-stu-id="32b48-198">You can try out your new proxy by copying hello Proxy URL and testing it in hello browser or with your favorite HTTP client.</span></span>

## <a name="create-a-mock-api"></a><span data-ttu-id="32b48-199">Criar uma API mock</span><span class="sxs-lookup"><span data-stu-id="32b48-199">Create a mock API</span></span>

<span data-ttu-id="32b48-200">Em seguida, irá utilizar um proxy toocreate uma API mock para a sua solução.</span><span class="sxs-lookup"><span data-stu-id="32b48-200">Next, you will use a proxy toocreate a mock API for your solution.</span></span> <span data-ttu-id="32b48-201">Isto permite que o desenvolvimento de cliente tooprogress, sem necessitar de back-end de Olá totalmente implementado.</span><span class="sxs-lookup"><span data-stu-id="32b48-201">This allows client development tooprogress, without needing hello backend fully implemented.</span></span> <span data-ttu-id="32b48-202">Mais tarde no desenvolvimento, pode criar uma nova aplicação de função que suporte esta lógica e redirecionar o tooit de proxy.</span><span class="sxs-lookup"><span data-stu-id="32b48-202">Later in development, you could create a new function app which supports this logic and redirect your proxy tooit.</span></span>

<span data-ttu-id="32b48-203">toocreate mock esta API, vamos criar um novo proxy, desta vez utilizando o Olá [Editor do serviço de aplicações](https://github.com/projectkudu/kudu/wiki/App-Service-Editor).</span><span class="sxs-lookup"><span data-stu-id="32b48-203">toocreate this mock API, we will create a new proxy, this time using hello [App Service Editor](https://github.com/projectkudu/kudu/wiki/App-Service-Editor).</span></span> <span data-ttu-id="32b48-204">tooget iniciado, navegue tooyour a aplicação de função no portal de Olá.</span><span class="sxs-lookup"><span data-stu-id="32b48-204">tooget started, navigate tooyour function app in hello portal.</span></span> <span data-ttu-id="32b48-205">Selecione **funcionalidades da plataforma** e localizar **Editor do serviço de aplicações**.</span><span class="sxs-lookup"><span data-stu-id="32b48-205">Select **Platform features** and find **App Service Editor**.</span></span> <span data-ttu-id="32b48-206">Clicar em Isto abrirá Olá Editor do serviço de aplicações num novo separador.</span><span class="sxs-lookup"><span data-stu-id="32b48-206">Clicking this will open hello App Service Editor in a new tab.</span></span>

<span data-ttu-id="32b48-207">Selecione `proxies.json` no Olá deixado navegação.</span><span class="sxs-lookup"><span data-stu-id="32b48-207">Select `proxies.json` in hello left navigation.</span></span> <span data-ttu-id="32b48-208">Este é o ficheiro de Olá que armazena a configuração de Olá para todos os seus proxies.</span><span class="sxs-lookup"><span data-stu-id="32b48-208">This is hello file which stores hello configuration for all of your proxies.</span></span> <span data-ttu-id="32b48-209">Se utilizar um dos Olá [funciona métodos de implementação](https://docs.microsoft.com/azure/azure-functions/functions-continuous-deployment), este é o ficheiro Olá irão manter o controlo de origem.</span><span class="sxs-lookup"><span data-stu-id="32b48-209">If you use one of hello [Functions deployment methods](https://docs.microsoft.com/azure/azure-functions/functions-continuous-deployment), this is hello file you will maintain in source control.</span></span> <span data-ttu-id="32b48-210">toolearn mais informações sobre este ficheiro, consulte [Proxies advanced configuration](https://docs.microsoft.com/azure/azure-functions/functions-proxies#advanced-configuration).</span><span class="sxs-lookup"><span data-stu-id="32b48-210">toolearn more about this file, see [Proxies advanced configuration](https://docs.microsoft.com/azure/azure-functions/functions-proxies#advanced-configuration).</span></span>

<span data-ttu-id="32b48-211">Se tiver seguido até ao momento, o proxies.json deve aspeto Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="32b48-211">If you've followed along so far, your proxies.json should look like hello following:</span></span>

```json
{
    "$schema": "http://json.schemastore.org/proxies",
    "proxies": {
        "HelloProxy": {
            "matchCondition": {
                "route": "/api/hello"
            },
            "backendUri": "https://%HELLO_HOST%/api/hello"
        }
    }
}
```

<span data-ttu-id="32b48-212">Em seguida irá adicionar a API mock.</span><span class="sxs-lookup"><span data-stu-id="32b48-212">Next you'll add your mock API.</span></span> <span data-ttu-id="32b48-213">Substitua o ficheiro proxies.json seguinte Olá:</span><span class="sxs-lookup"><span data-stu-id="32b48-213">Replace your proxies.json file with hello following:</span></span>

```json
{
    "$schema": "http://json.schemastore.org/proxies",
    "proxies": {
        "HelloProxy": {
            "matchCondition": {
                "route": "/api/hello"
            },
            "backendUri": "https://%HELLO_HOST%/api/hello"
        },
        "GetUserByName" : {
            "matchCondition": {
                "methods": [ "GET" ],
                "route": "/api/users/{username}"
            },
            "responseOverrides": {
                "response.statusCode": "200",
                "response.headers.Content-Type" : "application/json",
                "response.body": {
                    "name": "{username}",
                    "description": "Awesome developer and master of serverless APIs",
                    "skills": [
                        "Serverless",
                        "APIs",
                        "Azure",
                        "Cloud"
                    ]
                }
            }
        }
    }
}
```

<span data-ttu-id="32b48-214">Esta ação adiciona um novo proxy, "GetUserByName", sem a propriedade de backendUri Olá.</span><span class="sxs-lookup"><span data-stu-id="32b48-214">This adds a new proxy, "GetUserByName", without hello backendUri property.</span></span> <span data-ttu-id="32b48-215">Em vez de chamar outro recurso, modifica a resposta de predefinição Olá de Proxies utilizando uma substituição de resposta.</span><span class="sxs-lookup"><span data-stu-id="32b48-215">Instead of calling another resource, it modifies hello default response from Proxies using a response override.</span></span> <span data-ttu-id="32b48-216">Substituições de pedido e resposta também podem ser utilizadas em conjunto com um URL de back-end.</span><span class="sxs-lookup"><span data-stu-id="32b48-216">Request and response overrides can also be used in conjunction with a backend URL.</span></span> <span data-ttu-id="32b48-217">Isto é particularmente útil quando a funcionalidade de proxy tooa legado sistema, onde poderá ser necessário toomodify cabeçalhos, parâmetros de consulta, etc. toolearn mais sobre o pedido e resposta substituições, consulte [modificar pedidos e respostas no Proxies](https://docs.microsoft.com/azure/azure-functions/functions-proxies#a-namemodify-requests-responsesamodifying-requests-and-responses).</span><span class="sxs-lookup"><span data-stu-id="32b48-217">This is particularly useful when proxying tooa legacy system, where you might need toomodify headers, query parameters, etc. toolearn more about request and response overrides, see [Modifying requests and responses in Proxies](https://docs.microsoft.com/azure/azure-functions/functions-proxies#a-namemodify-requests-responsesamodifying-requests-and-responses).</span></span>

<span data-ttu-id="32b48-218">Testar a sua API mock ao chamar Olá `/api/users/{username}` ponto final utilizando um browser ou o cliente REST favorito.</span><span class="sxs-lookup"><span data-stu-id="32b48-218">Test your mock API by calling hello `/api/users/{username}` endpoint using a browser or your favorite REST client.</span></span> <span data-ttu-id="32b48-219">Ser tooreplace se _{username}_ com um valor de cadeia representando um nome de utilizador.</span><span class="sxs-lookup"><span data-stu-id="32b48-219">Be sure tooreplace _{username}_ with a string value representing a username.</span></span>

## <a name="next-steps"></a><span data-ttu-id="32b48-220">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="32b48-220">Next steps</span></span>

<span data-ttu-id="32b48-221">Neste tutorial, aprendeu como toobuild e personalizar uma API das funções do Azure.</span><span class="sxs-lookup"><span data-stu-id="32b48-221">In this tutorial, you learned how toobuild and customize an API on Azure Functions.</span></span> <span data-ttu-id="32b48-222">Também aprendeu como toobring várias APIs, incluindo mocks, em conjunto como uma superfície de API unificada.</span><span class="sxs-lookup"><span data-stu-id="32b48-222">You also learned how toobring multiple APIs, including mocks, together as a unified API surface.</span></span> <span data-ttu-id="32b48-223">Pode utilizar estes toobuild técnicas os APIs de qualquer complexidade, todos os durante a execução em Olá sem servidor computação modelo forneceu as funções do Azure.</span><span class="sxs-lookup"><span data-stu-id="32b48-223">You can use these techniques toobuild out APIs of any complexity, all while running on hello serverless compute model provided by Azure Functions.</span></span>

<span data-ttu-id="32b48-224">Olá referências seguintes podem ser útil como desenvolver ainda mais a API:</span><span class="sxs-lookup"><span data-stu-id="32b48-224">hello following references may be helpful as you develop your API further:</span></span>

- [<span data-ttu-id="32b48-225">Enlaces de funções de HTTP e webhook do Azure</span><span class="sxs-lookup"><span data-stu-id="32b48-225">Azure Functions HTTP and webhook bindings</span></span>](https://docs.microsoft.com/azure/azure-functions/functions-bindings-http-webhook)
- <span data-ttu-id="32b48-226">[trabalhar com os Proxies de funções do Azure (pré-visualização)]</span><span class="sxs-lookup"><span data-stu-id="32b48-226">[Working with Azure Functions Proxies (preview)]</span></span>
- [<span data-ttu-id="32b48-227">Documentar uma API de funções do Azure (pré-visualização)</span><span class="sxs-lookup"><span data-stu-id="32b48-227">Documenting an Azure Functions API (preview)</span></span>](https://docs.microsoft.com/azure/azure-functions/functions-api-definition-getting-started)


[Create your first function]: https://docs.microsoft.com/azure/azure-functions/functions-create-first-azure-function
[trabalhar com os Proxies de funções do Azure (pré-visualização)]: https://docs.microsoft.com/azure/azure-functions/functions-proxies
