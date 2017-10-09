---
title: "esquema de subscrição de evento grelha aaaAzure"
description: "Descreve propriedades Olá para subscrição tooan evento com grelha de eventos do Azure."
services: event-grid
author: banisadr
manager: timlt
ms.service: event-grid
ms.topic: article
ms.date: 08/17/2017
ms.author: babanisa
ms.openlocfilehash: 6a96d67975a5a733c5ea3c56ea54501f94ea4cd2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="event-grid-subscription-schema"></a><span data-ttu-id="97f38-103">Esquema de subscrição de grelha de eventos</span><span class="sxs-lookup"><span data-stu-id="97f38-103">Event Grid subscription schema</span></span>

<span data-ttu-id="97f38-104">toocreate uma subscrição de evento grelha, envia um pedido toohello operação de subscrição de evento de criar.</span><span class="sxs-lookup"><span data-stu-id="97f38-104">toocreate an Event Grid subscription, you send a request toohello Create Event subscription operation.</span></span> <span data-ttu-id="97f38-105">Utilize Olá seguinte formato:</span><span class="sxs-lookup"><span data-stu-id="97f38-105">Use hello following format:</span></span>

```
PUT /subscriptions/{subscription-id}/resourceGroups/{group-name}/providers/{resource-provider}/{resource-type}/{resource-name}/Microsoft.EventGrid/eventSubscriptions/{event-type-definitions}?api-version=2017-06-15-preview
``` 

<span data-ttu-id="97f38-106">Por exemplo, para uma conta de armazenamento com o nome de uma subscrição de evento toocreate `examplestorage` num grupo de recursos denominado `examplegroup`, utilize Olá seguinte formato:</span><span class="sxs-lookup"><span data-stu-id="97f38-106">For example, toocreate an event subscription for a storage account named `examplestorage` in a resource group named `examplegroup`, use hello following format:</span></span>

```
PUT /subscriptions/{subscription-id}/resourceGroups/examplegroup/providers/Microsoft.Storage/storageaccounts/examplestorage/Microsoft.EventGrid/eventSubscriptions/{event-type-definitions}?api-version=2017-06-15-preview
``` 

<span data-ttu-id="97f38-107">artigo de Olá Descreve propriedades Olá e o esquema para o corpo de Olá de pedido de Olá.</span><span class="sxs-lookup"><span data-stu-id="97f38-107">hello article describes hello properties and schema for hello body of hello request.</span></span>
 
## <a name="event-subscription-properties"></a><span data-ttu-id="97f38-108">Propriedades de subscrição de evento</span><span class="sxs-lookup"><span data-stu-id="97f38-108">Event subscription properties</span></span>

| <span data-ttu-id="97f38-109">Propriedade</span><span class="sxs-lookup"><span data-stu-id="97f38-109">Property</span></span> | <span data-ttu-id="97f38-110">Tipo</span><span class="sxs-lookup"><span data-stu-id="97f38-110">Type</span></span> | <span data-ttu-id="97f38-111">Descrição</span><span class="sxs-lookup"><span data-stu-id="97f38-111">Description</span></span> |
| -------- | ---- | ----------- |
| <span data-ttu-id="97f38-112">Destino</span><span class="sxs-lookup"><span data-stu-id="97f38-112">destination</span></span> | <span data-ttu-id="97f38-113">objeto</span><span class="sxs-lookup"><span data-stu-id="97f38-113">object</span></span> | <span data-ttu-id="97f38-114">objeto de Olá que define o ponto final de Olá.</span><span class="sxs-lookup"><span data-stu-id="97f38-114">hello object that defines hello endpoint.</span></span> |
| <span data-ttu-id="97f38-115">filtro</span><span class="sxs-lookup"><span data-stu-id="97f38-115">filter</span></span> | <span data-ttu-id="97f38-116">objeto</span><span class="sxs-lookup"><span data-stu-id="97f38-116">object</span></span> | <span data-ttu-id="97f38-117">Um campo opcional para efeitos de filtragem de tipos de Olá de eventos.</span><span class="sxs-lookup"><span data-stu-id="97f38-117">An optional field for filtering hello types of events.</span></span> |

### <a name="destination-object"></a><span data-ttu-id="97f38-118">objeto de destino</span><span class="sxs-lookup"><span data-stu-id="97f38-118">destination object</span></span>

| <span data-ttu-id="97f38-119">Propriedade</span><span class="sxs-lookup"><span data-stu-id="97f38-119">Property</span></span> | <span data-ttu-id="97f38-120">Tipo</span><span class="sxs-lookup"><span data-stu-id="97f38-120">Type</span></span> | <span data-ttu-id="97f38-121">Descrição</span><span class="sxs-lookup"><span data-stu-id="97f38-121">Description</span></span> |
| -------- | ---- | ----------- |
| <span data-ttu-id="97f38-122">endpointType</span><span class="sxs-lookup"><span data-stu-id="97f38-122">endpointType</span></span> | <span data-ttu-id="97f38-123">Cadeia</span><span class="sxs-lookup"><span data-stu-id="97f38-123">string</span></span> | <span data-ttu-id="97f38-124">tipo de Olá do ponto final para a subscrição de Olá (webhook/HTTP, Hub de eventos ou fila).</span><span class="sxs-lookup"><span data-stu-id="97f38-124">hello type of endpoint for hello subscription (webhook/HTTP, Event Hub, or queue).</span></span> | 
| <span data-ttu-id="97f38-125">endpointUrl</span><span class="sxs-lookup"><span data-stu-id="97f38-125">endpointUrl</span></span> | <span data-ttu-id="97f38-126">Cadeia</span><span class="sxs-lookup"><span data-stu-id="97f38-126">string</span></span> |  | 

