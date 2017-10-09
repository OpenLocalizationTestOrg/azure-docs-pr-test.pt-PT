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
# <a name="device-information-metadata-in-hello-remote-monitoring-preconfigured-solution"></a><span data-ttu-id="08cfe-103">Metadados de informações do dispositivo Olá solução pré-configurada de monitorização remota</span><span class="sxs-lookup"><span data-stu-id="08cfe-103">Device information metadata in hello remote monitoring preconfigured solution</span></span>

<span data-ttu-id="08cfe-104">Olá solução pré-configurada de monitorização remota do Azure IoT Suite demonstra uma abordagem para gerir os metadados do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="08cfe-104">hello Azure IoT Suite remote monitoring preconfigured solution demonstrates an approach for managing device metadata.</span></span> <span data-ttu-id="08cfe-105">Este artigo descreve a abordagem de Olá esta solução assume tooenable toounderstand:</span><span class="sxs-lookup"><span data-stu-id="08cfe-105">This article outlines hello approach this solution takes tooenable you toounderstand:</span></span>

* <span data-ttu-id="08cfe-106">Armazena que solução de Olá de metadados do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="08cfe-106">What device metadata hello solution stores.</span></span>
* <span data-ttu-id="08cfe-107">Como solução de Olá gere Olá metadados do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="08cfe-107">How hello solution manages hello device metadata.</span></span>

## <a name="context"></a><span data-ttu-id="08cfe-108">Contexto</span><span class="sxs-lookup"><span data-stu-id="08cfe-108">Context</span></span>

<span data-ttu-id="08cfe-109">Olá pré-configurada de monitorização remota solução utiliza [IoT Hub do Azure] [ lnk-iot-hub] tooenable toohello de dados de toosend os dispositivos da nuvem.</span><span class="sxs-lookup"><span data-stu-id="08cfe-109">hello remote monitoring preconfigured solution uses [Azure IoT Hub][lnk-iot-hub] tooenable your devices toosend data toohello cloud.</span></span> <span data-ttu-id="08cfe-110">solução Olá armazena informações sobre os dispositivos em três localizações diferentes:</span><span class="sxs-lookup"><span data-stu-id="08cfe-110">hello solution stores information about devices in three different locations:</span></span>

| <span data-ttu-id="08cfe-111">Localização</span><span class="sxs-lookup"><span data-stu-id="08cfe-111">Location</span></span> | <span data-ttu-id="08cfe-112">Informações armazenadas</span><span class="sxs-lookup"><span data-stu-id="08cfe-112">Information stored</span></span> | <span data-ttu-id="08cfe-113">Implementação</span><span class="sxs-lookup"><span data-stu-id="08cfe-113">Implementation</span></span> |
| -------- | ------------------ | -------------- |
| <span data-ttu-id="08cfe-114">Registo de identidade</span><span class="sxs-lookup"><span data-stu-id="08cfe-114">Identity registry</span></span> | <span data-ttu-id="08cfe-115">Id de dispositivo, chaves de autenticação, estado ativado</span><span class="sxs-lookup"><span data-stu-id="08cfe-115">Device id, authentication keys, enabled state</span></span> | <span data-ttu-id="08cfe-116">Incorporada na tooIoT Hub</span><span class="sxs-lookup"><span data-stu-id="08cfe-116">Built in tooIoT Hub</span></span> |
| <span data-ttu-id="08cfe-117">Dispositivos duplos</span><span class="sxs-lookup"><span data-stu-id="08cfe-117">Device twins</span></span> | <span data-ttu-id="08cfe-118">Metadados: propriedades comunicadas propriedades pretendidas, etiquetas</span><span class="sxs-lookup"><span data-stu-id="08cfe-118">Metadata: reported properties, desired properties, tags</span></span> | <span data-ttu-id="08cfe-119">Incorporada na tooIoT Hub</span><span class="sxs-lookup"><span data-stu-id="08cfe-119">Built in tooIoT Hub</span></span> |
| <span data-ttu-id="08cfe-120">Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="08cfe-120">Cosmos DB</span></span> | <span data-ttu-id="08cfe-121">Histórico de comando e o método</span><span class="sxs-lookup"><span data-stu-id="08cfe-121">Command and method history</span></span> | <span data-ttu-id="08cfe-122">Personalizada para soluções</span><span class="sxs-lookup"><span data-stu-id="08cfe-122">Custom for solution</span></span> |

