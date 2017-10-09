---
title: "dados JSON personalizado aaaCollecting na análise de registos do OMS | Microsoft Docs"
description: "Origens de dados JSON personalizadas podem ser recolhidas para análise de registos utilizando Olá agente do OMS para Linux.  Estas origens de dados personalizados podem ser scripts simples devolver JSON como curl ou um dos 300 + plug-ins do FluentD. Este artigo descreve a configuração de Olá necessária para esta recolha de dados."
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
ms.date: 05/04/2017
ms.author: magoedte
ms.openlocfilehash: 97d401408a8c206d4a9ef2ec9b13ba1ca6b5e92b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="collecting-custom-json-data-sources-with-hello-oms-agent-for-linux-in-log-analytics"></a><span data-ttu-id="9a4d7-105">Recolha de origens de dados JSON personalizadas com Olá agente do OMS para Linux na análise de registos</span><span class="sxs-lookup"><span data-stu-id="9a4d7-105">Collecting custom JSON data sources with hello OMS Agent for Linux in Log Analytics</span></span>
<span data-ttu-id="9a4d7-106">Origens de dados JSON personalizadas podem ser recolhidas para análise de registos utilizando Olá agente do OMS para Linux.</span><span class="sxs-lookup"><span data-stu-id="9a4d7-106">Custom JSON data sources can be collected into Log Analytics using hello OMS Agent for Linux.</span></span>  <span data-ttu-id="9a4d7-107">Estas origens de dados personalizados podem ser scripts simples, tais como a devolver o JSON [curl](https://curl.haxx.se/) ou um dos [300 + plug-ins do FluentD](http://www.fluentd.org/plugins/all).</span><span class="sxs-lookup"><span data-stu-id="9a4d7-107">These custom data sources can be simple scripts returning JSON such as [curl](https://curl.haxx.se/) or one of [FluentD's 300+ plugins](http://www.fluentd.org/plugins/all).</span></span> <span data-ttu-id="9a4d7-108">Este artigo descreve a configuração de Olá necessária para esta recolha de dados.</span><span class="sxs-lookup"><span data-stu-id="9a4d7-108">This article describes hello configuration required for this data collection.</span></span>

> [!NOTE]
> <span data-ttu-id="9a4d7-109">Agente do OMS para Linux v1.1.0-217 + é necessário para dados de JSON personalizado</span><span class="sxs-lookup"><span data-stu-id="9a4d7-109">OMS Agent for Linux v1.1.0-217+ is required for Custom JSON Data</span></span>

## <a name="configuration"></a><span data-ttu-id="9a4d7-110">Configuração</span><span class="sxs-lookup"><span data-stu-id="9a4d7-110">Configuration</span></span>

### <a name="configure-input-plugin"></a><span data-ttu-id="9a4d7-111">Configurar o plug-in de entrada</span><span class="sxs-lookup"><span data-stu-id="9a4d7-111">Configure input plugin</span></span>

<span data-ttu-id="9a4d7-112">adicionar dados JSON toocollect na análise de registos, `oms.api.` toohello início de uma etiqueta de FluentD num plug-in de entrada.</span><span class="sxs-lookup"><span data-stu-id="9a4d7-112">toocollect JSON data in Log Analytics, add `oms.api.` toohello start of a FluentD tag in an input plugin.</span></span>

<span data-ttu-id="9a4d7-113">Por exemplo, segue-se um ficheiro de configuração separadas `exec-json.conf` no `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/`.</span><span class="sxs-lookup"><span data-stu-id="9a4d7-113">For example, following is a separate configuration file `exec-json.conf` in `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/`.</span></span>  <span data-ttu-id="9a4d7-114">Esta opção utiliza os plug-in do Olá FluentD `exec` toorun um comando curl cada 30 segundos.</span><span class="sxs-lookup"><span data-stu-id="9a4d7-114">This uses hello FluentD plugin `exec` toorun a curl command every 30 seconds.</span></span>  <span data-ttu-id="9a4d7-115">resultado de Olá partir deste comando é recolhido pelo plug-in de saída do Olá JSON.</span><span class="sxs-lookup"><span data-stu-id="9a4d7-115">hello output from this command is collected by hello JSON output plugin.</span></span>

```
<source>
  type exec
  command 'curl localhost/json.output'
  format json
  tag oms.api.httpresponse
  run_interval 30s
</source>

<match oms.api.httpresponse>
  type out_oms_api
  log_level info

  buffer_chunk_limit 5m
  buffer_type file
  buffer_path /var/opt/microsoft/omsagent/<workspace id>/state/out_oms_api_httpresponse*.buffer
  buffer_queue_limit 10
  flush_interval 20s
  retry_limit 10
  retry_wait 30s
</match>
```
<span data-ttu-id="9a4d7-116">ficheiro de configuração de Olá adicionado em `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/` exigirá toohave alterar a propriedade com Olá os seguintes comandos.</span><span class="sxs-lookup"><span data-stu-id="9a4d7-116">hello configuration file added under `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/` will require toohave its ownership changed with hello following command.</span></span>

`sudo chown omsagent:omiusers /etc/opt/microsoft/omsagent/conf/omsagent.d/exec-json.conf`

### <a name="configure-output-plugin"></a><span data-ttu-id="9a4d7-117">Configurar o plug-in de saída</span><span class="sxs-lookup"><span data-stu-id="9a4d7-117">Configure output plugin</span></span> 
<span data-ttu-id="9a4d7-118">Adicionar Olá seguir saída Plug-in configuração toohello principal configuração no `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf` ou como um ficheiro de configuração separadas colocado no`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/`</span><span class="sxs-lookup"><span data-stu-id="9a4d7-118">Add hello following output plugin configuration toohello main configuration in `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf` or as a separate configuration file placed in `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/`</span></span>

```
<match oms.api.**>
  type out_oms_api
  log_level info

  buffer_chunk_limit 5m
  buffer_type file
  buffer_path /var/opt/microsoft/omsagent/<workspace id>/state/out_oms_api*.buffer
  buffer_queue_limit 10
  flush_interval 20s
  retry_limit 10
  retry_wait 30s
</match>
```

### <a name="restart-oms-agent-for-linux"></a><span data-ttu-id="9a4d7-119">Reinicie o agente do OMS para Linux</span><span class="sxs-lookup"><span data-stu-id="9a4d7-119">Restart OMS Agent for Linux</span></span>
<span data-ttu-id="9a4d7-120">Reinicie Olá agente do OMS para o serviço de Linux com Olá os seguintes comandos.</span><span class="sxs-lookup"><span data-stu-id="9a4d7-120">Restart hello OMS Agent for Linux service with hello following command.</span></span>

    sudo /opt/microsoft/omsagent/bin/service_control restart 

## <a name="output"></a><span data-ttu-id="9a4d7-121">Saída</span><span class="sxs-lookup"><span data-stu-id="9a4d7-121">Output</span></span>
<span data-ttu-id="9a4d7-122">Olá serão possível recolher os dados na análise de registos com um tipo de registo de `<FLUENTD_TAG>_CL`.</span><span class="sxs-lookup"><span data-stu-id="9a4d7-122">hello data will be collected in Log Analytics with a record type of `<FLUENTD_TAG>_CL`.</span></span>

<span data-ttu-id="9a4d7-123">Por exemplo, Olá etiqueta personalizada `tag oms.api.tomcat` na análise de registos com um tipo de registo de `tomcat_CL`.</span><span class="sxs-lookup"><span data-stu-id="9a4d7-123">For example, hello custom tag `tag oms.api.tomcat` in Log Analytics with a record type of `tomcat_CL`.</span></span>  <span data-ttu-id="9a4d7-124">Foi possível obter todos os registos deste tipo com Olá seguir pesquisa de registo.</span><span class="sxs-lookup"><span data-stu-id="9a4d7-124">You could retrieve all records of this type with hello following log search.</span></span>

    Type=tomcat_CL

<span data-ttu-id="9a4d7-125">Dados JSON aninhados origens são suportadas, mas são indexadas baseiam nos campo principal.</span><span class="sxs-lookup"><span data-stu-id="9a4d7-125">Nested JSON data sources are supported, but are indexed based off of parent field.</span></span> <span data-ttu-id="9a4d7-126">Por exemplo, Olá os seguintes dados JSON é devolvido a partir de uma pesquisa de análise de registos como `tag_s : "[{ "a":"1", "b":"2" }]`.</span><span class="sxs-lookup"><span data-stu-id="9a4d7-126">For example, hello following JSON data is returned from a Log Analytics search as `tag_s : "[{ "a":"1", "b":"2" }]`.</span></span>

```
{
    "tag": [{
        "a":"1",
        "b":"2"
    }]
}
```


## <a name="next-steps"></a><span data-ttu-id="9a4d7-127">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="9a4d7-127">Next steps</span></span>
* <span data-ttu-id="9a4d7-128">Saiba mais sobre [pesquisas de registo](log-analytics-log-searches.md) dados de Olá tooanalyze recolhidos a partir de origens de dados e soluções.</span><span class="sxs-lookup"><span data-stu-id="9a4d7-128">Learn about [log searches](log-analytics-log-searches.md) tooanalyze hello data collected from data sources and solutions.</span></span> 
 