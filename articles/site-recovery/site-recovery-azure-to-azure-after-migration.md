---
title: "aaaPrepare máquinas tooset segurança de recuperação após desastre entre regiões do Azure após a migração tooAzure utilizando a recuperação de Site | Microsoft Docs"
description: "Este artigo descreve como tooprepare máquinas tooset segurança de recuperação após desastre entre regiões do Azure após a migração tooAzure utilizando o Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: ponatara
manager: abhemraj
editor: 
ms.assetid: 9126f5e8-e9ed-4c31-b6b4-bf969c12c184
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: ponatara
ms.openlocfilehash: b6274e3df210c1d8a7b8289cc85868ee6414e523
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-azure-vms-tooanother-region-after-migration-tooazure-by-using-azure-site-recovery"></a>Replicar VMs do Azure tooanother região após migração tooAzure utilizando o Azure Site Recovery

>[!NOTE]
> Azure Site Recovery replicação para máquinas de virtuais (VMs) do Azure está atualmente em pré-visualização.

## <a name="overview"></a>Descrição geral

Este artigo ajuda-o a preparar máquinas virtuais do Azure para a replicação entre duas regiões do Azure depois destas máquinas tiverem sido migradas de um tooAzure de ambiente no local utilizando o Azure Site Recovery.

## <a name="disaster-recovery-and-compliance"></a>Recuperação após desastre e conformidade
Atualmente, as empresas mais estão a mover tooAzure as respetivas cargas de trabalho. Com que as empresas mover produção fundamentais no local tooAzure de cargas de trabalho, como configurar a recuperação após desastre para estas cargas de trabalho é obrigatório para toosafeguard em relação a quaisquer interrupções na região do Azure e de conformidade.

## <a name="steps-for-preparing-migrated-machines-for-replication"></a>Passos para preparar máquinas migradas para a replicação
tooprepare migrou máquinas para configurar a replicação tooanother região do Azure:

1. Concluir a migração.
2. Instale Olá agente do Azure, se necessário.
3. Remova o serviço de mobilidade Olá.  
4. Reinicie Olá VM.

Estes passos são descritos mais detalhadamente na Olá secções a seguir.

### <a name="step-1-migrate-workloads-running-on-hyper-v-vms-vmware-vms-and-physical-servers-toorun-on-azure-vms"></a>Passo 1: Migrar cargas de trabalho em execução em VMs Hyper-V, as VMs VMware e servidores físicos toorun em VMs do Azure

tooset até a replicação e migrar o seu local Hyper-V, VMware e cargas de trabalho físicas tooAzure, siga Olá passos Olá [máquinas de virtuais do IaaS do Azure migrar entre regiões do Azure com o Azure Site Recovery](site-recovery-migrate-to-azure.md) artigo. 

Após a migração, não precisa de toocommit ou eliminar uma ativação pós-falha. Em vez disso, selecione Olá **concluir a migração** opção para cada máquina que pretende toomigrate:
1. No **itens replicados**, faça duplo clique Olá VM e, em **concluir a migração**. Clique em **OK** passo de Olá toocomplete. Pode controlar o progresso nas propriedades VM Olá pela monitorização de tarefa de migração completa Olá na **as tarefas de recuperação de Site**.
2. Olá **concluir a migração** ação conclui o processo de migração de Olá, remove a replicação da máquina de Olá e deixa de faturação de recuperação de Site para a máquina Olá.

   ![completemigration](./media/site-recovery-hyper-v-site-to-azure/migrate.png)