<span data-ttu-id="08cfe-123">O IoT Hub inclui um [registo de identidade de dispositivo] [ lnk-identity-registry] toomanage aceder tooan IoT hub e utiliza [dispositivos duplos] [ lnk-device-twin] toomanage metadados do dispositivo .</span><span class="sxs-lookup"><span data-stu-id="08cfe-123">IoT Hub includes a [device identity registry][lnk-identity-registry] toomanage access tooan IoT hub and uses [device twins][lnk-device-twin] toomanage device metadata.</span></span> <span data-ttu-id="08cfe-124">Há também um remoto monitorização específicos *registo do dispositivo* que armazena o histórico de comando e o método.</span><span class="sxs-lookup"><span data-stu-id="08cfe-124">There is also a remote monitoring solution-specific *device registry* that stores command and method history.</span></span> <span data-ttu-id="08cfe-125">Olá utiliza de solução de monitorização remota uma [Cosmos DB] [ lnk-docdb] tooimplement de base de dados um arquivo personalizado para o histórico de comando e o método.</span><span class="sxs-lookup"><span data-stu-id="08cfe-125">hello remote monitoring solution uses a [Cosmos DB][lnk-docdb] database tooimplement a custom store for command and method history.</span></span>

> [!NOTE]
> <span data-ttu-id="08cfe-126">Olá solução pré-configurada de monitorização remota mantém o registo de identidade de dispositivo Olá, sincronizadas com as informações de Olá na base de dados do Olá BD do Cosmos.</span><span class="sxs-lookup"><span data-stu-id="08cfe-126">hello remote monitoring preconfigured solution keeps hello device identity registry in sync with hello information in hello Cosmos DB database.</span></span> <span data-ttu-id="08cfe-127">Utilizam ambos Olá mesmo toouniquely de id de dispositivo identificar cada dispositivo ligado tooyour IoT hub.</span><span class="sxs-lookup"><span data-stu-id="08cfe-127">Both use hello same device id toouniquely identify each device connected tooyour IoT hub.</span></span>

## <a name="device-metadata"></a><span data-ttu-id="08cfe-128">Metadados do dispositivo</span><span class="sxs-lookup"><span data-stu-id="08cfe-128">Device metadata</span></span>

<span data-ttu-id="08cfe-129">IoT Hub mantém um [dispositivo duplo] [ lnk-device-twin] para cada dispositivo simulado e físico ligado tooa solução de monitorização remota.</span><span class="sxs-lookup"><span data-stu-id="08cfe-129">IoT Hub maintains a [device twin][lnk-device-twin] for each simulated and physical device connected tooa remote monitoring solution.</span></span> <span data-ttu-id="08cfe-130">solução Olá utiliza dispositivos duplos toomanage Olá os metadados associados à dispositivos.</span><span class="sxs-lookup"><span data-stu-id="08cfe-130">hello solution uses device twins toomanage hello metadata associated with devices.</span></span> <span data-ttu-id="08cfe-131">Um dispositivo duplo é um documento JSON mantido pelo IoT Hub e solução Olá utiliza Olá toointeract de API do IoT Hub com dispositivos duplos.</span><span class="sxs-lookup"><span data-stu-id="08cfe-131">A device twin is a JSON document maintained by IoT Hub, and hello solution uses hello IoT Hub API toointeract with device twins.</span></span>

<span data-ttu-id="08cfe-132">Um dispositivo duplo armazena três tipos de metadados:</span><span class="sxs-lookup"><span data-stu-id="08cfe-132">A device twin stores three types of metadata:</span></span>

