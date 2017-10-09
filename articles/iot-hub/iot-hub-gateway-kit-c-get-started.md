---
title: "Dispositivos SensorTag & Gateway de IoT do Azure - introdução | Microsoft Docs"
description: "Introdução ao IoT Gateway Starter Kit, criar o seu hub IoT do Azure e ligar SensorTag e Gateway toohello do IoT hub"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "hub iot do Azure, gateway de iot, introdução ao hello internet das coisas, iot toolkit"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 56d05f4e-f2c1-4b22-8701-f01e14deead6
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: d8e4057e7774e43c069dd3f2f2e03f098c1ac844
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-iot-gateway-starter-kit-with-a-sensortag"></a><span data-ttu-id="f8dae-104">Introdução ao IoT Gateway Starter Kit com um SensorTag</span><span class="sxs-lookup"><span data-stu-id="f8dae-104">Get started with IoT Gateway Starter Kit with a SensorTag</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="f8dae-105">SensorTag</span><span class="sxs-lookup"><span data-stu-id="f8dae-105">SensorTag</span></span>](iot-hub-gateway-kit-c-get-started.md)
> * [<span data-ttu-id="f8dae-106">Dispositivo simulado</span><span class="sxs-lookup"><span data-stu-id="f8dae-106">Simulated Device</span></span>](iot-hub-gateway-kit-c-sim-get-started.md)

