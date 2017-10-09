---
title: "aaaMonitor estado de funcionamento da sua aplicação e a utilização com o Application Insights"
description: "Introdução ao Application Insights. Analise a utilização, disponibilidade e desempenho dos seus no local ou aplicações do Microsoft Azure."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 40650472-e860-4c1b-a589-9956245df307
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 11/25/2015
ms.author: bwren
ms.openlocfilehash: 9230a6e65e5afb00c36122ff1d1de01ba19cd7f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-performance-in-web-applications"></a>Monitorizar o desempenho nas aplicações Web


Certifique-se de que a aplicação está a executar corretamente e descobrir rapidamente sobre eventuais falhas. [Application Insights] [ start] conte quaisquer problemas de desempenho e exceções e ajudar a localizar e diagnosticar Olá de causas raiz.

Application Insights podem monitorizar aplicações web de Java e ASP.NET e serviços, serviços do WCF. Podem ser alojado no local, em máquinas virtuais, ou como Web sites do Microsoft Azure. 

No lado do cliente de Olá, Application Insights pode demorar a telemetria de páginas web e uma ampla variedade de dispositivos incluindo dispositivos iOS, Android e aplicações da loja Windows.

>[!Note]
> Efetuamos uma nova experiência disponível para localizar lenta efetuar páginas na sua aplicação web. Se não tiver acesso tooit, ativá-la ao configurar as opções de pré-visualização com Olá [painel de pré-visualização](app-insights-previews.md). Leia sobre esta nova experiência em [localizar e corrigir os congestionamentos de desempenho com investigação de desempenho interativa Olá](#Find-and-fix-performance-bottlenecks-with-an-interactive-Performance-investigation).

## <a name="setup"></a>Configurar a monitorização de desempenho
Se ainda não adicionou o Application Insights tooyour (ou seja, se não tem Applicationinsights) do projeto, escolha uma das seguintes maneiras tooget iniciado:

* [Aplicações web do ASP.NET](app-insights-asp-net.md)
  * [Adicionar a monitorização de exceções](app-insights-asp-net-exceptions.md)
  * [Adicionar a monitorização de dependência](app-insights-monitor-performance-live-website-now.md)
* [Aplicações web J2EE](app-insights-java-get-started.md)
  * [Adicionar a monitorização de dependência](app-insights-java-agent.md)

## <a name="view"></a>Explorar métricas de desempenho
No [Olá portal do Azure](https://portal.azure.com), procure o recurso do Application Insights toohello que configurou para a sua aplicação. Painel de descrição geral de Olá mostra os dados de desempenho básico:

Clique em qualquer gráfico toosee mais detalhes e resultados toosee durante um período de tempo. Por exemplo, clique no mosaico pedidos Olá e, em seguida, selecione um intervalo de tempo:

![Clicar toomore dados e selecione um intervalo de tempo](./media/app-insights-web-monitor-performance/appinsights-48metrics.png)

Clique em toochoose um gráfico que métricas apresenta, ou adicione um novo gráfico e selecionar a métricas:

![Clique em métricas de toochoose um gráfico](./media/app-insights-web-monitor-performance/appinsights-61perfchoices.png)

> [!NOTE]
> **Desmarque todas as métricas de Olá** toosee Olá completa seleção que está disponível. métricas de Olá enquadram-se grupos; Quando qualquer membro de um grupo é selecionado, só hello outros membros desse grupo aparecem.

## <a name="metrics"></a>O que faz-média de todos os? Os mosaicos de desempenho e relatórios
Existem várias métricas de desempenho, que pode obter. Vamos começar com as que são apresentados por predefinição no painel de aplicação Olá.

### <a name="requests"></a>Pedidos
Olá número de pedidos HTTP recebidos no período de tempo especificado. Compare isto com resultados de Olá no toosee outros relatórios como a aplicação se comporta como Olá carga varia.

Pedidos de HTTP incluem todos os pedidos GET ou POST de páginas, dados e imagens.

Clique em Olá mosaico tooget contagens para URLs específicos.

### <a name="average-response-time"></a>Tempo de resposta médio
Tempo de Olá medidas entre um pedido web introduzir a sua aplicação e Olá resposta a ser devolvida.

pontos de Olá mostram uma mudança médio. Se existirem muitos pedidos, poderão existir alguns desvio de média de Olá sem um horário de pico óbvios ou dip no gráfico de Olá.

Procure picos de atividade invulgares. Em geral, espere toorise de tempo de resposta com um aumento súbito do pedidos. Se o aumento súbito Olá desproporcionado, a aplicação pode atingir um limite de recursos, tais como a capacidade de CPU ou Olá de um serviço que utiliza.

Clique em tempos de tooget Olá mosaico para URLs específicos.

![](./media/app-insights-web-monitor-performance/appinsights-42reqs.png)

### <a name="slowest-requests"></a>Pedidos mais lentos
![](./media/app-insights-web-monitor-performance/appinsights-44slowest.png)

Mostra quais os pedidos poderão ter de otimização de desempenho.

### <a name="failed-requests"></a>Pedidos falhados
![](./media/app-insights-web-monitor-performance/appinsights-46failed.png)

Uma contagem de pedidos que emitiu exceções não identificadas.

Clique Olá mosaico toosee Olá os detalhes de falhas específicas e selecione um toosee de pedido individual respetivos detalhes. 

Apenas uma amostra representativa de falhas é mantida para inspecção individuais.

### <a name="other-metrics"></a>Outras métricas
toosee que outras métricas pode apresentar, clique num gráfico e, em seguida, anular seleção de todas as Olá métricas toosee Olá completa disponível conjunto. Clique em (i) toosee definição cada métrica.

![Anular seleção de todas as métricas toosee Olá todo conjunto](./media/app-insights-web-monitor-performance/appinsights-62allchoices.png)

Selecionar qualquer Olá desativa métrica outras pessoas que não pode aparecer no Olá mesmo gráfico.

## <a name="set-alerts"></a>Definir alertas
toobe notificado por correio eletrónico dos valores invulgares de qualquer métrica, adicione um alerta. Pode escolher administradores de conta do toosend Olá e-mail toohello ou toospecific endereços de correio eletrónico.

![](./media/app-insights-web-monitor-performance/appinsights-413setMetricAlert.png)

Defina recurso Olá antes Olá outras propriedades. Não escolha a recursos de webtest Olá se pretende os alertas de tooset no desempenho ou a métrica de utilização.

Ser unidades de Olá toonote cuidado no qual está a pedido valor de limiar de Olá tooenter.

*Não vejo o botão de alerta Olá adicionar.* -Esta é uma toowhich de conta de grupo têm acesso só de leitura? Consulte o administrador de conta Olá.

## <a name="diagnosis"></a>Diagnosticar problemas
Eis algumas sugestões para localizar e diagnosticar problemas de desempenho:

* Configurar [testes web] [ availability] toobe alertado se o web site ficar inativo ou responder lentamente ou incorretamente. 
* Compare a contagem de pedido de Olá com outra métricas toosee se falhas ou resposta lenta relacionado tooload.
* [Inserir, procure as instruções de rastreio] [ diagnostic] no seu código toohelp identificar problemas.
* Monitorizar a aplicação Web na operação com [métricas em fluxo em direto][livestream].
* Capturar estado do Olá da aplicação .net com [instantâneo depurador][snapshot].

## <a name="find-and-fix-performance-bottlenecks-with-an-interactive-performance-investigation"></a>Localizar e corrigir os congestionamentos de desempenho com uma investigação de desempenho interativa

Pode utilizar Olá novo Application Insights desempenho interativa investigação toolocate áreas da sua aplicação Web que são abrandamento desempenho global. Pode rapidamente localizar específico páginas são abrandamento e utilizam Olá [ferramenta de criação de perfis](app-insights-profiler.md) toosee se houver uma correlação entre estas páginas.

### <a name="create-a-list-of-slow-performing-pages"></a>Criar uma lista de páginas lentas de desempenho 

primeiro passo de Olá para encontrar problemas de desempenho é tooget uma lista de Olá lenta de páginas a responder. ecrã de Olá captura abaixo demonstra Olá desempenho painel tooget uma lista de potenciais tooinvestigate de páginas ainda mais a utilizar. Pode ver rapidamente nesta página que ocorreu uma slow-down no tempo de resposta de Olá da aplicação Olá aproximadamente 6:00 PM e novamente em aproximadamente as 22: 00. Também pode ver que a operação de cliente/detalhes Olá GET tinha execução algumas longa operações com um tempo de resposta mediano de 507.05 milissegundos. 

![Desempenho interativa do Application Insights](./media/app-insights-web-monitor-performance/performance1.png)

### <a name="drill-down-on-specific-pages"></a>Desagregar nas páginas específicas

Assim que tiver um instantâneo do desempenho da aplicação, pode obter mais detalhes nas operações de desempenho lento específicas. Clique em qualquer operação no Olá lista toosee Olá detalhes, como mostrado abaixo. Do gráfico Olá pode ver se o desempenho de Olá foi com base numa dependência. Também pode ver quantas Olá experiente de utilizadores vários tempos de resposta. 

![Painel de operações do Application Insights](./media/app-insights-web-monitor-performance/performance5.png)

### <a name="drill-down-on-a-specific-time-period"></a>Desagregar no período de tempo específico

Depois de identificar um ponto no tempo tooinvestigate, desagregar ainda mais toolook em operações específicas Olá que possam ter provocado slow-down de desempenho de Olá. Quando clica num ponto específico no tempo a obter detalhes de Olá da página Olá, conforme mostrado abaixo. No Olá exemplo abaixo, pode ver as operações de Olá listadas para um determinado período de tempo, juntamente com códigos de resposta do servidor de Olá e duração de operação de Olá. Também tem o url de Olá para abrir um item de trabalho do TFS, se precisar de toosend esta equipa de desenvolvimento de tooyour de informações.

![Intervalo de tempo do Application Insights](./media/app-insights-web-monitor-performance/performance2.png)

### <a name="drill-down-on-a-specific-operation"></a>Desagregar uma operação específica

Depois de identificar um ponto no tempo tooinvestigate, desagregar ainda mais toolook em operações específicas Olá que possam ter provocado slow-down de desempenho de Olá. Clique numa operação de Olá lista toosee Olá os detalhes da operação de Olá, conforme mostrado abaixo. Neste exemplo, pode ver que falha na operação de Olá e Application Insights forneceu Olá os detalhes do Olá emitiu aplicação Olá de exceção. Novamente, pode facilmente criar um item de trabalho do TFS a partir deste painel.

![Painel de operação do Application Insights](./media/app-insights-web-monitor-performance/performance3.png)


## <a name="next"></a>Passos seguintes
[Testes Web] [ availability] -pedidos web enviaram tooyour aplicação em intervalos regulares de volta Olá mundo.

[Capturar e procurar rastreios de diagnóstico] [ diagnostic] - inserir chamadas de rastreio e pouco úteis através de problemas de toopinpoint Olá resultados.

[Controlo de utilização] [ usage] -saber como as pessoas utilizam a sua aplicação.

[Resolução de problemas] [ qna] - e as perguntas e respostas



<!--Link references-->

[availability]: app-insights-monitor-web-app-availability.md
[diagnostic]: app-insights-diagnostic-search.md
[greenbrown]: app-insights-asp-net.md
[qna]: app-insights-troubleshoot-faq.md
[redfield]: app-insights-monitor-performance-live-website-now.md
[start]: app-insights-overview.md
[usage]: app-insights-web-track-usage.md
[livestream]: app-insights-live-stream.md
[snapshot]: app-insights-snapshot-debugger.md



