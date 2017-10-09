---
title: "aaaWork com os proxies de funções do Azure | Microsoft Docs"
description: "Descrição geral de como toouse Proxies de funções do Azure"
services: functions
documentationcenter: 
author: mattchenderson
manager: erikre
editor: 
ms.assetid: 
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 04/11/2017
ms.author: mahender
ms.openlocfilehash: 4d94c89e8f8f2d2c771b01bae142bf9a4f3b7f2a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="work-with-azure-functions-proxies-preview"></a><span data-ttu-id="52909-103">Trabalhar com os Proxies de funções do Azure (pré-visualização)</span><span class="sxs-lookup"><span data-stu-id="52909-103">Work with Azure Functions Proxies (preview)</span></span>

> [!NOTE] 
> <span data-ttu-id="52909-104">Proxies de funções do Azure está atualmente em pré-visualização.</span><span class="sxs-lookup"><span data-stu-id="52909-104">Azure Functions Proxies is currently in preview.</span></span> <span data-ttu-id="52909-105">É gratuito enquanto na pré-visualização, mas funções padrão faturação aplica-se tooproxy execuções.</span><span class="sxs-lookup"><span data-stu-id="52909-105">It is free while in preview, but standard Functions billing applies tooproxy executions.</span></span> <span data-ttu-id="52909-106">Para obter mais informações, consulte [preços de funções do Azure](https://azure.microsoft.com/pricing/details/functions/).</span><span class="sxs-lookup"><span data-stu-id="52909-106">For more information, see [Azure Functions pricing](https://azure.microsoft.com/pricing/details/functions/).</span></span>

<span data-ttu-id="52909-107">Este artigo explica como tooconfigure e funcionam com os Proxies de funções do Azure.</span><span class="sxs-lookup"><span data-stu-id="52909-107">This article explains how tooconfigure and work with Azure Functions Proxies.</span></span> <span data-ttu-id="52909-108">Com esta funcionalidade, pode especificar pontos finais na sua aplicação de função que são implementados por outro recurso.</span><span class="sxs-lookup"><span data-stu-id="52909-108">With this feature, you can specify endpoints on your function app that are implemented by another resource.</span></span> <span data-ttu-id="52909-109">Pode utilizar estes toobreak proxies uma API de grandes dimensões em várias aplicações de função (como uma arquitetura de microsserviço), enquanto ainda apresentar uma único superfície de API para os clientes.</span><span class="sxs-lookup"><span data-stu-id="52909-109">You can use these proxies toobreak a large API into multiple function apps (as in a microservice architecture), while still presenting a single API surface for clients.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]


## <span data-ttu-id="52909-110"><a name="enable"></a>Ativar as funções do Azure Proxies</span><span class="sxs-lookup"><span data-stu-id="52909-110"><a name="enable"></a>Enable Azure Functions Proxies</span></span>

<span data-ttu-id="52909-111">Proxies não estão ativadas por predefinição.</span><span class="sxs-lookup"><span data-stu-id="52909-111">Proxies are not enabled by default.</span></span> <span data-ttu-id="52909-112">Pode criar proxies enquanto Olá funcionalidade está desativada, mas não executará.</span><span class="sxs-lookup"><span data-stu-id="52909-112">You can create proxies while hello feature is disabled, but they will not execute.</span></span> <span data-ttu-id="52909-113">tooenable proxies Olá seguintes:</span><span class="sxs-lookup"><span data-stu-id="52909-113">tooenable proxies, do hello following:</span></span>

1. <span data-ttu-id="52909-114">Abra Olá [portal do Azure], e, em seguida, aceda a aplicação de função tooyour.</span><span class="sxs-lookup"><span data-stu-id="52909-114">Open hello [Azure portal], and then go tooyour function app.</span></span>
2. <span data-ttu-id="52909-115">Selecione **as definições de aplicação de função**.</span><span class="sxs-lookup"><span data-stu-id="52909-115">Select **Function app settings**.</span></span>
3. <span data-ttu-id="52909-116">Comutador **ativar Proxies de funções do Azure (pré-visualização)** demasiado**no**.</span><span class="sxs-lookup"><span data-stu-id="52909-116">Switch **Enable Azure Functions Proxies (preview)** too**On**.</span></span>

<span data-ttu-id="52909-117">Também pode regressar aqui o tempo de execução do tooupdate Olá proxy à novas funcionalidades ficam disponíveis.</span><span class="sxs-lookup"><span data-stu-id="52909-117">You can also return here tooupdate hello proxy runtime as new features become available.</span></span>


## <span data-ttu-id="52909-118"><a name="create"></a>Criar um proxy</span><span class="sxs-lookup"><span data-stu-id="52909-118"><a name="create"></a>Create a proxy</span></span>

<span data-ttu-id="52909-119">Esta secção mostra como toocreate um proxy em Olá portal das funções.</span><span class="sxs-lookup"><span data-stu-id="52909-119">This section shows you how toocreate a proxy in hello Functions portal.</span></span>

