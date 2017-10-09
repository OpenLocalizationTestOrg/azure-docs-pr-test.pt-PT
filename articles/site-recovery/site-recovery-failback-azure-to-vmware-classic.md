---
title: "aaaFail fazer uma cópia de VMs de VMware a partir do Azure no portal clássico Olá | Microsoft Docs"
description: "Saiba mais sobre o site no local de back-toohello a falhar após a ativação pós-falha de VMs de VMware e servidores físicos tooAzure."
services: site-recovery
documentationcenter: 
author: ruturaj
manager: mkjain
editor: 
ms.assetid: 7ca86e21-7a5d-45ab-8f4b-e42da90f199a
ms.service: site-recovery
ms.devlang: na
ms.tgt_pltfrm: na
ms.topic: article
ms.workload: storage-backup-recovery
ms.date: 06/05/2017
ms.author: ruturajd
ms.openlocfilehash: 80bc3ab2708a5df953c6532b353da19a4c44ac34
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="fail-back-vmware-virtual-machines-and-physical-servers-toohello-on-premises-site-classic-portal"></a>Falhar back-máquinas de virtuais de VMware e site do servidores físicos toohello no local (portal clássico)
> [!div class="op_single_selector"]
> * [Portal do Azure](site-recovery-failback-azure-to-vmware.md)
> * [Portal Clássico do Azure](site-recovery-failback-azure-to-vmware-classic.md)
> * [Portal clássico do Azure (legados)](site-recovery-failback-azure-to-vmware-classic-legacy.md)
>
>

Este artigo descreve como toofail fazer uma cópia de máquinas virtuais do Azure do site do Azure toohello no local. Siga as instruções de Olá neste artigo quando estiver pronto toofail fazer uma cópia das máquinas virtuais VMware ou servidores físicos Windows/Linux depois que tem a ativação pós-falha de Olá local no site tooAzure utilizando este [tutorial](site-recovery-vmware-to-azure-classic.md).

## <a name="overview"></a>Descrição geral
Este diagrama mostra a arquitetura de reativação pós-falha Olá para este cenário.

Utilize esta arquitetura quando o servidor de processos de Olá está no local e estiver a utilizar o ExpressRoute.

![](./media/site-recovery-failback-azure-to-vmware-classic/architecture.png)

Utilize esta arquitetura quando o servidor de processos de Olá está no Azure e tiver uma VPN ou uma ligação ExpressRoute.

![](./media/site-recovery-failback-azure-to-vmware-classic/architecture2.png)

lista completa de Olá toosee de portas e diagrama de architechture de reativação pós-falha Olá Consulte toohello imagem abaixo

![](./media/site-recovery-failback-azure-to-vmware-classic/Failover-Failback.png)

Eis como funciona a reativação pós-falha:

