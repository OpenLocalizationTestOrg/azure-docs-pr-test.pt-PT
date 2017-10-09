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
# <a name="understand-and-invoke-direct-methods-from-iot-hub"></a>Compreender e invocar métodos diretos do IoT Hub
## <a name="overview"></a>Descrição geral
IoT Hub dá-lhe métodos direta do capacidade tooinvoke nos dispositivos da nuvem Olá. Métodos diretos de representar uma interação de pedido-resposta com um dispositivo de tooan semelhante HTTP chamar em que são ou não bem-sucedidos imediatamente (após um tempo limite especificado de um utilizador). Isto é útil para cenários em que é diferente consoante se o dispositivo de Olá era possível toorespond, como o envio de um dispositivo de reativação tooa SMS se um dispositivo estiver offline (SMS a ser mais dispendioso do que uma chamada de método) a Olá ação imediata.

Cada método de dispositivo está direcionada para um único dispositivo. [As tarefas] [ lnk-devguide-jobs] fornecem uma forma tooinvoke métodos diretos em vários dispositivos e agendar a invocação de métodos para dispositivos desligados.

Qualquer pessoa com **serviço ligar** permissões no IoT Hub podem invocar um método num dispositivo.

### <a name="when-toouse"></a>Quando toouse
Os métodos diretos seguem um padrão de resposta-pedido e destinam-se para as comunicações que necessitam de confirmação imediata do respetivo resultado, o controlo interactivo normalmente de dispositivo Olá, por exemplo tooturn numa ventoinha.

Consulte demasiado[orientações de comunicação de nuvem para o dispositivo] [ lnk-c2d-guidance] em caso de dúvida entre a utilização pretendidas propriedades, direcionar a mensagens da nuvem para o dispositivo ou métodos.

## <a name="method-lifecycle"></a>Ciclo de vida do método
Métodos diretos são implementados num dispositivo Olá e podem necessitar de zero ou mais entradas no Olá método payload toocorrectly instanciar. Invocar um método direto através de um URI de serviço com acesso à (`{iot hub}/twins/{device id}/methods/`). Um dispositivo recebe métodos diretos através de um tópico MQTT específicos do dispositivo (`$iothub/methods/POST/{method name}/`). Pode suportamos métodos diretos no lado do dispositivo rede protocolos adicionais no Olá futura.

