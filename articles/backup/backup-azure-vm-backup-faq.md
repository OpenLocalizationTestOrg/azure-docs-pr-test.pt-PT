---
title: FAQ sobre o Azure VM Backup | Microsoft Docs
description: "Respostas a perguntas comuns sobre como funcionam as cópias de segurança de VMs do Azure, as limitações e o que ocorre quando há alterações a políticas"
services: backup
documentationcenter: 
author: trinadhk
manager: shreeshd
editor: 
keywords: "cópia de segurança de vm do azure, restauro de vm do azure, política de cópias de segurança"
ms.assetid: c4cd7ff6-8206-45a3-adf5-787f64dbd7e1
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/18/2017
ms.author: trinadhk;pullabhk;
ms.openlocfilehash: 9a08495c1b395871c04c0c2b06a6efbdb4bfeaa2
ms.sourcegitcommit: 1fbaa2ccda2fb826c74755d42a31835d9d30e05f
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 01/22/2018
---
# <a name="questions-about-the-azure-vm-backup-service"></a>Perguntas sobre o serviço Azure VM Backup
Este artigo tem respostas a perguntas comuns para o ajudar a compreender rapidamente os componentes do Azure VM Backup. Em algumas das respostas, existem ligações para os artigos que incluem informação abrangente. Também pode publicar perguntas sobre o serviço de Backup do Azure no [fórum de debate](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazureonlinebackup).

## <a name="configure-backup"></a>Configurar a cópia de segurança
### <a name="do-recovery-services-vaults-support-classic-vms-or-resource-manager-based-vms-br"></a>Os cofres dos Serviços de Recuperação suportam VMs clássicas ou VMs no Resource Manager? <br/>
Os cofres dos Serviços de Recuperação suportam ambos os modelos.  Pode criar uma cópia de segurança de uma VM clássica (criada no Portal clássico) ou de uma VM do Resource Manager (criada no portal do Azure) num cofre dos Serviços de Recuperação.

