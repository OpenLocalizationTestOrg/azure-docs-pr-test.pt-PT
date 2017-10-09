---
title: "métodos de direcionar aaaUnderstand IoT Hub do Azure | Microsoft Docs"
description: "Guia para programadores - utilize métodos direta tooinvoke código nos seus dispositivos a partir de uma aplicação de serviço."
services: iot-hub
documentationcenter: .net
author: nberdy
manager: timlt
editor: 
ms.assetid: 9f0535f1-02e6-467a-9fc4-c0950702102d
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: nberdy
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 0d15d44a0c3e1d1cda1669c1ed011c2f932e3d92
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="understand-and-invoke-direct-methods-from-iot-hub"></a><span data-ttu-id="5bd4e-103">Compreender e invocar métodos diretos do IoT Hub</span><span class="sxs-lookup"><span data-stu-id="5bd4e-103">Understand and invoke direct methods from IoT Hub</span></span>
## <a name="overview"></a><span data-ttu-id="5bd4e-104">Descrição geral</span><span class="sxs-lookup"><span data-stu-id="5bd4e-104">Overview</span></span>
<span data-ttu-id="5bd4e-105">IoT Hub dá-lhe métodos direta do capacidade tooinvoke nos dispositivos da nuvem Olá.</span><span class="sxs-lookup"><span data-stu-id="5bd4e-105">IoT Hub gives you ability tooinvoke direct methods on devices from hello cloud.</span></span> <span data-ttu-id="5bd4e-106">Métodos diretos de representar uma interação de pedido-resposta com um dispositivo de tooan semelhante HTTP chamar em que são ou não bem-sucedidos imediatamente (após um tempo limite especificado de um utilizador).</span><span class="sxs-lookup"><span data-stu-id="5bd4e-106">Direct methods represent a request-reply interaction with a device similar tooan HTTP call in that they succeed or fail immediately (after a user-specified timeout).</span></span> <span data-ttu-id="5bd4e-107">Isto é útil para cenários em que é diferente consoante se o dispositivo de Olá era possível toorespond, como o envio de um dispositivo de reativação tooa SMS se um dispositivo estiver offline (SMS a ser mais dispendioso do que uma chamada de método) a Olá ação imediata.</span><span class="sxs-lookup"><span data-stu-id="5bd4e-107">This is useful for scenarios where hello course of immediate action is different depending on whether hello device was able toorespond, such as sending an SMS wake-up tooa device if a device is offline (SMS being more expensive than a method call).</span></span>

<span data-ttu-id="5bd4e-108">Cada método de dispositivo está direcionada para um único dispositivo.</span><span class="sxs-lookup"><span data-stu-id="5bd4e-108">Each device method targets a single device.</span></span> <span data-ttu-id="5bd4e-109">[As tarefas] [ lnk-devguide-jobs] fornecem uma forma tooinvoke métodos diretos em vários dispositivos e agendar a invocação de métodos para dispositivos desligados.</span><span class="sxs-lookup"><span data-stu-id="5bd4e-109">[Jobs][lnk-devguide-jobs] provide a way tooinvoke direct methods on multiple devices, and schedule method invocation for disconnected devices.</span></span>

<span data-ttu-id="5bd4e-110">Qualquer pessoa com **serviço ligar** permissões no IoT Hub podem invocar um método num dispositivo.</span><span class="sxs-lookup"><span data-stu-id="5bd4e-110">Anyone with **service connect** permissions on IoT Hub may invoke a method on a device.</span></span>

### <a name="when-toouse"></a><span data-ttu-id="5bd4e-111">Quando toouse</span><span class="sxs-lookup"><span data-stu-id="5bd4e-111">When toouse</span></span>
<span data-ttu-id="5bd4e-112">Os métodos diretos seguem um padrão de resposta-pedido e destinam-se para as comunicações que necessitam de confirmação imediata do respetivo resultado, o controlo interactivo normalmente de dispositivo Olá, por exemplo tooturn numa ventoinha.</span><span class="sxs-lookup"><span data-stu-id="5bd4e-112">Direct methods follow a request-response pattern and are meant for communications that require immediate confirmation of their result, usually interactive control of hello device, for example tooturn on a fan.</span></span>

