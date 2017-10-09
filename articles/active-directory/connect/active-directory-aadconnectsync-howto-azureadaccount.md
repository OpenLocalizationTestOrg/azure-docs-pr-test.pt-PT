---
title: "Sincronização do Azure AD Connect: como conta de serviço toomanage Olá do Azure AD | Microsoft Docs"
description: "Este tópico documenta como conta de serviço toorestore Olá do Azure AD."
services: active-directory
keywords: "AADSTS70002, AADSTS50054, como tooreset Olá palavra-passe para Olá sincronização do Azure AD Connect conta de serviço do conector"
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 6077043a-27f1-4304-a44b-81dc46620f24
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: e563518eae173de42a1d40bb5a76e63f29f9da42
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-how-toomanage-hello-azure-ad-service-account"></a>Sincronização do Azure AD Connect: como conta de serviço toomanage Olá do Azure AD
conta de serviço de Olá utilizada pelo conector do Azure AD de Olá deveria toobe serviço gratuito. Se precisar de tooreset as respetivas credenciais, em seguida, este tópico é que o utilizador. Por exemplo, se um Administrador Global tiver por erro reposição Olá palavra-passe na conta de serviço Olá através do PowerShell.

## <a name="reset-hello-credentials"></a>Repor as credenciais de Olá
Se a conta de serviço Olá definida na Olá conector do Azure AD não consegue contactar o Azure AD devido a problemas de tooauthentication, é possível repor a palavra-passe de Olá.

1. Inicie sessão no servidor de sincronização do Azure AD Connect toohello e inicie o PowerShell.
2. Execute `Add-ADSyncAADServiceAccount`.  
   ![Addadsyncaadserviceaccount de cmdlet do PowerShell](./media/active-directory-aadconnectsync-howto-azureadaccount/addadsyncaadserviceaccount.png)
3. Forneça as credenciais de Administrador Global do Azure AD.

Este cmdlet repõe Olá palavra-passe da conta de serviço Olá e atualizá-lo no Azure AD e no motor de sincronização de Olá.

## <a name="known-issues-these-steps-can-solve"></a>Estes passos podem resolver os problemas conhecidos
Esta secção se uma lista de erros comunicados pelos clientes que foram corrigidos por um credenciais repor em Olá conta de serviço do Azure AD.

- - -
Evento 6900  
servidor de Olá encontrou um erro inesperado ao processar uma notificação de alteração de palavra-passe:  
AADSTS70002: Erro a validar as credenciais. AADSTS50054: Palavra-passe antiga é utilizado para autenticação.

- - -
Evento 659  
Erro ao obter a configuração de sincronização da política de palavra-passe. Microsoft.IdentityModel.Clients.ActiveDirectory.AdalServiceException:  
AADSTS70002: Erro a validar as credenciais. AADSTS50054: Palavra-passe antiga é utilizado para autenticação.

## <a name="next-steps"></a>Passos seguintes
**Tópicos de descrição geral**

* [Sincronização do Azure AD Connect: Noções e personalizar a sincronização](active-directory-aadconnectsync-whatis.md)
* [Integrar as identidades no local ao Azure Active Directory](active-directory-aadconnect.md)

