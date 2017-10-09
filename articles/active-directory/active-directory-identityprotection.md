---
title: "aaaAzure proteção de identidade do Active Directory | Microsoft Docs"
description: "Saiba como do Azure AD Identity Protection permite-lhe capacidade de Olá toolimit de tooexploit um atacante uma identidade comprometida ou dispositivo e toosecure uma identidade ou um dispositivo que anteriormente estava toobe conhecido ou potencialmente comprometido."
services: active-directory
keywords: "proteção de identidade do Azure Active Directory, o cloud app discovery, gestão de aplicações, segurança, risco, nível de risco, vulnerabilidade, política de segurança"
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: e7434eeb-4e98-4b6b-a895-b5598a6cccf1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: ecca4f3cdb65585687cf44a80024f26c7cab22ca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-identity-protection"></a><span data-ttu-id="ee71c-104">Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="ee71c-104">Azure Active Directory Identity Protection</span></span>

<span data-ttu-id="ee71c-105">Azure Active Directory Identity Protection é uma funcionalidade de edição de Olá, Azure AD Premium P2 que lhe permite:</span><span class="sxs-lookup"><span data-stu-id="ee71c-105">Azure Active Directory Identity Protection is a feature of hello Azure AD Premium P2 edition that enables you to:</span></span>

- <span data-ttu-id="ee71c-106">Detetar potenciais vulnerabilidades que afetam as identidades da organização</span><span class="sxs-lookup"><span data-stu-id="ee71c-106">Detect potential vulnerabilities affecting your organization’s identities</span></span>

- <span data-ttu-id="ee71c-107">Configurar respostas automáticas toodetected suspeita ações que são identidades da organização tooyour relacionados</span><span class="sxs-lookup"><span data-stu-id="ee71c-107">Configure automated responses toodetected suspicious actions that are related tooyour organization’s identities</span></span>  

- <span data-ttu-id="ee71c-108">Investigar incidentes suspeitas e tome as medidas adequadas tooresolve-las</span><span class="sxs-lookup"><span data-stu-id="ee71c-108">Investigate suspicious incidents and take appropriate action tooresolve them</span></span>   


## <a name="getting-started"></a><span data-ttu-id="ee71c-109">Introdução</span><span class="sxs-lookup"><span data-stu-id="ee71c-109">Getting started</span></span>

<span data-ttu-id="ee71c-110">Microsoft protege identidades baseado na nuvem para a mais do que um decade.</span><span class="sxs-lookup"><span data-stu-id="ee71c-110">Microsoft secures cloud-based identities for more than a decade.</span></span> <span data-ttu-id="ee71c-111">Com o Azure Active Directory Identity Protection, no seu ambiente, pode utilizar Olá sistemas de proteção mesmo Microsoft utiliza toosecure identidades.</span><span class="sxs-lookup"><span data-stu-id="ee71c-111">With Azure Active Directory Identity Protection, in your environment, you can use hello same protection systems Microsoft uses toosecure identities.</span></span>

<span data-ttu-id="ee71c-112">Coloque vasta maioria de Olá de tomar de falhas de segurança quando os atacantes ganham ambiente de tooan acesso roubo de identidade do utilizador.</span><span class="sxs-lookup"><span data-stu-id="ee71c-112">hello vast majority of security breaches take place when attackers gain access tooan environment by stealing a user’s identity.</span></span> <span data-ttu-id="ee71c-113">Ao longo de anos Olá, os atacantes tem tornar-se cada vez mais eficientes tirar partido das violações de terceiros e utilização de ataques de phishing sofisticadas.</span><span class="sxs-lookup"><span data-stu-id="ee71c-113">Over hello years, attackers have become increasingly effective in leveraging third party breaches and using sophisticated phishing attacks.</span></span> <span data-ttu-id="ee71c-114">Assim que um atacante obtiver acesso a contas de utilizador com privilégios baixa tooeven, é relativamente fácil para os mesmos toogain aceder tooimportant a recursos empresariais através de movimento lateral.</span><span class="sxs-lookup"><span data-stu-id="ee71c-114">As soon as an attacker gains access tooeven low privileged user accounts, it is relatively easy for them toogain access tooimportant company resources through lateral movement.</span></span>

<span data-ttu-id="ee71c-115">Como consequência, tem de:</span><span class="sxs-lookup"><span data-stu-id="ee71c-115">As a consequence of this, you need to:</span></span>

- <span data-ttu-id="ee71c-116">Proteger todas as identidades independentemente do respetivo nível de privilégios</span><span class="sxs-lookup"><span data-stu-id="ee71c-116">Protect all identities regardless of their privilege level</span></span>

- <span data-ttu-id="ee71c-117">Proativamente impedir identidades comprometidas que está a ser abused</span><span class="sxs-lookup"><span data-stu-id="ee71c-117">Proactively prevent compromised identities from being abused</span></span>

<span data-ttu-id="ee71c-118">Detetar identidades comprometidas não é nenhuma tarefa fácil.</span><span class="sxs-lookup"><span data-stu-id="ee71c-118">Discovering compromised identities is no easy task.</span></span> <span data-ttu-id="ee71c-119">Azure Active Directory utiliza adaptável algoritmos de aprendizagem automática e anomalias de toodetect heurística e incidentes suspeitas que indiquem potencialmente comprometido identidades.</span><span class="sxs-lookup"><span data-stu-id="ee71c-119">Azure Active Directory uses adaptive machine learning algorithms and heuristics toodetect anomalies and suspicious incidents that indicate potentially compromised identities.</span></span> <span data-ttu-id="ee71c-120">Utilizando estes dados, Identity Protection gera relatórios e alertas que permitem Olá tooevaluate detetados problemas e demorar mitigação adequada ou ações de remediação.</span><span class="sxs-lookup"><span data-stu-id="ee71c-120">Using this data, Identity Protection generates reports and alerts that enable you tooevaluate hello detected issues and take appropriate mitigation or remediation actions.</span></span>

<span data-ttu-id="ee71c-121">Azure Active Directory Identity Protection é maior do que uma monitorização e a ferramenta de relatórios.</span><span class="sxs-lookup"><span data-stu-id="ee71c-121">Azure Active Directory Identity Protection is more than a monitoring and reporting tool.</span></span> <span data-ttu-id="ee71c-122">tooprotect as identidades da organização, pode configurar as políticas baseadas em risco que respondam automaticamente toodetected problemas quando for atingido a um nível de risco especificado.</span><span class="sxs-lookup"><span data-stu-id="ee71c-122">tooprotect your organization's identities, you can configure risk-based policies that automatically respond toodetected issues when a specified risk level has been reached.</span></span> <span data-ttu-id="ee71c-123">Estas políticas, além disso tooother condicional aceder controlos fornecidos pelo Azure Active Directory e o EMS, pode bloquear automaticamente ou iniciar ações de remediação adaptável incluindo reposições de palavra-passe e de imposição de autenticação multifator.</span><span class="sxs-lookup"><span data-stu-id="ee71c-123">These policies, in addition tooother conditional access controls provided by Azure Active Directory and EMS, can either automatically block or initiate adaptive remediation actions including password resets and multi-factor authentication enforcement.</span></span>


#### <a name="identity-protection-capabilities"></a><span data-ttu-id="ee71c-124">Capacidades de proteção de identidade</span><span class="sxs-lookup"><span data-stu-id="ee71c-124">Identity Protection capabilities</span></span>

<span data-ttu-id="ee71c-125">**Detetar vulnerabilidades e contas de risco:**</span><span class="sxs-lookup"><span data-stu-id="ee71c-125">**Detecting vulnerabilities and risky accounts:**</span></span>  

* <span data-ttu-id="ee71c-126">Fornecer recomendações personalizado tooimprove geral postura de segurança por realce vulnerabilidades</span><span class="sxs-lookup"><span data-stu-id="ee71c-126">Providing custom recommendations tooimprove overall security posture by highlighting vulnerabilities</span></span>
* <span data-ttu-id="ee71c-127">A calcular níveis de risco de início de sessão</span><span class="sxs-lookup"><span data-stu-id="ee71c-127">Calculating sign-in risk levels</span></span>
* <span data-ttu-id="ee71c-128">A calcular níveis de risco do utilizador</span><span class="sxs-lookup"><span data-stu-id="ee71c-128">Calculating user risk levels</span></span>


<span data-ttu-id="ee71c-129">**Investigar os eventos de risco:**</span><span class="sxs-lookup"><span data-stu-id="ee71c-129">**Investigating risk events:**</span></span>

* <span data-ttu-id="ee71c-130">Enviar notificações para eventos de risco</span><span class="sxs-lookup"><span data-stu-id="ee71c-130">Sending notifications for risk events</span></span>
* <span data-ttu-id="ee71c-131">Investigar os eventos de risco utilizando informações relevantes e contextuais</span><span class="sxs-lookup"><span data-stu-id="ee71c-131">Investigating risk events using relevant and contextual information</span></span>
* <span data-ttu-id="ee71c-132">Fornecer as investigações de tootrack de fluxos de trabalho básicos</span><span class="sxs-lookup"><span data-stu-id="ee71c-132">Providing basic workflows tootrack investigations</span></span>
* <span data-ttu-id="ee71c-133">Fornecer acesso fácil tooremediation ações, como a reposição de palavra-passe</span><span class="sxs-lookup"><span data-stu-id="ee71c-133">Providing easy access tooremediation actions such as password reset</span></span>

<span data-ttu-id="ee71c-134">**Políticas de acesso condicional baseado em risco:**</span><span class="sxs-lookup"><span data-stu-id="ee71c-134">**Risk-based conditional access policies:**</span></span>

