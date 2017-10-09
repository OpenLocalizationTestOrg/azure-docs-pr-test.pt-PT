---
title: "aaaForward tooOMS de dados de tarefa de automatização do Azure Log Analytics | Microsoft Docs"
description: "Este artigo demonstra como a tarefa de runbook e o estado da tarefa toosend fluxos informações adicionais do tooMicrosoft análise de registos do Operations Management Suite toodeliver e gestão."
services: automation
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: tysonn
ms.assetid: c12724c6-01a9-4b55-80ae-d8b7b99bd436
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/02/2017
ms.author: magoedte
ms.openlocfilehash: e78b6c6677d6502711ce828e2d32b7a91922ae26
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="forward-job-status-and-job-streams-from-automation-toolog-analytics-oms"></a>Reencaminhar o estado da tarefa e fluxos de trabalho de automatização tooLog análise (OMS)
Automatização pode enviar runbook tarefa estado e tarefa fluxos tooyour análise de registos do Microsoft Operations Management Suite (OMS) área de trabalho.  Os registos de tarefa e fluxos de trabalho são visíveis no Olá portal do Azure, ou com o PowerShell, para tarefas individuais e Isto permite-lhe as investigações simples de tooperform. Agora com a análise de registos, pode:

* Obter conhecimentos aprofundados sobre as tarefas de automatização
* Acionamento um e-mail ou o alerta com base no seu estado de tarefa de runbook (por exemplo, falha ou suspenso)
* Escrever consultas avançadas nos seus fluxos de trabalho
* Correlacionar tarefas em contas de automatização
* Visualizar o histórico do trabalho ao longo do tempo     

## <a name="prerequisites-and-deployment-considerations"></a>Pré-requisitos e considerações de implementação
toostart enviar a automatização tooLog análise de registos, tem de:

1. Olá Novembro de 2016 ou versão posterior do [Azure PowerShell](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/) (v2.3.0).
2. Uma área de trabalho de análise de registos. Para obter mais informações, consulte [introdução à análise de registos](../log-analytics/log-analytics-get-started.md). 
3. Olá ResourceId para a sua conta de automatização do Azure

toofind Olá ResourceId para a conta de automatização do Azure e a área de trabalho de análise de registos, execute Olá PowerShell os seguintes:

```powershell
# Find hello ResourceId for hello Automation Account
Find-AzureRmResource -ResourceType "Microsoft.Automation/automationAccounts"

# Find hello ResourceId for hello Log Analytics workspace
Find-AzureRmResource -ResourceType "Microsoft.OperationalInsights/workspaces"
```

Se tiver várias contas de automatização ou áreas de trabalho, resultado Olá Olá precedente comandos, localize Olá *nome* precisar tooconfigure e copie o valor de Olá para *ResourceId*.

Se precisar de toofind Olá *nome* da sua conta de automatização na Olá portal do Azure selecione a conta de automatização de Olá **conta de automatização** painel e selecione **todas as definições**.  De Olá **todas as definições** painel, em **as definições da conta** selecione **propriedades**.  No Olá **propriedades** painel, pode ter em atenção estes valores.<br> ![Propriedades da conta de automatização](media/automation-manage-send-joblogs-log-analytics/automation-account-properties.png).

## <a name="set-up-integration-with-log-analytics"></a>Configurar a integração com a análise de registos
1. No seu computador, inicie **do Windows PowerShell** de Olá **iniciar** ecrã.  
2. Copiar e colar Olá seguir o PowerShell e editar o valor de Olá para Olá `$workspaceId` e `$automationAccountId`.  Para Olá `-Environment` parâmetro, os valores válidos são *AzureCloud* ou *AzureUSGovernment* consoante estiver a trabalhar num ambiente de nuvem de Olá.     

