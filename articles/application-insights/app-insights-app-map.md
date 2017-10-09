---
title: aaaApplication mapa no Azure Application Insights | Microsoft Docs
description: "Uma apresentação visual de dependências de Olá entre os componentes de aplicação, etiquetadas com alertas e KPIs."
services: application-insights
documentationcenter: 
author: SoubhagyaDash
manager: carmonm
ms.assetid: 3bf37fe9-70d7-4229-98d6-4f624d256c36
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: 96ab753a100ea53ec7d367e3559b6622ab6fd182
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="application-map-in-application-insights"></a>Mapa de aplicação no Application Insights
No [Azure Application Insights](app-insights-overview.md), o mapeamento de aplicações é um esquema visual de relações de dependência de Olá dos componentes da aplicação. Cada componente mostra KPIs, tais como toohelp de carga, desempenho, falhas e os alertas, detetar qualquer componente causar um problema de desempenho ou a falha. Pode clicar sucessivamente de qualquer componente toomore detalhadas de diagnóstico, tais como eventos do Application Insights. Se a sua aplicação utiliza serviços do Azure, também pode clicar sucessivamente tooAzure diagnostics, manutenção automática, tais como recomendações do Assistente de base de dados do SQL Server.

Como outros gráficos, pode afixar um toohello de mapa de aplicação dashboard do Azure, onde este fica totalmente funcional. 

## <a name="open-hello-application-map"></a>Mapa de aplicação Olá aberta
Mapa de Olá aberto a partir do painel de descrição geral de Olá para a sua aplicação:

![Abra o mapa de aplicação](./media/app-insights-app-map/01.png)

![mapa de aplicação](./media/app-insights-app-map/02.png)

mapa de Olá mostra:

* Testes de disponibilidade
* Componente do lado do cliente (monitorizado com Olá JavaScript SDK)
* Componente do lado do servidor
* Dependências de componentes de cliente e servidor Olá

Pode expandir e fechar a grupos de ligação de dependência:

![Fechar](./media/app-insights-app-map/03.png)

Se tiver uma grande quantidade de dependências de um tipo (SQL Server, etc. HTTP), que possam aparecer agrupados. 

![dependências agrupadas](./media/app-insights-app-map/03-2.png)

## <a name="spot-problems"></a>Problemas de lugar para cima
Cada nó tem indicadores de desempenho relevantes, tais como as taxas de carga, desempenho e falha Olá desse componente. 

Ícones de aviso destacar informações sobre problemas possíveis. Um aviso laranja significa que existem falhas nos pedidos, vistas de página ou chamadas de dependência. Vermelho significa uma taxa de falhas superior a 5%. Se quiser tooadjust estes limiares, abra as opções.

![ícones de falha](./media/app-insights-app-map/04.png)

Active Directory também alertas Mostrar cópias de segurança: 

![alertas ativos](./media/app-insights-app-map/05.png)

Se utilizar o SQL Azure, há um ícone que mostra quando existem recomendações sobre como melhorar o desempenho. 

![recomendação do Azure](./media/app-insights-app-map/06.png)

Clique em qualquer tooget ícone mais detalhes:

![recomendação do Azure](./media/app-insights-app-map/07.png)

## <a name="diagnostic-click-through"></a>Clique em diagnóstico através do
Cada um de nós de Olá num mapa Olá oferece clique visado através de diagnóstico. Opções de Olá variam consoante o tipo de Olá do nó de Olá.

![Opções de servidor](./media/app-insights-app-map/09.png)

Para os componentes que estão alojados no Azure, as opções de Olá incluem hiperligações diretas toothem.

## <a name="filters-and-time-range"></a>Filtros e o intervalo de tempo
Por predefinição, o mapa de Olá resume todos os dados de Olá disponíveis para Olá escolhido o intervalo de tempo. Mas pode filtrar os nomes de operações específicas apenas de tooinclude ou dependências.

* Nome da operação: inclui os vistas de página e os tipos de pedido do lado do servidor. Com esta opção, Olá mapa mostra Olá KPI no nó do lado do servidor/cliente Olá para apenas operações de Olá selecionado. Mostra as dependências de Olá chamadas no contexto de Olá dessas operações específicas.
* Nome de base de dependência: Isto inclui as dependências de browser de AJAX Olá e dependências do lado do servidor. Se o relatório telemetria de dependência personalizado com Olá TrackDependency API, também aparecem aqui. Pode selecionar Olá dependências tooshow num mapa Olá. Atualmente esta seleção não filtrar pedidos do lado do servidor de Olá ou vistas de página do lado do cliente Olá.

![Conjunto de filtros](./media/app-insights-app-map/11.png)

## <a name="save-filters"></a>Guardar filtros
filtros de Olá toosave tiver aplicado, Olá pin filtrado vista para um [dashboard](app-insights-dashboards.md).

![PIN toodashboard](./media/app-insights-app-map/12.png)

## <a name="error-pane"></a>Painel de erro
Quando clicar num nó de mapa de Olá, um painel de erro é apresentado no lado direito Olá resumir falhas para esse nó. Falhas são agrupadas primeiro por ID de operação e, em seguida, agrupadas por ID do problema.

![Painel de erro](./media/app-insights-app-map/error-pane.png)

Clicar numa falha leva-o toohello instância mais recente do que falha.

## <a name="resource-health"></a>Estado de funcionamento de recursos
Alguns tipos de recurso, o estado de funcionamento do recurso é apresentado, Olá parte superior do painel de erro Olá. Por exemplo, clicando num nó do SQL Server irá mostrar o estado de funcionamento do Olá da base de dados e todos os alertas que tenham desencadeou.

![Estado de funcionamento de recursos](./media/app-insights-app-map/resource-health.png)

Pode clicar em métricas descrição geral de padrão tooview de nome de recurso de Olá para esse recurso.

## <a name="end-to-end-system-app-maps"></a>Mapas de aplicação de sistema de ponto a ponto

*Requer SDK versão 2.3 ou superior*

Se a aplicação tem vários componentes - por exemplo, um serviço de back-end além toohello aplicação de web -, em seguida, que pode apresentá-las a todos os num mapa de uma aplicação integrada.

![Conjunto de filtros](./media/app-insights-app-map/multi-component-app-map.png)

mapa de aplicação Olá localiza nós do servidor seguindo quaisquer chamadas de dependência HTTP feitas entre servidores com Olá que Application Insights SDK instalado. Cada recurso do Application Insights é assumido toocontain um servidor.

### <a name="multi-role-app-map-preview"></a>Mapa de aplicação de função multi (pré-visualização)

funcionalidade de mapa de aplicação de função multi de pré-visualização Olá permite-lhe toouse Olá aplicação mapa com vários servidores de envio de dados toohello mesmo recurso do Application Insights / chave de instrumentação. Servidores no mapa de Olá são segmentados pela propriedade de cloud_RoleName Olá em itens de telemetria. Definir *mapa de aplicação de função Multi* demasiado*no* de Olá pré-visualizações painel tooenable esta configuração.

Esta abordagem poderá ser pretendida numa aplicação microserviços ou noutros cenários onde pretende que os eventos de toocorrelate em vários servidores dentro de um único recurso do Application Insights.

## <a name="video"></a>Vídeo

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player] 

## <a name="feedback"></a>Comentários
Forneça comentários através da opção de portal comentários de Olá.

![Imagem de MapLink-1](./media/app-insights-app-map/13.png)


## <a name="next-steps"></a>Passos seguintes

* [Portal do Azure](https://portal.azure.com)