* Depois de ter a efetuar a ativação pós-falha tooAzure, falhar site no local de back-tooyour em alguns fases:
  * **Fase 1**: Proteja as VMs do Azure de Olá, de modo a que são iniciados replicar VMs de back-tooVMware em execução no seu site no local. Ativar só desloca Olá VM para um grupo de proteção de reativação pós-falha que foi criado automaticamente quando criou o grupo de proteção de ativação pós-falha de Olá originalmente. Se tiver adicionado o plano de recuperação tooa de grupo de proteção de ativação pós-falha, em seguida, grupo de proteção de reativação pós-falha Olá foi também adicionado automaticamente toohello plano.  Durante a reproteção que especificar como tooplan toofail fazer uma cópia.
  * **Fase 2**: depois das suas VMs do Azure são replicar site no local de tooyour, executar uma falha ao longo do toofail novamente a partir do Azure.
  * **Fase 3**: depois dos dados falhou novamente, proteja Olá VMs no local não conseguiu fazer uma cópia, para que possam iniciar a replicação tooAzure.


  [!VIDEO https://channel9.msdn.com/Blogs/Azure/Enhanced-VMware-to-Azure-Failback/player]

### <a name="failback-toohello-original-or-alternate-location"></a>Reativação pós-falha toohello localização original ou alternativa
Se efetuar a ativação pós-falha de uma VM de VMware pode falhar back toohello mesma VM de origem caso ainda exista no local. Neste cenário apenas alterações de delta de Olá serão efetuadas a cópia. Tenha em atenção que:

* Se efetuar a ativação pós-falha de servidores físicos, em seguida, reativação pós-falha é sempre tooa nova VM de VMware.
  * Antes de voltar a falhar um computador físico tenha em atenção que
  * Máquina física protegida regressará como uma Máquina Virtual quando a ativação pós-falha novamente a partir do tooVMware do Azure
  * Certifique-se de que detetar, pelo menos, um servidor de destino mestre juntamente com Olá necessário ESX/ESXi anfitriões toowhich terá toofailback.
* Se falhar novamente toohello original VM Olá segue-se necessário:

  * Se hello VM for gerida por um servidor vCenter anfitrião do ESX de destino mestre Olá deve ter o arquivo de dados do acesso toohello VMs.
  * Se hello VM estiver num anfitrião ESX, mas não é gerida pelo vCenter, em seguida, de disco rígido Olá Olá VM tem de constar um arquivo de dados acessível pelo anfitrião Olá do MT.
  * Se a VM num anfitrião do ESX e não utilize o vCenter deve efetuar a deteção do anfitrião do ESX Olá de Olá MT antes que voltar a proteger. Isto aplica-se se está a reativar demasiado servidores físicos novamente.
  * Outra opção (se Olá no local encontra VM) é toodelete-lo antes de efetuar uma reativação pós-falha. Em seguida, reativação pós-falha, irá criar uma nova VM, em seguida, no Olá mesmo anfitrião como anfitrião do ESX Olá destino mestre.
* Quando reativação pós-falha tooan localização alternativa Olá dados será recuperada toohello mesmo arquivo de dados e Olá mesmo anfitrião ESX que foi utilizado pelo servidor de destino mestre Olá no local.

## <a name="prerequisites"></a>Pré-requisitos
* Irá precisar de um ambiente de VMware no back toofail de ordem VMs de VMware e servidores físicos. A falhar back tooa servidor físico não é suportado.
* Na ordem toofail novamente, deverá ter criado uma rede do Azure quando configurar inicialmente a proteção. Reativação pós-falha necessita de uma ligação VPN ou ExpressRoute do Azure de Olá rede na qual Olá VMs do Azure são site do toohello localizados no local.
* Se as VMs de Olá quiser tooare back toofail gerido por um servidor vCenter terá toomake se que tem as permissões de Olá necessário para a deteção de VMs nos servidores do vCenter. [Leia mais](site-recovery-vmware-to-azure-classic.md).
* Se existirem instantâneos numa VM só irá falhar. Pode eliminar os instantâneos de Olá ou discos Olá.
* Antes de efetuar pós-falha terá toocreate um número de componentes:
  * **Criar um servidor de processos no Azure**. Esta é uma VM do Azure que irá precisar de toocreate e continuará a ser executada durante a reativação pós-falha. Pode eliminar a máquina de Olá após a conclusão da reativação pós-falha.
  * **Criar um servidor de destino mestre**: servidor de destino mestre Olá envia e recebe dados de reativação pós-falha. servidor de gestão de Olá que criou no local tem um servidor de destino mestre instalado por predefinição. No entanto, consoante o volume de Olá de tráfego de back-falhado poderá ser necessário toocreate um servidor de destino principal separado para reativação pós-falha.
  * Se quiser toocreate um servidor de destino mestre adicionais em execução no Linux, terá tooset segurança Olá VM com Linux antes de instalar o servidor de destino mestre Olá, conforme descrito abaixo.
* Servidor de configuração é necessário no local quando fizer uma reativação pós-falha. Durante a reativação pós-falha, máquina virtual de Olá tem de existir na Olá configuração servidor da base de dados, que reativação pós-falha wont seja concluída com êxito a falhar. Por conseguinte, certifique-se de que efetuar cópia de segurança agendada normal do seu servidor. No caso de um desastre, terá de toorestore com Olá mesmo endereço IP, para que a reativação pós-falha irá funcionar.

## <a name="set-up-hello-process-server-in-azure"></a>Configurar o servidor de processos de Olá no Azure
Terá de tooinstall um servidor de processos no Azure para que as VMs do Azure de Olá possa enviar o servidor de destino mestre Olá dados back-tooon local.

1. No portal de recuperação de Site Olá > **servidores de configuração** selecione tooadd um novo servidor de processos.

   ![](./media/site-recovery-failback-azure-to-vmware-classic/ps1.png)
2. Especifique um nome de servidor de processo e introduza um nome e a palavra-passe, irá utilizar tooconnect toohello VM do Azure como administrador. No **servidor de configuração** selecione o servidor de gestão no local Olá e especifique Olá do Azure na qual Olá deve ser implementado servidor de processos de rede. Deve ser rede Olá no qual as VMs do Azure de Olá estão localizadas. Especifique um endereço IP exclusivo da sub-rede selecione Olá e iniciar a implementação.

   ![](./media/site-recovery-failback-azure-to-vmware-classic/ps2.png)

   Um servidor de processos do tarefa toodeploy Olá será acionado

   ![](./media/site-recovery-failback-azure-to-vmware-classic/ps3.png)

   Após Olá o servidor de processos é implementado no Azure, pode iniciar sessão no mesmo utilizando credenciais Olá que especificou. Olá pela primeira vez que iniciar sessão na caixa de diálogo de servidor de processos de Olá será executado. Tipo de endereço de IP Olá Olá no local do servidor de gestão e o frase de acesso. Deixe Olá predefinição a porta 443. Também pode deixar Olá porta de 9443 predefinida para a replicação de dados, exceto se especificamente modificar esta definição quando configurou o servidor de gestão do Olá no local.

   > [!NOTE]
   > servidor de Olá não será visível em **propriedades VM**. Só é visível em Olá **servidores** separador toowhich de servidor de gestão de Olá está registada. Pode demorar sobre 10 a 15 minutos para tooappear de servidor de processo Olá.
   >
   >

## <a name="set-up-hello-master-target-server-on-premises"></a>Configurar Olá destino mestre server no local
servidor de destino mestre Olá recebe dados de reativação pós-falha Olá. Um servidor de destino principal é automaticamente instalado no servidor de gestão do Olá no local, mas se está a reativar novamente uma grande quantidade de dados poderá ser necessário tooset configurar um servidor de destino mestre adicionais. Fazê-lo da seguinte forma:

> [!NOTE]
> Se quiser tooinstall um servidor de destino principal no Linux, siga instruções de Olá no procedimento seguinte Olá.
>
>

1. Se estiver a instalar o servidor de destino mestre Olá no Windows, abra a página de início rápido Olá Olá VM em que estiver a instalar o servidor de destino mestre Olá e transferir o ficheiro de instalação de Olá para o Assistente de configuração de unificada do Azure Site Recovery Olá.
2. Execute a configuração e na **antes de começar** selecione **adicionar tooscale de servidores de processos adicionais saída implementação**.
3. Assistente de Olá completa no Olá mesma forma que fez quando [configurar o servidor de gestão de Olá](site-recovery-vmware-to-azure-classic.md). No Olá **detalhes do servidor de configuração** página, especifique o endereço IP Olá deste servidor de destino principal e Olá de tooaccess uma frase de acesso VM.

### <a name="set-up-a-linux-vm-as-hello-master-target-server"></a>Configurar uma VM com Linux como servidor de destino mestre Olá
tooset segurança do servidor de gestão de Olá com o servidor de destino mestre Olá como um VM, precisará tooinstall Olá cêntimos do Linux) S 6.6 sistema operativo mínimo, obter Olá os IDs de SCSI para cada disco de rígido SCSI, instalar alguns pacotes adicionais e aplicam-se algumas alterações personalizadas.

