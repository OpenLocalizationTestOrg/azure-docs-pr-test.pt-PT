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
# <a name="walkthrough-integrate-rest-api-claims-exchanges-in-your-azure-ad-b2c-user-journey-as-validation-on-user-input"></a><span data-ttu-id="3b54e-103">Instruções: Integrar o REST API trocas de afirmações da sua viagem do Azure AD B2C utilizador como validação no intervenção do utilizador</span><span class="sxs-lookup"><span data-stu-id="3b54e-103">Walkthrough: Integrate REST API claims exchanges in your Azure AD B2C user journey as validation on user input</span></span>

<span data-ttu-id="3b54e-104">Olá identidade experiência Framework (IEF) subjacente do Azure Active Directory B2C (Azure AD B2C) permite Olá identidade programador toointegrate uma interação com uma API RESTful em journey um utilizador.</span><span class="sxs-lookup"><span data-stu-id="3b54e-104">hello Identity Experience Framework (IEF) that underlies Azure Active Directory B2C (Azure AD B2C) enables hello identity developer toointegrate an interaction with a RESTful API in a user journey.</span></span>  

<span data-ttu-id="3b54e-105">No final de Olá destas instruções, será capaz de toocreate um journey de utilizador do Azure AD B2C que interage com os serviços RESTful.</span><span class="sxs-lookup"><span data-stu-id="3b54e-105">At hello end of this walkthrough, you will be able toocreate an Azure AD B2C user journey that interacts with RESTful services.</span></span>

<span data-ttu-id="3b54e-106">Olá IEF envia os dados em afirmações e recebe dados novamente nas afirmações.</span><span class="sxs-lookup"><span data-stu-id="3b54e-106">hello IEF sends data in claims and receives data back in claims.</span></span> <span data-ttu-id="3b54e-107">interação de Olá com Olá API:</span><span class="sxs-lookup"><span data-stu-id="3b54e-107">hello interaction with hello API:</span></span>

- <span data-ttu-id="3b54e-108">Pode ser estruturada como uma troca de afirmações de REST API ou como um perfil de validação, o que acontece no interior de um passo de orquestração.</span><span class="sxs-lookup"><span data-stu-id="3b54e-108">Can be designed as a REST API claims exchange or as a validation profile, which happens inside an orchestration step.</span></span>
- <span data-ttu-id="3b54e-109">Normalmente, valida a entrada de utilizador de Olá.</span><span class="sxs-lookup"><span data-stu-id="3b54e-109">Typically validates input from hello user.</span></span> <span data-ttu-id="3b54e-110">Se o valor de Olá de utilizador de Olá é rejeitado, o utilizador Olá pode tentar novamente tooenter um valor válido com Olá oportunidade tooreturn uma mensagem de erro.</span><span class="sxs-lookup"><span data-stu-id="3b54e-110">If hello value from hello user is rejected, hello user can try again tooenter a valid value with hello opportunity tooreturn an error message.</span></span>

<span data-ttu-id="3b54e-111">Também pode conceber interação Olá como um passo de orquestração.</span><span class="sxs-lookup"><span data-stu-id="3b54e-111">You can also design hello interaction as an orchestration step.</span></span> <span data-ttu-id="3b54e-112">Para obter mais informações, consulte [explicação passo a passo: trocas da sua do Azure AD B2C utilizador viagem como um passo de orquestração de afirmações de integrar o API de REST](active-directory-b2c-rest-api-step-custom.md).</span><span class="sxs-lookup"><span data-stu-id="3b54e-112">For more information, see [Walkthrough: Integrate REST API claims exchanges in your Azure AD B2C user journey as an orchestration step](active-directory-b2c-rest-api-step-custom.md).</span></span>

<span data-ttu-id="3b54e-113">Por exemplo de perfil de validação de Olá, utilizaremos journey do Olá perfil Editar utilizador no ficheiro de pacote de arranque Olá ProfileEdit.xml.</span><span class="sxs-lookup"><span data-stu-id="3b54e-113">For hello validation profile example, we will use hello profile edit user journey in hello starter pack file ProfileEdit.xml.</span></span>

<span data-ttu-id="3b54e-114">Verificar a esse nome Olá fornecido pelo utilizador Olá no perfil de Olá editar não faz parte de uma lista de exclusão.</span><span class="sxs-lookup"><span data-stu-id="3b54e-114">We can verify that hello name provided by hello user in hello profile edit is not part of an exclusion list.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3b54e-115">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="3b54e-115">Prerequisites</span></span>

