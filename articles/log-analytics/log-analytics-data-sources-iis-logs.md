---
title: "os registos de aaaIIS na análise de registos | Microsoft Docs"
description: "Serviços de informação Internet (IIS) armazena atividade do utilizador nos ficheiros de registo que podem ser recolhidos através da análise de registos.  Este artigo descreve como tooconfigure coleção de registos IIS e os detalhes de registos de Olá criarem no repositório do Olá OMS."
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: cec5ff0a-01f5-4262-b2e8-e3db7b7467d2
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/12/2017
ms.author: bwren
ms.openlocfilehash: c5575351090cdabaf651bcb49867794ee3a4b6e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="iis-logs-in-log-analytics"></a>Registo do IIS na análise de registos
Serviços de informação Internet (IIS) armazena atividade do utilizador nos ficheiros de registo que podem ser recolhidos através da análise de registos.  

![Registos do IIS](media/log-analytics-data-sources-iis-logs/overview.png)

## <a name="configuring-iis-logs"></a>Configurar o IIS regista
Análise de registos recolhe as entradas de ficheiros de registo criados pelo IIS, por isso, tem de [configurar o IIS para o registo](https://technet.microsoft.com/library/hh831775.aspx).

Análise de registos só suporta ficheiros de registo do IIS armazenados num formato de W3C e não suporta campos personalizados ou avançados registo do IIS.  
Análise de registos não recolhe registos no formato nativo NCSA nem o IIS.

Configurar os registos do IIS na análise de registos de Olá [menu dados nas definições de análise do registo](log-analytics-data-sources.md#configuring-data-sources).  Não há nenhuma configuração necessária à seleção **ficheiros de registo de W3C recolher formato IIS**.

Recomendamos que quando ativar a recolha de registos do IIS, deve configurar definição de rollover de registo IIS Olá em cada servidor.

## <a name="data-collection"></a>Recolha de dados
Análise de registos recolhe entradas de registo do IIS de cada origem ligada aproximadamente a cada 15 minutos.  agente de Olá regista seu lugar em cada registo de eventos que recolhe a partir de.  Se o agente de Olá ficar offline, em seguida, análise de registos recolhe os eventos de onde pela última vez foi deixada, mesmo que esses eventos foram criados ao agente Olá foi offline.

## <a name="iis-log-record-properties"></a>Propriedades de registo de registo do IIS
Registos do IIS tem um tipo de **W3CIISLog** e ter propriedades de Olá Olá a tabela seguinte:

| Propriedade | Descrição |
|:--- |:--- |
| Computador |Nome do computador de Olá que Olá evento foi recolhido a partir de. |
| cIP |Endereço IP do cliente de Olá. |
| csMethod |Método de pedido de Olá, tal como GET ou POST. |
| csReferer |Site que Olá utilizador abriu uma hiperligação toohello site atual. |
| csUserAgent |Tipo de browser do cliente de Olá. |
| csUserName |Nome do Olá autenticar o utilizador aceder ao servidor de Olá. Utilizadores anónimos são indicados por um hífen. |
| csUriStem |Destino do pedido de Olá, tal como uma página web. |
| csUriQuery |Consulta, se existirem, esse cliente Olá foi tentar tooperform. |
| ManagementGroupName |Nome do grupo de gestão de Olá para agentes do Operations Manager.  Para outros agentes, o que é AOI -\<ID da área de trabalho\> |
| RemoteIPCountry |País do endereço IP de hello do cliente de Olá. |
| RemoteIPLatitude |Latitude do endereço IP do cliente Olá. |
| RemoteIPLongitude |Longitude do endereço IP do cliente Olá. |
| scStatus |Código de estado HTTP. |
| scSubStatus |Código de erro de subestado. |
| scWin32Status |Código de estado do Windows. |
| sIP |Endereço IP do servidor de web de Olá. |
| SourceSystem |OpsMgr |
| Porta |Porta do cliente de hello do servidor de Olá ligada a. |
| sSiteName |Nome do site do IIS Olá. |
| TimeGenerated |Data e hora de entrada de Olá foi registada. |
| timeTaken |Solicitar comprimento de Olá tooprocess de tempo em milissegundos. |

## <a name="log-searches-with-iis-logs"></a>Registo de pesquisas com registos IIS
Olá tabela seguinte fornece exemplos diferentes de consultas de registo que obter registos IIS.

| Consulta | Descrição |
|:--- |:--- |
| Tipo = W3CIISLog |Todos os registos de registo do IIS. |
| Tipo = W3CIISLog scStatus = 500 |Todos os registos de registo IIS com o estado devolvido 500. |
| Tipo = W3CIISLog &#124; Medida existente pelo cIP |Contagem dos IIS entradas de registo por endereço IP do cliente. |
| Tipo = W3CIISLog csHost = "www.contoso.com" &#124; Medida existente pelo csUriStem |Entradas pelo URL para Olá anfitrião www.contoso.com de registo de contagem de IIS. |
| Tipo = W3CIISLog &#124; Medidas Sum(csBytes) pelo computador &#124; parte superior 500000 |Total de bytes recebidos por cada computador do IIS. |

>[!NOTE]
> Se a sua área de trabalho tiver sido atualizado toohello [idioma de consulta de análise de registos nova](log-analytics-log-search-upgrade.md), em seguida, Olá acima consultas alteraria toohello seguinte.

> | Consulta | Descrição |
|:--- |:--- |
| W3CIISLog |Todos os registos de registo do IIS. |
| W3CIISLog &#124; onde scStatus = = 500 |Todos os registos de registo IIS com o estado devolvido 500. |
| W3CIISLog &#124; resumir existente pelo cIP |Contagem dos IIS entradas de registo por endereço IP do cliente. |
| W3CIISLog &#124; onde csHost = = "www.contoso.com" &#124; resumir existente pelo csUriStem |Entradas pelo URL para Olá anfitrião www.contoso.com de registo de contagem de IIS. |
| W3CIISLog &#124; resumir sum(csBytes) pelo computador &#124; tirar 500000 |Total de bytes recebidos por cada computador do IIS. |

## <a name="next-steps"></a>Passos seguintes
* Configurar a análise de registos toocollect outros [origens de dados](log-analytics-data-sources.md) para análise.
* Saiba mais sobre [pesquisas de registo](log-analytics-log-searches.md) dados de Olá tooanalyze recolhidos a partir de origens de dados e soluções.
* Configure alertas no Log Analytics tooproactively notificá-lo de condições importantes encontradas nos registos IIS.
