---
title: aaaProcess mensagens de dispositivo para a nuvem do IoT Hub do Azure (Java) | Microsoft Docs
description: "Como tooprocess mensagens do dispositivo para a nuvem do IoT Hub utilizando regras de encaminhamento e os pontos finais personalizados toodispatch mensagens tooother serviços de back-end."
services: iot-hub
documentationcenter: java
author: dominicbetts
manager: timlt
editor: 
ms.assetid: bd9af5f9-a740-4780-a2a6-8c0e2752cf48
ms.service: iot-hub
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/29/2017
ms.author: dobett
ms.openlocfilehash: 084e84e721ca4297c4d7d6cb06a43b0bed9bce85
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="process-iot-hub-device-to-cloud-messages-java"></a>Processar mensagens do dispositivo para a nuvem do IoT Hub (Java)

[!INCLUDE [iot-hub-selector-process-d2c](../../includes/iot-hub-selector-process-d2c.md)]

IoT Hub do Azure é um serviço completamente gerido que permite fiável e seguras comunicações bidirecionais entre milhões de dispositivos e uma solução de back-end. Outros tutoriais ([introdução ao IoT Hub] e [enviar mensagens da nuvem para o dispositivo com o IoT Hub][lnk-c2d]) mostram-lhe como toouse Olá básico dispositivo para nuvem e da nuvem para o dispositivo funcionalidade serviço de mensagens do IoT Hub.

Este tutorial de mensagens em fila baseia-se no código Olá mostrado Olá [introdução ao IoT Hub] tutorial e apresenta-lhe como toouse mensagem encaminhamento tooprocess de mensagens dispositivo-nuvem de uma forma escalável. tutorial de Olá ilustra como tooprocess mensagens em fila que requerem ação imediata da solução de Olá back-end. Por exemplo, um dispositivo pode enviar uma mensagem de alarme que aciona a inserir um pedido de um sistema CRM. Por outro lado, as mensagens de ponto de dados simplesmente feed para um motor de análise. Por exemplo, a telemetria de temperatura de um dispositivo que é toobe armazenado para análise posterior é uma mensagem de ponto de dados.

No final de Olá deste tutorial, execute três aplicações de consola Java:

* **simulated-device**, uma versão modificada da aplicação Olá criada no Olá [introdução ao IoT Hub] tutorial, envia mensagens do dispositivo para a nuvem de ponto de dados de cada segundo e interativa dispositivo-nuvem mensagens cada 10 segundos. Esta aplicação utiliza Olá AMQP protocolo toocommunicate com o IoT Hub.
* **Read-d2c-messages** apresenta a telemetria de Olá enviada pela sua aplicação de dispositivo.
* **leitura críticos fila** remove mensagens críticos hello do Olá barramento de serviço fila ligada toohello IoT hub.

> [!NOTE]
> IoT Hub tem suporte SDK para várias plataformas de dispositivos e idiomas, incluindo C, Java e JavaScript. Para obter instruções sobre como tooreplace Olá dispositivo neste tutorial com um dispositivo físico, e como tooconnect dispositivos tooan IoT Hub, consulte Olá [Centro de programadores do IoT do Azure].

toocomplete neste tutorial, terá de Olá seguintes:

