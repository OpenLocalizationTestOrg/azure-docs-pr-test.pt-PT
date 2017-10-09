---
title: "aaaTroubleshooting a filiação dinâmica para grupos | Microsoft Docs"
description: "Sugestões de resolução de problemas para a filiação dinâmica para grupos no Azure AD."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 89bb04b6-a379-49c2-8465-fe386641816a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/08/2017
ms.author: curtand
ms.openlocfilehash: d792fc406288844e2c5dbe3702c2c9870d09473e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-dynamic-memberships-for-groups"></a>Resolver problemas de associações dinâmicas a grupos
**Posso configurar uma regra num grupo, mas não associações for atualizadas no grupo de Olá**<br/>Certifique-se de que Olá **ativar gestão de grupo delegada** definição está definida demasiado**Sim** no Olá **configurar** separador. Irá ver esta definição apenas se tem sessão iniciada como um toowhom utilizador uma licença do Azure Active Directory Premium está atribuído. Verifique os valores de Olá para atributos de utilizador na regra Olá: existem utilizadores que satisfazem Olá regra?

**Posso configurado uma regra, mas agora membros existentes de Olá da regra de Olá são removidos**<br/>Este comportamento está previsto. Membros existentes do grupo de Olá são removidos quando uma regra está ativada ou alterada. são adicionados utilizadores de Olá devolvidos de avaliação da regra de Olá como grupo de toohello de membros.     

**Não consigo ver associação mudar instantly quando adicionar ou alterar uma regra, por que motivo não?**<br/>Avaliação da associação dedicada é feita periodicamente num processo em segundo plano assíncronas. Quanto Olá processo demora é determinado pelo número de Olá de utilizadores no seu diretório e Olá o tamanho do grupo de Olá criado no seguimento da regra de Olá. Normalmente, diretórios com pequeno número de utilizadores verão as alterações de associação de grupo Olá em menos de alguns minutos. Diretórios com um grande número de utilizadores podem demorar 30 minutos ou mais toopopulate.

### <a name="next-steps"></a>Passos seguintes
Estes artigos fornecem informações adicionais acerca do Azure Active Directory.

* [Gerir o acesso tooresources com grupos do Azure Active Directory](active-directory-manage-groups.md)
* [Índice de Artigos da Gestão da Aplicação no Azure Active Directory](active-directory-apps-index.md)
* [O que é o Azure Active Directory?](active-directory-whatis.md)
* [Integrar as identidades no local ao Azure Active Directory](active-directory-aadconnect.md)
