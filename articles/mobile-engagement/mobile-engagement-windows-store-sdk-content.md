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
# <a name="windows-universal-apps-sdk-content"></a><span data-ttu-id="90e43-103">Conteúdo do SDK de aplicações universais do Windows</span><span class="sxs-lookup"><span data-stu-id="90e43-103">Windows Universal Apps SDK content</span></span>
<span data-ttu-id="90e43-104">Este documento apresenta e descreve o conteúdo de Olá implementado por Olá SDK na sua aplicação.</span><span class="sxs-lookup"><span data-stu-id="90e43-104">This document lists and describes hello content deployed by hello SDK in your application.</span></span>

## <a name="hello-resources-folder"></a><span data-ttu-id="90e43-105">Olá `/Resources` pasta</span><span class="sxs-lookup"><span data-stu-id="90e43-105">hello `/Resources` folder</span></span>
<span data-ttu-id="90e43-106">Esta pasta contém todos os recursos de Olá que necessita de Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="90e43-106">This folder contains all hello resources that Mobile Engagement needs.</span></span> <span data-ttu-id="90e43-107">Também pode personalizá-las toofit a aplicação.</span><span class="sxs-lookup"><span data-stu-id="90e43-107">You can also customize them toofit your app.</span></span>

* <span data-ttu-id="90e43-108">`EngagementConfiguration.xml`: Olá o ficheiro de configuração do Mobile Engagement, isto é onde pode personalizar as definições de Mobile Engagement (cadeia de ligação do Mobile Engagement, falhas de relatório...).</span><span class="sxs-lookup"><span data-stu-id="90e43-108">`EngagementConfiguration.xml` : hello Mobile Engagement's configuration file, this is where you can customize Mobile Engagement settings (Mobile Engagement connection string, report crash...).</span></span>

### <a name="html-folder"></a><span data-ttu-id="90e43-109">pasta /HTML</span><span class="sxs-lookup"><span data-stu-id="90e43-109">/html folder</span></span>
* <span data-ttu-id="90e43-110">`EngagementNotification.html`: Olá `Notification` web estrutura de html da vista de faixas na aplicação.</span><span class="sxs-lookup"><span data-stu-id="90e43-110">`EngagementNotification.html` : hello `Notification` web view html design for in-app banners.</span></span>
* <span data-ttu-id="90e43-111">`EngagementAnnouncement.html`: Olá `Announcement` web estrutura da vista html para vistas interstitial na aplicação.</span><span class="sxs-lookup"><span data-stu-id="90e43-111">`EngagementAnnouncement.html` : hello `Announcement` web view html design for in-app interstitial views.</span></span>

### <a name="images-folder"></a><span data-ttu-id="90e43-112">pasta /Images</span><span class="sxs-lookup"><span data-stu-id="90e43-112">/images folder</span></span>
* <span data-ttu-id="90e43-113">`EngagementIconNotification.png`: ícone de marca de Olá apresentado em Olá à esquerda de uma notificação, substituir este pelo ícone de marca.</span><span class="sxs-lookup"><span data-stu-id="90e43-113">`EngagementIconNotification.png` : hello brand icon displayed at hello left of a notification, replace this one by your brand icon.</span></span>
* <span data-ttu-id="90e43-114">`EngagementIconOk.png`: Olá `Ok` ícone de páginas de conteúdo de alcance de Olá para botão de ação ou validação de Olá.</span><span class="sxs-lookup"><span data-stu-id="90e43-114">`EngagementIconOk.png` : hello `Ok` icon of hello reach content pages for hello action or validation button.</span></span>
* <span data-ttu-id="90e43-115">`EngagementIconNOK.png`: Olá `NOK` ícone utilizado quando o botão de validação de Olá das páginas de conteúdo de alcance Olá está desativado.</span><span class="sxs-lookup"><span data-stu-id="90e43-115">`EngagementIconNOK.png` : hello `NOK` icon used when hello validation button of hello reach content pages is disabled.</span></span>
* <span data-ttu-id="90e43-116">`EngagementIconClose.png`: Olá `Close` ícone de Olá alcançar notificações e conteúdo Olá dispensa botão.</span><span class="sxs-lookup"><span data-stu-id="90e43-116">`EngagementIconClose.png` : hello `Close` icon of hello reach notifications and contents for hello dismiss button.</span></span>

### <a name="overlay-folder"></a><span data-ttu-id="90e43-117">pasta /Overlay</span><span class="sxs-lookup"><span data-stu-id="90e43-117">/overlay folder</span></span>
* <span data-ttu-id="90e43-118">`EngagementPageOverlay.cs`: Olá sobreposição página responsável pela adição Olá alcance do Engagement subordinado de tooits de IU na aplicação.</span><span class="sxs-lookup"><span data-stu-id="90e43-118">`EngagementPageOverlay.cs` : hello overlay page responsible for adding hello Engagement reach in-app UI tooits child.</span></span>

