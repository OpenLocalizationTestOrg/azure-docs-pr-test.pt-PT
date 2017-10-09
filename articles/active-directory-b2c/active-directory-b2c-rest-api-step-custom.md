---
title: "O Azure Active Directory B2C: API de REST afirmações trocas como um passo de orquestração | Microsoft Docs"
description: "Um tópico no Azure Active Directory B2C políticas personalizadas que se integram com uma API"
services: active-directory-b2c
documentationcenter: 
author: rojasja
manager: krassk
editor: rojasja
ms.assetid: 
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 04/24/2017
ms.author: joroja
ms.openlocfilehash: 90a495029f48d70232ef3f99de4ea4d351395aa7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-integrate-rest-api-claims-exchanges-in-your-azure-ad-b2c-user-journey-as-an-orchestration-step"></a>Instruções: Integrar o REST API trocas de afirmações da sua viagem do Azure AD B2C utilizador como um passo de orquestração

Olá identidade experiência Framework (IEF) subjacente do Azure Active Directory B2C (Azure AD B2C) permite Olá identidade programador toointegrate uma interação com uma API RESTful em journey um utilizador.  

No final de Olá destas instruções, será capaz de toocreate um journey de utilizador do Azure AD B2C que interage com os serviços RESTful.

Olá IEF envia os dados em afirmações e recebe dados novamente nas afirmações. Olá REST API afirmações exchange:

- Pode ser desenvolvido como um passo de orquestração.
- Pode acionar uma ação externa. Por exemplo, pode iniciar um evento numa base de dados externa.
- Pode ser toofetch utilizado um valor e, em seguida, guarde-o numa base de dados de utilizador de Olá.

Pode utilizar afirmações de Olá recebido fluxo de Olá toochange posterior de execução.

Também pode conceber interação Olá como um perfil de validação. Para obter mais informações, consulte [explicação passo a passo: integrar o API de REST afirmações trocas da sua viagem do Azure AD B2C utilizador como validação na entrada de utilizador](active-directory-b2c-rest-api-validation-custom.md).

cenário de Olá é que quando um utilizador efetua uma edição de perfil, queremos:

1. Procure um utilizador Olá num sistema externo.
2. Cidade de Olá Get em que o utilizador está registado.
3. Devolva essa aplicação toohello de atributo como uma afirmação.

## <a name="prerequisites"></a>Pré-requisitos

- Um toocomplete de configurado de inquilino do Azure AD B2C uma conta local sessão-up/início de sessão, conforme descrito em [introdução](active-directory-b2c-get-started-custom.md).
- Um ponto final de REST API é toointeract com. Estas instruções utilizam um webhook de aplicação de função do Azure simples como exemplo.
- *Recomendado*: Olá concluída [exchange instruções como um passo de validação de afirmações de REST API](active-directory-b2c-rest-api-validation-custom.md).

## <a name="step-1-prepare-hello-rest-api-function"></a>Passo 1: Preparar a função de REST API de Olá

