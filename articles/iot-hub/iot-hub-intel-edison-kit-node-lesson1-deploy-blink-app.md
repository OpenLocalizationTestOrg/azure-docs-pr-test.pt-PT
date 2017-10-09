---
title: "Ligar Intel Edison (nó) tooAzure IoT - Lesson 1: implementar a aplicação | Microsoft Docs"
description: "Clone a aplicação de exemplo C Olá a partir do GitHub e execute gulp toodeploy tooyour esta aplicação quadro Intel Edison. Esta aplicação de exemplo fica intermitente Olá LED ligado toohello quadro cada dois segundos."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "arduino guiado projetos, arduino guiado blink, arduino guiado blink código, arduino blink programa, arduino blink exemplo"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: ed2c21d0-c72c-4ac2-9e70-347e9a0711c0
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: bc03c7e45bd1ba9e9b2c8f2fec70a1be647e96b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-deploy-hello-blink-application"></a><span data-ttu-id="d6626-105">Criar e implementar a aplicação de blink Olá</span><span class="sxs-lookup"><span data-stu-id="d6626-105">Create and deploy hello blink application</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="d6626-106">O que irá fazer</span><span class="sxs-lookup"><span data-stu-id="d6626-106">What you will do</span></span>
<span data-ttu-id="d6626-107">Clone a aplicação de exemplo C Olá a partir do GitHub e utilizar Olá gulp ferramenta toodeploy Olá exemplo aplicação tooIntel Edison.</span><span class="sxs-lookup"><span data-stu-id="d6626-107">Clone hello sample C application from GitHub, and use hello gulp tool toodeploy hello sample application tooIntel Edison.</span></span> <span data-ttu-id="d6626-108">aplicação de exemplo de Olá fica intermitente Olá LED ligado toohello quadro cada dois segundos.</span><span class="sxs-lookup"><span data-stu-id="d6626-108">hello sample application blinks hello LED connected toohello board every two seconds.</span></span> <span data-ttu-id="d6626-109">Se tiver quaisquer problemas, procurar soluções no Olá [resolução de problemas de página][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="d6626-109">If you have any problems, look for solutions on hello [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="d6626-110">O que aprenderá</span><span class="sxs-lookup"><span data-stu-id="d6626-110">What you will learn</span></span>
* <span data-ttu-id="d6626-111">Como toodeploy e execução Olá aplicação de exemplo no Edison.</span><span class="sxs-lookup"><span data-stu-id="d6626-111">How toodeploy and run hello sample application on Edison.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="d6626-112">Do que precisa</span><span class="sxs-lookup"><span data-stu-id="d6626-112">What you need</span></span>
<span data-ttu-id="d6626-113">Tem concluiu com sucesso Olá seguintes operações:</span><span class="sxs-lookup"><span data-stu-id="d6626-113">You must have successfully completed hello following operations:</span></span>

* <span data-ttu-id="d6626-114">[Configurar o dispositivo][configure-your-device]</span><span class="sxs-lookup"><span data-stu-id="d6626-114">[Configure your device][configure-your-device]</span></span>
* <span data-ttu-id="d6626-115">[Obtenha as ferramentas de Olá][get-the-tools]</span><span class="sxs-lookup"><span data-stu-id="d6626-115">[Get hello tools][get-the-tools]</span></span>

## <a name="open-hello-sample-application"></a><span data-ttu-id="d6626-116">Aplicação de exemplo de Olá aberta</span><span class="sxs-lookup"><span data-stu-id="d6626-116">Open hello sample application</span></span>
<span data-ttu-id="d6626-117">Olá tooopen aplicação de exemplo, siga estes passos:</span><span class="sxs-lookup"><span data-stu-id="d6626-117">tooopen hello sample application, follow these steps:</span></span>

1. <span data-ttu-id="d6626-118">Clone o repositório de exemplo de Olá a partir do GitHub executando Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="d6626-118">Clone hello sample repository from GitHub by running hello following command:</span></span>

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-node-edison-getting-started.git
   ```
2. <span data-ttu-id="d6626-119">Abra a aplicação de exemplo de Olá no Visual Studio Code executando Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="d6626-119">Open hello sample application in Visual Studio Code by running hello following commands:</span></span>

   ```bash
   cd iot-hub-node-edison-getting-started
   cd Lesson1
   code .
   ```

   ![Estrutura do repositório][repo-structure]

<span data-ttu-id="d6626-121">ficheiro Olá Olá `app` subpasta é o ficheiro de origem da chave de Olá que contém Olá código toocontrol Olá LED.</span><span class="sxs-lookup"><span data-stu-id="d6626-121">hello file in hello `app` subfolder is hello key source file that contains hello code toocontrol hello LED.</span></span>

### <a name="install-application-dependencies"></a><span data-ttu-id="d6626-122">Instale as dependências da aplicação</span><span class="sxs-lookup"><span data-stu-id="d6626-122">Install application dependencies</span></span>
<span data-ttu-id="d6626-123">Instale as bibliotecas de Olá e outros módulos que precisa para a aplicação de exemplo de Olá executando Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="d6626-123">Install hello libraries and other modules you need for hello sample application by running hello following command:</span></span>

```bash
npm install
```

## <a name="configure-hello-device-connection"></a><span data-ttu-id="d6626-124">Configurar a ligação ao dispositivo Olá</span><span class="sxs-lookup"><span data-stu-id="d6626-124">Configure hello device connection</span></span>
<span data-ttu-id="d6626-125">tooconfigure Olá ligação do dispositivo, siga estes passos:</span><span class="sxs-lookup"><span data-stu-id="d6626-125">tooconfigure hello device connection, follow these steps:</span></span>

1. <span data-ttu-id="d6626-126">Gere o ficheiro de configuração de dispositivo Olá executando Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="d6626-126">Generate hello device configuration file by running hello following command:</span></span>

   ```bash
   gulp init
   ```

   <span data-ttu-id="d6626-127">ficheiro de configuração de Olá `config-edison.json` contém credenciais de utilizador de Olá utilize toolog tooEdison.</span><span class="sxs-lookup"><span data-stu-id="d6626-127">hello configuration file `config-edison.json` contains hello user credentials you use toolog in tooEdison.</span></span> <span data-ttu-id="d6626-128">fuga de Olá tooavoid das credenciais do utilizador, o ficheiro de configuração de Olá é gerado na subpasta Olá `.iot-hub-getting-started` da pasta raiz de Olá no seu computador.</span><span class="sxs-lookup"><span data-stu-id="d6626-128">tooavoid hello leak of user credentials, hello configuration file is generated in hello subfolder `.iot-hub-getting-started` of hello home folder on your computer.</span></span>

2. <span data-ttu-id="d6626-129">Abra o ficheiro de configuração de dispositivo Olá no Visual Studio Code executando Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="d6626-129">Open hello device configuration file in Visual Studio Code by running hello following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-edison.json

   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-edison.json
   ```

3. <span data-ttu-id="d6626-130">Substitua o marcador de posição de Olá `[device hostname or IP address]` e `[device password]` com o endereço IP Olá e a palavra-passe que marcado para baixo no lesson anterior.</span><span class="sxs-lookup"><span data-stu-id="d6626-130">Replace hello placeholder `[device hostname or IP address]` and `[device password]` with hello IP address and password that you marked down in previous lesson.</span></span>

   ![Config](media/iot-hub-intel-edison-lessons/lesson1/vscode-config-mac.png)

<span data-ttu-id="d6626-132">Parabéns!</span><span class="sxs-lookup"><span data-stu-id="d6626-132">Congratulations!</span></span> <span data-ttu-id="d6626-133">Criou com êxito Olá primeiro exemplo de aplicação para Edison.</span><span class="sxs-lookup"><span data-stu-id="d6626-133">You've successfully created hello first sample application for Edison.</span></span>

## <a name="deploy-and-run-hello-sample-application"></a><span data-ttu-id="d6626-134">Implementar e executar a aplicação de exemplo de Olá</span><span class="sxs-lookup"><span data-stu-id="d6626-134">Deploy and run hello sample application</span></span>

### <a name="deploy-and-run-hello-sample-app"></a><span data-ttu-id="d6626-135">Implementar e executar a aplicação de exemplo de Olá</span><span class="sxs-lookup"><span data-stu-id="d6626-135">Deploy and run hello sample app</span></span>
<span data-ttu-id="d6626-136">Implementar e executar a aplicação de exemplo de Olá executando Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="d6626-136">Deploy and run hello sample application by running hello following command:</span></span>

```bash
gulp deploy && gulp run
```

### <a name="verify-hello-app-works"></a><span data-ttu-id="d6626-137">Verificar Olá aplicação funciona</span><span class="sxs-lookup"><span data-stu-id="d6626-137">Verify hello app works</span></span>
<span data-ttu-id="d6626-138">aplicação de exemplo de Olá automaticamente termina após Olá LED fica intermitente para 20 vezes.</span><span class="sxs-lookup"><span data-stu-id="d6626-138">hello sample application terminates automatically after hello LED blinks for 20 times.</span></span> <span data-ttu-id="d6626-139">Se não vir Olá LED blinking, consulte Olá [guia de resolução de problemas] [ troubleshooting] para problemas de toocommon soluções.</span><span class="sxs-lookup"><span data-stu-id="d6626-139">If you don’t see hello LED blinking, see hello [troubleshooting guide][troubleshooting] for solutions toocommon problems.</span></span>

![LED blinking][led-blinking]

## <a name="summary"></a><span data-ttu-id="d6626-141">Resumo</span><span class="sxs-lookup"><span data-stu-id="d6626-141">Summary</span></span>
<span data-ttu-id="d6626-142">Ter instalado Olá necessário ferramentas toowork com Edison e implementado um Olá no exemplo aplicação tooEdison tooblink LED.</span><span class="sxs-lookup"><span data-stu-id="d6626-142">You've installed hello required tools toowork with Edison and deployed a sample application tooEdison tooblink hello LED.</span></span> <span data-ttu-id="d6626-143">Agora pode criar, implementar e executar outra aplicação de exemplo que se liga Edison tooAzure toosend do IoT Hub e receber mensagens.</span><span class="sxs-lookup"><span data-stu-id="d6626-143">You can now create, deploy, and run another sample application that connects Edison tooAzure IoT Hub toosend and receive messages.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d6626-144">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="d6626-144">Next steps</span></span>
<span data-ttu-id="d6626-145">[Obter Olá ferramentas do Azure][get-the-azure-tools]</span><span class="sxs-lookup"><span data-stu-id="d6626-145">[Get hello Azure tools][get-the-azure-tools]</span></span>

<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[Configure-your-device]: iot-hub-intel-edison-kit-node-lesson1-configure-your-device.md
[get-the-tools]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-win32.md
[repo-structure]: media/iot-hub-intel-edison-lessons/lesson1/repo_structure.png
[led-blinking]: media/iot-hub-intel-edison-lessons/lesson1/led_blinking.png
[get-the-azure-tools]: iot-hub-intel-edison-kit-node-lesson2-get-azure-tools-win32.md
