---
title: "aaaAzure AD v2 JS SPA orientado o programa de configuração - configurar | Microsoft Docs"
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
ms.openlocfilehash: 1b93298d4bd4e17dd261dbb75502a122c30aac97
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
## <a name="register-your-application"></a><span data-ttu-id="96181-103">Registar a sua aplicação</span><span class="sxs-lookup"><span data-stu-id="96181-103">Register your application</span></span>

<span data-ttu-id="96181-104">Existem várias formas toocreate uma aplicação, selecione um dos atributos:</span><span class="sxs-lookup"><span data-stu-id="96181-104">There are multiple ways toocreate an application, please select one of them:</span></span>

### <a name="option-1-register-your-application-express-mode"></a><span data-ttu-id="96181-105">Opção 1: Registar a sua aplicação (modo Express)</span><span class="sxs-lookup"><span data-stu-id="96181-105">Option 1: Register your application (Express mode)</span></span>
<span data-ttu-id="96181-106">Agora tem tooregister a aplicação no Olá *Portal de registo de aplicações do Microsoft*:</span><span class="sxs-lookup"><span data-stu-id="96181-106">Now you need tooregister your application in hello *Microsoft Application Registration Portal*:</span></span>

1.  <span data-ttu-id="96181-107">Registar a sua aplicação através de Olá [Portal de registo de aplicações do Microsoft](https://apps.dev.microsoft.com/portal/register-app?appType=singlePageApp&appTech=javascriptSpa&step=configure)</span><span class="sxs-lookup"><span data-stu-id="96181-107">Register your application via hello [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/portal/register-app?appType=singlePageApp&appTech=javascriptSpa&step=configure)</span></span>
2.  <span data-ttu-id="96181-108">Introduza um nome para a aplicação e o seu correio eletrónico</span><span class="sxs-lookup"><span data-stu-id="96181-108">Enter a name for your application and your email</span></span>
3.  <span data-ttu-id="96181-109">Certifique-se de que opção de Olá *orientado configuração* está marcada</span><span class="sxs-lookup"><span data-stu-id="96181-109">Make sure hello option for *Guided Setup* is checked</span></span>
4.  <span data-ttu-id="96181-110">Siga o ID da aplicação Olá instruções tooobtain Olá e cole-o para o seu código</span><span class="sxs-lookup"><span data-stu-id="96181-110">Follow hello instructions tooobtain hello application ID and paste it into your code</span></span>

### <a name="option-2-register-your-application-advanced-mode"></a><span data-ttu-id="96181-111">Opção 2: Registar a sua aplicação (modo avançado)</span><span class="sxs-lookup"><span data-stu-id="96181-111">Option 2: Register your application (Advanced mode)</span></span>

1. <span data-ttu-id="96181-112">Aceda toohello [Portal de registo de aplicações do Microsoft](https://apps.dev.microsoft.com/portal/register-app) tooregister uma aplicação</span><span class="sxs-lookup"><span data-stu-id="96181-112">Go toohello [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/portal/register-app) tooregister an application</span></span>
2. <span data-ttu-id="96181-113">Introduza um nome para a aplicação e o seu correio eletrónico</span><span class="sxs-lookup"><span data-stu-id="96181-113">Enter a name for your application and your email</span></span> 
3. <span data-ttu-id="96181-114">Certifique-se de que opção de Olá *orientado configuração* está desmarcada</span><span class="sxs-lookup"><span data-stu-id="96181-114">Make sure hello option for *Guided Setup* is unchecked</span></span>
4.  <span data-ttu-id="96181-115">Clique em `Add Platform`, em seguida, selecione`Web`</span><span class="sxs-lookup"><span data-stu-id="96181-115">Click `Add Platform`, then select `Web`</span></span>
5. <span data-ttu-id="96181-116">Adicionar Olá `Redirect URL` que correspondem o URL da aplicação toohello com base no seu servidor web.</span><span class="sxs-lookup"><span data-stu-id="96181-116">Add hello `Redirect URL` that correspond toohello application's URL based on your web server.</span></span> <span data-ttu-id="96181-117">Consulte as secções de Olá abaixo para obter instruções sobre como tooset / obter o URL de redirecionamento Olá no Visual Studio e Python.</span><span class="sxs-lookup"><span data-stu-id="96181-117">See hello sections below for instructions on how tooset/ obtain hello redirect URL in Visual Studio and Python.</span></span>
6. <span data-ttu-id="96181-118">Clique em *guardar*</span><span class="sxs-lookup"><span data-stu-id="96181-118">Click *Save*</span></span>

> #### <a name="visual-studio-instructions-for-obtaining-redirect-url"></a><span data-ttu-id="96181-119">Visual Studio instruções para obter o URL de redirecionamento</span><span class="sxs-lookup"><span data-stu-id="96181-119">Visual Studio instructions for obtaining redirect URL</span></span>
> <span data-ttu-id="96181-120">Siga o seu URL de redirecionamento de Olá instruções tooobtain:</span><span class="sxs-lookup"><span data-stu-id="96181-120">Follow hello instructions tooobtain your redirect URL:</span></span>
> 1.    <span data-ttu-id="96181-121">No *Explorador de soluções*, selecione o projeto de Olá e observe Olá `Properties` janela (se não for apresentada uma janela de propriedades, prima `F4`)</span><span class="sxs-lookup"><span data-stu-id="96181-121">In *Solution Explorer*, select hello project and look at hello `Properties` window (if you don’t see a Properties window, press `F4`)</span></span>
> 2.    <span data-ttu-id="96181-122">Copie o valor Olá `URL` toohello área de transferência:</span><span class="sxs-lookup"><span data-stu-id="96181-122">Copy hello value from `URL` toohello clipboard:</span></span><br/> <span data-ttu-id="96181-123">![Propriedades do projeto](media/active-directory-singlepageapp-javascriptspa-configure/vs-project-properties-screenshot.png)</span><span class="sxs-lookup"><span data-stu-id="96181-123">![Project properties](media/active-directory-singlepageapp-javascriptspa-configure/vs-project-properties-screenshot.png)</span></span><br />
> 3.    <span data-ttu-id="96181-124">Comutador back toohello *Portal de registo de aplicação* e cole o valor de Olá como um `Redirect URL` e clique em 'Guardar'</span><span class="sxs-lookup"><span data-stu-id="96181-124">Switch back toohello *Application Registration Portal* and paste hello value as a `Redirect URL` and click 'Save'</span></span>

<p/>

> #### <a name="setting-redirect-url-for-python"></a><span data-ttu-id="96181-125">URL de redirecionamento de definição para Python</span><span class="sxs-lookup"><span data-stu-id="96181-125">Setting Redirect URL for Python</span></span>
> <span data-ttu-id="96181-126">Para o Python, pode definir a porta do servidor web Olá através de linha de comandos.</span><span class="sxs-lookup"><span data-stu-id="96181-126">For Python, you can set hello web server port via command line.</span></span> <span data-ttu-id="96181-127">Esta configuração orientada utiliza a porta de Olá 8080 para referência, mas pode toouse livre qualquer porta disponível.</span><span class="sxs-lookup"><span data-stu-id="96181-127">This guided setup uses hello port 8080 for reference but feel free toouse any other port available.</span></span> <span data-ttu-id="96181-128">Em qualquer caso, siga instruções Olá abaixo tooset configurar um URL de redirecionamento nas informações de registo de aplicação Olá:</span><span class="sxs-lookup"><span data-stu-id="96181-128">In any case, follow hello instructions below tooset up a redirect URL in hello application registration information:</span></span><br/>
> - <span data-ttu-id="96181-129">Comutador toohello back- *Portal de registo de aplicação* e defina `http://localhost:8080/` como um `Redirect URL`, ou utilize `http://localhost:[port]/` se estiver a utilizar uma porta TCP personalizada (onde *[porta]* Olá é a porta TCP personalizado número) e clique em 'Guardar'</span><span class="sxs-lookup"><span data-stu-id="96181-129">Switch back toohello *Application Registration Portal* and set `http://localhost:8080/` as a `Redirect URL`, or use `http://localhost:[port]/` if you are using a custom TCP port (where *[port]* is hello custom TCP port number) and click 'Save'</span></span>


#### <a name="configure-your-javascript-spa"></a><span data-ttu-id="96181-130">Configurar o JavaScript SPA</span><span class="sxs-lookup"><span data-stu-id="96181-130">Configure your JavaScript SPA</span></span>

1.  <span data-ttu-id="96181-131">Crie um ficheiro denominado `msalconfig.js` que contém as informações de registo de aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="96181-131">Create a file named `msalconfig.js` containing hello application registration information.</span></span> <span data-ttu-id="96181-132">Se estiver a utilizar o Visual Studio, o projeto de Olá selecione (pasta raiz do projeto), clique com botão direito e selecione: `Add`  >  `New Item`  >  `JavaScript File`.</span><span class="sxs-lookup"><span data-stu-id="96181-132">If you are using Visual Studio, select hello project (project root folder), right-click and select: `Add` > `New Item` > `JavaScript File`.</span></span> <span data-ttu-id="96181-133">Nome`msalconfig.js`</span><span class="sxs-lookup"><span data-stu-id="96181-133">Name it `msalconfig.js`</span></span>
2.  <span data-ttu-id="96181-134">Adicionar Olá seguinte código tooyour `msalconfig.js` ficheiro:</span><span class="sxs-lookup"><span data-stu-id="96181-134">Add hello following code tooyour `msalconfig.js` file:</span></span>

```javascript
var msalconfig = {
    clientID: "Enter_the_Application_Id_here",
    redirectUri: location.origin
};
```
<ol start="3">
<li>
<span data-ttu-id="96181-135">Substitua <code>Enter_the_Application_Id_here</code> com Olá Id da aplicação que acabou de ser registado</span><span class="sxs-lookup"><span data-stu-id="96181-135">Replace <code>Enter_the_Application_Id_here</code> with hello Application Id you just registered</span></span>
</li>
</ol>
