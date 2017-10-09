---
title: aaaFailback VMs de VMware tooon local do Azure | Microsoft Docs
description: "Saiba mais sobre o site no local de back-toohello a falhar após a ativação pós-falha de VMs de VMware e servidores físicos tooAzure."
services: site-recovery
documentationcenter: 
author: ruturaj
manager: mkjain
editor: 
ms.assetid: 5a47337f-89a9-43e8-8fdc-7da373c0fb0f
ms.service: site-recovery
ms.devlang: na
ms.tgt_pltfrm: na
ms.topic: article
ms.workload: storage-backup-recovery
ms.date: 03/27/2017
ms.author: ruturajd
ms.openlocfilehash: 258f5a55252083135b2040e5a235fa1ffbf3b9d0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="fail-back-vmware-virtual-machines-and-physical-servers-toohello-on-premises-site"></a>Falhar back-máquinas de virtuais de VMware e site do servidores físicos toohello no local


Este artigo descreve como toofailback Azure máquinas virtuais a partir do site do Azure toohello no local. Siga as instruções de Olá aqui quando estiver pronto toofail novamente as máquinas virtuais VMware ou servidores físicos do Windows ou Linux depois da proteger as máquinas com este [referência](site-recovery-how-to-reprotect.md).

>[!NOTE]
>Se estiver a utilizar o portal clássico do Azure Olá, consulte tooinstructions mencionado [aqui](site-recovery-failback-azure-to-vmware-classic.md) arquitetura de tooAzure VMware avançado e [aqui](site-recovery-failback-azure-to-vmware-classic-legacy.md) para arquitetura herdada Olá

## <a name="overview"></a>Descrição geral
diagramas de Olá nesta secção mostram a arquitetura de reativação pós-falha Olá para este cenário.

Ao hello do servidor de processos for no local e estiver a utilizar uma ligação ExpressRoute do Azure, utilize esta arquitetura:

![Diagrama de arquitetura para o ExpressRoute](./media/site-recovery-failback-azure-to-vmware-classic/architecture.png)

Quando Olá servidor de processos está no Azure e têm uma VPN ou uma ligação ExpressRoute, utilize esta arquitetura:

![Diagrama de arquitetura para VPN](./media/site-recovery-failback-azure-to-vmware-classic/architecture2.png)

Para obter uma lista completa das portas e diagrama de arquitetura de reativação pós-falha Olá, consulte toohello seguinte imagem:

![Lista de reativação pós-falha de ativação pós-falha de todas as portas](./media/site-recovery-failback-azure-to-vmware-classic/Failover-Failback.png)

Depois de ter a efetuar a ativação pós-falha tooAzure, falhar site no local de back-tooyour em três fases:

* **Fase 1**: Proteja as VMs do Azure de Olá, de modo a que são iniciados replicar VMs de VMware back toohello que estejam a executar no seu site no local.
* **Fase 2**: depois das suas VMs do Azure site no local de tooyour replicados, executar um toofail de ativação pós-falha novamente a partir do Azure.
* **Fase 3**: depois dos dados falhou novamente, proteja Olá VMs no local não conseguiu fazer uma cópia, para que possam iniciar a replicação tooAzure.

### <a name="fail-back-toohello-original-location-or-an-alternate-location"></a>Falhar back toohello a localização original ou uma localização alternativa
Após a ativação pós-falha numa VM de VMware, pode falhar back toohello mesma VM de origem caso ainda exista no local. Neste cenário, apenas os deltas de Olá foi novamente.

Se a ativação pós-falha servidores físicos, a reativação pós-falha é sempre tooa nova VM de VMware. Antes de voltar a falhar um computador físico, tenha em atenção que:
* Um computador físico protegido regressará como uma máquina virtual quando esta é a ativação pós-falha novamente a partir do tooVMware do Azure. Um computador físico do Windows Server 2008 R2 SP1, se está protegido e efetuar a ativação pós-falha tooAzure, não é possível efetuar a novamente. Uma máquina de Windows Server 2008 R2 SP1 que foi iniciado como uma máquina virtual no local será capaz de toofail back.
* Certifique-se de que detetar, pelo menos, um servidor de destino mestre juntamente com Olá necessários anfitriões ESX/ESXi terá toofail novamente para.

