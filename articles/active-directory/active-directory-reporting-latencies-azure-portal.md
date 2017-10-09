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
# <a name="azure-active-directory-reporting-latencies"></a>Azure Active Directory latências de relatórios

Com [reporting](active-directory-preview-explainer.md) no Azure Active Directory Olá, obtém todas as informações de Olá terá toodetermine como ambiente está a fazer. Olá período de tempo que demora para relatórios tooshow de dados de cópia de segurança no portal do Azure de Olá também é conhecido como latência. 

Este tópico lista as informações de latência de Olá para Olá todas as categorias de relatórios no Olá portal do Azure. 


## <a name="activity-reports"></a>Relatórios de atividade

Existem duas áreas de criação de relatórios de atividade:

- **As atividades de início de sessão** – informações sobre a utilização de Olá de aplicações geridas e as atividades de início de sessão de utilizador
- **Registos de auditoria** - informações de atividades do sistema sobre gestão de utilizadores e de grupos, as suas aplicações geridas e atividades de diretório

Olá, a tabela seguinte lista as informações de latência de Olá para relatórios de atividade.

| Relatório | Mínimo | Média | Máximo |
| :-- | --- | --- | --- |
| Registos de auditoria             | 30 minutos  | 45 minutos | 1 hora     |
| Inícios de sessão               | 15 minutos  | 15 minutos | 2 horas *   |

>[!NOTE]
> Para alguns dados de atividade de inícios de sessão provenientes das aplicações do office legado, pode demorar horas too8 Olá comunicar tooshow de dados. 


## <a name="security-reports"></a>Relatórios de segurança

Existem duas áreas de criação de relatórios de segurança:

- **Inícios de sessão arriscados** -um risco início de sessão é um indicador para uma tentativa de início de sessão que poderão ter sido executada por alguém que não é proprietário legítimos Olá uma conta de utilizador. 
- **Utilizadores sinalizados para risco** – Um utilizador de risco é um indicador de uma conta de utilizador que pode ter sido comprometida. 

Olá, a tabela seguinte lista as informações de latência de Olá para relatórios de segurança.

| Relatório | Mínimo | Média | Máximo |
| :-- | --- | --- | --- |
| Utilizadores em risco          | 5 minutos   | 15 minutos  | 2 horas  |
| Risco inícios de sessão         | 5 minutos   | 15 minutos  | 2 horas  |

## <a name="risk-events"></a>Eventos de risco

Azure Active Directory utiliza adaptável do machine learning algoritmos e heurística toodetect suspeitas ações que estão relacionados tooyour contas de utilizador. Cada detetada ação suspeita é armazenada um evento de risco chamada de registo.

Olá, a tabela seguinte lista as informações de latência de Olá para eventos de risco.

| Relatório | Mínimo | Média | Máximo |
| :-- | --- | --- | --- |
| Inícios de sessão de endereços IP anónimos |5 minutos |15 minutos |2 horas |
| Inícios de sessão a partir de localizações desconhecidas |5 minutos |15 minutos |2 horas |
| Utilizadores com credenciais obtidas ilicitamente |2 horas |4 horas |8 horas |
| Impossível tooatypical localizações |5 minutos |1 hora |8 horas  |
| Inícios de sessão a partir de dispositivos infetados |2 horas |4 horas |8 horas  |
| Inícios de sessão de endereços IP com atividade suspeita |2 horas |4 horas |8 horas  |



## <a name="next-steps"></a>Passos seguintes

Se quiser tooknow mais sobre os relatórios de atividade Olá no Olá portal do Azure, consulte:

- [Relatórios de atividade de início de sessão no portal do Azure Active Directory Olá](active-directory-reporting-activity-sign-ins.md)
- [Relatórios de atividade no portal do Azure Active Directory Olá de auditoria](active-directory-reporting-activity-audit-logs.md)

Se quiser tooknow mais sobre os relatórios de segurança de Olá no Olá portal do Azure, consulte:

- [Utilizadores no relatório de segurança de risco no portal do Azure Active Directory Olá](active-directory-reporting-security-user-at-risk.md)
- [Relatório de risco inícios de sessão no portal do Azure Active Directory Olá](active-directory-reporting-security-risky-sign-ins.md)

Se pretender mais informações sobre eventos de risco tooknow, veja [eventos de risco do Azure Active Directory](active-directory-reporting-risk-events.md).
