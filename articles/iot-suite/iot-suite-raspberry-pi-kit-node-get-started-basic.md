---
title: aaaConnect tooAzure um Raspberry Pi IoT Suite com o Node.js com sensores reais | Microsoft Docs
description: "Utilize Olá Starter Kit do Microsoft Azure IoT para Olá Raspberry Pi 3 e o Azure IoT Suite. Utilizar Node.js tooconnect sua toohello Raspberry Pi solução de monitorização remota, enviar telemetria a partir de sensores toohello cloud e responder toomethods invocado a partir do dashboard de solução Olá."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.service: iot-suite
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: dobett
ms.openlocfilehash: 7ffb4a7a8c04b424a1f29170f4739d89f39a2429
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-raspberry-pi-3-toohello-remote-monitoring-solution-and-send-telemetry-from-a-real-sensor-using-nodejs"></a>Ligar a sua solução de monitorização remota de toohello Raspberry Pi 3 e enviar telemetria a partir de um sensor real com o Node.js

[!INCLUDE [iot-suite-raspberry-pi-kit-selector](../../includes/iot-suite-raspberry-pi-kit-selector.md)]

Este tutorial mostra como toouse hello Starter Kit do Microsoft Azure IoT para Raspberry Pi 3 toodevelop um leitor de temperatura e humidade que pode comunicar com a nuvem de Olá. tutorial de Olá utiliza:

- SO de Raspbian, Olá Node.js linguagem de programação e hello SDK do Microsoft Azure IoT para Node.js tooimplement um dispositivo de exemplo.
- Olá IoT Suite remoto solução pré-configurada de monitorização como Olá baseado na nuvem de back-end.

## <a name="overview"></a>Descrição geral

Neste tutorial, conclua Olá os seguintes passos:

- Implemente uma instância do tooyour de solução pré-configurada Olá remoto monitorização subscrição do Azure. Este passo automaticamente implementa e configura vários serviços do Azure.
- Configure o seu dispositivo e sensores toocommunicate com o seu computador e Olá solução de monitorização remota.
- Atualize Olá exemplo dispositivo código tooconnect toohello solução de monitorização remota e enviar telemetria que pode ver no dashboard da solução Olá.

[!INCLUDE [iot-suite-raspberry-pi-kit-prerequisites](../../includes/iot-suite-raspberry-pi-kit-prerequisites.md)]

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

> [!WARNING]
> Olá Aprovisiona de solução de monitorização remota de um conjunto de serviços do Azure na sua subscrição do Azure. implementação de Olá reflete uma arquitetura de empresas reais. encargos de consumo do Azure desnecessários tooavoid, elimine a instância da solução de Olá pré-configurada em azureiotsuite.com quando tiver terminado com o mesmo. Se precisar de hello novamente solução pré-configurada, pode recriá-lo facilmente. Para obter mais informações sobre a redução do consumo ao hello execuções de solução de monitorização remota, consulte [soluções para fins de demonstração de pré-configuradas de configurar o Azure IoT Suite][lnk-demo-config].

[!INCLUDE [iot-suite-raspberry-pi-kit-view-solution](../../includes/iot-suite-raspberry-pi-kit-view-solution.md)]

[!INCLUDE [iot-suite-raspberry-pi-kit-prepare-pi](../../includes/iot-suite-raspberry-pi-kit-prepare-pi.md)]

## <a name="download-and-configure-hello-sample"></a>Transferir e configurar o exemplo de Olá

Agora pode transferir e configurar a aplicação de cliente de monitorização remota de Olá no seu Raspberry Pi.

### <a name="install-nodejs"></a>Instalar o Node.js

Instale o Node.js no seu Raspberry Pi. Olá IoT SDK para Node.js requer a versão 0.11.5 do Node.js ou posterior. Olá passos seguintes mostram como tooinstall Node.js v6.10.2 no seu Raspberry Pi:

1. Utilize Olá tooupdate de comando a seguir a Raspberry Pi:

    ```sh
    sudo apt-get update
    ```

1. Utilize os seguintes comandos toodownload Olá Node.js binários tooyour Raspberry Pi de Olá:

    ```sh
    wget https://nodejs.org/dist/v6.10.2/node-v6.10.2-linux-armv7l.tar.gz
    ```

1. Utilize Olá binários de Olá tooinstall de comando a seguir:

    ```sh
    sudo tar -C /usr/local --strip-components 1 -xzf node-v6.10.2-linux-armv7l.tar.gz
    ```

1. Utilize Olá tooverify de comando que instalou o Node.js v6.10.2 com êxito os seguintes:

    ```sh
    node --version
    ```

### <a name="clone-hello-repositories"></a>Repositórios de Olá clone

Se ainda não o fez, Olá clone necessário Olá de repositórios executando os seguintes comandos no seu Pi:

```sh
cd ~
git clone --recursive https://github.com/Azure-Samples/iot-remote-monitoring-node-raspberrypi-getstartedkit.git`
```

### <a name="update-hello-device-connection-string"></a>Atualizar a cadeia de ligação do dispositivo Olá

Ficheiro de origem de exemplo de Olá aberta no Olá **nano** editor utilizando Olá os seguintes comandos:

```sh
nano ~/iot-remote-monitoring-node-raspberrypi-getstartedkit/basic/remote_monitoring.js
```

Localize a linha de Olá:

```javascript
var connectionString = 'HostName=[Your IoT hub name].azure-devices.net;DeviceId=[Your device id];SharedAccessKey=[Your device key]';
```

Substitua os valores de marcador de posição de Olá dispositivo Olá e informações de IoT Hub é criado e guardado no início de Olá deste tutorial. Guardar as alterações (**Ctrl-O**, **Enter**) e saída Olá editor (**Ctrl-X**).

## <a name="run-hello-sample"></a>Executar o exemplo de Olá

Seguinte Olá executar comandos tooinstall Olá pré-requisitos pacotes de exemplo de Olá:

```sh
cd ~/iot-remote-monitoring-node-raspberrypi-getstartedkit/basic
npm install
```

Pode agora executar o programa de exemplo de Olá no Olá Raspberry Pi. Introduza o comando de Olá:

```sh
sudo node ~/iot-remote-monitoring-node-raspberrypi-getstartedkit/basic/remote_monitoring.js
```

Olá saída de exemplo seguinte é um exemplo de saída de Olá que consulte na linha de comandos de Olá no Olá Raspberry Pi:

![Resultado da aplicação Raspberry Pi][img-raspberry-output]

Prima **Ctrl-C** programa de Olá tooexit em qualquer altura.

[!INCLUDE [iot-suite-raspberry-pi-kit-view-telemetry](../../includes/iot-suite-raspberry-pi-kit-view-telemetry.md)]

## <a name="next-steps"></a>Passos seguintes

Visite Olá [Dev Center do Azure IoT](https://azure.microsoft.com/develop/iot/) para obter mais exemplos e documentação no Azure IoT.

[img-raspberry-output]: ./media/iot-suite-raspberry-pi-kit-node-get-started-basic/app-output.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md
