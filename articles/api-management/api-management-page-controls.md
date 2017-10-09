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
# <a name="azure-api-management-page-controls"></a><span data-ttu-id="8f3e3-103">Controlos de página de API Management do Azure</span><span class="sxs-lookup"><span data-stu-id="8f3e3-103">Azure API Management page controls</span></span>
<span data-ttu-id="8f3e3-104">Gestão de API do Azure fornece Olá seguintes controlos para utilização em modelos de portal de programador Olá.</span><span class="sxs-lookup"><span data-stu-id="8f3e3-104">Azure API Management provides hello following controls for use in hello developer portal templates.</span></span>  
  
 <span data-ttu-id="8f3e3-105">toouse um controlo, coloque-o numa localização Olá pretendido no modelo do portal de programador Olá.</span><span class="sxs-lookup"><span data-stu-id="8f3e3-105">toouse a control, place it in hello desired location in hello developer portal template.</span></span> <span data-ttu-id="8f3e3-106">Alguns controlos, tais como Olá [ações de aplicação](#app-actions) controlar, ter parâmetros, conforme mostrado no seguinte exemplo de Olá.</span><span class="sxs-lookup"><span data-stu-id="8f3e3-106">Some controls, such as hello [app-actions](#app-actions) control, have parameters, as shown in hello following example.</span></span>  
  
```xml  
<app-actions params="{ appId: '{{app.id}}' }"></app-actions>  
```  
  
 <span data-ttu-id="8f3e3-107">Olá os valores de parâmetros de Olá são transmitidos como parte do modelo de dados de Olá para o modelo de Olá.</span><span class="sxs-lookup"><span data-stu-id="8f3e3-107">hello values for hello parameters are passed in as part of hello data model for hello template.</span></span> <span data-ttu-id="8f3e3-108">Na maioria dos casos, pode simplesmente colar Olá fornecido exemplo para cada controlo para o mesmo toowork corretamente.</span><span class="sxs-lookup"><span data-stu-id="8f3e3-108">In most cases, you can simply paste in hello provided example for each control for it toowork correctly.</span></span> <span data-ttu-id="8f3e3-109">Para mais informações sobre os valores de parâmetros de Olá, pode ver a secção de modelo de dados de Olá para cada modelo no qual um controlo pode ser utilizado.</span><span class="sxs-lookup"><span data-stu-id="8f3e3-109">For more information on hello parameter values, you can see hello data model section for each template in which a control may be used.</span></span>  
  
 <span data-ttu-id="8f3e3-110">Para obter mais informações sobre como trabalhar com modelos, consulte [como toocustomize Olá utilizando modelos de portal do Programador de API Management](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span><span class="sxs-lookup"><span data-stu-id="8f3e3-110">For more information about working with templates, see [How toocustomize hello API Management developer portal using templates](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span></span>  
  
## <a name="developer-portal-template-page-controls"></a><span data-ttu-id="8f3e3-111">Controlos de página de modelo do portal do Programador</span><span class="sxs-lookup"><span data-stu-id="8f3e3-111">Developer portal template page controls</span></span>  
  
-   [<span data-ttu-id="8f3e3-112">ações de aplicações</span><span class="sxs-lookup"><span data-stu-id="8f3e3-112">app-actions</span></span>](#app-actions)  
  
-   [<span data-ttu-id="8f3e3-113">início de sessão básica</span><span class="sxs-lookup"><span data-stu-id="8f3e3-113">basic-signin</span></span>](#basic-signin)  
  
-   [<span data-ttu-id="8f3e3-114">controlo de paginação</span><span class="sxs-lookup"><span data-stu-id="8f3e3-114">paging-control</span></span>](#paging-control)  
  
-   [<span data-ttu-id="8f3e3-115">fornecedores</span><span class="sxs-lookup"><span data-stu-id="8f3e3-115">providers</span></span>](#providers)  
  
-   [<span data-ttu-id="8f3e3-116">controlo de procura</span><span class="sxs-lookup"><span data-stu-id="8f3e3-116">search-control</span></span>](#search-control)  
  
-   [<span data-ttu-id="8f3e3-117">inscrição</span><span class="sxs-lookup"><span data-stu-id="8f3e3-117">sign-up</span></span>](#sign-up)  
  
-   [<span data-ttu-id="8f3e3-118">botão subscrever</span><span class="sxs-lookup"><span data-stu-id="8f3e3-118">subscribe-button</span></span>](#subscribe-button)  
  
-   [<span data-ttu-id="8f3e3-119">Cancelar subscrição</span><span class="sxs-lookup"><span data-stu-id="8f3e3-119">subscription-cancel</span></span>](#subscription-cancel)  
  
##  <span data-ttu-id="8f3e3-120"><a name="app-actions"></a>ações de aplicações</span><span class="sxs-lookup"><span data-stu-id="8f3e3-120"><a name="app-actions"></a> app-actions</span></span>  
 <span data-ttu-id="8f3e3-121">Olá `app-actions` controlo fornece uma interface de utilizador para interagir com aplicações na página de perfil de utilizador Olá no portal de programador Olá.</span><span class="sxs-lookup"><span data-stu-id="8f3e3-121">hello `app-actions` control provides a user interface for interacting with applications on hello user profile page in hello developer portal.</span></span>  
  
 <span data-ttu-id="8f3e3-122">![aplicação &#45; controlo ações](./media/api-management-page-controls/APIM-app-actions-control.png "controlo de aplicação ações APIM")</span><span class="sxs-lookup"><span data-stu-id="8f3e3-122">![app&#45;actions control](./media/api-management-page-controls/APIM-app-actions-control.png "APIM app-actions control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="8f3e3-123">Utilização</span><span class="sxs-lookup"><span data-stu-id="8f3e3-123">Usage</span></span>  
  
```xml  
<app-actions params="{ appId: '{{app.id}}' }"></app-actions>  
```  
  
### <a name="parameters"></a><span data-ttu-id="8f3e3-124">Parâmetros</span><span class="sxs-lookup"><span data-stu-id="8f3e3-124">Parameters</span></span>  
  
|<span data-ttu-id="8f3e3-125">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="8f3e3-125">Parameter</span></span>|<span data-ttu-id="8f3e3-126">Descrição</span><span class="sxs-lookup"><span data-stu-id="8f3e3-126">Description</span></span>|  
|---------------|-----------------|  
|<span data-ttu-id="8f3e3-127">AppId</span><span class="sxs-lookup"><span data-stu-id="8f3e3-127">appId</span></span>|<span data-ttu-id="8f3e3-128">id da aplicação Olá Olá.</span><span class="sxs-lookup"><span data-stu-id="8f3e3-128">hello id of hello application.</span></span>|  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="8f3e3-129">Modelos de portais de programador</span><span class="sxs-lookup"><span data-stu-id="8f3e3-129">Developer portal templates</span></span>  
 <span data-ttu-id="8f3e3-130">Olá `app-actions` controlo pode ser utilizado numa Olá seguintes modelos de portal de programador.</span><span class="sxs-lookup"><span data-stu-id="8f3e3-130">hello `app-actions` control may be used in hello following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="8f3e3-131">Aplicações</span><span class="sxs-lookup"><span data-stu-id="8f3e3-131">Applications</span></span>](api-management-user-profile-templates.md#Applications)  
  
##  <span data-ttu-id="8f3e3-132"><a name="basic-signin"></a>início de sessão básica</span><span class="sxs-lookup"><span data-stu-id="8f3e3-132"><a name="basic-signin"></a> basic-signin</span></span>  
 <span data-ttu-id="8f3e3-133">Olá `basic-signin` controlo fornece um controlo para recolher o início de sessão do utilizador nas informações no Olá iniciar sessão na página no portal do programador Olá.</span><span class="sxs-lookup"><span data-stu-id="8f3e3-133">hello `basic-signin` control provides a control for collecting user sign in information in hello sign in page in hello developer portal.</span></span>  
  
 <span data-ttu-id="8f3e3-134">![Basic &#45; o controlo de início de sessão](./media/api-management-page-controls/APIM-basic-signin-control.png "controlo de início de sessão básica APIM")</span><span class="sxs-lookup"><span data-stu-id="8f3e3-134">![basic&#45;signin control](./media/api-management-page-controls/APIM-basic-signin-control.png "APIM basic-signin control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="8f3e3-135">Utilização</span><span class="sxs-lookup"><span data-stu-id="8f3e3-135">Usage</span></span>  
  
```xml  
<basic-SignIn></basic-SignIn>  
```  
  
### <a name="parameters"></a><span data-ttu-id="8f3e3-136">Parâmetros</span><span class="sxs-lookup"><span data-stu-id="8f3e3-136">Parameters</span></span>  
 <span data-ttu-id="8f3e3-137">nenhum.</span><span class="sxs-lookup"><span data-stu-id="8f3e3-137">None.</span></span>  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="8f3e3-138">Modelos de portais de programador</span><span class="sxs-lookup"><span data-stu-id="8f3e3-138">Developer portal templates</span></span>  
 <span data-ttu-id="8f3e3-139">Olá `basic-signin` controlo pode ser utilizado numa Olá seguintes modelos de portal de programador.</span><span class="sxs-lookup"><span data-stu-id="8f3e3-139">hello `basic-signin` control may be used in hello following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="8f3e3-140">A iniciar sessão</span><span class="sxs-lookup"><span data-stu-id="8f3e3-140">Sign in</span></span>](api-management-page-templates.md#SignIn)  
  
##  <span data-ttu-id="8f3e3-141"><a name="paging-control"></a>controlo de paginação</span><span class="sxs-lookup"><span data-stu-id="8f3e3-141"><a name="paging-control"></a> paging-control</span></span>  
 <span data-ttu-id="8f3e3-142">Olá `paging-control` fornece a funcionalidade de paginação no programador as páginas do portal que apresentam uma lista de itens.</span><span class="sxs-lookup"><span data-stu-id="8f3e3-142">hello `paging-control` provides paging functionality on developer portal pages that display a list of items.</span></span>  
  
 <span data-ttu-id="8f3e3-143">![controlo de paginação](./media/api-management-page-controls/APIM-paging-control.png "controlo de paginação APIM")</span><span class="sxs-lookup"><span data-stu-id="8f3e3-143">![paging control](./media/api-management-page-controls/APIM-paging-control.png "APIM paging control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="8f3e3-144">Utilização</span><span class="sxs-lookup"><span data-stu-id="8f3e3-144">Usage</span></span>  
  
```xml  
<paging-control></paging-control>  
```  
  
### <a name="parameters"></a><span data-ttu-id="8f3e3-145">Parâmetros</span><span class="sxs-lookup"><span data-stu-id="8f3e3-145">Parameters</span></span>  
 <span data-ttu-id="8f3e3-146">nenhum.</span><span class="sxs-lookup"><span data-stu-id="8f3e3-146">None.</span></span>  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="8f3e3-147">Modelos de portais de programador</span><span class="sxs-lookup"><span data-stu-id="8f3e3-147">Developer portal templates</span></span>  
 <span data-ttu-id="8f3e3-148">Olá `paging-control` controlo pode ser utilizado numa Olá seguintes modelos de portal de programador.</span><span class="sxs-lookup"><span data-stu-id="8f3e3-148">hello `paging-control` control may be used in hello following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="8f3e3-149">Lista de API</span><span class="sxs-lookup"><span data-stu-id="8f3e3-149">API list</span></span>](api-management-api-templates.md#APIList)  
  
-   [<span data-ttu-id="8f3e3-150">Lista de problema</span><span class="sxs-lookup"><span data-stu-id="8f3e3-150">Issue list</span></span>](api-management-issue-templates.md#IssueList)  
  
-   [<span data-ttu-id="8f3e3-151">Lista de produto</span><span class="sxs-lookup"><span data-stu-id="8f3e3-151">Product list</span></span>](api-management-product-templates.md#ProductList)  
  
##  <span data-ttu-id="8f3e3-152"><a name="providers"></a>fornecedores</span><span class="sxs-lookup"><span data-stu-id="8f3e3-152"><a name="providers"></a> providers</span></span>  
 <span data-ttu-id="8f3e3-153">Olá `providers` controlo fornece um controlo de seleção de fornecedores de autenticação no Olá página no portal de programador Olá de início de sessão.</span><span class="sxs-lookup"><span data-stu-id="8f3e3-153">hello `providers` control provides a control for selection of authentication providers in hello sign in page in hello developer portal.</span></span>  
  
 <span data-ttu-id="8f3e3-154">![controlo de fornecedores](./media/api-management-page-controls/APIM-providers-control.png "controlo de fornecedores APIM")</span><span class="sxs-lookup"><span data-stu-id="8f3e3-154">![providers control](./media/api-management-page-controls/APIM-providers-control.png "APIM providers control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="8f3e3-155">Utilização</span><span class="sxs-lookup"><span data-stu-id="8f3e3-155">Usage</span></span>  
  
```xml  
<providers></providers>  
```  
  
### <a name="parameters"></a><span data-ttu-id="8f3e3-156">Parâmetros</span><span class="sxs-lookup"><span data-stu-id="8f3e3-156">Parameters</span></span>  
 <span data-ttu-id="8f3e3-157">nenhum.</span><span class="sxs-lookup"><span data-stu-id="8f3e3-157">None.</span></span>  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="8f3e3-158">Modelos de portais de programador</span><span class="sxs-lookup"><span data-stu-id="8f3e3-158">Developer portal templates</span></span>  
 <span data-ttu-id="8f3e3-159">Olá `providers` controlo pode ser utilizado numa Olá seguintes modelos de portal de programador.</span><span class="sxs-lookup"><span data-stu-id="8f3e3-159">hello `providers` control may be used in hello following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="8f3e3-160">A iniciar sessão</span><span class="sxs-lookup"><span data-stu-id="8f3e3-160">Sign in</span></span>](api-management-page-templates.md#SignIn)  
  
##  <span data-ttu-id="8f3e3-161"><a name="search-control"></a>controlo de procura</span><span class="sxs-lookup"><span data-stu-id="8f3e3-161"><a name="search-control"></a> search-control</span></span>  
 <span data-ttu-id="8f3e3-162">Olá `search-control` fornece funcionalidade de pesquisa no programador as páginas do portal que apresentam uma lista de itens.</span><span class="sxs-lookup"><span data-stu-id="8f3e3-162">hello `search-control` provides search functionality on developer portal pages that display a list of items.</span></span>  
  
 <span data-ttu-id="8f3e3-163">![Procurar controlo](./media/api-management-page-controls/APIM-search-control.png "controlo de procura APIM")</span><span class="sxs-lookup"><span data-stu-id="8f3e3-163">![search control](./media/api-management-page-controls/APIM-search-control.png "APIM search control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="8f3e3-164">Utilização</span><span class="sxs-lookup"><span data-stu-id="8f3e3-164">Usage</span></span>  
  
```xml  
<search-control></search-control>  
```  
  
### <a name="parameters"></a><span data-ttu-id="8f3e3-165">Parâmetros</span><span class="sxs-lookup"><span data-stu-id="8f3e3-165">Parameters</span></span>  
 <span data-ttu-id="8f3e3-166">nenhum.</span><span class="sxs-lookup"><span data-stu-id="8f3e3-166">None.</span></span>  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="8f3e3-167">Modelos de portais de programador</span><span class="sxs-lookup"><span data-stu-id="8f3e3-167">Developer portal templates</span></span>  
 <span data-ttu-id="8f3e3-168">Olá `search-control` controlo pode ser utilizado numa Olá seguintes modelos de portal de programador.</span><span class="sxs-lookup"><span data-stu-id="8f3e3-168">hello `search-control` control may be used in hello following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="8f3e3-169">Lista de API</span><span class="sxs-lookup"><span data-stu-id="8f3e3-169">API list</span></span>](api-management-api-templates.md#APIList)  
  
-   [<span data-ttu-id="8f3e3-170">Lista de produto</span><span class="sxs-lookup"><span data-stu-id="8f3e3-170">Product list</span></span>](api-management-product-templates.md#ProductList)  
  
##  <span data-ttu-id="8f3e3-171"><a name="sign-up"></a>inscrição</span><span class="sxs-lookup"><span data-stu-id="8f3e3-171"><a name="sign-up"></a> sign-up</span></span>  
 <span data-ttu-id="8f3e3-172">Olá `sign-up` controlo fornece um controlo para recolher informações de perfil de utilizador na página no portal de programador Olá inscrição Olá.</span><span class="sxs-lookup"><span data-stu-id="8f3e3-172">hello `sign-up` control provides a control for collecting user profile information in hello sign up page in hello developer portal.</span></span>  
  
 <span data-ttu-id="8f3e3-173">![início de sessão &#45; até o controlo](./media/api-management-page-controls/APIM-sign-up-control.png "controlo APIM de inscrição")</span><span class="sxs-lookup"><span data-stu-id="8f3e3-173">![sign&#45;up control](./media/api-management-page-controls/APIM-sign-up-control.png "APIM sign-up control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="8f3e3-174">Utilização</span><span class="sxs-lookup"><span data-stu-id="8f3e3-174">Usage</span></span>  
  
```xml  
<sign-up></sign-up>  
```  
  
### <a name="parameters"></a><span data-ttu-id="8f3e3-175">Parâmetros</span><span class="sxs-lookup"><span data-stu-id="8f3e3-175">Parameters</span></span>  
 <span data-ttu-id="8f3e3-176">nenhum.</span><span class="sxs-lookup"><span data-stu-id="8f3e3-176">None.</span></span>  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="8f3e3-177">Modelos de portais de programador</span><span class="sxs-lookup"><span data-stu-id="8f3e3-177">Developer portal templates</span></span>  
 <span data-ttu-id="8f3e3-178">Olá `sign-up` controlo pode ser utilizado numa Olá seguintes modelos de portal de programador.</span><span class="sxs-lookup"><span data-stu-id="8f3e3-178">hello `sign-up` control may be used in hello following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="8f3e3-179">Inscrever-se</span><span class="sxs-lookup"><span data-stu-id="8f3e3-179">Sign up</span></span>](api-management-page-templates.md#SignUp)  
  
##  <span data-ttu-id="8f3e3-180"><a name="subscribe-button"></a>botão subscrever</span><span class="sxs-lookup"><span data-stu-id="8f3e3-180"><a name="subscribe-button"></a> subscribe-button</span></span>  
 <span data-ttu-id="8f3e3-181">Olá `subscribe-button` fornece um controlo para subscrever um produto de tooa do utilizador.</span><span class="sxs-lookup"><span data-stu-id="8f3e3-181">hello `subscribe-button` provides a control for subscribing a user tooa product.</span></span>  
  
 <span data-ttu-id="8f3e3-182">![subscrever &#45; o controlo de botão](./media/api-management-page-controls/APIM-subscribe-button-control.png "APIM subscrever-controlo de botão")</span><span class="sxs-lookup"><span data-stu-id="8f3e3-182">![subscribe&#45;button control](./media/api-management-page-controls/APIM-subscribe-button-control.png "APIM subscribe-button control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="8f3e3-183">Utilização</span><span class="sxs-lookup"><span data-stu-id="8f3e3-183">Usage</span></span>  
  
```xml  
<subscribe-button></subscribe-button>  
```  
  
### <a name="parameters"></a><span data-ttu-id="8f3e3-184">Parâmetros</span><span class="sxs-lookup"><span data-stu-id="8f3e3-184">Parameters</span></span>  
 <span data-ttu-id="8f3e3-185">nenhum.</span><span class="sxs-lookup"><span data-stu-id="8f3e3-185">None.</span></span>  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="8f3e3-186">Modelos de portais de programador</span><span class="sxs-lookup"><span data-stu-id="8f3e3-186">Developer portal templates</span></span>  
 <span data-ttu-id="8f3e3-187">Olá `subscribe-button` controlo pode ser utilizado numa Olá seguintes modelos de portal de programador.</span><span class="sxs-lookup"><span data-stu-id="8f3e3-187">hello `subscribe-button` control may be used in hello following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="8f3e3-188">Produto</span><span class="sxs-lookup"><span data-stu-id="8f3e3-188">Product</span></span>](api-management-product-templates.md#Product)  
  
##  <span data-ttu-id="8f3e3-189"><a name="subscription-cancel"></a>Cancelar subscrição</span><span class="sxs-lookup"><span data-stu-id="8f3e3-189"><a name="subscription-cancel"></a> subscription-cancel</span></span>  
 <span data-ttu-id="8f3e3-190">Olá `subscription-cancel` controlo fornece um controlo para cancelar um produto de tooa de subscrição na página de perfil de utilizador Olá no portal de programador Olá.</span><span class="sxs-lookup"><span data-stu-id="8f3e3-190">hello `subscription-cancel` control provides a control for cancelling a subscription tooa product in hello user profile page in hello developer portal.</span></span>  
  
 <span data-ttu-id="8f3e3-191">![subscrição &#45; Cancelar controlo](./media/api-management-page-controls/APIM-subscription-cancel-control.png "controlo de subscrição cancelar APIM")</span><span class="sxs-lookup"><span data-stu-id="8f3e3-191">![subscription&#45;cancel control](./media/api-management-page-controls/APIM-subscription-cancel-control.png "APIM subscription-cancel control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="8f3e3-192">Utilização</span><span class="sxs-lookup"><span data-stu-id="8f3e3-192">Usage</span></span>  
  
```xml  
<subscription-cancel params="{ subscriptionId: '{{subscription.id}}', cancelUrl: '{{subscription.cancelUrl}}' }">  
</subscription-cancel>  
  
```  
  
### <a name="parameters"></a><span data-ttu-id="8f3e3-193">Parâmetros</span><span class="sxs-lookup"><span data-stu-id="8f3e3-193">Parameters</span></span>  
  
|<span data-ttu-id="8f3e3-194">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="8f3e3-194">Parameter</span></span>|<span data-ttu-id="8f3e3-195">Descrição</span><span class="sxs-lookup"><span data-stu-id="8f3e3-195">Description</span></span>|  
|---------------|-----------------|  
|<span data-ttu-id="8f3e3-196">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="8f3e3-196">subscriptionId</span></span>|<span data-ttu-id="8f3e3-197">id de Olá do Olá toocancel de subscrição.</span><span class="sxs-lookup"><span data-stu-id="8f3e3-197">hello id of hello subscription toocancel.</span></span>|  
|<span data-ttu-id="8f3e3-198">cancelUrl</span><span class="sxs-lookup"><span data-stu-id="8f3e3-198">cancelUrl</span></span>|<span data-ttu-id="8f3e3-199">subscrição de Olá Cancelar URL.</span><span class="sxs-lookup"><span data-stu-id="8f3e3-199">hello subscription cancel URL.</span></span>|  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="8f3e3-200">Modelos de portais de programador</span><span class="sxs-lookup"><span data-stu-id="8f3e3-200">Developer portal templates</span></span>  
 <span data-ttu-id="8f3e3-201">Olá `subscription-cancel` controlo pode ser utilizado numa Olá seguintes modelos de portal de programador.</span><span class="sxs-lookup"><span data-stu-id="8f3e3-201">hello `subscription-cancel` control may be used in hello following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="8f3e3-202">Produto</span><span class="sxs-lookup"><span data-stu-id="8f3e3-202">Product</span></span>](api-management-product-templates.md#Product)

## <a name="next-steps"></a><span data-ttu-id="8f3e3-203">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="8f3e3-203">Next steps</span></span>
<span data-ttu-id="8f3e3-204">Para obter mais informações sobre como trabalhar com modelos, consulte [como toocustomize Olá utilizando modelos de portal do Programador de API Management](api-management-developer-portal-templates.md).</span><span class="sxs-lookup"><span data-stu-id="8f3e3-204">For more information about working with templates, see [How toocustomize hello API Management developer portal using templates](api-management-developer-portal-templates.md).</span></span>
