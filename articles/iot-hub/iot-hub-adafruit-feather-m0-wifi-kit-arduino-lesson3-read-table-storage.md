---
title: 'Connect Arduino (C) tooAzure IoT - Lesson 3: armazenamento de tabela | Microsoft Docs'
description: "Monitorizar mensagens hello do dispositivo para a nuvem, eles são escritas tooyour Table storage do Azure."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "dados em nuvem Olá, recolha de dados de nuvem, serviço de nuvem do iot, dados de iot"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: 386083e0-0dbb-48c0-9ac2-4f8fb4590772
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 9fef18bc9e780e78d95f0c643a5f193125130a5b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="read-messages-persisted-in-azure-storage"></a><span data-ttu-id="9a8ba-104">Mensagens de leitura continuada no armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="9a8ba-104">Read messages persisted in Azure Storage</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="9a8ba-105">O que irá fazer</span><span class="sxs-lookup"><span data-stu-id="9a8ba-105">What you will do</span></span>
<span data-ttu-id="9a8ba-106">Mensagens do dispositivo para nuvem de Olá monitor que são enviadas do seu IoT hub do Adafruit Feather M0 Wi-Fi Arduino quadro tooyour como mensagens hello são escritas tooyour Table storage do Azure.</span><span class="sxs-lookup"><span data-stu-id="9a8ba-106">Monitor hello device-to-cloud messages that are sent from your Adafruit Feather M0 WiFi Arduino board tooyour IoT hub as hello messages are written tooyour Azure Table storage.</span></span>

