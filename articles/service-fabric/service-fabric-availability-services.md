---
title: "aaaAvailability dos serviços do Service Fabric | Microsoft Docs"
description: "Descreve a deteção de falhas e ativação pós-falha e recuperação para os serviços"
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: 279ba4a4-f2ef-4e4e-b164-daefd10582e4
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: c443aadfe31a1413359b08d34c4b7dd5db4edd16
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="availability-of-service-fabric-services"></a>Disponibilidade dos serviços do Service Fabric
Este artigo fornece uma descrição geral de como o Service Fabric mantém a disponibilidade de um serviço.

## <a name="availability-of-service-fabric-stateless-services"></a>Disponibilidade dos serviços sem monitorização de estado do Service Fabric
Serviços do Service Fabric do Azure podem ser com monitorização de estado ou sem monitorização de estado. Um serviço sem monitorização de estado é um serviço de aplicações que não tem nenhuma [estado local](service-fabric-concepts-state.md) que necessita de toobe altamente disponível ou fiável.

A criação de um serviço sem estado requer a definir um `InstanceCount`. Contagem de instâncias de Olá define o número de Olá de instâncias de lógica de aplicação do serviço Olá sem monitorização de estado que deve estar em execução no cluster de Olá. Aumentar o número de instâncias Olá é Olá recomendado forma de ampliar um serviço sem estado.

Quando uma instância de um sem monitorização de estado com o nome do serviço falha, é criada uma nova instância em algumas elegível nó no cluster de Olá. Por exemplo, uma instância de serviço sem monitorização de estado pode falhar no Nó1 e ser recriada no Nó5.

## <a name="availability-of-service-fabric-stateful-services"></a>Disponibilidade dos serviços de monitorização de estado de Service Fabric
Um serviço com estado tem algumas Estado associado. No Service Fabric, um serviço com estado é modelado como um conjunto de réplicas. Cada réplica é uma instância em execução de código Olá Olá do serviço de que tem também uma cópia do Estado de Olá relativamente a esse serviço. Operações de leitura e escrita são efetuadas a uma réplica (denominada Olá principal). Alterações toostate de operações de escrita são *replicado* toohello outras réplicas no conjunto de réplicas de Olá (denominadas bases de dados secundárias Active Directory) e aplicada. 

Podem existir apenas uma réplica primária, mas podem existir várias réplicas secundárias do Active Directory. número de Olá de réplicas secundárias do Active Directory é configurável e um número mais elevado de réplicas pode tolerar um maior número de falhas de hardware e software em simultâneo.

Se a réplica primária Olá ficar inativo, o Service Fabric faz com que um dos Olá secundária ativa réplicas Olá nova réplica primária. Esta réplica secundária, o Active Directory já tem uma versão Olá atualizado do Estado de Olá (através de *replicação*), pode continuar a processar leitura adicional e operações de escrita.

Este conceito, de uma réplica a ser um principal ou secundária ativa, é conhecido como Olá função de réplica.

### <a name="replica-roles"></a>Funções de réplica
função de Olá de uma réplica é utilizado toomanage Olá do ciclo de vida do Estado de Olá a ser gerido por essa réplica. Pedidos de leitura de uma réplica cuja função é serviços primários. Olá principal também processa todos os pedidos de escrita ao atualizar o estado e replicar Olá alterações. Estas alterações são aplicada toohello Active Directory bases de dados secundárias no conjunto de réplicas Olá. tarefa de Olá de uma secundária ativa é alterações de estado de tooreceive Olá réplica primária foi replicado e atualize a vista de estado de Olá.

> [!NOTE]
> Programação de nível mais elevada, tais como modelos [Reliable Actors](service-fabric-reliable-actors-introduction.md) e [Reliable Services](service-fabric-reliable-services-introduction.md) ocultar o conceito de Olá da função de réplica do Programador de Olá. Atores, noção Olá da função é desnecessária, nos serviços de que é amplamente simplificado para a maioria dos cenários.
>

## <a name="next-steps"></a>Passos seguintes
Para obter mais informações sobre os conceitos de Service Fabric, consulte Olá seguintes artigos:

- [Dimensionamento serviços do Service Fabric](service-fabric-concepts-scalability.md)
- [A criação de partições de serviços do Service Fabric](service-fabric-concepts-partitioning.md)
- [Definir e gerir o Estado](service-fabric-concepts-state.md)
- [Reliable Services](service-fabric-reliable-services-introduction.md)
