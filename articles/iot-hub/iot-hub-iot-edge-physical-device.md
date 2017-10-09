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
# <a name="use-azure-iot-edge-on-a-raspberry-pi-tooforward-device-to-cloud-messages-tooiot-hub"></a><span data-ttu-id="d7bd3-104">Utilizar o Azure IoT Edge no tooIoT de mensagens do dispositivo para nuvem tooforward Raspberry Pi Hub</span><span class="sxs-lookup"><span data-stu-id="d7bd3-104">Use Azure IoT Edge on a Raspberry Pi tooforward device-to-cloud messages tooIoT Hub</span></span>

<span data-ttu-id="d7bd3-105">Estas instruções de Olá [exemplo de baixa energia Bluetooth] [ lnk-ble-samplecode] mostra-lhe como toouse [Azure IoT Edge] [ lnk-sdk] para:</span><span class="sxs-lookup"><span data-stu-id="d7bd3-105">This walkthrough of hello [Bluetooth low energy sample][lnk-ble-samplecode] shows you how toouse [Azure IoT Edge][lnk-sdk] to:</span></span>

* <span data-ttu-id="d7bd3-106">Reencaminhe tooIoT de telemetria do dispositivo para nuvem Hub a partir de um dispositivo físico.</span><span class="sxs-lookup"><span data-stu-id="d7bd3-106">Forward device-to-cloud telemetry tooIoT Hub from a physical device.</span></span>
* <span data-ttu-id="d7bd3-107">Comandos de rota do dispositivo físico do IoT Hub tooa.</span><span class="sxs-lookup"><span data-stu-id="d7bd3-107">Route commands from IoT Hub tooa physical device.</span></span>

<span data-ttu-id="d7bd3-108">Estas instruções abrangem:</span><span class="sxs-lookup"><span data-stu-id="d7bd3-108">This walkthrough covers:</span></span>

* <span data-ttu-id="d7bd3-109">**Arquitetura**: as informações da arquitetura importantes sobre Olá Bluetooth baixa energia de amostra.</span><span class="sxs-lookup"><span data-stu-id="d7bd3-109">**Architecture**: important architectural information about hello Bluetooth low energy sample.</span></span>
* <span data-ttu-id="d7bd3-110">**Compilar e executar**: Olá passos necessários toobuild e exemplo de Olá execução.</span><span class="sxs-lookup"><span data-stu-id="d7bd3-110">**Build and run**: hello steps required toobuild and run hello sample.</span></span>

## <a name="architecture"></a><span data-ttu-id="d7bd3-111">Arquitetura</span><span class="sxs-lookup"><span data-stu-id="d7bd3-111">Architecture</span></span>

<span data-ttu-id="d7bd3-112">instruções de Olá mostram como toobuild e executar um gateway de IoT em 3 de Pi um Raspberry que é executado Raspbian Linux.</span><span class="sxs-lookup"><span data-stu-id="d7bd3-112">hello walkthrough shows you how toobuild and run an IoT Edge gateway on a Raspberry Pi 3 that runs Raspbian Linux.</span></span> <span data-ttu-id="d7bd3-113">gateway de Olá é criada com o limite de IoT.</span><span class="sxs-lookup"><span data-stu-id="d7bd3-113">hello gateway is built using IoT Edge.</span></span> <span data-ttu-id="d7bd3-114">exemplo de Olá utiliza um Texas Instruments SensorTag Bluetooth baixa energia (var) dispositivo toocollect temperatura de dados.</span><span class="sxs-lookup"><span data-stu-id="d7bd3-114">hello sample uses a Texas Instruments SensorTag Bluetooth Low Energy (BLE) device toocollect temperature data.</span></span>

<span data-ttu-id="d7bd3-115">Quando executa Olá gateway de IoT-lo:</span><span class="sxs-lookup"><span data-stu-id="d7bd3-115">When you run hello IoT Edge gateway it:</span></span>

* <span data-ttu-id="d7bd3-116">Estabelece ligação tooa SensorTag dispositivo através do protocolo de Bluetooth baixa energia (var) Olá.</span><span class="sxs-lookup"><span data-stu-id="d7bd3-116">Connects tooa SensorTag device using hello Bluetooth Low Energy (BLE) protocol.</span></span>
* <span data-ttu-id="d7bd3-117">Estabelece ligação tooIoT Hub através do protocolo de Olá HTTP.</span><span class="sxs-lookup"><span data-stu-id="d7bd3-117">Connects tooIoT Hub using hello HTTP protocol.</span></span>
* <span data-ttu-id="d7bd3-118">Reencaminha a telemetria de Olá SensorTag dispositivo tooIoT Hub.</span><span class="sxs-lookup"><span data-stu-id="d7bd3-118">Forwards telemetry from hello SensorTag device tooIoT Hub.</span></span>
* <span data-ttu-id="d7bd3-119">Comandos de dispositivos do IoT Hub toohello SensorTag de rotas.</span><span class="sxs-lookup"><span data-stu-id="d7bd3-119">Routes commands from IoT Hub toohello SensorTag device.</span></span>

<span data-ttu-id="d7bd3-120">gateway de Olá contém Olá seguintes módulos de limite de IoT:</span><span class="sxs-lookup"><span data-stu-id="d7bd3-120">hello gateway contains hello following IoT Edge modules:</span></span>

* <span data-ttu-id="d7bd3-121">A *módulo var* que interaja com um var dispositivo tooreceive temperatura de dados do dispositivo de Olá e enviar comandos toohello dispositivo.</span><span class="sxs-lookup"><span data-stu-id="d7bd3-121">A *BLE module* that interfaces with a BLE device tooreceive temperature data from hello device and send commands toohello device.</span></span>
* <span data-ttu-id="d7bd3-122">A *módulo do var nuvem toodevice* que traduz mensagens JSON enviadas a partir do IoT Hub para var as instruções para Olá *módulo var*.</span><span class="sxs-lookup"><span data-stu-id="d7bd3-122">A *BLE cloud toodevice module* that translates JSON messages sent from IoT Hub into BLE instructions for hello *BLE module*.</span></span>
* <span data-ttu-id="d7bd3-123">A *módulo de registo* que regista todos os gateway mensagens tooa ficheiro local.</span><span class="sxs-lookup"><span data-stu-id="d7bd3-123">A *logger module* that logs all gateway messages tooa local file.</span></span>
* <span data-ttu-id="d7bd3-124">Um *módulo de mapeamento de identidades* que traduz entre endereços de MAC do dispositivo var e identidades de dispositivo do IoT Hub do Azure.</span><span class="sxs-lookup"><span data-stu-id="d7bd3-124">An *identity mapping module* that translates between BLE device MAC addresses and Azure IoT Hub device identities.</span></span>
* <span data-ttu-id="d7bd3-125">Um *módulo do IoT Hub* que carrega o hub IoT do telemetria dados tooan e recebe comandos de dispositivo a partir de um hub IoT.</span><span class="sxs-lookup"><span data-stu-id="d7bd3-125">An *IoT Hub module* that uploads telemetry data tooan IoT hub and receives device commands from an IoT hub.</span></span>
* <span data-ttu-id="d7bd3-126">A *módulo de impressora var* que interpreta telemetria do dispositivo de var Olá e imprime dados formatados toohello consola tooenable resolução de problemas e depuração.</span><span class="sxs-lookup"><span data-stu-id="d7bd3-126">A *BLE printer module* that interprets telemetry from hello BLE device and prints formatted data toohello console tooenable troubleshooting and debugging.</span></span>

