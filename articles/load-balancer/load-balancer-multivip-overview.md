---
title: aaaMultiple VIP de Balanceador de carga do Azure | Microsoft Docs
description: "Descrição geral de vários VIPs no balanceador de carga do Azure"
services: load-balancer
documentationcenter: na
author: chkuhtz
manager: narayan
editor: 
ms.assetid: 748e50cd-3087-4c2e-a9e1-ac0ecce4f869
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/11/2016
ms.author: chkuhtz
ms.openlocfilehash: e186e1248e7d187e7efd0668dc3244465ce3e156
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="multiple-vips-for-azure-load-balancer"></a>Múltiplos VIPs para o Azure Load Balancer

Balanceador de carga do Azure permite-lhe equilibrar os serviços tooload em várias portas, vários endereços IP ou ambos. Pode utilizar os fluxos de balanceamento de carga interno e público balanceador definições tooload através de um conjunto de VMs.

Este artigo descreve Olá Noções básicas sobre esta capacidade, conceitos importantes e as restrições. Se a que apenas pretende tooexpose serviços um endereço IP, pode encontrar instruções simplificadas para [pública](load-balancer-get-started-internet-portal.md) ou [interno](load-balancer-get-started-ilb-arm-portal.md) configurações de Balanceador de carga. A adição de vários VIPs é a configuração de VIP único incremental tooa. Utilizar conceitos Olá neste artigo, pode expandir uma configuração simplificada em qualquer altura.

Quando definir um balanceador de carga do Azure, estão ligados com regras de front-end e uma configuração de back-end. Olá referenciada pela regra Olá de sonda de estado de funcionamento é utilizada toodetermine como novo fluxos são enviados tooa nó no conjunto de back-end Olá. front-end de Olá é definido por um IP Virtual (VIP), que é uma 3 cadeias de identificação composta por um endereço IP (interno ou público), um protocolo de transporte (UDP ou TCP) e um número de porta. Um DIP é que um endereço IP numa NIC virtual do Azure anexados tooa VM no conjunto de back-end Olá.

Olá, a tabela seguinte contém algumas configurações de front-end de exemplo:

| VIP | Endereço IP | Protocolo | porta |
| --- | --- | --- | --- |
| 1 |65.52.0.1 |TCP |80 |
| 2 |65.52.0.1 |TCP |*8080* |
| 3 |65.52.0.1 |*UDP* |80 |
| 4 |*65.52.0.2* |TCP |80 |

tabela de Olá mostra quatro frontends diferentes. Frontends n. º 1, #2 e #3 são um VIP único com várias regras. Olá mesmo endereço IP é utilizado, mas porta Olá ou protocolo é diferente para cada front-end. Frontends n. º 1 e #4 são um exemplo de vários VIPs, onde hello mesmo protocolo de front-end e porta são reutilizadas em vários VIPs.

Balanceador de carga do Azure fornece flexibilidade na definição de regras de balanceamento de carga Olá. Uma regra declara como um endereço e porta de front-end de Olá está mapeada toohello endereço de destino e a porta no back-end de Olá. Se pretende ou não as portas de back-end são reutilizadas em regras dependem de tipo de Olá da regra de Olá. Cada tipo de regra tem requisitos específicos que podem afetar a estrutura de configuração e a sonda do anfitrião. Existem dois tipos de regras:

1. reutilizar a regra predefinida de Olá com nenhuma porta de back-end
2. regra de IP flutuante olá onde são reutilizadas portas de back-end

Balanceador de carga do Azure permite-lhe toomix ambos os tipos de regra no Olá a mesma configuração de Balanceador de carga. Balanceador de carga Olá pode utilizá-los em simultâneo para uma determinada VM ou qualquer combinação, desde que cumprir por restrições de Olá da regra de Olá. O tipo de regra que escolher depende de requisitos de Olá da sua aplicação e Olá complexidade de oferecer suporte a que a configuração. Deve avaliar que tipos de regra são melhores para o seu cenário.

Vamos explorar estes cenários mais iniciando com o comportamento predefinido de Olá.

## <a name="rule-type-1-no-backend-port-reuse"></a>#1 do tipo de regra: nenhum reutilização de porta de back-end

![Ilustração de MultiVIP](./media/load-balancer-multivip-overview/load-balancer-multivip.png)

Neste cenário, front-end de Olá VIPs estão configuradas da seguinte forma:

