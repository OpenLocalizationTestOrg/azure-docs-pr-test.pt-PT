---
title: 'Ligar Arduino tooAzure IoT - Lesson 2: registar o dispositivo | Microsoft Docs'
description: "Criar um grupo de recursos, criar um hub IoT do Azure e registar Adafruit Feather M0 Wi-Fi no hub IoT do Azure de Olá utilizando Olá CLI do Azure."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: ligar arduino toocloud, hub iot do azure, internet nuvem coisas, dispositivo, nuvem arduino de criar do hub iot do azure
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: 5edc690b-7a1d-4ebc-b011-ff27bfffe6e8
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: ca362f9c143dd3a98bf47a66b63a9725a0ffc2d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-iot-hub-and-register-your-adafruit-feather-m0-wifi-arduino-board"></a><span data-ttu-id="4592b-104">Criar o seu IoT hub e registar o seu painel Adafruit Feather M0 Wi-Fi Arduino</span><span class="sxs-lookup"><span data-stu-id="4592b-104">Create your IoT hub and register your Adafruit Feather M0 WiFi Arduino board</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="4592b-105">O que irá fazer</span><span class="sxs-lookup"><span data-stu-id="4592b-105">What you will do</span></span>
* <span data-ttu-id="4592b-106">Crie um grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="4592b-106">Create a resource group.</span></span>
* <span data-ttu-id="4592b-107">Crie o seu hub IoT do Azure no grupo de recursos de Olá.</span><span class="sxs-lookup"><span data-stu-id="4592b-107">Create your Azure IoT hub in hello resource group.</span></span>
* <span data-ttu-id="4592b-108">Adicione o seu Arduino quadro toohello Azure IoT hub utilizando Olá interface de linha de comandos do Azure (CLI do Azure).</span><span class="sxs-lookup"><span data-stu-id="4592b-108">Add your Arduino board toohello Azure IoT hub by using hello Azure command-line interface (Azure CLI).</span></span>

<span data-ttu-id="4592b-109">Quando utilizar Olá CLI do Azure tooadd Arduino quadro tooyour hub IoT, o serviço de Olá gera uma chave para o seu tooauthenticate de placa de Arduino com o serviço de Olá.</span><span class="sxs-lookup"><span data-stu-id="4592b-109">When you use hello Azure CLI tooadd your Arduino board tooyour IoT hub, hello service generates a key for your Arduino board tooauthenticate with hello service.</span></span> <span data-ttu-id="4592b-110">Se tiver quaisquer problemas, procurar soluções no Olá [resolução de problemas de página][troubleshoot].</span><span class="sxs-lookup"><span data-stu-id="4592b-110">If you have any problems, look for solutions on hello [troubleshooting page][troubleshoot].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="4592b-111">O que aprenderá</span><span class="sxs-lookup"><span data-stu-id="4592b-111">What you will learn</span></span>
<span data-ttu-id="4592b-112">Neste artigo, irá aprender:</span><span class="sxs-lookup"><span data-stu-id="4592b-112">In this article, you will learn:</span></span>
* <span data-ttu-id="4592b-113">Como toouse Olá CLI do Azure toocreate um IoT hub.</span><span class="sxs-lookup"><span data-stu-id="4592b-113">How toouse hello Azure CLI toocreate an IoT hub.</span></span>
* <span data-ttu-id="4592b-114">Como toocreate uma identidade de dispositivo para a sua Arduino quadro no seu IoT hub.</span><span class="sxs-lookup"><span data-stu-id="4592b-114">How toocreate a device identity for your Arduino board in your IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="4592b-115">Do que precisa</span><span class="sxs-lookup"><span data-stu-id="4592b-115">What you need</span></span>
* <span data-ttu-id="4592b-116">Uma conta do Azure</span><span class="sxs-lookup"><span data-stu-id="4592b-116">An Azure account</span></span>
* <span data-ttu-id="4592b-117">CLI do Azure de um computador com Olá instalada</span><span class="sxs-lookup"><span data-stu-id="4592b-117">A computer with hello Azure CLI installed</span></span>

## <a name="create-your-iot-hub"></a><span data-ttu-id="4592b-118">Criar o hub IoT</span><span class="sxs-lookup"><span data-stu-id="4592b-118">Create your IoT hub</span></span>
<span data-ttu-id="4592b-119">IoT Hub do Azure ajuda-o a ligar, monitorizar e gerir milhões de ativos de IoT.</span><span class="sxs-lookup"><span data-stu-id="4592b-119">Azure IoT Hub helps you connect, monitor, and manage millions of IoT assets.</span></span> <span data-ttu-id="4592b-120">toocreate seu IoT hub, siga estes passos:</span><span class="sxs-lookup"><span data-stu-id="4592b-120">toocreate your IoT hub, follow these steps:</span></span>

1. <span data-ttu-id="4592b-121">Inicie sessão no tooyour conta do Azure executando Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="4592b-121">Sign in tooyour Azure account by running hello following command:</span></span>

   ```bash
   az login
   ```

   <span data-ttu-id="4592b-122">Todas as subscrições disponíveis são apresentadas a seguir um bem-sucedida início de sessão.</span><span class="sxs-lookup"><span data-stu-id="4592b-122">All your available subscriptions are listed after a successful sign-in.</span></span>

2. <span data-ttu-id="4592b-123">Definir a subscrição predefinida de Olá que pretende que toouse executando Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="4592b-123">Set hello default subscription that you want toouse by running hello following command:</span></span>

   ```bash
   az account set --subscription {subscription id or name}
   ```

   <span data-ttu-id="4592b-124">`subscription ID or name`podem ser encontrados no resultado Olá Olá `az login` ou Olá `az account list` comando.</span><span class="sxs-lookup"><span data-stu-id="4592b-124">`subscription ID or name` can be found in hello output of hello `az login` or hello `az account list` command.</span></span>

