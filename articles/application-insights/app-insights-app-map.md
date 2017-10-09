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
# <a name="application-map-in-application-insights"></a><span data-ttu-id="b6b14-103">Mapa de aplicação no Application Insights</span><span class="sxs-lookup"><span data-stu-id="b6b14-103">Application Map in Application Insights</span></span>
<span data-ttu-id="b6b14-104">No [Azure Application Insights](app-insights-overview.md), o mapeamento de aplicações é um esquema visual de relações de dependência de Olá dos componentes da aplicação.</span><span class="sxs-lookup"><span data-stu-id="b6b14-104">In [Azure Application Insights](app-insights-overview.md), Application Map is a visual layout of hello dependency relationships of your application components.</span></span> <span data-ttu-id="b6b14-105">Cada componente mostra KPIs, tais como toohelp de carga, desempenho, falhas e os alertas, detetar qualquer componente causar um problema de desempenho ou a falha.</span><span class="sxs-lookup"><span data-stu-id="b6b14-105">Each component shows KPIs such as load, performance, failures, and alerts, toohelp you discover any component causing a performance issue or failure.</span></span> <span data-ttu-id="b6b14-106">Pode clicar sucessivamente de qualquer componente toomore detalhadas de diagnóstico, tais como eventos do Application Insights.</span><span class="sxs-lookup"><span data-stu-id="b6b14-106">You can click through from any component toomore detailed diagnostics, such as Application Insights events.</span></span> <span data-ttu-id="b6b14-107">Se a sua aplicação utiliza serviços do Azure, também pode clicar sucessivamente tooAzure diagnostics, manutenção automática, tais como recomendações do Assistente de base de dados do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="b6b14-107">If your app uses Azure services, you can also click through tooAzure diagnostics, such as SQL Database Advisor recommendations.</span></span>

<span data-ttu-id="b6b14-108">Como outros gráficos, pode afixar um toohello de mapa de aplicação dashboard do Azure, onde este fica totalmente funcional.</span><span class="sxs-lookup"><span data-stu-id="b6b14-108">Like other charts, you can pin an application map toohello Azure dashboard, where it is fully functional.</span></span> 

## <a name="open-hello-application-map"></a><span data-ttu-id="b6b14-109">Mapa de aplicação Olá aberta</span><span class="sxs-lookup"><span data-stu-id="b6b14-109">Open hello application map</span></span>
<span data-ttu-id="b6b14-110">Mapa de Olá aberto a partir do painel de descrição geral de Olá para a sua aplicação:</span><span class="sxs-lookup"><span data-stu-id="b6b14-110">Open hello map from hello overview blade for your application:</span></span>

![Abra o mapa de aplicação](./media/app-insights-app-map/01.png)

![mapa de aplicação](./media/app-insights-app-map/02.png)

<span data-ttu-id="b6b14-113">mapa de Olá mostra:</span><span class="sxs-lookup"><span data-stu-id="b6b14-113">hello map shows:</span></span>

* <span data-ttu-id="b6b14-114">Testes de disponibilidade</span><span class="sxs-lookup"><span data-stu-id="b6b14-114">Availability tests</span></span>
* <span data-ttu-id="b6b14-115">Componente do lado do cliente (monitorizado com Olá JavaScript SDK)</span><span class="sxs-lookup"><span data-stu-id="b6b14-115">Client-side component (monitored with hello JavaScript SDK)</span></span>
* <span data-ttu-id="b6b14-116">Componente do lado do servidor</span><span class="sxs-lookup"><span data-stu-id="b6b14-116">Server-side component</span></span>
* <span data-ttu-id="b6b14-117">Dependências de componentes de cliente e servidor Olá</span><span class="sxs-lookup"><span data-stu-id="b6b14-117">Dependencies of hello client and server components</span></span>

<span data-ttu-id="b6b14-118">Pode expandir e fechar a grupos de ligação de dependência:</span><span class="sxs-lookup"><span data-stu-id="b6b14-118">You can expand and collapse dependency link groups:</span></span>

![Fechar](./media/app-insights-app-map/03.png)

<span data-ttu-id="b6b14-120">Se tiver uma grande quantidade de dependências de um tipo (SQL Server, etc. HTTP), que possam aparecer agrupados.</span><span class="sxs-lookup"><span data-stu-id="b6b14-120">If you have many dependencies of one type (SQL, HTTP etc.), they may appear grouped.</span></span> 

![dependências agrupadas](./media/app-insights-app-map/03-2.png)

