---
title: "Replicar VMs do Azure entre regiões do Azure para recuperação após desastre tem: tooAzure do Azure | Microsoft Docs"
description: "Resume os passos de Olá precisa de VMs do Azure tooreplicate entre regiões do Azure (Azure para o Azure) com o serviço do Azure Site Recovery Olá para as necessidades de recuperação após desastre."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmon
editor: 
ms.assetid: dab98aa5-9c41-4475-b7dc-2e07ab1cfd18
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/10/2017
ms.author: raynew
ms.openlocfilehash: c4c425af260a9bcc3dd4dcc13da26109e20f03bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-azure-vms-between-regions-with-azure-site-recovery"></a>Replicar VMs do Azure entre regiões com o Azure Site Recovery

>[!NOTE]
>
> Azure Site Recovery replicação para máquinas de virtuais (VMs) do Azure está atualmente em pré-visualização.

Este artigo descreve como tooreplicate VMs do Azure entre regiões do Azure utilizando Olá [recuperação de Site](site-recovery-overview.md) serviço no Olá portal do Azure.

Publique comentários e perguntas na parte inferior de Olá deste artigo ou no Olá [fórum do Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="disaster-recovery-in-azure"></a>Recuperação após desastre no Azure

Funcionalidades e capacidades de infraestrutura do Azure incorporada contribuem tooa estratégia de disponibilidade robusto e resiliente para cargas de trabalho que são executados em VMs do Azure. No entanto, existem muitos motivos por que motivo precisa tooplan para recuperação após desastre entre regiões do Azure por si:

- Terá das diretrizes de conformidade toomeet para aplicações específicas e cargas de trabalho que requerem uma continuidade do negócio e a estratégia de recuperação (BCDR) de desastre.
- Pretende Olá capacidade tooprotect e recuperar as VMs do Azure com base nas suas decisões de negócio e não apenas com base na funcionalidade do Azure integrada.
- Terá de tootest de ativação pós-falha e recuperação de acordo com as suas necessidades comerciais e de conformidade, sem afetar a produção.
- Tem de toofail através de região de recuperação toohello no evento Olá de um desastre e falhar back toohello região de origem original de forma totalmente integrada.

Utilizar a recuperação de Site para a VM do Azure para o Azure replicação toohelp fizer todas estas tarefas.


## <a name="why-use-site-recovery"></a>Por que utilizar a Recuperação de Sites?      

Recuperação de sites fornece uma forma simples tooreplicate VMs do Azure entre regiões:

- **Implementação automática**. Ao contrário de um modelo de replicação ativo-ativo, não é necessário para uma infraestrutura dispendiosas e complexa na região secundária Olá. Ao ativar a replicação, a recuperação de sites cria automaticamente recursos Olá necessária na região de destino Olá, com base nas definições de região de origem.
- **Controlar regiões**. Com a recuperação de Site, pode replicar a partir de qualquer região de tooany região dentro de um continente. Compare-as com o armazenamento georredundante de acesso de leitura, o que replica de forma assíncrona entre padrão [emparelhado regiões](https://docs.microsoft.com/azure/best-practices-availability-paired-regions) apenas. Armazenamento georredundante com acesso de leitura fornece dados de toohello acesso só de leitura na região de destino Olá.
- **Automatizada replicação**. Recuperação de sites fornece automatizada replicação contínua. Ativação pós-falha e a reativação pós-falha podem ser acionadas com um único clique.
- **RTO e RPO**. Recuperação de site tira partido da infraestrutura de rede do Azure de Olá que liga regiões tookeep RTO e RPO muito baixo.
- **Testar**. Pode executar simulações de recuperação após desastre com as ativações pós-falha de teste a pedido, como e quando for necessárias, sem afetar as cargas de trabalho de produção ou a replicação em curso.
- **Planos de recuperação**. Pode utilizar a ativação pós-falha de tooorchestrate de planos de recuperação e a reativação pós-falha da aplicação todo Olá em execução em várias VMs. funcionalidade de plano de recuperação Olá tem integração de primeira classe avançada com runbooks de automatização do Azure.


## <a name="deployment-summary"></a>Resumo de implementação

Eis um resumo de que precisa toodo tooset a replicação de VMs entre regiões do Azure:

1. Crie um cofre dos Serviços de Recuperação. cofre Olá contém definições de configuração e orquestra a replicação.
2. Ative a replicação para Olá VMs do Azure.
3. Execute um toomake de ativação pós-falha de teste se tudo está a funcionar conforme esperado.

>[!IMPORTANT]
>
> Pode verificar Olá [matriz de suporte para a replicação de VM do Azure](./site-recovery-support-matrix-azure-to-azure.md).

>[!IMPORTANT]
>
> Para obter informações sobre como o tooconfigure Olá necessárias conectividade de saída de rede para as VMs do Azure para replicação de recuperação de sites, consulte Olá [rede documento de orientação](./site-recovery-azure-to-azure-networking-guidance.md).

### <a name="before-you-start"></a>Antes de começar

* A conta de utilizador do Azure tem toohave determinadas [permissões](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) tooenable a replicação da máquina virtual do Azure.
* A subscrição do Azure deve estar ativada toocreate VMs na localização de destino Olá que pretende que o toouse como região de recuperação de desastre Olá. Contacte o suporte tooenable Olá necessário quota.

## <a name="create-a-recovery-services-vault"></a>Criar um cofre dos Serviços de Recuperação 

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]

>[!NOTE]
>
> Recomendamos que crie o Cofre de serviços de recuperação de Olá na localização de olá onde pretende que o seu tooreplicate VMs. Por exemplo, se a localização de destino é hello centro dos EUA, criar cofre Olá **EUA Central**.

## <a name="enable-replication"></a>Ativar a replicação

No **cofres dos serviços de recuperação**, clique em nome do cofre Olá. No Cofre de Olá, clique em Olá **+ replicar** botão.

### <a name="step-1-configure-hello-source"></a>Passo 1. Configurar a origem de Olá
1. No **origem**, selecione **Azure - pré-visualização**.
2. No **localização de origem**, selecione a origem de Olá região do Azure onde as VMs estão a ser executados.
3. Modelo de implementação de Olá selecione das suas VMs: **Resource Manager** ou **clássico**.
4. Selecione Olá **grupo de recursos de origem** para as VMs do Gestor de recursos ou **serviço em nuvem** para VMs clássicas.

    ![Configurar a origem de Olá](./media/site-recovery-azure-to-azure/source.png)

### <a name="step-2-select-virtual-machines"></a>Passo 2. Selecione as máquinas virtuais

* Selecione Olá VMs que pretende tooreplicate e, em seguida, clique em **OK**.

    ![Selecione as VMs](./media/site-recovery-azure-to-azure/vms.png)

### <a name="step-3-configure-settings"></a>Passo 3. Configurar definições

1. predefinição de Olá toooverride as definições de destino e especifique as definições de Olá à sua escolha, clique em **personalizar**. Para obter mais informações, consulte [Personalizar recursos de destino](site-recovery-replicate-azure-to-azure.md##customize-target-resources).

    ![Configurar definições](./media/site-recovery-azure-to-azure/settings.png)


2. Por predefinição, a recuperação de sites cria uma política de replicação que tem instantâneos consistentes com aplicação todas as 4 horas e mantém pontos de recuperação durante 24 horas. toocreate uma política com diferentes definições, clique em **personalizar** seguinte demasiado**política de replicação**.

    ![Personalizar a política](./media/site-recovery-azure-to-azure/customize-policy.png)

3. toostart aprovisionamento Olá recursos do destino, clique em **criar recursos de destino**. Aprovisionamento leva um minuto ou. Não feche o painel de Olá durante o aprovisionamento ou precisar de toostart sobre.

4. replicação tootrigger de Olá selecionada VM, clique em **ativar a replicação**.

5. Pode controlar o progresso de Olá **ativar a proteção** da tarefa no **definições** > **tarefas** > **tarefas de recuperação de Site**.

6. No **definições** > **itens replicados**, pode ver o estado de Olá de VMs e Olá progresso da replicação inicial. Clique em Olá VM toodrill para baixo para as respetivas definições.

## <a name="run-a-test-failover"></a>Executar uma ativação pós-falha de teste

Depois de configurar tudo, execute um toomake de ativação pós-falha de teste se tudo está a funcionar conforme esperado:

1. toofail através de uma única máquina no **definições** > **itens replicados**, clique em Olá VM **+ ativação pós-falha de teste** ícone.

2. Planear toofail através de uma recuperação, na **definições** > **planos de recuperação**, plano do contexto Olá **ativação pós-falha de teste**. toocreate um plano de recuperação, [siga estas instruções](site-recovery-create-recovery-plans.md). 

3. No **ativação pós-falha de teste**, selecione toowhich de rede virtual do Azure de destino Olá VMs do Azure estão ligadas após a ocorrência da ativação pós-falha de Olá.

4. toostart Olá ativação pós-falha, clique em **OK**. tootrack progresso, clique em Olá VM tooopen as respetivas propriedades. Ou pode clicar em Olá **ativação pós-falha de teste** tarefa no nome do cofre Olá > **definições** > **tarefas** > **astarefasderecuperaçãodesites**.

5. Depois de Olá conclusão ativação pós-falha, réplica Olá máquina do Azure é apresentado no portal do Azure de Olá > **máquinas virtuais**. Certifique-se que Olá VM Olá um tamanho adequado, que tenha ligado toohello adequada de rede, e que está em execução.

6. Olá toodelete VMs que foram criados durante a ativação pós-falha de teste de Olá, clique em **ativação pós-falha de teste de limpeza** em Olá replicadas item ou Olá plano de recuperação. No **notas**, registar e guardar todas as observações associadas à ativação pós-falha de teste de Olá. 

[Saiba mais](site-recovery-test-failover-to-azure.md) sobre as ativações pós-falha de teste.


## <a name="next-steps"></a>Passos seguintes

Depois de testar a implementação de Olá:

- [Saiba mais](site-recovery-failover.md) sobre os diferentes tipos de ativações pós-falha e como toorun-los.
- Saiba mais sobre [planos de recuperação a utilizar](site-recovery-create-recovery-plans.md) tooreduce RTO.
