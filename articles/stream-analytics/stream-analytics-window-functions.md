---
title: "as funções de janela de análise do aaaIntroduction tooStream | Microsoft Docs"
description: "Saiba mais sobre Olá três as funções de janela no Stream Analytics (em cascata, hopping, a deslizante)."
keywords: em cascata janela, numa janela, hopping janela deslizante
documentationcenter: 
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 0d8d8717-5d23-43f0-b475-af078ab4627d
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 7fc36eb9afb2b28e2791d925d26923145eb38074
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toostream-analytics-window-functions"></a><span data-ttu-id="6eabf-104">Funções de janela de análise de tooStream de introdução</span><span class="sxs-lookup"><span data-stu-id="6eabf-104">Introduction tooStream Analytics Window functions</span></span>
<span data-ttu-id="6eabf-105">Em tempo real muitos cenários de transmissão em fluxo, é necessário tooperform operações apenas nos dados de Olá contidos no windows temporais.</span><span class="sxs-lookup"><span data-stu-id="6eabf-105">In many real time streaming scenarios, it is necessary tooperform operations only on hello data contained in temporal windows.</span></span> <span data-ttu-id="6eabf-106">Suporte nativo para funções de modos de janela é uma funcionalidade chave do Azure Stream Analytics que são transmitidos agulha Olá na produtividade do programador na criação as tarefas de processamento de fluxo complexas.</span><span class="sxs-lookup"><span data-stu-id="6eabf-106">Native support for windowing functions is a key feature of Azure Stream Analytics that moves hello needle on developer productivity in authoring complex stream processing jobs.</span></span> <span data-ttu-id="6eabf-107">Do Stream Analytics permite aos programadores toouse [ **em cascata**](https://msdn.microsoft.com/library/dn835055.aspx), [ **Hopping** ](https://msdn.microsoft.com/library/dn835041.aspx) e [ **deslizantes** ](https://msdn.microsoft.com/library/dn835051.aspx) windows tooperform temporal operações dados de transmissão em fluxo.</span><span class="sxs-lookup"><span data-stu-id="6eabf-107">Stream Analytics enables developers toouse [**Tumbling**](https://msdn.microsoft.com/library/dn835055.aspx), [**Hopping**](https://msdn.microsoft.com/library/dn835041.aspx) and [**Sliding**](https://msdn.microsoft.com/library/dn835051.aspx) windows tooperform temporal operations on streaming data.</span></span> <span data-ttu-id="6eabf-108">É importante salientar que, todos os [janela](https://msdn.microsoft.com/library/dn835019.aspx) operações saída resultados em Olá **final** da janela de Olá.</span><span class="sxs-lookup"><span data-stu-id="6eabf-108">It is worth noting that all [Window](https://msdn.microsoft.com/library/dn835019.aspx) operations output results at hello **end** of hello window.</span></span> <span data-ttu-id="6eabf-109">saída de Olá da janela de Olá será evento único com base na função de agregação Olá utilizada.</span><span class="sxs-lookup"><span data-stu-id="6eabf-109">hello output of hello window will be single event based on hello aggregate function used.</span></span> <span data-ttu-id="6eabf-110">evento de Olá terão carimbo de hora Olá da extremidade Olá da janela de Olá e todas as funções de janela estão definidas com um comprimento fixo.</span><span class="sxs-lookup"><span data-stu-id="6eabf-110">hello event will have hello time stamp of hello end of hello window and all Window functions are defined with a fixed length.</span></span> <span data-ttu-id="6eabf-111">Por último é importante toonote que todas as funções de janela devem ser utilizadas num [ **GROUP BY** ](https://msdn.microsoft.com/library/dn835023.aspx) cláusula.</span><span class="sxs-lookup"><span data-stu-id="6eabf-111">Lastly it is important toonote that all Window functions should be used in a [**GROUP BY**](https://msdn.microsoft.com/library/dn835023.aspx) clause.</span></span>

![Conceitos de funções de janela de análise de fluxo](media/stream-analytics-window-functions/stream-analytics-window-functions-conceptual.png)

## <a name="tumbling-window"></a><span data-ttu-id="6eabf-113">Janela em cascata</span><span class="sxs-lookup"><span data-stu-id="6eabf-113">Tumbling Window</span></span>
<span data-ttu-id="6eabf-114">As funções de janela em cascata são utilizado toosegment um fluxo de dados em segmentos de hora diferente e uma função contra eles, como exemplo de Olá abaixo.</span><span class="sxs-lookup"><span data-stu-id="6eabf-114">Tumbling window functions are used toosegment a data stream into distinct time segments and perform a function against them, such as hello example below.</span></span> <span data-ttu-id="6eabf-115">differentiators de chave Olá de uma janela em cascata são que eles repetir, não se sobreponha e um evento não pode pertencer toomore que uma janela em cascata.</span><span class="sxs-lookup"><span data-stu-id="6eabf-115">hello key differentiators of a Tumbling window are that they repeat, do not overlap and an event cannot belong toomore than one tumbling window.</span></span>

![Funções de janela de análise de fluxo em cascata introdução](media/stream-analytics-window-functions/stream-analytics-window-functions-tumbling-intro.png)

## <a name="hopping-window"></a><span data-ttu-id="6eabf-117">Janela de salto</span><span class="sxs-lookup"><span data-stu-id="6eabf-117">Hopping Window</span></span>
<span data-ttu-id="6eabf-118">Salto salto de funções de janela reencaminhar na hora por um período fixo.</span><span class="sxs-lookup"><span data-stu-id="6eabf-118">Hopping window functions hop forward in time by a fixed period.</span></span> <span data-ttu-id="6eabf-119">Poderá ser toothink fácil deles como janelas em cascata podem sobrepor-se, pelo que os eventos podem pertencer toomore que um conjunto de resultados de janela Hopping.</span><span class="sxs-lookup"><span data-stu-id="6eabf-119">It may be easy toothink of them as Tumbling windows that can overlap, so events can belong toomore than one Hopping window result set.</span></span> <span data-ttu-id="6eabf-120">toomake uma janela de Hopping Olá mesmo como uma janela em cascata um especificaria simplesmente toobe de tamanho de salto Olá Olá mesmo como o tamanho da janela Olá.</span><span class="sxs-lookup"><span data-stu-id="6eabf-120">toomake a Hopping window hello same as a Tumbling window one would simply specify hello hop size toobe hello same as hello window size.</span></span> 

![Janela do Stream Analytics funciona salto de introdução](media/stream-analytics-window-functions/stream-analytics-window-functions-hopping-intro.png)

## <a name="sliding-window"></a><span data-ttu-id="6eabf-122">Numa janela deslizante</span><span class="sxs-lookup"><span data-stu-id="6eabf-122">Sliding Window</span></span>
<span data-ttu-id="6eabf-123">Funções de janela deslizante, ao contrário do salto windows, ou em cascata produzem uma saída **apenas** quando ocorre um evento.</span><span class="sxs-lookup"><span data-stu-id="6eabf-123">Sliding window functions, unlike Tumbling or Hopping windows, produce an output **only**  when an event occurs.</span></span> <span data-ttu-id="6eabf-124">Cada janela vai ter, pelo menos, um evento e janela Olá continuamente move reencaminhar por um € (epsilon).</span><span class="sxs-lookup"><span data-stu-id="6eabf-124">Every window will have at least one event and hello window continuously moves forward by an € (epsilon).</span></span> <span data-ttu-id="6eabf-125">Como salto Windows, os eventos podem pertencer toomore que uma janela a deslizante.</span><span class="sxs-lookup"><span data-stu-id="6eabf-125">Like Hopping Windows, events can belong toomore than one Sliding Window.</span></span>

![Funções de Stream Analytics janela deslizante de introdução](media/stream-analytics-window-functions/stream-analytics-window-functions-sliding-intro.png)

## <a name="getting-help-with-window-functions"></a><span data-ttu-id="6eabf-127">Obter ajuda com as funções de janela</span><span class="sxs-lookup"><span data-stu-id="6eabf-127">Getting help with Window functions</span></span>
<span data-ttu-id="6eabf-128">Para mais assistência, tente ler o nosso [fórum do Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="6eabf-128">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="6eabf-129">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="6eabf-129">Next steps</span></span>
* [<span data-ttu-id="6eabf-130">Introdução tooAzure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="6eabf-130">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="6eabf-131">Começar a utilizar o Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="6eabf-131">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="6eabf-132">Tarefas de escala do Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="6eabf-132">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="6eabf-133">Referência do idioma de consulta do Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="6eabf-133">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="6eabf-134">Referência de API do REST de gestão do Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="6eabf-134">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