1. <span data-ttu-id="52909-120">Abra Olá [portal do Azure], e, em seguida, aceda a aplicação de função tooyour.</span><span class="sxs-lookup"><span data-stu-id="52909-120">Open hello [Azure portal], and then go tooyour function app.</span></span>
2. <span data-ttu-id="52909-121">No painel esquerdo Olá, selecione **novo proxy**.</span><span class="sxs-lookup"><span data-stu-id="52909-121">In hello left pane, select **New proxy**.</span></span>
3. <span data-ttu-id="52909-122">Forneça um nome para o proxy.</span><span class="sxs-lookup"><span data-stu-id="52909-122">Provide a name for your proxy.</span></span>
4. <span data-ttu-id="52909-123">Configurar o ponto final de Olá que é exposto nesta aplicação de função especificando Olá **modelo de rota** e **métodos de HTTP**.</span><span class="sxs-lookup"><span data-stu-id="52909-123">Configure hello endpoint that's exposed on this function app by specifying hello **route template** and **HTTP methods**.</span></span> <span data-ttu-id="52909-124">Estes parâmetros comportar-se de acordo com as regras de toohello para [HTTP acionadores].</span><span class="sxs-lookup"><span data-stu-id="52909-124">These parameters behave according toohello rules for [HTTP triggers].</span></span>
5. <span data-ttu-id="52909-125">Conjunto Olá **URL back-end** tooanother endpoint.</span><span class="sxs-lookup"><span data-stu-id="52909-125">Set hello **backend URL** tooanother endpoint.</span></span> <span data-ttu-id="52909-126">Este ponto final pode ser uma função na outra aplicação de função, ou pode ser qualquer outra API.</span><span class="sxs-lookup"><span data-stu-id="52909-126">This endpoint could be a function in another function app, or it could be any other API.</span></span> <span data-ttu-id="52909-127">Olá valor não necessita de toobe estática e pode fazer referência a [definições da aplicação] e [parâmetros do pedido de cliente original Olá].</span><span class="sxs-lookup"><span data-stu-id="52909-127">hello value does not need toobe static, and it can reference [application settings] and [parameters from hello original client request].</span></span>
6. <span data-ttu-id="52909-128">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="52909-128">Click **Create**.</span></span>

<span data-ttu-id="52909-129">O proxy agora existe como um novo ponto final na sua aplicação de função.</span><span class="sxs-lookup"><span data-stu-id="52909-129">Your proxy now exists as a new endpoint on your function app.</span></span> <span data-ttu-id="52909-130">A partir de uma perspetiva do cliente, é equivalente tooan HttpTrigger nas funções do Azure.</span><span class="sxs-lookup"><span data-stu-id="52909-130">From a client perspective, it is equivalent tooan HttpTrigger in Azure Functions.</span></span> <span data-ttu-id="52909-131">Pode experimentar o seu novo proxy ao copiar Olá URL de Proxy e testá-lo com o cliente HTTP favorito.</span><span class="sxs-lookup"><span data-stu-id="52909-131">You can try out your new proxy by copying hello Proxy URL and testing it with your favorite HTTP client.</span></span>

## <span data-ttu-id="52909-132"><a name="modify-requests-responses"></a>Modificar pedidos e respostas</span><span class="sxs-lookup"><span data-stu-id="52909-132"><a name="modify-requests-responses"></a>Modify requests and responses</span></span>

<span data-ttu-id="52909-133">Com os Proxies de funções do Azure, pode modificar pedidos tooand respostas de back-end Olá.</span><span class="sxs-lookup"><span data-stu-id="52909-133">With Azure Functions Proxies, you can modify requests tooand responses from hello back end.</span></span> <span data-ttu-id="52909-134">Estes transformações podem utilizar variáveis, tal como definido no [utilizar variáveis].</span><span class="sxs-lookup"><span data-stu-id="52909-134">These transformations can use variables as defined in [Use variables].</span></span>

### <span data-ttu-id="52909-135"><a name="modify-backend-request"></a>Modificar o pedido de back-end Olá</span><span class="sxs-lookup"><span data-stu-id="52909-135"><a name="modify-backend-request"></a>Modify hello back-end request</span></span>

<span data-ttu-id="52909-136">Por predefinição, o pedido de back-end Olá é inicializado como uma cópia do pedido original Olá.</span><span class="sxs-lookup"><span data-stu-id="52909-136">By default, hello back-end request is initialized as a copy of hello original request.</span></span> <span data-ttu-id="52909-137">Além disso toosetting Olá back-end URL, pode efetuar alterações toohello HTTP, cabeçalhos sendo que os parâmetros de cadeia de consulta.</span><span class="sxs-lookup"><span data-stu-id="52909-137">In addition toosetting hello back-end URL, you can make changes toohello HTTP method, headers, and query string parameters.</span></span> <span data-ttu-id="52909-138">Olá modificados valores podem referenciar [definições da aplicação] e [parâmetros do pedido de cliente original Olá].</span><span class="sxs-lookup"><span data-stu-id="52909-138">hello modified values can reference [application settings] and [parameters from hello original client request].</span></span>

