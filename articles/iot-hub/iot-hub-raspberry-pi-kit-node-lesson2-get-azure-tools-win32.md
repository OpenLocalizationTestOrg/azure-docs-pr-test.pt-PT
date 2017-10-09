---
title: "Ligar Raspberry Pi (nó) tooAzure IoT - Lesson 2: obter ferramentas (Windows) | Microsoft Docs"
description: "Instale o Python e Olá interface de linha de comandos do Azure (CLI do Azure) no Windows 7 e versões posteriores."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "cli de serviço, do azure de nuvem do IOT"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: acfa13e3-6d2c-4e68-9a77-1cbc2cf3f9c1
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 25b50214322137ea32861fd1131c474e2fc7ebb7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="get-azure-tools-windows-7-and-later"></a>Obter ferramentas do Azure (Windows 7 e posterior)
> [!div class="op_single_selector"]
> * [Windows 7 e posterior](iot-hub-raspberry-pi-kit-node-lesson2-get-azure-tools-win32.md)
> * [Ubuntu 16.04](iot-hub-raspberry-pi-kit-node-lesson2-get-azure-tools-ubuntu.md)
> * [macOS 10.10](iot-hub-raspberry-pi-kit-node-lesson2-get-azure-tools-mac.md)

## <a name="what-you-will-do"></a>O que irá fazer
Instalar o Python e Olá interface de linha de comandos do Azure (CLI do Azure). Se tiver quaisquer problemas, procurar soluções no Olá [resolução de problemas de página](iot-hub-raspberry-pi-kit-node-troubleshooting.md).

## <a name="what-you-will-learn"></a>O que aprenderá
Neste artigo, irá aprender:
* Como tooinstall Python.
* Como tooinstall Olá CLI do Azure.

## <a name="what-you-need"></a>Do que precisa
* Um computador Windows com uma ligação à Internet.
* Uma subscrição ativa do Azure. Se não tiver uma conta do Azure, crie um [conta de avaliação do Azure gratuita](http://azure.microsoft.com/pricing/free-trial/) em apenas alguns minutos.

## <a name="install-python"></a>Instalar o Python
[Instalar o Python](https://www.python.org/downloads/) no seu computador Windows. Pode instalar o Python 2.7, 3.4 ou 3.5. Este tutorial baseia-se no Python 2.7. Se já tiver instalado o Python, aceda a secção seguinte toohello e instalar Olá CLI do Azure.

Também precisa de caminho de Olá tooadd das pastas de olá onde python.exe e pip.exe são instalados toohello sistema `PATH` variável de ambiente. Por predefinição, python.exe é instalado em `C:\Python27` e pip.exe está instalado no `C:\Python27\Scripts`.

## <a name="install-hello-azure-cli"></a>Instalar Olá CLI do Azure
Olá CLI do Azure fornece uma experiência de linha de comandos multiplataformas para o Azure. Trabalhar diretamente a partir do seu tooprovision da linha de comandos e gerir os recursos.

Olá tooinstall CLI do Azure, siga estes passos:

1. Abra uma janela de linha de comandos como administrador.
2. Execute Olá os seguintes comandos:

   ```bash
   pip install --upgrade azure-cli
   pip install --upgrade azure-cli-iot
   ```
3. Verificar a instalação de Olá executando Olá os seguintes comandos:

   ```bash
   az iot -h
   ```

Consulte a seguinte Olá de saída se a instalação de Olá é efetuada com êxito.

![Saída que indica êxito](media/iot-hub-raspberry-pi-lessons/lesson2/az_iot_help_win.png)

## <a name="summary"></a>Resumo
Instalou Olá CLI do Azure. A seguinte tarefa toocreate sua identidade de dispositivo e do hub IoT do Azure utilizando Olá CLI do Azure.

## <a name="next-steps"></a>Passos seguintes
[Crie o seu IoT hub e registe Raspberry Pi 3](iot-hub-raspberry-pi-kit-node-lesson2-prepare-azure-iot-hub.md)

