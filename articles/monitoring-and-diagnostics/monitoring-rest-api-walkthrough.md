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
# <a name="azure-monitoring-rest-api-walkthrough"></a>Instruções de API de REST de monitorização do Azure
Este artigo mostra como autenticação tooperform pelo seu código pode utilizar Olá [referência de API de REST do Microsoft Azure Monitor](https://msdn.microsoft.com/library/azure/dn931943.aspx).         

Olá API de Monitor do Azure torna possível tooprogrammatically obter Olá predefinidas disponíveis as definições de métrica (tipo de Olá de métrica de tempo de CPU, pedidos, etc.), granularidade e valores de métricos. Depois de obtido, dados de Olá podem ser guardados num arquivo de dados separada, como SQL Database do Azure, base de dados do Azure Cosmos ou do Azure Data Lake. A partir daí analysis adicionais podem ser efetuadas conforme necessário.

Para além de trabalhar com vários pontos de dados métricos, como este artigo demonstra, Olá Monitor API torna regras de alertas possíveis toolist, ver registos de atividade e muito mais. Para obter uma lista completa de operações disponíveis, consulte Olá [referência de API de REST do Microsoft Azure Monitor](https://msdn.microsoft.com/library/azure/dn931943.aspx).

## <a name="authenticating-azure-monitor-requests"></a>Autenticar pedidos de monitorização do Azure
Step-by-Olá primeiro passo é o pedido de Olá tooauthenticate.

Todas as tarefas de Olá executadas contra modelo de autenticação de Azure Resource Manager Utilize Olá Olá API de Monitor do Azure. Por conseguinte, todos os pedidos têm de ser autenticados no Azure Active Directory (Azure AD). Uma aplicação de cliente do Olá tooauthenticate abordagem é toocreate um principal de serviço do Azure AD e obter Olá token de autenticação (JWT). Olá script de exemplo seguinte demonstra a criar um Azure AD principal de serviço através do PowerShell. Para instruções mais detalhadas, consulte a documentação do toohello no [utilizando o Azure PowerShell toocreate um recursos de principal tooaccess de serviço](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-password). É também possível demasiado[criar um principal de serviço através do portal do Azure de Olá](../azure-resource-manager/resource-group-create-service-principal-portal.md).

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

Olá tooquery API de Monitor do Azure, aplicação de cliente Olá deve utilizar Olá tooauthenticate principal de serviço que criou anteriormente. Olá seguinte script do PowerShell de exemplo mostra uma abordagem, utilizando Olá [Active Directory Authentication Library](../active-directory/active-directory-authentication-libraries.md) (ADAL) toohelp obter autenticação de JWT Olá token. token JWT de Olá é transmitida como parte de um parâmetro de autorização de HTTP no pedidos toohello API de REST de Monitor do Azure.

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

Após a conclusão do passo de configuração de autenticação de Olá, em seguida, pode executar consultas contra Olá API de REST de Monitor do Azure. Existem duas consultas úteis:

1. Lista as definições de métrica Olá para um recurso
2. Obter valores de métrica de Olá

## <a name="retrieve-metric-definitions"></a>Obter as definições de métrica
> [!NOTE]
> tooretrieve as definições de métrica utilizando Olá API de REST de Monitor do Azure, utilize "2016-03-01" Olá, versão de API.
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
Para uma aplicação lógica do Azure, as definições de métrica de Olá aparecia toohello semelhante captura de ecrã a seguir:

![ALT "Vista JSON da resposta de definição de métrica".](./media/monitoring-rest-api-walkthrough/available_metric_definitions_logic_app_json_response_clean.png)

Para obter mais informações, consulte Olá [lista as definições de métrica Olá para um recurso na API REST da Azure Monitor](https://msdn.microsoft.com/library/azure/mt743621.aspx) documentação.

## <a name="retrieve-metric-values"></a>Obter valores de métricos
Assim que as definições de métrica disponível Olá são conhecidas, é, em seguida, tooretrieve possíveis Olá os valores de métricos relacionados. Utilize nome 'value' da métrica de Olá (não Olá 'localizedValue') para quaisquer pedidos filtragem (por exemplo, obter Olá 'CpuTime' e 'Pedidos' Métrica pontos de dados). Se não existem filtros forem especificados, é devolvida métrica da predefinição de Olá.

> [!NOTE]
> os valores de métrica tooretrieve utilizando Olá API de REST de Monitor do Azure, utilize "2016-06-01" Olá versão da API.
>
>

**Método**: introdução

**URI de pedido**: https://management.azure.com/subscriptions/*{id de subscrição}*/resourceGroups/*{nome de grupo de recursos}*/providers/*{ recursos-fornecedor-namespace}*/*{tipo de recurso}*/*{nome do recurso}*/providers/microsoft.insights/metrics?$filter= *{filtro}*& api-version =*{apiVersion}*

Por exemplo, tooretrieve Olá RunsSucceeded métrica dos pontos de dados para Olá dado intervalo de tempo e um grão de tempo de 1 hora, o pedido de Olá seria o seguinte:

```PowerShell
$apiVersion = "2016-06-01"
$filter = "(name.value eq 'RunsSucceeded') and aggregationType eq 'Total' and startTime eq 2016-09-23 and endTime eq 2016-09-24 and timeGrain eq duration'PT1H'"
$request = "https://management.azure.com/subscriptions/${subscriptionId}/resourceGroups/${resourceGroupName}/providers/${resourceProviderNamespace}/${resourceType}/${resourceName}/providers/microsoft.insights/metrics?`$filter=${filter}&api-version=${apiVersion}"
(Invoke-RestMethod -Uri $request `
                   -Headers $authHeader `
                   -Method Get `
                   -Verbose).Value | ConvertTo-Json
```

resultado de Olá aparecia semelhante toohello exemplo que segue captura de ecrã:

![ALT "Com o valor de métrica de tempo de resposta médio de resposta JSON"](./media/monitoring-rest-api-walkthrough/available_metrics_logic_app_json_response.png)

tooretrieve pontos de dados de várias ou agregação, adicione os nomes de definição de métrica de Olá e o filtro de toohello de tipos de agregação, como mostrado no seguinte exemplo de Olá:

```PowerShell
$apiVersion = "2016-06-01"
$filter = "(name.value eq 'ActionsCompleted' or name.value eq 'RunsSucceeded') and (aggregationType eq 'Total' or aggregationType eq 'Average') and startTime eq 2016-09-23T13:30:00Z and endTime eq 2016-09-23T14:30:00Z and timeGrain eq duration'PT1M'"
$request = "https://management.azure.com/subscriptions/${subscriptionId}/resourceGroups/${resourceGroupName}/providers/${resourceProviderNamespace}/${resourceType}/${resourceName}/providers/microsoft.insights/metrics?`$filter=${filter}&api-version=${apiVersion}"
(Invoke-RestMethod -Uri $request `
                   -Headers $authHeader `
                   -Method Get `
                   -Verbose).Value | ConvertTo-Json
```

### <a name="use-armclient"></a>Utilizar ARMClient
Uma alternativa toousing PowerShell (conforme mostrado acima), é toouse [ARMClient](https://github.com/projectkudu/ARMClient) no seu computador Windows. ARMClient processa a autenticação de Olá do Azure AD (e resultante token JWT) automaticamente. Olá passos seguintes descrevem a utilização de ARMClient para obter os dados métricos:

1. Instalar [Chocolatey](https://chocolatey.org/) e [ARMClient](https://github.com/projectkudu/ARMClient).
2. Na janela de terminal, escreva *armclient.exe início de sessão*. Isto irá pedir-lhe toolog no tooAzure.
3. Tipo *armclient GET [your_resource_id]/providers/microsoft.insights/metricdefinitions?api-version=2016-03-01*
4. Tipo *armclient GET [your_resource_id]/providers/microsoft.insights/metrics?api-version=2016-06-01*

![ALT "Using ARMClient toowork com Olá API de REST de monitorização do Azure"](./media/monitoring-rest-api-walkthrough/armclient_metricdefinitions.png)

## <a name="retrieve-hello-resource-id"></a>Obter Olá ID de recurso
Utilizando a REST API de Olá realmente pode ajudar toounderstand Olá disponíveis as definições de métrica, granularidade e os valores relacionados. Essa informação é útil quando utilizar Olá [biblioteca de gestão do Azure](https://msdn.microsoft.com/library/azure/mt417623.aspx).

Para Olá precedente código, toouse de ID de recurso Olá é Olá caminho completo toohello pretendido recursos do Azure. Por exemplo, tooquery em relação a uma aplicação Web do Azure, ID de recurso Olá seria:

*/subscriptions/{Subscription-ID}/resourceGroups/{Resource-group-name}/providers/Microsoft.Web/sites/{site-name}/*

Olá lista seguinte contém alguns exemplos de formatos de ID de recurso para vários recursos do Azure:

* **IoT Hub** -/subscriptions/{targetsubscriptionid}/resourcegroups/{targetresourcegroupname}*{id de subscrição}*/resourceGroups/*{nome de grupo de recursos}*/providers/Microsoft.Devices/IotHubs/*{iot-hub-name}*
* **Agrupamento elástico de SQL** -/subscriptions/{targetsubscriptionid}/resourcegroups/{targetresourcegroupname}*{id de subscrição}*/resourceGroups/*{nome de grupo de recursos}*/providers/Microsoft.Sql/servers/*{conjunto-db}*/elasticpools/*{nome de conjunto de sql}*
* **Base de dados do SQL (v12)** -/subscriptions/{targetsubscriptionid}/resourcegroups/{targetresourcegroupname}*{id de subscrição}*/resourceGroups/*{nome de grupo de recursos}*/providers/Microsoft.Sql/servers/*{nome do servidor}* /databases/*{nome-base de dados}*
* **Barramento de serviço** -/subscriptions/{targetsubscriptionid}/resourcegroups/{targetresourcegroupname}*{id de subscrição}*/resourceGroups/*{nome de grupo de recursos}*/providers/Microsoft.ServiceBus/*{namespace}* / *{nome-servicebus}*
* **Conjuntos de dimensionamento de VM** -/subscriptions/{targetsubscriptionid}/resourcegroups/{targetresourcegroupname}*{id de subscrição}*/resourceGroups/*{nome de grupo de recursos}*/providers/Microsoft.Compute/virtualMachineScaleSets/*{ nome da VM}*
* **VMs** -/subscriptions/{targetsubscriptionid}/resourcegroups/{targetresourcegroupname}*{id de subscrição}*/resourceGroups/*{nome de grupo de recursos}*/providers/Microsoft.Compute/virtualMachines/*{nome da vm}*
* **Os Event Hubs** -/subscriptions/{targetsubscriptionid}/resourcegroups/{targetresourcegroupname}*{id de subscrição}*/resourceGroups/*{nome de grupo de recursos}*/providers/Microsoft.EventHub/namespaces/*{ eventhub-namespace}*

Existem abordagens alternativas tooretrieving Olá ID de recurso, incluindo a utilização do Explorador de recursos do Azure, visualizar recursos Olá pretendido na Olá portal do Azure e através do PowerShell ou Olá CLI do Azure.

### <a name="azure-resource-explorer"></a>Explorador de Recursos do Azure
ID do recurso de Olá toofind para um recurso pretendido, uma abordagem útil é toouse Olá [Explorador de recursos do Azure](https://resources.azure.com) ferramenta. Navegue recursos toohello pretendido e, em seguida, observe o ID de Olá apresentado, tal como em Olá captura de ecrã a seguir:

![ALT "Explorador de recursos do Azure"](./media/monitoring-rest-api-walkthrough/azure_resource_explorer.png)

### <a name="azure-portal"></a>Portal do Azure
Pode também obter o ID de recurso Olá Olá portal do Azure. toodo por isso, navegue até recursos toohello pretendido e, em seguida, selecione propriedades. Olá ID de recurso é apresentado no painel de propriedades de Olá, como mostrado na seguinte captura de ecrã de Olá:

![ALT "ID de recurso apresentado no painel de propriedades de Olá no Olá portal do Azure"](./media/monitoring-rest-api-walkthrough/resourceid_azure_portal.png)

### <a name="azure-powershell"></a>Azure PowerShell
ID de recurso Olá pode ser obtido utilizando cmdlets do PowerShell do Azure. Por exemplo, tooobtain Olá ID de recurso para uma aplicação Web do Azure, execute o cmdlet Olá Get-AzureRmWebApp, tal como em Olá seguinte captura de ecrã:

![ALT "ID de recurso obtido através do PowerShell"](./media/monitoring-rest-api-walkthrough/resourceid_powershell.png)

### <a name="azure-cli"></a>CLI do Azure
tooretrieve Olá ID de recurso utilizando Olá CLI do Azure, execute o comando de "Mostrar webapp do azure" Olá, especificando Olá ' – json' opção, conforme mostrado na seguinte captura de ecrã de Olá:

![ALT "ID de recurso obtido através do PowerShell"](./media/monitoring-rest-api-walkthrough/resourceid_azurecli.png)

## <a name="retrieve-activity-log-data"></a>Obter dados de registo de atividade
Adição tooworking com as definições de métrica e os valores relacionados, é também possível tooretrieve interessantes insights relacionados tooAzure recursos adicionais. Por exemplo, é possível tooquery [registo de atividade](https://msdn.microsoft.com/library/azure/dn931934.aspx) dados. Olá exemplo seguinte demonstra com Olá os dados de registo da atividade de tooquery de API REST da Azure Monitor dentro de um intervalo de datas específico para uma subscrição do Azure:

```PowerShell
$apiVersion = "2014-04-01"
$filter = "eventTimestamp ge '2016-09-23' and eventTimestamp le '2016-09-24'and eventChannels eq 'Admin, Operation'"
$request = "https://management.azure.com/subscriptions/${subscriptionId}/providers/microsoft.insights/eventtypes/management/values?api-version=${apiVersion}&`$filter=${filter}"
(Invoke-RestMethod -Uri $request `
                   -Headers $authHeader `
                   -Method Get `
                   -Verbose).Value | ConvertTo-Json
```

## <a name="next-steps"></a>Passos seguintes
* Olá revisão [descrição geral da monitorização](monitoring-overview.md).
* Olá vista [suportado métricas com a monitorização do Azure](monitoring-supported-metrics.md).
* Olá revisão [referência de API de REST do Microsoft Azure Monitor](https://msdn.microsoft.com/library/azure/dn931943.aspx).
* Olá revisão [biblioteca de gestão do Azure](https://msdn.microsoft.com/library/azure/mt417623.aspx).