```powershell
[cmdletBinding()]
    Param
    (
        [Parameter(Mandatory=$True)]
        [ValidateSet("AzureCloud","AzureUSGovernment")]
        [string]$Environment="AzureCloud"
    )

#Check toosee which cloud environment toosign into.
Switch ($Environment)
   {
       "AzureCloud" {Login-AzureRmAccount}
       "AzureUSGovernment" {Login-AzureRmAccount -EnvironmentName AzureUSGovernment} 
   }

# if you have one Log Analytics workspace you can use hello following command tooget hello resource id of hello workspace
$workspaceId = (Get-AzureRmOperationalInsightsWorkspace).ResourceId

$automationAccountId = "/SUBSCRIPTIONS/ec11ca60-1234-491e-5678-0ea07feae25c/RESOURCEGROUPS/DEMO/PROVIDERS/MICROSOFT.AUTOMATION/ACCOUNTS/DEMO" 

Set-AzureRmDiagnosticSetting -ResourceId $automationAccountId -WorkspaceId $workspaceId -Enabled $true

```

Depois de executar este script, irá ver registos de análise de registos dentro de 10 minutos de novos JobLogs ou JobStreams que está a ser escrito.

toosee Olá os registos, executados Olá seguinte de consulta em pesquisa de registos de análise de registos:`Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION"`

### <a name="verify-configuration"></a>Verifique a configuração
tooconfirm que está a sua conta de automatização enviar registos de área de trabalho de análise de registos de tooyour, verifique que diagnóstico está definido corretamente na conta de automatização de Olá com Olá PowerShell os seguintes:

```powershell
[cmdletBinding()]
    Param
    (
        [Parameter(Mandatory=$True)]
        [ValidateSet("AzureCloud","AzureUSGovernment")]
        [string]$Environment="AzureCloud"
    )

#Check toosee which cloud environment toosign into.
Switch ($Environment)
   {
       "AzureCloud" {Login-AzureRmAccount}
       "AzureUSGovernment" {Login-AzureRmAccount -EnvironmentName AzureUSGovernment} 
   }
# if you have one Log Analytics workspace you can use hello following command tooget hello resource id of hello workspace
$workspaceId = (Get-AzureRmOperationalInsightsWorkspace).ResourceId

$automationAccountId = "/SUBSCRIPTIONS/ec11ca60-1234-491e-5678-0ea07feae25c/RESOURCEGROUPS/DEMO/PROVIDERS/MICROSOFT.AUTOMATION/ACCOUNTS/DEMO" 

Get-AzureRmDiagnosticSetting -ResourceId $automationAccountId
```

Na saída de Olá Certifique-se de que:
+ Em *registos*, Olá valor para *ativado* é *verdadeiro*
+ Olá valor *WorkspaceId* está definido toohello ResourceId da sua área de trabalho de análise de registos


## <a name="log-analytics-records"></a>Registos do Log Analytics
Cria dois tipos de registos de análise de registos de diagnóstico da automatização do Azure e é etiquetado como **tipo = AzureDiagnostics**.

### <a name="job-logs"></a>Registos da tarefa
| Propriedade | Descrição |
| --- | --- |
| TimeGenerated |Data e hora quando executar a tarefa de runbook Olá. |
| RunbookName_s |nome de Olá de Olá runbook. |
| Caller_s |Quem iniciou a operação de Olá.  Os valores possíveis são um endereço de e-mail ou o sistema para trabalhos agendados. |
| Tenant_g | GUID que identifica o inquilino Olá para Olá autor da chamada. |
| JobId_g |GUID que é Olá Id da tarefa de runbook Olá. |
| ResultType |Estado da tarefa de runbook Olá Olá.  Os valores possíveis são:<br>- Iniciado<br>- Parado<br>- Suspenso<br>- Falhado<br>-Concluída |
| Categoria | Classificação do tipo de Olá de dados.  Para automatização, o valor de Olá é JobLogs. |
| OperationName | Especifica o tipo de Olá da operação efetuada no Azure.  Para automatização, o valor de Olá é tarefa. |
| Recurso | Nome da conta de automatização de Olá |
| SourceSystem | Como a análise de registos recolhidos dados de Olá. Sempre *Azure* para diagnóstico do Azure. |
| ResultDescription |Descreve o estado de resultado da tarefa de runbook de Olá.  Os valores possíveis são:<br>- Trabalho iniciado<br>- Trabalho falhado<br>- Trabalho Concluído |
| CorrelationId |GUID que é Olá Id de correlação da tarefa de runbook Olá. |
| ResourceId |Especifica o id do recurso de conta de automatização do Azure do Olá de Olá runbook. |
| SubscriptionId | Olá subscrição do Azure Id (GUID) para Olá conta de automatização. |
| ResourceGroup | Nome do grupo de recursos de Olá para Olá conta de automatização. |
| ResourceProvider | MICROSOFT. AUTOMATIZAÇÃO |
| ResourceType | AUTOMATIONACCOUNTS |