> [!NOTE]
> Quando invocar um método direto num dispositivo, valores e nomes de propriedade podem apenas conter imprimível US-ASCII alfanuméricos, exceto qualquer no seguinte conjunto de Olá: ``{'$', '(', ')', '<', '>', '@', ',', ';', ':', '\', '"', '/', '[', ']', '?', '=', '{', '}', SP, HT}``.
> 
> 

Direcionar métodos são síncronos e o êxito ou falhar depois do período de tempo limite de Olá (predefinição: 30 segundos, pode ser definidos se too3600 segundos). Métodos diretos são úteis em cenários interativos onde pretende que um dispositivo tooact se e apenas se o dispositivo de Olá está online e receber comandos, como ativar uma leve do telefone. Nestes cenários, quer toosee um imediato êxito ou falha para que o serviço em nuvem Olá pode agir em resultado de Olá logo que possível. dispositivo Olá pode devolver algumas corpo da mensagem em resultado de método Olá, mas não é necessária para Olá método toodo para. Não há nenhuma garantia na ordenação ou qualquer semântica de concorrência em chamadas de método.

Método direto são só de HTTP do lado da nuvem de Olá e MQTT apenas do lado do dispositivo de Olá.

payload de Olá para pedidos de método e as respostas é um documento JSON segurança too8KB.

## <a name="reference-topics"></a>Tópicos de referência:
Olá seguintes tópicos de referência, poderá obter mais informações sobre como utilizar métodos diretos.

## <a name="invoke-a-direct-method-from-a-back-end-app"></a>Invocar um método direto a partir de uma aplicação de back-end
### <a name="method-invocation"></a>Invocação de métodos
Invocações de método direto num dispositivo são chamadas HTTP que incluem:

* Olá *URI* toohello específico de dispositivo (`{iot hub}/twins/{device id}/methods/`)
* Olá POST *método*
* *Cabeçalhos* que contém a autorização de Olá, pedir ID, tipo de conteúdo e codificação de conteúdo
* Um JSON transparente *corpo* no Olá seguinte formato:

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

Tempo limite é em segundos. Se o tempo limite não for definido, será assumida too30 segundos.

### <a name="response"></a>Resposta
aplicação de back-end Olá recebe uma resposta que inclui:

* *Código de estado HTTP*, que é utilizado para erros feitos Olá IoT Hub, incluindo um erro 404 para dispositivos atualmente não ligado
* *Cabeçalhos* que contém Olá ETag, pedir ID, tipo de conteúdo e codificação de conteúdo
* Um JSON *corpo* no Olá seguinte formato:

```
{
    "status" : 201,
    "payload" : {...}
}
```

   Ambos `status` e `body` são fornecidos pelo dispositivo Olá e utilizado toorespond com o código de estado do dispositivo Olá e/ou a descrição.

## <a name="handle-a-direct-method-on-a-device"></a>Identificador de um método direto num dispositivo
### <a name="method-invocation"></a>Invocação de métodos
Dispositivos recebem pedidos de método direto no tópico MQTT Olá:`$iothub/methods/POST/{method name}/?$rid={request id}`

corpo de Olá que dispositivo Olá recebe está a ser Olá seguinte formato:

```
{
    "input1": "someInput",
    "input2": "anotherInput"
}
```

Pedidos de método são QoS 0.

### <a name="response"></a>Resposta
dispositivo de Olá envia respostas demasiado`$iothub/methods/res/{status}/?$rid={request id}`, em que:

* Olá `status` propriedade está Olá fornecido pelo dispositivo o estado de execução do método.
* Olá `$rid` propriedade é Olá ID do pedido de invocação do método Olá recebida a partir do IoT Hub.

corpo de Olá é definido por dispositivo Olá e pode ser qualquer Estado.

## <a name="additional-reference-material"></a>Material de referência adicionais
Outros tópicos de referência Olá guia para programadores do IoT Hub incluem:

* [Pontos finais de IoT Hub] [ lnk-endpoints] descreve Olá vários pontos finais que cada IoT hub expõe para operações de gestão e de tempo de execução.
* [Limitação e quotas] [ lnk-quotas] descreve quotas Olá que se aplicam toohello serviço IoT Hub e Olá tooexpect limitação do comportamento quando utilizar Olá serviço.
* [Azure SDKs IoT do serviço e dispositivo] [ lnk-sdks] listas Olá idioma vários SDKs que pode utilizar ao desenvolver aplicações de serviço e dispositivo que interagem com o IoT Hub.
* [Idioma de consulta do IoT Hub para dispositivos duplos, tarefas e o encaminhamento de mensagens] [ lnk-query] descreve Olá idioma de consulta do IoT Hub pode utilizar informações de tooretrieve a partir do IoT Hub sobre os dispositivos duplos e tarefas.
* [Suporte do IoT Hub MQTT] [ lnk-devguide-mqtt] fornece mais informações sobre o suporte do IoT Hub para o protocolo MQTT Olá.

## <a name="next-steps"></a>Passos seguintes
Agora que tem aprendeu como métodos direta de toouse, poderá estar interessado no Olá seguinte tópico de guia de programadores do IoT Hub:

* [Agenda de tarefas em vários dispositivos][lnk-devguide-jobs]

Se quiser tootry alguns dos conceitos de Olá descritos neste artigo, poderá estar interessado no Olá seguir o tutorial do IoT Hub:

* [Utilize métodos diretos][lnk-methods-tutorial]

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
