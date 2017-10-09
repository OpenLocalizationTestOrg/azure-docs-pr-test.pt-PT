---
title: "aaaCreate um IoT Hub do Azure através de um modelo (PowerShell) | Microsoft Docs"
description: Como toouse um toocreate de modelo do Azure Resource Manager um IoT Hub com o PowerShell.
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 7eade855-c289-4ffb-b5ef-02be8c5f670f
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: dobett
ms.openlocfilehash: e98ff5e898200cd727b9326fb3df393e43b021e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-iot-hub-using-azure-resource-manager-template-powershell"></a><span data-ttu-id="19e37-103">Criar um hub IoT utilizando o modelo Azure Resource Manager (PowerShell)</span><span class="sxs-lookup"><span data-stu-id="19e37-103">Create an IoT hub using Azure Resource Manager template (PowerShell)</span></span>

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

<span data-ttu-id="19e37-104">Pode utilizar o Azure Resource Manager toocreate e gerir os hubs IoT do Azure através de programação.</span><span class="sxs-lookup"><span data-stu-id="19e37-104">You can use Azure Resource Manager toocreate and manage Azure IoT hubs programmatically.</span></span> <span data-ttu-id="19e37-105">Este tutorial mostra como toouse um toocreate de modelo do Azure Resource Manager um IoT hub com o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="19e37-105">This tutorial shows you how toouse an Azure Resource Manager template toocreate an IoT hub with PowerShell.</span></span>

