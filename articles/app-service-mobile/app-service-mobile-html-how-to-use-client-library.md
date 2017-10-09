---
title: "aaaHow tooUse Olá JavaScript SDK de Mobile Apps do Azure"
description: Como v tooUse para Mobile Apps do Azure
services: app-service\mobile
documentationcenter: javascript
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 53b78965-caa3-4b22-bb67-5bd5c19d03c4
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: html
ms.devlang: javascript
ms.topic: article
ms.date: 10/30/2016
ms.author: glenga
ms.openlocfilehash: 3fcbb0c5bd6918a285bdafa1946ba0bd47bb21b0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-javascript-client-library-for-azure-mobile-apps"></a><span data-ttu-id="be51f-103">Como tooUse hello a biblioteca de cliente JavaScript para Mobile Apps do Azure</span><span class="sxs-lookup"><span data-stu-id="be51f-103">How tooUse hello JavaScript client library for Azure Mobile Apps</span></span>
[!INCLUDE [app-service-mobile-selector-client-library](../../includes/app-service-mobile-selector-client-library.md)]

<span data-ttu-id="be51f-104">Este guia informa tooperform cenários comuns utilizando Olá mais recente [JavaScript SDK de Mobile Apps do Azure].</span><span class="sxs-lookup"><span data-stu-id="be51f-104">This guide teaches you tooperform common scenarios using hello latest [JavaScript SDK for Azure Mobile Apps].</span></span> <span data-ttu-id="be51f-105">Se for novo tooAzure Mobile Apps, primeiro conclua [Azure Mobile Apps início rápido] toocreate um back-end e criar uma tabela.</span><span class="sxs-lookup"><span data-stu-id="be51f-105">If you are new tooAzure Mobile Apps, first complete [Azure Mobile Apps Quick Start] toocreate a backend and create a table.</span></span> <span data-ttu-id="be51f-106">Neste guia, iremos focar-se sobre como utilizar o back-end móvel Olá nas aplicações Web HTML/JavaScript.</span><span class="sxs-lookup"><span data-stu-id="be51f-106">In this guide, we focus on using hello mobile backend in HTML/JavaScript Web applications.</span></span>

## <a name="supported-platforms"></a><span data-ttu-id="be51f-107">Plataformas suportadas</span><span class="sxs-lookup"><span data-stu-id="be51f-107">Supported platforms</span></span>
<span data-ttu-id="be51f-108">Estamos a limitar browser suporte toohello atual e a última versões do Olá browsers principais: Google Chrome, o Microsoft Edge, o Microsoft Internet Explorer e o Mozilla Firefox.</span><span class="sxs-lookup"><span data-stu-id="be51f-108">We limit browser support toohello current and last versions of hello major browsers:  Google Chrome, Microsoft Edge, Microsoft Internet Explorer, and Mozilla Firefox.</span></span>  <span data-ttu-id="be51f-109">Esperamos Olá SDK toofunction com qualquer browser relativamente moderna.</span><span class="sxs-lookup"><span data-stu-id="be51f-109">We expect hello SDK toofunction with any relatively modern browser.</span></span>

<span data-ttu-id="be51f-110">pacote de Olá é distribuído como um módulo de JavaScript Universal, para que suporta globais, AMD, e CommonJS formatos.</span><span class="sxs-lookup"><span data-stu-id="be51f-110">hello package is distributed as a Universal JavaScript Module, so it supports globals, AMD, and CommonJS formats.</span></span>

## <span data-ttu-id="be51f-111"><a name="Setup"></a>A configuração e pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="be51f-111"><a name="Setup"></a>Setup and prerequisites</span></span>
<span data-ttu-id="be51f-112">Este guia pressupõe que criou um back-end com uma tabela.</span><span class="sxs-lookup"><span data-stu-id="be51f-112">This guide assumes that you have created a backend with a table.</span></span> <span data-ttu-id="be51f-113">Este guia pressupõe que tabela Olá tem Olá mesmo esquema como tabelas Olá estes tutoriais.</span><span class="sxs-lookup"><span data-stu-id="be51f-113">This guide assumes that hello table has hello same schema as hello tables in those tutorials.</span></span>

