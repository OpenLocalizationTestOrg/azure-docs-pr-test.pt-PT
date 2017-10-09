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
# <a name="product-templates-in-azure-api-management"></a>Modelos de produtos na API Management do Azure
Gestão de API do Azure fornece que Olá capacidade toocustomize Olá conteúdo páginas portal para programadores utilizando um conjunto de modelos que configurar o respetivo conteúdo. Utilizar [DotLiquid](http://dotliquidmarkup.org/) sintaxe e Olá editor à sua escolha, tal como [DotLiquid para Designers](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), e um conjunto de fornecido localizado [recursos de cadeia](api-management-template-resources.md#strings), [ Recursos de glifo](api-management-template-resources.md#glyphs), e [página controlos](api-management-page-controls.md), ter uma enorme flexibilidade tooconfigure Olá conteúdo páginas Olá como julgar utilizando estes modelos.  
  
 modelos de Olá nesta secção permitem conteúdo de Olá toocustomize das páginas de produto Olá no portal de programador Olá.  
  
-   [Lista de produto](#ProductList)  
  
-   [Produto](#Product)  
  
> [!NOTE]
>  Modelos predefinidos de exemplo estão incluídos no Olá seguir documentação, mas são requerente toochange devido toocontinuous melhoramentos. Pode ver os modelos de predefinidos em direto de Olá no portal de programador Olá navegando modelos individuais toohello assim o desejar. Para obter mais informações sobre como trabalhar com modelos, consulte [como toocustomize Olá utilizando modelos de portal do Programador de API Management](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).  
  
##  <a name="ProductList"></a>Lista de produto  
 Olá **lista produto** modelo permite-lhe corpo de Olá toocustomize da página de lista de produto Olá no portal de programador Olá.  
  
 ![Lista de produtos](./media/api-management-product-templates/APIM_ProductsListTemplatePage.png "APIM_ProductsListTemplatePage")  
  
### <a name="default-template"></a>Modelo predefinido  
  
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
  
### <a name="controls"></a>Controlos  
 Olá `Product list` modelo pode utilizar o seguinte Olá [página controlos](api-management-page-controls.md).  
  
-   [controlo de paginação](api-management-page-controls.md#paging-control)  
  
-   [controlo de procura](api-management-page-controls.md#search-control)  
  
### <a name="data-model"></a>Modelo de dados  
  
|Propriedade|Tipo|Descrição|  
|--------------|----------|-----------------|  
|Paginação|[Paginação](api-management-template-data-model-reference.md#Paging) entidade.|informações de paginação de Olá para a coleção de produtos Olá.|  
|Filtragem|[Filtragem](api-management-template-data-model-reference.md#Filtering) entidade.|Olá filtragem informações de produtos Olá listam página.|  
|Produtos|Coleção de [produto](api-management-template-data-model-reference.md#Product) entidades.|Olá produtos toohello visível utilizador atual.|  
  
### <a name="sample-template-data"></a>Dados de exemplo do modelo  
  
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
  
##  <a name="Product"></a>Produto  
 Olá **produto** modelo permite-lhe corpo de Olá toocustomize da página de produto Olá no portal de programador Olá.  
  
 ![Página de produto do portal de programador](./media/api-management-product-templates/APIM_ProductPage.png "APIM_ProductPage")  
  
### <a name="default-template"></a>Modelo predefinido  
  
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
  
### <a name="controls"></a>Controlos  
 Olá `Product list` modelo pode utilizar o seguinte Olá [página controlos](api-management-page-controls.md).  
  
-   [botão subscrever](api-management-page-controls.md#subscribe-button)  
  
### <a name="data-model"></a>Modelo de dados  
  
|Propriedade|Tipo|Descrição|  
|--------------|----------|-----------------|  
|Produto|[Produto](api-management-template-data-model-reference.md#Product)|produto especificado Olá.|  
|IsDeveloperSubscribed|Valor booleano|Indica se o utilizador atual Olá está subscrito toothis produto.|  
|SubscriptionState|Número|Estado da subscrição Olá Olá. Estados possíveis são:<br /><br /> -   `0 - suspended`– subscrição Olá está bloqueada e subscritor Olá não é possível chamar as APIs do produto Olá.<br />-   `1 - active`– Olá subscrição está ativa.<br />-   `2 - expired`– subscrição de Olá atingiu a respetiva data de expiração e foi desativada.<br />-   `3 - submitted`– pedido de subscrição de Olá foi efetuado por programador Olá, mas ainda não foi aprovado ou rejeitado.<br />-   `4 - rejected`– Olá subscrição pedido foi recusado por um administrador.<br />-   `5 - cancelled`– subscrição Olá foi cancelada pelo administrador ou programador Olá.|  
|Limites|Matriz|Esta propriedade foi preterida e não deve ser utilizada.|  
|DelegatedSubscriptionEnabled|Valor booleano|Se [delegação](https://azure.microsoft.com/documentation/articles/api-management-howto-setup-delegation/) está ativada para esta subscrição.|  
|DelegatedSubscriptionUrl|Cadeia|Se estiver ativada a delegação, Olá delegado URL da subscrição.|  
|IsAgreed|Valor booleano|Se o produto de Olá tem termos, se utilizador atual Olá tem Aceito os termos de toohello.|  
|Subscrições|Coleção de [resumo de subscrição](api-management-template-data-model-reference.md#SubscriptionSummary) entidades.|produto de toohello do Olá subscrições.|  
|APIs|Coleção de [API](api-management-template-data-model-reference.md#API) entidades.|Olá APIs este produto.|  
|CannotAddBecauseSubscriptionNumberLimitReached|Valor booleano|Indica se o utilizador atual Olá está toosubscribe elegível toothis produto com limite de subscrição de toohello regard.|  
|CannotAddBecauseMultipleSubscriptionsNotAllowed|Valor booleano|Indica se o utilizador atual Olá está toosubscribe elegível toothis produto com subscrições de toomultiple regard permitidas ou não.|  
  
### <a name="sample-template-data"></a>Dados de exemplo do modelo  
  
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

## <a name="next-steps"></a>Passos seguintes
Para obter mais informações sobre como trabalhar com modelos, consulte [como toocustomize Olá utilizando modelos de portal do Programador de API Management](api-management-developer-portal-templates.md).
