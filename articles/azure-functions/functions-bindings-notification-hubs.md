---
title: "enlace de Hub de notificação de funções aaaAzure | Microsoft Docs"
description: "Compreender como enlace de Hub de notificação do Azure toouse das funções do Azure."
services: functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
keywords: "das funções do Azure, funções, processamento de eventos, computação dinâmica, arquitetura sem servidor"
ms.assetid: 0ff0c949-20bf-430b-8dd5-d72b7b6ee6f7
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 10/27/2016
ms.author: glenga
ms.openlocfilehash: d192424a8ec701d02f8bcb4aa4c1d189b20537a5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-notification-hub-output-binding"></a><span data-ttu-id="e8476-104">Enlace de saída do Hub de notificação de funções do Azure</span><span class="sxs-lookup"><span data-stu-id="e8476-104">Azure Functions Notification Hub output binding</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="e8476-105">Este artigo explica como tooconfigure e código de enlaces de Hub de notificação do Azure das funções do Azure.</span><span class="sxs-lookup"><span data-stu-id="e8476-105">This article explains how tooconfigure and code Azure Notification Hub bindings in Azure Functions.</span></span> 

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<span data-ttu-id="e8476-106">As suas funções podem enviar notificações push através de um Hub de notificação do Azure configurada com poucas linhas de código.</span><span class="sxs-lookup"><span data-stu-id="e8476-106">Your functions can send push notifications using a configured Azure Notification Hub with a few lines of code.</span></span> <span data-ttu-id="e8476-107">No entanto, Olá Notification Hub do Azure tem de ser configurado para Olá serviços de notificações de plataforma (PNS) que pretende toouse.</span><span class="sxs-lookup"><span data-stu-id="e8476-107">However, hello Azure Notification Hub must be configured for hello Platform Notifications Services (PNS) you want toouse.</span></span> <span data-ttu-id="e8476-108">Para obter mais informações sobre a configuração de um Hub de notificação do Azure e desenvolver um aplicações de cliente que registar tooreceive notificações, consulte [introdução aos Notification Hubs](../notification-hubs/notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) e clique em sua plataforma de cliente de destino em Olá parte superior.</span><span class="sxs-lookup"><span data-stu-id="e8476-108">For more information on configuring an Azure Notification Hub and developing a client applications that register tooreceive notifications, see [Getting started with Notification Hubs](../notification-hubs/notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) and click your target client platform at hello top.</span></span>

<span data-ttu-id="e8476-109">notificações de Olá que enviar podem ser notificações nativas ou notificações de modelo.</span><span class="sxs-lookup"><span data-stu-id="e8476-109">hello notifications you send can be native notifications or template notifications.</span></span> <span data-ttu-id="e8476-110">Notificações nativas uma plataforma de notificação específicos de destino, conforme configurado na Olá `platform` propriedade Olá vínculo de saída.</span><span class="sxs-lookup"><span data-stu-id="e8476-110">Native notifications target a specific notification platform as configured in hello `platform` property of hello output binding.</span></span> <span data-ttu-id="e8476-111">Uma notificação de modelo pode ser utilizado tootarget várias plataformas.</span><span class="sxs-lookup"><span data-stu-id="e8476-111">A template notification can be used tootarget multiple platforms.</span></span>   

## <a name="notification-hub-output-binding-properties"></a><span data-ttu-id="e8476-112">Propriedades de enlace de saída de hub de notificação</span><span class="sxs-lookup"><span data-stu-id="e8476-112">Notification hub output binding properties</span></span>
<span data-ttu-id="e8476-113">ficheiro de function.json Olá fornece Olá seguintes propriedades:</span><span class="sxs-lookup"><span data-stu-id="e8476-113">hello function.json file provides hello following properties:</span></span>

