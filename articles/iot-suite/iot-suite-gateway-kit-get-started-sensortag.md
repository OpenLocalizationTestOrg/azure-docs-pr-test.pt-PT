---
title: aaaConnect tooAzure um gateway com um NUC Intel do IoT Suite | Microsoft Docs
description: "Utilize Olá Kit de Gateway do Microsoft IoT comerciais e Olá remota solução pré-configurada de monitorização. Utilizar tooenable de gateway do Azure IoT Edge Olá um SensorTag dispositivo tooconnect toohello solução de monitorização remota, nuvem toohello de telemetria de enviar e responder toomethods invocado a partir do dashboard de solução Olá."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.service: iot-suite
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/24/2017
ms.author: dobett
ms.openlocfilehash: 6f98ee3c1e2311a8644da9d72d40e671e7cbcf00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-azure-iot-edge-gateway-toohello-remote-monitoring-preconfigured-solution-and-send-telemetry-from-a-sensortag"></a>Ligar o seu toohello de gateway do Azure IoT Edge solução pré-configurada de monitorização remota e enviar telemetria a partir de um SensorTag

[!INCLUDE [iot-suite-gateway-kit-selector](../../includes/iot-suite-gateway-kit-selector.md)]

Este tutorial mostra como toouse Azure IoT Edge toosend relativos à temperatura e humidade dados de SensorTag dispositivo toohello monitorização remota solução pré-configurada. Olá SensorTag estabelece a ligação de gateway do Intel NUC toohello utilizando o Bluetooth. tutorial de Olá utiliza:

- Um gateway de exemplo de tooimplement IoT Edge do Azure.
- Olá IoT Suite remoto solução pré-configurada de monitorização como Olá baseado na nuvem de back-end.

## <a name="overview"></a>Descrição geral

Neste tutorial, conclua Olá os seguintes passos:

- Implemente uma instância do tooyour de solução pré-configurada Olá remoto monitorização subscrição do Azure. Este passo automaticamente implementa e configura vários serviços do Azure.
- Configure a sua toocommunicate de dispositivo de gateway Intel NUC com o seu computador e a solução de monitorização remota Olá.
- Configurar a sua telemetria do Intel NUC gateway tooreceive de um dispositivo SensorTag e enviá-lo toohello dashboard de monitorização remota.

[!INCLUDE [iot-suite-gateway-kit-prerequisites](../../includes/iot-suite-gateway-kit-prerequisites.md)]

[Texas Instruments var SensorTag][lnk-sensortag]. Este tutorial obtém dados de telemetria sobre o Bluetooth do dispositivo de SensorTag Olá.

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

> [!WARNING]
> Olá Aprovisiona de solução de monitorização remota de um conjunto de serviços do Azure na sua subscrição do Azure. implementação de Olá reflete uma arquitetura de empresas reais. encargos de consumo do Azure desnecessários tooavoid, elimine a instância da solução de Olá pré-configurada em azureiotsuite.com quando tiver terminado com o mesmo. Se precisar de hello novamente solução pré-configurada, pode recriá-lo facilmente. Para obter mais informações sobre a redução do consumo ao hello execuções de solução de monitorização remota, consulte [soluções para fins de demonstração de pré-configuradas de configurar o Azure IoT Suite][lnk-demo-config].

[!INCLUDE [iot-suite-gateway-kit-view-solution](../../includes/iot-suite-gateway-kit-view-solution.md)]

[!INCLUDE [iot-suite-gateway-kit-prepare-nuc-connectivity](../../includes/iot-suite-gateway-kit-prepare-nuc-connectivity.md)]

## <a name="configure-bluetooth-connectivity"></a>Configurar a conectividade do Bluetooth

Configurar o Bluetooth Olá Intel NUC tooenable Olá SensorTag dispositivo tooconnect e enviar telemetria.

### <a name="find-hello-mac-address-of-hello-sensortag"></a>Localizar o endereço MAC Olá Olá SensorTag

1. Na shell de Olá no Olá Intel NUC, execute Olá serviço Bluetooth do comando toounblock Olá os seguintes:

    ```bash
    sudo rfkill unblock bluetooth
    ```

