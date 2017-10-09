---
title: "planos toorecovery de runbooks de automatização do Azure do aaaAdd no Azure Site Recovery | Microsoft Docs"
description: "Saiba como do Azure Site Recovery pode ajudá-lo expandir planos de recuperação através da automatização do Azure. Saiba como toocomplete complexas tarefas durante a recuperação tooAzure."
services: site-recovery
documentationcenter: 
author: ruturaj
manager: gauravd
editor: 
ms.assetid: ecece14d-5f92-4596-bbaf-5204addb95c2
ms.service: site-recovery
ms.devlang: powershell
ms.tgt_pltfrm: na
ms.topic: article
ms.workload: storage-backup-recovery
ms.date: 06/23/2017
ms.author: ruturajd@microsoft.com
ms.openlocfilehash: 90d517200cec5527e98a0d00da466bace587b70b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="add-azure-automation-runbooks-toorecovery-plans"></a><span data-ttu-id="8424d-104">Adicionar planos de toorecovery runbooks de automatização do Azure</span><span class="sxs-lookup"><span data-stu-id="8424d-104">Add Azure Automation runbooks toorecovery plans</span></span>
<span data-ttu-id="8424d-105">Neste artigo, vamos descrever como o Azure Site Recovery integra toohelp de automatização do Azure expandir os planos de recuperação.</span><span class="sxs-lookup"><span data-stu-id="8424d-105">In this article, we describe how Azure Site Recovery integrates with Azure Automation toohelp you extend your recovery plans.</span></span> <span data-ttu-id="8424d-106">Planos de recuperação podem orquestrar a recuperação de VMs que estão protegidos com a recuperação de Site.</span><span class="sxs-lookup"><span data-stu-id="8424d-106">Recovery plans can orchestrate recovery of VMs that are protected with Site Recovery.</span></span> <span data-ttu-id="8424d-107">Funcionam planos de recuperação para a nuvem de secundária de tooa de replicação tanto para tooAzure de replicação.</span><span class="sxs-lookup"><span data-stu-id="8424d-107">Recovery plans work both for replication tooa secondary cloud, and for replication tooAzure.</span></span> <span data-ttu-id="8424d-108">Planos de recuperação também ajudam a efetuar a recuperação de Olá **consistentemente exata**, **repetíveis**, e **automatizada**.</span><span class="sxs-lookup"><span data-stu-id="8424d-108">Recovery plans also help make hello recovery **consistently accurate**, **repeatable**, and **automated**.</span></span> <span data-ttu-id="8424d-109">Se falhar a tooAzure VMs, integração com a automatização do Azure expande os planos de recuperação.</span><span class="sxs-lookup"><span data-stu-id="8424d-109">If you fail over your VMs tooAzure, integration with Azure Automation extends your recovery plans.</span></span> <span data-ttu-id="8424d-110">Pode utilizá-la tooexecute runbooks, que oferece tarefas de automatização de elevado desempenho.</span><span class="sxs-lookup"><span data-stu-id="8424d-110">You can use it tooexecute runbooks, which offer powerful automation tasks.</span></span>

