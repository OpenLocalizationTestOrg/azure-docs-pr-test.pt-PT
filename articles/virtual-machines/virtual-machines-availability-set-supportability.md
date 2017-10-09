---
title: "aaaSupportability da adição de conjunto de disponibilidade existente tooan VMs do Azure | Microsoft Docs"
description: "Suporte de adição de conjunto de disponibilidade existente tooan VMs do Azure."
services: virtual-machines-linux
documentationcenter: 
author: Deland-Han
manager: cshepard
editor: 
ms.assetid: 
ms.service: virtual-machines
ms.workload: virtual-machines
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/15/2017
ms.author: delhan
ms.openlocfilehash: dc2bd86b916f1d1a0a0d4c9e870df829434c96b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="supportability-of-adding-azure-vms-tooan-existing-availability-set"></a><span data-ttu-id="2bd15-103">Suporte de adição de conjunto de disponibilidade existente tooan VMs do Azure</span><span class="sxs-lookup"><span data-stu-id="2bd15-103">Supportability of adding Azure VMs tooan existing availability set</span></span>

<span data-ttu-id="2bd15-104">Ocasionalmente, poderá encontrar limitações ao adicionar novas máquinas virtuais (VMs) tooan conjunto de disponibilidade existente.</span><span class="sxs-lookup"><span data-stu-id="2bd15-104">You may occasionally encounter limitations when you add new virtual machines (VMs) tooan existing availability set.</span></span> <span data-ttu-id="2bd15-105">Olá os detalhes do gráfico que série VM pode misturar no Olá mesmo conjunto de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="2bd15-105">hello following chart details which VM series you can mix in hello same availability set.</span></span>

<span data-ttu-id="2bd15-106">Eis Olá Suportabilidade matriz toomix diferentes tipos de VMs:</span><span class="sxs-lookup"><span data-stu-id="2bd15-106">Here is hello supportability matrix toomix different types of VMs:</span></span>