| VIP | Endereço IP | Protocolo | porta |
| --- | --- | --- | --- |
| ![VIP](./media/load-balancer-multivip-overview/load-balancer-rule-green.png) 1 |65.52.0.1 |TCP |80 |
| ![VIP](./media/load-balancer-multivip-overview/load-balancer-rule-purple.png) 2 |*65.52.0.2* |TCP |80 |

Olá DIP é destino Olá Olá fluxo de entrada. No conjunto de back-end Olá, cada VM expõe serviço Olá pretendido numa porta exclusivo num DIP. Este serviço está associado a front-end de Olá através da definição de uma regra.

Iremos definir duas regras:

| Regra | Mapear front-end | conjunto de toobackend |
| --- | --- | --- |
| 1 |![VIP](./media/load-balancer-multivip-overview/load-balancer-rule-green.png) VIP1:80 |![back-end](./media/load-balancer-multivip-overview/load-balancer-rule-green.png) DIP1:80, ![back-end](./media/load-balancer-multivip-overview/load-balancer-rule-green.png) DIP2:80 |
| 2 |![VIP](./media/load-balancer-multivip-overview/load-balancer-rule-purple.png) VIP2:80 |![back-end](./media/load-balancer-multivip-overview/load-balancer-rule-purple.png) DIP1:81, ![back-end](./media/load-balancer-multivip-overview/load-balancer-rule-purple.png) DIP2:81 |

mapeamento de conclusão de Olá no balanceador de carga do Azure está agora da seguinte forma:

| Regra | Endereço IP de VIP | Protocolo | porta | Destino | porta |
| --- | --- | --- | --- | --- | --- |
| ![Regra](./media/load-balancer-multivip-overview/load-balancer-rule-green.png) 1 |65.52.0.1 |TCP |80 |Endereço IP |80 |
| ![Regra](./media/load-balancer-multivip-overview/load-balancer-rule-purple.png) 2 |65.52.0.2 |TCP |80 |Endereço IP |81 |

Cada regra deve produzir um fluxo com uma combinação única de endereço IP de destino e porta de destino. Por variando Olá da porta de destino do fluxo de Olá, várias regras podem proporcionar fluxos toohello DIP mesmo nas portas diferentes.

Sondas de estado de funcionamento são sempre toohello direcionado DIP de uma VM. Tem de se certificar de se sua pesquisa reflete o estado de funcionamento de Olá de Olá VM.

## <a name="rule-type-2-backend-port-reuse-by-using-floating-ip"></a>Regra de tipo #2: reutilização de porta de back-end utilizando o IP flutuante

Balanceador de carga do Azure fornece flexibilidade de Olá porta de front-end de Olá tooreuse vários VIPs independentemente do tipo de regra de Olá utilizado. Além disso, alguns cenários de aplicação preferem ou exigem Olá mesmo toobe utilizado por várias instâncias de aplicações numa única VM no conjunto de back-end Olá de porta. Exemplos comuns de uma reutilização de porta incluem o clustering de elevada disponibilidade, aplicações virtuais e expor vários pontos finais TLS sem a encriptação de rede.

Se pretender que a porta de back-end de Olá tooreuse através de várias regras, tem de ativar o IP flutuante na definição da regra de Olá.

IP flutuante é uma parte do que é conhecida como direta servidor devolver (DSR). DSR consiste em duas partes: uma topologia de fluxo e um endereço IP esquema de mapeamento. Um nível de plataforma, o Balanceador de carga do Azure sempre funciona numa topologia de fluxo DSR independentemente se o IP flutuante está ativada ou não. Isto significa que Olá saída parte um fluxo sempre origem de anterior diretamente toohello tooflow corretamente conversão.

Com o tipo de regra predefinida de Olá, Azure expõe uma esquema de mapeamento de endereço IP para facilitar a utilização de balanceamento de carga tradicional. Ativar IP flutuante alterações Olá tooallow de esquema de mapeamento de endereço IP de flexibilidade adicional, como explicado abaixo.

Olá seguinte diagrama ilustra esta configuração:

![Ilustração de MultiVIP](./media/load-balancer-multivip-overview/load-balancer-multivip-dsr.png)

Para este cenário, a cada VM no conjunto de back-end Olá tem três interfaces de rede:

* DIP: uma NIC Virtual associado Olá VM (configuração de IP do recurso NIC do Azure)
* O VIP1: uma interface de loopback dentro do SO que está configurado com o endereço IP do VIP1 convidado
* VIP2: uma interface de loopback dentro do SO que está configurado com endereço IP de VIP2 convidado

