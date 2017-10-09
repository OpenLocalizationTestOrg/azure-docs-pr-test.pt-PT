---
title: "ambiente de informações de séries de tempo do aaaSend eventos tooAzure | Microsoft Docs"
description: "Este tutorial abrange o ambiente de informações de séries de tempo de tooyour toopush eventos Olá passos"
keywords: 
services: tsi
documentationcenter: 
author: venkatgct
manager: jhubbard
editor: 
ms.assetid: 
ms.service: tsi
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/21/2017
ms.author: venkatja
ms.openlocfilehash: dbccc23f61351a0033cd48c1a02fb3841b45d560
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="send-events-tooa-time-series-insights-environment-using-event-hub"></a>Enviar o ambiente de informações de séries de tempo de tooa de eventos utilizando o hub de eventos

Este tutorial explica como toocreate e configurar o hub de eventos e execute um toopush de aplicação de exemplo eventos. Se tiver um hub de eventos existente que já contém eventos no formato JSON, pode ignorar este tutorial e ver o seu ambiente no [Time Series Insights](https://insights.timeseries.azure.com).

## <a name="configure-an-event-hub"></a>Configurar um hub de eventos
1. toocreate um hub de eventos, siga as instruções do Hub de eventos de Olá [documentação](https://docs.microsoft.com/azure/event-hubs/event-hubs-create).

2. Confirme que cria um grupo de consumidores que seja utilizado exclusivamente pela sua origem de eventos do Time Series Insights.

  > [!IMPORTANT]
  > Certifique-se de que este grupo de consumidores não é utilizado por nenhum outro serviço (como uma tarefa do Stream Analytics ou outro ambiente do Time Series Insights). Se o grupo de consumidores é utilizado por outros serviços, leia a operação é afetada negativamente para este ambiente e Olá outros serviços. Se estiver a utilizar "$Default" como grupo de consumidores Olá, pode levar toopotential reutilização por outros leitores.

  ![Selecionar o grupo de consumidores do hub de eventos](media/send-events/consumer-group.png)

3. No hub de eventos de Olá, crie "MySendPolicy" que é utilizado toosend eventos no exemplo de csharp Olá.

  ![Selecione Políticas de acesso partilhado e clique no botão Adicionar](media/send-events/shared-access-policy.png)  

  ![Adicionar uma política de acesso partilhado nova](media/send-events/shared-access-policy-2.png)  

## <a name="create-time-series-insights-event-source"></a>Criar a origem de eventos do Time Series Insights
1. Se ainda não criou uma origem de evento, siga [estas instruções](time-series-insights-add-event-source.md) toocreate uma origem de evento.

2. Especifique "deviceTimestamp" como nome da propriedade timestamp Olá – esta propriedade é utilizada como Olá timestamp real no exemplo de csharp Olá. nome da propriedade timestamp Olá é sensível e valores têm de seguir o formato de Olá __aaaa-MM-ddTHH. FFFFFFFK__ quando enviada como concentrador de tooevent JSON. Se Olá propriedade não existe no evento Olá, em seguida, hello tempo de colocados em fila de hub de eventos é utilizado.

  ![Crie a origem de eventos](media/send-events/event-source-1.png)

## <a name="sample-code-toopush-events"></a>Eventos de toopush de código de exemplo
1. Aceda a política de hub de eventos de toohello "MySendPolicy" e copie a cadeia de ligação de Olá com a chave de política de Olá.

  ![Copie a cadeia de ligação MySendPolicy](media/send-events/sample-code-connection-string.png)

2. Execute Olá seguinte código que eventos de toosend 600 por cada um dos dispositivos Olá três. Atualize `eventHubConnectionString` com a sua cadeia de ligação.

```csharp
using System;
using System.Collections.Generic;
using System.Globalization;
using System.IO;
using Microsoft.ServiceBus.Messaging;

namespace Microsoft.Rdx.DataGenerator
{
    internal class Program
    {
        private static void Main(string[] args)
        {
            var from = new DateTime(2017, 4, 20, 15, 0, 0, DateTimeKind.Utc);
            Random r = new Random();
            const int numberOfEvents = 600;

            var deviceIds = new[] { "device1", "device2", "device3" };

            var events = new List<string>();
            for (int i = 0; i < numberOfEvents; ++i)
            {
                for (int device = 0; device < deviceIds.Length; ++device)
                {
                    // Generate event and serialize as JSON object:
                    // { "deviceTimestamp": "utc timestamp", "deviceId": "guid", "value": 123.456 }
                    events.Add(
                        String.Format(
                            CultureInfo.InvariantCulture,
                            @"{{ ""deviceTimestamp"": ""{0}"", ""deviceId"": ""{1}"", ""value"": {2} }}",
                            (from + TimeSpan.FromSeconds(i * 30)).ToString("o"),
                            deviceIds[device],
                            r.NextDouble()));
                }
            }

            // Create event hub connection.
            var eventHubConnectionString = @"Endpoint=sb://...";
            var eventHubClient = EventHubClient.CreateFromConnectionString(eventHubConnectionString);

            using (var ms = new MemoryStream())
            using (var sw = new StreamWriter(ms))
            {
                // Wrap events into JSON array:
                sw.Write("[");
                for (int i = 0; i < events.Count; ++i)
                {
                    if (i > 0)
                    {
                        sw.Write(',');
                    }
                    sw.Write(events[i]);
                }
                sw.Write("]");

                sw.Flush();
                ms.Position = 0;

                // Send JSON tooevent hub.
                EventData eventData = new EventData(ms);
                eventHubClient.Send(eventData);
            }
        }
    }
}

```
## <a name="supported-json-shapes"></a>Formas JSON suportadas
### <a name="sample-1"></a>Exemplo 1

#### <a name="input"></a>Input

Um objeto JSON simples.

```json
{
    "id":"device1",
    "timestamp":"2016-01-08T01:08:00Z"
}
```
#### <a name="output---1-event"></a>Saída - 1 evento

|ID|carimbo de data/hora|
|--------|---------------|
|device1|2016-01-08T01:08:00Z|

### <a name="sample-2"></a>Exemplo 2

#### <a name="input"></a>Input
Uma matriz JSON com dois objetos JSON. Cada objeto JSON será convertida tooan eventos.
```json
[
    {
        "id":"device1",
        "timestamp":"2016-01-08T01:08:00Z"
    },
    {
        "id":"device2",
        "timestamp":"2016-01-17T01:17:00Z"
    }
]
```
#### <a name="output---2-events"></a>Saída - 2 eventos

|ID|carimbo de data/hora|
|--------|---------------|
|device1|2016-01-08T01:08:00Z|
|device2|2016-01-08T01:17:00Z|
### <a name="sample-3"></a>Exemplo 3

#### <a name="input"></a>Input

Um objeto JSON com uma matriz JSON aninhada que contém dois objetos JSON.
```json
{
    "location":"WestUs",
    "events":[
        {
            "id":"device1",
            "timestamp":"2016-01-08T01:08:00Z"
        },
        {
            "id":"device2",
            "timestamp":"2016-01-17T01:17:00Z"
        }
    ]
}

```
#### <a name="output---2-events"></a>Saída - 2 eventos
Tenha em atenção que a propriedade Olá "localização" é copiada através de tooeach do evento de Olá.

|localização|events.id|events.timestamp|
|--------|---------------|----------------------|
|WestUs|device1|2016-01-08T01:08:00Z|
|WestUs|device2|2016-01-08T01:17:00Z|

### <a name="sample-4"></a>Exemplo 4

#### <a name="input"></a>Input

Um objeto JSON com uma matriz JSON aninhada que contém dois objetos JSON. Esta entrada demonstra que propriedades globais Olá podem ser representadas por um objeto JSON Olá complexo.

```json
{
    "location":"WestUs",
    "manufacturer":{
        "name":"manufacturer1",
        "location":"EastUs"
    },
    "events":[
        {
            "id":"device1",
            "timestamp":"2016-01-08T01:08:00Z",
            "data":{
                "type":"pressure",
                "units":"psi",
                "value":108.09
            }
        },
        {
            "id":"device2",
            "timestamp":"2016-01-17T01:17:00Z",
            "data":{
                "type":"vibration",
                "units":"abs G",
                "value":217.09
            }
        }
    ]
}
```
#### <a name="output---2-events"></a>Saída - 2 eventos

|localização|manufacturer.name|manufacturer.location|events.id|events.timestamp|events.data.type|events.data.units|events.data.value|
|---|---|---|---|---|---|---|---|
|WestUs|manufacturer1|EastUs|device1|2016-01-08T01:08:00Z|pressure|psi|108.09|
|WestUs|manufacturer1|EastUs|device2|2016-01-08T01:17:00Z|vibration|abs G|217.09|

## <a name="next-steps"></a>Passos seguintes

* Ver o seu ambiente no [Portal do Time Series Insights](https://insights.timeseries.azure.com)
