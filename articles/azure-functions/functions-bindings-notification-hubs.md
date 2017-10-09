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
# <a name="azure-functions-notification-hub-output-binding"></a>Enlace de saída do Hub de notificação de funções do Azure
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

Este artigo explica como tooconfigure e código de enlaces de Hub de notificação do Azure das funções do Azure. 

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

As suas funções podem enviar notificações push através de um Hub de notificação do Azure configurada com poucas linhas de código. No entanto, Olá Notification Hub do Azure tem de ser configurado para Olá serviços de notificações de plataforma (PNS) que pretende toouse. Para obter mais informações sobre a configuração de um Hub de notificação do Azure e desenvolver um aplicações de cliente que registar tooreceive notificações, consulte [introdução aos Notification Hubs](../notification-hubs/notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) e clique em sua plataforma de cliente de destino em Olá parte superior.

notificações de Olá que enviar podem ser notificações nativas ou notificações de modelo. Notificações nativas uma plataforma de notificação específicos de destino, conforme configurado na Olá `platform` propriedade Olá vínculo de saída. Uma notificação de modelo pode ser utilizado tootarget várias plataformas.   

## <a name="notification-hub-output-binding-properties"></a>Propriedades de enlace de saída de hub de notificação
ficheiro de function.json Olá fornece Olá seguintes propriedades:

