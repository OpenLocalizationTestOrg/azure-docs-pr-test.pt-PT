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
# <a name="geo-fenced-push-notifications-with-azure-notification-hubs-and-bing-spatial-data"></a>Notificações push de perímetro geográfico com Notification Hubs do Azure e Dados Geográficos do Bing
> [!NOTE]
> toocomplete neste tutorial, tem de ter uma conta do Azure Active Directory. Se não tiver uma conta, pode criar uma conta de avaliação gratuita em apenas alguns minutos. Para obter mais detalhes, consulte [Avaliação Gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02).
> 
> 

Neste tutorial, ficará a saber como toodeliver baseada na localização push notificações com Notification Hubs do Azure e dados geográficos do Bing, alavancada numa aplicação plataforma Universal do Windows seio da.

## <a name="prerequisites"></a>Pré-requisitos
Primeiro e mais importante, terá de toomake se de que tem todas as Olá software e o serviço de pré-requisitos:

* [Visual Studio 2015 Update 1](https://www.visualstudio.com/en-us/downloads/download-visual-studio-vs.aspx) ou posterior (a [Edição Community](https://go.microsoft.com/fwlink/?LinkId=691978&clcid=0x409) também serve). 
* Versão mais recente do Olá [Azure SDK](https://azure.microsoft.com/downloads/). 
* [Conta do Dev Center do Bing Maps](https://www.bingmapsportal.com/) (pode criar uma gratuitamente e associá-la à conta Microsoft). 

## <a name="getting-started"></a>Introdução
Vamos começar por criar o projeto de Olá. No Visual Studio, inicie um novo projeto do tipo **Aplicação em Branco (Universal Windows)**.

![](./media/notification-hubs-geofence/notification-hubs-create-blank-app.png)

Depois de concluída a criação do projeto Olá, deve ter o escudo Olá para aplicação Olá em si. Agora vamos configurar tudo para a infraestrutura de geométrico Olá. Uma vez que estamos toouse que serviços Bing para isto, existe é um ponto de final público REST API que nos permite molduras de localização específicas tooquery:

    http://spatial.virtualearth.net/REST/v1/data/

Terá de toospecify Olá os seguintes parâmetros tooget funcionar:

* **ID da Origem de Dados** e **Nome da Origem de Dados** – na API Bing Maps, origens de dados contêm vários metadados agrupados, como localizações e horas de expediente da operação. Pode ler mais acerca deles aqui. 
* **Nome da entidade** – Olá entidade que pretende toouse como um ponto de referência para notificação de Olá. 
* **Chave de API do Bing Maps** – esta é Olá chave que obteve anteriormente quando criou a conta do Dev Center do Bing Olá.

Vamos fazer uma descrição profunda na configuração de Olá para cada um dos elementos de Olá acima.

## <a name="setting-up-hello-data-source"></a>Configurar a origem de dados de Olá
Pode fazê-lo no Olá Dev Center do Bing Maps. Basta clicar em **origens de dados** no Olá barra navegação superior e selecione **gerir origens de dados**.

![](./media/notification-hubs-geofence/bing-maps-manage-data.png)

Se não já trabalhou com a Bing Maps API, provavelmente não existir origens de dados presentes, para que apenas possa criar uma nova clicando na origem de dados do carregamento de dados tooa. Certifique-se de que preenche todos os campos de Olá necessário:

![](./media/notification-hubs-geofence/bing-maps-create-data.png)

Poderá estar a pensar – o que é o ficheiro de dados de Olá e o que deve estar carregar? Para efeitos de Olá deste teste, podemos utilizar simplesmente amostra de Olá baseada em pipe que enquadra uma área da marítima de frente são Francisco Olá:

    Bing Spatial Data Services, 1.0, TestBoundaries
    EntityID(Edm.String,primaryKey)|Name(Edm.String)|Longitude(Edm.Double)|Latitude(Edm.Double)|Boundary(Edm.Geography)
    1|SanFranciscoPier|||POLYGON ((-122.389825 37.776598,-122.389438 37.773087,-122.381885 37.771849,-122.382186 37.777022,-122.389825 37.776598))

Olá acima representa esta entidade:

![](./media/notification-hubs-geofence/bing-maps-geofence.png)

Basta copiar e colar a cadeia de Olá acima para um novo ficheiro e guarde-o como **Notificationhubsgeofence**e carregá-lo no Olá Dev Center do Bing.

> [!NOTE]
> Poderá ser toospecify que lhes é pedida uma nova chave para Olá **chave mestra** que é diferente do Olá **chave de consulta**. Crie simplesmente uma nova chave através do dashboard e atualize Olá dados origem carregamento de página Olá.
> 
> 

Depois de carregar o ficheiro de dados de Olá, terá de certificar-se de que pode publicar a origem de dados de Olá toomake. 

Aceda demasiado**gerir origens de dados**, como fizemos acima, localize a origem de dados na lista de Olá e clique em **publicar** no Olá **ações** coluna. Em mais um pouco, deverá ver a origem de dados no Olá **origens de dados publicados** separador:

![](./media/notification-hubs-geofence/bing-maps-published-data.png)

Se clicar em **editar**, será capaz de toosee rapidamente as localizações que introduzimos:

![](./media/notification-hubs-geofence/bing-maps-data-details.png)

Neste momento, Olá portal não mostra Olá limites para Olá geográfico que criámos – precisamos apenas é uma confirmação de que a localização de Olá especificada está na vizinhança certa Olá.

Agora, tem de todos os requisitos de Olá Olá origem de dados. Clique em detalhes de Olá tooget no URL do pedido Olá para chamada Olá API, no Dev Center do Bing Maps, de Olá **origens de dados** e selecione **informações da origem de dados**.

![](./media/notification-hubs-geofence/bing-maps-data-info.png)

Olá **URL da consulta** é o que procuramos aqui. Este é o ponto final de Olá relativamente ao qual podemos executar consultas toocheck se Olá dispositivo não estiver atualmente dentro dos limites de Olá de uma localização ou não. tooperform esta verificação, precisamos simplesmente tooexecute uma ação obter chamar contra o URL da consulta Olá, com Olá seguir os parâmetros anexados:

    ?spatialFilter=intersects(%27POINT%20LONGITUDE%20LATITUDE)%27)&$format=json&key=QUERY_KEY

Dessa forma, a especificar um ponto de destino que obtemos do dispositivo Olá e Bing Maps efetuará automaticamente Olá cálculos toosee se está dentro do perímetro geográfico de Olá. Depois de executar o pedido de Olá através de um browser (ou cURL), irá obter padrão uma resposta JSON:

![](./media/notification-hubs-geofence/bing-maps-json.png)

Esta resposta só aparece quando o ponto de Olá, na verdade, está dentro do Olá designado limites. Se não estiver, obterá um registo de **resultados** vazio:

![](./media/notification-hubs-geofence/bing-maps-nores.png)

## <a name="setting-up-hello-uwp-application"></a>Configurar a aplicação de UWP Olá
Agora que temos a origem de dados de Olá pronta, podemos começar a trabalhar no Olá aplicação UWP de que fizemos anteriormente.

Primeiro e mais importante, temos de ativar os serviços de localização para a nossa aplicação. toodo, faça duplo clique no `Package.appxmanifest` ficheiros **Explorador de soluções**.

![](./media/notification-hubs-geofence/vs-package-manifest.png)

No Olá separador Propriedades pacote que acabou de abrir, clique em **capacidades** e certifique-se de que seleciona **localização**:

![](./media/notification-hubs-geofence/vs-package-location.png)

Como Olá capacidade de localização é declarada, crie uma nova pasta na solução com o nome `Core`e adicione um novo ficheiro dentro da mesma, denominado `LocationHelper.cs`:

![](./media/notification-hubs-geofence/vs-location-helper.png)

Olá `LocationHelper` classe em si é bastante básica nesta fase – tudo o que faz é permitir-na localização do utilizador Olá tooobtain através do sistema de Olá API:

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

Pode ler mais sobre como obter Olá localização do utilizador em aplicações UWP no oficial Olá [documento MSDN](https://msdn.microsoft.com/library/windows/apps/mt219698.aspx).

toocheck aquisição de localização de Olá, na verdade, está a funcionar, abra o lado de código de Olá da sua página principal (`MainPage.xaml.cs`). Crie um processador de eventos para Olá `Loaded` evento no Olá `MainPage` construtor:

    public MainPage()
    {
        this.InitializeComponent();
        this.Loaded += MainPage_Loaded;
    }

implementação de Olá de processador de eventos de Olá é o seguinte:

    private async void MainPage_Loaded(object sender, RoutedEventArgs e)
    {
        var location = await LocationHelper.GetCurrentLocation();

        if (location != null)
        {
            Debug.WriteLine(string.Concat(location.Coordinate.Longitude,
                " ", location.Coordinate.Latitude));
        }
    }

Repare que declarámos Olá processador como assíncrono porque `GetCurrentLocation` é passível de espera e necessita, por conseguinte, toobe executado num contexto assíncrono. Além disso, porque em determinadas circunstâncias poderá ficar com uma localização nula (por exemplo, os serviços de localização de Olá estão desativados ou aplicações Olá foi negada a localização de tooaccess de permissões), é necessário toomake certificar-se de que é corretamente processada com uma verificação nula.

Execute a aplicação Olá. Certifique-se de que permite o acesso de localização:

![](./media/notification-hubs-geofence/notification-hubs-location-access.png)

Olá, uma vez iniciada aplicação, deve ser capaz de toosee Olá coordenadas no Olá **saída** janela:

![](./media/notification-hubs-geofence/notification-hubs-location-output.png)

Agora, sabe que funciona de aquisição de localização – sentir processador de eventos de teste de Olá tooremove livre para carregado porque que não será possível utilizá-lo.

Olá passo seguinte consiste em toocapture alterações de localização. Para isso, vamos back toohello `LocationHelper` classe e adicione o processador de eventos de Olá para `PositionChanged`:

    geolocator.PositionChanged += Geolocator_PositionChanged;

implementação de Olá irá mostrar coordenadas de localização de Olá no Olá **saída** janela:

    private static async void Geolocator_PositionChanged(Geolocator sender, PositionChangedEventArgs args)
    {
        await CoreApplication.MainView.CoreWindow.Dispatcher.RunAsync(CoreDispatcherPriority.Normal, () =>
        {
            Debug.WriteLine(string.Concat(args.Position.Coordinate.Longitude, " ", args.Position.Coordinate.Latitude));
        });
    }

## <a name="setting-up-hello-backend"></a>Configurar o back-end de Olá
Transferir Olá [exemplo de back-end do .NET a partir do GitHub](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/NotifyUsers). Uma vez concluída a transferência de Olá, abra Olá `NotifyUsers` pasta e, subsequentemente, Olá `NotifyUsers.sln` ficheiro.

Conjunto Olá `AppBackend` projeto como Olá **projeto de arranque** e inicie.

![](./media/notification-hubs-geofence/vs-startup-project.png)

Olá projeto já está configurado toosend push notificações tootarget dispositivos, pelo que precisamos toodo apenas duas coisas – trocar a cadeia de ligação correta Olá para o hub de notificação de Olá e adicionar a notificação de Olá de toosend do limite identificação apenas quando hello utilizador está dentro do perímetro geográfico de Olá.

tooconfigure Olá cadeia de ligação, Olá `Models` pasta abra `Notifications.cs`. Olá `NotificationHubClient.CreateClientFromConnectionString` função deve conter informações de Olá acerca do notification hub que pode obter no Olá [Portal do Azure](https://portal.azure.com) (procure dentro Olá **políticas de acesso** painel no  **Definições**). Guarde o ficheiro de configuração atualizada Olá.

Agora precisamos toocreate um modelo para Olá resultado de API do Bing Maps. Olá toodo de forma mais fácil que é o botão direito no Olá `Models` pasta, **adicionar** > **classe**. Dê-lhe o nome `GeofenceBoundary.cs`. Quando tiver terminado, copie Olá JSON da resposta de Olá API que discutimos na primeira secção de Olá e no Visual Studio, utilize **editar** > **Colar especial** > **colar JSON como Classes**. 

Dessa forma, certifique-se esse objeto Olá será possível anular a serialização exatamente tal como era destinado. O conjunto de classes resultante deve assemelhar-se a isto:

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

Em seguida, abra `Controllers` > `NotificationsController.cs`. É necessário tootweak Olá Post chamada tooaccount de latitude e longitude do destino de Olá. Para tal, adicione simplesmente assinatura de função de toohello de duas cadeias – `latitude` e `longitude`.

    public async Task<HttpResponseMessage> Post(string pns, [FromBody]string message, string to_tag, string latitude, string longitude)

Criar uma nova classe no projeto Olá designado `ApiHelper.cs` – vamos utilizá-lo intersecções de limites do tooconnect tooBing toocheck ponto. Implemente uma função `IsPointWithinBounds`, como esta:

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
> Certifique-se de que toosubstitute, ponto final de Olá API, com o URL da consulta Olá que obteve anteriormente do Olá Dev Center do Bing (mesmo se aplica a chave de API de toohello). 
> 
> 

Se existirem consulta toohello de resultados, o que significa que Olá ponto especificado está dentro do Olá dos limites do perímetro geográfico de Olá, voltamos `true`. Se não existirem resultados, Bing é informar-nos que o ponto de Olá está fora do intervalo de pesquisa de Olá, voltamos `false`.

Novamente no `NotificationsController.cs`, crie uma verificação mesmo antes da instrução Olá:

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

Dessa forma, Olá notificação é apenas enviada quando o ponto de Olá está dentro dos limites de Olá.

## <a name="testing-push-notifications-in-hello-uwp-app"></a>Testar notificações push na aplicação UWP Olá
Retroceder toohello aplicação UWP, deverá ser agora tootest capaz de notificações. Dentro do Olá `LocationHelper` classe, crie uma nova função – `SendLocationToBackend`:

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
> Comutação Olá `POST_URL` toohello localização da sua aplicação web implementada que criámos na secção anterior Olá. Por agora, está OK toorun-la localmente, mas à medida que trabalha na implementação de uma versão pública, será necessário toohost-o com um fornecedor externo.
> 
> 

Vamos agora garantir que registamos a aplicação UWP Olá para notificações push. No Visual Studio, clique em **projeto** > **armazenar** > **associar aplicação à loja Olá**.

![](./media/notification-hubs-geofence/vs-associate-with-store.png)

Depois de iniciar sessão na conta de programador tooyour, certifique-se de que seleciona uma aplicação existente ou crie um novo e associa pacote Olá com o mesmo. 

Vá toohello Dev Center e abra Olá aplicação que acabou de criar. Clique em **Serviços** > **Notificações Push** > **Site dos Serviços Live**.

![](./media/notification-hubs-geofence/ms-live-services.png)

No site de Olá, tome nota do Olá **segredo da aplicação** e Olá **SID do pacote**. Terá de ambos no Portal do Azure – de Olá, abra o notification hub, clique em **definições** > **serviços de notificação** > **Windows (WNS)**e introduza as informações de Olá nos campos de Olá necessário.

![](./media/notification-hubs-geofence/notification-hubs-wns.png)

Clique em **Guardar**.

Clique com o botão direito do rato em **Referências** no **Explorador de Soluções** e, em seguida, clique em **Gerir Pacotes NuGet**. Vamos precisar de tooadd toohello uma referência **biblioteca gerida do Service Bus do Microsoft Azure** – basta procurar `WindowsAzure.Messaging.Managed` e adicioná-la tooyour projeto.

![](./media/notification-hubs-geofence/vs-nuget.png)

Para fins de teste, podemos criar Olá `MainPage_Loaded` novamente o processador de eventos e adicione esta tooit de fragmento de código:

    var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();

    var hub = new NotificationHub("HUB_NAME", "HUB_LISTEN_CONNECTION_STRING");
    var result = await hub.RegisterNativeAsync(channel.Uri);

    // Displays hello registration ID so you know it was successful
    if (result.RegistrationId != null)
    {
        Debug.WriteLine("Reg successful.");
    }

Olá acima regista aplicação Olá no hub de notificação de Olá. São toogo pronto! 

No `LocationHelper`, dentro de Olá `Geolocator_PositionChanged` processador, pode adicionar um fragmento de código de teste que coloca forçadamente a localização de Olá dentro do perímetro geográfico de Olá:

    await LocationHelper.SendLocationToBackend("wns", "TEST_USER", "TEST", "37.7746", "-122.3858");

Uma vez que não está a transmitir as coordenadas reais Olá (que poderão não estar dentro de limites de Olá momento Olá) e estiver a utilizar valores de teste predefinidos, veremos aparecer uma notificação na atualização:

![](./media/notification-hubs-geofence/notification-hubs-test-notification.png)

## <a name="whats-next"></a>Passos seguintes?
Existem alguns passos que poderá ter toofollow na adição toohello acima toomake se de que a solução de Olá prontos para produção.

Primeiro e mais importante, poderá ser necessário tooensure que perímetros geográficos são dinâmicos. Isto irá exigir algum trabalho adicional com Olá API do Bing na ordem toobe tooupload capaz de novos limites dentro origem de dados existente Olá. Consulte Olá [documentação da API de serviços de dados geográficos do Bing](https://msdn.microsoft.com/library/ff701734.aspx) para obter mais detalhes sobre o assunto de Olá.

Segundo, como são tooensure de trabalho que a entrega de Olá é feita participantes corretos toohello, é aconselhável tootarget-las através de [etiquetagem](notification-hubs-tags-segment-push-message.md).

solução Olá mostrada acima descreve um cenário em que poderá ter uma grande variedade de plataformas de destino, pelo que iremos limita as capacidades de toosystem específicas do Olá barreira geográfica. Dito isto, Olá plataforma Universal do Windows oferece capacidades demasiado[detetar perímetros geográficos direito out-of-a-box](https://msdn.microsoft.com/windows/uwp/maps-and-location/set-up-a-geofence).

Para obter mais detalhes sobre as capacidades dos Notification Hubs, consulte o nosso [portal de documentação](https://azure.microsoft.com/documentation/services/notification-hubs/).

