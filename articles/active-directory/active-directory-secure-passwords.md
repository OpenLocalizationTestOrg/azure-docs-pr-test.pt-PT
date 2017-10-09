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
# <a name="a-multi-tiered-approach-tooazure-ad-password-security"></a><span data-ttu-id="b27f6-103">Uma abordagem de várias camadas tooAzure AD palavra-passe de segurança</span><span class="sxs-lookup"><span data-stu-id="b27f6-103">A multi-tiered approach tooAzure AD password security</span></span>

<span data-ttu-id="b27f6-104">Este artigo aborda algumas melhores práticas que pode seguir como um utilizador ou como um administrador tooprotect seu Azure Active Directory (Azure AD) ou Account Microsoft.</span><span class="sxs-lookup"><span data-stu-id="b27f6-104">This article discusses some best practices you can follow as a user or as an administrator tooprotect your Azure Active Directory (Azure AD) or Microsoft Account.</span></span>

 > [!NOTE]
 > <span data-ttu-id="b27f6-105">Os administradores do AD do Azure podem repor palavras-passe de utilizador utilizando a orientação de Olá artigo Olá [Olá da reposição de palavra-passe de um utilizador no Azure Active Directory](active-directory-users-reset-password-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="b27f6-105">Azure AD administrators can reset user passwords using hello guidance in hello article [Reset hello password for a user in Azure Active Directory](active-directory-users-reset-password-azure-portal.md).</span></span>
 >
 > <span data-ttu-id="b27f6-106">Os utilizadores podem repor a sua própria palavra-passe utilizando a orientação de Olá artigo Olá [ajuda esqueci minha palavra-passe do Azure AD](active-directory-passwords-update-your-own-password.md).</span><span class="sxs-lookup"><span data-stu-id="b27f6-106">Users can reset their own password using hello guidance in hello article [Help I forgot my Azure AD password](active-directory-passwords-update-your-own-password.md).</span></span>
 >

## <a name="password-requirements"></a><span data-ttu-id="b27f6-107">Requisitos de palavra-passe</span><span class="sxs-lookup"><span data-stu-id="b27f6-107">Password requirements</span></span>

<span data-ttu-id="b27f6-108">Azure AD incorpora Olá seguir comuns abordagens toosecuring as palavras-passe:</span><span class="sxs-lookup"><span data-stu-id="b27f6-108">Azure AD incorporates hello following common approaches toosecuring passwords:</span></span>

* <span data-ttu-id="b27f6-109">Requisitos de comprimento de palavras-passe</span><span class="sxs-lookup"><span data-stu-id="b27f6-109">Password length requirements</span></span>
* <span data-ttu-id="b27f6-110">Requisitos de complexidade de palavra-passe</span><span class="sxs-lookup"><span data-stu-id="b27f6-110">Password complexity requirements</span></span>
* <span data-ttu-id="b27f6-111">Expiração de palavras-passe regular e periódica</span><span class="sxs-lookup"><span data-stu-id="b27f6-111">Regular and periodic password expiration</span></span>

<span data-ttu-id="b27f6-112">Para obter informações sobre a reposição no Azure Active Directory palavra-passe, consulte o tópico de Olá [passe self-service do Azure AD ' Repor para Olá profissional de TI](active-directory-passwords.md).</span><span class="sxs-lookup"><span data-stu-id="b27f6-112">For information about password reset in Azure Active Directory, see hello topic [Azure AD self-service password reset for hello IT professional](active-directory-passwords.md).</span></span>

## <a name="azure-ad-password-protections"></a><span data-ttu-id="b27f6-113">Proteções de palavra-passe do Azure AD</span><span class="sxs-lookup"><span data-stu-id="b27f6-113">Azure AD password protections</span></span>

<span data-ttu-id="b27f6-114">Azure AD e Olá sistema de contas Microsoft utilizar da indústria comprovada se aproxima tooensure proteção segura de utilizador e administrador de palavras-passe, incluindo:</span><span class="sxs-lookup"><span data-stu-id="b27f6-114">Azure AD and hello Microsoft Account System use industry proven approaches tooensure secure protection of user and administrator passwords including:</span></span>

* <span data-ttu-id="b27f6-115">Palavras-passe banidas dinamicamente</span><span class="sxs-lookup"><span data-stu-id="b27f6-115">Dynamically banned passwords</span></span>
* <span data-ttu-id="b27f6-116">Smart Password Lockout</span><span class="sxs-lookup"><span data-stu-id="b27f6-116">Smart Password Lockout</span></span>

<span data-ttu-id="b27f6-117">Para informações sobre a gestão de palavra-passe com base na investigação atual, consulte o documento de Olá [orientações de palavra-passe](http://aka.ms/passwordguidance).</span><span class="sxs-lookup"><span data-stu-id="b27f6-117">For information about password management based on current research, see hello whitepaper [Password Guidance](http://aka.ms/passwordguidance).</span></span>

### <a name="dynamically-banned-passwords"></a><span data-ttu-id="b27f6-118">Palavras-passe banidas dinamicamente</span><span class="sxs-lookup"><span data-stu-id="b27f6-118">Dynamically banned passwords</span></span>

<span data-ttu-id="b27f6-119">Azure AD e Accounts Microsoft salvaguardar proteção de palavra-passe por dinamicamente banning palavras-passe utilizadas frequentemente.</span><span class="sxs-lookup"><span data-stu-id="b27f6-119">Azure AD and Microsoft Accounts safeguard password protection by dynamically banning commonly used passwords.</span></span> <span data-ttu-id="b27f6-120">equipa de proteção de identidade do Azure ID Olá analisa regularmente listas banned palavra-passe, impedir que os utilizadores a seleção de palavras-passe utilizadas frequentemente.</span><span class="sxs-lookup"><span data-stu-id="b27f6-120">hello Azure ID Identity Protection team routinely analyzes banned password lists, preventing users from selecting commonly used passwords.</span></span> <span data-ttu-id="b27f6-121">Este serviço é tooAzure disponível AD e os clientes de serviço da conta Microsoft hello.</span><span class="sxs-lookup"><span data-stu-id="b27f6-121">This service is available tooAzure AD and hello Microsoft Account Service customers.</span></span>

<span data-ttu-id="b27f6-122">Ao criar palavras-passe, é importante para os administradores tooencourage utilizadores toochoose palavra-passe expressões que incluam uma combinação de letras, números, carateres ou palavras exclusivos.</span><span class="sxs-lookup"><span data-stu-id="b27f6-122">When creating passwords, it is important for administrators tooencourage users toochoose password phrases that include a unique combination of letters, numbers, characters, or words.</span></span> <span data-ttu-id="b27f6-123">Esta abordagem ajuda toomake utilizador as palavras-passe toobe praticamente impossível comprometido, mas é mais fácil para os utilizadores tooremember.</span><span class="sxs-lookup"><span data-stu-id="b27f6-123">This approach helps toomake user passwords nearly impossible toobe compromised but easier for users tooremember.</span></span>

#### <a name="password-breaches"></a><span data-ttu-id="b27f6-124">Falhas de palavra-passe</span><span class="sxs-lookup"><span data-stu-id="b27f6-124">Password breaches</span></span>

<span data-ttu-id="b27f6-125">Microsoft está a trabalhar sempre toostay um passo à frente das criminals informático.</span><span class="sxs-lookup"><span data-stu-id="b27f6-125">Microsoft is always working toostay one step ahead of cyber-criminals.</span></span>

<span data-ttu-id="b27f6-126">equipa do Azure AD Identity Protection Olá continuamente analisa as palavras-passe que são frequentemente utilizadas.</span><span class="sxs-lookup"><span data-stu-id="b27f6-126">hello Azure AD Identity Protection team continually analyzes passwords that are commonly used.</span></span> <span data-ttu-id="b27f6-127">Informático criminals utilizam também semelhante estratégias tooinform os seus ataques, como criar um [tabela rainbow](https://en.wikipedia.org/wiki/Rainbow_table) para cracking hashes de palavra-passe.</span><span class="sxs-lookup"><span data-stu-id="b27f6-127">Cyber-criminals also use similar strategies tooinform their attacks, such as building a [rainbow table](https://en.wikipedia.org/wiki/Rainbow_table) for cracking password hashes.</span></span>

<span data-ttu-id="b27f6-128">A Microsoft continuamente analisa [falhas de dados](https://www.privacyrights.org/data-breaches) toomaintain uma lista de palavra-passe de banned dinamicamente atualizada, que garante que as palavras-passe vulnerável são banned antes de ficarem um real da ameaça tooAzure AD clientes.</span><span class="sxs-lookup"><span data-stu-id="b27f6-128">Microsoft continually analyzes [data breaches](https://www.privacyrights.org/data-breaches) toomaintain a dynamically updated banned password list, which ensures that vulnerable passwords are banned before they become a real threat tooAzure AD customers.</span></span> <span data-ttu-id="b27f6-129">Para obter mais informações sobre a nossa esforços de segurança atual, consulte Olá [Microsoft segurança Intelligence relatório](https://www.microsoft.com/security/sir/default.aspx).</span><span class="sxs-lookup"><span data-stu-id="b27f6-129">For more information about our current security efforts, see hello [Microsoft Security Intelligence Report](https://www.microsoft.com/security/sir/default.aspx).</span></span>

### <a name="smart-password-lockout"></a><span data-ttu-id="b27f6-130">Smart Password Lockout</span><span class="sxs-lookup"><span data-stu-id="b27f6-130">Smart Password Lockout</span></span>

<span data-ttu-id="b27f6-131">Quando o Azure AD Deteta uma potencial toohack de tentar informático criminal para uma palavra-passe do utilizador, iremos bloquear a conta de utilizador de Olá com inteligente de palavra-passe de bloqueio.</span><span class="sxs-lookup"><span data-stu-id="b27f6-131">When Azure AD detects a potential cyber-criminal trying toohack into a user password, we lock hello user account with Smart Password Lockout.</span></span> <span data-ttu-id="b27f6-132">Azure AD foi concebido risco de Olá toodetermine associado sessões de início de sessão específica.</span><span class="sxs-lookup"><span data-stu-id="b27f6-132">Azure AD is designed toodetermine hello risk associated with specific login sessions.</span></span> <span data-ttu-id="b27f6-133">Em seguida, utilizando os dados de segurança mais atualizadas à sua Olá, iremos aplicar ameaças do bloqueio semântica toostop informático.</span><span class="sxs-lookup"><span data-stu-id="b27f6-133">Then using hello most up-to-date security data, we apply lockout semantics toostop cyber threats.</span></span>

<span data-ttu-id="b27f6-134">Se um utilizador está bloqueado fora do Azure AD, o seu ecrã procura toohello semelhante que se segue:</span><span class="sxs-lookup"><span data-stu-id="b27f6-134">If a user is locked out of Azure AD, their screen looks similar toohello one that follows:</span></span>

  ![Bloqueado do Azure AD](./media/active-directory-secure-passwords/locked-out-azuread.png)

<span data-ttu-id="b27f6-136">Para outras contas Microsoft, o seu ecrã procura toohello semelhante que se segue:</span><span class="sxs-lookup"><span data-stu-id="b27f6-136">For other Microsoft accounts, their screen looks similar toohello one that follows:</span></span>

  ![Bloqueado de uma conta Microsoft](./media/active-directory-secure-passwords/locked-out-ms-accounts.png)

<span data-ttu-id="b27f6-138">Para obter informações sobre a reposição no Azure Active Directory palavra-passe, consulte o tópico de Olá [passe self-service do Azure AD ' Repor para Olá profissional de TI](active-directory-passwords.md).</span><span class="sxs-lookup"><span data-stu-id="b27f6-138">For information about password reset in Azure Active Directory, see hello topic [Azure AD self-service password reset for hello IT professional](active-directory-passwords.md).</span></span>

  >[!NOTE]
  ><span data-ttu-id="b27f6-139">Se for um administrador do Azure AD, poderá ser útil toouse [Windows Hello](https://www.microsoft.com/windows/windows-hello) tooavoid ter aos utilizadores criar palavras-passe tradicional completamente.</span><span class="sxs-lookup"><span data-stu-id="b27f6-139">If you are an Azure AD administrator, you may want toouse [Windows Hello](https://www.microsoft.com/windows/windows-hello) tooavoid having your users create traditional passwords altogether.</span></span>
  >

## <a name="next-steps"></a><span data-ttu-id="b27f6-140">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="b27f6-140">Next steps</span></span>

* [<span data-ttu-id="b27f6-141">Como tooupdate a própria palavra-passe</span><span class="sxs-lookup"><span data-stu-id="b27f6-141">How tooupdate your own password</span></span>](active-directory-passwords-update-your-own-password.md)
* [<span data-ttu-id="b27f6-142">Olá Noções básicas de gestão de identidades do Azure</span><span class="sxs-lookup"><span data-stu-id="b27f6-142">hello fundamentals of Azure identity management</span></span>](fundamentals-identity.md)
* [<span data-ttu-id="b27f6-143">Atividade de reposição de relatório na palavra-passe</span><span class="sxs-lookup"><span data-stu-id="b27f6-143">Report on password reset activity</span></span>](active-directory-passwords-reporting.md)


