---
title: "O Azure Active Directory B2C: Gerir o SSO e personalização token com as políticas personalizadas | Microsoft Docs"
description: 
services: active-directory-b2c
documentationcenter: 
author: sama
ms.assetid: eec4d418-453f-4755-8b30-5ed997841b56
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 05/02/2017
ms.author: sama
ms.openlocfilehash: b65271a22c77ea41eeec2126e4a3ad24364edd17
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-manage-sso-and-token-customization-with-custom-policies"></a><span data-ttu-id="bf85a-102">O Azure Active Directory B2C: Gerir o SSO e personalização token com as políticas personalizadas</span><span class="sxs-lookup"><span data-stu-id="bf85a-102">Azure Active Directory B2C: Manage SSO and token customization with custom policies</span></span>
<span data-ttu-id="bf85a-103">Utilizar políticas personalizadas fornece que Olá mesmo controlo sobre o token, a sessão e o único configurações de início de sessão (SSO) como através de políticas incorporadas.</span><span class="sxs-lookup"><span data-stu-id="bf85a-103">Using custom policies provides you hello same control over your token, session and single sign-on (SSO) configurations as through built-in policies.</span></span>  <span data-ttu-id="bf85a-104">toolearn que cada definição faz, consulte a documentação de Olá [aqui](#active-directory-b2c-token-session-sso).</span><span class="sxs-lookup"><span data-stu-id="bf85a-104">toolearn what each setting does, please see hello documentation [here](#active-directory-b2c-token-session-sso).</span></span>

## <a name="token-lifetimes-and-claims-configuration"></a><span data-ttu-id="bf85a-105">Configuração de afirmações e durações token</span><span class="sxs-lookup"><span data-stu-id="bf85a-105">Token lifetimes and claims configuration</span></span>
<span data-ttu-id="bf85a-106">definições de Olá toochange no seu token durações, terá de tooadd um `<ClaimsProviders>` elemento no ficheiro de entidade confiadora terceiros Olá da política de Olá pretende tooimpact.</span><span class="sxs-lookup"><span data-stu-id="bf85a-106">toochange hello settings on your token lifetimes, you need tooadd a `<ClaimsProviders>` element in hello relying party file of hello policy you want tooimpact.</span></span>  <span data-ttu-id="bf85a-107">Olá `<ClaimsProviders>` elemento é um subordinado de Olá `<TrustFrameworkPolicy>`.</span><span class="sxs-lookup"><span data-stu-id="bf85a-107">hello `<ClaimsProviders>` element is a child of hello `<TrustFrameworkPolicy>`.</span></span>  <span data-ttu-id="bf85a-108">No interior irá precisar de informações de Olá tooput que afeta as durações token.</span><span class="sxs-lookup"><span data-stu-id="bf85a-108">Inside you'll need tooput hello information that affects your token lifetimes.</span></span>  <span data-ttu-id="bf85a-109">Olá XML tem o seguinte aspeto:</span><span class="sxs-lookup"><span data-stu-id="bf85a-109">hello XML looks like this:</span></span>

```XML
<ClaimsProviders>
   <ClaimsProvider>
      <DisplayName>Token Issuer</DisplayName>
      <TechnicalProfiles>
         <TechnicalProfile Id="JwtIssuer">
            <Metadata>
               <Item Key="token_lifetime_secs">3600</Item>
               <Item Key="id_token_lifetime_secs">3600</Item>
               <Item Key="refresh_token_lifetime_secs">1209600</Item>
               <Item Key="rolling_refresh_token_lifetime_secs">7776000</Item>
               <Item Key="IssuanceClaimPattern">AuthorityAndTenantGuid</Item>
               <Item Key="AuthenticationContextReferenceClaimPattern">None</Item>
            </Metadata>
         </TechnicalProfile>
      </TechnicalProfiles>
   </ClaimsProvider>
</ClaimsProviders>
```

<span data-ttu-id="bf85a-110">**Durações de token de acesso** Olá acesso duração do token pode ser alterada modificando o valor Olá Olá `<Item>` com Olá chave = "token_lifetime_secs" em segundos.</span><span class="sxs-lookup"><span data-stu-id="bf85a-110">**Access token lifetimes** hello access token lifetime can be changed by modifying hello value inside hello `<Item>` with hello Key="token_lifetime_secs" in seconds.</span></span>  <span data-ttu-id="bf85a-111">valor predefinido Olá incorporado é 3600 segundos (60 minutos).</span><span class="sxs-lookup"><span data-stu-id="bf85a-111">hello default value in built-in is 3600 seconds (60 minutes).</span></span>

<span data-ttu-id="bf85a-112">**Duração do token ID** duração do token Olá ID pode ser alterada modificando o valor Olá Olá `<Item>` com Olá chave = "id_token_lifetime_secs" em segundos.</span><span class="sxs-lookup"><span data-stu-id="bf85a-112">**ID token lifetime** hello ID token lifetime can be changed by modifying hello value inside hello `<Item>` with hello Key="id_token_lifetime_secs" in seconds.</span></span>  <span data-ttu-id="bf85a-113">valor predefinido Olá incorporado é 3600 segundos (60 minutos).</span><span class="sxs-lookup"><span data-stu-id="bf85a-113">hello default value in built-in is 3600 seconds (60 minutes).</span></span>

<span data-ttu-id="bf85a-114">**Atualize a duração do token** duração do token Olá atualização pode ser alterada modificando o valor Olá Olá `<Item>` com Olá chave = "refresh_token_lifetime_secs" em segundos.</span><span class="sxs-lookup"><span data-stu-id="bf85a-114">**Refresh token lifetime** hello refresh token lifetime can be changed by modifying hello value inside hello `<Item>` with hello Key="refresh_token_lifetime_secs" in seconds.</span></span>  <span data-ttu-id="bf85a-115">valor predefinido Olá incorporado é 1209600 segundos (14 dias).</span><span class="sxs-lookup"><span data-stu-id="bf85a-115">hello default value in built-in is 1209600 seconds (14 days).</span></span>

<span data-ttu-id="bf85a-116">**Atualizar o token duração de janela deslizante** se gostaria tooset um token de atualização de tooyour de duração da janela deslizante, modifique o valor de Olá dentro `<Item>` com Olá chave = "rolling_refresh_token_lifetime_secs" em segundos.</span><span class="sxs-lookup"><span data-stu-id="bf85a-116">**Refresh token sliding window lifetime** If you would like tooset a sliding window lifetime tooyour refresh token, modify hello value inside `<Item>` with hello Key="rolling_refresh_token_lifetime_secs" in seconds.</span></span>  <span data-ttu-id="bf85a-117">valor predefinido Olá incorporado é 7776000 (90 dias).</span><span class="sxs-lookup"><span data-stu-id="bf85a-117">hello default value in built-in is 7776000 (90 days).</span></span>  <span data-ttu-id="bf85a-118">Se não quiser tooenfore um deslizante duração da janela, substitua esta linha com:</span><span class="sxs-lookup"><span data-stu-id="bf85a-118">If you don't want tooenfore a sliding window lifetime, replace this line with:</span></span>
```XML
<Item Key="allow_infinite_rolling_refresh_token">True</Item>
```

<span data-ttu-id="bf85a-119">**O emissor (iss) afirmação** se pretender que a afirmação de emissor (iss) toochange Olá, modifique o valor de Olá dentro Olá `<Item>` com Olá chave = "IssuanceClaimPattern".</span><span class="sxs-lookup"><span data-stu-id="bf85a-119">**Issuer (iss) claim** If you want toochange hello Issuer (iss) claim, modify hello value inside hello `<Item>` with hello Key="IssuanceClaimPattern".</span></span>  <span data-ttu-id="bf85a-120">os valores de aplicável Olá são `AuthorityAndTenantGuid` e `AuthorityWithTfp`.</span><span class="sxs-lookup"><span data-stu-id="bf85a-120">hello applicable values are `AuthorityAndTenantGuid` and `AuthorityWithTfp`.</span></span>

<span data-ttu-id="bf85a-121">**Definição que representa o ID de política de afirmações** Olá as opções para a definição deste valor são TFP (confiança da política de framework) e ACR (referência de contexto de autenticação).</span><span class="sxs-lookup"><span data-stu-id="bf85a-121">**Setting claim representing policy ID** hello options for setting this value are TFP (trust framework policy) and ACR (authentication context reference).</span></span>  
<span data-ttu-id="bf85a-122">Iremos Recomendamos que defina esta tooTFP, toodo isto, certifique-se Olá `<Item>` com Olá chave = "AuthenticationContextReferenceClaimPattern" existe e está de valor de Olá `None`.</span><span class="sxs-lookup"><span data-stu-id="bf85a-122">We recommend setting this tooTFP, toodo this, ensure hello `<Item>` with hello Key="AuthenticationContextReferenceClaimPattern" exists and hello value is `None`.</span></span>
<span data-ttu-id="bf85a-123">No seu `<OutputClaims>` item, adicione este elemento:</span><span class="sxs-lookup"><span data-stu-id="bf85a-123">In your `<OutputClaims>` item, add this element:</span></span>
```XML
<OutputClaim ClaimTypeReferenceId="trustFrameworkPolicy" Required="true" DefaultValue="{policy}" />
```
<span data-ttu-id="bf85a-124">Para o ACR, remova Olá `<Item>` com Olá chave = "AuthenticationContextReferenceClaimPattern".</span><span class="sxs-lookup"><span data-stu-id="bf85a-124">For ACR, remove hello `<Item>` with hello Key="AuthenticationContextReferenceClaimPattern".</span></span>

<span data-ttu-id="bf85a-125">**Requerente (sub) afirmação** esta opção é predefinidas tooObjectID, se desejar tooswitch isto demasiado`Not Supported`, Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="bf85a-125">**Subject (sub) claim** This option is defaulted tooObjectID, if you would like tooswitch this too`Not Supported`, do hello following:</span></span>

<span data-ttu-id="bf85a-126">Substitua esta linha</span><span class="sxs-lookup"><span data-stu-id="bf85a-126">Replace this line</span></span> 
```XML
<OutputClaim ClaimTypeReferenceId="objectId" PartnerClaimType="sub" />
```
<span data-ttu-id="bf85a-127">com esta linha:</span><span class="sxs-lookup"><span data-stu-id="bf85a-127">with this line:</span></span>
```XML
<OutputClaim ClaimTypeReferenceId="sub" />
```

## <a name="session-behavior-and-sso"></a><span data-ttu-id="bf85a-128">Comportamento de sessão e SSO</span><span class="sxs-lookup"><span data-stu-id="bf85a-128">Session behavior and SSO</span></span>
<span data-ttu-id="bf85a-129">toochange o comportamento de sessão e configurações de SSO, é necessário tooadd um `<UserJourneyBehaviors>` elemento dentro Olá `<RelyingParty>` elemento.</span><span class="sxs-lookup"><span data-stu-id="bf85a-129">toochange your session behavior and SSO configurations, you need tooadd a `<UserJourneyBehaviors>` element inside of hello `<RelyingParty>` element.</span></span>  <span data-ttu-id="bf85a-130">Olá `<UserJourneyBehaviors>` elemento tem de seguir imediato Olá `<DefaultUserJourney>`.</span><span class="sxs-lookup"><span data-stu-id="bf85a-130">hello `<UserJourneyBehaviors>` element must immediately follow hello `<DefaultUserJourney>`.</span></span>  <span data-ttu-id="bf85a-131">Olá dentro do seu `<UserJourneyBehavors>` elemento deve ter o seguinte aspeto:</span><span class="sxs-lookup"><span data-stu-id="bf85a-131">hello inside of your `<UserJourneyBehavors>` element should look like this:</span></span>

```XML
<UserJourneyBehaviors>
   <SingleSignOn Scope="Application" />
   <SessionExpiryType>Absolute</SessionExpiryType>
   <SessionExpiryInSeconds>86400</SessionExpiryInSeconds>
</UserJourneyBehaviors>
```
<span data-ttu-id="bf85a-132">**Configuração início de sessão único (SSO)** toochange Olá configuração única de início de sessão, terá de valor Olá toomodify `<SingleSignOn>`.</span><span class="sxs-lookup"><span data-stu-id="bf85a-132">**Single sign-on (SSO) configuration** toochange hello single sign-on configuration, you need toomodify hello value of `<SingleSignOn>`.</span></span>  <span data-ttu-id="bf85a-133">os valores de aplicável Olá são `Tenant`, `Application`, `Policy` e `Disabled`.</span><span class="sxs-lookup"><span data-stu-id="bf85a-133">hello applicable values are `Tenant`, `Application`, `Policy` and `Disabled`.</span></span> 

<span data-ttu-id="bf85a-134">**Aplicação Web duração de sessão (minutos)** toochange Olá Olá web app duração de sessão, terá de valor toomodify Olá `<SessionExpiryInSeconds>` elemento.</span><span class="sxs-lookup"><span data-stu-id="bf85a-134">**Web app session lifetime (minutes)** toochange hello hello web app session lifetime, you need toomodify value of hello `<SessionExpiryInSeconds>` element.</span></span>  <span data-ttu-id="bf85a-135">valor predefinido de Olá nas políticas incorporadas é segundos 86400 (1440 minutos).</span><span class="sxs-lookup"><span data-stu-id="bf85a-135">hello default value in built-in policies is 86400 seconds (1440 minutes).</span></span>

<span data-ttu-id="bf85a-136">**Tempo limite de sessão de aplicação Web** toochange Olá web app tempo limite da sessão, terá de valor Olá toomodify `<SessionExpiryType>`.</span><span class="sxs-lookup"><span data-stu-id="bf85a-136">**Web app session timeout** toochange hello web app session timeout, you need toomodify hello value of `<SessionExpiryType>`.</span></span>  <span data-ttu-id="bf85a-137">os valores de aplicável Olá são `Absolute` e `Rolling`.</span><span class="sxs-lookup"><span data-stu-id="bf85a-137">hello applicable values are `Absolute` and `Rolling`.</span></span>
