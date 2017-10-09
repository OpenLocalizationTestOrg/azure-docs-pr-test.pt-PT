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
# <a name="overview-of-common-autoscale-patterns"></a><span data-ttu-id="408be-103">Descrição geral de padrões comuns de dimensionamento automático</span><span class="sxs-lookup"><span data-stu-id="408be-103">Overview of common autoscale patterns</span></span>
<span data-ttu-id="408be-104">Este artigo descreve algumas das Olá tooscale de padrões comuns o recursos no Azure.</span><span class="sxs-lookup"><span data-stu-id="408be-104">This article describes some of hello common patterns tooscale your resource in Azure.</span></span>

<span data-ttu-id="408be-105">Escala de automática de Monitor do Azure aplicam-se apenas tooVirtual conjuntos de dimensionamento de máquina (VMSS), cloud services, planos de serviço de aplicações e ambientes do app service.</span><span class="sxs-lookup"><span data-stu-id="408be-105">Azure Monitor auto scale applies only tooVirtual Machine Scale Sets (VMSS), cloud services, app service plans and app service environments.</span></span> 

# <a name="lets-get-started"></a><span data-ttu-id="408be-106">Permite começar a utilizar</span><span class="sxs-lookup"><span data-stu-id="408be-106">Lets get started</span></span>

<span data-ttu-id="408be-107">Este artigo pressupõe que está familiarizado com uma escala automática.</span><span class="sxs-lookup"><span data-stu-id="408be-107">This article assumes that you are familiar with auto scale.</span></span> <span data-ttu-id="408be-108">Pode [obter introdução tooscale aqui o recurso][1].</span><span class="sxs-lookup"><span data-stu-id="408be-108">You can [get started here tooscale your resource][1].</span></span> <span data-ttu-id="408be-109">Olá são apresentados alguns dos padrões comuns da escala Olá.</span><span class="sxs-lookup"><span data-stu-id="408be-109">hello following are some of hello common scale patterns.</span></span>

## <a name="scale-based-on-cpu"></a><span data-ttu-id="408be-110">Escala com base na CPU</span><span class="sxs-lookup"><span data-stu-id="408be-110">Scale based on CPU</span></span>

<span data-ttu-id="408be-111">Tiver uma aplicação web (VMSS/nuvem função do serviço) e</span><span class="sxs-lookup"><span data-stu-id="408be-111">You have a web app (/VMSS/cloud service role) and</span></span> 

- <span data-ttu-id="408be-112">Pretende tooscale out/escala em CPU com base no.</span><span class="sxs-lookup"><span data-stu-id="408be-112">You want tooscale out/scale in based on CPU.</span></span>
- <span data-ttu-id="408be-113">Além disso, pretende tooensure há um número mínimo de instâncias.</span><span class="sxs-lookup"><span data-stu-id="408be-113">Additionally, you want tooensure there is a minimum number of instances.</span></span> 
- <span data-ttu-id="408be-114">Além disso, pretende tooensure que definir uma limite máximo toohello diversas instâncias que pode escalar.</span><span class="sxs-lookup"><span data-stu-id="408be-114">Also, you want tooensure that you set a maximum limit toohello number of instances you can scale to.</span></span>

![Escala com base na CPU][2]

## <a name="scale-differently-on-weekdays-vs-weekends"></a><span data-ttu-id="408be-116">Dimensionar de forma diferente no fim de semana do dias da semana vs</span><span class="sxs-lookup"><span data-stu-id="408be-116">Scale differently on weekdays vs weekends</span></span>

<span data-ttu-id="408be-117">Tiver uma aplicação web (VMSS/nuvem função do serviço) e</span><span class="sxs-lookup"><span data-stu-id="408be-117">You have a web app (/VMSS/cloud service role) and</span></span>

- <span data-ttu-id="408be-118">Pretende 3 instâncias por predefinição (em dias da semana)</span><span class="sxs-lookup"><span data-stu-id="408be-118">You want 3 instances by default (on weekdays)</span></span>
- <span data-ttu-id="408be-119">Não espera que o tráfego no fim de semana e, por conseguinte, pretende tooscale baixo too1 instância no fim de semana.</span><span class="sxs-lookup"><span data-stu-id="408be-119">You don't expect traffic on weekends and hence you want tooscale down too1 instance on weekends.</span></span>

![Dimensionar de forma diferente no fim de semana do dias da semana vs][3]

## <a name="scale-differently-during-holidays"></a><span data-ttu-id="408be-121">Dimensionar de forma diferente durante feriados</span><span class="sxs-lookup"><span data-stu-id="408be-121">Scale differently during holidays</span></span>

<span data-ttu-id="408be-122">Tiver uma aplicação web (VMSS/nuvem função do serviço) e</span><span class="sxs-lookup"><span data-stu-id="408be-122">You have a web app (/VMSS/cloud service role) and</span></span> 

- <span data-ttu-id="408be-123">Pretende tooscale para cima/para baixo com base na utilização da CPU por predefinição</span><span class="sxs-lookup"><span data-stu-id="408be-123">You want tooscale up/down based on CPU usage by default</span></span>
- <span data-ttu-id="408be-124">No entanto, durante a época (ou os dias específicos que são importantes para a sua empresa) pretende toooverride Olá predefinições e mais capacidade de ter no seu disposal.</span><span class="sxs-lookup"><span data-stu-id="408be-124">However, during holiday season (or specific days that are important for your business) you want toooverride hello defaults and have more capacity at your disposal.</span></span>

![Feriados de forma diferente em escala][4]

## <a name="scale-based-on-custom-metric"></a><span data-ttu-id="408be-126">Escala com base numa métrica personalizada</span><span class="sxs-lookup"><span data-stu-id="408be-126">Scale based on custom metric</span></span>

<span data-ttu-id="408be-127">Tem um front-end da web e uma camada de API que comunica com o back-end de Olá.</span><span class="sxs-lookup"><span data-stu-id="408be-127">You have a web front end and a API tier that communicates with hello backend.</span></span> 

- <span data-ttu-id="408be-128">Pretende que a camada de Olá API tooscale com base em eventos personalizados no front-end de Olá (exemplo: pretende que o processo de finalização da compra com base no número de Olá de itens na Olá carrinho de compras de tooscale)</span><span class="sxs-lookup"><span data-stu-id="408be-128">You want tooscale hello API tier based on custom events in hello front end (example: You want tooscale your checkout process based on hello number of items in hello shopping cart)</span></span>

![Escala com base numa métrica personalizada][5]

<!--Reference-->
[1]: ./monitoring-autoscale-get-started.md
[2]: ./media/monitoring-autoscale-common-scale-patterns/scale-based-on-cpu.png
[3]: ./media/monitoring-autoscale-common-scale-patterns/weekday-weekend-scale.png
[4]: ./media/monitoring-autoscale-common-scale-patterns/holidays-scale.png
[5]: ./media/monitoring-autoscale-common-scale-patterns/custom-metric-scale.png