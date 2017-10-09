---
title: "suporte de feed aaaWorking com alteração de Olá do BD Azure Cosmos | Microsoft Docs"
description: "Utilização do Azure Cosmos DB alterar suporte feed tootrack alterações em documentos e efetuar com base em eventos processamento como acionadores e manter os sistemas de caches e análise atualizado."
keywords: "Alteração do feed"
services: cosmos-db
author: arramac
manager: jhubbard
editor: mimig
documentationcenter: 
ms.assetid: 2d7798db-857f-431a-b10f-3ccbc7d93b50
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: rest-api
ms.topic: article
ms.date: 08/15/2017
ms.author: arramac
ms.openlocfilehash: a4dcf4ceb476e3e08266dbcdcbee1d75e1d1eed4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="working-with-hello-change-feed-support-in-azure-cosmos-db"></a><span data-ttu-id="0cfdc-104">Trabalhar com suporte de feed de alteração de Olá do BD Azure Cosmos</span><span class="sxs-lookup"><span data-stu-id="0cfdc-104">Working with hello change feed support in Azure Cosmos DB</span></span>
<span data-ttu-id="0cfdc-105">[BD do Azure do Cosmos](../cosmos-db/introduction.md) são um fast e flexível globalmente replicados serviço de base de dados que é utilizado para armazenar dados de elevado volume transacionais e operacionais com latência previsível dígito milissegundo para leituras e escritas.</span><span class="sxs-lookup"><span data-stu-id="0cfdc-105">[Azure Cosmos DB](../cosmos-db/introduction.md) is a fast and flexible globally replicated database service that is used for storing high-volume transactional and operational data with predictable single-digit millisecond latency for reads and writes.</span></span> <span data-ttu-id="0cfdc-106">Isto torna adequada para IoT, revenda, jogos e aplicações de registo operacional.</span><span class="sxs-lookup"><span data-stu-id="0cfdc-106">This makes it well-suited for IoT, gaming, retail, and operational logging applications.</span></span> <span data-ttu-id="0cfdc-107">É um padrão de conceção comuns nestas aplicações tootrack alterações efetuadas tooAzure Cosmos DB dados e atualizar as vistas materializadas, efetuar a análise em tempo real, o armazenamento de dados de arquivo toocold e notificações de Acionador em determinados eventos com base nestas alterações.</span><span class="sxs-lookup"><span data-stu-id="0cfdc-107">A common design pattern in these applications is tootrack changes made tooAzure Cosmos DB data, and update materialized views, perform real-time analytics, archive data toocold storage, and trigger notifications on certain events based on these changes.</span></span> <span data-ttu-id="0cfdc-108">Olá **alteração feed suporte** do BD Azure Cosmos permite-lhe toobuild eficientes e dimensionáveis soluções para cada um desses padrões.</span><span class="sxs-lookup"><span data-stu-id="0cfdc-108">hello **change feed support** in Azure Cosmos DB enables you toobuild efficient and scalable solutions for each of these patterns.</span></span>

<span data-ttu-id="0cfdc-109">Com alteração de feed de suporte, base de dados do Azure Cosmos fornece uma lista ordenada de documentos dentro de uma coleção de base de dados do Azure Cosmos por ordem de Olá em que foram modificadas.</span><span class="sxs-lookup"><span data-stu-id="0cfdc-109">With change feed support, Azure Cosmos DB provides a sorted list of documents within an Azure Cosmos DB collection in hello order in which they were modified.</span></span> <span data-ttu-id="0cfdc-110">Este feed pode ser utilizado toolisten para modificações toodata dentro da coleção de Olá e realizar ações tais como:</span><span class="sxs-lookup"><span data-stu-id="0cfdc-110">This feed can be used toolisten for modifications toodata within hello collection and perform actions such as:</span></span>

* <span data-ttu-id="0cfdc-111">Acionar um tooan chamada API, quando um documento é inserido ou modificado</span><span class="sxs-lookup"><span data-stu-id="0cfdc-111">Trigger a call tooan API when a document is inserted or modified</span></span>
* <span data-ttu-id="0cfdc-112">Efetuar o processamento em tempo real (fluxo) sobre atualizações</span><span class="sxs-lookup"><span data-stu-id="0cfdc-112">Perform real-time (stream) processing on updates</span></span>
* <span data-ttu-id="0cfdc-113">Sincronizar dados com uma cache, o motor de busca ou do armazém de dados</span><span class="sxs-lookup"><span data-stu-id="0cfdc-113">Synchronize data with a cache, search engine, or data warehouse</span></span>

<span data-ttu-id="0cfdc-114">Alterações do BD Azure Cosmos são mantidas e podem ser processadas de forma assíncrona e distribuídas por um ou mais consumidores para processamento paralelo.</span><span class="sxs-lookup"><span data-stu-id="0cfdc-114">Changes in Azure Cosmos DB are persisted and can be processed asynchronously, and distributed across one or more consumers for parallel processing.</span></span> <span data-ttu-id="0cfdc-115">Vamos ver Olá APIs para o feed de alteração e como pode utilizá-los toobuild dimensionável, aplicações em tempo real.</span><span class="sxs-lookup"><span data-stu-id="0cfdc-115">Let's look at hello APIs for change feed and how you can use them toobuild scalable real-time applications.</span></span> <span data-ttu-id="0cfdc-116">Este artigo mostra como toowork com base de dados do Azure Cosmos alterar feed e Olá API do DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="0cfdc-116">This article shows how toowork with Azure Cosmos DB change feed and hello DocumentDB API.</span></span> 

![Utilizar base de dados do Azure Cosmos alteração feed toopower de análise em tempo real e condicionada por eventos cenários de computação](./media/change-feed/changefeedoverview.png)

> [!NOTE]
> <span data-ttu-id="0cfdc-118">Alteração de suporte de feed só é fornecida para Olá DocumentDB API nesta altura; Olá Graph API e a API de tabela não são atualmente suportadas.</span><span class="sxs-lookup"><span data-stu-id="0cfdc-118">Change feed support is only provided for hello DocumentDB API at this time; hello Graph API and Table API are not currently supported.</span></span>

## <a name="use-cases-and-scenarios"></a><span data-ttu-id="0cfdc-119">Cenários e casos de utilização</span><span class="sxs-lookup"><span data-stu-id="0cfdc-119">Use cases and scenarios</span></span>
<span data-ttu-id="0cfdc-120">Alteração feed permite processamento eficiente de grandes conjuntos de dados com um grande volume de escritas e oferece uma tooidentify de conjuntos de dados completo tooquerying alternativo que tenha sido alterado.</span><span class="sxs-lookup"><span data-stu-id="0cfdc-120">Change feed allows for efficient processing of large datasets with a high volume of writes, and offers an alternative tooquerying entire datasets tooidentify what has changed.</span></span> <span data-ttu-id="0cfdc-121">Por exemplo, pode efetuar Olá eficazmente os seguintes tarefas:</span><span class="sxs-lookup"><span data-stu-id="0cfdc-121">For example, you can perform hello following tasks efficiently:</span></span>

