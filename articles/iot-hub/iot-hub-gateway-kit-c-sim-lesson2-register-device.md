---
title: 'Simulated dispositivo & Gateway do IoT do Azure - Lesson 2: registar o dispositivo | Microsoft Docs'
description: 
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: hub iot do Azure, a internet do iot hub do azure, nuvem coisas criar dispositivo, sensortag de ti, var de ti
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 23cfbe21-22c6-4fe1-ae41-63714a897f12
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: d1052ed2fa9e022966e6e71fa2c7d4f18c333b2f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-azure-iot-hub-and-register-your-device"></a><span data-ttu-id="ba4d7-103">Criar o seu hub IoT do Azure e registar o dispositivo</span><span class="sxs-lookup"><span data-stu-id="ba4d7-103">Create your Azure IoT hub and register your device</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="ba4d7-104">O que irá fazer</span><span class="sxs-lookup"><span data-stu-id="ba4d7-104">What you will do</span></span>

- <span data-ttu-id="ba4d7-105">Criar um grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="ba4d7-105">Create a resource group</span></span>
- <span data-ttu-id="ba4d7-106">Criar o seu IoT hub primeiro</span><span class="sxs-lookup"><span data-stu-id="ba4d7-106">Create your first IoT hub</span></span>
- <span data-ttu-id="ba4d7-107">Registe o seu dispositivo no seu IoT hub com Olá CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="ba4d7-107">Register your device in your IoT hub by using hello Azure CLI.</span></span> 

<span data-ttu-id="ba4d7-108">Quando registar o seu dispositivo no seu IoT hub, Olá serviço IoT Hub do Azure gera uma chave para o seu tooauthenticate toouse de dispositivo com o serviço de Olá.</span><span class="sxs-lookup"><span data-stu-id="ba4d7-108">When you register your device in your IoT hub, hello Azure IoT Hub service generates a key for your device toouse tooauthenticate with hello service.</span></span> 

