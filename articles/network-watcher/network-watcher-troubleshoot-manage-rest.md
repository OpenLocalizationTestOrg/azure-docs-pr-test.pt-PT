---
title: "aaaTroubleshoot Gateway de rede Virtual e ligações com o observador de rede do Azure - REST | Microsoft Docs"
description: "Esta página explica como REST tootroubleshoot Gateways da Virtual Network e ligações com a utilização do observador de rede do Azure"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: e4d5f195-b839-4394-94ef-a04192766e55
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/19/2017
ms.author: gwallace
ms.openlocfilehash: cc89b46643fdbfefe53727b45d6b7d06914b58a6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-virtual-network-gateway-and-connections-using-azure-network-watcher"></a><span data-ttu-id="de8c8-103">Resolver problemas de gateway de rede Virtual e ligações utilizando o observador de rede do Azure</span><span class="sxs-lookup"><span data-stu-id="de8c8-103">Troubleshoot Virtual Network gateway and Connections using Azure Network Watcher</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="de8c8-104">Portal</span><span class="sxs-lookup"><span data-stu-id="de8c8-104">Portal</span></span>](network-watcher-troubleshoot-manage-portal.md)
> - [<span data-ttu-id="de8c8-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="de8c8-105">PowerShell</span></span>](network-watcher-troubleshoot-manage-powershell.md)
> - [<span data-ttu-id="de8c8-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="de8c8-106">CLI 1.0</span></span>](network-watcher-troubleshoot-manage-cli-nodejs.md)
> - [<span data-ttu-id="de8c8-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="de8c8-107">CLI 2.0</span></span>](network-watcher-troubleshoot-manage-cli.md)
> - [<span data-ttu-id="de8c8-108">API REST</span><span class="sxs-lookup"><span data-stu-id="de8c8-108">REST API</span></span>](network-watcher-troubleshoot-manage-rest.md)

<span data-ttu-id="de8c8-109">Observador de rede oferece muitas funcionalidades no que respeita toounderstanding os recursos de rede no Azure.</span><span class="sxs-lookup"><span data-stu-id="de8c8-109">Network Watcher provides many capabilities as it relates toounderstanding your network resources in Azure.</span></span> <span data-ttu-id="de8c8-110">Uma dessas funcionalidades é recursos de resolução de problemas.</span><span class="sxs-lookup"><span data-stu-id="de8c8-110">One of these capabilities is resource troubleshooting.</span></span> <span data-ttu-id="de8c8-111">Resolução de problemas de recursos pode ser chamada através do portal de Olá, do PowerShell, CLI ou REST API.</span><span class="sxs-lookup"><span data-stu-id="de8c8-111">Resource troubleshooting can be called through hello portal, PowerShell, CLI, or REST API.</span></span> <span data-ttu-id="de8c8-112">Quando chamado, o observador de rede inspeciona o estado de funcionamento de Olá de um Gateway de rede Virtual ou uma ligação e devolve conclusões.</span><span class="sxs-lookup"><span data-stu-id="de8c8-112">When called, Network Watcher inspects hello health of a Virtual Network Gateway or a Connection and returns its findings.</span></span>

<span data-ttu-id="de8c8-113">Este artigo leva-o através de tarefas de gestão diferentes Olá que estão atualmente disponíveis para a resolução de problemas de recursos.</span><span class="sxs-lookup"><span data-stu-id="de8c8-113">This article takes you through hello different management tasks that are currently available for resource troubleshooting.</span></span>

- [<span data-ttu-id="de8c8-114">**Resolver problemas relacionados com um gateway de rede Virtual**</span><span class="sxs-lookup"><span data-stu-id="de8c8-114">**Troubleshoot a Virtual Network gateway**</span></span>](#troubleshoot-a-virtual-network-gateway)
- [<span data-ttu-id="de8c8-115">**Resolver problemas de uma ligação**</span><span class="sxs-lookup"><span data-stu-id="de8c8-115">**Troubleshoot a Connection**</span></span>](#troubleshoot-connections)

## <a name="before-you-begin"></a><span data-ttu-id="de8c8-116">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="de8c8-116">Before you begin</span></span>

<span data-ttu-id="de8c8-117">ARMclient é a API de REST de Olá toocall utilizado com o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="de8c8-117">ARMclient is used toocall hello REST API using PowerShell.</span></span> <span data-ttu-id="de8c8-118">ARMClient for encontrado no chocolatey em [ARMClient no Chocolatey](https://chocolatey.org/packages/ARMClient)</span><span class="sxs-lookup"><span data-stu-id="de8c8-118">ARMClient is found on chocolatey at [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient)</span></span>

<span data-ttu-id="de8c8-119">Este cenário pressupõe que já tiver seguido os passos de Olá no [criar um observador de rede](network-watcher-create.md) toocreate um observador de rede.</span><span class="sxs-lookup"><span data-stu-id="de8c8-119">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span>

<span data-ttu-id="de8c8-120">Para obter uma lista de visita de tipos de gateway suportados, [tipos de Gateway suportado](network-watcher-troubleshoot-overview.md#supported-gateway-types).</span><span class="sxs-lookup"><span data-stu-id="de8c8-120">For a list of supported gateway types visit, [Supported Gateway types](network-watcher-troubleshoot-overview.md#supported-gateway-types).</span></span>

## <a name="overview"></a><span data-ttu-id="de8c8-121">Descrição geral</span><span class="sxs-lookup"><span data-stu-id="de8c8-121">Overview</span></span>

<span data-ttu-id="de8c8-122">Resolução de problemas de observador de rede fornece a capacidade de Olá resolver problemas que surgem com gateways de rede Virtual e ligações.</span><span class="sxs-lookup"><span data-stu-id="de8c8-122">Network Watcher troubleshooting provides hello ability troubleshoot issues that arise with Virtual Network gateways and Connections.</span></span> <span data-ttu-id="de8c8-123">Quando é efetuado um pedido de recurso toohello e resolução de problemas, registos estiver a consultar inspecioná-los.</span><span class="sxs-lookup"><span data-stu-id="de8c8-123">When a request is made toohello resource troubleshooting, logs are querying and inspected.</span></span> <span data-ttu-id="de8c8-124">Quando a inspeção estiver concluída, resultados de Olá são devolvidos.</span><span class="sxs-lookup"><span data-stu-id="de8c8-124">When inspection is complete, hello results are returned.</span></span> <span data-ttu-id="de8c8-125">API de resolução de problemas do Olá pedidos são longos pedidos, o que pode demorar vários minutos tooreturn um resultado em execução.</span><span class="sxs-lookup"><span data-stu-id="de8c8-125">hello troubleshoot API requests are long running requests, which could take multiple minutes tooreturn a result.</span></span> <span data-ttu-id="de8c8-126">Os registos são armazenados num contentor numa conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="de8c8-126">Logs are stored in a container on a storage account.</span></span>

## <a name="log-in-with-armclient"></a><span data-ttu-id="de8c8-127">Iniciar sessão com ARMClient</span><span class="sxs-lookup"><span data-stu-id="de8c8-127">Log in with ARMClient</span></span>

```PowerShell
armclient login
```

## <a name="troubleshoot-a-virtual-network-gateway"></a><span data-ttu-id="de8c8-128">Resolver problemas relacionados com um gateway de rede Virtual</span><span class="sxs-lookup"><span data-stu-id="de8c8-128">Troubleshoot a Virtual Network gateway</span></span>


### <a name="post-hello-troubleshoot-request"></a><span data-ttu-id="de8c8-129">Olá POST resolver problemas do pedido</span><span class="sxs-lookup"><span data-stu-id="de8c8-129">POST hello troubleshoot request</span></span>

<span data-ttu-id="de8c8-130">Olá seguir o estado de Olá de consultas de exemplo de um gateway de rede Virtual.</span><span class="sxs-lookup"><span data-stu-id="de8c8-130">hello following example queries hello status of a Virtual Network gateway.</span></span>

```powershell

$subscriptionId = "00000000-0000-0000-0000-000000000000"
$resourceGroupName = "ContosoRG"
$NWresourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
$vnetGatewayName = "ContosoVNETGateway"
$storageAccountName = "contososa"
$containerName = "gwlogs"
$requestBody = @"
{
'TargetResourceId': '/subscriptions/${subscriptionId}/resourceGroups/${resourceGroupName}/providers/Microsoft.Network/virtualNetworkGateways/${vnetGatewayName}',
'Properties': {
'StorageId': '/subscriptions/${subscriptionId}/resourceGroups/${resourceGroupName}/providers/Microsoft.Storage/storageAccounts/${storageAccountName}',
'StoragePath': 'https://${storageAccountName}.blob.core.windows.net/${containerName}'
}
}
"@

}
armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${NWresourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/troubleshoot?api-version=2016-03-30 "
```

<span data-ttu-id="de8c8-131">Uma vez que esta operação é muito a executar, hello URI para consultar a operação de Olá e Olá URI para o resultado de Olá é devolvido no cabeçalho de resposta de Olá, conforme mostrado no Olá seguinte resposta:</span><span class="sxs-lookup"><span data-stu-id="de8c8-131">Since this operation is long running, hello URI for querying hello operation and hello URI for hello result is returned in hello response header as shown in hello following response:</span></span>

<span data-ttu-id="de8c8-132">**Valores importantes**</span><span class="sxs-lookup"><span data-stu-id="de8c8-132">**Important Values**</span></span>

* <span data-ttu-id="de8c8-133">**Azure AsyncOperation** -esta propriedade contém Olá URI tooquery Olá Async resolver problemas de operação</span><span class="sxs-lookup"><span data-stu-id="de8c8-133">**Azure-AsyncOperation** - This property contains hello URI tooquery hello Async troubleshoot operation</span></span>
* <span data-ttu-id="de8c8-134">**Localização** -esta propriedade contém Olá URI onde Olá os resultados são quando hello operação foi concluída</span><span class="sxs-lookup"><span data-stu-id="de8c8-134">**Location** - This property contains hello URI where hello results are when hello operation is complete</span></span>

```
HTTP/1.1 202 Accepted
Pragma: no-cache
Retry-After: 10
x-ms-request-id: 8a1167b7-6768-4ac1-85dc-703c9c9b9247
Azure-AsyncOperation: https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operations/8a1167b7-6768-4ac1-85dc-703c9c9b9247?api-version=2016-03-30
Strict-Transport-Security: max-age=31536000; includeSubDomains
Cache-Control: no-cache
Location: https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operationResults/8a1167b7-6768-4ac1-85dc-703c9c9b9247?api-version=2016-03-30
Server: Microsoft-HTTPAPI/2.0; Microsoft-HTTPAPI/2.0
x-ms-ratelimit-remaining-subscription-writes: 1199
x-ms-correlation-request-id: 4364d88a-bd08-422c-a716-dbb0cdc99f7b
x-ms-routing-request-id: NORTHCENTRALUS:20170112T183202Z:4364d88a-bd08-422c-a716-dbb0cdc99f7b
Date: Thu, 12 Jan 2017 18:32:01 GMT

null
```

### <a name="query-hello-async-operation-for-completion"></a><span data-ttu-id="de8c8-135">Olá async operação para conclusão de consulta</span><span class="sxs-lookup"><span data-stu-id="de8c8-135">Query hello async operation for completion</span></span>

<span data-ttu-id="de8c8-136">Utilize Olá operações URI tooquery para progresso Olá operação de Olá, como mostrado no seguinte exemplo de Olá:</span><span class="sxs-lookup"><span data-stu-id="de8c8-136">Use hello operations URI tooquery for hello progress of hello operation as seen in hello following example:</span></span>

```powershell
armclient get "https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operations/8a1167b7-6768-4ac1-85dc-703c9c9b9247?api-version=2016-03-30"
```

<span data-ttu-id="de8c8-137">Enquanto a operação de Olá está em curso, Olá resposta mostra **em curso** como mostrado no seguinte exemplo de Olá:</span><span class="sxs-lookup"><span data-stu-id="de8c8-137">While hello operation is in progress, hello response shows **InProgress** as seen in hello following example:</span></span>

```json
{
  "status": "InProgress"
}
```

<span data-ttu-id="de8c8-138">Quando a operação de Olá é alterações de estado de conclusão Olá demasiado**com êxito**.</span><span class="sxs-lookup"><span data-stu-id="de8c8-138">When hello operation is complete hello status changes too**Succeeded**.</span></span>

```json
{
  "status": "Succeeded"
}
```

### <a name="retrieve-hello-results"></a><span data-ttu-id="de8c8-139">Obter resultados Olá</span><span class="sxs-lookup"><span data-stu-id="de8c8-139">Retrieve hello results</span></span>

<span data-ttu-id="de8c8-140">Depois de estado de Olá devolvidos é **com êxito**, chamar um método obter Olá operationResult URI tooretrieve resultados Olá.</span><span class="sxs-lookup"><span data-stu-id="de8c8-140">Once hello status returned is **Succeeded**, call a GET Method on hello operationResult URI tooretrieve hello results.</span></span>

```powershell
armclient get "https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operationResults/8a1167b7-6768-4ac1-85dc-703c9c9b9247?api-version=2016-03-30"
```

<span data-ttu-id="de8c8-141">Olá respostas seguintes são exemplos de uma resposta degradada típico devolvido quando a consulta de Olá resultados de um gateway de resolução de problemas.</span><span class="sxs-lookup"><span data-stu-id="de8c8-141">hello following responses are examples of a typical degraded response returned when querying hello results of troubleshooting a gateway.</span></span> <span data-ttu-id="de8c8-142">Consulte [compreender resultados Olá](#understanding-the-results) tooget esclarecimentos nas propriedades que Olá em média de resposta de Olá.</span><span class="sxs-lookup"><span data-stu-id="de8c8-142">See [Understanding hello results](#understanding-the-results) tooget clarification on what hello properties in hello response mean.</span></span>

```json
{
  "startTime": "2017-01-12T10:31:41.562646-08:00",
  "endTime": "2017-01-12T18:31:48.677Z",
  "code": "Degraded",
  "results": [
    {
      "id": "PlatformInActive",
      "summary": "We are sorry, your VPN gateway is in standby mode",
      "detail": "During this time hello gateway will not initiate or accept VPN connections with on premises VPN devices or other Azure VPN Gateways. This is a transient state while hello Azure platform is being updated.",
      "recommendedActions": [
        {
          "actionText": "If hello condition persists, please try resetting your Azure VPN gateway",
          "actionUri": "https://azure.microsoft.com/en-us/documentation/articles/vpn-gateway-resetgw-classic/",
          "actionUriText": "resetting hello VPN Gateway"
        },
        {
          "actionText": "If your VPN gateway isn't up and running by hello expected resolution time, contact support",
          "actionUri": "http://azure.microsoft.com/support",
          "actionUriText": "contact support"
        }
      ]
    },
    {
      "id": "NoFault",
      "summary": "This VPN gateway is running normally",
      "detail": "There aren't any known Azure platform problems affecting this VPN Connection",
      "recommendedActions": [
        {
          "actionText": "If you are still experience problems with hello VPN gateway, please try resetting hello VPN gateway.",
          "actionUri": "https://azure.microsoft.com/en-us/documentation/articles/vpn-gateway-resetgw-classic/",
          "actionUriText": "resetting VPN gateway"
        },
        {
          "actionText": "If you are experiencing problems you believe are caused by Azure, contact support",
          "actionUri": "http://azure.microsoft.com/support",
          "actionUriText": "contact support"
        }
      ]
    }
  ]
}
```


## <a name="troubleshoot-connections"></a><span data-ttu-id="de8c8-143">Resolver problemas de ligações</span><span class="sxs-lookup"><span data-stu-id="de8c8-143">Troubleshoot Connections</span></span>

<span data-ttu-id="de8c8-144">Olá seguir o estado de Olá de consultas de exemplo de uma ligação.</span><span class="sxs-lookup"><span data-stu-id="de8c8-144">hello following example queries hello status of a Connection.</span></span>

```powershell

$subscriptionId = "00000000-0000-0000-0000-000000000000"
$resourceGroupName = "ContosoRG"
$NWresourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
$connectionName = "VNET2toVNET1Connection"
$storageAccountName = "contososa"
$containerName = "gwlogs"
$requestBody = @{
"TargetResourceId": "/subscriptions/${subscriptionId}/resourceGroups/${resourceGroupName}/providers/Microsoft.Network/connections/${connectionName}",
"Properties": {
"StorageId": "/subscriptions/${subscriptionId}/resourceGroups/${resourceGroupName}/providers/Microsoft.Storage/storageAccounts/${storageAccountName}",
"StoragePath": "https://${storageAccountName}.blob.core.windows.net/${containerName}"
}

}
armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${NWresourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/troubleshoot?api-version=2016-03-30 "
```

> [!NOTE]
> <span data-ttu-id="de8c8-145">Olá de resolver problemas relacionados com a operação não pode ser executado em paralelo no respetivos gateways correspondentes e de uma ligação.</span><span class="sxs-lookup"><span data-stu-id="de8c8-145">hello troubleshoot operation cannot be run in parallel on a Connection and its corresponding gateways.</span></span> <span data-ttu-id="de8c8-146">operação Olá tem de concluir toorunning anterior-lo no recurso de Olá anterior.</span><span class="sxs-lookup"><span data-stu-id="de8c8-146">hello operation must complete prior toorunning it on hello previous resource.</span></span>

<span data-ttu-id="de8c8-147">Uma vez que esta é uma transação de execução longa, no cabeçalho de resposta de Olá, Olá URI para consultar a operação de Olá e Olá URI para o resultado de Olá é devolvido como mostrado na Olá seguinte resposta:</span><span class="sxs-lookup"><span data-stu-id="de8c8-147">Since this is a long running transaction, in hello response header, hello URI for querying hello operation and hello URI for hello result is returned as shown in hello following response:</span></span>

<span data-ttu-id="de8c8-148">**Valores importantes**</span><span class="sxs-lookup"><span data-stu-id="de8c8-148">**Important Values**</span></span>

* <span data-ttu-id="de8c8-149">**Azure AsyncOperation** -esta propriedade contém Olá URI tooquery Olá Async resolver problemas de operação</span><span class="sxs-lookup"><span data-stu-id="de8c8-149">**Azure-AsyncOperation** - This property contains hello URI tooquery hello Async troubleshoot operation</span></span>
* <span data-ttu-id="de8c8-150">**Localização** -esta propriedade contém Olá URI onde Olá os resultados são quando hello operação foi concluída</span><span class="sxs-lookup"><span data-stu-id="de8c8-150">**Location** - This property contains hello URI where hello results are when hello operation is complete</span></span>

```
HTTP/1.1 202 Accepted
Pragma: no-cache
Retry-After: 10
x-ms-request-id: 8a1167b7-6768-4ac1-85dc-703c9c9b9247
Azure-AsyncOperation: https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operations/8a1167b7-6768-4ac1-85dc-703c9c9b9247?api-version=2016-03-30
Strict-Transport-Security: max-age=31536000; includeSubDomains
Cache-Control: no-cache
Location: https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operationResults/8a1167b7-6768-4ac1-85dc-703c9c9b9247?api-version=2016-03-30
Server: Microsoft-HTTPAPI/2.0; Microsoft-HTTPAPI/2.0
x-ms-ratelimit-remaining-subscription-writes: 1199
x-ms-correlation-request-id: 4364d88a-bd08-422c-a716-dbb0cdc99f7b
x-ms-routing-request-id: NORTHCENTRALUS:20170112T183202Z:4364d88a-bd08-422c-a716-dbb0cdc99f7b
Date: Thu, 12 Jan 2017 18:32:01 GMT

null
```

### <a name="query-hello-async-operation-for-completion"></a><span data-ttu-id="de8c8-151">Olá async operação para conclusão de consulta</span><span class="sxs-lookup"><span data-stu-id="de8c8-151">Query hello async operation for completion</span></span>

<span data-ttu-id="de8c8-152">Utilize Olá operações URI tooquery para progresso Olá operação de Olá, como mostrado no seguinte exemplo de Olá:</span><span class="sxs-lookup"><span data-stu-id="de8c8-152">Use hello operations URI tooquery for hello progress of hello operation as seen in hello following example:</span></span>

```powershell
armclient get "https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operations/843b1c31-4717-4fdd-b7a6-4c786ca9c501?api-version=2016-03-30"
```

<span data-ttu-id="de8c8-153">Enquanto a operação de Olá está em curso, Olá resposta mostra **em curso** como mostrado no seguinte exemplo de Olá:</span><span class="sxs-lookup"><span data-stu-id="de8c8-153">While hello operation is in progress, hello response shows **InProgress** as seen in hello following example:</span></span>

```json
{
  "status": "InProgress"
}
```

<span data-ttu-id="de8c8-154">Quando a operação de Olá estiver concluída, o estado de Olá mudar demasiado**com êxito**.</span><span class="sxs-lookup"><span data-stu-id="de8c8-154">When hello operation is complete, hello status changes too**Succeeded**.</span></span>

```json
{
  "status": "Succeeded"
}
```

<span data-ttu-id="de8c8-155">Olá respostas seguintes são exemplos de uma resposta típico devolvido quando a consulta de Olá resultados de uma ligação de resolução de problemas.</span><span class="sxs-lookup"><span data-stu-id="de8c8-155">hello following responses are examples of a typical response returned when querying hello results of troubleshooting a Connection.</span></span>

### <a name="retrieve-hello-results"></a><span data-ttu-id="de8c8-156">Obter resultados Olá</span><span class="sxs-lookup"><span data-stu-id="de8c8-156">Retrieve hello results</span></span>

<span data-ttu-id="de8c8-157">Depois de estado de Olá devolvidos é **com êxito**, chamar um método obter Olá operationResult URI tooretrieve resultados Olá.</span><span class="sxs-lookup"><span data-stu-id="de8c8-157">Once hello status returned is **Succeeded**, call a GET Method on hello operationResult URI tooretrieve hello results.</span></span>

```powershell
armclient get "https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operationResults/843b1c31-4717-4fdd-b7a6-4c786ca9c501?api-version=2016-03-30"
```

<span data-ttu-id="de8c8-158">Olá respostas seguintes são exemplos de uma resposta típico devolvido quando a consulta de Olá resultados de uma ligação de resolução de problemas.</span><span class="sxs-lookup"><span data-stu-id="de8c8-158">hello following responses are examples of a typical response returned when querying hello results of troubleshooting a Connection.</span></span>

```json
{
  "startTime": "2017-01-12T14:09:19.1215346-08:00",
  "endTime": "2017-01-12T22:09:23.747Z",
  "code": "UnHealthy",
  "results": [
    {
      "id": "PlatformInActive",
      "summary": "We are sorry, your VPN gateway is in standby mode",
      "detail": "During this time hello gateway will not initiate or accept VPN connections with on premises VPN devices or other Azure VPN Gateways. This 
is a transient state while hello Azure platform is being updated.",
      "recommendedActions": [
        {
          "actionText": "If hello condition persists, please try resetting your Azure VPN gateway",
          "actionUri": "https://azure.microsoft.com/en-us/documentation/articles/vpn-gateway-resetgw-classic/",
          "actionUriText": "resetting hello VPN gateway"
        },
        {
          "actionText": "If your VPN Connection isn't up and running by hello expected resolution time, contact support",
          "actionUri": "http://azure.microsoft.com/support",
          "actionUriText": "contact support"
        }
      ]
    },
    {
      "id": "NoFault",
      "summary": "This VPN Connection is running normally",
      "detail": "There aren't any known Azure platform problems affecting this VPN Connection",
      "recommendedActions": [
        {
          "actionText": "If you are still experience problems with hello VPN gateway, please try resetting hello VPN gateway.",
          "actionUri": "https://azure.microsoft.com/en-us/documentation/articles/vpn-gateway-resetgw-classic/",
          "actionUriText": "resetting VPN gateway"
        },
        {
          "actionText": "If you are experiencing problems you believe are caused by Azure, contact support",
          "actionUri": "http://azure.microsoft.com/support",
          "actionUriText": "contact support"
        }
      ]
    }
  ]
}
```

## <a name="understanding-hello-results"></a><span data-ttu-id="de8c8-159">Compreender os resultados de Olá</span><span class="sxs-lookup"><span data-stu-id="de8c8-159">Understanding hello results</span></span>

<span data-ttu-id="de8c8-160">o texto de ação de Olá fornece orientações gerais sobre como tooresolve Olá problema.</span><span class="sxs-lookup"><span data-stu-id="de8c8-160">hello action text provides general guidance on how tooresolve hello issue.</span></span> <span data-ttu-id="de8c8-161">Se uma ação pode ser levada para o problema de Olá, é fornecida uma ligação com orientações adicionais.</span><span class="sxs-lookup"><span data-stu-id="de8c8-161">If an action can be taken for hello issue, a link is provided with additional guidance.</span></span> <span data-ttu-id="de8c8-162">No caso de Olá em que não existe nenhuma orientação adicional, resposta Olá fornece Olá url tooopen um incidente de suporte.</span><span class="sxs-lookup"><span data-stu-id="de8c8-162">In hello case where there is no additional guidance, hello response provides hello url tooopen a support case.</span></span>  <span data-ttu-id="de8c8-163">Para obter mais informações sobre as propriedades de Olá de resposta Olá e que está incluído, visite [descrição geral de resolução de problemas de observador de rede](network-watcher-troubleshoot-overview.md)</span><span class="sxs-lookup"><span data-stu-id="de8c8-163">For more information about hello properties of hello response and what is included, visit [Network Watcher Troubleshoot overview](network-watcher-troubleshoot-overview.md)</span></span>

<span data-ttu-id="de8c8-164">Para obter instruções sobre como transferir ficheiros entre contas de armazenamento do azure, consulte demasiado[introdução ao Blob storage do Azure através do .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="de8c8-164">For instructions on downloading files from azure storage accounts, refer too[Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span> <span data-ttu-id="de8c8-165">Outra ferramenta que pode ser utilizada é Explorador de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="de8c8-165">Another tool that can be used is Storage Explorer.</span></span> <span data-ttu-id="de8c8-166">Obter mais informações sobre o Explorador de armazenamento podem ser encontradas aqui em Olá seguinte hiperligação: [Explorador de armazenamento](http://storageexplorer.com/)</span><span class="sxs-lookup"><span data-stu-id="de8c8-166">More information about Storage Explorer can be found here at hello following link: [Storage Explorer](http://storageexplorer.com/)</span></span>

## <a name="next-steps"></a><span data-ttu-id="de8c8-167">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="de8c8-167">Next steps</span></span>

<span data-ttu-id="de8c8-168">Se foram alteradas as definições que conectividade VPN de parar, consulte o artigo [gerir grupos de segurança de rede](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack baixo Olá rede segurança e de grupo de regras de segurança que podem ser em questão.</span><span class="sxs-lookup"><span data-stu-id="de8c8-168">If settings have been changed that stop VPN connectivity, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack down hello network security group and security rules that may be in question.</span></span>
