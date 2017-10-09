---
title: "Cópia de segurança do Azure: Restaurar máquinas virtuais utilizando o portal do Azure de Olá | Microsoft Docs"
description: "Restaurar uma máquina virtual do Azure a partir de um ponto de recuperação através do portal do Azure"
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
keywords: "restaurar a cópia de segurança; como toorestore; ponto de recuperação;"
ms.assetid: 372b87c6-3544-4dc5-bbc9-c742ca502159
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/15/2017
ms.author: markgal;trinadhk;
ms.openlocfilehash: f4f75d1da73c7760d2952afe80ff94918a08351c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-portal-toorestore-virtual-machines"></a>Utilize máquinas virtuais de toorestore portal do Azure
> [!div class="op_single_selector"]
> * [Restaurar VMs no portal clássico](backup-azure-restore-vms.md)
> * [Restaurar VMs no portal do Azure](backup-azure-arm-restore-vms.md)
>
>

Proteger os seus dados, efetuando os instantâneos dos seus dados em intervalos definidos. Estes instantâneos são conhecidos como pontos de recuperação e que estão armazenados nos cofres dos serviços de recuperação. Se, ou quando for necessário toorepair ou reconstruir uma VM, pode restaurar Olá VM a partir de qualquer um dos Olá guardado pontos de recuperação. Quando restaurar um ponto de recuperação, pode criar uma nova VM, que é uma representação de ponto no tempo da sua VM de cópia de segurança, ou restaurar os discos e utilizar o modelo Olá que vem com o mesmo toocustomize Olá restaurada VM ou efetuar uma recuperação de ficheiros individuais. Este artigo explica como toorestore tooa uma VM nova VM ou discos de restauro todos os cópia de segurança. Recuperação de ficheiros individuais, consulte demasiado[recuperar ficheiros de cópia de segurança de VM do Azure](backup-azure-restore-files-from-vm.md)

![3-ways-Restore-from-VM-backup](./media/backup-azure-arm-restore-vms/azure-vm-backup-restore.png)

> [!NOTE]
> O Azure tem dois modelos de implementação para criar e trabalhar com recursos: [Resource Manager e clássico](../azure-resource-manager/resource-manager-deployment-model.md). Este artigo fornece informações de Olá e procedimentos para restaurar VMs implementadas utilizando o modelo do Resource Manager Olá.
>
>

Restaurar uma VM ou todos os discos de VM a cópia de segurança envolve dois passos:

1. Selecione um ponto de restauro do restauro
2. Selecionar Olá restaurar tipo - criar uma nova VM ou restaurar os discos e especificar os parâmetros necessários. 

