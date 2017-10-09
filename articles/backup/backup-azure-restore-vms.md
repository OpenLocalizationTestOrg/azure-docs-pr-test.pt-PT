---
title: "aaaRestore a máquinas virtuais a partir de cópia de segurança | Microsoft Docs"
description: "Saiba como toorestore uma máquina virtual do Azure a partir de uma recuperação do ponto de"
services: backup
documentationcenter: 
author: trinadhk
manager: shreeshd
editor: 
keywords: "restaurar a cópia de segurança; como toorestore; ponto de recuperação;"
ms.assetid: fed877b3-b496-49fb-99e4-653be7c23e3a
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: trinadhk; jimpark;
ms.openlocfilehash: 44c25f3248784accd1c2beaabb2c9a4dca3232d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="restore-virtual-machines-in-azure"></a>Restaurar máquinas virtuais no Azure
> [!div class="op_single_selector"]
> * [Restaurar VMs no portal do Azure](backup-azure-arm-restore-vms.md)
> * [Restaurar VMs no portal clássico](backup-azure-restore-vms.md)
>
>

Restaure um tooa de máquina virtual nova VM a partir de cópias de segurança de Olá armazenadas num cofre do Backup do Azure com Olá os seguintes passos.

> [!IMPORTANT]
> Agora pode atualizar os cópia de segurança cofres tooRecovery os cofres dos serviços. Para obter mais informações, consulte o artigo de Olá [atualizar um tooa do Cofre de cópia de segurança do cofre dos serviços de recuperação](backup-azure-upgrade-backup-to-recovery-services.md). Microsoft encoraja tooupgrade a cópia de segurança cofres dos cofres dos serviços de tooRecovery.<br/> **15 de Outubro de 2017**, deixará de estar cofres de cópia de segurança do toouse capaz de PowerShell toocreate. <br/> **A partir de 1 de novembro de 2017**:
>- Qualquer restantes cofres de cópia de segurança serão os cofres dos serviços de tooRecovery automaticamente atualizado.
>- Não será capaz de tooaccess os dados de cópia de segurança no portal clássico Olá. Em vez disso, utilize Olá tooaccess portal do Azure os dados de cópia de segurança cofres dos serviços de recuperação.
>

## <a name="restore-workflow"></a>Restaurar fluxo de trabalho
### <a name="step-1-choose-an-item-toorestore"></a>Passo 1: Selecione um item toorestore
1. Navegue toohello **itens protegidos** separador e selecione Olá máquina virtual que pretende toorestore tooa nova VM.

    ![Itens protegidos](./media/backup-azure-restore-vms/protected-items.png)

    Olá **ponto de recuperação** coluna na Olá **itens protegidos** página informará Olá o número de pontos de recuperação para uma máquina virtual. Olá **ponto de recuperação mais recente** coluna indica Olá tempo de Olá mais recente cópia de segurança do que uma máquina virtual pode ser restaurada.
2. Clique em **restaurar** tooopen Olá **restaurar um Item** assistente.

    ![Restaurar um item](./media/backup-azure-restore-vms/restore-item.png)

### <a name="step-2-pick-a-recovery-point"></a>Passo 2: Escolha um ponto de recuperação
1. No Olá **selecionar um ponto de recuperação** ecrã, pode restaurar Olá mais recente ponto de recuperação ou a partir de um ponto anterior no tempo. Olá opção predefinida selecionada quando é aberto o assistente é *ponto de recuperação mais recente*.

    ![Selecione um ponto de recuperação](./media/backup-azure-restore-vms/select-recovery-point.png)
