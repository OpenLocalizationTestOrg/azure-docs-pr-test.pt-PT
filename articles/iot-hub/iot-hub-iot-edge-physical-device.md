---
title: "aaaUse um dispositivo físico com o Azure IoT Edge | Microsoft Docs"
description: "Como toouse um Texas Instruments SensorTag dispositivo toosend dados tooan IoT hub através de um gateway de IoT Edge em execução num dispositivo Raspberry Pi 3. gateway de Olá é criada com o Azure IoT Edge."
services: iot-hub
documentationcenter: 
author: chipalost
manager: timlt
editor: 
ms.assetid: 212dacbf-e5e9-48b2-9c8a-1c14d9e7b913
ms.service: iot-hub
ms.devlang: cpp
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/12/2017
ms.author: andbuc
ms.openlocfilehash: a2385accdbd99012ad094232653ee47d4e5c7839
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-iot-edge-on-a-raspberry-pi-tooforward-device-to-cloud-messages-tooiot-hub"></a>Utilizar o Azure IoT Edge no tooIoT de mensagens do dispositivo para nuvem tooforward Raspberry Pi Hub

Estas instruções de Olá [exemplo de baixa energia Bluetooth] [ lnk-ble-samplecode] mostra-lhe como toouse [Azure IoT Edge] [ lnk-sdk] para:

* Reencaminhe tooIoT de telemetria do dispositivo para nuvem Hub a partir de um dispositivo físico.
* Comandos de rota do dispositivo físico do IoT Hub tooa.

Estas instruções abrangem:

* **Arquitetura**: as informações da arquitetura importantes sobre Olá Bluetooth baixa energia de amostra.
* **Compilar e executar**: Olá passos necessários toobuild e exemplo de Olá execução.

## <a name="architecture"></a>Arquitetura

instruções de Olá mostram como toobuild e executar um gateway de IoT em 3 de Pi um Raspberry que é executado Raspbian Linux. gateway de Olá é criada com o limite de IoT. exemplo de Olá utiliza um Texas Instruments SensorTag Bluetooth baixa energia (var) dispositivo toocollect temperatura de dados.

Quando executa Olá gateway de IoT-lo:

* Estabelece ligação tooa SensorTag dispositivo através do protocolo de Bluetooth baixa energia (var) Olá.
* Estabelece ligação tooIoT Hub através do protocolo de Olá HTTP.
* Reencaminha a telemetria de Olá SensorTag dispositivo tooIoT Hub.
* Comandos de dispositivos do IoT Hub toohello SensorTag de rotas.

gateway de Olá contém Olá seguintes módulos de limite de IoT:

* A *módulo var* que interaja com um var dispositivo tooreceive temperatura de dados do dispositivo de Olá e enviar comandos toohello dispositivo.
* A *módulo do var nuvem toodevice* que traduz mensagens JSON enviadas a partir do IoT Hub para var as instruções para Olá *módulo var*.
* A *módulo de registo* que regista todos os gateway mensagens tooa ficheiro local.
* Um *módulo de mapeamento de identidades* que traduz entre endereços de MAC do dispositivo var e identidades de dispositivo do IoT Hub do Azure.
* Um *módulo do IoT Hub* que carrega o hub IoT do telemetria dados tooan e recebe comandos de dispositivo a partir de um hub IoT.
* A *módulo de impressora var* que interpreta telemetria do dispositivo de var Olá e imprime dados formatados toohello consola tooenable resolução de problemas e depuração.

### <a name="how-data-flows-through-hello-gateway"></a>Como os dados de saída flui através do gateway Olá

Olá diagrama de blocos a seguir ilustra o pipeline de fluxo de dados de carregamento telemetria Olá:

![Pipeline de gateway de carregamento de telemetria](media/iot-hub-iot-edge-physical-device/gateway_ble_upload_data_flow.png)

passos de Olá que um item de telemetria demora estiverem em deslocação de uma tooIoT de dispositivo var Hub são:

