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
# <a name="how-to-send-scheduled-notifications"></a>Como: Enviar notificações agendadas
## <a name="overview"></a>Descrição geral
Se tiver um cenário no qual pretende toosend uma notificação, a determinada altura no Olá futuras mas não dispõe de uma forma fácil toowake a notificação do código de back-end toosend Olá de ativação. Hubs de notificação de escalão Standard suporta uma funcionalidade que permite-lhe tooschedule notificações dos dias too7 Olá futura.

Quando enviar uma notificação, basta utilizar Olá [ScheduledNotification](https://msdn.microsoft.com/library/microsoft.azure.notificationhubs.schedulednotification.aspx) classe no Olá SDK dos Notification Hubs, conforme mostrado no seguinte exemplo de Olá:

    Notification notification = new AppleNotification("{\"aps\":{\"alert\":\"Happy birthday!\"}}");
    var scheduled = await hub.ScheduleNotificationAsync(notification, new DateTime(2014, 7, 19, 0, 0, 0));

Além disso, pode cancelar uma notificação anteriormente agendada utilizando o respetivo notificationId:

    await hub.CancelNotificationAsync(scheduled.ScheduledNotificationId);

Não existem não existem limites no número de Olá de notificações agendadas, que pode enviar.

