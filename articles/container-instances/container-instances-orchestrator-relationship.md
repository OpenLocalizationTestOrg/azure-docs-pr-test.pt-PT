---
title: "Instâncias de contentor aaaAzure e orquestração de contentor"
description: "Compreender a forma como as instâncias de contentor do Azure interagir com orchestrators de contentor"
services: container-instances
documentationcenter: 
author: seanmck
manager: timlt
editor: 
tags: 
keywords: 
ms.assetid: 
ms.service: container-instances
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/24/2017
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: 69a39edc6f14d885c1ac300990ed1399002ccfee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-container-instances-and-container-orchestrators"></a>Instâncias de contentor do Azure e orchestrators de contentor

Devido ao respetivo tamanho pequeno e a orientação de aplicação, os contentores são adequados para ambientes de entrega seja ágil e arquiteturas de microsserviço. tarefa de Olá de automatizar e gerir um grande número de contentores e como eles interagem é conhecida como *orchestration*. Orchestrators contentor populares incluem Kubernetes, DC/OS e Docker Swarm, todos os que estão disponíveis no Olá [serviço de contentor Azure](https://docs.microsoft.com/azure/container-service/).

Instâncias de contentor do Azure fornece algumas das Olá básico de funcionalidades de plataformas de orquestração de agendamento, mas não abrange os serviços de valor mais alto de Olá que essas plataformas fornecem e na realidade podem ser complementares com os mesmos. Este artigo descreve âmbito Olá que processa as instâncias de contentor do Azure e como completa orchestrators contentor podem interagir com ele.

## <a name="traditional-orchestration"></a>Orquestração tradicional

definição do padrão de Olá da orquestração inclui Olá seguintes tarefas:

- **Agendamento**: dada uma imagem de contentor e um pedido de recurso, localizar uma máquina adequada no contentor de Olá que toorun.
- **Afinidade/Anti-affinity**: especificar que um conjunto de contentores deverão ser executadas próximas entre si (para um desempenho) ou suficientemente até que ponto apart (para disponibilidade).
- **Monitorização de estado de funcionamento**: ver para as falhas de contentor e automaticamente reprogramá-los.
- **Ativação pós-falha**: monitorizar o que está a ser executado em cada máquina e Reprogramar contentores de nós de toohealthy máquinas com falhas.
- **Dimensionamento**: Adicionar ou remover o pedido de toomatch de instâncias de contentor, manualmente ou automaticamente.
- **Rede**: forneça uma rede de sobreposição para coordenar contentores toocommunicate em várias máquinas de anfitrião.
- **Deteção do serviço**: Ativar contentores toolocate entre si automaticamente, mesmo que tal como mover entre computadores anfitriões e alterar os endereços IP.
- **Coordenado as atualizações de aplicações**: Gerir contentor atualizações tooavoid aplicação tempo e ativar a reversão se algo não bate certo.

## <a name="orchestration-with-azure-container-instances-a-layered-approach"></a>Orquestração com instâncias de contentor do Azure: uma abordagem em camadas

Instâncias de contentor do Azure permite tooorchestration uma abordagem em camadas, fornecendo todas Olá agendamento e as capacidades de gestão necessário toorun um único contentor, permitindo orchestrator tarefas de contentor de várias plataformas toomanage seguir.

Porque todos os Olá subjacente infraestrutura para instâncias de contentor é gerido pelo Azure, uma plataforma do orchestrator não precisa de tooconcern próprio com localizar uma máquina de anfitrião adequado no qual toorun um único contentor. elasticidade Olá da nuvem Olá garante que uma está sempre disponível. Em vez disso, o orchestrator Olá pode se focarem em tarefas de Olá que simplificam o desenvolvimento de Olá de arquiteturas de contentor multi, incluindo o dimensionamento e atualizações coordenadas.



## <a name="potential-scenarios"></a>Potenciais cenários

Enquanto a integração do orchestrator com instâncias de contentor do Azure é ainda nascent, iremos prevê que podem surgir alguns ambientes diferentes:

### <a name="orchestration-of-container-instances-exclusively"></a>Orquestração de instâncias de contentor de forma exclusiva

Pois começar rapidamente e faturado por Olá segundo, um ambiente com base no exclusivamente instâncias de contentor do Azure oferece iniciado Olá tooget de forma mais rápida e toodeal com cargas de trabalho altamente variáveis.

### <a name="combination-of-container-instances-and-containers-in-virtual-machines"></a>Combinação de instâncias de contentor e contentores nas máquinas virtuais

Para demoradas, cargas de trabalho estáveis, da orquestração contentores num cluster de máquinas virtuais dedicadas normalmente, será mais barata que executar Olá contentores mesmos com instâncias de contentor. No entanto, as instâncias de contentor oferecem uma excelente solução para rápida expansão e contracting toodeal da capacidade global com picos inesperados ou curta duração em utilização. Em vez de aumentar horizontalmente o número de Olá de máquinas virtuais no seu cluster, em seguida, implementar contentores adicionais dessas máquinas, Olá orchestrator pode simplesmente agendar contentores adicionais Olá utilizando as instâncias de contentor e eliminá-los quando forem não são necessários.

## <a name="sample-implementation-azure-container-instances-connector-for-kubernetes"></a>Implementação de exemplo: conector de instâncias de contentor do Azure para Kubernetes

toodemonstrate como plataformas de orquestração do contentor podem integrar com instâncias de contentor do Azure, podemos ter sido iniciado edifício um [conector de exemplo para Kubernetes][aci-connector-k8s]. 

Olá conector para Kubernetes mimics Olá [kubelet] [ kubelet-doc] ao registar como um nó com capacidade ilimitada e emissão criação Olá de [pods] [ pod-doc] como grupos de contentor em instâncias de contentor do Azure. 

<!-- ![ACI Connector for Kubernetes][aci-connector-k8s-gif] -->

Pode ser criados conectores para outras orchestrators que da mesma forma integrada com energia Olá de toocombine de primitivos do plataforma do orchestrator Olá API com velocidade de Olá e na simplicidade da gestão de contentores em instâncias de contentor do Azure.

> [!WARNING]
> Olá conector ACI para Kubernetes é *experimental* e não deve ser utilizado em produção.

## <a name="next-steps"></a>Passos seguintes

Criar o contentor do primeiro com instâncias de contentor do Azure utilizando o Olá [guia de introdução](container-instances-quickstart.md).

<!-- IMAGES -->
[aci-connector-k8s-gif]: ./media/container-instances-orchestrator-relationship/aci-connector-k8s.gif

<!-- LINKS -->
[aci-connector-k8s]: https://github.com/azure/aci-connector-k8s
[kubelet-doc]: https://kubernetes.io/docs/admin/kubelet/
[pod-doc]: https://kubernetes.io/docs/concepts/workloads/pods/pod/