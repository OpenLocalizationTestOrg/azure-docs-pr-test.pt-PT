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
# <a name="supportability-of-adding-azure-vms-tooan-existing-availability-set"></a>Suporte de adição de conjunto de disponibilidade existente tooan VMs do Azure

Ocasionalmente, poderá encontrar limitações ao adicionar novas máquinas virtuais (VMs) tooan conjunto de disponibilidade existente. Olá os detalhes do gráfico que série VM pode misturar no Olá mesmo conjunto de disponibilidade.

Eis Olá Suportabilidade matriz toomix diferentes tipos de VMs:

Série & conjunto de disponibilidade|VM segundo|A|Av2|D|Dv2|Dv3|
|---|---|---|---|---|---|---|
|Primeira VM|||||||
|A||OK|OK|OK|OK|OK|
|Av2||OK|OK|OK|OK|OK|
|D||OK|OK|OK|OK|OK|
|Dv2||OK|OK|OK|OK|OK|
|Dv3||OK|OK|OK|OK|OK|

Todos os outro série não foi possível no Olá do conjunto de disponibilidade mesma pois requerem que um hardware específico.
