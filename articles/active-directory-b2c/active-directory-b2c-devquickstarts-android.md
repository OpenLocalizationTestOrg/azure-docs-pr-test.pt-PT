---
title: "O Azure Active Directory B2C: Adquirir um token a utilizar uma aplicação Android | Microsoft Docs"
description: "Este artigo irá mostrar como toocreate uma aplicação Android que utiliza AppAuth com identidades de utilizador do Azure Active Directory B2C toomanage e autentica utilizadores."
services: active-directory-b2c
documentationcenter: android
author: parakhj
manager: krassk
editor: 
ms.assetid: d00947c3-dcaa-4cb3-8c2e-d94e0746d8b2
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: article
ms.date: 03/06/2017
ms.author: parakhj
ms.openlocfilehash: 0236398673115a34951f035cb1e73e89417abf86
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-sign-in-using-an-android-application"></a><span data-ttu-id="ca8ad-103">O Azure AD B2C: Início de sessão utilizando uma aplicação Android</span><span class="sxs-lookup"><span data-stu-id="ca8ad-103">Azure AD B2C: Sign-in using an Android application</span></span>

<span data-ttu-id="ca8ad-104">plataforma de identidade do Microsoft Olá utiliza as normas de abertura, como o OAuth2 e o OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="ca8ad-104">hello Microsoft identity platform uses open standards such as OAuth2 and OpenID Connect.</span></span> <span data-ttu-id="ca8ad-105">Isto permite aos programadores tooleverage qualquer biblioteca que pretendam toointegrate aos nossos serviços.</span><span class="sxs-lookup"><span data-stu-id="ca8ad-105">This allows developers tooleverage any library they wish toointegrate with our services.</span></span> <span data-ttu-id="ca8ad-106">os programadores de tooaid utilizando a nossa plataforma com outras bibliotecas, escrevemos algumas instruções como esta um toodemonstrate como tooconfigure 3rd terceiros bibliotecas tooconnect toohello Microsoft plataforma de identidade.</span><span class="sxs-lookup"><span data-stu-id="ca8ad-106">tooaid developers in using our platform with other libraries, we've written a few walkthroughs like this one toodemonstrate how tooconfigure 3rd party libraries tooconnect toohello Microsoft identity platform.</span></span> <span data-ttu-id="ca8ad-107">A maioria das bibliotecas que implementam [spec Olá especificação RFC6749 OAuth2](https://tools.ietf.org/html/rfc6749) será plataforma do tooconnect capaz de toohello Microsoft Identity.</span><span class="sxs-lookup"><span data-stu-id="ca8ad-107">Most libraries that implement [hello RFC6749 OAuth2 spec](https://tools.ietf.org/html/rfc6749) will be able tooconnect toohello Microsoft Identity platform.</span></span>

> [!WARNING]
> <span data-ttu-id="ca8ad-108">A Microsoft não cede correções para 3rd bibliotecas de terceiros e não tiverem efetuado uma revisão desses bibliotecas.</span><span class="sxs-lookup"><span data-stu-id="ca8ad-108">Microsoft does not provide fixes for 3rd party libraries and has not done a review of those libraries.</span></span> <span data-ttu-id="ca8ad-109">Este exemplo está a utilizar uma biblioteca de terceiros 3rd chamada AppAuth foi testado para compatibilidade em cenários básicos com Olá, Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="ca8ad-109">This sample is using a 3rd party library called AppAuth that has been tested for compatibility in basic scenarios with hello Azure AD B2C.</span></span> <span data-ttu-id="ca8ad-110">Problemas e pedidos de funcionalidades devem ser o projeto de fonte aberta da biblioteca de toohello direcionados.</span><span class="sxs-lookup"><span data-stu-id="ca8ad-110">Issues and feature requests should be directed toohello library's open-source project.</span></span> <span data-ttu-id="ca8ad-111">Consulte [neste artigo](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-libraries) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="ca8ad-111">Please see [this article](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-libraries) for more information.</span></span>  
>
>

<span data-ttu-id="ca8ad-112">Se tiver tooOAuth2 novo ou o OpenID Connect muito este exemplo de configuração poderá não fazer muito sentido tooyou.</span><span class="sxs-lookup"><span data-stu-id="ca8ad-112">If you're new tooOAuth2 or OpenID Connect much of this sample configuration may not make much sense tooyou.</span></span> <span data-ttu-id="ca8ad-113">Recomendamos que leia a breve [descrição geral do protocolo de Olá aqui documentado](active-directory-b2c-reference-protocols.md).</span><span class="sxs-lookup"><span data-stu-id="ca8ad-113">We recommend you look at a brief [overview of hello protocol we've documented here](active-directory-b2c-reference-protocols.md).</span></span>

