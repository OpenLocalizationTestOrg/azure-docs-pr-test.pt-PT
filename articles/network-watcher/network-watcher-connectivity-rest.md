---
title: conectividade aaaCheck observador de rede do Azure - portal do Azure | Microsoft Docs
description: "Esta página explica como toocheck conectividade com o observador de rede no Olá portal do Azure"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/02/2017
ms.author: gwallace
ms.openlocfilehash: 8560011906fcce46d31556fc52cbfa671e8e653a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="check-connectivity-with-azure-network-watcher-using-hello-azure-portal"></a><span data-ttu-id="f3b09-103">Verifique a conectividade com o observador de rede do Azure utilizando Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="f3b09-103">Check connectivity with Azure Network Watcher using hello Azure portal</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="f3b09-104">Portal</span><span class="sxs-lookup"><span data-stu-id="f3b09-104">Portal</span></span>](network-watcher-connectivity-portal.md)
> - [<span data-ttu-id="f3b09-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f3b09-105">PowerShell</span></span>](network-watcher-connectivity-powershell.md)
> - [<span data-ttu-id="f3b09-106">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="f3b09-106">CLI 2.0</span></span>](network-watcher-connectivity-cli.md)
> - [<span data-ttu-id="f3b09-107">API REST do Azure</span><span class="sxs-lookup"><span data-stu-id="f3b09-107">Azure REST API</span></span>](network-watcher-connectivity-rest.md)

<span data-ttu-id="f3b09-108">Saiba como toouse conectividade tooverify se uma ligação de TCP direta de um tooa de máquina virtual fornecido ponto final pode ser estabelecida.</span><span class="sxs-lookup"><span data-stu-id="f3b09-108">Learn how toouse connectivity tooverify if a direct TCP connection from a virtual machine tooa given endpoint can be established.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="f3b09-109">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="f3b09-109">Before you begin</span></span>

<span data-ttu-id="f3b09-110">Este artigo pressupõe que tem Olá os seguintes recursos:</span><span class="sxs-lookup"><span data-stu-id="f3b09-110">This article assumes you have hello following resources:</span></span>

* <span data-ttu-id="f3b09-111">Uma instância de observador de rede na região de Olá que pretende toocheck conectividade.</span><span class="sxs-lookup"><span data-stu-id="f3b09-111">An instance of Network Watcher in hello region you want toocheck connectivity.</span></span>

* <span data-ttu-id="f3b09-112">Máquinas virtuais toocheck conectividade.</span><span class="sxs-lookup"><span data-stu-id="f3b09-112">Virtual machines toocheck connectivity with.</span></span>

<span data-ttu-id="f3b09-113">ARMclient é a API de REST de Olá toocall utilizado com o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f3b09-113">ARMclient is used toocall hello REST API using PowerShell.</span></span> <span data-ttu-id="f3b09-114">ARMClient for encontrado no chocolatey em [ARMClient no Chocolatey](https://chocolatey.org/packages/ARMClient).</span><span class="sxs-lookup"><span data-stu-id="f3b09-114">ARMClient is found on chocolatey at [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient).</span></span>

<span data-ttu-id="f3b09-115">Este cenário pressupõe que já tiver seguido os passos de Olá no [criar um observador de rede](network-watcher-create.md) toocreate um observador de rede.</span><span class="sxs-lookup"><span data-stu-id="f3b09-115">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span>

[!INCLUDE [network-watcher-preview](../../includes/network-watcher-public-preview-notice.md)]

> [!IMPORTANT]
> <span data-ttu-id="f3b09-116">Verificação da conectividade requer uma extensão da máquina virtual `AzureNetworkWatcherExtension`.</span><span class="sxs-lookup"><span data-stu-id="f3b09-116">Connectivity check requires a virtual machine extension `AzureNetworkWatcherExtension`.</span></span> <span data-ttu-id="f3b09-117">Para instalar a extensão de Olá numa Windows VM visite [extensão da máquina virtual de agente de observador de rede do Azure para Windows](../virtual-machines/windows/extensions-nwa.md) e para, visite VM com Linux [extensão da máquina virtual de agente de observador de rede do Azure para Linux](../virtual-machines/linux/extensions-nwa.md).</span><span class="sxs-lookup"><span data-stu-id="f3b09-117">For installing hello extension on a Windows VM visit [Azure Network Watcher Agent virtual machine extension for Windows](../virtual-machines/windows/extensions-nwa.md) and for Linux VM visit [Azure Network Watcher Agent virtual machine extension for Linux](../virtual-machines/linux/extensions-nwa.md).</span></span>