- <span data-ttu-id="08cfe-133">*Comunicado propriedades* são enviados tooan IoT hub por um dispositivo.</span><span class="sxs-lookup"><span data-stu-id="08cfe-133">*Reported properties* are sent tooan IoT hub by a device.</span></span> <span data-ttu-id="08cfe-134">Na solução de monitorização remota, Olá, dispositivos simulados enviam comunicadas propriedades no arranque e na resposta demasiado**alterar estado do dispositivo** comandos e métodos.</span><span class="sxs-lookup"><span data-stu-id="08cfe-134">In hello remote monitoring solution, simulated devices send reported properties at start-up and in response too**Change device state** commands and methods.</span></span> <span data-ttu-id="08cfe-135">Pode ver as propriedades comunicadas no Olá **lista de dispositivos** e **detalhes do dispositivo** no portal de solução Olá.</span><span class="sxs-lookup"><span data-stu-id="08cfe-135">You can view reported properties in hello **Device list** and **Device details** in hello solution portal.</span></span> <span data-ttu-id="08cfe-136">Propriedades comunicadas são só de leitura.</span><span class="sxs-lookup"><span data-stu-id="08cfe-136">Reported properties are read only.</span></span>
- <span data-ttu-id="08cfe-137">*Pretender propriedades* são obtidos a partir do IoT hub do Olá pelos dispositivos.</span><span class="sxs-lookup"><span data-stu-id="08cfe-137">*Desired properties* are retrieved from hello IoT hub by devices.</span></span> <span data-ttu-id="08cfe-138">É Olá responsabilidade de Olá dispositivo toomake alterar qualquer configuração necessária no dispositivo Olá.</span><span class="sxs-lookup"><span data-stu-id="08cfe-138">It is hello responsibility of hello device toomake any necessary configuration change on hello device.</span></span> <span data-ttu-id="08cfe-139">Também é responsabilidade Olá do hub de back-toohello de alteração tooreport Olá Olá dispositivo como uma propriedade que relatados.</span><span class="sxs-lookup"><span data-stu-id="08cfe-139">It is also hello responsibility of hello device tooreport hello change back toohello hub as a reported property.</span></span> <span data-ttu-id="08cfe-140">Pode definir um valor de propriedade pretendido através do portal de solução Olá.</span><span class="sxs-lookup"><span data-stu-id="08cfe-140">You can set a desired property value through hello solution portal.</span></span>
- <span data-ttu-id="08cfe-141">*Etiquetas* existam apenas no dispositivo duplo de Olá e nunca estão sincronizadas com um dispositivo.</span><span class="sxs-lookup"><span data-stu-id="08cfe-141">*Tags* only exist in hello device twin and are never synchronized with a device.</span></span> <span data-ttu-id="08cfe-142">Pode definir valores de etiqueta no portal de solução Olá e utilizá-los ao filtrar lista Olá de dispositivos.</span><span class="sxs-lookup"><span data-stu-id="08cfe-142">You can set tag values in hello solution portal and use them when you filter hello list of devices.</span></span> <span data-ttu-id="08cfe-143">solução Olá também utiliza uma tag tooidentify Olá ícone toodisplay para um dispositivo no portal de solução Olá.</span><span class="sxs-lookup"><span data-stu-id="08cfe-143">hello solution also uses a tag tooidentify hello icon toodisplay for a device in hello solution portal.</span></span>

<span data-ttu-id="08cfe-144">Exemplo comunicadas as propriedades dos dispositivos Olá simulado incluem o fabricante, número de modelo, latitude e longitude.</span><span class="sxs-lookup"><span data-stu-id="08cfe-144">Example reported properties from hello simulated devices include manufacturer, model number, latitude, and longitude.</span></span> <span data-ttu-id="08cfe-145">Dispositivos simulados Olá também retorno lista de métodos suportados como uma propriedade que relatados.</span><span class="sxs-lookup"><span data-stu-id="08cfe-145">Simulated devices also return hello list of supported methods as a reported property.</span></span>

> [!NOTE]
> <span data-ttu-id="08cfe-146">Olá código de dispositivo simulado utiliza apenas Olá **Desired.Config.TemperatureMeanValue** e **Desired.Config.TelemetryInterval** Olá de tooupdate propriedades pretendido comunicadas propriedades enviadas novamente tooIoT Hub.</span><span class="sxs-lookup"><span data-stu-id="08cfe-146">hello simulated device code only uses hello **Desired.Config.TemperatureMeanValue** and **Desired.Config.TelemetryInterval** desired properties tooupdate hello reported properties sent back tooIoT Hub.</span></span> <span data-ttu-id="08cfe-147">Todos os outros pedidos de alteração de propriedade pretendido são ignorados.</span><span class="sxs-lookup"><span data-stu-id="08cfe-147">All other desired property change requests are ignored.</span></span>

