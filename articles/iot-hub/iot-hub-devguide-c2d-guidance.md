---
title: "Opções de aaaAzure cloud para dispositivos da IoT Hub | Microsoft Docs"
description: "Guia para programadores - orientações sobre quando toouse direcionar métodos, dispositivo duplo propriedades pretendidas ou mensagens da nuvem para o dispositivo para comunicações de nuvem para o dispositivo."
services: iot-hub
documentationcenter: 
author: fsautomata
manager: timlt
editor: 
ms.assetid: 1ac90923-1edf-4134-bbd4-77fee9b68d24
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/25/2017
ms.author: elioda
ms.openlocfilehash: bb95445054fa2711e34fc1d928c3665e0246c81c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="cloud-to-device-communications-guidance"></a>Orientações de comunicações da nuvem para o dispositivo
IoT Hub fornece três opções para a aplicação de back-end do dispositivo aplicações tooexpose funcionalidade tooa:

* [Direcionar métodos] [ lnk-methods] para comunicações que necessitam de confirmação imediata de resultado de Olá. Métodos diretos são frequentemente utilizados para controlo interactivo dos dispositivos como ativar uma ventoinha.
* [Duplo do pretendido propriedades] [ lnk-twins] para comandos de execução longa destinam a dispositivos de Olá tooput para uma determinada pretendido estado. Por exemplo, o conjunto Olá telemetria enviar minuto do intervalo too30.
* [Mensagens da nuvem para dispositivo] [ lnk-c2d] para a aplicação de dispositivo de toohello notificações unidirecional.

Eis uma comparação detalhada das Olá várias opções de comunicação de nuvem para o dispositivo.

|  | Métodos diretos | Propriedades pretendidas do duplo | Mensagens da nuvem para dispositivo |
| ---- | ------- | ---------- | ---- |
| Cenário | Comando que precise de confirmação imediata, como ativar uma ventoinha. | Comandos de longa execução que se destina a dispositivos de Olá tooput para um determinado estado pretendido. Por exemplo, o conjunto Olá telemetria enviar minuto do intervalo too30. | Aplicação de dispositivo toohello notificações unidirecional. |
| Fluxo de dados | Bidirecional. aplicação de dispositivo Olá pode responder toohello método imediato. Olá solução de back-end recebe resultado Olá reconhecimento do contexto toohello pedido. | Unidirecional. aplicação de dispositivo Olá recebe uma notificação de alteração de propriedade Olá. | Unidirecional. aplicação de dispositivo Olá recebe a mensagem de saudação
| Durabilidade | Não são contactados dispositivos desligados. Olá solução de back-end é notificado que nesse dispositivo Olá não está ligado. | Os valores de propriedade são mantidos no dispositivo duplo de Olá. Dispositivo irão lê-lo no seguinte restabelecimento de ligação. Valores de propriedade são recuperável com Olá [idioma de consulta do IoT Hub][lnk-query]. | As mensagens podem ser mantidas pelo IoT Hub para cópia de segurança too48 horas. |
| Destinos | Utilização de único dispositivo **deviceId**, ou em vários dispositivos com [tarefas][lnk-jobs]. | Utilização de único dispositivo **deviceId**, ou em vários dispositivos com [tarefas][lnk-jobs]. | Único dispositivo por **deviceId**. |
| Tamanho | Cópia de segurança too8KB pedidos e respostas de 8KB. | Máximo pretendido tamanho de propriedades é de 8KB. | Cópia de segurança too64KB mensagens. |
| Frequência | Elevada. Para obter mais informações, consulte [limita do IoT Hub][lnk-quotas]. | Média. Para obter mais informações, consulte [limita do IoT Hub][lnk-quotas]. | Baixa. Para obter mais informações, consulte [limita do IoT Hub][lnk-quotas]. |
| Protocolo | Atualmente disponível apenas quando utilizar MQTT. | Atualmente disponível apenas quando utilizar MQTT. | Disponível em todos os protocolos. Dispositivo tem de inquirir quando utilizar HTTP. |

Saiba como toouse direcionar métodos, propriedades pretendidas e mensagens da nuvem para o dispositivo no Olá seguintes tutoriais:

* [Utilize métodos diretos][lnk-methods-tutorial], para métodos diretos;
* [Utilizar propriedades pretendido tooconfigure dispositivos][lnk-twin-properties], para o dispositivo duplo do pretendido propriedades; 
* [Enviar mensagens da nuvem para dispositivo][lnk-c2d-tutorial], mensagens da nuvem para o dispositivo.

[lnk-twins]: iot-hub-devguide-device-twins.md
[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-jobs]: iot-hub-devguide-jobs.md
[lnk-c2d]: iot-hub-devguide-messages-c2d.md
[lnk-methods]: iot-hub-devguide-direct-methods.md
[lnk-methods-tutorial]: iot-hub-node-node-direct-methods.md
[lnk-twin-properties]: iot-hub-node-node-twin-how-to-configure.md
[lnk-c2d-tutorial]: iot-hub-node-node-c2d.md
