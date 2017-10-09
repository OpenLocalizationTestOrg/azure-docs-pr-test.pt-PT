---
title: "aaaReplicate servidores físicos tooAzure | Microsoft Docs"
description: "Descreve como toodeploy do Azure Site Recovery tooorchestrate replicação, ativação pós-falha e recuperação do local tooAzure de servidores físicos Windows/Linux utilizando Olá portal do Azure"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: 
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: raynew
ROBOTS: NOINDEX, NOFOLLOW
redirect_url: physical-walkthrough-overview
ms.openlocfilehash: cf5928fb631f6858d57b27f6f21babc312714e21
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
---
# <a name="replicate-physical-machines-tooazure-by-using-site-recovery"></a>Replicar máquinas físicas tooAzure utilizando a recuperação de Site


Este artigo descreve como tooreplicate no local máquinas físicas tooAzure utilizando o serviço do Azure Site Recovery Olá no Olá portal do Azure.

Se quiser toomigrate máquinas físicas tooAzure (ativação pós-falha apenas), leitura [migrar tooAzure com a recuperação de Site](site-recovery-migrate-to-azure.md) toolearn mais.

Publique comentários e perguntas na parte inferior de Olá deste artigo ou no Olá [fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="prerequisites"></a>Pré-requisitos

**Requisito de suporte** | **Detalhes**
--- | ---
**Azure** | Saiba mais sobre os [requisitos do Azure](site-recovery-prereq.md#azure-requirements).
**Servidor de configuração no local** | Máquina no local (física ou VM do VMware) com o Windows Server 2012 R2 ou posterior. Configurar o servidor de configuração de Olá durante a implementação da recuperação de Site.<br/><br/> Por predefinição, o servidor de processos de Olá e servidor de destino principal estão também instalados neste computador. Quando aumentar verticalmente, poderá ser necessário um servidor de processo separado e tem Olá mesmos requisitos como servidor de configuração de Olá.<br/><br/> Saiba mais sobre estes componentes no [configurar o ambiente de origem Olá](site-recovery-set-up-vmware-to-azure.md#configuration-server-minimum-requirements).
**VMs no local** | As máquinas que pretende tooreplicate devem estar a executar um [sistema operativo suportado](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions) e estar em conformidade com [pré-requisitos do Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).
**URLs** | servidor de configuração de Olá necessita de acesso toothese URLs:<br/><br/> [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]<br/><br/> Se tiver regras de firewall baseadas no endereço IP, certifique-se de que permitem comunicação tooAzure.<br/></br> Permitir Olá [intervalos de IP do Datacenter do Azure](https://www.microsoft.com/download/confirmation.aspx?id=41653) e Olá porta HTTPS (443).<br/></br> Permita intervalos de endereços IP para Olá região do Azure da sua subscrição e para EUA oeste (utilizado para gestão de identidade e controlo de acesso).<br/><br/> Permitir que este URL para transferência de MySQL Olá: http://cdn.mysql.com/archives/mysql-5.5/mysql-5.5.37-win32.msi.
**Serviço de mobilidade** | Este serviço é instalado em cada máquina que pretende tooreplicate.

## <a name="limitations"></a>Limitações

**Limitação** | **Detalhes**
--- | ---
**Azure** | Contas de armazenamento e rede tem de constar Olá mesma região que Olá cofre.<br/><br/> Se utilizar uma conta de armazenamento premium, terá também uma norma armazenar os registos de replicação de toostore de conta.<br/><br/> Não é possível replicar toopremium contas no centro e sul da Índia.
**Servidor de configuração no local** | Se instalar o servidor de configuração de Olá numa VMware VM, Olá o tipo de adaptador VM deve ser VMXNET3. Se não estiver, [instalar esta atualização](https://kb.vmware.com/selfservice/microsites/search.do?cmd=displayKC&docType=kc&externalId=2110245&sliceId=1&docTypeID=DT_KB_1_1&dialogID=26228401&stateId=1).<br/><br/> Se estiver a utilizar uma VM de VMware, vSphere PowerCLI 6.0 deve ser instalado no mesmo.<br/><br> máquina Olá não deve ser um controlador de domínio.<br/><br/> máquina Olá deve ter um endereço IP estático.<br/><br/> nome de anfitrião de Olá deve ter 15 carateres ou menos e sistema de operativo Olá deve estar em inglês.
**Máquinas replicadas** | Certifique-se [limitações de VM do Azure](site-recovery-prereq.md#azure-requirements).<br/><br/> Se pretender que o tooenable a consistência multi VM, que permite que as máquinas em execução Olá mesma carga de trabalho toobe recuperado tooa em conjunto de dados consistente ponto, abra a porta 20004 na máquina de Olá.<br/><br/> Tipos específicos de [Linux armazenamento](site-recovery-support-matrix-to-azure.md#support-for-storage) são suportados.
**Reativação pós-falha** | Não pode falhar novamente a partir do computador físico tooa do Azure. Se quiser toobe toofail capaz de back-tooon local após a ativação pós-falha, terá de um ambiente VMware, para que pode falhar back tooa VM de VMware.


## <a name="set-up-azure"></a>Configurar o Azure

1. [Configurar uma rede Azure](../virtual-network/virtual-networks-create-vnet-arm-pportal.md).

      a. As VMs do Azure são colocadas nesta rede quando são criados após a ativação pós-falha.

      b. Pode configurar uma rede no Azure [Resource Manager](../resource-manager-deployment-model.md) ou no modo clássico.

2. Configurar um [conta do storage do Azure](../storage/storage-create-storage-account.md#create-a-storage-account) para dados replicados.

    a. conta de Olá pode ser padrão ou [premium](../storage/storage-premium-storage.md).

    b. Pode configurar uma conta no Gestor de recursos ou no modo clássico.

## <a name="prepare-hello-configuration-server"></a>Preparar o servidor de configuração de Olá

1. Instale o Windows Server 2012 R2 ou posterior num servidor físico no local ou numa VM de VMware.

2. Certifique-se a máquina de Olá tem acesso toohello URLs listados na [pré-requisitos](#prerequisites).

## <a name="prepare-for-mobility-service-installation"></a>Preparar a instalação do serviço de mobilidade

Se quiser toopush Olá mobilidade serviço tooa máquina física, terá de uma conta que pode ser utilizada por máquinas de Olá Olá processo server tooaccess. conta de Olá é utilizada apenas para a instalação de push Olá. Pode utilizar um domínio ou conta local:

  - Para o Windows, se não estiver a utilizar uma conta de domínio, terá de toodisable controlo de acesso de utilizador remoto no computador local Olá. toodo isto, no registo de Olá em **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System**, adicionar a entrada de DWORD Olá **LocalAccountTokenFilterPolicy**, com um valor de 1. Se quiser entrada de registo de Olá tooadd para o Windows a partir de uma interface de linha de comandos, escreva:

        ``REG ADD HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System /v LocalAccountTokenFilterPolicy /t REG_DWORD /d 1.``
  - Para Linux conta Olá deve ser um utilizador de raiz no servidor de Linux Olá origem.


## <a name="create-a-recovery-services-vault"></a>Criar um cofre dos Serviços de Recuperação 

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]


## <a name="select-hello-protection-goal"></a>Selecione o objetivo de proteção de Olá

Selecione o que pretender tooreplicate e onde pretende tooreplicate para.

1. Clique em **cofres dos serviços de recuperação** > **cofre**.
2. No Olá **recursos** menu, clique em **recuperação de Site** > **preparar infraestrutura** > **objetivo de proteção**.

    ![Selecione os objetivos](./media/site-recovery-vmware-to-azure/choose-goal-physical.PNG)

3. No **objetivo de proteção**, selecione **tooAzure** > **não virtualizados / outras**.


## <a name="set-up-hello-source-environment"></a>Configurar o ambiente de origem Olá

Configurar o servidor de configuração de Olá, registe-o num cofre Olá e detetar VMs.

1. Clique em **recuperação de sites** > **preparar infraestrutura** > **origem**.
2. Se não tiver um servidor de configuração, clique em **+ o servidor de configuração**.

    ![Configurar a origem](./media/site-recovery-vmware-to-azure/set-source1.png)

3. No **Adicionar servidor**, verifique se **servidor de configuração** aparece no **tipo de servidor**.
4. Transferir Olá **Unified configuração do Site Recovery** ficheiro de instalação.
5. Transferir Olá **chave de registo do cofre**. Terá desta chave quando executar a configuração do Unified. chave de Olá é válido durante cinco dias depois de gerá-la.

   ![Configurar a origem](./media/site-recovery-vmware-to-azure/set-source2.png)


## <a name="run-site-recovery-unified-setup"></a>Recuperação de Site execução Unified programa de configuração

Antes de começar, Olá a seguir:

- Obter uma descrição geral de vídeo. (Olá vídeo descreve como processar tooreplicate VMs de VMware, mas Olá é semelhante para a replicação de máquina física.)

    > [!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video1-Source-Infrastructure-Setup/player]

- No computador do servidor de configuração de Olá, certifique-se de que o relógio do sistema Olá está sincronizado com um [hora server](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service). Se estiver à frente 15 minutos ou para trás, a configuração poderá falhar.
- Execute a configuração como um administrador local no computador do servidor de configuração de Olá.
- Certifique-se de que TLS 1.0 está ativada no computador de Olá.

[!INCLUDE [site-recovery-add-configuration-server](../../includes/site-recovery-add-configuration-server.md)]

> [!NOTE]
> Também pode ser instalado o servidor de configuração de Olá [partir da linha de comandos Olá](http://aka.ms/installconfigsrv).


## <a name="set-up-hello-target-environment"></a>Configurar o ambiente de destino Olá

Antes de configurar o ambiente de destino Olá, verifique toomake se de que tem um [conta do storage do Azure e rede](#set-up-azure).

1. Clique em **preparar infraestrutura** > **destino**, e selecione Olá pretende toouse de subscrição do Azure.
2. Especifique se o seu modelo de implementação de destino é o Gestor de recursos ou clássico.
3. Recuperação de sites verifica toomake se de que tem um ou mais contas do storage do Azure compatível e redes.

   ![destino](./media/site-recovery-vmware-to-azure/gs-target.png)

4. Se ainda não criou uma conta de armazenamento ou de rede, clique em **+ contas de armazenamento** ou **+ rede** toocreate inline de rede ou a conta de Gestor de recursos.

## <a name="set-up-replication-settings"></a>Configurar as definições de replicação

Antes de começar, obtenha uma rápida descrição geral do vídeo. (Olá vídeo descreve como processar tooreplicate VMs de VMware, mas Olá é semelhante para a replicação de máquina física.)

> [!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video2-vCenter-Server-Discovery-and-Replication-Policy/player]

1. toocreate uma nova política de replicação, clique em **infraestrutura de recuperação de Site** > **políticas de replicação** > **+ política de replicação**.
2. No **criar política de replicação**, especifique um nome de política.
3. No **limiar RPO**, especificar Olá RPO limite. Este valor Especifica com que frequência são criados pontos de recuperação de dados. É gerado um alerta se a replicação contínua excede este limite.
4. No **retenção do ponto de recuperação**, especifique o período de tempo (em horas) está janela de retenção de Olá para cada ponto de recuperação. VMs replicadas podem ser recuperados tooany ponto numa janela. Cópia de segurança too24 retenção dos horas é suportada para máquinas toopremium replicadas armazenamento. Cópia de segurança too72 retenção dos horas é suportada para máquinas toostandard replicadas armazenamento.
5. No **frequência de instantâneos consistentes com aplicação**, especifique com que frequência (em minutos) são criados pontos de recuperação que contêm os instantâneos consistentes com aplicações. Clique em **OK** política de Olá toocreate.

    ![Política de replicação](./media/site-recovery-vmware-to-azure/gs-replication2.png)

6. Quando cria uma nova política,-la automaticamente associado ao servidor de configuração de Olá. Por predefinição, uma política correspondente é criada automaticamente para reativação pós-falha. Por exemplo, se hello política de replicação é **rep política**, em seguida, a política de reativação pós-falha Olá é **rep-política-reativação pós-falha**. Esta política não é utilizada depois de iniciar uma reativação pós-falha a partir do Azure.  


## <a name="plan-capacity"></a>Planear a capacidade

1. Agora que configurou a sua infraestrutura básica, configurar, pode pensar sobre o planeamento de capacidade e averiguar se precisa de recursos adicionais. [Saiba mais](site-recovery-plan-capacity-vmware.md).
2. Quando tiver terminado com o planeamento de capacidade, selecione **Sim** no **concluiu o planeamento de capacidade?**

   ![Planeamento de capacidade](./media/site-recovery-vmware-to-azure/gs-capacity-planning.png)


## <a name="prepare-vms-for-replication"></a>Preparar as VMs para a replicação

Todas as máquinas que pretende que o tooreplicate tem de ter instalado um serviço de mobilidade de Olá. Pode instalar o serviço de mobilidade Olá de diversas formas:

- Instale o serviço de Olá com uma instalação push do servidor de processos de Olá. Necessita de máquinas de tooprepare no avançadas toouse este método.
- Instale o serviço de Olá utilizando ferramentas de implementação, como o System Center Configuration Manager ou a configuração de estado pretendido do Azure da automatização.
- Instale manualmente o serviço de Olá.

[Saiba mais](site-recovery-vmware-to-azure-install-mob-svc.md).


## <a name="enable-replication"></a>Ativar a replicação

Antes de começar:

- A conta de utilizador do Azure tem toohave determinadas [permissões](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) tooenable replicação de um novo tooAzure de máquina virtual.
- Quando adiciona ou modifica as VMs, pode demorar até too15 minutos ou já está para efeitos de tootake alterações e para os mesmos tooappear no portal de Olá.
- Pode verificar o tempo Olá pela última vez detetado para VMs no **servidores de configuração** > **último contacto em**.
- tooadd VMs sem aguardar deteção agendada do Olá, servidor de configuração de Olá realce (não clique nele) e clique em **atualizar**.
- Se uma VM está preparada para a instalação de push, o servidor de processos de Olá instala automaticamente o serviço de mobilidade Olá ao ativar a replicação.
- Obter uma descrição geral de vídeo. (Olá vídeo descreve como processar tooreplicate VMs de VMware, mas Olá é semelhante para a replicação de máquina física.)

    >[!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video3-Protect-VMware-Virtual-Machines/player]


### <a name="exclude-disks-from-replication"></a>Excluir discos da replicação

Por predefinição, todos os discos numa máquina são replicados. Pode excluir discos de replicação. Por exemplo, não poderá tooreplicate discos com dados temporários ou dados que foi atualizada a cada hora reinicia um computador ou da aplicação (por exemplo, pagefile.sys ou tempdb do SQL Server).

### <a name="replicate-vms"></a>Replicar VMs

1. Clique em **replicar aplicação** > **origem**.
2. No **origem**, selecione **no local**.
3. No **localização de origem**, selecione nome do servidor de configuração de Olá.
4. No **máquina tipo**, selecione **máquinas físicas**.
5. No **servidor de processos**, escolha o servidor de processos de Olá. Se ainda não criou quaisquer servidores de processos adicionais, este servidor é o servidor de configuração de Olá. Em seguida, clique em **OK**.

    ![Ativar a replicação](./media/site-recovery-physical-to-azure/chooseVM.png)

6. No **destino**, selecione Olá **subscrição** e Olá **grupo de recursos** em que pretende toocreate Olá VMs do Azure após a ativação pós-falha. Escolha a implementação de Olá modelo que pretende que o toouse no Azure (clássico ou do Resource Manager) para Olá efetuada a ativação pós-falha VMs.

7. Selecione a conta de armazenamento do Azure de Olá que pretende toouse para replicar os dados. Se não quiser toouse uma conta que já configurou, pode criar um novo.

8. Selecione Olá **rede Azure** e **sub-rede** ligar toowhich VMs do Azure após a ativação pós-falha. Selecione **configurar agora para as máquinas selecionadas** tooapply Olá rede definição tooall máquinas selecionadas para proteção. Selecione **configurar mais tarde** tooselect Olá rede do Azure por máquina. Se não quiser toouse uma rede existente, pode criar uma.

    ![Ativar a replicação](./media/site-recovery-physical-to-azure/targetsettings.png)

9. No **máquinas físicas**, clique em **+ máquina física** e introduza Olá **nome** e **endereço IP**. Escolha o sistema de operativo Olá da máquina de Olá pretende tooreplicate. Demora alguns minutos até que as máquinas são detetadas e apresentadas na lista de Olá.

    ![Ativar a replicação](./media/site-recovery-physical-to-azure/machineselect.png)

10. No **propriedades** > **configurar propriedades**, selecione a conta de Olá toobe utilizado pelo tooautomatically de servidor de processo Olá instalar o serviço de mobilidade Olá na máquina de Olá.
11. Por predefinição, todos os discos são replicados. Clique em **todos os discos**e desmarque todos os discos que não pretende tooreplicate. Em seguida, clique em **OK**. Pode definir propriedades VM adicionais mais tarde.

    ![Ativar a replicação](./media/site-recovery-physical-to-azure/configprop.png)

12. No **as definições de replicação** > **configurar as definições de replicação**, certifique-se de que Olá correta está selecionada a política de replicação. Se modificar uma política, as alterações serão aplicada toohello máquina e toonew máquinas a replicar.
13. Ativar **a consistência Multi VM** se pretender toogather máquinas para um grupo de replicação e especificar um nome para o grupo de Olá. Em seguida, clique em **OK**. Tenha em atenção que:

    a. Computadores em grupos de replicação replicar em conjunto e tem partilhado pontos de recuperação consistentes com falhas e consistentes da aplicação quando efetuar a ativação pós-falha.

    b. Recomendamos que pode reunir VMs e servidores físicos, para que estes espelhar as cargas de trabalho. Ativar a consistência de várias VMS pode afetar o desempenho da carga de trabalho. Deve ser utilizada apenas se as máquinas estão em execução Olá mesma carga de trabalho e necessitar de consistência.

    ![Ativar a replicação](./media/site-recovery-physical-to-azure/policy.png)

14. Clique em **ativar a replicação**. Pode controlar o progresso de Olá **ativar proteção** da tarefa no **definições** > **tarefas** > **tarefas de recuperação de Site**. Depois de Olá **finalizar proteção** tarefa será executada, a máquina de Olá está preparada para ativação pós-falha.

Depois de ativar a replicação, Olá serviço de mobilidade está instalado se configurou a instalação push. Após Olá serviço de mobilidade push instalado num computador, uma tarefa de proteção é iniciado e falha. Após a falha de Olá, terá de toomanually reiniciar cada máquina. Em seguida, a tarefa de proteção Olá começa novamente e ocorre a replicação inicial.


### <a name="view-and-manage-azure-vm-properties"></a>Ver e gerir propriedades da VM do Azure

Recomendamos que verifique Olá propriedades da VM e efetue as alterações que precisa.

1. Clique em **replicado itens**e selecione Olá máquina. Olá **Essentials** painel mostra informações sobre o estado e as definições de máquinas.
2. No **propriedades**, pode ver a replicação e informações de ativação pós-falha para Olá VM.
3. No **computação e rede** > **propriedades de computação**, pode especificar o tamanho de nome e o destino da VM do Azure Olá. Modificar Olá nome toocomply com [requisitos do Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements) se for necessário.
4. Modificar as definições de rede de destino Olá, uma sub-rede e endereço IP que são atribuídas toohello VM do Azure:

    a. Pode definir o endereço IP de destino Olá.

    b.  Se não fornecer um endereço, Olá efetuada a ativação pós-falha utiliza DHCP.

    c. Se definir um endereço que não está disponível na ativação pós-falha, a ativação pós-falha não funciona.

    d. Olá mesmo endereço IP de destino pode ser utilizado para ativação pós-falha de teste se o endereço de Olá está disponível na rede de ativação pós-falha de teste de Olá.

    e. número de Olá dos adaptadores de rede é ditado pelo tamanho de Olá especificado para a máquina virtual de destino Olá:

     - Se Olá o número de adaptadores de rede na máquina de origem Olá é Olá igual ou inferior ao número de Olá de adaptadores permitido para o tamanho da máquina de destino Olá, em seguida, o destino de Olá tem Olá mesmo número de adaptadores que origem Olá.
     - Se Olá número de adaptadores Olá máquina virtual de origem exceder o número de Olá permitido para o tamanho de destino Olá, em seguida, é utilizado o tamanho máximo de destino Olá.
     - Por exemplo, se uma máquina de origem tiver dois adaptadores de rede e tamanho da máquina Olá destino suporta quatro, o computador de destino de Olá tem dois adaptadores. Se Olá máquina de origem tiver dois adaptadores, mas o tamanho de destino Olá suportado suporta apenas um, o computador de destino de Olá tem apenas um adaptador.     
   - Se a máquina virtual de Olá tiver múltiplos adaptadores de rede, todos os ligam toohello mesma rede.
   - Se máquinas de virtuais Olá tem vários adaptadores de rede, em seguida, hello primeiro mostrado na lista de Olá fica Olá *predefinido* adaptador de rede no Olá VM do Azure.
5. No **discos**, pode ver o sistema de operativo Olá VM e os discos de dados de Olá são replicados.

## <a name="run-a-test-failover"></a>Executar uma ativação pós-falha de teste

Depois de ter configurado tudo, execute um toomake de ativação pós-falha de teste se que tudo está a funcionar conforme esperado. Veja uma rápida descrição geral do vídeo antes de começar.

>[!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video4-Recovery-Plan-DR-Drill-and-Failover/player]


1. toofail através de uma única máquina no **definições** > **itens replicados**, clique em **ativação pós-falha de teste**.

    ![Ativação pós-falha de teste](./media/site-recovery-vmware-to-azure/TestFailover.png)

2. Planear toofail através de uma recuperação, na **definições** > **planos de recuperação**, plano do contexto Olá > **ativação pós-falha de teste**. toocreate um plano de recuperação, [siga estas instruções](site-recovery-create-recovery-plans.md).  
3. No **ativação pós-falha de teste**, selecione Olá rede Azure toowhich VMs do Azure estão ligadas após a ocorrência da ativação pós-falha.
4. Clique em **OK** toobegin ativação pós-falha de Olá. Pode controlar o progresso clicando Olá VM tooopen as respetivas propriedades ou clicando Olá **ativação pós-falha de teste** tarefa no nome do cofre > **definições** > **tarefas**  >  **As tarefas de recuperação de site**.
5. Após a conclusão da ativação pós-falha de Olá, também deve ser capaz de réplica de Olá toosee máquina do Azure são apresentados no Olá portal do Azure > **máquinas virtuais**. Certifique-se que Olá VM Olá um tamanho adequado, que tenha ligado toohello adequada de rede, e que está em execução.
6. Se lhe [preparou para as ligações após a ativação pós-falha](site-recovery-test-failover-to-azure.md#prepare-to-connect-to-azure-vms-after-failover), deve ser capaz de tooconnect toohello VM do Azure.
7. Quando tiver terminado, clique em **ativação pós-falha de teste de limpeza** no plano de recuperação Olá. No **notas**, registar e guardar todas as observações associadas à ativação pós-falha de teste de Olá. Este passo elimina Olá as máquinas virtuais que foram criadas durante a ativação pós-falha de teste.

Para obter mais informações, consulte Olá [tooAzure de ativação pós-falha de teste](site-recovery-test-failover-to-azure.md) documento.

## <a name="next-steps"></a>Passos seguintes

Depois de obter replicação cópias de segurança e em execução, quando ocorre uma falha falhar tooAzure e as VMs do Azure são criadas a partir dos dados de Olá replicado. Pode, em seguida, aceder a cargas de trabalho e aplicações do Azure, até falhar localização primária de back-tooyour quando se retomam as operações de toonormal.

- [Saiba mais](site-recovery-failover.md) sobre os diferentes tipos de ativações pós-falha e como toorun-los.
- Se estiver a migrar máquinas em vez de replicar e a falhar back, [ler mais](site-recovery-migrate-to-azure.md#migrate-on-premises-vms-and-physical-servers).
- Quando replicar máquinas físicas, pode apenas reativação pós-falha tooa VMware ambiente. [Leia sobre a reativação pós-falha](site-recovery-failback-azure-to-vmware.md).

## <a name="third-party-software-notices-and-information"></a>Informações e avisos de software de terceiros
Não traduzir ou localizar

software Olá e firmware em execução no Olá produto da Microsoft ou de serviço baseia-se no incorpora material de Olá projetos listados abaixo (coletivamente designados por "código de terceiros"). A Microsoft não está autor original de Olá de Olá código de terceiros. Aviso de direitos original Olá e licenciamento, sob a qual a Microsoft recebido desse código de terceiros, estão definidos especificado abaixo.

informações Olá secção A estão sobre o código de terceiros componentes de projetos de Olá listados abaixo. Essas licenças e as informações são fornecidas apenas para fins informativos. Este código de terceiros está a ser tooyou relicensed pela Microsoft em termos de licenciamento Olá Microsoft produto ou serviço de licenciamento de software da Microsoft.  

informações de Olá na secção B é sobre componentes de código de terceiros que estão a ser efetuados tooyou disponível pela Microsoft em termos de licenciamento original Olá.

ficheiro completo Olá pode ser encontrado no Olá [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=529428). Microsoft reserva-se a todos os direitos que não estejam expressamente concedidos neste documento, seja por implicação, preclusão, ou, caso contrário.
