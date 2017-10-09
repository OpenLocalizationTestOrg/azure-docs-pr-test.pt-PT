---
title: aaaAzure Active Directory Identity Protection - como utilizadores toounblock | Microsoft Docs
description: "Saiba como desbloquear utilizadores que foram bloqueados por uma política do Azure Active Directory Identity Protection."
services: active-directory
keywords: "proteção de identidade do Azure Active Directory, desbloquear utilizador"
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: a953d425-a3ef-41f8-a55d-0202c3f250a7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: cdda2808822888f76aa75cf46478738c94df51a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-identity-protection---how-toounblock-users"></a>Proteção do Azure Active Directory identidade - como toounblock utilizadores
Com o Azure Active Directory Identity Protection, pode configurar políticas tooblock utilizadores se Olá configurado condições forem satisfeitos. Normalmente, um utilizador bloqueado contactos ajuda para o suporte técnico toobecome desbloqueado. Este tópicos explica os passos de Olá pode efetuar toounblock um utilizador bloqueado.

## <a name="determine-hello-reason-for-blocking"></a>Determinar a razão de Olá para bloquear
Como um passo primeiro toounblock um utilizador, terá de tipo de Olá toodetermine de política que bloqueou utilizador Olá porque os passos seguintes são consoante no mesmo.
Com o Azure Active Directory Identity Protection, um utilizador pode ser está bloqueado por uma política de início de sessão risco ou uma política de risco do utilizador.

Pode obter o tipo de Olá de política que bloqueou um utilizador de cabeçalho de Olá na caixa de diálogo de Olá apresentado toohello utilizador durante a tentativa de início de sessão:

| Política | Caixa de diálogo utilizador |
| --- | --- |
| Risco de início de sessão |![O início de sessão bloqueado](./media/active-directory-identityprotection-unblock-howto/02.png) |
| Risco de utilizador |![Conta bloqueada](./media/active-directory-identityprotection-unblock-howto/104.png) |

Um utilizador que está bloqueado por:

* Uma política de início de sessão risco também é conhecido como o início de sessão suspeito
* Uma política de risco de utilizador também é conhecido como uma conta em risco

## <a name="unblocking-suspicious-sign-ins"></a>Desbloqueio suspeitos inícios de sessão
toounblock uma suspeita início de sessão, terá de Olá seguintes opções:

1. **Início de sessão de um dispositivo ou localização familiar** -um motivo comum bloqueados suspeitos inícios de sessão são tentativas de início de sessão de localizações desconhecidas ou dispositivos. Os utilizadores rapidamente podem determinar se se trata de Olá bloquear razão tentando toosign-in de localização familiar ou dispositivos.
2. **Excluir da política** - se considera que a configuração atual do Olá da sua política de início de sessão está a causar problemas para utilizadores específicos, pode excluir utilizadores Olá do mesmo. Consulte [do Azure Active Directory Identity Protection](active-directory-identityprotection.md) para obter mais detalhes.
3. **Desativar política** - se considera que a configuração de política está a causar problemas de todos os seus utilizadores, pode desativar a política de Olá. Consulte [do Azure Active Directory Identity Protection](active-directory-identityprotection.md) para obter mais detalhes.

## <a name="unblocking-accounts-at-risk"></a>Desbloqueio contas em risco
toounblock uma conta em risco, tiver Olá seguintes opções:

1. **Repor palavra-passe** -pode repor a palavra-passe do utilizador Olá. Consulte [reposição de palavra-passe segura manual](active-directory-identityprotection.md#manual-secure-password-reset) para obter mais detalhes.
2. **Ignore todos os eventos de risco** -política de risco do utilizador Olá bloqueia um utilizador se o nível de risco de utilizador Olá configurado para bloquear o acesso foi atingido. Pode reduzir a um utilizador do nível de risco fechando manualmente comunicadas eventos de risco. Para obter mais detalhes, consulte [fechar os eventos de risco manualmente](active-directory-identityprotection.md#closing-risk-events-manually).
3. **Excluir da política** - se considera que a configuração atual do Olá da sua política de início de sessão está a causar problemas para utilizadores específicos, pode excluir utilizadores Olá do mesmo. Consulte [do Azure Active Directory Identity Protection](active-directory-identityprotection.md) para obter mais detalhes.
4. **Desativar política** - se considera que a configuração de política está a causar problemas de todos os seus utilizadores, pode desativar a política de Olá. Consulte [do Azure Active Directory Identity Protection](active-directory-identityprotection.md) para obter mais detalhes.

## <a name="next-steps"></a>Passos seguintes
 Pretende tooknow mais sobre o Azure AD Identity Protection? Veja [do Azure Active Directory Identity Protection](active-directory-identityprotection.md).
