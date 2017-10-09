---
title: Alertas de aaaSet no Azure Application Insights | Microsoft Docs
description: "Seja notificado sobre tempos de resposta lento, exceções e outros desempenho ou alterações de utilização na sua aplicação web."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: f8ebde72-f819-4ba5-afa2-31dbd49509a5
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: e160cb173e68fda2e6d97f29da342c46b7ac4f19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="set-alerts-in-application-insights"></a>Definir alertas no Application Insights
[Azure Application Insights] [ start] podem alertá-lo toochanges nas métricas de desempenho ou a utilização na sua aplicação web. 

Application Insights monitoriza a sua aplicação em direto num [ampla variedade de plataformas] [ platforms] toohelp diagnosticar problemas de desempenho e compreender os padrões de utilização.

Existem três tipos de alertas:

* **Alertas métricas** indicam quando uma métrica atravesse um valor de limiar para um determinado período - como tempos de resposta, contagens de exceção, utilização da CPU ou vistas de página. 
* [**Testes Web** ] [ availability] indicam quando o site se encontra disponível no Olá internet ou responder lentamente. [Saiba mais][availability].
* [**O diagnóstico** ](app-insights-proactive-diagnostics.md) são automaticamente configurados toonotify-lo sobre os padrões de desempenho de atividade invulgar.

Iremos focar-se de alertas métricas neste artigo.

## <a name="set-a-metric-alert"></a>Definir um alerta de métrico
Painel de regras de alertas abertos Olá e, em seguida, utilize Olá botão adicionam. 

![No painel de regras de alerta de Olá, escolha Adicionar alerta. Configurar a aplicação como Olá toomeasure de recursos, forneça um nome para o alerta de Olá e escolha uma métrica.](./media/app-insights-alerts/01-set-metric.png)

* Defina recurso Olá antes Olá outras propriedades. **Escolha o recurso de Olá "(componentes)"** se quiser tooset alertas nas métricas de desempenho ou utilização.
* nome de Olá que dê toohello alerta deve ser exclusivo dentro do grupo de recursos de Olá (não apenas a aplicação).
* Ser unidades de Olá toonote cuidado no qual está a pedido valor de limiar de Olá tooenter.
* Se selecionar a caixa de Olá "... proprietários de E-Mail", os alertas são enviados por e-mail tooeveryone que possua o grupo de recursos de toothis de acesso. tooexpand este conjunto de pessoas, adicioná-los toohello [grupo de recursos ou subscrição](app-insights-resources-roles-access-control.md) (não Olá recursos).
* Se especificar "Adicionais mensagens de correio eletrónico", os alertas são enviados toothose pessoas ou grupos (ou não tiver selecionado a caixa de "e-mail proprietários …" Olá). 
* Definir um [webhook endereço](../monitoring-and-diagnostics/insights-webhooks-alerts.md) se tiver configurado uma aplicação web que responde tooalerts. É denominado quando o alerta de Olá está ativada e quando for resolvida. (Mas tenha em atenção que neste momento, os parâmetros de consulta não são submetidos como propriedades de webhook).
* Pode desativar ou ativar alerta de Olá: consulte os botões de Olá, Olá parte superior do painel de Olá.

*Não vejo o botão de alerta Olá adicionar.* 

* Está a utilizar uma conta institucional? Pode definir alertas se tiver proprietário ou contribuinte recurso de aplicação de toothis de acesso. Observe o painel de controlo de acesso de Olá. [Saiba mais sobre o controlo de acesso][roles].

> [!NOTE]
> No painel de alertas de Olá, verá que já há um conjunto de alerta cópias de segurança: [diagnóstico](app-insights-proactive-failure-diagnostics.md). alerta de automática Olá monitoriza um determinado métrica, pedido taxa de falhas. A menos que decida alerta proativo do toodisable Olá, não precisa tooset o seus próprios alerta de taxa de falhas de pedido. 
> 
> 

## <a name="see-your-alerts"></a>Consulte os alertas
Obter um e-mail quando um alerta muda de estado entre inativos e Active Directory. 

estado atual do Olá de cada alerta é apresentado no painel de regras de alerta de Olá.

Há um resumo da atividade recente alertas Olá pendente:

![Lista de alertas pendente](./media/app-insights-alerts/010-alert-drop.png)

histórico de Olá de alterações de estado está a ser Olá registo de atividade:

![No painel de descrição geral de Olá, clique em definições, os registos de auditoria](./media/app-insights-alerts/09-alerts.png)

