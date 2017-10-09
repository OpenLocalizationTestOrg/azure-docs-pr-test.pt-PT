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
# <a name="connect-your-raspberry-pi-3-toohello-remote-monitoring-solution-and-send-telemetry-from-a-real-sensor-using-nodejs"></a><span data-ttu-id="b9486-104">Ligar a sua solução de monitorização remota de toohello Raspberry Pi 3 e enviar telemetria a partir de um sensor real com o Node.js</span><span class="sxs-lookup"><span data-stu-id="b9486-104">Connect your Raspberry Pi 3 toohello remote monitoring solution and send telemetry from a real sensor using Node.js</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-selector](../../includes/iot-suite-raspberry-pi-kit-selector.md)]

<span data-ttu-id="b9486-105">Este tutorial mostra como toouse hello Starter Kit do Microsoft Azure IoT para Raspberry Pi 3 toodevelop um leitor de temperatura e humidade que pode comunicar com a nuvem de Olá.</span><span class="sxs-lookup"><span data-stu-id="b9486-105">This tutorial shows you how toouse hello Microsoft Azure IoT Starter Kit for Raspberry Pi 3 toodevelop a temperature and humidity reader that can communicate with hello cloud.</span></span> <span data-ttu-id="b9486-106">tutorial de Olá utiliza:</span><span class="sxs-lookup"><span data-stu-id="b9486-106">hello tutorial uses:</span></span>

- <span data-ttu-id="b9486-107">SO de Raspbian, Olá Node.js linguagem de programação e hello SDK do Microsoft Azure IoT para Node.js tooimplement um dispositivo de exemplo.</span><span class="sxs-lookup"><span data-stu-id="b9486-107">Raspbian OS, hello Node.js programming language, and hello Microsoft Azure IoT SDK for Node.js tooimplement a sample device.</span></span>
- <span data-ttu-id="b9486-108">Olá IoT Suite remoto solução pré-configurada de monitorização como Olá baseado na nuvem de back-end.</span><span class="sxs-lookup"><span data-stu-id="b9486-108">hello IoT Suite remote monitoring preconfigured solution as hello cloud-based back end.</span></span>

## <a name="overview"></a><span data-ttu-id="b9486-109">Descrição geral</span><span class="sxs-lookup"><span data-stu-id="b9486-109">Overview</span></span>

<span data-ttu-id="b9486-110">Neste tutorial, conclua Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="b9486-110">In this tutorial, you complete hello following steps:</span></span>

- <span data-ttu-id="b9486-111">Implemente uma instância do tooyour de solução pré-configurada Olá remoto monitorização subscrição do Azure.</span><span class="sxs-lookup"><span data-stu-id="b9486-111">Deploy an instance of hello remote monitoring preconfigured solution tooyour Azure subscription.</span></span> <span data-ttu-id="b9486-112">Este passo automaticamente implementa e configura vários serviços do Azure.</span><span class="sxs-lookup"><span data-stu-id="b9486-112">This step automatically deploys and configures multiple Azure services.</span></span>
- <span data-ttu-id="b9486-113">Configure o seu dispositivo e sensores toocommunicate com o seu computador e Olá solução de monitorização remota.</span><span class="sxs-lookup"><span data-stu-id="b9486-113">Set up your device and sensors toocommunicate with your computer and hello remote monitoring solution.</span></span>
- <span data-ttu-id="b9486-114">Atualize Olá exemplo dispositivo código tooconnect toohello solução de monitorização remota e enviar telemetria que pode ver no dashboard da solução Olá.</span><span class="sxs-lookup"><span data-stu-id="b9486-114">Update hello sample device code tooconnect toohello remote monitoring solution, and send telemetry that you can view on hello solution dashboard.</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-prerequisites](../../includes/iot-suite-raspberry-pi-kit-prerequisites.md)]

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

