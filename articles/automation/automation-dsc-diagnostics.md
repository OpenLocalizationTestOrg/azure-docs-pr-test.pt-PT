---
title: "aaaForward tooOMS de dados relatórios análise de registos do Automation DSC do Azure | Microsoft Docs"
description: "Este artigo demonstra como toosend Desired Configuration (DSC) dados tooMicrosoft análise de registos do Operations Management Suite toodeliver obter informações adicionais e gestão de relatórios de estado."
services: automation
documentationcenter: 
author: eslesar
manager: carmonm
editor: tysonn
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/24/2017
ms.author: eslesar
ms.openlocfilehash: 21f78d5549d53ba3d7e237f55d9086f380cf3351
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="forward-azure-automation-dsc-reporting-data-toooms-log-analytics"></a>Reencaminhar relatórios de dados tooOMS Log Analytics do Azure Automation DSC

Automatização pode enviar DSC nó Estado dados tooyour análise de registos do Microsoft Operations Management Suite (OMS) área de trabalho.  
Estado de conformidade é visível no portal do Azure de Olá, ou com o PowerShell, para nós e para recursos de DSC individuais em configurações de nó. Análise de registos pode:

* Obter as informações de compatibilidade para os nós geridos e recursos individuais
* Acionar um e-mail ou o alerta com base no estado de conformidade
* Escrever consultas avançadas entre os nós geridos
* Correlacionar o estado de conformidade em contas de automatização
* Visualizar o histórico de conformidade do nó ao longo do tempo

## <a name="prerequisites"></a>Pré-requisitos

enviar o DSC de automatização de toostart relatórios tooLog análise, tem de:

* Olá Novembro de 2016 ou versão posterior do [Azure PowerShell](/powershell/azure/overview) (v2.3.0).
* Uma conta de Automatização do Azure. Para obter mais informações, consulte [introdução da automatização do Azure](automation-offering-get-started.md)
* Uma área de trabalho de análise de registos com um **automatização e controlo** oferta de serviço. Para obter mais informações, consulte [introdução à análise de registos](../log-analytics/log-analytics-get-started.md).
* Pelo menos um nó de DSC de automatização do Azure. Para obter mais informações, consulte [máquinas de integração de gestão do Automation DSC do Azure](automation-dsc-onboarding.md) 

## <a name="set-up-integration-with-log-analytics"></a>Configurar a integração com a análise de registos

toobegin importar dados do Automation DSC do Azure para a análise de registos, Olá concluir os passos seguintes:

1. Inicie sessão no tooyour conta do Azure no PowerShell. Consulte [iniciar sessão com o Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/authenticate-azureps?view=azurermps-4.0.0)
1. Obter Olá _ResourceId_ da sua conta de automatização, executando o seguinte comando do PowerShell de Olá: (se tiver mais do que uma conta de automatização, escolha Olá _ResourceID_ para a conta de Olá pretende tooconfigure).

  ```powershell
  # Find hello ResourceId for hello Automation Account
  Find-AzureRmResource -ResourceType "Microsoft.Automation/automationAccounts"
  ```
1. Obter Olá _ResourceId_ da sua área de trabalho de análise de registos, executando o seguinte comando do PowerShell de Olá: (se tiver mais de uma área de trabalho, escolha Olá _ResourceID_ para área de trabalho Olá pretende tooconfigure).

  ```powershell
  # Find hello ResourceId for hello Log Analytics workspace
  Find-AzureRmResource -ResourceType "Microsoft.OperationalInsights/workspaces"
  ```
1. Olá executar seguinte comando do PowerShell, substituindo `<AutomationResourceId>` e `<WorkspaceResourceId>` com Olá _ResourceId_ valores de cada um dos passos anteriores Olá:

  ```powershell
  Set-AzureRmDiagnosticSetting -ResourceId <AutomationResourceId> -WorkspaceId <WorkspaceResourceId> -Enabled $true -Categories "DscNodeStatus"
  ```

