---
title: "relatório de inícios de sessão aaaRisky no portal do Azure Active Directory Olá | Microsoft Docs"
description: "Saiba mais sobre Olá arriscados inícios de sessão de relatórios no portal do Azure Active Directory Olá"
services: active-directory
author: MarkusVi
manager: femila
ms.assetid: 7728fcd7-3dd5-4b99-a0e4-949c69788c0f
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/24/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: d8df5cafea6b38f3e364c24a6aff599abe088e88
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="risky-sign-ins-report-in-hello-azure-active-directory-portal"></a>Relatório de risco inícios de sessão no portal do Azure Active Directory Olá

Com Olá relatórios de segurança no Azure Active Directory (Azure AD) pode obter informações sobre a probabilidade de Olá de contas de utilizador comprometidas no seu ambiente. 

Azure AD Deteta suspeitas ações que estão relacionados tooyour contas de utilizador. Para cada ação detetada, é criado um registo denominado *evento de risco*. Para obter mais detalhes, veja [Eventos de risco do Azure Active Directory](active-directory-identity-protection-risk-events.md). 

Olá detetou eventos de risco são toocalculate utilizado:

- **Inícios de sessão arriscados** -um risco início de sessão é um indicador para uma tentativa de início de sessão que poderão ter sido executada por alguém que não é proprietário legítimos Olá uma conta de utilizador. Para obter mais detalhes, veja [Inícios de sessão de risco](active-directory-identityprotection.md#risky-sign-ins). 

- **Utilizadores sinalizados para risco** – Um utilizador de risco é um indicador de uma conta de utilizador que pode ter sido comprometida. Para obter mais detalhes, veja [Utilizadores sinalizados para risco](active-directory-identityprotection.md#users-flagged-for-risk).  

No [Olá portal do Azure](https://portal.azure.com), pode encontrar os relatórios de segurança de Olá no Olá **do Azure Active Directory** painel no Olá **segurança** secção. 

![Inícios de Sessão de Risco](./media/active-directory-reporting-security-risky-sign-ins/10.png)


## <a name="what-azure-ad-license-do-you-need-tooaccess-a-security-report"></a>As licenças do Azure AD tem tooaccess um relatório de segurança?  

Todas as edições do Azure Active Directory disponibilizam os relatórios de inícios de sessão de risco.  
No entanto, o nível de Olá de granularidade do relatório varia entre edições Olá: 

- No Olá **edições gratuito do Azure Active Directory e Basic**, já a obter uma lista do risco de inícios de sessão. 

- Olá **do Azure Active Directory Premium 1** edição expande este modelo, permitindo também tooexamine algumas das Olá subjacente eventos de risco que foram detetados para cada relatório. 

- Olá **do Azure Active Directory Premium 2** edição fornece-lhe Olá mais informações detalhadas sobre todos os eventos de risco subjacente e também lhe permite tooconfigure as políticas de segurança que respondam automaticamente tooconfigured níveis de risco.



## <a name="azure-active-directory-free-and-basic-edition"></a>Edição gratuita e básica do Azure Active Directory

as edições basic e Olá do Azure Active Directory gratuito lhe fornecem uma lista de risco inícios de sessão que foram detetados para os seus utilizadores. Este relatório lista:

- **Utilizador** - hello nome de utilizador de Olá que foi utilizado durante a operação de início de sessão Olá
- **IP** -Olá endereço IP do dispositivo Olá que foi utilizado tooconnect tooAzure do Active Directory
- **Localização** -localização Olá utilizado tooconnect tooAzure do Active Directory
- **Hora de início de sessão** -tempo Olá quando Olá início de sessão foi efetuado
- **Estado** -Olá Estado Olá início de sessão


![Inícios de Sessão de Risco](./media/active-directory-reporting-security-risky-sign-ins/01.png)

Com base na sua investigação de Olá arriscados início de sessão, pode fornecer comentários tooAzure Active Directory no formulário de Olá seguintes ações:

- Resolver
- Marcar como falso positivo
- Ignorar
- Reativar

![Inícios de Sessão de Risco](./media/active-directory-reporting-security-risky-sign-ins/21.png)

Para obter mais detalhes, veja [Fechar eventos de risco manualmente](active-directory-identityprotection.md#closing-risk-events-manually).

Este relatório disponibiliza uma opção para:

- Pesquisar recursos
- Transferência de dados do relatório Olá


![Inícios de Sessão de Risco](./media/active-directory-reporting-security-risky-sign-ins/93.png)


## <a name="azure-active-directory-premium-editions"></a>Edições premium do Azure Active Directory

relatório de inícios de sessão arriscados Olá nas edições de premium do Azure Active Directory Olá fornece-lhe:

- Agregar informações sobre Olá [tipos de eventos de risco](active-directory-identity-protection-risk-events.md) que foram detetadas

- Um relatório de Olá toodownload opção


![Inícios de Sessão de Risco](./media/active-directory-reporting-security-risky-sign-ins/456.png)


Ao selecionar um evento de risco, obtém uma vista de relatório detalhado para este evento de risco que lhe permite:

- Uma opção tooconfigure um [política de remediação de risco do utilizador](active-directory-identityprotection.md#user-risk-security-policy)  

- Reveja a linha cronológica de deteção de Olá para eventos de risco Olá  

- Reveja uma lista de utilizadores para os quais foi detetado este evento de risco

- [Feche manualmente eventos de risco](active-directory-identityprotection.md#closing-risk-events-manually) ou reative um evento de risco fechado manualmente. 


![Inícios de Sessão de Risco](./media/active-directory-reporting-security-risky-sign-ins/457.png)

Ao selecionar um utilizador, obtém uma vista de relatório detalhado para este utilizador que lhe permite:

- Abrir Olá que ver todos os inícios de sessão

- Repor palavra-passe do utilizador Olá

- Dispensar todos os eventos

- Investigue os eventos de risco comunicado para utilizador Olá. 


![Inícios de Sessão de Risco](./media/active-directory-reporting-security-risky-sign-ins/324.png)


tooinvestigate um evento de risco, selecione um Olá na lista.  
Esta ação abre Olá **detalhes** painel para este evento de risco. No Olá **detalhes** painel, tiver Olá opção tooeither [fechar manualmente um evento de risco](active-directory-identityprotection.md#closing-risk-events-manually) ou reativar um evento de risco fechado manualmente. 


![Inícios de Sessão de Risco](./media/active-directory-reporting-security-risky-sign-ins/325.png)





## <a name="next-steps"></a>Passos seguintes

- Para obter mais informações sobre o Azure Active Directory Identity Protection, veja [Azure Active Directory Identity Protection](active-directory-identityprotection.md).