> [!WARNING]
> <span data-ttu-id="b9486-115">Olá Aprovisiona de solução de monitorização remota de um conjunto de serviços do Azure na sua subscrição do Azure.</span><span class="sxs-lookup"><span data-stu-id="b9486-115">hello remote monitoring solution provisions a set of Azure services in your Azure subscription.</span></span> <span data-ttu-id="b9486-116">implementação de Olá reflete uma arquitetura de empresas reais.</span><span class="sxs-lookup"><span data-stu-id="b9486-116">hello deployment reflects a real enterprise architecture.</span></span> <span data-ttu-id="b9486-117">encargos de consumo do Azure desnecessários tooavoid, elimine a instância da solução de Olá pré-configurada em azureiotsuite.com quando tiver terminado com o mesmo.</span><span class="sxs-lookup"><span data-stu-id="b9486-117">tooavoid unnecessary Azure consumption charges, delete your instance of hello preconfigured solution at azureiotsuite.com when you have finished with it.</span></span> <span data-ttu-id="b9486-118">Se precisar de hello novamente solução pré-configurada, pode recriá-lo facilmente.</span><span class="sxs-lookup"><span data-stu-id="b9486-118">If you need hello preconfigured solution again, you can easily recreate it.</span></span> <span data-ttu-id="b9486-119">Para obter mais informações sobre a redução do consumo ao hello execuções de solução de monitorização remota, consulte [soluções para fins de demonstração de pré-configuradas de configurar o Azure IoT Suite][lnk-demo-config].</span><span class="sxs-lookup"><span data-stu-id="b9486-119">For more information about reducing consumption while hello remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-view-solution](../../includes/iot-suite-raspberry-pi-kit-view-solution.md)]

[!INCLUDE [iot-suite-raspberry-pi-kit-prepare-pi](../../includes/iot-suite-raspberry-pi-kit-prepare-pi.md)]

## <a name="download-and-configure-hello-sample"></a><span data-ttu-id="b9486-120">Transferir e configurar o exemplo de Olá</span><span class="sxs-lookup"><span data-stu-id="b9486-120">Download and configure hello sample</span></span>

<span data-ttu-id="b9486-121">Agora pode transferir e configurar a aplicação de cliente de monitorização remota de Olá no seu Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="b9486-121">You can now download and configure hello remote monitoring client application on your Raspberry Pi.</span></span>

### <a name="install-nodejs"></a><span data-ttu-id="b9486-122">Instalar o Node.js</span><span class="sxs-lookup"><span data-stu-id="b9486-122">Install Node.js</span></span>

<span data-ttu-id="b9486-123">Instale o Node.js no seu Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="b9486-123">Install Node.js on your Raspberry Pi.</span></span> <span data-ttu-id="b9486-124">Olá IoT SDK para Node.js requer a versão 0.11.5 do Node.js ou posterior.</span><span class="sxs-lookup"><span data-stu-id="b9486-124">hello IoT SDK for Node.js requires version 0.11.5 of Node.js or later.</span></span> <span data-ttu-id="b9486-125">Olá passos seguintes mostram como tooinstall Node.js v6.10.2 no seu Raspberry Pi:</span><span class="sxs-lookup"><span data-stu-id="b9486-125">hello following steps show you how tooinstall Node.js v6.10.2 on your Raspberry Pi:</span></span>

1. <span data-ttu-id="b9486-126">Utilize Olá tooupdate de comando a seguir a Raspberry Pi:</span><span class="sxs-lookup"><span data-stu-id="b9486-126">Use hello following command tooupdate your Raspberry Pi:</span></span>

    ```sh
    sudo apt-get update
    ```

1. <span data-ttu-id="b9486-127">Utilize os seguintes comandos toodownload Olá Node.js binários tooyour Raspberry Pi de Olá:</span><span class="sxs-lookup"><span data-stu-id="b9486-127">Use hello following command toodownload hello Node.js binaries tooyour Raspberry Pi:</span></span>

    ```sh
    wget https://nodejs.org/dist/v6.10.2/node-v6.10.2-linux-armv7l.tar.gz
    ```

1. <span data-ttu-id="b9486-128">Utilize Olá binários de Olá tooinstall de comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="b9486-128">Use hello following command tooinstall hello binaries:</span></span>

    ```sh
    sudo tar -C /usr/local --strip-components 1 -xzf node-v6.10.2-linux-armv7l.tar.gz
    ```

1. <span data-ttu-id="b9486-129">Utilize Olá tooverify de comando que instalou o Node.js v6.10.2 com êxito os seguintes:</span><span class="sxs-lookup"><span data-stu-id="b9486-129">Use hello following command tooverify you have installed Node.js v6.10.2 successfully:</span></span>

    ```sh
    node --version
    ```

### <a name="clone-hello-repositories"></a><span data-ttu-id="b9486-130">Repositórios de Olá clone</span><span class="sxs-lookup"><span data-stu-id="b9486-130">Clone hello repositories</span></span>

<span data-ttu-id="b9486-131">Se ainda não o fez, Olá clone necessário Olá de repositórios executando os seguintes comandos no seu Pi:</span><span class="sxs-lookup"><span data-stu-id="b9486-131">If you haven't already done so, clone hello required repositories by running hello following commands on your Pi:</span></span>

