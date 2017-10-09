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
# <a name="walkthrough-integrate-rest-api-claims-exchanges-in-your-azure-ad-b2c-user-journey-as-an-orchestration-step"></a><span data-ttu-id="6448a-103">Instruções: Integrar o REST API trocas de afirmações da sua viagem do Azure AD B2C utilizador como um passo de orquestração</span><span class="sxs-lookup"><span data-stu-id="6448a-103">Walkthrough: Integrate REST API claims exchanges in your Azure AD B2C user journey as an orchestration step</span></span>

<span data-ttu-id="6448a-104">Olá identidade experiência Framework (IEF) subjacente do Azure Active Directory B2C (Azure AD B2C) permite Olá identidade programador toointegrate uma interação com uma API RESTful em journey um utilizador.</span><span class="sxs-lookup"><span data-stu-id="6448a-104">hello Identity Experience Framework (IEF) that underlies Azure Active Directory B2C (Azure AD B2C) enables hello identity developer toointegrate an interaction with a RESTful API in a user journey.</span></span>  

<span data-ttu-id="6448a-105">No final de Olá destas instruções, será capaz de toocreate um journey de utilizador do Azure AD B2C que interage com os serviços RESTful.</span><span class="sxs-lookup"><span data-stu-id="6448a-105">At hello end of this walkthrough, you will be able toocreate an Azure AD B2C user journey that interacts with RESTful services.</span></span>

<span data-ttu-id="6448a-106">Olá IEF envia os dados em afirmações e recebe dados novamente nas afirmações.</span><span class="sxs-lookup"><span data-stu-id="6448a-106">hello IEF sends data in claims and receives data back in claims.</span></span> <span data-ttu-id="6448a-107">Olá REST API afirmações exchange:</span><span class="sxs-lookup"><span data-stu-id="6448a-107">hello REST API claims exchange:</span></span>

- <span data-ttu-id="6448a-108">Pode ser desenvolvido como um passo de orquestração.</span><span class="sxs-lookup"><span data-stu-id="6448a-108">Can be designed as an orchestration step.</span></span>
- <span data-ttu-id="6448a-109">Pode acionar uma ação externa.</span><span class="sxs-lookup"><span data-stu-id="6448a-109">Can trigger an external action.</span></span> <span data-ttu-id="6448a-110">Por exemplo, pode iniciar um evento numa base de dados externa.</span><span class="sxs-lookup"><span data-stu-id="6448a-110">For instance, it can log an event in an external database.</span></span>
- <span data-ttu-id="6448a-111">Pode ser toofetch utilizado um valor e, em seguida, guarde-o numa base de dados de utilizador de Olá.</span><span class="sxs-lookup"><span data-stu-id="6448a-111">Can be used toofetch a value and then store it in hello user database.</span></span>

<span data-ttu-id="6448a-112">Pode utilizar afirmações de Olá recebido fluxo de Olá toochange posterior de execução.</span><span class="sxs-lookup"><span data-stu-id="6448a-112">You can use hello received claims later toochange hello flow of execution.</span></span>

<span data-ttu-id="6448a-113">Também pode conceber interação Olá como um perfil de validação.</span><span class="sxs-lookup"><span data-stu-id="6448a-113">You can also design hello interaction as a validation profile.</span></span> <span data-ttu-id="6448a-114">Para obter mais informações, consulte [explicação passo a passo: integrar o API de REST afirmações trocas da sua viagem do Azure AD B2C utilizador como validação na entrada de utilizador](active-directory-b2c-rest-api-validation-custom.md).</span><span class="sxs-lookup"><span data-stu-id="6448a-114">For more information, see [Walkthrough: Integrate REST API claims exchanges in your Azure AD B2C user journey as validation on user input](active-directory-b2c-rest-api-validation-custom.md).</span></span>

<span data-ttu-id="6448a-115">cenário de Olá é que quando um utilizador efetua uma edição de perfil, queremos:</span><span class="sxs-lookup"><span data-stu-id="6448a-115">hello scenario is that when a user performs a profile edit, we want to:</span></span>

