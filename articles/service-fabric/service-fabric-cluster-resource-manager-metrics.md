---
title: "carga de microsserviço Azure aaaManage através de métricas | Microsoft Docs"
description: "Saiba mais sobre como métricas tooconfigure e utilização no Service Fabric toomanage service consumo de recursos."
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: 0d622ea6-a7c7-4bef-886b-06e6b85a97fb
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: 592dc749ce30683a1e439a702b7d0dc0a638276f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="managing-resource-consumption-and-load-in-service-fabric-with-metrics"></a>Gestão consumo de recursos e a carga no Service Fabric com a métrica
*Métricas* Olá recursos que o cuidado de serviços sobre e que são fornecidos por nós de Olá no cluster de Olá. Uma métrica é tudo o que pretende que o toomanage na ordem tooimprove monitor Olá um desempenho ou dos seus serviços. Por exemplo, poderá ver tooknow de consumo de memória se o serviço estiver sobrecarregado. Utilize outro é toofigure enviados se o serviço de Olá foi possível mover noutro local onde a memória é que inferior restritas na ordem tooget melhorar o desempenho.

Coisas como a utilização de memória, disco e CPU são exemplos de métricas. Estas métricas são métricas físicas, recursos que correspondam toophysical recursos num nó de Olá que necessitam de toobe gerido. Métricas também podem ser (e são geralmente) métricas lógicas. A métrica de lógica está coisas como "MyWorkQueueDepth" ou "MessagesToProcess" ou "TotalRecords". Métricas lógicas são definidas pela aplicação e indiretamente correspondem toosome consumo de recurso físico. Métricas lógicas são comuns porque pode ser difícil toomeasure e consumo de relatório de recursos físicos numa base por serviço. complexidade Olá de medição e elaboração de relatórios de métricas físicas é também por que motivo o Service Fabric fornece algumas nas métricas predefinidas.

## <a name="default-metrics"></a>Nas métricas predefinidas
Digamos que pretende que o tooget iniciado escrever e implementar o seu serviço. Neste momento, não sabe que recursos físicos ou lógicos que consome. Que é adequado! Olá Gestor de recursos de Cluster do serviço de recursos de infraestrutura utiliza algumas nas métricas predefinidas quando não existem outras métricas são especificadas. São:

  - PrimaryCount - contagem de réplicas primárias num nó de Olá 
  - ReplicaCount - contagem de totais réplicas com monitorização de estado do nó de Olá
  - Contagem - contagem de todos os objetos do serviço (sem monitorização de estado e com monitorização de estado) no nó de Olá

| Métrica | Carga de instância sem monitorização de estado | Carga secundária com monitorização de estado | Com monitorização de estado carga primária |
| --- | --- | --- | --- |
| PrimaryCount |0 |0 |1 |
| ReplicaCount |0 |1 |1 |
| Contagem |1 |1 |1 |

Para cargas de trabalho básicas, nas métricas predefinidas de Olá fornecem uma distribuição decent de trabalho no cluster de Olá. No seguinte exemplo de Olá, vamos ver o que acontece quando iremos criar dois serviços e baseiam-se nas métricas predefinidas de Olá para balanceamento. serviço primeiro Olá é um serviço com monitorização de estado com partições de três e definir o tamanho de três uma réplica de destino. serviço segundo Olá é um serviço sem monitorização de estado com uma partição e uma contagem de instâncias de três.

Eis o que obtém:

<center>
![Esquema de cluster com nas métricas predefinidas][Image1]
</center>

Toonote algumas coisas:
  - Réplicas principais de serviço com estado Olá estão distribuídas por vários nós
  - Réplicas para Olá mesma partição são em nós diferentes
  - número total de Olá de primaries e bases de dados secundárias é distribuído no cluster de Olá
  - número total de Olá de objetos de serviço é alocado uniformemente em cada nó

Boa!

nas métricas predefinidas de Olá great funcionam como um início. No entanto, nas métricas predefinidas de Olá irão apenas transportar, até ao momento. Por exemplo: o que é a probabilidade de Olá que a criação de partições de Olá esquema selecionado resultados no mesmo perfeitamente utilização por todas as partições? O que é a possibilidade de Olá Olá carga para um determinado serviço é constante ao longo do tempo, ou mesmo apenas Olá mesmo através de várias partições agora?