<span data-ttu-id="9a8ba-107">Se tiver quaisquer problemas, procurar soluções no Olá [resolução de problemas de página][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="9a8ba-107">If you have any problems, look for solutions on hello [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="9a8ba-108">O que aprenderá</span><span class="sxs-lookup"><span data-stu-id="9a8ba-108">What you will learn</span></span>
<span data-ttu-id="9a8ba-109">Neste artigo, ficará a saber como toouse mensagens hello do gulp tarefa mensagem de leitura tooread continuada no seu armazenamento de tabelas do Azure.</span><span class="sxs-lookup"><span data-stu-id="9a8ba-109">In this article, you will learn how toouse hello gulp read-message task tooread messages persisted in your Azure Table storage.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="9a8ba-110">Do que precisa</span><span class="sxs-lookup"><span data-stu-id="9a8ba-110">What you need</span></span>
<span data-ttu-id="9a8ba-111">Antes de iniciar este processo, tem concluiu com sucesso [executar a aplicação de exemplo Olá blink do Azure no seu painel Arduino][run-blink-application].</span><span class="sxs-lookup"><span data-stu-id="9a8ba-111">Before starting this process, you must have successfully completed [Run hello Azure blink sample application on your Arduino board][run-blink-application].</span></span>

## <a name="read-new-messages-from-your-storage-account"></a><span data-ttu-id="9a8ba-112">Novas mensagens de leitura da sua conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="9a8ba-112">Read new messages from your storage account</span></span>
<span data-ttu-id="9a8ba-113">No artigo anterior Olá, ficou um exemplo de aplicação no seu painel Arduino.</span><span class="sxs-lookup"><span data-stu-id="9a8ba-113">In hello previous article, you ran a sample application on your Arduino board.</span></span> <span data-ttu-id="9a8ba-114">aplicação de exemplo de Olá enviadas mensagens tooyour Azure do IoT hub.</span><span class="sxs-lookup"><span data-stu-id="9a8ba-114">hello sample application sent messages tooyour Azure IoT hub.</span></span> <span data-ttu-id="9a8ba-115">mensagens Hello enviadas tooyour IoT hub são armazenadas no seu armazenamento de tabelas do Azure através da aplicação Olá função do Azure.</span><span class="sxs-lookup"><span data-stu-id="9a8ba-115">hello messages sent tooyour IoT hub are stored into your Azure Table storage via hello Azure function app.</span></span> <span data-ttu-id="9a8ba-116">Terá de mensagens de tooread de cadeia de ligação de armazenamento do Azure de Olá do seu armazenamento de tabelas do Azure.</span><span class="sxs-lookup"><span data-stu-id="9a8ba-116">You need hello Azure storage connection string tooread messages from your Azure Table storage.</span></span>

<span data-ttu-id="9a8ba-117">mensagens de tooread armazenadas no seu armazenamento de tabelas do Azure, siga estes passos:</span><span class="sxs-lookup"><span data-stu-id="9a8ba-117">tooread messages stored in your Azure Table storage, follow these steps:</span></span>

1. <span data-ttu-id="9a8ba-118">Obter a cadeia de ligação de Olá executando Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="9a8ba-118">Get hello connection string by running hello following commands:</span></span>

   ```bash
   az storage account list -g iot-sample --query [].name
   az storage account show-connection-string -g iot-sample -n {storage name}
   ```

   <span data-ttu-id="9a8ba-119">comando primeiro Olá obtém Olá `storage name` que é utilizado no Olá segundo comando tooget Olá cadeia de ligação.</span><span class="sxs-lookup"><span data-stu-id="9a8ba-119">hello first command retrieves hello `storage name` that is used in hello second command tooget hello connection string.</span></span> <span data-ttu-id="9a8ba-120">Utilize `iot-sample` como valor Olá `{resource group name}` se não alterar o valor de Olá.</span><span class="sxs-lookup"><span data-stu-id="9a8ba-120">Use `iot-sample` as hello value of `{resource group name}` if you didn't change hello value.</span></span>
2. <span data-ttu-id="9a8ba-121">Ficheiro de configuração aberta Olá `config-arduino.json` no Visual Studio Code executando Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="9a8ba-121">Open hello configuration file `config-arduino.json` in Visual Studio Code by running hello following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-arduino.json

   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-arduino.json
   ```
3. <span data-ttu-id="9a8ba-122">Substitua `[Azure storage connection string]` com a cadeia de ligação de Olá que obteve no passo 1.</span><span class="sxs-lookup"><span data-stu-id="9a8ba-122">Replace `[Azure storage connection string]` with hello connection string you got in step 1.</span></span>
4. <span data-ttu-id="9a8ba-123">Guardar Olá `config-arduino.json` ficheiro.</span><span class="sxs-lookup"><span data-stu-id="9a8ba-123">Save hello `config-arduino.json` file.</span></span>
5. <span data-ttu-id="9a8ba-124">Enviar mensagens novamente e lê-los do seu armazenamento de tabelas do Azure executando Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="9a8ba-124">Send messages again and read them from your Azure Table storage by running hello following command:</span></span>

   ```bash
   gulp run --read-storage

   # You can monitor hello serial port by running listen task:
   gulp listen

   # Or you can combine above two gulp tasks into one:
   gulp run --read-storage --listen
   ```

   <span data-ttu-id="9a8ba-125">Olá lógica para ler a partir do Table storage do Azure está a ser Olá `azure-table.js` ficheiro.</span><span class="sxs-lookup"><span data-stu-id="9a8ba-125">hello logic for reading from Azure Table storage is in hello `azure-table.js` file.</span></span>

   ![gulp executar – armazenamento de leitura][gulp-run]

## <a name="summary"></a><span data-ttu-id="9a8ba-127">Resumo</span><span class="sxs-lookup"><span data-stu-id="9a8ba-127">Summary</span></span>
<span data-ttu-id="9a8ba-128">Tiver ligado Arduino quadro tooyour hub IoT na nuvem de Olá e utilizado mensagens dispositivo-nuvem da toosend aplicação Olá blink exemplo com êxito.</span><span class="sxs-lookup"><span data-stu-id="9a8ba-128">You've successfully connected your Arduino board tooyour IoT hub in hello cloud and used hello blink sample application toosend device-to-cloud messages.</span></span> <span data-ttu-id="9a8ba-129">Também utilizado Olá função do Azure aplicação toostore entrado IoT hub mensagens tooyour Table storage do Azure.</span><span class="sxs-lookup"><span data-stu-id="9a8ba-129">You also used hello Azure function app toostore incoming IoT hub messages tooyour Azure Table storage.</span></span> <span data-ttu-id="9a8ba-130">Agora pode enviar mensagens de nuvem para o dispositivo do seu tooyour do hub IoT Arduino quadro.</span><span class="sxs-lookup"><span data-stu-id="9a8ba-130">You can now send cloud-to-device messages from your IoT hub tooyour Arduino board.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9a8ba-131">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="9a8ba-131">Next steps</span></span>
<span data-ttu-id="9a8ba-132">[Enviar mensagens da nuvem para dispositivo][send-cloud-to-device-messages]</span><span class="sxs-lookup"><span data-stu-id="9a8ba-132">[Send cloud-to-device messages][send-cloud-to-device-messages]</span></span>
<!-- Images and links -->

[troubleshooting]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md
[run-blink-application]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson3-run-azure-blink.md
[gulp-run]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson3/gulp_read_message_arduino.png
[send-cloud-to-device-messages]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson4-send-cloud-to-device-messages.md