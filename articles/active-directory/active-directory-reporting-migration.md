---
title: "atividade aaaFind relatórios no portal do Azure de Olá | Microsoft Docs"
description: "Saiba como toofind atividade do Azure Active Directory relatórios no Olá portal do Azure."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: d93521f8-dc21-4feb-aaff-4bb300f04812
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/19/2017
ms.author: dhanyahk;markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: f8d7a968403e10ccc5319f27fedad38b1553ded0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="find-activity-reports-in-hello-azure-portal"></a>Localizar os relatórios de atividade no Olá portal do Azure

Se estiver a mover de Olá toohello de portal clássico do Azure portal do Azure, obtenha uma nova vista de olhos registos de atividade do Azure Active Directory (Azure AD). Num recente [blogue](https://blogs.technet.microsoft.com/enterprisemobility/2016/11/08/azuread-weve-just-turned-on-detailed-auditing-and-sign-in-logs-in-the-new-azure-portal/), vamos explicar como pode ver os registos de atividade no contexto de Olá do recurso de Olá está a trabalhar no Olá portal do Azure. Neste artigo, vamos descrever como toofind relatórios que utilizou no portal clássico do Azure no portal do Azure de Olá de Olá.

## <a name="whats-new"></a>Novidades

Relatórios no portal clássico do Azure de Olá estão separados em categorias:

1.  Relatórios de segurança
2.  Relatórios de atividade
3.  Relatórios de aplicação integrada

### <a name="activity-and-integrated-app-reports"></a>Atividade e os relatórios de aplicação integrada

Para baseado no contexto de relatórios no Olá portal do Azure, os relatórios existentes são intercalados numa única vista. Uma API único, subjacente fornece Olá dados toohello.

toosee esta vista, no Olá **do Azure Active Directory** painel, em **ATIVIDADE**, selecione **registos de auditoria**.

![Registos de auditoria](./media/active-directory-reporting-migration/482.png "Registos de auditoria")

Olá, os seguintes relatórios é consolidado nesta vista:

-   Relatório de auditoria
-   Atividade de reposição de palavra-passe
-   Atividade de registo de reposição de palavra-passe
-   Atividade de grupos self-service
-   Alterações de nome de grupo do Office 365
-   Atividade de aprovisionamento de contas
-   Estado de rollover de palavra-passe
-   Erros de aprovisionamento de contas


Olá relatório de utilização da aplicação foi melhorado e está incluído no Olá **inícios de sessão** vista. toosee esta vista, no Olá **do Azure Active Directory** painel, em **ATIVIDADE**, selecione **inícios de sessão**.

![Vista de inícios de sessão](./media/active-directory-reporting-migration/483.png "ver inícios de sessão")

Olá **inícios de sessão** vista inclui todos os utilizadores inícios de sessão. Pode utilizar estas informações de utilização de aplicação de tooget de informações. Também pode ver informações de utilização da aplicação no Olá **aplicações empresariais** descrição geral, no Olá **GERIR** secção.

![As aplicações empresariais](./media/active-directory-reporting-migration/484.png "aplicações da empresa")

## <a name="access-a-specific-report"></a>Aceder a um relatório específico

Embora Olá portal do Azure oferece uma vista única, também pode ver relatórios específicos.

### <a name="audit-logs"></a>Registos de auditoria

Em comentários de toocustomer de resposta, no Olá portal do Azure, pode utilizar avançada filtragem tooaccess Olá de dados que pretende. É um filtro pode utilizar um *categoria de atividade*, que apresenta uma lista de tipos diferentes de Olá da atividade de registo no Azure AD. toonarrow resulta toowhat que procura, pode selecionar uma categoria.

Por exemplo, se estiver interessado apenas em atividades reposições de relacionados tooself de palavra-passe, pode escolher Olá **gestão de palavras-passe Self-Service** categoria. categorias Olá que vir baseiam-se no recurso de Olá que está a trabalhar.  

![Opções de categorias na página de registos de auditoria de filtro de Olá](./media/active-directory-reporting-migration/06.png "opções de categorias na página de registos de auditoria de filtro de Olá")

Categorias de atividade incluem:

- Diretório do Núcleo
- Gestão de Palavra-passe Personalizada
- Gestão de Grupos Personalizada
- Aprovisionamento de Contas

### <a name="application-usage"></a>Utilização da aplicação

tooview detalhes sobre a utilização de aplicação para todas as aplicações ou para uma única aplicação em **ATIVIDADE**, selecione **inícios de sessão**. os resultados de Olá toonarrow, pode filtrar por nome de utilizador ou nome da aplicação.

![Página de início de sessão de eventos de filtro](./media/active-directory-reporting-migration/07.png "página Eventos de início de sessão de filtragem")

### <a name="security-reports"></a>Relatórios de segurança

#### <a name="azure-ad-anomalous-activity-reports"></a>Relatórios de atividade anómala do Azure AD

Segurança de atividade anómala do Azure AD relatórios a partir do portal clássico do Azure de Olá foram consolidado tooprovide-lhe uma, vista central. Esta vista mostra todos os eventos de risco relacionado com a segurança de que o do Azure AD pode detetar e comunicar.

Olá, a tabela seguinte apresenta uma lista de relatórios de segurança de atividade anómala Olá do Azure AD e tipos de eventos de risco correspondentes no Olá portal do Azure.

| Relatório de atividade anómala do Azure AD |  Tipo de evento de risco de proteção de identidade|
| :--- | :--- |
| Utilizadores com credenciais obtidas ilicitamente | Credenciais obtidas ilicitamente |
| Atividades irregulares de início de sessão | Impossível tooatypical localizações |
| Inícios de sessão de dispositivos possivelmente infetados | Inícios de sessão a partir de dispositivos infetados|
| Inícios de sessão de fontes desconhecidas | Inícios de sessão de endereços IP anónimos |
| Inícios de sessão de endereços IP com atividade suspeita | Inícios de sessão de endereços IP com atividade suspeita |
| - | Inícios de sessão a partir de localizações desconhecidas |

Olá segurança do Azure AD atividade anómala os seguintes relatórios não estão incluídos como eventos de risco no Olá portal do Azure:

* Inícios de sessão após várias falhas
* Inícios de sessão de várias localizações geográficas

Estes relatórios ainda estão disponíveis Olá portal clássico do Azure, mas que vão ser preteridas momento no Olá futura.

Para obter mais informações, consulte [Eventos de risco do Azure Active Directory](active-directory-identity-protection-risk-events.md).  


#### <a name="detected-risk-events"></a>Eventos de risco detetados

No portal do Azure Olá, pode aceder a relatórios sobre eventos de risco detetados no Olá **do Azure Active Directory** painel, em **segurança**. Eventos de risco detetados são controlados na Olá os seguintes relatórios:   

- Utilizadores em risco
- Inícios de Sessão de Risco

![Relatórios de segurança](./media/active-directory-reporting-migration/04.png "relatórios de segurança")

Para obter mais informações sobre os relatórios de segurança, consulte:

- [Utilizadores no relatório de segurança de risco no portal do Azure Active Directory Olá](active-directory-reporting-security-user-at-risk.md)
- [Risco relatório de inícios de sessão no portal do Azure Active Directory Olá](active-directory-reporting-security-risky-sign-ins.md)


## <a name="activity-reports-in-hello-azure-classic-portal-vs-hello-azure-portal"></a>Relatórios de atividade no Olá portal clássico do Azure vs Olá portal do Azure

tabela de Olá nesta secção apresenta uma lista de relatórios existentes no Olá portal clássico do Azure. Também descreve como obter Olá mesmas informações em Olá portal do Azure.

tooview todos os dados no Olá de auditoria **do Azure Active Directory** painel, em **ATIVIDADE**, aceda demasiado**registos de auditoria**.

![Registos de auditoria](./media/active-directory-reporting-migration/61.png "Registos de auditoria")

| Portal Clássico do Azure                 | toofind no Olá portal do Azure                                                         |
| ---                                  | ---                                                                        |
| Registos de auditoria                           | Para **categoria de atividade**, selecione **Core diretório**.                       |
| Atividade de reposição de palavra-passe              | Para **categoria de atividade**, selecione **gestão de palavras-passe Self-Service**. |
| Atividade de registo de reposição de palavra-passe | Para **categoria de atividade**, selecione **gestão de palavras-passe Self-Service**.     |
| Atividade de grupos self-service         | Para **categoria de atividade**, selecione **Self-Service de grupo de gestão**.        |
| Atividade de aprovisionamento de contas        | Para **categoria de atividade**, selecione **aprovisionamento de utilizador da conta**.         |
| Estado de rollover de palavra-passe             | Para **categoria de atividade**, selecione **Rollover de palavra-passe de aplicação automática**.      |
| Erros de aprovisionamento de contas          | Para **categoria de atividade**, selecione **aprovisionamento de utilizador da conta**.        |
| Alterações de nome de grupo do Office 365         | Para **categoria de atividade**, selecione **gestão de palavras-passe Self-Service**. Para **tipo de recurso de atividade**, selecione **grupo**. Para **atividade origem**, selecione **grupos do Office 365**.|

Olá tooview **utilização da aplicação** relatório, no Olá **do Azure Active Directory** painel, em **GERIR**, selecione **aplicações da empresa**e, em seguida, selecione **inícios de sessão**.


![Relatório de inícios de sessão do aplicações empresariais](./media/active-directory-reporting-migration/199.png "relatório Enterprise aplicações inícios de sessão")

## <a name="next-steps"></a>Passos seguintes

Para obter uma descrição geral de criação de relatórios, consulte Olá [relatórios do Azure Active Directory](active-directory-reporting-azure-portal.md).