## <a name="spot-problems"></a><span data-ttu-id="b6b14-122">Problemas de lugar para cima</span><span class="sxs-lookup"><span data-stu-id="b6b14-122">Spot problems</span></span>
<span data-ttu-id="b6b14-123">Cada nó tem indicadores de desempenho relevantes, tais como as taxas de carga, desempenho e falha Olá desse componente.</span><span class="sxs-lookup"><span data-stu-id="b6b14-123">Each node has relevant performance indicators, such as hello load, performance, and failure rates for that component.</span></span> 

<span data-ttu-id="b6b14-124">Ícones de aviso destacar informações sobre problemas possíveis.</span><span class="sxs-lookup"><span data-stu-id="b6b14-124">Warning icons highlight possible problems.</span></span> <span data-ttu-id="b6b14-125">Um aviso laranja significa que existem falhas nos pedidos, vistas de página ou chamadas de dependência.</span><span class="sxs-lookup"><span data-stu-id="b6b14-125">An orange warning means there are failures in requests, page views or dependency calls.</span></span> <span data-ttu-id="b6b14-126">Vermelho significa uma taxa de falhas superior a 5%.</span><span class="sxs-lookup"><span data-stu-id="b6b14-126">Red means a failure rate above 5%.</span></span> <span data-ttu-id="b6b14-127">Se quiser tooadjust estes limiares, abra as opções.</span><span class="sxs-lookup"><span data-stu-id="b6b14-127">If you want tooadjust these thresholds, open Options.</span></span>

![ícones de falha](./media/app-insights-app-map/04.png)

<span data-ttu-id="b6b14-129">Active Directory também alertas Mostrar cópias de segurança:</span><span class="sxs-lookup"><span data-stu-id="b6b14-129">Active alerts also show up:</span></span> 

![alertas ativos](./media/app-insights-app-map/05.png)

<span data-ttu-id="b6b14-131">Se utilizar o SQL Azure, há um ícone que mostra quando existem recomendações sobre como melhorar o desempenho.</span><span class="sxs-lookup"><span data-stu-id="b6b14-131">If you use SQL Azure, there's an icon that shows when there are recommendations on how you can improve performance.</span></span> 

![recomendação do Azure](./media/app-insights-app-map/06.png)

<span data-ttu-id="b6b14-133">Clique em qualquer tooget ícone mais detalhes:</span><span class="sxs-lookup"><span data-stu-id="b6b14-133">Click any icon tooget more details:</span></span>

![recomendação do Azure](./media/app-insights-app-map/07.png)

## <a name="diagnostic-click-through"></a><span data-ttu-id="b6b14-135">Clique em diagnóstico através do</span><span class="sxs-lookup"><span data-stu-id="b6b14-135">Diagnostic click through</span></span>
<span data-ttu-id="b6b14-136">Cada um de nós de Olá num mapa Olá oferece clique visado através de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="b6b14-136">Each of hello nodes on hello map offers targeted click through for diagnostics.</span></span> <span data-ttu-id="b6b14-137">Opções de Olá variam consoante o tipo de Olá do nó de Olá.</span><span class="sxs-lookup"><span data-stu-id="b6b14-137">hello options vary depending on hello type of hello node.</span></span>

![Opções de servidor](./media/app-insights-app-map/09.png)

<span data-ttu-id="b6b14-139">Para os componentes que estão alojados no Azure, as opções de Olá incluem hiperligações diretas toothem.</span><span class="sxs-lookup"><span data-stu-id="b6b14-139">For components that are hosted in Azure, hello options include direct links toothem.</span></span>

## <a name="filters-and-time-range"></a><span data-ttu-id="b6b14-140">Filtros e o intervalo de tempo</span><span class="sxs-lookup"><span data-stu-id="b6b14-140">Filters and time range</span></span>
<span data-ttu-id="b6b14-141">Por predefinição, o mapa de Olá resume todos os dados de Olá disponíveis para Olá escolhido o intervalo de tempo.</span><span class="sxs-lookup"><span data-stu-id="b6b14-141">By default, hello map summarizes all hello data available for hello chosen time range.</span></span> <span data-ttu-id="b6b14-142">Mas pode filtrar os nomes de operações específicas apenas de tooinclude ou dependências.</span><span class="sxs-lookup"><span data-stu-id="b6b14-142">But you can filter it tooinclude only specific operation names or dependencies.</span></span>

