---
title: "Referência do protocolo SAML do AD de aaaAzure | Microsoft Docs"
description: "Este artigo fornece uma descrição geral dos perfis de Single Sign-On e única Sign-Out SAML Olá no Azure Active Directory."
services: active-directory
documentationcenter: .net
author: priyamohanram
manager: mbaldwin
editor: 
ms.assetid: 88125cfc-45c1-448b-9903-a629d8f31b01
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: priyamo
ms.openlocfilehash: d540b8cd9352e3196a0f4a40f0070d0e61127bee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# Como o Azure Active Directory utiliza o protocolo SAML Olá
Azure Active Directory (Azure AD) utiliza Olá SAML 2.0 protocolo tooenable aplicações tooprovide um início de sessão experiência tootheir utilizadores. Olá [Single Sign-On](active-directory-single-sign-on-protocol-reference.md) e [fim de sessão único](active-directory-single-sign-out-protocol-reference.md) perfis SAML do Azure AD explicam como SAML asserções, protocolos e enlaces são utilizados no serviço do fornecedor de identidade de Olá.

Protocolo SAML requer o fornecedor de identidade Olá (Azure AD) e Olá service provider (aplicação Olá) tooexchange obter informações sobre si próprios.

Quando uma aplicação for registada com o Azure AD, o programador da aplicação Olá regista informações relacionadas com a Federação com o Azure AD. Isto inclui Olá **URI de redirecionamento** da aplicação Olá.

Azure Active Directory expõe específicas do inquilino e comuns (independente de inquilino) único início de sessão e única fim de sessão pontos finais. Estes URLs representam localizações endereçáveis – não são apenas um identificadores –, pelo que pode aceder toohello endpoint tooread Olá metadados.

* ponto final de Olá inquilino específico está localizado em `https://login.microsoftonline.com/<TenantDomainName>/FederationMetadata/2007-06/FederationMetadata.xml`.  Olá <TenantDomainName> marcador de posição representa um nome de domínio registado ou o GUID de TenantID de um inquilino do Azure AD. Por exemplo, metadados de Federação Olá do inquilino de contoso.com Olá são: https://login.microsoftonline.com/contoso.com/FederationMetadata/2007-06/FederationMetadata.xml

* ponto final de Olá independente de inquilino está localizado em `https://login.microsoftonline.com/common/FederationMetadata/2007-06/FederationMetadata.xml`. Este endereço de ponto final, **comuns** for apresentada, em vez de um nome de domínio do inquilino ou um ID.

Para obter informações sobre os documentos de metadados da Federação Olá que publica do Azure AD, consulte [metadados da Federação](active-directory-federation-metadata.md).
