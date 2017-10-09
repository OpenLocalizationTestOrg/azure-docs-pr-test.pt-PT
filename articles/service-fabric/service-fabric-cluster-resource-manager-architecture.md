---
title: Arquitetura do Gestor de aaaResource | Microsoft Docs
description: "Uma descrição geral da arquitetura do Service Fabric Cluster Gestor de recursos."
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: 6c4421f9-834b-450c-939f-1cb4ff456b9b
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: 9ea80273d0566a2ac25143ada3662875656b57b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="cluster-resource-manager-architecture-overview"></a>Descrição geral da arquitetura de Gestor de recursos de cluster
Olá Gestor de recursos de Cluster do serviço de recursos de infraestrutura é um serviço central que é executado no cluster de Olá. Gere Estado Olá pretendida dos serviços de Olá num cluster de Olá, particularmente com relativamente tooresource consumo e quaisquer regras de posicionamento. 

toomanage Olá recursos no seu cluster Olá Gestor de recursos de Cluster do Service Fabric tem de ter vários tipos de informações:

- Serviços de que existem atualmente
- Cada serviço actual do (ou predefinido) consumo de recursos 
- capacidade de cluster restante Olá 
- capacidade de Olá de nós de Olá no cluster de Olá 
- quantidade de Olá de recursos que são consumidos em cada nó

consumo de recursos de Olá de um determinado serviço pode alterar ao longo do tempo e serviços, normalmente, se preocupar com mais do que um tipo de recurso. Nos vários serviços diferentes, podem existir ambos real recursos físicos e físicos a ser medidos. Serviços podem monitorizar as métricas físicas, como o consumo de memória e o disco. Mais frequentemente, os serviços podem se preocupar com métricas lógicas - coisas como "WorkQueueDepth" ou "TotalRequests". Métricas de lógicas e físicas podem ser utilizadas no Olá mesmo cluster. Métricas podem ser partilhadas em vários serviços ou estar serviço específico tooa específico.

## <a name="other-considerations"></a>Outras considerações
Olá proprietários e operadores de cluster Olá podem ser diferentes do Olá autores de serviços e de aplicações, ou em a são mínima Olá mesmo pessoas wearing hats diferentes. Quando desenvolver a sua aplicação sabe alguns aspetos sobre o que necessita. Tiver uma estimativa de Olá recursos irá consumir e como diferentes serviços devem ser implementados. Por exemplo, camada web de Olá tem toorun no toohello nós exposto à Internet, enquanto os serviços de base de dados de Olá não devem. Outro exemplo, os serviços web de Olá provavelmente estão restritos pelo CPU e da rede, ao cuidado dos serviços de camada de dados do Olá mais informações sobre o consumo de memória e o disco. No entanto, pessoa Olá processamento site em direto ou um incidente para que o serviço na produção, que está a gerir um serviço de atualização toohello tem um toodo tarefa diferente e necessita de ferramentas diferentes. 

Cluster de Olá e serviços são dinâmicos:

- número de Olá de nós no cluster de Olá pode aumentar e diminuir
- Nós de diferentes tamanhos e tipos podem ficar e aceda
- Os serviços podem ser criados, remover e alterar as respetivas alocações de recursos desejados e regras de colocação
- Outras operações de gestão de atualizações ou podem implementar através do cluster de Olá aplicação Olá nos níveis de infraestrutura
- Falhas podem acontecer em qualquer altura.

## <a name="cluster-resource-manager-components-and-data-flow"></a>Componentes de Gestor de recursos do cluster e o fluxo de dados
Olá Gestor de recursos do Cluster tem requisitos de Olá de tootrack de cada serviço e Olá o consumo de recursos por cada objecto de serviço dentro desses serviços. Olá Gestor de recursos do Cluster tem duas partes concetuais: agentes que são executadas em cada nó e um serviço com tolerância a falhas. agentes de Olá em cada nó de carga de controlar relatórios a partir de serviços, agregação-los e, periodicamente comunicá-los. Olá serviço Gestor de recursos de Cluster agrega todos os Olá as informações de agentes local Olá e reage com base na configuração atual.

Vamos ver Olá diagrama a seguir:

<center>
![Arquitetura de Balanceador de recursos][Image1]
</center>

Durante o tempo de execução, existem várias alterações que pode ter ocorrido. Por exemplo, vamos supor que quantidade de Olá dos recursos de alguns serviços consumam alterações, falham alguns serviços, e alguns nós associarem e deixam Olá cluster. Todas as alterações de Olá num nó são agregadas e enviadas periodicamente toohello Gestor de recursos do Cluster de serviço (1,2) onde que estão agregados novamente, analisados e armazenados. Cada alguns segundos, que observa alterações Olá e determina se são necessárias quaisquer ações do serviço (3). Por exemplo, pode reparar que foram adicionados alguns nós vazios toohello cluster. Como resultado,-decide toomove alguns nós toothose de serviços. Olá Gestor de recursos do Cluster foi também tenha em atenção que um determinado nó estiver sobrecarregado ou que determinados serviços tem falhou ou foi eliminados, libertando recursos noutro local.

Vamos observar Olá diagrama a seguir e ver o que acontece em seguida. Vamos diga esse gestor de recursos do Cluster de Olá determina que são necessárias alterações. Coordena com outras serviços (Olá específico Gestor de ativação pós-falha) toomake Olá necessárias alterações de sistema. Em seguida, Olá necessários são enviados toohello adequado nós (4). Por exemplo, vamos supor que o Olá Resource Manager reparado Nó5 foi sobrecarregado e, por isso, decidiu toomove serviço B tooNode4 Nó5. No final de Olá de reconfiguração Olá (5), o cluster de Olá este aspeto:

<center>
![Arquitetura de Balanceador de recursos][Image2]
</center>

## <a name="next-steps"></a>Passos seguintes
- Olá Gestor de recursos do Cluster tem muitas opções para descrever o cluster de Olá. toofind mais informações sobre os mesmos, consulte este artigo no [que descrevem um cluster do Service Fabric](./service-fabric-cluster-resource-manager-cluster-description.md)
- deveres primário Olá Cluster o Gestor de recursos do são reequilíbrio cluster Olá e impor regras de posicionamento. Para obter mais informações sobre como configurar estas comportamentos, consulte [balanceamento de cluster do Service Fabric](./service-fabric-cluster-resource-manager-balancing.md)

[Image1]:./media/service-fabric-cluster-resource-manager-architecture/Service-Fabric-Resource-Manager-Architecture-Activity-1.png
[Image2]:./media/service-fabric-cluster-resource-manager-architecture/Service-Fabric-Resource-Manager-Architecture-Activity-2.png
