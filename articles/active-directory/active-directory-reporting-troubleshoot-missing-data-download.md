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
# <a name="i-cant-find-any-data-in-hello-azure-active-directory-activity-logs-i-have-downloaded"></a>Não é possível localizar a quaisquer dados nos registos de atividade do Azure Active Directory do Olá que posso ter transferido


## <a name="symptoms"></a>Sintomas

Transferido a registos de atividade Olá (auditoria ou inícios de sessão) e não vejo todos os registos de Olá durante o período de tempo de Olá que devo escolher. Porquê? 

 ![Relatórios](./media/active-directory-reporting-troubleshoot-missing-data-download/01.png)
 

## <a name="cause"></a>Causa

Quando transferir os registos de atividade no portal do Azure de Olá, limitamos registos too120K escala Olá, ordenados por mais recente. 

## <a name="resolution"></a>Resolução

Pode tirar partido [APIs de relatórios do Azure AD](active-directory-reporting-api-getting-started.md) toofetch segurança tooa milhões de registos em qualquer momento especificado. A nossa abordagem recomendada é toorun um script de forma agendada que chama Olá relatórios APIs toofetch regista de forma incremental durante um período de tempo (por exemplo, diária ou semanalmente).

## <a name="next-steps"></a>Passos seguintes
Consulte Olá [Azure Active Directory reporting FAQ](active-directory-reporting-faq.md).

