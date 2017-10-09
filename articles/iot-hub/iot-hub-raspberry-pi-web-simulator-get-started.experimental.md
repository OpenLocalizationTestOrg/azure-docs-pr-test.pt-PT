---
title: aaaSimulated Raspberry Pi toocloud (Node.js) - ligar Raspberry Pi web simulador tooAzure IoT Hub | Microsoft Docs
description: Ligar Raspberry Pi web simulador tooAzure IoT Hub para Raspberry Pi toosend dados toohello em nuvem do Azure.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: raspberry pi simulador, azure raspberry pi, raspberry pi iot hub iot, raspberry pi enviar dados toocloud, raspberry pi toocloud
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-web-simulator-get-started
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 7/7/2017
ms.author: xshi
ms.openlocfilehash: 0ebe1004e96ff4e64fdd1b05b7e35192ec42f7d0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="connect-raspberry-pi-online-simulator-tooazure-iot-hub-nodejs"></a>Ligar Raspberry Pi simulador online tooAzure IoT Hub (Node.js)

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

Neste tutorial, comece por learning Olá Noções básicas de trabalhar com simulador online Raspberry Pi. Em seguida, saiba como tooseamlessly estabelecer a ligação em nuvem do Olá Pi simulador toohello utilizando [IoT Hub do Azure](iot-hub-what-is-iot-hub.md). 

Se tiver dispositivos físicos, visite [ligar Raspberry Pi tooAzure IoT Hub](iot-hub-raspberry-pi-kit-node-get-started.md) tooget foi iniciado. 

<p>
<div id="diag" style="width:100%; text-align:center">
<a href="https://azure-samples.github.io/raspberry-pi-web-simulator/#getstarted">
<img src="media/iot-hub-raspberry-pi-web-simulator/3_banner.png" alt="Connect Raspberry Pi web simulator tooAzure IoT Hub" width="400">
</div>
<p>
<div id="button" style="width:100%; text-align:center">
<a href="https://azure-samples.github.io/raspberry-pi-web-simulator/#Getstarted">
<img src="media/iot-hub-raspberry-pi-web-simulator/6_button_default.png" alt="Start Raspberry Pi simulator" width="400" onmouseover="this.src='media/iot-hub-raspberry-pi-web-simulator/5_button_click.png';" onmouseout="this.src='media/iot-hub-raspberry-pi-web-simulator/6_button_default.png';">
</div>

## <a name="what-you-do"></a>O que fazer

* Saiba Olá Noções básicas do simulador online Raspberry Pi.
* Crie um hub IoT.
* Registe um dispositivo para Pi no seu IoT hub.
* Execute um exemplo de aplicação no Pi toosend simulado sensor dados tooyour IoT hub.

Ligar simulado Raspberry Pi tooan IoT hub que criou. Em seguida, execute uma aplicação de exemplo com dados de sensores do Olá simulador toogenerate. Por fim, enviar Olá sensor dados tooyour do IoT hub.

## <a name="what-you-learn"></a>O que irá aprender

* Como toocreate um hub IoT do Azure e obter a cadeia de ligação do novo dispositivo. Se não tiver uma conta do Azure, [criar uma conta de avaliação gratuita do Azure](https://azure.microsoft.com/free/) em apenas alguns minutos.
* Como toowork com simulador online Raspberry Pi.
* Como toosend sensor dados tooyour do IoT hub.

## <a name="overview-of-raspberry-pi-web-simulator"></a>Descrição geral do simulador de web Raspberry Pi

Clique em simulador online do Olá botão toolaunch Raspberry Pi.

> [!div class="button"]
[Iniciar o simulador Raspberry Pi](https://azure-samples.github.io/raspberry-pi-web-simulator/#GetStarted)

Existem três áreas no simulador do Olá web.
* Área de assemblagem - circuito de predefinição Olá é que um Pi estabelece ligação com um sensor BME280 e um LED. área de Olá está bloqueada na versão de pré-visualização, por isso, atualmente não é possível efetuar a personalização.
* Codificação área - um editor de código online para toocode com Raspberry Pi. aplicação de exemplo Olá predefinida ajuda toocollect dados de sensores do BME280 sensor e envia tooyour IoT Hub do Azure. aplicação Olá é totalmente compatível com dispositivos de Pi reais. 
* Janela de consola integrada - Mostra saída Olá do seu código. Na parte superior de Olá desta janela, existem três botões.
   * **Executar** -executar a aplicação de Olá no Olá codificação área.
   * **Repor** -Olá de reposição de codificação área toohello predefinido exemplo de aplicação.
   * **Expandir/subconjuntos de validação** - no Olá direita lado existe é um botão para que expanda/toofold Olá janela da consola.

> [!NOTE] 
simulador de web de Raspberry Pi Olá está agora disponível numa versão de pré-visualização. Gostaríamos toohear sua voz no Olá [Gitter Chatroom](https://gitter.im/Microsoft/raspberry-pi-web-simulator). código de origem Olá é público no [Github](https://github.com/Azure-Samples/raspberry-pi-web-simulator).

![Descrição geral do simulador online Pi](media/iot-hub-raspberry-pi-web-simulator/0_overview.png)

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]


## <a name="run-a-sample-application-on-pi-web-simulator"></a>Execute um exemplo de aplicação no simulador do instalador de plataforma web

1. Na área de codificação, certifique-se de que está a trabalhar na aplicação de exemplo Olá predefinida. Substitua o marcador de posição de Olá na linha 15 por Olá cadeia de ligação de dispositivos do Azure IoT hub.
   ![Substitua a cadeia de ligação do dispositivo Olá](media/iot-hub-raspberry-pi-web-simulator/1_connectionstring.png)

2. Clique em **executar** ou tipo `npm start` aplicação de Olá toorun.


Deverá ver a saída de Olá seguinte que mostra os dados de sensores de Olá Olá mensagens e que são enviados tooyour IoT hub ![saída - dados de sensor enviados a partir do IoT hub tooyour Raspberry Pi](media/iot-hub-raspberry-pi-web-simulator/2_run_application.png)


## <a name="next-steps"></a>Passos seguintes

Executar um dados de sensores de toocollect de aplicação de exemplo e enviá-lo tooyour IoT hub.

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
