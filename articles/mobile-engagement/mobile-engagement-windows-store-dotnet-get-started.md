---
title: "aaaGet ao Windows Universal aplicações do Azure Mobile Engagement"
description: "Saiba como toouse Azure Mobile Engagement com notificações push e de análise para aplicações universais do Windows."
services: mobile-engagement
documentationcenter: windows
author: piyushjo
manager: erikre
editor: 
ms.assetid: 48103867-7f64-4646-b019-42bd797d38e2
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 08/12/2016
ms.author: piyushjo;ricksal
ms.openlocfilehash: 8224a6d3789cfe4784bbc9472005f9eddb94a8b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-windows-universal-apps"></a><span data-ttu-id="c535c-103">Introdução ao Azure Mobile Engagement para Aplicações Universais do Windows</span><span class="sxs-lookup"><span data-stu-id="c535c-103">Get started with Azure Mobile Engagement for Windows Universal Apps</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="c535c-104">Este tópico mostra como toouse Azure Mobile Engagement toounderstand a utilização da aplicação e enviar push a utilizadores de toosegmented de notificações de uma aplicação Universal do Windows.</span><span class="sxs-lookup"><span data-stu-id="c535c-104">This topic shows you how toouse Azure Mobile Engagement toounderstand your app usage and send push notifications toosegmented users of a Windows Universal application.</span></span>
<span data-ttu-id="c535c-105">Este tutorial demonstra Olá cenário de difusão simples utilizando o Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="c535c-105">This tutorial demonstrates hello simple broadcast scenario using Mobile Engagement.</span></span> <span data-ttu-id="c535c-106">Irá criar uma Aplicação Universal do Windows em branco que recolhe dados de utilização de aplicação básicas e recebe notificações push através do Serviço de Notificações do Windows (WNS).</span><span class="sxs-lookup"><span data-stu-id="c535c-106">You create a blank Windows Universal App that collects basic app usage data and receives push notifications using Windows Notification Service (WNS).</span></span>

