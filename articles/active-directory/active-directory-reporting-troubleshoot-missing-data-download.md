---
title: "Resolução de problemas: Os dados em falta no Olá transferido registos de atividade do Azure Active Directory | Microsoft Docs"
description: "Fornece dados de toomissing uma resolução nos registos de atividade transferidos do Azure Active Directory."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: ffce7eb1-99da-4ea7-9c4d-2322b755c8ce
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/15/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 027b70e6efc570f81d3c836f50ee52aaa89be71a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="i-cant-find-any-data-in-hello-azure-active-directory-activity-logs-i-have-downloaded"></a><span data-ttu-id="05e38-103">Não é possível localizar a quaisquer dados nos registos de atividade do Azure Active Directory do Olá que posso ter transferido</span><span class="sxs-lookup"><span data-stu-id="05e38-103">I can’t find any data in hello Azure Active Directory activity logs I have downloaded</span></span>


## <a name="symptoms"></a><span data-ttu-id="05e38-104">Sintomas</span><span class="sxs-lookup"><span data-stu-id="05e38-104">Symptoms</span></span>

<span data-ttu-id="05e38-105">Transferido a registos de atividade Olá (auditoria ou inícios de sessão) e não vejo todos os registos de Olá durante o período de tempo de Olá que devo escolher.</span><span class="sxs-lookup"><span data-stu-id="05e38-105">I downloaded hello activity logs (audit or sign-ins) and I don’t see all hello records for hello time I chose.</span></span> <span data-ttu-id="05e38-106">Porquê?</span><span class="sxs-lookup"><span data-stu-id="05e38-106">Why?</span></span> 

 ![Relatórios](./media/active-directory-reporting-troubleshoot-missing-data-download/01.png)
 

## <a name="cause"></a><span data-ttu-id="05e38-108">Causa</span><span class="sxs-lookup"><span data-stu-id="05e38-108">Cause</span></span>

<span data-ttu-id="05e38-109">Quando transferir os registos de atividade no portal do Azure de Olá, limitamos registos too120K escala Olá, ordenados por mais recente.</span><span class="sxs-lookup"><span data-stu-id="05e38-109">When you download activity logs in hello Azure portal, we limit hello scale too120K records, sorted by most recent.</span></span> 

## <a name="resolution"></a><span data-ttu-id="05e38-110">Resolução</span><span class="sxs-lookup"><span data-stu-id="05e38-110">Resolution</span></span>

<span data-ttu-id="05e38-111">Pode tirar partido [APIs de relatórios do Azure AD](active-directory-reporting-api-getting-started.md) toofetch segurança tooa milhões de registos em qualquer momento especificado.</span><span class="sxs-lookup"><span data-stu-id="05e38-111">You can leverage [Azure AD Reporting APIs](active-directory-reporting-api-getting-started.md) toofetch up tooa million records at any given point.</span></span> <span data-ttu-id="05e38-112">A nossa abordagem recomendada é toorun um script de forma agendada que chama Olá relatórios APIs toofetch regista de forma incremental durante um período de tempo (por exemplo, diária ou semanalmente).</span><span class="sxs-lookup"><span data-stu-id="05e38-112">Our recommended approach is toorun a script on a scheduled basis that calls hello reporting APIs toofetch records in an incremental fashion over a period of time (e.g., daily or weekly).</span></span>

## <a name="next-steps"></a><span data-ttu-id="05e38-113">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="05e38-113">Next steps</span></span>
<span data-ttu-id="05e38-114">Consulte Olá [Azure Active Directory reporting FAQ](active-directory-reporting-faq.md).</span><span class="sxs-lookup"><span data-stu-id="05e38-114">See hello [Azure Active Directory reporting FAQ](active-directory-reporting-faq.md).</span></span>

