---
title: aaaSubscription e de conta para VMs com Linux no Azure | Microsoft Docs
description: "Saiba mais sobre Olá chaves design e implementação diretrizes para as subscrições e contas no Azure."
documentationcenter: 
services: virtual-machines-linux
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 19343826-7eef-42a1-98be-4ec65b0f377a
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 9025a40783c008310ebd0f674deb4a9001ae974a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-subscription-and-accounts-guidelines-for-linux-vms"></a>Diretrizes de contas e subscrição do Azure para VMs com Linux

[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-intro](../../../includes/virtual-machines-linux-infrastructure-guidelines-intro.md)]

Este artigo foca-se em compreender o crescimentos de gestão de subscrição e a conta de tooapproach como o seu ambiente e a base de utilizadores.

## <a name="implementation-guidelines-for-subscriptions-and-accounts"></a>Diretrizes de implementação para as subscrições e contas
Decisões:

* O conjunto de subscrições e contas precisa toohost a carga de trabalho IT ou infraestrutura?
* Como toobreak baixo Olá hierarquia toofit sua organização?

Tarefas:

* Definir a sua hierarquia de organização lógica como gostaria de toomanage-lo a partir de um nível de subscrição.
* toomatch esta hierarquia lógica, definir as contas de Olá necessários e as subscrições em cada conta.
* Crie conjunto de Olá de subscrições e contas de utilizar a Convenção de nomenclatura.

## <a name="subscriptions-and-accounts"></a>Subscrições e contas
toowork com o Azure, terá de uma ou mais subscrições do Azure. Recursos como máquinas virtuais (VMs) ou rede virtual existir nessas subscrições.

* Os clientes empresariais têm normalmente uma inscrição Enterprise, o que é Olá mais alto recurso na hierarquia de Olá, não sendo tooone associado ou mais contas.
* Para consumidores e os clientes sem uma inscrição Enterprise, o recurso de mais alto de Olá é conta Olá.
* As subscrições são tooaccounts associados e pode existir uma ou mais subscrições por conta. Registos do Azure informações ao nível da subscrição de Olá de faturação.

Devido a toohello limite dos níveis de hierarquia de duas na relação de subscrição de conta/Olá, é importante tooalign Olá Convenção de nomenclatura subscrições e contas toohello necessidades de faturação. Por exemplo, se uma empresa global utiliza o Azure, pode optar por utilizar toohave uma conta por região e tem subscrições geridos de Olá nível Região:

![](media/virtual-machines-common-infrastructure-service-guidelines/sub01.png)

Por exemplo, poderá utilizar Olá seguir a estrutura:

![](media/virtual-machines-common-infrastructure-service-guidelines/sub02.png)

Se uma região decidir toohave mais do que grupo específico de tooa associada uma subscrição, convenção de nomenclatura de Olá deve incorporar um tooencode de forma Olá dados adicionais sobre a conta de Olá ou o nome da subscrição Olá. Esta organização permite massaging faturação dados toogenerate Olá novos níveis da hierarquia durante a faturação relatórios:

![](media/virtual-machines-common-infrastructure-service-guidelines/sub03.png)

organização Olá foi aspeto Olá seguinte exemplo:

![](media/virtual-machines-common-infrastructure-service-guidelines/sub04.png)

Fornecemos faturação detalhada através de um ficheiro transferível para uma única conta ou para todas as contas de um contrato enterprise.

## <a name="next-steps"></a>Passos seguintes
[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-next-steps](../../../includes/virtual-machines-linux-infrastructure-guidelines-next-steps.md)]