* <span data-ttu-id="b6b14-143">Nome da operação: inclui os vistas de página e os tipos de pedido do lado do servidor.</span><span class="sxs-lookup"><span data-stu-id="b6b14-143">Operation name: This includes both page views and server-side request types.</span></span> <span data-ttu-id="b6b14-144">Com esta opção, Olá mapa mostra Olá KPI no nó do lado do servidor/cliente Olá para apenas operações de Olá selecionado.</span><span class="sxs-lookup"><span data-stu-id="b6b14-144">With this option, hello map shows hello KPI on hello server/client-side node for hello selected operations only.</span></span> <span data-ttu-id="b6b14-145">Mostra as dependências de Olá chamadas no contexto de Olá dessas operações específicas.</span><span class="sxs-lookup"><span data-stu-id="b6b14-145">It shows hello dependencies called in hello context of those specific operations.</span></span>
* <span data-ttu-id="b6b14-146">Nome de base de dependência: Isto inclui as dependências de browser de AJAX Olá e dependências do lado do servidor.</span><span class="sxs-lookup"><span data-stu-id="b6b14-146">Dependency base name: This includes hello AJAX browser dependencies and server-side dependencies.</span></span> <span data-ttu-id="b6b14-147">Se o relatório telemetria de dependência personalizado com Olá TrackDependency API, também aparecem aqui.</span><span class="sxs-lookup"><span data-stu-id="b6b14-147">If you report custom dependency telemetry with hello TrackDependency API, they also appear here.</span></span> <span data-ttu-id="b6b14-148">Pode selecionar Olá dependências tooshow num mapa Olá.</span><span class="sxs-lookup"><span data-stu-id="b6b14-148">You can select hello dependencies tooshow on hello map.</span></span> <span data-ttu-id="b6b14-149">Atualmente esta seleção não filtrar pedidos do lado do servidor de Olá ou vistas de página do lado do cliente Olá.</span><span class="sxs-lookup"><span data-stu-id="b6b14-149">Currently this selection does not filter hello server-side requests, or hello client-side page views.</span></span>

![Conjunto de filtros](./media/app-insights-app-map/11.png)

## <a name="save-filters"></a><span data-ttu-id="b6b14-151">Guardar filtros</span><span class="sxs-lookup"><span data-stu-id="b6b14-151">Save filters</span></span>
<span data-ttu-id="b6b14-152">filtros de Olá toosave tiver aplicado, Olá pin filtrado vista para um [dashboard](app-insights-dashboards.md).</span><span class="sxs-lookup"><span data-stu-id="b6b14-152">toosave hello filters you have applied, pin hello filtered view onto a [dashboard](app-insights-dashboards.md).</span></span>

![PIN toodashboard](./media/app-insights-app-map/12.png)

## <a name="error-pane"></a><span data-ttu-id="b6b14-154">Painel de erro</span><span class="sxs-lookup"><span data-stu-id="b6b14-154">Error pane</span></span>
<span data-ttu-id="b6b14-155">Quando clicar num nó de mapa de Olá, um painel de erro é apresentado no lado direito Olá resumir falhas para esse nó.</span><span class="sxs-lookup"><span data-stu-id="b6b14-155">When you click a node in hello map, an error pane is displayed on hello right-hand side summarizing failures for that node.</span></span> <span data-ttu-id="b6b14-156">Falhas são agrupadas primeiro por ID de operação e, em seguida, agrupadas por ID do problema.</span><span class="sxs-lookup"><span data-stu-id="b6b14-156">Failures are grouped first by operation ID and then grouped by problem ID.</span></span>

![Painel de erro](./media/app-insights-app-map/error-pane.png)

<span data-ttu-id="b6b14-158">Clicar numa falha leva-o toohello instância mais recente do que falha.</span><span class="sxs-lookup"><span data-stu-id="b6b14-158">Clicking on a failure takes you toohello most recent instance of that failure.</span></span>

## <a name="resource-health"></a><span data-ttu-id="b6b14-159">Estado de funcionamento de recursos</span><span class="sxs-lookup"><span data-stu-id="b6b14-159">Resource health</span></span>
<span data-ttu-id="b6b14-160">Alguns tipos de recurso, o estado de funcionamento do recurso é apresentado, Olá parte superior do painel de erro Olá.</span><span class="sxs-lookup"><span data-stu-id="b6b14-160">For some resource types, resource health is displayed at hello top of hello error pane.</span></span> <span data-ttu-id="b6b14-161">Por exemplo, clicando num nó do SQL Server irá mostrar o estado de funcionamento do Olá da base de dados e todos os alertas que tenham desencadeou.</span><span class="sxs-lookup"><span data-stu-id="b6b14-161">For example, clicking a SQL node will show hello database health and any alerts that have fired.</span></span>

![Estado de funcionamento de recursos](./media/app-insights-app-map/resource-health.png)

