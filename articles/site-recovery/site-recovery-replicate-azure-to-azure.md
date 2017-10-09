---
title: "aplicações de aaaReplicate (tooAzure do Azure) | Microsoft Docs"
description: "Este artigo descreve como tooset a replicação de virtual máquinas em execução na região do Azure um demasiado noutra região no Azure."
services: site-recovery
documentationcenter: 
author: asgang
manager: rochakm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 5/22/2017
ms.author: asgang
ms.openlocfilehash: fb190dac14419f892a1c6b45a3d991d8005e4bd0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-azure-virtual-machines-tooanother-azure-region"></a>Replicar máquinas virtuais do Azure tooanother região do Azure



>[!NOTE]
>
> Replicação de recuperação de site para máquinas virtuais do Azure está atualmente em pré-visualização.

Este artigo descreve como tooset a replicação de virtual máquinas em execução numa região do Azure tooanother região do Azure.

## <a name="prerequisites"></a>Pré-requisitos

* artigo de Olá pressupõe que já sabe sobre recuperação de Site e o Cofre de serviços de recuperação. É necessário toohave um pre 'Cofre dos serviços de recuperação' criado.

    >[!NOTE]
    >
    > Recomenda-se que crie Olá "Cofre dos serviços de recuperação" na localização de olá onde pretende que o seu tooreplicate VMs. Por exemplo, se a localização de destino "E.U.A. Central", crie o Cofre "E.U.A. Central".

* Se estiver a utilizar as regras de grupos de segurança de rede (NSG) ou firewall proxy toocontrol acesso toooutbound a conectividade à internet no Olá VMs do Azure, certifique-se de que Olá de lista branca necessários URLs ou IPs. Consulte demasiado[documento de orientação do funcionamento em rede](./site-recovery-azure-to-azure-networking-guidance.md) para obter mais detalhes.

