---
title: "Olá aaaUnderstand SDKs IoT do Azure | Microsoft Docs"
description: "Guia para programadores - toohello ligações e informações sobre vários Azure IoT serviço e dispositivo SDKs que pode utilizar toobuild aplicações de dispositivos e aplicações de back-end."
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: c5c9a497-bb03-4301-be2d-00edfb7d308f
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: dobett
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: e319451ca97876666e1c011ee0e1a73d0a0f1ed1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="understand-and-use-azure-iot-sdks"></a><span data-ttu-id="c01f4-103">Compreender e utilizar os SDKs IoT do Azure</span><span class="sxs-lookup"><span data-stu-id="c01f4-103">Understand and use Azure IoT SDKs</span></span>

<span data-ttu-id="c01f4-104">Existem três categorias do SDK para trabalhar com o IoT Hub:</span><span class="sxs-lookup"><span data-stu-id="c01f4-104">There are three categories of SDK for working with IoT Hub:</span></span>

* <span data-ttu-id="c01f4-105">**SDKs do dispositivo** permitem-lhe toobuild aplicações que são executados nos seus dispositivos de IoT.</span><span class="sxs-lookup"><span data-stu-id="c01f4-105">**Device SDKs** enable you toobuild apps that run on your IoT devices.</span></span> <span data-ttu-id="c01f4-106">Estas aplicações enviar o IoT hub tooyour telemetria e, opcionalmente, recebem mensagens do seu IoT hub.</span><span class="sxs-lookup"><span data-stu-id="c01f4-106">These apps send telemetry tooyour IoT hub, and optionally receive messages from your IoT hub.</span></span>

* <span data-ttu-id="c01f4-107">**Serviço SDKs** ativar toomanage o seu IoT hub e, opcionalmente, enviar mensagens tooyour dispositivos de IoT.</span><span class="sxs-lookup"><span data-stu-id="c01f4-107">**Service SDKs** enable you toomanage your IoT hub, and optionally send messages tooyour IoT devices.</span></span>

* <span data-ttu-id="c01f4-108">**Limite de IoT do Azure** permite-lhe toobuild gateways tooenable os dispositivos que não utilize um dos protocolos Olá suportado, ou quando precisa de mensagens de tooprocess no limite de Olá.</span><span class="sxs-lookup"><span data-stu-id="c01f4-108">**Azure IoT Edge** enables you toobuild gateways tooenable devices that don't use one of hello supported protocols, or when you need tooprocess messages on hello edge.</span></span>

<span data-ttu-id="c01f4-109">SDKs são fornecidas toosupport várias linguagens de programação.</span><span class="sxs-lookup"><span data-stu-id="c01f4-109">SDKs are provided toosupport multiple programming languages.</span></span>

## <a name="azure-iot-device-sdks"></a><span data-ttu-id="c01f4-110">SDKs do Azure do dispositivo IoT</span><span class="sxs-lookup"><span data-stu-id="c01f4-110">Azure IoT device SDKs</span></span>

<span data-ttu-id="c01f4-111">Olá SDKs do dispositivo IoT do Microsoft Azure contêm código que facilita a criação de dispositivos e aplicações que ligam tooand são geridas pelos serviços do IoT Hub do Azure.</span><span class="sxs-lookup"><span data-stu-id="c01f4-111">hello Microsoft Azure IoT device SDKs contain code that facilitates building devices and applications that connect tooand are managed by Azure IoT Hub services.</span></span>

<span data-ttu-id="c01f4-112">Olá seguintes SDKs do dispositivo IoT do Azure são toodownload disponível a partir do GitHub:</span><span class="sxs-lookup"><span data-stu-id="c01f4-112">hello following Azure IoT device SDKs are available toodownload from GitHub:</span></span>

