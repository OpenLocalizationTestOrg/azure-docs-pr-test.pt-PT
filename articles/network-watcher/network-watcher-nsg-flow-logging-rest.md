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
# <a name="configuring-network-security-group-flow-logs-using-rest-api"></a>Registos de fluxo de configurar o grupo de segurança de rede através da API de REST

> [!div class="op_single_selector"]
> - [Portal do Azure](network-watcher-nsg-flow-logging-portal.md)
> - [PowerShell](network-watcher-nsg-flow-logging-powershell.md)
> - [CLI 1.0](network-watcher-nsg-flow-logging-cli-nodejs.md)
> - [CLI 2.0](network-watcher-nsg-flow-logging-cli.md)
> - [API REST](network-watcher-nsg-flow-logging-rest.md)

Registos de fluxo do grupo de segurança de rede são uma funcionalidade do observador de rede que permite-lhe tooview informações sobre o tráfego IP de entrada e de saída através de um grupo de segurança de rede. Estes registos de fluxo são escritos no formato json e mostram a saída e entrados fluxos numa base por regra, Olá fluxo de Olá NIC se aplica, informações de 5 cadeias de identificação sobre o fluxo de Olá (origem/destino IP, porta de origem/destino, protocolo) e se hello tráfego foi permitido ou negado.

## <a name="before-you-begin"></a>Antes de começar

ARMclient é a API de REST de Olá toocall utilizado com o PowerShell. ARMClient for encontrado no chocolatey em [ARMClient no Chocolatey](https://chocolatey.org/packages/ARMClient)

Este cenário pressupõe que já tiver seguido os passos de Olá no [criar um observador de rede](network-watcher-create.md) toocreate um observador de rede.

> [!Important]
> Para a API de REST de observador de rede chamadas Olá nome do grupo de recursos no pedido de Olá que URI é o grupo de recursos de Olá contém Olá observador de rede, não os recursos de Olá estiver a efetuar ações de diagnóstico Olá do.

## <a name="scenario"></a>Cenário

cenário de Olá abordado neste artigo mostra-lhe como tooenable, desativar e consulta o fluxo de registos com Olá REST API. toolearn mais informações sobre loggings de fluxo do grupo de segurança de rede, visite [registo de fluxo do grupo de segurança de rede - descrição geral](network-watcher-nsg-flow-logging-overview.md).

Neste cenário, irá:

* Ativar registos de fluxo
* Desativar os registos de fluxo
* Estado de registos de fluxo de consulta

## <a name="log-in-with-armclient"></a>Iniciar sessão com ARMClient

Inicie sessão no tooarmclient com as suas credenciais do Azure.

```PowerShell
armclient login
```

## <a name="register-insights-provider"></a>Fornecedor de informações de registo

Ordem de fluxo de registo toowork com êxito, Olá **insights** fornecedor tem de estar registado. Se não tem a certeza se hello **insights** fornecedor está registado, hello execute seguinte script.

```powershell
$subscriptionId = "00000000-0000-0000-0000-000000000000"
armclient post "https://management.azure.com//subscriptions/${subscriptionId}/providers/Microsoft.Insights/register?api-version=2016-09-01"
```

## <a name="enable-network-security-group-flow-logs"></a>Registos de fluxo de ativar o grupo de segurança de rede

Olá comando tooenable fluxo registos é mostrado no seguinte exemplo de Olá:

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

resposta Olá devolvido de Olá anterior exemplo é o seguinte:

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

## <a name="disable-network-security-group-flow-logs"></a>Registos de fluxo de desativar o grupo de segurança de rede

Os seguintes registos de fluxo de toodisable de exemplo Olá de utilização. Olá chamada é Olá mesmo que ativar registos de fluxo, exceto **falso** está definido para a propriedade Olá ativada.

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

resposta Olá devolvido de Olá anterior exemplo é o seguinte:

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

## <a name="query-flow-logs"></a>Registos de fluxo de consulta

Olá chamada REST de consultas de estado do fluxo de Olá os seguintes os registos de um grupo de segurança de rede.

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

Olá segue-se um exemplo de Olá resposta devolvida:

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

## <a name="download-a-flow-log"></a>Transferir um registo de fluxo

localização de armazenamento Olá de um registo de fluxo é definida na criação. Um tooaccess ferramenta conveniente destas contas de armazenamento do fluxo registos guardados tooa é Explorador de armazenamento do Microsoft Azure, que pode ser transferida aqui: http://storageexplorer.com/

Se for especificada uma conta de armazenamento, ficheiros de captura de pacotes são guardados tooa a conta de armazenamento em Olá seguinte localização:

```
https://{storageAccountName}.blob.core.windows.net/insights-logs-networksecuritygroupflowevent/resourceId%3D/subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/microsoft.network/networksecuritygroups/{nsgName}/{year}/{month}/{day}/PT1H.json
```

## <a name="next-steps"></a>Passos seguintes

Saiba como demasiado[visualizar os registos de fluxo NSG com o PowerBI](network-watcher-visualize-nsg-flow-logs-power-bi.md)

Saiba como demasiado[visualizar os registos de fluxo NSG com ferramentas open source](network-watcher-visualize-nsg-flow-logs-open-source-tools.md)
