---
title: 'Connect Intel EDISON (C) tooAzure IoT - Lesson 4: receber mensagens | Microsoft Docs'
description: "Um exemplo de aplicação é executada em Edison e monitoriza mensagens a receber do seu IoT hub. Uma nova tarefa gulp envia mensagens tooEdison do seu Olá de tooblink do IoT hub LED."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "controlo de arduino guiado da web, controlo de arduino guiado através da web"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-c-get-started
ms.assetid: 820d38f3-d3b8-4249-9e2b-f1b9b771e62f
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: f0424506ff755e0b9514684787b37584d406d320
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="run-a-sample-application-tooreceive-cloud-to-device-messages"></a>Executar um tooreceive de aplicação de exemplo mensagens da nuvem para dispositivo
Neste artigo, implementar uma aplicação de exemplo no Intel Edison. aplicação de exemplo de Olá monitoriza mensagens a receber do seu IoT hub. Executar também uma tarefa gulp no seu tooEdison do computador toosend mensagens do seu IoT hub. Quando a aplicação de exemplo de Olá recebe mensagens hello, fica intermitente Olá LED. Se tiver quaisquer problemas, procurar soluções no Olá [resolução de problemas de página][troubleshooting].

## <a name="what-you-will-do"></a>O que irá fazer
* Ligar Olá exemplo aplicação tooyour do IoT hub.
* Implementar e executar a aplicação de exemplo de Olá.
* Envie mensagens do seu Olá de tooblink tooEdison LED do IoT hub.

## <a name="what-you-will-learn"></a>O que aprenderá
Neste artigo, irá aprender:
* Como toomonitor as mensagens a receber do seu IoT hub.
* Como toosend nuvem para o dispositivo mensagens do seu tooEdison de hub IoT.

## <a name="what-you-need"></a>Do que precisa
* Intel Edison, configurar para utilização. toolearn como tooset segurança Edison, consulte [configurar o dispositivo][configure-your-device].
* Um IoT hub que é criado na sua subscrição do Azure. toolearn como toocreate IoT hub, consulte [criar o seu IoT Hub do Azure][create-your-azure-iot-hub].

## <a name="connect-hello-sample-application-tooyour-iot-hub"></a>Ligar Olá exemplo aplicação tooyour do IoT hub
1. Certifique-se de que está na pasta do repositório de Olá `iot-hub-c-edison-getting-started`. Abra a aplicação de exemplo de Olá no Visual Studio Code executando Olá os seguintes comandos:

   ```bash
   cd Lesson4
   code .
   ```

   ficheiro Olá Olá `app` subpasta é o ficheiro de origem da chave de Olá que contém mensagens hello do código toomonitor recebidos do hub IoT de Olá. Olá `blinkLED` Olá LED fica intermitente de função.

   ![Estrutura de repositório na aplicação de exemplo de Olá][repo-structure]
2. Inicializar o ficheiro de configuração de Olá executando Olá os seguintes comandos:

   ```bash
   npm install
   gulp init
   ```

   Se concluiu passos Olá [criar uma conta de armazenamento e de aplicação de função do Azure] [ create-an-azure-function-app-and-storage-account] neste computador, todas as configurações de Olá são herdadas, para que possa avançar tarefas de toohello Olá passo da implementação e a executar a aplicação de exemplo de Olá. Se concluiu passos Olá [criar uma conta de armazenamento e de aplicação de função do Azure] [ create-an-azure-function-app-and-storage-account] num computador diferente, terá de marcadores de posição do tooreplace Olá no Olá `config-edison.json` ficheiro. Olá `config-edison.json` ficheiro está a ser subpasta Olá da sua pasta raiz.

   ![Conteúdo do ficheiro de configuração edison.json Olá](media/iot-hub-intel-edison-lessons/lesson4/config-edison.png)

   * Substitua **[nome de anfitrião do dispositivo ou endereço IP]** com o endereço IP do dispositivo do Olá marcado como inativo quando configurou o seu dispositivo.
   * Substitua **[cadeia de ligação do dispositivo IoT]** pela cadeia de ligação de dispositivo Olá que obtém executando Olá `az iot device show-connection-string --hub-name {my hub name} --device-id {device id}` comando.
   * Substitua **[cadeia de ligação do hub IoT]** com Olá cadeia de ligação do IoT hub que obtém executando Olá `az iot hub show-connection-string --name {my hub name}` comando.

   > [!NOTE]
   > Executar **gulp ferramentas de instalação** bem, se ainda não o fez, na Lesson 1.

## <a name="deploy-and-run-hello-sample-application"></a>Implementar e executar a aplicação de exemplo de Olá
Implementar e executar aplicações de exemplo de Olá em Edison executando Olá os seguintes comandos:

```bash
gulp deploy && gulp run
```

comando de gulp Olá implementa tooEdison de aplicação de exemplo de Olá. Em seguida, executa aplicação Olá Edison e uma tarefa separada no anfitrião do computador toosend 20 blink mensagens tooEdison do seu IoT hub.

Após a execução da aplicação de exemplo de Olá, começa a escutar toomessages do seu IoT hub. Entretanto, a tarefa de gulp Olá envia várias mensagens "blink" do seu tooEdison de hub IoT. Para cada mensagem blink que recebe Edison, a aplicação de exemplo de Olá chama Olá `blinkLED` Olá de tooblink função LED.

Deverá ver blink LED Olá cada dois segundos como Olá gulp tarefa envia 20 mensagens do seu tooEdison de hub IoT. Olá pela última vez um é uma mensagem de "Parar" deixa de aplicação Olá em execução.

![Aplicação de exemplo com gulp comando e blink mensagens][gulp-command-and-blink-messages]

## <a name="summary"></a>Resumo
Que enviou com êxito as mensagens do seu Olá de tooblink tooEdison LED do IoT hub. tarefa seguinte Olá é opcional: altere Olá e desativar o comportamento de Olá LED.

## <a name="next-steps"></a>Passos seguintes
[Alterar Olá e desativar o comportamento de Olá LED][change-the-on-and-off-behavior-of-the-led]

<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-c-troubleshooting.md
[configure-your-device]: iot-hub-intel-edison-kit-c-lesson1-configure-your-device.md
[create-your-azure-iot-hub]: iot-hub-intel-edison-kit-c-lesson2-prepare-azure-iot-hub.md
[repo-structure]: media/iot-hub-intel-edison-lessons/lesson4/repo_structure_c.png
[create-an-azure-function-app-and-storage-account]: iot-hub-intel-edison-kit-c-lesson3-deploy-resource-manager-template.md
[gulp-command-and-blink-messages]: media/iot-hub-intel-edison-lessons/lesson4/gulp_blink_c.png
[change-the-on-and-off-behavior-of-the-led]: iot-hub-intel-edison-kit-c-lesson4-change-led-behavior.md