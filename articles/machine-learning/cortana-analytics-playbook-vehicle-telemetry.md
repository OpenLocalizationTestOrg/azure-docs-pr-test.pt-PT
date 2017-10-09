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
# <a name="vehicle-telemetry-analytics-solution-playbook"></a><span data-ttu-id="dd15e-103">Playbook de solução de análise de telemetria de veículos</span><span class="sxs-lookup"><span data-stu-id="dd15e-103">Vehicle telemetry analytics solution playbook</span></span>
<span data-ttu-id="dd15e-104">Isto **menu** liga toohello capítulos neste manual de comunicação social.</span><span class="sxs-lookup"><span data-stu-id="dd15e-104">This **menu** links toohello chapters in this playbook.</span></span> 

[!INCLUDE [cap-vehicle-telemetry-playbook-selector](../../includes/cap-vehicle-telemetry-playbook-selector.md)]

## <a name="overview"></a><span data-ttu-id="dd15e-105">Descrição geral</span><span class="sxs-lookup"><span data-stu-id="dd15e-105">Overview</span></span>
<span data-ttu-id="dd15e-106">Computadores superutilizadores movido fora do laboratório de Olá e agora são parqueados no nosso garage!</span><span class="sxs-lookup"><span data-stu-id="dd15e-106">Super computers have moved out of hello lab and are now parked in our garage!</span></span> <span data-ttu-id="dd15e-107">Estes automóveis inovadores contêm um conjunto de sensores, concedendo-lhes Olá capacidade tootrack e monitorizar milhões de eventos a cada segundo.</span><span class="sxs-lookup"><span data-stu-id="dd15e-107">These cutting-edge automobiles contain a myriad of sensors, giving them hello ability tootrack and monitor millions of events every second.</span></span> <span data-ttu-id="dd15e-108">Esperamos que por 2020, a maioria destas carros irá ter sido toohello ligado à Internet.</span><span class="sxs-lookup"><span data-stu-id="dd15e-108">We expect that by 2020, most of these cars will have been connected toohello Internet.</span></span> <span data-ttu-id="dd15e-109">Imagine tocar para este variedade de segurança maior de tooprovide de dados, fiabilidade e uma experiência despertar melhor!</span><span class="sxs-lookup"><span data-stu-id="dd15e-109">Imagine tapping into this wealth of data tooprovide greater safety, reliability and a better driving experience!</span></span> <span data-ttu-id="dd15e-110">Microsoft efetuou esta dream uma realidade com Cortana Intelligence.</span><span class="sxs-lookup"><span data-stu-id="dd15e-110">Microsoft has made this dream a reality with Cortana Intelligence.</span></span>

<span data-ttu-id="dd15e-111">Cortana Intelligence da Microsoft é um macrodados completamente geridos e avançadas suite de análise que permite-lhe tootransform os dados em ação inteligente.</span><span class="sxs-lookup"><span data-stu-id="dd15e-111">Microsoft’s Cortana Intelligence is a fully managed big data and advanced analytics suite that enables you tootransform your data into intelligent action.</span></span> <span data-ttu-id="dd15e-112">Queremos toointroduce toohello modelo de solução de análise do Cortana Intelligence Vehicle telemetria.</span><span class="sxs-lookup"><span data-stu-id="dd15e-112">We want toointroduce you toohello Cortana Intelligence Vehicle Telemetry Analytics Solution Template.</span></span> <span data-ttu-id="dd15e-113">Esta solução demonstra como dealerships carro, fabricantes automóveis e insurance empresas podem utilizar Olá das capacidades do Cortana Intelligence toogain em tempo real e conhecimentos aprofundados preditivos acerca do Estado de funcionamento vehicle e ocasionar hábitos.</span><span class="sxs-lookup"><span data-stu-id="dd15e-113">This solution demonstrates how car dealerships, automobile manufacturers, and insurance companies can use hello capabilities of Cortana Intelligence toogain real-time and predictive insights on vehicle health and driving habits.</span></span> 

