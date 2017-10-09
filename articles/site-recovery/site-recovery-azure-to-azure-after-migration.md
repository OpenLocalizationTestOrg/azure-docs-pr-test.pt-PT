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
# <a name="replicate-azure-vms-tooanother-region-after-migration-tooazure-by-using-azure-site-recovery"></a><span data-ttu-id="82690-103">Replicar VMs do Azure tooanother região após migração tooAzure utilizando o Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="82690-103">Replicate Azure VMs tooanother region after migration tooAzure by using Azure Site Recovery</span></span>

>[!NOTE]
> <span data-ttu-id="82690-104">Azure Site Recovery replicação para máquinas de virtuais (VMs) do Azure está atualmente em pré-visualização.</span><span class="sxs-lookup"><span data-stu-id="82690-104">Azure Site Recovery replication for Azure virtual machines (VMs) is currently in preview.</span></span>

## <a name="overview"></a><span data-ttu-id="82690-105">Descrição geral</span><span class="sxs-lookup"><span data-stu-id="82690-105">Overview</span></span>

<span data-ttu-id="82690-106">Este artigo ajuda-o a preparar máquinas virtuais do Azure para a replicação entre duas regiões do Azure depois destas máquinas tiverem sido migradas de um tooAzure de ambiente no local utilizando o Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="82690-106">This article helps you prepare Azure virtual machines for replication between two Azure regions after these machines have been migrated from an on-premises environment tooAzure by using Azure Site Recovery.</span></span>

## <a name="disaster-recovery-and-compliance"></a><span data-ttu-id="82690-107">Recuperação após desastre e conformidade</span><span class="sxs-lookup"><span data-stu-id="82690-107">Disaster recovery and compliance</span></span>
<span data-ttu-id="82690-108">Atualmente, as empresas mais estão a mover tooAzure as respetivas cargas de trabalho.</span><span class="sxs-lookup"><span data-stu-id="82690-108">Today, more and more enterprises are moving their workloads tooAzure.</span></span> <span data-ttu-id="82690-109">Com que as empresas mover produção fundamentais no local tooAzure de cargas de trabalho, como configurar a recuperação após desastre para estas cargas de trabalho é obrigatório para toosafeguard em relação a quaisquer interrupções na região do Azure e de conformidade.</span><span class="sxs-lookup"><span data-stu-id="82690-109">With enterprises moving mission-critical on-premises production workloads tooAzure, setting up disaster recovery for these workloads is mandatory for compliance and toosafeguard against any disruptions in an Azure region.</span></span>

## <a name="steps-for-preparing-migrated-machines-for-replication"></a><span data-ttu-id="82690-110">Passos para preparar máquinas migradas para a replicação</span><span class="sxs-lookup"><span data-stu-id="82690-110">Steps for preparing migrated machines for replication</span></span>
<span data-ttu-id="82690-111">tooprepare migrou máquinas para configurar a replicação tooanother região do Azure:</span><span class="sxs-lookup"><span data-stu-id="82690-111">tooprepare migrated machines for setting up replication tooanother Azure region:</span></span>

1. <span data-ttu-id="82690-112">Concluir a migração.</span><span class="sxs-lookup"><span data-stu-id="82690-112">Complete migration.</span></span>
2. <span data-ttu-id="82690-113">Instale Olá agente do Azure, se necessário.</span><span class="sxs-lookup"><span data-stu-id="82690-113">Install hello Azure agent if needed.</span></span>
3. <span data-ttu-id="82690-114">Remova o serviço de mobilidade Olá.</span><span class="sxs-lookup"><span data-stu-id="82690-114">Remove hello Mobility service.</span></span>  
4. <span data-ttu-id="82690-115">Reinicie Olá VM.</span><span class="sxs-lookup"><span data-stu-id="82690-115">Restart hello VM.</span></span>

<span data-ttu-id="82690-116">Estes passos são descritos mais detalhadamente na Olá secções a seguir.</span><span class="sxs-lookup"><span data-stu-id="82690-116">These steps are described in more detail in hello following sections.</span></span>

### <a name="step-1-migrate-workloads-running-on-hyper-v-vms-vmware-vms-and-physical-servers-toorun-on-azure-vms"></a><span data-ttu-id="82690-117">Passo 1: Migrar cargas de trabalho em execução em VMs Hyper-V, as VMs VMware e servidores físicos toorun em VMs do Azure</span><span class="sxs-lookup"><span data-stu-id="82690-117">Step 1: Migrate workloads running on Hyper-V VMs, VMware VMs, and physical servers toorun on Azure VMs</span></span>

