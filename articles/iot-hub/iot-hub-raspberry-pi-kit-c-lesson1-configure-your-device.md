---
title: 'Connect Raspberry PI (C) tooAzure IoT - Lesson 1: configurar o dispositivo | Microsoft Docs'
description: "Configure Raspberry Pi 3 para utilizar primeiro e instale Olá Raspbian SO, um sistema operativo livre que está otimizado para Olá hardware Raspberry Pi."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "instalação raspbian, transferência raspbian, como tooinstall raspbian, raspbian configuração, raspberry pi instalação raspbian, raspberry pi instalação SO, raspberry pi sd cartão instalar, raspberry pi ligar, ligar a conectividade do tooraspberry pi, raspberry pi"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: 8ee9b23c-93f7-43ff-8ea1-e7761eb87a6f
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: ba3466f6d5d46352326a2a63eb011e117da5aca5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-your-device"></a><span data-ttu-id="e68a9-104">Configurar o seu dispositivo</span><span class="sxs-lookup"><span data-stu-id="e68a9-104">Configure your device</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="e68a9-105">O que irá fazer</span><span class="sxs-lookup"><span data-stu-id="e68a9-105">What you will do</span></span>
<span data-ttu-id="e68a9-106">Configurar Pi para utilização da primeira vez e instalar o sistema de operativo Olá Raspbian.</span><span class="sxs-lookup"><span data-stu-id="e68a9-106">Configure Pi for first-time use and install hello Raspbian operating system.</span></span> <span data-ttu-id="e68a9-107">Raspbian é um sistema operativo livre que está otimizado para Olá hardware Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="e68a9-107">Raspbian is a free operating system that is optimized for hello Raspberry Pi hardware.</span></span> <span data-ttu-id="e68a9-108">Se tiver quaisquer problemas, procurar soluções no Olá [resolução de problemas de página](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="e68a9-108">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="e68a9-109">O que aprenderá</span><span class="sxs-lookup"><span data-stu-id="e68a9-109">What you will learn</span></span>
<span data-ttu-id="e68a9-110">Neste artigo, irá aprender:</span><span class="sxs-lookup"><span data-stu-id="e68a9-110">In this article, you will learn:</span></span>

* <span data-ttu-id="e68a9-111">Como tooinstall Raspbian no Pi.</span><span class="sxs-lookup"><span data-stu-id="e68a9-111">How tooinstall Raspbian on Pi.</span></span>
* <span data-ttu-id="e68a9-112">Como toopower segurança Pi utilizando um cabo USB.</span><span class="sxs-lookup"><span data-stu-id="e68a9-112">How toopower up Pi by using a USB cable.</span></span>
* <span data-ttu-id="e68a9-113">Como tooconnect Pi toohello rede utilizando um cabo de Ethernet ou de uma rede sem fios.</span><span class="sxs-lookup"><span data-stu-id="e68a9-113">How tooconnect Pi toohello network by using an Ethernet cable or wireless network.</span></span>
* <span data-ttu-id="e68a9-114">Como tooadd um toohello LED breadboard e ligá-lo tooPi.</span><span class="sxs-lookup"><span data-stu-id="e68a9-114">How tooadd an LED toohello breadboard and connect it tooPi.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="e68a9-115">Do que precisa</span><span class="sxs-lookup"><span data-stu-id="e68a9-115">What you need</span></span>
<span data-ttu-id="e68a9-116">toocomplete desta operação, terá de Olá seguintes partes do seu Raspberry Pi 3 Starter Kit:</span><span class="sxs-lookup"><span data-stu-id="e68a9-116">toocomplete this operation, you need hello following parts from your Raspberry Pi 3 Starter Kit:</span></span>

* <span data-ttu-id="e68a9-117">Olá quadro Raspberry Pi 3</span><span class="sxs-lookup"><span data-stu-id="e68a9-117">hello Raspberry Pi 3 board</span></span>
* <span data-ttu-id="e68a9-118">cartão microSD de 16 GB de Olá</span><span class="sxs-lookup"><span data-stu-id="e68a9-118">hello 16-GB microSD card</span></span>
* <span data-ttu-id="e68a9-119">Olá 5 volt 2 amp fonte de alimentação com o cabo do Olá 6 online micro USB</span><span class="sxs-lookup"><span data-stu-id="e68a9-119">hello 5-volt 2-amp power supply with hello 6-foot micro USB cable</span></span>
* <span data-ttu-id="e68a9-120">breadboard Olá</span><span class="sxs-lookup"><span data-stu-id="e68a9-120">hello breadboard</span></span>
* <span data-ttu-id="e68a9-121">Cablagem de conector</span><span class="sxs-lookup"><span data-stu-id="e68a9-121">Connector wires</span></span>
* <span data-ttu-id="e68a9-122">Um resistor 560 ohm</span><span class="sxs-lookup"><span data-stu-id="e68a9-122">A 560-ohm resistor</span></span>
* <span data-ttu-id="e68a9-123">Um diffused LED de 10 mm</span><span class="sxs-lookup"><span data-stu-id="e68a9-123">A diffused 10-mm LED</span></span>
* <span data-ttu-id="e68a9-124">Olá cabo de Ethernet</span><span class="sxs-lookup"><span data-stu-id="e68a9-124">hello Ethernet cable</span></span>

![Coisas no seu Starter Kit](media/iot-hub-raspberry-pi-lessons/lesson1/starter_kit.jpg)

<span data-ttu-id="e68a9-126">Também tem de ter:</span><span class="sxs-lookup"><span data-stu-id="e68a9-126">You also need:</span></span>

* <span data-ttu-id="e68a9-127">Uma ligação com ou sem fios para Pi tooconnect para.</span><span class="sxs-lookup"><span data-stu-id="e68a9-127">A wired or wireless connection for Pi tooconnect to.</span></span>
* <span data-ttu-id="e68a9-128">Um USB SD adaptador ou mini-SD cartão tooburn Olá SO imagem no cartão microSD de Olá.</span><span class="sxs-lookup"><span data-stu-id="e68a9-128">A USB-SD adapter or mini-SD card tooburn hello OS image onto hello microSD card.</span></span>
* <span data-ttu-id="e68a9-129">Um computador com Windows, Mac ou Linux.</span><span class="sxs-lookup"><span data-stu-id="e68a9-129">A computer running Windows, Mac, or Linux.</span></span> <span data-ttu-id="e68a9-130">computador Olá é utilizado tooinstall Raspbian no cartão microSD de Olá.</span><span class="sxs-lookup"><span data-stu-id="e68a9-130">hello computer is used tooinstall Raspbian on hello microSD card.</span></span>
* <span data-ttu-id="e68a9-131">Um toodownload de ligação de Internet Olá ferramentas necessárias e software.</span><span class="sxs-lookup"><span data-stu-id="e68a9-131">An Internet connection toodownload hello necessary tools and software.</span></span>

## <a name="install-raspbian-on-hello-microsd-card"></a><span data-ttu-id="e68a9-132">Instalar Raspbian no cartão MicroSD de Olá</span><span class="sxs-lookup"><span data-stu-id="e68a9-132">Install Raspbian on hello MicroSD card</span></span>
<span data-ttu-id="e68a9-133">Prepare o cartão microSD de Olá para a instalação da imagem de Raspbian Olá.</span><span class="sxs-lookup"><span data-stu-id="e68a9-133">Prepare hello microSD card for installation of hello Raspbian image.</span></span>

1. <span data-ttu-id="e68a9-134">Transferir Raspbian.</span><span class="sxs-lookup"><span data-stu-id="e68a9-134">Download Raspbian.</span></span>
   1. <span data-ttu-id="e68a9-135">[Transferir](https://www.raspberrypi.org/downloads/raspbian/) ficheiro. zip Olá Raspbian Jessie com Pixel.</span><span class="sxs-lookup"><span data-stu-id="e68a9-135">[Download](https://www.raspberrypi.org/downloads/raspbian/) hello .zip file for Raspbian Jessie with Pixel.</span></span>
   2. <span data-ttu-id="e68a9-136">Extrair Olá Raspbian imagem tooa pasta do computador.</span><span class="sxs-lookup"><span data-stu-id="e68a9-136">Extract hello Raspbian image tooa folder on your computer.</span></span>
2. <span data-ttu-id="e68a9-137">Instale Raspbian toohello microSD cartão.</span><span class="sxs-lookup"><span data-stu-id="e68a9-137">Install Raspbian toohello microSD card.</span></span>
   1. <span data-ttu-id="e68a9-138">[Transferir](https://www.etcher.io) e instalar o utilitário de burner de cartão Olá Etcher SD.</span><span class="sxs-lookup"><span data-stu-id="e68a9-138">[Download](https://www.etcher.io) and install hello Etcher SD card burner utility.</span></span>
   2. <span data-ttu-id="e68a9-139">Execute Etcher e selecione a imagem de Raspbian Olá que extraiu no passo 1.</span><span class="sxs-lookup"><span data-stu-id="e68a9-139">Run Etcher and select hello Raspbian image that you extracted in step 1.</span></span>
   3. <span data-ttu-id="e68a9-140">Selecione a unidade de cartão microSD de Olá.</span><span class="sxs-lookup"><span data-stu-id="e68a9-140">Select hello microSD card drive.</span></span>
      <span data-ttu-id="e68a9-141">Tenha em atenção que Etcher poderá já selecionou correta da unidade Olá.</span><span class="sxs-lookup"><span data-stu-id="e68a9-141">Note that Etcher may have already selected hello correct drive.</span></span>
   4. <span data-ttu-id="e68a9-142">Clique em **Flash** tooinstall Raspbian toohello microSD cartão.</span><span class="sxs-lookup"><span data-stu-id="e68a9-142">Click **Flash** tooinstall Raspbian toohello microSD card.</span></span>
   5. <span data-ttu-id="e68a9-143">Remova o cartão microSD de Olá do seu computador quando a instalação estiver concluída.</span><span class="sxs-lookup"><span data-stu-id="e68a9-143">Remove hello microSD card from your computer when installation is complete.</span></span>
      <span data-ttu-id="e68a9-144">É diretamente cartão de microSD Olá tooremove seguro porque Etcher automaticamente ejects ou unmounts cartão microSD de Olá após a conclusão.</span><span class="sxs-lookup"><span data-stu-id="e68a9-144">It is safe tooremove hello microSD card directly because Etcher automatically ejects or unmounts hello microSD card upon completion.</span></span>
   6. <span data-ttu-id="e68a9-145">Inserir cartão microSD de Olá a Pi.</span><span class="sxs-lookup"><span data-stu-id="e68a9-145">Insert hello microSD card into your Pi.</span></span>

![Inserir o cartão SD do Olá](media/iot-hub-raspberry-pi-lessons/lesson1/insert_sdcard.jpg)

## <a name="turn-on-pi"></a><span data-ttu-id="e68a9-147">Ativar o instalador de plataforma</span><span class="sxs-lookup"><span data-stu-id="e68a9-147">Turn on Pi</span></span>
<span data-ttu-id="e68a9-148">Ative a Pi utilizando o cabo USB micro Olá e fonte de alimentação Olá.</span><span class="sxs-lookup"><span data-stu-id="e68a9-148">Turn on Pi by using hello micro USB cable and hello power supply.</span></span>

![Ativar](media/iot-hub-raspberry-pi-lessons/lesson1/micro_usb_power_on.jpg)

> [!NOTE]
> <span data-ttu-id="e68a9-150">É importante toouse Olá fonte de alimentação no kit de Olá que seja, pelo menos, 2A toomake se de que o seu Raspberry tem suficiente toowork energia corretamente.</span><span class="sxs-lookup"><span data-stu-id="e68a9-150">It is important toouse hello power supply in hello kit that is at least 2A toomake sure that your Raspberry has enough power toowork correctly.</span></span>

## <a name="enable-ssh"></a><span data-ttu-id="e68a9-151">Ativar SSH</span><span class="sxs-lookup"><span data-stu-id="e68a9-151">Enable SSH</span></span>
<span data-ttu-id="e68a9-152">A partir da versão de Novembro de 2016 Olá, Raspbian tem Olá SSH de servidor desativadas por predefinição.</span><span class="sxs-lookup"><span data-stu-id="e68a9-152">As of hello November 2016 release, Raspbian has hello SSH server disabled by default.</span></span> <span data-ttu-id="e68a9-153">Terá de tooenable-lo manualmente.</span><span class="sxs-lookup"><span data-stu-id="e68a9-153">You need tooenable it manually.</span></span> <span data-ttu-id="e68a9-154">Pode consultar toohello [instruções oficiais](https://www.raspberrypi.org/documentation/remote-access/ssh/) ou ligar um monitor e aceda demasiado**preferências -> Raspberry Pi configuração** tooenable SSH.</span><span class="sxs-lookup"><span data-stu-id="e68a9-154">You can refer toohello [official instructions](https://www.raspberrypi.org/documentation/remote-access/ssh/) or connect a monitor and go too**Preferences -> Raspberry Pi Configuration** tooenable SSH.</span></span>

## <a name="connect-raspberry-pi-3-toohello-network"></a><span data-ttu-id="e68a9-155">Ligar a rede de toohello Raspberry Pi 3</span><span class="sxs-lookup"><span data-stu-id="e68a9-155">Connect Raspberry Pi 3 toohello network</span></span>
<span data-ttu-id="e68a9-156">Pode ligar tooa Pi com fios tooa de rede sem fios ou de rede.</span><span class="sxs-lookup"><span data-stu-id="e68a9-156">You can connect Pi tooa wired network or tooa wireless network.</span></span> <span data-ttu-id="e68a9-157">Certifique-se que Pi toohello ligado, mesmo que o computador de rede.</span><span class="sxs-lookup"><span data-stu-id="e68a9-157">Make sure that Pi is connected toohello same network as your computer.</span></span> <span data-ttu-id="e68a9-158">Por exemplo, pode ligar toohello Pi que mesmo comutador a que o computador está ligado à.</span><span class="sxs-lookup"><span data-stu-id="e68a9-158">For example, you can connect Pi toohello same switch that your computer is connected to.</span></span>

### <a name="connect-tooa-wired-network"></a><span data-ttu-id="e68a9-159">Ligar tooa rede com fios</span><span class="sxs-lookup"><span data-stu-id="e68a9-159">Connect tooa wired network</span></span>
<span data-ttu-id="e68a9-160">Utilize Olá Ethernet cabo tooconnect tooyour Pi rede com fios.</span><span class="sxs-lookup"><span data-stu-id="e68a9-160">Use hello Ethernet cable tooconnect Pi tooyour wired network.</span></span> <span data-ttu-id="e68a9-161">Olá dois LEDs no Pi ativassem se Olá ligação for estabelecida.</span><span class="sxs-lookup"><span data-stu-id="e68a9-161">hello two LEDs on Pi turn on if hello connection is established.</span></span>

![Ligar utilizando um cabo de Ethernet](media/iot-hub-raspberry-pi-lessons/lesson1/connect_ethernet.jpg)

### <a name="connect-tooa-wireless-network"></a><span data-ttu-id="e68a9-163">Ligar a rede sem fios tooa</span><span class="sxs-lookup"><span data-stu-id="e68a9-163">Connect tooa wireless network</span></span>
<span data-ttu-id="e68a9-164">Siga Olá [instruções](https://www.raspberrypi.org/learning/software-guide/wifi/) de Olá Raspberry Pi Foundation tooconnect Pi tooyour rede sem fios.</span><span class="sxs-lookup"><span data-stu-id="e68a9-164">Follow hello [instructions](https://www.raspberrypi.org/learning/software-guide/wifi/) from hello Raspberry Pi Foundation tooconnect Pi tooyour wireless network.</span></span> <span data-ttu-id="e68a9-165">Estas instruções requerem toofirst ligar um monitor e um tooPi teclado.</span><span class="sxs-lookup"><span data-stu-id="e68a9-165">These instructions require you toofirst connect a monitor and a keyboard tooPi.</span></span>

## <a name="connect-hello-led-toopi"></a><span data-ttu-id="e68a9-166">Ligar Olá LED tooPi</span><span class="sxs-lookup"><span data-stu-id="e68a9-166">Connect hello LED tooPi</span></span>
<span data-ttu-id="e68a9-167">toocomplete esta tarefa, utilize Olá [breadboard](https://learn.sparkfun.com/tutorials/how-to-use-a-breadboard), Olá cablagem de conector, Olá LED e Olá resistor.</span><span class="sxs-lookup"><span data-stu-id="e68a9-167">toocomplete this task, use hello [breadboard](https://learn.sparkfun.com/tutorials/how-to-use-a-breadboard), hello connector wires, hello LED, and hello resistor.</span></span> <span data-ttu-id="e68a9-168">Ligue-toohello [para fins gerais de entrada/saída](https://www.raspberrypi.org/documentation/usage/gpio/) portas (GPIO) de Pi.</span><span class="sxs-lookup"><span data-stu-id="e68a9-168">Connect them toohello [general-purpose input/output](https://www.raspberrypi.org/documentation/usage/gpio/) (GPIO) ports of Pi.</span></span>

![Breadboard, LED e Resistor](media/iot-hub-raspberry-pi-lessons/lesson1/breadboard_led_resistor.jpg)

1. <span data-ttu-id="e68a9-170">Ligar a parte mais curto do Olá de Olá LED demasiado**GPIO GND (Pin 6)**.</span><span class="sxs-lookup"><span data-stu-id="e68a9-170">Connect hello shorter leg of hello LED too**GPIO GND (Pin 6)**.</span></span>
2. <span data-ttu-id="e68a9-171">Ligar a parte superior do Olá de Olá LED tooone fase de resistor Olá.</span><span class="sxs-lookup"><span data-stu-id="e68a9-171">Connect hello longer leg of hello LED tooone leg of hello resistor.</span></span>
3. <span data-ttu-id="e68a9-172">Ligar Olá outro fase de resistor Olá demasiado**GPIO 4 (Pin 7)**.</span><span class="sxs-lookup"><span data-stu-id="e68a9-172">Connect hello other leg of hello resistor too**GPIO 4 (Pin 7)**.</span></span>

<span data-ttu-id="e68a9-173">Tenha em atenção que polarity Olá LED é importante.</span><span class="sxs-lookup"><span data-stu-id="e68a9-173">Note that hello LED polarity is important.</span></span> <span data-ttu-id="e68a9-174">Esta definição polarity é geralmente conhecida como baixa Active Directory.</span><span class="sxs-lookup"><span data-stu-id="e68a9-174">This polarity setting is commonly known as Active Low.</span></span>

![Pinout](media/iot-hub-raspberry-pi-lessons/lesson1/pinout_breadboard.png)

<span data-ttu-id="e68a9-176">Parabéns!</span><span class="sxs-lookup"><span data-stu-id="e68a9-176">Congratulations!</span></span> <span data-ttu-id="e68a9-177">Configurou com êxito Pi.</span><span class="sxs-lookup"><span data-stu-id="e68a9-177">You've successfully configured Pi.</span></span>

## <a name="summary"></a><span data-ttu-id="e68a9-178">Resumo</span><span class="sxs-lookup"><span data-stu-id="e68a9-178">Summary</span></span>
<span data-ttu-id="e68a9-179">Neste artigo, aprendeu como tooconfigure Pi através da instalação Raspbian, rede de tooa Pi ligação e ligar um tooPi LED.</span><span class="sxs-lookup"><span data-stu-id="e68a9-179">In this article, you’ve learned how tooconfigure Pi by installing Raspbian, connecting Pi tooa network, and connecting an LED tooPi.</span></span> <span data-ttu-id="e68a9-180">Tenha em atenção que Olá que LED ainda não apresentado.</span><span class="sxs-lookup"><span data-stu-id="e68a9-180">Note that hello LED doesn't yet light up.</span></span> <span data-ttu-id="e68a9-181">a tarefa seguinte Olá está ferramentas necessárias do tooinstall Olá e software em preparação para executar uma aplicação de exemplo num Pi.</span><span class="sxs-lookup"><span data-stu-id="e68a9-181">hello next task is tooinstall hello necessary tools and software in preparation for running a sample application on Pi.</span></span>

![Hardware está preparado](media/iot-hub-raspberry-pi-lessons/lesson1/hardware_ready.jpg)

## <a name="next-steps"></a><span data-ttu-id="e68a9-183">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="e68a9-183">Next steps</span></span>
[<span data-ttu-id="e68a9-184">Obtenha as ferramentas de Olá</span><span class="sxs-lookup"><span data-stu-id="e68a9-184">Get hello tools</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-win32.md)

