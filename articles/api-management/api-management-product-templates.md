---
title: modelos de aaaProduct na API Management do Azure | Microsoft Docs
description: "Saiba como o conteúdo de Olá toocustomize produto Olá páginas no portal de programador Olá API Management do Azure."
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 49f9254c-4c5f-4ed4-9c8d-798f44e805ee
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 60600299287aad87f9b621782ab5ceb866601d03
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="product-templates-in-azure-api-management"></a><span data-ttu-id="47966-103">Modelos de produtos na API Management do Azure</span><span class="sxs-lookup"><span data-stu-id="47966-103">Product templates in Azure API Management</span></span>
<span data-ttu-id="47966-104">Gestão de API do Azure fornece que Olá capacidade toocustomize Olá conteúdo páginas portal para programadores utilizando um conjunto de modelos que configurar o respetivo conteúdo.</span><span class="sxs-lookup"><span data-stu-id="47966-104">Azure API Management provides you hello ability toocustomize hello content of developer portal pages using a set of templates that configure their content.</span></span> <span data-ttu-id="47966-105">Utilizar [DotLiquid](http://dotliquidmarkup.org/) sintaxe e Olá editor à sua escolha, tal como [DotLiquid para Designers](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), e um conjunto de fornecido localizado [recursos de cadeia](api-management-template-resources.md#strings), [ Recursos de glifo](api-management-template-resources.md#glyphs), e [página controlos](api-management-page-controls.md), ter uma enorme flexibilidade tooconfigure Olá conteúdo páginas Olá como julgar utilizando estes modelos.</span><span class="sxs-lookup"><span data-stu-id="47966-105">Using [DotLiquid](http://dotliquidmarkup.org/) syntax and hello editor of your choice, such as [DotLiquid for Designers](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), and a provided set of localized [String resources](api-management-template-resources.md#strings), [Glyph resources](api-management-template-resources.md#glyphs), and [Page controls](api-management-page-controls.md), you have great flexibility tooconfigure hello content of hello pages as you see fit using these templates.</span></span>  
  
 <span data-ttu-id="47966-106">modelos de Olá nesta secção permitem conteúdo de Olá toocustomize das páginas de produto Olá no portal de programador Olá.</span><span class="sxs-lookup"><span data-stu-id="47966-106">hello templates in this section allow you toocustomize hello content of hello product pages in hello developer portal.</span></span>  
  
-   [<span data-ttu-id="47966-107">Lista de produto</span><span class="sxs-lookup"><span data-stu-id="47966-107">Product list</span></span>](#ProductList)  
  
-   [<span data-ttu-id="47966-108">Produto</span><span class="sxs-lookup"><span data-stu-id="47966-108">Product</span></span>](#Product)  
  
> [!NOTE]
>  <span data-ttu-id="47966-109">Modelos predefinidos de exemplo estão incluídos no Olá seguir documentação, mas são requerente toochange devido toocontinuous melhoramentos.</span><span class="sxs-lookup"><span data-stu-id="47966-109">Sample default templates are included in hello following documentation, but are subject toochange due toocontinuous improvements.</span></span> <span data-ttu-id="47966-110">Pode ver os modelos de predefinidos em direto de Olá no portal de programador Olá navegando modelos individuais toohello assim o desejar.</span><span class="sxs-lookup"><span data-stu-id="47966-110">You can view hello live default templates in hello developer portal by navigating toohello desired individual templates.</span></span> <span data-ttu-id="47966-111">Para obter mais informações sobre como trabalhar com modelos, consulte [como toocustomize Olá utilizando modelos de portal do Programador de API Management](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span><span class="sxs-lookup"><span data-stu-id="47966-111">For more information about working with templates, see [How toocustomize hello API Management developer portal using templates](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span></span>  
  
##  <span data-ttu-id="47966-112"><a name="ProductList"></a>Lista de produto</span><span class="sxs-lookup"><span data-stu-id="47966-112"><a name="ProductList"></a> Product list</span></span>  
 <span data-ttu-id="47966-113">Olá **lista produto** modelo permite-lhe corpo de Olá toocustomize da página de lista de produto Olá no portal de programador Olá.</span><span class="sxs-lookup"><span data-stu-id="47966-113">hello **Product list** template allows you toocustomize hello body of hello product list page in hello developer portal.</span></span>  
  
 <span data-ttu-id="47966-114">![Lista de produtos](./media/api-management-product-templates/APIM_ProductsListTemplatePage.png "APIM_ProductsListTemplatePage")</span><span class="sxs-lookup"><span data-stu-id="47966-114">![Products list](./media/api-management-product-templates/APIM_ProductsListTemplatePage.png "APIM_ProductsListTemplatePage")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="47966-115">Modelo predefinido</span><span class="sxs-lookup"><span data-stu-id="47966-115">Default template</span></span>  
  
```xml  
<search-control></search-control>  
<div class="row">  
    <div class="col-md-9">  
        <h2>{% localized "ProductsStrings|PageTitleProducts" %}</h2>  
    </div>  
</div>  
<div class="row">  
    <div class="col-md-12">  
    {% if products.size > 0 %}  
    <ul class="list-unstyled">  
    {% for product in products %}  
        <li>  
            <h3><a href="/products/{{product.id}}">{{product.title}}</a></h3>  
            {{product.description}}  
        </li>     
    {% endfor %}  
    </ul>  
    <paging-control></paging-control>  
    {% else %}  
    {% localized "CommonResources|NoItemsToDisplay" %}  
    {% endif %}  
    </div>  
</div>  
```  
  
### <a name="controls"></a><span data-ttu-id="47966-116">Controlos</span><span class="sxs-lookup"><span data-stu-id="47966-116">Controls</span></span>  
 <span data-ttu-id="47966-117">Olá `Product list` modelo pode utilizar o seguinte Olá [página controlos](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="47966-117">hello `Product list` template may use hello following [page controls](api-management-page-controls.md).</span></span>  
  
-   [<span data-ttu-id="47966-118">controlo de paginação</span><span class="sxs-lookup"><span data-stu-id="47966-118">paging-control</span></span>](api-management-page-controls.md#paging-control)  
  
-   [<span data-ttu-id="47966-119">controlo de procura</span><span class="sxs-lookup"><span data-stu-id="47966-119">search-control</span></span>](api-management-page-controls.md#search-control)  
  
### <a name="data-model"></a><span data-ttu-id="47966-120">Modelo de dados</span><span class="sxs-lookup"><span data-stu-id="47966-120">Data model</span></span>  
  
|<span data-ttu-id="47966-121">Propriedade</span><span class="sxs-lookup"><span data-stu-id="47966-121">Property</span></span>|<span data-ttu-id="47966-122">Tipo</span><span class="sxs-lookup"><span data-stu-id="47966-122">Type</span></span>|<span data-ttu-id="47966-123">Descrição</span><span class="sxs-lookup"><span data-stu-id="47966-123">Description</span></span>|  
|--------------|----------|-----------------|  
|<span data-ttu-id="47966-124">Paginação</span><span class="sxs-lookup"><span data-stu-id="47966-124">Paging</span></span>|<span data-ttu-id="47966-125">[Paginação](api-management-template-data-model-reference.md#Paging) entidade.</span><span class="sxs-lookup"><span data-stu-id="47966-125">[Paging](api-management-template-data-model-reference.md#Paging) entity.</span></span>|<span data-ttu-id="47966-126">informações de paginação de Olá para a coleção de produtos Olá.</span><span class="sxs-lookup"><span data-stu-id="47966-126">hello paging information for hello products collection.</span></span>|  
|<span data-ttu-id="47966-127">Filtragem</span><span class="sxs-lookup"><span data-stu-id="47966-127">Filtering</span></span>|<span data-ttu-id="47966-128">[Filtragem](api-management-template-data-model-reference.md#Filtering) entidade.</span><span class="sxs-lookup"><span data-stu-id="47966-128">[Filtering](api-management-template-data-model-reference.md#Filtering) entity.</span></span>|<span data-ttu-id="47966-129">Olá filtragem informações de produtos Olá listam página.</span><span class="sxs-lookup"><span data-stu-id="47966-129">hello filtering information for hello products list page.</span></span>|  
|<span data-ttu-id="47966-130">Produtos</span><span class="sxs-lookup"><span data-stu-id="47966-130">Products</span></span>|<span data-ttu-id="47966-131">Coleção de [produto](api-management-template-data-model-reference.md#Product) entidades.</span><span class="sxs-lookup"><span data-stu-id="47966-131">Collection of [Product](api-management-template-data-model-reference.md#Product) entities.</span></span>|<span data-ttu-id="47966-132">Olá produtos toohello visível utilizador atual.</span><span class="sxs-lookup"><span data-stu-id="47966-132">hello products visible toohello current user.</span></span>|  
  
### <a name="sample-template-data"></a><span data-ttu-id="47966-133">Dados de exemplo do modelo</span><span class="sxs-lookup"><span data-stu-id="47966-133">Sample template data</span></span>  
  
```json  
{  
    "Paging": {  
        "Page": 1,  
        "PageSize": 10,  
        "TotalItemCount": 2,  
        "ShowAll": false,  
        "PageCount": 1  
    },  
    "Filtering": {  
        "Pattern": null,  
        "Placeholder": "Search products"  
    },  
    "Products": [  
        {  
            "Id": "56f9445ffaf7560049060001",  
            "Title": "Starter",  
            "Description": "Subscribers will be able toorun 5 calls/minute up tooa maximum of 100 calls/week.",  
            "Terms": "",  
            "ProductState": 1,  
            "AllowMultipleSubscriptions": false,  
            "MultipleSubscriptionsCount": 1  
        },  
        {  
            "Id": "56f9445ffaf7560049060002",  
            "Title": "Unlimited",  
            "Description": "Subscribers have completely unlimited access toohello API. Administrator approval is required.",  
            "Terms": null,  
            "ProductState": 1,  
            "AllowMultipleSubscriptions": false,  
            "MultipleSubscriptionsCount": 1  
        }  
    ]  
}  
```  
  
##  <span data-ttu-id="47966-134"><a name="Product"></a>Produto</span><span class="sxs-lookup"><span data-stu-id="47966-134"><a name="Product"></a> Product</span></span>  
 <span data-ttu-id="47966-135">Olá **produto** modelo permite-lhe corpo de Olá toocustomize da página de produto Olá no portal de programador Olá.</span><span class="sxs-lookup"><span data-stu-id="47966-135">hello **Product** template allows you toocustomize hello body of hello product page in hello developer portal.</span></span>  
  
 <span data-ttu-id="47966-136">![Página de produto do portal de programador](./media/api-management-product-templates/APIM_ProductPage.png "APIM_ProductPage")</span><span class="sxs-lookup"><span data-stu-id="47966-136">![Developer portal product page](./media/api-management-product-templates/APIM_ProductPage.png "APIM_ProductPage")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="47966-137">Modelo predefinido</span><span class="sxs-lookup"><span data-stu-id="47966-137">Default template</span></span>  
  
```xml  
<h2>{{Product.Title}}</h2>  
<p>{{Product.Description}}</p>  
  
{% assign replaceString0 = '{0}' %}  
  
{% if Limits and Limits.size > 0 %}  
<h3>{% localized "ProductDetailsStrings|WebProductsUsageLimitsHeader"%}</h3>  
<ul>  
  {% for limit in Limits %}  
  <li>{{limit.DisplayName}}</li>  
  {% endfor %}  
</ul>  
{% endif %}  
  
{% if apis.size > 0 %}  
<p>  
  <b>  
    {% if apis.size == 1 %}  
    {% capture apisCountText %}{% localized "ProductDetailsStrings|TextblockSingleApisCount" %}{% endcapture %}  
    {% else %}  
    {% capture apisCountText %}{% localized "ProductDetailsStrings|TextblockMultipleApisCount" %}{% endcapture %}  
    {% endif %}  
  
    {% capture apisCount %}{{apis.size}}{% endcapture %}  
    {{ apisCountText | replace : replaceString0, apisCount }}  
  </b>  
</p>  
  
<ul>  
  {% for api in Apis %}  
  <li>  
    <a href="/docs/services/{{api.Id}}">{{api.Name}}</a>  
  </li>  
  {% endfor %}  
</ul>  
{% endif %}  
  
{% if subscriptions.size > 0 %}  
<p>  
  <b>  
    {% if subscriptions.size == 1 %}  
    {% capture subscriptionsCountText %}{% localized "ProductDetailsStrings|TextblockSingleSubscriptionsCount" %}{% endcapture %}  
    {% else %}  
    {% capture subscriptionsCountText %}{% localized "ProductDetailsStrings|TextblockMultipleSubscriptionsCount" %}{% endcapture %}  
    {% endif %}  
  
    {% capture subscriptionsCount %}{{subscriptions.size}}{% endcapture %}  
    {{ subscriptionsCountText | replace : replaceString0, subscriptionsCount }}  
  </b>  
</p>  
  
<ul>  
  {% for subscription in subscriptions %}  
  <li>  
    <a href="/developer#{{subscription.Id}}">{{subscription.DisplayName}}</a>  
  </li>  
  {% endfor %}  
</ul>  
{% endif %}  
{% if CannotAddBecauseSubscriptionNumberLimitReached %}  
<b>{% localized "ProductDetailsStrings|TextblockSubscriptionLimitReached" %}</b>  
{% elsif CannotAddBecauseMultipleSubscriptionsNotAllowed == false %}  
<subscribe-button></subscribe-button>  
{% endif %}  
```  
  
### <a name="controls"></a><span data-ttu-id="47966-138">Controlos</span><span class="sxs-lookup"><span data-stu-id="47966-138">Controls</span></span>  
 <span data-ttu-id="47966-139">Olá `Product list` modelo pode utilizar o seguinte Olá [página controlos](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="47966-139">hello `Product list` template may use hello following [page controls](api-management-page-controls.md).</span></span>  
  
-   [<span data-ttu-id="47966-140">botão subscrever</span><span class="sxs-lookup"><span data-stu-id="47966-140">subscribe-button</span></span>](api-management-page-controls.md#subscribe-button)  
  
### <a name="data-model"></a><span data-ttu-id="47966-141">Modelo de dados</span><span class="sxs-lookup"><span data-stu-id="47966-141">Data model</span></span>  
  
|<span data-ttu-id="47966-142">Propriedade</span><span class="sxs-lookup"><span data-stu-id="47966-142">Property</span></span>|<span data-ttu-id="47966-143">Tipo</span><span class="sxs-lookup"><span data-stu-id="47966-143">Type</span></span>|<span data-ttu-id="47966-144">Descrição</span><span class="sxs-lookup"><span data-stu-id="47966-144">Description</span></span>|  
|--------------|----------|-----------------|  
|<span data-ttu-id="47966-145">Produto</span><span class="sxs-lookup"><span data-stu-id="47966-145">Product</span></span>|[<span data-ttu-id="47966-146">Produto</span><span class="sxs-lookup"><span data-stu-id="47966-146">Product</span></span>](api-management-template-data-model-reference.md#Product)|<span data-ttu-id="47966-147">produto especificado Olá.</span><span class="sxs-lookup"><span data-stu-id="47966-147">hello specified product.</span></span>|  
|<span data-ttu-id="47966-148">IsDeveloperSubscribed</span><span class="sxs-lookup"><span data-stu-id="47966-148">IsDeveloperSubscribed</span></span>|<span data-ttu-id="47966-149">Valor booleano</span><span class="sxs-lookup"><span data-stu-id="47966-149">boolean</span></span>|<span data-ttu-id="47966-150">Indica se o utilizador atual Olá está subscrito toothis produto.</span><span class="sxs-lookup"><span data-stu-id="47966-150">Whether hello current user is subscribed toothis product.</span></span>|  
|<span data-ttu-id="47966-151">SubscriptionState</span><span class="sxs-lookup"><span data-stu-id="47966-151">SubscriptionState</span></span>|<span data-ttu-id="47966-152">Número</span><span class="sxs-lookup"><span data-stu-id="47966-152">number</span></span>|<span data-ttu-id="47966-153">Estado da subscrição Olá Olá.</span><span class="sxs-lookup"><span data-stu-id="47966-153">hello state of hello subscription.</span></span> <span data-ttu-id="47966-154">Estados possíveis são:</span><span class="sxs-lookup"><span data-stu-id="47966-154">Possible states are:</span></span><br /><br /> <span data-ttu-id="47966-155">-   `0 - suspended`– subscrição Olá está bloqueada e subscritor Olá não é possível chamar as APIs do produto Olá.</span><span class="sxs-lookup"><span data-stu-id="47966-155">-   `0 - suspended` – hello subscription is blocked, and hello subscriber cannot call any APIs of hello product.</span></span><br /><span data-ttu-id="47966-156">-   `1 - active`– Olá subscrição está ativa.</span><span class="sxs-lookup"><span data-stu-id="47966-156">-   `1 - active` – hello subscription is active.</span></span><br /><span data-ttu-id="47966-157">-   `2 - expired`– subscrição de Olá atingiu a respetiva data de expiração e foi desativada.</span><span class="sxs-lookup"><span data-stu-id="47966-157">-   `2 - expired` – hello subscription reached its expiration date and was deactivated.</span></span><br /><span data-ttu-id="47966-158">-   `3 - submitted`– pedido de subscrição de Olá foi efetuado por programador Olá, mas ainda não foi aprovado ou rejeitado.</span><span class="sxs-lookup"><span data-stu-id="47966-158">-   `3 - submitted` – hello subscription request has been made by hello developer, but has not yet been approved or rejected.</span></span><br /><span data-ttu-id="47966-159">-   `4 - rejected`– Olá subscrição pedido foi recusado por um administrador.</span><span class="sxs-lookup"><span data-stu-id="47966-159">-   `4 - rejected` – hello subscription request has been denied by an administrator.</span></span><br /><span data-ttu-id="47966-160">-   `5 - cancelled`– subscrição Olá foi cancelada pelo administrador ou programador Olá.</span><span class="sxs-lookup"><span data-stu-id="47966-160">-   `5 - cancelled` – hello subscription has been cancelled by hello developer or administrator.</span></span>|  
|<span data-ttu-id="47966-161">Limites</span><span class="sxs-lookup"><span data-stu-id="47966-161">Limits</span></span>|<span data-ttu-id="47966-162">Matriz</span><span class="sxs-lookup"><span data-stu-id="47966-162">array</span></span>|<span data-ttu-id="47966-163">Esta propriedade foi preterida e não deve ser utilizada.</span><span class="sxs-lookup"><span data-stu-id="47966-163">This property is deprecated and should not be used.</span></span>|  
|<span data-ttu-id="47966-164">DelegatedSubscriptionEnabled</span><span class="sxs-lookup"><span data-stu-id="47966-164">DelegatedSubscriptionEnabled</span></span>|<span data-ttu-id="47966-165">Valor booleano</span><span class="sxs-lookup"><span data-stu-id="47966-165">boolean</span></span>|<span data-ttu-id="47966-166">Se [delegação](https://azure.microsoft.com/documentation/articles/api-management-howto-setup-delegation/) está ativada para esta subscrição.</span><span class="sxs-lookup"><span data-stu-id="47966-166">Whether [delegation](https://azure.microsoft.com/documentation/articles/api-management-howto-setup-delegation/) is enabled for this subscription.</span></span>|  
|<span data-ttu-id="47966-167">DelegatedSubscriptionUrl</span><span class="sxs-lookup"><span data-stu-id="47966-167">DelegatedSubscriptionUrl</span></span>|<span data-ttu-id="47966-168">Cadeia</span><span class="sxs-lookup"><span data-stu-id="47966-168">string</span></span>|<span data-ttu-id="47966-169">Se estiver ativada a delegação, Olá delegado URL da subscrição.</span><span class="sxs-lookup"><span data-stu-id="47966-169">If delegation is enabled, hello delegated subscription URL.</span></span>|  
|<span data-ttu-id="47966-170">IsAgreed</span><span class="sxs-lookup"><span data-stu-id="47966-170">IsAgreed</span></span>|<span data-ttu-id="47966-171">Valor booleano</span><span class="sxs-lookup"><span data-stu-id="47966-171">boolean</span></span>|<span data-ttu-id="47966-172">Se o produto de Olá tem termos, se utilizador atual Olá tem Aceito os termos de toohello.</span><span class="sxs-lookup"><span data-stu-id="47966-172">If hello product has terms, whether hello current user has agreed toohello terms.</span></span>|  
|<span data-ttu-id="47966-173">Subscrições</span><span class="sxs-lookup"><span data-stu-id="47966-173">Subscriptions</span></span>|<span data-ttu-id="47966-174">Coleção de [resumo de subscrição](api-management-template-data-model-reference.md#SubscriptionSummary) entidades.</span><span class="sxs-lookup"><span data-stu-id="47966-174">Collection of [Subscription summary](api-management-template-data-model-reference.md#SubscriptionSummary) entities.</span></span>|<span data-ttu-id="47966-175">produto de toohello do Olá subscrições.</span><span class="sxs-lookup"><span data-stu-id="47966-175">hello subscriptions toohello product.</span></span>|  
|<span data-ttu-id="47966-176">APIs</span><span class="sxs-lookup"><span data-stu-id="47966-176">Apis</span></span>|<span data-ttu-id="47966-177">Coleção de [API](api-management-template-data-model-reference.md#API) entidades.</span><span class="sxs-lookup"><span data-stu-id="47966-177">Collection of [API](api-management-template-data-model-reference.md#API) entities.</span></span>|<span data-ttu-id="47966-178">Olá APIs este produto.</span><span class="sxs-lookup"><span data-stu-id="47966-178">hello APIs in this product.</span></span>|  
|<span data-ttu-id="47966-179">CannotAddBecauseSubscriptionNumberLimitReached</span><span class="sxs-lookup"><span data-stu-id="47966-179">CannotAddBecauseSubscriptionNumberLimitReached</span></span>|<span data-ttu-id="47966-180">Valor booleano</span><span class="sxs-lookup"><span data-stu-id="47966-180">boolean</span></span>|<span data-ttu-id="47966-181">Indica se o utilizador atual Olá está toosubscribe elegível toothis produto com limite de subscrição de toohello regard.</span><span class="sxs-lookup"><span data-stu-id="47966-181">Whether hello current user is eligible toosubscribe toothis product with regard toohello subscription limit.</span></span>|  
|<span data-ttu-id="47966-182">CannotAddBecauseMultipleSubscriptionsNotAllowed</span><span class="sxs-lookup"><span data-stu-id="47966-182">CannotAddBecauseMultipleSubscriptionsNotAllowed</span></span>|<span data-ttu-id="47966-183">Valor booleano</span><span class="sxs-lookup"><span data-stu-id="47966-183">boolean</span></span>|<span data-ttu-id="47966-184">Indica se o utilizador atual Olá está toosubscribe elegível toothis produto com subscrições de toomultiple regard permitidas ou não.</span><span class="sxs-lookup"><span data-stu-id="47966-184">Whether hello current user is eligible toosubscribe toothis product with regard toomultiple subscriptions being allowed or not.</span></span>|  
  
### <a name="sample-template-data"></a><span data-ttu-id="47966-185">Dados de exemplo do modelo</span><span class="sxs-lookup"><span data-stu-id="47966-185">Sample template data</span></span>  
  
```json  
{  
    "Product": {  
        "Id": "56f9445ffaf7560049060001",  
        "Title": "Starter",  
        "Description": "Subscribers will be able toorun 5 calls/minute up tooa maximum of 100 calls/week.",  
        "Terms": "",  
        "ProductState": 1,  
        "AllowMultipleSubscriptions": false,  
        "MultipleSubscriptionsCount": 1  
    },  
    "IsDeveloperSubscribed": true,  
    "SubscriptionState": 1,  
    "Limits": [],  
    "DelegatedSubscriptionEnabled": false,  
    "DelegatedSubscriptionUrl": null,  
    "IsAgreed": false,  
    "Subscriptions": [  
        {  
            "Id": "56f9445ffaf7560049070001",  
            "DisplayName": "Starter  (default)"  
        }  
    ],  
    "Apis": [  
        {  
            "id": "56f9445ffaf7560049040001",  
            "name": "Echo API",  
            "description": null,  
            "serviceUrl": "http://echoapi.cloudapp.net/api",  
            "path": "echo",  
            "protocols": [  
                2  
            ],  
            "authenticationSettings": null,  
            "subscriptionKeyParameterNames": null  
        }  
    ],  
    "CannotAddBecauseSubscriptionNumberLimitReached": false,  
    "CannotAddBecauseMultipleSubscriptionsNotAllowed": true  
}  
```

## <a name="next-steps"></a><span data-ttu-id="47966-186">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="47966-186">Next steps</span></span>
<span data-ttu-id="47966-187">Para obter mais informações sobre como trabalhar com modelos, consulte [como toocustomize Olá utilizando modelos de portal do Programador de API Management](api-management-developer-portal-templates.md).</span><span class="sxs-lookup"><span data-stu-id="47966-187">For more information about working with templates, see [How toocustomize hello API Management developer portal using templates](api-management-developer-portal-templates.md).</span></span>