- <span data-ttu-id="3b54e-116">Um toocomplete de configurado de inquilino do Azure AD B2C uma conta local sessão-up/início de sessão, conforme descrito em [introdução](active-directory-b2c-get-started-custom.md).</span><span class="sxs-lookup"><span data-stu-id="3b54e-116">An Azure AD B2C tenant configured toocomplete a local account sign-up/sign-in, as described in [Getting started](active-directory-b2c-get-started-custom.md).</span></span>
- <span data-ttu-id="3b54e-117">Um ponto final de REST API é toointeract com.</span><span class="sxs-lookup"><span data-stu-id="3b54e-117">A REST API endpoint toointeract with.</span></span> <span data-ttu-id="3b54e-118">Nestas instruções, configurámos um site de demonstração chamado [WingTipGames](https://wingtipgamesb2c.azurewebsites.net/) com um serviço de REST API.</span><span class="sxs-lookup"><span data-stu-id="3b54e-118">For this walkthrough, we've set up a demo site called [WingTipGames](https://wingtipgamesb2c.azurewebsites.net/) with a REST API service.</span></span>

## <a name="step-1-prepare-hello-rest-api-function"></a><span data-ttu-id="3b54e-119">Passo 1: Preparar a função de REST API de Olá</span><span class="sxs-lookup"><span data-stu-id="3b54e-119">Step 1: Prepare hello REST API function</span></span>

> [!NOTE]
> <span data-ttu-id="3b54e-120">A configuração de funções de API de REST está fora do âmbito de Olá deste artigo.</span><span class="sxs-lookup"><span data-stu-id="3b54e-120">Setup of REST API functions is outside hello scope of this article.</span></span> <span data-ttu-id="3b54e-121">[As funções do Azure](https://docs.microsoft.com/azure/azure-functions/functions-reference) fornece uma excelente toolkit toocreate serviços RESTful na nuvem de Olá.</span><span class="sxs-lookup"><span data-stu-id="3b54e-121">[Azure Functions](https://docs.microsoft.com/azure/azure-functions/functions-reference) provides an excellent toolkit toocreate RESTful services in hello cloud.</span></span>

<span data-ttu-id="3b54e-122">Criámos uma função do Azure que recebe uma afirmação que se espera como `playerTag`.</span><span class="sxs-lookup"><span data-stu-id="3b54e-122">We have created an Azure function that receives a claim that it expects as `playerTag`.</span></span> <span data-ttu-id="3b54e-123">a função Olá valida se esta afirmação existe.</span><span class="sxs-lookup"><span data-stu-id="3b54e-123">hello function validates whether this claim exists.</span></span> <span data-ttu-id="3b54e-124">Pode aceder ao código de função do Azure completa Olá no [GitHub](https://github.com/Azure-Samples/active-directory-b2c-advanced-policies/tree/master/AzureFunctionsSamples).</span><span class="sxs-lookup"><span data-stu-id="3b54e-124">You can access hello complete Azure function code in [GitHub](https://github.com/Azure-Samples/active-directory-b2c-advanced-policies/tree/master/AzureFunctionsSamples).</span></span>

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

<span data-ttu-id="3b54e-125">Olá IEF espera Olá `userMessage` afirmação devolve esse Olá função do Azure.</span><span class="sxs-lookup"><span data-stu-id="3b54e-125">hello IEF expects hello `userMessage` claim that hello Azure function returns.</span></span> <span data-ttu-id="3b54e-126">Esta afirmação será apresentada como um utilizador de toohello de cadeia se a validação de Olá falhar, por exemplo, quando um Estado de 409 conflito é devolvido em Olá anterior exemplo.</span><span class="sxs-lookup"><span data-stu-id="3b54e-126">This claim will be presented as a string toohello user if hello validation fails, such as when a 409 conflict status is returned in hello preceding example.</span></span>

## <a name="step-2-configure-hello-restful-api-claims-exchange-as-a-technical-profile-in-your-trustframeworkextensionsxml-file"></a><span data-ttu-id="3b54e-127">Passo 2: Configurar o exchange de afirmações de RESTful API Olá como um perfil no seu ficheiro TrustFrameworkExtensions.xml técnico</span><span class="sxs-lookup"><span data-stu-id="3b54e-127">Step 2: Configure hello RESTful API claims exchange as a technical profile in your TrustFrameworkExtensions.xml file</span></span>

<span data-ttu-id="3b54e-128">Um perfil técnico é a configuração completa do Olá do exchange Olá pretendido com Olá serviço RESTful.</span><span class="sxs-lookup"><span data-stu-id="3b54e-128">A technical profile is hello full configuration of hello exchange desired with hello RESTful service.</span></span> <span data-ttu-id="3b54e-129">Abrir o ficheiro de TrustFrameworkExtensions.xml Olá e adicione Olá seguinte fragmento XML dentro Olá `<ClaimsProviders>` elemento.</span><span class="sxs-lookup"><span data-stu-id="3b54e-129">Open hello TrustFrameworkExtensions.xml file and add hello following XML snippet inside hello `<ClaimsProviders>` element.</span></span>

> [!NOTE]
> <span data-ttu-id="3b54e-130">No Olá seguir XML, fornecedor RESTful `Version=1.0.0.0` será descrita como protocolo de Olá.</span><span class="sxs-lookup"><span data-stu-id="3b54e-130">In hello following XML, RESTful provider `Version=1.0.0.0` is described as hello protocol.</span></span> <span data-ttu-id="3b54e-131">Considere-lo como a função Olá que irá interagir com o serviço de Olá externo.</span><span class="sxs-lookup"><span data-stu-id="3b54e-131">Consider it as hello function that will interact with hello external service.</span></span> <!-- TODO: A full definition of hello schema can be found...link tooRESTful Provider schema definition>-->

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

<span data-ttu-id="3b54e-132">Olá `InputClaims` elemento define afirmações Olá que serão enviadas Olá serviço do IEF toohello REST.</span><span class="sxs-lookup"><span data-stu-id="3b54e-132">hello `InputClaims` element defines hello claims that will be sent from hello IEF toohello REST service.</span></span> <span data-ttu-id="3b54e-133">Neste exemplo, Olá conteúdos da afirmação Olá `givenName` serão enviados toohello o serviço REST como `playerTag`.</span><span class="sxs-lookup"><span data-stu-id="3b54e-133">In this example, hello contents of hello claim `givenName` will be sent toohello REST service as `playerTag`.</span></span> <span data-ttu-id="3b54e-134">Neste exemplo, Olá que IEF não espera afirmações novamente.</span><span class="sxs-lookup"><span data-stu-id="3b54e-134">In this example, hello IEF does not expect claims back.</span></span> <span data-ttu-id="3b54e-135">Em vez disso, aguarda para uma resposta do serviço REST de Olá e atos baseados em códigos de estado de Olá que recebe.</span><span class="sxs-lookup"><span data-stu-id="3b54e-135">Instead, it waits for a response from hello REST service and acts based on hello status codes that it receives.</span></span>

## <a name="step-3-include-hello-restful-service-claims-exchange-in-self-asserted-technical-profile-where-you-want-toovalidate-hello-user-input"></a><span data-ttu-id="3b54e-136">Passo 3: Incluem Olá serviço RESTful afirmações exchange no perfil técnica automática permitido onde pretende intervenção do utilizador toovalidate Olá</span><span class="sxs-lookup"><span data-stu-id="3b54e-136">Step 3: Include hello RESTful service claims exchange in self-asserted technical profile where you want toovalidate hello user input</span></span>

<span data-ttu-id="3b54e-137">Olá mais comuns a utilização do passo de validação de Olá está no interação Olá com um utilizador.</span><span class="sxs-lookup"><span data-stu-id="3b54e-137">hello most common use of hello validation step is in hello interaction with a user.</span></span> <span data-ttu-id="3b54e-138">Todas as interações onde o utilizador Olá é tooprovide esperado de entrada são *automática permitido perfis técnicas*.</span><span class="sxs-lookup"><span data-stu-id="3b54e-138">All interactions where hello user is expected tooprovide input are *self-asserted technical profiles*.</span></span> <span data-ttu-id="3b54e-139">Neste exemplo, iremos adicionar perfil técnica de Olá validação toohello Self Asserted ProfileUpdate.</span><span class="sxs-lookup"><span data-stu-id="3b54e-139">For this example, we will add hello validation toohello Self-Asserted-ProfileUpdate technical profile.</span></span> <span data-ttu-id="3b54e-140">Este é Olá perfil técnica que Olá ficheiro da política de entidade confiadora (RP) de terceiros `Profile Edit` utiliza.</span><span class="sxs-lookup"><span data-stu-id="3b54e-140">This is hello technical profile that hello relying party (RP) policy file `Profile Edit` uses.</span></span>

<span data-ttu-id="3b54e-141">Olá de tooadd afirmações exchange toohello automática permitido técnica perfil:</span><span class="sxs-lookup"><span data-stu-id="3b54e-141">tooadd hello claims exchange toohello self-asserted technical profile:</span></span>

1. <span data-ttu-id="3b54e-142">Abra o ficheiro de TrustFrameworkBase.xml Olá e procure `<TechnicalProfile Id="SelfAsserted-ProfileUpdate">`.</span><span class="sxs-lookup"><span data-stu-id="3b54e-142">Open hello TrustFrameworkBase.xml file and search for `<TechnicalProfile Id="SelfAsserted-ProfileUpdate">`.</span></span>
2. <span data-ttu-id="3b54e-143">Reveja a configuração de Olá deste perfil técnica.</span><span class="sxs-lookup"><span data-stu-id="3b54e-143">Review hello configuration of this technical profile.</span></span> <span data-ttu-id="3b54e-144">Observe como o exchange Olá com utilizador Olá está definido como afirmações que serão pedidas ao utilizador Olá (afirmações de entrada) e as afirmações que serão esperadas novamente a partir do fornecedor de Self-permitido Olá (afirmações de saída).</span><span class="sxs-lookup"><span data-stu-id="3b54e-144">Observe how hello exchange with hello user is defined as claims that will be asked of hello user (input claims) and claims that will be expected back from hello self-asserted provider (output claims).</span></span>
3. <span data-ttu-id="3b54e-145">Procurar `TechnicalProfileReferenceId="SelfAsserted-ProfileUpdate`e tenha em atenção que este perfil é invocado como orchestration passo 6 `<UserJourney Id="ProfileEdit">`.</span><span class="sxs-lookup"><span data-stu-id="3b54e-145">Search for `TechnicalProfileReferenceId="SelfAsserted-ProfileUpdate`, and notice that this profile is invoked as orchestration step 6 of `<UserJourney Id="ProfileEdit">`.</span></span>

## <a name="step-4-upload-and-test-hello-profile-edit-rp-policy-file"></a><span data-ttu-id="3b54e-146">Passo 4: Carregar e testar o ficheiro de política do Olá perfil editar RP</span><span class="sxs-lookup"><span data-stu-id="3b54e-146">Step 4: Upload and test hello profile edit RP policy file</span></span>

1. <span data-ttu-id="3b54e-147">Carregar a versão nova do Olá do ficheiro de TrustFrameworkExtensions.xml Olá.</span><span class="sxs-lookup"><span data-stu-id="3b54e-147">Upload hello new version of hello TrustFrameworkExtensions.xml file.</span></span>
2. <span data-ttu-id="3b54e-148">Utilize **executar agora** perfil de Olá tootest editar o ficheiro de política RP.</span><span class="sxs-lookup"><span data-stu-id="3b54e-148">Use **Run now** tootest hello profile edit RP policy file.</span></span>
3. <span data-ttu-id="3b54e-149">Teste de validação de Olá, fornecendo um dos nomes de Olá existente (por exemplo, mcvinny) num Olá **o nome fornecido** campo.</span><span class="sxs-lookup"><span data-stu-id="3b54e-149">Test hello validation by providing one of hello existing names (for example, mcvinny) in hello **Given Name** field.</span></span> <span data-ttu-id="3b54e-150">Se tudo está configurado corretamente, deverá receber uma mensagem que notifica o utilizador Olá que tag de leitor de Olá já está a ser utilizado.</span><span class="sxs-lookup"><span data-stu-id="3b54e-150">If everything is set up correctly, you should receive a message that notifies hello user that hello player tag is already used.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3b54e-151">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="3b54e-151">Next steps</span></span>

[<span data-ttu-id="3b54e-152">Modificar Olá perfil utilizador e editar registo toogather informação adicional sobre os seus utilizadores</span><span class="sxs-lookup"><span data-stu-id="3b54e-152">Modify hello profile edit and user registration toogather additional information from your users</span></span>](active-directory-b2c-create-custom-attributes-profile-edit-custom.md)

[<span data-ttu-id="3b54e-153">Instruções: Integrar o REST API trocas de afirmações da sua viagem do Azure AD B2C utilizador como um passo de orquestração</span><span class="sxs-lookup"><span data-stu-id="3b54e-153">Walkthrough: Integrate REST API claims exchanges in your Azure AD B2C user journey as an orchestration step</span></span>](active-directory-b2c-rest-api-step-custom.md)
