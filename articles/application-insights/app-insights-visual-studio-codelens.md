---
title: aaaApplication telemetria Insights no Visual Studio CodeLens | Microsoft Docs
description: "Aceda rapidamente ao seu pedido do Application Insights e telemetria de exceção com o CodeLens no Visual Studio."
services: application-insights
documentationcenter: .net
author: numberbycolors
manager: carmonm
ms.assetid: 93559e44-23cb-4b9d-8425-60f7f0d0a82c
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/17/2017
ms.author: bwren
ms.openlocfilehash: e812aa48f2a67eea860e7ecde341855763bb8a8b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="application-insights-telemetry-in-visual-studio-codelens"></a>Telemetria do Application Insights no Visual Studio CodeLens
Os métodos no código Olá da sua aplicação web podem ser anotados com telemetria sobre exceções de tempo de execução e tempos de resposta do pedido. Se instalar [Azure Application Insights](app-insights-overview.md) na sua aplicação, é apresentada a telemetria de Olá no Visual Studio [CodeLens](https://msdn.microsoft.com/library/dn269218.aspx) -Olá notas na parte superior de Olá de cada função em que estiver a utilizar tooseeing útil informações como o número de Olá da função de Olá locais são referenciadas ou Olá última pessoa que editou-lo.

![CodeLens](./media/app-insights-visual-studio-codelens/codelens-overview.png)

> [!NOTE]
> Application Insights no CodeLens está disponível no Visual Studio 2015 Update 3 e posterior ou com a versão mais recente do Olá do [extensão do Developer Analytics Tools](https://visualstudiogallery.msdn.microsoft.com/82367b81-3f97-4de1-bbf1-eaf52ddc635a). CodeLens está disponível na Olá Enterprise e Professional edições do Visual Studio.
> 
> 

## <a name="where-toofind-application-insights-data"></a>Onde toofind dados do Application Insights
Procure telemetria do Application Insights no indicadores de CodeLens Olá dos métodos de pedido pública Olá da aplicação web. Os indicadores de CodeLens são apresentados acima do método e de outras declarações de código C# e Visual Basic. Se os dados do Application Insights estiverem disponíveis para um método, verá indicadores para os pedidos e exceções, tais como "100 pedidos, 1% falhou" ou "10 exceções". Clique num indicador de CodeLens para obter mais detalhes. 

> [!TIP]
> Pedem do Application Insights e os indicadores de exceção podem demorar alguns segundos Extras tooload depois de aparecem outros indicadores de CodeLens.
> 
> 

## <a name="exceptions-in-codelens"></a>Exceções no CodeLens
![TBD](./media/app-insights-visual-studio-codelens/codelens-exceptions.png)

indicador de CodeLens Olá exceção mostra o número de Olá de exceções que ocorreram no Olá das últimas 24 horas de Olá 15 a maioria das exceções frequentemente occurring na sua aplicação durante esse período, ao processar o pedido de Olá servidas pelo método Olá.

toosee mais detalhes, clique no indicador de CodeLens Olá exceções:

* percentagem de Olá alteração no número de exceções de Olá mais recente 24 horas relativo toohello anterior 24 horas
* Escolha **aceda toocode** toonavigate toohello código de origem para a função de Olá gerar Olá exceção
* Escolha **pesquisa** tooquery Olá, todas as instâncias desta exceção que ocorreram nas últimas 24 horas
* Escolha **tendência** tooview uma visualização de tendência para ocorrências desta exceção no Olá das últimas 24 horas
* Escolha **ver todas as exceções nesta aplicação** tooquery Olá, todas as exceções que ocorreram nas últimas 24 horas
* Escolha **explorar tendências de exceção** tooview uma visualização de tendência para todas as exceções que ocorreram no Olá das últimas 24 horas. 

> [!TIP]
> Se vir "0 exceções" no CodeLens mas sabe que deverá existir exceções, verifique se o recurso do Application Insights à direita Olá está selecionado no CodeLens toomake. tooselect outro recurso, faça duplo clique no seu projeto em Olá Explorador de soluções e escolha **Application Insights > Escolher origem telemetria**. CodeLens é mostrado apenas para Olá 15 a maioria das exceções frequentemente occurring na sua aplicação no Olá das últimas 24 horas, por isso, caso uma exceção é Olá frequentemente 16th mais ou menos, verá "0 exceções". As exceções de vistas do ASP.NET não podem aparecer em métodos de controlador de Olá essas vistas geradas.
> 
> [!TIP]
> Se vir "? exceções"no CodeLens, terá de tooassociate a que sua conta do Azure com o Visual Studio ou as credenciais de conta do Azure pode ter expirado. Em ambos os casos, clique em "? exceções"e escolha **adicionar uma conta...**  tooenter as suas credenciais.
> 
> 

## <a name="requests-in-codelens"></a>Pedidos no CodeLens
![TBD](./media/app-insights-visual-studio-codelens/codelens-requests.png)

Olá mostra de indicador de CodeLens Olá número de HTTP do pedido de pedidos que foram servidos por um método de Olá passado 24 horas, além de percentagem de Olá desses pedidos que falharam.

toosee obter mais detalhes, clique Olá pedidos CodeLens indicador:

* Olá absoluto e percentagem de alterações no número de pedidos, pedidos falhados e tempos de resposta médio ao longo de Olá passado toohello de 24 horas em comparação comparadas anterior 24 horas
* fiabilidade Olá do método Olá, calculado como a percentagem de Olá de pedidos que não foi possível efetuar em Olá das últimas 24 horas
* Escolha **pesquisa** pedidos nem tooquery de pedidos falhados Olá todos os pedidos (falhados) que ocorreram nas Olá das últimas 24 horas
* Escolha **tendência** tooview uma visualização de tendência para pedidos, pedidos falhados ou resposta médio vezes em Olá das últimas 24 horas.
* Escolha o nome de Olá do Olá recurso do Application Insights no Olá canto superior esquerdo do Olá CodeLens detalhes vista toochange qual o recurso é origem Olá CodeLens dados.

## <a name="next"></a>Passos seguintes
|  |  |
| --- | --- |
| **[Trabalhar com o Application Insights no Visual Studio](app-insights-visual-studio.md)**<br/>Procure telemetria, veja dados no CodeLens e configure o Application Insights. Tudo isto no Visual Studio. |![Clique no projeto Olá e escolha Application Insights, pesquisa](./media/app-insights-visual-studio-codelens/34.png) |
| **[Adicionar mais dados](app-insights-asp-net-more.md)**<br/>Monitorize a utilização, a disponibilidade, as dependências e as exceções. Integre rastreios a partir de arquiteturas de registo. Grave a telemetria personalizada. |![Visual Studio](./media/app-insights-visual-studio-codelens/64.png) |
| **[Trabalhar com o portal do Application Insights Olá](app-insights-dashboards.md)**<br/>Dashboards, ferramentas de diagnóstico e análise poderosas, alertas, mapa de dependência em direto da aplicação e exportação de telemetria. |![Visual Studio](./media/app-insights-visual-studio-codelens/62.png) |

