---
title: "aaaCapacity planeamento para aplicações de Service Fabric | Microsoft Docs"
description: "Descreve como tooidentify Olá número de nós de computação necessária para uma aplicação de Service Fabric"
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: markfuss
editor: 
ms.assetid: 9fa47be0-50a2-4a51-84a5-20992af94bea
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: 44a69e9d8ec5efcc43122dc42e8f923ef37378f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="capacity-planning-for-service-fabric-applications"></a>Planeamento da capacidade para aplicações de Service Fabric
Este documento informa como tooestimate Olá a quantidade de recursos (CPU, RAM, armazenamento de disco) terá de toorun as suas aplicações Azure Service Fabric. É comum para sua toochange de requisitos de recursos ao longo do tempo. Normalmente, é necessário alguns recursos à medida que o serviço de desenvolve/teste e, em seguida, requerem mais recursos, vá para a produção e a sua aplicação cresce no popularidade. Ao conceber a sua aplicação, analisar os requisitos de longa duração Olá e certifique-opções que permitem que o pedido do cliente elevada tooscale toomeet o serviço.

 Quando cria um cluster do Service Fabric, decida que tipos de máquinas virtuais (VMs) constituem cluster Olá. Cada VM vem com uma quantidade limitada de recursos na forma de Olá de CPU (núcleos e velocidade), a largura de banda, RAM e armazenamento em disco. À medida que cresce o serviço ao longo do tempo, pode atualizar tooVMs que oferecem maiores recursos e/ou adicionar o cluster de tooyour mais VMs. Olá de toodo anterior será ignorada, a tem architect seu serviço inicialmente, de modo que pode tirar partido das novas VMs adicionadas dinamicamente toohello cluster.

Alguns serviços gerem dados toono pouca Olá VMs. Por conseguinte, para estes serviços devem focar-se principalmente no desempenho, o que significa selecionar Olá o planeamento de capacidade adequado CPU (núcleos e velocidade) de Olá VMs. Além disso, deve considerar a largura de banda de rede, incluindo a frequência das transferências de rede estão a ocorrer e está a ser transferida a quantidade de dados. Se o serviço necessitar tooperform bem à medida que aumenta de utilização do serviço, pode adicionar o cluster de toohello VMs mais e a carga de pedidos de rede do saldo Olá em todas as VMs de Olá.

Para os serviços que gerem grandes quantidades de dados em Olá VMs, planeamento de capacidade deve focar-se principalmente nas tamanho. Assim, deve considerar cuidadosamente a capacidade de Olá de armazenamento de RAM e o disco da VM Olá. sistema de gestão de memória virtual Olá no Windows faz com que o espaço em disco aspeto RAM tooapplication código. Além disso, o tempo de execução do Service Fabric Olá fornece manter apenas os dados na memória e mover toodisk de dados amovíveis Olá a paginação inteligente. As aplicações, por conseguinte, podem utilizar mais memória do que é fisicamente disponível no Olá VM. Basta ter mais RAM aumenta a desempenho, uma vez que Olá VM pode manter mais armazenamento em disco na RAM. Olá VM selecionar deve ter um disco toostore suficientemente grande Olá de dados que pretende ter nos Olá VM. Da mesma forma, Olá VM deve ter suficiente tooprovide de RAM, com Olá pretendidos ao nível de desempenho. Se o crescimentos de dados do serviço ao longo do tempo, pode adicionar mais VMs toohello cluster e partição Olá dados em todas as VMs de Olá.

## <a name="determine-how-many-nodes-you-need"></a>Determinar quantos nós é necessário
O serviço de criação de partições permite-lhe tooscale saída dados do seu serviço. Para obter mais informações sobre a criação de partições, consulte [criação de partições de Service Fabric](service-fabric-concepts-partitioning.md). Cada partição deve encaixar-se dentro de uma única VM, mas várias partições (pequenas) podem ser colocadas numa única VM. Por isso, ter mais partições pequenas dá-lhe uma maior flexibilidade ao ter alguns partições maior. compromisso de Olá é ter muitos partições aumenta a sobrecarga de Service Fabric e não é possível efetuar operações transacionadas em partições. É também mais tráfego de rede potenciais se código do serviço tem frequentemente tooaccess peças de dados que residem no partições diferentes. Ao conceber o seu serviço, deve considerar cuidadosamente estas tooarrive os profissionais de TI e contras numa estratégia de criação de partições efetiva.

