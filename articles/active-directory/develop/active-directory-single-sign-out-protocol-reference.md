---
title: "aaaAzure início de sessão único limite protocolo SAML | Microsoft Docs"
description: "Este artigo descreve Olá único protocolo de SAML Sign-Out no Azure Active Directory"
services: active-directory
documentationcenter: .net
author: priyamohanram
manager: mbaldwin
editor: 
ms.assetid: 0e4aa75d-d1ad-4bde-a94c-d8a41fb0abe6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: priyamo
ms.custom: aaddev
ms.openlocfilehash: 889c9b3397a601c16ba6971d2b15bfee305576de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# Protocolo SAML fim de sessão único
Olá de suporte do Azure Active Directory (Azure AD) SAML 2.0 web browser único fim de sessão perfil. Para toowork fim de sessão único corretamente, Olá **LogoutURL** para aplicação Olá tem de ser explicitamente registada com o Azure AD durante o registo de aplicação. Azure AD utiliza os utilizadores do Olá LogoutURL tooredirect após são terminadas.

Este diagrama apresenta o fluxo de trabalho de Olá do processo de início de sessão único Olá do Azure AD.

![Início de sessão único o fluxo de trabalho](media/active-directory-single-sign-out-protocol-reference/active-directory-saml-single-sign-out-workflow.png)

## LogoutRequest
Olá nuvem serviço envia um `LogoutRequest` mensagem tooAzure AD tooindicate que uma sessão foi terminada. Olá excerpt seguinte mostra um exemplo `LogoutRequest` elemento.

```
<samlp:LogoutRequest xmlns="urn:oasis:names:tc:SAML:2.0:metadata" ID="idaa6ebe6839094fe4abc4ebd5281ec780" Version="2.0" IssueInstant="2013-03-28T07:10:49.6004822Z" xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol">
  <Issuer xmlns="urn:oasis:names:tc:SAML:2.0:assertion">https://www.workaad.com</Issuer>
  <NameID xmlns="urn:oasis:names:tc:SAML:2.0:assertion"> Uz2Pqz1X7pxe4XLWxV9KJQ+n59d573SepSAkuYKSde8=</NameID>
</samlp:LogoutRequest>
```

### LogoutRequest
Olá `LogoutRequest` tooAzure elemento enviado AD requer Olá seguintes atributos:

* `ID`: Este identifica o pedido de início de sessão Olá. Olá valor `ID` não devem começar com um número. prática típico Olá é tooappend **id** toohello representação de cadeia de um GUID.
* `Version`: Definir o valor de Olá deste elemento demasiado**2.0**. Este valor é preciso.
* `IssueInstant`: Este é um `DateTime` cadeia com um valor de hora Universal Coordenada (UTC) e [formato reportadas round-trip ("o")](https://msdn.microsoft.com/library/az4se3k1.aspx). Azure AD espera um valor deste tipo, mas não impõe.

### emissor
Olá `Issuer` elemento um `LogoutRequest` deve corresponder exatamente um dos Olá **ServicePrincipalNames** num serviço em nuvem de Olá no Azure AD. Normalmente, isto é definido toohello **URI de ID de aplicação** que é especificado durante o registo de aplicação.

### NameID
Olá, valor de Olá `NameID` elemento deve corresponder exatamente Olá `NameID` do utilizador Olá que está a ser terminada.

## LogoutResponse
Azure AD envia um `LogoutResponse` na resposta tooa `LogoutRequest` elemento. Olá excerpt seguinte mostra um exemplo `LogoutResponse`.

```
<samlp:LogoutResponse ID="_f0961a83-d071-4be5-a18c-9ae7b22987a4" Version="2.0" IssueInstant="2013-03-18T08:49:24.405Z" InResponseTo="iddce91f96e56747b5ace6d2e2aa9d4f8c" xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol">
  <Issuer xmlns="urn:oasis:names:tc:SAML:2.0:assertion">https://sts.windows.net/82869000-6ad1-48f0-8171-272ed18796e9/</Issuer>
  <samlp:Status>
    <samlp:StatusCode Value="urn:oasis:names:tc:SAML:2.0:status:Success" />
  </samlp:Status>
</samlp:LogoutResponse>
```

### LogoutResponse
Azure AD define Olá `ID`, `Version` e `IssueInstant` valores Olá `LogoutResponse` elemento. Também define Olá `InResponseTo` toohello o valor do elemento de Olá `ID` atributo de Olá `LogoutRequest` que elicited resposta Olá.

### emissor
Azure AD define este valor demasiado`https://login.microsoftonline.com/<TenantIdGUID>/` onde <TenantIdGUID> Olá inquilino ID do inquilino Olá do Azure AD.

valor Olá tooevaluate Olá `Issuer` elemento, utilize Olá valor Olá **URI de ID de aplicação** fornecido durante o registo de aplicação.

### Estado
Utiliza o Azure AD Olá `StatusCode` elemento Olá `Status` êxito do elemento tooindicate Olá ou a falha de início de sessão. Quando Olá fim de sessão tentativa falhar, hello `StatusCode` elemento também pode conter mensagens de erro personalizadas.