<span data-ttu-id="08cfe-148">Um documento de metadados informações do dispositivo JSON armazenado na base de dados do Olá dispositivo registo Cosmos DB tem Olá seguir a estrutura:</span><span class="sxs-lookup"><span data-stu-id="08cfe-148">A device information metadata JSON document stored in hello device registry Cosmos DB database has hello following structure:</span></span>

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
> <span data-ttu-id="08cfe-149">Informações do dispositivo também podem incluir metadados toodescribe Olá telemetria Olá dispositivo envia tooIoT Hub.</span><span class="sxs-lookup"><span data-stu-id="08cfe-149">Device information can also include metadata toodescribe hello telemetry hello device sends tooIoT Hub.</span></span> <span data-ttu-id="08cfe-150">solução de monitorização remota Olá utiliza este toocustomize de metadados de telemetria como dashboard Olá apresenta [telemetria dinâmica][lnk-dynamic-telemetry].</span><span class="sxs-lookup"><span data-stu-id="08cfe-150">hello remote monitoring solution uses this telemetry metadata toocustomize how hello dashboard displays [dynamic telemetry][lnk-dynamic-telemetry].</span></span>

## <a name="lifecycle"></a><span data-ttu-id="08cfe-151">Ciclo de vida</span><span class="sxs-lookup"><span data-stu-id="08cfe-151">Lifecycle</span></span>

<span data-ttu-id="08cfe-152">Quando cria um dispositivo pela primeira vez no portal de solução Olá, a solução de Olá cria uma entrada no Olá comandos de toostore de base de dados de base de dados do Cosmos e o histórico de método.</span><span class="sxs-lookup"><span data-stu-id="08cfe-152">When you first create a device in hello solution portal, hello solution creates an entry in hello Cosmos DB database toostore command and method history.</span></span> <span data-ttu-id="08cfe-153">Neste momento, a solução de Olá também cria uma entrada para o dispositivo de Olá no registo de identidade do Olá dispositivo, que gera Olá chaves Olá dispositivo utiliza tooauthenticate com o IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="08cfe-153">At this point, hello solution also creates an entry for hello device in hello device identity registry, which generates hello keys hello device uses tooauthenticate with IoT Hub.</span></span> <span data-ttu-id="08cfe-154">Também cria um dispositivo duplo.</span><span class="sxs-lookup"><span data-stu-id="08cfe-154">It also creates a device twin.</span></span>

<span data-ttu-id="08cfe-155">Quando um dispositivo ligado toohello solução pela primeira vez, envia uma mensagem de informações do dispositivo e propriedades comunicadas.</span><span class="sxs-lookup"><span data-stu-id="08cfe-155">When a device first connects toohello solution, it sends reported properties and a device information message.</span></span> <span data-ttu-id="08cfe-156">Olá reportou que os valores de propriedade são guardados automaticamente no dispositivo duplo de Olá.</span><span class="sxs-lookup"><span data-stu-id="08cfe-156">hello reported property values are automatically saved in hello device twin.</span></span> <span data-ttu-id="08cfe-157">Olá comunicadas propriedades incluem o fabricante do dispositivo Olá, o número de modelo, o número de série e uma lista de métodos suportados.</span><span class="sxs-lookup"><span data-stu-id="08cfe-157">hello reported properties include hello device manufacturer, model number, serial number, and a list of supported methods.</span></span> <span data-ttu-id="08cfe-158">mensagem de informações de dispositivo de saudação inclui lista Olá dos comandos Olá dispositivo Olá suporta incluindo informações sobre quaisquer parâmetros de comando.</span><span class="sxs-lookup"><span data-stu-id="08cfe-158">hello device information message includes hello list of hello commands hello device supports including information about any command parameters.</span></span> <span data-ttu-id="08cfe-159">Quando a solução de Olá recebe esta mensagem, atualizações de informações do dispositivo Olá na base de dados do Olá BD do Cosmos.</span><span class="sxs-lookup"><span data-stu-id="08cfe-159">When hello solution receives this message, it updates hello device information in hello Cosmos DB database.</span></span>

