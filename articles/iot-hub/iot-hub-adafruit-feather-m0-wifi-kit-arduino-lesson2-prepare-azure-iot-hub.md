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
# <a name="create-your-iot-hub-and-register-your-adafruit-feather-m0-wifi-arduino-board"></a>Criar o seu IoT hub e registar o seu painel Adafruit Feather M0 Wi-Fi Arduino

## <a name="what-you-will-do"></a>O que irá fazer
* Crie um grupo de recursos.
* Crie o seu hub IoT do Azure no grupo de recursos de Olá.
* Adicione o seu Arduino quadro toohello Azure IoT hub utilizando Olá interface de linha de comandos do Azure (CLI do Azure).

Quando utilizar Olá CLI do Azure tooadd Arduino quadro tooyour hub IoT, o serviço de Olá gera uma chave para o seu tooauthenticate de placa de Arduino com o serviço de Olá. Se tiver quaisquer problemas, procurar soluções no Olá [resolução de problemas de página][troubleshoot].

## <a name="what-you-will-learn"></a>O que aprenderá
Neste artigo, irá aprender:
* Como toouse Olá CLI do Azure toocreate um IoT hub.
* Como toocreate uma identidade de dispositivo para a sua Arduino quadro no seu IoT hub.

## <a name="what-you-need"></a>Do que precisa
* Uma conta do Azure
* CLI do Azure de um computador com Olá instalada

## <a name="create-your-iot-hub"></a>Criar o hub IoT
IoT Hub do Azure ajuda-o a ligar, monitorizar e gerir milhões de ativos de IoT. toocreate seu IoT hub, siga estes passos:

1. Inicie sessão no tooyour conta do Azure executando Olá os seguintes comandos:

   ```bash
   az login
   ```

   Todas as subscrições disponíveis são apresentadas a seguir um bem-sucedida início de sessão.

2. Definir a subscrição predefinida de Olá que pretende que toouse executando Olá os seguintes comandos:

   ```bash
   az account set --subscription {subscription id or name}
   ```

   `subscription ID or name`podem ser encontrados no resultado Olá Olá `az login` ou Olá `az account list` comando.

3. Registe o fornecedor de Olá Olá os seguintes comandos a executar. Fornecedores de recursos são serviços que fornece recursos para a sua aplicação. Tem de registar o fornecedor de Olá antes de poder implementar Olá recursos do Azure que Olá ofertas de fornecedor.

   ```bash
   az provider register -n "Microsoft.Devices"
   ```
4. Crie um grupo de recursos com o nome exemplo iot na região de EUA oeste Olá executando Olá os seguintes comandos:

   ```bash
   az group create --name iot-sample --location westus
   ```

   `westus`é a localização de Olá criar o grupo de recursos. Se pretender que toouse noutra localização, pode executar `az account list-locations -o table` toosee Olá todas as localizações de suporte do Azure.

5. Crie um hub IoT no grupo de recursos de iot-exemplo de Olá executando Olá os seguintes comandos:

   ```bash
   az iot hub create --name {my hub name} --resource-group iot-sample
   ```

Por predefinição, a ferramenta de Olá cria um IoT Hub no escalão de preço gratuito Olá. Para obter mais informações, consulte [preços do IoT Hub do Azure](https://azure.microsoft.com/pricing/details/iot-hub/).

> [!NOTE]
> nome de Olá do seu IoT hub deve ser globalmente exclusivo.
> Pode criar apenas uma edição de F1 do IoT Hub do Azure na sua subscrição do Azure.

## <a name="register-your-arduino-board-in-your-iot-hub"></a>Registar o seu painel Arduino no seu IoT hub
Cada dispositivo que envia o IoT hub tooyour mensagens e recebe mensagens do seu IoT hub tem de ser registado com um ID exclusivo.

Registe o seu painel Arduino no seu IoT hub em execução seguinte comando:

```bash
az iot device create --device-id mym0wifi --hub-name {my hub name}
```

## <a name="summary"></a>Resumo
Já criou um IoT hub e registado o seu painel Arduino com uma identidade de dispositivo no seu IoT hub. Está pronto toolearn como toosend mensagens do seu IoT hub do Arduino quadro tooyour.

## <a name="next-steps"></a>Passos seguintes
[Criar uma aplicação de função do Azure e um armazenamento do Azure conta tooprocess e arquivo IoT hub mensagens][process-and-store-iot-hub-messages].


<!-- Images and links -->

[troubleshoot]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md
[process-and-store-iot-hub-messages]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson3-deploy-resource-manager-template.md