1. Olá executar comandos seguintes toostart Olá Bluetooth serviço Olá Intel NUC e introduza a shell de Bluetooth Olá:

    ```bash
    sudo systemctl start bluetooth
    bluetoothctl
    ```

1. Execute Olá toopower comando num controlador de Bluetooth Olá os seguintes:

    ```bash
    power on
    ```

    Quando o controlador de Olá está ativado, verá uma mensagem **a alteração de energia no foi concluída com êxito**.

1. Execute Olá tooscan de comando para próximas dispositivos Bluetooth os seguintes:

    ```bash
    scan on
    ```

1. Prima Olá energia botão no Olá SensorTag toomake-Detetáveis. Olá verde LED está intermitente.

1. Quando vir uma mensagem na shell de Olá desse controlador Olá detetou Olá SensorTag, anote Olá endereço MAC do dispositivo Olá. Olá endereço MAC é semelhante **A0:E6:F8:B5:F6:00**. Tem de endereço de MAC hello mais tarde no tutorial Olá quando configurar o gateway de Olá.

1. Execute Olá tooturn comando desativar a análise de Bluetooth os seguintes:

    ```bash
    scan off
    ```

1. Execute Olá tooverify de comando que pode ligar dispositivos SensorTag de toohello os seguintes:

    ```bash
    connect <SensorTag MAC address>
    ```

    Se ligar com êxito, shell Olá mostra mensagem de saudação **ligação com êxito** e imprime informações sobre Olá SensorTag do dispositivo. Se não conseguir ligar, verifique Olá que sensortag ainda está ligado.

1. Pode agora desligar do Olá SensorTag e sair da shell de Bluetooth Olá executando Olá os seguintes comandos:

    ```bash
    disconnect
    exit
    ```

[!INCLUDE [iot-suite-gateway-kit-prepare-nuc-software](../../includes/iot-suite-gateway-kit-prepare-nuc-software.md)]

## <a name="build-hello-custom-iot-edge-module"></a>Construir Olá módulo de limite de IoT personalizado

Agora pode compilar módulo IoT Edge personalizado Olá que permite Olá gateway toosend mensagens toohello solução de monitorização remota. Para obter mais informações sobre como configurar um gateway e os módulos de limite de IoT, consulte [conceitos do Azure IoT Edge][lnk-gateway-concepts].

Transferir o código de origem Olá para módulos de limite de IoT personalizados Olá a partir do GitHub com Olá os seguintes comandos:

```bash
cd ~
git clone https://github.com/Azure-Samples/iot-remote-monitoring-c-intel-nuc-gateway-getting-started.git
```

Crie módulo Olá personalizado IoT Edge utilizando Olá os seguintes comandos:

```bash
cd ~/iot-remote-monitoring-c-intel-nuc-gateway-getting-started/basic
chmod u+x build.sh
sed -i -e 's/\r$//' build.sh
./build.sh
```

script de compilação de Olá coloca o módulo de limite de IoT personalizado libsensor2remotemonitoring.so Olá na pasta de compilação de Olá.

## <a name="configure-and-run-hello-iot-edge-gateway"></a>Configurar e executar Olá gateway de IoT

Agora pode configurar Olá telemetria de toosend do gateway de IoT limite da sua tooyour de dispositivos SensorTag dashboard de monitorização remota. Para obter mais informações sobre como configurar um gateway e os módulos de limite de IoT, consulte [conceitos do Azure IoT Edge][lnk-gateway-concepts].