É possível executar com apenas Olá nas métricas predefinidas de. No entanto, se o fizer, normalmente, significa que a utilização do cluster inferior e mais desigual que gostaria de. Isto acontece porque Olá nas métricas predefinidas não é adaptável e presumem que tudo é equivalente. Por exemplo, um site primário que está ocupado e outro que não é ambas contribuem métrica de PrimaryCount toohello "1". Olá pior das hipóteses, utilizar apenas Olá nas métricas predefinidas de pode também originar de nós overscheduled, resultando em problemas de desempenho. Se estiver interessado em obter Olá a maioria das fora do seu cluster e evitar problemas de desempenho, terá de métricas personalizadas toouse e relatórios de carga dinâmico.

## <a name="custom-metrics"></a>Métricas personalizadas
As métricas são configuradas numa base por denominado-service-instância quando estiver a criar serviço Olá.

Qualquer métrica tem algumas propriedades que descrevem este: um nome, uma ponderação e uma carga predefinida.

* : Métrica Olá nome da métrica de Olá. o nome da métrica Olá é um identificador exclusivo para a métrica de Olá num cluster de Olá perspetiva Olá Resource Manager.
* Peso: Ponderação métrica define como importante esta métrica é relativo toohello outras métricas para este serviço.
* Carga de predefinição: carga predefinido de Olá é representada forma diferente dependendo se o serviço de Olá é sem monitorização de estado ou com monitorização de estado.
  * Para os serviços sem monitorização de estado, cada métrica tem uma propriedade de único com o nome DefaultLoad
  * Para definir os serviços com monitorização de estado:
    * PrimaryDefaultLoad: período desta métrica que este serviço consome quando for um site primário predefinido de Olá
    * SecondaryDefaultLoad: período desta métrica que este serviço consome quando for uma secundária predefinido de Olá

> [!NOTE]
> Se definir métricas personalizadas e pretender nas métricas predefinidas de too_also_ utilize Olá, terá de too_explicitly_ adicionar nas métricas predefinidas de Olá criar e definem ponderações e valores para os mesmos. Isto acontece porque tem de definir relação Olá entre Olá nas métricas predefinidas e as métricas personalizadas. Por exemplo, talvez que mais lhe interessam ConnectionCount ou WorkQueueDepth mais do que a distribuição primária. Por ponderação de Olá predefinido de Olá PrimaryCount métrica é elevado, pelo que pretende tooreduce-tooMedium quando adicionar o seu tooensure métricas que têm precedência.
>

### <a name="defining-metrics-for-your-service---an-example"></a>Definir métricas para o seu serviço - um exemplo
Vamos supor que quiser Olá a seguinte configuração:

  - O serviço de relatórios uma métrica com o nome "ConnectionCount"
  - Também deve nas métricas predefinidas de toouse Olá 
  - Tiver terminado algumas medidas e saber o que normalmente uma réplica primária do que o serviço demora 20 unidades de "ConnectionCount"
  - Bases de dados secundárias utilizam 5 unidades de "ConnectionCount"
  - Sabe que "ConnectionCount" é a métrica mais importante de Olá em termos de gerir o desempenho de Olá deste serviço específico
  - Pretender continuar com balanceamento de réplicas primárias. Balanceamento de réplicas primárias geralmente é uma boa ideia, independentemente da que. Isto ajuda a evitar a perda de Olá de algumas domínio nó ou falhas de afetar a maioria das réplicas primárias juntamente com o mesmo. 
  - Caso contrário, nas métricas predefinidas de Olá estejam funcionais

Eis o código de Olá que seria a escrever toocreate um serviço com que a configuração da métrica:

Código:

