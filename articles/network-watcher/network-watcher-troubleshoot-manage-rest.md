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
# <a name="troubleshoot-virtual-network-gateway-and-connections-using-azure-network-watcher"></a>Resolver problemas de gateway de rede Virtual e ligações utilizando o observador de rede do Azure

> [!div class="op_single_selector"]
> - [Portal](network-watcher-troubleshoot-manage-portal.md)
> - [PowerShell](network-watcher-troubleshoot-manage-powershell.md)
> - [CLI 1.0](network-watcher-troubleshoot-manage-cli-nodejs.md)
> - [CLI 2.0](network-watcher-troubleshoot-manage-cli.md)
> - [API REST](network-watcher-troubleshoot-manage-rest.md)

Observador de rede oferece muitas funcionalidades no que respeita toounderstanding os recursos de rede no Azure. Uma dessas funcionalidades é recursos de resolução de problemas. Resolução de problemas de recursos pode ser chamada através do portal de Olá, do PowerShell, CLI ou REST API. Quando chamado, o observador de rede inspeciona o estado de funcionamento de Olá de um Gateway de rede Virtual ou uma ligação e devolve conclusões.

Este artigo leva-o através de tarefas de gestão diferentes Olá que estão atualmente disponíveis para a resolução de problemas de recursos.

