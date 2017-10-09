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
# <a name="create-an-azure-function-app-and-storage-account"></a>Criar uma aplicação de função do Azure e uma conta de armazenamento

As funções do Azure é uma solução para uma fácil execução _funções_ (pequenos blocos de código) na nuvem de Olá. Uma aplicação de função do Azure aloja a execução de Olá das suas funções no Azure. 

## <a name="what-you-will-do"></a>O que irá fazer

- Utilize um toocreate de modelo Azure Resource Manager, uma aplicação de função do Azure e uma conta de armazenamento do Azure. aplicação de função do Azure de Olá escuta de eventos do tooAzure IoT hub, processa mensagens a receber e escreve-los tooAzure o Table storage.

Se tiver quaisquer problemas, procurar soluções no Olá [resolução de problemas de página](iot-hub-gateway-kit-c-sim-troubleshooting.md).


## <a name="what-you-will-learn"></a>O que aprenderá

Este lesson, irá aprender:

- Como toouse do Azure Resource Manager toodeploy recursos do Azure.
- Como toouse do Azure funcionar aplicação tooprocess mensagens do IoT Hub e escrevê-las tooa tabela no Table storage do Azure.

## <a name="what-you-need"></a>Do que precisa

Tem concluiu com sucesso lições anterior Olá:

- [Lesson 1: Configurar o seu NUC Intel como um gateway de IoT](iot-hub-gateway-kit-c-sim-lesson1-set-up-nuc.md)
- [Lesson 2: Preparar o seu computador anfitrião e o hub IoT do Azure](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-win32.md)
- [Lesson 3: Receber mensagens do dispositivo simulado Olá e ler mensagens do seu IoT hub](iot-hub-gateway-kit-c-sim-lesson3-configure-simulated-device-app.md)

## <a name="open-a-sample-app"></a>Abrir uma aplicação de exemplo

Aceda tooyour `iot-hub-c-intel-nuc-gateway-getting-started` repositório pasta, ficheiros de configuração de Olá inicializar e projeto de exemplo de Olá, em seguida, abrir no Visual Studio Code executando Olá os seguintes comandos:

```bash
cd Lesson4
npm install
gulp init
code .
```

![Estrutura do repositório](media/iot-hub-gateway-kit-lessons/lesson4/arm_template.png)

- Olá `arm-template.json` ficheiro é o modelo Azure Resource Manager Olá que contenha uma aplicação de função do Azure e uma conta de armazenamento do Azure.
- Olá `arm-template-param.json` ficheiro é o ficheiro de configuração de Olá utilizado pelo modelo do Azure Resource Manager Olá.
- Olá `ReceiveDeviceMessages` subpasta contém código Node.js Olá Olá função do Azure.

## <a name="configure-azure-resource-manager-templates-and-create-resources-in-azure"></a>Configurar modelos Azure Resource Manager e criar recursos no Azure

Olá atualização `arm-template-param.json` ficheiro no Visual Studio Code.

![json de modelo Arm](media/iot-hub-gateway-kit-lessons/lesson4/arm_template_param.png)

- Substitua `[your IoT Hub name]` com `{my hub name}` que especificou no Lesson 2.

Depois de atualizar Olá `arm-template-param.json` de ficheiros, implementar Olá recursos tooAzure executando Olá os seguintes comandos:

```bash
az group deployment create --template-file arm-template.json --parameters @arm-template-param.json -g iot-gateway
```

Utilize `iot-gateway` como valor Olá `{resource group name}` se não tiver a alterar o valor de Olá no Lesson 2.

## <a name="summary"></a>Resumo

Criou o tooprocess de aplicação de função do Azure mensagens do IoT hub e um armazenamento do Azure conta toostore estas mensagens. Agora pode ler as mensagens que são enviadas pelo seu IoT hub do gateway tooyour.

## <a name="next-steps"></a>Passos seguintes
[Mensagens de leitura continuada no armazenamento do Azure](iot-hub-gateway-kit-c-sim-lesson4-read-table-storage.md).
