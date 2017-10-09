---
title: "as definições de métricas e colocação aaaSpecify no Azure micro-serviços | Microsoft Docs"
description: "Que descrevem um serviço do Service Fabric, especificando métricas, restrições de posicionamento e outras políticas de colocação."
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: 16e135c1-a00a-4c6f-9302-6651a090571a
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: c633518b5dbf0c7b84e0d46c06bf1f92365d184d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-cluster-resource-manager-settings-for-service-fabric-services"></a>Configurar definições de Gestor de recursos do cluster para serviços do Service Fabric
Olá Gestor de recursos de Cluster do serviço de recursos de infraestrutura permite um controlo detalhado sobre regras de Olá que regem cada indivíduo com o nome de serviço. Cada serviço com o nome pode especificar regras para a forma como deve ser alocada no cluster de Olá. Cada serviço com nome também pode definir o conjunto de Olá de métricas que quer que tooreport, incluindo como estes são importantes toothat serviço. Configurar os serviços divide em três tarefas diferentes:

1. Configurar restrições de posicionamento
2. Configurar as métricas
3. Configurar políticas de colocação avançadas e outras regras (menos comum)

## <a name="placement-constraints"></a>Restrições de posicionamento
Restrições de posicionamento são utilizado toocontrol quais os nós no cluster de Olá um serviço, na verdade, pode executar em. Normalmente, um determinado nome instância de serviço ou de todos os serviços de toorun um determinado tipo restringido num determinado tipo de nó. Restrições de posicionamento estão extensíveis. Pode definir qualquer conjunto de propriedades de cada tipo de nó e, em seguida, selecione para os mesmos com restrições de durante a criação de serviços. Também pode alterar as restrições de posicionamento de um serviço enquanto estiver em execução. Isto permite-lhe toorespond toochanges no cluster de Olá ou requisitos de Olá do serviço de Olá. Também é possível atualizar as propriedades de Olá de um determinado nó dinamicamente num cluster de Olá. Obter mais informações sobre restrições de posicionamento e como tooconfigure-los podem ser encontrados na [neste artigo](service-fabric-cluster-resource-manager-cluster-description.md#node-properties-and-placement-constraints)

## <a name="metrics"></a>Métricas
As métricas são conjunto de Olá dos recursos que necessita de um determinado serviço com nome. Configuração da métrica de um serviço inclui a quantidade de recurso de cada réplica de monitorização de estado ou sem monitorização de estado instância desse serviço consome por predefinição. As métricas incluem também uma ponderação que indica a importância balanceamento esse métrica é toothat serviço, no caso de fala é necessárias.

## <a name="advanced-placement-rules"></a>Regras de posicionamento avançadas
Existem outros tipos de regras de posicionamento que são úteis em menos cenários comuns. Alguns exemplos incluem:
- Restrições que ajudar com clusters distribuídos geograficamente
- Determinados arquiteturas de aplicações

Outras regras de posicionamento são configuradas através de correlações ou políticas.

## <a name="next-steps"></a>Passos seguintes
- As métricas são como Olá Manager de recursos de Cluster de recursos de infraestrutura de serviço gere consumo e capacidade Olá cluster. mais informações sobre as métricas de toolearn e como tooconfigure-las, consulte [neste artigo](service-fabric-cluster-resource-manager-metrics.md)
- Afinidade é um modo, que pode configurar para os serviços. Não é comum, mas se for necessário, pode saber [aqui](service-fabric-cluster-resource-manager-advanced-placement-rules-affinity.md)
- Existem várias regras de posicionamento diferentes que podem ser configuradas no seu serviço toohandle noutros cenários. Pode descobrir sobre as políticas de colocação diferentes [aqui](service-fabric-cluster-resource-manager-advanced-placement-rules-placement-policies.md)
- Partir do início de Olá e [obter uma introdução toohello Gestor de recursos de Cluster do Service Fabric](service-fabric-cluster-resource-manager-introduction.md)
- toofind saída sobre como Olá Gestor de recursos do Cluster gere e equilibra a carga no cluster de Olá, veja artigo Olá no [balanceamento de carga](service-fabric-cluster-resource-manager-balancing.md)
- Olá Gestor de recursos do Cluster tem muitas opções para descrever o cluster de Olá. toofind mais informações sobre os mesmos, consulte este artigo no [que descrevem um cluster do Service Fabric](service-fabric-cluster-resource-manager-cluster-description.md)
