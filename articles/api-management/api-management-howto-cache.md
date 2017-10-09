---
title: "aaaAdd colocação em cache tooimprove desempenho na API Management do Azure | Microsoft Docs"
description: "Saiba como carregar a latência de Olá tooimprove, o consumo de largura de banda e o serviço web para chamadas de serviço de API Management."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 740f6a27-8323-474d-ade2-828ae0c75e7a
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 056ab7cf788218327e30bd5c028b76e3b1977fb0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="add-caching-tooimprove-performance-in-azure-api-management"></a><span data-ttu-id="ed0ee-103">Adicionar a colocação em cache tooimprove desempenho na API Management do Azure</span><span class="sxs-lookup"><span data-stu-id="ed0ee-103">Add caching tooimprove performance in Azure API Management</span></span>
<span data-ttu-id="ed0ee-104">É possível configurar as operações da API Management para colocar as respostas em cache.</span><span class="sxs-lookup"><span data-stu-id="ed0ee-104">Operations in API Management can be configured for response caching.</span></span> <span data-ttu-id="ed0ee-105">A colocação de respostas em cache pode reduzir significativamente a latência da API, o consumo de largura de banda e a carga do serviço Web para os dados que não são alterados com frequência.</span><span class="sxs-lookup"><span data-stu-id="ed0ee-105">Response caching can significantly reduce API latency, bandwidth consumption, and web service load for data that does not change frequently.</span></span>

<span data-ttu-id="ed0ee-106">Este guia mostra como resposta tooadd colocação em cache para a API e configurar políticas para as operações de API eco de exemplo de Olá.</span><span class="sxs-lookup"><span data-stu-id="ed0ee-106">This guide shows you how tooadd response caching for your API and configure policies for hello sample Echo API operations.</span></span> <span data-ttu-id="ed0ee-107">Em seguida, pode chamar a operação a Olá de Olá programador portal tooverify em cache em ação.</span><span class="sxs-lookup"><span data-stu-id="ed0ee-107">You can then call hello operation from hello developer portal tooverify caching in action.</span></span>

