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
# <a name="connect-your-azure-iot-edge-gateway-toohello-remote-monitoring-preconfigured-solution-and-send-telemetry-from-a-sensortag"></a><span data-ttu-id="fa799-104">Ligar o seu toohello de gateway do Azure IoT Edge solução pré-configurada de monitorização remota e enviar telemetria a partir de um SensorTag</span><span class="sxs-lookup"><span data-stu-id="fa799-104">Connect your Azure IoT Edge gateway toohello remote monitoring preconfigured solution and send telemetry from a SensorTag</span></span>

[!INCLUDE [iot-suite-gateway-kit-selector](../../includes/iot-suite-gateway-kit-selector.md)]

<span data-ttu-id="fa799-105">Este tutorial mostra como toouse Azure IoT Edge toosend relativos à temperatura e humidade dados de SensorTag dispositivo toohello monitorização remota solução pré-configurada.</span><span class="sxs-lookup"><span data-stu-id="fa799-105">This tutorial shows you how toouse Azure IoT Edge toosend temperature and humidity data from SensorTag device toohello remote monitoring preconfigured solution.</span></span> <span data-ttu-id="fa799-106">Olá SensorTag estabelece a ligação de gateway do Intel NUC toohello utilizando o Bluetooth.</span><span class="sxs-lookup"><span data-stu-id="fa799-106">hello SensorTag connects toohello Intel NUC gateway using Bluetooth.</span></span> <span data-ttu-id="fa799-107">tutorial de Olá utiliza:</span><span class="sxs-lookup"><span data-stu-id="fa799-107">hello tutorial uses:</span></span>

- <span data-ttu-id="fa799-108">Um gateway de exemplo de tooimplement IoT Edge do Azure.</span><span class="sxs-lookup"><span data-stu-id="fa799-108">Azure IoT Edge tooimplement a sample gateway.</span></span>
- <span data-ttu-id="fa799-109">Olá IoT Suite remoto solução pré-configurada de monitorização como Olá baseado na nuvem de back-end.</span><span class="sxs-lookup"><span data-stu-id="fa799-109">hello IoT Suite remote monitoring preconfigured solution as hello cloud-based back end.</span></span>

## <a name="overview"></a><span data-ttu-id="fa799-110">Descrição geral</span><span class="sxs-lookup"><span data-stu-id="fa799-110">Overview</span></span>

<span data-ttu-id="fa799-111">Neste tutorial, conclua Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="fa799-111">In this tutorial, you complete hello following steps:</span></span>

- <span data-ttu-id="fa799-112">Implemente uma instância do tooyour de solução pré-configurada Olá remoto monitorização subscrição do Azure.</span><span class="sxs-lookup"><span data-stu-id="fa799-112">Deploy an instance of hello remote monitoring preconfigured solution tooyour Azure subscription.</span></span> <span data-ttu-id="fa799-113">Este passo automaticamente implementa e configura vários serviços do Azure.</span><span class="sxs-lookup"><span data-stu-id="fa799-113">This step automatically deploys and configures multiple Azure services.</span></span>
- <span data-ttu-id="fa799-114">Configure a sua toocommunicate de dispositivo de gateway Intel NUC com o seu computador e a solução de monitorização remota Olá.</span><span class="sxs-lookup"><span data-stu-id="fa799-114">Set up your Intel NUC gateway device toocommunicate with your computer and hello remote monitoring solution.</span></span>
- <span data-ttu-id="fa799-115">Configurar a sua telemetria do Intel NUC gateway tooreceive de um dispositivo SensorTag e enviá-lo toohello dashboard de monitorização remota.</span><span class="sxs-lookup"><span data-stu-id="fa799-115">Set up your Intel NUC gateway tooreceive telemetry from a SensorTag device and send it toohello remote monitoring dashboard.</span></span>

[!INCLUDE [iot-suite-gateway-kit-prerequisites](../../includes/iot-suite-gateway-kit-prerequisites.md)]

<span data-ttu-id="fa799-116">[Texas Instruments var SensorTag][lnk-sensortag].</span><span class="sxs-lookup"><span data-stu-id="fa799-116">[Texas Instruments BLE SensorTag][lnk-sensortag].</span></span> <span data-ttu-id="fa799-117">Este tutorial obtém dados de telemetria sobre o Bluetooth do dispositivo de SensorTag Olá.</span><span class="sxs-lookup"><span data-stu-id="fa799-117">This tutorial retrieves telemetry data over Bluetooth from hello SensorTag device.</span></span>

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