```csharp
StatefulServiceDescription serviceDescription = new StatefulServiceDescription();
StatefulServiceLoadMetricDescription connectionMetric = new StatefulServiceLoadMetricDescription();
connectionMetric.Name = "ConnectionCount";
connectionMetric.PrimaryDefaultLoad = 20;
connectionMetric.SecondaryDefaultLoad = 5;
connectionMetric.Weight = ServiceLoadMetricWeight.High;

StatefulServiceLoadMetricDescription primaryCountMetric = new StatefulServiceLoadMetricDescription();
primaryCountMetric.Name = "PrimaryCount";
primaryCountMetric.PrimaryDefaultLoad = 1;
primaryCountMetric.SecondaryDefaultLoad = 0;
primaryCountMetric.Weight = ServiceLoadMetricWeight.Medium;

StatefulServiceLoadMetricDescription replicaCountMetric = new StatefulServiceLoadMetricDescription();
replicaCountMetric.Name = "ReplicaCount";
replicaCountMetric.PrimaryDefaultLoad = 1;
replicaCountMetric.SecondaryDefaultLoad = 1;
replicaCountMetric.Weight = ServiceLoadMetricWeight.Low;

StatefulServiceLoadMetricDescription totalCountMetric = new StatefulServiceLoadMetricDescription();
totalCountMetric.Name = "Count";
totalCountMetric.PrimaryDefaultLoad = 1;
totalCountMetric.SecondaryDefaultLoad = 1;
totalCountMetric.Weight = ServiceLoadMetricWeight.Low;

serviceDescription.Metrics.Add(connectionMetric);
serviceDescription.Metrics.Add(primaryCountMetric);
serviceDescription.Metrics.Add(replicaCountMetric);
serviceDescription.Metrics.Add(totalCountMetric);

await fabricClient.ServiceManager.CreateServiceAsync(serviceDescription);
```

