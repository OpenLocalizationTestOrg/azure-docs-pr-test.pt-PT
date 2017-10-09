---
title: "notificações push aaaGeo-protegidos com Notification Hubs do Azure e dados geográficos do Bing | Microsoft Docs"
description: "Neste tutorial, ficará a saber como toodeliver baseada na localização push notificações com Notification Hubs do Azure e dados geográficos do Bing."
services: notification-hubs
documentationcenter: windows
keywords: "notificação push, notificação push"
author: dend
manager: yuaxu
editor: dend
ms.assetid: f41beea1-0d62-4418-9ffc-c9d70607a1b7
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 05/31/2016
ms.author: dendeli
ms.openlocfilehash: d6efe473537f2159240c53e780741f12619c045d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="geo-fenced-push-notifications-with-azure-notification-hubs-and-bing-spatial-data"></a><span data-ttu-id="93d29-104">Notificações push de perímetro geográfico com Notification Hubs do Azure e Dados Geográficos do Bing</span><span class="sxs-lookup"><span data-stu-id="93d29-104">Geo-fenced push notifications with Azure Notification Hubs and Bing Spatial Data</span></span>
> [!NOTE]
> <span data-ttu-id="93d29-105">toocomplete neste tutorial, tem de ter uma conta do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="93d29-105">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="93d29-106">Se não tiver uma conta, pode criar uma conta de avaliação gratuita em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="93d29-106">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="93d29-107">Para obter mais detalhes, consulte [Avaliação Gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02).</span><span class="sxs-lookup"><span data-stu-id="93d29-107">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02).</span></span>
> 
> 

<span data-ttu-id="93d29-108">Neste tutorial, ficará a saber como toodeliver baseada na localização push notificações com Notification Hubs do Azure e dados geográficos do Bing, alavancada numa aplicação plataforma Universal do Windows seio da.</span><span class="sxs-lookup"><span data-stu-id="93d29-108">In this tutorial, you will learn how toodeliver location-based push notifications with Azure Notification Hubs and Bing Spatial Data, leveraged from within a Universal Windows Platform application.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="93d29-109">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="93d29-109">Prerequisites</span></span>
<span data-ttu-id="93d29-110">Primeiro e mais importante, terá de toomake se de que tem todas as Olá software e o serviço de pré-requisitos:</span><span class="sxs-lookup"><span data-stu-id="93d29-110">First and foremost, you need toomake sure that you have all hello software and service pre-requisites:</span></span>

