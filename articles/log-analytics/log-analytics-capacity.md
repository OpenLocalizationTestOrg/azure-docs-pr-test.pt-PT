---
title: "aaaCapacity e solução de desempenho no Log Analytics do Azure | Microsoft Docs"
description: "Olá utilize capacidade e a solução de desempenho no toohelp de análise de registos que compreende Olá capacidade dos seus servidores de Hyper-V."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: 51617a6f-ffdd-4ed2-8b74-1257149ce3d4
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: banders
ms.openlocfilehash: c47bb1e8bb9d4460b0241e89a616f3b356844b08
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="plan-hyper-v-virtual-machine-capacity-with-hello-capacity-and-performance-solution-preview"></a>Planear a capacidade de máquina virtual de Hyper-V com Olá capacidade e a solução de desempenho (pré-visualização)

![Símbolo de capacidade e o desempenho](./media/log-analytics-capacity/capacity-solution.png)

Pode utilizar Olá capacidade e a solução de desempenho no toohelp de análise de registos que compreende Olá capacidade dos seus servidores de Hyper-V. solução Olá fornece informações para o seu ambiente de Hyper-V para mostrar Olá utilização geral (CPU, memória e o disco) de anfitriões de Olá e Olá VMs em execução nesses anfitriões Hyper-V. As métricas são recolhidas para a CPU, memória e discos em todos os anfitriões e VMs Olá-los em execução.

solução Olá:

-   Mostra os anfitriões com maior e mais baixa utilização da CPU e memória
-   Mostra as VMs com maior e mais baixa utilização da CPU e memória
-   Mostra as VMs com a utilização de IOPS e débito mais elevada e mais baixa
-   Mostra quais as VMs estão em execução os anfitriões
-   Mostra Olá discos superiores com débito elevado, o IOPS, e volumes partilhados de latência em cluster
- Permite-lhe toocustomize e filtrar com base nos grupos

> [!NOTE]
> versão anterior do Olá de Olá capacidade e a solução de desempenho denominada a capacidade de gestão necessário System Center Operations Manager e do Microsoft System Center Virtual Machine Manager. Esta solução atualizada não tem as dependências.


## <a name="connected-sources"></a>Origens ligadas

Olá, a tabela seguinte descreve as origens de Olá ligado que são suportadas por esta solução.

| Origem Ligada | Suporte | Descrição |
|---|---|---|
| [Agentes do Windows](log-analytics-windows-agents.md) | Sim | solução Olá recolhe informações de dados de capacidade e o desempenho de agentes do Windows. |
| [Agentes do Linux](log-analytics-linux-agents.md) | Não    | solução Olá recolhe informações de dados de capacidade e o desempenho de agentes diretos do Linux.|
| [Grupo de gestão do SCOM](log-analytics-om-agents.md) | Sim |solução Olá recolhe dados de capacidade e o desempenho de agentes num grupo de gestão do SCOM ligado. Não é necessária uma ligação direta de tooOMS de agente do SCOM Olá. Dados serão reencaminhados de repositório do Olá gestão grupo toohello OMS.|
| [Conta de armazenamento do Azure](log-analytics-azure-storage.md) | Não | Armazenamento do Azure não inclui dados de desempenho e da capacidade.|

## <a name="prerequisites"></a>Pré-requisitos

- Windows ou agentes do Operations Manager tem de estar instalados no Windows Server 2012 ou superiores anfitriões de Hyper-V, não as máquinas virtuais.


## <a name="configuration"></a>Configuração

Efetue Olá seguir passo tooadd Olá capacidade e o desempenho solução tooyour área de trabalho.

- Adicionar Olá capacidade e desempenho solução tooyour área de trabalho OMS através de Olá processo descrito no [soluções de análise de registos de adicionar de Olá soluções galeria](log-analytics-add-solutions.md).

## <a name="management-packs"></a>Pacotes de gestão

Se o grupo de gestão do SCOM é ligado tooyour área de trabalho do OMS, em seguida, Olá os seguintes pacotes de gestão será instalada no SCOM quando adicionar esta solução. Estes pacotes de gestão não precisam de configurações nem de manutenção.