<span data-ttu-id="be51f-114">Instalar Olá JavaScript SDK do Azure Mobile Apps pode ser feito através de Olá `npm` comando:</span><span class="sxs-lookup"><span data-stu-id="be51f-114">Installing hello Azure Mobile Apps JavaScript SDK can be done via hello `npm` command:</span></span>

```
npm install azure-mobile-apps-client --save
```

<span data-ttu-id="be51f-115">biblioteca de Olá também pode ser utilizada como um módulo de ES2015, dentro de ambientes de CommonJS como Browserify e Webpack e como uma biblioteca AMD.</span><span class="sxs-lookup"><span data-stu-id="be51f-115">hello library can also be used as an ES2015 module, within CommonJS environments such as Browserify and Webpack and as an AMD library.</span></span>  <span data-ttu-id="be51f-116">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="be51f-116">For example:</span></span>

```
# For ECMAScript 5.1 CommonJS
var WindowsAzure = require('azure-mobile-apps-client');
# For ES2015 modules
import * as WindowsAzure from 'azure-mobile-apps-client';
```

<span data-ttu-id="be51f-117">Também pode utilizar uma versão de Olá SDK pré-criadas transferindo-a diretamente a partir do nosso CDN:</span><span class="sxs-lookup"><span data-stu-id="be51f-117">You can also use a pre-built version of hello SDK by downloading directly from our CDN:</span></span>

```html
<script src="https://zumo.blob.core.windows.net/sdk/azure-mobile-apps-client.min.js"></script>
```

[!INCLUDE [app-service-mobile-html-js-library](../../includes/app-service-mobile-html-js-library.md)]

## <span data-ttu-id="be51f-118"><a name="auth"></a>Como: autenticar os utilizadores</span><span class="sxs-lookup"><span data-stu-id="be51f-118"><a name="auth"></a>How to: Authenticate users</span></span>
<span data-ttu-id="be51f-119">App Service do Azure suporta autenticar e autorizar utilizadores de aplicações através de vários fornecedores de identidade externas: Facebook, Google, Account Microsoft e Twitter.</span><span class="sxs-lookup"><span data-stu-id="be51f-119">Azure App Service supports authenticating and authorizing app users using various external identity providers: Facebook, Google, Microsoft Account, and Twitter.</span></span> <span data-ttu-id="be51f-120">Pode definir permissões de acesso de toorestrict tabelas para operações específicas tooonly autenticada utilizadores.</span><span class="sxs-lookup"><span data-stu-id="be51f-120">You can set permissions on tables toorestrict access for specific operations tooonly authenticated users.</span></span> <span data-ttu-id="be51f-121">Também pode utilizar a identidade de Olá utilizadores autenticados tooimplement das regras de autorização em scripts de servidor.</span><span class="sxs-lookup"><span data-stu-id="be51f-121">You can also use hello identity of authenticated users tooimplement authorization rules in server scripts.</span></span> <span data-ttu-id="be51f-122">Para obter mais informações, consulte Olá [introdução à autenticação] tutorial.</span><span class="sxs-lookup"><span data-stu-id="be51f-122">For more information, see hello [Get started with authentication] tutorial.</span></span>

<span data-ttu-id="be51f-123">São suportados dois fluxos de autenticação: um fluxo de servidor e um fluxo de cliente.</span><span class="sxs-lookup"><span data-stu-id="be51f-123">Two authentication flows are supported: a server flow and a client flow.</span></span>  <span data-ttu-id="be51f-124">fluxo de servidor Olá fornece a experiência de autenticação mais simples de Olá, como baseia-se na interface de autenticação de web do fornecedor de Olá.</span><span class="sxs-lookup"><span data-stu-id="be51f-124">hello server flow provides hello simplest authentication experience, as it relies on hello provider's web authentication interface.</span></span> <span data-ttu-id="be51f-125">Olá fluxo de cliente permite para uma integração mais profunda com as capacidades específicas do dispositivo, tal como single-sign-on como depende SDKs específica do fornecedor.</span><span class="sxs-lookup"><span data-stu-id="be51f-125">hello client flow allows for deeper integration with device-specific capabilities such as single-sign-on as it relies on provider-specific SDKs.</span></span>