* <span data-ttu-id="93d29-111">[Visual Studio 2015 Update 1](https://www.visualstudio.com/en-us/downloads/download-visual-studio-vs.aspx) ou posterior (a [Edição Community](https://go.microsoft.com/fwlink/?LinkId=691978&clcid=0x409) também serve).</span><span class="sxs-lookup"><span data-stu-id="93d29-111">[Visual Studio 2015 Update 1](https://www.visualstudio.com/en-us/downloads/download-visual-studio-vs.aspx) or later ([Community Edition](https://go.microsoft.com/fwlink/?LinkId=691978&clcid=0x409) will do as well).</span></span> 
* <span data-ttu-id="93d29-112">Versão mais recente do Olá [Azure SDK](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="93d29-112">Latest version of hello [Azure SDK](https://azure.microsoft.com/downloads/).</span></span> 
* <span data-ttu-id="93d29-113">[Conta do Dev Center do Bing Maps](https://www.bingmapsportal.com/) (pode criar uma gratuitamente e associá-la à conta Microsoft).</span><span class="sxs-lookup"><span data-stu-id="93d29-113">[Bing Maps Dev Center account](https://www.bingmapsportal.com/) (you can create one for free and associate it with your Microsoft account).</span></span> 

## <a name="getting-started"></a><span data-ttu-id="93d29-114">Introdução</span><span class="sxs-lookup"><span data-stu-id="93d29-114">Getting Started</span></span>
<span data-ttu-id="93d29-115">Vamos começar por criar o projeto de Olá.</span><span class="sxs-lookup"><span data-stu-id="93d29-115">Let’s start by creating hello project.</span></span> <span data-ttu-id="93d29-116">No Visual Studio, inicie um novo projeto do tipo **Aplicação em Branco (Universal Windows)**.</span><span class="sxs-lookup"><span data-stu-id="93d29-116">In Visual Studio, start a new project of type **Blank App (Universal Windows)**.</span></span>

![](./media/notification-hubs-geofence/notification-hubs-create-blank-app.png)

<span data-ttu-id="93d29-117">Depois de concluída a criação do projeto Olá, deve ter o escudo Olá para aplicação Olá em si.</span><span class="sxs-lookup"><span data-stu-id="93d29-117">Once hello project creation is complete, you should have hello harness for hello app itself.</span></span> <span data-ttu-id="93d29-118">Agora vamos configurar tudo para a infraestrutura de geométrico Olá.</span><span class="sxs-lookup"><span data-stu-id="93d29-118">Now let’s set up everything for hello geo-fencing infrastructure.</span></span> <span data-ttu-id="93d29-119">Uma vez que estamos toouse que serviços Bing para isto, existe é um ponto de final público REST API que nos permite molduras de localização específicas tooquery:</span><span class="sxs-lookup"><span data-stu-id="93d29-119">Because we are going toouse Bing services for this, there is a public REST API endpoint that allows us tooquery specific location frames:</span></span>

    http://spatial.virtualearth.net/REST/v1/data/

<span data-ttu-id="93d29-120">Terá de toospecify Olá os seguintes parâmetros tooget funcionar:</span><span class="sxs-lookup"><span data-stu-id="93d29-120">You will need toospecify hello following parameters tooget it working:</span></span>

* <span data-ttu-id="93d29-121">**ID da Origem de Dados** e **Nome da Origem de Dados** – na API Bing Maps, origens de dados contêm vários metadados agrupados, como localizações e horas de expediente da operação.</span><span class="sxs-lookup"><span data-stu-id="93d29-121">**Data Source ID** and **Data Source Name** – in Bing Maps API, data sources contain various bucketed metadata, such as locations and business hours of operation.</span></span> <span data-ttu-id="93d29-122">Pode ler mais acerca deles aqui.</span><span class="sxs-lookup"><span data-stu-id="93d29-122">You can read more about those here.</span></span> 
* <span data-ttu-id="93d29-123">**Nome da entidade** – Olá entidade que pretende toouse como um ponto de referência para notificação de Olá.</span><span class="sxs-lookup"><span data-stu-id="93d29-123">**Entity Name** – hello entity you want toouse as a reference point for hello notification.</span></span> 
* <span data-ttu-id="93d29-124">**Chave de API do Bing Maps** – esta é Olá chave que obteve anteriormente quando criou a conta do Dev Center do Bing Olá.</span><span class="sxs-lookup"><span data-stu-id="93d29-124">**Bing Maps API Key** – this is hello key that you obtained earlier when you created hello Bing Dev Center account.</span></span>

<span data-ttu-id="93d29-125">Vamos fazer uma descrição profunda na configuração de Olá para cada um dos elementos de Olá acima.</span><span class="sxs-lookup"><span data-stu-id="93d29-125">Let’s do a deep-dive on hello setup for each of hello elements above.</span></span>

## <a name="setting-up-hello-data-source"></a><span data-ttu-id="93d29-126">Configurar a origem de dados de Olá</span><span class="sxs-lookup"><span data-stu-id="93d29-126">Setting up hello data source</span></span>
<span data-ttu-id="93d29-127">Pode fazê-lo no Olá Dev Center do Bing Maps.</span><span class="sxs-lookup"><span data-stu-id="93d29-127">You can do it in hello Bing Maps Dev Center.</span></span> <span data-ttu-id="93d29-128">Basta clicar em **origens de dados** no Olá barra navegação superior e selecione **gerir origens de dados**.</span><span class="sxs-lookup"><span data-stu-id="93d29-128">Simply click on **Data sources** in hello top navigation bar and select **Manage Data Sources**.</span></span>

![](./media/notification-hubs-geofence/bing-maps-manage-data.png)

<span data-ttu-id="93d29-129">Se não já trabalhou com a Bing Maps API, provavelmente não existir origens de dados presentes, para que apenas possa criar uma nova clicando na origem de dados do carregamento de dados tooa.</span><span class="sxs-lookup"><span data-stu-id="93d29-129">If you have not worked with Bing Maps API before, most likely there won’t be any data sources present, so you can just create a new one by clicking on Upload data tooa data source.</span></span> <span data-ttu-id="93d29-130">Certifique-se de que preenche todos os campos de Olá necessário:</span><span class="sxs-lookup"><span data-stu-id="93d29-130">Make sure you fill out all hello required fields:</span></span>

![](./media/notification-hubs-geofence/bing-maps-create-data.png)

<span data-ttu-id="93d29-131">Poderá estar a pensar – o que é o ficheiro de dados de Olá e o que deve estar carregar?</span><span class="sxs-lookup"><span data-stu-id="93d29-131">You might be wondering – what is hello data file and what should you be uploading?</span></span> <span data-ttu-id="93d29-132">Para efeitos de Olá deste teste, podemos utilizar simplesmente amostra de Olá baseada em pipe que enquadra uma área da marítima de frente são Francisco Olá:</span><span class="sxs-lookup"><span data-stu-id="93d29-132">For hello purposes of this test, we can just use hello sample pipe-based that frames an area of hello San Francisco waterfront:</span></span>

    Bing Spatial Data Services, 1.0, TestBoundaries
    EntityID(Edm.String,primaryKey)|Name(Edm.String)|Longitude(Edm.Double)|Latitude(Edm.Double)|Boundary(Edm.Geography)
    1|SanFranciscoPier|||POLYGON ((-122.389825 37.776598,-122.389438 37.773087,-122.381885 37.771849,-122.382186 37.777022,-122.389825 37.776598))

<span data-ttu-id="93d29-133">Olá acima representa esta entidade:</span><span class="sxs-lookup"><span data-stu-id="93d29-133">hello above represents this entity:</span></span>

![](./media/notification-hubs-geofence/bing-maps-geofence.png)

<span data-ttu-id="93d29-134">Basta copiar e colar a cadeia de Olá acima para um novo ficheiro e guarde-o como **Notificationhubsgeofence**e carregá-lo no Olá Dev Center do Bing.</span><span class="sxs-lookup"><span data-stu-id="93d29-134">Simply copy and paste hello string above into a new file and save it as **NotificationHubsGeofence.pipe**, and upload it in hello Bing Dev Center.</span></span>

> [!NOTE]
> <span data-ttu-id="93d29-135">Poderá ser toospecify que lhes é pedida uma nova chave para Olá **chave mestra** que é diferente do Olá **chave de consulta**.</span><span class="sxs-lookup"><span data-stu-id="93d29-135">You might be prompted toospecify a new key for hello **Master Key** that is different from hello **Query Key**.</span></span> <span data-ttu-id="93d29-136">Crie simplesmente uma nova chave através do dashboard e atualize Olá dados origem carregamento de página Olá.</span><span class="sxs-lookup"><span data-stu-id="93d29-136">Simply create a new key through hello dashboard and refresh hello data source upload page.</span></span>
> 
> 

<span data-ttu-id="93d29-137">Depois de carregar o ficheiro de dados de Olá, terá de certificar-se de que pode publicar a origem de dados de Olá toomake.</span><span class="sxs-lookup"><span data-stu-id="93d29-137">Once you upload hello data file, you will need toomake sure that you publish hello data source.</span></span> 

<span data-ttu-id="93d29-138">Aceda demasiado**gerir origens de dados**, como fizemos acima, localize a origem de dados na lista de Olá e clique em **publicar** no Olá **ações** coluna.</span><span class="sxs-lookup"><span data-stu-id="93d29-138">Go too**Manage Data Sources**, just like we did above, find your data source in hello list and click on **Publish** in hello **Actions** column.</span></span> <span data-ttu-id="93d29-139">Em mais um pouco, deverá ver a origem de dados no Olá **origens de dados publicados** separador:</span><span class="sxs-lookup"><span data-stu-id="93d29-139">In a bit, you should see your data source in hello **Published Data Sources** tab:</span></span>

![](./media/notification-hubs-geofence/bing-maps-published-data.png)

<span data-ttu-id="93d29-140">Se clicar em **editar**, será capaz de toosee rapidamente as localizações que introduzimos:</span><span class="sxs-lookup"><span data-stu-id="93d29-140">If you click **Edit**, you will be able toosee at a glance what locations we introduced in it:</span></span>

![](./media/notification-hubs-geofence/bing-maps-data-details.png)

<span data-ttu-id="93d29-141">Neste momento, Olá portal não mostra Olá limites para Olá geográfico que criámos – precisamos apenas é uma confirmação de que a localização de Olá especificada está na vizinhança certa Olá.</span><span class="sxs-lookup"><span data-stu-id="93d29-141">At this point, hello portal does not show you hello boundaries for hello geofence that we created – all we need is a confirmation that hello location specified is in hello right vicinity.</span></span>

<span data-ttu-id="93d29-142">Agora, tem de todos os requisitos de Olá Olá origem de dados.</span><span class="sxs-lookup"><span data-stu-id="93d29-142">Now you have all hello requirements for hello data source.</span></span> <span data-ttu-id="93d29-143">Clique em detalhes de Olá tooget no URL do pedido Olá para chamada Olá API, no Dev Center do Bing Maps, de Olá **origens de dados** e selecione **informações da origem de dados**.</span><span class="sxs-lookup"><span data-stu-id="93d29-143">tooget hello details on hello request URL for hello API call, in hello Bing Maps Dev Center, click **Data sources** and select **Data Source Information**.</span></span>

![](./media/notification-hubs-geofence/bing-maps-data-info.png)

<span data-ttu-id="93d29-144">Olá **URL da consulta** é o que procuramos aqui.</span><span class="sxs-lookup"><span data-stu-id="93d29-144">hello **Query URL** is what we’re after here.</span></span> <span data-ttu-id="93d29-145">Este é o ponto final de Olá relativamente ao qual podemos executar consultas toocheck se Olá dispositivo não estiver atualmente dentro dos limites de Olá de uma localização ou não.</span><span class="sxs-lookup"><span data-stu-id="93d29-145">This is hello endpoint against which we can execute queries toocheck whether hello device is currently within hello boundaries of a location or not.</span></span> <span data-ttu-id="93d29-146">tooperform esta verificação, precisamos simplesmente tooexecute uma ação obter chamar contra o URL da consulta Olá, com Olá seguir os parâmetros anexados:</span><span class="sxs-lookup"><span data-stu-id="93d29-146">tooperform this check, we simply need tooexecute a GET call against hello query URL, with hello following parameters appended:</span></span>

    ?spatialFilter=intersects(%27POINT%20LONGITUDE%20LATITUDE)%27)&$format=json&key=QUERY_KEY

<span data-ttu-id="93d29-147">Dessa forma, a especificar um ponto de destino que obtemos do dispositivo Olá e Bing Maps efetuará automaticamente Olá cálculos toosee se está dentro do perímetro geográfico de Olá.</span><span class="sxs-lookup"><span data-stu-id="93d29-147">That way you're specifying a target point that we obtain from hello device and Bing Maps will automatically perform hello calculations toosee whether it is within hello geofence.</span></span> <span data-ttu-id="93d29-148">Depois de executar o pedido de Olá através de um browser (ou cURL), irá obter padrão uma resposta JSON:</span><span class="sxs-lookup"><span data-stu-id="93d29-148">Once you execute hello request through a browser (or cURL), you will get standard a JSON response:</span></span>

![](./media/notification-hubs-geofence/bing-maps-json.png)

<span data-ttu-id="93d29-149">Esta resposta só aparece quando o ponto de Olá, na verdade, está dentro do Olá designado limites.</span><span class="sxs-lookup"><span data-stu-id="93d29-149">This response only happens when hello point is actually within hello designated boundaries.</span></span> <span data-ttu-id="93d29-150">Se não estiver, obterá um registo de **resultados** vazio:</span><span class="sxs-lookup"><span data-stu-id="93d29-150">If it is not, you will get an empty **results** bucket:</span></span>

![](./media/notification-hubs-geofence/bing-maps-nores.png)

## <a name="setting-up-hello-uwp-application"></a><span data-ttu-id="93d29-151">Configurar a aplicação de UWP Olá</span><span class="sxs-lookup"><span data-stu-id="93d29-151">Setting up hello UWP application</span></span>
<span data-ttu-id="93d29-152">Agora que temos a origem de dados de Olá pronta, podemos começar a trabalhar no Olá aplicação UWP de que fizemos anteriormente.</span><span class="sxs-lookup"><span data-stu-id="93d29-152">Now that we have hello data source ready, we can start working on hello UWP application that we bootstrapped earlier.</span></span>

<span data-ttu-id="93d29-153">Primeiro e mais importante, temos de ativar os serviços de localização para a nossa aplicação.</span><span class="sxs-lookup"><span data-stu-id="93d29-153">First and foremost, we must enable location services for our application.</span></span> <span data-ttu-id="93d29-154">toodo, faça duplo clique no `Package.appxmanifest` ficheiros **Explorador de soluções**.</span><span class="sxs-lookup"><span data-stu-id="93d29-154">toodo this, double-click on `Package.appxmanifest` file in **Solution Explorer**.</span></span>

![](./media/notification-hubs-geofence/vs-package-manifest.png)

<span data-ttu-id="93d29-155">No Olá separador Propriedades pacote que acabou de abrir, clique em **capacidades** e certifique-se de que seleciona **localização**:</span><span class="sxs-lookup"><span data-stu-id="93d29-155">In hello package properties tab that just opened, click on **Capabilities** and make sure that you select **Location**:</span></span>

![](./media/notification-hubs-geofence/vs-package-location.png)

<span data-ttu-id="93d29-156">Como Olá capacidade de localização é declarada, crie uma nova pasta na solução com o nome `Core`e adicione um novo ficheiro dentro da mesma, denominado `LocationHelper.cs`:</span><span class="sxs-lookup"><span data-stu-id="93d29-156">As hello location capability is declared, create a new folder in your solution named `Core`, and add a new file within it, called `LocationHelper.cs`:</span></span>

![](./media/notification-hubs-geofence/vs-location-helper.png)

<span data-ttu-id="93d29-157">Olá `LocationHelper` classe em si é bastante básica nesta fase – tudo o que faz é permitir-na localização do utilizador Olá tooobtain através do sistema de Olá API:</span><span class="sxs-lookup"><span data-stu-id="93d29-157">hello `LocationHelper` class itself is fairly basic at this point – all it does is allow us tooobtain hello user location through hello system API:</span></span>

    using System;
    using System.Threading.Tasks;
    using Windows.Devices.Geolocation;

    namespace NotificationHubs.Geofence.Core
    {
        public class LocationHelper
        {
            private static readonly uint AppDesiredAccuracyInMeters = 10;

            public async static Task<Geoposition> GetCurrentLocation()
            {
                var accessStatus = await Geolocator.RequestAccessAsync();
                switch (accessStatus)
                {
                    case GeolocationAccessStatus.Allowed:
                        {
                            Geolocator geolocator = new Geolocator { DesiredAccuracyInMeters = AppDesiredAccuracyInMeters };

                            return await geolocator.GetGeopositionAsync();
                        }
                    default:
                        {
                            return null;
                        }
                }
            }

        }
    }

<span data-ttu-id="93d29-158">Pode ler mais sobre como obter Olá localização do utilizador em aplicações UWP no oficial Olá [documento MSDN](https://msdn.microsoft.com/library/windows/apps/mt219698.aspx).</span><span class="sxs-lookup"><span data-stu-id="93d29-158">You can read more about getting hello user’s location in UWP apps in hello official [MSDN document](https://msdn.microsoft.com/library/windows/apps/mt219698.aspx).</span></span>

<span data-ttu-id="93d29-159">toocheck aquisição de localização de Olá, na verdade, está a funcionar, abra o lado de código de Olá da sua página principal (`MainPage.xaml.cs`).</span><span class="sxs-lookup"><span data-stu-id="93d29-159">toocheck that hello location acquisition is actually working, open hello code side of your main page (`MainPage.xaml.cs`).</span></span> <span data-ttu-id="93d29-160">Crie um processador de eventos para Olá `Loaded` evento no Olá `MainPage` construtor:</span><span class="sxs-lookup"><span data-stu-id="93d29-160">Create a new event handler for hello `Loaded` event in hello `MainPage` constructor:</span></span>

    public MainPage()
    {
        this.InitializeComponent();
        this.Loaded += MainPage_Loaded;
    }

<span data-ttu-id="93d29-161">implementação de Olá de processador de eventos de Olá é o seguinte:</span><span class="sxs-lookup"><span data-stu-id="93d29-161">hello implementation of hello event handler is as follows:</span></span>

    private async void MainPage_Loaded(object sender, RoutedEventArgs e)
    {
        var location = await LocationHelper.GetCurrentLocation();

        if (location != null)
        {
            Debug.WriteLine(string.Concat(location.Coordinate.Longitude,
                " ", location.Coordinate.Latitude));
        }
    }

<span data-ttu-id="93d29-162">Repare que declarámos Olá processador como assíncrono porque `GetCurrentLocation` é passível de espera e necessita, por conseguinte, toobe executado num contexto assíncrono.</span><span class="sxs-lookup"><span data-stu-id="93d29-162">Notice that we declared hello handler as async because `GetCurrentLocation` is awaitable, and therefore requires toobe executed in an async context.</span></span> <span data-ttu-id="93d29-163">Além disso, porque em determinadas circunstâncias poderá ficar com uma localização nula (por exemplo, os serviços de localização de Olá estão desativados ou aplicações Olá foi negada a localização de tooaccess de permissões), é necessário toomake certificar-se de que é corretamente processada com uma verificação nula.</span><span class="sxs-lookup"><span data-stu-id="93d29-163">Also, because under certain circumstances we might end up with a null location (e.g. hello location services are disabled or hello application was denied permissions tooaccess location), we need toomake sure that it is properly handled with a null check.</span></span>

<span data-ttu-id="93d29-164">Execute a aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="93d29-164">Run hello application.</span></span> <span data-ttu-id="93d29-165">Certifique-se de que permite o acesso de localização:</span><span class="sxs-lookup"><span data-stu-id="93d29-165">Make sure you allow location access:</span></span>

![](./media/notification-hubs-geofence/notification-hubs-location-access.png)

<span data-ttu-id="93d29-166">Olá, uma vez iniciada aplicação, deve ser capaz de toosee Olá coordenadas no Olá **saída** janela:</span><span class="sxs-lookup"><span data-stu-id="93d29-166">Once hello application launches, you should be able toosee hello coordinates in hello **Output** window:</span></span>

![](./media/notification-hubs-geofence/notification-hubs-location-output.png)

<span data-ttu-id="93d29-167">Agora, sabe que funciona de aquisição de localização – sentir processador de eventos de teste de Olá tooremove livre para carregado porque que não será possível utilizá-lo.</span><span class="sxs-lookup"><span data-stu-id="93d29-167">Now you know that location acquisition works – feel free tooremove hello test event handler for Loaded because we won’t be using it anymore.</span></span>

<span data-ttu-id="93d29-168">Olá passo seguinte consiste em toocapture alterações de localização.</span><span class="sxs-lookup"><span data-stu-id="93d29-168">hello next step is toocapture location changes.</span></span> <span data-ttu-id="93d29-169">Para isso, vamos back toohello `LocationHelper` classe e adicione o processador de eventos de Olá para `PositionChanged`:</span><span class="sxs-lookup"><span data-stu-id="93d29-169">For that, let’s go back toohello `LocationHelper` class and add hello event handler for `PositionChanged`:</span></span>

    geolocator.PositionChanged += Geolocator_PositionChanged;

<span data-ttu-id="93d29-170">implementação de Olá irá mostrar coordenadas de localização de Olá no Olá **saída** janela:</span><span class="sxs-lookup"><span data-stu-id="93d29-170">hello implementation will show hello location coordinates in hello **Output** window:</span></span>

    private static async void Geolocator_PositionChanged(Geolocator sender, PositionChangedEventArgs args)
    {
        await CoreApplication.MainView.CoreWindow.Dispatcher.RunAsync(CoreDispatcherPriority.Normal, () =>
        {
            Debug.WriteLine(string.Concat(args.Position.Coordinate.Longitude, " ", args.Position.Coordinate.Latitude));
        });
    }

## <a name="setting-up-hello-backend"></a><span data-ttu-id="93d29-171">Configurar o back-end de Olá</span><span class="sxs-lookup"><span data-stu-id="93d29-171">Setting up hello backend</span></span>
<span data-ttu-id="93d29-172">Transferir Olá [exemplo de back-end do .NET a partir do GitHub](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/NotifyUsers).</span><span class="sxs-lookup"><span data-stu-id="93d29-172">Download hello [.NET Backend Sample from GitHub](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/NotifyUsers).</span></span> <span data-ttu-id="93d29-173">Uma vez concluída a transferência de Olá, abra Olá `NotifyUsers` pasta e, subsequentemente, Olá `NotifyUsers.sln` ficheiro.</span><span class="sxs-lookup"><span data-stu-id="93d29-173">Once hello download completes, open hello `NotifyUsers` folder, and subsequently – hello `NotifyUsers.sln` file.</span></span>

<span data-ttu-id="93d29-174">Conjunto Olá `AppBackend` projeto como Olá **projeto de arranque** e inicie.</span><span class="sxs-lookup"><span data-stu-id="93d29-174">Set hello `AppBackend` project as hello **StartUp Project** and launch it.</span></span>

![](./media/notification-hubs-geofence/vs-startup-project.png)

<span data-ttu-id="93d29-175">Olá projeto já está configurado toosend push notificações tootarget dispositivos, pelo que precisamos toodo apenas duas coisas – trocar a cadeia de ligação correta Olá para o hub de notificação de Olá e adicionar a notificação de Olá de toosend do limite identificação apenas quando hello utilizador está dentro do perímetro geográfico de Olá.</span><span class="sxs-lookup"><span data-stu-id="93d29-175">hello project is already configured toosend push notifications tootarget devices, so we’ll need toodo only two things – swap out hello right connection string for hello notification hub and add boundary identification toosend hello notification only when hello user is within hello geofence.</span></span>

<span data-ttu-id="93d29-176">tooconfigure Olá cadeia de ligação, Olá `Models` pasta abra `Notifications.cs`.</span><span class="sxs-lookup"><span data-stu-id="93d29-176">tooconfigure hello connection string, in hello `Models` folder open `Notifications.cs`.</span></span> <span data-ttu-id="93d29-177">Olá `NotificationHubClient.CreateClientFromConnectionString` função deve conter informações de Olá acerca do notification hub que pode obter no Olá [Portal do Azure](https://portal.azure.com) (procure dentro Olá **políticas de acesso** painel no  **Definições**).</span><span class="sxs-lookup"><span data-stu-id="93d29-177">hello `NotificationHubClient.CreateClientFromConnectionString` function should contain hello information about your notification hub that you can get in hello [Azure Portal](https://portal.azure.com) (look inside hello **Access Policies** blade in **Settings**).</span></span> <span data-ttu-id="93d29-178">Guarde o ficheiro de configuração atualizada Olá.</span><span class="sxs-lookup"><span data-stu-id="93d29-178">Save hello updated configuration file.</span></span>

<span data-ttu-id="93d29-179">Agora precisamos toocreate um modelo para Olá resultado de API do Bing Maps.</span><span class="sxs-lookup"><span data-stu-id="93d29-179">Now we need toocreate a model for hello Bing Maps API result.</span></span> <span data-ttu-id="93d29-180">Olá toodo de forma mais fácil que é o botão direito no Olá `Models` pasta, **adicionar** > **classe**.</span><span class="sxs-lookup"><span data-stu-id="93d29-180">hello easiest way toodo that is right-click on hello `Models` folder, **Add** > **Class**.</span></span> <span data-ttu-id="93d29-181">Dê-lhe o nome `GeofenceBoundary.cs`.</span><span class="sxs-lookup"><span data-stu-id="93d29-181">Name it `GeofenceBoundary.cs`.</span></span> <span data-ttu-id="93d29-182">Quando tiver terminado, copie Olá JSON da resposta de Olá API que discutimos na primeira secção de Olá e no Visual Studio, utilize **editar** > **Colar especial** > **colar JSON como Classes**.</span><span class="sxs-lookup"><span data-stu-id="93d29-182">Once done, copy hello JSON from hello API response that we discussed in hello first section and in Visual Studio use **Edit** > **Paste Special** > **Paste JSON as Classes**.</span></span> 

<span data-ttu-id="93d29-183">Dessa forma, certifique-se esse objeto Olá será possível anular a serialização exatamente tal como era destinado.</span><span class="sxs-lookup"><span data-stu-id="93d29-183">That way we ensure that hello object will be deserialized exactly as it was intended.</span></span> <span data-ttu-id="93d29-184">O conjunto de classes resultante deve assemelhar-se a isto:</span><span class="sxs-lookup"><span data-stu-id="93d29-184">Your resulting class set should resemble this:</span></span>

    namespace AppBackend.Models
    {
        public class Rootobject
        {
            public D d { get; set; }
        }

        public class D
        {
            public string __copyright { get; set; }
            public Result[] results { get; set; }
        }

        public class Result
        {
            public __Metadata __metadata { get; set; }
            public string EntityID { get; set; }
            public string Name { get; set; }
            public float Longitude { get; set; }
            public float Latitude { get; set; }
            public string Boundary { get; set; }
            public string Confidence { get; set; }
            public string Locality { get; set; }
            public string AddressLine { get; set; }
            public string AdminDistrict { get; set; }
            public string CountryRegion { get; set; }
            public string PostalCode { get; set; }
        }

        public class __Metadata
        {
            public string uri { get; set; }
        }
    }

<span data-ttu-id="93d29-185">Em seguida, abra `Controllers` > `NotificationsController.cs`.</span><span class="sxs-lookup"><span data-stu-id="93d29-185">Next, open `Controllers` > `NotificationsController.cs`.</span></span> <span data-ttu-id="93d29-186">É necessário tootweak Olá Post chamada tooaccount de latitude e longitude do destino de Olá.</span><span class="sxs-lookup"><span data-stu-id="93d29-186">We need tootweak hello Post call tooaccount for hello target longitude and latitude.</span></span> <span data-ttu-id="93d29-187">Para tal, adicione simplesmente assinatura de função de toohello de duas cadeias – `latitude` e `longitude`.</span><span class="sxs-lookup"><span data-stu-id="93d29-187">For that, simply add two strings toohello function signature – `latitude` and `longitude`.</span></span>

    public async Task<HttpResponseMessage> Post(string pns, [FromBody]string message, string to_tag, string latitude, string longitude)

<span data-ttu-id="93d29-188">Criar uma nova classe no projeto Olá designado `ApiHelper.cs` – vamos utilizá-lo intersecções de limites do tooconnect tooBing toocheck ponto.</span><span class="sxs-lookup"><span data-stu-id="93d29-188">Create a new class within hello project called `ApiHelper.cs` – we’ll use it tooconnect tooBing toocheck point boundary intersections.</span></span> <span data-ttu-id="93d29-189">Implemente uma função `IsPointWithinBounds`, como esta:</span><span class="sxs-lookup"><span data-stu-id="93d29-189">Implement a `IsPointWithinBounds` function, like this:</span></span>

    public class ApiHelper
    {
        public static readonly string ApiEndpoint = "{YOUR_QUERY_ENDPOINT}?spatialFilter=intersects(%27POINT%20({0}%20{1})%27)&$format=json&key={2}";
        public static readonly string ApiKey = "{YOUR_API_KEY}";

        public static bool IsPointWithinBounds(string longitude,string latitude)
        {
            var json = new WebClient().DownloadString(string.Format(ApiEndpoint, longitude, latitude, ApiKey));
            var result = JsonConvert.DeserializeObject<Rootobject>(json);
            if (result.d.results != null && result.d.results.Count() > 0)
            {
                return true;
            }
            else
            {
                return false;
            }
        }
    }

> [!NOTE]
> <span data-ttu-id="93d29-190">Certifique-se de que toosubstitute, ponto final de Olá API, com o URL da consulta Olá que obteve anteriormente do Olá Dev Center do Bing (mesmo se aplica a chave de API de toohello).</span><span class="sxs-lookup"><span data-stu-id="93d29-190">Make sure toosubstitute hello API endpoint with hello query URL that you obtained earlier from hello Bing Dev Center (same applies toohello API key).</span></span> 
> 
> 

<span data-ttu-id="93d29-191">Se existirem consulta toohello de resultados, o que significa que Olá ponto especificado está dentro do Olá dos limites do perímetro geográfico de Olá, voltamos `true`.</span><span class="sxs-lookup"><span data-stu-id="93d29-191">If there are results toohello query, that means that hello specified point is within hello boundaries of hello geofence, so we return `true`.</span></span> <span data-ttu-id="93d29-192">Se não existirem resultados, Bing é informar-nos que o ponto de Olá está fora do intervalo de pesquisa de Olá, voltamos `false`.</span><span class="sxs-lookup"><span data-stu-id="93d29-192">If there are no results, Bing is telling us that hello point is outside hello lookup frame, so we return `false`.</span></span>

<span data-ttu-id="93d29-193">Novamente no `NotificationsController.cs`, crie uma verificação mesmo antes da instrução Olá:</span><span class="sxs-lookup"><span data-stu-id="93d29-193">Back in `NotificationsController.cs`, create a check right before hello switch statement:</span></span>

    if (ApiHelper.IsPointWithinBounds(longitude, latitude))
    {
        switch (pns.ToLower())
        {
            case "wns":
                //// Windows 8.1 / Windows Phone 8.1
                var toast = @"<toast><visual><binding template=""ToastText01""><text id=""1"">" +
                            "From " + user + ": " + message + "</text></binding></visual></toast>";
                outcome = await Notifications.Instance.Hub.SendWindowsNativeNotificationAsync(toast, userTag);

                // Windows 10 specific Action Center support
                toast = @"<toast><visual><binding template=""ToastGeneric""><text id=""1"">" +
                            "From " + user + ": " + message + "</text></binding></visual></toast>";
                outcome = await Notifications.Instance.Hub.SendWindowsNativeNotificationAsync(toast, userTag);

                break;
        }
    }

<span data-ttu-id="93d29-194">Dessa forma, Olá notificação é apenas enviada quando o ponto de Olá está dentro dos limites de Olá.</span><span class="sxs-lookup"><span data-stu-id="93d29-194">That way, hello notification is only sent when hello point is within hello boundaries.</span></span>

## <a name="testing-push-notifications-in-hello-uwp-app"></a><span data-ttu-id="93d29-195">Testar notificações push na aplicação UWP Olá</span><span class="sxs-lookup"><span data-stu-id="93d29-195">Testing push notifications in hello UWP app</span></span>
<span data-ttu-id="93d29-196">Retroceder toohello aplicação UWP, deverá ser agora tootest capaz de notificações.</span><span class="sxs-lookup"><span data-stu-id="93d29-196">Going back toohello UWP app, we should now be able tootest notifications.</span></span> <span data-ttu-id="93d29-197">Dentro do Olá `LocationHelper` classe, crie uma nova função – `SendLocationToBackend`:</span><span class="sxs-lookup"><span data-stu-id="93d29-197">Within hello `LocationHelper` class, create a new function – `SendLocationToBackend`:</span></span>

    public static async Task SendLocationToBackend(string pns, string userTag, string message, string latitude, string longitude)
    {
        var POST_URL = "http://localhost:8741/api/notifications?pns=" +
            pns + "&to_tag=" + userTag + "&latitude=" + latitude + "&longitude=" + longitude;

        using (var httpClient = new HttpClient())
        {
            try
            {
                await httpClient.PostAsync(POST_URL, new StringContent("\"" + message + "\"",
                    System.Text.Encoding.UTF8, "application/json"));
            }
            catch (Exception ex)
            {
                Debug.WriteLine(ex.Message);
            }
        }
    }

> [!NOTE]
> <span data-ttu-id="93d29-198">Comutação Olá `POST_URL` toohello localização da sua aplicação web implementada que criámos na secção anterior Olá.</span><span class="sxs-lookup"><span data-stu-id="93d29-198">Swap hello `POST_URL` toohello location of your deployed web application that we created in hello previous section.</span></span> <span data-ttu-id="93d29-199">Por agora, está OK toorun-la localmente, mas à medida que trabalha na implementação de uma versão pública, será necessário toohost-o com um fornecedor externo.</span><span class="sxs-lookup"><span data-stu-id="93d29-199">For now, it’s OK toorun it locally, but as you work on deploying a public version, you will need toohost it with an external provider.</span></span>
> 
> 

<span data-ttu-id="93d29-200">Vamos agora garantir que registamos a aplicação UWP Olá para notificações push.</span><span class="sxs-lookup"><span data-stu-id="93d29-200">Let’s now make sure that we register hello UWP app for push notifications.</span></span> <span data-ttu-id="93d29-201">No Visual Studio, clique em **projeto** > **armazenar** > **associar aplicação à loja Olá**.</span><span class="sxs-lookup"><span data-stu-id="93d29-201">In Visual Studio, click on **Project** > **Store** > **Associate app with hello store**.</span></span>

![](./media/notification-hubs-geofence/vs-associate-with-store.png)

<span data-ttu-id="93d29-202">Depois de iniciar sessão na conta de programador tooyour, certifique-se de que seleciona uma aplicação existente ou crie um novo e associa pacote Olá com o mesmo.</span><span class="sxs-lookup"><span data-stu-id="93d29-202">Once you sign in tooyour developer account, make sure you select an existing app or create a new one and associate hello package with it.</span></span> 

<span data-ttu-id="93d29-203">Vá toohello Dev Center e abra Olá aplicação que acabou de criar.</span><span class="sxs-lookup"><span data-stu-id="93d29-203">Go toohello Dev Center and open hello app that you just created.</span></span> <span data-ttu-id="93d29-204">Clique em **Serviços** > **Notificações Push** > **Site dos Serviços Live**.</span><span class="sxs-lookup"><span data-stu-id="93d29-204">Click **Services** > **Push Notifications** > **Live Services site**.</span></span>

![](./media/notification-hubs-geofence/ms-live-services.png)

<span data-ttu-id="93d29-205">No site de Olá, tome nota do Olá **segredo da aplicação** e Olá **SID do pacote**.</span><span class="sxs-lookup"><span data-stu-id="93d29-205">On hello site, take note of hello **Application Secret** and hello **Package SID**.</span></span> <span data-ttu-id="93d29-206">Terá de ambos no Portal do Azure – de Olá, abra o notification hub, clique em **definições** > **serviços de notificação** > **Windows (WNS)**e introduza as informações de Olá nos campos de Olá necessário.</span><span class="sxs-lookup"><span data-stu-id="93d29-206">You will need both in hello Azure Portal – open your notification hub, click on **Settings** > **Notification Services** > **Windows (WNS)** and enter hello information in hello required fields.</span></span>

![](./media/notification-hubs-geofence/notification-hubs-wns.png)

<span data-ttu-id="93d29-207">Clique em **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="93d29-207">Click on **Save**.</span></span>

<span data-ttu-id="93d29-208">Clique com o botão direito do rato em **Referências** no **Explorador de Soluções** e, em seguida, clique em **Gerir Pacotes NuGet**.</span><span class="sxs-lookup"><span data-stu-id="93d29-208">Right click on **References** in **Solution Explorer** and select **Manage NuGet Packages**.</span></span> <span data-ttu-id="93d29-209">Vamos precisar de tooadd toohello uma referência **biblioteca gerida do Service Bus do Microsoft Azure** – basta procurar `WindowsAzure.Messaging.Managed` e adicioná-la tooyour projeto.</span><span class="sxs-lookup"><span data-stu-id="93d29-209">We will need tooadd a reference toohello **Microsoft Azure Service Bus managed library** – simply search for `WindowsAzure.Messaging.Managed` and add it tooyour project.</span></span>

![](./media/notification-hubs-geofence/vs-nuget.png)

<span data-ttu-id="93d29-210">Para fins de teste, podemos criar Olá `MainPage_Loaded` novamente o processador de eventos e adicione esta tooit de fragmento de código:</span><span class="sxs-lookup"><span data-stu-id="93d29-210">For testing purposes, we can create hello `MainPage_Loaded` event handler once again, and add this code snippet tooit:</span></span>

    var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();

    var hub = new NotificationHub("HUB_NAME", "HUB_LISTEN_CONNECTION_STRING");
    var result = await hub.RegisterNativeAsync(channel.Uri);

    // Displays hello registration ID so you know it was successful
    if (result.RegistrationId != null)
    {
        Debug.WriteLine("Reg successful.");
    }

<span data-ttu-id="93d29-211">Olá acima regista aplicação Olá no hub de notificação de Olá.</span><span class="sxs-lookup"><span data-stu-id="93d29-211">hello above registers hello app with hello notification hub.</span></span> <span data-ttu-id="93d29-212">São toogo pronto!</span><span class="sxs-lookup"><span data-stu-id="93d29-212">You are ready toogo!</span></span> 

<span data-ttu-id="93d29-213">No `LocationHelper`, dentro de Olá `Geolocator_PositionChanged` processador, pode adicionar um fragmento de código de teste que coloca forçadamente a localização de Olá dentro do perímetro geográfico de Olá:</span><span class="sxs-lookup"><span data-stu-id="93d29-213">In `LocationHelper`, inside hello `Geolocator_PositionChanged` handler, you can add a piece of test code that will forcefully put hello location inside hello geofence:</span></span>

    await LocationHelper.SendLocationToBackend("wns", "TEST_USER", "TEST", "37.7746", "-122.3858");

<span data-ttu-id="93d29-214">Uma vez que não está a transmitir as coordenadas reais Olá (que poderão não estar dentro de limites de Olá momento Olá) e estiver a utilizar valores de teste predefinidos, veremos aparecer uma notificação na atualização:</span><span class="sxs-lookup"><span data-stu-id="93d29-214">Because we are not passing hello real coordinates (which might not be within hello boundaries at hello moment) and are using predefined test values, we will see a notification show up on update:</span></span>

![](./media/notification-hubs-geofence/notification-hubs-test-notification.png)

## <a name="whats-next"></a><span data-ttu-id="93d29-215">Passos seguintes?</span><span class="sxs-lookup"><span data-stu-id="93d29-215">What’s next?</span></span>
<span data-ttu-id="93d29-216">Existem alguns passos que poderá ter toofollow na adição toohello acima toomake se de que a solução de Olá prontos para produção.</span><span class="sxs-lookup"><span data-stu-id="93d29-216">There are a couple of steps that you might need toofollow in addition toohello above toomake sure that hello solution is production-ready.</span></span>

<span data-ttu-id="93d29-217">Primeiro e mais importante, poderá ser necessário tooensure que perímetros geográficos são dinâmicos.</span><span class="sxs-lookup"><span data-stu-id="93d29-217">First and foremost, you might need tooensure that geofences are dynamic.</span></span> <span data-ttu-id="93d29-218">Isto irá exigir algum trabalho adicional com Olá API do Bing na ordem toobe tooupload capaz de novos limites dentro origem de dados existente Olá.</span><span class="sxs-lookup"><span data-stu-id="93d29-218">This will require some extra work with hello Bing API in order toobe able tooupload new boundaries within hello existing data source.</span></span> <span data-ttu-id="93d29-219">Consulte Olá [documentação da API de serviços de dados geográficos do Bing](https://msdn.microsoft.com/library/ff701734.aspx) para obter mais detalhes sobre o assunto de Olá.</span><span class="sxs-lookup"><span data-stu-id="93d29-219">Consult hello [Bing Spatial Data Services API documentation](https://msdn.microsoft.com/library/ff701734.aspx) for more details on hello subject.</span></span>

<span data-ttu-id="93d29-220">Segundo, como são tooensure de trabalho que a entrega de Olá é feita participantes corretos toohello, é aconselhável tootarget-las através de [etiquetagem](notification-hubs-tags-segment-push-message.md).</span><span class="sxs-lookup"><span data-stu-id="93d29-220">Second, as you are working tooensure that hello delivery is done toohello right participants, you might want tootarget them via [tagging](notification-hubs-tags-segment-push-message.md).</span></span>

<span data-ttu-id="93d29-221">solução Olá mostrada acima descreve um cenário em que poderá ter uma grande variedade de plataformas de destino, pelo que iremos limita as capacidades de toosystem específicas do Olá barreira geográfica.</span><span class="sxs-lookup"><span data-stu-id="93d29-221">hello solution shown above describes a scenario in which you might have a wide variety of target platforms, so we did not limit hello geofencing toosystem-specific capabilities.</span></span> <span data-ttu-id="93d29-222">Dito isto, Olá plataforma Universal do Windows oferece capacidades demasiado[detetar perímetros geográficos direito out-of-a-box](https://msdn.microsoft.com/windows/uwp/maps-and-location/set-up-a-geofence).</span><span class="sxs-lookup"><span data-stu-id="93d29-222">That said, hello Universal Windows Platform offers capabilities too[detect geofences right out-of-the-box](https://msdn.microsoft.com/windows/uwp/maps-and-location/set-up-a-geofence).</span></span>

<span data-ttu-id="93d29-223">Para obter mais detalhes sobre as capacidades dos Notification Hubs, consulte o nosso [portal de documentação](https://azure.microsoft.com/documentation/services/notification-hubs/).</span><span class="sxs-lookup"><span data-stu-id="93d29-223">For more details regarding Notification Hubs capabilities, check out our [documentation portal](https://azure.microsoft.com/documentation/services/notification-hubs/).</span></span>