#### <a name="install-centos-66"></a>Instalar CentOS 6.6
1. Instale o sistema operativo mínimo do Olá CentOS 6.6 no servidor de gestão de Olá VM. Manter Olá ISO num DVD unidade e arranque Olá sistema. Ignorar Olá suporte de dados de teste, selecione inglês no idioma Olá, selecione **básico dispositivos de armazenamento**, verifique se o disco rígido de Olá não tem quaisquer dados importantes e clique em **Sim**, eliminar quaisquer dados. Introduza o nome de anfitrião Olá hello do servidor de gestão e selecione o adaptador de rede do servidor de Olá.  No Olá **editar sistema** caixa de diálogo Selecionar * * ligar automaticamente * * e adicione um endereço IP estático, rede e as definições de DNS. Especifique um fuso horário e um servidor de gestão de Olá de tooaccess de palavra-passe de raiz.
2. Quando solicitado tipo Olá de instalação que pretende selecionar **criar esquema de personalizado** como partição de Olá. Depois de clicar em **seguinte** selecione **livres** e clique em criar. Criar  **/** , **/var/falhas** e **/partições de casa** com **FS tipo:** **ext4**. Criar partion de troca de Olá como **FS tipo: troca**.
3. Se não for encontrados dispositivos pré-existente, que será apresentada uma mensagem de aviso. Clique em **formato** unidade de Olá tooformat com definições de partição Olá. Clique em **escrita alterar toodisk** alterações de partição de Olá tooapply.
4. Selecione **carregador de arranque de instalação** > **seguinte** carregador de arranque Olá tooinstall na partição de raiz de Olá.
5. Quando a instalação estiver concluída clique **reiniciar**.