<span data-ttu-id="2bd15-107">Série & conjunto de disponibilidade</span><span class="sxs-lookup"><span data-stu-id="2bd15-107">Series & Availability Set</span></span>|<span data-ttu-id="2bd15-108">VM segundo</span><span class="sxs-lookup"><span data-stu-id="2bd15-108">Second VM</span></span>|<span data-ttu-id="2bd15-109">A</span><span class="sxs-lookup"><span data-stu-id="2bd15-109">A</span></span>|<span data-ttu-id="2bd15-110">Av2</span><span class="sxs-lookup"><span data-stu-id="2bd15-110">Av2</span></span>|<span data-ttu-id="2bd15-111">D</span><span class="sxs-lookup"><span data-stu-id="2bd15-111">D</span></span>|<span data-ttu-id="2bd15-112">Dv2</span><span class="sxs-lookup"><span data-stu-id="2bd15-112">Dv2</span></span>|<span data-ttu-id="2bd15-113">Dv3</span><span class="sxs-lookup"><span data-stu-id="2bd15-113">Dv3</span></span>|
|---|---|---|---|---|---|---|
|<span data-ttu-id="2bd15-114">Primeira VM</span><span class="sxs-lookup"><span data-stu-id="2bd15-114">First VM</span></span>|||||||
|<span data-ttu-id="2bd15-115">A</span><span class="sxs-lookup"><span data-stu-id="2bd15-115">A</span></span>||<span data-ttu-id="2bd15-116">OK</span><span class="sxs-lookup"><span data-stu-id="2bd15-116">OK</span></span>|<span data-ttu-id="2bd15-117">OK</span><span class="sxs-lookup"><span data-stu-id="2bd15-117">OK</span></span>|<span data-ttu-id="2bd15-118">OK</span><span class="sxs-lookup"><span data-stu-id="2bd15-118">OK</span></span>|<span data-ttu-id="2bd15-119">OK</span><span class="sxs-lookup"><span data-stu-id="2bd15-119">OK</span></span>|<span data-ttu-id="2bd15-120">OK</span><span class="sxs-lookup"><span data-stu-id="2bd15-120">OK</span></span>|
|<span data-ttu-id="2bd15-121">Av2</span><span class="sxs-lookup"><span data-stu-id="2bd15-121">Av2</span></span>||<span data-ttu-id="2bd15-122">OK</span><span class="sxs-lookup"><span data-stu-id="2bd15-122">OK</span></span>|<span data-ttu-id="2bd15-123">OK</span><span class="sxs-lookup"><span data-stu-id="2bd15-123">OK</span></span>|<span data-ttu-id="2bd15-124">OK</span><span class="sxs-lookup"><span data-stu-id="2bd15-124">OK</span></span>|<span data-ttu-id="2bd15-125">OK</span><span class="sxs-lookup"><span data-stu-id="2bd15-125">OK</span></span>|<span data-ttu-id="2bd15-126">OK</span><span class="sxs-lookup"><span data-stu-id="2bd15-126">OK</span></span>|
|<span data-ttu-id="2bd15-127">D</span><span class="sxs-lookup"><span data-stu-id="2bd15-127">D</span></span>||<span data-ttu-id="2bd15-128">OK</span><span class="sxs-lookup"><span data-stu-id="2bd15-128">OK</span></span>|<span data-ttu-id="2bd15-129">OK</span><span class="sxs-lookup"><span data-stu-id="2bd15-129">OK</span></span>|<span data-ttu-id="2bd15-130">OK</span><span class="sxs-lookup"><span data-stu-id="2bd15-130">OK</span></span>|<span data-ttu-id="2bd15-131">OK</span><span class="sxs-lookup"><span data-stu-id="2bd15-131">OK</span></span>|<span data-ttu-id="2bd15-132">OK</span><span class="sxs-lookup"><span data-stu-id="2bd15-132">OK</span></span>|
|<span data-ttu-id="2bd15-133">Dv2</span><span class="sxs-lookup"><span data-stu-id="2bd15-133">Dv2</span></span>||<span data-ttu-id="2bd15-134">OK</span><span class="sxs-lookup"><span data-stu-id="2bd15-134">OK</span></span>|<span data-ttu-id="2bd15-135">OK</span><span class="sxs-lookup"><span data-stu-id="2bd15-135">OK</span></span>|<span data-ttu-id="2bd15-136">OK</span><span class="sxs-lookup"><span data-stu-id="2bd15-136">OK</span></span>|<span data-ttu-id="2bd15-137">OK</span><span class="sxs-lookup"><span data-stu-id="2bd15-137">OK</span></span>|<span data-ttu-id="2bd15-138">OK</span><span class="sxs-lookup"><span data-stu-id="2bd15-138">OK</span></span>|
|<span data-ttu-id="2bd15-139">Dv3</span><span class="sxs-lookup"><span data-stu-id="2bd15-139">Dv3</span></span>||<span data-ttu-id="2bd15-140">OK</span><span class="sxs-lookup"><span data-stu-id="2bd15-140">OK</span></span>|<span data-ttu-id="2bd15-141">OK</span><span class="sxs-lookup"><span data-stu-id="2bd15-141">OK</span></span>|<span data-ttu-id="2bd15-142">OK</span><span class="sxs-lookup"><span data-stu-id="2bd15-142">OK</span></span>|<span data-ttu-id="2bd15-143">OK</span><span class="sxs-lookup"><span data-stu-id="2bd15-143">OK</span></span>|<span data-ttu-id="2bd15-144">OK</span><span class="sxs-lookup"><span data-stu-id="2bd15-144">OK</span></span>|

<span data-ttu-id="2bd15-145">Todos os outro série não foi possível no Olá do conjunto de disponibilidade mesma pois requerem que um hardware específico.</span><span class="sxs-lookup"><span data-stu-id="2bd15-145">All other series could not be in hello same availability set because they require a specific hardware.</span></span>
