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
# <a name="configure-iot-hub-file-uploads-using-azure-cli"></a><span data-ttu-id="89fc3-103">Configurar o IoT Hub carregamentos de ficheiros utilizando a CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="89fc3-103">Configure IoT Hub file uploads using Azure CLI</span></span>

[!INCLUDE [iot-hub-file-upload-selector](../../includes/iot-hub-file-upload-selector.md)]

<span data-ttu-id="89fc3-104">Olá toouse [funcionalidade de carregamento de ficheiros no IoT Hub][lnk-upload], tem primeiro de associar uma conta de armazenamento do Azure com o seu IoT hub.</span><span class="sxs-lookup"><span data-stu-id="89fc3-104">toouse hello [file upload functionality in IoT Hub][lnk-upload], you must first associate an Azure Storage account with your IoT hub.</span></span> <span data-ttu-id="89fc3-105">Pode utilizar uma conta de armazenamento existente ou crie um novo.</span><span class="sxs-lookup"><span data-stu-id="89fc3-105">You can use an existing storage account or create a new one.</span></span>

<span data-ttu-id="89fc3-106">toocomplete neste tutorial, terá de Olá seguintes:</span><span class="sxs-lookup"><span data-stu-id="89fc3-106">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="89fc3-107">Uma conta ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="89fc3-107">An active Azure account.</span></span> <span data-ttu-id="89fc3-108">Se não tiver uma conta, pode criar uma [conta gratuita][lnk-free-trial] em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="89fc3-108">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>
* <span data-ttu-id="89fc3-109">[CLI do Azure 2.0][lnk-CLI-install].</span><span class="sxs-lookup"><span data-stu-id="89fc3-109">[Azure CLI 2.0][lnk-CLI-install].</span></span>
* <span data-ttu-id="89fc3-110">Um hub IoT do Azure.</span><span class="sxs-lookup"><span data-stu-id="89fc3-110">An Azure IoT hub.</span></span> <span data-ttu-id="89fc3-111">Se não tiver um IoT hub, pode utilizar Olá `az iot hub create` [comando] [ lnk-cli-create-iothub] toocreate um ou utilize Olá portal demasiado [criar um hub IoT] [Ink-portal-hub].</span><span class="sxs-lookup"><span data-stu-id="89fc3-111">If you don't have an IoT hub, you can use hello `az iot hub create` [command][lnk-cli-create-iothub] toocreate one or use hello portal too[Create an IoT hub][lnk-portal-hub].</span></span>
* <span data-ttu-id="89fc3-112">Uma conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="89fc3-112">An Azure Storage account.</span></span> <span data-ttu-id="89fc3-113">Se não tiver uma conta de armazenamento do Azure, pode utilizar Olá [2.0 do CLI do Azure - gerir contas de armazenamento] [ lnk-manage-storage] toocreate um ou utilize Olá portal demasiado[criar uma conta de armazenamento] [lnk-portal-storage].</span><span class="sxs-lookup"><span data-stu-id="89fc3-113">If you don't have an Azure Storage account, you can use hello [Azure CLI 2.0 - Manage storage accounts][lnk-manage-storage] toocreate one or use hello portal too[Create a storage account][lnk-portal-storage].</span></span>

## <a name="sign-in-and-set-your-azure-account"></a><span data-ttu-id="89fc3-114">A iniciar sessão e definir a sua conta do Azure</span><span class="sxs-lookup"><span data-stu-id="89fc3-114">Sign in and set your Azure account</span></span>

<span data-ttu-id="89fc3-115">Inicie sessão tooyour conta do Azure e selecionar a sua subscrição.</span><span class="sxs-lookup"><span data-stu-id="89fc3-115">Sign in tooyour Azure account and select your subscription.</span></span>

1. <span data-ttu-id="89fc3-116">Na linha de comandos Olá, execute Olá [comando de início de sessão][lnk-login-command]:</span><span class="sxs-lookup"><span data-stu-id="89fc3-116">At hello command prompt, run hello [login command][lnk-login-command]:</span></span>

    ```azurecli
    az login
    ```

    <span data-ttu-id="89fc3-117">Siga Olá instruções tooauthenticate utilizando código Olá e inicie sessão tooyour conta do Azure através de um browser.</span><span class="sxs-lookup"><span data-stu-id="89fc3-117">Follow hello instructions tooauthenticate using hello code and sign in tooyour Azure account through a web browser.</span></span>

