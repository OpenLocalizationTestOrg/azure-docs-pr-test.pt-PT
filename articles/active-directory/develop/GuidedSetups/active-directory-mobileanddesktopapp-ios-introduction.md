---
title: "aaaAzure AD v2 iOS introdução - introdução | Microsoft Docs"
description: "Como as aplicações do iOS (Swift) podem chamar uma API que necessitam de tokens de acesso ao ponto final do Azure Active Directory v2"
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andret
ms.openlocfilehash: f40aebbb75490912e533aecc7eedfb2b2dcd8c6c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="call-hello-microsoft-graph-api-from-an-ios-app"></a><span data-ttu-id="fc5d5-103">Chamar Olá Microsoft Graph API a partir de uma aplicação iOS</span><span class="sxs-lookup"><span data-stu-id="fc5d5-103">Call hello Microsoft Graph API from an iOS app</span></span>

<span data-ttu-id="fc5d5-104">Este guia demonstra como uma aplicação nativa do iOS (Swift) pode obter o token de acesso e chamar Olá Microsoft Graph API ou outras APIs que necessitam de tokens de acesso a partir do ponto final do Azure Active Directory v2.</span><span class="sxs-lookup"><span data-stu-id="fc5d5-104">This guide demonstrates how a native iOS application (Swift) can get an access token and call hello Microsoft Graph API or other APIs that require access tokens from Azure Active Directory v2 endpoint.</span></span>

<span data-ttu-id="fc5d5-105">No final de Olá deste guia, a aplicação irá ser capaz de toocall uma API protegida com contas pessoais (incluindo outlook.com, live.com e outros), bem como de trabalho e as contas de profissional de qualquer da empresa ou organização que tenha o Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="fc5d5-105">At hello end of this guide, your application will be able toocall a protected API using personal accounts (including outlook.com, live.com, and others) as well as work and school accounts from any company or organization that has Azure Active Directory.</span></span>

