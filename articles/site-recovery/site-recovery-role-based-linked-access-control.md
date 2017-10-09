---
title: "aaaUsing toomanage de controlo de acesso baseado em funções do Azure Site Recovery | Microsoft Docs"
description: "Este artigo descreve como tooapply e da utilização baseada em funções do controlo de acesso (RBAC) toomanage as implementações do Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: mayanknayar
manager: rochakm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.workload: backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: manayar
ms.openlocfilehash: 7b721090351e561b28317ccdcf0ff283e0b146ca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="use-role-based-access-control-toomanage-azure-site-recovery-deployments"></a>Utilizar implementações do controlo de acesso baseado em funções toomanage do Azure Site Recovery

O Controlo de Acesso Baseado em Funções (RBAC) do Azure permite uma gestão pormenorizada de acesso ao Azure. Utilizar o RBAC, pode segregar responsabilidades na sua equipa e conceder toousers para permissões de acesso específicas apenas como trabalhos específicos tooperform necessários.

O Azure Site Recovery fornece 3 funções incorporadas toocontrol operações de gestão de recuperação de sites. Saber mais sobre [funções incorporadas do RBAC do Azure](../active-directory/role-based-access-built-in-roles.md)

* [Contribuinte de recuperação de sites](../active-directory/role-based-access-built-in-roles.md#site-recovery-contributor) -esta função tem todas as permissões necessárias toomanage do Azure Site Recovery operações num cofre dos serviços de recuperação. Um utilizador com esta função, no entanto, não é possível criar ou eliminar um cofre dos serviços de recuperação ou atribuir utilizadores tooother de direitos de acesso. Esta função é mais adequada para os administradores de recuperação de desastres que podem ativar e gerir a recuperação após desastre para aplicações ou organizações completos, como caso Olá pode ser.
* [Operador de recuperação de sites](../active-directory/role-based-access-built-in-roles.md#site-recovery-operator) -esta função tem permissões tooexecute e o Gestor de ativação pós-falha e a reativação pós-falha operações. Um utilizador com esta função não é possível ativar ou desativar a replicação, crie ou eliminar cofres, registar a nova infraestrutura ou atribuir utilizadores tooother de direitos de acesso. Esta função é mais adequada para um operador de recuperação de desastre quem pode máquinas virtuais de ativação pós-falha ou as aplicações quando indicado pelos proprietários da aplicação e os administradores de TI uma situação real ou simulado desastre como uma DR desagregar. Post resolução de desastre Olá, operador Olá DR pode voltar a proteger e a reativação pós-falha Olá máquinas virtuais.
* [Leitor de recuperação de sites](../active-directory/role-based-access-built-in-roles.md#site-recovery-reader) -esta função tem permissões tooview todas as operações de gestão do Site Recovery. Esta função é mais adequada para um executivo de monitorização de IT que pode monitorizar o estado atual do Olá da proteção e emitir pedidos de suporte, se necessário.

Se estiver à procura toodefine as suas próprias funções para o controlo ainda mais, consulte como demasiado[criar funções personalizadas](../active-directory/role-based-access-control-custom-roles.md) no Azure.

## <a name="permissions-required-tooenable-replication-for-new-virtual-machines"></a>Permissões necessárias tooEnable replicação para novas máquinas virtuais
Quando uma nova máquina Virtual replicada tooAzure utilizando o Azure Site Recovery, níveis de acesso do utilizador Olá associado são validado tooensure que Olá utilizador Olá requer permissões toouse Olá recursos do Azure fornecidos tooSite recuperação.

tooenable replicação para uma nova máquina virtual, um utilizador tem de ter:
* Permissão toocreate uma máquina virtual no grupo de recursos selecionado Olá
* Permissão toocreate uma máquina virtual na rede virtual selecionada de Olá
* Permissão toowrite toohello selecionado a conta de armazenamento

O utilizador precisa de Olá seguir replicação toocomplete de permissões de uma nova máquina virtual.

> [!IMPORTANT]
>Certifique-se de que as permissões relevantes estão adicionadas por modelo de implementação de Olá (Gestor de recursos / clássico) utilizado para a implementação de recursos.

| **Tipo de Recurso** | **Modelo de implementação** | **Permissão** |
| --- | --- | --- |
| Computação | Resource Manager | Microsoft.Compute/availabilitySets/read |
|  |  | Microsoft.Compute/virtualMachines/read |
|  |  | Microsoft.Compute/virtualMachines/write |
|  |  | Microsoft.Compute/virtualMachines/delete |
|  | Clássica | Microsoft.ClassicCompute/domainNames/read |
|  |  | Microsoft.ClassicCompute/domainNames/write |
|  |  | Microsoft.ClassicCompute/domainNames/delete |
|  |  | Microsoft.ClassicCompute/virtualMachines/read |
|  |  | Microsoft.ClassicCompute/virtualMachines/write |
|  |  | Microsoft.ClassicCompute/virtualMachines/delete |
| Rede | Resource Manager | Microsoft.Network/networkInterfaces/read |
|  |  | Microsoft.Network/networkInterfaces/write |
|  |  | Microsoft.Network/networkInterfaces/delete |
|  |  | Microsoft.Network/networkInterfaces/join/action |
|  |  | Microsoft.Network/virtualNetworks/read |
|  |  | Microsoft.Network/virtualNetworks/subnets/read |
|  |  | Microsoft.Network/virtualNetworks/subnets/join/action |
|  | Clássica | Microsoft.ClassicNetwork/virtualNetworks/read |
|  |  | Microsoft.ClassicNetwork/virtualNetworks/join/action |
| Armazenamento | Resource Manager | Microsoft.Storage/storageAccounts/read |
|  |  | Microsoft.Storage/storageAccounts/listkeys/action |
|  | Clássica | Microsoft.ClassicStorage/storageAccounts/read |
|  |  | Microsoft.ClassicStorage/storageAccounts/listKeys/action |
| Grupo de Recursos | Resource Manager | Microsoft.Resources/deployments/* |
|  |  | Microsoft.Resources/subscriptions/resourceGroups/read |

Considere a utilização de Olá 'Contribuinte de Máquina Virtual' e 'Clássico contribuinte de Máquina Virtual' [funções incorporadas](../active-directory/role-based-access-built-in-roles.md) para a implementação do Resource Manager e clássico modelos, respetivamente.

## <a name="next-steps"></a>Passos seguintes
* [Controlo de acesso baseado em funções](../active-directory/role-based-access-control-configure.md): introdução ao utilizar o RBAC em Olá portal do Azure.
* Saiba como toomanage aceder com:
  * [PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md)
  * [CLI do Azure](../active-directory/role-based-access-control-manage-access-azure-cli.md)
  * [API REST](../active-directory/role-based-access-control-manage-access-rest.md)
* [Resolução de problemas de controlo de acesso baseado em funções](../active-directory/role-based-access-control-troubleshooting.md): Obtenha sugestões sobre como corrigir problemas comuns.
