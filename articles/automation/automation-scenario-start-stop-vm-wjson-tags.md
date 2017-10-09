---
title: aaaUse estado da VM do Azure tooschedule etiquetas formatada em JSON | Microsoft Docs
description: "Este artigo demonstra como toouse JSON cadeias em etiquetas tooautomate Olá agendamento de VM de arranque e encerramento."
services: automation
documentationcenter: 
author: MGoedtel
manager: jwhit
editor: tysonn
ms.assetid: 6afed5d2-e939-4749-8b2c-9312b4c16fb2
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: magoedte;paulomarquesc
ms.openlocfilehash: f6bbf1dea1c193e5d1010f12f3b1ed63562f9daf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-automation-scenario-using-json-formatted-tags-toocreate-a-schedule-for-azure-vm-startup-and-shutdown"></a><span data-ttu-id="61d69-103">Cenário de automatização do Azure: utilizar a formatados em JSON etiquetas toocreate uma agenda para a VM do Azure de arranque e encerramento</span><span class="sxs-lookup"><span data-stu-id="61d69-103">Azure Automation scenario: Using JSON-formatted tags toocreate a schedule for Azure VM startup and shutdown</span></span>
<span data-ttu-id="61d69-104">Os clientes pretendem, muitas vezes, o arranque de Olá tooschedule e encerramento de máquinas virtuais toohelp reduzir os custos de subscrição ou empresariais e requisitos técnicos de suporte.</span><span class="sxs-lookup"><span data-stu-id="61d69-104">Customers often want tooschedule hello startup and shutdown of virtual machines toohelp reduce subscription costs or support business and technical requirements.</span></span>

<span data-ttu-id="61d69-105">Olá seguinte cenário permite-lhe tooset cópias de segurança automatizada de arranque e encerramento das suas VMs através da utilização de uma tag denominada agenda a um nível de máquina virtual no Azure ou ao nível do grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="61d69-105">hello following scenario enables you tooset up automated startup and shutdown of your VMs by using a tag called Schedule at a resource group level or virtual machine level in Azure.</span></span> <span data-ttu-id="61d69-106">Este agendamento pode ser configurado de Domingo tooSaturday com um tempo de arranque e o tempo de encerramento.</span><span class="sxs-lookup"><span data-stu-id="61d69-106">This schedule can be configured from Sunday tooSaturday with a startup time and shutdown time.</span></span>

<span data-ttu-id="61d69-107">Temos algumas opções de out of box.</span><span class="sxs-lookup"><span data-stu-id="61d69-107">We do have some out-of-the-box options.</span></span> <span data-ttu-id="61d69-108">Estas incluem:</span><span class="sxs-lookup"><span data-stu-id="61d69-108">These include:</span></span>

* <span data-ttu-id="61d69-109">[Conjuntos de dimensionamento de máquina virtual](../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md) com definições de dimensionamento automático que lhe permitem tooscale entrada ou saída.</span><span class="sxs-lookup"><span data-stu-id="61d69-109">[Virtual machine scale sets](../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md) with autoscale settings that enable you tooscale in or out.</span></span>
* <span data-ttu-id="61d69-110">[DevTest Labs](../devtest-lab/devtest-lab-overview.md) serviço, que tem Olá capacidade incorporada do agendamento de arranque e encerramento operações.</span><span class="sxs-lookup"><span data-stu-id="61d69-110">[DevTest Labs](../devtest-lab/devtest-lab-overview.md) service, which has hello built-in capability of scheduling startup and shutdown operations.</span></span>

<span data-ttu-id="61d69-111">No entanto, estas opções só suportam cenários específicos e não pode ser aplicado tooinfrastructure-como-um-serviço (IaaS) VMs.</span><span class="sxs-lookup"><span data-stu-id="61d69-111">However, these options only support specific scenarios and cannot be applied tooinfrastructure-as-a-service (IaaS) VMs.</span></span>

<span data-ttu-id="61d69-112">Quando Olá tag da agenda é aplicado tooa grupo de recursos, também é aplicado tooall máquinas de virtuais dentro desse grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="61d69-112">When hello Schedule tag is applied tooa resource group, it's also applied tooall virtual machines inside that resource group.</span></span> <span data-ttu-id="61d69-113">Se uma agenda também é diretamente aplicado tooa VM, agenda último Olá prevalece no Olá seguinte ordem:</span><span class="sxs-lookup"><span data-stu-id="61d69-113">If a schedule is also directly applied tooa VM, hello last schedule takes precedence in hello following order:</span></span>

1. <span data-ttu-id="61d69-114">Grupo de recursos de tooa aplicados agenda</span><span class="sxs-lookup"><span data-stu-id="61d69-114">Schedule applied tooa resource group</span></span>
2. <span data-ttu-id="61d69-115">Agendar o grupo de recursos de tooa aplicadas e a máquina virtual no grupo de recursos de Olá</span><span class="sxs-lookup"><span data-stu-id="61d69-115">Schedule applied tooa resource group and virtual machine in hello resource group</span></span>
3. <span data-ttu-id="61d69-116">Agendar a máquina virtual de tooa aplicados</span><span class="sxs-lookup"><span data-stu-id="61d69-116">Schedule applied tooa virtual machine</span></span>

