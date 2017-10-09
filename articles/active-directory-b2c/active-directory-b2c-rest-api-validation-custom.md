---
title: "O Azure Active Directory B2C: API de REST afirmações trocas como validação | Microsoft Docs"
description: "Um tópico sobre as políticas personalizadas do Azure Active Directory B2C"
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
ms.openlocfilehash: cec6c6e110514a8bbe0e0780f36738ff21ae2f00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-integrate-rest-api-claims-exchanges-in-your-azure-ad-b2c-user-journey-as-validation-on-user-input"></a>Instruções: Integrar o REST API trocas de afirmações da sua viagem do Azure AD B2C utilizador como validação no intervenção do utilizador

Olá identidade experiência Framework (IEF) subjacente do Azure Active Directory B2C (Azure AD B2C) permite Olá identidade programador toointegrate uma interação com uma API RESTful em journey um utilizador.  

No final de Olá destas instruções, será capaz de toocreate um journey de utilizador do Azure AD B2C que interage com os serviços RESTful.

Olá IEF envia os dados em afirmações e recebe dados novamente nas afirmações. interação de Olá com Olá API:

- Pode ser estruturada como uma troca de afirmações de REST API ou como um perfil de validação, o que acontece no interior de um passo de orquestração.
- Normalmente, valida a entrada de utilizador de Olá. Se o valor de Olá de utilizador de Olá é rejeitado, o utilizador Olá pode tentar novamente tooenter um valor válido com Olá oportunidade tooreturn uma mensagem de erro.

Também pode conceber interação Olá como um passo de orquestração. Para obter mais informações, consulte [explicação passo a passo: trocas da sua do Azure AD B2C utilizador viagem como um passo de orquestração de afirmações de integrar o API de REST](active-directory-b2c-rest-api-step-custom.md).

Por exemplo de perfil de validação de Olá, utilizaremos journey do Olá perfil Editar utilizador no ficheiro de pacote de arranque Olá ProfileEdit.xml.

Verificar a esse nome Olá fornecido pelo utilizador Olá no perfil de Olá editar não faz parte de uma lista de exclusão.

## <a name="prerequisites"></a>Pré-requisitos