<span data-ttu-id="8424d-111">Se for novo tooAzure automatização, pode [inscrever](https://azure.microsoft.com/services/automation/) e [transfira scripts de exemplo](https://azure.microsoft.com/documentation/scripts/).</span><span class="sxs-lookup"><span data-stu-id="8424d-111">If you are new tooAzure Automation, you can [sign up](https://azure.microsoft.com/services/automation/) and [download sample scripts](https://azure.microsoft.com/documentation/scripts/).</span></span> <span data-ttu-id="8424d-112">Para obter mais informações e toolearn como tooorchestrate recuperação tooAzure utilizando [planos de recuperação](https://azure.microsoft.com/blog/?p=166264), consulte [do Azure Site Recovery](https://azure.microsoft.com/services/site-recovery/).</span><span class="sxs-lookup"><span data-stu-id="8424d-112">For more information, and toolearn how tooorchestrate recovery tooAzure by using [recovery plans](https://azure.microsoft.com/blog/?p=166264), see [Azure Site Recovery](https://azure.microsoft.com/services/site-recovery/).</span></span>

<span data-ttu-id="8424d-113">Neste artigo, vamos descrever a forma como pode integrar os runbooks de automatização do Azure os planos de recuperação.</span><span class="sxs-lookup"><span data-stu-id="8424d-113">In this article, we describe how you can integrate Azure Automation runbooks into your recovery plans.</span></span> <span data-ttu-id="8424d-114">Utilizamos exemplos tooautomate tarefas básicas que anteriormente necessitavam de intervenção manual.</span><span class="sxs-lookup"><span data-stu-id="8424d-114">We use examples tooautomate basic tasks that previously required manual intervention.</span></span> <span data-ttu-id="8424d-115">Podemos também descrevem como tooconvert tooa uma recuperação de vários passos clique único ação de recuperação.</span><span class="sxs-lookup"><span data-stu-id="8424d-115">We also describe how tooconvert a multi-step recovery tooa single-click recovery action.</span></span>

## <a name="customize-hello-recovery-plan"></a><span data-ttu-id="8424d-116">Personalizar o plano de recuperação Olá</span><span class="sxs-lookup"><span data-stu-id="8424d-116">Customize hello recovery plan</span></span>
1. <span data-ttu-id="8424d-117">Aceda toohello **recuperação de Site** painel de recursos do plano de recuperação.</span><span class="sxs-lookup"><span data-stu-id="8424d-117">Go toohello **Site Recovery** recovery plan resource blade.</span></span> <span data-ttu-id="8424d-118">Neste exemplo, o plano de recuperação de Olá tem dois tooit de adicionada VMs, para recuperação.</span><span class="sxs-lookup"><span data-stu-id="8424d-118">For this example, hello recovery plan has two VMs added tooit, for recovery.</span></span> <span data-ttu-id="8424d-119">toobegin adição de um runbook, clique em Olá **personalizar** separador.</span><span class="sxs-lookup"><span data-stu-id="8424d-119">toobegin adding a runbook, click hello **Customize** tab.</span></span>

    ![Clique no botão de personalizar Olá](media/site-recovery-runbook-automation-new/essentials-rp.png)


2. <span data-ttu-id="8424d-121">Clique com botão direito **grupo 1: Iniciar**e, em seguida, selecione **post adicionar ação**.</span><span class="sxs-lookup"><span data-stu-id="8424d-121">Right-click **Group 1: Start**, and then select **Add post action**.</span></span>

    ![Contexto grupo 1: Iniciar e adicionar post ação](media/site-recovery-runbook-automation-new/customize-rp.png)

3. <span data-ttu-id="8424d-123">Clique em **escolher um script**.</span><span class="sxs-lookup"><span data-stu-id="8424d-123">Click **Choose a script**.</span></span>

4. <span data-ttu-id="8424d-124">No Olá **atualizar ação** painel, o script de Olá nome **Olá mundo**.</span><span class="sxs-lookup"><span data-stu-id="8424d-124">On hello **Update action** blade, name hello script **Hello World**.</span></span>

    ![Painel de ação de atualização de Olá](media/site-recovery-runbook-automation-new/update-rp.png)

5. <span data-ttu-id="8424d-126">Introduza um nome de conta de automatização.</span><span class="sxs-lookup"><span data-stu-id="8424d-126">Enter an Automation account name.</span></span>
    >[!NOTE]
    > <span data-ttu-id="8424d-127">Olá conta de automatização pode estar em qualquer região do Azure.</span><span class="sxs-lookup"><span data-stu-id="8424d-127">hello Automation account can be in any Azure region.</span></span> <span data-ttu-id="8424d-128">conta de automatização de Olá tem de constar Olá mesma subscrição do cofre do Azure Site Recovery Olá.</span><span class="sxs-lookup"><span data-stu-id="8424d-128">hello Automation account must be in hello same subscription as hello Azure Site Recovery vault.</span></span>

6. <span data-ttu-id="8424d-129">Na sua conta de automatização, selecione um runbook.</span><span class="sxs-lookup"><span data-stu-id="8424d-129">In your Automation account, select a runbook.</span></span> <span data-ttu-id="8424d-130">Este runbook é o script de Olá que é executado durante a execução de Olá Olá do plano de recuperação, após a recuperação de Olá do primeiro grupo de Olá.</span><span class="sxs-lookup"><span data-stu-id="8424d-130">This runbook is hello script that runs during hello execution of hello recovery plan, after hello recovery of hello first group.</span></span>

7. <span data-ttu-id="8424d-131">script de Olá toosave, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="8424d-131">toosave hello script, click **OK**.</span></span> <span data-ttu-id="8424d-132">script de Olá é adicionada demasiado**grupo 1: pós-passos**.</span><span class="sxs-lookup"><span data-stu-id="8424d-132">hello script is added too**Group 1: Post-steps**.</span></span>

    ![Grupo de pós-ação de 1:Start](media/site-recovery-runbook-automation-new/addedscript-rp.PNG)


## <a name="considerations-for-adding-a-script"></a><span data-ttu-id="8424d-134">Considerações para adicionar um script</span><span class="sxs-lookup"><span data-stu-id="8424d-134">Considerations for adding a script</span></span>

* <span data-ttu-id="8424d-135">Para as opções de demasiado**eliminar um passo** ou **atualizar o script de Olá**, faça duplo clique script Olá.</span><span class="sxs-lookup"><span data-stu-id="8424d-135">For options too**delete a step** or **update hello script**, right-click hello script.</span></span>
* <span data-ttu-id="8424d-136">Um script pode executar no Azure durante a ativação pós-falha de um tooAzure de máquina no local.</span><span class="sxs-lookup"><span data-stu-id="8424d-136">A script can run on Azure during failover from an on-premises machine tooAzure.</span></span> <span data-ttu-id="8424d-137">-Também pode executar no Azure como um script de site principal antes de encerramento, durante a reativação pós-falha da máquina no local de tooan do Azure.</span><span class="sxs-lookup"><span data-stu-id="8424d-137">It also can run on Azure as a primary-site script before shutdown, during failback from Azure tooan on-premises machine.</span></span>
* <span data-ttu-id="8424d-138">Quando executa um script, injects um contexto de plano de recuperação.</span><span class="sxs-lookup"><span data-stu-id="8424d-138">When a script runs, it injects a recovery plan context.</span></span> <span data-ttu-id="8424d-139">Olá seguinte exemplo mostra uma variável de contexto:</span><span class="sxs-lookup"><span data-stu-id="8424d-139">hello following example shows a context variable:</span></span>

    ```
            {"RecoveryPlanName":"hrweb-recovery",

            "FailoverType":"Test",

            "FailoverDirection":"PrimaryToSecondary",

            "GroupId":"1",

            "VmMap":{"7a1069c6-c1d6-49c5-8c5d-33bfce8dd183":

                    { "SubscriptionId":"7a1111111-c1d6-49c5-8c5d-111ce8dd183",

                    "ResourceGroupName":"ContosoRG",

                    "CloudServiceName":"pod02hrweb-Chicago-test",

                    "RoleName":"Fabrikam-Hrweb-frontend-test",

                    "RecoveryPointId":"TimeStamp"}

                    }

            }
    ```

    <span data-ttu-id="8424d-140">Olá, a tabela seguinte lista Olá nome e uma descrição de cada variável no contexto de Olá.</span><span class="sxs-lookup"><span data-stu-id="8424d-140">hello following table lists hello name and description of each variable in hello context.</span></span>

    | <span data-ttu-id="8424d-141">**Nome da variável**</span><span class="sxs-lookup"><span data-stu-id="8424d-141">**Variable name**</span></span> | <span data-ttu-id="8424d-142">**Descrição**</span><span class="sxs-lookup"><span data-stu-id="8424d-142">**Description**</span></span> |
    | --- | --- |
    | <span data-ttu-id="8424d-143">RecoveryPlanName</span><span class="sxs-lookup"><span data-stu-id="8424d-143">RecoveryPlanName</span></span> |<span data-ttu-id="8424d-144">nome de Olá do plano de Olá a ser executado.</span><span class="sxs-lookup"><span data-stu-id="8424d-144">hello name of hello plan being run.</span></span> <span data-ttu-id="8424d-145">Esta variável ajuda a efetuar ações diferentes com base no nome do plano de recuperação Olá.</span><span class="sxs-lookup"><span data-stu-id="8424d-145">This variable helps you take different actions based on hello recovery plan name.</span></span> <span data-ttu-id="8424d-146">Também pode reutilizar script Olá.</span><span class="sxs-lookup"><span data-stu-id="8424d-146">You also can reuse hello script.</span></span> |
    | <span data-ttu-id="8424d-147">FailoverType</span><span class="sxs-lookup"><span data-stu-id="8424d-147">FailoverType</span></span> |<span data-ttu-id="8424d-148">Especifica se é um teste de ativação pós-falha de Olá, planeada ou não planeada.</span><span class="sxs-lookup"><span data-stu-id="8424d-148">Specifies whether hello failover is a test, planned, or unplanned.</span></span> |
    | <span data-ttu-id="8424d-149">FailoverDirection</span><span class="sxs-lookup"><span data-stu-id="8424d-149">FailoverDirection</span></span> |<span data-ttu-id="8424d-150">Especifica se a recuperação é o site primário ou secundário do tooa.</span><span class="sxs-lookup"><span data-stu-id="8424d-150">Specifies whether recovery is tooa primary or secondary site.</span></span> |
    | <span data-ttu-id="8424d-151">GroupID</span><span class="sxs-lookup"><span data-stu-id="8424d-151">GroupID</span></span> |<span data-ttu-id="8424d-152">Identifica o número de grupo Olá no plano de recuperação Olá quando plano Olá está em execução.</span><span class="sxs-lookup"><span data-stu-id="8424d-152">Identifies hello group number in hello recovery plan when hello plan is running.</span></span> |
    | <span data-ttu-id="8424d-153">VmMap</span><span class="sxs-lookup"><span data-stu-id="8424d-153">VmMap</span></span> |<span data-ttu-id="8424d-154">Uma matriz de todas as VMs no grupo de Olá.</span><span class="sxs-lookup"><span data-stu-id="8424d-154">An array of all VMs in hello group.</span></span> |
    | <span data-ttu-id="8424d-155">Chave de VMMap</span><span class="sxs-lookup"><span data-stu-id="8424d-155">VMMap key</span></span> |<span data-ttu-id="8424d-156">Uma chave exclusiva (GUID) para cada VM.</span><span class="sxs-lookup"><span data-stu-id="8424d-156">A unique key (GUID) for each VM.</span></span> <span data-ttu-id="8424d-157">De Olá igual Olá, Azure Virtual Machine Manager (VMM) ID Olá VM, onde for aplicável.</span><span class="sxs-lookup"><span data-stu-id="8424d-157">It's hello same as hello Azure Virtual Machine Manager (VMM) ID of hello VM, where applicable.</span></span> |
    | <span data-ttu-id="8424d-158">SubscriptionId</span><span class="sxs-lookup"><span data-stu-id="8424d-158">SubscriptionId</span></span> |<span data-ttu-id="8424d-159">Olá ID de subscrição do Azure na qual Olá VM foi criado.</span><span class="sxs-lookup"><span data-stu-id="8424d-159">hello Azure subscription ID in which hello VM was created.</span></span> |
    | <span data-ttu-id="8424d-160">RoleName</span><span class="sxs-lookup"><span data-stu-id="8424d-160">RoleName</span></span> |<span data-ttu-id="8424d-161">nome de Olá do Olá VM do Azure que está a ser recuperada.</span><span class="sxs-lookup"><span data-stu-id="8424d-161">hello name of hello Azure VM that's being recovered.</span></span> |
    | <span data-ttu-id="8424d-162">CloudServiceName</span><span class="sxs-lookup"><span data-stu-id="8424d-162">CloudServiceName</span></span> |<span data-ttu-id="8424d-163">nome do serviço em nuvem do Azure Olá que sob a qual Olá VM foi criada.</span><span class="sxs-lookup"><span data-stu-id="8424d-163">hello Azure cloud service name under which hello VM was created.</span></span> |
    | <span data-ttu-id="8424d-164">resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="8424d-164">ResourceGroupName</span></span>|<span data-ttu-id="8424d-165">nome do grupo de recursos do Azure Olá que sob a qual Olá VM foi criado.</span><span class="sxs-lookup"><span data-stu-id="8424d-165">hello Azure resource group name under which hello VM was created.</span></span> |
    | <span data-ttu-id="8424d-166">RecoveryPointId</span><span class="sxs-lookup"><span data-stu-id="8424d-166">RecoveryPointId</span></span>|<span data-ttu-id="8424d-167">Olá timestamp para quando Olá VM for recuperada.</span><span class="sxs-lookup"><span data-stu-id="8424d-167">hello timestamp for when hello VM is recovered.</span></span> |

* <span data-ttu-id="8424d-168">Certifique-se de que a conta de automatização de Olá tem Olá seguintes módulos:</span><span class="sxs-lookup"><span data-stu-id="8424d-168">Ensure that hello Automation account has hello following modules:</span></span>
    * <span data-ttu-id="8424d-169">AzureRM.profile</span><span class="sxs-lookup"><span data-stu-id="8424d-169">AzureRM.profile</span></span>
    * <span data-ttu-id="8424d-170">AzureRM.Resources</span><span class="sxs-lookup"><span data-stu-id="8424d-170">AzureRM.Resources</span></span>
    * <span data-ttu-id="8424d-171">AzureRM.Automation</span><span class="sxs-lookup"><span data-stu-id="8424d-171">AzureRM.Automation</span></span>
    * <span data-ttu-id="8424d-172">AzureRM.Network</span><span class="sxs-lookup"><span data-stu-id="8424d-172">AzureRM.Network</span></span>
    * <span data-ttu-id="8424d-173">AzureRM.Compute</span><span class="sxs-lookup"><span data-stu-id="8424d-173">AzureRM.Compute</span></span>

<span data-ttu-id="8424d-174">Todos os módulos devem ser das versões compatíveis.</span><span class="sxs-lookup"><span data-stu-id="8424d-174">All modules should be of compatible versions.</span></span> <span data-ttu-id="8424d-175">Tooensure uma forma fácil que todos os módulos são compatíveis é toouse versões mais recentes do Olá de todos os módulos de Olá.</span><span class="sxs-lookup"><span data-stu-id="8424d-175">An easy way tooensure that all modules are compatible is toouse hello latest versions of all hello modules.</span></span>

### <a name="access-all-vms-of-hello-vmmap-in-a-loop"></a><span data-ttu-id="8424d-176">Aceder a todas as VMs de Olá VMMap num ciclo</span><span class="sxs-lookup"><span data-stu-id="8424d-176">Access all VMs of hello VMMap in a loop</span></span>
<span data-ttu-id="8424d-177">Utilize Olá seguir tooloop de código em todas as VMs de Olá Microsoft VMMap:</span><span class="sxs-lookup"><span data-stu-id="8424d-177">Use hello following code tooloop across all VMs of hello Microsoft VMMap:</span></span>

```
$VMinfo = $RecoveryPlanContext.VmMap | Get-Member | Where-Object MemberType -EQ NoteProperty | select -ExpandProperty Name
$vmMap = $RecoveryPlanContext.VmMap
 foreach($VMID in $VMinfo)
 {
     $VM = $vmMap.$VMID                
             if( !(($VM -eq $Null) -Or ($VM.ResourceGroupName -eq $Null) -Or ($VM.RoleName -eq $Null))) {
         #this check is tooensure that we skip when some data is not available else it will fail
 Write-output "Resource group name ", $VM.ResourceGroupName
 Write-output "Rolename " = $VM.RoleName
     }
 }

```

> [!NOTE]
> <span data-ttu-id="8424d-178">Olá recursos grupo e função de valores de nome estão vazios quando o script de Olá é um grupo de arranque de pré-ação tooa.</span><span class="sxs-lookup"><span data-stu-id="8424d-178">hello resource group name and role name values are empty when hello script is a pre-action tooa boot group.</span></span> <span data-ttu-id="8424d-179">valores de Olá são preenchidos apenas se Olá VM desse grupo for bem sucedida na ativação pós-falha.</span><span class="sxs-lookup"><span data-stu-id="8424d-179">hello values are populated only if hello VM of that group succeeds in failover.</span></span> <span data-ttu-id="8424d-180">script de Olá é uma pós-ação de do grupo de arranque Olá.</span><span class="sxs-lookup"><span data-stu-id="8424d-180">hello script is a post-action of hello boot group.</span></span>

## <a name="use-hello-same-automation-runbook-in-multiple-recovery-plans"></a><span data-ttu-id="8424d-181">Utilize Olá mesmo runbook da automatização em vários planos de recuperação</span><span class="sxs-lookup"><span data-stu-id="8424d-181">Use hello same Automation runbook in multiple recovery plans</span></span>

<span data-ttu-id="8424d-182">Pode utilizar um script único nos vários planos de recuperação através da utilização de variáveis externas.</span><span class="sxs-lookup"><span data-stu-id="8424d-182">You can use a single script in multiple recovery plans by using external variables.</span></span> <span data-ttu-id="8424d-183">Pode utilizar [variáveis da automatização do Azure](../automation/automation-variables.md) toostore parâmetros que podem passar para a recuperação de uma plano de execução.</span><span class="sxs-lookup"><span data-stu-id="8424d-183">You can use [Azure Automation variables](../automation/automation-variables.md) toostore parameters that you can pass for a recovery plan execution.</span></span> <span data-ttu-id="8424d-184">Ao adicionar o nome do plano de recuperação Olá como uma variável de toohello de prefixo, pode criar variáveis individuais para cada plano de recuperação.</span><span class="sxs-lookup"><span data-stu-id="8424d-184">By adding hello recovery plan name as a prefix toohello variable, you can create individual variables for each recovery plan.</span></span> <span data-ttu-id="8424d-185">Em seguida, utilize variáveis de Olá como parâmetros.</span><span class="sxs-lookup"><span data-stu-id="8424d-185">Then, use hello variables as parameters.</span></span> <span data-ttu-id="8424d-186">Pode alterar o parâmetro sem alterar o script de Olá, mas ainda alteração Olá Olá forma script funciona.</span><span class="sxs-lookup"><span data-stu-id="8424d-186">You can change a parameter without changing hello script, but still change hello way hello script works.</span></span>

### <a name="use-a-simple-string-variable-in-a-runbook-script"></a><span data-ttu-id="8424d-187">Utilizar uma variável de cadeia simples num runbook script</span><span class="sxs-lookup"><span data-stu-id="8424d-187">Use a simple string variable in a runbook script</span></span>

<span data-ttu-id="8424d-188">Neste exemplo, um script aceita entrada de Olá de um grupo de segurança de rede (NSG) e aplica-se de as VMs de toohello de um plano de recuperação.</span><span class="sxs-lookup"><span data-stu-id="8424d-188">In this example, a script takes hello input of a Network Security Group (NSG) and applies it toohello VMs of a recovery plan.</span></span>

<span data-ttu-id="8424d-189">Para Olá toodetect de script que plano de recuperação está em execução, utilize o contexto de plano de recuperação Olá:</span><span class="sxs-lookup"><span data-stu-id="8424d-189">For hello script toodetect which recovery plan is running, use hello recovery plan context:</span></span>

```
workflow AddPublicIPAndNSG {
    param (
          [parameter(Mandatory=$false)]
          [Object]$RecoveryPlanContext
    )

    $RPName = $RecoveryPlanContext.RecoveryPlanName
```

<span data-ttu-id="8424d-190">tooapply um NSG existente, tem de saber nome NSG Olá e nome do grupo de recursos do Olá NSG.</span><span class="sxs-lookup"><span data-stu-id="8424d-190">tooapply an existing NSG, you must know hello NSG name and hello NSG resource group name.</span></span> <span data-ttu-id="8424d-191">Utilize estas variáveis como entradas para os scripts de plano de recuperação.</span><span class="sxs-lookup"><span data-stu-id="8424d-191">Use these variables as inputs for recovery plan scripts.</span></span> <span data-ttu-id="8424d-192">toodo isto, crie duas variáveis no Olá ativos de conta de automatização.</span><span class="sxs-lookup"><span data-stu-id="8424d-192">toodo this, create two variables in hello Automation account assets.</span></span> <span data-ttu-id="8424d-193">Adicione nome Olá Olá do plano de recuperação que está a criar os parâmetros de Olá para como um nome de variável de toohello prefixo.</span><span class="sxs-lookup"><span data-stu-id="8424d-193">Add hello name of hello recovery plan that you are creating hello parameters for as a prefix toohello variable name.</span></span>

1. <span data-ttu-id="8424d-194">Crie um nome NSG Olá toostore variável.</span><span class="sxs-lookup"><span data-stu-id="8424d-194">Create a variable toostore hello NSG name.</span></span> <span data-ttu-id="8424d-195">Adicione um nome de variável de toohello de prefixo utilizando o nome de Olá Olá do plano de recuperação.</span><span class="sxs-lookup"><span data-stu-id="8424d-195">Add a prefix toohello variable name by using hello name of hello recovery plan.</span></span>

    ![Criar uma variável de nome do NSG](media/site-recovery-runbook-automation-new/var1.png)

2. <span data-ttu-id="8424d-197">Crie o nome do grupo de recursos de uma variável toostore Olá NSG.</span><span class="sxs-lookup"><span data-stu-id="8424d-197">Create a variable toostore hello NSG's resource group name.</span></span> <span data-ttu-id="8424d-198">Adicione um nome de variável de toohello de prefixo utilizando o nome de Olá Olá do plano de recuperação.</span><span class="sxs-lookup"><span data-stu-id="8424d-198">Add a prefix toohello variable name by using hello name of hello recovery plan.</span></span>

    ![Criar um nome de grupo de recursos do NSG](media/site-recovery-runbook-automation-new/var2.png)


3.  <span data-ttu-id="8424d-200">No script de Olá, utilize Olá referência código tooget Olá os valores das variáveis os seguintes:</span><span class="sxs-lookup"><span data-stu-id="8424d-200">In hello script, use hello following reference code tooget hello variable values:</span></span>

    ```
    $NSGValue = $RecoveryPlanContext.RecoveryPlanName + "-NSG"
    $NSGRGValue = $RecoveryPlanContext.RecoveryPlanName + "-NSGRG"

    $NSGnameVar = Get-AutomationVariable -Name $NSGValue
    $RGnameVar = Get-AutomationVariable -Name $NSGRGValue
    ```

4.  <span data-ttu-id="8424d-201">Utilize Olá variáveis no Olá runbook tooapply Olá NSG toohello interface de rede de Olá efetuada a ativação pós-falha VM:</span><span class="sxs-lookup"><span data-stu-id="8424d-201">Use hello variables in hello runbook tooapply hello NSG toohello network interface of hello failed-over VM:</span></span>

    ```
    InlineScript {
    if (($Using:NSGname -ne $Null) -And ($Using:NSGRGname -ne $Null)) {
            $NSG = Get-AzureRmNetworkSecurityGroup -Name $Using:NSGname -ResourceGroupName $Using:NSGRGname
            Write-output $NSG.Id
            #Apply hello NSG tooa network interface
            #$vnet = Get-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet
            #Set-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name FrontEnd `
            #  -AddressPrefix 192.168.1.0/24 -NetworkSecurityGroup $NSG
        }
    }
    ```

<span data-ttu-id="8424d-202">Para cada plano de recuperação, crie variáveis independentes, para que possa reutilizar o script de Olá.</span><span class="sxs-lookup"><span data-stu-id="8424d-202">For each recovery plan, create independent variables so that you can reuse hello script.</span></span> <span data-ttu-id="8424d-203">Adicione um prefixo com o nome do plano de recuperação Olá.</span><span class="sxs-lookup"><span data-stu-id="8424d-203">Add a prefix by using hello recovery plan name.</span></span> <span data-ttu-id="8424d-204">Para um script completado, ponto a ponto para este cenário, consulte [adicionar um tooVMs IP e NSG público durante a ativação pós-falha de teste de um plano de recuperação do Site Recovery](https://gallery.technet.microsoft.com/Add-Public-IP-and-NSG-to-a6bb8fee).</span><span class="sxs-lookup"><span data-stu-id="8424d-204">For a complete, end-to-end script for this scenario, see [Add a public IP and NSG tooVMs during test failover of a Site Recovery recovery plan](https://gallery.technet.microsoft.com/Add-Public-IP-and-NSG-to-a6bb8fee).</span></span>


### <a name="use-a-complex-variable-toostore-more-information"></a><span data-ttu-id="8424d-205">Utilizar uma variável de complexas toostore obter mais informações</span><span class="sxs-lookup"><span data-stu-id="8424d-205">Use a complex variable toostore more information</span></span>

<span data-ttu-id="8424d-206">Considere um cenário em que pretende tooturn um script único num IP público em VMs específicos.</span><span class="sxs-lookup"><span data-stu-id="8424d-206">Consider a scenario in which you want a single script tooturn on a public IP on specific VMs.</span></span> <span data-ttu-id="8424d-207">Outro cenário, é aconselhável tooapply NSGs diferentes em diferentes VMs (e não em todas as VMs).</span><span class="sxs-lookup"><span data-stu-id="8424d-207">In another scenario, you might want tooapply different NSGs on different VMs (not on all VMs).</span></span> <span data-ttu-id="8424d-208">Pode efetuar um script que é reutilizável para qualquer plano de recuperação.</span><span class="sxs-lookup"><span data-stu-id="8424d-208">You can make a script that is reusable for any recovery plan.</span></span> <span data-ttu-id="8424d-209">Cada plano de recuperação pode ter um número de VMs de variável.</span><span class="sxs-lookup"><span data-stu-id="8424d-209">Each recovery plan can have a variable number of VMs.</span></span> <span data-ttu-id="8424d-210">Por exemplo, uma recuperação do SharePoint tem dois front-ends.</span><span class="sxs-lookup"><span data-stu-id="8424d-210">For example, a SharePoint recovery has two front ends.</span></span> <span data-ttu-id="8424d-211">Uma aplicação básica linha de negócio (LOB) tem apenas um front-end.</span><span class="sxs-lookup"><span data-stu-id="8424d-211">A basic line-of-business (LOB) application has only one front end.</span></span> <span data-ttu-id="8424d-212">Não é possível criar variáveis separadas para cada plano de recuperação.</span><span class="sxs-lookup"><span data-stu-id="8424d-212">You cannot create separate variables for each recovery plan.</span></span> 

<span data-ttu-id="8424d-213">No seguinte exemplo de Olá, iremos utilizar uma novo técnica e criar um [complexas variável](https://msdn.microsoft.com/library/dn913767.aspx?f=255&MSPPError=-2147217396) em recursos de conta de automatização do Azure Olá.</span><span class="sxs-lookup"><span data-stu-id="8424d-213">In hello following example, we use a new technique and create a [complex variable](https://msdn.microsoft.com/library/dn913767.aspx?f=255&MSPPError=-2147217396) in hello Azure Automation account assets.</span></span> <span data-ttu-id="8424d-214">Fazê-lo especificando valores múltiplos.</span><span class="sxs-lookup"><span data-stu-id="8424d-214">You do this by specifying multiple values.</span></span> <span data-ttu-id="8424d-215">Tem de utilizar o Azure PowerShell toocomplete Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="8424d-215">You must use Azure PowerShell toocomplete hello following steps:</span></span>

1. <span data-ttu-id="8424d-216">No PowerShell, inicie sessão tooyour subscrição do Azure:</span><span class="sxs-lookup"><span data-stu-id="8424d-216">In PowerShell, sign in tooyour Azure subscription:</span></span>

    ```
    login-azurermaccount
    $sub = Get-AzureRmSubscription -Name <SubscriptionName>
    $sub | Select-AzureRmSubscription
    ```

2. <span data-ttu-id="8424d-217">parâmetros de Olá toostore, criar Olá complexas variável utilizando o nome de Olá Olá do plano de recuperação:</span><span class="sxs-lookup"><span data-stu-id="8424d-217">toostore hello parameters, create hello complex variable by using hello name of hello recovery plan:</span></span>

    ```
    $VMDetails = @{"VMGUID"=@{"ResourceGroupName"="RGNameOfNSG";"NSGName"="NameOfNSG"};"VMGUID2"=@{"ResourceGroupName"="RGNameOfNSG";"NSGName"="NameOfNSG"}}
        New-AzureRmAutomationVariable -ResourceGroupName <RG of Automation Account> -AutomationAccountName <AA Name> -Name <RecoveryPlanName> -Value $VMDetails -Encrypted $false
    ```

3. <span data-ttu-id="8424d-218">Nesta variável complexas, **VMDetails** é Olá ID de VM para Olá protegidas VM.</span><span class="sxs-lookup"><span data-stu-id="8424d-218">In this complex variable, **VMDetails** is hello VM ID for hello protected VM.</span></span> <span data-ttu-id="8424d-219">ID de VM, do tooget Olá no portal do Azure, de Olá ver propriedades VM de Olá.</span><span class="sxs-lookup"><span data-stu-id="8424d-219">tooget hello VM ID, in hello Azure portal, view hello VM properties.</span></span> <span data-ttu-id="8424d-220">Olá seguinte captura de ecrã mostra uma variável que armazena detalhes de Olá de duas VMs:</span><span class="sxs-lookup"><span data-stu-id="8424d-220">hello following screenshot shows a variable that stores hello details of two VMs:</span></span>

    ![Utilizar Olá ID de VM, como Olá GUID](media/site-recovery-runbook-automation-new/vmguid.png)

4. <span data-ttu-id="8424d-222">Utilize esta variável no runbook.</span><span class="sxs-lookup"><span data-stu-id="8424d-222">Use this variable in your runbook.</span></span> <span data-ttu-id="8424d-223">Se Olá indicado que GUID da VM se encontra no contexto de plano de recuperação Olá, aplicar Olá NSG Olá VM:</span><span class="sxs-lookup"><span data-stu-id="8424d-223">If hello indicated VM GUID is found in hello recovery plan context, apply hello NSG on hello VM:</span></span>

    ```
    $VMDetailsObj = Get-AutomationVariable -Name $RecoveryPlanContext.RecoveryPlanName
    ```

4. <span data-ttu-id="8424d-224">No runbook, percorrer Olá VMs do contexto de plano de recuperação Olá.</span><span class="sxs-lookup"><span data-stu-id="8424d-224">In your runbook, loop through hello VMs of hello recovery plan context.</span></span> <span data-ttu-id="8424d-225">Verifique se Olá VM existe no **$VMDetailsObj**.</span><span class="sxs-lookup"><span data-stu-id="8424d-225">Check whether hello VM exists in **$VMDetailsObj**.</span></span> <span data-ttu-id="8424d-226">Se existir, aceder às propriedades de Olá da Olá de variável tooapply Olá NSG:</span><span class="sxs-lookup"><span data-stu-id="8424d-226">If it exists, access hello properties of hello variable tooapply hello NSG:</span></span>

    ```
        $VMinfo = $RecoveryPlanContext.VmMap | Get-Member | Where-Object MemberType -EQ NoteProperty | select -ExpandProperty Name
        $vmMap = $RecoveryPlanContext.VmMap

        foreach($VMID in $VMinfo) {
            Write-output $VMDetailsObj.value.$VMID

            if ($VMDetailsObj.value.$VMID -ne $Null) { #If hello VM exists in hello context, this will not b Null
                $VM = $vmMap.$VMID
                # Access hello properties of hello variable
                $NSGname = $VMDetailsObj.value.$VMID.'NSGName'
                $NSGRGname = $VMDetailsObj.value.$VMID.'NSGResourceGroupName'

                # Add code tooapply hello NSG properties toohello VM
            }
        }
    ```

<span data-ttu-id="8424d-227">Pode utilizar Olá mesmo script para planos de recuperação diferente.</span><span class="sxs-lookup"><span data-stu-id="8424d-227">You can use hello same script for different recovery plans.</span></span> <span data-ttu-id="8424d-228">Introduza diferentes parâmetros armazenando valor Olá que corresponde ao plano de recuperação tooa em diferentes variáveis.</span><span class="sxs-lookup"><span data-stu-id="8424d-228">Enter different parameters by storing hello value that corresponds tooa recovery plan in different variables.</span></span>

## <a name="sample-scripts"></a><span data-ttu-id="8424d-229">Scripts de exemplo</span><span class="sxs-lookup"><span data-stu-id="8424d-229">Sample scripts</span></span>

<span data-ttu-id="8424d-230">tooyour de scripts de exemplo toodeploy conta de automatização, clique em Olá **implementar tooAzure** botão.</span><span class="sxs-lookup"><span data-stu-id="8424d-230">toodeploy sample scripts tooyour Automation account, click hello **Deploy tooAzure** button.</span></span>

<span data-ttu-id="8424d-231">[![Implementar tooAzure](https://azurecomcdn.azureedge.net/mediahandler/acomblog/media/Default/blog/c4803408-340e-49e3-9a1f-0ed3f689813d.png)](https://aka.ms/asr-automationrunbooks-deploy)</span><span class="sxs-lookup"><span data-stu-id="8424d-231">[![Deploy tooAzure](https://azurecomcdn.azureedge.net/mediahandler/acomblog/media/Default/blog/c4803408-340e-49e3-9a1f-0ed3f689813d.png)](https://aka.ms/asr-automationrunbooks-deploy)</span></span>

<span data-ttu-id="8424d-232">Para obter outro exemplo, consulte Olá seguir as vídeo.</span><span class="sxs-lookup"><span data-stu-id="8424d-232">For another example, see hello following video.</span></span> <span data-ttu-id="8424d-233">Demonstra como toorecover um tooAzure de aplicação do WordPress de duas camadas:</span><span class="sxs-lookup"><span data-stu-id="8424d-233">It demonstrates how toorecover a two-tier WordPress application tooAzure:</span></span>


> [!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/One-click-failover-of-a-2-tier-WordPress-application-using-Azure-Site-Recovery/player]



## <a name="additional-resources"></a><span data-ttu-id="8424d-234">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="8424d-234">Additional resources</span></span>
* [<span data-ttu-id="8424d-235">Conta do Azure Automation serviço Run As</span><span class="sxs-lookup"><span data-stu-id="8424d-235">Azure Automation service Run As account</span></span>](../automation/automation-sec-configure-azure-runas-account.md)
* [<span data-ttu-id="8424d-236">Descrição geral de automatização do Azure</span><span class="sxs-lookup"><span data-stu-id="8424d-236">Azure Automation overview</span></span>](http://msdn.microsoft.com/library/azure/dn643629.aspx "descrição geral da automatização do Azure")
* [<span data-ttu-id="8424d-237">Scripts de exemplo de automatização do Azure</span><span class="sxs-lookup"><span data-stu-id="8424d-237">Azure Automation sample scripts</span></span>](http://gallery.technet.microsoft.com/scriptcenter/site/search?f\[0\].Type=User&f\[0\].Value=SC%20Automation%20Product%20Team&f\[0\].Text=SC%20Automation%20Product%20Team "scripts de exemplo da automatização do Azure")
