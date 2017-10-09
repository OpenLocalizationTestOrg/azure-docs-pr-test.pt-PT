---
title: "Exemplos de início rápido do aaaAzure Monitor PowerShell. | Microsoft Docs"
description: "Utilize o PowerShell tooaccess funcionalidades de monitorização do Azure, tais como o dimensionamento automático, alertas, webhooks e procure-os registos de atividade."
author: kamathashwin
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: c0761814-7148-4ab5-8c27-a2c9fa4cfef5
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: ashwink
ms.openlocfilehash: 6eece0b0227e0bbf08225bd330d0601169911f55
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-monitor-powershell-quick-start-samples"></a>Exemplos de início rápido do Azure PowerShell de Monitor
Este artigo apresenta o exemplo toohelp de comandos do PowerShell que aceder às funcionalidades de monitorização do Azure. Monitor do Azure permite-lhe tooAutoScale serviços em nuvem, as máquinas virtuais e aplicações Web e toosend as notificações de alerta ou chamada web URLs com base nos valores de dados de telemetria configurado.

> [!NOTE]
> Monitor do Azure é o nome novo Olá que foi chamado "Informações do Azure" até 25th de Setembro de 2016. No entanto, Olá espaços de nomes e, consequentemente, Olá os seguintes comandos ainda contenham insights"Olá".
> 
> 

## <a name="set-up-powershell"></a>Configurar o PowerShell
Se ainda não o tiver feito, configure toorun PowerShell no seu computador. Para obter mais informações, consulte [como tooInstall e configurar o PowerShell](/powershell/azure/overview).