<span data-ttu-id="f8dae-107">Neste tutorial, começar por learning Olá Noções básicas de trabalhar com [IoT Gateway Starter Kit](https://aka.ms/gateway-kit).</span><span class="sxs-lookup"><span data-stu-id="f8dae-107">In this tutorial, you begin by learning hello basics of working with [IoT Gateway Starter Kit](https://aka.ms/gateway-kit).</span></span> <span data-ttu-id="f8dae-108">Que irá trabalhar com NUC Intel que está a executar Linux vento River e Olá [TI SensorTag](http://www.ti.com/ww/en/wireless_connectivity/sensortag2015/index.html#main).</span><span class="sxs-lookup"><span data-stu-id="f8dae-108">You will be working with Intel NUC that's running Wind River Linux and hello [TI SensorTag](http://www.ti.com/ww/en/wireless_connectivity/sensortag2015/index.html#main).</span></span> <span data-ttu-id="f8dae-109">Ficará a saber como tooseamleesly ligar nuvem toohello dispositivos com o IoT Hub do Azure.</span><span class="sxs-lookup"><span data-stu-id="f8dae-109">You will learn how tooseamleesly connect your devices toohello cloud by using Azure IoT Hub.</span></span>

***
<span data-ttu-id="f8dae-110">**Ainda não tem um kit?:** clique [aqui](https://aka.ms/gateway-kit).</span><span class="sxs-lookup"><span data-stu-id="f8dae-110">**Don't have a kit yet?:** Click [here](https://aka.ms/gateway-kit).</span></span> <span data-ttu-id="f8dae-111">**Não tem um SensorTag?:** [começar com um dispositivo simulado](iot-hub-gateway-kit-c-sim-get-started.md) ou [comprar um SensorTag](http://www.ti.com/ww/en/wireless_connectivity/sensortag2015/?INTC=SensorTag&HQS=sensortag)</span><span class="sxs-lookup"><span data-stu-id="f8dae-111">**Don't have a SensorTag?:** [Start with a simulated device](iot-hub-gateway-kit-c-sim-get-started.md) or [buy a SensorTag](http://www.ti.com/ww/en/wireless_connectivity/sensortag2015/?INTC=SensorTag&HQS=sensortag)</span></span>
***

## <a name="lesson-1-configure-your-nuc"></a><span data-ttu-id="f8dae-112">Lição 1: Configurar o NUC</span><span class="sxs-lookup"><span data-stu-id="f8dae-112">Lesson 1: Configure your NUC</span></span>
![Diagrama de ponto a ponto Lesson1](media/iot-hub-gateway-kit-lessons/e2e-lesson1.png)

<span data-ttu-id="f8dae-114">Este lesson, configurou NUC Intel (seguinte unidade de computação) em Olá Kit como um gateway de IoT do Azure, instalar o pacote de limite de IoT do Azure de Olá no NUC e executar uma funcionalidade de gateway Olá de tooverify de aplicação de exemplo.</span><span class="sxs-lookup"><span data-stu-id="f8dae-114">In this lesson, you set up Intel NUC (Next Unit of Computing) in hello Kit as an Azure IoT gateway, install hello Azure IoT Edge package on NUC, and run a sample app tooverify hello gateway functionality.</span></span>

<span data-ttu-id="f8dae-115">*Estimado tempo toocomplete: 15 minutos*</span><span class="sxs-lookup"><span data-stu-id="f8dae-115">*Estimated time toocomplete: 15 minutes*</span></span>

<span data-ttu-id="f8dae-116">Aceda demasiado[configurar Intel NUC como um gateway de IoT](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md)</span><span class="sxs-lookup"><span data-stu-id="f8dae-116">Go too[Set up Intel NUC as an IoT gateway](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md)</span></span>

## <a name="lesson-2-create-your-iot-hub"></a><span data-ttu-id="f8dae-117">Lição 2: Criar um Hub IoT</span><span class="sxs-lookup"><span data-stu-id="f8dae-117">Lesson 2: Create your IoT Hub</span></span>
![Diagrama de ponto a ponto Lesson2](media/iot-hub-gateway-kit-lessons/e2e-lesson2.png)

<span data-ttu-id="f8dae-119">Este lesson instalou ferramentas Olá e software no computador anfitrião.</span><span class="sxs-lookup"><span data-stu-id="f8dae-119">In this lesson, you install hello tools and software on your host computer.</span></span> <span data-ttu-id="f8dae-120">Em seguida, criar a sua conta gratuita do Azure, aprovisionar o seu hub IoT do Azure e criar o primeiro dispositivo no hub IoT de Olá.</span><span class="sxs-lookup"><span data-stu-id="f8dae-120">Then you create your free Azure account, provision your Azure IoT hub and create your first device in hello IoT hub.</span></span>

<span data-ttu-id="f8dae-121">1 Lesson concluída antes de começar este lesson.</span><span class="sxs-lookup"><span data-stu-id="f8dae-121">Complete Lesson 1 before you start this lesson.</span></span>

### <a name="get-hello-tools"></a><span data-ttu-id="f8dae-122">Obtenha as ferramentas de Olá</span><span class="sxs-lookup"><span data-stu-id="f8dae-122">Get hello tools</span></span>
<span data-ttu-id="f8dae-123">Instale software e ferramentas de Olá no computador anfitrião.</span><span class="sxs-lookup"><span data-stu-id="f8dae-123">Install hello tools and software on your host computer.</span></span>

<span data-ttu-id="f8dae-124">*Estimado tempo toocomplete: 20 minutos*</span><span class="sxs-lookup"><span data-stu-id="f8dae-124">*Estimated time toocomplete: 20 minutes*</span></span>

<span data-ttu-id="f8dae-125">Aceda demasiado[obter ferramentas Olá](iot-hub-gateway-kit-c-lesson2-get-the-tools-win32.md)</span><span class="sxs-lookup"><span data-stu-id="f8dae-125">Go too[Get hello tools](iot-hub-gateway-kit-c-lesson2-get-the-tools-win32.md)</span></span>

### <a name="create-an-iot-hub-and-register-your-device"></a><span data-ttu-id="f8dae-126">Criar um hub IoT e registar o dispositivo</span><span class="sxs-lookup"><span data-stu-id="f8dae-126">Create an IoT hub and register your device</span></span>
<span data-ttu-id="f8dae-127">Criar o grupo de recursos, aprovisionar o seu hub IoT do Azure primeiro e adicionar o primeiro dispositivo toohello IoT hub com Olá CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="f8dae-127">Create your resource group, provision your first Azure IoT hub, and add your first device toohello IoT hub using hello Azure CLI.</span></span>

<span data-ttu-id="f8dae-128">*Estimado tempo toocomplete: 10 minutos*</span><span class="sxs-lookup"><span data-stu-id="f8dae-128">*Estimated time toocomplete: 10 minutes*</span></span>

<span data-ttu-id="f8dae-129">Aceda demasiado[criar um hub IoT e registar o dispositivo](iot-hub-gateway-kit-c-lesson2-register-device.md)</span><span class="sxs-lookup"><span data-stu-id="f8dae-129">Go too[Create an IoT hub and register your device](iot-hub-gateway-kit-c-lesson2-register-device.md)</span></span>

## <a name="lesson-3-receive-messages-from-sensortag-and-read-messages-from-your-iot-hub"></a><span data-ttu-id="f8dae-130">Lesson 3: Receber mensagens de SensorTag e ler mensagens do seu IoT hub</span><span class="sxs-lookup"><span data-stu-id="f8dae-130">Lesson 3: Receive messages from SensorTag and read messages from your IoT hub</span></span>
<span data-ttu-id="f8dae-131">Este lesson, vai utilizar configuração de Olá tooautomate de scripts e a execução de uma aplicação de exemplo var no seu gateway.</span><span class="sxs-lookup"><span data-stu-id="f8dae-131">In this lesson, you will use scripts tooautomate hello configuration and execution of a BLE sample application in your gateway.</span></span> <span data-ttu-id="f8dae-132">Essas aplicações utilizam uma coleção de dados de transformação e tooaggregate de módulos, processam comandos ou efetuar qualquer número de tarefas relacionadas.</span><span class="sxs-lookup"><span data-stu-id="f8dae-132">Such applications use a collection of modules tooaggregate and transform data, process commands, or perform any number of related tasks.</span></span> <span data-ttu-id="f8dae-133">Módulos de comunicam entre si através de um mediador de mensagens.</span><span class="sxs-lookup"><span data-stu-id="f8dae-133">Modules communicate with one another via a message broker.</span></span> <span data-ttu-id="f8dae-134">aplicação de exemplo de Olá tem um módulo de var e um módulo de hub IoT.</span><span class="sxs-lookup"><span data-stu-id="f8dae-134">hello sample application has a BLE module and an IoT hub module.</span></span> <span data-ttu-id="f8dae-135">módulo de var Olá recebe dados de var SensorTag.</span><span class="sxs-lookup"><span data-stu-id="f8dae-135">hello BLE module receives data from BLE SensorTag.</span></span> <span data-ttu-id="f8dae-136">Olá, pacotes de módulo de hub IoT dados Olá receberam e envia-tooyour IoT hub através de arquitetura de gateway Olá fornecido no Azure IoT Edge.</span><span class="sxs-lookup"><span data-stu-id="f8dae-136">hello IoT hub module packages hello data received and sends it tooyour IoT hub through hello gateway framework provided in Azure IoT Edge.</span></span>

![Diagrama de ponto a ponto Lesson 3](media/iot-hub-gateway-kit-lessons/e2e-lesson3.png)

### <a name="configure-and-run-hello-ble-sample-app"></a><span data-ttu-id="f8dae-138">Configurar e executar a aplicação de exemplo Olá var</span><span class="sxs-lookup"><span data-stu-id="f8dae-138">Configure and run hello BLE sample app</span></span>
<span data-ttu-id="f8dae-139">Configure a conectividade de Olá entre SensorTag e o gateway.</span><span class="sxs-lookup"><span data-stu-id="f8dae-139">Set up hello connectivity between SensorTag and your gateway.</span></span> <span data-ttu-id="f8dae-140">Em seguida, Concluir configuração Olá e execute a aplicação de exemplo Olá var.</span><span class="sxs-lookup"><span data-stu-id="f8dae-140">Then finish hello configuration and run hello BLE sample application.</span></span>

<span data-ttu-id="f8dae-141">*Estimado tempo toocomplete: 15 minutos*</span><span class="sxs-lookup"><span data-stu-id="f8dae-141">*Estimated time toocomplete: 15 minutes*</span></span>

<span data-ttu-id="f8dae-142">Aceda demasiado[configurar e executar Olá var aplicação de exemplo](iot-hub-gateway-kit-c-lesson3-configure-ble-app.md)</span><span class="sxs-lookup"><span data-stu-id="f8dae-142">Go too[Configure and run hello BLE sample app](iot-hub-gateway-kit-c-lesson3-configure-ble-app.md)</span></span>

### <a name="read-messages-from-your-iot-hub"></a><span data-ttu-id="f8dae-143">Ler mensagens do seu IoT hub</span><span class="sxs-lookup"><span data-stu-id="f8dae-143">Read messages from your IoT hub</span></span>
<span data-ttu-id="f8dae-144">Execute o código de exemplo no seu anfitrião mensagens tooread de computador do seu IoT hub.</span><span class="sxs-lookup"><span data-stu-id="f8dae-144">Run sample code on your host computer tooread messages from your IoT hub.</span></span>

<span data-ttu-id="f8dae-145">*Estimado tempo toocomplete: 15 minutos*</span><span class="sxs-lookup"><span data-stu-id="f8dae-145">*Estimated time toocomplete: 15 minutes*</span></span>

<span data-ttu-id="f8dae-146">Aceda demasiado[ler mensagens do seu IoT hub](iot-hub-gateway-kit-c-lesson3-read-messages-from-hub.md)</span><span class="sxs-lookup"><span data-stu-id="f8dae-146">Go too[Read messages from your IoT hub](iot-hub-gateway-kit-c-lesson3-read-messages-from-hub.md)</span></span>

## <a name="lesson-4-save-messages-tooazure-table-storage"></a><span data-ttu-id="f8dae-147">Lesson 4: Guardar mensagens tooAzure o Table storage</span><span class="sxs-lookup"><span data-stu-id="f8dae-147">Lesson 4: Save messages tooAzure Table storage</span></span>
<span data-ttu-id="f8dae-148">Crie uma aplicação de função do Azure que obtém mensagens recebidas a partir do seu IoT hub e escreve-los tooAzure o Table storage.</span><span class="sxs-lookup"><span data-stu-id="f8dae-148">Create an Azure function app that gets incoming messages from your IoT hub and writes them tooAzure Table storage.</span></span>

![Diagrama de ponto a ponto Lesson 4](media/iot-hub-gateway-kit-lessons/e2e-lesson4.png)

### <a name="create-an-azure-function-app-and-azure-storage-account"></a><span data-ttu-id="f8dae-150">Criar uma aplicação de função do Azure e a conta de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="f8dae-150">Create an Azure function app and Azure Storage account</span></span>
<span data-ttu-id="f8dae-151">Utilize um toocreate de modelo Azure Resource Manager, uma aplicação de função do Azure e uma conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="f8dae-151">Use an Azure Resource Manager template toocreate an Azure function app and an Azure Storage account.</span></span>

<span data-ttu-id="f8dae-152">*Estimado tempo toocomplete: 10 minutos*</span><span class="sxs-lookup"><span data-stu-id="f8dae-152">*Estimated time toocomplete: 10 minutes*</span></span>

<span data-ttu-id="f8dae-153">Aceda demasiado[criar uma aplicação de função do Azure e a conta de armazenamento do Azure](iot-hub-gateway-kit-c-lesson4-deploy-resource-manager-template.md)</span><span class="sxs-lookup"><span data-stu-id="f8dae-153">Go too[Create an Azure function app and Azure Storage account](iot-hub-gateway-kit-c-lesson4-deploy-resource-manager-template.md)</span></span>

### <a name="read-messages-persisted-in-azure-table-storage"></a><span data-ttu-id="f8dae-154">Mensagens de leitura continuada no armazenamento de tabelas do Azure</span><span class="sxs-lookup"><span data-stu-id="f8dae-154">Read messages persisted in Azure Table storage</span></span>
<span data-ttu-id="f8dae-155">Monitorizar as mensagens hello do gateway para a nuvem, eles são escritas tooAzure o Table storage.</span><span class="sxs-lookup"><span data-stu-id="f8dae-155">Monitor hello gateway-to-cloud messages as they are written tooAzure Table storage.</span></span>

<span data-ttu-id="f8dae-156">*Estimado tempo toocomplete: 5 minutos*</span><span class="sxs-lookup"><span data-stu-id="f8dae-156">*Estimated time toocomplete: 5 minutes*</span></span>

<span data-ttu-id="f8dae-157">Aceda demasiado[mensagens de leitura continuada no armazenamento de Azure Table](iot-hub-gateway-kit-c-lesson4-read-table-storage.md).</span><span class="sxs-lookup"><span data-stu-id="f8dae-157">Go too[Read messages persisted in Azure Table storage](iot-hub-gateway-kit-c-lesson4-read-table-storage.md).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="f8dae-158">Resolução de problemas</span><span class="sxs-lookup"><span data-stu-id="f8dae-158">Troubleshooting</span></span>
<span data-ttu-id="f8dae-159">Se tiver quaisquer problemas durante lições Olá, procurar soluções no Olá [resolução de problemas](iot-hub-gateway-kit-c-troubleshooting.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="f8dae-159">If you have any problems during hello lessons, look for solutions in hello [Troubleshooting](iot-hub-gateway-kit-c-troubleshooting.md) article.</span></span>

## <a name="explore-more"></a><span data-ttu-id="f8dae-160">Explorar mais</span><span class="sxs-lookup"><span data-stu-id="f8dae-160">Explore more</span></span>
<span data-ttu-id="f8dae-161">Visite Olá [zona de programador do Kit de Gateway de IoT Intel](http://software.intel.com/iot/microsoft-azure) toolearn mais.</span><span class="sxs-lookup"><span data-stu-id="f8dae-161">Visit hello [Intel IoT Gateway Kit developer zone](http://software.intel.com/iot/microsoft-azure) toolearn more.</span></span>
