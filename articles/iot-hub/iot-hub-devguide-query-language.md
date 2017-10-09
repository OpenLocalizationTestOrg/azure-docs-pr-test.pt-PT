---
title: "Olá aaaUnderstand idioma de consulta do IoT Hub do Azure | Microsoft Docs"
description: "Guia para programadores - descrição do idioma de consulta de SQL Server como o IoT Hub Olá utilizado tooretrieve informações sobre dispositivos duplos e tarefas a partir do seu IoT hub."
services: iot-hub
documentationcenter: .net
author: fsautomata
manager: timlt
editor: 
ms.assetid: 851a9ed3-b69e-422e-8a5d-1d79f91ddf15
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/25/17
ms.author: elioda
ms.openlocfilehash: 01a7c8ffdf44c6c27b834739d02c8fef1dd3d3fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="reference---iot-hub-query-language-for-device-twins-jobs-and-message-routing"></a><span data-ttu-id="5ade2-103">Referência - idioma de consulta do IoT Hub para dispositivos duplos, tarefas e o encaminhamento de mensagens</span><span class="sxs-lookup"><span data-stu-id="5ade2-103">Reference - IoT Hub query language for device twins, jobs, and message routing</span></span>

<span data-ttu-id="5ade2-104">IoT Hub fornece informações de tooretrieve um poderosa linguagem semelhante a SQL relativos à [dispositivos duplos] [ lnk-twins] e [tarefas][lnk-jobs]e [mensagem encaminhamento][lnk-devguide-messaging-routes].</span><span class="sxs-lookup"><span data-stu-id="5ade2-104">IoT Hub provides a powerful SQL-like language tooretrieve information regarding [device twins][lnk-twins] and [jobs][lnk-jobs], and [message routing][lnk-devguide-messaging-routes].</span></span> <span data-ttu-id="5ade2-105">Este artigo apresenta:</span><span class="sxs-lookup"><span data-stu-id="5ade2-105">This article presents:</span></span>

* <span data-ttu-id="5ade2-106">Uma introdução toohello principais funcionalidades de Olá idioma de consulta do IoT Hub, e</span><span class="sxs-lookup"><span data-stu-id="5ade2-106">An introduction toohello major features of hello IoT Hub query language, and</span></span>
* <span data-ttu-id="5ade2-107">Olá detalhadas descrição de idioma de Olá.</span><span class="sxs-lookup"><span data-stu-id="5ade2-107">hello detailed description of hello language.</span></span>

## <a name="get-started-with-device-twin-queries"></a><span data-ttu-id="5ade2-108">Começar a utilizar consultas do dispositivo duplo</span><span class="sxs-lookup"><span data-stu-id="5ade2-108">Get started with device twin queries</span></span>
<span data-ttu-id="5ade2-109">[Dispositivos duplos] [ lnk-twins] pode conter objetos JSON arbitrários, como as etiquetas e propriedades.</span><span class="sxs-lookup"><span data-stu-id="5ade2-109">[Device twins][lnk-twins] can contain arbitrary JSON objects as both tags and properties.</span></span> <span data-ttu-id="5ade2-110">IoT Hub permite-lhe tooquery dispositivos duplos como um único documento JSON que contém todas as informações do dispositivo duplo.</span><span class="sxs-lookup"><span data-stu-id="5ade2-110">IoT Hub enables you tooquery device twins as a single JSON document containing all device twin information.</span></span>
<span data-ttu-id="5ade2-111">Partem do princípio de, por exemplo, que os dispositivos duplos do IoT hub tem Olá seguir a estrutura:</span><span class="sxs-lookup"><span data-stu-id="5ade2-111">Assume, for instance, that your IoT hub device twins have hello following structure:</span></span>

```json
{
    "deviceId": "myDeviceId",
    "etag": "AAAAAAAAAAc=",
    "tags": {
        "location": {
            "region": "US",
            "plant": "Redmond43"
        }
    },
    "properties": {
        "desired": {
            "telemetryConfig": {
                "configId": "db00ebf5-eeeb-42be-86a1-458cccb69e57",
                "sendFrequencyInSecs": 300
            },
            "$metadata": {
            ...
            },
            "$version": 4
        },
        "reported": {
            "connectivity": {
                "type": "cellular"
            },
            "telemetryConfig": {
                "configId": "db00ebf5-eeeb-42be-86a1-458cccb69e57",
                "sendFrequencyInSecs": 300,
                "status": "Success"
            },
            "$metadata": {
            ...
            },
            "$version": 7
        }
    }
}
```

<span data-ttu-id="5ade2-112">IoT Hub expõe dispositivos duplos da Olá como uma coleção de documentos chamada **dispositivos**.</span><span class="sxs-lookup"><span data-stu-id="5ade2-112">IoT Hub exposes hello device twins as a document collection called **devices**.</span></span>
<span data-ttu-id="5ade2-113">Por isso, Olá seguinte consulta obtém o conjunto completo de Olá de dispositivos duplos:</span><span class="sxs-lookup"><span data-stu-id="5ade2-113">So hello following query retrieves hello whole set of device twins:</span></span>

```sql
SELECT * FROM devices
```

> [!NOTE]
> <span data-ttu-id="5ade2-114">[Os SDKs IoT do Azure] [ lnk-hub-sdks] suporta paginação dos resultados grande.</span><span class="sxs-lookup"><span data-stu-id="5ade2-114">[Azure IoT SDKs][lnk-hub-sdks] support paging of large results.</span></span>

<span data-ttu-id="5ade2-115">IoT Hub permite-lhe tooretrieve dispositivos duplos filtragem com condições arbitrários.</span><span class="sxs-lookup"><span data-stu-id="5ade2-115">IoT Hub allows you tooretrieve device twins filtering with arbitrary conditions.</span></span> <span data-ttu-id="5ade2-116">Por exemplo,</span><span class="sxs-lookup"><span data-stu-id="5ade2-116">For instance,</span></span>

```sql
SELECT * FROM devices
WHERE tags.location.region = 'US'
```

<span data-ttu-id="5ade2-117">obtém Olá dispositivos duplos com Olá **location.region** etiquetas definido demasiado**E.U.A.**.</span><span class="sxs-lookup"><span data-stu-id="5ade2-117">retrieves hello device twins with hello **location.region** tag set too**US**.</span></span>
<span data-ttu-id="5ade2-118">Operadores booleanos e comparações aritméticas suportadas, bem como, por exemplo</span><span class="sxs-lookup"><span data-stu-id="5ade2-118">Boolean operators and arithmetic comparisons are supported as well, for example</span></span>

```sql
SELECT * FROM devices
WHERE tags.location.region = 'US'
    AND properties.reported.telemetryConfig.sendFrequencyInSecs >= 60
```

<span data-ttu-id="5ade2-119">obtém todos os dispositivos duplos, localizados na Olá nos configurado toosend telemetria inferior, muitas vezes, a cada minuto.</span><span class="sxs-lookup"><span data-stu-id="5ade2-119">retrieves all device twins located in hello US configured toosend telemetry less often than every minute.</span></span> <span data-ttu-id="5ade2-120">Para efeitos práticos, também é possível toouse constantes de matriz com Olá **IN** e **NIN** operadores (não nos).</span><span class="sxs-lookup"><span data-stu-id="5ade2-120">As a convenience, it is also possible toouse array constants with hello **IN** and **NIN** (not in) operators.</span></span> <span data-ttu-id="5ade2-121">Por exemplo,</span><span class="sxs-lookup"><span data-stu-id="5ade2-121">For instance,</span></span>

```sql
SELECT * FROM devices
WHERE properties.reported.connectivity IN ['wired', 'wifi']
```

<span data-ttu-id="5ade2-122">obtém todos os dispositivos duplos, que comunicou Wi-Fi ou com fios conectividade.</span><span class="sxs-lookup"><span data-stu-id="5ade2-122">retrieves all device twins that reported WiFi or wired connectivity.</span></span> <span data-ttu-id="5ade2-123">Este é frequentemente necessário tooidentify todos os dispositivos duplos, que contém uma propriedade específica.</span><span class="sxs-lookup"><span data-stu-id="5ade2-123">It is often necessary tooidentify all device twins that contain a specific property.</span></span> <span data-ttu-id="5ade2-124">IoT Hub suporta função Olá `is_defined()` para esta finalidade.</span><span class="sxs-lookup"><span data-stu-id="5ade2-124">IoT Hub supports hello function `is_defined()` for this purpose.</span></span> <span data-ttu-id="5ade2-125">Por exemplo,</span><span class="sxs-lookup"><span data-stu-id="5ade2-125">For instance,</span></span>

