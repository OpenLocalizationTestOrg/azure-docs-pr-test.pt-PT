---
title: "aaaPlan de rede para a replicação do VMware tooAzure | Microsoft Docs"
description: "Este artigo aborda de planeamento necessários quando replicar VMs de VMware tooAzure da rede"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 5578a0b4-0352-41c3-9cce-56beb17a4d97
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: 2b4f385c768cc7f5e98abae0afb8258b00f3724f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="step-4-plan-networking-for-vmware-tooazure-replication"></a>Passo 4: Planear o funcionamento em rede para a replicação de tooAzure de VMware

Este artigo resume rede considerações de planeamento quando replicar no local tooAzure de VMs de VMware utilizando Olá [do Azure Site Recovery](site-recovery-overview.md) serviço.

Publique quaisquer comentários na parte inferior deste artigo hello, ou colocar questões no Olá [fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="connect-tooreplica-vms"></a>Ligar as VMs de tooreplica

Ao planear a replicação e a estratégia de ativação pós-falha, uma das perguntas chave Olá é como tooconnect toohello VM do Azure após a ativação pós-falha. Existem duas opções ao conceber a estratégia de rede para a réplica de VMs do Azure:

- **Utilize o endereço IP diferente**: pode selecionar toouse um intervalo de endereços IP diferentes para Olá replicado a rede VM do Azure. Olá este cenário VM obtém um novo endereço IP, após a ativação pós-falha e é necessária uma atualização DNS.
- **Manter o mesmo endereço IP**: É aconselhável toouse Olá mesmo intervalo de endereços IP que no seu site no local primário, Olá rede Azure após a ativação pós-falha. Olá manter os mesmos endereços IP simplifica a recuperação de Olá, reduzindo relativamente a problemas de rede após a ativação pós-falha. No entanto, quando está a replicar tooAzure, terá de rotas tooupdate com a localização nova Olá endereços IP Olá após a ativação pós-falha. 


## <a name="retain-ip-addresses"></a>Manter os endereços IP

Recuperação de sites fornece a capacidade de Olá tooretain fixo endereços IP quando efetuar a ativação pós-falha tooAzure, com uma sub-rede de ativação pós-falha.

Com a ativação pós-falha de sub-rede, uma sub-rede específica está presente no Site 1 ou 2 do Site, mas nunca em ambos os sites em simultâneo. Na ordem toomaintain Olá espaço de endereços IP no evento Olá de uma ativação pós-falha, é através de programação dispor Olá router infraestrutura toomove Olá sub-redes de um site tooanother. Durante a ativação pós-falha, Olá sub-redes mover com Olá associados a máquinas virtuais protegidas. desvantagem principal Olá é que o evento de Olá de uma falha, têm toomove Olá todo sub-rede.


### <a name="failover-example"></a>Exemplo de ativação pós-falha

Vamos ver um exemplo de tooAzure de ativação pós-falha.

- Uma empresa de ficticious, o Woodgrove Bank, tem uma infraestrutura no local, as aplicações de empresas de alojamento. As aplicações móveis estão alojadas no Azure.
- A conectividade entre VMs do Banco Woodgrove nos servidores do Azure e no local é fornecida por uma ligação de (VPN) de site a site entre a rede de limite Olá no local e Olá rede virtual do Azure.
- Isto significa VPN que Olá da rede virtual da empresa no Azure aparece como uma extensão da sua rede no local.
- Woodgrove pretende tooAzure de cargas de trabalho do toouse recuperação de Site tooreplicate no local.
 - Woodgrove tem toodeal com as aplicações e configurações que dependem hard-coded endereços IP e, por conseguinte, tem de endereços IP tooretain para as aplicações após tooAzure de ativação pós-falha.
 - Woodgrove tem endereços IP do intervalo 172.16.1.0/24, 172.16.2.0/24 tooits recursos atribuídos em execução no Azure.


Para Woodgrove toobe capaz de tooreplicate respetivo tooAzure VMS enquanto mantém Olá IP endereços, é aqui que empresa Olá tem toodo:

1. Crie uma rede virtual do Azure. Deve ser uma extensão de Olá no local rede, para que as aplicações podem efetuar a ativação pós-falha totalmente integrada.
2. O Azure permite-lhe tooadd local para conetividade VPN, além disso redes do toohello de conetividade toopoint para o site virtual criadas no Azure.
3. Quando configurar a ligação de site a site Olá, no Olá Azure de rede, pode encaminhar localização do tráfego toohello no local (rede local) apenas se o intervalo de endereços IP Olá é diferente do intervalo de endereços IP Olá no local.
    - Isto acontece porque o Azure não suporta sub-redes Stretch. Por isso, se tiver de sub-rede 192.168.1.0/24 no local, não é possível adicionar um 192.168.1.0/24 local da rede no Olá rede do Azure.
    - Isto é esperado porque o Azure não sabe que existem sem VMs do Active Directory na sub-rede Olá e essa sub-rede Olá está a ser criada para a recuperação de desastre apenas.
    - toobe toocorrectly consegue encaminhar o tráfego de rede fora de uma rede Azure Olá sub-redes rede Olá e Olá da rede local não pode entrar em conflito.

![Antes da ativação pós-falha de sub-rede](./media/site-recovery-network-design/network-design7.png)

### <a name="before-failover"></a>Antes da ativação pós-falha

1. Crie uma rede adicional (por exemplo rede recuperação). Esta é Olá rede em que executar a ativação pós-falha de VMs são criados.
2. tooensure hello endereço IP para uma VM é mantido após uma ativação pós-falha, nas propriedades VM Olá > **configurar**, especifique Olá esse Olá VM tem no local e clique em de endereços IP mesmo **guardar**.
3. Quando Olá VM é efetuada a ativação pós-falha, o Azure Site Recovery atribuirá Olá fornecido tooit de endereço IP.

    ![Propriedades da rede](./media/site-recovery-network-design/network-design8.png)

4. Após a ativação pós-falha acionador é acionado e Olá VMs são criadas no Azure com o endereço IP Olá necessário, pode ligar toohello rede utilizando um [Vnet tooVnet ligação](../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md). Esta ação pode ser colocado em script.
5. Tem de rotas toobe adequadamente modificado, tooreflect esse 192.168.1.0/24 foi agora movido tooAzure.

    ![Após a ativação pós-falha de sub-rede](./media/site-recovery-network-design/network-design9.png)

### <a name="after-failover"></a>Após a ativação pós-falha

Se não tiver uma rede do Azure, conforme ilustrado acima, pode criar uma ligação de VPN de site a site entre o site primário e o Azure, após a ativação pós-falha.

## <a name="change-ip-addresses"></a>Alterar os endereços IP

Isto [blogue](http://azure.microsoft.com/blog/2014/09/04/networking-infrastructure-setup-for-microsoft-azure-as-a-disaster-recovery-site/) explica como tooset segurança Olá infraestrutura de rede do Azure quando não precisar tooretain IP endereços após a ativação pós-falha. Começa com uma descrição da aplicação, procura como tooset configurar redes no local e no Azure e conclui com informações sobre como executar as ativações pós-falha.  

## <a name="next-steps"></a>Passos seguintes

Aceda demasiado[passo 5: preparar o Azure](vmware-walkthrough-prepare-azure.md)