Se falhar back toohello original VM, Olá seguem-se necessário:

* Se hello VM for gerida por um servidor vCenter, hello anfitrião do ESX de destino principal deve ter o arquivo de dados do acesso toohello VMs.
* Se hello VM está num anfitrião ESX, mas não é gerida pelo vCenter, de disco rígido Olá Olá VM tem de ser no arquivo de dados que seja acessível pelo anfitrião Olá do MT.
* Se a VM num anfitrião do ESX e não utilize o vCenter, deve efetuar a deteção de anfitrião do ESX Olá de Olá MT antes que voltar a proteger. Isto aplica-se se está a reativar demasiado servidores físicos novamente.
* Outra opção (se Olá no local encontra VM) é toodelete-lo antes de efetuar uma reativação pós-falha. Reativação pós-falha, em seguida, cria uma nova VM em Olá mesmo anfitrião como anfitrião do ESX Olá destino mestre.

Quando houver uma localização alternativa back tooan, os dados de Olá são toohello recuperado mesmo arquivo de dados e Olá mesmo anfitrião ESX que foi utilizado pelo servidor de destino mestre Olá no local.

## <a name="prerequisites"></a>Pré-requisitos
* toofail back VMs de VMware e servidores físicos, precisa de um ambiente VMware. A falhar back tooa servidor físico não é suportado.
* toofail novamente, tem tiver criado uma rede do Azure quando configurar inicialmente a proteção. Reativação pós-falha necessita de uma ligação VPN ou ExpressRoute do Azure de Olá rede na qual Olá VMs do Azure são site do toohello localizados no local.
* Se hello VMs que pretende que o toofail uma tooare gerido por um servidor vCenter, certifique-se de que tem permissões de Olá necessário para a deteção de VMs nos servidores do vCenter. Para obter mais informações, consulte [máquinas virtuais VMware replicar e servidores físicos tooAzure com o Azure Site Recovery](site-recovery-vmware-to-azure-classic.md).
* Se existirem instantâneos numa VM, irá falhar. Pode eliminar os instantâneos de Olá ou discos Olá.
* Antes de falhar novamente, crie estes componentes:
  * **Criar um servidor de processos no Azure**. Este componente é uma VM do Azure que criar e manter em execução durante a reativação pós-falha. Pode eliminar Olá VM após a conclusão da reativação pós-falha.
  * **Criar um servidor de destino mestre**: servidor de destino mestre Olá envia e recebe dados de reativação pós-falha. servidor de gestão de Olá que criou no local tem um servidor de destino principal está instalado por predefinição. No entanto, consoante o volume de Olá de tráfego de cópia falhou, poderá ser necessário toocreate um servidor de destino principal separado para reativação pós-falha.
  * toocreate um servidor de destino mestre adicional que é executado no Linux, configurar Olá VM com Linux antes de instalar o servidor de destino mestre Olá, conforme descrito mais tarde.
* Um servidor de configuração é necessário no local quando fizer uma reativação pós-falha. Durante a reativação pós-falha, máquina virtual de Olá tem de existir na base de dados de servidor de configuração de Olá. Se a base de dados de servidor de configuração de Olá não contém nenhuma VM, reativação pós-falha não teve êxito. Por conseguinte, certifique-se de que efetue cópias de segurança agendadas regulares do seu servidor. Um desastre, terá de toorestore com Olá mesmo IP endereços, que reativação pós-falha funciona.
* Definir a definição de disk.enableUUID=true Olá **parâmetros de configuração** do mestre de Olá de destino VM do VMware. Se esta linha não existir, adicioná-lo. Esta definição é necessária tooprovide um consistente Identificador universalmente exclusivo (UUID) toohello disco (VMDK) ficheiro da máquina virtual para que este se encontra instalado corretamente.
* Lembre-se de um "mestre de servidor de destino não pode ser armazenamento vMotioned" condição, o que pode fazer com que Olá toofail de reativação pós-falha. Olá VM não é possível detetar um porque discos Olá não são efetuados tooit disponível.
* Adicione uma unidade, denominada uma unidade de retenção, no servidor de destino mestre Olá. Adicione um disco e formatar a unidade de Olá.

