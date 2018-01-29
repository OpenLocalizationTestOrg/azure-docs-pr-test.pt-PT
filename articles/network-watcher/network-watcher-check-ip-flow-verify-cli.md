---
title: "Certifique-se de tráfego com o Azure rede observador IP fluxo verifique - CLI do Azure | Microsoft Docs"
description: "Este artigo descreve como verificar se o tráfego de ou para uma máquina virtual é permitido ou negado utilizando a CLI do Azure"
services: network-watcher
documentationcenter: na
author: jimdial
manager: timlt
editor: 
ms.assetid: 92b857ed-c834-4c1b-8ee9-538e7ae7391d
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: jdial
ms.openlocfilehash: 3f4a7d3f96a08b3296dd1abfec8abfbcb9759e9f
ms.sourcegitcommit: b5c6197f997aa6858f420302d375896360dd7ceb
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/21/2017
---
# <a name="check-if-traffic-is-allowed-or-denied-to-or-from-a-vm-with-ip-flow-verify-a-component-of-azure-network-watcher"></a>Verifique se o tráfego é permitido ou negado de uma VM com o IP fluxo verificar ou para um componente do observador de rede do Azure

> [!div class="op_single_selector"]
> - [Portal do Azure](network-watcher-check-ip-flow-verify-portal.md)
> - [PowerShell](network-watcher-check-ip-flow-verify-powershell.md)
> - [CLI 1.0](network-watcher-check-ip-flow-verify-cli-nodejs.md)
> - [CLI 2.0](network-watcher-check-ip-flow-verify-cli.md)
> - [API REST do Azure](network-watcher-check-ip-flow-verify-rest.md)


Fluxo de IP verificar é uma funcionalidade do observador de rede que permite-lhe verificar se o tráfego é permitido para ou a partir de uma máquina virtual. Este cenário é útil para obter um estado atual do se uma máquina virtual pode comunicar com um recurso externo ou o back-end. Verificar o fluxo IP podem ser utilizadas para verificar se as regras do grupo de segurança de rede (NSG) estão configuradas corretamente e resolver problemas relacionados com fluxos que estão a ser bloqueados por regras NSG. Outra razão para utilizar o IP fluxo verificar é certificar-se de que o tráfego que pretende que sejam bloqueadas está a ser bloqueado corretamente por NSG.

Este artigo utiliza o nosso CLI de próxima geração para o modelo de implementação de gestão de recursos, Azure CLI 2.0, que está disponível para o Windows, Mac e Linux.

Para efetuar os passos neste artigo, terá de [instalar a Interface de linha de comandos do Azure para Mac, Linux e Windows (CLI do Azure)](https://docs.microsoft.com/cli/azure/install-az-cli2).

## <a name="before-you-begin"></a>Antes de começar

Este cenário pressupõe que já tiver seguido os passos em [criar um observador de rede](network-watcher-create.md) para criar um observador de rede ou ter uma instância existente do observador de rede. O cenário também parte do princípio de que existe um grupo de recursos com uma máquina virtual válida para ser utilizado.

## <a name="scenario"></a>Cenário

Este cenário utiliza fluxo Certifique-se de IP para verificar se uma máquina virtual pode comunicar com um endereço IP do Bing conhecido. Se o tráfego for recusado, devolve a regra de segurança que está a negar esse tráfego. Para mais informações sobre o fluxo Certifique-se de IP, visite [IP fluxo Certifique-se de descrição geral](network-watcher-ip-flow-verify-overview.md)

## <a name="get-a-vm"></a>Obter uma VM

Fluxo IP Certifique-se o tráfego de testes para ou de um endereço IP numa máquina virtual para ou a partir de um destino remoto. Um Id de uma máquina virtual é necessário para o cmdlet. Se já souber o ID da máquina virtual a utilizar, pode ignorar este passo.

```azurecli
az vm show --resource-group MyResourceGroup5431 --name MyVM-Web
```

## <a name="get-the-nics"></a>Obter os NICS

O endereço IP de uma NIC na máquina virtual é necessário, neste exemplo, obtemos os NICs numa máquina virtual. Se já conhece o endereço IP que pretende testar na máquina virtual, pode ignorar este passo.

```azurecli
az network nic show --resource-group MyResourceGroup5431 --name MyNic-Web
```

## <a name="run-ip-flow-verify"></a>Certifique-se de execução de fluxo de IP

Agora que temos as informações necessárias para executar o cmdlet, iremos executar o `az network watcher test-ip-flow` cmdlet para testar o tráfego. Neste exemplo, estamos a utilizar o primeiro endereço IP no NIC primeiro.

```azurecli
az network watcher test-ip-flow --resource-group resourceGroupName --direction directionInboundorOutbound --protocol protocolTCPorUDP --local ipAddressandPort --remote ipAddressandPort --vm vmNameorID --nic nicNameorID
```

> [!NOTE]
> Fluxo de IP verificar requer que o recurso VM está alocado para executar.

## <a name="review-results"></a>Reveja os resultados

Após a execução `az network watcher test-ip-flow` os resultados são devolvidos, o exemplo seguinte é os resultados devolvidos a partir do passo anterior.

```azurecli
{
    "access": "Allow",
    "ruleName": "defaultSecurityRules/AllowInternetOutBound"
}
```

## <a name="next-steps"></a>Passos Seguintes

Se o tráfego está a ser bloqueado e não deve ser, consulte [gerir grupos de segurança de rede](../virtual-network/virtual-network-manage-nsg-arm-portal.md) para identificar as regras de segurança e de grupo de segurança de rede que estão definidas.

Saiba como as definições de NSG de auditoria, visitando [auditoria de segurança de rede grupos (NSG) com o observador de rede](network-watcher-nsg-auditing-powershell.md).

[1]: ./media/network-watcher-check-ip-flow-verify-portal/figure1.png
[2]: ./media/network-watcher-check-ip-flow-verify-portal/figure2.png