> [!WARNING]
> <span data-ttu-id="fa799-118">Olá Aprovisiona de solução de monitorização remota de um conjunto de serviços do Azure na sua subscrição do Azure.</span><span class="sxs-lookup"><span data-stu-id="fa799-118">hello remote monitoring solution provisions a set of Azure services in your Azure subscription.</span></span> <span data-ttu-id="fa799-119">implementação de Olá reflete uma arquitetura de empresas reais.</span><span class="sxs-lookup"><span data-stu-id="fa799-119">hello deployment reflects a real enterprise architecture.</span></span> <span data-ttu-id="fa799-120">encargos de consumo do Azure desnecessários tooavoid, elimine a instância da solução de Olá pré-configurada em azureiotsuite.com quando tiver terminado com o mesmo.</span><span class="sxs-lookup"><span data-stu-id="fa799-120">tooavoid unnecessary Azure consumption charges, delete your instance of hello preconfigured solution at azureiotsuite.com when you have finished with it.</span></span> <span data-ttu-id="fa799-121">Se precisar de hello novamente solução pré-configurada, pode recriá-lo facilmente.</span><span class="sxs-lookup"><span data-stu-id="fa799-121">If you need hello preconfigured solution again, you can easily recreate it.</span></span> <span data-ttu-id="fa799-122">Para obter mais informações sobre a redução do consumo ao hello execuções de solução de monitorização remota, consulte [soluções para fins de demonstração de pré-configuradas de configurar o Azure IoT Suite][lnk-demo-config].</span><span class="sxs-lookup"><span data-stu-id="fa799-122">For more information about reducing consumption while hello remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span>

[!INCLUDE [iot-suite-gateway-kit-view-solution](../../includes/iot-suite-gateway-kit-view-solution.md)]

[!INCLUDE [iot-suite-gateway-kit-prepare-nuc-connectivity](../../includes/iot-suite-gateway-kit-prepare-nuc-connectivity.md)]

## <a name="configure-bluetooth-connectivity"></a><span data-ttu-id="fa799-123">Configurar a conectividade do Bluetooth</span><span class="sxs-lookup"><span data-stu-id="fa799-123">Configure Bluetooth connectivity</span></span>

<span data-ttu-id="fa799-124">Configurar o Bluetooth Olá Intel NUC tooenable Olá SensorTag dispositivo tooconnect e enviar telemetria.</span><span class="sxs-lookup"><span data-stu-id="fa799-124">Configure Bluetooth on hello Intel NUC tooenable hello SensorTag device tooconnect and send telemetry.</span></span>

### <a name="find-hello-mac-address-of-hello-sensortag"></a><span data-ttu-id="fa799-125">Localizar o endereço MAC Olá Olá SensorTag</span><span class="sxs-lookup"><span data-stu-id="fa799-125">Find hello MAC address of hello SensorTag</span></span>

1. <span data-ttu-id="fa799-126">Na shell de Olá no Olá Intel NUC, execute Olá serviço Bluetooth do comando toounblock Olá os seguintes:</span><span class="sxs-lookup"><span data-stu-id="fa799-126">In hello shell on hello Intel NUC, run hello following command toounblock hello Bluetooth service:</span></span>

    ```bash
    sudo rfkill unblock bluetooth
    ```

1. <span data-ttu-id="fa799-127">Olá executar comandos seguintes toostart Olá Bluetooth serviço Olá Intel NUC e introduza a shell de Bluetooth Olá:</span><span class="sxs-lookup"><span data-stu-id="fa799-127">Run hello following commands toostart hello Bluetooth service on hello Intel NUC and enter hello Bluetooth shell:</span></span>

    ```bash
    sudo systemctl start bluetooth
    bluetoothctl
    ```

1. <span data-ttu-id="fa799-128">Execute Olá toopower comando num controlador de Bluetooth Olá os seguintes:</span><span class="sxs-lookup"><span data-stu-id="fa799-128">Run hello following command toopower on hello Bluetooth controller:</span></span>

    ```bash
    power on
    ```

    <span data-ttu-id="fa799-129">Quando o controlador de Olá está ativado, verá uma mensagem **a alteração de energia no foi concluída com êxito**.</span><span class="sxs-lookup"><span data-stu-id="fa799-129">When hello controller is on, you see a message **Changing power on succeeded**.</span></span>

