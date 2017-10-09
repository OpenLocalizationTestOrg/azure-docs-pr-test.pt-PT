---
title: "Adquirir um token a utilizar uma aplicação iOS - Azure AD B2C | Microsoft Docs"
description: "Este artigo irá mostrar como toocreate uma aplicação iOS que utiliza AppAuth com identidades de utilizador do Azure Active Directory B2C toomanage e autentica utilizadores."
services: active-directory-b2c
documentationcenter: ios
author: saeedakhter-msft
manager: krassk
editor: parakhj
ms.assetid: d818a634-42c2-4cbd-bf73-32fa0c8c69d3
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: mobile-ios
ms.devlang: objectivec
ms.topic: article
ms.date: 03/07/2017
ms.author: saeedakhter-msft
ms.openlocfilehash: e7cbe2de6e9ae3d45448cdd36292c457a0ef4887
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-sign-in-using-an-ios-application"></a><span data-ttu-id="aff6b-103">O Azure AD B2C: Início de sessão utilizando uma aplicação iOS</span><span class="sxs-lookup"><span data-stu-id="aff6b-103">Azure AD B2C: Sign-in using an iOS application</span></span>

<span data-ttu-id="aff6b-104">plataforma de identidade do Microsoft Olá utiliza as normas de abertura, como o OAuth2 e o OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="aff6b-104">hello Microsoft identity platform uses open standards such as OAuth2 and OpenID Connect.</span></span> <span data-ttu-id="aff6b-105">Utilizar um protocolo padrão aberto oferece mais opções de programador quando selecionar um toointegrate biblioteca aos nossos serviços.</span><span class="sxs-lookup"><span data-stu-id="aff6b-105">Using an open standard protocol offers more developer choice when selecting a library toointegrate with our services.</span></span> <span data-ttu-id="aff6b-106">Fornecemos esta explicação passo a passo e outros, como se tooaid programadores com aplicações que ligam a plataforma do Microsoft Identity de toohello escrita.</span><span class="sxs-lookup"><span data-stu-id="aff6b-106">We've provided this walkthrough and others like it tooaid developers with writing applications that connect toohello Microsoft Identity platform.</span></span> <span data-ttu-id="aff6b-107">A maioria das bibliotecas que implementam [spec Olá especificação RFC6749 OAuth2](https://tools.ietf.org/html/rfc6749) são plataforma do tooconnect capaz de toohello Microsoft Identity.</span><span class="sxs-lookup"><span data-stu-id="aff6b-107">Most libraries that implement [hello RFC6749 OAuth2 spec](https://tools.ietf.org/html/rfc6749) are able tooconnect toohello Microsoft Identity platform.</span></span>

> [!WARNING]
> <span data-ttu-id="aff6b-108">A Microsoft não cede corrige para bibliotecas de terceiros e não tiver efetuado uma revisão desses bibliotecas.</span><span class="sxs-lookup"><span data-stu-id="aff6b-108">Microsoft does not provide fixes for third-party libraries and has not done a review of those libraries.</span></span> <span data-ttu-id="aff6b-109">Este exemplo está a utilizar uma biblioteca de terceiros chamada AppAuth foi testado para compatibilidade em cenários básicos com Olá, Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="aff6b-109">This sample is using a third-party library called AppAuth that has been tested for compatibility in basic scenarios with hello Azure AD B2C.</span></span> <span data-ttu-id="aff6b-110">Problemas e pedidos de funcionalidades devem ser o projeto de fonte aberta da biblioteca de toohello direcionados.</span><span class="sxs-lookup"><span data-stu-id="aff6b-110">Issues and feature requests should be directed toohello library's open-source project.</span></span> <span data-ttu-id="aff6b-111">Para obter mais informações, consulte [este artigo](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-libraries).</span><span class="sxs-lookup"><span data-stu-id="aff6b-111">For more information, see [this article](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-libraries).</span></span>
>
>

