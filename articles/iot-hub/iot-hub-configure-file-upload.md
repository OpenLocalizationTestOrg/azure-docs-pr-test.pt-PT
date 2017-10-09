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
# <a name="configure-iot-hub-file-uploads-using-hello-azure-portal"></a><span data-ttu-id="61d7f-104">Configurar o IoT Hub carregamentos de ficheiros utilizando Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="61d7f-104">Configure IoT Hub file uploads using hello Azure portal</span></span>

[!INCLUDE [iot-hub-file-upload-selector](../../includes/iot-hub-file-upload-selector.md)]

## <a name="file-upload"></a><span data-ttu-id="61d7f-105">Carregamento de ficheiros</span><span class="sxs-lookup"><span data-stu-id="61d7f-105">File upload</span></span>

<span data-ttu-id="61d7f-106">Olá toouse [funcionalidade de carregamento de ficheiros no IoT Hub][lnk-upload], primeiro tem de associar uma conta de armazenamento do Azure com o seu hub.</span><span class="sxs-lookup"><span data-stu-id="61d7f-106">toouse hello [file upload functionality in IoT Hub][lnk-upload], you must first associate an Azure Storage account with your hub.</span></span> <span data-ttu-id="61d7f-107">Selecione **carregamento de ficheiros** toodisplay uma lista de propriedades de carregamento de ficheiros para Olá do IoT hub que está a ser modificado.</span><span class="sxs-lookup"><span data-stu-id="61d7f-107">Select **File upload** toodisplay a list of file upload properties for hello IoT hub that is being modified.</span></span>

![Ficheiro de IoT Hub da vista carregar as definições no portal de Olá][13]

<span data-ttu-id="61d7f-109">**Contentor de armazenamento**: Utilize Olá tooselect portal do Azure, um contentor de BLOBs numa conta de armazenamento do Azure no seu atual tooassociate de subscrição do Azure com o seu IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="61d7f-109">**Storage container**: Use hello Azure portal tooselect a blob container in an Azure Storage account in your current Azure subscription tooassociate with your IoT Hub.</span></span> <span data-ttu-id="61d7f-110">Se necessário, pode criar uma conta de armazenamento do Azure no Olá **contas do Storage** painel e BLOBs de contentor no Olá **contentores** painel.</span><span class="sxs-lookup"><span data-stu-id="61d7f-110">If necessary, you can create an Azure Storage account on hello **Storage accounts** blade and blob container on hello **Containers** blade.</span></span> <span data-ttu-id="61d7f-111">IoT Hub gera automaticamente SAS URIs com permissões de escrita toothis contentor de BLOBs para dispositivos toouse quando carregam estes ficheiros.</span><span class="sxs-lookup"><span data-stu-id="61d7f-111">IoT Hub automatically generates SAS URIs with write permissions toothis blob container for devices toouse when they upload files.</span></span>

![Ver os contentores de armazenamento para o carregamento de ficheiros no portal de Olá][14]

<span data-ttu-id="61d7f-113">**Receber notificações para os ficheiros carregados**: Ativar ou desativar notificações de carregamento de ficheiros através do botão de alternar Olá.</span><span class="sxs-lookup"><span data-stu-id="61d7f-113">**Receive notifications for uploaded files**: Enable or disable file upload notifications via hello toggle.</span></span>

<span data-ttu-id="61d7f-114">**TTL de SAS**: esta definição é Olá time-to-live das Olá SAS URIs devolvido toohello dispositivo ao IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="61d7f-114">**SAS TTL**: This setting is hello time-to-live of hello SAS URIs returned toohello device by IoT Hub.</span></span> <span data-ttu-id="61d7f-115">Definir a hora de tooone por predefinição, mas podem ser personalizado tooother valores a utilizar o controlo de deslize Olá.</span><span class="sxs-lookup"><span data-stu-id="61d7f-115">Set tooone hour by default but can be customized tooother values using hello slider.</span></span>

<span data-ttu-id="61d7f-116">**Notificação de definições predefinidas TTL ficheiros**: Olá time-to-live de uma notificação de carregamento do ficheiro antes de expirar.</span><span class="sxs-lookup"><span data-stu-id="61d7f-116">**File notification settings default TTL**: hello time-to-live of a file upload notification before it is expired.</span></span> <span data-ttu-id="61d7f-117">Definir o dia de tooone por predefinição, mas podem ser personalizado tooother valores a utilizar o controlo de deslize Olá.</span><span class="sxs-lookup"><span data-stu-id="61d7f-117">Set tooone day by default but can be customized tooother values using hello slider.</span></span>

<span data-ttu-id="61d7f-118">**Contagem máxima de entrega de notificação de ficheiros**: número de Olá de vezes Olá IoT Hub tentativas toodeliver uma notificação de carregamento de ficheiros.</span><span class="sxs-lookup"><span data-stu-id="61d7f-118">**File notification maximum delivery count**: hello number of times hello IoT Hub attempts toodeliver a file upload notification.</span></span> <span data-ttu-id="61d7f-119">Definir too10 por predefinição, mas podem ser personalizado tooother valores a utilizar o controlo de deslize Olá.</span><span class="sxs-lookup"><span data-stu-id="61d7f-119">Set too10 by default but can be customized tooother values using hello slider.</span></span>

![Configurar o carregamento de ficheiros do IoT Hub no portal de Olá][15]

## <a name="next-steps"></a><span data-ttu-id="61d7f-121">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="61d7f-121">Next steps</span></span>

<span data-ttu-id="61d7f-122">Para obter mais informações sobre as capacidades de carregamento do ficheiro Olá do IoT Hub, consulte [carregar ficheiros a partir de um dispositivo] [ lnk-upload] no Olá guia para programadores do IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="61d7f-122">For more information about hello file upload capabilities of IoT Hub, see [Upload files from a device][lnk-upload] in hello IoT Hub developer guide.</span></span>

<span data-ttu-id="61d7f-123">Siga estes toolearn ligações mais sobre a gestão do Azure IoT Hub:</span><span class="sxs-lookup"><span data-stu-id="61d7f-123">Follow these links toolearn more about managing Azure IoT Hub:</span></span>

* <span data-ttu-id="61d7f-124">[Em massa gerir dispositivos de IoT][lnk-bulk]</span><span class="sxs-lookup"><span data-stu-id="61d7f-124">[Bulk manage IoT devices][lnk-bulk]</span></span>
* <span data-ttu-id="61d7f-125">[Métricas de IoT Hub][lnk-metrics]</span><span class="sxs-lookup"><span data-stu-id="61d7f-125">[IoT Hub metrics][lnk-metrics]</span></span>
* <span data-ttu-id="61d7f-126">[Operações de monitorização][lnk-monitor]</span><span class="sxs-lookup"><span data-stu-id="61d7f-126">[Operations monitoring][lnk-monitor]</span></span>

<span data-ttu-id="61d7f-127">toofurther explorar Olá das capacidades do IoT Hub, consulte:</span><span class="sxs-lookup"><span data-stu-id="61d7f-127">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="61d7f-128">[Guia para programadores do IoT Hub][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="61d7f-128">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="61d7f-129">[Simulando um dispositivo com o limite de IoT][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="61d7f-129">[Simulating a device with IoT Edge][lnk-iotedge]</span></span>
* <span data-ttu-id="61d7f-130">[Proteger a sua solução de IoT de Olá fundo cópias de segurança][lnk-securing]</span><span class="sxs-lookup"><span data-stu-id="61d7f-130">[Secure your IoT solution from hello ground up][lnk-securing]</span></span>

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