## <a name="failback-policy"></a>Política de reativação pós-falha
tooreplicate back tooon local, terá de uma política de reativação pós-falha. política de Olá é criada automaticamente quando criar uma política de direção direta e é automaticamente associado ao servidor de configuração de Olá. Não é editável. política de Olá tem Olá seguir as definições de replicação:

* Limiar RPO = 15 minutos
* Retenção do ponto de recuperação = 24 horas
* Frequência de instantâneos de consistência da aplicação = 60 minutos

 ![Definições de replicação da política de reativação pós-falha Olá](./media/site-recovery-failback-azure-to-vmware-new/failback-policy.png)

## <a name="set-up-a-process-server-in-azure"></a>Configurar um servidor de processos no Azure
Instale um servidor de processos no Azure, para que as VMs do Azure de Olá possa enviar o servidor de destino principal do Olá dados back toohello no local.

Se proteger as máquinas virtuais como recursos Clássicos (ou seja, Olá recuperada VM no Azure é uma VM que foi criada utilizando o modelo de implementação clássica Olá), precisa de um servidor de processos no Azure. Se tiver recuperado Olá VMs com o Azure Resource Manager como tipo de implementação de Olá, hello do servidor de processos tem de ter o Gestor de recursos como tipo de implementação de Olá. Olá tipo de implementação está selecionado por Olá Azure rede virtual que implementar Olá servidor de processos para.

1. No **cofre** > **definições** > **infraestrutura de recuperação de sites** (em **gerir**) > **Servidores de configuração** (em **para VMware e máquinas físicas**), selecione o servidor de configuração de Olá.
2. Clique em **processar servidor**.

  ![Botão de servidor de processo](./media/site-recovery-failback-azure-to-vmware-classic/add-processserver.png)
3. Escolha toodeploy hello do servidor de processos como **implementar uma servidor de processos no Azure do reativação pós-falha**.
4. Selecione a subscrição de Olá que tiver recuperado Olá VMs.
5. Selecione Olá rede do Azure que tiver recuperado Olá VMs. Olá toobe necessidades de servidor de processos no Olá que mesmo de rede para que Olá recuperados VMs e hello servidor de processos possam comunicar.
6. Se tiver selecionado um *modelo de implementação clássica* de rede, crie uma VM através de Olá Azure Marketplace e, em seguida, instalar hello do servidor de processos no mesmo.

 ![janela de "Adicionar servidor de processos" Olá](./media/site-recovery-failback-azure-to-vmware-classic/add-classic.png)

 Como estiver a criar hello do servidor de processos, paga seguinte de toohello atenção:
 * o nome da imagem de Olá Olá é *V2 de servidor do Microsoft Azure Site Recovery processo*. Selecione **clássico** como modelo de implementação de Olá.

       ![Select "Classic" as hello Process Server deployment model](./media/site-recovery-failback-azure-to-vmware-classic/templatename.png)
 * Instalar Olá servidor de processos de acordo com toohello instruções [máquinas virtuais VMware replicar e servidores físicos tooAzure com o Azure Site Recovery](site-recovery-vmware-to-azure-classic.md).
7. Se selecionar Olá *Resource Manager* Azure de rede, implementar hello do servidor de processos, fornecendo Olá seguintes informações:

  * nome de Olá Olá do grupo de recursos que pretende que o servidor de Olá toodeploy para
  * nome de Hello do servidor de Olá
  * Um nome de utilizador e palavra-passe para iniciar sessão no servidor de toohello
  * conta de armazenamento de Olá que pretende que toodeploy Olá servidor
  * a sub-rede de Olá e interface de rede de Olá que pretende que o tooconnect tooit
   >[!NOTE]
   >Tem de criar os seus próprios [interface de rede](../virtual-network/virtual-networks-multiple-nics.md) (NIC) e selecione-a durante a implementação de hello do servidor de processos.

    ![Introduza as informações na caixa de diálogo de "Adicionar servidor de processos" Olá](./media/site-recovery-failback-azure-to-vmware-classic/psinputsadd.png)