* <span data-ttu-id="0cfdc-122">Atualize uma cache, o índice de pesquisa ou um armazém de dados com dados armazenados na base de dados do Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="0cfdc-122">Update a cache, search index, or a data warehouse with data stored in Azure Cosmos DB.</span></span>
* <span data-ttu-id="0cfdc-123">Implementar dados ao nível da aplicação e o arquivo de camadas, ou seja, armazenar "dados" na base de dados do Azure Cosmos e expira "dados amovíveis" demasiado[Blob Storage do Azure](../storage/common/storage-introduction.md) ou [Azure Data Lake Store](../data-lake-store/data-lake-store-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0cfdc-123">Implement application-level data tiering and archival, that is, store "hot data" in Azure Cosmos DB, and age out "cold data" too[Azure Blob Storage](../storage/common/storage-introduction.md) or [Azure Data Lake Store](../data-lake-store/data-lake-store-overview.md).</span></span>
* <span data-ttu-id="0cfdc-124">Implementar a análise de lote em dados utilizando [do Apache Hadoop](run-hadoop-with-hdinsight.md).</span><span class="sxs-lookup"><span data-stu-id="0cfdc-124">Implement batch analytics on data using [Apache Hadoop](run-hadoop-with-hdinsight.md).</span></span>
* <span data-ttu-id="0cfdc-125">Implementar [pipelines de lambda no Azure](https://blogs.technet.microsoft.com/msuspartner/2016/01/27/azure-partner-community-big-data-advanced-analytics-and-lambda-architecture/) com base de dados do Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="0cfdc-125">Implement [lambda pipelines on Azure](https://blogs.technet.microsoft.com/msuspartner/2016/01/27/azure-partner-community-big-data-advanced-analytics-and-lambda-architecture/) with Azure Cosmos DB.</span></span> <span data-ttu-id="0cfdc-126">BD do Cosmos do Azure fornece uma solução de bases de dados dimensionável que pode processar ingestão e consulta e implementa arquiteturas de lambda com TCO baixa.</span><span class="sxs-lookup"><span data-stu-id="0cfdc-126">Azure Cosmos DB provides a scalable database solution that can handle both ingestion and query, and implement lambda architectures with low TCO.</span></span> 
* <span data-ttu-id="0cfdc-127">Efetue zero tooanother migrações de tempo inferior a conta de base de dados do Azure Cosmos com um esquema de partições diferente.</span><span class="sxs-lookup"><span data-stu-id="0cfdc-127">Perform zero down-time migrations tooanother Azure Cosmos DB account with a different partitioning scheme.</span></span>

<span data-ttu-id="0cfdc-128">**Lambda Pipelines com a BD do Cosmos do Azure para ingestão e a consulta:**</span><span class="sxs-lookup"><span data-stu-id="0cfdc-128">**Lambda Pipelines with Azure Cosmos DB for ingestion and query:**</span></span>

![Pipeline de lambda de BD do Cosmos com base do Azure para ingestão e consulta](./media/change-feed/lambda.png)

<span data-ttu-id="0cfdc-130">Pode utilizar a base de dados do Azure Cosmos tooreceive e armazenar dados de eventos de dispositivos, sensores, infraestrutura e de aplicações e processar estes eventos em tempo real com [Azure Stream Analytics](../stream-analytics/stream-analytics-documentdb-output.md), [Apache Storm](../hdinsight/hdinsight-storm-overview.md), ou [do Apache Spark](../hdinsight/hdinsight-apache-spark-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0cfdc-130">You can use Azure Cosmos DB tooreceive and store event data from devices, sensors, infrastructure, and applications, and process these events in real-time with [Azure Stream Analytics](../stream-analytics/stream-analytics-documentdb-output.md), [Apache Storm](../hdinsight/hdinsight-storm-overview.md), or [Apache Spark](../hdinsight/hdinsight-apache-spark-overview.md).</span></span> 

<span data-ttu-id="0cfdc-131">Dentro do seu [sem servidor](http://azure.com/serverless) web apps e móveis, pode controlar eventos como tootrigger de perfil, as preferências ou localização do cliente tooyour alterações determinadas ações, como o envio de push dispositivos tootheir de notificações utilizando [As funções do azure](../azure-functions/functions-bindings-documentdb.md) ou [serviços aplicacionais](https://azure.microsoft.com/services/app-service/).</span><span class="sxs-lookup"><span data-stu-id="0cfdc-131">Within your [serverless](http://azure.com/serverless) web and mobile apps, you can track events such as changes tooyour customer's profile, preferences, or location tootrigger certain actions like sending push notifications tootheir devices using [Azure Functions](../azure-functions/functions-bindings-documentdb.md) or [App Services](https://azure.microsoft.com/services/app-service/).</span></span> <span data-ttu-id="0cfdc-132">Se estiver a utilizar a base de dados do Azure Cosmos toobuild um jogo, por exemplo, pode utilizar alteração feed tooimplement leaderboards em tempo real com base no pontuações de jogos concluídas.</span><span class="sxs-lookup"><span data-stu-id="0cfdc-132">If you're using Azure Cosmos DB toobuild a game, you can, for example, use change feed tooimplement real-time leaderboards based on scores from completed games.</span></span>

## <a name="how-change-feed-works-in-azure-cosmos-db"></a><span data-ttu-id="0cfdc-133">Como funciona o feed de alteração do BD Azure Cosmos</span><span class="sxs-lookup"><span data-stu-id="0cfdc-133">How change feed works in Azure Cosmos DB</span></span>
<span data-ttu-id="0cfdc-134">BD do Azure do Cosmos fornece Olá capacidade tooincrementally ler atualizações efetuadas tooan coleção da base de dados do Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="0cfdc-134">Azure Cosmos DB provides hello ability tooincrementally read updates made tooan Azure Cosmos DB collection.</span></span> <span data-ttu-id="0cfdc-135">Este feed de alteração tem Olá seguintes propriedades:</span><span class="sxs-lookup"><span data-stu-id="0cfdc-135">This change feed has hello following properties:</span></span>

* <span data-ttu-id="0cfdc-136">As alterações sejam persistentes na base de dados do Azure Cosmos e podem ser processadas de forma assíncrona.</span><span class="sxs-lookup"><span data-stu-id="0cfdc-136">Changes are persistent in Azure Cosmos DB and can be processed asynchronously.</span></span>
* <span data-ttu-id="0cfdc-137">As alterações toodocuments dentro de uma coleção estão disponíveis imediatamente no feed de alteração de Olá.</span><span class="sxs-lookup"><span data-stu-id="0cfdc-137">Changes toodocuments within a collection are available immediately in hello change feed.</span></span>
* <span data-ttu-id="0cfdc-138">Cada documento de tooa alteração aparece exatamente uma vez no feed de alteração de Olá e clientes gerir os respetivos lógica de pontos de verificação.</span><span class="sxs-lookup"><span data-stu-id="0cfdc-138">Each change tooa document appears exactly once in hello change feed, and clients manage their checkpointing logic.</span></span> <span data-ttu-id="0cfdc-139">biblioteca de processador de feed de alteração de Olá fornece pontos de verificação automático e ", pelo menos, uma vez" semântica.</span><span class="sxs-lookup"><span data-stu-id="0cfdc-139">hello change feed processor library provides automatic checkpointing and "at least once" semantics.</span></span>
* <span data-ttu-id="0cfdc-140">Apenas alteração mais recente de Olá para um determinado documento está incluída no registo de alterações de Olá.</span><span class="sxs-lookup"><span data-stu-id="0cfdc-140">Only hello most recent change for a given document is included in hello change log.</span></span> <span data-ttu-id="0cfdc-141">Alterações intermédias poderão não estar disponíveis.</span><span class="sxs-lookup"><span data-stu-id="0cfdc-141">Intermediate changes may not be available.</span></span>
* <span data-ttu-id="0cfdc-142">Olá alteração feed é ordenada by order of modificação dentro de cada valor de chave de partição.</span><span class="sxs-lookup"><span data-stu-id="0cfdc-142">hello change feed is sorted by order of modification within each partition key value.</span></span> <span data-ttu-id="0cfdc-143">Não há nenhuma ordem garantida entre os valores de chave de partição.</span><span class="sxs-lookup"><span data-stu-id="0cfdc-143">There is no guaranteed order across partition-key values.</span></span>
* <span data-ttu-id="0cfdc-144">As alterações podem ser sincronizadas a partir de qualquer ponto no tempo, ou seja, não existe nenhum período de retenção de dados fixa para o qual as alterações estão disponíveis.</span><span class="sxs-lookup"><span data-stu-id="0cfdc-144">Changes can be synchronized from any point-in-time, that is, there is no fixed data retention period for which changes are available.</span></span>
* <span data-ttu-id="0cfdc-145">As alterações estão disponíveis em segmentos de intervalos de chaves de partição.</span><span class="sxs-lookup"><span data-stu-id="0cfdc-145">Changes are available in chunks of partition key ranges.</span></span> <span data-ttu-id="0cfdc-146">Esta capacidade permite alterações de toobe de coleções de grandes dimensões processados em paralelo por vários consumidores/servidores.</span><span class="sxs-lookup"><span data-stu-id="0cfdc-146">This capability allows changes from large collections toobe processed in parallel by multiple consumers/servers.</span></span>
* <span data-ttu-id="0cfdc-147">As aplicações podem o pedido de alteração vários feeds em simultâneo no Olá mesma coleção.</span><span class="sxs-lookup"><span data-stu-id="0cfdc-147">Applications can request for multiple change feeds simultaneously on hello same collection.</span></span>

<span data-ttu-id="0cfdc-148">Feed de alteração da BD Cosmos do Azure está ativada por predefinição para todas as contas.</span><span class="sxs-lookup"><span data-stu-id="0cfdc-148">Azure Cosmos DB's change feed is enabled by default for all accounts.</span></span> <span data-ttu-id="0cfdc-149">Pode utilizar o [débito aprovisionado](request-units.md) na sua região de escrita ou qualquer [ler região](distribute-data-globally.md) tooread de Olá alterar feed, tal como qualquer outra operação da base de dados do Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="0cfdc-149">You can use your [provisioned throughput](request-units.md) in your write region or any [read region](distribute-data-globally.md) tooread from hello change feed, just like any other operation from Azure Cosmos DB.</span></span> <span data-ttu-id="0cfdc-150">Olá alteração feed inclui as operações de atualização efetuadas toodocuments dentro da coleção de Olá e inserções.</span><span class="sxs-lookup"><span data-stu-id="0cfdc-150">hello change feed includes inserts and update operations made toodocuments within hello collection.</span></span> <span data-ttu-id="0cfdc-151">Pode capturar eliminações ao definir um sinalizador de "eliminar de forma recuperável" dentro os documentos em vez de eliminações.</span><span class="sxs-lookup"><span data-stu-id="0cfdc-151">You can capture deletes by setting a "soft-delete" flag within your documents in place of deletes.</span></span> <span data-ttu-id="0cfdc-152">Em alternativa, pode definir um período de expiração finita para os documentos através de Olá [capacidade TTL](time-to-live.md), para o exemplo, 24 horas e a utilização Olá valor da propriedade toocapture elimina.</span><span class="sxs-lookup"><span data-stu-id="0cfdc-152">Alternatively, you can set a finite expiration period for your documents via hello [TTL capability](time-to-live.md), for example, 24 hours and use hello value of that property toocapture deletes.</span></span> <span data-ttu-id="0cfdc-153">Com esta solução, tem alterações tooprocess dentro de um intervalo de tempo mais curto que o período de expiração do Olá TTL.</span><span class="sxs-lookup"><span data-stu-id="0cfdc-153">With this solution, you have tooprocess changes within a shorter time interval than hello TTL expiration period.</span></span> <span data-ttu-id="0cfdc-154">Olá alteração feed está disponível para cada intervalo de chave de partição dentro da coleção de documentos Olá e, por conseguinte, pode ser distribuído por um ou mais consumidores para processamento paralelo.</span><span class="sxs-lookup"><span data-stu-id="0cfdc-154">hello change feed is available for each partition key range within hello document collection, and thus can be distributed across one or more consumers for parallel processing.</span></span> 

![Feed de processamento distribuído de alteração de base de dados do Azure Cosmos](./media/change-feed/changefeedvisual.png)

<span data-ttu-id="0cfdc-156">Tem algumas opções como implementar uma alteração do feed no seu código de cliente.</span><span class="sxs-lookup"><span data-stu-id="0cfdc-156">You have a few options in how you implement a change feed in your client code.</span></span> <span data-ttu-id="0cfdc-157">Olá secções que imediatamente a seguir descrevem como tooimplement Olá utilizando Olá API REST da Azure Cosmos DB de feed de alteração e Olá SDKs do DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="0cfdc-157">hello sections that immediately follow describe how tooimplement hello change feed using hello Azure Cosmos DB REST API and hello DocumentDB SDKs.</span></span> <span data-ttu-id="0cfdc-158">No entanto, para aplicações de .NET, recomendamos que utilize Olá novo [alteração feed biblioteca processador](#change-feed-processor) para eventos de processamento de Olá alteração feed como simplifica as alterações de leitura em partições e permite que vários threads a funcionar no paralelo.</span><span class="sxs-lookup"><span data-stu-id="0cfdc-158">However, for .NET applications, we recommend using hello new [Change feed processor library](#change-feed-processor) for processing events from hello change feed as it simplifies reading changes across partitions and enables multiple threads working in parallel.</span></span> 

## <span data-ttu-id="0cfdc-159"><a id="rest-apis"></a>Trabalhar com Olá REST API e SDKs do DocumentDB</span><span class="sxs-lookup"><span data-stu-id="0cfdc-159"><a id="rest-apis"></a>Working with hello REST API and DocumentDB SDKs</span></span>
<span data-ttu-id="0cfdc-160">BD do Azure do Cosmos fornece elásticos contentores de armazenamento e débito chamado **coleções**.</span><span class="sxs-lookup"><span data-stu-id="0cfdc-160">Azure Cosmos DB provides elastic containers of storage and throughput called **collections**.</span></span> <span data-ttu-id="0cfdc-161">Os dados dentro de coleções são logicamente agrupados utilizando [chaves de partição](partition-data.md) para escalabilidade e desempenho.</span><span class="sxs-lookup"><span data-stu-id="0cfdc-161">Data within collections is logically grouped using [partition keys](partition-data.md) for scalability and performance.</span></span> <span data-ttu-id="0cfdc-162">BD do Azure do Cosmos fornece diversas APIs para aceder a estes dados, incluindo a pesquisa por ID (leitura/Get), consulta e feeds de leitura (análises).</span><span class="sxs-lookup"><span data-stu-id="0cfdc-162">Azure Cosmos DB provides various APIs for accessing this data, including lookup by ID (Read/Get), query, and read-feeds (scans).</span></span> <span data-ttu-id="0cfdc-163">Olá feed de alteração pode ser obtido ao preencher dois novos pedido cabeçalhos toohello DocumentDB `ReadDocumentFeed` API e podem ser processados em paralelo em intervalos de chaves de partição.</span><span class="sxs-lookup"><span data-stu-id="0cfdc-163">hello change feed can be obtained by populating two new request headers toohello DocumentDB `ReadDocumentFeed` API, and can be processed in parallel across ranges of partition keys.</span></span>

### <a name="readdocumentfeed-api"></a><span data-ttu-id="0cfdc-164">ReadDocumentFeed API</span><span class="sxs-lookup"><span data-stu-id="0cfdc-164">ReadDocumentFeed API</span></span>
<span data-ttu-id="0cfdc-165">Vamos observe breve como ReadDocumentFeed funciona.</span><span class="sxs-lookup"><span data-stu-id="0cfdc-165">Let's take a brief look at how ReadDocumentFeed works.</span></span> <span data-ttu-id="0cfdc-166">BD do Azure do Cosmos suporta a leitura de um feed de documentos numa coleção através de Olá `ReadDocumentFeed` API.</span><span class="sxs-lookup"><span data-stu-id="0cfdc-166">Azure Cosmos DB supports reading a feed of documents within a collection via hello `ReadDocumentFeed` API.</span></span> <span data-ttu-id="0cfdc-167">Por exemplo, hello pedido seguinte devolve uma página de documentos no interior Olá `serverlogs` coleção.</span><span class="sxs-lookup"><span data-stu-id="0cfdc-167">For example, hello following request returns a page of documents inside hello `serverlogs` collection.</span></span> 

    GET https://mydocumentdb.documents.azure.com/dbs/smalldb/colls/serverlogs HTTP/1.1
    x-ms-date: Tue, 22 Nov 2016 17:05:14 GMT
    authorization: type%3dmaster%26ver%3d1.0%26sig%3dgo7JEogZDn6ritWhwc5hX%2fNTV4wwM1u9V2Is1H4%2bDRg%3d
    Cache-Control: no-cache
    x-ms-consistency-level: Strong
    User-Agent: Microsoft.Azure.Documents.Client/1.10.27.5
    x-ms-version: 2016-07-11
    Accept: application/json
    Host: mydocumentdb.documents.azure.com

<span data-ttu-id="0cfdc-168">Os resultados podem ser limitados utilizando Olá `x-ms-max-item-count` cabeçalho e leituras podem ser retomado por voltar a submeter pedido Olá com um `x-ms-continuation` cabeçalho devolvido na resposta anterior Olá.</span><span class="sxs-lookup"><span data-stu-id="0cfdc-168">Results can be limited by using hello `x-ms-max-item-count` header, and reads can be resumed by resubmitting hello request with a `x-ms-continuation` header returned in hello previous response.</span></span> <span data-ttu-id="0cfdc-169">Durante a execução de um único cliente, `ReadDocumentFeed` itera através de resultados em partições serialmente.</span><span class="sxs-lookup"><span data-stu-id="0cfdc-169">When performed from a single client, `ReadDocumentFeed` iterates through results across partitions serially.</span></span> 

<span data-ttu-id="0cfdc-170">**Série ler o feed do documento**</span><span class="sxs-lookup"><span data-stu-id="0cfdc-170">**Serial read document feed**</span></span>

<span data-ttu-id="0cfdc-171">Também pode obter o feed Olá de documentos através de um dos Olá suportado [SDKs de BD do Azure Cosmos](documentdb-sdk-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="0cfdc-171">You can also retrieve hello feed of documents using one of hello supported [Azure Cosmos DB SDKs](documentdb-sdk-dotnet.md).</span></span> <span data-ttu-id="0cfdc-172">Por exemplo, Olá seguinte fragmento mostra como toouse Olá [ReadDocumentFeedAsync método](/dotnet/api/microsoft.azure.documents.client.documentclient.readdocumentfeedasync?view=azure-dotnet) no .NET.</span><span class="sxs-lookup"><span data-stu-id="0cfdc-172">For example, hello following snippet shows how toouse hello [ReadDocumentFeedAsync method](/dotnet/api/microsoft.azure.documents.client.documentclient.readdocumentfeedasync?view=azure-dotnet) in .NET.</span></span>

```csharp
FeedResponse<dynamic> feedResponse = null;
do
{
    feedResponse = await client.ReadDocumentFeedAsync(collection, new FeedOptions { MaxItemCount = -1 });
}
while (feedResponse.ResponseContinuation != null);
```

### <a name="distributed-execution-of-readdocumentfeed"></a><span data-ttu-id="0cfdc-173">Execução distribuída do ReadDocumentFeed</span><span class="sxs-lookup"><span data-stu-id="0cfdc-173">Distributed execution of ReadDocumentFeed</span></span>
<span data-ttu-id="0cfdc-174">Para coleções que contêm terabytes de dados ou mais, ou um grande volume de atualizações de inserção, execução de série do feed de leitura de um único computador cliente poderá não ser prática.</span><span class="sxs-lookup"><span data-stu-id="0cfdc-174">For collections that contain terabytes of data or more, or ingest a large volume of updates, serial execution of read feed from a single client machine might not be practical.</span></span> <span data-ttu-id="0cfdc-175">Na ordem toosupport nestes cenários de macrodados, Azure Cosmos DB fornece APIs toodistribute `ReadDocumentFeed` chamadas de forma transparente entre vários cliente de leitores de consumidores.</span><span class="sxs-lookup"><span data-stu-id="0cfdc-175">In order toosupport these big data scenarios, Azure Cosmos DB provides APIs toodistribute `ReadDocumentFeed` calls transparently across multiple client readers/consumers.</span></span> 

<span data-ttu-id="0cfdc-176">**Feed do documento de leitura distribuída**</span><span class="sxs-lookup"><span data-stu-id="0cfdc-176">**Distributed Read Document Feed**</span></span>

<span data-ttu-id="0cfdc-177">tooprovide processamento dimensionável de alterações incrementais, Cosmos BD do Azure suporta um modelo de escalamento horizontal para alteração Olá feed API com base nos intervalos de chaves de partição.</span><span class="sxs-lookup"><span data-stu-id="0cfdc-177">tooprovide scalable processing of incremental changes, Azure Cosmos DB supports a scale-out model for hello change feed API based on ranges of partition keys.</span></span>

* <span data-ttu-id="0cfdc-178">Pode obter uma lista de partição intervalos de chaves para uma coleção efetuar um `ReadPartitionKeyRanges` chamada.</span><span class="sxs-lookup"><span data-stu-id="0cfdc-178">You can obtain a list of partition key ranges for a collection performing a `ReadPartitionKeyRanges` call.</span></span> 
* <span data-ttu-id="0cfdc-179">Para cada intervalo de chave de partição, pode realizar uma `ReadDocumentFeed` tooread documentos com chaves de partição dentro desse intervalo.</span><span class="sxs-lookup"><span data-stu-id="0cfdc-179">For each partition key range, you can perform a `ReadDocumentFeed` tooread documents with partition keys within that range.</span></span>

### <a name="retrieving-partition-key-ranges-for-a-collection"></a><span data-ttu-id="0cfdc-180">Obter intervalos de chaves de partição para uma coleção</span><span class="sxs-lookup"><span data-stu-id="0cfdc-180">Retrieving partition key ranges for a collection</span></span>
<span data-ttu-id="0cfdc-181">Pode obter intervalos de chaves de partição de Olá pelo requerente Olá `pkranges` recursos numa coleção.</span><span class="sxs-lookup"><span data-stu-id="0cfdc-181">You can retrieve hello partition key ranges by requesting hello `pkranges` resource within a collection.</span></span> <span data-ttu-id="0cfdc-182">Por exemplo Olá pedido seguinte obtém Olá lista de intervalos de chaves de partição para Olá `serverlogs` coleção:</span><span class="sxs-lookup"><span data-stu-id="0cfdc-182">For example hello following request retrieves hello list of partition key ranges for hello `serverlogs` collection:</span></span>

    GET https://querydemo.documents.azure.com/dbs/bigdb/colls/serverlogs/pkranges HTTP/1.1
    x-ms-date: Tue, 15 Nov 2016 07:26:51 GMT
    authorization: type%3dmaster%26ver%3d1.0%26sig%3dEConYmRgDExu6q%2bZ8GjfUGOH0AcOx%2behkancw3LsGQ8%3d
    x-ms-consistency-level: Session
    x-ms-version: 2016-07-11
    Accept: application/json
    Host: querydemo.documents.azure.com

<span data-ttu-id="0cfdc-183">Este pedido devolve Olá resposta que contém metadados sobre intervalos de chaves de partição de Olá os seguintes:</span><span class="sxs-lookup"><span data-stu-id="0cfdc-183">This request returns hello following response containing metadata about hello partition key ranges:</span></span>

    HTTP/1.1 200 Ok
    Content-Type: application/json
    x-ms-item-count: 25
    x-ms-schemaversion: 1.1
    Date: Tue, 15 Nov 2016 07:26:51 GMT

    {
       "_rid":"qYcAAPEvJBQ=",
       "PartitionKeyRanges":[
          {
             "_rid":"qYcAAPEvJBQCAAAAAAAAUA==",
             "id":"0",
             "_etag":"\"00002800-0000-0000-0000-580ac4ea0000\"",
             "minInclusive":"",
             "maxExclusive":"05C1CFFFFFFFF8",
             "_self":"dbs\/qYcAAA==\/colls\/qYcAAPEvJBQ=\/pkranges\/qYcAAPEvJBQCAAAAAAAAUA==\/",
             "_ts":1477100776
          },
          ...
       ],
       "_count": 25
    }


<span data-ttu-id="0cfdc-184">**Propriedades de intervalo de chaves de partição**: cada intervalo de chave de partição inclui as propriedades de metadados de Olá Olá a tabela seguinte:</span><span class="sxs-lookup"><span data-stu-id="0cfdc-184">**Partition key range properties**: Each partition key range includes hello metadata properties in hello following table:</span></span>

<table>
    <tr>
        <th><span data-ttu-id="0cfdc-185">Nome do cabeçalho</span><span class="sxs-lookup"><span data-stu-id="0cfdc-185">Header name</span></span></th>
        <th><span data-ttu-id="0cfdc-186">Descrição</span><span class="sxs-lookup"><span data-stu-id="0cfdc-186">Description</span></span></th>
    </tr>
    <tr>
        <td><span data-ttu-id="0cfdc-187">ID</span><span class="sxs-lookup"><span data-stu-id="0cfdc-187">id</span></span></td>
        <td>
            <p><span data-ttu-id="0cfdc-188">ID de Olá de intervalo de chave de partição de Olá.</span><span class="sxs-lookup"><span data-stu-id="0cfdc-188">hello ID for hello partition key range.</span></span> <span data-ttu-id="0cfdc-189">Este é um ID exclusivo e estável dentro de cada coleção.</span><span class="sxs-lookup"><span data-stu-id="0cfdc-189">This is a stable and unique ID within each collection.</span></span></p>
            <p><span data-ttu-id="0cfdc-190">Tem de ser utilizado no Olá seguir chamada tooread alterações ao intervalo de chaves de partição.</span><span class="sxs-lookup"><span data-stu-id="0cfdc-190">Must be used in hello following call tooread changes by partition key range.</span></span></p>
        </td>
    </tr>
    <tr>
        <td><span data-ttu-id="0cfdc-191">maxExclusive</span><span class="sxs-lookup"><span data-stu-id="0cfdc-191">maxExclusive</span></span></td>
        <td><span data-ttu-id="0cfdc-192">valor de hash de chave de partição máximo de Olá para o intervalo de chave de partição de Olá.</span><span class="sxs-lookup"><span data-stu-id="0cfdc-192">hello maximum partition key hash value for hello partition key range.</span></span> <span data-ttu-id="0cfdc-193">Para utilização interna.</span><span class="sxs-lookup"><span data-stu-id="0cfdc-193">For internal use.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="0cfdc-194">minInclusive</span><span class="sxs-lookup"><span data-stu-id="0cfdc-194">minInclusive</span></span></td>
        <td><span data-ttu-id="0cfdc-195">valor de hash de chave de partição mínima de Olá para o intervalo de chaves de partição do Olá.</span><span class="sxs-lookup"><span data-stu-id="0cfdc-195">hello minimum partition key hash value for hello partition key range.</span></span> <span data-ttu-id="0cfdc-196">Para utilização interna.</span><span class="sxs-lookup"><span data-stu-id="0cfdc-196">For internal use.</span></span></td>
    </tr>       
</table>

<span data-ttu-id="0cfdc-197">Isto pode ser feito utilizando um dos Olá suportado [SDKs de BD do Azure Cosmos](documentdb-sdk-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="0cfdc-197">You can do this using one of hello supported [Azure Cosmos DB SDKs](documentdb-sdk-dotnet.md).</span></span> <span data-ttu-id="0cfdc-198">Por exemplo, hello fragmento seguinte mostra como a chave de partição tooretrieve intervalos no .NET utilizando Olá [ReadPartitionKeyRangeFeedAsync](/dotnet/api/microsoft.azure.documents.client.documentclient.readpartitionkeyrangefeedasync?view=azure-dotnet) método.</span><span class="sxs-lookup"><span data-stu-id="0cfdc-198">For example, hello following snippet shows how tooretrieve partition key ranges in .NET using hello [ReadPartitionKeyRangeFeedAsync](/dotnet/api/microsoft.azure.documents.client.documentclient.readpartitionkeyrangefeedasync?view=azure-dotnet) method.</span></span>

```csharp
string pkRangesResponseContinuation = null;
List<PartitionKeyRange> partitionKeyRanges = new List<PartitionKeyRange>();

do
{
    FeedResponse<PartitionKeyRange> pkRangesResponse = await client.ReadPartitionKeyRangeFeedAsync(
        collectionUri, 
        new FeedOptions { RequestContinuation = pkRangesResponseContinuation });

    partitionKeyRanges.AddRange(pkRangesResponse);
    pkRangesResponseContinuation = pkRangesResponse.ResponseContinuation;
}
while (pkRangesResponseContinuation != null);
```

<span data-ttu-id="0cfdc-199">BD do Cosmos do Azure suporta a obtenção de documentos por intervalo de chaves de partição, definição Olá opcional `x-ms-documentdb-partitionkeyrangeid` cabeçalho.</span><span class="sxs-lookup"><span data-stu-id="0cfdc-199">Azure Cosmos DB supports retrieval of documents per partition key range by setting hello optional `x-ms-documentdb-partitionkeyrangeid` header.</span></span> 

### <a name="performing-an-incremental-readdocumentfeed"></a><span data-ttu-id="0cfdc-200">Efetuar uma ReadDocumentFeed incremental</span><span class="sxs-lookup"><span data-stu-id="0cfdc-200">Performing an incremental ReadDocumentFeed</span></span>
<span data-ttu-id="0cfdc-201">ReadDocumentFeed suporta Olá cenários/tarefas para processamento incremental das alterações de coleções de base de dados do Azure Cosmos os seguintes:</span><span class="sxs-lookup"><span data-stu-id="0cfdc-201">ReadDocumentFeed supports hello following scenarios/tasks for incremental processing of changes in Azure Cosmos DB collections:</span></span>

* <span data-ttu-id="0cfdc-202">Ler todas as alterações toodocuments desde o início de Olá, ou seja, da criação de coleção.</span><span class="sxs-lookup"><span data-stu-id="0cfdc-202">Read all changes toodocuments from hello beginning, that is, from collection creation.</span></span>
* <span data-ttu-id="0cfdc-203">Ler todas as alterações toofuture atualizações toodocuments da hora atual, ou todas as alterações desde um período de tempo de utilizador especificado.</span><span class="sxs-lookup"><span data-stu-id="0cfdc-203">Read all changes toofuture updates toodocuments from current time, or any changes since a user-specified time.</span></span>
* <span data-ttu-id="0cfdc-204">Ler todas as alterações toodocuments a partir de uma versão lógica da coleção de Olá (ETag).</span><span class="sxs-lookup"><span data-stu-id="0cfdc-204">Read all changes toodocuments from a logical version of hello collection (ETag).</span></span> <span data-ttu-id="0cfdc-205">Pode os consumidores com base no Olá devolvido ETag de pedidos de leitura feed incrementais de ponto de verificação.</span><span class="sxs-lookup"><span data-stu-id="0cfdc-205">You can checkpoint your consumers based on hello returned ETag from incremental read-feed requests.</span></span>

<span data-ttu-id="0cfdc-206">alterações de Olá incluem toodocuments inserções e atualizações.</span><span class="sxs-lookup"><span data-stu-id="0cfdc-206">hello changes include inserts and updates toodocuments.</span></span> <span data-ttu-id="0cfdc-207">Elimina toocapture, tem de utilizar uma propriedade de "eliminação de forma recuperável" dentro os documentos ou utilizar Olá [propriedade incorporada do TTL](time-to-live.md) toosignal uma eliminação pendente no Olá alterar feed.</span><span class="sxs-lookup"><span data-stu-id="0cfdc-207">toocapture deletes, you must use a "soft delete" property within your documents, or use hello [built-in TTL property](time-to-live.md) toosignal a pending deletion in hello change feed.</span></span>

<span data-ttu-id="0cfdc-208">Olá seguinte tabela apresenta uma lista de Olá [pedido](/rest/api/documentdb/common-documentdb-rest-request-headers.md) e [cabeçalhos de resposta](/rest/api/documentdb/common-documentdb-rest-response-headers.md) para operações de ReadDocumentFeed.</span><span class="sxs-lookup"><span data-stu-id="0cfdc-208">hello following table lists hello [request](/rest/api/documentdb/common-documentdb-rest-request-headers.md) and [response headers](/rest/api/documentdb/common-documentdb-rest-response-headers.md) for ReadDocumentFeed operations.</span></span>

<span data-ttu-id="0cfdc-209">**Cabeçalhos de pedido para incremental ReadDocumentFeed**:</span><span class="sxs-lookup"><span data-stu-id="0cfdc-209">**Request headers for incremental ReadDocumentFeed**:</span></span>

<table>
    <tr>
        <th><span data-ttu-id="0cfdc-210">Nome do cabeçalho</span><span class="sxs-lookup"><span data-stu-id="0cfdc-210">Header name</span></span></th>
        <th><span data-ttu-id="0cfdc-211">Descrição</span><span class="sxs-lookup"><span data-stu-id="0cfdc-211">Description</span></span></th>
    </tr>
    <tr>
        <td><span data-ttu-id="0cfdc-212">A MI</span><span class="sxs-lookup"><span data-stu-id="0cfdc-212">A-IM</span></span></td>
        <td><span data-ttu-id="0cfdc-213">Tem de ser definido demasiado "Incremental feed", ou omitido caso contrário</span><span class="sxs-lookup"><span data-stu-id="0cfdc-213">Must be set too"Incremental feed", or omitted otherwise</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="0cfdc-214">If-None-Match</span><span class="sxs-lookup"><span data-stu-id="0cfdc-214">If-None-Match</span></span></td>
        <td>
            <p><span data-ttu-id="0cfdc-215">Não existe um cabeçalho: devolve todas as alterações de Olá a partir da (criação de coleção)</span><span class="sxs-lookup"><span data-stu-id="0cfdc-215">No header: returns all changes from hello beginning (collection creation)</span></span></p>
            <p><span data-ttu-id="0cfdc-216">"*": devolve todas as novas alterações toodata dentro da coleção de Olá</span><span class="sxs-lookup"><span data-stu-id="0cfdc-216">"*": returns all new changes toodata within hello collection</span></span></p>         
            <p><span data-ttu-id="0cfdc-217">&lt;ETag&gt;: Se definir tooa coleção ETag, devolve todas as alterações efetuadas desde que timestamp lógica</span><span class="sxs-lookup"><span data-stu-id="0cfdc-217">&lt;etag&gt;: If set tooa collection ETag, returns all changes made since that logical timestamp</span></span></p>
        </td>
    </tr>
    <tr>    
        <td><span data-ttu-id="0cfdc-218">Se-modificado-Since</span><span class="sxs-lookup"><span data-stu-id="0cfdc-218">If-Modified-Since</span></span></td> 
        <td><span data-ttu-id="0cfdc-219">Formato de hora RFC 1123; ignorado se If-None-Match foi especificado</span><span class="sxs-lookup"><span data-stu-id="0cfdc-219">RFC 1123 time format; ignored if If-None-Match is specified</span></span></td> 
    </tr> 
    <tr>
        <td><span data-ttu-id="0cfdc-220">x-ms-documentdb-partitionkeyrangeid</span><span class="sxs-lookup"><span data-stu-id="0cfdc-220">x-ms-documentdb-partitionkeyrangeid</span></span></td>
        <td><span data-ttu-id="0cfdc-221">ID de intervalo de chaves de partição de Olá para a leitura de dados.</span><span class="sxs-lookup"><span data-stu-id="0cfdc-221">hello partition key range ID for reading data.</span></span></td>
    </tr>
</table>

<span data-ttu-id="0cfdc-222">**Cabeçalhos de resposta para incremental ReadDocumentFeed**:</span><span class="sxs-lookup"><span data-stu-id="0cfdc-222">**Response headers for incremental ReadDocumentFeed**:</span></span>

<table> <tr>
        <th><span data-ttu-id="0cfdc-223">Nome do cabeçalho</span><span class="sxs-lookup"><span data-stu-id="0cfdc-223">Header name</span></span></th>
        <th><span data-ttu-id="0cfdc-224">Descrição</span><span class="sxs-lookup"><span data-stu-id="0cfdc-224">Description</span></span></th>
    </tr>
    <tr>
        <td><span data-ttu-id="0cfdc-225">ETag</span><span class="sxs-lookup"><span data-stu-id="0cfdc-225">etag</span></span></td>
        <td>
            <p><span data-ttu-id="0cfdc-226">Olá lógica número de sequência (LSN) da última documento devolvido na resposta Olá.</span><span class="sxs-lookup"><span data-stu-id="0cfdc-226">hello logical sequence number (LSN) of last document returned in hello response.</span></span></p>
            <p><span data-ttu-id="0cfdc-227">É possível retomar incremental ReadDocumentFeed ao voltar a submeter este valor na If-None-Match.</span><span class="sxs-lookup"><span data-stu-id="0cfdc-227">Incremental ReadDocumentFeed can be resumed by resubmitting this value in If-None-Match.</span></span></p>
        </td>
    </tr>
</table>

<span data-ttu-id="0cfdc-228">Eis um tooreturn de pedido de exemplo todas as alterações incrementais numa coleção de Olá lógica versão/ETag `28535` e o intervalo de chaves de partição = `16`:</span><span class="sxs-lookup"><span data-stu-id="0cfdc-228">Here's a sample request tooreturn all incremental changes in collection from hello logical version/ETag `28535` and partition key range = `16`:</span></span>

    GET https://mydocumentdb.documents.azure.com/dbs/bigdb/colls/bigcoll/docs HTTP/1.1
    x-ms-max-item-count: 1
    If-None-Match: "28535"
    A-IM: Incremental feed
    x-ms-documentdb-partitionkeyrangeid: 16
    x-ms-date: Tue, 22 Nov 2016 20:43:01 GMT
    authorization: type%3dmaster%26ver%3d1.0%26sig%3dzdpL2QQ8TCfiNbW%2fEcT88JHNvWeCgDA8gWeRZ%2btfN5o%3d
    x-ms-version: 2016-07-11
    Accept: application/json
    Host: mydocumentdb.documents.azure.com

<span data-ttu-id="0cfdc-229">As alterações são ordenadas por tempo dentro de cada valor de chave de partição dentro do intervalo de chave de partição de Olá.</span><span class="sxs-lookup"><span data-stu-id="0cfdc-229">Changes are ordered by time within each partition key value within hello partition key range.</span></span> <span data-ttu-id="0cfdc-230">Não há nenhuma ordem garantida entre os valores de chave de partição.</span><span class="sxs-lookup"><span data-stu-id="0cfdc-230">There is no guaranteed order across partition-key values.</span></span> <span data-ttu-id="0cfdc-231">Se não existirem resultados mais que o se podem ajustar numa única página, pode ler página seguinte do Olá de resultados ao voltar a submeter pedido Olá com Olá `If-None-Match` cabeçalho com o valor de toohello igual `etag` da resposta anterior Olá.</span><span class="sxs-lookup"><span data-stu-id="0cfdc-231">If there are more results than can fit in a single page, you can read hello next page of results by resubmitting hello request with hello `If-None-Match` header with value equal toohello `etag` from hello previous response.</span></span> <span data-ttu-id="0cfdc-232">Se vários documentos foram inseridos ou atualizados uma forma dentro de um procedimento armazenado ou acionador, serão todas devolvidos dentro Olá mesmo página de resposta.</span><span class="sxs-lookup"><span data-stu-id="0cfdc-232">If multiple documents were inserted or updated transactionally within a stored procedure or trigger, they will all be returned within hello same response page.</span></span>

> [!NOTE]
> <span data-ttu-id="0cfdc-233">Com o feed de alteração, poderá obter mais itens devolvidas uma página de início especificada no `x-ms-max-item-count` no caso de Olá de vários documentos inseridas ou atualizadas dentro de um procedimentos armazenados ou acionadores.</span><span class="sxs-lookup"><span data-stu-id="0cfdc-233">With change feed, you might get more items returned in a page than specified in `x-ms-max-item-count` in hello case of multiple documents inserted or updated inside a stored procedures or triggers.</span></span> 

<span data-ttu-id="0cfdc-234">Quando utilizar Olá SDK do .NET (1.17.0), defina o campo de Olá `StartTime` no `ChangeFeedOptions` documentos toodirectly retorno mudou desde `StartTime` ao chamar `CreateDocumentChangeFeedQuery`.</span><span class="sxs-lookup"><span data-stu-id="0cfdc-234">When using hello .NET SDK (1.17.0), set hello field `StartTime` in `ChangeFeedOptions` toodirectly return changed documents since `StartTime` when calling  `CreateDocumentChangeFeedQuery`.</span></span> <span data-ttu-id="0cfdc-235">Ao especificar `If-Modified-Since` utilizar Olá REST API, o pedido irá devolver não documentos de Olá próprios, mas em vez do token de continuação Olá ou `etag` no cabeçalho de resposta de Olá.</span><span class="sxs-lookup"><span data-stu-id="0cfdc-235">By specifying `If-Modified-Since` using hello REST API, your request will return not hello documents themselves, but rather hello continuation token or `etag` in hello response header.</span></span> <span data-ttu-id="0cfdc-236">documentos de Olá tooreturn Olá modificado especificado tempo, o token de continuação Olá `etag` , em seguida, devem ser utilizadas no próximo pedido de Olá com `If-None-Match` tooreturn Olá documentos reais.</span><span class="sxs-lookup"><span data-stu-id="0cfdc-236">tooreturn hello documents modified hello specified time, hello continuation token `etag` must then be used in hello next request with `If-None-Match` tooreturn hello actual documents.</span></span> 

<span data-ttu-id="0cfdc-237">Olá .NET SDK fornece Olá [CreateDocumentChangeFeedQuery](/dotnet/api/microsoft.azure.documents.client.documentclient.createdocumentchangefeedquery?view=azure-dotnet) e [ChangeFeedOptions](/dotnet/api/microsoft.azure.documents.client.changefeedoptions?view=azure-dotnet) classes de programa auxiliar tooaccess alterações tooa coleção.</span><span class="sxs-lookup"><span data-stu-id="0cfdc-237">hello .NET SDK provides hello [CreateDocumentChangeFeedQuery](/dotnet/api/microsoft.azure.documents.client.documentclient.createdocumentchangefeedquery?view=azure-dotnet) and [ChangeFeedOptions](/dotnet/api/microsoft.azure.documents.client.changefeedoptions?view=azure-dotnet) helper classes tooaccess changes made tooa collection.</span></span> <span data-ttu-id="0cfdc-238">Olá fragmento seguinte mostra como tooretrieve todas as alterações desde início Olá utilizando Olá .NET SDK a partir de um único cliente.</span><span class="sxs-lookup"><span data-stu-id="0cfdc-238">hello following snippet shows how tooretrieve all changes from hello beginning using hello .NET SDK from a single client.</span></span>

```csharp
private async Task<Dictionary<string, string>> GetChanges(
    DocumentClient client,
    string collection,
    Dictionary<string, string> checkpoints)
{
    string pkRangesResponseContinuation = null;
    List<PartitionKeyRange> partitionKeyRanges = new List<PartitionKeyRange>();

    do
    {
        FeedResponse<PartitionKeyRange> pkRangesResponse = await client.ReadPartitionKeyRangeFeedAsync(
            collectionUri, 
            new FeedOptions { RequestContinuation = pkRangesResponseContinuation });

        partitionKeyRanges.AddRange(pkRangesResponse);
        pkRangesResponseContinuation = pkRangesResponse.ResponseContinuation;
    }
    while (pkRangesResponseContinuation != null);

    foreach (PartitionKeyRange pkRange in partitionKeyRanges)
    {
        string continuation = null;
        checkpoints.TryGetValue(pkRange.Id, out continuation);

        IDocumentQuery<Document> query = client.CreateDocumentChangeFeedQuery(
            collection,
            new ChangeFeedOptions
            {
                PartitionKeyRangeId = pkRange.Id,
                StartFromBeginning = true,
                RequestContinuation = continuation,
                MaxItemCount = 1
            });

        while (query.HasMoreResults)
        {
            FeedResponse<DeviceReading> readChangesResponse = query.ExecuteNextAsync<DeviceReading>().Result;

            foreach (DeviceReading changedDocument in readChangesResponse)
            {
                Console.WriteLine(changedDocument.Id);
            }

            checkpoints[pkRange.Id] = readChangesResponse.ResponseContinuation;
        }
    }

    return checkpoints;
}
```
<span data-ttu-id="0cfdc-239">E hello fragmento seguinte mostra como tooprocess alterações em tempo real com base de dados do Azure Cosmos através da utilização de alteração de Olá feed suporte e Olá anterior a função.</span><span class="sxs-lookup"><span data-stu-id="0cfdc-239">And hello following snippet shows how tooprocess changes in real-time with Azure Cosmos DB by using hello change feed support and hello preceding function.</span></span> <span data-ttu-id="0cfdc-240">chamada primeiro Olá devolve todos os documentos de Olá na coleção de Olá e Olá segundo só devolve Olá dois documentos criados que foram criados desde o último ponto de verificação Olá.</span><span class="sxs-lookup"><span data-stu-id="0cfdc-240">hello first call returns all hello documents in hello collection, and hello second only returns hello two documents created that were created since hello last checkpoint.</span></span>

```csharp
// Returns all documents in hello collection.
Dictionary<string, string> checkpoints = await GetChanges(client, collection, new Dictionary<string, string>());

await client.CreateDocumentAsync(collection, new DeviceReading { DeviceId = "xsensr-201", MetricType = "Temperature", Unit = "Celsius", MetricValue = 1000 });
await client.CreateDocumentAsync(collection, new DeviceReading { DeviceId = "xsensr-212", MetricType = "Pressure", Unit = "psi", MetricValue = 1000 });

// Returns only hello two documents created above.
checkpoints = await GetChanges(client, collection, checkpoints);
```

<span data-ttu-id="0cfdc-241">Também pode filtrar o feed de alteração de Olá com eventos de processo de tooselectively de lógica do lado do cliente.</span><span class="sxs-lookup"><span data-stu-id="0cfdc-241">You can also filter hello change feed using client side logic tooselectively process events.</span></span> <span data-ttu-id="0cfdc-242">Por exemplo, eis um fragmento que utiliza o cliente lado LINQ tooprocess apenas eventos de alteração de temperatura de sensores de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="0cfdc-242">For example, here's a snippet that uses client side LINQ tooprocess only temperature change events from device sensors.</span></span>

```csharp
FeedResponse<DeviceReading> readChangesResponse = query.ExecuteNextAsync<DeviceReading>().Result;

foreach (DeviceReading changedDocument in 
    readChangesResponse.AsEnumerable().Where(d => d.MetricType == "Temperature" && d.MetricValue > 1000L))
{
    // trigger an action, like call an API
}
```

## <span data-ttu-id="0cfdc-243"><a id="change-feed-processor"></a>Biblioteca de processador de Feed de alteração</span><span class="sxs-lookup"><span data-stu-id="0cfdc-243"><a id="change-feed-processor"></a>Change Feed Processor library</span></span>
<span data-ttu-id="0cfdc-244">Outra opção consiste toouse Olá [biblioteca do Azure Cosmos DB alterar Feed processador](https://docs.microsoft.com/azure/cosmos-db/documentdb-sdk-dotnet-changefeed), que podem ajudar a distribuir facilmente o processamento de uma alteração do feed em vários consumidores de eventos.</span><span class="sxs-lookup"><span data-stu-id="0cfdc-244">Another option is toouse hello [Azure Cosmos DB Change Feed Processor library](https://docs.microsoft.com/azure/cosmos-db/documentdb-sdk-dotnet-changefeed), which can help you easily distribute event processing from a change feed across multiple consumers.</span></span> <span data-ttu-id="0cfdc-245">biblioteca de Olá é excelente para a criação de alteração feed leitores na plataforma de .NET Olá.</span><span class="sxs-lookup"><span data-stu-id="0cfdc-245">hello library is great for building change feed readers on hello .NET platform.</span></span> <span data-ttu-id="0cfdc-246">Alguns fluxos de trabalho que seriam simplificados, utilizando a biblioteca de processador de Feed de alteração de Olá através de métodos de Olá incluídos no Olá outros SDKs de BD do Cosmos incluem:</span><span class="sxs-lookup"><span data-stu-id="0cfdc-246">Some workflows that would be simplified by using hello Change Feed Processor library over hello methods included in hello other Cosmos DB SDKs include:</span></span> 

* <span data-ttu-id="0cfdc-247">Quando os dados são armazenados em várias partições de feed de solicitação de atualizações de alteração</span><span class="sxs-lookup"><span data-stu-id="0cfdc-247">Pulling updates from change feed when data is stored across multiple partitions</span></span>
* <span data-ttu-id="0cfdc-248">Mover ou replicar dados a partir de uma coleção tooanother</span><span class="sxs-lookup"><span data-stu-id="0cfdc-248">Moving or replicating data from one collection tooanother</span></span>
* <span data-ttu-id="0cfdc-249">Execução paralela de ações acionadas por atualizações toodata e alteração feed</span><span class="sxs-lookup"><span data-stu-id="0cfdc-249">Parallel execution of actions triggered by updates toodata and change feed</span></span> 

<span data-ttu-id="0cfdc-250">Enquanto a utilização de Olá APIs no Olá Cosmos SDKs fornece acesso preciso toochange feed atualizações em cada partição, utilizando a biblioteca de processador de Feed de alteração de Olá simplifica as alterações de leitura em partições e de vários threads funcionam em paralelo.</span><span class="sxs-lookup"><span data-stu-id="0cfdc-250">While using hello APIs in hello Cosmos SDKs provides precise access toochange feed updates in each partition, using hello Change Feed Processor library simplifies reading changes across partitions and multiple threads working in parallel.</span></span> <span data-ttu-id="0cfdc-251">Em vez de manualmente ao ler as alterações de cada contentor e guardar um token de continuação para cada partição, Olá alteração Feed processador gere automaticamente as alterações de leitura em partições utilizando um mecanismo de concessão.</span><span class="sxs-lookup"><span data-stu-id="0cfdc-251">Instead of manually reading changes from each container and saving a continuation token for each partition, hello Change Feed Processor automatically manages reading changes across partitions using a lease mechanism.</span></span>

<span data-ttu-id="0cfdc-252">biblioteca de Olá está disponível como um pacote NuGet: [Microsoft.Azure.Documents.ChangeFeedProcessor](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.ChangeFeedProcessor/) e a partir do código de origem como uma Github [exemplo](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/ChangeFeedProcessor).</span><span class="sxs-lookup"><span data-stu-id="0cfdc-252">hello library is available as a NuGet Package: [Microsoft.Azure.Documents.ChangeFeedProcessor](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.ChangeFeedProcessor/) and from source code as a Github [sample](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/ChangeFeedProcessor).</span></span> 

### <a name="understanding-change-feed-processor-library"></a><span data-ttu-id="0cfdc-253">Biblioteca de processador de Feed de alteração de compreender</span><span class="sxs-lookup"><span data-stu-id="0cfdc-253">Understanding Change Feed Processor library</span></span> 

<span data-ttu-id="0cfdc-254">Existem quatro componentes principais de implementação Olá processador de Feed de alteração: Olá monitorizado coleção, a recolha de concessão de Olá, anfitrião do processador Olá e consumidores de Olá.</span><span class="sxs-lookup"><span data-stu-id="0cfdc-254">There are four main components of implementing hello Change Feed Processor: hello monitored collection, hello lease collection, hello processor host, and hello consumers.</span></span> 

<span data-ttu-id="0cfdc-255">**Coleção de monitorizado:** Olá monitorizado coleção encontra-se dados Olá partir do qual Olá o feed de alteração é gerada.</span><span class="sxs-lookup"><span data-stu-id="0cfdc-255">**Monitored Collection:** hello monitored collection is hello data from which hello change feed is generated.</span></span> <span data-ttu-id="0cfdc-256">Uma coleção de toohello monitorizado inserções e as alterações são refletidas no feed de alteração de Olá da coleção de Olá.</span><span class="sxs-lookup"><span data-stu-id="0cfdc-256">Any inserts and changes toohello monitored collection are reflected in hello change feed of hello collection.</span></span> 

<span data-ttu-id="0cfdc-257">**Coleção de concessão:** Olá coordenadas de coleção de concessão processar a alteração de Olá feed entre vários workers.</span><span class="sxs-lookup"><span data-stu-id="0cfdc-257">**Lease Collection:** hello lease collection coordinates processing hello change feed across multiple workers.</span></span> <span data-ttu-id="0cfdc-258">Uma coleção separada é concessões de Olá toostore utilizada com uma concessão por partição.</span><span class="sxs-lookup"><span data-stu-id="0cfdc-258">A separate collection is used toostore hello leases with one lease per partition.</span></span> <span data-ttu-id="0cfdc-259">É vantajoso toostore esta coleção de concessão numa conta diferente com Olá escrever Olá região próximo toowhere está a executar o processador de Feed de alteração.</span><span class="sxs-lookup"><span data-stu-id="0cfdc-259">It is advantageous toostore this lease collection on a different account with hello write region closer toowhere hello Change Feed Processor is running.</span></span> <span data-ttu-id="0cfdc-260">Um objeto de concessão contém Olá seguintes atributos:</span><span class="sxs-lookup"><span data-stu-id="0cfdc-260">A lease object contains hello following attributes:</span></span> 
* <span data-ttu-id="0cfdc-261">Proprietário: Especifica o anfitrião de Olá que é proprietário de concessão de Olá</span><span class="sxs-lookup"><span data-stu-id="0cfdc-261">Owner: Specifies hello host that owns hello lease</span></span>
* <span data-ttu-id="0cfdc-262">Continuação: Especifica a posição de Olá (token de continuação) em alteração Olá feed para uma determinada partição</span><span class="sxs-lookup"><span data-stu-id="0cfdc-262">Continuation: Specifies hello position (continuation token) in hello change feed for a particular partition</span></span>
* <span data-ttu-id="0cfdc-263">Timestamp: Hora da última concessão foi atualizada; Olá timestamp pode ser utilizado toocheck se concessão Olá é considerado expirou</span><span class="sxs-lookup"><span data-stu-id="0cfdc-263">Timestamp: Last time lease was updated; hello timestamp can be used toocheck whether hello lease is considered expired</span></span> 

<span data-ttu-id="0cfdc-264">**Anfitrião do processador:** cada anfitrião determina quantos tooprocess de partições com base em quantos outras instâncias dos anfitriões têm concessões ativas são.</span><span class="sxs-lookup"><span data-stu-id="0cfdc-264">**Processor Host:** Each host determines how many partitions tooprocess based on how many other instances of hosts have active leases.</span></span> 
1.  <span data-ttu-id="0cfdc-265">Quando um anfitrião é iniciado, adquire carga de trabalho do concessões toobalance Olá em todos os anfitriões.</span><span class="sxs-lookup"><span data-stu-id="0cfdc-265">When a host starts up, it acquires leases toobalance hello workload across all hosts.</span></span> <span data-ttu-id="0cfdc-266">Um anfitrião periodicamente é renovada de concessões de, pelo que concessões permanecem ativos.</span><span class="sxs-lookup"><span data-stu-id="0cfdc-266">A host periodically renews leases, so leases remain active.</span></span> 
2.  <span data-ttu-id="0cfdc-267">Ler uma anfitrião pontos de verificação Olá último continuação token tooits concessão para cada.</span><span class="sxs-lookup"><span data-stu-id="0cfdc-267">A host checkpoints hello last continuation token tooits lease for each read.</span></span> <span data-ttu-id="0cfdc-268">segurança de concorrência tooensure, um anfitrião verifica Olá ETag para cada atualização de concessão.</span><span class="sxs-lookup"><span data-stu-id="0cfdc-268">tooensure concurrency safety, a host checks hello ETag for each lease update.</span></span> <span data-ttu-id="0cfdc-269">Também são suportadas outras estratégias de ponto de verificação.</span><span class="sxs-lookup"><span data-stu-id="0cfdc-269">Other checkpoint strategies are also supported.</span></span>  
3.  <span data-ttu-id="0cfdc-270">Após encerramento, um anfitrião versões concessões de todos os mas mantém Olá informações de continuação, para que possa retomar ler a partir do ponto de verificação armazenado hello mais tarde.</span><span class="sxs-lookup"><span data-stu-id="0cfdc-270">Upon shutdown, a host releases all leases but keeps hello continuation information, so it can resume reading from hello stored checkpoint later.</span></span> 

<span data-ttu-id="0cfdc-271">Neste momento, número de Olá de anfitriões não pode ser superior ao número de Olá de partições (concessões).</span><span class="sxs-lookup"><span data-stu-id="0cfdc-271">At this time hello number of hosts cannot be greater than hello number of partitions (leases).</span></span>

<span data-ttu-id="0cfdc-272">**Os consumidores:** consumidores ou técnicos, existem threads que efetuar a alteração de Olá feed processamento iniciado por cada anfitrião.</span><span class="sxs-lookup"><span data-stu-id="0cfdc-272">**Consumers:** Consumers, or workers, are threads that perform hello change feed processing initiated by each host.</span></span> <span data-ttu-id="0cfdc-273">Cada anfitrião do processador pode ter vários consumidores.</span><span class="sxs-lookup"><span data-stu-id="0cfdc-273">Each processor host can have multiple consumers.</span></span> <span data-ttu-id="0cfdc-274">Cada consumidor lê Olá alteração feed Olá partição está atribuído tooand notifica o respetivo anfitrião de alterações e expirado concessões.</span><span class="sxs-lookup"><span data-stu-id="0cfdc-274">Each consumer reads hello change feed from hello partition it is assigned tooand notifies its host of changes and expired leases.</span></span>

<span data-ttu-id="0cfdc-275">toofurther compreender como estes quatro elementos do processador de Feed de alteração de trabalham em conjunto, vamos ver um exemplo Olá diagrama a seguir.</span><span class="sxs-lookup"><span data-stu-id="0cfdc-275">toofurther understand how these four elements of Change Feed Processor work together, let's look at an example in hello following diagram.</span></span> <span data-ttu-id="0cfdc-276">Olá monitorizado documentos de arquivos de coleção e utiliza cidade"Olá" como chave de partição Olá.</span><span class="sxs-lookup"><span data-stu-id="0cfdc-276">hello monitored collection stores documents and uses hello "city" as hello partition key.</span></span> <span data-ttu-id="0cfdc-277">Vemos que a partição de Olá azul contém documentos com o campo de "Cidade" Olá da "A E" e assim sucessivamente.</span><span class="sxs-lookup"><span data-stu-id="0cfdc-277">We see that hello blue partition contains documents with hello "city" field from "A-E" and so on.</span></span> <span data-ttu-id="0cfdc-278">Existem dois anfitriões, cada um com dois os consumidores de ler a partir de partições de Olá quatro em paralelo.</span><span class="sxs-lookup"><span data-stu-id="0cfdc-278">There are two hosts, each with two consumers reading from hello four partitions in parallel.</span></span> <span data-ttu-id="0cfdc-279">Olá setas mostram o consumidores Olá ler a partir de um lugar para cima específico no Olá alterar feed.</span><span class="sxs-lookup"><span data-stu-id="0cfdc-279">hello arrows show hello consumers reading from a specific spot in hello change feed.</span></span> <span data-ttu-id="0cfdc-280">Na primeira partição Olá, azul darker Olá representa alterações unread enquanto blue leve Olá representa Olá já ler as alterações no feed de alteração de Olá.</span><span class="sxs-lookup"><span data-stu-id="0cfdc-280">In hello first partition, hello darker blue represents unread changes while hello light blue represents hello already read changes on hello change feed.</span></span> <span data-ttu-id="0cfdc-281">os anfitriões de Olá utilizam Olá concessão coleção toostore um registo de tookeep de valor de "continuação" da Olá atual de leitura de posição para cada consumidor.</span><span class="sxs-lookup"><span data-stu-id="0cfdc-281">hello hosts use hello lease collection toostore a "continuation" value tookeep track of hello current reading position for each consumer.</span></span> 

![Utilizar a alteração de base de dados do Azure Cosmos Olá feed anfitrião do processador](./media/change-feed/changefeedprocessornew.png)

### <a name="using-change-feed-processor-library"></a><span data-ttu-id="0cfdc-283">Utilizar a alteração de Feed de biblioteca de processador</span><span class="sxs-lookup"><span data-stu-id="0cfdc-283">Using Change Feed Processor Library</span></span> 
<span data-ttu-id="0cfdc-284">Olá seguinte secção explica como toouse Olá biblioteca de processador de Feed de alteração do contexto de Olá de replicar as alterações a partir de uma coleção de destino de tooa de coleção de origem.</span><span class="sxs-lookup"><span data-stu-id="0cfdc-284">hello following section explains how toouse hello Change Feed Processor library in hello context of replicating changes from a source collection tooa destination collection.</span></span> <span data-ttu-id="0cfdc-285">Aqui, a coleção de origem Olá é coleção Olá monitorizado no processador de Feed de alteração.</span><span class="sxs-lookup"><span data-stu-id="0cfdc-285">Here, hello source collection is hello monitored collection in Change Feed Processor.</span></span> 

<span data-ttu-id="0cfdc-286">**Instalar e incluir o pacote NuGet de processador de Feed de alteração de Olá**</span><span class="sxs-lookup"><span data-stu-id="0cfdc-286">**Install and include hello Change Feed Processor NuGet package**</span></span> 

<span data-ttu-id="0cfdc-287">Antes de instalar pacotes de NuGet processador de Feed de alteração, instale primeiro:</span><span class="sxs-lookup"><span data-stu-id="0cfdc-287">Before installing Change Feed Processor NuGet Package, first install:</span></span> 
* <span data-ttu-id="0cfdc-288">Microsoft.Azure.DocumentDB, versão 1.13.1 ou superior</span><span class="sxs-lookup"><span data-stu-id="0cfdc-288">Microsoft.Azure.DocumentDB, version 1.13.1 or above</span></span> 
* <span data-ttu-id="0cfdc-289">Newtonsoft, versão 9.0.1 ou acima instalação `Microsoft.Azure.DocumentDB.ChangeFeedProcessor` e incluí-la como uma referência.</span><span class="sxs-lookup"><span data-stu-id="0cfdc-289">Newtonsoft.Json, version 9.0.1 or above Install `Microsoft.Azure.DocumentDB.ChangeFeedProcessor` and include it as a reference.</span></span>

<span data-ttu-id="0cfdc-290">**Criar uma coleção de destino e de concessão monitorizada,**</span><span class="sxs-lookup"><span data-stu-id="0cfdc-290">**Create a monitored, lease and destination collection**</span></span> 

<span data-ttu-id="0cfdc-291">No toouse Olá da ordem biblioteca de processador de Feeds de alteração, Olá concessão necessita toobe criado antes de executar um ou mais anfitriões de processador de Olá.</span><span class="sxs-lookup"><span data-stu-id="0cfdc-291">In order toouse hello Change Feed Processor Library, hello lease collection needs toobe created before running hello processor host(s).</span></span> <span data-ttu-id="0cfdc-292">Novamente, recomendamos o armazenamento de uma coleção de concessão numa conta diferente com uma Olá escrita região próximo toowhere que está a executar o processador de Feed de alteração.</span><span class="sxs-lookup"><span data-stu-id="0cfdc-292">Again, we recommend storing a lease collection on a different account with a write region closer toowhere hello Change Feed Processor is running.</span></span> <span data-ttu-id="0cfdc-293">Neste exemplo de movimento de dados, precisamos de coleção de destino Olá toocreate antes de executar o anfitrião do processador de Feed de alteração de Olá.</span><span class="sxs-lookup"><span data-stu-id="0cfdc-293">In this data movement example, we need toocreate hello destination collection before running hello Change Feed Processor host.</span></span> <span data-ttu-id="0cfdc-294">No código de exemplo de Olá chamamos um Olá toocreate do método de programa auxiliar monitorizado, nos concessionados e coleções de destino, caso ainda não existam.</span><span class="sxs-lookup"><span data-stu-id="0cfdc-294">In hello sample code we call a helper method toocreate hello monitored, leased, and destination collections if they do not already exist.</span></span> 

> [!WARNING]
> <span data-ttu-id="0cfdc-295">Criar uma coleção tem implicações, de preços são reservar o débito para Olá toocommunicate de aplicação com a base de dados do Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="0cfdc-295">Creating a collection has pricing implications, as you are reserving throughput for hello application toocommunicate with Azure Cosmos DB.</span></span> <span data-ttu-id="0cfdc-296">Para obter mais detalhes, visite Olá [página de preços](https://azure.microsoft.com/pricing/details/cosmos-db/)</span><span class="sxs-lookup"><span data-stu-id="0cfdc-296">For more details, please visit hello [pricing page](https://azure.microsoft.com/pricing/details/cosmos-db/)</span></span>
> 
> 

<span data-ttu-id="0cfdc-297">*Criar um anfitrião do processador*</span><span class="sxs-lookup"><span data-stu-id="0cfdc-297">*Creating a processor host*</span></span>

<span data-ttu-id="0cfdc-298">Olá `ChangeFeedProcessorHost` classe fornece um ambiente de tempo de execução seguro para thread com vários processos, segura para as implementações do processador de eventos que também fornece a gestão de concessão de pontos de verificação e partição.</span><span class="sxs-lookup"><span data-stu-id="0cfdc-298">hello `ChangeFeedProcessorHost` class provides a thread-safe, multi-process, safe runtime environment for event processor implementations that also provides checkpointing and partition lease management.</span></span> <span data-ttu-id="0cfdc-299">Olá toouse `ChangeFeedProcessorHost` classe, pode implementar `IChangeFeedObserver`.</span><span class="sxs-lookup"><span data-stu-id="0cfdc-299">toouse hello `ChangeFeedProcessorHost` class, you can implement `IChangeFeedObserver`.</span></span> <span data-ttu-id="0cfdc-300">Esta interface contém três métodos:</span><span class="sxs-lookup"><span data-stu-id="0cfdc-300">This interface contains three methods:</span></span>

* <span data-ttu-id="0cfdc-301">`OpenAsync`: Esta função é chamada quando observador de feed de alteração é aberto.</span><span class="sxs-lookup"><span data-stu-id="0cfdc-301">`OpenAsync`: This function is called when change feed observer is opened.</span></span> <span data-ttu-id="0cfdc-302">Pode ser modificado tooperform uma ação específica quando consumidor/observador é aberto.</span><span class="sxs-lookup"><span data-stu-id="0cfdc-302">It can be modified tooperform a specific action when consumer/observer is opened.</span></span>  
* <span data-ttu-id="0cfdc-303">`CloseAsync`: Esta função é chamada quando observador de feed de alteração foi terminada.</span><span class="sxs-lookup"><span data-stu-id="0cfdc-303">`CloseAsync`: This function is called when change feed observer is terminated.</span></span> <span data-ttu-id="0cfdc-304">Pode ser modificado tooperform uma ação específica ao consumidor/observador está fechado.</span><span class="sxs-lookup"><span data-stu-id="0cfdc-304">It can be modified tooperform a specific action when consumer/observer is closed.</span></span>  
* <span data-ttu-id="0cfdc-305">`ProcessChangesAsync`: Esta função é chamada quando novas alterações de documento estão disponíveis no feed de alteração.</span><span class="sxs-lookup"><span data-stu-id="0cfdc-305">`ProcessChangesAsync`: This function is called when document new changes are available on change feed.</span></span> <span data-ttu-id="0cfdc-306">Pode ser modificado tooperform uma ação específica após todas as atualizações de alteração do feed.</span><span class="sxs-lookup"><span data-stu-id="0cfdc-306">It can be modified tooperform a specific action upon every change feed update.</span></span>  

<span data-ttu-id="0cfdc-307">No nosso exemplo, vamos implementa a interface de Olá `IChangeFeedObserver` através de Olá `DocumentFeedObserver` classe.</span><span class="sxs-lookup"><span data-stu-id="0cfdc-307">In our example, we implement hello interface `IChangeFeedObserver` through hello `DocumentFeedObserver` class.</span></span> <span data-ttu-id="0cfdc-308">Aqui, Olá `ProcessChangesAsync` upserts (atualizações) na coleção de destino Olá de feed de um documento de alteração de função.</span><span class="sxs-lookup"><span data-stu-id="0cfdc-308">Here, hello `ProcessChangesAsync` function upserts (updates) a document from change feed into hello destination collection.</span></span> <span data-ttu-id="0cfdc-309">Neste exemplo é útil para mover dados de uma coleção tooanother na ordem toochange Olá a chave de partição de um conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="0cfdc-309">This example is useful for moving data from one collection tooanother in order toochange hello partition key of a data set.</span></span> 

<span data-ttu-id="0cfdc-310">*Executar Olá anfitrião do processador*</span><span class="sxs-lookup"><span data-stu-id="0cfdc-310">*Running hello Processor Host*</span></span>

<span data-ttu-id="0cfdc-311">Antes de iniciar o processamento de eventos, ambos alterar opções de feed e opções de anfitrião de feed de alteração podem ser personalizadas.</span><span class="sxs-lookup"><span data-stu-id="0cfdc-311">Before beginning event processing, both change feed options and change feed host options can be customized.</span></span> 
```csharp
    // Customizable change feed option and host options 
    ChangeFeedOptions feedOptions = new ChangeFeedOptions();

    // ie customize StartFromBeginning so change feed reads from beginning
    // can customize MaxItemCount, PartitonKeyRangeId, RequestContinuation, SessionToken and StartFromBeginning
    feedOptions.StartFromBeginning = true;

    ChangeFeedHostOptions feedHostOptions = new ChangeFeedHostOptions();

    // ie. customizing lease renewal interval too15 seconds
    // can customize LeaseRenewInterval, LeaseAcquireInterval, LeaseExpirationInterval, FeedPollDelay 
    feedHostOptions.LeaseRenewInterval = TimeSpan.FromSeconds(15);

```
<span data-ttu-id="0cfdc-312">campos específicos Olá que podem ser personalizados estão resumidos na Olá tabelas a seguir.</span><span class="sxs-lookup"><span data-stu-id="0cfdc-312">hello specific fields that can be customized are summarized in hello following tables.</span></span> 

<span data-ttu-id="0cfdc-313">**Alterar as opções de Feed**:</span><span class="sxs-lookup"><span data-stu-id="0cfdc-313">**Change Feed Options**:</span></span>
<table>
    <tr>
        <th><span data-ttu-id="0cfdc-314">Nome da propriedade</span><span class="sxs-lookup"><span data-stu-id="0cfdc-314">Property Name</span></span></th>
        <th><span data-ttu-id="0cfdc-315">Descrição</span><span class="sxs-lookup"><span data-stu-id="0cfdc-315">Description</span></span></th>
    </tr>
    <tr>
        <td><span data-ttu-id="0cfdc-316">MaxItemCount</span><span class="sxs-lookup"><span data-stu-id="0cfdc-316">MaxItemCount</span></span></td>
        <td><span data-ttu-id="0cfdc-317">Obtém ou define o número máximo de Olá de toobe itens devolvido numa operação de enumeração de Olá no Olá serviço de base de dados de base de dados do Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="0cfdc-317">Gets or sets hello maximum number of items toobe returned in hello enumeration operation in hello Azure Cosmos DB database service.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="0cfdc-318">PartitionKeyRangeId</span><span class="sxs-lookup"><span data-stu-id="0cfdc-318">PartitionKeyRangeId</span></span></td>
        <td><span data-ttu-id="0cfdc-319">Obtém ou define o id de intervalo de chaves de partição Olá para o pedido atual Olá no serviço de base de dados de base de dados do Azure Cosmos Olá.</span><span class="sxs-lookup"><span data-stu-id="0cfdc-319">Gets or sets hello partition key range id for hello current request in hello Azure Cosmos DB database service.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="0cfdc-320">RequestContinuation</span><span class="sxs-lookup"><span data-stu-id="0cfdc-320">RequestContinuation</span></span></td>
        <td><span data-ttu-id="0cfdc-321">Obtém ou define o token de continuação de pedido de Olá no serviço de base de dados de base de dados do Azure Cosmos Olá.</span><span class="sxs-lookup"><span data-stu-id="0cfdc-321">Gets or sets hello request continuation token in hello Azure Cosmos DB database service.</span></span></td>
    </tr>
        <tr>
        <td><span data-ttu-id="0cfdc-322">SessionToken</span><span class="sxs-lookup"><span data-stu-id="0cfdc-322">SessionToken</span></span></td>
        <td><span data-ttu-id="0cfdc-323">Obtém ou define o token da sessão Olá para utilização com consistência de sessão no Olá serviço de base de dados de base de dados do Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="0cfdc-323">Gets or sets hello session token for use with session consistency in hello Azure Cosmos DB database service.</span></span></td>
    </tr>
        <tr>
        <td><span data-ttu-id="0cfdc-324">StartFromBeginning</span><span class="sxs-lookup"><span data-stu-id="0cfdc-324">StartFromBeginning</span></span></td>
        <td><span data-ttu-id="0cfdc-325">Obtém ou define se deve iniciar a alteração do feed no serviço de base de dados de base de dados do Azure Cosmos Olá Olá a partir da (true) ou a atual (false).</span><span class="sxs-lookup"><span data-stu-id="0cfdc-325">Gets or sets whether change feed in hello Azure Cosmos DB database service should start from hello beginning (true) or from current (false).</span></span> <span data-ttu-id="0cfdc-326">Por predefinição, este inicia a partir do atual (false).</span><span class="sxs-lookup"><span data-stu-id="0cfdc-326">By default, it starts from current (false).</span></span></td>
    </tr>
</table>

<span data-ttu-id="0cfdc-327">**Alterar as opções de anfitrião Feed**:</span><span class="sxs-lookup"><span data-stu-id="0cfdc-327">**Change Feed Host Options**:</span></span>
<table>
    <tr>
        <th><span data-ttu-id="0cfdc-328">Nome da propriedade</span><span class="sxs-lookup"><span data-stu-id="0cfdc-328">Property Name</span></span></th>
        <th><span data-ttu-id="0cfdc-329">Tipo</span><span class="sxs-lookup"><span data-stu-id="0cfdc-329">Type</span></span></th>
        <th><span data-ttu-id="0cfdc-330">Descrição</span><span class="sxs-lookup"><span data-stu-id="0cfdc-330">Description</span></span></th>
    </tr>
    <tr>
        <td><span data-ttu-id="0cfdc-331">LeaseRenewInterval</span><span class="sxs-lookup"><span data-stu-id="0cfdc-331">LeaseRenewInterval</span></span></td>
        <td><span data-ttu-id="0cfdc-332">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="0cfdc-332">TimeSpan</span></span></td>
        <td><span data-ttu-id="0cfdc-333">intervalo de Olá para todas as concessões para partições atualmente retido por instância de ChangeFeedEventHost Olá.</span><span class="sxs-lookup"><span data-stu-id="0cfdc-333">hello interval for all leases for partitions currently held by hello ChangeFeedEventHost instance.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="0cfdc-334">LeaseAcquireInterval</span><span class="sxs-lookup"><span data-stu-id="0cfdc-334">LeaseAcquireInterval</span></span></td>
        <td><span data-ttu-id="0cfdc-335">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="0cfdc-335">TimeSpan</span></span></td>
        <td><span data-ttu-id="0cfdc-336">Olá intervalo tookick desativar uma tarefa toocompute se as partições são distribuídas uniformemente entre instâncias de anfitrião conhecido.</span><span class="sxs-lookup"><span data-stu-id="0cfdc-336">hello interval tookick off a task toocompute whether partitions are distributed evenly among known host instances.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="0cfdc-337">LeaseExpirationInterval</span><span class="sxs-lookup"><span data-stu-id="0cfdc-337">LeaseExpirationInterval</span></span></td>
        <td><span data-ttu-id="0cfdc-338">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="0cfdc-338">TimeSpan</span></span></td>
        <td><span data-ttu-id="0cfdc-339">intervalo de Olá para que Olá concessão é criada numa concessão que representa uma partição.</span><span class="sxs-lookup"><span data-stu-id="0cfdc-339">hello interval for which hello lease is taken on a lease representing a partition.</span></span> <span data-ttu-id="0cfdc-340">Se a concessão de Olá não for renovado dentro deste intervalo, expirar e a propriedade da partição Olá move tooanother ChangeFeedEventHost instância.</span><span class="sxs-lookup"><span data-stu-id="0cfdc-340">If hello lease is not renewed within this interval, it is expired and ownership of hello partition moves tooanother ChangeFeedEventHost instance.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="0cfdc-341">FeedPollDelay</span><span class="sxs-lookup"><span data-stu-id="0cfdc-341">FeedPollDelay</span></span></td>
        <td><span data-ttu-id="0cfdc-342">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="0cfdc-342">TimeSpan</span></span></td>
        <td><span data-ttu-id="0cfdc-343">atraso de Olá entre consulta uma partição para novas alterações no Olá feed, depois de todas as alterações atuais são drained.</span><span class="sxs-lookup"><span data-stu-id="0cfdc-343">hello delay between polling a partition for new changes on hello feed, after all current changes are drained.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="0cfdc-344">CheckpointFrequency</span><span class="sxs-lookup"><span data-stu-id="0cfdc-344">CheckpointFrequency</span></span></td>
        <td><span data-ttu-id="0cfdc-345">CheckpointFrequency</span><span class="sxs-lookup"><span data-stu-id="0cfdc-345">CheckpointFrequency</span></span></td>
        <td><span data-ttu-id="0cfdc-346">Olá concessões de toocheckpoint frequência.</span><span class="sxs-lookup"><span data-stu-id="0cfdc-346">hello frequency toocheckpoint leases.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="0cfdc-347">MinPartitionCount</span><span class="sxs-lookup"><span data-stu-id="0cfdc-347">MinPartitionCount</span></span></td>
        <td><span data-ttu-id="0cfdc-348">Int</span><span class="sxs-lookup"><span data-stu-id="0cfdc-348">Int</span></span></td>
        <td><span data-ttu-id="0cfdc-349">Olá mínimo partições para o anfitrião de Olá.</span><span class="sxs-lookup"><span data-stu-id="0cfdc-349">hello minimum partition count for hello host.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="0cfdc-350">MaxPartitionCount</span><span class="sxs-lookup"><span data-stu-id="0cfdc-350">MaxPartitionCount</span></span></td>
        <td><span data-ttu-id="0cfdc-351">Int</span><span class="sxs-lookup"><span data-stu-id="0cfdc-351">Int</span></span></td>
        <td><span data-ttu-id="0cfdc-352">pode servir o número máximo de Olá de anfitrião de Olá partições.</span><span class="sxs-lookup"><span data-stu-id="0cfdc-352">hello maximum number of partitions hello host can serve.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="0cfdc-353">DiscardExistingLeases</span><span class="sxs-lookup"><span data-stu-id="0cfdc-353">DiscardExistingLeases</span></span></td>
        <td><span data-ttu-id="0cfdc-354">bool</span><span class="sxs-lookup"><span data-stu-id="0cfdc-354">Bool</span></span></td>
        <td><span data-ttu-id="0cfdc-355">Se no Olá início do anfitrião Olá todas as concessões existentes deve ser eliminado e anfitrião Olá deve começar do zero.</span><span class="sxs-lookup"><span data-stu-id="0cfdc-355">Whether on hello start of hello host all existing leases should be deleted and hello host should start from scratch.</span></span></td>
    </tr>
</table>


<span data-ttu-id="0cfdc-356">processamento de eventos de toostart instanciar `ChangeFeedProcessorHost`, fornecendo os parâmetros adequados Olá para a coleção de BD do Cosmos do Azure.</span><span class="sxs-lookup"><span data-stu-id="0cfdc-356">toostart event processing, instantiate `ChangeFeedProcessorHost`, providing hello appropriate parameters for your Azure Cosmos DB collection.</span></span> <span data-ttu-id="0cfdc-357">Em seguida, chame `RegisterObserverAsync` tooregister sua `IChangeFeedObserver` implementação (DocumentFeedObserver neste exemplo) com Olá tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="0cfdc-357">Then, call `RegisterObserverAsync` tooregister your `IChangeFeedObserver` (DocumentFeedObserver in this example) implementation with hello runtime.</span></span> <span data-ttu-id="0cfdc-358">Neste momento, o anfitrião de Olá tenta tooacquire uma concessão em cada intervalo de chaves de partição na coleção de base de dados do Azure Cosmos Olá utilizando um algoritmo "abrangente".</span><span class="sxs-lookup"><span data-stu-id="0cfdc-358">At this point, hello host attempts tooacquire a lease on every partition key range in hello Azure Cosmos DB collection using a "greedy" algorithm.</span></span> <span data-ttu-id="0cfdc-359">Estas concessões última para um determinado período de tempo e, em seguida, tem de ser renovados.</span><span class="sxs-lookup"><span data-stu-id="0cfdc-359">These leases last for a given timeframe and must then be renewed.</span></span> <span data-ttu-id="0cfdc-360">Como novos nós, instâncias de trabalho, neste caso, fique online, colocam reservas de concessões e ao longo do tempo carga Olá desvia entre nós, cada anfitrião tenta tooacquire mais concessões.</span><span class="sxs-lookup"><span data-stu-id="0cfdc-360">As new nodes, worker instances, in this case, come online, they place lease reservations and over time hello load shifts between nodes as each host attempts tooacquire more leases.</span></span> 

<span data-ttu-id="0cfdc-361">Código de exemplo de Olá, utilizamos uma toocreate de classe (DocumentFeedObserverFactory.cs) fábrica um observador e Olá `RegistObserverFactoryAsync` observador de Olá tooregister.</span><span class="sxs-lookup"><span data-stu-id="0cfdc-361">In hello sample code, we use a factory class (DocumentFeedObserverFactory.cs) toocreate an observer and hello `RegistObserverFactoryAsync` tooregister hello observer.</span></span> 

```csharp
using (DocumentClient destClient = new DocumentClient(destCollInfo.Uri, destCollInfo.MasterKey))
    {
        DocumentFeedObserverFactory docObserverFactory = new DocumentFeedObserverFactory(destClient, destCollInfo);
        ChangeFeedEventHost host = new ChangeFeedEventHost(hostName, documentCollectionLocation, leaseCollectionLocation, feedOptions, feedHostOptions);

        await host.RegisterObserverFactoryAsync(docObserverFactory);

        Console.WriteLine("Running... Press enter toostop.");
        Console.ReadLine();

        await host.UnregisterObserversAsync();
    }
```
<span data-ttu-id="0cfdc-362">Ao longo do tempo, é estabelecido um equilíbrio.</span><span class="sxs-lookup"><span data-stu-id="0cfdc-362">Over time, an equilibrium is established.</span></span> <span data-ttu-id="0cfdc-363">Esta capacidade dinâmica permite baseado em CPU dimensionamento automático tooconsumers de toobe aplicada para ambos aumentar verticalmente e horizontalmente.</span><span class="sxs-lookup"><span data-stu-id="0cfdc-363">This dynamic capability enables CPU-based auto-scaling toobe applied tooconsumers for both scale-up and scale-down.</span></span> <span data-ttu-id="0cfdc-364">Se as alterações disponíveis do BD Azure Cosmos rapidamente do que os consumidores podem processar, Olá aumento de CPU nos consumidores pode ser utilizado toocause um dimensionamento automático na contagem de instâncias de trabalho.</span><span class="sxs-lookup"><span data-stu-id="0cfdc-364">If changes are available in Azure Cosmos DB at a faster rate than consumers can process, hello CPU increase on consumers can be used toocause an auto-scale on worker instance count.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0cfdc-365">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="0cfdc-365">Next steps</span></span>
* <span data-ttu-id="0cfdc-366">Tente Olá [Azure Cosmos DB altere feed exemplos de código no GitHub](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/code-samples/ChangeFeed)</span><span class="sxs-lookup"><span data-stu-id="0cfdc-366">Try hello [Azure Cosmos DB Change feed code samples on GitHub](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/code-samples/ChangeFeed)</span></span>
* <span data-ttu-id="0cfdc-367">Introdução à programação com Olá [SDKs de BD do Azure Cosmos](documentdb-sdk-dotnet.md) ou Olá [REST API](/rest/api/documentdb/).</span><span class="sxs-lookup"><span data-stu-id="0cfdc-367">Get started coding with hello [Azure Cosmos DB SDKs](documentdb-sdk-dotnet.md) or hello [REST API](/rest/api/documentdb/).</span></span>