<span data-ttu-id="52909-139">Atualmente, não há nenhum experiência do portal para modificar pedidos de back-end.</span><span class="sxs-lookup"><span data-stu-id="52909-139">Currently, there is no portal experience for modifying back-end requests.</span></span> <span data-ttu-id="52909-140">toolearn como tooapply esta capacidade de proxies.json, consulte o artigo [definir um objeto de requestOverrides].</span><span class="sxs-lookup"><span data-stu-id="52909-140">toolearn how tooapply this capability from proxies.json, see [Define a requestOverrides object].</span></span>

### <span data-ttu-id="52909-141"><a name="modify-response"></a>Modificar a resposta Olá</span><span class="sxs-lookup"><span data-stu-id="52909-141"><a name="modify-response"></a>Modify hello response</span></span>

<span data-ttu-id="52909-142">Por predefinição, a resposta do cliente Olá foi inicializada como uma cópia da resposta de back-end Olá.</span><span class="sxs-lookup"><span data-stu-id="52909-142">By default, hello client response is initialized as a copy of hello back-end response.</span></span> <span data-ttu-id="52909-143">Pode efetuar o código de estado de resposta de toohello a alterações, frase de razão, os cabeçalhos e corpo.</span><span class="sxs-lookup"><span data-stu-id="52909-143">You can make changes toohello response's status code, reason phrase, headers, and body.</span></span> <span data-ttu-id="52909-144">Olá modificados valores podem referenciar [definições da aplicação], [parâmetros do pedido de cliente original Olá], e [parâmetros da resposta de back-end Olá].</span><span class="sxs-lookup"><span data-stu-id="52909-144">hello modified values can reference [application settings], [parameters from hello original client request], and [parameters from hello back-end response].</span></span>

<span data-ttu-id="52909-145">Atualmente, não há nenhum experiência do portal para modificar as respostas.</span><span class="sxs-lookup"><span data-stu-id="52909-145">Currently, there is no portal experience for modifying responses.</span></span> <span data-ttu-id="52909-146">toolearn como tooapply esta capacidade de proxies.json, consulte o artigo [definir um objeto de responseOverrides].</span><span class="sxs-lookup"><span data-stu-id="52909-146">toolearn how tooapply this capability from proxies.json, see [Define a responseOverrides object].</span></span>

## <span data-ttu-id="52909-147"><a name="using-variables"></a>Utilizar variáveis</span><span class="sxs-lookup"><span data-stu-id="52909-147"><a name="using-variables"></a>Use variables</span></span>

<span data-ttu-id="52909-148">configuração de Olá para um proxy não precisa de toobe estático.</span><span class="sxs-lookup"><span data-stu-id="52909-148">hello configuration for a proxy does not need toobe static.</span></span> <span data-ttu-id="52909-149">Pode condição-toouse variáveis do pedido original Olá, resposta de back-end Olá ou as definições da aplicação.</span><span class="sxs-lookup"><span data-stu-id="52909-149">You can condition it toouse variables from hello original request, hello back-end response, or application settings.</span></span>

### <span data-ttu-id="52909-150"><a name="request-parameters"></a>Parâmetros do pedido de referência</span><span class="sxs-lookup"><span data-stu-id="52909-150"><a name="request-parameters"></a>Reference request parameters</span></span>

<span data-ttu-id="52909-151">Pode utilizar os parâmetros do pedido como entradas de propriedade de URL de back-end toohello ou como parte de modificar os pedidos e respostas.</span><span class="sxs-lookup"><span data-stu-id="52909-151">You can use request parameters as inputs toohello back-end URL property or as part of modifying requests and responses.</span></span> <span data-ttu-id="52909-152">Alguns parâmetros podem estar vinculados a partir do modelo de rota Olá especificado na configuração de base proxy Olá e outros utilizadores podem ter a partir das propriedades de pedido de entrada Olá.</span><span class="sxs-lookup"><span data-stu-id="52909-152">Some parameters can be bound from hello route template that's specified in hello base proxy configuration, and others can come from properties of hello incoming request.</span></span>

#### <a name="route-template-parameters"></a><span data-ttu-id="52909-153">Parâmetros do modelo de rota</span><span class="sxs-lookup"><span data-stu-id="52909-153">Route template parameters</span></span>
<span data-ttu-id="52909-154">Os parâmetros que são utilizados no modelo de rota Olá se toobe disponível referenciada por nome.</span><span class="sxs-lookup"><span data-stu-id="52909-154">Parameters that are used in hello route template are available toobe referenced by name.</span></span> <span data-ttu-id="52909-155">os nomes dos parâmetros de Olá são colocados entre chavetas ({}).</span><span class="sxs-lookup"><span data-stu-id="52909-155">hello parameter names are enclosed in braces ({}).</span></span>

