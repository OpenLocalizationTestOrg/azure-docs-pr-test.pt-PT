---
title: aaaAzure amostras CLI | Microsoft Docs
description: Exemplos da CLI do Azure
services: virtual-network
documentationcenter: virtual-network
author: KumudD
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: 
ms.workload: infrastructure
ms.date: 04/25/2017
ms.author: kumud
ms.openlocfilehash: 8001b7e72480cfd0122325f7fb81c32aaad072d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cli-samples-for-networking"></a>Exemplos da CLI do Azure para funcionamento em rede

Olá tabela que se segue inclui ligações toobash scripts compiladas com Olá CLI do Azure.

| | |
|-|-|
|**Conectividade entre os recursos do Azure**||
| [Criar uma rede virtual para aplicações de várias camadas](./scripts/virtual-network-cli-sample-multi-tier-application.md?toc=%2fazure%2fnetworking%2ftoc.json) | Cria uma rede virtual com as sub-redes de front-end e back-end. Sub-rede de front-end do tráfego toohello tooHTTP limitado e SSH, ao tráfego toohello sub-rede de back-end é limitado tooMySQL, porta 3306. |
| [Elemento duas redes virtuais](./scripts/virtual-network-cli-sample-peer-two-virtual-networks.md?toc=%2fazure%2fnetworking%2ftoc.json) | Cria e ligar duas redes virtuais na Olá mesma região. |
| [Encaminhar o tráfego através de uma aplicação virtual de rede](./scripts/virtual-network-cli-sample-route-traffic-through-nva.md?toc=%2fazure%2fnetworking%2ftoc.json) | Cria uma rede virtual com uma VM que é capaz de tooroute tráfego entre sub-redes Olá dois e as sub-redes de front-end e back-end. |
| [Filtrar o tráfego de rede VM de entrada e saído](./scripts/virtual-network-filter-network-traffic.md?toc=%2fazure%2fnetworking%2ftoc.json) | Cria uma rede virtual com as sub-redes de front-end e back-end. Tráfego de rede de entrada toohello sub-rede front-end é limitado tooHTTP, HTTPS e SSH. Tráfego de saída toohello Internet da sub-rede de back-end Olá não é permitida. |
|**Direção do tráfego e balanceamento de carga**||
| [Carregar saldo tráfego tooVMs para elevada disponibilidade](./scripts/load-balancer-linux-cli-sample-nlb.md?toc=%2fazure%2fnetworking%2ftoc.json) | Cria várias máquinas virtuais da elevada disponibilidade e a configuração de balanceamento de carga. |
| [Balanceamento de carga de vários sites em VMs](./scripts/load-balancer-linux-cli-load-balance-multiple-websites-vm.md?toc=%2fazure%2fnetworking%2ftoc.json) | Cria duas VMs com várias configurações de IP, tooan associados a um Azure do conjunto de disponibilidade, acessível através de um balanceador de carga do Azure. |
| [Direto tráfego em várias regiões para disponibilidade elevada de aplicação](./scripts/traffic-manager-cli-websites-high-availability.md?toc=%2fazure%2fnetworking%2ftoc.json) |  Cria duas planos de serviço de aplicações, duas aplicações web, um perfil do Gestor de tráfego e dois pontos finais Gestor de tráfego. |
| | |