## <a name="register-hello-preview-capability"></a><span data-ttu-id="f3b09-118">Registar a capacidade de pré-visualização de Olá</span><span class="sxs-lookup"><span data-stu-id="f3b09-118">Register hello preview capability</span></span>

<span data-ttu-id="f3b09-119">Verificação da conectividade está, atualmente em pré-visualização pública, toouse esta funcionalidade necessita de toobe registado.</span><span class="sxs-lookup"><span data-stu-id="f3b09-119">Connectivity check is currently in public preview, toouse this feature it needs toobe registered.</span></span> <span data-ttu-id="f3b09-120">toodo, Olá de execução do PowerShell exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="f3b09-120">toodo this, run hello following PowerShell sample:</span></span>

```powershell
Register-AzureRmProviderFeature -FeatureName AllowNetworkWatcherConnectivityCheck  -ProviderNamespace Microsoft.Network
Register-AzureRmResourceProvider -ProviderNamespace Microsoft.Network
```

<span data-ttu-id="f3b09-121">o registo de Olá tooverify foi bem sucedido, execute Olá Powershell de exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="f3b09-121">tooverify hello registration was successful, run hello following Powershell sample:</span></span>

```powershell
Get-AzureRmProviderFeature -FeatureName AllowNetworkWatcherConnectivityCheck  -ProviderNamespace  Microsoft.Network
```

<span data-ttu-id="f3b09-122">Se a funcionalidade de Olá foi registada correctamente, saída Olá deve corresponder ao seguinte Olá:</span><span class="sxs-lookup"><span data-stu-id="f3b09-122">If hello feature was properly registered, hello output should match hello following:</span></span>

```
FeatureName                             ProviderName      RegistrationState
-----------                             ------------      -----------------
AllowNetworkWatcherConnectivityCheck    Microsoft.Network Registered
```

## <a name="log-in-with-armclient"></a><span data-ttu-id="f3b09-123">Iniciar sessão com ARMClient</span><span class="sxs-lookup"><span data-stu-id="f3b09-123">Log in with ARMClient</span></span>

<span data-ttu-id="f3b09-124">Inicie sessão no tooarmclient com as suas credenciais do Azure.</span><span class="sxs-lookup"><span data-stu-id="f3b09-124">Log in tooarmclient with your Azure credentials.</span></span>

```PowerShell
armclient login
```

## <a name="retrieve-a-virtual-machine"></a><span data-ttu-id="f3b09-125">Obter uma máquina virtual</span><span class="sxs-lookup"><span data-stu-id="f3b09-125">Retrieve a virtual machine</span></span>

<span data-ttu-id="f3b09-126">Execute Olá tooreturn de script a seguir uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="f3b09-126">Run hello following script tooreturn a virtual machine.</span></span> <span data-ttu-id="f3b09-127">Estas informações são necessárias para a execução de conectividade.</span><span class="sxs-lookup"><span data-stu-id="f3b09-127">This information is needed for running connectivity.</span></span> 

<span data-ttu-id="f3b09-128">Olá seguinte código tem valores para Olá seguintes variáveis:</span><span class="sxs-lookup"><span data-stu-id="f3b09-128">hello following code needs values for hello following variables:</span></span>

- <span data-ttu-id="f3b09-129">**subscriptionId** -Olá toouse de ID de subscrição.</span><span class="sxs-lookup"><span data-stu-id="f3b09-129">**subscriptionId** - hello subscription ID toouse.</span></span>
- <span data-ttu-id="f3b09-130">**resourceGroupName** - hello nome de um grupo de recursos que contém máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="f3b09-130">**resourceGroupName** - hello name of a resource group that contains virtual machines.</span></span>

```powershell
$subscriptionId = '<subscription id>'
$resourceGroupName = '<resource group name>'

armclient get https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Compute/virtualMachines?api-version=2015-05-01-preview
```

<span data-ttu-id="f3b09-131">Do seguinte de Olá de saída, Olá ID da máquina virtual de Olá é utilizado no seguinte exemplo de Olá:</span><span class="sxs-lookup"><span data-stu-id="f3b09-131">From hello following output, hello ID of hello virtual machine is used in hello following example:</span></span>

