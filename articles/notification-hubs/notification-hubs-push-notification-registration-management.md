---
title: "aaaRegistration gestão"
description: "Este tópico explica como tooregister dispositivos com os notification hubs em ordem tooreceive notificações push."
services: notification-hubs
documentationcenter: .net
author: ysxu
manager: erikre
editor: 
ms.assetid: fd0ee230-132c-4143-b4f9-65cef7f463a1
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: dotnet
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: 76471a45c7a0da1614ceed82b73cdb3319979ff7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="registration-management"></a>Gestão de registos
## <a name="overview"></a>Descrição geral
Este tópico explica como tooregister dispositivos com os notification hubs em ordem tooreceive notificações push. tópico de Olá descreve registos a um nível elevado, em seguida, apresenta os padrões de principais de Olá dois para registar dispositivos: registo de dispositivo Olá diretamente toohello notification hub e registar através de um back-end da aplicação. 

## <a name="what-is-device-registration"></a>O que é o registo de dispositivos
Registo de dispositivos com um Hub de notificação é realizado através de um **registo** ou **instalação**.

#### <a name="registrations"></a>Registos
Um registo associa Olá identificador de serviço de notificação de plataforma (PNS) para um dispositivo com as etiquetas e possivelmente um modelo. Identificador PNS do Olá pode ser um ChannelURI, o token do dispositivo ou o id de registo do GCM. As etiquetas são utilizados tooroute notificações toohello conjunto correto de identificadores do dispositivo. Para obter mais informações, consulte [de encaminhamento e expressões de etiqueta](notification-hubs-tags-segment-push-message.md). Os modelos são tooimplement utilizados por registo transformação. Para obter mais informações, consulte [modelos](notification-hubs-templates-cross-platform-push-messages.md).

