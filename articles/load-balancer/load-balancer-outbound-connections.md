---
title: "ligações de saída aaaUnderstanding no Azure | Microsoft Docs"
description: "Este artigo explica como o Azure permite toocommunicate VMs com serviços de Internet pública."
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: 
ms.assetid: 5f666f2a-3a63-405a-abcd-b2e34d40e001
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 5/31/2017
ms.author: kumud
ms.openlocfilehash: ffe59971b934a16c9f6f78e3b15869a0072320d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="understanding-outbound-connections-in-azure"></a>Compreender as ligações de saída no Azure

Uma Máquina Virtual (VM) no Azure podem comunicar com pontos finais fora do Azure no espaço de endereços IP públicos. Quando uma VM inicia um destino de fluxo de saída tooa no espaço de endereço IP público, o Azure mapeia privado IP endereço tooa endereço IP público da VM Olá e permite Olá tooreach do tráfego de retorno VM.

O Azure oferece três métodos diferentes tooachieve conectividade de saída. Cada método tem as suas próprias capacidades e limitações. Reveja cada método cuidadosamente toochoose que satisfaça as suas necessidades.

| Cenário | Método | Nota |
| --- | --- | --- |
| VM autónoma (nenhum Balanceador de carga, nenhum endereço IP público de nível de instância) |Predefinição realizar o SNAT |Azure associa um endereço IP público para realizar o SNAT |
| VM de balanceamento de carga (nenhum endereço IP público de nível de instância na VM) |Realizar o SNAT utilizando Olá Balanceador de carga |Azure utiliza um endereço IP público de Olá Balanceador de carga para realizar o SNAT |
| VM com o endereço IP público de nível de instância (com ou sem Balanceador de carga) |Realizar o SNAT não é utilizado |IP público Olá atribuído toohello VM utiliza o Azure |

