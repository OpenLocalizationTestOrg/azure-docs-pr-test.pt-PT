---
title: "Executar um exercício de recuperação de desastres para máquinas no local para o Azure com o Azure Site Recovery | Microsoft Docs"
description: "Saiba mais sobre como executar exercício de recuperação após desastre no local para o Azure, com o Azure Site Recovery"
services: site-recovery
author: rayne-wiselman
ms.service: site-recovery
ms.topic: tutorial
ms.date: 12/31/2017
ms.author: raynew
ms.openlocfilehash: f7dc5e2df95a64685a8b70d25e839c371d4fc2de
ms.sourcegitcommit: 85012dbead7879f1f6c2965daa61302eb78bd366
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 01/02/2018
---
# <a name="run-a-disaster-recovery-drill-to-azure"></a>Executar um teste de recuperação após desastre para o Azure

Este tutorial mostra como executar um exercício de recuperação de desastres para uma máquina no local para o Azure, utilizando uma ativação pós-falha de teste. Um exercício valida a estratégia de replicação sem perda de dados. Neste tutorial, ficará a saber como:

> [!div class="checklist"]
> * Configurar uma rede isolada a ativação pós-falha de teste
> * Preparar a ligação à VM do Azure após a ativação pós-falha
> * Executar uma ativação pós-falha de teste para uma única máquina

Este é o quarto tutorial uma série. Este tutorial parte do princípio de que já concluiu as tarefas nos tutoriais anteriores.

1. [Preparar o Azure](tutorial-prepare-azure.md)
2. [Preparar o VMware no local](tutorial-prepare-on-premises-vmware.md)
3. [Configurar a recuperação após desastre](tutorial-vmware-to-azure.md)

## <a name="verify-vm-properties"></a>Verifique as propriedades VM

Antes de executar uma ativação pós-falha de teste, verifique as propriedades da VM e certifique-se de que a VM está em conformidade com [requisitos do Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).

1. No **itens protegidos**, clique em **itens replicados** > VM.
2. No **replicados item** painel, existe um resumo das informações de VM, o estado de funcionamento, e pontos de recuperação mais recente disponível. Clique em **propriedades** para ver mais detalhes.
3. No **computação e rede**, pode modificar o nome do Azure, o grupo de recursos, o tamanho de destino, [conjunto de disponibilidade](../virtual-machines/windows/tutorial-availability-sets.md)e geridas as definições do disco.
   
      >[!NOTE]
      Reativação pós-falha para máquinas de Hyper-V no local a partir de VMs do Azure com discos geridos não é atualmente suportada. Só deve utilizar a opção de discos geridos para ativação pós-falha, se estiver a planear migrar VMs no local para o Azure, sem voltar a falhá-los.
   
4. Pode ver e modificar as definições de rede, incluindo a rede/sub-rede na qual a VM do Azure estarão localizada após a ativação pós-falha e o endereço IP que será atribuído ao mesmo.
5. No **discos**, pode ver informações sobre o sistema operativo e os discos de dados na VM.

## <a name="run-a-test-failover-for-a-single-vm"></a>Execute uma ativação pós-falha de teste para uma única VM

Quando executar uma ativação pós-falha de teste, ocorrerá o seguinte:

1. Verificação de um pré-requisitos é executado para se certificar de que todas as condições necessárias para a ativação pós-falha estão em vigor.
2. Ativação pós-falha processa os dados, para que uma VM do Azure podem ser criada. Se selecionar o ponto de recuperação mais recente, um ponto de recuperação é criado a partir de dados.
3. VM do Azure é criada utilizando os dados processados no passo anterior.

Execute a ativação pós-falha de teste da seguinte forma:

1. No **definições** > **itens replicados**, clique na VM > **+ ativação pós-falha de teste**.
2. Selecione o **mais recentes processados** ponto de recuperação para este tutorial. Esta ativação pós-falha da VM para o ponto mais recente no tempo. O carimbo de hora é apresentado. Com esta opção, não tempo é gasto a processar dados, pelo que fornece um RTO baixa (objetivo de tempo de recuperação).
3. No **ativação pós-falha de teste**, selecione o destino do Azure rede para as VMs do Azure serão ligadas após a ocorrência da ativação pós-falha.
4. Clique em **OK** para iniciar a ativação pós-falha. Pode controlar o progresso clicando na VM para abrir as respetivas propriedades. Ou pode clicar no **ativação pós-falha de teste** tarefa no nome do cofre > **definições** > **tarefas** >
   **tarefas de recuperação de Site**.
5. Após a ativação pós-falha, a réplica VM do Azure é apresentado no portal do Azure > **máquinas virtuais**. Certifique-se de que a VM é o tamanho adequado, tenha ligado à rede à direita, e que está em execução.
6. Agora deverá conseguir ligar à VM replicada no Azure.
7. Para eliminar as VMs do Azure criado durante a ativação pós-falha de teste, clique em **ativação pós-falha de teste de limpeza** na VM. No **notas**, registar e guardar todas as observações associadas à ativação pós-falha de teste.

Em alguns cenários, a ativação pós-falha requer processamento adicional, que demora cerca de oito a dez minutos a concluir. É possível que repare já tempos de ativação pós-falha para computadores VMware Linux, VMs de VMware que não tenham o permite o serviço DHCP e VMs de VMware que não tem os seguintes controladores de arranque de teste: storvsc, vmbus, storflt, intelide, atapi.

## <a name="next-steps"></a>Passos Seguintes

> [!div class="nextstepaction"]
> [Execute uma ativação pós-falha e a reativação pós-falha para as VMs de VMware no local](tutorial-vmware-to-azure-failover-failback.md).