<span data-ttu-id="82690-118">tooset até a replicação e migrar o seu local Hyper-V, VMware e cargas de trabalho físicas tooAzure, siga Olá passos Olá [máquinas de virtuais do IaaS do Azure migrar entre regiões do Azure com o Azure Site Recovery](site-recovery-migrate-to-azure.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="82690-118">tooset up replication and migrate your on-premises Hyper-V, VMware, and physical workloads tooAzure, follow hello steps in hello [Migrate Azure IaaS virtual machines between Azure regions with Azure Site Recovery](site-recovery-migrate-to-azure.md) article.</span></span> 

<span data-ttu-id="82690-119">Após a migração, não precisa de toocommit ou eliminar uma ativação pós-falha.</span><span class="sxs-lookup"><span data-stu-id="82690-119">After migration, you don't need toocommit or delete a failover.</span></span> <span data-ttu-id="82690-120">Em vez disso, selecione Olá **concluir a migração** opção para cada máquina que pretende toomigrate:</span><span class="sxs-lookup"><span data-stu-id="82690-120">Instead, select hello **Complete Migration** option for each machine you want toomigrate:</span></span>
1. <span data-ttu-id="82690-121">No **itens replicados**, faça duplo clique Olá VM e, em **concluir a migração**.</span><span class="sxs-lookup"><span data-stu-id="82690-121">In **Replicated Items**, right-click hello VM, and click **Complete Migration**.</span></span> <span data-ttu-id="82690-122">Clique em **OK** passo de Olá toocomplete.</span><span class="sxs-lookup"><span data-stu-id="82690-122">Click **OK** toocomplete hello step.</span></span> <span data-ttu-id="82690-123">Pode controlar o progresso nas propriedades VM Olá pela monitorização de tarefa de migração completa Olá na **as tarefas de recuperação de Site**.</span><span class="sxs-lookup"><span data-stu-id="82690-123">You can track progress in hello VM properties by monitoring hello Complete Migration job in **Site Recovery jobs**.</span></span>
2. <span data-ttu-id="82690-124">Olá **concluir a migração** ação conclui o processo de migração de Olá, remove a replicação da máquina de Olá e deixa de faturação de recuperação de Site para a máquina Olá.</span><span class="sxs-lookup"><span data-stu-id="82690-124">hello **Complete Migration** action completes hello migration process, removes replication for hello machine, and stops Site Recovery billing for hello machine.</span></span>

   ![completemigration](./media/site-recovery-hyper-v-site-to-azure/migrate.png)

### <a name="step-2-install-hello-azure-vm-agent-on-hello-virtual-machine"></a><span data-ttu-id="82690-126">Passo 2: Instalar o agente da VM do Azure de Olá na máquina virtual de Olá</span><span class="sxs-lookup"><span data-stu-id="82690-126">Step 2: Install hello Azure VM agent on hello virtual machine</span></span>
<span data-ttu-id="82690-127">Olá, Azure [agente da VM](../virtual-machines/windows/classic/agents-and-extensions.md#azure-vm-agents-for-windows-and-linux) tem de estar instalado na máquina virtual de Olá para toowork de extensão de recuperação de Site Olá e toohelp proteger Olá VM.</span><span class="sxs-lookup"><span data-stu-id="82690-127">hello Azure [VM agent](../virtual-machines/windows/classic/agents-and-extensions.md#azure-vm-agents-for-windows-and-linux) must be installed on hello virtual machine for hello Site Recovery extension toowork and toohelp protect hello VM.</span></span>

>[!IMPORTANT]
><span data-ttu-id="82690-128">A partir da versão 9.7.0.0, nas máquinas de virtuais do Windows, instalador do serviço de mobilidade de Olá também instala o Olá mais recente disponível agente VM do Azure.</span><span class="sxs-lookup"><span data-stu-id="82690-128">Beginning with version 9.7.0.0, on Windows virtual machines, hello Mobility service installer also installs hello latest available Azure VM agent.</span></span> <span data-ttu-id="82690-129">Na migração, a máquina virtual de Olá cumpre a instalação do agente pré-requisitos para utilizar qualquer extensão VM, incluindo a extensão de recuperação de Site Olá.</span><span class="sxs-lookup"><span data-stu-id="82690-129">On migration, hello virtual machine meets the agent installation prerequisite for using any VM extension, including hello Site Recovery extension.</span></span> <span data-ttu-id="82690-130">Olá VM do Azure agente necessidades toobe instalado manualmente apenas se Olá serviço de mobilidade instalado Olá migrada a máquina está versão 9.6 ou anterior.</span><span class="sxs-lookup"><span data-stu-id="82690-130">hello Azure VM agent needs toobe manually installed only if hello Mobility service installed on hello migrated machine is version 9.6 or earlier.</span></span>

<span data-ttu-id="82690-131">Olá tabela seguinte fornece informações adicionais sobre como instalar o agente da VM Olá e a validar que tenha sido instalado:</span><span class="sxs-lookup"><span data-stu-id="82690-131">hello following table provides additional information about installing hello VM agent and validating that it was installed:</span></span>

| <span data-ttu-id="82690-132">**Operação**</span><span class="sxs-lookup"><span data-stu-id="82690-132">**Operation**</span></span> | <span data-ttu-id="82690-133">**Windows**</span><span class="sxs-lookup"><span data-stu-id="82690-133">**Windows**</span></span> | <span data-ttu-id="82690-134">**Linux**</span><span class="sxs-lookup"><span data-stu-id="82690-134">**Linux**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="82690-135">Instalar agente da VM Olá</span><span class="sxs-lookup"><span data-stu-id="82690-135">Installing hello VM agent</span></span> |<span data-ttu-id="82690-136">Transfira e instale Olá [MSI do agente](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="82690-136">Download and install hello [agent MSI](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409).</span></span> <span data-ttu-id="82690-137">Terá de instalação de Olá de toocomplete de privilégios de administrador.</span><span class="sxs-lookup"><span data-stu-id="82690-137">You need administrator privileges toocomplete hello installation.</span></span> |<span data-ttu-id="82690-138">Instale os mais recentes Olá [agente Linux](../virtual-machines/linux/agent-user-guide.md).</span><span class="sxs-lookup"><span data-stu-id="82690-138">Install hello latest [Linux agent](../virtual-machines/linux/agent-user-guide.md).</span></span> <span data-ttu-id="82690-139">Terá de instalação de Olá de toocomplete de privilégios de administrador.</span><span class="sxs-lookup"><span data-stu-id="82690-139">You need administrator privileges toocomplete hello installation.</span></span> <span data-ttu-id="82690-140">Recomendamos que instale o agente de Olá do seu repositório de distribuição.</span><span class="sxs-lookup"><span data-stu-id="82690-140">We recommend installing hello agent from your distribution repository.</span></span> <span data-ttu-id="82690-141">Iremos *não é recomendada a* instalar Olá agente da VM com Linux diretamente a partir do GitHub.</span><span class="sxs-lookup"><span data-stu-id="82690-141">We *do not recommend* installing hello Linux VM agent directly from GitHub.</span></span>  |
| <span data-ttu-id="82690-142">A validar a instalação do agente VM de Olá</span><span class="sxs-lookup"><span data-stu-id="82690-142">Validating hello VM agent installation</span></span> |<span data-ttu-id="82690-143">1. Procure a pasta C:\WindowsAzure\Packages toohello Olá VM do Azure.</span><span class="sxs-lookup"><span data-stu-id="82690-143">1. Browse toohello C:\WindowsAzure\Packages folder in hello Azure VM.</span></span> <span data-ttu-id="82690-144">Deverá ver ficheiro WaAppAgent.exe de Olá.</span><span class="sxs-lookup"><span data-stu-id="82690-144">You should see hello WaAppAgent.exe file.</span></span> <br><span data-ttu-id="82690-145">2. Clique no ficheiro de Olá, visite demasiado**propriedades**e, em seguida, selecione Olá **detalhes** Olá separador **versão do produto** campo deve ser 2.6.1198.718 ou superior.</span><span class="sxs-lookup"><span data-stu-id="82690-145">2. Right-click hello file, go too**Properties**, and then select hello **Details** tab. hello **Product Version** field should be 2.6.1198.718 or higher.</span></span> |<span data-ttu-id="82690-146">N/D</span><span class="sxs-lookup"><span data-stu-id="82690-146">N/A</span></span> |


### <a name="step-3-remove-hello-mobility-service-from-hello-migrated-virtual-machine"></a><span data-ttu-id="82690-147">Passo 3: Remover Olá serviço de mobilidade de Olá de máquina virtual migrada</span><span class="sxs-lookup"><span data-stu-id="82690-147">Step 3: Remove hello Mobility service from hello migrated virtual machine</span></span>

<span data-ttu-id="82690-148">Se tiver migrado sua máquinas de VMware no local ou servidores físicos Windows/Linux, tem de serviço de mobilidade desinstalar/remoção de Olá do toomanually de Olá de máquina virtual migrada.</span><span class="sxs-lookup"><span data-stu-id="82690-148">If you have migrated your on-premises VMware machines or physical servers on Windows/Linux, you need toomanually remove/uninstall hello Mobility service from hello migrated virtual machine.</span></span>

>[!IMPORTANT]
><span data-ttu-id="82690-149">Este passo não é necessário para tooAzure migrado VMs de Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="82690-149">This step is not required for Hyper-V VMs migrated tooAzure.</span></span>

#### <a name="uninstall-hello-mobility-service-on-a-windows-server-vm"></a><span data-ttu-id="82690-150">Desinstale o serviço de mobilidade Olá na VM do Windows Server</span><span class="sxs-lookup"><span data-stu-id="82690-150">Uninstall hello Mobility service on a Windows Server VM</span></span>
<span data-ttu-id="82690-151">Utilize um dos Olá seguir o serviço de mobilidade métodos toouninstall Olá num computador Windows Server.</span><span class="sxs-lookup"><span data-stu-id="82690-151">Use one of hello following methods toouninstall hello Mobility service on a Windows Server computer.</span></span>

##### <a name="uninstall-by-using-hello-windows-ui"></a><span data-ttu-id="82690-152">Desinstalar utilizando Olá IU do Windows</span><span class="sxs-lookup"><span data-stu-id="82690-152">Uninstall by using hello Windows UI</span></span>
1. <span data-ttu-id="82690-153">No painel de controlo Olá, selecione **programas**.</span><span class="sxs-lookup"><span data-stu-id="82690-153">In hello Control Panel, select **Programs**.</span></span>
2. <span data-ttu-id="82690-154">Selecione **servidor de destino mestre do serviço de mobilidade recuperação Microsoft Azure Site**e, em seguida, selecione **desinstalação**.</span><span class="sxs-lookup"><span data-stu-id="82690-154">Select **Microsoft Azure Site Recovery Mobility Service/Master Target server**, and then select **Uninstall**.</span></span>

##### <a name="uninstall-at-a-command-prompt"></a><span data-ttu-id="82690-155">Desinstalar uma linha de comandos</span><span class="sxs-lookup"><span data-stu-id="82690-155">Uninstall at a command prompt</span></span>
1. <span data-ttu-id="82690-156">Abra uma janela de linha de comandos como administrador.</span><span class="sxs-lookup"><span data-stu-id="82690-156">Open a Command Prompt window as an administrator.</span></span>
2. <span data-ttu-id="82690-157">toouninstall Olá serviço de mobilidade, execute Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="82690-157">toouninstall hello Mobility service, run hello following command:</span></span>

   ```
   MsiExec.exe /qn /x {275197FC-14FD-4560-A5EB-38217F80CBD1} /L+*V "C:\ProgramData\ASRSetupLogs\UnifiedAgentMSIUninstall.log"
   ```

#### <a name="uninstall-hello-mobility-service-on-a-linux-computer"></a><span data-ttu-id="82690-158">Desinstale o serviço de mobilidade Olá num computador com Linux</span><span class="sxs-lookup"><span data-stu-id="82690-158">Uninstall hello Mobility service on a Linux computer</span></span>
1. <span data-ttu-id="82690-159">No seu servidor Linux, inicie sessão como um **raiz** utilizador.</span><span class="sxs-lookup"><span data-stu-id="82690-159">On your Linux server, sign in as a **root** user.</span></span>
2. <span data-ttu-id="82690-160">Num terminal, visite demasiado/utilizador/local/ASR.</span><span class="sxs-lookup"><span data-stu-id="82690-160">In a terminal, go too/user/local/ASR.</span></span>
3. <span data-ttu-id="82690-161">toouninstall Olá serviço de mobilidade, execute Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="82690-161">toouninstall hello Mobility service, run hello following command:</span></span>

   ```
   uninstall.sh -Y
   ```

### <a name="step-4-restart-hello-vm"></a><span data-ttu-id="82690-162">Passo 4: Reiniciar Olá VM</span><span class="sxs-lookup"><span data-stu-id="82690-162">Step 4: Restart hello VM</span></span>

<span data-ttu-id="82690-163">Depois de desinstalar o serviço de mobilidade Olá, reinício Olá VM antes de configurar a replicação tooanother região do Azure.</span><span class="sxs-lookup"><span data-stu-id="82690-163">After you uninstall hello Mobility service, restart hello VM before you set up replication tooanother Azure region.</span></span>


## <a name="next-steps"></a><span data-ttu-id="82690-164">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="82690-164">Next steps</span></span>
- <span data-ttu-id="82690-165">Começar a proteger as cargas de trabalho por [replicar máquinas virtuais do Azure](site-recovery-azure-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="82690-165">Start protecting your workloads by [replicating Azure virtual machines](site-recovery-azure-to-azure.md).</span></span>
- <span data-ttu-id="82690-166">Saiba mais sobre [redes orientações para replicar máquinas virtuais do Azure](site-recovery-azure-to-azure-networking-guidance.md).</span><span class="sxs-lookup"><span data-stu-id="82690-166">Learn more about [networking guidance for replicating Azure virtual machines](site-recovery-azure-to-azure-networking-guidance.md).</span></span>
