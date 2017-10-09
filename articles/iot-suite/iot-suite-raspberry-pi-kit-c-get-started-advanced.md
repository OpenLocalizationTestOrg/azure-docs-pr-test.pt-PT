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
# <a name="connect-your-raspberry-pi-3-toohello-remote-monitoring-solution-and-enable-remote-firmware-updates-using-c"></a><span data-ttu-id="5464f-104">Ligar a sua solução de monitorização remota de toohello Raspberry Pi 3 e ativar as atualizações de firmware remoto utilizando C</span><span class="sxs-lookup"><span data-stu-id="5464f-104">Connect your Raspberry Pi 3 toohello remote monitoring solution and enable remote firmware updates using C</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-selector](../../includes/iot-suite-raspberry-pi-kit-selector.md)]

<span data-ttu-id="5464f-105">Este tutorial mostra como toouse Olá Starter Kit do Microsoft Azure IoT para Raspberry Pi 3 para:</span><span class="sxs-lookup"><span data-stu-id="5464f-105">This tutorial shows you how toouse hello Microsoft Azure IoT Starter Kit for Raspberry Pi 3 to:</span></span>

* <span data-ttu-id="5464f-106">Desenvolva um leitor de temperatura e humidade que pode comunicar com a nuvem de Olá.</span><span class="sxs-lookup"><span data-stu-id="5464f-106">Develop a temperature and humidity reader that can communicate with hello cloud.</span></span>
* <span data-ttu-id="5464f-107">Ativar e executar uma aplicação de cliente do firmware remoto atualização tooupdate Olá no Olá Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="5464f-107">Enable and perform a remote firmware update tooupdate hello client application on hello Raspberry Pi.</span></span>

<span data-ttu-id="5464f-108">tutorial de Olá utiliza:</span><span class="sxs-lookup"><span data-stu-id="5464f-108">hello tutorial uses:</span></span>

* <span data-ttu-id="5464f-109">SO de Raspbian, linguagem de programação Olá C e Olá SDK do Microsoft Azure IoT para C tooimplement um dispositivo de exemplo.</span><span class="sxs-lookup"><span data-stu-id="5464f-109">Raspbian OS, hello C programming language, and hello Microsoft Azure IoT SDK for C tooimplement a sample device.</span></span>
* <span data-ttu-id="5464f-110">Olá IoT Suite remoto solução pré-configurada de monitorização como Olá baseado na nuvem de back-end.</span><span class="sxs-lookup"><span data-stu-id="5464f-110">hello IoT Suite remote monitoring preconfigured solution as hello cloud-based back end.</span></span>

## <a name="overview"></a><span data-ttu-id="5464f-111">Descrição geral</span><span class="sxs-lookup"><span data-stu-id="5464f-111">Overview</span></span>

<span data-ttu-id="5464f-112">Neste tutorial, conclua Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="5464f-112">In this tutorial, you complete hello following steps:</span></span>

* <span data-ttu-id="5464f-113">Implemente uma instância do tooyour de solução pré-configurada Olá remoto monitorização subscrição do Azure.</span><span class="sxs-lookup"><span data-stu-id="5464f-113">Deploy an instance of hello remote monitoring preconfigured solution tooyour Azure subscription.</span></span> <span data-ttu-id="5464f-114">Este passo automaticamente implementa e configura vários serviços do Azure.</span><span class="sxs-lookup"><span data-stu-id="5464f-114">This step automatically deploys and configures multiple Azure services.</span></span>
* <span data-ttu-id="5464f-115">Configure o seu dispositivo e sensores toocommunicate com o seu computador e Olá solução de monitorização remota.</span><span class="sxs-lookup"><span data-stu-id="5464f-115">Set up your device and sensors toocommunicate with your computer and hello remote monitoring solution.</span></span>
* <span data-ttu-id="5464f-116">Atualize Olá exemplo dispositivo código tooconnect toohello solução de monitorização remota e enviar telemetria que pode ver no dashboard da solução Olá.</span><span class="sxs-lookup"><span data-stu-id="5464f-116">Update hello sample device code tooconnect toohello remote monitoring solution, and send telemetry that you can view on hello solution dashboard.</span></span>
* <span data-ttu-id="5464f-117">Utilize a aplicação de cliente ao hello do tooupdate de código Olá exemplo dispositivo.</span><span class="sxs-lookup"><span data-stu-id="5464f-117">Use hello sample device code tooupdate hello client application.</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-prerequisites](../../includes/iot-suite-raspberry-pi-kit-prerequisites.md)]

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

