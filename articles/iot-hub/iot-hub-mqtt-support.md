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
# <a name="communicate-with-your-iot-hub-using-hello-mqtt-protocol"></a>Comunicar com o IoT hub com o protocolo MQTT Olá

IoT Hub permite dispositivos toocommunicate com pontos finais dispositivos de IoT Hub Olá utilizando Olá [MQTT v 3.1.1] [ lnk-mqtt-org] protocolo na porta 8883 ou MQTT v 3.1.1 através do protocolo WebSocket na porta 443. IoT Hub requer que todos os dispositivos comunicação toobe protegida com TLS/SSL (por conseguinte, o IoT Hub não suporta ligações não segura através da porta 1883).

## <a name="connecting-tooiot-hub"></a>Ligar tooIoT Hub

Um dispositivo pode utilizar o Olá MQTT protocolo tooconnect tooan IoT hub utilizando bibliotecas de Olá na Olá [SDKs IoT do Azure] [ lnk-device-sdks] ou utilizando o protocolo MQTT Olá diretamente.

## <a name="using-hello-device-sdks"></a>Utilizar os SDKs do dispositivo Olá

[SDKs do dispositivo] [ lnk-device-sdks] Olá que suporte o protocolo MQTT estão disponíveis para Java, Node.js, C, c# e Python. SDKs do dispositivo Olá utilizar Olá padrão do IoT Hub ligação cadeia tooestablish uma ligação tooan do IoT hub. protocolo MQTT do toouse Olá, parâmetro de protocolo do cliente Olá tem de ser definido demasiado**MQTT**. Por predefinição, o dispositivo de Olá SDKs ligar tooan IoT Hub com Olá **CleanSession** sinalizador definido demasiado**0** e utilizar **QoS 1** para a troca de mensagem com o IoT hub do Olá.

Quando um dispositivo está ligado tooan IoT hub, SDKs do dispositivo Olá fornecem métodos que permitem toosend mensagens dispositivo hello do tooand receber mensagens de um hub IoT.

Olá tabela seguinte contém hiperligações toocode exemplos para cada idioma suportado e especifica Olá parâmetro toouse tooestablish tooIoT uma ligação Hub através do protocolo MQTT Olá.

