---
title: "aaaAzure AD v2 Android introdução - introdução | Microsoft Docs"
description: "Como uma aplicação Android pode obter um token de acesso e chamar Graph API do Microsoft ou de APIs que necessitam de tokens de acesso a partir do ponto final do Azure Active Directory v2"
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
ms.openlocfilehash: 7c76ab8bbf1a6c934ab672cccf85ae82f03f601a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="call-hello-microsoft-graph-api-from-an-android-app"></a><span data-ttu-id="96ed9-103">Chamar Olá Microsoft Graph API a partir de uma aplicação Android</span><span class="sxs-lookup"><span data-stu-id="96ed9-103">Call hello Microsoft Graph API from an Android app</span></span>

<span data-ttu-id="96ed9-104">Este guia demonstra como uma aplicação Android nativa pode obter um token de acesso e chamar outras APIs que necessitam de tokens de acesso a partir do ponto final do Azure Active Directory v2 ou Microsoft Graph API.</span><span class="sxs-lookup"><span data-stu-id="96ed9-104">This guide demonstrates how a native Android application can get an access token and call Microsoft Graph API or other APIs that require access tokens from Azure Active Directory v2 endpoint.</span></span>

<span data-ttu-id="96ed9-105">No final de Olá deste guia, a aplicação irá ser capaz de toocall uma API protegida com contas pessoais (incluindo outlook.com, live.com e outros), bem como de trabalho e as contas de profissional de qualquer da empresa ou organização que tenha o Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="96ed9-105">At hello end of this guide, your application will be able toocall a protected API using personal accounts (including outlook.com, live.com, and others) as well as work and school accounts from any company or organization that has Azure Active Directory.</span></span>  

### <a name="how-this-sample-works"></a><span data-ttu-id="96ed9-106">Como funciona este exemplo</span><span class="sxs-lookup"><span data-stu-id="96ed9-106">How this sample works</span></span>
![Como funciona este exemplo](media/active-directory-mobileanddesktopapp-android-intro/android-intro.png)

<span data-ttu-id="96ed9-108">exemplo de Olá criado por este guia baseia-se um cenário onde uma aplicação Android é utilizado tooquery uma API Web que aceita tokens a partir do Azure Active Directory v2 endpoint – neste caso, Microsoft Graph API.</span><span class="sxs-lookup"><span data-stu-id="96ed9-108">hello sample created by this guide is based on a scenario where an Android application is used tooquery a Web API that accepts tokens from Azure Active Directory v2 endpoint – in this case, Microsoft Graph API.</span></span> <span data-ttu-id="96ed9-109">Neste cenário, um token é adicionado tooHTTP pedidos através do cabeçalho de autorização de Olá.</span><span class="sxs-lookup"><span data-stu-id="96ed9-109">For this scenario, a token is added tooHTTP requests via hello Authorization header.</span></span> <span data-ttu-id="96ed9-110">Aquisição do token e a renovação é processado pelo Olá biblioteca de autenticação da Microsoft (MSAL).</span><span class="sxs-lookup"><span data-stu-id="96ed9-110">Token acquisition and renewal is handled by hello Microsoft Authentication Library (MSAL).</span></span>

### <a name="pre-requisites"></a><span data-ttu-id="96ed9-111">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="96ed9-111">Pre-requisites</span></span>
* <span data-ttu-id="96ed9-112">Esta configuração orientada concentra-se no Android Studio, mas qualquer outro ambiente de desenvolvimento de uma aplicação Android também é aceitável.</span><span class="sxs-lookup"><span data-stu-id="96ed9-112">This guided setup is focused on Android Studio, but any other Android application development environment is also acceptable.</span></span> 
* <span data-ttu-id="96ed9-113">É necessário o Android SDK 21 ou mais recente (recomenda-se SDK 25).</span><span class="sxs-lookup"><span data-stu-id="96ed9-113">Android SDK 21 or newer is required (SDK 25 is recommended).</span></span>
* <span data-ttu-id="96ed9-114">Google Chrome ou um browser utilizando separadores personalizada é necessário para esta versão da biblioteca de autenticação da Microsoft (MSAL) para Android.</span><span class="sxs-lookup"><span data-stu-id="96ed9-114">Google Chrome or a web browser using Custom Tabs is required for this release of Microsoft Authentication Library (MSAL) for Android.</span></span>

