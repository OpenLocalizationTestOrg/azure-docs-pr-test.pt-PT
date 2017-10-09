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
# <a name="azure-ad-b2c-sign-in-using-an-ios-application"></a>O Azure AD B2C: Início de sessão utilizando uma aplicação iOS

plataforma de identidade do Microsoft Olá utiliza as normas de abertura, como o OAuth2 e o OpenID Connect. Utilizar um protocolo padrão aberto oferece mais opções de programador quando selecionar um toointegrate biblioteca aos nossos serviços. Fornecemos esta explicação passo a passo e outros, como se tooaid programadores com aplicações que ligam a plataforma do Microsoft Identity de toohello escrita. A maioria das bibliotecas que implementam [spec Olá especificação RFC6749 OAuth2](https://tools.ietf.org/html/rfc6749) são plataforma do tooconnect capaz de toohello Microsoft Identity.

> [!WARNING]
> A Microsoft não cede corrige para bibliotecas de terceiros e não tiver efetuado uma revisão desses bibliotecas. Este exemplo está a utilizar uma biblioteca de terceiros chamada AppAuth foi testado para compatibilidade em cenários básicos com Olá, Azure AD B2C. Problemas e pedidos de funcionalidades devem ser o projeto de fonte aberta da biblioteca de toohello direcionados. Para obter mais informações, consulte [este artigo](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-libraries).
>
>

Se tiver tooOAuth2 novo ou o OpenID Connect, muito este exemplo de configuração poderá não fazer muito sentido tooyou. Recomendamos que leia a breve [descrição geral do protocolo de Olá aqui documentado](active-directory-b2c-reference-protocols.md).

## <a name="get-an-azure-ad-b2c-directory"></a>Obter um diretório do Azure AD B2C
Para poder utilizar o Azure AD B2C, tem de criar um diretório ou inquilino. Um diretório é um contentor para todos os seus utilizadores, aplicações, grupos e muito mais. Se ainda não tiver um, [crie um diretório do B2C](active-directory-b2c-get-started.md) antes de continuar.

## <a name="create-an-application"></a>Criar uma aplicação
Em seguida, terá de toocreate uma aplicação no diretório do B2C. registo de aplicação Olá dá-informações do Azure AD que necessita de toocommunicate em segurança com a sua aplicação. toocreate uma aplicação móvel, siga [estas instruções](active-directory-b2c-app-registration.md). É necessário:

* Incluir um **cliente nativo** na aplicação Olá.
* Olá cópia **ID da aplicação** que é atribuído tooyour aplicação. Este GUID é necessário mais tarde.
* Configurar um **URI de redirecionamento** com um esquema personalizado (por exemplo, com.onmicrosoft.fabrikamb2c.exampleapp://oauth/redirect). É necessário este URI mais tarde.

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a>Criar as políticas
No Azure AD B2C, cada experiência de utilizador é definida por uma [política](active-directory-b2c-reference-policies.md). Esta aplicação contém uma experiência de identidade: um combinado início de sessão e inscrição. Crie esta política, conforme descrito no [artigo de referência de política](active-directory-b2c-reference-policies.md#create-a-sign-up-policy). Quando criar política Olá, não se esqueça de:

* Em **atributos de inscrição**, selecione o atributo de Olá **nome a apresentar**.  Pode selecionar, bem como outros atributos.
* Em **afirmações de aplicação**, selecionar Olá afirmações **nome a apresentar** e **ID de objeto do utilizador**. Pode selecionar outras afirmações.
* Olá cópia **nome** de cada política depois de a criar. O nome da sua política é o prefixo `b2c_1_` quando guardar política Olá.  É necessário o nome da política Olá mais tarde.

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

Depois de criar as políticas, está pronto toobuild a aplicação.

## <a name="download-hello-sample-code"></a>Transferir o código de exemplo de Olá
Fornecemos um exemplo de trabalho que utiliza AppAuth com o Azure AD B2C [no GitHub](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c). Pode transferir Olá código e executá-la. toouse inquilino a sua própria do Azure AD B2C, siga as instruções de Olá Olá [README.md](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c/blob/master/README.md).

Este exemplo foi criado ao seguir as instruções de Leia-me Olá por Olá [projeto iOS AppAuth no GitHub](https://github.com/openid/AppAuth-iOS). Para obter mais detalhes sobre como funcionam exemplo Olá e biblioteca Olá, referência Olá Leia-me de AppAuth no GitHub.

## <a name="modifying-your-app-toouse-azure-ad-b2c-with-appauth"></a>Modificar o toouse de aplicação do Azure AD B2C com AppAuth

> [!NOTE]
> AppAuth suporta iOS 7 e posterior.  No entanto, os inícios de sessão de redes sociais toosupport no Google, SFSafariViewController é necessário que requer o iOS 9 ou superior.
>

### <a name="configuration"></a>Configuração

Pode configurar a comunicação com o Azure AD B2C, especificando o ponto final de autorização de Olá e o ponto final de tokens de URI.  toogenerate estes URIs, terá de Olá seguintes informações:
* ID do inquilino (por exemplo, contoso.onmicrosoft.com)
* Nome da política (por exemplo, B2C\_1\_SignUpIn)

Olá ponto final de tokens URI que pode ser gerado ao substituir Olá inquilino\_ID e a política de Olá\_nome no Olá seguinte URL:

```objc
static NSString *const tokenEndpoint = @"https://login.microsoftonline.com/te/<Tenant_ID>/<Policy_Name>/oauth2/v2.0/token";
```

Olá ponto final de autorização URI que pode ser gerado ao substituir Olá inquilino\_ID e a política de Olá\_nome no Olá seguinte URL:

```objc
static NSString *const authorizationEndpoint = @"https://login.microsoftonline.com/te/<Tenant_ID>/<Policy_Name>/oauth2/v2.0/authorize";
```

Execute Olá toocreate de código a seguir o objeto de AuthorizationServiceConfiguration:

```objc
OIDServiceConfiguration *configuration = 
    [[OIDServiceConfiguration alloc] initWithAuthorizationEndpoint:authorizationEndpoint tokenEndpoint:tokenEndpoint];
// now we are ready tooperform hello auth request...
```

### <a name="authorizing"></a>Autorizar

Depois de configurar ou obtenção de uma configuração de serviço de autorização, pode ser construído a um pedido de autorização. pedir toocreate Olá, terá de Olá seguintes informações:  
* ID de cliente (por exemplo, 00000000-0000-0000-0000-000000000000)
* URI de redirecionamento com um esquema personalizado (por exemplo, com.onmicrosoft.fabrikamb2c.exampleapp://oauth/redirect)

Ambos os itens devem ter sido guardados quando era [registar a sua aplicação](#create-an-application).

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

tooset se a sua aplicação toohandle Olá redirecionamento toohello URI com o esquema personalizado Olá, terá de lista de Olá tooupdate de esquemas de URL no seu ficheiro info. plist:
* Abra o ficheiro info. plist.
* Coloque o cursor sobre uma linha, como 'Código de tipo de SO do pacote' e clique em Olá \+ símbolo.
* Mudar o nome Olá nova linha 'URL types'.
* Clique em esquerda toohello de seta de Olá da árvore de Olá de tooopen 'URL types'.
* Clique em esquerda toohello de seta de Olá da árvore de Olá tooopen 'Item 0'.
* Mudar o nome do primeiro item por baixo dos Item 0 too'URL os esquemas.
* Clique em esquerda toohello de seta de Olá da árvore de Olá tooopen de esquemas de URL.
* Na coluna de 'Value' Olá, há uma esquerda de toohello campo em branco de 'Item 0"por baixo de esquemas de URL.  Defina o esquema exclusivo da aplicação de Olá, valor tooyour.  valor de Olá tem de corresponder ao esquema de Olá utilizado no redirectURL ao criar objeto de OIDAuthorizationRequest Olá.  No nosso exemplo, utilizámos o esquema de Olá 'com.onmicrosoft.fabrikamb2c.exampleapp'.

Consulte toohello [AppAuth guia](https://openid.github.io/AppAuth-iOS/) no como toocomplete Olá rest do processo de Olá. Se precisar de tooquickly começar com uma aplicação de trabalho, consulte [nosso exemplo](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c). Siga os passos de Olá Olá [README.md](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c/blob/master/README.md) tooenter a própria configuração do Azure AD B2C.

Estamos sempre toofeedback aberta e sugestões! Se tiver dificuldades em causa com este tópico ou tiver recomendações para melhorar este conteúdo, Agradecemos os seus comentários na Olá parte inferior da página Olá. Para pedidos de funcionalidades, adicioná-los demasiado[UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c).