| Idioma | Parâmetro de protocolo |
| --- | --- |
| [NODE.js][lnk-sample-node] |Azure-iot-dispositivo-mqtt |
| [Java][lnk-sample-java] |IotHubClientProtocol.MQTT |
| [C][lnk-sample-c] |MQTT_Protocol |
| [C#][lnk-sample-csharp] |TransportType.Mqtt |
| [Python][lnk-sample-python] |IoTHubTransportProvider.MQTT |

### <a name="migrating-a-device-app-from-amqp-toomqtt"></a>Migrar uma aplicação de dispositivo do AMQP tooMQTT

Se estiver a utilizar Olá [SDKs do dispositivo][lnk-device-sdks], mudar de utilizar AMQP tooMQTT exige a alteração parâmetro de protocolo de Olá na inicialização do cliente de Olá conforme indicado anteriormente.

Ao fazê-lo, certifique-se de que toocheck Olá, seguintes itens:

* AMQP devolve erros para várias condições, enquanto MQTT termina ligação Olá. Como resultado, a excepção a processar a lógica exijam algumas alterações.
* MQTT não suporta Olá *rejeitar* operações quando receber [mensagens da nuvem para dispositivo][lnk-messaging]. Se a aplicação de back-end tem tooreceive uma resposta da aplicação de dispositivo Olá, considere utilizar [direcionar métodos][lnk-methods].

## <a name="using-hello-mqtt-protocol-directly"></a>Utilizando o protocolo MQTT Olá diretamente
Se um dispositivo não é possível utilizar os SDKs do dispositivo Olá, ainda pode ligar a pontos finais de dispositivo público de toohello utilizando o protocolo MQTT Olá na porta 8883. No Olá **CONNECT** dispositivo do pacote Olá deve utilizar Olá os seguintes valores:

* Para Olá **ClientId** campo, utilize Olá **deviceId**.
* Para Olá **Username** campo, utilize `{iothubhostname}/{device_id}/api-version=2016-11-14`, em que {iothubhostname} é Olá CName completo do IoT hub do Olá.

    Por exemplo, se hello o nome do IoT hub é **contoso.azure devices.net** e se o nome do seu dispositivo Olá for **MyDevice01**, Olá completa **Username** campo deve conter `contoso.azure-devices.net/MyDevice01/api-version=2016-11-14`.
* Para Olá **palavra-passe** campo, utilize um token SAS. formato de Olá de Olá SAS token é Olá mesmo para Olá HTTP e protocolos AMQP:<br/>`SharedAccessSignature sig={signature-string}&se={expiry}&sr={URL-encoded-resourceURI}`.

    Para obter mais informações sobre como toogenerate tokens SAS, consulte a secção dispositivos Olá [tokens de segurança a utilizar o IoT Hub][lnk-sas-tokens].

    Quando o testar, também pode utilizar Olá [Explorador de dispositivo] [ lnk-device-explorer] ferramenta tooquickly gerar um token SAS, que pode copiar e colar no seu próprio código:

  1. Aceda toohello **gestão** separador **Explorador de dispositivo**.
  2. Clique em **SAS Token** (principais direita).
  3. No **SASTokenForm**, selecione o seu dispositivo no Olá **DeviceID** pendente. Definir o **TTL**.
  4. Clique em **gerar** toocreate o token.

     Olá token SAS, que é gerado tem esta estrutura: `HostName={your hub name}.azure-devices.net;DeviceId=javadevice;SharedAccessSignature=SharedAccessSignature sr={your hub name}.azure-devices.net%2Fdevices%2FMyDevice01%2Fapi-version%3D2016-11-14&sig=vSgHBMUG.....Ntg%3d&se=1456481802`.

     Olá parte este token toouse como Olá **palavra-passe** tooconnect campo utilizando MQTT é: `SharedAccessSignature sr={your hub name}.azure-devices.net%2Fdevices%2FMyDevice01%2Fapi-version%3D2016-11-14&sig=vSgHBMUG.....Ntg%3d&se=1456481802`.

Para MQTT ligar e desligar pacotes, o IoT Hub emite um evento no Olá **operações de monitorização** canal com informações adicionais que podem ajudá-lo tootroubleshoot problemas de conectividade.

### <a name="sending-device-to-cloud-messages"></a>Enviar mensagens do dispositivo-nuvem

Depois de efetuar uma ligação com êxito, um dispositivo pode enviar mensagens tooIoT Hub utilizando `devices/{device_id}/messages/events/` ou `devices/{device_id}/messages/events/{property_bag}` como um **o nome do tópico**. Olá `{property_bag}` elemento permite mensagens hello do toosend dispositivo com propriedades adicionais num formato com codificação url. Por exemplo:

```
RFC 2396-encoded(<PropertyName1>)=RFC 2396-encoded(<PropertyValue1>)&RFC 2396-encoded(<PropertyName2>)=RFC 2396-encoded(<PropertyValue2>)…
```

> [!NOTE]
> Isto `{property_bag}` elemento utiliza Olá codificação mesmo para cadeias de consulta no protocolo Olá HTTP.
>
>

Também pode utilizar a aplicação de dispositivo Olá `devices/{device_id}/messages/events/{property_bag}` como Olá **será o nome do tópico** toodefine *será mensagens* toobe reencaminhado como uma mensagem de telemetria.

- IoT Hub não suporta mensagens QoS 2. Se uma aplicação de dispositivo publica uma mensagem com **QoS 2**, o IoT Hub fecha a ligação de rede de Olá.
- IoT Hub não persiste manter mensagens. Se um dispositivo envia uma mensagem com Olá **manter** too1 o sinalizador definido, o IoT Hub adiciona Olá **x-optar ativamente por participar-manter** mensagem de toohello de propriedade de aplicação. Neste caso, em vez de Olá persistentes manter mensagem, o IoT Hub passa-a aplicação de back-end toohello.
- IoT Hub apenas suporta uma ligação de MQTT Active Directory por dispositivo. Qualquer nova ligação de MQTT em nome Olá mesmo ID de dispositivo faz com que o IoT Hub ligação do toodrop Olá existente.

Para obter mais informações, consulte [mensagens guia para programadores][lnk-messaging].

### <a name="receiving-cloud-to-device-messages"></a>Receber mensagens da nuvem para dispositivo

mensagens de tooreceive do IoT Hub, um dispositivo deve subscrever com `devices/{device_id}/messages/devicebound/#` como um **tópico filtro**. Olá universal múltiplos nível  **#**  Olá tópico filtro é utilizado apenas tooallow Olá tooreceive adicionais as propriedades do dispositivo no nome do tópico Olá. IoT Hub não permite a utilização de Olá de Olá  **#**  ou **?** carateres universais para filtragem de tópicos secundárias. Uma vez que o IoT Hub não é um mediador de mensagens de pub sub de propósito geral, só suporta nomes de tópico Olá documentado e filtros de tópico.

Olá dispositivo não receber as mensagens do IoT Hub, até que subscreveu com êxito ponto final de específicos do dispositivo tooits, representado pelo Olá `devices/{device_id}/messages/devicebound/#` filtro de tópico. Depois de estabelecida com êxito subscrição, o dispositivo de Olá é iniciado receber mensagens apenas na nuvem para o dispositivo que foram enviadas tooit após a hora de Olá da subscrição Olá. Se o dispositivo de Olá estabelece ligação com **CleanSession** sinalizador definido demasiado**0**, subscrição de Olá é persistente em sessões diferentes. Neste caso, Olá vez seguinte que for ligado com **CleanSession 0** dispositivo Olá recebe mensagens pendentes que foram enviadas tooit enquanto estava desligado. Se utilizar o dispositivo de Olá **CleanSession** sinalizador definido demasiado**1** ,-não receber quaisquer mensagens de IoT Hub até que subscreve tooits dispositivo-endpoint.

IoT Hub disponibiliza as mensagens com Olá **o nome do tópico** `devices/{device_id}/messages/devicebound/`, ou `devices/{device_id}/messages/devicebound/{property_bag}` se existirem quaisquer propriedades da mensagem. `{property_bag}`contém com codificação url pares chave-valor das propriedades da mensagem. Apenas as propriedades da aplicação e as propriedades do sistema pode ser definida utilizador (tais como **messageId** ou **correlationId**) estão incluídas na matriz de propriedades de Olá. Os nomes de propriedade de sistema têm o prefixo de Olá  **$** , propriedades da aplicação utilizam o nome da propriedade original Olá com nenhuma prefixo.

Quando uma aplicação de dispositivo subscreve tooa tópico com **QoS 2**, o IoT Hub concede máximo QoS nível 1 Olá **SUBACK** pacotes. Depois disso, o IoT Hub fornece mensagens toohello era o dispositivo utilizar QoS 1.

### <a name="retrieving-a-device-twins-properties"></a>Obter as propriedades de um dispositivo duplo

Em primeiro lugar, um dispositivo subscreve demasiado`$iothub/twin/res/#`, respostas da operação de Olá tooreceive. Em seguida, envia uma mensagem vazia tootopic `$iothub/twin/GET/?$rid={request id}`, com um valor preenchido para **id do pedido**. serviço Olá, em seguida, envia uma mensagem de resposta que contêm Olá dispositivo duplo dados no tópico `$iothub/twin/res/{status}/?$rid={request id}`, utilizando Olá mesmo  **id do pedido** como pedido Olá.

Id do pedido pode ser qualquer valor válido para um valor de propriedade da mensagem, como por [mensagens guia para programadores do IoT Hub][lnk-messaging], e o estado é validado como um número inteiro.
corpo da resposta Olá contém uma secção de propriedades de Olá do dispositivo duplo de Olá:

corpo de Olá da entrada de registo de identidade Olá limitada toohello membro de "Propriedades", por exemplo:

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

Olá códigos de estado possíveis são:

|Estado | Descrição |
| ----- | ----------- |
| 200 | Êxito |
| 429 | Demasiados pedidos (limitados), como por [limitação do IoT Hub][lnk-quotas] |
| 5** | Erros de servidor |

Para obter mais informações, consulte [dispositivos duplos guia para programadores do][lnk-devguide-twin].

### <a name="update-device-twins-reported-properties"></a>Atualizar as propriedades do dispositivo duplo comunicado

Olá sequência seguinte descreve como um dispositivo atualizações Olá comunicadas propriedades no Olá dispositivo duplo na IoT Hub:

1. Um dispositivo tem primeiro de subscrever toohello `$iothub/twin/res/#` respostas da operação do tópico tooreceive Olá do IoT Hub.

1. Um dispositivo envia uma mensagem que contém Olá dispositivo duplo atualização toohello `$iothub/twin/PATCH/properties/reported/?$rid={request id}` tópico. Esta mensagem inclui uma **id do pedido** valor.

1. Olá, serviço, em seguida, envia uma mensagem de resposta que contém Olá novo valor ETag Olá coleção de propriedades comunicado no tópico `$iothub/twin/res/{status}/?$rid={request id}`. Esta mensagem de resposta utiliza Olá mesmo **id do pedido** como pedido Olá.

corpo de mensagem de pedido de Olá contém um documento JSON, que fornece novos valores de propriedades comunicadas (nenhuma propriedade ou metadados podem ser modificados).
Cada membro no documento JSON de Olá atualizações ou adicionar um membro correspondente Olá documento do Olá dispositivo duplo. Um membro definido demasiado`null`, eliminações Olá membro da Olá que contém o objeto. Por exemplo:

        {
            "telemetrySendFrequency": "35m",
            "batteryLevel": 60
        }

Olá códigos de estado possíveis são:

|Estado | Descrição |
| ----- | ----------- |
| 200 | Êxito |
| 400 | Pedido incorreto. JSON com formato incorreto |
| 429 | Demasiados pedidos (limitados), como por [limitação do IoT Hub][lnk-quotas] |
| 5** | Erros de servidor |

Para obter mais informações, consulte [dispositivos duplos guia para programadores do][lnk-devguide-twin].

### <a name="receiving-desired-properties-update-notifications"></a>Receber notificações de atualização de propriedades pretendida

Quando um dispositivo estiver ligado, o IoT Hub envia tópico de toohello notificações `$iothub/twin/PATCH/properties/desired/?$version={new version}`, que contêm conteúdo de Olá da atualização de Olá realizado Olá solução de back-end. Por exemplo:

        {
            "telemetrySendFrequency": "5m",
            "route": null
        }

Para atualizações da propriedade, `null` significa de valores que Olá JSON objeto membro está a ser eliminado.


> [!IMPORTANT] 
> IoT Hub gera notificações de alteração apenas quando os dispositivos estão ligados. Certifique-se de que tooimplement Olá [fluxo de restabelecimento de ligação do dispositivo] [ lnk-devguide-twin-reconnection] tookeep Olá pretendido propriedades sincronizadas entre o IoT Hub e a aplicação de dispositivo Olá.

Para obter mais informações, consulte [dispositivos duplos guia para programadores do][lnk-devguide-twin].

### <a name="respond-tooa-direct-method"></a>Método direto tooa de responder

Em primeiro lugar, um dispositivo tem toosubscribe demasiado`$iothub/methods/POST/#`. IoT Hub envia o tópico do método pedidos toohello `$iothub/methods/POST/{method name}/?$rid={request id}`, com um JSON válido ou uma mensagem vazia.

toorespond, o dispositivo de Olá envia uma mensagem com um JSON válido ou um tópico do corpo vazio toohello `$iothub/methods/res/{status}/?$rid={request id}`, onde **id do pedido** tem toomatch Olá um na mensagem de pedido de Olá, e **estado** tem toobe um número inteiro .

Para obter mais informações, consulte [direcionar método guia para programadores do][lnk-methods].

### <a name="additional-considerations"></a>Considerações adicionais

Como uma consideração final, se precisar de comportamento de protocolo do toocustomize Olá MQTT no lado de nuvem Olá, deve rever Olá [gateway de protocolo do Azure IoT] [ lnk-azure-protocol-gateway] que lhe permitem toodeploy um elevado desempenho gateway de protocolo personalizado que interaja diretamente com o IoT Hub. gateway de protocolo do Azure IoT Olá permite-lhe toocustomize Olá dispositivo protocolo tooaccommodate brownfield MQTT implementações ou outros protocolos personalizados. Esta abordagem requer, no entanto, que executa e operar um gateway de protocolo personalizado.

## <a name="next-steps"></a>Passos seguintes

toolearn mais informações sobre o protocolo MQTT Olá, consulte Olá [documentação MQTT][lnk-mqtt-docs].

toolearn mais sobre o planeamento da sua implementação do IoT Hub, consulte:

* [Certificado do Azure para o catálogo de dispositivos de IoT][lnk-devices]
* [Suporte de protocolos adicionais][lnk-protocols]
* [Comparar com os Event Hubs][lnk-compare]
* [Dimensionamento, HA e DR][lnk-scaling]

toofurther explorar Olá das capacidades do IoT Hub, consulte:

* [Guia para programadores do IoT Hub][lnk-devguide]
* [Simulando um dispositivo com o Azure IoT Edge][lnk-iotedge]

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