```json
...
,
      "type": "Microsoft.Compute/virtualMachines",
      "location": "westcentralus",
      "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoExampleRG/providers/Microsoft.Compute
/virtualMachines/ContosoVM",
      "name": "ContosoVM"
    }
  ]
}
```

## <a name="check-connectivity-tooa-virtual-machine"></a><span data-ttu-id="f3b09-132">Verifique a conectividade tooa máquina</span><span class="sxs-lookup"><span data-stu-id="f3b09-132">Check connectivity tooa virtual machine</span></span>

<span data-ttu-id="f3b09-133">Neste exemplo verifica conectividade tooa máquina de virtual de destino através da porta 80.</span><span class="sxs-lookup"><span data-stu-id="f3b09-133">This example checks connectivity tooa destination virtual machine over port 80.</span></span>

### <a name="example"></a><span data-ttu-id="f3b09-134">Exemplo</span><span class="sxs-lookup"><span data-stu-id="f3b09-134">Example</span></span>

```powershell
$subscriptionId = "00000000-0000-0000-0000-000000000000"
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
$sourceResourceId = "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Compute/virtualMachines/MultiTierApp0"
$destinationAddress = "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Compute/virtualMachines/Database0"
$destinationPort = "0"
$requestBody = @"
{
  'source': {
    'resourceId': '${sourceResourceId}',
    'port': 0
  },
  'destination': {
    'resourceId': '${destinationAddress}',
    'port': ${destinationPort}
  }
}
"@

$response = armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/connectivityCheck?api-version=2017-03-01" $requestBody
```

<span data-ttu-id="f3b09-135">Uma vez que esta operação é muito a executar, Olá resultado Olá é devolvido o URI no cabeçalho de resposta de Olá conforme mostrado no Olá seguinte resposta:</span><span class="sxs-lookup"><span data-stu-id="f3b09-135">Since this operation is long running, hello URI for hello result is returned in hello response header as shown in hello following response:</span></span>

<span data-ttu-id="f3b09-136">**Valores importantes**</span><span class="sxs-lookup"><span data-stu-id="f3b09-136">**Important Values**</span></span>

* <span data-ttu-id="f3b09-137">**Localização** -esta propriedade contém Olá URI onde Olá os resultados são quando hello operação foi concluída</span><span class="sxs-lookup"><span data-stu-id="f3b09-137">**Location** - This property contains hello URI where hello results are when hello operation is complete</span></span>

```
HTTP/1.1 202 Accepted
Pragma: no-cache
Retry-After: 10
x-ms-request-id: f09b55fe-1d3a-4df7-817f-bceb8d2a94c8
Strict-Transport-Security: max-age=31536000; includeSubDomains
Cache-Control: no-cache
Location: https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operationResults/f09b55fe-1d3a-4df7-817f-bceb8d2a94c8?api-version=2017-03-01
Server: Microsoft-HTTPAPI/2.0; Microsoft-HTTPAPI/2.0
x-ms-ratelimit-remaining-subscription-writes: 1199
x-ms-correlation-request-id: 367a91aa-7142-436a-867d-d3a36f80bc54
x-ms-routing-request-id: WESTUS2:20170602T202117Z:367a91aa-7142-436a-867d-d3a36f80bc54
Date: Fri, 02 Jun 2017 20:21:16 GMT

null
```

### <a name="response"></a><span data-ttu-id="f3b09-138">Resposta</span><span class="sxs-lookup"><span data-stu-id="f3b09-138">Response</span></span>

<span data-ttu-id="f3b09-139">Olá seguinte resposta é do exemplo anterior Olá.</span><span class="sxs-lookup"><span data-stu-id="f3b09-139">hello following response is from hello previous example.</span></span>  <span data-ttu-id="f3b09-140">Esta resposta, Olá `ConnectionStatus` é **Unreachable**.</span><span class="sxs-lookup"><span data-stu-id="f3b09-140">In this response, hello `ConnectionStatus` is **Unreachable**.</span></span> <span data-ttu-id="f3b09-141">Pode ver todos os Olá de sondas enviadas com falhas.</span><span class="sxs-lookup"><span data-stu-id="f3b09-141">You can see that all hello probes sent failed.</span></span> <span data-ttu-id="f3b09-142">Falha de conectividade de Olá na aplicação virtual Olá tooa devida configurada pelo utilizador `NetworkSecurityRule` denominado **UserRule_Port80**, configurado tooblock tráfego de entrada na porta 80.</span><span class="sxs-lookup"><span data-stu-id="f3b09-142">hello connectivity failed at hello virtual appliance due tooa user-configured `NetworkSecurityRule` named **UserRule_Port80**, configured tooblock incoming traffic on port 80.</span></span> <span data-ttu-id="f3b09-143">Estas informações podem ser utilizados tooresearch problemas de ligação.</span><span class="sxs-lookup"><span data-stu-id="f3b09-143">This information can be used tooresearch connection issues.</span></span>

