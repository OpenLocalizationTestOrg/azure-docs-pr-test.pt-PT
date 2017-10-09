---
title: "aaaAzure AD camadas de segurança de palavra-passe | Microsoft Docs"
description: "Explica a forma como os do Azure AD impõe palavras-passe seguras e protege as palavras-passe de utilizadores de criminals informático,"
services: active-directory
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: joflore
ms.openlocfilehash: 10d8b600d9f4c02355b2cd8c5dccf8505aaf210d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="a-multi-tiered-approach-tooazure-ad-password-security"></a>Uma abordagem de várias camadas tooAzure AD palavra-passe de segurança

Este artigo aborda algumas melhores práticas que pode seguir como um utilizador ou como um administrador tooprotect seu Azure Active Directory (Azure AD) ou Account Microsoft.

 > [!NOTE]
 > Os administradores do AD do Azure podem repor palavras-passe de utilizador utilizando a orientação de Olá artigo Olá [Olá da reposição de palavra-passe de um utilizador no Azure Active Directory](active-directory-users-reset-password-azure-portal.md).
 >
 > Os utilizadores podem repor a sua própria palavra-passe utilizando a orientação de Olá artigo Olá [ajuda esqueci minha palavra-passe do Azure AD](active-directory-passwords-update-your-own-password.md).
 >

## <a name="password-requirements"></a>Requisitos de palavra-passe

Azure AD incorpora Olá seguir comuns abordagens toosecuring as palavras-passe:

* Requisitos de comprimento de palavras-passe
* Requisitos de complexidade de palavra-passe
* Expiração de palavras-passe regular e periódica

Para obter informações sobre a reposição no Azure Active Directory palavra-passe, consulte o tópico de Olá [passe self-service do Azure AD ' Repor para Olá profissional de TI](active-directory-passwords.md).

## <a name="azure-ad-password-protections"></a>Proteções de palavra-passe do Azure AD

Azure AD e Olá sistema de contas Microsoft utilizar da indústria comprovada se aproxima tooensure proteção segura de utilizador e administrador de palavras-passe, incluindo:

* Palavras-passe banidas dinamicamente
* Smart Password Lockout

Para informações sobre a gestão de palavra-passe com base na investigação atual, consulte o documento de Olá [orientações de palavra-passe](http://aka.ms/passwordguidance).

### <a name="dynamically-banned-passwords"></a>Palavras-passe banidas dinamicamente

Azure AD e Accounts Microsoft salvaguardar proteção de palavra-passe por dinamicamente banning palavras-passe utilizadas frequentemente. equipa de proteção de identidade do Azure ID Olá analisa regularmente listas banned palavra-passe, impedir que os utilizadores a seleção de palavras-passe utilizadas frequentemente. Este serviço é tooAzure disponível AD e os clientes de serviço da conta Microsoft hello.

Ao criar palavras-passe, é importante para os administradores tooencourage utilizadores toochoose palavra-passe expressões que incluam uma combinação de letras, números, carateres ou palavras exclusivos. Esta abordagem ajuda toomake utilizador as palavras-passe toobe praticamente impossível comprometido, mas é mais fácil para os utilizadores tooremember.

#### <a name="password-breaches"></a>Falhas de palavra-passe

Microsoft está a trabalhar sempre toostay um passo à frente das criminals informático.

equipa do Azure AD Identity Protection Olá continuamente analisa as palavras-passe que são frequentemente utilizadas. Informático criminals utilizam também semelhante estratégias tooinform os seus ataques, como criar um [tabela rainbow](https://en.wikipedia.org/wiki/Rainbow_table) para cracking hashes de palavra-passe.

A Microsoft continuamente analisa [falhas de dados](https://www.privacyrights.org/data-breaches) toomaintain uma lista de palavra-passe de banned dinamicamente atualizada, que garante que as palavras-passe vulnerável são banned antes de ficarem um real da ameaça tooAzure AD clientes. Para obter mais informações sobre a nossa esforços de segurança atual, consulte Olá [Microsoft segurança Intelligence relatório](https://www.microsoft.com/security/sir/default.aspx).

### <a name="smart-password-lockout"></a>Smart Password Lockout

Quando o Azure AD Deteta uma potencial toohack de tentar informático criminal para uma palavra-passe do utilizador, iremos bloquear a conta de utilizador de Olá com inteligente de palavra-passe de bloqueio. Azure AD foi concebido risco de Olá toodetermine associado sessões de início de sessão específica. Em seguida, utilizando os dados de segurança mais atualizadas à sua Olá, iremos aplicar ameaças do bloqueio semântica toostop informático.

Se um utilizador está bloqueado fora do Azure AD, o seu ecrã procura toohello semelhante que se segue:

  ![Bloqueado do Azure AD](./media/active-directory-secure-passwords/locked-out-azuread.png)

Para outras contas Microsoft, o seu ecrã procura toohello semelhante que se segue:

  ![Bloqueado de uma conta Microsoft](./media/active-directory-secure-passwords/locked-out-ms-accounts.png)

Para obter informações sobre a reposição no Azure Active Directory palavra-passe, consulte o tópico de Olá [passe self-service do Azure AD ' Repor para Olá profissional de TI](active-directory-passwords.md).

  >[!NOTE]
  >Se for um administrador do Azure AD, poderá ser útil toouse [Windows Hello](https://www.microsoft.com/windows/windows-hello) tooavoid ter aos utilizadores criar palavras-passe tradicional completamente.
  >

## <a name="next-steps"></a>Passos seguintes

* [Como tooupdate a própria palavra-passe](active-directory-passwords-update-your-own-password.md)
* [Olá Noções básicas de gestão de identidades do Azure](fundamentals-identity.md)
* [Atividade de reposição de relatório na palavra-passe](active-directory-passwords-reporting.md)