<span data-ttu-id="b6b14-163">Pode clicar em métricas descrição geral de padrão tooview de nome de recurso de Olá para esse recurso.</span><span class="sxs-lookup"><span data-stu-id="b6b14-163">You can click hello resource name tooview standard overview metrics for that resource.</span></span>

## <a name="end-to-end-system-app-maps"></a><span data-ttu-id="b6b14-164">Mapas de aplicação de sistema de ponto a ponto</span><span class="sxs-lookup"><span data-stu-id="b6b14-164">End-to-end system app maps</span></span>

<span data-ttu-id="b6b14-165">*Requer SDK versão 2.3 ou superior*</span><span class="sxs-lookup"><span data-stu-id="b6b14-165">*Requires SDK version 2.3 or higher*</span></span>

<span data-ttu-id="b6b14-166">Se a aplicação tem vários componentes - por exemplo, um serviço de back-end além toohello aplicação de web -, em seguida, que pode apresentá-las a todos os num mapa de uma aplicação integrada.</span><span class="sxs-lookup"><span data-stu-id="b6b14-166">If your application has several components - for example, a back-end service in addition toohello web app - then you can show them all on one integrated app map.</span></span>

![Conjunto de filtros](./media/app-insights-app-map/multi-component-app-map.png)

<span data-ttu-id="b6b14-168">mapa de aplicação Olá localiza nós do servidor seguindo quaisquer chamadas de dependência HTTP feitas entre servidores com Olá que Application Insights SDK instalado.</span><span class="sxs-lookup"><span data-stu-id="b6b14-168">hello app map finds server nodes by following any HTTP dependency calls made between servers with hello Application Insights SDK installed.</span></span> <span data-ttu-id="b6b14-169">Cada recurso do Application Insights é assumido toocontain um servidor.</span><span class="sxs-lookup"><span data-stu-id="b6b14-169">Each Application Insights resource is assumed toocontain one server.</span></span>

### <a name="multi-role-app-map-preview"></a><span data-ttu-id="b6b14-170">Mapa de aplicação de função multi (pré-visualização)</span><span class="sxs-lookup"><span data-stu-id="b6b14-170">Multi-role app map (preview)</span></span>

<span data-ttu-id="b6b14-171">funcionalidade de mapa de aplicação de função multi de pré-visualização Olá permite-lhe toouse Olá aplicação mapa com vários servidores de envio de dados toohello mesmo recurso do Application Insights / chave de instrumentação.</span><span class="sxs-lookup"><span data-stu-id="b6b14-171">hello preview multi-role app map feature allows you toouse hello app map with multiple servers sending data toohello same Application Insights resource  / instrumentation key.</span></span> <span data-ttu-id="b6b14-172">Servidores no mapa de Olá são segmentados pela propriedade de cloud_RoleName Olá em itens de telemetria.</span><span class="sxs-lookup"><span data-stu-id="b6b14-172">Servers in hello map are segmented by hello cloud_RoleName property on telemetry items.</span></span> <span data-ttu-id="b6b14-173">Definir *mapa de aplicação de função Multi* demasiado*no* de Olá pré-visualizações painel tooenable esta configuração.</span><span class="sxs-lookup"><span data-stu-id="b6b14-173">Set *Multi-role Application Map* too*On* from hello Previews blade tooenable this configuration.</span></span>

<span data-ttu-id="b6b14-174">Esta abordagem poderá ser pretendida numa aplicação microserviços ou noutros cenários onde pretende que os eventos de toocorrelate em vários servidores dentro de um único recurso do Application Insights.</span><span class="sxs-lookup"><span data-stu-id="b6b14-174">This approach may be desired in a micro-services application, or in other scenarios where you want toocorrelate events across multiple servers within a single Application Insights resource.</span></span>

## <a name="video"></a><span data-ttu-id="b6b14-175">Vídeo</span><span class="sxs-lookup"><span data-stu-id="b6b14-175">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player] 

## <a name="feedback"></a><span data-ttu-id="b6b14-176">Comentários</span><span class="sxs-lookup"><span data-stu-id="b6b14-176">Feedback</span></span>
<span data-ttu-id="b6b14-177">Forneça comentários através da opção de portal comentários de Olá.</span><span class="sxs-lookup"><span data-stu-id="b6b14-177">Please provide feedback through hello portal feedback option.</span></span>

![Imagem de MapLink-1](./media/app-insights-app-map/13.png)


## <a name="next-steps"></a><span data-ttu-id="b6b14-179">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="b6b14-179">Next steps</span></span>

* [<span data-ttu-id="b6b14-180">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="b6b14-180">Azure portal</span></span>](https://portal.azure.com)
