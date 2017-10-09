---
title: "atividade de início de sessão aaaIrregular"
description: "Um relatório que inclua inícios de sessão que foi identificada como anómala pelos nossos algoritmos do machine learning."
services: active-directory
documentationcenter: 
author: SSalahAhmed
manager: gchander
editor: 
ms.assetid: a5a270a9-a0eb-4a99-b04c-ccde3829ffe4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/04/2016
ms.author: saah;kenhoff
ms.openlocfilehash: 95822ebf26404d388473cdfb7b3926be96678cdf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="irregular-sign-in-activity"></a>Atividades irregulares de início de sessão
Dados de inícios de sessão são aqueles que tenham sido identificadas pelo nosso algoritmos do machine learning, numa base de Olá de uma condição de "Impossível" combinada com um início de sessão anómalo no dispositivo e localização. Isto pode indicar que um hacker iniciou sessão com êxito utilizando esta conta.
Iremos enviar um toohello de notificação de correio eletrónico para administradores de globais se encontrarem iremos 10 ou mais anómalos início de sessão eventos num período de 30 dias ou menos. Tenha ser tooinclude se aad-alerts-noreply@mail.windowsazure.com na sua lista de remetentes seguros.