<span data-ttu-id="ba4d7-109">Se tiver quaisquer problemas, procurar soluções no Olá [resolução de problemas de página](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="ba4d7-109">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="ba4d7-110">O que aprenderá</span><span class="sxs-lookup"><span data-stu-id="ba4d7-110">What you will learn</span></span>

<span data-ttu-id="ba4d7-111">Este lesson, irá aprender:</span><span class="sxs-lookup"><span data-stu-id="ba4d7-111">In this lesson, you will learn:</span></span>

- <span data-ttu-id="ba4d7-112">Como toouse Olá CLI do Azure toocreate um IoT hub.</span><span class="sxs-lookup"><span data-stu-id="ba4d7-112">How toouse hello Azure CLI toocreate an IoT hub.</span></span>
- <span data-ttu-id="ba4d7-113">Como tooregister um dispositivo de um hub IoT.</span><span class="sxs-lookup"><span data-stu-id="ba4d7-113">How tooregister a device in an IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="ba4d7-114">Do que precisa</span><span class="sxs-lookup"><span data-stu-id="ba4d7-114">What you need</span></span>

- <span data-ttu-id="ba4d7-115">Uma subscrição ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="ba4d7-115">An active Azure subscription.</span></span> <span data-ttu-id="ba4d7-116">Se não tiver uma conta do Azure, pode criar um [conta de avaliação do Azure gratuita](http://azure.microsoft.com/pricing/free-trial/) em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="ba4d7-116">If you don't have an Azure account, you can create a [free Azure trial account](http://azure.microsoft.com/pricing/free-trial/) in just a few minutes.</span></span>
- <span data-ttu-id="ba4d7-117">É necessário ter Olá instalado da CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="ba4d7-117">You should have hello Azure CLI installed.</span></span>

## <a name="create-an-iot-hub"></a><span data-ttu-id="ba4d7-118">Criar um hub IoT</span><span class="sxs-lookup"><span data-stu-id="ba4d7-118">Create an IoT hub</span></span>

<span data-ttu-id="ba4d7-119">toocreate um IoT hub, siga estes passos:</span><span class="sxs-lookup"><span data-stu-id="ba4d7-119">toocreate an IoT hub, follow these steps:</span></span>

1. <span data-ttu-id="ba4d7-120">Inicie sessão no tooyour conta do Azure executando Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="ba4d7-120">Sign in tooyour Azure account by running hello following command:</span></span>

   ```bash
   az login
   ```

   <span data-ttu-id="ba4d7-121">Todas as subscrições disponíveis serão apresentadas a seguir um bem-sucedida início de sessão.</span><span class="sxs-lookup"><span data-stu-id="ba4d7-121">All your available subscriptions will be listed after a successful sign-in.</span></span>

2. <span data-ttu-id="ba4d7-122">Predefinir Olá subscrição do Azure que pretende que toouse executando Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="ba4d7-122">Set hello default Azure subscription that you want toouse by running hello following command:</span></span>

   ```bash
   az account set --subscription {subscription id or name}
   ```

   <span data-ttu-id="ba4d7-123">`subscription ID or name`podem ser encontrados no resultado Olá Olá `az login` ou Olá `az account list` comando.</span><span class="sxs-lookup"><span data-stu-id="ba4d7-123">`subscription ID or name` can be found in hello output of hello `az login` or hello `az account list` command.</span></span>

3. <span data-ttu-id="ba4d7-124">Registe o fornecedor de Olá Olá os seguintes comandos a executar.</span><span class="sxs-lookup"><span data-stu-id="ba4d7-124">Register hello provider by running hello following command.</span></span> <span data-ttu-id="ba4d7-125">Fornecedores de recursos são serviços que fornece recursos para a sua aplicação.</span><span class="sxs-lookup"><span data-stu-id="ba4d7-125">Resource providers are services that provide resources for your application.</span></span> <span data-ttu-id="ba4d7-126">Tem de registar o fornecedor de Olá antes de poder implementar Olá recursos do Azure que Olá ofertas de fornecedor.</span><span class="sxs-lookup"><span data-stu-id="ba4d7-126">You must register hello provider before you can deploy hello Azure resource that hello provider offers.</span></span>

   ```bash
   az provider register -n "Microsoft.Devices"
   ```

4. <span data-ttu-id="ba4d7-127">Crie um grupo de recursos denominado `iot-gateway` na região de EUA oeste Olá executando Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="ba4d7-127">Create a resource group named `iot-gateway` in hello West US region by running hello following command:</span></span>

   ```bash
   az group create --name iot-gateway --location westus
   ```
   
   <span data-ttu-id="ba4d7-128">`westus`é a localização de Olá criar o grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="ba4d7-128">`westus` is hello location you create your resource group.</span></span> <span data-ttu-id="ba4d7-129">Se pretender que toouse noutra localização, pode executar `az account list-locations -o table` toosee Olá todas as localizações de suporte do Azure.</span><span class="sxs-lookup"><span data-stu-id="ba4d7-129">If you want toouse another location, you can run `az account list-locations -o table` toosee all hello locations Azure supports.</span></span>

5. <span data-ttu-id="ba4d7-130">Criar um hub IoT no Olá `iot-gateway` grupo de recursos, executando Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="ba4d7-130">Create an IoT hub in hello `iot-gateway` resource group by running hello following command:</span></span>

   ```bash
   az iot hub create --name {my hub name} --resource-group iot-gateway
   ```

<span data-ttu-id="ba4d7-131">Por predefinição, a ferramenta de Olá cria um IoT Hub no escalão de preço gratuito Olá.</span><span class="sxs-lookup"><span data-stu-id="ba4d7-131">By default, hello tool creates an IoT Hub in hello Free pricing tier.</span></span> <span data-ttu-id="ba4d7-132">Para obter mais informações, consulte [preços do IoT Hub do Azure](https://azure.microsoft.com/pricing/details/iot-hub/).</span><span class="sxs-lookup"><span data-stu-id="ba4d7-132">For more infomation, see [Azure IoT Hub pricing](https://azure.microsoft.com/pricing/details/iot-hub/).</span></span>

> [!NOTE]
> <span data-ttu-id="ba4d7-133">nome de Olá do seu IoT hub deve ser globalmente exclusivo.</span><span class="sxs-lookup"><span data-stu-id="ba4d7-133">hello name of your IoT hub must be globally unique.</span></span> <span data-ttu-id="ba4d7-134">Pode criar apenas uma edição de F1 do Iot Hub do Azure na sua subscrição do Azure.</span><span class="sxs-lookup"><span data-stu-id="ba4d7-134">You can create only one F1 edition of Azure Iot Hub under your Azure subscription.</span></span>

## <a name="register-your-device-in-your-iot-hub"></a><span data-ttu-id="ba4d7-135">Registar o seu dispositivo no seu IoT hub</span><span class="sxs-lookup"><span data-stu-id="ba4d7-135">Register your device in your IoT hub</span></span>

<span data-ttu-id="ba4d7-136">Cada dispositivo que envia o IoT hub tooyour mensagens e recebe mensagens do seu IoT hub tem de ser registado com um ID exclusivo.</span><span class="sxs-lookup"><span data-stu-id="ba4d7-136">Each device that sends messages tooyour IoT hub and receives messages from your IoT hub must be registered with a unique ID.</span></span>
<span data-ttu-id="ba4d7-137">Registe o seu dispositivo no seu IoT hub ao executar seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="ba4d7-137">Register your device in your IoT hub by running following command:</span></span>

```bash
az iot device create --device-id mydevice --hub-name {my hub name} --resource-group iot-gateway
```

## <a name="summary"></a><span data-ttu-id="ba4d7-138">Resumo</span><span class="sxs-lookup"><span data-stu-id="ba4d7-138">Summary</span></span>

<span data-ttu-id="ba4d7-139">Já criou um IoT hub e registado o dispositivo lógico com uma identidade de dispositivo no seu IoT hub.</span><span class="sxs-lookup"><span data-stu-id="ba4d7-139">You've created an IoT hub and registered your logical device with a device identity in your IoT hub.</span></span> <span data-ttu-id="ba4d7-140">Está pronto toolearn como tooconfigure e executar um gateway exemplo aplicação toosend de dados do seu IoT hub do dispositivo físico tooyour no Olá na nuvem.</span><span class="sxs-lookup"><span data-stu-id="ba4d7-140">You're ready toolearn how tooconfigure and run a gateway sample application toosend data from your physical device tooyour IoT hub in hello cloud.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ba4d7-141">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="ba4d7-141">Next steps</span></span>
[<span data-ttu-id="ba4d7-142">Configurar e executar uma aplicação de exemplo de carregamento do dispositivo simulado na nuvem</span><span class="sxs-lookup"><span data-stu-id="ba4d7-142">Configure and run a simulated device cloud upload sample application</span></span>](iot-hub-gateway-kit-c-sim-lesson3-configure-simulated-device-app.md)