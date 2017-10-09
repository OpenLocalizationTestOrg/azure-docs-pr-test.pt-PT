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
# <a name="create-an-event-hubs-namespace-with-an-event-hub-and-enable-capture-using-an-azure-resource-manager-template"></a><span data-ttu-id="1d0c8-103">Criar um espaço de nomes de Hubs de Eventos com o hub de um evento e ativar a Captura através de um modelo do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="1d0c8-103">Create an Event Hubs namespace with an event hub and enable Capture using an Azure Resource Manager template</span></span>

<span data-ttu-id="1d0c8-104">Este artigo mostra como toouse um modelo Azure Resource Manager que cria um espaço de nomes de Event Hubs, com instância de hub de um evento e também permite Olá [funcionalidade de captura](event-hubs-capture-overview.md) no hub de eventos de Olá.</span><span class="sxs-lookup"><span data-stu-id="1d0c8-104">This article shows how toouse an Azure Resource Manager template that creates an Event Hubs namespace, with one event hub instance, and also enables hello [Capture feature](event-hubs-capture-overview.md) on hello event hub.</span></span> <span data-ttu-id="1d0c8-105">Olá artigo descreve como toodefine os recursos são implementados e como toodefine parâmetros que são especificados quando a implementação de Olá é executada.</span><span class="sxs-lookup"><span data-stu-id="1d0c8-105">hello article describes how toodefine which resources are deployed, and how toodefine parameters that are specified when hello deployment is executed.</span></span> <span data-ttu-id="1d0c8-106">Pode utilizar este modelo para as suas próprias implementações ou personalize-toomeet os seus requisitos.</span><span class="sxs-lookup"><span data-stu-id="1d0c8-106">You can use this template for your own deployments, or customize it toomeet your requirements.</span></span>

<span data-ttu-id="1d0c8-107">Este artigo também mostra como toospecify que eventos são capturados para o Blobs Storage do Azure ou um Azure Data Lake Store, com base no Olá destino que escolher.</span><span class="sxs-lookup"><span data-stu-id="1d0c8-107">This article also shows how toospecify that events are captured into either Azure Storage Blobs or an Azure Data Lake Store, based on hello destination you choose.</span></span>

<span data-ttu-id="1d0c8-108">Para obter mais informações sobre a criação de modelos, consulte [Authoring Azure Resource Manager templates][Authoring Azure Resource Manager templates] (Criar modelos do Azure Resource Manager).</span><span class="sxs-lookup"><span data-stu-id="1d0c8-108">For more information about creating templates, see [Authoring Azure Resource Manager templates][Authoring Azure Resource Manager templates].</span></span>

<span data-ttu-id="1d0c8-109">Para obter mais informações sobre padrões e práticas das convenções de nomenclatura de Recursos do Azure, veja [Azure Resources naming conventions][Azure Resources naming conventions] (Convenções de nomenclatura de Recursos do Azure).</span><span class="sxs-lookup"><span data-stu-id="1d0c8-109">For more information about patterns and practices for Azure Resources naming conventions, see [Azure Resources naming conventions][Azure Resources naming conventions].</span></span>

<span data-ttu-id="1d0c8-110">Os modelos concluída Olá, clique em Olá seguintes hiperligações do GitHub:</span><span class="sxs-lookup"><span data-stu-id="1d0c8-110">For hello complete templates, click hello following GitHub links:</span></span>

- <span data-ttu-id="1d0c8-111">[Hub e ativar captura tooStorage modelo de evento][Event Hub and enable Capture tooStorage template]</span><span class="sxs-lookup"><span data-stu-id="1d0c8-111">[Event hub and enable Capture tooStorage template][Event Hub and enable Capture tooStorage template]</span></span> 
- <span data-ttu-id="1d0c8-112">[Hub e ativar captura tooAzure Data Lake Store modelo de evento][Event Hub and enable Capture tooAzure Data Lake Store template]</span><span class="sxs-lookup"><span data-stu-id="1d0c8-112">[Event hub and enable Capture tooAzure Data Lake Store template][Event Hub and enable Capture tooAzure Data Lake Store template]</span></span>

> [!NOTE]
> <span data-ttu-id="1d0c8-113">toocheck para modelos de mais recentes Olá, visite Olá [modelos de início rápido do Azure] [ Azure Quickstart Templates] Galeria e pesquisa para os Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="1d0c8-113">toocheck for hello latest templates, visit hello [Azure Quickstart Templates][Azure Quickstart Templates] gallery and search for Event Hubs.</span></span>
> 
> 

