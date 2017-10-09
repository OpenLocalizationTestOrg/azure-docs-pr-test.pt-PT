---
title: 'Connect Raspberry PI (C) tooAzure IoT - Lesson 1: configurar o dispositivo | Microsoft Docs'
description: "Configure Raspberry Pi 3 para utilizar primeiro e instale Olá Raspbian SO, um sistema operativo livre que está otimizado para Olá hardware Raspberry Pi."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "instalação raspbian, transferência raspbian, como tooinstall raspbian, raspbian configuração, raspberry pi instalação raspbian, raspberry pi instalação SO, raspberry pi sd cartão instalar, raspberry pi ligar, ligar a conectividade do tooraspberry pi, raspberry pi"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: 8ee9b23c-93f7-43ff-8ea1-e7761eb87a6f
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: ba3466f6d5d46352326a2a63eb011e117da5aca5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-your-device"></a>Configurar o seu dispositivo
## <a name="what-you-will-do"></a>O que irá fazer
Configurar Pi para utilização da primeira vez e instalar o sistema de operativo Olá Raspbian. Raspbian é um sistema operativo livre que está otimizado para Olá hardware Raspberry Pi. Se tiver quaisquer problemas, procurar soluções no Olá [resolução de problemas de página](iot-hub-raspberry-pi-kit-c-troubleshooting.md).

## <a name="what-you-will-learn"></a>O que aprenderá
Neste artigo, irá aprender:

* Como tooinstall Raspbian no Pi.
* Como toopower segurança Pi utilizando um cabo USB.
* Como tooconnect Pi toohello rede utilizando um cabo de Ethernet ou de uma rede sem fios.
* Como tooadd um toohello LED breadboard e ligá-lo tooPi.

## <a name="what-you-need"></a>Do que precisa
toocomplete desta operação, terá de Olá seguintes partes do seu Raspberry Pi 3 Starter Kit:

* Olá quadro Raspberry Pi 3
* cartão microSD de 16 GB de Olá
* Olá 5 volt 2 amp fonte de alimentação com o cabo do Olá 6 online micro USB
* breadboard Olá
* Cablagem de conector
* Um resistor 560 ohm
* Um diffused LED de 10 mm
* Olá cabo de Ethernet

![Coisas no seu Starter Kit](media/iot-hub-raspberry-pi-lessons/lesson1/starter_kit.jpg)

Também tem de ter:

* Uma ligação com ou sem fios para Pi tooconnect para.
* Um USB SD adaptador ou mini-SD cartão tooburn Olá SO imagem no cartão microSD de Olá.
* Um computador com Windows, Mac ou Linux. computador Olá é utilizado tooinstall Raspbian no cartão microSD de Olá.
* Um toodownload de ligação de Internet Olá ferramentas necessárias e software.

## <a name="install-raspbian-on-hello-microsd-card"></a>Instalar Raspbian no cartão MicroSD de Olá
Prepare o cartão microSD de Olá para a instalação da imagem de Raspbian Olá.