## <a name="how-alerts-work"></a>Como funcionam os alertas
* Um alerta tem três Estados: "Nunca ativado", "Ativado" e "Resolvido". Significa ativada Olá condição que especificou foi for VERDADEIRO, quando foi avaliado pela última vez.
* Uma notificação é gerada quando um alerta muda de estado. (Se a condição de alerta de Olá já foi verdadeira quando criou o alerta de Olá, poderá não receberá uma notificação até que a condição de Olá fica falsa.)
* Cada notificação gera uma mensagem de e-mail, se selecionado Olá caixa de correio eletrónico ou fornecidos endereços de correio eletrónico. Também pode ver Olá notificações na lista pendente.
* Um alerta é avaliado sempre que uma métrica de chega, mas não, caso contrário.
* agrega métrica Olá através de Olá precedente período de avaliação de Olá e compara-toohello limiar toodetermine Olá novo Estado.
* período de Olá que escolher Especifica o intervalo de Olá durante o qual são agregadas métricas. Não afeta a frequência hello alerta de avaliação: que depende da frequência de Olá de chegada de métricas.
* Se não existem dados são recebidos para uma determinado métrica durante algum tempo intervalo Olá tem diferentes efeitos na avaliação de alerta e em gráficos de Olá no Explorador de métrica. No Explorador de métrica, se não existem dados são utilizados durante um período superior intervalo de amostragem do gráfico Olá, o gráfico de Olá mostra um valor de 0. Mas um alerta com base no Olá mesma métrica não é possível reavaliadas e Olá permanece de estado do alerta inalterada. 
  
    Quando os dados são recebidos eventualmente, o gráfico de Olá salta tooa back-não igual a zero valor. alerta de Olá avalia com base nos dados de Olá disponíveis para período Olá que especificou. Se o novo ponto de dados Olá Olá apenas um disponível no período de Olá, Olá agregado baseia-se apenas no ponto de dados.
* Um alerta pode flicker frequentemente entre os Estados de bom estado de funcionamento e alertas, mesmo se definir um período de tempo. Isto pode acontecer se o valor métrico de Olá passa em torno do limiar de Olá. Não há nenhum hysteresis limiar Olá: Olá transição tooalert ocorre ao hello mesmo valor como Olá toohealthy de transição.

## <a name="what-are-good-alerts-tooset"></a>O que são alertas boa tooset?
Depende da aplicação. toostart com, tem melhor não tooset demasiados métricas. Passe algum tempo a observar os métricos gráficos enquanto a aplicação está em execução, tooget uma funcionalidade para como esta se comporta normalmente. Esta prática ajuda-o a encontrar formas tooimprove o desempenho dele. Em seguida, configure alertas tootell, quando as métricas de Olá ficam fora do horário normal Olá. 

Alertas populares incluem:

* [Métricas de browser][client], especialmente Browser **tempos de carregamento de página**, está pronto para aplicações web. Se a sua página tiver muitos scripts, deve procurar **exceções de browser**. Ordem tooget estas métricas e os alertas, é necessário tooset [monitorização da página web][client].
* **Tempo de resposta do servidor** para o lado do servidor de Olá de aplicações web. Bem como configurar alertas, atento esta métrica toosee se-disproportionately varia com taxas de pedidos elevada: variação pode indicar que a aplicação está a ficar sem recursos. 
* **Exceções de servidor** -toosee-las, tem algumas toodo [configuração adicional](app-insights-asp-net-exceptions.md).

Não se esqueça de que [diagnósticos de taxa de falhas proativa](app-insights-proactive-failure-diagnostics.md) automaticamente monitor Olá velocidade a que a sua aplicação responde toorequests com códigos de falha. 

## <a name="automation"></a>Automatização
* [Utilizar o PowerShell tooautomate configurar alertas](app-insights-powershell-alerts.md)
* [Utilizar webhooks tooautomate responde tooalerts](../monitoring-and-diagnostics/insights-webhooks-alerts.md)

## <a name="video"></a>Vídeo

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player]

## <a name="see-also"></a>Consultar também
* [Testes web de disponibilidade](app-insights-monitor-web-app-availability.md)
* [Automatizar a configuração de alertas](app-insights-powershell-alerts.md)
* [Diagnóstico](app-insights-proactive-diagnostics.md) 

<!--Link references-->

[availability]: app-insights-monitor-web-app-availability.md
[client]: app-insights-javascript.md
[platforms]: app-insights-platforms.md
[roles]: app-insights-resources-roles-access-control.md
[start]: app-insights-overview.md

