---
title: "tráfego de aaaVerify com Azure rede observador IP fluxo verifique - CLI do Azure | Microsoft Docs"
description: "Este artigo descreve como toocheck se tooor de tráfego de uma máquina virtual for permitido ou negado utilizando a CLI do Azure"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 92b857ed-c834-4c1b-8ee9-538e7ae7391d
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 128a00b4296994551e7e17838a51e6d9de180e21
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="check-if-traffic-is-allowed-or-denied-tooor-from-a-vm-with-ip-flow-verify-a-component-of-azure-network-watcher"></a>Verifique se o tráfego é permitido ou negado tooor de uma VM com o IP fluxo Certifique-se um componente do observador de rede do Azure

> [!div class="op_single_selector"]
> - [Portal do Azure](network-watcher-check-ip-flow-verify-portal.md)
> - [PowerShell](network-watcher-check-ip-flow-verify-powershell.md)
> - [CLI 1.0](network-watcher-check-ip-flow-verify-cli-nodejs.md)
> - [CLI 2.0](network-watcher-check-ip-flow-verify-cli.md)
> - [API REST do Azure](network-watcher-check-ip-flow-verify-rest.md)


Fluxo de IP verificar é uma funcionalidade do observador de rede que permite-lhe tooverify se o tráfego é permitido tooor de uma máquina virtual. Este cenário é útil tooget um estado atual da se uma máquina virtual pode comunicar com um recurso externo tooan ou back-end. Fluxo IP verificar tooverify utilizada se as regras do grupo de segurança de rede (NSG) estão configuradas corretamente e resolver problemas relacionados com fluxos que estão a ser bloqueados por regras NSG. Outra razão para utilizar o IP fluxo verifique tráfego tooensure que pretende bloqueadas que está a ser bloqueado corretamente por Olá NSG.

Este artigo utiliza a nossa próxima geração CLI do modelo de implementação da gestão de recursos de Olá, Azure CLI 2.0, que está disponível para o Windows, Mac e Linux.

Olá tooperform os passos neste artigo, terá de demasiado[instalar Olá Interface de linha de comandos do Azure para Mac, Linux e Windows (CLI do Azure)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).

## <a name="before-you-begin"></a>Antes de começar

Este cenário pressupõe que já tiver seguido os passos de Olá no [criar um observador de rede](network-watcher-create.md) toocreate um observador de rede ou ter uma instância existente do observador de rede. cenário de Olá também parte do princípio de que um grupo de recursos com uma máquina virtual válida existe toobe utilizado.

## <a name="scenario"></a>Cenário

Este cenário utiliza tooverify IP fluxo verificar se uma máquina virtual pode falar tooa conhecidos endereço IP do Bing. Se for negado o tráfego de Olá, devolve regra de segurança de Olá que está a negar esse tráfego. toolearn mais informações sobre o fluxo verificar IP, visite [IP fluxo Certifique-se de descrição geral](network-watcher-ip-flow-verify-overview.md)

## <a name="get-a-vm"></a>Obter uma VM

Fluxo IP verifique tooor de tráfego de testes de um endereço IP no tooor máquina virtual de um destino remoto. Um Id de uma máquina virtual é necessário para Olá cmdlet. Se já souber o ID Olá Olá toouse de máquina virtual, pode ignorar este passo.

```azurecli
az vm show --resource-group MyResourceGroup5431 --name MyVM-Web
```

## <a name="get-hello-nics"></a>Obter Olá NICS

endereço IP Olá de uma NIC na máquina virtual de Olá for necessária, neste exemplo, obtemos Olá NICs numa máquina virtual. Se já conhece o IP de Olá endereço que pretende tootest numa máquina virtual de Olá, pode ignorar este passo.

```azurecli
az network nic show --resource-group MyResourceGroup5431 --name MyNic-Web
```

## <a name="run-ip-flow-verify"></a>Certifique-se de execução de fluxo de IP

Agora que temos informações Olá necessário toorun Olá cmdlet, iremos executar Olá `az network watcher test-ip-flow` tráfego do cmdlet tootest Olá. Neste exemplo, estamos a utilizar endereço IP primeiro Olá numa NIC primeiro Olá em

```azurecli
az network watcher test-ip-flow --resource-group resourceGroupName --direction directionInboundorOutbound --protocol protocolTCPorUDP --local ipAddressandPort --remote ipAddressandPort --vm vmNameorID --nic nicNameorID
```

> [!NOTE]
> Fluxo de IP verificar requer que o recurso VM Olá está alocado toorun.

## <a name="review-results"></a>Reveja os resultados

Após a execução `az network watcher test-ip-flow` Olá resultados são devolvidos, hello exemplo seguinte é resultados Olá devolvidos de Olá precedente passo.

```azurecli
{
    "access": "Allow",
    "ruleName": "defaultSecurityRules/AllowInternetOutBound"
}
```

## <a name="next-steps"></a>Passos seguintes

Se o tráfego está a ser bloqueado e não deve ser, consulte [gerir grupos de segurança de rede](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack baixo Olá rede segurança e de grupo de regras de segurança que estão definidos.

Saiba tooaudit as definições de NSG, visitando [auditoria de segurança de rede grupos (NSG) com o observador de rede](network-watcher-nsg-auditing-powershell.md).

[1]: ./media/network-watcher-check-ip-flow-verify-portal/figure1.png
[2]: ./media/network-watcher-check-ip-flow-verify-portal/figure2.png
