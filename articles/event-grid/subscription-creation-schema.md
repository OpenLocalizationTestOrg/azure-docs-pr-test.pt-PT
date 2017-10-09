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
# <a name="event-grid-subscription-schema"></a>Esquema de subscrição de grelha de eventos

toocreate uma subscrição de evento grelha, envia um pedido toohello operação de subscrição de evento de criar. Utilize Olá seguinte formato:

```
PUT /subscriptions/{subscription-id}/resourceGroups/{group-name}/providers/{resource-provider}/{resource-type}/{resource-name}/Microsoft.EventGrid/eventSubscriptions/{event-type-definitions}?api-version=2017-06-15-preview
``` 

Por exemplo, para uma conta de armazenamento com o nome de uma subscrição de evento toocreate `examplestorage` num grupo de recursos denominado `examplegroup`, utilize Olá seguinte formato:

```
PUT /subscriptions/{subscription-id}/resourceGroups/examplegroup/providers/Microsoft.Storage/storageaccounts/examplestorage/Microsoft.EventGrid/eventSubscriptions/{event-type-definitions}?api-version=2017-06-15-preview
``` 

artigo de Olá Descreve propriedades Olá e o esquema para o corpo de Olá de pedido de Olá.
 
## <a name="event-subscription-properties"></a>Propriedades de subscrição de evento

| Propriedade | Tipo | Descrição |
| -------- | ---- | ----------- |
| Destino | objeto | objeto de Olá que define o ponto final de Olá. |
| filtro | objeto | Um campo opcional para efeitos de filtragem de tipos de Olá de eventos. |

### <a name="destination-object"></a>objeto de destino

| Propriedade | Tipo | Descrição |
| -------- | ---- | ----------- |
| endpointType | Cadeia | tipo de Olá do ponto final para a subscrição de Olá (webhook/HTTP, Hub de eventos ou fila). | 
| endpointUrl | Cadeia |  | 

### <a name="filter-object"></a>objeto de filtro

| Propriedade | Tipo | Descrição |
| -------- | ---- | ----------- |
| includedEventTypes | Matriz | Efetuar a correspondência quando o tipo de evento Olá na mensagem de evento Olá tooone uma correspondência exata destes nomes de tipo de evento. Gera um erro ao nome do evento não corresponder os nomes de tipo de evento Olá registado para a origem de evento Olá. Predefinição corresponde a todos os tipos de eventos. |
| subjectBeginsWith | Cadeia | Um correspondência de prefixo filtro toohello campo requerente na mensagem de evento de saudação. predefinição Olá ou uma cadeia vazia corresponde a todos. | 
| subjectEndsWith | Cadeia | Um correspondência de sufixo filtro toohello campo requerente na mensagem de evento de saudação. predefinição Olá ou uma cadeia vazia corresponde a todos. |
| subjectIsCaseSensitive | Cadeia | Controlos de maiúsculas e minúsculas de correspondência de filtros. |


## <a name="example-subscription-schema"></a>Esquema de subscrição de exemplo

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

## <a name="next-steps"></a>Passos seguintes

* Para uma introdução tooEvent grelha, consulte [Novidades grelha de evento?](overview.md)
