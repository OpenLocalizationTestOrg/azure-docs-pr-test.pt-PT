---
title: aaaRaspberry Pi toocloud (Node.js) - ligar Raspberry Pi tooAzure IoT Hub | Microsoft Docs
description: Saiba como toosetup e ligar Raspberry Pi tooAzure IoT Hub para a plataforma de nuvem do Azure do Raspberry Pi toosend dados toohello neste tutorial.
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: iot do Azure raspberry pi, raspberry pi iot hub, raspberry pi enviar dados toocloud, raspberry pi toocloud
ms.assetid: b0e14bfa-8e64-440a-a6ec-e507ca0f76ba
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 5/27/2017
ms.author: xshi
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 57a15ab3984021a9c18ff0aa1316a4d4c6ebdec1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="connect-raspberry-pi-tooazure-iot-hub-nodejs"></a><span data-ttu-id="22035-104">Ligar Raspberry Pi tooAzure IoT Hub (Node.js)</span><span class="sxs-lookup"><span data-stu-id="22035-104">Connect Raspberry Pi tooAzure IoT Hub (Node.js)</span></span>

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

<span data-ttu-id="22035-105">Neste tutorial, começar por Olá Noções básicas de trabalhar com Raspberry Pi que está a executar Raspbian de aprendizagem.</span><span class="sxs-lookup"><span data-stu-id="22035-105">In this tutorial, you begin by learning hello basics of working with Raspberry Pi that's running Raspbian.</span></span> <span data-ttu-id="22035-106">Em seguida, saiba como tooseamlessly ligar a sua nuvem toohello de dispositivos utilizando [IoT Hub do Azure](iot-hub-what-is-iot-hub.md).</span><span class="sxs-lookup"><span data-stu-id="22035-106">You then learn how tooseamlessly connect your devices toohello cloud by using [Azure IoT Hub](iot-hub-what-is-iot-hub.md).</span></span> <span data-ttu-id="22035-107">Para exemplos do Windows 10 IoT Core, visite toohello [Windows Dev Center](http://www.windowsondevices.com/).</span><span class="sxs-lookup"><span data-stu-id="22035-107">For Windows 10 IoT Core samples, go toohello [Windows Dev Center](http://www.windowsondevices.com/).</span></span>

<span data-ttu-id="22035-108">Não tem um kit ainda?</span><span class="sxs-lookup"><span data-stu-id="22035-108">Don't have a kit yet?</span></span> <span data-ttu-id="22035-109">Tente [simulador online Raspberry Pi](iot-hub-raspberry-pi-web-simulator-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="22035-109">Try [Raspberry Pi online simulator](iot-hub-raspberry-pi-web-simulator-get-started.md).</span></span> <span data-ttu-id="22035-110">Ou comprar um novo kit [aqui](https://azure.microsoft.com/develop/iot/starter-kits).</span><span class="sxs-lookup"><span data-stu-id="22035-110">Or buy a new kit [here](https://azure.microsoft.com/develop/iot/starter-kits).</span></span>


## <a name="what-you-do"></a><span data-ttu-id="22035-111">O que fazer</span><span class="sxs-lookup"><span data-stu-id="22035-111">What you do</span></span>

* <span data-ttu-id="22035-112">Crie um hub IoT.</span><span class="sxs-lookup"><span data-stu-id="22035-112">Create an IoT hub.</span></span>
* <span data-ttu-id="22035-113">Registe um dispositivo para Pi no seu IoT hub.</span><span class="sxs-lookup"><span data-stu-id="22035-113">Register a device for Pi in your IoT hub.</span></span>
* <span data-ttu-id="22035-114">A configuração Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="22035-114">Setup Raspberry Pi.</span></span>
* <span data-ttu-id="22035-115">Execute um exemplo de aplicação no Pi toosend sensor dados tooyour do IoT hub.</span><span class="sxs-lookup"><span data-stu-id="22035-115">Run a sample application on Pi toosend sensor data tooyour IoT hub.</span></span>