1. <span data-ttu-id="fa799-130">Execute Olá tooscan de comando para próximas dispositivos Bluetooth os seguintes:</span><span class="sxs-lookup"><span data-stu-id="fa799-130">Run hello following command tooscan for nearby Bluetooth devices:</span></span>

    ```bash
    scan on
    ```

1. <span data-ttu-id="fa799-131">Prima Olá energia botão no Olá SensorTag toomake-Detetáveis.</span><span class="sxs-lookup"><span data-stu-id="fa799-131">Press hello power button on hello SensorTag toomake it discoverable.</span></span> <span data-ttu-id="fa799-132">Olá verde LED está intermitente.</span><span class="sxs-lookup"><span data-stu-id="fa799-132">hello green LED flashes.</span></span>

1. <span data-ttu-id="fa799-133">Quando vir uma mensagem na shell de Olá desse controlador Olá detetou Olá SensorTag, anote Olá endereço MAC do dispositivo Olá.</span><span class="sxs-lookup"><span data-stu-id="fa799-133">When you see a message in hello shell that hello controller has discovered hello SensorTag, make a note of hello MAC address of hello device.</span></span> <span data-ttu-id="fa799-134">Olá endereço MAC é semelhante **A0:E6:F8:B5:F6:00**.</span><span class="sxs-lookup"><span data-stu-id="fa799-134">hello MAC address looks like **A0:E6:F8:B5:F6:00**.</span></span> <span data-ttu-id="fa799-135">Tem de endereço de MAC hello mais tarde no tutorial Olá quando configurar o gateway de Olá.</span><span class="sxs-lookup"><span data-stu-id="fa799-135">You need hello MAC address later in hello tutorial when you configure hello gateway.</span></span>

1. <span data-ttu-id="fa799-136">Execute Olá tooturn comando desativar a análise de Bluetooth os seguintes:</span><span class="sxs-lookup"><span data-stu-id="fa799-136">Run hello following command tooturn off Bluetooth scanning:</span></span>

    ```bash
    scan off
    ```

1. <span data-ttu-id="fa799-137">Execute Olá tooverify de comando que pode ligar dispositivos SensorTag de toohello os seguintes:</span><span class="sxs-lookup"><span data-stu-id="fa799-137">Run hello following command tooverify that you can connect toohello SensorTag device:</span></span>

    ```bash
    connect <SensorTag MAC address>
    ```

    <span data-ttu-id="fa799-138">Se ligar com êxito, shell Olá mostra mensagem de saudação **ligação com êxito** e imprime informações sobre Olá SensorTag do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="fa799-138">If you connect successfully, hello shell shows hello message **Connection successful** and prints information about hello SensorTag device.</span></span> <span data-ttu-id="fa799-139">Se não conseguir ligar, verifique Olá que sensortag ainda está ligado.</span><span class="sxs-lookup"><span data-stu-id="fa799-139">If you cannot connect, check hello SensorTag is still powered on.</span></span>

1. <span data-ttu-id="fa799-140">Pode agora desligar do Olá SensorTag e sair da shell de Bluetooth Olá executando Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="fa799-140">You can now disconnect from hello SensorTag and exit hello Bluetooth shell by running hello following commands:</span></span>

    ```bash
    disconnect
    exit
    ```

[!INCLUDE [iot-suite-gateway-kit-prepare-nuc-software](../../includes/iot-suite-gateway-kit-prepare-nuc-software.md)]

## <a name="build-hello-custom-iot-edge-module"></a><span data-ttu-id="fa799-141">Construir Olá módulo de limite de IoT personalizado</span><span class="sxs-lookup"><span data-stu-id="fa799-141">Build hello custom IoT Edge module</span></span>