<span data-ttu-id="aff6b-112">Se tiver tooOAuth2 novo ou o OpenID Connect, muito este exemplo de configuração poderá não fazer muito sentido tooyou.</span><span class="sxs-lookup"><span data-stu-id="aff6b-112">If you're new tooOAuth2 or OpenID Connect, much of this sample configuration may not make much sense tooyou.</span></span> <span data-ttu-id="aff6b-113">Recomendamos que leia a breve [descrição geral do protocolo de Olá aqui documentado](active-directory-b2c-reference-protocols.md).</span><span class="sxs-lookup"><span data-stu-id="aff6b-113">We recommend you look at a brief [overview of hello protocol we've documented here](active-directory-b2c-reference-protocols.md).</span></span>

## <a name="get-an-azure-ad-b2c-directory"></a><span data-ttu-id="aff6b-114">Obter um diretório do Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="aff6b-114">Get an Azure AD B2C directory</span></span>
<span data-ttu-id="aff6b-115">Para poder utilizar o Azure AD B2C, tem de criar um diretório ou inquilino.</span><span class="sxs-lookup"><span data-stu-id="aff6b-115">Before you can use Azure AD B2C, you must create a directory, or tenant.</span></span> <span data-ttu-id="aff6b-116">Um diretório é um contentor para todos os seus utilizadores, aplicações, grupos e muito mais.</span><span class="sxs-lookup"><span data-stu-id="aff6b-116">A directory is a container for all your users, apps, groups, and more.</span></span> <span data-ttu-id="aff6b-117">Se ainda não tiver um, [crie um diretório do B2C](active-directory-b2c-get-started.md) antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="aff6b-117">If you don't have one already, [create a B2C directory](active-directory-b2c-get-started.md) before you continue.</span></span>

