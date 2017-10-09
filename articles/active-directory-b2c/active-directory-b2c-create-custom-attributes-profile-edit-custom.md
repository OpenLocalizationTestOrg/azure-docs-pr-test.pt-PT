---
title: "O Azure Active Directory B2C: Adicionar as suas políticas de toocustom atributos e utilizar no perfil editar | Microsoft Docs"
description: "Instruções sobre como utilizar as propriedades de extensão, atributos personalizados e incluindo-los na interface de utilizador Olá"
services: active-directory-b2c
documentationcenter: 
author: rojasja
manager: krassk
editor: 
ms.assetid: 
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 08/04/2017
ms.author: joroja
ms.openlocfilehash: 8cc9c6a38d7652797ba54a3e02078ac2bf4a693b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-creating-and-using-custom-attributes-in-a-custom-profile-edit-policy"></a>O Azure Active Directory B2C: Criar e utilizar atributos personalizados num perfil personalizado Editar política

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

Neste artigo, pode criar um atributo personalizado no diretório do Azure AD B2C e utiliza este novo atributo como uma afirmação personalizada no journey de utilizador de edição de perfil Olá.

## <a name="prerequisites"></a>Pré-requisitos

Olá concluir os passos no artigo Olá [introdução com as políticas personalizadas](active-directory-b2c-get-started-custom.md).

## <a name="use-custom-attributes-toocollect-information-about-your-customers-in-azure-active-directory-b2c-using-custom-policies"></a>Utilize os atributos personalizados toocollect informações sobre os seus clientes no Azure Active Directory B2C através de políticas personalizadas
Diretório do Azure Active Directory (Azure AD) B2C é fornecido com um conjunto de atributos incorporado: determinado nome, o apelido, cidade, Código Postal, userPrincipalName, etc.  Muitas vezes, precisa de toocreate os seus próprios atributos.  Por exemplo:
* Necessita de uma aplicação de cliente orientado toopersist um atributo, tais como "LoyaltyNumber."
* Um fornecedor de identidade tem um identificador exclusivo do utilizador que tem de ser guardado como "uniqueUserGUID"."
* Um journey personalizadas do utilizador tem de estado de Olá toopersist do utilizador, tais como "migrationStatus."

Com o Azure AD B2C, pode expandir o conjunto de Olá de atributos armazenados em cada conta de utilizador. Também pode ler e escrever estes atributos utilizando Olá [AD Graph API do Azure](active-directory-b2c-devquickstarts-graph-dotnet.md).

As propriedades de extensão expandem o esquema de Olá Olá de objetos de utilizador no diretório de Olá.  propriedade de extensão de termos de Olá, o atributo personalizado e afirmações personalizadas Consulte toohello a mesma coisa no contexto de Olá deste nome artigo e Olá varia consoante o contexto de Olá (aplicação, objeto, política).

As propriedades de extensão só podem ser registadas um objeto de aplicação, apesar de estes poderão conter dados para um utilizador. propriedade de Olá é aplicação toohello anexado. objeto da aplicação Olá tem de ser concedido acesso de escrita tooregister uma propriedade de extensão. 100 propriedades de extensão (em todos os tipos e todas as aplicações) podem ser escritas tooany único objeto. As propriedades de extensão são adicionados a tipo de diretório de destino toohello e torna-se imediatamente acessíveis no inquilino do diretório de Olá, Azure AD B2C.
Se for eliminada aplicação Olá, essas propriedades de extensão, juntamente com quaisquer dados contidos nos mesmos para todos os utilizadores também são removidas. Se uma propriedade de extensão é eliminada por Olá aplicação, é removido no Olá objetos de diretório de destino e Olá valores eliminados.

Propriedades da extensão existem apenas num contexto de Olá de uma aplicação registada no inquilino Olá. id de objeto Olá dessa aplicação deve ser incluído no Olá TechnicalProfile utilizá-lo.

>[!NOTE]
>diretório de Olá, Azure AD B2C, incluem normalmente uma aplicação Web com o nome `b2c-extensions-app`.  Esta aplicação é principalmente utilizada pelo políticas incorporadas do b2c Olá para afirmações personalizadas Olá criadas através de Olá portal do Azure.  É recomendado utilizar extensões de tooregister esta aplicação para as políticas personalizadas do b2c apenas para utilizadores avançados.  Instruções para isto são incluídas no Olá secção passos neste artigo.