> [!TIP]
> Neste tutorial, utiliza o padrão de Olá `vi` editor de texto no Olá Intel NUC. Se não tiver utilizado `vi` anteriormente, deve efetuar um tutorial introdutórias, tais como [Unix - Olá vi Editor Tutorial] [ lnk-vi-tutorial] toofamiliarize por si deste editor. Em alternativa, pode instalar mais intuitivo Olá [nano](https://www.nano-editor.org/) editor utilizando o comando de Olá `smart install nano -y`.

Ficheiro de configuração de exemplo de Olá aberto em Olá **vi** editor utilizando Olá os seguintes comandos:

```bash
vi ~/iot-remote-monitoring-c-intel-nuc-gateway-getting-started/basic/remote_monitoring.json
```

Localize Olá seguintes linhas na configuração de Olá para o módulo de IoTHub Olá:

```json
"args": {
  "IoTHubName": "<<Azure IoT Hub Name>>",
  "IoTHubSuffix": "<<Azure IoT Hub Suffix>>",
  "Transport": "http"
}
```

Substitua o marcador de posição de Olá valores com Olá informações do IoT Hub é criado e guardado no Olá iniciar deste tutorial. valor de Olá para IoTHubName aspeto **yourrmsolution37e08**, e o valor de Olá para IoTSuffix é normalmente **azure devices.net**.

Localize Olá seguintes linhas na configuração de Olá para o módulo de mapeamento de Olá:

```json
args": [
  {
    "macAddress": "<<AA:BB:CC:DD:EE:FF>>",
    "deviceId": "<<Azure IoT Hub Device ID>>",
    "deviceKey": "<<Azure IoT Hub Device Key>>"
  }
]
```

Substitua Olá **macAddress** marcador Olá endereço MAC do seu SensorTag que apontou anteriormente. Substitua Olá **deviceID** e **deviceKey** marcadores de posição com os IDs de Olá e chaves para dispositivos Olá dois na solução de monitorização remota Olá que criou anteriormente.

Localize Olá seguintes linhas na configuração de Olá para o módulo de SensorTag Olá:

```json
"args": {
  "controller_index": 0,
  "device_mac_address": "<<AA:BB:CC:DD:EE:FF>>",
  ...
}
```

Substitua Olá **dispositivo\_mac\_endereço** marcador Olá endereço MAC do seu SensorTag que apontou anteriormente.

Guarde as alterações.

Pode agora executar gateway Olá utilizando Olá os seguintes comandos:

```bash
cd ~/iot-remote-monitoring-c-intel-nuc-gateway-getting-started/basic
/usr/share/azureiotgatewaysdk/samples/ble_gateway/ble_gateway remote_monitoring.json
```

Olá gateway de IoT é iniciado num Olá Intel NUC e envia a telemetria da Olá solução de monitorização remota SensorTag toohello:

![Gateway de IoT envia a telemetria da Olá SensorTag][img-telemetry]

Prima **Ctrl-C** programa de Olá tooexit em qualquer altura.

## <a name="view-hello-telemetry"></a>Telemetria de visualizações de Olá

gateway de Olá agora está a enviar telemetria de Olá SensorTag dispositivo toohello solução de monitorização remota. Pode ver a telemetria de Olá no dashboard da solução Olá. Também pode enviar o dispositivo de SensorTag tooyour comandos através do gateway de Olá a partir do dashboard de solução Olá.

- Navegue toohello dashboard da solução.
- Dispositivo Olá selecione configurada no gateway de Olá que representa Olá SensorTag no Olá **dispositivo tooView** pendente.
- Apresenta a telemetria de Olá de dispositivos SensorTag de Olá no dashboard de Olá.

![Apresentar a telemetria de dispositivos SensorTag de Olá][img-telemetry-display]

> [!WARNING]
> Se deixar Olá em execução na sua conta do Azure de solução de monitorização remota, é-lhe faturado por período de tempo de Olá que é executada. Para obter mais informações sobre a redução do consumo ao hello execuções de solução de monitorização remota, consulte [soluções para fins de demonstração de pré-configuradas de configurar o Azure IoT Suite][lnk-demo-config]. Elimine a solução pré-configurada de Olá da sua conta do Azure quando tiver concluído a utilizá-la.


## <a name="next-steps"></a>Passos seguintes

Visite Olá [Dev Center do Azure IoT](https://azure.microsoft.com/develop/iot/) para obter mais exemplos e documentação no Azure IoT.

[img-telemetry]: ./media/iot-suite-gateway-kit-get-started-sensortag/appoutput.png


[img-telemetry-display]: ./media/iot-suite-gateway-kit-get-started-sensortag/telemetry.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md
[lnk-vi-tutorial]: http://www.tutorialspoint.com/unix/unix-vi-editor.htm
[lnk-sensortag]: http://www.ti.com/ww/en/wireless_connectivity/sensortag/
[lnk-gateway-concepts]: https://docs.microsoft.com/azure/iot-hub/iot-hub-linux-iot-edge-get-started