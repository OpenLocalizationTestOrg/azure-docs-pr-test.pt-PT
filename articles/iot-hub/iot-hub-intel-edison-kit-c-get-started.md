---
title: aaaIntel Edison toocloud (C) - ligar Intel Edison tooAzure IoT Hub | Microsoft Docs
description: Saiba como toosetup e ligar Intel Edison tooAzure IoT Hub para a plataforma de nuvem do Azure do Intel Edison toosend dados toohello neste tutorial.
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: iot do Azure intel edison, intel iothub edison, intel edison enviar dados toocloud, intel edison toocloud
ms.assetid: 4885fa2c-c2ee-4253-b37f-ccd55f92b006
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 4/17/2017
ms.author: xshi
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d0928e6c7870d724ff2044280937a45a9e032c75
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="connect-intel-edison-tooazure-iot-hub-c"></a>Ligar Intel Edison tooAzure IoT Hub (C)

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

Neste tutorial, comece por Olá Noções básicas de trabalhar com Intel Edison de aprendizagem. Em seguida, saiba como tooseamlessly ligar a sua nuvem toohello de dispositivos utilizando [IoT Hub do Azure](iot-hub-what-is-iot-hub.md).

Não tem um kit ainda? Iniciar [aqui](https://azure.microsoft.com/develop/iot/starter-kits)

## <a name="what-you-do"></a>O que fazer

* Intel Edison o programa de configuração e e Grove módulos.
* Crie um hub IoT.
* Registe um dispositivo para Edison no seu IoT hub.
* Execute um exemplo de aplicação no Edison toosend sensor dados tooyour do IoT hub.

Ligar Intel Edison tooan do IoT hub que criou. Em seguida, execute um exemplo de aplicação no Edison toocollect relativos à temperatura e humidade dados de um sensor de temperatura Grove. Por fim, enviar Olá sensor dados tooyour do IoT hub.

## <a name="what-you-learn"></a>O que irá aprender

* Como toocreate um hub IoT do Azure e obter a cadeia de ligação do novo dispositivo.
* Como tooconnect Edison com um sensor de temperatura Grove.
* Como dados de sensores de toocollect ao executar uma aplicação de exemplo no Edison.
* Como toosend sensor dados tooyour do IoT hub.

## <a name="what-you-need"></a>Do que precisa

![Do que precisa](media/iot-hub-intel-edison-kit-c-get-started/0_kit.png)

* Olá quadro Intel Edison
* Placa de expansão Arduino
* Uma subscrição ativa do Azure. Se não tiver uma conta do Azure, [criar uma conta de avaliação gratuita do Azure](https://azure.microsoft.com/free/) em apenas alguns minutos.
* Um Mac ou num PC com Windows ou Linux.
* Uma ligação à Internet.
* Um cabo USB de um de tooType Micro B
* Alimentação direta atual (DC). Fonte de alimentação deve ser classificado da seguinte forma:
  - 7 15V DC
  - Pelo menos 1500mA
  - pin de center/interna Olá deve ser Olá positivos pólo de fonte de alimentação Olá

Olá seguintes itens é opcional:

* Grove proteção Base V2
* Grove - Sensor de temperatura
* Grove cabo
* Qualquer barras spacer ou screws incluídos em empacotamento Olá, incluindo quadro de expansão de toohello Olá módulo dois screws toofasten e quatro conjuntos de screws e plastic spacers.

> [!NOTE] 
Estes itens são opcionais, porque o suporte de exemplo de código Olá simulated dados de sensores.

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="setup-intel-edison"></a>A configuração Intel Edison

### <a name="assemble-your-board"></a>Monte a sua placa

Esta secção contém passos tooattach a placa de expansão do Intel Edison de® módulo tooyour.

1. Coloque o módulo de Intel Edison de® Olá dentro do contorno Olá branco no seu painel expansão, lining segurança holes Olá no módulo Olá com screws Olá no quadro de expansão de Olá.

2. Prima para baixo no módulo Olá imediatamente por baixo palavras Olá `What will you make?` até sentir um snap.

   ![Monte quadro 2](media/iot-hub-intel-edison-kit-c-get-started/1_assemble_board2.jpg)

3. Utilize Olá dois nuts hexadecimais (incluídos no pacote de Olá) toosecure Olá módulo toohello expansão quadro.

   ![Monte quadro 3](media/iot-hub-intel-edison-kit-c-get-started/2_assemble_board3.jpg)

4. Inserir uma screw dos holes canto quatro Olá no quadro de expansão de Olá. Twist e reforçar a um dos spacers plastic de Olá branco no screw Olá.

   ![Monte quadro 4](media/iot-hub-intel-edison-kit-c-get-started/3_assemble_board4.jpg)

5. Repita para Olá outros spacers três canto.

   ![Monte quadro 5](media/iot-hub-intel-edison-kit-c-get-started/4_assemble_board5.jpg)

Agora é assembled seu painel.

   ![placa assembled](media/iot-hub-intel-edison-kit-c-get-started/5_assembled_board.jpg)

### <a name="connect-hello-grove-base-shield-and-hello-temperature-sensor"></a>Ligar Olá Grove Base proteção e sensor de temperatura Olá

1. Coloque Olá Grove Base proteção no quadro tooyour. Certifique-se de que todos os pins totalmente são ligados à sua placa.
   
   ![Proteção de Base Grove](media/iot-hub-intel-edison-kit-c-get-started/6_grove_base_sheild.jpg)

2. Sensor de temperatura de utilização Grove cabo tooconnect Grove no Olá Grove Base proteção **A0** porta.

   ![Ligar tootemperature sensor](media/iot-hub-intel-edison-kit-c-get-started/7_temperature_sensor.jpg)
   
   ![Ligação EDISON e sensor](media/iot-hub-intel-edison-kit-c-get-started/16_edion_sensor.png)

O sensor está agora pronta.

### <a name="power-up-edison"></a>Energia segurança Edison

1. Plug-in fonte de alimentação Olá.

   ![Plug-in fonte de alimentação](media/iot-hub-intel-edison-kit-c-get-started/8_plug_power.jpg)

2. Um LED verde (com a etiqueta DS1 no Olá quadro de expansão Arduino *) deve ser apresentado e permaneça lit.

3. Aguarde um minuto para Olá quadro toofinish arrancar de segurança.

   > [!NOTE]
   > Se não tiver uma fonte de alimentação do DC, pode ainda quadro de Olá de energia através de uma porta USB. Consulte `Connect Edison tooyour computer` secção para obter detalhes. A ligar a sua placa desta forma poderão resultar num comportamento imprevisível do seu painel, especialmente quando através de Wi-Fi ou ocasionar motors.

### <a name="connect-edison-tooyour-computer"></a>Ligue Edison tooyour computador

1. Alternar para baixo Olá microswitch para Olá dois micro portas USB, para que Edison está no modo de dispositivo. Para as diferenças entre o modo de anfitrião e de dispositivo, referência [aqui](https://software.intel.com/en-us/node/628233#usb-device-mode-vs-usb-host-mode).

   ![Alternar para baixo Olá microswitch](media/iot-hub-intel-edison-kit-c-get-started/9_toggle_down_microswitch.jpg)

2. Cabo do Olá micro USB ligue-se a porta USB de micro superior de Olá.

   ![Porta USB de micro superior](media/iot-hub-intel-edison-kit-c-get-started/10_top_usbport.jpg)

3. Plug Olá outra extremidade do cabo USB no seu computador.

   ![Computador USB](media/iot-hub-intel-edison-kit-c-get-started/11_computer_usb.jpg)

4. Ficará a saber o que a placa é completamente inicializada quando o computador monta uma nova unidade (muito semelhante a inserir um cartão SD, no seu computador).

## <a name="download-and-run-hello-configuration-tool"></a>Transfira e execute a ferramenta de configuração de Olá
Obter a ferramenta configuração mais recente Olá do [esta ligação](https://software.intel.com/en-us/iot/hardware/edison/downloads) listados na Olá `Installers` cabeçalho. Executar a ferramenta de Olá e siga o ecrã instruções, clicar em seguinte, quando necessário

### <a name="flash-firmware"></a>Flash firmware
1. No Olá `Set up options` página, clique em `Flash Firmware`.
2. Selecione Olá tooflash de imagem no seu painel efetuando um dos seguintes Olá:
   - toodownload e flash seu painel com Olá mais recente firmware imagem disponível a partir da Intel, selecione `Download hello latest image version xxxx`.
   - Selecione a placa com uma imagem já tiver guardado no seu computador, de tooflash `Select hello local image`. Procure a imagem de Olá selecione tooand pretende tooflash tooyour quadro.
3. ferramenta de configuração de Olá tentará tooflash seu painel. processo de intermitente completo Olá pode demorar até too10 minutos.

### <a name="set-password"></a>Definir palavra-passe
1. No Olá `Set up options` página, clique em `Enable Security`.
2. Pode definir um nome personalizado para o seu painel Intel Edison de®. Isto é opcional.
3. Escreva uma palavra-passe para a placa, em seguida, clique em `Set password`.
4. Marcar para baixo Olá palavra-passe, que é utilizado mais tarde.

### <a name="connect-wi-fi"></a>Estabelecer a ligação Wi-Fi
1. No Olá `Set up options` página, clique em `Connect Wi-Fi`. Aguarde pela cópia de segurança tooone minuto, como as análises de computador para redes Wi-Fi disponíveis.
2. De Olá `Detected Networks` pendente lista, selecione a sua rede.
3. De Olá `Security` na lista pendente, tipo de segurança da rede Olá selecione.
4. Indique as informações de início de sessão e palavra-passe e clique em `Configure Wi-Fi`.
5. Marcar para baixo Olá endereço IP, que é utilizado mais tarde.

> [!NOTE]
> Certifique-se que Edison toohello ligado, mesmo que o computador de rede. O computador liga-se tooyour Edison através do endereço IP Olá.

   ![Ligar tootemperature sensor](media/iot-hub-intel-edison-kit-c-get-started/12_configuration_tool.png)

Parabéns! Configurou com êxito Edison.

## <a name="run-a-sample-application-on-intel-edison"></a>Executar uma aplicação de exemplo no Intel Edison

### <a name="prepare-hello-azure-iot-device-sdk"></a>Preparar Olá SDK de dispositivos do IoT do Azure

1. Utilize um dos seguintes clientes SSH do seu tooyour de tooconnect do computador anfitrião Intel Edison de Olá. endereço IP Olá é da ferramenta de configuração de Olá e palavra-passe de Olá é Olá um que definiu essa ferramenta.
    - [PuTTY](http://www.putty.org/) para Windows.
    - Olá SSH no cliente incorporado Ubuntu ou macOS (executar `ssh root@"hello IP address"`).

2. Clone Olá exemplo aplicação tooyour dispositivo cliente. 
   
   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-c-intel-edison-client-app.git
   ```

3. Em seguida, navegue Olá toorun toohello repositório pasta os seguintes comandos toobuild SDK IoT do Azure

   ```bash
   cd iot-hub-c-intel-edison-client-app
   sed -i -e 's/\r$//' buildSDK.sh
   chmod 755 buildSDK.sh
   ./buildSDK.sh
   ```

### <a name="configure-hello-sample-application"></a>Configurar a aplicação de exemplo de Olá

1. Abra o ficheiro de configuração de Olá executando Olá os seguintes comandos:

   ```bash
   nano config.h
   ```

   ![Ficheiro de configuração](media/iot-hub-intel-edison-kit-c-get-started/13_configure_file.png)

   Existem dois macros neste ficheiro, pode configurate. Olá primeiro um é `INTERVAL`, que define o intervalo de tempo de Olá entre duas mensagens que enviam toocloud. Olá segunda `SIMULATED_DATA`, que é um valor booleano para se toouse simulated dados de sensores ou não.

   Se lhe **não tiver sensor Olá**, hello Defina `SIMULATED_DATA` valor demasiado`1` aplicação de exemplo de Olá toomake criar e utilizar dados de sensores simulados.

2. Guarde e saia, premindo O controlo > introduza > X de controlo.

### <a name="build-and-run-hello-sample-application"></a>Compilar e executar a aplicação de exemplo de Olá

1. Crie aplicação de exemplo de Olá executando Olá os seguintes comandos:

   ```bash
   cmake . && make
   ```
   ![Saída de compilação](media/iot-hub-intel-edison-kit-c-get-started/14_build_output.png)

1. Execute a aplicação de exemplo de Olá executando Olá os seguintes comandos:

   ```bash
   sudo ./app '<your Azure IoT hub device connection string>'
   ```

   > [!NOTE] 
   Certifique-se de que copiar-colar a cadeia de ligação de dispositivo de Olá para plicas Olá.

Deverá ver a seguinte Olá de saída que mostra Olá sensor dados e Olá mensagens enviadas tooyour IoT hub.

![Saída - dados de sensores enviados a partir do IoT hub do Intel Edison tooyour](media/iot-hub-intel-edison-kit-c-get-started/15_message_sent.png)

## <a name="next-steps"></a>Passos seguintes

Executar um dados de sensores de toocollect de aplicação de exemplo e enviá-lo tooyour IoT hub.

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
