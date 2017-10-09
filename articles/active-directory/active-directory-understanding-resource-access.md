---
title: acesso a recursos no Azure aaaUnderstanding | Microsoft Docs
description: "Este tópico explica os conceitos sobre como utilizar o acesso a recursos subscrição administradores toocontrol no Olá portal Azure completo"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
ms.assetid: 174f1706-b959-4230-9a75-bf651227ebf6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/24/2017
ms.author: curtand
ms.custom: oldportal;it-pro;
ms.openlocfilehash: 06b9c4166bdea849faae67cae3146c6c278deb97
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="understanding-resource-access-in-azure"></a>Compreender o acesso a recursos no Azure
> [!IMPORTANT]
> A Microsoft recomenda que gere o Azure AD através de Olá [Centro de administração do Azure AD](https://aad.portal.azure.com) no Olá portal do Azure em vez de utilizar Olá portal clássico do Azure referenciado neste artigo. Olá portal do Azure fornece [controlo de acesso baseado em funções](role-based-access-control-configure.md) para recursos do Azure podem ser geridos de forma mais precisa.
> 
> 

Em Outubro de 2013, Olá portal clássico do Azure e APIs de gestão de serviço foram integradas no Azure Active Directory na base de Olá toolay ordem para melhorar a experiência de utilizador de Olá para gerir o acesso a recursos tooAzure. Azure Active Directory já fornece excelente capacidades como gestão de utilizadores, sincronização de diretórios no local, a autenticação multifator e controlo de acesso de aplicação. Naturalmente, estes devem também ser disponibilizados para gerir recursos do Azure across-the-board.

Controlo de acesso no Azure inicia-se de uma perspetiva de faturação. proprietário de Olá de uma conta do Azure, acedido, visitando Olá [Centro de contas do Azure](https://account.windowsazure.com/subscriptions), é Olá conta de administrador (AA). As subscrições são um contentor para faturação, mas também agir como um limite de segurança: cada subscrição tem um serviço de administrador (SA) que pode adicionar, remover e modificar recursos do Azure nessa subscrição utilizando Olá [doportalclássicodoAzure](https://manage.windowsazure.com/). Olá predefinido SA de uma nova subscrição é AA Olá, mas Olá AA pode alterar Olá SA no Olá Centro de contas do Azure.

<br><br>![Contas do Azure][1]

As subscrições também terem uma associação a um diretório. diretório de Olá define um conjunto de utilizadores. Estes podem ser os utilizadores da empresa ou escola que criou o diretório de Olá Olá ou podem ser utilizadores externos (ou seja, Accounts Microsoft). Subscrições podem ser acedidas por um subconjunto dos utilizadores de diretório que atribuiu como administrador de serviço (SA) ou Coadministrador (AC); Olá apenas exceção é que, por motivos de legado, Accounts da Microsoft (anteriormente Windows Live ID) podem ser atribuídos como SA ou AC sem estar presente no diretório de Olá.

<br><br>![Controlo de acesso no Azure][2]

Funcionalidade dentro do Olá portal clássico do Azure permite SAs que são assinados utilizando Account Microsoft toochange Olá diretório uma subscrição é associada através da utilização de Olá **Editar diretório** comando no Olá **Subscrições** página em **definições**. Tenha em atenção que esta operação tem implicações no controlo de acesso de Olá dessa subscrição.

> [!NOTE]
> Olá **Editar diretório** comando no Olá clássico do Azure portal não está disponível toousers que têm sessão iniciada na utilização de um trabalho ou escola conta porque podem iniciar sessão apenas toohello diretório toowhich pertencem a essas contas.
> 
> 

<br><br>![Fluxo de início de sessão do utilizador simples][3]

No caso de simples Olá, uma organização (por exemplo, Contoso) irá impor a faturação e controlo de acesso em Olá mesmo conjunto de subscrições. Ou seja, o diretório de Olá é toosubscriptions associado que são propriedade de uma única conta do Azure. Após o início de sessão com êxito toohello portal clássico do Azure, os utilizadores veem duas coleções de recursos (descritos na ilustração anterior Olá de cor de laranja):

* Diretórios onde a conta de utilizador existe (obtido ou adicionado como um principal de externo). Tenha em atenção o diretório Olá utilizado para início de sessão não está a computação toothis relevantes, para que os diretórios serão apresentados sempre, independentemente de onde que iniciou sessão.
* Recursos que fazem parte das subscrições que estão associados com o diretório de Olá utilizado para início de sessão e Olá que o utilizador podem aceder (onde são uma AC ou SA).

<br><br>![Utilizador com várias subscrições e diretórios][4]

Os utilizadores com subscrições em vários diretórios tem Olá capacidade tooswitch Olá contexto actual do Olá portal clássico do Azure utilizando o filtro de subscrição de Olá. Em bastidores Olá, isto resulta no início de sessão separada tooa outro diretório, mas isto é conseguido de forma totalmente integrada utilizando início de sessão único (SSO).

As operações, tal como mover recursos entre subscrições podem ser mais difícil devido a esta vista de diretório única de subscrições. transferência de recursos do tooperform Olá, poderá ser necessário toofirst utilizar Olá **Editar diretório** comando na página de subscrições Olá no **definições** tooassociate Olá subscrições toohello mesmo diretório .

## <a name="next-steps"></a>Passos Seguintes
* mais informações sobre como toolearn como administradores toochange para uma subscrição do Azure, consulte [como tooadd ou alterar funções de administrador do Azure](../billing/billing-add-change-azure-subscription-administrator.md)
* Para obter mais informações sobre como do Active Directory do Azure se relaciona com tooyour subscrição do Azure, consulte [subscrições do Azure como estão associadas ao Azure Active Directory](active-directory-how-subscriptions-associated-directory.md)
* Para obter mais informações sobre como tooassign funções no Azure AD, consulte [atribuir funções de administrador no Azure Active Directory](active-directory-assign-admin-roles.md)

<!--Image references-->
[1]: ./media/active-directory-understanding-resource-access/IC707931.png
[2]: ./media/active-directory-understanding-resource-access/IC707932.png
[3]: ./media/active-directory-understanding-resource-access/IC707933.png
[4]: ./media/active-directory-understanding-resource-access/IC707934.png
