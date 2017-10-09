---
title: "aaaAzure AD Cordova introdução | Microsoft Docs"
description: "Como toobuild uma aplicação Cordova que se integra com o Azure AD para início de sessão e chama APIs do Azure AD protegida utilizando OAuth."
services: active-directory
documentationcenter: 
author: vibronet
manager: mbaldwin
editor: 
ms.assetid: b1a8d7bd-7ad6-44d5-8ccb-5255bb623345
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: article
ms.date: 01/07/2017
ms.author: vittorib
ms.custom: aaddev
ms.openlocfilehash: 573ed638c2180c5231648bcb8c49ceb6f53296f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-ad-with-an-apache-cordova-app"></a><span data-ttu-id="355da-103">Integrar o Azure AD com um Apache aplicação Cordova</span><span class="sxs-lookup"><span data-stu-id="355da-103">Integrate Azure AD with an Apache Cordova app</span></span>
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

<span data-ttu-id="355da-104">Pode utilizar o Apache Cordova toodevelop HTML5/JavaScript as aplicações que podem ser executadas em dispositivos móveis, como aplicações nativas totalmente funcional.</span><span class="sxs-lookup"><span data-stu-id="355da-104">You can use Apache Cordova toodevelop HTML5/JavaScript applications that can run on mobile devices as full-fledged native applications.</span></span> <span data-ttu-id="355da-105">Com o Azure Active Directory (Azure AD), pode adicionar aplicações de Cordova de tooyour de capacidades de autenticação de nível empresarial.</span><span class="sxs-lookup"><span data-stu-id="355da-105">With Azure Active Directory (Azure AD), you can add enterprise-grade authentication capabilities tooyour Cordova applications.</span></span>

<span data-ttu-id="355da-106">Um plug-in de Cordova encapsula num wrapper do Azure AD SDKs nativas no iOS, Android, Loja Windows e Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="355da-106">A Cordova plug-in wraps Azure AD native SDKs on iOS, Android, Windows Store, and Windows Phone.</span></span> <span data-ttu-id="355da-107">Ao utilizar que Plug-in, pode melhorar a sua aplicação toosupport início de sessão com contas do Windows Server Active Directory dos utilizadores, obter acesso tooOffice 365 e APIs do Azure e, inclusivamente ajudar a proteger chamadas tooyour própria personalizado API web.</span><span class="sxs-lookup"><span data-stu-id="355da-107">By using that plug-in, you can enhance your application toosupport sign-in with your users' Windows Server Active Directory accounts, gain access tooOffice 365 and Azure APIs, and even help protect calls tooyour own custom web API.</span></span>

<span data-ttu-id="355da-108">Neste tutorial, iremos utilizar Olá Apache Cordova Plug-in para o Active Directory Authentication Library (ADAL) tooimprove uma aplicação simples adicionando Olá seguintes funcionalidades:</span><span class="sxs-lookup"><span data-stu-id="355da-108">In this tutorial, we'll use hello Apache Cordova plug-in for Active Directory Authentication Library (ADAL) tooimprove a simple app by adding hello following features:</span></span>

* <span data-ttu-id="355da-109">Com apenas alguns linhas de código, autenticar um utilizador e obter um token.</span><span class="sxs-lookup"><span data-stu-id="355da-109">With just a few lines of code, authenticate a user and obtain a token.</span></span>
* <span data-ttu-id="355da-110">Utilize essa tooquery de Graph API do token tooinvoke Olá nesse diretório e apresentar resultados de Olá.</span><span class="sxs-lookup"><span data-stu-id="355da-110">Use that token tooinvoke hello Graph API tooquery that directory and display hello results.</span></span>  
* <span data-ttu-id="355da-111">Utilize a autenticação de toominimize de cache de token ADAL Olá pede ao utilizador Olá.</span><span class="sxs-lookup"><span data-stu-id="355da-111">Use hello ADAL token cache toominimize authentication prompts for hello user.</span></span>

<span data-ttu-id="355da-112">toomake essas melhorias, tem de:</span><span class="sxs-lookup"><span data-stu-id="355da-112">toomake those improvements, you need to:</span></span>

1. <span data-ttu-id="355da-113">Registar uma aplicação com o Azure AD.</span><span class="sxs-lookup"><span data-stu-id="355da-113">Register an application with Azure AD.</span></span>
2. <span data-ttu-id="355da-114">Adicione tokens de toorequest do código tooyour aplicação.</span><span class="sxs-lookup"><span data-stu-id="355da-114">Add code tooyour app toorequest tokens.</span></span>
3. <span data-ttu-id="355da-115">Adicionar código toouse Olá token para consultas Olá Graph API e ver os resultados.</span><span class="sxs-lookup"><span data-stu-id="355da-115">Add code toouse hello token for querying hello Graph API and display results.</span></span>
4. <span data-ttu-id="355da-116">Criar o projeto de implementação de Cordova Olá com todas as plataformas de Olá pretende tootarget, adicionar Olá Cordova ADAL Plug-in e testar a solução de Olá emuladores.</span><span class="sxs-lookup"><span data-stu-id="355da-116">Create hello Cordova deployment project with all hello platforms you want tootarget, add hello Cordova ADAL plug-in, and test hello solution in emulators.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="355da-117">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="355da-117">Prerequisites</span></span>
<span data-ttu-id="355da-118">toocomplete neste tutorial, precisa de:</span><span class="sxs-lookup"><span data-stu-id="355da-118">toocomplete this tutorial, you need:</span></span>

* <span data-ttu-id="355da-119">Um inquilino do Azure AD em que tenha uma conta com direitos de desenvolvimento de aplicações.</span><span class="sxs-lookup"><span data-stu-id="355da-119">An Azure AD tenant where you have an account with app development rights.</span></span>
* <span data-ttu-id="355da-120">Ambiente de desenvolvimento que tenha configurado toouse Apache Cordova.</span><span class="sxs-lookup"><span data-stu-id="355da-120">A development environment that's configured toouse Apache Cordova.</span></span>  

