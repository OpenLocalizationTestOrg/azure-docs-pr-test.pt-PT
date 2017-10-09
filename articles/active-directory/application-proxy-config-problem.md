---
title: "criar uma aplicação de Proxy de aplicações de aaaProblem | Microsoft Docs"
description: "Como tootroubleshoot emite criar aplicações de Proxy da aplicação no portal de administração do Azure AD Olá"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 24fab83c38a49a9e5754854acf2f9711e374e559
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="problem-creating-an-application-proxy-application"></a>Problema ao criar uma aplicação de Proxy de aplicações 

Seguem-se alguns dos problemas comuns de Olá enfrentam pessoas ao criar uma nova aplicação de proxy de aplicações.

## <a name="recommended-documents"></a>Documentos recomendados 

Consulte toolearn mais sobre a criação de uma aplicação de Proxy de aplicações através do Portal de administração de Olá [publicar aplicações através do Proxy de aplicações do Azure AD](https://docs.microsoft.com/azure/active-directory/application-proxy-publish-azure-portal).

Se estiver a seguir passos Olá esse documento e está a obter um erro ao criar a aplicação Olá, consulte os detalhes do erro de Olá para informações e sugestões sobre como toofix Olá a aplicação. A maioria das mensagens de erro incluem uma correção sugerida. 

## <a name="specific-things-toocheck"></a>Toocheck coisas específico

erros comuns tooavoid, certifique-se:

-   É um administrador com permissão toocreate uma aplicação de Proxy de aplicações

-   URL interno Olá é exclusivo

-   URL externo Olá é exclusivo

-   Olá URLs início com http ou https e terminar com um "/"

-   URL de Olá deve ser um nome de domínio e não um endereço IP

mensagem de erro de saudação deve apresentar no canto superior direito Olá quando criar aplicação Olá. Também pode selecionar Olá notificação ícone toosee Olá as mensagens de erro.

   ![Pedido de notificação](./media/application-proxy-config-problem/error-message.png)

## <a name="next-steps"></a>Passos seguintes
[Ativar o Proxy de aplicações no Olá portal do Azure](active-directory-application-proxy-enable.md)
