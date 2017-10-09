---
title: aaaAzure Cosmos DB dimensionamento e o teste de desempenho | Microsoft Docs
description: Saiba como dimensionar tooperform e teste de desempenho com base de dados do Azure Cosmos
keywords: Teste de desempenho
services: cosmos-db
author: arramac
manager: jhubbard
editor: 
documentationcenter: 
ms.assetid: f4c96ebd-f53c-427d-a500-3f28fe7b11d0
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: arramac
ms.openlocfilehash: 46d1217e11a39ee970a868de9a5c5dfcf52cedf3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="performance-and-scale-testing-with-azure-cosmos-db"></a><span data-ttu-id="70178-104">Desempenho e dimensionamento de teste com base de dados do Azure Cosmos</span><span class="sxs-lookup"><span data-stu-id="70178-104">Performance and scale testing with Azure Cosmos DB</span></span>
<span data-ttu-id="70178-105">Desempenho e dimensionamento de teste é um passo chave no desenvolvimento de aplicações.</span><span class="sxs-lookup"><span data-stu-id="70178-105">Performance and scale testing is a key step in application development.</span></span> <span data-ttu-id="70178-106">Para muitas aplicações, o escalão de base de dados de Olá tem um impacto significativo Olá escalabilidade e desempenho global e está, por conseguinte, um componente crítico de desempenho de teste.</span><span class="sxs-lookup"><span data-stu-id="70178-106">For many applications, hello database tier has a significant impact on hello overall performance and scalability, and is therefore a critical component of performance testing.</span></span> <span data-ttu-id="70178-107">[BD do Azure do Cosmos](https://azure.microsoft.com/services/cosmos-db/) é específico para a escala elástica e um desempenho previsível e, por conseguinte, uma excelente opção para aplicações que necessitam de uma camada de base de dados de elevado desempenho.</span><span class="sxs-lookup"><span data-stu-id="70178-107">[Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) is purpose-built for elastic scale and predictable performance, and therefore a great fit for applications that need a high-performance database tier.</span></span> 

<span data-ttu-id="70178-108">Este artigo é uma referência para programadores implementar conjuntos de teste de desempenho para as respetivas cargas de trabalho de BD do Cosmos ou avaliar Cosmos DB para cenários de aplicações de elevado desempenho.</span><span class="sxs-lookup"><span data-stu-id="70178-108">This article is a reference for developers implementing performance test suites for their Cosmos DB workloads, or evaluating Cosmos DB for high-performance application scenarios.</span></span> <span data-ttu-id="70178-109">Concentra-se principalmente nas teste isolado de desempenho da base de dados de Olá, mas também inclui as melhores práticas para aplicações de produção.</span><span class="sxs-lookup"><span data-stu-id="70178-109">It focuses primarily on isolated performance testing of hello database, but also includes best practices for production applications.</span></span>

<span data-ttu-id="70178-110">Depois de ler este artigo, irá ser Olá tooanswer capaz de seguintes perguntas:</span><span class="sxs-lookup"><span data-stu-id="70178-110">After reading this article, you will be able tooanswer hello following questions:</span></span>   

* <span data-ttu-id="70178-111">Onde posso encontrar um exemplo de aplicação de cliente .NET para o teste de desempenho da base de dados do Cosmos?</span><span class="sxs-lookup"><span data-stu-id="70178-111">Where can I find a sample .NET client application for performance testing of Cosmos DB?</span></span> 
* <span data-ttu-id="70178-112">Como alcançar níveis de débito elevado com Cosmos DB a minha aplicação de cliente?</span><span class="sxs-lookup"><span data-stu-id="70178-112">How do I achieve high throughput levels with Cosmos DB from my client application?</span></span>

<span data-ttu-id="70178-113">tooget iniciado com o código,. Transfira o projeto de Olá de [amostra de testes de desempenho do Azure Cosmos DB](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/documentdb-benchmark).</span><span class="sxs-lookup"><span data-stu-id="70178-113">tooget started with code, please download hello project from [Azure Cosmos DB Performance Testing Sample](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/documentdb-benchmark).</span></span> 

> [!NOTE]
> <span data-ttu-id="70178-114">objetivo Olá esta aplicação é toodemonstrate melhores práticas para extrair um melhor desempenho fora do Cosmos DB com um pequeno número de computadores cliente.</span><span class="sxs-lookup"><span data-stu-id="70178-114">hello goal of this application is toodemonstrate best practices for extracting better performance out of Cosmos DB with a small number of client machines.</span></span> <span data-ttu-id="70178-115">Este não foi efetuada uma capacidade de pico de Olá toodemonstrate do serviço de Olá, o que pode dimensionar ilimitada.</span><span class="sxs-lookup"><span data-stu-id="70178-115">This was not made toodemonstrate hello peak capacity of hello service, which can scale limitlessly.</span></span>
> 
> 

<span data-ttu-id="70178-116">Se estiver à procura de opções de configuração do lado do cliente tooimprove desempenho de base de dados do Cosmos, consulte o artigo [sugestões de desempenho de base de dados do Azure Cosmos](performance-tips.md).</span><span class="sxs-lookup"><span data-stu-id="70178-116">If you're looking for client-side configuration options tooimprove Cosmos DB performance, see [Azure Cosmos DB performance tips](performance-tips.md).</span></span>

## <a name="run-hello-performance-testing-application"></a><span data-ttu-id="70178-117">Executar a aplicação de testes de desempenho de Olá</span><span class="sxs-lookup"><span data-stu-id="70178-117">Run hello performance testing application</span></span>
<span data-ttu-id="70178-118">Olá tooget de forma mais rápida iniciado é toocompile e exemplos de .NET de execução Olá abaixo, conforme descrito nos passos Olá abaixo.</span><span class="sxs-lookup"><span data-stu-id="70178-118">hello quickest way tooget started is toocompile and run hello .NET sample below, as described in hello steps below.</span></span> <span data-ttu-id="70178-119">Também pode rever o código de origem Olá e implementar aplicações de cliente própria de tooyour de configurações semelhantes.</span><span class="sxs-lookup"><span data-stu-id="70178-119">You can also review hello source code and implement similar configurations tooyour own client applications.</span></span>

<span data-ttu-id="70178-120">**Passo 1:** projeto Olá de transferência do [amostra de testes de desempenho do Azure Cosmos DB](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/documentdb-benchmark), ou o repositório do GitHub bifurcação Olá.</span><span class="sxs-lookup"><span data-stu-id="70178-120">**Step 1:** Download hello project from [Azure Cosmos DB Performance Testing Sample](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/documentdb-benchmark), or fork hello GitHub repository.</span></span>

<span data-ttu-id="70178-121">**Passo 2:** modificar definições de Olá EndpointUrl, AuthorizationKey, CollectionThroughput e DocumentTemplate (opcional) no App. config.</span><span class="sxs-lookup"><span data-stu-id="70178-121">**Step 2:** Modify hello settings for EndpointUrl, AuthorizationKey, CollectionThroughput and DocumentTemplate (optional) in App.config.</span></span>

> [!NOTE]
> <span data-ttu-id="70178-122">Antes do aprovisionamento de coleções com débito elevado, consulte toohello [página de preços](https://azure.microsoft.com/pricing/details/cosmos-db/) os custos de Olá tooestimate por coleção.</span><span class="sxs-lookup"><span data-stu-id="70178-122">Before provisioning collections with high throughput, please refer toohello [Pricing Page](https://azure.microsoft.com/pricing/details/cosmos-db/) tooestimate hello costs per collection.</span></span> <span data-ttu-id="70178-123">BD do Azure do Cosmos faturas armazenamento e débito independentemente numa base horária, pelo que pode reduzir os custos eliminando ou reduzir o débito de Olá das suas coleções de base de dados do Azure Cosmos depois de testar.</span><span class="sxs-lookup"><span data-stu-id="70178-123">Azure Cosmos DB bills storage and throughput independently on an hourly basis, so you can save costs by deleting or lowering hello throughput of your Azure Cosmos DB collections after testing.</span></span>
> 
> 

<span data-ttu-id="70178-124">**Passo 3:** compilar e executar a aplicação de consola de Olá Olá linha de comandos.</span><span class="sxs-lookup"><span data-stu-id="70178-124">**Step 3:** Compile and run hello console app from hello command line.</span></span> <span data-ttu-id="70178-125">Deverá ver um resultado semelhante Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="70178-125">You should see output like hello following:</span></span>

    Summary:
    ---------------------------------------------------------------------
    Endpoint: https://docdb-scale-demo.documents.azure.com:443/
    Collection : db.testdata at 50000 request units per second
    Document Template*: Player.json
    Degree of parallelism*: 500
    ---------------------------------------------------------------------

    DocumentDBBenchmark starting...
    Creating database db
    Creating collection testdata
    Creating metric collection metrics
    Retrying after sleeping for 00:03:34.1720000
    Starting Inserts with 500 tasks
    Inserted 661 docs @ 656 writes/s, 6860 RU/s (18B max monthly 1KB reads)
    Inserted 6505 docs @ 2668 writes/s, 27962 RU/s (72B max monthly 1KB reads)
    Inserted 11756 docs @ 3240 writes/s, 33957 RU/s (88B max monthly 1KB reads)
    Inserted 17076 docs @ 3590 writes/s, 37627 RU/s (98B max monthly 1KB reads)
    Inserted 22106 docs @ 3748 writes/s, 39281 RU/s (102B max monthly 1KB reads)
    Inserted 28430 docs @ 3902 writes/s, 40897 RU/s (106B max monthly 1KB reads)
    Inserted 33492 docs @ 3928 writes/s, 41168 RU/s (107B max monthly 1KB reads)
    Inserted 38392 docs @ 3963 writes/s, 41528 RU/s (108B max monthly 1KB reads)
    Inserted 43371 docs @ 4012 writes/s, 42051 RU/s (109B max monthly 1KB reads)
    Inserted 48477 docs @ 4035 writes/s, 42282 RU/s (110B max monthly 1KB reads)
    Inserted 53845 docs @ 4088 writes/s, 42845 RU/s (111B max monthly 1KB reads)
    Inserted 59267 docs @ 4138 writes/s, 43364 RU/s (112B max monthly 1KB reads)
    Inserted 64703 docs @ 4197 writes/s, 43981 RU/s (114B max monthly 1KB reads)
    Inserted 70428 docs @ 4216 writes/s, 44181 RU/s (115B max monthly 1KB reads)
    Inserted 75868 docs @ 4247 writes/s, 44505 RU/s (115B max monthly 1KB reads)
    Inserted 81571 docs @ 4280 writes/s, 44852 RU/s (116B max monthly 1KB reads)
    Inserted 86271 docs @ 4273 writes/s, 44783 RU/s (116B max monthly 1KB reads)
    Inserted 91993 docs @ 4299 writes/s, 45056 RU/s (117B max monthly 1KB reads)
    Inserted 97469 docs @ 4292 writes/s, 44984 RU/s (117B max monthly 1KB reads)
    Inserted 99736 docs @ 4192 writes/s, 43930 RU/s (114B max monthly 1KB reads)
    Inserted 99997 docs @ 4013 writes/s, 42051 RU/s (109B max monthly 1KB reads)
    Inserted 100000 docs @ 3846 writes/s, 40304 RU/s (104B max monthly 1KB reads)

    Summary:
    ---------------------------------------------------------------------
    Inserted 100000 docs @ 3834 writes/s, 40180 RU/s (104B max monthly 1KB reads)
    ---------------------------------------------------------------------
    DocumentDBBenchmark completed successfully.


<span data-ttu-id="70178-126">**Passo 4 (se necessário):** Olá débito comunicado (RU/s) da ferramenta de Olá deve ser Olá igual ou superior ao débito aprovisionado de Olá da coleção de Olá.</span><span class="sxs-lookup"><span data-stu-id="70178-126">**Step 4 (if necessary):** hello throughput reported (RU/s) from hello tool should be hello same or higher than hello provisioned throughput of hello collection.</span></span> <span data-ttu-id="70178-127">Caso contrário, crescente Olá DegreeOfParallelism pequenos incrementos pode ajudá-lo a atingir o limite de Olá.</span><span class="sxs-lookup"><span data-stu-id="70178-127">If not, increasing hello DegreeOfParallelism in small increments may help you reach hello limit.</span></span> <span data-ttu-id="70178-128">Se plateaus débito Olá da sua aplicação de cliente, iniciar múltiplas instâncias da aplicação Olá no mesmo Olá ou diferentes máquinas irão ajudar a alcançar o limite de Olá aprovisionado em Olá instâncias diferentes.</span><span class="sxs-lookup"><span data-stu-id="70178-128">If hello throughput from your client app plateaus, launching multiple instances of hello app on hello same or different machines will help you reach hello provisioned limit across hello different instances.</span></span> <span data-ttu-id="70178-129">Se precisar de ajuda com este passo, escreva uma mensagem de e-mail tooaskcosmosdb@microsoft.com ou ficheiros de um pedido de suporte de Olá [Portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="70178-129">If you need help with this step, please, write an email tooaskcosmosdb@microsoft.com or file a support ticket from hello [Azure Portal](https://portal.azure.com).</span></span>

<span data-ttu-id="70178-130">Assim que tiver de executar a aplicação Olá, pode experimentar diferentes [indexação políticas](indexing-policies.md) e [níveis de consistência](consistency-levels.md) toounderstand o impacto na débito e latência.</span><span class="sxs-lookup"><span data-stu-id="70178-130">Once you have hello app running, you can try different [Indexing policies](indexing-policies.md) and [Consistency levels](consistency-levels.md) toounderstand their impact on throughput and latency.</span></span> <span data-ttu-id="70178-131">Também pode rever o código de origem Olá e implementar aplicações de produção ou conjuntos de teste própria de tooyour configurações semelhantes.</span><span class="sxs-lookup"><span data-stu-id="70178-131">You can also review hello source code and implement similar configurations tooyour own test suites or production applications.</span></span>

## <a name="next-steps"></a><span data-ttu-id="70178-132">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="70178-132">Next steps</span></span>
<span data-ttu-id="70178-133">Neste artigo, vamos consultou como pode efetuar o desempenho e dimensionamento de teste com base de dados do Cosmos através de uma aplicação de consola .NET.</span><span class="sxs-lookup"><span data-stu-id="70178-133">In this article, we looked at how you can perform performance and scale testing with Cosmos DB using a .NET console app.</span></span> <span data-ttu-id="70178-134">Consulte toohello ligações abaixo para obter informações adicionais sobre como trabalhar com a base de dados do Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="70178-134">Please refer toohello links below for additional information on working with Azure Cosmos DB.</span></span>

* [<span data-ttu-id="70178-135">Exemplo de testes de desempenho de base de dados do Cosmos do Azure</span><span class="sxs-lookup"><span data-stu-id="70178-135">Azure Cosmos DB performance testing sample</span></span>](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/documentdb-benchmark)
* [<span data-ttu-id="70178-136">Tooimprove de opções de configuração do cliente desempenho de base de dados do Azure Cosmos</span><span class="sxs-lookup"><span data-stu-id="70178-136">Client configuration options tooimprove Azure Cosmos DB performance</span></span>](performance-tips.md)
* [<span data-ttu-id="70178-137">Criação de partições do lado do servidor na base de dados do Azure Cosmos</span><span class="sxs-lookup"><span data-stu-id="70178-137">Server-side partitioning in Azure Cosmos DB</span></span>](partition-data.md)