> [!NOTE]
> <span data-ttu-id="c535c-107">serviço de Azure Mobile Engagement Olá será descontinuado Março de 2018 e está, atualmente, apenas os clientes de tooexisting disponíveis.</span><span class="sxs-lookup"><span data-stu-id="c535c-107">hello Azure Mobile Engagement service will be retired March 2018 and is currently only available tooexisting customers.</span></span> <span data-ttu-id="c535c-108">Para obter mais informações, veja [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span><span class="sxs-lookup"><span data-stu-id="c535c-108">For more information, see [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c535c-109">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="c535c-109">Prerequisites</span></span>
[!INCLUDE [Prereqs](../../includes/mobile-engagement-windows-store-prereqs.md)]

## <a name="set-up-mobile-engagement-for-your-windows-universal-app"></a><span data-ttu-id="c535c-110">Configurar o Mobile Engagement para a aplicação Universal do Windows</span><span class="sxs-lookup"><span data-stu-id="c535c-110">Set up Mobile Engagement for your Windows Universal app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <span data-ttu-id="c535c-111"><a id="connecting-app"></a>Ligar o back-end da aplicação toohello Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="c535c-111"><a id="connecting-app"></a>Connect your app toohello Mobile Engagement backend</span></span>
<span data-ttu-id="c535c-112">Este tutorial apresenta uma "integração básica," que é definida de Olá mínima necessária toocollect dados e enviar uma notificação push.</span><span class="sxs-lookup"><span data-stu-id="c535c-112">This tutorial presents a "basic integration," which is hello minimal set required toocollect data and send a push notification.</span></span> <span data-ttu-id="c535c-113">a documentação da integração completa Olá pode ser encontrada na Olá [integração do SDK do Mobile Engagement Windows Universal](mobile-engagement-windows-store-sdk-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c535c-113">hello complete integration documentation can be found in hello [Mobile Engagement Windows Universal SDK integration](mobile-engagement-windows-store-sdk-overview.md).</span></span>

<span data-ttu-id="c535c-114">Criar uma aplicação básica com a integração do Visual Studio toodemonstrate Olá.</span><span class="sxs-lookup"><span data-stu-id="c535c-114">You create a basic app with Visual Studio toodemonstrate hello integration.</span></span>

### <a name="create-a-windows-universal-app-project"></a><span data-ttu-id="c535c-115">Criar um projeto da Aplicação Universal do Windows</span><span class="sxs-lookup"><span data-stu-id="c535c-115">Create a Windows Universal App project</span></span>
<span data-ttu-id="c535c-116">Olá seguintes passos assumem Olá utilização do Visual Studio 2015 apesar dos passos de Olá serem semelhantes em versões anteriores do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c535c-116">hello following steps assume hello use of Visual Studio 2015 though hello steps are similar in earlier versions of Visual Studio.</span></span>

1. <span data-ttu-id="c535c-117">Inicie o Visual Studio e em Olá **home page** ecrã, selecione **novo projeto**.</span><span class="sxs-lookup"><span data-stu-id="c535c-117">Start Visual Studio, and in hello **Home** screen, select **New Project**.</span></span>
2. <span data-ttu-id="c535c-118">No pop-up de Olá, selecione **Windows** -> **Universal** -> **aplicação em branco (Universal Windows)**.</span><span class="sxs-lookup"><span data-stu-id="c535c-118">In hello pop-up, select **Windows** -> **Universal** -> **Blank App (Universal Windows)**.</span></span> <span data-ttu-id="c535c-119">Preencha aplicação Olá **nome** e **nome da solução**e, em seguida, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="c535c-119">Fill in hello app **Name** and **Solution name**, and then click **OK**.</span></span>

    ![][1]

<span data-ttu-id="c535c-120">Acabou de criar um projeto de aplicação Universal do Windows no qual, em seguida, integrar Olá Azure Mobile Engagement SDK.</span><span class="sxs-lookup"><span data-stu-id="c535c-120">You have now created a Windows Universal App project into which you next integrate hello Azure Mobile Engagement SDK.</span></span>

### <a name="connect-your-app-toomobile-engagement-backend"></a><span data-ttu-id="c535c-121">Ligar o back-end da aplicação tooMobile Engagement</span><span class="sxs-lookup"><span data-stu-id="c535c-121">Connect your app tooMobile Engagement backend</span></span>
1. <span data-ttu-id="c535c-122">Instalar Olá [microsoftazure. Mobileengagement] pacote Nuget do seu projeto.</span><span class="sxs-lookup"><span data-stu-id="c535c-122">Install hello [MicrosoftAzure.MobileEngagement] Nuget package in your project.</span></span> <span data-ttu-id="c535c-123">Se tiver como objetivo as plataformas Windows e Windows Phone, terá de toodo isto para ambos os projetos.</span><span class="sxs-lookup"><span data-stu-id="c535c-123">If you are targeting both Windows and Windows Phone platforms, you need toodo this for both projects.</span></span> <span data-ttu-id="c535c-124">Para o Windows 8. x e Windows Phone 8.1, Olá mesmos Nuget pacote locais Olá corretos binários específicos da plataforma em cada projeto.</span><span class="sxs-lookup"><span data-stu-id="c535c-124">For Windows 8.x and Windows Phone 8.1, hello same Nuget package places hello correct platform-specific binaries in each project.</span></span>
2. <span data-ttu-id="c535c-125">Abra **Package. appxmanifest** e certifique-se de que Olá seguir capacidade está adicionada aí:</span><span class="sxs-lookup"><span data-stu-id="c535c-125">Open **Package.appxmanifest** and make sure that hello following capability is added there:</span></span>

        Internet (Client)

    ![][2]
3. <span data-ttu-id="c535c-126">Agora copie a cadeia de ligação de Olá que copiou anteriormente para a sua aplicação de Mobile Engagement e cole-o no Olá `Resources\EngagementConfiguration.xml` ficheiros, entre Olá `<connectionString>` e `</connectionString>` etiquetas:</span><span class="sxs-lookup"><span data-stu-id="c535c-126">Now copy hello connection string that you copied earlier for your Mobile Engagement App and paste it in hello `Resources\EngagementConfiguration.xml` file, between hello `<connectionString>` and `</connectionString>` tags:</span></span>

    ![][3]

    > [!TIP]
    > <span data-ttu-id="c535c-127">Se a sua Aplicação visar as plataformas Windows e Windows Phone, deve criar ainda duas Aplicações Mobile Engagement – uma para cada plataforma suportada.</span><span class="sxs-lookup"><span data-stu-id="c535c-127">If your App targets both Windows and Windows Phone platforms, you should still create two Mobile Engagement Applications - one for each supported platform.</span></span> <span data-ttu-id="c535c-128">Ter duas aplicações assegura que pode criar a segmentação correta do público-alvo de Olá e pode enviar notificações adequadamente segmentadas para cada plataforma.</span><span class="sxs-lookup"><span data-stu-id="c535c-128">Having two apps ensures that you can create correct segmentation of hello audience and can send appropriately targeted notifications for each platform.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="c535c-129">NuGet automaticamente não copiar recursos do SDK Olá na sua aplicação UWP do Windows 10.</span><span class="sxs-lookup"><span data-stu-id="c535c-129">NuGet does not automatically copy hello SDK resources in your Windows 10 UWP application.</span></span> <span data-ttu-id="c535c-130">Tiver toodo-lo manualmente os seguintes passos de Olá que apareçam (readme.txt) quando o pacote Nuget de Olá está instalado.</span><span class="sxs-lookup"><span data-stu-id="c535c-130">You have toodo it manually following hello steps which show up (readme.txt) when hello Nuget package is installed.</span></span>  

1. <span data-ttu-id="c535c-131">No Olá `App.xaml.cs` ficheiro:</span><span class="sxs-lookup"><span data-stu-id="c535c-131">In hello `App.xaml.cs` file:</span></span>

    <span data-ttu-id="c535c-132">a.</span><span class="sxs-lookup"><span data-stu-id="c535c-132">a.</span></span> <span data-ttu-id="c535c-133">Adicionar Olá `using` instrução:</span><span class="sxs-lookup"><span data-stu-id="c535c-133">Add hello `using` statement:</span></span>

            using Microsoft.Azure.Engagement;

    <span data-ttu-id="c535c-134">b.</span><span class="sxs-lookup"><span data-stu-id="c535c-134">b.</span></span> <span data-ttu-id="c535c-135">Adicione um método que inicializa Olá o Engagement:</span><span class="sxs-lookup"><span data-stu-id="c535c-135">Add a method that initializes hello Engagement:</span></span>

           private void InitEngagement(IActivatedEventArgs e)
           {
             EngagementAgent.Instance.Init(e);

             //... rest of hello code
           }

    <span data-ttu-id="c535c-136">c.</span><span class="sxs-lookup"><span data-stu-id="c535c-136">c.</span></span> <span data-ttu-id="c535c-137">Inicializar Olá SDK no Olá **OnLaunched** método:</span><span class="sxs-lookup"><span data-stu-id="c535c-137">Initialize hello SDK in hello **OnLaunched** method:</span></span>

            protected override void OnLaunched(LaunchActivatedEventArgs e)
            {
              InitEngagement(e);

              //... rest of hello code
            }

    <span data-ttu-id="c535c-138">c.</span><span class="sxs-lookup"><span data-stu-id="c535c-138">c.</span></span> <span data-ttu-id="c535c-139">Insira o seguinte Olá na Olá **OnActivated** método e adicione o método de Olá se não estiver já presente:</span><span class="sxs-lookup"><span data-stu-id="c535c-139">Insert hello following in hello **OnActivated** method and add hello method if it is not already present:</span></span>

            protected override void OnActivated(IActivatedEventArgs e)
            {
              InitEngagement(e);

              //... rest of hello code
            }

## <span data-ttu-id="c535c-140"><a id="monitor"></a>Ativar a monitorização em tempo real</span><span class="sxs-lookup"><span data-stu-id="c535c-140"><a id="monitor"></a>Enable real-time monitoring</span></span>
<span data-ttu-id="c535c-141">toostart envio de dados e garantir que os utilizadores de Olá estão ativos, terá de enviar, pelo menos, um ecrã (atividade) o toohello Mobile Engagement backend.</span><span class="sxs-lookup"><span data-stu-id="c535c-141">toostart sending data and ensuring that hello users are active, you must send at least one screen (Activity) toohello Mobile Engagement backend.</span></span>

1. <span data-ttu-id="c535c-142">No Olá **MainPage.xaml.cs**, adicione Olá seguinte `using` instrução:</span><span class="sxs-lookup"><span data-stu-id="c535c-142">In hello **MainPage.xaml.cs**, add hello following `using` statement:</span></span>

    <span data-ttu-id="c535c-143">utilizar o Microsoft.Azure.Engagement.Overlay;</span><span class="sxs-lookup"><span data-stu-id="c535c-143">using Microsoft.Azure.Engagement.Overlay;</span></span>
2. <span data-ttu-id="c535c-144">Alterar a classe base do Olá de **MainPage** de **página** demasiado**EngagementPageOverlay**:</span><span class="sxs-lookup"><span data-stu-id="c535c-144">Change hello base class of **MainPage** from **Page** too**EngagementPageOverlay**:</span></span>

        class MainPage : EngagementPageOverlay
3. <span data-ttu-id="c535c-145">No Olá `MainPage.xaml` ficheiro:</span><span class="sxs-lookup"><span data-stu-id="c535c-145">In hello `MainPage.xaml` file:</span></span>

    <span data-ttu-id="c535c-146">a.</span><span class="sxs-lookup"><span data-stu-id="c535c-146">a.</span></span> <span data-ttu-id="c535c-147">Adicione declarações de espaços de nomes de tooyour:</span><span class="sxs-lookup"><span data-stu-id="c535c-147">Add tooyour namespaces declarations:</span></span>

        xmlns:engagement="using:Microsoft.Azure.Engagement.Overlay"

    <span data-ttu-id="c535c-148">b.</span><span class="sxs-lookup"><span data-stu-id="c535c-148">b.</span></span> <span data-ttu-id="c535c-149">Substitua Olá **página** no nome de etiqueta XML Olá com **engagement: EngagementPageOverlay**</span><span class="sxs-lookup"><span data-stu-id="c535c-149">Replace hello **Page** in hello XML tag name with **engagement:EngagementPageOverlay**</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c535c-150">Se a sua página substitui Olá `OnNavigatedTo` método, ser toocall se `base.OnNavigatedTo(e)`.</span><span class="sxs-lookup"><span data-stu-id="c535c-150">If your page overrides hello `OnNavigatedTo` method, be sure toocall `base.OnNavigatedTo(e)`.</span></span> <span data-ttu-id="c535c-151">Caso contrário, não foi reportada atividade Olá `EngagementPage` chamadas `StartActivity` dentro respetivo `OnNavigatedTo` método).</span><span class="sxs-lookup"><span data-stu-id="c535c-151">Otherwise, hello activity is not reported `EngagementPage` calls `StartActivity` inside its `OnNavigatedTo` method).</span></span> <span data-ttu-id="c535c-152">Isto é especialmente importante num projeto Windows Phone onde Olá predefinido modelo tem um `OnNavigatedTo` método.</span><span class="sxs-lookup"><span data-stu-id="c535c-152">This is especially important in a Windows Phone project where hello default template has an `OnNavigatedTo` method.</span></span>
>
> <span data-ttu-id="c535c-153">Para **aplicações universais do Windows 10**, utilizar o método de Olá recomendado na Olá "recomendado método: Sobrecarga as classes de página" secção [avançadas de relatórios com Olá SDK Windows Universal do aplicações Engagement](mobile-engagement-windows-store-advanced-reporting.md) , em vez de Olá um mencionados acima.</span><span class="sxs-lookup"><span data-stu-id="c535c-153">For **Windows 10 Universal apps**, use hello method recommended in hello "Recommended method: overload your Page classes" section of [Advanced Reporting with hello Windows Universal Apps Engagement SDK](mobile-engagement-windows-store-advanced-reporting.md), rather than hello one mentioned above.</span></span>

## <span data-ttu-id="c535c-154"><a id="monitor"></a>Ligar a aplicação com a monitorização em tempo real</span><span class="sxs-lookup"><span data-stu-id="c535c-154"><a id="monitor"></a>Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <span data-ttu-id="c535c-155"><a id="integrate-push"></a>Ativar as notificações push e mensagens na aplicação</span><span class="sxs-lookup"><span data-stu-id="c535c-155"><a id="integrate-push"></a>Enable push notifications and in-app messaging</span></span>
<span data-ttu-id="c535c-156">O Mobile Engagement permite-lhe toointeract e alcançar os seus utilizadores com notificações push e mensagens no contexto de Olá das campanhas na aplicação.</span><span class="sxs-lookup"><span data-stu-id="c535c-156">Mobile Engagement allows you toointeract and reach your users with push notifications and in-app messaging in hello context of campaigns.</span></span> <span data-ttu-id="c535c-157">Este módulo é designado alcance no portal de Mobile Engagement Olá.</span><span class="sxs-lookup"><span data-stu-id="c535c-157">This module is called REACH in hello Mobile Engagement portal.</span></span>
<span data-ttu-id="c535c-158">Olá secções seguintes configuram a aplicação tooreceive-los.</span><span class="sxs-lookup"><span data-stu-id="c535c-158">hello following sections set up your app tooreceive them.</span></span>

### <a name="enable-your-app-tooreceive-wns-push-notifications"></a><span data-ttu-id="c535c-159">Ativar a sua aplicação tooreceive notificações Push do WNS</span><span class="sxs-lookup"><span data-stu-id="c535c-159">Enable your app tooreceive WNS Push Notifications</span></span>
1. <span data-ttu-id="c535c-160">No Olá `Package.appxmanifest` ficheiro no Olá **aplicação** separador em **notificações**, defina **com capacidade de alerta:** demasiado**Sim**</span><span class="sxs-lookup"><span data-stu-id="c535c-160">In hello `Package.appxmanifest` file, in hello **Application** tab, under **Notifications**, set **Toast capable:** too**Yes**</span></span>

    ![][5]

### <a name="initialize-hello-reach-sdk"></a><span data-ttu-id="c535c-161">Inicializar Olá ALCANÇAR SDK</span><span class="sxs-lookup"><span data-stu-id="c535c-161">Initialize hello REACH SDK</span></span>
<span data-ttu-id="c535c-162">No `App.xaml.cs`, chamar **EngagementReach.Instance.Init(e);** no Olá **InitEngagement** função imediatamente após a inicialização do agente Olá:</span><span class="sxs-lookup"><span data-stu-id="c535c-162">In `App.xaml.cs`, call **EngagementReach.Instance.Init(e);** in hello **InitEngagement** function right after hello agent initialization:</span></span>

        private void InitEngagement(IActivatedEventArgs e)
        {
           EngagementAgent.Instance.Init(e);
           EngagementReach.Instance.Init(e);
        }

<span data-ttu-id="c535c-163">Está pronto toosend um alerta.</span><span class="sxs-lookup"><span data-stu-id="c535c-163">You're ready toosend a toast.</span></span> <span data-ttu-id="c535c-164">A seguir, vamos confirmar que realizou corretamente esta integração básica.</span><span class="sxs-lookup"><span data-stu-id="c535c-164">Next we verify that you have correctly carried out this basic integration.</span></span>

### <a name="grant-access-toomobile-engagement-toosend-notifications"></a><span data-ttu-id="c535c-165">Conceda acesso tooMobile Engagement toosend notificações</span><span class="sxs-lookup"><span data-stu-id="c535c-165">Grant access tooMobile Engagement toosend notifications</span></span>
1. <span data-ttu-id="c535c-166">Abra o [Dev Center da Loja Windows] no seu browser, inicie sessão e crie uma conta, se necessário.</span><span class="sxs-lookup"><span data-stu-id="c535c-166">Open [Windows Store Dev Center] in your web browser, login, and create an account if necessary.</span></span>
2. <span data-ttu-id="c535c-167">Clique em **Dashboard** Olá superior direita canto e, em seguida, clique em **criar uma nova aplicação** no menu de Olá painel esquerdo.</span><span class="sxs-lookup"><span data-stu-id="c535c-167">Click **Dashboard** at hello top right corner and then click **Create a new app** from hello left panel menu.</span></span>

    ![][9]
3. <span data-ttu-id="c535c-168">Crie a sua aplicação ao reservar o respetivo nome.</span><span class="sxs-lookup"><span data-stu-id="c535c-168">Create your app by reserving its name.</span></span>

    ![][10]
4. <span data-ttu-id="c535c-169">Quando tiver sido criada a aplicação Olá, navegue até demasiado**serviços -> notificações Push** no menu esquerdo Olá.</span><span class="sxs-lookup"><span data-stu-id="c535c-169">Once hello app has been created, navigate too**Services -> Push notifications** from hello left menu.</span></span>

    ![][11]
5. <span data-ttu-id="c535c-170">No Olá de secção notificações Push, clique em Olá **site dos Serviços Live** ligação.</span><span class="sxs-lookup"><span data-stu-id="c535c-170">In hello Push notifications section, click hello **Live Services site** link.</span></span>

    ![][12]
6. <span data-ttu-id="c535c-171">Navegue toohello secção de credenciais de Push.</span><span class="sxs-lookup"><span data-stu-id="c535c-171">You navigate toohello Push credentials section.</span></span> <span data-ttu-id="c535c-172">Certifique-se de que está em Olá **as definições de aplicação** secção e, em seguida, copie o **SID do pacote** e **segredo do cliente**</span><span class="sxs-lookup"><span data-stu-id="c535c-172">Make sure you are in hello **App Settings** section and then copy your **Package SID** and **Client secret**</span></span>

    ![][13]
7. <span data-ttu-id="c535c-173">Navegue toohello **definições** do portal do Mobile Engagement e clique em Olá **Push nativo** secção Olá esquerda.</span><span class="sxs-lookup"><span data-stu-id="c535c-173">Navigate toohello **Settings** of your Mobile Engagement portal, and click hello **Native Push** section on hello left.</span></span> <span data-ttu-id="c535c-174">Em seguida, clique em Olá **editar** botão tooenter sua **identificador de segurança do pacote (SID)** e os seus **chave secreta** conforme mostrado:</span><span class="sxs-lookup"><span data-stu-id="c535c-174">Then, click hello **Edit** button tooenter your **Package security identifier (SID)** and your **Secret Key** as shown:</span></span>

    ![][6]
8. <span data-ttu-id="c535c-175">Por fim, certifique-se de que associou a sua aplicação do Visual Studio a esta aplicação criada numa loja de aplicações de Olá.</span><span class="sxs-lookup"><span data-stu-id="c535c-175">Finally make sure that you have associated your Visual Studio app with this created app in hello App store.</span></span> <span data-ttu-id="c535c-176">Clique em **Associar a Aplicação à Loja** no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c535c-176">Click **Associate App with Store** in Visual Studio.</span></span>

    ![][7]

## <span data-ttu-id="c535c-177"><a id="send"></a>Enviar uma aplicação de tooyour de notificação</span><span class="sxs-lookup"><span data-stu-id="c535c-177"><a id="send"></a>Send a notification tooyour app</span></span>
[!INCLUDE [Create Windows Push campaign](../../includes/mobile-engagement-windows-push-campaign.md)]

<span data-ttu-id="c535c-178">Se estiver a executar a aplicação de Olá, verá uma notificação na aplicação.</span><span class="sxs-lookup"><span data-stu-id="c535c-178">If hello app is running, you see an in-app notification.</span></span> <span data-ttu-id="c535c-179">caso contrário, se a aplicação Olá estiver fechada, verá uma notificação de alerta.</span><span class="sxs-lookup"><span data-stu-id="c535c-179">otherwise if hello app is closed, you see a toast notification.</span></span>
<span data-ttu-id="c535c-180">Se vir uma notificação na aplicação, mas não uma notificação de alerta e Olá aplicação estiver a executar no modo de depuração no Visual Studio, em seguida, tente **eventos de ciclo de vida -> suspender** no Olá barra de ferramentas tooensure essa aplicação Olá é suspenso.</span><span class="sxs-lookup"><span data-stu-id="c535c-180">If you see an in-app notification but not a toast notification, and you are running hello app in debug mode in Visual Studio, then try **Lifecycle events -> Suspend** in hello toolbar tooensure that hello app is suspended.</span></span> <span data-ttu-id="c535c-181">Se clicou no botão de Home Olá durante a depuração da aplicação Olá no Visual Studio, em seguida, não fica sempre suspensa e consulte notificação Olá como na aplicação, não aparecer como uma notificação de alerta.</span><span class="sxs-lookup"><span data-stu-id="c535c-181">If you clicked hello Home button while debugging hello application in Visual Studio, then it doesn't always get suspended and while you see hello notification as in-app, it doesn't show up as a toast notification.</span></span>  

![][8]

<!-- URLs. -->
[Mobile Engagement Windows Universal SDK documentation]: ../mobile-engagement-windows-store-integrate-engagement/
[microsoftazure. Mobileengagement]: http://go.microsoft.com/?linkid=9864592
[Dev Center da Loja Windows]: https://dev.windows.com
[Windows Universal Apps - Overlay integration]: ../mobile-engagement-windows-store-integrate-engagement-reach/#overlay-integration

<!-- Images. -->
[1]: ./media/mobile-engagement-windows-store-dotnet-get-started/universal-app-creation.png
[2]: ./media/mobile-engagement-windows-store-dotnet-get-started/manifest-capabilities.png
[3]: ./media/mobile-engagement-windows-store-dotnet-get-started/add-connection-info.png
[5]: ./media/mobile-engagement-windows-store-dotnet-get-started/manifest-toast.png
[6]: ./media/mobile-engagement-windows-store-dotnet-get-started/enter-credentials.png
[7]: ./media/mobile-engagement-windows-store-dotnet-get-started/associate-app-store.png
[8]: ./media/mobile-engagement-windows-store-dotnet-get-started/vs-suspend.png
[9]: ./media/mobile-engagement-windows-store-dotnet-get-started/dashboard_create_app.png
[10]: ./media/mobile-engagement-windows-store-dotnet-get-started/dashboard_app_name.png
[11]: ./media/mobile-engagement-windows-store-dotnet-get-started/dashboard_services_push.png
[12]: ./media/mobile-engagement-windows-store-dotnet-get-started/dashboard_services_push_1.png
[13]: ./media/mobile-engagement-windows-store-dotnet-get-started/dashboard_services_push_creds.png