> [!WARNING]
> <span data-ttu-id="5464f-118">Olá Aprovisiona de solução de monitorização remota de um conjunto de serviços do Azure na sua subscrição do Azure.</span><span class="sxs-lookup"><span data-stu-id="5464f-118">hello remote monitoring solution provisions a set of Azure services in your Azure subscription.</span></span> <span data-ttu-id="5464f-119">implementação de Olá reflete uma arquitetura de empresas reais.</span><span class="sxs-lookup"><span data-stu-id="5464f-119">hello deployment reflects a real enterprise architecture.</span></span> <span data-ttu-id="5464f-120">encargos de consumo do Azure desnecessários tooavoid, elimine a instância da solução de Olá pré-configurada em azureiotsuite.com quando tiver terminado com o mesmo.</span><span class="sxs-lookup"><span data-stu-id="5464f-120">tooavoid unnecessary Azure consumption charges, delete your instance of hello preconfigured solution at azureiotsuite.com when you have finished with it.</span></span> <span data-ttu-id="5464f-121">Se precisar de hello novamente solução pré-configurada, pode recriá-lo facilmente.</span><span class="sxs-lookup"><span data-stu-id="5464f-121">If you need hello preconfigured solution again, you can easily recreate it.</span></span> <span data-ttu-id="5464f-122">Para obter mais informações sobre a redução do consumo ao hello execuções de solução de monitorização remota, consulte [soluções para fins de demonstração de pré-configuradas de configurar o Azure IoT Suite][lnk-demo-config].</span><span class="sxs-lookup"><span data-stu-id="5464f-122">For more information about reducing consumption while hello remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-view-solution](../../includes/iot-suite-raspberry-pi-kit-view-solution.md)]

[!INCLUDE [iot-suite-raspberry-pi-kit-prepare-pi](../../includes/iot-suite-raspberry-pi-kit-prepare-pi.md)]

## <a name="download-and-configure-hello-sample"></a><span data-ttu-id="5464f-123">Transferir e configurar o exemplo de Olá</span><span class="sxs-lookup"><span data-stu-id="5464f-123">Download and configure hello sample</span></span>

<span data-ttu-id="5464f-124">Agora pode transferir e configurar a aplicação de cliente de monitorização remota de Olá no seu Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="5464f-124">You can now download and configure hello remote monitoring client application on your Raspberry Pi.</span></span>

### <a name="clone-hello-repositories"></a><span data-ttu-id="5464f-125">Repositórios de Olá clone</span><span class="sxs-lookup"><span data-stu-id="5464f-125">Clone hello repositories</span></span>

<span data-ttu-id="5464f-126">Se não tiver o feito, Olá clone necessário Olá de repositórios executando os seguintes comandos no seu Pi:</span><span class="sxs-lookup"><span data-stu-id="5464f-126">If you haven't done so already, clone hello required repositories by running hello following commands on your Pi:</span></span>

```sh
cd ~
git clone --recursive https://github.com/Azure-Samples/iot-remote-monitoring-c-raspberrypi-getstartedkit.git
```

### <a name="update-hello-device-connection-string"></a><span data-ttu-id="5464f-127">Atualizar a cadeia de ligação do dispositivo Olá</span><span class="sxs-lookup"><span data-stu-id="5464f-127">Update hello device connection string</span></span>

<span data-ttu-id="5464f-128">Ficheiro de configuração de exemplo de Olá aberto em Olá **nano** editor utilizando Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="5464f-128">Open hello sample configuration file in hello **nano** editor using hello following command:</span></span>

