---
title: "aaaMonitor acesso registos, registos de desempenho, estado de funcionamento de back-end e métricas de Gateway de aplicação | Microsoft Docs"
description: "Saiba como tooenable e gerir registos de acesso e registos de desempenho para o Gateway de aplicação"
services: application-gateway
documentationcenter: na
author: amitsriva
manager: rossort
editor: tysonn
tags: azure-resource-manager
ms.assetid: 300628b8-8e3d-40ab-b294-3ecc5e48ef98
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/17/2017
ms.author: amitsriva
ms.openlocfilehash: 36ebf15c28f776158350ef8e73d617ef68e09266
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="back-end-health-diagnostic-logs-and-metrics-for-application-gateway"></a><span data-ttu-id="ecaff-103">Estado de funcionamento de back-end, os registos de diagnóstico e métricas de Gateway de aplicação</span><span class="sxs-lookup"><span data-stu-id="ecaff-103">Back-end health, diagnostic logs, and metrics for Application Gateway</span></span>

<span data-ttu-id="ecaff-104">Ao utilizar o Gateway de aplicação do Azure, pode monitorizar recursos Olá seguintes formas:</span><span class="sxs-lookup"><span data-stu-id="ecaff-104">By using Azure Application Gateway, you can monitor resources in hello following ways:</span></span>

