---
title: "dados aaaCollect CollectD na análise de registos do OMS | Microsoft Docs"
description: "CollectD é um daemon de Linux de código aberto periodicamente recolhe dados das aplicações e informações de nível do sistema.  Este artigo fornece informações sobre a recolha de dados de CollectD na análise de registos."
services: log-analytics
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: tysonn
ms.assetid: f1d5bde4-6b86-4b8e-b5c1-3ecbaba76198
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/02/2017
ms.author: magoedte
ms.openlocfilehash: 7ad82c9c67a664aabd44f08bef2253d84cd2dfba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="collect-data-from-collectd-on-linux-agents-in-log-analytics"></a><span data-ttu-id="4c306-104">Recolher dados de CollectD nos agentes Linux na análise de registos</span><span class="sxs-lookup"><span data-stu-id="4c306-104">Collect data from CollectD on Linux agents in Log Analytics</span></span>
<span data-ttu-id="4c306-105">[CollectD](https://collectd.org/) é um daemon de Linux de código aberto periodicamente recolhe métricas de desempenho de aplicações e informações de nível do sistema.</span><span class="sxs-lookup"><span data-stu-id="4c306-105">[CollectD](https://collectd.org/) is an open source Linux daemon that periodically collects performance metrics from applications and system level information.</span></span> <span data-ttu-id="4c306-106">Aplicações de exemplo incluem Olá Máquina Virtual de Java (JVM), o servidor de MySQL e Nginx.</span><span class="sxs-lookup"><span data-stu-id="4c306-106">Example applications include hello Java Virtual Machine (JVM), MySQL Server, and Nginx.</span></span> <span data-ttu-id="4c306-107">Este artigo fornece informações sobre a recolha de dados de desempenho de CollectD na análise de registos.</span><span class="sxs-lookup"><span data-stu-id="4c306-107">This article provides information on collecting performance data from CollectD in Log Analytics.</span></span>

<span data-ttu-id="4c306-108">Uma lista completa de plug-ins disponíveis pode ser encontrada em [tabela de plug-ins](https://collectd.org/wiki/index.php/Table_of_Plugins).</span><span class="sxs-lookup"><span data-stu-id="4c306-108">A full list of available plugins can be found at [Table of Plugins](https://collectd.org/wiki/index.php/Table_of_Plugins).</span></span>

![Descrição geral de CollectD](media/log-analytics-data-sources-collectd/overview.png)

<span data-ttu-id="4c306-110">Olá configuração CollectD seguinte está incluída no Olá agente do OMS para Linux tooroute CollectD dados toohello agente do OMS do Linux.</span><span class="sxs-lookup"><span data-stu-id="4c306-110">hello following CollectD configuration is included in hello OMS Agent for Linux tooroute  CollectD data toohello OMS Agent for Linux.</span></span>

    LoadPlugin write_http

    <Plugin write_http>
         <Node "oms">
         URL "127.0.0.1:26000/oms.collectd"
         Format "JSON"
         StoreRates true
         </Node>
    </Plugin>

<span data-ttu-id="4c306-111">Além disso, se utilizar um versões do collectD antes de utilizar o 5.5 Olá seguintes em vez disso, a configuração.</span><span class="sxs-lookup"><span data-stu-id="4c306-111">Additionally, if using an versions of collectD before 5.5 use hello following configuration instead.</span></span>

    LoadPlugin write_http

    <Plugin write_http>
       <URL "127.0.0.1:26000/oms.collectd">
        Format "JSON"
         StoreRates true
       </URL>
    </Plugin>

<span data-ttu-id="4c306-112">configuração do Hello CollectD utiliza Olá`write_http` dados métrica do desempenho de toosend de plug-in através da porta 26000 tooOMS agente para Linux.</span><span class="sxs-lookup"><span data-stu-id="4c306-112">hello CollectD configuration uses hello default`write_http` plugin toosend performance metric data over port 26000 tooOMS Agent for Linux.</span></span> 

> [!NOTE]
> <span data-ttu-id="4c306-113">Esta porta pode ser configurado tooa personalizado porta, se necessário.</span><span class="sxs-lookup"><span data-stu-id="4c306-113">This port can be configured tooa custom-defined port if needed.</span></span>

<span data-ttu-id="4c306-114">Olá agente do OMS para Linux também escuta na porta 26000 CollectD com base nas métricas e, em seguida, converte-os tooOMS métricas de esquema.</span><span class="sxs-lookup"><span data-stu-id="4c306-114">hello OMS Agent for Linux also listens on port 26000 for CollectD metrics and then converts them tooOMS schema metrics.</span></span> <span data-ttu-id="4c306-115">Olá que se segue Olá agente do OMS para a configuração do Linux `collectd.conf`.</span><span class="sxs-lookup"><span data-stu-id="4c306-115">hello following is hello OMS Agent for Linux configuration  `collectd.conf`.</span></span>

    <source>
      type http
      port 26000
      bind 127.0.0.1
    </source>

    <filter oms.collectd>
      type filter_collectd
    </filter>


## <a name="versions-supported"></a><span data-ttu-id="4c306-116">Versões suportadas</span><span class="sxs-lookup"><span data-stu-id="4c306-116">Versions supported</span></span>
- <span data-ttu-id="4c306-117">Análise de registos suporta atualmente CollectD versão 4.8 e superior.</span><span class="sxs-lookup"><span data-stu-id="4c306-117">Log Analytics currently supports CollectD version 4.8 and above.</span></span>
- <span data-ttu-id="4c306-118">Agente do OMS para Linux v1.1.0-217 ou superior é necessário para a coleção de métrica de CollectD.</span><span class="sxs-lookup"><span data-stu-id="4c306-118">OMS Agent for Linux v1.1.0-217 or above is required for CollectD metric collection.</span></span>


## <a name="configuration"></a><span data-ttu-id="4c306-119">Configuração</span><span class="sxs-lookup"><span data-stu-id="4c306-119">Configuration</span></span>
<span data-ttu-id="4c306-120">Olá seguem-se a recolha de tooconfigure de passos básicos dos dados de CollectD na análise de registos.</span><span class="sxs-lookup"><span data-stu-id="4c306-120">hello following are basic steps tooconfigure collection of CollectD data in Log Analytics.</span></span>

1. <span data-ttu-id="4c306-121">Configure CollectD toosend dados toohello agente do OMS Linux utilizando o plug-in do Olá write_http.</span><span class="sxs-lookup"><span data-stu-id="4c306-121">Configure CollectD toosend data toohello OMS Agent for Linux using hello write_http plugin.</span></span>  
2. <span data-ttu-id="4c306-122">Configure Olá agente do OMS para Linux toolisten para hello CollectD dados na porta adequada Olá.</span><span class="sxs-lookup"><span data-stu-id="4c306-122">Configure hello OMS Agent for Linux toolisten for hello CollectD data on hello appropriate port.</span></span>
3. <span data-ttu-id="4c306-123">Reinicie CollectD e o agente do OMS para Linux.</span><span class="sxs-lookup"><span data-stu-id="4c306-123">Restart CollectD and OMS Agent for Linux.</span></span>

### <a name="configure-collectd-tooforward-data"></a><span data-ttu-id="4c306-124">Configurar CollectD tooforward dados</span><span class="sxs-lookup"><span data-stu-id="4c306-124">Configure CollectD tooforward data</span></span> 

1. <span data-ttu-id="4c306-125">tooroute CollectD dados toohello agente do OMS para Linux `oms.conf` toobe tem de adicionar o diretório de configuração do tooCollectD.</span><span class="sxs-lookup"><span data-stu-id="4c306-125">tooroute CollectD data toohello OMS Agent for Linux, `oms.conf` needs toobe added tooCollectD's configuration directory.</span></span> <span data-ttu-id="4c306-126">destino de Olá deste ficheiro depende Olá Linux distro da sua máquina.</span><span class="sxs-lookup"><span data-stu-id="4c306-126">hello destination of this file depends on hello Linux  distro of your machine.</span></span>

    <span data-ttu-id="4c306-127">Se o diretório de configuração CollectD está localizado na /etc/collectd.d/:</span><span class="sxs-lookup"><span data-stu-id="4c306-127">If your CollectD config directory is located in /etc/collectd.d/:</span></span>

        sudo cp /etc/opt/microsoft/omsagent/sysconf/omsagent.d/oms.conf /etc/collectd.d/oms.conf

    <span data-ttu-id="4c306-128">Se o diretório de configuração CollectD está localizado na /etc/collectd/collectd.conf.d/:</span><span class="sxs-lookup"><span data-stu-id="4c306-128">If your CollectD config directory is located in /etc/collectd/collectd.conf.d/:</span></span>

        sudo cp /etc/opt/microsoft/omsagent/sysconf/omsagent.d/oms.conf /etc/collectd/collectd.conf.d/oms.conf

    >[!NOTE]
    ><span data-ttu-id="4c306-129">Para versões de CollectD antes 5.5 terão toomodify etiquetas de Olá no `oms.conf` conforme mostrado acima.</span><span class="sxs-lookup"><span data-stu-id="4c306-129">For CollectD versions before 5.5 you will have toomodify hello tags in `oms.conf` as shown above.</span></span>
    >

2. <span data-ttu-id="4c306-130">Cópia collectd.conf toohello pretendido diretório de configuração de omsagent da área de trabalho.</span><span class="sxs-lookup"><span data-stu-id="4c306-130">Copy collectd.conf toohello desired workspace's omsagent configuration directory.</span></span>

        sudo cp /etc/opt/microsoft/omsagent/sysconf/omsagent.d/collectd.conf /etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/
        sudo chown omsagent:omiusers /etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/collectd.conf

3. <span data-ttu-id="4c306-131">Reinicie CollectD e o agente do OMS para Linux com Olá os seguintes comandos.</span><span class="sxs-lookup"><span data-stu-id="4c306-131">Restart CollectD and OMS Agent for Linux with hello following commands.</span></span>

    <span data-ttu-id="4c306-132">sudo collectd reinício sudo /opt/microsoft/omsagent/bin/service_control reiniciar o serviço do</span><span class="sxs-lookup"><span data-stu-id="4c306-132">sudo service collectd restart  sudo /opt/microsoft/omsagent/bin/service_control restart</span></span>

## <a name="collectd-metrics-toolog-analytics-schema-conversion"></a><span data-ttu-id="4c306-133">CollectD métricas tooLog conversão de esquema de análise</span><span class="sxs-lookup"><span data-stu-id="4c306-133">CollectD metrics tooLog Analytics schema conversion</span></span>
<span data-ttu-id="4c306-134">toomaintain um modelo familiar entre as métricas de infraestrutura recolhidos pelo agente do OMS, Linux e Olá nova com base nas métricas recolhidas pelo CollectD Olá seguir o mapeamento de esquema é utilizado:</span><span class="sxs-lookup"><span data-stu-id="4c306-134">toomaintain a familiar model between infrastructure metrics already collected by OMS Agent for Linux and hello new metrics collected by CollectD hello following schema mapping is used:</span></span>

| <span data-ttu-id="4c306-135">Campo de métrica de CollectD</span><span class="sxs-lookup"><span data-stu-id="4c306-135">CollectD Metric field</span></span> | <span data-ttu-id="4c306-136">Campo de análise do registo</span><span class="sxs-lookup"><span data-stu-id="4c306-136">Log Analytics field</span></span> |
|:--|:--|
| <span data-ttu-id="4c306-137">anfitrião</span><span class="sxs-lookup"><span data-stu-id="4c306-137">host</span></span> | <span data-ttu-id="4c306-138">Computador</span><span class="sxs-lookup"><span data-stu-id="4c306-138">Computer</span></span> |
| <span data-ttu-id="4c306-139">Plug-in</span><span class="sxs-lookup"><span data-stu-id="4c306-139">plugin</span></span> | <span data-ttu-id="4c306-140">Nenhuma</span><span class="sxs-lookup"><span data-stu-id="4c306-140">None</span></span> |
| <span data-ttu-id="4c306-141">plugin_instance</span><span class="sxs-lookup"><span data-stu-id="4c306-141">plugin_instance</span></span> | <span data-ttu-id="4c306-142">Nome da instância</span><span class="sxs-lookup"><span data-stu-id="4c306-142">Instance Name</span></span><br><span data-ttu-id="4c306-143">Se **plugin_instance** é *nulo* , em seguida, InstanceName = "*total*"</span><span class="sxs-lookup"><span data-stu-id="4c306-143">If **plugin_instance** is *null* then InstanceName="*_Total*"</span></span> |
| <span data-ttu-id="4c306-144">tipo</span><span class="sxs-lookup"><span data-stu-id="4c306-144">type</span></span> | <span data-ttu-id="4c306-145">ObjectName</span><span class="sxs-lookup"><span data-stu-id="4c306-145">ObjectName</span></span> |
| <span data-ttu-id="4c306-146">type_instance</span><span class="sxs-lookup"><span data-stu-id="4c306-146">type_instance</span></span> | <span data-ttu-id="4c306-147">CounterName</span><span class="sxs-lookup"><span data-stu-id="4c306-147">CounterName</span></span><br><span data-ttu-id="4c306-148">Se **type_instance** é *nulo* , em seguida, CounterName =**em branco**</span><span class="sxs-lookup"><span data-stu-id="4c306-148">If **type_instance** is *null* then CounterName=**blank**</span></span> |
| <span data-ttu-id="4c306-149">dsnames []</span><span class="sxs-lookup"><span data-stu-id="4c306-149">dsnames[]</span></span> | <span data-ttu-id="4c306-150">CounterName</span><span class="sxs-lookup"><span data-stu-id="4c306-150">CounterName</span></span> |
| <span data-ttu-id="4c306-151">dstypes</span><span class="sxs-lookup"><span data-stu-id="4c306-151">dstypes</span></span> | <span data-ttu-id="4c306-152">Nenhuma</span><span class="sxs-lookup"><span data-stu-id="4c306-152">None</span></span> |
| <span data-ttu-id="4c306-153">os valores]</span><span class="sxs-lookup"><span data-stu-id="4c306-153">values[]</span></span> | <span data-ttu-id="4c306-154">CounterValue</span><span class="sxs-lookup"><span data-stu-id="4c306-154">CounterValue</span></span> |

## <a name="next-steps"></a><span data-ttu-id="4c306-155">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="4c306-155">Next steps</span></span>
* <span data-ttu-id="4c306-156">Saiba mais sobre [pesquisas de registo](log-analytics-log-searches.md) dados de Olá tooanalyze recolhidos a partir de origens de dados e soluções.</span><span class="sxs-lookup"><span data-stu-id="4c306-156">Learn about [log searches](log-analytics-log-searches.md) tooanalyze hello data collected from data sources and solutions.</span></span> 
* <span data-ttu-id="4c306-157">Utilize [campos personalizados](log-analytics-custom-fields.md) tooparse dados de registos de syslog em campos individuais.</span><span class="sxs-lookup"><span data-stu-id="4c306-157">Use [Custom Fields](log-analytics-custom-fields.md) tooparse data from syslog records into individual fields.</span></span>