## <a name="creating-a-new-application-toostore-hello-extension-properties"></a>Criar um novo toostore de aplicação as propriedades de extensão de Olá

1. Abra uma sessão de navegação e navegue toohello [Azure porta](https://portal.azure.com) e inicie sessão com credenciais administrativas de Olá desejar tooconfigure de diretório do B2C.
1. Clique em **do Azure Active Directory** no menu de navegação esquerdo Olá. Poderá ser necessário toofind-lo ao selecionar mais de serviços >.
1. Selecione **registos de aplicação** e clique em **novo registo de aplicação**
1. Fornece o seguinte Olá recomendado entradas:
  * Especifique um nome para a aplicação web de Olá: **WebApp-GraphAPI-DirectoryExtensions**
  * Tipo de aplicação: app/API Web
  * Início de sessão URL:https://{tenantName}.onmicrosoft.com/WebApp-GraphAPI-DirectoryExtensions
1. Selecione * * criar. É apresentada a conclusão com êxito no Olá **notificações**
1. Selecione a aplicação web de Olá recém-criado: **WebApp-GraphAPI-DirectoryExtensions**
1. Selecionadas definições: **as permissões necessárias**
1. Selecionar a API **do Active Directory do Windows**
1. Coloque uma marca de verificação nas permissões de aplicação: **leitura e escrita de dados de diretório**, e **guardar**
1. Escolha **conceder permissões** e confirme **Sim**.
1. Copie a área de transferência tooyour e guarde Olá seguintes identificadores de WebApp-GraphAPI-DirectoryExtensions > Definições > propriedades >
*  **ID da aplicação** . Exemplo:`103ee0e6-f92d-4183-b576-8c3739027780`
* **ID de objeto**. Exemplo:`80d8296a-da0a-49ee-b6ab-fd232aa45201`



## <a name="modifying-your-custom-policy-tooadd-hello-applicationobjectid"></a>Modificar o Olá tooadd de política personalizada ApplicationObjectId

```xml
    <ClaimsProviders>
        <ClaimsProvider>
              <DisplayName>Azure Active Directory</DisplayName>
            <TechnicalProfile Id="AAD-Common">
              <DisplayName>Azure Active Directory</DisplayName>
              <Protocol Name="Proprietary" Handler="Web.TPEngine.Providers.AzureActiveDirectoryProvider, Web.TPEngine, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
              <!-- Provide objectId and appId before using extension properties. -->
              <Metadata>
                <Item Key="ApplicationObjectId">insert objectId here</Item>
                <Item Key="ClientId">insert appId here</Item>
              </Metadata>
            <!-- End of changes -->
              <CryptographicKeys>
                <Key Id="issuer_secret" StorageReferenceId="TokenSigningKeyContainer" />
              </CryptographicKeys>
              <IncludeInSso>false</IncludeInSso>
              <UseTechnicalProfileForSessionManagement ReferenceId="SM-Noop" />
            </TechnicalProfile>
        </ClaimsProvider>
    </ClaimsProviders>
```

>[!NOTE]
>Olá <TechnicalProfile Id="AAD-Common"> é referenciado tooas "comuns", porque os respetivos elementos são incluídos no e reutilizados em todos os Olá do Azure Active Directory TechnicalProfiles utilizando o elemento de Olá:`<IncludeTechnicalProfile ReferenceId="AAD-Common" />`

>[!NOTE]
>Quando hello TechnicalProfile escritas para a propriedade de extensão para Olá primeiro tempo toohello recentemente criado, pode deparar-se um erro de uso individual.  propriedade de extensão de Olá é criada Olá pela primeira vez que é utilizado.  

## <a name="using-hello-new-extension-property--custom-attribute-in-a-user-journey"></a>Utilizar a nova propriedade de extensão Olá / personalizado o atributo em journey um utilizador


1. Olá abrir ficheiro de entidade Confiadora Party(RP) que descreve a política de editar journey de utilizador.  Se estiver a iniciar a, poderá ser aconselhável toodownload a versão já configurada do hello RP PolicyEdit ficheiros diretamente a partir de Olá secção política do Azure B2C personalizada Olá portal do Azure.  Em alternativa, abra o ficheiro XML a partir da sua pasta de armazenamento.
2. Adicionar uma afirmação personalizada `loyaltyId`.  Incluindo Olá personalizada de afirmação no Olá `<RelyingParty>` elemento, que é transmitida como um parâmetro toohello UserJourney TechnicalProfiles e incluída no token de Olá para aplicação Olá.
```xml
<RelyingParty>
   <DefaultUserJourney ReferenceId="ProfileEdit" />
   <TechnicalProfile Id="PolicyProfile">
     <DisplayName>PolicyProfile</DisplayName>
     <Protocol Name="OpenIdConnect" />
     <OutputClaims>
       <OutputClaim ClaimTypeReferenceId="objectId" PartnerClaimType="sub"/>
       <OutputClaim ClaimTypeReferenceId="city" />

       <OutputClaim ClaimTypeReferenceId="extension_loyaltyId" />

     </OutputClaims>
     <SubjectNamingInfo ClaimType="sub" />
   </TechnicalProfile>
 </RelyingParty>
 ```
3. Adicionar um ficheiro de política de extensão de toohello de definição de afirmação `TrustFrameworkExtensions.xml` dentro Olá `<ClaimsSchema>` elemento conforme mostrado.
```xml
<ClaimsSchema>
        <ClaimType Id="extension_loyaltyId">
            <DisplayName>Loyalty Identification Tag</DisplayName>
            <DataType>string</DataType>
            <UserHelpText>Your loyalty number from your membership card</UserHelpText>
            <UserInputType>TextBox</UserInputType>
        </ClaimType>
</ClaimsSchema>
```
4. Adicionar Olá afirmação mesmo ficheiro de definição de política de Base de toohello `TrustFrameworkBase.xml`.  
>Adicionar um `ClaimType` definição na base de Olá e ficheiro de extensões de Olá normalmente não é necessária, no entanto, uma vez que os passos seguintes Olá adicionará Olá extension_loyaltyId tooTechnicalProfiles no ficheiro de Base de Olá, validação de política de Olá irão rejeitar o carregamento de Olá do ficheiro de base de Olá sem ele.
>Poderá ser útil tootrace execução Olá Olá journey de utilizador com o nome "ProfileEdit" no ficheiro de TrustFrameworkBase.xml Olá.  Procure journey de utilizador de Olá de Olá mesmo nome no seu editor e observar se Orchestration passo 5 invoca Olá TechnicalProfileReferenceID = "SelfAsserted ProfileUpdate".  Procurar e inspecionar este toofamiliarize TechnicalProfile por si com o fluxo de Olá.
5. Adicionar loyaltyId como afirmações de entrada e saída no Olá TechnicalProfile "SelfAsserted ProfileUpdate"
```xml
<TechnicalProfile Id="SelfAsserted-ProfileUpdate">
          <DisplayName>User ID signup</DisplayName>
          <Protocol Name="Proprietary" Handler="Web.TPEngine.Providers.SelfAssertedAttributeProvider, Web.TPEngine, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
          <Metadata>
            <Item Key="ContentDefinitionReferenceId">api.selfasserted.profileupdate</Item>
          </Metadata>
          <IncludeInSso>false</IncludeInSso>
          <InputClaims>

            <InputClaim ClaimTypeReferenceId="alternativeSecurityId" />
            <InputClaim ClaimTypeReferenceId="userPrincipalName" />

            <!-- Optional claims. These claims are collected from hello user and can be modified. Any claim added here should be updated in the
                 ValidationTechnicalProfile referenced below so it can be written toodirectory after being updateed by hello user, i.e. AAD-UserWriteProfileUsingObjectId. -->
            <InputClaim ClaimTypeReferenceId="givenName" />
            <InputClaim ClaimTypeReferenceId="surname" />
            <InputClaim ClaimTypeReferenceId="extension_loyaltyId"/>
          </InputClaims>
          <OutputClaims>
            <!-- Required claims -->
            <OutputClaim ClaimTypeReferenceId="executed-SelfAsserted-Input" DefaultValue="true" />

            <!-- Optional claims. These claims are collected from hello user and can be modified. Any claim added here should be updated in the
                 ValidationTechnicalProfile referenced below so it can be written toodirectory after being updateed by hello user, i.e. AAD-UserWriteProfileUsingObjectId. -->
            <OutputClaim ClaimTypeReferenceId="givenName" />
            <OutputClaim ClaimTypeReferenceId="surname" />
            <OutputClaim ClaimTypeReferenceId="extension_loyaltyId"/>
          </OutputClaims>
          <ValidationTechnicalProfiles>
            <ValidationTechnicalProfile ReferenceId="AAD-UserWriteProfileUsingObjectId" />
          </ValidationTechnicalProfiles>
        </TechnicalProfile>
```
6. Adicione afirmação TechnicalProfile "AAD UserWriteProfileUsingObjectId" toopersist Olá valor Olá afirmação na propriedade de extensão de Olá, para o utilizador atual do Olá no diretório de Olá.
```xml
<TechnicalProfile Id="AAD-UserWriteProfileUsingObjectId">
          <Metadata>
            <Item Key="Operation">Write</Item>
            <Item Key="RaiseErrorIfClaimsPrincipalAlreadyExists">false</Item>
            <Item Key="RaiseErrorIfClaimsPrincipalDoesNotExist">true</Item>
          </Metadata>
          <IncludeInSso>false</IncludeInSso>
          <InputClaims>
            <InputClaim ClaimTypeReferenceId="objectId" Required="true" />
          </InputClaims>
          <PersistedClaims>
            <!-- Required claims -->
            <PersistedClaim ClaimTypeReferenceId="objectId" />

            <!-- Optional claims -->
            <PersistedClaim ClaimTypeReferenceId="givenName" />
            <PersistedClaim ClaimTypeReferenceId="surname" />
            <PersistedClaim ClaimTypeReferenceId="extension_loyaltyId" />

          </PersistedClaims>
          <IncludeTechnicalProfile ReferenceId="AAD-Common" />
        </TechnicalProfile>
```
7. Adicione afirmação no valor de Olá tooread TechnicalProfile "AAD UserReadUsingObjectId" do atributo de extensão de Olá sempre que um utilizador inicia sessão. Deste modo, até que ponto Olá TechnicalProfiles foram alterados no fluxo de Olá do apenas para contas locais.  Se o atributo novo Olá for pretendido no fluxo de Olá de uma conta federada/social, um conjunto diferente de TechnicalProfiles tem toobe alterado. Consulte os passos seguintes.

```xml
<!-- hello following technical profile is used tooread data after user authenticates. -->
     <TechnicalProfile Id="AAD-UserReadUsingObjectId">
       <Metadata>
         <Item Key="Operation">Read</Item>
         <Item Key="RaiseErrorIfClaimsPrincipalDoesNotExist">true</Item>
       </Metadata>
       <IncludeInSso>false</IncludeInSso>
       <InputClaims>
         <InputClaim ClaimTypeReferenceId="objectId" Required="true" />
       </InputClaims>
       <OutputClaims>
         <!-- Optional claims -->
         <OutputClaim ClaimTypeReferenceId="signInNames.emailAddress" />
         <OutputClaim ClaimTypeReferenceId="displayName" />
         <OutputClaim ClaimTypeReferenceId="otherMails" />
         <OutputClaim ClaimTypeReferenceId="givenName" />
         <OutputClaim ClaimTypeReferenceId="surname" />
         <OutputClaim ClaimTypeReferenceId="extension_loyaltyId" />
       </OutputClaims>
       <IncludeTechnicalProfile ReferenceId="AAD-Common" />
     </TechnicalProfile>
```


>[!IMPORTANT]
>elemento de IncludeTechnicalProfile Olá adiciona todos os elementos de Olá do AAD comuns toothis TechnicalProfile.

## <a name="test-hello-custom-policy-using-run-now"></a>Testar a política personalizada de Olá utilizando "Executar agora"
1. Abra Olá **do Azure AD B2c** e navegue demasiado**identidade experiência Framework > políticas personalizadas**.
1. Selecione a política personalizada de Olá que carregou e clique em Olá **executar agora** botão.
1. Deve ser capaz de toosign através de um endereço de e-mail.

token de id de Olá devolveu tooyour aplicação inclui a nova propriedade de extensão Olá como uma afirmação personalizada precedida por extension_loyaltyId. Consulte o exemplo.

```
{
  "exp": 1493585187,
  "nbf": 1493581587,
  "ver": "1.0",
  "iss": "https://login.microsoftonline.com/f06c2fe8-709f-4030-85dc-38a4bfd9e82d/v2.0/",
  "sub": "a58e7c6c-7535-4074-93da-b0023fbaf3ac",
  "aud": "4e87c1dd-e5f5-4ac8-8368-bc6a98751b8b",
  "acr": "b2c_1a_trustframeworkprofileedit",
  "nonce": "defaultNonce",
  "iat": 1493581587,
  "auth_time": 1493581587,
  "extension_loyaltyId": "abc",
  "city": "Redmond"
}
```

## <a name="next-steps"></a>Passos seguintes

Adicione Olá nova afirmação toohello fluxos para inícios de sessão de conta de redes sociais alterando Olá TechnicalProfiles listados. Estas duas TechnicalProfiles são utilizados por toowrite de inícios de sessão de conta federada/social e ler os dados de utilizador de Olá utilizando Olá alternativeSecurityId como Olá localizador de objeto de utilizador de Olá.
```
  <TechnicalProfile Id="AAD-UserWriteUsingAlternativeSecurityId">

  <TechnicalProfile Id="AAD-UserReadUsingAlternativeSecurityId">
```

Utilizar Olá mesmos atributos de extensão entre as políticas incorporadas e personalizadas.
Quando adiciona os atributos de extensão (também conhecido como atributos personalizados) através de experiência do portal Olá, esses atributos estão registados utilizando Olá * *-extensões-aplicação b2c que existe na cada inquilino do b2c.  toouse estes atributos de extensão na sua política personalizada:
1. Dentro do seu inquilino do b2c em portal.azure.com, navegue até demasiado**do Azure Active Directory** e selecione **registos de aplicação**
2. Localizar o **aplicação de extensões de b2c** e selecione-
3. Em Olá de registo 'Essentials' **ID da aplicação** e Olá **ID de objeto**
4. Inclui-los os seus metadados do perfil comum AAD técnica como da seguinte forma:

```xml
    <ClaimsProviders>
        <ClaimsProvider>
              <DisplayName>Azure Active Directory</DisplayName>
            <TechnicalProfile Id="AAD-Common">
              <DisplayName>Azure Active Directory</DisplayName>
              <Protocol Name="Proprietary" Handler="Web.TPEngine.Providers.AzureActiveDirectoryProvider, Web.TPEngine, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
              <!-- Provide objectId and appId before using extension properties. -->
              <Metadata>
                <Item Key="ApplicationObjectId">insert objectId here</Item> <!-- This is hello "Object ID" from hello "b2c-extensions-app"-->
                <Item Key="ClientId">insert appId here</Item> <!--This is hello "Application ID" from hello "b2c-extensions-app"-->
              </Metadata>
```

tookeep consistência com a experiência de portal Olá, criar estes atributos através da IU do portal de Olá *antes* utilizá-los no seu políticas personalizadas.  Quando cria um atributo "ActivationStatus" no portal de Olá, tem de referenciar tooit da seguinte forma:

```
extension_ActivationStatus in hello custom policy
extension_<app-guid>_ActivationStatus via hello Graph API.
```


## <a name="reference"></a>Referência

* A **perfil técnica (TP)** é um tipo de elemento que pode considerar como um *função* que define o nome de um ponto final, os metadados, o protocolo e detalhes Olá exchange de afirmações que Olá identidade Experiência Framework deverá efetuar.  Quando isto *função* denomina-se um passo de orquestração ou a partir de outro TechnicalProfile, Olá InputClaims e OutputClaims são fornecidos como parâmetros pelo autor da chamada de Olá.


* Para um total tratamento nas propriedades da extensão, consulte o artigo de Olá [EXTENSÕES de esquema de DIRETÓRIO | CONCEITOS DE API DO GRÁFICO](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-directory-schema-extensions)

>[!NOTE]
>Os atributos de extensão no Graph API são denominados utilizando Convenção Olá `extension_ApplicationObjectID_attributename`. As políticas personalizadas Consulte tooextensions atributos como extension_attributename, deste modo, omitindo Olá ApplicationObjectId no Olá XML