8. Clique em **OK**. Esta ação aciona uma tarefa que cria uma máquina virtual de tipo de implementação de Gestor de recursos durante a configuração do servidor de processos de Olá. tooregister Olá servidor toohello configuração configuração do servidor, execute Olá dentro Olá VM ao seguir as instruções Olá [máquinas virtuais VMware replicar e servidores físicos tooAzure com o Azure Site Recovery](site-recovery-vmware-to-azure-classic.md). Também é acionado um Olá toodeploy de tarefa servidor de processos.

  Olá servidor de processos está listado no Olá **servidores de configuração** > **associados a servidores** > **servidores de processos** separador.

    ![](./media/site-recovery-failback-azure-to-vmware-new/pslistingincs.png)

    > [!NOTE]
    > Olá servidor de processos não estão visível em **propriedades VM**. É visível apenas Olá **servidores** separador no servidor de gestão de Olá que é registado. Pode demorar 10 minutos too15 Olá tooappear de servidor de processos.


## <a name="set-up-hello-master-target-server-on-premises"></a>Configurar Olá destino mestre server no local
servidor de destino mestre Olá recebe dados de reativação pós-falha Olá. servidor Olá é automaticamente instalado no servidor de gestão do Olá no local, mas se está a reativar novamente excesso de dados, poderá ter de tooset configurar um servidor de destino mestre adicionais. tooset segurança um mestre no local do servidor de destino, Olá a seguir:

> [!NOTE]
> tooset configurar um servidor de destino principal no Linux, ignorar toohello próximo procedimento. Utilize apenas CentOS 6.6 sistema operativo mínimo como Olá SO de destino principal.

1. Se estiver a configurar o servidor de destino mestre Olá no Windows, abra a página de início rápido Olá de Olá VM estiver a instalar o servidor de destino mestre Olá num.
2. Transfira o ficheiro de instalação de Olá de Assistente de configuração de unificada do Azure Site Recovery Olá.
3. Execute a configuração de Olá e, em **antes de começar**, selecione **adicionar tooscale de servidores de processos adicional saída implementação**.
4. Assistente de Olá completa no Olá mesma forma que fez quando [configurar o servidor de gestão de Olá](site-recovery-vmware-to-azure-classic.md). No Olá **detalhes do servidor de configuração** página, especifique o endereço IP de hello do servidor de destino mestre Olá e introduza Olá de tooaccess uma frase de acesso VM.

### <a name="set-up-a-linux-vm-as-hello-master-target-server"></a>Configurar uma VM com Linux como servidor de destino mestre Olá
tooset segurança do servidor de gestão de Olá com o servidor de destino mestre Olá como uma VM com Linux, instalar o sistema operativo mínimo do Olá CentOS 6.6. Em seguida, obter Olá os IDs de SCSI para cada disco de rígido SCSI, instalar alguns pacotes adicionais e aplicam-se algumas alterações personalizadas.

#### <a name="install-centos-66"></a>Instalar CentOS 6.6

1. Instale o sistema operativo mínimo do Olá CentOS 6.6 no servidor de gestão de Olá VM. Manter Olá ISO numa unidade de DVD e Olá sistema de arranque. Ignore Olá suporte de dados de teste. Selecione **inglês** como linguagem de Olá, selecione **básico dispositivos de armazenamento**, verifique se o disco rígido de Olá não tem quaisquer dados importantes, clique em **Sim**e eliminar quaisquer dados. Introduza o nome de anfitrião Olá hello do servidor de gestão e selecione o adaptador de rede do servidor de Olá.  No Olá **editar sistema** caixa de diálogo, selecione **ligar automaticamente**e, em seguida, adicione um endereço IP estático, rede e as definições de DNS. Especifique um fuso horário. tooaccess Olá servidor de gestão, introduza a palavra-passe de raiz de Olá.
2. Quando estiver a lhe for perguntado que tipo de instalação que pretende, selecione **criar esquema de personalizado** como partição de Olá. Clique em **Seguinte**. Selecione **livres**e, em seguida, clique em **criar**. Criar  **/** , **/var/falhas**, e **/partições de casa** com **FS tipo:** **ext4**. Criar a partição de troca de Olá como **FS tipo: troca**.
3. Se forem encontrados dispositivos já existentes, é apresentada uma mensagem de aviso. Clique em **formato** unidade de Olá tooformat com definições de partição Olá. Clique em **escrita alterar toodisk** alterações de partição de Olá tooapply.
4. Selecione **carregador de arranque de instalação** > **seguinte** carregador de arranque Olá tooinstall na partição de raiz de Olá.
5. Quando Olá instalação estiver concluída, clique em **reiniciar**.