```sh
nano ~/iot-remote-monitoring-c-raspberrypi-getstartedkit/advanced/config/deviceinfo
```

<span data-ttu-id="5464f-129">Substitua os valores de marcador de posição de Olá Olá ID e o IoT Hub informações do dispositivo é criado e guardado no início de Olá deste tutorial.</span><span class="sxs-lookup"><span data-stu-id="5464f-129">Replace hello placeholder values with hello device ID and IoT Hub information you created and saved at hello start of this tutorial.</span></span>

<span data-ttu-id="5464f-130">Quando tiver terminado, Olá conteúdo de Olá deviceinfo ficheiro deverá ser semelhante Olá seguinte exemplo:</span><span class="sxs-lookup"><span data-stu-id="5464f-130">When you are done, hello contents of hello deviceinfo file should look like hello following example:</span></span>

```conf
yourdeviceid
HostName=youriothubname.azure-devices.net;DeviceId=yourdeviceid;SharedAccessKey=yourdevicekey
```

<span data-ttu-id="5464f-131">Guardar as alterações (**Ctrl-O**, **Enter**) e saída Olá editor (**Ctrl-X**).</span><span class="sxs-lookup"><span data-stu-id="5464f-131">Save your changes (**Ctrl-O**, **Enter**) and exit hello editor (**Ctrl-X**).</span></span>

## <a name="build-hello-sample"></a><span data-ttu-id="5464f-132">Exemplo de Olá de compilação</span><span class="sxs-lookup"><span data-stu-id="5464f-132">Build hello sample</span></span>

<span data-ttu-id="5464f-133">Se ainda não o tiver feito, instale pacotes de pré-requisitos de Olá para Olá SDK de dispositivos do IoT do Microsoft Azure para C, executando os seguintes comandos num terminal no Olá Raspberry Pi de Olá:</span><span class="sxs-lookup"><span data-stu-id="5464f-133">If you have not already done so, install hello prerequisite packages for hello Microsoft Azure IoT Device SDK for C by running hello following commands in a terminal on hello Raspberry Pi:</span></span>

```sh
sudo apt-get update
sudo apt-get install g++ make cmake git libcurl4-openssl-dev libssl-dev uuid-dev
```

<span data-ttu-id="5464f-134">Agora pode compilar a solução de exemplo de Olá no Olá Raspberry Pi:</span><span class="sxs-lookup"><span data-stu-id="5464f-134">You can now build hello sample solution on hello Raspberry Pi:</span></span>

```sh
chmod +x ~/iot-remote-monitoring-c-raspberrypi-getstartedkit/advanced/1.0/build.sh
~/iot-remote-monitoring-c-raspberrypi-getstartedkit/advanced/1.0/build.sh
```

<span data-ttu-id="5464f-135">Pode agora executar o programa de exemplo de Olá no Olá Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="5464f-135">You can now run hello sample program on hello Raspberry Pi.</span></span> <span data-ttu-id="5464f-136">Introduza o comando de Olá:</span><span class="sxs-lookup"><span data-stu-id="5464f-136">Enter hello command:</span></span>

  ```sh
  sudo ~/cmake/remote_monitoring/remote_monitoring
  ```

<span data-ttu-id="5464f-137">Olá saída de exemplo seguinte é um exemplo de saída de Olá que consulte na linha de comandos de Olá no Olá Raspberry Pi:</span><span class="sxs-lookup"><span data-stu-id="5464f-137">hello following sample output is an example of hello output you see at hello command prompt on hello Raspberry Pi:</span></span>

![Resultado da aplicação Raspberry Pi][img-raspberry-output]

<span data-ttu-id="5464f-139">Prima **Ctrl-C** programa de Olá tooexit em qualquer altura.</span><span class="sxs-lookup"><span data-stu-id="5464f-139">Press **Ctrl-C** tooexit hello program at any time.</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-view-telemetry-advanced](../../includes/iot-suite-raspberry-pi-kit-view-telemetry-advanced.md)]

