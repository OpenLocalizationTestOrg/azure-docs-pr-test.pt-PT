---
title: gateway de protocolo de IoT aaaAzure | Microsoft Docs
description: "Como toouse IoT do Azure protocolo tooextend IoT Hub as capacidades e gateway protocolo suporte tooenable dispositivos tooconnect tooyour hub utilizando protocolos não suportados nativamente pelo IoT Hub."
services: iot-hub
documentationcenter: 
author: kdotchkoff
manager: timlt
editor: 
ms.assetid: 555e59ae-3136-4533-8ba8-f3a3b6acf648
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/11/2017
ms.author: kdotchko
ms.openlocfilehash: 9cfed30149672d8f7e021a9899192105bbcdd400
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# Suporte de protocolos adicionais para o IoT Hub
IoT Hub do Azure suporta nativamente comunicação através de protocolos de Olá MQTT, AMQP e HTTP. Em alguns casos, os dispositivos ou gateways de campo poderão não ser capaz de toouse um estes protocolos padrão em necessitarão adaptation de protocolo. Nestes casos, pode utilizar um gateway personalizado. Um gateway personalizado pode ativar adaptation de protocolo para pontos finais de IoT Hub ao Data Center bridging Olá tráfego tooand do IoT Hub. Pode utilizar Olá [gateway de protocolo do Azure IoT](https://github.com/Azure/azure-iot-protocol-gateway/blob/master/README.md) como um adaptation de protocolo de tooenable gateway personalizado para o IoT Hub.

## Gateway de protocolo do IoT do Azure
gateway de protocolo do Azure IoT Olá é uma estrutura para adaptation de protocolo que foi concebido para alta escala, comunicação do dispositivo bidirecional com o IoT Hub. gateway de protocolo de Olá é um componente de pass-through que aceita ligações de dispositivos através de um protocolo específico. -Pontes Olá tráfego tooIoT Hub através de AMQP 1.0. gateway de protocolo do Azure IoT Olá está disponível como uma flexibilidade de tooprovide do projeto de software open source para adicionar suporte para vários protocolos e as versões de protocolo.

Pode implementar o gateway de protocolo de Olá no Azure de uma forma altamente dimensionável, utilizando o Azure Service Fabric, as funções de trabalho do Cloud Services do Azure ou máquinas virtuais do Windows. Além disso, o gateway de protocolo de Olá pode ser implementado em ambientes no local, tais como gateways de campo.

gateway de protocolo do Azure IoT Olá inclui um adaptador de protocolo MQTT permite-lhe toocustomize Olá comportamento de protocolo MQTT se necessário. Uma vez que o IoT Hub fornece suporte incorporado para o protocolo do Olá MQTT v 3.1.1, deve apenas de considerar a utilização de placa de protocolo MQTT Olá se são necessários as personalizações de protocolo ou requisitos específicos para funcionalidades adicionais.

adaptador MQTT Olá também demonstra o modelo de programação Olá para a criação de adaptadores de protocolo para outros protocolos. Além disso, modelo de gateway de protocolo IoT do Azure do Olá programação permite especializada tooplug nos componentes personalizados para processamento como autenticação personalizada, transformações de mensagem, compressão/descompressão ou encriptação/desencriptação de tráfego entre os dispositivos de Olá e IoT Hub.

Flexibilidade, gateway de protocolo de Olá e implementação de MQTT são fornecidos num projeto software open source. Isto permite-lhe toocustomize implementação de Olá conforme necessário.

## Passos seguintes
mais informações sobre o gateway de protocolo do Azure IoT Olá toolearn e como toouse e implementá-la como parte da solução IoT, consulte:

* [Repositório de gateway do IoT protocolo do Azure no GitHub](https://github.com/Azure/azure-iot-protocol-gateway/blob/master/README.md)
* [Guia do Programador de gateway de protocolo do Azure IoT](https://github.com/Azure/azure-iot-protocol-gateway/blob/master/docs/DeveloperGuide.md)

toolearn mais sobre o planeamento da sua implementação do IoT Hub, consulte:

* [Comparar com os Event Hubs][lnk-compare]
* [Dimensionamento, HA e DR][lnk-scaling]
* [Guia para programadores do IoT Hub][lnk-devguide]

[lnk-compare]: iot-hub-compare-event-hubs.md
[lnk-scaling]: iot-hub-scaling.md
[lnk-devguide]: iot-hub-devguide.md
