---
title: aaaConnect tooAzure um Raspberry Pi IoT Suite com C sensores reais | Microsoft Docs
description: "Utilize Olá Starter Kit do Microsoft Azure IoT para Olá Raspberry Pi 3 e o Azure IoT Suite. Utilizar C tooconnect sua toohello Raspberry Pi solução de monitorização remota, enviar telemetria a partir de sensores toohello cloud e responder toomethods invocado a partir do dashboard de solução Olá."
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
ms.openlocfilehash: 7dac55ae5fde4c6f8e3ea6a7debf9a6822dc07ee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-raspberry-pi-3-toohello-remote-monitoring-solution-and-send-telemetry-from-a-real-sensor-using-c"></a><span data-ttu-id="5bcd6-104">Ligar a sua solução de monitorização remota de toohello Raspberry Pi 3 e enviar telemetria a partir de um sensor real utilizando C</span><span class="sxs-lookup"><span data-stu-id="5bcd6-104">Connect your Raspberry Pi 3 toohello remote monitoring solution and send telemetry from a real sensor using C</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-selector](../../includes/iot-suite-raspberry-pi-kit-selector.md)]

<span data-ttu-id="5bcd6-105">Este tutorial mostra como toouse hello Starter Kit do Microsoft Azure IoT para Raspberry Pi 3 toodevelop um leitor de temperatura e humidade que pode comunicar com a nuvem de Olá.</span><span class="sxs-lookup"><span data-stu-id="5bcd6-105">This tutorial shows you how toouse hello Microsoft Azure IoT Starter Kit for Raspberry Pi 3 toodevelop a temperature and humidity reader that can communicate with hello cloud.</span></span> <span data-ttu-id="5bcd6-106">tutorial de Olá utiliza:</span><span class="sxs-lookup"><span data-stu-id="5bcd6-106">hello tutorial uses:</span></span>

- <span data-ttu-id="5bcd6-107">SO de Raspbian, linguagem de programação Olá C e Olá SDK do Microsoft Azure IoT para C tooimplement um dispositivo de exemplo.</span><span class="sxs-lookup"><span data-stu-id="5bcd6-107">Raspbian OS, hello C programming language, and hello Microsoft Azure IoT SDK for C tooimplement a sample device.</span></span>
- <span data-ttu-id="5bcd6-108">Olá IoT Suite remoto solução pré-configurada de monitorização como Olá baseado na nuvem de back-end.</span><span class="sxs-lookup"><span data-stu-id="5bcd6-108">hello IoT Suite remote monitoring preconfigured solution as hello cloud-based back end.</span></span>

## <a name="overview"></a><span data-ttu-id="5bcd6-109">Descrição geral</span><span class="sxs-lookup"><span data-stu-id="5bcd6-109">Overview</span></span>

<span data-ttu-id="5bcd6-110">Neste tutorial, conclua Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="5bcd6-110">In this tutorial, you complete hello following steps:</span></span>

- <span data-ttu-id="5bcd6-111">Implemente uma instância do tooyour de solução pré-configurada Olá remoto monitorização subscrição do Azure.</span><span class="sxs-lookup"><span data-stu-id="5bcd6-111">Deploy an instance of hello remote monitoring preconfigured solution tooyour Azure subscription.</span></span> <span data-ttu-id="5bcd6-112">Este passo automaticamente implementa e configura vários serviços do Azure.</span><span class="sxs-lookup"><span data-stu-id="5bcd6-112">This step automatically deploys and configures multiple Azure services.</span></span>
- <span data-ttu-id="5bcd6-113">Configure o seu dispositivo e sensores toocommunicate com o seu computador e Olá solução de monitorização remota.</span><span class="sxs-lookup"><span data-stu-id="5bcd6-113">Set up your device and sensors toocommunicate with your computer and hello remote monitoring solution.</span></span>
- <span data-ttu-id="5bcd6-114">Atualize Olá exemplo dispositivo código tooconnect toohello solução de monitorização remota e enviar telemetria que pode ver no dashboard da solução Olá.</span><span class="sxs-lookup"><span data-stu-id="5bcd6-114">Update hello sample device code tooconnect toohello remote monitoring solution, and send telemetry that you can view on hello solution dashboard.</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-prerequisites](../../includes/iot-suite-raspberry-pi-kit-prerequisites.md)]

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

