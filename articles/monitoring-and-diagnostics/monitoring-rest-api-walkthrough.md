---
title: "aaaAzure instruções de monitorização REST API | Microsoft Docs"
description: "Como tooauthenticate pedidos tooand utilize Olá API de REST de monitorização do Azure."
author: mcollier
manager: 
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 565e6a88-3131-4a48-8b82-3effc9a3d5c6
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/27/2016
ms.author: mcollier
ms.openlocfilehash: b8ae3a03fd21af872f1dc5fed40a101a24ca1652
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-monitoring-rest-api-walkthrough"></a><span data-ttu-id="fd362-103">Instruções de API de REST de monitorização do Azure</span><span class="sxs-lookup"><span data-stu-id="fd362-103">Azure Monitoring REST API Walkthrough</span></span>
<span data-ttu-id="fd362-104">Este artigo mostra como autenticação tooperform pelo seu código pode utilizar Olá [referência de API de REST do Microsoft Azure Monitor](https://msdn.microsoft.com/library/azure/dn931943.aspx).</span><span class="sxs-lookup"><span data-stu-id="fd362-104">This article shows you how tooperform authentication so your code can use hello [Microsoft Azure Monitor REST API Reference](https://msdn.microsoft.com/library/azure/dn931943.aspx).</span></span>         

<span data-ttu-id="fd362-105">Olá API de Monitor do Azure torna possível tooprogrammatically obter Olá predefinidas disponíveis as definições de métrica (tipo de Olá de métrica de tempo de CPU, pedidos, etc.), granularidade e valores de métricos.</span><span class="sxs-lookup"><span data-stu-id="fd362-105">hello Azure Monitor API makes it possible tooprogrammatically retrieve hello available default metric definitions (hello type of metric such as CPU Time, Requests, etc.), granularity, and metric values.</span></span> <span data-ttu-id="fd362-106">Depois de obtido, dados de Olá podem ser guardados num arquivo de dados separada, como SQL Database do Azure, base de dados do Azure Cosmos ou do Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="fd362-106">Once retrieved, hello data can be saved in a separate data store such as Azure SQL Database, Azure Cosmos DB, or Azure Data Lake.</span></span> <span data-ttu-id="fd362-107">A partir daí analysis adicionais podem ser efetuadas conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="fd362-107">From there additional analysis can be performed as needed.</span></span>

<span data-ttu-id="fd362-108">Para além de trabalhar com vários pontos de dados métricos, como este artigo demonstra, Olá Monitor API torna regras de alertas possíveis toolist, ver registos de atividade e muito mais.</span><span class="sxs-lookup"><span data-stu-id="fd362-108">Besides working with various metric data points, as this article demonstrates, hello Monitor API makes it possible toolist alert rules, view activity logs, and much more.</span></span> <span data-ttu-id="fd362-109">Para obter uma lista completa de operações disponíveis, consulte Olá [referência de API de REST do Microsoft Azure Monitor](https://msdn.microsoft.com/library/azure/dn931943.aspx).</span><span class="sxs-lookup"><span data-stu-id="fd362-109">For a full list of available operations, see hello [Microsoft Azure Monitor REST API Reference](https://msdn.microsoft.com/library/azure/dn931943.aspx).</span></span>

## <a name="authenticating-azure-monitor-requests"></a><span data-ttu-id="fd362-110">Autenticar pedidos de monitorização do Azure</span><span class="sxs-lookup"><span data-stu-id="fd362-110">Authenticating Azure Monitor Requests</span></span>
<span data-ttu-id="fd362-111">Step-by-Olá primeiro passo é o pedido de Olá tooauthenticate.</span><span class="sxs-lookup"><span data-stu-id="fd362-111">hello first step is tooauthenticate hello request.</span></span>

<span data-ttu-id="fd362-112">Todas as tarefas de Olá executadas contra modelo de autenticação de Azure Resource Manager Utilize Olá Olá API de Monitor do Azure.</span><span class="sxs-lookup"><span data-stu-id="fd362-112">All hello tasks executed against hello Azure Monitor API use hello Azure Resource Manager authentication model.</span></span> <span data-ttu-id="fd362-113">Por conseguinte, todos os pedidos têm de ser autenticados no Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="fd362-113">Therefore, all requests must be authenticated with Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="fd362-114">Uma aplicação de cliente do Olá tooauthenticate abordagem é toocreate um principal de serviço do Azure AD e obter Olá token de autenticação (JWT).</span><span class="sxs-lookup"><span data-stu-id="fd362-114">One approach tooauthenticate hello client application is toocreate an Azure AD service principal and retrieve hello authentication (JWT) token.</span></span> <span data-ttu-id="fd362-115">Olá script de exemplo seguinte demonstra a criar um Azure AD principal de serviço através do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="fd362-115">hello following sample script demonstrates creating an Azure AD service principal via PowerShell.</span></span> <span data-ttu-id="fd362-116">Para instruções mais detalhadas, consulte a documentação do toohello no [utilizando o Azure PowerShell toocreate um recursos de principal tooaccess de serviço](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-password).</span><span class="sxs-lookup"><span data-stu-id="fd362-116">For a more detailed walk-through, refer toohello documentation on [using Azure PowerShell toocreate a service principal tooaccess resources](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-password).</span></span> <span data-ttu-id="fd362-117">É também possível demasiado[criar um principal de serviço através do portal do Azure de Olá](../azure-resource-manager/resource-group-create-service-principal-portal.md).</span><span class="sxs-lookup"><span data-stu-id="fd362-117">It is also possible too[create a service principal via hello Azure portal](../azure-resource-manager/resource-group-create-service-principal-portal.md).</span></span>

```PowerShell
$subscriptionId = "{azure-subscription-id}"
$resourceGroupName = "{resource-group-name}"
$location = "centralus"

# Authenticate tooa specific Azure subscription.
Login-AzureRmAccount -SubscriptionId $subscriptionId

# Password for hello service principal
$pwd = "{service-principal-password}"

# Create a new Azure AD application
$azureAdApplication = New-AzureRmADApplication `
                        -DisplayName "My Azure Monitor" `
                        -HomePage "https://localhost/azure-monitor" `
                        -IdentifierUris "https://localhost/azure-monitor" `
                        -Password $pwd

# Create a new service principal associated with hello designated application
New-AzureRmADServicePrincipal -ApplicationId $azureAdApplication.ApplicationId

# Assign Reader role toohello newly created service principal
New-AzureRmRoleAssignment -RoleDefinitionName Reader `
                          -ServicePrincipalName $azureAdApplication.ApplicationId.Guid

```

<span data-ttu-id="fd362-118">Olá tooquery API de Monitor do Azure, aplicação de cliente Olá deve utilizar Olá tooauthenticate principal de serviço que criou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="fd362-118">tooquery hello Azure Monitor API, hello client application should use hello previously created service principal tooauthenticate.</span></span> <span data-ttu-id="fd362-119">Olá seguinte script do PowerShell de exemplo mostra uma abordagem, utilizando Olá [Active Directory Authentication Library](../active-directory/active-directory-authentication-libraries.md) (ADAL) toohelp obter autenticação de JWT Olá token.</span><span class="sxs-lookup"><span data-stu-id="fd362-119">hello following example PowerShell script shows one approach, using hello [Active Directory Authentication Library](../active-directory/active-directory-authentication-libraries.md) (ADAL) toohelp get hello JWT authentication token.</span></span> <span data-ttu-id="fd362-120">token JWT de Olá é transmitida como parte de um parâmetro de autorização de HTTP no pedidos toohello API de REST de Monitor do Azure.</span><span class="sxs-lookup"><span data-stu-id="fd362-120">hello JWT token is passed as part of an HTTP Authorization parameter in requests toohello Azure Monitor REST API.</span></span>

```PowerShell
$azureAdApplication = Get-AzureRmADApplication -IdentifierUri "https://localhost/azure-monitor"

$subscription = Get-AzureRmSubscription -SubscriptionId $subscriptionId

$clientId = $azureAdApplication.ApplicationId.Guid
$tenantId = $subscription.TenantId
$authUrl = "https://login.microsoftonline.com/${tenantId}"

$AuthContext = [Microsoft.IdentityModel.Clients.ActiveDirectory.AuthenticationContext]$authUrl
$cred = New-Object -TypeName Microsoft.IdentityModel.Clients.ActiveDirectory.ClientCredential -ArgumentList ($clientId, $pwd)

$result = $AuthContext.AcquireToken("https://management.core.windows.net/", $cred)

# Build an array of HTTP header values
$authHeader = @{
'Content-Type'='application/json'
'Accept'='application/json'
'Authorization'=$result.CreateAuthorizationHeader()
}
```

<span data-ttu-id="fd362-121">Após a conclusão do passo de configuração de autenticação de Olá, em seguida, pode executar consultas contra Olá API de REST de Monitor do Azure.</span><span class="sxs-lookup"><span data-stu-id="fd362-121">Once hello authentication setup step is complete, queries can then be executed against hello Azure Monitor REST API.</span></span> <span data-ttu-id="fd362-122">Existem duas consultas úteis:</span><span class="sxs-lookup"><span data-stu-id="fd362-122">There are two helpful queries:</span></span>

1. <span data-ttu-id="fd362-123">Lista as definições de métrica Olá para um recurso</span><span class="sxs-lookup"><span data-stu-id="fd362-123">List hello metric definitions for a resource</span></span>
2. <span data-ttu-id="fd362-124">Obter valores de métrica de Olá</span><span class="sxs-lookup"><span data-stu-id="fd362-124">Retrieve hello metric values</span></span>

## <a name="retrieve-metric-definitions"></a><span data-ttu-id="fd362-125">Obter as definições de métrica</span><span class="sxs-lookup"><span data-stu-id="fd362-125">Retrieve Metric Definitions</span></span>
> [!NOTE]
> <span data-ttu-id="fd362-126">tooretrieve as definições de métrica utilizando Olá API de REST de Monitor do Azure, utilize "2016-03-01" Olá, versão de API.</span><span class="sxs-lookup"><span data-stu-id="fd362-126">tooretrieve metric definitions using hello Azure Monitor REST API, use "2016-03-01" as hello API version.</span></span>
>
>

```PowerShell
$apiVersion = "2016-03-01"
$request = "https://management.azure.com/subscriptions/${subscriptionId}/resourceGroups/${resourceGroupName}/providers/${resourceProviderNamespace}/${resourceType}/${resourceName}/providers/microsoft.insights/metricDefinitions?api-version=${apiVersion}"

Invoke-RestMethod -Uri $request `
                  -Headers $authHeader `
                  -Method Get `
                  -Verbose
```
<span data-ttu-id="fd362-127">Para uma aplicação lógica do Azure, as definições de métrica de Olá aparecia toohello semelhante captura de ecrã a seguir:</span><span class="sxs-lookup"><span data-stu-id="fd362-127">For an Azure Logic App, hello metric definitions would appear similar toohello following screenshot:</span></span>

![ALT "Vista JSON da resposta de definição de métrica".](./media/monitoring-rest-api-walkthrough/available_metric_definitions_logic_app_json_response_clean.png)

<span data-ttu-id="fd362-129">Para obter mais informações, consulte Olá [lista as definições de métrica Olá para um recurso na API REST da Azure Monitor](https://msdn.microsoft.com/library/azure/mt743621.aspx) documentação.</span><span class="sxs-lookup"><span data-stu-id="fd362-129">For more information, see hello [List hello metric definitions for a resource in Azure Monitor REST API](https://msdn.microsoft.com/library/azure/mt743621.aspx) documentation.</span></span>

## <a name="retrieve-metric-values"></a><span data-ttu-id="fd362-130">Obter valores de métricos</span><span class="sxs-lookup"><span data-stu-id="fd362-130">Retrieve Metric Values</span></span>
<span data-ttu-id="fd362-131">Assim que as definições de métrica disponível Olá são conhecidas, é, em seguida, tooretrieve possíveis Olá os valores de métricos relacionados.</span><span class="sxs-lookup"><span data-stu-id="fd362-131">Once hello available metric definitions are known, it is then possible tooretrieve hello related metric values.</span></span> <span data-ttu-id="fd362-132">Utilize nome 'value' da métrica de Olá (não Olá 'localizedValue') para quaisquer pedidos filtragem (por exemplo, obter Olá 'CpuTime' e 'Pedidos' Métrica pontos de dados).</span><span class="sxs-lookup"><span data-stu-id="fd362-132">Use hello metric’s name ‘value’ (not hello ‘localizedValue’) for any filtering requests (for example, retrieve hello ‘CpuTime’ and ‘Requests’ metric data points).</span></span> <span data-ttu-id="fd362-133">Se não existem filtros forem especificados, é devolvida métrica da predefinição de Olá.</span><span class="sxs-lookup"><span data-stu-id="fd362-133">If no filters are specified, hello default metric is returned.</span></span>

> [!NOTE]
> <span data-ttu-id="fd362-134">os valores de métrica tooretrieve utilizando Olá API de REST de Monitor do Azure, utilize "2016-06-01" Olá versão da API.</span><span class="sxs-lookup"><span data-stu-id="fd362-134">tooretrieve metric values using hello Azure Monitor REST API, use "2016-06-01" as hello API version.</span></span>
>
>

<span data-ttu-id="fd362-135">**Método**: introdução</span><span class="sxs-lookup"><span data-stu-id="fd362-135">**Method**: GET</span></span>

<span data-ttu-id="fd362-136">**URI de pedido**: https://management.azure.com/subscriptions/*{id de subscrição}*/resourceGroups/*{nome de grupo de recursos}*/providers/*{ recursos-fornecedor-namespace}*/*{tipo de recurso}*/*{nome do recurso}*/providers/microsoft.insights/metrics?$filter= *{filtro}*& api-version =*{apiVersion}*</span><span class="sxs-lookup"><span data-stu-id="fd362-136">**Request URI**: https://management.azure.com/subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/*{resource-provider-namespace}*/*{resource-type}*/*{resource-name}*/providers/microsoft.insights/metrics?$filter=*{filter}*&api-version=*{apiVersion}*</span></span>

<span data-ttu-id="fd362-137">Por exemplo, tooretrieve Olá RunsSucceeded métrica dos pontos de dados para Olá dado intervalo de tempo e um grão de tempo de 1 hora, o pedido de Olá seria o seguinte:</span><span class="sxs-lookup"><span data-stu-id="fd362-137">For example, tooretrieve hello RunsSucceeded metric data points for hello given time range and for a time grain of 1 hour, hello request would be as follows:</span></span>

```PowerShell
$apiVersion = "2016-06-01"
$filter = "(name.value eq 'RunsSucceeded') and aggregationType eq 'Total' and startTime eq 2016-09-23 and endTime eq 2016-09-24 and timeGrain eq duration'PT1H'"
$request = "https://management.azure.com/subscriptions/${subscriptionId}/resourceGroups/${resourceGroupName}/providers/${resourceProviderNamespace}/${resourceType}/${resourceName}/providers/microsoft.insights/metrics?`$filter=${filter}&api-version=${apiVersion}"
(Invoke-RestMethod -Uri $request `
                   -Headers $authHeader `
                   -Method Get `
                   -Verbose).Value | ConvertTo-Json
```

<span data-ttu-id="fd362-138">resultado de Olá aparecia semelhante toohello exemplo que segue captura de ecrã:</span><span class="sxs-lookup"><span data-stu-id="fd362-138">hello result would appear similar toohello example following screenshot:</span></span>

![ALT "Com o valor de métrica de tempo de resposta médio de resposta JSON"](./media/monitoring-rest-api-walkthrough/available_metrics_logic_app_json_response.png)

<span data-ttu-id="fd362-140">tooretrieve pontos de dados de várias ou agregação, adicione os nomes de definição de métrica de Olá e o filtro de toohello de tipos de agregação, como mostrado no seguinte exemplo de Olá:</span><span class="sxs-lookup"><span data-stu-id="fd362-140">tooretrieve multiple data or aggregation points, add hello metric definition names and aggregation types toohello filter, as seen in hello following example:</span></span>

```PowerShell
$apiVersion = "2016-06-01"
$filter = "(name.value eq 'ActionsCompleted' or name.value eq 'RunsSucceeded') and (aggregationType eq 'Total' or aggregationType eq 'Average') and startTime eq 2016-09-23T13:30:00Z and endTime eq 2016-09-23T14:30:00Z and timeGrain eq duration'PT1M'"
$request = "https://management.azure.com/subscriptions/${subscriptionId}/resourceGroups/${resourceGroupName}/providers/${resourceProviderNamespace}/${resourceType}/${resourceName}/providers/microsoft.insights/metrics?`$filter=${filter}&api-version=${apiVersion}"
(Invoke-RestMethod -Uri $request `
                   -Headers $authHeader `
                   -Method Get `
                   -Verbose).Value | ConvertTo-Json
```

### <a name="use-armclient"></a><span data-ttu-id="fd362-141">Utilizar ARMClient</span><span class="sxs-lookup"><span data-stu-id="fd362-141">Use ARMClient</span></span>
<span data-ttu-id="fd362-142">Uma alternativa toousing PowerShell (conforme mostrado acima), é toouse [ARMClient](https://github.com/projectkudu/ARMClient) no seu computador Windows.</span><span class="sxs-lookup"><span data-stu-id="fd362-142">An alternative toousing PowerShell (as shown above), is toouse [ARMClient](https://github.com/projectkudu/ARMClient) on your Windows machine.</span></span> <span data-ttu-id="fd362-143">ARMClient processa a autenticação de Olá do Azure AD (e resultante token JWT) automaticamente.</span><span class="sxs-lookup"><span data-stu-id="fd362-143">ARMClient handles hello Azure AD authentication (and resulting JWT token) automatically.</span></span> <span data-ttu-id="fd362-144">Olá passos seguintes descrevem a utilização de ARMClient para obter os dados métricos:</span><span class="sxs-lookup"><span data-stu-id="fd362-144">hello following steps outline use of ARMClient for retrieving metric data:</span></span>

1. <span data-ttu-id="fd362-145">Instalar [Chocolatey](https://chocolatey.org/) e [ARMClient](https://github.com/projectkudu/ARMClient).</span><span class="sxs-lookup"><span data-stu-id="fd362-145">Install [Chocolatey](https://chocolatey.org/) and [ARMClient](https://github.com/projectkudu/ARMClient).</span></span>
2. <span data-ttu-id="fd362-146">Na janela de terminal, escreva *armclient.exe início de sessão*.</span><span class="sxs-lookup"><span data-stu-id="fd362-146">In a terminal window, type *armclient.exe login*.</span></span> <span data-ttu-id="fd362-147">Isto irá pedir-lhe toolog no tooAzure.</span><span class="sxs-lookup"><span data-stu-id="fd362-147">This prompts you toolog in tooAzure.</span></span>
3. <span data-ttu-id="fd362-148">Tipo *armclient GET [your_resource_id]/providers/microsoft.insights/metricdefinitions?api-version=2016-03-01*</span><span class="sxs-lookup"><span data-stu-id="fd362-148">Type *armclient GET [your_resource_id]/providers/microsoft.insights/metricdefinitions?api-version=2016-03-01*</span></span>
4. <span data-ttu-id="fd362-149">Tipo *armclient GET [your_resource_id]/providers/microsoft.insights/metrics?api-version=2016-06-01*</span><span class="sxs-lookup"><span data-stu-id="fd362-149">Type *armclient GET [your_resource_id]/providers/microsoft.insights/metrics?api-version=2016-06-01*</span></span>

![ALT "Using ARMClient toowork com Olá API de REST de monitorização do Azure"](./media/monitoring-rest-api-walkthrough/armclient_metricdefinitions.png)

## <a name="retrieve-hello-resource-id"></a><span data-ttu-id="fd362-151">Obter Olá ID de recurso</span><span class="sxs-lookup"><span data-stu-id="fd362-151">Retrieve hello Resource ID</span></span>
<span data-ttu-id="fd362-152">Utilizando a REST API de Olá realmente pode ajudar toounderstand Olá disponíveis as definições de métrica, granularidade e os valores relacionados.</span><span class="sxs-lookup"><span data-stu-id="fd362-152">Using hello REST API can really help toounderstand hello available metric definitions, granularity, and related values.</span></span> <span data-ttu-id="fd362-153">Essa informação é útil quando utilizar Olá [biblioteca de gestão do Azure](https://msdn.microsoft.com/library/azure/mt417623.aspx).</span><span class="sxs-lookup"><span data-stu-id="fd362-153">That information is helpful when using hello [Azure Management Library](https://msdn.microsoft.com/library/azure/mt417623.aspx).</span></span>

<span data-ttu-id="fd362-154">Para Olá precedente código, toouse de ID de recurso Olá é Olá caminho completo toohello pretendido recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="fd362-154">For hello preceding code, hello resource ID toouse is hello full path toohello desired Azure resource.</span></span> <span data-ttu-id="fd362-155">Por exemplo, tooquery em relação a uma aplicação Web do Azure, ID de recurso Olá seria:</span><span class="sxs-lookup"><span data-stu-id="fd362-155">For example, tooquery against an Azure Web App, hello resource ID would be:</span></span>

<span data-ttu-id="fd362-156">*/subscriptions/{Subscription-ID}/resourceGroups/{Resource-group-name}/providers/Microsoft.Web/sites/{site-name}/*</span><span class="sxs-lookup"><span data-stu-id="fd362-156">*/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{site-name}/*</span></span>

<span data-ttu-id="fd362-157">Olá lista seguinte contém alguns exemplos de formatos de ID de recurso para vários recursos do Azure:</span><span class="sxs-lookup"><span data-stu-id="fd362-157">hello following list contains a few examples of resource ID formats for various Azure resources:</span></span>

* <span data-ttu-id="fd362-158">**IoT Hub** -/subscriptions/{targetsubscriptionid}/resourcegroups/{targetresourcegroupname}*{id de subscrição}*/resourceGroups/*{nome de grupo de recursos}*/providers/Microsoft.Devices/IotHubs/*{iot-hub-name}*</span><span class="sxs-lookup"><span data-stu-id="fd362-158">**IoT Hub** - /subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/Microsoft.Devices/IotHubs/*{iot-hub-name}*</span></span>
* <span data-ttu-id="fd362-159">**Agrupamento elástico de SQL** -/subscriptions/{targetsubscriptionid}/resourcegroups/{targetresourcegroupname}*{id de subscrição}*/resourceGroups/*{nome de grupo de recursos}*/providers/Microsoft.Sql/servers/*{conjunto-db}*/elasticpools/*{nome de conjunto de sql}*</span><span class="sxs-lookup"><span data-stu-id="fd362-159">**Elastic SQL Pool** - /subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/Microsoft.Sql/servers/*{pool-db}*/elasticpools/*{sql-pool-name}*</span></span>
* <span data-ttu-id="fd362-160">**Base de dados do SQL (v12)** -/subscriptions/{targetsubscriptionid}/resourcegroups/{targetresourcegroupname}*{id de subscrição}*/resourceGroups/*{nome de grupo de recursos}*/providers/Microsoft.Sql/servers/*{nome do servidor}* /databases/*{nome-base de dados}*</span><span class="sxs-lookup"><span data-stu-id="fd362-160">**SQL Database (v12)** - /subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/Microsoft.Sql/servers/*{server-name}*/databases/*{database-name}*</span></span>
* <span data-ttu-id="fd362-161">**Barramento de serviço** -/subscriptions/{targetsubscriptionid}/resourcegroups/{targetresourcegroupname}*{id de subscrição}*/resourceGroups/*{nome de grupo de recursos}*/providers/Microsoft.ServiceBus/*{namespace}* / *{nome-servicebus}*</span><span class="sxs-lookup"><span data-stu-id="fd362-161">**Service Bus** - /subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/Microsoft.ServiceBus/*{namespace}*/*{servicebus-name}*</span></span>
* <span data-ttu-id="fd362-162">**Conjuntos de dimensionamento de VM** -/subscriptions/{targetsubscriptionid}/resourcegroups/{targetresourcegroupname}*{id de subscrição}*/resourceGroups/*{nome de grupo de recursos}*/providers/Microsoft.Compute/virtualMachineScaleSets/*{ nome da VM}*</span><span class="sxs-lookup"><span data-stu-id="fd362-162">**VM Scale Sets** - /subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/Microsoft.Compute/virtualMachineScaleSets/*{vm-name}*</span></span>
* <span data-ttu-id="fd362-163">**VMs** -/subscriptions/{targetsubscriptionid}/resourcegroups/{targetresourcegroupname}*{id de subscrição}*/resourceGroups/*{nome de grupo de recursos}*/providers/Microsoft.Compute/virtualMachines/*{nome da vm}*</span><span class="sxs-lookup"><span data-stu-id="fd362-163">**VMs** - /subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/Microsoft.Compute/virtualMachines/*{vm-name}*</span></span>
* <span data-ttu-id="fd362-164">**Os Event Hubs** -/subscriptions/{targetsubscriptionid}/resourcegroups/{targetresourcegroupname}*{id de subscrição}*/resourceGroups/*{nome de grupo de recursos}*/providers/Microsoft.EventHub/namespaces/*{ eventhub-namespace}*</span><span class="sxs-lookup"><span data-stu-id="fd362-164">**Event Hubs** - /subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/Microsoft.EventHub/namespaces/*{eventhub-namespace}*</span></span>

<span data-ttu-id="fd362-165">Existem abordagens alternativas tooretrieving Olá ID de recurso, incluindo a utilização do Explorador de recursos do Azure, visualizar recursos Olá pretendido na Olá portal do Azure e através do PowerShell ou Olá CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="fd362-165">There are alternative approaches tooretrieving hello resource ID, including using Azure Resource Explorer, viewing hello desired resource in hello Azure portal, and via PowerShell or hello Azure CLI.</span></span>

### <a name="azure-resource-explorer"></a><span data-ttu-id="fd362-166">Explorador de Recursos do Azure</span><span class="sxs-lookup"><span data-stu-id="fd362-166">Azure Resource Explorer</span></span>
<span data-ttu-id="fd362-167">ID do recurso de Olá toofind para um recurso pretendido, uma abordagem útil é toouse Olá [Explorador de recursos do Azure](https://resources.azure.com) ferramenta.</span><span class="sxs-lookup"><span data-stu-id="fd362-167">toofind hello resource ID for a desired resource, one helpful approach is toouse hello [Azure Resource Explorer](https://resources.azure.com) tool.</span></span> <span data-ttu-id="fd362-168">Navegue recursos toohello pretendido e, em seguida, observe o ID de Olá apresentado, tal como em Olá captura de ecrã a seguir:</span><span class="sxs-lookup"><span data-stu-id="fd362-168">Navigate toohello desired resource and then look at hello ID shown, as in hello following screenshot:</span></span>

![ALT "Explorador de recursos do Azure"](./media/monitoring-rest-api-walkthrough/azure_resource_explorer.png)

### <a name="azure-portal"></a><span data-ttu-id="fd362-170">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="fd362-170">Azure portal</span></span>
<span data-ttu-id="fd362-171">Pode também obter o ID de recurso Olá Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="fd362-171">hello resource ID can also be obtained from hello Azure portal.</span></span> <span data-ttu-id="fd362-172">toodo por isso, navegue até recursos toohello pretendido e, em seguida, selecione propriedades.</span><span class="sxs-lookup"><span data-stu-id="fd362-172">toodo so, navigate toohello desired resource and then select Properties.</span></span> <span data-ttu-id="fd362-173">Olá ID de recurso é apresentado no painel de propriedades de Olá, como mostrado na seguinte captura de ecrã de Olá:</span><span class="sxs-lookup"><span data-stu-id="fd362-173">hello Resource ID is displayed in hello Properties blade, as seen in hello following screenshot:</span></span>

![ALT "ID de recurso apresentado no painel de propriedades de Olá no Olá portal do Azure"](./media/monitoring-rest-api-walkthrough/resourceid_azure_portal.png)

### <a name="azure-powershell"></a><span data-ttu-id="fd362-175">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="fd362-175">Azure PowerShell</span></span>
<span data-ttu-id="fd362-176">ID de recurso Olá pode ser obtido utilizando cmdlets do PowerShell do Azure.</span><span class="sxs-lookup"><span data-stu-id="fd362-176">hello resource ID can be retrieved using Azure PowerShell cmdlets as well.</span></span> <span data-ttu-id="fd362-177">Por exemplo, tooobtain Olá ID de recurso para uma aplicação Web do Azure, execute o cmdlet Olá Get-AzureRmWebApp, tal como em Olá seguinte captura de ecrã:</span><span class="sxs-lookup"><span data-stu-id="fd362-177">For example, tooobtain hello resource ID for an Azure Web App, execute hello Get-AzureRmWebApp cmdlet, as in hello following screenshot:</span></span>

![ALT "ID de recurso obtido através do PowerShell"](./media/monitoring-rest-api-walkthrough/resourceid_powershell.png)

### <a name="azure-cli"></a><span data-ttu-id="fd362-179">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="fd362-179">Azure CLI</span></span>
<span data-ttu-id="fd362-180">tooretrieve Olá ID de recurso utilizando Olá CLI do Azure, execute o comando de "Mostrar webapp do azure" Olá, especificando Olá ' – json' opção, conforme mostrado na seguinte captura de ecrã de Olá:</span><span class="sxs-lookup"><span data-stu-id="fd362-180">tooretrieve hello resource ID using hello Azure CLI, execute hello 'azure webapp show' command, specifying hello '--json' option, as shown in hello following screenshot:</span></span>

![ALT "ID de recurso obtido através do PowerShell"](./media/monitoring-rest-api-walkthrough/resourceid_azurecli.png)

## <a name="retrieve-activity-log-data"></a><span data-ttu-id="fd362-182">Obter dados de registo de atividade</span><span class="sxs-lookup"><span data-stu-id="fd362-182">Retrieve Activity Log Data</span></span>
<span data-ttu-id="fd362-183">Adição tooworking com as definições de métrica e os valores relacionados, é também possível tooretrieve interessantes insights relacionados tooAzure recursos adicionais.</span><span class="sxs-lookup"><span data-stu-id="fd362-183">In addition tooworking with metric definitions and related values, it is also possible tooretrieve additional interesting insights related tooAzure resources.</span></span> <span data-ttu-id="fd362-184">Por exemplo, é possível tooquery [registo de atividade](https://msdn.microsoft.com/library/azure/dn931934.aspx) dados.</span><span class="sxs-lookup"><span data-stu-id="fd362-184">As an example, it is possible tooquery [activity log](https://msdn.microsoft.com/library/azure/dn931934.aspx) data.</span></span> <span data-ttu-id="fd362-185">Olá exemplo seguinte demonstra com Olá os dados de registo da atividade de tooquery de API REST da Azure Monitor dentro de um intervalo de datas específico para uma subscrição do Azure:</span><span class="sxs-lookup"><span data-stu-id="fd362-185">hello following sample demonstrates using hello Azure Monitor REST API tooquery activity log data within a specific date range for an Azure subscription:</span></span>

```PowerShell
$apiVersion = "2014-04-01"
$filter = "eventTimestamp ge '2016-09-23' and eventTimestamp le '2016-09-24'and eventChannels eq 'Admin, Operation'"
$request = "https://management.azure.com/subscriptions/${subscriptionId}/providers/microsoft.insights/eventtypes/management/values?api-version=${apiVersion}&`$filter=${filter}"
(Invoke-RestMethod -Uri $request `
                   -Headers $authHeader `
                   -Method Get `
                   -Verbose).Value | ConvertTo-Json
```

## <a name="next-steps"></a><span data-ttu-id="fd362-186">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="fd362-186">Next steps</span></span>
* <span data-ttu-id="fd362-187">Olá revisão [descrição geral da monitorização](monitoring-overview.md).</span><span class="sxs-lookup"><span data-stu-id="fd362-187">Review hello [Overview of Monitoring](monitoring-overview.md).</span></span>
* <span data-ttu-id="fd362-188">Olá vista [suportado métricas com a monitorização do Azure](monitoring-supported-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="fd362-188">View hello [Supported metrics with Azure Monitor](monitoring-supported-metrics.md).</span></span>
* <span data-ttu-id="fd362-189">Olá revisão [referência de API de REST do Microsoft Azure Monitor](https://msdn.microsoft.com/library/azure/dn931943.aspx).</span><span class="sxs-lookup"><span data-stu-id="fd362-189">Review hello [Microsoft Azure Monitor REST API Reference](https://msdn.microsoft.com/library/azure/dn931943.aspx).</span></span>
* <span data-ttu-id="fd362-190">Olá revisão [biblioteca de gestão do Azure](https://msdn.microsoft.com/library/azure/mt417623.aspx).</span><span class="sxs-lookup"><span data-stu-id="fd362-190">Review hello [Azure Management Library](https://msdn.microsoft.com/library/azure/mt417623.aspx).</span></span>