<span data-ttu-id="22035-116">Ligar Raspberry Pi tooan do IoT hub que criou.</span><span class="sxs-lookup"><span data-stu-id="22035-116">Connect Raspberry Pi tooan IoT hub that you create.</span></span> <span data-ttu-id="22035-117">Em seguida, executar uma aplicação de exemplo nos dados relativos à temperatura e humidade do toocollect Pi a partir de um sensor BME280.</span><span class="sxs-lookup"><span data-stu-id="22035-117">Then you run a sample application on Pi toocollect temperature and humidity data from a BME280 sensor.</span></span> <span data-ttu-id="22035-118">Por fim, enviar Olá sensor dados tooyour do IoT hub.</span><span class="sxs-lookup"><span data-stu-id="22035-118">Finally, you send hello sensor data tooyour IoT hub.</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="22035-119">O que irá aprender</span><span class="sxs-lookup"><span data-stu-id="22035-119">What you learn</span></span>

* <span data-ttu-id="22035-120">Como toocreate um hub IoT do Azure e obter a cadeia de ligação do novo dispositivo.</span><span class="sxs-lookup"><span data-stu-id="22035-120">How toocreate an Azure IoT hub and get your new device connection string.</span></span>
* <span data-ttu-id="22035-121">Como tooconnect Pi com um sensor BME280.</span><span class="sxs-lookup"><span data-stu-id="22035-121">How tooconnect Pi with a BME280 sensor.</span></span>
* <span data-ttu-id="22035-122">Como dados de sensores de toocollect ao executar uma aplicação de exemplo no Pi.</span><span class="sxs-lookup"><span data-stu-id="22035-122">How toocollect sensor data by running a sample application on Pi.</span></span>
* <span data-ttu-id="22035-123">Como toosend sensor dados tooyour do IoT hub.</span><span class="sxs-lookup"><span data-stu-id="22035-123">How toosend sensor data tooyour IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="22035-124">Do que precisa</span><span class="sxs-lookup"><span data-stu-id="22035-124">What you need</span></span>

![Do que precisa](media/iot-hub-raspberry-pi-kit-node-get-started/0_starter_kit.jpg)