```json
{
  "hops": [
    {
      "type": "Source",
      "id": "0cb75c91-7ebf-4df8-8424-15594d6fb51c",
      "address": "10.1.1.4",
      "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/appNic0/ipConfigurations/ipconfig1",
      "nextHopIds": [
        "06dee00a-9c4a-4fb1-b2ea-fa0a539ca684"
      ],
      "issues": []
    },
    {
      "type": "VirtualAppliance",
      "id": "06dee00a-9c4a-4fb1-b2ea-fa0a539ca684",
      "address": "10.1.2.4",
      "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/fwNic/ipConfigurations/ipconfig1",
      "nextHopIds": [
        "75e0cfa5-f9d2-48d8-b705-2c7016f81570"
      ],
      "issues": []
    },
    {
      "type": "VirtualAppliance",
      "id": "75e0cfa5-f9d2-48d8-b705-2c7016f81570",
      "address": "10.1.3.4",
      "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/auNic/ipConfigurations/ipconfig1",
      "nextHopIds": [
        "86caf6aa-33b0-48a1-b4da-f3c9ce785072"
      ],
      "issues": [
        {
          "origin": "Outbound",
          "severity": "Error",
          "type": "NetworkSecurityRule",
          "context": [
            {
              "key": "RuleName",
              "value": "UserRule_Port80"
            }
          ]
        }
      ]
    },
    {
      "type": "VnetLocal",
      "id": "86caf6aa-33b0-48a1-b4da-f3c9ce785072",
      "address": "10.1.4.4",
      "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/dbNic0/ipConfigurations/ipconfig1",
      "nextHopIds": [],
      "issues": []
    }
  ],
  "connectionStatus": "Unreachable",
  "probesSent": 100,
  "probesFailed": 100
}
```

## <a name="validate-routing-issues"></a><span data-ttu-id="f3b09-144">Validar a problemas de encaminhamento</span><span class="sxs-lookup"><span data-stu-id="f3b09-144">Validate routing issues</span></span>

<span data-ttu-id="f3b09-145">exemplo de Olá verifica a conectividade entre uma máquina virtual e um ponto final remoto.</span><span class="sxs-lookup"><span data-stu-id="f3b09-145">hello example checks connectivity between a virtual machine and a remote endpoint.</span></span>

### <a name="example"></a><span data-ttu-id="f3b09-146">Exemplo</span><span class="sxs-lookup"><span data-stu-id="f3b09-146">Example</span></span>

```powershell
$subscriptionId = "00000000-0000-0000-0000-000000000000"
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
$sourceResourceId = "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Compute/virtualMachines/MultiTierApp0"
$destinationAddress = "13.107.21.200"
$destinationPort = "80"
$requestBody = @"
{
  'source': {
    'resourceId': '${sourceResourceId}',
    'port': 0
  },
  'destination': {
    'address': '${destinationAddress}',
    'port': ${destinationPort}
  }
}
"@

$response = armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/connectivityCheck?api-version=2017-03-01" $requestBody
```

<span data-ttu-id="f3b09-147">Uma vez que esta operação é muito a executar, Olá resultado Olá é devolvido o URI no cabeçalho de resposta de Olá conforme mostrado no Olá seguinte resposta:</span><span class="sxs-lookup"><span data-stu-id="f3b09-147">Since this operation is long running, hello URI for hello result is returned in hello response header as shown in hello following response:</span></span>

<span data-ttu-id="f3b09-148">**Valores importantes**</span><span class="sxs-lookup"><span data-stu-id="f3b09-148">**Important Values**</span></span>

* <span data-ttu-id="f3b09-149">**Localização** -esta propriedade contém Olá URI onde Olá os resultados são quando hello operação foi concluída</span><span class="sxs-lookup"><span data-stu-id="f3b09-149">**Location** - This property contains hello URI where hello results are when hello operation is complete</span></span>

