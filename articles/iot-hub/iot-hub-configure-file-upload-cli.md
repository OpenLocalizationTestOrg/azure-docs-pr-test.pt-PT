---
title: tooIoT de carregamento de ficheiros aaaConfigure Hub utilizando a CLI do Azure (az.py) | Microsoft Docs
description: "Como utilizar o IoT Hub tooconfigure fileuploads tooAzure Olá plataforma Azure CLI 2.0 (az.py)."
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
ms.date: 08/08/2017
ms.author: dobett
ms.openlocfilehash: 390113df2d96df9833b6aa383ed66805528614a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-iot-hub-file-uploads-using-azure-cli"></a>Configurar o IoT Hub carregamentos de ficheiros utilizando a CLI do Azure

[!INCLUDE [iot-hub-file-upload-selector](../../includes/iot-hub-file-upload-selector.md)]

Olá toouse [funcionalidade de carregamento de ficheiros no IoT Hub][lnk-upload], tem primeiro de associar uma conta de armazenamento do Azure com o seu IoT hub. Pode utilizar uma conta de armazenamento existente ou crie um novo.

toocomplete neste tutorial, terá de Olá seguintes:

* Uma conta ativa do Azure. Se não tiver uma conta, pode criar uma [conta gratuita][lnk-free-trial] em apenas alguns minutos.
* [CLI do Azure 2.0][lnk-CLI-install].
* Um hub IoT do Azure. Se não tiver um IoT hub, pode utilizar Olá `az iot hub create` [comando] [ lnk-cli-create-iothub] toocreate um ou utilize Olá portal demasiado [criar um hub IoT] [Ink-portal-hub].
* Uma conta de armazenamento do Azure. Se não tiver uma conta de armazenamento do Azure, pode utilizar Olá [2.0 do CLI do Azure - gerir contas de armazenamento] [ lnk-manage-storage] toocreate um ou utilize Olá portal demasiado[criar uma conta de armazenamento] [lnk-portal-storage].

## <a name="sign-in-and-set-your-azure-account"></a>A iniciar sessão e definir a sua conta do Azure

Inicie sessão tooyour conta do Azure e selecionar a sua subscrição.

1. Na linha de comandos Olá, execute Olá [comando de início de sessão][lnk-login-command]:

    ```azurecli
    az login
    ```

    Siga Olá instruções tooauthenticate utilizando código Olá e inicie sessão tooyour conta do Azure através de um browser.

1. Se tiver várias subscrições do Azure, iniciar sessão tooAzure concede acesso tooall Olá as contas do Azure associadas com as suas credenciais. Utilize o seguinte Olá [toolist comando Olá as contas do Azure] [ lnk-az-account-command] disponíveis para toouse:

    ```azurecli
    az account list
    ```

    Utilize Olá seguir subscrição tooselect de comando que pretende que o toouse toorun Olá comandos toocreate seu IoT hub. Pode utilizar o nome da subscrição Olá ou o ID da saída de Olá do comando anterior Olá:

    ```azurecli
    az account set --subscription {your subscription name or id}
    ```

## <a name="retrieve-your-storage-account-details"></a>Obter os detalhes de conta de armazenamento

Olá passos partem do princípio de que criou a conta de armazenamento com Olá **Resource Manager** modelo de implementação e não Olá **clássico** modelo de implementação.

ficheiro tooconfigure carrega dos seus dispositivos, precisa de cadeia de ligação de Olá para uma conta de armazenamento do Azure. conta de armazenamento Olá tem de constar Olá mesma subscrição do seu IoT hub. Também precisa de nome de Olá de um contentor de blob na conta do storage Olá. Utilize Olá tooretrieve de comando a seguir as chaves de conta de armazenamento:

```azurecli
az storage account show-connection-string --name {your storage account name} --resource-group {your storage account resource group}
```

Tome nota do Olá **connectionString** valor. Terá no Olá os seguintes passos.

Pode utilizar um contentor de blob existente para carregamentos de ficheiros ou crie uma nova:

* contentores de BLOBs de existente de Olá do toolist na sua conta de armazenamento, utilize Olá os seguintes comandos:

    ```azurecli
    az storage container list --connection-string "{your storage account connection string}"
    ```

* toocreate um contentor de BLOBs na sua conta de armazenamento, Olá utilize os seguintes comandos:

    ```azurecli
    az storage container create --name {container name} --connection-string "{your storage account connection string}"
    ```

## <a name="file-upload"></a>Carregamento de ficheiros