### <a name="job-streams"></a>Fluxos de trabalho
| Propriedade | Descrição |
| --- | --- |
| TimeGenerated |Data e hora quando executar a tarefa de runbook Olá. |
| RunbookName_s |nome de Olá de Olá runbook. |
| Caller_s |Quem iniciou a operação de Olá.  Os valores possíveis são um endereço de e-mail ou o sistema para trabalhos agendados. |
| StreamType_s |tipo de Olá do fluxo de trabalho. Os valores possíveis são:<br>- Em Curso<br>- Saída<br>- Aviso<br>- Erro<br>- Depuração<br>- Verboso |
| Tenant_g | GUID que identifica o inquilino Olá para Olá autor da chamada. |
| JobId_g |GUID que é Olá Id da tarefa de runbook Olá. |
| ResultType |Estado da tarefa de runbook Olá Olá.  Os valores possíveis são:<br>-Em curso |
| Categoria | Classificação do tipo de Olá de dados.  Para automatização, o valor de Olá é JobStreams. |
| OperationName | Especifica o tipo de Olá da operação efetuada no Azure.  Para automatização, o valor de Olá é tarefa. |
| Recurso | Nome da conta de automatização de Olá |
| SourceSystem | Como a análise de registos recolhidos dados de Olá. Sempre *Azure* para diagnóstico do Azure. |
| ResultDescription |Inclui o fluxo de saída de Olá do runbook Olá. |
| CorrelationId |GUID que é Olá Id de correlação da tarefa de runbook Olá. |
| ResourceId |Especifica o id do recurso de conta de automatização do Azure do Olá de Olá runbook. |
| SubscriptionId | Olá subscrição do Azure Id (GUID) para Olá conta de automatização. |
| ResourceGroup | Nome do grupo de recursos de Olá para Olá conta de automatização. |
| ResourceProvider | MICROSOFT. AUTOMATIZAÇÃO |
| ResourceType | AUTOMATIONACCOUNTS |

## <a name="viewing-automation-logs-in-log-analytics"></a>Visualizar automatização registos de análise de registos
Agora que iniciou a enviar o tooLog de registos de tarefa de automatização análise, vamos ver o que pode fazer com estes registos no interior de análise de registos.

toosee Olá os registos, executados Olá seguinte consulta:`Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION"`

### <a name="send-an-email-when-a-runbook-job-fails-or-suspends"></a>Envie um e-mail quando uma tarefa de runbook falha ou suspende
Uma das nossa principal cliente pede-lhe destina-se Olá capacidade toosend um texto ou um e-mail quando algo não bate com uma tarefa de runbook.   

regra de toocreate um alerta, que comece por criar uma pesquisa de registo do runbook Olá registos de tarefa que devem invocar alerta Olá.  Clique em Olá **alerta** botão toocreate e configurar a regra de alerta de Olá.

