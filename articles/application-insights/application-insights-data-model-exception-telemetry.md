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
# <a name="exception-telemetry-application-insights-data-model"></a>Telemetria de exceção: modelo de dados do Application Insights

No [Application Insights](app-insights-overview.md), uma instância de exceção representa uma exceção não processada ou processada que ocorreram durante a execução da aplicação Olá monitorizado.

## <a name="problem-id"></a>Id do problema

Identificador do onde Olá foi emitida no código. Utilizado para as exceções de agrupamento. Normalmente, uma combinação de tipo de exceção e uma função de Olá pilha de chamadas.

Comprimento máximo: 1024 carateres

## <a name="severity-level"></a>Nível de gravidade

Nível de gravidade de rastreio. O valor pode ser `Verbose`, `Information`, `Warning`, `Error`, `Critical`.

## <a name="exception-details"></a>Detalhes da exceção

(toobe expandido)

## <a name="custom-properties"></a>Propriedades personalizadas

[!INCLUDE [application-insights-data-model-properties](../../includes/application-insights-data-model-properties.md)]

## <a name="custom-measurements"></a>Medidas personalizadas

[!INCLUDE [application-insights-data-model-measurements](../../includes/application-insights-data-model-measurements.md)]

## <a name="next-steps"></a>Passos seguintes

- Consulte [modelo de dados](application-insights-data-model.md) para o modelo de tipos e os dados do Application Insights.
- Saiba como demasiado[diagnosticar exceções nas suas aplicações web com o Application Insights](app-insights-asp-net-exceptions.md).
- Veja [plataformas](app-insights-platforms.md) suportado pelo Application Insights.