#### <a name="retrieve-hello-scsi-ids"></a>Obter os IDs de SCSI Olá

1. Após a instalação de Olá, obter Olá IDs de SCSI para cada disco de rígido SCSI de Olá VM. toodo encerrado por isso, o servidor de gestão de Olá VM. Nas propriedades VM de Olá no VMware, faça duplo clique entrada VM Olá > **editar definições de** > **opções**.
2. Selecione **avançadas** > **item geral**e, em seguida, clique em **parâmetros de configuração**. Esta opção não está disponível quando Olá máquina está em execução. Para Olá toobe de opção disponível, Olá máquina tem de ser encerrada.
3. Efetue um dos seguintes Olá:
 * Se hello linha **disco. EnableUUID** existe, certifique-se de que o valor de Olá está definido demasiado**verdadeiro** (sensível às maiúsculas e). Se o valor de Olá já está definida tooTrue, pode cancelar e testar o comando de SCSI Olá dentro de um sistema operativo convidado depois for iniciado.
 * Se hello linha **disco. EnableUUID** não existe, clique em **linha adicionar**e, em seguida, adicioná-la com Olá **verdadeiro** valor. Não utilize aspas duplas.

#### <a name="install-additional-packages"></a>Instalar pacotes adicionais
Transferir e instalar pacotes adicionais.

1. Certifique-se o servidor de destino mestre Olá toohello ligado à Internet.
2. toodownload e instalar 15 pacotes do repositório de CentOS Olá, execute este comando: `# yum install –y xfsprogs perl lsscsi rsync wget kexec-tools`.
3. Se máquinas de origem Olá proteger executam Linux com um Reiser ou XFS sistema para o dispositivo de arranque ou raiz Olá de ficheiros, transferir e instalar pacotes adicionais da seguinte forma:

   * \#CD /usr/local
   * \#wget [http://elrepo.org/linux/elrepo/el6/x86_64/RPMS/kmod-reiserfs-0.0-1.el6.elrepo.x86_64.rpm](http://elrepo.org/linux/elrepo/el6/x86_64/RPMS/kmod-reiserfs-0.0-1.el6.elrepo.x86_64.rpm)
   * \#wget [http://elrepo.org/linux/elrepo/el6/x86_64/RPMS/reiserfs-utils-3.6.21-1.el6.elrepo.x86_64.rpm](http://elrepo.org/linux/elrepo/el6/x86_64/RPMS/reiserfs-utils-3.6.21-1.el6.elrepo.x86_64.rpm)
   * \#reiserfs de kmod-reiserfs 0,0 1.el6.elrepo.x86_64.rpm da – ivh rpm-utils-3.6.21-1.el6.elrepo.x86_64.rpm
   * \#wget [http://mirror.centos.org/centos/6.6/os/x86_64/Packages/xfsprogs-3.1.1-16.el6.x86_65.rpm](http://mirror.centos.org/centos/6.6/os/x86_64/Packages/xfsprogs-3.1.1-16.el6.x86_65.rpm)
   * \#rpm – ivh xfsprogs-3.1.1-16.el6.x86_64.rpm
   * \#yum instalar mapeador-dispositivo-multipath (tooenable necessário multipath pacotes no servidor de destino mestre Olá)

#### <a name="apply-custom-changes"></a>Aplicar alterações personalizadas
Após concluir os passos de pós-instalação Olá e pacotes de Olá instalado, aplicar alterações personalizadas, Olá seguinte:

1. Copie Olá agente Unified do RHEL 6-64 binário toohello VM. Olá de toountar binário, execute este comando: `tar –zxvf <file name>`.
2. permissões de toogive, execute este comando: `# chmod 755 ./ApplyCustomChanges.sh`.
3. Execute hello seguintes script: `# ./ApplyCustomChanges.sh`. Execute apenas uma vez. Depois de ser executado com êxito, reinicie o servidor de Olá.

