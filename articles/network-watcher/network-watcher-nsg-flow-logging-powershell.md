---
title: "Gerir registos de fluxo de grupo de segurança de rede com o observador de rede do Azure - PowerShell | Microsoft Docs"
description: "Esta página explica como gerir os registos de fluxo de grupo de segurança de rede no Azure observador de rede com o PowerShell"
services: network-watcher
documentationcenter: na
author: jimdial
manager: timlt
editor: 
ms.assetid: 2dfc3112-8294-4357-b2f8-f81840da67d3
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: jdial
ms.openlocfilehash: 5c514cc3d281d9e2baeae415aed240579af75650
ms.sourcegitcommit: b5c6197f997aa6858f420302d375896360dd7ceb
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/21/2017
---
# <a name="configuring-network-security-group-flow-logs-with-powershell"></a>Configurar os registos de fluxo de grupo de segurança de rede com o PowerShell

> [!div class="op_single_selector"]
> - [Portal do Azure](network-watcher-nsg-flow-logging-portal.md)
> - [PowerShell](network-watcher-nsg-flow-logging-powershell.md)
> - [CLI 1.0](network-watcher-nsg-flow-logging-cli-nodejs.md)
> - [CLI 2.0](network-watcher-nsg-flow-logging-cli.md)
> - [API REST](network-watcher-nsg-flow-logging-rest.md)

Registos de fluxo do grupo de segurança de rede são uma funcionalidade do observador de rede que permite-lhe ver informações sobre o tráfego IP de entrada e de saída através de um grupo de segurança de rede. Estes registos de fluxo são escritos no formato json e Mostrar fluxos de saída e entrados numa base por regra, o NIC o fluxo de mensagens em fila aplica-se a informações de 5 cadeias de identificação sobre o fluxo (origem/destino IP, porta de origem/destino, protocolo), e se o tráfego foi permitido ou negado.

## <a name="register-insights-provider"></a>Fornecedor de informações de registo

Ordem de fluxo de registo para trabalhar com êxito, o **insights** fornecedor tem de estar registado. Se não tiver a certeza se a **insights** fornecedor está registado, execute o seguinte script.

```powershell
Register-AzureRmResourceProvider -ProviderNamespace Microsoft.Insights
```

## <a name="enable-network-security-group-flow-logs"></a>Registos de fluxo de ativar o grupo de segurança de rede

O comando para ativar registos de fluxo é mostrado no exemplo seguinte:

```powershell
$NW = Get-AzurermNetworkWatcher -ResourceGroupName NetworkWatcherRg -Name NetworkWatcher_westcentralus
$nsg = Get-AzureRmNetworkSecurityGroup -ResourceGroupName nsgRG-Name nsgName
$storageAccount = Get-AzureRmStorageAccount -ResourceGroupName StorageRG -Name contosostorage123
Get-AzureRmNetworkWatcherFlowLogStatus -NetworkWatcher $NW -TargetResourceId $nsg.Id
Set-AzureRmNetworkWatcherConfigFlowLog -NetworkWatcher $NW -TargetResourceId $nsg.Id -StorageAccountId $storageAccount.Id -EnableFlowLog $true
```

## <a name="disable-network-security-group-flow-logs"></a>Registos de fluxo de desativar o grupo de segurança de rede

Utilize o exemplo seguinte para desativar os registos de fluxo:

```powershell
Set-AzureRmNetworkWatcherConfigFlowLog -NetworkWatcher $NW -TargetResourceId $nsg.Id -StorageAccountId $storageAccount.Id -EnableFlowLog $false
```

## <a name="download-a-flow-log"></a>Transferir um registo de fluxo

A localização de armazenamento de um registo de fluxo é definida na criação. Uma ferramenta conveniente para aceder a estes registos de fluxo guardados para uma conta de armazenamento é Explorador de armazenamento do Microsoft Azure, que pode ser transferida aqui: http://storageexplorer.com/

Se for especificada uma conta de armazenamento, ficheiros de captura de pacotes são guardados para uma conta de armazenamento disponíveis na seguinte localização:

```
https://{storageAccountName}.blob.core.windows.net/insights-logs-networksecuritygroupflowevent/resourceId=/SUBSCRIPTIONS/{subscriptionID}/RESOURCEGROUPS/{resourceGroupName}/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUPS/{nsgName}/y={year}/m={month}/d={day}/h={hour}/m=00/macAddress={macAddress}/PT1H.json
```

Para obter informações sobre a estrutura do registo visite [descrição geral do fluxo de grupo de segurança de rede registo](network-watcher-nsg-flow-logging-overview.md)

## <a name="next-steps"></a>Próximos Passos

Saiba como [visualizar os registos de fluxo NSG com o PowerBI](network-watcher-visualize-nsg-flow-logs-power-bi.md)

Saiba como [visualizar os registos de fluxo NSG com ferramentas open source](network-watcher-visualize-nsg-flow-logs-open-source-tools.md)