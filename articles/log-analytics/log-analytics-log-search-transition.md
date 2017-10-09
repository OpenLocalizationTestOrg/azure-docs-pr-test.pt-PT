---
title: "folha de referência de linguagem de consulta de análise de registos de aaaAzure | Microsoft Docs"
description: "Este artigo fornece assistência sobre a transição toohello novo idioma de consulta de análise de registos, se já estiver familiarizado com o idioma de legado Olá."
services: operations-management-suite
documentationcenter: 
author: bwren
manager: carmonm
editor: tysonn
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/23/2017
ms.author: bwren
ms.openlocfilehash: 8b4ee3d0b5e1ec8a9f95a09e0ad9835615ad1342
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="transitioning-tooazure-log-analytics-new-query-language"></a>Mudar o idioma de consulta nova análise de registos tooAzure

> [!NOTE]
> Pode ler mais sobre Olá idioma de consulta de nova análise de registos e obter Olá procedimento tooupgrade sua área de trabalho na atualização do seu [pesquisa de registo do Log Analytics do Azure área de trabalho toonew](log-analytics-log-search-upgrade.md).

Este artigo fornece assistência sobre a transição toohello novo idioma de consulta de análise de registos, se já estiver familiarizado com o idioma de legado Olá.

## <a name="language-converter"></a>Conversor de idioma

Se estiver familiarizado com o idioma de consulta de análise de registos legado Olá, Olá toocreate Olá mesma consulta no idioma novo Olá de forma mais fácil é toouse Olá conversor de idioma que está instalado no portal de registo de pesquisa de Olá quando a sua área de trabalho é convertida.  A utilização de conversor Olá é tão simple como escrever uma consulta na caixa de texto superior Olá legada e, em seguida, clicando em **converter**.  Pode clique Olá botão toorun Olá consulta ou copiar e colar toouse-lo algures pessoa.

![Conversor de idioma](media/log-analytics-log-search-upgrade/language-converter.png)


## <a name="cheat-sheet"></a>Nota

Olá tabela seguinte fornece uma comparação entre uma variedade de consultas comuns tooequivalent comandos entre o idioma de consulta novo e legado Olá no Log Analytics do Azure.

| Descrição | Legado | novo |
|:--|:--|:--|
| Todas as tabelas de pesquisa      | erro | procurar "error" (não sensível confidencial) |
| Selecione os dados da tabela | Tipo de evento de = |  Evento |
|                        | Tipo = eventos &#124; Selecione a origem, o registo de eventos, EventID | Evento &#124; EventID de origem, o registo de eventos, do projeto |
|                        | Tipo = eventos &#124; primeiros 100 | Evento &#124; tirar 100 |
| Comparação de cadeias      | Tipo = Computer=srv01.contoso.com de eventos   | Evento &#124; onde computador = = "srv01.contoso.com" |
|                        | Tipo = Computer=contains("contoso") de eventos | Evento &#124; em que o computador contém "contoso" (não sensível confidencial)<br>Evento &#124; onde computador contains_cs "Contoso" (sensível às maiúsculas e) |
|                        | Tipo = evento computador = RegEx ("@contoso@")  | Evento &#124; em que o computador com regex ". *contoso*" |
| Comparação de data        | Tipo = eventos TimeGenerated > 1DAYS agora | Evento &#124; onde TimeGenerated > ago(1d) |
|                        | Tipo = eventos TimeGenerated > 2017-05-01 TimeGenerated < 2017-05-31 | Evento &#124; onde TimeGenerated entre (datetime(2017-05-01).. datetime(2017-05-31)) |
| Comparação booleana     | Tipo = Heartbeat IsGatewayInstalled = false  | Heartbeat | onde IsGatewayInstalled = = false |
| Ordenar                   | Tipo = eventos &#124; Ordenar asc do computador, desc de registo de eventos, EventLevelName asc | Evento \| Ordenar por computador asc, desc de registo de eventos, EventLevelName asc |
| Distintos               | Tipo = eventos &#124; a eliminação de duplicados computador \| Selecione o computador | Evento &#124; Resumir por computador, o registo de eventos |
| Expandir colunas         | Tipo = desempenho CounterName = "% tempo do processador" &#124; EXPANDA if(map(CounterValue,0,50,0,1),"HIGH","LOW") como utilização | Desempenho &#124; onde CounterName = = "% tempo do processador" \| expandir a utilização = iff (CounterValue > 50, "Alta", "Baixa") |
| Agregação            | Tipo = eventos &#124; medida existente como contagem por computador | Evento &#124; resumir contagem = existente pelo computador |
|                                | Tipo = desempenho ObjectName = processador CounterName = "% tempo do processador" &#124; medidas avg(CounterValue) por intervalo de computador 5 minutos | Desempenho &#124; onde ObjectName = = "Processador" e CounterName = = "% tempo do processador" &#124; resumir avg(CounterValue) por computador, bin (TimeGenerated, 5min) |
| Agregação de limite | Tipo = eventos &#124; medida existente pelo computador &#124; 10 principais | Evento &#124; resumir AggregatedValue = existente pelo computador &#124; limite de 10 |
| União                  | Tipo = eventos ou tipo = Syslog | União evento Syslog |
| Associar                   | Tipo = NetworkMonitoring &#124; associação interna AgentIP (tipo = Heartbeat) ComputerIP | NetworkMonitoring &#124; tipo de associação = interna (tipo de pesquisa = = "Heartbeat") no $left. AgentIP = = $right.ComputerIP |



## <a name="next-steps"></a>Passos seguintes
- Veja uma [tutorial sobre como escrever consultas](https://go.microsoft.com/fwlink/?linkid=856078) utilizando a linguagem de consulta Olá novo.
- Consulte toohello [referência de linguagem de consulta](https://go.microsoft.com/fwlink/?linkid=856079) para obter detalhes sobre todos os comandos, operadores e funções para o idioma de consulta nova Olá.  
