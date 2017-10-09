---
title: dimensionamento do aaaAzure IoT Hub | Microsoft Docs
description: "Como tooscale sua toosupport de hub IoT o débito de mensagem previsto. Inclui um resumo das opções de fragmentação e débito Olá suportado para cada camada."
services: iot-hub
documentationcenter: 
author: fsautomata
manager: timlt
editor: 
ms.assetid: e7bd4968-db46-46cf-865d-9c944f683832
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: elioda
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 3b8bf6c44631c65b34b69752d9043c21db24bb01
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="scale-your-iot-hub-solution"></a><span data-ttu-id="44713-104">Dimensionar a sua solução de hub IoT</span><span class="sxs-lookup"><span data-stu-id="44713-104">Scale your IoT hub solution</span></span>
<span data-ttu-id="44713-105">IoT Hub do Azure pode suportar dispositivos ligados em simultâneo milhões de tooa.</span><span class="sxs-lookup"><span data-stu-id="44713-105">Azure IoT Hub can support up tooa million simultaneously connected devices.</span></span> <span data-ttu-id="44713-106">Para obter mais informações, consulte [IoT Hub preços][lnk-pricing].</span><span class="sxs-lookup"><span data-stu-id="44713-106">For more information, see [IoT Hub pricing][lnk-pricing].</span></span> <span data-ttu-id="44713-107">Cada unidade de IoT Hub permite que um determinado número de mensagens diárias.</span><span class="sxs-lookup"><span data-stu-id="44713-107">Each IoT Hub unit allows a certain number of daily messages.</span></span>

<span data-ttu-id="44713-108">tooproperly dimensionar a sua solução, considere a utilização do IoT Hub específica.</span><span class="sxs-lookup"><span data-stu-id="44713-108">tooproperly scale your solution, consider your particular use of IoT Hub.</span></span> <span data-ttu-id="44713-109">Em particular, considere o débito de pico Olá necessário para Olá seguintes categorias de operações:</span><span class="sxs-lookup"><span data-stu-id="44713-109">In particular, consider hello required peak throughput for hello following categories of operations:</span></span>

* <span data-ttu-id="44713-110">Mensagens do dispositivo para a cloud</span><span class="sxs-lookup"><span data-stu-id="44713-110">Device-to-cloud messages</span></span>
* <span data-ttu-id="44713-111">Mensagens da nuvem para dispositivo</span><span class="sxs-lookup"><span data-stu-id="44713-111">Cloud-to-device messages</span></span>
* <span data-ttu-id="44713-112">Operações de registo de identidade</span><span class="sxs-lookup"><span data-stu-id="44713-112">Identity registry operations</span></span>

<span data-ttu-id="44713-113">Informações de débito toothis de adição, consulte [quotas do IoT Hub e limitações] [ IoT Hub quotas and throttles] e estruturar a solução em conformidade.</span><span class="sxs-lookup"><span data-stu-id="44713-113">In addition toothis throughput information, see [IoT Hub quotas and throttles][IoT Hub quotas and throttles] and design your solution accordingly.</span></span>

## <a name="device-to-cloud-and-cloud-to-device-message-throughput"></a><span data-ttu-id="44713-114">Débito de mensagens do dispositivo para nuvem e da nuvem para o dispositivo</span><span class="sxs-lookup"><span data-stu-id="44713-114">Device-to-cloud and cloud-to-device message throughput</span></span>
<span data-ttu-id="44713-115">Olá melhor forma toosize uma solução de IoT Hub é o tráfego de Olá tooevaluate numa base por unidade.</span><span class="sxs-lookup"><span data-stu-id="44713-115">hello best way toosize an IoT Hub solution is tooevaluate hello traffic on a per-unit basis.</span></span>

<span data-ttu-id="44713-116">Mensagens do dispositivo para nuvem siga estas diretrizes de débito constante.</span><span class="sxs-lookup"><span data-stu-id="44713-116">Device-to-cloud messages follow these sustained throughput guidelines.</span></span>