> [!NOTE]
> <span data-ttu-id="19e37-106">O Azure tem dois modelos de implementação diferentes para criar e trabalhar com recursos: [do Azure Resource Manager e clássico](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="19e37-106">Azure has two different deployment models for creating and working with resources: [Azure Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="19e37-107">Este artigo abrange utilizando o modelo de implementação Azure Resource Manager Olá.</span><span class="sxs-lookup"><span data-stu-id="19e37-107">This article covers using hello Azure Resource Manager deployment model.</span></span>

<span data-ttu-id="19e37-108">toocomplete neste tutorial, terá de Olá seguintes:</span><span class="sxs-lookup"><span data-stu-id="19e37-108">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="19e37-109">Uma conta ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="19e37-109">An active Azure account.</span></span> <br/><span data-ttu-id="19e37-110">Se não tiver uma conta, pode criar uma [conta gratuita][lnk-free-trial] em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="19e37-110">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>
* <span data-ttu-id="19e37-111">[Azure PowerShell 1.0] [ lnk-powershell-install] ou posterior.</span><span class="sxs-lookup"><span data-stu-id="19e37-111">[Azure PowerShell 1.0][lnk-powershell-install] or later.</span></span>

> [!TIP]
> <span data-ttu-id="19e37-112">artigo de Olá [utilizar o Azure PowerShell com o Azure Resource Manager] [ lnk-powershell-arm] fornece mais informações sobre como toouse de PowerShell e o Azure Resource Manager de toocreate de modelos do Azure recursos.</span><span class="sxs-lookup"><span data-stu-id="19e37-112">hello article [Using Azure PowerShell with Azure Resource Manager][lnk-powershell-arm] provides more information about how toouse PowerShell and Azure Resource Manager templates toocreate Azure resources.</span></span>

## <a name="connect-tooyour-azure-subscription"></a><span data-ttu-id="19e37-113">Ligar tooyour subscrição do Azure</span><span class="sxs-lookup"><span data-stu-id="19e37-113">Connect tooyour Azure subscription</span></span>

<span data-ttu-id="19e37-114">Numa linha de comandos do PowerShell, introduza Olá os seguintes comandos toosign no tooyour subscrição do Azure:</span><span class="sxs-lookup"><span data-stu-id="19e37-114">In a PowerShell command prompt, enter hello following command toosign in tooyour Azure subscription:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="19e37-115">Se tiver várias subscrições do Azure, iniciar sessão tooAzure concede acesso tooall Olá subscrições Azure associadas as suas credenciais.</span><span class="sxs-lookup"><span data-stu-id="19e37-115">If you have multiple Azure subscriptions, signing in tooAzure grants you access tooall hello Azure subscriptions associated with your credentials.</span></span> <span data-ttu-id="19e37-116">Utilize Olá toolist Olá subscrições do Azure disponíveis para si toouse de comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="19e37-116">Use hello following command toolist hello Azure subscriptions available for you toouse:</span></span>

```powershell
Get-AzureRMSubscription
```

<span data-ttu-id="19e37-117">Utilize Olá seguir subscrição tooselect de comando que pretende que o toouse toorun Olá comandos toocreate seu IoT hub.</span><span class="sxs-lookup"><span data-stu-id="19e37-117">Use hello following command tooselect subscription that you want toouse toorun hello commands toocreate your IoT hub.</span></span> <span data-ttu-id="19e37-118">Pode utilizar o nome da subscrição Olá ou o ID da saída de Olá do comando anterior Olá:</span><span class="sxs-lookup"><span data-stu-id="19e37-118">You can use either hello subscription name or ID from hello output of hello previous command:</span></span>

```powershell
Select-AzureRMSubscription `
    -SubscriptionName "{your subscription name}"
```

<span data-ttu-id="19e37-119">Pode utilizar Olá os seguintes comandos toodiscover onde pode implementar um hub IoT e Olá atualmente suportado versões de API:</span><span class="sxs-lookup"><span data-stu-id="19e37-119">You can use hello following commands toodiscover where you can deploy an IoT hub and hello currently supported API versions:</span></span>

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Devices).ResourceTypes | Where-Object ResourceTypeName -eq IoTHubs).Locations
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Devices).ResourceTypes | Where-Object ResourceTypeName -eq IoTHubs).ApiVersions
```

<span data-ttu-id="19e37-120">Crie um toocontain do grupo de recursos com o IoT hub com Olá os seguintes comandos das localizações de Olá suportado para o IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="19e37-120">Create a resource group toocontain your IoT hub using hello following command in one of hello supported locations for IoT Hub.</span></span> <span data-ttu-id="19e37-121">Este exemplo cria um grupo de recursos denominado **MyIoTRG1**:</span><span class="sxs-lookup"><span data-stu-id="19e37-121">This example creates a resource group called **MyIoTRG1**:</span></span>

```powershell
New-AzureRmResourceGroup -Name MyIoTRG1 -Location "East US"
```

## <a name="submit-a-template-toocreate-an-iot-hub"></a><span data-ttu-id="19e37-122">Submeter um toocreate modelo um hub IoT</span><span class="sxs-lookup"><span data-stu-id="19e37-122">Submit a template toocreate an IoT hub</span></span>

<span data-ttu-id="19e37-123">Utilize um toocreate de modelo JSON um IoT hub no seu grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="19e37-123">Use a JSON template toocreate an IoT hub in your resource group.</span></span> <span data-ttu-id="19e37-124">Também pode utilizar um Gestor de recursos do Azure modelo toomake alterações tooan IoT hub.</span><span class="sxs-lookup"><span data-stu-id="19e37-124">You can also use an Azure Resource Manager template toomake changes tooan existing IoT hub.</span></span>

1. <span data-ttu-id="19e37-125">Utilize um toocreate do editor de texto chamado de um modelo Azure Resource Manager **Template** com Olá seguintes toocreate de definição do recurso de um novo IoT hub padrão.</span><span class="sxs-lookup"><span data-stu-id="19e37-125">Use a text editor toocreate an Azure Resource Manager template called **template.json** with hello following resource definition toocreate a new standard IoT hub.</span></span> <span data-ttu-id="19e37-126">Este exemplo adiciona Olá IoT Hub na Olá **EUA Leste** região, cria dois grupos de consumidores (**cg1** e **cg2**) no ponto final de Olá compatível com o Event Hub e utiliza Olá **2016-02-03** versão da API.</span><span class="sxs-lookup"><span data-stu-id="19e37-126">This example adds hello IoT Hub in hello **East US** region, creates two consumer groups (**cg1** and **cg2**) on hello Event Hub-compatible endpoint, and uses hello **2016-02-03** API version.</span></span> <span data-ttu-id="19e37-127">Este modelo também espera toopass no nome de hub IoT Olá como um parâmetro denominado **hubName**.</span><span class="sxs-lookup"><span data-stu-id="19e37-127">This template also expects you toopass in hello IoT hub name as a parameter called **hubName**.</span></span> <span data-ttu-id="19e37-128">Para a lista atual de Olá de localizações que suportam o IoT Hub consulte [Azure estado][lnk-status].</span><span class="sxs-lookup"><span data-stu-id="19e37-128">For hello current list of locations that support IoT Hub see [Azure Status][lnk-status].</span></span>

    ```json
    {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
      "contentVersion": "1.0.0.0",
      "parameters": {
        "hubName": {
          "type": "string"
        }
      },
      "resources": [
      {
        "apiVersion": "2016-02-03",
        "type": "Microsoft.Devices/IotHubs",
        "name": "[parameters('hubName')]",
        "location": "East US",
        "sku": {
          "name": "S1",
          "tier": "Standard",
          "capacity": 1
        },
        "properties": {
          "location": "East US"
        }
      },
      {
        "apiVersion": "2016-02-03",
        "type": "Microsoft.Devices/IotHubs/eventhubEndpoints/ConsumerGroups",
        "name": "[concat(parameters('hubName'), '/events/cg1')]",
        "dependsOn": [
          "[concat('Microsoft.Devices/Iothubs/', parameters('hubName'))]"
        ]
      },
      {
        "apiVersion": "2016-02-03",
        "type": "Microsoft.Devices/IotHubs/eventhubEndpoints/ConsumerGroups",
        "name": "[concat(parameters('hubName'), '/events/cg2')]",
        "dependsOn": [
          "[concat('Microsoft.Devices/Iothubs/', parameters('hubName'))]"
        ]
      }
      ],
      "outputs": {
        "hubKeys": {
          "value": "[listKeys(resourceId('Microsoft.Devices/IotHubs', parameters('hubName')), '2016-02-03')]",
          "type": "object"
        }
      }
    }
    ```

2. <span data-ttu-id="19e37-129">Guarde o ficheiro de modelo do Azure Resource Manager Olá no seu computador local.</span><span class="sxs-lookup"><span data-stu-id="19e37-129">Save hello Azure Resource Manager template file on your local machine.</span></span> <span data-ttu-id="19e37-130">Este exemplo assume que guarde-o numa pasta chamada **c:\templates**.</span><span class="sxs-lookup"><span data-stu-id="19e37-130">This example assumes you save it in a folder called **c:\templates**.</span></span>

3. <span data-ttu-id="19e37-131">Execute Olá os seguintes comandos toodeploy novo hub IoT, transmitir o nome de Olá do seu IoT hub como um parâmetro.</span><span class="sxs-lookup"><span data-stu-id="19e37-131">Run hello following command toodeploy your new IoT hub, passing hello name of your IoT hub as a parameter.</span></span> <span data-ttu-id="19e37-132">Neste exemplo, o nome de Olá do hub IoT de Olá é `abcmyiothub`.</span><span class="sxs-lookup"><span data-stu-id="19e37-132">In this example, hello name of hello IoT hub is `abcmyiothub`.</span></span> <span data-ttu-id="19e37-133">nome de Olá do seu IoT hub deve ser globalmente exclusivo:</span><span class="sxs-lookup"><span data-stu-id="19e37-133">hello name of your IoT hub must be globally unique:</span></span>

    ```powershell
    New-AzureRmResourceGroupDeployment -ResourceGroupName MyIoTRG1 -TemplateFile C:\templates\template.json -hubName abcmyiothub
    ```
  [!INCLUDE [iot-hub-pii-note-naming-hub](../../includes/iot-hub-pii-note-naming-hub.md)]

4. <span data-ttu-id="19e37-134">saída de Olá apresenta Olá as chaves de Olá IoT hub que criou.</span><span class="sxs-lookup"><span data-stu-id="19e37-134">hello output displays hello keys for hello IoT hub you created.</span></span>

5. <span data-ttu-id="19e37-135">tooverify adicionada a sua aplicação Olá novo IoT hub, visite Olá [portal do Azure] [ lnk-azure-portal] e ver a lista de recursos.</span><span class="sxs-lookup"><span data-stu-id="19e37-135">tooverify your application added hello new IoT hub, visit hello [Azure portal][lnk-azure-portal] and view your list of resources.</span></span> <span data-ttu-id="19e37-136">Em alternativa, utilize Olá **Get-AzureRmResource** cmdlet do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="19e37-136">Alternatively, use hello **Get-AzureRmResource** PowerShell cmdlet.</span></span>

> [!NOTE]
> <span data-ttu-id="19e37-137">Esta aplicação de exemplo adiciona uma S1 Standard IoT Hub para o qual é-lhe faturado.</span><span class="sxs-lookup"><span data-stu-id="19e37-137">This example application adds an S1 Standard IoT Hub for which you are billed.</span></span> <span data-ttu-id="19e37-138">Pode eliminar o hub IoT de Olá através de Olá [portal do Azure] [ lnk-azure-portal] ou utilizando Olá **remover AzureRmResource** cmdlet do PowerShell quando tiver terminado.</span><span class="sxs-lookup"><span data-stu-id="19e37-138">You can delete hello IoT hub through hello [Azure portal][lnk-azure-portal] or by using hello **Remove-AzureRmResource** PowerShell cmdlet when you are finished.</span></span>

## <a name="next-steps"></a><span data-ttu-id="19e37-139">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="19e37-139">Next steps</span></span>

<span data-ttu-id="19e37-140">Agora que implementou um IoT hub utilizando um modelo Azure Resource Manager com o PowerShell, poderá ser útil tooexplore mais:</span><span class="sxs-lookup"><span data-stu-id="19e37-140">Now you have deployed an IoT hub using an Azure Resource Manager template with PowerShell, you may want tooexplore further:</span></span>

* <span data-ttu-id="19e37-141">Leia sobre as capacidades de Olá de Olá [fornecedor de recursos do IoT Hub REST API][lnk-rest-api].</span><span class="sxs-lookup"><span data-stu-id="19e37-141">Read about hello capabilities of hello [IoT Hub resource provider REST API][lnk-rest-api].</span></span>
* <span data-ttu-id="19e37-142">Leitura [descrição geral do Azure Resource Manager] [ lnk-azure-rm-overview] toolearn mais sobre as capacidades de Olá do Gestor de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="19e37-142">Read [Azure Resource Manager overview][lnk-azure-rm-overview] toolearn more about hello capabilities of Azure Resource Manager.</span></span>

<span data-ttu-id="19e37-143">toolearn mais informações sobre desenvolver para o IoT Hub, consulte Olá seguintes artigos:</span><span class="sxs-lookup"><span data-stu-id="19e37-143">toolearn more about developing for IoT Hub, see hello following articles:</span></span>

* <span data-ttu-id="19e37-144">[Introdução tooC SDK][lnk-c-sdk]</span><span class="sxs-lookup"><span data-stu-id="19e37-144">[Introduction tooC SDK][lnk-c-sdk]</span></span>
* <span data-ttu-id="19e37-145">[SDKs IoT do Azure][lnk-sdks]</span><span class="sxs-lookup"><span data-stu-id="19e37-145">[Azure IoT SDKs][lnk-sdks]</span></span>

<span data-ttu-id="19e37-146">toofurther explorar Olá das capacidades do IoT Hub, consulte:</span><span class="sxs-lookup"><span data-stu-id="19e37-146">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="19e37-147">[Simulando um dispositivo com o Azure IoT Edge][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="19e37-147">[Simulating a device with Azure IoT Edge][lnk-iotedge]</span></span>

<!-- Links -->
[lnk-free-trial]: https://azure.microsoft.com/pricing/free-trial/
[lnk-azure-portal]: https://portal.azure.com/
[lnk-status]: https://azure.microsoft.com/status/
[lnk-powershell-install]: /powershell/azure/install-azurerm-ps
[lnk-rest-api]: https://docs.microsoft.com/rest/api/iothub/iothubresource
[lnk-azure-rm-overview]: ../azure-resource-manager/resource-group-overview.md
[lnk-powershell-arm]: ../azure-resource-manager/powershell-azure-resource-manager.md

[lnk-c-sdk]: iot-hub-device-sdk-c-intro.md
[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
