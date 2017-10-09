---
title: "aaaAzure AD v2 JS SPA orientado configuração - introdução | Microsoft Docs"
description: "Como aplicações de JavaScript SPA podem chamar uma API que necessitam de tokens de acesso ao ponto final do Azure Active Directory v2"
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
ms.date: 06/01/2017
ms.author: andret
ms.openlocfilehash: 7e4250ccca837a17489a99603da167009cc2e3d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="call-hello-microsoft-graph-api-from-a-javascript-single-page-application-spa"></a><span data-ttu-id="0d374-103">Chamar Olá Microsoft Graph API a partir de um JavaScript única página aplicação (SPA)</span><span class="sxs-lookup"><span data-stu-id="0d374-103">Call hello Microsoft Graph API from a JavaScript Single Page Application (SPA)</span></span>

<span data-ttu-id="0d374-104">Este guia demonstra como uma aplicação JavaScript página única (SPA) pode iniciar sessão no trabalhos pessoais e contas escolares, obter um token de acesso e chamar Olá Microsoft Graph API ou outras APIs que necessitam de tokens de acesso de Olá ponto final do Azure Active Directory v2.</span><span class="sxs-lookup"><span data-stu-id="0d374-104">This guide demonstrates how a JavaScript Single Page Application (SPA) can sign in personal, work and school accounts, get an access token, and call hello Microsoft Graph API or other APIs that require access tokens from hello Azure Active Directory v2 endpoint.</span></span>

### <a name="how-this-guide-works"></a><span data-ttu-id="0d374-105">Como funciona este guia</span><span class="sxs-lookup"><span data-stu-id="0d374-105">How this guide works</span></span>

![Como funciona a aplicação de exemplo de Olá gerada por este guia](media/active-directory-singlepageapp-javascriptspa-introduction/javascriptspa-intro.png)

<!--start-collapse-->
### <a name="more-information"></a><span data-ttu-id="0d374-107">Mais Informações</span><span class="sxs-lookup"><span data-stu-id="0d374-107">More Information</span></span>

<span data-ttu-id="0d374-108">aplicação de exemplo de Olá criada por este guia permite um Olá tooquery de JavaScript SPA Microsoft Graph API ou uma API Web que aceita tokens de ponto final do Azure Active Directory v2.</span><span class="sxs-lookup"><span data-stu-id="0d374-108">hello sample application created by this guide enables a JavaScript SPA tooquery hello Microsoft Graph API or a Web API that accepts tokens from Azure Active Directory v2 endpoint.</span></span> <span data-ttu-id="0d374-109">Para este cenário, depois de um utilizador inicia sessão, um token de acesso é pedidos tooHTTP pedida e foram adicionados através do cabeçalho de autorização de Olá.</span><span class="sxs-lookup"><span data-stu-id="0d374-109">For this scenario, after a user signs-in, an access token is requested and added tooHTTP requests via hello authorization header.</span></span> <span data-ttu-id="0d374-110">Aquisição do token e a renovação são processados pela Olá biblioteca de autenticação da Microsoft (MSAL).</span><span class="sxs-lookup"><span data-stu-id="0d374-110">Token acquisition and renewal are handled by hello Microsoft Authentication Library (MSAL).</span></span>

<!--end-collapse-->

<!--start-collapse-->
### <a name="libraries"></a><span data-ttu-id="0d374-111">Bibliotecas</span><span class="sxs-lookup"><span data-stu-id="0d374-111">Libraries</span></span>

<span data-ttu-id="0d374-112">Este guia utiliza Olá biblioteca os seguintes:</span><span class="sxs-lookup"><span data-stu-id="0d374-112">This guide uses hello following library:</span></span>

|<span data-ttu-id="0d374-113">Biblioteca</span><span class="sxs-lookup"><span data-stu-id="0d374-113">Library</span></span>|<span data-ttu-id="0d374-114">Descrição</span><span class="sxs-lookup"><span data-stu-id="0d374-114">Description</span></span>|
|---|---|
|[<span data-ttu-id="0d374-115">msal.js</span><span class="sxs-lookup"><span data-stu-id="0d374-115">msal.js</span></span>](https://github.com/AzureAD/microsoft-authentication-library-for-js)|<span data-ttu-id="0d374-116">Biblioteca de autenticação da Microsoft para a pré-visualização de JavaScript</span><span class="sxs-lookup"><span data-stu-id="0d374-116">Microsoft Authentication Library for JavaScript Preview</span></span>|

> [!NOTE]
> <span data-ttu-id="0d374-117">*msal.js* Olá destinos *ponto final do Azure Active Directory v2* -que permite a contas pessoal, profissional e escolar toosign no e adquirir tokens.</span><span class="sxs-lookup"><span data-stu-id="0d374-117">*msal.js* targets hello *Azure Active Directory v2 endpoint* - which enables personal, school and work accounts toosign in and acquire tokens.</span></span> <span data-ttu-id="0d374-118">Olá *ponto final do Azure Active Directory v2* tem [algumas limitações](..\active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="0d374-118">hello *Azure Active Directory v2 endpoint* has [some limitations](..\active-directory-v2-limitations.md).</span></span> <span data-ttu-id="0d374-119">Se estiver interessado apenas em contas profissional e escolar, utilize *adal.js* e Olá *V1 endpoint*.</span><span class="sxs-lookup"><span data-stu-id="0d374-119">If you are interested only in school and work accounts, use *adal.js* and hello *V1 endpoint*.</span></span> <span data-ttu-id="0d374-120">toounderstand diferenças entre os pontos finais v1 e v2 de Olá ler Olá [v1 v2 comparação](..\active-directory-v2-compare.md).</span><span class="sxs-lookup"><span data-stu-id="0d374-120">toounderstand differences between hello v1 and v2 endpoints read hello [v1-v2 comparison](..\active-directory-v2-compare.md).</span></span>

<!--end-collapse-->
