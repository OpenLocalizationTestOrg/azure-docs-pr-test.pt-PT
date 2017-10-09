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
# <a name="azure-ad-b2c-sign-in-using-an-android-application"></a>O Azure AD B2C: Início de sessão utilizando uma aplicação Android

plataforma de identidade do Microsoft Olá utiliza as normas de abertura, como o OAuth2 e o OpenID Connect. Isto permite aos programadores tooleverage qualquer biblioteca que pretendam toointegrate aos nossos serviços. os programadores de tooaid utilizando a nossa plataforma com outras bibliotecas, escrevemos algumas instruções como esta um toodemonstrate como tooconfigure 3rd terceiros bibliotecas tooconnect toohello Microsoft plataforma de identidade. A maioria das bibliotecas que implementam [spec Olá especificação RFC6749 OAuth2](https://tools.ietf.org/html/rfc6749) será plataforma do tooconnect capaz de toohello Microsoft Identity.

> [!WARNING]
> A Microsoft não cede correções para 3rd bibliotecas de terceiros e não tiverem efetuado uma revisão desses bibliotecas. Este exemplo está a utilizar uma biblioteca de terceiros 3rd chamada AppAuth foi testado para compatibilidade em cenários básicos com Olá, Azure AD B2C. Problemas e pedidos de funcionalidades devem ser o projeto de fonte aberta da biblioteca de toohello direcionados. Consulte [neste artigo](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-libraries) para obter mais informações.  
>
>

Se tiver tooOAuth2 novo ou o OpenID Connect muito este exemplo de configuração poderá não fazer muito sentido tooyou. Recomendamos que leia a breve [descrição geral do protocolo de Olá aqui documentado](active-directory-b2c-reference-protocols.md).

## <a name="get-an-azure-ad-b2c-directory"></a>Obter um diretório do Azure AD B2C

Para poder utilizar o Azure AD B2C, tem de criar um diretório ou inquilino. Um diretório é um contentor para todos os seus utilizadores, aplicações, grupos, etc. Se ainda não tiver um, [crie um diretório do B2C](active-directory-b2c-get-started.md) antes de continuar.

## <a name="create-an-application"></a>Criar uma aplicação

Em seguida, terá de toocreate uma aplicação no diretório do B2C. Isto dá-informações do Azure AD que necessita de toocommunicate em segurança com a sua aplicação. toocreate uma aplicação móvel, siga [estas instruções](active-directory-b2c-app-registration.md). É necessário:

* Incluir um **Native Client** na aplicação Olá.
* Olá cópia **ID da aplicação** que é atribuído tooyour aplicação. Irá precisar deste mais tarde.
* Configurar um cliente nativo **URI de redirecionamento** (por exemplo, com.onmicrosoft.fabrikamb2c.exampleapp://oauth/redirect). Também irá precisar deste mais tarde.

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a>Criar as políticas

No Azure AD B2C, cada experiência de utilizador é definida por uma [política](active-directory-b2c-reference-policies.md). Esta aplicação contém uma experiência de identidade: um combinado início de sessão e inscrição. Terá de toocreate desta política, conforme descrito no [artigo de referência de política](active-directory-b2c-reference-policies.md#create-a-sign-up-policy). Quando criar política Olá, não se esqueça de:

* Escolha Olá **nome a apresentar** como um atributo na política de inscrição.
* Escolha Olá **nome a apresentar** e **ID de objeto** afirmações de aplicação em cada política. Também pode escolher outras afirmações.
* Olá cópia **nome** de cada política depois de a criar. Deve ter o prefixo de Olá `b2c_1_`.  Terá de nome da política hello mais tarde.

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

Depois de criar as políticas, está pronto toobuild a aplicação.

## <a name="download-hello-sample-code"></a>Transferir o código de exemplo de Olá

Fornecemos um exemplo de trabalho que utiliza AppAuth com o Azure AD B2C [no GitHub](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c). Pode transferir Olá código e executá-la. Pode rapidamente começar a utilizar com a sua própria aplicação utilizando a sua própria configuração do Azure AD B2C ao seguir as instruções de Olá Olá [README.md](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c/blob/master/README.md).

exemplo de Olá é uma modificação de exemplo de Olá fornecida pelo [AppAuth](https://openid.github.io/AppAuth-Android/). Visite os respetivos toolearn página mais informações sobre AppAuth e as respetivas funcionalidades.

## <a name="modifying-your-app-toouse-azure-ad-b2c-with-appauth"></a>Modificar o toouse de aplicação do Azure AD B2C com AppAuth

> [!NOTE]
> AppAuth suporta Android API 16 (Jellybean) e superior. Recomendamos que utilize a API 23 e superior.
>

### <a name="configuration"></a>Configuração

Pode configurar a comunicação com o Azure AD B2C por detetar Olá especificação URI ou especificando um ponto final de autorização de Olá e o ponto final de tokens de URI. Em ambos os casos, terá de Olá seguintes informações:

* ID do inquilino (por exemplo, contoso.onmicrosoft.com)
* Nome da política (por exemplo, B2C\_1\_SignUpIn)

Se escolher tooautomatically detetar Olá autorização e tokens endpoint URIs, irá necessitar de informações de toofetch da deteção de Olá URI. Deteção de Olá URI que pode ser gerado ao substituir Olá inquilino\_ID e a política de Olá\_nome no Olá seguinte URL:

```java
String mDiscoveryURI = "https://login.microsoftonline.com/<Tenant_ID>/v2.0/.well-known/openid-configuration?p=<Policy_Name>";
```

Em seguida, pode adquirir Olá autorização e de ponto final de tokens URIs e criar um objeto de AuthorizationServiceConfiguration executando o seguinte Olá:

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

Em vez de utilizar a autorização de Olá tooobtain de deteção e o ponto final de tokens URIs, também pode especificá-los explicitamente, substituindo Olá inquilino\_ID e a política de Olá\_nome no URL de Olá abaixo:

```java
String mAuthEndpoint = "https://login.microsoftonline.com/<Tenant_ID>/oauth2/v2.0/authorize?p=<Policy_Name>";

String mTokenEndpoint = "https://login.microsoftonline.com/<Tenant_ID>/oauth2/v2.0/token?p=<Policy_Name>";
```

Execute Olá toocreate de código a seguir o objeto de AuthorizationServiceConfiguration:

```java
AuthorizationServiceConfiguration config =
        new AuthorizationServiceConfiguration(name, mAuthEndpoint, mTokenEndpoint);

// perform hello auth request...
```

### <a name="authorizing"></a>Autorizar

Depois de configurar ou obtenção de uma configuração de serviço de autorização, pode ser construído a um pedido de autorização. pedir toocreate Olá, terá de Olá seguintes informações:

* ID de cliente (por exemplo, 00000000-0000-0000-0000-000000000000)
* URI de redirecionamento com um esquema personalizado (por exemplo, com.onmicrosoft.fabrikamb2c.exampleapp://oauthredirect)

Ambos os itens devem ter sido guardados quando era [registar a sua aplicação](#create-an-application).

```java
AuthorizationRequest req = new AuthorizationRequest.Builder(
    config,
    clientId,
    ResponseTypeValues.CODE,
    redirectUri)
    .build();
```

Consulte toohello [AppAuth guia](https://openid.github.io/AppAuth-Android/) no como toocomplete Olá rest do processo de Olá. Se precisar de tooquickly começar com uma aplicação de trabalho, consulte [nosso exemplo](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c). Siga os passos de Olá Olá [README.md](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c/blob/master/README.md) tooenter a própria configuração do Azure AD B2C.

Estamos sempre toofeedback aberta e sugestões! Se tiver dificuldades em causa com este tópico ou tiver recomendações para melhorar este conteúdo, Agradecemos os seus comentários na Olá parte inferior da página Olá. Para pedidos de funcionalidades, adicioná-los demasiado[UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c).