1. <span data-ttu-id="89fc3-118">Se tiver várias subscrições do Azure, iniciar sessão tooAzure concede acesso tooall Olá as contas do Azure associadas com as suas credenciais.</span><span class="sxs-lookup"><span data-stu-id="89fc3-118">If you have multiple Azure subscriptions, signing in tooAzure grants you access tooall hello Azure accounts associated with your credentials.</span></span> <span data-ttu-id="89fc3-119">Utilize o seguinte Olá [toolist comando Olá as contas do Azure] [ lnk-az-account-command] disponíveis para toouse:</span><span class="sxs-lookup"><span data-stu-id="89fc3-119">Use hello following [command toolist hello Azure accounts][lnk-az-account-command] available for you toouse:</span></span>

    ```azurecli
    az account list
    ```

    <span data-ttu-id="89fc3-120">Utilize Olá seguir subscrição tooselect de comando que pretende que o toouse toorun Olá comandos toocreate seu IoT hub.</span><span class="sxs-lookup"><span data-stu-id="89fc3-120">Use hello following command tooselect subscription that you want toouse toorun hello commands toocreate your IoT hub.</span></span> <span data-ttu-id="89fc3-121">Pode utilizar o nome da subscrição Olá ou o ID da saída de Olá do comando anterior Olá:</span><span class="sxs-lookup"><span data-stu-id="89fc3-121">You can use either hello subscription name or ID from hello output of hello previous command:</span></span>

    ```azurecli
    az account set --subscription {your subscription name or id}
    ```

## <a name="retrieve-your-storage-account-details"></a><span data-ttu-id="89fc3-122">Obter os detalhes de conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="89fc3-122">Retrieve your storage account details</span></span>

<span data-ttu-id="89fc3-123">Olá passos partem do princípio de que criou a conta de armazenamento com Olá **Resource Manager** modelo de implementação e não Olá **clássico** modelo de implementação.</span><span class="sxs-lookup"><span data-stu-id="89fc3-123">hello following steps assume that you created your storage account using hello **Resource Manager** deployment model, and not hello **Classic** deployment model.</span></span>

<span data-ttu-id="89fc3-124">ficheiro tooconfigure carrega dos seus dispositivos, precisa de cadeia de ligação de Olá para uma conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="89fc3-124">tooconfigure file uploads from your devices, you need hello connection string for an Azure storage account.</span></span> <span data-ttu-id="89fc3-125">conta de armazenamento Olá tem de constar Olá mesma subscrição do seu IoT hub.</span><span class="sxs-lookup"><span data-stu-id="89fc3-125">hello storage account must be in hello same subscription as your IoT hub.</span></span> <span data-ttu-id="89fc3-126">Também precisa de nome de Olá de um contentor de blob na conta do storage Olá.</span><span class="sxs-lookup"><span data-stu-id="89fc3-126">You also need hello name of a blob container in hello storage account.</span></span> <span data-ttu-id="89fc3-127">Utilize Olá tooretrieve de comando a seguir as chaves de conta de armazenamento:</span><span class="sxs-lookup"><span data-stu-id="89fc3-127">Use hello following command tooretrieve your storage account keys:</span></span>

```azurecli
az storage account show-connection-string --name {your storage account name} --resource-group {your storage account resource group}
```

<span data-ttu-id="89fc3-128">Tome nota do Olá **connectionString** valor.</span><span class="sxs-lookup"><span data-stu-id="89fc3-128">Make a note of hello **connectionString** value.</span></span> <span data-ttu-id="89fc3-129">Terá no Olá os seguintes passos.</span><span class="sxs-lookup"><span data-stu-id="89fc3-129">You need it in hello following steps.</span></span>

<span data-ttu-id="89fc3-130">Pode utilizar um contentor de blob existente para carregamentos de ficheiros ou crie uma nova:</span><span class="sxs-lookup"><span data-stu-id="89fc3-130">You can either use an existing blob container for your file uploads or create new one:</span></span>

* <span data-ttu-id="89fc3-131">contentores de BLOBs de existente de Olá do toolist na sua conta de armazenamento, utilize Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="89fc3-131">toolist hello existing blob containers in your storage account, use hello following command:</span></span>

    ```azurecli
    az storage container list --connection-string "{your storage account connection string}"
    ```