### <a name="view-and-edit-device-information-in-hello-solution-portal"></a><span data-ttu-id="08cfe-160">Ver e editar as informações do dispositivo no portal de solução Olá</span><span class="sxs-lookup"><span data-stu-id="08cfe-160">View and edit device information in hello solution portal</span></span>

<span data-ttu-id="08cfe-161">Olá lista de dispositivos no portal de solução Olá apresenta Olá seguintes propriedades do dispositivo como colunas por predefinição: **estado**, **DeviceId**, **fabricante**, **Número de modelo**, **número de série**, **Firmware**, **plataforma**, **processador**e  **Instalado RAM**.</span><span class="sxs-lookup"><span data-stu-id="08cfe-161">hello device list in hello solution portal displays hello following device properties as columns by default: **Status**, **DeviceId**, **Manufacturer**, **Model Number**, **Serial Number**, **Firmware**, **Platform**, **Processor**, and **Installed RAM**.</span></span> <span data-ttu-id="08cfe-162">Pode personalizar as colunas de Olá clicando **editor colunas**.</span><span class="sxs-lookup"><span data-stu-id="08cfe-162">You can customize hello columns by clicking **Column editor**.</span></span> <span data-ttu-id="08cfe-163">Propriedades do dispositivo de Olá **Latitude** e **Longitude** unidade localização Olá Olá mapas Bing no dashboard de Olá.</span><span class="sxs-lookup"><span data-stu-id="08cfe-163">hello device properties **Latitude** and **Longitude** drive hello location in hello Bing Map on hello dashboard.</span></span>

![Editor de colunas na lista de dispositivos][img-device-list]

<span data-ttu-id="08cfe-165">No Olá **detalhes do dispositivo** painel no portal de solução Olá, pode editar as etiquetas e propriedades pretendidas (comunicadas propriedades são só de leitura).</span><span class="sxs-lookup"><span data-stu-id="08cfe-165">In hello **Device Details** pane in hello solution portal, you can edit desired properties and tags (reported properties are read only).</span></span>

![Painel de detalhes do dispositivo][img-device-edit]

<span data-ttu-id="08cfe-167">Pode utilizar tooremove portal de solução Olá um dispositivo da solução.</span><span class="sxs-lookup"><span data-stu-id="08cfe-167">You can use hello solution portal tooremove a device from your solution.</span></span> <span data-ttu-id="08cfe-168">Quando remove um dispositivo, a solução de Olá remove a entrada de dispositivo Olá do registo de identidade e, em seguida, elimina o dispositivo duplo de Olá.</span><span class="sxs-lookup"><span data-stu-id="08cfe-168">When you remove a device, hello solution removes hello device entry from identity registry and then deletes hello device twin.</span></span> <span data-ttu-id="08cfe-169">solução Olá também remove o dispositivo de toohello relacionados de informações da base de dados do Olá BD do Cosmos.</span><span class="sxs-lookup"><span data-stu-id="08cfe-169">hello solution also removes information related toohello device from hello Cosmos DB database.</span></span> <span data-ttu-id="08cfe-170">Antes de poder remover um dispositivo, tem de o desativar.</span><span class="sxs-lookup"><span data-stu-id="08cfe-170">Before you can remove a device, you must disable it.</span></span>

![Remover dispositivo][img-device-remove]

## <a name="device-information-message-processing"></a><span data-ttu-id="08cfe-172">Processamento de mensagens de informações do dispositivo</span><span class="sxs-lookup"><span data-stu-id="08cfe-172">Device information message processing</span></span>