* <span data-ttu-id="c01f4-113">[Dispositivos de IoT do Azure SDK para C] [ lnk-c-device-sdk] escritos em ANSI C (C99) para portabilidade e compatibilidade de plataforma abrangente.</span><span class="sxs-lookup"><span data-stu-id="c01f4-113">[Azure IoT device SDK for C][lnk-c-device-sdk] written in ANSI C (C99) for portability and broad platform compatibility.</span></span> <span data-ttu-id="c01f4-114">Existem duas bibliotecas de cliente de dispositivo para C, hello nível baixo **iothub_client** e Olá **serializador**.</span><span class="sxs-lookup"><span data-stu-id="c01f4-114">There are two device client libraries for C, hello low-level **iothub_client** and hello **serializer**.</span></span>
* <span data-ttu-id="c01f4-115">[Dispositivos de IoT do Azure SDK para .NET][lnk-dotnet-device-sdk]</span><span class="sxs-lookup"><span data-stu-id="c01f4-115">[Azure IoT device SDK for .NET][lnk-dotnet-device-sdk]</span></span>
* <span data-ttu-id="c01f4-116">[Dispositivos de IoT do Azure SDK para Java][lnk-java-device-sdk]</span><span class="sxs-lookup"><span data-stu-id="c01f4-116">[Azure IoT device SDK for Java][lnk-java-device-sdk]</span></span>
* <span data-ttu-id="c01f4-117">[Dispositivos de IoT do Azure SDK para Node.js][lnk-node-device-sdk]</span><span class="sxs-lookup"><span data-stu-id="c01f4-117">[Azure IoT device SDK for Node.js][lnk-node-device-sdk]</span></span>
* <span data-ttu-id="c01f4-118">[Dispositivos de IoT do Azure SDK para Python][lnk-python-device-sdk]</span><span class="sxs-lookup"><span data-stu-id="c01f4-118">[Azure IoT device SDK for Python][lnk-python-device-sdk]</span></span>

> [!NOTE]
> <span data-ttu-id="c01f4-119">Consulte Olá Leia-me ficheiros repositórios do GitHub Olá para obter informações sobre como utilizar o idioma e os binários do pacote específico da plataforma gestores tooinstall e dependências no computador de desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="c01f4-119">See hello readme files in hello GitHub repositories for information about using language and platform-specific package managers tooinstall binaries and dependencies on your development machine.</span></span>
> 
> 

### <a name="os-platform-and-hardware-compatibility"></a><span data-ttu-id="c01f4-120">Compatibilidade de plataforma e o hardware do SO</span><span class="sxs-lookup"><span data-stu-id="c01f4-120">OS platform and hardware compatibility</span></span>

<span data-ttu-id="c01f4-121">Para obter mais informações sobre a compatibilidade de SDK com dispositivos de hardware específicos, consulte Olá [Azure certificadas para o catálogo de dispositivos de IoT][lnk-certified].</span><span class="sxs-lookup"><span data-stu-id="c01f4-121">For more information about SDK compatibility with specific hardware devices, see hello [Azure Certified for IoT device catalog][lnk-certified].</span></span>

## <a name="azure-iot-service-sdks"></a><span data-ttu-id="c01f4-122">SDKs de serviço do IoT do Azure</span><span class="sxs-lookup"><span data-stu-id="c01f4-122">Azure IoT service SDKs</span></span>

<span data-ttu-id="c01f4-123">serviço de Azure IoT Olá SDKs contenham toofacilitate código compilar aplicações interagem diretamente com os dispositivos do IoT Hub toomanage e segurança.</span><span class="sxs-lookup"><span data-stu-id="c01f4-123">hello Azure IoT service SDKs contain code toofacilitate building applications that interact directly with IoT Hub toomanage devices and security.</span></span>

<span data-ttu-id="c01f4-124">Olá SDKs de serviço do Azure IoT seguintes são toodownload disponível a partir do GitHub:</span><span class="sxs-lookup"><span data-stu-id="c01f4-124">hello following Azure IoT service SDKs are available toodownload from GitHub:</span></span>

* <span data-ttu-id="c01f4-125">[Serviço de IoT do Azure SDK para .NET][lnk-dotnet-service-sdk]</span><span class="sxs-lookup"><span data-stu-id="c01f4-125">[Azure IoT service SDK for .NET][lnk-dotnet-service-sdk]</span></span>
* <span data-ttu-id="c01f4-126">[Serviço de IoT do Azure SDK para Node.js][lnk-node-service-sdk]</span><span class="sxs-lookup"><span data-stu-id="c01f4-126">[Azure IoT service SDK for Node.js][lnk-node-service-sdk]</span></span>
* <span data-ttu-id="c01f4-127">[Serviço de IoT do Azure SDK para Java][lnk-java-service-sdk]</span><span class="sxs-lookup"><span data-stu-id="c01f4-127">[Azure IoT service SDK for Java][lnk-java-service-sdk]</span></span>
* <span data-ttu-id="c01f4-128">[Serviço de IoT do Azure SDK para Python][lnk-python-service-sdk]</span><span class="sxs-lookup"><span data-stu-id="c01f4-128">[Azure IoT service SDK for Python][lnk-python-service-sdk]</span></span>
* <span data-ttu-id="c01f4-129">[Serviço de IoT do Azure SDK para C][lnk-c-service-sdk]</span><span class="sxs-lookup"><span data-stu-id="c01f4-129">[Azure IoT service SDK for C][lnk-c-service-sdk]</span></span>