## <a name="create-an-application"></a><span data-ttu-id="aff6b-118">Criar uma aplicação</span><span class="sxs-lookup"><span data-stu-id="aff6b-118">Create an application</span></span>
<span data-ttu-id="aff6b-119">Em seguida, terá de toocreate uma aplicação no diretório do B2C.</span><span class="sxs-lookup"><span data-stu-id="aff6b-119">Next, you need toocreate an app in your B2C directory.</span></span> <span data-ttu-id="aff6b-120">registo de aplicação Olá dá-informações do Azure AD que necessita de toocommunicate em segurança com a sua aplicação.</span><span class="sxs-lookup"><span data-stu-id="aff6b-120">hello app registration gives Azure AD information that it needs toocommunicate securely with your app.</span></span> <span data-ttu-id="aff6b-121">toocreate uma aplicação móvel, siga [estas instruções](active-directory-b2c-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="aff6b-121">toocreate a mobile app, follow [these instructions](active-directory-b2c-app-registration.md).</span></span> <span data-ttu-id="aff6b-122">É necessário:</span><span class="sxs-lookup"><span data-stu-id="aff6b-122">Be sure to:</span></span>

* <span data-ttu-id="aff6b-123">Incluir um **cliente nativo** na aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="aff6b-123">Include a **Native client** in hello application.</span></span>
* <span data-ttu-id="aff6b-124">Olá cópia **ID da aplicação** que é atribuído tooyour aplicação.</span><span class="sxs-lookup"><span data-stu-id="aff6b-124">Copy hello **Application ID** that is assigned tooyour app.</span></span> <span data-ttu-id="aff6b-125">Este GUID é necessário mais tarde.</span><span class="sxs-lookup"><span data-stu-id="aff6b-125">You need this GUID later.</span></span>
* <span data-ttu-id="aff6b-126">Configurar um **URI de redirecionamento** com um esquema personalizado (por exemplo, com.onmicrosoft.fabrikamb2c.exampleapp://oauth/redirect).</span><span class="sxs-lookup"><span data-stu-id="aff6b-126">Set up a **Redirect URI** with a custom scheme (for example, com.onmicrosoft.fabrikamb2c.exampleapp://oauth/redirect).</span></span> <span data-ttu-id="aff6b-127">É necessário este URI mais tarde.</span><span class="sxs-lookup"><span data-stu-id="aff6b-127">You need this URI later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a><span data-ttu-id="aff6b-128">Criar as políticas</span><span class="sxs-lookup"><span data-stu-id="aff6b-128">Create your policies</span></span>
<span data-ttu-id="aff6b-129">No Azure AD B2C, cada experiência de utilizador é definida por uma [política](active-directory-b2c-reference-policies.md).</span><span class="sxs-lookup"><span data-stu-id="aff6b-129">In Azure AD B2C, every user experience is defined by a [policy](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="aff6b-130">Esta aplicação contém uma experiência de identidade: um combinado início de sessão e inscrição.</span><span class="sxs-lookup"><span data-stu-id="aff6b-130">This app contains one identity experience: a combined sign-in and sign-up.</span></span> <span data-ttu-id="aff6b-131">Crie esta política, conforme descrito no [artigo de referência de política](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span><span class="sxs-lookup"><span data-stu-id="aff6b-131">Create this policy as described in the [policy reference article](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span></span> <span data-ttu-id="aff6b-132">Quando criar política Olá, não se esqueça de:</span><span class="sxs-lookup"><span data-stu-id="aff6b-132">When you create hello policy, be sure to:</span></span>

* <span data-ttu-id="aff6b-133">Em **atributos de inscrição**, selecione o atributo de Olá **nome a apresentar**.</span><span class="sxs-lookup"><span data-stu-id="aff6b-133">Under **Sign-up attributes**, select hello attribute **Display name**.</span></span>  <span data-ttu-id="aff6b-134">Pode selecionar, bem como outros atributos.</span><span class="sxs-lookup"><span data-stu-id="aff6b-134">You can select other attributes as well.</span></span>
* <span data-ttu-id="aff6b-135">Em **afirmações de aplicação**, selecionar Olá afirmações **nome a apresentar** e **ID de objeto do utilizador**.</span><span class="sxs-lookup"><span data-stu-id="aff6b-135">Under **Application claims**, select hello claims **Display name** and **User's Object ID**.</span></span> <span data-ttu-id="aff6b-136">Pode selecionar outras afirmações.</span><span class="sxs-lookup"><span data-stu-id="aff6b-136">You can select other claims as well.</span></span>
* <span data-ttu-id="aff6b-137">Olá cópia **nome** de cada política depois de a criar.</span><span class="sxs-lookup"><span data-stu-id="aff6b-137">Copy hello **Name** of each policy after you create it.</span></span> <span data-ttu-id="aff6b-138">O nome da sua política é o prefixo `b2c_1_` quando guardar política Olá.</span><span class="sxs-lookup"><span data-stu-id="aff6b-138">Your policy name is prefixed with `b2c_1_` when you save hello policy.</span></span>  <span data-ttu-id="aff6b-139">É necessário o nome da política Olá mais tarde.</span><span class="sxs-lookup"><span data-stu-id="aff6b-139">You need hello policy name later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

<span data-ttu-id="aff6b-140">Depois de criar as políticas, está pronto toobuild a aplicação.</span><span class="sxs-lookup"><span data-stu-id="aff6b-140">After you have created your policies, you're ready toobuild your app.</span></span>

## <a name="download-hello-sample-code"></a><span data-ttu-id="aff6b-141">Transferir o código de exemplo de Olá</span><span class="sxs-lookup"><span data-stu-id="aff6b-141">Download hello sample code</span></span>
<span data-ttu-id="aff6b-142">Fornecemos um exemplo de trabalho que utiliza AppAuth com o Azure AD B2C [no GitHub](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c).</span><span class="sxs-lookup"><span data-stu-id="aff6b-142">We have provided a working sample that uses AppAuth with Azure AD B2C [on GitHub](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c).</span></span> <span data-ttu-id="aff6b-143">Pode transferir Olá código e executá-la.</span><span class="sxs-lookup"><span data-stu-id="aff6b-143">You can download hello code and run it.</span></span> <span data-ttu-id="aff6b-144">toouse inquilino a sua própria do Azure AD B2C, siga as instruções de Olá Olá [README.md](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c/blob/master/README.md).</span><span class="sxs-lookup"><span data-stu-id="aff6b-144">toouse your own Azure AD B2C tenant, follow hello instructions in hello [README.md](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c/blob/master/README.md).</span></span>

<span data-ttu-id="aff6b-145">Este exemplo foi criado ao seguir as instruções de Leia-me Olá por Olá [projeto iOS AppAuth no GitHub](https://github.com/openid/AppAuth-iOS).</span><span class="sxs-lookup"><span data-stu-id="aff6b-145">This sample was created by following hello README instructions by hello [iOS AppAuth project on GitHub](https://github.com/openid/AppAuth-iOS).</span></span> <span data-ttu-id="aff6b-146">Para obter mais detalhes sobre como funcionam exemplo Olá e biblioteca Olá, referência Olá Leia-me de AppAuth no GitHub.</span><span class="sxs-lookup"><span data-stu-id="aff6b-146">For more details on how hello sample and hello library work, reference hello AppAuth README on GitHub.</span></span>

## <a name="modifying-your-app-toouse-azure-ad-b2c-with-appauth"></a><span data-ttu-id="aff6b-147">Modificar o toouse de aplicação do Azure AD B2C com AppAuth</span><span class="sxs-lookup"><span data-stu-id="aff6b-147">Modifying your app toouse Azure AD B2C with AppAuth</span></span>

> [!NOTE]
> <span data-ttu-id="aff6b-148">AppAuth suporta iOS 7 e posterior.</span><span class="sxs-lookup"><span data-stu-id="aff6b-148">AppAuth supports iOS 7 and above.</span></span>  <span data-ttu-id="aff6b-149">No entanto, os inícios de sessão de redes sociais toosupport no Google, SFSafariViewController é necessário que requer o iOS 9 ou superior.</span><span class="sxs-lookup"><span data-stu-id="aff6b-149">However, toosupport social logins on Google, SFSafariViewController is needed which requires iOS 9 or higher.</span></span>
>

### <a name="configuration"></a><span data-ttu-id="aff6b-150">Configuração</span><span class="sxs-lookup"><span data-stu-id="aff6b-150">Configuration</span></span>

<span data-ttu-id="aff6b-151">Pode configurar a comunicação com o Azure AD B2C, especificando o ponto final de autorização de Olá e o ponto final de tokens de URI.</span><span class="sxs-lookup"><span data-stu-id="aff6b-151">You can configure communication with Azure AD B2C by specifying both hello authorization endpoint and token endpoint URIs.</span></span>  <span data-ttu-id="aff6b-152">toogenerate estes URIs, terá de Olá seguintes informações:</span><span class="sxs-lookup"><span data-stu-id="aff6b-152">toogenerate these URIs, you need hello following information:</span></span>
* <span data-ttu-id="aff6b-153">ID do inquilino (por exemplo, contoso.onmicrosoft.com)</span><span class="sxs-lookup"><span data-stu-id="aff6b-153">Tenant ID (for example, contoso.onmicrosoft.com)</span></span>
* <span data-ttu-id="aff6b-154">Nome da política (por exemplo, B2C\_1\_SignUpIn)</span><span class="sxs-lookup"><span data-stu-id="aff6b-154">Policy name (for example, B2C\_1\_SignUpIn)</span></span>

<span data-ttu-id="aff6b-155">Olá ponto final de tokens URI que pode ser gerado ao substituir Olá inquilino\_ID e a política de Olá\_nome no Olá seguinte URL:</span><span class="sxs-lookup"><span data-stu-id="aff6b-155">hello token endpoint URI can be generated by replacing hello Tenant\_ID and hello Policy\_Name in hello following URL:</span></span>

```objc
static NSString *const tokenEndpoint = @"https://login.microsoftonline.com/te/<Tenant_ID>/<Policy_Name>/oauth2/v2.0/token";
```

<span data-ttu-id="aff6b-156">Olá ponto final de autorização URI que pode ser gerado ao substituir Olá inquilino\_ID e a política de Olá\_nome no Olá seguinte URL:</span><span class="sxs-lookup"><span data-stu-id="aff6b-156">hello authorization endpoint URI can be generated by replacing hello Tenant\_ID and hello Policy\_Name in hello following URL:</span></span>

```objc
static NSString *const authorizationEndpoint = @"https://login.microsoftonline.com/te/<Tenant_ID>/<Policy_Name>/oauth2/v2.0/authorize";
```

<span data-ttu-id="aff6b-157">Execute Olá toocreate de código a seguir o objeto de AuthorizationServiceConfiguration:</span><span class="sxs-lookup"><span data-stu-id="aff6b-157">Run hello following code toocreate your AuthorizationServiceConfiguration object:</span></span>

```objc
OIDServiceConfiguration *configuration = 
    [[OIDServiceConfiguration alloc] initWithAuthorizationEndpoint:authorizationEndpoint tokenEndpoint:tokenEndpoint];
// now we are ready tooperform hello auth request...
```

### <a name="authorizing"></a><span data-ttu-id="aff6b-158">Autorizar</span><span class="sxs-lookup"><span data-stu-id="aff6b-158">Authorizing</span></span>

<span data-ttu-id="aff6b-159">Depois de configurar ou obtenção de uma configuração de serviço de autorização, pode ser construído a um pedido de autorização.</span><span class="sxs-lookup"><span data-stu-id="aff6b-159">After configuring or retrieving an authorization service configuration, an authorization request can be constructed.</span></span> <span data-ttu-id="aff6b-160">pedir toocreate Olá, terá de Olá seguintes informações:</span><span class="sxs-lookup"><span data-stu-id="aff6b-160">toocreate hello request, you need hello following information:</span></span>  
* <span data-ttu-id="aff6b-161">ID de cliente (por exemplo, 00000000-0000-0000-0000-000000000000)</span><span class="sxs-lookup"><span data-stu-id="aff6b-161">Client ID (for example, 00000000-0000-0000-0000-000000000000)</span></span>
* <span data-ttu-id="aff6b-162">URI de redirecionamento com um esquema personalizado (por exemplo, com.onmicrosoft.fabrikamb2c.exampleapp://oauth/redirect)</span><span class="sxs-lookup"><span data-stu-id="aff6b-162">Redirect URI with a custom scheme (for example, com.onmicrosoft.fabrikamb2c.exampleapp://oauth/redirect)</span></span>

<span data-ttu-id="aff6b-163">Ambos os itens devem ter sido guardados quando era [registar a sua aplicação](#create-an-application).</span><span class="sxs-lookup"><span data-stu-id="aff6b-163">Both items should have been saved when you were [registering your app](#create-an-application).</span></span>

```objc
OIDAuthorizationRequest *request = 
    [[OIDAuthorizationRequest alloc] initWithConfiguration:configuration
                                                  clientId:kClientId
                                                    scopes:@[OIDScopeOpenID, OIDScopeProfile]
                                               redirectURL:[NSURL URLWithString:kRedirectUri]
                                              responseType:OIDResponseTypeCode
                                      additionalParameters:nil];

AppDelegate *appDelegate = (AppDelegate *)[UIApplication sharedApplication].delegate;
appDelegate.currentAuthorizationFlow = 
    [OIDAuthState authStateByPresentingAuthorizationRequest:request
                                   presentingViewController:self
                                                   callback:^(OIDAuthState *_Nullable authState, NSError *_Nullable error) {
        if (authState) {
            NSLog(@"Got authorization tokens. Access token: %@", authState.lastTokenResponse.accessToken);
            [self setAuthState:authState];
        } else {
            NSLog(@"Authorization error: %@", [error localizedDescription]);
            [self setAuthState:nil];
        }
    }];
```

<span data-ttu-id="aff6b-164">tooset se a sua aplicação toohandle Olá redirecionamento toohello URI com o esquema personalizado Olá, terá de lista de Olá tooupdate de esquemas de URL no seu ficheiro info. plist:</span><span class="sxs-lookup"><span data-stu-id="aff6b-164">tooset up your application toohandle hello redirect toohello URI with hello custom scheme, you need tooupdate hello list of 'URL Schemes' in your Info.pList:</span></span>
* <span data-ttu-id="aff6b-165">Abra o ficheiro info. plist.</span><span class="sxs-lookup"><span data-stu-id="aff6b-165">Open Info.pList.</span></span>
* <span data-ttu-id="aff6b-166">Coloque o cursor sobre uma linha, como 'Código de tipo de SO do pacote' e clique em Olá \+ símbolo.</span><span class="sxs-lookup"><span data-stu-id="aff6b-166">Hover over a row like 'Bundle OS Type Code' and click hello \+ symbol.</span></span>
* <span data-ttu-id="aff6b-167">Mudar o nome Olá nova linha 'URL types'.</span><span class="sxs-lookup"><span data-stu-id="aff6b-167">Rename hello new row 'URL types'.</span></span>
* <span data-ttu-id="aff6b-168">Clique em esquerda toohello de seta de Olá da árvore de Olá de tooopen 'URL types'.</span><span class="sxs-lookup"><span data-stu-id="aff6b-168">Click hello arrow toohello left of 'URL types' tooopen hello tree.</span></span>
* <span data-ttu-id="aff6b-169">Clique em esquerda toohello de seta de Olá da árvore de Olá tooopen 'Item 0'.</span><span class="sxs-lookup"><span data-stu-id="aff6b-169">Click hello arrow toohello left of 'Item 0' tooopen hello tree.</span></span>
* <span data-ttu-id="aff6b-170">Mudar o nome do primeiro item por baixo dos Item 0 too'URL os esquemas.</span><span class="sxs-lookup"><span data-stu-id="aff6b-170">Rename first item underneath Item 0 too'URL Schemes'.</span></span>
* <span data-ttu-id="aff6b-171">Clique em esquerda toohello de seta de Olá da árvore de Olá tooopen de esquemas de URL.</span><span class="sxs-lookup"><span data-stu-id="aff6b-171">Click hello arrow toohello left of 'URL Schemes' tooopen hello tree.</span></span>
* <span data-ttu-id="aff6b-172">Na coluna de 'Value' Olá, há uma esquerda de toohello campo em branco de 'Item 0"por baixo de esquemas de URL.</span><span class="sxs-lookup"><span data-stu-id="aff6b-172">In hello 'Value' column, there is a blank field toohello left of 'Item 0' underneath 'URL Schemes'.</span></span>  <span data-ttu-id="aff6b-173">Defina o esquema exclusivo da aplicação de Olá, valor tooyour.</span><span class="sxs-lookup"><span data-stu-id="aff6b-173">Set hello value tooyour application's unique scheme.</span></span>  <span data-ttu-id="aff6b-174">valor de Olá tem de corresponder ao esquema de Olá utilizado no redirectURL ao criar objeto de OIDAuthorizationRequest Olá.</span><span class="sxs-lookup"><span data-stu-id="aff6b-174">hello value must match hello scheme used in redirectURL when creating hello OIDAuthorizationRequest object.</span></span>  <span data-ttu-id="aff6b-175">No nosso exemplo, utilizámos o esquema de Olá 'com.onmicrosoft.fabrikamb2c.exampleapp'.</span><span class="sxs-lookup"><span data-stu-id="aff6b-175">In our sample, we used hello scheme 'com.onmicrosoft.fabrikamb2c.exampleapp'.</span></span>

<span data-ttu-id="aff6b-176">Consulte toohello [AppAuth guia](https://openid.github.io/AppAuth-iOS/) no como toocomplete Olá rest do processo de Olá.</span><span class="sxs-lookup"><span data-stu-id="aff6b-176">Refer toohello [AppAuth guide](https://openid.github.io/AppAuth-iOS/) on how toocomplete hello rest of hello process.</span></span> <span data-ttu-id="aff6b-177">Se precisar de tooquickly começar com uma aplicação de trabalho, consulte [nosso exemplo](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c).</span><span class="sxs-lookup"><span data-stu-id="aff6b-177">If you need tooquickly get started with a working app, check out [our sample](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c).</span></span> <span data-ttu-id="aff6b-178">Siga os passos de Olá Olá [README.md](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c/blob/master/README.md) tooenter a própria configuração do Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="aff6b-178">Follow hello steps in hello [README.md](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c/blob/master/README.md) tooenter your own Azure AD B2C configuration.</span></span>

<span data-ttu-id="aff6b-179">Estamos sempre toofeedback aberta e sugestões!</span><span class="sxs-lookup"><span data-stu-id="aff6b-179">We are always open toofeedback and suggestions!</span></span> <span data-ttu-id="aff6b-180">Se tiver dificuldades em causa com este tópico ou tiver recomendações para melhorar este conteúdo, Agradecemos os seus comentários na Olá parte inferior da página Olá.</span><span class="sxs-lookup"><span data-stu-id="aff6b-180">If you have any difficulties with this topic, or have recommendations for improving this content, we would appreciate your feedback at hello bottom of hello page.</span></span> <span data-ttu-id="aff6b-181">Para pedidos de funcionalidades, adicioná-los demasiado[UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c).</span><span class="sxs-lookup"><span data-stu-id="aff6b-181">For feature requests, add them too[UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c).</span></span>
