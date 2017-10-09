---
title: "aaaAzure AD Android introdução | Microsoft Docs"
description: "Como toobuild uma aplicação Android que se integra com o Azure AD para início de sessão e chamadas do Azure AD protegido APIs através da utilização de OAuth."
services: active-directory
documentationcenter: android
author: danieldobalian
manager: mbaldwin
editor: 
ms.assetid: da1ee39f-89d3-4d36-96f1-4eabbc662343
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: article
ms.date: 01/07/2017
ms.author: dadobali
ms.custom: aaddev
ms.openlocfilehash: 1aedc8ff60874b405a182a4ccbfb2c8b4d9d3704
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-ad-into-an-android-app"></a><span data-ttu-id="642ec-103">Integrar o Azure AD para uma aplicação Android</span><span class="sxs-lookup"><span data-stu-id="642ec-103">Integrate Azure AD into an Android app</span></span>
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

> [!TIP]
> <span data-ttu-id="642ec-104">Experimentar a pré-visualização de Olá do nosso novo [portal do programador](https://identity.microsoft.com/Docs/Android), que irá ajudar a começar a trabalhar com o Azure AD em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="642ec-104">Try hello preview of our new [developer portal](https://identity.microsoft.com/Docs/Android), which will help you get up and running with Azure AD in just a few minutes.</span></span> <span data-ttu-id="642ec-105">portal do programador Olá irá guiá-lo através do processo de Olá de registar uma aplicação e a integração do Azure AD para o seu código.</span><span class="sxs-lookup"><span data-stu-id="642ec-105">hello developer portal will walk you through hello process of registering an app and integrating Azure AD into your code.</span></span> <span data-ttu-id="642ec-106">Quando tiver terminado, terá uma aplicação simples que pode autenticar utilizadores no seu inquilino e um back-end que podem aceitar tokens e efetuar a validação.</span><span class="sxs-lookup"><span data-stu-id="642ec-106">When you’re finished, you'll have a simple application that can authenticate users in your tenant and a back end that can accept tokens and perform validation.</span></span>
>
>

<span data-ttu-id="642ec-107">Se estiver a desenvolver uma aplicação de ambiente de trabalho, do Azure Active Directory (Azure AD) permite simples e fácil para tooauthenticate os utilizadores através das respetivas contas do Active Directory no local.</span><span class="sxs-lookup"><span data-stu-id="642ec-107">If you're developing a desktop application, Azure Active Directory (Azure AD) makes it simple and straightforward for you tooauthenticate your users by using their on-premises Active Directory accounts.</span></span> <span data-ttu-id="642ec-108">Também permite que a aplicação toosecurely consumir qualquer API web protegida pelo Azure AD, tal como Olá APIs do Office 365 ou Olá API do Azure.</span><span class="sxs-lookup"><span data-stu-id="642ec-108">It also enables your application toosecurely consume any web API protected by Azure AD, such as hello Office 365 APIs or hello Azure API.</span></span>

<span data-ttu-id="642ec-109">Para Android clientes que necessitam de recursos de tooaccess protegido, o Azure AD fornece Olá Active Directory Authentication Library (ADAL).</span><span class="sxs-lookup"><span data-stu-id="642ec-109">For Android clients that need tooaccess protected resources, Azure AD provides hello Active Directory Authentication Library (ADAL).</span></span> <span data-ttu-id="642ec-110">Olá único objetivo ADAL é toomake-lo mais fácil para os tokens de acesso de tooget de aplicação.</span><span class="sxs-lookup"><span data-stu-id="642ec-110">hello sole purpose of ADAL is toomake it easy for your app tooget access tokens.</span></span> <span data-ttu-id="642ec-111">toodemonstrate como fácil é, iremos irá criar uma aplicação Android lista de tarefas que:</span><span class="sxs-lookup"><span data-stu-id="642ec-111">toodemonstrate how easy it is, we’ll build an Android To-Do List application that:</span></span>

* <span data-ttu-id="642ec-112">Obtém acesso tokens para chamar uma API da lista de tarefas utilizando Olá [protocolo de autenticação OAuth 2.0](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span><span class="sxs-lookup"><span data-stu-id="642ec-112">Gets access tokens for calling a To-Do List API by using hello [OAuth 2.0 authentication protocol](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span></span>
* <span data-ttu-id="642ec-113">Obtém a lista de tarefas de um utilizador.</span><span class="sxs-lookup"><span data-stu-id="642ec-113">Gets a user's to-do list.</span></span>
* <span data-ttu-id="642ec-114">Inicia os utilizadores.</span><span class="sxs-lookup"><span data-stu-id="642ec-114">Signs out users.</span></span>

<span data-ttu-id="642ec-115">tooget iniciada, é necessário um inquilino do Azure AD, onde pode criar utilizadores e registar uma aplicação.</span><span class="sxs-lookup"><span data-stu-id="642ec-115">tooget started, you need an Azure AD tenant in which you can create users and register an application.</span></span> <span data-ttu-id="642ec-116">Se ainda não tiver um inquilino, [Saiba como tooget um](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="642ec-116">If you don't already have a tenant, [learn how tooget one](active-directory-howto-tenant.md).</span></span>

## <a name="step-1-download-and-run-hello-nodejs-rest-api-todo-sample-server"></a><span data-ttu-id="642ec-117">Passo 1: Transferir e executar o servidor de exemplo Olá TODO de API de REST do Node.js</span><span class="sxs-lookup"><span data-stu-id="642ec-117">Step 1: Download and run hello Node.js REST API TODO sample server</span></span>
<span data-ttu-id="642ec-118">exemplo de TODO de API de REST do Node.js Olá é escrito especificamente toowork no nosso exemplo existente para criar um API de REST de itens pendentes de único inquilino do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="642ec-118">hello Node.js REST API TODO sample is written specifically toowork against our existing sample for building a single-tenant To-Do REST API for Azure AD.</span></span> <span data-ttu-id="642ec-119">Este é um pré-requisito para Olá início rápido.</span><span class="sxs-lookup"><span data-stu-id="642ec-119">This is a prerequisite for hello Quick Start.</span></span>

<span data-ttu-id="642ec-120">Para obter informações sobre como tooset esta cópia de segurança, consulte o artigo nossos exemplos existentes no [serviço Microsoft Azure Active Directory exemplo REST API para Node.js](active-directory-devquickstarts-webapi-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="642ec-120">For information on how tooset this up, see our existing samples in [Microsoft Azure Active Directory Sample REST API Service for Node.js](active-directory-devquickstarts-webapi-nodejs.md).</span></span>


## <a name="step-2-register-your-web-api-with-your-azure-ad-tenant"></a><span data-ttu-id="642ec-121">Passo 2: Registar a API web no inquilino do Azure AD</span><span class="sxs-lookup"><span data-stu-id="642ec-121">Step 2: Register your web API with your Azure AD tenant</span></span>
<span data-ttu-id="642ec-122">Active Directory suporta a adição de dois tipos de aplicações:</span><span class="sxs-lookup"><span data-stu-id="642ec-122">Active Directory supports adding two types of applications:</span></span>

- <span data-ttu-id="642ec-123">As APIs que oferecem toousers de serviços Web</span><span class="sxs-lookup"><span data-stu-id="642ec-123">Web APIs that offer services toousers</span></span>
- <span data-ttu-id="642ec-124">As aplicações (executado na web Olá ou num dispositivo) que aceder às APIs web</span><span class="sxs-lookup"><span data-stu-id="642ec-124">Applications (running either on hello web or on a device) that access those web APIs</span></span>

<span data-ttu-id="642ec-125">Neste passo, que está a registar Olá web API que estiver a executar localmente para este exemplo de teste.</span><span class="sxs-lookup"><span data-stu-id="642ec-125">In this step, you're registering hello web API that you're running locally for testing this sample.</span></span> <span data-ttu-id="642ec-126">Normalmente, esta API web é um serviço REST que é a funcionalidade de oferta de que pretende que um tooaccess de aplicação.</span><span class="sxs-lookup"><span data-stu-id="642ec-126">Normally, this web API is a REST service that's offering functionality that you want an app tooaccess.</span></span> <span data-ttu-id="642ec-127">Azure AD pode ajudar a proteger qualquer ponto final.</span><span class="sxs-lookup"><span data-stu-id="642ec-127">Azure AD can help protect any endpoint.</span></span>

<span data-ttu-id="642ec-128">Partimos do princípio que está a registar Olá API de REST de TODO referenciado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="642ec-128">We're assuming that you're registering hello TODO REST API referenced earlier.</span></span> <span data-ttu-id="642ec-129">Mas isto funciona para qualquer web API que pretende que o Azure Active Directory toohelp proteger.</span><span class="sxs-lookup"><span data-stu-id="642ec-129">But this works for any web API that you want Azure Active Directory toohelp protect.</span></span>

1. <span data-ttu-id="642ec-130">Inicie sessão no toohello [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="642ec-130">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="642ec-131">Na barra superior Olá, clique em sua conta.</span><span class="sxs-lookup"><span data-stu-id="642ec-131">On hello top bar, click your account.</span></span> <span data-ttu-id="642ec-132">No Olá **diretório** lista, escolha inquilino Olá do Azure AD, onde pretende tooregister a aplicação.</span><span class="sxs-lookup"><span data-stu-id="642ec-132">In hello **Directory** list, choose hello Azure AD tenant where you want tooregister your application.</span></span>
3. <span data-ttu-id="642ec-133">Clique em **mais serviços** no Olá painel esquerdo e, em seguida, selecione **do Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="642ec-133">Click **More Services** in hello left pane, and then select **Azure Active Directory**.</span></span>
4. <span data-ttu-id="642ec-134">Clique em **registos de aplicação**e, em seguida, selecione **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="642ec-134">Click **App registrations**, and then select **Add**.</span></span>
5. <span data-ttu-id="642ec-135">Introduza um nome amigável para aplicação Olá (por exemplo, **TodoListService**), selecione **aplicação Web e/ou Web API**e clique em **seguinte**.</span><span class="sxs-lookup"><span data-stu-id="642ec-135">Enter a friendly name for hello application (for example, **TodoListService**), select **Web Application and/or Web API**, and click **Next**.</span></span>
6. <span data-ttu-id="642ec-136">Para Olá início de sessão no URL, introduza o URL de base de Olá de exemplo de Olá.</span><span class="sxs-lookup"><span data-stu-id="642ec-136">For hello sign-on URL, enter hello base URL for hello sample.</span></span> <span data-ttu-id="642ec-137">Por predefinição, este é `https://localhost:8080`.</span><span class="sxs-lookup"><span data-stu-id="642ec-137">By default, this is `https://localhost:8080`.</span></span>
7. <span data-ttu-id="642ec-138">Clique em **OK** registo de Olá toocomplete.</span><span class="sxs-lookup"><span data-stu-id="642ec-138">Click **OK** toocomplete hello registration.</span></span>
8. <span data-ttu-id="642ec-139">Enquanto ainda Olá portal do Azure, visite a página da aplicação tooyour, localizar o valor de ID de aplicação Olá e copiá-lo.</span><span class="sxs-lookup"><span data-stu-id="642ec-139">While still in hello Azure portal, go tooyour application page, find hello application ID value, and copy it.</span></span> <span data-ttu-id="642ec-140">Irá precisar deste mais tarde quando configurar a sua aplicação.</span><span class="sxs-lookup"><span data-stu-id="642ec-140">You'll need this later when configuring your application.</span></span>
9. <span data-ttu-id="642ec-141">De Olá **definições** -> **propriedades** página, atualizar a aplicação Olá ID URI - introduza `https://<your_tenant_name>/TodoListService`.</span><span class="sxs-lookup"><span data-stu-id="642ec-141">From hello **Settings** -> **Properties** page, update hello app ID URI - enter `https://<your_tenant_name>/TodoListService`.</span></span> <span data-ttu-id="642ec-142">Substitua `<your_tenant_name>` com o nome de Olá do seu inquilino do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="642ec-142">Replace `<your_tenant_name>` with hello name of your Azure AD tenant.</span></span>

## <a name="step-3-register-hello-sample-android-native-client-application"></a><span data-ttu-id="642ec-143">Passo 3: Registar a aplicação de cliente nativo Android de exemplo de Olá</span><span class="sxs-lookup"><span data-stu-id="642ec-143">Step 3: Register hello sample Android Native Client application</span></span>
<span data-ttu-id="642ec-144">Tem de registar a aplicação web neste exemplo.</span><span class="sxs-lookup"><span data-stu-id="642ec-144">You must register your web application in this sample.</span></span> <span data-ttu-id="642ec-145">Isto permite que o seu toocommunicate de aplicação com Olá just-registado API web do.</span><span class="sxs-lookup"><span data-stu-id="642ec-145">This allows your application toocommunicate with hello just-registered web API.</span></span> <span data-ttu-id="642ec-146">Azure AD irá refuse tooeven permitir tooask a aplicação de início de sessão, a menos que está registado.</span><span class="sxs-lookup"><span data-stu-id="642ec-146">Azure AD will refuse tooeven allow your application tooask for sign-in unless it's registered.</span></span> <span data-ttu-id="642ec-147">Que faz parte de segurança de Olá do modelo de Olá.</span><span class="sxs-lookup"><span data-stu-id="642ec-147">That's part of hello security of hello model.</span></span>

<span data-ttu-id="642ec-148">Partimos do princípio que está a registar a aplicação de exemplo de Olá referenciada anteriormente.</span><span class="sxs-lookup"><span data-stu-id="642ec-148">We're assuming that you're registering hello sample application referenced earlier.</span></span> <span data-ttu-id="642ec-149">Mas este procedimento funciona para qualquer aplicação que estiver a desenvolver.</span><span class="sxs-lookup"><span data-stu-id="642ec-149">But this procedure works for any app that you're developing.</span></span>

> [!NOTE]
> <span data-ttu-id="642ec-150">Poderá wonder por que motivo está a colocar uma aplicação e uma API web no um inquilino.</span><span class="sxs-lookup"><span data-stu-id="642ec-150">You might wonder why you're putting both an application and a web API in one tenant.</span></span> <span data-ttu-id="642ec-151">Como o poderá ter adivinhado, pode criar uma aplicação que acede a uma API externa que está registada no Azure AD a partir de outro inquilino.</span><span class="sxs-lookup"><span data-stu-id="642ec-151">As you might have guessed, you can build an app that accesses an external API that is registered in Azure AD from another tenant.</span></span> <span data-ttu-id="642ec-152">Se, fazê-lo, os seus clientes será solicitado tooconsent toohello utilização Olá API na aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="642ec-152">If you do that, your customers will be prompted tooconsent toohello use of hello API in hello application.</span></span> <span data-ttu-id="642ec-153">Biblioteca de autenticação do Active Directory para iOS encarrega-se deste consentimento para si.</span><span class="sxs-lookup"><span data-stu-id="642ec-153">Active Directory Authentication Library for iOS takes care of this consent for you.</span></span> <span data-ttu-id="642ec-154">Como podemos explorar as funcionalidades mais avançadas, verá que se trata de uma parte importante da suite Olá do Olá trabalho tooaccess necessárias das APIs do Microsoft Azure e Office, bem como qualquer outro fornecedor de serviços.</span><span class="sxs-lookup"><span data-stu-id="642ec-154">As we explore more advanced features, you'll see that this is an important part of hello work needed tooaccess hello suite of Microsoft APIs from Azure and Office, as well as any other service provider.</span></span> <span data-ttu-id="642ec-155">Por agora, porque registado web API e a aplicação Olá mesmo inquilino, não verão qualquer pede consentimento.</span><span class="sxs-lookup"><span data-stu-id="642ec-155">For now, because you registered both your web API and your application under hello same tenant, you won't see any prompts for consent.</span></span> <span data-ttu-id="642ec-156">Isto é normalmente o caso de Olá se estiver a desenvolver uma aplicação apenas para sua própria toouse da empresa.</span><span class="sxs-lookup"><span data-stu-id="642ec-156">This is usually hello case if you're developing an application just for your own company toouse.</span></span>

1. <span data-ttu-id="642ec-157">Inicie sessão no toohello [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="642ec-157">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="642ec-158">Na barra superior Olá, clique em sua conta.</span><span class="sxs-lookup"><span data-stu-id="642ec-158">On hello top bar, click your account.</span></span> <span data-ttu-id="642ec-159">No Olá **diretório** lista, escolha inquilino Olá do Azure AD, onde pretende tooregister a aplicação.</span><span class="sxs-lookup"><span data-stu-id="642ec-159">In hello **Directory** list, choose hello Azure AD tenant where you want tooregister your application.</span></span>
3. <span data-ttu-id="642ec-160">Clique em **mais serviços** no Olá painel esquerdo e, em seguida, selecione **do Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="642ec-160">Click **More Services** in hello left pane, and then select **Azure Active Directory**.</span></span>
4. <span data-ttu-id="642ec-161">Clique em **registos de aplicação**e, em seguida, selecione **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="642ec-161">Click **App registrations**, and then select **Add**.</span></span>
5. <span data-ttu-id="642ec-162">Introduza um nome amigável para aplicação Olá (por exemplo, **TodoListClient Android**), selecione **aplicação cliente nativa**e clique em **seguinte**.</span><span class="sxs-lookup"><span data-stu-id="642ec-162">Enter a friendly name for hello application (for example, **TodoListClient-Android**), select **Native Client Application**, and click **Next**.</span></span>
6. <span data-ttu-id="642ec-163">Para Olá URI de redirecionamento, introduza `http://TodoListClient`.</span><span class="sxs-lookup"><span data-stu-id="642ec-163">For hello redirect URI, enter `http://TodoListClient`.</span></span> <span data-ttu-id="642ec-164">Clique em **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="642ec-164">Click **Finish**.</span></span>
7. <span data-ttu-id="642ec-165">A partir da página da aplicação Olá, localize o valor de ID de aplicação Olá e copiá-lo.</span><span class="sxs-lookup"><span data-stu-id="642ec-165">From hello application page, find hello application ID value and copy it.</span></span> <span data-ttu-id="642ec-166">Irá precisar deste mais tarde quando configurar a sua aplicação.</span><span class="sxs-lookup"><span data-stu-id="642ec-166">You'll need this later when configuring your application.</span></span>
8. <span data-ttu-id="642ec-167">De Olá **definições** página, selecione **permissões obrigatórias** e selecione **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="642ec-167">From hello **Settings** page, select **Required Permissions** and select **Add**.</span></span>  <span data-ttu-id="642ec-168">Localize e selecione TodoListService, adicione Olá **acesso TodoListService** permissão em **permissões delegadas**e clique em **feito**.</span><span class="sxs-lookup"><span data-stu-id="642ec-168">Locate and select TodoListService, add hello **Access TodoListService** permission under **Delegated Permissions**, and click **Done**.</span></span>

<span data-ttu-id="642ec-169">toobuild com o Maven, pode utilizar pom.xml no nível superior Olá:</span><span class="sxs-lookup"><span data-stu-id="642ec-169">toobuild with Maven, you can use pom.xml at hello top level:</span></span>

1. <span data-ttu-id="642ec-170">Este repositório do clone para um diretório da sua preferência:</span><span class="sxs-lookup"><span data-stu-id="642ec-170">Clone this repo into a directory of your choice:</span></span>

  `$ git clone git@github.com:AzureADSamples/NativeClient-Android.git`  
2. <span data-ttu-id="642ec-171">Siga os passos de Olá Olá [pré-requisitos tooset configurar o ambiente de Maven para Android](https://github.com/MSOpenTech/azure-activedirectory-library-for-android/wiki/Setting-up-maven-environment-for-Android).</span><span class="sxs-lookup"><span data-stu-id="642ec-171">Follow hello steps in hello [prerequisites tooset up your Maven environment for Android](https://github.com/MSOpenTech/azure-activedirectory-library-for-android/wiki/Setting-up-maven-environment-for-Android).</span></span>
3. <span data-ttu-id="642ec-172">Configure o emulador de Olá com 19 de SDK.</span><span class="sxs-lookup"><span data-stu-id="642ec-172">Set up hello emulator with SDK 19.</span></span>
4. <span data-ttu-id="642ec-173">Aceda toohello a pasta raiz onde clonou o repositório de Olá.</span><span class="sxs-lookup"><span data-stu-id="642ec-173">Go toohello root folder where you cloned hello repo.</span></span>
5. <span data-ttu-id="642ec-174">Execute este comando:`mvn clean install`</span><span class="sxs-lookup"><span data-stu-id="642ec-174">Run this command: `mvn clean install`</span></span>
6. <span data-ttu-id="642ec-175">Alterar o exemplo Olá diretório toohello início rápido:`cd samples\hello`</span><span class="sxs-lookup"><span data-stu-id="642ec-175">Change hello directory toohello Quick Start sample: `cd samples\hello`</span></span>
7. <span data-ttu-id="642ec-176">Execute este comando:`mvn android:deploy android:run`</span><span class="sxs-lookup"><span data-stu-id="642ec-176">Run this command: `mvn android:deploy android:run`</span></span>

   <span data-ttu-id="642ec-177">Deverá ver a iniciar a aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="642ec-177">You should see hello app starting.</span></span>
8. <span data-ttu-id="642ec-178">Introduza tootry de credenciais de utilizador de teste.</span><span class="sxs-lookup"><span data-stu-id="642ec-178">Enter test user credentials tootry.</span></span>

<span data-ttu-id="642ec-179">Pacotes JAR irão ser submetidos para além do pacote de AAR Olá.</span><span class="sxs-lookup"><span data-stu-id="642ec-179">JAR packages will be submitted beside hello AAR package.</span></span>

## <a name="step-4-download-hello-android-adal-and-add-it-tooyour-eclipse-workspace"></a><span data-ttu-id="642ec-180">Passo 4: Transferir Olá Android ADAL e adicione-a área de trabalho do tooyour Eclipse</span><span class="sxs-lookup"><span data-stu-id="642ec-180">Step 4: Download hello Android ADAL and add it tooyour Eclipse workspace</span></span>
<span data-ttu-id="642ec-181">Fizemos-lo mais fácil para toohave tem várias opções toouse ADAL no seu projeto Android:</span><span class="sxs-lookup"><span data-stu-id="642ec-181">We've made it easy for you toohave multiple options toouse ADAL in your Android project:</span></span>

* <span data-ttu-id="642ec-182">Pode utilizar tooimport de código de origem Olá nesta biblioteca na aplicação de tooyour Eclipse e a ligação.</span><span class="sxs-lookup"><span data-stu-id="642ec-182">You can use hello source code tooimport this library into Eclipse and link tooyour application.</span></span>
* <span data-ttu-id="642ec-183">Se estiver a utilizar o Android Studio, pode utilizar Olá AAR pacote formato e referência Olá binários.</span><span class="sxs-lookup"><span data-stu-id="642ec-183">If you're using Android Studio, you can use hello AAR package format and reference hello binaries.</span></span>

### <a name="option-1-source-zip"></a><span data-ttu-id="642ec-184">Opção 1: Origem Zip</span><span class="sxs-lookup"><span data-stu-id="642ec-184">Option 1: Source Zip</span></span>
<span data-ttu-id="642ec-185">Clique em toodownload uma cópia do código de origem Olá, **transferir ZIP** no lado direito de Olá da página Olá.</span><span class="sxs-lookup"><span data-stu-id="642ec-185">toodownload a copy of hello source code, click **Download ZIP** on hello right side of hello page.</span></span> <span data-ttu-id="642ec-186">Ou pode [transferir a partir do GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-android/archive/v1.0.9.tar.gz).</span><span class="sxs-lookup"><span data-stu-id="642ec-186">Or you can [download from GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-android/archive/v1.0.9.tar.gz).</span></span>

### <a name="option-2-source-via-git"></a><span data-ttu-id="642ec-187">Opção 2: Origem via Git</span><span class="sxs-lookup"><span data-stu-id="642ec-187">Option 2: Source via Git</span></span>
<span data-ttu-id="642ec-188">código de origem Olá tooget de Olá SDK através de Git, escreva:</span><span class="sxs-lookup"><span data-stu-id="642ec-188">tooget hello source code of hello SDK via Git, type:</span></span>

    git clone git@github.com:AzureAD/azure-activedirectory-library-for-android.git
    cd ./azure-activedirectory-library-for-android/src

### <a name="option-3-binaries-via-gradle"></a><span data-ttu-id="642ec-189">Opção 3: Binários através do Gradle</span><span class="sxs-lookup"><span data-stu-id="642ec-189">Option 3: Binaries via Gradle</span></span>
<span data-ttu-id="642ec-190">Pode obter os binários de Olá do repositório central do Olá Maven.</span><span class="sxs-lookup"><span data-stu-id="642ec-190">You can get hello binaries from hello Maven central repo.</span></span> <span data-ttu-id="642ec-191">pacote de AAR Olá pode ser incluído forma no seu projeto no Android Studio:</span><span class="sxs-lookup"><span data-stu-id="642ec-191">hello AAR package can be included as follows in your project in Android Studio:</span></span>

```gradle
repositories {
    mavenCentral()
    flatDir {
        dirs 'libs'
    }
    maven {
        url "YourLocalMavenRepoPath\\.m2\\repository"
    }
}
dependencies {
    compile fileTree(dir: 'libs', include: ['*.jar'])
    compile('com.microsoft.aad:adal:1.1.1') {
        exclude group: 'com.android.support'
    } // Recent version is 1.1.1
}
```

### <a name="option-4-aar-via-maven"></a><span data-ttu-id="642ec-192">Opção 4: AAR através do Maven</span><span class="sxs-lookup"><span data-stu-id="642ec-192">Option 4: AAR via Maven</span></span>
<span data-ttu-id="642ec-193">Se estiver a utilizar Olá M2Eclipse Plug-in, pode especificar a dependência de Olá no seu ficheiro pom.xml:</span><span class="sxs-lookup"><span data-stu-id="642ec-193">If you're using hello M2Eclipse plug-in, you can specify hello dependency in your pom.xml file:</span></span>

```xml
<dependency>
    <groupId>com.microsoft.aad</groupId>
    <artifactId>adal</artifactId>
    <version>1.1.1</version>
    <type>aar</type>
</dependency>
```


### <a name="option-5-jar-package-inside-hello-libs-folder"></a><span data-ttu-id="642ec-194">Opção 5: Pacote JAR Olá libs pasta</span><span class="sxs-lookup"><span data-stu-id="642ec-194">Option 5: JAR package inside hello libs folder</span></span>
<span data-ttu-id="642ec-195">Pode obter o ficheiro JAR de Olá do repositório de Maven Olá e solte-o no Olá **libs** pasta no seu projeto.</span><span class="sxs-lookup"><span data-stu-id="642ec-195">You can get hello JAR file from hello Maven repo and drop it into hello **libs** folder in your project.</span></span> <span data-ttu-id="642ec-196">Terá de projeto, de tooyour do toocopy Olá recursos necessários porque não incluem pacotes JAR Olá-los.</span><span class="sxs-lookup"><span data-stu-id="642ec-196">You need toocopy hello required resources tooyour project as well, because hello JAR packages don't include them.</span></span>

## <a name="step-5-add-references-tooandroid-adal-tooyour-project"></a><span data-ttu-id="642ec-197">Passo 5: Adicionar o projeto do referências tooAndroid ADAL tooyour</span><span class="sxs-lookup"><span data-stu-id="642ec-197">Step 5: Add references tooAndroid ADAL tooyour project</span></span>
1. <span data-ttu-id="642ec-198">Adicione um projeto de tooyour de referência e especificá-la como uma biblioteca do Android.</span><span class="sxs-lookup"><span data-stu-id="642ec-198">Add a reference tooyour project and specify it as an Android library.</span></span> <span data-ttu-id="642ec-199">Se estiver incerto como toodo, pode obter mais informações sobre Olá [site do Android Studio](http://developer.android.com/tools/projects/projects-eclipse.html).</span><span class="sxs-lookup"><span data-stu-id="642ec-199">If you're uncertain how toodo this, you can get more information on hello [Android Studio site](http://developer.android.com/tools/projects/projects-eclipse.html).</span></span>
2. <span data-ttu-id="642ec-200">Adicione dependência do projeto de Olá de depuração para as definições do projeto.</span><span class="sxs-lookup"><span data-stu-id="642ec-200">Add hello project dependency for debugging into your project settings.</span></span>
3. <span data-ttu-id="642ec-201">Atualize tooinclude de ficheiro do seu projeto AndroidManifest.xml:</span><span class="sxs-lookup"><span data-stu-id="642ec-201">Update your project's AndroidManifest.xml file tooinclude:</span></span>

        <uses-permission android:name="android.permission.INTERNET" />
        <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
        <application
            android:allowBackup="true"
            android:debuggable="true"
            android:icon="@drawable/ic_launcher"
            android:label="@string/app_name"
            android:theme="@style/AppTheme" >

            <activity
                android:name="com.microsoft.aad.adal.AuthenticationActivity"
                android:label="@string/title_login_hello_app" >
            </activity>
            ....
        <application/>

4. <span data-ttu-id="642ec-202">Crie uma instância de AuthenticationContext a atividade principal.</span><span class="sxs-lookup"><span data-stu-id="642ec-202">Create an instance of AuthenticationContext at your main activity.</span></span> <span data-ttu-id="642ec-203">detalhes de Olá desta chamada estejam fora do âmbito Olá deste tópico, mas pode obter um bom ponto de partida ao observar Olá [exemplo Android Native Client](https://github.com/AzureADSamples/NativeClient-Android).</span><span class="sxs-lookup"><span data-stu-id="642ec-203">hello details of this call are beyond hello scope of this topic, but you can get a good start by looking at hello [Android Native Client sample](https://github.com/AzureADSamples/NativeClient-Android).</span></span> <span data-ttu-id="642ec-204">No seguinte exemplo de Olá, SharedPreferences é cache predefinido de Olá e autoridade está no formato Olá `https://login.microsoftonline.com/yourtenant.onmicrosoft.com`:</span><span class="sxs-lookup"><span data-stu-id="642ec-204">In hello following example, SharedPreferences is hello default cache, and Authority is in hello form of `https://login.microsoftonline.com/yourtenant.onmicrosoft.com`:</span></span>

    `mContext = new AuthenticationContext(MainActivity.this, authority, true); // mContext is a field in your activity`

5. <span data-ttu-id="642ec-205">Copie este código bloco toohandle Olá final AuthenticationActivity depois de recebe um código de autorização e introduz credenciais de utilizador de Olá:</span><span class="sxs-lookup"><span data-stu-id="642ec-205">Copy this code block toohandle hello end of AuthenticationActivity after hello user enters credentials and receives an authorization code:</span></span>

        @Override
         protected void onActivityResult(int requestCode, int resultCode, Intent data) {
             super.onActivityResult(requestCode, resultCode, data);
             if (mContext != null) {
                mContext.onActivityResult(requestCode, resultCode, data);
             }
         }

6. <span data-ttu-id="642ec-206">tooask para obter um token, definir uma chamada de retorno:</span><span class="sxs-lookup"><span data-stu-id="642ec-206">tooask for a token, define a callback:</span></span>

        private AuthenticationCallback<AuthenticationResult> callback = new AuthenticationCallback<AuthenticationResult>() {

            @Override
            public void onError(Exception exc) {
                if (exc instanceof AuthenticationException) {
                    textViewStatus.setText("Cancelled");
                    Log.d(TAG, "Cancelled");
                } else {
                    textViewStatus.setText("Authentication error:" + exc.getMessage());
                    Log.d(TAG, "Authentication error:" + exc.getMessage());
                }
            }

            @Override
            public void onSuccess(AuthenticationResult result) {
                mResult = result;

                if (result == null || result.getAccessToken() == null
                        || result.getAccessToken().isEmpty()) {
                    textViewStatus.setText("Token is empty");
                    Log.d(TAG, "Token is empty");
                } else {
                    // request is successful
                    Log.d(TAG, "Status:" + result.getStatus() + " Expired:"
                            + result.getExpiresOn().toString());
                    textViewStatus.setText(PASSED);
                }
            }
        };

7. <span data-ttu-id="642ec-207">Por fim, voltar a pedir um token utilizando esse chamada de retorno:</span><span class="sxs-lookup"><span data-stu-id="642ec-207">Finally, ask for a token by using that callback:</span></span>

    `mContext.acquireToken(MainActivity.this, resource, clientId, redirect, user_loginhint, PromptBehavior.Auto, "",
                   callback);`

<span data-ttu-id="642ec-208">Eis uma explicação dos parâmetros de Olá:</span><span class="sxs-lookup"><span data-stu-id="642ec-208">Here's an explanation of hello parameters:</span></span>

* <span data-ttu-id="642ec-209">*recurso* é necessário e é recurso Olá que está a tentar tooaccess.</span><span class="sxs-lookup"><span data-stu-id="642ec-209">*resource* is required and is hello resource you're trying tooaccess.</span></span>
* <span data-ttu-id="642ec-210">*ClientID* é necessário e provém do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="642ec-210">*clientid* is required and comes from Azure AD.</span></span>
* <span data-ttu-id="642ec-211">*RedirectUri* não é necessário toobe fornecido para a chamada de acquireToken Olá.</span><span class="sxs-lookup"><span data-stu-id="642ec-211">*RedirectUri* is not required toobe provided for hello acquireToken call.</span></span> <span data-ttu-id="642ec-212">Pode configurar, como o nome do pacote.</span><span class="sxs-lookup"><span data-stu-id="642ec-212">You can set it up as your package name.</span></span>
* <span data-ttu-id="642ec-213">*PromptBehavior* ajuda tooask para cache de Olá tooskip de credenciais e o cookie.</span><span class="sxs-lookup"><span data-stu-id="642ec-213">*PromptBehavior* helps tooask for credentials tooskip hello cache and cookie.</span></span>
* <span data-ttu-id="642ec-214">*chamada de retorno* for chamado depois do código de autorização de Olá é trocado para obter um token.</span><span class="sxs-lookup"><span data-stu-id="642ec-214">*callback* is called after hello authorization code is exchanged for a token.</span></span> <span data-ttu-id="642ec-215">Tem um objeto do AuthenticationResult, que tem um token de acesso, data expirou e ID as informações do token.</span><span class="sxs-lookup"><span data-stu-id="642ec-215">It has an object of AuthenticationResult, which has access token, date expired, and ID token information.</span></span>
* <span data-ttu-id="642ec-216">*acquireTokenSilent* é opcional.</span><span class="sxs-lookup"><span data-stu-id="642ec-216">*acquireTokenSilent* is optional.</span></span> <span data-ttu-id="642ec-217">Pode chamá-lo toohandle colocação em cache e atualização do token.</span><span class="sxs-lookup"><span data-stu-id="642ec-217">You can call it toohandle caching and token refresh.</span></span> <span data-ttu-id="642ec-218">Também fornece versão da sincronização Olá.</span><span class="sxs-lookup"><span data-stu-id="642ec-218">It also provides hello sync version.</span></span> <span data-ttu-id="642ec-219">Aceita *userId* como parâmetro.</span><span class="sxs-lookup"><span data-stu-id="642ec-219">It accepts *userId* as a parameter.</span></span>

        mContext.acquireTokenSilent(resource, clientid, userId, callback );

<span data-ttu-id="642ec-220">Ao utilizar estas instruções, deve ter o que precisa de toosuccessfully integrar com o Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="642ec-220">By using this walkthrough, you should have what you need toosuccessfully integrate with Azure Active Directory.</span></span> <span data-ttu-id="642ec-221">Para obter mais exemplos de como este trabalhar, visite Olá AzureADSamples / repositório no GitHub.</span><span class="sxs-lookup"><span data-stu-id="642ec-221">For more examples of this working, visit hello AzureADSamples/ repository on GitHub.</span></span>

## <a name="important-information"></a><span data-ttu-id="642ec-222">Informações importantes</span><span class="sxs-lookup"><span data-stu-id="642ec-222">Important information</span></span>
### <a name="customization"></a><span data-ttu-id="642ec-223">Personalização</span><span class="sxs-lookup"><span data-stu-id="642ec-223">Customization</span></span>
<span data-ttu-id="642ec-224">Os recursos de aplicação podem substituir os recursos do projeto de biblioteca.</span><span class="sxs-lookup"><span data-stu-id="642ec-224">Your application resources can overwrite library project resources.</span></span> <span data-ttu-id="642ec-225">Isto acontece quando a aplicação está a ser criada.</span><span class="sxs-lookup"><span data-stu-id="642ec-225">This happens when your app is being built.</span></span> <span data-ttu-id="642ec-226">Por este motivo, pode personalizar autenticação atividade esquema Olá gosta.</span><span class="sxs-lookup"><span data-stu-id="642ec-226">For this reason, you can customize authentication activity layout hello way you want.</span></span> <span data-ttu-id="642ec-227">Ser se tookeep Olá ID controlos Olá esse ADAL utiliza (WebView).</span><span class="sxs-lookup"><span data-stu-id="642ec-227">Be sure tookeep hello ID of hello controls that ADAL uses (WebView).</span></span>

### <a name="broker"></a><span data-ttu-id="642ec-228">Mediador</span><span class="sxs-lookup"><span data-stu-id="642ec-228">Broker</span></span>
<span data-ttu-id="642ec-229">aplicação de Portal da empresa do Microsoft Intune Olá fornece o componente de Mediador de Olá.</span><span class="sxs-lookup"><span data-stu-id="642ec-229">hello Microsoft Intune Company Portal app provides hello broker component.</span></span> <span data-ttu-id="642ec-230">é criada a conta de Olá na AccountManager.</span><span class="sxs-lookup"><span data-stu-id="642ec-230">hello account is created in AccountManager.</span></span> <span data-ttu-id="642ec-231">tipo de conta de Olá é "workaccount."</span><span class="sxs-lookup"><span data-stu-id="642ec-231">hello account type is "com.microsoft.workaccount."</span></span> <span data-ttu-id="642ec-232">AccountManager permite apenas uma única conta SSO.</span><span class="sxs-lookup"><span data-stu-id="642ec-232">AccountManager allows only a single SSO account.</span></span> <span data-ttu-id="642ec-233">Cria um cookie SSO para utilizador Olá depois de concluir o desafio de dispositivo Olá para uma das aplicações de Olá.</span><span class="sxs-lookup"><span data-stu-id="642ec-233">It creates an SSO cookie for hello user after completing hello device challenge for one of hello apps.</span></span>

<span data-ttu-id="642ec-234">ADAL utiliza a conta de Mediador de Olá se uma conta de utilizador é criada neste autenticador e optar por não tooskip-lo.</span><span class="sxs-lookup"><span data-stu-id="642ec-234">ADAL uses hello broker account if one user account is created at this authenticator and you choose not tooskip it.</span></span> <span data-ttu-id="642ec-235">Pode ignorar o utilizador de Mediador de Olá com:</span><span class="sxs-lookup"><span data-stu-id="642ec-235">You can skip hello broker user with:</span></span>

   `AuthenticationSettings.Instance.setSkipBroker(true);`

<span data-ttu-id="642ec-236">É necessário tooregister um RedirectUri especial para utilização do Mediador.</span><span class="sxs-lookup"><span data-stu-id="642ec-236">You need tooregister a special RedirectUri for broker usage.</span></span> <span data-ttu-id="642ec-237">RedirectUri está num formato de Olá de `msauth://packagename/Base64UrlencodedSignature`.</span><span class="sxs-lookup"><span data-stu-id="642ec-237">RedirectUri is in hello format of `msauth://packagename/Base64UrlencodedSignature`.</span></span> <span data-ttu-id="642ec-238">Pode obter o RedirectUri para a sua aplicação através da utilização de Olá script brokerRedirectPrint.ps1 ou Olá API chamada mContext.getBrokerRedirectUri.</span><span class="sxs-lookup"><span data-stu-id="642ec-238">You can get your RedirectUri for your app by using hello script brokerRedirectPrint.ps1 or hello API call mContext.getBrokerRedirectUri.</span></span> <span data-ttu-id="642ec-239">a assinatura de Olá é tooyour relacionadas com certificados de assinatura.</span><span class="sxs-lookup"><span data-stu-id="642ec-239">hello signature is related tooyour signing certificates.</span></span>

<span data-ttu-id="642ec-240">modelo de Mediador atual Olá destina-se um utilizador.</span><span class="sxs-lookup"><span data-stu-id="642ec-240">hello current broker model is for one user.</span></span> <span data-ttu-id="642ec-241">AuthenticationContext fornece utilizador de Mediador de Olá método tooget Olá API.</span><span class="sxs-lookup"><span data-stu-id="642ec-241">AuthenticationContext provides hello API method tooget hello broker user.</span></span>

   `String brokerAccount =  mContext.getBrokerUser(); //Broker user is returned if account is valid.`

<span data-ttu-id="642ec-242">O manifesto da aplicação deve ter Olá seguintes contas de AccountManager toouse de permissões.</span><span class="sxs-lookup"><span data-stu-id="642ec-242">Your app manifest should have hello following permissions toouse AccountManager accounts.</span></span> <span data-ttu-id="642ec-243">Para obter mais informações, consulte Olá [AccountManager informações no site do Android Olá](http://developer.android.com/reference/android/accounts/AccountManager.html).</span><span class="sxs-lookup"><span data-stu-id="642ec-243">For details, see hello [AccountManager information on hello Android site](http://developer.android.com/reference/android/accounts/AccountManager.html).</span></span>

* <span data-ttu-id="642ec-244">GET_ACCOUNTS</span><span class="sxs-lookup"><span data-stu-id="642ec-244">GET_ACCOUNTS</span></span>
* <span data-ttu-id="642ec-245">USE_CREDENTIALS</span><span class="sxs-lookup"><span data-stu-id="642ec-245">USE_CREDENTIALS</span></span>
* <span data-ttu-id="642ec-246">MANAGE_ACCOUNTS</span><span class="sxs-lookup"><span data-stu-id="642ec-246">MANAGE_ACCOUNTS</span></span>

### <a name="authority-url-and-ad-fs"></a><span data-ttu-id="642ec-247">URL de autoridade e o AD FS</span><span class="sxs-lookup"><span data-stu-id="642ec-247">Authority URL and AD FS</span></span>
<span data-ttu-id="642ec-248">Serviços de Federação do Active Directory (AD FS) não é reconhecido como produção STS, para que precisa de tooturn da deteção de instância e transmita o valor false no construtor de AuthenticationContext Olá.</span><span class="sxs-lookup"><span data-stu-id="642ec-248">Active Directory Federation Services (AD FS) is not recognized as production STS, so you need tooturn of instance discovery and pass false at hello AuthenticationContext constructor.</span></span>

<span data-ttu-id="642ec-249">URL de autoridade de Olá necessita de uma instância de STS e um [nome do inquilino](https://login.microsoftonline.com/yourtenant.onmicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="642ec-249">hello authority URL needs an STS instance and a [tenant name](https://login.microsoftonline.com/yourtenant.onmicrosoft.com).</span></span>

### <a name="querying-cache-items"></a><span data-ttu-id="642ec-250">Consultar os itens da cache</span><span class="sxs-lookup"><span data-stu-id="642ec-250">Querying cache items</span></span>
<span data-ttu-id="642ec-251">ADAL fornece uma cache de predefinição na SharedPreferences com a cache de algumas simple funções de consulta.</span><span class="sxs-lookup"><span data-stu-id="642ec-251">ADAL provides a default cache in SharedPreferences with some simple cache query functions.</span></span> <span data-ttu-id="642ec-252">Pode aproveitar cache atual Olá AuthenticationContext utilizando:</span><span class="sxs-lookup"><span data-stu-id="642ec-252">You can get hello current cache from AuthenticationContext by using:</span></span>

    ITokenCacheStore cache = mContext.getCache();

<span data-ttu-id="642ec-253">Também pode fornecer a implementação de cache, se quiser toocustomize-lo.</span><span class="sxs-lookup"><span data-stu-id="642ec-253">You can also provide your cache implementation, if you want toocustomize it.</span></span>

    mContext = new AuthenticationContext(MainActivity.this, authority, true, yourCache);

### <a name="prompt-behavior"></a><span data-ttu-id="642ec-254">Comportamento de aviso</span><span class="sxs-lookup"><span data-stu-id="642ec-254">Prompt behavior</span></span>
<span data-ttu-id="642ec-255">ADAL fornece um comportamento de aviso de toospecify opção.</span><span class="sxs-lookup"><span data-stu-id="642ec-255">ADAL provides an option toospecify prompt behavior.</span></span> <span data-ttu-id="642ec-256">PromptBehavior.Auto mostrará Olá IU se o token de atualização de Olá é inválido e são necessárias credenciais de utilizador.</span><span class="sxs-lookup"><span data-stu-id="642ec-256">PromptBehavior.Auto will show hello UI if hello refresh token is invalid and user credentials are required.</span></span> <span data-ttu-id="642ec-257">PromptBehavior.Always irá ignorar a utilização da cache de Olá e Mostrar sempre Olá IU.</span><span class="sxs-lookup"><span data-stu-id="642ec-257">PromptBehavior.Always will skip hello cache usage and always show hello UI.</span></span>

### <a name="silent-token-request-from-cache-and-refresh"></a><span data-ttu-id="642ec-258">Pedido de token automática da cache e atualizar</span><span class="sxs-lookup"><span data-stu-id="642ec-258">Silent token request from cache and refresh</span></span>
<span data-ttu-id="642ec-259">Um pedido de token automática não utiliza Olá IU pop-up e não necessita de uma atividade.</span><span class="sxs-lookup"><span data-stu-id="642ec-259">A silent token request does not use hello UI pop-up and does not require an activity.</span></span> <span data-ttu-id="642ec-260">Devolve um token da cache de Olá, se disponível.</span><span class="sxs-lookup"><span data-stu-id="642ec-260">It returns a token from hello cache if available.</span></span> <span data-ttu-id="642ec-261">Se o token de Olá expirou, este método tenta toorefresh-lo.</span><span class="sxs-lookup"><span data-stu-id="642ec-261">If hello token is expired, this method tries toorefresh it.</span></span> <span data-ttu-id="642ec-262">Se o token de atualização de Olá expirou ou falha, devolve AuthenticationException.</span><span class="sxs-lookup"><span data-stu-id="642ec-262">If hello refresh token is expired or failed, it returns AuthenticationException.</span></span>

    Future<AuthenticationResult> result = mContext.acquireTokenSilent(resource, clientid, userId, callback );

<span data-ttu-id="642ec-263">Também pode efetuar uma sincronização chamar através deste método.</span><span class="sxs-lookup"><span data-stu-id="642ec-263">You can also make a sync call by using this method.</span></span> <span data-ttu-id="642ec-264">Pode definir toocallback nulo ou utilizar acquireTokenSilentSync.</span><span class="sxs-lookup"><span data-stu-id="642ec-264">You can set null toocallback or use acquireTokenSilentSync.</span></span>

### <a name="diagnostics"></a><span data-ttu-id="642ec-265">Diagnóstico</span><span class="sxs-lookup"><span data-stu-id="642ec-265">Diagnostics</span></span>
<span data-ttu-id="642ec-266">Estes são origens principais de Olá de informações para diagnosticar problemas:</span><span class="sxs-lookup"><span data-stu-id="642ec-266">These are hello primary sources of information for diagnosing issues:</span></span>

* <span data-ttu-id="642ec-267">Exceções</span><span class="sxs-lookup"><span data-stu-id="642ec-267">Exceptions</span></span>
* <span data-ttu-id="642ec-268">Registos</span><span class="sxs-lookup"><span data-stu-id="642ec-268">Logs</span></span>
* <span data-ttu-id="642ec-269">Rastreios de rede</span><span class="sxs-lookup"><span data-stu-id="642ec-269">Network traces</span></span>

<span data-ttu-id="642ec-270">Tenha em atenção que os IDs de correlação são diagnóstico central toohello na biblioteca de Olá.</span><span class="sxs-lookup"><span data-stu-id="642ec-270">Note that correlation IDs are central toohello diagnostics in hello library.</span></span> <span data-ttu-id="642ec-271">Pode definir os IDs de correlação numa base por pedido, se quiser toocorrelate um ADAL pedido com outras operações no seu código.</span><span class="sxs-lookup"><span data-stu-id="642ec-271">You can set your correlation IDs on a per-request basis if you want toocorrelate an ADAL request with other operations in your code.</span></span> <span data-ttu-id="642ec-272">Se não definir um ID de correlação, ADAL irá gerar um aleatório.</span><span class="sxs-lookup"><span data-stu-id="642ec-272">If you don't set a correlation ID, ADAL will generate a random one.</span></span> <span data-ttu-id="642ec-273">Registar todas as mensagens e chamadas de rede serão, em seguida, ser carimbo de data / com o ID de correlação Olá.</span><span class="sxs-lookup"><span data-stu-id="642ec-273">All log messages and network calls will then be stamped with hello correlation ID.</span></span> <span data-ttu-id="642ec-274">Olá geradas automaticamente ID as alterações em cada pedido.</span><span class="sxs-lookup"><span data-stu-id="642ec-274">hello self-generated ID changes on each request.</span></span>

#### <a name="exceptions"></a><span data-ttu-id="642ec-275">Exceções</span><span class="sxs-lookup"><span data-stu-id="642ec-275">Exceptions</span></span>
<span data-ttu-id="642ec-276">Exceções são Olá primeiro diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="642ec-276">Exceptions are hello first diagnostic.</span></span> <span data-ttu-id="642ec-277">Vamos tentar tooprovide mensagens de erro úteis.</span><span class="sxs-lookup"><span data-stu-id="642ec-277">We try tooprovide helpful error messages.</span></span> <span data-ttu-id="642ec-278">Se encontrar um que não seja útil, ficheiro, um problema e informe-nos.</span><span class="sxs-lookup"><span data-stu-id="642ec-278">If you find one that is not helpful, please file an issue and let us know.</span></span> <span data-ttu-id="642ec-279">Inclua informações de dispositivo como modelo e número SDK.</span><span class="sxs-lookup"><span data-stu-id="642ec-279">Include device information such as model and SDK number.</span></span>

#### <a name="logs"></a><span data-ttu-id="642ec-280">Registos</span><span class="sxs-lookup"><span data-stu-id="642ec-280">Logs</span></span>
<span data-ttu-id="642ec-281">Pode configurar Olá biblioteca toogenerate mensagens de registo que pode utilizar toohelp diagnosticar problemas.</span><span class="sxs-lookup"><span data-stu-id="642ec-281">You can configure hello library toogenerate log messages that you can use toohelp diagnose issues.</span></span> <span data-ttu-id="642ec-282">Configurar o registo efetuando o seguinte Olá chamar tooconfigure uma chamada de retorno que ADAL utilizará toohand desativar cada mensagem do registo como é gerada.</span><span class="sxs-lookup"><span data-stu-id="642ec-282">You configure logging by making hello following call tooconfigure a callback that ADAL will use toohand off each log message as it's generated.</span></span>

    Logger.getInstance().setExternalLogger(new ILogger() {
        @Override
        public void Log(String tag, String message, String additionalMessage, LogLevel level, ADALError errorCode) {
        ...
        // You can write this toolog file depending on level or error code.
        writeToLogFile(getApplicationContext(), tag +":" + message + "-" + additionalMessage);
        }
    }

<span data-ttu-id="642ec-283">As mensagens podem ser escritas tooa o ficheiro de registo personalizado, conforme mostrado no Olá seguinte código.</span><span class="sxs-lookup"><span data-stu-id="642ec-283">Messages can be written tooa custom log file, as shown in hello following code.</span></span> <span data-ttu-id="642ec-284">Infelizmente, não é possível padrão recuperá registos a partir de um dispositivo.</span><span class="sxs-lookup"><span data-stu-id="642ec-284">Unfortunately, there is no standard way of getting logs from a device.</span></span> <span data-ttu-id="642ec-285">Existem alguns serviços que podem ajudá-lo com esta.</span><span class="sxs-lookup"><span data-stu-id="642ec-285">There are some services that can help you with this.</span></span> <span data-ttu-id="642ec-286">Também pode invent o suas próprias, tal como servidor de envio tooa de ficheiros de Olá.</span><span class="sxs-lookup"><span data-stu-id="642ec-286">You can also invent your own, such as sending hello file tooa server.</span></span>

    private syncronized void writeToLogFile(Context ctx, String msg) {
       File directory = ctx.getDir(ctx.getPackageName(), Context.MODE_PRIVATE);
       File logFile = new File(directory, "logfile");
       FileOutputStream outputStream = new FileOutputStream(logFile, true);
       OutputStreamWriter osw = new OutputStreamWriter(outputStream);
       osw.write(msg);
       osw.flush();
       osw.close();
    }

<span data-ttu-id="642ec-287">Estes são os níveis de registo de Olá:</span><span class="sxs-lookup"><span data-stu-id="642ec-287">These are hello logging levels:</span></span>
* <span data-ttu-id="642ec-288">Erro (exceções)</span><span class="sxs-lookup"><span data-stu-id="642ec-288">Error (exceptions)</span></span>
* <span data-ttu-id="642ec-289">Avisar (aviso)</span><span class="sxs-lookup"><span data-stu-id="642ec-289">Warn (warning)</span></span>
* <span data-ttu-id="642ec-290">Informações (fins informações)</span><span class="sxs-lookup"><span data-stu-id="642ec-290">Info (information purposes)</span></span>
* <span data-ttu-id="642ec-291">Verboso (obter mais detalhes)</span><span class="sxs-lookup"><span data-stu-id="642ec-291">Verbose (more details)</span></span>

<span data-ttu-id="642ec-292">Definir o nível de registo de Olá como esta:</span><span class="sxs-lookup"><span data-stu-id="642ec-292">You set hello log level like this:</span></span>

    Logger.getInstance().setLogLevel(Logger.LogLevel.Verbose);

 <span data-ttu-id="642ec-293">Todas as mensagens de registo são enviadas toologcat, em chamadas de retorno de registo personalizado de tooany de adição.</span><span class="sxs-lookup"><span data-stu-id="642ec-293">All log messages are sent toologcat, in addition tooany custom log callbacks.</span></span>
<span data-ttu-id="642ec-294">Pode obter um ficheiro de registo de tooa do logcat da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="642ec-294">You can get a log tooa file from logcat as follows:</span></span>

    adb logcat > "C:\logmsg\logfile.txt"

 <span data-ttu-id="642ec-295">Para obter mais informações sobre os comandos adb, consulte Olá [logcat informações no site do Android Olá](https://developer.android.com/tools/debugging/debugging-log.html#startingLogcat).</span><span class="sxs-lookup"><span data-stu-id="642ec-295">For details about adb commands, see hello [logcat information on hello Android site](https://developer.android.com/tools/debugging/debugging-log.html#startingLogcat).</span></span>

#### <a name="network-traces"></a><span data-ttu-id="642ec-296">Rastreios de rede</span><span class="sxs-lookup"><span data-stu-id="642ec-296">Network traces</span></span>
<span data-ttu-id="642ec-297">Pode utilizar várias ferramentas toocapture Olá tráfego HTTP que gera ADAL.</span><span class="sxs-lookup"><span data-stu-id="642ec-297">You can use various tools toocapture hello HTTP traffic that ADAL generates.</span></span>  <span data-ttu-id="642ec-298">Isto é mais útil se estiver familiarizado com Olá protocolo de OAuth ou se precisar de tooprovide informações de diagnóstico tooMicrosoft ou outros canais de suporte.</span><span class="sxs-lookup"><span data-stu-id="642ec-298">This is most useful if you're familiar with hello OAuth protocol or if you need tooprovide diagnostic information tooMicrosoft or other support channels.</span></span>

<span data-ttu-id="642ec-299">Fiddler é Olá ferramenta de rastreio de HTTP mais fácil.</span><span class="sxs-lookup"><span data-stu-id="642ec-299">Fiddler is hello easiest HTTP tracing tool.</span></span> <span data-ttu-id="642ec-300">Seguinte de Olá utilize liga tooset-cópia de segurança toocorrectly registo ADAL tráfego de rede.</span><span class="sxs-lookup"><span data-stu-id="642ec-300">Use hello following links tooset it up toocorrectly record ADAL network traffic.</span></span> <span data-ttu-id="642ec-301">Para obter uma ferramenta de rastreio, como o Fiddler ou Charles toobe útil, tem de configurá-lo toorecord não encriptada SSL tráfego.</span><span class="sxs-lookup"><span data-stu-id="642ec-301">For a tracing tool like Fiddler or Charles toobe useful, you must configure it toorecord unencrypted SSL traffic.</span></span>  

> [!NOTE]
> <span data-ttu-id="642ec-302">Os rastreios gerados desta forma poderão conter informações privilegiadas como tokens de acesso, nomes de utilizador e palavras-passe.</span><span class="sxs-lookup"><span data-stu-id="642ec-302">Traces generated in this way might contain highly privileged information such as access tokens, usernames, and passwords.</span></span> <span data-ttu-id="642ec-303">Se estiver a utilizar contas de produção, não deve partilhe estes rastreios com terceiros.</span><span class="sxs-lookup"><span data-stu-id="642ec-303">If you're using production accounts, do not share these traces with third parties.</span></span> <span data-ttu-id="642ec-304">Se precisar de toosupply toosomeone um rastreio no suporte de tooget ordem, reproduza o problema de Olá utilizando uma conta temporária com nomes de utilizador e palavras-passe que não atenção a partilha.</span><span class="sxs-lookup"><span data-stu-id="642ec-304">If you need toosupply a trace toosomeone in order tooget support, reproduce hello issue by using a temporary account with usernames and passwords that you don't mind sharing.</span></span>

* <span data-ttu-id="642ec-305">A partir do site de Telerik Olá: [definição de cópia de segurança Fiddler para Android](http://docs.telerik.com/fiddler/configure-fiddler/tasks/ConfigureForAndroid)</span><span class="sxs-lookup"><span data-stu-id="642ec-305">From hello Telerik website: [Setting Up Fiddler For Android](http://docs.telerik.com/fiddler/configure-fiddler/tasks/ConfigureForAndroid)</span></span>
* <span data-ttu-id="642ec-306">A partir do GitHub: [configurar regras de Fiddler da ADAL](https://github.com/AzureAD/azure-activedirectory-library-for-android/wiki/How-to-listen-to-httpUrlConnection-in-Android-app-from-Fiddler)</span><span class="sxs-lookup"><span data-stu-id="642ec-306">From GitHub: [Configure Fiddler Rules For ADAL](https://github.com/AzureAD/azure-activedirectory-library-for-android/wiki/How-to-listen-to-httpUrlConnection-in-Android-app-from-Fiddler)</span></span>

### <a name="dialog-mode"></a><span data-ttu-id="642ec-307">Modo de caixa de diálogo</span><span class="sxs-lookup"><span data-stu-id="642ec-307">Dialog mode</span></span>
<span data-ttu-id="642ec-308">método de acquireToken Olá sem atividade suporta uma linha de comandos de caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="642ec-308">hello acquireToken method without activity supports a dialog prompt.</span></span>

### <a name="encryption"></a><span data-ttu-id="642ec-309">Encriptação</span><span class="sxs-lookup"><span data-stu-id="642ec-309">Encryption</span></span>
<span data-ttu-id="642ec-310">ADAL encripta tokens Olá e arquivo na SharedPreferences por predefinição.</span><span class="sxs-lookup"><span data-stu-id="642ec-310">ADAL encrypts hello tokens and store in SharedPreferences by default.</span></span> <span data-ttu-id="642ec-311">Pode ver detalhes da Olá toosee Olá StorageHelper classe.</span><span class="sxs-lookup"><span data-stu-id="642ec-311">You can look at hello StorageHelper class toosee hello details.</span></span> <span data-ttu-id="642ec-312">Android introduzida Android Keystore 4.3 (18 de API) de armazenamento seguro de chaves privadas.</span><span class="sxs-lookup"><span data-stu-id="642ec-312">Android introduced Android Keystore for 4.3 (API 18) secure storage of private keys.</span></span> <span data-ttu-id="642ec-313">ADAL utiliza esse para 18 de API e superiores.</span><span class="sxs-lookup"><span data-stu-id="642ec-313">ADAL uses that for API 18 and higher.</span></span> <span data-ttu-id="642ec-314">Se pretender toouse ADAL para versões do SDK inferiores, terá de tooprovide uma chave secreta no AuthenticationSettings.INSTANCE.setSecretKey.</span><span class="sxs-lookup"><span data-stu-id="642ec-314">If you want toouse ADAL for lower SDK versions, you need tooprovide a secret key at AuthenticationSettings.INSTANCE.setSecretKey.</span></span>

### <a name="oauth2-bearer-challenge"></a><span data-ttu-id="642ec-315">Desafio de portador do OAuth2</span><span class="sxs-lookup"><span data-stu-id="642ec-315">OAuth2 bearer challenge</span></span>
<span data-ttu-id="642ec-316">Olá AuthenticationParameters classe fornece funcionalidade tooget authorization_uri de Olá desafio de portador do OAuth2.</span><span class="sxs-lookup"><span data-stu-id="642ec-316">hello AuthenticationParameters class provides functionality tooget authorization_uri from hello OAuth2 bearer challenge.</span></span>

### <a name="session-cookies-in-webview"></a><span data-ttu-id="642ec-317">Cookies de sessão no WebView</span><span class="sxs-lookup"><span data-stu-id="642ec-317">Session cookies in WebView</span></span>
<span data-ttu-id="642ec-318">Android WebView não limpa cookies de sessão após a aplicação Olá está fechada.</span><span class="sxs-lookup"><span data-stu-id="642ec-318">Android WebView does not clear session cookies after hello app is closed.</span></span> <span data-ttu-id="642ec-319">Pode processar que ao utilizar este código de exemplo:</span><span class="sxs-lookup"><span data-stu-id="642ec-319">You can handle that by using this sample code:</span></span>

    CookieSyncManager.createInstance(getApplicationContext());
    CookieManager cookieManager = CookieManager.getInstance();
    cookieManager.removeSessionCookie();
    CookieSyncManager.getInstance().sync();

<span data-ttu-id="642ec-320">Para obter mais informações sobre os cookies, consulte Olá [CookieSyncManager informações no site do Android Olá](http://developer.android.com/reference/android/webkit/CookieSyncManager.html).</span><span class="sxs-lookup"><span data-stu-id="642ec-320">For details about cookies, see hello [CookieSyncManager information on hello Android site](http://developer.android.com/reference/android/webkit/CookieSyncManager.html).</span></span>

### <a name="resource-overrides"></a><span data-ttu-id="642ec-321">Substituições de recursos</span><span class="sxs-lookup"><span data-stu-id="642ec-321">Resource overrides</span></span>
<span data-ttu-id="642ec-322">biblioteca da ADAL Olá inclui cadeias inglês ProgressDialog mensagens.</span><span class="sxs-lookup"><span data-stu-id="642ec-322">hello ADAL library includes English strings for ProgressDialog messages.</span></span> <span data-ttu-id="642ec-323">A aplicação deve substituí-los se pretender que as cadeias localizadas.</span><span class="sxs-lookup"><span data-stu-id="642ec-323">Your application should overwrite them if you want localized strings.</span></span>

     <string name="app_loading">Loading...</string>
     <string name="broker_processing">Broker is processing</string>
     <string name="http_auth_dialog_username">Username</string>
     <string name="http_auth_dialog_password">Password</string>
     <string name="http_auth_dialog_title">Sign In</string>
     <string name="http_auth_dialog_login">Login</string>
     <string name="http_auth_dialog_cancel">Cancel</string>

### <a name="ntlm-dialog-box"></a><span data-ttu-id="642ec-324">Caixa de diálogo NTLM</span><span class="sxs-lookup"><span data-stu-id="642ec-324">NTLM dialog box</span></span>
<span data-ttu-id="642ec-325">Versão da ADAL 1.1.0 suporta uma caixa de diálogo NTLM é processada através do evento onReceivedHttpAuthRequest Olá WebViewClient.</span><span class="sxs-lookup"><span data-stu-id="642ec-325">ADAL version 1.1.0 supports an NTLM dialog box that is processed through hello onReceivedHttpAuthRequest event from WebViewClient.</span></span> <span data-ttu-id="642ec-326">Pode personalizar o esquema de Olá e cadeias de caixa de diálogo Olá.</span><span class="sxs-lookup"><span data-stu-id="642ec-326">You can customize hello layout and strings for hello dialog box.</span></span>

### <a name="cross-app-sso"></a><span data-ttu-id="642ec-327">SSO em várias aplicações</span><span class="sxs-lookup"><span data-stu-id="642ec-327">Cross-app SSO</span></span>
<span data-ttu-id="642ec-328">Saiba [como tooenable SSO em várias aplicações no Android utilizando ADAL](active-directory-sso-android.md).</span><span class="sxs-lookup"><span data-stu-id="642ec-328">Learn [how tooenable cross-app SSO on Android by using ADAL](active-directory-sso-android.md).</span></span>  

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
