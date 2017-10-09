---
title: modelos de aaaIssue na API Management do Azure | Microsoft Docs
description: "Saiba como toocustomize Olá conteúdo de páginas de problema Olá no portal do programador Olá na API Management do Azure."
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 47da4bb2-426e-4e53-8fa7-214ee2e3ab37
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: e12902e52c164f73902a97f15ea550790dfecf1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="issue-templates-in-azure-api-management"></a><span data-ttu-id="7575e-103">Emitir modelos na API Management do Azure</span><span class="sxs-lookup"><span data-stu-id="7575e-103">Issue templates in Azure API Management</span></span>
<span data-ttu-id="7575e-104">Gestão de API do Azure fornece que Olá capacidade toocustomize Olá conteúdo páginas portal para programadores utilizando um conjunto de modelos que configurar o respetivo conteúdo.</span><span class="sxs-lookup"><span data-stu-id="7575e-104">Azure API Management provides you hello ability toocustomize hello content of developer portal pages using a set of templates that configure their content.</span></span> <span data-ttu-id="7575e-105">Utilizar [DotLiquid](http://dotliquidmarkup.org/) sintaxe e Olá editor à sua escolha, tal como [DotLiquid para Designers](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), e um conjunto de fornecido localizado [recursos de cadeia](api-management-template-resources.md#strings), [ Recursos de glifo](api-management-template-resources.md#glyphs), e [página controlos](api-management-page-controls.md), ter uma enorme flexibilidade tooconfigure Olá conteúdo páginas Olá como julgar utilizando estes modelos.</span><span class="sxs-lookup"><span data-stu-id="7575e-105">Using [DotLiquid](http://dotliquidmarkup.org/) syntax and hello editor of your choice, such as [DotLiquid for Designers](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), and a provided set of localized [String resources](api-management-template-resources.md#strings), [Glyph resources](api-management-template-resources.md#glyphs), and [Page controls](api-management-page-controls.md), you have great flexibility tooconfigure hello content of hello pages as you see fit using these templates.</span></span>  
  
 <span data-ttu-id="7575e-106">modelos de Olá nesta secção permitem conteúdo de Olá toocustomize das páginas de problema Olá no portal de programador Olá.</span><span class="sxs-lookup"><span data-stu-id="7575e-106">hello templates in this section allow you toocustomize hello content of hello Issue pages in hello developer portal.</span></span>  
  
-   [<span data-ttu-id="7575e-107">Lista de problema</span><span class="sxs-lookup"><span data-stu-id="7575e-107">Issue list</span></span>](#IssueList)  
  
> [!NOTE]
>  <span data-ttu-id="7575e-108">Modelos predefinidos de exemplo estão incluídos no Olá seguir documentação, mas são requerente toochange devido toocontinuous melhoramentos.</span><span class="sxs-lookup"><span data-stu-id="7575e-108">Sample default templates are included in hello following documentation, but are subject toochange due toocontinuous improvements.</span></span> <span data-ttu-id="7575e-109">Pode ver os modelos de predefinidos em direto de Olá no portal de programador Olá navegando modelos individuais toohello assim o desejar.</span><span class="sxs-lookup"><span data-stu-id="7575e-109">You can view hello live default templates in hello developer portal by navigating toohello desired individual templates.</span></span> <span data-ttu-id="7575e-110">Para obter mais informações sobre como trabalhar com modelos, consulte [como toocustomize Olá utilizando modelos de portal do Programador de API Management](api-management-developer-portal-templates.md).</span><span class="sxs-lookup"><span data-stu-id="7575e-110">For more information about working with templates, see [How toocustomize hello API Management developer portal using templates](api-management-developer-portal-templates.md).</span></span>  
  
##  <span data-ttu-id="7575e-111"><a name="IssueList"></a>Lista de problema</span><span class="sxs-lookup"><span data-stu-id="7575e-111"><a name="IssueList"></a> Issue list</span></span>  
 <span data-ttu-id="7575e-112">Olá **lista problema** modelo permite-lhe corpo de Olá toocustomize da página de lista de problema Olá no portal de programador Olá.</span><span class="sxs-lookup"><span data-stu-id="7575e-112">hello **Issue list** template allows you toocustomize hello body of hello issue list page in hello developer portal.</span></span>  
  
 <span data-ttu-id="7575e-113">![Portal de programador da lista de emitir](./media/api-management-issue-templates/APIM-Issue-List-Developer-Portal.png "APIM Portal do Programador de lista de problema")</span><span class="sxs-lookup"><span data-stu-id="7575e-113">![Issue List Developer Portal](./media/api-management-issue-templates/APIM-Issue-List-Developer-Portal.png "APIM Issue List Developer Portal")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="7575e-114">Modelo predefinido</span><span class="sxs-lookup"><span data-stu-id="7575e-114">Default template</span></span>  
  
```xml  
<div class="row">  
  <div class="col-md-9">  
    <h2>{% localized "IssuesStrings|WebIssuesIndexTitle" %}</h2>  
  </div>  
</div>  
<div class="row">  
  <div class="col-md-12">  
    {% if issues.size > 0 %}  
    <ul class="list-unstyled">  
      {% capture reportedBy %}{% localized "IssuesStrings|WebIssuesStatusReportedBy" %}{% endcapture %}  
      {% assign replaceString0 = '{0}' %}  
      {% assign replaceString1 = '{1}' %}  
      {% for issue in issues %}  
      <li>  
        <h3>  
          <a href="/issues/{{issue.id}}">{{issue.title}}</a>  
        </h3>  
        <p>{{issue.description}}</p>  
        <em>  
          {% capture state %}{{issue.issueState}}{% endcapture %}  
          {% capture devName %}{{issue.subscriptionDeveloperName}}{% endcapture %}  
          {% capture str1 %}{{ reportedBy | replace : replaceString0, state }}{% endcapture %}  
          {{ str1 | replace : replaceString1, devName }}  
          <span class="UtcDateElement">{{ issue.reportedOn | date: "r" }}</span>  
        </em>  
      </li>  
      {% endfor %}  
    </ul>  
    <paging-control></paging-control>  
    {% else %}  
    {% localized "CommonResources|NoItemsToDisplay" %}  
    {% endif %}  
    {% if canReportIssue %}  
    <a class="btn btn-primary" id="createIssue" href="/Issues/Create">{% localized "IssuesStrings|WebIssuesReportIssueButton" %}</a>  
    {% elsif isAuthenticated %}  
    <hr />  
    <p>{% localized "IssuesStrings|WebIssuesNoActiveSubscriptions" %}</p>  
    {% else %}  
    <hr />  
    <p>  
      {% capture signIntext %}{% localized "IssuesStrings|WebIssuesNotSignin" %}{% endcapture %}  
      {% capture link %}<a href="/signin">{% localized "IssuesStrings|WebIssuesSignIn" %}</a>{% endcapture %}  
      {{ signIntext | replace : replaceString0, link }}  
    </p>  
    {% endif %}  
  </div>  
</div>  
```  
  
### <a name="controls"></a><span data-ttu-id="7575e-115">Controlos</span><span class="sxs-lookup"><span data-stu-id="7575e-115">Controls</span></span>  
 <span data-ttu-id="7575e-116">Olá `Issue list` modelo pode utilizar o seguinte Olá [página controlos](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="7575e-116">hello `Issue list` template may use hello following [page controls](api-management-page-controls.md).</span></span>  
  
-   [<span data-ttu-id="7575e-117">controlo de paginação</span><span class="sxs-lookup"><span data-stu-id="7575e-117">paging-control</span></span>](api-management-page-controls.md#paging-control)  
  
### <a name="data-model"></a><span data-ttu-id="7575e-118">Modelo de dados</span><span class="sxs-lookup"><span data-stu-id="7575e-118">Data model</span></span>  
  
|<span data-ttu-id="7575e-119">Propriedade</span><span class="sxs-lookup"><span data-stu-id="7575e-119">Property</span></span>|<span data-ttu-id="7575e-120">Tipo</span><span class="sxs-lookup"><span data-stu-id="7575e-120">Type</span></span>|<span data-ttu-id="7575e-121">Descrição</span><span class="sxs-lookup"><span data-stu-id="7575e-121">Description</span></span>|  
|--------------|----------|-----------------|  
|<span data-ttu-id="7575e-122">Problemas</span><span class="sxs-lookup"><span data-stu-id="7575e-122">Issues</span></span>|<span data-ttu-id="7575e-123">Coleção de [problema](api-management-template-data-model-reference.md#Issue) entidades.</span><span class="sxs-lookup"><span data-stu-id="7575e-123">Collection of [Issue](api-management-template-data-model-reference.md#Issue) entities.</span></span>|<span data-ttu-id="7575e-124">Olá problemas toohello visível utilizador atual.</span><span class="sxs-lookup"><span data-stu-id="7575e-124">hello issues visible toohello current user.</span></span>|  
|<span data-ttu-id="7575e-125">Paginação</span><span class="sxs-lookup"><span data-stu-id="7575e-125">Paging</span></span>|<span data-ttu-id="7575e-126">[Paginação](api-management-template-data-model-reference.md#Paging) entidade.</span><span class="sxs-lookup"><span data-stu-id="7575e-126">[Paging](api-management-template-data-model-reference.md#Paging) entity.</span></span>|<span data-ttu-id="7575e-127">informações de paginação de Olá para a coleção de aplicações de Olá.</span><span class="sxs-lookup"><span data-stu-id="7575e-127">hello paging information for hello applications collection.</span></span>|  
|<span data-ttu-id="7575e-128">IsAuthenticated</span><span class="sxs-lookup"><span data-stu-id="7575e-128">IsAuthenticated</span></span>|<span data-ttu-id="7575e-129">Valor booleano</span><span class="sxs-lookup"><span data-stu-id="7575e-129">boolean</span></span>|<span data-ttu-id="7575e-130">Indica se o utilizador atual Olá está toohello assinado no portal do programador.</span><span class="sxs-lookup"><span data-stu-id="7575e-130">Whether hello current user is signed-in toohello developer portal.</span></span>|  
|<span data-ttu-id="7575e-131">CanReportIssues</span><span class="sxs-lookup"><span data-stu-id="7575e-131">CanReportIssues</span></span>|<span data-ttu-id="7575e-132">Valor booleano</span><span class="sxs-lookup"><span data-stu-id="7575e-132">boolean</span></span>|<span data-ttu-id="7575e-133">Se o utilizador atual Olá tem permissões toofile um problema.</span><span class="sxs-lookup"><span data-stu-id="7575e-133">Whether hello current user has permissions toofile an issue.</span></span>|  
|<span data-ttu-id="7575e-134">Pesquisa</span><span class="sxs-lookup"><span data-stu-id="7575e-134">Search</span></span>|<span data-ttu-id="7575e-135">Cadeia</span><span class="sxs-lookup"><span data-stu-id="7575e-135">string</span></span>|<span data-ttu-id="7575e-136">Esta propriedade foi preterida e não deve ser utilizada.</span><span class="sxs-lookup"><span data-stu-id="7575e-136">This property is deprecated and should not be used.</span></span>|  
  
### <a name="sample-template-data"></a><span data-ttu-id="7575e-137">Dados de exemplo do modelo</span><span class="sxs-lookup"><span data-stu-id="7575e-137">Sample template data</span></span>  
  
```json  
{  
    "Issues": [  
        {  
            "Id": "5702b68bb16653124c8f9ba7",  
            "ApiId": "570275f1b16653124c8f9ba3",  
            "Title": "I couldn't figure out how tooconnect my application toohello API",  
            "Description": "I'm having trouble connecting my application toohello backend API.",  
            "SubscriptionDeveloperName": "Clayton",  
            "IssueState": "Proposed",  
            "ReportedOn": "2016-04-04T18:46:35.64",  
            "Comments": null,  
            "Attachments": null,  
            "Services": null  
        }  
    ],  
    "Paging": {  
        "Page": 1,  
        "PageSize": 10,  
        "TotalItemCount": 1,  
        "ShowAll": false,  
        "PageCount": 1  
    },  
    "IsAuthenticated": true,  
    "CanReportIssue": true,  
    "Search": null  
}  
```

## <a name="next-steps"></a><span data-ttu-id="7575e-138">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="7575e-138">Next steps</span></span>
<span data-ttu-id="7575e-139">Para obter mais informações sobre como trabalhar com modelos, consulte [como toocustomize Olá utilizando modelos de portal do Programador de API Management](api-management-developer-portal-templates.md).</span><span class="sxs-lookup"><span data-stu-id="7575e-139">For more information about working with templates, see [How toocustomize hello API Management developer portal using templates](api-management-developer-portal-templates.md).</span></span>
