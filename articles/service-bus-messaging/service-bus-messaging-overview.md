---
title: "Descrição geral de mensagens de Service Bus do aaaAzure | Microsoft Docs"
description: "Descrição das mensagens do Service Bus e Reencaminhamento do Azure"
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: f99766cb-8f4b-4baf-b061-4b1e2ae570e4
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: get-started-article
ms.date: 05/25/2017
ms.author: sethm
ms.openlocfilehash: ede2904e11544d8f9428a2d657dcc77dacd95ac4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="service-bus-messaging-flexible-data-delivery-in-hello-cloud"></a>Mensagens do Service Bus: entrega flexível de dados na nuvem de Olá
O Microsoft Azure Service Bus é um serviço fiável de entrega de informações. objetivo Olá deste serviço é mais fácil de comunicação toomake. Quando duas ou mais entidades querem tooexchange informações, precisam de um facilitator de comunicação. O Service Bus é um mecanismo de comunicação mediado ou de terceiros. Isto é semelhante serviço postal de tooa no Olá, mundo físico. Os serviços postais torna muito fácil toosend diferentes tipos de cartas e pacotes com uma variedade de garantias de entrega, em qualquer lugar no Olá mundo.

Serviço postal semelhante toohello, entrega letras, o Service Bus é entrega flexível de informações do remetente de Olá e destinatário Olá. Olá, serviço de mensagens assegura que as informações de Olá é entregue, mesmo se Olá duas partes nunca estão online em Olá mesmo tempo, ou se não estão disponíveis em Olá exacta mesmo tempo. Desta forma, as mensagens são semelhante toosending uma letra, enquanto a comunicação não mediada é semelhante tooplacing uma chamada telefónica (ou como uma chamada telefónica costumava toobe - antes da chamada de espera ID, o qual são muito mais semelhantes a mensagens mediadas).

remetente da mensagem Olá também pode exigir uma variedade de características de entrega incluindo transações, deteção de duplicados, expiração com base no tempo e criação de batches. Estes padrões também têm analogias postais: repetição de entrega, assinatura necessária, alteração de endereço ou devolução de chamada.

O Service Bus suporta dois padrões de mensagens distintos: *Reencaminhamento do Azure* e *Mensagens do Service Bus*.

## <a name="azure-relay"></a>Reencaminhamento do Azure
Olá [reencaminhamento WCF](../service-bus-relay/relay-what-is-it.md) componente do reencaminhamento do Azure é um serviço centralizado (mas carga muito equilibrada) que suporta uma variedade de protocolos diferentes de transporte e padrões de serviços Web. Inclui SOAP, WS-* e até REST. Olá [serviço de reencaminhamento](../service-bus-relay/service-bus-dotnet-how-to-use-relay.md) proporciona uma variedade de opções de conectividade de reencaminhamento diferentes e podem ajudá-lo a negociação de ligações diretas ponto a ponto a ponto sempre que for possível. Barramento de serviço está otimizado para os programadores de .NET que utilizam Olá Windows Communication Foundation (WCF), ambos com regard tooperformance e a facilidade de utilização, e fornece acesso total tooits serviço de reencaminhamento através de interfaces SOAP e REST. Isto torna possível para qualquer programação SOAP ou REST toointegrate de ambiente com o Service Bus.

serviço de reencaminhamento de Olá suporta as tradicionais mensagens unidirecionais, mensagens de mensagens de pedido/resposta e mensagens ponto a ponto. Também suporta a distribuição de eventos no âmbito de Internet tooenable de publicação-subscrição e comunicação de socket bidirecional para eficiência ponto a ponto aumento de cenários. No padrão de mensagens retransmitido do Olá, um serviço no local liga-se o serviço de reencaminhamento toohello através de uma porta de saída e cria um socket bidirecional para o endereço de encontro específico tooa comunicação associada. cliente de Olá, em seguida, pode comunicar com o serviço no local de Olá enviando mensagens toohello serviço de reencaminhamento Olá endereço de encontro. serviço de reencaminhamento de Olá será, em seguida, "serviço de reencaminhamento" mensagens toohello no local através de socket bidirecional de Olá já no local. Olá cliente não precisa de um serviço do ligação direta toohello no local, nem é it necessário tooknow onde reside o serviço de Olá e serviço do Olá no local não precisa de nenhuma porta de entrada aberta na firewall de Olá.