* <span data-ttu-id="ee71c-135">Política toomitigate arriscados inícios de sessão por bloquear inícios de sessão ou exigindo desafios de autenticação multifator.</span><span class="sxs-lookup"><span data-stu-id="ee71c-135">Policy toomitigate risky sign-ins by blocking sign-ins or requiring multi-factor authentication challenges.</span></span>
* <span data-ttu-id="ee71c-136">Política tooblock ou contas de utilizador de risco segura</span><span class="sxs-lookup"><span data-stu-id="ee71c-136">Policy tooblock or secure risky user accounts</span></span>
* <span data-ttu-id="ee71c-137">Política toorequire utilizadores tooregister para autenticação multifator</span><span class="sxs-lookup"><span data-stu-id="ee71c-137">Policy toorequire users tooregister for multi-factor authentication</span></span>



## <a name="identity-protection-roles"></a><span data-ttu-id="ee71c-138">Funções de proteção de identidade</span><span class="sxs-lookup"><span data-stu-id="ee71c-138">Identity Protection roles</span></span>

<span data-ttu-id="ee71c-139">tooload saldo Olá atividades de gestão em torno da sua implementação Identity Protection, pode atribuir várias funções.</span><span class="sxs-lookup"><span data-stu-id="ee71c-139">tooload balance hello management activities around your Identity Protection implementation, you can assign several roles.</span></span> <span data-ttu-id="ee71c-140">Azure AD Identity Protection suporta 3 funções do diretório:</span><span class="sxs-lookup"><span data-stu-id="ee71c-140">Azure AD Identity Protection supports 3 directory roles:</span></span>

| <span data-ttu-id="ee71c-141">Função</span><span class="sxs-lookup"><span data-stu-id="ee71c-141">Role</span></span>                         | <span data-ttu-id="ee71c-142">Pode fazê-lo</span><span class="sxs-lookup"><span data-stu-id="ee71c-142">Can do</span></span>                          | <span data-ttu-id="ee71c-143">Não é possível efetuar</span><span class="sxs-lookup"><span data-stu-id="ee71c-143">Cannot do</span></span>
| :--                          | ---                                |  ---   |
| <span data-ttu-id="ee71c-144">Administrador global</span><span class="sxs-lookup"><span data-stu-id="ee71c-144">Global administrator</span></span>         | <span data-ttu-id="ee71c-145">Acesso total tooIdentity proteção, carregar Identity Protection</span><span class="sxs-lookup"><span data-stu-id="ee71c-145">Full access tooIdentity Protection, Onboard Identity Protection</span></span>| |
| <span data-ttu-id="ee71c-146">Administrador de segurança</span><span class="sxs-lookup"><span data-stu-id="ee71c-146">Security administrator</span></span>       | <span data-ttu-id="ee71c-147">Acesso total tooIdentity proteção</span><span class="sxs-lookup"><span data-stu-id="ee71c-147">Full access tooIdentity Protection</span></span> | <span data-ttu-id="ee71c-148">Carregar Identity Protection, repor palavras-passe para um utilizador</span><span class="sxs-lookup"><span data-stu-id="ee71c-148">Onboard Identity Protection,  reset passwords for a user</span></span> |
| <span data-ttu-id="ee71c-149">Leitor de segurança</span><span class="sxs-lookup"><span data-stu-id="ee71c-149">Security reader</span></span>              | <span data-ttu-id="ee71c-150">Acesso só de pronto tooIdentity proteção</span><span class="sxs-lookup"><span data-stu-id="ee71c-150">Ready-only access tooIdentity Protection</span></span> | <span data-ttu-id="ee71c-151">Carregar Identity Protection, remidiate utilizadores, configurar políticas, repor palavras-passe</span><span class="sxs-lookup"><span data-stu-id="ee71c-151">Onboard Identity Protection, remidiate users, configure policies,  reset passwords</span></span> |




<span data-ttu-id="ee71c-152">Para obter mais detalhes, consulte [atribuir funções de administrador no Azure Active Directory](active-directory-assign-admin-roles-azure-portal.md)</span><span class="sxs-lookup"><span data-stu-id="ee71c-152">For more details, see [Assigning administrator roles in Azure Active Directory](active-directory-assign-admin-roles-azure-portal.md)</span></span>



## <a name="detection"></a><span data-ttu-id="ee71c-153">Deteção</span><span class="sxs-lookup"><span data-stu-id="ee71c-153">Detection</span></span>

### <a name="vulnerabilities"></a><span data-ttu-id="ee71c-154">Vulnerabilidades</span><span class="sxs-lookup"><span data-stu-id="ee71c-154">Vulnerabilities</span></span>

<span data-ttu-id="ee71c-155">Azure Active Directory Identity Protection analyses a configuração e Deteta que pode ter um impacto nas identidades dos utilizadores.</span><span class="sxs-lookup"><span data-stu-id="ee71c-155">Azure Active Directory Identity Protection analyses your configuration and detects vulnerabilities that can have an impact on your user's identities.</span></span> <span data-ttu-id="ee71c-156">Para obter mais detalhes, consulte [vulnerabilidades detetadas pelo Azure Active Directory Identity Protection](active-directory-identityprotection-vulnerabilities.md).</span><span class="sxs-lookup"><span data-stu-id="ee71c-156">For more details, see [Vulnerabilities detected by Azure Active Directory Identity Protection](active-directory-identityprotection-vulnerabilities.md).</span></span>

### <a name="risk-events"></a><span data-ttu-id="ee71c-157">Eventos de risco</span><span class="sxs-lookup"><span data-stu-id="ee71c-157">Risk events</span></span>

<span data-ttu-id="ee71c-158">Azure Active Directory utiliza adaptável do machine learning algoritmos e heurística toodetect suspeitas ações que são as identidades dos utilizadores tooyour relacionados.</span><span class="sxs-lookup"><span data-stu-id="ee71c-158">Azure Active Directory uses adaptive machine learning algorithms and heuristics toodetect suspicious actions that are related tooyour user's identities.</span></span> <span data-ttu-id="ee71c-159">sistema de Olá cria um registo para cada ação suspeito detetado.</span><span class="sxs-lookup"><span data-stu-id="ee71c-159">hello system creates a record for each detected suspicious action.</span></span> <span data-ttu-id="ee71c-160">Estes registos são também conhecidos como eventos de risco.</span><span class="sxs-lookup"><span data-stu-id="ee71c-160">These records are also known as risk events.</span></span>  
<span data-ttu-id="ee71c-161">Para obter mais detalhes, veja [Eventos de risco do Azure Active Directory](active-directory-identity-protection-risk-events.md).</span><span class="sxs-lookup"><span data-stu-id="ee71c-161">For more details, see [Azure Active Directory risk events](active-directory-identity-protection-risk-events.md).</span></span>


## <a name="investigation"></a><span data-ttu-id="ee71c-162">Investigação</span><span class="sxs-lookup"><span data-stu-id="ee71c-162">Investigation</span></span>
<span data-ttu-id="ee71c-163">Da sua viagem através da proteção de identidade normalmente começa com o dashboard de Identity Protection Olá.</span><span class="sxs-lookup"><span data-stu-id="ee71c-163">Your journey through Identity Protection typically starts with hello Identity Protection dashboard.</span></span>

<span data-ttu-id="ee71c-164">![Remediação](./media/active-directory-identityprotection/1000.png "remediação")</span><span class="sxs-lookup"><span data-stu-id="ee71c-164">![Remediation](./media/active-directory-identityprotection/1000.png "Remediation")</span></span>

<span data-ttu-id="ee71c-165">dashboard de Olá dá-lhe acesso ao:</span><span class="sxs-lookup"><span data-stu-id="ee71c-165">hello dashboard gives you access to:</span></span>

* <span data-ttu-id="ee71c-166">Os relatórios tal como **utilizadores sinalizados para risco**, **eventos de risco** e **vulnerabilidades**</span><span class="sxs-lookup"><span data-stu-id="ee71c-166">Reports such as **Users flagged for risk**, **Risk events** and **Vulnerabilities**</span></span>
* <span data-ttu-id="ee71c-167">Definições, tais como a configuração de Olá do seu **políticas de segurança**, **notificações** e **registo de autenticação multifator**</span><span class="sxs-lookup"><span data-stu-id="ee71c-167">Settings such as hello configuration of your **Security Policies**, **Notifications** and **multi-factor authentication registration**</span></span>

<span data-ttu-id="ee71c-168">É, geralmente, o ponto de partida para investigação, que é o processo de Olá de rever Olá atividades, registos e outras informações relevantes tooa relacionado toodecide de eventos de risco, se são necessários passos de remediação ou atenuação, e como identidade Olá foi comprometido e compreender como Olá comprometido identidade foi utilizada.</span><span class="sxs-lookup"><span data-stu-id="ee71c-168">It is typically your starting point for investigation, which is hello process of reviewing hello activities, logs, and other relevant information related tooa risk event toodecide whether remediation or mitigation steps are necessary,  and how hello identity was compromised, and understand how hello compromised identity was used.</span></span>

<span data-ttu-id="ee71c-169">Pode associar o seu toohello de atividades de investigação [notificações](active-directory-identityprotection-notifications.md) do Azure Active Directory proteção enviar por e-mail.</span><span class="sxs-lookup"><span data-stu-id="ee71c-169">You can tie your investigation activities toohello [notifications](active-directory-identityprotection-notifications.md) Azure Active Directory Protection sends per email.</span></span>

<span data-ttu-id="ee71c-170">Olá secções seguintes fornecem mais detalhes e passos de Olá que estão relacionados tooan investigação.</span><span class="sxs-lookup"><span data-stu-id="ee71c-170">hello following sections provide you with more details and hello steps that are related tooan investigation.</span></span>  


## <a name="risky-sign-ins"></a><span data-ttu-id="ee71c-171">Risco inícios de sessão</span><span class="sxs-lookup"><span data-stu-id="ee71c-171">Risky sign-ins</span></span>