> [!WARNING]
> <span data-ttu-id="5bcd6-115">Olá Aprovisiona de solução de monitorização remota de um conjunto de serviços do Azure na sua subscrição do Azure.</span><span class="sxs-lookup"><span data-stu-id="5bcd6-115">hello remote monitoring solution provisions a set of Azure services in your Azure subscription.</span></span> <span data-ttu-id="5bcd6-116">implementação de Olá reflete uma arquitetura de empresas reais.</span><span class="sxs-lookup"><span data-stu-id="5bcd6-116">hello deployment reflects a real enterprise architecture.</span></span> <span data-ttu-id="5bcd6-117">encargos de consumo do Azure desnecessários tooavoid, elimine a instância da solução de Olá pré-configurada em azureiotsuite.com quando tiver terminado com o mesmo.</span><span class="sxs-lookup"><span data-stu-id="5bcd6-117">tooavoid unnecessary Azure consumption charges, delete your instance of hello preconfigured solution at azureiotsuite.com when you have finished with it.</span></span> <span data-ttu-id="5bcd6-118">Se precisar de hello novamente solução pré-configurada, pode recriá-lo facilmente.</span><span class="sxs-lookup"><span data-stu-id="5bcd6-118">If you need hello preconfigured solution again, you can easily recreate it.</span></span> <span data-ttu-id="5bcd6-119">Para obter mais informações sobre a redução do consumo ao hello execuções de solução de monitorização remota, consulte [soluções para fins de demonstração de pré-configuradas de configurar o Azure IoT Suite][lnk-demo-config].</span><span class="sxs-lookup"><span data-stu-id="5bcd6-119">For more information about reducing consumption while hello remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-view-solution](../../includes/iot-suite-raspberry-pi-kit-view-solution.md)]

[!INCLUDE [iot-suite-raspberry-pi-kit-prepare-pi](../../includes/iot-suite-raspberry-pi-kit-prepare-pi.md)]

## <a name="download-and-configure-hello-sample"></a><span data-ttu-id="5bcd6-120">Transferir e configurar o exemplo de Olá</span><span class="sxs-lookup"><span data-stu-id="5bcd6-120">Download and configure hello sample</span></span>

<span data-ttu-id="5bcd6-121">Agora pode transferir e configurar a aplicação de cliente de monitorização remota de Olá no seu Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="5bcd6-121">You can now download and configure hello remote monitoring client application on your Raspberry Pi.</span></span>

### <a name="clone-hello-repositories"></a><span data-ttu-id="5bcd6-122">Repositórios de Olá clone</span><span class="sxs-lookup"><span data-stu-id="5bcd6-122">Clone hello repositories</span></span>

<span data-ttu-id="5bcd6-123">Se ainda não o fez, Olá clone necessário Olá de repositórios executando os seguintes comandos num terminal no seu Pi:</span><span class="sxs-lookup"><span data-stu-id="5bcd6-123">If you haven't already done so, clone hello required repositories by running hello following commands in a terminal on your Pi:</span></span>

```sh
cd ~
git clone --recursive https://github.com/Azure-Samples/iot-remote-monitoring-c-raspberrypi-getstartedkit.git
git clone --recursive https://github.com/WiringPi/WiringPi.git
```

### <a name="update-hello-device-connection-string"></a><span data-ttu-id="5bcd6-124">Atualizar a cadeia de ligação do dispositivo Olá</span><span class="sxs-lookup"><span data-stu-id="5bcd6-124">Update hello device connection string</span></span>

<span data-ttu-id="5bcd6-125">Ficheiro de origem de exemplo de Olá aberta no Olá **nano** editor utilizando Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="5bcd6-125">Open hello sample source file in hello **nano** editor using hello following command:</span></span>

```sh
nano ~/iot-remote-monitoring-c-raspberrypi-getstartedkit/basic/remote_monitoring/remote_monitoring.c
```

<span data-ttu-id="5bcd6-126">Localize Olá seguintes linhas:</span><span class="sxs-lookup"><span data-stu-id="5bcd6-126">Locate hello following lines:</span></span>

