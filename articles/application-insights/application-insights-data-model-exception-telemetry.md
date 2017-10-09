---
title: "aaaAzure modelo de dados do Application Insights telemetria - telemetria de exceção | Microsoft Docs"
description: "Modelo de dados do Application Insights para telemetria de exceção"
services: application-insights
documentationcenter: .net
author: SergeyKanzhelev
manager: carmonm
ms.service: application-insights
ms.workload: TBD
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 04/25/2017
ms.author: bwren
ms.openlocfilehash: 4c2b7d1ac3816d5623db9a35819a48a68a13a9cd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="exception-telemetry-application-insights-data-model"></a><span data-ttu-id="e5cd0-103">Telemetria de exceção: modelo de dados do Application Insights</span><span class="sxs-lookup"><span data-stu-id="e5cd0-103">Exception telemetry: Application Insights data model</span></span>

<span data-ttu-id="e5cd0-104">No [Application Insights](app-insights-overview.md), uma instância de exceção representa uma exceção não processada ou processada que ocorreram durante a execução da aplicação Olá monitorizado.</span><span class="sxs-lookup"><span data-stu-id="e5cd0-104">In [Application Insights](app-insights-overview.md), an instance of Exception represents a handled or unhandled exception that occurred during execution of hello monitored application.</span></span>

## <a name="problem-id"></a><span data-ttu-id="e5cd0-105">Id do problema</span><span class="sxs-lookup"><span data-stu-id="e5cd0-105">Problem Id</span></span>

<span data-ttu-id="e5cd0-106">Identificador do onde Olá foi emitida no código.</span><span class="sxs-lookup"><span data-stu-id="e5cd0-106">Identifier of where hello exception was thrown in code.</span></span> <span data-ttu-id="e5cd0-107">Utilizado para as exceções de agrupamento.</span><span class="sxs-lookup"><span data-stu-id="e5cd0-107">Used for exceptions grouping.</span></span> <span data-ttu-id="e5cd0-108">Normalmente, uma combinação de tipo de exceção e uma função de Olá pilha de chamadas.</span><span class="sxs-lookup"><span data-stu-id="e5cd0-108">Typically a combination of exception type and a function from hello call stack.</span></span>

<span data-ttu-id="e5cd0-109">Comprimento máximo: 1024 carateres</span><span class="sxs-lookup"><span data-stu-id="e5cd0-109">Max length: 1024 characters</span></span>

## <a name="severity-level"></a><span data-ttu-id="e5cd0-110">Nível de gravidade</span><span class="sxs-lookup"><span data-stu-id="e5cd0-110">Severity level</span></span>

<span data-ttu-id="e5cd0-111">Nível de gravidade de rastreio.</span><span class="sxs-lookup"><span data-stu-id="e5cd0-111">Trace severity level.</span></span> <span data-ttu-id="e5cd0-112">O valor pode ser `Verbose`, `Information`, `Warning`, `Error`, `Critical`.</span><span class="sxs-lookup"><span data-stu-id="e5cd0-112">Value can be `Verbose`, `Information`, `Warning`, `Error`, `Critical`.</span></span>

## <a name="exception-details"></a><span data-ttu-id="e5cd0-113">Detalhes da exceção</span><span class="sxs-lookup"><span data-stu-id="e5cd0-113">Exception details</span></span>

<span data-ttu-id="e5cd0-114">(toobe expandido)</span><span class="sxs-lookup"><span data-stu-id="e5cd0-114">(toobe extended)</span></span>

## <a name="custom-properties"></a><span data-ttu-id="e5cd0-115">Propriedades personalizadas</span><span class="sxs-lookup"><span data-stu-id="e5cd0-115">Custom properties</span></span>

[!INCLUDE [application-insights-data-model-properties](../../includes/application-insights-data-model-properties.md)]

## <a name="custom-measurements"></a><span data-ttu-id="e5cd0-116">Medidas personalizadas</span><span class="sxs-lookup"><span data-stu-id="e5cd0-116">Custom measurements</span></span>

[!INCLUDE [application-insights-data-model-measurements](../../includes/application-insights-data-model-measurements.md)]

## <a name="next-steps"></a><span data-ttu-id="e5cd0-117">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="e5cd0-117">Next steps</span></span>

- <span data-ttu-id="e5cd0-118">Consulte [modelo de dados](application-insights-data-model.md) para o modelo de tipos e os dados do Application Insights.</span><span class="sxs-lookup"><span data-stu-id="e5cd0-118">See [data model](application-insights-data-model.md) for Application Insights types and data model.</span></span>
- <span data-ttu-id="e5cd0-119">Saiba como demasiado[diagnosticar exceções nas suas aplicações web com o Application Insights](app-insights-asp-net-exceptions.md).</span><span class="sxs-lookup"><span data-stu-id="e5cd0-119">Learn how too[diagnose exceptions in your web apps with Application Insights](app-insights-asp-net-exceptions.md).</span></span>
- <span data-ttu-id="e5cd0-120">Veja [plataformas](app-insights-platforms.md) suportado pelo Application Insights.</span><span class="sxs-lookup"><span data-stu-id="e5cd0-120">Check out [platforms](app-insights-platforms.md) supported by Application Insights.</span></span>