## <a name="what-will-you-deploy"></a><span data-ttu-id="1d0c8-114">O que irá implementar?</span><span class="sxs-lookup"><span data-stu-id="1d0c8-114">What will you deploy?</span></span>

<span data-ttu-id="1d0c8-115">Com esTe modelo, implementa um espaço de nomes de Hubs de Eventos com o hub de um evento e também ativa a [Captura de Hubs de Eventos](event-hubs-capture-overview.md).</span><span class="sxs-lookup"><span data-stu-id="1d0c8-115">With this template, you deploy an Event Hubs namespace with an event hub, and also enable [Event Hubs Capture](event-hubs-capture-overview.md).</span></span>

<span data-ttu-id="1d0c8-116">[Os Event Hubs](event-hubs-what-is-event-hubs.md) é um evento de processamento de serviço utilizado tooprovide telemetria e eventos de entrada tooAzure em grande escala, com baixa latência e alta fiabilidade.</span><span class="sxs-lookup"><span data-stu-id="1d0c8-116">[Event Hubs](event-hubs-what-is-event-hubs.md) is an event processing service used tooprovide event and telemetry ingress tooAzure at massive scale, with low latency and high reliability.</span></span> <span data-ttu-id="1d0c8-117">Event Hubs capturar permite tooautomatically fornecer Olá transmissão em fluxo de dados no armazenamento de Blobs do Event Hubs tooAzure ou do Azure Data Lake Store, dentro de um tempo especificado ou o intervalo de tamanho da sua escolha.</span><span class="sxs-lookup"><span data-stu-id="1d0c8-117">Event Hubs Capture enables you tooautomatically deliver hello streaming data in Event Hubs tooAzure Blob storage or Azure Data Lake Store, within a specified time or size interval of your choosing.</span></span>

<span data-ttu-id="1d0c8-118">Clique em Olá seguir tooenable botão capturar os Hubs de eventos para o armazenamento do Azure:</span><span class="sxs-lookup"><span data-stu-id="1d0c8-118">Click hello following button tooenable Event Hubs Capture into Azure Storage:</span></span>

