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
# <a name="add-push-notifications-tooyour-xamarinandroid-app"></a><span data-ttu-id="3d93c-103">Adicionar a aplicação de xamarin. Android de tooyour de notificações push</span><span class="sxs-lookup"><span data-stu-id="3d93c-103">Add push notifications tooyour Xamarin.Android app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a><span data-ttu-id="3d93c-104">Descrição geral</span><span class="sxs-lookup"><span data-stu-id="3d93c-104">Overview</span></span>
<span data-ttu-id="3d93c-105">Neste tutorial, adicionar toohello de notificações push [início rápido do xamarin. Android](app-service-mobile-windows-store-dotnet-get-started.md) projeto para que uma notificação push é enviada toohello dispositivo sempre que é inserido um registo.</span><span class="sxs-lookup"><span data-stu-id="3d93c-105">In this tutorial, you add push notifications toohello [Xamarin.Android quick start](app-service-mobile-windows-store-dotnet-get-started.md) project so that a push notification is sent toohello device every time a record is inserted.</span></span>

<span data-ttu-id="3d93c-106">Se não utilizar Olá transferir o projeto de servidor de início rápido, será necessário Olá pacote de extensão de notificação push.</span><span class="sxs-lookup"><span data-stu-id="3d93c-106">If you do not use hello downloaded quick start server project, you will need hello push notification extension package.</span></span> <span data-ttu-id="3d93c-107">Consulte [trabalhar com o servidor de back-end de .NET Olá SDK de Mobile Apps do Azure](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="3d93c-107">See [Work with hello .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) for more information.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3d93c-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="3d93c-108">Prerequisites</span></span>
<span data-ttu-id="3d93c-109">Este tutorial requer o seguinte Olá:</span><span class="sxs-lookup"><span data-stu-id="3d93c-109">This tutorial requires hello following:</span></span>

* <span data-ttu-id="3d93c-110">Uma conta Google ativa.</span><span class="sxs-lookup"><span data-stu-id="3d93c-110">An active Google account.</span></span> <span data-ttu-id="3d93c-111">Pode inscrever-se para uma conta do Google na [accounts.google.com](http://go.microsoft.com/fwlink/p/?LinkId=268302).</span><span class="sxs-lookup"><span data-stu-id="3d93c-111">You can sign up for a Google account at [accounts.google.com](http://go.microsoft.com/fwlink/p/?LinkId=268302).</span></span>
* <span data-ttu-id="3d93c-112">[Google Cloud Messaging o componente de cliente](http://components.xamarin.com/view/GCMClient/).</span><span class="sxs-lookup"><span data-stu-id="3d93c-112">[Google Cloud Messaging Client Component](http://components.xamarin.com/view/GCMClient/).</span></span>

## <span data-ttu-id="3d93c-113"><a name="configure-hub"></a>Configurar um Hub de notificação</span><span class="sxs-lookup"><span data-stu-id="3d93c-113"><a name="configure-hub"></a>Configure a Notification Hub</span></span>
[!INCLUDE [app-service-mobile-configure-notification-hub](../../includes/app-service-mobile-configure-notification-hub.md)]

## <span data-ttu-id="3d93c-114"><a id="register"></a>Ativar o Firebase Cloud Messaging</span><span class="sxs-lookup"><span data-stu-id="3d93c-114"><a id="register"></a>Enable Firebase Cloud Messaging</span></span>
[!INCLUDE [notification-hubs-enable-firebase-cloud-messaging](../../includes/notification-hubs-enable-firebase-cloud-messaging.md)]

## <a name="configure-azure-toosend-push-requests"></a><span data-ttu-id="3d93c-115">Configurar os pedidos de push toosend do Azure</span><span class="sxs-lookup"><span data-stu-id="3d93c-115">Configure Azure toosend push requests</span></span>
[!INCLUDE [app-service-mobile-android-configure-push](../../includes/app-service-mobile-android-configure-push-for-firebase.md)]

## <span data-ttu-id="3d93c-116"><a id="update-server"></a>Atualizar notificações de push Olá servidor projeto toosend</span><span class="sxs-lookup"><span data-stu-id="3d93c-116"><a id="update-server"></a>Update hello server project toosend push notifications</span></span>
[!INCLUDE [app-service-mobile-update-server-project-for-push-template](../../includes/app-service-mobile-update-server-project-for-push-template.md)]

## <span data-ttu-id="3d93c-117"><a id="configure-app"></a>Configurar o projeto de cliente Olá para notificações push</span><span class="sxs-lookup"><span data-stu-id="3d93c-117"><a id="configure-app"></a>Configure hello client project for push notifications</span></span>
[!INCLUDE [mobile-services-xamarin-android-push-configure-project](../../includes/mobile-services-xamarin-android-push-configure-project.md)]

## <span data-ttu-id="3d93c-118"><a id="add-push"></a>Adicionar a aplicação de tooyour de código de notificações push</span><span class="sxs-lookup"><span data-stu-id="3d93c-118"><a id="add-push"></a>Add push notifications code tooyour app</span></span>
[!INCLUDE [app-service-mobile-xamarin-android-push-add-to-app](../../includes/app-service-mobile-xamarin-android-push-add-to-app.md)]

## <span data-ttu-id="3d93c-119"><a name="test"></a>Notificações de push de teste na sua aplicação</span><span class="sxs-lookup"><span data-stu-id="3d93c-119"><a name="test"></a>Test push notifications in your app</span></span>
<span data-ttu-id="3d93c-120">Pode testar a aplicação Olá através da utilização de um dispositivo virtual no emulador Olá.</span><span class="sxs-lookup"><span data-stu-id="3d93c-120">You can test hello app by using a virtual device in hello emulator.</span></span> <span data-ttu-id="3d93c-121">Existem passos de configuração adicionais necessários quando em execução num emulador.</span><span class="sxs-lookup"><span data-stu-id="3d93c-121">There are additional configuration steps required when running on an emulator.</span></span>

1. <span data-ttu-id="3d93c-122">Certifique-se de que está a implementar tooor depuração num dispositivo virtual que tenha as APIs da Google definir como destino de Olá, conforme mostrado abaixo no Gestor do Olá dispositivo Virtual Android (AVD).</span><span class="sxs-lookup"><span data-stu-id="3d93c-122">Make sure that you are deploying tooor debugging on a virtual device that has Google APIs set as hello target, as shown below in hello Android Virtual Device (AVD) manager.</span></span>
   
    ![](./media/app-service-mobile-xamarin-android-get-started-push/google-apis-avd-settings.png)
2. <span data-ttu-id="3d93c-123">Adicionar um dispositivo Android do Google conta toohello clicando **aplicações** > **definições** > **adicionar conta**, em seguida, siga as instruções de Olá.</span><span class="sxs-lookup"><span data-stu-id="3d93c-123">Add a Google account toohello Android device by clicking **Apps** > **Settings** > **Add account**, then follow hello prompts.</span></span>
   
    ![](./media/app-service-mobile-xamarin-android-get-started-push/add-google-account.png)
3. <span data-ttu-id="3d93c-124">Executar a aplicação de todolist Olá como antes e inserir um novo item de todo.</span><span class="sxs-lookup"><span data-stu-id="3d93c-124">Run hello todolist app as before and insert a new todo item.</span></span> <span data-ttu-id="3d93c-125">Este tempo, um ícone de notificação é apresentado na área de notificação de Olá.</span><span class="sxs-lookup"><span data-stu-id="3d93c-125">This time, a notification icon is displayed in hello notification area.</span></span> <span data-ttu-id="3d93c-126">Pode abrir Olá notificação gaveta tooview Olá texto completo de notificação de Olá.</span><span class="sxs-lookup"><span data-stu-id="3d93c-126">You can open hello notification drawer tooview hello full text of hello notification.</span></span>
   
    ![](./media/app-service-mobile-xamarin-android-get-started-push/android-notifications.png)

<!-- URLs. -->
[Xamarin.Android quick start]: app-service-mobile-xamarin-android-get-started.md
[Google Cloud Messaging Client Component]: http://components.xamarin.com/view/GCMClient/
[Azure Mobile Services Component]: http://components.xamarin.com/view/azure-mobile-services/
