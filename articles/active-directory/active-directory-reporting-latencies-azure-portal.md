---
title: "latências de relatórios de Active Directory aaaAzure | Microsoft Docs"
description: "Saiba mais sobre Olá período de tempo que demora a comunicar tooshow de eventos no portal do Azure"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 9b88958d-94a2-4f4b-a18c-616f0617a24e
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/15/2017
ms.author: markvi;dhanyahk
ms.reviewer: dhanyahk
ms.openlocfilehash: eee959331262ba59b313dd038cb54699dbef48a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-reporting-latencies"></a><span data-ttu-id="28a91-103">Azure Active Directory latências de relatórios</span><span class="sxs-lookup"><span data-stu-id="28a91-103">Azure Active Directory reporting latencies</span></span>

<span data-ttu-id="28a91-104">Com [reporting](active-directory-preview-explainer.md) no Azure Active Directory Olá, obtém todas as informações de Olá terá toodetermine como ambiente está a fazer.</span><span class="sxs-lookup"><span data-stu-id="28a91-104">With [reporting](active-directory-preview-explainer.md) in hello Azure Active Directory, you get all hello information you need toodetermine how your environment is doing.</span></span> <span data-ttu-id="28a91-105">Olá período de tempo que demora para relatórios tooshow de dados de cópia de segurança no portal do Azure de Olá também é conhecido como latência.</span><span class="sxs-lookup"><span data-stu-id="28a91-105">hello amount of time it takes for reporting data tooshow up in hello Azure portal is also known as latency.</span></span> 

<span data-ttu-id="28a91-106">Este tópico lista as informações de latência de Olá para Olá todas as categorias de relatórios no Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="28a91-106">This topic lists hello latency information for hello all reporting categories in hello Azure portal.</span></span> 


## <a name="activity-reports"></a><span data-ttu-id="28a91-107">Relatórios de atividade</span><span class="sxs-lookup"><span data-stu-id="28a91-107">Activity reports</span></span>

<span data-ttu-id="28a91-108">Existem duas áreas de criação de relatórios de atividade:</span><span class="sxs-lookup"><span data-stu-id="28a91-108">There are two areas of activity reporting:</span></span>

- <span data-ttu-id="28a91-109">**As atividades de início de sessão** – informações sobre a utilização de Olá de aplicações geridas e as atividades de início de sessão de utilizador</span><span class="sxs-lookup"><span data-stu-id="28a91-109">**Sign-in activities** – Information about hello usage of managed applications and user sign-in activities</span></span>
- <span data-ttu-id="28a91-110">**Registos de auditoria** - informações de atividades do sistema sobre gestão de utilizadores e de grupos, as suas aplicações geridas e atividades de diretório</span><span class="sxs-lookup"><span data-stu-id="28a91-110">**Audit logs** - System activity information about users and group management, your managed applications and directory activities</span></span>

<span data-ttu-id="28a91-111">Olá, a tabela seguinte lista as informações de latência de Olá para relatórios de atividade.</span><span class="sxs-lookup"><span data-stu-id="28a91-111">hello following table lists hello latency information for activity reports.</span></span>

| <span data-ttu-id="28a91-112">Relatório</span><span class="sxs-lookup"><span data-stu-id="28a91-112">Report</span></span> | <span data-ttu-id="28a91-113">Mínimo</span><span class="sxs-lookup"><span data-stu-id="28a91-113">Minimum</span></span> | <span data-ttu-id="28a91-114">Média</span><span class="sxs-lookup"><span data-stu-id="28a91-114">Average</span></span> | <span data-ttu-id="28a91-115">Máximo</span><span class="sxs-lookup"><span data-stu-id="28a91-115">Maximum</span></span> |
| :-- | --- | --- | --- |
| <span data-ttu-id="28a91-116">Registos de auditoria</span><span class="sxs-lookup"><span data-stu-id="28a91-116">Audit logs</span></span>             | <span data-ttu-id="28a91-117">30 minutos</span><span class="sxs-lookup"><span data-stu-id="28a91-117">30 minutes</span></span>  | <span data-ttu-id="28a91-118">45 minutos</span><span class="sxs-lookup"><span data-stu-id="28a91-118">45 Minutes</span></span> | <span data-ttu-id="28a91-119">1 hora</span><span class="sxs-lookup"><span data-stu-id="28a91-119">1 hour</span></span>     |
| <span data-ttu-id="28a91-120">Inícios de sessão</span><span class="sxs-lookup"><span data-stu-id="28a91-120">Sign-ins</span></span>               | <span data-ttu-id="28a91-121">15 minutos</span><span class="sxs-lookup"><span data-stu-id="28a91-121">15 minutes</span></span>  | <span data-ttu-id="28a91-122">15 minutos</span><span class="sxs-lookup"><span data-stu-id="28a91-122">15 minutes</span></span> | <span data-ttu-id="28a91-123">2 horas *</span><span class="sxs-lookup"><span data-stu-id="28a91-123">2 hours*</span></span>   |