<span data-ttu-id="08cfe-173">As mensagens de informações de dispositivo enviadas por um dispositivo são diferentes das mensagens de telemetria.</span><span class="sxs-lookup"><span data-stu-id="08cfe-173">Device information messages sent by a device are distinct from telemetry messages.</span></span> <span data-ttu-id="08cfe-174">Mensagens de informações do dispositivo incluem comandos Olá que um dispositivo pode responder e nenhum histórico de comando.</span><span class="sxs-lookup"><span data-stu-id="08cfe-174">Device information messages include hello commands a device can respond to, and any command history.</span></span> <span data-ttu-id="08cfe-175">IoT Hub propriamente dito não tem conhecimento de metadados de Olá contidos numa mensagem de informações do dispositivo e processos Olá mensagem Olá mesma forma que processa mensagens de qualquer dispositivo para a nuvem.</span><span class="sxs-lookup"><span data-stu-id="08cfe-175">IoT Hub itself has no knowledge of hello metadata contained in a device information message and processes hello message in hello same way it processes any device-to-cloud message.</span></span> <span data-ttu-id="08cfe-176">Na solução, de monitorização remota Olá um [Azure Stream Analytics] [ lnk-stream-analytics] tarefa (ASA) lê mensagens hello do IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="08cfe-176">In hello remote monitoring solution, an [Azure Stream Analytics][lnk-stream-analytics] (ASA) job reads hello messages from IoT Hub.</span></span> <span data-ttu-id="08cfe-177">Olá **DeviceInfo** filtros para mensagens que contêm de tarefa de stream analytics **"ObjectType": "DeviceInfo"** e reencaminha-os toohello **EventProcessorHost** anfitrião instância que executa uma tarefa de web.</span><span class="sxs-lookup"><span data-stu-id="08cfe-177">hello **DeviceInfo** stream analytics job filters for messages that contain **"ObjectType": "DeviceInfo"** and forwards them toohello **EventProcessorHost** host instance that runs in a web job.</span></span> <span data-ttu-id="08cfe-178">A lógica em Olá **EventProcessorHost** instância utiliza registos de BD do Cosmos de Olá id toofind Olá dispositivos para Olá dispositivo e a atualização Olá registo específicos.</span><span class="sxs-lookup"><span data-stu-id="08cfe-178">Logic in hello **EventProcessorHost** instance uses hello device id toofind hello Cosmos DB record for hello specific device and update hello record.</span></span>

> [!NOTE]
> <span data-ttu-id="08cfe-179">Uma mensagem de informações do dispositivo é uma mensagem de dispositivo para nuvem padrão.</span><span class="sxs-lookup"><span data-stu-id="08cfe-179">A device information message is a standard device-to-cloud message.</span></span> <span data-ttu-id="08cfe-180">solução Olá distingue entre mensagens de telemetria e mensagens de informações do dispositivo utilizando ASA consultas.</span><span class="sxs-lookup"><span data-stu-id="08cfe-180">hello solution distinguishes between device information messages and telemetry messages by using ASA queries.</span></span>

## <a name="next-steps"></a><span data-ttu-id="08cfe-181">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="08cfe-181">Next steps</span></span>

<span data-ttu-id="08cfe-182">Agora que concluiu a aprender como pode personalizar soluções Olá pré-configurada, pode explorar algumas das Olá outras funcionalidades e capacidades das soluções pré-configuradas do IoT Suite de Olá:</span><span class="sxs-lookup"><span data-stu-id="08cfe-182">Now you've finished learning how you can customize hello preconfigured solutions, you can explore some of hello other features and capabilities of hello IoT Suite preconfigured solutions:</span></span>

* <span data-ttu-id="08cfe-183">[Descrição geral de solução pré-configurada de manutenção preditiva][lnk-predictive-overview]</span><span class="sxs-lookup"><span data-stu-id="08cfe-183">[Predictive maintenance preconfigured solution overview][lnk-predictive-overview]</span></span>
* <span data-ttu-id="08cfe-184">[Perguntas mais frequentes sobre o IoT Suite][lnk-faq]</span><span class="sxs-lookup"><span data-stu-id="08cfe-184">[Frequently asked questions for IoT Suite][lnk-faq]</span></span>
* <span data-ttu-id="08cfe-185">[Segurança de IoT a partir de Olá fundo cópias de segurança][lnk-security-groundup]</span><span class="sxs-lookup"><span data-stu-id="08cfe-185">[IoT security from hello ground up][lnk-security-groundup]</span></span>

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