PowerShell:

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceTypeName –Stateful -MinReplicaSetSize 3 -TargetReplicaSetSize 3 -PartitionSchemeSingleton –Metric @("ConnectionCount,High,20,5”,"PrimaryCount,Medium,1,0”,"ReplicaCount,Low,1,1”,"Count,Low,1,1”)
```

> [!NOTE]
> Olá acima exemplos e hello rest deste documento descrevem as métricas de gestão numa base por-nome-service. Também é possível toodefine métricas para os serviços no serviço de Olá _tipo_ nível. Isto é conseguido através da especificação-los no seu manifestos de serviço. Definir as métricas de nível de tipo não é recomendada por vários motivos. motivo primeiro Olá é que os nomes de métricos são frequentemente específico do ambiente. A menos que exista um contrato sólido no local, não é possível não se esqueça de que métrica Olá "Núcleos" no um ambiente não se encontra "MiliCores" ou "Núcleos" em outras pessoas. Se as métricas são definidas no seu manifesto tem toocreate manifestos novo por ambiente. Normalmente, isto leva tooa proliferação de manifestos diferentes com apenas diferenças menores, que podem levar toomanagement dificuldades.  
>
> Métricas cargas normalmente são atribuídas numa base por-nome--instância de serviço. Por exemplo, vamos supor que cria uma instância de Olá service para CustomerA quem planos toouse apenas ligeiramente. Também Digamos que criar outro para CustomerB que tenha uma maior carga de trabalho. Neste caso, provavelmente, seria aconselhável predefinido de Olá tootweak carrega para esses serviços. Se tiver métricas e carrega definida através de manifestos e quiser toosupport neste cenário, requer diferentes aplicações e tipos de serviço para cada cliente. os valores de Olá definidos no momento de criação do serviço substituem as definido no manifesto de Olá, pelo que pode utilizar essa tooset Olá específico as predefinições de. No entanto, se o fizer que faz com que os valores de Olá declarados na correspondência de toonot Olá manifestos que esses Olá, na verdade, é executado o serviço com. Isto pode levar tooconfusion. 
>

Como um lembrete: Se pretender apenas nas métricas predefinidas de toouse Olá, não precisa de coleção de métricas de Olá tootouch de todo ou fazer nada especiais ao criar o seu serviço. nas métricas predefinidas de Olá obterem utilizadas automaticamente quando não existem outros são definidos. 

Agora, vamos através de cada uma destas definições em mais detalhe e falar sobre o comportamento de Olá que afeta.

## <a name="load"></a>Carregar
Olá ponto todo de definir a métrica é toorepresent algumas carga. *Carga* é a quantidade de uma determinada métrica é consumido por algumas instâncias de serviço ou a réplica de um determinado nó. Carga pode ser configurada em praticamente qualquer momento. Por exemplo:

  - Carga pode ser definida quando é criado um serviço. Esta opção é denominada _carga predefinido_.
  - carrega as informações das métricas Olá, incluindo o predefinido, para um serviço podem ser atualizados depois do serviço de Olá é criado. Esta opção é denominada _atualizar um serviço_. 
  - Olá cargas para uma determinada partição podem ser reposição toohello os valores predefinidos, para que o serviço. Esta opção é denominada _repor a carga da partição_.
  - Pode ser comunicada carga num por base do objeto de serviço dinamicamente durante o tempo de execução. Esta opção é denominada _reporting carga_. 
  
Todas estas estratégias podem ser utilizadas dentro Olá mesmo service longo da respetiva duração. 

## <a name="default-load"></a>Carga predefinido
*Predefinição carga* é a quantidade de métrica de Olá consome de cada objeto de serviço (instância sem monitorização de estado ou réplica com monitorização de estado) deste serviço. Olá Gestor de recursos de Cluster utiliza este número para a carga Olá do objeto de serviço Olá até receber outras informações, tais como um relatório de carga dinâmico. Para serviços mais simples, a carga de predefinição Olá é uma definição de estática. o carregamento da predefinição Olá nunca é atualizado e é utilizado para a duração de Olá do serviço de Olá. Predefinição carrega ótimo funciona para cenários em que determinados quantidades de recursos dedicado toodifferent cargas de trabalho e não alteram o planeamento de capacidade simple.

> [!NOTE]
> Para obter mais informações sobre a gestão de capacidade e definir as capacidades para nós de Olá no seu cluster, consulte [neste artigo](service-fabric-cluster-resource-manager-cluster-description.md#capacity).
> 

Olá Gestor de recursos de Cluster permite toospecify de serviços com monitorização de estado de carga predefinido diferente Primaries e secundárias. Serviços sem monitorização de estado só podem especificar um valor que se aplica tooall instâncias. Para os serviços com monitorização de estado, carga de predefinição Olá para réplicas principais e secundários são normalmente diferentes, uma vez que as réplicas fazer diferentes tipos de trabalho em cada função. Por exemplo, Primaries normalmente servir leituras e escritas e lidar com a maior parte da carga de computacional Olá, enquanto não secundárias. Normalmente, a carga de predefinição Olá para uma réplica primária é superior ao Olá predefinido de carga para as réplicas secundárias. Olá real números deve dependem os seus próprios valores.

## <a name="dynamic-load"></a>Carga dinâmico
Imaginemos que tiver sido a executar o seu serviço de tempo. Com alguns monitorização, ter reparado que:

1. Algumas partições ou instâncias de um determinado serviço consumam mais recursos do que outras pessoas
2. Alguns serviços tem carga varia ao longo do tempo.

Há muitos coisas que pode fazer com que estes tipos de flutuações de carga. Por exemplo, diferentes serviços ou partições estão associadas a diferentes clientes com requisitos diferentes. Também pode alterar a carga porque a quantidade de Olá de serviço do trabalho Olá varia decorrer Olá do dia de Olá. Independentemente da razão de Olá, normalmente, não há nenhum número único que pode utilizar para a predefinição. Isto é particularmente verdadeiro se quiser tooget Olá mais utilização fora do cluster de Olá. Qualquer valor que escolha para a carga de predefinição está errada algumas das tempo Olá. Predefinição incorreta carrega resultará na Olá Gestor de recursos do Cluster de ativação pós-falha ou em alocar recursos. Como resultado, tiver nós que são através de ou em utilizados, apesar de Olá Gestor de recursos do Cluster pensa balanceamento de cluster Olá. Predefinição são ainda boa, uma vez que fornecem algumas informações para colocação inicial, mas não ainda é um bloco completo para cargas de trabalho reais. captura tooaccurately alterar os requisitos de recursos, Olá Gestor de recursos de Cluster permite que cada tooupdate de objeto de serviço própria carga durante o tempo de execução. Esta opção é denominada relatórios de carga dinâmico.

Relatórios de carga dinâmico permitir que as réplicas ou instâncias tooadjust respetiva carga comunicadas/alocação de métricas ao longo da respetiva duração. Uma réplica de serviço ou a instância que foi frio e não efetuar qualquer trabalho normalmente reportarão que estava a utilizar baixas quantidades de uma métrica indicada. Uma réplica ocupada ou instância reportarão que estão a utilizar mais.

Carga por réplica ou de instância de relatórios permite Olá tooreorganize do Gestor de recursos do Cluster de objetos do serviço de individuais Olá num cluster de Olá. Reorganizar serviços Olá ajuda a garantir a obtêm recursos Olá necessitam. Serviços ocupados eficazmente obter demasiado "recuperar" recursos a partir de outros as réplicas ou instâncias que estão atualmente frio ou fazer menos trabalho.

Dentro do Reliable Services, carga de tooreport Olá código dinamicamente este aspeto:

Código:

```csharp
this.Partition.ReportLoad(new List<LoadMetric> { new LoadMetric("CurrentConnectionCount", 1234), new LoadMetric("metric1", 42) });
```

Um serviço pode comunicar em qualquer uma das métricas de Olá definidas para o mesmo no momento de criação. Se uma carga de relatórios do serviço para uma métrica de que não seja configurado toouse, o Service Fabric ignora desse relatório. Se existirem outras métricas comunicadas num Olá mesmo tempo que sejam válidos, esses relatórios são aceites. Código do serviço pode medir e gerar relatórios Olá todas as métricas que confie como, e operadores podem especificar Olá configuração da métrica toouse sem ter de código do serviço toochange Olá. 

### <a name="updating-a-services-metric-configuration"></a>Atualizar a configuração de métrica de um serviço
lista Olá das métricas associados ao serviço de Olá, e propriedades Olá desses métricas podem ser atualizadas dinamicamente, enquanto serviço Olá está em direto. Isto permite a experimentação e flexibilidade. Alguns exemplos de quando isto é útil são:

  - desativar uma métrica com um relatório buggy para um serviço específico
  - reconfiguração Olá ponderações de métricas com base no comportamento pretendido
  - Ativar uma métrica de novo, apenas depois de código Olá já foi implementado e validar através de outros mecanismos
  - alterar Olá predefinido de carga para um serviço com base no comportamento observado e consumo

Olá principais APIs para alterar a configuração da métrica são `FabricClient.ServiceManagementClient.UpdateServiceAsync` em c# e `Update-ServiceFabricService` no PowerShell. Qualquer informação especificar com estas APIs substitui Olá existente as informações das métricas para o serviço de Olá imediatamente. 

## <a name="mixing-default-load-values-and-dynamic-load-reports"></a>A combinação de valores de carga predefinido e os relatórios de carga dinâmico
Carga predefinido e carrega dinâmica pode ser utilizadas para Olá mesmo serviço. Quando utiliza um serviço de carregamento predefinido e relatórios de carga dinâmico, carga predefinido funciona como uma estimativa até apareçam relatórios dinâmicos. Carregamento predefinido é boa porque proporciona Olá Gestor de recursos do Cluster algo toowork com. carga de predefinição Olá permite Olá tooplace do Gestor de recursos do Cluster de objetos do serviço Olá em localizações boas quando forem criados. Se não existem informações de carga predefinido, colocação dos serviços é efetivamente aleatória. Quando a carga relatórios chegam mais tarde colocação aleatório inicial de Olá é frequentemente errada e Olá Gestor de recursos do Cluster tem toomove serviços.

Vamos colocar o nosso exemplo anterior e ver o que acontece quando adicionamos alguns métricas personalizadas e, em seguida, relatórios de carga dinâmico. Neste exemplo, utilizamos "MemoryInMb" como uma métrica de exemplo.

> [!NOTE]
> Memória é uma das métricas de sistema de Olá Service Fabric pode [recursos governar](service-fabric-resource-governance.md), e relatórios por si é normalmente difícil. Não, na verdade, esperamos que tooreport no consumo de memória Memória é utilizado aqui como um toolearning ajuda sobre as capacidades de Olá de Olá Gestor de recursos do Cluster.
>

Vamos presumem que criámos inicialmente serviço com estado Olá com Olá os seguintes comandos:

PowerShell:

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceTypeName –Stateful -MinReplicaSetSize 3 -TargetReplicaSetSize 3 -PartitionSchemeSingleton –Metric @("MemoryInMb,High,21,11”,"PrimaryCount,Medium,1,0”,"ReplicaCount,Low,1,1”,"Count,Low,1,1”)
```