#### <a name="installations"></a>Instalações
Uma instalação é um avançada as propriedades relacionadas com registo que inclui uma matriz de push. É Olá abordagem melhor e mais recentes tooregistering os seus dispositivos. No entanto, não é suportado pelo .NET SDK do lado do cliente ([SDK dos Notification Hub para operações de back-end](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/)) chegou.  Isto significa que se está a registar Olá próprio dispositivo cliente, terá de toouse Olá [API REST dos Notification Hubs](https://msdn.microsoft.com/library/mt621153.aspx) abordar toosupport instalações. Se estiver a utilizar um serviço de back-end, deve ser capaz de toouse [SDK dos Notification Hub para operações de back-end](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).

Olá seguem-se algumas instalações de toousing vantagens chave:

* Criar ou atualizar uma instalação totalmente é idempotent. Por isso, pode repetir sem as preocupações registos duplicados.
* modelo de instalação de Olá permite pushes individuais toodo fácil - direcionada para dispositivos específicos. Uma tag de sistema **"$InstallationId: [installationId]"** é adicionado automaticamente com cada registo de instalação com base. Por isso, pode chamar um tootarget de etiqueta de toothis enviar um dispositivo específico sem ter toodo codificação adicionais.
* Utilizar as instalações permite também toodo registo parcial atualizações. Olá atualização parcial de uma instalação é solicitada com um método de PATCH utilizando Olá [padrão de Patch de JSON](https://tools.ietf.org/html/rfc6902). Isto é particularmente útil quando pretender tooupdate etiquetas no registo de Olá. Não tiver toopull baixo registo todo Olá e, em seguida, reenviar todas as etiquetas de anterior Olá novamente.

Uma instalação pode conter Olá Olá seguintes propriedades. Para uma lista completa de Olá consulte de propriedades de instalação, [criar ou substituir uma instalação com a REST API](https://msdn.microsoft.com/library/azure/mt621153.aspx) ou [as propriedades de instalação](https://msdn.microsoft.com/library/azure/microsoft.azure.notificationhubs.installation_properties.aspx) para Olá.

    // Example installation format tooshow some supported properties
    {
        installationId: "",
        expirationTime: "",
        tags: [],
        platform: "",
        pushChannel: "",
        ………
        templates: {
            "templateName1" : {
                body: "",
                tags: [] },
            "templateName2" : {
                body: "",
                // Headers are for Windows Store only
                headers: {
                    "X-WNS-Type": "wns/tile" }
                tags: [] }
        },
        secondaryTiles: {
            "tileId1": {
                pushChannel: "",
                tags: [],
                templates: {
                    "otherTemplate": {
                        bodyTemplate: "",
                        headers: {
                            ... }
                        tags: [] }
                }
            }
        }
    }



É importante toonote que já não expiração registos e as instalações por predefinição.

As instalações e registos tem de conter um identificador PNS válido para cada dispositivo/canal. Uma vez identificadores PNS só podem ser obtidos numa aplicação cliente no dispositivo Olá, um padrão é tooregister diretamente em que o dispositivo com a aplicação de cliente Olá. Nos Olá outros mão, as considerações de segurança e lógica de negócio relacionados com tootags pode implicar o registo de dispositivos de toomanage no back-end da aplicação Olá. 

#### <a name="templates"></a>Modelos
Se quiser toouse [modelos](notification-hubs-templates-cross-platform-push-messages.md), a instalação do dispositivo Olá também conter todos os modelos associados com que o dispositivo num JSON formatar (consulte exemplo acima). Olá nomes dos modelos ajudam destino modelos diferentes para Olá mesmo dispositivo.

Tenha em atenção que cada nome de modelo mapeia o corpo do modelo de tooa e um conjunto opcional de etiquetas. Além disso, cada plataforma pode ter propriedades do modelo adicionais. Para a loja Windows (WNS utilizando) e Windows Phone 8 (utilizando MPNS), um conjunto de cabeçalhos adicionais pode fazer parte do modelo de Olá. No caso de Olá do APNs, pode definir um tooeither de propriedade de expiração uma constante ou tooa expressão de modelo. Para uma lista completa de Olá consulte de propriedades de instalação, [criar ou substituir uma instalação com REST](https://msdn.microsoft.com/library/azure/mt621153.aspx) tópico.

#### <a name="secondary-tiles-for-windows-store-apps"></a>Secundários mosaicos para aplicações da loja Windows
Para aplicações de cliente da loja Windows, o envio notificações toosecondary mosaicos é Olá mesmo como lhes enviar toohello primário. Isto também é suportado em instalações. Tenha em atenção que os mosaicos secundários tem um ChannelUri diferentes, que Olá SDK na sua aplicação de cliente processa de forma transparente.

Olá SecondaryTiles dicionário utiliza Olá TileId mesmo que é utilizado toocreate Olá SecondaryTiles objeto na sua aplicação da loja Windows.
Como com Olá ChannelUri primário, ChannelUris de mosaicos secundários pode alterar qualquer momento. Na ordem tookeep Olá as instalações no hub de notificação de Olá atualizado, o dispositivo de Olá deve atualizá-los com Olá ChannelUris atual de mosaicos secundário Olá.

## <a name="registration-management-from-hello-device"></a>Gestão de registo do dispositivo Olá
Quando a gerir o registo de dispositivos de aplicações de cliente, o back-end de Olá só é responsável pelo envio de notificações. As aplicações cliente manter identificadores PNS segurança toodate e registe as etiquetas. Olá imagem a seguir ilustra este padrão.

![](./media/notification-hubs-registration-management/notification-hubs-registering-on-device.png)

dispositivo Olá primeiro obtém Olá identificador PNS do Olá PNS, em seguida, regista no hub de notificação de Olá diretamente. Após o registo de Olá, Olá back-end de aplicação pode enviar uma notificação de filtragem desse registo. Para obter mais informações sobre como toosend notificações, consulte [de encaminhamento e expressões de etiqueta](notification-hubs-tags-segment-push-message.md).
Tenha em atenção que neste caso, irá utilizar apenas estão à escuta direitos tooaccess os hubs de notificação de dispositivo Olá. Para obter mais informações, consulte [segurança](notification-hubs-push-notification-security.md).

Registo do dispositivo Olá é o método mais simples de Olá, mas tem algumas desvantagens.
desvantagem primeiro Olá é que as respetivas etiquetas só pode atualizar uma aplicação de cliente quando a aplicação Olá está ativa. Por exemplo, se um utilizador tiver dois dispositivos registem equipas de relacionados toosport etiquetas, quando o primeiro dispositivo de Olá regista uma tag adicional (por exemplo, Seahawks), dispositivos segundo Olá não irão receber notificações de Olá sobre Olá Seahawks até que a aplicação Olá Olá segundo dispositivo é executado uma segunda vez. Mais geralmente, quando as etiquetas são afetadas por vários dispositivos, gerir etiquetas de back-end de Olá é uma opção de desejados.
desvantagem segundo do Olá da gestão do registo da aplicação de cliente Olá é que, uma vez que as aplicações podem ser vítima de acesso ilícito, proteger o registo de Olá toospecific etiquetas requer cuidado extra, conforme explicado na secção de Olá "segurança de nível de etiqueta".

#### <a name="example-code-tooregister-with-a-notification-hub-from-a-device-using-an-installation"></a>Código de exemplo tooregister com um hub de notificação de um dispositivo com uma instalação
Neste momento, isto só é suportado utilizando Olá [API REST dos Notification Hubs](https://msdn.microsoft.com/library/mt621153.aspx).

Também pode utilizar o método de PATCH de Olá utilizando Olá [padrão de Patch de JSON](https://tools.ietf.org/html/rfc6902) para atualizar a instalação de Olá.

    class DeviceInstallation
    {
        public string installationId { get; set; }
        public string platform { get; set; }
        public string pushChannel { get; set; }
        public string[] tags { get; set; }
    }

    private async Task<HttpStatusCode> CreateOrUpdateInstallationAsync(DeviceInstallation deviceInstallation,
         string hubName, string listenConnectionString)
    {
        if (deviceInstallation.installationId == null)
            return HttpStatusCode.BadRequest;

        // Parse connection string (https://msdn.microsoft.com/library/azure/dn495627.aspx)
        ConnectionStringUtility connectionSaSUtil = new ConnectionStringUtility(listenConnectionString);
        string hubResource = "installations/" + deviceInstallation.installationId + "?";
        string apiVersion = "api-version=2015-04";

        // Determine hello targetUri that we will sign
        string uri = connectionSaSUtil.Endpoint + hubName + "/" + hubResource + apiVersion;

        //=== Generate SaS Security Token for Authorization header ===
        // See, https://msdn.microsoft.com/library/azure/dn495627.aspx
        string SasToken = connectionSaSUtil.getSaSToken(uri, 60);

        using (var httpClient = new HttpClient())
        {
            string json = JsonConvert.SerializeObject(deviceInstallation);

            httpClient.DefaultRequestHeaders.Add("Authorization", SasToken);

            var response = await httpClient.PutAsync(uri, new StringContent(json, System.Text.Encoding.UTF8, "application/json"));
            return response.StatusCode;
        }
    }

    var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();

    string installationId = null;
    var settings = ApplicationData.Current.LocalSettings.Values;

    // If we have not stored a installation id in application data, create and store as application data.
    if (!settings.ContainsKey("__NHInstallationId"))
    {
        installationId = Guid.NewGuid().ToString();
        settings.Add("__NHInstallationId", installationId);
    }

    installationId = (string)settings["__NHInstallationId"];

    var deviceInstallation = new DeviceInstallation
    {
        installationId = installationId,
        platform = "wns",
        pushChannel = channel.Uri,
        //tags = tags.ToArray<string>()
    };

    var statusCode = await CreateOrUpdateInstallationAsync(deviceInstallation, 
                        "<HUBNAME>", "<SHARED LISTEN CONNECTION STRING>");

    if (statusCode != HttpStatusCode.Accepted)
    {
        var dialog = new MessageDialog(statusCode.ToString(), "Registration failed. Installation Id : " + installationId);
        dialog.Commands.Add(new UICommand("OK"));
        await dialog.ShowAsync();
    }
    else
    {
        var dialog = new MessageDialog("Registration successful using installation Id : " + installationId);
        dialog.Commands.Add(new UICommand("OK"));
        await dialog.ShowAsync();
    }



#### <a name="example-code-tooregister-with-a-notification-hub-from-a-device-using-a-registration"></a>Código de exemplo tooregister com um hub de notificação de um dispositivo com um registo
Estes métodos criar ou atualizar um registo de dispositivo Olá no qual são denominados. Isto significa que na ordem tooupdate Olá identificador ou Olá etiquetas, tem de substituir registo todo Olá. Lembre-se de que os registos são transitórios, pelo que deve ter sempre um arquivo fiável com etiquetas de atual Olá que necessita de um dispositivo específico.

    // Initialize hello Notification Hub
    NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString(listenConnString, hubName);

    // hello Device id from hello PNS
    var pushChannel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();

    // If you are registering from hello client itself, then store this registration id in device
    // storage. Then when hello app starts, you can check if a registration id already exists or not before
    // creating.
    var settings = ApplicationData.Current.LocalSettings.Values;

    // If we have not stored a registration id in application data, store in application data.
    if (!settings.ContainsKey("__NHRegistrationId"))
    {
        // make sure there are no existing registrations for this push handle (used for iOS and Android)    
        string newRegistrationId = null;
        var registrations = await hub.GetRegistrationsByChannelAsync(pushChannel.Uri, 100);
        foreach (RegistrationDescription registration in registrations)
        {
            if (newRegistrationId == null)
            {
                newRegistrationId = registration.RegistrationId;
            }
            else
            {
                await hub.DeleteRegistrationAsync(registration);
            }
        }

        newRegistrationId = await hub.CreateRegistrationIdAsync();

        settings.Add("__NHRegistrationId", newRegistrationId);
    }

    string regId = (string)settings["__NHRegistrationId"];

    RegistrationDescription registration = new WindowsRegistrationDescription(pushChannel.Uri);
    registration.RegistrationId = regId;
    registration.Tags = new HashSet<string>(YourTags);

    try
    {
        await hub.CreateOrUpdateRegistrationAsync(registration);
    }
    catch (Microsoft.WindowsAzure.Messaging.RegistrationGoneException e)
    {
        settings.Remove("__NHRegistrationId");
    }


## <a name="registration-management-from-a-backend"></a>Gestão de registo de um back-end
Gerir registos de back-end de Olá requer a escrever código adicional. aplicação Olá de dispositivo Olá tem de fornecer Olá backend de toohello de identificador PNS atualizada sempre que inicia a aplicação Olá (juntamente com as etiquetas e modelos) e back-end de Olá tem de atualizar este identificador no hub de notificação de Olá. Olá imagem a seguir ilustra esta estrutura.

![](./media/notification-hubs-registration-management/notification-hubs-registering-on-backend.png)

Olá das vantagens de gerir registos de back-end de Olá incluem Olá capacidade toomodify etiquetas tooregistrations, mesmo quando Olá aplicação correspondente no dispositivo Olá está inativa e aplicação de cliente de Olá tooauthenticate antes de adicionar um registo de tooits etiquetas.

#### <a name="example-code-tooregister-with-a-notification-hub-from-a-backend-using-an-installation"></a>Código de exemplo tooregister com um hub de notificação de um back-end através de uma instalação
dispositivo de cliente Olá ainda obtém o identificador PNS e propriedades de instalação relevantes como anteriormente e chamadas uma API personalizada no back-end de Olá que pode executar o registo de Olá e autorizar etiquetas Olá de etc. back-end podem tirar partido dos Olá [SDK dos Notification Hub para operações de back-end](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).

Também pode utilizar o método de PATCH de Olá utilizando Olá [padrão de Patch de JSON](https://tools.ietf.org/html/rfc6902) para atualizar a instalação de Olá.

    // Initialize hello Notification Hub
    NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString(listenConnString, hubName);

    // Custom API on hello backend
    public async Task<HttpResponseMessage> Put(DeviceInstallation deviceUpdate)
    {

        Installation installation = new Installation();
        installation.InstallationId = deviceUpdate.InstallationId;
        installation.PushChannel = deviceUpdate.Handle;
        installation.Tags = deviceUpdate.Tags;

        switch (deviceUpdate.Platform)
        {
            case "mpns":
                installation.Platform = NotificationPlatform.Mpns;
                break;
            case "wns":
                installation.Platform = NotificationPlatform.Wns;
                break;
            case "apns":
                installation.Platform = NotificationPlatform.Apns;
                break;
            case "gcm":
                installation.Platform = NotificationPlatform.Gcm;
                break;
            default:
                throw new HttpResponseException(HttpStatusCode.BadRequest);
        }


        // In hello backend we can control if a user is allowed tooadd tags
        //installation.Tags = new List<string>(deviceUpdate.Tags);
        //installation.Tags.Add("username:" + username);

        await hub.CreateOrUpdateInstallationAsync(installation);

        return Request.CreateResponse(HttpStatusCode.OK);
    }


#### <a name="example-code-tooregister-with-a-notification-hub-from-a-device-using-a-registration-id"></a>Código de exemplo tooregister com um hub de notificação de um dispositivo utilizando um id de registo
Do seu back-end da aplicação, pode executar operações básicas de CRUDS registarem. Por exemplo:

    var hub = NotificationHubClient.CreateClientFromConnectionString("{connectionString}", "hubName");

    // create a registration description object of hello correct type, e.g.
    var reg = new WindowsRegistrationDescription(channelUri, tags);

    // Create
    await hub.CreateRegistrationAsync(reg);

    // Get by id
    var r = await hub.GetRegistrationAsync<RegistrationDescription>("id");

    // update
    r.Tags.Add("myTag");

    // update on hub
    await hub.UpdateRegistrationAsync(r);

    // delete
    await hub.DeleteRegistrationAsync(r);


back-end de Olá deve processar simultaneidade entre as atualizações do registo. Barramento de serviço oferece controlo de simultaneidade otimista para a gestão de registo. Ao nível de Olá HTTP, isto é implementado com utilização Olá ETag nas operações de gestão do registo. Esta funcionalidade é transparente utilizada pelo Microsoft SDKs, que acionar uma excepção se uma atualização foi rejeitada por motivos de concorrência. Olá back-end de aplicação é responsável por processar estas exceções e repetir a operação de atualização de Olá se necessário.