* <span data-ttu-id="22035-126">Olá quadro Raspberry Pi 2 ou 3 do Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="22035-126">hello Raspberry Pi 2 or Raspberry Pi 3 board.</span></span>
* <span data-ttu-id="22035-127">Uma subscrição ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="22035-127">An active Azure subscription.</span></span> <span data-ttu-id="22035-128">Se não tiver uma conta do Azure, [criar uma conta de avaliação gratuita do Azure](https://azure.microsoft.com/free/) em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="22035-128">If you don't have an Azure account, [create a free Azure trial account](https://azure.microsoft.com/free/) in just a few minutes.</span></span>
* <span data-ttu-id="22035-129">Um monitor, um teclado USB e um rato que se ligam tooPi.</span><span class="sxs-lookup"><span data-stu-id="22035-129">A monitor, a USB keyboard, and mouse that connect tooPi.</span></span>
* <span data-ttu-id="22035-130">Um Mac ou num PC com Windows ou Linux.</span><span class="sxs-lookup"><span data-stu-id="22035-130">A Mac or a PC that is running Windows or Linux.</span></span>
* <span data-ttu-id="22035-131">Uma ligação à Internet.</span><span class="sxs-lookup"><span data-stu-id="22035-131">An Internet connection.</span></span>
* <span data-ttu-id="22035-132">Um 16 GB ou superior cartão microSD.</span><span class="sxs-lookup"><span data-stu-id="22035-132">A 16 GB or above microSD card.</span></span>
* <span data-ttu-id="22035-133">Um USB SD adaptador ou microSD cartão tooburn Olá imagem do sistema operativo no cartão microSD de Olá.</span><span class="sxs-lookup"><span data-stu-id="22035-133">A USB-SD adapter or microSD card tooburn hello operating system image onto hello microSD card.</span></span>
* <span data-ttu-id="22035-134">Forneça uma potência de 2 amp 5 volt com o cabo USB micro do Olá 6 online.</span><span class="sxs-lookup"><span data-stu-id="22035-134">A 5-volt 2-amp power supply with hello 6-foot micro USB cable.</span></span>

<span data-ttu-id="22035-135">Olá seguintes itens é opcional:</span><span class="sxs-lookup"><span data-stu-id="22035-135">hello following items are optional:</span></span>

* <span data-ttu-id="22035-136">Um assembled Adafruit BME280 temperatura, pressão e humidade sensor.</span><span class="sxs-lookup"><span data-stu-id="22035-136">An assembled Adafruit BME280 temperature, pressure, and humidity sensor.</span></span>
* <span data-ttu-id="22035-137">Um breadboard.</span><span class="sxs-lookup"><span data-stu-id="22035-137">A breadboard.</span></span>
* <span data-ttu-id="22035-138">Cablagem de jumper 6 F/M.</span><span class="sxs-lookup"><span data-stu-id="22035-138">6 F/M jumper wires.</span></span>
* <span data-ttu-id="22035-139">Um diffused LED 10 mm.</span><span class="sxs-lookup"><span data-stu-id="22035-139">A diffused 10-mm LED.</span></span>


> [!NOTE] 
<span data-ttu-id="22035-140">Estes itens são opcionais, porque o suporte de exemplo de código Olá simulated dados de sensores.</span><span class="sxs-lookup"><span data-stu-id="22035-140">These items are optional because hello code sample support simulated sensor data.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="setup-raspberry-pi"></a><span data-ttu-id="22035-141">Configurar Raspberry Pi</span><span class="sxs-lookup"><span data-stu-id="22035-141">Setup Raspberry Pi</span></span>

### <a name="install-hello-raspbian-operating-system-for-pi"></a><span data-ttu-id="22035-142">Instalar o sistema de operativo Olá Raspbian para Pi</span><span class="sxs-lookup"><span data-stu-id="22035-142">Install hello Raspbian operating system for Pi</span></span>

<span data-ttu-id="22035-143">Prepare o cartão microSD de Olá para a instalação da imagem de Raspbian Olá.</span><span class="sxs-lookup"><span data-stu-id="22035-143">Prepare hello microSD card for installation of hello Raspbian image.</span></span>

1. <span data-ttu-id="22035-144">Transferir Raspbian.</span><span class="sxs-lookup"><span data-stu-id="22035-144">Download Raspbian.</span></span>
   1. <span data-ttu-id="22035-145">[Transferir Raspbian Jessie com ambiente de trabalho](https://www.raspberrypi.org/downloads/raspbian/) (ficheiro. zip de Olá).</span><span class="sxs-lookup"><span data-stu-id="22035-145">[Download Raspbian Jessie with Desktop](https://www.raspberrypi.org/downloads/raspbian/) (hello .zip file).</span></span>
   1. <span data-ttu-id="22035-146">Extrair Olá Raspbian imagem tooa pasta do computador.</span><span class="sxs-lookup"><span data-stu-id="22035-146">Extract hello Raspbian image tooa folder on your computer.</span></span>
1. <span data-ttu-id="22035-147">Instale Raspbian toohello microSD cartão.</span><span class="sxs-lookup"><span data-stu-id="22035-147">Install Raspbian toohello microSD card.</span></span>
   1. <span data-ttu-id="22035-148">[Transfira e instale o utilitário de burner Olá Etcher SD cartão](https://etcher.io/).</span><span class="sxs-lookup"><span data-stu-id="22035-148">[Download and install hello Etcher SD card burner utility](https://etcher.io/).</span></span>
   1. <span data-ttu-id="22035-149">Execute Etcher e selecione a imagem de Raspbian Olá que extraiu no passo 1.</span><span class="sxs-lookup"><span data-stu-id="22035-149">Run Etcher and select hello Raspbian image that you extracted in step 1.</span></span>
   1. <span data-ttu-id="22035-150">Selecione a unidade de cartão microSD de Olá.</span><span class="sxs-lookup"><span data-stu-id="22035-150">Select hello microSD card drive.</span></span> <span data-ttu-id="22035-151">Tenha em atenção que Etcher poderá já selecionou correta da unidade Olá.</span><span class="sxs-lookup"><span data-stu-id="22035-151">Note that Etcher may have already selected hello correct drive.</span></span>
   1. <span data-ttu-id="22035-152">Clique em Flash tooinstall Raspbian toohello microSD cartão.</span><span class="sxs-lookup"><span data-stu-id="22035-152">Click Flash tooinstall Raspbian toohello microSD card.</span></span>
   1. <span data-ttu-id="22035-153">Remova o cartão microSD de Olá do seu computador quando a instalação estiver concluída.</span><span class="sxs-lookup"><span data-stu-id="22035-153">Remove hello microSD card from your computer when installation is complete.</span></span> <span data-ttu-id="22035-154">É diretamente cartão de microSD Olá tooremove seguro porque Etcher automaticamente ejects ou unmounts cartão microSD de Olá após a conclusão.</span><span class="sxs-lookup"><span data-stu-id="22035-154">It's safe tooremove hello microSD card directly because Etcher automatically ejects or unmounts hello microSD card upon completion.</span></span>
   1. <span data-ttu-id="22035-155">Inserir cartão microSD de Olá Pi.</span><span class="sxs-lookup"><span data-stu-id="22035-155">Insert hello microSD card into Pi.</span></span>

### <a name="enable-ssh-and-i2c"></a><span data-ttu-id="22035-156">Ativar o SSH e I2C</span><span class="sxs-lookup"><span data-stu-id="22035-156">Enable SSH and I2C</span></span>

1. <span data-ttu-id="22035-157">Ligar o monitor de toohello Pi, teclado e rato, inicie o instalador de plataforma e, em seguida, inicie sessão no Raspbian utilizando `pi` como nome de utilizador Olá e `raspberry` como palavra-passe de Olá.</span><span class="sxs-lookup"><span data-stu-id="22035-157">Connect Pi toohello monitor, keyboard and mouse, start Pi and then log in Raspbian by using `pi` as hello user name and `raspberry` as hello password.</span></span>
1. <span data-ttu-id="22035-158">Clique em Olá Raspberry ícone > **preferências** > **Raspberry Pi configuração**.</span><span class="sxs-lookup"><span data-stu-id="22035-158">Click hello Raspberry icon > **Preferences** > **Raspberry Pi Configuration**.</span></span>

   ![menu de preferências Raspbian Olá](media/iot-hub-raspberry-pi-kit-node-get-started/1_raspbian-preferences-menu.png)

1. <span data-ttu-id="22035-160">No Olá **Interfaces** separador, defina **I2C** e **SSH** demasiado**ativar**e, em seguida, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="22035-160">On hello **Interfaces** tab, set **I2C** and **SSH** too**Enable**, and then click **OK**.</span></span> <span data-ttu-id="22035-161">Se não tiver sensores físicos e pretende que os dados de sensores de toouse simulated, este passo é opcional.</span><span class="sxs-lookup"><span data-stu-id="22035-161">If you don't have physical sensors and want toouse simulated sensor data, this step is optional.</span></span>

   ![Ativar I2C e SSH no Raspberry Pi](media/iot-hub-raspberry-pi-kit-node-get-started/2_enable-i2c-ssh-on-raspberry-pi.png)

> [!NOTE] 
<span data-ttu-id="22035-163">tooenable SSH e I2C, pode encontrar mais de referência de documentos no [raspberrypi.org](https://www.raspberrypi.org/documentation/remote-access/ssh/) e [Adafruit.com](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-4-gpio-setup/configuring-i2c).</span><span class="sxs-lookup"><span data-stu-id="22035-163">tooenable SSH and I2C, you can find more reference documents on [raspberrypi.org](https://www.raspberrypi.org/documentation/remote-access/ssh/) and [Adafruit.com](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-4-gpio-setup/configuring-i2c).</span></span>

### <a name="connect-hello-sensor-toopi"></a><span data-ttu-id="22035-164">Ligar Olá sensor tooPi</span><span class="sxs-lookup"><span data-stu-id="22035-164">Connect hello sensor tooPi</span></span>

<span data-ttu-id="22035-165">Utilize Olá de breadboard e jumper de tooconnect de cablagem um LED e um tooPi BME280 da seguinte forma.</span><span class="sxs-lookup"><span data-stu-id="22035-165">Use hello breadboard and jumper wires tooconnect an LED and a BME280 tooPi as follows.</span></span> <span data-ttu-id="22035-166">Se não tiver sensor Olá, [ignorar esta secção](#connect-pi-to-the-network).</span><span class="sxs-lookup"><span data-stu-id="22035-166">If you don’t have hello sensor, [skip this section](#connect-pi-to-the-network).</span></span>

![Olá ligação Raspberry Pi e sensor](media/iot-hub-raspberry-pi-kit-node-get-started/3_raspberry-pi-sensor-connection.png)

<span data-ttu-id="22035-168">sensor de Olá BME280 pode recolher dados relativos à temperatura e humidade.</span><span class="sxs-lookup"><span data-stu-id="22035-168">hello BME280 sensor can collect temperature and humidity data.</span></span> <span data-ttu-id="22035-169">E Olá LED será blink se houver uma comunicação entre o dispositivo e Olá nuvem.</span><span class="sxs-lookup"><span data-stu-id="22035-169">And hello LED will blink if there is a communication between device and hello cloud.</span></span> 

<span data-ttu-id="22035-170">Para sensor pins, utilize Olá wiring os seguintes:</span><span class="sxs-lookup"><span data-stu-id="22035-170">For sensor pins, use hello following wiring:</span></span>

| <span data-ttu-id="22035-171">Iniciar (Sensor & LED)</span><span class="sxs-lookup"><span data-stu-id="22035-171">Start (Sensor & LED)</span></span>     | <span data-ttu-id="22035-172">Fim (quadro)</span><span class="sxs-lookup"><span data-stu-id="22035-172">End (Board)</span></span>            | <span data-ttu-id="22035-173">Cor de cabo</span><span class="sxs-lookup"><span data-stu-id="22035-173">Cable Color</span></span>   |
| -----------------------  | ---------------------- | ------------: |
| <span data-ttu-id="22035-174">VDD (Pin 5g)</span><span class="sxs-lookup"><span data-stu-id="22035-174">VDD (Pin 5G)</span></span>             | <span data-ttu-id="22035-175">3.3V PWR (Pin 1)</span><span class="sxs-lookup"><span data-stu-id="22035-175">3.3V PWR (Pin 1)</span></span>       | <span data-ttu-id="22035-176">Cabo branco</span><span class="sxs-lookup"><span data-stu-id="22035-176">White cable</span></span>   |
| <span data-ttu-id="22035-177">GND (Pin 7G)</span><span class="sxs-lookup"><span data-stu-id="22035-177">GND (Pin 7G)</span></span>             | <span data-ttu-id="22035-178">GND (Pin 6)</span><span class="sxs-lookup"><span data-stu-id="22035-178">GND (Pin 6)</span></span>            | <span data-ttu-id="22035-179">Cabo castanha</span><span class="sxs-lookup"><span data-stu-id="22035-179">Brown cable</span></span>   |
| <span data-ttu-id="22035-180">SDI (Pin 10g)</span><span class="sxs-lookup"><span data-stu-id="22035-180">SDI (Pin 10G)</span></span>            | <span data-ttu-id="22035-181">I2C1 SDA (Pin 3)</span><span class="sxs-lookup"><span data-stu-id="22035-181">I2C1 SDA (Pin 3)</span></span>       | <span data-ttu-id="22035-182">Cabo vermelho</span><span class="sxs-lookup"><span data-stu-id="22035-182">Red cable</span></span>     |
| <span data-ttu-id="22035-183">SCK (Pin 8G)</span><span class="sxs-lookup"><span data-stu-id="22035-183">SCK (Pin 8G)</span></span>             | <span data-ttu-id="22035-184">I2C1 SCL (Pin 5)</span><span class="sxs-lookup"><span data-stu-id="22035-184">I2C1 SCL (Pin 5)</span></span>       | <span data-ttu-id="22035-185">Cabo laranja</span><span class="sxs-lookup"><span data-stu-id="22035-185">Orange cable</span></span>  |
| <span data-ttu-id="22035-186">LED VDD (Pin 18F)</span><span class="sxs-lookup"><span data-stu-id="22035-186">LED VDD (Pin 18F)</span></span>        | <span data-ttu-id="22035-187">GPIO 24 (Pin 18)</span><span class="sxs-lookup"><span data-stu-id="22035-187">GPIO 24 (Pin 18)</span></span>       | <span data-ttu-id="22035-188">Cabo branco</span><span class="sxs-lookup"><span data-stu-id="22035-188">White cable</span></span>   |
| <span data-ttu-id="22035-189">LED GND (Pin 17F)</span><span class="sxs-lookup"><span data-stu-id="22035-189">LED GND (Pin 17F)</span></span>        | <span data-ttu-id="22035-190">GND (Pin 20)</span><span class="sxs-lookup"><span data-stu-id="22035-190">GND (Pin 20)</span></span>           | <span data-ttu-id="22035-191">Cabo preto</span><span class="sxs-lookup"><span data-stu-id="22035-191">Black cable</span></span>   |

<span data-ttu-id="22035-192">Clique em tooview [Raspberry Pi 2 e 3 mapeamentos de Pin](https://developer.microsoft.com/windows/iot/docs/pinmappingsrpi) para referência.</span><span class="sxs-lookup"><span data-stu-id="22035-192">Click tooview [Raspberry Pi 2 & 3 Pin mappings](https://developer.microsoft.com/windows/iot/docs/pinmappingsrpi) for your reference.</span></span>

<span data-ttu-id="22035-193">Depois de se ligar com êxito BME280 tooyour Raspberry Pi, deve ser como abaixo imagem.</span><span class="sxs-lookup"><span data-stu-id="22035-193">After you've successfully connected BME280 tooyour Raspberry Pi, it should be like below image.</span></span>

![Instalador de plataforma ligado e BME280](media/iot-hub-raspberry-pi-kit-node-get-started/4_connected-pi.jpg)

### <a name="connect-pi-toohello-network"></a><span data-ttu-id="22035-195">Ligar a rede de toohello Pi</span><span class="sxs-lookup"><span data-stu-id="22035-195">Connect Pi toohello network</span></span>

<span data-ttu-id="22035-196">Ative a Pi utilizando o cabo USB micro Olá e fonte de alimentação Olá.</span><span class="sxs-lookup"><span data-stu-id="22035-196">Turn on Pi by using hello micro USB cable and hello power supply.</span></span> <span data-ttu-id="22035-197">Utilize Olá Ethernet cabo tooconnect Pi tooyour com fios de rede ou seguir Olá [instruções de Olá Raspberry Pi Foundation](https://www.raspberrypi.org/learning/software-guide/wifi/) rede sem fios do tooconnect Pi tooyour.</span><span class="sxs-lookup"><span data-stu-id="22035-197">Use hello Ethernet cable tooconnect Pi tooyour wired network or follow hello [instructions from hello Raspberry Pi Foundation](https://www.raspberrypi.org/learning/software-guide/wifi/) tooconnect Pi tooyour wireless network.</span></span> <span data-ttu-id="22035-198">Após a sua Pi foi rede toohello ligado com êxito, é necessário tootake nota Olá [endereço IP do seu Pi](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-3-network-setup/finding-your-pis-ip-address).</span><span class="sxs-lookup"><span data-stu-id="22035-198">After your Pi has been successfully connected toohello network, you need tootake a note of hello [IP address of your Pi](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-3-network-setup/finding-your-pis-ip-address).</span></span>

![Rede toowired ligado](media/iot-hub-raspberry-pi-kit-node-get-started/5_power-on-pi.jpg)

> [!NOTE]
> <span data-ttu-id="22035-200">Certifique-se que Pi toohello ligado, mesmo que o computador de rede.</span><span class="sxs-lookup"><span data-stu-id="22035-200">Make sure that Pi is connected toohello same network as your computer.</span></span> <span data-ttu-id="22035-201">Por exemplo, se o computador está ligado tooa rede sem fios enquanto Pi está ligado tooa rede com fios, poderá não o ver Olá IP endereço na saída de devdisco Olá.</span><span class="sxs-lookup"><span data-stu-id="22035-201">For example, if your computer is connected tooa wireless network while Pi is connected tooa wired network, you might not see hello IP address in hello devdisco output.</span></span>

## <a name="run-a-sample-application-on-pi"></a><span data-ttu-id="22035-202">Executar uma aplicação de exemplo no instalador de plataforma</span><span class="sxs-lookup"><span data-stu-id="22035-202">Run a sample application on Pi</span></span>

### <a name="clone-sample-application-and-install-hello-prerequisite-packages"></a><span data-ttu-id="22035-203">Clonar o exemplo de aplicação e instalar pacotes de pré-requisitos Olá</span><span class="sxs-lookup"><span data-stu-id="22035-203">Clone sample application and install hello prerequisite packages</span></span>

1. <span data-ttu-id="22035-204">Utilize um dos Olá os seguintes clientes SSH do seu tooyour de tooconnect do computador anfitrião Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="22035-204">Use one of hello following SSH clients from your host computer tooconnect tooyour Raspberry Pi.</span></span>
   
   <span data-ttu-id="22035-205">**Utilizadores do Windows**</span><span class="sxs-lookup"><span data-stu-id="22035-205">**Windows Users**</span></span>
   1. <span data-ttu-id="22035-206">Transfira e instale [PuTTY](http://www.putty.org/) para Windows.</span><span class="sxs-lookup"><span data-stu-id="22035-206">Download and install [PuTTY](http://www.putty.org/) for Windows.</span></span> 
   1. <span data-ttu-id="22035-207">Copie o endereço IP Olá a secção de instalador de plataforma para Olá anfitrião nome (ou endereço IP) e selecione SSH como tipo de ligação de Olá.</span><span class="sxs-lookup"><span data-stu-id="22035-207">Copy hello IP address of your Pi into hello Host name (or IP address) section and select SSH as hello connection type.</span></span>
   
   ![PuTTy](media/iot-hub-raspberry-pi-kit-node-get-started/7_putty-windows.png)
   
   <span data-ttu-id="22035-209">**Mac e Ubuntu utilizadores**</span><span class="sxs-lookup"><span data-stu-id="22035-209">**Mac and Ubuntu Users**</span></span>
   
   <span data-ttu-id="22035-210">Utilize Olá SSH no cliente incorporado Ubuntu ou macOS.</span><span class="sxs-lookup"><span data-stu-id="22035-210">Use hello built-in SSH client on Ubuntu or macOS.</span></span> <span data-ttu-id="22035-211">Poderá ser necessário toorun `ssh pi@<ip address of pi>` tooconnect Pi através de SSH.</span><span class="sxs-lookup"><span data-stu-id="22035-211">You might need toorun `ssh pi@<ip address of pi>` tooconnect Pi via SSH.</span></span>
   > [!NOTE] 
   <span data-ttu-id="22035-212">o nome de utilizador do Olá predefinido é `pi` , e a palavra-passe de Olá é `raspberry`.</span><span class="sxs-lookup"><span data-stu-id="22035-212">hello default username is `pi` , and hello password is `raspberry`.</span></span>

1. <span data-ttu-id="22035-213">Instale Node.js e NPM tooyour Pi.</span><span class="sxs-lookup"><span data-stu-id="22035-213">Install Node.js and NPM tooyour Pi.</span></span>
   
   <span data-ttu-id="22035-214">Primeiro deverá verificar a sua versão de Node.js com Olá os seguintes comandos.</span><span class="sxs-lookup"><span data-stu-id="22035-214">First you should check your Node.js version with hello following command.</span></span> 
   
   ```bash
   node -v
   ```

   <span data-ttu-id="22035-215">Se a versão de Olá é inferior à 4. x ou não há nenhum Node.js na sua Pi, em seguida, executar Olá tooinstall de comando a seguir ou atualizar Node.js.</span><span class="sxs-lookup"><span data-stu-id="22035-215">If hello version is lower than 4.x or there is no Node.js on your Pi, then run hello following command tooinstall or update Node.js.</span></span>

   ```bash
   curl -sL http://deb.nodesource.com/setup_4.x | sudo -E bash
   sudo apt-get -y install nodejs
   ```

1. <span data-ttu-id="22035-216">Clone a aplicação de exemplo Olá executando Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="22035-216">Clone hello sample application by running hello following command:</span></span>

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-node-raspberrypi-client-app
   ```

1. <span data-ttu-id="22035-217">Instale todos os pacotes hello os seguintes comandos.</span><span class="sxs-lookup"><span data-stu-id="22035-217">Install all packages by hello following command.</span></span> <span data-ttu-id="22035-218">Inclui dispositivos IoT do Azure SDK, BME280 Sensor biblioteca e da biblioteca de preparar o Pi.</span><span class="sxs-lookup"><span data-stu-id="22035-218">It includes Azure IoT device SDK, BME280 Sensor library and Wiring Pi library.</span></span>

   ```bash
   cd iot-hub-node-raspberrypi-client-app
   sudo npm install
   ```
   > [!NOTE] 
   <span data-ttu-id="22035-219">Poderá demorar vários minutos toofinish este processo de instalação, dependendo da sua ligação de rede.</span><span class="sxs-lookup"><span data-stu-id="22035-219">It might take several minutes toofinish this installation process depending on your network connection.</span></span>

### <a name="configure-hello-sample-application"></a><span data-ttu-id="22035-220">Configurar a aplicação de exemplo de Olá</span><span class="sxs-lookup"><span data-stu-id="22035-220">Configure hello sample application</span></span>

1. <span data-ttu-id="22035-221">Abra o ficheiro de configuração de Olá executando Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="22035-221">Open hello config file by running hello following commands:</span></span>

   ```bash
   nano config.json
   ```

   ![Ficheiro de configuração](media/iot-hub-raspberry-pi-kit-node-get-started/6_config-file.png)

   <span data-ttu-id="22035-223">Existem dois itens neste ficheiro, pode configurate.</span><span class="sxs-lookup"><span data-stu-id="22035-223">There are two items in this file you can configurate.</span></span> <span data-ttu-id="22035-224">Olá primeiro um é `interval`, que define o intervalo de tempo de Olá (em milissegundos) entre duas mensagens que enviam toocloud.</span><span class="sxs-lookup"><span data-stu-id="22035-224">hello first one is `interval`, which defines hello time interval (in milliseconds) between two messages that send toocloud.</span></span> <span data-ttu-id="22035-225">Olá segunda `simulatedData`, que é um valor booleano para se toouse simulated dados de sensores ou não.</span><span class="sxs-lookup"><span data-stu-id="22035-225">hello second one `simulatedData`,which is a Boolean value for whether toouse simulated sensor data or not.</span></span>

   <span data-ttu-id="22035-226">Se lhe **não tiver sensor Olá**, hello Defina `simulatedData` valor demasiado`true` aplicação de exemplo de Olá toomake criar e utilizar dados de sensores simulados.</span><span class="sxs-lookup"><span data-stu-id="22035-226">If you **don't have hello sensor**, set hello `simulatedData` value too`true` toomake hello sample application create and use simulated sensor data.</span></span>

1. <span data-ttu-id="22035-227">Guarde e saia, premindo O controlo > introduza > X de controlo.</span><span class="sxs-lookup"><span data-stu-id="22035-227">Save and exit by pressing Control-O > Enter > Control-X.</span></span>

### <a name="run-hello-sample-application"></a><span data-ttu-id="22035-228">Executar a aplicação de exemplo de Olá</span><span class="sxs-lookup"><span data-stu-id="22035-228">Run hello sample application</span></span>

<span data-ttu-id="22035-229">Execute a aplicação de exemplo de Olá executando Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="22035-229">Run hello sample application by running hello following command:</span></span>

   ```bash
   sudo node index.js '<YOUR AZURE IOT HUB DEVICE CONNECTION STRING>'
   ```

   > [!NOTE] 
   <span data-ttu-id="22035-230">Certifique-se de que copiar-colar a cadeia de ligação de dispositivo de Olá para plicas Olá.</span><span class="sxs-lookup"><span data-stu-id="22035-230">Make sure you copy-paste hello device connection string into hello single quotes.</span></span>


<span data-ttu-id="22035-231">Deverá ver a seguinte Olá de saída que mostra Olá sensor dados e Olá mensagens enviadas tooyour IoT hub.</span><span class="sxs-lookup"><span data-stu-id="22035-231">You should see hello following output that shows hello sensor data and hello messages that are sent tooyour IoT hub.</span></span>

![Saída - dados de sensor enviados a partir do IoT hub tooyour Raspberry Pi](media/iot-hub-raspberry-pi-kit-node-get-started/8_run-output.png)

## <a name="next-steps"></a><span data-ttu-id="22035-233">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="22035-233">Next steps</span></span>

<span data-ttu-id="22035-234">Executar um dados de sensores de toocollect de aplicação de exemplo e enviá-lo tooyour IoT hub.</span><span class="sxs-lookup"><span data-stu-id="22035-234">You’ve run a sample application toocollect sensor data and send it tooyour IoT hub.</span></span> <span data-ttu-id="22035-235">mensagens hello do toosee que sua Raspberry Pi enviou tooyour IoT hub ou enviar mensagens tooyour Raspberry Pi numa interface de linha de comandos, consulte Olá [gerir dispositivos de cloud messaging com tutorial de iothub Explorador](https://docs.microsoft.com/en-gb/azure/iot-hub/iot-hub-explorer-cloud-device-messaging).</span><span class="sxs-lookup"><span data-stu-id="22035-235">toosee hello messages that your Raspberry Pi has sent tooyour IoT hub or send messages tooyour Raspberry Pi in a command line interface, see hello [Manage cloud device messaging with iothub-explorer tutorial](https://docs.microsoft.com/en-gb/azure/iot-hub/iot-hub-explorer-cloud-device-messaging).</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
