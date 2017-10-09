---
title: "aaaWindows conteúdo Universal SDK de aplicações"
description: "Saiba mais sobre o conteúdo Olá Olá SDK Windows Universal do aplicações do Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 8fa1b701-1c2b-4aec-940c-06c974ef5405
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: a8013d2433c0be62d737c8bc6e8360ed79bbe532
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="windows-universal-apps-sdk-content"></a>Conteúdo do SDK de aplicações universais do Windows
Este documento apresenta e descreve o conteúdo de Olá implementado por Olá SDK na sua aplicação.

## <a name="hello-resources-folder"></a>Olá `/Resources` pasta
Esta pasta contém todos os recursos de Olá que necessita de Mobile Engagement. Também pode personalizá-las toofit a aplicação.

* `EngagementConfiguration.xml`: Olá o ficheiro de configuração do Mobile Engagement, isto é onde pode personalizar as definições de Mobile Engagement (cadeia de ligação do Mobile Engagement, falhas de relatório...).

### <a name="html-folder"></a>pasta /HTML
* `EngagementNotification.html`: Olá `Notification` web estrutura de html da vista de faixas na aplicação.
* `EngagementAnnouncement.html`: Olá `Announcement` web estrutura da vista html para vistas interstitial na aplicação.

### <a name="images-folder"></a>pasta /Images
* `EngagementIconNotification.png`: ícone de marca de Olá apresentado em Olá à esquerda de uma notificação, substituir este pelo ícone de marca.
* `EngagementIconOk.png`: Olá `Ok` ícone de páginas de conteúdo de alcance de Olá para botão de ação ou validação de Olá.
* `EngagementIconNOK.png`: Olá `NOK` ícone utilizado quando o botão de validação de Olá das páginas de conteúdo de alcance Olá está desativado.
* `EngagementIconClose.png`: Olá `Close` ícone de Olá alcançar notificações e conteúdo Olá dispensa botão.

### <a name="overlay-folder"></a>pasta /Overlay
* `EngagementPageOverlay.cs`: Olá sobreposição página responsável pela adição Olá alcance do Engagement subordinado de tooits de IU na aplicação.

