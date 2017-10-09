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
# <a name="registration-management"></a><span data-ttu-id="baa9f-103">Gestão de registos</span><span class="sxs-lookup"><span data-stu-id="baa9f-103">Registration management</span></span>
## <a name="overview"></a><span data-ttu-id="baa9f-104">Descrição geral</span><span class="sxs-lookup"><span data-stu-id="baa9f-104">Overview</span></span>
<span data-ttu-id="baa9f-105">Este tópico explica como tooregister dispositivos com os notification hubs em ordem tooreceive notificações push.</span><span class="sxs-lookup"><span data-stu-id="baa9f-105">This topic explains how tooregister devices with notification hubs in order tooreceive push notifications.</span></span> <span data-ttu-id="baa9f-106">tópico de Olá descreve registos a um nível elevado, em seguida, apresenta os padrões de principais de Olá dois para registar dispositivos: registo de dispositivo Olá diretamente toohello notification hub e registar através de um back-end da aplicação.</span><span class="sxs-lookup"><span data-stu-id="baa9f-106">hello topic describes registrations at a high level, then introduces hello two main patterns for registering devices: registering from hello device directly toohello notification hub, and registering through an application backend.</span></span> 

## <a name="what-is-device-registration"></a><span data-ttu-id="baa9f-107">O que é o registo de dispositivos</span><span class="sxs-lookup"><span data-stu-id="baa9f-107">What is device registration</span></span>
<span data-ttu-id="baa9f-108">Registo de dispositivos com um Hub de notificação é realizado através de um **registo** ou **instalação**.</span><span class="sxs-lookup"><span data-stu-id="baa9f-108">Device registration with a Notification Hub is accomplished using a **Registration** or **Installation**.</span></span>

#### <a name="registrations"></a><span data-ttu-id="baa9f-109">Registos</span><span class="sxs-lookup"><span data-stu-id="baa9f-109">Registrations</span></span>
<span data-ttu-id="baa9f-110">Um registo associa Olá identificador de serviço de notificação de plataforma (PNS) para um dispositivo com as etiquetas e possivelmente um modelo.</span><span class="sxs-lookup"><span data-stu-id="baa9f-110">A registration associates hello Platform Notification Service (PNS) handle for a device with tags and possibly a template.</span></span> <span data-ttu-id="baa9f-111">Identificador PNS do Olá pode ser um ChannelURI, o token do dispositivo ou o id de registo do GCM. As etiquetas são utilizados tooroute notificações toohello conjunto correto de identificadores do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="baa9f-111">hello PNS handle could be a ChannelURI, device token, or GCM registration id. Tags are used tooroute notifications toohello correct set of device handles.</span></span> <span data-ttu-id="baa9f-112">Para obter mais informações, consulte [de encaminhamento e expressões de etiqueta](notification-hubs-tags-segment-push-message.md).</span><span class="sxs-lookup"><span data-stu-id="baa9f-112">For more information, see [Routing and Tag Expressions](notification-hubs-tags-segment-push-message.md).</span></span> <span data-ttu-id="baa9f-113">Os modelos são tooimplement utilizados por registo transformação.</span><span class="sxs-lookup"><span data-stu-id="baa9f-113">Templates are used tooimplement per-registration transformation.</span></span> <span data-ttu-id="baa9f-114">Para obter mais informações, consulte [modelos](notification-hubs-templates-cross-platform-push-messages.md).</span><span class="sxs-lookup"><span data-stu-id="baa9f-114">For more information, see [Templates](notification-hubs-templates-cross-platform-push-messages.md).</span></span>

