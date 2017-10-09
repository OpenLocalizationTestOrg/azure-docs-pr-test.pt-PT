---
title: "arquitetura de Olá aaaReview para tooAzure de replicação (com o System Center VMM) de Hyper-V com o Azure Site Recovery | Microsoft Docs"
description: "Este artigo fornece uma descrição geral dos componentes e arquitetura utilizada quando replicar no local VMs de Hyper-V na tooAzure de nuvens do VMM, com o serviço do Azure Site Recovery Olá."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: c413efcd-d750-4b22-b34b-15bcaa03934a
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/24/2017
ms.author: raynew
ms.openlocfilehash: ee1f2775b0c929894933b639464176d7a0441519
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="step-1-review-hello-architecture"></a>Passo 1: Rever arquitetura Olá


Este artigo descreve os componentes de Olá e processos utilizados quando replicar no local máquinas de virtuais de Hyper-V em nuvens do System Center Virtual Machine Manager (VMM), tooAzure utilizando Olá [do Azure Site Recovery](site-recovery-overview.md) serviço.

Publique quaisquer comentários na parte inferior de Olá deste artigo ou no Olá [fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).



## <a name="architectural-components"></a>Componentes da arquitetura

Existem vários componentes envolvidos quando replicar VMs Hyper-V no tooAzure de nuvens do VMM.

**Componente** | **Requisito** | **Detalhes**
--- | --- | ---
**Azure** | No Azure, precisa de uma conta do Microsoft Azure, de uma conta de armazenamento do Azure e de uma rede do Azure. | Dados replicados são guardados na conta do storage Olá e as VMs do Azure são criadas com dados Olá replicado quando ocorre a ativação pós-falha do seu site no local.<br/><br/> Olá VMs do Azure ligar toohello rede virtual do Azure quando são criados.
**Servidor VMM** | servidor do VMM Olá tem uma ou mais nuvens que contêm anfitriões Hyper-V. | No servidor do VMM Olá instale a replicação de tooorchestrate do fornecedor da recuperação de Site de Olá com a recuperação de Site e registar o servidor de Olá no Olá que cofre dos serviços de recuperação.
**Anfitrião Hyper-V** | Um ou mais anfitriões/clusters de Hyper-V geridos pelo VMM. |  Instale o agente de serviços de recuperação de Olá em cada membro de anfitrião ou cluster.
**VMs de Hyper-V** | Uma ou mais VMs em execução num servidor de anfitrião Hyper-V. | Nada tem tooexplicitly instalado em VMs.
**Redes** |Lógicas e redes VM configurado no servidor do VMM Olá. Uma rede VM deve ser ligado tooa rede lógica que está associada à nuvem Olá. | Redes VM são mapeadas tooAzure de redes virtuais, para que as VMs do Azure estão localizadas numa rede quando são criados após a ativação pós-falha.

Saiba mais sobre os pré-requisitos de implementação de Olá e os requisitos para cada um destes componentes no Olá [matriz de suporte](site-recovery-support-matrix-to-azure.md).


**Figura 1: Replicar VMs em anfitriões Hyper-V no VMM nuvens tooAzure**

![Componentes](./media/vmm-to-azure-walkthrough-architecture/arch-onprem-onprem-azure-vmm.png)


## <a name="replication-process"></a>Processo de replicação

**Figura 2: Processo de replicação e a recuperação para tooAzure de replicação de Hyper-V**

![fluxo de trabalho](./media/vmm-to-azure-walkthrough-architecture/arch-hyperv-azure-workflow.png)

### <a name="enable-protection"></a>Ativar a proteção