| <span data-ttu-id="44713-117">Escalão</span><span class="sxs-lookup"><span data-stu-id="44713-117">Tier</span></span> | <span data-ttu-id="44713-118">Débito constante</span><span class="sxs-lookup"><span data-stu-id="44713-118">Sustained throughput</span></span> | <span data-ttu-id="44713-119">Velocidade de envio constante</span><span class="sxs-lookup"><span data-stu-id="44713-119">Sustained send rate</span></span> |
| --- | --- | --- |
| <span data-ttu-id="44713-120">S1</span><span class="sxs-lookup"><span data-stu-id="44713-120">S1</span></span> |<span data-ttu-id="44713-121">Cópia de segurança too1111 KB por minuto por unidade</span><span class="sxs-lookup"><span data-stu-id="44713-121">Up too1111 KB/minute per unit</span></span><br/><span data-ttu-id="44713-122">(1,5 GB/dia/unidade)</span><span class="sxs-lookup"><span data-stu-id="44713-122">(1.5 GB/day/unit)</span></span> |<span data-ttu-id="44713-123">Média de mensagens por minuto 278 por unidade</span><span class="sxs-lookup"><span data-stu-id="44713-123">Average of 278 messages/minute per unit</span></span><br/><span data-ttu-id="44713-124">(um máximo de 400.000 mensagens diário por unidade)</span><span class="sxs-lookup"><span data-stu-id="44713-124">(400,000 messages/day per unit)</span></span> |
| <span data-ttu-id="44713-125">S2</span><span class="sxs-lookup"><span data-stu-id="44713-125">S2</span></span> |<span data-ttu-id="44713-126">Cópia de segurança too16 MB por minuto por unidade</span><span class="sxs-lookup"><span data-stu-id="44713-126">Up too16 MB/minute per unit</span></span><br/><span data-ttu-id="44713-127">(22.8 GB/dia/unidade)</span><span class="sxs-lookup"><span data-stu-id="44713-127">(22.8 GB/day/unit)</span></span> |<span data-ttu-id="44713-128">Média de mensagens por minuto 4,167 por unidade</span><span class="sxs-lookup"><span data-stu-id="44713-128">Average of 4,167 messages/minute per unit</span></span><br/><span data-ttu-id="44713-129">(milhões de 6 mensagens diário por unidade)</span><span class="sxs-lookup"><span data-stu-id="44713-129">(6 million messages/day per unit)</span></span> |
| <span data-ttu-id="44713-130">S3</span><span class="sxs-lookup"><span data-stu-id="44713-130">S3</span></span> |<span data-ttu-id="44713-131">Cópia de segurança too814 MB por minuto por unidade</span><span class="sxs-lookup"><span data-stu-id="44713-131">Up too814 MB/minute per unit</span></span><br/><span data-ttu-id="44713-132">(1144.4 GB/dia/unidade)</span><span class="sxs-lookup"><span data-stu-id="44713-132">(1144.4 GB/day/unit)</span></span> |<span data-ttu-id="44713-133">Média de mensagens por minuto 208,333 por unidade</span><span class="sxs-lookup"><span data-stu-id="44713-133">Average of 208,333 messages/minute per unit</span></span><br/><span data-ttu-id="44713-134">(milhões de 300 mensagens diário por unidade)</span><span class="sxs-lookup"><span data-stu-id="44713-134">(300 million messages/day per unit)</span></span> |

## <a name="identity-registry-operation-throughput"></a><span data-ttu-id="44713-135">Débito de operação de registo de identidade</span><span class="sxs-lookup"><span data-stu-id="44713-135">Identity registry operation throughput</span></span>
<span data-ttu-id="44713-136">Operações de registo de identidade do IoT Hub não são supostas toobe operações de tempo de execução, conforme forem principalmente relacionada toodevice aprovisionamento.</span><span class="sxs-lookup"><span data-stu-id="44713-136">IoT Hub identity registry operations are not supposed toobe run-time operations, as they are mostly related toodevice provisioning.</span></span>

<span data-ttu-id="44713-137">Para números de desempenho de rajada específicos, consulte [quotas do IoT Hub e limitações][IoT Hub quotas and throttles].</span><span class="sxs-lookup"><span data-stu-id="44713-137">For specific burst performance numbers, see [IoT Hub quotas and throttles][IoT Hub quotas and throttles].</span></span>

## <a name="sharding"></a><span data-ttu-id="44713-138">Fragmentação</span><span class="sxs-lookup"><span data-stu-id="44713-138">Sharding</span></span>
<span data-ttu-id="44713-139">Embora um único IoT hub pode dimensionar toomillions dos dispositivos, por vezes, a solução requer características de desempenho específica que não pode garantir que um único IoT hub.</span><span class="sxs-lookup"><span data-stu-id="44713-139">While a single IoT hub can scale toomillions of devices, sometimes your solution requires specific performance characteristics that a single IoT hub cannot guarantee.</span></span> <span data-ttu-id="44713-140">Nesse caso, é recomendado que partição os seus dispositivos para vários os hubs IoT.</span><span class="sxs-lookup"><span data-stu-id="44713-140">In that case, it is recommended that you partition your devices into multiple IoT hubs.</span></span> <span data-ttu-id="44713-141">Vários aos hubs IoT uniforme bursts de tráfego e obter débito necessário Olá ou taxas de operação que são necessárias.</span><span class="sxs-lookup"><span data-stu-id="44713-141">Multiple IoT hubs smooth traffic bursts and obtain hello required throughput or operation rates that are required.</span></span>

## <a name="next-steps"></a><span data-ttu-id="44713-142">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="44713-142">Next steps</span></span>
<span data-ttu-id="44713-143">toofurther explorar Olá das capacidades do IoT Hub, consulte:</span><span class="sxs-lookup"><span data-stu-id="44713-143">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="44713-144">[Guia para programadores do IoT Hub][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="44713-144">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="44713-145">[Simulando um dispositivo com o Azure IoT Edge][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="44713-145">[Simulating a device with Azure IoT Edge][lnk-iotedge]</span></span>

[lnk-pricing]: https://azure.microsoft.com/pricing/details/iot-hub
[IoT Hub quotas and throttles]: iot-hub-devguide-quotas-throttling.md

[lnk-devguide]: iot-hub-devguide.md
[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