* <span data-ttu-id="e8476-114">`name`: Nome variável utilizado no código de função para mensagem de hub de notificação de saudação.</span><span class="sxs-lookup"><span data-stu-id="e8476-114">`name` : Variable name used in function code for hello notification hub message.</span></span>
* <span data-ttu-id="e8476-115">`type`: tem de ser definido demasiado*"notificationHub"*.</span><span class="sxs-lookup"><span data-stu-id="e8476-115">`type` : must be set too*"notificationHub"*.</span></span>
* <span data-ttu-id="e8476-116">`tagExpression`: Expressões de etiqueta permitem-lhe toospecify que possível entregar notificações tooa conjunto de dispositivos que registou as notificações de tooreceive que corresponde à expressão de tag Olá.</span><span class="sxs-lookup"><span data-stu-id="e8476-116">`tagExpression` : Tag expressions allow you toospecify that notifications be delivered tooa set of devices who have registered tooreceive notifications that match hello tag expression.</span></span>  <span data-ttu-id="e8476-117">Para obter mais informações, consulte [expressões de encaminhamento e etiqueta](../notification-hubs/notification-hubs-tags-segment-push-message.md).</span><span class="sxs-lookup"><span data-stu-id="e8476-117">For more information, see [Routing and tag expressions](../notification-hubs/notification-hubs-tags-segment-push-message.md).</span></span>
* <span data-ttu-id="e8476-118">`hubName`: Nome do recurso de hub de notificação de Olá no Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="e8476-118">`hubName` : Name of hello notification hub resource in hello Azure portal.</span></span>
* <span data-ttu-id="e8476-119">`connection`: Esta cadeia de ligação tem de ser um **definição da aplicação** toohello de definir a cadeia de ligação *DefaultFullSharedAccessSignature* valor para o seu hub de notificação.</span><span class="sxs-lookup"><span data-stu-id="e8476-119">`connection` : This connection string must be an **Application Setting** connection string set toohello *DefaultFullSharedAccessSignature* value for your notification hub.</span></span>
* <span data-ttu-id="e8476-120">`direction`: tem de ser definido demasiado*"out"*.</span><span class="sxs-lookup"><span data-stu-id="e8476-120">`direction` : must be set too*"out"*.</span></span> 
* <span data-ttu-id="e8476-121">`platform`: propriedade de plataforma Olá indica plataforma de notificação de Olá os destinos de notificação.</span><span class="sxs-lookup"><span data-stu-id="e8476-121">`platform` : hello platform property indicates hello notification platform your notification targets.</span></span> <span data-ttu-id="e8476-122">Tem de ser um dos seguintes valores de Olá:</span><span class="sxs-lookup"><span data-stu-id="e8476-122">Must be one of hello following values:</span></span>
  * <span data-ttu-id="e8476-123">Por predefinição, se a propriedade de plataforma Olá for omitida da saída de Olá enlace, as notificações de modelo podem ser utilizado tootarget qualquer plataforma configurada no Olá Notification Hub do Azure.</span><span class="sxs-lookup"><span data-stu-id="e8476-123">By default, if hello platform property is omitted from hello output binding, template notifications can be used tootarget any platform configured on hello Azure Notification Hub.</span></span> <span data-ttu-id="e8476-124">Para obter mais informações sobre como utilizar os modelos em geral toosend cruzada notificações de plataforma com um Hub de notificação do Azure, consulte [modelos](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md).</span><span class="sxs-lookup"><span data-stu-id="e8476-124">For more information on using templates in general toosend cross platform notifications with an Azure Notification Hub, see [Templates](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md).</span></span>
  * <span data-ttu-id="e8476-125">`apns`: Serviço do Apple Push Notification.</span><span class="sxs-lookup"><span data-stu-id="e8476-125">`apns` : Apple Push Notification Service.</span></span> <span data-ttu-id="e8476-126">Para obter mais informações sobre a configuração de hub de notificação de Olá para APNS e receber a notificação de Olá numa aplicação cliente, consulte [Sending tooiOS de notificações push com Notification Hubs do Azure](../notification-hubs/notification-hubs-ios-apple-push-notification-apns-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="e8476-126">For more information on configuring hello notification hub for APNS and receiving hello notification in a client app, see [Sending push notifications tooiOS with Azure Notification Hubs](../notification-hubs/notification-hubs-ios-apple-push-notification-apns-get-started.md)</span></span> 
  * <span data-ttu-id="e8476-127">`adm`: [Amazon Device Messaging](https://developer.amazon.com/device-messaging).</span><span class="sxs-lookup"><span data-stu-id="e8476-127">`adm` : [Amazon Device Messaging](https://developer.amazon.com/device-messaging).</span></span> <span data-ttu-id="e8476-128">Para obter mais informações sobre configurar o hub de notificação de Olá para ADM e receber a notificação de Olá numa aplicação Kindle, consulte [introdução aos Notification Hubs para aplicações Kindle](../notification-hubs/notification-hubs-kindle-amazon-adm-push-notification.md)</span><span class="sxs-lookup"><span data-stu-id="e8476-128">For more information on configuring hello notification hub for ADM and receiving hello notification in a Kindle app, see [Getting Started with Notification Hubs for Kindle apps](../notification-hubs/notification-hubs-kindle-amazon-adm-push-notification.md)</span></span> 
  * <span data-ttu-id="e8476-129">`gcm`: [Google Cloud Messaging](https://developers.google.com/cloud-messaging/).</span><span class="sxs-lookup"><span data-stu-id="e8476-129">`gcm` : [Google Cloud Messaging](https://developers.google.com/cloud-messaging/).</span></span> <span data-ttu-id="e8476-130">Firebase Cloud Messaging, que é a versão nova do Olá do GCM, também é suportada.</span><span class="sxs-lookup"><span data-stu-id="e8476-130">Firebase Cloud Messaging, which is hello new version of GCM, is also supported.</span></span> <span data-ttu-id="e8476-131">Para obter mais informações sobre configurar o hub de notificação de Olá para GCM/FCM e receber a notificação de Olá numa aplicação cliente do Android, consulte [Sending tooAndroid de notificações push com Notification Hubs do Azure](../notification-hubs/notification-hubs-android-push-notification-google-fcm-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="e8476-131">For more information on configuring hello notification hub for GCM/FCM and receiving hello notification in an Android client app, see [Sending push notifications tooAndroid with Azure Notification Hubs](../notification-hubs/notification-hubs-android-push-notification-google-fcm-get-started.md)</span></span>
  * <span data-ttu-id="e8476-132">`wns`: [Serviços de notificação Push do Windows](https://msdn.microsoft.com/en-us/windows/uwp/controls-and-patterns/tiles-and-notifications-windows-push-notification-services--wns--overview) direcionada para plataformas Windows.</span><span class="sxs-lookup"><span data-stu-id="e8476-132">`wns` : [Windows Push Notification Services](https://msdn.microsoft.com/en-us/windows/uwp/controls-and-patterns/tiles-and-notifications-windows-push-notification-services--wns--overview) targeting Windows platforms.</span></span> <span data-ttu-id="e8476-133">Windows Phone 8.1 e posterior também é suportada pelo WNS.</span><span class="sxs-lookup"><span data-stu-id="e8476-133">Windows Phone 8.1 and later is also supported by WNS.</span></span> <span data-ttu-id="e8476-134">Para obter mais informações sobre a configuração de hub de notificação de Olá para WNS e receber a notificação de Olá numa aplicação plataforma Universal do Windows (UWP), consulte [introdução aos Notification Hubs para aplicações universais do Windows plataforma](../notification-hubs/notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md)</span><span class="sxs-lookup"><span data-stu-id="e8476-134">For more information on configuring hello notification hub for WNS and receiving hello notification in a Universal Windows Platform (UWP) app, see [Getting started with Notification Hubs for Windows Universal Platform Apps](../notification-hubs/notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md)</span></span>
  * <span data-ttu-id="e8476-135">`mpns`: [Serviço de notificação Push da Microsoft](https://msdn.microsoft.com/en-us/library/windows/apps/ff402558.aspx).</span><span class="sxs-lookup"><span data-stu-id="e8476-135">`mpns` : [Microsoft Push Notification Service](https://msdn.microsoft.com/en-us/library/windows/apps/ff402558.aspx).</span></span> <span data-ttu-id="e8476-136">Esta plataforma suporta o Windows Phone 8 e plataformas do Windows Phone anteriores.</span><span class="sxs-lookup"><span data-stu-id="e8476-136">This platform supports Windows Phone 8 and earlier Windows Phone platforms.</span></span> <span data-ttu-id="e8476-137">Para obter mais informações sobre a configuração de hub de notificação de Olá para MPNS e receber a notificação de Olá numa aplicação Windows Phone, consulte [enviar notificações de push com os Hubs de notificação do Azure no Windows Phone](../notification-hubs/notification-hubs-windows-mobile-push-notifications-mpns.md)</span><span class="sxs-lookup"><span data-stu-id="e8476-137">For more information on configuring hello notification hub for MPNS and receiving hello notification in a Windows Phone app, see [Sending push notifications with Azure Notification Hubs on Windows Phone](../notification-hubs/notification-hubs-windows-mobile-push-notifications-mpns.md)</span></span>

<span data-ttu-id="e8476-138">Function.json de exemplo:</span><span class="sxs-lookup"><span data-stu-id="e8476-138">Example function.json:</span></span>

```json
{
  "bindings": [
    {
      "name": "notification",
      "type": "notificationHub",
      "tagExpression": "",
      "hubName": "my-notification-hub",
      "connection": "MyHubConnectionString",
      "platform": "gcm",
      "direction": "out"
    }
  ],
  "disabled": false
}
```

## <a name="notification-hub-connection-string-setup"></a><span data-ttu-id="e8476-139">Configuração de cadeia de ligação de hub de notificação</span><span class="sxs-lookup"><span data-stu-id="e8476-139">Notification hub connection string setup</span></span>
<span data-ttu-id="e8476-140">enlace de saída toouse um hub de notificação, tem de configurar a cadeia de ligação de Olá para hub Olá.</span><span class="sxs-lookup"><span data-stu-id="e8476-140">toouse a Notification hub output binding, you must configure hello connection string for hello hub.</span></span> <span data-ttu-id="e8476-141">Isto pode ser feito no Olá *integrar* separador, selecionando o hub de notificação ou criar um novo.</span><span class="sxs-lookup"><span data-stu-id="e8476-141">This can be done on hello *Integrate* tab by selecting your notification hub or creating a new one.</span></span> 

<span data-ttu-id="e8476-142">Pode também pode adicionar manualmente uma cadeia de ligação para um hub existente através da adição de uma cadeia de ligação para Olá *DefaultFullSharedAccessSignature* tooyour hub de notificação.</span><span class="sxs-lookup"><span data-stu-id="e8476-142">You can also manually add a connection string for an existing hub by adding a connection string for hello *DefaultFullSharedAccessSignature* tooyour notification hub.</span></span> <span data-ttu-id="e8476-143">Esta cadeia de ligação fornece o acesso de função mensagens de notificação de toosend de permissão.</span><span class="sxs-lookup"><span data-stu-id="e8476-143">This connection string provides your function access permission toosend notification messages.</span></span> <span data-ttu-id="e8476-144">Olá *DefaultFullSharedAccessSignature* valor de cadeia de ligação pode ser acedido a partir Olá **chaves** botão no painel principal do Olá do seu recurso de hub de notificação no Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="e8476-144">hello *DefaultFullSharedAccessSignature* connection string value can be accessed from hello **keys** button in hello main blade of your notification hub resource in hello Azure portal.</span></span> <span data-ttu-id="e8476-145">toomanually adicionar uma cadeia de ligação do hub, Olá utilize os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="e8476-145">toomanually add a connection string for your hub, use hello following steps:</span></span> 

1. <span data-ttu-id="e8476-146">No Olá **aplicação de função** painel de Olá portal do Azure, clique em **as definições de aplicação de função > aceda a definições de serviço tooApp**.</span><span class="sxs-lookup"><span data-stu-id="e8476-146">On hello **Function app** blade of hello Azure portal, click **Function App Settings > Go tooApp Service settings**.</span></span>
2. <span data-ttu-id="e8476-147">No Olá **definições** painel, clique em **definições da aplicação**.</span><span class="sxs-lookup"><span data-stu-id="e8476-147">In hello **Settings** blade, click **Application Settings**.</span></span>
3. <span data-ttu-id="e8476-148">Desloque para baixo toohello **as definições de aplicação** secção e adicione uma entrada nomeada para *DefaultFullSharedAccessSignature* valor para o seu hub de notificação.</span><span class="sxs-lookup"><span data-stu-id="e8476-148">Scroll down toohello **App settings** section, and add a named entry for *DefaultFullSharedAccessSignature* value for your notification hub.</span></span>
4. <span data-ttu-id="e8476-149">Referência a sua aplicação, nome da definição cadeia no Olá enlaces de saída.</span><span class="sxs-lookup"><span data-stu-id="e8476-149">Reference your App setting string name in hello output bindings.</span></span> <span data-ttu-id="e8476-150">Semelhante demasiado**MyHubConnectionString** utilizadas no exemplo Olá acima.</span><span class="sxs-lookup"><span data-stu-id="e8476-150">Similar too**MyHubConnectionString** used in hello example above.</span></span>

## <a name="apns-native-notifications-with-c-queue-triggers"></a><span data-ttu-id="e8476-151">Notificações nativas do APNS com os acionadores de filas c#</span><span class="sxs-lookup"><span data-stu-id="e8476-151">APNS native notifications with C# queue triggers</span></span>
<span data-ttu-id="e8476-152">Este exemplo mostra como os tipos de toouse definidos em Olá [biblioteca de Hubs de notificação do Microsoft Azure](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) toosend uma notificação de APNS nativa.</span><span class="sxs-lookup"><span data-stu-id="e8476-152">This example shows how toouse types defined in hello [Microsoft Azure Notification Hubs Library](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) toosend a native APNS notification.</span></span> 

```cs
#r "Microsoft.Azure.NotificationHubs"
#r "Newtonsoft.Json"

using System;
using Microsoft.Azure.NotificationHubs;
using Newtonsoft.Json;

public static async Task Run(string myQueueItem, IAsyncCollector<Notification> notification, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");

    // In this example hello queue item is a new user toobe processed in hello form of a JSON string with 
    // a "name" value.
    //
    // hello JSON format for a native APNS notification is ...
    // { "aps": { "alert": "notification message" }}  

    log.Info($"Sending APNS notification of a new user");    
    dynamic user = JsonConvert.DeserializeObject(myQueueItem);    
    string apnsNotificationPayload = "{\"aps\": {\"alert\": \"A new user wants toobe added (" + 
                                        user.name + ")\" }}";
    log.Info($"{apnsNotificationPayload}");
    await notification.AddAsync(new AppleNotification(apnsNotificationPayload));        
}
```

## <a name="gcm-native-notifications-with-c-queue-triggers"></a><span data-ttu-id="e8476-153">Notificações nativas do GCM com os acionadores de filas c#</span><span class="sxs-lookup"><span data-stu-id="e8476-153">GCM native notifications with C# queue triggers</span></span>
<span data-ttu-id="e8476-154">Este exemplo mostra como os tipos de toouse definidos em Olá [biblioteca de Hubs de notificação do Microsoft Azure](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) toosend uma notificação de GCM nativa.</span><span class="sxs-lookup"><span data-stu-id="e8476-154">This example shows how toouse types defined in hello [Microsoft Azure Notification Hubs Library](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) toosend a native GCM notification.</span></span> 

```cs
#r "Microsoft.Azure.NotificationHubs"
#r "Newtonsoft.Json"

using System;
using Microsoft.Azure.NotificationHubs;
using Newtonsoft.Json;

public static async Task Run(string myQueueItem, IAsyncCollector<Notification> notification, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");

    // In this example hello queue item is a new user toobe processed in hello form of a JSON string with 
    // a "name" value.
    //
    // hello JSON format for a native GCM notification is ...
    // { "data": { "message": "notification message" }}  

    log.Info($"Sending GCM notification of a new user");    
    dynamic user = JsonConvert.DeserializeObject(myQueueItem);    
    string gcmNotificationPayload = "{\"data\": {\"message\": \"A new user wants toobe added (" + 
                                        user.name + ")\" }}";
    log.Info($"{gcmNotificationPayload}");
    await notification.AddAsync(new GcmNotification(gcmNotificationPayload));        
}
```

## <a name="wns-native-notifications-with-c-queue-triggers"></a><span data-ttu-id="e8476-155">Notificações nativas do WNS com os acionadores de filas c#</span><span class="sxs-lookup"><span data-stu-id="e8476-155">WNS native notifications with C# queue triggers</span></span>
<span data-ttu-id="e8476-156">Este exemplo mostra como os tipos de toouse definidos em Olá [biblioteca de Hubs de notificação do Microsoft Azure](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) toosend um WNS nativo alerta notificação.</span><span class="sxs-lookup"><span data-stu-id="e8476-156">This example shows how toouse types defined in hello [Microsoft Azure Notification Hubs Library](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) toosend a native WNS toast notification.</span></span> 

```cs
#r "Microsoft.Azure.NotificationHubs"
#r "Newtonsoft.Json"

using System;
using Microsoft.Azure.NotificationHubs;
using Newtonsoft.Json;

public static async Task Run(string myQueueItem, IAsyncCollector<Notification> notification, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");

    // In this example hello queue item is a new user toobe processed in hello form of a JSON string with 
    // a "name" value.
    //
    // hello XML format for a native WNS toast notification is ...
    // <?xml version="1.0" encoding="utf-8"?>
    // <toast>
    //      <visual>
    //     <binding template="ToastText01">
    //       <text id="1">notification message</text>
    //     </binding>
    //   </visual>
    // </toast>

    log.Info($"Sending WNS toast notification of a new user");    
    dynamic user = JsonConvert.DeserializeObject(myQueueItem);    
    string wnsNotificationPayload = "<?xml version=\"1.0\" encoding=\"utf-8\"?>" +
                                    "<toast><visual><binding template=\"ToastText01\">" +
                                        "<text id=\"1\">" + 
                                            "A new user wants toobe added (" + user.name + ")" + 
                                        "</text>" +
                                    "</binding></visual></toast>";

    log.Info($"{wnsNotificationPayload}");
    await notification.AddAsync(new WindowsNotification(wnsNotificationPayload));        
}
```

## <a name="template-example-for-nodejs-timer-triggers"></a><span data-ttu-id="e8476-157">Exemplo de modelo para acionadores de temporizador do Node.js</span><span class="sxs-lookup"><span data-stu-id="e8476-157">Template example for Node.js timer triggers</span></span>
<span data-ttu-id="e8476-158">Neste exemplo envia uma notificação um [registo modelo](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) que contenha `location` e `message`.</span><span class="sxs-lookup"><span data-stu-id="e8476-158">This example sends a notification for a [template registration](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) that contains `location` and `message`.</span></span>

```javascript
module.exports = function (context, myTimer) {
    var timeStamp = new Date().toISOString();

    if(myTimer.isPastDue)
    {
        context.log('Node.js is running late!');
    }
    context.log('Node.js timer trigger function ran!', timeStamp);  
    context.bindings.notification = {
        location: "Redmond",
        message: "Hello from Node!"
    };
    context.done();
};
```

## <a name="template-example-for-f-timer-triggers"></a><span data-ttu-id="e8476-159">Exemplo de modelo para o F # temporizador acionadores</span><span class="sxs-lookup"><span data-stu-id="e8476-159">Template example for F# timer triggers</span></span>
<span data-ttu-id="e8476-160">Neste exemplo envia uma notificação um [registo modelo](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) que contenha `location` e `message`.</span><span class="sxs-lookup"><span data-stu-id="e8476-160">This example sends a notification for a [template registration](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) that contains `location` and `message`.</span></span>

```fsharp
let Run(myTimer: TimerInfo, notification: byref<IDictionary<string, string>>) =
    notification = dict [("location", "Redmond"); ("message", "Hello from F#!")]
```

## <a name="template-example-using-an-out-parameter"></a><span data-ttu-id="e8476-161">Exemplo de modelo com um parâmetro de saída</span><span class="sxs-lookup"><span data-stu-id="e8476-161">Template example using an out parameter</span></span>
<span data-ttu-id="e8476-162">Neste exemplo envia uma notificação um [registo modelo](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) que contenha um `message` marcador de posição no modelo de Olá.</span><span class="sxs-lookup"><span data-stu-id="e8476-162">This example sends a notification for a [template registration](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) that contains a `message` place holder in hello template.</span></span>

```cs
using System;
using System.Threading.Tasks;
using System.Collections.Generic;

public static void Run(string myQueueItem,  out IDictionary<string, string> notification, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");
    notification = GetTemplateProperties(myQueueItem);
}

private static IDictionary<string, string> GetTemplateProperties(string message)
{
    Dictionary<string, string> templateProperties = new Dictionary<string, string>();
    templateProperties["message"] = message;
    return templateProperties;
}
```

## <a name="template-example-with-asynchronous-function"></a><span data-ttu-id="e8476-163">Exemplo de modelo com função assíncrona</span><span class="sxs-lookup"><span data-stu-id="e8476-163">Template example with asynchronous function</span></span>
<span data-ttu-id="e8476-164">Se estiver a utilizar código assíncrono, parâmetros de saída não são permitidas.</span><span class="sxs-lookup"><span data-stu-id="e8476-164">If you are using asynchronous code, out parameters are not allowed.</span></span> <span data-ttu-id="e8476-165">Neste caso, utilize `IAsyncCollector` tooreturn sua notificação de modelo.</span><span class="sxs-lookup"><span data-stu-id="e8476-165">In this case use `IAsyncCollector` tooreturn your template notification.</span></span> <span data-ttu-id="e8476-166">Olá código seguinte é um exemplo de código Olá acima assíncrono.</span><span class="sxs-lookup"><span data-stu-id="e8476-166">hello following code is an asynchronous example of hello code above.</span></span> 

```cs
using System;
using System.Threading.Tasks;
using System.Collections.Generic;

public static async Task Run(string myQueueItem, IAsyncCollector<IDictionary<string,string>> notification, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");

    log.Info($"Sending Template Notification tooNotification Hub");
    await notification.AddAsync(GetTemplateProperties(myQueueItem));    
}

private static IDictionary<string, string> GetTemplateProperties(string message)
{
    Dictionary<string, string> templateProperties = new Dictionary<string, string>();
    templateProperties["user"] = "A new user wants toobe added : " + message;
    return templateProperties;
}
```

## <a name="template-example-using-json"></a><span data-ttu-id="e8476-167">Utilizar o JSON de exemplo de modelo</span><span class="sxs-lookup"><span data-stu-id="e8476-167">Template example using JSON</span></span>
<span data-ttu-id="e8476-168">Neste exemplo envia uma notificação um [registo modelo](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) que contenha um `message` marcador de posição no modelo de Olá utilização de uma cadeia JSON válida.</span><span class="sxs-lookup"><span data-stu-id="e8476-168">This example sends a notification for a [template registration](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) that contains a `message` place holder in hello template using a valid JSON string.</span></span>

```cs
using System;

public static void Run(string myQueueItem,  out string notification, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");
    notification = "{\"message\":\"Hello from C#. Processed a queue item!\"}";
}
```

## <a name="template-example-using-notification-hubs-library-types"></a><span data-ttu-id="e8476-169">Exemplo de modelo através de tipos de biblioteca de Hubs de notificação</span><span class="sxs-lookup"><span data-stu-id="e8476-169">Template example using Notification Hubs library types</span></span>
<span data-ttu-id="e8476-170">Este exemplo mostra como os tipos de toouse definidos em Olá [biblioteca de Hubs de notificação do Microsoft Azure](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span><span class="sxs-lookup"><span data-stu-id="e8476-170">This example shows how toouse types defined in hello [Microsoft Azure Notification Hubs Library](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span></span> 

```cs
#r "Microsoft.Azure.NotificationHubs"

using System;
using System.Threading.Tasks;
using Microsoft.Azure.NotificationHubs;

public static void Run(string myQueueItem,  out Notification notification, TraceWriter log)
{
   log.Info($"C# Queue trigger function processed: {myQueueItem}");
   notification = GetTemplateNotification(myQueueItem);
}

private static TemplateNotification GetTemplateNotification(string message)
{
    Dictionary<string, string> templateProperties = new Dictionary<string, string>();
    templateProperties["message"] = message;
    return new TemplateNotification(templateProperties);
}
```

## <a name="next-steps"></a><span data-ttu-id="e8476-171">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="e8476-171">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

