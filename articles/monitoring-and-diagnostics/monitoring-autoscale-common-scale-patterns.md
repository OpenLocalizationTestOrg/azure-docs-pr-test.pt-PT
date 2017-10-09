---
title: "aaaOverview de padrões comuns de dimensionamento automático | Microsoft Docs"
description: "Saiba mais que alguns dos tooauto de padrões comuns Olá dimensionar os recursos no Azure."
author: anirudhcavale
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: d37d3fda-8ef1-477c-a360-a855b418de84
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/07/2017
ms.author: ancav
ms.openlocfilehash: fc5bd97852e0af01aa32940c99721ab8e21033ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-common-autoscale-patterns"></a>Descrição geral de padrões comuns de dimensionamento automático
Este artigo descreve algumas das Olá tooscale de padrões comuns o recursos no Azure.

Escala de automática de Monitor do Azure aplicam-se apenas tooVirtual conjuntos de dimensionamento de máquina (VMSS), cloud services, planos de serviço de aplicações e ambientes do app service. 

# <a name="lets-get-started"></a>Permite começar a utilizar

Este artigo pressupõe que está familiarizado com uma escala automática. Pode [obter introdução tooscale aqui o recurso][1]. Olá são apresentados alguns dos padrões comuns da escala Olá.

## <a name="scale-based-on-cpu"></a>Escala com base na CPU

Tiver uma aplicação web (VMSS/nuvem função do serviço) e 

- Pretende tooscale out/escala em CPU com base no.
- Além disso, pretende tooensure há um número mínimo de instâncias. 
- Além disso, pretende tooensure que definir uma limite máximo toohello diversas instâncias que pode escalar.

![Escala com base na CPU][2]

## <a name="scale-differently-on-weekdays-vs-weekends"></a>Dimensionar de forma diferente no fim de semana do dias da semana vs

Tiver uma aplicação web (VMSS/nuvem função do serviço) e

- Pretende 3 instâncias por predefinição (em dias da semana)
- Não espera que o tráfego no fim de semana e, por conseguinte, pretende tooscale baixo too1 instância no fim de semana.

![Dimensionar de forma diferente no fim de semana do dias da semana vs][3]

## <a name="scale-differently-during-holidays"></a>Dimensionar de forma diferente durante feriados

Tiver uma aplicação web (VMSS/nuvem função do serviço) e 

- Pretende tooscale para cima/para baixo com base na utilização da CPU por predefinição
- No entanto, durante a época (ou os dias específicos que são importantes para a sua empresa) pretende toooverride Olá predefinições e mais capacidade de ter no seu disposal.

![Feriados de forma diferente em escala][4]

## <a name="scale-based-on-custom-metric"></a>Escala com base numa métrica personalizada

Tem um front-end da web e uma camada de API que comunica com o back-end de Olá. 

- Pretende que a camada de Olá API tooscale com base em eventos personalizados no front-end de Olá (exemplo: pretende que o processo de finalização da compra com base no número de Olá de itens na Olá carrinho de compras de tooscale)

![Escala com base numa métrica personalizada][5]

<!--Reference-->
[1]: ./monitoring-autoscale-get-started.md
[2]: ./media/monitoring-autoscale-common-scale-patterns/scale-based-on-cpu.png
[3]: ./media/monitoring-autoscale-common-scale-patterns/weekday-weekend-scale.png
[4]: ./media/monitoring-autoscale-common-scale-patterns/holidays-scale.png
[5]: ./media/monitoring-autoscale-common-scale-patterns/custom-metric-scale.png