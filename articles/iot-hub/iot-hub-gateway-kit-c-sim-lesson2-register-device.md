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
# <a name="create-your-azure-iot-hub-and-register-your-device"></a>Criar o seu hub IoT do Azure e registar o dispositivo

## <a name="what-you-will-do"></a>O que irá fazer

- Criar um grupo de recursos
- Criar o seu IoT hub primeiro
- Registe o seu dispositivo no seu IoT hub com Olá CLI do Azure. 

Quando registar o seu dispositivo no seu IoT hub, Olá serviço IoT Hub do Azure gera uma chave para o seu tooauthenticate toouse de dispositivo com o serviço de Olá. 

Se tiver quaisquer problemas, procurar soluções no Olá [resolução de problemas de página](iot-hub-gateway-kit-c-sim-troubleshooting.md).

## <a name="what-you-will-learn"></a>O que aprenderá

Este lesson, irá aprender:

- Como toouse Olá CLI do Azure toocreate um IoT hub.
- Como tooregister um dispositivo de um hub IoT.

## <a name="what-you-need"></a>Do que precisa

- Uma subscrição ativa do Azure. Se não tiver uma conta do Azure, pode criar um [conta de avaliação do Azure gratuita](http://azure.microsoft.com/pricing/free-trial/) em apenas alguns minutos.
- É necessário ter Olá instalado da CLI do Azure.

## <a name="create-an-iot-hub"></a>Criar um hub IoT

toocreate um IoT hub, siga estes passos:

1. Inicie sessão no tooyour conta do Azure executando Olá os seguintes comandos:

   ```bash
   az login
   ```

   Todas as subscrições disponíveis serão apresentadas a seguir um bem-sucedida início de sessão.

2. Predefinir Olá subscrição do Azure que pretende que toouse executando Olá os seguintes comandos:

   ```bash
   az account set --subscription {subscription id or name}
   ```

   `subscription ID or name`podem ser encontrados no resultado Olá Olá `az login` ou Olá `az account list` comando.

3. Registe o fornecedor de Olá Olá os seguintes comandos a executar. Fornecedores de recursos são serviços que fornece recursos para a sua aplicação. Tem de registar o fornecedor de Olá antes de poder implementar Olá recursos do Azure que Olá ofertas de fornecedor.

   ```bash
   az provider register -n "Microsoft.Devices"
   ```

4. Crie um grupo de recursos denominado `iot-gateway` na região de EUA oeste Olá executando Olá os seguintes comandos:

   ```bash
   az group create --name iot-gateway --location westus
   ```
   
   `westus`é a localização de Olá criar o grupo de recursos. Se pretender que toouse noutra localização, pode executar `az account list-locations -o table` toosee Olá todas as localizações de suporte do Azure.

5. Criar um hub IoT no Olá `iot-gateway` grupo de recursos, executando Olá os seguintes comandos:

   ```bash
   az iot hub create --name {my hub name} --resource-group iot-gateway
   ```

Por predefinição, a ferramenta de Olá cria um IoT Hub no escalão de preço gratuito Olá. Para obter mais informações, consulte [preços do IoT Hub do Azure](https://azure.microsoft.com/pricing/details/iot-hub/).

> [!NOTE]
> nome de Olá do seu IoT hub deve ser globalmente exclusivo. Pode criar apenas uma edição de F1 do Iot Hub do Azure na sua subscrição do Azure.

## <a name="register-your-device-in-your-iot-hub"></a>Registar o seu dispositivo no seu IoT hub

Cada dispositivo que envia o IoT hub tooyour mensagens e recebe mensagens do seu IoT hub tem de ser registado com um ID exclusivo.
Registe o seu dispositivo no seu IoT hub ao executar seguinte comando:

```bash
az iot device create --device-id mydevice --hub-name {my hub name} --resource-group iot-gateway
```

## <a name="summary"></a>Resumo

Já criou um IoT hub e registado o dispositivo lógico com uma identidade de dispositivo no seu IoT hub. Está pronto toolearn como tooconfigure e executar um gateway exemplo aplicação toosend de dados do seu IoT hub do dispositivo físico tooyour no Olá na nuvem.

## <a name="next-steps"></a>Passos seguintes
[Configurar e executar uma aplicação de exemplo de carregamento do dispositivo simulado na nuvem](iot-hub-gateway-kit-c-sim-lesson3-configure-simulated-device-app.md)