Iniciar ligação Olá entre o serviço no local e o serviço de reencaminhamento de Olá, utilizando um conjunto de enlaces de "reencaminhamento" WCF. Em segundo plano do Olá, Olá enlaces de reencaminhamento mapeiam tootransport enlace elementos concebidos toocreate WCF os componentes de canal que se integram ao Service Bus na nuvem de Olá.

Reencaminhamento WCF muitas vantagens, mas requer Olá servidor e cliente tooboth estar online no Olá mesmo tempo em ordem toosend e receber mensagens. Não é ideal para comunicação de estilo HTTP, na qual Olá pedidos não podem ser normalmente longa duração, nem para os clientes que só se ligam ocasionalmente, tais como navegadores, aplicações móveis e assim sucessivamente. As mensagens mediadas suportam comunicação desacoplada e tem as suas próprias vantagens; os clientes e servidores podem ligar-se quando seja necessário e efetuar as operações de forma assíncrona.

## <a name="brokered-messaging"></a>Mensagens mediadas
Em contrapartida toohello reencaminhamento esquema de mensagens, do Service Bus ou [mensagens mediadas](service-bus-queues-topics-subscriptions.md) pode ser considerar-se como assíncronas ou "temporariamente desacopladas". Os produtores (remetentes) e os consumidores (recetores) não têm toobe online em Olá mesmo tempo. infraestrutura de mensagens Hello armazena de forma fiável as mensagens no "Mediador" (por exemplo, uma fila) até que a parte consumidora Olá está pronto tooreceive-los. Isto permite que os componentes de Olá de Olá distribuída aplicação toobe desligados, quer voluntariamente; Por exemplo, para manutenção, quer devido a falha de componente tooa, sem afetar o sistema completo Olá. Além disso, aplicação recetora Olá só pode ter toocome online durante determinadas horas do dia de Olá, tais como um sistema de gestão que apenas é necessário toorun no fim de Olá do dia de negócio Olá.

componentes principais de Olá da infraestrutura de mensagens mediada Olá Service Bus são filas, tópicos e subscrições.  Step-by-Olá principal diferença é que os tópicos suportam funcionalidades de publicação/subscrição que podem ser utilizadas para sofisticadas baseada no conteúdo encaminhamento e lógica de entrega, incluindo o envio toomultiple destinatários. Estes componentes permitem novos cenários de mensagens assíncronas, tais como desacoplamento temporal, publicação/subscrição e balanceamento de carga. Para mais informações sobre estas entidades de mensagens, consulte o artigo [Filas, tópicos e subscrições do Service Bus](service-bus-queues-topics-subscriptions.md).

Como com a infraestrutura de reencaminhamento de WCF Olá, Olá mensagens mediadas capacidade é fornecida para programadores de WCF e .NET Framework bem como através de REST.

## <a name="next-steps"></a>Passos seguintes
toolearn mais informações sobre mensagens do Service Bus, consulte Olá os seguintes tópicos.

* [Noções básicas sobre o Service Bus](service-bus-fundamentals-hybrid-solutions.md)
* [Filas, tópicos e subscrições do Service Bus](service-bus-queues-topics-subscriptions.md)
* [Como toouse filas do Service Bus](service-bus-dotnet-get-started-with-queues.md)
* [Como toouse Service Bus tópicos e subscrições](service-bus-dotnet-how-to-use-topics-subscriptions.md)