Como um lembrete, esta sintaxe é ("MetricName MetricWeight, PrimaryDefaultLoad, SecondaryDefaultLoad").

Vamos ver que um esquema de cluster possíveis pode ter o seguinte aspeto:

<center>
![Cluster equilibrado com métricas predefinidos e personalizados][Image2]
</center>

Algumas coisas que são vale a pena realçar:

* Cada réplicas secundárias dentro de uma partição podem ter as seus próprios carga
* Em geral métricas Olá parecer equilibradas. Para memória, Olá rácio entre Olá máxima e mínima de carga é 1.75 (nó Olá com Olá mais carga é N3, Olá pelo menos, N2 e 28/16 = 1.75).

Existem algumas coisas que ainda temos tooexplain:

* O que determinou que o se um rácio de 1.75 foi razoável, ou não? Como Olá Gestor de recursos do Cluster saber se isto for suficientemente boa ou se houver mais toodo de trabalho?
* Quando balanceamento acontecer?
* O que, significa que memória foi ponderada "Alto"?

## <a name="metric-weights"></a>Métricas ponderações
Controlo Olá mesmo métricas em diferentes serviços é importante. Se a vista global é o que permite Olá consumo de tootrack do Gestor de recursos de Cluster no cluster de Olá, balancear consumo em nós e certifique-se de que nós não passam capacidade. No entanto, os serviços podem ter vistas diferentes como toohello importância de Olá métrica do mesma. Além disso, num cluster com várias métricas e muitos dos serviços, perfeitamente com balanceamento de soluções podem não existir para todas as métricas. Como é que Olá Gestor de recursos de Cluster deve processar estas situações?