## <a name="select-restore-point-for-restore"></a>Selecione o ponto de restauro do restauro
1. Inicie sessão no toohello [portal do Azure](http://portal.azure.com/)
2. No menu do Azure Olá, clique em **procurar** e, na lista de Olá de serviços, escreva **dos serviços de recuperação**. lista de Olá de serviços ajusta toowhat que escrever. Quando vir **cofres dos serviços de recuperação**, selecione-o.

    ![Abra o Cofre dos serviços de recuperação](./media/backup-azure-arm-restore-vms/open-recovery-services-vault.png)

    é apresentada a lista de Olá de cofres na subscrição Olá.

    ![Lista de serviços de recuperação cofres dos](./media/backup-azure-arm-restore-vms/list-of-rs-vaults.png)
3. Na lista de Olá, cofre Olá selecione associado Olá VM pretende toorestore. Ao clicar cofre Olá, abre o dashboard.

    ![Lista de serviços de recuperação cofres dos](./media/backup-azure-arm-restore-vms/select-vault-open-vault-blade.png)
4. Agora que está no dashboard do cofre Olá. No Olá **itens de cópia de segurança** mosaico, clique em **Virtual Machines do Azure** toodisplay Olá VMs associados com o Cofre de Olá.

    ![dashboard do Cofre](./media/backup-azure-arm-restore-vms/vault-dashboard.png)

    Olá **itens de cópia de segurança** painel abre e apresenta a lista de Olá de máquinas virtuais do Azure.

    ![lista de VMs no Cofre](./media/backup-azure-arm-restore-vms/list-of-vms-in-vault.png)
5. Na lista de Olá, selecione um dashboard de Olá tooopen VM. dashboard VM Olá abre toohello área de monitorização, que contém o mosaico de pontos de restauro Olá.

    ![lista de VMs no Cofre](./media/backup-azure-arm-restore-vms/vm-blade.png)
6. No menu do dashboard VM de Olá, clique em **restaurar**

    ![lista de VMs no Cofre](./media/backup-azure-arm-restore-vms/vm-blade-menu-restore.png)

    é aberto o painel de restauro de Olá.

    ![restaurar painel](./media/backup-azure-arm-restore-vms/restore-blade.png)
7. No Olá **restaurar** painel, clique em **ponto de restauro** tooopen Olá **selecione Restaurar ponto** painel.

    ![restaurar painel](./media/backup-azure-arm-restore-vms/recovery-point-selector.png)

    Por predefinição, o diálogo Olá apresenta todos os pontos de restauro de Olá últimos 30 dias. Olá utilize **filtro** intervalo de tempo de Olá tooalter do Olá restaurar pontos apresentados. Por predefinição, são apresentados os pontos de restauro de todos os consistência. Modificar **restaurar todos os pontos** filtrar tooselect uma consistência específica de pontos de restauro. Para obter mais informações sobre cada tipo de ponto de restauro, consulte a explicação sobre Olá [consistência dos dados](backup-azure-vms-introduction.md#data-consistency).  

   * **Restaurar o ponto de consistência** desta lista escolha:
     * Pontos de restauro consistentes de falhas
     * Pontos de restauro consistentes da aplicação,
     * Pontos de restauro consistentes do sistema de ficheiros
     * Restaurar todos os pontos.  
8. Escolha um ponto de restauro e clique em **OK**.

    ![Escolha o ponto de restauro](./media/backup-azure-arm-restore-vms/select-recovery-point.png)

    Olá **restaurar** painel mostra Olá ponto de restauro está definido.

    ![ponto de restauro está definido](./media/backup-azure-arm-restore-vms/recovery-point-set.png)
9. No Olá **restaurar** painel, **restauro configuração** abre-se automaticamente após o ponto de restauro está definido.

## <a name="choosing-a-vm-restore-configuration"></a>Escolher uma configuração de restauro de VM
Agora que tiver selecionado o ponto de restauro Olá, escolha uma configuração para o restauro de VM. As opções para configurar Olá restaurada VM são toouse: portal do Azure ou o PowerShell.

1. Se não estiver já existir, avance toohello **restaurar** painel. Certifique-se de um [foi selecionado o ponto de restauro](#select-restore-point-for-restore)e clique em **restauro configuração** tooopen Olá **configuração da recuperação** painel.

    ![Assistente de configuração de recuperação está definido](./media/backup-azure-arm-restore-vms/recovery-configuration-wizard-recovery-type.png)
2. No Olá **restauro configuração** painel, tem duas opções:
   * Restaurar a máquina de virtual completa
   * Restaurar uma cópia de segurança discos

Portal fornece uma opção de criação rápida para a VM restaurada. Se pretender que a configuração de VM de Olá toocustomize ou nomes de recursos de Olá criados como parte de criar uma nova opção VM, utilize o PowerShell ou portal toorestore cópia de segurança discos e utilizar tooattach de comandos do PowerShell-los toochoice de modelo de utilização ou de configuração de VM que é fornecido com o restauro Olá de toocustomize discos restaurada a VM. Consulte [restaurar uma VM com configurações de rede especiais](#restoring-vms-with-special-network-configurations) para obter detalhes sobre como toorestore VM que tem vários NICs ou sob o Balanceador de carga. Se a VM do Windows utiliza [HUB licenciamento](../virtual-machines/windows/hybrid-use-benefit-licensing.md), precisa de discos de toorestore e utilizar o PowerShell/modelo conforme especificado abaixo toocreate Olá VM e certifique-se de que especificou LicenseType como "Windows_Server" durante a criação de VM tooavail HUB vantagens em VM restaurada. 
 
## <a name="create-a-new-vm-from-restore-point"></a>Criar uma nova VM a partir do ponto de restauro
Se não estiver já existe, [selecionar um ponto de restauro](#restoring-vms-with-special-network-configurations) antes de continuar toocreating uma nova VM a partir de restauro do ponto. Assim que o ponto de restauro está selecionado, no Olá **restauro configuração** painel, introduza ou selecione os valores para cada um dos Olá seguintes campos:

* **Restaurar tipo** -criar a máquina virtual.
* **Nome da máquina virtual** -forneça um nome para Olá VM. nome de Olá tem de ser exclusivo toohello o grupo de recursos (para uma VM implementadas no Resource Manager) ou serviço em nuvem (para uma VM clássico). Não é possível substituir a máquina virtual de Olá se já existe na subscrição Olá.
* **Grupo de recursos** - utilizar um grupo de recursos existente ou crie um novo. Se estiver a restaurar uma VMS clássicas, utilize este toospecify Olá o nome do campo de um novo serviço em nuvem. Se estiver a criar um novo serviço de nuvem/grupo de recursos, o nome de Olá deve ser globalmente exclusivo. Normalmente, nome do serviço de nuvem de Olá está associado um URL de destinado ao público - por exemplo: [cloudservice]. cloudapp.net. Se tentar toouse um nome para o serviço nuvem/grupo de recursos de nuvem de Olá que já tenha sido utilizado, o serviço de nuvem/grupo de recursos do Azure atribui Olá Olá mesmo nome como Olá VM. Azure apresenta recursos grupos/cloud services e as VMs que não associadas a quaisquer grupos de afinidade. Para obter mais informações, consulte [como toomigrate de tooa de grupos de afinidade de rede Virtual Regional (VNet)](../virtual-network/virtual-networks-migrate-to-regional-vnet.md).
* **Rede virtual** - selecione Olá de rede virtual de Olá (VNET) durante a criação de VM. campo de Olá fornece todas as VNETs associadas à subscrição Olá. Grupo de recursos Olá VM é apresentado no parênteses.
* **Sub-rede** -se Olá VNET tiver sub-redes, a primeira sub-rede da Olá está selecionada por predefinição. Se existirem sub-redes adicionais, selecione a sub-rede Olá assim o desejar.
* **Conta de armazenamento** -este menu apresenta uma lista de contas de armazenamento Olá na Olá Olá mesma localização do cofre dos serviços de recuperação. As contas de armazenamento que são zona redundante não são suportadas. Se existirem não existem contas de armazenamento com hello mesma localização que Olá dos serviços de recuperação cofre, tem de criar um antes de iniciar a operação de restauro Olá. tipo de replicação de uma conta de armazenamento Olá é mencionado na parênteses.

![Assistente de configuração de restauro está definido](./media/backup-azure-arm-restore-vms/recovery-configuration-wizard.png)

> [!NOTE]
> 1. Se estiver a restaurar uma VM implementadas no Resource Manager, tem de identificar uma rede virtual (VNET). Uma rede virtual (VNET) é opcional para uma VM clássico.
> 2. Se estiver a restaurar VMs com discos geridos, certifique-se de que conta de armazenamento selecionada não está ativada para Encryption(SSE) do serviço de armazenamento no seu período de duração.
> 3. Com base no tipo de armazenamento Olá da conta de armazenamento selecionada (premium ou standard), todos os discos restaurados será premium ou discos padrão. Não é atualmente suportado modo misto de discos ao restaurar.  
>
>

No Olá **restauro configuração** painel, clique em **OK** configuração de restauro de Olá toofinalize. No Olá **restaurar** painel, clique em **restaurar** operação de restauro de Olá tootrigger.

## <a name="restore-backed-up-disks"></a>Restaurar uma cópia de segurança discos
Se quiser toocustomize Olá virtual máquina que pretende toocreate de uma cópia de segurança discos de que está presente no painel de configuração de restauro, selecione **restaurar discos** como valor para **restaurar tipo**. Esta opção pede-lhe uma conta do storage onde os discos de cópias de segurança são copiados. Ao escolher uma conta de armazenamento, selecione uma conta partilhas Olá mesma localização, como o Cofre dos serviços de recuperação Olá. As contas de armazenamento que são zona redundante não são suportadas. Se existirem não existem contas de armazenamento com hello mesma localização que Olá dos serviços de recuperação cofre, tem de criar um antes de iniciar a operação de restauro Olá. tipo de replicação de uma conta de armazenamento Olá é mencionado na parênteses.

Depois de concluída a operação de restauro, pode:
* [Olá de toocustomize do modelo de utilização restaurada VM](#use-templates-to-customize-restore-vm)
* [Olá utilize restaurada discos tooattach tooan máquina virtual](../virtual-machines/windows/attach-managed-disk-portal.md)
* [Crie uma nova máquina virtual através do PowerShell de discos restaurados.](./backup-azure-vms-automation.md#restore-an-azure-vm)

No Olá **restauro configuração** painel, clique em **OK** configuração de restauro de Olá toofinalize. No Olá **restaurar** painel, clique em **restaurar** operação de restauro de Olá tootrigger.

![Configuração de recuperação concluída](./media/backup-azure-arm-restore-vms/trigger-restore-operation.png)

## <a name="track-hello-restore-operation"></a>Controlar a operação de restauro Olá
Assim que o acionar a operação de restauro Olá, Olá serviço de cópia de segurança cria uma tarefa para a operação de restauro Olá de controlo. Olá serviço de cópia de segurança também cria e apresenta temporariamente notificação Olá na área de notificações do portal. Se não vir a notificação de Olá, pode sempre clicar tooview de ícone de notificações de Olá as notificações.

![Restauro acionado](./media/backup-azure-arm-restore-vms/restore-notification.png)

operação de Olá tooview enquanto estiver a processar ou tooview quando tiver terminado, abrir lista de tarefas de cópia de segurança de Olá.

1. No menu do Azure Olá, clique em **procurar** e, na lista de Olá de serviços, escreva **dos serviços de recuperação**. lista de Olá de serviços ajusta toowhat que escrever. Quando vir **cofres dos serviços de recuperação**, selecione-o.

    ![Abra o Cofre dos serviços de recuperação](./media/backup-azure-arm-restore-vms/open-recovery-services-vault.png)

    é apresentada a lista de Olá de cofres na subscrição Olá.

    ![Lista de serviços de recuperação cofres dos](./media/backup-azure-arm-restore-vms/list-of-rs-vaults.png)
2. Na lista de Olá, cofre Olá selecione associado Olá VM é restaurada. Ao clicar cofre Olá, abre o dashboard.
3. No dashboard do cofre Olá no Olá **tarefas de cópia de segurança** mosaico, clique em **Virtual Machines do Azure** tarefas de Olá toodisplay associadas Olá cofre.

    ![dashboard do Cofre](./media/backup-azure-arm-restore-vms/vault-dashboard-jobs.png)

    Olá **tarefas de cópia de segurança** painel abre e apresenta a lista de Olá de tarefas.

    ![lista de VMs no Cofre](./media/backup-azure-arm-restore-vms/restore-job-in-progress.png)
    
## <a name="use-templates-toocustomize-restore-vm"></a>Utilizar modelos toocustomize restauro vm
Uma vez [concluir a operação de restauro do discos](#Track-the-restore-operation), pode utilizar o modelo de Olá que é gerado como parte da operação de restauro toocreate uma nova VM com uma configuração diferente dos nomes de configuração ou toocustomize cópia de segurança de recursos criado como criar uma nova vm a partir do ponto de restauro. 

> [!NOTE]
> Modelos serão adicionados como parte dos discos de restaurar para pontos de recuperação efetuadas após 1 de Março de 2017. São aplicáveis para disco não encriptada e não geridas VMs. Suporte para VMs e as VMs de disco gerido encriptados estará disponível em versões futuras. 
>
>

modelo de Olá tooget gerado como parte da opção de discos de restauro,

1. Visite os detalhes da tarefa toorestore correspondente toohello tarefa. 
2. No ecrã de detalhes da tarefa do restauro Olá, clique em *implementar a modelo* botão tooinitiate a implementação do modelo. 

     ![restaurar tarefa desagregar](./media/backup-azure-arm-restore-vms/restore-job-drill-down.png)
   
No Olá implementar modelo Painel implementação personalizada, utilize a implementação do modelo demasiado[editar e implementar a modelo Olá](../azure-resource-manager/resource-group-template-deploy-portal.md#deploy-resources-from-custom-template) ou acrescentar mais personalizações pela [criar um modelo de](../azure-resource-manager/resource-group-authoring-templates.md) antes de implementar. 

   ![carregar a implementação do modelo](./media/backup-azure-arm-restore-vms/loading-template.png)
   
Depois de introduzir valores Olá necessário, aceitar Olá *termos e condições* e clique em **Compra**.

   ![a submeter a implementação do modelo](./media/backup-azure-arm-restore-vms/submitting-template.png)

## <a name="post-restore-steps"></a>Passos de pós-restauro
* Se estiver a utilizar uma distribuição de Linux baseado em nuvem-init, tais como Ubuntu, por motivos de segurança, a palavra-passe é bloqueado após o restauro. . Utilize extensão VMAccess Olá restaurada VM demasiado[Olá de reposição de palavra-passe](../virtual-machines/linux/classic/reset-access.md). Recomendamos a utilização de chaves SSH nestes tooavoid distribuições Repor palavra-passe post restauro.
* Extensões presentes durante a configuração de cópia de segurança de Olá serão instaladas, no entanto, não serão ativadas. Volte a instalar as extensões se vir qualquer problema. 
* Se Olá com cópia de segurança a VM tem o IP estático, o restauro de post, VM restaurada terão um conflito de tooavoid IP dinâmico quando criar restaurada a VM. Saiba mais sobre como pode [adicionar um toorestored IP estático VM](../virtual-network/virtual-networks-reserved-private-ip.md#how-to-add-a-static-internal-ip-to-an-existing-vm)
* VM restaurada não terão o conjunto de valores de disponibilidade. Recomendamos que utilize a opção de discos de restauro e [adicionar conjunto de disponibilidade](../virtual-machines/windows/tutorial-availability-sets.md) quando criar uma VM a partir do PowerShell ou modelos utilizando discos de restaurado. 


## <a name="backup-for-restored-vms"></a>Cópia de segurança para VMs restauradas
Caso tenha restaurado VM toosame grupo de recursos com o mesmo nome como originalmente cópias de segurança VM de Olá, cópia de segurança continua em Olá o restauro de post VM. Se tiver de restaurar o grupo de recursos do VM tooa diferente ou especificado um nome diferente para a VM restaurada, esta é tratada como uma nova VM e que precisa toosetup cópia de segurança para a VM restaurada.

## <a name="restoring-a-vm-during-azure-datacenter-disaster"></a>Restaurar uma VM durante a desastres do dataCenter do Azure
Cópia de segurança do Azure permite restaurar uma cópia de segurança VMs toohello emparelhado Datacenter no caso do Centro de dados principal olá onde as VMs estão em execução experiências desastre e configurou toobe do Cofre de cópia de segurança georredundante. Durante a tais cenários, terá de tooselect uma conta de armazenamento, que está presente no Centro de dados emparelhado e rest do processo de restauro Olá permanece o mesmo. Cópia de segurança do Azure utiliza o serviço de computação da máquina virtual do georreplicação emparelhado toocreate Olá restaurada. Saiba mais sobre [resiliência do Centro de dados do Azure](../resiliency/resiliency-technical-guidance-recovery-loss-azure-region.md)

## <a name="restoring-domain-controller-vms"></a>Restaurar VMs do controlador de domínio
Cópia de segurança de máquinas de virtuais do controlador de domínio (DC) é um cenário suportado com o Backup do Azure. No entanto, deve ter cuidado durante o processo de restauro Olá. processo de restauro correto de Olá depende da estrutura de Olá do domínio Olá. Caso mais simples de Olá tem um único controlador de domínio num único domínio. Mais frequentemente para cargas de produção, terá um único domínio com vários controladores de domínio, talvez com alguns DCs no local. Por fim, pode ter uma floresta com vários domínios. 

A partir de um Olá de perspetiva do Active Directory o VM do Azure é como qualquer outra VM num hipervisor suportado Moderno. Olá principais diferença com hipervisores no local é que não há nenhuma consola da VM no Azure. Uma consola é necessária para determinados cenários tais como recuperar utilizando uma cópia de segurança do tipo de recuperação Bare bare Metal (BMR). No entanto, o restauro de VM do Cofre de cópia de segurança de Olá é uma substituição completa para a BMR. Modo de restauro de diretório Active Directory (DSRM), também está disponível, pelo que todos os cenários de recuperação do Active Directory são viável. Para obter mais informações em segundo plano, verifique [cópia de segurança e restauro considerações para controladores de domínio virtualizado](https://technet.microsoft.com/en-us/library/virtual_active_directory_domain_controller_virtualization_hyperv(v=ws.10).aspx#backup_and_restore_considerations_for_virtualized_domain_controllers) e [planear a recuperação de floresta do Active Directory](https://technet.microsoft.com/en-us/library/planning-active-directory-forest-recovery(v=ws.10).aspx).

### <a name="single-dc-in-a-single-domain"></a>Único DC num domínio único
Olá VM pode ser restaurada (como outra VM) de Olá Azure portal ou com o PowerShell.

### <a name="multiple-dcs-in-a-single-domain"></a>Vários controladores de domínio num domínio único
Quando restantes DCs do mesmo domínio pode ser contactado através de Olá hello rede, pode ser restaurada Olá DC como qualquer VM. Se for Olá último DC restantes no domínio Olá ou uma recuperação numa rede isolada é executada, tem de ser seguido um procedimento de recuperação de floresta.

### <a name="multiple-domains-in-one-forest"></a>Vários domínios numa floresta
Quando restantes DCs do mesmo domínio pode ser contactado através de Olá hello rede, pode ser restaurada Olá DC como qualquer VM. No entanto, todos os outros casos é recomendada uma recuperação de floresta.

## <a name="restoring-vms-with-special-network-configurations"></a>Restaurar VMs com configurações de rede especiais
É possível tooback cópias de segurança e restaurar VMs com Olá seguintes configurações de rede especiais. No entanto, estas configurações requerem algum especial atenção ao percorrer o processo de restauro Olá.

* VMs no balanceador de carga (interno e externo)
* VMs com vários IPs reservados
* VMs com vários NICs

> [!IMPORTANT]
> Ao criar a configuração de rede especiais Olá para VMs, tem de utilizar o PowerShell toocreate VMs de discos de Olá restauradas.
>
>

máquinas virtuais do toofully recrie Olá após o restauro toodisk, siga estes passos:

1. Restaurar os discos de Olá a partir dos serviços de recuperação cofre utilizando [PowerShell](backup-azure-vms-automation.md#restore-an-azure-vm)
2. Criar a configuração de VM de Olá necessária para o Balanceador de carga / vários NIC/vários reservado IP com Olá cmdlets do PowerShell e utilizá-la toocreate Olá VM de configuração pretendida.

   * Criar a VM no serviço em nuvem com [Balanceador de carga interno](https://azure.microsoft.com/documentation/articles/load-balancer-internal-getstarted/)
   * Criar a VM tooconnect demasiado[Internet com o Balanceador de carga](https://azure.microsoft.com/en-us/documentation/articles/load-balancer-internet-getstarted/)
   * Criar a VM com [vários NICs](https://azure.microsoft.com/documentation/articles/virtual-networks-multiple-nics/)
   * Criar a VM com [vários reservado IPs](https://azure.microsoft.com/documentation/articles/virtual-networks-reserved-public-ip/)

## <a name="next-steps"></a>Passos seguintes
Agora que pode restaurar as suas VMs, consulte Olá artigo para obter informações sobre erros comuns com VMs de resolução de problemas. Além disso, consulte o artigo de Olá na gestão de tarefas com as suas VMs.

* [Resolução de problemas de erros](backup-azure-vms-troubleshoot.md#restore)
* [Gerir máquinas virtuais](backup-azure-manage-vms.md)
