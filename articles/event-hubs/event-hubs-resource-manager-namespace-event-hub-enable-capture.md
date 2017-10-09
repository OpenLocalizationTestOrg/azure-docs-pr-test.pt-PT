---
title: "aaaCreate um espaço de nomes de Event Hubs do Azure e ativar capturar utilizando um modelo | Microsoft Docs"
description: "Criar um espaço de nomes de Hubs de Eventos do Azure com o hub de um evento e ativar a Captura através de um modelo do Azure Resource Manager"
services: event-hubs
documentationcenter: .net
author: ShubhaVijayasarathy
manager: timlt
editor: 
ms.assetid: 8bdda6a2-5ff1-45e3-b696-c553768f1090
ms.service: event-hubs
ms.devlang: tbd
ms.topic: get-started-article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 08/28/2017
ms.author: sethm
ms.openlocfilehash: a43b4e8d690ae825047e8a9d609bfda89cf2a06f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-event-hubs-namespace-with-an-event-hub-and-enable-capture-using-an-azure-resource-manager-template"></a>Criar um espaço de nomes de Hubs de Eventos com o hub de um evento e ativar a Captura através de um modelo do Azure Resource Manager

Este artigo mostra como toouse um modelo Azure Resource Manager que cria um espaço de nomes de Event Hubs, com instância de hub de um evento e também permite Olá [funcionalidade de captura](event-hubs-capture-overview.md) no hub de eventos de Olá. Olá artigo descreve como toodefine os recursos são implementados e como toodefine parâmetros que são especificados quando a implementação de Olá é executada. Pode utilizar este modelo para as suas próprias implementações ou personalize-toomeet os seus requisitos.

Este artigo também mostra como toospecify que eventos são capturados para o Blobs Storage do Azure ou um Azure Data Lake Store, com base no Olá destino que escolher.

Para obter mais informações sobre a criação de modelos, consulte [Authoring Azure Resource Manager templates][Authoring Azure Resource Manager templates] (Criar modelos do Azure Resource Manager).

Para obter mais informações sobre padrões e práticas das convenções de nomenclatura de Recursos do Azure, veja [Azure Resources naming conventions][Azure Resources naming conventions] (Convenções de nomenclatura de Recursos do Azure).

Os modelos concluída Olá, clique em Olá seguintes hiperligações do GitHub:

- [Hub e ativar captura tooStorage modelo de evento][Event Hub and enable Capture tooStorage template] 
- [Hub e ativar captura tooAzure Data Lake Store modelo de evento][Event Hub and enable Capture tooAzure Data Lake Store template]

> [!NOTE]
> toocheck para modelos de mais recentes Olá, visite Olá [modelos de início rápido do Azure] [ Azure Quickstart Templates] Galeria e pesquisa para os Event Hubs.
> 
> 

## <a name="what-will-you-deploy"></a>O que irá implementar?

Com esTe modelo, implementa um espaço de nomes de Hubs de Eventos com o hub de um evento e também ativa a [Captura de Hubs de Eventos](event-hubs-capture-overview.md).

[Os Event Hubs](event-hubs-what-is-event-hubs.md) é um evento de processamento de serviço utilizado tooprovide telemetria e eventos de entrada tooAzure em grande escala, com baixa latência e alta fiabilidade. Event Hubs capturar permite tooautomatically fornecer Olá transmissão em fluxo de dados no armazenamento de Blobs do Event Hubs tooAzure ou do Azure Data Lake Store, dentro de um tempo especificado ou o intervalo de tamanho da sua escolha.

Clique em Olá seguir tooenable botão capturar os Hubs de eventos para o armazenamento do Azure:

