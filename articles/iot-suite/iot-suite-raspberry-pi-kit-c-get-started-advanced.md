---
title: "atualizações do aaaConnect tooAzure um Raspberry Pi utilizando C toosupport firmware do IoT Suite | Microsoft Docs"
description: "Utilize Olá Starter Kit do Microsoft Azure IoT para Olá Raspberry Pi 3 e o Azure IoT Suite. Utilizar C tooconnect sua toohello Raspberry Pi solução de monitorização remota, enviar telemetria a partir de sensores toohello cloud e efetuar uma atualização de firmware remoto."
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
ms.date: 07/25/2017
ms.author: dobett
ms.openlocfilehash: 36d39c6d754ddb025fd3f6b74d7795ed907b754c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-raspberry-pi-3-toohello-remote-monitoring-solution-and-enable-remote-firmware-updates-using-c"></a>Ligar a sua solução de monitorização remota de toohello Raspberry Pi 3 e ativar as atualizações de firmware remoto utilizando C

[!INCLUDE [iot-suite-raspberry-pi-kit-selector](../../includes/iot-suite-raspberry-pi-kit-selector.md)]

Este tutorial mostra como toouse Olá Starter Kit do Microsoft Azure IoT para Raspberry Pi 3 para:

* Desenvolva um leitor de temperatura e humidade que pode comunicar com a nuvem de Olá.
* Ativar e executar uma aplicação de cliente do firmware remoto atualização tooupdate Olá no Olá Raspberry Pi.

tutorial de Olá utiliza:

* SO de Raspbian, linguagem de programação Olá C e Olá SDK do Microsoft Azure IoT para C tooimplement um dispositivo de exemplo.
* Olá IoT Suite remoto solução pré-configurada de monitorização como Olá baseado na nuvem de back-end.

## <a name="overview"></a>Descrição geral

Neste tutorial, conclua Olá os seguintes passos:

* Implemente uma instância do tooyour de solução pré-configurada Olá remoto monitorização subscrição do Azure. Este passo automaticamente implementa e configura vários serviços do Azure.
* Configure o seu dispositivo e sensores toocommunicate com o seu computador e Olá solução de monitorização remota.
* Atualize Olá exemplo dispositivo código tooconnect toohello solução de monitorização remota e enviar telemetria que pode ver no dashboard da solução Olá.
* Utilize a aplicação de cliente ao hello do tooupdate de código Olá exemplo dispositivo.

[!INCLUDE [iot-suite-raspberry-pi-kit-prerequisites](../../includes/iot-suite-raspberry-pi-kit-prerequisites.md)]

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

> [!WARNING]
> Olá Aprovisiona de solução de monitorização remota de um conjunto de serviços do Azure na sua subscrição do Azure. implementação de Olá reflete uma arquitetura de empresas reais. encargos de consumo do Azure desnecessários tooavoid, elimine a instância da solução de Olá pré-configurada em azureiotsuite.com quando tiver terminado com o mesmo. Se precisar de hello novamente solução pré-configurada, pode recriá-lo facilmente. Para obter mais informações sobre a redução do consumo ao hello execuções de solução de monitorização remota, consulte [soluções para fins de demonstração de pré-configuradas de configurar o Azure IoT Suite][lnk-demo-config].

[!INCLUDE [iot-suite-raspberry-pi-kit-view-solution](../../includes/iot-suite-raspberry-pi-kit-view-solution.md)]

[!INCLUDE [iot-suite-raspberry-pi-kit-prepare-pi](../../includes/iot-suite-raspberry-pi-kit-prepare-pi.md)]

## <a name="download-and-configure-hello-sample"></a>Transferir e configurar o exemplo de Olá

Agora pode transferir e configurar a aplicação de cliente de monitorização remota de Olá no seu Raspberry Pi.

### <a name="clone-hello-repositories"></a>Repositórios de Olá clone

Se não tiver o feito, Olá clone necessário Olá de repositórios executando os seguintes comandos no seu Pi:

```sh
cd ~
git clone --recursive https://github.com/Azure-Samples/iot-remote-monitoring-c-raspberrypi-getstartedkit.git
```

### <a name="update-hello-device-connection-string"></a>Atualizar a cadeia de ligação do dispositivo Olá

Ficheiro de configuração de exemplo de Olá aberto em Olá **nano** editor utilizando Olá os seguintes comandos:

```sh
nano ~/iot-remote-monitoring-c-raspberrypi-getstartedkit/advanced/config/deviceinfo
```

Substitua os valores de marcador de posição de Olá Olá ID e o IoT Hub informações do dispositivo é criado e guardado no início de Olá deste tutorial.

Quando tiver terminado, Olá conteúdo de Olá deviceinfo ficheiro deverá ser semelhante Olá seguinte exemplo:

```conf
yourdeviceid
HostName=youriothubname.azure-devices.net;DeviceId=yourdeviceid;SharedAccessKey=yourdevicekey
```

Guardar as alterações (**Ctrl-O**, **Enter**) e saída Olá editor (**Ctrl-X**).

