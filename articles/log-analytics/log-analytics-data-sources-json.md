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
# <a name="collecting-custom-json-data-sources-with-hello-oms-agent-for-linux-in-log-analytics"></a>Recolha de origens de dados JSON personalizadas com Olá agente do OMS para Linux na análise de registos
Origens de dados JSON personalizadas podem ser recolhidas para análise de registos utilizando Olá agente do OMS para Linux.  Estas origens de dados personalizados podem ser scripts simples, tais como a devolver o JSON [curl](https://curl.haxx.se/) ou um dos [300 + plug-ins do FluentD](http://www.fluentd.org/plugins/all). Este artigo descreve a configuração de Olá necessária para esta recolha de dados.

> [!NOTE]
> Agente do OMS para Linux v1.1.0-217 + é necessário para dados de JSON personalizado

## <a name="configuration"></a>Configuração

### <a name="configure-input-plugin"></a>Configurar o plug-in de entrada

adicionar dados JSON toocollect na análise de registos, `oms.api.` toohello início de uma etiqueta de FluentD num plug-in de entrada.

Por exemplo, segue-se um ficheiro de configuração separadas `exec-json.conf` no `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/`.  Esta opção utiliza os plug-in do Olá FluentD `exec` toorun um comando curl cada 30 segundos.  resultado de Olá partir deste comando é recolhido pelo plug-in de saída do Olá JSON.

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
ficheiro de configuração de Olá adicionado em `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/` exigirá toohave alterar a propriedade com Olá os seguintes comandos.

`sudo chown omsagent:omiusers /etc/opt/microsoft/omsagent/conf/omsagent.d/exec-json.conf`

### <a name="configure-output-plugin"></a>Configurar o plug-in de saída 
Adicionar Olá seguir saída Plug-in configuração toohello principal configuração no `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf` ou como um ficheiro de configuração separadas colocado no`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/`

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

### <a name="restart-oms-agent-for-linux"></a>Reinicie o agente do OMS para Linux
Reinicie Olá agente do OMS para o serviço de Linux com Olá os seguintes comandos.

    sudo /opt/microsoft/omsagent/bin/service_control restart 

## <a name="output"></a>Saída
Olá serão possível recolher os dados na análise de registos com um tipo de registo de `<FLUENTD_TAG>_CL`.

Por exemplo, Olá etiqueta personalizada `tag oms.api.tomcat` na análise de registos com um tipo de registo de `tomcat_CL`.  Foi possível obter todos os registos deste tipo com Olá seguir pesquisa de registo.

    Type=tomcat_CL

Dados JSON aninhados origens são suportadas, mas são indexadas baseiam nos campo principal. Por exemplo, Olá os seguintes dados JSON é devolvido a partir de uma pesquisa de análise de registos como `tag_s : "[{ "a":"1", "b":"2" }]`.

```
{
    "tag": [{
        "a":"1",
        "b":"2"
    }]
}
```


## <a name="next-steps"></a>Passos seguintes
* Saiba mais sobre [pesquisas de registo](log-analytics-log-searches.md) dados de Olá tooanalyze recolhidos a partir de origens de dados e soluções. 
 