> ### <a name="pre-requisites"></a><span data-ttu-id="fc5d5-106">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="fc5d5-106">Pre-requisites</span></span>
> - <span data-ttu-id="fc5d5-107">XCode 8. x é necessário para este guia.</span><span class="sxs-lookup"><span data-stu-id="fc5d5-107">XCode 8.x is required for this guide.</span></span> <span data-ttu-id="fc5d5-108">Pode transferir o XCode [aqui](https://geo.itunes.apple.com/us/app/xcode/id497799835?mt=12 "XCode transferir URL").</span><span class="sxs-lookup"><span data-stu-id="fc5d5-108">You can download XCode [from here](https://geo.itunes.apple.com/us/app/xcode/id497799835?mt=12 "XCode Download URL").</span></span>
> - <span data-ttu-id="fc5d5-109">[Carthage](https://github.com/Carthage/Carthage) para gestão de pacotes</span><span class="sxs-lookup"><span data-stu-id="fc5d5-109">[Carthage](https://github.com/Carthage/Carthage) for package management</span></span>

### <a name="how-this-guide-works"></a><span data-ttu-id="fc5d5-110">Como funciona este guia</span><span class="sxs-lookup"><span data-stu-id="fc5d5-110">How this guide works</span></span>

![Como funciona este guia](media/active-directory-mobileanddesktopapp-ios-introduction/iosintro.png)

<span data-ttu-id="fc5d5-112">aplicação de exemplo de Olá criada por este guia permite um Olá de tooquery de aplicação iOS Microsoft Graph API ou uma API Web que aceita tokens de ponto final do Azure Active Directory v2.</span><span class="sxs-lookup"><span data-stu-id="fc5d5-112">hello sample application created by this guide enables an iOS application tooquery hello Microsoft Graph API or a Web API that accepts tokens from Azure Active Directory v2 endpoint.</span></span> <span data-ttu-id="fc5d5-113">Neste cenário, um token é adicionado tooHTTP pedidos através do cabeçalho de autorização de Olá.</span><span class="sxs-lookup"><span data-stu-id="fc5d5-113">For this scenario, a token is added tooHTTP requests via hello Authorization header.</span></span> <span data-ttu-id="fc5d5-114">Aquisição do token e a renovação é processado pelo Olá biblioteca de autenticação da Microsoft (MSAL).</span><span class="sxs-lookup"><span data-stu-id="fc5d5-114">Token acquisition and renewal is handled by hello Microsoft Authentication Library (MSAL).</span></span>


### <a name="handling-token-acquisition-for-accessing-protected-web-apis"></a><span data-ttu-id="fc5d5-115">Processamento de aquisição de token para aceder ao protegidos APIs da Web</span><span class="sxs-lookup"><span data-stu-id="fc5d5-115">Handling token acquisition for accessing protected Web APIs</span></span>

<span data-ttu-id="fc5d5-116">Depois do utilizador Olá efetua a autenticação, a aplicação de exemplo de Olá recebe um token que pode ser utilizados tooquery Olá Microsoft Graph API ou uma API Web protegida pelo Microsoft Azure Active Directory v2.</span><span class="sxs-lookup"><span data-stu-id="fc5d5-116">After hello user authenticates, hello sample application receives a token that can be used tooquery hello Microsoft Graph API or a Web API secured by Microsoft Azure Active Directory v2.</span></span>

<span data-ttu-id="fc5d5-117">APIs, tais como o Microsoft Graph requerem um tooallow de token de acesso a aceder a recursos específicos – por exemplo, tooread um perfil de utilizador, aceder ao calendário do utilizador ou enviem um e-mail.</span><span class="sxs-lookup"><span data-stu-id="fc5d5-117">APIs such as Microsoft Graph require an access token tooallow accessing specific resources – for example, tooread a user’s profile, access user’s calendar or send an email.</span></span> <span data-ttu-id="fc5d5-118">A aplicação pode pedir um token de acesso utilizando MSAL especificando âmbitos de API.</span><span class="sxs-lookup"><span data-stu-id="fc5d5-118">Your application can request an access token using MSAL by specifying API scopes.</span></span> <span data-ttu-id="fc5d5-119">Este token de acesso é, em seguida, adicionado toohello cabeçalho de autorização de HTTP para cada chamada realizada em Olá recurso protegido.</span><span class="sxs-lookup"><span data-stu-id="fc5d5-119">This access token is then added toohello HTTP Authorization header for every call made against hello protected resource.</span></span>

<span data-ttu-id="fc5d5-120">MSAL gere a colocação em cache e atualizar os tokens de acesso para si, pelo que não tem da aplicação.</span><span class="sxs-lookup"><span data-stu-id="fc5d5-120">MSAL manages caching and refreshing access tokens for you, so your application doesn't need to.</span></span>


### <a name="nuget-packages"></a><span data-ttu-id="fc5d5-121">Pacotes NuGet</span><span class="sxs-lookup"><span data-stu-id="fc5d5-121">NuGet packages</span></span>

<span data-ttu-id="fc5d5-122">Este guia utiliza Olá pacotes NuGet os seguintes:</span><span class="sxs-lookup"><span data-stu-id="fc5d5-122">This guide uses hello following NuGet packages:</span></span>

|<span data-ttu-id="fc5d5-123">Biblioteca</span><span class="sxs-lookup"><span data-stu-id="fc5d5-123">Library</span></span>|<span data-ttu-id="fc5d5-124">Descrição</span><span class="sxs-lookup"><span data-stu-id="fc5d5-124">Description</span></span>|
|---|---|
|[<span data-ttu-id="fc5d5-125">MSAL.framework</span><span class="sxs-lookup"><span data-stu-id="fc5d5-125">MSAL.framework</span></span>](https://github.com/AzureAD/microsoft-authentication-library-for-objc)|<span data-ttu-id="fc5d5-126">Pré-visualização biblioteca de autenticação de Microsoft para iOS</span><span class="sxs-lookup"><span data-stu-id="fc5d5-126">Microsoft Authentication Library Preview for iOS</span></span>|

