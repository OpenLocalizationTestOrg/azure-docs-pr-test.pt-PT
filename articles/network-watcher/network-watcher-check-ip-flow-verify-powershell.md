---
title: "verificar o tráfego de aaaverify com o fluxo de IP de observador de rede do Azure - PowerShell | Microsoft Docs"
description: "Este artigo descreve como toocheck se tooor de tráfego de uma máquina virtual for permitido ou negado utilizando o PowerShell"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: e1dad757-8c5d-467f-812e-7cc751143207
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 924da1de1bd554e15816886f8e51d7f170f0e7ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="check-if-traffic-is-allowed-or-denied-tooor-from-a-vm-with-ip-flow-verify-a-component-of-azure-network-watcher"></a>Verifique se o tráfego é permitido ou negado tooor de uma VM com o fluxo IP Certifique-se de um componente do observador de rede do Azure

> [!div class="op_single_selector"]
> - [Portal do Azure](network-watcher-check-ip-flow-verify-portal.md)
> - [PowerShell](network-watcher-check-ip-flow-verify-powershell.md)
> - [CLI 1.0](network-watcher-check-ip-flow-verify-cli-nodejs.md)
> - [CLI 2.0](network-watcher-check-ip-flow-verify-cli.md)
> - [API REST do Azure](network-watcher-check-ip-flow-verify-rest.md)


Verificar o fluxo IP é uma funcionalidade do observador de rede que permite-lhe tooverify se o tráfego é permitido tooor de uma máquina virtual. Este cenário é útil tooget um estado atual da se uma máquina virtual pode comunicar com um recurso externo tooan ou back-end. Fluxo IP verificar tooverify utilizada se as regras do grupo de segurança de rede (NSG) estão configuradas corretamente e resolver problemas relacionados com fluxos que estão a ser bloqueados por regras NSG. Outra razão para utilizar o IP fluxo verifique tráfego tooensure que pretende bloqueadas que está a ser bloqueado corretamente por Olá NSG.

## <a name="before-you-begin"></a>Antes de começar

Este cenário pressupõe que já tiver seguido os passos de Olá no [criar um observador de rede](network-watcher-create.md) toocreate um observador de rede ou ter uma instância existente do observador de rede. cenário de Olá também parte do princípio de que um grupo de recursos com uma máquina virtual válida existe toobe utilizado.

## <a name="scenario"></a>Cenário

Este fluxo IP do cenário utiliza verificar tooverify se uma máquina virtual pode falar tooa conhecidos endereço IP do Bing. Se for negado o tráfego de Olá, devolve regra de segurança de Olá que está a negar esse tráfego. mais informações sobre o fluxo IP verificar, visite toolearn [fluxo IP verificar descrição geral](network-watcher-ip-flow-verify-overview.md)

## <a name="retrieve-network-watcher"></a>Obter o observador de rede

Step-by-Olá primeiro passo é a instância do tooretrieve Olá observador de rede. Olá `$networkWatcher` variável ser passada toohello IP fluxo verificar cmdlet.

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" } 
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName 
```

## <a name="get-a-vm"></a>Obter uma VM

Fluxo IP verifique tooor de tráfego de testes de um endereço IP no tooor máquina virtual de um destino remoto. Um Id de uma máquina virtual é necessário para Olá cmdlet. Se já souber o ID Olá Olá toouse de máquina virtual, pode ignorar este passo.

```powershell
$VM = Get-AzurermVM -ResourceGroupName "testrg" -Name "testvm1"
```

## <a name="get-hello-nics"></a>Obter Olá NICS

endereço IP Olá de uma NIC na máquina virtual de Olá for necessária, neste exemplo, obtemos Olá NICs numa máquina virtual. Se já conhece o IP de Olá endereço que pretende tootest numa máquina virtual de Olá, pode ignorar este passo.

```powershell
$Nics = Get-AzureRmNetworkInterface | Where {$_.Id -eq $vm.NetworkProfile.NetworkInterfaces.Id.ForEach({$_})}
```

## <a name="run-ip-flow-verify"></a>Certifique-se de execução de fluxo de IP

Agora que temos informações Olá necessário toorun Olá cmdlet, iremos executar Olá `Test-AzureRmNetworkWatcherIPFlow` tráfego do cmdlet tootest Olá. Neste exemplo, estamos a utilizar endereço IP primeiro Olá numa NIC primeiro Olá em

```powershell
Test-AzureRmNetworkWatcherIPFlow -NetworkWatcher $networkWatcher -TargetVirtualMachineId $VM.Id `
-Direction Outbound -Protocol TCP `
-LocalIPAddress $nics[0].IpConfigurations[0].PrivateIpAddress -LocalPort 6895 -RemoteIPAddress 204.79.197.200 -RemotePort 80
```

> [!NOTE]
> Fluxo IP verificar requer que o recurso VM Olá está alocado toorun.

## <a name="review-results"></a>Reveja os resultados

Após a execução `Test-AzureRmNetworkWatcherIPFlow` Olá resultados são devolvidos, hello exemplo seguinte é resultados Olá devolvidos de Olá precedente passo.

```
Access RuleName                                  
------ --------                                  
Allow  defaultSecurityRules/AllowInternetOutBound
```

## <a name="next-steps"></a>Passos seguintes

Se o tráfego está a ser bloqueado e não deve ser, consulte [gerir grupos de segurança de rede](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack baixo Olá rede segurança e de grupo de regras de segurança que estão definidos.

[1]: ./media/network-watcher-check-ip-flow-verify-portal/figure1.png
[2]: ./media/network-watcher-check-ip-flow-verify-portal/figure2.png













