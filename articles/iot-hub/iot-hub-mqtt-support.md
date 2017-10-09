---
title: aaaUnderstand suporte do Azure IoT Hub MQTT | Microsoft Docs
description: "Programador orientá - suporte para dispositivos que se ligam através de ponto final do IoT Hub orientado para o dispositivo de tooan Olá protocolo MQTT. Inclui informações sobre o suporte MQTT incorporado no Olá SDKs do dispositivo IoT do Azure."
services: iot-hub
documentationcenter: .net
author: kdotchkoff
manager: timlt
editor: 
ms.assetid: 1d71c27c-b466-4a40-b95b-d6550cf85144
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/11/2017
ms.author: kdotchko
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: e461687963138987acdf1f4e0e34c453744ea191
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="communicate-with-your-iot-hub-using-hello-mqtt-protocol"></a><span data-ttu-id="939a1-104">Comunicar com o IoT hub com o protocolo MQTT Olá</span><span class="sxs-lookup"><span data-stu-id="939a1-104">Communicate with your IoT hub using hello MQTT protocol</span></span>

<span data-ttu-id="939a1-105">IoT Hub permite dispositivos toocommunicate com pontos finais dispositivos de IoT Hub Olá utilizando Olá [MQTT v 3.1.1] [ lnk-mqtt-org] protocolo na porta 8883 ou MQTT v 3.1.1 através do protocolo WebSocket na porta 443.</span><span class="sxs-lookup"><span data-stu-id="939a1-105">IoT Hub enables devices toocommunicate with hello IoT Hub device endpoints using hello [MQTT v3.1.1][lnk-mqtt-org] protocol on port 8883 or MQTT v3.1.1 over WebSocket protocol on port 443.</span></span> <span data-ttu-id="939a1-106">IoT Hub requer que todos os dispositivos comunicação toobe protegida com TLS/SSL (por conseguinte, o IoT Hub não suporta ligações não segura através da porta 1883).</span><span class="sxs-lookup"><span data-stu-id="939a1-106">IoT Hub requires all device communication toobe secured using TLS/SSL (hence, IoT Hub doesn’t support non-secure connections over port 1883).</span></span>

## <a name="connecting-tooiot-hub"></a><span data-ttu-id="939a1-107">Ligar tooIoT Hub</span><span class="sxs-lookup"><span data-stu-id="939a1-107">Connecting tooIoT Hub</span></span>

<span data-ttu-id="939a1-108">Um dispositivo pode utilizar o Olá MQTT protocolo tooconnect tooan IoT hub utilizando bibliotecas de Olá na Olá [SDKs IoT do Azure] [ lnk-device-sdks] ou utilizando o protocolo MQTT Olá diretamente.</span><span class="sxs-lookup"><span data-stu-id="939a1-108">A device can use hello MQTT protocol tooconnect tooan IoT hub either by using hello libraries in hello [Azure IoT SDKs][lnk-device-sdks] or by using hello MQTT protocol directly.</span></span>

## <a name="using-hello-device-sdks"></a><span data-ttu-id="939a1-109">Utilizar os SDKs do dispositivo Olá</span><span class="sxs-lookup"><span data-stu-id="939a1-109">Using hello device SDKs</span></span>

<span data-ttu-id="939a1-110">[SDKs do dispositivo] [ lnk-device-sdks] Olá que suporte o protocolo MQTT estão disponíveis para Java, Node.js, C, c# e Python.</span><span class="sxs-lookup"><span data-stu-id="939a1-110">[Device SDKs][lnk-device-sdks] that support hello MQTT protocol are available for Java, Node.js, C, C#, and Python.</span></span> <span data-ttu-id="939a1-111">SDKs do dispositivo Olá utilizar Olá padrão do IoT Hub ligação cadeia tooestablish uma ligação tooan do IoT hub.</span><span class="sxs-lookup"><span data-stu-id="939a1-111">hello device SDKs use hello standard IoT Hub connection string tooestablish a connection tooan IoT hub.</span></span> <span data-ttu-id="939a1-112">protocolo MQTT do toouse Olá, parâmetro de protocolo do cliente Olá tem de ser definido demasiado**MQTT**.</span><span class="sxs-lookup"><span data-stu-id="939a1-112">toouse hello MQTT protocol, hello client protocol parameter must be set too**MQTT**.</span></span> <span data-ttu-id="939a1-113">Por predefinição, o dispositivo de Olá SDKs ligar tooan IoT Hub com Olá **CleanSession** sinalizador definido demasiado**0** e utilizar **QoS 1** para a troca de mensagem com o IoT hub do Olá.</span><span class="sxs-lookup"><span data-stu-id="939a1-113">By default, hello device SDKs connect tooan IoT Hub with hello **CleanSession** flag set too**0** and use **QoS 1** for message exchange with hello IoT hub.</span></span>

<span data-ttu-id="939a1-114">Quando um dispositivo está ligado tooan IoT hub, SDKs do dispositivo Olá fornecem métodos que permitem toosend mensagens dispositivo hello do tooand receber mensagens de um hub IoT.</span><span class="sxs-lookup"><span data-stu-id="939a1-114">When a device is connected tooan IoT hub, hello device SDKs provide methods that enable hello device toosend messages tooand receive messages from an IoT hub.</span></span>

<span data-ttu-id="939a1-115">Olá tabela seguinte contém hiperligações toocode exemplos para cada idioma suportado e especifica Olá parâmetro toouse tooestablish tooIoT uma ligação Hub através do protocolo MQTT Olá.</span><span class="sxs-lookup"><span data-stu-id="939a1-115">hello following table contains links toocode samples for each supported language and specifies hello parameter toouse tooestablish a connection tooIoT Hub using hello MQTT protocol.</span></span>

