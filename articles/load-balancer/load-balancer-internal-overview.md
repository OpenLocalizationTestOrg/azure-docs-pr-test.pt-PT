---
title: "Balanceador de carga aaaInternal descrição geral | Microsoft Docs"
description: "Descrição geral para o Balanceador de carga interno e as respetivas funcionalidades. Como funciona a um balanceador de carga para pontos finais internos do Azure e possíveis cenários tooconfigure"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: tysonn
ms.assetid: 36065bfe-0ef1-46f9-a9e1-80b229105c85
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/24/2016
ms.author: kumud
ms.openlocfilehash: 9a901aad224d8821c154e130e142699d57282b25
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="internal-load-balancer-overview"></a>Descrição geral do Balanceador de carga interno

Ao contrário Olá Internet destinado ao balanceador de carga, o Balanceador de carga interno (ILB) do Olá direciona tráfego tooresources apenas dentro de serviço de nuvem Olá ou através de VPN tooaccess Olá infraestrutura do Azure. infraestrutura de Olá restringe o acesso toohello com balanceamento de carga endereços IP virtual (VIP) de um serviço em nuvem ou de uma rede Virtual para que nunca serão tooan diretamente expostos Internet endpoint. Isto permite interna de linha de negócio (LOB) toorun de aplicações no Azure e acedido a partir da nuvem Olá ou recursos no local.

## <a name="why-you-may-need-an-internal-load-balancer"></a>Por que razão poderá ser necessário um balanceador de carga interno

Azure interno carregar balanceamento (ILB) fornece balanceamento da carga entre máquinas virtuais que residem no interior de um serviço em nuvem ou de uma rede virtual com um âmbito regional. Para obter informações sobre a utilização de Olá e a configuração de redes virtuais com um âmbito regional, consulte [redes virtuais regionais](https://azure.microsoft.com/blog/2014/05/14/regional-virtual-networks/) no Olá blogue do Azure. As redes virtuais existentes que foram configuradas para um grupo de afinidades não podem utilizar o ILB.

ILB permite Olá os seguintes tipos de balanceamento de carga:

* Dentro de um serviço de nuvem de máquinas virtuais tooa conjunto de máquinas virtuais que residem no Olá mesmo serviço em nuvem (consulte a figura 1).
* Dentro de uma rede virtual, a partir de máquinas virtuais no conjunto de tooa de rede virtuais Olá de máquinas virtuais que residem no Olá mesmo serviço em nuvem de Olá virtual de rede (consulte a figura 2).
* Para uma rede virtual de vários locais, de conjunto de tooa de computadores no local de máquinas virtuais que residem no Olá mesmo serviço em nuvem de Olá virtual de rede (consulte a figura 3).
* As aplicações para a Internet, multicamadas na qual camadas de back-end Olá não são para a Internet, mas requerem balanceamento de carga para tráfego de camada de acesso à Internet Olá.
* Balanceamento de carga para aplicações de LOB alojadas no Azure, sem necessidade de software ou hardware de Balanceador de carga adicional. Incluindo servidores no local no conjunto de Olá de computadores cujo tráfego está a carga balanceado.

## <a name="internet-facing-multi-tier-applications"></a>Aplicações de várias camadas de com acesso à Internet

camada da web de Olá tem pontos finais com acesso à Internet para clientes de Internet e faz parte de um conjunto com balanceamento de carga. Balanceador de carga Olá distribui o tráfego recebido dos clientes web para TCP porta 443 (HTTPS) toohello servidores web.

servidores de base de dados de Olá estejam atrás de um ponto final ILB, que os servidores de web de Olá utilizam para armazenamento. Ponto final, o tráfego é balanceamento de carga em servidores de base de dados de Olá no conjunto ILB Olá com balanceamento de carga do serviço esta base de dados.

Olá a seguir mostra imagem Olá com acesso à aplicação multicamadas Internet dentro Olá mesmo serviço em nuvem.

![Serviço de nuvem única de balanceamento de carga interno](./media/load-balancer-internal-overview/IC736321.png)

Figura 1 - com acesso à aplicação multicamadas Internet

Outro uso possíveis para uma aplicação multicamada é quando Olá ILB implementado um serviço cloud diferente tooa que Olá um serviço de Olá consumo para Olá ILB.

Nuvem ponto final ILB de toohello aceder a serviços com Olá terão a mesma rede virtual. Olá segue mostra de imagem são servidores web front-end num serviço cloud diferente da base de dados de Olá back-end e utilizar Olá ponto final ILB dentro Olá mesma rede virtual.

![Interna balanceamento da carga entre serviços cloud](./media/load-balancer-internal-overview/IC744147.png)

Figura 2 - servidores front-end num serviço cloud diferente

## <a name="intranet-line-of-business-applications"></a>Intranet aplicações de linha de negócio

Tráfego de clientes na rede no local de Olá obter com balanceamento de carga em conjunto Olá dos servidores LOB utilizando a rede de tooAzure de ligação VPN.

computador de cliente Olá terão acesso tooan endereço IP do serviço de VPN do Azure através da VPN de ponto toosite. Permite Olá de utilização de Olá alojada por trás do ponto final ILB de Olá de aplicação de LOB.

![Através da VPN de ponto toosite de balanceamento de carga interno](./media/load-balancer-internal-overview/IC744148.png)

Figura 3 - aplicações de LOB alojadas por trás do ponto final de Olá LB

Outro cenário para Olá LOB é toohave uma toosite toohello virtual rede de VPNs onde o ponto final ILB de Olá está configurado. Isto permite que a rede tráfego toobe encaminhado toohello ILB ponto final no local.

![Site toosite VPN a utilizar o balanceamento de carga interno](./media/load-balancer-internal-overview/IC744150.png)

Figura 4 - tráfego de rede no local encaminhada toohello ILB endpoint

## <a name="limitations"></a>Limitações

Configurações de Balanceador de carga internas não suportam a realizar o SNAT. No contexto de Olá deste documento, realizar o SNAT refere-se tradução de endereços de rede tooport masquerading origem.  Isto aplica-se tooscenarios em que uma VM com um conjunto de Balanceador de carga tem o endereço IP de front-end do tooreach Olá respetivos interno Balanceador de carga. Este cenário não é suportado para o Balanceador de carga interno. Falhas de ligação irão ocorrer quando o fluxo de Olá é com balanceamento de carga toohello VM que teve origem fluxo Olá. Tem de utilizar um balanceador de carga de estilo de proxy para tais cenários.

## <a name="next-steps"></a>Passos Seguintes

[Suporte do Azure Resource Manager para o Balanceador de carga do Azure](load-balancer-arm.md)

[Começar a configurar um balanceador de carga com acesso de Internet](load-balancer-get-started-internet-arm-ps.md)

[Começar a configurar um balanceador de carga interno](load-balancer-get-started-ilb-arm-ps.md)

[Configurar um modo de distribuição de Balanceador de carga](load-balancer-distribution-mode.md)

[Configurar definições de tempo limite TCP inativo para o balanceador de carga](load-balancer-tcp-idle-timeout.md)
