---
title: aaaGet iniciado com o Azure Mobile Engagement para xamarin. Android
description: "Saiba como toouse Azure Mobile Engagement com notificações Push para aplicações xamarin. Android e de análise."
services: mobile-engagement
documentationcenter: xamarin
author: piyushjo
manager: erikre
editor: 
ms.assetid: fb68cf98-08a2-41b5-8e59-757469de3fe7
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-android
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 06/16/2016
ms.author: piyushjo
ms.openlocfilehash: 9d584fea8e8153d511258cf9b6f87f31dac6aeca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-xamarinandroid-apps"></a><span data-ttu-id="6b120-103">Introdução ao Azure Mobile Engagement para Aplicações Xamarin.Android</span><span class="sxs-lookup"><span data-stu-id="6b120-103">Get Started with Azure Mobile Engagement for Xamarin.Android Apps</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="6b120-104">Este tópico mostra como toouse Azure Mobile Engagement toounderstand a utilização da aplicação e como toosend push a utilizadores de toosegmented de notificações de uma aplicação xamarin. Android.</span><span class="sxs-lookup"><span data-stu-id="6b120-104">This topic shows you how toouse Azure Mobile Engagement toounderstand your app usage and how toosend push notifications toosegmented users of a Xamarin.Android application.</span></span>
<span data-ttu-id="6b120-105">Este tutorial demonstra Olá cenário de difusão simples utilizando o Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="6b120-105">This tutorial demonstrates hello simple broadcast scenario using Mobile Engagement.</span></span> <span data-ttu-id="6b120-106">Aqui, vai criar uma aplicação Xamarin.Android em branco que recolhe dados básicos e recebe notificações push através Google Cloud Messaging (GCM).</span><span class="sxs-lookup"><span data-stu-id="6b120-106">In it, you create a blank Xamarin.Android app that collects basic data and receives push notifications using Google Cloud Messaging (GCM).</span></span>