- Um toocomplete de configurado de inquilino do Azure AD B2C uma conta local sessão-up/início de sessão, conforme descrito em [introdução](active-directory-b2c-get-started-custom.md).
- Um ponto final de REST API é toointeract com. Nestas instruções, configurámos um site de demonstração chamado [WingTipGames](https://wingtipgamesb2c.azurewebsites.net/) com um serviço de REST API.

## <a name="step-1-prepare-hello-rest-api-function"></a>Passo 1: Preparar a função de REST API de Olá

> [!NOTE]
> A configuração de funções de API de REST está fora do âmbito de Olá deste artigo. [As funções do Azure](https://docs.microsoft.com/azure/azure-functions/functions-reference) fornece uma excelente toolkit toocreate serviços RESTful na nuvem de Olá.

Criámos uma função do Azure que recebe uma afirmação que se espera como `playerTag`. a função Olá valida se esta afirmação existe. Pode aceder ao código de função do Azure completa Olá no [GitHub](https://github.com/Azure-Samples/active-directory-b2c-advanced-policies/tree/master/AzureFunctionsSamples).

```csharp
if (requestContentAsJObject.playerTag == null)
{
  return request.CreateResponse(HttpStatusCode.BadRequest);
}

var playerTag = ((string) requestContentAsJObject.playerTag).ToLower();

if (playerTag == "mcvinny" || playerTag == "msgates123" || playerTag == "revcottonmarcus")
{
  return request.CreateResponse<ResponseContent>(
    HttpStatusCode.Conflict,
    new ResponseContent
    {
      version = "1.0.0",
      status = (int) HttpStatusCode.Conflict,
      userMessage = $"hello player tag '{requestContentAsJObject.playerTag}' is already used."
    },
    new JsonMediaTypeFormatter(),
    "application/json");
}

return request.CreateResponse(HttpStatusCode.OK);
```

Olá IEF espera Olá `userMessage` afirmação devolve esse Olá função do Azure. Esta afirmação será apresentada como um utilizador de toohello de cadeia se a validação de Olá falhar, por exemplo, quando um Estado de 409 conflito é devolvido em Olá anterior exemplo.

## <a name="step-2-configure-hello-restful-api-claims-exchange-as-a-technical-profile-in-your-trustframeworkextensionsxml-file"></a>Passo 2: Configurar o exchange de afirmações de RESTful API Olá como um perfil no seu ficheiro TrustFrameworkExtensions.xml técnico

Um perfil técnico é a configuração completa do Olá do exchange Olá pretendido com Olá serviço RESTful. Abrir o ficheiro de TrustFrameworkExtensions.xml Olá e adicione Olá seguinte fragmento XML dentro Olá `<ClaimsProviders>` elemento.

> [!NOTE]
> No Olá seguir XML, fornecedor RESTful `Version=1.0.0.0` será descrita como protocolo de Olá. Considere-lo como a função Olá que irá interagir com o serviço de Olá externo. <!-- TODO: A full definition of hello schema can be found...link tooRESTful Provider schema definition>-->

```xml
<ClaimsProvider>
    <DisplayName>REST APIs</DisplayName>
    <TechnicalProfiles>
        <TechnicalProfile Id="AzureFunctions-CheckPlayerTagWebHook">
            <DisplayName>Check Player Tag Web Hook Azure Function</DisplayName>
            <Protocol Name="Proprietary" Handler="Web.TPEngine.Providers.RestfulProvider, Web.TPEngine, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
            <Metadata>
                <Item Key="ServiceUrl">https://wingtipb2cfuncs.azurewebsites.net/api/CheckPlayerTagWebHook?code=L/05YRSpojU0nECzM4Tp3LjBiA2ZGh3kTwwp1OVV7m0SelnvlRVLCg==</Item>
                <Item Key="AuthenticationType">None</Item>
                <Item Key="SendClaimsIn">Body</Item>
            </Metadata>
            <InputClaims>
                <InputClaim ClaimTypeReferenceId="givenName" PartnerClaimType="playerTag" />
            </InputClaims>
            <UseTechnicalProfileForSessionManagement ReferenceId="SM-Noop" />
        </TechnicalProfile>
        <TechnicalProfile Id="SelfAsserted-ProfileUpdate">
            <ValidationTechnicalProfiles>
                <ValidationTechnicalProfile ReferenceId="AzureFunctions-CheckPlayerTagWebHook" />
            </ValidationTechnicalProfiles>
        </TechnicalProfile>
    </TechnicalProfiles>
</ClaimsProvider>
```

Olá `InputClaims` elemento define afirmações Olá que serão enviadas Olá serviço do IEF toohello REST. Neste exemplo, Olá conteúdos da afirmação Olá `givenName` serão enviados toohello o serviço REST como `playerTag`. Neste exemplo, Olá que IEF não espera afirmações novamente. Em vez disso, aguarda para uma resposta do serviço REST de Olá e atos baseados em códigos de estado de Olá que recebe.

## <a name="step-3-include-hello-restful-service-claims-exchange-in-self-asserted-technical-profile-where-you-want-toovalidate-hello-user-input"></a>Passo 3: Incluem Olá serviço RESTful afirmações exchange no perfil técnica automática permitido onde pretende intervenção do utilizador toovalidate Olá

Olá mais comuns a utilização do passo de validação de Olá está no interação Olá com um utilizador. Todas as interações onde o utilizador Olá é tooprovide esperado de entrada são *automática permitido perfis técnicas*. Neste exemplo, iremos adicionar perfil técnica de Olá validação toohello Self Asserted ProfileUpdate. Este é Olá perfil técnica que Olá ficheiro da política de entidade confiadora (RP) de terceiros `Profile Edit` utiliza.

Olá de tooadd afirmações exchange toohello automática permitido técnica perfil:

1. Abra o ficheiro de TrustFrameworkBase.xml Olá e procure `<TechnicalProfile Id="SelfAsserted-ProfileUpdate">`.
2. Reveja a configuração de Olá deste perfil técnica. Observe como o exchange Olá com utilizador Olá está definido como afirmações que serão pedidas ao utilizador Olá (afirmações de entrada) e as afirmações que serão esperadas novamente a partir do fornecedor de Self-permitido Olá (afirmações de saída).
3. Procurar `TechnicalProfileReferenceId="SelfAsserted-ProfileUpdate`e tenha em atenção que este perfil é invocado como orchestration passo 6 `<UserJourney Id="ProfileEdit">`.

## <a name="step-4-upload-and-test-hello-profile-edit-rp-policy-file"></a>Passo 4: Carregar e testar o ficheiro de política do Olá perfil editar RP

1. Carregar a versão nova do Olá do ficheiro de TrustFrameworkExtensions.xml Olá.
2. Utilize **executar agora** perfil de Olá tootest editar o ficheiro de política RP.
3. Teste de validação de Olá, fornecendo um dos nomes de Olá existente (por exemplo, mcvinny) num Olá **o nome fornecido** campo. Se tudo está configurado corretamente, deverá receber uma mensagem que notifica o utilizador Olá que tag de leitor de Olá já está a ser utilizado.

## <a name="next-steps"></a>Passos seguintes

[Modificar Olá perfil utilizador e editar registo toogather informação adicional sobre os seus utilizadores](active-directory-b2c-create-custom-attributes-profile-edit-custom.md)

[Instruções: Integrar o REST API trocas de afirmações da sua viagem do Azure AD B2C utilizador como um passo de orquestração](active-directory-b2c-rest-api-step-custom.md)