1. <span data-ttu-id="6448a-116">Procure um utilizador Olá num sistema externo.</span><span class="sxs-lookup"><span data-stu-id="6448a-116">Look up hello user in an external system.</span></span>
2. <span data-ttu-id="6448a-117">Cidade de Olá Get em que o utilizador está registado.</span><span class="sxs-lookup"><span data-stu-id="6448a-117">Get hello city where that user is registered.</span></span>
3. <span data-ttu-id="6448a-118">Devolva essa aplicação toohello de atributo como uma afirmação.</span><span class="sxs-lookup"><span data-stu-id="6448a-118">Return that attribute toohello application as a claim.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6448a-119">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="6448a-119">Prerequisites</span></span>

- <span data-ttu-id="6448a-120">Um toocomplete de configurado de inquilino do Azure AD B2C uma conta local sessão-up/início de sessão, conforme descrito em [introdução](active-directory-b2c-get-started-custom.md).</span><span class="sxs-lookup"><span data-stu-id="6448a-120">An Azure AD B2C tenant configured toocomplete a local account sign-up/sign-in, as described in [Getting started](active-directory-b2c-get-started-custom.md).</span></span>
- <span data-ttu-id="6448a-121">Um ponto final de REST API é toointeract com.</span><span class="sxs-lookup"><span data-stu-id="6448a-121">A REST API endpoint toointeract with.</span></span> <span data-ttu-id="6448a-122">Estas instruções utilizam um webhook de aplicação de função do Azure simples como exemplo.</span><span class="sxs-lookup"><span data-stu-id="6448a-122">This walkthrough uses a simple Azure function app webhook as an example.</span></span>
- <span data-ttu-id="6448a-123">*Recomendado*: Olá concluída [exchange instruções como um passo de validação de afirmações de REST API](active-directory-b2c-rest-api-validation-custom.md).</span><span class="sxs-lookup"><span data-stu-id="6448a-123">*Recommended*: Complete hello [REST API claims exchange walkthrough as a validation step](active-directory-b2c-rest-api-validation-custom.md).</span></span>

## <a name="step-1-prepare-hello-rest-api-function"></a><span data-ttu-id="6448a-124">Passo 1: Preparar a função de REST API de Olá</span><span class="sxs-lookup"><span data-stu-id="6448a-124">Step 1: Prepare hello REST API function</span></span>