> [!NOTE]
> <span data-ttu-id="ed0ee-108">Para obter informações sobre a colocação em cache de itens por chave utilizando expressões de política, consulte [Colocação em cache personalizada na API Management do Azure](api-management-sample-cache-by-key.md).</span><span class="sxs-lookup"><span data-stu-id="ed0ee-108">For information on caching items by key using policy expressions, see [Custom caching in Azure API Management](api-management-sample-cache-by-key.md).</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="ed0ee-109">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="ed0ee-109">Prerequisites</span></span>
<span data-ttu-id="ed0ee-110">Passos seguinte Olá neste guia, tem de ter uma instância de serviço de API Management com uma API e um produto configurado.</span><span class="sxs-lookup"><span data-stu-id="ed0ee-110">Before following hello steps in this guide, you must have an API Management service instance with an API and a product configured.</span></span> <span data-ttu-id="ed0ee-111">Se ainda não criou uma instância de serviço de API Management, consulte [criar uma instância de serviço de API Management] [ Create an API Management service instance] no Olá [introdução à API Management do Azure] [ Get started with Azure API Management] tutorial.</span><span class="sxs-lookup"><span data-stu-id="ed0ee-111">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in hello [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>

## <span data-ttu-id="ed0ee-112"><a name="configure-caching"> </a>Configurar uma operação para colocação em cache</span><span class="sxs-lookup"><span data-stu-id="ed0ee-112"><a name="configure-caching"> </a>Configure an operation for caching</span></span>
<span data-ttu-id="ed0ee-113">Neste passo, irá rever Olá colocação em cache as definições de Olá **recurso GET (em cache)** operação de exemplo de Olá API eco.</span><span class="sxs-lookup"><span data-stu-id="ed0ee-113">In this step, you will review hello caching settings of hello **GET Resource (cached)** operation of hello sample Echo API.</span></span>

> [!NOTE]
> <span data-ttu-id="ed0ee-114">Cada instância de serviço de API Management está pré-configurada com uma API eco que pode ser utilizado tooexperiment com e saber mais sobre a API Management.</span><span class="sxs-lookup"><span data-stu-id="ed0ee-114">Each API Management service instance comes preconfigured with an Echo API that can be used tooexperiment with and learn about API Management.</span></span> <span data-ttu-id="ed0ee-115">Para obter mais informações, consulte [Introdução à Gestão de API do Azure][Get started with Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="ed0ee-115">For more information, see [Get started with Azure API Management][Get started with Azure API Management].</span></span>
> 
> 

<span data-ttu-id="ed0ee-116">tooget iniciado, clique em **portal do publicador** no Olá Portal do Azure para o seu serviço de API Management.</span><span class="sxs-lookup"><span data-stu-id="ed0ee-116">tooget started, click **Publisher portal** in hello Azure Portal for your API Management service.</span></span> <span data-ttu-id="ed0ee-117">Isto leva-o portal do publicador da API Management toohello.</span><span class="sxs-lookup"><span data-stu-id="ed0ee-117">This takes you toohello API Management publisher portal.</span></span>

![Portal do publicador][api-management-management-console]

<span data-ttu-id="ed0ee-119">Clique em **APIs** de Olá **API Management** menu Olá à esquerda e, em seguida, clique em **API eco**.</span><span class="sxs-lookup"><span data-stu-id="ed0ee-119">Click **APIs** from hello **API Management** menu on hello left, and then click **Echo API**.</span></span>

![API Eco][api-management-echo-api]

<span data-ttu-id="ed0ee-121">Clique em Olá **operações** separador e, em seguida, clique em Olá **recurso GET (em cache)** operação a partir da Olá **operações** lista.</span><span class="sxs-lookup"><span data-stu-id="ed0ee-121">Click hello **Operations** tab, and then click hello **GET Resource (cached)** operation from hello **Operations** list.</span></span>

![Operações da API Eco][api-management-echo-api-operations]

<span data-ttu-id="ed0ee-123">Clique em Olá **colocação em cache** Olá tooview de separador colocação em cache as definições para esta operação.</span><span class="sxs-lookup"><span data-stu-id="ed0ee-123">Click hello **Caching** tab tooview hello caching settings for this operation.</span></span>

![Separador Colocação em cache][api-management-caching-tab]

<span data-ttu-id="ed0ee-125">tooenable colocação em cache para uma operação, selecione de Olá **ativar** caixa de verificação.</span><span class="sxs-lookup"><span data-stu-id="ed0ee-125">tooenable caching for an operation, select hello **Enable** check box.</span></span> <span data-ttu-id="ed0ee-126">Neste exemplo, a colocação em cache está ativada.</span><span class="sxs-lookup"><span data-stu-id="ed0ee-126">In this example, caching is enabled.</span></span>

<span data-ttu-id="ed0ee-127">Cada resposta da operação é codificada, com base nos valores de Olá no Olá **variação por parâmetros de cadeia de consulta** e **variação por cabeçalhos** campos.</span><span class="sxs-lookup"><span data-stu-id="ed0ee-127">Each operation response is keyed, based on hello values in hello **Vary by query string parameters** and **Vary by headers** fields.</span></span> <span data-ttu-id="ed0ee-128">Se quiser toocache várias respostas com base nos parâmetros de cadeia de consulta ou nos cabeçalhos, pode configurá-las nestes dois campos.</span><span class="sxs-lookup"><span data-stu-id="ed0ee-128">If you want toocache multiple responses based on query string parameters or headers, you can configure them in these two fields.</span></span>

<span data-ttu-id="ed0ee-129">**Duração** Especifica o intervalo de expiração de Olá das respostas hello em cache.</span><span class="sxs-lookup"><span data-stu-id="ed0ee-129">**Duration** specifies hello expiration interval of hello cached responses.</span></span> <span data-ttu-id="ed0ee-130">Neste exemplo, o intervalo de Olá é **3600** segundos, que é equivalente tooone hora.</span><span class="sxs-lookup"><span data-stu-id="ed0ee-130">In this example, hello interval is **3600** seconds, which is equivalent tooone hour.</span></span>

<span data-ttu-id="ed0ee-131">Utilizar a colocação em cache de configuração neste exemplo de Olá, Olá primeiro pedido toohello **recurso GET (em cache)** operação devolve uma resposta do serviço de back-end Olá.</span><span class="sxs-lookup"><span data-stu-id="ed0ee-131">Using hello caching configuration in this example, hello first request toohello **GET Resource (cached)** operation returns a response from hello backend service.</span></span> <span data-ttu-id="ed0ee-132">Esta resposta serão colocadas em cache, codificada por Olá especificado parâmetros de cadeia de consulta e de cabeçalhos.</span><span class="sxs-lookup"><span data-stu-id="ed0ee-132">This response will be cached, keyed by hello specified headers and query string parameters.</span></span> <span data-ttu-id="ed0ee-133">As chamadas subsequentes operação toohello, com correspondentes aos parâmetros, terá de Olá colocadas em cache resposta devolvida, até que o intervalo de duração da cache Olá expirou.</span><span class="sxs-lookup"><span data-stu-id="ed0ee-133">Subsequent calls toohello operation, with matching parameters, will have hello cached response returned, until hello cache duration interval has expired.</span></span>

## <span data-ttu-id="ed0ee-134"><a name="caching-policies"></a>Olá de rever as políticas de colocação em cache</span><span class="sxs-lookup"><span data-stu-id="ed0ee-134"><a name="caching-policies"> </a>Review hello caching policies</span></span>
<span data-ttu-id="ed0ee-135">Neste passo, consulte Olá colocação em cache as definições de Olá **recurso GET (em cache)** operação de exemplo de Olá API eco.</span><span class="sxs-lookup"><span data-stu-id="ed0ee-135">In this step, you review hello caching settings for hello **GET Resource (cached)** operation of hello sample Echo API.</span></span>

<span data-ttu-id="ed0ee-136">Quando as definições de colocação em cache são configuradas para uma operação no Olá **colocação em cache** separador colocação em cache as políticas são adicionadas para a operação de Olá.</span><span class="sxs-lookup"><span data-stu-id="ed0ee-136">When caching settings are configured for an operation on hello **Caching** tab, caching policies are added for hello operation.</span></span> <span data-ttu-id="ed0ee-137">Estas políticas podem ser visualizadas e editá-lo no editor de políticas de Olá.</span><span class="sxs-lookup"><span data-stu-id="ed0ee-137">These policies can be viewed and edited in hello policy editor.</span></span>

<span data-ttu-id="ed0ee-138">Clique em **políticas** de Olá **API Management** menu Olá esquerda e, em seguida, selecione **API eco / recurso (em cache) GET** de Olá **operação**na lista pendente.</span><span class="sxs-lookup"><span data-stu-id="ed0ee-138">Click **Policies** from hello **API Management** menu on hello left, and then select **Echo API / GET Resource (cached)** from hello **Operation** drop-down list.</span></span>

![Operação de âmbito da política][api-management-operation-dropdown]

<span data-ttu-id="ed0ee-140">Esta ação apresenta as políticas de Olá para esta operação no editor de políticas de Olá.</span><span class="sxs-lookup"><span data-stu-id="ed0ee-140">This displays hello policies for this operation in hello policy editor.</span></span>

![Editor de políticas da API Management][api-management-policy-editor]

<span data-ttu-id="ed0ee-142">definição de política de Olá para esta operação inclui Olá as políticas que definem Olá configuração de colocação em cache que foram revistas utilizando Olá **colocação em cache** separador no passo anterior Olá.</span><span class="sxs-lookup"><span data-stu-id="ed0ee-142">hello policy definition for this operation includes hello policies that define hello caching configuration that were reviewed using hello **Caching** tab in hello previous step.</span></span>

```xml
<policies>
    <inbound>
        <base />
        <cache-lookup vary-by-developer="false" vary-by-developer-groups="false">
            <vary-by-header>Accept</vary-by-header>
            <vary-by-header>Accept-Charset</vary-by-header>
        </cache-lookup>
        <rewrite-uri template="/resource" />
    </inbound>
    <outbound>
        <base />
        <cache-store caching-mode="cache-on" duration="3600" />
    </outbound>
</policies>
```

> [!NOTE]
> <span data-ttu-id="ed0ee-143">Toohello as alterações efetuadas políticas no editor de políticas de Olá a colocação em cache será refletido na Olá **colocação em cache** separador de uma operação e vice-versa.</span><span class="sxs-lookup"><span data-stu-id="ed0ee-143">Changes made toohello caching policies in hello policy editor will be reflected on hello **Caching** tab of an operation, and vice-versa.</span></span>
> 
> 

## <span data-ttu-id="ed0ee-144"><a name="test-operation"></a>Chamar uma operação e testar Olá colocação em cache</span><span class="sxs-lookup"><span data-stu-id="ed0ee-144"><a name="test-operation"> </a>Call an operation and test hello caching</span></span>
<span data-ttu-id="ed0ee-145">Olá toosee colocação em cache em ação, podemos chamar a operação de Olá partir do portal de programador Olá.</span><span class="sxs-lookup"><span data-stu-id="ed0ee-145">toosee hello caching in action, we can call hello operation from hello developer portal.</span></span> <span data-ttu-id="ed0ee-146">Clique em **portal do programador** no menu superior direito Olá.</span><span class="sxs-lookup"><span data-stu-id="ed0ee-146">Click **Developer portal** in hello top right menu.</span></span>

![Portal do programador][api-management-developer-portal-menu]

<span data-ttu-id="ed0ee-148">Clique em **APIs** no Olá menu superior e, em seguida, selecione **API eco**.</span><span class="sxs-lookup"><span data-stu-id="ed0ee-148">Click **APIs** in hello top menu, and then select **Echo API**.</span></span>

![API Eco][api-management-apis-echo-api]

> <span data-ttu-id="ed0ee-150">Se tiver apenas uma API configurada ou visível tooyour conta, em seguida, clicar em APIs leva-o diretamente toohello operações dessa API.</span><span class="sxs-lookup"><span data-stu-id="ed0ee-150">If you have only one API configured or visible tooyour account, then clicking APIs takes you directly toohello operations for that API.</span></span>
> 
> 

<span data-ttu-id="ed0ee-151">Selecione Olá **recurso GET (em cache)** operação e, em seguida, clique em **abrir a consola**.</span><span class="sxs-lookup"><span data-stu-id="ed0ee-151">Select hello **GET Resource (cached)** operation, and then click **Open Console**.</span></span>

![Abrir consola][api-management-open-console]

<span data-ttu-id="ed0ee-153">consola de Olá permite-lhe tooinvoke operações diretamente a partir do portal do programador Olá.</span><span class="sxs-lookup"><span data-stu-id="ed0ee-153">hello console allows you tooinvoke operations directly from hello developer portal.</span></span>

![Consola][api-management-console]

<span data-ttu-id="ed0ee-155">Mantenha os valores predefinidos de Olá para **param1** e **param2**.</span><span class="sxs-lookup"><span data-stu-id="ed0ee-155">Keep hello default values for **param1** and **param2**.</span></span>

<span data-ttu-id="ed0ee-156">Selecione Olá chave pretendida Olá **chave de subscrição** na lista pendente.</span><span class="sxs-lookup"><span data-stu-id="ed0ee-156">Select hello desired key from hello **subscription-key** drop-down list.</span></span> <span data-ttu-id="ed0ee-157">Se a sua conta tiver apenas uma subscrição, esta já estará selecionada.</span><span class="sxs-lookup"><span data-stu-id="ed0ee-157">If your account has only one subscription, it will already be selected.</span></span>

<span data-ttu-id="ed0ee-158">Introduza **sampleheader: value1** no Olá **cabeçalhos de pedido** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="ed0ee-158">Enter **sampleheader:value1** in hello **Request headers** text box.</span></span>

<span data-ttu-id="ed0ee-159">Clique em **HTTP Get** e tome nota do Olá cabeçalhos de resposta.</span><span class="sxs-lookup"><span data-stu-id="ed0ee-159">Click **HTTP Get** and make a note of hello response headers.</span></span>

<span data-ttu-id="ed0ee-160">Introduza **sampleheader: value2** no Olá **cabeçalhos de pedido** caixa de texto e, em seguida, clique em **HTTP Get**.</span><span class="sxs-lookup"><span data-stu-id="ed0ee-160">Enter **sampleheader:value2** in hello **Request headers** text box, and then click **HTTP Get**.</span></span>

<span data-ttu-id="ed0ee-161">Tenha em atenção que o valor de Olá **sampleheader** ainda **value1** na resposta Olá.</span><span class="sxs-lookup"><span data-stu-id="ed0ee-161">Note that hello value of **sampleheader** is still **value1** in hello response.</span></span> <span data-ttu-id="ed0ee-162">Experimente alguns valores diferentes e tenha em atenção que Olá resposta em cache da primeira chamada de Olá é devolvida.</span><span class="sxs-lookup"><span data-stu-id="ed0ee-162">Try some different values and note that hello cached response from hello first call is returned.</span></span>

<span data-ttu-id="ed0ee-163">Introduza **25** para Olá **param2** campo e, em seguida, clique em **HTTP Get**.</span><span class="sxs-lookup"><span data-stu-id="ed0ee-163">Enter **25** into hello **param2** field, and then click **HTTP Get**.</span></span>

<span data-ttu-id="ed0ee-164">Tenha em atenção que o valor de Olá **sampleheader** Olá resposta é agora **value2**.</span><span class="sxs-lookup"><span data-stu-id="ed0ee-164">Note that hello value of **sampleheader** in hello response is now **value2**.</span></span> <span data-ttu-id="ed0ee-165">Porque os resultados da operação Olá são codificados por cadeia de consulta, a resposta em cache anterior Olá não foi devolvida.</span><span class="sxs-lookup"><span data-stu-id="ed0ee-165">Because hello operation results are keyed by query string, hello previous cached response was not returned.</span></span>

## <span data-ttu-id="ed0ee-166"><a name="next-steps"> </a>Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="ed0ee-166"><a name="next-steps"> </a>Next steps</span></span>
* <span data-ttu-id="ed0ee-167">Para obter mais informações sobre as políticas de colocação em cache, consulte [políticas de colocação em cache] [ Caching policies] no Olá [referência de política de gestão de API][API Management policy reference].</span><span class="sxs-lookup"><span data-stu-id="ed0ee-167">For more information about caching policies, see [Caching policies][Caching policies] in hello [API Management policy reference][API Management policy reference].</span></span>
* <span data-ttu-id="ed0ee-168">Para obter informações sobre a colocação em cache de itens por chave utilizando expressões de política, consulte [Colocação em cache personalizada na API Management do Azure](api-management-sample-cache-by-key.md).</span><span class="sxs-lookup"><span data-stu-id="ed0ee-168">For information on caching items by key using policy expressions, see [Custom caching in Azure API Management](api-management-sample-cache-by-key.md).</span></span>

[api-management-management-console]: ./media/api-management-howto-cache/api-management-management-console.png
[api-management-echo-api]: ./media/api-management-howto-cache/api-management-echo-api.png
[api-management-echo-api-operations]: ./media/api-management-howto-cache/api-management-echo-api-operations.png
[api-management-caching-tab]: ./media/api-management-howto-cache/api-management-caching-tab.png
[api-management-operation-dropdown]: ./media/api-management-howto-cache/api-management-operation-dropdown.png
[api-management-policy-editor]: ./media/api-management-howto-cache/api-management-policy-editor.png
[api-management-developer-portal-menu]: ./media/api-management-howto-cache/api-management-developer-portal-menu.png
[api-management-apis-echo-api]: ./media/api-management-howto-cache/api-management-apis-echo-api.png
[api-management-open-console]: ./media/api-management-howto-cache/api-management-open-console.png
[api-management-console]: ./media/api-management-howto-cache/api-management-console.png


[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How tooadd and publish a product]: api-management-howto-add-products.md
[Monitoring and analytics]: api-management-monitoring.md
[Add APIs tooa product]: api-management-howto-add-products.md#add-apis
[Publish a product]: api-management-howto-add-products.md#publish-product
[Get started with Azure API Management]: api-management-get-started.md

[API Management policy reference]: https://msdn.microsoft.com/library/azure/dn894081.aspx
[Caching policies]: https://msdn.microsoft.com/library/azure/dn894086.aspx

[Create an API Management service instance]: api-management-get-started.md#create-service-instance

[Configure an operation for caching]: #configure-caching
[Review hello caching policies]: #caching-policies
[Call an operation and test hello caching]: #test-operation
[Next steps]: #next-steps
