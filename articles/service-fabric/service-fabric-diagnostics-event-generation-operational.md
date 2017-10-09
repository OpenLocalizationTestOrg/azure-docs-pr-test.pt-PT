---
title: "aaaAzure canal do serviço de recursos de infraestrutura operacional | Microsoft Docs"
description: "Lista completa dos registos gerados em clusters do Olá operacional canal do Service Fabric do Azure."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/19/2017
ms.author: dekapur
ms.openlocfilehash: 358782420ed62b202d6a89fe0f200b5ef0384c9c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="operational-channel"></a>Canal operacional 

canal operacional Olá é constituído por registos de alto nível ações executadas pelo Service Fabric nos nós e o cluster. Quando o "diagnóstico" está ativado para um cluster, Olá agente de diagnóstico do Azure está implementada no seu cluster e, por predefinição, está configurado tooread nos registos do canal operacional Olá. Leia mais sobre como configurar Olá [agente de diagnóstico do Azure](service-fabric-diagnostics-event-aggregation-wad.md) configuração de diagnósticos de Olá toomodify do seu toopick de cluster mais registos ou os contadores de desempenho. 

## <a name="operational-channel-logs"></a>Registos de canal operacional 

Eis uma lista completa de registos fornecidos pelo Service Fabric no canal operacional Olá. 

| EventId | Nome | Origem (tarefas) | Nível |
| --- | --- | --- | --- |
| 25620 | NodeOpening | FabricNode | Informativo |
| 25621 | NodeOpenedSuccess | FabricNode | Informativo |
| 25622 | NodeOpenedFailed | FabricNode | Informativo |
| 25623 | NodeClosing | FabricNode | Informativo |
| 25624 | NodeClosed | FabricNode | Informativo |
| 25625 | NodeAborting | FabricNode | Informativo |
| 25626 | NodeAborted | FabricNode | Informativo |
| 29627 | ClusterUpgradeStart | CM | Informativo |
| 29628 | ClusterUpgradeComplete | CM | Informativo |
| 29629 | ClusterUpgradeRollback | CM | Informativo |
| 29630 | ClusterUpgradeRollbackComplete | CM | Informativo |
| 29631 | ClusterUpgradeDomainComplete | CM | Informativo |
| 23074 | ContainerActivated | Alojamento | Informativo |
| 23075 | ContainerDeactivated | Alojamento | Informativo |
| 29620 | ApplicationCreated | CM | Informativo |
| 29621 | ApplicationUpgradeStart | CM | Informativo |
| 29622 | ApplicationUpgradeComplete | CM | Informativo |
| 29623 | ApplicationUpgradeRollback | CM | Informativo |
| 29624 | ApplicationUpgradeRollbackComplete | CM | Informativo |
| 29625 | ApplicationDeleted | CM | Informativo |
| 29626 | ApplicationUpgradeDomainComplete | CM | Informativo |
| 18566 | ServiceCreated | FM | Informativo |
| 18567 | ServiceDeleted | FM | Informativo |

## <a name="next-steps"></a>Passos seguintes

* Saiba mais sobre o global [geração de eventos ao nível da plataforma de Olá](service-fabric-diagnostics-event-generation-infra.md) no Service Fabric
* Modificar o [diagnósticos do Azure](service-fabric-diagnostics-event-aggregation-wad.md) configuração toocollect mais registos
* [Configurar o Application Insights](service-fabric-diagnostics-event-analysis-appinsights.md) toosee o canal operacional registos
