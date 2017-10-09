---
title: "instruções de manutenção aaaPredictive | Microsoft Docs"
description: "Instruções de manutenção preditiva do Azure IoT Olá solução pré-configurada."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 3c48a716-b805-4c99-8177-414cc4bec3de
ms.service: iot-suite
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: dobett
ms.openlocfilehash: 900d6351019489a8e2f4b98908364e3bd14975c5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="predictive-maintenance-preconfigured-solution-walkthrough"></a>Instruções sobre a solução pré-configurada de manutenção preditiva

solução pré-configurada de manutenção preditiva de Olá é uma solução ponto a ponto para um cenário de negócio que prevê o ponto de Olá em que uma falha é provavelmente toooccur. Pode utilizar, de forma pró-ativa, esta solução pré-configurada para atividades como a manutenção de otimização. solução Olá combina principais serviços do Azure IoT Suite, como o IoT Hub, Stream analytics e um [Azure Machine Learning] [ lnk-machine-learning] área de trabalho. Esta área de trabalho contém um modelo, com base num conjunto de dados de exemplo público, toopredict Olá vida útil restante (RUL) do motor de uma aeronave. solução Olá totalmente implementa o cenário de negócio de IoT Olá como um ponto de partida para tooplan e implementar uma solução que satisfaça as suas próprias necessidades comerciais específicas.

## <a name="logical-architecture"></a>Arquitetura lógica

Olá diagrama a seguir descreve os componentes lógicos de Olá da solução pré-configurada de Olá:

![][img-architecture]

os itens de Olá azul são os serviços do Azure aprovisionados na região de olá onde implementou a solução pré-configurada de Olá. lista de Olá das regiões onde pode implementar a solução pré-configurada de Olá apresenta no Olá [página aprovisionamento][lnk-azureiotsuite].

item de Olá verde é um dispositivo simulado que representa um motor de aeronave. Pode saber mais sobre estes dispositivos simulados em Olá secção a seguir.

Olá itens a cinzento representam componentes que implementam *gestão de dispositivos* capacidades. versão atual do Olá da solução pré-configurada de manutenção preditiva de Olá não Aprovisiona estes recursos. toolearn mais informações sobre a gestão de dispositivos, consulte toohello [solução pré-configurada de monitorização remota][lnk-remote-monitoring].

## <a name="simulated-devices"></a>Dispositivos simulados

Na solução pré-configurada de Olá, um dispositivo simulado representa um motor de aeronave. solução de Olá é aprovisionada com dois motores que mapeiam tooa única aeronave. Cada motor emite quatro tipos de telemetria: Sensor 9, Sensor 11, Sensor 14 e Sensor 15 fornecerem dados de Olá necessários para toocalculate Olá RUL do Machine Learning modelo Olá de motor de Olá. Cada dispositivo simulado envia Olá seguintes mensagens de telemetria tooIoT Hub:

*Ciclo de contagem*. Um ciclo representa um voo concluído com uma duração entre duas a dez horas. Durante o voo Olá, dados de telemetria são capturados a cada meia hora.

*Telemetria*. Existem quatro sensores que representam os atributos do motor. sensores de Olá são geralmente denominados Sensor 9, Sensor 11, Sensor 14 e Sensor 15. Estes quatro sensores representam a telemetria suficiente tooobtain útil os resultados do modelo RUL Olá. modelo de Olá utilizado na solução pré-configurada de Olá é criado a partir de um conjunto de dados público, que inclui dados de sensores do motor. Para obter mais informações sobre como criação do modelo de Olá Olá conjunto de dados original, consulte Olá [modelo de manutenção Cortana Intelligence Gallery preditiva][lnk-cortana-analytics].

dispositivos de Olá simulado podem processar Olá os seguintes comandos enviados a partir do hub IoT de Olá na solução de Olá:

| Comando | Descrição |
| --- | --- |
| StartTelemetry |Controlos Olá estado da simulação Olá.<br/>Inicia Olá dispositivo que envia a telemetria |
| StopTelemetry |Controlos Olá estado da simulação Olá.<br/>Olá, deixa de dispositivo que envia a telemetria |

O IoT Hub reconhece o comando do dispositivo.

## <a name="azure-stream-analytics-job"></a>Tarefa do Azure Stream Analytics

**Tarefa: Telemetria** opera em Olá entrada fluxo telemetria do dispositivo utilizando duas instruções:

* Olá primeiro seleciona todas as telemetrias dos dispositivos Olá e envia esta tooblob de armazenamento de dados. Aqui, serão visualizados na aplicação web de Olá.
* Olá segundo calcula médios do sensor os valores uma dois janela deslizante e envia esses dados através de tooan de hub de eventos de Olá **processador de eventos**.

## <a name="event-processor"></a>Processador de eventos
Olá **anfitrião do processador de eventos** executa uma tarefa de Web do Azure. Olá **processador de eventos** assume os valores médios do sensor de Olá para um ciclo concluído. Em seguida, estes passam tooan esses valores API que expõe Olá de toocalculate de modelo treinado RUL de um motor. Olá API é exposto por uma área de trabalho do Machine Learning que está aprovisionada como parte da solução de Olá.

## <a name="machine-learning"></a>Machine Learning
componente de Machine Learning Olá utiliza um modelo derivado de dados recolhidos a partir dos motores das aeronaves real. Pode navegar toohello área de trabalho de Machine Learning do mosaico de Olá no Olá [azureiotsuite.com] [ lnk-azureiotsuite] página para a sua solução aprovisionada. Olá mosaico está disponível quando está a ser Olá solução Olá **pronto** estado.


## <a name="next-steps"></a>Passos seguintes
Agora que viu componentes chave do Olá da solução pré-configurada de manutenção preditiva de Olá, poderá ser útil toocustomize-lo. Consulte [Guidance on customizing preconfigured solutions (Documentação de orientação sobre como personalizar soluções pré-configuradas)][lnk-customize].

Também pode explorar algumas das Olá outras funcionalidades e capacidades das soluções pré-configuradas do IoT Suite de Olá:

* [Perguntas mais frequentes sobre o IoT Suite][lnk-faq]
* [Segurança de IoT a partir de Olá fundo cópias de segurança][lnk-security-groundup]

[img-architecture]: media/iot-suite-predictive-walkthrough/architecture.png

[lnk-remote-monitoring]: iot-suite-remote-monitoring-sample-walkthrough.md
[lnk-cortana-analytics]: http://gallery.cortanaintelligence.com/Collection/Predictive-Maintenance-Template-3
[lnk-azureiotsuite]: https://www.azureiotsuite.com/
[lnk-customize]: iot-suite-guidance-on-customizing-preconfigured-solutions.md
[lnk-faq]: iot-suite-faq.md
[lnk-security-groundup]: securing-iot-ground-up.md
[lnk-machine-learning]: https://azure.microsoft.com/services/machine-learning/