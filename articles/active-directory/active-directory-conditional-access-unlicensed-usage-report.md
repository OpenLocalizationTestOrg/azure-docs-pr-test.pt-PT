---
title: "aaaUnlicensed relatório de utilização | Microsoft Docs"
description: "Olá, relatório de utilização não autorizada paga de ajuda a que identificar os utilizadores sem licença que estão a utilizar funcionalidades do Azure AD."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 92138f43-9528-4c8a-b834-66a47da476e3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: markvi
ms.openlocfilehash: c44d1756b4641d7ca88434017eedb6c5e2567cb0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="unlicensed-usage-report"></a>Relatório de utilização não autorizada
Olá, relatório de utilização não autorizada paga de ajuda a que identificar os utilizadores sem licença que estão a utilizar funcionalidades do Azure AD. Isto permite-lhe toomake utilize melhor de licenças que adquiriu e tooidentify sabe quando poderá ter licenças adicionais. 

relatório de Olá mostra a utilização de Active Directory de Olá paga funcionalidades no Olá últimos 30 dias. 

## <a name="report-structure"></a>Estrutura de relatório
| Nome da coluna | Descrição |
|:--- |:--- |
| Sem licença de utilizador |Nome de utilizador de Olá |
| Funcionalidade |nome da funcionalidade Olá. Por exemplo: acesso condicional |
| Aplicação acedida |nome da aplicação Olá que estiver a ser acedido com funcionalidade Olá Olá. Por exemplo: Office 365 SharePoint Online |

> [!NOTE]
> Se uma conta de utilizador foi eliminada Olá 'Sem licença User' coluna será preenchida com o ID, como 1003000090D8B285
> 
> 

## <a name="conditional-access-feature"></a>Funcionalidade de acesso condicional
Utilizadores sem licença vai ser sinalizados quando acedem a um serviço com a política de acesso condicional aplicada se não tiver uma licença do Azure AD Premium. 

Isto aplica-se tooMFA / políticas de localização, bem como dispositivos políticas que utilizar o Intune.

## <a name="see-also"></a>Consultar também
* [Utilizar o acesso condicional com o Office 365 e outros Azure Active Directory ligado aplicações](active-directory-conditional-access.md)
* [Introdução ao acesso condicional tooAzure AD](active-directory-conditional-access-azuread-connected-apps.md) 

