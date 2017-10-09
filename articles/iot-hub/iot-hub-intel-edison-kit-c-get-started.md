---
title: aaaIntel Edison toocloud (C) - ligar Intel Edison tooAzure IoT Hub | Microsoft Docs
description: Saiba como toosetup e ligar Intel Edison tooAzure IoT Hub para a plataforma de nuvem do Azure do Intel Edison toosend dados toohello neste tutorial.
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: iot do Azure intel edison, intel iothub edison, intel edison enviar dados toocloud, intel edison toocloud
ms.assetid: 4885fa2c-c2ee-4253-b37f-ccd55f92b006
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 4/17/2017
ms.author: xshi
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d0928e6c7870d724ff2044280937a45a9e032c75
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="connect-intel-edison-tooazure-iot-hub-c"></a><span data-ttu-id="147f2-104">Ligar Intel Edison tooAzure IoT Hub (C)</span><span class="sxs-lookup"><span data-stu-id="147f2-104">Connect Intel Edison tooAzure IoT Hub (C)</span></span>

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

<span data-ttu-id="147f2-105">Neste tutorial, comece por Olá Noções básicas de trabalhar com Intel Edison de aprendizagem.</span><span class="sxs-lookup"><span data-stu-id="147f2-105">In this tutorial, you begin by learning hello basics of working with Intel Edison.</span></span> <span data-ttu-id="147f2-106">Em seguida, saiba como tooseamlessly ligar a sua nuvem toohello de dispositivos utilizando [IoT Hub do Azure](iot-hub-what-is-iot-hub.md).</span><span class="sxs-lookup"><span data-stu-id="147f2-106">You then learn how tooseamlessly connect your devices toohello cloud by using [Azure IoT Hub](iot-hub-what-is-iot-hub.md).</span></span>

<span data-ttu-id="147f2-107">Não tem um kit ainda?</span><span class="sxs-lookup"><span data-stu-id="147f2-107">Don't have a kit yet?</span></span> <span data-ttu-id="147f2-108">Iniciar [aqui](https://azure.microsoft.com/develop/iot/starter-kits)</span><span class="sxs-lookup"><span data-stu-id="147f2-108">Start [here](https://azure.microsoft.com/develop/iot/starter-kits)</span></span>

## <a name="what-you-do"></a><span data-ttu-id="147f2-109">O que fazer</span><span class="sxs-lookup"><span data-stu-id="147f2-109">What you do</span></span>

* <span data-ttu-id="147f2-110">Intel Edison o programa de configuração e e Grove módulos.</span><span class="sxs-lookup"><span data-stu-id="147f2-110">Setup Intel Edison and and Grove modules.</span></span>
* <span data-ttu-id="147f2-111">Crie um hub IoT.</span><span class="sxs-lookup"><span data-stu-id="147f2-111">Create an IoT hub.</span></span>
* <span data-ttu-id="147f2-112">Registe um dispositivo para Edison no seu IoT hub.</span><span class="sxs-lookup"><span data-stu-id="147f2-112">Register a device for Edison in your IoT hub.</span></span>
* <span data-ttu-id="147f2-113">Execute um exemplo de aplicação no Edison toosend sensor dados tooyour do IoT hub.</span><span class="sxs-lookup"><span data-stu-id="147f2-113">Run a sample application on Edison toosend sensor data tooyour IoT hub.</span></span>

<span data-ttu-id="147f2-114">Ligar Intel Edison tooan do IoT hub que criou.</span><span class="sxs-lookup"><span data-stu-id="147f2-114">Connect Intel Edison tooan IoT hub that you create.</span></span> <span data-ttu-id="147f2-115">Em seguida, execute um exemplo de aplicação no Edison toocollect relativos à temperatura e humidade dados de um sensor de temperatura Grove.</span><span class="sxs-lookup"><span data-stu-id="147f2-115">Then you run a sample application on Edison toocollect temperature and humidity data from a Grove temperature sensor.</span></span> <span data-ttu-id="147f2-116">Por fim, enviar Olá sensor dados tooyour do IoT hub.</span><span class="sxs-lookup"><span data-stu-id="147f2-116">Finally, you send hello sensor data tooyour IoT hub.</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="147f2-117">O que irá aprender</span><span class="sxs-lookup"><span data-stu-id="147f2-117">What you learn</span></span>

