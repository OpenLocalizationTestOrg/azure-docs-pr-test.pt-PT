---
title: "aaaFail fazer uma cópia de VMs de VMware a partir do Azure no portal clássico legado de Olá | Microsoft Docs"
description: "Este artigo descreve como toofail back uma máquina virtual VMware que foi replicado tooAzure com o Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: ruturaj
manager: mkjain
editor: 
ms.assetid: a63524bf-990c-42ee-8554-e017e6e67e68
ms.service: site-recovery
ms.devlang: na
ms.tgt_pltfrm: na
ms.topic: article
ms.workload: storage-backup-recovery
ms.date: 06/05/2017
ms.author: ruturajd@microsoft.com
ms.openlocfilehash: 5ef66b366dcdc43f3bc171e0ed1532216cc2ab89
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="fail-back-vmware-virtual-machines-and-physical-servers-from-azure-toovmware-with-azure-site-recovery-legacy"></a>Falhar back em máquinas virtuais VMware e servidores físicos do tooVMware do Azure com o Azure Site Recovery (legados)
> [!div class="op_single_selector"]
> * [Portal do Azure](site-recovery-failback-azure-to-vmware.md)
> * [Portal Clássico do Azure](site-recovery-failback-azure-to-vmware-classic.md)
> * [Portal clássico do Azure (legados)](site-recovery-failback-azure-to-vmware-classic-legacy.md)
>
>

Este artigo descreve como toofail back-as máquinas virtuais VMware e servidores físicos Windows/Linux do site no local de tooyour do Azure após tiver replicado do seu local de sites tooAzure utilizando [do Azure Site Recovery?](site-recovery-overview.md).

Este artigo descreve uma configuração antiga e não deve ser utilizado para cofres de novo.

## <a name="architecture"></a>Arquitetura
Este diagrama representa o cenário de ativação pós-falha e a reativação pós-falha Olá. linhas de Olá azul são ligações Olá utilizadas durante a ativação pós-falha. linhas de Olá vermelho são ligações Olá utilizadas durante a reativação pós-falha. linhas de Olá com setas passam Olá internet.

![](./media/site-recovery-failback-azure-to-vmware/vconports.png)

## <a name="before-you-start"></a>Antes de começar
* Deve ter houve ativação pós-falha de VMs de VMware ou servidores físicos e devem estar a executar no Azure.
* Deve ter em atenção que apenas pode proceder back em máquinas virtuais VMware e servidores físicos Windows/Linux provenientes de máquinas de virtuais tooVMware do Azure no site primário do Olá no local.  Se está a reativar novamente um computador físico, tooAzure de ativação pós-falha irá convertê-lo tooan VM do Azure e reativação pós-falha tooVMware irá convertê-lo tooa VM de VMware.

Eis como configurar a reativação pós-falha:

1. **Configurar componentes de reativação pós-falha**: irá precisar de tooset configurar um servidor vContinuum no local e aponte-o servidor de configuração de toohello VM no Azure. Irá também configurar um servidor de processos como um servidor de destino principal no local do VM do Azure toosend dados toohello anterior. Registar o servidor de processos de Olá com servidor de configuração de Olá processado de ativação pós-falha de Olá. Instalar um servidor de destino principal no local. Se precisar de um servidor de destino principal do Windows, é configurado automaticamente quando instala vContinuum. Se precisar de Linux terá tooset-cópia de segurança manualmente num servidor separado.
2. **Ativar a proteção e a reativação pós-falha**: depois de ter configurado os componentes de Olá, no vContinuum, terá proteção tooenable para efetuar a ativação pós-falha de VMs do Azure. Irá executar uma verificação de disponibilidade no Olá VMs e executar uma ativação pós-falha a partir do site do Azure tooyour no local. Após a conclusão da reativação pós-falha Proteja máquinas no local para que possam iniciar a replicação tooAzure.

## <a name="step-1-install-vcontinuum-on-premises"></a>Passo 1: Instalar vContinuum no local
Irá precisar de tooinstall um servidor vContinuum no local e aponte-o servidor de configuração toohello.