<span data-ttu-id="dd15e-114">solução Olá é implementada como um [padrão de arquitetura de lambda](https://en.wikipedia.org/wiki/Lambda_architecture) Mostrar Olá potencial da plataforma do Cortana Intelligence Olá para em tempo real e processamento em lote.</span><span class="sxs-lookup"><span data-stu-id="dd15e-114">hello solution is implemented as a [lambda architecture pattern](https://en.wikipedia.org/wiki/Lambda_architecture) showing hello full potential of hello Cortana Intelligence platform for real-time and batch processing.</span></span> <span data-ttu-id="dd15e-115">solução Olá:</span><span class="sxs-lookup"><span data-stu-id="dd15e-115">hello solution:</span></span> 

* <span data-ttu-id="dd15e-116">Fornece um simulador Vehicle Telematics</span><span class="sxs-lookup"><span data-stu-id="dd15e-116">provides a Vehicle Telematics simulator</span></span>
* <span data-ttu-id="dd15e-117">tira partido dos Event Hubs para ingestão de milhões de eventos de telemetria simulada vehicle relacionadas no Azure</span><span class="sxs-lookup"><span data-stu-id="dd15e-117">leverages Event Hubs for ingesting millions of simulated vehicle telemetry events into Azure</span></span> 
* <span data-ttu-id="dd15e-118">utiliza as informações em tempo real do Stream Analytics toogain no estado de funcionamento vehicle</span><span class="sxs-lookup"><span data-stu-id="dd15e-118">uses Stream Analytics toogain real-time insights on vehicle health</span></span>
* <span data-ttu-id="dd15e-119">mantém os dados de Olá para armazenamento a longo prazo para a análise de lote mais rico.</span><span class="sxs-lookup"><span data-stu-id="dd15e-119">persists hello data into long-term storage for richer batch analytics.</span></span> 
* <span data-ttu-id="dd15e-120">tira partido da Machine Learning para deteção de anomalias em tempo real e processamento toogain preditiva insights do batch.</span><span class="sxs-lookup"><span data-stu-id="dd15e-120">takes advantage of Machine Learning for anomaly detection in real-time and batch processing toogain predictive insights.</span></span>
* <span data-ttu-id="dd15e-121">tira partido do HDInsight tootransform dados em escala e orquestração do Data Factory toohandle, agendamento, gestão de recursos e a monitorização do pipeline de processamento de lote Olá</span><span class="sxs-lookup"><span data-stu-id="dd15e-121">leverages HDInsight tootransform data at scale and Data Factory toohandle orchestration, scheduling, resource management, and monitoring of hello batch processing pipeline</span></span> 
* <span data-ttu-id="dd15e-122">fornece esta solução um dashboard avançado para dados em tempo real e visualizações de Análise Preditiva através do Power BI</span><span class="sxs-lookup"><span data-stu-id="dd15e-122">gives this solution a rich dashboard for real-time data and predictive analytics visualizations using Power BI</span></span>

## <a name="architecture"></a><span data-ttu-id="dd15e-123">Arquitetura</span><span class="sxs-lookup"><span data-stu-id="dd15e-123">Architecture</span></span>
<span data-ttu-id="dd15e-124">![Diagrama de arquitetura de solução](./media/cortana-analytics-playbook-vehicle-telemetry/fig1-vehicle-telemetry-annalytics-solution-architecture.png)
*figura 1 – arquitetura de solução de análise de telemetria Vehicle*</span><span class="sxs-lookup"><span data-stu-id="dd15e-124">![Solution architecture diagram](./media/cortana-analytics-playbook-vehicle-telemetry/fig1-vehicle-telemetry-annalytics-solution-architecture.png)
*Figure 1 – Vehicle Telemetry Analytics Solution Architecture*</span></span>

<span data-ttu-id="dd15e-125">Esta solução inclui seguinte Olá **componentes do Cortana Intelligence** e showcases os respetivos integração de tooend final:</span><span class="sxs-lookup"><span data-stu-id="dd15e-125">This solution includes hello following **Cortana Intelligence components** and showcases their end tooend integration:</span></span>

* <span data-ttu-id="dd15e-126">**Os Event Hubs** para ingestão de milhões de eventos de telemetria vehicle relacionadas no Azure.</span><span class="sxs-lookup"><span data-stu-id="dd15e-126">**Event Hubs** for ingesting millions of vehicle telemetry events into Azure.</span></span>
* <span data-ttu-id="dd15e-127">**Stream Analytics** para obter informações em tempo real no estado de funcionamento vehicle e persistir os dados para armazenamento a longo prazo para a análise de lote mais rico.</span><span class="sxs-lookup"><span data-stu-id="dd15e-127">**Stream Analytics** for gaining real-time insights on vehicle health and persists that data into long-term storage for richer batch analytics.</span></span>
* <span data-ttu-id="dd15e-128">**Machine Learning** para deteção de anomalias em tempo real e insights preditiva toogain de processamento em lote.</span><span class="sxs-lookup"><span data-stu-id="dd15e-128">**Machine Learning** for anomaly detection in real-time and batch processing toogain predictive insights.</span></span>
* <span data-ttu-id="dd15e-129">**HDInsight** aproveitadas tootransform dados à escala</span><span class="sxs-lookup"><span data-stu-id="dd15e-129">**HDInsight** is leveraged tootransform data at scale</span></span>
* <span data-ttu-id="dd15e-130">**Fábrica de dados** processa orchestration, agendamento, de gestão de recursos e monitorização do pipeline de processamento de lote Olá.</span><span class="sxs-lookup"><span data-stu-id="dd15e-130">**Data Factory** handles orchestration, scheduling, resource management and monitoring of hello batch processing pipeline.</span></span>
* <span data-ttu-id="dd15e-131">**Power BI** fornece esta solução um dashboard avançado para dados em tempo real e visualizações de Análise Preditiva.</span><span class="sxs-lookup"><span data-stu-id="dd15e-131">**Power BI** gives this solution a rich dashboard for real-time data and predictive analytics visualizations.</span></span>

<span data-ttu-id="dd15e-132">Acede a esta solução dois diferentes **origens de dados**:</span><span class="sxs-lookup"><span data-stu-id="dd15e-132">This solution accesses two different **data sources**:</span></span> 

* <span data-ttu-id="dd15e-133">**Simulated vehicle sinais e diagnóstico**: um simulador de telematics vehicle emite informações de diagnóstico e sinais que correspondem toohello Estado vehicle Olá e Olá ocasionar padrão num determinado ponto no tempo.</span><span class="sxs-lookup"><span data-stu-id="dd15e-133">**Simulated vehicle signals and diagnostics**: A vehicle telematics simulator emits diagnostic information and signals that correspond toohello state of hello vehicle and hello driving pattern at a given point in time.</span></span> 
* <span data-ttu-id="dd15e-134">**Catálogo de vehicle**: um conjunto de dados de referência que contém um mapeamento de toomodel VIN.</span><span class="sxs-lookup"><span data-stu-id="dd15e-134">**Vehicle catalog**: A reference dataset containing a VIN toomodel mapping.</span></span>

