---
title: "aaaCollect Azure service métricas e registos de análise de registos | Microsoft Docs"
description: "Configure o diagnóstico nos recursos do Azure toowrite registos e as métricas tooLog análise."
services: log-analytics
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: 
ms.assetid: 84105740-3697-4109-bc59-2452c1131bfe
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/12/2017
ms.author: magoedte
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 1cede9a94ec83c4e3a95853dc2ec355d8df06d6e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="collect-azure-service-logs-and-metrics-for-use-in-log-analytics"></a>Recolher métricas para utilização na análise de registos e registos do serviço do Azure

Existem quatro formas diferentes de recolha de registos e as métricas para os serviços do Azure:

1. Diagnóstico do Azure direcionar tooLog análise (*diagnóstico* no Olá a tabela seguinte)
2. Diagnóstico do Azure tooAzure armazenamento tooLog análise (*armazenamento* no Olá a tabela seguinte)
3. Os conectores para serviços do Azure (*conectores* no Olá a tabela seguinte)
4. Scripts toocollect e, em seguida, os dados de post para análise de registos (espaços em branco no Olá a tabela seguinte e serviços que não estejam listados)


| Serviço                 | Tipo de Recurso                           | Registos        | Métricas     | Solução |
| --- | --- | --- | --- | --- |
| Gateways de aplicação    | Network/applicationgateways   | Diagnóstico | Diagnóstico | [Análise de Gateway de aplicação do Azure](log-analytics-azure-networking-analytics.md#azure-application-gateway-analytics-solution-in-log-analytics) |
| Informações de aplicação    |                                         | conector   | conector   | [Conector do Application Insights](https://blogs.technet.microsoft.com/msoms/2016/09/26/application-insights-connector-in-oms/) (pré-visualização) |
| Contas de Automatização     | Microsoft.Automation/AutomationAccounts | Diagnóstico |             | [Obter mais informações](../automation/automation-manage-send-joblogs-log-analytics.md)|
| Contas do batch          | Microsoft.Batch/batchAccounts           | Diagnóstico | Diagnóstico | |
| Serviços cloud clássico  |                                         | Armazenamento     |             | [Obter mais informações](log-analytics-azure-storage-iis-table.md) |
| Serviços cognitivos      | Microsoft.CognitiveServices/accounts    |             | Diagnóstico | |
| Análise do Data Lake     | Microsoft.DataLakeAnalytics/accounts    | Diagnóstico |             | |
| Arquivo data Lake         | Microsoft.DataLakeStore/accounts        | Diagnóstico |             | |
| Espaço de nomes de Hub de eventos     | Microsoft.EventHub/namespaces           | Diagnóstico | Diagnóstico | |
| Hubs IoT                | Microsoft.Devices/IotHubs               |             | Diagnóstico | |
| Cofre de Chaves               | Microsoft.KeyVault/vaults               | Diagnóstico |             | [Análise de KeyVault](log-analytics-azure-key-vault.md) |
| Balanceadores de carga          | Microsoft.Network/loadBalancers         | Diagnóstico |             |  |
| Aplicações Lógicas              | Microsoft.Logic/workflows <br> Microsoft.Logic/integrationAccounts | Diagnóstico | Diagnóstico | |
| Grupos de Segurança de Rede | Microsoft.Network/networksecuritygroups | Diagnóstico |             | [Análise de grupo de segurança de rede do Azure](log-analytics-azure-networking-analytics.md#azure-network-security-group-analytics-solution-in-log-analytics) |
| Cofres de recuperação         | Microsoft.RecoveryServices/vaults       |             |             | [O Azure Recovery Services análise (pré-visualização)](https://github.com/krnese/AzureDeploy/blob/master/OMS/MSOMS/Solutions/recoveryservices/)|
| Procurar serviços         | Microsoft.Search/searchServices         | Diagnóstico | Diagnóstico | |
| Espaço de nomes do Service Bus   | Microsoft.ServiceBus/namespaces         | Diagnóstico | Diagnóstico | [Análise de barramento de serviço (pré-visualização)](https://github.com/Azure/azure-quickstart-templates/tree/master/oms-servicebus-solution)|
| Service Fabric          |                                         | Armazenamento     |             | [Análise de recursos de infraestrutura de serviço (pré-visualização)](log-analytics-service-fabric.md) |
| SQL (v12)               | Microsoft.Sql/servers/databases <br> Microsoft.Sql/servers/elasticPools |             | Diagnóstico | [Análise de SQL do Azure (pré-visualização)](log-analytics-azure-sql.md) |
| Armazenamento                 |                                         |             | Script      | [Análise de armazenamento do Azure (pré-visualização)](https://github.com/Azure/azure-quickstart-templates/tree/master/oms-azure-storage-analytics-solution) |
| Virtual Machines        | Microsoft.Compute/virtualMachines       | Extensão   | Extensão <br> Diagnóstico  | |
| Conjuntos de dimensionamento de máquinas virtuais | Microsoft.Compute/virtualMachines <br> Microsoft.Compute/virtualMachineScaleSets/virtualMachines |             | Diagnóstico | |
| Web farms de servidores        | Microsoft.Web/serverfarms               |             | Diagnóstico | |
| Web Sites               | Microsoft.Web/sites <br> Microsoft.Web/sites/slots |             | Diagnóstico | [Análise de aplicações Web do Azure (pré-visualização)](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.AzureWebAppsAnalyticsOMS?tab=Overview) |


> [!NOTE]
> Para monitorizar máquinas virtuais do Azure (Linux e Windows), recomendamos que instale Olá [extensão da VM de análise do registo](log-analytics-azure-vm-extension.md). agente de Olá fornece-lhe insights recolhidos a partir de máquinas virtuais. Também pode utilizar a extensão de Olá para conjuntos de dimensionamento de Máquina Virtual.
>
>

## <a name="azure-diagnostics-direct-toolog-analytics"></a>Diagnóstico do Azure direcionar tooLog análise
Muitos recursos do Azure são toowrite capaz de registos de diagnóstico e métricas diretamente tooLog análise e isto é a forma de Olá preferencial de recolha de dados de Olá para análise. Ao utilizar o diagnóstico do Azure, são escritos dados no imediatamente tooLog análise e existe sem necessidade de toofirst escrita Olá dados toostorage.

Recursos do Azure que suportem [Azure monitor](../monitoring-and-diagnostics/monitoring-overview.md) pode enviar os registos e as métricas diretamente tooLog análise.

* Para obter detalhes de Olá das métricas disponíveis Olá, consulte demasiado[suportado métricas com a monitorização do Azure](../monitoring-and-diagnostics/monitoring-supported-metrics.md).
* Para obter detalhes de Olá de registos disponíveis Olá, consulte demasiado[suportado serviços e o esquema para os registos de diagnóstico](../monitoring-and-diagnostics/monitoring-diagnostic-logs-schema.md).

### <a name="enable-diagnostics-with-powershell"></a>Ativar diagnósticos com o PowerShell
Precisa de Olá Novembro de 2016 (v2.3.0) ou versão posterior do [Azure PowerShell](/powershell/azure/overview).

Olá seguir PowerShell exemplo mostra como toouse [Set-AzureRmDiagnosticSetting](/powershell/module/azurerm.insights/set-azurermdiagnosticsetting) tooenable diagnóstico num grupo de segurança de rede. Olá mesma abordagem funciona para todos os recursos suportados - definir `$resourceId` toohello id de recurso do recurso de Olá pretende tooenable diagnósticos para.

```powershell
$workspaceId = "/subscriptions/d2e37fee-1234-40b2-5678-0b2199de3b50/resourcegroups/oi-default-east-us/providers/microsoft.operationalinsights/workspaces/rollingbaskets"

$resourceId = "/SUBSCRIPTIONS/ec11ca60-1234-491e-5678-0ea07feae25c/RESOURCEGROUPS/DEMO/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUPS/DEMO"

Set-AzureRmDiagnosticSetting -ResourceId $ResourceId  -WorkspaceId $workspaceId -Enabled $true
```

### <a name="enable-diagnostics-with-resource-manager-templates"></a>Ativar o diagnóstico com modelos do Resource Manager

diagnóstico de tooenable num recurso quando é criado e diagnóstico Olá enviaram área de trabalho do Log Analytics tooyour que pode utilizar um toohello semelhante modelo um abaixo. Neste exemplo é para uma conta de automatização, mas funciona para todos os tipos de recurso suportados.

```json
        {
            "type": "Microsoft.Automation/automationAccounts/providers/diagnosticSettings",
            "name": "[concat(parameters('omsAutomationAccountName'), '/', 'Microsoft.Insights/service')]",
            "apiVersion": "2015-07-01",
            "dependsOn": [
                "[concat('Microsoft.Automation/automationAccounts/', parameters('omsAutomationAccountName'))]",
                "[concat('Microsoft.OperationalInsights/workspaces/', parameters('omsWorkspaceName'))]"
            ],
            "properties": {
                "workspaceId": "[resourceId('Microsoft.OperationalInsights/workspaces', parameters('omsWorkspaceName'))]",
                "logs": [
                    {
                        "category": "JobLogs",
                        "enabled": true
                    },
                    {
                        "category": "JobStreams",
                        "enabled": true
                    }
                ]
            }
        }
```

[!INCLUDE [log-analytics-troubleshoot-azure-diagnostics](../../includes/log-analytics-troubleshoot-azure-diagnostics.md)]

## <a name="azure-diagnostics-toostorage-then-toolog-analytics"></a>Toostorage de diagnóstico do Azure, em seguida, tooLog análise

Para recolher registos de dentro de alguns dos recursos, é possível toosend Olá registos tooAzure armazenamento e, em seguida, configurar o registo tooread Olá pelos registos de análise do armazenamento.

Análise de registos pode utilizar esta abordagem toocollect obter um diagnóstico do armazenamento do Azure para Olá registos de recursos e os seguintes:

| Recurso | Registos |
| --- | --- |
| Service Fabric |ETWEvent <br> Eventos operacionais <br> Evento de Ator fiável <br> Evento de serviço fiável |
| Virtual Machines |Linux Syslog <br> Eventos do Windows <br> Registo do IIS <br> Windows ETWEvent |
| Funções da Web <br> Funções de trabalho |Linux Syslog <br> Eventos do Windows <br> Registo do IIS <br> Windows ETWEvent |

> [!NOTE]
> São-lhe cobrados a taxas de dados do Azure normais para armazenamento e transações quando enviar diagnósticos tooa conta de armazenamento e para quando Log Analytics lê dados de Olá da sua conta de armazenamento.
>
>

Consulte [armazenamento de BLOBs de utilização para o IIS e a tabela de armazenamento para os eventos](log-analytics-azure-storage-iis-table.md) toolearn mais informações sobre como a análise de registos pode recolher estes registos.

## <a name="connectors-for-azure-services"></a>Conectores para serviços do Azure

Não há um conector para o Application Insights, que permite que os dados recolhidos pelo toobe Application Insights enviado tooLog análise.

Saiba mais sobre Olá [conector do Application Insights](https://blogs.technet.microsoft.com/msoms/2016/09/26/application-insights-connector-in-oms/).

## <a name="scripts-toocollect-and-post-data-toolog-analytics"></a>Scripts toocollect e publique tooLog análise de dados

Para os serviços do Azure que não fornecem uma forma direta toosend registos e as métricas tooLog análise pode utilizar um toocollect de script da automatização do Azure Olá métricas e registo. Olá script podem, em seguida, enviar Olá dados tooLog análise utilizando Olá [API de recoletores de dados](log-analytics-data-collector-api.md)

tem de Galeria de modelo do Azure Olá [exemplos de utilização da automatização do Azure](https://azure.microsoft.com/en-us/resources/templates/?term=OMS) toocollect dados de serviços e enviar tooLog análise.

## <a name="next-steps"></a>Passos seguintes

* [Utilizar o blob storage para o IIS e a tabela de armazenamento para eventos](log-analytics-azure-storage-iis-table.md) registos de Olá tooread para serviços do Azure que escrever diagnóstico tootable armazenamento nem o IIS regista armazenamento tooblob escrito.
* [Permitir soluções](log-analytics-add-solutions.md) tooprovide aprofundadas sobre dados Olá.
* [Utilizar consultas de pesquisa](log-analytics-log-searches.md) dados de Olá tooanalyze.
