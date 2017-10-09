---
title: 'Simulated dispositivo & Gateway do IoT do Azure - Lesson 1: Configurar NUC | Microsoft Docs'
description: "Configurar Intel NUC toowork como um gateway de IoT entre um sensor e informações de sensores de toocollect do IoT Hub do Azure e enviá-lo tooIoT Hub."
services: iot-hub
documentationcenter: 
author: shizn
manager: yjianfeng
tags: 
keywords: gateway de IOT intel nuc, nuc computador, DE3815TYKE
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: f41d6b2e-9b00-40df-90eb-17d824bea883
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: c2146c7cd8ca54adbd0af279364ec8484be1b45b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-intel-nuc-as-an-iot-gateway"></a><span data-ttu-id="238d2-104">Configurar Intel NUC como um gateway de IoT</span><span class="sxs-lookup"><span data-stu-id="238d2-104">Set up Intel NUC as an IoT gateway</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="238d2-105">O que irá fazer</span><span class="sxs-lookup"><span data-stu-id="238d2-105">What you will do</span></span>

- <span data-ttu-id="238d2-106">Configure Intel NUC como um gateway de IoT.</span><span class="sxs-lookup"><span data-stu-id="238d2-106">Set up Intel NUC as an IoT gateway.</span></span>
- <span data-ttu-id="238d2-107">Instale o pacote de limite de IoT do Azure de Olá no Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="238d2-107">Install hello Azure IoT Edge package on Intel NUC.</span></span>
- <span data-ttu-id="238d2-108">Execute uma aplicação de exemplo "hello_world" sobre a funcionalidade de gateway do Intel NUC tooverify Olá.</span><span class="sxs-lookup"><span data-stu-id="238d2-108">Run a "hello_world" sample application on Intel NUC tooverify hello gateway functionality.</span></span>
<span data-ttu-id="238d2-109">Se tiver quaisquer problemas, procurar soluções no Olá [resolução de problemas de página](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="238d2-109">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="238d2-110">O que aprenderá</span><span class="sxs-lookup"><span data-stu-id="238d2-110">What you will learn</span></span>

<span data-ttu-id="238d2-111">Este lesson, irá aprender:</span><span class="sxs-lookup"><span data-stu-id="238d2-111">In this lesson, you will learn:</span></span>

- <span data-ttu-id="238d2-112">Como tooconnect Intel NUC com periféricos.</span><span class="sxs-lookup"><span data-stu-id="238d2-112">How tooconnect Intel NUC with peripherals.</span></span>
- <span data-ttu-id="238d2-113">Como tooinstall e atualização Olá necessário pacotes a utilizar Intel NUC Olá inteligente Gestor de pacotes.</span><span class="sxs-lookup"><span data-stu-id="238d2-113">How tooinstall and update hello required packages on Intel NUC using hello Smart Package Manager.</span></span>
- <span data-ttu-id="238d2-114">Como toorun Olá "hello_world" exemplo funcionalidade de gateway tooverify Olá da aplicação.</span><span class="sxs-lookup"><span data-stu-id="238d2-114">How toorun hello "hello_world" sample application tooverify hello gateway functionality.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="238d2-115">Do que precisa</span><span class="sxs-lookup"><span data-stu-id="238d2-115">What you need</span></span>

- <span data-ttu-id="238d2-116">Um DE3815TYKE do Kit de NUC Intel com Olá Intel IoT Suite de Software do Gateway (Linux vento River * 7.0.0.13) pré-instalado.</span><span class="sxs-lookup"><span data-stu-id="238d2-116">An Intel NUC Kit DE3815TYKE with hello Intel IoT Gateway Software Suite (Wind River Linux *7.0.0.13) preinstalled.</span></span>
- <span data-ttu-id="238d2-117">Um cabo de Ethernet.</span><span class="sxs-lookup"><span data-stu-id="238d2-117">An Ethernet cable.</span></span>
- <span data-ttu-id="238d2-118">Um teclado.</span><span class="sxs-lookup"><span data-stu-id="238d2-118">A keyboard.</span></span>
- <span data-ttu-id="238d2-119">Um cabo HDMI ou VGA.</span><span class="sxs-lookup"><span data-stu-id="238d2-119">An HDMI or VGA cable.</span></span>
- <span data-ttu-id="238d2-120">Monitor com uma porta HDMI ou VGA.</span><span class="sxs-lookup"><span data-stu-id="238d2-120">A monitor with an HDMI or VGA port.</span></span>

![Kit de gateway](media/iot-hub-gateway-kit-lessons/lesson1/kit_without_sensortag.png)

## <a name="connect-intel-nuc-with-hello-peripherals"></a><span data-ttu-id="238d2-122">Ligar Intel NUC com periféricos Olá</span><span class="sxs-lookup"><span data-stu-id="238d2-122">Connect Intel NUC with hello peripherals</span></span>

<span data-ttu-id="238d2-123">imagem de Olá abaixo está um exemplo de NUC Intel que está ligada à periféricos vários:</span><span class="sxs-lookup"><span data-stu-id="238d2-123">hello image below is an example of Intel NUC that is connected with various peripherals:</span></span>

1. <span data-ttu-id="238d2-124">Teclado tooa ligado.</span><span class="sxs-lookup"><span data-stu-id="238d2-124">Connected tooa keyboard.</span></span>
2. <span data-ttu-id="238d2-125">Ligado toohello monitor por um cabo VGA ou um cabo HDMI.</span><span class="sxs-lookup"><span data-stu-id="238d2-125">Connected toohello monitor by a VGA cable or HDMI cable.</span></span>
3. <span data-ttu-id="238d2-126">Ligado tooa rede com fios através de um cabo de Ethernet.</span><span class="sxs-lookup"><span data-stu-id="238d2-126">Connected tooa wired network by an Ethernet cable.</span></span>
4. <span data-ttu-id="238d2-127">Ligado toohello fonte de alimentação com um cabo de energia.</span><span class="sxs-lookup"><span data-stu-id="238d2-127">Connected toohello power supply with a power cable.</span></span>

![Intel NUC ligado tooperipherals](media/iot-hub-gateway-kit-lessons/lesson1/nuc.png)

## <a name="connect-toohello-intel-nuc-system-from-host-computer-via-secure-shell-ssh"></a><span data-ttu-id="238d2-129">Ligar o sistema de Intel NUC toohello do computador anfitrião através de Secure Shell (SSH)</span><span class="sxs-lookup"><span data-stu-id="238d2-129">Connect toohello Intel NUC system from host computer via Secure Shell (SSH)</span></span>

<span data-ttu-id="238d2-130">Aqui tem de teclado e monitor tooget Olá endereço IP do seu dispositivo NUC.</span><span class="sxs-lookup"><span data-stu-id="238d2-130">Here you need keyboard and monitor tooget hello IP address of your NUC device.</span></span> <span data-ttu-id="238d2-131">Se já conhece o IP de Olá endereço, pode ignorar toostep 3 nesta secção.</span><span class="sxs-lookup"><span data-stu-id="238d2-131">If you already know hello IP address, you can skip toostep 3 in this section.</span></span>

1. <span data-ttu-id="238d2-132">Ative o Intel NUC, premindo o botão de energia Olá e registo no sistema Olá.</span><span class="sxs-lookup"><span data-stu-id="238d2-132">Turn on Intel NUC by pressing hello Power button and log in hello system.</span></span>

   <span data-ttu-id="238d2-133">nome de utilizador predefinido Olá e a palavra-passe são ambos `root`.</span><span class="sxs-lookup"><span data-stu-id="238d2-133">hello default user name and password are both `root`.</span></span>

2. <span data-ttu-id="238d2-134">Obtenha o endereço IP Olá NUC executando Olá `ifconfig` comando.</span><span class="sxs-lookup"><span data-stu-id="238d2-134">Get hello IP address of NUC by running hello `ifconfig` command.</span></span> <span data-ttu-id="238d2-135">Este passo é realizado no dispositivo NUC Olá.</span><span class="sxs-lookup"><span data-stu-id="238d2-135">This step is done on hello NUC device.</span></span>

   <span data-ttu-id="238d2-136">Eis um exemplo de saída do comando Olá.</span><span class="sxs-lookup"><span data-stu-id="238d2-136">Here is an example of hello command output.</span></span>

   ![saída de ifconfig Mostrar NUC IP](media/iot-hub-gateway-kit-lessons/lesson1/ifconfig.png)

   <span data-ttu-id="238d2-138">Neste exemplo, Olá valor que se segue `inet addr:` é o endereço IP Olá que necessita quando planeia tooconnect remotamente a partir de um tooIntel do computador anfitrião NUC.</span><span class="sxs-lookup"><span data-stu-id="238d2-138">In this example, hello value that follows `inet addr:` is hello IP address that you need when you plan tooconnect remotely from a host computer tooIntel NUC.</span></span>

3. <span data-ttu-id="238d2-139">Utilize um dos seguintes clientes SSH de tooIntel de tooconnect máquina do anfitrião NUC de Olá.</span><span class="sxs-lookup"><span data-stu-id="238d2-139">Use one of hello following SSH clients from your host machine tooconnect tooIntel NUC.</span></span>

   - <span data-ttu-id="238d2-140">[PuTTY](http://www.putty.org/) para Windows.</span><span class="sxs-lookup"><span data-stu-id="238d2-140">[PuTTY](http://www.putty.org/) for Windows.</span></span>
   - <span data-ttu-id="238d2-141">Olá compilação no cliente SSH no Ubuntu ou macOS.</span><span class="sxs-lookup"><span data-stu-id="238d2-141">hello build-in SSH client on Ubuntu or macOS.</span></span>

   <span data-ttu-id="238d2-142">É mais eficiente e produtiva toooperate no Intel NUC de um computador anfitrião.</span><span class="sxs-lookup"><span data-stu-id="238d2-142">It is more efficient and productive toooperate on Intel NUC from a host computer.</span></span> <span data-ttu-id="238d2-143">Terá de endereço IP de Olá Olá, nome de utilizador e palavra-passe tooconnect Olá NUC através do cliente SSH.</span><span class="sxs-lookup"><span data-stu-id="238d2-143">You need hello hello IP address, user name and password tooconnect hello NUC via SSH client.</span></span> <span data-ttu-id="238d2-144">Segue-se o cliente SSH de utilização de exemplo de Olá no macOS.</span><span class="sxs-lookup"><span data-stu-id="238d2-144">Here is hello example use SSH client on macOS.</span></span>
   <span data-ttu-id="238d2-145">![Cliente SSH em execução no macOS](media/iot-hub-gateway-kit-lessons/lesson1/ssh.png)</span><span class="sxs-lookup"><span data-stu-id="238d2-145">![SSH client running on macOS](media/iot-hub-gateway-kit-lessons/lesson1/ssh.png)</span></span>

## <a name="install-hello-azure-iot-edge-package"></a><span data-ttu-id="238d2-146">Instalar o pacote de limite de IoT do Azure Olá</span><span class="sxs-lookup"><span data-stu-id="238d2-146">Install hello Azure IoT Edge package</span></span>

<span data-ttu-id="238d2-147">pacote de limite de IoT do Azure Olá contém binários previamente compilados Olá Olá SDK e as respetivas dependências.</span><span class="sxs-lookup"><span data-stu-id="238d2-147">hello Azure IoT Edge package contains hello pre-compiled binaries of hello SDK and its dependencies.</span></span> <span data-ttu-id="238d2-148">Estes binários são Azure IoT Edge, Olá SDK do Azure IoT e ferramentas correspondente Olá.</span><span class="sxs-lookup"><span data-stu-id="238d2-148">These binaries are Azure IoT Edge, hello Azure IoT SDK and hello corresponding tools.</span></span> <span data-ttu-id="238d2-149">pacote de Olá também contém uma aplicação de exemplo de "hello_world" que é a funcionalidade de gateway de Olá toovalidate utilizados.</span><span class="sxs-lookup"><span data-stu-id="238d2-149">hello package also contains a "hello_world" sample application that is used toovalidate hello gateway functionality.</span></span> <span data-ttu-id="238d2-150">Limite de IoT faz parte de núcleos de Olá do gateway de Olá.</span><span class="sxs-lookup"><span data-stu-id="238d2-150">IoT Edge is hello core part of hello gateway.</span></span> <span data-ttu-id="238d2-151">Olá tooinstall do pacote, siga estes passos:</span><span class="sxs-lookup"><span data-stu-id="238d2-151">tooinstall hello package, follow these steps:</span></span>

1. <span data-ttu-id="238d2-152">Adicione o repositório de nuvem do IoT Olá executando Olá os seguintes comandos numa janela de terminal:</span><span class="sxs-lookup"><span data-stu-id="238d2-152">Add hello IoT cloud repository by running hello following commands in a terminal window:</span></span>

   ```bash
   rpm --import http://iotdk.intel.com/misc/iot_pub.key
   smart channel --add IoT_Cloud type=rpm-md name="IoT_Cloud" baseurl=http://iotdk.intel.com/repos/iot-cloud/wrlinux7/rcpl13/ -y
   ```

   <span data-ttu-id="238d2-153">Olá `rpm` comando importa Olá chave rpm.</span><span class="sxs-lookup"><span data-stu-id="238d2-153">hello `rpm` command imports hello rpm key.</span></span> <span data-ttu-id="238d2-154">Olá `smart channel` comando adiciona rpm Olá canal toohello inteligente Gestor de pacotes.</span><span class="sxs-lookup"><span data-stu-id="238d2-154">hello `smart channel` command adds hello rpm channel toohello Smart Package Manager.</span></span> <span data-ttu-id="238d2-155">Antes de executar Olá `smart update` comando, verá um resultado como abaixo.</span><span class="sxs-lookup"><span data-stu-id="238d2-155">Before you run hello `smart update` command, you see an output like below.</span></span>

   ![rpm e de saída de comandos do canal inteligente](media/iot-hub-gateway-kit-lessons/lesson1/rpm_smart_channel.png)

   ```bash
   smart update
   ```

2. <span data-ttu-id="238d2-157">Instale o pacote de Olá executando Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="238d2-157">Install hello package by running hello following command:</span></span>

   ```bash
   smart install packagegroup-cloud-azure -y
   ```

   <span data-ttu-id="238d2-158">`packagegroup-cloud-azure`é Olá nome do pacote de Olá.</span><span class="sxs-lookup"><span data-stu-id="238d2-158">`packagegroup-cloud-azure` is hello name of hello package.</span></span> <span data-ttu-id="238d2-159">Olá `smart install` comando é o pacote de Olá tooinstall utilizado.</span><span class="sxs-lookup"><span data-stu-id="238d2-159">hello `smart install` command is used tooinstall hello package.</span></span>

   <span data-ttu-id="238d2-160">Após a instalação do pacote de Olá, Intel NUC é esperado toowork como um gateway.</span><span class="sxs-lookup"><span data-stu-id="238d2-160">After hello package is installed, Intel NUC is expected toowork as a gateway.</span></span>

## <a name="run-hello-azure-iot-edge-helloworld-sample-application"></a><span data-ttu-id="238d2-161">Executar a aplicação de exemplo Olá Azure IoT Edge "hello_world"</span><span class="sxs-lookup"><span data-stu-id="238d2-161">Run hello Azure IoT Edge "hello_world" sample application</span></span>

<span data-ttu-id="238d2-162">Aceda demasiado`azureiotgatewaysdk/samples` e execute a aplicação de exemplo Olá exemplo "hello_world".</span><span class="sxs-lookup"><span data-stu-id="238d2-162">Go too`azureiotgatewaysdk/samples` and run hello sample "hello_world" sample application.</span></span> <span data-ttu-id="238d2-163">Esta aplicação de exemplo cria um gateway de Olá `hello_world.json` do ficheiro e utiliza componentes fundamentais do Olá de Olá Azure IoT Edge arquitetura toolog um ficheiro de tooa Olá mundo mensagem a cada cinco segundos.</span><span class="sxs-lookup"><span data-stu-id="238d2-163">This sample application creates a gateway from hello `hello_world.json` file and uses hello fundamental components of hello Azure IoT Edge architecture toolog a hello world message tooa file every 5 seconds.</span></span>

<span data-ttu-id="238d2-164">Pode executar a aplicação de exemplo de "hello_world" de exemplo de Olá executando Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="238d2-164">You can run hello sample "hello_world" sample application by running hello following command:</span></span>

```bash
cd /usr/share/azureiotgatewaysdk/samples/hello_world/
./hello_world hello_world.json
```

<span data-ttu-id="238d2-165">aplicação de exemplo de Olá produz seguinte Olá saída se a funcionalidade de gateway Olá está a funcionar corretamente:</span><span class="sxs-lookup"><span data-stu-id="238d2-165">hello sample application produces hello following output if hello gateway functionality is working correctly:</span></span>

![saída da aplicação](media/iot-hub-gateway-kit-lessons/lesson1/hello_world.png)

<span data-ttu-id="238d2-167">Se tiver quaisquer problemas, procurar soluções no Olá [resolução de problemas de página](iot-hub-gateway-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="238d2-167">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-gateway-kit-c-troubleshooting.md).</span></span>

## <a name="summary"></a><span data-ttu-id="238d2-168">Resumo</span><span class="sxs-lookup"><span data-stu-id="238d2-168">Summary</span></span>

<span data-ttu-id="238d2-169">Parabéns!</span><span class="sxs-lookup"><span data-stu-id="238d2-169">Congratulations!</span></span> <span data-ttu-id="238d2-170">Concluiu a cópia de segurança Intel NUC como um gateway.</span><span class="sxs-lookup"><span data-stu-id="238d2-170">You've finished setting up Intel NUC as a gateway.</span></span> <span data-ttu-id="238d2-171">Agora está pronto toomove no seguinte lesson tooset toohello cópia de segurança do computador anfitrião, criar um hub IoT do Azure e registar o seu dispositivo lógico do Azure IoT hub.</span><span class="sxs-lookup"><span data-stu-id="238d2-171">Now you're ready toomove on toohello next lesson tooset up your host computer, create an Azure IoT hub and register your Azure IoT hub logical device.</span></span>

## <a name="next-steps"></a><span data-ttu-id="238d2-172">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="238d2-172">Next steps</span></span>
[<span data-ttu-id="238d2-173">Preparar o seu computador anfitrião e o hub IoT do Azure</span><span class="sxs-lookup"><span data-stu-id="238d2-173">Get your host computer and Azure IoT hub ready</span></span>](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-win32.md)