> <span data-ttu-id="96ed9-115">Nota: Google Chrome não está incluído no Visual Studio emulador do Android.</span><span class="sxs-lookup"><span data-stu-id="96ed9-115">Note: Google Chrome is not included on Visual Studio Emulator for Android.</span></span> <span data-ttu-id="96ed9-116">Recomendamos que tootest este código um emulador com API 25 ou uma imagem com API 21 ou mais recente que tem com o Google Chrome instalada.</span><span class="sxs-lookup"><span data-stu-id="96ed9-116">We recommend you tootest this code on an Emulator with API 25 or an image with API 21 or newer that has with Google Chrome installed.</span></span>


### <a name="how-toohandle-token-acquisition-tooaccess-a-protected-web-api"></a><span data-ttu-id="96ed9-117">Como toohandle token aquisição tooaccess uma API Web protegida</span><span class="sxs-lookup"><span data-stu-id="96ed9-117">How toohandle token acquisition tooaccess a protected Web API</span></span>

<span data-ttu-id="96ed9-118">Depois do utilizador Olá efetua a autenticação, a aplicação de exemplo de Olá recebe um token que pode ser utilizado tooquery Microsoft Graph API ou uma API Web protegida pelo Microsoft Azure Active Directory v2.</span><span class="sxs-lookup"><span data-stu-id="96ed9-118">After hello user authenticates, hello sample application receives a token that can be used tooquery Microsoft Graph API or a Web API secured by Microsoft Azure Active Directory v2.</span></span>

<span data-ttu-id="96ed9-119">APIs, tais como o Microsoft Graph requerem um tooallow de token de acesso a aceder a recursos específicos – por exemplo, tooread um perfil de utilizador, aceder ao calendário do utilizador ou enviem um e-mail.</span><span class="sxs-lookup"><span data-stu-id="96ed9-119">APIs such as Microsoft Graph require an access token tooallow accessing specific resources – for example, tooread a user’s profile, access user’s calendar or send an email.</span></span> <span data-ttu-id="96ed9-120">A aplicação pode pedir um token de acesso utilizando MSAL tooaccess estes recursos especificar âmbitos de API.</span><span class="sxs-lookup"><span data-stu-id="96ed9-120">Your application can request an access token using MSAL tooaccess these resources by specifying API scopes.</span></span> <span data-ttu-id="96ed9-121">Este token de acesso é, em seguida, adicionado toohello cabeçalho de autorização de HTTP para cada chamada realizada em Olá recurso protegido.</span><span class="sxs-lookup"><span data-stu-id="96ed9-121">This access token is then added toohello HTTP Authorization header for every call made against hello protected resource.</span></span> 

<span data-ttu-id="96ed9-122">MSAL gere a colocação em cache e atualizar os tokens de acesso para si, pelo que não tem da aplicação.</span><span class="sxs-lookup"><span data-stu-id="96ed9-122">MSAL manages caching and refreshing access tokens for you, so your application doesn't need to.</span></span>

### <a name="libraries"></a><span data-ttu-id="96ed9-123">Bibliotecas</span><span class="sxs-lookup"><span data-stu-id="96ed9-123">Libraries</span></span>

<span data-ttu-id="96ed9-124">Este guia utiliza Olá bibliotecas os seguintes:</span><span class="sxs-lookup"><span data-stu-id="96ed9-124">This guide uses hello following libraries:</span></span>

|<span data-ttu-id="96ed9-125">Biblioteca</span><span class="sxs-lookup"><span data-stu-id="96ed9-125">Library</span></span>|<span data-ttu-id="96ed9-126">Descrição</span><span class="sxs-lookup"><span data-stu-id="96ed9-126">Description</span></span>|
|---|---|
|[<span data-ttu-id="96ed9-127">com.microsoft.Identity.Client</span><span class="sxs-lookup"><span data-stu-id="96ed9-127">com.microsoft.identity.client</span></span>](http://javadoc.io/doc/com.microsoft.identity.client/msal)|<span data-ttu-id="96ed9-128">Biblioteca de autenticação da Microsoft (MSAL)</span><span class="sxs-lookup"><span data-stu-id="96ed9-128">Microsoft Authentication Library (MSAL)</span></span>|