> [!NOTE]
> A configuração de funções de API de REST está fora do âmbito de Olá deste artigo. [As funções do Azure](https://docs.microsoft.com/azure/azure-functions/functions-reference) fornece uma excelente toolkit toocreate serviços RESTful na nuvem de Olá.

Vamos configurar uma função do Azure que recebe uma afirmação denominada `email`, e, em seguida, devolve Olá afirmação `city` com o valor Olá atribuído `Redmond`. exemplo de Olá função do Azure está em [GitHub](https://github.com/Azure-Samples/active-directory-b2c-advanced-policies/tree/master/AzureFunctionsSamples).

Olá `userMessage` afirmação Olá devolve a função do Azure é opcional neste contexto e Olá IEF ignorará. Potencialmente pode utilizá-lo como uma mensagem transmitida toohello aplicação e apresentados toohello utilizador mais tarde.

```csharp
if (requestContentAsJObject.email == null)
{
    return request.CreateResponse(HttpStatusCode.BadRequest);
}

var email = ((string) requestContentAsJObject.email).ToLower();

return request.CreateResponse<ResponseContent>(
    HttpStatusCode.OK,
    new ResponseContent
    {
        version = "1.0.0",
        status = (int) HttpStatusCode.OK,
        userMessage = "User Found",
        city = "Redmond"
    },
    new JsonMediaTypeFormatter(),
    "application/json");
```

Uma aplicação de função do Azure faz com que o URL de função do tooget fácil Olá, que inclui o identificador de Olá da função específica Olá. Neste caso, é o URL de Olá: https://wingtipb2cfuncs.azurewebsites.net/api/LookUpLoyaltyWebHook?code=MQuG7BIE3eXBaCZ/YCfY1SHabm55HEphpNLmh1OP3hdfHkvI2QwPrw==. Pode utilizá-lo para fins de teste.

## <a name="step-2-configure-hello-restful-api-claims-exchange-as-a-technical-profile-in-your-trustframeworextensionsxml-file"></a>Passo 2: Configurar o exchange de afirmações de RESTful API Olá como um perfil no seu ficheiro TrustFrameworExtensions.xml técnico

Um perfil técnico é a configuração completa do Olá do exchange Olá pretendido com Olá serviço RESTful. Abrir o ficheiro de TrustFrameworkExtensions.xml Olá e adicione Olá seguinte fragmento XML dentro Olá `<ClaimsProvider>` elemento.

> [!NOTE]
> No Olá seguir XML, fornecedor RESTful `Version=1.0.0.0` será descrita como protocolo de Olá. Considere-lo como a função Olá que irá interagir com o serviço de Olá externo. <!-- TODO: A full definition of hello schema can be found...link tooRESTful Provider schema definition>-->

```XML
<ClaimsProvider>
    <DisplayName>REST APIs</DisplayName>
    <TechnicalProfiles>
        <TechnicalProfile Id="AzureFunctions-LookUpLoyaltyWebHook">
            <DisplayName>Check LookUpLoyalty Web Hook Azure Function</DisplayName>
            <Protocol Name="Proprietary" Handler="Web.TPEngine.Providers.RestfulProvider, Web.TPEngine, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
            <Metadata>
                <Item Key="ServiceUrl">https://wingtipb2cfuncs.azurewebsites.net/api/LookUpLoyaltyWebHook?code=MQuG7BIE3eXBaCZ/YCfY1SHabm55HEphpNLmh1OP3hdfHkvI2QwPrw==</Item>
                <Item Key="AuthenticationType">None</Item>
                <Item Key="SendClaimsIn">Body</Item>
            </Metadata>
            <InputClaims>
                <InputClaim ClaimTypeReferenceId="givenName" PartnerClaimType="email" />
            </InputClaims>
            <OutputClaims>
                <OutputClaim ClaimTypeReferenceId="city" PartnerClaimType="city" />
            </OutputClaims>
            <UseTechnicalProfileForSessionManagement ReferenceId="SM-Noop" />
        </TechnicalProfile>
    </TechnicalProfiles>
</ClaimsProvider>
```

Olá `<InputClaims>` elemento define afirmações Olá que serão enviadas Olá serviço do IEF toohello REST. Neste exemplo, Olá conteúdos da afirmação Olá `givenName` será enviado serviço REST de toohello como afirmação Olá `email`.  

Olá `<OutputClaims>` elemento define Olá afirmações que Olá IEF irá esperar do serviço REST de Olá. Independentemente do número de Olá de afirmações que são recebidos, Olá IEF irá utilizar apenas os identificado aqui. Neste exemplo, uma afirmação recebida como `city` será chamada tooan mapeada IEF afirmação `city`.

## <a name="step-3-add-hello-new-claim-city-toohello-schema-of-your-trustframeworkextensionsxml-file"></a>Passo 3: Adicionar nova afirmação de Olá `city` toohello esquema do ficheiro TrustFrameworkExtensions.xml

Olá afirmação `city` é ainda não definidos em qualquer lugar no nosso esquema. Por isso, adicione uma definição no interior do elemento de Olá `<BuildingBlocks>`. Pode encontrar este elemento de início de Olá do ficheiro de TrustFrameworkExtensions.xml Olá.

```XML
<BuildingBlocks>
    <!--hello claimtype city must be added toohello TrustFrameworkPolicy-->
    <!-- You can add new claims in hello BASE file Section III, or in hello extensions file-->
    <ClaimsSchema>
        <ClaimType Id="city">
            <DisplayName>City</DisplayName>
            <DataType>string</DataType>
            <UserHelpText>Your city</UserHelpText>
            <UserInputType>TextBox</UserInputType>
        </ClaimType>
    </ClaimsSchema>
</BuildingBlocks>
```

## <a name="step-4-include-hello-rest-service-claims-exchange-as-an-orchestration-step-in-your-profile-edit-user-journey-in-trustframeworkextensionsxml"></a>Passo 4: Incluir Olá REST serviço afirmações exchange como um passo de orquestração da sua perfil Editar utilizador viagem no TrustFrameworkExtensions.xml

Adicione um passo toohello perfil Editar utilizador journey, depois do utilizador Olá foi autenticado (orchestration passos 1 a 4 olá seguir XML) e utilizador Olá forneceu informações de perfil Olá atualizado (passo 5).

> [!NOTE]
> Existem muitos casos de utilização onde Olá chamada da REST API pode ser utilizado como um passo de orquestração. Como um passo de orquestração, pode ser utilizado como um sistema externo de tooan atualização depois de um utilizador foi concluída com êxito uma tarefa, como o registo da primeira vez ou como um perfil de atualizar informações de tookeep sincronizadas. Neste caso, é utilizado tooaugment informações de Olá fornecidas toohello aplicação depois de editar o perfil de Olá.

Perfil de Olá cópia editar o código XML de journey de utilizador do ficheiro do Olá TrustFrameworkBase.xml ficheiro tooyour TrustFrameworkExtensions.xml dentro Olá `<UserJourneys>` elemento. Em seguida, efetue modificação de Olá no passo 6.

```XML
<OrchestrationStep Order="6" Type="ClaimsExchange">
    <ClaimsExchanges>
        <ClaimsExchange Id="GetLoyaltyData" TechnicalProfileReferenceId="AzureFunctions-LookUpLoyaltyWebHook" />
    </ClaimsExchanges>
</OrchestrationStep>
```

> [!IMPORTANT]
> Se a ordem de Olá não corresponde à sua versão, certifique-se de que inserir o código de Olá como passo Olá antes Olá `ClaimsExchange` tipo `SendClaims`.

Olá final XML para journey de utilizador Olá deve ter o seguinte aspeto:

```XML
<UserJourney Id="ProfileEdit">
    <OrchestrationSteps>
        <OrchestrationStep Order="1" Type="ClaimsProviderSelection" ContentDefinitionReferenceId="api.idpselections">
            <ClaimsProviderSelections>
                <ClaimsProviderSelection TargetClaimsExchangeId="FacebookExchange" />
                <ClaimsProviderSelection TargetClaimsExchangeId="LocalAccountSigninEmailExchange" />
            </ClaimsProviderSelections>
        </OrchestrationStep>
        <OrchestrationStep Order="2" Type="ClaimsExchange">
            <ClaimsExchanges>
                <ClaimsExchange Id="FacebookExchange" TechnicalProfileReferenceId="Facebook-OAUTH" />
                <ClaimsExchange Id="LocalAccountSigninEmailExchange" TechnicalProfileReferenceId="SelfAsserted-LocalAccountSignin-Email" />
            </ClaimsExchanges>
        </OrchestrationStep>
        <OrchestrationStep Order="3" Type="ClaimsExchange">
            <Preconditions>
                <Precondition Type="ClaimEquals" ExecuteActionsIf="true">
                    <Value>authenticationSource</Value>
                    <Value>localAccountAuthentication</Value>
                    <Action>SkipThisOrchestrationStep</Action>
                </Precondition>
            </Preconditions>
            <ClaimsExchanges>
                <ClaimsExchange Id="AADUserRead" TechnicalProfileReferenceId="AAD-UserReadUsingAlternativeSecurityId" />
            </ClaimsExchanges>
        </OrchestrationStep>
        <OrchestrationStep Order="4" Type="ClaimsExchange">
            <Preconditions>
                <Precondition Type="ClaimEquals" ExecuteActionsIf="true">
                    <Value>authenticationSource</Value>
                    <Value>socialIdpAuthentication</Value>
                    <Action>SkipThisOrchestrationStep</Action>
                </Precondition>
            </Preconditions>
            <ClaimsExchanges>
                <ClaimsExchange Id="AADUserReadWithObjectId" TechnicalProfileReferenceId="AAD-UserReadUsingObjectId" />
            </ClaimsExchanges>
        </OrchestrationStep>
        <OrchestrationStep Order="5" Type="ClaimsExchange">
            <ClaimsExchanges>
                <ClaimsExchange Id="B2CUserProfileUpdateExchange" TechnicalProfileReferenceId="SelfAsserted-ProfileUpdate" />
            </ClaimsExchanges>
        </OrchestrationStep>
        <!-- Add a step 6 toohello user journey before hello JWT token is created-->
        <OrchestrationStep Order="6" Type="ClaimsExchange">
            <ClaimsExchanges>
                <ClaimsExchange Id="GetLoyaltyData" TechnicalProfileReferenceId="AzureFunctions-LookUpLoyaltyWebHook" />
            </ClaimsExchanges>
        </OrchestrationStep>
        <OrchestrationStep Order="7" Type="SendClaims" CpimIssuerTechnicalProfileReferenceId="JwtIssuer" />
    </OrchestrationSteps>
    <ClientDefinition ReferenceId="DefaultWeb" />
</UserJourney>
```

## <a name="step-5-add-hello-claim-city-tooyour-relying-party-policy-file-so-hello-claim-is-sent-tooyour-application"></a>Passo 5: Adicionar Olá afirmação `city` tooyour política da entidade confiadora do ficheiro para que a afirmação de Olá é enviada tooyour aplicação

Edite o ficheiro do ProfileEdit.xml entidade confiadora (RP) de terceiros e modifique Olá `<TechnicalProfile Id="PolicyProfile">` seguinte do elemento tooadd Olá: `<OutputClaim ClaimTypeReferenceId="city" />`.

Depois de adicionar a nova afirmação de Olá, perfil técnica Olá este aspeto:

```XML
<DisplayName>PolicyProfile</DisplayName>
    <Protocol Name="OpenIdConnect" />
    <OutputClaims>
      <OutputClaim ClaimTypeReferenceId="objectId" PartnerClaimType="sub"/>
      <OutputClaim ClaimTypeReferenceId="city" />
    </OutputClaims>
    <SubjectNamingInfo ClaimType="sub" />
</TechnicalProfile>
```

## <a name="step-6-upload-your-changes-and-test"></a>Passo 6: Carregar as suas alterações e teste

Substitua as versões existentes do Olá da política de Olá.

1.  (Opcional:) Guarde versão existente Olá (transferindo) do seu ficheiro extensões antes de continuar. tookeep Olá inicial complexidade baixa, recomendamos que não carregar várias versões do ficheiro de extensões de Olá.
2.  (Opcional:) Mudar o nome da nova versão de Olá do ID de política de Olá para o ficheiro de edição de política de Olá alterando `PolicyId="B2C_1A_TrustFrameworkProfileEdit"`.
3.  Carregar ficheiro de extensões de Olá.
4.  Carregue o ficheiro RP da edição de política de Olá.
5.  Utilize **executar agora** política de Olá tootest. Token de Olá de revisão que Olá IEF devolve toohello aplicação.

Se tudo está configurado corretamente, o token de Olá irá incluir afirmação nova Olá `city`, com o valor de Olá `Redmond`.

```JSON
{
  "exp": 1493053292,
  "nbf": 1493049692,
  "ver": "1.0",
  "iss": "https://login.microsoftonline.com/f06c2fe8-709f-4030-85dc-38a4bfd9e82d/v2.0/",
  "sub": "a58e7c6c-7535-4074-93da-b0023fbaf3ac",
  "aud": "4e87c1dd-e5f5-4ac8-8368-bc6a98751b8b",
  "acr": "b2c_1a_trustframeworkprofileedit",
  "nonce": "defaultNonce",
  "iat": 1493049692,
  "auth_time": 1493049692,
  "city": "Redmond"
}
```

## <a name="next-steps"></a>Passos seguintes

[Utilizar uma API REST como um passo de validação](active-directory-b2c-rest-api-validation-custom.md)

[Modificar Olá perfil editar toogather informação adicional sobre os seus utilizadores](active-directory-b2c-create-custom-attributes-profile-edit-custom.md)
