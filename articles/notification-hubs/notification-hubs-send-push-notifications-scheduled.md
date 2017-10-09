---
title: "aaaHow toosend agendada notificações | Microsoft Docs"
description: "Este tópico descreve a utilizar notificações agendada com Notification Hubs do Azure."
services: notification-hubs
documentationcenter: .net
keywords: "notificações push, notificação push, notificações push de agendamento"
author: ysxu
manager: erikre
editor: 
ms.assetid: 6b718c75-75dd-4c99-aee3-db1288235c1a
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: dotnet
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: 9b3ba715dad6f5d824a615e83f2863b0db47b533
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-to-send-scheduled-notifications"></a><span data-ttu-id="05aad-104">Como: Enviar notificações agendadas</span><span class="sxs-lookup"><span data-stu-id="05aad-104">How To: Send scheduled notifications</span></span>
## <a name="overview"></a><span data-ttu-id="05aad-105">Descrição geral</span><span class="sxs-lookup"><span data-stu-id="05aad-105">Overview</span></span>
<span data-ttu-id="05aad-106">Se tiver um cenário no qual pretende toosend uma notificação, a determinada altura no Olá futuras mas não dispõe de uma forma fácil toowake a notificação do código de back-end toosend Olá de ativação.</span><span class="sxs-lookup"><span data-stu-id="05aad-106">If you have a scenario in which you want toosend a notification at some point in hello future, but do not have an easy way toowake up your back-end code toosend hello notification.</span></span> <span data-ttu-id="05aad-107">Hubs de notificação de escalão Standard suporta uma funcionalidade que permite-lhe tooschedule notificações dos dias too7 Olá futura.</span><span class="sxs-lookup"><span data-stu-id="05aad-107">Standard tier Notification Hubs supports a feature that enables you tooschedule notifications up too7 days in hello future.</span></span>

<span data-ttu-id="05aad-108">Quando enviar uma notificação, basta utilizar Olá [ScheduledNotification](https://msdn.microsoft.com/library/microsoft.azure.notificationhubs.schedulednotification.aspx) classe no Olá SDK dos Notification Hubs, conforme mostrado no seguinte exemplo de Olá:</span><span class="sxs-lookup"><span data-stu-id="05aad-108">When sending a notification, simply use hello [ScheduledNotification](https://msdn.microsoft.com/library/microsoft.azure.notificationhubs.schedulednotification.aspx) class in hello Notification Hubs SDK as shown in hello following example:</span></span>

    Notification notification = new AppleNotification("{\"aps\":{\"alert\":\"Happy birthday!\"}}");
    var scheduled = await hub.ScheduleNotificationAsync(notification, new DateTime(2014, 7, 19, 0, 0, 0));

<span data-ttu-id="05aad-109">Além disso, pode cancelar uma notificação anteriormente agendada utilizando o respetivo notificationId:</span><span class="sxs-lookup"><span data-stu-id="05aad-109">Also, you can cancel a previously scheduled notification using its notificationId:</span></span>

    await hub.CancelNotificationAsync(scheduled.ScheduledNotificationId);

<span data-ttu-id="05aad-110">Não existem não existem limites no número de Olá de notificações agendadas, que pode enviar.</span><span class="sxs-lookup"><span data-stu-id="05aad-110">There are no limits on hello number of scheduled notifications you can send.</span></span>