## <a name="run-hello-failback"></a>Execute a reativação pós-falha da Olá
### <a name="reprotect-hello-azure-vms"></a>Proteja as VMs do Azure de Olá
1. No **cofre**, na **replicado itens**, faça duplo clique Olá VM que tenha sido efetuada a ativação pós-falha e, em seguida, selecione **voltar a proteger**.
2. No painel de Olá, pode ver essa direção Olá de proteção **tooOn local do Azure** já está selecionada.
3. No **servidor de destino mestre** e **servidor de processos**, selecione o servidor de destino mestre no local Olá e hello do servidor de processos de VM do Azure.
4. Selecione Olá arquivo de dados que pretende que os discos de Olá toorecover no local para. Utilize esta opção quando Olá no local VM é eliminada e terá de toocreate novos discos. Ignore a opção de Olá se hello discos já existirem, mas continua a precisar de toospecify um valor.
5. Utilize uma retenção unidade toostop Olá pontos no tempo quando Olá VM é replicado back tooon local. Alguns dos critérios de uma unidade de retenção estão listados aqui. Sem estes critérios, unidade de Olá não é listada para o servidor de destino mestre Olá.

  * Volume não deve estar a ser utilizada para qualquer outra finalidade (destino de replicação e assim sucessivamente).
  * O volume não deve estar no modo de bloqueio.
  * O volume não deve ser o volume de cache. (instalação de destino mestre Olá não deve existir nesse volume. Olá, servidor de processos e o mestre de volume de instalação personalizada de destino não é elegível para o volume de retenção. Aqui, Olá instalado o servidor de processos e o volume de destino principal é o volume de cache de Olá de destino mestre Olá.)
  * tipo de sistema de ficheiros de volume Olá não deve ser FAT e FAT32.
  * capacidade do volume Olá deve ser diferente de zero.
  * volume de retenção Olá predefinido para o Windows é o volume de R.
  * volume de retenção predefinido Olá para Linux é /mnt/retention.

6. política de reativação pós-falha Olá é selecionada automaticamente.
7. Depois de clicar em **OK** toobegin só, uma tarefa começa tooreplicate Olá VM a partir do site do Azure toohello no local. Pode controlar o progresso de Olá no Olá **tarefas** separador.

Se pretender que a localização alternativa de tooan toorecover, selecione a unidade de retenção de Olá e arquivo de dados que estão configurados para o servidor de destino mestre Olá. Quando não conseguem site no local de back-toohello, Olá VMs de VMware no plano de proteção de reativação pós-falha Olá utilizar Olá mesmo arquivo de dados como servidor de destino mestre Olá. Se quiser toorecover Olá réplica VM do Azure toohello mesmo local VM, Olá no local VM deve já estar em Olá mesmo arquivo de dados como servidor de destino mestre Olá. Se não houver nenhuma VM no local, é criado um novo durante só.

![Selecione "Azure tooon. local" no menu pendente de Olá](./media/site-recovery-failback-azure-to-vmware-new/reprotectinputs.png)

Também pode voltar a proteger um nível de plano de recuperação. Se tiver um grupo de replicação, pode Proteja-utilizando apenas a um plano de recuperação. Quando voltar a proteger através da utilização de um plano de recuperação, utilize valores anterior Olá para cada máquina protegida.

> [!NOTE]
> Grupos de replicação devem ser protegidos com o Olá mesmo destino mestre. Se estes estiverem protegidos com o servidores de destino mestre diferente, um ponto no tempo comuns não é possível determinar para os mesmos.

### <a name="run-a-failover-toohello-on-premises-site"></a>Executar uma ativação pós-falha toohello no local
Depois de voltar a proteger Olá VM, pode iniciar uma ativação pós-falha do tooon local do Azure.

1. Na página de itens replicados Olá, faça duplo clique Olá máquina e, em seguida, selecione **ativação pós-falha não planeada**.
2. No **confirmar ativação pós-falha**, certifique-se a direção de ativação pós-falha de Olá (a partir do Azure) e, em seguida, selecione o ponto de recuperação de Olá que pretende que toouse para ativação pós-falha de Olá (Olá mais recente ou Olá último consistentes da aplicação ponto de recuperação). Um ponto de recuperação consistentes da aplicação ocorre antes do ponto mais recente Olá no tempo e irá fazer com que alguma perda de dados.
3. Durante a ativação pós-falha, a recuperação de Site encerra Olá VMs do Azure. Depois de verificar que esse reativação pós-falha foi concluída conforme esperado, pode verificar tooensure que as VMs do Azure de Olá ter foi encerradas conforme esperado.

