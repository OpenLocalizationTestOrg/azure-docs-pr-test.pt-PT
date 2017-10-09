---
title: 'Azure Cosmos DB: API de Java do DocumentDB, SDK & recursos | Microsoft Docs'
description: "Saiba tudo sobre Olá Java API e SDK, incluindo as datas de versão, datas de extinção e as alterações efetuadas entre cada versão do Olá SDK de Java DocumentDB do Azure Cosmos DB."
services: cosmos-db
documentationcenter: java
author: rnagpal
manager: jhubbard
editor: cgronlun
ms.assetid: 7861cadf-2a05-471a-9925-0fec0599351b
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: article
ms.date: 07/11/2017
ms.author: khdang
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 8ef43ebeb7ae1bfc55512c4a7489c1b7930122d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-documentdb-java-sdk-release-notes-and-resources"></a><span data-ttu-id="3f0ce-103">Azure Cosmos DB: SDK de DocumentDB Java notas de versão e recursos</span><span class="sxs-lookup"><span data-stu-id="3f0ce-103">Azure Cosmos DB: DocumentDB Java SDK release notes and resources</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="3f0ce-104">.NET</span><span class="sxs-lookup"><span data-stu-id="3f0ce-104">.NET</span></span>](documentdb-sdk-dotnet.md)
> * [<span data-ttu-id="3f0ce-105">Feed de alteração de .NET</span><span class="sxs-lookup"><span data-stu-id="3f0ce-105">.NET Change Feed</span></span>](documentdb-sdk-dotnet-changefeed.md)
> * [<span data-ttu-id="3f0ce-106">.NET Core</span><span class="sxs-lookup"><span data-stu-id="3f0ce-106">.NET Core</span></span>](documentdb-sdk-dotnet-core.md)
> * [<span data-ttu-id="3f0ce-107">Node.js</span><span class="sxs-lookup"><span data-stu-id="3f0ce-107">Node.js</span></span>](documentdb-sdk-node.md)
> * [<span data-ttu-id="3f0ce-108">Java</span><span class="sxs-lookup"><span data-stu-id="3f0ce-108">Java</span></span>](documentdb-sdk-java.md)
> * [<span data-ttu-id="3f0ce-109">Python</span><span class="sxs-lookup"><span data-stu-id="3f0ce-109">Python</span></span>](documentdb-sdk-python.md)
> * [<span data-ttu-id="3f0ce-110">REST</span><span class="sxs-lookup"><span data-stu-id="3f0ce-110">REST</span></span>](https://docs.microsoft.com/rest/api/documentdb/)
> * [<span data-ttu-id="3f0ce-111">Fornecedor de Recursos REST</span><span class="sxs-lookup"><span data-stu-id="3f0ce-111">REST Resource Provider</span></span>](https://docs.microsoft.com/rest/api/documentdbresourceprovider/)
> * [<span data-ttu-id="3f0ce-112">SQL</span><span class="sxs-lookup"><span data-stu-id="3f0ce-112">SQL</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx)
> 
> 

<table>

<tr><td><span data-ttu-id="3f0ce-113">**Transferência do SDK**</span><span class="sxs-lookup"><span data-stu-id="3f0ce-113">**SDK Download**</span></span></td><td>[<span data-ttu-id="3f0ce-114">Maven</span><span class="sxs-lookup"><span data-stu-id="3f0ce-114">Maven</span></span>](http://search.maven.org/#search%7Cgav%7C1%7Cg%3A%22com.microsoft.azure%22%20AND%20a%3A%22azure-documentdb%22)</td></tr>

<tr><td><span data-ttu-id="3f0ce-115">**Documentação da API**</span><span class="sxs-lookup"><span data-stu-id="3f0ce-115">**API documentation**</span></span></td><td>[<span data-ttu-id="3f0ce-116">Documentação de referência da API de Java</span><span class="sxs-lookup"><span data-stu-id="3f0ce-116">Java API reference documentation</span></span>](/java/api/com.microsoft.azure.documentdb)</td></tr>

<tr><td><span data-ttu-id="3f0ce-117">**Contribuir tooSDK**</span><span class="sxs-lookup"><span data-stu-id="3f0ce-117">**Contribute tooSDK**</span></span></td><td>[<span data-ttu-id="3f0ce-118">GitHub</span><span class="sxs-lookup"><span data-stu-id="3f0ce-118">GitHub</span></span>](https://github.com/Azure/azure-documentdb-java/)</td></tr>

<tr><td><span data-ttu-id="3f0ce-119">**Introdução**</span><span class="sxs-lookup"><span data-stu-id="3f0ce-119">**Get started**</span></span></td><td>[<span data-ttu-id="3f0ce-120">Introdução ao hello Java SDK</span><span class="sxs-lookup"><span data-stu-id="3f0ce-120">Get started with hello Java SDK</span></span>](documentdb-java-get-started.md)</td></tr>

<tr><td><span data-ttu-id="3f0ce-121">**Tutorial de aplicação Web**</span><span class="sxs-lookup"><span data-stu-id="3f0ce-121">**Web app tutorial**</span></span></td><td>[<span data-ttu-id="3f0ce-122">Desenvolvimento da aplicação Web com base de dados do Azure Cosmos</span><span class="sxs-lookup"><span data-stu-id="3f0ce-122">Web application development with Azure Cosmos DB</span></span>](documentdb-java-application.md)</td></tr>

<tr><td><span data-ttu-id="3f0ce-123">**Tempo de execução suportado atual**</span><span class="sxs-lookup"><span data-stu-id="3f0ce-123">**Current supported runtime**</span></span></td><td>[<span data-ttu-id="3f0ce-124">JDK 7</span><span class="sxs-lookup"><span data-stu-id="3f0ce-124">JDK 7</span></span>](http://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html)</td></tr>
</table></br>

## <a name="release-notes"></a><span data-ttu-id="3f0ce-125">Notas de Versão</span><span class="sxs-lookup"><span data-stu-id="3f0ce-125">Release Notes</span></span>

### <a name="a-name11201120"></a><span data-ttu-id="3f0ce-126"><a name="1.12.0"/>1.12.0</span><span class="sxs-lookup"><span data-stu-id="3f0ce-126"><a name="1.12.0"/>1.12.0</span></span>
* <span data-ttu-id="3f0ce-127">Divide toorequest críticos correções de erros durante a partição de processamento.</span><span class="sxs-lookup"><span data-stu-id="3f0ce-127">Critical bug fixes toorequest processing during partition splits.</span></span>
* <span data-ttu-id="3f0ce-128">Foi corrigido um problema com Olá forte e BoundedStaleness níveis de consistência.</span><span class="sxs-lookup"><span data-stu-id="3f0ce-128">Fixed an issue with hello Strong and BoundedStaleness consistency levels.</span></span>

### <a name="a-name11101110"></a><span data-ttu-id="3f0ce-129"><a name="1.11.0"/>1.11.0</span><span class="sxs-lookup"><span data-stu-id="3f0ce-129"><a name="1.11.0"/>1.11.0</span></span>
* <span data-ttu-id="3f0ce-130">Suporte adicionado para um novo nível de consistência chamado ConsistentPrefix.</span><span class="sxs-lookup"><span data-stu-id="3f0ce-130">Added support for a new consistency level called ConsistentPrefix.</span></span>
* <span data-ttu-id="3f0ce-131">Corrigido um erro ao ler a coleção no modo de sessão.</span><span class="sxs-lookup"><span data-stu-id="3f0ce-131">Fixed a bug in reading collection in session mode.</span></span>

### <a name="a-name11001100"></a><span data-ttu-id="3f0ce-132"><a name="1.10.0"/>1.10.0</span><span class="sxs-lookup"><span data-stu-id="3f0ce-132"><a name="1.10.0"/>1.10.0</span></span>
* <span data-ttu-id="3f0ce-133">Suporte ativado para uma coleção particionada com como baixa como 2500 RU/seg e dimensionar em incrementos de 100 RU/seg.</span><span class="sxs-lookup"><span data-stu-id="3f0ce-133">Enabled support for partitioned collection with as low as 2,500 RU/sec and scale in increments of 100 RU/sec.</span></span>
* <span data-ttu-id="3f0ce-134">Corrigido um erro na assemblagem de nativa Olá que pode originar a exceção de NullRef em algumas consultas.</span><span class="sxs-lookup"><span data-stu-id="3f0ce-134">Fixed a bug in hello native assembly which can cause NullRef exception in some queries.</span></span>

### <a name="a-name196196"></a><span data-ttu-id="3f0ce-135"><a name="1.9.6"/>1.9.6</span><span class="sxs-lookup"><span data-stu-id="3f0ce-135"><a name="1.9.6"/>1.9.6</span></span>
* <span data-ttu-id="3f0ce-136">Corrigido um erro na configuração do motor de consulta Olá que pode fazer com que as exceções para consultas no modo de Gateway.</span><span class="sxs-lookup"><span data-stu-id="3f0ce-136">Fixed a bug in hello query engine configuration that may cause exceptions for queries in Gateway mode.</span></span>
* <span data-ttu-id="3f0ce-137">Corrigido alguns erros no contentor de sessão de Olá que podem causar uma exceção de "Recurso de proprietário não encontrada" para pedidos imediatamente após a criação de coleção.</span><span class="sxs-lookup"><span data-stu-id="3f0ce-137">Fixed a few bugs in hello session container that may cause an "Owner resource not found" exception for requests immediately after collection creation.</span></span>

### <a name="a-name195195"></a><span data-ttu-id="3f0ce-138"><a name="1.9.5"/>1.9.5</span><span class="sxs-lookup"><span data-stu-id="3f0ce-138"><a name="1.9.5"/>1.9.5</span></span>
* <span data-ttu-id="3f0ce-139">Suporte adicionado para consultas de agregação (CONTAGEM, MIN, MAX, soma e média).</span><span class="sxs-lookup"><span data-stu-id="3f0ce-139">Added support for aggregation queries (COUNT, MIN, MAX, SUM, and AVG).</span></span> <span data-ttu-id="3f0ce-140">Consulte [suporte de agregação](documentdb-sql-query.md#Aggregates).</span><span class="sxs-lookup"><span data-stu-id="3f0ce-140">See [Aggregation support](documentdb-sql-query.md#Aggregates).</span></span>
* <span data-ttu-id="3f0ce-141">Suporte adicionado para alteração do feed.</span><span class="sxs-lookup"><span data-stu-id="3f0ce-141">Added support for change feed.</span></span>
* <span data-ttu-id="3f0ce-142">Suporte adicionado para informações sobre a quota coleção através de RequestOptions.setPopulateQuotaInfo.</span><span class="sxs-lookup"><span data-stu-id="3f0ce-142">Added support for collection quota information through RequestOptions.setPopulateQuotaInfo.</span></span>
* <span data-ttu-id="3f0ce-143">Adicionado suporte para registo de script do procedimento armazenado através de RequestOptions.setScriptLoggingEnabled.</span><span class="sxs-lookup"><span data-stu-id="3f0ce-143">Added support for stored procedure script logging through RequestOptions.setScriptLoggingEnabled.</span></span>
* <span data-ttu-id="3f0ce-144">Corrigido um erro onde a consulta no modo de DirectHttps poderá bloquear quando encontra falhas de limitação.</span><span class="sxs-lookup"><span data-stu-id="3f0ce-144">Fixed a bug where query in DirectHttps mode may hang when encountering throttle failures.</span></span>
* <span data-ttu-id="3f0ce-145">Corrigido um erro no modo de consistência de sessão.</span><span class="sxs-lookup"><span data-stu-id="3f0ce-145">Fixed a bug in session consistency mode.</span></span>
* <span data-ttu-id="3f0ce-146">Corrigido um erro que poderá provocar NullReferenceException HttpContext quando a taxa de pedidos é elevada.</span><span class="sxs-lookup"><span data-stu-id="3f0ce-146">Fixed a bug which may cause NullReferenceException in HttpContext when request rate is high.</span></span>
* <span data-ttu-id="3f0ce-147">Melhoria do desempenho do modo de DirectHttps.</span><span class="sxs-lookup"><span data-stu-id="3f0ce-147">Improved performance of DirectHttps mode.</span></span>

### <a name="a-name194194"></a><span data-ttu-id="3f0ce-148"><a name="1.9.4"/>1.9.4</span><span class="sxs-lookup"><span data-stu-id="3f0ce-148"><a name="1.9.4"/>1.9.4</span></span>
* <span data-ttu-id="3f0ce-149">Suporte de proxy baseado na instância de cliente simples adicionado ConnectionPolicy.setProxy() API.</span><span class="sxs-lookup"><span data-stu-id="3f0ce-149">Added simple client instance-based proxy support with ConnectionPolicy.setProxy() API.</span></span>
* <span data-ttu-id="3f0ce-150">Foram adicionada DocumentClient.close() API tooproperly encerrado DocumentClient instância.</span><span class="sxs-lookup"><span data-stu-id="3f0ce-150">Added DocumentClient.close() API tooproperly shutdown DocumentClient instance.</span></span>
* <span data-ttu-id="3f0ce-151">Desempenho das consultas melhorada no modo de ligação direta ao efetuar a derivação de plano de consulta Olá de assemblagem nativo do Olá em vez de Olá Gateway.</span><span class="sxs-lookup"><span data-stu-id="3f0ce-151">Improved query performance in direct connectivity mode by deriving hello query plan from hello native assembly instead of hello Gateway.</span></span>
* <span data-ttu-id="3f0ce-152">Definir FAIL_ON_UNKNOWN_PROPERTIES = false para que os utilizadores não precisam de toodefine JsonIgnoreProperties no respetivo POJO.</span><span class="sxs-lookup"><span data-stu-id="3f0ce-152">Set FAIL_ON_UNKNOWN_PROPERTIES = false so users don't need toodefine JsonIgnoreProperties in their POJO.</span></span>
* <span data-ttu-id="3f0ce-153">Registo refatorizado toouse SLF4J.</span><span class="sxs-lookup"><span data-stu-id="3f0ce-153">Refactored logging toouse SLF4J.</span></span>
* <span data-ttu-id="3f0ce-154">Corrigidos alguns outros erros no leitor de consistência.</span><span class="sxs-lookup"><span data-stu-id="3f0ce-154">Fixed a few other bugs in consistency reader.</span></span>

### <a name="a-name193193"></a><span data-ttu-id="3f0ce-155"><a name="1.9.3"/>1.9.3</span><span class="sxs-lookup"><span data-stu-id="3f0ce-155"><a name="1.9.3"/>1.9.3</span></span>
* <span data-ttu-id="3f0ce-156">Corrigido um erro na ligação Gestão tooprevent ligação fugas de Olá no modo de ligação direta.</span><span class="sxs-lookup"><span data-stu-id="3f0ce-156">Fixed a bug in hello connection management tooprevent connection leaks in direct connectivity mode.</span></span>
* <span data-ttu-id="3f0ce-157">Corrigido um erro na consulta superior olá onde pode acionar NullReferenece exceção.</span><span class="sxs-lookup"><span data-stu-id="3f0ce-157">Fixed a bug in hello TOP query where it may throw NullReferenece exception.</span></span>
* <span data-ttu-id="3f0ce-158">Melhoria do desempenho ao reduzir o número de Olá de chamada de rede para caches internas Olá.</span><span class="sxs-lookup"><span data-stu-id="3f0ce-158">Improved performance by reducing hello number of network call for hello internal caches.</span></span>
* <span data-ttu-id="3f0ce-159">Código de estado adicionado, ActivityID e URI de pedido no DocumentClientException para melhor de resolução de problemas.</span><span class="sxs-lookup"><span data-stu-id="3f0ce-159">Added status code, ActivityID and Request URI in DocumentClientException for better troubleshooting.</span></span>

### <a name="a-name192192"></a><span data-ttu-id="3f0ce-160"><a name="1.9.2"/>1.9.2</span><span class="sxs-lookup"><span data-stu-id="3f0ce-160"><a name="1.9.2"/>1.9.2</span></span>
* <span data-ttu-id="3f0ce-161">Foi corrigido um problema na gestão de ligações de Olá para estabilidade.</span><span class="sxs-lookup"><span data-stu-id="3f0ce-161">Fixed an issue in hello connection management for stability.</span></span>

### <a name="a-name191191"></a><span data-ttu-id="3f0ce-162"><a name="1.9.1"/>1.9.1</span><span class="sxs-lookup"><span data-stu-id="3f0ce-162"><a name="1.9.1"/>1.9.1</span></span>
* <span data-ttu-id="3f0ce-163">Suporte adicionado para BoundedStaleness nível de consistência.</span><span class="sxs-lookup"><span data-stu-id="3f0ce-163">Added support for BoundedStaleness consistency level.</span></span>
* <span data-ttu-id="3f0ce-164">Suporte adicionado para ligação direta para as operações CRUD para coleções particionadas.</span><span class="sxs-lookup"><span data-stu-id="3f0ce-164">Added support for direct connectivity for CRUD operations for partitioned collections.</span></span>
* <span data-ttu-id="3f0ce-165">Corrigido um erro no consultar uma base de dados com o SQL Server.</span><span class="sxs-lookup"><span data-stu-id="3f0ce-165">Fixed a bug in querying a database with SQL.</span></span>
* <span data-ttu-id="3f0ce-166">Corrigido um erro na cache de sessão de olá onde o token da sessão pode ser definida incorretamente.</span><span class="sxs-lookup"><span data-stu-id="3f0ce-166">Fixed a bug in hello session cache where session token may be set incorrectly.</span></span>

### <a name="a-name190190"></a><span data-ttu-id="3f0ce-167"><a name="1.9.0"/>1.9.0</span><span class="sxs-lookup"><span data-stu-id="3f0ce-167"><a name="1.9.0"/>1.9.0</span></span>
* <span data-ttu-id="3f0ce-168">Suporte adicionado para entre consultas paralelas de partição.</span><span class="sxs-lookup"><span data-stu-id="3f0ce-168">Added support for cross partition parallel queries.</span></span>
* <span data-ttu-id="3f0ce-169">Suporte adicionado para consultas de parte superior/ORDER BY para coleções particionadas.</span><span class="sxs-lookup"><span data-stu-id="3f0ce-169">Added support for TOP/ORDER BY queries for partitioned collections.</span></span>
* <span data-ttu-id="3f0ce-170">Adicionado suporte para a consistência forte.</span><span class="sxs-lookup"><span data-stu-id="3f0ce-170">Added support for strong consistency.</span></span>
* <span data-ttu-id="3f0ce-171">Suporte adicionado para pedidos de nomes com base em quando utilizar a ligação direta.</span><span class="sxs-lookup"><span data-stu-id="3f0ce-171">Added support for name based requests when using direct connectivity.</span></span>
* <span data-ttu-id="3f0ce-172">Toomake fixo ActivityId permanecem consistentes em todas as tentativas de pedido.</span><span class="sxs-lookup"><span data-stu-id="3f0ce-172">Fixed toomake ActivityId stay consistent across all request retries.</span></span>
* <span data-ttu-id="3f0ce-173">Corrigido um erro relacionado com a cache da sessão toohello quando recriar uma coleção com Olá mesmo nome.</span><span class="sxs-lookup"><span data-stu-id="3f0ce-173">Fixed a bug related toohello session cache when recreating a collection with hello same name.</span></span>
* <span data-ttu-id="3f0ce-174">Foram adicionadas polígono e tipos de dados de LineString ao especificar a coleção de indexação de política para consultas geográficos barreiras geográficas.</span><span class="sxs-lookup"><span data-stu-id="3f0ce-174">Added Polygon and LineString DataTypes while specifying collection indexing policy for geo-fencing spatial queries.</span></span>
* <span data-ttu-id="3f0ce-175">Fixos problemas com a documentação do Java para 1.8 do Java.</span><span class="sxs-lookup"><span data-stu-id="3f0ce-175">Fixed issues with Java Doc for Java 1.8.</span></span>

### <a name="a-name181181"></a><span data-ttu-id="3f0ce-176"><a name="1.8.1"/>1.8.1</span><span class="sxs-lookup"><span data-stu-id="3f0ce-176"><a name="1.8.1"/>1.8.1</span></span>
* <span data-ttu-id="3f0ce-177">Corrigido um erro no PartitionKeyDefinitionMap coleções de partições únicas toocache e não disponibilizar extra obter partição pedidos de chave.</span><span class="sxs-lookup"><span data-stu-id="3f0ce-177">Fixed a bug in PartitionKeyDefinitionMap toocache single partition collections and not make extra fetch partition key requests.</span></span>
* <span data-ttu-id="3f0ce-178">Corrigido uma repetição de toonot erros quando é fornecido um valor de chave de partição incorreto.</span><span class="sxs-lookup"><span data-stu-id="3f0ce-178">Fixed a bug toonot retry when an incorrect partition key value is provided.</span></span>

### <a name="a-name180180"></a><span data-ttu-id="3f0ce-179"><a name="1.8.0"/>1.8.0</span><span class="sxs-lookup"><span data-stu-id="3f0ce-179"><a name="1.8.0"/>1.8.0</span></span>
* <span data-ttu-id="3f0ce-180">Suporte adicionado Olá para contas de multirregião base de dados.</span><span class="sxs-lookup"><span data-stu-id="3f0ce-180">Added hello support for multi-region database accounts.</span></span>
* <span data-ttu-id="3f0ce-181">Suporte adicionado para repetição automática em pedidos otimizadas com Olá de toocustomize opções máximo tentativas de repetição e repita máx tempo de espera.</span><span class="sxs-lookup"><span data-stu-id="3f0ce-181">Added support for automatic retry on throttled requests with options toocustomize hello max retry attempts and max retry wait time.</span></span>  <span data-ttu-id="3f0ce-182">Ver RetryOptions e ConnectionPolicy.getRetryOptions().</span><span class="sxs-lookup"><span data-stu-id="3f0ce-182">See RetryOptions and ConnectionPolicy.getRetryOptions().</span></span>
* <span data-ttu-id="3f0ce-183">IPartitionResolver preterido com a base de código personalizado de criação de partições.</span><span class="sxs-lookup"><span data-stu-id="3f0ce-183">Deprecated IPartitionResolver based custom partitioning code.</span></span> <span data-ttu-id="3f0ce-184">Utilize coleções particionadas para superior armazenamento e débito.</span><span class="sxs-lookup"><span data-stu-id="3f0ce-184">Please use partitioned collections for higher storage and throughput.</span></span>

### <a name="a-name171171"></a><span data-ttu-id="3f0ce-185"><a name="1.7.1"/>1.7.1</span><span class="sxs-lookup"><span data-stu-id="3f0ce-185"><a name="1.7.1"/>1.7.1</span></span>
* <span data-ttu-id="3f0ce-186">Suporte de política de repetição adicionado para limitação.</span><span class="sxs-lookup"><span data-stu-id="3f0ce-186">Added retry policy support for throttling.</span></span>  

### <a name="a-name170170"></a><span data-ttu-id="3f0ce-187"><a name="1.7.0"/>1.7.0</span><span class="sxs-lookup"><span data-stu-id="3f0ce-187"><a name="1.7.0"/>1.7.0</span></span>
* <span data-ttu-id="3f0ce-188">Tempo toolive (TTL) suporte adicionado para documentos.</span><span class="sxs-lookup"><span data-stu-id="3f0ce-188">Added time toolive (TTL) support for documents.</span></span>

### <a name="a-name160160"></a><span data-ttu-id="3f0ce-189"><a name="1.6.0"/>1.6.0</span><span class="sxs-lookup"><span data-stu-id="3f0ce-189"><a name="1.6.0"/>1.6.0</span></span>
* <span data-ttu-id="3f0ce-190">Implementado [particionada coleções](partition-data.md) e [níveis de desempenho definido pelo utilizador](performance-levels.md).</span><span class="sxs-lookup"><span data-stu-id="3f0ce-190">Implemented [partitioned collections](partition-data.md) and [user-defined performance levels](performance-levels.md).</span></span>

### <a name="a-name151151"></a><span data-ttu-id="3f0ce-191"><a name="1.5.1"/>1.5.1</span><span class="sxs-lookup"><span data-stu-id="3f0ce-191"><a name="1.5.1"/>1.5.1</span></span>
* <span data-ttu-id="3f0ce-192">Corrigido um erro no HashPartitionResolver toogenerate os valores de hash no toobe little endian consistente com outros SDKs.</span><span class="sxs-lookup"><span data-stu-id="3f0ce-192">Fixed a bug in HashPartitionResolver toogenerate hash values in little-endian toobe consistent with other SDKs.</span></span>

### <a name="a-name150150"></a><span data-ttu-id="3f0ce-193"><a name="1.5.0"/>1.5.0</span><span class="sxs-lookup"><span data-stu-id="3f0ce-193"><a name="1.5.0"/>1.5.0</span></span>
* <span data-ttu-id="3f0ce-194">Adicionar Hash & intervalo de partição resoluções tooassist com as aplicações de fragmentação através de várias partições.</span><span class="sxs-lookup"><span data-stu-id="3f0ce-194">Add Hash & Range partition resolvers tooassist with sharding applications across multiple partitions.</span></span>

### <a name="a-name140140"></a><span data-ttu-id="3f0ce-195"><a name="1.4.0"/>1.4.0</span><span class="sxs-lookup"><span data-stu-id="3f0ce-195"><a name="1.4.0"/>1.4.0</span></span>
* <span data-ttu-id="3f0ce-196">Implemente Upsert.</span><span class="sxs-lookup"><span data-stu-id="3f0ce-196">Implement Upsert.</span></span> <span data-ttu-id="3f0ce-197">Novos métodos de upsertXXX adicionado toosupport Upsert funcionalidade.</span><span class="sxs-lookup"><span data-stu-id="3f0ce-197">New upsertXXX methods added toosupport Upsert feature.</span></span>
* <span data-ttu-id="3f0ce-198">ID de implementar baseado Routing.</span><span class="sxs-lookup"><span data-stu-id="3f0ce-198">Implement ID Based Routing.</span></span> <span data-ttu-id="3f0ce-199">Sem alterações de API públicas, todas as alterações internas.</span><span class="sxs-lookup"><span data-stu-id="3f0ce-199">No public API changes, all changes internal.</span></span>

### <a name="a-name130130"></a><span data-ttu-id="3f0ce-200"><a name="1.3.0"/>1.3.0</span><span class="sxs-lookup"><span data-stu-id="3f0ce-200"><a name="1.3.0"/>1.3.0</span></span>
* <span data-ttu-id="3f0ce-201">Versão ignorada toobring o número de versão em alinhamento com outros SDKs</span><span class="sxs-lookup"><span data-stu-id="3f0ce-201">Release skipped toobring version number in alignment with other SDKs</span></span>

### <a name="a-name120120"></a><span data-ttu-id="3f0ce-202"><a name="1.2.0"/>1.2.0</span><span class="sxs-lookup"><span data-stu-id="3f0ce-202"><a name="1.2.0"/>1.2.0</span></span>
* <span data-ttu-id="3f0ce-203">Suporta Geoespacial índice</span><span class="sxs-lookup"><span data-stu-id="3f0ce-203">Supports GeoSpatial Index</span></span>
* <span data-ttu-id="3f0ce-204">Valida a propriedade id de todos os recursos.</span><span class="sxs-lookup"><span data-stu-id="3f0ce-204">Validates id property for all resources.</span></span> <span data-ttu-id="3f0ce-205">Os IDs de recursos não podem conter?, /, #, \, carateres nem terminar com um espaço.</span><span class="sxs-lookup"><span data-stu-id="3f0ce-205">Ids for resources cannot contain ?, /, #, \, characters or end with a space.</span></span>
* <span data-ttu-id="3f0ce-206">Adiciona tooResourceResponse de "progresso de transformação de índice" do novo cabeçalho.</span><span class="sxs-lookup"><span data-stu-id="3f0ce-206">Adds new header "index transformation progress" tooResourceResponse.</span></span>

### <a name="a-name110110"></a><span data-ttu-id="3f0ce-207"><a name="1.1.0"/>1.1.0</span><span class="sxs-lookup"><span data-stu-id="3f0ce-207"><a name="1.1.0"/>1.1.0</span></span>
* <span data-ttu-id="3f0ce-208">Implementa a política de indexação V2</span><span class="sxs-lookup"><span data-stu-id="3f0ce-208">Implements V2 indexing policy</span></span>

### <a name="a-name100100"></a><span data-ttu-id="3f0ce-209"><a name="1.0.0"/>1.0.0</span><span class="sxs-lookup"><span data-stu-id="3f0ce-209"><a name="1.0.0"/>1.0.0</span></span>
* <span data-ttu-id="3f0ce-210">GA SDK</span><span class="sxs-lookup"><span data-stu-id="3f0ce-210">GA SDK</span></span>

## <a name="release--retirement-dates"></a><span data-ttu-id="3f0ce-211">Datas de extinção & versão</span><span class="sxs-lookup"><span data-stu-id="3f0ce-211">Release & Retirement Dates</span></span>
<span data-ttu-id="3f0ce-212">A Microsoft vai fornecer pelo menos notificação **12 meses** previamente extinguir um SDK na ordem toosmooth Olá transição tooa/suportada mais recente versão.</span><span class="sxs-lookup"><span data-stu-id="3f0ce-212">Microsoft will provide notification at least **12 months** in advance of retiring an SDK in order toosmooth hello transition tooa newer/supported version.</span></span>

<span data-ttu-id="3f0ce-213">Apenas são adicionadas novas funcionalidades e a funcionalidade e otimizações o atual toohello SDK, como tal, é recomendado que lhe toohello sempre atualização mais recente versão do SDK antecipadamente quanto possível.</span><span class="sxs-lookup"><span data-stu-id="3f0ce-213">New features and functionality and optimizations are only added toohello current SDK, as such it is  recommend that you always upgrade toohello latest SDK version as early as possible.</span></span>

<span data-ttu-id="3f0ce-214">Qualquer tooCosmos pedido BD utilizando um SDK extinto serão rejeitadas pelo serviço de Olá.</span><span class="sxs-lookup"><span data-stu-id="3f0ce-214">Any request tooCosmos DB using a retired SDK will be rejected by hello service.</span></span>

> [!WARNING]
> <span data-ttu-id="3f0ce-215">Todas as versões do Olá DocumentDB SDK para tooversion anterior Java **1.0.0** serão descontinuados no **29 de Fevereiro de 2016**.</span><span class="sxs-lookup"><span data-stu-id="3f0ce-215">All versions of hello DocumentDB SDK for Java prior tooversion **1.0.0** will be retired on **February 29, 2016**.</span></span>
> 
> 

<br/>

| <span data-ttu-id="3f0ce-216">Versão</span><span class="sxs-lookup"><span data-stu-id="3f0ce-216">Version</span></span> | <span data-ttu-id="3f0ce-217">Data da versão</span><span class="sxs-lookup"><span data-stu-id="3f0ce-217">Release Date</span></span> | <span data-ttu-id="3f0ce-218">Data de retirada</span><span class="sxs-lookup"><span data-stu-id="3f0ce-218">Retirement Date</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="3f0ce-219">1.12.0</span><span class="sxs-lookup"><span data-stu-id="3f0ce-219">1.12.0</span></span>](#1.12.0) |<span data-ttu-id="3f0ce-220">11 de Julho de 2017</span><span class="sxs-lookup"><span data-stu-id="3f0ce-220">July 11, 2017</span></span> |--- |
| [<span data-ttu-id="3f0ce-221">1.11.0</span><span class="sxs-lookup"><span data-stu-id="3f0ce-221">1.11.0</span></span>](#1.11.0) |<span data-ttu-id="3f0ce-222">10 de maio de 2017</span><span class="sxs-lookup"><span data-stu-id="3f0ce-222">May 10, 2017</span></span> |--- |
| [<span data-ttu-id="3f0ce-223">1.10.0</span><span class="sxs-lookup"><span data-stu-id="3f0ce-223">1.10.0</span></span>](#1.10.0) |<span data-ttu-id="3f0ce-224">11 de Março de 2017</span><span class="sxs-lookup"><span data-stu-id="3f0ce-224">March 11, 2017</span></span> |--- |
| [<span data-ttu-id="3f0ce-225">1.9.6</span><span class="sxs-lookup"><span data-stu-id="3f0ce-225">1.9.6</span></span>](#1.9.6) |<span data-ttu-id="3f0ce-226">21 de Fevereiro de 2017</span><span class="sxs-lookup"><span data-stu-id="3f0ce-226">February 21, 2017</span></span> |--- |
| [<span data-ttu-id="3f0ce-227">1.9.5</span><span class="sxs-lookup"><span data-stu-id="3f0ce-227">1.9.5</span></span>](#1.9.5) |<span data-ttu-id="3f0ce-228">31 de Janeiro de 2017</span><span class="sxs-lookup"><span data-stu-id="3f0ce-228">January 31, 2017</span></span> |--- |
| [<span data-ttu-id="3f0ce-229">1.9.4</span><span class="sxs-lookup"><span data-stu-id="3f0ce-229">1.9.4</span></span>](#1.9.4) |<span data-ttu-id="3f0ce-230">24 de Novembro de 2016</span><span class="sxs-lookup"><span data-stu-id="3f0ce-230">November 24, 2016</span></span> |--- |
| [<span data-ttu-id="3f0ce-231">1.9.3</span><span class="sxs-lookup"><span data-stu-id="3f0ce-231">1.9.3</span></span>](#1.9.3) |<span data-ttu-id="3f0ce-232">30 de Outubro de 2016</span><span class="sxs-lookup"><span data-stu-id="3f0ce-232">October 30, 2016</span></span> |--- |
| [<span data-ttu-id="3f0ce-233">1.9.2</span><span class="sxs-lookup"><span data-stu-id="3f0ce-233">1.9.2</span></span>](#1.9.2) |<span data-ttu-id="3f0ce-234">28 de Outubro de 2016</span><span class="sxs-lookup"><span data-stu-id="3f0ce-234">October 28, 2016</span></span> |--- |
| [<span data-ttu-id="3f0ce-235">1.9.1</span><span class="sxs-lookup"><span data-stu-id="3f0ce-235">1.9.1</span></span>](#1.9.1) |<span data-ttu-id="3f0ce-236">26 de Outubro de 2016</span><span class="sxs-lookup"><span data-stu-id="3f0ce-236">October 26, 2016</span></span> |--- |
| [<span data-ttu-id="3f0ce-237">1.9.0</span><span class="sxs-lookup"><span data-stu-id="3f0ce-237">1.9.0</span></span>](#1.9.0) |<span data-ttu-id="3f0ce-238">03 de Outubro de 2016</span><span class="sxs-lookup"><span data-stu-id="3f0ce-238">October 03, 2016</span></span> |--- |
| [<span data-ttu-id="3f0ce-239">1.8.1</span><span class="sxs-lookup"><span data-stu-id="3f0ce-239">1.8.1</span></span>](#1.8.1) |<span data-ttu-id="3f0ce-240">30 de Junho de 2016</span><span class="sxs-lookup"><span data-stu-id="3f0ce-240">June 30, 2016</span></span> |--- |
| [<span data-ttu-id="3f0ce-241">1.8.0</span><span class="sxs-lookup"><span data-stu-id="3f0ce-241">1.8.0</span></span>](#1.8.0) |<span data-ttu-id="3f0ce-242">14 de Junho de 2016</span><span class="sxs-lookup"><span data-stu-id="3f0ce-242">June 14, 2016</span></span> |--- |
| [<span data-ttu-id="3f0ce-243">1.7.1</span><span class="sxs-lookup"><span data-stu-id="3f0ce-243">1.7.1</span></span>](#1.7.1) |<span data-ttu-id="3f0ce-244">30 de Abril de 2016</span><span class="sxs-lookup"><span data-stu-id="3f0ce-244">April 30, 2016</span></span> |--- |
| [<span data-ttu-id="3f0ce-245">1.7.0</span><span class="sxs-lookup"><span data-stu-id="3f0ce-245">1.7.0</span></span>](#1.7.0) |<span data-ttu-id="3f0ce-246">27 de Abril de 2016</span><span class="sxs-lookup"><span data-stu-id="3f0ce-246">April 27, 2016</span></span> |--- |
| [<span data-ttu-id="3f0ce-247">1.6.0</span><span class="sxs-lookup"><span data-stu-id="3f0ce-247">1.6.0</span></span>](#1.6.0) |<span data-ttu-id="3f0ce-248">29 de Março de 2016</span><span class="sxs-lookup"><span data-stu-id="3f0ce-248">March 29, 2016</span></span> |--- |
| [<span data-ttu-id="3f0ce-249">1.5.1</span><span class="sxs-lookup"><span data-stu-id="3f0ce-249">1.5.1</span></span>](#1.5.1) |<span data-ttu-id="3f0ce-250">31 de Dezembro de 2015</span><span class="sxs-lookup"><span data-stu-id="3f0ce-250">December 31, 2015</span></span> |--- |
| [<span data-ttu-id="3f0ce-251">1.5.0</span><span class="sxs-lookup"><span data-stu-id="3f0ce-251">1.5.0</span></span>](#1.5.0) |<span data-ttu-id="3f0ce-252">04 de Dezembro de 2015</span><span class="sxs-lookup"><span data-stu-id="3f0ce-252">December 04, 2015</span></span> |--- |
| [<span data-ttu-id="3f0ce-253">1.4.0</span><span class="sxs-lookup"><span data-stu-id="3f0ce-253">1.4.0</span></span>](#1.4.0) |<span data-ttu-id="3f0ce-254">05 de Outubro de 2015</span><span class="sxs-lookup"><span data-stu-id="3f0ce-254">October 05, 2015</span></span> |--- |
| [<span data-ttu-id="3f0ce-255">1.3.0</span><span class="sxs-lookup"><span data-stu-id="3f0ce-255">1.3.0</span></span>](#1.3.0) |<span data-ttu-id="3f0ce-256">05 de Outubro de 2015</span><span class="sxs-lookup"><span data-stu-id="3f0ce-256">October 05, 2015</span></span> |--- |
| [<span data-ttu-id="3f0ce-257">1.2.0</span><span class="sxs-lookup"><span data-stu-id="3f0ce-257">1.2.0</span></span>](#1.2.0) |<span data-ttu-id="3f0ce-258">05 de Agosto de 2015</span><span class="sxs-lookup"><span data-stu-id="3f0ce-258">August 05, 2015</span></span> |--- |
| [<span data-ttu-id="3f0ce-259">1.1.0</span><span class="sxs-lookup"><span data-stu-id="3f0ce-259">1.1.0</span></span>](#1.1.0) |<span data-ttu-id="3f0ce-260">09 de Julho de 2015</span><span class="sxs-lookup"><span data-stu-id="3f0ce-260">July 09, 2015</span></span> |--- |
| [<span data-ttu-id="3f0ce-261">1.0.1</span><span class="sxs-lookup"><span data-stu-id="3f0ce-261">1.0.1</span></span>](#1.0.1) |<span data-ttu-id="3f0ce-262">12 de Maio de 2015</span><span class="sxs-lookup"><span data-stu-id="3f0ce-262">May 12, 2015</span></span> |--- |
| [<span data-ttu-id="3f0ce-263">1.0.0</span><span class="sxs-lookup"><span data-stu-id="3f0ce-263">1.0.0</span></span>](#1.0.0) |<span data-ttu-id="3f0ce-264">07 de Abril de 2015</span><span class="sxs-lookup"><span data-stu-id="3f0ce-264">April 07, 2015</span></span> |--- |
| <span data-ttu-id="3f0ce-265">0.9.5-prelease</span><span class="sxs-lookup"><span data-stu-id="3f0ce-265">0.9.5-prelease</span></span> |<span data-ttu-id="3f0ce-266">09 de mar de 2015</span><span class="sxs-lookup"><span data-stu-id="3f0ce-266">Mar 09, 2015</span></span> |<span data-ttu-id="3f0ce-267">29 de Fevereiro de 2016</span><span class="sxs-lookup"><span data-stu-id="3f0ce-267">February 29, 2016</span></span> |
| <span data-ttu-id="3f0ce-268">0.9.4-prelease</span><span class="sxs-lookup"><span data-stu-id="3f0ce-268">0.9.4-prelease</span></span> |<span data-ttu-id="3f0ce-269">17 de Fevereiro de 2015</span><span class="sxs-lookup"><span data-stu-id="3f0ce-269">February 17, 2015</span></span> |<span data-ttu-id="3f0ce-270">29 de Fevereiro de 2016</span><span class="sxs-lookup"><span data-stu-id="3f0ce-270">February 29, 2016</span></span> |
| <span data-ttu-id="3f0ce-271">0.9.3-prelease</span><span class="sxs-lookup"><span data-stu-id="3f0ce-271">0.9.3-prelease</span></span> |<span data-ttu-id="3f0ce-272">13 de Janeiro de 2015</span><span class="sxs-lookup"><span data-stu-id="3f0ce-272">January 13, 2015</span></span> |<span data-ttu-id="3f0ce-273">29 de Fevereiro de 2016</span><span class="sxs-lookup"><span data-stu-id="3f0ce-273">February 29, 2016</span></span> |
| <span data-ttu-id="3f0ce-274">0.9.2-prelease</span><span class="sxs-lookup"><span data-stu-id="3f0ce-274">0.9.2-prelease</span></span> |<span data-ttu-id="3f0ce-275">19 de Dezembro de 2014</span><span class="sxs-lookup"><span data-stu-id="3f0ce-275">December 19, 2014</span></span> |<span data-ttu-id="3f0ce-276">29 de Fevereiro de 2016</span><span class="sxs-lookup"><span data-stu-id="3f0ce-276">February 29, 2016</span></span> |
| <span data-ttu-id="3f0ce-277">0.9.1-prelease</span><span class="sxs-lookup"><span data-stu-id="3f0ce-277">0.9.1-prelease</span></span> |<span data-ttu-id="3f0ce-278">19 de Dezembro de 2014</span><span class="sxs-lookup"><span data-stu-id="3f0ce-278">December 19, 2014</span></span> |<span data-ttu-id="3f0ce-279">29 de Fevereiro de 2016</span><span class="sxs-lookup"><span data-stu-id="3f0ce-279">February 29, 2016</span></span> |
| <span data-ttu-id="3f0ce-280">0.9.0-prelease</span><span class="sxs-lookup"><span data-stu-id="3f0ce-280">0.9.0-prelease</span></span> |<span data-ttu-id="3f0ce-281">10 de Dezembro de 2014</span><span class="sxs-lookup"><span data-stu-id="3f0ce-281">December 10, 2014</span></span> |<span data-ttu-id="3f0ce-282">29 de Fevereiro de 2016</span><span class="sxs-lookup"><span data-stu-id="3f0ce-282">February 29, 2016</span></span> |

## <a name="faq"></a><span data-ttu-id="3f0ce-283">FAQ</span><span class="sxs-lookup"><span data-stu-id="3f0ce-283">FAQ</span></span>
[!INCLUDE [cosmos-db-sdk-faq](../../includes/cosmos-db-sdk-faq.md)]

## <a name="see-also"></a><span data-ttu-id="3f0ce-284">Veja Também</span><span class="sxs-lookup"><span data-stu-id="3f0ce-284">See Also</span></span>
<span data-ttu-id="3f0ce-285">toolearn mais informações sobre a base de dados do Cosmos, consulte [base de dados do Microsoft Azure Cosmos](https://azure.microsoft.com/services/cosmos-db/) página do serviço.</span><span class="sxs-lookup"><span data-stu-id="3f0ce-285">toolearn more about Cosmos DB, see [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) service page.</span></span>