- Microsoft.IntelligencePacks.CapacityPerformance

evento de 1201 Olá assemelha-se:


```
New Management Pack with id:"Microsoft.IntelligencePacks.CapacityPerformance", version:"1.10.3190.0" received.
```

Quando é atualizado Olá solução capacidade e o desempenho, irá alterar o número de versão Olá.

Para obter mais informações sobre a forma como os pacotes de gestão de solução são atualizados, consulte [ligar o Operations Manager tooLog análise](log-analytics-om-agents.md).

## <a name="using-hello-solution"></a>Utilizar a solução de Olá

Quando adiciona Olá capacidade e o desempenho solução tooyour área de trabalho, Olá capacidade e o desempenho é adicionada toohello dashboard da descrição geral. Este mosaico mostra uma contagem do número de Olá de anfitriões de Hyper-V atualmente ativas e número de Olá do Active Directory máquinas virtuais que foram monitorizados por período de tempo de Olá período selecionado.

![Mosaico de capacidade e o desempenho](./media/log-analytics-capacity/capacity-tile.png)


### <a name="review-utilization"></a>Utilização de revisão

Clique em Olá capacidade e desempenho mosaico tooopen Olá capacidade e o desempenho dashboard. dashboard de Olá inclui colunas Olá Olá a tabela seguinte. Apresenta uma lista dos itens de tooten correspondente que critérios da coluna para Olá especificado intervalo de tempo e o âmbito de cada coluna. Pode executar uma pesquisa de registo que devolve todos os registos clicando **ver todos os** na parte inferior de Olá da coluna de Olá ou ao clicar no cabeçalho da coluna Olá.

- **Anfitriões**
    - **Utilização da CPU do anfitrião** mostra uma tendência gráfica de utilização de Olá da CPU de computadores de anfitrião e uma lista de anfitriões, com base na Olá selecionado o período de tempo. Coloque o cursor sobre Olá linha gráfico tooview os detalhes para um ponto específico no tempo. Clique em Olá gráfico tooview mais detalhes na pesquisa de registo. Clique em qualquer pesquisa de registo de tooopen de nome de anfitrião e ver os detalhes do contador de CPU para as VMs alojadas.
    - **Utilização da memória de anfitrião** mostra uma tendência gráfica de utilização da memória Olá de computadores de anfitrião e uma lista de anfitriões, com base na Olá selecionado o período de tempo. Coloque o cursor sobre Olá linha gráfico tooview os detalhes para um ponto específico no tempo. Clique em Olá gráfico tooview mais detalhes na pesquisa de registo. Clique em qualquer anfitrião nome tooopen registo pesquisa e ver memória os detalhes do contador para VMs alojadas.
- **Máquinas Virtuais**
    - **Utilização de CPU VM** mostra uma tendência gráfica de utilização de Olá da CPU de máquinas virtuais e uma lista de máquinas virtuais, com base no Olá selecionado o período de tempo. Coloque o cursor sobre Olá linha gráfico tooview os detalhes para um ponto específico no tempo para Olá principais 3 VMs. Clique em Olá gráfico tooview mais detalhes na pesquisa de registo. Clique em qualquer VM nome tooopen registo procurar e ver os detalhes do contador agregados da CPU para Olá VM.
    - **Utilização de memória da VM** mostra uma tendência gráfica de utilização da memória Olá de máquinas virtuais e uma lista de máquinas virtuais, com base no Olá selecionado o período de tempo. Coloque o cursor sobre Olá linha gráfico tooview os detalhes para um ponto específico no tempo para Olá principais 3 VMs. Clique em Olá gráfico tooview mais detalhes na pesquisa de registo. Clique em qualquer VM nome tooopen registo procurar e ver os detalhes do contador de agregados de memória para Olá VM.
    - **VM Total disco IOPS** mostra uma tendência gráfica de Olá total disco IOPS para máquinas virtuais e uma lista de máquinas virtuais com Olá IOPS para cada um, com base no Olá selecionado o período de tempo. Coloque o cursor sobre Olá linha gráfico tooview os detalhes para um ponto específico no tempo para Olá principais 3 VMs. Clique em Olá gráfico tooview mais detalhes na pesquisa de registo. Clique em qualquer pesquisa de tooopen de registo de nome VM e a vista de detalhes de Olá VM do contador de disco agregado IOPS.
    - **VM débito Total do disco** mostra uma tendência gráfica do débito total do disco de Olá para máquinas virtuais e uma lista de máquinas virtuais com débito total do disco de Olá para cada um, Olá com base no período de tempo de selecionado. Coloque o cursor sobre Olá linha gráfico tooview os detalhes para um ponto específico no tempo para Olá principais 3 VMs. Clique em Olá gráfico tooview mais detalhes na pesquisa de registo. Clique em qualquer VM nome tooopen registo procurar e ver os detalhes do contador de débito agregado total do disco para Olá VM.
