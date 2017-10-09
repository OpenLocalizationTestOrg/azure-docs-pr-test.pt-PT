---
title: aaaESP8266 toocloud - ligar o Feather HUZZAH ESP8266 tooAzure IoT Hub | Microsoft Docs
description: Saiba como toosetup e ligue-se Adafruit Feather HUZZAH ESP8266 tooAzure IoT Hub para a mesma plataforma de nuvem do Azure toosend dados toohello neste tutorial.
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: 
ms.assetid: c505aacf-89a8-40ed-a853-493b75bec524
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/15/2017
ms.author: xshi
ms.openlocfilehash: 44fd47232488948d21c7aa71bdd865397e41e63e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="connect-adafruit-feather-huzzah-esp8266-tooazure-iot-hub-in-hello-cloud"></a>Ligar Adafruit Feather HUZZAH ESP8266 tooAzure IoT Hub na nuvem de Olá

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

![Ligação entre DHT22, Feather HUZZAH ESP8266 e IoT Hub](media/iot-hub-arduino-huzzah-esp8266-get-started/1_connection-hdt22-feather-huzzah-iot-hub.png)

## <a name="what-you-do"></a>O que fazer


Ligar Adafruit Feather HUZZAH ESP8266 tooan IoT hub que criou. Em seguida, executar uma aplicação de exemplo no ESP8266 toocollect Olá relativos à temperatura e humidade dados a partir de um sensor DHT22. Por fim, enviar Olá sensor dados tooyour do IoT hub.