#### <a name="installations"></a><span data-ttu-id="baa9f-115">Instalações</span><span class="sxs-lookup"><span data-stu-id="baa9f-115">Installations</span></span>
<span data-ttu-id="baa9f-116">Uma instalação é um avançada as propriedades relacionadas com registo que inclui uma matriz de push.</span><span class="sxs-lookup"><span data-stu-id="baa9f-116">An Installation is an enhanced registration that includes a bag of push related properties.</span></span> <span data-ttu-id="baa9f-117">É Olá abordagem melhor e mais recentes tooregistering os seus dispositivos.</span><span class="sxs-lookup"><span data-stu-id="baa9f-117">It is hello latest and best approach tooregistering your devices.</span></span> <span data-ttu-id="baa9f-118">No entanto, não é suportado pelo .NET SDK do lado do cliente ([SDK dos Notification Hub para operações de back-end](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/)) chegou.</span><span class="sxs-lookup"><span data-stu-id="baa9f-118">However, it is not supported by client side .NET SDK ([Notification Hub SDK for backend operations](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/)) as of yet.</span></span>  <span data-ttu-id="baa9f-119">Isto significa que se está a registar Olá próprio dispositivo cliente, terá de toouse Olá [API REST dos Notification Hubs](https://msdn.microsoft.com/library/mt621153.aspx) abordar toosupport instalações.</span><span class="sxs-lookup"><span data-stu-id="baa9f-119">This means if you are registering from hello client device itself, you would have toouse hello [Notification Hubs REST API](https://msdn.microsoft.com/library/mt621153.aspx) approach toosupport installations.</span></span> <span data-ttu-id="baa9f-120">Se estiver a utilizar um serviço de back-end, deve ser capaz de toouse [SDK dos Notification Hub para operações de back-end](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span><span class="sxs-lookup"><span data-stu-id="baa9f-120">If you are using a backend service, you should be able toouse [Notification Hub SDK for backend operations](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span></span>

<span data-ttu-id="baa9f-121">Olá seguem-se algumas instalações de toousing vantagens chave:</span><span class="sxs-lookup"><span data-stu-id="baa9f-121">hello following are some key advantages toousing installations:</span></span>

* <span data-ttu-id="baa9f-122">Criar ou atualizar uma instalação totalmente é idempotent.</span><span class="sxs-lookup"><span data-stu-id="baa9f-122">Creating or updating an installation is fully idempotent.</span></span> <span data-ttu-id="baa9f-123">Por isso, pode repetir sem as preocupações registos duplicados.</span><span class="sxs-lookup"><span data-stu-id="baa9f-123">So you can retry it without any concerns about duplicate registrations.</span></span>
* <span data-ttu-id="baa9f-124">modelo de instalação de Olá permite pushes individuais toodo fácil - direcionada para dispositivos específicos.</span><span class="sxs-lookup"><span data-stu-id="baa9f-124">hello installation model makes it easy toodo individual pushes - targeting specific device.</span></span> <span data-ttu-id="baa9f-125">Uma tag de sistema **"$InstallationId: [installationId]"** é adicionado automaticamente com cada registo de instalação com base.</span><span class="sxs-lookup"><span data-stu-id="baa9f-125">A system tag **"$InstallationId:[installationId]"** is automatically added with each installation based registration.</span></span> <span data-ttu-id="baa9f-126">Por isso, pode chamar um tootarget de etiqueta de toothis enviar um dispositivo específico sem ter toodo codificação adicionais.</span><span class="sxs-lookup"><span data-stu-id="baa9f-126">So you can call a send toothis tag tootarget a specific device without having toodo any additional coding.</span></span>
* <span data-ttu-id="baa9f-127">Utilizar as instalações permite também toodo registo parcial atualizações.</span><span class="sxs-lookup"><span data-stu-id="baa9f-127">Using installations also enables you toodo partial registration updates.</span></span> <span data-ttu-id="baa9f-128">Olá atualização parcial de uma instalação é solicitada com um método de PATCH utilizando Olá [padrão de Patch de JSON](https://tools.ietf.org/html/rfc6902).</span><span class="sxs-lookup"><span data-stu-id="baa9f-128">hello partial update of an installation is requested with a PATCH method using hello [JSON-Patch standard](https://tools.ietf.org/html/rfc6902).</span></span> <span data-ttu-id="baa9f-129">Isto é particularmente útil quando pretender tooupdate etiquetas no registo de Olá.</span><span class="sxs-lookup"><span data-stu-id="baa9f-129">This is particularly useful when you want tooupdate tags on hello registration.</span></span> <span data-ttu-id="baa9f-130">Não tiver toopull baixo registo todo Olá e, em seguida, reenviar todas as etiquetas de anterior Olá novamente.</span><span class="sxs-lookup"><span data-stu-id="baa9f-130">You don't have toopull down hello entire registration and then resend all hello previous tags again.</span></span>

<span data-ttu-id="baa9f-131">Uma instalação pode conter Olá Olá seguintes propriedades.</span><span class="sxs-lookup"><span data-stu-id="baa9f-131">An installation can contain hello hello following properties.</span></span> <span data-ttu-id="baa9f-132">Para uma lista completa de Olá consulte de propriedades de instalação, [criar ou substituir uma instalação com a REST API](https://msdn.microsoft.com/library/azure/mt621153.aspx) ou [as propriedades de instalação](https://msdn.microsoft.com/library/azure/microsoft.azure.notificationhubs.installation_properties.aspx) para Olá.</span><span class="sxs-lookup"><span data-stu-id="baa9f-132">For a complete listing of hello installation properties see, [Create or Overwrite an Installation with REST API](https://msdn.microsoft.com/library/azure/mt621153.aspx) or [Installation Properties](https://msdn.microsoft.com/library/azure/microsoft.azure.notificationhubs.installation_properties.aspx) for hello .</span></span>

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



<span data-ttu-id="baa9f-133">É importante toonote que já não expiração registos e as instalações por predefinição.</span><span class="sxs-lookup"><span data-stu-id="baa9f-133">It is important toonote that registrations and installations by default no longer expire.</span></span>

<span data-ttu-id="baa9f-134">As instalações e registos tem de conter um identificador PNS válido para cada dispositivo/canal.</span><span class="sxs-lookup"><span data-stu-id="baa9f-134">Registrations and installations must contain a valid PNS handle for each device/channel.</span></span> <span data-ttu-id="baa9f-135">Uma vez identificadores PNS só podem ser obtidos numa aplicação cliente no dispositivo Olá, um padrão é tooregister diretamente em que o dispositivo com a aplicação de cliente Olá.</span><span class="sxs-lookup"><span data-stu-id="baa9f-135">Because PNS handles can only be obtained in a client app on hello device, one pattern is tooregister directly on that device with hello client app.</span></span> <span data-ttu-id="baa9f-136">Nos Olá outros mão, as considerações de segurança e lógica de negócio relacionados com tootags pode implicar o registo de dispositivos de toomanage no back-end da aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="baa9f-136">On hello other hand, security considerations and business logic related tootags might require you toomanage device registration in hello app back-end.</span></span> 

#### <a name="templates"></a><span data-ttu-id="baa9f-137">Modelos</span><span class="sxs-lookup"><span data-stu-id="baa9f-137">Templates</span></span>
<span data-ttu-id="baa9f-138">Se quiser toouse [modelos](notification-hubs-templates-cross-platform-push-messages.md), a instalação do dispositivo Olá também conter todos os modelos associados com que o dispositivo num JSON formatar (consulte exemplo acima).</span><span class="sxs-lookup"><span data-stu-id="baa9f-138">If you want toouse [Templates](notification-hubs-templates-cross-platform-push-messages.md), hello device installation also hold all templates associated with that device in a JSON format (see sample above).</span></span> <span data-ttu-id="baa9f-139">Olá nomes dos modelos ajudam destino modelos diferentes para Olá mesmo dispositivo.</span><span class="sxs-lookup"><span data-stu-id="baa9f-139">hello template names help target different templates for hello same device.</span></span>

<span data-ttu-id="baa9f-140">Tenha em atenção que cada nome de modelo mapeia o corpo do modelo de tooa e um conjunto opcional de etiquetas.</span><span class="sxs-lookup"><span data-stu-id="baa9f-140">Note that each template name maps tooa template body and an optional set of tags.</span></span> <span data-ttu-id="baa9f-141">Além disso, cada plataforma pode ter propriedades do modelo adicionais.</span><span class="sxs-lookup"><span data-stu-id="baa9f-141">Moreover, each platform can have additional template properties.</span></span> <span data-ttu-id="baa9f-142">Para a loja Windows (WNS utilizando) e Windows Phone 8 (utilizando MPNS), um conjunto de cabeçalhos adicionais pode fazer parte do modelo de Olá.</span><span class="sxs-lookup"><span data-stu-id="baa9f-142">For Windows Store (using WNS) and Windows Phone 8 (using MPNS), an additional set of headers can be part of hello template.</span></span> <span data-ttu-id="baa9f-143">No caso de Olá do APNs, pode definir um tooeither de propriedade de expiração uma constante ou tooa expressão de modelo.</span><span class="sxs-lookup"><span data-stu-id="baa9f-143">In hello case of APNs, you can set an expiry property tooeither a constant or tooa template expression.</span></span> <span data-ttu-id="baa9f-144">Para uma lista completa de Olá consulte de propriedades de instalação, [criar ou substituir uma instalação com REST](https://msdn.microsoft.com/library/azure/mt621153.aspx) tópico.</span><span class="sxs-lookup"><span data-stu-id="baa9f-144">For a complete listing of hello installation properties see, [Create or Overwrite an Installation with REST](https://msdn.microsoft.com/library/azure/mt621153.aspx) topic.</span></span>

#### <a name="secondary-tiles-for-windows-store-apps"></a><span data-ttu-id="baa9f-145">Secundários mosaicos para aplicações da loja Windows</span><span class="sxs-lookup"><span data-stu-id="baa9f-145">Secondary Tiles for Windows Store Apps</span></span>
<span data-ttu-id="baa9f-146">Para aplicações de cliente da loja Windows, o envio notificações toosecondary mosaicos é Olá mesmo como lhes enviar toohello primário.</span><span class="sxs-lookup"><span data-stu-id="baa9f-146">For Windows Store client applications, sending notifications toosecondary tiles is hello same as sending them toohello primary one.</span></span> <span data-ttu-id="baa9f-147">Isto também é suportado em instalações.</span><span class="sxs-lookup"><span data-stu-id="baa9f-147">This is also supported in installations.</span></span> <span data-ttu-id="baa9f-148">Tenha em atenção que os mosaicos secundários tem um ChannelUri diferentes, que Olá SDK na sua aplicação de cliente processa de forma transparente.</span><span class="sxs-lookup"><span data-stu-id="baa9f-148">Note that secondary tiles have a different ChannelUri, which hello SDK on your client app handles transparently.</span></span>

<span data-ttu-id="baa9f-149">Olá SecondaryTiles dicionário utiliza Olá TileId mesmo que é utilizado toocreate Olá SecondaryTiles objeto na sua aplicação da loja Windows.</span><span class="sxs-lookup"><span data-stu-id="baa9f-149">hello SecondaryTiles dictionary uses hello same TileId that is used toocreate hello SecondaryTiles object in your Windows Store app.</span></span>
<span data-ttu-id="baa9f-150">Como com Olá ChannelUri primário, ChannelUris de mosaicos secundários pode alterar qualquer momento.</span><span class="sxs-lookup"><span data-stu-id="baa9f-150">As with hello primary ChannelUri, ChannelUris of secondary tiles can change at any moment.</span></span> <span data-ttu-id="baa9f-151">Na ordem tookeep Olá as instalações no hub de notificação de Olá atualizado, o dispositivo de Olá deve atualizá-los com Olá ChannelUris atual de mosaicos secundário Olá.</span><span class="sxs-lookup"><span data-stu-id="baa9f-151">In order tookeep hello installations in hello notification hub updated, hello device must refresh them with hello current ChannelUris of hello secondary tiles.</span></span>

## <a name="registration-management-from-hello-device"></a><span data-ttu-id="baa9f-152">Gestão de registo do dispositivo Olá</span><span class="sxs-lookup"><span data-stu-id="baa9f-152">Registration management from hello device</span></span>
<span data-ttu-id="baa9f-153">Quando a gerir o registo de dispositivos de aplicações de cliente, o back-end de Olá só é responsável pelo envio de notificações.</span><span class="sxs-lookup"><span data-stu-id="baa9f-153">When managing device registration from client apps, hello backend is only responsible for sending notifications.</span></span> <span data-ttu-id="baa9f-154">As aplicações cliente manter identificadores PNS segurança toodate e registe as etiquetas.</span><span class="sxs-lookup"><span data-stu-id="baa9f-154">Client apps keep PNS handles up toodate, and register tags.</span></span> <span data-ttu-id="baa9f-155">Olá imagem a seguir ilustra este padrão.</span><span class="sxs-lookup"><span data-stu-id="baa9f-155">hello following picture illustrates this pattern.</span></span>

![](./media/notification-hubs-registration-management/notification-hubs-registering-on-device.png)

<span data-ttu-id="baa9f-156">dispositivo Olá primeiro obtém Olá identificador PNS do Olá PNS, em seguida, regista no hub de notificação de Olá diretamente.</span><span class="sxs-lookup"><span data-stu-id="baa9f-156">hello device first retrieves hello PNS handle from hello PNS, then registers with hello notification hub directly.</span></span> <span data-ttu-id="baa9f-157">Após o registo de Olá, Olá back-end de aplicação pode enviar uma notificação de filtragem desse registo.</span><span class="sxs-lookup"><span data-stu-id="baa9f-157">After hello registration is successful, hello app backend can send a notification targeting that registration.</span></span> <span data-ttu-id="baa9f-158">Para obter mais informações sobre como toosend notificações, consulte [de encaminhamento e expressões de etiqueta](notification-hubs-tags-segment-push-message.md).</span><span class="sxs-lookup"><span data-stu-id="baa9f-158">For more information about how toosend notifications, see [Routing and Tag Expressions](notification-hubs-tags-segment-push-message.md).</span></span>
<span data-ttu-id="baa9f-159">Tenha em atenção que neste caso, irá utilizar apenas estão à escuta direitos tooaccess os hubs de notificação de dispositivo Olá.</span><span class="sxs-lookup"><span data-stu-id="baa9f-159">Note that in this case, you will use only Listen rights tooaccess your notification hubs from hello device.</span></span> <span data-ttu-id="baa9f-160">Para obter mais informações, consulte [segurança](notification-hubs-push-notification-security.md).</span><span class="sxs-lookup"><span data-stu-id="baa9f-160">For more information, see [Security](notification-hubs-push-notification-security.md).</span></span>

<span data-ttu-id="baa9f-161">Registo do dispositivo Olá é o método mais simples de Olá, mas tem algumas desvantagens.</span><span class="sxs-lookup"><span data-stu-id="baa9f-161">Registering from hello device is hello simplest method, but it has some drawbacks.</span></span>
<span data-ttu-id="baa9f-162">desvantagem primeiro Olá é que as respetivas etiquetas só pode atualizar uma aplicação de cliente quando a aplicação Olá está ativa.</span><span class="sxs-lookup"><span data-stu-id="baa9f-162">hello first drawback is that a client app can only update its tags when hello app is active.</span></span> <span data-ttu-id="baa9f-163">Por exemplo, se um utilizador tiver dois dispositivos registem equipas de relacionados toosport etiquetas, quando o primeiro dispositivo de Olá regista uma tag adicional (por exemplo, Seahawks), dispositivos segundo Olá não irão receber notificações de Olá sobre Olá Seahawks até que a aplicação Olá Olá segundo dispositivo é executado uma segunda vez.</span><span class="sxs-lookup"><span data-stu-id="baa9f-163">For example, if a user has two devices that register tags related toosport teams, when hello first device registers for an additional tag (for example, Seahawks), hello second device will not receive hello notifications about hello Seahawks until hello app on hello second device is executed a second time.</span></span> <span data-ttu-id="baa9f-164">Mais geralmente, quando as etiquetas são afetadas por vários dispositivos, gerir etiquetas de back-end de Olá é uma opção de desejados.</span><span class="sxs-lookup"><span data-stu-id="baa9f-164">More generally, when tags are affected by multiple devices, managing tags from hello backend is a desirable option.</span></span>
<span data-ttu-id="baa9f-165">desvantagem segundo do Olá da gestão do registo da aplicação de cliente Olá é que, uma vez que as aplicações podem ser vítima de acesso ilícito, proteger o registo de Olá toospecific etiquetas requer cuidado extra, conforme explicado na secção de Olá "segurança de nível de etiqueta".</span><span class="sxs-lookup"><span data-stu-id="baa9f-165">hello second drawback of registration management from hello client app is that, since apps can be hacked, securing hello registration toospecific tags requires extra care, as explained in hello section “Tag-level security.”</span></span>

#### <a name="example-code-tooregister-with-a-notification-hub-from-a-device-using-an-installation"></a><span data-ttu-id="baa9f-166">Código de exemplo tooregister com um hub de notificação de um dispositivo com uma instalação</span><span class="sxs-lookup"><span data-stu-id="baa9f-166">Example code tooregister with a notification hub from a device using an installation</span></span>
<span data-ttu-id="baa9f-167">Neste momento, isto só é suportado utilizando Olá [API REST dos Notification Hubs](https://msdn.microsoft.com/library/mt621153.aspx).</span><span class="sxs-lookup"><span data-stu-id="baa9f-167">At this time, this is only supported using hello [Notification Hubs REST API](https://msdn.microsoft.com/library/mt621153.aspx).</span></span>

<span data-ttu-id="baa9f-168">Também pode utilizar o método de PATCH de Olá utilizando Olá [padrão de Patch de JSON](https://tools.ietf.org/html/rfc6902) para atualizar a instalação de Olá.</span><span class="sxs-lookup"><span data-stu-id="baa9f-168">You can also use hello PATCH method using hello [JSON-Patch standard](https://tools.ietf.org/html/rfc6902) for updating hello installation.</span></span>

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



#### <a name="example-code-tooregister-with-a-notification-hub-from-a-device-using-a-registration"></a><span data-ttu-id="baa9f-169">Código de exemplo tooregister com um hub de notificação de um dispositivo com um registo</span><span class="sxs-lookup"><span data-stu-id="baa9f-169">Example code tooregister with a notification hub from a device using a registration</span></span>
<span data-ttu-id="baa9f-170">Estes métodos criar ou atualizar um registo de dispositivo Olá no qual são denominados.</span><span class="sxs-lookup"><span data-stu-id="baa9f-170">These methods create or update a registration for hello device on which they are called.</span></span> <span data-ttu-id="baa9f-171">Isto significa que na ordem tooupdate Olá identificador ou Olá etiquetas, tem de substituir registo todo Olá.</span><span class="sxs-lookup"><span data-stu-id="baa9f-171">This means that in order tooupdate hello handle or hello tags, you must overwrite hello entire registration.</span></span> <span data-ttu-id="baa9f-172">Lembre-se de que os registos são transitórios, pelo que deve ter sempre um arquivo fiável com etiquetas de atual Olá que necessita de um dispositivo específico.</span><span class="sxs-lookup"><span data-stu-id="baa9f-172">Remember that registrations are transient, so you should always have a reliable store with hello current tags that a specific device needs.</span></span>

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


## <a name="registration-management-from-a-backend"></a><span data-ttu-id="baa9f-173">Gestão de registo de um back-end</span><span class="sxs-lookup"><span data-stu-id="baa9f-173">Registration management from a backend</span></span>
<span data-ttu-id="baa9f-174">Gerir registos de back-end de Olá requer a escrever código adicional.</span><span class="sxs-lookup"><span data-stu-id="baa9f-174">Managing registrations from hello backend requires writing additional code.</span></span> <span data-ttu-id="baa9f-175">aplicação Olá de dispositivo Olá tem de fornecer Olá backend de toohello de identificador PNS atualizada sempre que inicia a aplicação Olá (juntamente com as etiquetas e modelos) e back-end de Olá tem de atualizar este identificador no hub de notificação de Olá.</span><span class="sxs-lookup"><span data-stu-id="baa9f-175">hello app from hello device must provide hello updated PNS handle toohello backend every time hello app starts (along with tags and templates), and hello backend must update this handle on hello notification hub.</span></span> <span data-ttu-id="baa9f-176">Olá imagem a seguir ilustra esta estrutura.</span><span class="sxs-lookup"><span data-stu-id="baa9f-176">hello following picture illustrates this design.</span></span>

![](./media/notification-hubs-registration-management/notification-hubs-registering-on-backend.png)

<span data-ttu-id="baa9f-177">Olá das vantagens de gerir registos de back-end de Olá incluem Olá capacidade toomodify etiquetas tooregistrations, mesmo quando Olá aplicação correspondente no dispositivo Olá está inativa e aplicação de cliente de Olá tooauthenticate antes de adicionar um registo de tooits etiquetas.</span><span class="sxs-lookup"><span data-stu-id="baa9f-177">hello advantages of managing registrations from hello backend include hello ability toomodify tags tooregistrations even when hello corresponding app on hello device is inactive, and tooauthenticate hello client app before adding a tag tooits registration.</span></span>

#### <a name="example-code-tooregister-with-a-notification-hub-from-a-backend-using-an-installation"></a><span data-ttu-id="baa9f-178">Código de exemplo tooregister com um hub de notificação de um back-end através de uma instalação</span><span class="sxs-lookup"><span data-stu-id="baa9f-178">Example code tooregister with a notification hub from a backend using an installation</span></span>
<span data-ttu-id="baa9f-179">dispositivo de cliente Olá ainda obtém o identificador PNS e propriedades de instalação relevantes como anteriormente e chamadas uma API personalizada no back-end de Olá que pode executar o registo de Olá e autorizar etiquetas Olá de etc. back-end podem tirar partido dos Olá [SDK dos Notification Hub para operações de back-end](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span><span class="sxs-lookup"><span data-stu-id="baa9f-179">hello client device still gets its PNS handle and relevant installation properties as before and calls a custom API on hello backend that can perform hello registration and authorize tags etc. hello backend can leverage hello [Notification Hub SDK for backend operations](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span></span>

<span data-ttu-id="baa9f-180">Também pode utilizar o método de PATCH de Olá utilizando Olá [padrão de Patch de JSON](https://tools.ietf.org/html/rfc6902) para atualizar a instalação de Olá.</span><span class="sxs-lookup"><span data-stu-id="baa9f-180">You can also use hello PATCH method using hello [JSON-Patch standard](https://tools.ietf.org/html/rfc6902) for updating hello installation.</span></span>

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


#### <a name="example-code-tooregister-with-a-notification-hub-from-a-device-using-a-registration-id"></a><span data-ttu-id="baa9f-181">Código de exemplo tooregister com um hub de notificação de um dispositivo utilizando um id de registo</span><span class="sxs-lookup"><span data-stu-id="baa9f-181">Example code tooregister with a notification hub from a device using a registration id</span></span>
<span data-ttu-id="baa9f-182">Do seu back-end da aplicação, pode executar operações básicas de CRUDS registarem.</span><span class="sxs-lookup"><span data-stu-id="baa9f-182">From your app backend, you can perform basic CRUDS operations on registrations.</span></span> <span data-ttu-id="baa9f-183">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="baa9f-183">For example:</span></span>

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


<span data-ttu-id="baa9f-184">back-end de Olá deve processar simultaneidade entre as atualizações do registo.</span><span class="sxs-lookup"><span data-stu-id="baa9f-184">hello backend must handle concurrency between registration updates.</span></span> <span data-ttu-id="baa9f-185">Barramento de serviço oferece controlo de simultaneidade otimista para a gestão de registo.</span><span class="sxs-lookup"><span data-stu-id="baa9f-185">Service Bus offers optimistic concurrency control for registration management.</span></span> <span data-ttu-id="baa9f-186">Ao nível de Olá HTTP, isto é implementado com utilização Olá ETag nas operações de gestão do registo.</span><span class="sxs-lookup"><span data-stu-id="baa9f-186">At hello HTTP level, this is implemented with hello use of ETag on registration management operations.</span></span> <span data-ttu-id="baa9f-187">Esta funcionalidade é transparente utilizada pelo Microsoft SDKs, que acionar uma excepção se uma atualização foi rejeitada por motivos de concorrência.</span><span class="sxs-lookup"><span data-stu-id="baa9f-187">This feature is transparently used by Microsoft SDKs, which throw an exception if an update is rejected for concurrency reasons.</span></span> <span data-ttu-id="baa9f-188">Olá back-end de aplicação é responsável por processar estas exceções e repetir a operação de atualização de Olá se necessário.</span><span class="sxs-lookup"><span data-stu-id="baa9f-188">hello app backend is responsible for handling these exceptions and retrying hello update if required.</span></span>

