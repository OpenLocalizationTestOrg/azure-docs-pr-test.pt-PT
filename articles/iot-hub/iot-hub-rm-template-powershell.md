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
# <a name="create-an-iot-hub-using-azure-resource-manager-template-powershell"></a>Criar um hub IoT utilizando o modelo Azure Resource Manager (PowerShell)

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

Pode utilizar o Azure Resource Manager toocreate e gerir os hubs IoT do Azure através de programação. Este tutorial mostra como toouse um toocreate de modelo do Azure Resource Manager um IoT hub com o PowerShell.

> [!NOTE]
> O Azure tem dois modelos de implementação diferentes para criar e trabalhar com recursos: [do Azure Resource Manager e clássico](../azure-resource-manager/resource-manager-deployment-model.md). Este artigo abrange utilizando o modelo de implementação Azure Resource Manager Olá.

toocomplete neste tutorial, terá de Olá seguintes:

* Uma conta ativa do Azure. <br/>Se não tiver uma conta, pode criar uma [conta gratuita][lnk-free-trial] em apenas alguns minutos.
* [Azure PowerShell 1.0] [ lnk-powershell-install] ou posterior.

> [!TIP]
> artigo de Olá [utilizar o Azure PowerShell com o Azure Resource Manager] [ lnk-powershell-arm] fornece mais informações sobre como toouse de PowerShell e o Azure Resource Manager de toocreate de modelos do Azure recursos.

## <a name="connect-tooyour-azure-subscription"></a>Ligar tooyour subscrição do Azure

Numa linha de comandos do PowerShell, introduza Olá os seguintes comandos toosign no tooyour subscrição do Azure:

```powershell
Login-AzureRmAccount
```

Se tiver várias subscrições do Azure, iniciar sessão tooAzure concede acesso tooall Olá subscrições Azure associadas as suas credenciais. Utilize Olá toolist Olá subscrições do Azure disponíveis para si toouse de comando a seguir:

```powershell
Get-AzureRMSubscription
```

Utilize Olá seguir subscrição tooselect de comando que pretende que o toouse toorun Olá comandos toocreate seu IoT hub. Pode utilizar o nome da subscrição Olá ou o ID da saída de Olá do comando anterior Olá:

```powershell
Select-AzureRMSubscription `
    -SubscriptionName "{your subscription name}"
```

Pode utilizar Olá os seguintes comandos toodiscover onde pode implementar um hub IoT e Olá atualmente suportado versões de API:

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Devices).ResourceTypes | Where-Object ResourceTypeName -eq IoTHubs).Locations
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Devices).ResourceTypes | Where-Object ResourceTypeName -eq IoTHubs).ApiVersions
```

Crie um toocontain do grupo de recursos com o IoT hub com Olá os seguintes comandos das localizações de Olá suportado para o IoT Hub. Este exemplo cria um grupo de recursos denominado **MyIoTRG1**:

```powershell
New-AzureRmResourceGroup -Name MyIoTRG1 -Location "East US"
```

## <a name="submit-a-template-toocreate-an-iot-hub"></a>Submeter um toocreate modelo um hub IoT

Utilize um toocreate de modelo JSON um IoT hub no seu grupo de recursos. Também pode utilizar um Gestor de recursos do Azure modelo toomake alterações tooan IoT hub.

1. Utilize um toocreate do editor de texto chamado de um modelo Azure Resource Manager **Template** com Olá seguintes toocreate de definição do recurso de um novo IoT hub padrão. Este exemplo adiciona Olá IoT Hub na Olá **EUA Leste** região, cria dois grupos de consumidores (**cg1** e **cg2**) no ponto final de Olá compatível com o Event Hub e utiliza Olá **2016-02-03** versão da API. Este modelo também espera toopass no nome de hub IoT Olá como um parâmetro denominado **hubName**. Para a lista atual de Olá de localizações que suportam o IoT Hub consulte [Azure estado][lnk-status].

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

2. Guarde o ficheiro de modelo do Azure Resource Manager Olá no seu computador local. Este exemplo assume que guarde-o numa pasta chamada **c:\templates**.

3. Execute Olá os seguintes comandos toodeploy novo hub IoT, transmitir o nome de Olá do seu IoT hub como um parâmetro. Neste exemplo, o nome de Olá do hub IoT de Olá é `abcmyiothub`. nome de Olá do seu IoT hub deve ser globalmente exclusivo:

    ```powershell
    New-AzureRmResourceGroupDeployment -ResourceGroupName MyIoTRG1 -TemplateFile C:\templates\template.json -hubName abcmyiothub
    ```
  [!INCLUDE [iot-hub-pii-note-naming-hub](../../includes/iot-hub-pii-note-naming-hub.md)]

4. saída de Olá apresenta Olá as chaves de Olá IoT hub que criou.

5. tooverify adicionada a sua aplicação Olá novo IoT hub, visite Olá [portal do Azure] [ lnk-azure-portal] e ver a lista de recursos. Em alternativa, utilize Olá **Get-AzureRmResource** cmdlet do PowerShell.

> [!NOTE]
> Esta aplicação de exemplo adiciona uma S1 Standard IoT Hub para o qual é-lhe faturado. Pode eliminar o hub IoT de Olá através de Olá [portal do Azure] [ lnk-azure-portal] ou utilizando Olá **remover AzureRmResource** cmdlet do PowerShell quando tiver terminado.

## <a name="next-steps"></a>Passos seguintes

Agora que implementou um IoT hub utilizando um modelo Azure Resource Manager com o PowerShell, poderá ser útil tooexplore mais:

* Leia sobre as capacidades de Olá de Olá [fornecedor de recursos do IoT Hub REST API][lnk-rest-api].
* Leitura [descrição geral do Azure Resource Manager] [ lnk-azure-rm-overview] toolearn mais sobre as capacidades de Olá do Gestor de recursos do Azure.

toolearn mais informações sobre desenvolver para o IoT Hub, consulte Olá seguintes artigos:

* [Introdução tooC SDK][lnk-c-sdk]
* [SDKs IoT do Azure][lnk-sdks]

toofurther explorar Olá das capacidades do IoT Hub, consulte:

* [Simulando um dispositivo com o Azure IoT Edge][lnk-iotedge]

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
