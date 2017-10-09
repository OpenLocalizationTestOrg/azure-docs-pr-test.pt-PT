---
title: "aaaDefragmentation das métricas no Service Fabric do Azure | Microsoft Docs"
description: "Uma descrição geral da utilização desfragmentação ou packing como uma estratégia de métricas no Service Fabric"
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: e5ebfae5-c8f7-4d6c-9173-3e22a9730552
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: d09045a6cf196d2771f1a0794637f4579d3eb96b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="defragmentation-of-metrics-and-load-in-service-fabric"></a>Desfragmentação de métricas e a carga no Service Fabric
estratégia de predefinição de Olá recursos de infraestrutura Cluster recursos do Service Manager para gerir as métricas de carga num cluster de Olá é toodistribute Olá em carga. Garantir que os nós estão uniformemente utilizados evita oportunidades de acesso frequente e amovíveis que levar a contenção de tooboth e wasted recursos. Distribuição de cargas de trabalho no cluster de Olá também é Olá esta em termos de reiniciadas falhas, uma vez que garante que uma falha não remova uma grande percentagem de uma carga de trabalho especificada. 

Olá Gestor de recursos de Cluster do serviço de recursos de infraestrutura suporta uma estratégia de diferentes para gerir a carga, o que é a desfragmentação. Desfragmentação significa que, em vez de tentar a utilização de Olá toodistribute de uma métrica de cluster Olá, este é consolidado. Consolidação é apenas um inversion da predefinição de Olá balanceamento estratégia – em vez de minimizar Olá desvio-padrão médio de métrica de carga, Olá Gestor de recursos de Cluster tenta tooincrease-lo.

## <a name="when-toouse-defragmentation"></a>Quando a desfragmentação de toouse
Distribuição de carga num cluster de Olá consome alguns dos recursos de Olá em cada nó. Algumas cargas de trabalho criar serviços que são exceptionally grandes e consumam a maior parte ou a totalidade de um nó. Nestes casos, é possível que quando existem grandes cargas de trabalho ser criadas não é suficiente espaço em qualquer nó toorun-los. Um problema no Service Fabric; não são de grandes cargas de trabalho no Olá casos Gestor de recursos do Cluster determina que necessita de espaço de toomake do tooreorganize Olá cluster para este grande carga de trabalho. No entanto, Olá entretanto que carga de trabalho tem toobe toowait agendada no cluster de Olá.

Se existirem vários serviços e estado toomove em torno, em seguida, pode demorar muito tempo para Olá grande carga de trabalho toobe colocado em cluster Olá. Isto é mais provável se outras cargas de trabalho no cluster de Olá também são grandes e, por isso, demorar mais longo tooreorganize. equipa de Service Fabric Olá medida tempos de criação no simulações deste cenário. Detetámos que demorou muito mais criar serviços grande assim que a utilização do cluster obteve acima entre 30% e 50%. toohandle neste cenário, introduzimos desfragmentação como uma estratégia de balanceamento. Detetámos que para grandes cargas de trabalho, especialmente aqueles em que a hora de criação foi importante, desfragmentação realmente ajudou a estas novas cargas de trabalho obterem agendadas no cluster de Olá.

Pode configurar a desfragmentação métricas toohave Olá carga do Gestor de recursos do Cluster tooproactively tente toocondense Olá dos serviços de Olá em menos de nós. Isto ajuda a garantir que existe quase sempre espaço para grandes serviços sem reorganizar cluster Olá. Não ter clusters de Olá tooreorganize permite criar rapidamente grandes cargas de trabalho.

A maioria das pessoas não precisam de desfragmentação. Os serviços são normalmente ser pequeno, pelo que não é do espaço de disco rígido toofind para-los num cluster de Olá. Quando a reorganização for possível, passa rapidamente, novamente porque a maioria dos serviços são pequenas e pode ser movida rapidamente e em paralelo. No entanto, se tem os serviços de grande e precisar deles criado rapidamente Olá estratégia de desfragmentação é que o utilizador. Vamos abordar fala Olá da utilização de desfragmentação seguinte. 

