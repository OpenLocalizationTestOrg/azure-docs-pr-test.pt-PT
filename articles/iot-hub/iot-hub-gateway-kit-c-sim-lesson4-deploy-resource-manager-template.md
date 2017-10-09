---
title: 'Simulated dispositivo & Gateway do IoT do Azure - Lesson 4: guardar mensagens | Microsoft Docs'
description: "Guardar as mensagens a partir do IoT hub tooyour Intel NUC, escrevê-las tooAzure o Table storage e, em seguida, lê-los a partir da nuvem Olá."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "armazenar dados na nuvem Olá, dados armazenados na nuvem, iot serviço em nuvem"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: ffed0c2e-b092-40e1-9113-8196ec057d67
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 230f2708b62b89c6eed2e238efefc1c4da86e373
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-function-app-and-storage-account"></a><span data-ttu-id="f5894-104">Criar uma aplicação de função do Azure e uma conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="f5894-104">Create an Azure function app and storage account</span></span>

<span data-ttu-id="f5894-105">As funções do Azure é uma solução para uma fácil execução _funções_ (pequenos blocos de código) na nuvem de Olá.</span><span class="sxs-lookup"><span data-stu-id="f5894-105">Azure Functions is a solution for easily running _functions_ (small pieces of code) in hello cloud.</span></span> <span data-ttu-id="f5894-106">Uma aplicação de função do Azure aloja a execução de Olá das suas funções no Azure.</span><span class="sxs-lookup"><span data-stu-id="f5894-106">An Azure function app hosts hello execution of your functions in Azure.</span></span> 

## <a name="what-you-will-do"></a><span data-ttu-id="f5894-107">O que irá fazer</span><span class="sxs-lookup"><span data-stu-id="f5894-107">What you will do</span></span>

- <span data-ttu-id="f5894-108">Utilize um toocreate de modelo Azure Resource Manager, uma aplicação de função do Azure e uma conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="f5894-108">Use an Azure Resource Manager template toocreate an Azure function app and an Azure storage account.</span></span> <span data-ttu-id="f5894-109">aplicação de função do Azure de Olá escuta de eventos do tooAzure IoT hub, processa mensagens a receber e escreve-los tooAzure o Table storage.</span><span class="sxs-lookup"><span data-stu-id="f5894-109">hello Azure function app listens tooAzure IoT hub events, processes incoming messages, and writes them tooAzure Table storage.</span></span>