> [!NOTE]
> <span data-ttu-id="6448a-125">A configuração de funções de API de REST está fora do âmbito de Olá deste artigo.</span><span class="sxs-lookup"><span data-stu-id="6448a-125">Setup of REST API functions is outside hello scope of this article.</span></span> <span data-ttu-id="6448a-126">[As funções do Azure](https://docs.microsoft.com/azure/azure-functions/functions-reference) fornece uma excelente toolkit toocreate serviços RESTful na nuvem de Olá.</span><span class="sxs-lookup"><span data-stu-id="6448a-126">[Azure Functions](https://docs.microsoft.com/azure/azure-functions/functions-reference) provides an excellent toolkit toocreate RESTful services in hello cloud.</span></span>

<span data-ttu-id="6448a-127">Vamos configurar uma função do Azure que recebe uma afirmação denominada `email`, e, em seguida, devolve Olá afirmação `city` com o valor Olá atribuído `Redmond`.</span><span class="sxs-lookup"><span data-stu-id="6448a-127">We have set up an Azure function that receives a claim called `email`, and then returns hello claim `city` with hello assigned value of `Redmond`.</span></span> <span data-ttu-id="6448a-128">exemplo de Olá função do Azure está em [GitHub](https://github.com/Azure-Samples/active-directory-b2c-advanced-policies/tree/master/AzureFunctionsSamples).</span><span class="sxs-lookup"><span data-stu-id="6448a-128">hello sample Azure function is on [GitHub](https://github.com/Azure-Samples/active-directory-b2c-advanced-policies/tree/master/AzureFunctionsSamples).</span></span>

<span data-ttu-id="6448a-129">Olá `userMessage` afirmação Olá devolve a função do Azure é opcional neste contexto e Olá IEF ignorará.</span><span class="sxs-lookup"><span data-stu-id="6448a-129">hello `userMessage` claim that hello Azure function returns is optional in this context, and hello IEF will ignore it.</span></span> <span data-ttu-id="6448a-130">Potencialmente pode utilizá-lo como uma mensagem transmitida toohello aplicação e apresentados toohello utilizador mais tarde.</span><span class="sxs-lookup"><span data-stu-id="6448a-130">You can potentially use it as a message passed toohello application and presented toohello user later.</span></span>

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

<span data-ttu-id="6448a-131">Uma aplicação de função do Azure faz com que o URL de função do tooget fácil Olá, que inclui o identificador de Olá da função específica Olá.</span><span class="sxs-lookup"><span data-stu-id="6448a-131">An Azure function app makes it easy tooget hello function URL, which includes hello identifier of hello specific function.</span></span> <span data-ttu-id="6448a-132">Neste caso, é o URL de Olá: https://wingtipb2cfuncs.azurewebsites.net/api/LookUpLoyaltyWebHook?code=MQuG7BIE3eXBaCZ/YCfY1SHabm55HEphpNLmh1OP3hdfHkvI2QwPrw==.</span><span class="sxs-lookup"><span data-stu-id="6448a-132">In this case, hello URL is: https://wingtipb2cfuncs.azurewebsites.net/api/LookUpLoyaltyWebHook?code=MQuG7BIE3eXBaCZ/YCfY1SHabm55HEphpNLmh1OP3hdfHkvI2QwPrw==.</span></span> <span data-ttu-id="6448a-133">Pode utilizá-lo para fins de teste.</span><span class="sxs-lookup"><span data-stu-id="6448a-133">You can use it for testing.</span></span>

## <a name="step-2-configure-hello-restful-api-claims-exchange-as-a-technical-profile-in-your-trustframeworextensionsxml-file"></a><span data-ttu-id="6448a-134">Passo 2: Configurar o exchange de afirmações de RESTful API Olá como um perfil no seu ficheiro TrustFrameworExtensions.xml técnico</span><span class="sxs-lookup"><span data-stu-id="6448a-134">Step 2: Configure hello RESTful API claims exchange as a technical profile in your TrustFrameworExtensions.xml file</span></span>

<span data-ttu-id="6448a-135">Um perfil técnico é a configuração completa do Olá do exchange Olá pretendido com Olá serviço RESTful.</span><span class="sxs-lookup"><span data-stu-id="6448a-135">A technical profile is hello full configuration of hello exchange desired with hello RESTful service.</span></span> <span data-ttu-id="6448a-136">Abrir o ficheiro de TrustFrameworkExtensions.xml Olá e adicione Olá seguinte fragmento XML dentro Olá `<ClaimsProvider>` elemento.</span><span class="sxs-lookup"><span data-stu-id="6448a-136">Open hello TrustFrameworkExtensions.xml file and add hello following XML snippet inside hello `<ClaimsProvider>` element.</span></span>

> [!NOTE]
> <span data-ttu-id="6448a-137">No Olá seguir XML, fornecedor RESTful `Version=1.0.0.0` será descrita como protocolo de Olá.</span><span class="sxs-lookup"><span data-stu-id="6448a-137">In hello following XML, RESTful provider `Version=1.0.0.0` is described as hello protocol.</span></span> <span data-ttu-id="6448a-138">Considere-lo como a função Olá que irá interagir com o serviço de Olá externo.</span><span class="sxs-lookup"><span data-stu-id="6448a-138">Consider it as hello function that will interact with hello external service.</span></span> <!-- TODO: A full definition of hello schema can be found...link tooRESTful Provider schema definition>-->

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

<span data-ttu-id="6448a-139">Olá `<InputClaims>` elemento define afirmações Olá que serão enviadas Olá serviço do IEF toohello REST.</span><span class="sxs-lookup"><span data-stu-id="6448a-139">hello `<InputClaims>` element defines hello claims that will be sent from hello IEF toohello REST service.</span></span> <span data-ttu-id="6448a-140">Neste exemplo, Olá conteúdos da afirmação Olá `givenName` será enviado serviço REST de toohello como afirmação Olá `email`.</span><span class="sxs-lookup"><span data-stu-id="6448a-140">In this example, hello contents of hello claim `givenName` will be sent toohello REST service as hello claim `email`.</span></span>  

<span data-ttu-id="6448a-141">Olá `<OutputClaims>` elemento define Olá afirmações que Olá IEF irá esperar do serviço REST de Olá.</span><span class="sxs-lookup"><span data-stu-id="6448a-141">hello `<OutputClaims>` element defines hello claims that hello IEF will expect from hello REST service.</span></span> <span data-ttu-id="6448a-142">Independentemente do número de Olá de afirmações que são recebidos, Olá IEF irá utilizar apenas os identificado aqui.</span><span class="sxs-lookup"><span data-stu-id="6448a-142">Regardless of hello number of claims that are received, hello IEF will use only those identified here.</span></span> <span data-ttu-id="6448a-143">Neste exemplo, uma afirmação recebida como `city` será chamada tooan mapeada IEF afirmação `city`.</span><span class="sxs-lookup"><span data-stu-id="6448a-143">In this example, a claim received as `city` will be mapped tooan IEF claim called `city`.</span></span>

## <a name="step-3-add-hello-new-claim-city-toohello-schema-of-your-trustframeworkextensionsxml-file"></a><span data-ttu-id="6448a-144">Passo 3: Adicionar nova afirmação de Olá `city` toohello esquema do ficheiro TrustFrameworkExtensions.xml</span><span class="sxs-lookup"><span data-stu-id="6448a-144">Step 3: Add hello new claim `city` toohello schema of your TrustFrameworkExtensions.xml file</span></span>

<span data-ttu-id="6448a-145">Olá afirmação `city` é ainda não definidos em qualquer lugar no nosso esquema.</span><span class="sxs-lookup"><span data-stu-id="6448a-145">hello claim `city` is not yet defined anywhere in our schema.</span></span> <span data-ttu-id="6448a-146">Por isso, adicione uma definição no interior do elemento de Olá `<BuildingBlocks>`.</span><span class="sxs-lookup"><span data-stu-id="6448a-146">So, add a definition inside hello element `<BuildingBlocks>`.</span></span> <span data-ttu-id="6448a-147">Pode encontrar este elemento de início de Olá do ficheiro de TrustFrameworkExtensions.xml Olá.</span><span class="sxs-lookup"><span data-stu-id="6448a-147">You can find this element at hello beginning of hello TrustFrameworkExtensions.xml file.</span></span>

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

## <a name="step-4-include-hello-rest-service-claims-exchange-as-an-orchestration-step-in-your-profile-edit-user-journey-in-trustframeworkextensionsxml"></a><span data-ttu-id="6448a-148">Passo 4: Incluir Olá REST serviço afirmações exchange como um passo de orquestração da sua perfil Editar utilizador viagem no TrustFrameworkExtensions.xml</span><span class="sxs-lookup"><span data-stu-id="6448a-148">Step 4: Include hello REST service claims exchange as an orchestration step in your profile edit user journey in TrustFrameworkExtensions.xml</span></span>

<span data-ttu-id="6448a-149">Adicione um passo toohello perfil Editar utilizador journey, depois do utilizador Olá foi autenticado (orchestration passos 1 a 4 olá seguir XML) e utilizador Olá forneceu informações de perfil Olá atualizado (passo 5).</span><span class="sxs-lookup"><span data-stu-id="6448a-149">Add a step toohello profile edit user journey, after hello user has been authenticated (orchestration steps 1-4 in hello following XML) and hello user has provided hello updated profile information (step 5).</span></span>

> [!NOTE]
> <span data-ttu-id="6448a-150">Existem muitos casos de utilização onde Olá chamada da REST API pode ser utilizado como um passo de orquestração.</span><span class="sxs-lookup"><span data-stu-id="6448a-150">There are many use cases where hello REST API call can be used as an orchestration step.</span></span> <span data-ttu-id="6448a-151">Como um passo de orquestração, pode ser utilizado como um sistema externo de tooan atualização depois de um utilizador foi concluída com êxito uma tarefa, como o registo da primeira vez ou como um perfil de atualizar informações de tookeep sincronizadas.</span><span class="sxs-lookup"><span data-stu-id="6448a-151">As an orchestration step, it can be used as an update tooan external system after a user has successfully completed a task like first-time registration, or as a profile update tookeep information synchronized.</span></span> <span data-ttu-id="6448a-152">Neste caso, é utilizado tooaugment informações de Olá fornecidas toohello aplicação depois de editar o perfil de Olá.</span><span class="sxs-lookup"><span data-stu-id="6448a-152">In this case, it's used tooaugment hello information provided toohello application after hello profile edit.</span></span>

<span data-ttu-id="6448a-153">Perfil de Olá cópia editar o código XML de journey de utilizador do ficheiro do Olá TrustFrameworkBase.xml ficheiro tooyour TrustFrameworkExtensions.xml dentro Olá `<UserJourneys>` elemento.</span><span class="sxs-lookup"><span data-stu-id="6448a-153">Copy hello profile edit user journey XML code from hello TrustFrameworkBase.xml file tooyour TrustFrameworkExtensions.xml file inside hello `<UserJourneys>` element.</span></span> <span data-ttu-id="6448a-154">Em seguida, efetue modificação de Olá no passo 6.</span><span class="sxs-lookup"><span data-stu-id="6448a-154">Then make hello modification under step 6.</span></span>

```XML
<OrchestrationStep Order="6" Type="ClaimsExchange">
    <ClaimsExchanges>
        <ClaimsExchange Id="GetLoyaltyData" TechnicalProfileReferenceId="AzureFunctions-LookUpLoyaltyWebHook" />
    </ClaimsExchanges>
</OrchestrationStep>
```

> [!IMPORTANT]
> <span data-ttu-id="6448a-155">Se a ordem de Olá não corresponde à sua versão, certifique-se de que inserir o código de Olá como passo Olá antes Olá `ClaimsExchange` tipo `SendClaims`.</span><span class="sxs-lookup"><span data-stu-id="6448a-155">If hello order does not match your version, make sure that you insert hello code as hello step before hello `ClaimsExchange` type `SendClaims`.</span></span>

<span data-ttu-id="6448a-156">Olá final XML para journey de utilizador Olá deve ter o seguinte aspeto:</span><span class="sxs-lookup"><span data-stu-id="6448a-156">hello final XML for hello user journey should look like this:</span></span>

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

## <a name="step-5-add-hello-claim-city-tooyour-relying-party-policy-file-so-hello-claim-is-sent-tooyour-application"></a><span data-ttu-id="6448a-157">Passo 5: Adicionar Olá afirmação `city` tooyour política da entidade confiadora do ficheiro para que a afirmação de Olá é enviada tooyour aplicação</span><span class="sxs-lookup"><span data-stu-id="6448a-157">Step 5: Add hello claim `city` tooyour relying party policy file so hello claim is sent tooyour application</span></span>

<span data-ttu-id="6448a-158">Edite o ficheiro do ProfileEdit.xml entidade confiadora (RP) de terceiros e modifique Olá `<TechnicalProfile Id="PolicyProfile">` seguinte do elemento tooadd Olá: `<OutputClaim ClaimTypeReferenceId="city" />`.</span><span class="sxs-lookup"><span data-stu-id="6448a-158">Edit your ProfileEdit.xml relying party (RP) file and modify hello `<TechnicalProfile Id="PolicyProfile">` element tooadd hello following: `<OutputClaim ClaimTypeReferenceId="city" />`.</span></span>

<span data-ttu-id="6448a-159">Depois de adicionar a nova afirmação de Olá, perfil técnica Olá este aspeto:</span><span class="sxs-lookup"><span data-stu-id="6448a-159">After you add hello new claim, hello technical profile looks like this:</span></span>

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

## <a name="step-6-upload-your-changes-and-test"></a><span data-ttu-id="6448a-160">Passo 6: Carregar as suas alterações e teste</span><span class="sxs-lookup"><span data-stu-id="6448a-160">Step 6: Upload your changes and test</span></span>

<span data-ttu-id="6448a-161">Substitua as versões existentes do Olá da política de Olá.</span><span class="sxs-lookup"><span data-stu-id="6448a-161">Overwrite hello existing versions of hello policy.</span></span>

1.  <span data-ttu-id="6448a-162">(Opcional:) Guarde versão existente Olá (transferindo) do seu ficheiro extensões antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="6448a-162">(Optional:) Save hello existing version (by downloading) of your extensions file before you proceed.</span></span> <span data-ttu-id="6448a-163">tookeep Olá inicial complexidade baixa, recomendamos que não carregar várias versões do ficheiro de extensões de Olá.</span><span class="sxs-lookup"><span data-stu-id="6448a-163">tookeep hello initial complexity low, we recommend that you do not upload multiple versions of hello extensions file.</span></span>
2.  <span data-ttu-id="6448a-164">(Opcional:) Mudar o nome da nova versão de Olá do ID de política de Olá para o ficheiro de edição de política de Olá alterando `PolicyId="B2C_1A_TrustFrameworkProfileEdit"`.</span><span class="sxs-lookup"><span data-stu-id="6448a-164">(Optional:) Rename hello new version of hello policy ID for hello policy edit file by changing   `PolicyId="B2C_1A_TrustFrameworkProfileEdit"`.</span></span>
3.  <span data-ttu-id="6448a-165">Carregar ficheiro de extensões de Olá.</span><span class="sxs-lookup"><span data-stu-id="6448a-165">Upload hello extensions file.</span></span>
4.  <span data-ttu-id="6448a-166">Carregue o ficheiro RP da edição de política de Olá.</span><span class="sxs-lookup"><span data-stu-id="6448a-166">Upload hello policy edit RP file.</span></span>
5.  <span data-ttu-id="6448a-167">Utilize **executar agora** política de Olá tootest.</span><span class="sxs-lookup"><span data-stu-id="6448a-167">Use **Run Now** tootest hello policy.</span></span> <span data-ttu-id="6448a-168">Token de Olá de revisão que Olá IEF devolve toohello aplicação.</span><span class="sxs-lookup"><span data-stu-id="6448a-168">Review hello token that hello IEF returns toohello application.</span></span>

<span data-ttu-id="6448a-169">Se tudo está configurado corretamente, o token de Olá irá incluir afirmação nova Olá `city`, com o valor de Olá `Redmond`.</span><span class="sxs-lookup"><span data-stu-id="6448a-169">If everything is set up correctly, hello token will include hello new claim `city`, with hello value `Redmond`.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="6448a-170">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="6448a-170">Next steps</span></span>

[<span data-ttu-id="6448a-171">Utilizar uma API REST como um passo de validação</span><span class="sxs-lookup"><span data-stu-id="6448a-171">Use a REST API as a validation step</span></span>](active-directory-b2c-rest-api-validation-custom.md)

[<span data-ttu-id="6448a-172">Modificar Olá perfil editar toogather informação adicional sobre os seus utilizadores</span><span class="sxs-lookup"><span data-stu-id="6448a-172">Modify hello profile edit toogather additional information from your users</span></span>](active-directory-b2c-create-custom-attributes-profile-edit-custom.md)