<span data-ttu-id="1d0c8-119">[![Implementar tooAzure](./media/event-hubs-resource-manager-namespace-event-hub/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-eventhubs-create-namespace-and-enable-capture%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="1d0c8-119">[![Deploy tooAzure](./media/event-hubs-resource-manager-namespace-event-hub/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-eventhubs-create-namespace-and-enable-capture%2Fazuredeploy.json)</span></span>

<span data-ttu-id="1d0c8-120">Clique em Olá seguir tooenable botão capturar os Hubs de eventos para o Azure Data Lake Store:</span><span class="sxs-lookup"><span data-stu-id="1d0c8-120">Click hello following button tooenable Event Hubs Capture into Azure Data Lake Store:</span></span>

<span data-ttu-id="1d0c8-121">[![Implementar tooAzure](./media/event-hubs-resource-manager-namespace-event-hub/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-eventhubs-create-namespace-and-enable-capture-for-adls%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="1d0c8-121">[![Deploy tooAzure](./media/event-hubs-resource-manager-namespace-event-hub/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-eventhubs-create-namespace-and-enable-capture-for-adls%2Fazuredeploy.json)</span></span>

## <a name="parameters"></a><span data-ttu-id="1d0c8-122">Parâmetros</span><span class="sxs-lookup"><span data-stu-id="1d0c8-122">Parameters</span></span>

<span data-ttu-id="1d0c8-123">Com o Azure Resource Manager, define os parâmetros para os valores que pretende toospecify quando o modelo de Olá é implementado.</span><span class="sxs-lookup"><span data-stu-id="1d0c8-123">With Azure Resource Manager, you define parameters for values you want toospecify when hello template is deployed.</span></span> <span data-ttu-id="1d0c8-124">modelo de Olá inclui uma secção denominada `Parameters` que contém todos os valores de parâmetro de Olá.</span><span class="sxs-lookup"><span data-stu-id="1d0c8-124">hello template includes a section called `Parameters` that contains all hello parameter values.</span></span> <span data-ttu-id="1d0c8-125">Deve definir um parâmetro para esses valores que variam com base no projeto Olá que estiver a implementar ou com base no ambiente de Olá que estiver a implementar.</span><span class="sxs-lookup"><span data-stu-id="1d0c8-125">You should define a parameter for those values that vary based on hello project you are deploying or based on hello environment you are deploying to.</span></span> <span data-ttu-id="1d0c8-126">Não defina parâmetros para valores que permanecem sempre Olá mesmo.</span><span class="sxs-lookup"><span data-stu-id="1d0c8-126">Do not define parameters for values that always stay hello same.</span></span> <span data-ttu-id="1d0c8-127">Cada valor do parâmetro é utilizado em Olá toodefine Olá recursos do modelo que são implementados.</span><span class="sxs-lookup"><span data-stu-id="1d0c8-127">Each parameter value is used in hello template toodefine hello resources that are deployed.</span></span>

<span data-ttu-id="1d0c8-128">modelo de Olá define Olá seguir os parâmetros.</span><span class="sxs-lookup"><span data-stu-id="1d0c8-128">hello template defines hello following parameters.</span></span>

### <a name="eventhubnamespacename"></a><span data-ttu-id="1d0c8-129">eventHubNamespaceName</span><span class="sxs-lookup"><span data-stu-id="1d0c8-129">eventHubNamespaceName</span></span>

<span data-ttu-id="1d0c8-130">nome de Olá de Olá [espaço de nomes de Event Hubs](event-hubs-create.md) toocreate.</span><span class="sxs-lookup"><span data-stu-id="1d0c8-130">hello name of hello [Event Hubs namespace](event-hubs-create.md) toocreate.</span></span>

```json
"eventHubNamespaceName":{  
     "type":"string",
     "metadata":{  
         "description":"Name of hello EventHub namespace"
      }
}
```

### <a name="eventhubname"></a><span data-ttu-id="1d0c8-131">eventHubName</span><span class="sxs-lookup"><span data-stu-id="1d0c8-131">eventHubName</span></span>

<span data-ttu-id="1d0c8-132">nome de Olá Olá do hub de eventos criado no Olá [espaço de nomes de Event Hubs](event-hubs-create.md).</span><span class="sxs-lookup"><span data-stu-id="1d0c8-132">hello name of hello event hub created in hello [Event Hubs namespace](event-hubs-create.md).</span></span>

```json
"eventHubName":{  
    "type":"string",
    "metadata":{  
        "description":"Name of hello event hub"
    }
}
```

### <a name="messageretentionindays"></a><span data-ttu-id="1d0c8-133">messageRetentionInDays</span><span class="sxs-lookup"><span data-stu-id="1d0c8-133">messageRetentionInDays</span></span>

<span data-ttu-id="1d0c8-134">Olá número dias tooretain Olá mensagens num hub de eventos de Olá.</span><span class="sxs-lookup"><span data-stu-id="1d0c8-134">hello number of days tooretain hello messages in hello event hub.</span></span> 

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

### <a name="partitioncount"></a><span data-ttu-id="1d0c8-135">partitionCount</span><span class="sxs-lookup"><span data-stu-id="1d0c8-135">partitionCount</span></span>

<span data-ttu-id="1d0c8-136">Olá número toocreate de partições num hub de eventos de Olá.</span><span class="sxs-lookup"><span data-stu-id="1d0c8-136">hello number of partitions toocreate in hello event hub.</span></span>

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

### <a name="captureenabled"></a><span data-ttu-id="1d0c8-137">captureEnabled</span><span class="sxs-lookup"><span data-stu-id="1d0c8-137">captureEnabled</span></span>

<span data-ttu-id="1d0c8-138">Ative a captura no hub de eventos de Olá.</span><span class="sxs-lookup"><span data-stu-id="1d0c8-138">Enable Capture on hello event hub.</span></span>

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
### <a name="captureencodingformat"></a><span data-ttu-id="1d0c8-139">captureEncodingFormat</span><span class="sxs-lookup"><span data-stu-id="1d0c8-139">captureEncodingFormat</span></span>

<span data-ttu-id="1d0c8-140">formato de codificação Olá especificar dados de eventos de Olá tooserialize.</span><span class="sxs-lookup"><span data-stu-id="1d0c8-140">hello encoding format you specify tooserialize hello event data.</span></span>

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

### <a name="capturetime"></a><span data-ttu-id="1d0c8-141">captureTime</span><span class="sxs-lookup"><span data-stu-id="1d0c8-141">captureTime</span></span>

<span data-ttu-id="1d0c8-142">intervalo de tempo de Olá na qual capturar os Hubs de eventos é iniciado capturar os dados de Olá.</span><span class="sxs-lookup"><span data-stu-id="1d0c8-142">hello time interval in which Event Hubs Capture starts capturing hello data.</span></span>

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

### <a name="capturesize"></a><span data-ttu-id="1d0c8-143">captureSize</span><span class="sxs-lookup"><span data-stu-id="1d0c8-143">captureSize</span></span>
<span data-ttu-id="1d0c8-144">intervalo de tamanho de Olá que captura inicia capturar os dados de Olá.</span><span class="sxs-lookup"><span data-stu-id="1d0c8-144">hello size interval at which Capture starts capturing hello data.</span></span>

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

###<a name="capturenameformat"></a><span data-ttu-id="1d0c8-145">captureNameFormat</span><span class="sxs-lookup"><span data-stu-id="1d0c8-145">captureNameFormat</span></span>

<span data-ttu-id="1d0c8-146">formato de nome de Olá utilizado pela captura de Hubs de eventos toowrite Olá Avro os ficheiros.</span><span class="sxs-lookup"><span data-stu-id="1d0c8-146">hello name format used by Event Hubs Capture toowrite hello Avro files.</span></span> <span data-ttu-id="1d0c8-147">Tenha em atenção que formato de nome de Captura tem de conter os campos `{Namespace}`, `{EventHub}`, `{PartitionId}`, `{Year}`, `{Month}`, `{Day}`, `{Hour}`, `{Minute}` e `{Second}`.</span><span class="sxs-lookup"><span data-stu-id="1d0c8-147">Note that a Capture name format must contain `{Namespace}`, `{EventHub}`, `{PartitionId}`, `{Year}`, `{Month}`, `{Day}`, `{Hour}`, `{Minute}`, and `{Second}` fields.</span></span> <span data-ttu-id="1d0c8-148">Estes podem ser dispostas por qualquer ordem, com ou sem delimitadores.</span><span class="sxs-lookup"><span data-stu-id="1d0c8-148">These can be arranged in any order, with or without delimiters.</span></span>
 
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

### <a name="apiversion"></a><span data-ttu-id="1d0c8-149">apiVersion</span><span class="sxs-lookup"><span data-stu-id="1d0c8-149">apiVersion</span></span>

<span data-ttu-id="1d0c8-150">versão de Olá API de modelo de Olá.</span><span class="sxs-lookup"><span data-stu-id="1d0c8-150">hello API version of hello template.</span></span>

```json
 "apiVersion":{  
    "type":"string",
    "defaultValue":"2015-08-01",
    "metadata":{  
        "description":"ApiVersion used by hello template"
    }
 }
```

<span data-ttu-id="1d0c8-151">Utilize Olá seguir os parâmetros se escolher o Storage do Azure como destino.</span><span class="sxs-lookup"><span data-stu-id="1d0c8-151">Use hello following parameters if you choose Azure Storage as your destination.</span></span>

### <a name="destinationstorageaccountresourceid"></a><span data-ttu-id="1d0c8-152">destinationStorageAccountResourceId</span><span class="sxs-lookup"><span data-stu-id="1d0c8-152">destinationStorageAccountResourceId</span></span>

<span data-ttu-id="1d0c8-153">Captura requer um tooenable de ID do recurso do armazenamento do Azure conta capturar tooyour pretendido conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="1d0c8-153">Capture requires an Azure Storage account resource ID tooenable capturing tooyour desired Storage account.</span></span>

```json
 "destinationStorageAccountResourceId":{
    "type":"string",
    "metadata":{
        "description":"Your existing Storage account resource ID where you want hello blobs be captured"
    }
 }
```

### <a name="blobcontainername"></a><span data-ttu-id="1d0c8-154">blobContainerName</span><span class="sxs-lookup"><span data-stu-id="1d0c8-154">blobContainerName</span></span>

<span data-ttu-id="1d0c8-155">Olá contentor do blob no qual toocapture os dados de eventos.</span><span class="sxs-lookup"><span data-stu-id="1d0c8-155">hello blob container in which toocapture your event data.</span></span>

```json
 "blobContainerName":{
    "type":"string",
    "metadata":{
        "description":"Your existing storage container in which you want hello blobs captured"
    }
}
```

<span data-ttu-id="1d0c8-156">Utilize Olá seguir os parâmetros se escolher o Azure Data Lake Store como destino.</span><span class="sxs-lookup"><span data-stu-id="1d0c8-156">Use hello following parameters if you choose Azure Data Lake Store as your destination.</span></span> <span data-ttu-id="1d0c8-157">Tem de definir as permissões no seu caminho de Data Lake Store, do qual pretende que o evento de Olá tooCapture.</span><span class="sxs-lookup"><span data-stu-id="1d0c8-157">You must set permissions on your Data Lake Store path, in which you want tooCapture hello event.</span></span> <span data-ttu-id="1d0c8-158">tooset permissões, consulte [neste artigo](event-hubs-capture-enable-through-portal.md#capture-data-to-an-azure-data-lake-store-account).</span><span class="sxs-lookup"><span data-stu-id="1d0c8-158">tooset permissions, see [this article](event-hubs-capture-enable-through-portal.md#capture-data-to-an-azure-data-lake-store-account).</span></span>

###<a name="subscriptionid"></a><span data-ttu-id="1d0c8-159">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="1d0c8-159">subscriptionId</span></span>

<span data-ttu-id="1d0c8-160">ID de subscrição para o espaço de nomes do Olá Event Hubs e o Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="1d0c8-160">Subscription ID for hello Event Hubs namespace and Azure Data Lake Store.</span></span> <span data-ttu-id="1d0c8-161">Ambos estes recursos tem de estar sob Olá mesmo ID de subscrição.</span><span class="sxs-lookup"><span data-stu-id="1d0c8-161">Both these resources must be under hello same subscription ID.</span></span>

```json
"subscriptionId": {
    "type": "string",
    "metadata": {
        "description": "Subscription Id of both Azure Data Lake Store and Event Hub namespace"
     }
 }
```

###<a name="datalakeaccountname"></a><span data-ttu-id="1d0c8-162">dataLakeAccountName</span><span class="sxs-lookup"><span data-stu-id="1d0c8-162">dataLakeAccountName</span></span>

<span data-ttu-id="1d0c8-163">nome do Azure Data Lake Store Olá para Olá capturados eventos.</span><span class="sxs-lookup"><span data-stu-id="1d0c8-163">hello Azure Data Lake Store name for hello captured events.</span></span>

```json
"dataLakeAccountName": {
    "type": "string",
    "metadata": {
        "description": "Azure Data Lake Store name"
    }
}
```

###<a name="datalakefolderpath"></a><span data-ttu-id="1d0c8-164">dataLakeFolderPath</span><span class="sxs-lookup"><span data-stu-id="1d0c8-164">dataLakeFolderPath</span></span>

<span data-ttu-id="1d0c8-165">caminho de pasta de destino Olá para Olá capturados eventos.</span><span class="sxs-lookup"><span data-stu-id="1d0c8-165">hello destination folder path for hello captured events.</span></span>

```json
"dataLakeFolderPath": {
    "type": "string",
    "metadata": {
        "description": "Destination archive folder path"
    }
}
```

## <a name="resources-toodeploy-for-azure-storage-as-destination-toocaptured-events"></a><span data-ttu-id="1d0c8-166">Toodeploy de recursos de armazenamento do Azure como eventos toocaptured de destino</span><span class="sxs-lookup"><span data-stu-id="1d0c8-166">Resources toodeploy for Azure Storage as destination toocaptured events</span></span>

<span data-ttu-id="1d0c8-167">Cria um espaço de nomes do tipo **EventHubs**, com um hub de eventos e também permite capturar tooAzure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="1d0c8-167">Creates a namespace of type **EventHubs**, with one event hub, and also enables Capture tooAzure Blob Storage.</span></span>

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

## <a name="resources-toodeploy-for-azure-data-lake-store-as-destination"></a><span data-ttu-id="1d0c8-168">Toodeploy de recursos do Azure Data Lake Store, como destino</span><span class="sxs-lookup"><span data-stu-id="1d0c8-168">Resources toodeploy for Azure Data Lake Store as destination</span></span>

<span data-ttu-id="1d0c8-169">Cria um espaço de nomes do tipo **EventHubs**, com um hub de eventos e também permite capturar tooAzure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="1d0c8-169">Creates a namespace of type **EventHubs**, with one event hub, and also enables Capture tooAzure Data Lake Store.</span></span>

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

## <a name="commands-toorun-deployment"></a><span data-ttu-id="1d0c8-170">Implementação de toorun de comandos</span><span class="sxs-lookup"><span data-stu-id="1d0c8-170">Commands toorun deployment</span></span>

[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

## <a name="powershell"></a><span data-ttu-id="1d0c8-171">PowerShell</span><span class="sxs-lookup"><span data-stu-id="1d0c8-171">PowerShell</span></span>

<span data-ttu-id="1d0c8-172">Implemente o tooenable modelo capturar os Hubs de eventos para o armazenamento do Azure:</span><span class="sxs-lookup"><span data-stu-id="1d0c8-172">Deploy your template tooenable Event Hubs Capture into Azure Storage:</span></span>
 
```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName \<resource-group-name\> -TemplateFile https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-eventhubs-create-namespace-and-enable-capture/azuredeploy.json
```

<span data-ttu-id="1d0c8-173">Implemente o tooenable modelo capturar os Hubs de eventos para o Azure Data Lake Store:</span><span class="sxs-lookup"><span data-stu-id="1d0c8-173">Deploy your template tooenable Event Hubs Capture into Azure Data Lake Store:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName \<resource-group-name\> -TemplateFile https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-eventhubs-create-namespace-and-enable-capture-for-adls/azuredeploy.json
```

## <a name="azure-cli"></a><span data-ttu-id="1d0c8-174">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="1d0c8-174">Azure CLI</span></span>

<span data-ttu-id="1d0c8-175">Escolher o Armazenamento de Blob do Azure como destino:</span><span class="sxs-lookup"><span data-stu-id="1d0c8-175">Choosing Azure Blob Storage as destination:</span></span>

```azurecli
azure config mode arm

azure group deployment create \<my-resource-group\> \<my-deployment-name\> --template-uri [https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-eventhubs-create-namespace-and-enable-capture/azuredeploy.json][]
```

<span data-ttu-id="1d0c8-176">Escolher o Azure Data Lake Store como destino:</span><span class="sxs-lookup"><span data-stu-id="1d0c8-176">Choosing Azure Data Lake Store as destination:</span></span>

```azurecli
azure config mode arm

azure group deployment create \<my-resource-group\> \<my-deployment-name\> --template-uri [https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-eventhubs-create-namespace-and-enable-capture-for-adls/azuredeploy.json][]
```

## <a name="next-steps"></a><span data-ttu-id="1d0c8-177">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="1d0c8-177">Next steps</span></span>

<span data-ttu-id="1d0c8-178">Também pode configurar capturar os Hubs de eventos através de Olá [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="1d0c8-178">You can also configure Event Hubs Capture via hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="1d0c8-179">Para obter mais informações, consulte [ativar a captura de Hubs de eventos utilizando Olá portal do Azure](event-hubs-capture-enable-through-portal.md).</span><span class="sxs-lookup"><span data-stu-id="1d0c8-179">For more information, see [Enable Event Hubs Capture using hello Azure portal](event-hubs-capture-enable-through-portal.md).</span></span>

<span data-ttu-id="1d0c8-180">Pode saber mais sobre os Event Hubs, visitando Olá seguintes ligações:</span><span class="sxs-lookup"><span data-stu-id="1d0c8-180">You can learn more about Event Hubs by visiting hello following links:</span></span>

* [<span data-ttu-id="1d0c8-181">Descrição geral dos Hubs de Eventos</span><span class="sxs-lookup"><span data-stu-id="1d0c8-181">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="1d0c8-182">Criar um hub de eventos</span><span class="sxs-lookup"><span data-stu-id="1d0c8-182">Create an event hub</span></span>](event-hubs-create.md)
* [<span data-ttu-id="1d0c8-183">FAQ dos Hubs de Eventos</span><span class="sxs-lookup"><span data-stu-id="1d0c8-183">Event Hubs FAQ</span></span>](event-hubs-faq.md)

[Authoring Azure Resource Manager templates]: ../azure-resource-manager/resource-group-authoring-templates.md
[Azure Quickstart Templates]:  https://azure.microsoft.com/documentation/templates/?term=event+hubs
[Azure Resources naming conventions]: https://azure.microsoft.com/documentation/articles/guidance-naming-conventions/
[Event hub and enable Capture tooStorage template]: https://github.com/Azure/azure-quickstart-templates/tree/master/201-eventhubs-create-namespace-and-enable-capture
[Event hub and enable Capture tooAzure Data Lake Store template]: https://github.com/Azure/azure-quickstart-templates/tree/master/201-eventhubs-create-namespace-and-enable-capture-for-adls