<span data-ttu-id="fa799-142">Agora pode compilar módulo IoT Edge personalizado Olá que permite Olá gateway toosend mensagens toohello solução de monitorização remota.</span><span class="sxs-lookup"><span data-stu-id="fa799-142">You can now build hello custom IoT Edge module that enables hello gateway toosend messages toohello remote monitoring solution.</span></span> <span data-ttu-id="fa799-143">Para obter mais informações sobre como configurar um gateway e os módulos de limite de IoT, consulte [conceitos do Azure IoT Edge][lnk-gateway-concepts].</span><span class="sxs-lookup"><span data-stu-id="fa799-143">For more information about configuring a gateway and IoT Edge modules, see [Azure IoT Edge concepts][lnk-gateway-concepts].</span></span>

<span data-ttu-id="fa799-144">Transferir o código de origem Olá para módulos de limite de IoT personalizados Olá a partir do GitHub com Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="fa799-144">Download hello source code for hello custom IoT Edge modules from GitHub using hello following commands:</span></span>

```bash
cd ~
git clone https://github.com/Azure-Samples/iot-remote-monitoring-c-intel-nuc-gateway-getting-started.git
```

<span data-ttu-id="fa799-145">Crie módulo Olá personalizado IoT Edge utilizando Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="fa799-145">Build hello custom IoT Edge module using hello following commands:</span></span>

```bash
cd ~/iot-remote-monitoring-c-intel-nuc-gateway-getting-started/basic
chmod u+x build.sh
sed -i -e 's/\r$//' build.sh
./build.sh
```

<span data-ttu-id="fa799-146">script de compilação de Olá coloca o módulo de limite de IoT personalizado libsensor2remotemonitoring.so Olá na pasta de compilação de Olá.</span><span class="sxs-lookup"><span data-stu-id="fa799-146">hello build script places hello libsensor2remotemonitoring.so custom IoT Edge module in hello build folder.</span></span>

## <a name="configure-and-run-hello-iot-edge-gateway"></a><span data-ttu-id="fa799-147">Configurar e executar Olá gateway de IoT</span><span class="sxs-lookup"><span data-stu-id="fa799-147">Configure and run hello IoT Edge gateway</span></span>

<span data-ttu-id="fa799-148">Agora pode configurar Olá telemetria de toosend do gateway de IoT limite da sua tooyour de dispositivos SensorTag dashboard de monitorização remota.</span><span class="sxs-lookup"><span data-stu-id="fa799-148">You can now configure hello IoT Edge gateway toosend telemetry from your SensorTag device tooyour remote monitoring dashboard.</span></span> <span data-ttu-id="fa799-149">Para obter mais informações sobre como configurar um gateway e os módulos de limite de IoT, consulte [conceitos do Azure IoT Edge][lnk-gateway-concepts].</span><span class="sxs-lookup"><span data-stu-id="fa799-149">For more information about configuring a gateway and IoT Edge modules, see [Azure IoT Edge concepts][lnk-gateway-concepts].</span></span>