```
HTTP/1.1 202 Accepted
Pragma: no-cache
Retry-After: 10
x-ms-request-id: 15eeeb69-fcef-41db-bc4a-e2adcf2658e0
Strict-Transport-Security: max-age=31536000; includeSubDomains
Cache-Control: no-cache
Location: https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operationResults/15eeeb69-fcef-41db-bc4a-e2adcf2658e0?api-version=2017-03-01
Server: Microsoft-HTTPAPI/2.0; Microsoft-HTTPAPI/2.0
x-ms-ratelimit-remaining-subscription-writes: 1199
x-ms-correlation-request-id: 4370b798-cd8b-4d3e-ba28-22232bc81dc5
x-ms-routing-request-id: WESTUS:20170602T202606Z:4370b798-cd8b-4d3e-ba28-22232bc81dc5
Date: Fri, 02 Jun 2017 20:26:05 GMT

null
```

### <a name="response"></a><span data-ttu-id="f3b09-150">Resposta</span><span class="sxs-lookup"><span data-stu-id="f3b09-150">Response</span></span>

<span data-ttu-id="f3b09-151">No seguinte exemplo de Olá, Olá `connectionStatus` é mostrado como **Unreachable**.</span><span class="sxs-lookup"><span data-stu-id="f3b09-151">In hello following example, hello `connectionStatus` is shown as **Unreachable**.</span></span> <span data-ttu-id="f3b09-152">No Olá `hops` mais detalhes, pode ver em `issues` que tráfego Olá foi bloqueado devido tooa `UserDefinedRoute`.</span><span class="sxs-lookup"><span data-stu-id="f3b09-152">In hello `hops` details, you can see under `issues` that hello traffic was blocked due tooa `UserDefinedRoute`.</span></span>

```json
{
  "hops": [
    {
      "type": "Source",
      "id": "5528055a-b393-4751-97bc-353d8c0aaeff",
      "address": "10.1.1.4",
      "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/appNic0/ipConfigurations/ipconfig1",
      "nextHopIds": [
        "66eefa79-5bfe-48b2-b6ca-eec8247457a3"
      ],
      "issues": [
        {
          "origin": "Outbound",
          "severity": "Error",
          "type": "UserDefinedRoute",
          "context": [
            {
              "key": "RouteType",
              "value": "User"
            }
          ]
        }
      ]
    },
    {
      "type": "Destination",
      "id": "66eefa79-5bfe-48b2-b6ca-eec8247457a3",
      "address": "13.107.21.200",
      "resourceId": "Unknown",
      "nextHopIds": [],
      "issues": []
    }
  ],
  "connectionStatus": "Unreachable",
  "probesSent": 100,
  "probesFailed": 100
}
```

## <a name="check-website-latency"></a><span data-ttu-id="f3b09-153">Verifique a latência de Web site</span><span class="sxs-lookup"><span data-stu-id="f3b09-153">Check website latency</span></span>

<span data-ttu-id="f3b09-154">Olá exemplo seguinte verifica o Web site do Olá conectividade tooa.</span><span class="sxs-lookup"><span data-stu-id="f3b09-154">hello following example checks hello connectivity tooa website.</span></span>

### <a name="example"></a><span data-ttu-id="f3b09-155">Exemplo</span><span class="sxs-lookup"><span data-stu-id="f3b09-155">Example</span></span>

```powershell
$subscriptionId = "00000000-0000-0000-0000-000000000000"
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
$sourceResourceId = "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Compute/virtualMachines/MultiTierApp0"
$destinationAddress = "http://bing.com"
$destinationPort = "0"
$requestBody = @"
{
  'source': {
    'resourceId': '${sourceResourceId}',
    'port': 0
  },
  'destination': {
    'address': '${destinationAddress}',
    'port': ${destinationPort}
  }
}
"@

$response = armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/connectivityCheck?api-version=2017-03-01" $requestBody
```

<span data-ttu-id="f3b09-156">Uma vez que esta operação é muito a executar, Olá resultado Olá é devolvido o URI no cabeçalho de resposta de Olá conforme mostrado no Olá seguinte resposta:</span><span class="sxs-lookup"><span data-stu-id="f3b09-156">Since this operation is long running, hello URI for hello result is returned in hello response header as shown in hello following response:</span></span>

<span data-ttu-id="f3b09-157">**Valores importantes**</span><span class="sxs-lookup"><span data-stu-id="f3b09-157">**Important Values**</span></span>