> [!NOTE]
> <span data-ttu-id="6b120-107">serviço de Azure Mobile Engagement Olá será descontinuado Março de 2018 e está, atualmente, apenas os clientes de tooexisting disponíveis.</span><span class="sxs-lookup"><span data-stu-id="6b120-107">hello Azure Mobile Engagement service will be retired March 2018 and is currently only available tooexisting customers.</span></span> <span data-ttu-id="6b120-108">Para obter mais informações, veja [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span><span class="sxs-lookup"><span data-stu-id="6b120-108">For more information, see [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span></span>

<span data-ttu-id="6b120-109">Este tutorial requer o seguinte Olá:</span><span class="sxs-lookup"><span data-stu-id="6b120-109">This tutorial requires hello following:</span></span>

* <span data-ttu-id="6b120-110">[Xamarin Studio](http://xamarin.com/studio).</span><span class="sxs-lookup"><span data-stu-id="6b120-110">[Xamarin Studio](http://xamarin.com/studio).</span></span> <span data-ttu-id="6b120-111">Também pode utilizar o Visual Studio com Xamarin, mas este tutorial utiliza o Xamarin Studio.</span><span class="sxs-lookup"><span data-stu-id="6b120-111">You can also use Visual Studio with Xamarin but this tutorial uses Xamarin Studio.</span></span> <span data-ttu-id="6b120-112">Para obter instruções de instalação, consulte [Configuração e Instalação do Visual Studio e Xamarin](https://msdn.microsoft.com/library/mt613162.aspx).</span><span class="sxs-lookup"><span data-stu-id="6b120-112">For installation instructions, see [Setup and Install for Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx).</span></span>
* [<span data-ttu-id="6b120-113">SDK Xamarin do Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="6b120-113">Mobile Engagement Xamarin SDK</span></span>](https://www.nuget.org/packages/Microsoft.Azure.Engagement.Xamarin/)

> [!NOTE]
> <span data-ttu-id="6b120-114">toocomplete neste tutorial, tem de ter uma conta do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="6b120-114">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="6b120-115">Se não tiver uma conta, pode criar uma conta de avaliação gratuita em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="6b120-115">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="6b120-116">Para obter mais detalhes, consulte [Avaliação Gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-xamarin-android-get-started).</span><span class="sxs-lookup"><span data-stu-id="6b120-116">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-xamarin-android-get-started).</span></span>
> 
> 

## <span data-ttu-id="6b120-117"><a id="setup-azme"></a>Configurar o Mobile Engagement para a aplicação Android</span><span class="sxs-lookup"><span data-stu-id="6b120-117"><a id="setup-azme"></a>Setup Mobile Engagement for your Android app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <span data-ttu-id="6b120-118"><a id="connecting-app"></a>Ligar o back-end da aplicação toohello Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="6b120-118"><a id="connecting-app"></a>Connect your app toohello Mobile Engagement backend</span></span>
<span data-ttu-id="6b120-119">Este tutorial apresenta uma "integração básica", que é definida de Olá mínima necessária toocollect dados e enviar uma notificação push.</span><span class="sxs-lookup"><span data-stu-id="6b120-119">This tutorial presents a "basic integration", which is hello minimal set required toocollect data and send a push notification.</span></span> 

<span data-ttu-id="6b120-120">Iremos criar uma aplicação básica com a integração do Xamarin Studio toodemonstrate Olá.</span><span class="sxs-lookup"><span data-stu-id="6b120-120">We will create a basic app with Xamarin Studio toodemonstrate hello integration.</span></span>

### <a name="create-a-new-xamarinandroid-project"></a><span data-ttu-id="6b120-121">Criar um novo projeto Xamarin.Android</span><span class="sxs-lookup"><span data-stu-id="6b120-121">Create a new Xamarin.Android project</span></span>
1. <span data-ttu-id="6b120-122">Iniciar **Xamarin Studio** aceda demasiado**ficheiro** -> **novo** -> **solução**</span><span class="sxs-lookup"><span data-stu-id="6b120-122">Launch **Xamarin Studio** Go too**File** -> **New** -> **Solution**</span></span> 
   
    ![][1]
2. <span data-ttu-id="6b120-123">Selecione **aplicação Android** , em seguida, certifique-se de idioma Olá selecionado **c#** e clique em **seguinte**.</span><span class="sxs-lookup"><span data-stu-id="6b120-123">Select **Android App** then make sure hello selected language is **C#** and click **Next**.</span></span>
   
    ![][2]
3. <span data-ttu-id="6b120-124">Preencha Olá **nome da aplicação** e Olá **identificador de organização**.</span><span class="sxs-lookup"><span data-stu-id="6b120-124">Fill in hello **App Name** and hello **Organization Identifier**.</span></span> <span data-ttu-id="6b120-125">Certifique-se de que toocheckmark **serviços Google Play** e, em seguida, clique em **seguinte**.</span><span class="sxs-lookup"><span data-stu-id="6b120-125">Make sure toocheckmark **Google Play Services** and then click **Next**.</span></span> 
   
    ![][3]
4. <span data-ttu-id="6b120-126">Olá atualização **nome do projeto**, **nome da solução** e **localização** se necessário e clique em **criar**.</span><span class="sxs-lookup"><span data-stu-id="6b120-126">Update hello **Project Name**, **Solution Name** and **Location** if required and click **Create**.</span></span>
   
    ![][4]

<span data-ttu-id="6b120-127">Xamarin Studio criará a aplicação Olá na qual iremos integrar o Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="6b120-127">Xamarin Studio will create hello app in which we will integrate Mobile Engagement.</span></span> 

### <a name="connect-your-app-toomobile-engagement-backend"></a><span data-ttu-id="6b120-128">Ligar o back-end da aplicação tooMobile Engagement</span><span class="sxs-lookup"><span data-stu-id="6b120-128">Connect your app tooMobile Engagement backend</span></span>
1. <span data-ttu-id="6b120-129">Clique com o botão direito do rato em Olá **pacotes** pasta nas janelas solução de Olá e selecione **adicionar pacotes...**</span><span class="sxs-lookup"><span data-stu-id="6b120-129">Right click hello **Packages** folder in hello Solution windows and select **Add Packages...**</span></span>
   
    ![][5]
2. <span data-ttu-id="6b120-130">Procure Olá **SDK Xamarin do Microsoft Azure Mobile Engagement** e adicioná-la tooyour solução.</span><span class="sxs-lookup"><span data-stu-id="6b120-130">Search for hello **Microsoft Azure Mobile Engagement Xamarin SDK** and add it tooyour solution.</span></span>  
   
    ![][6]
3. <span data-ttu-id="6b120-131">Abra **mainactivity. cs** e adicione Olá seguintes instruções de utilização:</span><span class="sxs-lookup"><span data-stu-id="6b120-131">Open **MainActivity.cs** and add hello following using statements:</span></span>
   
        using Microsoft.Azure.Engagement;
        using Microsoft.Azure.Engagement.Activity;
4. <span data-ttu-id="6b120-132">No Olá `OnCreate` método, adicione Olá seguinte ligação de Olá tooinitialize com back-end do Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="6b120-132">In hello `OnCreate` method, add hello following tooinitialize hello connection with Mobile Engagement backend.</span></span> <span data-ttu-id="6b120-133">Certifique-se de que tooadd sua **ConnectionString**.</span><span class="sxs-lookup"><span data-stu-id="6b120-133">Make sure tooadd your **ConnectionString**.</span></span> 
   
        EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
        engagementConfiguration.ConnectionString = "YourConnectionStringFromAzurePortal";
        EngagementAgent.Init(engagementConfiguration);

### <a name="add-permissions-and-a-service-declaration"></a><span data-ttu-id="6b120-134">Adicionar permissões e uma declaração de serviço</span><span class="sxs-lookup"><span data-stu-id="6b120-134">Add permissions and a service declaration</span></span>
1. <span data-ttu-id="6b120-135">Abra Olá **Manifest.xml** ficheiro na pasta de propriedades de Olá.</span><span class="sxs-lookup"><span data-stu-id="6b120-135">Open up hello **Manifest.xml** file under hello Properties folder.</span></span> <span data-ttu-id="6b120-136">Selecione o separador origem para que a origem XML Olá diretamente de atualização.</span><span class="sxs-lookup"><span data-stu-id="6b120-136">Select Source tab so that you directly update hello XML source.</span></span>
2. <span data-ttu-id="6b120-137">Adicione estas permissões toohello Manifest.xml (que pode ser encontrado na Olá **propriedades** pasta) do projeto imediatamente antes ou depois Olá `<application>` etiquetas:</span><span class="sxs-lookup"><span data-stu-id="6b120-137">Add these permissions toohello Manifest.xml (which can be found under hello **Properties** folder) of your project immediately before or after hello `<application>` tag:</span></span>
   
        <uses-permission android:name="android.permission.INTERNET"/>
        <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>
        <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/>
        <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />
        <uses-permission android:name="android.permission.VIBRATE" />
        <uses-permission android:name="android.permission.DOWNLOAD_WITHOUT_NOTIFICATION"/>
3. <span data-ttu-id="6b120-138">Adicione o seguinte Olá entre Olá `<application>` e `</application>` etiquetas de serviço do agente toodeclare Olá:</span><span class="sxs-lookup"><span data-stu-id="6b120-138">Add hello following between hello `<application>` and `</application>` tags toodeclare hello agent service:</span></span>
   
        <service
             android:name="com.microsoft.azure.engagement.service.EngagementService"
             android:exported="false"
             android:label="<Your application name>"
             android:process=":Engagement"/>
4. <span data-ttu-id="6b120-139">No código de Olá que acabou de colar, substitua `"<Your application name>"` na etiqueta Olá.</span><span class="sxs-lookup"><span data-stu-id="6b120-139">In hello code you just pasted, replace `"<Your application name>"` in hello label.</span></span> <span data-ttu-id="6b120-140">Isto é apresentado no Olá **definições** menu onde os utilizadores podem ver os serviços em execução no dispositivo Olá.</span><span class="sxs-lookup"><span data-stu-id="6b120-140">This is displayed in hello **Settings** menu where users can see services running on hello device.</span></span> <span data-ttu-id="6b120-141">Por exemplo, pode adicionar palavra Olá "Serviço" nessa etiqueta.</span><span class="sxs-lookup"><span data-stu-id="6b120-141">You can add hello word "Service" in that label for example.</span></span>

### <a name="send-a-screen-toomobile-engagement"></a><span data-ttu-id="6b120-142">Enviar um ecrã tooMobile Engagement</span><span class="sxs-lookup"><span data-stu-id="6b120-142">Send a screen tooMobile Engagement</span></span>
<span data-ttu-id="6b120-143">Na ordem toostart envio de dados e garantir Olá utilizadores estão ativos, terá de enviar, pelo menos, um ecrã o toohello Mobile Engagement backend.</span><span class="sxs-lookup"><span data-stu-id="6b120-143">In order toostart sending data and ensuring hello users are active, you must send at least one screen toohello Mobile Engagement backend.</span></span> <span data-ttu-id="6b120-144">Para fazê-lo-certifique-se de que Olá `MainActivity` herda `EngagementActivity` em vez de `Activity`.</span><span class="sxs-lookup"><span data-stu-id="6b120-144">For doing this - ensure that hello `MainActivity` inherits from `EngagementActivity` instead of `Activity`.</span></span>

    public class MainActivity : EngagementActivity

<span data-ttu-id="6b120-145">Em alternativa, se não for possível herdar de `EngagementActivity`, deve adicionar os métodos `.StartActivity` e `.EndActivity` em `OnResume` e `OnPause`, respetivamente.</span><span class="sxs-lookup"><span data-stu-id="6b120-145">Alternatively, if you cannot inherit from `EngagementActivity` then you must add `.StartActivity` and `.EndActivity` methods in `OnResume` and `OnPause` respectively.</span></span>  

        protected override void OnResume()
            {
                EngagementAgent.StartActivity(EngagementAgentUtils.BuildEngagementActivityName(Java.Lang.Class.FromType(this.GetType())), null);
                base.OnResume();             
            }

            protected override void OnPause()
            {
                EngagementAgent.EndActivity();
                base.OnPause();            
            }

## <span data-ttu-id="6b120-146"><a id="monitor"></a>Ligar a aplicação com a monitorização em tempo real</span><span class="sxs-lookup"><span data-stu-id="6b120-146"><a id="monitor"></a>Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <span data-ttu-id="6b120-147"><a id="integrate-push"></a>Ativar as notificações push e mensagens na aplicação</span><span class="sxs-lookup"><span data-stu-id="6b120-147"><a id="integrate-push"></a>Enable push notifications and in-app messaging</span></span>
<span data-ttu-id="6b120-148">O Mobile Engagement permite-lhe toointeract com e ALCANÇAR os seus utilizadores com notificações push e mensagens no contexto de Olá das campanhas na aplicação.</span><span class="sxs-lookup"><span data-stu-id="6b120-148">Mobile Engagement allows you toointeract with and REACH your users with push notifications and in-app messaging in hello context of campaigns.</span></span> <span data-ttu-id="6b120-149">Este módulo é designado alcance no portal de Mobile Engagement Olá.</span><span class="sxs-lookup"><span data-stu-id="6b120-149">This module is called REACH in hello Mobile Engagement portal.</span></span>
<span data-ttu-id="6b120-150">Olá secções a seguir configura a aplicação tooreceive-los.</span><span class="sxs-lookup"><span data-stu-id="6b120-150">hello following sections sets up your app tooreceive them.</span></span>

[!INCLUDE [Enable Google Cloud Messaging](../../includes/mobile-engagement-enable-google-cloud-messaging.md)]

[!INCLUDE [Enable in-app messaging](../../includes/mobile-engagement-android-send-push.md)]

[!INCLUDE [Send notification from portal](../../includes/mobile-engagement-android-send-push-from-portal.md)]

<!-- Images -->
[1]: ./media/mobile-engagement-xamarin-android-get-started/1.png
[2]: ./media/mobile-engagement-xamarin-android-get-started/2.png
[3]: ./media/mobile-engagement-xamarin-android-get-started/3.png
[4]: ./media/mobile-engagement-xamarin-android-get-started/4.png
[5]: ./media/mobile-engagement-xamarin-android-get-started/5.png
[6]: ./media/mobile-engagement-xamarin-android-get-started/6.png
