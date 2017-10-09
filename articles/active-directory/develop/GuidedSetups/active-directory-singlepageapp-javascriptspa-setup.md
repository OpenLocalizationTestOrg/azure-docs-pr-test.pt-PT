---
title: "aaaAzure AD v2 JS SPA orientado configuração - configuração | Microsoft Docs"
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
ms.openlocfilehash: 19e15c6c8db8bea2975f30e7505af79ccad17e02
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
## <a name="setting-up-your-web-server-or-project"></a><span data-ttu-id="55ee5-103">Configurar o seu servidor web ou o projeto</span><span class="sxs-lookup"><span data-stu-id="55ee5-103">Setting up your web server or project</span></span>

> <span data-ttu-id="55ee5-104">Prefere toodownload projeto este exemplo em vez disso?</span><span class="sxs-lookup"><span data-stu-id="55ee5-104">Prefer toodownload this sample's project instead?</span></span> 
> - [<span data-ttu-id="55ee5-105">Transferir o projeto do Visual Studio Olá</span><span class="sxs-lookup"><span data-stu-id="55ee5-105">Download hello Visual Studio project</span></span>](https://github.com/Azure-Samples/active-directory-javascript-graphapi-v2/archive/VisualStudio.zip)
>
> <span data-ttu-id="55ee5-106">ou</span><span class="sxs-lookup"><span data-stu-id="55ee5-106">or</span></span>
> - <span data-ttu-id="55ee5-107">[Transferir ficheiros de projeto Olá](https://github.com/Azure-Samples/active-directory-javascript-graphapi-v2/archive/core.zip) para um servidor local web, como o Python</span><span class="sxs-lookup"><span data-stu-id="55ee5-107">[Download hello project files](https://github.com/Azure-Samples/active-directory-javascript-graphapi-v2/archive/core.zip) for a local web server, such as Python</span></span>
>
> <span data-ttu-id="55ee5-108">E, em seguida, avançar toohello [passo da configuração](#create-an-application-express) tooconfigure Olá código de exemplo antes de executá-lo.</span><span class="sxs-lookup"><span data-stu-id="55ee5-108">And then  skip toohello [Configuration step](#create-an-application-express) tooconfigure hello code sample before executing it.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="55ee5-109">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="55ee5-109">Prerequisites</span></span>
<span data-ttu-id="55ee5-110">Um servidor local web como [Python http.server](https://www.python.org/downloads/), [servidor http](https://www.npmjs.com/package/http-server/), [.NET Core](https://www.microsoft.com/net/core), ou IIS Express integração com [Visual Studio 2017](https://www.visualstudio.com/downloads/) é necessário toorun esta configuração orientada.</span><span class="sxs-lookup"><span data-stu-id="55ee5-110">A local web server such as [Python http.server](https://www.python.org/downloads/), [http-server](https://www.npmjs.com/package/http-server/), [.NET Core](https://www.microsoft.com/net/core), or IIS Express integration with [Visual Studio 2017](https://www.visualstudio.com/downloads/) is required toorun this guided setup.</span></span> 

<span data-ttu-id="55ee5-111">As instruções neste guia são baseadas no Python e Visual Studio 2017, mas sentir toouse livre qualquer outro ambiente de desenvolvimento ou de servidor Web.</span><span class="sxs-lookup"><span data-stu-id="55ee5-111">Instructions in this guide are based on both Python and Visual Studio 2017, but feel free toouse any other development environment or Web Server.</span></span>

## <a name="create-your-project"></a><span data-ttu-id="55ee5-112">Criar o projeto</span><span class="sxs-lookup"><span data-stu-id="55ee5-112">Create your project</span></span> 

> ### <a name="option-1-visual-studio"></a><span data-ttu-id="55ee5-113">Opção 1: Visual Studio</span><span class="sxs-lookup"><span data-stu-id="55ee5-113">Option 1: Visual Studio</span></span> 
> <span data-ttu-id="55ee5-114">Se estiver a utilizar o Visual Studio e estiver a criar um novo projeto, siga os passos de Olá abaixo toocreate uma nova solução do Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="55ee5-114">If you are using Visual Studio and are creating a new project, follow hello steps below toocreate a new Visual Studio solution:</span></span>
> 1.    <span data-ttu-id="55ee5-115">No Visual Studio:`File` > `New` > `Project`</span><span class="sxs-lookup"><span data-stu-id="55ee5-115">In Visual Studio:  `File` > `New` > `Project`</span></span>
> 2.    <span data-ttu-id="55ee5-116">Em `Visual C#\Web`, selecione`ASP.NET Web Application (.NET Framework)`</span><span class="sxs-lookup"><span data-stu-id="55ee5-116">Under `Visual C#\Web`, select `ASP.NET Web Application (.NET Framework)`</span></span>
> 3.    <span data-ttu-id="55ee5-117">Nome da aplicação e clique em *OK*</span><span class="sxs-lookup"><span data-stu-id="55ee5-117">Name your application and click *OK*</span></span>
> 4.    <span data-ttu-id="55ee5-118">Em `New ASP.NET Web Application`, selecione`Empty`</span><span class="sxs-lookup"><span data-stu-id="55ee5-118">Under `New ASP.NET Web Application`, select `Empty`</span></span>

<p/><!-- -->

> ### <a name="option-2-python-other-web-servers"></a><span data-ttu-id="55ee5-119">Opção 2: Python / outros servidores web</span><span class="sxs-lookup"><span data-stu-id="55ee5-119">Option 2: Python/ other web servers</span></span>
> <span data-ttu-id="55ee5-120">Certifique-se de que instalou [Python](https://www.python.org/downloads/), em seguida, siga o passo de Olá abaixo:</span><span class="sxs-lookup"><span data-stu-id="55ee5-120">Make sure you have installed [Python](https://www.python.org/downloads/), then follow hello step below:</span></span>
> - <span data-ttu-id="55ee5-121">Crie uma pasta toohost a sua aplicação.</span><span class="sxs-lookup"><span data-stu-id="55ee5-121">Create a folder toohost your application.</span></span>


## <a name="create-your-single-page-applications-ui"></a><span data-ttu-id="55ee5-122">Criar a IU sua aplicação única página</span><span class="sxs-lookup"><span data-stu-id="55ee5-122">Create your single page application’s UI</span></span>
1.  <span data-ttu-id="55ee5-123">Criar um *index.html* ficheiro para o seu SPA JavaScript.</span><span class="sxs-lookup"><span data-stu-id="55ee5-123">Create an *index.html* file for your JavaScript SPA.</span></span> <span data-ttu-id="55ee5-124">Se estiver a utilizar o Visual Studio, o projeto de Olá selecione (pasta raiz do projeto), clique com o botão direito e selecione: `Add`  >  `New Item`  >  `HTML page` e dê-lhe o nome index.html</span><span class="sxs-lookup"><span data-stu-id="55ee5-124">If you are using Visual Studio, select hello project (project root folder), right click and select: `Add` > `New Item` > `HTML page` and name it index.html</span></span>
2.  <span data-ttu-id="55ee5-125">Adicione Olá página de códigos de tooyour os seguintes:</span><span class="sxs-lookup"><span data-stu-id="55ee5-125">Add hello following code tooyour page:</span></span>
```html
<!DOCTYPE html>
<html>
<head>
    <!-- bootstrap reference used for styling hello page -->
    <link href="//maxcdn.bootstrapcdn.com/bootstrap/3.3.7/css/bootstrap.min.css" rel="stylesheet">
    <title>JavaScript SPA Guided Setup</title>
</head>
<body style="margin: 40px">
    <button id="callGraphButton" type="button" class="btn btn-primary" onclick="callGraphApi()">Call Microsoft Graph API</button>
    <div id="errorMessage" class="text-danger"></div>
    <div class="hidden">
        <h3>Graph API Call Response</h3>
        <pre class="well" id="graphResponse"></pre>
    </div>
    <div class="hidden">
        <h3>Access Token</h3>
        <pre class="well" id="accessToken"></pre>
    </div>
    <div class="hidden">
        <h3>ID Token Claims</h3>
        <pre class="well" id="userInfo"></pre>
    </div>
    <button id="signOutButton" type="button" class="btn btn-primary hidden" onclick="signOut()">Sign out</button>

    <!-- This app uses cdn tooreference msal.js (recommended). 
         You can also download it from: https://github.com/AzureAD/microsoft-authentication-library-for-js -->
    <script src="https://secure.aadcdn.microsoftonline-p.com/lib/0.1.1/js/msal.min.js"></script>

    <!-- hello 'bluebird' and 'fetch' references below are required if you need toorun this application on Internet Explorer -->
    <script src="https://cdnjs.cloudflare.com/ajax/libs/bluebird/3.3.4/bluebird.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/fetch/2.0.3/fetch.min.js"></script>

    <script type="text/javascript" src="msalconfig.js"></script>
    <script type="text/javascript" src="app.js"></script>
</body>
</html>
````
