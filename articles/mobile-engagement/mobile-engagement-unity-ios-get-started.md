---
title: "aaaGet iniciado com o Azure Mobile Engagement para implementação do Unity iOS"
description: "Saiba como toouse Azure Mobile Engagement com notificações Push e de análise para aplicações Unity tooiOS dispositivos."
services: mobile-engagement
documentationcenter: unity
author: piyushjo
manager: erikre
editor: 
ms.assetid: 7ddfbac3-8d13-4ebe-b061-c865f357297f
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-unity-ios
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: f4247b0a9240cbe2bf1a6618388919d3554c07fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-unity-ios-deployment"></a><span data-ttu-id="08fe2-103">Introdução ao Azure Mobile Engagement para implementação do Unity iOS</span><span class="sxs-lookup"><span data-stu-id="08fe2-103">Get Started with Azure Mobile Engagement for Unity iOS deployment</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="08fe2-104">Este tópico mostra como toouse Azure Mobile Engagement toounderstand a utilização da aplicação e como toosend push a utilizadores de toosegmented notificações de uma aplicação Unity quando implementar o dispositivo iOS tooan.</span><span class="sxs-lookup"><span data-stu-id="08fe2-104">This topic shows you how toouse Azure Mobile Engagement toounderstand your app usage and how toosend push notifications toosegmented users of a Unity application when deploying tooan iOS device.</span></span>
<span data-ttu-id="08fe2-105">Este tutorial utiliza Olá clássico Unity Roll um tutorial Ball como Olá ponto de partida.</span><span class="sxs-lookup"><span data-stu-id="08fe2-105">This tutorial uses hello classic Unity Roll a Ball tutorial as hello starting point.</span></span> <span data-ttu-id="08fe2-106">Deve seguir os passos de Olá neste [tutorial](mobile-engagement-unity-roll-a-ball.md) antes de continuar com Olá integração do Mobile Engagement que demonstramos no tutorial Olá abaixo.</span><span class="sxs-lookup"><span data-stu-id="08fe2-106">You should follow hello steps in this [tutorial](mobile-engagement-unity-roll-a-ball.md) before proceeding with hello Mobile Engagement integration we showcase in hello tutorial below.</span></span> 

<span data-ttu-id="08fe2-107">Este tutorial requer o seguinte Olá:</span><span class="sxs-lookup"><span data-stu-id="08fe2-107">This tutorial requires hello following:</span></span>