>[!NOTE]
> <span data-ttu-id="28a91-124">Para alguns dados de atividade de inícios de sessão provenientes das aplicações do office legado, pode demorar horas too8 Olá comunicar tooshow de dados.</span><span class="sxs-lookup"><span data-stu-id="28a91-124">For some sign-ins activity data coming from legacy office applications, it can take too8 hours for hello reporting data tooshow up.</span></span> 


## <a name="security-reports"></a><span data-ttu-id="28a91-125">Relatórios de segurança</span><span class="sxs-lookup"><span data-stu-id="28a91-125">Security reports</span></span>

<span data-ttu-id="28a91-126">Existem duas áreas de criação de relatórios de segurança:</span><span class="sxs-lookup"><span data-stu-id="28a91-126">There are two areas of security reporting:</span></span>

- <span data-ttu-id="28a91-127">**Inícios de sessão arriscados** -um risco início de sessão é um indicador para uma tentativa de início de sessão que poderão ter sido executada por alguém que não é proprietário legítimos Olá uma conta de utilizador.</span><span class="sxs-lookup"><span data-stu-id="28a91-127">**Risky sign-ins** - A risky sign-in is an indicator for a sign-in attempt that might have been performed by someone who is not hello legitimate owner of a user account.</span></span> 
- <span data-ttu-id="28a91-128">**Utilizadores sinalizados para risco** – Um utilizador de risco é um indicador de uma conta de utilizador que pode ter sido comprometida.</span><span class="sxs-lookup"><span data-stu-id="28a91-128">**Users flagged for risk** - A risky user is an indicator for a user account that might have been compromised.</span></span> 

<span data-ttu-id="28a91-129">Olá, a tabela seguinte lista as informações de latência de Olá para relatórios de segurança.</span><span class="sxs-lookup"><span data-stu-id="28a91-129">hello following table lists hello latency information for security reports.</span></span>

| <span data-ttu-id="28a91-130">Relatório</span><span class="sxs-lookup"><span data-stu-id="28a91-130">Report</span></span> | <span data-ttu-id="28a91-131">Mínimo</span><span class="sxs-lookup"><span data-stu-id="28a91-131">Minimum</span></span> | <span data-ttu-id="28a91-132">Média</span><span class="sxs-lookup"><span data-stu-id="28a91-132">Average</span></span> | <span data-ttu-id="28a91-133">Máximo</span><span class="sxs-lookup"><span data-stu-id="28a91-133">Maximum</span></span> |
| :-- | --- | --- | --- |
| <span data-ttu-id="28a91-134">Utilizadores em risco</span><span class="sxs-lookup"><span data-stu-id="28a91-134">Users at risk</span></span>          | <span data-ttu-id="28a91-135">5 minutos</span><span class="sxs-lookup"><span data-stu-id="28a91-135">5 minutes</span></span>   | <span data-ttu-id="28a91-136">15 minutos</span><span class="sxs-lookup"><span data-stu-id="28a91-136">15 minutes</span></span>  | <span data-ttu-id="28a91-137">2 horas</span><span class="sxs-lookup"><span data-stu-id="28a91-137">2 hours</span></span>  |
| <span data-ttu-id="28a91-138">Risco inícios de sessão</span><span class="sxs-lookup"><span data-stu-id="28a91-138">Risky sign-ins</span></span>         | <span data-ttu-id="28a91-139">5 minutos</span><span class="sxs-lookup"><span data-stu-id="28a91-139">5 minutes</span></span>   | <span data-ttu-id="28a91-140">15 minutos</span><span class="sxs-lookup"><span data-stu-id="28a91-140">15 minutes</span></span>  | <span data-ttu-id="28a91-141">2 horas</span><span class="sxs-lookup"><span data-stu-id="28a91-141">2 hours</span></span>  |

