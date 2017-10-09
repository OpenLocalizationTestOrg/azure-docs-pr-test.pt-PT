---
title: "aaaRun uma ativação pós-falha de teste para o site secundário do tooa de replicação de VM de Hyper-V com o Azure Site Recovery | Microsoft Docs"
description: "Descreve como toorun uma ativação pós-falha de teste para tooa de replicação de VM de Hyper-V secundário para o System Center VMM do site com o Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: a3fd11ce-65a1-4308-8435-45cf954353ef
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/30/2017
ms.author: raynew
ms.openlocfilehash: a60411541c2db001c573735bcb0d651f6618f295
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="step-10-run-a-test-failover-for-hyper-v-replication-tooa-secondary-site"></a>Passo 10: Executar uma ativação pós-falha de teste para o site secundário do tooa de replicação de Hyper-V


Depois de ativar a replicação para máquinas virtuais de Hyper-V (VMs) com [do Azure Site Recovery](site-recovery-overview.md), utilize este artigo de toorun uma ativação pós-falha de teste. Uma ativação pós-falha de teste verifica que a replicação está a funcionar, sem afetar o seu ambiente de produção. 


Depois de ler este artigo, publique quaisquer comentários na parte inferior do hello, ou no Olá [fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="before-you-start"></a>Antes de começar

- Quando estiver a acionar uma ativação pós-falha de teste, pode especificar as réplica de teste toowhich de rede do Olá Olá que ligarão as VMs. [Saiba mais](site-recovery-test-failover-vmm-to-vmm.md#network-options-in-site-recovery) sobre as opções de rede Olá.
- Recomendamos que não escolha uma rede que selecionou durante o mapeamento da rede.
- instruções de Olá neste artigo descrevem como toofail através de uma única VM. Leia sobre [criar planos de recuperação](site-recovery-create-recovery-plans.md) se quiser toofail através de várias VMs em conjunto.
- Leia sobre [limitações para as ativações pós-falha de teste](site-recovery-test-failover-vmm-to-vmm.md#things-to-note).
- Olá endereço IP especificado tooa VM durante a ativação pós-falha de teste é Olá mesmo endereço IP que Olá VM receberia para uma ativação de pós-falha planeada ou imprevista (presuming que o endereço IP Olá está disponível na rede de ativação pós-falha de teste de Olá). Se o endereço IP Olá não está disponível na rede de ativação pós-falha de teste de Olá, Olá VM recebe outro endereço IP que está disponível na rede de ativação pós-falha de teste de Olá.
- Se pretender toodo uma ativação pós-falha de teste na sua rede de produção, para validatation completo da máquina de conectividade de rede ponto a ponto, tenha em atenção que:
    - Olá que VM principal deve ser encerrado quando estiver a efetuar ativação pós-falha de teste de Olá. Caso contrário, duas VMs com Olá mesma identidade será executado numa Olá mesmo rede em Olá mesmo tempo. 
    - Se efetuar alterações tootest VMs, essas alterações serão perdidas quando a limpeza Olá ativação pós-falha de teste. Estas alterações não são replicada toohello back VM principal.
    - Testar uma rede de produção leva toodowntime para as cargas de trabalho de produção. Peça aos utilizadores não toouse aplicação Olá quando exercício de recuperação de desastre Olá está em curso.  


## <a name="run-a-test-failover-for-a-vm"></a>Executar uma ativação pós-falha de teste para uma VM

1. toofail através de uma única VM, na **itens replicados**, clique em Olá VM > **ativação pós-falha de teste**.
2. No **ativação pós-falha de teste**, especifique como o teste VMs será ligado toonetworks após a ativação pós-falha de teste de Olá. 
3. Clique em **OK** toobegin ativação pós-falha de Olá. Controlar o progresso no Olá **tarefas** separador.
5. Após a conclusão da ativação pós-falha, certifique-se que teste Olá início VMs com êxito.
6. Quando tiver terminado, clique em **ativação pós-falha de teste de limpeza** no plano de recuperação Olá.
7. No **notas**, registar e guardar todas as observações associadas à ativação pós-falha de teste de Olá. Este passo elimina Olá máquinas de virtuais e redes que foram criados durante a ativação pós-falha de teste.


## <a name="next-steps"></a>Passos seguintes

Depois de ter testado implementação Olá, saiba mais sobre outros tipos de [ativação pós-falha](site-recovery-failover.md).