* <span data-ttu-id="f3b09-158">**Localização** -esta propriedade contém Olá URI onde Olá os resultados são quando hello operação foi concluída</span><span class="sxs-lookup"><span data-stu-id="f3b09-158">**Location** - This property contains hello URI where hello results are when hello operation is complete</span></span>

```
HTTP/1.1 202 Accepted
Pragma: no-cache
Retry-After: 10
x-ms-request-id: e49b12c7-c232-472c-b6d2-6c257ce80fa5
Strict-Transport-Security: max-age=31536000; includeSubDomains
Cache-Control: no-cache
Location: https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operationResults/e49b12c7-c232-472c-b6d2-6c257ce80fa5?api-version=2017-03-01
Server: Microsoft-HTTPAPI/2.0; Microsoft-HTTPAPI/2.0
x-ms-ratelimit-remaining-subscription-writes: 1199
x-ms-correlation-request-id: c3d9744f-5683-427d-bdd1-636b68ab01b6
x-ms-routing-request-id: WESTUS:20170602T203101Z:c3d9744f-5683-427d-bdd1-636b68ab01b6
Date: Fri, 02 Jun 2017 20:31:00 GMT

null
```

### <a name="response"></a><span data-ttu-id="f3b09-159">Resposta</span><span class="sxs-lookup"><span data-stu-id="f3b09-159">Response</span></span>

<span data-ttu-id="f3b09-160">Olá resposta a seguir, pode ver Olá `connectionStatus` mostra como **Reachable**.</span><span class="sxs-lookup"><span data-stu-id="f3b09-160">In hello following response, you can see hello `connectionStatus` shows as **Reachable**.</span></span> <span data-ttu-id="f3b09-161">Quando uma ligação é bem-sucedida, são fornecidos valores de latência.</span><span class="sxs-lookup"><span data-stu-id="f3b09-161">When a connection is successful, latency values are provided.</span></span>

```json
{
  "hops": [
    {
      "type": "Source",
      "id": "6adc0fe1-e384-4220-b1b1-f0d181220072",
      "address": "10.1.1.4",
      "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/appNic0/ipConfigurations/ipconfig1",
      "nextHopIds": [
        "b50b7076-9ff2-4782-b40e-0b89cf758f74"
      ],
      "issues": []
    },
    {
      "type": "Internet",
      "id": "b50b7076-9ff2-4782-b40e-0b89cf758f74",
      "address": "204.79.197.200",
      "resourceId": "Internet",
      "nextHopIds": [],
      "issues": []
    }
  ],
  "connectionStatus": "Reachable",
  "avgLatencyInMs": 1,
  "minLatencyInMs": 0,
  "maxLatencyInMs": 7,
  "probesSent": 100,
  "probesFailed": 0
}
```

## <a name="check-connectivity-tooa-storage-endpoint"></a><span data-ttu-id="f3b09-162">Verifique o ponto final de armazenamento de tooa de conectividade</span><span class="sxs-lookup"><span data-stu-id="f3b09-162">Check connectivity tooa storage endpoint</span></span>

<span data-ttu-id="f3b09-163">Olá exemplo seguinte verifica a conetividade de Olá de uma conta de armazenamento do blogue de tooa máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="f3b09-163">hello following example checks hello connectivity from a virtual machine tooa blog storage account.</span></span>

### <a name="example"></a><span data-ttu-id="f3b09-164">Exemplo</span><span class="sxs-lookup"><span data-stu-id="f3b09-164">Example</span></span>

```powershell
$subscriptionId = "00000000-0000-0000-0000-000000000000"
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
$sourceResourceId = "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Compute/virtualMachines/MultiTierApp0"
$destinationAddress = "https://build2017nwdiag360.blob.core.windows.net/"
$destinationPort = "0"
$requestBody = @"
{
  'source': {
    'resourceId': '${sourceResourceId}',
    'port': 0
  },
  'destination': {
    'address': '${destinationAddress}',
    'port': ${destinationPort}
  }
}
"@

$response = armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/connectivityCheck?api-version=2017-03-01" $requestBody
```

<span data-ttu-id="f3b09-165">Uma vez que esta operação é muito a executar, Olá resultado Olá é devolvido o URI no cabeçalho de resposta de Olá conforme mostrado no Olá seguinte resposta:</span><span class="sxs-lookup"><span data-stu-id="f3b09-165">Since this operation is long running, hello URI for hello result is returned in hello response header as shown in hello following response:</span></span>

