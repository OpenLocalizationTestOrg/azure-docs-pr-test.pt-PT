---
title: "o estado de funcionamento do aaaPredict vehicle e hábitos - Azure | Microsoft Docs"
description: "Utilizar capacidades de Olá do Cortana Intelligence toogain preditivos e em tempo real das informações no estado de funcionamento vehicle e ocasionar hábitos."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 09fad60b-2f48-488b-8a7e-47d1f969ec6f
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: 54cc890ff39493bc040bb809721388349665720f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="vehicle-telemetry-analytics-solution-playbook"></a>Playbook de solução de análise de telemetria de veículos
Isto **menu** liga toohello capítulos neste manual de comunicação social. 

[!INCLUDE [cap-vehicle-telemetry-playbook-selector](../../includes/cap-vehicle-telemetry-playbook-selector.md)]

## <a name="overview"></a>Descrição geral
Computadores superutilizadores movido fora do laboratório de Olá e agora são parqueados no nosso garage! Estes automóveis inovadores contêm um conjunto de sensores, concedendo-lhes Olá capacidade tootrack e monitorizar milhões de eventos a cada segundo. Esperamos que por 2020, a maioria destas carros irá ter sido toohello ligado à Internet. Imagine tocar para este variedade de segurança maior de tooprovide de dados, fiabilidade e uma experiência despertar melhor! Microsoft efetuou esta dream uma realidade com Cortana Intelligence.

Cortana Intelligence da Microsoft é um macrodados completamente geridos e avançadas suite de análise que permite-lhe tootransform os dados em ação inteligente. Queremos toointroduce toohello modelo de solução de análise do Cortana Intelligence Vehicle telemetria. Esta solução demonstra como dealerships carro, fabricantes automóveis e insurance empresas podem utilizar Olá das capacidades do Cortana Intelligence toogain em tempo real e conhecimentos aprofundados preditivos acerca do Estado de funcionamento vehicle e ocasionar hábitos. 

solução Olá é implementada como um [padrão de arquitetura de lambda](https://en.wikipedia.org/wiki/Lambda_architecture) Mostrar Olá potencial da plataforma do Cortana Intelligence Olá para em tempo real e processamento em lote. solução Olá: 

* Fornece um simulador Vehicle Telematics
* tira partido dos Event Hubs para ingestão de milhões de eventos de telemetria simulada vehicle relacionadas no Azure 
* utiliza as informações em tempo real do Stream Analytics toogain no estado de funcionamento vehicle
* mantém os dados de Olá para armazenamento a longo prazo para a análise de lote mais rico. 
* tira partido da Machine Learning para deteção de anomalias em tempo real e processamento toogain preditiva insights do batch.
* tira partido do HDInsight tootransform dados em escala e orquestração do Data Factory toohandle, agendamento, gestão de recursos e a monitorização do pipeline de processamento de lote Olá 
* fornece esta solução um dashboard avançado para dados em tempo real e visualizações de Análise Preditiva através do Power BI

## <a name="architecture"></a>Arquitetura
![Diagrama de arquitetura de solução](./media/cortana-analytics-playbook-vehicle-telemetry/fig1-vehicle-telemetry-annalytics-solution-architecture.png)
*figura 1 – arquitetura de solução de análise de telemetria Vehicle*

Esta solução inclui seguinte Olá **componentes do Cortana Intelligence** e showcases os respetivos integração de tooend final:

* **Os Event Hubs** para ingestão de milhões de eventos de telemetria vehicle relacionadas no Azure.
* **Stream Analytics** para obter informações em tempo real no estado de funcionamento vehicle e persistir os dados para armazenamento a longo prazo para a análise de lote mais rico.
* **Machine Learning** para deteção de anomalias em tempo real e insights preditiva toogain de processamento em lote.
* **HDInsight** aproveitadas tootransform dados à escala
* **Fábrica de dados** processa orchestration, agendamento, de gestão de recursos e monitorização do pipeline de processamento de lote Olá.
* **Power BI** fornece esta solução um dashboard avançado para dados em tempo real e visualizações de Análise Preditiva.

Acede a esta solução dois diferentes **origens de dados**: 

* **Simulated vehicle sinais e diagnóstico**: um simulador de telematics vehicle emite informações de diagnóstico e sinais que correspondem toohello Estado vehicle Olá e Olá ocasionar padrão num determinado ponto no tempo. 
* **Catálogo de vehicle**: um conjunto de dados de referência que contém um mapeamento de toomodel VIN.