1. [Transferir vContinuum](http://go.microsoft.com/fwlink/?linkid=526305).
2. Em seguida, transferir Olá [vContinuum atualização](http://go.microsoft.com/fwlink/?LinkID=533813) versão.
3. Instale a versão mais recente do Olá de vContinuum. No Olá **boas-vindas** página clique **seguinte**.
    ![](./media/site-recovery-failback-azure-to-vmware/image2.png)
4. Na Olá primeira página do Assistente de Olá especifique o endereço IP do servidor CX Olá e porta do servidor Olá CX. Selecione **utilizar HTTPS**.

   ![](./media/site-recovery-failback-azure-to-vmware/image3.png)
5. Localizar o servidor de configuração de Olá endereço IP no Olá **Dashboard** separador do servidor de configuração de Olá VM no Azure.
   ![](./media/site-recovery-failback-azure-to-vmware/image4.png)
6. Localizar o servidor de configuração de Olá HTTPS Porta pública no Olá **pontos finais** separador do servidor de configuração de Olá VM no Azure.

   ![](./media/site-recovery-failback-azure-to-vmware/image5.png)
7. No Olá **CS frase de acesso detalhes** página especificar Olá frase de acesso que anotou inativo quando registar o servidor de configuração de Olá. Não se lembra-registá-lo **c:\\os ficheiros de programa (x86)\\InMage sistemas\\privada\\connection.passphrase** no servidor de configuração de Olá VM.

    ![](./media/site-recovery-failback-azure-to-vmware/image6.png)
8. No Olá **selecionar localização de destino** página especificar onde pretende tooinstall Olá vContinuum servidor e clique em **instalar**.

   ![](./media/site-recovery-failback-azure-to-vmware/image7.png)
9. Depois de concluída a instalação, pode iniciar vContinuum.
    ![](./media/site-recovery-failback-azure-to-vmware/image8.png)

## <a name="step-2-install-a-process-server-in-azure"></a>Passo 2: Instalar um servidor de processos no Azure
Terá de tooinstall um servidor de processos no Azure para que Olá VMs no Azure podem enviar o servidor de destino principal do Olá dados back tooan no local.

1. No Olá **servidores de configuração** página no Azure, selecione tooadd um novo servidor de processos.

   ![](./media/site-recovery-failback-azure-to-vmware/image9.png)
2. Especifique um nome de servidor de processos e um nome e palavra-passe tooconnect toohello das máquinas virtuais como administrador. Selecione toowhich de servidor de configuração de Olá pretende que o servidor de processos de Olá tooregister. Isto deve ser Olá mesmo servidor que está a utilizar tooprotect e efetuar a ativação pós-falha de máquinas virtuais.
3. Especifique Olá Azure rede na qual Olá o servidor de processos deve ser implementado. Deve ser Olá mesmo rede como servidor de configuração de Olá. Especifique uma sub-rede de endereço selecionado IP exclusiva e iniciar a implementação.

   ![](./media/site-recovery-failback-azure-to-vmware/image10.png)
4. Uma tarefa é o servidor de processos de Olá toodeploy accionadas.

   ![](./media/site-recovery-failback-azure-to-vmware/image11.png)
5. Depois do servidor de processos de Olá é implementado no Azure pode iniciar sessão no servidor de Olá utilizando credenciais de Olá que especificou. Registar o servidor de processos de Olá no Olá mesma forma que registou Olá-local no servidor de processos.

   ![](./media/site-recovery-failback-azure-to-vmware/image12.png)

> [!NOTE]
> registado durante a reativação pós-falha de servidores de Olá não será visíveis em propriedades VM na recuperação de Site. Apenas são visíveis em Olá **servidores** separador de toowhich de servidor de configuração de Olá que está a ser registados. Pode demorar cerca de 10 a 15 minutos até que Olá o processo de servidor é apresentado no separador de Olá.
>
>

## <a name="step-3-install-a-master-target-server-on-premises"></a>Passo 3: Instalar um servidor de destino principal no local
Consoante o sistema operativo de máquinas virtuais de origem, terá de tooinstall um Linux ou um servidor de destino principal do Windows no local.

### <a name="deploy-a-windows-master-target-server"></a>Implementar um servidor de destino principal do Windows
Um destino principal do Windows já está incluído com a configuração de vContinuum. Quando instala vContinuum Olá, um servidor mestre for também implementado num Olá mesmo computador e o servidor de configuração de toohello registado.

1. implementação de toobegin, criar vazio máquina no local do anfitrião do ESX Olá em que pretende toorecover Olá VMs do Azure.
2. Certifique-se de que existem, pelo menos, dois discos anexados toohello VM – um é utilizado para o sistema de operativo Olá e Olá outro é utilizada para a unidade de retenção de Olá.
3. Instale o sistema de operativo Olá.
4. Instale Olá vContinuum no servidor de Olá. Isto também conclui a instalação do servidor de destino mestre Olá.

### <a name="deploy-a-linux-master-target-server"></a>Implementar um servidor de destino principal do Linux
1. implementação de toobegin, criar vazio máquina no local do anfitrião do ESX Olá em que pretende toorecover Olá VMs do Azure.
2. Certifique-se de que existem, pelo menos, dois discos anexados toohello VM – um é utilizado para o sistema de operativo Olá e Olá outro é utilizada para a unidade de retenção de Olá.
3. Instale o sistema de operativo Olá Linux. Olá sistema de destino principal do Linux não deve utilizar LVM raiz ou de retenção para espaços de armazenamento. Um Linux ao servidor de destino mestre está configurado a deteção de partições/discos tooavoid LVM por predefinição.
4. Partições que pode criar:

   ![](./media/site-recovery-failback-azure-to-vmware/image13.png)
5. Realizar Olá passos de instalação de post abaixo antes de iniciar a instalação de destino mestre Olá.

#### <a name="post-os-installation-steps"></a>Publique os passos de instalação do SO
tooget Olá IDs de SCSI para cada disco de rígido SCSI numa máquina virtual Linux, ativar o parâmetro de Olá ". o disco. EnableUUID = TRUE "da seguinte forma:

1. Encerre a máquina virtual.
2. Faça duplo clique de entrada VM Olá no painel da esquerda Olá > **editar definições de**.
3. Clique em Olá **opções** separador. Selecione **avançadas\>item geral** > **parâmetros de configuração**. Olá **parâmetros de configuração** opção só está disponível quando máquina Olá é encerrada.

    ![](./media/site-recovery-failback-azure-to-vmware/image14.png)
4. Verifica se uma linha com **disco. EnableUUID** existe. Se e está definido demasiado**falso** , em seguida, defini-lo demasiado**verdadeiro** (não sensível confidenciais). Se existe e está definido tootrue, clique em **Cancelar** e testar o comando de SCSI Olá no interior do sistema de operativo convidado Olá depois-é arrancado cópias de segurança. Se não existir clique **linha adicionar**.
5. Adicione o disco. EnableUUID no Olá **nome** coluna. Defina o respetivo valor como verdadeiro. Não adicione Olá acima valores juntamente com aspas duplas.

    ![](./media/site-recovery-failback-azure-to-vmware/image15.png)

#### <a name="download-and-install-hello-additional-packages"></a>Transferir e instalar pacotes adicionais Olá
Nota: Certifique-se de que o sistema de Olá tem conectividade internet antes de transferir e instalar pacotes adicionais Olá.

\#yum install -y xfsprogs perl lsscsi rsync wget kexec-tools

Este comando descarrega estes 15 pacotes do CentOS 6.6 repositório e instala-los:

BC-1.06.95-1.el6.x86\_64. rpm

busybox-1.15.1-20.el6.x86\_64. rpm

elfutils libs-0.158 3.2.el6.x86\_64. rpm

kexec-ferramentas-2.0.0-280.el6.x86\_64. rpm

lsscsi-0.23-2.el6.x86\_64. rpm

lzo-2.03-3.1.el6\_5.1.x86\_64. rpm

Perl-5.10.1-136.el6\_6.1.x86\_64. rpm

Perl-módulo-incorporável-3.90-136.el6\_6.1.x86\_64. rpm

Perl-Pod-Escapes-1.04-136.el6\_6.1.x86\_64. rpm

Perl-Pod-simples-3.13-136.el6\_6.1.x86\_64. rpm

Perl libs-5.10.1 136.el6\_6.1.x86\_64. rpm

Perl-versão 0.77 136.el6\_6.1.x86\_64. rpm

rsync-3.0.6-12.el6.x86\_64. rpm

snappy 1.1.0 1.el6.x86\_64. rpm

wget-1.12-5.el6\_6.1.x86\_64. rpm

Se a máquina de origem Olá utiliza Reiser ou XFS sistema de ficheiros para o dispositivo de arranque ou raiz Olá, em seguida, os pacotes seguintes devem ser transferidos e instalados nos tooprotection de anterior de destino principal do Linux.

\#CD /usr/local

\#wget <http://elrepo.org/linux/elrepo/el6/x86_64/RPMS/kmod-reiserfs-0.0-1.el6.elrepo.x86_64.rpm>

\#wget <http://elrepo.org/linux/elrepo/el6/x86_64/RPMS/reiserfs-utils-3.6.21-1.el6.elrepo.x86_64.rpm>

\#rpm - ivh kmod-reiserfs-0,0-1.el6.elrepo.x86\_64. rpm reiserfs-utils-3.6.21-1.el6.elrepo.x86\_64. rpm

\#wget <http://mirror.centos.org/centos/6.6/os/x86_64/Packages/xfsprogs-3.1.1-16.el6.x86_64.rpm>

\#rpm - ivh xfsprogs-3.1.1-16.el6.x86\_64. rpm

#### <a name="apply-custom-configuration-changes"></a>Aplicar alterações de configuração personalizada
Antes de aplicar estas alterações, certifique-se de que concluiu a secção anterior Olá, em seguida, siga estes passos:

1. Copie Olá agente Unified do RHEL 6-64 binário toohello recém-criado SO.
2. Execute este Olá de toountar comando binário: **tar - zxvf \<nome de ficheiro\>**
3. Execute este permissões toogive de comando: \# **chmod 755./ApplyCustomChanges.sh**
4. Executar script de Olá:  **\# ./ApplyCustomChanges.sh**. Execute o script de Olá apenas uma vez no servidor de Olá. Reinicie o servidor de Olá depois Olá script é executado.

### <a name="install-hello-linux-server"></a>Instalar o servidor de Linux Olá
1. [Transferir](http://go.microsoft.com/fwlink/?LinkID=529757) ficheiro de instalação de Olá.
2. Copie o ficheiro de Olá toohello máquina virtual de destino principal do Linux utilizando um utilitário de cliente sftp à sua escolha. Em alternativa pode iniciar sessão na máquina de virtual de destino principal do Olá Linux e utilizar o pacote de instalação do wget toodownload Olá partir da ligação fornecida
3. Registo no Olá Linux destino mestre servidor máquina virtual a utilizar um ssh cliente à sua escolha
4. Se estiver ligado toohello Azure rede em que tiver implementado o servidor de destino principal do Linux através de uma ligação VPN, em seguida, utiliza o endereço IP para o servidor de Olá que pode encontrar na máquina virtual **Dashboard** separador e porta 22 principal do Linux tooconnect toohello utilizando Secure Shell do servidor de destino.
5. Se estiver a ligar o servidor de destino principal do Linux toohello através de uma ligação de internet públicas utilizar público um endereço IP virtual Olá Linux destino mestre servidor (provenientes de máquinas virtuais de Olá **Dashboard** separador) e Olá ponto final público criar para ssh toologin toohello Linux servder.
6. Extraia os ficheiros de Olá do arquivo de tar ao programa de instalação do servidor de destino mestre Olá gzipped Linux executando: *"tar – xvzf Microsoft ASR\_UA\_8.2.0.0\_RHEL6 64\"* do diretório de Olá que contém o ficheiro de instalador de Olá.

    ![](./media/site-recovery-failback-azure-to-vmware/image16.png)
7. Se alterar a Olá extraídos instalador ficheiros tooa outro diretório toohello diretório toowhich Olá conteúdo Olá tar arquivo foram extraído. Deste caminho de diretório, execute "sudo. / install.sh".

    ![](./media/site-recovery-failback-azure-to-vmware/image17.png)
8. Quando selecionar toochoose que lhes é pedida uma função primária **2 (o destino principal)**. Deixe Olá outras opções de instalação interativa os respetivos valores predefinidos.
9. Aguarde pela instalação toocontinue e Olá tooappear Interface de configuração do anfitrião. Olá utilitário de configuração do anfitrião de destino principal do Olá Linux Server é um utilitário de linha de comandos. Não redimensione Olá ssh janela do utilitário de cliente. Olá do utilize Olá seta chaves tooselect **Global** opção e prima INTRODUZA no teclado.

    ![](./media/site-recovery-failback-azure-to-vmware/image18.png)

    ![](./media/site-recovery-failback-azure-to-vmware/image19.png)
10. No campo Olá **IP** introduza o endereço de IP interno de hello do servidor de configuração de Olá (pode encontrá-lo no Olá **Dashboard** separador do servidor de configuração de Olá VM) e prima ENTER. No **porta** introduza **22** e prima ENTER.
11. Deixe **utilize HTTPS** como **Sim**, e prima ENTER.
12. Introduza Olá frase de acesso que foi gerado no servidor de configuração de Olá. Se estiver a utilizar um cliente PUTTY máquina toossh toohello Linux máquina virtual do Windows pode utilizar Shift + Insert toopaste Olá conteúdo da área de transferência Olá. Copiar Olá frase de acesso toohello local da área de transferência utilizando Ctrl-C e utilizar Shift + Insert toopaste-lo. Prima ENTER.
13. Utilize Olá seta para a direita toonavigate chave tooquit e prima ENTER. Aguarde pela instalação toocomplete.

    ![](./media/site-recovery-failback-azure-to-vmware/image20.png)

Se por alguma razão não conseguiu tooregister o servidor de configuração toohello de servidor de destino principal de Linux que pode fazer, por isso, novamente, executando o utilitário de configuração de anfitrião a partir de /usr/local/ASR/Vx/bin/hostconfigcli (terá primeiro toothis de permissões de acesso de tooset diretório executando chmod como um Superutilizador).

#### <a name="validate-master-target-registration"></a>Validar o registo de destino mestre
Pode validar que Olá o servidor de destino principal foi registado com êxito toohello o servidor de configuração no cofre Azure Site Recovery > **servidor de configuração** > **detalhes do servidor**.

> [!NOTE]
> Depois de registar o servidor de destino mestre Olá, se receber erros de configuração que Olá máquina virtual poderá ter sido eliminada do Azure ou que os pontos finais não estarem corretamente configurados, isto acontece porque embora hello configuração de destino principal é detetada por Olá dndpoints do Azure quando o destino principal Olá é implementado no Azure, este não é verdadeiro para um local no destino principal servidor no local. Isto não irá afetar a reativação pós-falha e pode ignorar estes erros.
>
>

## <a name="step-4-protect-hello-virtual-machines-toohello-on-premises-site"></a>Passo 4: Proteger o site do Olá máquinas virtuais toohello no local
Terá de site no local do tooprotect VMs toohello antes da ativação anterior.

### <a name="before-you-begin"></a>Antes de começar
Quando uma VM pós-falha tooAzure, adiciona uma unidade extra temporária para o ficheiro de página. Esta é uma unidade adicional que normalmente não é necessária pelo seu efetuada, uma vez que já tenham uma unidade dedicada para o ficheiro de paginação. Antes de começar inversa proteção de máquinas virtuais de Olá, tem de garantir que este disco seja colocado offline para que não obter protegido. Fazê-lo da seguinte forma:

1. Abra a gestão de computador e selecione gestão de armazenamento, de modo a que lista máquina do Olá discos toohello online e ligado.
2. Selecione Olá disco temporário toohello ligado ao computador e escolha toobring-offline.

### <a name="protect-hello-vms"></a>Proteger VMs Olá
1. No portal do Azure Olá, verifique os Estados de Olá de Olá tooensure de máquina virtual que está a executar a ativação pós-falha.

    ![](./media/site-recovery-failback-azure-to-vmware/image21.png)
2. Inicie vContinuum no seu computador.

    ![](./media/site-recovery-failback-azure-to-vmware/image8.png)
3. Clique em **nova proteção** e selecione o tipo de sistema de operação de Olá, o
4. Numa nova janela do Olá que abrem Olá selecione **tipo de SO** > **obter detalhes** Olá VMs pretende toofail novamente. No **detalhes do servidor primário**, identificar e selecione Olá máquinas virtuais que pretende que o tooprotect. As VMs estão listadas em nome de anfitrião de vCenter Olá estivessem nas suas antes da ativação pós-falha.
5. Quando seleciona uma máquina virtual tooprotect (e já ativou pós-falha tooAzure) uma janela de pop-up fornece duas entradas para a máquina virtual de Olá. Isto acontece porque o servidor de configuração de Olá Deteta duas instâncias do Olá tooit de máquinas virtuais registadas. Terá de entrada de Olá tooremove para Olá no local VM para que possam proteger Olá VM correto. tooidentify Olá correta VM do Azure entrada aqui, que pode iniciar sessão na Olá VM do Azure e aceda tooC:\Program ficheiros (x86) \Microsoft Azure Site Recovery\Application Data\etc. No Olá ficheiro drscout.conf, identificar Olá ID do anfitrião. Na caixa de diálogo de vContinuum Olá, mantenha a entrada de Olá que Olá ID de anfitrião foi encontrado no Olá VM. Elimine todos os outras entradas. Olá tooselect corrigir VM podem referir-se tooits endereço IP. Olá IP endereço intervalo no local irá ser Olá VM no local.

   ![](./media/site-recovery-failback-azure-to-vmware/image22.png)

   ![](./media/site-recovery-failback-azure-to-vmware/image23.png)
6. No servidor do vCenter Olá pare a máquina virtual de Olá. Também pode eliminar Olá VMs no local.
7. Em seguida, especifique Olá no local MT servidor toowhich pretende tooprotect Olá VMs. toodo, ligar toohello vCenter server toowhich pretende toofail novamente.

    ![](./media/site-recovery-failback-azure-to-vmware/image24.png)
8. Servidor de destino mestre Olá selecione com base no Olá anfitrião toowhich pretende toorecover Olá VM.

    ![](./media/site-recovery-failback-azure-to-vmware/image24.png)
9. Forneça a opção de replicação de Olá para cada uma das máquinas virtuais Olá. toodo isto precisa de tooselect Olá recuperação lado arquivo de dados toowhich Olá VMs serão recuperadas. tabela de Olá resume as diferentes opções de Olá terá tooprovide para cada VM.

    ![](./media/site-recovery-failback-azure-to-vmware/image25.png)

   | **Opção** | **Opção valor recomendada** |
   | --- | --- |
   |  Endereço IP do servidor de processos |Selecionar servidor de processos de Olá implementado no Azure |
   |  Tamanho de retenção em MB | |
   |  Valor de retenção |1 |
   |  Horas/dias |Dias |
   |  Intervalo de consistência |1 |
   |  Selecionar arquivo de dados de destino |Olá arquivo de dados disponível no site de recuperação Olá. arquivo de dados de Olá deve tem espaço suficiente e ser anfitrião do ESX toohello disponíveis no qual pretende toorestore Olá máquina. |
10. Configure Olá vão adquirir propriedades Olá máquina virtual após o site de tooon local de ativação pós-falha. Propriedades de Olá estão resumidas na Olá a tabela seguinte.

    ![](./media/site-recovery-failback-azure-to-vmware/image26.png)

    | **Propriedade** | **Detalhes** |
    | --- | --- |
    | Configuração da rede |Para cada adaptador de rede detetado, selecione-o e clique em **alteração** endereço IP do tooconfigure Olá reativação pós-falha da máquina virtual de Olá. |
    | Configuração de hardware |Especifique Olá CPU e memória Olá Olá VM. As definições podem ser aplicados tooall Olá VMs que está a tentar tooprotect. tooidentify Olá valores corretos para Olá da CPU e memória, pode fazer referência toohello tamanho de função de VMs de IAAS e ver Olá número de núcleos e a memória atribuída. |
    | Nome a apresentar |Após a reativação pós-falha tooon no local, pode mudar o nome de máquinas virtuais Olá como irá aparecem no inventário de vCenter Olá. nome de predefinido de Olá é o nome de anfitrião do computador de máquina virtual de Olá. nome da VM tooidentify Olá, pode ver lista VM toohello no grupo de proteção de Olá. |
    | Configuração de NAT |Abordada em detalhe abaixo |

    ![](./media/site-recovery-failback-azure-to-vmware/image27.png)

#### <a name="configure-nat-settings"></a>Configurar definições de NAT
1. tooenable proteção de máquinas virtuais de Olá, precisam de dois canais de comunicação toobe estabelecida. canal primeiro Olá está entre a máquina virtual de Olá e servidor de processos de Olá. Este canal recolhe dados de Olá do Olá VM e envia-o servidor de processos de toohello que, em seguida, envia Olá servidor de destino mestre toohello de dados. Se o servidor de processos de Olá Olá toobe de máquina virtual protegida, sendo no Olá mesma rede virtual do Azure, em seguida, que não precisa de definições de NAT toouse. Caso contrário, especifique as definições de NAT. Ver o endereço IP público Olá hello do servidor de processos no Azure.

    ![](./media/site-recovery-failback-azure-to-vmware/image28.png)
2. canal segundo Olá está entre o servidor de processos de Olá e servidor de destino mestre Olá. Olá opção toouse NAT ou depende não estiver a utilizar uma ligação VPN com base ou a comunicar através de Olá internet. Não selecione NAt se estiver a utilizar VPN, mas apenas se estiver a utilizar uma ligação à internet.

    ![](./media/site-recovery-failback-azure-to-vmware/image29.png)

    ![](./media/site-recovery-failback-azure-to-vmware/image30.png)
3. Se ainda não eliminar Olá no local as máquinas virtuais, conforme especificado e se Olá arquivo de dados é toostill anterior falhar contém do VMDK Olá antigo, terá tooensure esse reativação pós-falha Olá VM obtém criada um novo local. toodo este Olá selecione **avançadas** definições e especifique uma alternativa toorestore tooin da pasta **definições de nome de pasta**. Deixe Olá outras opções com as respetivas predefinições. Aplica Olá pasta definições tooall Olá servidores de nomes de.

    ![](./media/site-recovery-failback-azure-to-vmware/image31.png)
4. Executar uma verificação de preparação tooensure que as máquinas virtuais de Olá são toobe pronto protegido local tooon anterior.

    ![](./media/site-recovery-failback-azure-to-vmware/image32.png)
5. Aguarde pela respetiva toocomplete. Se estiver com êxito em todas as VMs pode especificar um nome para o plano de proteção de Olá. Em seguida, clique em **proteger** toobegin.

    ![](./media/site-recovery-failback-azure-to-vmware/image33.png)
6. Pode monitorizar o progresso na vContinuum.

    ![](./media/site-recovery-failback-azure-to-vmware/image34.png)
7. Após o passo de Olá **ativar proteção planear** estiver concluída, pode monitorizar a proteção de VM no portal de recuperação de Site Olá.

    ![](./media/site-recovery-failback-azure-to-vmware/image35.png)
8. Pode ver estado exato de Olá clicando no Olá VM e monitorizar o respetivo progresso.

    ![](./media/site-recovery-failback-azure-to-vmware/image36.png)

## <a name="prepare-hello-failback-plan"></a>Preparar o plano de reativação pós-falha Olá
Pode preparar um plano de reativação pós-falha utilizando vContinuum para que a aplicação Olá pode ser toohello back-falha no local em qualquer altura. Estes planos de recuperação são muito semelhantes planos de recuperação de toohello no Site Recovery.

1. Iniciar vContinuum e selecione **gerir planos** > **recuperar.** Pode ver a lista de todos os planos de Olá que tenham sido utilizado toofail ativação pós-falha das VMs. Pode utilizar Olá mesmo planos toorecover.

   ![](./media/site-recovery-failback-azure-to-vmware/image37.png)
2. Selecione o plano de proteção de Olá e todos os Olá VMs que pretende toorecover no mesmo. Quando selecionar cada VM, pode ver mais detalhes, incluindo do ESX server do Olá destino e o disco de VM de origem Olá. Clique em **seguinte** toobegin Olá assistente recuperar e selecione VMs Olá pretende toorecover.

    ![](./media/site-recovery-failback-azure-to-vmware/image38.png)
3. Pode recuperar com base em várias opções, mas recomendamos que utilize **etiqueta mais recente** e selecione **aplicar para todas as VMs** tooensure Olá dados mais recentes da máquina virtual de Olá será utilizado.
4. Executar Olá **verificar preparação.** Isto irá verificar se os parâmetros de direito de Olá são tooenable configurado VM recuperação. Clique em **seguinte** se todas as verificações de Olá forem efetuadas com êxito. Se não verifique o registo de Olá e resolva os erros de Olá.

    ![](./media/site-recovery-failback-azure-to-vmware/image39.png)
5. No **configuração de VM** Certifique-se de que as definições de recuperação Olá estão corretamente definidas. Pode alterar as definições da VM Olá se for necessário.

   ![](./media/site-recovery-failback-azure-to-vmware/image40.png)
6. Reveja a lista de Olá de máquinas virtuais que serão recuperadas e especificar uma ordem de recuperação. Tenha em atenção que as VMs estão listadas com o nome de anfitrião do computador Olá. Poderá ser Olá toomap difícil computador anfitrião nome toohello da máquina virtual.
   os nomes de Olá toomap, máquinas virtuais toohello aceda **Dashboard** no Azure e verificação de nome de anfitrião VM Olá.

    ![](./media/site-recovery-failback-azure-to-vmware/image41.png)
7. Especifique um nome de plano e selecione **recuperar mais tarde**. Recomendamos toorecover mais tarde, uma vez que a proteção inicial Olá poderão não estar completa.
8. Clique em **recuperar** toosave Olá plano ou acionador Olá recuperação se selecionou toorecover agora e não mais tarde. Pode verificar toosee de estado de recuperação Olá se plano Olá do foram guardado.

   ![](./media/site-recovery-failback-azure-to-vmware/image42.png)

   ![](./media/site-recovery-failback-azure-to-vmware/image43.png)

## <a name="recover-virtual-machines"></a>Recuperar máquinas virtuais
Depois do foi criado o plano de Olá, pode recuperar máquinas virtuais Olá. Antes de verificar que Olá virtual máquinas concluiu a sincronização. Se o estado de replicação mostra OK proteção Olá está concluída e limiar do RPO Olá foram cumprido. Pode verificar o estado de funcionamento nas propriedades VM Olá.

![](./media/site-recovery-failback-azure-to-vmware/image44.png)

Desative Olá máquinas virtuais do Azure antes de iniciar a recuperação de Olá. Isto garante que não existe nenhum "de divisão-brain" e que os utilizadores acedem apenas uma cópia da aplicação Olá.

1. Inicie Olá guardada o plano. No vContinuum selecione **Monitor** Olá planos. Isto apresenta uma lista de todos os planos de Olá que foram executados.

   ![](./media/site-recovery-failback-azure-to-vmware/image45.png)
2. Plano de Olá selecione no **recuperação** e clique em **iniciar**. Pode monitorizar a recuperação. Depois de tem sido ativadas VMs no pode ligar toothem no vCenter.

   ![](./media/site-recovery-failback-azure-to-vmware/image46.png)

## <a name="protect-tooazure-again-after-failback"></a>Proteger tooAzure novamente após a reativação pós-falha
Depois de concluir a reativação pós-falha provavelmente, será útil máquinas de virtuais tooprotect Olá novamente. Fazê-lo da seguinte forma:

1. Certifique-se de que o Olá máquinas virtuais no local está a funcionar e que as aplicações são acessíveis.
2. No portal do Azure Site Recovery Olá, selecione as máquinas virtuais de Olá e eliminá-los. Selecione proteção de Olá toodisable das máquinas de virtuais Olá. Isto garante que as VMs de Olá mais não estão protegidas.
3. No Azure eliminar Olá efetuada a ativação pós-falha de máquinas virtuais do Azure
4. Elimine a máquina virtual antigo de Olá no vSpehere. Estes são Olá VMs que pós-falha tooAzure anteriormente.
5. No portal de recuperação de Site Olá proteger Olá VMs recentemente a ativação pós-falha. Depois de se estão protegidas poder adicioná-los tooa plano de recuperação.

## <a name="next-steps"></a>Passos seguintes
* [Leia sobre](site-recovery-vmware-to-azure-classic.md) replicar máquinas virtuais VMware e tooAzure servidores físicos utilizando a implementação de Olá avançada.