## <a name="build-hello-sample"></a>Exemplo de Olá de compilação

Se ainda não o tiver feito, instale pacotes de pré-requisitos de Olá para Olá SDK de dispositivos do IoT do Microsoft Azure para C, executando os seguintes comandos num terminal no Olá Raspberry Pi de Olá:

```sh
sudo apt-get update
sudo apt-get install g++ make cmake git libcurl4-openssl-dev libssl-dev uuid-dev
```

Agora pode compilar a solução de exemplo de Olá no Olá Raspberry Pi:

```sh
chmod +x ~/iot-remote-monitoring-c-raspberrypi-getstartedkit/advanced/1.0/build.sh
~/iot-remote-monitoring-c-raspberrypi-getstartedkit/advanced/1.0/build.sh
```

Pode agora executar o programa de exemplo de Olá no Olá Raspberry Pi. Introduza o comando de Olá:

  ```sh
  sudo ~/cmake/remote_monitoring/remote_monitoring
  ```

Olá saída de exemplo seguinte é um exemplo de saída de Olá que consulte na linha de comandos de Olá no Olá Raspberry Pi:

![Resultado da aplicação Raspberry Pi][img-raspberry-output]

Prima **Ctrl-C** programa de Olá tooexit em qualquer altura.

[!INCLUDE [iot-suite-raspberry-pi-kit-view-telemetry-advanced](../../includes/iot-suite-raspberry-pi-kit-view-telemetry-advanced.md)]

1. No dashboard de solução Olá, clique em **dispositivos** toovisit Olá **dispositivos** página. Selecione o seu Raspberry Pi na Olá **lista de dispositivos**. Em seguida, escolha **métodos**:

    ![Lista de dispositivos no dashboard][img-list-devices]

1. No Olá **invocar método** página, escolha **InitiateFirmwareUpdate** no Olá **método** pendente.

1. No Olá **FWPackageURI** campo, introduza **https://github.com/Azure-Samples/iot-remote-monitoring-c-raspberrypi-getstartedkit/raw/master/advanced/2.0/package/remote_monitoring.zip**. Este ficheiro de arquivo contém implementação Olá da versão 2.0 do firmware de Olá.

1. Escolha **InvokeMethod**. aplicação Olá Olá Raspberry Pi envia um dashboard de solução de back-toohello confirmação. Em seguida, inicia processo de atualização de firmware Olá ao transferir a versão nova do Olá do firmware de Olá:

    ![Mostrar histórico de método][img-method-history]

## <a name="observe-hello-firmware-update-process"></a>Observar o processo de atualização de firmware Olá

Pode observar o processo de atualização de firmware Olá enquanto é executada no dispositivo Olá e visualizando Olá comunicado propriedades no dashboard de solução Olá:

1. Pode ver o progresso Olá no processo de atualização de Olá no Olá Raspberry Pi:

    ![Mostrar Progresso da atualização][img-update-progress]

    > [!NOTE]
    > aplicação de monitorização remota Olá reinicia automaticamente quando concluir a atualização de Olá. Utilize o comando de Olá `ps -ef` tooverify está em execução. Se pretender que o processo de Olá tooterminate, utilize Olá `kill` comando com o id de processo Olá.

1. Pode ver o estado de Olá de atualização de firmware Olá, conforme comunicado pelo dispositivo Olá, no portal de solução Olá. Olá seguinte captura de ecrã mostra o estado de Olá e duração de cada fase do processo de atualização de Olá e a nova versão de firmware Olá:

    ![Mostrar estado da tarefa][img-job-status]

    Se navegar back toohello dashboard, pode verificar o dispositivo Olá ainda está a enviar telemetria a seguinte atualização de firmware Olá.

> [!WARNING]
> Se deixar Olá em execução na sua conta do Azure de solução de monitorização remota, é-lhe faturado por período de tempo de Olá que é executada. Para obter mais informações sobre a redução do consumo ao hello execuções de solução de monitorização remota, consulte [soluções para fins de demonstração de pré-configuradas de configurar o Azure IoT Suite][lnk-demo-config]. Elimine a solução pré-configurada de Olá da sua conta do Azure quando tiver concluído a utilizá-la.

## <a name="next-steps"></a>Passos seguintes

Visite Olá [Dev Center do Azure IoT](https://azure.microsoft.com/develop/iot/) para obter mais exemplos e documentação no Azure IoT.


[img-raspberry-output]: ./media/iot-suite-raspberry-pi-kit-c-get-started-advanced/app-output.png
[img-update-progress]: ./media/iot-suite-raspberry-pi-kit-c-get-started-advanced/updateprogress.png
[img-job-status]: ./media/iot-suite-raspberry-pi-kit-c-get-started-advanced/jobstatus.png
[img-list-devices]: ./media/iot-suite-raspberry-pi-kit-c-get-started-advanced/listdevices.png
[img-method-history]: ./media/iot-suite-raspberry-pi-kit-c-get-started-advanced/methodhistory.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md