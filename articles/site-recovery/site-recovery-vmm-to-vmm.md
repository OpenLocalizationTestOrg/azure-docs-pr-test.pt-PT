---
title: "site secundário do aaaReplicate VMs de Hyper-V tooa com o Azure Site Recovery | Microsoft Docs"
description: "Descreve como tooreplicate VMs de Hyper-V no VMM nuvens tooa secundário VMM site utilizar Olá portal do Azure."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: b33a1922-aed6-4916-9209-0e257620fded
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: raynew
ms.openlocfilehash: e79dbdeab74266e843e5146298dc5aadfe66b5df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-virtual-machines-in-vmm-clouds-tooa-secondary-vmm-site-using-hello-azure-portal"></a>Replicar máquinas virtuais de Hyper-V no VMM nuvens tooa site VMM secundário com Olá portal do Azure
> [!div class="op_single_selector"]
> * [Portal do Azure](site-recovery-vmm-to-vmm.md)
> * [Portal clássico](site-recovery-vmm-to-vmm-classic.md)
> * [PowerShell – Resource Manager](site-recovery-vmm-to-vmm-powershell-resource-manager.md)
>
>

Este artigo descreve como tooreplicate no local máquinas de virtuais de Hyper-V geridas em nuvens do System Center Virtual Machine Manager (VMM), utilizando o site secundário tooa [do Azure Site Recovery](site-recovery-overview.md) no Olá portal do Azure. Saiba mais sobre esta [arquitetura do cenário](site-recovery-components.md).