* [<span data-ttu-id="08fe2-108">Unity Editor</span><span class="sxs-lookup"><span data-stu-id="08fe2-108">Unity Editor</span></span>](http://unity3d.com/get-unity)
* [<span data-ttu-id="08fe2-109">SDK Unity do Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="08fe2-109">Mobile Engagement Unity SDK</span></span>](https://aka.ms/azmeunitysdk)
* <span data-ttu-id="08fe2-110">XCode Editor</span><span class="sxs-lookup"><span data-stu-id="08fe2-110">XCode Editor</span></span>

> [!NOTE]
> <span data-ttu-id="08fe2-111">toocomplete neste tutorial, tem de ter uma conta do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="08fe2-111">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="08fe2-112">Se não tiver uma conta, pode criar uma conta de avaliação gratuita em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="08fe2-112">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="08fe2-113">Para obter mais detalhes, consulte [Avaliação Gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-unity-ios-get-started).</span><span class="sxs-lookup"><span data-stu-id="08fe2-113">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-unity-ios-get-started).</span></span>
> 
> 

## <span data-ttu-id="08fe2-114"><a id="setup-azme"></a>Configurar o Mobile Engagement para a aplicação iOS</span><span class="sxs-lookup"><span data-stu-id="08fe2-114"><a id="setup-azme"></a>Setup Mobile Engagement for your iOS app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <span data-ttu-id="08fe2-115"><a id="connecting-app"></a>Ligar o back-end da aplicação toohello Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="08fe2-115"><a id="connecting-app"></a>Connect your app toohello Mobile Engagement backend</span></span>
### <a name="import-hello-unity-package"></a><span data-ttu-id="08fe2-116">Importar o pacote do Unity Olá</span><span class="sxs-lookup"><span data-stu-id="08fe2-116">Import hello Unity package</span></span>
1. <span data-ttu-id="08fe2-117">Transferir Olá [pacote Unity do Mobile Engagement](https://aka.ms/azmeunitysdk) e guarde-o computador local tooyour.</span><span class="sxs-lookup"><span data-stu-id="08fe2-117">Download hello [Mobile Engagement Unity package](https://aka.ms/azmeunitysdk) and save it tooyour local machine.</span></span> 
2. <span data-ttu-id="08fe2-118">Aceda demasiado**elementos -> Importar pacote -> pacote personalizado** e selecione Olá do pacote transferido no Olá passos acima.</span><span class="sxs-lookup"><span data-stu-id="08fe2-118">Go too**Assets -> Import Package -> Custom Package** and select hello package you downloaded in hello above step.</span></span> 
   
    ![][70] 
3. <span data-ttu-id="08fe2-119">Certifique-se de que todos os ficheiros estão selecionados e clique no botão **Importar**.</span><span class="sxs-lookup"><span data-stu-id="08fe2-119">Make sure all files are selected and click **Import** button.</span></span> 
   
    ![][71] 
4. <span data-ttu-id="08fe2-120">Assim que importar com êxito, verá os ficheiros do SDK de Olá importado no seu projeto.</span><span class="sxs-lookup"><span data-stu-id="08fe2-120">Once Import is successful, you will see hello imported SDK files in your project.</span></span>  
   
    ![][72] 

### <a name="update-hello-engagementconfiguration"></a><span data-ttu-id="08fe2-121">Atualizar Olá EngagementConfiguration</span><span class="sxs-lookup"><span data-stu-id="08fe2-121">Update hello EngagementConfiguration</span></span>
1. <span data-ttu-id="08fe2-122">Abra Olá **EngagementConfiguration** ficheiro de script de Olá de pasta e a atualização do SDK de Olá **IOS\_ligação\_cadeia** com a cadeia de ligação de Olá que obteve anteriormente de Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="08fe2-122">Open up hello **EngagementConfiguration** script file from hello SDK folder and update hello **IOS\_CONNECTION\_STRING** with hello connection string you obtained earlier from hello Azure portal.</span></span>  
   
    ![][73]
2. <span data-ttu-id="08fe2-123">Guarde o ficheiro de Olá.</span><span class="sxs-lookup"><span data-stu-id="08fe2-123">Save hello file.</span></span> 

### <a name="configure-hello-app-for-basic-tracking"></a><span data-ttu-id="08fe2-124">Configurar aplicação Olá para controlo básico</span><span class="sxs-lookup"><span data-stu-id="08fe2-124">Configure hello app for basic tracking</span></span>
1. <span data-ttu-id="08fe2-125">Abra Olá **PlayerController** script anexado toohello o objeto de leitor para edição.</span><span class="sxs-lookup"><span data-stu-id="08fe2-125">Open up hello **PlayerController** script attached toohello Player object for editing.</span></span> 
2. <span data-ttu-id="08fe2-126">Adicione Olá seguinte utilizando a instrução:</span><span class="sxs-lookup"><span data-stu-id="08fe2-126">Add hello following using statement:</span></span>
   
        using Microsoft.Azure.Engagement.Unity;
3. <span data-ttu-id="08fe2-127">Adicionar Olá seguir toohello `Start()` método</span><span class="sxs-lookup"><span data-stu-id="08fe2-127">Add hello following toohello `Start()` method</span></span>
   
        EngagementAgent.Initialize();
        EngagementAgent.StartActivity("Home");

### <a name="deploy-and-run-hello-app"></a><span data-ttu-id="08fe2-128">Implementar e executar a aplicação de Olá</span><span class="sxs-lookup"><span data-stu-id="08fe2-128">Deploy and run hello app</span></span>
1. <span data-ttu-id="08fe2-129">Ligar uma máquina de tooyour do dispositivo iOS.</span><span class="sxs-lookup"><span data-stu-id="08fe2-129">Connect an iOS device tooyour machine.</span></span> 
2. <span data-ttu-id="08fe2-130">Abra **Ficheiro -> Definições de Criação**</span><span class="sxs-lookup"><span data-stu-id="08fe2-130">Open up **File -> Build Settings**</span></span> 
   
    ![][40]
3. <span data-ttu-id="08fe2-131">Selecione **iOS** e, em seguida, clique em **Alternar Plataforma**</span><span class="sxs-lookup"><span data-stu-id="08fe2-131">Select **iOS** and then click on **Switch Platform**</span></span>
   
    ![][41]
   
    ![][42]
4. <span data-ttu-id="08fe2-132">Clique em **Definições de leitor** e faculte um Identificador de Pacote válido.</span><span class="sxs-lookup"><span data-stu-id="08fe2-132">Click on **Player settings** and provide a valid Bundle Identifier.</span></span> 
   
    ![][53]
5. <span data-ttu-id="08fe2-133">Finalmente, clique em **Criar e Executar**</span><span class="sxs-lookup"><span data-stu-id="08fe2-133">Finally click on **Build And Run**</span></span>
   
    ![][54]
6. <span data-ttu-id="08fe2-134">Poderá ser-lhe pedido tooprovide um pacote de iOS Olá de toostore de nome de pasta.</span><span class="sxs-lookup"><span data-stu-id="08fe2-134">You may be asked tooprovide a folder name toostore hello iOS package.</span></span> 
   
    ![][43]
7. <span data-ttu-id="08fe2-135">Se tudo correr bem, Olá projeto será compilado e deve abri-lo cópias de segurança na sua aplicação XCode.</span><span class="sxs-lookup"><span data-stu-id="08fe2-135">If everything goes fine, then hello project will be compiled and you should open it up on your XCode application.</span></span> 
8. <span data-ttu-id="08fe2-136">Certifique-se de que Olá **identificador de pacote** está correto no projeto Olá.</span><span class="sxs-lookup"><span data-stu-id="08fe2-136">Make sure that hello **Bundle identifier** is correct in hello project.</span></span>  
   
    ![][75]
9. <span data-ttu-id="08fe2-137">Agora, execute Olá aplicação no XCode para que o pacote de Olá é o dispositivo ligado tooyour implementado e deverá ver o seu jogo Unity no seu telemóvel!</span><span class="sxs-lookup"><span data-stu-id="08fe2-137">Now run hello app in XCode so that hello package is deployed tooyour connected device and you should see your Unity game on your phone!</span></span> 

## <span data-ttu-id="08fe2-138"><a id="monitor"></a>Ligar a aplicação com a monitorização em tempo real</span><span class="sxs-lookup"><span data-stu-id="08fe2-138"><a id="monitor"></a>Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <span data-ttu-id="08fe2-139"><a id="integrate-push"></a>Ativar as notificações push e mensagens na aplicação</span><span class="sxs-lookup"><span data-stu-id="08fe2-139"><a id="integrate-push"></a>Enable push notifications and in-app messaging</span></span>
<span data-ttu-id="08fe2-140">O Mobile Engagement permite-lhe toointeract com os seus utilizadores e ao alcance com notificações push e mensagens no contexto de Olá das campanhas na aplicação.</span><span class="sxs-lookup"><span data-stu-id="08fe2-140">Mobile Engagement allows you toointeract with your users and REACH with push notifications and in-app messaging in hello context of campaigns.</span></span> <span data-ttu-id="08fe2-141">Este módulo é designado alcance no portal de Mobile Engagement Olá.</span><span class="sxs-lookup"><span data-stu-id="08fe2-141">This module is called REACH in hello Mobile Engagement portal.</span></span>
<span data-ttu-id="08fe2-142">Toodo não tem qualquer configuração adicional na sua tooreceive notificações da aplicação e já está configurada para tal.</span><span class="sxs-lookup"><span data-stu-id="08fe2-142">You don't have toodo any additional configuration in your app tooreceive notifications and it is already setup for it.</span></span>

[!INCLUDE [mobile-engagement-ios-send-push-push](../../includes/mobile-engagement-ios-send-push.md)]

<!-- Images. -->
[40]: ./media/mobile-engagement-unity-ios-get-started/40.png
[41]: ./media/mobile-engagement-unity-ios-get-started/41.png
[42]: ./media/mobile-engagement-unity-ios-get-started/42.png
[43]: ./media/mobile-engagement-unity-ios-get-started/43.png
[53]: ./media/mobile-engagement-unity-ios-get-started/53.png
[54]: ./media/mobile-engagement-unity-ios-get-started/54.png
[70]: ./media/mobile-engagement-unity-ios-get-started/70.png
[71]: ./media/mobile-engagement-unity-ios-get-started/71.png
[72]: ./media/mobile-engagement-unity-ios-get-started/72.png
[73]: ./media/mobile-engagement-unity-ios-get-started/73.png
[74]: ./media/mobile-engagement-unity-ios-get-started/74.png
[75]: ./media/mobile-engagement-unity-ios-get-started/75.png