1. gera uma amostra de temperatura e envia-o ao longo do módulo de var toohello Bluetooth no gateway de Olá de Olá var dispositivos.
1. módulo de var Olá recebe exemplo Olá e publica-broker toohello juntamente com o endereço de MAC Olá do dispositivo Olá.
1. módulo de mapeamento de identidades Olá escolherá esta mensagem e utiliza um Olá tootranslate de tabela interna endereço MAC do dispositivo Olá para uma identidade de dispositivo IoT Hub. Uma identidade de dispositivo do IoT Hub é composta por um ID de dispositivo e a chave do dispositivo.
1. módulo de mapeamento de identidades Olá publica uma nova mensagem que contém dados de exemplo de temperatura Olá, endereço de MAC Olá de dispositivo Olá, ID de dispositivo Olá e chave do dispositivo Olá.
1. Olá módulo do IoT Hub recebe esta mensagem nova (gerada pelo módulo de mapeamento de identidades de Olá) e publica-tooIoT Hub.
1. módulo de registo Olá regista todas as mensagens de ficheiro do Olá mediador tooa local.

Olá diagrama de blocos a seguir ilustra o pipeline de fluxo de dados de comando dispositivo Olá:

![Pipeline de gateway do comando de dispositivo](media/iot-hub-iot-edge-physical-device/gateway_ble_command_data_flow.png)

1. Olá IoT Hub módulo consulta periodicamente se existem Olá IoT hub para novas mensagens de comando.
1. Quando Olá módulo do IoT Hub recebe uma nova mensagem de comando, publica-toohello mediador.
1. módulo de mapeamento de identidades Olá escolherá a mensagem de comando de saudação e utiliza um Olá tootranslate de tabela interna dispositivos do IoT Hub dispositivo ID tooa endereço MAC. Em seguida, publica uma nova mensagem, que inclui o endereço de MAC Olá do dispositivo-alvo Olá no mapa de propriedades de Olá de mensagem de saudação.
1. módulo de var nuvem para o dispositivo de Olá escolherá esta mensagem e converte-lo em instruções var adequada Olá para o módulo de var Olá. Em seguida, publica uma nova mensagem.
1. módulo de var Olá escolherá esta mensagem e executa a instrução de e/s de Olá através da comunique com Olá var.
1. módulo de registo Olá regista todas as mensagens do ficheiro de disco Olá mediador tooa.

## <a name="prerequisites"></a>Pré-requisitos

toocomplete neste tutorial, necessita de uma subscrição do Azure Active Directory.

> [!NOTE]
> Se não tiver uma conta, pode criar uma de avaliação gratuita em apenas alguns minutos. Para obter mais detalhes, consulte [Azure Free Trial (Avaliação Gratuita do Azure)][lnk-free-trial].

Precisa de cliente SSH no seu tooenable de ambiente de trabalho de máquina tooremotely acesso Olá comando linha no Olá Raspberry Pi.