2. toopick um ponto anterior no tempo, escolha Olá **selecione data** opção Olá pendente e selecione uma data no controlo de calendário Olá ao clicar no Olá **ícone de calendário**. No controlo Olá, todas as datas com pontos de recuperação são preenchidas com uma ligeira shade cinzento em são selecionáveis pelo utilizador Olá.

    ![Selecione uma data](./media/backup-azure-restore-vms/select-date.png)

    Assim que clicar numa data no controlo de calendário Olá, recuperação Olá pontos disponível em que data será mostrada na tabela de pontos de recuperação abaixo. Olá **tempo** coluna indica o tempo de Olá no qual Olá instantâneo foi tirado. Olá **tipo** coluna apresenta Olá [consistência](https://azure.microsoft.com/documentation/articles/backup-azure-vms/#consistency-of-recovery-points) Olá do ponto de recuperação. cabeçalho de tabela Olá mostra o número de Olá de pontos de recuperação disponíveis nesse dia parênteses.

    ![Pontos de recuperação](./media/backup-azure-restore-vms/recovery-points.png)
3. Selecione o ponto de recuperação Olá Olá **pontos de recuperação** tabela e clique em Olá seta toogo toohello seguinte ecrã seguinte.

### <a name="step-3-specify-a-destination-location"></a>Passo 3: Especificar uma localização de destino
1. No Olá **selecione Restaurar instância** ecrã especificar detalhes de onde toorestore Olá máquina virtual.

   * Especifique o nome da máquina virtual Olá: no serviço de nuvem especificada, o nome da máquina virtual Olá deve ser exclusivo. Não suportamos escrita excessiva de VM existente.
   * Selecione um serviço em nuvem para Olá VM: Isto é obrigatório para criar uma VM. Pode escolher tooeither utilize um serviço em nuvem existente ou criar um novo serviço de nuvem.

        Foi selecionado qualquer nome de serviço de nuvem deve ser globalmente exclusivo. Normalmente, o nome do serviço de nuvem de Olá obtém associado a um URL de destinado ao público no formato Olá [cloudservice]. cloudapp.net. Azure não permitirá toocreate um novo serviço em nuvem se já tiver sido utilizado o nome de Olá. Se optar por toocreate um novo serviço em nuvem, será fornecido Olá mesmo nome como máquina virtual de Olá – na qual Olá maiúsculas VM nome selecionado deve ser o serviço em nuvem do toobe exclusivo suficientemente aplicada toohello associado.

        Iremos apresentar apenas os serviços de nuvem e redes virtuais que não estão associados a quaisquer grupos de afinidades Olá restaurar detalhes de instância. [Saiba mais](../virtual-network/virtual-networks-migrate-to-regional-vnet.md).
2. Selecione uma conta de armazenamento para Olá VM: Isto é obrigatório para a criação de Olá VM. Pode selecionar das contas do storage existente na Olá mesma região que Olá Cofre de cópia de segurança do Azure. As contas de armazenamento que são zona redundante ou do tipo de armazenamento Premium não é suportada.

    Se não houver nenhuma conta de armazenamento com configuração suportada, crie uma conta de armazenamento de operação de restauro anterior toostarting configuração suportada.

    ![Selecione uma rede virtual](./media/backup-azure-restore-vms/restore-sa.png)
3. Selecione uma rede Virtual: rede de Olá virtual (VNET) para a máquina virtual de Olá deve ser selecionada no momento da criação da Olá Olá VM. Olá restaurar IU mostra todas as VNETs Olá dentro desta subscrição que podem ser utilizadas. Não é obrigatório tooselect uma VNET para Olá restaurada VM – será capaz de tooconnect toohello restaurada máquina através de Olá internet, mesmo se hello VNET não está aplicado.

    Se Olá na nuvem serviço selecionado está associado uma rede virtual, em seguida, o não é possível alterar a rede virtual Olá.

    ![Selecione uma rede virtual](./media/backup-azure-restore-vms/restore-cs-vnet.png)
4. Selecione uma sub-rede: no caso de Olá VNET tem sub-redes, por predefinição sub-rede primeiro Olá será selecionado. Escolha uma sub-rede de Olá à sua escolha das opções de lista pendente de Olá. Para detalhes de sub-rede, visite tooNetworks extensão no Olá [home page do portal](https://manage.windowsazure.com/), aceda demasiado**redes virtuais** e rede virtual Olá selecione e desagregação para configurar os detalhes da sub-rede toosee.

    ![Selecione uma sub-rede](./media/backup-azure-restore-vms/select-subnet.png)
5. Clique em Olá **submeter** ícone na Olá assistente toosubmit Olá detalhes e criar uma tarefa de restauro.

## <a name="track-hello-restore-operation"></a>Controlar a operação de restauro Olá
Depois de ter todas as informações de Olá no Assistente de restauro Olá de entrada e submetido-cópia de segurança do Azure tentará toocreate uma operação de restauro do tarefa tootrack Olá.

![Criar uma tarefa de restauro](./media/backup-azure-restore-vms/create-restore-job.png)

Se a criação da tarefa de Olá for bem sucedida, verá uma notificação de alerta a indicar que essa tarefa Olá é criada. Pode obter mais detalhes clicando Olá **ver tarefa** botão que irá demorar demasiado**tarefas** separador.

![Restaurar tarefa criada](./media/backup-azure-restore-vms/restore-job-created.png)

Depois de concluída a operação de restauro Olá, será marcada como concluído no **tarefas** separador.

![Restaurar tarefa concluída](./media/backup-azure-restore-vms/restore-job-complete.png)

Depois de restaurar Olá a máquina virtual poderá ter extensões de Olá toore instalação existente no Olá original VM e [modificar pontos finais de Olá](../virtual-machines/windows/classic/setup-endpoints.md) para a máquina virtual de Olá no Olá portal do Azure.

## <a name="post-restore-steps"></a>Passos de pós-restauro
Se estiver a utilizar uma distribuição de Linux baseado em nuvem-init, tais como Ubuntu, por motivos de segurança, palavra-passe será bloqueada após o restauro. . Utilize extensão VMAccess Olá restaurada VM demasiado[Olá de reposição de palavra-passe](../virtual-machines/linux/classic/reset-access.md). Recomendamos a utilização de chaves SSH nestes tooavoid distribuições Repor palavra-passe post restauro.

## <a name="backup-for-restored-vms"></a>Cópia de segurança para VMs restauradas
Caso tenha restaurado VM toosame o serviço em nuvem com o mesmo nome como originalmente cópias de segurança VM de Olá, cópia de segurança irá continuar em Olá restauro de post VM. Se tiver de restaurar um serviço cloud diferente tooa VM ou especificar um nome diferente para a VM restaurada, este será tratado como uma nova VM, sendo necessário toosetup cópia de segurança para a VM restaurada.

## <a name="restoring-a-vm-during-azure-datacenter-disaster"></a>Restaurar uma VM durante desastre de centro de dados do Azure
Cópia de segurança do Azure permite restaurar uma cópia de segurança VMs toohello emparelhado Datacenter no caso do Centro de dados principal olá onde as VMs estão em execução experiências desastre e configurou toobe do Cofre de cópia de segurança georredundante. Durante a tais cenários, terá de tooselect uma conta de armazenamento que está presente no Centro de dados emparelhado e rest do processo de restauro Olá permanece o mesmo. Cópia de segurança do Azure utiliza o serviço de computação da máquina virtual do georreplicação emparelhado toocreate Olá restaurada. Saiba mais sobre [resiliência do Centro de dados do Azure](../resiliency/resiliency-technical-guidance-recovery-loss-azure-region.md)

## <a name="restoring-domain-controller-vms"></a>Restaurar VMs do controlador de domínio
Cópia de segurança de máquinas de virtuais do controlador de domínio (DC) é um cenário suportado com o Backup do Azure. No entanto, deve ter cuidado durante o processo de restauro Olá. processo de restauro correto de Olá depende da estrutura de Olá do domínio Olá. Caso mais simples de Olá tem um único controlador de domínio num único domínio. Mais frequentemente para cargas de produção, terá um único domínio com vários controladores de domínio, talvez com alguns DCs no local. Por fim, pode ter uma floresta com vários domínios.

A partir de um Olá de perspetiva do Active Directory o VM do Azure é como qualquer outra VM num hipervisor suportado Moderno. Olá principais diferença com hipervisores no local é que não há nenhuma consola da VM no Azure. Uma consola é necessária para determinados cenários tais como recuperar utilizando uma cópia de segurança do tipo de recuperação Bare bare Metal (BMR). No entanto, o restauro de VM do Cofre de cópia de segurança de Olá é uma substituição completa para a BMR. Modo de restauro de diretório Active Directory (DSRM), também está disponível, pelo que todos os cenários de recuperação do Active Directory são viável. Para obter mais informações em segundo plano, verifique [cópia de segurança e restauro considerações para controladores de domínio virtualizado](https://technet.microsoft.com/en-us/library/virtual_active_directory_domain_controller_virtualization_hyperv(v=ws.10).aspx#backup_and_restore_considerations_for_virtualized_domain_controllers) e [planear a recuperação de floresta do Active Directory](https://technet.microsoft.com/en-us/library/planning-active-directory-forest-recovery(v=ws.10).aspx).

### <a name="single-dc-in-a-single-domain"></a>Único DC num domínio único
Olá VM pode ser restaurada (como outra VM) de Olá Azure portal ou com o PowerShell.

### <a name="multiple-dcs-in-a-single-domain"></a>Vários controladores de domínio num domínio único
Quando restantes DCs do mesmo domínio pode ser contactado através de Olá hello rede, pode ser restaurada Olá DC como qualquer VM. Se for Olá último DC restantes no domínio Olá ou uma recuperação numa rede isolada é executada, tem de ser seguido um procedimento de recuperação de floresta.

### <a name="multiple-domains-in-one-forest"></a>Vários domínios numa floresta
Quando restantes DCs do mesmo domínio pode ser contactado através de Olá hello rede, pode ser restaurada Olá DC como qualquer VM. No entanto, todos os outros casos é recomendada uma recuperação de floresta.

<!--- WK: this following original supportability statement is incorrect, taking it out.
hello challenge arises because DSRM mode is not present in Azure. So toorestore such a VM, you cannot use hello Azure portal. hello only supported restore mechanism is disk-based restore using PowerShell.

> [!WARNING]
> For Domain Controller VMs in a multi-DC environment, do not use hello Azure portal for restore! Only PowerShell based restore is supported
>
>

Read more about hello [USN rollback problem](https://technet.microsoft.com/library/dd363553) and hello strategies suggested toofix it.
--->

## <a name="restoring-vms-with-special-network-configurations"></a>Restaurar VMs com configurações de rede especiais
Cópia de segurança do Azure suporta a cópia de segurança seguintes configurações de rede especiais de máquinas virtuais.

* VMs no balanceador de carga (interno e externo)
* VMs com vários IPs reservados
* VMs com vários NICs

Estas configurações mandatar seguintes considerações ao restaurá-los.

> [!TIP]
> Utilize o PowerShell com base em restauro fluxo toorecreate Olá especial configuração de rede de VMs post restauro.
>
>

### <a name="restoring-from-hello-ui"></a>Restaurar a partir da IU do Olá:
Enquanto restaurava a partir da IU, **sempre escolher um novo serviço em nuvem**. Tenha em atenção que uma vez que o portal só leva obrigatório parâmetros durante o fluxo de restauro, VMs restaurados com autoridade utilizando a IU irão perder a configuração de rede especiais de Olá que possuem. Por outras palavras, restaurar VMs ficará VMs normais sem configuração de Balanceador de carga ou várias NIC ou vários IP reservado.

### <a name="restoring-from-powershell"></a>Restaurar a partir do PowerShell:
PowerShell tem Olá capacidade toojust restaurar os discos da VM Olá da cópia de segurança e não criar a máquina virtual de Olá. Esta ação é útil quando o restauro de máquinas virtuais que requerem configurações de rede especiais mencionadas acima.

Ordem toofully recriar post de máquina virtual de Olá restauro dos discos, siga estes passos:

1. Restaurar os discos de Olá da utilização do Cofre de cópia de segurança [PowerShell de cópia de segurança do Azure](backup-azure-vms-classic-automation.md#restore-an-azure-vm)
2. Criar a configuração VM de Olá necessária para o Balanceador de carga / vários NIC/vários reservado IP com Olá cmdlets do PowerShell e utilizá-la toocreate Olá VM de configuração pretendida.

   * Criar a VM no serviço em nuvem com [Balanceador de carga interno](https://azure.microsoft.com/documentation/articles/load-balancer-internal-getstarted/)
   * Criar a VM tooconnect demasiado[Internet com o Balanceador de carga](https://azure.microsoft.com/en-us/documentation/articles/load-balancer-internet-getstarted/)
   * Criar a VM com [vários NICs](https://azure.microsoft.com/documentation/articles/virtual-networks-multiple-nics/)
   * Criar a VM com [vários reservado IPs](https://azure.microsoft.com/documentation/articles/virtual-networks-reserved-public-ip/)

## <a name="next-steps"></a>Passos seguintes
* [Resolução de problemas de erros](backup-azure-vms-troubleshoot.md#restore)
* [Gerir máquinas virtuais](backup-azure-manage-vms.md)
