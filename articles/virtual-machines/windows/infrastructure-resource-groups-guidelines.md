---
title: grupos de aaaResource para VMs do Windows no Azure | Microsoft Docs
description: "Saiba mais sobre Olá chaves design e implementação diretrizes para implementar grupos de recursos nos serviços de infraestrutura do Azure."
documentationcenter: 
services: virtual-machines-windows
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 0fbcabcd-e96d-4d71-a526-431984887451
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 56b5670ec98bf3e80b7a622d5d760a57a7d20809
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-resource-group-guidelines-for-windows-vms"></a>Diretrizes de grupo de recursos do Azure para VMs do Windows

[!INCLUDE [virtual-machines-windows-infrastructure-guidelines-intro](../../../includes/virtual-machines-windows-infrastructure-guidelines-intro.md)]

Este artigo foca-se em compreender como toologically construir o seu ambiente e todos os componentes de Olá em grupos de recursos de grupo.

## <a name="implementation-guidelines-for-resource-groups"></a>Diretrizes de implementação para grupos de recursos
Decisões:

* São vai toobuild os grupos de recursos por componentes de infraestrutura de núcleo de Olá ou implementação de aplicação completa?
* Necessita de toorestrict acesso tooResource grupos utilizar controlos de acesso baseado em funções?

Tarefas:

* Defina o que principais componentes de infraestrutura e dedicado precisar de grupos de recursos.
* Reveja como tooimplement modelos do Resource Manager para implementações consistentes e reproduzíveis.
* Defina as funções de acesso de utilizador é necessário para controlar o acesso a grupos de tooResource.
* Crie conjunto de Olá de utilizar a Convenção de nomenclatura de grupos de recursos. Pode utilizar o Azure PowerShell ou o portal de Olá.

## <a name="resource-groups"></a>Grupos de Recursos
No Azure, é logicamente grupo de recursos relacionados, tais como contas de armazenamento, redes virtuais e máquinas virtuais (VMs) toodeploy, gere e mantê-los como uma única entidade. Esta abordagem torna mais fácil toodeploy aplicações enquanto mantém Olá todos os recursos relacionados em conjunto de uma perspetiva de gestão ou toogrant outros grupo toothat acesso a recursos. Os nomes de grupo de recursos podem ter um máximo de 90 carateres de comprimento. Para obter uma compreensão mais abrangente dos grupos de recursos, leia o artigo Olá [descrição geral do Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).

Uma funcionalidade chave tooResource grupos é capacidade toobuild fora do seu ambiente através de modelos. Um modelo é simplesmente um ficheiro JSON que declara o armazenamento de Olá, funcionamento em rede e recursos de computação. Também pode definir qualquer relacionados scripts personalizados ou tooapply configurações. Ao utilizar estes modelos, crie consistentes e reproduzíveis implementações para as suas aplicações. Esta abordagem torna mais fácil toobuild fora de um ambiente de desenvolvimento e, em seguida, utilizar essa mesma toocreate de modelo uma implementação de produção, ou vice versa. Para uma melhor compreensão através de modelos, leia o artigo [Olá instruções do modelo](../../azure-resource-manager/resource-manager-template-walkthrough.md) que orienta-cada passo da conceção de Olá um modelo.

Existem duas abordagens diferentes que pode tomar quando conceber o seu ambiente com grupos de recursos:

* Grupos de recursos para cada implementação de aplicação que combina as contas do storage Olá, redes virtuais e sub-redes, VMs, carregar balanceadores, etc.
* Grupos de recursos centralizada que contêm as contas redes e armazenamento ou sub-redes virtuais principais. As aplicações, em seguida, são os seus próprios grupos de recursos que contêm apenas as VMs, balanceadores de carga, interfaces de rede, etc.

Como aumentar horizontalmente, criar grupos de recursos centralizada para as redes virtuais e sub-redes torna mais fácil toobuild em vários locais ligações para as opções de conectividade híbrida de rede. abordagem alternativa Olá é para cada aplicação toohave sua própria rede virtual que necessita de configuração e manutenção.  [Controlos de acesso baseado em funções](../../active-directory/role-based-access-control-what-is.md) fornecer um acesso de toocontrol de forma granulares tooResource grupos. Para aplicações de produção, pode controlar utilizadores Olá que podem aceder a esses recursos ou recursos de infraestrutura de núcleo de Olá pode limitar toowork para engenheiros de infraestrutura apenas com os mesmos. Os proprietários da aplicação só tem acesso toohello componentes da aplicação dentro do respetivo grupo de recursos e não núcleo de Olá infraestrutura do Azure do seu ambiente. Como estruturar o seu ambiente, considere os utilizadores de Olá que necessitam de aceder a recursos toohello e os grupos de recursos de design em conformidade. 

## <a name="next-steps"></a>Passos seguintes
[!INCLUDE [virtual-machines-windows-infrastructure-guidelines-next-steps](../../../includes/virtual-machines-windows-infrastructure-guidelines-next-steps.md)]