[!INCLUDE [app-service-mobile-html-js-auth-library](../../includes/app-service-mobile-html-js-auth-library.md)]

### <span data-ttu-id="be51f-126"><a name="configure-external-redirect-urls"></a>Como: configurar o serviço de aplicações móveis para os URLs de redirecionamento externo.</span><span class="sxs-lookup"><span data-stu-id="be51f-126"><a name="configure-external-redirect-urls"></a>How to: Configure your Mobile App Service for external redirect URLs.</span></span>
<span data-ttu-id="be51f-127">Vários tipos de aplicações de JavaScript utilizam um toohandle de capacidade de loopback que flui de IU de OAuth.</span><span class="sxs-lookup"><span data-stu-id="be51f-127">Several types of JavaScript applications use a loopback capability toohandle OAuth UI flows.</span></span>  <span data-ttu-id="be51f-128">Estas funcionalidades incluem:</span><span class="sxs-lookup"><span data-stu-id="be51f-128">These capabilities include:</span></span>

* <span data-ttu-id="be51f-129">Executar o serviço localmente</span><span class="sxs-lookup"><span data-stu-id="be51f-129">Running your service locally</span></span>
* <span data-ttu-id="be51f-130">Utilizar recarregar em direto com Olá Ionic Framework</span><span class="sxs-lookup"><span data-stu-id="be51f-130">Using Live Reload with hello Ionic Framework</span></span>
* <span data-ttu-id="be51f-131">Redirecionar tooApp serviço para a autenticação.</span><span class="sxs-lookup"><span data-stu-id="be51f-131">Redirecting tooApp Service for authentication.</span></span>

<span data-ttu-id="be51f-132">Executar localmente pode causar problemas, porque, por predefinição, a autenticação é apenas de serviço de aplicações configurado o acesso de tooallow de back-end da aplicação móvel.</span><span class="sxs-lookup"><span data-stu-id="be51f-132">Running locally can cause problems because, by default, App Service authentication is only configured tooallow access from your Mobile App backend.</span></span> <span data-ttu-id="be51f-133">Utilize Olá ao executar o servidor de Olá localmente os seguintes passos toochange Olá autenticação de tooenable de definições do serviço de aplicações:</span><span class="sxs-lookup"><span data-stu-id="be51f-133">Use hello following steps toochange hello App Service settings tooenable authentication when running hello server locally:</span></span>

1. <span data-ttu-id="be51f-134">Inicie sessão no toohello [portal do Azure]</span><span class="sxs-lookup"><span data-stu-id="be51f-134">Log in toohello [Azure portal]</span></span>
2. <span data-ttu-id="be51f-135">Navegue tooyour back-end da aplicação móvel.</span><span class="sxs-lookup"><span data-stu-id="be51f-135">Navigate tooyour Mobile App backend.</span></span>
3. <span data-ttu-id="be51f-136">Selecione **Explorador de recursos** no Olá **ferramentas de desenvolvimento** menu.</span><span class="sxs-lookup"><span data-stu-id="be51f-136">Select **Resource explorer** in hello **DEVELOPMENT TOOLS** menu.</span></span>
4. <span data-ttu-id="be51f-137">Clique em **aceda** Explorador de recursos de Olá tooopen de back-end da aplicação móvel num novo separador ou janela.</span><span class="sxs-lookup"><span data-stu-id="be51f-137">Click **Go** tooopen hello resource explorer for your Mobile App backend in a new tab or window.</span></span>
5. <span data-ttu-id="be51f-138">Expanda Olá **configuração** > **authsettings** nós para a sua aplicação.</span><span class="sxs-lookup"><span data-stu-id="be51f-138">Expand hello **config** > **authsettings** node for your app.</span></span>
6. <span data-ttu-id="be51f-139">Clique em Olá **editar** botão Editar tooenable do recurso de Olá.</span><span class="sxs-lookup"><span data-stu-id="be51f-139">Click hello **Edit** button tooenable editing of hello resource.</span></span>
7. <span data-ttu-id="be51f-140">Determinar Olá **allowedExternalRedirectUrls** elemento, que deve ser nulo.</span><span class="sxs-lookup"><span data-stu-id="be51f-140">Find hello **allowedExternalRedirectUrls** element, which should be null.</span></span> <span data-ttu-id="be51f-141">Adicione os URLs de uma matriz:</span><span class="sxs-lookup"><span data-stu-id="be51f-141">Add your URLs in an array:</span></span>

         "allowedExternalRedirectUrls": [
             "http://localhost:3000",
             "https://localhost:3000"
         ],

    <span data-ttu-id="be51f-142">Substitua os URLs de Olá na matriz de Olá Olá URLs do seu serviço, que, neste exemplo, é `http://localhost:3000` para o serviço de exemplo de Node.js Olá local.</span><span class="sxs-lookup"><span data-stu-id="be51f-142">Replace hello URLs in hello array with hello URLs of your service, which in this example is `http://localhost:3000` for hello local Node.js sample service.</span></span> <span data-ttu-id="be51f-143">Pode também utilizar `http://localhost:4400` Olá Ripple para ou de serviço outro URL, dependendo de como a aplicação está configurada.</span><span class="sxs-lookup"><span data-stu-id="be51f-143">You could also use `http://localhost:4400` for hello Ripple service or some other URL, depending on how your app is configured.</span></span>