1. <span data-ttu-id="5464f-140">No dashboard de solução Olá, clique em **dispositivos** toovisit Olá **dispositivos** página.</span><span class="sxs-lookup"><span data-stu-id="5464f-140">In hello solution dashboard, click **Devices** toovisit hello **Devices** page.</span></span> <span data-ttu-id="5464f-141">Selecione o seu Raspberry Pi na Olá **lista de dispositivos**.</span><span class="sxs-lookup"><span data-stu-id="5464f-141">Select your Raspberry Pi in hello **Device List**.</span></span> <span data-ttu-id="5464f-142">Em seguida, escolha **métodos**:</span><span class="sxs-lookup"><span data-stu-id="5464f-142">Then choose **Methods**:</span></span>

    ![Lista de dispositivos no dashboard][img-list-devices]

1. <span data-ttu-id="5464f-144">No Olá **invocar método** página, escolha **InitiateFirmwareUpdate** no Olá **método** pendente.</span><span class="sxs-lookup"><span data-stu-id="5464f-144">On hello **Invoke Method** page, choose **InitiateFirmwareUpdate** in hello **Method** dropdown.</span></span>

1. <span data-ttu-id="5464f-145">No Olá **FWPackageURI** campo, introduza **https://github.com/Azure-Samples/iot-remote-monitoring-c-raspberrypi-getstartedkit/raw/master/advanced/2.0/package/remote_monitoring.zip**.</span><span class="sxs-lookup"><span data-stu-id="5464f-145">In hello **FWPackageURI** field, enter **https://github.com/Azure-Samples/iot-remote-monitoring-c-raspberrypi-getstartedkit/raw/master/advanced/2.0/package/remote_monitoring.zip**.</span></span> <span data-ttu-id="5464f-146">Este ficheiro de arquivo contém implementação Olá da versão 2.0 do firmware de Olá.</span><span class="sxs-lookup"><span data-stu-id="5464f-146">This archive file contains hello implementation of version 2.0 of hello firmware.</span></span>

1. <span data-ttu-id="5464f-147">Escolha **InvokeMethod**.</span><span class="sxs-lookup"><span data-stu-id="5464f-147">Choose **InvokeMethod**.</span></span> <span data-ttu-id="5464f-148">aplicação Olá Olá Raspberry Pi envia um dashboard de solução de back-toohello confirmação.</span><span class="sxs-lookup"><span data-stu-id="5464f-148">hello app on hello Raspberry Pi sends an acknowledgment back toohello solution dashboard.</span></span> <span data-ttu-id="5464f-149">Em seguida, inicia processo de atualização de firmware Olá ao transferir a versão nova do Olá do firmware de Olá:</span><span class="sxs-lookup"><span data-stu-id="5464f-149">It then starts hello firmware update process by downloading hello new version of hello firmware:</span></span>

    ![Mostrar histórico de método][img-method-history]

## <a name="observe-hello-firmware-update-process"></a><span data-ttu-id="5464f-151">Observar o processo de atualização de firmware Olá</span><span class="sxs-lookup"><span data-stu-id="5464f-151">Observe hello firmware update process</span></span>

<span data-ttu-id="5464f-152">Pode observar o processo de atualização de firmware Olá enquanto é executada no dispositivo Olá e visualizando Olá comunicado propriedades no dashboard de solução Olá:</span><span class="sxs-lookup"><span data-stu-id="5464f-152">You can observe hello firmware update process as it runs on hello device and by viewing hello reported properties in hello solution dashboard:</span></span>

