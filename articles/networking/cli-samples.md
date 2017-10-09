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
# <a name="azure-cli-samples-for-networking"></a><span data-ttu-id="6bfd2-103">Exemplos da CLI do Azure para funcionamento em rede</span><span class="sxs-lookup"><span data-stu-id="6bfd2-103">Azure CLI Samples for networking</span></span>

<span data-ttu-id="6bfd2-104">Olá tabela que se segue inclui ligações toobash scripts compiladas com Olá CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="6bfd2-104">hello following table includes links toobash scripts built using hello Azure CLI.</span></span>

| | |
|-|-|
|<span data-ttu-id="6bfd2-105">**Conectividade entre os recursos do Azure**</span><span class="sxs-lookup"><span data-stu-id="6bfd2-105">**Connectivity between Azure resources**</span></span>||
| [<span data-ttu-id="6bfd2-106">Criar uma rede virtual para aplicações de várias camadas</span><span class="sxs-lookup"><span data-stu-id="6bfd2-106">Create a virtual network for multi-tier applications</span></span>](./scripts/virtual-network-cli-sample-multi-tier-application.md?toc=%2fazure%2fnetworking%2ftoc.json) | <span data-ttu-id="6bfd2-107">Cria uma rede virtual com as sub-redes de front-end e back-end.</span><span class="sxs-lookup"><span data-stu-id="6bfd2-107">Creates a virtual network with front-end and back-end subnets.</span></span> <span data-ttu-id="6bfd2-108">Sub-rede de front-end do tráfego toohello tooHTTP limitado e SSH, ao tráfego toohello sub-rede de back-end é limitado tooMySQL, porta 3306.</span><span class="sxs-lookup"><span data-stu-id="6bfd2-108">Traffic toohello front-end subnet is limited tooHTTP and SSH, while traffic toohello back-end subnet is limited tooMySQL, port 3306.</span></span> |
| [<span data-ttu-id="6bfd2-109">Elemento duas redes virtuais</span><span class="sxs-lookup"><span data-stu-id="6bfd2-109">Peer two virtual networks</span></span>](./scripts/virtual-network-cli-sample-peer-two-virtual-networks.md?toc=%2fazure%2fnetworking%2ftoc.json) | <span data-ttu-id="6bfd2-110">Cria e ligar duas redes virtuais na Olá mesma região.</span><span class="sxs-lookup"><span data-stu-id="6bfd2-110">Creates and connects two virtual networks in hello same region.</span></span> |
| [<span data-ttu-id="6bfd2-111">Encaminhar o tráfego através de uma aplicação virtual de rede</span><span class="sxs-lookup"><span data-stu-id="6bfd2-111">Route traffic through a network virtual appliance</span></span>](./scripts/virtual-network-cli-sample-route-traffic-through-nva.md?toc=%2fazure%2fnetworking%2ftoc.json) | <span data-ttu-id="6bfd2-112">Cria uma rede virtual com uma VM que é capaz de tooroute tráfego entre sub-redes Olá dois e as sub-redes de front-end e back-end.</span><span class="sxs-lookup"><span data-stu-id="6bfd2-112">Creates a virtual network with front-end and back-end subnets and a VM that is able tooroute traffic between hello two subnets.</span></span> |
| [<span data-ttu-id="6bfd2-113">Filtrar o tráfego de rede VM de entrada e saído</span><span class="sxs-lookup"><span data-stu-id="6bfd2-113">Filter inbound and outbound VM network traffic</span></span>](./scripts/virtual-network-filter-network-traffic.md?toc=%2fazure%2fnetworking%2ftoc.json) | <span data-ttu-id="6bfd2-114">Cria uma rede virtual com as sub-redes de front-end e back-end.</span><span class="sxs-lookup"><span data-stu-id="6bfd2-114">Creates a virtual network with front-end and back-end subnets.</span></span> <span data-ttu-id="6bfd2-115">Tráfego de rede de entrada toohello sub-rede front-end é limitado tooHTTP, HTTPS e SSH.</span><span class="sxs-lookup"><span data-stu-id="6bfd2-115">Inbound network traffic toohello front-end subnet is limited tooHTTP, HTTPS and SSH.</span></span> <span data-ttu-id="6bfd2-116">Tráfego de saída toohello Internet da sub-rede de back-end Olá não é permitida.</span><span class="sxs-lookup"><span data-stu-id="6bfd2-116">Outbound traffic toohello Internet from hello back-end subnet is not permitted.</span></span> |
|<span data-ttu-id="6bfd2-117">**Direção do tráfego e balanceamento de carga**</span><span class="sxs-lookup"><span data-stu-id="6bfd2-117">**Load balancing and traffic direction**</span></span>||
| [<span data-ttu-id="6bfd2-118">Carregar saldo tráfego tooVMs para elevada disponibilidade</span><span class="sxs-lookup"><span data-stu-id="6bfd2-118">Load balance traffic tooVMs for high availability</span></span>](./scripts/load-balancer-linux-cli-sample-nlb.md?toc=%2fazure%2fnetworking%2ftoc.json) | <span data-ttu-id="6bfd2-119">Cria várias máquinas virtuais da elevada disponibilidade e a configuração de balanceamento de carga.</span><span class="sxs-lookup"><span data-stu-id="6bfd2-119">Creates several virtual machines in a highly available and load balanced configuration.</span></span> |
| [<span data-ttu-id="6bfd2-120">Balanceamento de carga de vários sites em VMs</span><span class="sxs-lookup"><span data-stu-id="6bfd2-120">Load balance multiple websites on VMs</span></span>](./scripts/load-balancer-linux-cli-load-balance-multiple-websites-vm.md?toc=%2fazure%2fnetworking%2ftoc.json) | <span data-ttu-id="6bfd2-121">Cria duas VMs com várias configurações de IP, tooan associados a um Azure do conjunto de disponibilidade, acessível através de um balanceador de carga do Azure.</span><span class="sxs-lookup"><span data-stu-id="6bfd2-121">Creates two VMs with multiple IP configurations, joined tooan Azure Availability Set, accessible through an Azure Load Balancer.</span></span> |
| [<span data-ttu-id="6bfd2-122">Direto tráfego em várias regiões para disponibilidade elevada de aplicação</span><span class="sxs-lookup"><span data-stu-id="6bfd2-122">Direct traffic across multiple regions for high application availability</span></span>](./scripts/traffic-manager-cli-websites-high-availability.md?toc=%2fazure%2fnetworking%2ftoc.json) |  <span data-ttu-id="6bfd2-123">Cria duas planos de serviço de aplicações, duas aplicações web, um perfil do Gestor de tráfego e dois pontos finais Gestor de tráfego.</span><span class="sxs-lookup"><span data-stu-id="6bfd2-123">Creates two app service plans, two web apps, a traffic manager profile, and two traffic manager endpoints.</span></span> |
| | |
