---
title: "AAA \"eventos de início de eliminação de agrupamento do Azure Batch | Microsoft Docs\""
description: "Referência para o evento de início de eliminação de conjunto de Batch."
services: batch
author: tamram
manager: timlt
ms.assetid: 
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 04/20/2017
ms.author: tamram
ms.openlocfilehash: 79bb28bffc760a49cc0a95062f5086dc96c6a795
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="pool-delete-start-event"></a><span data-ttu-id="c0a58-103">Eventos de início de eliminação do conjunto</span><span class="sxs-lookup"><span data-stu-id="c0a58-103">Pool delete start event</span></span>

 <span data-ttu-id="c0a58-104">Este evento é emitido quando foi iniciada uma operação de eliminação do conjunto.</span><span class="sxs-lookup"><span data-stu-id="c0a58-104">This event is emitted when a pool delete operation has started.</span></span> <span data-ttu-id="c0a58-105">Uma vez que a eliminação do conjunto de Olá é um evento assíncrono, que pode esperar um evento completa de eliminação conjunto toobe emitido depois da operação de eliminação de Olá for concluída.</span><span class="sxs-lookup"><span data-stu-id="c0a58-105">Since hello pool delete is an asynchronous event, you can expect a pool delete complete event toobe emitted once hello delete operation completes.</span></span>

 <span data-ttu-id="c0a58-106">Olá exemplo seguinte mostra corpo Olá de um evento de início de eliminação do conjunto.</span><span class="sxs-lookup"><span data-stu-id="c0a58-106">hello following example shows hello body of a pool delete start event.</span></span>

```
{
    "id": "myPool1"
}
```

|<span data-ttu-id="c0a58-107">Elemento</span><span class="sxs-lookup"><span data-stu-id="c0a58-107">Element</span></span>|<span data-ttu-id="c0a58-108">Tipo</span><span class="sxs-lookup"><span data-stu-id="c0a58-108">Type</span></span>|<span data-ttu-id="c0a58-109">Notas</span><span class="sxs-lookup"><span data-stu-id="c0a58-109">Notes</span></span>|
|-------------|----------|-----------|
|<span data-ttu-id="c0a58-110">ID</span><span class="sxs-lookup"><span data-stu-id="c0a58-110">id</span></span>|<span data-ttu-id="c0a58-111">Cadeia</span><span class="sxs-lookup"><span data-stu-id="c0a58-111">String</span></span>|<span data-ttu-id="c0a58-112">id do conjunto de Olá Olá.</span><span class="sxs-lookup"><span data-stu-id="c0a58-112">hello id of hello pool.</span></span>|
