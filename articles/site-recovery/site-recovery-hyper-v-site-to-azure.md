---
title: aaaReplicate VMs de Hyper-V tooAzure | Microsoft Docs
description: "Descreve como tooorchestrate replicação, ativação pós-falha e recuperação do local Hyper-V VMs tooAzure"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: 1777e0eb-accb-42b5-a747-11272e131a52
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 04/05/2017
ms.author: raynew
ROBOTS: NOINDEX, NOFOLLOW
redirect_url: hyper-v-site-walkthrough-overview
ms.openlocfilehash: 6fba41e43823fc57511d51ea2e09691159693982
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-virtual-machines-without-vmm-tooazure-using-azure-site-recovery-with-hello-azure-portal"></a>Replicar tooAzure de máquinas virtuais (sem VMM) de Hyper-V com o Azure Site Recovery Olá portal do Azure

> [!div class="op_single_selector"]
> * [Portal do Azure](site-recovery-hyper-v-site-to-azure.md)
> * [Azure clássico](site-recovery-hyper-v-site-to-azure-classic.md)
> * [PowerShell – Resource Manager](site-recovery-deploy-with-powershell-resource-manager.md)
>
>

Este artigo descreve como tooreplicate no local tooAzure de máquinas virtuais de Hyper-V, utilizando [do Azure Site Recovery](site-recovery-overview.md) no Olá portal do Azure. VMs de Hyper-V esta implementação não são geridos pelo System Center Virtual Machine Manager (VMM).

