---
title: "Olá, aaaCreate utilizando um conjunto de dimensionamento da Máquina Virtual do Azure portal | Microsoft Docs"
description: Implemente os conjuntos de dimensionamento com o portal do Azure.
keywords: "Conjuntos de dimensionamento de máquina virtual"
services: virtual-machine-scale-sets
documentationcenter: 
author: gatneil
manager: madhana
editor: tysonn
tags: azure-resource-manager
ms.assetid: 9c1583f0-bcc7-4b51-9d64-84da76de1fda
ms.service: virtual-machine-scale-sets
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm
ms.devlang: na
ms.topic: article
ms.date: 05/01/2017
ms.author: negat
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 23c88f4b1ba99994a38f8886f60735da74e5c17e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-virtual-machine-scale-set-with-hello-azure-portal"></a>Como toocreate um conjunto de dimensionamento da Máquina Virtual com Olá portal do Azure
Este tutorial mostra como é fácil toocreate um conjunto de dimensionamento de Máquina Virtual em apenas alguns minutos, utilizando Olá portal do Azure. Se não tiver uma subscrição do Azure, crie uma [conta gratuita](https://azure.microsoft.com/free/) antes de começar.

## <a name="choose-hello-vm-image-from-hello-marketplace"></a>Selecione a imagem VM de Olá do marketplace Olá
No portal de Olá, pode facilmente implementar uma escala com CentOS, CoreOS, Debian, abra Suse, Red Hat Enterprise Linux, SUSE Linux Enterprise Server, Ubuntu Server ou imagens do Windows Server.

Em primeiro lugar, navegue até toohello [portal do Azure](https://portal.azure.com) num web browser. Clique em `New`, procure `scale set`e, em seguida, selecione Olá `Virtual machine scale set` entrada:

![ScaleSetPortalOverview](./media/virtual-machine-scale-sets-portal-create/ScaleSetPortalOverview.PNG)

## <a name="create-hello-scale-set"></a>Criar conjunto de dimensionamento de Olá
Agora pode utilizar predefinições Olá e criar conjunto de dimensionamento de Olá rapidamente.

* No Olá `Basics` painel, introduza um nome de conjunto de dimensionamento de Olá. Este nome fica Olá base do FQDN do Balanceador de carga Olá à frente do conjunto de dimensionamento de Olá Olá, por isso, certifique-se de nome de Olá é exclusivo em todas as do Azure.
* Selecione o SO pretendido escreva, introduza o seu nome de utilizador pretendido e, selecione o tipo de autenticação de que prefere. Se escolher uma palavra-passe, tem de ser, pelo menos, 12 carateres longos e cumprir os três fora de requisitos de complexidade de seguintes quatro de Olá: uma minúscula, uma maiúscula, um número e um caráter especial. Saiba mais sobre os [requisitos de nomes de utilizador e palavras-passe](../virtual-machines/windows/faq.md#what-are-the-username-requirements-when-creating-a-vm). Se optar por `SSH public key`ser tooonly se colar a chave pública, não a chave privada:

![ScaleSetPortalBasics](./media/virtual-machine-scale-sets-portal-create/ScaleSetPortalBasics.PNG)

* Escolha se pretende como grupo de posicionamento único tooa de conjunto de dimensionamento de Olá toolimit ou se se deve abranger vários grupos de colocação. Permitir Olá do conjunto de dimensionamento toospan grupos colocação permite de conjuntos de dimensionamento mais de 100 VMs de capacidade (cópia de segurança too1, 000) com certas limitações. Para obter mais informações, consulte [esta documentação](./virtual-machine-scale-sets-placement-groups.md).
* Introduza o nome do grupo de recursos desejados e a localização e, em seguida, clique em `OK`.
* No Olá `Virtual machine scale set service settings` painel: introduza a etiqueta de nome de domínio pretendida (base Olá de Olá FQDN Olá Balanceador de carga à frente do conjunto de dimensionamento de Olá). Esta etiqueta deve ser exclusiva em todas as do Azure.
* Escolha a sua imagem de disco do sistema operativo pretendido, a contagem de instâncias e o tamanho da máquina.
* Escolher o tipo de disco desejado: geridos ou não geridos. Para obter mais informações, consulte [esta documentação](./virtual-machine-scale-sets-managed-disks.md). Se tiver escolhido o conjunto de dimensionamento de Olá toohave span vários grupos de posicionamento, esta opção não estará disponível porque o disco gerido é necessário para grupos de colocação de toospan de conjuntos de dimensionamento.
* Ativar ou desativar o dimensionamento automático e configurar se estiver ativada:

![ScaleSetPortalService](./media/virtual-machine-scale-sets-portal-create/ScaleSetPortalService.PNG)

* No Olá `Summary` painel, quando é efetuada a validação, clique em `OK` conjunto de dimensionamento de Olá toostart da implementação.


## <a name="connect-tooa-vm-in-hello-scale-set"></a>Ligar tooa VM num conjunto de dimensionamento de Olá
Se escolheu toolimit a escala defina tooa grupo de posicionamento único, em seguida, o conjunto de dimensionamento de Olá é implementado com NAT regras configuradas toolet ligar facilmente a conjunto de dimensionamento de toohello (se não, tooconnect toohello máquinas virtuais na escala de Olá, provavelmente tem toocreate um jumpbox no Olá mesma rede virtual que o conjunto de dimensionamento de Olá). toosee-los, navegue até toohello `Inbound NAT Rules` separador Olá de Balanceador de carga de conjunto de dimensionamento de Olá:

![ScaleSetPortalNatRules](./media/virtual-machine-scale-sets-portal-create/ScaleSetPortalNatRules.PNG)

Pode ligar tooeach VM na escala de Olá definido utilizando estas regras NAT. Por exemplo, para um conjunto de dimensionamento do Windows, se existir uma regra NAT de entrada porta 50000, foi possível ligar toothat máquina através de RDP no `<load-balancer-ip-address>:50000`. Para um conjunto de dimensionamento do Linux, ligaria utilizando o comando de Olá `ssh -p 50000 <username>@<load-balancer-ip-address>`.

## <a name="next-steps"></a>Passos seguintes
Para obter documentação sobre como de conjuntos de dimensionamento de toodeploy de Olá CLI, consulte [esta documentação](virtual-machine-scale-sets-cli-quick-create.md).

Para obter documentação sobre como de conjuntos de dimensionamento de toodeploy a partir do PowerShell, consulte [esta documentação](virtual-machine-scale-sets-windows-create.md).

Para obter documentação sobre como toodeploy escala define a partir do Visual Studio, consulte [esta documentação](virtual-machine-scale-sets-vs-create.md).

Para obter documentação geral, veja Olá [página de descrição geral de documentação para conjuntos de dimensionamento](virtual-machine-scale-sets-overview.md).

Para obter informações gerais, veja Olá [página de destino principal para conjuntos de dimensionamento](https://azure.microsoft.com/services/virtual-machine-scale-sets/).