Métricas ponderações permitem Olá toodecide do Gestor de recursos do Cluster como toobalance Olá cluster quando não existe nenhuma resposta perfeita. Métricas ponderações também permitem Olá toobalance do Gestor de recursos do Cluster serviços específicos diferente. Métricas podem ter quatro níveis diferente ponderação: Zero, baixa, média e alta. Uma métrica com uma ponderação igual a zero contribui nada quando ponderar se as coisas são equilibradas ou não. No entanto, a sua carga ainda contribuir toocapacity gestão. Métricas com Zero ponderação são ainda úteis e são frequentemente utilizadas como parte do comportamento de serviço e a monitorização do desempenho. [Este artigo](service-fabric-diagnostics-event-generation-infra.md) fornece mais informações sobre a utilização de Olá de métricas para monitorização e diagnóstico dos seus serviços. 

impacto real de Olá de peso de métrico diferentes no cluster de Olá é que essa Olá Gestor de recursos do Cluster gera diferentes soluções. Métricas ponderações dizer Olá Gestor de recursos de Cluster que determinadas métricas são mais importantes do que outras pessoas. Quando não existe nenhum Olá solução perfeita Gestor de recursos do Cluster pode preferir soluções que equilibrar Olá superiores ponderado métricas melhor. Se um serviço pensa uma métrica específica é indiferente, que pode considerar a utilização dos que métrica imbalanced. Isto permite que outro serviço tooget uma distribuição, mesmo que alguns métrica que é importante tooit.

Vamos ver um exemplo de alguns relatórios de carga e a métrica de forma diferente ponderações resulta em alocações diferentes no cluster de Olá. Neste exemplo, Vemos que mudar o peso relativo de Olá das métricas de Olá faz com que Olá toocreate do Gestor de recursos de Cluster diferentes disposição dos serviços.

<center>
![Exemplo de métrica de ponderação e o seu impacto em soluções de balanceamento][Image3]
</center>

Neste exemplo, existem quatro diferentes serviços, todos os valores de diferentes relatórios dois diferentes com base nas métricas, MetricA e MetricB. Um cenário, todos os serviços de Olá definem MetricA é mais importante Olá (peso = alta) e MetricB como indiferente (peso = baixa). Como resultado, Vemos que Olá Gestor de recursos de Cluster coloca serviços Olá, de modo a que MetricA melhor com balanceamento de MetricB. "Melhor equilibrada" significa que MetricA tem um inferior tem um desvio-padrão inferior que MetricB. No segundo caso Olá, iremos inverter ponderações métrica Olá. Como resultado, Olá Gestor de recursos do Cluster trocas serviços A e B toocome cópias de segurança com uma alocação onde MetricB é melhor com balanceamento de MetricA.

> [!NOTE]
> Métricas ponderações determinam como deve equilibrar Olá Gestor de recursos do Cluster, mas não quando balanceamento deverá ocorrer. Para obter mais informações sobre balanceamento, veja [neste artigo](service-fabric-cluster-resource-manager-balancing.md)
>

### <a name="global-metric-weights"></a>Ponderações métricas global
Digamos ServiceA define MetricA como importância alta e ServiceB define ponderação Olá para MetricA tooLow ou Zero. O que é o peso de real Olá que acaba por ficar obter utilizado?

