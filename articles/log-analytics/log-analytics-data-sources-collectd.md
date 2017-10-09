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
# <a name="collect-data-from-collectd-on-linux-agents-in-log-analytics"></a>Recolher dados de CollectD nos agentes Linux na análise de registos
[CollectD](https://collectd.org/) é um daemon de Linux de código aberto periodicamente recolhe métricas de desempenho de aplicações e informações de nível do sistema. Aplicações de exemplo incluem Olá Máquina Virtual de Java (JVM), o servidor de MySQL e Nginx. Este artigo fornece informações sobre a recolha de dados de desempenho de CollectD na análise de registos.

Uma lista completa de plug-ins disponíveis pode ser encontrada em [tabela de plug-ins](https://collectd.org/wiki/index.php/Table_of_Plugins).

![Descrição geral de CollectD](media/log-analytics-data-sources-collectd/overview.png)

Olá configuração CollectD seguinte está incluída no Olá agente do OMS para Linux tooroute CollectD dados toohello agente do OMS do Linux.

    LoadPlugin write_http

    <Plugin write_http>
         <Node "oms">
         URL "127.0.0.1:26000/oms.collectd"
         Format "JSON"
         StoreRates true
         </Node>
    </Plugin>

Além disso, se utilizar um versões do collectD antes de utilizar o 5.5 Olá seguintes em vez disso, a configuração.

    LoadPlugin write_http

    <Plugin write_http>
       <URL "127.0.0.1:26000/oms.collectd">
        Format "JSON"
         StoreRates true
       </URL>
    </Plugin>

configuração do Hello CollectD utiliza Olá`write_http` dados métrica do desempenho de toosend de plug-in através da porta 26000 tooOMS agente para Linux. 

> [!NOTE]
> Esta porta pode ser configurado tooa personalizado porta, se necessário.

Olá agente do OMS para Linux também escuta na porta 26000 CollectD com base nas métricas e, em seguida, converte-os tooOMS métricas de esquema. Olá que se segue Olá agente do OMS para a configuração do Linux `collectd.conf`.

    <source>
      type http
      port 26000
      bind 127.0.0.1
    </source>

    <filter oms.collectd>
      type filter_collectd
    </filter>


## <a name="versions-supported"></a>Versões suportadas
- Análise de registos suporta atualmente CollectD versão 4.8 e superior.
- Agente do OMS para Linux v1.1.0-217 ou superior é necessário para a coleção de métrica de CollectD.


## <a name="configuration"></a>Configuração
Olá seguem-se a recolha de tooconfigure de passos básicos dos dados de CollectD na análise de registos.

1. Configure CollectD toosend dados toohello agente do OMS Linux utilizando o plug-in do Olá write_http.  
2. Configure Olá agente do OMS para Linux toolisten para hello CollectD dados na porta adequada Olá.
3. Reinicie CollectD e o agente do OMS para Linux.

### <a name="configure-collectd-tooforward-data"></a>Configurar CollectD tooforward dados 

1. tooroute CollectD dados toohello agente do OMS para Linux `oms.conf` toobe tem de adicionar o diretório de configuração do tooCollectD. destino de Olá deste ficheiro depende Olá Linux distro da sua máquina.

    Se o diretório de configuração CollectD está localizado na /etc/collectd.d/:

        sudo cp /etc/opt/microsoft/omsagent/sysconf/omsagent.d/oms.conf /etc/collectd.d/oms.conf

    Se o diretório de configuração CollectD está localizado na /etc/collectd/collectd.conf.d/:

        sudo cp /etc/opt/microsoft/omsagent/sysconf/omsagent.d/oms.conf /etc/collectd/collectd.conf.d/oms.conf

    >[!NOTE]
    >Para versões de CollectD antes 5.5 terão toomodify etiquetas de Olá no `oms.conf` conforme mostrado acima.
    >

2. Cópia collectd.conf toohello pretendido diretório de configuração de omsagent da área de trabalho.

        sudo cp /etc/opt/microsoft/omsagent/sysconf/omsagent.d/collectd.conf /etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/
        sudo chown omsagent:omiusers /etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/collectd.conf

3. Reinicie CollectD e o agente do OMS para Linux com Olá os seguintes comandos.

    sudo collectd reinício sudo /opt/microsoft/omsagent/bin/service_control reiniciar o serviço do

## <a name="collectd-metrics-toolog-analytics-schema-conversion"></a>CollectD métricas tooLog conversão de esquema de análise
toomaintain um modelo familiar entre as métricas de infraestrutura recolhidos pelo agente do OMS, Linux e Olá nova com base nas métricas recolhidas pelo CollectD Olá seguir o mapeamento de esquema é utilizado:

| Campo de métrica de CollectD | Campo de análise do registo |
|:--|:--|
| anfitrião | Computador |
| Plug-in | Nenhuma |
| plugin_instance | Nome da instância<br>Se **plugin_instance** é *nulo* , em seguida, InstanceName = "*total*" |
| tipo | ObjectName |
| type_instance | CounterName<br>Se **type_instance** é *nulo* , em seguida, CounterName =**em branco** |
| dsnames [] | CounterName |
| dstypes | Nenhuma |
| os valores] | CounterValue |

## <a name="next-steps"></a>Passos seguintes
* Saiba mais sobre [pesquisas de registo](log-analytics-log-searches.md) dados de Olá tooanalyze recolhidos a partir de origens de dados e soluções. 
* Utilize [campos personalizados](log-analytics-custom-fields.md) tooparse dados de registos de syslog em campos individuais.

