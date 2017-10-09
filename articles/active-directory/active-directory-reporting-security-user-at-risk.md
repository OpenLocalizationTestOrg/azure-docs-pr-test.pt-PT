---
title: "aaaUsers sinalizados para o relatório de segurança de risco no portal do Azure Active Directory Olá | Microsoft Docs"
description: "Saiba mais sobre os utilizadores Olá sinalizados para o relatório de segurança de risco no portal do Azure Active Directory Olá"
services: active-directory
author: MarkusVi
manager: femila
ms.assetid: addd60fe-d5ac-4b8b-983c-0736c80ace02
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/24/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 5077cd61d6119745a85ed712623904633a151331
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="users-flagged-for-risk-security-report-in-hello-azure-active-directory-portal"></a>Utilizadores sinalizados para o relatório de segurança de risco no portal do Azure Active Directory Olá

Com os relatórios de segurança de Olá no Olá Azure Active Directory (Azure AD), pode obter informações acerca da probabilidade Olá de contas de utilizador comprometidas no seu ambiente. 

Azure Active Directory Deteta suspeitas ações que estão relacionados tooyour contas de utilizador. Para cada ação detetada, é criado um registo denominado *evento de risco*. Para obter mais informações, consulte [Eventos de risco do Azure Active Directory](active-directory-identity-protection-risk-events.md). 

Olá detetou eventos de risco são toocalculate utilizado:

- **Inícios de sessão arriscados** -um risco início de sessão é um indicador para uma tentativa de início de sessão que poderão ter sido executada por alguém que não é proprietário legítimos Olá uma conta de utilizador. Para obter mais informações, veja [Inícios de sessão arriscados](active-directory-identityprotection.md#risky-sign-ins). 

- **Utilizadores sinalizados para risco** – Um utilizador de risco é um indicador de uma conta de utilizador que pode ter sido comprometida. Para obter mais informações, veja [Utilizadores sinalizados para risco](active-directory-identityprotection.md#users-flagged-for-risk).  

Olá portal do Azure, pode encontrar os relatórios de segurança de Olá no Olá **do Azure Active Directory** painel no Olá **segurança** secção.  

![Inícios de Sessão de Risco](./media/active-directory-reporting-security-user-at-risk/10.png)



## <a name="what-azure-ad-license-do-you-need-tooaccess-a-security-report"></a>As licenças do Azure AD tem tooaccess um relatório de segurança?  

Todas as edições do Azure Active Directory disponibilizam os relatórios de utilizadores sinalizados para risco.  
No entanto, o nível de Olá de granularidade do relatório varia entre edições Olá: 

- No Olá **edições gratuito do Azure Active Directory e Basic**, já a obter uma lista de utilizadores sinalizados para risco. 

- Olá **do Azure Active Directory Premium 1** edição expande este modelo, permitindo também tooexamine algumas das Olá subjacente eventos de risco que foram detetados para cada relatório. 

- Olá **do Azure Active Directory Premium 2** edição fornece-lhe Olá informações mais detalhadas sobre todos os eventos de risco subjacente e permite-lhe tooconfigure as políticas de segurança que respondam automaticamente tooconfigured risco níveis.



## <a name="azure-active-directory-free-and-basic-edition"></a>Edição gratuita e básica do Azure Active Directory

os utilizadores Olá sinalizados para o relatório de risco nas edições de livres e básicos do Azure Active Directory de Olá fornece uma lista de contas de utilizador que poderá ter sido comprometida. 


![Inícios de Sessão de Risco](./media/active-directory-reporting-security-user-at-risk/03.png)

Seleção de um utilizador abre o painel de dados de utilizador relacionadas Olá.
Para os utilizadores que estão em risco, pode rever o histórico de início de sessão do utilizador Olá e repor a palavra-passe de Olá, se necessário.

![Inícios de Sessão de Risco](./media/active-directory-reporting-security-user-at-risk/46.png)


Esta caixa de diálogo disponibiliza uma opção para:

- Transferir Olá relatório

- Procurar utilizadores

![Inícios de Sessão de Risco](./media/active-directory-reporting-security-user-at-risk/16.png)


## <a name="azure-active-directory-premium-editions"></a>Edições premium do Azure Active Directory

os utilizadores Olá sinalizados para o relatório de risco nas edições de premium do Azure Active Directory Olá fornece-lhe:

- Uma [lista de contas de utilizador](active-directory-identityprotection.md#users-flagged-for-risk) que poderão ter sido comprometidas 

- Agregar informações sobre Olá [tipos de eventos de risco](active-directory-identity-protection-risk-events.md) que foram detetadas

- Um relatório de Olá toodownload opção

- Uma opção tooconfigure um [política de remediação de risco do utilizador](active-directory-identityprotection.md#user-risk-security-policy)  


![Inícios de Sessão de Risco](./media/active-directory-reporting-security-user-at-risk/71.png)

Ao selecionar um utilizador, obtém uma vista de relatório detalhado para este utilizador que lhe permite:

- Abrir Olá que ver todos os inícios de sessão

- Repor palavra-passe do utilizador Olá

- Dispensar todos os eventos

- Investigue os eventos de risco comunicado para utilizador Olá. 


![Inícios de Sessão de Risco](./media/active-directory-reporting-security-user-at-risk/324.png)


tooinvestigate um evento de risco, selecione um Olá do Olá lista tooopen **detalhes** painel para este evento de risco. No Olá **detalhes** painel, tiver Olá opção tooeither [fechar manualmente um evento de risco](active-directory-identityprotection.md#closing-risk-events-manually) ou reativar um evento de risco fechado manualmente. 


![Inícios de Sessão de Risco](./media/active-directory-reporting-security-user-at-risk/325.png)



## <a name="next-steps"></a>Passos seguintes

- Para obter mais informações sobre o Azure Active Directory Identity Protection, veja [Azure Active Directory Identity Protection](active-directory-identityprotection.md).

