---
title: "aaaManage acesso e permissões com RBAC - RBAC do Azure | Microsoft Docs"
description: "Introdução à gestão de acessos com controlo de acesso baseado em funções do Azure no Olá Portal do Azure. Utilize permissões de tooassign atribuições de função no seu diretório."
services: active-directory
documentationcenter: 
author: andredm7
manager: femila
ms.assetid: 8f8aadeb-45c9-4d0e-af87-f1f79373e039
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/13/2017
ms.author: andredm
ms.reviewer: rqureshi
ms.openlocfilehash: 1c133b2b57b49d85f0e12a318c7997478e095fb9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-role-based-access-control-in-hello-azure-portal"></a>Introdução ao controlo de acesso baseado em funções na Olá portal do Azure
Segurança e orientado para empresas devem focar-se em fornecer aos funcionários Olá exato as permissões que precisam. Demasiados permissões podem expor um tooattackers de conta. Permissões insuficientes significa que os funcionários não é possível obter o trabalho feito de forma eficiente. Azure baseada em funções controlo de acesso (RBAC) ajuda a resolver este problema, oferecendo gestão de acesso detalhada para o Azure.

Utilizar o RBAC, pode segregar funções na sua equipa e conceder apenas de Olá quantidade de toousers de acesso que têm de tooperform as respetivas tarefas. Em vez de dar everybody sem restrições permissões na sua subscrição do Azure ou recursos, pode permitir que apenas determinadas ações. Por exemplo, utilize RBAC toolet um empregado gerir máquinas virtuais numa subscrição, enquanto outro pode gerir SQL bases de dados dentro de Olá mesma subscrição.

## <a name="basics-of-access-management-in-azure"></a>Noções básicas de gestão de acesso no Azure
Cada subscrição do Azure está associada um diretório do Azure Active Directory (AD). Os utilizadores, grupos e aplicações a partir desse diretório podem gerir recursos no Olá subscrição do Azure. Atribua estes direitos de acesso utilizando Olá portal do Azure, as ferramentas da linha de comandos do Azure e APIs de gestão do Azure.

Conceder acesso ao atribuir Olá toousers de funções RBAC adequada, grupos e aplicações num determinado âmbito. Olá âmbito de uma atribuição de função pode ser uma subscrição, um grupo de recursos ou um único recurso. Uma função atribuída a um âmbito principal também concede acesso subordinados toohello contidos. Por exemplo, um utilizador com o grupo de recursos do acesso tooa pode gerir todos os recursos de Olá contém, como Web sites, sub-redes e máquinas virtuais.

![Relação entre elementos do Azure Active Directory - diagrama](./media/role-based-access-control-what-is/rbac_aad.png)

função RBAC Olá que atribuir dita que utilizador Olá de recursos, grupo ou aplicação pode gerir esse âmbito.

## <a name="built-in-roles"></a>Funções incorporadas
RBAC do Azure tem três funções básicas que se aplicam tooall tipos de recursos:

* **Proprietário** tem acesso total tooall recursos, incluindo Olá toodelegate direita acesso tooothers.
* **Contribuidor** pode criar e gerir todos os tipos de recursos do Azure, mas não é possível conceder acesso tooothers.
* **Leitor** pode ver os recursos do Azure existentes.

rest Olá das funções do RBAC Olá no Azure permite a gestão de recursos do Azure específicos. Por exemplo, Olá função de contribuinte de Máquina Virtual permite Olá toocreate de utilizador e gerir máquinas virtuais. Se não atribuir-lhes rede virtual do acesso toohello ou sub-rede Olá Olá máquina virtual estabelece ligação ao. 

[Funções incorporadas do RBAC](role-based-access-built-in-roles.md) listas Olá funções disponíveis no Azure. Especifica as operações de Olá e âmbito que cada função incorporada concede toousers. Se estiver à procura toodefine as suas próprias funções para o controlo ainda mais, consulte como toobuild [funções personalizadas no Azure RBAC](role-based-access-control-custom-roles.md).

## <a name="resource-hierarchy-and-access-inheritance"></a>Herança de recursos de acesso e de hierarquia
* Cada **subscrição** no Azure pertence tooonly um diretório. (Mas cada diretório pode ter mais do que uma subscrição).
* Cada **grupo de recursos** pertence tooonly uma subscrição.
* Cada **recursos** pertence tooonly um grupo de recursos.

Acesso que conceda em âmbitos principal é herdado, os âmbitos subordinados. Por exemplo:

* Atribua o grupo do Azure AD tooan de função de leitor de Olá no âmbito de subscrição de Olá. membros desse grupo Olá podem ver todos os recursos e o grupo de recursos na subscrição Olá.
* Atribuir aplicação tooan de função de contribuinte do Olá no âmbito do grupo de recursos de Olá. -Pode gerir os recursos de todos os tipos nesse grupo de recursos, mas não outros grupos de recursos na subscrição Olá.

## <a name="azure-rbac-vs-classic-subscription-administrators"></a>RBAC do Azure vs. os administradores da subscrição clássica
Os administradores da subscrição clássico e coadministradores têm acesso total toohello subscrição do Azure. Gerir recursos através de Olá [portal do Azure](https://portal.azure.com) com APIs do Azure Resource Manager ou Olá [portal clássico do Azure](https://manage.windowsazure.com) e o modelo de implementação clássico do Azure. No modelo RBAC Olá, os administradores clássicos são atribuídos a função de proprietário Olá no âmbito de subscrição de Olá.

Apenas Olá portal do Azure e Olá novo suporte de APIs do Gestor de recursos do Azure RBAC do Azure. Utilizadores e aplicações que são atribuídas a funções RBAC não é possível utilizar o portal de gestão clássico Olá e o modelo de implementação clássico do Azure de Olá.

## <a name="authorization-for-management-vs-data-operations"></a>Autorização para gestão versus operações de dados
RBAC do Azure só suporta operações de gestão de recursos do Azure de Olá Olá portal do Azure e APIs do Azure Resource Manager. Não é possível autorizar o todas as operações de nível de dados para recursos do Azure. Por exemplo, podem autorizar alguém toomanage contas de armazenamento, mas não os blobs toohello ou tabelas dentro de uma conta de armazenamento. Da mesma forma, uma base de dados do SQL Server pode ser gerida, mas não Olá tabelas dentro da mesma.

## <a name="next-steps"></a>Passos Seguintes
* Introdução ao [controlo de acesso baseado em funções no portal do Azure de Olá](role-based-access-control-configure.md).
* Consulte Olá [funções incorporadas do RBAC](role-based-access-built-in-roles.md)
* Definir as suas [Funções personalizadas no Azure RBAC](role-based-access-control-custom-roles.md)
