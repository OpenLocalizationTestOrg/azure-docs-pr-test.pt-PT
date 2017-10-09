---
title: "aaaOverview das informações de séries de tempo do Azure | Microsoft Docs"
description: "Introdução tooAzure Insight de série de tempo, um novo serviço de análise de dados de séries de tempo e soluções de IoT"
keywords: 
services: tsi
documentationcenter: 
author: op-ravi
manager: jhubbard
editor: 
ms.assetid: 
ms.service: time-series-insights
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/20/2017
ms.author: omravi
ms.openlocfilehash: 8c022bf1fae88eddab3dbebc7bb36cc15a785172
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-time-series-insights"></a>O que é o Azure Time Series Insights

As informações de séries de tempo do Azure é um serviço em nuvem gerido com o armazenamento, a análise e os componentes de visualização que tornam mais fácil tooingest, armazenarem, explorar e analisam billions de eventos em simultâneo. O Time Series Insights dá-lhe uma vista global dos seus dados, o que lhe permite validar rapidamente as suas soluções de IoT e evitar um período de indisponibilidade dispendioso para os dispositivos ao ajudá-lo a descobrir tendências e anomalias ocultas e a realizar análises da origem dos problemas praticamente em tempo real. Informações de séries de tempo ingere dados de séries de tempo do evento-os corretores (por exemplo, os Hubs IoT ou Event Hubs), indexa dados Olá e ter extinguido dados com base numa política de retenção configurável. Os utilizadores consumam dados Olá através de um intuitiva UX ou APIs de consulta de REST.

![Descrição Geral do Time Series Insight](media/overview/time-series-insights-overview-flow.png)

## <a name="primary-scenarios"></a>Cenários principais

* Monitorizar e validar as soluções IoT em minutos.
* Visualizar e analisar dados de IoT em escala.
* Acelerar a análise de origens de problemas e a deteção de anomalias.
* Criar uma vista global de vários dispositivos, instalações e dados.

## <a name="capabilities-and-benefits"></a>Capacidades e vantagens

* **Fácil tooget iniciado**: informações de séries de tempo do Azure necessita de preparação não existem dados prévio e é incredibly rápida. Ligar toobillions de eventos no seu IoT Hub do Azure ou o Hub de eventos em minutos. Assim que estiver ligado, visualizar e interagir com dados de sensores em segundos tooquickly validar as suas soluções de IoT. Informações de séries de tempo é fácil toouse; pode interagir com os seus dados sem ter de escrever uma única linha de código.  Não há nenhum toolearn idioma nova; Informações de séries de tempo fornece uma superfície de consulta granular e texto livre para utilizadores avançados e ponto e clique em exploração para todos os.

* **Quase em tempo real insights**: Insights de séries de tempo pode ingerir centenas de milhões de eventos de sensor por dia, com uma latência de um minuto, para que possam reagir toochanges rapidamente. Proporciona-lhe informações mais detalhadas sobre os dados de sensores, ao ajudá-lo a detetar tendências e anomalias depressa, a realizar facilmente análises de origens de problemas complexas e a evitar tempos de indisponibilidade dispendiosos. Ao ativar cross-correlação entre os dados históricos e em tempo real, das informações de séries de tempo ajuda-o a desbloquear ocultas tendências em dados de Olá.

* **Criar soluções personalizadas**: incorpore dados do Azure Time Series Insights nas suas aplicações existentes ou crie soluções personalizadas novas com as APIs REST do Time Series Insights. Criar e partilhar personalizar vistas, pode partilhar para outros tooexplore as deteções.

* **Escalabilidade**: Insights de séries de tempo é concebida toosupport IoT à escala. Pré-visualização, pode entrada de too100 milhões de 1 milhões de eventos por dia, com uma retenção predefinido span de 31 dias. Pode ver e analisar fluxos de dados em direto em tempo quase real, juntamente com grandes quantidades de dados históricos. Daqui para a frente, taxas de entrada e de retenção irão aumentar tooaccommodate uma escala empresarial que alguma vez evolução.

## <a name="time-series-insights-glossary"></a>Glossário do Time Series Insights

* **Ambiente**: um ambiente é um recurso do Azure com capacidade de receção e armazenamento.  Os clientes aprovisionar ambientes através de Olá portal do Azure com as respetivas capacidades máximas necessária.
* **Origem de Eventos**: as Origens de Eventos do Time Series Insights derivam de um mediador de eventos, como os Hubs de Eventos do Azure.  Informações de séries de tempo liga-se diretamente tooEvent origens, ingestão de fluxo de dados de Olá relacionadas sem escrever qualquer código. Atualmente, o Time Series Insights suporta Hubs de Eventos do Azure e Hubs IoT do Azure.
* **Referência a dados**: Insights de séries de tempo fornece aos utilizadores de dados de série do tempo do Olá capacidade toojoin com dados de referência.  Os dados de referência podem incluir metadados sobre dispositivos ou outros dados estáticos que são alterados de forma relativamente pouco frequente. Informações de séries de tempo é associado a dados de referência de Olá com fluxos de dados, permitindo que os utilizadores toovisualize e analisar estes dados praticamente em tempo real.