* <span data-ttu-id="ecaff-105">[Estado de funcionamento de back-end](#back-end-health): Gateway de aplicação fornece Olá capacidade toomonitor Olá estado de funcionamento dos servidores Olá Olá conjuntos de back-end através de Olá portal do Azure e através do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ecaff-105">[Back-end health](#back-end-health): Application Gateway provides hello capability toomonitor hello health of hello servers in hello back-end pools through hello Azure portal and through PowerShell.</span></span> <span data-ttu-id="ecaff-106">Também pode encontrar o estado de funcionamento de Olá dos conjuntos de back-end Olá através de registos de diagnóstico de desempenho de Olá.</span><span class="sxs-lookup"><span data-stu-id="ecaff-106">You can also find hello health of hello back-end pools through hello performance diagnostic logs.</span></span>

* <span data-ttu-id="ecaff-107">[Os registos](#diagnostic-logs): permitir que os registos de desempenho, o acesso, e outro dados toobe guardado ou consumido de um recurso para efeitos de monitorização.</span><span class="sxs-lookup"><span data-stu-id="ecaff-107">[Logs](#diagnostic-logs): Logs allow for performance, access, and other data toobe saved or consumed from a resource for monitoring purposes.</span></span>

* <span data-ttu-id="ecaff-108">[Métricas](#metrics): Gateway de aplicação não tem atualmente uma métrica.</span><span class="sxs-lookup"><span data-stu-id="ecaff-108">[Metrics](#metrics): Application Gateway currently has one metric.</span></span> <span data-ttu-id="ecaff-109">Esta métrica mede o débito de Olá Olá do gateway de aplicação em bytes por segundo.</span><span class="sxs-lookup"><span data-stu-id="ecaff-109">This metric measures hello throughput of hello application gateway in bytes per second.</span></span>

## <a name="back-end-health"></a><span data-ttu-id="ecaff-110">Estado de funcionamento de back-end</span><span class="sxs-lookup"><span data-stu-id="ecaff-110">Back-end health</span></span>

<span data-ttu-id="ecaff-111">Gateway de aplicação fornece Olá capacidade toomonitor Olá estado de funcionamento dos membros individuais dos conjuntos de back-end Olá através do portal de Olá, PowerShell e Olá interface de linha de comandos (CLI).</span><span class="sxs-lookup"><span data-stu-id="ecaff-111">Application Gateway provides hello capability toomonitor hello health of individual members of hello back-end pools through hello portal, PowerShell, and hello command-line interface (CLI).</span></span> <span data-ttu-id="ecaff-112">Também pode encontrar um Estado de funcionamento agregado resumo dos conjuntos de back-end através de registos de diagnóstico de desempenho de Olá.</span><span class="sxs-lookup"><span data-stu-id="ecaff-112">You can also find an aggregated health summary of back-end pools through hello performance diagnostic logs.</span></span> 

<span data-ttu-id="ecaff-113">relatório de estado de funcionamento de back-end Olá reflete a saída de Olá de instâncias de Olá estado de funcionamento do Gateway de aplicação toohello de sonda back-end.</span><span class="sxs-lookup"><span data-stu-id="ecaff-113">hello back-end health report reflects hello output of hello Application Gateway health probe toohello back-end instances.</span></span> <span data-ttu-id="ecaff-114">Quando pesquisar é bem-sucedido e Olá novamente fim pode receber tráfego, é considerado em bom estado.</span><span class="sxs-lookup"><span data-stu-id="ecaff-114">When probing is successful and hello back end can receive traffic, it's considered healthy.</span></span> <span data-ttu-id="ecaff-115">Caso contrário, considera-se danificado.</span><span class="sxs-lookup"><span data-stu-id="ecaff-115">Otherwise, it's considered unhealthy.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ecaff-116">Se existir um grupo de segurança de rede (NSG) numa sub-rede de Gateway de aplicação, abra a intervalos de portas 65503 65534 na sub-rede de Gateway de aplicação Olá para tráfego de entrada.</span><span class="sxs-lookup"><span data-stu-id="ecaff-116">If there is a network security group (NSG) on an Application Gateway subnet, open port ranges 65503-65534 on hello Application Gateway subnet for inbound traffic.</span></span> <span data-ttu-id="ecaff-117">Estas portas são necessárias para toowork de API do Estado de funcionamento de back-end Olá.</span><span class="sxs-lookup"><span data-stu-id="ecaff-117">These ports are required for hello back-end health API toowork.</span></span>


### <a name="view-back-end-health-through-hello-portal"></a><span data-ttu-id="ecaff-118">Ver estado de funcionamento de back-end através do portal Olá</span><span class="sxs-lookup"><span data-stu-id="ecaff-118">View back-end health through hello portal</span></span>

<span data-ttu-id="ecaff-119">No portal de Olá, estado de funcionamento de back-end é fornecido automaticamente.</span><span class="sxs-lookup"><span data-stu-id="ecaff-119">In hello portal, back-end health is provided automatically.</span></span> <span data-ttu-id="ecaff-120">Num gateway de aplicação existente, selecione **monitorização** > **estado de funcionamento de back-end**.</span><span class="sxs-lookup"><span data-stu-id="ecaff-120">In an existing application gateway, select **Monitoring** > **Backend health**.</span></span> 

<span data-ttu-id="ecaff-121">Cada membro do conjunto de back-end Olá está listado nesta página (quer seja um NIC, IP ou FQDN).</span><span class="sxs-lookup"><span data-stu-id="ecaff-121">Each member in hello back-end pool is listed on this page (whether it's a NIC, IP, or FQDN).</span></span> <span data-ttu-id="ecaff-122">Nome do conjunto de back-end, porta, o nome de definições HTTP de back-end e estado de funcionamento são apresentadas.</span><span class="sxs-lookup"><span data-stu-id="ecaff-122">Back-end pool name, port, back-end HTTP settings name, and health status are shown.</span></span> <span data-ttu-id="ecaff-123">Os valores válidos para o estado de funcionamento são **bom estado de funcionamento**, **mau estado de funcionamento**, e **desconhecido**.</span><span class="sxs-lookup"><span data-stu-id="ecaff-123">Valid values for health status are **Healthy**, **Unhealthy**, and **Unknown**.</span></span>

> [!NOTE]
> <span data-ttu-id="ecaff-124">Se vir um Estado de funcionamento de back-end das **desconhecido**, certifique-se de que esse acesso toohello back-end não está bloqueado por uma regra NSG, uma rota definida pelo utilizador (UDR) ou um DNS na rede virtual Olá personalizado.</span><span class="sxs-lookup"><span data-stu-id="ecaff-124">If you see a back-end health status of **Unknown**, ensure that access toohello back end is not blocked by an NSG rule, a user-defined route (UDR), or a custom DNS in hello virtual network.</span></span>

![Estado de funcionamento de back-end][10]

### <a name="view-back-end-health-through-powershell"></a><span data-ttu-id="ecaff-126">Ver estado de funcionamento de back-end através do PowerShell</span><span class="sxs-lookup"><span data-stu-id="ecaff-126">View back-end health through PowerShell</span></span>

<span data-ttu-id="ecaff-127">Olá código do PowerShell a seguir mostra como o estado de funcionamento do tooview back-end utilizando Olá `Get-AzureRmApplicationGatewayBackendHealth` cmdlet:</span><span class="sxs-lookup"><span data-stu-id="ecaff-127">hello following PowerShell code shows how tooview back-end health by using hello `Get-AzureRmApplicationGatewayBackendHealth` cmdlet:</span></span>

```powershell
Get-AzureRmApplicationGatewayBackendHealth -Name ApplicationGateway1 -ResourceGroupName Contoso
```

### <a name="view-back-end-health-through-azure-cli-20"></a><span data-ttu-id="ecaff-128">Ver estado de funcionamento de back-end através do Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="ecaff-128">View back-end health through Azure CLI 2.0</span></span>

```azurecli
az network application-gateway show-backend-health --resource-group AdatumAppGatewayRG --name AdatumAppGateway
```

### <a name="results"></a><span data-ttu-id="ecaff-129">Resultados</span><span class="sxs-lookup"><span data-stu-id="ecaff-129">Results</span></span>

<span data-ttu-id="ecaff-130">Olá fragmento a seguir mostra um exemplo de resposta Olá:</span><span class="sxs-lookup"><span data-stu-id="ecaff-130">hello following snippet shows an example of hello response:</span></span>

```json
{
"BackendAddressPool": {
    "Id": "/subscriptions/00000000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/applicationGateways/applicationGateway1/backendAddressPools/appGatewayBackendPool"
},
"BackendHttpSettingsCollection": [
    {
    "BackendHttpSettings": {
        "Id": "/00000000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/applicationGateways/applicationGateway1/backendHttpSettingsCollection/appGatewayBackendHttpSettings"
    },
    "Servers": [
        {
        "Address": "hostname.westus.cloudapp.azure.com",
        "Health": "Healthy"
        },
        {
        "Address": "hostname.westus.cloudapp.azure.com",
        "Health": "Healthy"
        }
    ]
    }
]
}
```

## <span data-ttu-id="ecaff-131"><a name="diagnostic-logging"></a>Registos de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="ecaff-131"><a name="diagnostic-logging"></a>Diagnostic logs</span></span>

<span data-ttu-id="ecaff-132">Pode utilizar diferentes tipos de registos do Azure toomanage e resolver problemas de gateways de aplicação.</span><span class="sxs-lookup"><span data-stu-id="ecaff-132">You can use different types of logs in Azure toomanage and troubleshoot application gateways.</span></span> <span data-ttu-id="ecaff-133">Pode aceder a algumas destes registos através do portal Olá.</span><span class="sxs-lookup"><span data-stu-id="ecaff-133">You can access some of these logs through hello portal.</span></span> <span data-ttu-id="ecaff-134">Todos os registos podem ser extraídos de Blob storage do Azure e visualizados em diferentes ferramentas, tal como [Log Analytics](../log-analytics/log-analytics-azure-networking-analytics.md), Excel e o Power BI.</span><span class="sxs-lookup"><span data-stu-id="ecaff-134">All logs can be extracted from Azure Blob storage and viewed in different tools, such as [Log Analytics](../log-analytics/log-analytics-azure-networking-analytics.md), Excel, and Power BI.</span></span> <span data-ttu-id="ecaff-135">Pode saber mais sobre Olá diferentes tipos de registos de Olá lista a seguir:</span><span class="sxs-lookup"><span data-stu-id="ecaff-135">You can learn more about hello different types of logs from hello following list:</span></span>

* <span data-ttu-id="ecaff-136">**Registo de atividade**: pode utilizar [registos de atividade do Azure](../monitoring-and-diagnostics/insights-debugging-with-events.md) (anteriormente conhecido como registos de auditoria e registos operacionais) tooview todas as operações que são submetidos tooyour subscrição do Azure e o respetivo estado.</span><span class="sxs-lookup"><span data-stu-id="ecaff-136">**Activity log**: You can use [Azure activity logs](../monitoring-and-diagnostics/insights-debugging-with-events.md) (formerly known as operational logs and audit logs) tooview all operations that are submitted tooyour Azure subscription, and their status.</span></span> <span data-ttu-id="ecaff-137">Entradas de registo de atividade são recolhidas por predefinição, e pode visualizá-los no Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="ecaff-137">Activity log entries are collected by default, and you can view them in hello Azure portal.</span></span>
* <span data-ttu-id="ecaff-138">**Registo de acesso**: pode utilizar este padrões de acesso de Gateway de aplicação do registo tooview e analisar informações importantes, incluindo Olá invocadora IP, URL pedido, latência de resposta, código de retorno e bytes e terminar. Um registo de acesso é recolhido a cada 300 segundos.</span><span class="sxs-lookup"><span data-stu-id="ecaff-138">**Access log**: You can use this log tooview Application Gateway access patterns and analyze important information, including hello caller's IP, requested URL, response latency, return code, and bytes in and out. An access log is collected every 300 seconds.</span></span> <span data-ttu-id="ecaff-139">Este registo contém um registo por instância de Gateway de aplicação.</span><span class="sxs-lookup"><span data-stu-id="ecaff-139">This log contains one record per instance of Application Gateway.</span></span> <span data-ttu-id="ecaff-140">instância de Gateway de aplicação Olá pode ser identificada pela propriedade de instanceId Olá.</span><span class="sxs-lookup"><span data-stu-id="ecaff-140">hello Application Gateway instance can be identified by hello instanceId property.</span></span>
* <span data-ttu-id="ecaff-141">**Registo de desempenho**: pode utilizar este tooview de registo como instâncias de Gateway de aplicação estiver a efetuar.</span><span class="sxs-lookup"><span data-stu-id="ecaff-141">**Performance log**: You can use this log tooview how Application Gateway instances are performing.</span></span> <span data-ttu-id="ecaff-142">Este registo captura informações de desempenho para cada instância, incluindo o total de pedidos servidos, débito em bytes, total de pedidos servidos, contagem de pedidos falhados e contagem de instâncias de back-end de bom estado de funcionamento e mau estado de funcionamento.</span><span class="sxs-lookup"><span data-stu-id="ecaff-142">This log captures performance information for each instance, including total requests served, throughput in bytes, total requests served, failed request count, and healthy and unhealthy back-end instance count.</span></span> <span data-ttu-id="ecaff-143">Um registo de desempenho é recolhido a cada 60 segundos.</span><span class="sxs-lookup"><span data-stu-id="ecaff-143">A performance log is collected every 60 seconds.</span></span>
* <span data-ttu-id="ecaff-144">**Registo de firewall**: pode utilizar este tooview Olá gerar pedidos de registo que são registados através do modo de deteção ou prevenção de um gateway de aplicação que está configurado com firewall de aplicações web Olá.</span><span class="sxs-lookup"><span data-stu-id="ecaff-144">**Firewall log**: You can use this log tooview hello requests that are logged through either detection or prevention mode of an application gateway that is configured with hello web application firewall.</span></span>

> [!NOTE]
> <span data-ttu-id="ecaff-145">Estão disponíveis apenas para os recursos implementados no modelo de implementação Azure Resource Manager Olá registos.</span><span class="sxs-lookup"><span data-stu-id="ecaff-145">Logs are available only for resources deployed in hello Azure Resource Manager deployment model.</span></span> <span data-ttu-id="ecaff-146">Não é possível utilizar os registos de recursos no modelo de implementação clássica Olá.</span><span class="sxs-lookup"><span data-stu-id="ecaff-146">You cannot use logs for resources in hello classic deployment model.</span></span> <span data-ttu-id="ecaff-147">Para uma melhor compreensão dos modelos de Olá dois, consulte Olá [Gestor de recursos de compreender implementação clássica e](../azure-resource-manager/resource-manager-deployment-model.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="ecaff-147">For a better understanding of hello two models, see hello [Understanding Resource Manager deployment and classic deployment](../azure-resource-manager/resource-manager-deployment-model.md) article.</span></span>

<span data-ttu-id="ecaff-148">Tem três opções para armazenar os registos:</span><span class="sxs-lookup"><span data-stu-id="ecaff-148">You have three options for storing your logs:</span></span>

* <span data-ttu-id="ecaff-149">**Conta de armazenamento**: contas do Storage são melhor utilizadas para os registos quando os registos são armazenados durante um longo período de tempo e revistos quando necessário.</span><span class="sxs-lookup"><span data-stu-id="ecaff-149">**Storage account**: Storage accounts are best used for logs when logs are stored for a longer duration and reviewed when needed.</span></span>
* <span data-ttu-id="ecaff-150">**Os Event hubs**: os Event hubs são uma excelente opção para integrar com outras informações de segurança e alertas tooget nos seus recursos de ferramentas de gestão de eventos (SEIM).</span><span class="sxs-lookup"><span data-stu-id="ecaff-150">**Event hubs**: Event hubs are a great option for integrating with other security information and event management (SEIM) tools tooget alerts on your resources.</span></span>
* <span data-ttu-id="ecaff-151">**Análise de registo**: análise de registos melhor é utilizada para a monitorização em tempo real gerais da sua aplicação ou ao procurar tendências.</span><span class="sxs-lookup"><span data-stu-id="ecaff-151">**Log Analytics**: Log Analytics is best used for general real-time monitoring of your application or looking at trends.</span></span>

### <a name="enable-logging-through-powershell"></a><span data-ttu-id="ecaff-152">Ativar o registo através do PowerShell</span><span class="sxs-lookup"><span data-stu-id="ecaff-152">Enable logging through PowerShell</span></span>

<span data-ttu-id="ecaff-153">Registo de atividade é ativado automaticamente para todos os recursos do Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="ecaff-153">Activity logging is automatically enabled for every Resource Manager resource.</span></span> <span data-ttu-id="ecaff-154">Tem de ativar o acesso e o desempenho toostart de registo a recolher dados de Olá disponíveis através desses registos.</span><span class="sxs-lookup"><span data-stu-id="ecaff-154">You must enable access and performance logging toostart collecting hello data available through those logs.</span></span> <span data-ttu-id="ecaff-155">tooenable registo Olá utilize os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="ecaff-155">tooenable logging, use hello following steps:</span></span>

1. <span data-ttu-id="ecaff-156">Tenha em atenção o ID de recurso da sua conta do storage, onde os dados de registo Olá estão armazenados.</span><span class="sxs-lookup"><span data-stu-id="ecaff-156">Note your storage account's resource ID, where hello log data is stored.</span></span> <span data-ttu-id="ecaff-157">Este valor é o formato de Olá: /subscriptions/{targetsubscriptionid}/resourcegroups/{targetresourcegroupname}\<subscriptionId\>/resourceGroups/\<nome do grupo de recursos\>/providers/Microsoft.Storage/storageAccounts/\<denomedecontadostorage\>.</span><span class="sxs-lookup"><span data-stu-id="ecaff-157">This value is of hello form: /subscriptions/\<subscriptionId\>/resourceGroups/\<resource group name\>/providers/Microsoft.Storage/storageAccounts/\<storage account name\>.</span></span> <span data-ttu-id="ecaff-158">Pode utilizar qualquer conta de armazenamento na sua subscrição.</span><span class="sxs-lookup"><span data-stu-id="ecaff-158">You can use any storage account in your subscription.</span></span> <span data-ttu-id="ecaff-159">Pode utilizar estas informações a Olá toofind portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="ecaff-159">You can use hello Azure portal toofind this information.</span></span>

    ![Portal: ID de recurso conta de armazenamento](./media/application-gateway-diagnostics/diagnostics1.png)

2. <span data-ttu-id="ecaff-161">Tenha em atenção o ID de recurso do gateway de aplicação para o qual o registo está ativado.</span><span class="sxs-lookup"><span data-stu-id="ecaff-161">Note your application gateway's resource ID for which logging is enabled.</span></span> <span data-ttu-id="ecaff-162">Este valor é o formato de Olá: /subscriptions/{targetsubscriptionid}/resourcegroups/{targetresourcegroupname}\<subscriptionId\>/resourceGroups/\<nome do grupo de recursos\>/providers/Microsoft.Network/applicationGateways/\<gateway de aplicação nome\>.</span><span class="sxs-lookup"><span data-stu-id="ecaff-162">This value is of hello form: /subscriptions/\<subscriptionId\>/resourceGroups/\<resource group name\>/providers/Microsoft.Network/applicationGateways/\<application gateway name\>.</span></span> <span data-ttu-id="ecaff-163">Pode utilizar toofind portal Olá estas informações.</span><span class="sxs-lookup"><span data-stu-id="ecaff-163">You can use hello portal toofind this information.</span></span>

    ![Portal: ID de recurso para o gateway de aplicação](./media/application-gateway-diagnostics/diagnostics2.png)

3. <span data-ttu-id="ecaff-165">Ative o registo de diagnóstico utilizando Olá seguinte cmdlet do PowerShell:</span><span class="sxs-lookup"><span data-stu-id="ecaff-165">Enable diagnostic logging by using hello following PowerShell cmdlet:</span></span>

    ```powershell
    Set-AzureRmDiagnosticSetting  -ResourceId /subscriptions/<subscriptionId>/resourceGroups/<resource group name>/providers/Microsoft.Network/applicationGateways/<application gateway name> -StorageAccountId /subscriptions/<subscriptionId>/resourceGroups/<resource group name>/providers/Microsoft.Storage/storageAccounts/<storage account name> -Enabled $true     
    ```
    
> [!TIP] 
><span data-ttu-id="ecaff-166">Registos de atividade não necessitam de uma conta de armazenamento separada.</span><span class="sxs-lookup"><span data-stu-id="ecaff-166">Activity logs do not require a separate storage account.</span></span> <span data-ttu-id="ecaff-167">utilização de Olá de armazenamento de acesso e o registo de desempenho incorreu encargos de serviço.</span><span class="sxs-lookup"><span data-stu-id="ecaff-167">hello use of storage for access and performance logging incurs service charges.</span></span>

### <a name="enable-logging-through-hello-azure-portal"></a><span data-ttu-id="ecaff-168">Ativar o registo através de Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="ecaff-168">Enable logging through hello Azure portal</span></span>

1. <span data-ttu-id="ecaff-169">No Olá portal do Azure, localizar o recurso e clique em **registos de diagnóstico**.</span><span class="sxs-lookup"><span data-stu-id="ecaff-169">In hello Azure portal, find your resource and click **Diagnostic logs**.</span></span>

   <span data-ttu-id="ecaff-170">Gateway de aplicação, estão disponíveis três registos:</span><span class="sxs-lookup"><span data-stu-id="ecaff-170">For Application Gateway, three logs are available:</span></span>

   * <span data-ttu-id="ecaff-171">Registo de acesso</span><span class="sxs-lookup"><span data-stu-id="ecaff-171">Access log</span></span>
   * <span data-ttu-id="ecaff-172">Registo de desempenho</span><span class="sxs-lookup"><span data-stu-id="ecaff-172">Performance log</span></span>
   * <span data-ttu-id="ecaff-173">Registo de firewall</span><span class="sxs-lookup"><span data-stu-id="ecaff-173">Firewall log</span></span>

2. <span data-ttu-id="ecaff-174">recolher dados de toostart, clique em **ative os diagnósticos**.</span><span class="sxs-lookup"><span data-stu-id="ecaff-174">toostart collecting data, click **Turn on diagnostics**.</span></span>

   ![Ativar o diagnóstico][1]

3. <span data-ttu-id="ecaff-176">Olá **as definições de diagnóstico** painel fornece definições de Olá para Olá os registos de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="ecaff-176">hello **Diagnostics settings** blade provides hello settings for hello diagnostic logs.</span></span> <span data-ttu-id="ecaff-177">Neste exemplo, análise de registos armazena Olá registos.</span><span class="sxs-lookup"><span data-stu-id="ecaff-177">In this example, Log Analytics stores hello logs.</span></span> <span data-ttu-id="ecaff-178">Clique em **configurar** em **Log Analytics** tooconfigure sua área de trabalho.</span><span class="sxs-lookup"><span data-stu-id="ecaff-178">Click **Configure** under **Log Analytics** tooconfigure your workspace.</span></span> <span data-ttu-id="ecaff-179">Também pode utilizar um armazenamento conta toosave Olá os registos de diagnóstico e hubs de eventos.</span><span class="sxs-lookup"><span data-stu-id="ecaff-179">You can also use event hubs and a storage account toosave hello diagnostic logs.</span></span>

   ![Iniciar o processo de configuração de Olá][2]

4. <span data-ttu-id="ecaff-181">Escolha uma área de trabalho do Operations Management Suite (OMS) existente ou crie um novo.</span><span class="sxs-lookup"><span data-stu-id="ecaff-181">Choose an existing Operations Management Suite (OMS) workspace or create a new one.</span></span> <span data-ttu-id="ecaff-182">Este exemplo utiliza um existente.</span><span class="sxs-lookup"><span data-stu-id="ecaff-182">This example uses an existing one.</span></span>

   ![Opções para áreas de trabalho do OMS][3]

5. <span data-ttu-id="ecaff-184">Confirme as definições de Olá e clique em **guardar**.</span><span class="sxs-lookup"><span data-stu-id="ecaff-184">Confirm hello settings and click **Save**.</span></span>

   ![Painel de definições de diagnóstico com seleções][4]

### <a name="activity-log"></a><span data-ttu-id="ecaff-186">Registo de atividades</span><span class="sxs-lookup"><span data-stu-id="ecaff-186">Activity log</span></span>

<span data-ttu-id="ecaff-187">Por predefinição, o Azure gera o registo de atividade Olá.</span><span class="sxs-lookup"><span data-stu-id="ecaff-187">Azure generates hello activity log by default.</span></span> <span data-ttu-id="ecaff-188">Olá registos são preservados durante 90 dias no arquivo de registos de eventos do Azure Olá.</span><span class="sxs-lookup"><span data-stu-id="ecaff-188">hello logs are preserved for 90 days in hello Azure event logs store.</span></span> <span data-ttu-id="ecaff-189">Saiba mais sobre estes registos o lendo Olá [ver eventos e registo de atividade](../monitoring-and-diagnostics/insights-debugging-with-events.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="ecaff-189">Learn more about these logs by reading hello [View events and activity log](../monitoring-and-diagnostics/insights-debugging-with-events.md) article.</span></span>

### <a name="access-log"></a><span data-ttu-id="ecaff-190">Registo de acesso</span><span class="sxs-lookup"><span data-stu-id="ecaff-190">Access log</span></span>

<span data-ttu-id="ecaff-191">registo de acesso de Olá é gerado apenas se tiver ativado, cada instância de Gateway de aplicação, conforme detalhado em Olá precedente passos.</span><span class="sxs-lookup"><span data-stu-id="ecaff-191">hello access log is generated only if you've enabled it on each Application Gateway instance, as detailed in hello preceding steps.</span></span> <span data-ttu-id="ecaff-192">dados de Olá são armazenados na conta do storage Olá que especificou quando ativou o registo de Olá.</span><span class="sxs-lookup"><span data-stu-id="ecaff-192">hello data is stored in hello storage account that you specified when you enabled hello logging.</span></span> <span data-ttu-id="ecaff-193">Cada acesso do Gateway de aplicação é registado no formato JSON, conforme mostrado no seguinte exemplo de Olá:</span><span class="sxs-lookup"><span data-stu-id="ecaff-193">Each access of Application Gateway is logged in JSON format, as shown in hello following example:</span></span>


|<span data-ttu-id="ecaff-194">Valor</span><span class="sxs-lookup"><span data-stu-id="ecaff-194">Value</span></span>  |<span data-ttu-id="ecaff-195">Descrição</span><span class="sxs-lookup"><span data-stu-id="ecaff-195">Description</span></span>  |
|---------|---------|
|<span data-ttu-id="ecaff-196">instanceId</span><span class="sxs-lookup"><span data-stu-id="ecaff-196">instanceId</span></span>     | <span data-ttu-id="ecaff-197">Esse pedido Olá servidos de instância de Gateway de aplicação.</span><span class="sxs-lookup"><span data-stu-id="ecaff-197">Application Gateway instance that served hello request.</span></span>        |
|<span data-ttu-id="ecaff-198">ClientIP</span><span class="sxs-lookup"><span data-stu-id="ecaff-198">clientIP</span></span>     | <span data-ttu-id="ecaff-199">IP de origem para o pedido de Olá.</span><span class="sxs-lookup"><span data-stu-id="ecaff-199">Originating IP for hello request.</span></span>        |
|<span data-ttu-id="ecaff-200">clientPort</span><span class="sxs-lookup"><span data-stu-id="ecaff-200">clientPort</span></span>     | <span data-ttu-id="ecaff-201">Porta de origem para o pedido de Olá.</span><span class="sxs-lookup"><span data-stu-id="ecaff-201">Originating port for hello request.</span></span>       |
|<span data-ttu-id="ecaff-202">httpMethod</span><span class="sxs-lookup"><span data-stu-id="ecaff-202">httpMethod</span></span>     | <span data-ttu-id="ecaff-203">Método HTTP utilizado pelo pedido de Olá.</span><span class="sxs-lookup"><span data-stu-id="ecaff-203">HTTP method used by hello request.</span></span>       |
|<span data-ttu-id="ecaff-204">requestUri</span><span class="sxs-lookup"><span data-stu-id="ecaff-204">requestUri</span></span>     | <span data-ttu-id="ecaff-205">URI de Olá recebeu o pedido.</span><span class="sxs-lookup"><span data-stu-id="ecaff-205">URI of hello received request.</span></span>        |
|<span data-ttu-id="ecaff-206">RequestQuery</span><span class="sxs-lookup"><span data-stu-id="ecaff-206">RequestQuery</span></span>     | <span data-ttu-id="ecaff-207">**Encaminhados por servidor**: instância de conjunto de Back-end que lhe foi enviada o pedido de Olá.</span><span class="sxs-lookup"><span data-stu-id="ecaff-207">**Server-Routed**: Back-end pool instance that was sent hello request.</span></span> </br> <span data-ttu-id="ecaff-208">**X-AzureApplicationGateway-registo-ID**: ID de correlação utilizada Olá pedido.</span><span class="sxs-lookup"><span data-stu-id="ecaff-208">**X-AzureApplicationGateway-LOG-ID**: Correlation ID used for hello request.</span></span> <span data-ttu-id="ecaff-209">Pode ser utilizado tootroubleshoot tráfego problemas em servidores de back-end Olá.</span><span class="sxs-lookup"><span data-stu-id="ecaff-209">It can be used tootroubleshoot traffic issues on hello back-end servers.</span></span> </br><span data-ttu-id="ecaff-210">**Estado do servidor**: código de resposta HTTP recebido de Gateway de aplicação de back-end Olá.</span><span class="sxs-lookup"><span data-stu-id="ecaff-210">**SERVER-STATUS**: HTTP response code that Application Gateway received from hello back end.</span></span>       |
|<span data-ttu-id="ecaff-211">UserAgent</span><span class="sxs-lookup"><span data-stu-id="ecaff-211">UserAgent</span></span>     | <span data-ttu-id="ecaff-212">Agente de utilizador do cabeçalho de pedido de Olá HTTP.</span><span class="sxs-lookup"><span data-stu-id="ecaff-212">User agent from hello HTTP request header.</span></span>        |
|<span data-ttu-id="ecaff-213">httpStatus</span><span class="sxs-lookup"><span data-stu-id="ecaff-213">httpStatus</span></span>     | <span data-ttu-id="ecaff-214">Código de estado HTTP devolvido toohello cliente do Gateway de aplicação.</span><span class="sxs-lookup"><span data-stu-id="ecaff-214">HTTP status code returned toohello client from Application Gateway.</span></span>       |
|<span data-ttu-id="ecaff-215">httpVersion</span><span class="sxs-lookup"><span data-stu-id="ecaff-215">httpVersion</span></span>     | <span data-ttu-id="ecaff-216">Versão HTTP do pedido de Olá.</span><span class="sxs-lookup"><span data-stu-id="ecaff-216">HTTP version of hello request.</span></span>        |
|<span data-ttu-id="ecaff-217">receivedBytes</span><span class="sxs-lookup"><span data-stu-id="ecaff-217">receivedBytes</span></span>     | <span data-ttu-id="ecaff-218">Tamanho do pacote recebido, em bytes.</span><span class="sxs-lookup"><span data-stu-id="ecaff-218">Size of packet received, in bytes.</span></span>        |
|<span data-ttu-id="ecaff-219">sentBytes</span><span class="sxs-lookup"><span data-stu-id="ecaff-219">sentBytes</span></span>| <span data-ttu-id="ecaff-220">Tamanho do pacote enviado, em bytes.</span><span class="sxs-lookup"><span data-stu-id="ecaff-220">Size of packet sent, in bytes.</span></span>|
|<span data-ttu-id="ecaff-221">timeTaken</span><span class="sxs-lookup"><span data-stu-id="ecaff-221">timeTaken</span></span>| <span data-ttu-id="ecaff-222">Período de tempo (em milissegundos) que leva uma toobe de pedidos processados e respetivos toobe resposta enviada.</span><span class="sxs-lookup"><span data-stu-id="ecaff-222">Length of time (in milliseconds) that it takes for a request toobe processed and its response toobe sent.</span></span> <span data-ttu-id="ecaff-223">Esta é calculada como Olá início do intervalo tempo Olá quando o Gateway de aplicação recebe primeiro byte de Olá de um tempo de toohello de pedido HTTP quando resposta Olá enviar a operação depois de concluída.</span><span class="sxs-lookup"><span data-stu-id="ecaff-223">This is calculated as hello interval from hello time when Application Gateway receives hello first byte of an HTTP request toohello time when hello response send operation finishes.</span></span> <span data-ttu-id="ecaff-224">É importante toonote Olá Time-Taken campo normalmente inclui o tempo de Olá que pacotes hello a pedido e resposta são estiverem em deslocação rede Olá.</span><span class="sxs-lookup"><span data-stu-id="ecaff-224">It's important toonote that hello Time-Taken field usually includes hello time that hello request and response packets are traveling over hello network.</span></span> |
|<span data-ttu-id="ecaff-225">sslEnabled</span><span class="sxs-lookup"><span data-stu-id="ecaff-225">sslEnabled</span></span>| <span data-ttu-id="ecaff-226">Indica se os conjuntos de back-end de toohello de comunicação utilizados SSL.</span><span class="sxs-lookup"><span data-stu-id="ecaff-226">Whether communication toohello back-end pools used SSL.</span></span> <span data-ttu-id="ecaff-227">Os valores válidos são e desativar.</span><span class="sxs-lookup"><span data-stu-id="ecaff-227">Valid values are on and off.</span></span>|
```json
{
    "resourceId": "/SUBSCRIPTIONS/{subscriptionId}/RESOURCEGROUPS/PEERINGTEST/PROVIDERS/MICROSOFT.NETWORK/APPLICATIONGATEWAYS/{applicationGatewayName}",
    "operationName": "ApplicationGatewayAccess",
    "time": "2017-04-26T19:27:38Z",
    "category": "ApplicationGatewayAccessLog",
    "properties": {
        "instanceId": "ApplicationGatewayRole_IN_0",
        "clientIP": "191.96.249.97",
        "clientPort": 46886,
        "httpMethod": "GET",
        "requestUri": "/phpmyadmin/scripts/setup.php",
        "requestQuery": "X-AzureApplicationGateway-CACHE-HIT=0&SERVER-ROUTED=10.4.0.4&X-AzureApplicationGateway-LOG-ID=874f1f0f-6807-41c9-b7bc-f3cfa74aa0b1&SERVER-STATUS=404",
        "userAgent": "-",
        "httpStatus": 404,
        "httpVersion": "HTTP/1.0",
        "receivedBytes": 65,
        "sentBytes": 553,
        "timeTaken": 205,
        "sslEnabled": "off"
    }
}
```

### <a name="performance-log"></a><span data-ttu-id="ecaff-228">Registo de desempenho</span><span class="sxs-lookup"><span data-stu-id="ecaff-228">Performance log</span></span>

<span data-ttu-id="ecaff-229">registo de desempenho de Olá é gerado apenas se tiver ativado, cada instância de Gateway de aplicação, conforme detalhado em Olá precedente passos.</span><span class="sxs-lookup"><span data-stu-id="ecaff-229">hello performance log is generated only if you have enabled it on each Application Gateway instance, as detailed in hello preceding steps.</span></span> <span data-ttu-id="ecaff-230">dados de Olá são armazenados na conta do storage Olá que especificou quando ativou o registo de Olá.</span><span class="sxs-lookup"><span data-stu-id="ecaff-230">hello data is stored in hello storage account that you specified when you enabled hello logging.</span></span> <span data-ttu-id="ecaff-231">dados de registo de desempenho de Olá são gerados em intervalos de 1 minuto.</span><span class="sxs-lookup"><span data-stu-id="ecaff-231">hello performance log data is generated in 1-minute intervals.</span></span> <span data-ttu-id="ecaff-232">é registado Olá dados os seguintes:</span><span class="sxs-lookup"><span data-stu-id="ecaff-232">hello following data is logged:</span></span>


|<span data-ttu-id="ecaff-233">Valor</span><span class="sxs-lookup"><span data-stu-id="ecaff-233">Value</span></span>  |<span data-ttu-id="ecaff-234">Descrição</span><span class="sxs-lookup"><span data-stu-id="ecaff-234">Description</span></span>  |
|---------|---------|
|<span data-ttu-id="ecaff-235">instanceId</span><span class="sxs-lookup"><span data-stu-id="ecaff-235">instanceId</span></span>     |  <span data-ttu-id="ecaff-236">Instância de Gateway de aplicação para o desempenho de dados está a ser gerados.</span><span class="sxs-lookup"><span data-stu-id="ecaff-236">Application Gateway instance for which performance data is being generated.</span></span> <span data-ttu-id="ecaff-237">Para um gateway de aplicação de várias instâncias, há uma linha por instância.</span><span class="sxs-lookup"><span data-stu-id="ecaff-237">For a multiple-instance application gateway, there is one row per instance.</span></span>        |
|<span data-ttu-id="ecaff-238">healthyHostCount</span><span class="sxs-lookup"><span data-stu-id="ecaff-238">healthyHostCount</span></span>     | <span data-ttu-id="ecaff-239">Número de anfitriões bom estado de funcionamento no conjunto de back-end Olá.</span><span class="sxs-lookup"><span data-stu-id="ecaff-239">Number of healthy hosts in hello back-end pool.</span></span>        |
|<span data-ttu-id="ecaff-240">unHealthyHostCount</span><span class="sxs-lookup"><span data-stu-id="ecaff-240">unHealthyHostCount</span></span>     | <span data-ttu-id="ecaff-241">Número de anfitriões mau estado de funcionamento no conjunto de back-end Olá.</span><span class="sxs-lookup"><span data-stu-id="ecaff-241">Number of unhealthy hosts in hello back-end pool.</span></span>        |
|<span data-ttu-id="ecaff-242">requestCount</span><span class="sxs-lookup"><span data-stu-id="ecaff-242">requestCount</span></span>     | <span data-ttu-id="ecaff-243">Número de pedidos servidos.</span><span class="sxs-lookup"><span data-stu-id="ecaff-243">Number of requests served.</span></span>        |
|<span data-ttu-id="ecaff-244">latência</span><span class="sxs-lookup"><span data-stu-id="ecaff-244">latency</span></span> | <span data-ttu-id="ecaff-245">Latência (em milissegundos) de pedidos do Olá instância toohello back-end que serve Olá pedidos.</span><span class="sxs-lookup"><span data-stu-id="ecaff-245">Latency (in milliseconds) of requests from hello instance toohello back end that serves hello requests.</span></span> |
|<span data-ttu-id="ecaff-246">failedRequestCount</span><span class="sxs-lookup"><span data-stu-id="ecaff-246">failedRequestCount</span></span>| <span data-ttu-id="ecaff-247">Número de pedidos falhados.</span><span class="sxs-lookup"><span data-stu-id="ecaff-247">Number of failed requests.</span></span>|
|<span data-ttu-id="ecaff-248">Débito</span><span class="sxs-lookup"><span data-stu-id="ecaff-248">throughput</span></span>| <span data-ttu-id="ecaff-249">Débito médio desde o registo do último Olá, medido em bytes por segundo.</span><span class="sxs-lookup"><span data-stu-id="ecaff-249">Average throughput since hello last log, measured in bytes per second.</span></span>|

```json
{
    "resourceId": "/SUBSCRIPTIONS/{subscriptionId}/RESOURCEGROUPS/{resourceGroupName}/PROVIDERS/MICROSOFT.NETWORK/APPLICATIONGATEWAYS/{applicationGatewayName}",
    "operationName": "ApplicationGatewayPerformance",
    "time": "2016-04-09T00:00:00Z",
    "category": "ApplicationGatewayPerformanceLog",
    "properties":
    {
        "instanceId":"ApplicationGatewayRole_IN_1",
        "healthyHostCount":"4",
        "unHealthyHostCount":"0",
        "requestCount":"185",
        "latency":"0",
        "failedRequestCount":"0",
        "throughput":"119427"
    }
}
```

> [!NOTE]
> <span data-ttu-id="ecaff-250">Latência é calculada a partir de tempo de Olá ao primeiro byte de Olá de pedido de Olá HTTP está na altura de recebida toohello último byte de Olá de Olá resposta de HTTP é enviado.</span><span class="sxs-lookup"><span data-stu-id="ecaff-250">Latency is calculated from hello time when hello first byte of hello HTTP request is received toohello time when hello last byte of hello HTTP response is sent.</span></span> <span data-ttu-id="ecaff-251">Olá, de Olá soma do tempo de processamento de Gateway de aplicação plus hello rede custo toohello novamente terminar, juntamente com a hora de Olá Olá back-end demora tooprocess Olá pedido.</span><span class="sxs-lookup"><span data-stu-id="ecaff-251">It's hello sum of hello Application Gateway processing time plus hello network cost toohello back end, plus hello time that hello back end takes tooprocess hello request.</span></span>

### <a name="firewall-log"></a><span data-ttu-id="ecaff-252">Registo de firewall</span><span class="sxs-lookup"><span data-stu-id="ecaff-252">Firewall log</span></span>

<span data-ttu-id="ecaff-253">registo de firewall de Olá é gerado apenas se tiver ativado-la para cada gateway de aplicação, conforme detalhado em Olá precedente passos.</span><span class="sxs-lookup"><span data-stu-id="ecaff-253">hello firewall log is generated only if you have enabled it for each application gateway, as detailed in hello preceding steps.</span></span> <span data-ttu-id="ecaff-254">Este registo também requer que firewall de aplicações web Olá está configurado num gateway de aplicação.</span><span class="sxs-lookup"><span data-stu-id="ecaff-254">This log also requires that hello web application firewall is configured on an application gateway.</span></span> <span data-ttu-id="ecaff-255">dados de Olá são armazenados na conta do storage Olá que especificou quando ativou o registo de Olá.</span><span class="sxs-lookup"><span data-stu-id="ecaff-255">hello data is stored in hello storage account that you specified when you enabled hello logging.</span></span> <span data-ttu-id="ecaff-256">é registado Olá dados os seguintes:</span><span class="sxs-lookup"><span data-stu-id="ecaff-256">hello following data is logged:</span></span>


|<span data-ttu-id="ecaff-257">Valor</span><span class="sxs-lookup"><span data-stu-id="ecaff-257">Value</span></span>  |<span data-ttu-id="ecaff-258">Descrição</span><span class="sxs-lookup"><span data-stu-id="ecaff-258">Description</span></span>  |
|---------|---------|
|<span data-ttu-id="ecaff-259">instanceId</span><span class="sxs-lookup"><span data-stu-id="ecaff-259">instanceId</span></span>     | <span data-ttu-id="ecaff-260">Instância de Gateway de aplicação para que firewall dados está a ser gerados.</span><span class="sxs-lookup"><span data-stu-id="ecaff-260">Application Gateway instance for which firewall data is being generated.</span></span> <span data-ttu-id="ecaff-261">Para um gateway de aplicação de várias instâncias, há uma linha por instância.</span><span class="sxs-lookup"><span data-stu-id="ecaff-261">For a multiple-instance application gateway, there is one row per instance.</span></span>         |
|<span data-ttu-id="ecaff-262">clientIp</span><span class="sxs-lookup"><span data-stu-id="ecaff-262">clientIp</span></span>     |   <span data-ttu-id="ecaff-263">IP de origem para o pedido de Olá.</span><span class="sxs-lookup"><span data-stu-id="ecaff-263">Originating IP for hello request.</span></span>      |
|<span data-ttu-id="ecaff-264">clientPort</span><span class="sxs-lookup"><span data-stu-id="ecaff-264">clientPort</span></span>     |  <span data-ttu-id="ecaff-265">Porta de origem para o pedido de Olá.</span><span class="sxs-lookup"><span data-stu-id="ecaff-265">Originating port for hello request.</span></span>       |
|<span data-ttu-id="ecaff-266">requestUri</span><span class="sxs-lookup"><span data-stu-id="ecaff-266">requestUri</span></span>     | <span data-ttu-id="ecaff-267">URL do pedido recebido Olá.</span><span class="sxs-lookup"><span data-stu-id="ecaff-267">URL of hello received request.</span></span>       |
|<span data-ttu-id="ecaff-268">ruleSetType</span><span class="sxs-lookup"><span data-stu-id="ecaff-268">ruleSetType</span></span>     | <span data-ttu-id="ecaff-269">Tipo de conjunto de regras.</span><span class="sxs-lookup"><span data-stu-id="ecaff-269">Rule set type.</span></span> <span data-ttu-id="ecaff-270">o valor disponível Olá é OWASP.</span><span class="sxs-lookup"><span data-stu-id="ecaff-270">hello available value is OWASP.</span></span>        |
|<span data-ttu-id="ecaff-271">ruleSetVersion</span><span class="sxs-lookup"><span data-stu-id="ecaff-271">ruleSetVersion</span></span>     | <span data-ttu-id="ecaff-272">O conjunto de regras de versão utilizada.</span><span class="sxs-lookup"><span data-stu-id="ecaff-272">Rule set version used.</span></span> <span data-ttu-id="ecaff-273">Os valores disponíveis são 2.2.9 e 3.0.</span><span class="sxs-lookup"><span data-stu-id="ecaff-273">Available values are 2.2.9 and 3.0.</span></span>     |
|<span data-ttu-id="ecaff-274">ruleId</span><span class="sxs-lookup"><span data-stu-id="ecaff-274">ruleId</span></span>     | <span data-ttu-id="ecaff-275">ID de regra de Olá acionar eventos.</span><span class="sxs-lookup"><span data-stu-id="ecaff-275">Rule ID of hello triggering event.</span></span>        |
|<span data-ttu-id="ecaff-276">Mensagem</span><span class="sxs-lookup"><span data-stu-id="ecaff-276">message</span></span>     | <span data-ttu-id="ecaff-277">Mensagem amigável de utilizador para acionar eventos de Olá.</span><span class="sxs-lookup"><span data-stu-id="ecaff-277">User-friendly message for hello triggering event.</span></span> <span data-ttu-id="ecaff-278">Obter mais detalhes são fornecidos na secção de detalhes de Olá.</span><span class="sxs-lookup"><span data-stu-id="ecaff-278">More details are provided in hello details section.</span></span>        |
|<span data-ttu-id="ecaff-279">Ação</span><span class="sxs-lookup"><span data-stu-id="ecaff-279">action</span></span>     |  <span data-ttu-id="ecaff-280">Ação tomada pedido Olá.</span><span class="sxs-lookup"><span data-stu-id="ecaff-280">Action taken on hello request.</span></span> <span data-ttu-id="ecaff-281">Os valores disponíveis são bloqueado e permitido.</span><span class="sxs-lookup"><span data-stu-id="ecaff-281">Available values are Blocked and Allowed.</span></span>      |
|<span data-ttu-id="ecaff-282">site</span><span class="sxs-lookup"><span data-stu-id="ecaff-282">site</span></span>     | <span data-ttu-id="ecaff-283">Site para os qual Olá registo foi gerado.</span><span class="sxs-lookup"><span data-stu-id="ecaff-283">Site for which hello log was generated.</span></span> <span data-ttu-id="ecaff-284">Atualmente, apenas Global está listado porque as regras são globais.</span><span class="sxs-lookup"><span data-stu-id="ecaff-284">Currently, only Global is listed because rules are global.</span></span>|
|<span data-ttu-id="ecaff-285">Detalhes</span><span class="sxs-lookup"><span data-stu-id="ecaff-285">details</span></span>     | <span data-ttu-id="ecaff-286">Detalhes de Olá acionar eventos.</span><span class="sxs-lookup"><span data-stu-id="ecaff-286">Details of hello triggering event.</span></span>        |
|<span data-ttu-id="ecaff-287">details.Message</span><span class="sxs-lookup"><span data-stu-id="ecaff-287">details.message</span></span>     | <span data-ttu-id="ecaff-288">Descrição da regra de Olá.</span><span class="sxs-lookup"><span data-stu-id="ecaff-288">Description of hello rule.</span></span>        |
|<span data-ttu-id="ecaff-289">details.data</span><span class="sxs-lookup"><span data-stu-id="ecaff-289">details.data</span></span>     | <span data-ttu-id="ecaff-290">Dados específicos encontradas pedido dessa regra Olá correspondentes.</span><span class="sxs-lookup"><span data-stu-id="ecaff-290">Specific data found in request that matched hello rule.</span></span>         |
|<span data-ttu-id="ecaff-291">details.File</span><span class="sxs-lookup"><span data-stu-id="ecaff-291">details.file</span></span>     | <span data-ttu-id="ecaff-292">Ficheiro de configuração que continha regra Olá.</span><span class="sxs-lookup"><span data-stu-id="ecaff-292">Configuration file that contained hello rule.</span></span>        |
|<span data-ttu-id="ecaff-293">details.line</span><span class="sxs-lookup"><span data-stu-id="ecaff-293">details.line</span></span>     | <span data-ttu-id="ecaff-294">Número de linha no ficheiro de configuração de Olá que acionou o evento de Olá.</span><span class="sxs-lookup"><span data-stu-id="ecaff-294">Line number in hello configuration file that triggered hello event.</span></span>       |

```json
{
  "resourceId": "/SUBSCRIPTIONS/{subscriptionId}/RESOURCEGROUPS/{resourceGroupName}/PROVIDERS/MICROSOFT.NETWORK/APPLICATIONGATEWAYS/{applicationGatewayName}",
  "operationName": "ApplicationGatewayFirewall",
  "time": "2017-03-20T15:52:09.1494499Z",
  "category": "ApplicationGatewayFirewallLog",
  "properties": {
    "instanceId": "ApplicationGatewayRole_IN_0",
    "clientIp": "104.210.252.3",
    "clientPort": "4835",
    "requestUri": "/?a=%3Cscript%3Ealert(%22Hello%22);%3C/script%3E",
    "ruleSetType": "OWASP",
    "ruleSetVersion": "3.0",
    "ruleId": "941320",
    "message": "Possible XSS Attack Detected - HTML Tag Handler",
    "action": "Blocked",
    "site": "Global",
    "details": {
      "message": "Warning. Pattern match \"<(a|abbr|acronym|address|applet|area|audioscope|b|base|basefront|bdo|bgsound|big|blackface|blink|blockquote|body|bq|br|button|caption|center|cite|code|col|colgroup|comment|dd|del|dfn|dir|div|dl|dt|em|embed|fieldset|fn|font|form|frame|frameset|h1|head|h ...\" at ARGS:a.",
      "data": "Matched Data: <script> found within ARGS:a: <script>alert(\\x22hello\\x22);</script>",
      "file": "rules/REQUEST-941-APPLICATION-ATTACK-XSS.conf",
      "line": "865"
    }
  }
} 

```

### <a name="view-and-analyze-hello-activity-log"></a><span data-ttu-id="ecaff-295">Ver e analisar o registo de atividade Olá</span><span class="sxs-lookup"><span data-stu-id="ecaff-295">View and analyze hello activity log</span></span>

<span data-ttu-id="ecaff-296">Pode ver e analisar dados de registo de atividade, utilizando qualquer um dos seguintes métodos de Olá:</span><span class="sxs-lookup"><span data-stu-id="ecaff-296">You can view and analyze activity log data by using any of hello following methods:</span></span>

* <span data-ttu-id="ecaff-297">**Ferramentas do Azure**: obter as informações do registo de atividade Olá através do Azure PowerShell, Olá CLI do Azure, Olá API de REST do Azure, ou Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="ecaff-297">**Azure tools**: Retrieve information from hello activity log through Azure PowerShell, hello Azure CLI, hello Azure REST API, or hello Azure portal.</span></span> <span data-ttu-id="ecaff-298">Instruções passo a passo para cada método passo são detalhadas no Olá [operações de atividade com o Resource Manager](../azure-resource-manager/resource-group-audit.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="ecaff-298">Step-by-step instructions for each method are detailed in hello [Activity operations with Resource Manager](../azure-resource-manager/resource-group-audit.md) article.</span></span>
* <span data-ttu-id="ecaff-299">**Power BI**: Se ainda não tiver um [Power BI](https://powerbi.microsoft.com/pricing) conta, pode experimentar, gratuitamente.</span><span class="sxs-lookup"><span data-stu-id="ecaff-299">**Power BI**: If you don't already have a [Power BI](https://powerbi.microsoft.com/pricing) account, you can try it for free.</span></span> <span data-ttu-id="ecaff-300">Ao utilizar Olá [conteúdo de registos de atividade do Azure pack para o Power BI](https://powerbi.microsoft.com/en-us/documentation/powerbi-content-pack-azure-audit-logs/), pode analisar os dados com dashboards pré-configuradas que podem ser utilizados como está, ou personalizar.</span><span class="sxs-lookup"><span data-stu-id="ecaff-300">By using hello [Azure Activity Logs content pack for Power BI](https://powerbi.microsoft.com/en-us/documentation/powerbi-content-pack-azure-audit-logs/), you can analyze your data with preconfigured dashboards that you can use as is or customize.</span></span>

### <a name="view-and-analyze-hello-access-performance-and-firewall-logs"></a><span data-ttu-id="ecaff-301">Ver e analisar registos de firewall, desempenho e acesso de Olá</span><span class="sxs-lookup"><span data-stu-id="ecaff-301">View and analyze hello access, performance, and firewall logs</span></span>

<span data-ttu-id="ecaff-302">Azure [Log Analytics](../log-analytics/log-analytics-azure-networking-analytics.md) pode recolher ficheiros de registo de eventos e contadores de Olá da sua conta de armazenamento de Blobs.</span><span class="sxs-lookup"><span data-stu-id="ecaff-302">Azure [Log Analytics](../log-analytics/log-analytics-azure-networking-analytics.md) can collect hello counter and event log files from your Blob storage account.</span></span> <span data-ttu-id="ecaff-303">Inclui as visualizações e tooanalyze de capacidades de pesquisa poderosas os seus registos.</span><span class="sxs-lookup"><span data-stu-id="ecaff-303">It includes visualizations and powerful search capabilities tooanalyze your logs.</span></span>

<span data-ttu-id="ecaff-304">Também pode ligar-se a conta de armazenamento tooyour e obter entradas de registo Olá JSON para os registos de acesso e o desempenho.</span><span class="sxs-lookup"><span data-stu-id="ecaff-304">You can also connect tooyour storage account and retrieve hello JSON log entries for access and performance logs.</span></span> <span data-ttu-id="ecaff-305">Depois de transferir ficheiros JSON Olá, pode convertê-los tooCSV e visualizá-los no Excel, Power BI ou qualquer outra ferramenta de visualização de dados.</span><span class="sxs-lookup"><span data-stu-id="ecaff-305">After you download hello JSON files, you can convert them tooCSV and view them in Excel, Power BI, or any other data-visualization tool.</span></span>

> [!TIP]
> <span data-ttu-id="ecaff-306">Se estiver familiarizado com conceitos básicos do alterar os valores de constantes e variáveis em c# e o Visual Studio, pode utilizar Olá [iniciar ferramentas de conversor](https://github.com/Azure-Samples/networking-dotnet-log-converter) disponíveis a partir do GitHub.</span><span class="sxs-lookup"><span data-stu-id="ecaff-306">If you are familiar with Visual Studio and basic concepts of changing values for constants and variables in C#, you can use hello [log converter tools](https://github.com/Azure-Samples/networking-dotnet-log-converter) available from GitHub.</span></span>
> 
> 

## <a name="metrics"></a><span data-ttu-id="ecaff-307">Métricas</span><span class="sxs-lookup"><span data-stu-id="ecaff-307">Metrics</span></span>

<span data-ttu-id="ecaff-308">As métricas são uma funcionalidade de certos recursos do Azure, onde pode ver os contadores de desempenho no portal de Olá.</span><span class="sxs-lookup"><span data-stu-id="ecaff-308">Metrics are a feature for certain Azure resources where you can view performance counters in hello portal.</span></span> <span data-ttu-id="ecaff-309">Gateway de aplicação, uma métrica está actualmente disponível.</span><span class="sxs-lookup"><span data-stu-id="ecaff-309">For Application Gateway, one metric is available now.</span></span> <span data-ttu-id="ecaff-310">Esta métrica é o débito e pode vê-lo no portal de Olá.</span><span class="sxs-lookup"><span data-stu-id="ecaff-310">This metric is throughput, and you can see it in hello portal.</span></span> <span data-ttu-id="ecaff-311">Procurar tooan gateway de aplicação e clique em **métricas**.</span><span class="sxs-lookup"><span data-stu-id="ecaff-311">Browse tooan application gateway and click **Metrics**.</span></span> <span data-ttu-id="ecaff-312">os valores de Olá tooview, selecione de débito no Olá **as métricas disponíveis** secção.</span><span class="sxs-lookup"><span data-stu-id="ecaff-312">tooview hello values, select throughput in hello **Available metrics** section.</span></span> <span data-ttu-id="ecaff-313">Olá seguinte imagem, pode ver um exemplo com filtros de Olá que pode utilizar dados de Olá toodisplay em intervalos de tempo diferente.</span><span class="sxs-lookup"><span data-stu-id="ecaff-313">In hello following image, you can see an example with hello filters that you can use toodisplay hello data in different time ranges.</span></span>

![Vista de métrica com filtros][5]

<span data-ttu-id="ecaff-315">toosee uma lista atual de métricas, consulte [suportado métricas com a monitorização do Azure](../monitoring-and-diagnostics/monitoring-supported-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="ecaff-315">toosee a current list of metrics, see [Supported metrics with Azure Monitor](../monitoring-and-diagnostics/monitoring-supported-metrics.md).</span></span>

### <a name="alert-rules"></a><span data-ttu-id="ecaff-316">Regras de alertas</span><span class="sxs-lookup"><span data-stu-id="ecaff-316">Alert rules</span></span>

<span data-ttu-id="ecaff-317">Pode começar a regras de alertas com base nas métricas para um recurso.</span><span class="sxs-lookup"><span data-stu-id="ecaff-317">You can start alert rules based on metrics for a resource.</span></span> <span data-ttu-id="ecaff-318">Por exemplo, um alerta pode chamar um webhook ou um administrador de e-mail, se o débito de Olá Olá do gateway de aplicação é acima, abaixo ou com um limiar durante um período especificado.</span><span class="sxs-lookup"><span data-stu-id="ecaff-318">For example, an alert can call a webhook or email an administrator if hello throughput of hello application gateway is above, below, or at a threshold for a specified period.</span></span>

<span data-ttu-id="ecaff-319">Olá seguinte exemplo explica-lhe criar uma regra de alerta que envia um administrador de tooan e-mail depois de falhas de débito um limiar:</span><span class="sxs-lookup"><span data-stu-id="ecaff-319">hello following example walks you through creating an alert rule that sends an email tooan administrator after throughput breaches a threshold:</span></span>

1. <span data-ttu-id="ecaff-320">Clique em **Adicionar alerta métrica** tooopen Olá **Adicionar regra** painel.</span><span class="sxs-lookup"><span data-stu-id="ecaff-320">Click **Add metric alert** tooopen hello **Add rule** blade.</span></span> <span data-ttu-id="ecaff-321">Também pode contactar este painel a partir do painel de métricas de Olá.</span><span class="sxs-lookup"><span data-stu-id="ecaff-321">You can also reach this blade from hello metrics blade.</span></span>

   ![Botão "Adicionar alerta métrica"][6]

2. <span data-ttu-id="ecaff-323">No Olá **Adicionar regra** painel, preencha o nome de Olá, condição, notificar secções e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="ecaff-323">On hello **Add rule** blade, fill out hello name, condition, and notify sections, and click **OK**.</span></span>

   * <span data-ttu-id="ecaff-324">No Olá **condição** Seletor, selecione um dos valores de Olá quatro: **maior**, **igual ou maior do que**, **menor**, ou  **Menor ou igual a**.</span><span class="sxs-lookup"><span data-stu-id="ecaff-324">In hello **Condition** selector, select one of hello four values: **Greater than**, **Greater than or equal**, **Less than**, or **Less than or equal to**.</span></span>

   * <span data-ttu-id="ecaff-325">No Olá **período** Seletor, selecione um período de 5 minutos too6 horas.</span><span class="sxs-lookup"><span data-stu-id="ecaff-325">In hello **Period** selector, select a period from 5 minutes too6 hours.</span></span>

   * <span data-ttu-id="ecaff-326">Se selecionar **proprietários, contribuintes e leitores de E-Mail**, e-mail Olá pode ser dinâmica com base nos utilizadores de Olá que tenham acesso toothat recursos.</span><span class="sxs-lookup"><span data-stu-id="ecaff-326">If you select **Email owners, contributors, and readers**, hello email can be dynamic based on hello users who have access toothat resource.</span></span> <span data-ttu-id="ecaff-327">Caso contrário, pode fornecer uma lista separada por vírgulas de utilizadores de Olá **administrador adicionais email(s)** caixa.</span><span class="sxs-lookup"><span data-stu-id="ecaff-327">Otherwise, you can provide a comma-separated list of users in hello **Additional administrator email(s)** box.</span></span>

   ![Adicionar o painel de regra][7]

<span data-ttu-id="ecaff-329">Se o limiar de Olá é quebrado, chega uma mensagem de e-mail que é semelhante toohello um no Olá seguinte imagem:</span><span class="sxs-lookup"><span data-stu-id="ecaff-329">If hello threshold is breached, an email that's similar toohello one in hello following image arrives:</span></span>

![Correio eletrónico para o limiar infringido][8]

<span data-ttu-id="ecaff-331">É apresentada uma lista de alertas depois de criar um alerta de métrico.</span><span class="sxs-lookup"><span data-stu-id="ecaff-331">A list of alerts appears after you create a metric alert.</span></span> <span data-ttu-id="ecaff-332">Fornece uma descrição geral de todas as regras de alerta de Olá.</span><span class="sxs-lookup"><span data-stu-id="ecaff-332">It provides an overview of all hello alert rules.</span></span>

![Lista de alertas e regras][9]

<span data-ttu-id="ecaff-334">toolearn mais informações sobre notificações de alertas, consulte [receber notificações de alerta](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="ecaff-334">toolearn more about alert notifications, see [Receive alert notifications](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span></span>

<span data-ttu-id="ecaff-335">toounderstand mais informações sobre webhooks e como pode utilizá-los com alertas, visite [configurar um webhook num alerta métrico Azure](../monitoring-and-diagnostics/insights-webhooks-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="ecaff-335">toounderstand more about webhooks and how you can use them with alerts, visit [Configure a webhook on an Azure metric alert](../monitoring-and-diagnostics/insights-webhooks-alerts.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="ecaff-336">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="ecaff-336">Next steps</span></span>

* <span data-ttu-id="ecaff-337">Visualizar registos de eventos e contadores utilizando [Log Analytics](../log-analytics/log-analytics-azure-networking-analytics.md).</span><span class="sxs-lookup"><span data-stu-id="ecaff-337">Visualize counter and event logs by using [Log Analytics](../log-analytics/log-analytics-azure-networking-analytics.md).</span></span>
* <span data-ttu-id="ecaff-338">[Visualizar o registo de atividade do Azure com Power BI](http://blogs.msdn.com/b/powerbi/archive/2015/09/30/monitor-azure-audit-logs-with-power-bi.aspx) blogue.</span><span class="sxs-lookup"><span data-stu-id="ecaff-338">[Visualize your Azure activity log with Power BI](http://blogs.msdn.com/b/powerbi/archive/2015/09/30/monitor-azure-audit-logs-with-power-bi.aspx) blog post.</span></span>
* <span data-ttu-id="ecaff-339">[Ver e analisar registos de atividade do Azure no Power BI e muito mais](https://azure.microsoft.com/blog/analyze-azure-audit-logs-in-powerbi-more/) blogue.</span><span class="sxs-lookup"><span data-stu-id="ecaff-339">[View and analyze Azure activity logs in Power BI and more](https://azure.microsoft.com/blog/analyze-azure-audit-logs-in-powerbi-more/) blog post.</span></span>

[1]: ./media/application-gateway-diagnostics/figure1.png
[2]: ./media/application-gateway-diagnostics/figure2.png
[3]: ./media/application-gateway-diagnostics/figure3.png
[4]: ./media/application-gateway-diagnostics/figure4.png
[5]: ./media/application-gateway-diagnostics/figure5.png
[6]: ./media/application-gateway-diagnostics/figure6.png
[7]: ./media/application-gateway-diagnostics/figure7.png
[8]: ./media/application-gateway-diagnostics/figure8.png
[9]: ./media/application-gateway-diagnostics/figure9.png
[10]: ./media/application-gateway-diagnostics/figure10.png
