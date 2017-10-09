---
title: "controlos de página de API Management aaaAzure | Microsoft Docs"
description: "Saiba mais sobre controlos de página Olá disponíveis para utilização em modelos de portal do programador na API Management do Azure."
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 03e0ac8d-64ff-4e9a-b029-d7be14fb31e3
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 1a16a6fce197c0a2e14807ac21e81a9a73b515b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-api-management-page-controls"></a>Controlos de página de API Management do Azure
Gestão de API do Azure fornece Olá seguintes controlos para utilização em modelos de portal de programador Olá.  
  
 toouse um controlo, coloque-o numa localização Olá pretendido no modelo do portal de programador Olá. Alguns controlos, tais como Olá [ações de aplicação](#app-actions) controlar, ter parâmetros, conforme mostrado no seguinte exemplo de Olá.  
  
```xml  
<app-actions params="{ appId: '{{app.id}}' }"></app-actions>  
```  
  
 Olá os valores de parâmetros de Olá são transmitidos como parte do modelo de dados de Olá para o modelo de Olá. Na maioria dos casos, pode simplesmente colar Olá fornecido exemplo para cada controlo para o mesmo toowork corretamente. Para mais informações sobre os valores de parâmetros de Olá, pode ver a secção de modelo de dados de Olá para cada modelo no qual um controlo pode ser utilizado.  
  
 Para obter mais informações sobre como trabalhar com modelos, consulte [como toocustomize Olá utilizando modelos de portal do Programador de API Management](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).  
  
## <a name="developer-portal-template-page-controls"></a>Controlos de página de modelo do portal do Programador  
  
-   [ações de aplicações](#app-actions)  
  
-   [início de sessão básica](#basic-signin)  
  
-   [controlo de paginação](#paging-control)  
  
-   [fornecedores](#providers)  
  
-   [controlo de procura](#search-control)  
  
-   [inscrição](#sign-up)  
  
-   [botão subscrever](#subscribe-button)  
  
-   [Cancelar subscrição](#subscription-cancel)  
  
##  <a name="app-actions"></a>ações de aplicações  
 Olá `app-actions` controlo fornece uma interface de utilizador para interagir com aplicações na página de perfil de utilizador Olá no portal de programador Olá.  
  
 ![aplicação &#45; controlo ações](./media/api-management-page-controls/APIM-app-actions-control.png "controlo de aplicação ações APIM")  
  
### <a name="usage"></a>Utilização  
  
```xml  
<app-actions params="{ appId: '{{app.id}}' }"></app-actions>  
```  
  
### <a name="parameters"></a>Parâmetros  
  
|Parâmetro|Descrição|  
|---------------|-----------------|  
|AppId|id da aplicação Olá Olá.|  
  
### <a name="developer-portal-templates"></a>Modelos de portais de programador  
 Olá `app-actions` controlo pode ser utilizado numa Olá seguintes modelos de portal de programador.  
  
-   [Aplicações](api-management-user-profile-templates.md#Applications)  
  
##  <a name="basic-signin"></a>início de sessão básica  
 Olá `basic-signin` controlo fornece um controlo para recolher o início de sessão do utilizador nas informações no Olá iniciar sessão na página no portal do programador Olá.  
  
 ![Basic &#45; o controlo de início de sessão](./media/api-management-page-controls/APIM-basic-signin-control.png "controlo de início de sessão básica APIM")  
  
### <a name="usage"></a>Utilização  
  
```xml  
<basic-SignIn></basic-SignIn>  
```  
  
### <a name="parameters"></a>Parâmetros  
 nenhum.  
  
### <a name="developer-portal-templates"></a>Modelos de portais de programador  
 Olá `basic-signin` controlo pode ser utilizado numa Olá seguintes modelos de portal de programador.  
  
-   [A iniciar sessão](api-management-page-templates.md#SignIn)  
  
##  <a name="paging-control"></a>controlo de paginação  
 Olá `paging-control` fornece a funcionalidade de paginação no programador as páginas do portal que apresentam uma lista de itens.  
  
 ![controlo de paginação](./media/api-management-page-controls/APIM-paging-control.png "controlo de paginação APIM")  
  
### <a name="usage"></a>Utilização  
  
```xml  
<paging-control></paging-control>  
```  
  
### <a name="parameters"></a>Parâmetros  
 nenhum.  
  
### <a name="developer-portal-templates"></a>Modelos de portais de programador  
 Olá `paging-control` controlo pode ser utilizado numa Olá seguintes modelos de portal de programador.  
  
-   [Lista de API](api-management-api-templates.md#APIList)  
  
-   [Lista de problema](api-management-issue-templates.md#IssueList)  
  
-   [Lista de produto](api-management-product-templates.md#ProductList)  
  
##  <a name="providers"></a>fornecedores  
 Olá `providers` controlo fornece um controlo de seleção de fornecedores de autenticação no Olá página no portal de programador Olá de início de sessão.  
  
 ![controlo de fornecedores](./media/api-management-page-controls/APIM-providers-control.png "controlo de fornecedores APIM")  
  
### <a name="usage"></a>Utilização  
  
```xml  
<providers></providers>  
```  
  
### <a name="parameters"></a>Parâmetros  
 nenhum.  
  
### <a name="developer-portal-templates"></a>Modelos de portais de programador  
 Olá `providers` controlo pode ser utilizado numa Olá seguintes modelos de portal de programador.  
  
-   [A iniciar sessão](api-management-page-templates.md#SignIn)  
  
##  <a name="search-control"></a>controlo de procura  
 Olá `search-control` fornece funcionalidade de pesquisa no programador as páginas do portal que apresentam uma lista de itens.  
  
 ![Procurar controlo](./media/api-management-page-controls/APIM-search-control.png "controlo de procura APIM")  
  
### <a name="usage"></a>Utilização  
  
```xml  
<search-control></search-control>  
```  
  
### <a name="parameters"></a>Parâmetros  
 nenhum.  
  
### <a name="developer-portal-templates"></a>Modelos de portais de programador  
 Olá `search-control` controlo pode ser utilizado numa Olá seguintes modelos de portal de programador.  
  
-   [Lista de API](api-management-api-templates.md#APIList)  
  
-   [Lista de produto](api-management-product-templates.md#ProductList)  
  
##  <a name="sign-up"></a>inscrição  
 Olá `sign-up` controlo fornece um controlo para recolher informações de perfil de utilizador na página no portal de programador Olá inscrição Olá.  
  
 ![início de sessão &#45; até o controlo](./media/api-management-page-controls/APIM-sign-up-control.png "controlo APIM de inscrição")  
  
### <a name="usage"></a>Utilização  
  
```xml  
<sign-up></sign-up>  
```  
  
### <a name="parameters"></a>Parâmetros  
 nenhum.  
  
### <a name="developer-portal-templates"></a>Modelos de portais de programador  
 Olá `sign-up` controlo pode ser utilizado numa Olá seguintes modelos de portal de programador.  
  
-   [Inscrever-se](api-management-page-templates.md#SignUp)  
  
##  <a name="subscribe-button"></a>botão subscrever  
 Olá `subscribe-button` fornece um controlo para subscrever um produto de tooa do utilizador.  
  
 ![subscrever &#45; o controlo de botão](./media/api-management-page-controls/APIM-subscribe-button-control.png "APIM subscrever-controlo de botão")  
  
### <a name="usage"></a>Utilização  
  
```xml  
<subscribe-button></subscribe-button>  
```  
  
### <a name="parameters"></a>Parâmetros  
 nenhum.  
  
### <a name="developer-portal-templates"></a>Modelos de portais de programador  
 Olá `subscribe-button` controlo pode ser utilizado numa Olá seguintes modelos de portal de programador.  
  
-   [Produto](api-management-product-templates.md#Product)  
  
##  <a name="subscription-cancel"></a>Cancelar subscrição  
 Olá `subscription-cancel` controlo fornece um controlo para cancelar um produto de tooa de subscrição na página de perfil de utilizador Olá no portal de programador Olá.  
  
 ![subscrição &#45; Cancelar controlo](./media/api-management-page-controls/APIM-subscription-cancel-control.png "controlo de subscrição cancelar APIM")  
  
### <a name="usage"></a>Utilização  
  
```xml  
<subscription-cancel params="{ subscriptionId: '{{subscription.id}}', cancelUrl: '{{subscription.cancelUrl}}' }">  
</subscription-cancel>  
  
```  
  
### <a name="parameters"></a>Parâmetros  
  
|Parâmetro|Descrição|  
|---------------|-----------------|  
|subscriptionId|id de Olá do Olá toocancel de subscrição.|  
|cancelUrl|subscrição de Olá Cancelar URL.|  
  
### <a name="developer-portal-templates"></a>Modelos de portais de programador  
 Olá `subscription-cancel` controlo pode ser utilizado numa Olá seguintes modelos de portal de programador.  
  
-   [Produto](api-management-product-templates.md#Product)

## <a name="next-steps"></a>Passos seguintes
Para obter mais informações sobre como trabalhar com modelos, consulte [como toocustomize Olá utilizando modelos de portal do Programador de API Management](api-management-developer-portal-templates.md).