## <a name="defragmentation-tradeoffs"></a>Desfragmentação fala
Desfragmentação pode aumentar impactfulness de falhas, uma vez que mais serviços estão em execução em nós que não obedeçam a. Desfragmentação também pode aumentar os custos, uma vez que os recursos num cluster de Olá tem de ser contidos num reserva, a aguardar a criação de Olá de grandes cargas de trabalho.

Olá diagrama a seguir fornece uma representação visual de dois clusters, um que é defragmented e outro que não se encontra. 

<center>
![Comparar balanceamento e Defragmented Clusters][Image1]
</center>

No caso de Olá balanceado, considere o número de Olá de movimentos que seriam necessário tooplace um Olá maiores de objectos de serviço. Num cluster de defragmented Olá, carga de trabalho grande Olá foi possível colocar em nós quatro ou cinco sem ter toowait para quaisquer outro toomove de serviços.

## <a name="defragmentation-pros-and-cons"></a>Os profissionais de desfragmentação e contras
Por isso, quais são esses outras fala conceptual? Segue-se uma tabela rápida de coisas toothink sobre:

| Profissionais de desfragmentação | Contras de desfragmentação |
| --- | --- |
| Permite a criação rápida dos serviços de grande |Carregar concentrates em menos nós, aumentando a contenção |
| Permite reduzir o movimento de dados durante a criação |Falhas podem afetar mais serviços e fazer com que mais de volume de alterações |
| Permite avançada descrição dos requisitos e recuperação de espaço |Configuração de gestão de recursos mais complexa global |

Pode misturar defragmented e Olá de métricas normais no mesmo cluster. Olá Gestor de recursos de Cluster tenta tooconsolidate Olá desfragmentação métricas quanto possível durante propagando-se Olá outras pessoas. resultados de Olá de balanceamento de estratégias e a combinação de desfragmentação depende de vários fatores, incluindo:
  - número de Olá de balanceamento de métricas vs número Olá das métricas de desfragmentação
  - Se o serviço utiliza ambos os tipos de métricas 
  - ponderações métrica Olá
  - carrega métrica atual
  
Experimentação é necessário toodetermine Olá configuração exata necessária. Recomendamos a medida de detalhado das cargas de trabalho antes de ativar as métricas de desfragmentação na produção. Isto é especialmente verdadeiro quando a combinação de desfragmentação e métricas equilibradas dentro Olá mesmo serviço. 

## <a name="configuring-defragmentation-metrics"></a>Configuração de desfragmentação de métricas
Configurar as métricas de desfragmentação é uma decisão global num cluster de Olá e métricas individuais podem ser selecionadas para desfragmentação. Olá fragmentos de configuração a seguir mostra como tooconfigure métricas de desfragmentação. Neste caso, "Metric1" está configurado como uma métrica de desfragmentação, enquanto "Metric2" continuará toobe balanceamento normalmente. 

ClusterManifest.xml:

```xml
<Section Name="DefragmentationMetrics">
    <Parameter Name="Metric1" Value="true" />
    <Parameter Name="Metric2" Value="false" />
</Section>
```

através de Clusterconfig para implementações autónomas ou Template do Azure alojada clusters:

```json
"fabricSettings": [
  {
    "name": "DefragmentationMetrics",
    "parameters": [
      {
          "name": "Metric1",
          "value": "true"
      },
      {
          "name": "Metric2",
          "value": "false"
      }
    ]
  }
]
```


## <a name="next-steps"></a>Passos seguintes
- Olá Gestor de recursos do Cluster tem opções de man para descrever o cluster de Olá. toofind mais informações sobre os mesmos, consulte este artigo no [que descrevem um cluster do Service Fabric](service-fabric-cluster-resource-manager-cluster-description.md)
- As métricas são como Olá Manager de recursos de Cluster de recursos de infraestrutura de serviço gere consumo e capacidade Olá cluster. mais informações sobre as métricas de toolearn e como tooconfigure-las, consulte [neste artigo](service-fabric-cluster-resource-manager-metrics.md)

[Image1]:./media/service-fabric-cluster-resource-manager-defragmentation-metrics/balancing-defrag-compared.png