```SQL
SELECT * FROM devices
WHERE is_defined(properties.reported.connectivity)
```

<span data-ttu-id="5ade2-126">obter todos os dispositivos duplos que definem Olá `connectivity` comunicadas propriedade.</span><span class="sxs-lookup"><span data-stu-id="5ade2-126">retrieved all device twins that define hello `connectivity` reported property.</span></span> <span data-ttu-id="5ade2-127">Consulte toohello [cláusula WHERE] [ lnk-query-where] secção para referência completa Olá Olá capacidades de filtragem.</span><span class="sxs-lookup"><span data-stu-id="5ade2-127">Refer toohello [WHERE clause][lnk-query-where] section for hello full reference of hello filtering capabilities.</span></span>

<span data-ttu-id="5ade2-128">Agrupamento e agregações também são suportadas.</span><span class="sxs-lookup"><span data-stu-id="5ade2-128">Grouping and aggregations are also supported.</span></span> <span data-ttu-id="5ade2-129">Por exemplo,</span><span class="sxs-lookup"><span data-stu-id="5ade2-129">For instance,</span></span>

```sql
SELECT properties.reported.telemetryConfig.status AS status,
    COUNT() AS numberOfDevices
FROM devices
GROUP BY properties.reported.telemetryConfig.status
```

<span data-ttu-id="5ade2-130">Devolve a contagem de Olá de dispositivos de Olá em cada Estado de configuração de telemetria.</span><span class="sxs-lookup"><span data-stu-id="5ade2-130">returns hello count of hello devices in each telemetry configuration status.</span></span>

```json
[
    {
        "numberOfDevices": 3,
        "status": "Success"
    },
    {
        "numberOfDevices": 2,
        "status": "Pending"
    },
    {
        "numberOfDevices": 1,
        "status": "Error"
    }
]
```

<span data-ttu-id="5ade2-131">Olá anterior exemplo ilustra uma situação em que três dispositivos comunicados configuração com êxito, dois ainda a aplicar a configuração de Olá e um comunicou um erro.</span><span class="sxs-lookup"><span data-stu-id="5ade2-131">hello preceding example illustrates a situation where three devices reported successful configuration, two are still applying hello configuration, and one reported an error.</span></span>