<span data-ttu-id="61d69-117">Neste cenário, essencialmente, demora uma cadeia JSON com formato especificado e adiciona-o como valor de Olá para uma tag denominada agenda.</span><span class="sxs-lookup"><span data-stu-id="61d69-117">This scenario essentially takes a JSON string with a specified format and adds it as hello value for a tag called Schedule.</span></span> <span data-ttu-id="61d69-118">Em seguida, um runbook apresenta uma lista de todos os grupos de recursos e máquinas virtuais e identifica as agendas de Olá para cada VM com base em cenários de Olá listados anteriormente.</span><span class="sxs-lookup"><span data-stu-id="61d69-118">Then a runbook lists all resource groups and virtual machines and identifies hello schedules for each VM based on hello scenarios listed earlier.</span></span> <span data-ttu-id="61d69-119">Em seguida repetido ao longo Olá VMs que têm agendas ligadas e avalia que deverão ser executadas.</span><span class="sxs-lookup"><span data-stu-id="61d69-119">Next it loops through hello VMs that have schedules attached and evaluates what action should be taken.</span></span> <span data-ttu-id="61d69-120">Por exemplo, determina quais as VMs necessitar toobe parar, encerrar ou ignoradas.</span><span class="sxs-lookup"><span data-stu-id="61d69-120">For example, it determines which VMs need toobe stopped, shut down, or ignored.</span></span>

<span data-ttu-id="61d69-121">Estes runbooks autenticar utilizando Olá [conta Run As do Azure](automation-sec-configure-azure-runas-account.md).</span><span class="sxs-lookup"><span data-stu-id="61d69-121">These runbooks authenticate by using hello [Azure Run As account](automation-sec-configure-azure-runas-account.md).</span></span>

