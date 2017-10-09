---
title: "aaaAzure Application Insights suporte para vários componentes, micro-serviços e contentores | Microsoft Docs"
description: "Monitorização de aplicações que consistem em vários componentes do ou funções para o desempenho e utilização."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 05/17/2017
ms.author: bwren
ms.openlocfilehash: 6185eedf32ec450d7541603b94de6c3dcdf64a85
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-multi-component-applications-with-application-insights-preview"></a><span data-ttu-id="2e2a6-103">Monitorizar aplicações com múltiplos componente com o Application Insights (pré-visualização)</span><span class="sxs-lookup"><span data-stu-id="2e2a6-103">Monitor multi-component applications with Application Insights (preview)</span></span>

<span data-ttu-id="2e2a6-104">Pode monitorizar as aplicações que consistem de vários componentes de servidor, funções ou serviços com [Azure Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="2e2a6-104">You can monitor apps that consist of multiple server components, roles, or services with [Azure Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="2e2a6-105">Estado de funcionamento de Olá dos componentes de Olá e relações de Olá entre eles são apresentados num mapa de aplicação único.</span><span class="sxs-lookup"><span data-stu-id="2e2a6-105">hello health of hello components and hello relationships between them are displayed on a single Application Map.</span></span> <span data-ttu-id="2e2a6-106">Pode analisar individuais operações através de vários componentes com a correlação de HTTP automática.</span><span class="sxs-lookup"><span data-stu-id="2e2a6-106">You can trace individual operations through multiple components with automatic HTTP correlation.</span></span> <span data-ttu-id="2e2a6-107">Diagnóstico de contentor pode ser integrado e correlacionado com a telemetria da aplicação.</span><span class="sxs-lookup"><span data-stu-id="2e2a6-107">Container diagnostics can be integrated and correlated with application telemetry.</span></span> <span data-ttu-id="2e2a6-108">Utilize um único recurso do Application Insights para todos os componentes de Olá da sua aplicação.</span><span class="sxs-lookup"><span data-stu-id="2e2a6-108">Use a single Application Insights resource for all hello components of your application.</span></span> 

![Mapa de múltiplos componente da aplicação](./media/app-insights-monitor-multi-role-apps/app-map.png)

<span data-ttu-id="2e2a6-110">Utilizamos 'componente' toomean aqui qualquer parte de uma aplicação grande funcionar.</span><span class="sxs-lookup"><span data-stu-id="2e2a6-110">We use 'component' here toomean any functioning part of a large application.</span></span> <span data-ttu-id="2e2a6-111">Por exemplo, uma aplicação comercial normal pode consistir em código de cliente em execução nos browsers da web, falar com tooone ou mais serviços de aplicação web, que por sua vez voltar a utilizar serviços de fim.</span><span class="sxs-lookup"><span data-stu-id="2e2a6-111">For example, a typical business application may consist of client code running in web browsers, talking tooone or more web app services, which in turn use back end services.</span></span> <span data-ttu-id="2e2a6-112">Componentes de servidor podem ser alojado no local na nuvem de Olá, poderão ser funções da web e de trabalho do Azure ou podem executar nos contentores, tais como Docker ou de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="2e2a6-112">Server components may be hosted on-premises on in hello cloud, or may be Azure web and worker roles, or may run in containers such as Docker or Service Fabric.</span></span> 

### <a name="sharing-a-single-application-insights-resource"></a><span data-ttu-id="2e2a6-113">Partilhar um único recurso do Application Insights</span><span class="sxs-lookup"><span data-stu-id="2e2a6-113">Sharing a single Application Insights resource</span></span> 

<span data-ttu-id="2e2a6-114">Olá chave técnica aqui é toosend a telemetria de cada componente no seu toohello aplicação mesmo recurso do Application Insights, mas utilize Olá `cloud_RoleName` componentes de toodistinguish propriedade quando for necessário.</span><span class="sxs-lookup"><span data-stu-id="2e2a6-114">hello key technique here is toosend telemetry from every component in your application toohello same Application Insights resource, but use hello `cloud_RoleName` property toodistinguish components when necessary.</span></span> <span data-ttu-id="2e2a6-115">Olá Application Insights SDK adiciona Olá `cloud_RoleName` emissão de componentes de telemetria de toohello de propriedade.</span><span class="sxs-lookup"><span data-stu-id="2e2a6-115">hello Application Insights SDK adds hello `cloud_RoleName` property toohello telemetry components emit.</span></span> <span data-ttu-id="2e2a6-116">Por exemplo, Olá SDK irá adicionar um nome do web site ou toohello de nome de função de serviço `cloud_RoleName` propriedade.</span><span class="sxs-lookup"><span data-stu-id="2e2a6-116">For example, hello SDK will add a web site name, or service role name toohello `cloud_RoleName` property.</span></span> <span data-ttu-id="2e2a6-117">Pode substituir este valor com um telemetryinitializer.</span><span class="sxs-lookup"><span data-stu-id="2e2a6-117">You can override this value with a telemetryinitializer.</span></span> <span data-ttu-id="2e2a6-118">Olá o mapeamento de aplicações utiliza Olá `cloud_RoleName` propriedade tooidentify Olá componentes mapa Olá.</span><span class="sxs-lookup"><span data-stu-id="2e2a6-118">hello Application Map uses hello `cloud_RoleName` property tooidentify hello components on hello map.</span></span>

<span data-ttu-id="2e2a6-119">Para obter mais informações sobre como substituir Olá `cloud_RoleName` propriedade consulte [adicionar propriedades: ITelemetryInitializer](app-insights-api-filtering-sampling.md#add-properties-itelemetryinitializer).</span><span class="sxs-lookup"><span data-stu-id="2e2a6-119">For more information about how do override hello `cloud_RoleName` property see [Add properties: ITelemetryInitializer](app-insights-api-filtering-sampling.md#add-properties-itelemetryinitializer).</span></span>  

<span data-ttu-id="2e2a6-120">Em alguns casos, este não poderá ser apropriado e pode preferir toouse recursos separados para diferentes grupos de componentes.</span><span class="sxs-lookup"><span data-stu-id="2e2a6-120">In some cases, this may not be appropriate, and you may prefer toouse separate resources for different groups of components.</span></span> <span data-ttu-id="2e2a6-121">Por exemplo, poderá ter toouse diferentes recursos de gestão ou fins de faturação.</span><span class="sxs-lookup"><span data-stu-id="2e2a6-121">For example, you might need toouse different resources for management or billing purposes.</span></span> <span data-ttu-id="2e2a6-122">Utilizar recursos separados significa que não veja todos os componentes de Olá apresentados num mapa de aplicação único; e que não é possível consultar componentes no [análise](app-insights-analytics.md).</span><span class="sxs-lookup"><span data-stu-id="2e2a6-122">Using separate resources means that you don't see all hello components displayed on a single Application Map; and that you can't query across components in [Analytics](app-insights-analytics.md).</span></span> <span data-ttu-id="2e2a6-123">Também tem tooset recursos separado Olá.</span><span class="sxs-lookup"><span data-stu-id="2e2a6-123">You also have tooset up hello separate resources.</span></span>

<span data-ttu-id="2e2a6-124">Com esse advertência, iremos assumir resto Olá deste documento que pretende que os dados de toosend de vários componentes tooone recurso do Application Insights.</span><span class="sxs-lookup"><span data-stu-id="2e2a6-124">With that caveat, we'll assume in hello rest of this document that you want toosend data from multiple components tooone Application Insights resource.</span></span>

## <a name="configure-multi-component-applications"></a><span data-ttu-id="2e2a6-125">Configurar aplicações com múltiplos componente</span><span class="sxs-lookup"><span data-stu-id="2e2a6-125">Configure multi-component applications</span></span>

<span data-ttu-id="2e2a6-126">mapa de uma aplicação com múltiplos componente tooget, tem de tooachieve estes objetivos:</span><span class="sxs-lookup"><span data-stu-id="2e2a6-126">tooget a multi-component application map, you need tooachieve these goals:</span></span>

* <span data-ttu-id="2e2a6-127">**Instalar a versão de pré-lançamento mais recente Olá** pacote do Application Insights em cada componente da aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="2e2a6-127">**Install hello latest pre-release** Application Insights package in each component of hello application.</span></span> 
* <span data-ttu-id="2e2a6-128">**Partilhar um único recurso do Application Insights** para Olá todos os componentes da aplicação.</span><span class="sxs-lookup"><span data-stu-id="2e2a6-128">**Share a single Application Insights resource** for all hello components of your application.</span></span>
* <span data-ttu-id="2e2a6-129">**Ativar o mapa de aplicação de função Multi** no painel de pré-visualizações Olá.</span><span class="sxs-lookup"><span data-stu-id="2e2a6-129">**Enable Multi-role Application Map** in hello Previews blade.</span></span>

<span data-ttu-id="2e2a6-130">Configure cada componente da aplicação utilizando o método adequado Olá para o respetivo tipo.</span><span class="sxs-lookup"><span data-stu-id="2e2a6-130">Configure each component of your application using hello appropriate method for its type.</span></span> <span data-ttu-id="2e2a6-131">([ASP.NET](app-insights-asp-net.md), [Java](app-insights-java-get-started.md), [Node.js](app-insights-nodejs.md), [JavaScript](app-insights-javascript.md).)</span><span class="sxs-lookup"><span data-stu-id="2e2a6-131">([ASP.NET](app-insights-asp-net.md), [Java](app-insights-java-get-started.md), [Node.js](app-insights-nodejs.md), [JavaScript](app-insights-javascript.md).)</span></span>

### <a name="1-install-hello-latest-pre-release-package"></a><span data-ttu-id="2e2a6-132">1. Instalar o pacote de versão de pré-lançamento Olá mais recente</span><span class="sxs-lookup"><span data-stu-id="2e2a6-132">1. Install hello latest pre-release package</span></span>

<span data-ttu-id="2e2a6-133">Atualizar ou instalar pacotes de Appication Insights Olá no projeto de Olá para cada componente do servidor.</span><span class="sxs-lookup"><span data-stu-id="2e2a6-133">Update or install hello Appication Insights packages in hello project for each server component.</span></span> <span data-ttu-id="2e2a6-134">Se estiver a utilizar o Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="2e2a6-134">If you're using Visual Studio:</span></span>

1. <span data-ttu-id="2e2a6-135">Um projeto com o botão direito e selecione **gerir pacotes NuGet**.</span><span class="sxs-lookup"><span data-stu-id="2e2a6-135">Right-click a project and select **Manage NuGet Packages**.</span></span> 
2. <span data-ttu-id="2e2a6-136">Selecione **incluir pré-lançamento**.</span><span class="sxs-lookup"><span data-stu-id="2e2a6-136">Select **Include prerelease**.</span></span>
3. <span data-ttu-id="2e2a6-137">Se o Application Insights pacotes são apresentados nas atualizações, selecione-os.</span><span class="sxs-lookup"><span data-stu-id="2e2a6-137">If Application Insights packages appear in Updates, select them.</span></span> 

    <span data-ttu-id="2e2a6-138">Caso contrário, procurar e instalar pacote adequado Olá:</span><span class="sxs-lookup"><span data-stu-id="2e2a6-138">Otherwise, browse for and install hello appropriate package:</span></span>
    
    * <span data-ttu-id="2e2a6-139">Microsoft.ApplicationInsights.WindowsServer</span><span class="sxs-lookup"><span data-stu-id="2e2a6-139">Microsoft.ApplicationInsights.WindowsServer</span></span>
    * <span data-ttu-id="2e2a6-140">Microsoft.ApplicationInsights.ServiceFabric - de componentes em execução como convidado executáveis e contentores de Docker a executar uma aplicação de Service Fabric em</span><span class="sxs-lookup"><span data-stu-id="2e2a6-140">Microsoft.ApplicationInsights.ServiceFabric - for components running as guest executables and Docker containers running a in Service Fabric application</span></span>
    * <span data-ttu-id="2e2a6-141">Microsoft.ApplicationInsights.ServiceFabric.Native - fiável dos serviços de no ServiceFabric aplicações</span><span class="sxs-lookup"><span data-stu-id="2e2a6-141">Microsoft.ApplicationInsights.ServiceFabric.Native - for reliable services in ServiceFabric applications</span></span>
    * <span data-ttu-id="2e2a6-142">Microsoft.ApplicationInsights.Kubernetes de componentes em execução no Docker Kubernetes</span><span class="sxs-lookup"><span data-stu-id="2e2a6-142">Microsoft.ApplicationInsights.Kubernetes for components running in Docker on Kubernetes</span></span>

### <a name="2-share-a-single-application-insights-resource"></a><span data-ttu-id="2e2a6-143">2. Partilhar um único recurso do Application Insights</span><span class="sxs-lookup"><span data-stu-id="2e2a6-143">2. Share a single Application Insights resource</span></span>

* <span data-ttu-id="2e2a6-144">No Visual Studio, clique com o botão direito um projeto e selecione **configurar o Application Insights**, ou **Application Insights > configurar**.</span><span class="sxs-lookup"><span data-stu-id="2e2a6-144">In Visual Studio, right-click a project and select **Configure Application Insights**, or **Application Insights > Configure**.</span></span> <span data-ttu-id="2e2a6-145">Para o primeiro projeto Olá, utilize Olá assistente toocreate um recurso do Application Insights.</span><span class="sxs-lookup"><span data-stu-id="2e2a6-145">For hello first project, use hello wizard toocreate an Application Insights resource.</span></span> <span data-ttu-id="2e2a6-146">Para projetos subsequentes, selecione Olá mesmo recurso.</span><span class="sxs-lookup"><span data-stu-id="2e2a6-146">For subsequent projects, select hello same resource.</span></span>
* <span data-ttu-id="2e2a6-147">Se não houver nenhuma menu do Application Insights, configure manualmente:</span><span class="sxs-lookup"><span data-stu-id="2e2a6-147">If there is no Application Insights menu, configure manually:</span></span>

   1. <span data-ttu-id="2e2a6-148">No [portal do Azure](https://portal,azure.com), abra o recurso do Application Insights Olá já criado para outro componente.</span><span class="sxs-lookup"><span data-stu-id="2e2a6-148">In [Azure portal](https://portal,azure.com), open hello Application Insights resource you already created for another component.</span></span>
   2. <span data-ttu-id="2e2a6-149">No painel de descrição geral de Olá, separador de abrir Olá pendente Essentials e Olá cópia **chave de instrumentação.**</span><span class="sxs-lookup"><span data-stu-id="2e2a6-149">In hello Overview blade, open hello Essentials drop-down tab, and copy hello **Instrumentation Key.**</span></span>
   3. <span data-ttu-id="2e2a6-150">No seu projeto, abra Applicationinsights e inserir:`<InstrumentationKey>your copied key</InstrumentationKey>`</span><span class="sxs-lookup"><span data-stu-id="2e2a6-150">In your project, open ApplicationInsights.config and insert: `<InstrumentationKey>your copied key</InstrumentationKey>`</span></span>

![Copiar ficheiro. config do Olá instrumentação toohello chave](./media/app-insights-monitor-multi-role-apps/copy-instrumentation-key.png)


### <a name="3-enable-multi-role-application-map"></a><span data-ttu-id="2e2a6-152">3. Ativar função multi o mapeamento de aplicações</span><span class="sxs-lookup"><span data-stu-id="2e2a6-152">3. Enable multi-role Application Map</span></span>

<span data-ttu-id="2e2a6-153">No portal do Azure Olá, abra o recurso Olá para a sua aplicação.</span><span class="sxs-lookup"><span data-stu-id="2e2a6-153">In hello Azure portal, open hello resource for your application.</span></span> <span data-ttu-id="2e2a6-154">No painel de pré-visualizações Olá, ativar *mapa de aplicação de função Multi*.</span><span class="sxs-lookup"><span data-stu-id="2e2a6-154">In hello Previews blade, enable *Multi-role Application Map*.</span></span>

### <a name="4-enable-docker-metrics-optional"></a><span data-ttu-id="2e2a6-155">4. Ativar as métricas de Docker (opcional)</span><span class="sxs-lookup"><span data-stu-id="2e2a6-155">4. Enable Docker metrics (Optional)</span></span> 

<span data-ttu-id="2e2a6-156">Se um componente é executado num Docker alojada em VM Windows do Azure, pode recolher métricas adicionais do contentor de Olá.</span><span class="sxs-lookup"><span data-stu-id="2e2a6-156">If a component runs in a Docker hosted on an Azure Windows VM, you can collect additional metrics from hello container.</span></span> <span data-ttu-id="2e2a6-157">Insira-o no seu [diagnóstico do Azure](../monitoring-and-diagnostics/azure-diagnostics.md) ficheiro de configuração:</span><span class="sxs-lookup"><span data-stu-id="2e2a6-157">Insert this in your [Azure diagnostics](../monitoring-and-diagnostics/azure-diagnostics.md) configuration file:</span></span>

```
"DiagnosticMonitorConfiguration": {
        ...
        "sinks": "applicationInsights",
        "DockerSources": {
                "Stats": {
                    "enabled": true,
                    "sampleRate": "PT1M"
                }
            },
        ...
    }
    ...   
    "SinksConfig": {
        "Sink": [{
            "name": "applicationInsights",
            "ApplicationInsights": "<your instrumentation key here>"
        }]
    }
    ...
}

```

## <a name="use-cloudrolename-tooseparate-components"></a><span data-ttu-id="2e2a6-158">Utilizar cloud_RoleName tooseparate componentes</span><span class="sxs-lookup"><span data-stu-id="2e2a6-158">Use cloud_RoleName tooseparate components</span></span>

<span data-ttu-id="2e2a6-159">Olá `cloud_RoleName` propriedade é anexado tooall telemetria.</span><span class="sxs-lookup"><span data-stu-id="2e2a6-159">hello `cloud_RoleName` property is attached tooall telemetry.</span></span> <span data-ttu-id="2e2a6-160">Identifica componente Olá - serviço ou função Olá - que origina telemetria Olá.</span><span class="sxs-lookup"><span data-stu-id="2e2a6-160">It identifies hello component - hello role or service - that originates hello telemetry.</span></span> <span data-ttu-id="2e2a6-161">(É não Olá mesmo como cloud_RoleInstance, que separa idênticas funções que estejam a executar em paralelo em vários processos de servidor ou máquinas.)</span><span class="sxs-lookup"><span data-stu-id="2e2a6-161">(It is not hello same as cloud_RoleInstance, which separates identical roles that are running in parallel on multiple server processes or machines.)</span></span>

<span data-ttu-id="2e2a6-162">No portal de Olá, pode filtrar ou segmentar a telemetria com esta propriedade.</span><span class="sxs-lookup"><span data-stu-id="2e2a6-162">In hello portal, you can filter or segment your telemetry using this property.</span></span> <span data-ttu-id="2e2a6-163">Neste exemplo, o painel de falhas de Olá é tooshow filtrado informações apenas do serviço de front-end web Olá, filtragem de falhas de back-end de API do CRM de Olá:</span><span class="sxs-lookup"><span data-stu-id="2e2a6-163">In this example, hello Failures blade is filtered tooshow just information from hello front-end web service, filtering out failures from hello CRM API backend:</span></span>

![Métrico gráfico segmentado pelo nome da função de nuvem](./media/app-insights-monitor-multi-role-apps/cloud-role-name.png)

## <a name="trace-operations-between-components"></a><span data-ttu-id="2e2a6-165">Operações de rastreio entre componentes</span><span class="sxs-lookup"><span data-stu-id="2e2a6-165">Trace operations between components</span></span>

<span data-ttu-id="2e2a6-166">Pode rastrear a partir de um componente tooanother, as chamadas de Olá efetuadas ao processar uma operação individual.</span><span class="sxs-lookup"><span data-stu-id="2e2a6-166">You can trace from one component tooanother, hello calls made while processing an individual operation.</span></span>


![Mostrar a telemetria para a operação](./media/app-insights-monitor-multi-role-apps/show-telemetry-for-operation.png)

<span data-ttu-id="2e2a6-168">Clicar tooa lista correlacionado de telemetria para esta operação no servidor web front-end de Olá e Olá API de back-end:</span><span class="sxs-lookup"><span data-stu-id="2e2a6-168">Click through tooa correlated list of telemetry for this operation across hello front-end web server and hello back-end API:</span></span>

![Componentes de pesquisa](./media/app-insights-monitor-multi-role-apps/search-across-components.png)


## <a name="next-steps"></a><span data-ttu-id="2e2a6-170">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="2e2a6-170">Next steps</span></span>

* [<span data-ttu-id="2e2a6-171">Telemetria separada de desenvolvimento, teste e produção</span><span class="sxs-lookup"><span data-stu-id="2e2a6-171">Separate telemetry from Development, Test, and Production</span></span>](app-insights-separate-resources.md)