* Uma versão de trabalho completa do Olá [introdução ao IoT Hub] tutorial.
* Olá mais recente [8 de Kit de desenvolvimento do Java zar](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)
* [Maven 3](https://maven.apache.org/install.html)
* Uma conta ativa do Azure. (Se não tiver uma conta, pode criar uma [conta gratuita] [lnk-free-trial] em apenas alguns minutos.)

É necessário ter algum conhecimento básico de [Storage do Azure] e [Service Bus do Azure].

## <a name="send-interactive-messages-from-a-device-app"></a>Enviar mensagens interativas de uma aplicação de dispositivo
Nesta secção, pode modificar a aplicação de dispositivo de Olá que criou no Olá [introdução ao IoT Hub] tutorial toooccasionally enviar mensagens que necessitam de processamento de imediato.

1. Utilize o editor tooopen Olá simulated-device\src\main\java\com\mycompany\app\app.Java. ficheiro de texto. Este ficheiro contém o código de Olá para Olá **simulated-device** aplicação que criou no Olá [introdução ao IoT Hub] tutorial.

2. Substitua Olá **MessageSender** classe com Olá seguinte código:

    ```java
    private static class MessageSender implements Runnable {

        public void run()  {
            try {
                double minTemperature = 20;
                double minHumidity = 60;
                Random rand = new Random();

                while (true) {
                    String msgStr;
                    Message msg;
                    if (new Random().nextDouble() > 0.7) {
                        msgStr = "This is a critical message.";
                        msg = new Message(msgStr);
                        msg.setProperty("level", "critical");
                    } else {
                        double currentTemperature = minTemperature + rand.nextDouble() * 15;
                        double currentHumidity = minHumidity + rand.nextDouble() * 20; 
                        TelemetryDataPoint telemetryDataPoint = new TelemetryDataPoint();
                        telemetryDataPoint.deviceId = deviceId;
                        telemetryDataPoint.temperature = currentTemperature;
                        telemetryDataPoint.humidity = currentHumidity;

                        msgStr = telemetryDataPoint.serialize();
                        msg = new Message(msgStr);
                    }
                    
                    System.out.println("Sending: " + msgStr);

                    Object lockobj = new Object();
                    EventCallback callback = new EventCallback();
                    client.sendEventAsync(msg, callback, lockobj);

                    synchronized (lockobj) {
                        lockobj.wait();
                    }
                    Thread.sleep(1000);
                }
            } catch (InterruptedException e) {
                System.out.println("Finished.");
            }
        }
    }
    ```
   
    Este método aleatoriamente adiciona propriedade Olá `"level": "critical"` toomessages enviada pelo dispositivo Olá, o que simula uma mensagem que necessita de uma ação imediata por Olá aplicação back-end. aplicação Olá transfere a informação nas propriedades de mensagem de Olá, em vez de no corpo da mensagem Olá, para que o IoT Hub pode encaminhar o destino do Olá mensagem toohello mensagem adequado.
   
   > [!NOTE]
   > Pode utilizar mensagens de tooroute de propriedades de mensagem para vários cenários, incluindo frio-path processar, além disso exemplo de caminho frequente toohello mostrado aqui.

2. Guarde e feche o ficheiro simulated-device\src\main\java\com\mycompany\app\app.Java. de Olá.

    > [!NOTE]
    > Para sake Olá de simplicidade, este tutorial não implementa nenhuma política de repetição. No código de produção, deve implementar uma política de repetição como término exponencial, como sugerido no artigo do MSDN Olá [processamento de erros transitórios].

3. Olá toobuild **simulated-device** aplicação com o Maven, execute Olá seguinte comando na linha de comandos Olá na pasta simulated-device de Olá:

    ```cmd/sh
    mvn clean package -DskipTests
    ```

## <a name="add-a-queue-tooyour-iot-hub-and-route-messages-tooit"></a>Adicionar um IoT de tooyour fila em hub e encaminhar a tooit mensagens

Nesta secção, criar uma fila do Service Bus, ligue-tooyour IoT hub e configurar o seu IoT hub toosend toohello a fila de mensagens com base na presença de Olá de uma propriedade de mensagem de saudação. Para obter mais informações sobre como tooprocess mensagens de filas do Service Bus, consulte [introdução às filas][lnk-sb-queues-java].

1. Criar uma fila do Service Bus, conforme descrito em [introdução às filas][lnk-sb-queues-java]. Tome nota do nome de espaço de nomes e fila Olá.

2. No Olá portal do Azure, abra o seu IoT hub e clique em **pontos finais**.

    ![Pontos finais do IoT hub][30]

3. No Olá **pontos finais** painel, clique em **adicionar** em Olá tooadd superior a fila tooyour do IoT hub. Ponto final do nome Olá **CriticalQueue** e utilizar Olá listas pendentes tooselect **fila do Service Bus**, Olá espaço de nomes de barramento de serviço em que reside a sua fila e Olá nome da sua fila. Quando tiver terminado, clique em **guardar** na parte inferior de Olá.

    ![Adicionar um ponto final][31]

4. Agora, clique em **rotas** no seu IoT Hub. Clique em **adicionar** , Olá parte superior do Olá painel toocreate adicionada uma regra de encaminhamento encaminha mensagens toohello fila apenas. Selecione **DeviceTelemetry** como origem de Olá de dados. Introduza `level="critical"` como condição Olá e escolha a fila de Olá acabou de adicionar como um ponto final personalizado como Olá ponto final de regra de encaminhamento. Quando tiver terminado, clique em **guardar** na parte inferior de Olá.

    ![Adicionar uma rota][32]

    Certifique-se a rota de contingência Olá estiver definida demasiado**ON**. Esta definição é a configuração predefinida Olá um IoT hub.

    ![Rota de contingência][33]

## <a name="optional-read-from-hello-queue-endpoint"></a>(Opcional) Ler a partir do ponto final de fila de Olá

Opcionalmente, podem ler mensagens de Olá do ponto final de fila de Olá, seguindo as instruções Olá [introdução às filas][lnk-sb-queues-java]. Nome Olá aplicação **leitura críticos fila**.

## <a name="run-hello-applications"></a>Executar aplicações de Olá

Agora, está três aplicações de toorun pronto Olá.

1. Olá toorun **read-d2c-messages** aplicação, numa linha de comandos ou shell navegue pasta read-d2c de toohello e executar Olá os seguintes comandos:

   ```cmd/sh
   mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
   ```

   ![Executar read-d2c-messages][readd2c]

2. Olá toorun **leitura críticos fila** aplicação, numa linha de comandos ou shell navegue toohello pasta de leitura fila críticos e executar Olá os seguintes comandos:

   ```cmd/sh
   mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
   ```
   
   ![Executar leitura mensagens crítico][readqueue]

3. Olá toorun **simulated-device** aplicação, numa linha de comandos ou shell navegue pasta simulated-device de toohello e executar Olá os seguintes comandos:

   ```cmd/sh
   mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
   ```
   
   ![Executar simulated-device][simulateddevice]

## <a name="next-steps"></a>Passos seguintes

Neste tutorial, aprendeu como tooreliably emitir mensagens do dispositivo para nuvem utilizando a funcionalidade de encaminhamento de mensagens de Olá do IoT Hub.

Olá [como mensagens de toosend nuvem para o dispositivo com o IoT Hub] [ lnk-c2d] mostra-lhe como toosend mensagens tooyour dispositivos da sua solução de back-end.

Exemplos de toosee de soluções ponto-a-ponto completas que utilizam o IoT Hub, consulte [Azure IoT Suite][lnk-suite].

toolearn mais informações sobre desenvolver soluções de IoT hub, consulte Olá [guia para programadores do IoT Hub].

toolearn mais informações sobre o encaminhamento de mensagens do IoT Hub, consulte [enviar e receber mensagens com o IoT Hub][lnk-devguide-messaging].

<!-- Images. -->
<!-- TODO: UPDATE PICTURES -->
[simulateddevice]: ./media/iot-hub-java-java-process-d2c/runsimulateddevice.png
[readd2c]: ./media/iot-hub-java-java-process-d2c/runprocessinteractive.png
[readqueue]: ./media/iot-hub-java-java-process-d2c/runprocessd2c.png

[30]: ./media/iot-hub-java-java-process-d2c/click-endpoints.png
[31]: ./media/iot-hub-java-java-process-d2c/endpoint-creation.png
[32]: ./media/iot-hub-java-java-process-d2c/route-creation.png
[33]: ./media/iot-hub-java-java-process-d2c/fallback-route.png

<!-- Links -->

[lnk-sb-queues-java]: ../service-bus-messaging/service-bus-java-how-to-use-queues.md

[Storage do Azure]: https://azure.microsoft.com/documentation/services/storage/
[Service Bus do Azure]: https://azure.microsoft.com/documentation/services/service-bus/

[guia para programadores do IoT Hub]: iot-hub-devguide.md
[lnk-devguide-messaging]: iot-hub-devguide-messaging.md
[introdução ao IoT Hub]: iot-hub-java-java-getstarted.md
[Centro de programadores do IoT do Azure]: https://azure.microsoft.com/develop/iot
[processamento de erros transitórios]: https://msdn.microsoft.com/library/hh675232.aspx

<!-- Links -->
[Processamento de falhas transitórias]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx

[lnk-c2d]: iot-hub-java-java-c2d.md
[lnk-suite]: https://azure.microsoft.com/documentation/suites/iot-suite/