Vamos assumir que a aplicação tem um único serviço com monitorização de estado que tem um tamanho de arquivo que pode esperar toogrow tooDB_Size GB do ano. São tooadd disposto mais aplicações (e as partições) como experiência crescimento além desse ano.  Olá replicação fator (RF), que determina o número de Olá de réplicas para os impactos de serviço Olá total DB_Size. Olá DB_Size total em todas as réplicas é Olá multiplicado pelo DB_Size de fator de replicação.  Node_Size representa o espaço de disco de Olá/RAM por nó pretende toouse para o seu serviço. Para melhor desempenho, Olá DB_Size deve caber na memória em cluster Olá e um Node_Size que está em torno Olá RAM de Olá que VM deve ser selecionada. Atribuindo um Node_Size que é maior do que Olá capacidade de RAM, são depender paginação Olá fornecida pelo tempo de execução do Olá Service Fabric. Assim, o desempenho pode não ser ideal se os dados completos são considerados a toobe acesso frequente (desde o Olá, em seguida, dados é bloco paginados/out). No entanto, para vários serviços onde é frequente apenas uma fração de dados de Olá, é mais económico.

número de Olá de nós é necessário para o máximo desempenho pode ser calculado da seguinte forma:

```
Number of Nodes = (DB_Size * RF)/Node_Size

```


## <a name="account-for-growth"></a>Conta para o crescimento
Poderá pretender toocompute Olá diversas nós com base no Olá DB_Size espera que o toogrow de serviço, além disso toohello DB_Size que começou com. Em seguida, aumente o número de Olá de nós à medida que cresce o serviço para que lhe é não sobre-aprovisionar número Olá de nós. Mas o número de Olá de partições deve ser baseado no número de Olá de nós que são necessários quando estiver a executar o serviço em crescimento máximo.

Este é boa toohave algumas máquinas adicionais disponíveis em qualquer altura, para que pode processar qualquer picos inesperados ou a falha (por exemplo, se algumas VMs ficarem Inativos).  Embora Olá capacidade extra deve ser determinada ao utilizar os picos de esperado, um ponto de partida é tooreserve algumas VMs adicionais (5-10 por cento adicional).

Olá anterior assume um único serviço com monitorização de estado. Se tiver mais do que um serviço com estado, terá tooadd Olá DB_Size associado Olá outros serviços em equação de Olá. Em alternativa, pode calcular o número de Olá de nós em separado para cada serviço com monitorização de estado.  O serviço poderá ter as réplicas ou as partições que não são balanced. Tenha em atenção que as partições podem também ter mais de dados que outras pessoas. Para obter mais informações sobre a criação de partições, consulte [artigo sobre as melhores práticas de criação de partições](service-fabric-concepts-partitioning.md). No entanto, hello equação anterior é partição e réplica agnóstico relativamente, porque o Service Fabric assegura que as réplicas de Olá são distribuídas entre nós Olá de forma otimizada.

## <a name="use-a-spreadsheet-for-cost-calculation"></a>Utilize uma folha de cálculo de cálculo do custo
Agora vamos colocar alguns números real na fórmula Olá. Um [folha de cálculo de exemplo](https://servicefabricsdkstorage.blob.core.windows.net/publicrelease/SF%20VM%20Cost%20calculator-NEW.xlsx) mostra como tooplan Olá capacidade para uma aplicação que contém três tipos de objetos de dados. Para cada objeto, iremos aproximada tamanho e objetos quantos que esperamos toohave. Podemos também selecionar réplicas quantos queremos de cada tipo de objeto. folha de cálculo de Olá calcula a quantidade total de Olá de toobe memória armazenada Olá cluster.

Em seguida, iremos introduzir um tamanho da VM e o custo mensal. Com base no tamanho da VM de Olá, folha de cálculo de Olá indica que Olá número mínimo de partições que tem de utilizar toosplit que se adeque ao seu toophysically dados em nós de Olá. Pode pretendidos ao nível um grande número de tooaccommodate partições que necessidades de tráfego de rede e computação específico da sua aplicação. folha de cálculo de Olá mostra o número de Olá de partições que estiver a gerir objetos de perfil de utilizador Olá aumentou de um toosix.

Agora, com base em todas estas informações, folha de cálculo de Olá mostra que fisicamente foi possível obter todos os dados de Olá com partições de Olá pretendida e as réplicas num cluster de nó de 26. No entanto, este cluster seria possível densely packed, pelo que poderá ser útil algumas falhas de nó de tooaccommodate nós adicionais e atualizações. folha de cálculo de Olá também mostra que ter mais do que 57 nós fornece nenhum valor adicional porque terá de nós vazios. Novamente, poderá ser útil toogo acima 57 nós mesmo assim falhas de nó tooaccommodate e atualizações. Pode otimizar Olá folha de cálculo toomatch necessidades específicas da sua aplicação.   

![Folha de cálculo de cálculo do custo][Image1]

## <a name="next-steps"></a>Passos seguintes
Veja [serviços de criação de partições de Service Fabric] [ 10] toolearn mais informações sobre o serviço de criação de partições.

<!--Image references-->
[Image1]: ./media/SF-Cost.png

<!--Link references--In actual articles, you only need a single period before hello slash-->
[10]: service-fabric-concepts-partitioning.md
