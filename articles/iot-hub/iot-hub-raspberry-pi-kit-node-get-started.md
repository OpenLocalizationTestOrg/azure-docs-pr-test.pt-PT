---
title: aaaRaspberry Pi toocloud (Node.js) - ligar Raspberry Pi tooAzure IoT Hub | Microsoft Docs
description: Saiba como toosetup e ligar Raspberry Pi tooAzure IoT Hub para a plataforma de nuvem do Azure do Raspberry Pi toosend dados toohello neste tutorial.
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: iot do Azure raspberry pi, raspberry pi iot hub, raspberry pi enviar dados toocloud, raspberry pi toocloud
ms.assetid: b0e14bfa-8e64-440a-a6ec-e507ca0f76ba
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 5/27/2017
ms.author: xshi
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 57a15ab3984021a9c18ff0aa1316a4d4c6ebdec1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="connect-raspberry-pi-tooazure-iot-hub-nodejs"></a>Ligar Raspberry Pi tooAzure IoT Hub (Node.js)

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

Neste tutorial, começar por Olá Noções básicas de trabalhar com Raspberry Pi que está a executar Raspbian de aprendizagem. Em seguida, saiba como tooseamlessly ligar a sua nuvem toohello de dispositivos utilizando [IoT Hub do Azure](iot-hub-what-is-iot-hub.md). Para exemplos do Windows 10 IoT Core, visite toohello [Windows Dev Center](http://www.windowsondevices.com/).

Não tem um kit ainda? Tente [simulador online Raspberry Pi](iot-hub-raspberry-pi-web-simulator-get-started.md). Ou comprar um novo kit [aqui](https://azure.microsoft.com/develop/iot/starter-kits).


## <a name="what-you-do"></a>O que fazer

* Crie um hub IoT.
* Registe um dispositivo para Pi no seu IoT hub.
* A configuração Raspberry Pi.
* Execute um exemplo de aplicação no Pi toosend sensor dados tooyour do IoT hub.

Ligar Raspberry Pi tooan do IoT hub que criou. Em seguida, executar uma aplicação de exemplo nos dados relativos à temperatura e humidade do toocollect Pi a partir de um sensor BME280. Por fim, enviar Olá sensor dados tooyour do IoT hub.

## <a name="what-you-learn"></a>O que irá aprender

* Como toocreate um hub IoT do Azure e obter a cadeia de ligação do novo dispositivo.
* Como tooconnect Pi com um sensor BME280.
* Como dados de sensores de toocollect ao executar uma aplicação de exemplo no Pi.
* Como toosend sensor dados tooyour do IoT hub.

## <a name="what-you-need"></a>Do que precisa

![Do que precisa](media/iot-hub-raspberry-pi-kit-node-get-started/0_starter_kit.jpg)

* Olá quadro Raspberry Pi 2 ou 3 do Raspberry Pi.
* Uma subscrição ativa do Azure. Se não tiver uma conta do Azure, [criar uma conta de avaliação gratuita do Azure](https://azure.microsoft.com/free/) em apenas alguns minutos.
* Um monitor, um teclado USB e um rato que se ligam tooPi.
* Um Mac ou num PC com Windows ou Linux.
* Uma ligação à Internet.
* Um 16 GB ou superior cartão microSD.
* Um USB SD adaptador ou microSD cartão tooburn Olá imagem do sistema operativo no cartão microSD de Olá.
* Forneça uma potência de 2 amp 5 volt com o cabo USB micro do Olá 6 online.

Olá seguintes itens é opcional:

* Um assembled Adafruit BME280 temperatura, pressão e humidade sensor.
* Um breadboard.
* Cablagem de jumper 6 F/M.
* Um diffused LED 10 mm.


> [!NOTE] 
Estes itens são opcionais, porque o suporte de exemplo de código Olá simulated dados de sensores.

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="setup-raspberry-pi"></a>Configurar Raspberry Pi

### <a name="install-hello-raspbian-operating-system-for-pi"></a>Instalar o sistema de operativo Olá Raspbian para Pi

Prepare o cartão microSD de Olá para a instalação da imagem de Raspbian Olá.

1. Transferir Raspbian.
   1. [Transferir Raspbian Jessie com ambiente de trabalho](https://www.raspberrypi.org/downloads/raspbian/) (ficheiro. zip de Olá).
   1. Extrair Olá Raspbian imagem tooa pasta do computador.
1. Instale Raspbian toohello microSD cartão.
   1. [Transfira e instale o utilitário de burner Olá Etcher SD cartão](https://etcher.io/).
   1. Execute Etcher e selecione a imagem de Raspbian Olá que extraiu no passo 1.
   1. Selecione a unidade de cartão microSD de Olá. Tenha em atenção que Etcher poderá já selecionou correta da unidade Olá.
   1. Clique em Flash tooinstall Raspbian toohello microSD cartão.
   1. Remova o cartão microSD de Olá do seu computador quando a instalação estiver concluída. É diretamente cartão de microSD Olá tooremove seguro porque Etcher automaticamente ejects ou unmounts cartão microSD de Olá após a conclusão.
   1. Inserir cartão microSD de Olá Pi.

### <a name="enable-ssh-and-i2c"></a>Ativar o SSH e I2C

1. Ligar o monitor de toohello Pi, teclado e rato, inicie o instalador de plataforma e, em seguida, inicie sessão no Raspbian utilizando `pi` como nome de utilizador Olá e `raspberry` como palavra-passe de Olá.
1. Clique em Olá Raspberry ícone > **preferências** > **Raspberry Pi configuração**.

   ![menu de preferências Raspbian Olá](media/iot-hub-raspberry-pi-kit-node-get-started/1_raspbian-preferences-menu.png)

1. No Olá **Interfaces** separador, defina **I2C** e **SSH** demasiado**ativar**e, em seguida, clique em **OK**. Se não tiver sensores físicos e pretende que os dados de sensores de toouse simulated, este passo é opcional.

   ![Ativar I2C e SSH no Raspberry Pi](media/iot-hub-raspberry-pi-kit-node-get-started/2_enable-i2c-ssh-on-raspberry-pi.png)

> [!NOTE] 
tooenable SSH e I2C, pode encontrar mais de referência de documentos no [raspberrypi.org](https://www.raspberrypi.org/documentation/remote-access/ssh/) e [Adafruit.com](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-4-gpio-setup/configuring-i2c).

### <a name="connect-hello-sensor-toopi"></a>Ligar Olá sensor tooPi

Utilize Olá de breadboard e jumper de tooconnect de cablagem um LED e um tooPi BME280 da seguinte forma. Se não tiver sensor Olá, [ignorar esta secção](#connect-pi-to-the-network).

![Olá ligação Raspberry Pi e sensor](media/iot-hub-raspberry-pi-kit-node-get-started/3_raspberry-pi-sensor-connection.png)

sensor de Olá BME280 pode recolher dados relativos à temperatura e humidade. E Olá LED será blink se houver uma comunicação entre o dispositivo e Olá nuvem. 

Para sensor pins, utilize Olá wiring os seguintes:

| Iniciar (Sensor & LED)     | Fim (quadro)            | Cor de cabo   |
| -----------------------  | ---------------------- | ------------: |
| VDD (Pin 5g)             | 3.3V PWR (Pin 1)       | Cabo branco   |
| GND (Pin 7G)             | GND (Pin 6)            | Cabo castanha   |
| SDI (Pin 10g)            | I2C1 SDA (Pin 3)       | Cabo vermelho     |
| SCK (Pin 8G)             | I2C1 SCL (Pin 5)       | Cabo laranja  |
| LED VDD (Pin 18F)        | GPIO 24 (Pin 18)       | Cabo branco   |
| LED GND (Pin 17F)        | GND (Pin 20)           | Cabo preto   |

Clique em tooview [Raspberry Pi 2 e 3 mapeamentos de Pin](https://developer.microsoft.com/windows/iot/docs/pinmappingsrpi) para referência.

Depois de se ligar com êxito BME280 tooyour Raspberry Pi, deve ser como abaixo imagem.

![Instalador de plataforma ligado e BME280](media/iot-hub-raspberry-pi-kit-node-get-started/4_connected-pi.jpg)

### <a name="connect-pi-toohello-network"></a>Ligar a rede de toohello Pi

Ative a Pi utilizando o cabo USB micro Olá e fonte de alimentação Olá. Utilize Olá Ethernet cabo tooconnect Pi tooyour com fios de rede ou seguir Olá [instruções de Olá Raspberry Pi Foundation](https://www.raspberrypi.org/learning/software-guide/wifi/) rede sem fios do tooconnect Pi tooyour. Após a sua Pi foi rede toohello ligado com êxito, é necessário tootake nota Olá [endereço IP do seu Pi](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-3-network-setup/finding-your-pis-ip-address).

![Rede toowired ligado](media/iot-hub-raspberry-pi-kit-node-get-started/5_power-on-pi.jpg)

> [!NOTE]
> Certifique-se que Pi toohello ligado, mesmo que o computador de rede. Por exemplo, se o computador está ligado tooa rede sem fios enquanto Pi está ligado tooa rede com fios, poderá não o ver Olá IP endereço na saída de devdisco Olá.

## <a name="run-a-sample-application-on-pi"></a>Executar uma aplicação de exemplo no instalador de plataforma

### <a name="clone-sample-application-and-install-hello-prerequisite-packages"></a>Clonar o exemplo de aplicação e instalar pacotes de pré-requisitos Olá

1. Utilize um dos Olá os seguintes clientes SSH do seu tooyour de tooconnect do computador anfitrião Raspberry Pi.
   
   **Utilizadores do Windows**
   1. Transfira e instale [PuTTY](http://www.putty.org/) para Windows. 
   1. Copie o endereço IP Olá a secção de instalador de plataforma para Olá anfitrião nome (ou endereço IP) e selecione SSH como tipo de ligação de Olá.
   
   ![PuTTy](media/iot-hub-raspberry-pi-kit-node-get-started/7_putty-windows.png)
   
   **Mac e Ubuntu utilizadores**
   
   Utilize Olá SSH no cliente incorporado Ubuntu ou macOS. Poderá ser necessário toorun `ssh pi@<ip address of pi>` tooconnect Pi através de SSH.
   > [!NOTE] 
   o nome de utilizador do Olá predefinido é `pi` , e a palavra-passe de Olá é `raspberry`.

1. Instale Node.js e NPM tooyour Pi.
   
   Primeiro deverá verificar a sua versão de Node.js com Olá os seguintes comandos. 
   
   ```bash
   node -v
   ```

   Se a versão de Olá é inferior à 4. x ou não há nenhum Node.js na sua Pi, em seguida, executar Olá tooinstall de comando a seguir ou atualizar Node.js.

   ```bash
   curl -sL http://deb.nodesource.com/setup_4.x | sudo -E bash
   sudo apt-get -y install nodejs
   ```

1. Clone a aplicação de exemplo Olá executando Olá os seguintes comandos:

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-node-raspberrypi-client-app
   ```

1. Instale todos os pacotes hello os seguintes comandos. Inclui dispositivos IoT do Azure SDK, BME280 Sensor biblioteca e da biblioteca de preparar o Pi.

   ```bash
   cd iot-hub-node-raspberrypi-client-app
   sudo npm install
   ```
   > [!NOTE] 
   Poderá demorar vários minutos toofinish este processo de instalação, dependendo da sua ligação de rede.

### <a name="configure-hello-sample-application"></a>Configurar a aplicação de exemplo de Olá

1. Abra o ficheiro de configuração de Olá executando Olá os seguintes comandos:

   ```bash
   nano config.json
   ```

   ![Ficheiro de configuração](media/iot-hub-raspberry-pi-kit-node-get-started/6_config-file.png)

   Existem dois itens neste ficheiro, pode configurate. Olá primeiro um é `interval`, que define o intervalo de tempo de Olá (em milissegundos) entre duas mensagens que enviam toocloud. Olá segunda `simulatedData`, que é um valor booleano para se toouse simulated dados de sensores ou não.

   Se lhe **não tiver sensor Olá**, hello Defina `simulatedData` valor demasiado`true` aplicação de exemplo de Olá toomake criar e utilizar dados de sensores simulados.

1. Guarde e saia, premindo O controlo > introduza > X de controlo.

### <a name="run-hello-sample-application"></a>Executar a aplicação de exemplo de Olá

Execute a aplicação de exemplo de Olá executando Olá os seguintes comandos:

   ```bash
   sudo node index.js '<YOUR AZURE IOT HUB DEVICE CONNECTION STRING>'
   ```

   > [!NOTE] 
   Certifique-se de que copiar-colar a cadeia de ligação de dispositivo de Olá para plicas Olá.


Deverá ver a seguinte Olá de saída que mostra Olá sensor dados e Olá mensagens enviadas tooyour IoT hub.

![Saída - dados de sensor enviados a partir do IoT hub tooyour Raspberry Pi](media/iot-hub-raspberry-pi-kit-node-get-started/8_run-output.png)

## <a name="next-steps"></a>Passos seguintes

Executar um dados de sensores de toocollect de aplicação de exemplo e enviá-lo tooyour IoT hub. mensagens hello do toosee que sua Raspberry Pi enviou tooyour IoT hub ou enviar mensagens tooyour Raspberry Pi numa interface de linha de comandos, consulte Olá [gerir dispositivos de cloud messaging com tutorial de iothub Explorador](https://docs.microsoft.com/en-gb/azure/iot-hub/iot-hub-explorer-cloud-device-messaging).

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
