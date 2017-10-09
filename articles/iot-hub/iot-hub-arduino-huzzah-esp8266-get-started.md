---
title: aaaESP8266 toocloud - ligar o Feather HUZZAH ESP8266 tooAzure IoT Hub | Microsoft Docs
description: Saiba como toosetup e ligue-se Adafruit Feather HUZZAH ESP8266 tooAzure IoT Hub para a mesma plataforma de nuvem do Azure toosend dados toohello neste tutorial.
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: 
ms.assetid: c505aacf-89a8-40ed-a853-493b75bec524
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/15/2017
ms.author: xshi
ms.openlocfilehash: 44fd47232488948d21c7aa71bdd865397e41e63e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="connect-adafruit-feather-huzzah-esp8266-tooazure-iot-hub-in-hello-cloud"></a><span data-ttu-id="0b630-103">Ligar Adafruit Feather HUZZAH ESP8266 tooAzure IoT Hub na nuvem de Olá</span><span class="sxs-lookup"><span data-stu-id="0b630-103">Connect Adafruit Feather HUZZAH ESP8266 tooAzure IoT Hub in hello cloud</span></span>

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

![Ligação entre DHT22, Feather HUZZAH ESP8266 e IoT Hub](media/iot-hub-arduino-huzzah-esp8266-get-started/1_connection-hdt22-feather-huzzah-iot-hub.png)

## <a name="what-you-do"></a><span data-ttu-id="0b630-105">O que fazer</span><span class="sxs-lookup"><span data-stu-id="0b630-105">What you do</span></span>


<span data-ttu-id="0b630-106">Ligar Adafruit Feather HUZZAH ESP8266 tooan IoT hub que criou.</span><span class="sxs-lookup"><span data-stu-id="0b630-106">Connect Adafruit Feather HUZZAH ESP8266 tooan IoT hub that you create.</span></span> <span data-ttu-id="0b630-107">Em seguida, executar uma aplicação de exemplo no ESP8266 toocollect Olá relativos à temperatura e humidade dados a partir de um sensor DHT22.</span><span class="sxs-lookup"><span data-stu-id="0b630-107">Then you run a sample application on ESP8266 toocollect hello temperature and humidity data from a DHT22 sensor.</span></span> <span data-ttu-id="0b630-108">Por fim, enviar Olá sensor dados tooyour do IoT hub.</span><span class="sxs-lookup"><span data-stu-id="0b630-108">Finally, you send hello sensor data tooyour IoT hub.</span></span>