> [!TIP]
> <span data-ttu-id="fa799-150">Neste tutorial, utiliza o padrão de Olá `vi` editor de texto no Olá Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="fa799-150">In this tutorial, you use hello standard `vi` text editor on hello Intel NUC.</span></span> <span data-ttu-id="fa799-151">Se não tiver utilizado `vi` anteriormente, deve efetuar um tutorial introdutórias, tais como [Unix - Olá vi Editor Tutorial] [ lnk-vi-tutorial] toofamiliarize por si deste editor.</span><span class="sxs-lookup"><span data-stu-id="fa799-151">If you have not used `vi` before, you should complete an introductory tutorial, such as [Unix - hello vi Editor Tutorial][lnk-vi-tutorial] toofamiliarize yourself with this editor.</span></span> <span data-ttu-id="fa799-152">Em alternativa, pode instalar mais intuitivo Olá [nano](https://www.nano-editor.org/) editor utilizando o comando de Olá `smart install nano -y`.</span><span class="sxs-lookup"><span data-stu-id="fa799-152">Alternatively, you can install hello more user-friendly [nano](https://www.nano-editor.org/) editor using hello command `smart install nano -y`.</span></span>

<span data-ttu-id="fa799-153">Ficheiro de configuração de exemplo de Olá aberto em Olá **vi** editor utilizando Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="fa799-153">Open hello sample configuration file in hello **vi** editor using hello following command:</span></span>

```bash
vi ~/iot-remote-monitoring-c-intel-nuc-gateway-getting-started/basic/remote_monitoring.json
```

<span data-ttu-id="fa799-154">Localize Olá seguintes linhas na configuração de Olá para o módulo de IoTHub Olá:</span><span class="sxs-lookup"><span data-stu-id="fa799-154">Locate hello following lines in hello configuration for hello IoTHub module:</span></span>

```json
"args": {
  "IoTHubName": "<<Azure IoT Hub Name>>",
  "IoTHubSuffix": "<<Azure IoT Hub Suffix>>",
  "Transport": "http"
}
```

<span data-ttu-id="fa799-155">Substitua o marcador de posição de Olá valores com Olá informações do IoT Hub é criado e guardado no Olá iniciar deste tutorial.</span><span class="sxs-lookup"><span data-stu-id="fa799-155">Replace hello placeholder values with hello IoT Hub information you created and saved at hello start of this tutorial.</span></span> <span data-ttu-id="fa799-156">valor de Olá para IoTHubName aspeto **yourrmsolution37e08**, e o valor de Olá para IoTSuffix é normalmente **azure devices.net**.</span><span class="sxs-lookup"><span data-stu-id="fa799-156">hello value for IoTHubName looks like **yourrmsolution37e08**, and hello value for IoTSuffix is typically **azure-devices.net**.</span></span>

<span data-ttu-id="fa799-157">Localize Olá seguintes linhas na configuração de Olá para o módulo de mapeamento de Olá:</span><span class="sxs-lookup"><span data-stu-id="fa799-157">Locate hello following lines in hello configuration for hello mapping module:</span></span>

```json
args": [
  {
    "macAddress": "<<AA:BB:CC:DD:EE:FF>>",
    "deviceId": "<<Azure IoT Hub Device ID>>",
    "deviceKey": "<<Azure IoT Hub Device Key>>"
  }
]
```

<span data-ttu-id="fa799-158">Substitua Olá **macAddress** marcador Olá endereço MAC do seu SensorTag que apontou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="fa799-158">Replace hello **macAddress** placeholder with hello MAC address of your SensorTag you noted previously.</span></span> <span data-ttu-id="fa799-159">Substitua Olá **deviceID** e **deviceKey** marcadores de posição com os IDs de Olá e chaves para dispositivos Olá dois na solução de monitorização remota Olá que criou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="fa799-159">Replace hello **deviceID** and **deviceKey** placeholders with hello IDs and keys for hello two devices you created in hello remote monitoring solution previously.</span></span>

<span data-ttu-id="fa799-160">Localize Olá seguintes linhas na configuração de Olá para o módulo de SensorTag Olá:</span><span class="sxs-lookup"><span data-stu-id="fa799-160">Locate hello following lines in hello configuration for hello SensorTag module:</span></span>

```json
"args": {
  "controller_index": 0,
  "device_mac_address": "<<AA:BB:CC:DD:EE:FF>>",
  ...
}
```

<span data-ttu-id="fa799-161">Substitua Olá **dispositivo\_mac\_endereço** marcador Olá endereço MAC do seu SensorTag que apontou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="fa799-161">Replace hello **device\_mac\_address** placeholder  with hello MAC address of your SensorTag you noted previously.</span></span>

<span data-ttu-id="fa799-162">Guarde as alterações.</span><span class="sxs-lookup"><span data-stu-id="fa799-162">Save your changes.</span></span>

<span data-ttu-id="fa799-163">Pode agora executar gateway Olá utilizando Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="fa799-163">You can now run hello gateway using hello following commands:</span></span>

```bash
cd ~/iot-remote-monitoring-c-intel-nuc-gateway-getting-started/basic
/usr/share/azureiotgatewaysdk/samples/ble_gateway/ble_gateway remote_monitoring.json
```

<span data-ttu-id="fa799-164">Olá gateway de IoT é iniciado num Olá Intel NUC e envia a telemetria da Olá solução de monitorização remota SensorTag toohello:</span><span class="sxs-lookup"><span data-stu-id="fa799-164">hello IoT Edge gateway starts on hello Intel NUC and sends telemetry from hello SensorTag toohello remote monitoring solution:</span></span>

![Gateway de IoT envia a telemetria da Olá SensorTag][img-telemetry]

<span data-ttu-id="fa799-166">Prima **Ctrl-C** programa de Olá tooexit em qualquer altura.</span><span class="sxs-lookup"><span data-stu-id="fa799-166">Press **Ctrl-C** tooexit hello program at any time.</span></span>

## <a name="view-hello-telemetry"></a><span data-ttu-id="fa799-167">Telemetria de visualizações de Olá</span><span class="sxs-lookup"><span data-stu-id="fa799-167">View hello telemetry</span></span>

<span data-ttu-id="fa799-168">gateway de Olá agora está a enviar telemetria de Olá SensorTag dispositivo toohello solução de monitorização remota.</span><span class="sxs-lookup"><span data-stu-id="fa799-168">hello gateway is now sending telemetry from hello SensorTag device toohello remote monitoring solution.</span></span> <span data-ttu-id="fa799-169">Pode ver a telemetria de Olá no dashboard da solução Olá.</span><span class="sxs-lookup"><span data-stu-id="fa799-169">You can view hello telemetry on hello solution dashboard.</span></span> <span data-ttu-id="fa799-170">Também pode enviar o dispositivo de SensorTag tooyour comandos através do gateway de Olá a partir do dashboard de solução Olá.</span><span class="sxs-lookup"><span data-stu-id="fa799-170">You can also send commands tooyour SensorTag device through hello gateway from hello solution dashboard.</span></span>

- <span data-ttu-id="fa799-171">Navegue toohello dashboard da solução.</span><span class="sxs-lookup"><span data-stu-id="fa799-171">Navigate toohello solution dashboard.</span></span>
- <span data-ttu-id="fa799-172">Dispositivo Olá selecione configurada no gateway de Olá que representa Olá SensorTag no Olá **dispositivo tooView** pendente.</span><span class="sxs-lookup"><span data-stu-id="fa799-172">Select hello device you configured in hello gateway that represents hello SensorTag in hello **Device tooView** dropdown.</span></span>
- <span data-ttu-id="fa799-173">Apresenta a telemetria de Olá de dispositivos SensorTag de Olá no dashboard de Olá.</span><span class="sxs-lookup"><span data-stu-id="fa799-173">hello telemetry from hello SensorTag device displays on hello dashboard.</span></span>

![Apresentar a telemetria de dispositivos SensorTag de Olá][img-telemetry-display]

> [!WARNING]
> <span data-ttu-id="fa799-175">Se deixar Olá em execução na sua conta do Azure de solução de monitorização remota, é-lhe faturado por período de tempo de Olá que é executada.</span><span class="sxs-lookup"><span data-stu-id="fa799-175">If you leave hello remote monitoring solution running in your Azure account, you are billed for hello time it runs.</span></span> <span data-ttu-id="fa799-176">Para obter mais informações sobre a redução do consumo ao hello execuções de solução de monitorização remota, consulte [soluções para fins de demonstração de pré-configuradas de configurar o Azure IoT Suite][lnk-demo-config].</span><span class="sxs-lookup"><span data-stu-id="fa799-176">For more information about reducing consumption while hello remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span> <span data-ttu-id="fa799-177">Elimine a solução pré-configurada de Olá da sua conta do Azure quando tiver concluído a utilizá-la.</span><span class="sxs-lookup"><span data-stu-id="fa799-177">Delete hello preconfigured solution from your Azure account when you have finished using it.</span></span>


## <a name="next-steps"></a><span data-ttu-id="fa799-178">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="fa799-178">Next steps</span></span>

<span data-ttu-id="fa799-179">Visite Olá [Dev Center do Azure IoT](https://azure.microsoft.com/develop/iot/) para obter mais exemplos e documentação no Azure IoT.</span><span class="sxs-lookup"><span data-stu-id="fa799-179">Visit hello [Azure IoT Dev Center](https://azure.microsoft.com/develop/iot/) for more samples and documentation on Azure IoT.</span></span>

[img-telemetry]: ./media/iot-suite-gateway-kit-get-started-sensortag/appoutput.png


[img-telemetry-display]: ./media/iot-suite-gateway-kit-get-started-sensortag/telemetry.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md
[lnk-vi-tutorial]: http://www.tutorialspoint.com/unix/unix-vi-editor.htm
[lnk-sensortag]: http://www.ti.com/ww/en/wireless_connectivity/sensortag/
[lnk-gateway-concepts]: https://docs.microsoft.com/azure/iot-hub/iot-hub-linux-iot-edge-get-started