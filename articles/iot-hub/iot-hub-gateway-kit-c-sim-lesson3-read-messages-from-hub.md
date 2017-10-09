---
title: 'Simulated dispositivo & Gateway do IoT do Azure - Lesson 3: ler mensagens | Microsoft Docs'
description: "Execute um código de exemplo no seu mensagens hello do anfitrião computador tooread do seu IoT hub."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "dados em nuvem Olá, recolha de dados de nuvem, serviço de nuvem do iot, dados de iot"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 5a6ec9c1-d83c-41c1-beaf-7c0d3395d77f
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 540575724bb5cdac4db581a226d8a02a59004d8c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="read-messages-from-your-iot-hub"></a><span data-ttu-id="a46f9-104">Ler mensagens do seu IoT hub</span><span class="sxs-lookup"><span data-stu-id="a46f9-104">Read messages from your IoT hub</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="a46f9-105">O que irá fazer</span><span class="sxs-lookup"><span data-stu-id="a46f9-105">What you will do</span></span>

- <span data-ttu-id="a46f9-106">Execute o código de exemplo no seu anfitrião mensagens tooread de computador do seu IoT hub.</span><span class="sxs-lookup"><span data-stu-id="a46f9-106">Run sample code on your host computer tooread messages from your IoT hub.</span></span>