<span data-ttu-id="ee71c-172">Azure Active Directory Deteta [tipos de eventos de risco](active-directory-reporting-risk-events.md#risk-event-types) no offline e em tempo real.</span><span class="sxs-lookup"><span data-stu-id="ee71c-172">Azure Active Directory detects [risk event types](active-directory-reporting-risk-events.md#risk-event-types) in real-time and offline.</span></span> <span data-ttu-id="ee71c-173">Cada evento de risco que foi detetado para um início de sessão de um utilizador contribui conceito lógico tooa chamado arriscado início de sessão.</span><span class="sxs-lookup"><span data-stu-id="ee71c-173">Each risk event that has been detected for a sign-in of a user contributes tooa logical concept called risky sign-in.</span></span> <span data-ttu-id="ee71c-174">Um risco início de sessão é um indicador para uma tentativa de início de sessão não pode ter sido efetuada pelo proprietário de legítimos Olá de uma conta de utilizador.</span><span class="sxs-lookup"><span data-stu-id="ee71c-174">A risky sign-in is an indicator for a sign-in attempt that might not have been performed by hello legitimate owner of a user account.</span></span>


### <a name="sign-in-risk-level"></a><span data-ttu-id="ee71c-175">Nível de risco de início de sessão</span><span class="sxs-lookup"><span data-stu-id="ee71c-175">Sign-in risk level</span></span>

<span data-ttu-id="ee71c-176">Um nível de risco de início de sessão é uma indicação (alta, média ou baixa) de probabilidade de Olá que uma tentativa de início de sessão não foi efetuada pelo proprietário de legítimos Olá de uma conta de utilizador.</span><span class="sxs-lookup"><span data-stu-id="ee71c-176">A sign-in risk level is an indication (High, Medium, or Low) of hello likelihood that a sign-in attempt was not performed by hello legitimate owner of a user account.</span></span>

### <a name="mitigating-sign-in-risk-events"></a><span data-ttu-id="ee71c-177">Mitigar o risco de início de sessão de eventos</span><span class="sxs-lookup"><span data-stu-id="ee71c-177">Mitigating sign-in risk events</span></span>

<span data-ttu-id="ee71c-178">Uma mitigação é uma capacidade de Olá toolimit de ação de um atacante tooexploit uma identidade comprometida ou dispositivo sem estado de restauro Olá identidade ou dispositivo tooa seguro.</span><span class="sxs-lookup"><span data-stu-id="ee71c-178">A mitigation is an action toolimit hello ability of an attacker tooexploit a compromised identity or device without restoring hello identity or device tooa safe state.</span></span> <span data-ttu-id="ee71c-179">Uma mitigação não resolver eventos de risco de início de sessão anteriores associados à identidade Olá ou dispositivo.</span><span class="sxs-lookup"><span data-stu-id="ee71c-179">A mitigation does not resolve previous sign-in risk events associated with hello identity or device.</span></span>

<span data-ttu-id="ee71c-180">inícios de sessão de risco toomitigate automaticamente, pode configurar policicies de segurança de início de sessão de risco.</span><span class="sxs-lookup"><span data-stu-id="ee71c-180">toomitigate risky sign-ins automatically, you can configure sign-in risk security policicies.</span></span> <span data-ttu-id="ee71c-181">Utilizar estas políticas, consideram o nível de risco Olá de utilizador de Olá ou Olá início de sessão tooblock arriscados inícios de sessão ou exigir a autenticação multifator tooperform Olá.</span><span class="sxs-lookup"><span data-stu-id="ee71c-181">Using these policies, you consider hello risk level of hello user or hello sign-in tooblock risky sign-ins or require hello user tooperform multi-factor authentication.</span></span> <span data-ttu-id="ee71c-182">Estas ações podem impedir que um atacante explorá danos de toocause uma identidade roubado e poderão dar-lhe identidade de Olá de toosecure algum tempo.</span><span class="sxs-lookup"><span data-stu-id="ee71c-182">These actions may prevent an attacker from exploiting a stolen identity toocause damage, and may give you some time toosecure hello identity.</span></span>

### <a name="sign-in-risk-security-policy"></a><span data-ttu-id="ee71c-183">Política de segurança de início de sessão risco</span><span class="sxs-lookup"><span data-stu-id="ee71c-183">Sign-in risk security policy</span></span>
<span data-ttu-id="ee71c-184">Uma política de início de sessão risco é uma política de acesso condicional que avalia Olá risco tooa específico início de sessão e aplica-se mitigações com base nas condições predefinidas e as regras.</span><span class="sxs-lookup"><span data-stu-id="ee71c-184">A sign-in risk policy is a conditional access policy that evaluates hello risk tooa specific sign-in and applies mitigations based on predefined conditions and rules.</span></span>

<span data-ttu-id="ee71c-185">![Política de início de sessão risco](./media/active-directory-identityprotection/1014.png "início de sessão da política de risco")</span><span class="sxs-lookup"><span data-stu-id="ee71c-185">![Sign-in risk policy](./media/active-directory-identityprotection/1014.png "Sign-in risk policy")</span></span>

<span data-ttu-id="ee71c-186">Azure AD Identity Protection ajuda a gerir mitigação de Olá do risco de inícios de sessão, permitindo:</span><span class="sxs-lookup"><span data-stu-id="ee71c-186">Azure AD Identity Protection helps you manage hello mitigation of risky sign-ins by enabling you to:</span></span>

* <span data-ttu-id="ee71c-187">Conjunto Olá utilizadores e grupos Olá política aplica-se a:</span><span class="sxs-lookup"><span data-stu-id="ee71c-187">Set hello users and groups hello policy applies to:</span></span>

    <span data-ttu-id="ee71c-188">![Política de início de sessão risco](./media/active-directory-identityprotection/1015.png "início de sessão da política de risco")</span><span class="sxs-lookup"><span data-stu-id="ee71c-188">![Sign-in risk policy](./media/active-directory-identityprotection/1015.png "Sign-in risk policy")</span></span>
* <span data-ttu-id="ee71c-189">Definir Olá início de sessão risco nível limiar (baixa, média ou alta) que aciona a política de Olá:</span><span class="sxs-lookup"><span data-stu-id="ee71c-189">Set hello sign-in risk level threshold (low, medium, or high) that triggers hello policy:</span></span>

    <span data-ttu-id="ee71c-190">![Política de início de sessão risco](./media/active-directory-identityprotection/1016.png "início de sessão da política de risco")</span><span class="sxs-lookup"><span data-stu-id="ee71c-190">![Sign-in risk policy](./media/active-directory-identityprotection/1016.png "Sign-in risk policy")</span></span>
* <span data-ttu-id="ee71c-191">Conjunto Olá controlos toobe imposta quando a política de Olá aciona:</span><span class="sxs-lookup"><span data-stu-id="ee71c-191">Set hello controls toobe enforced when hello policy triggers:</span></span>  

    <span data-ttu-id="ee71c-192">![Política de início de sessão risco](./media/active-directory-identityprotection/1017.png "início de sessão da política de risco")</span><span class="sxs-lookup"><span data-stu-id="ee71c-192">![Sign-in risk policy](./media/active-directory-identityprotection/1017.png "Sign-in risk policy")</span></span>
* <span data-ttu-id="ee71c-193">Estado do comutador Olá da sua política:</span><span class="sxs-lookup"><span data-stu-id="ee71c-193">Switch hello state of your policy:</span></span>

    <span data-ttu-id="ee71c-194">![Registo do MFA](./media/active-directory-identityprotection/403.png "registo do MFA")</span><span class="sxs-lookup"><span data-stu-id="ee71c-194">![MFA Registration](./media/active-directory-identityprotection/403.png "MFA Registration")</span></span>
* <span data-ttu-id="ee71c-195">Rever e avaliar o impacto de Olá uma alteração antes de ativar esta:</span><span class="sxs-lookup"><span data-stu-id="ee71c-195">Review and evaluate hello impact of a change before activating it:</span></span>

    <span data-ttu-id="ee71c-196">![Política de início de sessão risco](./media/active-directory-identityprotection/1018.png "início de sessão da política de risco")</span><span class="sxs-lookup"><span data-stu-id="ee71c-196">![Sign-in risk policy](./media/active-directory-identityprotection/1018.png "Sign-in risk policy")</span></span>

#### <a name="what-you-need-tooknow"></a><span data-ttu-id="ee71c-197">O que precisa de tooknow</span><span class="sxs-lookup"><span data-stu-id="ee71c-197">What you need tooknow</span></span>
<span data-ttu-id="ee71c-198">Pode configurar uma risco de início de sessão segurança política toorequire a autenticação multifator:</span><span class="sxs-lookup"><span data-stu-id="ee71c-198">You can configure a sign-in risk security policy toorequire multi-factor authentication:</span></span>

<span data-ttu-id="ee71c-199">![Política de início de sessão risco](./media/active-directory-identityprotection/1017.png "início de sessão da política de risco")</span><span class="sxs-lookup"><span data-stu-id="ee71c-199">![Sign-in risk policy](./media/active-directory-identityprotection/1017.png "Sign-in risk policy")</span></span>

<span data-ttu-id="ee71c-200">No entanto, por motivos de segurança, esta definição só funciona para os utilizadores que já foram registados para autenticação multifator.</span><span class="sxs-lookup"><span data-stu-id="ee71c-200">However, for security reasons, this setting only works for users that have already been registered for multi-factor authentication.</span></span> <span data-ttu-id="ee71c-201">Se a autenticação multifator do Olá condição toorequire for satisfeita para um utilizador que ainda não está registado para autenticação multifator, utilizador de Olá está bloqueado.</span><span class="sxs-lookup"><span data-stu-id="ee71c-201">If hello condition toorequire multi-factor authentication is satisfied for a user who is not yet registered for multi-factor authentication, hello user is blocked.</span></span>

<span data-ttu-id="ee71c-202">Como melhor prática, se pretender que a autenticação multifator toorequire para inícios de sessão risco, deve:</span><span class="sxs-lookup"><span data-stu-id="ee71c-202">As a best practice, if you want toorequire multi-factor authentication for risky sign-ins, you should:</span></span>

1. <span data-ttu-id="ee71c-203">Ativar Olá [política de registo de autenticação multifator](#multi-factor-authentication-registration-policy) para Olá utilizadores afetados.</span><span class="sxs-lookup"><span data-stu-id="ee71c-203">Enable hello [multi-factor authentication registration policy](#multi-factor-authentication-registration-policy) for hello affected users.</span></span>
2. <span data-ttu-id="ee71c-204">Exigir Olá afetados toologin de utilizadores no tooperform sessão não arriscados um registo do MFA</span><span class="sxs-lookup"><span data-stu-id="ee71c-204">Require hello affected users toologin in a non-risky session tooperform a MFA registration</span></span>

<span data-ttu-id="ee71c-205">Concluir estes passos garante que a autenticação multifator é necessária para um risco início de sessão.</span><span class="sxs-lookup"><span data-stu-id="ee71c-205">Completing these steps ensures that multi-factor authentication is required for a risky sign-in.</span></span>

#### <a name="best-practices"></a><span data-ttu-id="ee71c-206">Melhores práticas</span><span class="sxs-lookup"><span data-stu-id="ee71c-206">Best practices</span></span>
<span data-ttu-id="ee71c-207">Escolher um **elevada** limiar reduz o número de Olá de vezes que uma política é acionada e minimiza Olá impacto toousers.</span><span class="sxs-lookup"><span data-stu-id="ee71c-207">Choosing a **High** threshold reduces hello number of times a policy is triggered and minimizes hello impact toousers.</span></span>  

<span data-ttu-id="ee71c-208">No entanto, exclui **baixa** e **média** inícios de sessão sinalizados para risco da política de Olá, que não pode bloquear um atacante de explorá uma identidade comprometida.</span><span class="sxs-lookup"><span data-stu-id="ee71c-208">However, it excludes **Low** and **Medium** sign-ins flagged for risk from hello policy, which may not block an attacker from exploiting a compromised identity.</span></span>

<span data-ttu-id="ee71c-209">Quando a definição Olá política,</span><span class="sxs-lookup"><span data-stu-id="ee71c-209">When setting hello policy,</span></span>

* <span data-ttu-id="ee71c-210">Excluir os utilizadores que não o fizer / não podem ter a autenticação multifator</span><span class="sxs-lookup"><span data-stu-id="ee71c-210">Exclude users who do not/cannot have multi-factor authentication</span></span>
* <span data-ttu-id="ee71c-211">Excluir utilizadores nas regiões onde o ativar política de Olá não é prático (por exemplo toohelpdesk sem acesso)</span><span class="sxs-lookup"><span data-stu-id="ee71c-211">Exclude users in locales where enabling hello policy is not practical (for example no access toohelpdesk)</span></span>
* <span data-ttu-id="ee71c-212">Excluir os utilizadores que são toogenerate provavelmente uma grande quantidade de Falso-positivos (programadores, os analistas de segurança)</span><span class="sxs-lookup"><span data-stu-id="ee71c-212">Exclude users who are likely toogenerate a lot of false-positives (developers, security analysts)</span></span>
* <span data-ttu-id="ee71c-213">Utilize um **elevada** limiar durante a agregação de política iniciais, ou se tem minimizar desafios vistos pelos utilizadores finais.</span><span class="sxs-lookup"><span data-stu-id="ee71c-213">Use a **High** threshold during initial policy roll out, or if you must minimize challenges seen by end users.</span></span>
* <span data-ttu-id="ee71c-214">Utilize um **baixa** limiar se a sua organização precisar de maior segurança.</span><span class="sxs-lookup"><span data-stu-id="ee71c-214">Use a **Low**  threshold if your organization requires greater security.</span></span> <span data-ttu-id="ee71c-215">Selecionar um **baixa** limiar apresenta utilizador adicionais início de sessão desafios, mas uma maior segurança.</span><span class="sxs-lookup"><span data-stu-id="ee71c-215">Selecting a **Low** threshold introduces additional user sign-in challenges, but increased security.</span></span>

<span data-ttu-id="ee71c-216">Olá recomendado predefinido para a maioria das organizações é tooconfigure uma regra para um **média** limiar toostrike um equilíbrio entre capacidade de utilização e segurança.</span><span class="sxs-lookup"><span data-stu-id="ee71c-216">hello recommended default for most organizations is tooconfigure a rule for a **Medium** threshold toostrike a balance between usability and security.</span></span>

<span data-ttu-id="ee71c-217">política de início de sessão risco Olá é:</span><span class="sxs-lookup"><span data-stu-id="ee71c-217">hello sign-in risk policy is:</span></span>

* <span data-ttu-id="ee71c-218">Tráfego de browser tooall aplicados e inícios de sessão que utilizam autenticação moderna.</span><span class="sxs-lookup"><span data-stu-id="ee71c-218">Applied tooall browser traffic and sign-ins using modern authentication.</span></span>
* <span data-ttu-id="ee71c-219">Não aplicado tooapplications utilizar protocolos de segurança mais antigos, desativando o ponto final de WS-Trust de Olá no IDP Olá federado, tais como o ADFS.</span><span class="sxs-lookup"><span data-stu-id="ee71c-219">Not applied tooapplications using older security protocols by disabling hello WS-Trust endpoint at hello federated IDP, such as ADFS.</span></span>

<span data-ttu-id="ee71c-220">Olá **eventos de risco** página na consola de Identity Protection Olá apresenta uma lista de todos os eventos:</span><span class="sxs-lookup"><span data-stu-id="ee71c-220">hello **Risk Events** page in hello Identity Protection console lists all events:</span></span>

* <span data-ttu-id="ee71c-221">Esta política foi aplicada ao</span><span class="sxs-lookup"><span data-stu-id="ee71c-221">This policy was applied to</span></span>
* <span data-ttu-id="ee71c-222">Pode Olá actividade de revisão e determinar se a ação de Olá foi adequada ou não</span><span class="sxs-lookup"><span data-stu-id="ee71c-222">You can review hello activity and determine whether hello action was appropriate or not</span></span>

<span data-ttu-id="ee71c-223">Para obter uma descrição geral de Olá relacionadas com a experiência de utilizador, consulte:</span><span class="sxs-lookup"><span data-stu-id="ee71c-223">For an overview of hello related user experience, see:</span></span>

* [<span data-ttu-id="ee71c-224">Recuperação de risco início de sessão</span><span class="sxs-lookup"><span data-stu-id="ee71c-224">Risky sign-in recovery</span></span>](active-directory-identityprotection-flows.md#risky-sign-in-recovery)
* [<span data-ttu-id="ee71c-225">Risco início de sessão bloqueado</span><span class="sxs-lookup"><span data-stu-id="ee71c-225">Risky sign-in blocked</span></span>](active-directory-identityprotection-flows.md#risky-sign-in-blocked)  
* [<span data-ttu-id="ee71c-226">Início de sessão experiências com o Azure AD Identity Protection</span><span class="sxs-lookup"><span data-stu-id="ee71c-226">Sign-in experiences with Azure AD Identity Protection</span></span>](active-directory-identityprotection-flows.md)  

<span data-ttu-id="ee71c-227">**caixa de diálogo de configuração relacionados de Olá de tooopen**:</span><span class="sxs-lookup"><span data-stu-id="ee71c-227">**tooopen hello related configuration dialog**:</span></span>

- <span data-ttu-id="ee71c-228">No Olá **do Azure AD Identity Protection** painel, no Olá **configurar** secção, clique em **início de sessão da política de risco**.</span><span class="sxs-lookup"><span data-stu-id="ee71c-228">On hello **Azure AD Identity Protection** blade, in hello **Configure** section, click **Sign-in risk policy**.</span></span>

    <span data-ttu-id="ee71c-229">![Política do utilizador ridk](./media/active-directory-identityprotection/1014.png "ridk de política de utilizador")</span><span class="sxs-lookup"><span data-stu-id="ee71c-229">![User ridk policy](./media/active-directory-identityprotection/1014.png "User ridk policy")</span></span>



## <a name="users-flagged-for-risk"></a><span data-ttu-id="ee71c-230">Utilizadores sinalizados para risco</span><span class="sxs-lookup"><span data-stu-id="ee71c-230">Users flagged for risk</span></span>

<span data-ttu-id="ee71c-231">Todas as ativas [eventos de risco](active-directory-identity-protection-risk-events.md) que foram detetados pelo Azure Active Directory para um utilizador contribuir conceito lógico tooa chamado risco do utilizador.</span><span class="sxs-lookup"><span data-stu-id="ee71c-231">All active [risk events](active-directory-identity-protection-risk-events.md) that were detected by Azure Active Directory for a user contribute tooa logical concept called user risk.</span></span> <span data-ttu-id="ee71c-232">Um utilizador sinalizado para risco é um indicador de uma conta de utilizador que possam ter sido comprometido.</span><span class="sxs-lookup"><span data-stu-id="ee71c-232">A user flagged for risk is an indicator for a user account that might have been compromised.</span></span>

![Utilizadores sinalizados para risco](./media/active-directory-identityprotection/1200.png)


### <a name="user-risk-level"></a><span data-ttu-id="ee71c-234">Nível de risco do utilizador</span><span class="sxs-lookup"><span data-stu-id="ee71c-234">User risk level</span></span>

<span data-ttu-id="ee71c-235">Um nível de risco do utilizador é uma indicação (alta, média ou baixa) de probabilidade de Olá que a identidade do utilizador Olá tiver sido comprometida.</span><span class="sxs-lookup"><span data-stu-id="ee71c-235">A user risk level is an indication (High, Medium, or Low) of hello likelihood that hello user’s identity has been compromised.</span></span> <span data-ttu-id="ee71c-236">Esta é calculada com base em eventos de risco de utilizador Olá que estão associados a identidade do utilizador.</span><span class="sxs-lookup"><span data-stu-id="ee71c-236">It is calculated based on hello user risk events that are associated with a user's identity.</span></span>

<span data-ttu-id="ee71c-237">Olá estado de um evento de risco é **Active Directory** ou **fechado**.</span><span class="sxs-lookup"><span data-stu-id="ee71c-237">hello status of a risk event is either **Active** or **Closed**.</span></span> <span data-ttu-id="ee71c-238">Apenas os eventos que são de risco **Active Directory** contribuir cálculo de nível de risco do toohello utilizador.</span><span class="sxs-lookup"><span data-stu-id="ee71c-238">Only risk events that are **Active** contribute toohello user risk level calculation.</span></span>

<span data-ttu-id="ee71c-239">nível de risco do utilizador Olá é calculado com Olá seguintes entradas:</span><span class="sxs-lookup"><span data-stu-id="ee71c-239">hello user risk level is calculated using hello following inputs:</span></span>

* <span data-ttu-id="ee71c-240">Eventos de risco Active Directory afetar utilizador Olá</span><span class="sxs-lookup"><span data-stu-id="ee71c-240">Active risk events impacting hello user</span></span>
* <span data-ttu-id="ee71c-241">Nível de risco destes eventos</span><span class="sxs-lookup"><span data-stu-id="ee71c-241">Risk level of these events</span></span>
* <span data-ttu-id="ee71c-242">Indica se foram efetuadas as ações de remediação</span><span class="sxs-lookup"><span data-stu-id="ee71c-242">Whether any remediation actions have been taken</span></span>

<span data-ttu-id="ee71c-243">![Riscos de utilizador](./media/active-directory-identityprotection/1031.png "riscos de utilizador")</span><span class="sxs-lookup"><span data-stu-id="ee71c-243">![User risks](./media/active-directory-identityprotection/1031.png "User risks")</span></span>

<span data-ttu-id="ee71c-244">Pode utilizar Olá utilizador risco níveis toocreate políticas de acesso condicional que impeça os utilizadores de risco de início de sessão ou forçá-los toosecurely alterar a palavra-passe.</span><span class="sxs-lookup"><span data-stu-id="ee71c-244">You can use hello user risk levels toocreate conditional access policies that block risky users from signing in, or force them toosecurely change their password.</span></span>

### <a name="closing-risk-events-manually"></a><span data-ttu-id="ee71c-245">Fechar os eventos de risco manualmente</span><span class="sxs-lookup"><span data-stu-id="ee71c-245">Closing risk events manually</span></span>

<span data-ttu-id="ee71c-246">Na maioria dos casos, irá tome as ações de remediação, tais como os eventos de risco fechar tooautomatically de reposição de uma palavra-passe segura.</span><span class="sxs-lookup"><span data-stu-id="ee71c-246">In most cases, you will take remediation actions such as a secure password reset tooautomatically close risk events.</span></span> <span data-ttu-id="ee71c-247">No entanto, isto poderá não ser sempre possível.</span><span class="sxs-lookup"><span data-stu-id="ee71c-247">However, this might not always be possible.</span></span>  
<span data-ttu-id="ee71c-248">Isto é, por exemplo, caso Olá, quando:</span><span class="sxs-lookup"><span data-stu-id="ee71c-248">This is, for example, hello case, when:</span></span>

* <span data-ttu-id="ee71c-249">Foi eliminado um utilizador com eventos de risco Active Directory</span><span class="sxs-lookup"><span data-stu-id="ee71c-249">A user with Active risk events has been deleted</span></span>
* <span data-ttu-id="ee71c-250">Uma investigação revela de que tem foi efetuar um evento de risco comunicado pelo utilizador legítimo Olá</span><span class="sxs-lookup"><span data-stu-id="ee71c-250">An investigation reveals that a reported risk event has been perform by hello legitimate user</span></span>

<span data-ttu-id="ee71c-251">Uma vez que os eventos de risco que são **Active Directory** contribuir cálculo de risco toohello utilizador, poderá ter toomanually reduzir um nível de risco fechando os eventos de risco manualmente.</span><span class="sxs-lookup"><span data-stu-id="ee71c-251">Because risk events that are **Active** contribute toohello user risk calculation, you may have toomanually lower a risk level by closing risk events manually.</span></span>  
<span data-ttu-id="ee71c-252">Decorrer Olá de investigação, pode escolher tootake qualquer uma destas ações toochange Olá Estado um evento de risco:</span><span class="sxs-lookup"><span data-stu-id="ee71c-252">During hello course of investigation, you can choose tootake any of these actions toochange hello status of a risk event:</span></span>

<span data-ttu-id="ee71c-253">![Ações](./media/active-directory-identityprotection/34.png "ações")</span><span class="sxs-lookup"><span data-stu-id="ee71c-253">![Actions](./media/active-directory-identityprotection/34.png "Actions")</span></span>

* <span data-ttu-id="ee71c-254">**Resolver** - se depois de investigar um evento de risco, demorou uma ação de remediação adequado fora Identity Protection e achar que eventos de risco Olá devem ser considerados fechados, o evento de Olá marca como resolvido.</span><span class="sxs-lookup"><span data-stu-id="ee71c-254">**Resolve** - If after investigating a risk event, you took an appropriate remediation action outside Identity Protection, and you believe that hello risk event should be considered closed, mark hello event as Resolved.</span></span> <span data-ttu-id="ee71c-255">Eventos resolvidos definirá tooClosed de estado do evento de risco Olá e eventos de risco Olá já não irão contribuir toouser risco.</span><span class="sxs-lookup"><span data-stu-id="ee71c-255">Resolved events will set hello risk event’s status tooClosed and hello risk event will no longer contribute toouser risk.</span></span>
* <span data-ttu-id="ee71c-256">**Marcar como falso-positivos** -em alguns casos, pode investigar um evento de risco e detetar que incorretamente foi sinalizado como um risco.</span><span class="sxs-lookup"><span data-stu-id="ee71c-256">**Mark as false-positive** - In some cases, you may investigate a risk event and discover that it was incorrectly flagged as a risky.</span></span> <span data-ttu-id="ee71c-257">Pode ajudar a reduzir o número de Olá de tais ocorrências assinalando eventos de risco Olá como falso-positivos.</span><span class="sxs-lookup"><span data-stu-id="ee71c-257">You can help reduce hello number of such occurrences by marking hello risk event as False-positive.</span></span> <span data-ttu-id="ee71c-258">Isto irá ajudar Olá aprendizagem automática classificação de Olá tooimprove algoritmos de eventos semelhantes em Olá futura.</span><span class="sxs-lookup"><span data-stu-id="ee71c-258">This will help hello machine learning algorithms tooimprove hello classification of similar events in hello future.</span></span> <span data-ttu-id="ee71c-259">Estado de Olá de eventos de Falso-positivos é demasiado**fechado** e já não contribuem toouser risco.</span><span class="sxs-lookup"><span data-stu-id="ee71c-259">hello status of false-positive events is too**Closed** and they will no longer contribute toouser risk.</span></span>
* <span data-ttu-id="ee71c-260">**Ignorar** - se de que não tenha sido qualquer ação de remediação, mas pretende Olá toobe de eventos de risco foi removido da lista de Active Directory Olá, pode marcar um evento de risco ignorar e o estado do evento Olá será fechado.</span><span class="sxs-lookup"><span data-stu-id="ee71c-260">**Ignore** - If you have not taken any remediation action, but want hello risk event toobe removed from hello active list, you can mark a risk event Ignore and hello event status will be Closed.</span></span> <span data-ttu-id="ee71c-261">Eventos ignorados não contribuir toouser risco.</span><span class="sxs-lookup"><span data-stu-id="ee71c-261">Ignored events do not contribute toouser risk.</span></span> <span data-ttu-id="ee71c-262">Esta opção só deve ser utilizada em circunstâncias invulgares.</span><span class="sxs-lookup"><span data-stu-id="ee71c-262">This option should only be used under unusual circumstances.</span></span>
* <span data-ttu-id="ee71c-263">**Reativar** -o risco de eventos que foram fechados manualmente (escolhendo **resolver**, **falsos positivos**, ou **ignorar**) pode ser reativado, definição Olá Estado do evento fazer uma cópia de demasiado**Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="ee71c-263">**Reactivate** - Risk events that were manually closed (by choosing **Resolve**, **False positive**, or **Ignore**) can be reactivated, setting hello event status back too**Active**.</span></span> <span data-ttu-id="ee71c-264">Eventos de risco reativado contribuem cálculo de nível de risco do toohello utilizador.</span><span class="sxs-lookup"><span data-stu-id="ee71c-264">Reactivated risk events contribute toohello user risk level calculation.</span></span> <span data-ttu-id="ee71c-265">Eventos de risco fechados através de remediação (tal como repor uma palavra-passe segura) não podem ser reativados.</span><span class="sxs-lookup"><span data-stu-id="ee71c-265">Risk events closed through remediation (such as a secure password reset) cannot be reactivated.</span></span>

<span data-ttu-id="ee71c-266">**caixa de diálogo de configuração relacionados de Olá de tooopen**:</span><span class="sxs-lookup"><span data-stu-id="ee71c-266">**tooopen hello related configuration dialog**:</span></span>

1. <span data-ttu-id="ee71c-267">No Olá **do Azure AD Identity Protection** painel, em **investigar**, clique em **eventos de risco**.</span><span class="sxs-lookup"><span data-stu-id="ee71c-267">On hello **Azure AD Identity Protection** blade, under **Investigate**, click **Risk events**.</span></span>

    <span data-ttu-id="ee71c-268">![Reposição de palavra-passe manual](./media/active-directory-identityprotection/1002.png "reposição de palavra-passe Manual")</span><span class="sxs-lookup"><span data-stu-id="ee71c-268">![Manual password reset](./media/active-directory-identityprotection/1002.png "Manual password reset")</span></span>
2. <span data-ttu-id="ee71c-269">No Olá **eventos de risco** lista, clique em risco.</span><span class="sxs-lookup"><span data-stu-id="ee71c-269">In hello **Risk events** list, click a risk.</span></span>

    <span data-ttu-id="ee71c-270">![Reposição de palavra-passe manual](./media/active-directory-identityprotection/1003.png "reposição de palavra-passe Manual")</span><span class="sxs-lookup"><span data-stu-id="ee71c-270">![Manual password reset](./media/active-directory-identityprotection/1003.png "Manual password reset")</span></span>
3. <span data-ttu-id="ee71c-271">No painel de risco Olá, faça duplo clique um utilizador.</span><span class="sxs-lookup"><span data-stu-id="ee71c-271">On hello risk blade, right-click a user.</span></span>

    <span data-ttu-id="ee71c-272">![Reposição de palavra-passe manual](./media/active-directory-identityprotection/1004.png "reposição de palavra-passe Manual")</span><span class="sxs-lookup"><span data-stu-id="ee71c-272">![Manual password reset](./media/active-directory-identityprotection/1004.png "Manual password reset")</span></span>

### <a name="closing-all-risk-events-for-a-user-manually"></a><span data-ttu-id="ee71c-273">Fechar todos os eventos de risco de um utilizador manualmente</span><span class="sxs-lookup"><span data-stu-id="ee71c-273">Closing all risk events for a user manually</span></span>
<span data-ttu-id="ee71c-274">Em vez de manualmente fechar os eventos de risco de um utilizador individualmente, do Azure Active Directory Identity Protection também fornece um método tooclose todos os eventos para um utilizador com um clique.</span><span class="sxs-lookup"><span data-stu-id="ee71c-274">Instead of manually closing risk events for a user individually, Azure Active Directory Identity Protection also provides you with a method tooclose all events for a user with one click.</span></span>

<span data-ttu-id="ee71c-275">![Ações](./media/active-directory-identityprotection/2222.png "ações")</span><span class="sxs-lookup"><span data-stu-id="ee71c-275">![Actions](./media/active-directory-identityprotection/2222.png "Actions")</span></span>

<span data-ttu-id="ee71c-276">Ao clicar em **dispensar todos os eventos**, todos os eventos estão fechados e utilizador Olá afetado já não está em risco.</span><span class="sxs-lookup"><span data-stu-id="ee71c-276">When you click **Dismiss all events**, all events are closed and hello affected user is no longer at risk.</span></span>

### <a name="remediating-user-risk-events"></a><span data-ttu-id="ee71c-277">Eventos de risco de utilizador de remediação</span><span class="sxs-lookup"><span data-stu-id="ee71c-277">Remediating user risk events</span></span>

<span data-ttu-id="ee71c-278">Uma remediação é toosecure uma ação uma identidade ou um dispositivo que anteriormente era suspeito ou conhecido toobe comprometido.</span><span class="sxs-lookup"><span data-stu-id="ee71c-278">A remediation is an action toosecure an identity or a device that was previously suspected or known toobe compromised.</span></span> <span data-ttu-id="ee71c-279">Uma ação de remediação restaura Olá identidade Estado ou de dispositivo tooa seguro e resolve os eventos de risco anteriores associados à identidade Olá ou dispositivo.</span><span class="sxs-lookup"><span data-stu-id="ee71c-279">A remediation action restores hello identity or device tooa safe state, and resolves previous risk events associated with hello identity or device.</span></span>

<span data-ttu-id="ee71c-280">eventos de risco de utilizador tooremediate, pode:</span><span class="sxs-lookup"><span data-stu-id="ee71c-280">tooremediate user risk events, you can:</span></span>

* <span data-ttu-id="ee71c-281">Efetue manualmente um eventos de risco utilizador de tooremediate de reposição de palavra-passe segura</span><span class="sxs-lookup"><span data-stu-id="ee71c-281">Perform a secure password reset tooremediate user risk events manually</span></span>
* <span data-ttu-id="ee71c-282">Configurar um toomitigate de política de segurança do utilizador risco ou remediar automaticamente os eventos de risco de utilizador</span><span class="sxs-lookup"><span data-stu-id="ee71c-282">Configure a user risk security policy toomitigate or remediate user risk events automatically</span></span>
* <span data-ttu-id="ee71c-283">Dispositivo de recriar a imagem de Olá infetado</span><span class="sxs-lookup"><span data-stu-id="ee71c-283">Re-image hello infected device</span></span>  

#### <a name="manual-secure-password-reset"></a><span data-ttu-id="ee71c-284">Reposição de palavra-passe segura manual</span><span class="sxs-lookup"><span data-stu-id="ee71c-284">Manual secure password reset</span></span>
<span data-ttu-id="ee71c-285">Uma reposição de palavra-passe segura é uma remediação eficaz para muitos eventos de risco e, quando efetuada, automaticamente fecha estes eventos de risco e recalcula o nível de risco Olá utilizador.</span><span class="sxs-lookup"><span data-stu-id="ee71c-285">A secure password reset is an effective remediation for many risk events, and when performed, automatically closes these risk events and recalculates hello user risk level.</span></span> <span data-ttu-id="ee71c-286">Pode utilizar Olá Identity Protection dashboard tooinitiate uma palavra-passe de reposição de um utilizador de risco.</span><span class="sxs-lookup"><span data-stu-id="ee71c-286">You can use hello Identity Protection dashboard tooinitiate a password reset for a risky user.</span></span>

<span data-ttu-id="ee71c-287">caixa de diálogo relacionados Olá fornece dois métodos diferentes tooreset uma palavra-passe:</span><span class="sxs-lookup"><span data-stu-id="ee71c-287">hello related dialog provides two different methods tooreset a password:</span></span>

<span data-ttu-id="ee71c-288">**Repor palavra-passe** - selecione **requerem Olá utilizador tooreset a palavra-passe** tooallow Olá tooself-recuperação de utilizador, se tiver registado utilizador Olá para autenticação multifator.</span><span class="sxs-lookup"><span data-stu-id="ee71c-288">**Reset password** - Select **Require hello user tooreset their password** tooallow hello user tooself-recover if hello user has registered for multi-factor authentication.</span></span> <span data-ttu-id="ee71c-289">Durante a próximo início de sessão do utilizador Olá, utilizador de Olá será necessário toosolve uma autenticação multifator com êxito de desafio e a palavra-passe do toochange forçada, em seguida, Olá.</span><span class="sxs-lookup"><span data-stu-id="ee71c-289">During hello user's next sign-in, hello user will be required toosolve a multi-factor authentication challenge successfully and then, forced toochange hello password.</span></span> <span data-ttu-id="ee71c-290">Esta opção não está disponível se a conta de utilizador Olá já não está registada autenticação multifator.</span><span class="sxs-lookup"><span data-stu-id="ee71c-290">This option isn't available if hello user account is not already registered multi-factor authentication.</span></span>

<span data-ttu-id="ee71c-291">**Palavra-passe temporária** - selecione **gerar uma palavra-passe temporária** tooimmediately invalidar palavra-passe Olá existente e criar uma nova palavra-passe temporária utilizador Olá.</span><span class="sxs-lookup"><span data-stu-id="ee71c-291">**Temporary password** - Select **Generate a temporary password** tooimmediately invalidate hello existing password, and create a new temporary password for hello user.</span></span> <span data-ttu-id="ee71c-292">Envie Olá nova palavra-passe temporária tooan endereço de e-mail alternativo para o utilizador Olá ou o Gestor do utilizador toohello.</span><span class="sxs-lookup"><span data-stu-id="ee71c-292">Send hello new temporary password tooan alternate email address for hello user or toohello user's manager.</span></span> <span data-ttu-id="ee71c-293">Porque a palavra-passe de Olá é temporário, utilizador de Olá será palavra-passe Olá de toochange pedido após o início de sessão.</span><span class="sxs-lookup"><span data-stu-id="ee71c-293">Because hello password is temporary, hello user will be prompted toochange hello password upon sign-in.</span></span>

<span data-ttu-id="ee71c-294">![Política](./media/active-directory-identityprotection/1005.png "política")</span><span class="sxs-lookup"><span data-stu-id="ee71c-294">![Policy](./media/active-directory-identityprotection/1005.png "Policy")</span></span>

<span data-ttu-id="ee71c-295">**caixa de diálogo de configuração relacionados de Olá de tooopen**:</span><span class="sxs-lookup"><span data-stu-id="ee71c-295">**tooopen hello related configuration dialog**:</span></span>

1. <span data-ttu-id="ee71c-296">No Olá **do Azure AD Identity Protection** painel, clique em **utilizadores sinalizados para risco**.</span><span class="sxs-lookup"><span data-stu-id="ee71c-296">On hello **Azure AD Identity Protection** blade, click **Users flagged for risk**.</span></span>

    <span data-ttu-id="ee71c-297">![Reposição de palavra-passe manual](./media/active-directory-identityprotection/1006.png "reposição de palavra-passe Manual")</span><span class="sxs-lookup"><span data-stu-id="ee71c-297">![Manual password reset](./media/active-directory-identityprotection/1006.png "Manual password reset")</span></span>
2. <span data-ttu-id="ee71c-298">Na lista de Olá de utilizadores, selecione um utilizador com eventos de risco pelo menos um.</span><span class="sxs-lookup"><span data-stu-id="ee71c-298">From hello list of users, select a user with at least one risk events.</span></span>

    <span data-ttu-id="ee71c-299">![Reposição de palavra-passe manual](./media/active-directory-identityprotection/1007.png "reposição de palavra-passe Manual")</span><span class="sxs-lookup"><span data-stu-id="ee71c-299">![Manual password reset](./media/active-directory-identityprotection/1007.png "Manual password reset")</span></span>
3. <span data-ttu-id="ee71c-300">No painel de utilizador de Olá, clique em **Repor palavra-passe**.</span><span class="sxs-lookup"><span data-stu-id="ee71c-300">On hello user blade, click **Reset password**.</span></span>

    <span data-ttu-id="ee71c-301">![Reposição de palavra-passe manual](./media/active-directory-identityprotection/1008.png "reposição de palavra-passe Manual")</span><span class="sxs-lookup"><span data-stu-id="ee71c-301">![Manual password reset](./media/active-directory-identityprotection/1008.png "Manual password reset")</span></span>

### <a name="user-risk-security-policy"></a><span data-ttu-id="ee71c-302">Política de segurança de risco do utilizador</span><span class="sxs-lookup"><span data-stu-id="ee71c-302">User risk security policy</span></span>
<span data-ttu-id="ee71c-303">Uma política de segurança do utilizador risco é uma política de acesso condicional que avalia utilizador específico de tooa ao nível do risco de Olá e aplica as ações de remediação e atenuação com base nas condições predefinidas e as regras.</span><span class="sxs-lookup"><span data-stu-id="ee71c-303">A user risk security policy is a conditional access policy that evaluates hello risk level tooa specific user and applies remediation and mitigation actions based on predefined conditions and rules.</span></span>

<span data-ttu-id="ee71c-304">![Política do utilizador ridk](./media/active-directory-identityprotection/1009.png "ridk de política de utilizador")</span><span class="sxs-lookup"><span data-stu-id="ee71c-304">![User ridk policy](./media/active-directory-identityprotection/1009.png "User ridk policy")</span></span>

<span data-ttu-id="ee71c-305">Azure AD Identity Protection ajuda a gerir mitigação de Olá e remediação de utilizadores sinalizados para risco ao permitir-lhe:</span><span class="sxs-lookup"><span data-stu-id="ee71c-305">Azure AD Identity Protection helps you manage hello mitigation and remediation of users flagged for risk by enabling you to:</span></span>

* <span data-ttu-id="ee71c-306">Conjunto Olá utilizadores e grupos Olá política aplica-se a:</span><span class="sxs-lookup"><span data-stu-id="ee71c-306">Set hello users and groups hello policy applies to:</span></span>

    <span data-ttu-id="ee71c-307">![Política do utilizador ridk](./media/active-directory-identityprotection/1010.png "ridk de política de utilizador")</span><span class="sxs-lookup"><span data-stu-id="ee71c-307">![User ridk policy](./media/active-directory-identityprotection/1010.png "User ridk policy")</span></span>
* <span data-ttu-id="ee71c-308">Definir Olá utilizador risco nível limiar (baixa, média ou alta) que aciona a política de Olá:</span><span class="sxs-lookup"><span data-stu-id="ee71c-308">Set hello user risk level threshold (low, medium, or high) that triggers hello policy:</span></span>

    <span data-ttu-id="ee71c-309">![Política do utilizador ridk](./media/active-directory-identityprotection/1011.png "ridk de política de utilizador")</span><span class="sxs-lookup"><span data-stu-id="ee71c-309">![User ridk policy](./media/active-directory-identityprotection/1011.png "User ridk policy")</span></span>
* <span data-ttu-id="ee71c-310">Conjunto Olá controlos toobe imposta quando a política de Olá aciona:</span><span class="sxs-lookup"><span data-stu-id="ee71c-310">Set hello controls toobe enforced when hello policy triggers:</span></span>

    <span data-ttu-id="ee71c-311">![Política do utilizador ridk](./media/active-directory-identityprotection/1012.png "ridk de política de utilizador")</span><span class="sxs-lookup"><span data-stu-id="ee71c-311">![User ridk policy](./media/active-directory-identityprotection/1012.png "User ridk policy")</span></span>
* <span data-ttu-id="ee71c-312">Estado do comutador Olá da sua política:</span><span class="sxs-lookup"><span data-stu-id="ee71c-312">Switch hello state of your policy:</span></span>

    <span data-ttu-id="ee71c-313">![Política do utilizador ridk](./media/active-directory-identityprotection/403.png "registo do MFA")</span><span class="sxs-lookup"><span data-stu-id="ee71c-313">![User ridk policy](./media/active-directory-identityprotection/403.png "MFA Registration")</span></span>
* <span data-ttu-id="ee71c-314">Rever e avaliar o impacto de Olá uma alteração antes de ativar esta:</span><span class="sxs-lookup"><span data-stu-id="ee71c-314">Review and evaluate hello impact of a change before activating it:</span></span>

    <span data-ttu-id="ee71c-315">![Política do utilizador ridk](./media/active-directory-identityprotection/1013.png "ridk de política de utilizador")</span><span class="sxs-lookup"><span data-stu-id="ee71c-315">![User ridk policy](./media/active-directory-identityprotection/1013.png "User ridk policy")</span></span>

<span data-ttu-id="ee71c-316">Escolher um **elevada** limiar reduz o número de Olá de vezes que uma política é acionada e minimiza Olá impacto toousers.</span><span class="sxs-lookup"><span data-stu-id="ee71c-316">Choosing a **High** threshold reduces hello number of times a policy is triggered and minimizes hello impact toousers.</span></span>
<span data-ttu-id="ee71c-317">No entanto, exclui **baixa** e **média** utilizadores sinalizados para risco de política de Olá, que poderá não segura identidades ou dispositivos que foram anteriormente suspeito ou conhecidos toobe comprometido.</span><span class="sxs-lookup"><span data-stu-id="ee71c-317">However, it excludes **Low** and **Medium** users flagged for risk from hello policy, which may not secure identities or devices that were previously suspected or known toobe compromised.</span></span>

<span data-ttu-id="ee71c-318">Quando a definição Olá política,</span><span class="sxs-lookup"><span data-stu-id="ee71c-318">When setting hello policy,</span></span>

* <span data-ttu-id="ee71c-319">Excluir os utilizadores que são toogenerate provavelmente uma grande quantidade de Falso-positivos (programadores, os analistas de segurança)</span><span class="sxs-lookup"><span data-stu-id="ee71c-319">Exclude users who are likely toogenerate a lot of false-positives (developers, security analysts)</span></span>
* <span data-ttu-id="ee71c-320">Excluir utilizadores nas regiões onde o ativar política de Olá não é prático (por exemplo toohelpdesk sem acesso)</span><span class="sxs-lookup"><span data-stu-id="ee71c-320">Exclude users in locales where enabling hello policy is not practical (for example no access toohelpdesk)</span></span>
* <span data-ttu-id="ee71c-321">Utilize um **elevada** limiar durante a agregação de política iniciais, ou se tem minimizar desafios vistos pelos utilizadores finais.</span><span class="sxs-lookup"><span data-stu-id="ee71c-321">Use a **High** threshold during initial policy roll out, or if you must minimize challenges seen by end users.</span></span>
* <span data-ttu-id="ee71c-322">Utilize um **baixa** limiar se a sua organização precisar de maior segurança.</span><span class="sxs-lookup"><span data-stu-id="ee71c-322">Use a **Low** threshold if your organization requires greater security.</span></span> <span data-ttu-id="ee71c-323">Selecionar um **baixa** limiar apresenta utilizador adicionais início de sessão desafios, mas uma maior segurança.</span><span class="sxs-lookup"><span data-stu-id="ee71c-323">Selecting a **Low** threshold introduces additional user sign-in challenges, but increased security.</span></span>

<span data-ttu-id="ee71c-324">Olá recomendado predefinido para a maioria das organizações é tooconfigure uma regra para um **média** limiar toostrike um equilíbrio entre capacidade de utilização e segurança.</span><span class="sxs-lookup"><span data-stu-id="ee71c-324">hello recommended default for most organizations is tooconfigure a rule for a **Medium** threshold toostrike a balance between usability and security.</span></span>

<span data-ttu-id="ee71c-325">Para obter uma descrição geral de Olá relacionadas com a experiência de utilizador, consulte:</span><span class="sxs-lookup"><span data-stu-id="ee71c-325">For an overview of hello related user experience, see:</span></span>

* <span data-ttu-id="ee71c-326">[Comprometido fluxo da recuperação de conta](active-directory-identityprotection-flows.md#compromised-account-recovery).</span><span class="sxs-lookup"><span data-stu-id="ee71c-326">[Compromised account recovery flow](active-directory-identityprotection-flows.md#compromised-account-recovery).</span></span>  
* <span data-ttu-id="ee71c-327">[Comprometido fluxo conta bloqueada](active-directory-identityprotection-flows.md#compromised-account-blocked).</span><span class="sxs-lookup"><span data-stu-id="ee71c-327">[Compromised account blocked flow](active-directory-identityprotection-flows.md#compromised-account-blocked).</span></span>  

<span data-ttu-id="ee71c-328">**caixa de diálogo de configuração relacionados de Olá de tooopen**:</span><span class="sxs-lookup"><span data-stu-id="ee71c-328">**tooopen hello related configuration dialog**:</span></span>

- <span data-ttu-id="ee71c-329">No Olá **do Azure AD Identity Protection** painel, no Olá **configurar** secção, clique em **política do utilizador risco**.</span><span class="sxs-lookup"><span data-stu-id="ee71c-329">On hello **Azure AD Identity Protection** blade, in hello **Configure** section, click **User risk policy**.</span></span>

    <span data-ttu-id="ee71c-330">![Política do utilizador ridk](./media/active-directory-identityprotection/1009.png "ridk de política de utilizador")</span><span class="sxs-lookup"><span data-stu-id="ee71c-330">![User ridk policy](./media/active-directory-identityprotection/1009.png "User ridk policy")</span></span>

### <a name="mitigating-user-risk-events"></a><span data-ttu-id="ee71c-331">Mitigar os eventos de risco do utilizador</span><span class="sxs-lookup"><span data-stu-id="ee71c-331">Mitigating user risk events</span></span>
<span data-ttu-id="ee71c-332">Os administradores podem definir um utilizador risco política tooblock os utilizadores de segurança após o início de sessão, dependendo do nível de risco Olá.</span><span class="sxs-lookup"><span data-stu-id="ee71c-332">Administrators can set a user risk security policy tooblock users upon sign-in depending on hello risk level.</span></span>

<span data-ttu-id="ee71c-333">Bloquear um início de sessão:</span><span class="sxs-lookup"><span data-stu-id="ee71c-333">Blocking a sign-in:</span></span>

* <span data-ttu-id="ee71c-334">Impede a geração de Olá novo utilizador de eventos de risco para o utilizador Olá afetado</span><span class="sxs-lookup"><span data-stu-id="ee71c-334">Prevents hello generation of new user risk events for hello affected user</span></span>
* <span data-ttu-id="ee71c-335">Permite que os administradores toomanually remediar eventos de risco Olá que afetam a identidade do utilizador Olá e restaurá-lo Estado segura tooa</span><span class="sxs-lookup"><span data-stu-id="ee71c-335">Enables administrators toomanually remediate hello risk events affecting hello user's identity and restore it tooa secure state</span></span>



## <a name="multi-factor-authentication-registration-policy"></a><span data-ttu-id="ee71c-336">Política de registo de autenticação multifator</span><span class="sxs-lookup"><span data-stu-id="ee71c-336">Multi-factor authentication registration policy</span></span>
<span data-ttu-id="ee71c-337">A autenticação multifator do Azure é um método de verificar que é que requer a utilização de Olá de mais do que apenas um nome de utilizador e palavra-passe.</span><span class="sxs-lookup"><span data-stu-id="ee71c-337">Azure multi-factor authentication is a method of verifying who you are that requires hello use of more than just a username and password.</span></span> <span data-ttu-id="ee71c-338">Fornece uma segunda camada de segurança toouser inícios de sessão e transações.</span><span class="sxs-lookup"><span data-stu-id="ee71c-338">It provides a second layer of security toouser sign-ins and transactions.</span></span>  
<span data-ttu-id="ee71c-339">Recomendamos que necessitam do Azure multi-factor authentication para inícios de sessão de utilizador porque esta:</span><span class="sxs-lookup"><span data-stu-id="ee71c-339">We recommend that you require Azure multi-factor authentication for user sign-ins because it:</span></span>

* <span data-ttu-id="ee71c-340">Fornece autenticação forte com uma gama de opções de verificação fácil</span><span class="sxs-lookup"><span data-stu-id="ee71c-340">Delivers strong authentication with a range of easy verification options</span></span>
* <span data-ttu-id="ee71c-341">Desempenha uma função de chave na preparação da sua organização tooprotect e recuperar os compromissos de conta</span><span class="sxs-lookup"><span data-stu-id="ee71c-341">Plays a key role in preparing your organization tooprotect and recover from account compromises</span></span>

<span data-ttu-id="ee71c-342">![Política do utilizador ridk](./media/active-directory-identityprotection/1019.png "ridk de política de utilizador")</span><span class="sxs-lookup"><span data-stu-id="ee71c-342">![User ridk policy](./media/active-directory-identityprotection/1019.png "User ridk policy")</span></span>

<span data-ttu-id="ee71c-343">Para obter mais detalhes, consulte [que é o Azure multi-factor Authentication?](../multi-factor-authentication/multi-factor-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="ee71c-343">For more details, see [What is Azure Multi-Factor Authentication?](../multi-factor-authentication/multi-factor-authentication.md)</span></span>

<span data-ttu-id="ee71c-344">Azure AD Identity Protection ajuda a gerir Olá roll-out do registo de autenticação multifator ao configurar uma política que permite-lhe:</span><span class="sxs-lookup"><span data-stu-id="ee71c-344">Azure AD Identity Protection helps you manage hello roll-out of multi-factor authentication registration by configuring a policy that enables you to:</span></span>

* <span data-ttu-id="ee71c-345">Conjunto Olá utilizadores e grupos Olá política aplica-se a:</span><span class="sxs-lookup"><span data-stu-id="ee71c-345">Set hello users and groups hello policy applies to:</span></span>

    <span data-ttu-id="ee71c-346">![Política da MFA](./media/active-directory-identityprotection/1020.png "política da MFA")</span><span class="sxs-lookup"><span data-stu-id="ee71c-346">![MFA policy](./media/active-directory-identityprotection/1020.png "MFA policy")</span></span>
* <span data-ttu-id="ee71c-347">Conjunto Olá controlos toobe imposta quando a política de Olá aciona::</span><span class="sxs-lookup"><span data-stu-id="ee71c-347">Set hello controls toobe enforced when hello policy triggers::</span></span>  

    <span data-ttu-id="ee71c-348">![Política da MFA](./media/active-directory-identityprotection/1021.png "política da MFA")</span><span class="sxs-lookup"><span data-stu-id="ee71c-348">![MFA policy](./media/active-directory-identityprotection/1021.png "MFA policy")</span></span>
* <span data-ttu-id="ee71c-349">Estado do comutador Olá da sua política:</span><span class="sxs-lookup"><span data-stu-id="ee71c-349">Switch hello state of your policy:</span></span>

    <span data-ttu-id="ee71c-350">![Política da MFA](./media/active-directory-identityprotection/403.png "política da MFA")</span><span class="sxs-lookup"><span data-stu-id="ee71c-350">![MFA policy](./media/active-directory-identityprotection/403.png "MFA policy")</span></span>
* <span data-ttu-id="ee71c-351">Ver o estado do registo atual Olá:</span><span class="sxs-lookup"><span data-stu-id="ee71c-351">View hello current registration status:</span></span>

    <span data-ttu-id="ee71c-352">![Política da MFA](./media/active-directory-identityprotection/1022.png "política da MFA")</span><span class="sxs-lookup"><span data-stu-id="ee71c-352">![MFA policy](./media/active-directory-identityprotection/1022.png "MFA policy")</span></span>

<span data-ttu-id="ee71c-353">Para obter uma descrição geral de Olá relacionadas com a experiência de utilizador, consulte:</span><span class="sxs-lookup"><span data-stu-id="ee71c-353">For an overview of hello related user experience, see:</span></span>

* <span data-ttu-id="ee71c-354">[Fluxo de registo de autenticação multifator](active-directory-identityprotection-flows.md#multi-factor-authentication-registration).</span><span class="sxs-lookup"><span data-stu-id="ee71c-354">[Multi-factor authentication registration flow](active-directory-identityprotection-flows.md#multi-factor-authentication-registration).</span></span>  
* <span data-ttu-id="ee71c-355">[Início de sessão experiências com o Azure AD Identity Protection](active-directory-identityprotection-flows.md).</span><span class="sxs-lookup"><span data-stu-id="ee71c-355">[Sign-in experiences with Azure AD Identity Protection](active-directory-identityprotection-flows.md).</span></span>  

<span data-ttu-id="ee71c-356">**caixa de diálogo de configuração relacionados de Olá de tooopen**:</span><span class="sxs-lookup"><span data-stu-id="ee71c-356">**tooopen hello related configuration dialog**:</span></span>

- <span data-ttu-id="ee71c-357">No Olá **do Azure AD Identity Protection** painel, no Olá **configurar** secção, clique em **registo de multi-factor authentication**.</span><span class="sxs-lookup"><span data-stu-id="ee71c-357">On hello **Azure AD Identity Protection** blade, in hello **Configure** section, click **Multi-factor authentication registration**.</span></span>

    <span data-ttu-id="ee71c-358">![Política da MFA](./media/active-directory-identityprotection/1019.png "política da MFA")</span><span class="sxs-lookup"><span data-stu-id="ee71c-358">![MFA policy](./media/active-directory-identityprotection/1019.png "MFA policy")</span></span>

## <a name="next-steps"></a><span data-ttu-id="ee71c-359">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="ee71c-359">Next steps</span></span>
* [<span data-ttu-id="ee71c-360">Canal 9: Do Azure AD e mostrar de identidade: identidade pré-visualização de proteção</span><span class="sxs-lookup"><span data-stu-id="ee71c-360">Channel 9: Azure AD and Identity Show: Identity Protection Preview</span></span>](https://channel9.msdn.com/Series/Azure-AD-Identity/Azure-AD-and-Identity-Show-Identity-Protection-Preview)

* [<span data-ttu-id="ee71c-361">Ativar a proteção de identidade do Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ee71c-361">Enabling Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection-enable.md)

* [<span data-ttu-id="ee71c-362">Vulnerabilidades detetadas pelo Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="ee71c-362">Vulnerabilities detected by Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection-vulnerabilities.md)

* [<span data-ttu-id="ee71c-363">Eventos de risco do Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ee71c-363">Azure Active Directory risk events</span></span>](active-directory-identity-protection-risk-events.md)

* [<span data-ttu-id="ee71c-364">Notificações de proteção de identidade do Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="ee71c-364">Azure Active Directory Identity Protection notifications</span></span>](active-directory-identityprotection-notifications.md)

* [<span data-ttu-id="ee71c-365">Azure Active Directory Identity Protection manual de comunicação social</span><span class="sxs-lookup"><span data-stu-id="ee71c-365">Azure Active Directory Identity Protection playbook</span></span>](active-directory-identityprotection-playbook.md)

* [<span data-ttu-id="ee71c-366">Glossário do Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="ee71c-366">Azure Active Directory Identity Protection glossary</span></span>](active-directory-identityprotection-glossary.md)

* [<span data-ttu-id="ee71c-367">Início de sessão experiências com o Azure AD Identity Protection</span><span class="sxs-lookup"><span data-stu-id="ee71c-367">Sign-in experiences with Azure AD Identity Protection</span></span>](active-directory-identityprotection-flows.md)

* [<span data-ttu-id="ee71c-368">Proteção do Azure Active Directory identidade - como toounblock utilizadores</span><span class="sxs-lookup"><span data-stu-id="ee71c-368">Azure Active Directory Identity Protection - How toounblock users</span></span>](active-directory-identityprotection-unblock-howto.md)

* [<span data-ttu-id="ee71c-369">Introdução ao Azure Active Directory Identity Protection e o Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="ee71c-369">Get started with Azure Active Directory Identity Protection and Microsoft Graph</span></span>](active-directory-identityprotection-graph-getting-started.md)