- [**Resolver problemas relacionados com um gateway de rede Virtual**](#troubleshoot-a-virtual-network-gateway)
- [**Resolver problemas de uma ligação**](#troubleshoot-connections)

## <a name="before-you-begin"></a>Antes de começar

ARMclient é a API de REST de Olá toocall utilizado com o PowerShell. ARMClient for encontrado no chocolatey em [ARMClient no Chocolatey](https://chocolatey.org/packages/ARMClient)

Este cenário pressupõe que já tiver seguido os passos de Olá no [criar um observador de rede](network-watcher-create.md) toocreate um observador de rede.

Para obter uma lista de visita de tipos de gateway suportados, [tipos de Gateway suportado](network-watcher-troubleshoot-overview.md#supported-gateway-types).

## <a name="overview"></a>Descrição geral

Resolução de problemas de observador de rede fornece a capacidade de Olá resolver problemas que surgem com gateways de rede Virtual e ligações. Quando é efetuado um pedido de recurso toohello e resolução de problemas, registos estiver a consultar inspecioná-los. Quando a inspeção estiver concluída, resultados de Olá são devolvidos. API de resolução de problemas do Olá pedidos são longos pedidos, o que pode demorar vários minutos tooreturn um resultado em execução. Os registos são armazenados num contentor numa conta de armazenamento.

## <a name="log-in-with-armclient"></a>Iniciar sessão com ARMClient

```PowerShell
armclient login
```

## <a name="troubleshoot-a-virtual-network-gateway"></a>Resolver problemas relacionados com um gateway de rede Virtual


### <a name="post-hello-troubleshoot-request"></a>Olá POST resolver problemas do pedido

Olá seguir o estado de Olá de consultas de exemplo de um gateway de rede Virtual.

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

Uma vez que esta operação é muito a executar, hello URI para consultar a operação de Olá e Olá URI para o resultado de Olá é devolvido no cabeçalho de resposta de Olá, conforme mostrado no Olá seguinte resposta:

**Valores importantes**

* **Azure AsyncOperation** -esta propriedade contém Olá URI tooquery Olá Async resolver problemas de operação
* **Localização** -esta propriedade contém Olá URI onde Olá os resultados são quando hello operação foi concluída

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

### <a name="query-hello-async-operation-for-completion"></a>Olá async operação para conclusão de consulta

Utilize Olá operações URI tooquery para progresso Olá operação de Olá, como mostrado no seguinte exemplo de Olá:

```powershell
armclient get "https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operations/8a1167b7-6768-4ac1-85dc-703c9c9b9247?api-version=2016-03-30"
```

Enquanto a operação de Olá está em curso, Olá resposta mostra **em curso** como mostrado no seguinte exemplo de Olá:

```json
{
  "status": "InProgress"
}
```

Quando a operação de Olá é alterações de estado de conclusão Olá demasiado**com êxito**.

```json
{
  "status": "Succeeded"
}
```

### <a name="retrieve-hello-results"></a>Obter resultados Olá

Depois de estado de Olá devolvidos é **com êxito**, chamar um método obter Olá operationResult URI tooretrieve resultados Olá.

```powershell
armclient get "https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operationResults/8a1167b7-6768-4ac1-85dc-703c9c9b9247?api-version=2016-03-30"
```

Olá respostas seguintes são exemplos de uma resposta degradada típico devolvido quando a consulta de Olá resultados de um gateway de resolução de problemas. Consulte [compreender resultados Olá](#understanding-the-results) tooget esclarecimentos nas propriedades que Olá em média de resposta de Olá.

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


## <a name="troubleshoot-connections"></a>Resolver problemas de ligações

Olá seguir o estado de Olá de consultas de exemplo de uma ligação.

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
> Olá de resolver problemas relacionados com a operação não pode ser executado em paralelo no respetivos gateways correspondentes e de uma ligação. operação Olá tem de concluir toorunning anterior-lo no recurso de Olá anterior.

Uma vez que esta é uma transação de execução longa, no cabeçalho de resposta de Olá, Olá URI para consultar a operação de Olá e Olá URI para o resultado de Olá é devolvido como mostrado na Olá seguinte resposta:

**Valores importantes**

* **Azure AsyncOperation** -esta propriedade contém Olá URI tooquery Olá Async resolver problemas de operação
* **Localização** -esta propriedade contém Olá URI onde Olá os resultados são quando hello operação foi concluída

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

### <a name="query-hello-async-operation-for-completion"></a>Olá async operação para conclusão de consulta

Utilize Olá operações URI tooquery para progresso Olá operação de Olá, como mostrado no seguinte exemplo de Olá:

```powershell
armclient get "https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operations/843b1c31-4717-4fdd-b7a6-4c786ca9c501?api-version=2016-03-30"
```

Enquanto a operação de Olá está em curso, Olá resposta mostra **em curso** como mostrado no seguinte exemplo de Olá:

```json
{
  "status": "InProgress"
}
```

Quando a operação de Olá estiver concluída, o estado de Olá mudar demasiado**com êxito**.

```json
{
  "status": "Succeeded"
}
```

Olá respostas seguintes são exemplos de uma resposta típico devolvido quando a consulta de Olá resultados de uma ligação de resolução de problemas.

### <a name="retrieve-hello-results"></a>Obter resultados Olá

Depois de estado de Olá devolvidos é **com êxito**, chamar um método obter Olá operationResult URI tooretrieve resultados Olá.

```powershell
armclient get "https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operationResults/843b1c31-4717-4fdd-b7a6-4c786ca9c501?api-version=2016-03-30"
```

Olá respostas seguintes são exemplos de uma resposta típico devolvido quando a consulta de Olá resultados de uma ligação de resolução de problemas.

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

## <a name="understanding-hello-results"></a>Compreender os resultados de Olá

o texto de ação de Olá fornece orientações gerais sobre como tooresolve Olá problema. Se uma ação pode ser levada para o problema de Olá, é fornecida uma ligação com orientações adicionais. No caso de Olá em que não existe nenhuma orientação adicional, resposta Olá fornece Olá url tooopen um incidente de suporte.  Para obter mais informações sobre as propriedades de Olá de resposta Olá e que está incluído, visite [descrição geral de resolução de problemas de observador de rede](network-watcher-troubleshoot-overview.md)

Para obter instruções sobre como transferir ficheiros entre contas de armazenamento do azure, consulte demasiado[introdução ao Blob storage do Azure através do .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md). Outra ferramenta que pode ser utilizada é Explorador de armazenamento. Obter mais informações sobre o Explorador de armazenamento podem ser encontradas aqui em Olá seguinte hiperligação: [Explorador de armazenamento](http://storageexplorer.com/)

## <a name="next-steps"></a>Passos seguintes

Se foram alteradas as definições que conectividade VPN de parar, consulte o artigo [gerir grupos de segurança de rede](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack baixo Olá rede segurança e de grupo de regras de segurança que podem ser em questão.