<span data-ttu-id="a46f9-107">Se tiver quaisquer problemas, procurar soluções no Olá [resolução de problemas de página](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="a46f9-107">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="a46f9-108">O que aprenderá</span><span class="sxs-lookup"><span data-stu-id="a46f9-108">What you will learn</span></span>

<span data-ttu-id="a46f9-109">Como toouse Olá gulp mensagens de tooread ferramenta do seu IoT hub.</span><span class="sxs-lookup"><span data-stu-id="a46f9-109">How toouse hello gulp tool tooread messages from your IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="a46f9-110">Do que precisa</span><span class="sxs-lookup"><span data-stu-id="a46f9-110">What you need</span></span>

- <span data-ttu-id="a46f9-111">exemplo de dispositivo simulado Olá no [configurar e executar uma nuvem de dispositivo simulado carregar a aplicação de exemplo](iot-hub-gateway-kit-c-sim-lesson3-configure-simulated-device-app.md).</span><span class="sxs-lookup"><span data-stu-id="a46f9-111">hello simulated device sample in [Configure and run a simulated device cloud upload sample application](iot-hub-gateway-kit-c-sim-lesson3-configure-simulated-device-app.md).</span></span>

## <a name="get-your-iot-hub-and-device-connection-strings"></a><span data-ttu-id="a46f9-112">Obter as cadeias de ligação do IoT hub e dispositivos</span><span class="sxs-lookup"><span data-stu-id="a46f9-112">Get your IoT hub and device connection strings</span></span>

<span data-ttu-id="a46f9-113">cadeia de ligação do dispositivo Olá é utilizada pelo seu dispositivo simulado tooconnect tooyour do IoT hub.</span><span class="sxs-lookup"><span data-stu-id="a46f9-113">hello device connection string is used by your simulated device tooconnect tooyour IoT hub.</span></span> <span data-ttu-id="a46f9-114">Olá cadeia de ligação do hub IoT é o registo de identidade toohello tooconnect utilizados nos seus dispositivos Olá do IoT hub toomanage que são permitidos tooconnect tooyour IoT hub.</span><span class="sxs-lookup"><span data-stu-id="a46f9-114">hello IoT hub connection string is used tooconnect toohello identity registry in your IoT hub toomanage hello devices that are allowed tooconnect tooyour IoT hub.</span></span>

- <span data-ttu-id="a46f9-115">Lista todos os os IoT hubs no seu grupo de recursos, executando Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="a46f9-115">List all your IoT hubs in your resource group by running hello following command:</span></span>

   ```bash
   az iot hub list -g iot-gateway --query [].name
   ```

   <span data-ttu-id="a46f9-116">Utilize `iot-gateway` como valor Olá `{resource group name}` se não alterá-la.</span><span class="sxs-lookup"><span data-stu-id="a46f9-116">Use `iot-gateway` as hello value of `{resource group name}` if you didn't change it.</span></span>
- <span data-ttu-id="a46f9-117">Obter a cadeia de ligação do Olá IoT hub executando Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="a46f9-117">Get hello IoT hub connection string by running hello following command:</span></span>

   ```bash
   az iot hub show-connection-string --name {my hub name} -g iot-gateway
   ```

   <span data-ttu-id="a46f9-118">`{my hub name}`é o nome de Olá que especificou no Lesson 2.</span><span class="sxs-lookup"><span data-stu-id="a46f9-118">`{my hub name}` is hello name that you specified in Lesson 2.</span></span>

## <a name="configure-hello-device-connection-for-hello-sample-code"></a><span data-ttu-id="a46f9-119">Configurar a ligação ao dispositivo para o código de exemplo de Olá Olá</span><span class="sxs-lookup"><span data-stu-id="a46f9-119">Configure hello device connection for hello sample code</span></span>

<span data-ttu-id="a46f9-120">Atualizar o IoT hub e o dispositivo de ligação configurações `config-azure.json` efetuando Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="a46f9-120">Update IoT hub and device connection configurations in `config-azure.json` by performing hello following steps:</span></span>

1. <span data-ttu-id="a46f9-121">Abra `config-azure.json` no Visual Studio Code executando Olá seguinte comando numa janela de consola:</span><span class="sxs-lookup"><span data-stu-id="a46f9-121">Open `config-azure.json` in Visual Studio Code by running hello following command in a console window:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-azure.json
   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-azure.json
   ```

2. <span data-ttu-id="a46f9-122">Tornar Olá seguir substituições no Olá `config-azure.json` ficheiro:</span><span class="sxs-lookup"><span data-stu-id="a46f9-122">Make hello following replacements in hello `config-azure.json` file:</span></span>

   ![captura de ecrã da configuração do azure](media/iot-hub-gateway-kit-lessons/lesson3/config_azure.png)

   <span data-ttu-id="a46f9-124">Substitua `[IoT hub connection string]` com Olá cadeia de ligação do IoT hub.</span><span class="sxs-lookup"><span data-stu-id="a46f9-124">Replace `[IoT hub connection string]` with hello IoT hub connection string.</span></span>

## <a name="read-messages-from-your-iot-hub"></a><span data-ttu-id="a46f9-125">Ler mensagens do seu IoT hub</span><span class="sxs-lookup"><span data-stu-id="a46f9-125">Read messages from your IoT hub</span></span>

<span data-ttu-id="a46f9-126">Executar a aplicação de exemplo Olá simulado dispositivo e ler mensagens de IoT Hub por Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="a46f9-126">Run hello simulated device sample application and read IoT Hub messages by hello following command:</span></span>

```bash
gulp run --iot-hub
```

<span data-ttu-id="a46f9-127">comando Olá executa a aplicação de Olá que envia o IoT hub tooyour mensagens cada 2 segundos.</span><span class="sxs-lookup"><span data-stu-id="a46f9-127">hello command runs hello application that sends messages tooyour IoT hub every 2 seconds.</span></span> <span data-ttu-id="a46f9-128">É também cria uma mensagem de saudação do tooreceive de processo subordinado.</span><span class="sxs-lookup"><span data-stu-id="a46f9-128">It also spawns a child process tooreceive hello message.</span></span>

<span data-ttu-id="a46f9-129">mensagens Hello que estão a ser enviadas e recebidos são todos os Olá apresentados de forma instantânea na mesma consola janela no Olá computador anfitrião.</span><span class="sxs-lookup"><span data-stu-id="a46f9-129">hello messages that are being sent and received are all displayed instantly on hello same console window in hello host machine.</span></span> <span data-ttu-id="a46f9-130">aplicação Olá será fechada em segundos, 40.</span><span class="sxs-lookup"><span data-stu-id="a46f9-130">hello application will exit in 40 seconds.</span></span>

![Aplicação de exemplo simulada com mensagens enviadas e recebidas](media/iot-hub-gateway-kit-lessons/lesson3/gulp_run_read_hub_simudev.png)

## <a name="summary"></a><span data-ttu-id="a46f9-132">Resumo</span><span class="sxs-lookup"><span data-stu-id="a46f9-132">Summary</span></span>

<span data-ttu-id="a46f9-133">Que já executou com êxito o Olá exemplo aplicação toosend dados tooyour do IoT hub com o dispositivo simulado.</span><span class="sxs-lookup"><span data-stu-id="a46f9-133">You've successfully run hello sample application toosend data tooyour IoT hub with simulated device.</span></span> <span data-ttu-id="a46f9-134">Também já leu mensagens hello que foram enviadas tooyour IoT hub.</span><span class="sxs-lookup"><span data-stu-id="a46f9-134">You've also read hello messages that have been sent tooyour IoT hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a46f9-135">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="a46f9-135">Next steps</span></span>
[<span data-ttu-id="a46f9-136">Criar uma aplicação de função do Azure e uma Conta de Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="a46f9-136">Create an Azure function app and Azure Storage account</span></span>](iot-hub-gateway-kit-c-sim-lesson4-deploy-resource-manager-template.md)