<span data-ttu-id="5bd4e-113">Consulte demasiado[orientações de comunicação de nuvem para o dispositivo] [ lnk-c2d-guidance] em caso de dúvida entre a utilização pretendidas propriedades, direcionar a mensagens da nuvem para o dispositivo ou métodos.</span><span class="sxs-lookup"><span data-stu-id="5bd4e-113">Refer too[Cloud-to-device communication guidance][lnk-c2d-guidance] if in doubt between using desired properties, direct methods, or cloud-to-device messages.</span></span>

## <a name="method-lifecycle"></a><span data-ttu-id="5bd4e-114">Ciclo de vida do método</span><span class="sxs-lookup"><span data-stu-id="5bd4e-114">Method lifecycle</span></span>
<span data-ttu-id="5bd4e-115">Métodos diretos são implementados num dispositivo Olá e podem necessitar de zero ou mais entradas no Olá método payload toocorrectly instanciar.</span><span class="sxs-lookup"><span data-stu-id="5bd4e-115">Direct methods are implemented on hello device and may require zero or more inputs in hello method payload toocorrectly instantiate.</span></span> <span data-ttu-id="5bd4e-116">Invocar um método direto através de um URI de serviço com acesso à (`{iot hub}/twins/{device id}/methods/`).</span><span class="sxs-lookup"><span data-stu-id="5bd4e-116">You invoke a direct method through a service-facing URI (`{iot hub}/twins/{device id}/methods/`).</span></span> <span data-ttu-id="5bd4e-117">Um dispositivo recebe métodos diretos através de um tópico MQTT específicos do dispositivo (`$iothub/methods/POST/{method name}/`).</span><span class="sxs-lookup"><span data-stu-id="5bd4e-117">A device receives direct methods through a device-specific MQTT topic (`$iothub/methods/POST/{method name}/`).</span></span> <span data-ttu-id="5bd4e-118">Pode suportamos métodos diretos no lado do dispositivo rede protocolos adicionais no Olá futura.</span><span class="sxs-lookup"><span data-stu-id="5bd4e-118">We may support direct methods on additional device-side networking protocols in hello future.</span></span>

