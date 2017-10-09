---
title: "aaaFailover na recuperação de Site | Microsoft Docs"
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
ms.date: 07/04/2017
ms.author: pratshar
ms.openlocfilehash: 7cacea829d78bb7de2b2d67402291b472b10f023
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="failover-in-site-recovery"></a>Reativação pós-falha na Recuperação de Sites
Este artigo descreve como toofailover máquinas de virtuais e servidores físicos protegidos pela recuperação de sites.

## <a name="prerequisites"></a>Pré-requisitos
1. Antes de efetuar uma ativação pós-falha, efetue um [ativação pós-falha de teste](site-recovery-test-failover-to-azure.md) tooensure que tudo está a funcionar conforme esperado.
1. [Preparar a rede de Olá](site-recovery-network-design.md) na localização de destino antes de efetuar uma ativação pós-falha.  


## <a name="run-a-failover"></a>Executar uma ativação pós-falha
Este procedimento descreve como toorun uma ativação pós-falha de um [plano de recuperação](site-recovery-create-recovery-plans.md). Em alternativa pode executar a ativação pós-falha de Olá para uma única máquina virtual ou um servidor físico partir Olá **replicado itens** página


![Ativação pós-falha](./media/site-recovery-failover/Failover.png)

1. Selecione **planos de recuperação** > *recoveryplan_name*. Clique em **ativação pós-falha**
2. No Olá **ativação pós-falha** ecrã, selecione um **ponto de recuperação** toofailover para. Pode utilizar uma das seguintes opções de Olá:
    1.  **Mais recente** (predefinição): esta opção primeiro processa todos os dados de Olá foram enviado tooSite recuperação serviço toocreate um ponto de recuperação para cada máquina virtual antes de efetuá-los a ativação pós-falha tooit. Esta opção fornece Olá RPO mais baixo (objetivo de ponto de recuperação) como Olá máquina virtual criada após ativação pós-falha tem todos os dados de Olá foi replicado tooSite serviço de recuperação quando a ativação pós-falha de Olá foi acionada.
    1.  **Mais recentes processados**: esta opção se falhar a todas as máquinas virtuais Olá recuperação plano toohello mais recente do ponto de recuperação que já tenha sido processada pelo serviço de recuperação de sites. Quando estiver a efetuar ativação pós-falha de teste de uma máquina virtual, carimbo de hora do último ponto de recuperação processados Olá também é apresentado. Se estão a fazer a ativação pós-falha de um plano de recuperação, pode ir a máquina virtual de tooindividual e observe **pontos de recuperação mais recente** mosaico tooget estas informações. Como não tempo é gasto tooprocess Olá dados não processados, esta opção fornece uma opção de ativação pós-falha baixa RTO (objetivo de tempo de recuperação).
    1.  **Mais recente consistentes da aplicação**: esta opção se falhar a todas as máquinas virtuais Olá plano toohello mais recente aplicação consistente de recuperação do ponto de recuperação que já tenha sido processada pelo serviço de recuperação de sites. Quando estão a fazer ativação pós-falha de teste de uma máquina virtual, o carimbo de hora do último ponto de recuperação consistentes da aplicação Olá também é apresentado. Se estão a fazer a ativação pós-falha de um plano de recuperação, pode ir a máquina virtual de tooindividual e observe **pontos de recuperação mais recente** mosaico tooget estas informações.
    1.  **Mais recente várias VMS processados**: esta opção só está disponível para planos de recuperação que têm, pelo menos, uma máquina virtual com consistência de várias VMS no. Ponto de máquinas virtuais que fazem parte de uma grupo ativação pós-falha toohello mais recente comuns várias VMS consistente recuperação de replicação. Outro máquinas virtuais ativação pós-falha tootheir mais recente processados ponto de recuperação.  
    1.  **Mais recente várias VMS consistentes da aplicação**: esta opção só está disponível para planos de recuperação que tenha, pelo menos, uma máquina virtual com ON de consistência de várias VMS. Máquinas virtuais que fazem parte de uma replicação do grupo de ativação pós-falha toohello mais recente várias VMS consistentes com aplicações ponto de recuperação comum. Outra máquinas virtuais ativação pós-falha tootheir mais recente consistentes com aplicações do ponto de recuperação.
    1.  **Personalizada**: Se estiver a efetuar ativação pós-falha de teste de uma máquina virtual, em seguida, pode utilizar esta opção toofailover tooa recuperação determinado ponto.

    > [!NOTE]
    > Olá opção toochoose um ponto de recuperação só está disponível quando estão a falhar tooAzure.
    >
    >


1. Se algumas das máquinas de virtuais Olá no plano de recuperação Olá foram a ativação pós-falha numa execução anterior e agora Olá máquinas de virtuais estão ativas na localização de origem e destino, pode utilizar **mudar a direção** opção direção de Olá toodecide no deverá ocorrer que Olá ativação pós-falha.
1. Se estiver a efetuar a ativação pós-falha de tooAzure e encriptação de dados é ativada para a nuvem de Olá (aplica-se apenas quando proteger máquinas virtuais Hyper-v de um servidor VMM), na **chave de encriptação** certificado Olá selecione que foi emitido quando a Ativar a encriptação de dados durante a configuração no servidor do VMM Olá.
1. Selecione **encerrar a máquina antes de iniciar a ativação pós-falha** se pretender que a recuperação de sites tooattempt toodo um encerramento de máquinas virtuais de origem antes de acionar Olá ativação pós-falha. Ativação pós-falha continua, mesmo se falha de encerramento.  

    > [!NOTE]
    > Em caso de máquinas virtuais de Hyper-v, esta opção também tenta toosynchronize Olá no local dados que tem ainda não foram enviados toohello serviço antes de acionar a ativação pós-falha de Olá.
    >
    >