## <a name="examples-in-this-article"></a>Exemplos neste artigo
Exemplos de Olá artigo Olá mostram como pode utilizar os cmdlets de Monitor do Azure. Também pode rever a lista completa de Olá Azure Monitor de cmdlets do PowerShell em [Cmdlets de Monitor do Azure (Insights)](https://msdn.microsoft.com/library/azure/mt282452#40v=azure.200#41.aspx).

## <a name="sign-in-and-use-subscriptions"></a>A iniciar sessão e utilizar subscrições
Em primeiro lugar, inicie sessão no tooyour subscrição do Azure.

```PowerShell
Login-AzureRmAccount
```

Isto requer toosign no. Quando o fizer, a conta, são apresentadas TenantID e ID de subscrição predefinido. Olá todos os cmdlets do Azure de trabalho no contexto de Olá da sua subscrição predefinida. lista de Olá tooview de subscrições tem acesso a, utilize Olá os seguintes comandos.

```PowerShell
Get-AzureRmSubscription
```

toochange a trabalho contexto tooa subscrição diferente, Olá utilize os seguintes comandos.

```PowerShell
Set-AzureRmContext -SubscriptionId <subscriptionid>
```


## <a name="retrieve-activity-log-for-a-subscription"></a>Obter o registo de atividade para uma subscrição
Olá utilize `Get-AzureRmLog` cmdlet.  Olá seguem-se alguns exemplos comuns.

Obter entradas de registo a partir deste toopresent de data/hora:

```PowerShell
Get-AzureRmLog -StartTime 2016-03-01T10:30
```

Obter entradas de registo entre um intervalo de data/hora:

```PowerShell
Get-AzureRmLog -StartTime 2015-01-01T10:30 -EndTime 2015-01-01T11:30
```

Obter entradas de registo de um grupo de recurso específico:

```PowerShell
Get-AzureRmLog -ResourceGroup 'myrg1'
```

Obter entradas de registo a partir de um fornecedor de recursos específico entre um intervalo de data/hora:

```PowerShell
Get-AzureRmLog -ResourceProvider 'Microsoft.Web' -StartTime 2015-01-01T10:30 -EndTime 2015-01-01T11:30
```

Obter todas as entradas de registo com um emissor específico:

```PowerShell
Get-AzureRmLog -Caller 'myname@company.com'
```

Olá comando obtém Olá últimas 1 000 eventos de registo de atividade Olá os seguintes:

```PowerShell
Get-AzureRmLog -MaxEvents 1000
```

`Get-AzureRmLog`suporta muitos outros parâmetros. Consulte Olá `Get-AzureRmLog` referência para obter mais informações.

> [!NOTE]
> `Get-AzureRmLog`Fornece apenas 15 dias do histórico. Utilizar Olá **- MaxEvents** parâmetro permite-lhe tooquery Olá últimas N eventos, para além de 15 dias. tooaccess eventos com mais de 15 dias, utilize Olá REST API ou o SDK (c# exemplo com Olá SDK). Se não incluir **StartTime**, em seguida, o valor predefinido de Olá é **EndTime** menos uma hora. Se não incluir **EndTime**, em seguida, o valor predefinido de Olá é o tempo atual. Todas as horas são em UTC.
> 
> 

## <a name="retrieve-alerts-history"></a>Obter o histórico de alertas
tooview alerta todos os eventos, pode consultar Olá registos do Azure Resource Manager utilizando Olá exemplos a seguir.

```PowerShell
Get-AzureRmLog -Caller "Microsoft.Insights/alertRules" -DetailedOutput -StartTime 2015-03-01
```

histórico de Olá tooview para um alerta específico da regra, pode utilizar Olá `Get-AzureRmAlertHistory` cmdlet, passando na ID de recurso Olá Olá de regra de alerta.

```PowerShell
Get-AzureRmAlertHistory -ResourceId /subscriptions/s1/resourceGroups/rg1/providers/microsoft.insights/alertrules/myalert -StartTime 2016-03-1 -Status Activated
```

Olá `Get-AzureRmAlertHistory` cmdlet suporta vários parâmetros. Obter mais informações, consulte [Get-AlertHistory](https://msdn.microsoft.com/library/mt282453.aspx).

## <a name="retrieve-information-on-alert-rules"></a>Obter informações sobre regras de alertas
Todos os seguintes comandos de Olá agirem sobre um grupo de recursos com o nome "montest".

Ver todas as propriedades de Olá Olá de regra de alerta:

```PowerShell
Get-AzureRmAlertRule -Name simpletestCPU -ResourceGroup montest -DetailedOutput
```

Obter todos os alertas no grupo de recursos:

```PowerShell
Get-AzureRmAlertRule -ResourceGroup montest
```

Obter todas as regras de alerta definido para um recurso de destino. Por exemplo, todas as regras de alerta definido numa VM.

```PowerShell
Get-AzureRmAlertRule -ResourceGroup montest -TargetResourceId /subscriptions/s1/resourceGroups/montest/providers/Microsoft.Compute/virtualMachines/testconfig
```

`Get-AzureRmAlertRule`suporta outros parâmetros. Consulte [Get-AlertRule](https://msdn.microsoft.com/library/mt282459.aspx) para obter mais informações.

## <a name="create-metric-alerts"></a>Criar métricas alertas
Pode utilizar Olá `Add-AlertRule` cmdlet toocreate, atualizar ou desativar uma regra de alerta.

Pode criar propriedades de e-mail e webhook utilizando `New-AzureRmAlertRuleEmail` e `New-AzureRmAlertRuleWebhook`, respetivamente. Cmdlet de regra de alerta de Olá, atribuir estes como ações toohello **ações** propriedade Olá regra de alerta.

Olá, a tabela seguinte descreve Olá parâmetros e valores utilizado toocreate um alerta utilizando uma métrica.

| Parâmetro | valor |
| --- | --- |
| Nome |simpletestdiskwrite |
| Localização desta regra de alerta |EUA Leste |
| ResourceGroup |montest |
| TargetResourceId |/subscriptions/S1/resourceGroups/montest/Providers/Microsoft.Compute/virtualMachines/testconfig |
| MetricName de alerta de Olá que é criada |\PhysicalDisk ( total) \Disk escritas/seg. Consulte Olá `Get-MetricDefinitions` cmdlet sobre como tooretrieve Olá exatos nomes métricos |
| operador |GreaterThan |
| Valor de limiar (contagem por segundo para esta métrica) |1 |
| WindowSize (formato hh: mm:) |00:05:00 |
| agregador (estatística de métrica de Olá, que utiliza a contagem média, neste caso) |Média |
| mensagens de correio eletrónico personalizadas (matriz de cadeia) |'foo@example.com','bar@example.com' |
| Enviar tooowners de e-mail, contribuintes e leitores |-SendToServiceOwners |

Criar uma ação de E-Mail

```PowerShell
$actionEmail = New-AzureRmAlertRuleEmail -CustomEmail myname@company.com
```

Criar uma ação do Webhook

```PowerShell
$actionWebhook = New-AzureRmAlertRuleWebhook -ServiceUri https://example.com?token=mytoken
```

Criar regra de alerta de Olá no métrica de % de CPU Olá numa VM clássica

```PowerShell
Add-AzureRmMetricAlertRule -Name vmcpu_gt_1 -Location "East US" -ResourceGroup myrg1 -TargetResourceId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.ClassicCompute/virtualMachines/my_vm1 -MetricName "Percentage CPU" -Operator GreaterThan -Threshold 1 -WindowSize 00:05:00 -TimeAggregationOperator Average -Actions $actionEmail, $actionWebhook -Description "alert on CPU > 1%"
```

Obter regra de alerta de Olá

```PowerShell
Get-AzureRmAlertRule -Name vmcpu_gt_1 -ResourceGroup myrg1 -DetailedOutput
```

Olá Adicionar alerta cmdlet também atualiza a regra de Olá se já existe uma regra de alerta para Olá fornecido propriedades. toodisable uma regra de alerta, inclua o parâmetro de Olá **- DisableRule**.

## <a name="get-a-list-of-available-metrics-for-alerts"></a>Obter uma lista de métricas disponíveis para os alertas
Pode utilizar Olá `Get-AzureRmMetricDefinition` lista de Olá tooview cmdlet de todas as métricas para um recurso específico.

```PowerShell
Get-AzureRmMetricDefinition -ResourceId <resource_id>
```

Olá exemplo seguinte gera uma tabela com o nome de métrica de Olá e Olá unidade para o mesmo.

```PowerShell
Get-AzureRmMetricDefinition -ResourceId <resource_id> | Format-Table -Property Name,Unit
```

Uma lista completa das opções disponíveis para `Get-AzureRmMetricDefinition` está disponível em [Get-MetricDefinitions](https://msdn.microsoft.com/library/mt282458.aspx).

## <a name="create-and-manage-autoscale-settings"></a>Criar e gerir definições de dimensionamento automático
Um recurso, tal como uma aplicação Web, VM, o serviço em nuvem ou o conjunto de dimensionamento da Máquina Virtual pode ter apenas uma definição de dimensionamento automático configurada para ele.
No entanto, cada definição de dimensionamento automático pode ter vários perfis. Por exemplo, um para um perfil de escala com base no desempenho e um segundo para um perfil com base na agenda. Cada perfil pode ter várias regras configuradas no mesmo. Para mais informações sobre o dimensionamento automático, consulte [como tooAutoscale uma aplicação](../cloud-services/cloud-services-how-to-scale.md).

Eis os passos de Olá que iremos utilizar:

1. Crie Regra (s).
2. Criar perfis Olá mapeamento regras que criou anteriormente toohello perfis.
3. Opcional: Crie as notificações de dimensionamento automático ao configurar propriedades de webhook e e-mail.
4. Crie uma definição de dimensionamento automático com um nome de recurso de destino Olá mediante o mapeamento de perfis de Olá e as notificações que criou nos passos anteriores Olá.

Olá exemplos seguintes mostram como pode criar uma definição de dimensionamento automático para um conjunto de dimensionamento de Máquina Virtual para um sistema operativo do Windows com base através da utilização de métrica de utilização de Olá da CPU.

Em primeiro lugar, crie um regra tooscale escalamento, com um aumento da contagem de instâncias.

```PowerShell
$rule1 = New-AzureRmAutoscaleRule -MetricName "Percentage CPU" -MetricResourceId /subscriptions/s1/resourceGroups/big2/providers/Microsoft.Compute/virtualMachineScaleSets/big2 -Operator GreaterThan -MetricStatistic Average -Threshold 60 -TimeGrain 00:01:00 -TimeWindow 00:10:00 -ScaleActionCooldown 00:10:00 -ScaleActionDirection Increase -ScaleActionValue 1
```        

Em seguida, crie uma regra tooscale-in, com um diminuir de contagem de instâncias.

```PowerShell
$rule2 = New-AzureRmAutoscaleRule -MetricName "Percentage CPU" -MetricResourceId /subscriptions/s1/resourceGroups/big2/providers/Microsoft.Compute/virtualMachineScaleSets/big2 -Operator GreaterThan -MetricStatistic Average -Threshold 30 -TimeGrain 00:01:00 -TimeWindow 00:10:00 -ScaleActionCooldown 00:10:00 -ScaleActionDirection Decrease -ScaleActionValue 1
```

Em seguida, crie um perfil para regras de Olá.

```PowerShell
$profile1 = New-AzureRmAutoscaleProfile -DefaultCapacity 2 -MaximumCapacity 10 -MinimumCapacity 2 -Rules $rule1,$rule2 -Name "My_Profile"
```

Crie uma propriedade do webhook.

```PowerShell
$webhook_scale = New-AzureRmAutoscaleWebhook -ServiceUri "https://example.com?mytoken=mytokenvalue"
```

Criar notificação de Olá propriedade para a definição de dimensionamento automático de Olá, incluindo e-mail e Olá webhook que criou anteriormente.

```PowerShell
$notification1= New-AzureRmAutoscaleNotification -CustomEmails ashwink@microsoft.com -SendEmailToSubscriptionAdministrators SendEmailToSubscriptionCoAdministrators -Webhooks $webhook_scale
```

Por fim, crie Olá dimensionamento automático definição tooadd Olá perfil que criou acima.

```PowerShell
Add-AzureRmAutoscaleSetting -Location "East US" -Name "MyScaleVMSSSetting" -ResourceGroup big2 -TargetResourceId /subscriptions/s1/resourceGroups/big2/providers/Microsoft.Compute/virtualMachineScaleSets/big2 -AutoscaleProfiles $profile1 -Notifications $notification1
```

Para obter mais informações sobre a gestão de definições de dimensionamento automático, consulte [Get-AutoscaleSetting](https://msdn.microsoft.com/library/mt282461.aspx).

## <a name="autoscale-history"></a>Histórico de dimensionamento automático
Olá exemplo seguinte mostra como pode ver eventos de dimensionamento automático e alerta recentes. Utilize o histórico de dimensionamento automático ao hello do tooview de pesquisa Olá atividade registos.

```PowerShell
Get-AzureRmLog -Caller "Microsoft.Insights/autoscaleSettings" -DetailedOutput -StartTime 2015-03-01
```

Pode utilizar Olá `Get-AzureRmAutoScaleHistory` cmdlet tooretrieve histórico de dimensionamento automático.

```PowerShell
Get-AzureRmAutoScaleHistory -ResourceId /subscriptions/s1/resourceGroups/myrg1/providers/microsoft.insights/autoscalesettings/myScaleSetting -StartTime 2016-03-15 -DetailedOutput
```

Para obter mais informações, consulte [Get-AutoscaleHistory](https://msdn.microsoft.com/library/mt282464.aspx).

### <a name="view-details-for-an-autoscale-setting"></a>Ver detalhes de uma definição de dimensionamento automático
Pode utilizar Olá `Get-Autoscalesetting` cmdlet tooretrieve mais informações sobre a definição de dimensionamento automático de Olá.

Olá exemplo seguinte mostra os detalhes sobre todas as definições de dimensionamento automático no grupo de recursos de Olá 'myrg1'.

```PowerShell
Get-AzureRmAutoscalesetting -ResourceGroup myrg1 -DetailedOutput
```

Olá exemplo seguinte mostra os detalhes sobre todas as definições de dimensionamento automático no grupo de recursos de Olá 'myrg1' e especificamente Olá com o nome 'MyScaleVMSSSetting' de definição de dimensionamento automático.

```PowerShell
Get-AzureRmAutoscalesetting -ResourceGroup myrg1 -Name MyScaleVMSSSetting -DetailedOutput
```

### <a name="remove-an-autoscale-setting"></a>Remover uma definição de dimensionamento automático
Pode utilizar Olá `Remove-Autoscalesetting` cmdlet toodelete uma definição de dimensionamento automático.

```PowerShell
Remove-AzureRmAutoscalesetting -ResourceGroup myrg1 -Name MyScaleVMSSSetting
```

## <a name="manage-log-profiles-for-activity-log"></a>Gerir perfis de registo para o registo de atividade
Pode criar um *registo perfil* e exportar dados da sua conta de armazenamento de tooa de registo de atividade e podem configurar a retenção de dados para o mesmo. Opcionalmente, também pode transmitir Olá dados tooyour Hub de eventos. Tenha em atenção que esta funcionalidade está atualmente em pré-visualização e só pode criar um perfil de registo por subscrição. Pode utilizar os seguintes cmdlets com a sua atual toocreate de subscrição de Olá e gerir perfis de registo. Também pode escolher uma determinada subscrição. Embora PowerShell predefinições subscrição atual toohello, pode sempre alterar esse utilizando `Set-AzureRmContext`. Pode configurar a conta de armazenamento de atividade registo tooroute dados tooany ou Hub de eventos dentro dessa subscrição. Dados são escritos como ficheiros do blob no formato JSON.

### <a name="get-a-log-profile"></a>Obter um perfil de registo
toofetch os perfis de registo existente, utilize Olá `Get-AzureRmLogProfile` cmdlet.

### <a name="add-a-log-profile-without-data-retention"></a>Adicionar um perfil de registo sem retenção de dados
```PowerShell
Add-AzureRmLogProfile -Name my_log_profile_s1 -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage -Locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia
```

### <a name="remove-a-log-profile"></a>Remover um perfil de registo
```PowerShell
Remove-AzureRmLogProfile -name my_log_profile_s1
```

### <a name="add-a-log-profile-with-data-retention"></a>Adicionar um perfil de registo com retenção de dados
Pode especificar Olá **- RetentionInDays** propriedade com Olá número de dias, como um número inteiro positivo, onde os dados de Olá são mantidos.

```PowerShell
Add-AzureRmLogProfile -Name my_log_profile_s1 -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage -Locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia -RetentionInDays 90
```

### <a name="add-log-profile-with-retention-and-eventhub"></a>Adicionar perfil de registo com retenção e EventHub
Na adição toorouting a conta de toostorage de dados, pode também ser transmitido em fluxo-tooan Hub de eventos. Tenha em atenção que nesta pré-visualização a configuração de conta de armazenamento de versão e Olá é obrigatória, mas a configuração do Hub de eventos é opcional.

```PowerShell
Add-AzureRmLogProfile -Name my_log_profile_s1 -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage -serviceBusRuleId /subscriptions/s1/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/mytestSB/authorizationrules/RootManageSharedAccessKey -Locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia -RetentionInDays 90
```

## <a name="configure-diagnostics-logs"></a>Configurar os registos de diagnóstico
Muitos serviços do Azure fornecem registos adicionais e telemetria que pode ser dados toosave configurada na sua conta do Storage do Azure, enviar tooEvent Hubs e/ou enviados tooan área de trabalho de análise de registos do OMS. Essa operação só pode ser efetuada num nível de recursos e concentrador de conta ou evento de armazenamento de Olá deve estar presente no Olá mesma região que o recurso de destino olá onde a definição de diagnóstico de Olá está configurada.

### <a name="get-diagnostic-setting"></a>Obter a definição de diagnóstico
```PowerShell
Get-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Logic/workflows/andy0315logicapp
```

Desativar a definição de diagnóstico

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Logic/workflows/andy0315logicapp -StorageAccountId /subscriptions/s1/resourceGroups/Default-Storage-WestUS/providers/Microsoft.Storage/storageAccounts/mystorageaccount -Enable $false
```

Ativar a definição de diagnóstico sem retenção

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Logic/workflows/andy0315logicapp -StorageAccountId /subscriptions/s1/resourceGroups/Default-Storage-WestUS/providers/Microsoft.Storage/storageAccounts/mystorageaccount -Enable $true
```

Ativar a definição de diagnóstico com retenção

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Logic/workflows/andy0315logicapp -StorageAccountId /subscriptions/s1/resourceGroups/Default-Storage-WestUS/providers/Microsoft.Storage/storageAccounts/mystorageaccount -Enable $true -RetentionEnabled $true -RetentionInDays 90
```

Ativar a definição de diagnóstico com o período de retenção para uma categoria de registo específico

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/insights-integration/providers/Microsoft.Network/networkSecurityGroups/viruela1 -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/sakteststorage -Categories NetworkSecurityGroupEvent -Enable $true -RetentionEnabled $true -RetentionInDays 90
```

Ativar a definição de diagnóstico para os Event Hubs

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/insights-integration/providers/Microsoft.Network/networkSecurityGroups/viruela1 -serviceBusRuleId /subscriptions/s1/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/mytestSB/authorizationrules/RootManageSharedAccessKey -Enable $true
```

Ativar a definição de diagnóstico para OMS

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/insights-integration/providers/Microsoft.Network/networkSecurityGroups/viruela1 -WorkspaceId 76d785fd-d1ce-4f50-8ca3-858fc819ca0f -Enabled $true

```