1. Depois de ativar a proteção para uma VM de Hyper-V, no Olá portal do Azure ou no local, Olá **ativar a proteção** é iniciado.
2. Olá tarefa verifica que a máquina Olá está em conformidade com os pré-requisitos, antes de invocar Olá [CreateReplicationRelationship](https://msdn.microsoft.com/library/hh850036.aspx), tooset a replicação com definições de Olá que configurou.
3. tarefa de Olá começa a replicação inicial invocando Olá [StartReplication](https://msdn.microsoft.com/library/hh850303.aspx) método, tooinitialize uma replicação completa de VM e tooAzure de discos virtuais de VM de Olá a enviar.
4. Pode monitorizar a tarefa de Olá na Olá **tarefas** separador.      ![Lista de tarefas](media/vmm-to-azure-walkthrough-architecture/image1.png)![Ativar a desagregação da proteção](media/vmm-to-azure-walkthrough-architecture/image2.png)

### <a name="replicate-hello-initial-data"></a>Replicar os dados iniciais Olá

1. Um [instantâneo de VM Hyper-V](https://technet.microsoft.com/library/dd560637.aspx) é tirado quando a replicação inicial é acionada.
2. Discos rígidos virtuais são replicados um de cada vez até estiverem tooAzure copiados todos os. Isto pode demorar algum tempo, dependendo Olá tamanho da VM e largura de banda de rede. toooptimize a utilização da rede, consulte [como toomanage no local a utilização de largura de banda da rede de proteção de tooAzure](https://support.microsoft.com/kb/3056159).
3. Se ocorrerem alterações de disco enquanto a replicação inicial está em curso, Olá controlador de replicação de réplica do Hyper-V controla essas alterações como registos de replicação de Hyper-V (. hrl). Estes ficheiros estão localizados no Olá mesma pasta que os discos de Olá. Cada disco tem um ficheiro. hrl associado que será enviado toosecondary armazenamento.
4. ficheiros de registo e de instantâneo de Olá consumam recursos de disco enquanto a replicação inicial está em curso.
5. Quando a replicação inicial Olá estiver concluída, o instantâneo VM de Olá é eliminado. Alterações de disco delta no registo de Olá são sincronizadas e intercaladas toohello disco de principal.


### <a name="finalize-protection"></a>Finalizar a proteção

1. Após a replicação inicial Olá, hello **finalizar proteção na máquina virtual de Olá** tarefa configura a rede e outras definições de pós-replicação para que máquina virtual de Olá está protegida.
    ![Finalizar a tarefa de proteção](media/vmm-to-azure-walkthrough-architecture/image3.png)
2. Se estiver a replicar tooAzure, poderá ter definições de Olá tootweak para a máquina virtual de Olá, para que fique preparada para ativação pós-falha. Neste momento, pode executar um toocheck de ativação pós-falha de teste que tudo está a funcionar conforme esperado.

### <a name="replicate-hello-delta"></a>Replicar delta Olá

1. Após a replicação inicial Olá, começa a sincronização delta, de acordo com as definições de replicação.
2. Olá controlador de replicação de réplica do Hyper-V controla Olá alterações tooa disco virtual como ficheiros. hrl. Cada disco que está configurado para replicação tem um ficheiro .hrl associado. Este registo é enviado a conta de armazenamento do cliente de toohello após a conclusão da replicação inicial. Quando um registo estiver em trânsito tooAzure, Olá as alterações no disco principal Olá são controladas no outro ficheiro de registo, na Olá mesmo diretório.
3. Durante a replicação inicial e diferenças, pode monitorizar Olá VM na Olá vista VM. [Saiba mais](site-recovery-monitoring-and-troubleshooting.md#monitor-replication-health-for-virtual-machines).  

### <a name="synchronize-replication"></a>Sincronizar replicação

1. Se a replicação delta falhar, e uma replicação completa seria dispendiosa em termos de largura de banda ou de tempo, então uma VM fica marcada para ressincronização. Por exemplo, se os ficheiros. hrl Olá atingirem 50% do tamanho do disco Olá, em seguida, hello VM será marcada para ressincronização.
2.  A ressincronização minimiza a quantidade de Olá de dados enviados por computação de somas de verificação de máquinas de virtuais de origem e destino Olá e enviar apenas os dados delta Olá. A ressincronização utiliza um algoritmo de segmentação com blocos fixos, em que os ficheiros de origem e de destino estão divididos em segmentos fixos. As somas de verificação para cada segmento são geradas e, em seguida, em comparação com toodetermine que bloqueia a partir do destino do Olá origem necessidade toobe toohello aplicados.
3. Após a conclusão da ressincronização, a replicação delta normal deve ser retomada. Por predefinição, a ressincronização está agendada toorun automaticamente fora do horário, mas pode ressincronizar uma máquina virtual manualmente. Por exemplo, pode retomar a ressincronização se ocorrer uma indisponibilidade de rede ou de outro tipo. toodo esta, selecione Olá VM no portal de Olá > **ressincronizar**.

    ![Ressincronização manual](media/vmm-to-azure-walkthrough-architecture/image4.png)


### <a name="retry-logic"></a>Repetir a lógica

Se ocorrer um erro de replicação, haverá uma repetição interna. Esta lógica pode ser classificada em duas categorias:

**Categoria** | **Detalhes**
--- | ---
**Erros não recuperáveis** | Não é efetuada qualquer tentativa. O estado da VM será **Crítico**, e é necessária a intervenção do administrador. Exemplos destes erros incluem: rutura da cadeia de VHD Estado inválido para a réplica de Olá VM; Erros de autenticação de rede: erros de autorização VM erros não encontrado (para servidores autónomos do Hyper-V)
**Erros recuperáveis** | As repetições ocorrem a cada intervalo de replicação, utilizando um exponencial término que aumenta Olá tentativas de início de Olá da primeira tentativa de Olá por 1, 2, 4, 8 e de 10 minutos. Se o erro persistir, tente novamente a cada 30 minutos. Os exemplos incluem: erros de rede; erros de espaço insuficiente no disco; condições de falta de memória |



## <a name="failover-and-failback-process"></a>Processo de ativação pós-falha e de reativação pós-falha

1. Pode executar um planeadas ou imprevistas [ativação pós-falha](site-recovery-failover.md) de tooAzure de VMs de Hyper-V no local. Se executar uma ativação pós-falha planeada, em seguida, as VMs de origem são encerradas tooensure sem perda de dados.
2. Pode efetuar a ativação pós-falha de um único computador ou criar [planos de recuperação](site-recovery-create-recovery-plans.md) ativação pós-falha de tooorchestrate de várias máquinas.
4. Depois de executar a ativação pós-falha de Olá, deve ser Olá toosee capaz de criar as VMs da réplica no Azure. Pode atribuir um toohello de endereço IP público VM, se necessário.
5. Em seguida, consolidar toostart de ativação pós-falha de Olá aceder à carga de trabalho Olá da réplica de Olá VM do Azure.
6. Quando o site no local primário estiver novamente disponível, pode fazer a [reativação pós-falha](site-recovery-failback-from-azure-to-hyper-v.md). Pode iniciar uma ativação pós-falha planeada do site primário toohello do Azure. Para uma ativação pós-falha planeada que pode toofailback selecione toohello mesmo VM ou tooan alternativo de localização e sincronizar as alterações entre o Azure e no local, tooensure sem perda de dados. Quando as VMs são criadas no local, a consolidação de ativação pós-falha de Olá.




## <a name="next-steps"></a>Passos seguintes

Aceda demasiado[passo 2: consultar os pré-requisitos de implementação de Olá](vmm-to-azure-walkthrough-prerequisites.md)