## <a name="download-hello-runbooks-for-hello-scenario"></a><span data-ttu-id="61d69-122">Transferir runbooks Olá para o cenário de Olá</span><span class="sxs-lookup"><span data-stu-id="61d69-122">Download hello runbooks for hello scenario</span></span>
<span data-ttu-id="61d69-123">Este cenário consiste em quatro runbooks do fluxo de trabalho do PowerShell que pode transferir da Olá [TechNet Gallery](https://gallery.technet.microsoft.com/Azure-Automation-Runbooks-84f0efc7) ou Olá [GitHub](https://github.com/paulomarquesdacosta/azure-automation-scheduled-shutdown-and-startup) repositório para este projeto.</span><span class="sxs-lookup"><span data-stu-id="61d69-123">This scenario consists of four PowerShell Workflow runbooks that you can download from hello [TechNet Gallery](https://gallery.technet.microsoft.com/Azure-Automation-Runbooks-84f0efc7) or hello [GitHub](https://github.com/paulomarquesdacosta/azure-automation-scheduled-shutdown-and-startup) repository for this project.</span></span>

| <span data-ttu-id="61d69-124">Runbook</span><span class="sxs-lookup"><span data-stu-id="61d69-124">Runbook</span></span> | <span data-ttu-id="61d69-125">Descrição</span><span class="sxs-lookup"><span data-stu-id="61d69-125">Description</span></span> |
| --- | --- |
| <span data-ttu-id="61d69-126">Teste ResourceSchedule</span><span class="sxs-lookup"><span data-stu-id="61d69-126">Test-ResourceSchedule</span></span> |<span data-ttu-id="61d69-127">Verifica cada agenda de máquina virtual e efetua o encerramento ou de arranque, consoante a agenda de Olá.</span><span class="sxs-lookup"><span data-stu-id="61d69-127">Checks each virtual machine schedule and performs shutdown or startup depending on hello schedule.</span></span> |
| <span data-ttu-id="61d69-128">ResourceSchedule adicionar</span><span class="sxs-lookup"><span data-stu-id="61d69-128">Add-ResourceSchedule</span></span> |<span data-ttu-id="61d69-129">Adiciona Olá agenda tag tooa VM ou grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="61d69-129">Adds hello Schedule tag tooa VM or resource group.</span></span> |
| <span data-ttu-id="61d69-130">Atualização ResourceSchedule</span><span class="sxs-lookup"><span data-stu-id="61d69-130">Update-ResourceSchedule</span></span> |<span data-ttu-id="61d69-131">Modifica a tag de agenda existente Olá, substituindo-lo com um novo.</span><span class="sxs-lookup"><span data-stu-id="61d69-131">Modifies hello existing Schedule tag by replacing it with a new one.</span></span> |
| <span data-ttu-id="61d69-132">Remover ResourceSchedule</span><span class="sxs-lookup"><span data-stu-id="61d69-132">Remove-ResourceSchedule</span></span> |<span data-ttu-id="61d69-133">Remove a tag de agenda Olá de um VM ou grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="61d69-133">Removes hello Schedule tag from a VM or resource group.</span></span> |

## <a name="install-and-configure-this-scenario"></a><span data-ttu-id="61d69-134">Instalar e configurar este cenário</span><span class="sxs-lookup"><span data-stu-id="61d69-134">Install and configure this scenario</span></span>
### <a name="install-and-publish-hello-runbooks"></a><span data-ttu-id="61d69-135">Instalar e publicar runbooks Olá</span><span class="sxs-lookup"><span data-stu-id="61d69-135">Install and publish hello runbooks</span></span>
<span data-ttu-id="61d69-136">Depois de transferir runbooks Olá, pode importá-los utilizando o procedimento Olá [criar ou importar um runbook na automatização do Azure](automation-creating-importing-runbook.md#importing-a-runbook-from-a-file-into-azure-automation).</span><span class="sxs-lookup"><span data-stu-id="61d69-136">After downloading hello runbooks, you can import them by using hello procedure in [Creating or importing a runbook in Azure Automation](automation-creating-importing-runbook.md#importing-a-runbook-from-a-file-into-azure-automation).</span></span>  <span data-ttu-id="61d69-137">Publica cada runbook após tem foi importada com êxito na sua conta de automatização.</span><span class="sxs-lookup"><span data-stu-id="61d69-137">Publish each runbook after it has been successfully imported into your Automation account.</span></span>

### <a name="add-a-schedule-toohello-test-resourceschedule-runbook"></a><span data-ttu-id="61d69-138">Adicionar um runbook de toohello ResourceSchedule de teste de agenda</span><span class="sxs-lookup"><span data-stu-id="61d69-138">Add a schedule toohello Test-ResourceSchedule runbook</span></span>
<span data-ttu-id="61d69-139">Siga estes passos tooenable Olá agenda Olá teste ResourceSchedule runbook.</span><span class="sxs-lookup"><span data-stu-id="61d69-139">Follow these steps tooenable hello schedule for hello Test-ResourceSchedule runbook.</span></span> <span data-ttu-id="61d69-140">Esta é Olá runbook que verifica a máquinas virtuais que deverão ser iniciadas, encerrar ou à esquerda é.</span><span class="sxs-lookup"><span data-stu-id="61d69-140">This is hello runbook that verifies which virtual machines should be started, shut down, or left as is.</span></span>

1. <span data-ttu-id="61d69-141">Olá portal do Azure, abra a sua conta de automatização e, em seguida, clique em Olá **Runbooks** mosaico.</span><span class="sxs-lookup"><span data-stu-id="61d69-141">From hello Azure portal, open your Automation account, and then click hello **Runbooks** tile.</span></span>
2. <span data-ttu-id="61d69-142">No Olá **teste ResourceSchedule** painel, clique em Olá **agendas** mosaico.</span><span class="sxs-lookup"><span data-stu-id="61d69-142">On hello **Test-ResourceSchedule** blade, click hello **Schedules** tile.</span></span>
3. <span data-ttu-id="61d69-143">No Olá **agendas** painel, clique em **adicionar uma agenda**.</span><span class="sxs-lookup"><span data-stu-id="61d69-143">On hello **Schedules** blade, click **Add a schedule**.</span></span>
4. <span data-ttu-id="61d69-144">No Olá **agendas** painel, selecione **ligar um runbook de tooyour agenda**.</span><span class="sxs-lookup"><span data-stu-id="61d69-144">On hello **Schedules** blade, select **Link a schedule tooyour runbook**.</span></span> <span data-ttu-id="61d69-145">Em seguida, selecione **criar uma nova agenda**.</span><span class="sxs-lookup"><span data-stu-id="61d69-145">Then select **Create a new schedule**.</span></span>
5. <span data-ttu-id="61d69-146">No Olá **nova agenda** painel, escreva o nome de Olá desta agenda, por exemplo: *HourlyExecution*.</span><span class="sxs-lookup"><span data-stu-id="61d69-146">On hello **New schedule** blade, type in hello name of this schedule, for example: *HourlyExecution*.</span></span>
6. <span data-ttu-id="61d69-147">Para a agenda de Olá **iniciar**, defina o incremento de hora do Olá início tempo tooan.</span><span class="sxs-lookup"><span data-stu-id="61d69-147">For hello schedule **Start**, set hello start time tooan hour increment.</span></span>
7. <span data-ttu-id="61d69-148">Selecione **periodicidade**e, em seguida, para **repetir a cada intervalo**, selecione **1 hora**.</span><span class="sxs-lookup"><span data-stu-id="61d69-148">Select **Recurrence**, and then for **Recur every interval**, select **1 hour**.</span></span>
8. <span data-ttu-id="61d69-149">Certifique-se de que **definir expiração** estiver definido demasiado**não**e, em seguida, clique em **criar** toosave a agenda de novo.</span><span class="sxs-lookup"><span data-stu-id="61d69-149">Verify that **Set expiration** is set too**No**, and then click **Create** toosave your new schedule.</span></span>
9. <span data-ttu-id="61d69-150">No Olá **agenda Runbook** painel de opções, selecione **parâmetros e definições de execução**.</span><span class="sxs-lookup"><span data-stu-id="61d69-150">On hello **Schedule Runbook** options blade, select **Parameters and run settings**.</span></span> <span data-ttu-id="61d69-151">No Olá teste ResourceSchedule **parâmetros** painel, introduza o nome de Olá da sua subscrição no Olá **SubscriptionName** campo.</span><span class="sxs-lookup"><span data-stu-id="61d69-151">In hello Test-ResourceSchedule **Parameters** blade, enter hello name of your subscription in hello **SubscriptionName** field.</span></span>  <span data-ttu-id="61d69-152">Este parâmetro só de Olá necessárias para o runbook Olá é.</span><span class="sxs-lookup"><span data-stu-id="61d69-152">This is hello only parameter that's required for hello runbook.</span></span>  <span data-ttu-id="61d69-153">Quando tiver terminado, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="61d69-153">When you're finished, click **OK**.</span></span>

<span data-ttu-id="61d69-154">agendamento do runbook Olá deve ter o seguinte aspeto Olá seguinte quando estiver concluída:</span><span class="sxs-lookup"><span data-stu-id="61d69-154">hello runbook schedule should look like hello following when it's completed:</span></span>

![Runbook de teste ResourceSchedule configurado](./media/automation-scenario-start-stop-vm-wjson-tags/automation-schedule-config.png)<br>

## <a name="format-hello-json-string"></a><span data-ttu-id="61d69-156">Olá formato cadeia JSON</span><span class="sxs-lookup"><span data-stu-id="61d69-156">Format hello JSON string</span></span>
<span data-ttu-id="61d69-157">Esta solução basicamente demora um JSON da cadeia de formato especificado e adiciona-o como valor de Olá para uma tag denominada agenda.</span><span class="sxs-lookup"><span data-stu-id="61d69-157">This solution basically takes a JSON string with a specified format and adds it as hello value for a tag called Schedule.</span></span> <span data-ttu-id="61d69-158">Em seguida, um runbook apresenta uma lista de todos os grupos de recursos e máquinas virtuais e identifica as agendas de Olá para cada máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="61d69-158">Then a runbook lists all resource groups and virtual machines and identifies hello schedules for each virtual machine.</span></span>

<span data-ttu-id="61d69-159">runbook Olá repete sobre Olá as máquinas virtuais que têm agendas ligadas e verifica que ações deverão ser executadas.</span><span class="sxs-lookup"><span data-stu-id="61d69-159">hello runbook loops over hello virtual machines that have schedules attached and checks what actions should be taken.</span></span> <span data-ttu-id="61d69-160">Olá segue-se um exemplo de como soluções de Olá devem ter o formato:</span><span class="sxs-lookup"><span data-stu-id="61d69-160">hello following is an example of how hello solutions should be formatted:</span></span>

```json
{
    "TzId": "Eastern Standard Time",
    "0": {
        "S": "11",
        "E": "17"
    },
    "1": {
        "S": "9",
        "E": "19"
    },
    "2": {
        "S": "9",
        "E": "19"
    },
}
```

<span data-ttu-id="61d69-161">Eis algumas informações detalhadas sobre esta estrutura:</span><span class="sxs-lookup"><span data-stu-id="61d69-161">Here is some detailed information about this structure:</span></span>

1. <span data-ttu-id="61d69-162">formato de Olá desta estrutura JSON é otimizada toowork à volta de limitação de 256 carateres de Olá de um valor de etiqueta única no Azure.</span><span class="sxs-lookup"><span data-stu-id="61d69-162">hello format of this JSON structure is optimized toowork around hello 256-character limitation of a single tag value in Azure.</span></span>
2. <span data-ttu-id="61d69-163">*TzId* representa Olá fuso horário da máquina virtual de Olá.</span><span class="sxs-lookup"><span data-stu-id="61d69-163">*TzId* represents hello time zone of hello virtual machine.</span></span> <span data-ttu-id="61d69-164">Este ID pode ser obtido utilizando a classe de TimeZoneInfo .NET Olá numa sessão de PowerShell –**[System.TimeZoneInfo]:: GetSystemTimeZones()**.</span><span class="sxs-lookup"><span data-stu-id="61d69-164">This ID can be obtained by using hello TimeZoneInfo .NET class in a PowerShell session--**[System.TimeZoneInfo]::GetSystemTimeZones()**.</span></span>

   ![GetSystemTimeZones no PowerShell](./media/automation-scenario-start-stop-vm-wjson-tags/automation-get-timzone-powershell.png)

   * <span data-ttu-id="61d69-166">Dias da semana são representados com um valor numérico de zero toosix.</span><span class="sxs-lookup"><span data-stu-id="61d69-166">Weekdays are represented with a numeric value of zero toosix.</span></span> <span data-ttu-id="61d69-167">o valor de Olá zero é igual a Domingo.</span><span class="sxs-lookup"><span data-stu-id="61d69-167">hello value zero equals Sunday.</span></span>
   * <span data-ttu-id="61d69-168">Olá hora de início é representada com Olá **S** atributo e o respetivo valor é um formato de 24 horas.</span><span class="sxs-lookup"><span data-stu-id="61d69-168">hello start time is represented with hello **S** attribute, and its value is in a 24-hour format.</span></span>
   * <span data-ttu-id="61d69-169">Olá hora de fim ou de encerramento é representada com Olá **i** atributo e o respetivo valor é um formato de 24 horas.</span><span class="sxs-lookup"><span data-stu-id="61d69-169">hello end or shutdown time is represented with hello **E** attribute, and its value is in a 24-hour format.</span></span>

     <span data-ttu-id="61d69-170">Se hello **S** e **i** atributos cada terem um valor de zero (0), a máquina virtual de Olá irá ser deixada no estado presente momento Olá da avaliação.</span><span class="sxs-lookup"><span data-stu-id="61d69-170">If hello **S** and **E** attributes each have a value of zero (0), hello virtual machine will be left in its present state at hello time of evaluation.</span></span>
3. <span data-ttu-id="61d69-171">Se quiser tooskip avaliação durante um dia da semana de Olá específico, não adicione uma secção para esse dia da semana de Olá.</span><span class="sxs-lookup"><span data-stu-id="61d69-171">If you want tooskip evaluation for a specific day of hello week, don’t add a section for that day of hello week.</span></span> <span data-ttu-id="61d69-172">Olá seguinte o exemplo, apenas a segunda é avaliada e hello outros dias da semana de Olá são ignorados:</span><span class="sxs-lookup"><span data-stu-id="61d69-172">In hello following example, only Monday is evaluated, and hello other days of hello week are ignored:</span></span>

    ```json
    {
        "TzId": "Eastern Standard Time",
        "1": {
            "S": "11",
            "E": "17"
        }
    }
    ```

## <a name="tag-resource-groups-or-vms"></a><span data-ttu-id="61d69-173">Grupos de recursos de etiqueta ou VMs</span><span class="sxs-lookup"><span data-stu-id="61d69-173">Tag resource groups or VMs</span></span>
<span data-ttu-id="61d69-174">tooshut baixo VMs, terá de tootag Olá VMs ou grupos de recursos de Olá no qual está localizados.</span><span class="sxs-lookup"><span data-stu-id="61d69-174">tooshut down VMs, you need tootag either hello VMs or hello resource groups in which they're located.</span></span> <span data-ttu-id="61d69-175">Máquinas virtuais que não tenham uma etiqueta de agenda não são avaliadas.</span><span class="sxs-lookup"><span data-stu-id="61d69-175">Virtual machines that don't have a Schedule tag are not evaluated.</span></span> <span data-ttu-id="61d69-176">Por conseguinte, não são iniciadas ou encerrados.</span><span class="sxs-lookup"><span data-stu-id="61d69-176">Therefore, they aren't started or shut down.</span></span>

<span data-ttu-id="61d69-177">Existem dois grupos de recursos de tootag formas ou VMs com esta solução.</span><span class="sxs-lookup"><span data-stu-id="61d69-177">There are two ways tootag resource groups or VMs with this solution.</span></span> <span data-ttu-id="61d69-178">Pode fazê-lo diretamente a partir do portal de Olá.</span><span class="sxs-lookup"><span data-stu-id="61d69-178">You can do it directly from hello portal.</span></span> <span data-ttu-id="61d69-179">Ou pode utilizar Olá adicionar ResourceSchedule, ResourceSchedule de atualização e remova ResourceSchedule runbooks.</span><span class="sxs-lookup"><span data-stu-id="61d69-179">Or you can use hello Add-ResourceSchedule, Update-ResourceSchedule, and Remove-ResourceSchedule runbooks.</span></span>

### <a name="tag-through-hello-portal"></a><span data-ttu-id="61d69-180">Etiqueta através do portal Olá</span><span class="sxs-lookup"><span data-stu-id="61d69-180">Tag through hello portal</span></span>
<span data-ttu-id="61d69-181">Siga estes passos tootag uma máquina virtual ou grupo de recursos no portal de Olá:</span><span class="sxs-lookup"><span data-stu-id="61d69-181">Follow these steps tootag a virtual machine or resource group in hello portal:</span></span>

1. <span data-ttu-id="61d69-182">Aplanar cadeia JSON de Olá e certifique-se de que não sabemos de quaisquer espaços.</span><span class="sxs-lookup"><span data-stu-id="61d69-182">Flatten hello JSON string and verify that there aren't any spaces.</span></span>  <span data-ttu-id="61d69-183">A cadeia JSON deve ter o seguinte aspeto:</span><span class="sxs-lookup"><span data-stu-id="61d69-183">Your JSON string should look like this:</span></span>

    ```json
    {"TzId":"Eastern Standard Time","0":{"S":"11","E":"17"},"1":{"S":"9","E":"19"},"2": {"S":"9","E":"19"},"3":{"S":"9","E":"19"},"4":{"S":"9","E":"19"},"5":{"S":"9","E":"19"},"6":{"S":"11","E":"17"}}
    ```

2. <span data-ttu-id="61d69-184">Selecione Olá **Tag** ícone para uma VM ou recurso grupo tooapply esta agenda.</span><span class="sxs-lookup"><span data-stu-id="61d69-184">Select hello **Tag** icon for a VM or resource group tooapply this schedule.</span></span>

   ![Opção de etiqueta VM](./media/automation-scenario-start-stop-vm-wjson-tags/automation-vm-tag-option.png)

3. <span data-ttu-id="61d69-186">As etiquetas são definidas seguir um par chave/valor.</span><span class="sxs-lookup"><span data-stu-id="61d69-186">Tags are defined following a key/value pair.</span></span> <span data-ttu-id="61d69-187">Tipo **agenda** no Olá **chave** campo e, em seguida, cole cadeia JSON de Olá Olá **valor** campo.</span><span class="sxs-lookup"><span data-stu-id="61d69-187">Type **Schedule** in hello **Key** field, and then paste hello JSON string into hello **Value** field.</span></span> <span data-ttu-id="61d69-188">Clique em **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="61d69-188">Click **Save**.</span></span> <span data-ttu-id="61d69-189">A nova etiqueta deverá agora aparecer na lista de Olá de etiquetas para o seu recurso.</span><span class="sxs-lookup"><span data-stu-id="61d69-189">Your new tag should now appear in hello list of tags for your resource.</span></span>

   ![Etiqueta de agenda VM](./media/automation-scenario-start-stop-vm-wjson-tags/automation-vm-schedule-tag.png)

### <a name="tag-from-powershell"></a><span data-ttu-id="61d69-191">Etiqueta do PowerShell</span><span class="sxs-lookup"><span data-stu-id="61d69-191">Tag from PowerShell</span></span>
<span data-ttu-id="61d69-192">Todos os runbooks importados contêm informações de ajuda no início de Olá do script de Olá que descreve como tooexecute Olá runbooks diretamente a partir do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="61d69-192">All imported runbooks contain help information at hello beginning of hello script that describes how tooexecute hello runbooks directly from PowerShell.</span></span> <span data-ttu-id="61d69-193">Pode chamar Olá adicionar ScheduleResource e atualização ScheduleResource runbooks a partir do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="61d69-193">You can call hello Add-ScheduleResource and Update-ScheduleResource runbooks from PowerShell.</span></span> <span data-ttu-id="61d69-194">Fazê-lo através da transmissão de parâmetros necessários, que lhe permitem toocreate ou atualização Olá agenda uma tag num VM ou grupo de recursos fora do portal de Olá.</span><span class="sxs-lookup"><span data-stu-id="61d69-194">You do this by passing required parameters that enable you toocreate or update hello Schedule tag on a VM or resource group outside of hello portal.</span></span>

<span data-ttu-id="61d69-195">toocreate, adicionar e eliminar etiquetas através do PowerShell, terá primeiro demasiado[configurar o ambiente de PowerShell para o Azure](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="61d69-195">toocreate, add, and delete tags through PowerShell, you first need too[set up your PowerShell environment for Azure](/powershell/azure/overview).</span></span> <span data-ttu-id="61d69-196">Depois de concluir a configuração de Olá, pode avançar com Olá os seguintes passos.</span><span class="sxs-lookup"><span data-stu-id="61d69-196">After you complete hello setup, you can proceed with hello following steps.</span></span>

### <a name="create-a-schedule-tag-with-powershell"></a><span data-ttu-id="61d69-197">Criar uma etiqueta de agenda com o PowerShell</span><span class="sxs-lookup"><span data-stu-id="61d69-197">Create a schedule tag with PowerShell</span></span>
1. <span data-ttu-id="61d69-198">Abra uma sessão do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="61d69-198">Open a PowerShell session.</span></span> <span data-ttu-id="61d69-199">Em seguida, utilize Olá tooauthenticate de exemplo com a conta Run As e toospecify uma subscrição a seguir:</span><span class="sxs-lookup"><span data-stu-id="61d69-199">Then use hello following example tooauthenticate with your Run As account and toospecify a subscription:</span></span>

    ```powershell
    $Conn = Get-AutomationConnection -Name AzureRunAsConnection
    Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID `
    -ApplicationId $Conn.ApplicationID -CertificateThumbprint $Conn.CertificateThumbprint
    Select-AzureRmSubscription -SubscriptionName "MySubscription"
    ```

2. <span data-ttu-id="61d69-200">Defina uma tabela hash de agenda.</span><span class="sxs-lookup"><span data-stu-id="61d69-200">Define a schedule hash table.</span></span> <span data-ttu-id="61d69-201">Eis um exemplo de como deve ser construído:</span><span class="sxs-lookup"><span data-stu-id="61d69-201">Here is an example of how it should be constructed:</span></span>

    ```powershell
    $schedule= @{ "TzId"="Eastern Standard Time"; "0"= @{"S"="11";"E"="17"};"1"= @{"S"="9";"E"="19"};"2"= @{"S"="9";"E"="19"};"3"= @{"S"="9";"E"="19"};"4"= @{"S"="9";"E"="19"};"5"= @{"S"="9";"E"="19"};"6"= @{"S"="11";"E"="17"}}
    ```

3. <span data-ttu-id="61d69-202">Defina os parâmetros de Olá que são necessários pelo runbook Olá.</span><span class="sxs-lookup"><span data-stu-id="61d69-202">Define hello parameters that are required by hello runbook.</span></span> <span data-ttu-id="61d69-203">No seguinte exemplo de Olá, iremos como objetivo uma VM:</span><span class="sxs-lookup"><span data-stu-id="61d69-203">In hello following example, we are targeting a VM:</span></span>

    ```powershell
    $params = @{"SubscriptionName"="MySubscription";"ResourceGroupName"="ResourceGroup01"; "VmName"="VM01";"Schedule"=$schedule}
    ```

    <span data-ttu-id="61d69-204">Se estiver a etiquetagem um grupo de recursos, remova Olá *VMName* parâmetro de hash de Olá $params tabela da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="61d69-204">If you’re tagging a resource group, remove hello *VMName* parameter from hello $params hash table as follows:</span></span>

    ```powershell
    $params = @{"SubscriptionName"="MySubscription";"ResourceGroupName"="ResourceGroup01"; "Schedule"=$schedule}
    ```

4. <span data-ttu-id="61d69-205">Execute Olá ResourceSchedule adicionar runbook com Olá tag de agenda parâmetros toocreate Olá os seguintes:</span><span class="sxs-lookup"><span data-stu-id="61d69-205">Run hello Add-ResourceSchedule runbook with hello following parameters toocreate hello Schedule tag:</span></span>

    ```powershell
    Start-AzureRmAutomationRunbook -Name "Add-ResourceSchedule" -Parameters $params `
    -AutomationAccountName "AutomationAccount" -ResourceGroupName "ResourceGroup01"
    ```

5. <span data-ttu-id="61d69-206">tooupdate uma etiqueta de máquina virtual ou grupo de recursos, executar Olá **atualização ResourceSchedule** runbook com Olá os seguintes parâmetros:</span><span class="sxs-lookup"><span data-stu-id="61d69-206">tooupdate a resource group or virtual machine tag, execute hello **Update-ResourceSchedule** runbook with hello following parameters:</span></span>

    ```powershell
    Start-AzureRmAutomationRunbook -Name "Update-ResourceSchedule" -Parameters $params `
    -AutomationAccountName "AutomationAccount" -ResourceGroupName "ResourceGroup01"
    ```

### <a name="remove-a-schedule-tag-with-powershell"></a><span data-ttu-id="61d69-207">Remover uma etiqueta de agenda com o PowerShell</span><span class="sxs-lookup"><span data-stu-id="61d69-207">Remove a schedule tag with PowerShell</span></span>
1. <span data-ttu-id="61d69-208">Abra uma sessão do PowerShell e execute Olá seguir tooauthenticate com a conta Run As e tooselect e especifique uma subscrição:</span><span class="sxs-lookup"><span data-stu-id="61d69-208">Open a PowerShell session and run hello following tooauthenticate with your Run As account and tooselect and specify a subscription:</span></span>

    ```powershell
    Conn = Get-AutomationConnection -Name AzureRunAsConnection
    Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID `
    -ApplicationId $Conn.ApplicationID -CertificateThumbprint $Conn.CertificateThumbprint
    Select-AzureRmSubscription -SubscriptionName "MySubscription"
    ```

2. <span data-ttu-id="61d69-209">Defina os parâmetros de Olá que são necessários pelo runbook Olá.</span><span class="sxs-lookup"><span data-stu-id="61d69-209">Define hello parameters that are required by hello runbook.</span></span> <span data-ttu-id="61d69-210">No seguinte exemplo de Olá, iremos como objetivo uma VM:</span><span class="sxs-lookup"><span data-stu-id="61d69-210">In hello following example, we are targeting a VM:</span></span>

    ```powershell
    $params = @{"SubscriptionName"="MySubscription";"ResourceGroupName"="ResourceGroup01";"VmName"="VM01"}
    ```

    <span data-ttu-id="61d69-211">Se estiver a remover uma etiqueta de um grupo de recursos, remova Olá *VMName* parâmetro de hash de Olá $params tabela da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="61d69-211">If you’re removing a tag from a resource group, remove hello *VMName* parameter from hello $params hash table as follows:</span></span>

    ```powershell
    $params = @{"SubscriptionName"="MySubscription";"ResourceGroupName"="ResourceGroup01"}
    ```

3. <span data-ttu-id="61d69-212">Execute a tag de agenda de Olá runbook tooremove Olá ResourceSchedule remover:</span><span class="sxs-lookup"><span data-stu-id="61d69-212">Execute hello Remove-ResourceSchedule runbook tooremove hello Schedule tag:</span></span>

    ```powershell
    Start-AzureRmAutomationRunbook -Name "Remove-ResourceSchedule" -Parameters $params `
    -AutomationAccountName "AutomationAccount" -ResourceGroupName "ResourceGroup01"
    ```

4. <span data-ttu-id="61d69-213">tooupdate uma etiqueta de máquina virtual ou grupo de recursos, executar o runbook de Olá remover ResourceSchedule com Olá os seguintes parâmetros:</span><span class="sxs-lookup"><span data-stu-id="61d69-213">tooupdate a resource group or virtual machine tag, execute hello Remove-ResourceSchedule runbook with hello following parameters:</span></span>

    ```powershell
    Start-AzureRmAutomationRunbook -Name "Remove-ResourceSchedule" -Parameters $params `
    -AutomationAccountName "AutomationAccount" -ResourceGroupName "ResourceGroup01"
    ```

> [!NOTE]
> <span data-ttu-id="61d69-214">É recomendável que monitorizar proativamente estes runbooks (e Estados da máquina virtual Olá) tooverify que as máquinas virtuais estão a ser encerrado e iniciado em conformidade.</span><span class="sxs-lookup"><span data-stu-id="61d69-214">We recommend that you proactively monitor these runbooks (and hello virtual machine states) tooverify that your virtual machines are being shut down and started accordingly.</span></span>
>

<span data-ttu-id="61d69-215">detalhes de Olá tooview de runbook Olá ResourceSchedule de teste da tarefa no Olá portal do Azure, selecione de Olá **tarefas** mosaico de Olá runbook.</span><span class="sxs-lookup"><span data-stu-id="61d69-215">tooview hello details of hello Test-ResourceSchedule runbook job in hello Azure portal, select hello **Jobs** tile of hello runbook.</span></span> <span data-ttu-id="61d69-216">Olá tarefa apresenta resumo Olá os parâmetros de entrada e saída de Olá transmitido em fluxo, além disso toogeneral informações sobre a tarefa de Olá e quaisquer exceções, caso ocorram.</span><span class="sxs-lookup"><span data-stu-id="61d69-216">hello job summary displays hello input parameters and hello output stream, in addition toogeneral information about hello job and any exceptions if they occurred.</span></span>

<span data-ttu-id="61d69-217">Olá **resumo da tarefa** inclui as mensagens de fluxos de saída, aviso e erro Olá.</span><span class="sxs-lookup"><span data-stu-id="61d69-217">hello **Job Summary** includes messages from hello output, warning, and error streams.</span></span> <span data-ttu-id="61d69-218">Selecione Olá **saída** mosaico tooview resultados da execução do runbook Olá detalhados.</span><span class="sxs-lookup"><span data-stu-id="61d69-218">Select hello **Output** tile tooview detailed results from hello runbook execution.</span></span>

![Resultado do teste ResourceSchedule](./media/automation-scenario-start-stop-vm-wjson-tags/automation-job-output.png)

## <a name="next-steps"></a><span data-ttu-id="61d69-220">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="61d69-220">Next steps</span></span>
* <span data-ttu-id="61d69-221">tooget iniciado com runbooks do fluxo de trabalho do PowerShell, consulte [o meu primeiro runbook do fluxo de trabalho do PowerShell](automation-first-runbook-textual.md).</span><span class="sxs-lookup"><span data-stu-id="61d69-221">tooget started with PowerShell workflow runbooks, see [My first PowerShell workflow runbook](automation-first-runbook-textual.md).</span></span>
* <span data-ttu-id="61d69-222">toolearn mais informações sobre tipos de runbook e as vantagens e limitações, consulte [tipos de runbook da automatização do Azure](automation-runbook-types.md).</span><span class="sxs-lookup"><span data-stu-id="61d69-222">toolearn more about runbook types, and their advantages and limitations, see [Azure Automation runbook types](automation-runbook-types.md).</span></span>
* <span data-ttu-id="61d69-223">Para obter mais informações sobre as funcionalidades de suporte de script do PowerShell, consulte [suporte de script de PowerShell nativo na automatização do Azure](https://azure.microsoft.com/blog/announcing-powershell-script-support-azure-automation-2/).</span><span class="sxs-lookup"><span data-stu-id="61d69-223">For more information about PowerShell script support features, see [Native PowerShell script support in Azure Automation](https://azure.microsoft.com/blog/announcing-powershell-script-support-azure-automation-2/).</span></span>
* <span data-ttu-id="61d69-224">toolearn mais informações sobre o registo do runbook e de saída, consulte [Runbook resultados e mensagens na automatização do Azure](automation-runbook-output-and-messages.md).</span><span class="sxs-lookup"><span data-stu-id="61d69-224">toolearn more about runbook logging and output, see [Runbook output and messages in Azure Automation](automation-runbook-output-and-messages.md).</span></span>
* <span data-ttu-id="61d69-225">mais informações sobre uma conta Run As do Azure e como tooauthenticate os runbooks ao utilizá-lo, consulte o artigo toolearn [autenticar runbooks com a conta Run As do Azure](automation-sec-configure-azure-runas-account.md).</span><span class="sxs-lookup"><span data-stu-id="61d69-225">toolearn more about an Azure Run As account and how tooauthenticate your runbooks by using it, see [Authenticate runbooks with Azure Run As account](automation-sec-configure-azure-runas-account.md).</span></span>
