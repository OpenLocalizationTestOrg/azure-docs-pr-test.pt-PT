---
title: 'Connect Raspberry PI (C) tooAzure IoT - Lesson 2: ferramentas do Azure (macOS) | Microsoft Docs'
description: Instale o Python e interface de linha de comandos do Azure (CLI do Azure) no macOS.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "cli de serviço, do azure de nuvem do IOT"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: f2d7d584-7734-401c-976c-81788a7282a3
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: a079250fd94fa9bc1c11b6c21de02a8d46f6f3bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="get-azure-tools-macos-1010"></a>Obter ferramentas do Azure (macOS 10.10)
> [!div class="op_single_selector"]
> * [Windows 7 e posterior](iot-hub-raspberry-pi-kit-c-lesson2-get-azure-tools-win32.md)
> * [Ubuntu 16.04](iot-hub-raspberry-pi-kit-c-lesson2-get-azure-tools-ubuntu.md)
> * [macOS 10.10](iot-hub-raspberry-pi-kit-c-lesson2-get-azure-tools-mac.md)

## <a name="what-you-will-do"></a>O que irá fazer
Instale Olá interface de linha de comandos do Azure (CLI do Azure). Se tiver quaisquer problemas, procurar soluções no Olá [resolução de problemas de página](iot-hub-raspberry-pi-kit-c-troubleshooting.md).

## <a name="what-you-will-learn"></a>O que aprenderá
Neste artigo, irá aprender:
* Como tooinstall CLI do Azure.
* Como tooadd um subgrupo IoT de Olá CLI do Azure.

## <a name="what-you-need"></a>Do que precisa
* Um Mac com uma ligação à Internet.
* Uma subscrição ativa do Azure. Se não tiver uma conta do Azure, pode criar um [conta de avaliação do Azure gratuita](http://azure.microsoft.com/pricing/free-trial/) em apenas alguns minutos.

## <a name="install-python"></a>Instalar o Python
Embora macOS é fornecido com o Python 2.7 Box Olá, recomendamos que instale Python através de Homebrew. Consulte [instalar o Python no macOS](http://docs.python-guide.org/en/latest/starting/install/osx/).

Instale o Python e pip executando Olá os seguintes comandos:

```bash
brew install python
```

## <a name="install-hello-azure-cli"></a>Instalar Olá CLI do Azure
Olá CLI do Azure fornece uma experiência de linha de comandos multiplataformas para o Azure. Trabalhar diretamente a partir do seu tooprovision de linha de comandos e gerir os recursos. 

tooinstall hello mais recente CLI do Azure, siga estes passos:

1. Olá execute os seguintes comandos numa janela de terminal. Poderá demorar cinco minutos tooinstall Olá CLI do Azure.

   ```bash
   pip install --upgrade azure-cli
   pip install --upgrade azure-cli-iot
   ```
2. Verificar a instalação de Olá executando Olá os seguintes comandos:

   ```bash
   az iot -h
   ```

Deverá ver a seguinte Olá de saída se a instalação de Olá é efetuada com êxito.

![Saída que indica êxito](media/iot-hub-raspberry-pi-lessons/lesson2/az_iot_help_osx.png)

## <a name="summary"></a>Resumo
Instalou Olá CLI do Azure. A próxima tarefa consiste toocreate sua identidade do Azure IoT hub e dispositivos através da utilização de Olá CLI do Azure.

## <a name="next-steps"></a>Passos seguintes
[Crie o seu IoT hub e registe Raspberry Pi 3](iot-hub-raspberry-pi-kit-c-lesson2-prepare-azure-iot-hub.md)

