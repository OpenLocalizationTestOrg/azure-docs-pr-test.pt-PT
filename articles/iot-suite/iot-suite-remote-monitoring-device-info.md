---
title: "metadados de informações de aaaDevice na solução de monitorização remota Olá | Microsoft Docs"
description: "Uma descrição da Olá pré-configuradas de IoT do Azure solução monitorização remota e respetiva arquitetura."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 1b334769-103b-4eb0-a293-184f3d1ba9a3
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: dobett
ms.openlocfilehash: 8387b98b8b2ae4934b0c900bc4df37dc17337c60
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="device-information-metadata-in-hello-remote-monitoring-preconfigured-solution"></a>Metadados de informações do dispositivo Olá solução pré-configurada de monitorização remota

Olá solução pré-configurada de monitorização remota do Azure IoT Suite demonstra uma abordagem para gerir os metadados do dispositivo. Este artigo descreve a abordagem de Olá esta solução assume tooenable toounderstand:

* Armazena que solução de Olá de metadados do dispositivo.
* Como solução de Olá gere Olá metadados do dispositivo.

## <a name="context"></a>Contexto

Olá pré-configurada de monitorização remota solução utiliza [IoT Hub do Azure] [ lnk-iot-hub] tooenable toohello de dados de toosend os dispositivos da nuvem. solução Olá armazena informações sobre os dispositivos em três localizações diferentes:

| Localização | Informações armazenadas | Implementação |
| -------- | ------------------ | -------------- |
| Registo de identidade | Id de dispositivo, chaves de autenticação, estado ativado | Incorporada na tooIoT Hub |
| Dispositivos duplos | Metadados: propriedades comunicadas propriedades pretendidas, etiquetas | Incorporada na tooIoT Hub |
| Cosmos DB | Histórico de comando e o método | Personalizada para soluções |

O IoT Hub inclui um [registo de identidade de dispositivo] [ lnk-identity-registry] toomanage aceder tooan IoT hub e utiliza [dispositivos duplos] [ lnk-device-twin] toomanage metadados do dispositivo . Há também um remoto monitorização específicos *registo do dispositivo* que armazena o histórico de comando e o método. Olá utiliza de solução de monitorização remota uma [Cosmos DB] [ lnk-docdb] tooimplement de base de dados um arquivo personalizado para o histórico de comando e o método.

> [!NOTE]
> Olá solução pré-configurada de monitorização remota mantém o registo de identidade de dispositivo Olá, sincronizadas com as informações de Olá na base de dados do Olá BD do Cosmos. Utilizam ambos Olá mesmo toouniquely de id de dispositivo identificar cada dispositivo ligado tooyour IoT hub.

## <a name="device-metadata"></a>Metadados do dispositivo

IoT Hub mantém um [dispositivo duplo] [ lnk-device-twin] para cada dispositivo simulado e físico ligado tooa solução de monitorização remota. solução Olá utiliza dispositivos duplos toomanage Olá os metadados associados à dispositivos. Um dispositivo duplo é um documento JSON mantido pelo IoT Hub e solução Olá utiliza Olá toointeract de API do IoT Hub com dispositivos duplos.

Um dispositivo duplo armazena três tipos de metadados:

- *Comunicado propriedades* são enviados tooan IoT hub por um dispositivo. Na solução de monitorização remota, Olá, dispositivos simulados enviam comunicadas propriedades no arranque e na resposta demasiado**alterar estado do dispositivo** comandos e métodos. Pode ver as propriedades comunicadas no Olá **lista de dispositivos** e **detalhes do dispositivo** no portal de solução Olá. Propriedades comunicadas são só de leitura.
- *Pretender propriedades* são obtidos a partir do IoT hub do Olá pelos dispositivos. É Olá responsabilidade de Olá dispositivo toomake alterar qualquer configuração necessária no dispositivo Olá. Também é responsabilidade Olá do hub de back-toohello de alteração tooreport Olá Olá dispositivo como uma propriedade que relatados. Pode definir um valor de propriedade pretendido através do portal de solução Olá.
- *Etiquetas* existam apenas no dispositivo duplo de Olá e nunca estão sincronizadas com um dispositivo. Pode definir valores de etiqueta no portal de solução Olá e utilizá-los ao filtrar lista Olá de dispositivos. solução Olá também utiliza uma tag tooidentify Olá ícone toodisplay para um dispositivo no portal de solução Olá.

Exemplo comunicadas as propriedades dos dispositivos Olá simulado incluem o fabricante, número de modelo, latitude e longitude. Dispositivos simulados Olá também retorno lista de métodos suportados como uma propriedade que relatados.

> [!NOTE]
> Olá código de dispositivo simulado utiliza apenas Olá **Desired.Config.TemperatureMeanValue** e **Desired.Config.TelemetryInterval** Olá de tooupdate propriedades pretendido comunicadas propriedades enviadas novamente tooIoT Hub. Todos os outros pedidos de alteração de propriedade pretendido são ignorados.

Um documento de metadados informações do dispositivo JSON armazenado na base de dados do Olá dispositivo registo Cosmos DB tem Olá seguir a estrutura:

```json
{
  "DeviceProperties": {
    "DeviceID": "deviceid1",
    "HubEnabledState": null,
    "CreatedTime": "2016-04-25T23:54:01.313802Z",
    "DeviceState": "normal",
    "UpdatedTime": null
    },
  "SystemProperties": {
    "ICCID": null
  },
  "Commands": [],
  "CommandHistory": [],
  "IsSimulatedDevice": false,
  "id": "fe81a81c-bcbc-4970-81f4-7f12f2d8bda8"
}
```