1. <span data-ttu-id="5464f-153">Pode ver o progresso Olá no processo de atualização de Olá no Olá Raspberry Pi:</span><span class="sxs-lookup"><span data-stu-id="5464f-153">You can view hello progress in of hello update process on hello Raspberry Pi:</span></span>

    ![Mostrar Progresso da atualização][img-update-progress]

    > [!NOTE]
    > <span data-ttu-id="5464f-155">aplicação de monitorização remota Olá reinicia automaticamente quando concluir a atualização de Olá.</span><span class="sxs-lookup"><span data-stu-id="5464f-155">hello remote monitoring app restarts silently when hello update completes.</span></span> <span data-ttu-id="5464f-156">Utilize o comando de Olá `ps -ef` tooverify está em execução.</span><span class="sxs-lookup"><span data-stu-id="5464f-156">Use hello command `ps -ef` tooverify it is running.</span></span> <span data-ttu-id="5464f-157">Se pretender que o processo de Olá tooterminate, utilize Olá `kill` comando com o id de processo Olá.</span><span class="sxs-lookup"><span data-stu-id="5464f-157">If you want tooterminate hello process, use hello `kill` command with hello process id.</span></span>

1. <span data-ttu-id="5464f-158">Pode ver o estado de Olá de atualização de firmware Olá, conforme comunicado pelo dispositivo Olá, no portal de solução Olá.</span><span class="sxs-lookup"><span data-stu-id="5464f-158">You can view hello status of hello firmware update, as reported by hello device, in hello solution portal.</span></span> <span data-ttu-id="5464f-159">Olá seguinte captura de ecrã mostra o estado de Olá e duração de cada fase do processo de atualização de Olá e a nova versão de firmware Olá:</span><span class="sxs-lookup"><span data-stu-id="5464f-159">hello following screenshot shows hello status and duration of each stage of hello update process, and hello new firmware version:</span></span>

    ![Mostrar estado da tarefa][img-job-status]

    <span data-ttu-id="5464f-161">Se navegar back toohello dashboard, pode verificar o dispositivo Olá ainda está a enviar telemetria a seguinte atualização de firmware Olá.</span><span class="sxs-lookup"><span data-stu-id="5464f-161">If you navigate back toohello dashboard, you can verify hello device is still sending telemetry following hello firmware update.</span></span>

> [!WARNING]
> <span data-ttu-id="5464f-162">Se deixar Olá em execução na sua conta do Azure de solução de monitorização remota, é-lhe faturado por período de tempo de Olá que é executada.</span><span class="sxs-lookup"><span data-stu-id="5464f-162">If you leave hello remote monitoring solution running in your Azure account, you are billed for hello time it runs.</span></span> <span data-ttu-id="5464f-163">Para obter mais informações sobre a redução do consumo ao hello execuções de solução de monitorização remota, consulte [soluções para fins de demonstração de pré-configuradas de configurar o Azure IoT Suite][lnk-demo-config].</span><span class="sxs-lookup"><span data-stu-id="5464f-163">For more information about reducing consumption while hello remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span> <span data-ttu-id="5464f-164">Elimine a solução pré-configurada de Olá da sua conta do Azure quando tiver concluído a utilizá-la.</span><span class="sxs-lookup"><span data-stu-id="5464f-164">Delete hello preconfigured solution from your Azure account when you have finished using it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5464f-165">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="5464f-165">Next steps</span></span>

<span data-ttu-id="5464f-166">Visite Olá [Dev Center do Azure IoT](https://azure.microsoft.com/develop/iot/) para obter mais exemplos e documentação no Azure IoT.</span><span class="sxs-lookup"><span data-stu-id="5464f-166">Visit hello [Azure IoT Dev Center](https://azure.microsoft.com/develop/iot/) for more samples and documentation on Azure IoT.</span></span>


[img-raspberry-output]: ./media/iot-suite-raspberry-pi-kit-c-get-started-advanced/app-output.png
[img-update-progress]: ./media/iot-suite-raspberry-pi-kit-c-get-started-advanced/updateprogress.png
[img-job-status]: ./media/iot-suite-raspberry-pi-kit-c-get-started-advanced/jobstatus.png
[img-list-devices]: ./media/iot-suite-raspberry-pi-kit-c-get-started-advanced/listdevices.png
[img-method-history]: ./media/iot-suite-raspberry-pi-kit-c-get-started-advanced/methodhistory.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md