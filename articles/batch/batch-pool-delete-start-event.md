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
# <a name="pool-delete-start-event"></a>Eventos de início de eliminação do conjunto

 Este evento é emitido quando foi iniciada uma operação de eliminação do conjunto. Uma vez que a eliminação do conjunto de Olá é um evento assíncrono, que pode esperar um evento completa de eliminação conjunto toobe emitido depois da operação de eliminação de Olá for concluída.

 Olá exemplo seguinte mostra corpo Olá de um evento de início de eliminação do conjunto.

```
{
    "id": "myPool1"
}
```

|Elemento|Tipo|Notas|
|-------------|----------|-----------|
|ID|Cadeia|id do conjunto de Olá Olá.|