> [!NOTE]
> <span data-ttu-id="5bd4e-119">Quando invocar um método direto num dispositivo, valores e nomes de propriedade podem apenas conter imprimível US-ASCII alfanuméricos, exceto qualquer no seguinte conjunto de Olá: ``{'$', '(', ')', '<', '>', '@', ',', ';', ':', '\', '"', '/', '[', ']', '?', '=', '{', '}', SP, HT}``.</span><span class="sxs-lookup"><span data-stu-id="5bd4e-119">When you invoke a direct method on a device, property names and values can only contain US-ASCII printable alphanumeric, except any in hello following set: ``{'$', '(', ')', '<', '>', '@', ',', ';', ':', '\', '"', '/', '[', ']', '?', '=', '{', '}', SP, HT}``.</span></span>
> 
> 

<span data-ttu-id="5bd4e-120">Direcionar métodos são síncronos e o êxito ou falhar depois do período de tempo limite de Olá (predefinição: 30 segundos, pode ser definidos se too3600 segundos).</span><span class="sxs-lookup"><span data-stu-id="5bd4e-120">Direct methods are synchronous and either succeed or fail after hello timeout period (default: 30 seconds, settable up too3600 seconds).</span></span> <span data-ttu-id="5bd4e-121">Métodos diretos são úteis em cenários interativos onde pretende que um dispositivo tooact se e apenas se o dispositivo de Olá está online e receber comandos, como ativar uma leve do telefone.</span><span class="sxs-lookup"><span data-stu-id="5bd4e-121">Direct methods are useful in interactive scenarios where you want a device tooact if and only if hello device is online and receiving commands, such as turning on a light from a phone.</span></span> <span data-ttu-id="5bd4e-122">Nestes cenários, quer toosee um imediato êxito ou falha para que o serviço em nuvem Olá pode agir em resultado de Olá logo que possível.</span><span class="sxs-lookup"><span data-stu-id="5bd4e-122">In these scenarios, you want toosee an immediate success or failure so hello cloud service can act on hello result as soon as possible.</span></span> <span data-ttu-id="5bd4e-123">dispositivo Olá pode devolver algumas corpo da mensagem em resultado de método Olá, mas não é necessária para Olá método toodo para.</span><span class="sxs-lookup"><span data-stu-id="5bd4e-123">hello device may return some message body as a result of hello method, but it isn't required for hello method toodo so.</span></span> <span data-ttu-id="5bd4e-124">Não há nenhuma garantia na ordenação ou qualquer semântica de concorrência em chamadas de método.</span><span class="sxs-lookup"><span data-stu-id="5bd4e-124">There is no guarantee on ordering or any concurrency semantics on method calls.</span></span>

<span data-ttu-id="5bd4e-125">Método direto são só de HTTP do lado da nuvem de Olá e MQTT apenas do lado do dispositivo de Olá.</span><span class="sxs-lookup"><span data-stu-id="5bd4e-125">Direct method are HTTP-only from hello cloud side, and MQTT-only from hello device side.</span></span>

<span data-ttu-id="5bd4e-126">payload de Olá para pedidos de método e as respostas é um documento JSON segurança too8KB.</span><span class="sxs-lookup"><span data-stu-id="5bd4e-126">hello payload for method requests and responses is a JSON document up too8KB.</span></span>

## <a name="reference-topics"></a><span data-ttu-id="5bd4e-127">Tópicos de referência:</span><span class="sxs-lookup"><span data-stu-id="5bd4e-127">Reference topics:</span></span>
<span data-ttu-id="5bd4e-128">Olá seguintes tópicos de referência, poderá obter mais informações sobre como utilizar métodos diretos.</span><span class="sxs-lookup"><span data-stu-id="5bd4e-128">hello following reference topics provide you with more information about using direct methods.</span></span>

## <a name="invoke-a-direct-method-from-a-back-end-app"></a><span data-ttu-id="5bd4e-129">Invocar um método direto a partir de uma aplicação de back-end</span><span class="sxs-lookup"><span data-stu-id="5bd4e-129">Invoke a direct method from a back-end app</span></span>
### <a name="method-invocation"></a><span data-ttu-id="5bd4e-130">Invocação de métodos</span><span class="sxs-lookup"><span data-stu-id="5bd4e-130">Method invocation</span></span>
<span data-ttu-id="5bd4e-131">Invocações de método direto num dispositivo são chamadas HTTP que incluem:</span><span class="sxs-lookup"><span data-stu-id="5bd4e-131">Direct method invocations on a device are HTTP calls which comprise:</span></span>

* <span data-ttu-id="5bd4e-132">Olá *URI* toohello específico de dispositivo (`{iot hub}/twins/{device id}/methods/`)</span><span class="sxs-lookup"><span data-stu-id="5bd4e-132">hello *URI* specific toohello device (`{iot hub}/twins/{device id}/methods/`)</span></span>
* <span data-ttu-id="5bd4e-133">Olá POST *método*</span><span class="sxs-lookup"><span data-stu-id="5bd4e-133">hello POST *method*</span></span>
* <span data-ttu-id="5bd4e-134">*Cabeçalhos* que contém a autorização de Olá, pedir ID, tipo de conteúdo e codificação de conteúdo</span><span class="sxs-lookup"><span data-stu-id="5bd4e-134">*Headers* which contain hello authorization, request ID, content type, and content encoding</span></span>
* <span data-ttu-id="5bd4e-135">Um JSON transparente *corpo* no Olá seguinte formato:</span><span class="sxs-lookup"><span data-stu-id="5bd4e-135">A transparent JSON *body* in hello following format:</span></span>

```
{
    "methodName": "reboot",
    "responseTimeoutInSeconds": 200,
    "payload": {
        "input1": "someInput",
        "input2": "anotherInput"
    }
}
```

<span data-ttu-id="5bd4e-136">Tempo limite é em segundos.</span><span class="sxs-lookup"><span data-stu-id="5bd4e-136">Timeout is in seconds.</span></span> <span data-ttu-id="5bd4e-137">Se o tempo limite não for definido, será assumida too30 segundos.</span><span class="sxs-lookup"><span data-stu-id="5bd4e-137">If timeout is not set, it defaults too30 seconds.</span></span>

### <a name="response"></a><span data-ttu-id="5bd4e-138">Resposta</span><span class="sxs-lookup"><span data-stu-id="5bd4e-138">Response</span></span>
<span data-ttu-id="5bd4e-139">aplicação de back-end Olá recebe uma resposta que inclui:</span><span class="sxs-lookup"><span data-stu-id="5bd4e-139">hello back-end app receives a response which comprises:</span></span>

* <span data-ttu-id="5bd4e-140">*Código de estado HTTP*, que é utilizado para erros feitos Olá IoT Hub, incluindo um erro 404 para dispositivos atualmente não ligado</span><span class="sxs-lookup"><span data-stu-id="5bd4e-140">*HTTP status code*, which is used for errors coming from hello IoT Hub, including a 404 error for devices not currently connected</span></span>
* <span data-ttu-id="5bd4e-141">*Cabeçalhos* que contém Olá ETag, pedir ID, tipo de conteúdo e codificação de conteúdo</span><span class="sxs-lookup"><span data-stu-id="5bd4e-141">*Headers* which contain hello ETag, request ID, content type, and content encoding</span></span>
* <span data-ttu-id="5bd4e-142">Um JSON *corpo* no Olá seguinte formato:</span><span class="sxs-lookup"><span data-stu-id="5bd4e-142">A JSON *body* in hello following format:</span></span>

```
{
    "status" : 201,
    "payload" : {...}
}
```

   <span data-ttu-id="5bd4e-143">Ambos `status` e `body` são fornecidos pelo dispositivo Olá e utilizado toorespond com o código de estado do dispositivo Olá e/ou a descrição.</span><span class="sxs-lookup"><span data-stu-id="5bd4e-143">Both `status` and `body` are provided by hello device and used toorespond with hello device's own status code and/or description.</span></span>

## <a name="handle-a-direct-method-on-a-device"></a><span data-ttu-id="5bd4e-144">Identificador de um método direto num dispositivo</span><span class="sxs-lookup"><span data-stu-id="5bd4e-144">Handle a direct method on a device</span></span>
### <a name="method-invocation"></a><span data-ttu-id="5bd4e-145">Invocação de métodos</span><span class="sxs-lookup"><span data-stu-id="5bd4e-145">Method invocation</span></span>
<span data-ttu-id="5bd4e-146">Dispositivos recebem pedidos de método direto no tópico MQTT Olá:`$iothub/methods/POST/{method name}/?$rid={request id}`</span><span class="sxs-lookup"><span data-stu-id="5bd4e-146">Devices receive direct method requests on hello MQTT topic: `$iothub/methods/POST/{method name}/?$rid={request id}`</span></span>

<span data-ttu-id="5bd4e-147">corpo de Olá que dispositivo Olá recebe está a ser Olá seguinte formato:</span><span class="sxs-lookup"><span data-stu-id="5bd4e-147">hello body which hello device receives is in hello following format:</span></span>

```
{
    "input1": "someInput",
    "input2": "anotherInput"
}
```

<span data-ttu-id="5bd4e-148">Pedidos de método são QoS 0.</span><span class="sxs-lookup"><span data-stu-id="5bd4e-148">Method requests are QoS 0.</span></span>

### <a name="response"></a><span data-ttu-id="5bd4e-149">Resposta</span><span class="sxs-lookup"><span data-stu-id="5bd4e-149">Response</span></span>
<span data-ttu-id="5bd4e-150">dispositivo de Olá envia respostas demasiado`$iothub/methods/res/{status}/?$rid={request id}`, em que:</span><span class="sxs-lookup"><span data-stu-id="5bd4e-150">hello device sends responses too`$iothub/methods/res/{status}/?$rid={request id}`, where:</span></span>

* <span data-ttu-id="5bd4e-151">Olá `status` propriedade está Olá fornecido pelo dispositivo o estado de execução do método.</span><span class="sxs-lookup"><span data-stu-id="5bd4e-151">hello `status` property is hello device-supplied status of method execution.</span></span>
* <span data-ttu-id="5bd4e-152">Olá `$rid` propriedade é Olá ID do pedido de invocação do método Olá recebida a partir do IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="5bd4e-152">hello `$rid` property is hello request ID from hello method invocation received from IoT Hub.</span></span>

<span data-ttu-id="5bd4e-153">corpo de Olá é definido por dispositivo Olá e pode ser qualquer Estado.</span><span class="sxs-lookup"><span data-stu-id="5bd4e-153">hello body is set by hello device and can be any status.</span></span>

## <a name="additional-reference-material"></a><span data-ttu-id="5bd4e-154">Material de referência adicionais</span><span class="sxs-lookup"><span data-stu-id="5bd4e-154">Additional reference material</span></span>
<span data-ttu-id="5bd4e-155">Outros tópicos de referência Olá guia para programadores do IoT Hub incluem:</span><span class="sxs-lookup"><span data-stu-id="5bd4e-155">Other reference topics in hello IoT Hub developer guide include:</span></span>

* <span data-ttu-id="5bd4e-156">[Pontos finais de IoT Hub] [ lnk-endpoints] descreve Olá vários pontos finais que cada IoT hub expõe para operações de gestão e de tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="5bd4e-156">[IoT Hub endpoints][lnk-endpoints] describes hello various endpoints that each IoT hub exposes for run-time and management operations.</span></span>
* <span data-ttu-id="5bd4e-157">[Limitação e quotas] [ lnk-quotas] descreve quotas Olá que se aplicam toohello serviço IoT Hub e Olá tooexpect limitação do comportamento quando utilizar Olá serviço.</span><span class="sxs-lookup"><span data-stu-id="5bd4e-157">[Throttling and quotas][lnk-quotas] describes hello quotas that apply toohello IoT Hub service and hello throttling behavior tooexpect when you use hello service.</span></span>
* <span data-ttu-id="5bd4e-158">[Azure SDKs IoT do serviço e dispositivo] [ lnk-sdks] listas Olá idioma vários SDKs que pode utilizar ao desenvolver aplicações de serviço e dispositivo que interagem com o IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="5bd4e-158">[Azure IoT device and service SDKs][lnk-sdks] lists hello various language SDKs you can use when you develop both device and service apps that interact with IoT Hub.</span></span>
* <span data-ttu-id="5bd4e-159">[Idioma de consulta do IoT Hub para dispositivos duplos, tarefas e o encaminhamento de mensagens] [ lnk-query] descreve Olá idioma de consulta do IoT Hub pode utilizar informações de tooretrieve a partir do IoT Hub sobre os dispositivos duplos e tarefas.</span><span class="sxs-lookup"><span data-stu-id="5bd4e-159">[IoT Hub query language for device twins, jobs, and message routing][lnk-query] describes hello IoT Hub query language you can use tooretrieve information from IoT Hub about your device twins and jobs.</span></span>
* <span data-ttu-id="5bd4e-160">[Suporte do IoT Hub MQTT] [ lnk-devguide-mqtt] fornece mais informações sobre o suporte do IoT Hub para o protocolo MQTT Olá.</span><span class="sxs-lookup"><span data-stu-id="5bd4e-160">[IoT Hub MQTT support][lnk-devguide-mqtt] provides more information about IoT Hub support for hello MQTT protocol.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5bd4e-161">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="5bd4e-161">Next steps</span></span>
<span data-ttu-id="5bd4e-162">Agora que tem aprendeu como métodos direta de toouse, poderá estar interessado no Olá seguinte tópico de guia de programadores do IoT Hub:</span><span class="sxs-lookup"><span data-stu-id="5bd4e-162">Now you have learned how toouse direct methods, you may be interested in hello following IoT Hub developer guide topic:</span></span>

* <span data-ttu-id="5bd4e-163">[Agenda de tarefas em vários dispositivos][lnk-devguide-jobs]</span><span class="sxs-lookup"><span data-stu-id="5bd4e-163">[Schedule jobs on multiple devices][lnk-devguide-jobs]</span></span>

<span data-ttu-id="5bd4e-164">Se quiser tootry alguns dos conceitos de Olá descritos neste artigo, poderá estar interessado no Olá seguir o tutorial do IoT Hub:</span><span class="sxs-lookup"><span data-stu-id="5bd4e-164">If you would like tootry out some of hello concepts described in this article, you may be interested in hello following IoT Hub tutorial:</span></span>

* <span data-ttu-id="5bd4e-165">[Utilize métodos diretos][lnk-methods-tutorial]</span><span class="sxs-lookup"><span data-stu-id="5bd4e-165">[Use direct methods][lnk-methods-tutorial]</span></span>

<!-- links and images -->

[lnk-endpoints]: iot-hub-devguide-endpoints.md
[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md

[lnk-devguide-jobs]: iot-hub-devguide-jobs.md
[lnk-methods-tutorial]: iot-hub-node-node-direct-methods.md
[lnk-devguide-messages]: iot-hub-devguide-messaging.md
[lnk-c2d-guidance]: iot-hub-devguide-c2d-guidance.md
