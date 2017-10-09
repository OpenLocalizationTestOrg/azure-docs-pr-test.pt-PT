---
featureFlags: usabilla
title: "Ligar Raspberry Pi (nó) tooAzure IoT - Lesson 4: nuvem para o dispositivo | Microsoft Docs"
description: "aplicação de exemplo de Olá é executado no Pi e monitoriza mensagens a receber do seu IoT hub. Uma nova tarefa gulp envia mensagens tooPi do seu Olá de tooblink do IoT hub LED."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: nuvem toodevice, mensagem da nuvem
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: 6ae6539e-1163-4490-8d72-fdf7803e3054
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: d69ded4e30c27378481ab2a4fb9c5b73be7bd44e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="run-hello-sample-application-tooreceive-cloud-to-device-messages"></a>Executar mensagens hello do exemplo aplicação tooreceive nuvem para o dispositivo
Neste artigo, implementar uma aplicação de exemplo em Raspberry Pi 3. aplicação de exemplo de Olá monitoriza mensagens a receber do seu IoT hub. Executar também uma tarefa gulp no seu tooPi do computador toosend mensagens do seu IoT hub. Quando a aplicação de exemplo de Olá recebe mensagens hello, fica intermitente Olá LED. Se tiver quaisquer problemas, procurar soluções no Olá [resolução de problemas de página](iot-hub-raspberry-pi-kit-node-troubleshooting.md).

## <a name="what-you-will-do"></a>O que irá fazer
* Ligar Olá exemplo aplicação tooyour do IoT hub.
* Implementar e executar a aplicação de exemplo de Olá.
* Envie mensagens do seu Olá de tooblink tooPi LED do IoT hub.

## <a name="what-you-will-learn"></a>O que aprenderá
Neste artigo, irá aprender:
* Como toomonitor as mensagens a receber do seu IoT hub
* Como toosend nuvem para o dispositivo mensagens do seu tooPi de hub IoT.

## <a name="what-you-need"></a>Do que precisa
* Raspberry Pi 3, configurar para utilização. toolearn como tooset segurança Pi, consulte [configurar o dispositivo](iot-hub-raspberry-pi-kit-node-lesson1-configure-your-device.md).
* Um IoT hub que é criado na sua subscrição do Azure. toolearn como toocreate IoT hub, consulte [crie o seu IoT hub e registe Raspberry Pi 3](iot-hub-raspberry-pi-kit-node-lesson2-prepare-azure-iot-hub.md).

## <a name="connect-hello-sample-application-tooyour-iot-hub"></a>Ligar Olá exemplo aplicação tooyour do IoT hub
1. Certifique-se de que está na pasta do repositório de Olá `iot-hub-node-raspberrypi-getting-started`. Abra a aplicação de exemplo de Olá no Visual Studio Code executando Olá os seguintes comandos:
   
   ```bash
   cd Lesson4
   code .
   ```
   
   Olá aviso `app.js` ficheiro Olá `app` subpasta. Olá `app.js` ficheiro é o ficheiro de origem da chave de Olá que contém mensagens hello do código toomonitor recebidos do hub IoT de Olá. Olá `blinkLED` Olá LED fica intermitente de função.
   
   ![Estrutura de repositório na aplicação de exemplo de Olá](media/iot-hub-raspberry-pi-lessons/lesson4/repo_structure.png)
2. Inicializar o ficheiro de configuração de Olá utilizando Olá os seguintes comandos:
   
   ```bash
   npm install
   gulp init
   ```
   
   Se concluiu passos Olá [criar uma conta de armazenamento e de aplicação de função do Azure](iot-hub-raspberry-pi-kit-node-lesson3-deploy-resource-manager-template.md) neste computador, todas as configurações de Olá são herdadas, para que possa avançar toohello tarefas de implementação e execução de aplicação de exemplo de Olá. Se concluiu passos Olá [criar uma conta de armazenamento e de aplicação de função do Azure](iot-hub-raspberry-pi-kit-node-lesson3-deploy-resource-manager-template.md) num computador diferente, terá de marcadores de posição do tooreplace Olá no Olá `config-raspberrypi.json` ficheiro. Olá `config-raspberrypi.json` ficheiro está a ser subpasta Olá da sua pasta raiz.
   
   ![Conteúdo do ficheiro de configuração raspberrypi.json Olá](media/iot-hub-raspberry-pi-lessons/lesson4/config_raspberrypi.png)

* Substitua **[nome de anfitrião do dispositivo ou endereço IP]** com o endereço IP Olá do nome de anfitrião Pi ou Olá que obtém executando Olá `devdisco list --eth` comando.
* Substitua **[cadeia de ligação do dispositivo IoT]** pela cadeia de ligação de dispositivo Olá que obtém executando Olá `az iot device show-connection-string --hub-name {my hub name} --device-id {device id} -g iot-sample {resource group name}` comando.
* Substitua **[cadeia de ligação do hub IoT]** com Olá cadeia de ligação do IoT hub que obtém executando Olá `az iot hub show-connection-string --name {my hub name} -g iot-sample {resource group name}` comando.

> [!NOTE]
> Executar **gulp ferramentas de instalação** bem, se ainda não o fez, na Lesson 1.

## <a name="deploy-and-run-hello-sample-application"></a>Implementar e executar a aplicação de exemplo de Olá
Implementar e executar aplicações de exemplo de Olá em Pi executando Olá os seguintes comandos:

```bash
gulp deploy && gulp run
```

comando Olá implementa tooPi de aplicação de exemplo de Olá. Em seguida, executa aplicação Olá Pi e uma tarefa separada no anfitrião do computador toosend 20 blink mensagens tooPi do seu IoT hub.

Após a execução da aplicação de exemplo de Olá, começa a escutar toomessages do seu IoT hub. Entretanto, a tarefa de gulp Olá envia várias mensagens "blink" do seu tooPi de hub IoT. Para cada mensagem blink que recebe Pi, a aplicação de exemplo de Olá chama Olá `blinkLED` Olá de tooblink função LED.

Deverá ver blink LED Olá cada dois segundos como Olá gulp tarefa envia 20 mensagens do seu tooPi de hub IoT. Olá pela última vez um é uma mensagem "Parar" indicar Olá toostop de aplicação em execução.

![Aplicação de exemplo com gulp comando e blink mensagens](media/iot-hub-raspberry-pi-lessons/lesson4/gulp_blink.png)

## <a name="summary"></a>Resumo
Que enviou com êxito as mensagens do seu Olá de tooblink tooPi LED do IoT hub. tarefa seguinte Olá é opcional: altere Olá e desativar o comportamento de Olá LED.

## <a name="next-steps"></a>Passos seguintes
[Alterar Olá e desativar o comportamento de Olá LED](iot-hub-raspberry-pi-kit-node-lesson4-change-led-behavior.md)