1. Na página de descrição geral da análise do registo de Olá, clique em **pesquisa registo**.
2. Criar uma consulta de pesquisa de registo para o alerta, escrevendo Olá seguir pesquisa no campo de consulta Olá: `Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION" Category=JobLogs (ResultType=Failed OR ResultType=Suspended)` também pode agrupar por Olá RunbookName utilizando:`Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION" Category=JobLogs (ResultType=Failed OR ResultType=Suspended) | measure Count() by RunbookName_s`   

   Se configurou os registos de mais do que uma conta ou a subscrição tooyour área de trabalho automatização, pode agrupar os alertas por subscrição e conta de automatização.  Nome da conta de automatização pode ser derivado de campo de recursos de Olá na pesquisa de Olá de JobLogs.  
3. Olá tooopen **Adicionar regra de alerta** ecrã, clique em **alerta** em Olá parte superior da página Olá. Para obter mais detalhes sobre o alerta do Olá opções tooconfigure Olá, consulte [alertas na análise de registos](../log-analytics/log-analytics-alerts.md#alert-rules).

### <a name="find-all-jobs-that-have-completed-with-errors"></a>Localizar todas as tarefas que foram concluídas com erros
Além disso tooalerting sobre falhas, pode encontrar quando uma tarefa de runbook tem um erro de não interrupção. Nestes casos PowerShell produz uma sequência de erro, mas a erros de não interrupção Olá não fazer com que a tarefa toosuspend ou falhar.    

1. Na sua área de trabalho de análise de registos, clique em **pesquisa registo**.
2. No campo de consulta Olá, escreva `Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION" Category=JobStreams StreamType_s=Error | measure count() by JobId_g` e, em seguida, clique em **pesquisa**.

### <a name="view-job-streams-for-a-job"></a>Fluxos de trabalho de vista de uma tarefa
Quando está a depurar uma tarefa, também poderá toolook em fluxos de trabalho de Olá.  Olá seguinte consulta apresenta todos os Olá fluxos de uma única tarefa com o GUID 2ebd22ea-e05e-4eb9 - 9d 76-d73cbd4356e0:   

`Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION" Category=JobStreams JobId_g="2ebd22ea-e05e-4eb9-9d76-d73cbd4356e0" | sort TimeGenerated | select ResultDescription`

### <a name="view-historical-job-status"></a>Ver o estado do histórico de tarefas
Por fim, poderá ser útil toovisualize o histórico do trabalho ao longo do tempo.  Pode utilizar este toosearch de consulta para o estado de Olá das suas tarefas ao longo do tempo.

`Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION" Category=JobLogs NOT(ResultType="started") | measure Count() by ResultType interval 1hour`  
<br> ![Gráfico de estado de tarefa históricos do OMS](media/automation-manage-send-joblogs-log-analytics/historical-job-status-chart.png)<br>

## <a name="summary"></a>Resumo
Enviando a automatização tarefa estado e o fluxo de dados tooLog análise, pode obter o melhor aprofundadas sobre o estado de Olá das suas tarefas de automatização por:
+ Configurar alertas toonotify, quando existe um problema
+ Utilizar vistas personalizadas e toovisualize de consultas de pesquisa os resultados de runbook, estado de tarefa de runbook e de outras relacionados com indicadores chaves ou métricas.  

Análise de registos fornece maior visibilidade operacional tooyour tarefas de automatização e pode ajudar a incidentes de endereço mais rápidas.  

## <a name="next-steps"></a>Passos seguintes
* toolearn mais informações sobre como consultas de pesquisa diferentes tooconstruct e revisão Olá automatização tarefa registos de análise de registos, consulte [pesquisas de registo na análise de registos](../log-analytics/log-analytics-log-searches.md)
* toounderstand como toocreate e obter resultados mensagens de erro e a partir de runbooks, consulte [Runbook de saída e as mensagens](automation-runbook-output-and-messages.md)
* mais sobre a execução do runbook, como as tarefas de runbook toomonitor e outros detalhes técnicos, consulte toolearn [controlar uma tarefa de runbook](automation-runbook-execution.md)
* toolearn mais informações sobre a análise de registos do OMS e origens de recolha de dados, consulte [dados de armazenamento do Azure recolha na descrição geral da análise de registos](../log-analytics/log-analytics-azure-storage.md)