<span data-ttu-id="f3b09-166">**Valores importantes**</span><span class="sxs-lookup"><span data-stu-id="f3b09-166">**Important Values**</span></span>

* <span data-ttu-id="f3b09-167">**Localização** -esta propriedade contém Olá URI onde Olá os resultados são quando hello operação foi concluída</span><span class="sxs-lookup"><span data-stu-id="f3b09-167">**Location** - This property contains hello URI where hello results are when hello operation is complete</span></span>

```
HTTP/1.1 202 Accepted
Pragma: no-cache
Retry-After: 10
x-ms-request-id: c4ed3806-61ea-4a6b-abc1-9d6f2afc79c2
Strict-Transport-Security: max-age=31536000; includeSubDomains
Cache-Control: no-cache
Location: https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operationResults/c4ed3806-61ea-4a6b-abc1-9d6f2afc79c2?api-version=2017-03-01
Server: Microsoft-HTTPAPI/2.0; Microsoft-HTTPAPI/2.0
x-ms-ratelimit-remaining-subscription-writes: 1199
x-ms-correlation-request-id: 93bf5af0-fef5-4b7a-bb9e-9976ba5cdb95
x-ms-routing-request-id: WESTUS2:20170602T200504Z:93bf5af0-fef5-4b7a-bb9e-9976ba5cdb95
Date: Fri, 02 Jun 2017 20:05:03 GMT

null
```

### <a name="response"></a><span data-ttu-id="f3b09-168">Resposta</span><span class="sxs-lookup"><span data-stu-id="f3b09-168">Response</span></span>

<span data-ttu-id="f3b09-169">Olá exemplo seguinte é resposta Olá a execução de chamada de API Olá anterior.</span><span class="sxs-lookup"><span data-stu-id="f3b09-169">hello following example is hello response from running hello previous API call.</span></span> <span data-ttu-id="f3b09-170">Como a verificação de Olá for bem sucedida, Olá `connectionStatus` propriedade mostra como **Reachable**.</span><span class="sxs-lookup"><span data-stu-id="f3b09-170">As hello check is successful, hello `connectionStatus` property shows as **Reachable**.</span></span>  <span data-ttu-id="f3b09-171">São fornecidos detalhes de Olá sobre o número de Olá de blob de armazenamento do saltos tooreach necessário Olá e latência.</span><span class="sxs-lookup"><span data-stu-id="f3b09-171">You are provided hello details regarding hello number of hops required tooreach hello storage blob and latency.</span></span>

```json
{
  "hops": [
    {
      "type": "Source",
      "id": "6adc0fe1-e384-4220-b1b1-f0d181220072",
      "address": "10.1.1.4",
      "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/appNic0/ipConfigurations/ipconfig1",
      "nextHopIds": [
        "b50b7076-9ff2-4782-b40e-0b89cf758f74"
      ],
      "issues": []
    },
    {
      "type": "Internet",
      "id": "b50b7076-9ff2-4782-b40e-0b89cf758f74",
      "address": "13.71.200.248",
      "resourceId": "Internet",
      "nextHopIds": [],
      "issues": []
    }
  ],
  "connectionStatus": "Reachable",
  "avgLatencyInMs": 1,
  "minLatencyInMs": 0,
  "maxLatencyInMs": 7,
  "probesSent": 100,
  "probesFailed": 0
}
```

## <a name="next-steps"></a><span data-ttu-id="f3b09-172">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="f3b09-172">Next steps</span></span>

<span data-ttu-id="f3b09-173">Saiba como capturas de pacotes de tooautomate com alertas de Máquina Virtual visualizando [criar uma captura de pacotes accionadas alerta](network-watcher-alert-triggered-packet-capture.md)</span><span class="sxs-lookup"><span data-stu-id="f3b09-173">Learn how tooautomate packet captures with Virtual machine alerts by viewing [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span></span>

<span data-ttu-id="f3b09-174">Determinar se determinados o tráfego é permitido dentro ou fora da sua VM, visitando [Certifique-se de fluxo de verificação de IP](network-watcher-check-ip-flow-verify-portal.md)</span><span class="sxs-lookup"><span data-stu-id="f3b09-174">Find if certain traffic is allowed in or out of your VM by visiting [Check IP flow verify](network-watcher-check-ip-flow-verify-portal.md)</span></span>

<!-- Image references -->














