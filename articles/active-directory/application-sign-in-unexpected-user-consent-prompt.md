---
title: "pedido de consentimento de aaaUnexpected quando iniciar sessão na aplicação tooan | Microsoft Docs"
description: "Como tootroubleshoot quando um utilizador verá um pedido de consentimento para uma aplicação tiver integrado com o Azure AD que não era esperado"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 32b7a5e6256faee0dcfe2e1644da3d3428812d35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="unexpected-consent-prompt-when-signing-in-tooan-application"></a>Pedido de consentimento inesperado quando iniciar sessão na aplicação tooan

Muitas aplicações que se integram com o Azure Active Directory requerem recursos toovarious permissões toorun de ordem. Quando estes recursos também estão integrados no Azure Active Directory, tooaccess permissões-lhes é pedida utilizando Olá do Azure AD consentimento framework. 

Isto resulta num pedido de consentimento a ser mostrado Olá pela primeira vez que é utilizada uma aplicação, que é, muitas vezes, uma operação única. 

## <a name="scenarios-in-which-users-see-consent-prompts"></a>Cenários em que os utilizadores veem consentimento dos avisos

Avisos adicionais podem ser esperados em vários cenários:

* Olá de permissões necessárias pela aplicação Olá ter alterado.

* Olá utilizador autorizado originalmente toohello aplicação não era um administrador e agora um utilizador diferente (não-administrador) está a utilizar a aplicação de Olá Olá pela primeira vez.

* Olá utilizador autorizado originalmente toohello aplicação foi um administrador, mas não consentimento em nome da organização inteira Olá.

* está a utilizar a aplicação Olá [consentimento incremental e dinâmico](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-compare#incremental-and-dynamic-consent) toorequest permissões adicionais depois de consentimento inicialmente foi concedido. Isto é frequentemente utilizado quando funcionalidades opcionais de uma aplicação adicional requerem permissões para além daquelas necessário para a funcionalidade de linha de base.

* Consentimento foi revogado depois de ser concedido inicialmente.

* Programador Olá configurou Olá aplicação toorequire um pedido de consentimento sempre que é utilizada (Nota: não é recomendado).

## <a name="next-steps"></a>Passos seguintes

-   [As aplicações, permissões e consentimento no Azure Active Directory (v 1.0 ponto final)](https://docs.microsoft.com/azure/active-directory/active-directory-apps-permissions-consent)

-   [Âmbitos, permissões e consentimento no Olá Azure Active Directory (ponto final v 2.0)](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes)