> [!NOTE]
> <span data-ttu-id="c01f4-130">Consulte Olá Leia-me ficheiros repositórios do GitHub Olá para obter informações sobre como utilizar o idioma e os binários do pacote específico da plataforma gestores tooinstall e dependências no computador de desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="c01f4-130">See hello readme files in hello GitHub repositories for information about using language and platform-specific package managers tooinstall binaries and dependencies on your development machine.</span></span>

## <a name="azure-iot-edge"></a><span data-ttu-id="c01f4-131">Azure IoT Edge</span><span class="sxs-lookup"><span data-stu-id="c01f4-131">Azure IoT Edge</span></span>

<span data-ttu-id="c01f4-132">Limite de IoT do Azure contém Olá infraestrutura e os módulos toocreate gateway soluções de IoT.</span><span class="sxs-lookup"><span data-stu-id="c01f4-132">Azure IoT Edge contains hello infrastructure and modules toocreate IoT gateway solutions.</span></span> <span data-ttu-id="c01f4-133">Pode expandir o cenário de ponto a ponto do limite de IoT toocreate gateways tooany personalizáveis.</span><span class="sxs-lookup"><span data-stu-id="c01f4-133">You can extend IoT Edge toocreate gateways tailored tooany end-to-end scenario.</span></span>

<span data-ttu-id="c01f4-134">Pode transferir [Azure IoT Edge] [ lnk-iot-edge] a partir do GitHub.</span><span class="sxs-lookup"><span data-stu-id="c01f4-134">You can download [Azure IoT Edge][lnk-iot-edge] from GitHub.</span></span>

## <a name="online-api-reference-documentation"></a><span data-ttu-id="c01f4-135">Documentação de referência de API online</span><span class="sxs-lookup"><span data-stu-id="c01f4-135">Online API reference documentation</span></span>

<span data-ttu-id="c01f4-136">Olá lista seguinte contém documentação de referência do ligações tooonline API para o dispositivo, o serviço e bibliotecas de gateway do Azure IoT:</span><span class="sxs-lookup"><span data-stu-id="c01f4-136">hello following list contains links tooonline API reference documentation for Azure IoT device, service, and gateway libraries:</span></span>

* <span data-ttu-id="c01f4-137">[Internet das coisas (IoT) .NET][lnk-dotnet-ref]</span><span class="sxs-lookup"><span data-stu-id="c01f4-137">[Internet of Things (IoT) .NET][lnk-dotnet-ref]</span></span>
* <span data-ttu-id="c01f4-138">[O IoT Hub REST][lnk-rest-ref]</span><span class="sxs-lookup"><span data-stu-id="c01f4-138">[IoT Hub REST][lnk-rest-ref]</span></span>
* <span data-ttu-id="c01f4-139">[Dispositivos de IoT do Azure SDK para C][lnk-c-ref]</span><span class="sxs-lookup"><span data-stu-id="c01f4-139">[Azure IoT device SDK for C][lnk-c-ref]</span></span>
* <span data-ttu-id="c01f4-140">[Dispositivos de IoT do Azure SDK para Java][lnk-java-ref]</span><span class="sxs-lookup"><span data-stu-id="c01f4-140">[Azure IoT device SDK for Java][lnk-java-ref]</span></span>
* <span data-ttu-id="c01f4-141">[Serviço de IoT do Azure SDK para Java][lnk-java-service-ref]</span><span class="sxs-lookup"><span data-stu-id="c01f4-141">[Azure IoT service SDK for Java][lnk-java-service-ref]</span></span>
* <span data-ttu-id="c01f4-142">[Dispositivos de IoT do Azure SDK para Node.js][lnk-node-ref]</span><span class="sxs-lookup"><span data-stu-id="c01f4-142">[Azure IoT device SDK for Node.js][lnk-node-ref]</span></span>
* <span data-ttu-id="c01f4-143">[Serviço de IoT do Azure SDK para Node.js][lnk-node-service-ref]</span><span class="sxs-lookup"><span data-stu-id="c01f4-143">[Azure IoT service SDK for Node.js][lnk-node-service-ref]</span></span>
* <span data-ttu-id="c01f4-144">[Limite de IoT do Azure][lnk-gateway-ref]</span><span class="sxs-lookup"><span data-stu-id="c01f4-144">[Azure IoT Edge][lnk-gateway-ref]</span></span>

