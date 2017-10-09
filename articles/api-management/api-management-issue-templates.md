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
# <a name="issue-templates-in-azure-api-management"></a>Emitir modelos na API Management do Azure
Gestão de API do Azure fornece que Olá capacidade toocustomize Olá conteúdo páginas portal para programadores utilizando um conjunto de modelos que configurar o respetivo conteúdo. Utilizar [DotLiquid](http://dotliquidmarkup.org/) sintaxe e Olá editor à sua escolha, tal como [DotLiquid para Designers](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), e um conjunto de fornecido localizado [recursos de cadeia](api-management-template-resources.md#strings), [ Recursos de glifo](api-management-template-resources.md#glyphs), e [página controlos](api-management-page-controls.md), ter uma enorme flexibilidade tooconfigure Olá conteúdo páginas Olá como julgar utilizando estes modelos.  
  
 modelos de Olá nesta secção permitem conteúdo de Olá toocustomize das páginas de problema Olá no portal de programador Olá.  
  
-   [Lista de problema](#IssueList)  
  
> [!NOTE]
>  Modelos predefinidos de exemplo estão incluídos no Olá seguir documentação, mas são requerente toochange devido toocontinuous melhoramentos. Pode ver os modelos de predefinidos em direto de Olá no portal de programador Olá navegando modelos individuais toohello assim o desejar. Para obter mais informações sobre como trabalhar com modelos, consulte [como toocustomize Olá utilizando modelos de portal do Programador de API Management](api-management-developer-portal-templates.md).  
  
##  <a name="IssueList"></a>Lista de problema  
 Olá **lista problema** modelo permite-lhe corpo de Olá toocustomize da página de lista de problema Olá no portal de programador Olá.  
  
 ![Portal de programador da lista de emitir](./media/api-management-issue-templates/APIM-Issue-List-Developer-Portal.png "APIM Portal do Programador de lista de problema")  
  
### <a name="default-template"></a>Modelo predefinido  
  
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
  
### <a name="controls"></a>Controlos  
 Olá `Issue list` modelo pode utilizar o seguinte Olá [página controlos](api-management-page-controls.md).  
  
-   [controlo de paginação](api-management-page-controls.md#paging-control)  
  
### <a name="data-model"></a>Modelo de dados  
  
|Propriedade|Tipo|Descrição|  
|--------------|----------|-----------------|  
|Problemas|Coleção de [problema](api-management-template-data-model-reference.md#Issue) entidades.|Olá problemas toohello visível utilizador atual.|  
|Paginação|[Paginação](api-management-template-data-model-reference.md#Paging) entidade.|informações de paginação de Olá para a coleção de aplicações de Olá.|  
|IsAuthenticated|Valor booleano|Indica se o utilizador atual Olá está toohello assinado no portal do programador.|  
|CanReportIssues|Valor booleano|Se o utilizador atual Olá tem permissões toofile um problema.|  
|Pesquisa|Cadeia|Esta propriedade foi preterida e não deve ser utilizada.|  
  
### <a name="sample-template-data"></a>Dados de exemplo do modelo  
  
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

## <a name="next-steps"></a>Passos seguintes
Para obter mais informações sobre como trabalhar com modelos, consulte [como toocustomize Olá utilizando modelos de portal do Programador de API Management](api-management-developer-portal-templates.md).
