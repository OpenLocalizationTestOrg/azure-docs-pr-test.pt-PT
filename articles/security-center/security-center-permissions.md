---
title: "aaaPermissions no Centro de segurança do Azure | Microsoft Docs"
description: "Este artigo explica como o Centro de segurança do Azure utiliza o controlo de acesso baseado em funções tooassign toousers de permissões e identifica Olá permitida ações para cada função."
services: security-center
cloud: na
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
ms.assetid: 
ms.service: security-center
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: terrylan
ms.openlocfilehash: 03e16132dc3d951ef8ad9e86b9970b9e4d15c76b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="permissions-in-azure-security-center"></a>Permissões no Centro de segurança do Azure

Centro de segurança do Azure utiliza [controlo de acesso baseado em funções (RBAC)](../active-directory/role-based-access-control-configure.md), que fornece [funções incorporadas](../active-directory/role-based-access-built-in-roles.md) que podem ser atribuídas toousers, grupos e serviços no Azure.

Centro de segurança avalia configuração Olá dos problemas de segurança de tooidentify de recursos e vulnerabilidades. No Centro de segurança, verá apenas as informações relacionadas com recursos tooa quando são atribuídos função Olá de proprietário, Contribuidor ou leitor para Olá subscrição ou grupo de recursos que um recurso pertence.

Funções de toothese de adição, existem duas funções específicas do Centro de segurança:

* **Leitor de segurança**: um utilizador que pertence toothis função tem de ver direitos tooSecurity Center. utilizador Olá pode ver as recomendações, alertas, uma política de segurança e Estados de segurança, mas não é possível efetuar alterações.
* **Administrador de segurança**: um utilizador que pertence a função de toothis tem Olá mesmo direitos como Olá leitor de segurança e pode também atualizar a política de segurança de Olá e dispensar alertas e recomendações.

> [!NOTE]
> funções de segurança de Olá, leitor de segurança e administrador de segurança, tem acesso apenas no Centro de segurança. funções de segurança de Olá não têm acesso tooother serviço áreas do Azure como armazenamento, Web & Mobile ou Internet das coisas.
>
>

## <a name="roles-and-allowed-actions"></a>Funções e as ações permitidas

Olá tabela seguinte apresenta as funções e permitido ações no Centro de segurança. Um X indica que a ação de Olá é permitida para essa função.

| Função | Editar política de segurança | Aplicar as recomendações de segurança para um recurso | Dispensar alertas e recomendações | Ver alertas e recomendações |
|:--- |:---:|:---:|:---:|:---:|
| Proprietário da subscrição | X | X | X | X |
| Contribuinte de subscrição | X | X | X | X |
| Proprietário do grupo de recursos | -- | X | -- | X |
| Grupo de recursos contribuinte | -- | X | -- | X |
| Leitor | -- | -- | -- | X |
| Administrador de segurança | X | -- | X | X |
| Leitor de segurança | -- | -- | -- | X |

> [!NOTE]
> Recomendamos que atribua Olá função menos permissiva necessária para os utilizadores toocomplete as respetivas tarefas. Por exemplo, atribua toousers de função de leitor Olá que basta tooview informações sobre o estado de funcionamento do Olá segurança de um recurso, mas não tomar medidas, tal como aplicar recomendações ou editar políticas.
>
>

## <a name="next-steps"></a>Passos seguintes
Este artigo explicado como o Centro de segurança utiliza o RBAC tooassign permissões toousers e identificado Olá permitida ações para cada função. Agora que está familiarizado com atribuições de funções de Olá necessário toomonitor Olá estado de segurança da sua subscrição, edite as políticas de segurança e aplicar recomendações, saiba como:

- [Definir políticas de segurança no Centro de segurança](security-center-policies.md)
- [Gerir recomendações de segurança no Centro de segurança](security-center-recommendations.md)
- [Monitorizar estado de funcionamento de segurança de Olá dos seus recursos do Azure](security-center-monitoring.md)
- [Gerir e responder a alertas de toosecurity no Centro de segurança](security-center-managing-and-responding-alerts.md)
- [Monitorizar soluções de segurança de parceiros](security-center-partner-solutions.md)