### <a name="how-data-flows-through-hello-gateway"></a><span data-ttu-id="d7bd3-127">Como os dados de saída flui através do gateway Olá</span><span class="sxs-lookup"><span data-stu-id="d7bd3-127">How data flows through hello gateway</span></span>

<span data-ttu-id="d7bd3-128">Olá diagrama de blocos a seguir ilustra o pipeline de fluxo de dados de carregamento telemetria Olá:</span><span class="sxs-lookup"><span data-stu-id="d7bd3-128">hello following block diagram illustrates hello telemetry upload data flow pipeline:</span></span>

![Pipeline de gateway de carregamento de telemetria](media/iot-hub-iot-edge-physical-device/gateway_ble_upload_data_flow.png)

<span data-ttu-id="d7bd3-130">passos de Olá que um item de telemetria demora estiverem em deslocação de uma tooIoT de dispositivo var Hub são:</span><span class="sxs-lookup"><span data-stu-id="d7bd3-130">hello steps that an item of telemetry takes traveling from a BLE device tooIoT Hub are:</span></span>

1. <span data-ttu-id="d7bd3-131">gera uma amostra de temperatura e envia-o ao longo do módulo de var toohello Bluetooth no gateway de Olá de Olá var dispositivos.</span><span class="sxs-lookup"><span data-stu-id="d7bd3-131">hello BLE device generates a temperature sample and sends it over Bluetooth toohello BLE module in hello gateway.</span></span>
1. <span data-ttu-id="d7bd3-132">módulo de var Olá recebe exemplo Olá e publica-broker toohello juntamente com o endereço de MAC Olá do dispositivo Olá.</span><span class="sxs-lookup"><span data-stu-id="d7bd3-132">hello BLE module receives hello sample and publishes it toohello broker along with hello MAC address of hello device.</span></span>
1. <span data-ttu-id="d7bd3-133">módulo de mapeamento de identidades Olá escolherá esta mensagem e utiliza um Olá tootranslate de tabela interna endereço MAC do dispositivo Olá para uma identidade de dispositivo IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="d7bd3-133">hello identity mapping module picks up this message and uses an internal table tootranslate hello MAC address of hello device into an IoT Hub device identity.</span></span> <span data-ttu-id="d7bd3-134">Uma identidade de dispositivo do IoT Hub é composta por um ID de dispositivo e a chave do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="d7bd3-134">An IoT Hub device identity consists of a device ID and device key.</span></span>
1. <span data-ttu-id="d7bd3-135">módulo de mapeamento de identidades Olá publica uma nova mensagem que contém dados de exemplo de temperatura Olá, endereço de MAC Olá de dispositivo Olá, ID de dispositivo Olá e chave do dispositivo Olá.</span><span class="sxs-lookup"><span data-stu-id="d7bd3-135">hello identity mapping module publishes a new message that contains hello temperature sample data, hello MAC address of hello device, hello device ID, and hello device key.</span></span>
1. <span data-ttu-id="d7bd3-136">Olá módulo do IoT Hub recebe esta mensagem nova (gerada pelo módulo de mapeamento de identidades de Olá) e publica-tooIoT Hub.</span><span class="sxs-lookup"><span data-stu-id="d7bd3-136">hello IoT Hub module receives this new message (generated by hello identity mapping module) and publishes it tooIoT Hub.</span></span>
1. <span data-ttu-id="d7bd3-137">módulo de registo Olá regista todas as mensagens de ficheiro do Olá mediador tooa local.</span><span class="sxs-lookup"><span data-stu-id="d7bd3-137">hello logger module logs all messages from hello broker tooa local file.</span></span>

<span data-ttu-id="d7bd3-138">Olá diagrama de blocos a seguir ilustra o pipeline de fluxo de dados de comando dispositivo Olá:</span><span class="sxs-lookup"><span data-stu-id="d7bd3-138">hello following block diagram illustrates hello device command data flow pipeline:</span></span>

![Pipeline de gateway do comando de dispositivo](media/iot-hub-iot-edge-physical-device/gateway_ble_command_data_flow.png)

1. <span data-ttu-id="d7bd3-140">Olá IoT Hub módulo consulta periodicamente se existem Olá IoT hub para novas mensagens de comando.</span><span class="sxs-lookup"><span data-stu-id="d7bd3-140">hello IoT Hub module periodically polls hello IoT hub for new command messages.</span></span>
1. <span data-ttu-id="d7bd3-141">Quando Olá módulo do IoT Hub recebe uma nova mensagem de comando, publica-toohello mediador.</span><span class="sxs-lookup"><span data-stu-id="d7bd3-141">When hello IoT Hub module receives a new command message, it publishes it toohello broker.</span></span>
1. <span data-ttu-id="d7bd3-142">módulo de mapeamento de identidades Olá escolherá a mensagem de comando de saudação e utiliza um Olá tootranslate de tabela interna dispositivos do IoT Hub dispositivo ID tooa endereço MAC.</span><span class="sxs-lookup"><span data-stu-id="d7bd3-142">hello identity mapping module picks up hello command message and uses an internal table tootranslate hello IoT Hub device ID tooa device MAC address.</span></span> <span data-ttu-id="d7bd3-143">Em seguida, publica uma nova mensagem, que inclui o endereço de MAC Olá do dispositivo-alvo Olá no mapa de propriedades de Olá de mensagem de saudação.</span><span class="sxs-lookup"><span data-stu-id="d7bd3-143">It then publishes a new message that includes hello MAC address of hello target device in hello properties map of hello message.</span></span>
1. <span data-ttu-id="d7bd3-144">módulo de var nuvem para o dispositivo de Olá escolherá esta mensagem e converte-lo em instruções var adequada Olá para o módulo de var Olá.</span><span class="sxs-lookup"><span data-stu-id="d7bd3-144">hello BLE Cloud-to-Device module picks up this message and translates it into hello proper BLE instruction for hello BLE module.</span></span> <span data-ttu-id="d7bd3-145">Em seguida, publica uma nova mensagem.</span><span class="sxs-lookup"><span data-stu-id="d7bd3-145">It then publishes a new message.</span></span>
1. <span data-ttu-id="d7bd3-146">módulo de var Olá escolherá esta mensagem e executa a instrução de e/s de Olá através da comunique com Olá var.</span><span class="sxs-lookup"><span data-stu-id="d7bd3-146">hello BLE module picks up this message and executes hello I/O instruction by communicating with hello BLE device.</span></span>
1. <span data-ttu-id="d7bd3-147">módulo de registo Olá regista todas as mensagens do ficheiro de disco Olá mediador tooa.</span><span class="sxs-lookup"><span data-stu-id="d7bd3-147">hello logger module logs all messages from hello broker tooa disk file.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d7bd3-148">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="d7bd3-148">Prerequisites</span></span>