> [!NOTE]
> Se estiver a utilizar outros quadros ESP8266, ainda pode seguir estes passos tooconnect-tooyour IoT hub. Dependendo do quadro de Olá ESP8266 estiver a utilizar, poderá ter tooreconfigure Olá `LED_PIN`. Por exemplo, se estiver a utilizar ESP8266 de AI Thinker, poderá alterar a `0` demasiado`2`. Não tem um kit ainda? Obtido a partir do Olá [Web site Azure](http://azure.com/iotstarterkits).




## <a name="what-you-learn"></a>O que irá aprender

* Como toocreate um hub IoT e registar um dispositivo para Feather HUZZAH ESP8266
* Como tooconnect Feather HUZZAH ESP8266 com sensor Olá e o seu computador
* Como dados de sensores de toocollect ao executar uma aplicação de exemplo no Feather HUZZAH ESP8266
* Como toosend hello do IoT hub do sensor dados tooyour

## <a name="what-you-need"></a>Do que precisa

![Componentes necessários para Olá tutorial](media/iot-hub-arduino-huzzah-esp8266-get-started/2_parts-needed-for-the-tutorial.png)

toocomplete desta operação, terá de Olá seguintes partes do seu Feather HUZZAH ESP8266 Starter Kit:

* Olá Feather HUZZAH ESP8266 placa
* Um cabo USB de um de tooType Micro USB

É também necessário Olá seguintes ações para o seu ambiente de desenvolvimento:

* Uma subscrição ativa do Azure. Se não tiver uma conta do Azure, [criar uma conta de avaliação gratuita do Azure](https://azure.microsoft.com/free/) em apenas alguns minutos.
* Mac ou PC com Windows ou Ubuntu.
* Rede sem fios para Feather HUZZAH ESP8266 tooconnect para.
* Ferramenta de configuração do Internet ligação toodownload Olá.
* [Arduino IDE](https://www.arduino.cc/en/main/software) versão 1.6.8 ou posterior. Versões anteriores não funcionam com a biblioteca de AzureIoT Olá.

Olá seguintes itens são opcionais no caso de não ter um sensor. Tem também a opção de Olá da utilização de dados de sensores simulados.

* Um sensor de temperatura e humidade Adafruit DHT22
* Um breadboard
* Cablagem jumper M/M


[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="connect-feather-huzzah-esp8266-with-hello-sensor-and-your-computer"></a>Ligar Feather HUZZAH ESP8266 com sensor Olá e o seu computador
Nesta secção, ligar quadro de tooyour Olá sensores. Em seguida, ligue no seu computador tooyour do dispositivo para obter mais utilização.
### <a name="connect-a-dht22-temperature-and-humidity-sensor-toofeather-huzzah-esp8266"></a>Ligar um DHT22 relativos à temperatura e humidade sensor tooFeather HUZZAH ESP8266

Utilize Olá breadboard jumper cablagem toomake Olá ligação e como se segue. Se não tiver um sensor, ignore esta secção dado que pode utilizar os dados de sensores simulados em vez disso.

![Referência de ligações](media/iot-hub-arduino-huzzah-esp8266-get-started/15_connections_on_breadboard.png)


Para sensor pins, utilize Olá wiring os seguintes:


| Iniciar (Sensor)           | Fim (quadro)           | Cor de cabo   |
| -----------------------  | ---------------------- | ------------: |
| VDD (Pin 31F)            | 3 v (afixar 58H)           | Cabo vermelho     |
| DADOS de (Pin 32F)           | GPIO 2 (Pin 46A)       | Cabo azul    |
| GND (Pin 34F)            | GND (PIn 56I)          | Cabo preto   |

Para obter mais informações, consulte [a configuração do sensor Adafruit DHT22](https://learn.adafruit.com/dht/connecting-to-a-dhtxx-sensor) e [Adafruit Feather HUZZAH Esp8266 Pinouts](https://learn.adafruit.com/adafruit-feather-huzzah-esp8266/using-arduino-ide?view=all#pinouts).



Agora a sua ESP8266 de Huzzah Feather devem estar ligadas com um sensor de trabalho.

![Ligar DHT22 com Feather Huzzah](media/iot-hub-arduino-huzzah-esp8266-get-started/8_connect-dht22-feather-huzzah.png)

### <a name="connect-feather-huzzah-esp8266-tooyour-computer"></a>Ligue Feather HUZZAH ESP8266 tooyour computador

Como é mostrado seguinte, utilize Olá Micro USB tooType A USB cable tooconnect Feather HUZZAH ESP8266 tooyour computador.

![Ligue Feather Huzzah tooyour computador](media/iot-hub-arduino-huzzah-esp8266-get-started/9_connect-feather-huzzah-computer.png)

### <a name="add-serial-port-permissions-ubuntu-only"></a>Adicione permissões de porta série (apenas Ubuntu)


Se utilizar Ubuntu, certifique-se que Olá permissões toooperate no Olá USB porta de Feather HUZZAH ESP8266. permissões de porta série tooadd, siga estes passos:


1. Execute Olá os seguintes comandos num terminal:

   ```bash
   ls -l /dev/ttyUSB*
   ls -l /dev/ttyACM*
   ```

   Obter um Olá saídas os seguintes:

   * crw-rw---1 raiz uucp xxxxxxxx
   * crw-rw---1 raiz dialout xxxxxxxx

   No resultado de Olá, repare que `uucp` ou `dialout` é o nome de proprietário do grupo de Olá de Olá porta USB.

1. Adicione grupo de toohello de utilizadores de Olá executando Olá os seguintes comandos:

   ```bash
   sudo usermod -a -G <group-owner-name> <username>
   ```

   `<group-owner-name>`é o nome de proprietário do grupo Olá que obteve no passo anterior Olá. `<username>`é o nome de utilizador Ubuntu.

1. Terminar a sessão do Ubuntu e, em seguida, inicie sessão novamente para Olá alteração tooappear.

## <a name="collect-sensor-data-and-send-it-tooyour-iot-hub"></a>Recolher dados de sensores e enviá-lo tooyour IoT hub

Nesta secção, implementar e executar uma aplicação de exemplo no Feather HUZZAH ESP8266. aplicação de exemplo de Olá fica intermitente Olá LED no Feather HUZZAH ESP8266 e envia temperatura Olá e dados de humidade recolhidos a partir Olá DHT22 sensor tooyour IoT hub.

### <a name="get-hello-sample-application-from-github"></a>Obter a aplicação de exemplo de Olá a partir do GitHub

aplicação de exemplo de Olá está alojada no GitHub. Clone o repositório de exemplo de Olá que contém a aplicação de exemplo de Olá a partir do GitHub. repositório de exemplo de Olá tooclone, siga estes passos:

1. Abra uma linha de comandos ou de uma janela de terminal.
1. Aceda a pasta de tooa onde pretende toobe de aplicação de exemplo de Olá armazenado.
1. Execute Olá os seguintes comandos:

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-feather-huzzah-client-app.git
   ```

Instale o pacote de Olá para Feather HUZZAH ESP8266 no Olá Arduino IDE:

1. Abra a pasta de olá onde a aplicação de exemplo de Olá está armazenada.
1. Abra o ficheiro de app.ino de Olá na pasta de aplicação Olá no Olá Arduino IDE.

   ![Abra a aplicação de exemplo de Olá no Arduino IDE](media/iot-hub-arduino-huzzah-esp8266-get-started/10_arduino-ide-open-sample-app.png)

1. No Olá Arduino IDE, clique em **ficheiro** > **preferências**.
1. No Olá **preferências** caixa de diálogo, clique em Olá ícone seguinte toohello **adicionais URLs de Gestor de quadros** caixa.
1. Na janela de pop-up Olá, introduza Olá seguinte URL e, em seguida, clique em **OK**.

   `http://arduino.esp8266.com/stable/package_esp8266com_index.json`

   ![Url do pacote tooa de ponto no Arduino IDE](media/iot-hub-arduino-huzzah-esp8266-get-started/11_arduino-ide-package-url.png)

1. No Olá **preferência** caixa de diálogo, clique em **OK**.
1. Clique em **ferramentas** > **quadro** > **quadros Manager**e, em seguida, procure esp8266.

   Gestor de quadros indica que ESP8266 com uma versão do 2.2.0 ou posterior está instalado.

   ![Olá esp8266 pacote está instalado](media/iot-hub-arduino-huzzah-esp8266-get-started/12_arduino-ide-esp8266-installed.png)

1. Clique em **ferramentas** > **quadro** > **Adafruit HUZZAH ESP8266**.

### <a name="install-necessary-libraries"></a>Instalar as bibliotecas necessárias

1. No Olá Arduino IDE, clique em **Sketch** > **incluem bibliotecas** > **gerir bibliotecas**.
1. Procure Olá os seguintes nomes de biblioteca um por um. Para cada biblioteca que encontrar, clique em **instalar**.
   * `AzureIoTHub`
   * `AzureIoTUtility`
   * `AzureIoTProtocol_MQTT`
   * `ArduinoJson`
   * `DHT sensor library`
   * `Adafruit Unified Sensor`

### <a name="dont-have-a-real-dht22-sensor"></a>Não tem um sensor DHT22 real?

aplicação de exemplo de Olá pode simular dados relativos à temperatura e humidade no caso de não ter um sensor DHT22 real. tooset Olá exemplo toouse simulated dos dados das aplicações, siga estes passos:

1. Abra Olá `config.h` ficheiro Olá `app` pasta.
1. Localize Olá seguinte linha de código e altere o valor Olá `false` demasiado`true`:
   ```c
   define SIMULATED_DATA true
   ```
   ![Configurar dados de toouse simulado de aplicação de exemplo de Olá](media/iot-hub-arduino-huzzah-esp8266-get-started/13_arduino-ide-configure-app-use-simulated-data.png)

1. Guarde o ficheiro de Olá com `Control-s`.

### <a name="deploy-hello-sample-application-toofeather-huzzah-esp8266"></a>Implementar tooFeather de aplicação de exemplo de Olá HUZZAH ESP8266

1. No Olá Arduino IDE, clique em **ferramenta** > **porta**e, em seguida, clique em de porta série Olá para Feather HUZZAH ESP8266.
1. Clique em **Sketch** > **carregar** toobuild e implementar tooFeather de aplicação de exemplo de Olá HUZZAH ESP8266.

### <a name="enter-your-credentials"></a>Introduza as suas credenciais

Após a conclusão do carregamento de Olá com êxito, siga estes passos tooenter as suas credenciais:

1. No Olá Arduino IDE, clique em **ferramentas** > **Monitor série**.
1. Na janela de monitor de série de Olá, tenha em atenção Olá dois na lista pendente no canto inferior direito de Olá.
1. Selecione **terminar nenhuma linha** para Olá esquerdo na lista pendente.
1. Selecione **transmissão 115200** para Olá direito na lista pendente.
1. A caixa de entrada Olá localizada em Olá parte superior da janela de monitor de série de Olá, introduza Olá seguintes informações se é-lhe perguntado tooprovide-los e, em seguida, clique em **enviar**.
   * SSID Wi-Fi
   * Palavra-passe de Wi-Fi
   * Cadeia de ligação do dispositivo

> [!Note]
> informações de credencial de Olá são armazenadas na Olá EEPROM de Feather HUZZAH ESP8266. Se clicar no botão de reposição de Olá na Olá Feather HUZZAH ESP8266 placa, a aplicação de exemplo de Olá pergunta se pretende que as informações de Olá tooerase. Introduza `Y` informações de Olá toohave apagadas. É-lhe perguntado informações de Olá tooprovide uma segunda vez.

### <a name="verify-hello-sample-application-is-running-successfully"></a>Certifique-se a aplicação de exemplo de Olá é executada com êxito

Se vir seguinte Olá o resultado da janela de monitor de série de Olá e Olá blinking LED no Feather HUZZAH ESP8266, aplicação de exemplo de Olá é executada com êxito.

![Resultado final no Arduino IDE](media/iot-hub-arduino-huzzah-esp8266-get-started/14_arduino-ide-final-output.png)

## <a name="next-steps"></a>Passos seguintes

Com êxito ter ligado um Feather HUZZAH ESP8266 tooyour IoT hub e enviados Olá capturada sensor dados tooyour IoT hub. 

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]