Se não pretender toocommunicate uma VM com pontos finais fora do Azure no espaço de endereços IP públicos, pode utilizar o acesso de tooblock de grupos de segurança de rede (NSG). Utilizar NSGs é abordada mais detalhadamente na [impedir a conectividade pública](#preventing-public-connectivity).

## <a name="standalone-vm-with-no-instance-level-public-ip-address"></a>VM autónoma com nenhum endereço IP público de nível de instância

Neste cenário, Olá VM não faz parte de um conjunto de Balanceador de carga do Azure e não tem um endereço de IP de público ao nível do instância (ILPIP) atribuído tooit. Quando Olá VM cria um fluxo de saída, Azure traduz endereço IP de origem privada Olá do endereço IP de origem público de tooa de fluxo de saída de Olá. endereço IP público Olá utilizado para este fluxo de saída não é configurável e não count contra Olá público IP recurso o limite da subscrição. Azure utiliza tooperform origem rede endereço tradução (realizar o SNAT), esta função. Portas efémeras do endereço IP público do Olá são fluxos individuais utilizados toodistinguish teve originados por Olá VM. Realizar o SNAT atribui dinamicamente portas efémeras quando fluxos são criados. Neste contexto, portas efémeras Olá utilizadas para realizar o SNAT são referidos tooas realizar o SNAT portas.

Portas de realizar o SNAT são um recurso finito que pode ser esgotado. É importante toounderstand como são consumidos. Uma porta de realizar o SNAT é consumida por endereço IP de destino única de tooa de fluxo. Para vários fluxos toohello mesmo endereço IP de destino, cada fluxo consome uma única porta de realizar o SNAT. Isto assegura que Olá fluxos são exclusivo quando teve origem Olá mesmo toohello de endereço IP público mesmo endereço IP de destino. Vários fluxos, cada endereço IP de destino diferentes tooa consumir uma única porta de realizar o SNAT por destino. endereço IP de destino Olá torna Olá fluxos única.

Pode utilizar [análise de registos para o Balanceador de carga](load-balancer-monitor-log.md) e [toomonitor de registos de eventos de alerta para mensagens de esgotamento de porta de realizar o SNAT](load-balancer-monitor-log.md#alert-event-log). Quando os recursos de porta de realizar o SNAT ficam esgotados, fluxos de saída falharem até que as portas de realizar o SNAT lançadas pela fluxos existentes. Balanceador de carga utiliza um tempo de limite de inatividade de 4 minutos para as portas de realizar o SNAT de reclamação.

## <a name="load-balanced-vm-with-no-instance-level-public-ip-address"></a>VM de balanceamento de carga com nenhum endereço IP público de nível de instância

Neste cenário, Olá VM faz parte de um conjunto de Balanceador de carga do Azure.  Olá VM não tem um endereço IP público atribuído tooit. Olá recurso de Balanceador de carga tem de ser configurado com uma regra toolink Olá pública IP Front-end com o conjunto de back-end Olá.  Se não concluir esta configuração, o comportamento de Olá é conforme descrito na secção de Olá acima para [autónoma de VM com nenhuma IP público de nível de instância](load-balancer-outbound-connections.md#standalone-vm-with-no-instance-level-public-ip-address).

Quando hello VM de balanceamento de carga cria um fluxo de saída, Azure traduz endereço IP de origem privada Olá do Olá fluxo de saída toohello endereço IP público do Olá pública Load Balancer front-end. Azure utiliza tooperform origem rede endereço tradução (realizar o SNAT), esta função. Portas efémeras do endereço IP público do Balanceador de carga Olá são fluxos individuais utilizados toodistinguish teve originados por Olá VM. Realizar o SNAT atribui dinamicamente portas efémeras quando são criados os fluxos de saída. Neste contexto, portas efémeras Olá utilizadas para realizar o SNAT são referidos tooas realizar o SNAT portas.

Portas de realizar o SNAT são um recurso finito que pode ser esgotado. É importante toounderstand como são consumidos. Uma porta de realizar o SNAT é consumida por endereço IP de destino única de tooa de fluxo. Para vários fluxos toohello mesmo endereço IP de destino, cada fluxo consome uma única porta de realizar o SNAT. Isto assegura que Olá fluxos são exclusivo quando teve origem Olá mesmo toohello de endereço IP público mesmo endereço IP de destino. Vários fluxos, cada endereço IP de destino diferentes tooa consumir uma única porta de realizar o SNAT por destino. endereço IP de destino Olá torna Olá fluxos única.

Pode utilizar [análise de registos para o Balanceador de carga](load-balancer-monitor-log.md) e [toomonitor de registos de eventos de alerta para mensagens de esgotamento de porta de realizar o SNAT](load-balancer-monitor-log.md#alert-event-log). Quando os recursos de porta de realizar o SNAT ficam esgotados, fluxos de saída falharem até que as portas de realizar o SNAT lançadas pela fluxos existentes. Balanceador de carga utiliza um tempo de limite de inatividade de 4 minutos para as portas de realizar o SNAT de reclamação.

## <a name="vm-with-an-instance-level-public-ip-address-with-or-without-load-balancer"></a>VM com um endereço IP público de nível de instância (com ou sem Balanceador de carga)

Neste cenário, Olá VM tem uma instância do nível pública IP (ILPIP) atribuído tooit. Não importa se Olá VM está ou não de balanceamento de carga. Quando é utilizado um ILPIP, origem rede endereço tradução (realizar o SNAT) não é utilizado. Olá VM utiliza Olá ILPIP para todos os fluxos de saída. Se muitos fluxos de saída inicia a sua aplicação e experiência de esgotamento de realizar o SNAT, deve considerar a atribuir um tooavoid ILPIP restrições de realizar o SNAT.

## <a name="discovering-hello-public-ip-used-by-a-given-vm"></a>Detetar Olá IP público utilizado por uma determinada VM

Existem várias formas endereço IP do toodetermine Olá fonte públicos de uma ligação de saída. OpenDNS fornece um serviço que pode apresentar-lhe Olá endereço IP público da sua VM. Utilização do comando nslookup Olá, pode enviar uma consulta DNS para resolução de OpenDNS Olá nome myip.opendns.com toohello. serviço de Olá devolve o endereço IP de origem Olá que estava a consulta de Olá toosend utilizados. Quando executar Olá seguintes consultas de VM, resposta Olá é Olá que IP público utilizado relativamente a essa VM.

    nslookup myip.opendns.com resolver1.opendns.com

## <a name="preventing-public-connectivity"></a>Impedir a Conetividade pública

Por vezes, não é desejável para uma VM toobe permitido toocreate um fluxo de saída ou poderá existir um toomanage de requisito que destinos podem ser acedidos com fluxos de saída. Neste caso, utilize [grupos de segurança de rede (NSG)](../virtual-network/virtual-networks-nsg.md) toomanage Olá destinos que Olá VM pode aceder. Quando aplica um NSG tooa com balanceamento de carga VM, tem de toopay atenção toohello [predefinido etiquetas](../virtual-network/virtual-networks-nsg.md#default-tags) e [predefinido regras](../virtual-network/virtual-networks-nsg.md#default-rules).

Tem de se certificar de que Olá VM pode receber pedidos de sonda de estado de funcionamento do Balanceador de carga do Azure. Se um NSG blocos estado de funcionamento pedidos de sonda de Olá etiqueta predefinida AZURE_LOADBALANCER, a pesquisa de estado de funcionamento da VM falha e Olá VM está marcado como. Balanceador de carga para o envio de novos fluxos toothat VM.

## <a name="limitations"></a>Limitações

Se [vários endereços IP (públicos) estão associados um balanceador de carga](load-balancer-multivip-overview.md), os endereços estes IPs públicos são uma candidata para fluxos de saída.

Azure utiliza uma algoritmo toodetermine Olá diversas portas realizar o SNAT disponíveis com base no tamanho Olá do conjunto de Olá.  Isto não é configurável neste momento.

É importante toorememember Olá número de portas de realizar o SNAT disponíveis traduz diretamente toonumber de ligações. Consulte acima para informações específicas sobre quando e como portas de realizar o SNAT são alocadas e como toomanage este recurso exhaustible.
