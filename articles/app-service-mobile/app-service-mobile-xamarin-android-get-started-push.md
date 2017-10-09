---
title: "aplicação de xamarin. Android de tooyour de notificações push aaaAdd | Microsoft Docs"
description: "Saiba como toouse App Service do Azure e Notification Hubs do Azure toosend aplicação de xamarin. Android tooyour de notificações push"
services: app-service\mobile
documentationcenter: xamarin
author: ysxu
manager: syntaxc4
editor: 
ms.assetid: 6f7e8517-e532-4559-9b07-874115f4c65b
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-android
ms.devlang: dotnet
ms.topic: article
ms.date: 10/12/2016
ms.author: yuaxu
ms.openlocfilehash: c93d1d0cae06ab15e3e3e5c4b342808b2cd49113
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="add-push-notifications-tooyour-xamarinandroid-app"></a>Adicionar a aplicação de xamarin. Android de tooyour de notificações push
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a>Descrição geral
Neste tutorial, adicionar toohello de notificações push [início rápido do xamarin. Android](app-service-mobile-windows-store-dotnet-get-started.md) projeto para que uma notificação push é enviada toohello dispositivo sempre que é inserido um registo.

Se não utilizar Olá transferir o projeto de servidor de início rápido, será necessário Olá pacote de extensão de notificação push. Consulte [trabalhar com o servidor de back-end de .NET Olá SDK de Mobile Apps do Azure](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) para obter mais informações.

## <a name="prerequisites"></a>Pré-requisitos
Este tutorial requer o seguinte Olá:

* Uma conta Google ativa. Pode inscrever-se para uma conta do Google na [accounts.google.com](http://go.microsoft.com/fwlink/p/?LinkId=268302).
* [Google Cloud Messaging o componente de cliente](http://components.xamarin.com/view/GCMClient/).

## <a name="configure-hub"></a>Configurar um Hub de notificação
[!INCLUDE [app-service-mobile-configure-notification-hub](../../includes/app-service-mobile-configure-notification-hub.md)]

## <a id="register"></a>Ativar o Firebase Cloud Messaging
[!INCLUDE [notification-hubs-enable-firebase-cloud-messaging](../../includes/notification-hubs-enable-firebase-cloud-messaging.md)]

## <a name="configure-azure-toosend-push-requests"></a>Configurar os pedidos de push toosend do Azure
[!INCLUDE [app-service-mobile-android-configure-push](../../includes/app-service-mobile-android-configure-push-for-firebase.md)]

## <a id="update-server"></a>Atualizar notificações de push Olá servidor projeto toosend
[!INCLUDE [app-service-mobile-update-server-project-for-push-template](../../includes/app-service-mobile-update-server-project-for-push-template.md)]

## <a id="configure-app"></a>Configurar o projeto de cliente Olá para notificações push
[!INCLUDE [mobile-services-xamarin-android-push-configure-project](../../includes/mobile-services-xamarin-android-push-configure-project.md)]

## <a id="add-push"></a>Adicionar a aplicação de tooyour de código de notificações push
[!INCLUDE [app-service-mobile-xamarin-android-push-add-to-app](../../includes/app-service-mobile-xamarin-android-push-add-to-app.md)]

## <a name="test"></a>Notificações de push de teste na sua aplicação
Pode testar a aplicação Olá através da utilização de um dispositivo virtual no emulador Olá. Existem passos de configuração adicionais necessários quando em execução num emulador.

1. Certifique-se de que está a implementar tooor depuração num dispositivo virtual que tenha as APIs da Google definir como destino de Olá, conforme mostrado abaixo no Gestor do Olá dispositivo Virtual Android (AVD).
   
    ![](./media/app-service-mobile-xamarin-android-get-started-push/google-apis-avd-settings.png)
2. Adicionar um dispositivo Android do Google conta toohello clicando **aplicações** > **definições** > **adicionar conta**, em seguida, siga as instruções de Olá.
   
    ![](./media/app-service-mobile-xamarin-android-get-started-push/add-google-account.png)
3. Executar a aplicação de todolist Olá como antes e inserir um novo item de todo. Este tempo, um ícone de notificação é apresentado na área de notificação de Olá. Pode abrir Olá notificação gaveta tooview Olá texto completo de notificação de Olá.
   
    ![](./media/app-service-mobile-xamarin-android-get-started-push/android-notifications.png)

<!-- URLs. -->
[Xamarin.Android quick start]: app-service-mobile-xamarin-android-get-started.md
[Google Cloud Messaging Client Component]: http://components.xamarin.com/view/GCMClient/
[Azure Mobile Services Component]: http://components.xamarin.com/view/azure-mobile-services/