<span data-ttu-id="f5894-110">Se tiver quaisquer problemas, procurar soluções no Olá [resolução de problemas de página](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="f5894-110">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span></span>


## <a name="what-you-will-learn"></a><span data-ttu-id="f5894-111">O que aprenderá</span><span class="sxs-lookup"><span data-stu-id="f5894-111">What you will learn</span></span>

<span data-ttu-id="f5894-112">Este lesson, irá aprender:</span><span class="sxs-lookup"><span data-stu-id="f5894-112">In this lesson, you will learn:</span></span>

- <span data-ttu-id="f5894-113">Como toouse do Azure Resource Manager toodeploy recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="f5894-113">How toouse Azure Resource Manager toodeploy Azure resources.</span></span>
- <span data-ttu-id="f5894-114">Como toouse do Azure funcionar aplicação tooprocess mensagens do IoT Hub e escrevê-las tooa tabela no Table storage do Azure.</span><span class="sxs-lookup"><span data-stu-id="f5894-114">How toouse an Azure function app tooprocess IoT Hub messages and write them tooa table in Azure Table storage.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="f5894-115">Do que precisa</span><span class="sxs-lookup"><span data-stu-id="f5894-115">What you need</span></span>

<span data-ttu-id="f5894-116">Tem concluiu com sucesso lições anterior Olá:</span><span class="sxs-lookup"><span data-stu-id="f5894-116">You must have successfully completed hello previous lessons:</span></span>

- [<span data-ttu-id="f5894-117">Lesson 1: Configurar o seu NUC Intel como um gateway de IoT</span><span class="sxs-lookup"><span data-stu-id="f5894-117">Lesson 1: Set up your Intel NUC as an IoT gateway</span></span>](iot-hub-gateway-kit-c-sim-lesson1-set-up-nuc.md)
- [<span data-ttu-id="f5894-118">Lesson 2: Preparar o seu computador anfitrião e o hub IoT do Azure</span><span class="sxs-lookup"><span data-stu-id="f5894-118">Lesson 2: Get your host computer and Azure IoT hub ready</span></span>](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-win32.md)
- [<span data-ttu-id="f5894-119">Lesson 3: Receber mensagens do dispositivo simulado Olá e ler mensagens do seu IoT hub</span><span class="sxs-lookup"><span data-stu-id="f5894-119">Lesson 3: Receive messages from hello simulated device and read messages from your IoT hub</span></span>](iot-hub-gateway-kit-c-sim-lesson3-configure-simulated-device-app.md)

## <a name="open-a-sample-app"></a><span data-ttu-id="f5894-120">Abrir uma aplicação de exemplo</span><span class="sxs-lookup"><span data-stu-id="f5894-120">Open a sample app</span></span>

<span data-ttu-id="f5894-121">Aceda tooyour `iot-hub-c-intel-nuc-gateway-getting-started` repositório pasta, ficheiros de configuração de Olá inicializar e projeto de exemplo de Olá, em seguida, abrir no Visual Studio Code executando Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="f5894-121">Go tooyour `iot-hub-c-intel-nuc-gateway-getting-started` repo folder, initialize hello configuration files, and then open hello sample project in Visual Studio Code by running hello following command:</span></span>

```bash
cd Lesson4
npm install
gulp init
code .
```

![Estrutura do repositório](media/iot-hub-gateway-kit-lessons/lesson4/arm_template.png)

- <span data-ttu-id="f5894-123">Olá `arm-template.json` ficheiro é o modelo Azure Resource Manager Olá que contenha uma aplicação de função do Azure e uma conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="f5894-123">hello `arm-template.json` file is hello Azure Resource Manager template that contains an Azure function app and an Azure storage account.</span></span>
- <span data-ttu-id="f5894-124">Olá `arm-template-param.json` ficheiro é o ficheiro de configuração de Olá utilizado pelo modelo do Azure Resource Manager Olá.</span><span class="sxs-lookup"><span data-stu-id="f5894-124">hello `arm-template-param.json` file is hello configuration file used by hello Azure Resource Manager template.</span></span>
- <span data-ttu-id="f5894-125">Olá `ReceiveDeviceMessages` subpasta contém código Node.js Olá Olá função do Azure.</span><span class="sxs-lookup"><span data-stu-id="f5894-125">hello `ReceiveDeviceMessages` subfolder contains hello Node.js code for hello Azure function.</span></span>

## <a name="configure-azure-resource-manager-templates-and-create-resources-in-azure"></a><span data-ttu-id="f5894-126">Configurar modelos Azure Resource Manager e criar recursos no Azure</span><span class="sxs-lookup"><span data-stu-id="f5894-126">Configure Azure Resource Manager templates and create resources in Azure</span></span>

<span data-ttu-id="f5894-127">Olá atualização `arm-template-param.json` ficheiro no Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="f5894-127">Update hello `arm-template-param.json` file in Visual Studio Code.</span></span>

![json de modelo Arm](media/iot-hub-gateway-kit-lessons/lesson4/arm_template_param.png)

- <span data-ttu-id="f5894-129">Substitua `[your IoT Hub name]` com `{my hub name}` que especificou no Lesson 2.</span><span class="sxs-lookup"><span data-stu-id="f5894-129">Replace `[your IoT Hub name]` with `{my hub name}` that you specified in Lesson 2.</span></span>

<span data-ttu-id="f5894-130">Depois de atualizar Olá `arm-template-param.json` de ficheiros, implementar Olá recursos tooAzure executando Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="f5894-130">After you update hello `arm-template-param.json` file, deploy hello resources tooAzure by running hello following command:</span></span>

```bash
az group deployment create --template-file arm-template.json --parameters @arm-template-param.json -g iot-gateway
```

<span data-ttu-id="f5894-131">Utilize `iot-gateway` como valor Olá `{resource group name}` se não tiver a alterar o valor de Olá no Lesson 2.</span><span class="sxs-lookup"><span data-stu-id="f5894-131">Use `iot-gateway` as hello value of `{resource group name}` if you didn't change hello value in Lesson 2.</span></span>

## <a name="summary"></a><span data-ttu-id="f5894-132">Resumo</span><span class="sxs-lookup"><span data-stu-id="f5894-132">Summary</span></span>

<span data-ttu-id="f5894-133">Criou o tooprocess de aplicação de função do Azure mensagens do IoT hub e um armazenamento do Azure conta toostore estas mensagens.</span><span class="sxs-lookup"><span data-stu-id="f5894-133">You've created your Azure function app tooprocess IoT hub messages and an Azure storage account toostore these messages.</span></span> <span data-ttu-id="f5894-134">Agora pode ler as mensagens que são enviadas pelo seu IoT hub do gateway tooyour.</span><span class="sxs-lookup"><span data-stu-id="f5894-134">You can now read messages that are sent by your gateway tooyour IoT hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f5894-135">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="f5894-135">Next steps</span></span>
<span data-ttu-id="f5894-136">[Mensagens de leitura continuada no armazenamento do Azure](iot-hub-gateway-kit-c-sim-lesson4-read-table-storage.md).</span><span class="sxs-lookup"><span data-stu-id="f5894-136">[Read messages persisted in Azure Storage](iot-hub-gateway-kit-c-sim-lesson4-read-table-storage.md).</span></span>