```sh
cd ~
git clone --recursive https://github.com/Azure-Samples/iot-remote-monitoring-node-raspberrypi-getstartedkit.git`
```

### <a name="update-hello-device-connection-string"></a><span data-ttu-id="b9486-132">Atualizar a cadeia de ligação do dispositivo Olá</span><span class="sxs-lookup"><span data-stu-id="b9486-132">Update hello device connection string</span></span>

<span data-ttu-id="b9486-133">Ficheiro de origem de exemplo de Olá aberta no Olá **nano** editor utilizando Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="b9486-133">Open hello sample source file in hello **nano** editor using hello following command:</span></span>

```sh
nano ~/iot-remote-monitoring-node-raspberrypi-getstartedkit/basic/remote_monitoring.js
```

<span data-ttu-id="b9486-134">Localize a linha de Olá:</span><span class="sxs-lookup"><span data-stu-id="b9486-134">Find hello line:</span></span>

```javascript
var connectionString = 'HostName=[Your IoT hub name].azure-devices.net;DeviceId=[Your device id];SharedAccessKey=[Your device key]';
```

<span data-ttu-id="b9486-135">Substitua os valores de marcador de posição de Olá dispositivo Olá e informações de IoT Hub é criado e guardado no início de Olá deste tutorial.</span><span class="sxs-lookup"><span data-stu-id="b9486-135">Replace hello placeholder values with hello device and IoT Hub information you created and saved at hello start of this tutorial.</span></span> <span data-ttu-id="b9486-136">Guardar as alterações (**Ctrl-O**, **Enter**) e saída Olá editor (**Ctrl-X**).</span><span class="sxs-lookup"><span data-stu-id="b9486-136">Save your changes (**Ctrl-O**, **Enter**) and exit hello editor (**Ctrl-X**).</span></span>

## <a name="run-hello-sample"></a><span data-ttu-id="b9486-137">Executar o exemplo de Olá</span><span class="sxs-lookup"><span data-stu-id="b9486-137">Run hello sample</span></span>

<span data-ttu-id="b9486-138">Seguinte Olá executar comandos tooinstall Olá pré-requisitos pacotes de exemplo de Olá:</span><span class="sxs-lookup"><span data-stu-id="b9486-138">Run hello following commands tooinstall hello prerequisite packages for hello sample:</span></span>

```sh
cd ~/iot-remote-monitoring-node-raspberrypi-getstartedkit/basic
npm install
```

<span data-ttu-id="b9486-139">Pode agora executar o programa de exemplo de Olá no Olá Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="b9486-139">You can now run hello sample program on hello Raspberry Pi.</span></span> <span data-ttu-id="b9486-140">Introduza o comando de Olá:</span><span class="sxs-lookup"><span data-stu-id="b9486-140">Enter hello command:</span></span>

```sh
sudo node ~/iot-remote-monitoring-node-raspberrypi-getstartedkit/basic/remote_monitoring.js
```

<span data-ttu-id="b9486-141">Olá saída de exemplo seguinte é um exemplo de saída de Olá que consulte na linha de comandos de Olá no Olá Raspberry Pi:</span><span class="sxs-lookup"><span data-stu-id="b9486-141">hello following sample output is an example of hello output you see at hello command prompt on hello Raspberry Pi:</span></span>

![Resultado da aplicação Raspberry Pi][img-raspberry-output]

<span data-ttu-id="b9486-143">Prima **Ctrl-C** programa de Olá tooexit em qualquer altura.</span><span class="sxs-lookup"><span data-stu-id="b9486-143">Press **Ctrl-C** tooexit hello program at any time.</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-view-telemetry](../../includes/iot-suite-raspberry-pi-kit-view-telemetry.md)]

## <a name="next-steps"></a><span data-ttu-id="b9486-144">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="b9486-144">Next steps</span></span>

<span data-ttu-id="b9486-145">Visite Olá [Dev Center do Azure IoT](https://azure.microsoft.com/develop/iot/) para obter mais exemplos e documentação no Azure IoT.</span><span class="sxs-lookup"><span data-stu-id="b9486-145">Visit hello [Azure IoT Dev Center](https://azure.microsoft.com/develop/iot/) for more samples and documentation on Azure IoT.</span></span>

[img-raspberry-output]: ./media/iot-suite-raspberry-pi-kit-node-get-started-basic/app-output.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md