<span data-ttu-id="52909-156">Por exemplo, se um proxy, tem um modelo de rota, tal como `/pets/{petId}`, Olá URL de back-end pode incluir valor Olá `{petId}`, como no `https://<AnotherApp>.azurewebsites.net/api/pets/{petId}`.</span><span class="sxs-lookup"><span data-stu-id="52909-156">For example, if a proxy has a route template, such as `/pets/{petId}`, hello back-end URL can include hello value of `{petId}`, as in `https://<AnotherApp>.azurewebsites.net/api/pets/{petId}`.</span></span> <span data-ttu-id="52909-157">Se o modelo de rota Olá termina num caráter universal, tais como `/api/{*restOfPath}`, Olá valor `{restOfPath}` é uma representação de cadeia de Olá restantes segmentos de caminho do pedido de entrada Olá.</span><span class="sxs-lookup"><span data-stu-id="52909-157">If hello route template terminates in a wildcard, such as `/api/{*restOfPath}`, hello value `{restOfPath}` is a string representation of hello remaining path segments from hello incoming request.</span></span>

#### <a name="additional-request-parameters"></a><span data-ttu-id="52909-158">Parâmetros do pedido adicionais</span><span class="sxs-lookup"><span data-stu-id="52909-158">Additional request parameters</span></span>
<span data-ttu-id="52909-159">Além disso toohello encaminhar os parâmetros do modelo, Olá os seguintes valores pode ser utilizado em valores de configuração:</span><span class="sxs-lookup"><span data-stu-id="52909-159">In addition toohello route template parameters, hello following values can be used in config values:</span></span>

* <span data-ttu-id="52909-160">**{request.method}** : Olá método HTTP que é utilizado no pedido original Olá.</span><span class="sxs-lookup"><span data-stu-id="52909-160">**{request.method}**: hello HTTP method that's used on hello original request.</span></span>
* <span data-ttu-id="52909-161">**{request.headers. \<HeaderName\>}**: um cabeçalho que pode ser lidos na pedido original Olá.</span><span class="sxs-lookup"><span data-stu-id="52909-161">**{request.headers.\<HeaderName\>}**: A header that can be read from hello original request.</span></span> <span data-ttu-id="52909-162">Substitua  *\<HeaderName\>*  com o nome de Olá de cabeçalho de Olá que pretende que o tooread.</span><span class="sxs-lookup"><span data-stu-id="52909-162">Replace *\<HeaderName\>* with hello name of hello header that you want tooread.</span></span> <span data-ttu-id="52909-163">Se o cabeçalho de Olá não está incluído no pedido de Olá, o valor de Olá será uma cadeia vazia Olá.</span><span class="sxs-lookup"><span data-stu-id="52909-163">If hello header is not included on hello request, hello value will be hello empty string.</span></span>
* <span data-ttu-id="52909-164">**{request.querystring. \<ParameterName\>}**: um parâmetro de cadeia de consulta que pode ser lidos na pedido original Olá.</span><span class="sxs-lookup"><span data-stu-id="52909-164">**{request.querystring.\<ParameterName\>}**: A query string parameter that can be read from hello original request.</span></span> <span data-ttu-id="52909-165">Substitua  *\<ParameterName\>*  com o nome de Olá do parâmetro de Olá que pretende que o tooread.</span><span class="sxs-lookup"><span data-stu-id="52909-165">Replace *\<ParameterName\>* with hello name of hello parameter that you want tooread.</span></span> <span data-ttu-id="52909-166">Se o parâmetro de Olá não está incluído no pedido de Olá, o valor de Olá será uma cadeia vazia Olá.</span><span class="sxs-lookup"><span data-stu-id="52909-166">If hello parameter is not included on hello request, hello value will be hello empty string.</span></span>

### <span data-ttu-id="52909-167"><a name="response-parameters"></a>Parâmetros de resposta de back-end de referência</span><span class="sxs-lookup"><span data-stu-id="52909-167"><a name="response-parameters"></a>Reference back-end response parameters</span></span>

<span data-ttu-id="52909-168">Parâmetros de resposta podem ser utilizados como parte de modificação de cliente de toohello Olá resposta.</span><span class="sxs-lookup"><span data-stu-id="52909-168">Response parameters can be used as part of modifying hello response toohello client.</span></span> <span data-ttu-id="52909-169">Olá, os seguintes valores pode ser utilizado valores de configuração:</span><span class="sxs-lookup"><span data-stu-id="52909-169">hello following values can be used in config values:</span></span>

