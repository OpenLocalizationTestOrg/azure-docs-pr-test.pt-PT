---
title: "aaaWhat é o reencaminhamento do Azure e utilizá-lo por que motivo de descrição geral | Microsoft Docs"
description: "Descrição Geral do Reencaminhamento do Azure"
services: service-bus-relay
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 1e3e971d-2a24-4f96-a88a-ce3ea2b1a1cd
ms.service: service-bus-relay
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: get-started-article
ms.date: 08/23/2017
ms.author: sethm
ms.openlocfilehash: 4cfd77048210a435c446b908b7896737cad0edbf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-relay"></a>O que é o Reencaminhamento do Azure?

Olá híbrida aplicações, permitindo toosecurely expõem os serviços que residem numa empresarial rede toohello nuvem pública, sem ter tooopen uma ligação de firewall ou exigem intrusivo facilita o serviço de reencaminhamento de Azure alterações tooa infraestrutura da rede empresarial. O Reencaminhamento suporta uma variedade de diferentes protocolos de transporte e de padrões de serviços Web.

serviço de reencaminhamento de Olá suporta tradicional unidirecional, pedido/resposta e o tráfego de ponto a ponto. Também suporta a distribuição de eventos em cenários de publicação do âmbito de internet tooenable e comunicação de socket bidirecional para eficiência ponto a ponto maior. 

Padrão de transferência de dados de Olá retransmitida, um serviço no local liga-se o serviço de reencaminhamento toohello através de uma porta de saída e cria um socket bidirecional para o endereço de encontro específico tooa comunicação associada. cliente de Olá, em seguida, pode comunicar com o serviço no local de Olá enviando tráfego toohello serviço de reencaminhamento Olá endereço de encontro. serviço de reencaminhamento de Olá, em seguida, "reencaminha" serviço local de toohello de dados através de um cliente de tooeach dedicado de socket bidirecional. Olá cliente não precisa de um serviço do ligação direta toohello no local, não é necessário tooknow onde reside o serviço de Olá e serviço do Olá no local não precisa de nenhuma porta de entrada aberta na firewall de Olá.

elementos de capacidade de chave de Olá fornecidos pelo reencaminhamento são comunicação bidirecional, colocada em limites de rede com o TCP como limitação, deteção de ponto final, o estado de conectividade e overlaid segurança ponto a ponto. capacidades de reencaminhamento de Olá diferem das tecnologias de integração de nível de rede, tais como VPN, esse reencaminhamento pode ser confinada tooa ponto final de aplicação única num único computador, enquanto a tecnologia VPN é muito mais intrusivo como baseia-se numa alteração de ambiente de rede Olá .

O Reencaminhamento do Azure tem duas funcionalidades:

1. [As ligações híbridas](#hybrid-connections) - utiliza os sockets de abra web padrão Olá ativar cenários de várias plataformas.
2. [Reencaminhamentos de WCF](#wcf-relays) -chamadas de procedimento remoto tooenable utiliza o Windows Communication Foundation (WCF). Reencaminhamento de WCF é reencaminhamento legado Olá oferta que já utilizam muitos clientes com os respetivos modelos de programação de WCF.

As ligações híbridas e WCF reencaminhamentos ativar tooassets ligação segura que existem numa rede empresarial. Utilização de um através de outro Olá está dependente nas suas necessidades particulares, conforme descrito em Olá a tabela seguinte:

|  | Reencaminhamento do WCF | Ligações Híbridas |
| --- |:---:|:---:|
| **WCF** |x | |
| **.NET Core** | |x |
| **.NET Framework** |x |x |
| **JavaScript/NodeJS** | |x |
| **Standards-Based Open Protocol (Protocolo Aberto Baseado em Normas)** | |x |
| **Vários Modelos de Programação de RPC** | |x |

## <a name="hybrid-connections"></a>Ligações Híbridas

Olá [Azure reencaminhamento híbrido ligações](relay-hybrid-connections-protocol.md) capacidade é uma evolução segura e abra-protocolo de Olá existente funcionalidades de reencaminhamento que podem ser implementadas em qualquer plataforma e em qualquer idioma que tem uma capacidade de WebSocket básica, que inclui explicitamente Olá API de WebSocket em browsers comuns. As Ligações Híbridas baseiam-se em HTTP e WebSockets.

### <a name="service-history"></a>Histórico do Serviço

As ligações híbridas supplants anterior Olá, da mesma forma com o nome de funcionalidade de "BizTalk Services" que foi criada no Olá reencaminhamento de WCF de barramento de serviço do Azure. nova capacidade de ligações híbridas Olá complementa a funcionalidade de reencaminhamento de WCF existente Olá e estas capacidades de dois serviço existem lado lado a lado no serviço de reencaminhamento do Azure Olá. Partilham um gateway comum, mas, de resto, são implementações diferentes.

## <a name="wcf-relays"></a>Reencaminhamentos do WCF

Olá reencaminhamento WCF funciona para Olá completa .NET Framework (NETFX) e do WCF. Iniciar a ligação de Olá entre o serviço no local e o serviço de reencaminhamento de Olá utilizando um conjunto de enlaces de "reencaminhamento" WCF. Em segundo plano do Olá, Olá enlaces de reencaminhamento mapeiam toonew transporte enlace elementos concebidos toocreate WCF os componentes de canal que se integram ao Service Bus na nuvem de Olá.

## <a name="architecture-processing-of-incoming-relay-requests"></a>Arquitetura: processamento de pedidos de reencaminhamento recebidos
Quando um cliente envia um pedido toohello [Azure reencaminhamento](/azure/service-bus-relay/) serviço, o Balanceador de carga do Azure de Olá encaminha o mesmo tooany de nós de gateway Olá. Se o pedido de Olá é um pedido de serviço de escuta, o nó de gateway Olá cria um novo reencaminhamento. Se o pedido de Olá é um reencaminhamento específico do pedido tooa de ligação, o nó de gateway de Olá reencaminha Olá ligação pedido toohello nó de gateway que detém o reencaminhamento de Olá. nó de gateway Olá que detém o reencaminhamento de Olá envia um encontro pedido toohello escuta cliente, solicitando toocreate do serviço de escuta de Olá um nó de gateway do canal temporário toohello que recebeu o pedido de ligação de Olá.

Quando é estabelecida a ligação de reencaminhamento de Olá, os clientes de Olá podem trocar mensagens através do nó de gateway Olá, que é utilizado para o encontro Olá.

![Processamento de Pedidos de Reencaminhamento de WCF Recebidos](./media/relay-what-is-it/ic690645.png)

## <a name="next-steps"></a>Passos seguintes

* [FAQ de Reencaminhamento](relay-faq.md)
* [Criar um espaço de nomes](relay-create-namespace-portal.md)
* [Introdução ao .NET](relay-hybrid-connections-dotnet-get-started.md)
* [Introdução ao Node](relay-hybrid-connections-node-get-started.md)