> [!IMPORTANT]
> configuração de Olá das interfaces lógica Olá é efetuada convidado Olá SO. Esta configuração não é efetuada ou é gerida pelo Azure. Sem esta configuração, as regras de Olá não irão funcionar. Definições de pesquisa de estado de funcionamento utilizam Olá DIP de Olá VM em vez de Olá VIP lógico. Por conseguinte, o serviço tem de fornecer respostas de pesquisa numa porta DIP que refletir o estado de Olá do serviço de Olá disponibilizado no VIP lógica Olá.

Vamos supor que Olá mesma configuração de front-end como no cenário anterior Olá:

| VIP | Endereço IP | Protocolo | porta |
| --- | --- | --- | --- |
| ![VIP](./media/load-balancer-multivip-overview/load-balancer-rule-green.png) 1 |65.52.0.1 |TCP |80 |
| ![VIP](./media/load-balancer-multivip-overview/load-balancer-rule-purple.png) 2 |*65.52.0.2* |TCP |80 |

Iremos definir duas regras:

| Regra | Mapear front-end | conjunto de toobackend |
| --- | --- | --- |
| 1 |![Regra](./media/load-balancer-multivip-overview/load-balancer-rule-green.png) VIP1:80 |![back-end](./media/load-balancer-multivip-overview/load-balancer-rule-green.png) VIP1:80 (na VM1 e VM2) |
| 2 |![Regra](./media/load-balancer-multivip-overview/load-balancer-rule-purple.png) VIP2:80 |![back-end](./media/load-balancer-multivip-overview/load-balancer-rule-purple.png) VIP2:80 (na VM1 e VM2) |

Olá a tabela seguinte mostra o mapeamento de conclusão de Olá no balanceador de carga Olá:

| Regra | Endereço IP de VIP | Protocolo | porta | Destino | porta |
| --- | --- | --- | --- | --- | --- |
| ![VIP](./media/load-balancer-multivip-overview/load-balancer-rule-green.png) 1 |65.52.0.1 |TCP |80 |igual ao VIP (65.52.0.1) |igual ao VIP (80) |
| ![VIP](./media/load-balancer-multivip-overview/load-balancer-rule-purple.png) 2 |65.52.0.2 |TCP |80 |igual ao VIP (65.52.0.2) |igual ao VIP (80) |

destino de Olá de Olá fluxo de entrada é o endereço de Olá VIP na interface de loopback de Olá no Olá VM. Cada regra deve produzir um fluxo com uma combinação única de endereço IP de destino e porta de destino. Por variando Olá endereço IP de destino do fluxo de Olá, é possível no reutilização de porta Olá mesma VM. O serviço é Balanceador de carga toohello expostos pelo enlace de endereço IP e porta de interface de loopback respetivos Olá toohello do VIP.

Tenha em atenção que este exemplo não altera a porta de destino Olá. Apesar de este ser um cenário de IP flutuante, o Balanceador de carga do Azure suporta também definir uma regra toorewrite Olá back-end da porta de destino e toomake-diferente da porta de destino Olá front-end.

Olá, tipo de regra de IP flutuante é foundation Olá de vários padrões de configuração de Balanceador de carga. Um exemplo que está atualmente disponível é Olá [AlwaysOn de SQL com vários serviços de escuta](../virtual-machines/windows/sql/virtual-machines-windows-portal-sql-ps-alwayson-int-listener.md) configuração. Ao longo do tempo, iremos irá documentos mais um destes cenários.

## <a name="limitations"></a>Limitações

* Múltiplas configurações de VIP só são suportadas com VMs de IaaS.
* Com a regra de IP flutuante Olá, a aplicação tem de utilizar Olá DIP para fluxos de saída. Se a sua aplicação vincula o endereço de VIP toohello configurado na interface de loopback de Olá no SO de convidado de Olá, em seguida, realizar o SNAT não é o fluxo de saída do toorewrite disponíveis Olá e fluxo Olá falha.
* Endereços IP públicos têm um efeito em faturação. Para obter mais informações, consulte [preços do endereço IP](https://azure.microsoft.com/pricing/details/ip-addresses/)
* São aplicáveis a limites de subscrição. Para obter mais informações, consulte [os limites de serviço](../azure-subscription-service-limits.md#networking-limits) para obter mais detalhes.