* <span data-ttu-id="52909-170">**{backend.response.statusCode}** : Olá código de estado HTTP que é devolvido numa resposta de back-end Olá.</span><span class="sxs-lookup"><span data-stu-id="52909-170">**{backend.response.statusCode}**: hello HTTP status code that's returned on hello back-end response.</span></span>
* <span data-ttu-id="52909-171">**{backend.response.statusReason}** : frase de razão Olá HTTP, que é devolvido numa resposta de back-end Olá.</span><span class="sxs-lookup"><span data-stu-id="52909-171">**{backend.response.statusReason}**: hello HTTP reason phrase that's returned on hello back-end response.</span></span>
* <span data-ttu-id="52909-172">**{backend.response.headers. \<HeaderName\>}**: um cabeçalho que pode ser lidos na resposta do Olá back-end.</span><span class="sxs-lookup"><span data-stu-id="52909-172">**{backend.response.headers.\<HeaderName\>}**: A header that can be read from hello back-end response.</span></span> <span data-ttu-id="52909-173">Substitua  *\<HeaderName\>*  com o nome de Olá de cabeçalho de Olá pretende tooread.</span><span class="sxs-lookup"><span data-stu-id="52909-173">Replace *\<HeaderName\>* with hello name of hello header you want tooread.</span></span> <span data-ttu-id="52909-174">Se o cabeçalho de Olá não está incluído no pedido de Olá, o valor de Olá será uma cadeia vazia Olá.</span><span class="sxs-lookup"><span data-stu-id="52909-174">If hello header is not included on hello request, hello value will be hello empty string.</span></span>

### <span data-ttu-id="52909-175"><a name="use-appsettings"></a>Definições da aplicação de referência</span><span class="sxs-lookup"><span data-stu-id="52909-175"><a name="use-appsettings"></a>Reference application settings</span></span>