> [!NOTE]
> Informações do dispositivo também podem incluir metadados toodescribe Olá telemetria Olá dispositivo envia tooIoT Hub. solução de monitorização remota Olá utiliza este toocustomize de metadados de telemetria como dashboard Olá apresenta [telemetria dinâmica][lnk-dynamic-telemetry].

## <a name="lifecycle"></a>Ciclo de vida

Quando cria um dispositivo pela primeira vez no portal de solução Olá, a solução de Olá cria uma entrada no Olá comandos de toostore de base de dados de base de dados do Cosmos e o histórico de método. Neste momento, a solução de Olá também cria uma entrada para o dispositivo de Olá no registo de identidade do Olá dispositivo, que gera Olá chaves Olá dispositivo utiliza tooauthenticate com o IoT Hub. Também cria um dispositivo duplo.

Quando um dispositivo ligado toohello solução pela primeira vez, envia uma mensagem de informações do dispositivo e propriedades comunicadas. Olá reportou que os valores de propriedade são guardados automaticamente no dispositivo duplo de Olá. Olá comunicadas propriedades incluem o fabricante do dispositivo Olá, o número de modelo, o número de série e uma lista de métodos suportados. mensagem de informações de dispositivo de saudação inclui lista Olá dos comandos Olá dispositivo Olá suporta incluindo informações sobre quaisquer parâmetros de comando. Quando a solução de Olá recebe esta mensagem, atualizações de informações do dispositivo Olá na base de dados do Olá BD do Cosmos.

### <a name="view-and-edit-device-information-in-hello-solution-portal"></a>Ver e editar as informações do dispositivo no portal de solução Olá

Olá lista de dispositivos no portal de solução Olá apresenta Olá seguintes propriedades do dispositivo como colunas por predefinição: **estado**, **DeviceId**, **fabricante**, **Número de modelo**, **número de série**, **Firmware**, **plataforma**, **processador**e  **Instalado RAM**. Pode personalizar as colunas de Olá clicando **editor colunas**. Propriedades do dispositivo de Olá **Latitude** e **Longitude** unidade localização Olá Olá mapas Bing no dashboard de Olá.

![Editor de colunas na lista de dispositivos][img-device-list]

No Olá **detalhes do dispositivo** painel no portal de solução Olá, pode editar as etiquetas e propriedades pretendidas (comunicadas propriedades são só de leitura).

![Painel de detalhes do dispositivo][img-device-edit]

Pode utilizar tooremove portal de solução Olá um dispositivo da solução. Quando remove um dispositivo, a solução de Olá remove a entrada de dispositivo Olá do registo de identidade e, em seguida, elimina o dispositivo duplo de Olá. solução Olá também remove o dispositivo de toohello relacionados de informações da base de dados do Olá BD do Cosmos. Antes de poder remover um dispositivo, tem de o desativar.

![Remover dispositivo][img-device-remove]

## <a name="device-information-message-processing"></a>Processamento de mensagens de informações do dispositivo

As mensagens de informações de dispositivo enviadas por um dispositivo são diferentes das mensagens de telemetria. Mensagens de informações do dispositivo incluem comandos Olá que um dispositivo pode responder e nenhum histórico de comando. IoT Hub propriamente dito não tem conhecimento de metadados de Olá contidos numa mensagem de informações do dispositivo e processos Olá mensagem Olá mesma forma que processa mensagens de qualquer dispositivo para a nuvem. Na solução, de monitorização remota Olá um [Azure Stream Analytics] [ lnk-stream-analytics] tarefa (ASA) lê mensagens hello do IoT Hub. Olá **DeviceInfo** filtros para mensagens que contêm de tarefa de stream analytics **"ObjectType": "DeviceInfo"** e reencaminha-os toohello **EventProcessorHost** anfitrião instância que executa uma tarefa de web. A lógica em Olá **EventProcessorHost** instância utiliza registos de BD do Cosmos de Olá id toofind Olá dispositivos para Olá dispositivo e a atualização Olá registo específicos.

> [!NOTE]
> Uma mensagem de informações do dispositivo é uma mensagem de dispositivo para nuvem padrão. solução Olá distingue entre mensagens de telemetria e mensagens de informações do dispositivo utilizando ASA consultas.

## <a name="next-steps"></a>Passos seguintes

Agora que concluiu a aprender como pode personalizar soluções Olá pré-configurada, pode explorar algumas das Olá outras funcionalidades e capacidades das soluções pré-configuradas do IoT Suite de Olá:

* [Descrição geral de solução pré-configurada de manutenção preditiva][lnk-predictive-overview]
* [Perguntas mais frequentes sobre o IoT Suite][lnk-faq]
* [Segurança de IoT a partir de Olá fundo cópias de segurança][lnk-security-groundup]

<!-- Images and links -->
[img-device-list]: media/iot-suite-remote-monitoring-device-info/image1.png
[img-device-edit]: media/iot-suite-remote-monitoring-device-info/image2.png
[img-device-remove]: media/iot-suite-remote-monitoring-device-info/image3.png

[lnk-iot-hub]: https://azure.microsoft.com/documentation/services/iot-hub/
[lnk-identity-registry]: ../iot-hub/iot-hub-devguide-identity-registry.md
[lnk-device-twin]: ../iot-hub/iot-hub-devguide-device-twins.md
[lnk-docdb]: https://azure.microsoft.com/documentation/services/documentdb/
[lnk-stream-analytics]: https://azure.microsoft.com/documentation/services/stream-analytics/
[lnk-dynamic-telemetry]: iot-suite-dynamic-telemetry.md

[lnk-predictive-overview]: iot-suite-predictive-overview.md
[lnk-faq]: iot-suite-faq.md
[lnk-security-groundup]: securing-iot-ground-up.md
