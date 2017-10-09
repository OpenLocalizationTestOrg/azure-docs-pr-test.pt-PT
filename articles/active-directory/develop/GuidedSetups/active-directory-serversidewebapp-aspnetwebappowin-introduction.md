---
title: "aaaAzure AD v2 ASP.NET Web Server introdução - introdução | Microsoft Docs"
description: "Implementar Microsoft início de sessão numa solução ASP.NET com uma aplicação de baseadas no browser web tradicional utilizando o padrão de OpenID Connect"
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.assetid: 820acdb7-d316-4c3b-8de9-79df48ba3b06
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andret
ms.custom: aaddev
ms.openlocfilehash: d6449926af2bdad24cbc8e91f74885a08f909103
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="add-sign-in-with-microsoft-tooan-aspnet-web-app"></a><span data-ttu-id="53dd5-103">Adicionar início de sessão com o Microsoft tooan ASP.NET web app</span><span class="sxs-lookup"><span data-stu-id="53dd5-103">Add sign-in with Microsoft tooan ASP.NET web app</span></span>

<span data-ttu-id="53dd5-104">Este guia demonstra como tooimplement início de sessão com a Microsoft através de uma solução de ASP.NET MVC com uma aplicação de baseada no browser tradicional web com OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="53dd5-104">This guide demonstrates how tooimplement sign-in with Microsoft using an ASP.NET MVC solution with a traditional web browser-based application using OpenID Connect.</span></span> 

<span data-ttu-id="53dd5-105">No final de Olá deste guia, a aplicação irá ser tooaccept capazes sessão ins do pessoal contas (incluindo outlook.com, live.com e outros), bem como funcionam contas escolares ou profissionais de qualquer da empresa ou organização que tem integrado com o Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="53dd5-105">At hello end of this guide, your application will be able tooaccept sign ins of personal accounts (including outlook.com, live.com, and others) as well as work and school accounts from any company or organization that has integrated with Azure Active Directory.</span></span> 

> <span data-ttu-id="53dd5-106">Este guia requer o Visual Studio 2015 Update 3 ou Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="53dd5-106">This guide requires Visual Studio 2015 Update 3 or Visual Studio 2017.</span></span>  <span data-ttu-id="53dd5-107">Não o tiver?</span><span class="sxs-lookup"><span data-stu-id="53dd5-107">Don’t have it?</span></span>  [<span data-ttu-id="53dd5-108">Transferir o Visual Studio 2017 gratuitamente</span><span class="sxs-lookup"><span data-stu-id="53dd5-108">Download Visual Studio 2017 for free</span></span>](https://www.visualstudio.com/downloads/)

## <a name="how-this-guide-works"></a><span data-ttu-id="53dd5-109">Como funciona este guia</span><span class="sxs-lookup"><span data-stu-id="53dd5-109">How this guide works</span></span>

![Como funciona este guia](media/active-directory-serversidewebapp-aspnetwebappowin-intro/aspnetbrowsergeneral.png)

<span data-ttu-id="53dd5-111">Este guia baseia-se num cenário de olá onde um browser acede a um web site do ASP.NET, pedindo uma tooauthenticate de utilizador através de um botão de início de sessão.</span><span class="sxs-lookup"><span data-stu-id="53dd5-111">This guide is based on hello scenario where a browser accesses an ASP.NET web site, requesting a user tooauthenticate via a sign-in button.</span></span> <span data-ttu-id="53dd5-112">Neste cenário, a maioria Olá trabalho toorender Olá web página ocorre no lado do servidor de Olá.</span><span class="sxs-lookup"><span data-stu-id="53dd5-112">In this scenario, most of hello work toorender hello web page occurs on hello server side.</span></span>

## <a name="libraries"></a><span data-ttu-id="53dd5-113">Bibliotecas</span><span class="sxs-lookup"><span data-stu-id="53dd5-113">Libraries</span></span>

<span data-ttu-id="53dd5-114">Este guia utiliza Olá bibliotecas os seguintes:</span><span class="sxs-lookup"><span data-stu-id="53dd5-114">This guide uses hello following libraries:</span></span>

|<span data-ttu-id="53dd5-115">Biblioteca</span><span class="sxs-lookup"><span data-stu-id="53dd5-115">Library</span></span>|<span data-ttu-id="53dd5-116">Descrição</span><span class="sxs-lookup"><span data-stu-id="53dd5-116">Description</span></span>|
|---|---|
|[<span data-ttu-id="53dd5-117">Microsoft.Owin.Security.OpenIdConnect</span><span class="sxs-lookup"><span data-stu-id="53dd5-117">Microsoft.Owin.Security.OpenIdConnect</span></span>](https://www.nuget.org/packages/Microsoft.Owin.Security.OpenIdConnect/)|<span data-ttu-id="53dd5-118">Middleware que permite uma aplicação toouse OpenIdConnect para autenticação</span><span class="sxs-lookup"><span data-stu-id="53dd5-118">Middleware that enables an application toouse OpenIdConnect for authentication</span></span>|
|[<span data-ttu-id="53dd5-119">Microsoft.Owin.Security.Cookies</span><span class="sxs-lookup"><span data-stu-id="53dd5-119">Microsoft.Owin.Security.Cookies</span></span>](https://www.nuget.org/packages/Microsoft.Owin.Security.Cookies)|<span data-ttu-id="53dd5-120">Middleware que permite uma sessão de utilizador de toomaintain de aplicação a utilização de cookies</span><span class="sxs-lookup"><span data-stu-id="53dd5-120">Middleware that enables an application toomaintain user session using cookies</span></span>|
|[<span data-ttu-id="53dd5-121">Microsoft.Owin.Host.SystemWeb</span><span class="sxs-lookup"><span data-stu-id="53dd5-121">Microsoft.Owin.Host.SystemWeb</span></span>](https://www.nuget.org/packages/Microsoft.Owin.Host.SystemWeb)|<span data-ttu-id="53dd5-122">Permite que aplicações baseadas em OWIN toorun no IIS através do pipeline de pedido do ASP.NET Olá</span><span class="sxs-lookup"><span data-stu-id="53dd5-122">Enables OWIN-based applications toorun on IIS using hello ASP.NET request pipeline</span></span>|