| <span data-ttu-id="939a1-116">Idioma</span><span class="sxs-lookup"><span data-stu-id="939a1-116">Language</span></span> | <span data-ttu-id="939a1-117">Parâmetro de protocolo</span><span class="sxs-lookup"><span data-stu-id="939a1-117">Protocol parameter</span></span> |
| --- | --- |
| <span data-ttu-id="939a1-118">[NODE.js][lnk-sample-node]</span><span class="sxs-lookup"><span data-stu-id="939a1-118">[Node.js][lnk-sample-node]</span></span> |<span data-ttu-id="939a1-119">Azure-iot-dispositivo-mqtt</span><span class="sxs-lookup"><span data-stu-id="939a1-119">azure-iot-device-mqtt</span></span> |
| <span data-ttu-id="939a1-120">[Java][lnk-sample-java]</span><span class="sxs-lookup"><span data-stu-id="939a1-120">[Java][lnk-sample-java]</span></span> |<span data-ttu-id="939a1-121">IotHubClientProtocol.MQTT</span><span class="sxs-lookup"><span data-stu-id="939a1-121">IotHubClientProtocol.MQTT</span></span> |
| <span data-ttu-id="939a1-122">[C][lnk-sample-c]</span><span class="sxs-lookup"><span data-stu-id="939a1-122">[C][lnk-sample-c]</span></span> |<span data-ttu-id="939a1-123">MQTT_Protocol</span><span class="sxs-lookup"><span data-stu-id="939a1-123">MQTT_Protocol</span></span> |
| <span data-ttu-id="939a1-124">[C#][lnk-sample-csharp]</span><span class="sxs-lookup"><span data-stu-id="939a1-124">[C#][lnk-sample-csharp]</span></span> |<span data-ttu-id="939a1-125">TransportType.Mqtt</span><span class="sxs-lookup"><span data-stu-id="939a1-125">TransportType.Mqtt</span></span> |
| <span data-ttu-id="939a1-126">[Python][lnk-sample-python]</span><span class="sxs-lookup"><span data-stu-id="939a1-126">[Python][lnk-sample-python]</span></span> |<span data-ttu-id="939a1-127">IoTHubTransportProvider.MQTT</span><span class="sxs-lookup"><span data-stu-id="939a1-127">IoTHubTransportProvider.MQTT</span></span> |

### <a name="migrating-a-device-app-from-amqp-toomqtt"></a><span data-ttu-id="939a1-128">Migrar uma aplicação de dispositivo do AMQP tooMQTT</span><span class="sxs-lookup"><span data-stu-id="939a1-128">Migrating a device app from AMQP tooMQTT</span></span>

<span data-ttu-id="939a1-129">Se estiver a utilizar Olá [SDKs do dispositivo][lnk-device-sdks], mudar de utilizar AMQP tooMQTT exige a alteração parâmetro de protocolo de Olá na inicialização do cliente de Olá conforme indicado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="939a1-129">If you are using hello [device SDKs][lnk-device-sdks], switching from using AMQP tooMQTT requires changing hello protocol parameter in hello client initialization as stated previously.</span></span>

<span data-ttu-id="939a1-130">Ao fazê-lo, certifique-se de que toocheck Olá, seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="939a1-130">When doing so, make sure toocheck hello following items:</span></span>

* <span data-ttu-id="939a1-131">AMQP devolve erros para várias condições, enquanto MQTT termina ligação Olá.</span><span class="sxs-lookup"><span data-stu-id="939a1-131">AMQP returns errors for many conditions, while MQTT terminates hello connection.</span></span> <span data-ttu-id="939a1-132">Como resultado, a excepção a processar a lógica exijam algumas alterações.</span><span class="sxs-lookup"><span data-stu-id="939a1-132">As a result your exception handling logic might require some changes.</span></span>
* <span data-ttu-id="939a1-133">MQTT não suporta Olá *rejeitar* operações quando receber [mensagens da nuvem para dispositivo][lnk-messaging].</span><span class="sxs-lookup"><span data-stu-id="939a1-133">MQTT does not support hello *reject* operations when receiving [cloud-to-device messages][lnk-messaging].</span></span> <span data-ttu-id="939a1-134">Se a aplicação de back-end tem tooreceive uma resposta da aplicação de dispositivo Olá, considere utilizar [direcionar métodos][lnk-methods].</span><span class="sxs-lookup"><span data-stu-id="939a1-134">If your back-end app needs tooreceive a response from hello device app, consider using [direct methods][lnk-methods].</span></span>

## <a name="using-hello-mqtt-protocol-directly"></a><span data-ttu-id="939a1-135">Utilizando o protocolo MQTT Olá diretamente</span><span class="sxs-lookup"><span data-stu-id="939a1-135">Using hello MQTT protocol directly</span></span>
<span data-ttu-id="939a1-136">Se um dispositivo não é possível utilizar os SDKs do dispositivo Olá, ainda pode ligar a pontos finais de dispositivo público de toohello utilizando o protocolo MQTT Olá na porta 8883.</span><span class="sxs-lookup"><span data-stu-id="939a1-136">If a device cannot use hello device SDKs, it can still connect toohello public device endpoints using hello MQTT protocol on port 8883.</span></span> <span data-ttu-id="939a1-137">No Olá **CONNECT** dispositivo do pacote Olá deve utilizar Olá os seguintes valores:</span><span class="sxs-lookup"><span data-stu-id="939a1-137">In hello **CONNECT** packet hello device should use hello following values:</span></span>

* <span data-ttu-id="939a1-138">Para Olá **ClientId** campo, utilize Olá **deviceId**.</span><span class="sxs-lookup"><span data-stu-id="939a1-138">For hello **ClientId** field, use hello **deviceId**.</span></span>
* <span data-ttu-id="939a1-139">Para Olá **Username** campo, utilize `{iothubhostname}/{device_id}/api-version=2016-11-14`, em que {iothubhostname} é Olá CName completo do IoT hub do Olá.</span><span class="sxs-lookup"><span data-stu-id="939a1-139">For hello **Username** field, use `{iothubhostname}/{device_id}/api-version=2016-11-14`, where {iothubhostname} is hello full CName of hello IoT hub.</span></span>

    <span data-ttu-id="939a1-140">Por exemplo, se hello o nome do IoT hub é **contoso.azure devices.net** e se o nome do seu dispositivo Olá for **MyDevice01**, Olá completa **Username** campo deve conter `contoso.azure-devices.net/MyDevice01/api-version=2016-11-14`.</span><span class="sxs-lookup"><span data-stu-id="939a1-140">For example, if hello name of your IoT hub is **contoso.azure-devices.net** and if hello name of your device is **MyDevice01**, hello full **Username** field should contain `contoso.azure-devices.net/MyDevice01/api-version=2016-11-14`.</span></span>
* <span data-ttu-id="939a1-141">Para Olá **palavra-passe** campo, utilize um token SAS.</span><span class="sxs-lookup"><span data-stu-id="939a1-141">For hello **Password** field, use a SAS token.</span></span> <span data-ttu-id="939a1-142">formato de Olá de Olá SAS token é Olá mesmo para Olá HTTP e protocolos AMQP:</span><span class="sxs-lookup"><span data-stu-id="939a1-142">hello format of hello SAS token is hello same as for both hello HTTP and AMQP protocols:</span></span><br/><span data-ttu-id="939a1-143">`SharedAccessSignature sig={signature-string}&se={expiry}&sr={URL-encoded-resourceURI}`.</span><span class="sxs-lookup"><span data-stu-id="939a1-143">`SharedAccessSignature sig={signature-string}&se={expiry}&sr={URL-encoded-resourceURI}`.</span></span>

    <span data-ttu-id="939a1-144">Para obter mais informações sobre como toogenerate tokens SAS, consulte a secção dispositivos Olá [tokens de segurança a utilizar o IoT Hub][lnk-sas-tokens].</span><span class="sxs-lookup"><span data-stu-id="939a1-144">For more information about how toogenerate SAS tokens, see hello device section of [Using IoT Hub security tokens][lnk-sas-tokens].</span></span>

    <span data-ttu-id="939a1-145">Quando o testar, também pode utilizar Olá [Explorador de dispositivo] [ lnk-device-explorer] ferramenta tooquickly gerar um token SAS, que pode copiar e colar no seu próprio código:</span><span class="sxs-lookup"><span data-stu-id="939a1-145">When testing, you can also use hello [device explorer][lnk-device-explorer] tool tooquickly generate a SAS token that you can copy and paste into your own code:</span></span>

  1. <span data-ttu-id="939a1-146">Aceda toohello **gestão** separador **Explorador de dispositivo**.</span><span class="sxs-lookup"><span data-stu-id="939a1-146">Go toohello **Management** tab in **Device Explorer**.</span></span>
  2. <span data-ttu-id="939a1-147">Clique em **SAS Token** (principais direita).</span><span class="sxs-lookup"><span data-stu-id="939a1-147">Click **SAS Token** (top right).</span></span>
  3. <span data-ttu-id="939a1-148">No **SASTokenForm**, selecione o seu dispositivo no Olá **DeviceID** pendente.</span><span class="sxs-lookup"><span data-stu-id="939a1-148">On **SASTokenForm**, select your device in hello **DeviceID** drop down.</span></span> <span data-ttu-id="939a1-149">Definir o **TTL**.</span><span class="sxs-lookup"><span data-stu-id="939a1-149">Set your **TTL**.</span></span>
  4. <span data-ttu-id="939a1-150">Clique em **gerar** toocreate o token.</span><span class="sxs-lookup"><span data-stu-id="939a1-150">Click **Generate** toocreate your token.</span></span>

     <span data-ttu-id="939a1-151">Olá token SAS, que é gerado tem esta estrutura: `HostName={your hub name}.azure-devices.net;DeviceId=javadevice;SharedAccessSignature=SharedAccessSignature sr={your hub name}.azure-devices.net%2Fdevices%2FMyDevice01%2Fapi-version%3D2016-11-14&sig=vSgHBMUG.....Ntg%3d&se=1456481802`.</span><span class="sxs-lookup"><span data-stu-id="939a1-151">hello SAS token that's generated has this structure: `HostName={your hub name}.azure-devices.net;DeviceId=javadevice;SharedAccessSignature=SharedAccessSignature sr={your hub name}.azure-devices.net%2Fdevices%2FMyDevice01%2Fapi-version%3D2016-11-14&sig=vSgHBMUG.....Ntg%3d&se=1456481802`.</span></span>

     <span data-ttu-id="939a1-152">Olá parte este token toouse como Olá **palavra-passe** tooconnect campo utilizando MQTT é: `SharedAccessSignature sr={your hub name}.azure-devices.net%2Fdevices%2FMyDevice01%2Fapi-version%3D2016-11-14&sig=vSgHBMUG.....Ntg%3d&se=1456481802`.</span><span class="sxs-lookup"><span data-stu-id="939a1-152">hello part of this token toouse as hello **Password** field tooconnect using MQTT is: `SharedAccessSignature sr={your hub name}.azure-devices.net%2Fdevices%2FMyDevice01%2Fapi-version%3D2016-11-14&sig=vSgHBMUG.....Ntg%3d&se=1456481802`.</span></span>

<span data-ttu-id="939a1-153">Para MQTT ligar e desligar pacotes, o IoT Hub emite um evento no Olá **operações de monitorização** canal com informações adicionais que podem ajudá-lo tootroubleshoot problemas de conectividade.</span><span class="sxs-lookup"><span data-stu-id="939a1-153">For MQTT connect and disconnect packets, IoT Hub issues an event on hello **Operations Monitoring** channel with additional information that can help you tootroubleshoot connectivity issues.</span></span>

### <a name="sending-device-to-cloud-messages"></a><span data-ttu-id="939a1-154">Enviar mensagens do dispositivo-nuvem</span><span class="sxs-lookup"><span data-stu-id="939a1-154">Sending device-to-cloud messages</span></span>

<span data-ttu-id="939a1-155">Depois de efetuar uma ligação com êxito, um dispositivo pode enviar mensagens tooIoT Hub utilizando `devices/{device_id}/messages/events/` ou `devices/{device_id}/messages/events/{property_bag}` como um **o nome do tópico**.</span><span class="sxs-lookup"><span data-stu-id="939a1-155">After making a successful connection, a device can send messages tooIoT Hub using `devices/{device_id}/messages/events/` or `devices/{device_id}/messages/events/{property_bag}` as a **Topic Name**.</span></span> <span data-ttu-id="939a1-156">Olá `{property_bag}` elemento permite mensagens hello do toosend dispositivo com propriedades adicionais num formato com codificação url.</span><span class="sxs-lookup"><span data-stu-id="939a1-156">hello `{property_bag}` element enables hello device toosend messages with additional properties in a url-encoded format.</span></span> <span data-ttu-id="939a1-157">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="939a1-157">For example:</span></span>

```
RFC 2396-encoded(<PropertyName1>)=RFC 2396-encoded(<PropertyValue1>)&RFC 2396-encoded(<PropertyName2>)=RFC 2396-encoded(<PropertyValue2>)…
```

> [!NOTE]
> <span data-ttu-id="939a1-158">Isto `{property_bag}` elemento utiliza Olá codificação mesmo para cadeias de consulta no protocolo Olá HTTP.</span><span class="sxs-lookup"><span data-stu-id="939a1-158">This `{property_bag}` element uses hello same encoding as for query strings in hello HTTP protocol.</span></span>
>
>

<span data-ttu-id="939a1-159">Também pode utilizar a aplicação de dispositivo Olá `devices/{device_id}/messages/events/{property_bag}` como Olá **será o nome do tópico** toodefine *será mensagens* toobe reencaminhado como uma mensagem de telemetria.</span><span class="sxs-lookup"><span data-stu-id="939a1-159">hello device app can also use `devices/{device_id}/messages/events/{property_bag}` as hello **Will topic name** toodefine *Will messages* toobe forwarded as a telemetry message.</span></span>

- <span data-ttu-id="939a1-160">IoT Hub não suporta mensagens QoS 2.</span><span class="sxs-lookup"><span data-stu-id="939a1-160">IoT Hub does not support QoS 2 messages.</span></span> <span data-ttu-id="939a1-161">Se uma aplicação de dispositivo publica uma mensagem com **QoS 2**, o IoT Hub fecha a ligação de rede de Olá.</span><span class="sxs-lookup"><span data-stu-id="939a1-161">If a device app publishes a message with **QoS 2**, IoT Hub closes hello network connection.</span></span>
- <span data-ttu-id="939a1-162">IoT Hub não persiste manter mensagens.</span><span class="sxs-lookup"><span data-stu-id="939a1-162">IoT Hub does not persist Retain messages.</span></span> <span data-ttu-id="939a1-163">Se um dispositivo envia uma mensagem com Olá **manter** too1 o sinalizador definido, o IoT Hub adiciona Olá **x-optar ativamente por participar-manter** mensagem de toohello de propriedade de aplicação.</span><span class="sxs-lookup"><span data-stu-id="939a1-163">If a device sends a message with hello **RETAIN** flag set too1, IoT Hub adds hello **x-opt-retain** application property toohello message.</span></span> <span data-ttu-id="939a1-164">Neste caso, em vez de Olá persistentes manter mensagem, o IoT Hub passa-a aplicação de back-end toohello.</span><span class="sxs-lookup"><span data-stu-id="939a1-164">In this case, instead of persisting hello retain message, IoT Hub passes it toohello backend app.</span></span>
- <span data-ttu-id="939a1-165">IoT Hub apenas suporta uma ligação de MQTT Active Directory por dispositivo.</span><span class="sxs-lookup"><span data-stu-id="939a1-165">IoT Hub only supports one active MQTT connection per device.</span></span> <span data-ttu-id="939a1-166">Qualquer nova ligação de MQTT em nome Olá mesmo ID de dispositivo faz com que o IoT Hub ligação do toodrop Olá existente.</span><span class="sxs-lookup"><span data-stu-id="939a1-166">Any new MQTT connection on behalf of hello same device ID causes IoT Hub toodrop hello existing connection.</span></span>

<span data-ttu-id="939a1-167">Para obter mais informações, consulte [mensagens guia para programadores][lnk-messaging].</span><span class="sxs-lookup"><span data-stu-id="939a1-167">For more information, see [Messaging developer's guide][lnk-messaging].</span></span>

### <a name="receiving-cloud-to-device-messages"></a><span data-ttu-id="939a1-168">Receber mensagens da nuvem para dispositivo</span><span class="sxs-lookup"><span data-stu-id="939a1-168">Receiving cloud-to-device messages</span></span>

<span data-ttu-id="939a1-169">mensagens de tooreceive do IoT Hub, um dispositivo deve subscrever com `devices/{device_id}/messages/devicebound/#` como um **tópico filtro**.</span><span class="sxs-lookup"><span data-stu-id="939a1-169">tooreceive messages from IoT Hub, a device should subscribe using `devices/{device_id}/messages/devicebound/#` as a **Topic Filter**.</span></span> <span data-ttu-id="939a1-170">Olá universal múltiplos nível  **#**  Olá tópico filtro é utilizado apenas tooallow Olá tooreceive adicionais as propriedades do dispositivo no nome do tópico Olá.</span><span class="sxs-lookup"><span data-stu-id="939a1-170">hello multi-level wildcard **#** in hello Topic Filter is used only tooallow hello device tooreceive additional properties in hello topic name.</span></span> <span data-ttu-id="939a1-171">IoT Hub não permite a utilização de Olá de Olá  **#**  ou **?**</span><span class="sxs-lookup"><span data-stu-id="939a1-171">IoT Hub does not allow hello usage of hello **#** or **?**</span></span> <span data-ttu-id="939a1-172">carateres universais para filtragem de tópicos secundárias.</span><span class="sxs-lookup"><span data-stu-id="939a1-172">wildcards for filtering of sub-topics.</span></span> <span data-ttu-id="939a1-173">Uma vez que o IoT Hub não é um mediador de mensagens de pub sub de propósito geral, só suporta nomes de tópico Olá documentado e filtros de tópico.</span><span class="sxs-lookup"><span data-stu-id="939a1-173">Since IoT Hub is not a general purpose pub-sub messaging broker, it only supports hello documented topic names and topic filters.</span></span>

<span data-ttu-id="939a1-174">Olá dispositivo não receber as mensagens do IoT Hub, até que subscreveu com êxito ponto final de específicos do dispositivo tooits, representado pelo Olá `devices/{device_id}/messages/devicebound/#` filtro de tópico.</span><span class="sxs-lookup"><span data-stu-id="939a1-174">hello device does not receive any messages from IoT Hub, until it has successfully subscribed tooits device-specific endpoint, represented by hello `devices/{device_id}/messages/devicebound/#` topic filter.</span></span> <span data-ttu-id="939a1-175">Depois de estabelecida com êxito subscrição, o dispositivo de Olá é iniciado receber mensagens apenas na nuvem para o dispositivo que foram enviadas tooit após a hora de Olá da subscrição Olá.</span><span class="sxs-lookup"><span data-stu-id="939a1-175">After successful subscription has been established, hello device starts receiving only cloud-to-device messages that have been sent tooit after hello time of hello subscription.</span></span> <span data-ttu-id="939a1-176">Se o dispositivo de Olá estabelece ligação com **CleanSession** sinalizador definido demasiado**0**, subscrição de Olá é persistente em sessões diferentes.</span><span class="sxs-lookup"><span data-stu-id="939a1-176">If hello device connects with **CleanSession** flag set too**0**, hello subscription is persisted across different sessions.</span></span> <span data-ttu-id="939a1-177">Neste caso, Olá vez seguinte que for ligado com **CleanSession 0** dispositivo Olá recebe mensagens pendentes que foram enviadas tooit enquanto estava desligado.</span><span class="sxs-lookup"><span data-stu-id="939a1-177">In this case, hello next time it connects with **CleanSession 0** hello device receives outstanding messages that have been sent tooit while it was disconnected.</span></span> <span data-ttu-id="939a1-178">Se utilizar o dispositivo de Olá **CleanSession** sinalizador definido demasiado**1** ,-não receber quaisquer mensagens de IoT Hub até que subscreve tooits dispositivo-endpoint.</span><span class="sxs-lookup"><span data-stu-id="939a1-178">If hello device uses **CleanSession** flag set too**1** though, it does not receive any messages from IoT Hub until it subscribes tooits device-endpoint.</span></span>

<span data-ttu-id="939a1-179">IoT Hub disponibiliza as mensagens com Olá **o nome do tópico** `devices/{device_id}/messages/devicebound/`, ou `devices/{device_id}/messages/devicebound/{property_bag}` se existirem quaisquer propriedades da mensagem.</span><span class="sxs-lookup"><span data-stu-id="939a1-179">IoT Hub delivers messages with hello **Topic Name** `devices/{device_id}/messages/devicebound/`, or `devices/{device_id}/messages/devicebound/{property_bag}` if there are any message properties.</span></span> <span data-ttu-id="939a1-180">`{property_bag}`contém com codificação url pares chave-valor das propriedades da mensagem.</span><span class="sxs-lookup"><span data-stu-id="939a1-180">`{property_bag}` contains url-encoded key/value pairs of message properties.</span></span> <span data-ttu-id="939a1-181">Apenas as propriedades da aplicação e as propriedades do sistema pode ser definida utilizador (tais como **messageId** ou **correlationId**) estão incluídas na matriz de propriedades de Olá.</span><span class="sxs-lookup"><span data-stu-id="939a1-181">Only application properties and user-settable system properties (such as **messageId** or **correlationId**) are included in hello property bag.</span></span> <span data-ttu-id="939a1-182">Os nomes de propriedade de sistema têm o prefixo de Olá  **$** , propriedades da aplicação utilizam o nome da propriedade original Olá com nenhuma prefixo.</span><span class="sxs-lookup"><span data-stu-id="939a1-182">System property names have hello prefix **$**, application properties use hello original property name with no prefix.</span></span>

<span data-ttu-id="939a1-183">Quando uma aplicação de dispositivo subscreve tooa tópico com **QoS 2**, o IoT Hub concede máximo QoS nível 1 Olá **SUBACK** pacotes.</span><span class="sxs-lookup"><span data-stu-id="939a1-183">When a device app subscribes tooa topic with **QoS 2**, IoT Hub grants maximum QoS level 1 in hello **SUBACK** packet.</span></span> <span data-ttu-id="939a1-184">Depois disso, o IoT Hub fornece mensagens toohello era o dispositivo utilizar QoS 1.</span><span class="sxs-lookup"><span data-stu-id="939a1-184">After that, IoT Hub delivers messages toohello device using QoS 1.</span></span>

### <a name="retrieving-a-device-twins-properties"></a><span data-ttu-id="939a1-185">Obter as propriedades de um dispositivo duplo</span><span class="sxs-lookup"><span data-stu-id="939a1-185">Retrieving a device twin's properties</span></span>

<span data-ttu-id="939a1-186">Em primeiro lugar, um dispositivo subscreve demasiado`$iothub/twin/res/#`, respostas da operação de Olá tooreceive.</span><span class="sxs-lookup"><span data-stu-id="939a1-186">First, a device subscribes too`$iothub/twin/res/#`, tooreceive hello operation's responses.</span></span> <span data-ttu-id="939a1-187">Em seguida, envia uma mensagem vazia tootopic `$iothub/twin/GET/?$rid={request id}`, com um valor preenchido para **id do pedido**. serviço Olá, em seguida, envia uma mensagem de resposta que contêm Olá dispositivo duplo dados no tópico `$iothub/twin/res/{status}/?$rid={request id}`, utilizando Olá mesmo  **id do pedido** como pedido Olá.</span><span class="sxs-lookup"><span data-stu-id="939a1-187">Then, it sends an empty message tootopic `$iothub/twin/GET/?$rid={request id}`, with a populated value for **request id**. hello service then sends a response message containing hello device twin data on topic `$iothub/twin/res/{status}/?$rid={request id}`, using hello same **request id** as hello request.</span></span>

<span data-ttu-id="939a1-188">Id do pedido pode ser qualquer valor válido para um valor de propriedade da mensagem, como por [mensagens guia para programadores do IoT Hub][lnk-messaging], e o estado é validado como um número inteiro.</span><span class="sxs-lookup"><span data-stu-id="939a1-188">Request id can be any valid value for a message property value, as per [IoT Hub messaging developer's guide][lnk-messaging], and status is validated as an integer.</span></span>
<span data-ttu-id="939a1-189">corpo da resposta Olá contém uma secção de propriedades de Olá do dispositivo duplo de Olá:</span><span class="sxs-lookup"><span data-stu-id="939a1-189">hello response body contains hello properties section of hello device twin:</span></span>

<span data-ttu-id="939a1-190">corpo de Olá da entrada de registo de identidade Olá limitada toohello membro de "Propriedades", por exemplo:</span><span class="sxs-lookup"><span data-stu-id="939a1-190">hello body of hello identity registry entry limited toohello “properties” member, for example:</span></span>

        {
            "properties": {
                "desired": {
                    "telemetrySendFrequency": "5m",
                    "$version": 12
                },
                "reported": {
                    "telemetrySendFrequency": "5m",
                    "batteryLevel": 55,
                    "$version": 123
                }
            }
        }

<span data-ttu-id="939a1-191">Olá códigos de estado possíveis são:</span><span class="sxs-lookup"><span data-stu-id="939a1-191">hello possible status codes are:</span></span>

|<span data-ttu-id="939a1-192">Estado</span><span class="sxs-lookup"><span data-stu-id="939a1-192">Status</span></span> | <span data-ttu-id="939a1-193">Descrição</span><span class="sxs-lookup"><span data-stu-id="939a1-193">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="939a1-194">200</span><span class="sxs-lookup"><span data-stu-id="939a1-194">200</span></span> | <span data-ttu-id="939a1-195">Êxito</span><span class="sxs-lookup"><span data-stu-id="939a1-195">Success</span></span> |
| <span data-ttu-id="939a1-196">429</span><span class="sxs-lookup"><span data-stu-id="939a1-196">429</span></span> | <span data-ttu-id="939a1-197">Demasiados pedidos (limitados), como por [limitação do IoT Hub][lnk-quotas]</span><span class="sxs-lookup"><span data-stu-id="939a1-197">Too many requests (throttled), as per [IoT Hub throttling][lnk-quotas]</span></span> |
| <span data-ttu-id="939a1-198">5**</span><span class="sxs-lookup"><span data-stu-id="939a1-198">5**</span></span> | <span data-ttu-id="939a1-199">Erros de servidor</span><span class="sxs-lookup"><span data-stu-id="939a1-199">Server errors</span></span> |

<span data-ttu-id="939a1-200">Para obter mais informações, consulte [dispositivos duplos guia para programadores do][lnk-devguide-twin].</span><span class="sxs-lookup"><span data-stu-id="939a1-200">For more information, see [Device twins developer's guide][lnk-devguide-twin].</span></span>

### <a name="update-device-twins-reported-properties"></a><span data-ttu-id="939a1-201">Atualizar as propriedades do dispositivo duplo comunicado</span><span class="sxs-lookup"><span data-stu-id="939a1-201">Update device twin's reported properties</span></span>

<span data-ttu-id="939a1-202">Olá sequência seguinte descreve como um dispositivo atualizações Olá comunicadas propriedades no Olá dispositivo duplo na IoT Hub:</span><span class="sxs-lookup"><span data-stu-id="939a1-202">hello following sequence describes how a device updates hello reported properties in hello device twin in IoT Hub:</span></span>

1. <span data-ttu-id="939a1-203">Um dispositivo tem primeiro de subscrever toohello `$iothub/twin/res/#` respostas da operação do tópico tooreceive Olá do IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="939a1-203">A device must first subscribe toohello `$iothub/twin/res/#` topic tooreceive hello operation's responses from IoT Hub.</span></span>

1. <span data-ttu-id="939a1-204">Um dispositivo envia uma mensagem que contém Olá dispositivo duplo atualização toohello `$iothub/twin/PATCH/properties/reported/?$rid={request id}` tópico.</span><span class="sxs-lookup"><span data-stu-id="939a1-204">A device sends a message that contains hello device twin update toohello `$iothub/twin/PATCH/properties/reported/?$rid={request id}` topic.</span></span> <span data-ttu-id="939a1-205">Esta mensagem inclui uma **id do pedido** valor.</span><span class="sxs-lookup"><span data-stu-id="939a1-205">This message includes a **request id** value.</span></span>

1. <span data-ttu-id="939a1-206">Olá, serviço, em seguida, envia uma mensagem de resposta que contém Olá novo valor ETag Olá coleção de propriedades comunicado no tópico `$iothub/twin/res/{status}/?$rid={request id}`.</span><span class="sxs-lookup"><span data-stu-id="939a1-206">hello service then sends a response message that contains hello new ETag value for hello reported properties collection on topic `$iothub/twin/res/{status}/?$rid={request id}`.</span></span> <span data-ttu-id="939a1-207">Esta mensagem de resposta utiliza Olá mesmo **id do pedido** como pedido Olá.</span><span class="sxs-lookup"><span data-stu-id="939a1-207">This response message uses hello same **request id** as hello request.</span></span>

<span data-ttu-id="939a1-208">corpo de mensagem de pedido de Olá contém um documento JSON, que fornece novos valores de propriedades comunicadas (nenhuma propriedade ou metadados podem ser modificados).</span><span class="sxs-lookup"><span data-stu-id="939a1-208">hello request message body contains a JSON document, which provides new values for reported properties (no other property or metadata can be modified).</span></span>
<span data-ttu-id="939a1-209">Cada membro no documento JSON de Olá atualizações ou adicionar um membro correspondente Olá documento do Olá dispositivo duplo.</span><span class="sxs-lookup"><span data-stu-id="939a1-209">Each member in hello JSON document updates or add hello corresponding member in hello device twin’s document.</span></span> <span data-ttu-id="939a1-210">Um membro definido demasiado`null`, eliminações Olá membro da Olá que contém o objeto.</span><span class="sxs-lookup"><span data-stu-id="939a1-210">A member set too`null`, deletes hello member from hello containing object.</span></span> <span data-ttu-id="939a1-211">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="939a1-211">For example:</span></span>

        {
            "telemetrySendFrequency": "35m",
            "batteryLevel": 60
        }

<span data-ttu-id="939a1-212">Olá códigos de estado possíveis são:</span><span class="sxs-lookup"><span data-stu-id="939a1-212">hello possible status codes are:</span></span>

|<span data-ttu-id="939a1-213">Estado</span><span class="sxs-lookup"><span data-stu-id="939a1-213">Status</span></span> | <span data-ttu-id="939a1-214">Descrição</span><span class="sxs-lookup"><span data-stu-id="939a1-214">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="939a1-215">200</span><span class="sxs-lookup"><span data-stu-id="939a1-215">200</span></span> | <span data-ttu-id="939a1-216">Êxito</span><span class="sxs-lookup"><span data-stu-id="939a1-216">Success</span></span> |
| <span data-ttu-id="939a1-217">400</span><span class="sxs-lookup"><span data-stu-id="939a1-217">400</span></span> | <span data-ttu-id="939a1-218">Pedido incorreto.</span><span class="sxs-lookup"><span data-stu-id="939a1-218">Bad Request.</span></span> <span data-ttu-id="939a1-219">JSON com formato incorreto</span><span class="sxs-lookup"><span data-stu-id="939a1-219">Malformed JSON</span></span> |
| <span data-ttu-id="939a1-220">429</span><span class="sxs-lookup"><span data-stu-id="939a1-220">429</span></span> | <span data-ttu-id="939a1-221">Demasiados pedidos (limitados), como por [limitação do IoT Hub][lnk-quotas]</span><span class="sxs-lookup"><span data-stu-id="939a1-221">Too many requests (throttled), as per [IoT Hub throttling][lnk-quotas]</span></span> |
| <span data-ttu-id="939a1-222">5**</span><span class="sxs-lookup"><span data-stu-id="939a1-222">5**</span></span> | <span data-ttu-id="939a1-223">Erros de servidor</span><span class="sxs-lookup"><span data-stu-id="939a1-223">Server errors</span></span> |

<span data-ttu-id="939a1-224">Para obter mais informações, consulte [dispositivos duplos guia para programadores do][lnk-devguide-twin].</span><span class="sxs-lookup"><span data-stu-id="939a1-224">For more information, see [Device twins developer's guide][lnk-devguide-twin].</span></span>

### <a name="receiving-desired-properties-update-notifications"></a><span data-ttu-id="939a1-225">Receber notificações de atualização de propriedades pretendida</span><span class="sxs-lookup"><span data-stu-id="939a1-225">Receiving desired properties update notifications</span></span>

<span data-ttu-id="939a1-226">Quando um dispositivo estiver ligado, o IoT Hub envia tópico de toohello notificações `$iothub/twin/PATCH/properties/desired/?$version={new version}`, que contêm conteúdo de Olá da atualização de Olá realizado Olá solução de back-end.</span><span class="sxs-lookup"><span data-stu-id="939a1-226">When a device is connected, IoT Hub sends notifications toohello topic `$iothub/twin/PATCH/properties/desired/?$version={new version}`, which contain hello content of hello update performed by hello solution back end.</span></span> <span data-ttu-id="939a1-227">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="939a1-227">For example:</span></span>

        {
            "telemetrySendFrequency": "5m",
            "route": null
        }

<span data-ttu-id="939a1-228">Para atualizações da propriedade, `null` significa de valores que Olá JSON objeto membro está a ser eliminado.</span><span class="sxs-lookup"><span data-stu-id="939a1-228">As for property updates, `null` values means that hello JSON object member is being deleted.</span></span>


> [!IMPORTANT] 
> <span data-ttu-id="939a1-229">IoT Hub gera notificações de alteração apenas quando os dispositivos estão ligados.</span><span class="sxs-lookup"><span data-stu-id="939a1-229">IoT Hub generates change notifications only when devices are connected.</span></span> <span data-ttu-id="939a1-230">Certifique-se de que tooimplement Olá [fluxo de restabelecimento de ligação do dispositivo] [ lnk-devguide-twin-reconnection] tookeep Olá pretendido propriedades sincronizadas entre o IoT Hub e a aplicação de dispositivo Olá.</span><span class="sxs-lookup"><span data-stu-id="939a1-230">Make sure tooimplement hello [device reconnection flow][lnk-devguide-twin-reconnection] tookeep hello desired properties synchronized between IoT Hub and hello device app.</span></span>

<span data-ttu-id="939a1-231">Para obter mais informações, consulte [dispositivos duplos guia para programadores do][lnk-devguide-twin].</span><span class="sxs-lookup"><span data-stu-id="939a1-231">For more information, see [Device twins developer's guide][lnk-devguide-twin].</span></span>

### <a name="respond-tooa-direct-method"></a><span data-ttu-id="939a1-232">Método direto tooa de responder</span><span class="sxs-lookup"><span data-stu-id="939a1-232">Respond tooa direct method</span></span>

<span data-ttu-id="939a1-233">Em primeiro lugar, um dispositivo tem toosubscribe demasiado`$iothub/methods/POST/#`.</span><span class="sxs-lookup"><span data-stu-id="939a1-233">First, a device has toosubscribe too`$iothub/methods/POST/#`.</span></span> <span data-ttu-id="939a1-234">IoT Hub envia o tópico do método pedidos toohello `$iothub/methods/POST/{method name}/?$rid={request id}`, com um JSON válido ou uma mensagem vazia.</span><span class="sxs-lookup"><span data-stu-id="939a1-234">IoT Hub sends method requests toohello topic `$iothub/methods/POST/{method name}/?$rid={request id}`, with either a valid JSON or an empty body.</span></span>

<span data-ttu-id="939a1-235">toorespond, o dispositivo de Olá envia uma mensagem com um JSON válido ou um tópico do corpo vazio toohello `$iothub/methods/res/{status}/?$rid={request id}`, onde **id do pedido** tem toomatch Olá um na mensagem de pedido de Olá, e **estado** tem toobe um número inteiro .</span><span class="sxs-lookup"><span data-stu-id="939a1-235">toorespond, hello device sends a message with a valid JSON or empty body toohello topic `$iothub/methods/res/{status}/?$rid={request id}`, where **request id** has toomatch hello one in hello request message, and **status** has toobe an integer.</span></span>

<span data-ttu-id="939a1-236">Para obter mais informações, consulte [direcionar método guia para programadores do][lnk-methods].</span><span class="sxs-lookup"><span data-stu-id="939a1-236">For more information, see [Direct method developer's guide][lnk-methods].</span></span>

### <a name="additional-considerations"></a><span data-ttu-id="939a1-237">Considerações adicionais</span><span class="sxs-lookup"><span data-stu-id="939a1-237">Additional considerations</span></span>

<span data-ttu-id="939a1-238">Como uma consideração final, se precisar de comportamento de protocolo do toocustomize Olá MQTT no lado de nuvem Olá, deve rever Olá [gateway de protocolo do Azure IoT] [ lnk-azure-protocol-gateway] que lhe permitem toodeploy um elevado desempenho gateway de protocolo personalizado que interaja diretamente com o IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="939a1-238">As a final consideration, if you need toocustomize hello MQTT protocol behavior on hello cloud side, you should review hello [Azure IoT protocol gateway][lnk-azure-protocol-gateway] that enables you toodeploy a high-performance custom protocol gateway that interfaces directly with IoT Hub.</span></span> <span data-ttu-id="939a1-239">gateway de protocolo do Azure IoT Olá permite-lhe toocustomize Olá dispositivo protocolo tooaccommodate brownfield MQTT implementações ou outros protocolos personalizados.</span><span class="sxs-lookup"><span data-stu-id="939a1-239">hello Azure IoT protocol gateway enables you toocustomize hello device protocol tooaccommodate brownfield MQTT deployments or other custom protocols.</span></span> <span data-ttu-id="939a1-240">Esta abordagem requer, no entanto, que executa e operar um gateway de protocolo personalizado.</span><span class="sxs-lookup"><span data-stu-id="939a1-240">This approach does require, however, that you run and operate a custom protocol gateway.</span></span>

## <a name="next-steps"></a><span data-ttu-id="939a1-241">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="939a1-241">Next steps</span></span>

<span data-ttu-id="939a1-242">toolearn mais informações sobre o protocolo MQTT Olá, consulte Olá [documentação MQTT][lnk-mqtt-docs].</span><span class="sxs-lookup"><span data-stu-id="939a1-242">toolearn more about hello MQTT protocol, see hello [MQTT documentation][lnk-mqtt-docs].</span></span>

<span data-ttu-id="939a1-243">toolearn mais sobre o planeamento da sua implementação do IoT Hub, consulte:</span><span class="sxs-lookup"><span data-stu-id="939a1-243">toolearn more about planning your IoT Hub deployment, see:</span></span>

* <span data-ttu-id="939a1-244">[Certificado do Azure para o catálogo de dispositivos de IoT][lnk-devices]</span><span class="sxs-lookup"><span data-stu-id="939a1-244">[Azure Certified for IoT device catalog][lnk-devices]</span></span>
* <span data-ttu-id="939a1-245">[Suporte de protocolos adicionais][lnk-protocols]</span><span class="sxs-lookup"><span data-stu-id="939a1-245">[Support additional protocols][lnk-protocols]</span></span>
* <span data-ttu-id="939a1-246">[Comparar com os Event Hubs][lnk-compare]</span><span class="sxs-lookup"><span data-stu-id="939a1-246">[Compare with Event Hubs][lnk-compare]</span></span>
* <span data-ttu-id="939a1-247">[Dimensionamento, HA e DR][lnk-scaling]</span><span class="sxs-lookup"><span data-stu-id="939a1-247">[Scaling, HA, and DR][lnk-scaling]</span></span>

<span data-ttu-id="939a1-248">toofurther explorar Olá das capacidades do IoT Hub, consulte:</span><span class="sxs-lookup"><span data-stu-id="939a1-248">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="939a1-249">[Guia para programadores do IoT Hub][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="939a1-249">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="939a1-250">[Simulando um dispositivo com o Azure IoT Edge][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="939a1-250">[Simulating a device with Azure IoT Edge][lnk-iotedge]</span></span>

[lnk-device-sdks]: https://github.com/Azure/azure-iot-sdks
[lnk-mqtt-org]: http://mqtt.org/
[lnk-mqtt-docs]: http://mqtt.org/documentation
[lnk-sample-node]: https://github.com/Azure/azure-iot-sdk-node/blob/master/device/samples/simple_sample_device.js
[lnk-sample-java]: https://github.com/Azure/azure-iot-sdk-java/tree/master/device/samples/send-receive-sample/src/main/java/samples/com/microsoft/azure/iothub/SendReceive.java
[lnk-sample-c]: https://github.com/Azure/azure-iot-sdk-c/tree/master/iothub_client/samples/iothub_client_sample_mqtt
[lnk-sample-csharp]: https://github.com/Azure/azure-iot-sdk-csharp/tree/master/device/samples
[lnk-sample-python]: https://github.com/Azure/azure-iot-sdk-python/tree/master/device/samples
[lnk-device-explorer]: https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer
[lnk-sas-tokens]: iot-hub-devguide-security.md#use-sas-tokens-in-a-device-app
[lnk-azure-protocol-gateway]: iot-hub-protocol-gateway.md

[lnk-devices]: https://catalog.azureiotsuite.com/
[lnk-protocols]: iot-hub-protocol-gateway.md
[lnk-compare]: iot-hub-compare-event-hubs.md
[lnk-scaling]: iot-hub-scaling.md
[lnk-devguide]: iot-hub-devguide.md
[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md

[lnk-methods]: iot-hub-devguide-direct-methods.md
[lnk-messaging]: iot-hub-devguide-messaging.md

[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-devguide-twin-reconnection]: iot-hub-devguide-device-twins.md#device-reconnection-flow
[lnk-devguide-twin]: iot-hub-devguide-device-twins.md
