---
title: aaaReplicate VMs de VMware tooAzure | Microsoft Docs
description: "Resume os passos de Olá que precisa para replicar as cargas de trabalho em execução em VMs de VMware tooAzure armazenamento"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: dab98aa5-9c41-4475-b7dc-2e07ab1cfd18
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: raynew
ROBOTS: NOINDEX, NOFOLLOW
redirect_url: vmware-walkthrough-overview
ms.openlocfilehash: f800e7d8a3b59a86809a995748eacf87630a1713
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-vmware-virtual-machines-tooazure-with-site-recovery"></a>Replicar máquinas virtuais de VMware tooAzure com a recuperação de Site

> [!div class="op_single_selector"]
> * [Portal do Azure](site-recovery-vmware-to-azure.md)
> * [Azure clássico](site-recovery-vmware-to-azure-classic.md)


Este artigo descreve como tooreplicate no local tooAzure de máquinas virtuais de VMware, utilizando Olá [do Azure Site Recovery](site-recovery-overview.md) serviço no Olá portal do Azure.

Se quiser toomigrate VMs de VMware tooAzure (ativação pós-falha apenas), leitura [neste artigo](site-recovery-migrate-to-azure.md) toolearn mais.

Publique comentários e perguntas na parte inferior de Olá deste artigo ou no Olá [fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="deployment-steps"></a>Passos da implementação

Eis o que precisa de toodo:

1. Verifique os pré-requisitos e as limitações.
2. Configure uma rede do Azure e contas de armazenamento.
3. Preparar a máquina no local de Olá que quiser toodeploy como servidor de configuração de Olá.
4. Prepare contas VMware toobe utilizado para a deteção automática de VMs e, opcionalmente, para a instalação push do serviço de mobilidade de Olá.
4. Crie um cofre dos Serviços de Recuperação. cofre Olá contém definições de configuração e orquestra a replicação.
5. Especifique as definições de replicação, origem e destino.
6. Implementar o serviço de mobilidade Olá em VMs que pretende tooreplicate.
7. Ative a replicação para Olá VMs.
7. Execute um toomake de ativação pós-falha de teste se que tudo está a funcionar conforme esperado.

## <a name="prerequisites"></a>Pré-requisitos

**Requisito de suporte** | **Detalhes**
--- | ---
**Azure** | Saiba mais sobre [requisitos do Azure](site-recovery-prereq.md#azure-requirements)
**Servidor de configuração no local** | Precisa de uma VM de VMware com o Windows Server 2012 R2 ou posterior. Configurar este servidor durante a implementação da recuperação de Site.<br/><br/> Processo de Olá predefinido o servidor e o servidor de destino principal também estão instaladas nesta VM. Quando aumentar verticalmente, poderá ser necessário um servidor de processo separado e tem Olá mesmos requisitos como servidor de configuração de Olá.<br/><br/> Saiba mais sobre estes componentes [aqui](site-recovery-set-up-vmware-to-azure.md#configuration-server-minimum-requirements)
**Servidores do VMware no local** | Um ou mais VMware vSphere servidores, com 6.0, 5.5, 5.1 com as atualizações mais recentes. Servidores devem estar localizados em Olá mesmo de rede como servidor de configuração de Olá (ou servidor de processo separado).<br/><br/> Recomendamos um vCenter anfitriões de toomanage de servidor, com as atualizações mais recentes do Olá 6.0 ou 5.5. Apenas as funcionalidades que estão disponíveis no 5.5 são suportadas quando implementar a versão 6.0.
**VMs no local** | As VMs que pretende tooreplicate devem estar a executar um [sistema operativo suportado](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions)e em conformidade com [pré-requisitos do Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements). VM deve ter as ferramentas do VMware em execução.
**URLs** | servidor de configuração de Olá necessita de acesso toothese URLs:<br/><br/> [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]<br/><br/> Se tiver regras de firewall baseadas no endereço IP, certifique-se de que permitem comunicação tooAzure.<br/></br> Permitir Olá [intervalos de IP do Datacenter do Azure](https://www.microsoft.com/download/confirmation.aspx?id=41653)e Olá porta HTTPS (443).<br/></br> Permita intervalos de endereços IP para Olá região do Azure da sua subscrição e para EUA oeste (utilizado para gestão de identidade e controlo de acesso).<br/><br/> Permitir que este URL para transferência de MySQL Olá: http://cdn.mysql.com/archives/mysql-5.5/mysql-5.5.37-win32.msi.
**Serviço de mobilidade** | Instalado em cada VM replicada.




## <a name="limitations"></a>Limitações

**Limitação** | **Detalhes**
--- | ---
**Azure** | Contas de armazenamento e rede tem de constar Olá mesma região que Olá Cofre<br/><br/> Se utilizar uma conta de armazenamento premium, terá também uma norma armazenar os registos de replicação de toostore de conta<br/><br/> Não é possível replicar toopremium contas no centro e sul da Índia.
**Servidor de configuração no local** | O tipo de adaptador de VM de VMware, deve ser VMXNET3. Se não estiver, [instalar esta atualização](https://kb.vmware.com/selfservice/microsites/search.do?cmd=displayKC&docType=kc&externalId=2110245&sliceId=1&docTypeID=DT_KB_1_1&dialogID=26228401&stateId=1)<br/><br/> deve ser instalado o vSphere PowerCLI 6.0.<br/><br> máquina Olá não deve ser um controlador de domínio. máquina Olá deve ter um endereço IP estático.<br/><br/> nome de anfitrião de Olá deve ter 15 carateres ou menos e sistema operativo deve estar em inglês.
**VMware** | Apenas 5.5 funcionalidades são suportadas no vCenter 6.0. Recuperação de sites não suporta o vCenter novo e vSphere 6.0 funcionalidades, tais como cruzam vCenter vMotion, volumes virtuais e armazenamento DRS.
**VMs** | Certifique-se [limitações de VM do Azure](site-recovery-prereq.md#azure-requirements)<br/><br/> Não é possível replicar as VMs com discos encriptados ou VMs com o arranque UEFI/EFI.<br/><br> Partilhada não são suportados clusters de disco. Se a VM de origem Olá tem o agrupamento NIC, é convertido tooa único NIC após a ativação pós-falha.<br/><br/> Se as VMs têm um disco iSCSI, a recuperação de sites converte-o ficheiro VHD tooa após a ativação pós-falha. Se o destino de iSCSI Olá pode ser acedido por Olá VM do Azure, liga tooit e vê-lo tanto Olá VHD. Se isto acontecer, desligar o destino de iSCSI Olá.<br/><br/> Se pretender que o tooenable a consistência multi VM, que permite que as VMs com Olá recuperado mesmo toobe de carga de trabalho tooa em conjunto de dados consistente ponto, abra a porta 20004 no Olá VM.<br/><br/> Windows tem de estar instalado na unidade de Olá C. disco do SO Olá deve ser básicas e não dinâmica. o disco de dados de Olá pode ser dinâmico.<br/><br/> Linux /etc/hosts ficheiros em VMs devem conter entradas que mapeiam Olá anfitrião local nome tooIP endereços associados a todos os adaptadores de rede. Olá, nome de anfitrião, pontos de montagem, nome do dispositivo, os caminhos de sistema e os nomes de ficheiros (/ etc; /usr) deve ser apenas em inglês.<br/><br/> Tipos específicos de [Linux armazenamento](site-recovery-support-matrix-to-azure.md#support-for-storage) são suportados.<br/><br/>Criar ou definir **disk.enableUUID=true** nas definições de VM Olá. Esta opção fornece um toohello UUID consistente VMDK, para que monta corretamente e assegura que as alterações de delta apenas são transferido back tooon local durante a reativação pós-falha, sem replicação completa.

## <a name="set-up-azure"></a>Configurar o Azure

1. [Configurar uma rede Azure](../virtual-network/virtual-networks-create-vnet-arm-pportal.md).
    - As VMs do Azure serão colocadas nesta rede quando são criados após a ativação pós-falha.
    - Pode configurar uma rede no [Resource Manager](../resource-manager-deployment-model.md), ou no modo clássico.

2. Configurar um [conta do storage do Azure](../storage/storage-create-storage-account.md#create-a-storage-account) para dados replicados.
    - conta de Olá pode ser padrão ou [premium](../storage/storage-premium-storage.md).
    - Pode configurar uma conta no Gestor de recursos, ou no modo clássico.

3. [Preparar uma conta](#prepare-for-automatic-discovery-and-push-installation) no Olá servidor vCenter ou anfitriões vSphere, por isso, esse Site Recovery pode detetar automaticamente as VMs de VMware.

## <a name="prepare-hello-configuration-server"></a>Preparar o servidor de configuração de Olá

1. Instale o Windows Server 2012 R2 ou posterior, numa VMware VM.
2. Certifique-se Olá VM tem acesso toohello URLs listados na [pré-requisitos](#prerequisites).
3. Instalar [VMware vSphere PowerCLI 6.0](https://my.vmware.com/web/vmware/details?productId=491&downloadGroup=PCLI600R1).


## <a name="prepare-for-automatic-discovery-and-push-installation"></a>Preparar para a instalação push e de deteção automática

- **Preparar uma conta de deteção automática**: servidor de processos de recuperação de Site Olá Deteta automaticamente as VMs. toodo, credenciais de necessidades de recuperação de sites que podem aceder a servidores vCenter e vSphere ESXi anfitriões.

    1. toouse uma conta dedicada, criar uma função (nível Olá vCenter, com estas [permissões](#vmware-account-permissions). Atribua um nome, tal como **Azure_Site_Recovery**.
    2. Em seguida, criar um utilizador no Olá vSphere anfitrião/servidor vCenter e atribua Olá função toohello utilizador. Especifique esta conta de utilizador durante a implementação da recuperação de Site.

- **Preparar uma Olá toopush de conta serviço de mobilidade**: Se pretender tooVMs de serviço de mobilidade de Olá toopush, precisa de uma conta que pode ser utilizada por Olá processo servidor tooaccess Olá VM. conta de Olá só é utilizada para a instalação de push Olá. Pode utilizar um domínio ou conta local:

    - Para o Windows, se não estiver a utilizar uma conta de domínio, terá de toodisable controlo de acesso de utilizador remoto no computador local Olá. toodo, Olá registar em **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System**, adicionar a entrada de DWORD Olá **LocalAccountTokenFilterPolicy**, com um valor de 1.
    - Se pretender que entrada de registo de Olá tooadd para Windows de um CLI, escreva:``REG ADD HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System /v LocalAccountTokenFilterPolicy /t REG_DWORD /d 1.``
    - Para Linux conta Olá deve ser a raiz no servidor de Linux Olá origem.

## <a name="create-a-recovery-services-vault"></a>Criar um cofre dos Serviços de Recuperação 

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]

## <a name="select-hello-protection-goal"></a>Selecione o objetivo de proteção de Olá

Selecione o que pretende tooreplicate, e onde pretende tooreplicate para.

1. Clique em **cofres dos serviços de recuperação** > cofre.
2. No Menu de recurso Olá, clique em **recuperação de Site** > **passo 1: preparar a infraestrutura** > **objetivo de proteção**.

    ![Selecione os objetivos](./media/site-recovery-vmware-to-azure/choose-goals.png)
3. No **objetivo de proteção**, selecione **tooAzure** > **Sim, com o VMware vSphere hipervisor**.

    ![Selecione os objetivos](./media/site-recovery-vmware-to-azure/choose-goals2.png)

## <a name="set-up-hello-source-environment"></a>Configurar o ambiente de origem Olá

Configurar o servidor de configuração de Olá, registe-o num cofre Olá e detetar VMs.

1. Clique em **recuperação de sites** > **passo 1: preparar infraestrutura** > **origem**.
2. Se não tiver um servidor de configuração, clique em **+ o servidor de configuração**.

    ![Configurar a origem](./media/site-recovery-vmware-to-azure/set-source1.png)
3. No **Adicionar servidor**, verifique se **servidor de configuração** aparece no **tipo de servidor**.
4. Transfira o ficheiro de instalação do programa de configuração do Site Recovery Unified Olá.
5. Transferir a chave de registo do cofre Olá. Isto tem quando executar a configuração do Unified. chave de Olá é válido durante cinco dias depois de gerá-la.

   ![Configurar a origem](./media/site-recovery-vmware-to-azure/set-source2.png)


## <a name="run-site-recovery-unified-setup"></a>Recuperação de Site execução Unified programa de configuração

Seguinte Olá antes de iniciar, em seguida, executar o servidor de configuração de Olá tooinstall Unified configuração, o servidor de processos de Olá e servidor de destino mestre Olá.
    - Obter uma descrição geral de vídeo

        > [!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video1-Source-Infrastructure-Setup/player]

    - No servidor de configuração de Olá VM, certifique-se de que o relógio do sistema Olá está sincronizado com um [hora Server](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service). Deve corresponder ao. Se estiver à frente 15 minutos ou para trás, a configuração poderá falhar.
    - Execute a configuração como um administrador Local no servidor de configuração de Olá VM.
    - Certifique-se de que TLS 1.0 está ativado no Olá VM.


[!INCLUDE [site-recovery-add-configuration-server](../../includes/site-recovery-add-configuration-server.md)]

> [!NOTE]
> Também pode ser instalado o servidor de configuração de Olá [partir da linha de comandos Olá](http://aka.ms/installconfigsrv).



### <a name="add-hello-account-for-automatic-discovery"></a>Adicionar a conta de Olá para a deteção automática

[!INCLUDE [site-recovery-add-vcenter-account](../../includes/site-recovery-add-vcenter-account.md)]

### <a name="connect-toovmware-servers"></a>Ligar servidores tooVMware

Ligar anfitriões ESXi de toovSphere ou servidores do vcenter Server, toodiscover VMs de VMware.

- Se adicionar Olá servidor vCenter ou anfitriões vSphere com uma conta sem privilégios de administrador no servidor de Olá, conta de Olá deve esses privilégios ativados:
    - Centro de dados, arquivo de dados, uma pasta, anfitrião, rede, recursos, Virtual machine, vSphere distribuídas comutador.
    - servidor do vCenter Olá necessita de permissões de vistas de armazenamento.
- Quando adiciona servidores VMware, pode demorar 15 minutos ou mais das mesmas tooappear no portal de Olá.
tooallow do Azure Site Recovery toodiscover máquinas virtuais em execução no seu ambiente no local, terá de tooconnect o servidor vCenter VMware ou vSphere ESXi anfitriões com a recuperação de Site.

Selecione **+ vCenter** toostart ligar um servidor VMware vCenter ou um anfitrião do VMware vSphere ESXi.

[!INCLUDE [site-recovery-add-vcenter](../../includes/site-recovery-add-vcenter.md)]

Recuperação de sites liga servidores tooVMware utilizar Olá especificadas as definições e Deteta as VMs.

## <a name="set-up-hello-target"></a>Configurar o destino de Olá

Antes de configurar o ambiente de destino Olá, certifique-se que tem um [conta do storage do Azure e da rede](#set-up-azure)

1. Clique em **preparar a infraestrutura** > **destino**, e selecione Olá pretende toouse de subscrição do Azure.
2. Especifique se o seu modelo de implementação de destino é baseado no Resource Manager ou clássico.
3. A Recuperação de Sites verifica que tem uma ou mais contas de armazenamento e redes do Azure compatíveis.

   ![destino](./media/site-recovery-vmware-to-azure/gs-target.png)
4. Se ainda não criou uma conta de armazenamento ou de rede, clique em **+ contas de armazenamento** ou **+ rede**, toocreate inline de rede ou a conta de Gestor de recursos.

## <a name="set-up-replication-settings"></a>Configurar as definições de replicação

Obter uma descrição geral do vídeo rápida antes de começar:
> [!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video2-vCenter-Server-Discovery-and-Replication-Policy/player]

1. toocreate uma nova política de replicação, clique em **infraestrutura de recuperação de Site** > **políticas de replicação** > **+ política de replicação**.
2. No **criar política de replicação**, especifique um nome de política.
3. No **limiar RPO**, especificar Olá RPO limite. Este valor Especifica com que frequência são criados pontos de recuperação de dados. É gerado um alerta se a replicação contínua excede este limite.
4. No **retenção do ponto de recuperação**, especifique o período de tempo (em horas) está janela de retenção de Olá para cada ponto de recuperação. VMs replicadas podem ser recuperados tooany ponto numa janela. Cópia de segurança too24 retenção horas é suportada em máquinas replicado toopremium armazenamento e 72 horas para armazenamento standard.
5. No **frequência de instantâneos consistentes com aplicação**, especifique com que frequência (em minutos) que contêm os instantâneos consistentes com aplicações de pontos de recuperação serão criados. Clique em **OK** política de Olá toocreate.

    ![Política de replicação](./media/site-recovery-vmware-to-azure/gs-replication2.png)
8. Quando cria uma nova política-lo automaticamente associado ao servidor de configuração de Olá. Por predefinição, uma política correspondente é criada automaticamente para reativação pós-falha. Por exemplo, se hello política de replicação é **rep política** política de reativação pós-falha Olá será **rep-política-reativação pós-falha**. Esta política não é utilizada depois de iniciar uma reativação pós-falha a partir do Azure.  



## <a name="plan-capacity"></a>Planear a capacidade

1. Agora que tem a infraestrutura configurada, pode pensar sobre o planeamento de capacidade e descobrir a necessidade de recursos adicionais. [Saiba mais](site-recovery-plan-capacity-vmware.md).
2. Quando tiver terminado com o planeamento de capacidade, selecione **Sim** no **concluiu o planeamento de capacidade?**

   ![Planeamento de capacidade](./media/site-recovery-vmware-to-azure/gs-capacity-planning.png)


## <a name="prepare-vms-for-replication"></a>Preparar as VMs para a replicação

Olá serviço de mobilidade tem de ser instalado em todas as VMs de VMware que pretende que o tooreplicate. Pode instalar o serviço de mobilidade Olá de diversas formas:

1. Instale com uma instalação push do servidor de processos de Olá. É necessário tooprepare VMs toouse este método.
2. Instalar utilizando as ferramentas de implementação, como o System Center Configuration Manager ou do Azure automation DSC.
3.  Instale manualmente.

[Saiba mais](site-recovery-vmware-to-azure-install-mob-svc.md)


## <a name="enable-replication"></a>Ativar a replicação

Antes de começar:

- A conta de utilizador do Azure tem toohave determinadas [permissões](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) tooenable replicação de um novo tooAzure de máquina virtual.
- Quando adiciona ou modifica as VMs, pode demorar até too15 minutos ou já está em vigor tootake de alterações e para os mesmos tooappear no portal de Olá.
- Pode verificar o tempo Olá pela última vez detetado para VMs no **servidores de configuração** > **último contacto em**.
- tooadd VMs sem aguardar deteção agendada do Olá, servidor de configuração de Olá realce (não clique nele) e clique em **atualizar**.
- Se uma VM está preparada para a instalação de push, o servidor de processos de Olá instala automaticamente o serviço de mobilidade Olá ao ativar a replicação.


### <a name="exclude-disks-from-replication"></a>Excluir discos da replicação

Por predefinição, todos os discos numa máquina são replicados. Pode excluir discos de replicação. Por exemplo, poderá pretender que os discos de tooreplicate com dados temporários ou dados que foi atualizada sempre que uma máquina ou aplicação reinicia (por exemplo pagefile.sys ou tempdb do SQL Server).

### <a name="replicate-vms"></a>Replicar VMs

Antes de começar, veja uma rápida descrição geral do vídeo

>[!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video3-Protect-VMware-Virtual-Machines/player]

1. Clique em **Passo 2: Replicar aplicação** > **Origem**.
2. No **origem**, selecione o servidor de configuração de Olá.
3. No **máquina tipo**, selecione **máquinas virtuais**.
4. No **vCenter/vSphere hipervisor**, selecione o servidor vCenter Olá que gere anfitriões vSphere de Olá ou selecione Olá anfitrião.
5. Selecione o servidor de processos de Olá. Se ainda não criou quaisquer servidores de processos adicionais este será o servidor de configuração de Olá. Em seguida, clique em **OK**.

    ![Ativar a replicação](./media/site-recovery-vmware-to-azure/enable-replication2.png)

6. No **destino**, selecione a subscrição de Olá e Olá o grupo de recursos em que pretende Olá toocreate pós-falha nas VMs. Escolha o modelo de implementação de Olá que pretende toouse no Azure (clássica ou recurso management), para Olá pós-falha nas VMs.


7. Selecione a conta de armazenamento do Azure de Olá que pretende toouse para replicar os dados. Se não quiser toouse uma conta que já configurou, pode criar um novo.

8. Selecione Olá Azure toowhich de rede e sub-rede VMs do Azure irá ligar, quando são criados após a ativação pós-falha. Selecione **configurar agora para as máquinas selecionadas**, tooapply Olá rede definição tooall máquinas selecionadas para proteção. Selecione **configurar mais tarde** tooselect Olá rede do Azure por máquina. Se não quiser toouse uma rede existente, pode criar uma.

    ![Ativar a replicação](./media/site-recovery-vmware-to-azure/enable-rep3.png)
9. No **máquinas virtuais** > **selecionar máquinas virtuais**, clique e selecione cada máquina que quiser tooreplicate. Só pode selecionar máquinas para as quais a replicação pode ser ativada. Em seguida, clique em **OK**.

    ![Ativar a replicação](./media/site-recovery-vmware-to-azure/enable-replication5.png)
10. No **propriedades** > **configurar propriedades**, selecione conta Olá que será utilizada pelo tooautomatically de servidor de processo Olá instalar o serviço de mobilidade Olá na máquina de Olá.
11. Por predefinição, todos os discos são replicados. Clique em **todos os discos** e desmarque todos os discos que não pretende tooreplicate. Em seguida, clique em **OK**. Pode definir propriedades VM adicionais mais tarde.

    ![Ativar a replicação](./media/site-recovery-vmware-to-azure/enable-replication6.png)
11. No **as definições de replicação** > **configurar as definições de replicação**, certifique-se de que Olá correta está selecionada a política de replicação. Se modificar uma política, as alterações serão aplicadas tooreplicating máquina e toonew máquinas.
12. Ativar **a consistência Multi VM** se pretender toogather máquinas para um grupo de replicação e especificar um nome para o grupo de Olá. Em seguida, clique em **OK**. Tenha em atenção que:

    * Computadores em grupos de replicação replicar em conjunto e tem partilhado pontos de recuperação consistentes com falhas e consistentes da aplicação quando efetuar a ativação pós-falha.
    * Recomendamos que pode reunir VMs e servidores físicos, para que estes espelhar as cargas de trabalho. Ativar a consistência de várias VMS pode afetar o desempenho da carga de trabalho e só deve ser utilizada se máquinas estiverem a executar Olá mesma carga de trabalho e necessitar de consistência.

    ![Ativar a replicação](./media/site-recovery-vmware-to-azure/enable-replication7.png)
13. Clique em **ativar a replicação**. Pode controlar o progresso de Olá **ativar proteção** da tarefa no **definições** > **tarefas** > **tarefas de recuperação de Site**. Depois de Olá **finalizar proteção** tarefa executa máquina Olá está preparada para ativação pós-falha.

### <a name="view-and-manage-vm-properties"></a>Ver e gerir propriedades da VM

Recomendamos que verifique Olá propriedades da VM e efetue as alterações, que é necessário.

1. Clique em **replicado itens** > e selecione Olá máquina. Olá **Essentials** painel mostra informações sobre o estado e as definições de máquinas.
2. No **propriedades**, pode ver a replicação e informações de ativação pós-falha para Olá VM.
3. No **computação e rede** > **propriedades de computação**, pode especificar o tamanho de nome e o destino da VM do Azure Olá. Modificar Olá nome toocomply com [requisitos do Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements) se for necessário.
4. Modificar as definições de rede de destino Olá, uma sub-rede e endereço IP que será atribuído toohello VM do Azure:

   - Pode definir o endereço IP de destino Olá.

    - Se não fornecer um endereço, Olá máquina a ativação pós-falha utilizará o DHCP.
    - Se definir um endereço que não está disponível na ativação pós-falha, a ativação pós-falha não funcionará.
    - Olá mesmo endereço IP de destino pode ser utilizado para ativação pós-falha de teste, se o endereço de Olá está disponível na rede de ativação pós-falha de teste de Olá.

   - número de Olá dos adaptadores de rede é ditado pelo tamanho de Olá especificado para a máquina virtual de destino Olá:

     - Se Olá o número de adaptadores de rede na máquina de origem Olá é Olá igual ou inferior ao número de Olá de adaptadores permitido para o tamanho da máquina de destino Olá, em seguida, terá de destino Olá Olá o mesmo número de adaptadores que origem Olá.
     - Se número de Olá de adaptadores Olá máquina virtual de origem exceder o número de Olá permitido para o tamanho de destino Olá, será utilizado o tamanho máximo de Olá destino.
     - Por exemplo, se uma máquina de origem tiver dois adaptadores de rede e tamanho da máquina Olá destino suporta quatro, a máquina de destino Olá terá dois adaptadores. Se Olá máquina de origem tiver dois adaptadores, mas hello tamanho de destino só suporta um computador de destino Olá terá apenas um adaptador.     
   - Se a máquina virtual de Olá tem vários adaptadores de rede, todos serão ligados toohello mesma rede.
   - Se a máquina virtual de Olá tem vários adaptadores de rede, em seguida, Olá primeiro mostrado na lista de Olá torna-se Olá *predefinido* adaptador de rede no Olá máquina virtual do Azure.
4. No **discos**, pode ver o sistema de operativo Olá VM e os dados de Olá discos que será replicada.

#### <a name="managed-disks"></a>Managed disks

No **computação e rede** > **propriedades de computação**, pode definir "utilização gerido por discos" definição demasiado "Sim" para Olá VM se pretender que tooattach discos geridos tooyour máquina no tooAzure de ativação pós-falha. Discos geridos simplifica a gestão de discos para VMs IaaS do Azure ao gerir contas do storage Olá associadas aos discos VM Olá. [Saiba mais sobre discos geridos.](https://docs.microsoft.com/en-us/azure/storage/storage-managed-disks-overview)

   - Discos geridos são criados e ligados toohello máquina de virtual apenas em tooAzure uma ativação pós-falha. Ativar a proteção, dados de máquinas no local irão continuar tooreplicate toostorage contas.  Discos geridos podem ser criados apenas para máquinas virtuais implementadas com o modelo de implementação do Olá Resource manager.  

   - Quando definir "utilização gerido por discos" demasiado "Sim", apenas conjuntos de disponibilidade no grupo de recursos de Olá com "utilização gerido por discos" definido demasiado "Sim" seria disponíveis para seleção. Isto acontece porque as máquinas virtuais com discos geridos podem apenas ser parte de conjuntos de disponibilidade com o conjunto de propriedade de "Utilize gerido discos" demasiado "Sim". Certifique-se que crie conjuntos de disponibilidade com o conjunto de propriedade de "Utilize gerido discos" com base nos seus discos toouse intenção gerido na ativação pós-falha.  Da mesma forma, quando definir "utilização gerido por discos" demasiado "não", apenas conjuntos de disponibilidade no grupo de recursos de Olá com a propriedade "utilização gerido por discos" definida demasiado "não" seria disponíveis para seleção. [Saiba mais sobre os discos geridos e os conjuntos de disponibilidade](https://docs.microsoft.com/en-us/azure/virtual-machines/windows/manage-availability#use-managed-disks-for-vms-in-an-availability-set).

  > [!NOTE]
  > Se a conta de armazenamento de Olá utilizada para a replicação foi encriptada com encriptação do serviço de armazenamento em qualquer ponto no tempo, a criação de discos geridos durante a ativação pós-falha irá falhar. Pode definir "utilização gerido por discos" demasiado "não" e repita a ativação pós-falha ou desative a proteção para a máquina virtual de Olá e protegê-lo tooa conta de armazenamento que não tinha ativada em qualquer ponto no tempo de encriptação do serviço de armazenamento.
  > [Saiba mais sobre a Encriptação do Serviço de Armazenamento e os discos geridos](https://docs.microsoft.com/en-us/azure/storage/storage-managed-disks-overview#managed-disks-and-encryption).


## <a name="run-a-test-failover"></a>Executar uma ativação pós-falha de teste


Depois de que configurou tudo, execute um toomake de ativação pós-falha de teste se que tudo está a funcionar conforme esperado. Obter uma descrição geral do vídeo rápida antes de começar
>[!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video4-Recovery-Plan-DR-Drill-and-Failover/player]


1. toofail através de uma única máquina no **definições** > **itens replicados**, clique em Olá VM > **+ ativação pós-falha de teste** ícone.

    ![Ativação pós-falha de teste](./media/site-recovery-vmware-to-azure/TestFailover.png)

1. Planear toofail através de uma recuperação, na **definições** > **planos de recuperação**, plano do contexto Olá > **ativação pós-falha de teste**. toocreate um plano de recuperação, [siga estas instruções](site-recovery-create-recovery-plans.md).  

1. No **ativação pós-falha de teste**, selecione Olá rede Azure toowhich VMs do Azure será ligada após a ocorrência da ativação pós-falha.

1. Clique em **OK** toobegin ativação pós-falha de Olá. Pode controlar o progresso clicando na Olá VM tooopen as respetivas propriedades ou na Olá **ativação pós-falha de teste** tarefa no nome do cofre > **definições** > **tarefas**  >  **As tarefas de recuperação de site**.

1. Após a conclusão da ativação pós-falha de Olá, também deve ser capaz de réplica de Olá toosee máquina do Azure são apresentados no Olá portal do Azure > **máquinas virtuais**. Deve Certifique-se de que Olá VM é Olá um tamanho adequado, que tenha ligado toohello adequada de rede, e que está em execução.

1. Se lhe [preparou para as ligações após a ativação pós-falha](site-recovery-test-failover-to-azure.md#prepare-to-connect-to-azure-vms-after-failover), deve ser capaz de tooconnect toohello VM do Azure.

1. Quando tiver terminado, clique em **ativação pós-falha de teste de limpeza** no plano de recuperação Olá. No **notas**, registar e guardar todas as observações associadas à ativação pós-falha de teste de Olá. Este procedimento eliminará Olá VMs que foram criadas durante a ativação pós-falha de teste.

[Saiba mais](site-recovery-test-failover-to-azure.md) sobre as ativações pós-falha de teste.


## <a name="vmware-account-permissions"></a>Permissões de conta de VMware

Recuperação de sites tem acesso tooVMware para tooautomatically de servidor de processo Olá detetar VMs e ativação pós-falha e a reativação pós-falha de VMs.

- **Migrar**: Se pretender que apenas toomigrate tooAzure de VMs de VMware, sem nunca voltar a falhá-los, pode utilizar uma conta do VMware com uma função só de leitura. Este tipo uma função pode executar a ativação pós-falha, mas não é possível encerrar máquinas de origem protegida. Esta operação não é necessária para a migração.
- **Replicar/recuperar**: Se pretender que a conta de Olá de replicação completo (replicar ativação pós-falha, a reativação pós-falha) toodeploy tem de ser capaz de toorun operações, tais como criar e remoção de discos, ligar as VMs etc.
- **A deteção automática**: é necessária, pelo menos, uma conta de só de leitura.


**Tarefa** | **Conta/função necessários** | **Permissões** | **Detalhes**
--- | --- | --- | ---
**Servidor de processos Deteta automaticamente as VMs de VMware** | Precisa de, pelo menos, um utilizador só de leitura | Objeto de centro de dados –> Propagate tooChild objeto, função = só de leitura | Utilizador atribuído ao nível do datacenter e tem acesso tooall Olá objetos no Centro de dados de Olá.<br/><br/> acesso de toorestrict, atribuir Olá **sem acesso** função com Olá **propagar toochild** objeto toohello objetos de subordinados (anfitriões vSphere, datastores, VMs e as redes).
**Ativação pós-falha** | Precisa de, pelo menos, um utilizador só de leitura | Objeto de centro de dados –> Propagate tooChild objeto, função = só de leitura | Utilizador atribuído ao nível do datacenter e tem acesso tooall Olá objetos no Centro de dados de Olá.<br/><br/> acesso de toorestrict, atribuir Olá **sem acesso** função com Olá **propagar toochild** objeto toohello objetos de subordinados (anfitriões vSphere, datastores, VMs e as redes).<br/><br/> Útil para fins de migração, mas não completa replicação, ativação pós-falha, reativação pós-falha.
**Ativação pós-falha e a reativação pós-falha** | Sugerimos que cria uma função (Azure_Site_Recovery) com permissões de Olá necessário e, em seguida, atribuir Olá função tooa VMware utilizador ou grupo | Objeto de centro de dados –> Propagate tooChild objeto, função = Azure_Site_Recovery<br/><br/> Arquivo de dados -> atribuir espaço em, procurar o arquivo de dados, as operações de baixo nível de ficheiro, remova o ficheiro, atualizar ficheiros de máquina virtual<br/><br/> Rede -> atribuição de rede<br/><br/> Recursos -> o conjunto de tooresource atribuir VM, migrar alimentado desligar a VM, migrar alimentado na VM<br/><br/> Tarefas -> tarefas de criação, a tarefa de atualização<br/><br/> Configuração -> de máquina virtual<br/><br/> Máquina virtual -> interagir -> pergunta de resposta, a ligação de dispositivos, configurar suporte de dados do CD, configurar o suporte de dados de disquetes, desligar, ligar, instalação de ferramentas do VMware<br/><br/> Máquina virtual -> inventário -> criar, registar, anular o registo<br/><br/> Máquina virtual -> aprovisionamento -> Permitir transferências de máquina virtual, permitem carregar ficheiros de máquina virtual<br/><br/> Máquina virtual -> instantâneos -> Remover instantâneos | Utilizador atribuído ao nível do datacenter e tem acesso tooall Olá objetos no Centro de dados de Olá.<br/><br/> acesso de toorestrict, atribuir Olá **sem acesso** função com Olá **propagar toochild** objeto toohello objetos de subordinados (anfitriões vSphere, datastores, VMs e as redes).


## <a name="next-steps"></a>Passos seguintes

Depois de obter replicação cópias de segurança e em execução, quando ocorre uma falha falhar tooAzure e as VMs do Azure são criadas a partir dos dados de Olá replicado. Pode, em seguida, aceder a cargas de trabalho e aplicações do Azure, até falhar localização primária de back-tooyour quando se retomam as operações de toonormal.

- [Saiba mais](site-recovery-failover.md) sobre os diferentes tipos de ativações pós-falha e como toorun-los.
- Se estiver a migrar máquinas em vez de replicar e a falhar back, [ler mais](site-recovery-migrate-to-azure.md#migrate-on-premises-vms-and-physical-servers).
- [Leia sobre a reativação pós-falha](site-recovery-failback-azure-to-vmware.md), toofail back e replicar as VMs do Azure fazer uma cópia toohello primário site no local.

## <a name="third-party-software-notices-and-information"></a>Informações e avisos de software de terceiros
Não traduzir ou localizar

software Olá e firmware em execução no Olá produto da Microsoft ou de serviço baseia-se no incorpora material de Olá projetos listados abaixo (coletivamente designados por "código de terceiros").  A Microsoft está Olá autor não original de Olá código de terceiros.  Aviso de direitos original Olá e licenciamento, sob a qual a Microsoft recebido desse código de terceiros, estão definidos especificado abaixo.

informações Olá secção A estão sobre o código de terceiros componentes de projetos de Olá listados abaixo. Essas licenças e as informações são fornecidas apenas para fins informativos.  Este código de terceiros está a ser tooyou relicensed pela Microsoft em termos de licenciamento Olá Microsoft produto ou serviço de licenciamento de software da Microsoft.  

informações de Olá na secção B é sobre componentes de código de terceiros que estão a ser efetuados tooyou disponível pela Microsoft em termos de licenciamento original Olá.

ficheiro completo Olá pode ser encontrado no Olá [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=529428). Microsoft reserva-se a todos os direitos que não estejam expressamente concedidos neste documento, seja por implicação, preclusão ou, caso contrário.