#### <a name="retrieve-hello-scsi-ids"></a>Obter os IDs de SCSI Olá
1. Após a instalação obter Olá IDs de SCSI para cada disco de rígido SCSI de Olá VM. toodo isto encerrar o servidor de gestão de Olá VM, na Olá VM propriedades do VMware com o botão direito entrada VM Olá > **editar definições de** > **opções**.
2. Selecione **avançadas** > **item geral** e clique em **parâmetros de configuração**. Esta opção estará de-active quando Olá máquina está em execução. toomake it tem de encerrar a máquina Olá Active Directory.
3. Se hello linha **disco. EnableUUID** existe Certifique-se de que o valor de Olá for definido demasiado**verdadeiro** (sensível às maiúsculas e). Se já estiver pode cancelar e testar o comando de SCSI Olá dentro de um sistema operativo convidado depois for iniciado.
4. Se a linha de Olá não existente clique **linha adicionar** – e adicioná-la com Olá **verdadeiro** valor. Não utilize aspas duplas.

#### <a name="install-additional-packages"></a>Instalar pacotes adicionais
Irá precisar de toodownload e instalar alguns pacotes adicionais.

1. Certifique-se o servidor de destino mestre Olá toohello ligado à internet.
2. Executar este toodownload de comando e instalar 15 pacotes do repositório de CentOS Olá: **# yum instalar – y xfsprogs perl lsscsi rsync wget kexec-tools**.
3. Se estiver a proteger máquinas de origem de Olá estiverem a executar Linux intera Reiser XFS sistema para a raiz de Olá de ficheiros ou efetuar o arranque de dispositivo, em seguida, deve transferir e instalar pacotes adicionais da seguinte forma:

   * # <a name="cd-usrlocal"></a>CD /usr/local
   * # <a name="wget-httpelrepoorglinuxelrepoel6x8664rpmskmod-reiserfs-00-1el6elrepox8664rpmhttpelrepoorglinuxelrepoel6x8664rpmskmod-reiserfs-00-1el6elrepox8664rpm"></a>wget [http://elrepo.org/linux/elrepo/el6/x86_64/RPMS/kmod-reiserfs-0.0-1.el6.elrepo.x86_64.rpm](http://elrepo.org/linux/elrepo/el6/x86_64/RPMS/kmod-reiserfs-0.0-1.el6.elrepo.x86_64.rpm)
   * # <a name="wget-httpelrepoorglinuxelrepoel6x8664rpmsreiserfs-utils-3621-1el6elrepox8664rpmhttpelrepoorglinuxelrepoel6x8664rpmsreiserfs-utils-3621-1el6elrepox8664rpm"></a>wget [http://elrepo.org/linux/elrepo/el6/x86_64/RPMS/reiserfs-utils-3.6.21-1.el6.elrepo.x86_64.rpm](http://elrepo.org/linux/elrepo/el6/x86_64/RPMS/reiserfs-utils-3.6.21-1.el6.elrepo.x86_64.rpm)
   * # <a name="rpm-ivh-kmod-reiserfs-00-1el6elrepox8664rpm-reiserfs-utils-3621-1el6elrepox8664rpm"></a>reiserfs de kmod-reiserfs 0,0 1.el6.elrepo.x86_64.rpm da – ivh rpm-utils-3.6.21-1.el6.elrepo.x86_64.rpm
   * # <a name="wget-httpmirrorcentosorgcentos66osx8664packagesxfsprogs-311-16el6x8665rpmhttpmirrorcentosorgcentos66osx8664packagesxfsprogs-311-16el6x8665rpm"></a>wget [http://mirror.centos.org/centos/6.6/os/x86_64/Packages/xfsprogs-3.1.1-16.el6.x86_65.rpm](http://mirror.centos.org/centos/6.6/os/x86_64/Packages/xfsprogs-3.1.1-16.el6.x86_65.rpm)
   * # <a name="rpm-ivh-xfsprogs-311-16el6x8664rpm"></a>rpm – ivh xfsprogs-3.1.1-16.el6.x86_64.rpm