### <a name="reprotect-hello-on-premises-site"></a>Proteja o site no local de Olá
Reativação pós-falha tenha sido concluída, são eliminados tooensure de máquina virtual de Olá consolidação Olá VMs recuperadas no Azure. toodo por isso, faça duplo clique item Olá protegido e, em seguida, clique em **consolidar**. Esta ação aciona uma tarefa que remove Olá anteriores recuperado as máquinas virtuais no Azure.

Consolidação de Olá esteja concluída, os dados devem estar novamente no site no local de Olá, mas não será possível protegê-lo. tooAzure replicação toostart novamente, Olá seguintes:

1. No **cofre**, na **definição** > **replicado itens**, selecione Olá VMs que falharam novamente e, em seguida, clique em **voltar a proteger**.
2. Forneça Olá valor hello do servidor de processos que tem toobe utilizado toosend dados back-tooAzure.
3. Clique em **OK**.

Depois de concluída a só Olá, Olá VM replica back tooAzure e pode efetuar uma ativação pós-falha.

### <a name="resolve-common-failback-issues"></a>Resolver problemas comuns de reativação pós-falha
* Se executar uma deteção de utilizadores de só de leitura do vCenter e proteger máquinas virtuais, tiver êxito e a ativação pós-falha funciona. Que, durante a ativação pós-falha falhará porque a Olá datastores não pode ser detetado. Como um sintoma, não verá datastores Olá listados durante só. tooresolve este problema, pode atualizar a credencial do vCenter Olá com uma conta adequada com permissões e repita a tarefa de Olá. Para obter mais informações, consulte [máquinas virtuais VMware replicar e servidores físicos tooAzure com o Azure Site Recovery](site-recovery-vmware-to-azure-classic.md)
* Quando efetuar pós-falha uma VM com Linux e executá-la no local, pode ver que esse pacote de Gestor de rede Olá máquina Olá foi desinstalado. Esta desinstalação acontece porque o pacote de Gestor de rede de Olá é removido quando for recuperada Olá VM no Azure.
* Quando uma VM está configurada com um endereço IP estático e é efetuada a ativação pós-falha tooAzure, endereço IP Olá é adquirido através de DHCP. Quando a ativação pós-falha local tooon anterior, Olá VM continua o endereço IP do toouse DHCP tooacquire Olá. Manualmente, inicie sessão na máquina de toohello e definir o endereço de back-tooa de endereço IP do Olá estático se necessário.
* Se estiver a utilizar a edição gratuita ESXi 5.5 ou edição gratuita do hipervisor vSphere 6, ativação pós-falha será bem-sucedida, mas não seria ativar a reativação pós-falha. reativação pós-falha tooenable, licença de avaliação do programa de atualização tooeither.
* Se é possível alcançar o servidor de configuração de hello do servidor de processos de Olá, verifique o servidor de configuração de toohello conectividade por máquina do servidor de configuração do Telnet toohello na porta 443. Também pode experimentar o servidor de configuração de Olá tooping da máquina do servidor de processos de Olá. Um servidor de processos também deve ter um heartbeat quando é ligado toohello servidor de configuração.
* Se estiver a tentar toofail back tooan alternativo vCenter, certifique-se de que o seu novo vCenter é detetado e esse servidor de destino mestre Olá também é detetado. Um típico sintoma é que Olá datastores não são acessíveis ou visível no Olá **Proteja** caixa de diálogo.
* Uma máquina WS2008R2SP1 protegida como uma máquina física no local não pode ser falhada novamente a partir do local tooon do Azure.

## <a name="fail-back-with-expressroute"></a>Falhar com o ExpressRoute
Pode efetuar a cópia através de uma ligação de VPN ou utilizando uma ligação ExpressRoute. Se quiser toouse uma ligação ExpressRoute, tenha em atenção o seguinte de Olá:

* Olá ligação do ExpressRoute deve ser configurada em Olá rede virtual do Azure que máquinas de origem Olá falharem tooand onde Olá VMs do Azure estão localizadas após a ocorrência da ativação pós-falha de Olá.
* Os dados são replicado tooan conta do storage do Azure de um ponto final público. toouse uma ligação ExpressRoute, configurar o peering público no ExpressRoute com o Centro de dados de destino Olá para replicação de recuperação de sites.
