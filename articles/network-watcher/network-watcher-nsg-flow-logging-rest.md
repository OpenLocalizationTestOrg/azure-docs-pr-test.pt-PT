---
title: "os registos de aaaManage fluxo do grupo de segurança de rede com o observador de rede do Azure - REST API | Microsoft Docs"
description: "Esta página explica como toomanage fluxo do grupo de segurança de rede nos registos observador de rede do Azure com a REST API"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 2ab25379-0fd3-4bfe-9d82-425dfc7ad6bb
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: be81e35f4d01c67efef99773e9b4e2ae4b8e209e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-network-security-group-flow-logs-using-rest-api"></a><span data-ttu-id="7cd49-103">Registos de fluxo de configurar o grupo de segurança de rede através da API de REST</span><span class="sxs-lookup"><span data-stu-id="7cd49-103">Configuring Network Security Group flow logs using REST API</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="7cd49-104">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="7cd49-104">Azure portal</span></span>](network-watcher-nsg-flow-logging-portal.md)
> - [<span data-ttu-id="7cd49-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="7cd49-105">PowerShell</span></span>](network-watcher-nsg-flow-logging-powershell.md)
> - [<span data-ttu-id="7cd49-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="7cd49-106">CLI 1.0</span></span>](network-watcher-nsg-flow-logging-cli-nodejs.md)
> - [<span data-ttu-id="7cd49-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="7cd49-107">CLI 2.0</span></span>](network-watcher-nsg-flow-logging-cli.md)
> - [<span data-ttu-id="7cd49-108">API REST</span><span class="sxs-lookup"><span data-stu-id="7cd49-108">REST API</span></span>](network-watcher-nsg-flow-logging-rest.md)

<span data-ttu-id="7cd49-109">Registos de fluxo do grupo de segurança de rede são uma funcionalidade do observador de rede que permite-lhe tooview informações sobre o tráfego IP de entrada e de saída através de um grupo de segurança de rede.</span><span class="sxs-lookup"><span data-stu-id="7cd49-109">Network Security Group flow logs are a feature of Network Watcher that allows you tooview information about ingress and egress IP traffic through a Network Security Group.</span></span> <span data-ttu-id="7cd49-110">Estes registos de fluxo são escritos no formato json e mostram a saída e entrados fluxos numa base por regra, Olá fluxo de Olá NIC se aplica, informações de 5 cadeias de identificação sobre o fluxo de Olá (origem/destino IP, porta de origem/destino, protocolo) e se hello tráfego foi permitido ou negado.</span><span class="sxs-lookup"><span data-stu-id="7cd49-110">These flow logs are written in json format and show outbound and inbound flows on a per rule basis, hello NIC hello flow applies to, 5-tuple information about hello flow (Source/Destination IP, Source/Destination Port, Protocol), and if hello traffic was allowed or denied.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="7cd49-111">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="7cd49-111">Before you begin</span></span>

<span data-ttu-id="7cd49-112">ARMclient é a API de REST de Olá toocall utilizado com o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7cd49-112">ARMclient is used toocall hello REST API using PowerShell.</span></span> <span data-ttu-id="7cd49-113">ARMClient for encontrado no chocolatey em [ARMClient no Chocolatey](https://chocolatey.org/packages/ARMClient)</span><span class="sxs-lookup"><span data-stu-id="7cd49-113">ARMClient is found on chocolatey at [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient)</span></span>

<span data-ttu-id="7cd49-114">Este cenário pressupõe que já tiver seguido os passos de Olá no [criar um observador de rede](network-watcher-create.md) toocreate um observador de rede.</span><span class="sxs-lookup"><span data-stu-id="7cd49-114">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span>

> [!Important]
> <span data-ttu-id="7cd49-115">Para a API de REST de observador de rede chamadas Olá nome do grupo de recursos no pedido de Olá que URI é o grupo de recursos de Olá contém Olá observador de rede, não os recursos de Olá estiver a efetuar ações de diagnóstico Olá do.</span><span class="sxs-lookup"><span data-stu-id="7cd49-115">For Network Watcher REST API calls hello resource group name in hello request URI is hello resource group that contains hello Network Watcher, not hello resources you are performing hello diagnostic actions on.</span></span>

## <a name="scenario"></a><span data-ttu-id="7cd49-116">Cenário</span><span class="sxs-lookup"><span data-stu-id="7cd49-116">Scenario</span></span>

<span data-ttu-id="7cd49-117">cenário de Olá abordado neste artigo mostra-lhe como tooenable, desativar e consulta o fluxo de registos com Olá REST API.</span><span class="sxs-lookup"><span data-stu-id="7cd49-117">hello scenario covered in this article shows you how tooenable, disable, and query flow logs using hello REST API.</span></span> <span data-ttu-id="7cd49-118">toolearn mais informações sobre loggings de fluxo do grupo de segurança de rede, visite [registo de fluxo do grupo de segurança de rede - descrição geral](network-watcher-nsg-flow-logging-overview.md).</span><span class="sxs-lookup"><span data-stu-id="7cd49-118">toolearn more about Network Security Group flow loggings, visit [Network Security Group flow logging - Overview](network-watcher-nsg-flow-logging-overview.md).</span></span>

<span data-ttu-id="7cd49-119">Neste cenário, irá:</span><span class="sxs-lookup"><span data-stu-id="7cd49-119">In this scenario, you will:</span></span>

* <span data-ttu-id="7cd49-120">Ativar registos de fluxo</span><span class="sxs-lookup"><span data-stu-id="7cd49-120">Enable flow logs</span></span>
* <span data-ttu-id="7cd49-121">Desativar os registos de fluxo</span><span class="sxs-lookup"><span data-stu-id="7cd49-121">Disable flow logs</span></span>
* <span data-ttu-id="7cd49-122">Estado de registos de fluxo de consulta</span><span class="sxs-lookup"><span data-stu-id="7cd49-122">Query flow logs status</span></span>

## <a name="log-in-with-armclient"></a><span data-ttu-id="7cd49-123">Iniciar sessão com ARMClient</span><span class="sxs-lookup"><span data-stu-id="7cd49-123">Log in with ARMClient</span></span>

<span data-ttu-id="7cd49-124">Inicie sessão no tooarmclient com as suas credenciais do Azure.</span><span class="sxs-lookup"><span data-stu-id="7cd49-124">Log in tooarmclient with your Azure credentials.</span></span>

```PowerShell
armclient login
```

## <a name="register-insights-provider"></a><span data-ttu-id="7cd49-125">Fornecedor de informações de registo</span><span class="sxs-lookup"><span data-stu-id="7cd49-125">Register Insights provider</span></span>

<span data-ttu-id="7cd49-126">Ordem de fluxo de registo toowork com êxito, Olá **insights** fornecedor tem de estar registado.</span><span class="sxs-lookup"><span data-stu-id="7cd49-126">In order for flow logging toowork successfully, hello **Microsoft.Insights** provider must be registered.</span></span> <span data-ttu-id="7cd49-127">Se não tem a certeza se hello **insights** fornecedor está registado, hello execute seguinte script.</span><span class="sxs-lookup"><span data-stu-id="7cd49-127">If you are not sure if hello **Microsoft.Insights** provider is registered, run hello following script.</span></span>

```powershell
$subscriptionId = "00000000-0000-0000-0000-000000000000"
armclient post "https://management.azure.com//subscriptions/${subscriptionId}/providers/Microsoft.Insights/register?api-version=2016-09-01"
```

## <a name="enable-network-security-group-flow-logs"></a><span data-ttu-id="7cd49-128">Registos de fluxo de ativar o grupo de segurança de rede</span><span class="sxs-lookup"><span data-stu-id="7cd49-128">Enable Network Security Group flow logs</span></span>

<span data-ttu-id="7cd49-129">Olá comando tooenable fluxo registos é mostrado no seguinte exemplo de Olá:</span><span class="sxs-lookup"><span data-stu-id="7cd49-129">hello command tooenable flow logs is shown in hello following example:</span></span>

```powershell
$subscriptionId = "00000000-0000-0000-0000-000000000000"
$targetUri = "" # example /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/{resourceGroupName/providers/Microsoft.Network/networkSecurityGroups/{nsgName}"
$storageId = "/subscriptions/00000000-0000-0000-0000-000000000000/{resourceGroupName/providers/Microsoft.Storage/storageAccounts/{saName}"
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
$requestBody = @"
{
    'targetResourceId': '${targetUri}',
    'properties': {
    'storageId': '${storageId}',
    'enabled': 'true',
    'retentionPolicy' : {
            days: 5,
            enabled: true
        }
    }
}
"@

armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/configureFlowLog?api-version=2016-12-01" $requestBody
```

<span data-ttu-id="7cd49-130">resposta Olá devolvido de Olá anterior exemplo é o seguinte:</span><span class="sxs-lookup"><span data-stu-id="7cd49-130">hello response returned from hello preceding example is as follows:</span></span>

```json
{
  "targetResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/networkSecurityGroups/{nsgName}",
  "properties": {
    "storageId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{saName}",
    "enabled": true,
    "retentionPolicy": {
      "days": 5,
      "enabled": true
    }
  }
}
```

## <a name="disable-network-security-group-flow-logs"></a><span data-ttu-id="7cd49-131">Registos de fluxo de desativar o grupo de segurança de rede</span><span class="sxs-lookup"><span data-stu-id="7cd49-131">Disable Network Security Group flow logs</span></span>

<span data-ttu-id="7cd49-132">Os seguintes registos de fluxo de toodisable de exemplo Olá de utilização.</span><span class="sxs-lookup"><span data-stu-id="7cd49-132">Use hello following example toodisable flow logs.</span></span> <span data-ttu-id="7cd49-133">Olá chamada é Olá mesmo que ativar registos de fluxo, exceto **falso** está definido para a propriedade Olá ativada.</span><span class="sxs-lookup"><span data-stu-id="7cd49-133">hello call is hello same as enabling flow logs, except **false** is set for hello enabled property.</span></span>

```powershell
$subscriptionId = "00000000-0000-0000-0000-000000000000"
$targetUri = "" # example /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/{resourceGroupName/providers/Microsoft.Network/networkSecurityGroups/{nsgName}"
$storageId = "/subscriptions/00000000-0000-0000-0000-000000000000/{resourceGroupName/providers/Microsoft.Storage/storageAccounts/{saName}"
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
$requestBody = @"
{
    'targetResourceId': '${targetUri}',
    'properties': {
    'storageId': '${storageId}',
    'enabled': 'false',
    'retentionPolicy' : {
            days: 5,
            enabled: true
        }
    }
}
"@

armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/configureFlowLog?api-version=2016-12-01" $requestBody
```

<span data-ttu-id="7cd49-134">resposta Olá devolvido de Olá anterior exemplo é o seguinte:</span><span class="sxs-lookup"><span data-stu-id="7cd49-134">hello response returned from hello preceding example is as follows:</span></span>

```json
{
  "targetResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/networkSecurityGroups/{nsgName}",
  "properties": {
    "storageId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{saName}",
    "enabled": false,
    "retentionPolicy": {
      "days": 5,
      "enabled": true
    }
  }
}
```

## <a name="query-flow-logs"></a><span data-ttu-id="7cd49-135">Registos de fluxo de consulta</span><span class="sxs-lookup"><span data-stu-id="7cd49-135">Query flow logs</span></span>

<span data-ttu-id="7cd49-136">Olá chamada REST de consultas de estado do fluxo de Olá os seguintes os registos de um grupo de segurança de rede.</span><span class="sxs-lookup"><span data-stu-id="7cd49-136">hello following REST call queries hello status of flow logs on a Network Security Group.</span></span>

```powershell
$subscriptionId = "00000000-0000-0000-0000-000000000000"
$targetUri = "" # example /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/{resourceGroupName/providers/Microsoft.Network/networkSecurityGroups/{nsgName}"
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
$requestBody = @"
{
    'targetResourceId': '${targetUri}',
}
"@

armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/queryFlowLogStatus?api-version=2016-12-01" $requestBody
```

<span data-ttu-id="7cd49-137">Olá segue-se um exemplo de Olá resposta devolvida:</span><span class="sxs-lookup"><span data-stu-id="7cd49-137">hello following is an example of hello response returned:</span></span>

```json
{
  "targetResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/networkSecurityGroups/{nsgName}",
  "properties": {
    "storageId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{saName}",
    "enabled": true,
   "retentionPolicy": {
      "days": 5,
      "enabled": true
    }
  }
}
```

## <a name="download-a-flow-log"></a><span data-ttu-id="7cd49-138">Transferir um registo de fluxo</span><span class="sxs-lookup"><span data-stu-id="7cd49-138">Download a flow log</span></span>

<span data-ttu-id="7cd49-139">localização de armazenamento Olá de um registo de fluxo é definida na criação.</span><span class="sxs-lookup"><span data-stu-id="7cd49-139">hello storage location of a flow log is defined at creation.</span></span> <span data-ttu-id="7cd49-140">Um tooaccess ferramenta conveniente destas contas de armazenamento do fluxo registos guardados tooa é Explorador de armazenamento do Microsoft Azure, que pode ser transferida aqui: http://storageexplorer.com/</span><span class="sxs-lookup"><span data-stu-id="7cd49-140">A convenient tool tooaccess these flow logs saved tooa storage account is Microsoft Azure Storage Explorer, which can be downloaded here:  http://storageexplorer.com/</span></span>

<span data-ttu-id="7cd49-141">Se for especificada uma conta de armazenamento, ficheiros de captura de pacotes são guardados tooa a conta de armazenamento em Olá seguinte localização:</span><span class="sxs-lookup"><span data-stu-id="7cd49-141">If a storage account is specified, packet capture files are saved tooa storage account at hello following location:</span></span>

```
https://{storageAccountName}.blob.core.windows.net/insights-logs-networksecuritygroupflowevent/resourceId%3D/subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/microsoft.network/networksecuritygroups/{nsgName}/{year}/{month}/{day}/PT1H.json
```

## <a name="next-steps"></a><span data-ttu-id="7cd49-142">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="7cd49-142">Next steps</span></span>

<span data-ttu-id="7cd49-143">Saiba como demasiado[visualizar os registos de fluxo NSG com o PowerBI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span><span class="sxs-lookup"><span data-stu-id="7cd49-143">Learn how too[Visualize your NSG flow logs with PowerBI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span></span>

<span data-ttu-id="7cd49-144">Saiba como demasiado[visualizar os registos de fluxo NSG com ferramentas open source](network-watcher-visualize-nsg-flow-logs-open-source-tools.md)</span><span class="sxs-lookup"><span data-stu-id="7cd49-144">Learn how too[Visualize your NSG flow logs with open source tools](network-watcher-visualize-nsg-flow-logs-open-source-tools.md)</span></span>
