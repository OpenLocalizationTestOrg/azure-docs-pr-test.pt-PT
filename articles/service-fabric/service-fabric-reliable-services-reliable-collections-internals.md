---
title: "aaaAzure características de Gestor de estado do serviço de recursos de infraestrutura fiável e fiável de coleção | Microsoft Docs"
description: "Descrição profunda sobre conceitos de coleção fiável e estrutura no Service Fabric do Azure."
services: service-fabric
documentationcenter: .net
author: mcoskun
manager: timlt
editor: rajak
ms.assetid: 62857523-604b-434e-bd1c-2141ea4b00d1
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 5/1/2017
ms.author: mcoskun
ms.openlocfilehash: 651bfb52785a2475e4840cd471e87220d1936391
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-service-fabric-reliable-state-manager-and-reliable-collection-internals"></a>Características de Gestor de estado de fiável de recursos de infraestrutura de serviço do Azure e fiável de coleção
Este documento delves no interior do Gestor de estado fiável e coleções fiável toosee como funcionam os componentes principais em segundo plano de Olá.

> [!NOTE]
> Este documento é trabalho em curso. Adicionar comentários toothis artigo tootell-nos que tópico que gostaria de mais informações sobre toolearn.
>

##  <a name="local-persistence-model-log-and-checkpoint"></a>Modelo de persistência local: registo e ponto de verificação
Olá fiável Gestor de estado e coleções fiável siga um modelo de persistência que é chamado registo e ponto de verificação.
Neste modelo, cada alteração de estado é registada no disco pela primeira vez e, em seguida, aplicada na memória.
Estado de conclusão de Olá próprio é persistente apenas ocasionalmente (a.k.a. Ponto de verificação).
benefício de Olá é que deltas transformados sequenciais acrescentar apenas operações de escrita no disco para um melhor desempenho.

toobetter compreender Olá registo e o modelo de ponto de verificação, vamos ver pela primeira vez no cenário de disco infinita Olá.
Olá fiável Gestor de estado os registos de cada operação está a replicar.
Registo permite-operação de Olá Olá coleções fiável tooapply apenas na memória.
Uma vez que os registos são mantidos, mesmo quando a réplica Olá falha e precisa de toobe reiniciado, Olá fiável Gestor de estado tem informações suficientes no respetivo registo tooreplay todas as operações de Olá perdeu-se a réplica de Olá.
Como disco de Olá é infinito, registos nunca precisam de toobe removido e hello fiável necessita de estado do toomanage apenas Olá dentro da memória.

Agora vamos ver cenário de Olá de disco finito.
Conforme registos acumularem, Olá fiável Gestor de estado irá executar sem espaço em disco.
Antes do que acontece, Olá fiável Gestor de estado tem tootruncate sala de toomake respetivo registo para os registos de Olá mais recentes.
Pedidos de Gestor de estado de fiável Olá coleções fiável toocheckpoint toodisk respetivo estado na memória.
Neste momento, coleções fiável Olá seria manter o estado de memória.
Depois de coleções fiável Olá concluir os respetivos pontos de verificação, Olá fiável Gestor de estado pode truncar Olá registo toofree espaço em disco.
Quando a réplica de Olá tem toobe reiniciado, coleções fiável recuperar o respetivo estado checkpointed e hello fiável Gestor de estado recupera e reproduz todas as alterações de estado de Olá que ocorreram desde o último ponto de verificação Olá.

Adicionar outro valor de ponto de verificação é o que melhora os tempos de recuperação em cenários comuns. Registo contém todas as operações que ocorreram desde o último ponto de verificação Olá.
Por isso,-pode incluir várias versões de um item como vários valores para uma linha fornecido no dicionário fiável.
Em contrapartida, pontos de verificação uma coleção fiável Olá apenas a versão mais recente de cada valor de uma chave.

## <a name="next-steps"></a>Passos seguintes
* [Transações e bloqueios](service-fabric-reliable-services-reliable-collections-transactions-locks.md)