### <a name="filter-object"></a><span data-ttu-id="97f38-127">objeto de filtro</span><span class="sxs-lookup"><span data-stu-id="97f38-127">filter object</span></span>

| <span data-ttu-id="97f38-128">Propriedade</span><span class="sxs-lookup"><span data-stu-id="97f38-128">Property</span></span> | <span data-ttu-id="97f38-129">Tipo</span><span class="sxs-lookup"><span data-stu-id="97f38-129">Type</span></span> | <span data-ttu-id="97f38-130">Descrição</span><span class="sxs-lookup"><span data-stu-id="97f38-130">Description</span></span> |
| -------- | ---- | ----------- |
| <span data-ttu-id="97f38-131">includedEventTypes</span><span class="sxs-lookup"><span data-stu-id="97f38-131">includedEventTypes</span></span> | <span data-ttu-id="97f38-132">Matriz</span><span class="sxs-lookup"><span data-stu-id="97f38-132">array</span></span> | <span data-ttu-id="97f38-133">Efetuar a correspondência quando o tipo de evento Olá na mensagem de evento Olá tooone uma correspondência exata destes nomes de tipo de evento.</span><span class="sxs-lookup"><span data-stu-id="97f38-133">Match when hello event type in hello event message is an exact match tooone of these event type names.</span></span> <span data-ttu-id="97f38-134">Gera um erro ao nome do evento não corresponder os nomes de tipo de evento Olá registado para a origem de evento Olá.</span><span class="sxs-lookup"><span data-stu-id="97f38-134">Raises an error when event name does not match hello registered event type names for hello event source.</span></span> <span data-ttu-id="97f38-135">Predefinição corresponde a todos os tipos de eventos.</span><span class="sxs-lookup"><span data-stu-id="97f38-135">Default matches all event types.</span></span> |
| <span data-ttu-id="97f38-136">subjectBeginsWith</span><span class="sxs-lookup"><span data-stu-id="97f38-136">subjectBeginsWith</span></span> | <span data-ttu-id="97f38-137">Cadeia</span><span class="sxs-lookup"><span data-stu-id="97f38-137">string</span></span> | <span data-ttu-id="97f38-138">Um correspondência de prefixo filtro toohello campo requerente na mensagem de evento de saudação.</span><span class="sxs-lookup"><span data-stu-id="97f38-138">A prefix-match filter toohello subject field in hello event message.</span></span> <span data-ttu-id="97f38-139">predefinição Olá ou uma cadeia vazia corresponde a todos.</span><span class="sxs-lookup"><span data-stu-id="97f38-139">hello default or empty string matches all.</span></span> | 
| <span data-ttu-id="97f38-140">subjectEndsWith</span><span class="sxs-lookup"><span data-stu-id="97f38-140">subjectEndsWith</span></span> | <span data-ttu-id="97f38-141">Cadeia</span><span class="sxs-lookup"><span data-stu-id="97f38-141">string</span></span> | <span data-ttu-id="97f38-142">Um correspondência de sufixo filtro toohello campo requerente na mensagem de evento de saudação.</span><span class="sxs-lookup"><span data-stu-id="97f38-142">A suffix-match filter toohello subject field in hello event message.</span></span> <span data-ttu-id="97f38-143">predefinição Olá ou uma cadeia vazia corresponde a todos.</span><span class="sxs-lookup"><span data-stu-id="97f38-143">hello default or empty string matches all.</span></span> |
| <span data-ttu-id="97f38-144">subjectIsCaseSensitive</span><span class="sxs-lookup"><span data-stu-id="97f38-144">subjectIsCaseSensitive</span></span> | <span data-ttu-id="97f38-145">Cadeia</span><span class="sxs-lookup"><span data-stu-id="97f38-145">string</span></span> | <span data-ttu-id="97f38-146">Controlos de maiúsculas e minúsculas de correspondência de filtros.</span><span class="sxs-lookup"><span data-stu-id="97f38-146">Controls case-sensitive matching for filters.</span></span> |


## <a name="example-subscription-schema"></a><span data-ttu-id="97f38-147">Esquema de subscrição de exemplo</span><span class="sxs-lookup"><span data-stu-id="97f38-147">Example subscription schema</span></span>

```json
{
  "properties": {
    "destination": {
      "endpointType": "webhook",
      "properties": {
          "endpointUrl": "https://example.azurewebsites.net/api/HttpTriggerCSharp1?code=VXbGWce53l48Mt8wuotr0GPmyJ/nDT4hgdFj9DpBiRt38qqnnm5OFg=="
      }
    },
    "filter": {
      "includedEventTypes": [ "blobCreated", "blobDeleted" ],
      "subjectBeginsWith": "blobServices/default/containers/mycontainer/log",
      "subjectEndsWith": ".jpg",
      "subjectIsCaseSensitive": "true"
    }
  }
}
```

## <a name="next-steps"></a><span data-ttu-id="97f38-148">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="97f38-148">Next steps</span></span>

* <span data-ttu-id="97f38-149">Para uma introdução tooEvent grelha, consulte [Novidades grelha de evento?](overview.md)</span><span class="sxs-lookup"><span data-stu-id="97f38-149">For an introduction tooEvent Grid, see [What is Event Grid?](overview.md)</span></span>