1. Pode seguir o progresso de ativação pós-falha Olá no Olá **tarefas** página. Mesmo se ocorrerem erros durante uma ativação pós-falha não planeada, o plano de recuperação Olá é executada até estar concluída.
1. Após a ativação pós-falha de Olá, valide a máquina virtual de Olá iniciando sessão tooit. Se quiser toogo outro ponto de recuperação para a máquina virtual de Olá, em seguida, pode utilizar **alterar o ponto de recuperação** opção.
1. Quando estiver satisfeito com Olá efetuada a ativação pós-falha da máquina virtual, pode **consolidar** Olá ativação pós-falha. Isto elimina todos os pontos de recuperação de Olá disponíveis com o serviço de Olá e **alterar o ponto de recuperação** opção deixará de estar disponível.

## <a name="planned-failover"></a>Ativação pós-falha planeada
Além de ativação pós-falha, as máquinas de virtuais de Hyper-V protegidas utilizando a recuperação de Site também suporte **a ativação pós-falha planeada**. Esta é uma zero opção do dados perda ativação pós-falha. Quando é acionada uma ativação pós-falha planeada, primeiro Olá máquinas virtuais são encerradas, dados de Olá ainda está sincronizada toobe sincronizada e, em seguida, é acionada uma ativação pós-falha de origem.

> [!NOTE]
> Quando a ativação pós-falha Hyper-v máquinas virtuais a partir de um local tooanother de site no local do site, toocome back toohello primário site no local tiver toofirst **replicar inversamente** site de back-tooprimary Olá máquina virtual e em seguida, acione uma ativação pós-falha. Se a máquina virtual primária de Olá não estiver disponível, em seguida, antes de começar demasiado**replicar inversamente** tiver toorestore Olá excluir máquina virtual de uma cópia de segurança.   
>
>

## <a name="failover-job"></a>Tarefa de ativação pós-falha

![Ativação pós-falha](./media/site-recovery-failover/FailoverJob.png)

Quando é acionada uma ativação pós-falha, envolve os seguintes passos:

1. Verificação de pré-requisitos: este passo garante que todas as condições necessárias para a ativação pós-falha são cumpridas
1. Ativação pós-falha: Este passo processa dados Olá e torna pronto para que uma máquina virtual do Azure podem ser criada fora do mesmo. Se tiver escolhido **mais recente** ponto de recuperação, este passo cria um ponto de recuperação dos dados de Olá que foi enviados toohello serviço.
1. Iniciar: Este passo cria uma máquina virtual do Azure utilizando os dados de Olá processados no passo anterior Olá.

> [!WARNING]
> **Não cancele um em curso ativação pós-falha**: antes de iniciar a ativação pós-falha, a replicação da máquina virtual de Olá está parada. Se lhe **Cancelar** uma tarefa de progresso, deixa de ativação pós-falha, máquina virtual de Olá, mas não será iniciada tooreplicate. Não é possível iniciar a replicação novamente.
>
>

## <a name="time-taken-for-failover-tooazure"></a>Tempo decorrido para tooAzure de ativação pós-falha

Em certos casos, a ativação pós-falha de máquinas virtuais requer um passo intermédio extra que normalmente demora cerca de 8 toocomplete de minutos too10. Nestes casos, são seguintes:

* Máquinas virtuais VMware com o serviço de mobilidade da versão mais antiga do que 9.8
* Servidores físicos 
* Máquinas virtuais Linux de VMware
* Máquinas virtuais de Hyper-V protegidas como servidores físicos
* Máquinas virtuais VMware onde seguintes controladores não estão presentes como controladores de arranque 
    * storvsc 
    * VMBus 
    * storflt 
    * intelide 
    * ATAPI
* Máquinas virtuais VMware que não tenham o serviço DHCP ativado independentemente se estão a utilizar DHCP ou estático de endereços IP

No Olá todos os outros casos este passo intermédio não é necessário e tempo de Olá decorrido para a ativação pós-falha Olá é significativamente inferior. 





## <a name="using-scripts-in-failover"></a>Utilizar scripts na ativação pós-falha
Pode querer tooautomate determinadas ações ao efetuar uma ativação pós-falha. Pode utilizar scripts ou [runbooks de automatização do Azure](site-recovery-runbook-automation.md) no [planos de recuperação](site-recovery-create-recovery-plans.md) toodo que.

## <a name="other-considerations"></a>Outras considerações
* **Letra de unidade** — letra de unidade de Olá tooretain em máquinas virtuais após a ativação pós-falha pode definir Olá **SAN política** para Olá virtual máquina demasiado**OnlineAll**. [Leia mais](https://support.microsoft.com/en-us/help/3031135/how-to-preserve-the-drive-letter-for-protected-virtual-machines-that-are-failed-over-or-migrated-to-azure).



## <a name="next-steps"></a>Passos seguintes
Depois de ter a executar a ativação pós-falha de máquinas virtuais e o Centro de dados no local Olá estiver disponível, deve [ **voltar a proteger** ](site-recovery-how-to-reprotect.md) toohello de centro de dados no local de cópia de máquinas virtuais VMware.

Utilize [ **a ativação pós-falha planeada** ](site-recovery-failback-from-azure-to-hyper-v.md) opção demasiado**reativação pós-falha** tooon local de cópia de máquinas virtuais Hyper-v do Azure.

Se tiverem falhado através de um dados de local de tooanother da máquina virtual de Hyper-v center gerido pelo VMM server e Olá primário Centro de dados estiver disponível, em seguida, utilize **a replicação inversa** opção toostart Olá replicação inversa toohello Centro de dados principal.
