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
# <a name="azure-active-directory-b2c-manage-sso-and-token-customization-with-custom-policies"></a>O Azure Active Directory B2C: Gerir o SSO e personalização token com as políticas personalizadas
Utilizar políticas personalizadas fornece que Olá mesmo controlo sobre o token, a sessão e o único configurações de início de sessão (SSO) como através de políticas incorporadas.  toolearn que cada definição faz, consulte a documentação de Olá [aqui](#active-directory-b2c-token-session-sso).

## <a name="token-lifetimes-and-claims-configuration"></a>Configuração de afirmações e durações token
definições de Olá toochange no seu token durações, terá de tooadd um `<ClaimsProviders>` elemento no ficheiro de entidade confiadora terceiros Olá da política de Olá pretende tooimpact.  Olá `<ClaimsProviders>` elemento é um subordinado de Olá `<TrustFrameworkPolicy>`.  No interior irá precisar de informações de Olá tooput que afeta as durações token.  Olá XML tem o seguinte aspeto:

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

**Durações de token de acesso** Olá acesso duração do token pode ser alterada modificando o valor Olá Olá `<Item>` com Olá chave = "token_lifetime_secs" em segundos.  valor predefinido Olá incorporado é 3600 segundos (60 minutos).

**Duração do token ID** duração do token Olá ID pode ser alterada modificando o valor Olá Olá `<Item>` com Olá chave = "id_token_lifetime_secs" em segundos.  valor predefinido Olá incorporado é 3600 segundos (60 minutos).

**Atualize a duração do token** duração do token Olá atualização pode ser alterada modificando o valor Olá Olá `<Item>` com Olá chave = "refresh_token_lifetime_secs" em segundos.  valor predefinido Olá incorporado é 1209600 segundos (14 dias).

**Atualizar o token duração de janela deslizante** se gostaria tooset um token de atualização de tooyour de duração da janela deslizante, modifique o valor de Olá dentro `<Item>` com Olá chave = "rolling_refresh_token_lifetime_secs" em segundos.  valor predefinido Olá incorporado é 7776000 (90 dias).  Se não quiser tooenfore um deslizante duração da janela, substitua esta linha com:
```XML
<Item Key="allow_infinite_rolling_refresh_token">True</Item>
```

**O emissor (iss) afirmação** se pretender que a afirmação de emissor (iss) toochange Olá, modifique o valor de Olá dentro Olá `<Item>` com Olá chave = "IssuanceClaimPattern".  os valores de aplicável Olá são `AuthorityAndTenantGuid` e `AuthorityWithTfp`.

**Definição que representa o ID de política de afirmações** Olá as opções para a definição deste valor são TFP (confiança da política de framework) e ACR (referência de contexto de autenticação).  
Iremos Recomendamos que defina esta tooTFP, toodo isto, certifique-se Olá `<Item>` com Olá chave = "AuthenticationContextReferenceClaimPattern" existe e está de valor de Olá `None`.
No seu `<OutputClaims>` item, adicione este elemento:
```XML
<OutputClaim ClaimTypeReferenceId="trustFrameworkPolicy" Required="true" DefaultValue="{policy}" />
```
Para o ACR, remova Olá `<Item>` com Olá chave = "AuthenticationContextReferenceClaimPattern".

**Requerente (sub) afirmação** esta opção é predefinidas tooObjectID, se desejar tooswitch isto demasiado`Not Supported`, Olá a seguir:

Substitua esta linha 
```XML
<OutputClaim ClaimTypeReferenceId="objectId" PartnerClaimType="sub" />
```
com esta linha:
```XML
<OutputClaim ClaimTypeReferenceId="sub" />
```

## <a name="session-behavior-and-sso"></a>Comportamento de sessão e SSO
toochange o comportamento de sessão e configurações de SSO, é necessário tooadd um `<UserJourneyBehaviors>` elemento dentro Olá `<RelyingParty>` elemento.  Olá `<UserJourneyBehaviors>` elemento tem de seguir imediato Olá `<DefaultUserJourney>`.  Olá dentro do seu `<UserJourneyBehavors>` elemento deve ter o seguinte aspeto:

```XML
<UserJourneyBehaviors>
   <SingleSignOn Scope="Application" />
   <SessionExpiryType>Absolute</SessionExpiryType>
   <SessionExpiryInSeconds>86400</SessionExpiryInSeconds>
</UserJourneyBehaviors>
```
**Configuração início de sessão único (SSO)** toochange Olá configuração única de início de sessão, terá de valor Olá toomodify `<SingleSignOn>`.  os valores de aplicável Olá são `Tenant`, `Application`, `Policy` e `Disabled`. 

**Aplicação Web duração de sessão (minutos)** toochange Olá Olá web app duração de sessão, terá de valor toomodify Olá `<SessionExpiryInSeconds>` elemento.  valor predefinido de Olá nas políticas incorporadas é segundos 86400 (1440 minutos).

**Tempo limite de sessão de aplicação Web** toochange Olá web app tempo limite da sessão, terá de valor Olá toomodify `<SessionExpiryType>`.  os valores de aplicável Olá são `Absolute` e `Rolling`.