[![Implementar tooAzure](./media/event-hubs-resource-manager-namespace-event-hub/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-eventhubs-create-namespace-and-enable-capture%2Fazuredeploy.json)

Clique em Olá seguir tooenable botão capturar os Hubs de eventos para o Azure Data Lake Store:

[![Implementar tooAzure](./media/event-hubs-resource-manager-namespace-event-hub/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-eventhubs-create-namespace-and-enable-capture-for-adls%2Fazuredeploy.json)

## <a name="parameters"></a>Parâmetros

Com o Azure Resource Manager, define os parâmetros para os valores que pretende toospecify quando o modelo de Olá é implementado. modelo de Olá inclui uma secção denominada `Parameters` que contém todos os valores de parâmetro de Olá. Deve definir um parâmetro para esses valores que variam com base no projeto Olá que estiver a implementar ou com base no ambiente de Olá que estiver a implementar. Não defina parâmetros para valores que permanecem sempre Olá mesmo. Cada valor do parâmetro é utilizado em Olá toodefine Olá recursos do modelo que são implementados.

modelo de Olá define Olá seguir os parâmetros.

### <a name="eventhubnamespacename"></a>eventHubNamespaceName

nome de Olá de Olá [espaço de nomes de Event Hubs](event-hubs-create.md) toocreate.

```json
"eventHubNamespaceName":{  
     "type":"string",
     "metadata":{  
         "description":"Name of hello EventHub namespace"
      }
}
```

### <a name="eventhubname"></a>eventHubName

nome de Olá Olá do hub de eventos criado no Olá [espaço de nomes de Event Hubs](event-hubs-create.md).

```json
"eventHubName":{  
    "type":"string",
    "metadata":{  
        "description":"Name of hello event hub"
    }
}
```

### <a name="messageretentionindays"></a>messageRetentionInDays

Olá número dias tooretain Olá mensagens num hub de eventos de Olá. 

```json
"messageRetentionInDays":{
    "type":"int",
    "defaultValue": 1,
    "minValue":"1",
    "maxValue":"7",
    "metadata":{
       "description":"How long tooretain hello data in event hub"
     }
 }
```

### <a name="partitioncount"></a>partitionCount

Olá número toocreate de partições num hub de eventos de Olá.

```json
"partitionCount":{
    "type":"int",
    "defaultValue":2,
    "minValue":2,
    "maxValue":32,
    "metadata":{
        "description":"Number of partitions chosen"
    }
 }
```

### <a name="captureenabled"></a>captureEnabled

Ative a captura no hub de eventos de Olá.

```json
"captureEnabled":{
    "type":"string",
    "defaultValue":"true",
    "allowedValues": [
    "false",
    "true"],
    "metadata":{
        "description":"Enable or disable hello Capture for your event hub"
    }
 }
```
### <a name="captureencodingformat"></a>captureEncodingFormat

formato de codificação Olá especificar dados de eventos de Olá tooserialize.

```json
"captureEncodingFormat":{
    "type":"string",
    "defaultValue":"Avro",
    "allowedValues":[
    "Avro"],
    "metadata":{
        "description":"hello encoding format in which Capture serializes hello EventData"
    }
}
```

### <a name="capturetime"></a>captureTime

intervalo de tempo de Olá na qual capturar os Hubs de eventos é iniciado capturar os dados de Olá.

```json
"captureTime":{
    "type":"int",
    "defaultValue":300,
    "minValue":60,
    "maxValue":900,
    "metadata":{
         "description":"hello time window in seconds for hello capture"
    }
}
```

### <a name="capturesize"></a>captureSize
intervalo de tamanho de Olá que captura inicia capturar os dados de Olá.

```json
"captureSize":{
    "type":"int",
    "defaultValue":314572800,
    "minValue":10485760,
    "maxValue":524288000,
    "metadata":{
        "description":"hello size window in bytes for capture"
    }
}
```

###<a name="capturenameformat"></a>captureNameFormat

formato de nome de Olá utilizado pela captura de Hubs de eventos toowrite Olá Avro os ficheiros. Tenha em atenção que formato de nome de Captura tem de conter os campos `{Namespace}`, `{EventHub}`, `{PartitionId}`, `{Year}`, `{Month}`, `{Day}`, `{Hour}`, `{Minute}` e `{Second}`. Estes podem ser dispostas por qualquer ordem, com ou sem delimitadores.
 
```json
"captureNameFormat": {
      "type": "string",
      "defaultValue": "{Namespace}/{EventHub}/{PartitionId}/{Year}/{Month}/{Day}/{Hour}/{Minute}/{Second}",
      "metadata": {
        "description": "A Capture Name Format must contain {Namespace}, {EventHub}, {PartitionId}, {Year}, {Month}, {Day}, {Hour}, {Minute} and {Second} fields. These can be arranged in any order with or without delimeters. E.g.  Prod_{EventHub}/{Namespace}\\{PartitionId}_{Year}_{Month}/{Day}/{Hour}/{Minute}/{Second}"
      }
    }
  }
```

### <a name="apiversion"></a>apiVersion

versão de Olá API de modelo de Olá.

```json
 "apiVersion":{  
    "type":"string",
    "defaultValue":"2015-08-01",
    "metadata":{  
        "description":"ApiVersion used by hello template"
    }
 }
```

Utilize Olá seguir os parâmetros se escolher o Storage do Azure como destino.

### <a name="destinationstorageaccountresourceid"></a>destinationStorageAccountResourceId

Captura requer um tooenable de ID do recurso do armazenamento do Azure conta capturar tooyour pretendido conta de armazenamento.

```json
 "destinationStorageAccountResourceId":{
    "type":"string",
    "metadata":{
        "description":"Your existing Storage account resource ID where you want hello blobs be captured"
    }
 }
```

### <a name="blobcontainername"></a>blobContainerName

Olá contentor do blob no qual toocapture os dados de eventos.

```json
 "blobContainerName":{
    "type":"string",
    "metadata":{
        "description":"Your existing storage container in which you want hello blobs captured"
    }
}
```

Utilize Olá seguir os parâmetros se escolher o Azure Data Lake Store como destino. Tem de definir as permissões no seu caminho de Data Lake Store, do qual pretende que o evento de Olá tooCapture. tooset permissões, consulte [neste artigo](event-hubs-capture-enable-through-portal.md#capture-data-to-an-azure-data-lake-store-account).

###<a name="subscriptionid"></a>subscriptionId

ID de subscrição para o espaço de nomes do Olá Event Hubs e o Azure Data Lake Store. Ambos estes recursos tem de estar sob Olá mesmo ID de subscrição.

```json
"subscriptionId": {
    "type": "string",
    "metadata": {
        "description": "Subscription Id of both Azure Data Lake Store and Event Hub namespace"
     }
 }
```

###<a name="datalakeaccountname"></a>dataLakeAccountName

nome do Azure Data Lake Store Olá para Olá capturados eventos.

```json
"dataLakeAccountName": {
    "type": "string",
    "metadata": {
        "description": "Azure Data Lake Store name"
    }
}
```

###<a name="datalakefolderpath"></a>dataLakeFolderPath

caminho de pasta de destino Olá para Olá capturados eventos.

```json
"dataLakeFolderPath": {
    "type": "string",
    "metadata": {
        "description": "Destination archive folder path"
    }
}
```

## <a name="resources-toodeploy-for-azure-storage-as-destination-toocaptured-events"></a>Toodeploy de recursos de armazenamento do Azure como eventos toocaptured de destino

Cria um espaço de nomes do tipo **EventHubs**, com um hub de eventos e também permite capturar tooAzure Blob Storage.

```json
"resources":[  
      {  
         "apiVersion":"[variables('ehVersion')]",
         "name":"[parameters('eventHubNamespaceName')]",
         "type":"Microsoft.EventHub/Namespaces",
         "location":"[variables('location')]",
         "sku":{  
            "name":"Standard",
            "tier":"Standard"
         },
         "resources":[  
            {  
               "apiVersion":"[variables('ehVersion')]",
               "name":"[parameters('eventHubName')]",
               "type":"EventHubs",
               "dependsOn":[  
                  "[concat('Microsoft.EventHub/namespaces/', parameters('eventHubNamespaceName'))]"
               ],
               "properties":{  
                  "path":"[parameters('eventHubName')]",
                  "MessageRetentionInDays":"[parameters('messageRetentionInDays')]",
                  "PartitionCount":"[parameters('partitionCount')]",
                  "CaptureDescription":{
                        "enabled":"[parameters('captureEnabled')]",
                        "encoding":"[parameters('captureEncodingFormat')]",
                        "intervalInSeconds":"[parameters('captureTime')]",
                        "sizeLimitInBytes":"[parameters('captureSize')]",
                        "destination":{
                            "name":"EventHubCapture.AzureBlockBlob",
                            "properties":{
                                "StorageAccountResourceId":"[parameters('destinationStorageAccountResourceId')]",
                                "BlobContainer":"[parameters('blobContainerName')]"
                            }
                        } 
                  }

               }

            }
         ]
      }
   ]
```

## <a name="resources-toodeploy-for-azure-data-lake-store-as-destination"></a>Toodeploy de recursos do Azure Data Lake Store, como destino

Cria um espaço de nomes do tipo **EventHubs**, com um hub de eventos e também permite capturar tooAzure Data Lake Store.

```json
 "resources": [
        {
            "apiVersion": "2015-08-01",
            "name": "[parameters('namespaceName')]",
            "type": "Microsoft.EventHub/Namespaces",
            "location": "[variables('location')]",
            "sku": {
                "name": "Standard",
                "tier": "Standard"
            },
            "resources": [
                {
                    "apiVersion": "2015-08-01",
                    "name": "[parameters('eventHubName')]",
                    "type": "EventHubs",
                    "dependsOn": [
                        "[concat('Microsoft.EventHub/namespaces/', parameters('namespaceName'))]"
                    ],
                    "properties": {
                        "path": "[parameters('eventHubName')]",
                        "ArchiveDescription": {
                            "enabled": "true",
                            "encoding": "[parameters('archiveEncodingFormat')]",
                            "intervalInSeconds": "[parameters('archiveTime')]",
                            "sizeLimitInBytes": "[parameters('archiveSize')]",
                            "destination": {
                                "name": "EventHubArchive.AzureDataLake",
                                "properties": {
                                    "DataLakeSubscriptionId": "[parameters('subscriptionId')]",
                                    "DataLakeAccountName": "[parameters('dataLakeAccountName')]",
                                    "DataLakeFolderPath": "[parameters('dataLakeFolderPath')]",
                                    "ArchiveNameFormat": "[parameters('archiveNameFormat')]"
                                }
                            }
                        }
                    }
                }
            ]
        }
    ]
```

## <a name="commands-toorun-deployment"></a>Implementação de toorun de comandos

[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

## <a name="powershell"></a>PowerShell

Implemente o tooenable modelo capturar os Hubs de eventos para o armazenamento do Azure:
 
```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName \<resource-group-name\> -TemplateFile https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-eventhubs-create-namespace-and-enable-capture/azuredeploy.json
```

Implemente o tooenable modelo capturar os Hubs de eventos para o Azure Data Lake Store:

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName \<resource-group-name\> -TemplateFile https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-eventhubs-create-namespace-and-enable-capture-for-adls/azuredeploy.json
```

## <a name="azure-cli"></a>CLI do Azure

Escolher o Armazenamento de Blob do Azure como destino:

```azurecli
azure config mode arm

azure group deployment create \<my-resource-group\> \<my-deployment-name\> --template-uri [https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-eventhubs-create-namespace-and-enable-capture/azuredeploy.json][]
```

Escolher o Azure Data Lake Store como destino:

```azurecli
azure config mode arm

azure group deployment create \<my-resource-group\> \<my-deployment-name\> --template-uri [https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-eventhubs-create-namespace-and-enable-capture-for-adls/azuredeploy.json][]
```

## <a name="next-steps"></a>Passos seguintes

Também pode configurar capturar os Hubs de eventos através de Olá [portal do Azure](https://portal.azure.com). Para obter mais informações, consulte [ativar a captura de Hubs de eventos utilizando Olá portal do Azure](event-hubs-capture-enable-through-portal.md).

Pode saber mais sobre os Event Hubs, visitando Olá seguintes ligações:

* [Descrição geral dos Hubs de Eventos](event-hubs-what-is-event-hubs.md)
* [Criar um hub de eventos](event-hubs-create.md)
* [FAQ dos Hubs de Eventos](event-hubs-faq.md)

[Authoring Azure Resource Manager templates]: ../azure-resource-manager/resource-group-authoring-templates.md
[Azure Quickstart Templates]:  https://azure.microsoft.com/documentation/templates/?term=event+hubs
[Azure Resources naming conventions]: https://azure.microsoft.com/documentation/articles/guidance-naming-conventions/
[Event hub and enable Capture tooStorage template]: https://github.com/Azure/azure-quickstart-templates/tree/master/201-eventhubs-create-namespace-and-enable-capture
[Event hub and enable Capture tooAzure Data Lake Store template]: https://github.com/Azure/azure-quickstart-templates/tree/master/201-eventhubs-create-namespace-and-enable-capture-for-adls