> [!NOTE]
> <span data-ttu-id="0b630-109">Se estiver a utilizar outros quadros ESP8266, ainda pode seguir estes passos tooconnect-tooyour IoT hub.</span><span class="sxs-lookup"><span data-stu-id="0b630-109">If you're using other ESP8266 boards, you can still follow these steps tooconnect it tooyour IoT hub.</span></span> <span data-ttu-id="0b630-110">Dependendo do quadro de Olá ESP8266 estiver a utilizar, poderá ter tooreconfigure Olá `LED_PIN`.</span><span class="sxs-lookup"><span data-stu-id="0b630-110">Depending on hello ESP8266 board you're using, you might need tooreconfigure hello `LED_PIN`.</span></span> <span data-ttu-id="0b630-111">Por exemplo, se estiver a utilizar ESP8266 de AI Thinker, poderá alterar a `0` demasiado`2`.</span><span class="sxs-lookup"><span data-stu-id="0b630-111">For example, if you're using ESP8266 from AI-Thinker, you might change it from `0` too`2`.</span></span> <span data-ttu-id="0b630-112">Não tem um kit ainda?</span><span class="sxs-lookup"><span data-stu-id="0b630-112">Don't have a kit yet?</span></span> <span data-ttu-id="0b630-113">Obtido a partir do Olá [Web site Azure](http://azure.com/iotstarterkits).</span><span class="sxs-lookup"><span data-stu-id="0b630-113">Get it from hello [Azure website](http://azure.com/iotstarterkits).</span></span>




## <a name="what-you-learn"></a><span data-ttu-id="0b630-114">O que irá aprender</span><span class="sxs-lookup"><span data-stu-id="0b630-114">What you learn</span></span>

* <span data-ttu-id="0b630-115">Como toocreate um hub IoT e registar um dispositivo para Feather HUZZAH ESP8266</span><span class="sxs-lookup"><span data-stu-id="0b630-115">How toocreate an IoT hub and register a device for Feather HUZZAH ESP8266</span></span>
* <span data-ttu-id="0b630-116">Como tooconnect Feather HUZZAH ESP8266 com sensor Olá e o seu computador</span><span class="sxs-lookup"><span data-stu-id="0b630-116">How tooconnect Feather HUZZAH ESP8266 with hello sensor and your computer</span></span>
* <span data-ttu-id="0b630-117">Como dados de sensores de toocollect ao executar uma aplicação de exemplo no Feather HUZZAH ESP8266</span><span class="sxs-lookup"><span data-stu-id="0b630-117">How toocollect sensor data by running a sample application on Feather HUZZAH ESP8266</span></span>
* <span data-ttu-id="0b630-118">Como toosend hello do IoT hub do sensor dados tooyour</span><span class="sxs-lookup"><span data-stu-id="0b630-118">How toosend hello sensor data tooyour IoT hub</span></span>

## <a name="what-you-need"></a><span data-ttu-id="0b630-119">Do que precisa</span><span class="sxs-lookup"><span data-stu-id="0b630-119">What you need</span></span>

![Componentes necessários para Olá tutorial](media/iot-hub-arduino-huzzah-esp8266-get-started/2_parts-needed-for-the-tutorial.png)

<span data-ttu-id="0b630-121">toocomplete desta operação, terá de Olá seguintes partes do seu Feather HUZZAH ESP8266 Starter Kit:</span><span class="sxs-lookup"><span data-stu-id="0b630-121">toocomplete this operation, you need hello following parts from your Feather HUZZAH ESP8266 Starter Kit:</span></span>

* <span data-ttu-id="0b630-122">Olá Feather HUZZAH ESP8266 placa</span><span class="sxs-lookup"><span data-stu-id="0b630-122">hello Feather HUZZAH ESP8266 board</span></span>
* <span data-ttu-id="0b630-123">Um cabo USB de um de tooType Micro USB</span><span class="sxs-lookup"><span data-stu-id="0b630-123">A Micro USB tooType A USB cable</span></span>

<span data-ttu-id="0b630-124">É também necessário Olá seguintes ações para o seu ambiente de desenvolvimento:</span><span class="sxs-lookup"><span data-stu-id="0b630-124">You also need hello following things for your development environment:</span></span>

* <span data-ttu-id="0b630-125">Uma subscrição ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="0b630-125">An active Azure subscription.</span></span> <span data-ttu-id="0b630-126">Se não tiver uma conta do Azure, [criar uma conta de avaliação gratuita do Azure](https://azure.microsoft.com/free/) em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="0b630-126">If you don't have an Azure account, [create a free Azure trial account](https://azure.microsoft.com/free/) in just a few minutes.</span></span>
* <span data-ttu-id="0b630-127">Mac ou PC com Windows ou Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="0b630-127">Mac or PC that is running Windows or Ubuntu.</span></span>
* <span data-ttu-id="0b630-128">Rede sem fios para Feather HUZZAH ESP8266 tooconnect para.</span><span class="sxs-lookup"><span data-stu-id="0b630-128">Wireless network for Feather HUZZAH ESP8266 tooconnect to.</span></span>
* <span data-ttu-id="0b630-129">Ferramenta de configuração do Internet ligação toodownload Olá.</span><span class="sxs-lookup"><span data-stu-id="0b630-129">Internet connection toodownload hello configuration tool.</span></span>
* <span data-ttu-id="0b630-130">[Arduino IDE](https://www.arduino.cc/en/main/software) versão 1.6.8 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="0b630-130">[Arduino IDE](https://www.arduino.cc/en/main/software) version 1.6.8 or later.</span></span> <span data-ttu-id="0b630-131">Versões anteriores não funcionam com a biblioteca de AzureIoT Olá.</span><span class="sxs-lookup"><span data-stu-id="0b630-131">Earlier versions don't work with hello AzureIoT library.</span></span>

<span data-ttu-id="0b630-132">Olá seguintes itens são opcionais no caso de não ter um sensor.</span><span class="sxs-lookup"><span data-stu-id="0b630-132">hello following items are optional in case you don’t have a sensor.</span></span> <span data-ttu-id="0b630-133">Tem também a opção de Olá da utilização de dados de sensores simulados.</span><span class="sxs-lookup"><span data-stu-id="0b630-133">You also have hello option of using simulated sensor data.</span></span>

* <span data-ttu-id="0b630-134">Um sensor de temperatura e humidade Adafruit DHT22</span><span class="sxs-lookup"><span data-stu-id="0b630-134">An Adafruit DHT22 temperature and humidity sensor</span></span>
* <span data-ttu-id="0b630-135">Um breadboard</span><span class="sxs-lookup"><span data-stu-id="0b630-135">A breadboard</span></span>
* <span data-ttu-id="0b630-136">Cablagem jumper M/M</span><span class="sxs-lookup"><span data-stu-id="0b630-136">M/M jumper wires</span></span>


[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="connect-feather-huzzah-esp8266-with-hello-sensor-and-your-computer"></a><span data-ttu-id="0b630-137">Ligar Feather HUZZAH ESP8266 com sensor Olá e o seu computador</span><span class="sxs-lookup"><span data-stu-id="0b630-137">Connect Feather HUZZAH ESP8266 with hello sensor and your computer</span></span>
<span data-ttu-id="0b630-138">Nesta secção, ligar quadro de tooyour Olá sensores.</span><span class="sxs-lookup"><span data-stu-id="0b630-138">In this section, you connect hello sensors tooyour board.</span></span> <span data-ttu-id="0b630-139">Em seguida, ligue no seu computador tooyour do dispositivo para obter mais utilização.</span><span class="sxs-lookup"><span data-stu-id="0b630-139">Then you plug in your device tooyour computer for further use.</span></span>
### <a name="connect-a-dht22-temperature-and-humidity-sensor-toofeather-huzzah-esp8266"></a><span data-ttu-id="0b630-140">Ligar um DHT22 relativos à temperatura e humidade sensor tooFeather HUZZAH ESP8266</span><span class="sxs-lookup"><span data-stu-id="0b630-140">Connect a DHT22 temperature and humidity sensor tooFeather HUZZAH ESP8266</span></span>

<span data-ttu-id="0b630-141">Utilize Olá breadboard jumper cablagem toomake Olá ligação e como se segue.</span><span class="sxs-lookup"><span data-stu-id="0b630-141">Use hello breadboard and jumper wires toomake hello connection as follows.</span></span> <span data-ttu-id="0b630-142">Se não tiver um sensor, ignore esta secção dado que pode utilizar os dados de sensores simulados em vez disso.</span><span class="sxs-lookup"><span data-stu-id="0b630-142">If you don’t have a sensor, skip this section because you can use simulated sensor data instead.</span></span>

![Referência de ligações](media/iot-hub-arduino-huzzah-esp8266-get-started/15_connections_on_breadboard.png)


<span data-ttu-id="0b630-144">Para sensor pins, utilize Olá wiring os seguintes:</span><span class="sxs-lookup"><span data-stu-id="0b630-144">For sensor pins, use hello following wiring:</span></span>


| <span data-ttu-id="0b630-145">Iniciar (Sensor)</span><span class="sxs-lookup"><span data-stu-id="0b630-145">Start (Sensor)</span></span>           | <span data-ttu-id="0b630-146">Fim (quadro)</span><span class="sxs-lookup"><span data-stu-id="0b630-146">End (Board)</span></span>           | <span data-ttu-id="0b630-147">Cor de cabo</span><span class="sxs-lookup"><span data-stu-id="0b630-147">Cable Color</span></span>   |
| -----------------------  | ---------------------- | ------------: |
| <span data-ttu-id="0b630-148">VDD (Pin 31F)</span><span class="sxs-lookup"><span data-stu-id="0b630-148">VDD (Pin 31F)</span></span>            | <span data-ttu-id="0b630-149">3 v (afixar 58H)</span><span class="sxs-lookup"><span data-stu-id="0b630-149">3V (Pin 58H)</span></span>           | <span data-ttu-id="0b630-150">Cabo vermelho</span><span class="sxs-lookup"><span data-stu-id="0b630-150">Red cable</span></span>     |
| <span data-ttu-id="0b630-151">DADOS de (Pin 32F)</span><span class="sxs-lookup"><span data-stu-id="0b630-151">DATA (Pin 32F)</span></span>           | <span data-ttu-id="0b630-152">GPIO 2 (Pin 46A)</span><span class="sxs-lookup"><span data-stu-id="0b630-152">GPIO 2 (Pin 46A)</span></span>       | <span data-ttu-id="0b630-153">Cabo azul</span><span class="sxs-lookup"><span data-stu-id="0b630-153">Blue cable</span></span>    |
| <span data-ttu-id="0b630-154">GND (Pin 34F)</span><span class="sxs-lookup"><span data-stu-id="0b630-154">GND (Pin 34F)</span></span>            | <span data-ttu-id="0b630-155">GND (PIn 56I)</span><span class="sxs-lookup"><span data-stu-id="0b630-155">GND (PIn 56I)</span></span>          | <span data-ttu-id="0b630-156">Cabo preto</span><span class="sxs-lookup"><span data-stu-id="0b630-156">Black cable</span></span>   |

<span data-ttu-id="0b630-157">Para obter mais informações, consulte [a configuração do sensor Adafruit DHT22](https://learn.adafruit.com/dht/connecting-to-a-dhtxx-sensor) e [Adafruit Feather HUZZAH Esp8266 Pinouts](https://learn.adafruit.com/adafruit-feather-huzzah-esp8266/using-arduino-ide?view=all#pinouts).</span><span class="sxs-lookup"><span data-stu-id="0b630-157">For more information, see [Adafruit DHT22 sensor setup](https://learn.adafruit.com/dht/connecting-to-a-dhtxx-sensor) and [Adafruit Feather HUZZAH Esp8266 Pinouts](https://learn.adafruit.com/adafruit-feather-huzzah-esp8266/using-arduino-ide?view=all#pinouts).</span></span>



<span data-ttu-id="0b630-158">Agora a sua ESP8266 de Huzzah Feather devem estar ligadas com um sensor de trabalho.</span><span class="sxs-lookup"><span data-stu-id="0b630-158">Now your Feather Huzzah ESP8266 should be connected with a working sensor.</span></span>

![Ligar DHT22 com Feather Huzzah](media/iot-hub-arduino-huzzah-esp8266-get-started/8_connect-dht22-feather-huzzah.png)

### <a name="connect-feather-huzzah-esp8266-tooyour-computer"></a><span data-ttu-id="0b630-160">Ligue Feather HUZZAH ESP8266 tooyour computador</span><span class="sxs-lookup"><span data-stu-id="0b630-160">Connect Feather HUZZAH ESP8266 tooyour computer</span></span>

<span data-ttu-id="0b630-161">Como é mostrado seguinte, utilize Olá Micro USB tooType A USB cable tooconnect Feather HUZZAH ESP8266 tooyour computador.</span><span class="sxs-lookup"><span data-stu-id="0b630-161">As shown next, use hello Micro USB tooType A USB cable tooconnect Feather HUZZAH ESP8266 tooyour computer.</span></span>

![Ligue Feather Huzzah tooyour computador](media/iot-hub-arduino-huzzah-esp8266-get-started/9_connect-feather-huzzah-computer.png)

### <a name="add-serial-port-permissions-ubuntu-only"></a><span data-ttu-id="0b630-163">Adicione permissões de porta série (apenas Ubuntu)</span><span class="sxs-lookup"><span data-stu-id="0b630-163">Add serial port permissions (Ubuntu only)</span></span>


<span data-ttu-id="0b630-164">Se utilizar Ubuntu, certifique-se que Olá permissões toooperate no Olá USB porta de Feather HUZZAH ESP8266.</span><span class="sxs-lookup"><span data-stu-id="0b630-164">If you use Ubuntu, make sure you have hello permissions toooperate on hello USB port of Feather HUZZAH ESP8266.</span></span> <span data-ttu-id="0b630-165">permissões de porta série tooadd, siga estes passos:</span><span class="sxs-lookup"><span data-stu-id="0b630-165">tooadd serial port permissions, follow these steps:</span></span>


1. <span data-ttu-id="0b630-166">Execute Olá os seguintes comandos num terminal:</span><span class="sxs-lookup"><span data-stu-id="0b630-166">Run hello following commands at a terminal:</span></span>

   ```bash
   ls -l /dev/ttyUSB*
   ls -l /dev/ttyACM*
   ```

   <span data-ttu-id="0b630-167">Obter um Olá saídas os seguintes:</span><span class="sxs-lookup"><span data-stu-id="0b630-167">You get one of hello following outputs:</span></span>

   * <span data-ttu-id="0b630-168">crw-rw---1 raiz uucp xxxxxxxx</span><span class="sxs-lookup"><span data-stu-id="0b630-168">crw-rw---- 1 root uucp xxxxxxxx</span></span>
   * <span data-ttu-id="0b630-169">crw-rw---1 raiz dialout xxxxxxxx</span><span class="sxs-lookup"><span data-stu-id="0b630-169">crw-rw---- 1 root dialout xxxxxxxx</span></span>

   <span data-ttu-id="0b630-170">No resultado de Olá, repare que `uucp` ou `dialout` é o nome de proprietário do grupo de Olá de Olá porta USB.</span><span class="sxs-lookup"><span data-stu-id="0b630-170">In hello output, notice that `uucp` or `dialout` is hello group owner name of hello USB port.</span></span>

1. <span data-ttu-id="0b630-171">Adicione grupo de toohello de utilizadores de Olá executando Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="0b630-171">Add hello user toohello group by running hello following command:</span></span>

   ```bash
   sudo usermod -a -G <group-owner-name> <username>
   ```

   <span data-ttu-id="0b630-172">`<group-owner-name>`é o nome de proprietário do grupo Olá que obteve no passo anterior Olá.</span><span class="sxs-lookup"><span data-stu-id="0b630-172">`<group-owner-name>` is hello group owner name you obtained in hello previous step.</span></span> <span data-ttu-id="0b630-173">`<username>`é o nome de utilizador Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="0b630-173">`<username>` is your Ubuntu user name.</span></span>

1. <span data-ttu-id="0b630-174">Terminar a sessão do Ubuntu e, em seguida, inicie sessão novamente para Olá alteração tooappear.</span><span class="sxs-lookup"><span data-stu-id="0b630-174">Sign out of Ubuntu, and then sign in again for hello change tooappear.</span></span>

## <a name="collect-sensor-data-and-send-it-tooyour-iot-hub"></a><span data-ttu-id="0b630-175">Recolher dados de sensores e enviá-lo tooyour IoT hub</span><span class="sxs-lookup"><span data-stu-id="0b630-175">Collect sensor data and send it tooyour IoT hub</span></span>

<span data-ttu-id="0b630-176">Nesta secção, implementar e executar uma aplicação de exemplo no Feather HUZZAH ESP8266.</span><span class="sxs-lookup"><span data-stu-id="0b630-176">In this section, you deploy and run a sample application on Feather HUZZAH ESP8266.</span></span> <span data-ttu-id="0b630-177">aplicação de exemplo de Olá fica intermitente Olá LED no Feather HUZZAH ESP8266 e envia temperatura Olá e dados de humidade recolhidos a partir Olá DHT22 sensor tooyour IoT hub.</span><span class="sxs-lookup"><span data-stu-id="0b630-177">hello sample application blinks hello LED on Feather HUZZAH ESP8266, and sends hello temperature and humidity data collected from hello DHT22 sensor tooyour IoT hub.</span></span>

### <a name="get-hello-sample-application-from-github"></a><span data-ttu-id="0b630-178">Obter a aplicação de exemplo de Olá a partir do GitHub</span><span class="sxs-lookup"><span data-stu-id="0b630-178">Get hello sample application from GitHub</span></span>

<span data-ttu-id="0b630-179">aplicação de exemplo de Olá está alojada no GitHub.</span><span class="sxs-lookup"><span data-stu-id="0b630-179">hello sample application is hosted on GitHub.</span></span> <span data-ttu-id="0b630-180">Clone o repositório de exemplo de Olá que contém a aplicação de exemplo de Olá a partir do GitHub.</span><span class="sxs-lookup"><span data-stu-id="0b630-180">Clone hello sample repository that contains hello sample application from GitHub.</span></span> <span data-ttu-id="0b630-181">repositório de exemplo de Olá tooclone, siga estes passos:</span><span class="sxs-lookup"><span data-stu-id="0b630-181">tooclone hello sample repository, follow these steps:</span></span>

1. <span data-ttu-id="0b630-182">Abra uma linha de comandos ou de uma janela de terminal.</span><span class="sxs-lookup"><span data-stu-id="0b630-182">Open a command prompt or a terminal window.</span></span>
1. <span data-ttu-id="0b630-183">Aceda a pasta de tooa onde pretende toobe de aplicação de exemplo de Olá armazenado.</span><span class="sxs-lookup"><span data-stu-id="0b630-183">Go tooa folder where you want hello sample application toobe stored.</span></span>
1. <span data-ttu-id="0b630-184">Execute Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="0b630-184">Run hello following command:</span></span>

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-feather-huzzah-client-app.git
   ```

<span data-ttu-id="0b630-185">Instale o pacote de Olá para Feather HUZZAH ESP8266 no Olá Arduino IDE:</span><span class="sxs-lookup"><span data-stu-id="0b630-185">Install hello package for Feather HUZZAH ESP8266 in hello Arduino IDE:</span></span>

1. <span data-ttu-id="0b630-186">Abra a pasta de olá onde a aplicação de exemplo de Olá está armazenada.</span><span class="sxs-lookup"><span data-stu-id="0b630-186">Open hello folder where hello sample application is stored.</span></span>
1. <span data-ttu-id="0b630-187">Abra o ficheiro de app.ino de Olá na pasta de aplicação Olá no Olá Arduino IDE.</span><span class="sxs-lookup"><span data-stu-id="0b630-187">Open hello app.ino file in hello app folder in hello Arduino IDE.</span></span>

   ![Abra a aplicação de exemplo de Olá no Arduino IDE](media/iot-hub-arduino-huzzah-esp8266-get-started/10_arduino-ide-open-sample-app.png)

1. <span data-ttu-id="0b630-189">No Olá Arduino IDE, clique em **ficheiro** > **preferências**.</span><span class="sxs-lookup"><span data-stu-id="0b630-189">In hello Arduino IDE, click **File** > **Preferences**.</span></span>
1. <span data-ttu-id="0b630-190">No Olá **preferências** caixa de diálogo, clique em Olá ícone seguinte toohello **adicionais URLs de Gestor de quadros** caixa.</span><span class="sxs-lookup"><span data-stu-id="0b630-190">In hello **Preferences** dialog box, click hello icon next toohello **Additional Boards Manager URLs** box.</span></span>
1. <span data-ttu-id="0b630-191">Na janela de pop-up Olá, introduza Olá seguinte URL e, em seguida, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="0b630-191">In hello pop-up window, enter hello following URL, and then click **OK**.</span></span>

   `http://arduino.esp8266.com/stable/package_esp8266com_index.json`

   ![Url do pacote tooa de ponto no Arduino IDE](media/iot-hub-arduino-huzzah-esp8266-get-started/11_arduino-ide-package-url.png)

1. <span data-ttu-id="0b630-193">No Olá **preferência** caixa de diálogo, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="0b630-193">In hello **Preference** dialog box, click **OK**.</span></span>
1. <span data-ttu-id="0b630-194">Clique em **ferramentas** > **quadro** > **quadros Manager**e, em seguida, procure esp8266.</span><span class="sxs-lookup"><span data-stu-id="0b630-194">Click **Tools** > **Board** > **Boards Manager**, and then search for esp8266.</span></span>

   <span data-ttu-id="0b630-195">Gestor de quadros indica que ESP8266 com uma versão do 2.2.0 ou posterior está instalado.</span><span class="sxs-lookup"><span data-stu-id="0b630-195">Boards Manager indicates that ESP8266 with a version of 2.2.0 or later is installed.</span></span>

   ![Olá esp8266 pacote está instalado](media/iot-hub-arduino-huzzah-esp8266-get-started/12_arduino-ide-esp8266-installed.png)

1. <span data-ttu-id="0b630-197">Clique em **ferramentas** > **quadro** > **Adafruit HUZZAH ESP8266**.</span><span class="sxs-lookup"><span data-stu-id="0b630-197">Click **Tools** > **Board** > **Adafruit HUZZAH ESP8266**.</span></span>

### <a name="install-necessary-libraries"></a><span data-ttu-id="0b630-198">Instalar as bibliotecas necessárias</span><span class="sxs-lookup"><span data-stu-id="0b630-198">Install necessary libraries</span></span>

1. <span data-ttu-id="0b630-199">No Olá Arduino IDE, clique em **Sketch** > **incluem bibliotecas** > **gerir bibliotecas**.</span><span class="sxs-lookup"><span data-stu-id="0b630-199">In hello Arduino IDE, click **Sketch** > **Include Library** > **Manage Libraries**.</span></span>
1. <span data-ttu-id="0b630-200">Procure Olá os seguintes nomes de biblioteca um por um.</span><span class="sxs-lookup"><span data-stu-id="0b630-200">Search for hello following library names one by one.</span></span> <span data-ttu-id="0b630-201">Para cada biblioteca que encontrar, clique em **instalar**.</span><span class="sxs-lookup"><span data-stu-id="0b630-201">For each  library that you find, click **Install**.</span></span>
   * `AzureIoTHub`
   * `AzureIoTUtility`
   * `AzureIoTProtocol_MQTT`
   * `ArduinoJson`
   * `DHT sensor library`
   * `Adafruit Unified Sensor`

### <a name="dont-have-a-real-dht22-sensor"></a><span data-ttu-id="0b630-202">Não tem um sensor DHT22 real?</span><span class="sxs-lookup"><span data-stu-id="0b630-202">Don’t have a real DHT22 sensor?</span></span>

<span data-ttu-id="0b630-203">aplicação de exemplo de Olá pode simular dados relativos à temperatura e humidade no caso de não ter um sensor DHT22 real.</span><span class="sxs-lookup"><span data-stu-id="0b630-203">hello sample application can simulate temperature and humidity data in case you don’t have a real DHT22 sensor.</span></span> <span data-ttu-id="0b630-204">tooset Olá exemplo toouse simulated dos dados das aplicações, siga estes passos:</span><span class="sxs-lookup"><span data-stu-id="0b630-204">tooset up hello sample application toouse simulated data, follow these steps:</span></span>

1. <span data-ttu-id="0b630-205">Abra Olá `config.h` ficheiro Olá `app` pasta.</span><span class="sxs-lookup"><span data-stu-id="0b630-205">Open hello `config.h` file in hello `app` folder.</span></span>
1. <span data-ttu-id="0b630-206">Localize Olá seguinte linha de código e altere o valor Olá `false` demasiado`true`:</span><span class="sxs-lookup"><span data-stu-id="0b630-206">Locate hello following line of code and change hello value from `false` too`true`:</span></span>
   ```c
   define SIMULATED_DATA true
   ```
   ![Configurar dados de toouse simulado de aplicação de exemplo de Olá](media/iot-hub-arduino-huzzah-esp8266-get-started/13_arduino-ide-configure-app-use-simulated-data.png)

1. <span data-ttu-id="0b630-208">Guarde o ficheiro de Olá com `Control-s`.</span><span class="sxs-lookup"><span data-stu-id="0b630-208">Save hello file with `Control-s`.</span></span>

### <a name="deploy-hello-sample-application-toofeather-huzzah-esp8266"></a><span data-ttu-id="0b630-209">Implementar tooFeather de aplicação de exemplo de Olá HUZZAH ESP8266</span><span class="sxs-lookup"><span data-stu-id="0b630-209">Deploy hello sample application tooFeather HUZZAH ESP8266</span></span>

1. <span data-ttu-id="0b630-210">No Olá Arduino IDE, clique em **ferramenta** > **porta**e, em seguida, clique em de porta série Olá para Feather HUZZAH ESP8266.</span><span class="sxs-lookup"><span data-stu-id="0b630-210">In hello Arduino IDE, click **Tool** > **Port**, and then click hello serial port for Feather HUZZAH ESP8266.</span></span>
1. <span data-ttu-id="0b630-211">Clique em **Sketch** > **carregar** toobuild e implementar tooFeather de aplicação de exemplo de Olá HUZZAH ESP8266.</span><span class="sxs-lookup"><span data-stu-id="0b630-211">Click **Sketch** > **Upload** toobuild and deploy hello sample application tooFeather HUZZAH ESP8266.</span></span>

### <a name="enter-your-credentials"></a><span data-ttu-id="0b630-212">Introduza as suas credenciais</span><span class="sxs-lookup"><span data-stu-id="0b630-212">Enter your credentials</span></span>

<span data-ttu-id="0b630-213">Após a conclusão do carregamento de Olá com êxito, siga estes passos tooenter as suas credenciais:</span><span class="sxs-lookup"><span data-stu-id="0b630-213">After hello upload completes successfully, follow these steps tooenter your credentials:</span></span>

1. <span data-ttu-id="0b630-214">No Olá Arduino IDE, clique em **ferramentas** > **Monitor série**.</span><span class="sxs-lookup"><span data-stu-id="0b630-214">In hello Arduino IDE, click **Tools** > **Serial Monitor**.</span></span>
1. <span data-ttu-id="0b630-215">Na janela de monitor de série de Olá, tenha em atenção Olá dois na lista pendente no canto inferior direito de Olá.</span><span class="sxs-lookup"><span data-stu-id="0b630-215">In hello serial monitor window, notice hello two drop-down lists in hello lower-right corner.</span></span>
1. <span data-ttu-id="0b630-216">Selecione **terminar nenhuma linha** para Olá esquerdo na lista pendente.</span><span class="sxs-lookup"><span data-stu-id="0b630-216">Select **No line ending** for hello left drop-down list.</span></span>
1. <span data-ttu-id="0b630-217">Selecione **transmissão 115200** para Olá direito na lista pendente.</span><span class="sxs-lookup"><span data-stu-id="0b630-217">Select **115200 baud** for hello right drop-down list.</span></span>
1. <span data-ttu-id="0b630-218">A caixa de entrada Olá localizada em Olá parte superior da janela de monitor de série de Olá, introduza Olá seguintes informações se é-lhe perguntado tooprovide-los e, em seguida, clique em **enviar**.</span><span class="sxs-lookup"><span data-stu-id="0b630-218">In hello input box located at hello top of hello serial monitor window, enter hello following information if you are asked tooprovide them, and then click **Send**.</span></span>
   * <span data-ttu-id="0b630-219">SSID Wi-Fi</span><span class="sxs-lookup"><span data-stu-id="0b630-219">Wi-Fi SSID</span></span>
   * <span data-ttu-id="0b630-220">Palavra-passe de Wi-Fi</span><span class="sxs-lookup"><span data-stu-id="0b630-220">Wi-Fi password</span></span>
   * <span data-ttu-id="0b630-221">Cadeia de ligação do dispositivo</span><span class="sxs-lookup"><span data-stu-id="0b630-221">Device connection string</span></span>

> [!Note]
> <span data-ttu-id="0b630-222">informações de credencial de Olá são armazenadas na Olá EEPROM de Feather HUZZAH ESP8266.</span><span class="sxs-lookup"><span data-stu-id="0b630-222">hello credential information is stored in hello EEPROM of Feather HUZZAH ESP8266.</span></span> <span data-ttu-id="0b630-223">Se clicar no botão de reposição de Olá na Olá Feather HUZZAH ESP8266 placa, a aplicação de exemplo de Olá pergunta se pretende que as informações de Olá tooerase.</span><span class="sxs-lookup"><span data-stu-id="0b630-223">If you click hello reset button on hello Feather HUZZAH ESP8266 board, hello sample application asks if you want tooerase hello information.</span></span> <span data-ttu-id="0b630-224">Introduza `Y` informações de Olá toohave apagadas.</span><span class="sxs-lookup"><span data-stu-id="0b630-224">Enter `Y` toohave hello information erased.</span></span> <span data-ttu-id="0b630-225">É-lhe perguntado informações de Olá tooprovide uma segunda vez.</span><span class="sxs-lookup"><span data-stu-id="0b630-225">You are asked tooprovide hello information a second time.</span></span>

### <a name="verify-hello-sample-application-is-running-successfully"></a><span data-ttu-id="0b630-226">Certifique-se a aplicação de exemplo de Olá é executada com êxito</span><span class="sxs-lookup"><span data-stu-id="0b630-226">Verify hello sample application is running successfully</span></span>

<span data-ttu-id="0b630-227">Se vir seguinte Olá o resultado da janela de monitor de série de Olá e Olá blinking LED no Feather HUZZAH ESP8266, aplicação de exemplo de Olá é executada com êxito.</span><span class="sxs-lookup"><span data-stu-id="0b630-227">If you see hello following output from hello serial monitor window and hello blinking LED on Feather HUZZAH ESP8266, hello sample application is running successfully.</span></span>

![Resultado final no Arduino IDE](media/iot-hub-arduino-huzzah-esp8266-get-started/14_arduino-ide-final-output.png)

## <a name="next-steps"></a><span data-ttu-id="0b630-229">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="0b630-229">Next steps</span></span>

<span data-ttu-id="0b630-230">Com êxito ter ligado um Feather HUZZAH ESP8266 tooyour IoT hub e enviados Olá capturada sensor dados tooyour IoT hub.</span><span class="sxs-lookup"><span data-stu-id="0b630-230">You have successfully connected a Feather HUZZAH ESP8266 tooyour IoT hub, and sent hello captured sensor data tooyour IoT hub.</span></span> 

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]