1. Transferir Raspbian.
   1. [Transferir](https://www.raspberrypi.org/downloads/raspbian/) ficheiro. zip Olá Raspbian Jessie com Pixel.
   2. Extrair Olá Raspbian imagem tooa pasta do computador.
2. Instale Raspbian toohello microSD cartão.
   1. [Transferir](https://www.etcher.io) e instalar o utilitário de burner de cartão Olá Etcher SD.
   2. Execute Etcher e selecione a imagem de Raspbian Olá que extraiu no passo 1.
   3. Selecione a unidade de cartão microSD de Olá.
      Tenha em atenção que Etcher poderá já selecionou correta da unidade Olá.
   4. Clique em **Flash** tooinstall Raspbian toohello microSD cartão.
   5. Remova o cartão microSD de Olá do seu computador quando a instalação estiver concluída.
      É diretamente cartão de microSD Olá tooremove seguro porque Etcher automaticamente ejects ou unmounts cartão microSD de Olá após a conclusão.
   6. Inserir cartão microSD de Olá a Pi.

![Inserir o cartão SD do Olá](media/iot-hub-raspberry-pi-lessons/lesson1/insert_sdcard.jpg)

## <a name="turn-on-pi"></a>Ativar o instalador de plataforma
Ative a Pi utilizando o cabo USB micro Olá e fonte de alimentação Olá.

![Ativar](media/iot-hub-raspberry-pi-lessons/lesson1/micro_usb_power_on.jpg)

> [!NOTE]
> É importante toouse Olá fonte de alimentação no kit de Olá que seja, pelo menos, 2A toomake se de que o seu Raspberry tem suficiente toowork energia corretamente.

## <a name="enable-ssh"></a>Ativar SSH
A partir da versão de Novembro de 2016 Olá, Raspbian tem Olá SSH de servidor desativadas por predefinição. Terá de tooenable-lo manualmente. Pode consultar toohello [instruções oficiais](https://www.raspberrypi.org/documentation/remote-access/ssh/) ou ligar um monitor e aceda demasiado**preferências -> Raspberry Pi configuração** tooenable SSH.

## <a name="connect-raspberry-pi-3-toohello-network"></a>Ligar a rede de toohello Raspberry Pi 3
Pode ligar tooa Pi com fios tooa de rede sem fios ou de rede. Certifique-se que Pi toohello ligado, mesmo que o computador de rede. Por exemplo, pode ligar toohello Pi que mesmo comutador a que o computador está ligado à.

### <a name="connect-tooa-wired-network"></a>Ligar tooa rede com fios
Utilize Olá Ethernet cabo tooconnect tooyour Pi rede com fios. Olá dois LEDs no Pi ativassem se Olá ligação for estabelecida.

![Ligar utilizando um cabo de Ethernet](media/iot-hub-raspberry-pi-lessons/lesson1/connect_ethernet.jpg)

### <a name="connect-tooa-wireless-network"></a>Ligar a rede sem fios tooa
Siga Olá [instruções](https://www.raspberrypi.org/learning/software-guide/wifi/) de Olá Raspberry Pi Foundation tooconnect Pi tooyour rede sem fios. Estas instruções requerem toofirst ligar um monitor e um tooPi teclado.

## <a name="connect-hello-led-toopi"></a>Ligar Olá LED tooPi
toocomplete esta tarefa, utilize Olá [breadboard](https://learn.sparkfun.com/tutorials/how-to-use-a-breadboard), Olá cablagem de conector, Olá LED e Olá resistor. Ligue-toohello [para fins gerais de entrada/saída](https://www.raspberrypi.org/documentation/usage/gpio/) portas (GPIO) de Pi.

![Breadboard, LED e Resistor](media/iot-hub-raspberry-pi-lessons/lesson1/breadboard_led_resistor.jpg)

1. Ligar a parte mais curto do Olá de Olá LED demasiado**GPIO GND (Pin 6)**.
2. Ligar a parte superior do Olá de Olá LED tooone fase de resistor Olá.
3. Ligar Olá outro fase de resistor Olá demasiado**GPIO 4 (Pin 7)**.

Tenha em atenção que polarity Olá LED é importante. Esta definição polarity é geralmente conhecida como baixa Active Directory.

![Pinout](media/iot-hub-raspberry-pi-lessons/lesson1/pinout_breadboard.png)

Parabéns! Configurou com êxito Pi.

## <a name="summary"></a>Resumo
Neste artigo, aprendeu como tooconfigure Pi através da instalação Raspbian, rede de tooa Pi ligação e ligar um tooPi LED. Tenha em atenção que Olá que LED ainda não apresentado. a tarefa seguinte Olá está ferramentas necessárias do tooinstall Olá e software em preparação para executar uma aplicação de exemplo num Pi.

![Hardware está preparado](media/iot-hub-raspberry-pi-lessons/lesson1/hardware_ready.jpg)

## <a name="next-steps"></a>Passos seguintes
[Obtenha as ferramentas de Olá](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-win32.md)

