---
title: "Dispositivos SensorTag & Gateway de IoT do Azure - introdução | Microsoft Docs"
description: "Introdução ao IoT Gateway Starter Kit, criar o seu hub IoT do Azure e ligar SensorTag e Gateway toohello do IoT hub"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "hub iot do Azure, gateway de iot, introdução ao hello internet das coisas, iot toolkit"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 56d05f4e-f2c1-4b22-8701-f01e14deead6
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: d8e4057e7774e43c069dd3f2f2e03f098c1ac844
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-iot-gateway-starter-kit-with-a-sensortag"></a>Introdução ao IoT Gateway Starter Kit com um SensorTag

> [!div class="op_single_selector"]
> * [SensorTag](iot-hub-gateway-kit-c-get-started.md)
> * [Dispositivo simulado](iot-hub-gateway-kit-c-sim-get-started.md)

Neste tutorial, começar por learning Olá Noções básicas de trabalhar com [IoT Gateway Starter Kit](https://aka.ms/gateway-kit). Que irá trabalhar com NUC Intel que está a executar Linux vento River e Olá [TI SensorTag](http://www.ti.com/ww/en/wireless_connectivity/sensortag2015/index.html#main). Ficará a saber como tooseamleesly ligar nuvem toohello dispositivos com o IoT Hub do Azure.

***
**Ainda não tem um kit?:** clique [aqui](https://aka.ms/gateway-kit). **Não tem um SensorTag?:** [começar com um dispositivo simulado](iot-hub-gateway-kit-c-sim-get-started.md) ou [comprar um SensorTag](http://www.ti.com/ww/en/wireless_connectivity/sensortag2015/?INTC=SensorTag&HQS=sensortag)
***

## <a name="lesson-1-configure-your-nuc"></a>Lição 1: Configurar o NUC
![Diagrama de ponto a ponto Lesson1](media/iot-hub-gateway-kit-lessons/e2e-lesson1.png)

Este lesson, configurou NUC Intel (seguinte unidade de computação) em Olá Kit como um gateway de IoT do Azure, instalar o pacote de limite de IoT do Azure de Olá no NUC e executar uma funcionalidade de gateway Olá de tooverify de aplicação de exemplo.

*Estimado tempo toocomplete: 15 minutos*

Aceda demasiado[configurar Intel NUC como um gateway de IoT](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md)

## <a name="lesson-2-create-your-iot-hub"></a>Lição 2: Criar um Hub IoT
![Diagrama de ponto a ponto Lesson2](media/iot-hub-gateway-kit-lessons/e2e-lesson2.png)

Este lesson instalou ferramentas Olá e software no computador anfitrião. Em seguida, criar a sua conta gratuita do Azure, aprovisionar o seu hub IoT do Azure e criar o primeiro dispositivo no hub IoT de Olá.

1 Lesson concluída antes de começar este lesson.

### <a name="get-hello-tools"></a>Obtenha as ferramentas de Olá
Instale software e ferramentas de Olá no computador anfitrião.

*Estimado tempo toocomplete: 20 minutos*

Aceda demasiado[obter ferramentas Olá](iot-hub-gateway-kit-c-lesson2-get-the-tools-win32.md)

### <a name="create-an-iot-hub-and-register-your-device"></a>Criar um hub IoT e registar o dispositivo
Criar o grupo de recursos, aprovisionar o seu hub IoT do Azure primeiro e adicionar o primeiro dispositivo toohello IoT hub com Olá CLI do Azure.

*Estimado tempo toocomplete: 10 minutos*

Aceda demasiado[criar um hub IoT e registar o dispositivo](iot-hub-gateway-kit-c-lesson2-register-device.md)

## <a name="lesson-3-receive-messages-from-sensortag-and-read-messages-from-your-iot-hub"></a>Lesson 3: Receber mensagens de SensorTag e ler mensagens do seu IoT hub
Este lesson, vai utilizar configuração de Olá tooautomate de scripts e a execução de uma aplicação de exemplo var no seu gateway. Essas aplicações utilizam uma coleção de dados de transformação e tooaggregate de módulos, processam comandos ou efetuar qualquer número de tarefas relacionadas. Módulos de comunicam entre si através de um mediador de mensagens. aplicação de exemplo de Olá tem um módulo de var e um módulo de hub IoT. módulo de var Olá recebe dados de var SensorTag. Olá, pacotes de módulo de hub IoT dados Olá receberam e envia-tooyour IoT hub através de arquitetura de gateway Olá fornecido no Azure IoT Edge.

![Diagrama de ponto a ponto Lesson 3](media/iot-hub-gateway-kit-lessons/e2e-lesson3.png)

### <a name="configure-and-run-hello-ble-sample-app"></a>Configurar e executar a aplicação de exemplo Olá var
Configure a conectividade de Olá entre SensorTag e o gateway. Em seguida, Concluir configuração Olá e execute a aplicação de exemplo Olá var.

*Estimado tempo toocomplete: 15 minutos*

Aceda demasiado[configurar e executar Olá var aplicação de exemplo](iot-hub-gateway-kit-c-lesson3-configure-ble-app.md)

### <a name="read-messages-from-your-iot-hub"></a>Ler mensagens do seu IoT hub
Execute o código de exemplo no seu anfitrião mensagens tooread de computador do seu IoT hub.

*Estimado tempo toocomplete: 15 minutos*

Aceda demasiado[ler mensagens do seu IoT hub](iot-hub-gateway-kit-c-lesson3-read-messages-from-hub.md)

## <a name="lesson-4-save-messages-tooazure-table-storage"></a>Lesson 4: Guardar mensagens tooAzure o Table storage
Crie uma aplicação de função do Azure que obtém mensagens recebidas a partir do seu IoT hub e escreve-los tooAzure o Table storage.

![Diagrama de ponto a ponto Lesson 4](media/iot-hub-gateway-kit-lessons/e2e-lesson4.png)

### <a name="create-an-azure-function-app-and-azure-storage-account"></a>Criar uma aplicação de função do Azure e a conta de armazenamento do Azure
Utilize um toocreate de modelo Azure Resource Manager, uma aplicação de função do Azure e uma conta de armazenamento do Azure.

*Estimado tempo toocomplete: 10 minutos*

Aceda demasiado[criar uma aplicação de função do Azure e a conta de armazenamento do Azure](iot-hub-gateway-kit-c-lesson4-deploy-resource-manager-template.md)

### <a name="read-messages-persisted-in-azure-table-storage"></a>Mensagens de leitura continuada no armazenamento de tabelas do Azure
Monitorizar as mensagens hello do gateway para a nuvem, eles são escritas tooAzure o Table storage.

*Estimado tempo toocomplete: 5 minutos*

Aceda demasiado[mensagens de leitura continuada no armazenamento de Azure Table](iot-hub-gateway-kit-c-lesson4-read-table-storage.md).

## <a name="troubleshooting"></a>Resolução de problemas
Se tiver quaisquer problemas durante lições Olá, procurar soluções no Olá [resolução de problemas](iot-hub-gateway-kit-c-troubleshooting.md) artigo.

## <a name="explore-more"></a>Explorar mais
Visite Olá [zona de programador do Kit de Gateway de IoT Intel](http://software.intel.com/iot/microsoft-azure) toolearn mais.