### <a name="c-example"></a><span data-ttu-id="5ade2-132">Exemplo do c#</span><span class="sxs-lookup"><span data-stu-id="5ade2-132">C# example</span></span>
<span data-ttu-id="5ade2-133">funcionalidade de consulta Olá é exposta pelo Olá [c# SDK do serviço] [ lnk-hub-sdks] no Olá **RegistryManager** classe.</span><span class="sxs-lookup"><span data-stu-id="5ade2-133">hello query functionality is exposed by hello [C# service SDK][lnk-hub-sdks] in hello **RegistryManager** class.</span></span>
<span data-ttu-id="5ade2-134">Eis um exemplo de uma consulta simples:</span><span class="sxs-lookup"><span data-stu-id="5ade2-134">Here is an example of a simple query:</span></span>

```csharp
var query = registryManager.CreateQuery("SELECT * FROM devices", 100);
while (query.HasMoreResults)
{
    var page = await query.GetNextAsTwinAsync();
    foreach (var twin in page)
    {
        // do work on twin object
    }
}
```

<span data-ttu-id="5ade2-135">Tenha em atenção como Olá **consulta** é criar instâncias do objecto com um tamanho de página (cópia de segurança too1000) e, em seguida, várias páginas podem ser obtidas pelos Olá chamar **GetNextAsTwinAsync** métodos várias vezes.</span><span class="sxs-lookup"><span data-stu-id="5ade2-135">Note how hello **query** object is instantiated with a page size (up too1000), and then multiple pages can be retrieved by calling hello **GetNextAsTwinAsync** methods multiple times.</span></span>
<span data-ttu-id="5ade2-136">Tenha em atenção que objeto da consulta Olá expõe vários **seguinte\***, dependendo da opção de anulação da serialização de Olá exigido pela consulta Olá, por exemplo, o dispositivo duplo ou tarefa de objetos, ou simples toobe JSON utilizados quando usar projeções.</span><span class="sxs-lookup"><span data-stu-id="5ade2-136">Note that hello query object exposes multiple **Next\***, depending on hello deserialization option required by hello query, such as device twin or job objects, or plain JSON toobe used when using projections.</span></span>

### <a name="nodejs-example"></a><span data-ttu-id="5ade2-137">Exemplo de node.js</span><span class="sxs-lookup"><span data-stu-id="5ade2-137">Node.js example</span></span>
<span data-ttu-id="5ade2-138">funcionalidade de consulta Olá é exposta pelo Olá [o serviço de IoT do Azure SDK para Node.js] [ lnk-hub-sdks] no Olá **registo** objeto.</span><span class="sxs-lookup"><span data-stu-id="5ade2-138">hello query functionality is exposed by hello [Azure IoT service SDK for Node.js][lnk-hub-sdks] in hello **Registry** object.</span></span>
<span data-ttu-id="5ade2-139">Eis um exemplo de uma consulta simples:</span><span class="sxs-lookup"><span data-stu-id="5ade2-139">Here is an example of a simple query:</span></span>

```nodejs
var query = registry.createQuery('SELECT * FROM devices', 100);
var onResults = function(err, results) {
    if (err) {
        console.error('Failed toofetch hello results: ' + err.message);
    } else {
        // Do something with hello results
        results.forEach(function(twin) {
            console.log(twin.deviceId);
        });

        if (query.hasMoreResults) {
            query.nextAsTwin(onResults);
        }
    }
};
query.nextAsTwin(onResults);
```

<span data-ttu-id="5ade2-140">Tenha em atenção como Olá **consulta** é criar instâncias do objecto com um tamanho de página (cópia de segurança too1000) e, em seguida, várias páginas podem ser obtidas pelos Olá chamar **nextAsTwin** métodos várias vezes.</span><span class="sxs-lookup"><span data-stu-id="5ade2-140">Note how hello **query** object is instantiated with a page size (up too1000), and then multiple pages can be retrieved by calling hello **nextAsTwin** methods multiple times.</span></span>
<span data-ttu-id="5ade2-141">Tenha em atenção que objeto da consulta Olá expõe vários **seguinte\***, dependendo da opção de anulação da serialização de Olá exigido pela consulta Olá, por exemplo, o dispositivo duplo ou tarefa de objetos, ou simples toobe JSON utilizados quando usar projeções.</span><span class="sxs-lookup"><span data-stu-id="5ade2-141">Note that hello query object exposes multiple **next\***, depending on hello deserialization option required by hello query, such as device twin or job objects, or plain JSON toobe used when using projections.</span></span>

### <a name="limitations"></a><span data-ttu-id="5ade2-142">Limitações</span><span class="sxs-lookup"><span data-stu-id="5ade2-142">Limitations</span></span>
> [!IMPORTANT]
> <span data-ttu-id="5ade2-143">Os resultados da consulta podem ter alguns minutos de atraso com valores mais recentes do relativamente toohello dispositivos duplos.</span><span class="sxs-lookup"><span data-stu-id="5ade2-143">Query results can have a few minutes of delay with respect toohello latest values in device twins.</span></span> <span data-ttu-id="5ade2-144">Se a consultar os dispositivos individuais duplos por id, é sempre preferível toouse Olá obter a API do dispositivo duplo, que sempre contém valores mais recentes Olá e tem os limites de limitação superior.</span><span class="sxs-lookup"><span data-stu-id="5ade2-144">If querying individual device twins by id, it is always preferable toouse hello retrieve device twin API, which always contains hello latest values and has higher throttling limits.</span></span>

<span data-ttu-id="5ade2-145">Atualmente, em que comparações são suportadas para a instância apenas entre tipos primitivos (não existem objetos), `... WHERE properties.desired.config = properties.reported.config` só é suportada se essas propriedades têm valores primitivos.</span><span class="sxs-lookup"><span data-stu-id="5ade2-145">Currently, comparisons are supported only between primitive types (no objects), for instance `... WHERE properties.desired.config = properties.reported.config` is supported only if those properties have primitive values.</span></span>

## <a name="get-started-with-jobs-queries"></a><span data-ttu-id="5ade2-146">Começar a utilizar consultas de tarefas</span><span class="sxs-lookup"><span data-stu-id="5ade2-146">Get started with jobs queries</span></span>
<span data-ttu-id="5ade2-147">[As tarefas] [ lnk-jobs] fornecem uma forma tooexecute operações em conjuntos de dispositivos.</span><span class="sxs-lookup"><span data-stu-id="5ade2-147">[Jobs][lnk-jobs] provide a way tooexecute operations on sets of devices.</span></span> <span data-ttu-id="5ade2-148">Cada dispositivo duplo contém informações de Olá das tarefas de Olá do qual faz parte de uma coleção chamada **tarefas**.</span><span class="sxs-lookup"><span data-stu-id="5ade2-148">Each device twin contains hello information of hello jobs of which it is part in a collection called **jobs**.</span></span>
<span data-ttu-id="5ade2-149">Logicamente,</span><span class="sxs-lookup"><span data-stu-id="5ade2-149">Logically,</span></span>

```json
{
    "deviceId": "myDeviceId",
    "etag": "AAAAAAAAAAc=",
    "tags": {
        ...
    },
    "properties": {
        ...
    },
    "jobs": [
        {
            "deviceId": "myDeviceId",
            "jobId": "myJobId",
            "jobType": "scheduleTwinUpdate",
            "status": "completed",
            "startTimeUtc": "2016-09-29T18:18:52.7418462",
            "endTimeUtc": "2016-09-29T18:20:52.7418462",
            "createdDateTimeUtc": "2016-09-29T18:18:56.7787107Z",
            "lastUpdatedDateTimeUtc": "2016-09-29T18:18:56.8894408Z",
            "outcome": {
                "deviceMethodResponse": null
            }
        },
        ...
    ]
}
```

<span data-ttu-id="5ade2-150">Atualmente, esta coleção está consultável como **devices.jobs** no Olá idioma de consulta do IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="5ade2-150">Currently, this collection is queryable as **devices.jobs** in hello IoT Hub query language.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5ade2-151">Atualmente, a propriedade de tarefas Olá nunca é devolvida ao consultar dispositivos duplos (ou seja, as consultas que contém 'a partir de dispositivos').</span><span class="sxs-lookup"><span data-stu-id="5ade2-151">Currently, hello jobs property is never returned when querying device twins (that is, queries that contains 'FROM devices').</span></span> <span data-ttu-id="5ade2-152">Só pode ser acedido diretamente com consultas através de `FROM devices.jobs`.</span><span class="sxs-lookup"><span data-stu-id="5ade2-152">It can only be accessed directly with queries using `FROM devices.jobs`.</span></span>
>
>

<span data-ttu-id="5ade2-153">Por exemplo, tooget todas as tarefas (últimos e agendadas) que afetam um único dispositivo, pode utilizar Olá seguinte consulta:</span><span class="sxs-lookup"><span data-stu-id="5ade2-153">For instance, tooget all jobs (past and scheduled) that affect a single device, you can use hello following query:</span></span>

```sql
SELECT * FROM devices.jobs
WHERE devices.jobs.deviceId = 'myDeviceId'
```

<span data-ttu-id="5ade2-154">Tenha em atenção a como esta consulta fornece o estado de específicos do dispositivo Olá (e possivelmente resposta de método direto Olá) de cada tarefa devolvida.</span><span class="sxs-lookup"><span data-stu-id="5ade2-154">Note how this query provides hello device-specific status (and possibly hello direct method response) of each job returned.</span></span>
<span data-ttu-id="5ade2-155">Também é possível toofilter com condições booleanos arbitrários em todas as propriedades do objeto no Olá **devices.jobs** coleção.</span><span class="sxs-lookup"><span data-stu-id="5ade2-155">It is also possible toofilter with arbitrary Boolean conditions on all object properties in hello **devices.jobs** collection.</span></span>
<span data-ttu-id="5ade2-156">Por exemplo, Olá seguinte consulta:</span><span class="sxs-lookup"><span data-stu-id="5ade2-156">For instance, hello following query:</span></span>

```sql
SELECT * FROM devices.jobs
WHERE devices.jobs.deviceId = 'myDeviceId'
    AND devices.jobs.jobType = 'scheduleTwinUpdate'
    AND devices.jobs.status = 'completed'
    AND devices.jobs.createdTimeUtc > '2016-09-01'
```

<span data-ttu-id="5ade2-157">tarefas de atualização do obtém todos os concluída dispositivo duplo para dispositivo **myDeviceId** que foram criados depois de Setembro de 2016.</span><span class="sxs-lookup"><span data-stu-id="5ade2-157">retrieves all completed device twin update jobs for device **myDeviceId** that were created after September 2016.</span></span>

<span data-ttu-id="5ade2-158">Também é possível tooretrieve resultados de por dispositivo Olá de uma única tarefa.</span><span class="sxs-lookup"><span data-stu-id="5ade2-158">It is also possible tooretrieve hello per-device outcomes of a single job.</span></span>

```sql
SELECT * FROM devices.jobs
WHERE devices.jobs.jobId = 'myJobId'
```

### <a name="limitations"></a><span data-ttu-id="5ade2-159">Limitações</span><span class="sxs-lookup"><span data-stu-id="5ade2-159">Limitations</span></span>
<span data-ttu-id="5ade2-160">Atualmente, a consulta do **devices.jobs** não suportam:</span><span class="sxs-lookup"><span data-stu-id="5ade2-160">Currently, queries on **devices.jobs** do not support:</span></span>

* <span data-ttu-id="5ade2-161">Projeções, por conseguinte, apenas `SELECT *` é possível.</span><span class="sxs-lookup"><span data-stu-id="5ade2-161">Projections, therefore only `SELECT *` is possible.</span></span>
* <span data-ttu-id="5ade2-162">Condições que fazem referência toohello dispositivo duplo nas propriedades de toojob de adição (consulte Olá anterior a secção).</span><span class="sxs-lookup"><span data-stu-id="5ade2-162">Conditions that refer toohello device twin in addition toojob properties (see hello preceding section).</span></span>
* <span data-ttu-id="5ade2-163">Efetuar agregações, tais como contagem, avg, agrupar por.</span><span class="sxs-lookup"><span data-stu-id="5ade2-163">Performing aggregations, such as count, avg, group by.</span></span>

## <a name="get-started-with-device-to-cloud-message-routes-query-expressions"></a><span data-ttu-id="5ade2-164">Começar a utilizar expressões de consulta de rotas de mensagens do dispositivo-nuvem</span><span class="sxs-lookup"><span data-stu-id="5ade2-164">Get started with device-to-cloud message routes query expressions</span></span>

<span data-ttu-id="5ade2-165">Utilizar [rotas de dispositivo para nuvem][lnk-devguide-messaging-routes], pode configurar pontos finais toodifferent com base em expressões avaliadas em comparação com as mensagens individuais de mensagens de toodispatch dispositivo para a nuvem do IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="5ade2-165">Using [device-to-cloud routes][lnk-devguide-messaging-routes], you can configure IoT Hub toodispatch device-to-cloud messages toodifferent endpoints based on expressions evaluated against individual messages.</span></span>

<span data-ttu-id="5ade2-166">rota de Olá [condição] [ lnk-query-expressions] utiliza Olá mesmo idioma de consulta de IoT Hub como condições de consultas duplo e a tarefa.</span><span class="sxs-lookup"><span data-stu-id="5ade2-166">hello route [condition][lnk-query-expressions] uses hello same IoT Hub query language as conditions in twin and job queries.</span></span> <span data-ttu-id="5ade2-167">Rota condições são avaliadas no cabeçalhos de mensagens hello e corpo.</span><span class="sxs-lookup"><span data-stu-id="5ade2-167">Route conditions are evaluated on hello message headers and body.</span></span> <span data-ttu-id="5ade2-168">A expressão de consulta encaminhamento poderá envolver o método apenas cabeçalhos de mensagens, apenas corpo da mensagem hello, ou ambos os cabeçalhos de mensagens e corpo da mensagem.</span><span class="sxs-lookup"><span data-stu-id="5ade2-168">Your routing query expression may involve only message headers, only hello message body, or both message headers and message body.</span></span> <span data-ttu-id="5ade2-169">IoT Hub assume um esquema específico para cabeçalhos de Olá e corpo da mensagem em mensagens de tooroute ordem e Olá seguintes secções descreve o que é necessário para a rota de tooproperly do IoT Hub:</span><span class="sxs-lookup"><span data-stu-id="5ade2-169">IoT Hub assumes a specific schema for hello headers and message body in order tooroute messages, and hello following sections describe what is required for IoT Hub tooproperly route:</span></span>

### <a name="routing-on-message-headers"></a><span data-ttu-id="5ade2-170">Encaminhamento nos cabeçalhos de mensagens</span><span class="sxs-lookup"><span data-stu-id="5ade2-170">Routing on message headers</span></span>

<span data-ttu-id="5ade2-171">IoT Hub assume Olá após a representação JSON de cabeçalhos de mensagens para o encaminhamento de mensagem:</span><span class="sxs-lookup"><span data-stu-id="5ade2-171">IoT Hub assumes hello following JSON representation of message headers for message routing:</span></span>

```json
{
    "$messageId": "",
    "$enqueuedTime": "",
    "$to": "",
    "$expiryTimeUtc": "",
    "$correlationId": "",
    "$userId": "",
    "$ack": "",
    "$connectionDeviceId": "",
    "$connectionDeviceGenerationId": "",
    "$connectionAuthMethod": "",
    "$content-type": "",
    "$content-encoding": "",

    "userProperty1": "",
    "userProperty2": ""
}
```

<span data-ttu-id="5ade2-172">Propriedades do sistema de mensagens têm o prefixo Olá `'$'` símbolo.</span><span class="sxs-lookup"><span data-stu-id="5ade2-172">Message system properties are prefixed with hello `'$'` symbol.</span></span>
<span data-ttu-id="5ade2-173">Propriedades do utilizador são sempre acedidas com os respetivos nomes.</span><span class="sxs-lookup"><span data-stu-id="5ade2-173">User properties are always accessed with their name.</span></span> <span data-ttu-id="5ade2-174">Se um nome de propriedade de utilizador acontece toocoincide com uma propriedade de sistema (tais como `$to`), será possível obter a propriedade de utilizador Olá com Olá `$to` expressão.</span><span class="sxs-lookup"><span data-stu-id="5ade2-174">If a user property name happens toocoincide with a system property (such as `$to`), hello user property will be retrieved with hello `$to` expression.</span></span>
<span data-ttu-id="5ade2-175">Pode sempre aceder à propriedade de sistema de Olá utilizando parênteses Retos `{}`: por exemplo, pode utilizar expressão Olá `{$to}` tooaccess Olá propriedade de sistema `to`.</span><span class="sxs-lookup"><span data-stu-id="5ade2-175">You can always access hello system property using brackets `{}`: for instance, you can use hello expression `{$to}` tooaccess hello system property `to`.</span></span> <span data-ttu-id="5ade2-176">Os nomes de propriedade entre parênteses obtêm sempre a propriedade de sistema Olá correspondente.</span><span class="sxs-lookup"><span data-stu-id="5ade2-176">Bracketed property names always retrieve hello corresponding system property.</span></span>

<span data-ttu-id="5ade2-177">Lembre-se de que os nomes de propriedades são sensível a maiúsculas e minúsculas.</span><span class="sxs-lookup"><span data-stu-id="5ade2-177">Remember that property names are case insensitive.</span></span>

> [!NOTE]
> <span data-ttu-id="5ade2-178">Todas as propriedades de mensagem são cadeias.</span><span class="sxs-lookup"><span data-stu-id="5ade2-178">All message properties are strings.</span></span> <span data-ttu-id="5ade2-179">Propriedades do sistema, conforme descrito em Olá [guia para programadores][lnk-devguide-messaging-format], atualmente não estão disponível toouse nas consultas.</span><span class="sxs-lookup"><span data-stu-id="5ade2-179">System properties, as described in hello [developer guide][lnk-devguide-messaging-format], are currently not available toouse in queries.</span></span>
>

<span data-ttu-id="5ade2-180">Por exemplo, se utilizar um `messageType` propriedade, poderá pretender tooroute todos os ponto final tooone de telemetria e ponto final de tooanother do todos os alertas.</span><span class="sxs-lookup"><span data-stu-id="5ade2-180">For example, if you use a `messageType` property, you might want tooroute all telemetry tooone endpoint, and all alerts tooanother endpoint.</span></span> <span data-ttu-id="5ade2-181">Pode escrever Olá telemetria de Olá expressão tooroute os seguintes:</span><span class="sxs-lookup"><span data-stu-id="5ade2-181">You can write hello following expression tooroute hello telemetry:</span></span>

```sql
messageType = 'telemetry'
```

<span data-ttu-id="5ade2-182">E Olá seguintes mensagens de alerta por Olá tooroute de expressão:</span><span class="sxs-lookup"><span data-stu-id="5ade2-182">And hello following expression tooroute hello alert messages:</span></span>

```sql
messageType = 'alert'
```

<span data-ttu-id="5ade2-183">Expressões e funções também são suportadas.</span><span class="sxs-lookup"><span data-stu-id="5ade2-183">Boolean expressions and functions are also supported.</span></span> <span data-ttu-id="5ade2-184">Esta funcionalidade permite-lhe toodistinguish entre o nível de gravidade, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="5ade2-184">This feature enables you toodistinguish between severity level, for example:</span></span>

```sql
messageType = 'alerts' AND as_number(severity) <= 2
```

<span data-ttu-id="5ade2-185">Consulte toohello [expressão e condições] [ lnk-query-expressions] secção para obter uma lista completa Olá operadores suportados e as funções.</span><span class="sxs-lookup"><span data-stu-id="5ade2-185">Refer toohello [Expression and conditions][lnk-query-expressions] section for hello full list of supported operators and functions.</span></span>

### <a name="routing-on-message-bodies"></a><span data-ttu-id="5ade2-186">Encaminhamento corpos de mensagens</span><span class="sxs-lookup"><span data-stu-id="5ade2-186">Routing on message bodies</span></span>

<span data-ttu-id="5ade2-187">IoT Hub apenas pode encaminhar com base no corpo da mensagem conteúdos se o corpo da mensagem Olá está corretamente formado JSON com codificação UTF-8, UTF-16 ou UTF-32.</span><span class="sxs-lookup"><span data-stu-id="5ade2-187">IoT Hub can only route based on message body contents if hello message body is properly formed JSON encoded in either UTF-8, UTF-16, or UTF-32.</span></span> <span data-ttu-id="5ade2-188">Tem de definir o tipo de mensagem de saudação conteúdo Olá demasiado`application/json` e Olá conteúdo tooone codificação de Olá suportado UTF codificações tooallow de cabeçalhos de mensagem de Olá mensagem de saudação do IoT Hub tooroute com base nos conteúdos do corpo de Olá.</span><span class="sxs-lookup"><span data-stu-id="5ade2-188">You must set hello content type of hello message too`application/json` and hello content encoding tooone of hello supported UTF encodings in hello message headers tooallow IoT Hub tooroute hello message based on hello body contents.</span></span> <span data-ttu-id="5ade2-189">Se qualquer um dos cabeçalhos de Olá não for especificado, o IoT Hub não tentará tooevaluate uma expressão de consulta que envolvem corpo Olá contra a mensagem de saudação.</span><span class="sxs-lookup"><span data-stu-id="5ade2-189">If either of hello headers is not specified, IoT Hub will not attempt tooevaluate any query expression involving hello body against hello message.</span></span> <span data-ttu-id="5ade2-190">Se a mensagem não é uma mensagem JSON ou se a mensagem de saudação não especifica o tipo de conteúdo de Olá e codificação de conteúdo, pode continuar a utilizar a mensagem de saudação tooroute com base nos cabeçalhos de mensagens hello de encaminhamento de mensagens.</span><span class="sxs-lookup"><span data-stu-id="5ade2-190">If your message is not a JSON message, or if hello message does not specify hello content type and content encoding, you may still use message routing tooroute hello message based on hello message headers.</span></span>

<span data-ttu-id="5ade2-191">Pode utilizar `$body` na mensagem de saudação do Olá consulta expressão tooroute.</span><span class="sxs-lookup"><span data-stu-id="5ade2-191">You can use `$body` in hello query expression tooroute hello message.</span></span> <span data-ttu-id="5ade2-192">Pode utilizar uma referência de corpo simples, de referência de matriz de corpo ou várias referências de corpo numa expressão de consulta Olá.</span><span class="sxs-lookup"><span data-stu-id="5ade2-192">You can use a simple body reference, body array reference, or multiple body references in hello query expression.</span></span> <span data-ttu-id="5ade2-193">A expressão de consulta também pode combinar uma referência de corpo com uma referência de cabeçalho da mensagem.</span><span class="sxs-lookup"><span data-stu-id="5ade2-193">Your query expression can also combine a body reference with a message header reference.</span></span> <span data-ttu-id="5ade2-194">Por exemplo, Olá são todas as expressões de consulta válida:</span><span class="sxs-lookup"><span data-stu-id="5ade2-194">For example, hello following are all valid query expressions:</span></span>

```sql
$body.message.Weather.Location.State = 'WA'
$body.Weather.HistoricalData[0].Month = 'Feb'
$body.Weather.Temperature = 50 AND $body.message.Weather.IsEnabled
length($body.Weather.Location.State) = 2
$body.Weather.Temperature = 50 AND Status = 'Active'
```

## <a name="basics-of-an-iot-hub-query"></a><span data-ttu-id="5ade2-195">Noções básicas de uma consulta do IoT Hub</span><span class="sxs-lookup"><span data-stu-id="5ade2-195">Basics of an IoT Hub query</span></span>
<span data-ttu-id="5ade2-196">Cada consulta de IoT Hub é composta por de um, SELECIONE e cláusulas FROM e onde opcional e GROUP BY cláusulas.</span><span class="sxs-lookup"><span data-stu-id="5ade2-196">Every IoT Hub query consists of a SELECT and FROM clauses and by optional WHERE and GROUP BY clauses.</span></span> <span data-ttu-id="5ade2-197">Cada consulta é executada numa coleção de documentos JSON, por exemplo, dispositivos duplos.</span><span class="sxs-lookup"><span data-stu-id="5ade2-197">Every query is run on a collection of JSON documents, for example device twins.</span></span> <span data-ttu-id="5ade2-198">cláusula FROM de Olá indica Olá documento coleção toobe iterated no (**dispositivos** ou **devices.jobs**).</span><span class="sxs-lookup"><span data-stu-id="5ade2-198">hello FROM clause indicates hello document collection toobe iterated on (**devices** or **devices.jobs**).</span></span> <span data-ttu-id="5ade2-199">Olá, em seguida, o filtro em olá onde é aplicada a cláusula.</span><span class="sxs-lookup"><span data-stu-id="5ade2-199">Then, hello filter in hello WHERE clause is applied.</span></span> <span data-ttu-id="5ade2-200">Com agregações, de resultados de Olá deste passo são agrupados como Olá especificado na cláusula GROUP BY e, para cada grupo, é gerada uma linha conforme especificado na cláusula SELECT Olá.</span><span class="sxs-lookup"><span data-stu-id="5ade2-200">With aggregations, hello results of this step are grouped as specified in hello GROUP BY clause and, for each group, a row is generated as specified in hello SELECT clause.</span></span>

```sql
SELECT <select_list>
FROM <from_specification>
[WHERE <filter_condition>]
[GROUP BY <group_specification>]
```

## <a name="from-clause"></a><span data-ttu-id="5ade2-201">A cláusula FROM</span><span class="sxs-lookup"><span data-stu-id="5ade2-201">FROM clause</span></span>
<span data-ttu-id="5ade2-202">Olá **do < from_specification >** cláusula pode assumir apenas dois valores: **dos dispositivos**, tooquery dispositivos duplos, ou **de devices.jobs**, tooquery tarefa por do dispositivo detalhes.</span><span class="sxs-lookup"><span data-stu-id="5ade2-202">hello **FROM <from_specification>** clause can assume only two values: **FROM devices**, tooquery device twins, or **FROM devices.jobs**, tooquery job per-device details.</span></span>

## <a name="where-clause"></a><span data-ttu-id="5ade2-203">Cláusula WHERE</span><span class="sxs-lookup"><span data-stu-id="5ade2-203">WHERE clause</span></span>
<span data-ttu-id="5ade2-204">Olá **onde < filter_condition >** cláusula é opcional.</span><span class="sxs-lookup"><span data-stu-id="5ade2-204">hello **WHERE <filter_condition>** clause is optional.</span></span> <span data-ttu-id="5ade2-205">Especifica uma ou mais condições que os documentos JSON de Olá na coleção de FROM Olá devem satisfazer toobe incluída como parte do resultado de Olá.</span><span class="sxs-lookup"><span data-stu-id="5ade2-205">It specifies one or more conditions that hello JSON documents in hello FROM collection must satisfy toobe included as part of hello result.</span></span> <span data-ttu-id="5ade2-206">De qualquer documento JSON tem de avaliar Olá especificado condições demasiado "true" toobe incluída no resultado de Olá.</span><span class="sxs-lookup"><span data-stu-id="5ade2-206">Any JSON document must evaluate hello specified conditions too"true" toobe included in hello result.</span></span>

<span data-ttu-id="5ade2-207">Olá permitido condições são descritas na secção [expressões e condições][lnk-query-expressions].</span><span class="sxs-lookup"><span data-stu-id="5ade2-207">hello allowed conditions are described in section [Expressions and conditions][lnk-query-expressions].</span></span>

## <a name="select-clause"></a><span data-ttu-id="5ade2-208">Cláusula SELECT</span><span class="sxs-lookup"><span data-stu-id="5ade2-208">SELECT clause</span></span>
<span data-ttu-id="5ade2-209">cláusula SELECT Olá (**SELECIONE < select_list >**) é obrigatória e especifica quais os valores são obtidos a partir de consulta Olá.</span><span class="sxs-lookup"><span data-stu-id="5ade2-209">hello SELECT clause (**SELECT <select_list>**) is mandatory and specifies what values are retrieved from hello query.</span></span> <span data-ttu-id="5ade2-210">Especifica Olá JSON valores toobe utilizado toogenerate novos objetos JSON.</span><span class="sxs-lookup"><span data-stu-id="5ade2-210">It specifies hello JSON values toobe used toogenerate new JSON objects.</span></span>
<span data-ttu-id="5ade2-211">Para cada elemento da Olá subconjunto filtrado (e opcionalmente agrupado) da coleção de FROM Olá, a fase de projeção Olá gera um novo objeto JSON, construído com valores de Olá especificados na cláusula SELECT Olá.</span><span class="sxs-lookup"><span data-stu-id="5ade2-211">For each element of hello filtered (and optionally grouped) subset of hello FROM collection, hello projection phase generates a new JSON object, constructed with hello values specified in hello SELECT clause.</span></span>

<span data-ttu-id="5ade2-212">Segue-se a gramática Olá da cláusula SELECT Olá:</span><span class="sxs-lookup"><span data-stu-id="5ade2-212">Following is hello grammar of hello SELECT clause:</span></span>

```
SELECT [TOP <max number>] <projection list>

<projection_list> ::=
    '*'
    | <projection_element> AS alias [, <projection_element> AS alias]+

<projection_element> :==
    attribute_name
    | <projection_element> '.' attribute_name
    | <aggregate>

<aggregate> :==
    count()
    | avg(<projection_element>)
    | sum(<projection_element>)
    | min(<projection_element>)
    | max(<projection_element>)
```

<span data-ttu-id="5ade2-213">onde **attribute_name** refere-se a propriedade tooany do documento JSON de Olá na coleção de FROM Olá.</span><span class="sxs-lookup"><span data-stu-id="5ade2-213">where **attribute_name** refers tooany property of hello JSON document in hello FROM collection.</span></span> <span data-ttu-id="5ade2-214">Alguns exemplos de cláusulas SELECT podem ser encontrados na Olá [introdução às consultas do dispositivo duplo] [ lnk-query-getstarted] secção.</span><span class="sxs-lookup"><span data-stu-id="5ade2-214">Some examples of SELECT clauses can be found in hello [Getting started with device twin queries][lnk-query-getstarted] section.</span></span>

<span data-ttu-id="5ade2-215">Atualmente, seleção cláusulas diferentes **SELECIONE \***  só são suportados em consultas de agregação em dispositivos duplos.</span><span class="sxs-lookup"><span data-stu-id="5ade2-215">Currently, selection clauses different than **SELECT \*** are only supported in aggregate queries on device twins.</span></span>

## <a name="group-by-clause"></a><span data-ttu-id="5ade2-216">Cláusula GROUP BY</span><span class="sxs-lookup"><span data-stu-id="5ade2-216">GROUP BY clause</span></span>
<span data-ttu-id="5ade2-217">Olá **GROUP BY < group_specification >** cláusula passo é opcional que pode ser executado após o filtro de Olá especificado no Olá cláusula WHERE e antes de projeção de Olá especificada no Olá SELECIONE.</span><span class="sxs-lookup"><span data-stu-id="5ade2-217">hello **GROUP BY <group_specification>** clause is an optional step that can be executed after hello filter specified in hello WHERE clause, and before hello projection specified in hello SELECT.</span></span> <span data-ttu-id="5ade2-218">Grupos de documentos com base no valor de Olá de um atributo.</span><span class="sxs-lookup"><span data-stu-id="5ade2-218">It groups documents based on hello value of an attribute.</span></span> <span data-ttu-id="5ade2-219">Estes grupos são utilizados toogenerate agregado valores conforme especificado na cláusula SELECT Olá.</span><span class="sxs-lookup"><span data-stu-id="5ade2-219">These groups are used toogenerate aggregated values as specified in hello SELECT clause.</span></span>

<span data-ttu-id="5ade2-220">Um exemplo de uma consulta com GROUP BY é:</span><span class="sxs-lookup"><span data-stu-id="5ade2-220">An example of a query using GROUP BY is:</span></span>

```sql
SELECT properties.reported.telemetryConfig.status AS status,
    COUNT() AS numberOfDevices
FROM devices
GROUP BY properties.reported.telemetryConfig.status
```

<span data-ttu-id="5ade2-221">Olá formal sintaxe GROUP BY está:</span><span class="sxs-lookup"><span data-stu-id="5ade2-221">hello formal syntax for GROUP BY is:</span></span>

```
GROUP BY <group_by_element>
<group_by_element> :==
    attribute_name
    | < group_by_element > '.' attribute_name
```

<span data-ttu-id="5ade2-222">onde **attribute_name** refere-se a propriedade tooany do documento JSON de Olá na coleção de FROM Olá.</span><span class="sxs-lookup"><span data-stu-id="5ade2-222">where **attribute_name** refers tooany property of hello JSON document in hello FROM collection.</span></span>

<span data-ttu-id="5ade2-223">Atualmente, a cláusula GROUP BY Olá só é suportada ao consultar dispositivos duplos.</span><span class="sxs-lookup"><span data-stu-id="5ade2-223">Currently, hello GROUP BY clause is only supported when querying device twins.</span></span>

## <a name="expressions-and-conditions"></a><span data-ttu-id="5ade2-224">As expressões e condições</span><span class="sxs-lookup"><span data-stu-id="5ade2-224">Expressions and conditions</span></span>
<span data-ttu-id="5ade2-225">Um nível elevado, um *expressão*:</span><span class="sxs-lookup"><span data-stu-id="5ade2-225">At a high level, an *expression*:</span></span>

* <span data-ttu-id="5ade2-226">Avalia a instância de tooan de um tipo JSON (por exemplo, booleano, número, cadeia, matriz ou objeto), e</span><span class="sxs-lookup"><span data-stu-id="5ade2-226">Evaluates tooan instance of a JSON type (such as Boolean, number, string, array, or object), and</span></span>
* <span data-ttu-id="5ade2-227">É definido pela manipulação de dados provenientes de documento JSON do dispositivo Olá e constantes utilizando operadores incorporados e funções.</span><span class="sxs-lookup"><span data-stu-id="5ade2-227">Is defined by manipulating data coming from hello device JSON document and constants using built-in operators and functions.</span></span>

<span data-ttu-id="5ade2-228">*Condições* são expressões avaliar tooa booleano.</span><span class="sxs-lookup"><span data-stu-id="5ade2-228">*Conditions* are expressions that evaluate tooa Boolean.</span></span> <span data-ttu-id="5ade2-229">Qualquer constante diferente booleano **verdadeiro** são considerados como estando **falso** (incluindo **nulo**, **indefinido**, qualquer instância de objeto ou a matriz qualquer cadeia e claramente Olá booleano **falso**).</span><span class="sxs-lookup"><span data-stu-id="5ade2-229">Any constant different than Boolean **true** is considered as **false** (including **null**, **undefined**, any object or array instance, any string, and clearly hello Boolean **false**).</span></span>

<span data-ttu-id="5ade2-230">Olá sintaxe para expressões é:</span><span class="sxs-lookup"><span data-stu-id="5ade2-230">hello syntax for expressions is:</span></span>

```
<expression> ::=
    <constant> |
    attribute_name |
    <function_call> |
    <expression> binary_operator <expression> |
    <create_array_expression> |
    '(' <expression> ')'

<function_call> ::=
    <function_name> '(' expression ')'

<constant> ::=
    <undefined_constant>
    | <null_constant>
    | <number_constant>
    | <string_constant>
    | <array_constant>

<undefined_constant> ::= undefined
<null_constant> ::= null
<number_constant> ::= decimal_literal | hexadecimal_literal
<string_constant> ::= string_literal
<array_constant> ::= '[' <constant> [, <constant>]+ ']'
```

<span data-ttu-id="5ade2-231">Em que:</span><span class="sxs-lookup"><span data-stu-id="5ade2-231">where:</span></span>

| <span data-ttu-id="5ade2-232">Símbolo</span><span class="sxs-lookup"><span data-stu-id="5ade2-232">Symbol</span></span> | <span data-ttu-id="5ade2-233">Definição</span><span class="sxs-lookup"><span data-stu-id="5ade2-233">Definition</span></span> |
| --- | --- |
| <span data-ttu-id="5ade2-234">attribute_name</span><span class="sxs-lookup"><span data-stu-id="5ade2-234">attribute_name</span></span> | <span data-ttu-id="5ade2-235">Uma propriedade de documento JSON Olá no Olá **FROM** coleção.</span><span class="sxs-lookup"><span data-stu-id="5ade2-235">Any property of hello JSON document in hello **FROM** collection.</span></span> |
| <span data-ttu-id="5ade2-236">binary_operator</span><span class="sxs-lookup"><span data-stu-id="5ade2-236">binary_operator</span></span> | <span data-ttu-id="5ade2-237">Nenhum operador binário listado no Olá [operadores](#operators) secção.</span><span class="sxs-lookup"><span data-stu-id="5ade2-237">Any binary operator listed in hello [Operators](#operators) section.</span></span> |
| <span data-ttu-id="5ade2-238">function_name</span><span class="sxs-lookup"><span data-stu-id="5ade2-238">function_name</span></span>| <span data-ttu-id="5ade2-239">Qualquer função listado no Olá [funções](#functions) secção.</span><span class="sxs-lookup"><span data-stu-id="5ade2-239">Any function listed in hello [Functions](#functions) section.</span></span> |
| <span data-ttu-id="5ade2-240">decimal_literal</span><span class="sxs-lookup"><span data-stu-id="5ade2-240">decimal_literal</span></span> |<span data-ttu-id="5ade2-241">Um número de vírgula flutuante expressado na notação decimal.</span><span class="sxs-lookup"><span data-stu-id="5ade2-241">A float expressed in decimal notation.</span></span> |
| <span data-ttu-id="5ade2-242">hexadecimal_literal</span><span class="sxs-lookup"><span data-stu-id="5ade2-242">hexadecimal_literal</span></span> |<span data-ttu-id="5ade2-243">Um número expresso por cadeia Olá '0x' seguido de uma cadeia de dígitos hexadecimais.</span><span class="sxs-lookup"><span data-stu-id="5ade2-243">A number expressed by hello string ‘0x’ followed by a string of hexadecimal digits.</span></span> |
| <span data-ttu-id="5ade2-244">string_literal</span><span class="sxs-lookup"><span data-stu-id="5ade2-244">string_literal</span></span> |<span data-ttu-id="5ade2-245">As literais de cadeia são cadeias Unicode representadas por uma sequência de zero ou mais carateres Unicode ou sequências de escape.</span><span class="sxs-lookup"><span data-stu-id="5ade2-245">String literals are Unicode strings represented by a sequence of zero or more Unicode characters or escape sequences.</span></span> <span data-ttu-id="5ade2-246">As literais de cadeia estão incluídas no plicas (apóstrofo: ') ou de aspas (aspas: ").</span><span class="sxs-lookup"><span data-stu-id="5ade2-246">String literals are enclosed in single quotes (apostrophe: ' ) or double quotes (quotation mark: ").</span></span> <span data-ttu-id="5ade2-247">Permitido escapes: `\'`, `\"`, `\\`, `\uXXXX` caracteres Unicode definido pelo 4 dígitos hexadecimais.</span><span class="sxs-lookup"><span data-stu-id="5ade2-247">Allowed escapes: `\'`, `\"`, `\\`, `\uXXXX` for Unicode characters defined by 4 hexadecimal digits.</span></span> |

### <a name="operators"></a><span data-ttu-id="5ade2-248">Operadores</span><span class="sxs-lookup"><span data-stu-id="5ade2-248">Operators</span></span>
<span data-ttu-id="5ade2-249">é suportado Olá seguintes operadores:</span><span class="sxs-lookup"><span data-stu-id="5ade2-249">hello following operators are supported:</span></span>

| <span data-ttu-id="5ade2-250">Família</span><span class="sxs-lookup"><span data-stu-id="5ade2-250">Family</span></span> | <span data-ttu-id="5ade2-251">Operadores</span><span class="sxs-lookup"><span data-stu-id="5ade2-251">Operators</span></span> |
| --- | --- |
| <span data-ttu-id="5ade2-252">Aritmética</span><span class="sxs-lookup"><span data-stu-id="5ade2-252">Arithmetic</span></span> |<span data-ttu-id="5ade2-253">+,-,*,/,%</span><span class="sxs-lookup"><span data-stu-id="5ade2-253">+,-,*,/,%</span></span> |
| <span data-ttu-id="5ade2-254">Lógica</span><span class="sxs-lookup"><span data-stu-id="5ade2-254">Logical</span></span> |<span data-ttu-id="5ade2-255">E, EM ALTERNATIVA, NÃO</span><span class="sxs-lookup"><span data-stu-id="5ade2-255">AND, OR, NOT</span></span> |
| <span data-ttu-id="5ade2-256">Comparação</span><span class="sxs-lookup"><span data-stu-id="5ade2-256">Comparison</span></span> |<span data-ttu-id="5ade2-257">=, !=, <, >, <=, >=, <></span><span class="sxs-lookup"><span data-stu-id="5ade2-257">=, !=, <, >, <=, >=, <></span></span> |

### <a name="functions"></a><span data-ttu-id="5ade2-258">Funções</span><span class="sxs-lookup"><span data-stu-id="5ade2-258">Functions</span></span>
<span data-ttu-id="5ade2-259">Ao consultar Olá duplos e tarefas, apenas é suportada a função é:</span><span class="sxs-lookup"><span data-stu-id="5ade2-259">When querying twins and jobs hello only supported function is:</span></span>

| <span data-ttu-id="5ade2-260">Função</span><span class="sxs-lookup"><span data-stu-id="5ade2-260">Function</span></span> | <span data-ttu-id="5ade2-261">Descrição</span><span class="sxs-lookup"><span data-stu-id="5ade2-261">Description</span></span> |
| -------- | ----------- |
| <span data-ttu-id="5ade2-262">IS_DEFINED(Property)</span><span class="sxs-lookup"><span data-stu-id="5ade2-262">IS_DEFINED(property)</span></span> | <span data-ttu-id="5ade2-263">Devolve um valor boleano que indica se foi atribuída um valor de propriedade de Olá (incluindo `null`).</span><span class="sxs-lookup"><span data-stu-id="5ade2-263">Returns a Boolean indicating if hello property has been assigned a value (including `null`).</span></span> |

<span data-ttu-id="5ade2-264">Em condições de rotas, Olá seguintes funções de bibliotecas é suportado:</span><span class="sxs-lookup"><span data-stu-id="5ade2-264">In routes conditions, hello following math functions are supported:</span></span>

| <span data-ttu-id="5ade2-265">Função</span><span class="sxs-lookup"><span data-stu-id="5ade2-265">Function</span></span> | <span data-ttu-id="5ade2-266">Descrição</span><span class="sxs-lookup"><span data-stu-id="5ade2-266">Description</span></span> |
| -------- | ----------- |
| <span data-ttu-id="5ade2-267">Abs(x)</span><span class="sxs-lookup"><span data-stu-id="5ade2-267">ABS(x)</span></span> | <span data-ttu-id="5ade2-268">Devolve Olá absoluto () especificado um valor positivo de Olá expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="5ade2-268">Returns hello absolute (positive) value of hello specified numeric expression.</span></span> |
| <span data-ttu-id="5ade2-269">Exp(x)</span><span class="sxs-lookup"><span data-stu-id="5ade2-269">EXP(x)</span></span> | <span data-ttu-id="5ade2-270">Devolve Olá valor exponencial Olá especificada a expressão numérica (i ^ x).</span><span class="sxs-lookup"><span data-stu-id="5ade2-270">Returns hello exponential value of hello specified numeric expression (e^x).</span></span> |
| <span data-ttu-id="5ade2-271">Power(x,y)</span><span class="sxs-lookup"><span data-stu-id="5ade2-271">POWER(x,y)</span></span> | <span data-ttu-id="5ade2-272">Devolve o valor de Olá especificado de Olá toohello de expressão especificado power (x ^ y).</span><span class="sxs-lookup"><span data-stu-id="5ade2-272">Returns hello value of hello specified expression toohello specified power (x^y).</span></span>|
| <span data-ttu-id="5ade2-273">SQUARE(x)</span><span class="sxs-lookup"><span data-stu-id="5ade2-273">SQUARE(x)</span></span> | <span data-ttu-id="5ade2-274">Olá devolve quadrado de Olá especificado valor numérico.</span><span class="sxs-lookup"><span data-stu-id="5ade2-274">Returns hello square of hello specified numeric value.</span></span> |
| <span data-ttu-id="5ade2-275">CEILING(x)</span><span class="sxs-lookup"><span data-stu-id="5ade2-275">CEILING(x)</span></span> | <span data-ttu-id="5ade2-276">Devolve Olá menor número inteiro maior que ou igual ao hello especificado expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="5ade2-276">Returns hello smallest integer value greater than, or equal to, hello specified numeric expression.</span></span> |
| <span data-ttu-id="5ade2-277">FLOOR(x)</span><span class="sxs-lookup"><span data-stu-id="5ade2-277">FLOOR(x)</span></span> | <span data-ttu-id="5ade2-278">Devolve um número inteiro maior de Olá inferior ou igual toohello especificada a expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="5ade2-278">Returns hello largest integer less than or equal toohello specified numeric expression.</span></span> |
| <span data-ttu-id="5ade2-279">Sign(x)</span><span class="sxs-lookup"><span data-stu-id="5ade2-279">SIGN(x)</span></span> | <span data-ttu-id="5ade2-280">Devolve Olá positivo (+ 1), zero (0), negativo (-1) sinal de Olá foi especificado ou expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="5ade2-280">Returns hello positive (+1), zero (0), or negative (-1) sign of hello specified numeric expression.</span></span>|
| <span data-ttu-id="5ade2-281">SQRT(x)</span><span class="sxs-lookup"><span data-stu-id="5ade2-281">SQRT(x)</span></span> | <span data-ttu-id="5ade2-282">Olá devolve quadrado de Olá especificado valor numérico.</span><span class="sxs-lookup"><span data-stu-id="5ade2-282">Returns hello square of hello specified numeric value.</span></span> |

<span data-ttu-id="5ade2-283">Em condições de rotas, é suportado Olá seguinte tipo de verificação e conversão de funções:</span><span class="sxs-lookup"><span data-stu-id="5ade2-283">In routes conditions, hello following type checking and casting functions are supported:</span></span>

| <span data-ttu-id="5ade2-284">Função</span><span class="sxs-lookup"><span data-stu-id="5ade2-284">Function</span></span> | <span data-ttu-id="5ade2-285">Descrição</span><span class="sxs-lookup"><span data-stu-id="5ade2-285">Description</span></span> |
| -------- | ----------- |
| <span data-ttu-id="5ade2-286">AS_NUMBER</span><span class="sxs-lookup"><span data-stu-id="5ade2-286">AS_NUMBER</span></span> | <span data-ttu-id="5ade2-287">Converte o número de tooa Olá cadeia de entrada.</span><span class="sxs-lookup"><span data-stu-id="5ade2-287">Converts hello input string tooa number.</span></span> <span data-ttu-id="5ade2-288">`noop`Se a entrada é um número; `Undefined` se a cadeia não representa um número.</span><span class="sxs-lookup"><span data-stu-id="5ade2-288">`noop` if input is a number; `Undefined` if string does not represent a number.</span></span>|
| <span data-ttu-id="5ade2-289">IS_ARRAY</span><span class="sxs-lookup"><span data-stu-id="5ade2-289">IS_ARRAY</span></span> | <span data-ttu-id="5ade2-290">Devolve um valor de Booleano indicando se Olá de Olá especificado expressão é uma matriz.</span><span class="sxs-lookup"><span data-stu-id="5ade2-290">Returns a Boolean value indicating if hello type of hello specified expression is an array.</span></span> |
| <span data-ttu-id="5ade2-291">IS_BOOL</span><span class="sxs-lookup"><span data-stu-id="5ade2-291">IS_BOOL</span></span> | <span data-ttu-id="5ade2-292">Devolve um valor de Booleano indicando se Olá de Olá especificado expressão é um valor booleano.</span><span class="sxs-lookup"><span data-stu-id="5ade2-292">Returns a Boolean value indicating if hello type of hello specified expression is a Boolean.</span></span> |
| <span data-ttu-id="5ade2-293">IS_DEFINED</span><span class="sxs-lookup"><span data-stu-id="5ade2-293">IS_DEFINED</span></span> | <span data-ttu-id="5ade2-294">Devolve um valor boleano que indica se foi atribuída um valor de propriedade de Olá.</span><span class="sxs-lookup"><span data-stu-id="5ade2-294">Returns a Boolean indicating if hello property has been assigned a value.</span></span> |
| <span data-ttu-id="5ade2-295">IS_NULL</span><span class="sxs-lookup"><span data-stu-id="5ade2-295">IS_NULL</span></span> | <span data-ttu-id="5ade2-296">Devolve um valor de Booleano indicando se Olá de Olá especificado expressão é nulo.</span><span class="sxs-lookup"><span data-stu-id="5ade2-296">Returns a Boolean value indicating if hello type of hello specified expression is null.</span></span> |
| <span data-ttu-id="5ade2-297">IS_NUMBER</span><span class="sxs-lookup"><span data-stu-id="5ade2-297">IS_NUMBER</span></span> | <span data-ttu-id="5ade2-298">Devolve um valor de Booleano indicando se Olá de Olá especificado expressão for um número.</span><span class="sxs-lookup"><span data-stu-id="5ade2-298">Returns a Boolean value indicating if hello type of hello specified expression is a number.</span></span> |
| <span data-ttu-id="5ade2-299">IS_OBJECT</span><span class="sxs-lookup"><span data-stu-id="5ade2-299">IS_OBJECT</span></span> | <span data-ttu-id="5ade2-300">Devolve um valor de Booleano indicando se Olá de Olá especificado expressão é um objeto JSON.</span><span class="sxs-lookup"><span data-stu-id="5ade2-300">Returns a Boolean value indicating if hello type of hello specified expression is a JSON object.</span></span> |
| <span data-ttu-id="5ade2-301">IS_PRIMITIVE</span><span class="sxs-lookup"><span data-stu-id="5ade2-301">IS_PRIMITIVE</span></span> | <span data-ttu-id="5ade2-302">Devolve um valor de Booleano indicando se Olá de Olá especificado expressão é uma primitiva (string, Boolean, numéricos ou `null`).</span><span class="sxs-lookup"><span data-stu-id="5ade2-302">Returns a Boolean value indicating if hello type of hello specified expression is a primitive (string, Boolean, numeric or `null`).</span></span> |
| <span data-ttu-id="5ade2-303">IS_STRING</span><span class="sxs-lookup"><span data-stu-id="5ade2-303">IS_STRING</span></span> | <span data-ttu-id="5ade2-304">Devolve um valor de Booleano indicando se Olá de Olá especificado expressão é uma cadeia.</span><span class="sxs-lookup"><span data-stu-id="5ade2-304">Returns a Boolean value indicating if hello type of hello specified expression is a string.</span></span> |

<span data-ttu-id="5ade2-305">Em condições de rotas, é suportado Olá seguintes funções de cadeia:</span><span class="sxs-lookup"><span data-stu-id="5ade2-305">In routes conditions, hello following string functions are supported:</span></span>

| <span data-ttu-id="5ade2-306">Função</span><span class="sxs-lookup"><span data-stu-id="5ade2-306">Function</span></span> | <span data-ttu-id="5ade2-307">Descrição</span><span class="sxs-lookup"><span data-stu-id="5ade2-307">Description</span></span> |
| -------- | ----------- |
| <span data-ttu-id="5ade2-308">CONCAT(x,...)</span><span class="sxs-lookup"><span data-stu-id="5ade2-308">CONCAT(x, …)</span></span> | <span data-ttu-id="5ade2-309">Devolve uma cadeia que é o resultado Olá concatenar duas ou mais valores de cadeia.</span><span class="sxs-lookup"><span data-stu-id="5ade2-309">Returns a string that is hello result of concatenating two or more string values.</span></span> |
| <span data-ttu-id="5ade2-310">LENGTH(x)</span><span class="sxs-lookup"><span data-stu-id="5ade2-310">LENGTH(x)</span></span> | <span data-ttu-id="5ade2-311">Devolve Olá número de carateres de Olá especificada a expressão de cadeia.</span><span class="sxs-lookup"><span data-stu-id="5ade2-311">Returns hello number of characters of hello specified string expression.</span></span>|
| <span data-ttu-id="5ade2-312">LOWER(x)</span><span class="sxs-lookup"><span data-stu-id="5ade2-312">LOWER(x)</span></span> | <span data-ttu-id="5ade2-313">Devolve uma expressão de cadeia após a conversão toolowercase de dados do caráter em maiúsculas.</span><span class="sxs-lookup"><span data-stu-id="5ade2-313">Returns a string expression after converting uppercase character data toolowercase.</span></span> |
| <span data-ttu-id="5ade2-314">UPPER(x)</span><span class="sxs-lookup"><span data-stu-id="5ade2-314">UPPER(x)</span></span> | <span data-ttu-id="5ade2-315">Devolve uma expressão de cadeia após a conversão toouppercase de dados do caráter em minúsculas.</span><span class="sxs-lookup"><span data-stu-id="5ade2-315">Returns a string expression after converting lowercase character data toouppercase.</span></span> |
| <span data-ttu-id="5ade2-316">SUBCADEIA (cadeia, início [, comprimento])</span><span class="sxs-lookup"><span data-stu-id="5ade2-316">SUBSTRING(string, start [, length])</span></span> | <span data-ttu-id="5ade2-317">Devolve parte de uma expressão de cadeia começando Olá especificado posição de caráter baseado em zero e continua a toohello especificado comprimento ou toohello fim da cadeia de Olá.</span><span class="sxs-lookup"><span data-stu-id="5ade2-317">Returns part of a string expression starting at hello specified character zero-based position and continues toohello specified length, or toohello end of hello string.</span></span> |
| <span data-ttu-id="5ade2-318">INDEX_OF (cadeia, fragmento)</span><span class="sxs-lookup"><span data-stu-id="5ade2-318">INDEX_OF(string, fragment)</span></span> | <span data-ttu-id="5ade2-319">Devolve Olá iniciar a posição da primeira ocorrência de Olá de Olá segunda cadeia expressão numa expressão de cadeia especificada primeiro Olá ou -1 se não é possível encontrar a cadeia de Olá.</span><span class="sxs-lookup"><span data-stu-id="5ade2-319">Returns hello starting position of hello first occurrence of hello second string expression within hello first specified string expression, or -1 if hello string is not found.</span></span>|
| <span data-ttu-id="5ade2-320">STARTS_WITH (x, y)</span><span class="sxs-lookup"><span data-stu-id="5ade2-320">STARTS_WITH(x, y)</span></span> | <span data-ttu-id="5ade2-321">Devolve um valor boleano que indica se primeira expressão de cadeia Olá começa com Olá segundo.</span><span class="sxs-lookup"><span data-stu-id="5ade2-321">Returns a Boolean indicating whether hello first string expression starts with hello second.</span></span> |
| <span data-ttu-id="5ade2-322">ENDS_WITH (x, y)</span><span class="sxs-lookup"><span data-stu-id="5ade2-322">ENDS_WITH(x, y)</span></span> | <span data-ttu-id="5ade2-323">Devolve um valor boleano que indica se primeira expressão de cadeia Olá termina com Olá segundo.</span><span class="sxs-lookup"><span data-stu-id="5ade2-323">Returns a Boolean indicating whether hello first string expression ends with hello second.</span></span> |
| <span data-ttu-id="5ade2-324">CONTAINS(x,y)</span><span class="sxs-lookup"><span data-stu-id="5ade2-324">CONTAINS(x,y)</span></span> | <span data-ttu-id="5ade2-325">Devolve um valor boleano que indica se primeira expressão de cadeia Olá contém Olá segundo.</span><span class="sxs-lookup"><span data-stu-id="5ade2-325">Returns a Boolean indicating whether hello first string expression contains hello second.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="5ade2-326">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="5ade2-326">Next steps</span></span>
<span data-ttu-id="5ade2-327">Saiba como tooexecute consulta nas suas aplicações utilizando [SDKs IoT do Azure][lnk-hub-sdks].</span><span class="sxs-lookup"><span data-stu-id="5ade2-327">Learn how tooexecute queries in your apps using [Azure IoT SDKs][lnk-hub-sdks].</span></span>

[lnk-query-where]: iot-hub-devguide-query-language.md#where-clause
[lnk-query-expressions]: iot-hub-devguide-query-language.md#expressions-and-conditions
[lnk-query-getstarted]: iot-hub-devguide-query-language.md#get-started-with-device-twin-queries

[lnk-twins]: iot-hub-devguide-device-twins.md
[lnk-jobs]: iot-hub-devguide-jobs.md
[lnk-devguide-endpoints]: iot-hub-devguide-endpoints.md
[lnk-devguide-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md
[lnk-devguide-messaging-routes]: iot-hub-devguide-messages-read-custom.md
[lnk-devguide-messaging-format]: iot-hub-devguide-messages-construct.md
[lnk-devguide-messaging-routes]: ./iot-hub-devguide-messages-read-custom.md

[lnk-hub-sdks]: iot-hub-devguide-sdks.md
