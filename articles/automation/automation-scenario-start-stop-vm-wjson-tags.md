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
# <a name="azure-automation-scenario-using-json-formatted-tags-toocreate-a-schedule-for-azure-vm-startup-and-shutdown"></a>Cenário de automatização do Azure: utilizar a formatados em JSON etiquetas toocreate uma agenda para a VM do Azure de arranque e encerramento
Os clientes pretendem, muitas vezes, o arranque de Olá tooschedule e encerramento de máquinas virtuais toohelp reduzir os custos de subscrição ou empresariais e requisitos técnicos de suporte.

Olá seguinte cenário permite-lhe tooset cópias de segurança automatizada de arranque e encerramento das suas VMs através da utilização de uma tag denominada agenda a um nível de máquina virtual no Azure ou ao nível do grupo de recursos. Este agendamento pode ser configurado de Domingo tooSaturday com um tempo de arranque e o tempo de encerramento.

Temos algumas opções de out of box. Estas incluem:

* [Conjuntos de dimensionamento de máquina virtual](../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md) com definições de dimensionamento automático que lhe permitem tooscale entrada ou saída.
* [DevTest Labs](../devtest-lab/devtest-lab-overview.md) serviço, que tem Olá capacidade incorporada do agendamento de arranque e encerramento operações.

No entanto, estas opções só suportam cenários específicos e não pode ser aplicado tooinfrastructure-como-um-serviço (IaaS) VMs.

Quando Olá tag da agenda é aplicado tooa grupo de recursos, também é aplicado tooall máquinas de virtuais dentro desse grupo de recursos. Se uma agenda também é diretamente aplicado tooa VM, agenda último Olá prevalece no Olá seguinte ordem:

1. Grupo de recursos de tooa aplicados agenda
2. Agendar o grupo de recursos de tooa aplicadas e a máquina virtual no grupo de recursos de Olá
3. Agendar a máquina virtual de tooa aplicados

Neste cenário, essencialmente, demora uma cadeia JSON com formato especificado e adiciona-o como valor de Olá para uma tag denominada agenda. Em seguida, um runbook apresenta uma lista de todos os grupos de recursos e máquinas virtuais e identifica as agendas de Olá para cada VM com base em cenários de Olá listados anteriormente. Em seguida repetido ao longo Olá VMs que têm agendas ligadas e avalia que deverão ser executadas. Por exemplo, determina quais as VMs necessitar toobe parar, encerrar ou ignoradas.

Estes runbooks autenticar utilizando Olá [conta Run As do Azure](automation-sec-configure-azure-runas-account.md).