#### <a name="apply-custom-changes"></a>Aplicar alterações personalizadas
Efetue Olá seguintes alterações personalizado tooapply depois de ter passos de pós-instalação concluída Olá e pacotes de Olá instalado:

1. Copie Olá agente Unified do RHEL 6-64 binário toohello VM. Execute este Olá de toountar comando binário: **tar – zxvf<file name>**
2. Execute este permissões toogive de comando: **# chmod 755./ApplyCustomChanges.sh**
3. Executar script de Olá: **#./ApplyCustomChanges.sh**. Apenas deve executar script de Olá, uma vez. Reinicie o servidor de Olá depois de script de Olá é executado com êxito.

## <a name="run-hello-failback"></a>Execute a reativação pós-falha da Olá
### <a name="reprotect-hello-azure-vms"></a>Proteja as VMs do Azure de Olá
1. No portal de recuperação de Site Olá > **máquinas** separador selecione Olá VM é foi efetuada a ativação pós-falha e clique em **voltar a proteger**.
2. No **servidor de destino mestre** e **servidor de processos** selecionar servidor de destino mestre no local Olá e o servidor de processos do Olá VM do Azure.
3. Selecione a conta de Olá configurado para ligar toohello VM.
4. Selecione a versão de reativação pós-falha Olá Olá do grupo de proteção. Por exemplo, se Olá VM está protegido na PG1, em seguida, irá precisar de tooselect PG1_Failback.
5. Se pretender que a localização alternativa de tooan toorecover, selecione unidade de retenção de Olá e configurado para o servidor de destino mestre Olá do arquivo de dados. Quando falhar back toohello local no site Olá VMs de VMware no plano de proteção de reativação pós-falha Olá utilizará Olá mesmo arquivo de dados como servidor de destino mestre Olá. Se quiser toorecover Olá réplica VM do Azure toohello mesmo local VM, em seguida, Olá no local VM já deve ser na Olá mesmo arquivo de dados, tal como Olá mestre de destino de servidor. Se não houver nenhuma VM no local será criada uma nova durante só.

   ![](./media/site-recovery-failback-azure-to-vmware-classic/failback1.png)
6. Depois de clicar em **OK** toobegin que uma tarefa começa tooreplicate Olá VM a partir do site do Azure toohello no local. Pode controlar o progresso de Olá no Olá **tarefas** separador.

   ![](./media/site-recovery-failback-azure-to-vmware-classic/failback2.png)