* `name`: Nome variável utilizado no código de função para mensagem de hub de notificação de saudação.
* `type`: tem de ser definido demasiado*"notificationHub"*.
* `tagExpression`: Expressões de etiqueta permitem-lhe toospecify que possível entregar notificações tooa conjunto de dispositivos que registou as notificações de tooreceive que corresponde à expressão de tag Olá.  Para obter mais informações, consulte [expressões de encaminhamento e etiqueta](../notification-hubs/notification-hubs-tags-segment-push-message.md).
* `hubName`: Nome do recurso de hub de notificação de Olá no Olá portal do Azure.
* `connection`: Esta cadeia de ligação tem de ser um **definição da aplicação** toohello de definir a cadeia de ligação *DefaultFullSharedAccessSignature* valor para o seu hub de notificação.
* `direction`: tem de ser definido demasiado*"out"*. 
* `platform`: propriedade de plataforma Olá indica plataforma de notificação de Olá os destinos de notificação. Tem de ser um dos seguintes valores de Olá:
  * Por predefinição, se a propriedade de plataforma Olá for omitida da saída de Olá enlace, as notificações de modelo podem ser utilizado tootarget qualquer plataforma configurada no Olá Notification Hub do Azure. Para obter mais informações sobre como utilizar os modelos em geral toosend cruzada notificações de plataforma com um Hub de notificação do Azure, consulte [modelos](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md).
  * `apns`: Serviço do Apple Push Notification. Para obter mais informações sobre a configuração de hub de notificação de Olá para APNS e receber a notificação de Olá numa aplicação cliente, consulte [Sending tooiOS de notificações push com Notification Hubs do Azure](../notification-hubs/notification-hubs-ios-apple-push-notification-apns-get-started.md) 
  * `adm`: [Amazon Device Messaging](https://developer.amazon.com/device-messaging). Para obter mais informações sobre configurar o hub de notificação de Olá para ADM e receber a notificação de Olá numa aplicação Kindle, consulte [introdução aos Notification Hubs para aplicações Kindle](../notification-hubs/notification-hubs-kindle-amazon-adm-push-notification.md) 
  * `gcm`: [Google Cloud Messaging](https://developers.google.com/cloud-messaging/). Firebase Cloud Messaging, que é a versão nova do Olá do GCM, também é suportada. Para obter mais informações sobre configurar o hub de notificação de Olá para GCM/FCM e receber a notificação de Olá numa aplicação cliente do Android, consulte [Sending tooAndroid de notificações push com Notification Hubs do Azure](../notification-hubs/notification-hubs-android-push-notification-google-fcm-get-started.md)
  * `wns`: [Serviços de notificação Push do Windows](https://msdn.microsoft.com/en-us/windows/uwp/controls-and-patterns/tiles-and-notifications-windows-push-notification-services--wns--overview) direcionada para plataformas Windows. Windows Phone 8.1 e posterior também é suportada pelo WNS. Para obter mais informações sobre a configuração de hub de notificação de Olá para WNS e receber a notificação de Olá numa aplicação plataforma Universal do Windows (UWP), consulte [introdução aos Notification Hubs para aplicações universais do Windows plataforma](../notification-hubs/notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md)
  * `mpns`: [Serviço de notificação Push da Microsoft](https://msdn.microsoft.com/en-us/library/windows/apps/ff402558.aspx). Esta plataforma suporta o Windows Phone 8 e plataformas do Windows Phone anteriores. Para obter mais informações sobre a configuração de hub de notificação de Olá para MPNS e receber a notificação de Olá numa aplicação Windows Phone, consulte [enviar notificações de push com os Hubs de notificação do Azure no Windows Phone](../notification-hubs/notification-hubs-windows-mobile-push-notifications-mpns.md)

Function.json de exemplo:

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

## <a name="notification-hub-connection-string-setup"></a>Configuração de cadeia de ligação de hub de notificação
enlace de saída toouse um hub de notificação, tem de configurar a cadeia de ligação de Olá para hub Olá. Isto pode ser feito no Olá *integrar* separador, selecionando o hub de notificação ou criar um novo. 

Pode também pode adicionar manualmente uma cadeia de ligação para um hub existente através da adição de uma cadeia de ligação para Olá *DefaultFullSharedAccessSignature* tooyour hub de notificação. Esta cadeia de ligação fornece o acesso de função mensagens de notificação de toosend de permissão. Olá *DefaultFullSharedAccessSignature* valor de cadeia de ligação pode ser acedido a partir Olá **chaves** botão no painel principal do Olá do seu recurso de hub de notificação no Olá portal do Azure. toomanually adicionar uma cadeia de ligação do hub, Olá utilize os seguintes passos: 

1. No Olá **aplicação de função** painel de Olá portal do Azure, clique em **as definições de aplicação de função > aceda a definições de serviço tooApp**.
2. No Olá **definições** painel, clique em **definições da aplicação**.
3. Desloque para baixo toohello **as definições de aplicação** secção e adicione uma entrada nomeada para *DefaultFullSharedAccessSignature* valor para o seu hub de notificação.
4. Referência a sua aplicação, nome da definição cadeia no Olá enlaces de saída. Semelhante demasiado**MyHubConnectionString** utilizadas no exemplo Olá acima.

## <a name="apns-native-notifications-with-c-queue-triggers"></a>Notificações nativas do APNS com os acionadores de filas c#
Este exemplo mostra como os tipos de toouse definidos em Olá [biblioteca de Hubs de notificação do Microsoft Azure](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) toosend uma notificação de APNS nativa. 

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

## <a name="gcm-native-notifications-with-c-queue-triggers"></a>Notificações nativas do GCM com os acionadores de filas c#
Este exemplo mostra como os tipos de toouse definidos em Olá [biblioteca de Hubs de notificação do Microsoft Azure](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) toosend uma notificação de GCM nativa. 

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

## <a name="wns-native-notifications-with-c-queue-triggers"></a>Notificações nativas do WNS com os acionadores de filas c#
Este exemplo mostra como os tipos de toouse definidos em Olá [biblioteca de Hubs de notificação do Microsoft Azure](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) toosend um WNS nativo alerta notificação. 

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

## <a name="template-example-for-nodejs-timer-triggers"></a>Exemplo de modelo para acionadores de temporizador do Node.js
Neste exemplo envia uma notificação um [registo modelo](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) que contenha `location` e `message`.

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

## <a name="template-example-for-f-timer-triggers"></a>Exemplo de modelo para o F # temporizador acionadores
Neste exemplo envia uma notificação um [registo modelo](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) que contenha `location` e `message`.

```fsharp
let Run(myTimer: TimerInfo, notification: byref<IDictionary<string, string>>) =
    notification = dict [("location", "Redmond"); ("message", "Hello from F#!")]
```

## <a name="template-example-using-an-out-parameter"></a>Exemplo de modelo com um parâmetro de saída
Neste exemplo envia uma notificação um [registo modelo](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) que contenha um `message` marcador de posição no modelo de Olá.

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

## <a name="template-example-with-asynchronous-function"></a>Exemplo de modelo com função assíncrona
Se estiver a utilizar código assíncrono, parâmetros de saída não são permitidas. Neste caso, utilize `IAsyncCollector` tooreturn sua notificação de modelo. Olá código seguinte é um exemplo de código Olá acima assíncrono. 

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

## <a name="template-example-using-json"></a>Utilizar o JSON de exemplo de modelo
Neste exemplo envia uma notificação um [registo modelo](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) que contenha um `message` marcador de posição no modelo de Olá utilização de uma cadeia JSON válida.

```cs
using System;

public static void Run(string myQueueItem,  out string notification, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");
    notification = "{\"message\":\"Hello from C#. Processed a queue item!\"}";
}
```

## <a name="template-example-using-notification-hubs-library-types"></a>Exemplo de modelo através de tipos de biblioteca de Hubs de notificação
Este exemplo mostra como os tipos de toouse definidos em Olá [biblioteca de Hubs de notificação do Microsoft Azure](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/). 

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

## <a name="next-steps"></a>Passos seguintes
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

