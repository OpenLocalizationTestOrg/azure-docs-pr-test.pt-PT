---
title: Compreender o acesso a recursos no Azure | Microsoft Docs
description: "Este tópico explica os conceitos sobre como utilizar os administradores da subscrição para controlar o acesso a recursos no portal do Azure completo"
services: active-directory
documentationcenter: 
author: curtand
manager: mtillman
ms.assetid: 174f1706-b959-4230-9a75-bf651227ebf6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/06/2017
ms.author: curtand
ms.custom: it-pro;
ms.openlocfilehash: ad6658aaed55801ac8f6a39a721fb7469892303d
ms.sourcegitcommit: e266df9f97d04acfc4a843770fadfd8edf4fa2b7
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/11/2017
---
# <a name="understanding-resource-access-in-azure"></a>Compreender o acesso a recursos no Azure

Controlo de acesso no Azure inicia-se de uma perspetiva de faturação. O proprietário de uma conta do Azure, acedido, visitando o [Centro de contas do Azure](https://account.windowsazure.com/subscriptions), é o administrador de conta (AA). As subscrições são um contentor para faturação, mas também agir como um limite de segurança: cada subscrição tem um serviço de administrador (SA) que pode adicionar, remover e modificar recursos do Azure nessa subscrição utilizando o [portal do Azure](https://portal.azure.com/). A predefinição SA de uma nova subscrição é AA, mas o AA pode alterar a SA no Centro de contas do Azure.

<br><br>![Contas do Azure][1]

As subscrições também terem uma associação a um diretório. O diretório define um conjunto de utilizadores. Estes podem ser os utilizadores do trabalho ou escola que criou o diretório ou podem ser os utilizadores convidados externos. Subscrições podem ser acedidas por um subconjunto dos utilizadores de diretório que atribuiu como administrador de serviço (SA) ou Coadministrador (AC); a única exceção é que, por motivos de legado, contas Microsoft (anteriormente Windows Live ID) podem ser atribuídas como SA ou AC sem estar presente no diretório.

<br><br>![Controlo de acesso no Azure][2]

Funcionalidade dentro do portal do Azure permite SAs que tem sessão iniciadas com uma Account Microsoft para alterar o diretório a que está associada uma subscrição. Esta operação tem implicações sobre o controlo de acesso dessa subscrição.

<br><br>![Fluxo de início de sessão de utilizador simples][3]

No caso simple, uma organização (por exemplo, Contoso) irá impor a faturação e controlo de acesso através do mesmo conjunto de subscrições. Ou seja, o diretório é associado às subscrições que pertencem a uma única conta do Azure. Após o início de sessão com êxito para o portal do Azure, os utilizadores veem duas coleções de recursos (representados no laranja na ilustração anterior):

* Diretórios onde a conta de utilizador existe (obtido ou adicionado como um principal de externo). Tenha em atenção que o diretório utilizado para início de sessão não se encontra relevante para este cálculo, pelo que os diretórios serão apresentados sempre, independentemente de onde que iniciou sessão.
* Recursos que fazem parte das subscrições que estão associados com o diretório utilizado para início de sessão e que o utilizador pode aceder (onde são uma AC ou SA).

<br><br>![Utilizador com várias subscrições e diretórios][4]

Os utilizadores com subscrições em vários diretórios têm a capacidade de mudar o contexto actual do portal do Azure utilizando o filtro de subscrição. Nos bastidores, isto resulta em separado um início de sessão para um diretório diferente, mas isto é conseguido de forma totalmente integrada utilizando início de sessão único (SSO).

As operações, tal como mover recursos entre subscrições podem ser mais difícil devido a esta vista de diretório única de subscrições. Para efetuar a transferência de recursos, poderá ser necessário utilizar primeiro a **Editar diretório** comando na página de subscrições de **definições** para associar as subscrições para o mesmo diretório.

## <a name="next-steps"></a>Passos Seguintes
* Para saber mais sobre como alterar os administradores para uma subscrição do Azure, consulte [Como adicionar ou alterar funções de administrador do Azure](../billing/billing-add-change-azure-subscription-administrator.md)
* Para obter mais informações sobre como o Azure Active Directory relacionada com a sua subscrição do Azure, consulte [subscrições do Azure como estão associadas ao Azure Active Directory](active-directory-how-subscriptions-associated-directory.md)
* Para obter mais informações sobre como atribuir funções no Azure AD, consulte [Atribuir funções de administrador no Azure Active Directory](active-directory-assign-admin-roles-azure-portal.md)

<!--Image references-->
[1]: ./media/active-directory-understanding-resource-access/IC707931.png
[2]: ./media/active-directory-understanding-resource-access/IC707932.png
[3]: ./media/active-directory-understanding-resource-access/IC707933.png
[4]: ./media/active-directory-understanding-resource-access/IC707934.png