<span data-ttu-id="52909-176">Também pode referenciar [definições da aplicação definidas para a aplicação de função Olá](https://docs.microsoft.com/azure/azure-functions/functions-how-to-use-azure-function-app-settings#develop) por envolvente nome da definição Olá com sinais de percentagem (%).</span><span class="sxs-lookup"><span data-stu-id="52909-176">You can also reference [application settings defined for hello function app](https://docs.microsoft.com/azure/azure-functions/functions-how-to-use-azure-function-app-settings#develop) by surrounding hello setting name with percent signs (%).</span></span>

<span data-ttu-id="52909-177">Por exemplo, um URL de back-end de *https://%ORDER_PROCESSING_HOST%/api/orders* teria aos "% ORDER_PROCESSING_HOST %" substituída pelo valor Olá da definição de ORDER_PROCESSING_HOST Olá.</span><span class="sxs-lookup"><span data-stu-id="52909-177">For example, a back-end URL of *https://%ORDER_PROCESSING_HOST%/api/orders* would have "%ORDER_PROCESSING_HOST%" replaced with hello value of hello ORDER_PROCESSING_HOST setting.</span></span>

> [!TIP] 
> <span data-ttu-id="52909-178">Utilize as definições da aplicação para os anfitriões de back-end, se tiver múltiplas implementações ou ambientes de teste.</span><span class="sxs-lookup"><span data-stu-id="52909-178">Use application settings for back-end hosts when you have multiple deployments or test environments.</span></span> <span data-ttu-id="52909-179">Dessa forma, pode certificar-se que sempre estamos a falar toohello direito novamente terminar nesse ambiente.</span><span class="sxs-lookup"><span data-stu-id="52909-179">That way, you can make sure that you are always talking toohello right back end for that environment.</span></span>

## <a name="advanced-configuration"></a><span data-ttu-id="52909-180">Configuração avançada</span><span class="sxs-lookup"><span data-stu-id="52909-180">Advanced configuration</span></span>

<span data-ttu-id="52909-181">proxies de Olá configuradas por si são armazenados num ficheiro proxies.json, que está localizado na raiz de Olá de um diretório de aplicação de função.</span><span class="sxs-lookup"><span data-stu-id="52909-181">hello proxies that you configure are stored in a proxies.json file, which is located in hello root of a function app directory.</span></span> <span data-ttu-id="52909-182">Pode editar este ficheiro manualmente e implementá-lo como parte da sua aplicação quando utilizar qualquer um dos Olá [métodos de implementação](https://docs.microsoft.com/azure/azure-functions/functions-continuous-deployment) que suporta as funções.</span><span class="sxs-lookup"><span data-stu-id="52909-182">You can manually edit this file and deploy it as part of your app when you use any of hello [deployment methods](https://docs.microsoft.com/azure/azure-functions/functions-continuous-deployment) that Functions supports.</span></span> <span data-ttu-id="52909-183">funcionalidade de Olá tem de ser [ativada](#enable) para Olá ficheiro toobe processado.</span><span class="sxs-lookup"><span data-stu-id="52909-183">hello feature must be [enabled](#enable) for hello file toobe processed.</span></span> 

> [!TIP] 
> <span data-ttu-id="52909-184">Se não configurou um dos métodos de implementação de Olá, também pode trabalhar com o ficheiro de proxies.json Olá no portal de Olá.</span><span class="sxs-lookup"><span data-stu-id="52909-184">If you have not set up one of hello deployment methods, you can also work with hello proxies.json file in hello portal.</span></span> <span data-ttu-id="52909-185">Aplicação de função tooyour aceda, selecione **funcionalidades da plataforma**e, em seguida, selecione **Editor do serviço de aplicações**.</span><span class="sxs-lookup"><span data-stu-id="52909-185">Go tooyour function app, select **Platform features**, and then select **App Service Editor**.</span></span> <span data-ttu-id="52909-186">Ao fazê-lo, pode ver a estrutura de Olá de ficheiro completo da sua aplicação de função e, em seguida, efetuar alterações.</span><span class="sxs-lookup"><span data-stu-id="52909-186">By doing so, you can view hello entire file structure of your function app and then make changes.</span></span>

<span data-ttu-id="52909-187">Proxies.JSON é definido por um objeto de proxies, que é composto por proxies com nome e as respetivas definições.</span><span class="sxs-lookup"><span data-stu-id="52909-187">Proxies.json is defined by a proxies object, which is composed of named proxies and their definitions.</span></span> <span data-ttu-id="52909-188">Opcionalmente, se o seu editor de o suportar, pode referenciar um [esquema JSON](http://json.schemastore.org/proxies) para conclusão de código.</span><span class="sxs-lookup"><span data-stu-id="52909-188">Optionally, if your editor supports it, you can reference a [JSON schema](http://json.schemastore.org/proxies) for code completion.</span></span> <span data-ttu-id="52909-189">Um ficheiro de exemplo aspeto que poderá ter Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="52909-189">An example file might look like hello following:</span></span>

```json
{
    "$schema": "http://json.schemastore.org/proxies",
    "proxies": {
        "proxy1": {
            "matchCondition": {
                "methods": [ "GET" ],
                "route": "/api/{test}"
            },
            "backendUri": "https://<AnotherApp>.azurewebsites.net/api/<FunctionName>"
        }
    }
}
```

<span data-ttu-id="52909-190">Cada proxy tem um nome amigável, tais como *proxy1* no Olá anterior exemplo.</span><span class="sxs-lookup"><span data-stu-id="52909-190">Each proxy has a friendly name, such as *proxy1* in hello preceding example.</span></span> <span data-ttu-id="52909-191">objeto de definição de proxy Olá correspondente é definido pela Olá seguintes propriedades:</span><span class="sxs-lookup"><span data-stu-id="52909-191">hello corresponding proxy definition object is defined by hello following properties:</span></span>

* <span data-ttu-id="52909-192">**matchCondition**: necessário – um objeto definir pedidos de Olá acionam a execução de Olá deste proxy.</span><span class="sxs-lookup"><span data-stu-id="52909-192">**matchCondition**: Required--an object defining hello requests that trigger hello execution of this proxy.</span></span> <span data-ttu-id="52909-193">Contém duas propriedades que são partilhadas com [HTTP acionadores]:</span><span class="sxs-lookup"><span data-stu-id="52909-193">It contains two properties that are shared with [HTTP triggers]:</span></span>
    * <span data-ttu-id="52909-194">_métodos_: uma matriz de métodos de Olá HTTP Olá proxy responde a.</span><span class="sxs-lookup"><span data-stu-id="52909-194">_methods_: An array of hello HTTP methods that hello proxy responds to.</span></span> <span data-ttu-id="52909-195">Se não for especificado, o proxy de Olá responde tooall métodos de HTTP na rota Olá.</span><span class="sxs-lookup"><span data-stu-id="52909-195">If it is not specified, hello proxy responds tooall HTTP methods on hello route.</span></span>
    * <span data-ttu-id="52909-196">_rota_: necessário – define o modelo de rota Olá, controlar qual pedido URLs o proxy responde a.</span><span class="sxs-lookup"><span data-stu-id="52909-196">_route_: Required--defines hello route template, controlling which request URLs your proxy responds to.</span></span> <span data-ttu-id="52909-197">Ao contrário no acionadores HTTP, não há nenhum valor predefinido.</span><span class="sxs-lookup"><span data-stu-id="52909-197">Unlike in HTTP triggers, there is no default value.</span></span>
* <span data-ttu-id="52909-198">**backendUri**: Olá URL do pedido de Olá Olá recursos de back-end toowhich deve ser efetuado.</span><span class="sxs-lookup"><span data-stu-id="52909-198">**backendUri**: hello URL of hello back-end resource toowhich hello request should be proxied.</span></span> <span data-ttu-id="52909-199">Este valor pode referenciar as definições da aplicação e os parâmetros do pedido de cliente Olá original.</span><span class="sxs-lookup"><span data-stu-id="52909-199">This value can reference application settings and parameters from hello original client request.</span></span> <span data-ttu-id="52909-200">Se esta propriedade não for incluída, as funções do Azure responde com uma HTTP 200 OK.</span><span class="sxs-lookup"><span data-stu-id="52909-200">If this property is not included, Azure Functions responds with an HTTP 200 OK.</span></span>
* <span data-ttu-id="52909-201">**requestOverrides**: um objeto que define o pedido de back-end de toohello transformações.</span><span class="sxs-lookup"><span data-stu-id="52909-201">**requestOverrides**: An object that defines transformations toohello back-end request.</span></span> <span data-ttu-id="52909-202">Consulte [definir um objeto de requestOverrides].</span><span class="sxs-lookup"><span data-stu-id="52909-202">See [Define a requestOverrides object].</span></span>
* <span data-ttu-id="52909-203">**responseOverrides**: um objeto que define a resposta de cliente de toohello transformações.</span><span class="sxs-lookup"><span data-stu-id="52909-203">**responseOverrides**: An object that defines transformations toohello client response.</span></span> <span data-ttu-id="52909-204">Consulte [definir um objeto de responseOverrides].</span><span class="sxs-lookup"><span data-stu-id="52909-204">See [Define a responseOverrides object].</span></span>

> [!NOTE] 
> <span data-ttu-id="52909-205">propriedade de rota Olá Proxies de funções do Azure não honrar a propriedade de routePrefix Olá da configuração do anfitrião Olá funções.</span><span class="sxs-lookup"><span data-stu-id="52909-205">hello route property Azure Functions Proxies does not honor hello routePrefix property of hello Functions host configuration.</span></span> <span data-ttu-id="52909-206">Se quiser tooinclude um prefixo como /api, tem de ser incluído na propriedade de rota Olá.</span><span class="sxs-lookup"><span data-stu-id="52909-206">If you want tooinclude a prefix such as /api, it must be included in hello route property.</span></span>

### <span data-ttu-id="52909-207"><a name="requestOverrides"></a>Definir um objeto de requestOverrides</span><span class="sxs-lookup"><span data-stu-id="52909-207"><a name="requestOverrides"></a>Define a requestOverrides object</span></span>

<span data-ttu-id="52909-208">objeto de requestOverrides Olá define as alterações efetuadas toohello pedido quando recursos de back-end Olá é chamado.</span><span class="sxs-lookup"><span data-stu-id="52909-208">hello requestOverrides object defines changes made toohello request when hello back-end resource is called.</span></span> <span data-ttu-id="52909-209">objeto de Olá é definido pela Olá seguintes propriedades:</span><span class="sxs-lookup"><span data-stu-id="52909-209">hello object is defined by hello following properties:</span></span>

* <span data-ttu-id="52909-210">**backend.Request.Method**: Olá método HTTP que foi utilizado toocall Olá de back-end.</span><span class="sxs-lookup"><span data-stu-id="52909-210">**backend.request.method**: hello HTTP method that's used toocall hello back end.</span></span>
* <span data-ttu-id="52909-211">**backend.Request.QueryString. \<ParameterName\>**: um parâmetro de cadeia de consulta que pode ser definido para Olá chamada toohello de back-end.</span><span class="sxs-lookup"><span data-stu-id="52909-211">**backend.request.querystring.\<ParameterName\>**: A query string parameter that can be set for hello call toohello back end.</span></span> <span data-ttu-id="52909-212">Substitua  *\<ParameterName\>*  com o nome de Olá do parâmetro de Olá que pretende que o tooset.</span><span class="sxs-lookup"><span data-stu-id="52909-212">Replace *\<ParameterName\>* with hello name of hello parameter that you want tooset.</span></span> <span data-ttu-id="52909-213">Se for fornecida uma cadeia vazia Olá parâmetro Olá não está incluído no pedido de back-end Olá.</span><span class="sxs-lookup"><span data-stu-id="52909-213">If hello empty string is provided, hello parameter is not included on hello back-end request.</span></span>
* <span data-ttu-id="52909-214">**backend.Request.Headers. \<HeaderName\>**: um cabeçalho que pode ser definido para Olá chamada toohello de back-end.</span><span class="sxs-lookup"><span data-stu-id="52909-214">**backend.request.headers.\<HeaderName\>**: A header that can be set for hello call toohello back end.</span></span> <span data-ttu-id="52909-215">Substitua  *\<HeaderName\>*  com o nome de Olá de cabeçalho de Olá que pretende que o tooset.</span><span class="sxs-lookup"><span data-stu-id="52909-215">Replace *\<HeaderName\>* with hello name of hello header that you want tooset.</span></span> <span data-ttu-id="52909-216">Se fornecer uma cadeia vazia Olá, cabeçalho Olá não está incluído no pedido de back-end Olá.</span><span class="sxs-lookup"><span data-stu-id="52909-216">If you provide hello empty string, hello header is not included on hello back-end request.</span></span>

<span data-ttu-id="52909-217">Valores podem referenciar as definições da aplicação e os parâmetros do pedido de cliente Olá original.</span><span class="sxs-lookup"><span data-stu-id="52909-217">Values can reference application settings and parameters from hello original client request.</span></span>

<span data-ttu-id="52909-218">Um exemplo de configuração aspeto que poderá ter Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="52909-218">An example configuration might look like hello following:</span></span>

```json
{
    "$schema": "http://json.schemastore.org/proxies",
    "proxies": {
        "proxy1": {
            "matchCondition": {
                "methods": [ "GET" ],
                "route": "/api/{test}"
            },
            "backendUri": "https://<AnotherApp>.azurewebsites.net/api/<FunctionName>",
            "requestOverrides": {
                "backend.request.headers.Accept": "application/xml",
                "backend.request.headers.x-functions-key": "%ANOTHERAPP_API_KEY%"
            }
        }
    }
}
```

### <span data-ttu-id="52909-219"><a name="responseOverrides"></a>Definir um objeto de responseOverrides</span><span class="sxs-lookup"><span data-stu-id="52909-219"><a name="responseOverrides"></a>Define a responseOverrides object</span></span>

<span data-ttu-id="52909-220">objeto de requestOverrides Olá define as alterações efetuadas toohello resposta que passou toohello back-cliente.</span><span class="sxs-lookup"><span data-stu-id="52909-220">hello requestOverrides object defines changes that are made toohello response that's passed back toohello client.</span></span> <span data-ttu-id="52909-221">objeto de Olá é definido pela Olá seguintes propriedades:</span><span class="sxs-lookup"><span data-stu-id="52909-221">hello object is defined by hello following properties:</span></span>

* <span data-ttu-id="52909-222">**response.statusCode**: toobe de código de estado de Olá HTTP devolvido toohello cliente.</span><span class="sxs-lookup"><span data-stu-id="52909-222">**response.statusCode**: hello HTTP status code toobe returned toohello client.</span></span>
* <span data-ttu-id="52909-223">**response.statusReason**: toobe de frase de razão Olá HTTP devolvido toohello cliente.</span><span class="sxs-lookup"><span data-stu-id="52909-223">**response.statusReason**: hello HTTP reason phrase toobe returned toohello client.</span></span>
* <span data-ttu-id="52909-224">**Response.body**: representação de cadeia Olá de Olá corpo toobe devolvido toohello cliente.</span><span class="sxs-lookup"><span data-stu-id="52909-224">**response.body**: hello string representation of hello body toobe returned toohello client.</span></span>
* <span data-ttu-id="52909-225">**Response.Headers. \<HeaderName\>**: um cabeçalho que pode ser definido para o cliente de toohello Olá resposta.</span><span class="sxs-lookup"><span data-stu-id="52909-225">**response.headers.\<HeaderName\>**: A header that can be set for hello response toohello client.</span></span> <span data-ttu-id="52909-226">Substitua  *\<HeaderName\>*  com o nome de Olá de cabeçalho de Olá que pretende que o tooset.</span><span class="sxs-lookup"><span data-stu-id="52909-226">Replace *\<HeaderName\>* with hello name of hello header that you want tooset.</span></span> <span data-ttu-id="52909-227">Se fornecer uma cadeia vazia Olá, o cabeçalho de Olá não está incluído na resposta Olá.</span><span class="sxs-lookup"><span data-stu-id="52909-227">If you provide hello empty string, hello header is not included on hello response.</span></span>

<span data-ttu-id="52909-228">Valores podem referenciar as definições da aplicação, parâmetros do pedido de cliente original Olá e os parâmetros da resposta de back-end Olá.</span><span class="sxs-lookup"><span data-stu-id="52909-228">Values can reference application settings, parameters from hello original client request, and parameters from hello back-end response.</span></span>

<span data-ttu-id="52909-229">Um exemplo de configuração aspeto que poderá ter Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="52909-229">An example configuration might look like hello following:</span></span>

```json
{
    "$schema": "http://json.schemastore.org/proxies",
    "proxies": {
        "proxy1": {
            "matchCondition": {
                "methods": [ "GET" ],
                "route": "/api/{test}"
            },
            "responseOverrides": {
                "response.body": "Hello, {test}",
                "response.headers.Content-Type": "text/plain"
            }
        }
    }
}
```
> [!NOTE] 
> <span data-ttu-id="52909-230">Neste exemplo, corpo Olá está a ser definido diretamente, por isso, não `backendUri` propriedade é necessária.</span><span class="sxs-lookup"><span data-stu-id="52909-230">In this example, hello body is being set directly, so no `backendUri` property is needed.</span></span> <span data-ttu-id="52909-231">exemplo de Olá mostra como pode utilizar os Proxies de funções do Azure para mocking APIs.</span><span class="sxs-lookup"><span data-stu-id="52909-231">hello example shows how you might use Azure Functions Proxies for mocking APIs.</span></span>

[portal do Azure]: https://portal.azure.com
[HTTP acionadores]: https://docs.microsoft.com/azure/azure-functions/functions-bindings-http-webhook#http-trigger
[Modify hello back-end request]: #modify-backend-request
[Modify hello response]: #modify-response
[definir um objeto de requestOverrides]: #requestOverrides
[definir um objeto de responseOverrides]: #responseOverrides
[definições da aplicação]: #use-appsettings
[utilizar variáveis]: #using-variables
[parâmetros do pedido de cliente original Olá]: #request-parameters
[parâmetros da resposta de back-end Olá]: #response-parameters
