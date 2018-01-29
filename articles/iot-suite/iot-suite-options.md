---
title: "Opções de IoT do Microsoft Azure | Microsoft Docs"
description: "Escolha como pretende implementar a sua solução IoT com o Azure IoT Suite, o Microsoft IoT Central ou o Hub IoT do Azure."
services: 
suite: iot-suite
author: dominicbetts
manager: timlt
ms.assetid: 2d38d08a-4133-4e5c-8b28-f93cadb5df05
ms.service: iot-suite
ms.topic: get-started-article
ms.date: 11/10/2017
ms.author: dobett
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 1a979bde37d247da5c630547924cadbd79c4a6a4
ms.sourcegitcommit: 7edfa9fbed0f9e274209cec6456bf4a689a4c1a6
ms.translationtype: HT
ms.contentlocale: pt-PT
ms.lasthandoff: 01/17/2018
---
# <a name="compare-azure-iot-options"></a>Comparar as opções de IoT do Azure

O artigo [Azure e a Internet das Coisas](iot-suite-what-is-azure-iot.md) descreve uma arquitetura de solução IoT típica, com as camadas seguintes:

* Conectividade e gestão de dispositivos
* Processamento e análise dos dados
* Apresentação e integração empresarial

Para implementar esta arquitetura,o Azure IoT oferece várias opções, cada uma delas adequada para diferentes conjuntos de requisitos de cliente:

* O [Azure IoT Suite](index.md) é uma coleção de nível empresarial de [soluções pré-configuradas](iot-suite-what-are-preconfigured-solutions.md) incorporadas na plataforma-como-um-serviço (PaaS) do Azure, que lhe permite acelerar o desenvolvimento de soluções de IoT personalizadas.

* O [Microsoft IoT Central](https://www.microsoft.com/internet-of-things/iot-central-saas-solutions) é uma solução SaaS (Software-as-a-Service) que utiliza uma abordagem baseada no modelo, que lhe permite criar soluções de IoT de nível empresarial sem a necessidade de conhecimentos de desenvolvimento de soluções na cloud.

## <a name="azure-iot-hub"></a>Azure IoT Hub

O Hub IoT é a principal PaaS do Azure que o Microsoft IoT Central e o Azure IoT Suite utilizam. O Hub IoT permite comunicações bidirecionais fiáveis e seguras entre milhões de dispositivos IoT e um solução na cloud. O Hub IoT ajuda a cumprir os desafios de implementação de IoT, como:

* Conectividade e gestão de dispositivos de volume elevado.
* Ingestão de telemetria de volume elevado.
* Comando e controlo de dispositivos.
* Imposição de segurança do dispositivo.

## <a name="compare-azure-iot-suite-and-microsoft-iot-central"></a>Comparar o Azure IoT Suite e o Microsoft IoT Central

Escolher o produto do Azure IoT é uma parte crítica do planeamento da solução de IoT. O Hub IoT é um serviço do Azure individual que, por si só, não fornece uma solução de IoT ponto a ponto. O Hub IoT pode ser utilizado como um ponto de partida para qualquer solução de IoT e não precisa de utilizar o Azure IoT Suite ou o Centro de IoT da Microsoft para utilizá-lo. Tanto o Azure IoT Suite, como o Microsoft IoT Central utilizam o Hub IoT, juntamente com outros serviços do Azure. A tabela seguinte resume as principais diferenças entre o Azure IoT Suite e o Microsoft IoT Central, para o ajudar a escolher o mais adequado para os seus requisitos:

|                        | Azure IoT Suite | Microsoft IoT Central |
| ---------------------- | --------- | ----------- |
| Utilização principal | Acelerar o desenvolvimento de uma solução de IoT personalizada que precisa da máxima flexibilidade. | Acelerar o tempo de colocação no mercado para soluções de IoT simples que não necessitam de personalização avançada do serviço. |
| Acesso aos serviços PaaS subjacentes          | Tem acesso aos serviços do Azure subjacentes para geri-los ou substituí-los, conforme necessário. | SaaS. Solução totalmente gerida, os serviços subjacentes não são expostos. |
| Flexibilidade            | Elevada. O código para os microsserviços é open source e pode modificá-lo conforme adequado. Além disso, pode personalizar a infraestrutura de implementação.| Média. Pode utilizar a experiência de utilizador baseada no browser incorporado para personalizar o modelo de solução e os aspetos da IU. A infraestrutura não é personalizável porque os diferentes componentes não são expostos.|
| Nível de competência                 | Médio-Elevado. Precisa de competências em Java ou .NET para personalizar o back-end da solução. Precisa de competências em JavaScript para personalizar a visualização. | Baixo. Precisa de competências de modelação para personalizar a solução. Não são necessárias competências de codificação. |
| Experiência de introdução | As soluções pré-configuradas implementam cenários de IoT comuns. Pode ser implementado em segundos. | Os modelos de aplicações e os modelos de dispositivos disponibilizam modelos pré-criados. Pode ser implementado em segundos. |
| Preços                | Pode ajustar os serviços para controlar o custo. | Estrutura de preços simples e previsível. |

A decisão do produto a utilizar para criar a sua solução de IoT é, em última análise, determinada por:

* Os seus requisitos comerciais.
* O tipo de solução que pretende criar
* O conjunto de competências da organização para criar e manter a solução a longo prazo.

## <a name="next-steps"></a>Passos seguintes

Com base no produto e na abordagem escolhidos, os passos seguintes sugeridos são:

* **Azure IoT Suite**: [Quais são as soluções pré-configuradas do Azure IoT?](iot-suite-what-are-preconfigured-solutions.md)
* **Microsoft IoT Central**: [Microsoft IoT Central](https://www.microsoft.com/internet-of-things/iot-central-saas-solutions).
* **Hub IoT**: [ Descrição geral do serviço Hub IoT do Azure](../iot-hub/iot-hub-what-is-iot-hub.md).