<span data-ttu-id="355da-121">Se ainda tiver ambos configurar, avançar diretamente toostep 1.</span><span class="sxs-lookup"><span data-stu-id="355da-121">If you have both already set up, proceed directly toostep 1.</span></span>

<span data-ttu-id="355da-122">Se não tiver um inquilino do Azure AD, utilize Olá [instruções sobre como tooget um](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="355da-122">If you don't have an Azure AD tenant, use hello [instructions on how tooget one](active-directory-howto-tenant.md).</span></span>

<span data-ttu-id="355da-123">Se não tiver Apache Cordova configurar no seu computador, instale o seguinte Olá:</span><span class="sxs-lookup"><span data-stu-id="355da-123">If you don't have Apache Cordova set up on your machine, install hello following:</span></span>

* [<span data-ttu-id="355da-124">Git</span><span class="sxs-lookup"><span data-stu-id="355da-124">Git</span></span>](http://git-scm.com/book/en/v2/Getting-Started-Installing-Git)
* [<span data-ttu-id="355da-125">Node.js</span><span class="sxs-lookup"><span data-stu-id="355da-125">Node.js</span></span>](https://nodejs.org/download/)
* <span data-ttu-id="355da-126">[Cordova CLI](https://cordova.apache.org/) (pode ser facilmente instalado através do Gestor de pacote NPM: `npm install -g cordova`)</span><span class="sxs-lookup"><span data-stu-id="355da-126">[Cordova CLI](https://cordova.apache.org/) (can be easily installed via NPM package manager: `npm install -g cordova`)</span></span>

<span data-ttu-id="355da-127">Olá precedente instalações deverão funcionar tanto no Olá PC na Olá Mac.</span><span class="sxs-lookup"><span data-stu-id="355da-127">hello preceding installations should work both on hello PC and on hello Mac.</span></span>

<span data-ttu-id="355da-128">Cada plataforma de destino apresenta diferentes pré-requisitos:</span><span class="sxs-lookup"><span data-stu-id="355da-128">Each target platform has different prerequisites:</span></span>

* <span data-ttu-id="355da-129">toobuild e executar uma aplicação para Windows Tablet/PC ou Windows Phone:</span><span class="sxs-lookup"><span data-stu-id="355da-129">toobuild and run an app for Windows Tablet/PC or Windows Phone:</span></span>
  * <span data-ttu-id="355da-130">Instalar [Visual Studio 2013 para Windows com a atualização 2 ou posterior](http://www.visualstudio.com/downloads/download-visual-studio-vs#d-express-windows-8) (rápida ou outra versão) ou [Visual Studio 2015](https://www.visualstudio.com/downloads/download-visual-studio-vs#d-community).</span><span class="sxs-lookup"><span data-stu-id="355da-130">Install [Visual Studio 2013 for Windows with Update 2 or later](http://www.visualstudio.com/downloads/download-visual-studio-vs#d-express-windows-8) (Express or another version) or [Visual Studio 2015](https://www.visualstudio.com/downloads/download-visual-studio-vs#d-community).</span></span>

* <span data-ttu-id="355da-131">toobuild e execute uma aplicação para iOS:</span><span class="sxs-lookup"><span data-stu-id="355da-131">toobuild and run an app for iOS:</span></span>

  * <span data-ttu-id="355da-132">Instalar Xcode 6. x ou posterior.</span><span class="sxs-lookup"><span data-stu-id="355da-132">Install Xcode 6.x or later.</span></span> <span data-ttu-id="355da-133">Transferência a partir da Olá [site Apple Developer](http://developer.apple.com/downloads) ou Olá [Mac App Store](http://itunes.apple.com/us/app/xcode/id497799835?mt=12).</span><span class="sxs-lookup"><span data-stu-id="355da-133">Download it from hello [Apple Developer site](http://developer.apple.com/downloads) or hello [Mac App Store](http://itunes.apple.com/us/app/xcode/id497799835?mt=12).</span></span>
  * <span data-ttu-id="355da-134">Instalar [ios-sim](https://www.npmjs.org/package/ios-sim).</span><span class="sxs-lookup"><span data-stu-id="355da-134">Install [ios-sim](https://www.npmjs.org/package/ios-sim).</span></span> <span data-ttu-id="355da-135">Pode utilizá-lo aplicações de iOS toostart no simulador iOS Olá linha de comandos.</span><span class="sxs-lookup"><span data-stu-id="355da-135">You can use it toostart iOS apps in iOS Simulator from hello command line.</span></span> <span data-ttu-id="355da-136">(Pode instalá-lo facilmente através de Olá terminal: `npm install -g ios-sim`.)</span><span class="sxs-lookup"><span data-stu-id="355da-136">(You can easily install it via hello terminal: `npm install -g ios-sim`.)</span></span>
* <span data-ttu-id="355da-137">toobuild e executar uma aplicação para Android:</span><span class="sxs-lookup"><span data-stu-id="355da-137">toobuild and run an app for Android:</span></span>

  * <span data-ttu-id="355da-138">Instalar [Kit de desenvolvimento Java (JDK) 7](http://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) ou posterior.</span><span class="sxs-lookup"><span data-stu-id="355da-138">Install [Java Development Kit (JDK) 7](http://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) or later.</span></span> <span data-ttu-id="355da-139">Certifique-se `JAVA_HOME` (variável de ambiente) está corretamente definida de acordo com caminho de instalação do JDK toohello (por exemplo, c:\Programas\Microsoft Files\Java\jdk1.7.0_75).</span><span class="sxs-lookup"><span data-stu-id="355da-139">Make sure `JAVA_HOME` (environment variable) is correctly set according toohello JDK installation path (for example, C:\Program Files\Java\jdk1.7.0_75).</span></span>
  * <span data-ttu-id="355da-140">Instalar [Android SDK](http://developer.android.com/sdk/installing/index.html?pkg=tools) e adicione Olá `<android-sdk-location>\tools` localização (por exemplo, C:\tools\Android\android-sdk\tools) tooyour `PATH` variável de ambiente.</span><span class="sxs-lookup"><span data-stu-id="355da-140">Install [Android SDK](http://developer.android.com/sdk/installing/index.html?pkg=tools) and add hello `<android-sdk-location>\tools` location (for example, C:\tools\Android\android-sdk\tools) tooyour `PATH` environment variable.</span></span>
  * <span data-ttu-id="355da-141">Abra o Gestor do Android SDK (por exemplo, através de Olá terminal: `android`) e instalar:</span><span class="sxs-lookup"><span data-stu-id="355da-141">Open Android SDK Manager (for example, via hello terminal: `android`) and install:</span></span>
    * <span data-ttu-id="355da-142">*Android 5.0.1 (API 21)* plataforma SDK</span><span class="sxs-lookup"><span data-stu-id="355da-142">*Android 5.0.1 (API 21)* platform SDK</span></span>
    * <span data-ttu-id="355da-143">*Ferramentas de criação de SDK Android* versão 19.1.0 ou posterior</span><span class="sxs-lookup"><span data-stu-id="355da-143">*Android SDK Build Tools* version 19.1.0 or later</span></span>
    * <span data-ttu-id="355da-144">*Suporte Android repositório* (Extras)</span><span class="sxs-lookup"><span data-stu-id="355da-144">*Android Support Repository* (Extras)</span></span>

  <span data-ttu-id="355da-145">Olá Android SDK não fornece qualquer instância de emulador predefinido.</span><span class="sxs-lookup"><span data-stu-id="355da-145">hello Android SDK doesn't provide any default emulator instance.</span></span> <span data-ttu-id="355da-146">Crie um executando `android avd` Olá terminal e, em seguida, selecionar **criar**, se pretender toorun Olá aplicação Android num emulador.</span><span class="sxs-lookup"><span data-stu-id="355da-146">Create one by running `android avd` from hello terminal and then selecting **Create**, if you want toorun hello Android app on an emulator.</span></span> <span data-ttu-id="355da-147">Recomendamos um nível de API de 19 ou superior.</span><span class="sxs-lookup"><span data-stu-id="355da-147">We recommend an API level of 19 or higher.</span></span> <span data-ttu-id="355da-148">Para mais informações sobre opções de emulador e a criação de Android no Olá, consulte [Gestor de AVD](http://developer.android.com/tools/help/avd-manager.html) no site do Android Olá.</span><span class="sxs-lookup"><span data-stu-id="355da-148">For more information about hello Android emulator and creation options, see [AVD Manager](http://developer.android.com/tools/help/avd-manager.html) on hello Android site.</span></span>

## <a name="step-1-register-an-application-with-azure-ad"></a><span data-ttu-id="355da-149">Passo 1: Registar uma aplicação com o Azure AD</span><span class="sxs-lookup"><span data-stu-id="355da-149">Step 1: Register an application with Azure AD</span></span>
<span data-ttu-id="355da-150">Este passo é opcional.</span><span class="sxs-lookup"><span data-stu-id="355da-150">This step is optional.</span></span> <span data-ttu-id="355da-151">Este tutorial fornece pré-aprovisionada valores que pode utilizar toosee Olá exemplo na ação sem efetuar qualquer aprovisionamento no seu próprio inquilino.</span><span class="sxs-lookup"><span data-stu-id="355da-151">This tutorial provides pre-provisioned values that you can use toosee hello sample in action without doing any provisioning in your own tenant.</span></span> <span data-ttu-id="355da-152">No entanto, recomendamos que execute este passo e se familiarize com o processo de Olá, porque irá ser necessário quando criar as suas próprias aplicações.</span><span class="sxs-lookup"><span data-stu-id="355da-152">However, we recommend that you do perform this step and become familiar with hello process, because it will be required when you create your own applications.</span></span>

<span data-ttu-id="355da-153">O Azure AD emite tooonly de tokens conhecidos aplicações.</span><span class="sxs-lookup"><span data-stu-id="355da-153">Azure AD issues tokens tooonly known applications.</span></span> <span data-ttu-id="355da-154">Antes de poder utilizar o Azure AD da sua aplicação, terá de toocreate uma entrada para o mesmo no seu inquilino.</span><span class="sxs-lookup"><span data-stu-id="355da-154">Before you can use Azure AD from your app, you need toocreate an entry for it in your tenant.</span></span> <span data-ttu-id="355da-155">tooregister uma nova aplicação no seu inquilino:</span><span class="sxs-lookup"><span data-stu-id="355da-155">tooregister a new application in your tenant:</span></span>

1. <span data-ttu-id="355da-156">Inicie sessão no toohello [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="355da-156">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="355da-157">Na barra superior Olá, clique em sua conta.</span><span class="sxs-lookup"><span data-stu-id="355da-157">On hello top bar, click your account.</span></span> <span data-ttu-id="355da-158">No Olá **diretório** lista, escolha inquilino Olá do Azure AD, onde pretende tooregister a aplicação.</span><span class="sxs-lookup"><span data-stu-id="355da-158">In hello **Directory** list, choose hello Azure AD tenant where you want tooregister your application.</span></span>
3. <span data-ttu-id="355da-159">Clique em **mais serviços** no Olá painel esquerdo e, em seguida, selecione **do Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="355da-159">Click **More Services** in hello left pane, and then select **Azure Active Directory**.</span></span>
4. <span data-ttu-id="355da-160">Clique em **registos de aplicação**e, em seguida, selecione **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="355da-160">Click **App registrations**, and then select **Add**.</span></span>
5. <span data-ttu-id="355da-161">Siga as instruções de Olá e criar um **aplicação cliente nativa**.</span><span class="sxs-lookup"><span data-stu-id="355da-161">Follow hello prompts and create a **Native Client Application**.</span></span> <span data-ttu-id="355da-162">(Embora aplicações Cordova HTML com base, estamos a criar uma aplicação cliente nativa aqui.</span><span class="sxs-lookup"><span data-stu-id="355da-162">(Although Cordova apps are HTML based, we're creating a native client application here.</span></span> <span data-ttu-id="355da-163">Olá **aplicação cliente nativa** tem de selecionar a opção ou aplicação Olá não funcionará.)</span><span class="sxs-lookup"><span data-stu-id="355da-163">hello **Native Client Application** option must be selected, or hello application won't work.)</span></span>
  * <span data-ttu-id="355da-164">**Nome** descreve toousers sua aplicação.</span><span class="sxs-lookup"><span data-stu-id="355da-164">**Name** describes your application toousers.</span></span>
  * <span data-ttu-id="355da-165">**URI de redirecionamento** é Olá URI que tenha utilizado tooreturn tokens tooyour aplicação.</span><span class="sxs-lookup"><span data-stu-id="355da-165">**Redirect URI** is hello URI that's used tooreturn tokens tooyour app.</span></span> <span data-ttu-id="355da-166">Introduza **http://MyDirectorySearcherApp**.</span><span class="sxs-lookup"><span data-stu-id="355da-166">Enter **http://MyDirectorySearcherApp**.</span></span>

<span data-ttu-id="355da-167">Depois de concluir o registo, o Azure AD atribui uma aplicação de tooyour de ID de aplicação único.</span><span class="sxs-lookup"><span data-stu-id="355da-167">After you finish registration, Azure AD assigns a unique application ID tooyour app.</span></span> <span data-ttu-id="355da-168">Irá precisar deste valor nas secções seguintes Olá.</span><span class="sxs-lookup"><span data-stu-id="355da-168">You’ll need this value in hello next sections.</span></span> <span data-ttu-id="355da-169">Pode encontrá-lo no separador de aplicação Olá de Olá aplicação criada recentemente.</span><span class="sxs-lookup"><span data-stu-id="355da-169">You can find it on hello application tab of hello newly created app.</span></span>

<span data-ttu-id="355da-170">toorun `DirSearchClient Sample`, conceder Olá recém-criado aplicação permissão tooquery Olá AD Graph API do Azure:</span><span class="sxs-lookup"><span data-stu-id="355da-170">toorun `DirSearchClient Sample`, grant hello newly created app permission tooquery hello Azure AD Graph API:</span></span>

1. <span data-ttu-id="355da-171">De Olá **definições** página, selecione **permissões obrigatórias**e, em seguida, selecione **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="355da-171">From hello **Settings** page, select **Required Permissions**, and then select **Add**.</span></span>  
2. <span data-ttu-id="355da-172">Para Olá aplicação Azure Active Directory, selecione **Microsoft Graph** como Olá API e adicione Olá **acesso ao diretório de Olá como utilizador com sessão iniciada Olá** permissão em **delegados Permissões**.</span><span class="sxs-lookup"><span data-stu-id="355da-172">For hello Azure Active Directory application, select **Microsoft Graph** as hello API and add hello **Access hello directory as hello signed-in user** permission under **Delegated Permissions**.</span></span>  <span data-ttu-id="355da-173">Isto permite que o seu Olá tooquery da aplicação Graph API para os utilizadores.</span><span class="sxs-lookup"><span data-stu-id="355da-173">This enables your application tooquery hello Graph API for users.</span></span>

## <a name="step-2-clone-hello-sample-app-repository"></a><span data-ttu-id="355da-174">Passo 2: Clonar o repositório de aplicação de exemplo de Olá</span><span class="sxs-lookup"><span data-stu-id="355da-174">Step 2: Clone hello sample app repository</span></span>
<span data-ttu-id="355da-175">A partir da shell ou a linha de comandos, escreva Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="355da-175">From your shell or command line, type hello following command:</span></span>

    git clone -b skeleton https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-Cordova.git

## <a name="step-3-create-hello-cordova-app"></a><span data-ttu-id="355da-176">Passo 3: Criar a aplicação Cordova de Olá</span><span class="sxs-lookup"><span data-stu-id="355da-176">Step 3: Create hello Cordova app</span></span>
<span data-ttu-id="355da-177">Existem várias formas o toocreate Cordova aplicações.</span><span class="sxs-lookup"><span data-stu-id="355da-177">There are multiple ways toocreate Cordova applications.</span></span> <span data-ttu-id="355da-178">Neste tutorial, iremos utilizar o interface de linha de comandos do Olá Cordova (CLI).</span><span class="sxs-lookup"><span data-stu-id="355da-178">In this tutorial, we'll use hello Cordova command-line interface (CLI).</span></span>

1. <span data-ttu-id="355da-179">A partir da shell ou a linha de comandos, escreva Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="355da-179">From your shell or command line, type hello following command:</span></span>

        cordova create DirSearchClient

   <span data-ttu-id="355da-180">Este comando cria estrutura de pastas de Olá e andaime para o projeto Cordova de Olá.</span><span class="sxs-lookup"><span data-stu-id="355da-180">That command creates hello folder structure and scaffolding for hello Cordova project.</span></span>

2. <span data-ttu-id="355da-181">Mova toohello nova DirSearchClient pasta:</span><span class="sxs-lookup"><span data-stu-id="355da-181">Move toohello new DirSearchClient folder:</span></span>

        cd .\DirSearchClient

3. <span data-ttu-id="355da-182">Copie o conteúdo de Olá do projeto de arranque Olá na subpasta de www Olá utilizando um Gestor de ficheiros ou Olá seguinte comando na sua shell:</span><span class="sxs-lookup"><span data-stu-id="355da-182">Copy hello content of hello starter project in hello www subfolder by using a file manager or hello following command in your shell:</span></span>

  * <span data-ttu-id="355da-183">Windows:`xcopy ..\NativeClient-MultiTarget-Cordova\DirSearchClient www /E /Y`</span><span class="sxs-lookup"><span data-stu-id="355da-183">Windows: `xcopy ..\NativeClient-MultiTarget-Cordova\DirSearchClient www /E /Y`</span></span>
  * <span data-ttu-id="355da-184">MAC:`cp -r  ../NativeClient-MultiTarget-Cordova/DirSearchClient/* www`</span><span class="sxs-lookup"><span data-stu-id="355da-184">Mac: `cp -r  ../NativeClient-MultiTarget-Cordova/DirSearchClient/* www`</span></span>

4. <span data-ttu-id="355da-185">Adicione a lista branca Olá Plug-in.</span><span class="sxs-lookup"><span data-stu-id="355da-185">Add hello whitelist plug-in.</span></span> <span data-ttu-id="355da-186">Isto é necessário para invocar Olá Graph API.</span><span class="sxs-lookup"><span data-stu-id="355da-186">This is necessary for invoking hello Graph API.</span></span>

        cordova plugin add cordova-plugin-whitelist

5. <span data-ttu-id="355da-187">Adicione todas as plataformas de Olá que pretende que o toosupport.</span><span class="sxs-lookup"><span data-stu-id="355da-187">Add all hello platforms that you want toosupport.</span></span> <span data-ttu-id="355da-188">toohave uma amostra de trabalho, terá de tooexecute pelo menos um dos seguintes comandos de Olá.</span><span class="sxs-lookup"><span data-stu-id="355da-188">toohave a working sample, you need tooexecute at least one of hello following commands.</span></span> <span data-ttu-id="355da-189">Tenha em atenção que não ser capaz de tooemulate iOS no Windows ou emular Windows num Mac.</span><span class="sxs-lookup"><span data-stu-id="355da-189">Note that you won't be able tooemulate iOS on Windows or emulate Windows on a Mac.</span></span>

        cordova platform add android
        cordova platform add ios
        cordova platform add windows

6. <span data-ttu-id="355da-190">Adicione Olá ADAL para o projeto de tooyour Plug-in Cordova:</span><span class="sxs-lookup"><span data-stu-id="355da-190">Add hello ADAL for Cordova plug-in tooyour project:</span></span>

        cordova plugin add cordova-plugin-ms-adal

## <a name="step-4-add-code-tooauthenticate-users-and-obtain-tokens-from-azure-ad"></a><span data-ttu-id="355da-191">Passo 4: Adicionar código tooauthenticate utilizadores e obter os tokens do Azure AD</span><span class="sxs-lookup"><span data-stu-id="355da-191">Step 4: Add code tooauthenticate users and obtain tokens from Azure AD</span></span>
<span data-ttu-id="355da-192">aplicação Olá que estiver a desenvolver neste tutorial, irá fornecer uma funcionalidade de pesquisa de diretório simples.</span><span class="sxs-lookup"><span data-stu-id="355da-192">hello application that you're developing in this tutorial will provide a simple directory search feature.</span></span> <span data-ttu-id="355da-193">utilizador Olá pode, em seguida, escreva o alias de Olá de qualquer utilizador no diretório de Olá e visualizar alguns atributos básicos.</span><span class="sxs-lookup"><span data-stu-id="355da-193">hello user can then type hello alias of any user in hello directory and visualize some basic attributes.</span></span> <span data-ttu-id="355da-194">projeto de arranque Olá contém uma definição de Olá da interface de utilizador básico Olá da aplicação Olá (em www/index.html) e andaime Olá que cablagem um evento de aplicações básica ciclos, enlaces de interface de utilizador e apresentar lógica (www/js/index.js) de resultados.</span><span class="sxs-lookup"><span data-stu-id="355da-194">hello starter project contains hello definition of hello basic user interface of hello app (in www/index.html) and hello scaffolding that wires up basic app event cycles, user interface bindings, and results display logic (in www/js/index.js).</span></span> <span data-ttu-id="355da-195">Olá apenas restantes para a tarefa está lógica de Olá tooadd que implementa as tarefas de identidade.</span><span class="sxs-lookup"><span data-stu-id="355da-195">hello only task left for you is tooadd hello logic that implements identity tasks.</span></span>

<span data-ttu-id="355da-196">Olá primeira coisa que precisa de toodo no seu código é introduzir os valores de protocolo de Olá que utiliza o Azure AD para identificar a sua aplicação e Olá recursos que o destino.</span><span class="sxs-lookup"><span data-stu-id="355da-196">hello first thing you need toodo in your code is introduce hello protocol values that Azure AD uses for identifying your app and hello resources that you target.</span></span> <span data-ttu-id="355da-197">Esses valores serão utilizados tooconstruct Olá pedidos de token mais tarde.</span><span class="sxs-lookup"><span data-stu-id="355da-197">Those values will be used tooconstruct hello token requests later on.</span></span> <span data-ttu-id="355da-198">Inserir Olá fragmento, Olá parte superior do ficheiro de index.js Olá os seguintes:</span><span class="sxs-lookup"><span data-stu-id="355da-198">Insert hello following snippet at hello top of hello index.js file:</span></span>

```javascript
var authority = "https://login.microsoftonline.com/common",
    redirectUri = "http://MyDirectorySearcherApp",
    resourceUri = "https://graph.windows.net",
    clientId = "a5d92493-ae5a-4a9f-bcbf-9f1d354067d3",
    graphApiVersion = "2013-11-08";
```

<span data-ttu-id="355da-199">Olá `redirectUri` e `clientId` valores devem corresponder ao valores Olá que descrevem a sua aplicação no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="355da-199">hello `redirectUri` and `clientId` values should match hello values that describe your app in Azure AD.</span></span> <span data-ttu-id="355da-200">Pode encontrar as do Olá **configurar** separador Olá portal do Azure, como descrito no passo 1, anteriormente neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="355da-200">You can find those from hello **Configure** tab in hello Azure portal, as described in step 1 earlier in this tutorial.</span></span>

> [!NOTE]
> <span data-ttu-id="355da-201">Se tiver optado por não registar uma nova aplicação no seu próprio inquilino, pode colar simplesmente valores Olá pré-configurada como está.</span><span class="sxs-lookup"><span data-stu-id="355da-201">If you opted for not registering a new app in your own tenant, you can simply paste hello preconfigured values as is.</span></span> <span data-ttu-id="355da-202">Em seguida, pode ver que executar o exemplo Olá, embora sempre deve criar sua própria entrada para as aplicações que se destinam para produção.</span><span class="sxs-lookup"><span data-stu-id="355da-202">You can then see hello sample running, though you should always create your own entry for your apps that are meant for production.</span></span>

<span data-ttu-id="355da-203">Em seguida, adicione o código de pedido de token de Olá.</span><span class="sxs-lookup"><span data-stu-id="355da-203">Next, add hello token request code.</span></span> <span data-ttu-id="355da-204">Inserir Olá seguinte fragmento entre Olá `search` e `renderData` definições:</span><span class="sxs-lookup"><span data-stu-id="355da-204">Insert hello following snippet between hello `search` and `renderData` definitions:</span></span>

```javascript
    // Shows hello user authentication dialog box if required
    authenticate: function (authCompletedCallback) {

        app.context = new Microsoft.ADAL.AuthenticationContext(authority);
        app.context.tokenCache.readItems().then(function (items) {
            if (items.length > 0) {
                authority = items[0].authority;
                app.context = new Microsoft.ADAL.AuthenticationContext(authority);
            }
            // Attempt tooauthorize hello user silently
            app.context.acquireTokenSilentAsync(resourceUri, clientId)
            .then(authCompletedCallback, function () {
                // We require user credentials, so this triggers hello authentication dialog box
                app.context.acquireTokenAsync(resourceUri, clientId, redirectUri)
                .then(authCompletedCallback, function (err) {
                    app.error("Failed tooauthenticate: " + err);
                });
            });
        });

    },
```
<span data-ttu-id="355da-205">Vamos examinar essa função ao eliminar-a para baixo em duas partes principais.</span><span class="sxs-lookup"><span data-stu-id="355da-205">Let's examine that function by breaking it down in its two main parts.</span></span>
<span data-ttu-id="355da-206">Este exemplo está concebida toowork com nenhum inquilino, como toobeing oposição ao associada tooa um determinado.</span><span class="sxs-lookup"><span data-stu-id="355da-206">This sample is designed toowork with any tenant, as opposed toobeing tied tooa particular one.</span></span> <span data-ttu-id="355da-207">Utiliza Olá "/ comuns" ponto final, que permite Olá utilizador tooenter qualquer conta no momento de autenticação e direciona o inquilino de toohello Olá pedido onde pertence.</span><span class="sxs-lookup"><span data-stu-id="355da-207">It uses hello "/common" endpoint, which allows hello user tooenter any account at authentication time and directs hello request toohello tenant where it belongs.</span></span>

<span data-ttu-id="355da-208">Esta primeira parte do método Olá inspeciona Olá ADAL cache toosee se um token já está armazenado.</span><span class="sxs-lookup"><span data-stu-id="355da-208">This first part of hello method inspects hello ADAL cache toosee if a token is already stored.</span></span> <span data-ttu-id="355da-209">Se Sim, o método de Olá utiliza inquilinos olá onde o token de Olá provém para reinicializar ADAL.</span><span class="sxs-lookup"><span data-stu-id="355da-209">If so, hello method uses hello tenants where hello token came from for reinitializing ADAL.</span></span> <span data-ttu-id="355da-210">Isto é necessário tooavoid pedidos adicionais, porque Olá utilização de "/ comuns" sempre resulta num perguntar Olá utilizador tooenter uma nova conta.</span><span class="sxs-lookup"><span data-stu-id="355da-210">This is necessary tooavoid extra prompts, because hello use of "/common" always results in asking hello user tooenter a new account.</span></span>

```javascript
        app.context = new Microsoft.ADAL.AuthenticationContext(authority);
        app.context.tokenCache.readItems().then(function (items) {
            if (items.length > 0) {
                authority = items[0].authority;
                app.context = new Microsoft.ADAL.AuthenticationContext(authority);
            }
```
<span data-ttu-id="355da-211">Olá segunda parte método Olá efetua o pedido de token adequada Olá.</span><span class="sxs-lookup"><span data-stu-id="355da-211">hello second part of hello method performs hello proper token request.</span></span> <span data-ttu-id="355da-212">Olá `acquireTokenSilentAsync` método pede-lhe ADAL tooreturn um token Olá especificado recurso sem qualquer UX. a mostrar</span><span class="sxs-lookup"><span data-stu-id="355da-212">hello `acquireTokenSilentAsync` method asks ADAL tooreturn a token for hello specified resource without showing any UX.</span></span> <span data-ttu-id="355da-213">Que pode acontecer se a cache de Olá já tem um token de acesso adequado armazenado, ou se um token de atualização pode ser utilizados tooget um novo token de acesso sem que mostra a qualquer linha de comandos.</span><span class="sxs-lookup"><span data-stu-id="355da-213">That can happen if hello cache already has a suitable access token stored, or if a refresh token can be used tooget a new access token without showing any prompt.</span></span> <span data-ttu-id="355da-214">Se que a tentativa falhar, iremos reverter `acquireTokenAsync`– que irá solicitar visibly Olá tooauthenticate de utilizador.</span><span class="sxs-lookup"><span data-stu-id="355da-214">If that attempt fails, we fall back on `acquireTokenAsync`--which will visibly prompt hello user tooauthenticate.</span></span>

```javascript
            // Attempt tooauthorize hello user silently
            app.context.acquireTokenSilentAsync(resourceUri, clientId)
            .then(authCompletedCallback, function () {
                // We require user credentials, so this triggers hello authentication dialog box
                app.context.acquireTokenAsync(resourceUri, clientId, redirectUri)
                .then(authCompletedCallback, function (err) {
                    app.error("Failed tooauthenticate: " + err);
                });
            });
```
<span data-ttu-id="355da-215">Agora que temos o token de Olá, iremos finally pode invocar Olá Graph API e executar a consulta de pesquisa de Olá que queremos.</span><span class="sxs-lookup"><span data-stu-id="355da-215">Now that we have hello token, we can finally invoke hello Graph API and perform hello search query that we want.</span></span> <span data-ttu-id="355da-216">Inserir Olá seguinte fragmento abaixo Olá `authenticate` definição:</span><span class="sxs-lookup"><span data-stu-id="355da-216">Insert hello following snippet below hello `authenticate` definition:</span></span>

```javascript
// Makes an API call tooreceive hello user list
    requestData: function (authResult, searchText) {
        var req = new XMLHttpRequest();
        var url = resourceUri + "/" + authResult.tenantId + "/users?api-version=" + graphApiVersion;
        url = searchText ? url + "&$filter=mailNickname eq '" + searchText + "'" : url + "&$top=10";

        req.open("GET", url, true);
        req.setRequestHeader('Authorization', 'Bearer ' + authResult.accessToken);

        req.onload = function(e) {
            if (e.target.status >= 200 && e.target.status < 300) {
                app.renderData(JSON.parse(e.target.response));
                return;
            }
            app.error('Data request failed: ' + e.target.response);
        };
        req.onerror = function(e) {
            app.error('Data request failed: ' + e.error);
        }

        req.send();
    },

```
<span data-ttu-id="355da-217">ficheiros do ponto inicial de Olá indicado um UX simple para introduzir o alias do utilizador na caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="355da-217">hello starting-point files supplied a simple UX for entering a user's alias in a text box.</span></span> <span data-ttu-id="355da-218">Este método utiliza esse valor tooconstruct uma consulta, combiná-la com o token de acesso de Olá, envia-as tooMicrosoft gráfico e analisar os resultados de Olá.</span><span class="sxs-lookup"><span data-stu-id="355da-218">This method uses that value tooconstruct a query, combine it with hello access token, send it tooMicrosoft Graph, and parse hello results.</span></span> <span data-ttu-id="355da-219">Olá `renderData` método, já está presente no ficheiro de ponto inicial de Olá, trata-se de visualizar os resultados de Olá.</span><span class="sxs-lookup"><span data-stu-id="355da-219">hello `renderData` method, already present in hello starting-point file, takes care of visualizing hello results.</span></span>

## <a name="step-5-run-hello-app"></a><span data-ttu-id="355da-220">Passo 5: Executar a aplicação Olá</span><span class="sxs-lookup"><span data-stu-id="355da-220">Step 5: Run hello app</span></span>
<span data-ttu-id="355da-221">A aplicação está toorun finally pronto.</span><span class="sxs-lookup"><span data-stu-id="355da-221">Your app is finally ready toorun.</span></span> <span data-ttu-id="355da-222">Funcionamento é simple: quando inicia a aplicação Olá, introduza alias Olá do utilizador Olá pretende toolook cópias de segurança e, em seguida, clique no botão de Olá.</span><span class="sxs-lookup"><span data-stu-id="355da-222">Operating it is simple: when hello app starts, enter hello alias of hello user you want toolook up, and then click hello button.</span></span> <span data-ttu-id="355da-223">Lhe for pedida a autenticação.</span><span class="sxs-lookup"><span data-stu-id="355da-223">You're prompted for authentication.</span></span> <span data-ttu-id="355da-224">Após a autenticação com êxito e êxito pesquisa, são apresentados Olá os atributos de utilizador de Olá procurado.</span><span class="sxs-lookup"><span data-stu-id="355da-224">Upon successful authentication and successful search, hello attributes of hello searched user are displayed.</span></span>

<span data-ttu-id="355da-225">Execuções subsequentes irão efetuar a pesquisa de Olá sem que mostra a qualquer linha de comandos, thanks presença toohello Olá anteriormente adquirir token na cache.</span><span class="sxs-lookup"><span data-stu-id="355da-225">Subsequent runs will perform hello search without showing any prompt, thanks toohello presence of hello previously acquired token in cache.</span></span>

<span data-ttu-id="355da-226">passos concreto de Olá para executar a aplicação Olá variam consoante a plataforma.</span><span class="sxs-lookup"><span data-stu-id="355da-226">hello concrete steps for running hello app vary by platform.</span></span>

### <a name="windows-10"></a><span data-ttu-id="355da-227">Windows 10</span><span class="sxs-lookup"><span data-stu-id="355da-227">Windows 10</span></span>
   <span data-ttu-id="355da-228">Tablet/PC:`cordova run windows --archs=x64 -- --appx=uap`</span><span class="sxs-lookup"><span data-stu-id="355da-228">Tablet/PC: `cordova run windows --archs=x64 -- --appx=uap`</span></span>

   <span data-ttu-id="355da-229">Dispositivo móvel (requer um tooa de dispositivo ligado do Windows 10 Mobile PC):`cordova run windows --archs=arm -- --appx=uap --phone`</span><span class="sxs-lookup"><span data-stu-id="355da-229">Mobile (requires a Windows 10 Mobile device connected tooa PC): `cordova run windows --archs=arm -- --appx=uap --phone`</span></span>

   > [!NOTE]
   > <span data-ttu-id="355da-230">Durante a Olá executar pela primeira vez, ser pedido toosign numa licença de programador.</span><span class="sxs-lookup"><span data-stu-id="355da-230">During hello first run, you might be asked toosign in for a developer license.</span></span> <span data-ttu-id="355da-231">Para obter mais informações, consulte [licença de programador](https://msdn.microsoft.com/library/windows/apps/hh974578.aspx).</span><span class="sxs-lookup"><span data-stu-id="355da-231">For more information, see [Developer license](https://msdn.microsoft.com/library/windows/apps/hh974578.aspx).</span></span>

### <a name="windows-81-tabletpc"></a><span data-ttu-id="355da-232">Windows 8.1 Tablet/PC</span><span class="sxs-lookup"><span data-stu-id="355da-232">Windows 8.1 Tablet/PC</span></span>
   `cordova run windows`

   > [!NOTE]
   > <span data-ttu-id="355da-233">Durante a Olá executar pela primeira vez, ser pedido toosign numa licença de programador.</span><span class="sxs-lookup"><span data-stu-id="355da-233">During hello first run, you might be asked toosign in for a developer license.</span></span> <span data-ttu-id="355da-234">Para obter mais informações, consulte [licença de programador](https://msdn.microsoft.com/library/windows/apps/hh974578.aspx).</span><span class="sxs-lookup"><span data-stu-id="355da-234">For more information, see [Developer license](https://msdn.microsoft.com/library/windows/apps/hh974578.aspx).</span></span>

### <a name="windows-phone-81"></a><span data-ttu-id="355da-235">Windows Phone 8.1</span><span class="sxs-lookup"><span data-stu-id="355da-235">Windows Phone 8.1</span></span>
   <span data-ttu-id="355da-236">toorun num dispositivo ligado:`cordova run windows --device -- --phone`</span><span class="sxs-lookup"><span data-stu-id="355da-236">toorun on a connected device: `cordova run windows --device -- --phone`</span></span>

   <span data-ttu-id="355da-237">toorun no emulador do Olá predefinido:`cordova emulate windows -- --phone`</span><span class="sxs-lookup"><span data-stu-id="355da-237">toorun on hello default emulator: `cordova emulate windows -- --phone`</span></span>

   <span data-ttu-id="355da-238">Utilize `cordova run windows --list -- --phone` toosee todos os destinos disponíveis e `cordova run windows --target=<target_name> -- --phone` aplicação de Olá toorun num dispositivo específico ou emulador (por exemplo, `cordova run windows --target="Emulator 8.1 720P 4.7 inch" -- --phone`).</span><span class="sxs-lookup"><span data-stu-id="355da-238">Use `cordova run windows --list -- --phone` toosee all available targets and `cordova run windows --target=<target_name> -- --phone` toorun hello application on a specific device or emulator (for example, `cordova run windows --target="Emulator 8.1 720P 4.7 inch" -- --phone`).</span></span>

### <a name="android"></a><span data-ttu-id="355da-239">Android</span><span class="sxs-lookup"><span data-stu-id="355da-239">Android</span></span>
   <span data-ttu-id="355da-240">toorun num dispositivo ligado:`cordova run android --device`</span><span class="sxs-lookup"><span data-stu-id="355da-240">toorun on a connected device: `cordova run android --device`</span></span>

   <span data-ttu-id="355da-241">toorun no emulador do Olá predefinido:`cordova emulate android`</span><span class="sxs-lookup"><span data-stu-id="355da-241">toorun on hello default emulator: `cordova emulate android`</span></span>

   <span data-ttu-id="355da-242">Certifique-se de que criou uma instância de emulador utilizando o Gestor de AVD, como descrito anteriormente Olá secção "Pré-requisitos".</span><span class="sxs-lookup"><span data-stu-id="355da-242">Make sure you've created an emulator instance by using AVD Manager, as described earlier in hello "Prerequisites" section.</span></span>

   <span data-ttu-id="355da-243">Utilize `cordova run android --list` toosee todos os destinos disponíveis e `cordova run android --target=<target_name>` aplicação de Olá toorun num dispositivo específico ou emulador (por exemplo, `cordova run android --target="Nexus4_emulator"`).</span><span class="sxs-lookup"><span data-stu-id="355da-243">Use `cordova run android --list` toosee all available targets and `cordova run android --target=<target_name>` toorun hello application on a specific device or emulator (for example, `cordova run android --target="Nexus4_emulator"`).</span></span>

### <a name="ios"></a><span data-ttu-id="355da-244">iOS</span><span class="sxs-lookup"><span data-stu-id="355da-244">iOS</span></span>
   <span data-ttu-id="355da-245">toorun num dispositivo ligado:`cordova run ios --device`</span><span class="sxs-lookup"><span data-stu-id="355da-245">toorun on a connected device: `cordova run ios --device`</span></span>

   <span data-ttu-id="355da-246">toorun no emulador do Olá predefinido:`cordova emulate ios`</span><span class="sxs-lookup"><span data-stu-id="355da-246">toorun on hello default emulator: `cordova emulate ios`</span></span>

   > [!NOTE]
   > <span data-ttu-id="355da-247">Certifique-se de que tem Olá `ios-sim` toorun pacote instalado no emulador Olá.</span><span class="sxs-lookup"><span data-stu-id="355da-247">Make sure you have hello `ios-sim` package installed toorun on hello emulator.</span></span> <span data-ttu-id="355da-248">Para obter mais informações, consulte Olá "pré-requisitos" secção.</span><span class="sxs-lookup"><span data-stu-id="355da-248">For more information, see hello "Prerequisites" section.</span></span>

    Use `cordova run ios --list` toosee all available targets and `cordova run ios --target=<target_name>` toorun hello application on specific device or emulator (for example, `cordova run android --target="iPhone-6"`).

    Use `cordova run --help` toosee additional build and run options.

## <a name="next-steps"></a><span data-ttu-id="355da-249">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="355da-249">Next steps</span></span>
<span data-ttu-id="355da-250">Para referência, está disponível no exemplo de Olá concluído (sem os valores de configuração) [GitHub](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-Cordova/tree/complete/DirSearchClient).</span><span class="sxs-lookup"><span data-stu-id="355da-250">For reference, hello completed sample (without your configuration values) is available in [GitHub](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-Cordova/tree/complete/DirSearchClient).</span></span>

<span data-ttu-id="355da-251">Pode agora os cenários de movimentação em toomore avançadas (e mais interessante).</span><span class="sxs-lookup"><span data-stu-id="355da-251">You can now move on toomore advanced (and more interesting) scenarios.</span></span> <span data-ttu-id="355da-252">É aconselhável tootry: [proteger uma API Web do Node.js com o Azure AD](active-directory-devquickstarts-webapi-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="355da-252">You might want tootry: [Secure a Node.js Web API with Azure AD](active-directory-devquickstarts-webapi-nodejs.md).</span></span>

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