### <a name="run-a-failover-toohello-on-premises-site"></a>Executar uma ativação pós-falha toohello no local
Após Olá só VM é versão de reativação pós-falha toohello movidas do respetivo grupo de proteção e é automaticamente adicionada toohello plano de recuperação utilizado para Olá tooAzure de ativação pós-falha se existir um.

1. No Olá **planos de recuperação** plano de recuperação de Olá selecione de página que contém o grupo de reativação pós-falha Olá e clique em **ativação pós-falha** > **ativação pós-falha não planeada**.
2. No **confirmar ativação pós-falha** Certifique-se a direção de ativação pós-falha de Olá (tooAzure) e selecione o ponto de recuperação de Olá pretende toouse para Olá de ativação pós-falha (mais recentes). Se tiver ativado **multi-VM** quando configurou propriedades de replicação pode recuperar toohello mais recente aplicação ou um ponto de recuperação consistentes com falhas. Clique em Olá marca de verificação toostart Olá ativação pós-falha.
3. Durante a ativação pós-falha, recuperação de Site irá encerrar Olá VMs do Azure. Depois de verificar que esse reativação pós-falha concluída conforme esperado, pode pode verificar que Olá que VMS do Azure ter sido encerradas conforme esperado.

### <a name="reprotect-hello--on-premises-site"></a>Proteja o site no local de Olá
Após a conclusão da reativação pós-falha os dados serão novamente no site do Olá no local, mas não irão ser protegidos. tooAzure replicação toostart novamente Olá seguintes:

1. No portal de recuperação de Site Olá > **máquinas** separador Olá selecione VMs que ocorreu uma falha anterior e clique em **voltar a proteger**.
2. Depois de verificar que tooAzure de replicação está a funcionar conforme esperado, no Azure pode eliminar Olá as VMs do Azure (atualmente não está em execução) que foram falha novamente.

### <a name="common-issues-in-failback"></a>Problemas comuns na reativação pós-falha
1. Se executar a deteção de utilizadores de só de leitura do vCenter e proteger máquinas virtuais, tiver êxito e a ativação pós-falha funciona. No momento de Olá de Reproteção, ocorrerá uma falha, uma vez que não podem ser detetados Olá datastores. Como um sintoma não verá datastores Olá listados ao voltar a proteger. tooresolve, pode atualizar a credencial do vCenter Olá com a conta adequada, que tem permissões e repita a tarefa de Olá. [Saiba mais](site-recovery-vmware-to-azure-classic.md)
2. Quando a reativação pós-falha uma VM com Linux e execute-o no local, verá esse pacote de Gestor de rede Olá é desinstalado do computador Olá. Isto acontece porque quando for recuperada Olá VM no Azure, o pacote do Gestor de rede de Olá é removida.
3. Quando uma VM está configurada com o endereço IP estático e é efetuada a ativação pós-falha tooAzure, endereço IP Olá é adquirido através de DHCP. Quando a ativação pós-falha local tooOn anterior, Olá VM continua o endereço IP do toouse DHCP tooacquire Olá. Terá de início de sessão toomanually numa máquina Olá e o endereço IP do conjunto Olá cópia tooStatic endereço, se necessário.
4. Se estiver a utilizar a edição gratuita ESXi 5.5 ou edição gratuita do hipervisor vSphere 6, ativação pós-falha seria bem-sucedida, mas a reativação pós-falha não será concluída com êxito. Irá ned reativação pós-falha tooenable do tooupgrade tooeither licença de avaliação.

## <a name="failing-back-with-expressroute"></a>Falhar back com o ExpressRoute
Pode efetuar a cópia através de uma ligação VPN ou Azure ExpressRoute. Se quiser seguinte de Olá toouse ExpressRoute Nota:

* ExpressRoute deve ser configurado em Olá rede virtual do Azure toowhich origem máquinas falhar ao longo e, na qual as VMs do Azure estão localizadas após a ocorrência da ativação pós-falha de Olá.
* Os dados são replicado tooan conta do storage do Azure de um ponto final público. Deve configurar um peering público no ExpressRoute com o Centro de dados de destino Olá para recuperação de Site replicação toouse ExpressRoute.