Depois de ler este artigo, publique quaisquer comentários na parte inferior do hello, ou no Olá [fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="prerequisites"></a>Pré-requisitos

**Pré-requisito** | **Detalhes**
--- | ---
**Azure** | Necessita de uma conta do [Microsoft Azure](http://azure.microsoft.com/). Pode começar com uma [avaliação gratuita](https://azure.microsoft.com/pricing/free-trial/). [Saiba mais](https://azure.microsoft.com/pricing/details/site-recovery/) sobre os preços da Recuperação de Sites.
**VMM no local** | Recomendamos que tiver dois servidores do VMM, um no site primário Olá e um em Olá secundário.<br/><br/> Pode replicar entre nuvens num único servidor VMM.<br/><br/> Servidores do VMM devem estar em execução, pelo menos, System Center 2012 SP1 com as atualizações mais recentes do Olá.<br/><br/> Servidores do VMM tem acesso à internet.
**Nuvens do VMM** | Cada servidor VMM tem de ter numa ou mais nuvens e todas as nuvens têm de ter conjunto de perfis de capacidade Hyper-V Olá. <br/><br/>Nuvens tem de conter um ou mais grupos de anfitriões do VMM.<br/><br/> Se tiver apenas um servidor do VMM, é necessário, pelo menos, dois nuvens, tooact como principal e secundário.
**Hyper-V** | Servidores Hyper-V tem de estar em execução, pelo menos, Windows Server 2012 com a função de Olá Hyper-V, e ter Olá atualizações mais recentes instaladas.<br/><br/> Um servidor Hyper-V deve conter uma ou mais VMs.<br/><br/>  Servidores de anfitrião Hyper-V devem estar localizados em grupos de anfitriões em nuvens do VMM primárias e secundárias Olá.<br/><br/> Se executar o Hyper-V num cluster no Windows Server 2012 R2, instale [atualizar 2961977](https://support.microsoft.com/kb/2961977)<br/><br/> Se executar o Hyper-V num cluster no Windows Server 2012, Mediador de clusters não é criado automaticamente se tiver um cluster de baseadas no endereço IP estático. Configure o Mediador de clusters de Olá manualmente. [Leia mais](http://social.technet.microsoft.com/wiki/contents/articles/18792.configure-replica-broker-role-cluster-to-cluster-replication.aspx).<br/><br/> Servidores Hyper-V tem acesso à internet.
**URLs** | Servidores do VMM e anfitriões Hyper-V devem ser capaz de tooreach estes URLs:<br/><br/> [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]

## <a name="deployment-steps"></a>Passos da implementação

Eis o que fazer:

1. Verifique os pré-requisitos.
2. Prepare o servidor do VMM Olá e anfitriões Hyper-V.
3. Crie um cofre dos Serviços de Recuperação. cofre Olá contém definições de configuração e orquestra a replicação.
4. Especifique as definições de replicação, origem e destino.
5. Implementar o serviço de mobilidade Olá em VMs que pretende tooreplicate.
6. Preparar para a replicação e ativar a replicação para as VMs de Hyper-V.
7. Execute um toomake de ativação pós-falha de teste se que tudo está a funcionar conforme esperado.

## <a name="prepare-vmm-servers-and-hyper-v-hosts"></a>Preparar servidores VMM e anfitriões Hyper-V

tooprepare para a implementação:

1. Certifique-se de que o servidor do VMM Olá anfitriões Hyper-V está em conformidade com os pré-requisitos de Olá descritos acima e podem contactar os URLs de Olá necessário.
2. Configurar redes do VMM, para que possa configurar [mapeamento da rede](#network-mapping-overview).

    - Certifique-se de que as VMs no servidor de anfitrião do Hyper-V de origem de Olá são ligado tooa rede VM do VMM. Essa rede deve ser ligado tooa rede lógica que esteja associado Olá nuvem.
    Certifique-se de que a nuvem de secundária de Olá que utilizar para recuperação tem uma rede VM correspondente configurada. Essa rede VM deve ser ligado tooa rede lógica que está associada à nuvem secundário Olá.

3. Preparar para uma [única implementação de servidor](#single-vmm-server-deployment), se pretender tooreplicate VMs entre nuvens no Olá mesmo servidor VMM.

## <a name="create-a-recovery-services-vault"></a>Criar um cofre dos Serviços de Recuperação 
1. Inicie sessão no toohello [portal do Azure](https://portal.azure.com).
2. Clique em **Novo** > **Gestão** > **Serviços de Recuperação**.
3. No **nome**, especifique um cofre de Olá tooidentify nome amigável. Se tiver mais do que uma subscrição, selecione uma delas.
4. [Crie um grupo de recursos](../azure-resource-manager/resource-group-template-deploy-portal.md) ou selecione um existente. Selecione uma região do Azure. Máquinas são replicadas toothis região. regiões toocheck suportada veja disponibilidade geográfica em [detalhes de preços do Azure Site Recovery](https://azure.microsoft.com/pricing/details/site-recovery/)
5. Se quiser tooquickly acesso Olá cofre a partir de Olá Dashboard, clique em **Pin toodashboard** > **criar cofre**.

    ![Novo cofre](./media/site-recovery-vmm-to-vmm/new-vault-settings.png)

novo cofre de Olá aparece no Olá **Dashboard**, na **todos os recursos**e em Olá principal **cofres dos serviços de recuperação** painel.


## <a name="choose-a-protection-goal"></a>Escolha um objetivo de proteção

Selecione o que pretender tooreplicate e onde pretende tooreplicate para.

2. Clique em **recuperação de Site** > **passo 1: preparar a infraestrutura** > **objetivo de proteção**.
3. Selecione **toorecovery site**e selecione **Sim, com o Hyper-V**.
4. Selecione **Sim** tooindicate estiver a utilizar anfitriões do VMM toomanage Olá Hyper-V.
5. Selecione **Sim** se tiver um servidor secundário do VMM. Se estiver a implementar a replicação entre nuvens num único servidor VMM, clique em **não**. Em seguida, clique em **OK**.

    ![Selecione os objetivos](./media/site-recovery-vmm-to-vmm/choose-goals.png)

## <a name="set-up-hello-source-environment"></a>Configurar o ambiente de origem Olá

Instalar Olá fornecedor do Azure Site Recovery nos servidores do VMM, detetar e registar os servidores no Cofre de Olá.

1. Clique em **passo 1: preparar infraestrutura** > **origem**.

    ![Configurar a origem](./media/site-recovery-vmm-to-vmm/goals-source.png)
2. No **preparar a origem**, clique em **+ VMM** tooadd um servidor do VMM.

    ![Configurar a origem](./media/site-recovery-vmm-to-vmm/set-source1.png)
3. No **Adicionar servidor**, verifique se **servidor VMM do System Center** aparece no **tipo de servidor** e esse servidor do VMM Olá cumpre Olá [pré-requisitos](#prerequisites).
4. Transfira o ficheiro de instalação do fornecedor do Azure Site Recovery Olá.
5. Transfira a chave de registo de Olá. Precisará disto quando executar a configuração. chave de Olá é válido durante cinco dias depois de gerá-la.

    ![Configurar a origem](./media/site-recovery-vmm-to-vmm/set-source3.png)
6. Instale Olá fornecedor do Azure Site Recovery no servidor do VMM Olá. Não precisa de tooexplicitly instala nada nos servidores de anfitrião do Hyper-V.


### <a name="install-hello-azure-site-recovery-provider"></a>Instalar Olá Azure Site Recovery Provider

1. Execute o ficheiro de configuração do fornecedor de Olá em cada servidor VMM. Se o VMM for implementado num cluster, efetue Olá seguir Olá pela primeira vez que instala:
    -  Instale o fornecedor de Olá num nó ativo e concluir o servidor do Olá instalação tooregister Olá VMM no Cofre de Olá.
    - Em seguida, instale o Olá fornecedor no Olá outros nós. Os nós do cluster devem executar todos os Olá mesma versão do fornecedor de Olá.
2. A configuração executa algumas verificações de pré-requisitos e os pedidos de serviço do VMM permissão toostop Olá. Olá serviço VMM será reiniciado automaticamente após a conclusão do programa de configuração. Se instalar num VMM cluster, está a função de Cluster de Olá toostop pedido.
3. No **Microsoft Update**, pode optar toospecify que as atualizações do fornecedor são instaladas de acordo com a política do Microsoft Update.
4. No **instalação**, aceite ou modifique a localização de instalação predefinida de Olá e clique em **instalar**.

    ![Localização de instalação](./media/site-recovery-vmm-to-vmm/provider-location.png)
5. Depois de concluída a instalação, clique em **registar** tooregister servidor Olá cofre Olá.

    ![Localização de instalação](./media/site-recovery-vmm-to-vmm/provider-register.png)
6. No **nome do cofre**, verifique o nome de Olá do Cofre de Olá no qual Olá servidor será registado. Clique em *Seguinte*.

    ![Registo do servidor](./media/site-recovery-vmm-to-vmm-classic/vaultcred.PNG)
7. No **ligação à Internet**, especifique como o fornecedor de Olá em execução no servidor do VMM Olá se liga a tooAzure.

    ![Definições da Internet](./media/site-recovery-vmm-to-vmm-classic/proxydetails.PNG)

   - Pode especificar esse fornecedor Olá deve ligar diretamente toohello internet, ou através de um proxy.
   - Especifique as definições de proxy, se necessário.
   - Se utilizar um proxy, uma conta RunAs do VMM (DRAProxyAccount) é automaticamente criada utilizando Olá especificada credenciais de proxy. Configure o servidor de proxy de Olá, para que esta conta pode autenticar com êxito. Olá definições de conta RunAs podem ser modificadas na consola do VMM Olá > **definições** > **segurança** > **contas Run as**. Reinicie Olá VMM serviço tooupdate é alterada.
8. No **chave de registo**, selecione chave Olá que transferido a partir do Azure Site Recovery e copiou toohello o servidor do VMM.
9. definição de encriptação de Olá só é utilizada quando replicar VMs Hyper-V no tooAzure de nuvens do VMM. Se estiver a replicar tooa site secundário não é utilizado.
10. No **nome do servidor**, especifique o servidor de nome amigável tooidentify Olá VMM no Cofre de Olá. Numa configuração de cluster especifique o nome de função de cluster do Olá VMM.
11. No **sincronizar metadados da nuvem**, selecione se pretende toosynchronize metadados para todas as nuvens no servidor do VMM Olá Vault Olá. Esta ação só deverá toohappen uma vez em cada servidor. Se não quiser toosynchronize todas as nuvens, pode deixar esta definição desmarcada e sincronizar cada nuvem individualmente nas propriedades de nuvem de Olá na consola do VMM Olá.
12. Clique em **seguinte** processo de Olá toocomplete. Após o registo, os metadados hello do servidor do VMM são obtidos pelo Azure Site Recovery. servidor de Olá é apresentado no Olá **servidores VMM** separador Olá **servidores** página no Olá cofre.

    ![Servidor](./media/site-recovery-vmm-to-vmm-classic/provider13.PNG)
13. Depois do servidor de Olá está disponível na consola da recuperação de sites de Olá, no **origem** > **preparar a origem** selecionar servidor do VMM Olá e nuvem de Olá selecione em que Olá Hyper-V anfitrião se encontra. Em seguida, clique em **OK**.

Também pode instalar o fornecedor de Olá Olá linha de comandos:

[!INCLUDE [site-recovery-rw-provider-command-line](../../includes/site-recovery-rw-provider-command-line.md)]


## <a name="set-up-hello-target-environment"></a>Configurar o ambiente de destino Olá

Selecione o servidor do VMM de destino de Olá e nuvem.

1. Clique em **preparar a infraestrutura** > **destino**e o servidor VMM de destino selecione Olá pretende toouse.
2. Serão apresentadas nuvens no servidor de Olá que são sincronizadas com a recuperação de sites. Selecione a nuvem de destino Olá.

   ![destino](./media/site-recovery-vmm-to-vmm/target-vmm.png)

## <a name="set-up-replication-settings"></a>Configurar as definições de replicação

- Quando cria uma política de replicação, todos os anfitriões através da política de Olá tem de ter Olá mesmo sistema operativo. Olá nuvem VMM pode conter os anfitriões de Hyper-V versões diferentes do Windows Server em execução, mas neste caso, terá de várias políticas de replicação.
- Pode efetuar Olá a replicação inicial offline. [Saiba mais](#prepare-for-initial-offline-replication)

1. Clique em toocreate uma nova política de replicação **preparar a infraestrutura** > **as definições de replicação** > **+ criar e associar**.

    ![Rede](./media/site-recovery-vmm-to-vmm/gs-replication.png)
2. Em **Criar e associar política**, especifique um nome de política. Olá tipo de origem e de destino deve ser **Hyper-V**.
3. No **versão de anfitrião do Hyper-V**, selecione o sistema operativo que está em execução no anfitrião de Olá.
4. No **tipo de autenticação** e **porta de autenticação**, especifique a forma como o tráfego for autenticado entre Olá principal e servidores de anfitrião do Hyper-V de recuperação. Selecione **certificado** a menos que tenha um Kerberos ambiente de trabalho. O Azure Site Recovery irá configurar automaticamente certificados para autenticação HTTPS. Não precisa de toodo nada manualmente. Por predefinição, a porta 8083 e 8084 (para certificados) será aberta em Olá Firewall do Windows nos servidores de anfitrião do Hyper-V Olá. Se selecionar **Kerberos**, será utilizada uma permissão Kerberos para autenticação mútua de servidores de anfitrião Olá. Tenha em atenção que esta definição só é relevante para servidores de anfitrião de Hyper-V em execução no Windows Server 2012 R2.
5. No **copiar frequência**, especifique a frequência pretende que os tooreplicate delta dados após a replicação inicial de Olá (cada 30 segundos, 5 ou 15 minutos).
6. No **retenção do ponto de recuperação**, especifique, em horas, quanto janela de retenção de Olá irá ser para cada ponto de recuperação. Máquinas protegidas podem ser recuperados tooany ponto nessa janela.
7. No **frequência de instantâneos consistentes com aplicação**, especifique a frequência (1-12 horas) pontos de recuperação que contêm instantâneos consistentes com aplicações são criados. Hyper-V utiliza dois tipos de instantâneos – um instantâneo padrão que fornece um instantâneo incremental de toda a máquina virtual Olá e um instantâneo consistente com aplicações, que tira um instantâneo de ponto no tempo dos dados de aplicação Olá no interior da máquina virtual de Olá. Instantâneos consistentes com aplicações utilizam tooensure do serviço de cópia de sombra de Volume (VSS) que aplicações estão num estado consistente quando se obtém o instantâneo de Olá. Se ativar instantâneos consistentes com aplicações, afetará o desempenho de Olá das aplicações em execução em máquinas virtuais de origem. Certifique-se de que valor Olá definido é inferior ao número de Olá de pontos de recuperação adicionais que configura.
8. No **compressão de transferência de dados**, especifique se os dados replicados que são transferidos devem ser comprimidos.
9. Selecione **Eliminar réplica VM**, toospecify Olá máquina virtual de réplica deve ser eliminado se desativar a proteção Olá de VM de origem. Se ativar esta definição, quando desativar a proteção Olá de VM de origem ser removido da consola da recuperação de Site Olá, definições de recuperação de sites para Olá VMM são removidas da consola do VMM Olá e réplica Olá é eliminada.
10. No **inicial método de replicação**, se está a replicar rede Olá, especifique se toostart Olá a replicação inicial ou agendá-la. toosave a largura de banda de rede, poderá pretender tooschedule-lo fora do horário de trabalho. Em seguida, clique em **OK**.

     ![Política de replicação](./media/site-recovery-vmm-to-vmm/gs-replication2.png)
11. Quando cria uma nova política, automaticamente fica associada Olá nuvem VMM. No **política de replicação**, clique em **OK**. Pode associar nuvens do VMM (e Olá VMs nas mesmas) adicionais com esta política de replicação em **replicação** > nome da política > **associar nuvem do VMM**.

     ![Política de replicação](./media/site-recovery-vmm-to-vmm/policy-associate.png)


### <a name="configure-network-mapping"></a>Configurar o mapeamento da rede

- Saiba mais sobre [mapeamento da rede](#prepare-for-network-mapping) antes de começar.
- Certifique-se de que as máquinas virtuais nos servidores VMM estão ligados tooa rede VM.


1. No **infraestrutura de recuperação de Site** > **mapeamento da rede** > **mapeamentos da rede**, clique em **+ mapeamento da rede**.

    ![Mapeamento da rede](./media/site-recovery-vmm-to-azure/network-mapping1.png)
2. No **adicionar mapeamento da rede** separador, selecione a origem de Olá e servidores do VMM de destino. redes VM de Olá associadas a servidores de Olá do VMM são obtidos.
3. No **rede de origem**, selecione rede Olá pretende toouse na lista de redes VM associadas com o servidor VMM principal do Olá Olá.
4. No **rede de destino**, selecione rede Olá pretende toouse do servidor VMM Olá secundário. Em seguida, clique em **OK**.

    ![Mapeamento da rede](./media/site-recovery-vmm-to-vmm/network-mapping2.png)

Veja a seguir o que acontece quando começa o mapeamento da rede:

* Quaisquer máquinas de virtuais de réplica existente que correspondem a rede VM de origem toohello será toohello ligado a rede VM de destino.
* Novas máquinas virtuais que estão ligados toohello rede VM de origem serão ligados toohello destino mapeadas rede após a replicação.
* Se modificar um mapeamento existente com uma nova rede, as máquinas virtuais de réplica serão ligadas utilizando as novas definições Olá.
* Se a rede de destino Olá tem várias sub-redes e uma dessas sub-redes tem Olá mesmo nome de sub-rede na máquina virtual de origem que Olá está localizado, em seguida, Olá máquina virtual de réplica será ligada toothat sub-rede de destino após a ativação pós-falha. Se não existir nenhuma sub-rede de destino com um nome correspondente, Olá máquina de virtual será ligado toohello primeira sub-rede Olá rede.

### <a name="configure-storage-mapping"></a>Configure o mapeamento de armazenamento.

[Mapeamento de armazenamento](#prepare-for-storage-mapping) não é suportado no novo portal do Azure Olá. No entanto, pode ser ativado através do Powershell. [Saiba mais](site-recovery-vmm-to-vmm-powershell-resource-manager.md#step-7-configure-storage-mapping).

## <a name="step-5-capacity-planning"></a>Passo 5: Planeamento de capacidade

Agora que tem a infraestrutura básica configurada, considere o planeamento da capacidade e averigue se precisa de recursos adicionais.

- Transferir e executar Olá [Planeador de capacidade de recuperação de Site do Azure](site-recovery-capacity-planner.md), toogather informações sobre o ambiente de replicação, incluindo VMs, discos por VM e de armazenamento por disco.
- Depois de ter recolhidas informações de replicação em tempo real, pode modificar Olá NetQos política toocontrol replicação da largura de banda para as VMs. Leia mais sobre [limitação de tráfego de réplica do Hyper-V](http://www.thomasmaurer.ch/2013/12/throttling-hyper-v-replica-traffic/), no blogue de blogue Maurer. Obter mais informações sobre Olá [cmdlet New-NetQosPolicy](https://technet.microsoft.com/library/hh967468.aspx.).

## <a name="enable-replication"></a>Ativar a replicação

1. Clique em **Passo 2: Replicar aplicação** > **Origem**. Depois de ativar a replicação para Olá pela primeira vez, clique em **+ replicar** na replicação de tooenable Olá cofre para máquinas adicionais.

    ![Ativar a replicação](./media/site-recovery-vmm-to-vmm/enable-replication1.png)
2. No **origem**, selecione o servidor do VMM Olá e Olá nuvem em que Olá estão localizados os anfitriões de Hyper-V que pretende tooreplicate. Em seguida, clique em **OK**.

    ![Ativar a replicação](./media/site-recovery-vmm-to-vmm/enable-replication2.png)
3. No **destino**, certifique-se de que servidor VMM secundário Olá e na nuvem.
4. No **máquinas virtuais**, selecione de VMs de Olá pretende tooprotect da lista de Olá.

    ![Ativar a proteção da máquina virtual](./media/site-recovery-vmm-to-vmm/enable-replication5.png)

Pode controlar o progresso de Olá **ativar proteção** ação no **tarefas** > **as tarefas de recuperação de Site**. Depois de Olá **finalizar proteção** tarefa estiver concluída, Olá máquina está preparada para ativação pós-falha.

Tenha em atenção que:

- Também pode ativar a proteção para máquinas virtuais na consola do VMM Olá. Clique em **ativar proteção** na barra de ferramentas de Olá nas propriedades da máquina virtual de Olá > **do Azure Site Recovery** separador.
- Depois de ativar a replicação, pode ver as propriedades de Olá VM na **itens replicados**. No Olá **Essentials** dashboard, pode ver informações sobre a política de replicação de Olá para Olá VM e o respetivo estado. Clique em **propriedades** para obter mais detalhes.

### <a name="onboard-existing-virtual-machines"></a>Carregar máquinas virtuais existentes
Se tiver máquinas virtuais existentes no VMM que estiver a replicar com a réplica do Hyper-V, pode carregá-las para replicação de recuperação de sites do Azure da seguinte forma:

1. Certifique-se de que o servidor Olá Hyper-V que aloja Olá que VM existente está localizado na nuvem principal Olá e esse servidor de Hyper-V Olá Olá máquina virtual de réplica de alojamento está localizado na nuvem secundário Olá.
2. Certifique-se de que uma política de replicação está configurada para a nuvem VMM principal Olá.
3. Ative a replicação para a máquina virtual primária de Olá. Do Azure Site Recovery e o VMM Certifique-se de que hello mesmo anfitrião de réplica e a máquina virtual é detetada e irá reutilizar o Azure Site Recovery e restabelecer a replicação utilizando Olá especificadas as definições.

## <a name="test-your-deployment"></a>Testar a implementação

tootest a implementação, pode executar um [ativação pós-falha de teste](site-recovery-test-failover-vmm-to-vmm.md) para uma única máquina virtual, ou [criar um plano de recuperação](site-recovery-create-recovery-plans.md) que contém uma ou mais máquinas virtuais.



## <a name="prepare-for-offline-initial-replication"></a>Preparar a replicação inicial offline

Pode efetuar a replicação offline para cópia de dados inicial Olá. Pode preparar isto da seguinte forma:

* No servidor de origem Olá, especifique uma localização de caminho a partir do qual Olá será realizada a exportação de dados. Atribua o controlo total para as permissões de NTFS e partilha toohello serviço do VMM no caminho de exportação de Olá. No servidor de destino Olá, especifique uma localização de caminho de importação de dados de Olá partir do qual irá ocorrer. Atribua Olá mesmas permissões neste caminho de importação.
* Se hello importar ou exportar caminho for partilhado, atribuir a associação de grupo de administrador, utilizador avançado, operador de impressão ou o operador de servidor para a conta de serviço do VMM Olá no computador remoto Olá que Olá partilhado está localizada.
* Se estiver a utilizar quaisquer anfitriões de tooadd Run As contas, no Olá importar e exportar caminhos, atribua a leitura e permissões de escrita toohello contas Run as no VMM.
* Olá, importar e Exportar partilhas não deve estar localizada em qualquer computador utilizado como um servidor de anfitrião do Hyper-V, porque a configuração de loopback não é suportada pelo Hyper-V.
* No Active Directory, em cada servidor de anfitrião do Hyper-V que contém máquinas virtuais que pretende tooprotect, ativar e configurar a delegação restrita tootrust Olá computadores remotos em que a importação de Olá e exportação caminhos estão localizados, da seguinte forma:
  1. No controlador de domínio Olá, abra **computadores e utilizadores do Active Directory**.
  2. Na árvore da consola de Olá, clique em **DomainName** > **computadores**.
  3. O nome do servidor de anfitrião de Hyper-V de Olá contexto > **propriedades**.
  4. No Olá **delegação** separador, clique em **confiar no computador para os serviços de toospecified de delegação apenas**.
  5. Clique em **utilizar qualquer protocolo de autenticação**.
  6. Clique em **adicionar** > **utilizadores e computadores**.
  7. Nome do tipo Olá do computador de Olá que aloja o caminho de exportação de Olá > **OK**. Na lista de Olá de serviços disponíveis, mantenha premida a tecla CTRL de Olá e clique em **cifs** > **OK**. Repita para nome de Olá do computador de Olá nesse caminho de importação de Olá de anfitriões. Repita conforme necessário para servidores de anfitrião de Hyper-V adicionais.



## <a name="prepare-for-network-mapping"></a>Preparar o mapeamento da rede
Mapas de mapeamento de rede entre redes de VM do VMM no Olá primários e secundários servidores do VMM para:

* Ideal colocar as VMs da réplica em anfitriões de Hyper-V secundários após a ativação pós-falha.
* Ligar redes VM de tooappropriate de VMs de réplica após a ativação pós-falha.

Tenha em atenção que:
- Mapeamento da rede pode ser configurado entre as redes VM em dois servidores do VMM, ou num único servidor VMM se dois sites são geridos pelo Olá mesmo servidor.
- Quando o mapeamento está configurado corretamente e a replicação está ativada, uma VM na localização primária Olá será ligado tooa rede e a réplica de localização de destino Olá será ligada tooits mapear a rede.
- Se a redes tem sido corretamente configurado no VMM, quando seleciona uma rede VM de destino durante o mapeamento da rede, Olá origem as nuvens do VMM que utilizam a rede VM de origem Olá serão apresentadas juntamente com redes VM de destino disponíveis Olá em nuvens do destino de Olá que são utilizadas para proteção.
- Se a rede de destino Olá tem várias sub-redes e uma dessas sub-redes tem o mesmo nome como Olá sub-rede na qual Olá máquina virtual de origem está localizada, em seguida, Olá de Olá máquina virtual de réplica será ligada toothat sub-rede de destino após a ativação pós-falha. Se não existir nenhuma sub-rede de destino com um nome correspondente, Olá máquina de virtual será ligado toohello primeira sub-rede Olá rede.


Eis um exemplo tooillustrate este mecanismo. Vamos organização com duas localizações em Nova Iorque e Chicago.

| **Localização** | **Servidor VMM** | **Redes VM** | **Mapeado para** |
| --- | --- | --- | --- |
| Nova Iorque |O VMM NewYork |VMNetwork1 NewYork |Mapeado tooVMNetwork1-Chicago |
| VMNetwork2 NewYork |Não mapeados | | |
| Chicago |O VMM Chicago |VMNetwork1 Chicago |TooVMNetwork1-NewYork mapeada |
| VMNetwork2 Chicago |Não mapeados | | |

Com este exemplo:

* Quando é criada uma máquina virtual de réplica para qualquer máquina virtual que está ligado tooVMNetwork1-NewYork, será ligado tooVMNetwork1-Chicago.
* Quando é criada uma máquina virtual de réplica para VMNetwork2 NewYork ou VMNetwork2 Chicago, não será possível rede tooany ligado.

Eis como nuvens do VMM estão configuradas no nosso exemplo e organização Olá as redes lógicas associadas a nuvens Olá.

### <a name="cloud-protection-settings"></a>Definições de proteção de nuvem
| **Nuvem protegida** | **Proteção de nuvem** | **Rede lógica (Nova Iorque)** |
| --- | --- | --- |
| GoldCloud1 |GoldCloud2 | |
| SilverCloud1 |SilverCloud2 | |
| GoldCloud2 |<p>ND</p><p></p> |<p>LogicalNetwork1 NewYork</p><p>LogicalNetwork1 Chicago</p> |
| SilverCloud2 |<p>ND</p><p></p> |<p>LogicalNetwork1 NewYork</p><p>LogicalNetwork1 Chicago</p> |

### <a name="logical-and-vm-network-settings"></a>As definições de rede lógicas e VM
| **Localização** | **Rede lógica** | **Rede VM associado** |
| --- | --- | --- |
| Nova Iorque |LogicalNetwork1 NewYork |VMNetwork1 NewYork |
| Chicago |LogicalNetwork1 Chicago |VMNetwork1 Chicago |
| LogicalNetwork2Chicago |VMNetwork2 Chicago | |

### <a name="target-networks"></a>Redes de destino
Com base nestas definições, quando seleciona a rede VM de destino Olá, Olá a tabela seguinte mostra as opções de Olá que irão estar disponíveis.

| **Selecionar** | **Nuvem protegida** | **Proteção de nuvem** | **Rede de destino disponível** |
| --- | --- | --- | --- |
| VMNetwork1 Chicago |SilverCloud1 |SilverCloud2 |Disponível |
| GoldCloud1 |GoldCloud2 |Disponível | |
| VMNetwork2 Chicago |SilverCloud1 |SilverCloud2 |Não disponível |
| GoldCloud1 |GoldCloud2 |Disponível | |


### <a name="failback"></a>Reativação pós-falha
toosee o que acontece no caso de Olá de reativação pós-falha (a replicação inversa), vamos assumir que VMNetwork1 NewYork está mapeada tooVMNetwork1-Chicago com Olá seguintes definições.

| **Máquina virtual** | **Rede tooVM ligado** |
| --- | --- |
| VM1 |Rede VMNetwork1 |
| VM2 (réplica do VM1) |VMNetwork1 Chicago |

Com estas definições, vamos rever o que acontece em alguns cenários possíveis.

| **Cenário** | **Resultado** |
| --- | --- |
| Nenhuma alteração nas propriedades da rede Olá de VM 2 após a ativação pós-falha. |VM 1 permanece ligado toohello rede de origem. |
| Propriedades da rede de VM-2 foram alterados após a ativação pós-falha e está desligado. |VM-1 é desligado. |
| Propriedades da rede de VM-2 foram alteradas após a ativação pós-falha e está ligado tooVMNetwork2-Chicago. |Se não está mapeada VMNetwork2 Chicago, VM 1 será desligado. |
| Mapeamento da rede de VMNetwork1 Chicago é alterado. |VM 1 será ligado toohello rede mapeada agora tooVMNetwork1-Chicago. |


## <a name="prepare-for-single-server-deployment"></a>Preparar a implementação de servidor único


Se tiver apenas um único servidor do VMM, pode replicar as VMs nos anfitriões Hyper-V na nuvem VMM de Olá demasiado[Azure](site-recovery-vmm-to-azure.md) ou tooa secundária nuvem do VMM. Recomendamos que opção de primeiro Olá porque a replicar entre nuvens não está totalmente integrada. Se quiser tooreplicate entre nuvens, pode replicar com um servidor VMM autónomo único ou com um único servidor do VMM implementado num cluster do Windows Stretch

### <a name="standalone-vmm-server"></a>Servidor de VMM autónomo

Neste cenário, pode implementar Olá único o servidor do VMM como uma máquina virtual no site primário Olá e replicar este site secundário de VM tooa utilizando a recuperação de sites e de réplica do Hyper-V.

1. **Configurar o VMM numa VM de Hyper-V**. Sugerimos que colocalizar instância do SQL Server Olá utilizada pelo VMM no Olá mesma VM. Isto poupa tempo, como apenas uma VM tem toobe criado. Se quiser toouse instância remota do SQL Server e ocorrer uma falha, é necessário toorecover essa instância para poder recuperar VMM.
2. **Certifique-se o servidor do VMM de Olá tem, pelo menos, dois nuvens configuradas**. Uma nuvem irá conter Olá VMs que pretende tooreplicate e Olá outra nuvem irão servir como localização secundária Olá. Olá cloud que contenha VMs Olá pretende tooprotect devem estar em conformidade com [pré-requisitos](#prerequisites).
3. Configure a recuperação de Site, tal como descrito neste artigo. Criar e registar o servidor do VMM Olá num cofre, configurar uma política de replicação e ativar a replicação. nomes VMM de origem e destino Olá será Olá à mesma. Especifique que a replicação inicial ocorre através de rede de Olá.
4. Quando configurar o mapeamento de rede mapa de rede VM Olá para a rede VM Olá nuvem principal toohello para a nuvem secundário Olá.
5. Na consola do Gestor de Hyper-V Olá, ativar a réplica do Hyper-V no anfitrião de Hyper-V de Olá contém Olá VM do VMM e ativar a replicação Olá VM. Certifique-se de que não acrescentam Olá VMM tooclouds de máquina virtual que estão protegidos pela recuperação de sites, tooensure que as definições de réplica do Hyper-V não são substituídas pela recuperação de sites.
6. Se criar planos de recuperação para ativação pós-falha que utiliza Olá mesmo servidor VMM de origem e de destino.
7. Uma falha completa, efetuar a ativação pós-falha e recuperar da seguinte forma:

   1. Execute uma ativação pós-falha não planeada na consola do Gestor de Hyper-V Olá no site secundário do Olá, toofail através de Olá primário VM do VMM toohello site secundário.
   2. Certifique-se de que Olá que VM do VMM está a funcionar e está em execução e no Cofre de Olá, execute um toofail de ativação pós-falha não planeada ativação pós-falha de VMs de Olá das nuvens toosecondary primário. Consolidar ativação pós-falha de Olá e selecione um ponto de recuperação alternativo, se necessário.
   3. Depois de Olá ativação pós-falha não planeada concluída, todos os recursos podem ser acedidos novamente de site primário Olá.
   4. Quando o site primário Olá está disponível novamente, na consola do Gestor de Hyper-V Olá no site secundário Olá, ative a replicação inversa para Olá VM do VMM. Esta ação inicia a replicação para Olá VM de tooprimary secundário.
   5. Execute uma ativação pós-falha planeada na consola do Gestor de Hyper-V Olá no site secundário do Olá, toofail através de Olá site primário do toohello VM do VMM. Consolide ativação pós-falha de Olá. Em seguida, ative a replicação inversa, para que hello VM do VMM é novamente replicar do toosecondary primário.
   6. No Cofre de serviços de recuperação Olá, ative a replicação inversa para a carga de trabalho Olá VMs, toostart replicá-los a partir de tooprimary secundário.
   7. No Cofre de serviços de recuperação do Olá, execute um ativação pós-falha planeada toofail Olá back carga de trabalho VMs toohello site primário. Consolidar toocomplete de ativação pós-falha de Olá-lo. Em seguida, ative a replicação inversa toostart replicação Olá carga de trabalho VMs de toosecondary primário.

### <a name="stretched-vmm-cluster"></a>Cluster do VMM Stretch

Em vez de implementar um servidor VMM autónomo como uma VM que replica tooa site secundário, pode efetuar VMM altamente disponível implementando-a como uma VM num cluster de ativação pós-falha do Windows. Esta opção fornece resiliência da carga de trabalho e a proteção contra falhas de hardware. toodeploy com Olá de recuperação de Site VM do VMM deve ser implementado num cluster de stretch em todos os sites geograficamente separadas. toodo isto:

1. Instalar o VMM numa máquina virtual num cluster de ativação pós-falha do Windows e selecione o servidor do Olá opção toorun Olá como altamente disponível durante a configuração.
2. instância do SQL Server Olá que é utilizada pelo VMM deve ser replicada com grupos de Disponibilidade AlwaysOn do SQL Server, pelo que não haja uma réplica da base de dados de Olá no site secundário Olá.
3. Siga as instruções de Olá toocreate este artigo um cofre, registar servidor Olá e configurar a proteção. É necessário tooregister cada servidor VMM Olá cluster no Olá cofre dos serviços de recuperação. toodo isto, instale Olá fornecedor num nó ativo e registar o servidor do VMM Olá. Em seguida, instale Olá fornecedor nos outros nós.
4. Quando ocorre uma falha, servidor do VMM Olá e respetiva base de dados correspondente do SQL Server estão a ativação pós-falha e acessível a partir do site secundário Olá.



## <a name="prepare-for-storage-mapping"></a>Preparar o mapeamento do armazenamento


Configurar armazenamento de mapeamento pelo mapeamento de classificações de armazenamento numa origem e destino seguinte do VMM servidores toodo Olá:

  * **Identificar o armazenamento de destino para máquinas virtuais de réplica**— um disco de rígido VM de origem serão replicadas armazenamento toohello que especificou (cluster ou partilha SMB volumes partilhados (CSV)) na localização de destino Olá.
  * **O posicionamento de máquinas virtuais de réplica**— o mapeamento de armazenamento é utilizado toooptimally máquinas de virtuais de réplica local nos servidores de anfitrião do Hyper-V. Máquinas virtuais de réplica serão colocadas em anfitriões que podem aceder a classificação de armazenamento Olá mapeado.
  * **Nenhum mapeamento de armazenamento**— se não configurar o mapeamento de armazenamento, máquinas virtuais serão replicadas toohello localização de armazenamento de predefinido especificada no servidor de anfitrião de Olá Hyper-V associado com Olá máquina virtual de réplica.

Tenha em atenção que:
- Pode configurar o mapeamento entre duas nuvens do VMM num único servidor.
- Classificações de armazenamento tem de ser toohello disponíveis grupos de anfitriões localizados em nuvens de origem e de destino.
- Não precisam de classificações toohave Olá mesmo tipo de armazenamento. Por exemplo, pode mapear uma classificação de origem que contém a classificação destino de tooa de partilhas SMB que contém CSV.

### <a name="example"></a>Exemplo
Se classificações estão configuradas corretamente no VMM, quando seleciona Olá origem e de servidor do VMM de destino durante o mapeamento de armazenamento, serão apresentadas classificações Olá de origem e de destino. Eis um exemplo de partilhas de ficheiros de armazenamento e classificações para uma organização com duas localizações em Nova Iorque e Chicago.

| **Localização** | **Servidor VMM** | **Partilha de ficheiro (origem)** | **Classificação (origem)** | **Mapeado para** | **Partilha de ficheiros (destino)** |
| --- | --- | --- | --- | --- | --- |
| Nova Iorque |VMM_Source |SourceShare1 |GOLD |GOLD_TARGET |TargetShare1 |
| SourceShare2 |SILVER |SILVER_TARGET |TargetShare2 | | |
| SourceShare3 |BRONZE |BRONZE_TARGET |TargetShare3 | | |
| Chicago |VMM_Target | |GOLD_TARGET |Não mapeados | |
|  |SILVER_TARGET |Não mapeados | | | |
|  |BRONZE_TARGET |Não mapeados | | | |

Com este exemplo:

* Quando é criada uma máquina virtual de réplica para qualquer máquina virtual no armazenamento de ouro (SourceShare1), serão replicadas tooa GOLD_TARGET armazenamento (TargetShare1).
* Quando é criada uma máquina virtual de réplica para qualquer máquina virtual no armazenamento prata (SourceShare2), este será seja replicado tooa SILVER_TARGET (TargetShare2) de armazenamento e assim sucessivamente.

### <a name="multiple-storage-locations"></a>Várias localizações de armazenamento
Se for atribuída a classificação de destino Olá partilhas do SMB toomultiple ou CSVs, localização de armazenamento ótimo Olá será automaticamente selecionada quando Olá a máquina virtual está protegida. Se nenhum armazenamento de destino adequado está disponível com Olá especificada a classificação, predefinição Olá localização de armazenamento especificada no anfitrião de Olá Hyper-V é utilizado tooplace Olá réplica os discos rígidos virtuais.

Olá, a tabela seguinte mostra como a classificação de armazenamento e volumes partilhados de cluster estão configurados no nosso exemplo.

| **Localização** | **Classificação** | **Armazenamento associado** |
| --- | --- | --- |
| Nova Iorque |GOLD |<p>C:\ClusterStorage\SourceVolume1</p><p>\\FileServer\SourceShare1</p> |
| SILVER |<p>C:\ClusterStorage\SourceVolume2</p><p>\\FileServer\SourceShare2</p> | |
| Chicago |GOLD_TARGET |<p>C:\ClusterStorage\TargetVolume1</p><p>\\FileServer\TargetShare1</p> |
| SILVER_TARGET |<p>C:\ClusterStorage\TargetVolume2</p><p>\\FileServer\TargetShare2</p> | |

Esta tabela resume o comportamento de Olá, quando ativar a proteção para máquinas virtuais (VM1 - VM5) neste ambiente de exemplo.

| **Máquina virtual** | **Armazenamento de origem** | **Classificação de origem** | **Armazenamento de destino mapeado** |
| --- | --- | --- | --- |
| VM1 |C:\ClusterStorage\SourceVolume1 |GOLD |<p>C:\ClusterStorage\SourceVolume1</p><p>\\\FileServer\SourceShare1</p><p>Ambos os GOLD_TARGET</p> |
| VM2 |\\FileServer\SourceShare1 |GOLD |<p>C:\ClusterStorage\SourceVolume1</p><p>\\FileServer\SourceShare1</p> <p>Ambos os GOLD_TARGET</p> |
| VM3 |C:\ClusterStorage\SourceVolume2 |SILVER |<p>C:\ClusterStorage\SourceVolume2</p><p>\FileServer\SourceShare2</p> |
| VM4 |\FileServer\SourceShare2 |SILVER |<p>C:\ClusterStorage\SourceVolume2</p><p>\\FileServer\SourceShare2</p><p>Ambos os SILVER_TARGET</p> |
| VM5 |C:\ClusterStorage\SourceVolume3 |N/D |Nenhum mapeamento, pelo que a localização de armazenamento predefinida Olá do anfitrião de Olá Hyper-V é utilizada |



### <a name="data-privacy-overview"></a>Descrição geral da privacidade de dados

Esta tabela resume o modo como os dados são armazenados neste cenário:

- - -
| Ação | **Detalhes** | **Dados recolhidos** | **Utilizar** | **Necessário** |
| --- | --- | --- | --- | --- |
| **Registo** | Registar um servidor do VMM num cofre dos serviços de recuperação. Se posteriormente quiser toounregister um servidor, pode fazê-lo ao eliminar as informações do servidor Olá de Olá portal do Azure. | Depois de um servidor do VMM está registado recuperação do Site recolhe, processos e transfere os metadados sobre o servidor do VMM Olá e nomes de Olá das nuvens do VMM Olá detetadas pelo Site Recovery. | dados Olá tooidentify utilizado e comunicam com o servidor do VMM adequado Olá e configurar as definições para as nuvens do VMM adequadas. | Esta funcionalidade é necessária. Se não quiser toosend este tooSite informações de recuperação não deve utilizar o serviço de recuperação de sites Olá. |
| **Ativar replicação** | Olá fornecedor do Azure Site Recovery está instalado no servidor do VMM Olá e conduit Olá para a comunicação com Olá serviço de recuperação de Site. Olá fornecedor é uma biblioteca de ligação dinâmica (DLL) alojada no processo VMM Olá. Após Olá que fornecedor está instalado, a funcionalidade de "Recuperação de centros de dados" Olá obtém ativada na consola de administrador do VMM Olá. VMs novas e existentes podem ativar a proteção de tooenable esta funcionalidade para uma VM. |Com esta propriedade definida, Olá fornecedor envia o nome de Olá e o ID de VM de Olá tooSite recuperação.  A replicação está ativada pelo Windows Server 2012 ou Windows Server 2012 R2 Hyper-V réplica. dados da máquina virtual Olá obtém replicados a partir de um tooanother de anfitrião de Hyper-V (normalmente localizado no Centro de dados diferentes "recuperação de"). |Recuperação de site utiliza Olá toopopulate Olá VM as informações de metadados Olá portal do Azure. | Esta funcionalidade é uma parte essencial do serviço de Olá e não pode ser desativada. Se não quiser toosend esta informação, não ative a proteção de recuperação de Site para as VMs. Tenha em atenção de que todos os dados enviados por Olá fornecedor tooSite recuperação é enviado através de HTTPS. |
| **Plano de recuperação** | Planos de recuperação ajudam a criar um plano de orquestração de centro de dados de recuperação Olá. Pode definir a ordem de Olá em que deverão ser iniciado no site de recuperação Olá VMs ou um grupo de máquinas virtuais. Também pode especificar qualquer toobe scripts automatizados, executar ou toobe qualquer ação manual captado, de momento Olá de recuperação para cada VM. Ativação pós-falha, normalmente, é acionada ao nível do plano de recuperação Olá para recuperação coordenada. | Recuperação de site recolhe, processa e transmite os metadados para o plano de recuperação Olá, incluindo os metadados da máquina virtual e metadados de quaisquer scripts de automatização e notas da ação manual. |os metadados de Olá são utilizados toobuild Olá plano de recuperação no Olá portal do Azure. |Esta funcionalidade é uma parte essencial do serviço de Olá e não pode ser desativada. Se não quiser toosend este tooSite informações de recuperação, não crie planos de recuperação. |
| **Mapeamento da rede** | Mapeamentos de rede informações a partir do Centro de dados de recuperação center toohello Olá dados primários. Quando são recuperadas VMs no site de recuperação Olá, mapeamento da rede ajuda a estabelecer conectividade de rede. |Recuperação de site recolhe, processa e transmite Olá metadados de redes lógicas do Olá para cada site (primário e datacenter). |metadados de Olá são toopopulate utilizadas as definições de rede para que pode mapear informações da rede Olá. | Esta funcionalidade é uma parte essencial do serviço de Olá e não pode ser desativada. Se não quiser toosend este tooSite informações de recuperação, não utilize o mapeamento da rede. |
| **Ativação pós-falha (planeada/não planeada/teste)** | Ativação pós-falha a ativação pós-falha VMs de tooanother do Centro de um dados gerida do VMM. ação de ativação pós-falha de Olá é acionada manualmente no Olá portal do Azure. |Olá fornecedor no servidor do VMM Olá é notificado de evento de ativação pós-falha de Olá pela recuperação de sites e executa uma ação de ativação pós-falha no anfitrião de Hyper-V Olá através de interfaces VMM. Ativação pós-falha real de uma VM é de um tooanother de anfitrião do Hyper-V e processado pelo Windows Server 2012 ou Windows Server 2012 R2 Hyper-V réplica. Recuperação de Site aft utiliza informações de Olá enviadas estado de Olá toopopulate das informações de ação de ativação pós-falha de Olá no Olá portal do Azure. | Esta funcionalidade é uma parte essencial do serviço de Olá e não pode ser desativada. Se não quiser toosend este tooSite informações de recuperação, não utilize a ativação pós-falha. |

## <a name="next-steps"></a>Passos seguintes

Depois de ter testado implementação Olá, saiba mais sobre outros tipos de [ativação pós-falha](site-recovery-failover.md)