## <a name="risk-events"></a><span data-ttu-id="28a91-142">Eventos de risco</span><span class="sxs-lookup"><span data-stu-id="28a91-142">Risk events</span></span>

<span data-ttu-id="28a91-143">Azure Active Directory utiliza adaptável do machine learning algoritmos e heurística toodetect suspeitas ações que estão relacionados tooyour contas de utilizador.</span><span class="sxs-lookup"><span data-stu-id="28a91-143">Azure Active Directory uses adaptive machine learning algorithms and heuristics toodetect suspicious actions that are related tooyour user accounts.</span></span> <span data-ttu-id="28a91-144">Cada detetada ação suspeita é armazenada um evento de risco chamada de registo.</span><span class="sxs-lookup"><span data-stu-id="28a91-144">Each detected suspicious action is stored in a record called risk event.</span></span>

<span data-ttu-id="28a91-145">Olá, a tabela seguinte lista as informações de latência de Olá para eventos de risco.</span><span class="sxs-lookup"><span data-stu-id="28a91-145">hello following table lists hello latency information for risk events.</span></span>

| <span data-ttu-id="28a91-146">Relatório</span><span class="sxs-lookup"><span data-stu-id="28a91-146">Report</span></span> | <span data-ttu-id="28a91-147">Mínimo</span><span class="sxs-lookup"><span data-stu-id="28a91-147">Minimum</span></span> | <span data-ttu-id="28a91-148">Média</span><span class="sxs-lookup"><span data-stu-id="28a91-148">Average</span></span> | <span data-ttu-id="28a91-149">Máximo</span><span class="sxs-lookup"><span data-stu-id="28a91-149">Maximum</span></span> |
| :-- | --- | --- | --- |
| <span data-ttu-id="28a91-150">Inícios de sessão de endereços IP anónimos</span><span class="sxs-lookup"><span data-stu-id="28a91-150">Sign-ins from anonymous IP addresses</span></span> |<span data-ttu-id="28a91-151">5 minutos</span><span class="sxs-lookup"><span data-stu-id="28a91-151">5 minutes</span></span> |<span data-ttu-id="28a91-152">15 minutos</span><span class="sxs-lookup"><span data-stu-id="28a91-152">15 Minutes</span></span> |<span data-ttu-id="28a91-153">2 horas</span><span class="sxs-lookup"><span data-stu-id="28a91-153">2 hours</span></span> |
| <span data-ttu-id="28a91-154">Inícios de sessão a partir de localizações desconhecidas</span><span class="sxs-lookup"><span data-stu-id="28a91-154">Sign-ins from unfamiliar locations</span></span> |<span data-ttu-id="28a91-155">5 minutos</span><span class="sxs-lookup"><span data-stu-id="28a91-155">5 minutes</span></span> |<span data-ttu-id="28a91-156">15 minutos</span><span class="sxs-lookup"><span data-stu-id="28a91-156">15 Minutes</span></span> |<span data-ttu-id="28a91-157">2 horas</span><span class="sxs-lookup"><span data-stu-id="28a91-157">2 hours</span></span> |
| <span data-ttu-id="28a91-158">Utilizadores com credenciais obtidas ilicitamente</span><span class="sxs-lookup"><span data-stu-id="28a91-158">Users with leaked credentials</span></span> |<span data-ttu-id="28a91-159">2 horas</span><span class="sxs-lookup"><span data-stu-id="28a91-159">2 hours</span></span> |<span data-ttu-id="28a91-160">4 horas</span><span class="sxs-lookup"><span data-stu-id="28a91-160">4 hours</span></span> |<span data-ttu-id="28a91-161">8 horas</span><span class="sxs-lookup"><span data-stu-id="28a91-161">8 hours</span></span> |
| <span data-ttu-id="28a91-162">Impossível tooatypical localizações</span><span class="sxs-lookup"><span data-stu-id="28a91-162">Impossible travel tooatypical locations</span></span> |<span data-ttu-id="28a91-163">5 minutos</span><span class="sxs-lookup"><span data-stu-id="28a91-163">5 minutes</span></span> |<span data-ttu-id="28a91-164">1 hora</span><span class="sxs-lookup"><span data-stu-id="28a91-164">1 hour</span></span> |<span data-ttu-id="28a91-165">8 horas</span><span class="sxs-lookup"><span data-stu-id="28a91-165">8 hours</span></span>  |
| <span data-ttu-id="28a91-166">Inícios de sessão a partir de dispositivos infetados</span><span class="sxs-lookup"><span data-stu-id="28a91-166">Sign-ins from infected devices</span></span> |<span data-ttu-id="28a91-167">2 horas</span><span class="sxs-lookup"><span data-stu-id="28a91-167">2 hours</span></span> |<span data-ttu-id="28a91-168">4 horas</span><span class="sxs-lookup"><span data-stu-id="28a91-168">4 hours</span></span> |<span data-ttu-id="28a91-169">8 horas</span><span class="sxs-lookup"><span data-stu-id="28a91-169">8 hours</span></span>  |
| <span data-ttu-id="28a91-170">Inícios de sessão de endereços IP com atividade suspeita</span><span class="sxs-lookup"><span data-stu-id="28a91-170">Sign-ins from IP addresses with suspicious activity</span></span> |<span data-ttu-id="28a91-171">2 horas</span><span class="sxs-lookup"><span data-stu-id="28a91-171">2 hours</span></span> |<span data-ttu-id="28a91-172">4 horas</span><span class="sxs-lookup"><span data-stu-id="28a91-172">4 hours</span></span> |<span data-ttu-id="28a91-173">8 horas</span><span class="sxs-lookup"><span data-stu-id="28a91-173">8 hours</span></span>  |