* <span data-ttu-id="147f2-118">Como toocreate um hub IoT do Azure e obter a cadeia de ligação do novo dispositivo.</span><span class="sxs-lookup"><span data-stu-id="147f2-118">How toocreate an Azure IoT hub and get your new device connection string.</span></span>
* <span data-ttu-id="147f2-119">Como tooconnect Edison com um sensor de temperatura Grove.</span><span class="sxs-lookup"><span data-stu-id="147f2-119">How tooconnect Edison with a Grove temperature sensor.</span></span>
* <span data-ttu-id="147f2-120">Como dados de sensores de toocollect ao executar uma aplicação de exemplo no Edison.</span><span class="sxs-lookup"><span data-stu-id="147f2-120">How toocollect sensor data by running a sample application on Edison.</span></span>
* <span data-ttu-id="147f2-121">Como toosend sensor dados tooyour do IoT hub.</span><span class="sxs-lookup"><span data-stu-id="147f2-121">How toosend sensor data tooyour IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="147f2-122">Do que precisa</span><span class="sxs-lookup"><span data-stu-id="147f2-122">What you need</span></span>

![Do que precisa](media/iot-hub-intel-edison-kit-c-get-started/0_kit.png)

* <span data-ttu-id="147f2-124">Olá quadro Intel Edison</span><span class="sxs-lookup"><span data-stu-id="147f2-124">hello Intel Edison board</span></span>
* <span data-ttu-id="147f2-125">Placa de expansão Arduino</span><span class="sxs-lookup"><span data-stu-id="147f2-125">Arduino expansion board</span></span>
* <span data-ttu-id="147f2-126">Uma subscrição ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="147f2-126">An active Azure subscription.</span></span> <span data-ttu-id="147f2-127">Se não tiver uma conta do Azure, [criar uma conta de avaliação gratuita do Azure](https://azure.microsoft.com/free/) em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="147f2-127">If you don't have an Azure account, [create a free Azure trial account](https://azure.microsoft.com/free/) in just a few minutes.</span></span>
* <span data-ttu-id="147f2-128">Um Mac ou num PC com Windows ou Linux.</span><span class="sxs-lookup"><span data-stu-id="147f2-128">A Mac or a PC that is running Windows or Linux.</span></span>
* <span data-ttu-id="147f2-129">Uma ligação à Internet.</span><span class="sxs-lookup"><span data-stu-id="147f2-129">An Internet connection.</span></span>
* <span data-ttu-id="147f2-130">Um cabo USB de um de tooType Micro B</span><span class="sxs-lookup"><span data-stu-id="147f2-130">A Micro B tooType A USB cable</span></span>
* <span data-ttu-id="147f2-131">Alimentação direta atual (DC).</span><span class="sxs-lookup"><span data-stu-id="147f2-131">A direct current (DC) power supply.</span></span> <span data-ttu-id="147f2-132">Fonte de alimentação deve ser classificado da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="147f2-132">Your power supply should be rated as follows:</span></span>
  - <span data-ttu-id="147f2-133">7 15V DC</span><span class="sxs-lookup"><span data-stu-id="147f2-133">7-15V DC</span></span>
  - <span data-ttu-id="147f2-134">Pelo menos 1500mA</span><span class="sxs-lookup"><span data-stu-id="147f2-134">At least 1500mA</span></span>
  - <span data-ttu-id="147f2-135">pin de center/interna Olá deve ser Olá positivos pólo de fonte de alimentação Olá</span><span class="sxs-lookup"><span data-stu-id="147f2-135">hello center/inner pin should be hello positive pole of hello power supply</span></span>

<span data-ttu-id="147f2-136">Olá seguintes itens é opcional:</span><span class="sxs-lookup"><span data-stu-id="147f2-136">hello following items are optional:</span></span>

* <span data-ttu-id="147f2-137">Grove proteção Base V2</span><span class="sxs-lookup"><span data-stu-id="147f2-137">Grove Base Shield V2</span></span>
* <span data-ttu-id="147f2-138">Grove - Sensor de temperatura</span><span class="sxs-lookup"><span data-stu-id="147f2-138">Grove - Temperature Sensor</span></span>
* <span data-ttu-id="147f2-139">Grove cabo</span><span class="sxs-lookup"><span data-stu-id="147f2-139">Grove Cable</span></span>
* <span data-ttu-id="147f2-140">Qualquer barras spacer ou screws incluídos em empacotamento Olá, incluindo quadro de expansão de toohello Olá módulo dois screws toofasten e quatro conjuntos de screws e plastic spacers.</span><span class="sxs-lookup"><span data-stu-id="147f2-140">Any spacer bars or screws included in hello packaging, including two screws toofasten hello module toohello expansion board and four sets of screws and plastic spacers.</span></span>

> [!NOTE] 
<span data-ttu-id="147f2-141">Estes itens são opcionais, porque o suporte de exemplo de código Olá simulated dados de sensores.</span><span class="sxs-lookup"><span data-stu-id="147f2-141">These items are optional because hello code sample support simulated sensor data.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="setup-intel-edison"></a><span data-ttu-id="147f2-142">A configuração Intel Edison</span><span class="sxs-lookup"><span data-stu-id="147f2-142">Setup Intel Edison</span></span>

### <a name="assemble-your-board"></a><span data-ttu-id="147f2-143">Monte a sua placa</span><span class="sxs-lookup"><span data-stu-id="147f2-143">Assemble your board</span></span>

<span data-ttu-id="147f2-144">Esta secção contém passos tooattach a placa de expansão do Intel Edison de® módulo tooyour.</span><span class="sxs-lookup"><span data-stu-id="147f2-144">This section contains steps tooattach your Intel® Edison module tooyour expansion board.</span></span>

1. <span data-ttu-id="147f2-145">Coloque o módulo de Intel Edison de® Olá dentro do contorno Olá branco no seu painel expansão, lining segurança holes Olá no módulo Olá com screws Olá no quadro de expansão de Olá.</span><span class="sxs-lookup"><span data-stu-id="147f2-145">Place hello Intel® Edison module within hello white outline on your expansion board, lining up hello holes on hello module with hello screws on hello expansion board.</span></span>

2. <span data-ttu-id="147f2-146">Prima para baixo no módulo Olá imediatamente por baixo palavras Olá `What will you make?` até sentir um snap.</span><span class="sxs-lookup"><span data-stu-id="147f2-146">Press down on hello module just below hello words `What will you make?` until you feel a snap.</span></span>

   ![Monte quadro 2](media/iot-hub-intel-edison-kit-c-get-started/1_assemble_board2.jpg)

3. <span data-ttu-id="147f2-148">Utilize Olá dois nuts hexadecimais (incluídos no pacote de Olá) toosecure Olá módulo toohello expansão quadro.</span><span class="sxs-lookup"><span data-stu-id="147f2-148">Use hello two hex nuts (included in hello package) toosecure hello module toohello expansion board.</span></span>

   ![Monte quadro 3](media/iot-hub-intel-edison-kit-c-get-started/2_assemble_board3.jpg)

4. <span data-ttu-id="147f2-150">Inserir uma screw dos holes canto quatro Olá no quadro de expansão de Olá.</span><span class="sxs-lookup"><span data-stu-id="147f2-150">Insert a screw in one of hello four corner holes on hello expansion board.</span></span> <span data-ttu-id="147f2-151">Twist e reforçar a um dos spacers plastic de Olá branco no screw Olá.</span><span class="sxs-lookup"><span data-stu-id="147f2-151">Twist and tighten one of hello white plastic spacers onto hello screw.</span></span>

   ![Monte quadro 4](media/iot-hub-intel-edison-kit-c-get-started/3_assemble_board4.jpg)

5. <span data-ttu-id="147f2-153">Repita para Olá outros spacers três canto.</span><span class="sxs-lookup"><span data-stu-id="147f2-153">Repeat for hello other three corner spacers.</span></span>

   ![Monte quadro 5](media/iot-hub-intel-edison-kit-c-get-started/4_assemble_board5.jpg)

<span data-ttu-id="147f2-155">Agora é assembled seu painel.</span><span class="sxs-lookup"><span data-stu-id="147f2-155">Now your board is assembled.</span></span>

   ![placa assembled](media/iot-hub-intel-edison-kit-c-get-started/5_assembled_board.jpg)

### <a name="connect-hello-grove-base-shield-and-hello-temperature-sensor"></a><span data-ttu-id="147f2-157">Ligar Olá Grove Base proteção e sensor de temperatura Olá</span><span class="sxs-lookup"><span data-stu-id="147f2-157">Connect hello Grove Base Shield and hello temperature sensor</span></span>

1. <span data-ttu-id="147f2-158">Coloque Olá Grove Base proteção no quadro tooyour.</span><span class="sxs-lookup"><span data-stu-id="147f2-158">Place hello Grove Base Shield on tooyour board.</span></span> <span data-ttu-id="147f2-159">Certifique-se de que todos os pins totalmente são ligados à sua placa.</span><span class="sxs-lookup"><span data-stu-id="147f2-159">Make sure all pins are tightly plugged into your board.</span></span>
   
   ![Proteção de Base Grove](media/iot-hub-intel-edison-kit-c-get-started/6_grove_base_sheild.jpg)

2. <span data-ttu-id="147f2-161">Sensor de temperatura de utilização Grove cabo tooconnect Grove no Olá Grove Base proteção **A0** porta.</span><span class="sxs-lookup"><span data-stu-id="147f2-161">Use Grove Cable tooconnect Grove temperature sensor onto hello Grove Base Shield **A0** port.</span></span>

   ![Ligar tootemperature sensor](media/iot-hub-intel-edison-kit-c-get-started/7_temperature_sensor.jpg)
   
   ![Ligação EDISON e sensor](media/iot-hub-intel-edison-kit-c-get-started/16_edion_sensor.png)

<span data-ttu-id="147f2-164">O sensor está agora pronta.</span><span class="sxs-lookup"><span data-stu-id="147f2-164">Now your sensor is ready.</span></span>

### <a name="power-up-edison"></a><span data-ttu-id="147f2-165">Energia segurança Edison</span><span class="sxs-lookup"><span data-stu-id="147f2-165">Power up Edison</span></span>

1. <span data-ttu-id="147f2-166">Plug-in fonte de alimentação Olá.</span><span class="sxs-lookup"><span data-stu-id="147f2-166">Plug in hello power supply.</span></span>

   ![Plug-in fonte de alimentação](media/iot-hub-intel-edison-kit-c-get-started/8_plug_power.jpg)

2. <span data-ttu-id="147f2-168">Um LED verde (com a etiqueta DS1 no Olá quadro de expansão Arduino *) deve ser apresentado e permaneça lit.</span><span class="sxs-lookup"><span data-stu-id="147f2-168">A green LED(labeled DS1 on hello Arduino* expansion board) should light up and stay lit.</span></span>

3. <span data-ttu-id="147f2-169">Aguarde um minuto para Olá quadro toofinish arrancar de segurança.</span><span class="sxs-lookup"><span data-stu-id="147f2-169">Wait one minute for hello board toofinish booting up.</span></span>

   > [!NOTE]
   > <span data-ttu-id="147f2-170">Se não tiver uma fonte de alimentação do DC, pode ainda quadro de Olá de energia através de uma porta USB.</span><span class="sxs-lookup"><span data-stu-id="147f2-170">If you do not have a DC power supply, you can still power hello board through a USB port.</span></span> <span data-ttu-id="147f2-171">Consulte `Connect Edison tooyour computer` secção para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="147f2-171">See `Connect Edison tooyour computer` section for details.</span></span> <span data-ttu-id="147f2-172">A ligar a sua placa desta forma poderão resultar num comportamento imprevisível do seu painel, especialmente quando através de Wi-Fi ou ocasionar motors.</span><span class="sxs-lookup"><span data-stu-id="147f2-172">Powering your board in this fashion may result in unpredictable behavior from your board, especially when using Wi-Fi or driving motors.</span></span>

### <a name="connect-edison-tooyour-computer"></a><span data-ttu-id="147f2-173">Ligue Edison tooyour computador</span><span class="sxs-lookup"><span data-stu-id="147f2-173">Connect Edison tooyour computer</span></span>

1. <span data-ttu-id="147f2-174">Alternar para baixo Olá microswitch para Olá dois micro portas USB, para que Edison está no modo de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="147f2-174">Toggle down hello microswitch towards hello two micro USB ports, so that Edison is in device mode.</span></span> <span data-ttu-id="147f2-175">Para as diferenças entre o modo de anfitrião e de dispositivo, referência [aqui](https://software.intel.com/en-us/node/628233#usb-device-mode-vs-usb-host-mode).</span><span class="sxs-lookup"><span data-stu-id="147f2-175">For differences between device mode and host mode, please reference [here](https://software.intel.com/en-us/node/628233#usb-device-mode-vs-usb-host-mode).</span></span>

   ![Alternar para baixo Olá microswitch](media/iot-hub-intel-edison-kit-c-get-started/9_toggle_down_microswitch.jpg)

2. <span data-ttu-id="147f2-177">Cabo do Olá micro USB ligue-se a porta USB de micro superior de Olá.</span><span class="sxs-lookup"><span data-stu-id="147f2-177">Plug hello micro USB cable into hello top micro USB port.</span></span>

   ![Porta USB de micro superior](media/iot-hub-intel-edison-kit-c-get-started/10_top_usbport.jpg)

3. <span data-ttu-id="147f2-179">Plug Olá outra extremidade do cabo USB no seu computador.</span><span class="sxs-lookup"><span data-stu-id="147f2-179">Plug hello other end of USB cable into your computer.</span></span>

   ![Computador USB](media/iot-hub-intel-edison-kit-c-get-started/11_computer_usb.jpg)

4. <span data-ttu-id="147f2-181">Ficará a saber o que a placa é completamente inicializada quando o computador monta uma nova unidade (muito semelhante a inserir um cartão SD, no seu computador).</span><span class="sxs-lookup"><span data-stu-id="147f2-181">You will know that your board is fully initialized when your computer mounts a new drive (much like inserting a SD card into your computer).</span></span>

## <a name="download-and-run-hello-configuration-tool"></a><span data-ttu-id="147f2-182">Transfira e execute a ferramenta de configuração de Olá</span><span class="sxs-lookup"><span data-stu-id="147f2-182">Download and run hello configuration tool</span></span>
<span data-ttu-id="147f2-183">Obter a ferramenta configuração mais recente Olá do [esta ligação](https://software.intel.com/en-us/iot/hardware/edison/downloads) listados na Olá `Installers` cabeçalho.</span><span class="sxs-lookup"><span data-stu-id="147f2-183">Get hello latest configuration tool from [this link](https://software.intel.com/en-us/iot/hardware/edison/downloads) listed under hello `Installers` heading.</span></span> <span data-ttu-id="147f2-184">Executar a ferramenta de Olá e siga o ecrã instruções, clicar em seguinte, quando necessário</span><span class="sxs-lookup"><span data-stu-id="147f2-184">Execute hello tool and follow its on-screen instructions, clicking Next where needed</span></span>

### <a name="flash-firmware"></a><span data-ttu-id="147f2-185">Flash firmware</span><span class="sxs-lookup"><span data-stu-id="147f2-185">Flash firmware</span></span>
1. <span data-ttu-id="147f2-186">No Olá `Set up options` página, clique em `Flash Firmware`.</span><span class="sxs-lookup"><span data-stu-id="147f2-186">On hello `Set up options` page, click `Flash Firmware`.</span></span>
2. <span data-ttu-id="147f2-187">Selecione Olá tooflash de imagem no seu painel efetuando um dos seguintes Olá:</span><span class="sxs-lookup"><span data-stu-id="147f2-187">Select hello image tooflash onto your board by doing one of hello following:</span></span>
   - <span data-ttu-id="147f2-188">toodownload e flash seu painel com Olá mais recente firmware imagem disponível a partir da Intel, selecione `Download hello latest image version xxxx`.</span><span class="sxs-lookup"><span data-stu-id="147f2-188">toodownload and flash your board with hello latest firmware image available from Intel, select `Download hello latest image version xxxx`.</span></span>
   - <span data-ttu-id="147f2-189">Selecione a placa com uma imagem já tiver guardado no seu computador, de tooflash `Select hello local image`.</span><span class="sxs-lookup"><span data-stu-id="147f2-189">tooflash your board with an image you already have saved on your computer, select `Select hello local image`.</span></span> <span data-ttu-id="147f2-190">Procure a imagem de Olá selecione tooand pretende tooflash tooyour quadro.</span><span class="sxs-lookup"><span data-stu-id="147f2-190">Browse tooand select hello image you want tooflash tooyour board.</span></span>
3. <span data-ttu-id="147f2-191">ferramenta de configuração de Olá tentará tooflash seu painel.</span><span class="sxs-lookup"><span data-stu-id="147f2-191">hello setup tool will attempt tooflash your board.</span></span> <span data-ttu-id="147f2-192">processo de intermitente completo Olá pode demorar até too10 minutos.</span><span class="sxs-lookup"><span data-stu-id="147f2-192">hello entire flashing process may take up too10 minutes.</span></span>

### <a name="set-password"></a><span data-ttu-id="147f2-193">Definir palavra-passe</span><span class="sxs-lookup"><span data-stu-id="147f2-193">Set password</span></span>
1. <span data-ttu-id="147f2-194">No Olá `Set up options` página, clique em `Enable Security`.</span><span class="sxs-lookup"><span data-stu-id="147f2-194">On hello `Set up options` page, click `Enable Security`.</span></span>
2. <span data-ttu-id="147f2-195">Pode definir um nome personalizado para o seu painel Intel Edison de®.</span><span class="sxs-lookup"><span data-stu-id="147f2-195">You can set a custom name for your Intel® Edison board.</span></span> <span data-ttu-id="147f2-196">Isto é opcional.</span><span class="sxs-lookup"><span data-stu-id="147f2-196">This is optional.</span></span>
3. <span data-ttu-id="147f2-197">Escreva uma palavra-passe para a placa, em seguida, clique em `Set password`.</span><span class="sxs-lookup"><span data-stu-id="147f2-197">Type a password for your board, then click `Set password`.</span></span>
4. <span data-ttu-id="147f2-198">Marcar para baixo Olá palavra-passe, que é utilizado mais tarde.</span><span class="sxs-lookup"><span data-stu-id="147f2-198">Mark down hello password, which is used later.</span></span>

### <a name="connect-wi-fi"></a><span data-ttu-id="147f2-199">Estabelecer a ligação Wi-Fi</span><span class="sxs-lookup"><span data-stu-id="147f2-199">Connect Wi-Fi</span></span>
1. <span data-ttu-id="147f2-200">No Olá `Set up options` página, clique em `Connect Wi-Fi`.</span><span class="sxs-lookup"><span data-stu-id="147f2-200">On hello `Set up options` page, click `Connect Wi-Fi`.</span></span> <span data-ttu-id="147f2-201">Aguarde pela cópia de segurança tooone minuto, como as análises de computador para redes Wi-Fi disponíveis.</span><span class="sxs-lookup"><span data-stu-id="147f2-201">Wait up tooone minute as your computer scans for available Wi-Fi networks.</span></span>
2. <span data-ttu-id="147f2-202">De Olá `Detected Networks` pendente lista, selecione a sua rede.</span><span class="sxs-lookup"><span data-stu-id="147f2-202">From hello `Detected Networks` drop-down list, select your network.</span></span>
3. <span data-ttu-id="147f2-203">De Olá `Security` na lista pendente, tipo de segurança da rede Olá selecione.</span><span class="sxs-lookup"><span data-stu-id="147f2-203">From hello `Security` drop-down list, select hello network's security type.</span></span>
4. <span data-ttu-id="147f2-204">Indique as informações de início de sessão e palavra-passe e clique em `Configure Wi-Fi`.</span><span class="sxs-lookup"><span data-stu-id="147f2-204">Provide your login and password information, then click `Configure Wi-Fi`.</span></span>
5. <span data-ttu-id="147f2-205">Marcar para baixo Olá endereço IP, que é utilizado mais tarde.</span><span class="sxs-lookup"><span data-stu-id="147f2-205">Mark down hello IP address, which is used later.</span></span>

> [!NOTE]
> <span data-ttu-id="147f2-206">Certifique-se que Edison toohello ligado, mesmo que o computador de rede.</span><span class="sxs-lookup"><span data-stu-id="147f2-206">Make sure that Edison is connected toohello same network as your computer.</span></span> <span data-ttu-id="147f2-207">O computador liga-se tooyour Edison através do endereço IP Olá.</span><span class="sxs-lookup"><span data-stu-id="147f2-207">Your computer connects tooyour Edison by using hello IP address.</span></span>

   ![Ligar tootemperature sensor](media/iot-hub-intel-edison-kit-c-get-started/12_configuration_tool.png)

<span data-ttu-id="147f2-209">Parabéns!</span><span class="sxs-lookup"><span data-stu-id="147f2-209">Congratulations!</span></span> <span data-ttu-id="147f2-210">Configurou com êxito Edison.</span><span class="sxs-lookup"><span data-stu-id="147f2-210">You've successfully configured Edison.</span></span>

## <a name="run-a-sample-application-on-intel-edison"></a><span data-ttu-id="147f2-211">Executar uma aplicação de exemplo no Intel Edison</span><span class="sxs-lookup"><span data-stu-id="147f2-211">Run a sample application on Intel Edison</span></span>

### <a name="prepare-hello-azure-iot-device-sdk"></a><span data-ttu-id="147f2-212">Preparar Olá SDK de dispositivos do IoT do Azure</span><span class="sxs-lookup"><span data-stu-id="147f2-212">Prepare hello Azure IoT Device SDK</span></span>

1. <span data-ttu-id="147f2-213">Utilize um dos seguintes clientes SSH do seu tooyour de tooconnect do computador anfitrião Intel Edison de Olá.</span><span class="sxs-lookup"><span data-stu-id="147f2-213">Use one of hello following SSH clients from your host computer tooconnect tooyour Intel Edison.</span></span> <span data-ttu-id="147f2-214">endereço IP Olá é da ferramenta de configuração de Olá e palavra-passe de Olá é Olá um que definiu essa ferramenta.</span><span class="sxs-lookup"><span data-stu-id="147f2-214">hello IP address is from hello configuration tool and hello password is hello one you've set in that tool.</span></span>
    - <span data-ttu-id="147f2-215">[PuTTY](http://www.putty.org/) para Windows.</span><span class="sxs-lookup"><span data-stu-id="147f2-215">[PuTTY](http://www.putty.org/) for Windows.</span></span>
    - <span data-ttu-id="147f2-216">Olá SSH no cliente incorporado Ubuntu ou macOS (executar `ssh root@"hello IP address"`).</span><span class="sxs-lookup"><span data-stu-id="147f2-216">hello built-in SSH client on Ubuntu or macOS (run `ssh root@"hello IP address"`).</span></span>

2. <span data-ttu-id="147f2-217">Clone Olá exemplo aplicação tooyour dispositivo cliente.</span><span class="sxs-lookup"><span data-stu-id="147f2-217">Clone hello sample client app tooyour device.</span></span> 
   
   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-c-intel-edison-client-app.git
   ```

3. <span data-ttu-id="147f2-218">Em seguida, navegue Olá toorun toohello repositório pasta os seguintes comandos toobuild SDK IoT do Azure</span><span class="sxs-lookup"><span data-stu-id="147f2-218">Then navigate toohello repo folder toorun hello following command toobuild Azure IoT SDK</span></span>

   ```bash
   cd iot-hub-c-intel-edison-client-app
   sed -i -e 's/\r$//' buildSDK.sh
   chmod 755 buildSDK.sh
   ./buildSDK.sh
   ```

### <a name="configure-hello-sample-application"></a><span data-ttu-id="147f2-219">Configurar a aplicação de exemplo de Olá</span><span class="sxs-lookup"><span data-stu-id="147f2-219">Configure hello sample application</span></span>

1. <span data-ttu-id="147f2-220">Abra o ficheiro de configuração de Olá executando Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="147f2-220">Open hello config file by running hello following commands:</span></span>

   ```bash
   nano config.h
   ```

   ![Ficheiro de configuração](media/iot-hub-intel-edison-kit-c-get-started/13_configure_file.png)

   <span data-ttu-id="147f2-222">Existem dois macros neste ficheiro, pode configurate.</span><span class="sxs-lookup"><span data-stu-id="147f2-222">There are two macros in this file you can configurate.</span></span> <span data-ttu-id="147f2-223">Olá primeiro um é `INTERVAL`, que define o intervalo de tempo de Olá entre duas mensagens que enviam toocloud.</span><span class="sxs-lookup"><span data-stu-id="147f2-223">hello first one is `INTERVAL`, which defines hello time interval between two messages that send toocloud.</span></span> <span data-ttu-id="147f2-224">Olá segunda `SIMULATED_DATA`, que é um valor booleano para se toouse simulated dados de sensores ou não.</span><span class="sxs-lookup"><span data-stu-id="147f2-224">hello second one `SIMULATED_DATA`,which is a Boolean value for whether toouse simulated sensor data or not.</span></span>

   <span data-ttu-id="147f2-225">Se lhe **não tiver sensor Olá**, hello Defina `SIMULATED_DATA` valor demasiado`1` aplicação de exemplo de Olá toomake criar e utilizar dados de sensores simulados.</span><span class="sxs-lookup"><span data-stu-id="147f2-225">If you **don't have hello sensor**, set hello `SIMULATED_DATA` value too`1` toomake hello sample application create and use simulated sensor data.</span></span>

2. <span data-ttu-id="147f2-226">Guarde e saia, premindo O controlo > introduza > X de controlo.</span><span class="sxs-lookup"><span data-stu-id="147f2-226">Save and exit by pressing Control-O > Enter > Control-X.</span></span>

### <a name="build-and-run-hello-sample-application"></a><span data-ttu-id="147f2-227">Compilar e executar a aplicação de exemplo de Olá</span><span class="sxs-lookup"><span data-stu-id="147f2-227">Build and run hello sample application</span></span>

1. <span data-ttu-id="147f2-228">Crie aplicação de exemplo de Olá executando Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="147f2-228">Build hello sample application by running hello following command:</span></span>

   ```bash
   cmake . && make
   ```
   ![Saída de compilação](media/iot-hub-intel-edison-kit-c-get-started/14_build_output.png)

1. <span data-ttu-id="147f2-230">Execute a aplicação de exemplo de Olá executando Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="147f2-230">Run hello sample application by running hello following command:</span></span>

   ```bash
   sudo ./app '<your Azure IoT hub device connection string>'
   ```

   > [!NOTE] 
   <span data-ttu-id="147f2-231">Certifique-se de que copiar-colar a cadeia de ligação de dispositivo de Olá para plicas Olá.</span><span class="sxs-lookup"><span data-stu-id="147f2-231">Make sure you copy-paste hello device connection string into hello single quotes.</span></span>

<span data-ttu-id="147f2-232">Deverá ver a seguinte Olá de saída que mostra Olá sensor dados e Olá mensagens enviadas tooyour IoT hub.</span><span class="sxs-lookup"><span data-stu-id="147f2-232">You should see hello following output that shows hello sensor data and hello messages that are sent tooyour IoT hub.</span></span>

![Saída - dados de sensores enviados a partir do IoT hub do Intel Edison tooyour](media/iot-hub-intel-edison-kit-c-get-started/15_message_sent.png)

## <a name="next-steps"></a><span data-ttu-id="147f2-234">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="147f2-234">Next steps</span></span>

<span data-ttu-id="147f2-235">Executar um dados de sensores de toocollect de aplicação de exemplo e enviá-lo tooyour IoT hub.</span><span class="sxs-lookup"><span data-stu-id="147f2-235">You’ve run a sample application toocollect sensor data and send it tooyour IoT hub.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