Se quiser toostop importar dados do Automation DSC do Azure para a análise de registos, execute Olá seguinte comando do PowerShell.

```powershell
Set-AzureRmDiagnosticSetting -ResourceId <AutomationResourceId> -WorkspaceId <WorkspaceResourceId> -Enabled $false -Categories "DscNodeStatus"
```

## <a name="view-hello-dsc-logs"></a>Ver registos de Olá DSC

Depois de configurar a integração com a análise de registos para os seus dados de DSC de automatização, um **pesquisa registo** botão será apresentado no Olá **nós de DSC** painel da sua conta de automatização. Clique em Olá **pesquisa registo** botão registos de Olá tooview para dados do nó DSC.

![Botão de procura de registo](media/automation-dsc-diagnostics/log-search-button.png)

Olá **pesquisa registo** abre painel e vir um **DscNodeStatusData** operação para cada nó de DSC e um **DscResourceStatusData** operação para cada [DSC recurso](https://msdn.microsoft.com/powershell/dsc/resources) chamado no nó do Olá nó Configuração toothat aplicados.

Olá **DscResourceStatusData** operação contém informações de erro para quaisquer recursos de DSC que falhou.

Clique em cada operação nos dados de Olá Olá lista toosee para essa operação.

Também pode ver os registos de Olá pesquisando [na análise de registos. Consulte [localizar dados através de pesquisas de registo](../log-analytics/log-analytics-log-searches.md).
Seguinte do tipo Olá consulta toofind o DSC registos:`Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION" Category = "DscNodeStatus"`

Também pode limitar a consulta de Olá por nome de operação de Olá. Por exemplo: ' tipo = AzureDiagnostics ResourceProvider = "MICROSOFT. Categoria de AUTOMATIZAÇÃO"="DscNodeStatus"OperationName ="DscNodeStatusData"

### <a name="send-an-email-when-a-dsc-compliance-check-fails"></a>Enviar um e-mail quando ocorre uma falha de uma verificação de compatibilidade de DSC

Um dos nossos pedidos de cliente superior é Olá capacidade toosend uma mensagem de e-mail ou um texto quando algo não bate com uma configuração de DSC.   

regra de toocreate um alerta, que comece por criar uma pesquisa de registo de registos de relatório de DSC Olá deve invocar alerta Olá.  Clique em Olá **alerta** botão toocreate e configurar a regra de alerta de Olá.

1. Na página de descrição geral da análise do registo de Olá, clique em **pesquisa registo**.
1. Crie uma consulta de pesquisa de registo para o alerta, escrevendo Olá seguir pesquisa no campo de consulta Olá:`Type=AzureDiagnostics Category=DscNodeStatus NodeName_s=DSCTEST1 OperationName=DscNodeStatusData ResultType=Failed`

  Se configurou os registos de mais do que uma conta ou a subscrição tooyour área de trabalho automatização, pode agrupar os alertas por subscrição e conta de automatização.  
  Nome da conta de automatização pode ser derivado de campo de recursos de Olá na pesquisa de Olá de DscNodeStatusData.  
1. Olá tooopen **Adicionar regra de alerta** ecrã, clique em **alerta** em Olá parte superior da página Olá. Para obter mais informações sobre o alerta do Olá opções tooconfigure Olá, consulte [alertas na análise de registos](../log-analytics/log-analytics-alerts.md#alert-rules).

### <a name="find-failed-dsc-resources-across-all-nodes"></a>Falha ao localizar recursos de DSC em todos os nós

Uma vantagem de utilizar a análise de registos é que pode procurar verificações falhadas entre nós.
toofind todas as instâncias de recursos de DSC que falhou.

1. Na página de descrição geral da análise do registo de Olá, clique em **pesquisa registo**.
1. Crie uma consulta de pesquisa de registo para o alerta, escrevendo Olá seguir pesquisa no campo de consulta Olá:`Type=AzureDiagnostics Category=DscNodeStatus OperationName=DscResourceStatusData ResultType=Failed`

### <a name="view-historical-dsc-node-status"></a>Ver estado histórico de nó DSC

Por fim, poderá ser útil toovisualize o histórico de estado do nó DSC ao longo do tempo.  
Pode utilizar este toosearch de consulta para o estado de Olá do Estado do nó DSC ao longo do tempo.

`Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION" Category=DscNodeStatus NOT(ResultType="started") | measure Count() by ResultType interval 1hour`  

Esta ação apresenta um gráfico de estado do nó de Olá ao longo do tempo.

## <a name="log-analytics-records"></a>Registos do Log Analytics

Diagnóstico da automatização do Azure cria duas categorias de registos de análise de registos.

### <a name="dscnodestatusdata"></a>DscNodeStatusData

| Propriedade | Descrição |
| --- | --- |
| TimeGenerated |Data e hora quando executou a verificação de conformidade de Olá. |
| OperationName |DscNodeStatusData |
| ResultType |Indica se o nó de Olá está em conformidade. |
| NodeName_s |nome de Olá do nó Olá de gerido. |
| NodeComplianceStatus_s |Indica se o nó de Olá está em conformidade. |
| DscReportStatus |Verifique se a compatibilidade Olá foi executada com êxito. |
| ConfigurationMode | Como a configuração de Olá é nó toohello aplicados. Os valores possíveis são __"ApplyOnly"__,__"ApplyandMonitior"__, e __"ApplyandAutoCorrect"__. <ul><li>__ApplyOnly__: DSC aplica-se a configuração de Olá e faz nada adicional a menos que é feito o Push de uma nova configuração de nó de destino toohello ou quando uma nova configuração é retirada de um servidor. Após a aplicação inicial de uma nova configuração, DSC não verificar que se desviam de um estado anteriormente configurado. DSC tenta configuração de Olá tooapply até ter êxito antes de __ApplyOnly__ entra em vigor. </li><li> __ApplyAndMonitor__: Este é o valor predefinido de Olá. Olá MMC aplica-se as configurações de novo. Após a aplicação inicial de uma nova configuração, se o nó de destino Olá drifts do Estado de Olá assim o desejar, DSC relatórios discrepância Olá nos registos. DSC tenta configuração de Olá tooapply até ter êxito antes de __ApplyAndMonitor__ entra em vigor.</li><li>__ApplyAndAutoCorrect__: DSC aplica-se as configurações de novo. Após a aplicação inicial de uma nova configuração, se o nó de destino Olá drifts do estado pretendido de Olá, DSC discrepância Olá nos registos de relatórios e, em seguida, volta a configuração atual Olá.</li></ul> |
| HostName_s | nome de Olá do nó Olá de gerido. |
| IPAddress | endereço de IPv4 Olá de Olá geridos nó. |
| Categoria | DscNodeStatus |
| Recurso | nome de Olá do Olá conta de automatização do Azure. |
| Tenant_g | GUID que identifica o inquilino Olá para Olá autor da chamada. |
| NodeId_g |GUID que identifica o nó Olá de gerido. |
| DscReportId_g |GUID que identifica o relatório de Olá. |
| LastSeenTime_t |Data e hora quando o relatório Olá pela última vez foi visualizado. |
| ReportStartTime_t |Data e hora quando o relatório de Olá foi iniciado. |
| ReportEndTime_t |Data e hora quando o relatório de Olá foi concluído. |
| NumberOfResources_d |número de Olá de recursos de DSC chamado no nó de toohello Olá configuração aplicada. |
| SourceSystem | Como a análise de registos recolhidos dados de Olá. Sempre *Azure* para diagnóstico do Azure. |
| ResourceId |Especifica a conta de automatização do Azure Olá. |
| ResultDescription | Descrição de Olá para esta operação. |
| SubscriptionId | Olá subscrição do Azure Id (GUID) para Olá conta de automatização. |
| ResourceGroup | Nome do grupo de recursos de Olá para Olá conta de automatização. |
| ResourceProvider | MICROSOFT. AUTOMATIZAÇÃO |
| ResourceType | AUTOMATIONACCOUNTS |
| CorrelationId |GUID que é Olá Id de correlação do relatório de compatibilidade de Olá. |

### <a name="dscresourcestatusdata"></a>DscResourceStatusData

| Propriedade | Descrição |
| --- | --- |
| TimeGenerated |Data e hora quando executou a verificação de conformidade de Olá. |
| OperationName |DscResourceStatusData|
| ResultType |Indica se o recurso de Olá está em conformidade. |
| NodeName_s |nome de Olá do nó Olá de gerido. |
| Categoria | DscNodeStatus |
| Recurso | nome de Olá do Olá conta de automatização do Azure. |
| Tenant_g | GUID que identifica o inquilino Olá para Olá autor da chamada. |
| NodeId_g |GUID que identifica o nó Olá de gerido. |
| DscReportId_g |GUID que identifica o relatório de Olá. |
| DscResourceId_s |nome da instância de recurso Olá DSC Olá. |
| DscResourceName_s |nome de Olá do recurso de Olá DSC. |
| DscResourceStatus_s |Indica se Olá recursos de DSC está em conformidade. |
| DscModuleName_s |nome do módulo do PowerShell Olá que contém os recursos de DSC Olá Olá. |
| DscModuleVersion_s |versão de Olá do módulo do PowerShell Olá que contém os recursos de DSC Olá. |
| DscConfigurationName_s |nome de Olá da configuração de Olá aplicadas nó toohello. |
| ErrorCode_s | código de erro de Olá se recursos Olá falhou. |
| ErrorMessage_s |mensagem de erro de Olá se recursos Olá falhou. |
| DscResourceDuration_d |tempo de Olá, em segundos, que tenha executado o recurso de Olá DSC. |
| SourceSystem | Como a análise de registos recolhidos dados de Olá. Sempre *Azure* para diagnóstico do Azure. |
| ResourceId |Especifica a conta de automatização do Azure Olá. |
| ResultDescription | Descrição de Olá para esta operação. |
| SubscriptionId | Olá subscrição do Azure Id (GUID) para Olá conta de automatização. |
| ResourceGroup | Nome do grupo de recursos de Olá para Olá conta de automatização. |
| ResourceProvider | MICROSOFT. AUTOMATIZAÇÃO |
| ResourceType | AUTOMATIONACCOUNTS |
| CorrelationId |GUID que é Olá Id de correlação do relatório de compatibilidade de Olá. |

## <a name="summary"></a>Resumo

Enviando o seu tooLog de dados do Automation DSC análise, pode obter o melhor aprofundadas sobre o estado de Olá os nós de DSC de automatização por:

* Configurar alertas toonotify, quando existe um problema
* Utilizar vistas personalizadas e toovisualize de consultas de pesquisa os resultados de runbook, estado de tarefa de runbook e de outras relacionados com indicadores chaves ou métricas.  

Análise de registos fornece dados de DSC de automatização de tooyour do maiores visibilidade operacional e pode ajudar a incidentes de endereço mais rapidamente.  

## <a name="next-steps"></a>Passos seguintes

* toolearn mais informações sobre como consultas de pesquisa diferentes tooconstruct e reveja Olá Automation DSC registos de análise do registo, consulte [pesquisas de registo na análise de registos](../log-analytics/log-analytics-log-searches.md)
* toolearn mais sobre a utilização do Automation DSC do Azure, consulte [introdução ao Azure Automation DSC](automation-dsc-getting-started.md)
* toolearn mais informações sobre a análise de registos do OMS e origens de recolha de dados, consulte [dados de armazenamento do Azure recolha na descrição geral da análise de registos](../log-analytics/log-analytics-azure-storage.md)