Depois de ler este artigo, publique quaisquer comentários na parte inferior do hello, ou coloque questões técnicas no Olá [fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

Se quiser toomigrate máquinas tooAzure (sem a reativação pós-falha), saiba mais em [neste artigo](site-recovery-migrate-to-azure.md).



## <a name="deployment-steps"></a>Passos da implementação

Siga estes passos de implementação de Olá artigo toocomplete:

1. [Saiba mais](site-recovery-components.md#hyper-v-to-azure) sobre a arquitetura de Olá para esta implementação. Além disso, [veja](site-recovery-hyper-v-azure-architecture.md) como funciona a replicação de Hyper-V no Site Recovery.
2. Verifique os pré-requisitos e as limitações.
3. Configure uma rede do Azure e contas de armazenamento.
4. Prepare anfitriões Hyper-V.
5. Crie um cofre dos Serviços de Recuperação. cofre Olá contém definições de configuração e orquestra a replicação.
6. Especifique as definições da origem. Criar um site de Hyper-V que contenha os anfitriões de Hyper-V Olá e registe o site de Olá no Cofre de Olá. Instale Olá Azure Site Recovery Provider e o agente de serviços de recuperação do Microsoft hello, nos anfitriões de Olá Hyper-V.
7. Configure as definições do destino e da replicação.
8. Ative a replicação para Olá VMs.
9. Execute um toomake de ativação pós-falha de teste se que tudo está a funcionar conforme esperado.



## <a name="prerequisites"></a>Pré-requisitos


**Requisito** | **Detalhes** |
--- | --- |
**Azure** | Saiba mais sobre os [requisitos do Azure](site-recovery-prereq.md#azure-requirements).
**Servidores no local** | [Saiba mais](site-recovery-prereq.md#disaster-recovery-of-hyper-v-virtual-machines-to-azure-no-virtual-machine-manager) sobre os requisitos para anfitriões de Hyper-V Olá no local.
**VMs de Hyper-V no local** | As VMs que pretende tooreplicate devem estar a executar um [sistema operativo suportado](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions)e em conformidade com [pré-requisitos do Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).
**URLs do Azure** | Anfitriões Hyper-V tem de aceder toothese URLs:<br/><br/> [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]<br/><br/> Se tiver regras de firewall baseadas no endereço IP, certifique-se de que permitem comunicação tooAzure.<br/></br> Permitir Olá [intervalos de IP do Datacenter do Azure](https://www.microsoft.com/download/confirmation.aspx?id=41653)e Olá porta HTTPS (443).<br/></br> Permita intervalos de endereços IP para Olá região do Azure da sua subscrição e para EUA oeste (utilizado para gestão de identidade e controlo de acesso).



## <a name="prepare-for-deployment"></a>Preparar para a implementação

tooprepare para a implementação que tem de:

1. [Configurar uma rede Azure](#set-up-an-azure-network) no qual as VMs do Azure estarão localizadas quando são criados após a ativação pós-falha.
2. [Configurar uma conta de armazenamento do Azure](#set-up-an-azure-storage-account) para dados replicados.
3. [Preparar os anfitriões de Hyper-V de Olá](#prepare-the-hyper-v-hosts) tooensure poderem aceder ao hello necessários URLs.

### <a name="set-up-an-azure-network"></a>Configurar uma rede do Azure

Configure uma rede do Azure. Precisará disto, para que as VMs do Azure de Olá criadas após ativação pós-falha estão ligados tooa rede.

* rede de Olá deve estar no Olá mesma região que Olá do cofre dos serviços de recuperação.
* Consoante o modelo de recursos de Olá pretende toouse para efetuar a ativação pós-falha de VMs do Azure, configurou Olá rede Azure no [modo Resource Manager](../virtual-network/virtual-networks-create-vnet-arm-pportal.md), ou [modo clássico](../virtual-network/virtual-networks-create-vnet-classic-pportal.md).
* Recomendamos que configure uma rede antes de começar. Se não o fizer, terá de toodo-lo durante a implementação da recuperação de Site.
- As contas de armazenamento utilizadas pela recuperação de sites não podem ser [movido](../azure-resource-manager/resource-group-move-resources.md) dentro do mesmo, ou em subscrições diferentes, de Olá.


### <a name="set-up-an-azure-storage-account"></a>Configurar uma conta de armazenamento do Azure

- Precisa de um conta de armazenamento do Azure toohold dados replicados tooAzure padrão/premium. [Armazenamento premium](../storage/storage-premium-storage.md) é normalmente utilizado para máquinas virtuais que necessitam de um forma consistente de elevado desempenho de e/s e baixa latência toohost e/s intensivas cargas de trabalho.
- Se quiser toouse um toostore de conta de premium dados replicados, terá também de um armazenamento standard conta toostore os registos de replicação que captura em curso alterações dados tooon local.
- Consoante o modelo de recursos de Olá pretende toouse para efetuar a ativação pós-falha de VMs do Azure, configure uma conta no [modo Resource Manager](../storage/storage-create-storage-account.md), ou [modo clássico](../storage/storage-create-storage-account-classic-portal.md).
- Recomendamos que configure uma conta de armazenamento antes de começar. Se não o fizer necessário toodo-lo durante a implementação da recuperação de Site. contas de Olá tem de constar Olá mesma região que Olá do cofre dos serviços de recuperação.
- Não é possível mover a contas de armazenamento utilizado pela recuperação de sites através de grupos de recursos dentro de Olá mesmo subscrição, ou em subscrições diferentes.


### <a name="prepare-hello-hyper-v-hosts"></a>Preparar os anfitriões de Hyper-V Olá

* Certifique-se de que os anfitriões de Hyper-V de Olá cumprem Olá [pré-requisitos](site-recovery-prereq.md#disaster-recovery-of-hyper-v-virtual-machines-to-azure-no-virtual-machine-manager).
- Certifique-se de que os anfitriões de Olá podem aceder ao Olá necessário URLs.


## <a name="create-a-recovery-services-vault"></a>Criar um cofre dos Serviços de Recuperação 
1. Inicie sessão no toohello [portal do Azure](https://portal.azure.com).
2. Clique em **Novo** > **Monitorização + Gestão** > **Backup e Site Recovery (OMS)**.  

    ![Novo cofre](./media/site-recovery-hyper-v-site-to-azure/new-vault.png)

3. No **nome**, especifique um cofre de Olá tooidentify nome amigável. Se tiver mais do que uma subscrição, selecione uma delas.

4. [Criar um novo grupo de recursos](../azure-resource-manager/resource-group-template-deploy-portal.md) ou selecione um existente e especificar uma região do Azure. As máquinas serão replicadas toothis região. regiões toocheck suportada, veja disponibilidade geográfica em [detalhes de preços do Azure Site Recovery](https://azure.microsoft.com/pricing/details/site-recovery/).

5. Se quiser tooquickly acesso Olá cofre a partir de Olá Dashboard, clique em **Pin toodashboard**e, em seguida, clique em **criar**.

    ![Novo cofre](./media/site-recovery-hyper-v-site-to-azure/new-vault-settings.png)

novo cofre de Olá aparece no Olá **Dashboard** > **todos os recursos** lista e, em Olá principal **cofres dos serviços de recuperação** painel.



## <a name="select-hello-protection-goal"></a>Selecione o objetivo de proteção de Olá

Selecione o que pretende tooreplicate, e onde pretende tooreplicate para.

1. No Olá **cofres dos serviços de recuperação**, selecione o Cofre de Olá.
2. Em **Introdução**, clique em **Site Recovery** > **Preparar a Infraestrutura** > **Objetivo de proteção**.

    ![Selecione os objetivos](./media/site-recovery-hyper-v-site-to-azure/choose-goals.png)
3. No **objetivo de proteção**, selecione **tooAzure**e selecione **Sim, com o Hyper-V**. Selecione **não** tooconfirm não estiver a utilizar o VMM. Em seguida, clique em **OK**.

    ![Selecione os objetivos](./media/site-recovery-hyper-v-site-to-azure/choose-goals2.png)

## <a name="set-up-hello-source-environment"></a>Configurar o ambiente de origem Olá

Configurar sites de Olá Hyper-V, instale Olá fornecedor do Azure Site Recovery e agente dos serviços de recuperação do Azure de Olá nos anfitriões de Hyper-V e registar o site Olá no Cofre de Olá.

1. No **preparar infraestrutura**, clique em **origem**. tooadd um novo site de Hyper-V como um contentor para os anfitriões Hyper-V ou clusters, clique em **+ Site Hyper-V**.

    ![Configurar a origem](./media/site-recovery-hyper-v-site-to-azure/set-source1.png)
2. No **site Hyper-V criar**, especifique um nome para o site de Olá. Em seguida, clique em **OK**. Agora, selecione o site de Olá criou e clique em **+ servidor Hyper-V** tooadd um site de toohello do servidor.

    ![Configurar a origem](./media/site-recovery-hyper-v-site-to-azure/set-source2.png)

3. No **Adicionar servidor** > **tipo de servidor**, verifique se **servidor Hyper-V** é apresentado.

    - Certifique-se de que o servidor Olá Hyper-V que pretende tooadd está em conformidade com Olá [pré-requisitos](#on-premises-prerequisites), e é capazes de tooaccess Olá URLs especificados.
    - Transfira o ficheiro de instalação do fornecedor do Azure Site Recovery Olá. Execute este Olá tooinstall de ficheiro fornecedor e Olá agente dos serviços de recuperação em cada anfitrião de Hyper-V.

    ![Configurar a origem](./media/site-recovery-hyper-v-site-to-azure/set-source3.png)


## <a name="install-hello-provider-and-agent"></a>Instalar Olá fornecedor e agente

1. Execute o ficheiro de configuração do fornecedor de Olá em cada anfitrião adicionado site toohello Hyper-V. Se estiver a instalar num cluster de Hyper-V, execute a configuração em cada nó de cluster. Instalar e registar cada nó de cluster do Hyper-V assegura que as VMs estão protegidas, mesmo que o se migrar entre nós.
2. Em **Microsoft Update**, pode optar pelas atualizações de modo a que as atualizações do Provider sejam instaladas de acordo com a sua política do Microsoft Update.
3. No **instalação**, aceite ou modifique a localização de instalação do fornecedor do Olá predefinida e clique em **instalar**.
4. No **as definições do cofre**, clique em **procurar** tooselect Olá cofre ficheiro de chave que transferiu. Especifique a subscrição do Azure Site Recovery Olá, nome do cofre Olá, e Olá Hyper-V site toowhich Olá Hyper-V servidor pertence.

    ![Registo do servidor](./media/site-recovery-hyper-v-site-to-azure/provider3.png)

5. No **as definições de Proxy**, especifique como o fornecedor em execução em anfitriões Hyper-V se liga tooAzure recuperação de sites através de Olá Olá internet.

    * Se quiser Olá fornecedor tooconnect diretamente selecione **se ligue diretamente tooAzure recuperação de sites sem um proxy**.
    * Se o seu proxy existente requer autenticação ou pretende toouse um proxy personalizado para ligação de fornecedor Olá, selecione **ligar tooAzure recuperação do Site utilizando um servidor proxy**.
    * Se utilizar um proxy:
        - Especifique o endereço de Olá, porta e credenciais
        - Certifique-se de que Olá URLs descritos em Olá [pré-requisitos](#prerequisites) são permitidos através do proxy de Olá.

    ![Internet](./media/site-recovery-hyper-v-site-to-azure/provider7.PNG)

6. Após a conclusão da instalação, clique em **registar** tooregister servidor Olá cofre Olá.

    ![Localização de instalação](./media/site-recovery-hyper-v-site-to-azure/provider2.png)

7. Após a conclusão de registo, os metadados do servidor de Olá Hyper-V são obtidos pelo Azure Site Recovery e Olá servidor é apresentado na **infraestrutura de recuperação de Site** > **anfitriões Hyper-V**.


## <a name="set-up-hello-target-environment"></a>Configurar o ambiente de destino Olá

Especifique a conta de armazenamento do Azure Olá para replicação e Olá toowhich de rede do Azure VMs do Azure irá ligar após a ativação pós-falha.

1. Clique em **preparar a infraestrutura** > **destino**.
2. Selecione a subscrição de Olá e grupo de recursos de Olá em que pretende toocreate Olá VMs do Azure após a ativação pós-falha. Escolha a implementação de Olá modelo que pretende que toouse no Azure (clássica ou recurso management) para Olá VMs.

3. A Recuperação de Sites verifica que tem uma ou mais contas de armazenamento e redes do Azure compatíveis.

    - Se não tiver uma conta de armazenamento, clique em **+ armazenamento** toocreate inline uma conta baseada no Resource Manager. Leia sobre [os requisitos de armazenamento](site-recovery-prereq.md#azure-requirements).
    - Se não tiver uma rede do Azure, clique em **+ rede** toocreate inline uma rede baseada no Resource Manager.

    ![Armazenamento](./media/site-recovery-vmware-to-azure/enable-rep3.png)




## <a name="configure-replication-settings"></a>Configurar as definições de replicação

1. toocreate uma nova política de replicação, clique em **preparar a infraestrutura** > **as definições de replicação** > **+ criar e associar**.

    ![Rede](./media/site-recovery-hyper-v-site-to-azure/gs-replication.png)
2. Em **Criar e associar política**, especifique um nome de política.
3. No **copiar frequência**, especifique a frequência pretende que os tooreplicate delta dados após a replicação inicial de Olá (cada 30 segundos, 5 ou 15 minutos).

    > [!NOTE]
    > Uma frequência de segundo 30 não é suportada quando replicar toopremium armazenamento. limitação de Olá é determinada pelo número do Olá de instantâneos por blob (100) suportado pelo armazenamento premium. [Saiba mais](../storage/storage-premium-storage.md#snapshots-and-copy-blob).

4. No **retenção do ponto de recuperação**, especifique, em horas quanto tempo é de janela de retenção de Olá para cada ponto de recuperação. As VMs podem ser recuperados tooany ponto nessa janela.
5. No **frequência de instantâneos consistentes com aplicação**, especifique a frequência (1-12 horas) pontos de recuperação que contêm instantâneos consistentes com aplicações são criados.

    - Hyper-V utiliza dois tipos de instantâneos – um instantâneo padrão que fornece um instantâneo incremental de toda a máquina virtual Olá e um instantâneo consistente com aplicações, que tira um instantâneo de ponto no tempo dos dados de aplicação Olá no interior da máquina virtual de Olá.
    - Instantâneos consistentes com aplicações utilizam tooensure do serviço de cópia de sombra de Volume (VSS) que aplicações estão num estado consistente quando se obtém o instantâneo de Olá.
    - Se ativar instantâneos consistentes com aplicações, afetará o desempenho de Olá das aplicações em execução em máquinas virtuais de origem. Certifique-se de que valor Olá definido é inferior ao número de Olá de pontos de recuperação adicionais que configura.

6. No **hora de início da replicação inicial**, especifique quando toostart Olá a replicação inicial. replicação de Olá ocorre através da sua largura de banda de internet, pelo que poderá ser útil tooschedule-lo fora do horário de trabalho. Em seguida, clique em **OK**.

    ![Política de replicação](./media/site-recovery-hyper-v-site-to-azure/gs-replication2.png)

Quando cria uma nova política,-la automaticamente associado ao site de Hyper-V Olá. Pode associar um site Hyper-V (e Olá VMs na mesma) várias políticas de replicação no **replicação** > nome da política > **associar o Site de Hyper-V**.

## <a name="capacity-planning"></a>Planeamento de capacidade

Agora que configurou a sua infraestrutura básica, configurar, pode pensar sobre o planeamento de capacidade e descobrir a necessidade de recursos adicionais.

Recuperação de sites fornece um toohelp Planeador de capacidade alocar recursos corretos Olá para computação, redes e armazenamento. Pode executar planner Olá no modo rápido para estimativas com base num número médio de VMs, discos e armazenamento, ou no modo de detalhado com números personalizados ao nível da carga de trabalho de Olá. Antes de começar, tem de:

* Recolher informações sobre o ambiente de replicação, incluindo VMs, discos por VMs e armazenamento por disco.
* Calcular a taxa alteração (renovação) diária Olá para os seus dados replicados. Pode utilizar Olá [Planeador de capacidade para réplica do Hyper-V](https://www.microsoft.com/download/details.aspx?id=39057) toohelp fazê-lo.

1. Clique em **transferir** toodownload Olá ferramenta e, em seguida, executá-la. [Artigo de Olá leitura](site-recovery-capacity-planner.md) que acompanha a ferramenta de Olá.
2. Quando estiver pronto, selecione **Sim** no **executou Olá Capacity Planner**?

   ![Planeamento de capacidade](./media/site-recovery-hyper-v-site-to-azure/gs-capacity-planning.png)

Saiba mais sobre como [controlar a largura de banda de rede](#network-bandwidth-considerations)



## <a name="enable-replication"></a>Ativar a replicação

Antes de começar, certifique-se de que a conta de utilizador do Azure tem Olá necessário [permissões](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) tooenable replicação de um novo tooAzure de máquina virtual.

Ative a replicação para as VMs da seguinte forma:          

1. Clique em **replicar aplicação** > **origem**. Depois de que configurou a replicação para Olá pela primeira vez, pode clicar **+ replicar** tooenable replicação para máquinas adicionais.

    ![Ativar a replicação](./media/site-recovery-hyper-v-site-to-azure/enable-replication.png)
2. No **origem**, selecione o site de Olá Hyper-V. Em seguida, clique em **OK**.
3. No **destino**, selecione a subscrição do Cofre de Olá e Olá pretende toouse no Azure (clássica ou recurso management) após a ativação pós-falha de modelo de ativação pós-falha.
4. Selecione a conta de armazenamento de Olá que pretende toouse. Se não tiver uma conta que pretende toouse, pode [criar um](#set-up-an-azure-storage-account). Em seguida, clique em **OK**.
5. Selecione Olá Azure toowhich de rede e sub-rede VMs do Azure estabelecerão ligação quando são criados a ativação pós-falha.

    - Selecione tooapply Olá rede definições tooall máquinas ativar para a replicação, **configurar agora para as máquinas selecionadas**.
    - Selecione **configurar mais tarde** tooselect Olá rede do Azure por máquina.
    - Se não tiver uma rede que pretende toouse, pode [criar um](#set-up-an-azure-network). Selecione uma sub-rede, se aplicável. Em seguida, clique em **OK**.

   ![Ativar a replicação](./media/site-recovery-hyper-v-site-to-azure/enable-replication11.png)

6. No **máquinas virtuais** > **selecionar máquinas virtuais**, clique e selecione cada máquina que quiser tooreplicate. Só pode selecionar máquinas para as quais a replicação pode ser ativada. Em seguida, clique em **OK**.

    ![Ativar a replicação](./media/site-recovery-hyper-v-site-to-azure/enable-replication5-for-exclude-disk.png)

7. No **propriedades** > **configurar propriedades**, selecione o sistema de operativo Olá para VMs Olá selecionado e Olá disco do SO.
8. Certifique-se de que nome de VM do Azure de Olá (nome de destino) está em conformidade com [requisitos de máquina virtual do Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).
9. Por predefinição, todos os discos Olá Olá VM são selecionados para a replicação, mas pode desmarcar discos tooexclude-los.
    - Pode querer tooexclude discos tooreduce replicação da largura de banda. Por exemplo, não poderá tooreplicate discos com dados temporários ou dados que foi atualizada sempre que um computador ou aplicações é reiniciado (como pagefile.sys ou tempdb do Microsoft SQL Server). Pode excluir disco Olá da replicação, disco de Olá unselecting.
    - Só os discos básicos podem ser excluídos. Não pode excluir discos de SO.
    - Recomendamos que não exclua discos dinâmicos. O Site Recovery não consegue identificar se um disco rígido virtual dentro de uma VM de convidado é básico ou dinâmico. Se todos os discos de volume dinâmico dependentes não são excluídos, Olá de disco dinâmico protegido irá mostrar como um disco com falha quando hello VM falha e a dados Olá esse disco não estar acessíveis.
        - Após a replicação estar ativada, não pode adicionar ou remover discos para replicação. Se pretender tooadd ou excluir um disco, tem de proteção toodisable para Olá VM e, em seguida, volte a ativá-la.
        - Não é possível fazer a reativação pós-falha nos discos que forem criados manualmente no Azure. Por exemplo, se falhar mais três discos e criar dois diretamente na VM do Azure, apenas Olá três discos que foram a ativação pós-falha serão efetuados a reativação a partir do Azure tooHyper-V. Não é possível incluir discos criados manualmente no reativação pós-falha, ou a replicação inversa do tooAzure de Hyper-V.
        - Se excluir um disco que tem necessários para uma aplicação toooperate, após a ativação pós-falha tooAzure terá toocreate manualmente no Azure, por isso que Olá replicados aplicação pode ser executado. Em alternativa, pode integrar da automatização do Azure um plano de recuperação, o disco de Olá toocreate durante a ativação pós-falha da máquina de Olá.

10. Clique em **OK** toosave alterações. Pode definir as propriedades adicionais mais tarde.

    ![Ativar a replicação](./media/site-recovery-hyper-v-site-to-azure/enable-replication6-with-exclude-disk.png)

11. No **as definições de replicação** > **configurar as definições de replicação**, selecione a política de replicação de Olá pretende tooapply para Olá protegidas VMs. Em seguida, clique em **OK**. Pode modificar a política de replicação de Olá em **políticas de replicação** > nome da política > **editar definições de**. As alterações que aplicar serão utilizadas para as máquinas que já estão a replicar e para as novas máquinas.


   ![Ativar a replicação](./media/site-recovery-hyper-v-site-to-azure/enable-replication7.png)

Pode controlar o progresso de Olá **ativar proteção** da tarefa no **tarefas** > **as tarefas de recuperação de Site**. Depois de Olá **finalizar proteção** tarefa executa máquina Olá está preparada para ativação pós-falha.

### <a name="view-and-manage-vm-properties"></a>Ver e gerir propriedades da VM

Recomendamos que verifique as propriedades de Olá Olá da máquina de origem.

1. No **itens protegidos**, clique em **itens replicados**e selecione Olá máquina.

    ![Ativar a replicação](./media/site-recovery-hyper-v-site-to-azure/test-failover1.png)
2. No **propriedades**, pode ver a replicação e informações de ativação pós-falha para Olá VM.

    ![Ativar a replicação](./media/site-recovery-hyper-v-site-to-azure/test-failover2.png)
3. No **computação e rede** > **propriedades de computação**, pode especificar o tamanho de nome e o destino da VM do Azure Olá. Modificar Olá nome toocomply com requisitos do Azure se for necessário. Também pode ver e modificar as informações sobre a rede de destino Olá, uma sub-rede e endereço IP que será atribuído toohello VM do Azure. Tenha em atenção o seguinte Olá:

   * Pode definir o endereço IP de destino Olá. Se não fornecer um endereço, Olá máquina a ativação pós-falha utilizará o DHCP. Se definir um endereço que não está disponível na ativação pós-falha, a ativação pós-falha de Olá irá falhar. Olá mesmo endereço IP de destino pode ser utilizado para ativação pós-falha de teste se o endereço de Olá está disponível na rede de ativação pós-falha de teste de Olá.
   * número de Olá dos adaptadores de rede é ditado pelo tamanho Olá que especificar para a máquina de virtual de destino Olá, da seguinte forma:

     * Se o número de Olá de adaptadores de rede na máquina de origem Olá é menor ou igual toohello número de adaptadores de permitido para o tamanho da máquina de destino Olá, em seguida, terá de destino Olá Olá o mesmo número de adaptadores que origem Olá.
     * Se o número de Olá de adaptadores Olá máquina virtual de origem excede o número de Olá permitido para o tamanho de destino Olá, o tamanho máximo de destino Olá será utilizado.
     * Por exemplo, se uma máquina de origem tiver dois adaptadores de rede e tamanho da máquina Olá destino suporta quatro, a máquina de destino Olá terá dois adaptadores. Se Olá máquina de origem tiver dois adaptadores, mas hello tamanho de destino só suporta um computador de destino Olá terá apenas um adaptador.     
     * Se Olá VM tem vários adaptadores de rede, todos serão ligados toohello mesma rede.
     * Se a máquina virtual de Olá tem vários adaptadores de rede, em seguida, Olá primeiro mostrado na lista de Olá torna-se Olá *predefinido* adaptador de rede no Olá máquina virtual do Azure.

     ![Ativar a replicação](./media/site-recovery-hyper-v-site-to-azure/test-failover4.png)

4. No **discos**, pode ver o sistema de operativo Olá e discos de dados no Olá VM que será replicada.

#### <a name="managed-disks"></a>Managed disks

No **computação e rede** > **propriedades de computação**, pode definir "utilização gerido por discos" definição demasiado "Sim" para Olá VM se pretender que tooattach discos geridos tooyour máquina no tooAzure de migração. Discos geridos simplifica a gestão de discos para VMs IaaS do Azure ao gerir contas do storage Olá associadas aos discos VM Olá. [Saiba mais sobre os discos geridos](https://docs.microsoft.com/en-us/azure/storage/storage-managed-disks-overview).

   - Discos geridos são criados e ligados toohello máquina de virtual apenas em tooAzure uma ativação pós-falha. Ativar a proteção, dados de máquinas no local irão continuar tooreplicate toostorage contas.
   Discos geridos podem ser criados apenas para máquinas virtuais implementadas com o modelo de implementação do Olá Resource manager.

  > [!NOTE]
  > Reativação pós-falha a partir do ambiente de Hyper-V local tooon do Azure não é atualmente suportada em máquinas com discos geridos. Defina "utilização gerido por discos" demasiado "Sim" apenas se tenciona toomigrate tooAzure nesta máquina.

   - Quando definir "utilização gerido por discos" demasiado "Sim", apenas conjuntos de disponibilidade no grupo de recursos de Olá com "utilização gerido por discos" definido demasiado "Sim" seria disponíveis para seleção. Isto acontece porque as máquinas virtuais com discos geridos podem apenas ser parte de conjuntos de disponibilidade com o conjunto de propriedade de "Utilize gerido discos" demasiado "Sim". Certifique-se que crie conjuntos de disponibilidade com o conjunto de propriedade de "Utilize gerido discos" com base nos seus discos toouse intenção gerido na ativação pós-falha. Da mesma forma, quando definir "utilização gerido por discos" demasiado "não", apenas conjuntos de disponibilidade no grupo de recursos de Olá com a propriedade "utilização gerido por discos" definida demasiado "não" seria disponíveis para seleção. [Saiba mais sobre os discos geridos e os conjuntos de disponibilidade](https://docs.microsoft.com/en-us/azure/virtual-machines/windows/manage-availability#use-managed-disks-for-vms-in-an-availability-set).

  > [!NOTE]
  > Se a conta de armazenamento de Olá utilizada para a replicação foi encriptada com encriptação do serviço de armazenamento em qualquer ponto no tempo, a criação de discos geridos durante a ativação pós-falha irá falhar. Pode definir "utilização gerido por discos" demasiado "não" e repita a ativação pós-falha ou desative a proteção para a máquina virtual de Olá e protegê-lo tooa conta de armazenamento que não tinha ativada em qualquer ponto no tempo de encriptação do serviço de armazenamento.
  > [Saiba mais sobre a Encriptação do Serviço de Armazenamento e os discos geridos](https://docs.microsoft.com/en-us/azure/storage/storage-managed-disks-overview#managed-disks-and-encryption).


## <a name="test-hello-deployment"></a>Testar a implementação de Olá

implementação de Olá tootest pode executar uma ativação pós-falha de teste para uma única máquina virtual ou um plano de recuperação que contém uma ou mais máquinas virtuais.

### <a name="before-you-start"></a>Antes de começar

 - Se quiser tooconnect tooAzure VMs com RDP após a ativação pós-falha, saiba mais sobre [preparar tooconnect](site-recovery-test-failover-to-azure.md#prepare-to-connect-to-azure-vms-after-failover).
 - teste de toofully necessita toocopy do Active Directory e DNS no seu ambiente de teste. [Saiba mais](site-recovery-active-directory.md#test-failover-considerations).

### <a name="run-a-test-failover"></a>Executar uma ativação pós-falha de teste

1. toofail através de uma única máquina no **itens replicados**, clique em Olá VM > **+ ativação pós-falha de teste** ícone.
2. Planear toofail através de uma recuperação, na **planos de recuperação**, plano do contexto Olá > **ativação pós-falha de teste**. toocreate um plano de recuperação, [siga estas instruções](site-recovery-create-recovery-plans.md).
3. No **ativação pós-falha de teste**, selecione Olá rede Azure toowhich VMs do Azure será ligada após a ocorrência da ativação pós-falha.
4. Clique em **OK** toobegin ativação pós-falha de Olá. Pode controlar o progresso clicando na Olá VM tooopen as respetivas propriedades ou na Olá **ativação pós-falha de teste** tarefa no nome do cofre > **tarefas** > **as tarefas de recuperação de Site**.
5. Após a conclusão da ativação pós-falha de Olá, também deve ser capaz de réplica de Olá toosee máquina do Azure são apresentados no Olá portal do Azure > **máquinas virtuais**. Deve Certifique-se de que Olá VM é Olá um tamanho adequado, que tenha ligado toohello adequada de rede, e que está em execução.
6. Se preparou para as ligações após a ativação pós-falha, deve ser capaz de tooconnect toohello VM do Azure.
7. Quando tiver terminado, clique em **ativação pós-falha de teste de limpeza** no plano de recuperação Olá. No **notas** registar e guardar todas as observações associadas à ativação pós-falha de teste de Olá. Este procedimento eliminará Olá as máquinas virtuais que foram criadas durante a ativação pós-falha de teste.

Para obter mais detalhes, leia o artigo Olá [tooAzure de ativação pós-falha de teste](site-recovery-test-failover-to-azure.md) artigo.



## <a name="monitor-hello-deployment"></a>Implementação de Olá do monitor

As definições de configuração do monitor Olá, o estado e o estado de funcionamento para a implementação da recuperação de sites:

1. Clique em Olá do Olá cofre nome tooaccess **Essentials** dashboard. Neste dashboard pode controlar as tarefas de recuperação de Site, estado de replicação, planos de recuperação, estado de funcionamento do servidor e eventos.  

    ![Essentials](./media/site-recovery-hyper-v-site-to-azure/essentials.png)
2. No Olá **estado de funcionamento** mosaico, pode monitorizar os servidores de site que estão a ter o problema e Olá eventos gerados pela recuperação de Site no Olá últimas 24 horas. Pode personalizar os mosaicos do Essentials tooshow Olá e modelos que são mais úteis tooyou, incluindo o estado de Olá de outra recuperação de sites e cofres de cópia de segurança.
3. Pode gerir e monitorizar a replicação nos Olá **itens replicados**, **planos de recuperação**, e **tarefas de recuperação de Site** mosaicos. Pode explorar tarefas para obter mais detalhes no **tarefas** > **tarefas de recuperação de Site**.

## <a name="command-line-provider-and-agent-installation"></a>Instalação da linha de comandos de fornecedor e agente

Olá fornecedor do Azure Site Recovery e agente também podem ser instalados utilizando Olá seguinte linha de comandos. Este método pode ser utilizado tooinstall fornecedor Olá um Server Core do Windows Server 2012 R2.

1. Transferir Olá fornecedor e o registo do ficheiro de chave tooa pasta de instalação. Por exemplo: C:\ASR.
2. A partir da linha de comandos elevada, execute o installer do fornecedor tooextract Olá estes comandos:

            C:\Windows\System32> CD C:\ASR
            C:\ASR> AzureSiteRecoveryProvider.exe /x:. /q
3. Execute este comando tooinstall componentes Olá:

            C:\ASR> setupdr.exe /i
4. Em seguida, execute o servidor de Olá estes comandos tooregister no Cofre de Olá:

            CD C:\Program Files\Microsoft Azure Site Recovery Provider\
            C:\Program Files\Microsoft Azure Site Recovery Provider\> DRConfigurator.exe /r  /Friendlyname <friendly name of hello server> /Credentials <path of hello credentials file>

<br/>
Em que:

* **/Credentials**: o parâmetro obrigatório que especifica a localização de Olá no qual Olá se encontra o ficheiro de chave de registo  
* **/ FriendlyName**: o parâmetro obrigatório para o nome de Olá Olá Hyper-V do servidor de anfitrião que é apresentado no portal do Azure Site Recovery Olá.
* **/proxyAddress**: o parâmetro opcional que especifica o endereço de hello do servidor de proxy de Olá.
* **/proxyaddress** : o parâmetro opcional que especifica a porta de hello do servidor de proxy de Olá.
* **/proxyUsername**: o parâmetro opcional que especifica o nome de utilizador de Proxy Olá (caso o proxy precise de autenticação).
* **/proxyPassword**: o parâmetro opcional que especifica Olá palavra-passe para autenticar com o servidor de proxy de Olá (se o proxy precise de autenticação).


## <a name="network-bandwidth-considerations"></a>Considerações sobre a largura de banda de rede
Pode utilizar Olá [ferramenta do Hyper-V capacity planner](site-recovery-capacity-planner.md) largura de banda do Olá toocalculate que precisa para a replicação (replicação inicial e, em seguida, delta). quantidade de Olá toocontrol de utilização de largura de banda para a replicação tem algumas opções:

* **Limitar largura de banda**: tráfego do Hyper-V que replica tooAzure passa através de um anfitrião Hyper-V específico. Pode limitar a largura de banda no servidor de anfitrião Olá.
* **Otimizar a largura de banda**: pode influenciar a largura de banda Olá utilizada na replicação através de um par de chaves de registo.

### <a name="throttle-bandwidth"></a>Limitar largura de banda
1. Abra Olá MMC da cópia de segurança do Microsoft Azure snap-in no servidor de anfitrião do Hyper-V Olá. Por predefinição, um atalho para cópia de segurança do Microsoft Azure está disponível no ambiente de trabalho Olá ou em c:\Programas\Microsoft c:\Programas\Microsoft Azure Recovery Services agent\bin\wabadmin..
2. No snap-in Olá clique **alterar propriedades**.
3. No Olá **limitação** separador selecione **ativar a limitação para operações de cópia de segurança de utilização de largura de banda de internet**e definir limites de Olá para o trabalho e de descanso horas. Intervalos válidos são de Kbps 512 too102 Mbps, por segundo.

    ![Limitar largura de banda](./media/site-recovery-hyper-v-site-to-azure/throttle2.png)

Também pode utilizar Olá [Set-OBMachineSetting](https://technet.microsoft.com/library/hh770409.aspx) cmdlet tooset limitação. Exemplo:

    $mon = [System.DayOfWeek]::Monday
    $tue = [System.DayOfWeek]::Tuesday
    Set-OBMachineSetting -WorkDay $mon, $tue -StartWorkHour "9:00:00" -EndWorkHour "18:00:00" -WorkHourBandwidth  (512*1024) -NonWorkHourBandwidth (2048*1024)

**Set-OBMachineSetting -NoThrottle** indica que não é necessária nenhuma limitação.

### <a name="influence-network-bandwidth"></a>Influência da largura de banda de rede
1. No registo de Olá navegue demasiado**HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Replication**.
   * tráfego de largura de banda de Olá tooinfluence num disco replicação, modificar Olá de valor de Olá **UploadThreadsPerVM**, ou crie a chave de Olá, se não existir.
   * largura de banda do tooinfluence Olá para tráfego de reativação pós-falha a partir do Azure, modifique o valor de Olá **DownloadThreadsPerVM**.
2. valor predefinido de Olá é 4. Numa rede "sobreaprovisionada", estas chaves do registo devem ser Olá valores predefinidos alteradas. Olá máximo é 32. Monitorizar o valor de Olá toooptimize de tráfego.

## <a name="next-steps"></a>Passos seguintes

Depois da replicação inicial está concluída e ter testado implementação Olá, pode invocar as ativações pós-falha conforme for necessário Olá. [Saiba mais](site-recovery-failover.md) sobre os diferentes tipos de ativações pós-falha e como toorun-los.
