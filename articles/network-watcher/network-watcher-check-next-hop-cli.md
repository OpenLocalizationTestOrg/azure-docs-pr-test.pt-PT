---
title: "Localizar o salto seguinte com o Azure rede observador do próximo salto - Azure CLI 2.0 | Microsoft Docs"
description: "Este artigo descreve como pode encontrar o que é o tipo de salto seguinte e o endereço ip utilizando o salto seguinte ao utilizar a CLI do Azure."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: jimdial
editor: 
ms.assetid: 0700c274-3e0d-4dca-acfa-3ceac8990613
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: jdial
ms.openlocfilehash: fb4a24fd758ad4b7231364f3ee7d56a9a2dbccb1
ms.sourcegitcommit: b5c6197f997aa6858f420302d375896360dd7ceb
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/21/2017
---
# <a name="find-out-what-the-next-hop-type-is-using-the-next-hop-capability-in-azure-network-watcher-using-azure-cli-20"></a>Saber que o tipo de próximo salto está a utilizar a capacidade de próximo salto na observador de rede do Azure a utilizar o Azure CLI 2.0

> [!div class="op_single_selector"]
> - [Portal do Azure](network-watcher-check-next-hop-portal.md)
> - [PowerShell](network-watcher-check-next-hop-powershell.md)
> - [CLI 1.0](network-watcher-check-next-hop-cli-nodejs.md)
> - [CLI 2.0](network-watcher-check-next-hop-cli.md)
> - [API REST do Azure](network-watcher-check-next-hop-rest.md)

Próximo salto é uma funcionalidade do observador de rede que fornece a capacidade de obter o tipo de salto seguinte e o endereço IP com base numa máquina virtual especificada. Esta funcionalidade é útil para determinar se o tráfego que sai de uma máquina virtual atravessa um gateway, internet ou redes virtuais para aceder ao respetivo destino.

Este artigo utiliza o nosso CLI de próxima geração para o modelo de implementação de gestão de recursos, Azure CLI 2.0, que está disponível para o Windows, Mac e Linux.

Para efetuar os passos neste artigo, terá de [instalar a Interface de linha de comandos do Azure para Mac, Linux e Windows (CLI do Azure)](https://docs.microsoft.com/cli/azure/install-az-cli2).

## <a name="before-you-begin"></a>Antes de começar

Neste cenário, irá utilizar a CLI do Azure para localizar o tipo de salto seguinte e o endereço IP.

Este cenário pressupõe que já tiver seguido os passos em [criar um observador de rede](network-watcher-create.md) para criar um observador de rede. O cenário também parte do princípio de que existe um grupo de recursos com uma máquina virtual válida para ser utilizado.

## <a name="scenario"></a>Cenário

O cenário abordado neste artigo utiliza o salto seguinte, uma funcionalidade do observador de rede que localiza o tipo de salto seguinte e o endereço IP para um recurso. Para mais informações sobre o próximo salto, visite [descrição geral de salto seguinte](network-watcher-next-hop-overview.md).


## <a name="get-next-hop"></a>Obter o salto seguinte

Para obter o salto seguinte chamamos a `az network watcher show-next-hop` cmdlet. O cmdlet podemos transmitir o grupo de recursos do observador de rede, NetworkWatcher, a máquina virtual Id, endereço IP de origem e endereço IP de destino. Neste exemplo, endereço IP de destino é uma VM na outra rede virtual. Não há um gateway de rede virtual entre as duas redes virtuais.

Se ainda não ainda, instalar e configurar a versão mais recente [Azure CLI 2.0](/cli/azure/install-az-cli2) e início de sessão para um Azure conta através de [início de sessão az](/cli/azure/#login). Em seguida, execute o seguinte comando:

```azurecli
az network watcher show-next-hop --resource-group <resourcegroupName> --vm <vmNameorID> --source-ip <source-ip> --dest-ip <destination-ip>

```

> [!NOTE]
Se a VM possui vários NICs e reencaminhamento IP está ativado em nenhum dos NICs, em seguida, o parâmetro NIC (-i nic id) tem de ser especificado. Caso contrário, é opcional.

## <a name="review-results"></a>Resultados da revisão

Quando terminar, os resultados são fornecidos. O endereço IP do próximo salto é devolvido, bem como o tipo de recurso é.

```azurecli
{
    "nextHopIpAddress": null,
    "nextHopType": "Internet",
    "routeTableId": "System Route"
}
```

A lista seguinte mostra os valores de NextHopType atualmente disponíveis:

**Tipo de próximo salto**

* Internet
* VirtualAppliance
* VirtualNetworkGateway
* VnetLocal
* HyperNetGateway
* VnetPeering
* Nenhuma

## <a name="next-steps"></a>Passos Seguintes

Saiba como rever as definições de grupo de segurança de rede através de programação, visitando [NSG auditoria com observador de rede](network-watcher-nsg-auditing-powershell.md)
