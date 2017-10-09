---
title: "O Azure Active Directory B2C: Adicionar ADFS como um fornecedor de identidade através de políticas personalizadas"
description: "Um tooarticle como sobre como configurar 2016 do AD FS utilizando o protocolo SAML e as políticas personalizadas"
services: active-directory-b2c
documentationcenter: 
author: yoelhor
manager: joroja
editor: 
ms.assetid: 
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 08/04/2017
ms.author: yoelh
ms.openlocfilehash: 30fb7700e7834e3d91fab1fc1b169b761584b204
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-add-adfs-as-a-saml-identity-provider-using-custom-policies"></a>O Azure Active Directory B2C: Adicionar ADFS como um fornecedor de identidade através de políticas personalizadas

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

Este artigo mostra como tooenable início de sessão para os utilizadores da conta do AD FS através da utilização de Olá de [políticas personalizadas](active-directory-b2c-overview-custom.md).

## <a name="prerequisites"></a>Pré-requisitos

Olá concluir os passos em Olá [introdução às políticas personalizadas](active-directory-b2c-get-started-custom.md) artigo.

Estes passos incluem:

1.  Criar uma confiança de entidade Confiadora de ADFS.
2.  Adicionar Olá ADFS confiança de entidade Confiadora certificado tooAzure AD B2C.
3.  A adicionar a política de tooa do fornecedor de afirmações.
4.  Conta ADFS Olá registar journey de utilizador de tooa do fornecedor de afirmações.
5.  Carregamento Olá tooan de política do Azure AD B2C inquilino e testá-lo.

## <a name="toocreate-a-claims-aware-relying-party-trust"></a>toocreate uma confiança da entidade Confiadora com suporte para afirmações

toouse ADFS como um fornecedor de identidade no Azure Active Directory (Azure AD) B2C, tem de toocreate um ADFS confiança da entidade Confiadora e fornecer com parâmetros corretos Olá.

tooadd uma nova entidade confiadora confiar utilizando Olá AD FS snap-in de gestão e configurar manualmente as definições de Olá, efetuar Olá segue o procedimento num servidor de Federação.