Existem vários ponderações que são controladas por cada métrica. peso da primeira Olá é Olá definido para a métrica de Olá quando o serviço de Olá é criado. Olá outra ponderação é uma ponderação global, que é calculada automaticamente. Olá Gestor de recursos de Cluster utiliza ambas estas ponderações quando a classificação de soluções. Tendo ambas as ponderações em consideração é importante. Isto permite Olá toobalance do Gestor de recursos de Cluster em cada serviço tooits de acordo com as prioridades de proprietário e certifique-se também desse cluster Olá como um todo está alocado corretamente.

O que aconteceria mediante Olá Gestor de recursos do Cluster não se preocupar com saldo global e local? Bem, é fácil tooconstruct soluções que são equilibrados globalmente, mas que resultar no equilíbrio de recursos fraca para serviços individuais. No seguinte exemplo de Olá, vamos observar um serviço configurado com apenas nas métricas predefinidas Olá e ver o que acontece quando apenas saldo global é considerado:

<center>
![Olá impacto de uma solução apenas Global][Image4]
</center>

No exemplo superior Olá baseado apenas saldo global, cluster Olá como um todo, de facto, é balanceado. Todos os nós têm Olá mesmo número de primaries e Olá mesmo número de réplicas totais. No entanto, se observar impacto real Olá esta atribuição não é por isso, boa: perda de Olá de qualquer nó afeta uma carga de trabalho específica disproportionately, porque demora enviados todos os respetivos primaries. Por exemplo, se o primeiro nó de Olá falhar primaries de três Olá para partições diferentes três Olá de Olá serviço círculo todas seria perdida. Por outro lado, Olá triângulo e serviços de Hexagon têm as respetivas partições perder uma réplica. Isto faz com que sem interrupção, que não sejam ter toorecover Olá para baixo de réplica.

Exemplo de inferior Olá, Olá Gestor de recursos do Cluster tiver distribuído réplicas Olá com base em ambos os saldo de Olá global e por serviço. Quando se calcular a classificação de Olá da solução de Olá proporciona maior parte da solução global do Olá ponderação toohello e os serviços de tooindividual uma parte (configurável). Saldo global para uma métrica é calculado com base em média Olá de peso de métrica de Olá de cada serviço. De acordo com tooits própria definido métrica ponderações é com balanceamento de cada serviço. Isto garante que os serviços de Olá são equilibrados dentro próprios de acordo com tootheir necessidades próprias. Como resultado, se hello mesmo primeiro nó falhar falha Olá é distribuído por todas as partições de todos os serviços. Olá impacto tooeach é Olá mesmo.

## <a name="next-steps"></a>Passos seguintes
- Para obter mais informações sobre como configurar os serviços, [Saiba mais sobre como configurar serviços](service-fabric-cluster-resource-manager-configure-services.md)(service-fabric-cluster-resource-manager-configure-services.md)
- Definir métricas de desfragmentação é tooconsolidate unidirecional carga em nós em vez de propagando-se este. toolearn como tooconfigure desfragmentação, consulte demasiado[neste artigo](service-fabric-cluster-resource-manager-defragmentation-metrics.md)
- toofind saída sobre como Olá Gestor de recursos do Cluster gere e equilibra a carga no cluster de Olá, veja artigo Olá no [balanceamento de carga](service-fabric-cluster-resource-manager-balancing.md)
- Partir do início de Olá e [obter uma introdução toohello Gestor de recursos de Cluster do Service Fabric](service-fabric-cluster-resource-manager-introduction.md)
- O custo de movimento é uma forma de sinalização toohello Gestor de recursos de Cluster que determinados serviços são mais dispendioso toomove que outros. toolearn mais informações sobre o custo de movimento, consulte demasiado[neste artigo](service-fabric-cluster-resource-manager-movement-cost.md)

[Image1]:./media/service-fabric-cluster-resource-manager-metrics/cluster-resource-manager-cluster-layout-with-default-metrics.png
[Image2]:./media/service-fabric-cluster-resource-manager-metrics/Service-Fabric-Resource-Manager-Dynamic-Load-Reports.png
[Image3]:./media/service-fabric-cluster-resource-manager-metrics/cluster-resource-manager-metric-weights-impact.png
[Image4]:./media/service-fabric-cluster-resource-manager-metrics/cluster-resource-manager-global-vs-local-balancing.png
