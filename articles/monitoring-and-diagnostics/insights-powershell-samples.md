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
# <a name="azure-monitor-powershell-quick-start-samples"></a><span data-ttu-id="29e7f-104">Exemplos de início rápido do Azure PowerShell de Monitor</span><span class="sxs-lookup"><span data-stu-id="29e7f-104">Azure Monitor PowerShell quick start samples</span></span>
<span data-ttu-id="29e7f-105">Este artigo apresenta o exemplo toohelp de comandos do PowerShell que aceder às funcionalidades de monitorização do Azure.</span><span class="sxs-lookup"><span data-stu-id="29e7f-105">This article shows you sample PowerShell commands toohelp you access Azure Monitor features.</span></span> <span data-ttu-id="29e7f-106">Monitor do Azure permite-lhe tooAutoScale serviços em nuvem, as máquinas virtuais e aplicações Web e toosend as notificações de alerta ou chamada web URLs com base nos valores de dados de telemetria configurado.</span><span class="sxs-lookup"><span data-stu-id="29e7f-106">Azure Monitor allows you tooAutoScale Cloud Services, Virtual Machines, and Web Apps and toosend alert notifications or call web URLs based on values of configured telemetry data.</span></span>

> [!NOTE]
> <span data-ttu-id="29e7f-107">Monitor do Azure é o nome novo Olá que foi chamado "Informações do Azure" até 25th de Setembro de 2016.</span><span class="sxs-lookup"><span data-stu-id="29e7f-107">Azure Monitor is hello new name for what was called "Azure Insights" until Sept 25th, 2016.</span></span> <span data-ttu-id="29e7f-108">No entanto, Olá espaços de nomes e, consequentemente, Olá os seguintes comandos ainda contenham insights"Olá".</span><span class="sxs-lookup"><span data-stu-id="29e7f-108">However, hello namespaces and thus hello following commands still contain hello "insights".</span></span>
> 
> 

## <a name="set-up-powershell"></a><span data-ttu-id="29e7f-109">Configurar o PowerShell</span><span class="sxs-lookup"><span data-stu-id="29e7f-109">Set up PowerShell</span></span>
<span data-ttu-id="29e7f-110">Se ainda não o tiver feito, configure toorun PowerShell no seu computador.</span><span class="sxs-lookup"><span data-stu-id="29e7f-110">If you haven't already, set up PowerShell toorun on your computer.</span></span> <span data-ttu-id="29e7f-111">Para obter mais informações, consulte [como tooInstall e configurar o PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="29e7f-111">For more information, see [How tooInstall and Configure PowerShell](/powershell/azure/overview).</span></span>

