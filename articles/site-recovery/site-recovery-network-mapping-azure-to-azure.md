---
title: "mapeamento de aaaNetwork entre duas regiões do Azure no Azure Site Recovery | Microsoft Docs"
description: "O Azure Site Recovery coordena a replicação de Olá, a ativação pós-falha e a recuperação de máquinas virtuais e servidores físicos. Saiba mais sobre tooAzure de ativação pós-falha ou num datacenter secundário."
services: site-recovery
documentationcenter: 
author: prateek9us
manager: gauravd
editor: 
ms.assetid: 44813a48-c680-4581-a92e-cecc57cc3b1e
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 08/11/2017
ms.author: pratshar
ms.openlocfilehash: 4f80c44e3f94eaf446bc01a7041d91fe34aa78d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="network-mapping-between-two-azure-regions"></a>Mapeamento de rede entre as duas regiões do Azure


Este artigo descreve como toomap Azure redes virtuais das duas regiões do Azure entre si. Mapeamento de rede assegura que quando a máquina virtual replicada é criada no destino Olá região do Azure, é criada em Olá de rede virtual é mapeado toovirtual rede Olá virtual da máquina de origem.  

## <a name="prerequisites"></a>Pré-requisitos
Antes de mapear redes Certifique-se, criou [redes virtuais do Azure](../virtual-network/virtual-networks-overview.md) na origem e destino regiões do Azure.

## <a name="map-networks"></a>Mapear redes

toomap uma Azure virtual network na rede virtual do tooanother de uma região do Azure noutra região, aceda tooSite infraestrutura de recuperação -> o mapeamento da rede (para máquinas virtuais do Azure) e crie um mapeamento da rede.

![Mapeamento da rede](./media/site-recovery-network-mapping-azure-to-azure/network-mapping1.png)


No Olá o exemplo abaixo minha máquina virtual está em execução na Ásia Oriental região e está a ser replicadas tooSoutheast Ásia.

Selecione a rede de origem e destino Olá e, em seguida, clique em OK toocreate um mapeamento de rede de Oriental tooSoutheast Ásia.

![Mapeamento da rede](./media/site-recovery-network-mapping-azure-to-azure/network-mapping2.png)


Olá a mesma coisa toocreate um mapeamento de rede do Sudeste asiático tooEast Ásia.  
![Mapeamento da rede](./media/site-recovery-network-mapping-azure-to-azure/network-mapping3.png)


## <a name="mapping-network-when-enabling-replication"></a>Mapeamento de rede ao ativar a replicação

Se não é executado o mapeamento da rede quando estiver a replicar uma máquina virtual para Olá primeiro tempo formulário uma região do Azure tooanother, em seguida, pode escolher a rede de destino como parte da Olá mesmo processo. Recuperação de sites cria os mapeamentos de rede da região de tootarget de região de origem e a região de toosource de região de destino com base nesta seleção.   

![Mapeamento da rede](./media/site-recovery-network-mapping-azure-to-azure/network-mapping4.png)

Por predefinição, a recuperação de sites cria uma rede na região de destino Olá que é a rede de origem toohello idênticas e adicionando '-asr' como um nome de toohello sufixos de rede de origem Olá. Pode escolher uma rede já criada ao clicar em Personalizar.

![Mapeamento da rede](./media/site-recovery-network-mapping-azure-to-azure/network-mapping5.png)


Se o mapeamento da rede Olá já é concluído, não é possível alterar a rede virtual de destino Olá durante a ativação da replicação. toochange, modifique o mapeamento de rede existente.  

![Mapeamento da rede](./media/site-recovery-network-mapping-azure-to-azure/network-mapping6.png)

![Mapeamento da rede](./media/site-recovery-network-mapping-azure-to-azure/modify-network-mapping.png)

> [!IMPORTANT]
> Se modificar um mapeamento de rede de 1 região tooregion-2, certifique-se que modificar o mapeamento da rede Olá de região-2 tooregion-1 também.
>
>


## <a name="subnet-selection"></a>Seleção de sub-rede
Sub-rede Olá virtual da máquina de destino está selecionado com base no nome de Olá da sub-rede Olá Olá virtual da máquina de origem. Se existir uma sub-rede de Olá mesmo nome que Olá virtual da máquina de origem disponível na rede de destino Olá, em seguida, o que é escolhido para Olá máquina virtual de destino. Se não existir nenhuma sub-rede com Olá mesmo nome na rede de destino Olá, em seguida, por ordem alfabética primeira sub-rede é escolhido como Olá sub-rede de destino. Pode modificar esta sub-rede acedendo tooCompute e definições de rede da máquina virtual de Olá.

![Modificar a sub-rede](./media/site-recovery-network-mapping-azure-to-azure/modify-subnet.png)


## <a name="ip-address"></a>Endereço IP

Endereço IP para cada interface de rede Olá Olá virtual da máquina de destino é escolhido, da seguinte forma:

### <a name="dhcp"></a>DHCP
Se a interface de rede Olá Olá virtual da máquina de origem estiver a utilizar DHCP, a interface de rede da máquina de virtual de destino Olá também está definido como DHCP.

### <a name="static-ip"></a>IP estático
Se a interface de rede Olá Olá virtual da máquina de origem utilizar IP estático, a interface de rede Olá virtual da máquina de destino seja também definido toouse IP estático. IP estático é escolhido, da seguinte forma:

#### <a name="same-address-space"></a>Mesmo espaço de endereços

Se a sub-rede de origem Olá e a sub-rede de destino Olá têm Olá mesmo espaço de endereços, IP de destino é definida igual ao IP Olá Olá da interface de rede Olá virtual da máquina de origem. Se o mesmo IP não estiver disponível, alguns outro IP disponível está definido como Olá IP de destino.

#### <a name="different-address-space"></a>Espaço de endereços diferente

Se a sub-rede de origem Olá e a sub-rede de destino Olá têm espaço de endereços diferente, IP de destino está definido como qualquer IP disponível na sub-rede de destino Olá.

Pode modificar o IP de destino Olá em cada interface de rede acedendo tooCompute e definições de rede da máquina virtual de Olá.

## <a name="next-steps"></a>Passos seguintes

- Saiba mais sobre [redes orientações para replicar as VMs do Azure](site-recovery-azure-to-azure-networking-guidance.md).