- **Volumes Partilhados de cluster**
    - **Total de débito** mostra soma Olá de ambos leituras e escritas em volumes partilhados de cluster.
    - **Total de IOPS** soma de Olá mostra das operações de entrada/saída por segundo em volumes partilhados de cluster.
    - **Total de latência** apresenta a latência total Olá nos volumes partilhados de cluster.
- **Anfitrião densidade** mosaico superior Olá mostra o número total do Olá da solução de toohello disponíveis anfitriões e máquinas virtuais. Clique em detalhes adicionais do Olá mosaico superior tooview na pesquisa de registo. Também apresenta uma lista de todos os anfitriões e número de Olá de máquinas virtuais que estão alojados. Clique em toodrill um anfitrião para resultados VM Olá na pesquisa de registo.


![Painel de anfitriões de dashboard](./media/log-analytics-capacity/dashboard-hosts.png)

![Painel de máquinas virtuais do dashboard](./media/log-analytics-capacity/dashboard-vms.png)


### <a name="evaluate-performance"></a>Avaliar o desempenho

Ambientes informáticos de produção ser consideravelmente diferem do tooanother de uma organização. Além disso, capacidade e o desempenho de cargas de trabalho poderão dependem da forma como as VMs estão em execução, e o que considerar normal. Toohelp procedimentos específicos medir o desempenho, provavelmente, não seria aplicadas tooyour ambiente. Portanto, mais generalizada orientação prescritiva é melhor se adequam toohelp. A Microsoft publica uma variedade de orientação prescritiva artigos toohelp medir o desempenho.