Agora, pode configurar a sua tooenable de hub IoT [funcionalidade de carregamento de ficheiros] [ lnk-upload] utilizando os detalhes de conta de armazenamento.

configuração de Olá requer Olá os seguintes valores:

**Contentor de armazenamento**: um contentor de BLOBs numa conta de armazenamento do Azure no seu atual tooassociate de subscrição do Azure com o seu IoT hub. Obter informações de conta de armazenamento necessário Olá no Olá anterior a secção. IoT Hub gera automaticamente SAS URIs com permissões de escrita toothis contentor de BLOBs para dispositivos toouse quando carregam estes ficheiros.

**Receber notificações para os ficheiros carregados**: Ativar ou desativar notificações de carregamento de ficheiros.

**TTL de SAS**: esta definição é Olá time-to-live das Olá SAS URIs devolvido toohello dispositivo ao IoT Hub. Definir a hora de tooone por predefinição.

**Notificação de definições predefinidas TTL ficheiros**: Olá time-to-live de uma notificação de carregamento do ficheiro antes de expirar. Definir o dia de tooone por predefinição.

**Contagem máxima de entrega de notificação de ficheiros**: número de Olá de vezes Olá IoT Hub tentativas toodeliver uma notificação de carregamento de ficheiros. Definir too10 por predefinição.

Utilize Olá seguintes definições de carregamento de ficheiros de Olá tooconfigure comandos CLI do Azure no seu IoT hub:

Uma utilização da shell de bash:

```azurecli
az iot hub update --name {your iot hub name} --set properties.storageEndpoints.'$default'.connectionString="{your storage account connection string}"
az iot hub update --name {your iot hub name} --set properties.storageEndpoints.'$default'.containerName="{your storage container name}"
az iot hub update --name {your iot hub name} --set properties.storageEndpoints.'$default'.sasTtlAsIso8601=PT1H0M0S

az iot hub update --name {your iot hub name} --set properties.enableFileUploadNotifications=true
az iot hub update --name {your iot hub name} --set properties.messagingEndpoints.fileNotifications.maxDeliveryCount=10
az iot hub update --name {your iot hub name} --set properties.messagingEndpoints.fileNotifications.ttlAsIso8601=PT1H0M0S
```

Cada uma utilização de linha de comandos do Windows:

```azurecli
az iot hub update --name {your iot hub name} --set "properties.storageEndpoints.$default.connectionString="{your storage account connection string}""
az iot hub update --name {your iot hub name} --set "properties.storageEndpoints.$default.containerName="{your storage container name}""
az iot hub update --name {your iot hub name} --set "properties.storageEndpoints.$default.sasTtlAsIso8601=PT1H0M0S"

az iot hub update --name {your iot hub name} --set properties.enableFileUploadNotifications=true
az iot hub update --name {your iot hub name} --set properties.messagingEndpoints.fileNotifications.maxDeliveryCount=10
az iot hub update --name {your iot hub name} --set properties.messagingEndpoints.fileNotifications.ttlAsIso8601=PT1H0M0S
```

Pode rever a configuração de carregamento de ficheiros de Olá no seu IoT hub com Olá os seguintes comandos:

```azurecli
az iot hub show --name {your iot hub name}
```

## <a name="next-steps"></a>Passos seguintes

Para obter mais informações sobre as capacidades de carregamento do ficheiro Olá do IoT Hub, consulte [carregar ficheiros a partir de um dispositivo][lnk-upload].

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


[lnk-free-trial]: https://azure.microsoft.com/pricing/free-trial/
[lnk-CLI-install]: https://docs.microsoft.com/cli/azure/install-az-cli2
[lnk-login-command]: https://docs.microsoft.com/cli/azure/get-started-with-az-cli2
[lnk-az-account-command]: https://docs.microsoft.com/cli/azure/account
[lnk-az-register-command]: https://docs.microsoft.com/cli/azure/provider
[lnk-az-addcomponent-command]: https://docs.microsoft.com/cli/azure/component
[lnk-az-resource-command]: https://docs.microsoft.com/cli/azure/resource
[lnk-az-iot-command]: https://docs.microsoft.com/cli/azure/iot
[lnk-iot-pricing]: https://azure.microsoft.com/pricing/details/iot-hub/
[lnk-manage-storage]:../storage/common/storage-azure-cli.md#manage-storage-accounts
[lnk-portal-storage]:../storage/common/storage-create-storage-account.md
[lnk-cli-create-iothub]: https://docs.microsoft.com/cli/azure/iot/hub#create