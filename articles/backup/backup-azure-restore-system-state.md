---
title: "Cópia de segurança do Azure: Tooa de restauro do Estado do sistema do Windows Server | Microsoft Docs"
description: "Passo por explicação passo para restaurar o estado do sistema do Windows Server a partir de uma cópia de segurança no Azure."
services: backup
documentationcenter: 
author: saurabhsensharma
manager: shivamg
editor: 
ms.assetid: 
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/18/2017
ms.author: saurse;trinadhk;markgal;
ms.openlocfilehash: a45506507f53e2744350d3b6b2e52f1db415de4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="restore-system-state-toowindows-server"></a><span data-ttu-id="e31c4-103">Restaurar estado do sistema tooWindows servidor</span><span class="sxs-lookup"><span data-stu-id="e31c4-103">Restore System State tooWindows Server</span></span>

<span data-ttu-id="e31c4-104">Este artigo explica como toorestore cópias de segurança de estado do sistema do Windows Server um serviços de recuperação do Azure do cofre.</span><span class="sxs-lookup"><span data-stu-id="e31c4-104">This article explains how toorestore Windows Server System State backups from an Azure Recovery Services vault.</span></span> <span data-ttu-id="e31c4-105">toorestore estado do sistema, tem de ter uma cópia de segurança do Estado do sistema (criadas com instruções Olá [cópia de segurança do Estado do sistema](backup-azure-system-state.md#back-up-windows-server-system-state-preview)) e certifique-se de que instalou Olá [versão mais recente do Olá recuperação do Microsoft Azure Agente de serviços (MARS)](http://aka.ms/azurebackup_agent).</span><span class="sxs-lookup"><span data-stu-id="e31c4-105">toorestore System State, you must have a System State backup (created using hello instructions in [Back up System State](backup-azure-system-state.md#back-up-windows-server-system-state-preview)), and make sure you have installed hello [latest version of hello Microsoft Azure Recovery Services (MARS) agent](http://aka.ms/azurebackup_agent).</span></span> <span data-ttu-id="e31c4-106">Recuperar dados de estado do sistema do Windows Server a partir de um cofre dos serviços de recuperação do Azure é um processo de dois passos:</span><span class="sxs-lookup"><span data-stu-id="e31c4-106">Recovering Windows Server System State data from an Azure Recovery Services vault is a two-step process:</span></span>

1. <span data-ttu-id="e31c4-107">Restaure estado do sistema como ficheiros de cópia de segurança do Azure.</span><span class="sxs-lookup"><span data-stu-id="e31c4-107">Restore System State as files from Azure Backup.</span></span> <span data-ttu-id="e31c4-108">Ao restaurar o estado do sistema de ficheiros de cópia de segurança do Azure, pode:</span><span class="sxs-lookup"><span data-stu-id="e31c4-108">When restoring System State as files from Azure Backup, you can either:</span></span>
  * <span data-ttu-id="e31c4-109">Restaurar estado do sistema toohello mesmo servidor em que foram executadas cópias de segurança hello, ou</span><span class="sxs-lookup"><span data-stu-id="e31c4-109">Restore System State toohello same server where hello backups were taken, or</span></span>
  * <span data-ttu-id="e31c4-110">Restaurar estado do sistema tooan alternativo servidor de ficheiros.</span><span class="sxs-lookup"><span data-stu-id="e31c4-110">Restore System State file tooan alternate server.</span></span>

2. <span data-ttu-id="e31c4-111">Aplica Olá restaurada estado do sistema ficheiros tooa do Windows Server.</span><span class="sxs-lookup"><span data-stu-id="e31c4-111">Apply hello restored System State files tooa Windows Server.</span></span>


## <a name="recover-system-state-files-toohello-same-server"></a><span data-ttu-id="e31c4-112">Estado do sistema de recuperar ficheiros toohello mesmo servidor</span><span class="sxs-lookup"><span data-stu-id="e31c4-112">Recover System State files toohello same server</span></span>
<span data-ttu-id="e31c4-113">Olá, os passos seguintes explica como tooroll fazer uma cópia do estado anterior do Windows Server configuração tooa.</span><span class="sxs-lookup"><span data-stu-id="e31c4-113">hello following steps explain how tooroll back your Windows Server configuration tooa previous state.</span></span> <span data-ttu-id="e31c4-114">A anular o servidor de configuração tooa back conhecida, estado estável, pode ser extremamente valiosa.</span><span class="sxs-lookup"><span data-stu-id="e31c4-114">Rolling your server configuration back tooa known, stable state, can be extremely valuable.</span></span> <span data-ttu-id="e31c4-115">Olá seguintes estado do sistema do servidor de passos, restauro Olá de um cofre dos serviços de recuperação.</span><span class="sxs-lookup"><span data-stu-id="e31c4-115">hello following steps restore hello server's System State from a Recovery Services vault.</span></span> 

1. <span data-ttu-id="e31c4-116">Abra Olá **cópia de segurança do Microsoft Azure** snap-in.</span><span class="sxs-lookup"><span data-stu-id="e31c4-116">Open hello **Microsoft Azure Backup** snap-in.</span></span> <span data-ttu-id="e31c4-117">Se não souber qual o snap-in do Olá foi instalado, pesquisar computador Olá ou um servidor para **cópia de segurança do Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="e31c4-117">If you don't know where hello snap-in was installed, search hello computer or server for **Microsoft Azure Backup**.</span></span>

    <span data-ttu-id="e31c4-118">aplicação de ambiente de trabalho Olá deve aparecer nos resultados de pesquisa de Olá.</span><span class="sxs-lookup"><span data-stu-id="e31c4-118">hello desktop app should appear in hello search results.</span></span>

2. <span data-ttu-id="e31c4-119">Clique em **recuperar dados** Assistente de Olá toostart.</span><span class="sxs-lookup"><span data-stu-id="e31c4-119">Click **Recover Data** toostart hello wizard.</span></span>

    ![Recuperar dados](./media/backup-azure-restore-windows-server/recover.png)

3. <span data-ttu-id="e31c4-121">No Olá **introdução** painel, toorestore Olá dados toohello mesmo servidor ou computador, selecione **neste servidor (`<server name>`)** e clique em **seguinte**.</span><span class="sxs-lookup"><span data-stu-id="e31c4-121">On hello **Getting Started** pane, toorestore hello data toohello same server or computer, select **This server (`<server name>`)** and click **Next**.</span></span>

    ![Escolha esta toohello de dados do servidor opção toorestore Olá mesma máquina](./media/backup-azure-restore-system-state/samemachine.png)

4. <span data-ttu-id="e31c4-123">No Olá **selecionar modo de recuperação** painel, escolha **estado do sistema** e, em seguida, clique em **seguinte**.</span><span class="sxs-lookup"><span data-stu-id="e31c4-123">On hello **Select Recovery Mode** pane, choose **System State** and then click **Next**.</span></span>

    ![Procurar ficheiros](./media/backup-azure-restore-system-state/recover-type-selection.png)

5. <span data-ttu-id="e31c4-125">No calendário Olá no **data e selecione o Volume** painel, selecione uma recuperação do ponto.</span><span class="sxs-lookup"><span data-stu-id="e31c4-125">On hello calendar in **Select Volume and Date** pane, select a recovery point.</span></span> 

    <span data-ttu-id="e31c4-126">Pode restaurar a partir de qualquer ponto de recuperação no tempo.</span><span class="sxs-lookup"><span data-stu-id="e31c4-126">You can restore from any recovery point in time.</span></span> <span data-ttu-id="e31c4-127">As datas em **negrito** indicar disponibilidade Olá de, pelo menos, um ponto de recuperação.</span><span class="sxs-lookup"><span data-stu-id="e31c4-127">Dates in **bold** indicate hello availability of at least one recovery point.</span></span> <span data-ttu-id="e31c4-128">Depois de selecionar uma data, se não estiverem disponíveis vários pontos de recuperação, escolha o ponto de recuperação específico Olá de Olá **tempo** menu pendente.</span><span class="sxs-lookup"><span data-stu-id="e31c4-128">Once you select a date, if multiple recovery points are available, choose hello specific recovery point from hello **Time** drop-down menu.</span></span>

    ![Data e de volume](./media/backup-azure-restore-system-state/select-date.png)

6. <span data-ttu-id="e31c4-130">Assim que tiver optado por toorestore de ponto de recuperação Olá, clique em **seguinte**.</span><span class="sxs-lookup"><span data-stu-id="e31c4-130">Once you have chosen hello recovery point toorestore, click **Next**.</span></span>

    <span data-ttu-id="e31c4-131">Cópia de segurança do Azure monta o ponto de recuperação do local de Olá e utiliza-o como um volume de recuperação.</span><span class="sxs-lookup"><span data-stu-id="e31c4-131">Azure Backup mounts hello local recovery point, and uses it as a recovery volume.</span></span>

7. <span data-ttu-id="e31c4-132">No painel seguinte da Olá, especifique o destino de Olá para Olá recuperar ficheiros de estado do sistema e clique em **procurar** tooopen Explorador do Windows e localizar Olá ficheiros e pastas que pretende.</span><span class="sxs-lookup"><span data-stu-id="e31c4-132">On hello next pane, specify hello destination for hello recovered System State files and click **Browse** tooopen Windows Explorer and find hello files and folders you want.</span></span> <span data-ttu-id="e31c4-133">Olá opção, **criar cópias de modo a que ambas as versões**, cria cópias dos ficheiros individuais num arquivo de ficheiros de estado do sistema existente em vez de criar a cópia de Olá do arquivo de estado do sistema completo Olá.</span><span class="sxs-lookup"><span data-stu-id="e31c4-133">hello option, **Create copies so that you have both versions**, creates copies of individual files in an existing System State file archive instead of creating hello copy of hello entire System State archive.</span></span>

    ![Opções de recuperação](./media/backup-azure-restore-system-state/recover-as-files.png)

8. <span data-ttu-id="e31c4-135">Verifique os detalhes de Olá de recuperação no Olá **confirmação** painel e clique em **recuperar**.</span><span class="sxs-lookup"><span data-stu-id="e31c4-135">Verify hello details of recovery on hello **Confirmation** pane and click **Recover**.</span></span>

   ![Clique em ação de recuperação do recuperar tooacknowledge Olá](./media/backup-azure-restore-system-state/confirm-recovery.png)

9. <span data-ttu-id="e31c4-137">Olá cópia *WindowsImageBackup* diretório no Olá volume não críticas do tooa de destino de recuperação do servidor de Olá.</span><span class="sxs-lookup"><span data-stu-id="e31c4-137">Copy hello *WindowsImageBackup* directory in hello Recovery destination tooa non-critical volume of hello server.</span></span> <span data-ttu-id="e31c4-138">Normalmente, Olá volume de sistema operativo Windows é o volume crítico Olá.</span><span class="sxs-lookup"><span data-stu-id="e31c4-138">Usually, hello Windows OS volume is hello critical volume.</span></span>

10. <span data-ttu-id="e31c4-139">Assim que a recuperação de Olá for bem sucedida, siga os passos de Olá na secção de Olá, [aplicar restaurada toohello de ficheiros de estado do sistema do Windows Server](backup-azure-restore-system-state.md#apply-restored-system-state-files-to-the-windows-server), toocomplete Olá processo de recuperação do Estado do sistema.</span><span class="sxs-lookup"><span data-stu-id="e31c4-139">Once hello recovery is successful, follow hello steps in hello section, [Apply restored System State files toohello Windows Server](backup-azure-restore-system-state.md#apply-restored-system-state-files-to-the-windows-server), toocomplete hello System State recovery process.</span></span>

## <a name="recover-system-state-files-tooan-alternate-server"></a><span data-ttu-id="e31c4-140">Servidor do Estado do sistema de recuperar ficheiros tooan alternativo</span><span class="sxs-lookup"><span data-stu-id="e31c4-140">Recover System State files tooan alternate server</span></span>

<span data-ttu-id="e31c4-141">Se o servidor do Windows está danificada ou estiver inacessível e pretender toorestore-tooa estado estável por recuperar Olá estado do sistema do Windows Server, pode restaurar estado do sistema do servidor Olá danificada a partir de outro servidor.</span><span class="sxs-lookup"><span data-stu-id="e31c4-141">If your Windows Server is corrupted or inaccessible, and you want toorestore it tooa stable state by recovering hello Windows Server System State, you can restore hello corrupted server's System State from another server.</span></span> <span data-ttu-id="e31c4-142">Utilize Olá os seguintes passos toohello restaurar estado do sistema num servidor separado.</span><span class="sxs-lookup"><span data-stu-id="e31c4-142">Use hello following steps toohello restore System State on a separate server.</span></span>  

<span data-ttu-id="e31c4-143">terminologia de Olá utilizada estes passos incluem:</span><span class="sxs-lookup"><span data-stu-id="e31c4-143">hello terminology used in these steps includes:</span></span>

- <span data-ttu-id="e31c4-144">*Máquina de origem* – máquina original Olá a partir de cópia de segurança que Olá foi executada e que não está atualmente disponível.</span><span class="sxs-lookup"><span data-stu-id="e31c4-144">*Source machine* – hello original machine from which hello backup was taken and which is currently unavailable.</span></span>
- <span data-ttu-id="e31c4-145">*A máquina de destino* – dados de Olá Olá máquina toowhich está a ser recuperados.</span><span class="sxs-lookup"><span data-stu-id="e31c4-145">*Target machine* – hello machine toowhich hello data is being recovered.</span></span>
- <span data-ttu-id="e31c4-146">*Cofre do exemplo* – Olá do Olá dos serviços de recuperação cofre toowhich *máquina de origem* e *máquina de destino* estão registados.</span><span class="sxs-lookup"><span data-stu-id="e31c4-146">*Sample vault* – hello Recovery Services vault toowhich hello *Source machine* and *Target machine* are registered.</span></span> <br/>

> [!NOTE]
> <span data-ttu-id="e31c4-147">As cópias de segurança obtidas a partir de uma máquina não podem ser máquina tooa restaurados com uma versão anterior do sistema de operativo Olá.</span><span class="sxs-lookup"><span data-stu-id="e31c4-147">Backups taken from one machine cannot be restored tooa machine running an earlier version of hello operating system.</span></span> <span data-ttu-id="e31c4-148">Por exemplo, as cópias de segurança obtidas a partir da máquina não pode ser um Windows Server 2016 restaurada tooWindows Server 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="e31c4-148">For example, backups taken from a Windows Server 2016 machine can't be restored tooWindows Server 2012 R2.</span></span> <span data-ttu-id="e31c4-149">No entanto, inverso Olá é possível.</span><span class="sxs-lookup"><span data-stu-id="e31c4-149">However, hello inverse is possible.</span></span> <span data-ttu-id="e31c4-150">Pode utilizar cópias de segurança do Windows Server 2012 R2 toorestore Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="e31c4-150">You can use backups from Windows Server 2012 R2 toorestore Windows Server 2016.</span></span>
>

1. <span data-ttu-id="e31c4-151">Abra Olá **cópia de segurança do Microsoft Azure** snap-in no Olá *máquina de destino*.</span><span class="sxs-lookup"><span data-stu-id="e31c4-151">Open hello **Microsoft Azure Backup** snap-in on hello *Target machine*.</span></span>
2. <span data-ttu-id="e31c4-152">Certifique-se de que Olá *máquina de destino* e Olá *máquina de origem* são registado toohello dos serviços de recuperação mesmo cofre.</span><span class="sxs-lookup"><span data-stu-id="e31c4-152">Ensure that hello *Target machine* and hello *Source machine* are registered toohello same Recovery Services vault.</span></span>
3. <span data-ttu-id="e31c4-153">Clique em **recuperar dados** o fluxo de trabalho do tooinitiate Olá.</span><span class="sxs-lookup"><span data-stu-id="e31c4-153">Click **Recover Data** tooinitiate hello workflow.</span></span>

    ![Recuperar dados](./media/backup-azure-restore-windows-server-classic/recover.png)

4. <span data-ttu-id="e31c4-155">Selecione **outro servidor**</span><span class="sxs-lookup"><span data-stu-id="e31c4-155">Select **Another server**</span></span>

    ![Outro servidor](./media/backup-azure-restore-system-state/anotherserver.png)

5. <span data-ttu-id="e31c4-157">Forneça o ficheiro de credenciais de cofre Olá corresponde toohello *Cofre de exemplo*.</span><span class="sxs-lookup"><span data-stu-id="e31c4-157">Provide hello vault credential file that corresponds toohello *Sample vault*.</span></span> <span data-ttu-id="e31c4-158">Se o ficheiro de credenciais do cofre Olá (expirou ou era inválida), transfira um novo ficheiro de credenciais do Cofre de Olá *Cofre de exemplo* no Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="e31c4-158">If hello vault credential file is invalid (or expired), download a new vault credential file from hello *Sample vault* in hello Azure portal.</span></span> <span data-ttu-id="e31c4-159">Depois do ficheiro de credenciais do cofre Olá for fornecido, é apresentado o Cofre de serviços de recuperação de Olá associada ao ficheiro de credenciais de cofre Olá.</span><span class="sxs-lookup"><span data-stu-id="e31c4-159">Once hello vault credential file is provided, hello Recovery Services vault associated with hello vault credential file appears.</span></span>

6. <span data-ttu-id="e31c4-160">No painel de selecionar o servidor de cópia de segurança de Olá, selecione Olá *máquina de origem* da lista de Olá máquinas apresentados.</span><span class="sxs-lookup"><span data-stu-id="e31c4-160">On hello Select Backup Server pane, select hello *Source machine* from hello list of displayed machines.</span></span>

    ![Lista de máquinas](./media/backup-azure-restore-windows-server-classic/machinelist.png)

7. <span data-ttu-id="e31c4-162">No painel de selecionar o modo de recuperação Olá, escolha **estado do sistema** e clique em **seguinte**.</span><span class="sxs-lookup"><span data-stu-id="e31c4-162">On hello Select Recovery Mode pane, choose **System State** and click **Next**.</span></span> 

    ![Pesquisa](./media/backup-azure-restore-system-state/recover-type-selection.png)

8. <span data-ttu-id="e31c4-164">No Olá calendário no Olá **data e selecione o Volume** painel, selecione uma recuperação do ponto.</span><span class="sxs-lookup"><span data-stu-id="e31c4-164">On hello Calendar in hello **Select Volume and Date** pane, select a recovery point.</span></span> <span data-ttu-id="e31c4-165">Pode restaurar a partir de qualquer ponto de recuperação no tempo.</span><span class="sxs-lookup"><span data-stu-id="e31c4-165">You can restore from any recovery point in time.</span></span> <span data-ttu-id="e31c4-166">As datas em **negrito** indicar disponibilidade Olá de, pelo menos, um ponto de recuperação.</span><span class="sxs-lookup"><span data-stu-id="e31c4-166">Dates in **bold** indicate hello availability of at least one recovery point.</span></span> <span data-ttu-id="e31c4-167">Depois de selecionar uma data, se não estiverem disponíveis vários pontos de recuperação, escolha o ponto de recuperação específico Olá de Olá **tempo** menu pendente.</span><span class="sxs-lookup"><span data-stu-id="e31c4-167">Once  you select a date, if multiple recovery points are available, choose hello specific recovery point from hello **Time** drop-down menu.</span></span> 

    ![Itens de procura](./media/backup-azure-restore-system-state/select-date.png)

9. <span data-ttu-id="e31c4-169">Assim que tiver optado por toorestore de ponto de recuperação Olá, clique em **seguinte**.</span><span class="sxs-lookup"><span data-stu-id="e31c4-169">Once you have chosen hello recovery point toorestore, click **Next**.</span></span>

10. <span data-ttu-id="e31c4-170">No Olá **selecionar modo de recuperação de estado de sistema** painel, especifique onde pretende toobe recuperar ficheiros de estado do sistema de destino de Olá, em seguida, clique em **seguinte**.</span><span class="sxs-lookup"><span data-stu-id="e31c4-170">On hello **Select System State Recovery Mode** pane, specify hello destination where you want System State files toobe recovered, then click **Next**.</span></span>

    ![Encriptação](./media/backup-azure-restore-system-state/recover-as-files.png)

    <span data-ttu-id="e31c4-172">Olá opção, **criar cópias de modo a que ambas as versões**, cria cópias dos ficheiros individuais num arquivo de ficheiros de estado do sistema existente em vez de criar a cópia de Olá do arquivo de estado do sistema completo Olá.</span><span class="sxs-lookup"><span data-stu-id="e31c4-172">hello option, **Create copies so that you have both versions**, creates copies of individual files in an existing System State file archive instead of creating hello copy of hello entire System State archive.</span></span>

11. <span data-ttu-id="e31c4-173">Verifique os detalhes de Olá de recuperação no painel de confirmação de Olá e clique em **recuperar**.</span><span class="sxs-lookup"><span data-stu-id="e31c4-173">Verify hello details of recovery on hello Confirmation pane, and click **Recover**.</span></span> 

    ![Clique em processo de recuperação de Olá botão tooconfirm Olá recuperar](./media/backup-azure-restore-system-state/confirm-recovery.png)

12. <span data-ttu-id="e31c4-175">Olá cópia *WindowsImageBackup* volume de não críticos tooa directory do servidor de Olá (por exemplo D:\).</span><span class="sxs-lookup"><span data-stu-id="e31c4-175">Copy hello *WindowsImageBackup* directory tooa non-critical volume of hello server (for example D:\).</span></span> <span data-ttu-id="e31c4-176">Normalmente, Olá volume de sistema operativo Windows é o volume crítico Olá.</span><span class="sxs-lookup"><span data-stu-id="e31c4-176">Usually hello Windows OS volume is hello critical volume.</span></span>

13. <span data-ttu-id="e31c4-177">processo de recuperação do toocomplete Olá, utilize seguinte de Olá secção demasiado[aplicam-se os ficheiros de estado do sistema de Olá restaurado num servidor Windows](backup-azure-restore-system-state.md#apply-restored-system-state-on-a-windows-server).</span><span class="sxs-lookup"><span data-stu-id="e31c4-177">toocomplete hello recovery process, use hello following section too[apply hello restored System State files on a Windows Server](backup-azure-restore-system-state.md#apply-restored-system-state-on-a-windows-server).</span></span>




## <a name="apply-restored-system-state-on-a-windows-server"></a><span data-ttu-id="e31c4-178">Aplicar o restauro do Estado do sistema no Windows Server</span><span class="sxs-lookup"><span data-stu-id="e31c4-178">Apply restored System State on a Windows Server</span></span>

<span data-ttu-id="e31c4-179">Assim que tiver recuperado o estado do sistema de ficheiros utilizando o Azure Recovery Services Agent, utilize Olá cópia de segurança do Windows Server utilitário tooapply Olá recuperar o estado do sistema tooWindows servidor.</span><span class="sxs-lookup"><span data-stu-id="e31c4-179">Once you have recovered System State as files using Azure Recovery Services Agent, use hello Windows Server Backup utility tooapply hello recovered System State tooWindows Server.</span></span> <span data-ttu-id="e31c4-180">já se encontra disponível no servidor de Olá Olá utilitário de cópia de segurança do Windows Server.</span><span class="sxs-lookup"><span data-stu-id="e31c4-180">hello Windows Server Backup utility is already available on hello server.</span></span> <span data-ttu-id="e31c4-181">Olá, os passos seguintes explica como tooapply Olá recuperar o estado do sistema.</span><span class="sxs-lookup"><span data-stu-id="e31c4-181">hello following steps explain how tooapply hello recovered System State.</span></span>

1. <span data-ttu-id="e31c4-182">Seguinte de Olá utilize comandos tooreboot o servidor no *modo de reparação de serviços de diretório*.</span><span class="sxs-lookup"><span data-stu-id="e31c4-182">Use hello following commands tooreboot your server in *Directory Services Repair Mode*.</span></span> <span data-ttu-id="e31c4-183">Na linha de comandos elevada:</span><span class="sxs-lookup"><span data-stu-id="e31c4-183">In an elevated command prompt:</span></span>

    ```
    PS C:\> Bcdedit /set safeboot dsrepair
    PS C:\> Shutdown /r /t 0
    ```

2. <span data-ttu-id="e31c4-184">Após o reinício de Olá, abra o snap-in cópia de segurança do Windows Server de Olá.</span><span class="sxs-lookup"><span data-stu-id="e31c4-184">After hello reboot, open hello Windows Server Backup snap-in.</span></span> <span data-ttu-id="e31c4-185">Se não souber qual o snap-in do Olá foi instalado, pesquisar computador Olá ou um servidor para **cópia de segurança do Windows Server**.</span><span class="sxs-lookup"><span data-stu-id="e31c4-185">If you don't know where hello snap-in was installed, search hello computer or server for **Windows Server Backup**.</span></span>

    <span data-ttu-id="e31c4-186">aplicação de ambiente de trabalho de Olá aparece nos resultados de pesquisa de Olá.</span><span class="sxs-lookup"><span data-stu-id="e31c4-186">hello desktop app appears in hello search results.</span></span>

3. <span data-ttu-id="e31c4-187">No snap-in Olá, selecione **cópia de segurança Local**.</span><span class="sxs-lookup"><span data-stu-id="e31c4-187">In hello snap-in, select **Local Backup**.</span></span>

    ![Selecione toorestore de cópia de segurança Local a partir daí](./media/backup-azure-restore-system-state/win-server-backup-local-backup.png)

4. <span data-ttu-id="e31c4-189">Na consola de cópia de segurança Local Olá, no Olá **painel ações**, clique em **recuperar** tooopen Olá Assistente de recuperação.</span><span class="sxs-lookup"><span data-stu-id="e31c4-189">On hello Local Backup console, in hello **Actions Pane**, click **Recover** tooopen hello Recovery Wizard.</span></span>

5. <span data-ttu-id="e31c4-190">Selecione a opção de Olá, **uma cópia de segurança armazenada noutra localização**e clique em **seguinte**.</span><span class="sxs-lookup"><span data-stu-id="e31c4-190">Select hello option, **A backup stored in another location**, and click **Next**.</span></span>

   ![Escolha toorecover tooa outro servidor](./media/backup-azure-restore-system-state/backup-stored-in-diff-location.png)

6. <span data-ttu-id="e31c4-192">Quando especificar o tipo de localização de Olá, selecione **remoto pasta partilhada** se a cópia de segurança do Estado do sistema foi recuperada tooanother servidor.</span><span class="sxs-lookup"><span data-stu-id="e31c4-192">When specifying hello location type, select **Remote shared folder** if your System State backup was recovered tooanother server.</span></span> <span data-ttu-id="e31c4-193">Se o estado do sistema foi recuperado localmente, em seguida, selecione **unidades locais**.</span><span class="sxs-lookup"><span data-stu-id="e31c4-193">If your System State was recovered locally, then select **Local drives**.</span></span> 

    ![Selecione se toorecovery do servidor local ou outro](./media/backup-azure-restore-system-state/ss-recovery-remote-shared-folder.png)

7. <span data-ttu-id="e31c4-195">Introduza Olá caminho toohello *WindowsImageBackup* diretório, ou escolha a unidade local Olá que contém este diretório (por exemplo, D:\WindowsImageBackup) recuperado como parte da recuperação de ficheiros de estado do sistema de Olá utilizando o Azure Recovery Serviços de agente e clique em **seguinte**.</span><span class="sxs-lookup"><span data-stu-id="e31c4-195">Enter hello path toohello *WindowsImageBackup* directory, or choose hello local drive containing this directory (for example, D:\WindowsImageBackup), recovered as part of hello System State files recovery using Azure Recovery Services Agent and click **Next**.</span></span>

    ![ficheiro partilhado do caminho toohello](./media/backup-azure-restore-system-state/ss-recovery-remote-folder.png)

8. <span data-ttu-id="e31c4-197">Versão de estado do sistema de Olá Selecione se pretende toorestore e clique em **seguinte**.</span><span class="sxs-lookup"><span data-stu-id="e31c4-197">Select hello System State version that you want toorestore, and click **Next**.</span></span>

9. <span data-ttu-id="e31c4-198">No painel do Olá selecionar tipo de recuperação, selecione **estado do sistema** e clique em **seguinte**.</span><span class="sxs-lookup"><span data-stu-id="e31c4-198">In hello Select Recovery Type pane, select **System State** and click **Next**.</span></span>

10. <span data-ttu-id="e31c4-199">Para a localização de Olá de Olá recuperação do Estado do sistema, selecione **localização Original**e clique em **seguinte**.</span><span class="sxs-lookup"><span data-stu-id="e31c4-199">For hello location of hello System State Recovery, select **Original Location**, and click **Next**.</span></span>

11. <span data-ttu-id="e31c4-200">Reveja os detalhes de confirmação de Olá, verifique as definições de reinício de Olá e clique em **recuperar** tooapplly Olá restaurar ficheiros de estado do sistema.</span><span class="sxs-lookup"><span data-stu-id="e31c4-200">Review hello confirmation details, verify hello reboot settings, and click **Recover** tooapplly hello restored System State files.</span></span>

    ![Iniciar Olá restaurar ficheiros de estado do sistema](./media/backup-azure-restore-system-state/launch-ss-recovery.png)

## <a name="special-considerations-for-system-state-recovery-on-active-directory-server"></a><span data-ttu-id="e31c4-202">Considerações especiais sobre a recuperação de estado do sistema no servidor do Active Directory</span><span class="sxs-lookup"><span data-stu-id="e31c4-202">Special considerations for System State recovery on Active Directory server</span></span>

<span data-ttu-id="e31c4-203">Cópia de segurança do Estado do sistema inclui dados do Active Directory.</span><span class="sxs-lookup"><span data-stu-id="e31c4-203">System State backup includes Active Directory data.</span></span> <span data-ttu-id="e31c4-204">Utilize Olá seguintes passos toorestore os serviços de domínio do Active Directory (AD DS) de estado tooa anterior estado atual.</span><span class="sxs-lookup"><span data-stu-id="e31c4-204">Use hello following steps toorestore Active Directory Domain Service (AD DS) from its current state tooa previous state.</span></span>

1. <span data-ttu-id="e31c4-205">Reinicie o controlador de domínio de Olá no serviços restaurar modo diretório (DSRM).</span><span class="sxs-lookup"><span data-stu-id="e31c4-205">Restart hello domain controller in Directory Services Restore Mode (DSRM).</span></span>
2. <span data-ttu-id="e31c4-206">Siga os passos de Olá [aqui](https://technet.microsoft.com/en-us/library/cc794755(v=ws.10).aspx) toouse Windows Server Backup cmdlets toorecover do AD DS.</span><span class="sxs-lookup"><span data-stu-id="e31c4-206">Follow hello steps [here](https://technet.microsoft.com/en-us/library/cc794755(v=ws.10).aspx) toouse Windows Server Backup cmdlets toorecover AD DS.</span></span>


## <a name="troubleshoot-failed-system-state-restore"></a><span data-ttu-id="e31c4-207">Resolver problemas de restauro de estado do sistema com falhas</span><span class="sxs-lookup"><span data-stu-id="e31c4-207">Troubleshoot failed System State restore</span></span>

<span data-ttu-id="e31c4-208">Se o processo anterior de Olá de aplicar o estado do sistema não for concluída com êxito, utilize o Windows Server Olá toorecover de ambiente de recuperação do Windows (Win RE).</span><span class="sxs-lookup"><span data-stu-id="e31c4-208">If hello previous process of applying System State does not complete successfully, use hello Windows Recovery Environment (Win RE) toorecover your Windows Server.</span></span> <span data-ttu-id="e31c4-209">Olá passos seguintes explicam como toorecover utilizando Win RE.</span><span class="sxs-lookup"><span data-stu-id="e31c4-209">hello following steps explain how toorecover using Win RE.</span></span> <span data-ttu-id="e31c4-210">Utilize esta opção apenas se o Windows Server não se inicie normalmente após um restauro do Estado do sistema.</span><span class="sxs-lookup"><span data-stu-id="e31c4-210">Use This option only if Windows Server does not boot normally after a System State restore.</span></span> <span data-ttu-id="e31c4-211">seguir o processo de Olá apague dados não pertencente ao sistema, tenha cuidado.</span><span class="sxs-lookup"><span data-stu-id="e31c4-211">hello following process erases non-system data, use caution.</span></span> 

1. <span data-ttu-id="e31c4-212">Arrancar o servidor do Windows hello ambiente de recuperação do Windows (Win RE).</span><span class="sxs-lookup"><span data-stu-id="e31c4-212">Boot your Windows Server into hello Windows Recovery Environment (Win RE).</span></span>

2. <span data-ttu-id="e31c4-213">Selecione as opções de disponíveis três Olá resolução de problemas.</span><span class="sxs-lookup"><span data-stu-id="e31c4-213">Select Troubleshoot from hello three available options.</span></span>

    ![menu abrir](./media/backup-azure-restore-system-state/winre-1.png)

3. <span data-ttu-id="e31c4-215">De Olá **opções avançadas** ecrã, selecione **linha de comandos** e forneça o nome de utilizador de administrador de servidor de Olá e a palavra-passe.</span><span class="sxs-lookup"><span data-stu-id="e31c4-215">From hello **Advanced Options** screen, select **Command Prompt** and provide hello server administrator username and password.</span></span>

   ![menu abrir](./media/backup-azure-restore-system-state/winre-2.png)

4. <span data-ttu-id="e31c4-217">Forneça o nome de utilizador de administrador de servidor de Olá e a palavra-passe.</span><span class="sxs-lookup"><span data-stu-id="e31c4-217">Provide hello server administrator username and password.</span></span>

    ![menu abrir](./media/backup-azure-restore-system-state/winre-3.png)

5. <span data-ttu-id="e31c4-219">Quando abrir Olá linha de comandos no modo de administrador, execute os seguintes versões cópia de segurança do comando tooget Olá estado do sistema.</span><span class="sxs-lookup"><span data-stu-id="e31c4-219">When you open hello command prompt in administrator mode, run following command tooget hello System State backup versions.</span></span>

    ```
    Wbadmin get versions -backuptarget:<Volume where WindowsImageBackup folder is copied>:
    ```
    ![obter versões de cópia de segurança do Estado do sistema](./media/backup-azure-restore-system-state/winre-4.png)

6. <span data-ttu-id="e31c4-221">Execute todos os volumes disponíveis na cópia de segurança de Olá de Olá tooget de comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="e31c4-221">Run hello following command tooget all volumes available in hello backup.</span></span>

    ```
    Wbadmin get items -version:<copy version from above step> -backuptarget:<Backup volume>
    ```

    ![obter versões de cópia de segurança do Estado do sistema](./media/backup-azure-restore-system-state/winre-5.png)

7. <span data-ttu-id="e31c4-223">Olá seguinte comando recupera todos os volumes que fazem parte do Olá cópia de segurança de estado de sistema.</span><span class="sxs-lookup"><span data-stu-id="e31c4-223">hello following command recovers all volumes that are part of hello System State Backup.</span></span> <span data-ttu-id="e31c4-224">Tenha em atenção que este passo recupera apenas Olá volumes críticos que fazem parte Olá do Estado do sistema.</span><span class="sxs-lookup"><span data-stu-id="e31c4-224">Note that this step recovers only hello critical volumes that are part of hello System State.</span></span> <span data-ttu-id="e31c4-225">Todos os dados de sistema não é eliminada.</span><span class="sxs-lookup"><span data-stu-id="e31c4-225">All non-System data is erased.</span></span>

    ```
    Wbadmin start recovery -items:C: -itemtype:Volume -version:<Backupversion> -backuptarget:<backup target volume>
    ```
     ![obter versões de cópia de segurança do Estado do sistema](./media/backup-azure-restore-system-state/winre-6.png)



## <a name="next-steps"></a><span data-ttu-id="e31c4-227">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="e31c4-227">Next steps</span></span>
* <span data-ttu-id="e31c4-228">Agora que recuperar os seus ficheiros e pastas, pode [gerir as cópias de segurança](backup-azure-manage-windows-server.md).</span><span class="sxs-lookup"><span data-stu-id="e31c4-228">Now that you've recovered your files and folders, you can [manage your backups](backup-azure-manage-windows-server.md).</span></span>