## <a name="next-steps"></a><span data-ttu-id="28a91-174">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="28a91-174">Next steps</span></span>

<span data-ttu-id="28a91-175">Se quiser tooknow mais sobre os relatórios de atividade Olá no Olá portal do Azure, consulte:</span><span class="sxs-lookup"><span data-stu-id="28a91-175">If you want tooknow more about hello activity reports in hello Azure portal, see:</span></span>

- [<span data-ttu-id="28a91-176">Relatórios de atividade de início de sessão no portal do Azure Active Directory Olá</span><span class="sxs-lookup"><span data-stu-id="28a91-176">Sign-in activity reports in hello Azure Active Directory portal</span></span>](active-directory-reporting-activity-sign-ins.md)
- [<span data-ttu-id="28a91-177">Relatórios de atividade no portal do Azure Active Directory Olá de auditoria</span><span class="sxs-lookup"><span data-stu-id="28a91-177">Audit activity reports in hello Azure Active Directory portal</span></span>](active-directory-reporting-activity-audit-logs.md)

<span data-ttu-id="28a91-178">Se quiser tooknow mais sobre os relatórios de segurança de Olá no Olá portal do Azure, consulte:</span><span class="sxs-lookup"><span data-stu-id="28a91-178">If you want tooknow more about hello security reports in hello Azure portal, see:</span></span>

- [<span data-ttu-id="28a91-179">Utilizadores no relatório de segurança de risco no portal do Azure Active Directory Olá</span><span class="sxs-lookup"><span data-stu-id="28a91-179">Users at risk security report in hello Azure Active Directory portal</span></span>](active-directory-reporting-security-user-at-risk.md)
- [<span data-ttu-id="28a91-180">Relatório de risco inícios de sessão no portal do Azure Active Directory Olá</span><span class="sxs-lookup"><span data-stu-id="28a91-180">Risky sign-ins report in hello Azure Active Directory portal</span></span>](active-directory-reporting-security-risky-sign-ins.md)

<span data-ttu-id="28a91-181">Se pretender mais informações sobre eventos de risco tooknow, veja [eventos de risco do Azure Active Directory](active-directory-reporting-risk-events.md).</span><span class="sxs-lookup"><span data-stu-id="28a91-181">If you want tooknow more about risk events, see [Azure Active Directory risk events](active-directory-reporting-risk-events.md).</span></span>