## <a name="next-steps"></a><span data-ttu-id="c01f4-145">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="c01f4-145">Next steps</span></span>

<span data-ttu-id="c01f4-146">Outros tópicos de referência neste guia para programadores do IoT Hub incluem:</span><span class="sxs-lookup"><span data-stu-id="c01f4-146">Other reference topics in this IoT Hub developer guide include:</span></span>

* <span data-ttu-id="c01f4-147">[Pontos finais de IoT Hub][lnk-devguide-endpoints]</span><span class="sxs-lookup"><span data-stu-id="c01f4-147">[IoT Hub endpoints][lnk-devguide-endpoints]</span></span>
* <span data-ttu-id="c01f4-148">[Idioma de consulta do IoT Hub para dispositivos duplos, tarefas e o encaminhamento de mensagens][lnk-devguide-query]</span><span class="sxs-lookup"><span data-stu-id="c01f4-148">[IoT Hub query language for device twins, jobs, and message routing][lnk-devguide-query]</span></span>
* <span data-ttu-id="c01f4-149">[Quotas e limitação][lnk-devguide-quotas]</span><span class="sxs-lookup"><span data-stu-id="c01f4-149">[Quotas and throttling][lnk-devguide-quotas]</span></span>
* <span data-ttu-id="c01f4-150">[Suporte de MQTT do IoT Hub][lnk-devguide-mqtt]</span><span class="sxs-lookup"><span data-stu-id="c01f4-150">[IoT Hub MQTT support][lnk-devguide-mqtt]</span></span>

<!-- Links and images -->

[lnk-c-device-sdk]: https://github.com/Azure/azure-iot-sdk-c
[lnk-c-service-sdk]: https://github.com/Azure/azure-iot-sdk-c/tree/master/iothub_service_client
[lnk-dotnet-device-sdk]: https://github.com/Azure/azure-iot-sdk-csharp/tree/master/device
[lnk-java-device-sdk]: https://github.com/Azure/azure-iot-sdk-java/tree/master/device
[lnk-dotnet-service-sdk]: https://github.com/Azure/azure-iot-sdk-csharp/tree/master/service
[lnk-java-service-sdk]: https://github.com/Azure/azure-iot-sdk-java/tree/master/service
[lnk-node-device-sdk]: https://github.com/Azure/azure-iot-sdk-node/tree/master/device
[lnk-node-service-sdk]: https://github.com/Azure/azure-iot-sdk-node/tree/master/service
[lnk-python-device-sdk]: https://github.com/Azure/azure-iot-sdk-python/tree/master/device
[lnk-python-service-sdk]: https://github.com/Azure/azure-iot-sdk-python/tree/master/service
[lnk-certified]: https://catalog.azureiotsuite.com/
[lnk-iot-edge]: https://github.com/Azure/iot-edge

[lnk-dotnet-ref]: https://docs.microsoft.com/dotnet/api/microsoft.azure.devices
[lnk-c-ref]: https://azure.github.io/azure-iot-sdk-c/index.html
[lnk-java-ref]: https://docs.microsoft.com/java/api/com.microsoft.azure.sdk.iot.device
[lnk-node-ref]: https://azure.github.io/azure-iot-sdk-node/
[lnk-rest-ref]: https://docs.microsoft.com/rest/api/iothub/
[lnk-java-service-ref]: https://docs.microsoft.com/java/api/com.microsoft.azure.sdk.iot.service.auth
[lnk-node-service-ref]: https://azure.github.io/azure-iot-sdk-node/
[lnk-gateway-ref]: http://azure.github.io/iot-edge/api_reference/c/html/

[lnk-devguide-endpoints]: iot-hub-devguide-endpoints.md
[lnk-devguide-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-devguide-query]: iot-hub-devguide-query-language.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md