3. <span data-ttu-id="4592b-125">Registe o fornecedor de Olá Olá os seguintes comandos a executar.</span><span class="sxs-lookup"><span data-stu-id="4592b-125">Register hello provider by running hello following command.</span></span> <span data-ttu-id="4592b-126">Fornecedores de recursos são serviços que fornece recursos para a sua aplicação.</span><span class="sxs-lookup"><span data-stu-id="4592b-126">Resource providers are services that provide resources for your application.</span></span> <span data-ttu-id="4592b-127">Tem de registar o fornecedor de Olá antes de poder implementar Olá recursos do Azure que Olá ofertas de fornecedor.</span><span class="sxs-lookup"><span data-stu-id="4592b-127">You must register hello provider before you can deploy hello Azure resource that hello provider offers.</span></span>

   ```bash
   az provider register -n "Microsoft.Devices"
   ```
4. <span data-ttu-id="4592b-128">Crie um grupo de recursos com o nome exemplo iot na região de EUA oeste Olá executando Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="4592b-128">Create a resource group named iot-sample in hello West US region by running hello following command:</span></span>

   ```bash
   az group create --name iot-sample --location westus
   ```

   <span data-ttu-id="4592b-129">`westus`é a localização de Olá criar o grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="4592b-129">`westus` is hello location you create your resource group.</span></span> <span data-ttu-id="4592b-130">Se pretender que toouse noutra localização, pode executar `az account list-locations -o table` toosee Olá todas as localizações de suporte do Azure.</span><span class="sxs-lookup"><span data-stu-id="4592b-130">If you want toouse another location, you can run `az account list-locations -o table` toosee all hello locations Azure supports.</span></span>

5. <span data-ttu-id="4592b-131">Crie um hub IoT no grupo de recursos de iot-exemplo de Olá executando Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="4592b-131">Create an IoT hub in hello iot-sample resource group by running hello following command:</span></span>

   ```bash
   az iot hub create --name {my hub name} --resource-group iot-sample
   ```

<span data-ttu-id="4592b-132">Por predefinição, a ferramenta de Olá cria um IoT Hub no escalão de preço gratuito Olá.</span><span class="sxs-lookup"><span data-stu-id="4592b-132">By default, hello tool creates an IoT Hub in hello Free pricing tier.</span></span> <span data-ttu-id="4592b-133">Para obter mais informações, consulte [preços do IoT Hub do Azure](https://azure.microsoft.com/pricing/details/iot-hub/).</span><span class="sxs-lookup"><span data-stu-id="4592b-133">For more infomation, see [Azure IoT Hub pricing](https://azure.microsoft.com/pricing/details/iot-hub/).</span></span>

> [!NOTE]
> <span data-ttu-id="4592b-134">nome de Olá do seu IoT hub deve ser globalmente exclusivo.</span><span class="sxs-lookup"><span data-stu-id="4592b-134">hello name of your IoT hub must be globally unique.</span></span>
> <span data-ttu-id="4592b-135">Pode criar apenas uma edição de F1 do IoT Hub do Azure na sua subscrição do Azure.</span><span class="sxs-lookup"><span data-stu-id="4592b-135">You can create only one F1 edition of Azure IoT Hub under your Azure subscription.</span></span>

## <a name="register-your-arduino-board-in-your-iot-hub"></a><span data-ttu-id="4592b-136">Registar o seu painel Arduino no seu IoT hub</span><span class="sxs-lookup"><span data-stu-id="4592b-136">Register your Arduino board in your IoT hub</span></span>
<span data-ttu-id="4592b-137">Cada dispositivo que envia o IoT hub tooyour mensagens e recebe mensagens do seu IoT hub tem de ser registado com um ID exclusivo.</span><span class="sxs-lookup"><span data-stu-id="4592b-137">Each device that sends messages tooyour IoT hub and receives messages from your IoT hub must be registered with a unique ID.</span></span>

<span data-ttu-id="4592b-138">Registe o seu painel Arduino no seu IoT hub em execução seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="4592b-138">Register your Arduino board in your IoT hub by running following command:</span></span>

```bash
az iot device create --device-id mym0wifi --hub-name {my hub name}
```

## <a name="summary"></a><span data-ttu-id="4592b-139">Resumo</span><span class="sxs-lookup"><span data-stu-id="4592b-139">Summary</span></span>
<span data-ttu-id="4592b-140">Já criou um IoT hub e registado o seu painel Arduino com uma identidade de dispositivo no seu IoT hub.</span><span class="sxs-lookup"><span data-stu-id="4592b-140">You've created an IoT hub and registered your Arduino board with a device identity in your IoT hub.</span></span> <span data-ttu-id="4592b-141">Está pronto toolearn como toosend mensagens do seu IoT hub do Arduino quadro tooyour.</span><span class="sxs-lookup"><span data-stu-id="4592b-141">You're ready toolearn how toosend messages from your Arduino board tooyour IoT hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4592b-142">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="4592b-142">Next steps</span></span>
<span data-ttu-id="4592b-143">[Criar uma aplicação de função do Azure e um armazenamento do Azure conta tooprocess e arquivo IoT hub mensagens][process-and-store-iot-hub-messages].</span><span class="sxs-lookup"><span data-stu-id="4592b-143">[Create an Azure function app and an Azure Storage account tooprocess and store IoT hub messages][process-and-store-iot-hub-messages].</span></span>


<!-- Images and links -->

[troubleshoot]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md
[process-and-store-iot-hub-messages]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson3-deploy-resource-manager-template.md