* <span data-ttu-id="89fc3-132">toocreate um contentor de BLOBs na sua conta de armazenamento, Olá utilize os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="89fc3-132">toocreate a blob container in your storage account, use hello following command:</span></span>

    ```azurecli
    az storage container create --name {container name} --connection-string "{your storage account connection string}"
    ```

## <a name="file-upload"></a><span data-ttu-id="89fc3-133">Carregamento de ficheiros</span><span class="sxs-lookup"><span data-stu-id="89fc3-133">File upload</span></span>

<span data-ttu-id="89fc3-134">Agora, pode configurar a sua tooenable de hub IoT [funcionalidade de carregamento de ficheiros] [ lnk-upload] utilizando os detalhes de conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="89fc3-134">You can now configure your IoT hub tooenable [file upload functionality][lnk-upload] using your storage account details.</span></span>

<span data-ttu-id="89fc3-135">configuração de Olá requer Olá os seguintes valores:</span><span class="sxs-lookup"><span data-stu-id="89fc3-135">hello configuration requires hello following values:</span></span>

<span data-ttu-id="89fc3-136">**Contentor de armazenamento**: um contentor de BLOBs numa conta de armazenamento do Azure no seu atual tooassociate de subscrição do Azure com o seu IoT hub.</span><span class="sxs-lookup"><span data-stu-id="89fc3-136">**Storage container**: A blob container in an Azure storage account in your current Azure subscription tooassociate with your IoT hub.</span></span> <span data-ttu-id="89fc3-137">Obter informações de conta de armazenamento necessário Olá no Olá anterior a secção.</span><span class="sxs-lookup"><span data-stu-id="89fc3-137">You retrieved hello necessary storage account information in hello preceding section.</span></span> <span data-ttu-id="89fc3-138">IoT Hub gera automaticamente SAS URIs com permissões de escrita toothis contentor de BLOBs para dispositivos toouse quando carregam estes ficheiros.</span><span class="sxs-lookup"><span data-stu-id="89fc3-138">IoT Hub automatically generates SAS URIs with write permissions toothis blob container for devices toouse when they upload files.</span></span>

<span data-ttu-id="89fc3-139">**Receber notificações para os ficheiros carregados**: Ativar ou desativar notificações de carregamento de ficheiros.</span><span class="sxs-lookup"><span data-stu-id="89fc3-139">**Receive notifications for uploaded files**: Enable or disable file upload notifications.</span></span>

<span data-ttu-id="89fc3-140">**TTL de SAS**: esta definição é Olá time-to-live das Olá SAS URIs devolvido toohello dispositivo ao IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="89fc3-140">**SAS TTL**: This setting is hello time-to-live of hello SAS URIs returned toohello device by IoT Hub.</span></span> <span data-ttu-id="89fc3-141">Definir a hora de tooone por predefinição.</span><span class="sxs-lookup"><span data-stu-id="89fc3-141">Set tooone hour by default.</span></span>

<span data-ttu-id="89fc3-142">**Notificação de definições predefinidas TTL ficheiros**: Olá time-to-live de uma notificação de carregamento do ficheiro antes de expirar.</span><span class="sxs-lookup"><span data-stu-id="89fc3-142">**File notification settings default TTL**: hello time-to-live of a file upload notification before it is expired.</span></span> <span data-ttu-id="89fc3-143">Definir o dia de tooone por predefinição.</span><span class="sxs-lookup"><span data-stu-id="89fc3-143">Set tooone day by default.</span></span>

<span data-ttu-id="89fc3-144">**Contagem máxima de entrega de notificação de ficheiros**: número de Olá de vezes Olá IoT Hub tentativas toodeliver uma notificação de carregamento de ficheiros.</span><span class="sxs-lookup"><span data-stu-id="89fc3-144">**File notification maximum delivery count**: hello number of times hello IoT Hub attempts toodeliver a file upload notification.</span></span> <span data-ttu-id="89fc3-145">Definir too10 por predefinição.</span><span class="sxs-lookup"><span data-stu-id="89fc3-145">Set too10 by default.</span></span>

<span data-ttu-id="89fc3-146">Utilize Olá seguintes definições de carregamento de ficheiros de Olá tooconfigure comandos CLI do Azure no seu IoT hub:</span><span class="sxs-lookup"><span data-stu-id="89fc3-146">Use hello following Azure CLI commands tooconfigure hello file upload settings on your IoT hub:</span></span>

