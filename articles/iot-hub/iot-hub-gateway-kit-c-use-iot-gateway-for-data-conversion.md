---
title: "conversão de aaaData no gateway de IoT com limite de IoT do Azure | Microsoft Docs"
description: "Utilize o IoT gateway tooconvert Olá formato de dados de sensor através de um módulo personalizado a partir do Azure IoT Edge."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "conversão de dados de gateway do IOT, transformação de dados do gateway de iot"
ms.assetid: 75f2573d-500b-4405-bff7-61021c4c3500
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/25/2017
ms.author: xshi
ms.openlocfilehash: ae94b1f96f36dfcb4f77fadc0ece3cff3d0bba91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="use-iot-gateway-for-sensor-data-transformation-with-azure-iot-edge"></a>Utilize o gateway de IoT para transformação de dados de sensor com limite de IoT do Azure

> [!NOTE]
> Antes de começar este tutorial, certifique-se que tiver concluído Olá seguir lições na sequência:
> * [Configurar o Intel NUC como um gateway do IoT](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md)
> * [Utilize o IoT gateway tooconnect coisas toohello nuvem - SensorTag tooAzure IoT Hub](iot-hub-gateway-kit-c-iot-gateway-connect-device-to-cloud.md)

Um objetivo de um gateway de Iot é tooprocess recolhidos dados antes de a enviar toohello nuvem. Limite de IoT do Azure introduz módulos que podem ser criados e assembled tooform fluxo de trabalho de processamento de dados de Olá. Um módulo recebe uma mensagem, efetua algumas ações no mesmo e, em seguida, mova-para outros tooprocess de módulos.

## <a name="what-you-learn"></a>O que irá aprender

Pode saber como toocreate tooconvert um módulo mensagens de Olá SensorTag num formato diferente.

## <a name="what-you-do"></a>O que fazer

* Crie um módulo tooconvert uma mensagem recebida num ficheiro em formato Olá. JSON.
* Compile o módulo Olá.
* Adicione aplicação de exemplo Olá módulo toohello var de limite de IoT do Azure.
* Execute a aplicação de exemplo de Olá.

## <a name="what-you-need"></a>Do que precisa

* Olá seguintes tutoriais foi concluídas em sequência:
  * [Configurar o Intel NUC como um gateway do IoT](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md)
  * [Utilize o IoT gateway tooconnect coisas toohello nuvem - SensorTag tooAzure IoT Hub](iot-hub-gateway-kit-c-iot-gateway-connect-device-to-cloud.md)
* Um cliente SSH que é executado no computador anfitrião. PuTTY recomenda-se no Windows. Linux e macOS já vêm com um cliente SSH.
* endereço IP Olá e Olá nome de utilizador e palavra-passe tooaccess Olá gateway a partir do cliente SSH Olá.
* Uma ligação à Internet.

## <a name="create-a-module"></a>Criar um módulo

1. No computador do anfitrião de Olá, execute o cliente SSH Olá e ligar o gateway de IoT toohello.
1. Clone o ficheiros de origem Olá do módulo de conversão de Olá do GitHub toohello diretório raiz do gateway de IoT Olá executando Olá os seguintes comandos:

   ```bash
   cd ~
   git clone https://github.com/Azure-Samples/iot-hub-c-intel-nuc-gateway-customized-module.git
   ```

   Este é um módulo nativo do limite do Azure, escrito no Olá linguagem de programação de C. módulo Olá converte formato Olá de mensagens recebidas Olá seguir uma:

   ```json
   {"deviceId": "Intel NUC Gateway", "messageId": 0, "temperature": 0.0}
   ```

## <a name="compile-hello-module"></a>Compilar o módulo Olá

no módulo de Olá toocompile, execute Olá os seguintes comandos:

```bash
cd iot-hub-c-intel-nuc-gateway-customized-module/my_module
# change hello build script runnable
chmod 777 build.sh
# remove hello invalid windows character
sed -i -e "s/\r$//" build.sh
# run hello build shell script
./build.sh
```

Obtém um `libmy_module.so` depois de concluída a compilação de Olá de ficheiros. Tome nota do caminho absoluto do Olá deste ficheiro.

## <a name="add-hello-module-toohello-ble-sample-application"></a>Adicionar a aplicação de exemplo Olá módulo toohello var

1. Aceda a pasta de amostras toohello executando Olá os seguintes comandos:

   ```bash
   cd /usr/share/azureiotgatewaysdk/samples
   ```

1. Abra o ficheiro de configuração de Olá executando Olá os seguintes comandos:

   ```bash
   vi ble_gateway.json
   ```

1. Adicionar um módulo através da inserção Olá seguinte código toohello `modules` secção.

   ```json
   {
       "name": "MyModule",
       "loader": {
           "name": "native",
           "entrypoint":{
               "module.path": "[Your libmy_module.so path]"
               }
            },
        "args": null
    },
    ```

1. Substitua `[Your libmy_module.so path]` no código Olá com o caminho absoluto do Olá de Olá libmy_module.so' ficheiros.
1. Substitua o código de Olá no Olá `links` secção com Olá seguir uma:

   ```json
   {
       "source": "SensorTag",
       "sink": "MyModule"
   },
   {
       "source": "MyModule",
       "sink": "mapping"
   }
   ```

1. Prima `ESC`e, em seguida, escreva `:wq` ficheiros de Olá toosave.

## <a name="run-hello-sample-application"></a>Executar a aplicação de exemplo de Olá

1. Ligar Olá SensorTag.
1. Definir variável de ambiente de SSL_CERT_FILE Olá executando Olá os seguintes comandos:

   ```bash
   export SSL_CERT_FILE=/etc/ssl/certs/ca-certificates.crt
   ```

1. Aplicação de exemplo de Olá execução com Olá adicionadas módulo executando Olá os seguintes comandos:

   ```bash
   ./ble_gateway ble_gateway.json
   ```

## <a name="next-steps"></a>Passos seguintes

Com êxito já utilizar IoT gateway tooconvert Olá mensagem de saudação do SensorTag num ficheiro em formato Olá. JSON.

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