<span data-ttu-id="d7bd3-149">toocomplete neste tutorial, necessita de uma subscrição do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d7bd3-149">toocomplete this tutorial, you need an active Azure subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="d7bd3-150">Se não tiver uma conta, pode criar uma de avaliação gratuita em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="d7bd3-150">If you don’t have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="d7bd3-151">Para obter mais detalhes, consulte [Azure Free Trial (Avaliação Gratuita do Azure)][lnk-free-trial].</span><span class="sxs-lookup"><span data-stu-id="d7bd3-151">For details, see [Azure Free Trial][lnk-free-trial].</span></span>

<span data-ttu-id="d7bd3-152">Precisa de cliente SSH no seu tooenable de ambiente de trabalho de máquina tooremotely acesso Olá comando linha no Olá Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="d7bd3-152">You need SSH client on your desktop machine tooenable you tooremotely access hello command line on hello Raspberry Pi.</span></span>

- <span data-ttu-id="d7bd3-153">Windows não inclui um cliente SSH.</span><span class="sxs-lookup"><span data-stu-id="d7bd3-153">Windows does not include an SSH client.</span></span> <span data-ttu-id="d7bd3-154">Recomendamos que utilize [PuTTY](http://www.putty.org/).</span><span class="sxs-lookup"><span data-stu-id="d7bd3-154">We recommend using [PuTTY](http://www.putty.org/).</span></span>
- <span data-ttu-id="d7bd3-155">A maioria das distribuições de Linux e Mac OS incluem SSH utilitário de linha de comandos Olá.</span><span class="sxs-lookup"><span data-stu-id="d7bd3-155">Most Linux distributions and Mac OS include hello command-line SSH utility.</span></span> <span data-ttu-id="d7bd3-156">Para obter mais informações, consulte [SSH utilizando o Linux ou Mac OS](https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md).</span><span class="sxs-lookup"><span data-stu-id="d7bd3-156">For more information, see [SSH Using Linux or Mac OS](https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md).</span></span>

## <a name="prepare-your-hardware"></a><span data-ttu-id="d7bd3-157">Prepare o hardware</span><span class="sxs-lookup"><span data-stu-id="d7bd3-157">Prepare your hardware</span></span>

<span data-ttu-id="d7bd3-158">Este tutorial parte do princípio de que está a utilizar um [Texas Instruments SensorTag](http://www.ti.com/ww/en/wireless_connectivity/sensortag2015/index.html) dispositivo ligado tooa Raspberry Pi 3 Raspbian a executar.</span><span class="sxs-lookup"><span data-stu-id="d7bd3-158">This tutorial assumes you are using a [Texas Instruments SensorTag](http://www.ti.com/ww/en/wireless_connectivity/sensortag2015/index.html) device connected tooa Raspberry Pi 3 running Raspbian.</span></span>

### <a name="install-raspbian"></a><span data-ttu-id="d7bd3-159">Instalar Raspbian</span><span class="sxs-lookup"><span data-stu-id="d7bd3-159">Install Raspbian</span></span>

<span data-ttu-id="d7bd3-160">Pode utilizar qualquer uma das seguintes opções tooinstall Raspbian no seu dispositivo Raspberry Pi 3 de Olá.</span><span class="sxs-lookup"><span data-stu-id="d7bd3-160">You can use either of hello following options tooinstall Raspbian on your Raspberry Pi 3 device.</span></span>

* <span data-ttu-id="d7bd3-161">versão mais recente de Olá tooinstall de Raspbian, utilize Olá [NOOBS] [ lnk-noobs] interface gráfica do utilizador.</span><span class="sxs-lookup"><span data-stu-id="d7bd3-161">tooinstall hello latest version of Raspbian, use hello [NOOBS][lnk-noobs] graphical user interface.</span></span>
* <span data-ttu-id="d7bd3-162">Manualmente [transferir] [ lnk-raspbian] e escrever Olá imagem mais recente do cartão de Olá Raspbian sistema operativo tooan SD.</span><span class="sxs-lookup"><span data-stu-id="d7bd3-162">Manually [download][lnk-raspbian] and write hello latest image of hello Raspbian operating system tooan SD card.</span></span>

### <a name="sign-in-and-access-hello-terminal"></a><span data-ttu-id="d7bd3-163">A iniciar sessão e aceder ao terminal Olá</span><span class="sxs-lookup"><span data-stu-id="d7bd3-163">Sign in and access hello terminal</span></span>

<span data-ttu-id="d7bd3-164">Tem duas opções tooaccess num ambiente de terminal no seu Raspberry Pi:</span><span class="sxs-lookup"><span data-stu-id="d7bd3-164">You have two options tooaccess a terminal environment on your Raspberry Pi:</span></span>

* <span data-ttu-id="d7bd3-165">Se tiver um teclado e monitorizar tooyour ligado Raspberry Pi, pode utilizar Olá Raspbian GUI tooaccess uma janela de terminal.</span><span class="sxs-lookup"><span data-stu-id="d7bd3-165">If you have a keyboard and monitor connected tooyour Raspberry Pi, you can use hello Raspbian GUI tooaccess a terminal window.</span></span>

* <span data-ttu-id="d7bd3-166">Linha de comandos de Olá de acesso na sua Raspberry Pi utilizando SSH a partir do seu computador de secretária.</span><span class="sxs-lookup"><span data-stu-id="d7bd3-166">Access hello command line on your Raspberry Pi using SSH from your desktop machine.</span></span>

#### <a name="use-a-terminal-window-in-hello-gui"></a><span data-ttu-id="d7bd3-167">Utilizar uma janela de terminal no Olá GUI</span><span class="sxs-lookup"><span data-stu-id="d7bd3-167">Use a terminal Window in hello GUI</span></span>

<span data-ttu-id="d7bd3-168">credenciais predefinidas Olá Raspbian são username **pi** e palavra-passe **raspberry**.</span><span class="sxs-lookup"><span data-stu-id="d7bd3-168">hello default credentials for Raspbian are username **pi** and password **raspberry**.</span></span> <span data-ttu-id="d7bd3-169">Na barra de tarefas de Olá no Olá GUI, pode iniciar Olá **Terminal** utilitário com ícone de Olá que se assemelha um monitor.</span><span class="sxs-lookup"><span data-stu-id="d7bd3-169">In hello task bar in hello GUI, you can launch hello **Terminal** utility using hello icon that looks like a monitor.</span></span>

#### <a name="sign-in-with-ssh"></a><span data-ttu-id="d7bd3-170">Inicie sessão com SSH</span><span class="sxs-lookup"><span data-stu-id="d7bd3-170">Sign in with SSH</span></span>

<span data-ttu-id="d7bd3-171">Pode utilizar o SSH para acesso da linha de comandos tooyour Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="d7bd3-171">You can use SSH for command-line access tooyour Raspberry Pi.</span></span> <span data-ttu-id="d7bd3-172">artigo de Olá [SSH (Secure Shell)] [ lnk-pi-ssh] descreve como tooconfigure SSH no seu Raspberry Pi e como tooconnect de [Windows] [ lnk-ssh-windows] ou [SO Linux & Mac][lnk-ssh-linux].</span><span class="sxs-lookup"><span data-stu-id="d7bd3-172">hello article [SSH (Secure Shell)][lnk-pi-ssh] describes how tooconfigure SSH on your Raspberry Pi, and how tooconnect from [Windows][lnk-ssh-windows] or [Linux & Mac OS][lnk-ssh-linux].</span></span>

<span data-ttu-id="d7bd3-173">Inicie sessão com o nome de utilizador **pi** e palavra-passe **raspberry**.</span><span class="sxs-lookup"><span data-stu-id="d7bd3-173">Sign in with username **pi** and password **raspberry**.</span></span>

### <a name="install-bluez-537"></a><span data-ttu-id="d7bd3-174">Instalar BlueZ 5.37</span><span class="sxs-lookup"><span data-stu-id="d7bd3-174">Install BlueZ 5.37</span></span>

<span data-ttu-id="d7bd3-175">módulos de var Olá falar toohello Bluetooth hardware através de pilha de BlueZ Olá.</span><span class="sxs-lookup"><span data-stu-id="d7bd3-175">hello BLE modules talk toohello Bluetooth hardware via hello BlueZ stack.</span></span> <span data-ttu-id="d7bd3-176">Precisa de versão 5.37 de BlueZ para Olá módulos toowork corretamente.</span><span class="sxs-lookup"><span data-stu-id="d7bd3-176">You need version 5.37 of BlueZ for hello modules toowork correctly.</span></span> <span data-ttu-id="d7bd3-177">Estas instruções Certifique-se de que está instalada a versão correta do Olá do BlueZ.</span><span class="sxs-lookup"><span data-stu-id="d7bd3-177">These instructions make sure hello correct version of BlueZ is installed.</span></span>

1. <span data-ttu-id="d7bd3-178">Pare o daemon de bluetooth Olá atual:</span><span class="sxs-lookup"><span data-stu-id="d7bd3-178">Stop hello current bluetooth daemon:</span></span>

    ```sh
    sudo systemctl stop bluetooth
    ```

1. <span data-ttu-id="d7bd3-179">Instale as dependências de BlueZ Olá:</span><span class="sxs-lookup"><span data-stu-id="d7bd3-179">Install hello BlueZ dependencies:</span></span>

    ```sh
    sudo apt-get update
    sudo apt-get install bluetooth bluez-tools build-essential autoconf glib2.0 libglib2.0-dev libdbus-1-dev libudev-dev libical-dev libreadline-dev
    ```

1. <span data-ttu-id="d7bd3-180">Transferir o código de origem do Olá BlueZ bluez.org:</span><span class="sxs-lookup"><span data-stu-id="d7bd3-180">Download hello BlueZ source code from bluez.org:</span></span>

    ```sh
    wget http://www.kernel.org/pub/linux/bluetooth/bluez-5.37.tar.xz
    ```

1. <span data-ttu-id="d7bd3-181">Deszipe o código de origem Olá:</span><span class="sxs-lookup"><span data-stu-id="d7bd3-181">Unzip hello source code:</span></span>

    ```sh
    tar -xvf bluez-5.37.tar.xz
    ```

1. <span data-ttu-id="d7bd3-182">Alterar pasta do toohello recém-criado diretórios:</span><span class="sxs-lookup"><span data-stu-id="d7bd3-182">Change directories toohello newly created folder:</span></span>

    ```sh
    cd bluez-5.37
    ```

1. <span data-ttu-id="d7bd3-183">Configure Olá BlueZ código toobe incorporada:</span><span class="sxs-lookup"><span data-stu-id="d7bd3-183">Configure hello BlueZ code toobe built:</span></span>

    ```sh
    ./configure --disable-udev --disable-systemd --enable-experimental
    ```

1. <span data-ttu-id="d7bd3-184">Crie BlueZ:</span><span class="sxs-lookup"><span data-stu-id="d7bd3-184">Build BlueZ:</span></span>

    ```sh
    make
    ```

1. <span data-ttu-id="d7bd3-185">Instalar BlueZ depois de estar concluído criação:</span><span class="sxs-lookup"><span data-stu-id="d7bd3-185">Install BlueZ once it is done building:</span></span>

    ```sh
    sudo make install
    ```

1. <span data-ttu-id="d7bd3-186">Alterar a configuração do serviço systemd para bluetooth para pontos de nova bluetooth daemon toohello no ficheiro de Olá `/lib/systemd/system/bluetooth.service`.</span><span class="sxs-lookup"><span data-stu-id="d7bd3-186">Change systemd service configuration for bluetooth so it points toohello new bluetooth daemon in hello file `/lib/systemd/system/bluetooth.service`.</span></span> <span data-ttu-id="d7bd3-187">Substitua a linha de 'ExecStart' Olá com Olá seguinte texto:</span><span class="sxs-lookup"><span data-stu-id="d7bd3-187">Replace hello 'ExecStart' line with hello following text:</span></span>

    ```conf
    ExecStart=/usr/local/libexec/bluetooth/bluetoothd -E
    ```

### <a name="enable-connectivity-toohello-sensortag-device-from-your-raspberry-pi-3-device"></a><span data-ttu-id="d7bd3-188">Ativar dispositivos SensorTag de toohello de conectividade do seu dispositivo Raspberry Pi 3</span><span class="sxs-lookup"><span data-stu-id="d7bd3-188">Enable connectivity toohello SensorTag device from your Raspberry Pi 3 device</span></span>

<span data-ttu-id="d7bd3-189">Antes de exemplo de Olá em execução, terá de tooverify que sua 3 de Pi Raspberry podem ligar toohello SensorTag dispositivo.</span><span class="sxs-lookup"><span data-stu-id="d7bd3-189">Before running hello sample, you need tooverify that your Raspberry Pi 3 can connect toohello SensorTag device.</span></span>

1. <span data-ttu-id="d7bd3-190">Certifique-se Olá `rfkill` utilitário está instalado:</span><span class="sxs-lookup"><span data-stu-id="d7bd3-190">Ensure hello `rfkill` utility is installed:</span></span>

    ```sh
    sudo apt-get install rfkill
    ```

1. <span data-ttu-id="d7bd3-191">Desbloquear bluetooth no Olá Raspberry Pi 3 e verificar se o número de versão Olá é **5.37**:</span><span class="sxs-lookup"><span data-stu-id="d7bd3-191">Unblock bluetooth on hello Raspberry Pi 3 and check that hello version number is **5.37**:</span></span>

    ```sh
    sudo rfkill unblock bluetooth
    bluetoothctl --version
    ```

1. <span data-ttu-id="d7bd3-192">shell do tooenter Olá bluetooth interativa, iniciar o serviço de bluetooth Olá e executar Olá **bluetoothctl** comando:</span><span class="sxs-lookup"><span data-stu-id="d7bd3-192">tooenter hello interactive bluetooth shell, start hello bluetooth service and execute hello **bluetoothctl** command :</span></span>

    ```sh
    sudo systemctl start bluetooth
    bluetoothctl
    ```

1. <span data-ttu-id="d7bd3-193">Introduza o comando de Olá **ativação** toopower se o controlador de bluetooth Olá.</span><span class="sxs-lookup"><span data-stu-id="d7bd3-193">Enter hello command **power on** toopower up hello bluetooth controller.</span></span> <span data-ttu-id="d7bd3-194">comando de Olá devolve seguinte de toohello semelhante de saída:</span><span class="sxs-lookup"><span data-stu-id="d7bd3-194">hello command returns output similar toohello following:</span></span>

    ```sh
    [NEW] Controller 98:4F:EE:04:1F:DF C3 raspberrypi [default]
    ```

1. <span data-ttu-id="d7bd3-195">Na shell de bluetooth interativa Olá, introduza o comando de Olá **verificar em** tooscan para dispositivos bluetooth.</span><span class="sxs-lookup"><span data-stu-id="d7bd3-195">In hello interactive bluetooth shell, enter hello command **scan on** tooscan for bluetooth devices.</span></span> <span data-ttu-id="d7bd3-196">comando de Olá devolve seguinte de toohello semelhante de saída:</span><span class="sxs-lookup"><span data-stu-id="d7bd3-196">hello command returns output similar toohello following:</span></span>

    ```sh
    Discovery started
    [CHG] Controller 98:4F:EE:04:1F:DF Discovering: yes
    ```

1. <span data-ttu-id="d7bd3-197">Certifique-dispositivos SensorTag de Olá detetável, premindo Olá pequeno botão (Olá deve flash LED verde).</span><span class="sxs-lookup"><span data-stu-id="d7bd3-197">Make hello SensorTag device discoverable by pressing hello small button (hello green LED should flash).</span></span> <span data-ttu-id="d7bd3-198">Olá Raspberry Pi 3 deve detetar dispositivos de SensorTag Olá:</span><span class="sxs-lookup"><span data-stu-id="d7bd3-198">hello Raspberry Pi 3 should discover hello SensorTag device:</span></span>

    ```sh
    [NEW] Device A0:E6:F8:B5:F6:00 CC2650 SensorTag
    [CHG] Device A0:E6:F8:B5:F6:00 TxPower: 0
    [CHG] Device A0:E6:F8:B5:F6:00 RSSI: -43
    ```

    <span data-ttu-id="d7bd3-199">Neste exemplo, pode ver essa Olá endereço MAC de Olá SensorTag o dispositivo está **A0:E6:F8:B5:F6:00**.</span><span class="sxs-lookup"><span data-stu-id="d7bd3-199">In this example, you can see that hello MAC address of hello SensorTag device is **A0:E6:F8:B5:F6:00**.</span></span>

1. <span data-ttu-id="d7bd3-200">Desativar a análise introduzindo Olá **analisar desativar** comando:</span><span class="sxs-lookup"><span data-stu-id="d7bd3-200">Turn off scanning by entering hello **scan off** command:</span></span>

    ```sh
    [CHG] Controller 98:4F:EE:04:1F:DF Discovering: no
    Discovery stopped
    ```

1. <span data-ttu-id="d7bd3-201">Ligar tooyour SensorTag dispositivo utilizando o seu endereço MAC introduzindo **ligar \<endereço MAC\>**.</span><span class="sxs-lookup"><span data-stu-id="d7bd3-201">Connect tooyour SensorTag device using its MAC address by entering **connect \<MAC address\>**.</span></span> <span data-ttu-id="d7bd3-202">é abreviada Olá saída de exemplo a seguir para efeitos de clareza:</span><span class="sxs-lookup"><span data-stu-id="d7bd3-202">hello following sample output is abbreviated for clarity:</span></span>

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

    > <span data-ttu-id="d7bd3-203">Pode listar as características de GATT Olá do dispositivo Olá novamente utilizando Olá **lista atributos** comando.</span><span class="sxs-lookup"><span data-stu-id="d7bd3-203">You can list hello GATT characteristics of hello device again using hello **list-attributes** command.</span></span>

1. <span data-ttu-id="d7bd3-204">Pode agora desligar do dispositivo Olá utilizando Olá **desligar** comando e, em seguida, a sair da shell de bluetooth Olá utilizando Olá **sair** comando:</span><span class="sxs-lookup"><span data-stu-id="d7bd3-204">You can now disconnect from hello device using hello **disconnect** command and then exit from hello bluetooth shell using hello **quit** command:</span></span>

    ```sh
    Attempting toodisconnect from A0:E6:F8:B5:F6:00
    Successful disconnected
    [CHG] Device A0:E6:F8:B5:F6:00 Connected: no
    ```

<span data-ttu-id="d7bd3-205">Agora, está exemplo de limite de IoT var toorun pronto Olá no seu 3 de Pi Raspberry.</span><span class="sxs-lookup"><span data-stu-id="d7bd3-205">You're now ready toorun hello BLE IoT Edge sample on your Raspberry Pi 3.</span></span>

## <a name="run-hello-iot-edge-ble-sample"></a><span data-ttu-id="d7bd3-206">Executar Olá IoT Edge var exemplo</span><span class="sxs-lookup"><span data-stu-id="d7bd3-206">Run hello IoT Edge BLE sample</span></span>

<span data-ttu-id="d7bd3-207">exemplo de IoT Edge var do toorun Olá, terá de tarefas de três toocomplete:</span><span class="sxs-lookup"><span data-stu-id="d7bd3-207">toorun hello IoT Edge BLE sample, you need toocomplete three tasks:</span></span>

* <span data-ttu-id="d7bd3-208">Configure dois dispositivos de exemplo no seu IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="d7bd3-208">Configure two sample devices in your IoT Hub.</span></span>
* <span data-ttu-id="d7bd3-209">Crie IoT Edge no seu dispositivo Raspberry Pi 3.</span><span class="sxs-lookup"><span data-stu-id="d7bd3-209">Build IoT Edge on your Raspberry Pi 3 device.</span></span>
* <span data-ttu-id="d7bd3-210">Configure e execute o exemplo de var Olá no seu dispositivo Raspberry Pi 3.</span><span class="sxs-lookup"><span data-stu-id="d7bd3-210">Configure and run hello BLE sample on your Raspberry Pi 3 device.</span></span>

<span data-ttu-id="d7bd3-211">Momento Olá de escrita, limite de IoT suporta apenas módulos var gateways em execução no Linux.</span><span class="sxs-lookup"><span data-stu-id="d7bd3-211">At hello time of writing, IoT Edge only supports BLE modules in gateways running on Linux.</span></span>

### <a name="configure-two-sample-devices-in-your-iot-hub"></a><span data-ttu-id="d7bd3-212">Configurar dois dispositivos de exemplo no seu IoT Hub</span><span class="sxs-lookup"><span data-stu-id="d7bd3-212">Configure two sample devices in your IoT Hub</span></span>

* <span data-ttu-id="d7bd3-213">[Criar um hub IoT] [ lnk-create-hub] na sua subscrição do Azure, terá de nome de Olá do seu hub toocomplete estas instruções.</span><span class="sxs-lookup"><span data-stu-id="d7bd3-213">[Create an IoT hub][lnk-create-hub] in your Azure subscription, you need hello name of your hub toocomplete this walkthrough.</span></span> <span data-ttu-id="d7bd3-214">Se não tiver uma conta, pode criar uma [conta gratuita][lnk-free-trial] em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="d7bd3-214">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>
* <span data-ttu-id="d7bd3-215">Adicionar um dispositivo designado **SensorTag_01** tooyour IoT hub e tome nota da respetiva chave id e o dispositivo.</span><span class="sxs-lookup"><span data-stu-id="d7bd3-215">Add one device called **SensorTag_01** tooyour IoT hub and make a note of its id and device key.</span></span> <span data-ttu-id="d7bd3-216">Pode utilizar Olá [Explorador de dispositivo ou no Explorador do iothub] [ lnk-explorer-tools] ferramentas tooadd este dispositivo toohello IoT hub que criou no passo anterior Olá e tooretrieve respetiva chave.</span><span class="sxs-lookup"><span data-stu-id="d7bd3-216">You can use hello [device explorer or iothub-explorer][lnk-explorer-tools] tools tooadd this device toohello IoT hub you created in hello previous step and tooretrieve its key.</span></span> <span data-ttu-id="d7bd3-217">Mapear este dispositivo do dispositivo toohello SensorTag quando configurar o gateway de Olá.</span><span class="sxs-lookup"><span data-stu-id="d7bd3-217">You map this device toohello SensorTag device when you configure hello gateway.</span></span>

### <a name="build-azure-iot-edge-on-your-raspberry-pi-3"></a><span data-ttu-id="d7bd3-218">Criar limite de IoT do Azure no seu Raspberry Pi 3</span><span class="sxs-lookup"><span data-stu-id="d7bd3-218">Build Azure IoT Edge on your Raspberry Pi 3</span></span>

<span data-ttu-id="d7bd3-219">Instale dependências para o limite do Azure IoT:</span><span class="sxs-lookup"><span data-stu-id="d7bd3-219">Install dependencies for Azure IoT Edge:</span></span>

```sh
sudo apt-get install cmake uuid-dev curl libcurl4-openssl-dev libssl-dev
```

<span data-ttu-id="d7bd3-220">Seguinte de Olá utilize comandos tooclone IoT Edge e todos os respetivo submodules tooyour diretório raiz:</span><span class="sxs-lookup"><span data-stu-id="d7bd3-220">Use hello following commands tooclone IoT Edge and all its submodules tooyour home directory:</span></span>

```sh
cd ~
git clone https://github.com/Azure/iot-edge.git
```

<span data-ttu-id="d7bd3-221">Quando tiver uma cópia completa de Olá repositório de limite de IoT no seu 3 de Pi Raspberry, pode criá-la utilizando Olá os seguintes comandos a partir da pasta de Olá que contém Olá SDK:</span><span class="sxs-lookup"><span data-stu-id="d7bd3-221">When you have a complete copy of hello IoT Edge repository on your Raspberry Pi 3, you can build it using hello following command from hello folder that contains hello SDK:</span></span>

```sh
cd ~/iot-edge
./tools/build.sh  --disable-native-remote-modules
```

### <a name="configure-and-run-hello-ble-sample-on-your-raspberry-pi-3"></a><span data-ttu-id="d7bd3-222">Configurar e executar o exemplo de var Olá no seu 3 de Pi Raspberry</span><span class="sxs-lookup"><span data-stu-id="d7bd3-222">Configure and run hello BLE sample on your Raspberry Pi 3</span></span>

<span data-ttu-id="d7bd3-223">toobootstrap e exemplo de Olá execute, tem de configurar cada módulo de limite de IoT que participa no gateway de Olá.</span><span class="sxs-lookup"><span data-stu-id="d7bd3-223">toobootstrap and run hello sample, you must configure each IoT Edge module that participates in hello gateway.</span></span> <span data-ttu-id="d7bd3-224">Esta configuração é fornecida um ficheiro JSON e tem de configurar todos os módulos de limite de IoT participantes cinco.</span><span class="sxs-lookup"><span data-stu-id="d7bd3-224">This configuration is provided in a JSON file and you must configure all five participating IoT Edge modules.</span></span> <span data-ttu-id="d7bd3-225">Há um ficheiro JSON de exemplo no repositório de Olá chamado **gateway\_sample.json** que pode utilizar como Olá ponto para a criação do seu próprio ficheiro de configuração de partida.</span><span class="sxs-lookup"><span data-stu-id="d7bd3-225">There is a sample JSON file in hello repository called **gateway\_sample.json** that you can use as hello starting point for building your own configuration file.</span></span> <span data-ttu-id="d7bd3-226">Este ficheiro está a ser Olá **ble_gateway/samples/src** pasta na cópia local do Olá repositório de limite de IoT.</span><span class="sxs-lookup"><span data-stu-id="d7bd3-226">This file is in hello **samples/ble_gateway/src** folder in local copy of hello IoT Edge repository.</span></span>

<span data-ttu-id="d7bd3-227">Olá secções seguintes descrevem como tooedit esta configuração de ficheiros de exemplo de var Olá e partem do princípio de que Olá repositório de limite de IoT é no Olá **/home/pi/iot-edge /** pasta no seu 3 de Pi Raspberry.</span><span class="sxs-lookup"><span data-stu-id="d7bd3-227">hello following sections describe how tooedit this configuration file for hello BLE sample and assume that hello IoT Edge repository is in hello **/home/pi/iot-edge/** folder on your Raspberry Pi 3.</span></span> <span data-ttu-id="d7bd3-228">Se o repositório de Olá noutro local, ajuste caminhos Olá em conformidade.</span><span class="sxs-lookup"><span data-stu-id="d7bd3-228">If hello repository is elsewhere, adjust hello paths accordingly.</span></span>

#### <a name="logger-configuration"></a><span data-ttu-id="d7bd3-229">Configuração de registo</span><span class="sxs-lookup"><span data-stu-id="d7bd3-229">Logger configuration</span></span>

<span data-ttu-id="d7bd3-230">Partindo do princípio de repositório do gateway de Olá está localizado na Olá **/home/pi/iot-edge /** pasta, configurar o módulo de registo Olá da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="d7bd3-230">Assuming hello gateway repository is located in hello **/home/pi/iot-edge/** folder, configure hello logger module as follows:</span></span>

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

#### <a name="ble-module-configuration"></a><span data-ttu-id="d7bd3-231">Configuração do módulo var</span><span class="sxs-lookup"><span data-stu-id="d7bd3-231">BLE module configuration</span></span>

<span data-ttu-id="d7bd3-232">configuração de exemplo de Olá para o dispositivo de var Olá assume um dispositivo da Texas Instruments SensorTag.</span><span class="sxs-lookup"><span data-stu-id="d7bd3-232">hello sample configuration for hello BLE device assumes a Texas Instruments SensorTag device.</span></span> <span data-ttu-id="d7bd3-233">Qualquer dispositivo var padrão que pode funcionar como um GATT periférico deverão funcionar mas poderá ser necessário tooupdate Olá GATT uma característica das IDs e os dados.</span><span class="sxs-lookup"><span data-stu-id="d7bd3-233">Any standard BLE device that can operate as a GATT peripheral should work but you may need tooupdate hello GATT characteristic IDs and data.</span></span> <span data-ttu-id="d7bd3-234">Adicione o endereço de MAC Olá do seu dispositivo SensorTag:</span><span class="sxs-lookup"><span data-stu-id="d7bd3-234">Add hello MAC address of your SensorTag device:</span></span>

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

<span data-ttu-id="d7bd3-235">Se não estiver a utilizar um dispositivo SensorTag, reveja a documentação de Olá para sua toodetermine de dispositivo var se são necessários tooupdate Olá GATT uma característica das IDs e valores de dados.</span><span class="sxs-lookup"><span data-stu-id="d7bd3-235">If you are not using a SensorTag device, review hello documentation for your BLE device toodetermine whether you need tooupdate hello GATT characteristic IDs and data values.</span></span>

#### <a name="iot-hub-module"></a><span data-ttu-id="d7bd3-236">Módulo do IoT Hub</span><span class="sxs-lookup"><span data-stu-id="d7bd3-236">IoT Hub module</span></span>

<span data-ttu-id="d7bd3-237">Adicione Olá nome do seu IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="d7bd3-237">Add hello name of your IoT Hub.</span></span> <span data-ttu-id="d7bd3-238">o valor de sufixo de Olá é normalmente **azure devices.net**:</span><span class="sxs-lookup"><span data-stu-id="d7bd3-238">hello suffix value is typically **azure-devices.net**:</span></span>

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

#### <a name="identity-mapping-module-configuration"></a><span data-ttu-id="d7bd3-239">Configuração do módulo de mapeamento de identidades</span><span class="sxs-lookup"><span data-stu-id="d7bd3-239">Identity mapping module configuration</span></span>

<span data-ttu-id="d7bd3-240">Adicione o endereço de MAC Olá dos seus dispositivos SensorTag e ID de dispositivo Olá e chave de Olá **SensorTag_01** dispositivo adicionado tooyour IoT Hub:</span><span class="sxs-lookup"><span data-stu-id="d7bd3-240">Add hello MAC address of your SensorTag device and hello device ID and key of hello **SensorTag_01** device you added tooyour IoT Hub:</span></span>

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

#### <a name="ble-printer-module-configuration"></a><span data-ttu-id="d7bd3-241">Configuração do módulo var impressora</span><span class="sxs-lookup"><span data-stu-id="d7bd3-241">BLE Printer module configuration</span></span>

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

#### <a name="blec2d-module-configuration"></a><span data-ttu-id="d7bd3-242">Configuração do módulo BLEC2D</span><span class="sxs-lookup"><span data-stu-id="d7bd3-242">BLEC2D Module Configuration</span></span>

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

#### <a name="routing-configuration"></a><span data-ttu-id="d7bd3-243">Configuração de encaminhamento</span><span class="sxs-lookup"><span data-stu-id="d7bd3-243">Routing Configuration</span></span>

<span data-ttu-id="d7bd3-244">Olá seguinte configuração garante seguinte Olá encaminhamento entre os módulos de limite de IoT:</span><span class="sxs-lookup"><span data-stu-id="d7bd3-244">hello following configuration ensures hello following routing between IoT Edge modules:</span></span>

* <span data-ttu-id="d7bd3-245">Olá **registador** módulo recebe e regista todas as mensagens.</span><span class="sxs-lookup"><span data-stu-id="d7bd3-245">hello **Logger** module receives and logs all messages.</span></span>
* <span data-ttu-id="d7bd3-246">Olá **SensorTag** módulo envia Olá de tooboth mensagens **mapeamento** e **var impressora** módulos.</span><span class="sxs-lookup"><span data-stu-id="d7bd3-246">hello **SensorTag** module sends messages tooboth hello **mapping** and **BLE Printer** modules.</span></span>
* <span data-ttu-id="d7bd3-247">Olá **mapeamento** módulo envia mensagens toohello **IoTHub** toobe módulo enviado tooyour IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="d7bd3-247">hello **mapping** module sends messages toohello **IoTHub** module toobe sent up tooyour IoT Hub.</span></span>
* <span data-ttu-id="d7bd3-248">Olá **IoTHub** módulo envia mensagens de fazer uma cópia toohello **mapeamento** módulo.</span><span class="sxs-lookup"><span data-stu-id="d7bd3-248">hello **IoTHub** module sends messages back toohello **mapping** module.</span></span>
* <span data-ttu-id="d7bd3-249">Olá **mapeamento** módulo envia mensagens toohello **BLEC2D** módulo.</span><span class="sxs-lookup"><span data-stu-id="d7bd3-249">hello **mapping** module sends messages toohello **BLEC2D** module.</span></span>
* <span data-ttu-id="d7bd3-250">Olá **BLEC2D** módulo envia mensagens de fazer uma cópia toohello **Sensor Tag** módulo.</span><span class="sxs-lookup"><span data-stu-id="d7bd3-250">hello **BLEC2D** module sends messages back toohello **Sensor Tag** module.</span></span>

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

<span data-ttu-id="d7bd3-251">exemplo de Olá toorun, passagem Olá caminho toohello JSON ficheiro de configuração como um parâmetro toohello **var\_gateway** binário.</span><span class="sxs-lookup"><span data-stu-id="d7bd3-251">toorun hello sample, pass hello path toohello JSON configuration file as a parameter toohello **ble\_gateway** binary.</span></span> <span data-ttu-id="d7bd3-252">Olá comando seguinte assume que está a utilizar Olá **gateway_sample.json** ficheiro de configuração.</span><span class="sxs-lookup"><span data-stu-id="d7bd3-252">hello following command assumes you are using hello **gateway_sample.json** configuration file.</span></span> <span data-ttu-id="d7bd3-253">Executar este comando de Olá **iot edge** pasta Olá Raspberry Pi:</span><span class="sxs-lookup"><span data-stu-id="d7bd3-253">Execute this command from hello **iot-edge** folder on hello Raspberry Pi:</span></span>

```sh
./build/samples/ble_gateway/ble_gateway ./samples/ble_gateway/src/gateway_sample.json
```

<span data-ttu-id="d7bd3-254">Poderá ser necessário toopress Olá pequeno botão no Olá SensorTag dispositivo toomake detetável-lo antes de executar o exemplo de Olá.</span><span class="sxs-lookup"><span data-stu-id="d7bd3-254">You may need toopress hello small button on hello SensorTag device toomake it discoverable before you run hello sample.</span></span>

<span data-ttu-id="d7bd3-255">Quando executar o exemplo de Olá, pode utilizar Olá [Explorador de dispositivo](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) ou Olá [iothub explorer](https://github.com/Azure/iothub-explorer) Olá mensagens ferramenta toomonitor Olá reencaminha o gateway de IoT a partir de dispositivos SensorTag de Olá.</span><span class="sxs-lookup"><span data-stu-id="d7bd3-255">When you run hello sample, you can use hello [device explorer](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) or hello [iothub-explorer](https://github.com/Azure/iothub-explorer) tool toomonitor hello messages hello IoT Edge gateway forwards from hello SensorTag device.</span></span> <span data-ttu-id="d7bd3-256">Por exemplo, através do Explorador do iothub pode monitorizar as mensagens de dispositivo para a nuvem utilizando Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="d7bd3-256">For example, using iothub-explorer you can monitor device-to-cloud messages using hello following command:</span></span>

```sh
iothub-explorer monitor-events --login "HostName={Your iot hub name}.azure-devices.net;SharedAccessKeyName=iothubowner;SharedAccessKey={Your IoT Hub key}"
```

## <a name="send-cloud-to-device-messages"></a><span data-ttu-id="d7bd3-257">Enviar mensagens da cloud para o dispositivo</span><span class="sxs-lookup"><span data-stu-id="d7bd3-257">Send cloud-to-device messages</span></span>

<span data-ttu-id="d7bd3-258">módulo de var Olá também suporta enviar comandos a partir de dispositivos do IoT Hub toohello.</span><span class="sxs-lookup"><span data-stu-id="d7bd3-258">hello BLE module also supports sending commands from IoT Hub toohello device.</span></span> <span data-ttu-id="d7bd3-259">Pode utilizar Olá [Explorador de dispositivo](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) ou Olá [iothub explorer](https://github.com/Azure/iothub-explorer) mensagens JSON ferramenta toosend esse módulo do Olá var gateway reencaminha no dispositivo de var toohello.</span><span class="sxs-lookup"><span data-stu-id="d7bd3-259">You can use hello [device explorer](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) or hello [iothub-explorer](https://github.com/Azure/iothub-explorer) tool toosend JSON messages that hello BLE gateway module forwards on toohello BLE device.</span></span>

<span data-ttu-id="d7bd3-260">Se estiver a utilizar o dispositivo de Texas Instruments SensorTag Olá, pode ativar o LED de Olá vermelho, LED verde ou buzzer ao enviar comandos a partir do IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="d7bd3-260">If you are using hello Texas Instruments SensorTag device, you can turn on hello red LED, green LED, or buzzer by sending commands from IoT Hub.</span></span> <span data-ttu-id="d7bd3-261">Antes de enviar comandos a partir do IoT Hub, envie primeiro Olá seguintes duas mensagens JSON por ordem.</span><span class="sxs-lookup"><span data-stu-id="d7bd3-261">Before you send commands from IoT Hub, first send hello following two JSON messages in order.</span></span> <span data-ttu-id="d7bd3-262">Em seguida, pode enviar quaisquer Olá comandos tooturn lights Olá ou buzzer.</span><span class="sxs-lookup"><span data-stu-id="d7bd3-262">Then you can send any of hello commands tooturn on hello lights or buzzer.</span></span>

1. <span data-ttu-id="d7bd3-263">Repor todas as LEDs e buzzer Olá (desligue-os):</span><span class="sxs-lookup"><span data-stu-id="d7bd3-263">Reset all LEDs and hello buzzer (turn them off):</span></span>

    ```json
    {
      "type": "write_once",
      "characteristic_uuid": "F000AA65-0451-4000-B000-000000000000",
      "data": "AA=="
    }
    ```

1. <span data-ttu-id="d7bd3-264">Configure e/s como 'remoto':</span><span class="sxs-lookup"><span data-stu-id="d7bd3-264">Configure I/O as 'remote':</span></span>

    ```json
    {
      "type": "write_once",
      "characteristic_uuid": "F000AA66-0451-4000-B000-000000000000",
      "data": "AQ=="
    }
    ```

<span data-ttu-id="d7bd3-265">Agora pode enviar quaisquer Olá os seguintes comandos tooturn lights Olá ou buzzer no dispositivo de SensorTag Olá:</span><span class="sxs-lookup"><span data-stu-id="d7bd3-265">Now you can send any of hello following commands tooturn on hello lights or buzzer on hello SensorTag device:</span></span>

* <span data-ttu-id="d7bd3-266">Ative LED Olá vermelho:</span><span class="sxs-lookup"><span data-stu-id="d7bd3-266">Turn on hello red LED:</span></span>

    ```json
    {
      "type": "write_once",
      "characteristic_uuid": "F000AA65-0451-4000-B000-000000000000",
      "data": "AQ=="
    }
    ```

* <span data-ttu-id="d7bd3-267">Ative LED Olá verde:</span><span class="sxs-lookup"><span data-stu-id="d7bd3-267">Turn on hello green LED:</span></span>

    ```json
    {
      "type": "write_once",
      "characteristic_uuid": "F000AA65-0451-4000-B000-000000000000",
      "data": "Ag=="
    }
    ```

* <span data-ttu-id="d7bd3-268">Ative buzzer Olá:</span><span class="sxs-lookup"><span data-stu-id="d7bd3-268">Turn on hello buzzer:</span></span>

    ```json
    {
      "type": "write_once",
      "characteristic_uuid": "F000AA65-0451-4000-B000-000000000000",
      "data": "BA=="
    }
    ```

## <a name="next-steps"></a><span data-ttu-id="d7bd3-269">Passos Seguintes</span><span class="sxs-lookup"><span data-stu-id="d7bd3-269">Next Steps</span></span>

<span data-ttu-id="d7bd3-270">Se pretender toogain uma compreensão mais avançada de limite de IoT e experimente alguns exemplos de código, visite o seguinte Olá tutoriais de programador e de recursos:</span><span class="sxs-lookup"><span data-stu-id="d7bd3-270">If you want toogain a more advanced understanding of IoT Edge and experiment with some code examples, visit hello following developer tutorials and resources:</span></span>

* <span data-ttu-id="d7bd3-271">[Limite de IoT do Azure][lnk-sdk]</span><span class="sxs-lookup"><span data-stu-id="d7bd3-271">[Azure IoT Edge][lnk-sdk]</span></span>

<span data-ttu-id="d7bd3-272">toofurther explorar Olá das capacidades do IoT Hub, consulte:</span><span class="sxs-lookup"><span data-stu-id="d7bd3-272">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="d7bd3-273">[Guia para programadores do IoT Hub][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="d7bd3-273">[IoT Hub developer guide][lnk-devguide]</span></span>

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