## <a name="get-an-azure-ad-b2c-directory"></a><span data-ttu-id="ca8ad-114">Obter um diretório do Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="ca8ad-114">Get an Azure AD B2C directory</span></span>

<span data-ttu-id="ca8ad-115">Para poder utilizar o Azure AD B2C, tem de criar um diretório ou inquilino.</span><span class="sxs-lookup"><span data-stu-id="ca8ad-115">Before you can use Azure AD B2C, you must create a directory, or tenant.</span></span> <span data-ttu-id="ca8ad-116">Um diretório é um contentor para todos os seus utilizadores, aplicações, grupos, etc.</span><span class="sxs-lookup"><span data-stu-id="ca8ad-116">A directory is a container for all of your users, apps, groups, and more.</span></span> <span data-ttu-id="ca8ad-117">Se ainda não tiver um, [crie um diretório do B2C](active-directory-b2c-get-started.md) antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="ca8ad-117">If you don't have one already, [create a B2C directory](active-directory-b2c-get-started.md) before you continue.</span></span>

## <a name="create-an-application"></a><span data-ttu-id="ca8ad-118">Criar uma aplicação</span><span class="sxs-lookup"><span data-stu-id="ca8ad-118">Create an application</span></span>

<span data-ttu-id="ca8ad-119">Em seguida, terá de toocreate uma aplicação no diretório do B2C.</span><span class="sxs-lookup"><span data-stu-id="ca8ad-119">Next, you need toocreate an app in your B2C directory.</span></span> <span data-ttu-id="ca8ad-120">Isto dá-informações do Azure AD que necessita de toocommunicate em segurança com a sua aplicação.</span><span class="sxs-lookup"><span data-stu-id="ca8ad-120">This gives Azure AD information that it needs toocommunicate securely with your app.</span></span> <span data-ttu-id="ca8ad-121">toocreate uma aplicação móvel, siga [estas instruções](active-directory-b2c-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="ca8ad-121">toocreate a mobile app, follow [these instructions](active-directory-b2c-app-registration.md).</span></span> <span data-ttu-id="ca8ad-122">É necessário:</span><span class="sxs-lookup"><span data-stu-id="ca8ad-122">Be sure to:</span></span>

* <span data-ttu-id="ca8ad-123">Incluir um **Native Client** na aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="ca8ad-123">Include a **Native Client** in hello application.</span></span>
* <span data-ttu-id="ca8ad-124">Olá cópia **ID da aplicação** que é atribuído tooyour aplicação.</span><span class="sxs-lookup"><span data-stu-id="ca8ad-124">Copy hello **Application ID** that is assigned tooyour app.</span></span> <span data-ttu-id="ca8ad-125">Irá precisar deste mais tarde.</span><span class="sxs-lookup"><span data-stu-id="ca8ad-125">You will need this later.</span></span>
* <span data-ttu-id="ca8ad-126">Configurar um cliente nativo **URI de redirecionamento** (por exemplo, com.onmicrosoft.fabrikamb2c.exampleapp://oauth/redirect).</span><span class="sxs-lookup"><span data-stu-id="ca8ad-126">Set up a native client **Redirect URI** (e.g. com.onmicrosoft.fabrikamb2c.exampleapp://oauth/redirect).</span></span> <span data-ttu-id="ca8ad-127">Também irá precisar deste mais tarde.</span><span class="sxs-lookup"><span data-stu-id="ca8ad-127">You will also need this later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a><span data-ttu-id="ca8ad-128">Criar as políticas</span><span class="sxs-lookup"><span data-stu-id="ca8ad-128">Create your policies</span></span>

<span data-ttu-id="ca8ad-129">No Azure AD B2C, cada experiência de utilizador é definida por uma [política](active-directory-b2c-reference-policies.md).</span><span class="sxs-lookup"><span data-stu-id="ca8ad-129">In Azure AD B2C, every user experience is defined by a [policy](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="ca8ad-130">Esta aplicação contém uma experiência de identidade: um combinado início de sessão e inscrição.</span><span class="sxs-lookup"><span data-stu-id="ca8ad-130">This app contains one identity experience: a combined sign-in and sign-up.</span></span> <span data-ttu-id="ca8ad-131">Terá de toocreate desta política, conforme descrito no [artigo de referência de política](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span><span class="sxs-lookup"><span data-stu-id="ca8ad-131">You need toocreate this policy, as described in the [policy reference article](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span></span> <span data-ttu-id="ca8ad-132">Quando criar política Olá, não se esqueça de:</span><span class="sxs-lookup"><span data-stu-id="ca8ad-132">When you create hello policy, be sure to:</span></span>

* <span data-ttu-id="ca8ad-133">Escolha Olá **nome a apresentar** como um atributo na política de inscrição.</span><span class="sxs-lookup"><span data-stu-id="ca8ad-133">Choose hello **Display name** as a sign-up attribute in your policy.</span></span>
* <span data-ttu-id="ca8ad-134">Escolha Olá **nome a apresentar** e **ID de objeto** afirmações de aplicação em cada política.</span><span class="sxs-lookup"><span data-stu-id="ca8ad-134">Choose hello **Display name** and **Object ID** application claims in every policy.</span></span> <span data-ttu-id="ca8ad-135">Também pode escolher outras afirmações.</span><span class="sxs-lookup"><span data-stu-id="ca8ad-135">You can choose other claims as well.</span></span>
* <span data-ttu-id="ca8ad-136">Olá cópia **nome** de cada política depois de a criar.</span><span class="sxs-lookup"><span data-stu-id="ca8ad-136">Copy hello **Name** of each policy after you create it.</span></span> <span data-ttu-id="ca8ad-137">Deve ter o prefixo de Olá `b2c_1_`.</span><span class="sxs-lookup"><span data-stu-id="ca8ad-137">It should have hello prefix `b2c_1_`.</span></span>  <span data-ttu-id="ca8ad-138">Terá de nome da política hello mais tarde.</span><span class="sxs-lookup"><span data-stu-id="ca8ad-138">You'll need hello policy name later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

<span data-ttu-id="ca8ad-139">Depois de criar as políticas, está pronto toobuild a aplicação.</span><span class="sxs-lookup"><span data-stu-id="ca8ad-139">After you have created your policies, you're ready toobuild your app.</span></span>

## <a name="download-hello-sample-code"></a><span data-ttu-id="ca8ad-140">Transferir o código de exemplo de Olá</span><span class="sxs-lookup"><span data-stu-id="ca8ad-140">Download hello sample code</span></span>

<span data-ttu-id="ca8ad-141">Fornecemos um exemplo de trabalho que utiliza AppAuth com o Azure AD B2C [no GitHub](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c).</span><span class="sxs-lookup"><span data-stu-id="ca8ad-141">We have provided a working sample that uses AppAuth with Azure AD B2C [on GitHub](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c).</span></span> <span data-ttu-id="ca8ad-142">Pode transferir Olá código e executá-la.</span><span class="sxs-lookup"><span data-stu-id="ca8ad-142">You can download hello code and run it.</span></span> <span data-ttu-id="ca8ad-143">Pode rapidamente começar a utilizar com a sua própria aplicação utilizando a sua própria configuração do Azure AD B2C ao seguir as instruções de Olá Olá [README.md](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c/blob/master/README.md).</span><span class="sxs-lookup"><span data-stu-id="ca8ad-143">You can quickly get started with your own app using your own Azure AD B2C configuration by following hello instructions in hello [README.md](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c/blob/master/README.md).</span></span>

<span data-ttu-id="ca8ad-144">exemplo de Olá é uma modificação de exemplo de Olá fornecida pelo [AppAuth](https://openid.github.io/AppAuth-Android/).</span><span class="sxs-lookup"><span data-stu-id="ca8ad-144">hello sample is a modification of hello sample provided by [AppAuth](https://openid.github.io/AppAuth-Android/).</span></span> <span data-ttu-id="ca8ad-145">Visite os respetivos toolearn página mais informações sobre AppAuth e as respetivas funcionalidades.</span><span class="sxs-lookup"><span data-stu-id="ca8ad-145">Please visit their page toolearn more about AppAuth and its features.</span></span>

## <a name="modifying-your-app-toouse-azure-ad-b2c-with-appauth"></a><span data-ttu-id="ca8ad-146">Modificar o toouse de aplicação do Azure AD B2C com AppAuth</span><span class="sxs-lookup"><span data-stu-id="ca8ad-146">Modifying your app toouse Azure AD B2C with AppAuth</span></span>

> [!NOTE]
> <span data-ttu-id="ca8ad-147">AppAuth suporta Android API 16 (Jellybean) e superior.</span><span class="sxs-lookup"><span data-stu-id="ca8ad-147">AppAuth supports Android API 16 (Jellybean) and above.</span></span> <span data-ttu-id="ca8ad-148">Recomendamos que utilize a API 23 e superior.</span><span class="sxs-lookup"><span data-stu-id="ca8ad-148">We recommend using API 23 and above.</span></span>
>

### <a name="configuration"></a><span data-ttu-id="ca8ad-149">Configuração</span><span class="sxs-lookup"><span data-stu-id="ca8ad-149">Configuration</span></span>

<span data-ttu-id="ca8ad-150">Pode configurar a comunicação com o Azure AD B2C por detetar Olá especificação URI ou especificando um ponto final de autorização de Olá e o ponto final de tokens de URI.</span><span class="sxs-lookup"><span data-stu-id="ca8ad-150">You can configure communication with Azure AD B2C by either specifying hello discovery URI or by specifying both hello authorization endpoint and token endpoint URIs.</span></span> <span data-ttu-id="ca8ad-151">Em ambos os casos, terá de Olá seguintes informações:</span><span class="sxs-lookup"><span data-stu-id="ca8ad-151">In either case, you will need hello following information:</span></span>

* <span data-ttu-id="ca8ad-152">ID do inquilino (por exemplo, contoso.onmicrosoft.com)</span><span class="sxs-lookup"><span data-stu-id="ca8ad-152">Tenant ID (e.g. contoso.onmicrosoft.com)</span></span>
* <span data-ttu-id="ca8ad-153">Nome da política (por exemplo, B2C\_1\_SignUpIn)</span><span class="sxs-lookup"><span data-stu-id="ca8ad-153">Policy name (e.g. B2C\_1\_SignUpIn)</span></span>

<span data-ttu-id="ca8ad-154">Se escolher tooautomatically detetar Olá autorização e tokens endpoint URIs, irá necessitar de informações de toofetch da deteção de Olá URI.</span><span class="sxs-lookup"><span data-stu-id="ca8ad-154">If you choose tooautomatically discover hello authorization and token endpoint URIs, you will need toofetch information from hello discovery URI.</span></span> <span data-ttu-id="ca8ad-155">Deteção de Olá URI que pode ser gerado ao substituir Olá inquilino\_ID e a política de Olá\_nome no Olá seguinte URL:</span><span class="sxs-lookup"><span data-stu-id="ca8ad-155">hello discovery URI can be generated by replacing hello Tenant\_ID and hello Policy\_Name in hello following URL:</span></span>

```java
String mDiscoveryURI = "https://login.microsoftonline.com/<Tenant_ID>/v2.0/.well-known/openid-configuration?p=<Policy_Name>";
```

<span data-ttu-id="ca8ad-156">Em seguida, pode adquirir Olá autorização e de ponto final de tokens URIs e criar um objeto de AuthorizationServiceConfiguration executando o seguinte Olá:</span><span class="sxs-lookup"><span data-stu-id="ca8ad-156">You can then acquire hello authorization and token endpoint URIs and create an AuthorizationServiceConfiguration object by running hello following:</span></span>

```java
final Uri issuerUri = Uri.parse(mDiscoveryURI);
AuthorizationServiceConfiguration config;

AuthorizationServiceConfiguration.fetchFromIssuer(
    issuerUri,
    new RetrieveConfigurationCallback() {
      @Override public void onFetchConfigurationCompleted(
          @Nullable AuthorizationServiceConfiguration serviceConfiguration,
          @Nullable AuthorizationException ex) {
        if (ex != null) {
            Log.w(TAG, "Failed tooretrieve configuration for " + issuerUri, ex);
        } else {
            // service configuration retrieved, proceed tooauthorization...
        }
      }
  });
```

<span data-ttu-id="ca8ad-157">Em vez de utilizar a autorização de Olá tooobtain de deteção e o ponto final de tokens URIs, também pode especificá-los explicitamente, substituindo Olá inquilino\_ID e a política de Olá\_nome no URL de Olá abaixo:</span><span class="sxs-lookup"><span data-stu-id="ca8ad-157">Instead of using discovery tooobtain hello authorization and token endpoint URIs, you can also specify them explicitly by replacing hello Tenant\_ID and hello Policy\_Name in hello URL's below:</span></span>

```java
String mAuthEndpoint = "https://login.microsoftonline.com/<Tenant_ID>/oauth2/v2.0/authorize?p=<Policy_Name>";

String mTokenEndpoint = "https://login.microsoftonline.com/<Tenant_ID>/oauth2/v2.0/token?p=<Policy_Name>";
```

<span data-ttu-id="ca8ad-158">Execute Olá toocreate de código a seguir o objeto de AuthorizationServiceConfiguration:</span><span class="sxs-lookup"><span data-stu-id="ca8ad-158">Run hello following code toocreate your AuthorizationServiceConfiguration object:</span></span>

```java
AuthorizationServiceConfiguration config =
        new AuthorizationServiceConfiguration(name, mAuthEndpoint, mTokenEndpoint);

// perform hello auth request...
```

### <a name="authorizing"></a><span data-ttu-id="ca8ad-159">Autorizar</span><span class="sxs-lookup"><span data-stu-id="ca8ad-159">Authorizing</span></span>

<span data-ttu-id="ca8ad-160">Depois de configurar ou obtenção de uma configuração de serviço de autorização, pode ser construído a um pedido de autorização.</span><span class="sxs-lookup"><span data-stu-id="ca8ad-160">After configuring or retrieving an authorization service configuration, an authorization request can be constructed.</span></span> <span data-ttu-id="ca8ad-161">pedir toocreate Olá, terá de Olá seguintes informações:</span><span class="sxs-lookup"><span data-stu-id="ca8ad-161">toocreate hello request, you will need hello following information:</span></span>

* <span data-ttu-id="ca8ad-162">ID de cliente (por exemplo, 00000000-0000-0000-0000-000000000000)</span><span class="sxs-lookup"><span data-stu-id="ca8ad-162">Client ID (e.g. 00000000-0000-0000-0000-000000000000)</span></span>
* <span data-ttu-id="ca8ad-163">URI de redirecionamento com um esquema personalizado (por exemplo, com.onmicrosoft.fabrikamb2c.exampleapp://oauthredirect)</span><span class="sxs-lookup"><span data-stu-id="ca8ad-163">Redirect URI with a custom scheme (e.g. com.onmicrosoft.fabrikamb2c.exampleapp://oauthredirect)</span></span>

<span data-ttu-id="ca8ad-164">Ambos os itens devem ter sido guardados quando era [registar a sua aplicação](#create-an-application).</span><span class="sxs-lookup"><span data-stu-id="ca8ad-164">Both items should have been saved when you were [registering your app](#create-an-application).</span></span>

```java
AuthorizationRequest req = new AuthorizationRequest.Builder(
    config,
    clientId,
    ResponseTypeValues.CODE,
    redirectUri)
    .build();
```

<span data-ttu-id="ca8ad-165">Consulte toohello [AppAuth guia](https://openid.github.io/AppAuth-Android/) no como toocomplete Olá rest do processo de Olá.</span><span class="sxs-lookup"><span data-stu-id="ca8ad-165">Please refer toohello [AppAuth guide](https://openid.github.io/AppAuth-Android/) on how toocomplete hello rest of hello process.</span></span> <span data-ttu-id="ca8ad-166">Se precisar de tooquickly começar com uma aplicação de trabalho, consulte [nosso exemplo](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c).</span><span class="sxs-lookup"><span data-stu-id="ca8ad-166">If you need tooquickly get started with a working app, check out [our sample](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c).</span></span> <span data-ttu-id="ca8ad-167">Siga os passos de Olá Olá [README.md](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c/blob/master/README.md) tooenter a própria configuração do Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="ca8ad-167">Follow hello steps in hello [README.md](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c/blob/master/README.md) tooenter your own Azure AD B2C configuration.</span></span>

<span data-ttu-id="ca8ad-168">Estamos sempre toofeedback aberta e sugestões!</span><span class="sxs-lookup"><span data-stu-id="ca8ad-168">We are always open toofeedback and suggestions!</span></span> <span data-ttu-id="ca8ad-169">Se tiver dificuldades em causa com este tópico ou tiver recomendações para melhorar este conteúdo, Agradecemos os seus comentários na Olá parte inferior da página Olá.</span><span class="sxs-lookup"><span data-stu-id="ca8ad-169">If you have any difficulties with this topic, or have recommendations for improving this content, we would appreciate your feedback at hello bottom of hello page.</span></span> <span data-ttu-id="ca8ad-170">Para pedidos de funcionalidades, adicioná-los demasiado[UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c).</span><span class="sxs-lookup"><span data-stu-id="ca8ad-170">For feature requests, add them too[UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c).</span></span>