### <a name="what-configurations-are-not-supported-by-azure-vm-backup"></a>Que configurações não são suportadas pela cópia de segurança de VM do Azure?
Avance [sistemas operativos suportados](backup-azure-arm-vms-prepare.md#supported-operating-systems-for-backup) e [limitações de cópia de segurança](backup-azure-arm-vms-prepare.md#limitations-when-backing-up-and-restoring-a-vm)

### <a name="why-cant-i-see-my-vm-in-configure-backup-wizard"></a>Por que motivo não vejo a minha VM no assistente de configuração de cópias de segurança?
No Assistente de cópia de segurança de configurar, cópia de segurança do Azure só apresenta as VMs que são:
  * Ainda não estiver protegida pode verificar o estado da cópia de segurança de uma VM ao aceder ao painel VM e a verificar o estado de cópia de segurança a partir do Menu de definições. Saiba mais sobre como [Verificar o estado da cópia de segurança de uma VM](backup-azure-vms-first-look-arm.md#configure-the-backup-job-from-the-vm-management-blade)
  * Pertençam à mesma região que a VM

## <a name="backup"></a>Cópia de segurança
### <a name="will-on-demand-backup-job-follow-same-retention-schedule-as-scheduled-backups"></a>As tarefas de cópias de segurança a pedido seguem a mesma agenda de retenção que as cópias de segurança agendadas?
Não. Deve especificar o período de retenção para uma tarefa de cópia de segurança a pedido. Por predefinição, é mantido durante 30 dias quando acionado a partir do portal. 

### <a name="i-recently-enabled-azure-disk-encryption-on-some-vms-will-my-backups-continue-to-work"></a>Ativei recentemente o Azure Disk Encryption em algumas VMs. As minhas cópias de segurança vão continuar a funcionar?
Tem de dar permissões ao serviço Azure Backup para aceder ao Key Vault. Pode conceder estas permissões no PowerShell com os passos mencionados na secção *Enable Backup* (Ativar Cópia de Segurança) da documentação do [PowerShell](backup-azure-vms-automation.md).

### <a name="i-migrated-disks-of-a-vm-to-managed-disks-will-my-backups-continue-to-work"></a>Migrei discos de uma VM para discos geridos. As minhas cópias de segurança vão continuar a funcionar?
Sim, as cópias de segurança funcionam sem problemas e não tem necessidade de reconfigurar a cópia de segurança. 

### <a name="my-vm-is-shut-down-will-an-on-demand-or-a-scheduled-backup-work"></a>A minha VM está a ser encerrado. Será uma pedido ou um trabalho de cópia de segurança agendado?
Sim. Mesmo quando uma máquina é encerrada cópias de segurança funcionam e o ponto de recuperação está marcado como falhas consistente. Para obter mais detalhes, consulte a secção de consistência de dados em [neste artigo](backup-azure-vms-introduction.md#how-does-azure-back-up-virtual-machines)

### <a name="can-i-cancel-an-in-progress-backup-job"></a>Pode cancelar uma tarefa de cópia de segurança em curso?
Sim. Pode cancelar a tarefa de cópia de segurança se estiver na fase "Criar instantâneo". **Não é possível cancelar uma tarefa de transferência de dados de instantâneo esteja em curso**. 

### <a name="i-enabled-resource-group-lock-on-my-backed-up-managed-disk-vms-will-my-backups-continue-to-work"></a>Posso ativar o bloqueio do grupo de recursos no meu disco gerido com cópia de segurança de VMs. As minhas cópias de segurança vão continuar a funcionar?
Se o utilizador bloqueia o grupo de recursos, serviço de cópia de segurança não é possível eliminar os pontos de restauro mais antigos. Devido a esta novas cópias de segurança começam a falhar, há um limite de pontos de restauro 18 máxima imposta de back-end. Se as cópias de segurança estão a falhar com um erro interno após o bloqueio RG, siga estes [passos para remover o restauro do ponto de coleção](backup-azure-troubleshoot-vm-backup-fails-snapshot-timeout.md#backup-service-does-not-have-permission-to-delete-the-old-restore-points-due-to-resource-group-lock).

## <a name="restore"></a>Restauro
### <a name="how-do-i-decide-between-restoring-disks-versus-full-vm-restore"></a>Como posso decidir entre o restauro de discos e o restauro de VMs completo?
Considere Azure restauro completo da VM como uma opção de criação rápida. Restaure as alterações de opção de VM os nomes dos discos, contentores utilizadas por essas discos, endereços IP públicos e nomes de interface de rede. A alteração é necessário para manter a exclusividade de recursos criado durante a criação da VM. Mas não irá adicionar a VM ao conjunto de disponibilidade. 

Utilize os discos de restauro para:
  * Personalizar a VM que é criada a partir do ponto na configuração de tempo, como a alteração do tamanho
  * Adicionar configurações, o que não estão presentes no momento da cópia de segurança 
  * Controlar a convenção de nomenclatura para os recursos que são criados
  * Adicionar a VM ao conjunto de disponibilidade
  * Para qualquer outra configuração que pode ser conseguido utilizando apenas a definição do PowerShell/um modelo declarativo
  
### <a name="can-i-use-backups-of-unmanaged-disk-vm-to-restore-after-i-upgrade-my-disks-to-managed-disks"></a>Pode utilizar cópias de segurança de VM de disco não gerido para restaurar após posso atualizar o meu discos para discos geridos?
Sim, pode utilizar as cópias de segurança colocadas antes de migrar discos de não gerido para gerido. Por predefinição, restauro VM tarefa irá criar uma VM com discos não geridos. Pode utilizar a funcionalidade de discos de restauro para restaurar os discos e utilizá-los para criar uma VM em discos geridos. 

### <a name="what-is-the-procedure-to-restore-a-vm-to-a-restore-point-taken-before-the-conversion-from-unmanaged-to-managed-disks-was-done-for-a-vm"></a>O que é o procedimento para restaurar uma VM para um ponto de restauro colocado antes da conversão de não gerido para gerido discos foi realizada para uma VM?
Neste cenário, por predefinição, restauro VM tarefa irá criar uma VM com discos não geridos. Para criar uma VM com discos geridos:
1. [Restaurar para discos não geridos](tutorial-restore-disk.md#restore-a-vm-disk)
2. [Converta os discos restaurados em discos geridos](tutorial-restore-disk.md#convert-the-restored-disk-to-a-managed-disk)
3. [Criar uma VM com discos geridos](tutorial-restore-disk.md#create-a-vm-from-the-restored-disk) <br>
Cmdlets do Powershell, consulte [aqui](backup-azure-vms-automation.md#restore-an-azure-vm).

## <a name="manage-vm-backups"></a>Gerir cópias de segurança de VMs
### <a name="what-happens-when-i-change-a-backup-policy-on-vms"></a>O que acontece quando altero uma política de cópias de segurança numa ou em várias VMs?
Quando uma nova política é aplicada no VM, agenda e a retenção da nova política é seguido. Se a retenção é expandida, pontos de recuperação existentes são marcados para mantê-las de acordo com a nova política. Se a retenção é reduzida, estão marcados para eliminação na próxima tarefa de limpeza e são eliminados subsequentemente. 

### <a name="how-can-i-move-a-vm-enrolled-in-azure-backup-between-resource-groups"></a>Como mover que uma VM inscrito na cópia de segurança do Azure entre os grupos de recursos?
Siga os passos abaixo para mover com êxito a cópia de segurança VM para o grupo de recursos de destino 
1. Temporariamente parar a cópia de segurança e manter os dados de cópia de segurança
2. Mova a VM para o grupo de recursos de destino
3. Volte a protegê-lo com o mesmo/novo cofre

Os utilizadores podem restaurar a partir dos pontos de restauro disponíveis criados antes da operação de movimentação.


