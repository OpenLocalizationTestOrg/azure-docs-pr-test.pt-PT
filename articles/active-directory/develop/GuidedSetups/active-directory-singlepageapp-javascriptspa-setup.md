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
## <a name="setting-up-your-web-server-or-project"></a>Configurar o seu servidor web ou o projeto

> Prefere toodownload projeto este exemplo em vez disso? 
> - [Transferir o projeto do Visual Studio Olá](https://github.com/Azure-Samples/active-directory-javascript-graphapi-v2/archive/VisualStudio.zip)
>
> ou
> - [Transferir ficheiros de projeto Olá](https://github.com/Azure-Samples/active-directory-javascript-graphapi-v2/archive/core.zip) para um servidor local web, como o Python
>
> E, em seguida, avançar toohello [passo da configuração](#create-an-application-express) tooconfigure Olá código de exemplo antes de executá-lo.

## <a name="prerequisites"></a>Pré-requisitos
Um servidor local web como [Python http.server](https://www.python.org/downloads/), [servidor http](https://www.npmjs.com/package/http-server/), [.NET Core](https://www.microsoft.com/net/core), ou IIS Express integração com [Visual Studio 2017](https://www.visualstudio.com/downloads/) é necessário toorun esta configuração orientada. 

As instruções neste guia são baseadas no Python e Visual Studio 2017, mas sentir toouse livre qualquer outro ambiente de desenvolvimento ou de servidor Web.

## <a name="create-your-project"></a>Criar o projeto 

> ### <a name="option-1-visual-studio"></a>Opção 1: Visual Studio 
> Se estiver a utilizar o Visual Studio e estiver a criar um novo projeto, siga os passos de Olá abaixo toocreate uma nova solução do Visual Studio:
> 1.    No Visual Studio:`File` > `New` > `Project`
> 2.    Em `Visual C#\Web`, selecione`ASP.NET Web Application (.NET Framework)`
> 3.    Nome da aplicação e clique em *OK*
> 4.    Em `New ASP.NET Web Application`, selecione`Empty`

<p/><!-- -->

> ### <a name="option-2-python-other-web-servers"></a>Opção 2: Python / outros servidores web
> Certifique-se de que instalou [Python](https://www.python.org/downloads/), em seguida, siga o passo de Olá abaixo:
> - Crie uma pasta toohost a sua aplicação.


## <a name="create-your-single-page-applications-ui"></a>Criar a IU sua aplicação única página
1.  Criar um *index.html* ficheiro para o seu SPA JavaScript. Se estiver a utilizar o Visual Studio, o projeto de Olá selecione (pasta raiz do projeto), clique com o botão direito e selecione: `Add`  >  `New Item`  >  `HTML page` e dê-lhe o nome index.html
2.  Adicione Olá página de códigos de tooyour os seguintes:
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