- Windows não inclui um cliente SSH. Recomendamos que utilize [PuTTY](http://www.putty.org/).
- A maioria das distribuições de Linux e Mac OS incluem SSH utilitário de linha de comandos Olá. Para obter mais informações, consulte [SSH utilizando o Linux ou Mac OS](https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md).

## <a name="prepare-your-hardware"></a>Prepare o hardware

Este tutorial parte do princípio de que está a utilizar um [Texas Instruments SensorTag](http://www.ti.com/ww/en/wireless_connectivity/sensortag2015/index.html) dispositivo ligado tooa Raspberry Pi 3 Raspbian a executar.

### <a name="install-raspbian"></a>Instalar Raspbian

Pode utilizar qualquer uma das seguintes opções tooinstall Raspbian no seu dispositivo Raspberry Pi 3 de Olá.

* versão mais recente de Olá tooinstall de Raspbian, utilize Olá [NOOBS] [ lnk-noobs] interface gráfica do utilizador.
* Manualmente [transferir] [ lnk-raspbian] e escrever Olá imagem mais recente do cartão de Olá Raspbian sistema operativo tooan SD.

### <a name="sign-in-and-access-hello-terminal"></a>A iniciar sessão e aceder ao terminal Olá

Tem duas opções tooaccess num ambiente de terminal no seu Raspberry Pi:

* Se tiver um teclado e monitorizar tooyour ligado Raspberry Pi, pode utilizar Olá Raspbian GUI tooaccess uma janela de terminal.

* Linha de comandos de Olá de acesso na sua Raspberry Pi utilizando SSH a partir do seu computador de secretária.

#### <a name="use-a-terminal-window-in-hello-gui"></a>Utilizar uma janela de terminal no Olá GUI

credenciais predefinidas Olá Raspbian são username **pi** e palavra-passe **raspberry**. Na barra de tarefas de Olá no Olá GUI, pode iniciar Olá **Terminal** utilitário com ícone de Olá que se assemelha um monitor.

#### <a name="sign-in-with-ssh"></a>Inicie sessão com SSH

Pode utilizar o SSH para acesso da linha de comandos tooyour Raspberry Pi. artigo de Olá [SSH (Secure Shell)] [ lnk-pi-ssh] descreve como tooconfigure SSH no seu Raspberry Pi e como tooconnect de [Windows] [ lnk-ssh-windows] ou [SO Linux & Mac][lnk-ssh-linux].

Inicie sessão com o nome de utilizador **pi** e palavra-passe **raspberry**.

### <a name="install-bluez-537"></a>Instalar BlueZ 5.37

módulos de var Olá falar toohello Bluetooth hardware através de pilha de BlueZ Olá. Precisa de versão 5.37 de BlueZ para Olá módulos toowork corretamente. Estas instruções Certifique-se de que está instalada a versão correta do Olá do BlueZ.

1. Pare o daemon de bluetooth Olá atual:

    ```sh
    sudo systemctl stop bluetooth
    ```

1. Instale as dependências de BlueZ Olá:

    ```sh
    sudo apt-get update
    sudo apt-get install bluetooth bluez-tools build-essential autoconf glib2.0 libglib2.0-dev libdbus-1-dev libudev-dev libical-dev libreadline-dev
    ```

1. Transferir o código de origem do Olá BlueZ bluez.org:

    ```sh
    wget http://www.kernel.org/pub/linux/bluetooth/bluez-5.37.tar.xz
    ```

1. Deszipe o código de origem Olá:

    ```sh
    tar -xvf bluez-5.37.tar.xz
    ```

1. Alterar pasta do toohello recém-criado diretórios:

    ```sh
    cd bluez-5.37
    ```

1. Configure Olá BlueZ código toobe incorporada:

    ```sh
    ./configure --disable-udev --disable-systemd --enable-experimental
    ```

1. Crie BlueZ:

    ```sh
    make
    ```

1. Instalar BlueZ depois de estar concluído criação:

    ```sh
    sudo make install
    ```

1. Alterar a configuração do serviço systemd para bluetooth para pontos de nova bluetooth daemon toohello no ficheiro de Olá `/lib/systemd/system/bluetooth.service`. Substitua a linha de 'ExecStart' Olá com Olá seguinte texto:

    ```conf
    ExecStart=/usr/local/libexec/bluetooth/bluetoothd -E
    ```

### <a name="enable-connectivity-toohello-sensortag-device-from-your-raspberry-pi-3-device"></a>Ativar dispositivos SensorTag de toohello de conectividade do seu dispositivo Raspberry Pi 3

Antes de exemplo de Olá em execução, terá de tooverify que sua 3 de Pi Raspberry podem ligar toohello SensorTag dispositivo.

1. Certifique-se Olá `rfkill` utilitário está instalado:

    ```sh
    sudo apt-get install rfkill
    ```

1. Desbloquear bluetooth no Olá Raspberry Pi 3 e verificar se o número de versão Olá é **5.37**:

    ```sh
    sudo rfkill unblock bluetooth
    bluetoothctl --version
    ```

1. shell do tooenter Olá bluetooth interativa, iniciar o serviço de bluetooth Olá e executar Olá **bluetoothctl** comando:

    ```sh
    sudo systemctl start bluetooth
    bluetoothctl
    ```

1. Introduza o comando de Olá **ativação** toopower se o controlador de bluetooth Olá. comando de Olá devolve seguinte de toohello semelhante de saída:

    ```sh
    [NEW] Controller 98:4F:EE:04:1F:DF C3 raspberrypi [default]
    ```

1. Na shell de bluetooth interativa Olá, introduza o comando de Olá **verificar em** tooscan para dispositivos bluetooth. comando de Olá devolve seguinte de toohello semelhante de saída:

    ```sh
    Discovery started
    [CHG] Controller 98:4F:EE:04:1F:DF Discovering: yes
    ```

1. Certifique-dispositivos SensorTag de Olá detetável, premindo Olá pequeno botão (Olá deve flash LED verde). Olá Raspberry Pi 3 deve detetar dispositivos de SensorTag Olá:

    ```sh
    [NEW] Device A0:E6:F8:B5:F6:00 CC2650 SensorTag
    [CHG] Device A0:E6:F8:B5:F6:00 TxPower: 0
    [CHG] Device A0:E6:F8:B5:F6:00 RSSI: -43
    ```

    Neste exemplo, pode ver essa Olá endereço MAC de Olá SensorTag o dispositivo está **A0:E6:F8:B5:F6:00**.

1. Desativar a análise introduzindo Olá **analisar desativar** comando:

    ```sh
    [CHG] Controller 98:4F:EE:04:1F:DF Discovering: no
    Discovery stopped
    ```

1. Ligar tooyour SensorTag dispositivo utilizando o seu endereço MAC introduzindo **ligar \<endereço MAC\>**. é abreviada Olá saída de exemplo a seguir para efeitos de clareza:

    ```sh
    Attempting tooconnect tooA0:E6:F8:B5:F6:00
    [CHG] Device A0:E6:F8:B5:F6:00 Connected: yes
    Connection successful
    [CHG] Device A0:E6:F8:B5:F6:00 UUIDs: 00001800-0000-1000-8000-00805f9b34fb
    ...
    [NEW] Primary Service
            /org/bluez/hci0/dev_A0_E6_F8_B5_F6_00/service000c
            Device Information
    ...
    [CHG] Device A0:E6:F8:B5:F6:00 GattServices: /org/bluez/hci0/dev_A0_E6_F8_B5_F6_00/service000c
    ...
    [CHG] Device A0:E6:F8:B5:F6:00 Name: SensorTag 2.0
    [CHG] Device A0:E6:F8:B5:F6:00 Alias: SensorTag 2.0
    [CHG] Device A0:E6:F8:B5:F6:00 Modalias: bluetooth:v000Dp0000d0110
    ```

    > Pode listar as características de GATT Olá do dispositivo Olá novamente utilizando Olá **lista atributos** comando.

1. Pode agora desligar do dispositivo Olá utilizando Olá **desligar** comando e, em seguida, a sair da shell de bluetooth Olá utilizando Olá **sair** comando:

    ```sh
    Attempting toodisconnect from A0:E6:F8:B5:F6:00
    Successful disconnected
    [CHG] Device A0:E6:F8:B5:F6:00 Connected: no
    ```

Agora, está exemplo de limite de IoT var toorun pronto Olá no seu 3 de Pi Raspberry.

## <a name="run-hello-iot-edge-ble-sample"></a>Executar Olá IoT Edge var exemplo

exemplo de IoT Edge var do toorun Olá, terá de tarefas de três toocomplete:

* Configure dois dispositivos de exemplo no seu IoT Hub.
* Crie IoT Edge no seu dispositivo Raspberry Pi 3.
* Configure e execute o exemplo de var Olá no seu dispositivo Raspberry Pi 3.

Momento Olá de escrita, limite de IoT suporta apenas módulos var gateways em execução no Linux.

### <a name="configure-two-sample-devices-in-your-iot-hub"></a>Configurar dois dispositivos de exemplo no seu IoT Hub

* [Criar um hub IoT] [ lnk-create-hub] na sua subscrição do Azure, terá de nome de Olá do seu hub toocomplete estas instruções. Se não tiver uma conta, pode criar uma [conta gratuita][lnk-free-trial] em apenas alguns minutos.
* Adicionar um dispositivo designado **SensorTag_01** tooyour IoT hub e tome nota da respetiva chave id e o dispositivo. Pode utilizar Olá [Explorador de dispositivo ou no Explorador do iothub] [ lnk-explorer-tools] ferramentas tooadd este dispositivo toohello IoT hub que criou no passo anterior Olá e tooretrieve respetiva chave. Mapear este dispositivo do dispositivo toohello SensorTag quando configurar o gateway de Olá.

### <a name="build-azure-iot-edge-on-your-raspberry-pi-3"></a>Criar limite de IoT do Azure no seu Raspberry Pi 3

Instale dependências para o limite do Azure IoT:

```sh
sudo apt-get install cmake uuid-dev curl libcurl4-openssl-dev libssl-dev
```

Seguinte de Olá utilize comandos tooclone IoT Edge e todos os respetivo submodules tooyour diretório raiz:

```sh
cd ~
git clone https://github.com/Azure/iot-edge.git
```

Quando tiver uma cópia completa de Olá repositório de limite de IoT no seu 3 de Pi Raspberry, pode criá-la utilizando Olá os seguintes comandos a partir da pasta de Olá que contém Olá SDK:

```sh
cd ~/iot-edge
./tools/build.sh  --disable-native-remote-modules
```

### <a name="configure-and-run-hello-ble-sample-on-your-raspberry-pi-3"></a>Configurar e executar o exemplo de var Olá no seu 3 de Pi Raspberry

toobootstrap e exemplo de Olá execute, tem de configurar cada módulo de limite de IoT que participa no gateway de Olá. Esta configuração é fornecida um ficheiro JSON e tem de configurar todos os módulos de limite de IoT participantes cinco. Há um ficheiro JSON de exemplo no repositório de Olá chamado **gateway\_sample.json** que pode utilizar como Olá ponto para a criação do seu próprio ficheiro de configuração de partida. Este ficheiro está a ser Olá **ble_gateway/samples/src** pasta na cópia local do Olá repositório de limite de IoT.

Olá secções seguintes descrevem como tooedit esta configuração de ficheiros de exemplo de var Olá e partem do princípio de que Olá repositório de limite de IoT é no Olá **/home/pi/iot-edge /** pasta no seu 3 de Pi Raspberry. Se o repositório de Olá noutro local, ajuste caminhos Olá em conformidade.

#### <a name="logger-configuration"></a>Configuração de registo

Partindo do princípio de repositório do gateway de Olá está localizado na Olá **/home/pi/iot-edge /** pasta, configurar o módulo de registo Olá da seguinte forma:

```json
{
  "name": "Logger",
  "loader": {
    "name" : "native",
    "entrypoint" : {
      "module.path" : "build/modules/logger/liblogger.so"
    }
  },
  "args":
  {
    "filename": "<</path/to/log-file.log>>"
  }
}
```

#### <a name="ble-module-configuration"></a>Configuração do módulo var

configuração de exemplo de Olá para o dispositivo de var Olá assume um dispositivo da Texas Instruments SensorTag. Qualquer dispositivo var padrão que pode funcionar como um GATT periférico deverão funcionar mas poderá ser necessário tooupdate Olá GATT uma característica das IDs e os dados. Adicione o endereço de MAC Olá do seu dispositivo SensorTag:

```json
{
  "name": "SensorTag",
  "loader": {
    "name" : "native",
    "entrypoint" : {
      "module.path": "build/modules/ble/libble.so"
    }
  },
  "args": {
    "controller_index": 0,
    "device_mac_address": "<<AA:BB:CC:DD:EE:FF>>",
    "instructions": [
      {
        "type": "read_once",
        "characteristic_uuid": "00002A24-0000-1000-8000-00805F9B34FB"
      },
      {
        "type": "read_once",
        "characteristic_uuid": "00002A25-0000-1000-8000-00805F9B34FB"
      },
      {
        "type": "read_once",
        "characteristic_uuid": "00002A26-0000-1000-8000-00805F9B34FB"
      },
      {
        "type": "read_once",
        "characteristic_uuid": "00002A27-0000-1000-8000-00805F9B34FB"
      },
      {
        "type": "read_once",
        "characteristic_uuid": "00002A28-0000-1000-8000-00805F9B34FB"
      },
      {
        "type": "read_once",
        "characteristic_uuid": "00002A29-0000-1000-8000-00805F9B34FB"
      },
      {
        "type": "write_at_init",
        "characteristic_uuid": "F000AA02-0451-4000-B000-000000000000",
        "data": "AQ=="
      },
      {
        "type": "read_periodic",
        "characteristic_uuid": "F000AA01-0451-4000-B000-000000000000",
        "interval_in_ms": 1000
      },
      {
        "type": "write_at_exit",
        "characteristic_uuid": "F000AA02-0451-4000-B000-000000000000",
        "data": "AA=="
      }
    ]
  }
}
```

Se não estiver a utilizar um dispositivo SensorTag, reveja a documentação de Olá para sua toodetermine de dispositivo var se são necessários tooupdate Olá GATT uma característica das IDs e valores de dados.

#### <a name="iot-hub-module"></a>Módulo do IoT Hub

Adicione Olá nome do seu IoT Hub. o valor de sufixo de Olá é normalmente **azure devices.net**:

```json
{
  "name": "IoTHub",
  "loader": {
    "name" : "native",
    "entrypoint" : {
      "module.path": "build/modules/iothub/libiothub.so"
    }
  },
  "args": {
    "IoTHubName": "<<Azure IoT Hub Name>>",
    "IoTHubSuffix": "<<Azure IoT Hub Suffix>>",
    "Transport" : "amqp"
  }
}
```

#### <a name="identity-mapping-module-configuration"></a>Configuração do módulo de mapeamento de identidades

Adicione o endereço de MAC Olá dos seus dispositivos SensorTag e ID de dispositivo Olá e chave de Olá **SensorTag_01** dispositivo adicionado tooyour IoT Hub:

```json
{
  "name": "mapping",
  "loader": {
    "name" : "native",
    "entrypoint" : {
      "module.path": "build/modules/identitymap/libidentity_map.so"
    }
  },
  "args": [
    {
      "macAddress": "<<AA:BB:CC:DD:EE:FF>>",
      "deviceId": "<<Azure IoT Hub Device ID>>",
      "deviceKey": "<<Azure IoT Hub Device Key>>"
    }
  ]
}
```

#### <a name="ble-printer-module-configuration"></a>Configuração do módulo var impressora

```json
{
  "name": "BLE Printer",
  "loader": {
    "name" : "native",
    "entrypoint" : {
      "module.path": "build/samples/ble_gateway/ble_printer/libble_printer.so"
    }
  },
  "args": null
}
```

#### <a name="blec2d-module-configuration"></a>Configuração do módulo BLEC2D

```json
{
  "name": "BLEC2D",
  "loader": {
    "name" : "native",
    "entrypoint" : {
      "module.path": "build/modules/ble/libble_c2d.so"
    }
  },
  "args": null
}
```

#### <a name="routing-configuration"></a>Configuração de encaminhamento

Olá seguinte configuração garante seguinte Olá encaminhamento entre os módulos de limite de IoT:

* Olá **registador** módulo recebe e regista todas as mensagens.
* Olá **SensorTag** módulo envia Olá de tooboth mensagens **mapeamento** e **var impressora** módulos.
* Olá **mapeamento** módulo envia mensagens toohello **IoTHub** toobe módulo enviado tooyour IoT Hub.
* Olá **IoTHub** módulo envia mensagens de fazer uma cópia toohello **mapeamento** módulo.
* Olá **mapeamento** módulo envia mensagens toohello **BLEC2D** módulo.
* Olá **BLEC2D** módulo envia mensagens de fazer uma cópia toohello **Sensor Tag** módulo.

```json
"links" : [
    {"source" : "*", "sink" : "Logger" },
    {"source" : "SensorTag", "sink" : "mapping" },
    {"source" : "SensorTag", "sink" : "BLE Printer" },
    {"source" : "mapping", "sink" : "IoTHub" },
    {"source" : "IoTHub", "sink" : "mapping" },
    {"source" : "mapping", "sink" : "BLEC2D" },
    {"source" : "BLEC2D", "sink" : "SensorTag"}
 ]
```

exemplo de Olá toorun, passagem Olá caminho toohello JSON ficheiro de configuração como um parâmetro toohello **var\_gateway** binário. Olá comando seguinte assume que está a utilizar Olá **gateway_sample.json** ficheiro de configuração. Executar este comando de Olá **iot edge** pasta Olá Raspberry Pi:

```sh
./build/samples/ble_gateway/ble_gateway ./samples/ble_gateway/src/gateway_sample.json
```

Poderá ser necessário toopress Olá pequeno botão no Olá SensorTag dispositivo toomake detetável-lo antes de executar o exemplo de Olá.

Quando executar o exemplo de Olá, pode utilizar Olá [Explorador de dispositivo](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) ou Olá [iothub explorer](https://github.com/Azure/iothub-explorer) Olá mensagens ferramenta toomonitor Olá reencaminha o gateway de IoT a partir de dispositivos SensorTag de Olá. Por exemplo, através do Explorador do iothub pode monitorizar as mensagens de dispositivo para a nuvem utilizando Olá os seguintes comandos:

```sh
iothub-explorer monitor-events --login "HostName={Your iot hub name}.azure-devices.net;SharedAccessKeyName=iothubowner;SharedAccessKey={Your IoT Hub key}"
```

## <a name="send-cloud-to-device-messages"></a>Enviar mensagens da cloud para o dispositivo

módulo de var Olá também suporta enviar comandos a partir de dispositivos do IoT Hub toohello. Pode utilizar Olá [Explorador de dispositivo](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) ou Olá [iothub explorer](https://github.com/Azure/iothub-explorer) mensagens JSON ferramenta toosend esse módulo do Olá var gateway reencaminha no dispositivo de var toohello.

Se estiver a utilizar o dispositivo de Texas Instruments SensorTag Olá, pode ativar o LED de Olá vermelho, LED verde ou buzzer ao enviar comandos a partir do IoT Hub. Antes de enviar comandos a partir do IoT Hub, envie primeiro Olá seguintes duas mensagens JSON por ordem. Em seguida, pode enviar quaisquer Olá comandos tooturn lights Olá ou buzzer.

1. Repor todas as LEDs e buzzer Olá (desligue-os):

    ```json
    {
      "type": "write_once",
      "characteristic_uuid": "F000AA65-0451-4000-B000-000000000000",
      "data": "AA=="
    }
    ```

1. Configure e/s como 'remoto':

    ```json
    {
      "type": "write_once",
      "characteristic_uuid": "F000AA66-0451-4000-B000-000000000000",
      "data": "AQ=="
    }
    ```

Agora pode enviar quaisquer Olá os seguintes comandos tooturn lights Olá ou buzzer no dispositivo de SensorTag Olá:

* Ative LED Olá vermelho:

    ```json
    {
      "type": "write_once",
      "characteristic_uuid": "F000AA65-0451-4000-B000-000000000000",
      "data": "AQ=="
    }
    ```

* Ative LED Olá verde:

    ```json
    {
      "type": "write_once",
      "characteristic_uuid": "F000AA65-0451-4000-B000-000000000000",
      "data": "Ag=="
    }
    ```

* Ative buzzer Olá:

    ```json
    {
      "type": "write_once",
      "characteristic_uuid": "F000AA65-0451-4000-B000-000000000000",
      "data": "BA=="
    }
    ```

## <a name="next-steps"></a>Passos Seguintes

Se pretender toogain uma compreensão mais avançada de limite de IoT e experimente alguns exemplos de código, visite o seguinte Olá tutoriais de programador e de recursos:

* [Limite de IoT do Azure][lnk-sdk]

toofurther explorar Olá das capacidades do IoT Hub, consulte:

* [Guia para programadores do IoT Hub][lnk-devguide]

<!-- Links -->
[lnk-ble-samplecode]: https://github.com/Azure/iot-edge/tree/master/samples/ble_gateway
[lnk-free-trial]: https://azure.microsoft.com/pricing/free-trial/
[lnk-explorer-tools]: https://github.com/Azure/azure-iot-sdks/blob/master/doc/manage_iot_hub.md
[lnk-sdk]: https://github.com/Azure/iot-edge/
[lnk-noobs]: https://www.raspberrypi.org/documentation/installation/noobs.md
[lnk-raspbian]: https://www.raspberrypi.org/downloads/raspbian/
[lnk-devguide]: iot-hub-devguide.md
[lnk-create-hub]: iot-hub-create-through-portal.md 
[lnk-pi-ssh]: https://www.raspberrypi.org/documentation/remote-access/ssh/README.md
[lnk-ssh-windows]: https://www.raspberrypi.org/documentation/remote-access/ssh/windows.md
[lnk-ssh-linux]: https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md