### <a name="step-2-install-hello-azure-vm-agent-on-hello-virtual-machine"></a>Passo 2: Instalar o agente da VM do Azure de Olá na máquina virtual de Olá
Olá, Azure [agente da VM](../virtual-machines/windows/classic/agents-and-extensions.md#azure-vm-agents-for-windows-and-linux) tem de estar instalado na máquina virtual de Olá para toowork de extensão de recuperação de Site Olá e toohelp proteger Olá VM.

>[!IMPORTANT]
>A partir da versão 9.7.0.0, nas máquinas de virtuais do Windows, instalador do serviço de mobilidade de Olá também instala o Olá mais recente disponível agente VM do Azure. Na migração, a máquina virtual de Olá cumpre a instalação do agente pré-requisitos para utilizar qualquer extensão VM, incluindo a extensão de recuperação de Site Olá. Olá VM do Azure agente necessidades toobe instalado manualmente apenas se Olá serviço de mobilidade instalado Olá migrada a máquina está versão 9.6 ou anterior.

Olá tabela seguinte fornece informações adicionais sobre como instalar o agente da VM Olá e a validar que tenha sido instalado:

| **Operação** | **Windows** | **Linux** |
| --- | --- | --- |
| Instalar agente da VM Olá |Transfira e instale Olá [MSI do agente](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409). Terá de instalação de Olá de toocomplete de privilégios de administrador. |Instale os mais recentes Olá [agente Linux](../virtual-machines/linux/agent-user-guide.md). Terá de instalação de Olá de toocomplete de privilégios de administrador. Recomendamos que instale o agente de Olá do seu repositório de distribuição. Iremos *não é recomendada a* instalar Olá agente da VM com Linux diretamente a partir do GitHub.  |
| A validar a instalação do agente VM de Olá |1. Procure a pasta C:\WindowsAzure\Packages toohello Olá VM do Azure. Deverá ver ficheiro WaAppAgent.exe de Olá. <br>2. Clique no ficheiro de Olá, visite demasiado**propriedades**e, em seguida, selecione Olá **detalhes** Olá separador **versão do produto** campo deve ser 2.6.1198.718 ou superior. |N/D |


### <a name="step-3-remove-hello-mobility-service-from-hello-migrated-virtual-machine"></a>Passo 3: Remover Olá serviço de mobilidade de Olá de máquina virtual migrada

Se tiver migrado sua máquinas de VMware no local ou servidores físicos Windows/Linux, tem de serviço de mobilidade desinstalar/remoção de Olá do toomanually de Olá de máquina virtual migrada.

>[!IMPORTANT]
>Este passo não é necessário para tooAzure migrado VMs de Hyper-V.

#### <a name="uninstall-hello-mobility-service-on-a-windows-server-vm"></a>Desinstale o serviço de mobilidade Olá na VM do Windows Server
Utilize um dos Olá seguir o serviço de mobilidade métodos toouninstall Olá num computador Windows Server.

##### <a name="uninstall-by-using-hello-windows-ui"></a>Desinstalar utilizando Olá IU do Windows
1. No painel de controlo Olá, selecione **programas**.
2. Selecione **servidor de destino mestre do serviço de mobilidade recuperação Microsoft Azure Site**e, em seguida, selecione **desinstalação**.

##### <a name="uninstall-at-a-command-prompt"></a>Desinstalar uma linha de comandos
1. Abra uma janela de linha de comandos como administrador.
2. toouninstall Olá serviço de mobilidade, execute Olá os seguintes comandos:

   ```
   MsiExec.exe /qn /x {275197FC-14FD-4560-A5EB-38217F80CBD1} /L+*V "C:\ProgramData\ASRSetupLogs\UnifiedAgentMSIUninstall.log"
   ```

#### <a name="uninstall-hello-mobility-service-on-a-linux-computer"></a>Desinstale o serviço de mobilidade Olá num computador com Linux
1. No seu servidor Linux, inicie sessão como um **raiz** utilizador.
2. Num terminal, visite demasiado/utilizador/local/ASR.
3. toouninstall Olá serviço de mobilidade, execute Olá os seguintes comandos:

   ```
   uninstall.sh -Y
   ```

### <a name="step-4-restart-hello-vm"></a>Passo 4: Reiniciar Olá VM

Depois de desinstalar o serviço de mobilidade Olá, reinício Olá VM antes de configurar a replicação tooanother região do Azure.


## <a name="next-steps"></a>Passos seguintes
- Começar a proteger as cargas de trabalho por [replicar máquinas virtuais do Azure](site-recovery-azure-to-azure.md).
- Saiba mais sobre [redes orientações para replicar máquinas virtuais do Azure](site-recovery-azure-to-azure-networking-guidance.md).
