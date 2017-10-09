---
title: "aaaCreate um ambiente de informações de séries de tempo do Azure | Microsoft Docs"
description: "Neste tutorial, ficará a saber como toocreate ambiente de séries de tempo, ligue-a origem de evento tooan e pronto tooanalyze os dados de eventos em minutos."
keywords: 
services: time-series-insights
documentationcenter: 
author: op-ravi
manager: santoshb
editor: cgronlun
ms.assetid: 
ms.service: time-series-insights
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/21/2017
ms.author: omravi
ms.openlocfilehash: 7120fc9a6e4d4a4972f8cb37e4d9945cfb746fd2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-new-time-series-insights-environment-in-hello-azure-portal"></a><span data-ttu-id="b2af7-103">Criar um novo ambiente de informações de séries de tempo no Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="b2af7-103">Create a new Time Series Insights environment in hello Azure portal</span></span>

<span data-ttu-id="b2af7-104">O ambiente do Time Series Insights é um recurso do Azure com capacidade de receção e armazenamento.</span><span class="sxs-lookup"><span data-stu-id="b2af7-104">Time Series Insights environment is an Azure resource with ingress and storage capacity.</span></span> <span data-ttu-id="b2af7-105">Os clientes aprovisionar ambientes através do portal do Azure de Olá com capacidade de Olá necessário.</span><span class="sxs-lookup"><span data-stu-id="b2af7-105">Customers provision environments via hello Azure portal with hello required capacity.</span></span>

## <a name="steps-toocreate-hello-environment"></a><span data-ttu-id="b2af7-106">Ambiente de Olá passos toocreate</span><span class="sxs-lookup"><span data-stu-id="b2af7-106">Steps toocreate hello environment</span></span>

<span data-ttu-id="b2af7-107">Siga estes passos toocreate seu ambiente:</span><span class="sxs-lookup"><span data-stu-id="b2af7-107">Follow these steps toocreate your environment:</span></span>

1.  <span data-ttu-id="b2af7-108">Inicie sessão no toohello [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b2af7-108">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2.  <span data-ttu-id="b2af7-109">Clique em Olá sinal de adição ("+"), na parte superior Olá esquerda canto.</span><span class="sxs-lookup"><span data-stu-id="b2af7-109">Click hello plus sign (“+”) in hello top left corner.</span></span>
3.  <span data-ttu-id="b2af7-110">Procure "Insights de séries de tempo" na caixa de pesquisa de Olá.</span><span class="sxs-lookup"><span data-stu-id="b2af7-110">Search for “Time Series Insights” in hello search box.</span></span>

  ![Criar ambiente de informações de séries de tempo de Olá](media/get-started/getstarted-create-environment1.png)

4.  <span data-ttu-id="b2af7-112">Selecione "Time Series Insights", clique em "Criar".</span><span class="sxs-lookup"><span data-stu-id="b2af7-112">Select “Time Series Insights”, click “Create”.</span></span>

  ![Criar grupo de recursos de informações de séries de tempo de Olá](media/get-started/getstarted-create-environment2.png)

5.  <span data-ttu-id="b2af7-114">Especifique o nome do ambiente.</span><span class="sxs-lookup"><span data-stu-id="b2af7-114">Specify environment name.</span></span> <span data-ttu-id="b2af7-115">Este nome irá representar o ambiente de Olá no [Explorador de séries de tempo](https://insights.timeseries.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b2af7-115">This name will represent hello environment in [time series explorer](https://insights.timeseries.azure.com).</span></span>
6.  <span data-ttu-id="b2af7-116">Selecione uma subscrição.</span><span class="sxs-lookup"><span data-stu-id="b2af7-116">Select a subscription.</span></span> <span data-ttu-id="b2af7-117">Escolha uma que contenha a origem do evento.</span><span class="sxs-lookup"><span data-stu-id="b2af7-117">Choose one that contains your event source.</span></span> <span data-ttu-id="b2af7-118">Informações de séries de tempo pode deteção automática do Azure IoT Hub e Olá de recursos de Hub de eventos existentes na mesma subscrição.</span><span class="sxs-lookup"><span data-stu-id="b2af7-118">Time Series Insights can auto-detect Azure IoT Hub and Event Hub resources existing in hello same subscription.</span></span>
7.  <span data-ttu-id="b2af7-119">Selecione ou crie um grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="b2af7-119">Select or create a resource group.</span></span> <span data-ttu-id="b2af7-120">Um grupo de recursos é uma coleção de recursos do Azure utilizados em conjunto.</span><span class="sxs-lookup"><span data-stu-id="b2af7-120">A resource group is a collection of Azure resources used together.</span></span>
8.  <span data-ttu-id="b2af7-121">Selecione uma localização de alojamento.</span><span class="sxs-lookup"><span data-stu-id="b2af7-121">Select a hosting location.</span></span> <span data-ttu-id="b2af7-122">os centros de dados de mover tooavoid em dados, escolha a localização que contém a origem de evento.</span><span class="sxs-lookup"><span data-stu-id="b2af7-122">tooavoid moving data across data centers, choose location that contains your event source.</span></span>
9.  <span data-ttu-id="b2af7-123">Selecione um escalão de preço.</span><span class="sxs-lookup"><span data-stu-id="b2af7-123">Select a pricing tier.</span></span>
10. <span data-ttu-id="b2af7-124">Selecione a capacidade.</span><span class="sxs-lookup"><span data-stu-id="b2af7-124">Select capacity.</span></span> <span data-ttu-id="b2af7-125">Pode alterar a capacidade de um ambiente após a criação.</span><span class="sxs-lookup"><span data-stu-id="b2af7-125">You can change capacity of an environment after creation.</span></span>
11. <span data-ttu-id="b2af7-126">Crie o seu ambiente.</span><span class="sxs-lookup"><span data-stu-id="b2af7-126">Create your environment.</span></span> <span data-ttu-id="b2af7-127">Também pode afixar o dashboard de toohello ambiente para facilitar o acesso sempre que iniciar sessão.</span><span class="sxs-lookup"><span data-stu-id="b2af7-127">You can also pin your environment toohello dashboard for easy access whenever you sign in.</span></span>

  ![Criar Olá Insights de séries de tempo pin toodashboard](media/get-started/getstarted-create-environment3.png)

## <a name="next-steps"></a><span data-ttu-id="b2af7-129">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="b2af7-129">Next steps</span></span>

* <span data-ttu-id="b2af7-130">[Definir políticas de acesso de dados](time-series-insights-data-access.md) tooaccess ambiente na [Portal de informações de séries de tempo](https://insights.timeseries.azure.com)</span><span class="sxs-lookup"><span data-stu-id="b2af7-130">[Define data access policies](time-series-insights-data-access.md) tooaccess your environment in [Time Series Insights Portal](https://insights.timeseries.azure.com)</span></span>
* [<span data-ttu-id="b2af7-131">Criar uma origem de eventos</span><span class="sxs-lookup"><span data-stu-id="b2af7-131">Create an event source</span></span>](time-series-insights-add-event-source.md)
* <span data-ttu-id="b2af7-132">[Enviar eventos](time-series-insights-send-events.md) toohello origem de evento</span><span class="sxs-lookup"><span data-stu-id="b2af7-132">[Send events](time-series-insights-send-events.md) toohello event source</span></span>
