---
title: 'Ligar Arduino tooAzure IoT - Lesson 2: ferramentas do Azure (Ubuntu) | Microsoft Docs'
description: Instale o Python e interface de linha de comandos do Azure (CLI do Azure) no Ubuntu.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "cli do Azure, o serviço de nuvem do iot, arduino nuvem"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: bb5cb602-7292-4772-ac90-c0b52ebc8340
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 7eb9c891a6340fee018894883583022d740ecb6f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="get-azure-tools-ubuntu-1604"></a>Obter ferramentas do Azure (Ubuntu 16.04)

> [!div class="op_single_selector"]
> * [Windows 7 ou posterior][windows]
> * [Ubuntu 16.04][ubuntu]
> * [macOS 10.10][macos]

## <a name="what-you-will-do"></a>O que irá fazer

Instale Olá interface de linha de comandos do Azure (CLI do Azure). Se tiver quaisquer problemas, procurar soluções no Olá [resolução de problemas de página](iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md) para seu painel Adafruit Feather M0 Wi-Fi Arduino.

## <a name="what-you-will-learn"></a>O que aprenderá
Neste artigo, irá aprender:
* Como tooinstall Olá CLI do Azure.
* Como tooadd um subgrupo IoT de Olá CLI do Azure.

## <a name="what-you-need"></a>Do que precisa
* Um computador de Ubuntu com uma ligação à Internet.
* Uma subscrição ativa do Azure. Se não tiver uma conta, pode criar um [conta de avaliação gratuita](http://azure.microsoft.com/pricing/free-trial/) em apenas alguns minutos.

## <a name="install-hello-azure-cli"></a>Instalar Olá CLI do Azure
Olá CLI do Azure fornece uma experiência multiplataformas de linha de comandos do Azure, permitindo-lhe toowork diretamente a partir do seu tooprovision de linha de comandos e gerir os recursos.

tooinstall hello mais recente CLI do Azure, siga estes passos:

1. Olá execute os seguintes comandos numa janela de terminal. Poderá demorar cinco minutos tooinstall Olá CLI do Azure.

   ```bash
   sudo apt-get update
   sudo apt-get install -y libssl-dev libffi-dev
   sudo apt-get install -y python-dev
   sudo apt-get install -y build-essential
   sudo apt-get install -y python-pip
   sudo pip install --upgrade azure-cli
   sudo pip install --upgrade azure-cli-iot
   ```
2. Verificar a instalação de Olá executando Olá os seguintes comandos:

   ```bash
   az iot -h
   ```

Deverá ver a seguinte Olá de saída se a instalação de Olá é efetuada com êxito.

![Saída que indica êxito][output]

## <a name="summary"></a>Resumo
Instalou Olá CLI do Azure. A próxima tarefa consiste toocreate o hub IoT do Azure e, em seguida, utilizar identidade de dispositivo Olá CLI do Azure.

## <a name="next-steps"></a>Passos seguintes
[Criar o seu IoT hub e registar o seu painel Arduino][create-your-iot-hub-and-register-your-arduino-board]
<!-- Images and links -->

[windows]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-get-azure-tools-win32.md
[ubuntu]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-get-azure-tools-ubuntu.md
[macos]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-get-azure-tools-mac.md
[output]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson2/az_iot_help_ubuntu.png
[create-your-iot-hub-and-register-your-arduino-board]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-prepare-azure-iot-hub.md