## <a name="examples-in-this-article"></a><span data-ttu-id="29e7f-112">Exemplos neste artigo</span><span class="sxs-lookup"><span data-stu-id="29e7f-112">Examples in this article</span></span>
<span data-ttu-id="29e7f-113">Exemplos de Olá artigo Olá mostram como pode utilizar os cmdlets de Monitor do Azure.</span><span class="sxs-lookup"><span data-stu-id="29e7f-113">hello examples in hello article illustrate how you can use Azure Monitor cmdlets.</span></span> <span data-ttu-id="29e7f-114">Também pode rever a lista completa de Olá Azure Monitor de cmdlets do PowerShell em [Cmdlets de Monitor do Azure (Insights)](https://msdn.microsoft.com/library/azure/mt282452#40v=azure.200#41.aspx).</span><span class="sxs-lookup"><span data-stu-id="29e7f-114">You can also review hello entire list of Azure Monitor PowerShell cmdlets at [Azure Monitor (Insights) Cmdlets](https://msdn.microsoft.com/library/azure/mt282452#40v=azure.200#41.aspx).</span></span>

## <a name="sign-in-and-use-subscriptions"></a><span data-ttu-id="29e7f-115">A iniciar sessão e utilizar subscrições</span><span class="sxs-lookup"><span data-stu-id="29e7f-115">Sign in and use subscriptions</span></span>
<span data-ttu-id="29e7f-116">Em primeiro lugar, inicie sessão no tooyour subscrição do Azure.</span><span class="sxs-lookup"><span data-stu-id="29e7f-116">First, log in tooyour Azure subscription.</span></span>

```PowerShell
Login-AzureRmAccount
```

<span data-ttu-id="29e7f-117">Isto requer toosign no.</span><span class="sxs-lookup"><span data-stu-id="29e7f-117">This requires you toosign in.</span></span> <span data-ttu-id="29e7f-118">Quando o fizer, a conta, são apresentadas TenantID e ID de subscrição predefinido.</span><span class="sxs-lookup"><span data-stu-id="29e7f-118">Once you do, your Account, TenantID and default Subscription ID are displayed.</span></span> <span data-ttu-id="29e7f-119">Olá todos os cmdlets do Azure de trabalho no contexto de Olá da sua subscrição predefinida.</span><span class="sxs-lookup"><span data-stu-id="29e7f-119">All hello Azure cmdlets work in hello context of your default subscription.</span></span> <span data-ttu-id="29e7f-120">lista de Olá tooview de subscrições tem acesso a, utilize Olá os seguintes comandos.</span><span class="sxs-lookup"><span data-stu-id="29e7f-120">tooview hello list of subscriptions you have access to, use hello following command.</span></span>

```PowerShell
Get-AzureRmSubscription
```

<span data-ttu-id="29e7f-121">toochange a trabalho contexto tooa subscrição diferente, Olá utilize os seguintes comandos.</span><span class="sxs-lookup"><span data-stu-id="29e7f-121">toochange your working context tooa different subscription, use hello following command.</span></span>

```PowerShell
Set-AzureRmContext -SubscriptionId <subscriptionid>
```


## <a name="retrieve-activity-log-for-a-subscription"></a><span data-ttu-id="29e7f-122">Obter o registo de atividade para uma subscrição</span><span class="sxs-lookup"><span data-stu-id="29e7f-122">Retrieve Activity log for a subscription</span></span>
<span data-ttu-id="29e7f-123">Olá utilize `Get-AzureRmLog` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="29e7f-123">Use hello `Get-AzureRmLog` cmdlet.</span></span>  <span data-ttu-id="29e7f-124">Olá seguem-se alguns exemplos comuns.</span><span class="sxs-lookup"><span data-stu-id="29e7f-124">hello following are some common examples.</span></span>

<span data-ttu-id="29e7f-125">Obter entradas de registo a partir deste toopresent de data/hora:</span><span class="sxs-lookup"><span data-stu-id="29e7f-125">Get log entries from this time/date toopresent:</span></span>

```PowerShell
Get-AzureRmLog -StartTime 2016-03-01T10:30
```

<span data-ttu-id="29e7f-126">Obter entradas de registo entre um intervalo de data/hora:</span><span class="sxs-lookup"><span data-stu-id="29e7f-126">Get log entries between a time/date range:</span></span>

```PowerShell
Get-AzureRmLog -StartTime 2015-01-01T10:30 -EndTime 2015-01-01T11:30
```

<span data-ttu-id="29e7f-127">Obter entradas de registo de um grupo de recurso específico:</span><span class="sxs-lookup"><span data-stu-id="29e7f-127">Get log entries from a specific resource group:</span></span>

```PowerShell
Get-AzureRmLog -ResourceGroup 'myrg1'
```

<span data-ttu-id="29e7f-128">Obter entradas de registo a partir de um fornecedor de recursos específico entre um intervalo de data/hora:</span><span class="sxs-lookup"><span data-stu-id="29e7f-128">Get log entries from a specific resource provider between a time/date range:</span></span>

```PowerShell
Get-AzureRmLog -ResourceProvider 'Microsoft.Web' -StartTime 2015-01-01T10:30 -EndTime 2015-01-01T11:30
```

<span data-ttu-id="29e7f-129">Obter todas as entradas de registo com um emissor específico:</span><span class="sxs-lookup"><span data-stu-id="29e7f-129">Get all log entries with a specific caller:</span></span>

```PowerShell
Get-AzureRmLog -Caller 'myname@company.com'
```

<span data-ttu-id="29e7f-130">Olá comando obtém Olá últimas 1 000 eventos de registo de atividade Olá os seguintes:</span><span class="sxs-lookup"><span data-stu-id="29e7f-130">hello following command retrieves hello last 1000 events from hello activity log:</span></span>

```PowerShell
Get-AzureRmLog -MaxEvents 1000
```

<span data-ttu-id="29e7f-131">`Get-AzureRmLog`suporta muitos outros parâmetros.</span><span class="sxs-lookup"><span data-stu-id="29e7f-131">`Get-AzureRmLog` supports many other parameters.</span></span> <span data-ttu-id="29e7f-132">Consulte Olá `Get-AzureRmLog` referência para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="29e7f-132">See hello `Get-AzureRmLog` reference for more information.</span></span>

> [!NOTE]
> <span data-ttu-id="29e7f-133">`Get-AzureRmLog`Fornece apenas 15 dias do histórico.</span><span class="sxs-lookup"><span data-stu-id="29e7f-133">`Get-AzureRmLog` only provides 15 days of history.</span></span> <span data-ttu-id="29e7f-134">Utilizar Olá **- MaxEvents** parâmetro permite-lhe tooquery Olá últimas N eventos, para além de 15 dias.</span><span class="sxs-lookup"><span data-stu-id="29e7f-134">Using hello **-MaxEvents** parameter allows you tooquery hello last N events, beyond 15 days.</span></span> <span data-ttu-id="29e7f-135">tooaccess eventos com mais de 15 dias, utilize Olá REST API ou o SDK (c# exemplo com Olá SDK).</span><span class="sxs-lookup"><span data-stu-id="29e7f-135">tooaccess events older than 15 days, use hello REST API or SDK (C# sample using hello SDK).</span></span> <span data-ttu-id="29e7f-136">Se não incluir **StartTime**, em seguida, o valor predefinido de Olá é **EndTime** menos uma hora.</span><span class="sxs-lookup"><span data-stu-id="29e7f-136">If you do not include **StartTime**, then hello default value is **EndTime** minus one hour.</span></span> <span data-ttu-id="29e7f-137">Se não incluir **EndTime**, em seguida, o valor predefinido de Olá é o tempo atual.</span><span class="sxs-lookup"><span data-stu-id="29e7f-137">If you do not include **EndTime**, then hello default value is current time.</span></span> <span data-ttu-id="29e7f-138">Todas as horas são em UTC.</span><span class="sxs-lookup"><span data-stu-id="29e7f-138">All times are in UTC.</span></span>
> 
> 

## <a name="retrieve-alerts-history"></a><span data-ttu-id="29e7f-139">Obter o histórico de alertas</span><span class="sxs-lookup"><span data-stu-id="29e7f-139">Retrieve alerts history</span></span>
<span data-ttu-id="29e7f-140">tooview alerta todos os eventos, pode consultar Olá registos do Azure Resource Manager utilizando Olá exemplos a seguir.</span><span class="sxs-lookup"><span data-stu-id="29e7f-140">tooview all alert events, you can query hello Azure Resource Manager logs using hello following examples.</span></span>

```PowerShell
Get-AzureRmLog -Caller "Microsoft.Insights/alertRules" -DetailedOutput -StartTime 2015-03-01
```

<span data-ttu-id="29e7f-141">histórico de Olá tooview para um alerta específico da regra, pode utilizar Olá `Get-AzureRmAlertHistory` cmdlet, passando na ID de recurso Olá Olá de regra de alerta.</span><span class="sxs-lookup"><span data-stu-id="29e7f-141">tooview hello history for a specific alert rule, you can use hello `Get-AzureRmAlertHistory` cmdlet, passing in hello resource ID of hello alert rule.</span></span>

```PowerShell
Get-AzureRmAlertHistory -ResourceId /subscriptions/s1/resourceGroups/rg1/providers/microsoft.insights/alertrules/myalert -StartTime 2016-03-1 -Status Activated
```

<span data-ttu-id="29e7f-142">Olá `Get-AzureRmAlertHistory` cmdlet suporta vários parâmetros.</span><span class="sxs-lookup"><span data-stu-id="29e7f-142">hello `Get-AzureRmAlertHistory` cmdlet supports various parameters.</span></span> <span data-ttu-id="29e7f-143">Obter mais informações, consulte [Get-AlertHistory](https://msdn.microsoft.com/library/mt282453.aspx).</span><span class="sxs-lookup"><span data-stu-id="29e7f-143">More information, see [Get-AlertHistory](https://msdn.microsoft.com/library/mt282453.aspx).</span></span>

## <a name="retrieve-information-on-alert-rules"></a><span data-ttu-id="29e7f-144">Obter informações sobre regras de alertas</span><span class="sxs-lookup"><span data-stu-id="29e7f-144">Retrieve information on alert rules</span></span>
<span data-ttu-id="29e7f-145">Todos os seguintes comandos de Olá agirem sobre um grupo de recursos com o nome "montest".</span><span class="sxs-lookup"><span data-stu-id="29e7f-145">All of hello following commands act on a Resource Group named "montest".</span></span>

<span data-ttu-id="29e7f-146">Ver todas as propriedades de Olá Olá de regra de alerta:</span><span class="sxs-lookup"><span data-stu-id="29e7f-146">View all hello properties of hello alert rule:</span></span>

```PowerShell
Get-AzureRmAlertRule -Name simpletestCPU -ResourceGroup montest -DetailedOutput
```

<span data-ttu-id="29e7f-147">Obter todos os alertas no grupo de recursos:</span><span class="sxs-lookup"><span data-stu-id="29e7f-147">Retrieve all alerts on a resource group:</span></span>

```PowerShell
Get-AzureRmAlertRule -ResourceGroup montest
```

<span data-ttu-id="29e7f-148">Obter todas as regras de alerta definido para um recurso de destino.</span><span class="sxs-lookup"><span data-stu-id="29e7f-148">Retrieve all alert rules set for a target resource.</span></span> <span data-ttu-id="29e7f-149">Por exemplo, todas as regras de alerta definido numa VM.</span><span class="sxs-lookup"><span data-stu-id="29e7f-149">For example, all alert rules set on a VM.</span></span>

```PowerShell
Get-AzureRmAlertRule -ResourceGroup montest -TargetResourceId /subscriptions/s1/resourceGroups/montest/providers/Microsoft.Compute/virtualMachines/testconfig
```

<span data-ttu-id="29e7f-150">`Get-AzureRmAlertRule`suporta outros parâmetros.</span><span class="sxs-lookup"><span data-stu-id="29e7f-150">`Get-AzureRmAlertRule` supports other parameters.</span></span> <span data-ttu-id="29e7f-151">Consulte [Get-AlertRule](https://msdn.microsoft.com/library/mt282459.aspx) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="29e7f-151">See [Get-AlertRule](https://msdn.microsoft.com/library/mt282459.aspx) for more information.</span></span>

## <a name="create-metric-alerts"></a><span data-ttu-id="29e7f-152">Criar métricas alertas</span><span class="sxs-lookup"><span data-stu-id="29e7f-152">Create metric alerts</span></span>
<span data-ttu-id="29e7f-153">Pode utilizar Olá `Add-AlertRule` cmdlet toocreate, atualizar ou desativar uma regra de alerta.</span><span class="sxs-lookup"><span data-stu-id="29e7f-153">You can use hello `Add-AlertRule` cmdlet toocreate, update or disable an alert rule.</span></span>

<span data-ttu-id="29e7f-154">Pode criar propriedades de e-mail e webhook utilizando `New-AzureRmAlertRuleEmail` e `New-AzureRmAlertRuleWebhook`, respetivamente.</span><span class="sxs-lookup"><span data-stu-id="29e7f-154">You can create email and webhook properties using  `New-AzureRmAlertRuleEmail` and `New-AzureRmAlertRuleWebhook`, respectively.</span></span> <span data-ttu-id="29e7f-155">Cmdlet de regra de alerta de Olá, atribuir estes como ações toohello **ações** propriedade Olá regra de alerta.</span><span class="sxs-lookup"><span data-stu-id="29e7f-155">In hello Alert rule cmdlet, assign these as actions toohello **Actions** property of hello Alert Rule.</span></span>

<span data-ttu-id="29e7f-156">Olá, a tabela seguinte descreve Olá parâmetros e valores utilizado toocreate um alerta utilizando uma métrica.</span><span class="sxs-lookup"><span data-stu-id="29e7f-156">hello following table describes hello parameters and values used toocreate an alert using a metric.</span></span>

| <span data-ttu-id="29e7f-157">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="29e7f-157">parameter</span></span> | <span data-ttu-id="29e7f-158">valor</span><span class="sxs-lookup"><span data-stu-id="29e7f-158">value</span></span> |
| --- | --- |
| <span data-ttu-id="29e7f-159">Nome</span><span class="sxs-lookup"><span data-stu-id="29e7f-159">Name</span></span> |<span data-ttu-id="29e7f-160">simpletestdiskwrite</span><span class="sxs-lookup"><span data-stu-id="29e7f-160">simpletestdiskwrite</span></span> |
| <span data-ttu-id="29e7f-161">Localização desta regra de alerta</span><span class="sxs-lookup"><span data-stu-id="29e7f-161">Location of this alert rule</span></span> |<span data-ttu-id="29e7f-162">EUA Leste</span><span class="sxs-lookup"><span data-stu-id="29e7f-162">East US</span></span> |
| <span data-ttu-id="29e7f-163">ResourceGroup</span><span class="sxs-lookup"><span data-stu-id="29e7f-163">ResourceGroup</span></span> |<span data-ttu-id="29e7f-164">montest</span><span class="sxs-lookup"><span data-stu-id="29e7f-164">montest</span></span> |
| <span data-ttu-id="29e7f-165">TargetResourceId</span><span class="sxs-lookup"><span data-stu-id="29e7f-165">TargetResourceId</span></span> |<span data-ttu-id="29e7f-166">/subscriptions/S1/resourceGroups/montest/Providers/Microsoft.Compute/virtualMachines/testconfig</span><span class="sxs-lookup"><span data-stu-id="29e7f-166">/subscriptions/s1/resourceGroups/montest/providers/Microsoft.Compute/virtualMachines/testconfig</span></span> |
| <span data-ttu-id="29e7f-167">MetricName de alerta de Olá que é criada</span><span class="sxs-lookup"><span data-stu-id="29e7f-167">MetricName of hello alert that is created</span></span> |<span data-ttu-id="29e7f-168">\PhysicalDisk ( total) \Disk escritas/seg. Consulte Olá `Get-MetricDefinitions` cmdlet sobre como tooretrieve Olá exatos nomes métricos</span><span class="sxs-lookup"><span data-stu-id="29e7f-168">\PhysicalDisk(_Total)\Disk Writes/sec. See hello `Get-MetricDefinitions` cmdlet about how tooretrieve hello exact metric names</span></span> |
| <span data-ttu-id="29e7f-169">operador</span><span class="sxs-lookup"><span data-stu-id="29e7f-169">operator</span></span> |<span data-ttu-id="29e7f-170">GreaterThan</span><span class="sxs-lookup"><span data-stu-id="29e7f-170">GreaterThan</span></span> |
| <span data-ttu-id="29e7f-171">Valor de limiar (contagem por segundo para esta métrica)</span><span class="sxs-lookup"><span data-stu-id="29e7f-171">Threshold value (count/sec in for this metric)</span></span> |<span data-ttu-id="29e7f-172">1</span><span class="sxs-lookup"><span data-stu-id="29e7f-172">1</span></span> |
| <span data-ttu-id="29e7f-173">WindowSize (formato hh: mm:)</span><span class="sxs-lookup"><span data-stu-id="29e7f-173">WindowSize (hh:mm:ss format)</span></span> |<span data-ttu-id="29e7f-174">00:05:00</span><span class="sxs-lookup"><span data-stu-id="29e7f-174">00:05:00</span></span> |
| <span data-ttu-id="29e7f-175">agregador (estatística de métrica de Olá, que utiliza a contagem média, neste caso)</span><span class="sxs-lookup"><span data-stu-id="29e7f-175">aggregator (statistic of hello metric, which uses Average count, in this case)</span></span> |<span data-ttu-id="29e7f-176">Média</span><span class="sxs-lookup"><span data-stu-id="29e7f-176">Average</span></span> |
| <span data-ttu-id="29e7f-177">mensagens de correio eletrónico personalizadas (matriz de cadeia)</span><span class="sxs-lookup"><span data-stu-id="29e7f-177">custom emails (string array)</span></span> |<span data-ttu-id="29e7f-178">'foo@example.com','bar@example.com'</span><span class="sxs-lookup"><span data-stu-id="29e7f-178">'foo@example.com','bar@example.com'</span></span> |
| <span data-ttu-id="29e7f-179">Enviar tooowners de e-mail, contribuintes e leitores</span><span class="sxs-lookup"><span data-stu-id="29e7f-179">send email tooowners, contributors and readers</span></span> |<span data-ttu-id="29e7f-180">-SendToServiceOwners</span><span class="sxs-lookup"><span data-stu-id="29e7f-180">-SendToServiceOwners</span></span> |

<span data-ttu-id="29e7f-181">Criar uma ação de E-Mail</span><span class="sxs-lookup"><span data-stu-id="29e7f-181">Create an Email action</span></span>

```PowerShell
$actionEmail = New-AzureRmAlertRuleEmail -CustomEmail myname@company.com
```

<span data-ttu-id="29e7f-182">Criar uma ação do Webhook</span><span class="sxs-lookup"><span data-stu-id="29e7f-182">Create a Webhook action</span></span>

```PowerShell
$actionWebhook = New-AzureRmAlertRuleWebhook -ServiceUri https://example.com?token=mytoken
```

<span data-ttu-id="29e7f-183">Criar regra de alerta de Olá no métrica de % de CPU Olá numa VM clássica</span><span class="sxs-lookup"><span data-stu-id="29e7f-183">Create hello alert rule on hello CPU% metric on a classic VM</span></span>

```PowerShell
Add-AzureRmMetricAlertRule -Name vmcpu_gt_1 -Location "East US" -ResourceGroup myrg1 -TargetResourceId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.ClassicCompute/virtualMachines/my_vm1 -MetricName "Percentage CPU" -Operator GreaterThan -Threshold 1 -WindowSize 00:05:00 -TimeAggregationOperator Average -Actions $actionEmail, $actionWebhook -Description "alert on CPU > 1%"
```

<span data-ttu-id="29e7f-184">Obter regra de alerta de Olá</span><span class="sxs-lookup"><span data-stu-id="29e7f-184">Retrieve hello alert rule</span></span>

```PowerShell
Get-AzureRmAlertRule -Name vmcpu_gt_1 -ResourceGroup myrg1 -DetailedOutput
```

<span data-ttu-id="29e7f-185">Olá Adicionar alerta cmdlet também atualiza a regra de Olá se já existe uma regra de alerta para Olá fornecido propriedades.</span><span class="sxs-lookup"><span data-stu-id="29e7f-185">hello Add alert cmdlet also updates hello rule if an alert rule already exists for hello given properties.</span></span> <span data-ttu-id="29e7f-186">toodisable uma regra de alerta, inclua o parâmetro de Olá **- DisableRule**.</span><span class="sxs-lookup"><span data-stu-id="29e7f-186">toodisable an alert rule, include hello parameter **-DisableRule**.</span></span>

## <a name="get-a-list-of-available-metrics-for-alerts"></a><span data-ttu-id="29e7f-187">Obter uma lista de métricas disponíveis para os alertas</span><span class="sxs-lookup"><span data-stu-id="29e7f-187">Get a list of available metrics for alerts</span></span>
<span data-ttu-id="29e7f-188">Pode utilizar Olá `Get-AzureRmMetricDefinition` lista de Olá tooview cmdlet de todas as métricas para um recurso específico.</span><span class="sxs-lookup"><span data-stu-id="29e7f-188">You can use hello `Get-AzureRmMetricDefinition` cmdlet tooview hello list of all metrics for a specific resource.</span></span>

```PowerShell
Get-AzureRmMetricDefinition -ResourceId <resource_id>
```

<span data-ttu-id="29e7f-189">Olá exemplo seguinte gera uma tabela com o nome de métrica de Olá e Olá unidade para o mesmo.</span><span class="sxs-lookup"><span data-stu-id="29e7f-189">hello following example generates a table with hello metric Name and hello Unit for it.</span></span>

```PowerShell
Get-AzureRmMetricDefinition -ResourceId <resource_id> | Format-Table -Property Name,Unit
```

<span data-ttu-id="29e7f-190">Uma lista completa das opções disponíveis para `Get-AzureRmMetricDefinition` está disponível em [Get-MetricDefinitions](https://msdn.microsoft.com/library/mt282458.aspx).</span><span class="sxs-lookup"><span data-stu-id="29e7f-190">A full list of available options for `Get-AzureRmMetricDefinition` is available at [Get-MetricDefinitions](https://msdn.microsoft.com/library/mt282458.aspx).</span></span>

## <a name="create-and-manage-autoscale-settings"></a><span data-ttu-id="29e7f-191">Criar e gerir definições de dimensionamento automático</span><span class="sxs-lookup"><span data-stu-id="29e7f-191">Create and manage AutoScale settings</span></span>
<span data-ttu-id="29e7f-192">Um recurso, tal como uma aplicação Web, VM, o serviço em nuvem ou o conjunto de dimensionamento da Máquina Virtual pode ter apenas uma definição de dimensionamento automático configurada para ele.</span><span class="sxs-lookup"><span data-stu-id="29e7f-192">A resource, such as a Web app, VM, Cloud Service or Virtual Machine Scale Set can have only one autoscale setting configured for it.</span></span>
<span data-ttu-id="29e7f-193">No entanto, cada definição de dimensionamento automático pode ter vários perfis.</span><span class="sxs-lookup"><span data-stu-id="29e7f-193">However, each autoscale setting can have multiple profiles.</span></span> <span data-ttu-id="29e7f-194">Por exemplo, um para um perfil de escala com base no desempenho e um segundo para um perfil com base na agenda.</span><span class="sxs-lookup"><span data-stu-id="29e7f-194">For example, one for a performance-based scale profile and a second one for a schedule-based profile.</span></span> <span data-ttu-id="29e7f-195">Cada perfil pode ter várias regras configuradas no mesmo.</span><span class="sxs-lookup"><span data-stu-id="29e7f-195">Each profile can have multiple rules configured on it.</span></span> <span data-ttu-id="29e7f-196">Para mais informações sobre o dimensionamento automático, consulte [como tooAutoscale uma aplicação](../cloud-services/cloud-services-how-to-scale.md).</span><span class="sxs-lookup"><span data-stu-id="29e7f-196">For more information about Autoscale, see [How tooAutoscale an Application](../cloud-services/cloud-services-how-to-scale.md).</span></span>

<span data-ttu-id="29e7f-197">Eis os passos de Olá que iremos utilizar:</span><span class="sxs-lookup"><span data-stu-id="29e7f-197">Here are hello steps we will use:</span></span>

1. <span data-ttu-id="29e7f-198">Crie Regra (s).</span><span class="sxs-lookup"><span data-stu-id="29e7f-198">Create rule(s).</span></span>
2. <span data-ttu-id="29e7f-199">Criar perfis Olá mapeamento regras que criou anteriormente toohello perfis.</span><span class="sxs-lookup"><span data-stu-id="29e7f-199">Create profile(s) mapping hello rules that you created previously toohello profiles.</span></span>
3. <span data-ttu-id="29e7f-200">Opcional: Crie as notificações de dimensionamento automático ao configurar propriedades de webhook e e-mail.</span><span class="sxs-lookup"><span data-stu-id="29e7f-200">Optional: Create notifications for autoscale by configuring webhook and email properties.</span></span>
4. <span data-ttu-id="29e7f-201">Crie uma definição de dimensionamento automático com um nome de recurso de destino Olá mediante o mapeamento de perfis de Olá e as notificações que criou nos passos anteriores Olá.</span><span class="sxs-lookup"><span data-stu-id="29e7f-201">Create an autoscale setting with a name on hello target resource by mapping hello profiles and notifications that you created in hello previous steps.</span></span>

<span data-ttu-id="29e7f-202">Olá exemplos seguintes mostram como pode criar uma definição de dimensionamento automático para um conjunto de dimensionamento de Máquina Virtual para um sistema operativo do Windows com base através da utilização de métrica de utilização de Olá da CPU.</span><span class="sxs-lookup"><span data-stu-id="29e7f-202">hello following examples show you how you can create an Autoscale setting for a Virtual Machine Scale Set for a Windows operating system based by using hello CPU utilization metric.</span></span>

<span data-ttu-id="29e7f-203">Em primeiro lugar, crie um regra tooscale escalamento, com um aumento da contagem de instâncias.</span><span class="sxs-lookup"><span data-stu-id="29e7f-203">First, create a rule tooscale-out, with an instance count increase.</span></span>

```PowerShell
$rule1 = New-AzureRmAutoscaleRule -MetricName "Percentage CPU" -MetricResourceId /subscriptions/s1/resourceGroups/big2/providers/Microsoft.Compute/virtualMachineScaleSets/big2 -Operator GreaterThan -MetricStatistic Average -Threshold 60 -TimeGrain 00:01:00 -TimeWindow 00:10:00 -ScaleActionCooldown 00:10:00 -ScaleActionDirection Increase -ScaleActionValue 1
```        

<span data-ttu-id="29e7f-204">Em seguida, crie uma regra tooscale-in, com um diminuir de contagem de instâncias.</span><span class="sxs-lookup"><span data-stu-id="29e7f-204">Next, create a rule tooscale-in, with an instance count decrease.</span></span>

```PowerShell
$rule2 = New-AzureRmAutoscaleRule -MetricName "Percentage CPU" -MetricResourceId /subscriptions/s1/resourceGroups/big2/providers/Microsoft.Compute/virtualMachineScaleSets/big2 -Operator GreaterThan -MetricStatistic Average -Threshold 30 -TimeGrain 00:01:00 -TimeWindow 00:10:00 -ScaleActionCooldown 00:10:00 -ScaleActionDirection Decrease -ScaleActionValue 1
```

<span data-ttu-id="29e7f-205">Em seguida, crie um perfil para regras de Olá.</span><span class="sxs-lookup"><span data-stu-id="29e7f-205">Then, create a profile for hello rules.</span></span>

```PowerShell
$profile1 = New-AzureRmAutoscaleProfile -DefaultCapacity 2 -MaximumCapacity 10 -MinimumCapacity 2 -Rules $rule1,$rule2 -Name "My_Profile"
```

<span data-ttu-id="29e7f-206">Crie uma propriedade do webhook.</span><span class="sxs-lookup"><span data-stu-id="29e7f-206">Create a webhook property.</span></span>

```PowerShell
$webhook_scale = New-AzureRmAutoscaleWebhook -ServiceUri "https://example.com?mytoken=mytokenvalue"
```

<span data-ttu-id="29e7f-207">Criar notificação de Olá propriedade para a definição de dimensionamento automático de Olá, incluindo e-mail e Olá webhook que criou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="29e7f-207">Create hello notification property for hello autoscale setting, including email and hello webhook that you created previously.</span></span>

```PowerShell
$notification1= New-AzureRmAutoscaleNotification -CustomEmails ashwink@microsoft.com -SendEmailToSubscriptionAdministrators SendEmailToSubscriptionCoAdministrators -Webhooks $webhook_scale
```

<span data-ttu-id="29e7f-208">Por fim, crie Olá dimensionamento automático definição tooadd Olá perfil que criou acima.</span><span class="sxs-lookup"><span data-stu-id="29e7f-208">Finally, create hello autoscale setting tooadd hello profile that you created above.</span></span>

```PowerShell
Add-AzureRmAutoscaleSetting -Location "East US" -Name "MyScaleVMSSSetting" -ResourceGroup big2 -TargetResourceId /subscriptions/s1/resourceGroups/big2/providers/Microsoft.Compute/virtualMachineScaleSets/big2 -AutoscaleProfiles $profile1 -Notifications $notification1
```

<span data-ttu-id="29e7f-209">Para obter mais informações sobre a gestão de definições de dimensionamento automático, consulte [Get-AutoscaleSetting](https://msdn.microsoft.com/library/mt282461.aspx).</span><span class="sxs-lookup"><span data-stu-id="29e7f-209">For more information about managing Autoscale settings, see [Get-AutoscaleSetting](https://msdn.microsoft.com/library/mt282461.aspx).</span></span>

## <a name="autoscale-history"></a><span data-ttu-id="29e7f-210">Histórico de dimensionamento automático</span><span class="sxs-lookup"><span data-stu-id="29e7f-210">Autoscale history</span></span>
<span data-ttu-id="29e7f-211">Olá exemplo seguinte mostra como pode ver eventos de dimensionamento automático e alerta recentes.</span><span class="sxs-lookup"><span data-stu-id="29e7f-211">hello following example shows you how you can view recent autoscale and alert events.</span></span> <span data-ttu-id="29e7f-212">Utilize o histórico de dimensionamento automático ao hello do tooview de pesquisa Olá atividade registos.</span><span class="sxs-lookup"><span data-stu-id="29e7f-212">Use hello activity log search tooview hello autoscale history.</span></span>

```PowerShell
Get-AzureRmLog -Caller "Microsoft.Insights/autoscaleSettings" -DetailedOutput -StartTime 2015-03-01
```

<span data-ttu-id="29e7f-213">Pode utilizar Olá `Get-AzureRmAutoScaleHistory` cmdlet tooretrieve histórico de dimensionamento automático.</span><span class="sxs-lookup"><span data-stu-id="29e7f-213">You can use hello `Get-AzureRmAutoScaleHistory` cmdlet tooretrieve AutoScale history.</span></span>

```PowerShell
Get-AzureRmAutoScaleHistory -ResourceId /subscriptions/s1/resourceGroups/myrg1/providers/microsoft.insights/autoscalesettings/myScaleSetting -StartTime 2016-03-15 -DetailedOutput
```

<span data-ttu-id="29e7f-214">Para obter mais informações, consulte [Get-AutoscaleHistory](https://msdn.microsoft.com/library/mt282464.aspx).</span><span class="sxs-lookup"><span data-stu-id="29e7f-214">For more information, see [Get-AutoscaleHistory](https://msdn.microsoft.com/library/mt282464.aspx).</span></span>

### <a name="view-details-for-an-autoscale-setting"></a><span data-ttu-id="29e7f-215">Ver detalhes de uma definição de dimensionamento automático</span><span class="sxs-lookup"><span data-stu-id="29e7f-215">View details for an autoscale setting</span></span>
<span data-ttu-id="29e7f-216">Pode utilizar Olá `Get-Autoscalesetting` cmdlet tooretrieve mais informações sobre a definição de dimensionamento automático de Olá.</span><span class="sxs-lookup"><span data-stu-id="29e7f-216">You can use hello `Get-Autoscalesetting` cmdlet tooretrieve more information about hello autoscale setting.</span></span>

<span data-ttu-id="29e7f-217">Olá exemplo seguinte mostra os detalhes sobre todas as definições de dimensionamento automático no grupo de recursos de Olá 'myrg1'.</span><span class="sxs-lookup"><span data-stu-id="29e7f-217">hello following example shows details about all autoscale settings in hello resource group 'myrg1'.</span></span>

```PowerShell
Get-AzureRmAutoscalesetting -ResourceGroup myrg1 -DetailedOutput
```

<span data-ttu-id="29e7f-218">Olá exemplo seguinte mostra os detalhes sobre todas as definições de dimensionamento automático no grupo de recursos de Olá 'myrg1' e especificamente Olá com o nome 'MyScaleVMSSSetting' de definição de dimensionamento automático.</span><span class="sxs-lookup"><span data-stu-id="29e7f-218">hello following example shows details about all autoscale settings in hello resource group 'myrg1' and specifically hello autoscale setting named 'MyScaleVMSSSetting'.</span></span>

```PowerShell
Get-AzureRmAutoscalesetting -ResourceGroup myrg1 -Name MyScaleVMSSSetting -DetailedOutput
```

### <a name="remove-an-autoscale-setting"></a><span data-ttu-id="29e7f-219">Remover uma definição de dimensionamento automático</span><span class="sxs-lookup"><span data-stu-id="29e7f-219">Remove an autoscale setting</span></span>
<span data-ttu-id="29e7f-220">Pode utilizar Olá `Remove-Autoscalesetting` cmdlet toodelete uma definição de dimensionamento automático.</span><span class="sxs-lookup"><span data-stu-id="29e7f-220">You can use hello `Remove-Autoscalesetting` cmdlet toodelete an autoscale setting.</span></span>

```PowerShell
Remove-AzureRmAutoscalesetting -ResourceGroup myrg1 -Name MyScaleVMSSSetting
```

## <a name="manage-log-profiles-for-activity-log"></a><span data-ttu-id="29e7f-221">Gerir perfis de registo para o registo de atividade</span><span class="sxs-lookup"><span data-stu-id="29e7f-221">Manage log profiles for activity log</span></span>
<span data-ttu-id="29e7f-222">Pode criar um *registo perfil* e exportar dados da sua conta de armazenamento de tooa de registo de atividade e podem configurar a retenção de dados para o mesmo.</span><span class="sxs-lookup"><span data-stu-id="29e7f-222">You can create a *log profile* and export data from your activity log tooa storage account and you can configure data retention for it.</span></span> <span data-ttu-id="29e7f-223">Opcionalmente, também pode transmitir Olá dados tooyour Hub de eventos.</span><span class="sxs-lookup"><span data-stu-id="29e7f-223">Optionally, you can also stream hello data tooyour Event Hub.</span></span> <span data-ttu-id="29e7f-224">Tenha em atenção que esta funcionalidade está atualmente em pré-visualização e só pode criar um perfil de registo por subscrição.</span><span class="sxs-lookup"><span data-stu-id="29e7f-224">Note that this feature is currently in Preview and you can only create one log profile per subscription.</span></span> <span data-ttu-id="29e7f-225">Pode utilizar os seguintes cmdlets com a sua atual toocreate de subscrição de Olá e gerir perfis de registo.</span><span class="sxs-lookup"><span data-stu-id="29e7f-225">You can use hello following cmdlets with your current subscription toocreate and manage log profiles.</span></span> <span data-ttu-id="29e7f-226">Também pode escolher uma determinada subscrição.</span><span class="sxs-lookup"><span data-stu-id="29e7f-226">You can also choose a particular subscription.</span></span> <span data-ttu-id="29e7f-227">Embora PowerShell predefinições subscrição atual toohello, pode sempre alterar esse utilizando `Set-AzureRmContext`.</span><span class="sxs-lookup"><span data-stu-id="29e7f-227">Although PowerShell defaults toohello current subscription, you can always change that using `Set-AzureRmContext`.</span></span> <span data-ttu-id="29e7f-228">Pode configurar a conta de armazenamento de atividade registo tooroute dados tooany ou Hub de eventos dentro dessa subscrição.</span><span class="sxs-lookup"><span data-stu-id="29e7f-228">You can configure activity log tooroute data tooany storage account or Event Hub within that subscription.</span></span> <span data-ttu-id="29e7f-229">Dados são escritos como ficheiros do blob no formato JSON.</span><span class="sxs-lookup"><span data-stu-id="29e7f-229">Data is written as blob files in JSON format.</span></span>

### <a name="get-a-log-profile"></a><span data-ttu-id="29e7f-230">Obter um perfil de registo</span><span class="sxs-lookup"><span data-stu-id="29e7f-230">Get a log profile</span></span>
<span data-ttu-id="29e7f-231">toofetch os perfis de registo existente, utilize Olá `Get-AzureRmLogProfile` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="29e7f-231">toofetch your existing log profiles, use hello `Get-AzureRmLogProfile` cmdlet.</span></span>

### <a name="add-a-log-profile-without-data-retention"></a><span data-ttu-id="29e7f-232">Adicionar um perfil de registo sem retenção de dados</span><span class="sxs-lookup"><span data-stu-id="29e7f-232">Add a log profile without data retention</span></span>
```PowerShell
Add-AzureRmLogProfile -Name my_log_profile_s1 -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage -Locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia
```

### <a name="remove-a-log-profile"></a><span data-ttu-id="29e7f-233">Remover um perfil de registo</span><span class="sxs-lookup"><span data-stu-id="29e7f-233">Remove a log profile</span></span>
```PowerShell
Remove-AzureRmLogProfile -name my_log_profile_s1
```

### <a name="add-a-log-profile-with-data-retention"></a><span data-ttu-id="29e7f-234">Adicionar um perfil de registo com retenção de dados</span><span class="sxs-lookup"><span data-stu-id="29e7f-234">Add a log profile with data retention</span></span>
<span data-ttu-id="29e7f-235">Pode especificar Olá **- RetentionInDays** propriedade com Olá número de dias, como um número inteiro positivo, onde os dados de Olá são mantidos.</span><span class="sxs-lookup"><span data-stu-id="29e7f-235">You can specify hello **-RetentionInDays** property with hello number of days, as a positive integer, where hello data is retained.</span></span>

```PowerShell
Add-AzureRmLogProfile -Name my_log_profile_s1 -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage -Locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia -RetentionInDays 90
```

### <a name="add-log-profile-with-retention-and-eventhub"></a><span data-ttu-id="29e7f-236">Adicionar perfil de registo com retenção e EventHub</span><span class="sxs-lookup"><span data-stu-id="29e7f-236">Add log profile with retention and EventHub</span></span>
<span data-ttu-id="29e7f-237">Na adição toorouting a conta de toostorage de dados, pode também ser transmitido em fluxo-tooan Hub de eventos.</span><span class="sxs-lookup"><span data-stu-id="29e7f-237">In addition toorouting your data toostorage account, you can also stream it tooan Event Hub.</span></span> <span data-ttu-id="29e7f-238">Tenha em atenção que nesta pré-visualização a configuração de conta de armazenamento de versão e Olá é obrigatória, mas a configuração do Hub de eventos é opcional.</span><span class="sxs-lookup"><span data-stu-id="29e7f-238">Note that in this preview release and hello storage account configuration is mandatory but Event Hub configuration is optional.</span></span>

```PowerShell
Add-AzureRmLogProfile -Name my_log_profile_s1 -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage -serviceBusRuleId /subscriptions/s1/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/mytestSB/authorizationrules/RootManageSharedAccessKey -Locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia -RetentionInDays 90
```

## <a name="configure-diagnostics-logs"></a><span data-ttu-id="29e7f-239">Configurar os registos de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="29e7f-239">Configure diagnostics logs</span></span>
<span data-ttu-id="29e7f-240">Muitos serviços do Azure fornecem registos adicionais e telemetria que pode ser dados toosave configurada na sua conta do Storage do Azure, enviar tooEvent Hubs e/ou enviados tooan área de trabalho de análise de registos do OMS.</span><span class="sxs-lookup"><span data-stu-id="29e7f-240">Many Azure services provide additional logs and telemetry that can be configured toosave data in your Azure Storage account, send tooEvent Hubs, and/or sent tooan OMS Log Analytics workspace.</span></span> <span data-ttu-id="29e7f-241">Essa operação só pode ser efetuada num nível de recursos e concentrador de conta ou evento de armazenamento de Olá deve estar presente no Olá mesma região que o recurso de destino olá onde a definição de diagnóstico de Olá está configurada.</span><span class="sxs-lookup"><span data-stu-id="29e7f-241">That operation can only be performed at a resource level and hello storage account or event hub should be present in hello same region as hello target resource where hello diagnostics setting is configured.</span></span>

### <a name="get-diagnostic-setting"></a><span data-ttu-id="29e7f-242">Obter a definição de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="29e7f-242">Get diagnostic setting</span></span>
```PowerShell
Get-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Logic/workflows/andy0315logicapp
```

<span data-ttu-id="29e7f-243">Desativar a definição de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="29e7f-243">Disable diagnostic setting</span></span>

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Logic/workflows/andy0315logicapp -StorageAccountId /subscriptions/s1/resourceGroups/Default-Storage-WestUS/providers/Microsoft.Storage/storageAccounts/mystorageaccount -Enable $false
```

<span data-ttu-id="29e7f-244">Ativar a definição de diagnóstico sem retenção</span><span class="sxs-lookup"><span data-stu-id="29e7f-244">Enable diagnostic setting without retention</span></span>

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Logic/workflows/andy0315logicapp -StorageAccountId /subscriptions/s1/resourceGroups/Default-Storage-WestUS/providers/Microsoft.Storage/storageAccounts/mystorageaccount -Enable $true
```

<span data-ttu-id="29e7f-245">Ativar a definição de diagnóstico com retenção</span><span class="sxs-lookup"><span data-stu-id="29e7f-245">Enable diagnostic setting with retention</span></span>

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Logic/workflows/andy0315logicapp -StorageAccountId /subscriptions/s1/resourceGroups/Default-Storage-WestUS/providers/Microsoft.Storage/storageAccounts/mystorageaccount -Enable $true -RetentionEnabled $true -RetentionInDays 90
```

<span data-ttu-id="29e7f-246">Ativar a definição de diagnóstico com o período de retenção para uma categoria de registo específico</span><span class="sxs-lookup"><span data-stu-id="29e7f-246">Enable diagnostic setting with retention for a specific log category</span></span>

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/insights-integration/providers/Microsoft.Network/networkSecurityGroups/viruela1 -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/sakteststorage -Categories NetworkSecurityGroupEvent -Enable $true -RetentionEnabled $true -RetentionInDays 90
```

<span data-ttu-id="29e7f-247">Ativar a definição de diagnóstico para os Event Hubs</span><span class="sxs-lookup"><span data-stu-id="29e7f-247">Enable diagnostic setting for Event Hubs</span></span>

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/insights-integration/providers/Microsoft.Network/networkSecurityGroups/viruela1 -serviceBusRuleId /subscriptions/s1/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/mytestSB/authorizationrules/RootManageSharedAccessKey -Enable $true
```

<span data-ttu-id="29e7f-248">Ativar a definição de diagnóstico para OMS</span><span class="sxs-lookup"><span data-stu-id="29e7f-248">Enable diagnostic setting for OMS</span></span>

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/insights-integration/providers/Microsoft.Network/networkSecurityGroups/viruela1 -WorkspaceId 76d785fd-d1ce-4f50-8ca3-858fc819ca0f -Enabled $true

```