<span data-ttu-id="89fc3-147">Uma utilização da shell de bash:</span><span class="sxs-lookup"><span data-stu-id="89fc3-147">In a bash shell use:</span></span>

```azurecli
az iot hub update --name {your iot hub name} --set properties.storageEndpoints.'$default'.connectionString="{your storage account connection string}"
az iot hub update --name {your iot hub name} --set properties.storageEndpoints.'$default'.containerName="{your storage container name}"
az iot hub update --name {your iot hub name} --set properties.storageEndpoints.'$default'.sasTtlAsIso8601=PT1H0M0S

az iot hub update --name {your iot hub name} --set properties.enableFileUploadNotifications=true
az iot hub update --name {your iot hub name} --set properties.messagingEndpoints.fileNotifications.maxDeliveryCount=10
az iot hub update --name {your iot hub name} --set properties.messagingEndpoints.fileNotifications.ttlAsIso8601=PT1H0M0S
```

<span data-ttu-id="89fc3-148">Cada uma utilização de linha de comandos do Windows:</span><span class="sxs-lookup"><span data-stu-id="89fc3-148">At a Windows command prompt use:</span></span>

```azurecli
az iot hub update --name {your iot hub name} --set "properties.storageEndpoints.$default.connectionString="{your storage account connection string}""
az iot hub update --name {your iot hub name} --set "properties.storageEndpoints.$default.containerName="{your storage container name}""
az iot hub update --name {your iot hub name} --set "properties.storageEndpoints.$default.sasTtlAsIso8601=PT1H0M0S"

az iot hub update --name {your iot hub name} --set properties.enableFileUploadNotifications=true
az iot hub update --name {your iot hub name} --set properties.messagingEndpoints.fileNotifications.maxDeliveryCount=10
az iot hub update --name {your iot hub name} --set properties.messagingEndpoints.fileNotifications.ttlAsIso8601=PT1H0M0S
```

<span data-ttu-id="89fc3-149">Pode rever a configuração de carregamento de ficheiros de Olá no seu IoT hub com Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="89fc3-149">You can review hello file upload configuration on your IoT hub using hello following command:</span></span>

```azurecli
az iot hub show --name {your iot hub name}
```

## <a name="next-steps"></a><span data-ttu-id="89fc3-150">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="89fc3-150">Next steps</span></span>

<span data-ttu-id="89fc3-151">Para obter mais informações sobre as capacidades de carregamento do ficheiro Olá do IoT Hub, consulte [carregar ficheiros a partir de um dispositivo][lnk-upload].</span><span class="sxs-lookup"><span data-stu-id="89fc3-151">For more information about hello file upload capabilities of IoT Hub, see [Upload files from a device][lnk-upload].</span></span>

<span data-ttu-id="89fc3-152">Siga estes toolearn ligações mais sobre a gestão do Azure IoT Hub:</span><span class="sxs-lookup"><span data-stu-id="89fc3-152">Follow these links toolearn more about managing Azure IoT Hub:</span></span>

* <span data-ttu-id="89fc3-153">[Em massa gerir dispositivos de IoT][lnk-bulk]</span><span class="sxs-lookup"><span data-stu-id="89fc3-153">[Bulk manage IoT devices][lnk-bulk]</span></span>
* <span data-ttu-id="89fc3-154">[Métricas de IoT Hub][lnk-metrics]</span><span class="sxs-lookup"><span data-stu-id="89fc3-154">[IoT Hub metrics][lnk-metrics]</span></span>
* <span data-ttu-id="89fc3-155">[Operações de monitorização][lnk-monitor]</span><span class="sxs-lookup"><span data-stu-id="89fc3-155">[Operations monitoring][lnk-monitor]</span></span>

<span data-ttu-id="89fc3-156">toofurther explorar Olá das capacidades do IoT Hub, consulte:</span><span class="sxs-lookup"><span data-stu-id="89fc3-156">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="89fc3-157">[Guia para programadores do IoT Hub][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="89fc3-157">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="89fc3-158">[Simulando um dispositivo com o limite de IoT][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="89fc3-158">[Simulating a device with IoT Edge][lnk-iotedge]</span></span>
* <span data-ttu-id="89fc3-159">[Proteger a sua solução de IoT de Olá fundo cópias de segurança][lnk-securing]</span><span class="sxs-lookup"><span data-stu-id="89fc3-159">[Secure your IoT solution from hello ground up][lnk-securing]</span></span>

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