* Se tiver o ExpressRoute ou de uma ligação VPN entre no local e Olá da origem de localização no Azure, siga [considerações de recuperação de Site para o local tooon Azure ExpressRoute / configuração de VPN](site-recovery-azure-to-azure-networking-guidance.md#guidelines-for-existing-azure-to-on-premises-expressroutevpn-configuration) documento.

* A conta de utilizador do Azure tem toohave determinadas [permissões](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) tooenable a replicação da máquina virtual do Azure.

* A subscrição do Azure deve estar ativada toocreate VMs na localização de destino Olá pretende toouse como região DR. Pode contactar o suporte tooenable Olá necessário quota.

## <a name="enable-replication-from-azure-site-recovery-vault"></a>Ative a replicação do cofre do Azure Site Recovery
Nesta ilustração, iremos irá replicar as VMs em execução no toohello de localização do Azure Olá 'Oriental' Localização ' Sudeste Asiático '. passos de Olá são os seguintes:

 Clique em **+ replicar** na replicação de tooenable Olá cofre para máquinas de virtuais Olá.

1. **Origem:** refere-se toohello ponto de origem das máquinas de Olá que neste caso é **Azure**.

2. **Localização de origem:** é Olá região do Azure a partir de onde pretende tooprotect as máquinas virtuais. Nesta ilustração, a localização de origem Olá será 'Oriental'

3. **Modelo de implementação:** refere-se modelo de implementação do Azure toohello das máquinas de origem Olá. Pode selecionar qualquer uma das clássico ou do resource manager e as máquinas que pertençam modelo específico toohello serão apresentadas para proteção no passo seguinte Olá.

      >[!NOTE]
      >
      > Apenas pode replicar uma máquina virtual clássica e recuperá-la como uma máquina virtual clássica. Não é possível recuperá-la como uma máquina virtual do Gestor de recursos.

4. **Grupo de recursos:** -lo do toowhich de grupo de recursos de Olá as máquinas virtuais de origem pertence. Olá todas as VMs no grupo de recursos selecionado Olá serão apresentados para proteção no passo seguinte Olá.

    ![Ativar a replicação](./media/site-recovery-replicate-azure-to-azure/enabledrwizard1.png)

No **máquinas virtuais > Selecione as máquinas virtuais**, clique e selecione cada máquina que quiser tooreplicate. Só pode selecionar máquinas para as quais a replicação pode ser ativada. Em seguida, clique em OK.
    ![Ativar replicação](./media/site-recovery-replicate-azure-to-azure/virtualmachine_selection.png)


Na secção de definições pode configurar as propriedades do site de destino

1. **Localização de destino:** esta é a localização de olá onde os dados de máquina virtual de origem serão replicados. Consoante a sua localização máquinas selecionadas, a recuperação de sites irá fornecer que Olá lista de regiões de destino adequado.

    > [!TIP]
    > Recomenda-se localização de destino tookeep mesmo a partir da recuperação do seu Cofre de serviços.

2. **Grupo de recursos de destino:** é toowhich de grupo de recursos de Olá irão pertencer todas as suas máquinas virtuais replicadas. Por predefinição a ASR irá criar um novo grupo de recursos na região de destino Olá com um nome que o sufixo "asr". No caso de grupo de recursos criado pelo ASR já existir, será reutilizada. Também pode escolher toocustomize-lo tal como mostrado na secção de Olá abaixo.    
3. **Rede Virtual de destino:** por predefinição, a ASR irá criar uma nova rede virtual numa região de destino Olá com um nome que o sufixo "asr". Isto será mapeada tooyour rede de origem e será utilizado para qualquer proteção futura.

    > [!NOTE]
    > [Verifique os detalhes de rede](site-recovery-network-mapping-azure-to-azure.md) tooknow mais sobre o mapeamento da rede.

4. **As contas de armazenamento de destino:** por predefinição, a ASR irá criar Olá novo destino conta de armazenamento mimicking a configuração de armazenamento VM de origem. No caso de conta de armazenamento criada por ASR já existir, será reutilizada.

5. **As contas de armazenamento em cache:** ASR tem chamou o armazenamento de cache na região de origem Olá de conta de armazenamento adicional. Olá todas as alterações a acontecer no Olá VMs de origem são controladas e enviadas toocache conta de armazenamento antes de localização de destino esses toohello a replicar.

6. **Conjunto de disponibilidade:** por predefinição, a ASR irá criar uma novo conjunto de disponibilidade na região de destino Olá com um nome que o sufixo "asr". No caso de conjunto de disponibilidade criado pelo ASR já existir, será reutilizada.

7.  **Política de replicação:** define Olá as definições de recuperação ponto retenção histórico e aplicação consistente frequência de instantâneos. Por predefinição, a ASR irá criar uma nova política de replicação com as predefinições dos ' 24 horas para retenção do ponto de recuperação e ' 60 minutos para a frequência de instantâneos consistentes da aplicação.

    ![Ativar a replicação](./media/site-recovery-replicate-azure-to-azure/enabledrwizard3.PNG)

## <a name="customize-target-resources"></a>Personalizar a recursos de destino

No caso de pretender que as predefinições de Olá toochange utilizadas pelo ASR, pode alterar as definições de Olá com base nas suas necessidades.

1. **Personalizar:** clique nele toochange Olá as predefinições utilizadas por ASR.

2. **Grupo de recursos de destino:** pode selecionar o grupo de recursos de Olá na lista de todos os grupos de recursos de Olá existente na localização de destino Olá numa subscrição Olá Olá.

3. **Rede Virtual de destino:** pode encontrar a lista de Olá de rede virtual de Olá todos os na localização de destino Olá.

4. **Conjunto de disponibilidade:** só é possível adicionar a disponibilidade conjuntos definições toohello máquinas virtuais que fazem parte de disponibilidade na região de origem.

5. **Contas de armazenamento de destino:**

![Ativar a replicação](./media/site-recovery-replicate-azure-to-azure/customize.PNG) clique em **criar o recurso de destino** e ativar a replicação


Depois de máquinas virtuais estão protegidas pode verificar o estado de Olá do Estado de funcionamento de VMs em **replicado itens**

>[!NOTE]
>Durante a Olá o momento da replicação inicial existe foi uma possibilidade que estado demora tempo toorefresh e não consegue ver o progresso durante algum tempo. Pode clicar no botão Atualizar Olá na parte superior de Olá de estado mais recente do Olá painel tooget Olá.
>

![Ativar a replicação](./media/site-recovery-replicate-azure-to-azure/replicateditems.PNG)


## <a name="next-steps"></a>Passos seguintes
- [Saiba mais](site-recovery-test-failover-to-azure.md) sobre como executar uma ativação pós-falha de teste.
- [Saiba mais](site-recovery-failover.md) sobre os diferentes tipos de ativações pós-falha e como toorun-los.
- Saiba mais sobre [planos de recuperação a utilizar](site-recovery-create-recovery-plans.md) tooreduce RTO.
- Saiba mais sobre [trocar as VMs do Azure](site-recovery-how-to-reprotect.md) após a ativação pós-falha.
