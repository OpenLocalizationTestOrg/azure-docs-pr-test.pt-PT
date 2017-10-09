---
title: "carregamento de ficheiros do aaaUse Olá tooconfigure portal do Azure | Microsoft Docs"
description: "Como toouse Olá tooconfigure portal do Azure carrega o ficheiro do IoT hub tooenable de dispositivos ligados. Inclui informações sobre como configurar a conta de armazenamento do Azure de destino Olá."
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 915f1597-272d-4fd4-8c5b-a0ccb1df0d91
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/03/2017
ms.author: dobett
ms.openlocfilehash: b90c3fbed47b4eb144d3cb7480068b7cfc776ba6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-iot-hub-file-uploads-using-hello-azure-portal"></a>Configurar o IoT Hub carregamentos de ficheiros utilizando Olá portal do Azure

[!INCLUDE [iot-hub-file-upload-selector](../../includes/iot-hub-file-upload-selector.md)]

## <a name="file-upload"></a>Carregamento de ficheiros

Olá toouse [funcionalidade de carregamento de ficheiros no IoT Hub][lnk-upload], primeiro tem de associar uma conta de armazenamento do Azure com o seu hub. Selecione **carregamento de ficheiros** toodisplay uma lista de propriedades de carregamento de ficheiros para Olá do IoT hub que está a ser modificado.

![Ficheiro de IoT Hub da vista carregar as definições no portal de Olá][13]

**Contentor de armazenamento**: Utilize Olá tooselect portal do Azure, um contentor de BLOBs numa conta de armazenamento do Azure no seu atual tooassociate de subscrição do Azure com o seu IoT Hub. Se necessário, pode criar uma conta de armazenamento do Azure no Olá **contas do Storage** painel e BLOBs de contentor no Olá **contentores** painel. IoT Hub gera automaticamente SAS URIs com permissões de escrita toothis contentor de BLOBs para dispositivos toouse quando carregam estes ficheiros.

![Ver os contentores de armazenamento para o carregamento de ficheiros no portal de Olá][14]

**Receber notificações para os ficheiros carregados**: Ativar ou desativar notificações de carregamento de ficheiros através do botão de alternar Olá.

**TTL de SAS**: esta definição é Olá time-to-live das Olá SAS URIs devolvido toohello dispositivo ao IoT Hub. Definir a hora de tooone por predefinição, mas podem ser personalizado tooother valores a utilizar o controlo de deslize Olá.

**Notificação de definições predefinidas TTL ficheiros**: Olá time-to-live de uma notificação de carregamento do ficheiro antes de expirar. Definir o dia de tooone por predefinição, mas podem ser personalizado tooother valores a utilizar o controlo de deslize Olá.

**Contagem máxima de entrega de notificação de ficheiros**: número de Olá de vezes Olá IoT Hub tentativas toodeliver uma notificação de carregamento de ficheiros. Definir too10 por predefinição, mas podem ser personalizado tooother valores a utilizar o controlo de deslize Olá.

![Configurar o carregamento de ficheiros do IoT Hub no portal de Olá][15]

## <a name="next-steps"></a>Passos seguintes

Para obter mais informações sobre as capacidades de carregamento do ficheiro Olá do IoT Hub, consulte [carregar ficheiros a partir de um dispositivo] [ lnk-upload] no Olá guia para programadores do IoT Hub.

Siga estes toolearn ligações mais sobre a gestão do Azure IoT Hub:

* [Em massa gerir dispositivos de IoT][lnk-bulk]
* [Métricas de IoT Hub][lnk-metrics]
* [Operações de monitorização][lnk-monitor]

toofurther explorar Olá das capacidades do IoT Hub, consulte:

* [Guia para programadores do IoT Hub][lnk-devguide]
* [Simulando um dispositivo com o limite de IoT][lnk-iotedge]
* [Proteger a sua solução de IoT de Olá fundo cópias de segurança][lnk-securing]

[13]: ./media/iot-hub-configure-file-upload/file-upload-settings.png
[14]: ./media/iot-hub-configure-file-upload/file-upload-container-selection.png
[15]: ./media/iot-hub-configure-file-upload/file-upload-selected-container.png

[lnk-upload]: iot-hub-devguide-file-upload.md

[lnk-bulk]: iot-hub-bulk-identity-mgmt.md
[lnk-metrics]: iot-hub-metrics.md
[lnk-monitor]: iot-hub-operations-monitoring.md

[lnk-devguide]: iot-hub-devguide.md
[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
[lnk-securing]: iot-hub-security-ground-up.md