8. <span data-ttu-id="be51f-144">Na Olá parte superior da página Olá, clique em **leitura/escrita**, em seguida, clique em **colocar** toosave as atualizações.</span><span class="sxs-lookup"><span data-stu-id="be51f-144">At hello top of hello page, click **Read/Write**, then click **PUT** toosave your updates.</span></span>

<span data-ttu-id="be51f-145">Também precisa de tooadd Olá mesmas loopback URLs toohello definições CORS da lista branca:</span><span class="sxs-lookup"><span data-stu-id="be51f-145">You also need tooadd hello same loopback URLs toohello CORS whitelist settings:</span></span>

1. <span data-ttu-id="be51f-146">Navegue back toohello [portal do Azure].</span><span class="sxs-lookup"><span data-stu-id="be51f-146">Navigate back toohello [Azure portal].</span></span>
2. <span data-ttu-id="be51f-147">Navegue tooyour back-end da aplicação móvel.</span><span class="sxs-lookup"><span data-stu-id="be51f-147">Navigate tooyour Mobile App backend.</span></span>
3. <span data-ttu-id="be51f-148">Clique em **CORS** no Olá **API** menu.</span><span class="sxs-lookup"><span data-stu-id="be51f-148">Click **CORS** in hello **API** menu.</span></span>
4. <span data-ttu-id="be51f-149">Introduza cada URL Olá vazio **origens permitidas** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="be51f-149">Enter each URL in hello empty **Allowed Origins** text box.</span></span>  <span data-ttu-id="be51f-150">É criada uma nova caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="be51f-150">A new text box is created.</span></span>
5. <span data-ttu-id="be51f-151">Clique em **guardar**</span><span class="sxs-lookup"><span data-stu-id="be51f-151">Click **SAVE**</span></span>

<span data-ttu-id="be51f-152">Depois de atualizações de back-end de Olá, será capaz de toouse Olá loopback novos URLs na sua aplicação.</span><span class="sxs-lookup"><span data-stu-id="be51f-152">After hello backend updates, you will be able toouse hello new loopback URLs in your app.</span></span>

<!-- URLs. -->
[Azure Mobile Apps início rápido]: app-service-mobile-cordova-get-started.md
[introdução à autenticação]: app-service-mobile-cordova-get-started-users.md
[Add authentication tooyour app]: app-service-mobile-cordova-get-started-users.md

[portal do Azure]: https://portal.azure.com/
[JavaScript SDK de Mobile Apps do Azure]: https://www.npmjs.com/package/azure-mobile-apps-client
[Query object documentation]: https://msdn.microsoft.com/en-us/library/azure/jj613353.aspx
