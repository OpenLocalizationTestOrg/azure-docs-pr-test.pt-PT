---
title: "aaaSet configurar uma política de replicação de VM de Hyper-V tooAzure de replicação (sem VMM do System Center) com o Azure Site Recovery | Microsoft Docs"
description: "Resume os passos de Olá terá tooset configurar uma política de replicação quando replicar VMs Hyper-V tooAzure armazenamento"
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 1777e0eb-accb-42b5-a747-11272e131a52
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/22/2017
ms.author: raynew
ms.openlocfilehash: 4bd7161f4a0f015da0ecf595fbc6861ede5d68b0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="step-9-set-up-a-replication-policy-for-hyper-v-vm-replication-tooazure"></a>Passo 9: Configurar uma política de replicação para tooAzure de replicação de VM de Hyper-V

Este artigo descreve como tooset configurar uma política de replicação quando está a replicar VMs Hyper-V tooAzure (sem VMM do System Center) utilizando Olá [do Azure Site Recovery](site-recovery-overview.md) serviço no Olá portal do Azure.


Publique comentários e perguntas na parte inferior de Olá deste artigo ou no Olá [fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="about-snapshots"></a>Sobre instantâneos

Hyper-V utiliza dois tipos de instantâneos – um instantâneo padrão que fornece um instantâneo incremental de toda a máquina virtual Olá e um instantâneo consistente com aplicações, que tira um instantâneo de ponto no tempo dos dados de aplicação Olá no interior da máquina virtual de Olá.
    - Instantâneos consistentes com aplicações utilizam tooensure do serviço de cópia de sombra de Volume (VSS) que aplicações estão num estado consistente quando se obtém o instantâneo de Olá.
    - Se ativar instantâneos consistentes com aplicações, afetará o desempenho de Olá das aplicações em execução em máquinas virtuais de origem. Certifique-se de que valor Olá definido é inferior ao número de Olá de pontos de recuperação adicionais que configura.

## <a name="set-up-a-replication-policy"></a>Configurar uma política de replicação

1. toocreate uma nova política de replicação, clique em **preparar a infraestrutura** > **as definições de replicação** > **+ criar e associar**.

    ![Rede](./media/hyper-v-site-walkthrough-replication/gs-replication.png)
2. Em **Criar e associar política**, especifique um nome de política.
3. No **copiar frequência**, especifique a frequência pretende que os tooreplicate delta dados após a replicação inicial de Olá (cada 30 segundos, 5 ou 15 minutos).

    > [!NOTE]
    > Uma frequência de segundo 30 não é suportada quando replicar toopremium armazenamento. limitação de Olá é determinada pelo número do Olá de instantâneos por blob (100) suportado pelo armazenamento premium. [Saiba mais](../storage/common/storage-premium-storage.md#snapshots-and-copy-blob).

4. No **retenção do ponto de recuperação**, especifique, em horas quanto tempo é de janela de retenção de Olá para cada ponto de recuperação. As VMs podem ser recuperados tooany ponto nessa janela.
5. No **frequência de instantâneos consistentes com aplicação**, especifique a frequência (1-12 horas) pontos de recuperação que contêm instantâneos consistentes com aplicações são criados.
6. No **hora de início da replicação inicial**, especifique quando toostart Olá a replicação inicial. replicação de Olá ocorre através da sua largura de banda de internet, pelo que poderá ser útil tooschedule-lo fora do horário de trabalho. Em seguida, clique em **OK**.

    ![Política de replicação](./media/hyper-v-site-walkthrough-replication/gs-replication2.png)

Quando cria uma nova política,-la automaticamente associado ao site de Hyper-V Olá. Pode associar um site Hyper-V (e Olá VMs na mesma) várias políticas de replicação no **replicação** > nome da política > **associar o Site de Hyper-V**.



## <a name="next-steps"></a>Passos seguintes

Aceda demasiado[passo 10: Ativar a replicação](hyper-v-site-walkthrough-enable-replication.md)