## <a name="download-hello-runbooks-for-hello-scenario"></a>Transferir runbooks Olá para o cenário de Olá
Este cenário consiste em quatro runbooks do fluxo de trabalho do PowerShell que pode transferir da Olá [TechNet Gallery](https://gallery.technet.microsoft.com/Azure-Automation-Runbooks-84f0efc7) ou Olá [GitHub](https://github.com/paulomarquesdacosta/azure-automation-scheduled-shutdown-and-startup) repositório para este projeto.

| Runbook | Descrição |
| --- | --- |
| Teste ResourceSchedule |Verifica cada agenda de máquina virtual e efetua o encerramento ou de arranque, consoante a agenda de Olá. |
| ResourceSchedule adicionar |Adiciona Olá agenda tag tooa VM ou grupo de recursos. |
| Atualização ResourceSchedule |Modifica a tag de agenda existente Olá, substituindo-lo com um novo. |
| Remover ResourceSchedule |Remove a tag de agenda Olá de um VM ou grupo de recursos. |

## <a name="install-and-configure-this-scenario"></a>Instalar e configurar este cenário
### <a name="install-and-publish-hello-runbooks"></a>Instalar e publicar runbooks Olá
Depois de transferir runbooks Olá, pode importá-los utilizando o procedimento Olá [criar ou importar um runbook na automatização do Azure](automation-creating-importing-runbook.md#importing-a-runbook-from-a-file-into-azure-automation).  Publica cada runbook após tem foi importada com êxito na sua conta de automatização.

### <a name="add-a-schedule-toohello-test-resourceschedule-runbook"></a>Adicionar um runbook de toohello ResourceSchedule de teste de agenda
Siga estes passos tooenable Olá agenda Olá teste ResourceSchedule runbook. Esta é Olá runbook que verifica a máquinas virtuais que deverão ser iniciadas, encerrar ou à esquerda é.

1. Olá portal do Azure, abra a sua conta de automatização e, em seguida, clique em Olá **Runbooks** mosaico.
2. No Olá **teste ResourceSchedule** painel, clique em Olá **agendas** mosaico.
3. No Olá **agendas** painel, clique em **adicionar uma agenda**.
4. No Olá **agendas** painel, selecione **ligar um runbook de tooyour agenda**. Em seguida, selecione **criar uma nova agenda**.
5. No Olá **nova agenda** painel, escreva o nome de Olá desta agenda, por exemplo: *HourlyExecution*.
6. Para a agenda de Olá **iniciar**, defina o incremento de hora do Olá início tempo tooan.
7. Selecione **periodicidade**e, em seguida, para **repetir a cada intervalo**, selecione **1 hora**.
8. Certifique-se de que **definir expiração** estiver definido demasiado**não**e, em seguida, clique em **criar** toosave a agenda de novo.
9. No Olá **agenda Runbook** painel de opções, selecione **parâmetros e definições de execução**. No Olá teste ResourceSchedule **parâmetros** painel, introduza o nome de Olá da sua subscrição no Olá **SubscriptionName** campo.  Este parâmetro só de Olá necessárias para o runbook Olá é.  Quando tiver terminado, clique em **OK**.

agendamento do runbook Olá deve ter o seguinte aspeto Olá seguinte quando estiver concluída:

![Runbook de teste ResourceSchedule configurado](./media/automation-scenario-start-stop-vm-wjson-tags/automation-schedule-config.png)<br>

## <a name="format-hello-json-string"></a>Olá formato cadeia JSON
Esta solução basicamente demora um JSON da cadeia de formato especificado e adiciona-o como valor de Olá para uma tag denominada agenda. Em seguida, um runbook apresenta uma lista de todos os grupos de recursos e máquinas virtuais e identifica as agendas de Olá para cada máquina virtual.

runbook Olá repete sobre Olá as máquinas virtuais que têm agendas ligadas e verifica que ações deverão ser executadas. Olá segue-se um exemplo de como soluções de Olá devem ter o formato:

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

Eis algumas informações detalhadas sobre esta estrutura:

1. formato de Olá desta estrutura JSON é otimizada toowork à volta de limitação de 256 carateres de Olá de um valor de etiqueta única no Azure.
2. *TzId* representa Olá fuso horário da máquina virtual de Olá. Este ID pode ser obtido utilizando a classe de TimeZoneInfo .NET Olá numa sessão de PowerShell –**[System.TimeZoneInfo]:: GetSystemTimeZones()**.

   ![GetSystemTimeZones no PowerShell](./media/automation-scenario-start-stop-vm-wjson-tags/automation-get-timzone-powershell.png)

   * Dias da semana são representados com um valor numérico de zero toosix. o valor de Olá zero é igual a Domingo.
   * Olá hora de início é representada com Olá **S** atributo e o respetivo valor é um formato de 24 horas.
   * Olá hora de fim ou de encerramento é representada com Olá **i** atributo e o respetivo valor é um formato de 24 horas.

     Se hello **S** e **i** atributos cada terem um valor de zero (0), a máquina virtual de Olá irá ser deixada no estado presente momento Olá da avaliação.
3. Se quiser tooskip avaliação durante um dia da semana de Olá específico, não adicione uma secção para esse dia da semana de Olá. Olá seguinte o exemplo, apenas a segunda é avaliada e hello outros dias da semana de Olá são ignorados:

    ```json
    {
        "TzId": "Eastern Standard Time",
        "1": {
            "S": "11",
            "E": "17"
        }
    }
    ```

## <a name="tag-resource-groups-or-vms"></a>Grupos de recursos de etiqueta ou VMs
tooshut baixo VMs, terá de tootag Olá VMs ou grupos de recursos de Olá no qual está localizados. Máquinas virtuais que não tenham uma etiqueta de agenda não são avaliadas. Por conseguinte, não são iniciadas ou encerrados.

Existem dois grupos de recursos de tootag formas ou VMs com esta solução. Pode fazê-lo diretamente a partir do portal de Olá. Ou pode utilizar Olá adicionar ResourceSchedule, ResourceSchedule de atualização e remova ResourceSchedule runbooks.

### <a name="tag-through-hello-portal"></a>Etiqueta através do portal Olá
Siga estes passos tootag uma máquina virtual ou grupo de recursos no portal de Olá:

1. Aplanar cadeia JSON de Olá e certifique-se de que não sabemos de quaisquer espaços.  A cadeia JSON deve ter o seguinte aspeto:

    ```json
    {"TzId":"Eastern Standard Time","0":{"S":"11","E":"17"},"1":{"S":"9","E":"19"},"2": {"S":"9","E":"19"},"3":{"S":"9","E":"19"},"4":{"S":"9","E":"19"},"5":{"S":"9","E":"19"},"6":{"S":"11","E":"17"}}
    ```

2. Selecione Olá **Tag** ícone para uma VM ou recurso grupo tooapply esta agenda.

   ![Opção de etiqueta VM](./media/automation-scenario-start-stop-vm-wjson-tags/automation-vm-tag-option.png)

3. As etiquetas são definidas seguir um par chave/valor. Tipo **agenda** no Olá **chave** campo e, em seguida, cole cadeia JSON de Olá Olá **valor** campo. Clique em **Guardar**. A nova etiqueta deverá agora aparecer na lista de Olá de etiquetas para o seu recurso.

   ![Etiqueta de agenda VM](./media/automation-scenario-start-stop-vm-wjson-tags/automation-vm-schedule-tag.png)

### <a name="tag-from-powershell"></a>Etiqueta do PowerShell
Todos os runbooks importados contêm informações de ajuda no início de Olá do script de Olá que descreve como tooexecute Olá runbooks diretamente a partir do PowerShell. Pode chamar Olá adicionar ScheduleResource e atualização ScheduleResource runbooks a partir do PowerShell. Fazê-lo através da transmissão de parâmetros necessários, que lhe permitem toocreate ou atualização Olá agenda uma tag num VM ou grupo de recursos fora do portal de Olá.

toocreate, adicionar e eliminar etiquetas através do PowerShell, terá primeiro demasiado[configurar o ambiente de PowerShell para o Azure](/powershell/azure/overview). Depois de concluir a configuração de Olá, pode avançar com Olá os seguintes passos.

### <a name="create-a-schedule-tag-with-powershell"></a>Criar uma etiqueta de agenda com o PowerShell
1. Abra uma sessão do PowerShell. Em seguida, utilize Olá tooauthenticate de exemplo com a conta Run As e toospecify uma subscrição a seguir:

    ```powershell
    $Conn = Get-AutomationConnection -Name AzureRunAsConnection
    Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID `
    -ApplicationId $Conn.ApplicationID -CertificateThumbprint $Conn.CertificateThumbprint
    Select-AzureRmSubscription -SubscriptionName "MySubscription"
    ```

2. Defina uma tabela hash de agenda. Eis um exemplo de como deve ser construído:

    ```powershell
    $schedule= @{ "TzId"="Eastern Standard Time"; "0"= @{"S"="11";"E"="17"};"1"= @{"S"="9";"E"="19"};"2"= @{"S"="9";"E"="19"};"3"= @{"S"="9";"E"="19"};"4"= @{"S"="9";"E"="19"};"5"= @{"S"="9";"E"="19"};"6"= @{"S"="11";"E"="17"}}
    ```

3. Defina os parâmetros de Olá que são necessários pelo runbook Olá. No seguinte exemplo de Olá, iremos como objetivo uma VM:

    ```powershell
    $params = @{"SubscriptionName"="MySubscription";"ResourceGroupName"="ResourceGroup01"; "VmName"="VM01";"Schedule"=$schedule}
    ```

    Se estiver a etiquetagem um grupo de recursos, remova Olá *VMName* parâmetro de hash de Olá $params tabela da seguinte forma:

    ```powershell
    $params = @{"SubscriptionName"="MySubscription";"ResourceGroupName"="ResourceGroup01"; "Schedule"=$schedule}
    ```

4. Execute Olá ResourceSchedule adicionar runbook com Olá tag de agenda parâmetros toocreate Olá os seguintes:

    ```powershell
    Start-AzureRmAutomationRunbook -Name "Add-ResourceSchedule" -Parameters $params `
    -AutomationAccountName "AutomationAccount" -ResourceGroupName "ResourceGroup01"
    ```

5. tooupdate uma etiqueta de máquina virtual ou grupo de recursos, executar Olá **atualização ResourceSchedule** runbook com Olá os seguintes parâmetros:

    ```powershell
    Start-AzureRmAutomationRunbook -Name "Update-ResourceSchedule" -Parameters $params `
    -AutomationAccountName "AutomationAccount" -ResourceGroupName "ResourceGroup01"
    ```

### <a name="remove-a-schedule-tag-with-powershell"></a>Remover uma etiqueta de agenda com o PowerShell
1. Abra uma sessão do PowerShell e execute Olá seguir tooauthenticate com a conta Run As e tooselect e especifique uma subscrição:

    ```powershell
    Conn = Get-AutomationConnection -Name AzureRunAsConnection
    Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID `
    -ApplicationId $Conn.ApplicationID -CertificateThumbprint $Conn.CertificateThumbprint
    Select-AzureRmSubscription -SubscriptionName "MySubscription"
    ```

2. Defina os parâmetros de Olá que são necessários pelo runbook Olá. No seguinte exemplo de Olá, iremos como objetivo uma VM:

    ```powershell
    $params = @{"SubscriptionName"="MySubscription";"ResourceGroupName"="ResourceGroup01";"VmName"="VM01"}
    ```

    Se estiver a remover uma etiqueta de um grupo de recursos, remova Olá *VMName* parâmetro de hash de Olá $params tabela da seguinte forma:

    ```powershell
    $params = @{"SubscriptionName"="MySubscription";"ResourceGroupName"="ResourceGroup01"}
    ```

3. Execute a tag de agenda de Olá runbook tooremove Olá ResourceSchedule remover:

    ```powershell
    Start-AzureRmAutomationRunbook -Name "Remove-ResourceSchedule" -Parameters $params `
    -AutomationAccountName "AutomationAccount" -ResourceGroupName "ResourceGroup01"
    ```

4. tooupdate uma etiqueta de máquina virtual ou grupo de recursos, executar o runbook de Olá remover ResourceSchedule com Olá os seguintes parâmetros:

    ```powershell
    Start-AzureRmAutomationRunbook -Name "Remove-ResourceSchedule" -Parameters $params `
    -AutomationAccountName "AutomationAccount" -ResourceGroupName "ResourceGroup01"
    ```

> [!NOTE]
> É recomendável que monitorizar proativamente estes runbooks (e Estados da máquina virtual Olá) tooverify que as máquinas virtuais estão a ser encerrado e iniciado em conformidade.
>

detalhes de Olá tooview de runbook Olá ResourceSchedule de teste da tarefa no Olá portal do Azure, selecione de Olá **tarefas** mosaico de Olá runbook. Olá tarefa apresenta resumo Olá os parâmetros de entrada e saída de Olá transmitido em fluxo, além disso toogeneral informações sobre a tarefa de Olá e quaisquer exceções, caso ocorram.

Olá **resumo da tarefa** inclui as mensagens de fluxos de saída, aviso e erro Olá. Selecione Olá **saída** mosaico tooview resultados da execução do runbook Olá detalhados.

![Resultado do teste ResourceSchedule](./media/automation-scenario-start-stop-vm-wjson-tags/automation-job-output.png)

## <a name="next-steps"></a>Passos seguintes
* tooget iniciado com runbooks do fluxo de trabalho do PowerShell, consulte [o meu primeiro runbook do fluxo de trabalho do PowerShell](automation-first-runbook-textual.md).
* toolearn mais informações sobre tipos de runbook e as vantagens e limitações, consulte [tipos de runbook da automatização do Azure](automation-runbook-types.md).
* Para obter mais informações sobre as funcionalidades de suporte de script do PowerShell, consulte [suporte de script de PowerShell nativo na automatização do Azure](https://azure.microsoft.com/blog/announcing-powershell-script-support-azure-automation-2/).
* toolearn mais informações sobre o registo do runbook e de saída, consulte [Runbook resultados e mensagens na automatização do Azure](automation-runbook-output-and-messages.md).
* mais informações sobre uma conta Run As do Azure e como tooauthenticate os runbooks ao utilizá-lo, consulte o artigo toolearn [autenticar runbooks com a conta Run As do Azure](automation-sec-configure-azure-runas-account.md).
