---
title: "Recursos de aplicação Web de aaaMove tooanother grupo de recursos"
description: "Descreve os cenários de olá onde pode mover as aplicações Web e serviços de aplicação de um grupo de recursos tooanother."
services: app-service
documentationcenter: 
author: ZainRizvi
manager: erikre
editor: 
ms.assetid: 22f97607-072e-4d1f-a46f-8d500420c33c
ms.service: app-service
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/21/2016
ms.author: zarizvi
ms.openlocfilehash: 931012fee656b7f8a4b2c225c38739a9171d3b2e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="supported-move-configurations"></a>Configurações de movimentação suportados
Pode mover recursos de aplicação Web do Azure através de Olá [Resource Manager mover recursos API](../azure-resource-manager/resource-group-move-resources.md).

As aplicações Web do Azure suporta atualmente Olá cenários de mover os seguintes:

* Mover Olá conteúdos completo de um grupo de recursos (web apps, planos de serviço de aplicações e certificados) tooanother grupo de recursos. 
   > [!Note]
   > grupo de recursos de destino Olá não pode conter quaisquer recursos Microsoft. Web neste cenário.

* Mova grupo de recursos diferente de tooa de aplicações web individuais, ao mesmo tempo ainda alojá-los no seu atual plano do app service (Olá aplicação serviço plano mantém-se no grupo de recursos antigo Olá).