```c
static const char* deviceId = "[Device Id]";
static const char* connectionString = "HostName=[IoTHub Name].azure-devices.net;DeviceId=[Device Id];SharedAccessKey=[Device Key]";
```

<span data-ttu-id="5bcd6-127">Substitua os valores de marcador de posição de Olá dispositivo Olá e informações de IoT Hub é criado e guardado no início de Olá deste tutorial.</span><span class="sxs-lookup"><span data-stu-id="5bcd6-127">Replace hello placeholder values with hello device and IoT Hub information you created and saved at hello start of this tutorial.</span></span> <span data-ttu-id="5bcd6-128">Guardar as alterações (**Ctrl-O**, **Enter**) e saída Olá editor (**Ctrl-X**).</span><span class="sxs-lookup"><span data-stu-id="5bcd6-128">Save your changes (**Ctrl-O**, **Enter**) and exit hello editor (**Ctrl-X**).</span></span>

## <a name="build-hello-sample"></a><span data-ttu-id="5bcd6-129">Exemplo de Olá de compilação</span><span class="sxs-lookup"><span data-stu-id="5bcd6-129">Build hello sample</span></span>

<span data-ttu-id="5bcd6-130">Instale pacotes de pré-requisitos de Olá para Olá SDK de dispositivos do IoT do Microsoft Azure para C, executando os seguintes comandos num terminal no Olá Raspberry Pi de Olá:</span><span class="sxs-lookup"><span data-stu-id="5bcd6-130">Install hello prerequisite packages for hello Microsoft Azure IoT Device SDK for C by running hello following commands in a terminal on hello Raspberry Pi:</span></span>

```sh
sudo apt-get update
sudo apt-get install g++ make cmake git libcurl4-openssl-dev libssl-dev uuid-dev
```

<span data-ttu-id="5bcd6-131">Agora pode compilar a solução de exemplo de Olá atualizado no Olá Raspberry Pi:</span><span class="sxs-lookup"><span data-stu-id="5bcd6-131">You can now build hello updated sample solution on hello Raspberry Pi:</span></span>

```sh
chmod +x ~/iot-remote-monitoring-c-raspberrypi-getstartedkit/basic/build.sh
~/iot-remote-monitoring-c-raspberrypi-getstartedkit/basic/build.sh
```

<span data-ttu-id="5bcd6-132">Pode agora executar o programa de exemplo de Olá no Olá Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="5bcd6-132">You can now run hello sample program on hello Raspberry Pi.</span></span> <span data-ttu-id="5bcd6-133">Introduza o comando de Olá:</span><span class="sxs-lookup"><span data-stu-id="5bcd6-133">Enter hello command:</span></span>

```sh
sudo ~/cmake/remote_monitoring/remote_monitoring
```

<span data-ttu-id="5bcd6-134">Olá saída de exemplo seguinte é um exemplo de saída de Olá que consulte na linha de comandos de Olá no Olá Raspberry Pi:</span><span class="sxs-lookup"><span data-stu-id="5bcd6-134">hello following sample output is an example of hello output you see at hello command prompt on hello Raspberry Pi:</span></span>

![Resultado da aplicação Raspberry Pi][img-raspberry-output]

<span data-ttu-id="5bcd6-136">Prima **Ctrl-C** programa de Olá tooexit em qualquer altura.</span><span class="sxs-lookup"><span data-stu-id="5bcd6-136">Press **Ctrl-C** tooexit hello program at any time.</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-view-telemetry](../../includes/iot-suite-raspberry-pi-kit-view-telemetry.md)]

## <a name="next-steps"></a><span data-ttu-id="5bcd6-137">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="5bcd6-137">Next steps</span></span>

<span data-ttu-id="5bcd6-138">Visite Olá [Dev Center do Azure IoT](https://azure.microsoft.com/develop/iot/) para obter mais exemplos e documentação no Azure IoT.</span><span class="sxs-lookup"><span data-stu-id="5bcd6-138">Visit hello [Azure IoT Dev Center](https://azure.microsoft.com/develop/iot/) for more samples and documentation on Azure IoT.</span></span>

[img-raspberry-output]: ./media/iot-suite-raspberry-pi-kit-c-get-started-basic/appoutput.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md