A associação **administradores**, ou equivalente, no computador local Olá toocomplete necessários mínimos de Olá este procedimento. Reveja os detalhes sobre como utilizar contas apropriadas Olá e associações a grupos em [locais e grupos predefinidos do domínio](http://go.microsoft.com/fwlink/?LinkId=83477)

1.  No Gestor de servidor, clique em **ferramentas**e, em seguida, selecione **ADFS gestão**.

2.  Clique em **adicionar confiança da entidade Confiadora**.
    ![Adicionar confiança da entidade Confiadora](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-1.png)

3.  No Olá **boas-vindas** página, escolha **com suporte para afirmações** e clique em **iniciar**.
    ![Na página de boas-vindas Olá, escolha com suporte para afirmações](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-2.png)
4.  No Olá **selecionar origem de dados** página, clique em **introduzir dados sobre a entidade confiadora Olá manualmente**e, em seguida, clique em **seguinte**.
    ![Introduzir dados sobre a entidade confiadora Olá](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-3.png)

5.  No Olá **Especificar nome a apresentar** , escreva um nome na **nome a apresentar**, em **notas** escreva uma descrição para esta confiança da entidade confiadora e, em seguida, clique em **seguinte** .
    ![Especifique o nome a apresentar e notas](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-4.png)
6.  Opcional. Se tiver um certificado de encriptação de tokens opcional, em seguida, no Olá **configurar certificado** página, clique em **procurar** toolocate o ficheiro de certificado e, em seguida, clique em **seguinte** .
    ![Configurar o certificado](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-5.png)
7.  No Olá **configurar URL** página, selecione de Olá **ativar o suporte para protocolo SAML 2.0 WebSSO de Olá** caixa de verificação. Em **URL de serviço SAML 2.0 SSO da entidade Confiadora**, escreva o URL do ponto final de serviço do Olá Security Assertion Markup Language (SAML) para esta confiança da entidade confiadora e, em seguida, clique em **seguinte**.  Para Olá **URL de serviço SAML 2.0 SSO da entidade Confiadora**, cole Olá `https://login.microsoftonline.com/te/{tenant}.onmicrosoft.com/{policy}`. Substitua {inquilino} com o nome do seu inquilino (por exemplo, contosob2c.onmicrosoft.com) e substitua Olá {política} com o nome da política extensões (por exemplo, B2C_1A_TrustFrameworkExtensions).
    > [!IMPORTANT]
    >nome da política Olá é Olá uma política de signup_or_signin herda, neste caso é: `B2C_1A_TrustFrameworkExtensions`.
    >Por exemplo Olá URL pode ser: https://login.microsoftonline.com/te/**contosob2c**.onmicrosoft.com/**B2C_1A_TrustFrameworkBase**.

    ![URL do serviço SAML 2.0 SSO de entidade confiadora](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-6.png)
8. No Olá **configurar identificadores** página, especifique Olá mesmo URL que o passo anterior Olá, clique em **adicionar** tooadd-los toohello lista e, em seguida, clique em **seguinte**.
    ![Entidade confiadora identificadores de confiança de entidade](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-7.png)
9.  No Olá **escolha política de controlo de acesso** selecionar uma política e clique em **seguinte**.
    ![Escolha a política de controlo de acesso](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-8.png)
10.  No Olá **pronto tooAdd confiança** página, reveja as definições de Olá e, em seguida, clique em **seguinte** toosave informações sobre a confiança da entidade confiadora.
    ![Guardar as informações de confiança de entidade entidade confiadora](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-9.png)
11.  No Olá **concluir** página, clique em **fechar**, esta ação apresenta automaticamente Olá **editar regras de afirmação** caixa de diálogo.
    ![Editar regras de afirmação](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-10.png)
12. Clique em **Adicionar regra**.  
      ![Adicionar nova regra](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-claims-1.png)
13.  No **modelo de regra de afirmação**, selecione **enviar atributos LDAP como afirmações**.
    ![Selecione enviar atributos LDAP como regra de modelo de afirmações](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-claims-2.png)
14.  Fornecer **nome da regra de afirmação**. Para Olá **arquivo de atributos** selecione **selecione Active Directory** adicionar Olá seguintes afirmações, em seguida, clique em **concluir** e **OK**.
    ![Defina as propriedades de regra](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-claims-3.png)
15.  No Gestor de servidor, selecione **confianças da entidade Confiadora** , em seguida, selecione a confiança da entidade confiadora Olá que criou e clique em **propriedades**.
    ![Entidade confiadora propriedades de edição de terceiros](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-sig-1.png)
16.  Olá uma entidade confiadora clique de janela de propriedades a confiança (B2C demonstração) de terceiros **assinatura** separador e clique em **adicionar**.  
    ![Assinatura de conjunto](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-sig-2.png)
17.  Adicione o certificado de assinatura (ficheiro .cert, sem chave privada).  
    ![Adicionar o certificado de assinatura](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-sig-3.png)
18.  Na janela de propriedades de fidedignidade (B2C demonstração) Olá entidade confiadora terceiros clique **avançadas** separador e alterar Olá **o algoritmo hash seguro** demasiado**SHA-1**, clique em **Ok**.  
    ![Definir o algoritmo de hash seguro tooSHA-1](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-sig-4.png)

## <a name="add-hello-adfs-account-application-key-tooazure-ad-b2c"></a>Adicionar Olá ADFS conta aplicação chave tooAzure AD B2C
A Federação com contas ADFS requer um segredo do cliente de AD FS tootrust de conta do Azure AD B2C em nome da aplicação Olá. É necessário toostore o certificado do AD FS no seu inquilino do Azure AD B2C. 

1.  Aceda inquilino tooyour do Azure AD B2C e selecione **definições do B2C** > **Framework de experiência de identidade**
2.  Selecione **política chaves** tooview Olá as chaves disponíveis no seu inquilino.
3.  Clique em **+ adicionar**.
4.  Para **opções**, utilize **carregar**.
5.  Para **nome**, utilize `ADFSSamlCert`.  
    prefixo de Olá `B2C_1A_` podem ser adicionados automaticamente.
6.  No carregamento do ficheiro Olá, * * selecionar o ficheiro de. pfx do certificado com chave privada. Nota: este certificado (com a chave privada de Olá) deve ser Olá mesmo mais emitido e utilizado para Olá ADFS entidade confiadora.
![Carregar política chave](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-cert.png)
7.  Clique em **Criar**.
8.  Confirme que criou a chave de Olá `B2C_1A_ADFSSamlCert`.

## <a name="add-a-claims-provider-in-your-extension-policy"></a>Adicionar um fornecedor de afirmações na política de extensão
Se pretender que os utilizadores toosign utilizando a conta do AD FS, precisa de toodefine ADFS conta como um fornecedor de afirmações. Por outras palavras, terá de toospecify um ponto final que o Azure AD B2C comunica com. ponto final de Olá fornece um conjunto de afirmações que são utilizados pelo Azure AD B2C tooverify que foi autenticado um utilizador específico.

Definir o ADFS como um fornecedor de afirmações, adicionando `<ClaimsProvider>` nó no seu ficheiro de política de extensão:

1. Abra o ficheiro de política de extensão de Olá (TrustFrameworkExtensions.xml) do diretório de trabalho. Se precisar de um editor de XML, [tente Visual Studio Code](https://code.visualstudio.com/download), um editor de plataforma simples.
2. Determinar Olá `<ClaimsProviders>` secção
3. Adicionar Olá seguinte fragmento XML em Olá `ClaimsProviders` elemento e substitua `identityProvider` com o seu DNS (valor arbitrário que indica o seu domínio) e guarde-Olá. 

```xml
<ClaimsProvider>
    <Domain>contoso.com</Domain>
    <DisplayName>Contoso ADFS</DisplayName>
    <TechnicalProfiles>
    <TechnicalProfile Id="Contoso-SAML2">
        <DisplayName>Contoso ADFS</DisplayName>
        <Description>Login with your Contoso account</Description>
        <Protocol Name="SAML2"/>
        <Metadata>
        <Item Key="RequestsSigned">false</Item>
        <Item Key="WantsEncryptedAssertions">false</Item>
        <Item Key="PartnerEntity">https://{your_ADFS_domain}/federationmetadata/2007-06/federationmetadata.xml</Item>
        </Metadata>
        <CryptographicKeys>
        <Key Id="SamlAssertionSigning" StorageReferenceId="B2C_1A_ADFSSamlCert"/>
        <Key Id="SamlMessageSigning" StorageReferenceId="B2C_1A_ADFSSamlCert"/>
        </CryptographicKeys>
        <OutputClaims>
        <OutputClaim ClaimTypeReferenceId="socialIdpUserId" PartnerClaimType="userPrincipalName" />
        <OutputClaim ClaimTypeReferenceId="givenName" PartnerClaimType="given_name"/>
        <OutputClaim ClaimTypeReferenceId="surname" PartnerClaimType="family_name"/>
        <OutputClaim ClaimTypeReferenceId="email" PartnerClaimType="email"/>
        <OutputClaim ClaimTypeReferenceId="displayName" PartnerClaimType="name"/>
        <OutputClaim ClaimTypeReferenceId="identityProvider" DefaultValue="contoso.com" />
        <OutputClaim ClaimTypeReferenceId="authenticationSource" DefaultValue="socialIdpAuthentication"/>
        </OutputClaims>
        <OutputClaimsTransformations>
        <OutputClaimsTransformation ReferenceId="CreateRandomUPNUserName"/>
        <OutputClaimsTransformation ReferenceId="CreateUserPrincipalName"/>
        <OutputClaimsTransformation ReferenceId="CreateAlternativeSecurityId"/>
        <OutputClaimsTransformation ReferenceId="CreateSubjectClaimFromAlternativeSecurityId"/>
        </OutputClaimsTransformations>
        <UseTechnicalProfileForSessionManagement ReferenceId="SM-Noop"/>
    </TechnicalProfile>
    </TechnicalProfiles>
</ClaimsProvider>
```

## <a name="register-hello-adfs-account-claims-provider-toosign-up-or-sign-in-user-journey"></a>Registar tooSign de fornecedor de afirmações do Olá ADFS conta se ou iniciar sessão no journey de utilizador
Neste momento, o fornecedor de identidade Olá foi configurado.  No entanto, não está disponível em nenhum dos Olá sessão-up/início de sessão ecrãs. Agora tem tooadd Olá ADFS identidade fornecedor tooyour utilizador da conta `SignUpOrSignIn` journey de utilizador. toomake-la disponível, criamos um duplicado de um existente journey de utilizador do modelo.  Em seguida, iremos modificá-lo para que inclui o fornecedor de identidade do ADFS Olá:
    >[!NOTE]
    >If you previously copied hello `<UserJourneys>` element from base file of your policy toohello extension file (TrustFrameworkExtensions.xml) you can skip this section.
1.  Abra o ficheiro de base de Olá da sua política (por exemplo, TrustFrameworkBase.xml).
2.  Determinar Olá `<UserJourneys>` elemento e cópia Olá todo o conteúdo de `<UserJourneys>` nós.
3.  Abra o ficheiro de extensão de Olá (por exemplo, TrustFrameworkExtensions.xml) e determinar Olá `<UserJourneys>` elemento. Se não existir elemento Olá, adicione um.
4.  Colar o conteúdo completo de Olá de `<UserJournesy>` nó que copiou como subordinado de Olá `<UserJourneys>` elemento.

### <a name="display-hello-button"></a>Botão de Olá de apresentação
Olá `<ClaimsProviderSelections>` elemento define lista Olá das opções de seleção de fornecedor de afirmações e a sua ordem.  `<ClaimsProviderSelection>`elemento está no botão do fornecedor de identidade tooan semelhante numa página sessão-up/início de sessão. Se adicionar um `<ClaimsProviderSelection>` elemento para a conta do AD FS, um novo botão aparece quando um utilizador lands na página Olá. tooadd este elemento:

1.  Determinar Olá `<UserJourney>` nó que inclui `Id="SignUpOrSignIn"` no journey de utilizador de Olá que copiou.
2.  Localizar Olá `<OrchestrationStep>` nó que inclui`Order="1"`
3.  Adicione o seguinte fragmento XML em `<ClaimsProviderSelections>` nó:

```xml
<ClaimsProviderSelection TargetClaimsExchangeId="ContosoExchange" />
```
### <a name="link-hello-button-tooan-action"></a>Ligação Olá botão tooan ação

Agora que tem um botão no local, terá de toolink-tooan ação. Olá, neste caso, é ação para o Azure AD B2C toocommunicate com ADFS conta tooreceive um token. Ligação Olá botão tooan ação associando perfil técnica Olá para o fornecedor de afirmações do ADFS conta:

1.  Determinar Olá `<OrchestrationStep>` que inclua `Order="2"` no Olá `<UserJourney>` nós.
2.  Adicione o seguinte fragmento XML em `<ClaimsExchanges>` nó:

```xml
<ClaimsExchange Id="ContosoExchange" TechnicalProfileReferenceId="Contoso-SAML2" />
```

> [!NOTE]
> * Certifique-se Olá `Id` tem Olá mesmo valor da `TargetClaimsExchangeId` no Olá anterior a secção.
> * Certifique-se `TechnicalProfileReferenceId` é definir perfil técnica toohello que criou anteriormente (Contoso-SAML2).

## <a name="upload-hello-policy-tooyour-tenant"></a>Carregar o inquilino de tooyour Olá política
1.  No Olá [portal do Azure](https://portal.azure.com), mudar para Olá [contexto do seu inquilino do Azure AD B2C](active-directory-b2c-navigate-to-b2c-context.md)e abra Olá **do Azure AD B2C** painel.
2.  Selecione **identidade experiência Framework**.
3.  Abra Olá **todas as políticas** painel.
4.  Selecione **carregar política**.
5.  Verifique **substituir a política de Olá, se existir** caixa.
6.  **Carregar** TrustFrameworkExtensions.xml e certifique-se de que não falha a validação de Olá

## <a name="test-hello-custom-policy-by-using-run-now"></a>Testar a política personalizada do Olá utilizando o executar agora
1.  Abra **definições do Azure AD B2C** e aceda demasiado**identidade experiência Framework**.
2.  Abra **B2C_1A_signup_signin**, Olá entidade confiadora política personalizada de terceiros (RP) que carregou. Selecione **executar agora**.
3.  Deve ser capaz de toosign sessão com a conta ADFS.

## <a name="optional-register-hello-adfs-account-claims-provider-tooprofile-edit-user-journey"></a>[Opcional] Registar journey de utilizador ao editar tooProfile do fornecedor de afirmações Olá ADFS conta
Poderá ser útil fornecedor de identidade de conta ADFS Olá tooadd também tooyour utilizador `ProfileEdit` journey de utilizador. toomake-la disponível, iremos repetir Olá últimos dois passos:

### <a name="display-hello-button"></a>Botão de Olá de apresentação
1.  Abra o ficheiro de extensão de Olá da sua política (por exemplo, TrustFrameworkExtensions.xml).
2.  Determinar Olá `<UserJourney>` nó que inclui `Id="ProfileEdit"` no journey de utilizador de Olá que copiou.
3.  Localizar Olá `<OrchestrationStep>` nó que inclui`Order="1"`
4.  Adicione o seguinte fragmento XML em `<ClaimsProviderSelections>` nó:

```xml
<ClaimsProviderSelection TargetClaimsExchangeId="ContosoExchange" />
```

### <a name="link-hello-button-tooan-action"></a>Ligação Olá botão tooan ação
1.  Determinar Olá `<OrchestrationStep>` que inclua `Order="2"` no Olá `<UserJourney>` nós.
2.  Adicione o seguinte fragmento XML em `<ClaimsExchanges>` nó:

```xml
<ClaimsExchange Id="ContosoExchange" TechnicalProfileReferenceId="Contoso-SAML2" />
```

### <a name="test-hello-custom-profile-edit-policy-by-using-run-now"></a>Testar a política de edição de perfil personalizada do Olá utilizando o executar agora
1.  Abra **definições do Azure AD B2C** e aceda demasiado**identidade experiência Framework**.
2.  Abra **B2C_1A_ProfileEdit**, Olá entidade confiadora política personalizada de terceiros (RP) que carregou. Selecione **executar agora**.
3.  Deve ser capaz de toosign sessão com a conta ADFS.

## <a name="download-hello-complete-policy-files"></a>Transferir ficheiros de política concluída Olá
Opcional: Recomendamos que crie o seu cenário de utilizar os seus próprios ficheiros de política personalizada depois de concluir Olá introdução com as políticas personalizadas guiá. [Ficheiros de política de exemplo para referência apenas](https://github.com/Azure-Samples/active-directory-b2c-custom-policy-starterpack/tree/master/scenarios/aadb2c-ief-setup-adfs2016-app)