toosummarize, solução de Olá recolhe dados de desempenho e capacidade de uma variedade de origens, incluindo os contadores de desempenho. Utilizar os dados de desempenho e da capacidade que apresentadas várias analisa na solução de Olá e compare o toothose resultados em Olá [medir o desempenho no Hyper-V](https://msdn.microsoft.com/library/cc768535.aspx) artigo. Embora o artigo de Olá foi publicado algum tempo há, métricas Olá, as considerações e diretrizes ainda são válidas. artigo de Olá contém recursos úteis de tooother ligações.


## <a name="sample-log-searches"></a>Pesquisas de registo de exemplo

Olá, a tabela seguinte fornece pesquisas de registo de exemplo para dados de desempenho e capacidade recolhidos e calculado por esta solução.

| Consulta | Descrição |
|---|---|
| Todas as configurações de memória de anfitrião | <code>Type=Perf ObjectName="Capacity and Performance" CounterName="Host Assigned Memory MB" &#124; measure avg(CounterValue) as MB by InstanceName</code> |
| Todas as configurações de memória da VM | <code>Type=Perf ObjectName="Capacity and Performance" CounterName="VM Assigned Memory MB" &#124; measure avg(CounterValue) as MB by InstanceName</code> |
| Divisão de IOPS de disco Total em todas as VMs | <code>Type=Perf ObjectName="Capacity and Performance" (CounterName="VHD Reads/s" OR CounterName="VHD Writes/s") &#124; top 2500 &#124; measure avg(CounterValue) by CounterName, InstanceName interval 1HOUR</code> |
| Divisão de débito Total do disco em todas as VMs | <code>Type=Perf ObjectName="Capacity and Performance" (CounterName="VHD Read MB/s" OR CounterName="VHD Write MB/s") &#124; top 2500 &#124; measure avg(CounterValue) by CounterName, InstanceName interval 1HOUR</code> |
| Divisão de IOPS Total em todos os CSVs | <code>Type=Perf ObjectName="Capacity and Performance" (CounterName="CSV Reads/s" OR CounterName="CSV Writes/s") &#124; top 2500 &#124; measure avg(CounterValue) by CounterName, InstanceName interval 1HOUR</code> |
| Divisão de débito Total em todos os CSVs | <code>Type=Perf ObjectName="Capacity and Performance" (CounterName="CSV Read MB/s" OR CounterName="CSV Write MB/s") &#124; top 2500 &#124; measure avg(CounterValue) by CounterName, InstanceName interval 1HOUR</code> |
| Divisão de latência Total em todos os CSVs | <code> Type=Perf ObjectName="Capacity and Performance" (CounterName="CSV Read Latency" OR CounterName="CSV Write Latency") &#124; top 2500 &#124; measure avg(CounterValue) by CounterName, InstanceName interval 1HOUR</code> |

>[!NOTE]
> Se a sua área de trabalho tiver sido atualizado toohello [idioma de consulta de análise de registos nova](log-analytics-log-search-upgrade.md), em seguida, Olá acima consultas alteraria toohello seguinte.

> | Consulta | Descrição |
|:--- |:--- |
| Todas as configurações de memória de anfitrião | Desempenho &#124; onde ObjectName = = "Capacidade e desempenho" e CounterName = = "Atribuído MB de memória do anfitrião" &#124; resumir os MB = avg(CounterValue) por InstanceName |
| Todas as configurações de memória da VM | Desempenho &#124; onde ObjectName = = "Capacidade e desempenho" e CounterName = = "MB de memória atribuída de VM" &#124; resumir os MB = avg(CounterValue) por InstanceName |
| Divisão de IOPS de disco Total em todas as VMs | Desempenho &#124; onde ObjectName = = "Capacidade e desempenho" e (CounterName = = "VHD leituras/s" ou CounterName = = "VHD escritas/s") &#124; resumir AggregatedValue = avg(CounterValue) por bin (TimeGenerated, 1h), CounterName, InstanceName |
| Divisão de débito Total do disco em todas as VMs | Desempenho &#124; onde ObjectName = = "Capacidade e desempenho" e (CounterName = = "VHD leitura MB/s" ou CounterName = = "MB/s de escrita de VHD") &#124; resumir AggregatedValue = avg(CounterValue) por bin (TimeGenerated, 1h), CounterName, InstanceName |
| Divisão de IOPS Total em todos os CSVs | Desempenho &#124; onde ObjectName = = "Capacidade e desempenho" e (CounterName = = "CSV leituras/s" ou CounterName = = "CSV escritas/s") &#124; resumir AggregatedValue = avg(CounterValue) por bin (TimeGenerated, 1h), CounterName, InstanceName |
| Divisão de débito Total em todos os CSVs | Desempenho &#124; onde ObjectName = = "Capacidade e desempenho" e (CounterName = = "CSV leituras/s" ou CounterName = = "CSV escritas/s") &#124; resumir AggregatedValue = avg(CounterValue) por bin (TimeGenerated, 1h), CounterName, InstanceName |
| Divisão de latência Total em todos os CSVs | Desempenho &#124; onde ObjectName = = "Capacidade e desempenho" e (CounterName = = "Latência de leitura do CSV" ou CounterName = = "Latência de escrita de CSV") &#124; resumir AggregatedValue = avg(CounterValue) por bin (TimeGenerated, 1h), CounterName, InstanceName |


## <a name="next-steps"></a>Passos seguintes
* Utilize [pesquisas de registo na análise de registos](log-analytics-log-searches.md) tooview detalhadas dados de desempenho e da capacidade.
