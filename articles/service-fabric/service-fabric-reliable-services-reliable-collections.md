---
title: "aaaIntroduction tooReliable coleções nos serviços de monitorização de estado de Service Fabric do Azure | Microsoft Docs"
description: "Serviços do Service Fabric com monitorização de estado fornecem fiáveis coleções que lhe permitem toowrite aplicações de nuvem de elevada disponibilidade, dimensionáveis e baixa latência."
services: service-fabric
documentationcenter: .net
author: mcoskun
manager: timlt
editor: masnider,rajak
ms.assetid: 62857523-604b-434e-bd1c-2141ea4b00d1
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 5/1/2017
ms.author: mcoskun
ms.openlocfilehash: 9f67c48f13e8b91b84977e127e2545cbb9d9a158
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooreliable-collections-in-azure-service-fabric-stateful-services"></a>Introdução tooReliable coleções nos serviços de monitorização de estado do Azure Service Fabric
Coleções fiáveis permitem às aplicações de nuvem de elevada disponibilidade, dimensionáveis e baixa latência toowrite dado a entender, foram escrever as aplicações de computador individual. Olá classes no Olá **Microsoft.ServiceFabric.Data.Collections** espaço de nomes fornecem um conjunto de coleções que tornam o estado de disponibilidade elevada automaticamente. Os programadores têm tooprogram apenas toohello fiável de coleção de APIs e permitem coleções fiável gerir Olá replicados e estado local.

diferença de chave de Olá entre coleções fiável e outras tecnologias de elevada disponibilidade (tais como Redis, o serviço de tabela do Azure e o serviço de fila do Azure) é que o estado de Olá é mantido localmente numa instância de serviço Olá ao também a ser tornado de elevada. Isto significa que:

* Todas as leituras são locais, que resulta numa latência baixa e lê débito elevado.
* Todas as escritas implicar Olá número mínimo de rede em IOs, que resulta em baixa latência e escreve débito elevado.

![Imagem da evolução das coleções.](media/service-fabric-reliable-services-reliable-collections/ReliableCollectionsEvolution.png)

Coleções fiáveis podem considerar como evolução natural do Olá do Olá **System.Collections** classes: um novo conjunto de coleções que foram concebidos para aplicações de nuvem e de computador multi Olá, sem aumentar a complexidade para Programador Olá. Como tal, são coleções fiável:

* Replicadas: Alterações de estado são replicadas para elevada disponibilidade.
* Persistente: Os dados são toodisk persistente para uma durabilidade contra falhas em grande escala (por exemplo, uma centro de dados de falha de energia).
* Assíncrona: As APIs são assíncrona tooensure que threads não estão bloqueadas durante a incorrer em e/s.
* Transacional: APIs utilizam abstração Olá de transações para que consiga gerir facilmente várias coleções fiável dentro de um serviço.

Coleções fiáveis de fornecer a consistência forte garante fora Olá caixa toomake reasoning sobre o estado da aplicação mais facilmente.
A consistência forte é conseguida ao garantir que a transação consolidações concluir apenas depois de transação todo Olá foi registada no quórum maioria de réplicas, incluindo Olá principal.
consistência mais fraco de tooachieve, aplicações podem reconhecer toohello anterior. o cliente/autor do pedido antes de consolidação assíncrona Olá devolve.

Olá fiável coleções as APIs são uma evolução de colecções simultâneas APIs (localizado no Olá **System.Collections.Concurrent** espaço de nomes):

* Assíncrona: Devolve uma tarefa, uma vez que, ao contrário das coleções em simultâneo, as operações de Olá são replicadas e persistente.
* Não parâmetros out: utiliza `ConditionalValue<T>` tooreturn um booleano e um valor em vez de parâmetros de saída. `ConditionalValue<T>`é como `Nullable<T>` mas não necessita de T toobe uma estrutura.
* Transações: Utiliza uma transação objeto tooenable Olá toogroup as ações do utilizador em várias coleções fiável numa transação.

Hoje em dia, **Microsoft.ServiceFabric.Data.Collections** contém três coleções:

* [Dicionário fiável](https://msdn.microsoft.com/library/azure/dn971511.aspx): representa uma coleção replicada, transacional e assíncrona de pares chave/valor. Semelhante demasiado**ConcurrentDictionary**, ambos Olá chave e valor de Olá pode ser de qualquer tipo.
* [Fila fiável](https://msdn.microsoft.com/library/azure/dn971527.aspx): representa uma replicados, transacional e assíncrona strict first in, First Out (FIFO) da fila. Semelhante demasiado**ConcurrentQueue**, valor de Olá pode ser de qualquer tipo.
* [Fila simultâneas fiável](service-fabric-reliable-services-reliable-concurrent-queue.md): representa um replicados, transacional e assíncrono melhor esforço ordenação fila para o débito elevado. Toohello semelhante **ConcurrentQueue**, valor de Olá pode ser de qualquer tipo.

## <a name="next-steps"></a>Passos seguintes
* [Coleção fiável diretrizes e recomendações](service-fabric-reliable-services-reliable-collections-guidelines.md)
* [Trabalhar com as Reliable Collections](service-fabric-work-with-reliable-collections.md)
* [Transações e bloqueios](service-fabric-reliable-services-reliable-collections-transactions-locks.md)
* [Gestor de estado fiável e características de coleção](service-fabric-reliable-services-reliable-collections-internals.md)
* Gestão de dados
  * [Cópia de Segurança e Restauro](service-fabric-reliable-services-backup-restore.md)
  * [Notificações](service-fabric-reliable-services-notifications.md)
  * [Serialização das Reliable Collections](service-fabric-reliable-services-reliable-collections-serialization.md)
  * [Serialização e a atualização](service-fabric-application-upgrade-data-serialization.md)
  * [Configuração do Gestor de estado de fiável](service-fabric-reliable-services-configuration.md)
* Outros
  * [Início rápido de serviços fiável](service-fabric-reliable-services-quick-start.md)
  * [Referência para programadores para coleções fiável](https://msdn.microsoft.com/library/azure/microsoft.servicefabric.data.collections.aspx)
