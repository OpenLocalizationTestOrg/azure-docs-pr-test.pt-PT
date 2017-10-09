---
title: aaaAzure Cosmos DB Node.js API, SDK & recursos | Microsoft Docs
description: "Saiba tudo sobre Olá Node.js API e SDK, incluindo as datas de versão, datas de extinção e as alterações efetuadas entre cada versão do Olá SDK Node.js do Azure Cosmos DB."
services: cosmos-db
documentationcenter: nodejs
author: rnagpal
manager: jhubbard
editor: cgronlun
ms.assetid: 9d5621fa-0e11-4619-a28b-a19d872bcf37
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/14/2017
ms.author: rnagpal
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d450b9a9ea7b0f4717ddae8940121fc458ea3744
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-nodejs-sdk-release-notes-and-resources"></a><span data-ttu-id="a6052-103">Azure SDK Node.js do Cosmos DB: Notas de versão e recursos</span><span class="sxs-lookup"><span data-stu-id="a6052-103">Azure Cosmos DB Node.js SDK: Release notes and resources</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a6052-104">.NET</span><span class="sxs-lookup"><span data-stu-id="a6052-104">.NET</span></span>](documentdb-sdk-dotnet.md)
> * [<span data-ttu-id="a6052-105">Feed de alteração de .NET</span><span class="sxs-lookup"><span data-stu-id="a6052-105">.NET Change Feed</span></span>](documentdb-sdk-dotnet-changefeed.md)
> * [<span data-ttu-id="a6052-106">.NET Core</span><span class="sxs-lookup"><span data-stu-id="a6052-106">.NET Core</span></span>](documentdb-sdk-dotnet-core.md)
> * [<span data-ttu-id="a6052-107">Node.js</span><span class="sxs-lookup"><span data-stu-id="a6052-107">Node.js</span></span>](documentdb-sdk-node.md)
> * [<span data-ttu-id="a6052-108">Java</span><span class="sxs-lookup"><span data-stu-id="a6052-108">Java</span></span>](documentdb-sdk-java.md)
> * [<span data-ttu-id="a6052-109">Python</span><span class="sxs-lookup"><span data-stu-id="a6052-109">Python</span></span>](documentdb-sdk-python.md)
> * [<span data-ttu-id="a6052-110">REST</span><span class="sxs-lookup"><span data-stu-id="a6052-110">REST</span></span>](https://docs.microsoft.com/rest/api/documentdb/)
> * [<span data-ttu-id="a6052-111">Fornecedor de Recursos REST</span><span class="sxs-lookup"><span data-stu-id="a6052-111">REST Resource Provider</span></span>](https://docs.microsoft.com/rest/api/documentdbresourceprovider/)
> * [<span data-ttu-id="a6052-112">SQL</span><span class="sxs-lookup"><span data-stu-id="a6052-112">SQL</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx)
> 
> 

<table>

<tr><td><span data-ttu-id="a6052-113">**Transferir o SDK**</span><span class="sxs-lookup"><span data-stu-id="a6052-113">**Download SDK**</span></span></td><td>[<span data-ttu-id="a6052-114">NPM</span><span class="sxs-lookup"><span data-stu-id="a6052-114">NPM</span></span>](https://www.npmjs.com/package/documentdb)</td></tr>

<tr><td><span data-ttu-id="a6052-115">**Documentação da API**</span><span class="sxs-lookup"><span data-stu-id="a6052-115">**API documentation**</span></span></td><td>[<span data-ttu-id="a6052-116">Documentação de referência de API node.js</span><span class="sxs-lookup"><span data-stu-id="a6052-116">Node.js API reference documentation</span></span>](http://azure.github.io/azure-documentdb-node/DocumentClient.html)</td></tr>

<tr><td><span data-ttu-id="a6052-117">**Instruções de instalação do SDK**</span><span class="sxs-lookup"><span data-stu-id="a6052-117">**SDK installation instructions**</span></span></td><td>[<span data-ttu-id="a6052-118">Instruções de instalação</span><span class="sxs-lookup"><span data-stu-id="a6052-118">Installation instructions</span></span>](http://azure.github.io/azure-documentdb-node/)</td></tr>

<tr><td><span data-ttu-id="a6052-119">**Contribuir tooSDK**</span><span class="sxs-lookup"><span data-stu-id="a6052-119">**Contribute tooSDK**</span></span></td><td>[<span data-ttu-id="a6052-120">GitHub</span><span class="sxs-lookup"><span data-stu-id="a6052-120">GitHub</span></span>](https://github.com/Azure/azure-documentdb-node/tree/master/source)</td></tr>

<tr><td><span data-ttu-id="a6052-121">**Amostras**</span><span class="sxs-lookup"><span data-stu-id="a6052-121">**Samples**</span></span></td><td>[<span data-ttu-id="a6052-122">Exemplos de código do node.js</span><span class="sxs-lookup"><span data-stu-id="a6052-122">Node.js code samples</span></span>](documentdb-nodejs-samples.md)</td></tr>

<tr><td><span data-ttu-id="a6052-123">**Tutorial de introdução**</span><span class="sxs-lookup"><span data-stu-id="a6052-123">**Get started tutorial**</span></span></td><td>[<span data-ttu-id="a6052-124">Introdução ao hello Node.js SDK</span><span class="sxs-lookup"><span data-stu-id="a6052-124">Get started with hello Node.js SDK</span></span>](documentdb-nodejs-get-started.md)</td></tr>

<tr><td><span data-ttu-id="a6052-125">**Tutorial de aplicação Web**</span><span class="sxs-lookup"><span data-stu-id="a6052-125">**Web app tutorial**</span></span></td><td>[<span data-ttu-id="a6052-126">Criar uma aplicação de web do Node.js utilizando o Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="a6052-126">Build a Node.js web application using Azure Cosmos DB</span></span>](documentdb-nodejs-application.md)</td></tr>

<tr><td><span data-ttu-id="a6052-127">**Plataforma suportada atual**</span><span class="sxs-lookup"><span data-stu-id="a6052-127">**Current supported platform**</span></span></td><td> 
[<span data-ttu-id="a6052-128">V6. x do node.js</span><span class="sxs-lookup"><span data-stu-id="a6052-128">Node.js v6.x</span></span>](https://nodejs.org/en/blog/release/v6.10.3/)<br/> 
[<span data-ttu-id="a6052-129">NODE.js v4.2.0</span><span class="sxs-lookup"><span data-stu-id="a6052-129">Node.js v4.2.0</span></span>](https://nodejs.org/en/blog/release/v4.2.0/)<br/> 
[<span data-ttu-id="a6052-130">NODE.js v0.12</span><span class="sxs-lookup"><span data-stu-id="a6052-130">Node.js v0.12</span></span>](https://nodejs.org/en/blog/release/v0.12.0/)<br/> 
<span data-ttu-id="a6052-131">[NODE.js v0.10](https://nodejs.org/en/blog/release/v0.10.0/) 
</span><span class="sxs-lookup"><span data-stu-id="a6052-131">[Node.js v0.10](https://nodejs.org/en/blog/release/v0.10.0/) 
</span></span></td></tr>
</table></br>

## <a name="release-notes"></a><span data-ttu-id="a6052-132">Notas de versão</span><span class="sxs-lookup"><span data-stu-id="a6052-132">Release notes</span></span>

### <span data-ttu-id="a6052-133"><a name="1.12.2"/>1.12.2</a></span><span class="sxs-lookup"><span data-stu-id="a6052-133"><a name="1.12.2"/>1.12.2</a></span></span>
*   <span data-ttu-id="a6052-134">documentação de npm for corrigida.</span><span class="sxs-lookup"><span data-stu-id="a6052-134">npm documentation fixed.</span></span>

### <span data-ttu-id="a6052-135"><a name="1.12.1"/>1.12.1</a></span><span class="sxs-lookup"><span data-stu-id="a6052-135"><a name="1.12.1"/>1.12.1</a></span></span>
* <span data-ttu-id="a6052-136">Corrigido um erro no executeStoredProcedure onde documentos envolvidos tinham carateres Unicode especiais (LS, PS).</span><span class="sxs-lookup"><span data-stu-id="a6052-136">Fixed a bug in executeStoredProcedure where documents involved had special Unicode characters (LS, PS).</span></span>
* <span data-ttu-id="a6052-137">Corrigido um erro no processamento de documentos com a chave de partição Olá carateres Unicode.</span><span class="sxs-lookup"><span data-stu-id="a6052-137">Fixed a bug in handling documents with Unicode characters in hello partition key.</span></span>
* <span data-ttu-id="a6052-138">Suporte fixo para criação de coleções com suporte de dados de nome de Olá.</span><span class="sxs-lookup"><span data-stu-id="a6052-138">Fixed support for creating collections with hello name media.</span></span> <span data-ttu-id="a6052-139">Problema de Github #114.</span><span class="sxs-lookup"><span data-stu-id="a6052-139">Github issue #114.</span></span>
* <span data-ttu-id="a6052-140">Suporte fixo para o token de autorização de permissão.</span><span class="sxs-lookup"><span data-stu-id="a6052-140">Fixed support for permission authorization token.</span></span> <span data-ttu-id="a6052-141">Problema de Github #178.</span><span class="sxs-lookup"><span data-stu-id="a6052-141">Github issue #178.</span></span>

### <span data-ttu-id="a6052-142"><a name="1.12.0"/>1.12.0</a></span><span class="sxs-lookup"><span data-stu-id="a6052-142"><a name="1.12.0"/>1.12.0</a></span></span>
* <span data-ttu-id="a6052-143">Foi adicionado suporte para um novo [nível de consistência](consistency-levels.md) chamado ConsistentPrefix.</span><span class="sxs-lookup"><span data-stu-id="a6052-143">Added support for a new [consistency level](consistency-levels.md) called ConsistentPrefix.</span></span>
* <span data-ttu-id="a6052-144">Suporte adicionado para UriFactory.</span><span class="sxs-lookup"><span data-stu-id="a6052-144">Added support for UriFactory.</span></span>
* <span data-ttu-id="a6052-145">Corrigido um erro de suporte de Unicode.</span><span class="sxs-lookup"><span data-stu-id="a6052-145">Fixed a Unicode support bug.</span></span> <span data-ttu-id="a6052-146">Problema de GitHub #171.</span><span class="sxs-lookup"><span data-stu-id="a6052-146">GitHub issue #171.</span></span>

### <span data-ttu-id="a6052-147"><a name="1.11.0"/>1.11.0</a></span><span class="sxs-lookup"><span data-stu-id="a6052-147"><a name="1.11.0"/>1.11.0</a></span></span>
* <span data-ttu-id="a6052-148">Suporte adicionado Olá para consultas de agregação (CONTAGEM, MIN, MAX, soma e média).</span><span class="sxs-lookup"><span data-stu-id="a6052-148">Added hello support for aggregation queries (COUNT, MIN, MAX, SUM, and AVG).</span></span>
* <span data-ttu-id="a6052-149">Opção de Olá foram adicionadas para controlar o grau de paralelismo para entre consultas de partição.</span><span class="sxs-lookup"><span data-stu-id="a6052-149">Added hello option for controlling degree of parallelism for cross partition queries.</span></span>
* <span data-ttu-id="a6052-150">Opção de Olá adicionado para desativar a verificação de SSL quando em execução contra o emulador de BD do Cosmos do Azure.</span><span class="sxs-lookup"><span data-stu-id="a6052-150">Added hello option for disabling SSL verification when running against Azure Cosmos DB Emulator.</span></span>
* <span data-ttu-id="a6052-151">Lowered débito mínimo em coleções particionadas de 10,100 RU/s too2500 RU/s.</span><span class="sxs-lookup"><span data-stu-id="a6052-151">Lowered minimum throughput on partitioned collections from 10,100 RU/s too2500 RU/s.</span></span>
* <span data-ttu-id="a6052-152">Erros de hora token do continuação Olá fixo para a coleção de partições únicas.</span><span class="sxs-lookup"><span data-stu-id="a6052-152">Fixed hello continuation token bug for single partition collection.</span></span> <span data-ttu-id="a6052-153">Problema de Github #107.</span><span class="sxs-lookup"><span data-stu-id="a6052-153">Github issue #107.</span></span>
* <span data-ttu-id="a6052-154">Erros de executeStoredProcedure Olá fixo processar 0 como param único.</span><span class="sxs-lookup"><span data-stu-id="a6052-154">Fixed hello executeStoredProcedure bug in handling 0 as single param.</span></span> <span data-ttu-id="a6052-155">Problema de Github #155.</span><span class="sxs-lookup"><span data-stu-id="a6052-155">Github issue #155.</span></span>

### <span data-ttu-id="a6052-156"><a name="1.10.2"/>1.10.2</a></span><span class="sxs-lookup"><span data-stu-id="a6052-156"><a name="1.10.2"/>1.10.2</a></span></span>
* <span data-ttu-id="a6052-157">Versão do agente de utilizador fixo cabeçalho tooinclude Olá SDK.</span><span class="sxs-lookup"><span data-stu-id="a6052-157">Fixed user-agent header tooinclude hello SDK version.</span></span>
* <span data-ttu-id="a6052-158">Limpeza de código secundárias.</span><span class="sxs-lookup"><span data-stu-id="a6052-158">Minor code cleanup.</span></span>

### <span data-ttu-id="a6052-159"><a name="1.10.1"/>1.10.1</a></span><span class="sxs-lookup"><span data-stu-id="a6052-159"><a name="1.10.1"/>1.10.1</a></span></span>
* <span data-ttu-id="a6052-160">Quando utilizar Olá SDK tootarget Olá emulator(hostname=localhost) a desativar a verificação de SSL.</span><span class="sxs-lookup"><span data-stu-id="a6052-160">Disabling SSL verification when using hello SDK tootarget hello emulator(hostname=localhost).</span></span>
* <span data-ttu-id="a6052-161">Suporte adicionado para ativar o registo de script durante a execução do procedimento armazenado.</span><span class="sxs-lookup"><span data-stu-id="a6052-161">Added support for enabling script logging during stored procedure execution.</span></span>

### <span data-ttu-id="a6052-162"><a name="1.10.0"/>1.10.0</a></span><span class="sxs-lookup"><span data-stu-id="a6052-162"><a name="1.10.0"/>1.10.0</a></span></span>
* <span data-ttu-id="a6052-163">Suporte adicionado para entre consultas paralelas de partição.</span><span class="sxs-lookup"><span data-stu-id="a6052-163">Added support for cross partition parallel queries.</span></span>
* <span data-ttu-id="a6052-164">Suporte adicionado para consultas de parte superior/ORDER BY para coleções particionadas.</span><span class="sxs-lookup"><span data-stu-id="a6052-164">Added support for TOP/ORDER BY queries for partitioned collections.</span></span>

### <span data-ttu-id="a6052-165"><a name="1.9.0"/>1.9.0</a></span><span class="sxs-lookup"><span data-stu-id="a6052-165"><a name="1.9.0"/>1.9.0</a></span></span>
* <span data-ttu-id="a6052-166">Suporte de política de repetição adicionado para pedidos otimizados.</span><span class="sxs-lookup"><span data-stu-id="a6052-166">Added retry policy support for throttled requests.</span></span> <span data-ttu-id="a6052-167">(Pedidos otimizados recebem uma pedido taxa demasiado grande exceção, o código de erro 429.) Por predefinição, base de dados do Azure Cosmos repete nove vezes para cada pedido quando for detetado o código de erro 429, para respeitar o tempo de retryAfter Olá no cabeçalho de resposta de Olá.</span><span class="sxs-lookup"><span data-stu-id="a6052-167">(Throttled requests receive a request rate too large exception, error code 429.) By default, Azure Cosmos DB retries nine times for each request when error code 429 is encountered, honoring hello retryAfter time in hello response header.</span></span> <span data-ttu-id="a6052-168">Um período de tempo do intervalo de repetição fixo pode agora ser definido como parte da Olá RetryOptions propriedade no objecto de ConnectionPolicy Olá se pretender que o tempo de retryAfter tooignore Olá devolvido pelo servidor entre repetições Olá.</span><span class="sxs-lookup"><span data-stu-id="a6052-168">A fixed retry interval time can now be set as part of hello RetryOptions property on hello ConnectionPolicy object if you want tooignore hello retryAfter time returned by server between hello retries.</span></span> <span data-ttu-id="a6052-169">BD do Azure do Cosmos aguarda agora um máximo de 30 segundos para cada pedido que está a ser limitado (independentemente da contagem de repetições) e devolve a resposta de Olá com o código de erro 429.</span><span class="sxs-lookup"><span data-stu-id="a6052-169">Azure Cosmos DB now waits for a maximum of 30 seconds for each request that is being throttled (irrespective of retry count) and returns hello response with error code 429.</span></span> <span data-ttu-id="a6052-170">Neste momento também pode ser substituído na Olá RetryOptions propriedade ConnectionPolicy objeto.</span><span class="sxs-lookup"><span data-stu-id="a6052-170">This time can also be overridden in hello RetryOptions property on ConnectionPolicy object.</span></span>
* <span data-ttu-id="a6052-171">BD do cosmos devolve agora x-ms-limitação--contagem de repetições e x-ms-throttle-retry-wait-time-ms como cabeçalhos de resposta de Olá em cada limitação do pedido toodenote Olá Repetir contagem e Olá cumulativo tempo do pedido Olá aguardaram entre repetições Olá.</span><span class="sxs-lookup"><span data-stu-id="a6052-171">Cosmos DB now returns x-ms-throttle-retry-count and x-ms-throttle-retry-wait-time-ms as hello response headers in every request toodenote hello throttle retry count and hello cumulative time hello request waited between hello retries.</span></span>
* <span data-ttu-id="a6052-172">foi adicionado Olá RetryOptions classe, a exposição de propriedade de RetryOptions Olá na classe de ConnectionPolicy Olá que pode ser utilizado toooverride algumas das predefinido Olá as opções de repetição.</span><span class="sxs-lookup"><span data-stu-id="a6052-172">hello RetryOptions class was added, exposing hello RetryOptions property on hello ConnectionPolicy class that can be used toooverride some of hello default retry options.</span></span>

### <span data-ttu-id="a6052-173"><a name="1.8.0"/>1.8.0</a></span><span class="sxs-lookup"><span data-stu-id="a6052-173"><a name="1.8.0"/>1.8.0</a></span></span>
* <span data-ttu-id="a6052-174">Suporte adicionado Olá para contas de multirregião base de dados.</span><span class="sxs-lookup"><span data-stu-id="a6052-174">Added hello support for multi-region database accounts.</span></span>

### <span data-ttu-id="a6052-175"><a name="1.7.0"/>1.7.0</a></span><span class="sxs-lookup"><span data-stu-id="a6052-175"><a name="1.7.0"/>1.7.0</a></span></span>
* <span data-ttu-id="a6052-176">Olá adicionado suporte para a funcionalidade de tooLive(TTL) de tempo para documentos.</span><span class="sxs-lookup"><span data-stu-id="a6052-176">Added hello support for Time tooLive(TTL) feature for documents.</span></span>

### <span data-ttu-id="a6052-177"><a name="1.6.0"/>1.6.0</a></span><span class="sxs-lookup"><span data-stu-id="a6052-177"><a name="1.6.0"/>1.6.0</a></span></span>
* <span data-ttu-id="a6052-178">Implementado [particionada coleções](partition-data.md) e [níveis de desempenho definido pelo utilizador](performance-levels.md).</span><span class="sxs-lookup"><span data-stu-id="a6052-178">Implemented [partitioned collections](partition-data.md) and [user-defined performance levels](performance-levels.md).</span></span>

### <span data-ttu-id="a6052-179"><a name="1.5.6"/>1.5.6</a></span><span class="sxs-lookup"><span data-stu-id="a6052-179"><a name="1.5.6"/>1.5.6</a></span></span>
* <span data-ttu-id="a6052-180">Erros de RangePartitionResolver.resolveForRead fixo onde não foi devolver ligações devido tooa concat incorreto de resultados.</span><span class="sxs-lookup"><span data-stu-id="a6052-180">Fixed RangePartitionResolver.resolveForRead bug where it was not returning links due tooa bad concat of results.</span></span>

### <span data-ttu-id="a6052-181"><a name="1.5.5"/>1.5.5</a></span><span class="sxs-lookup"><span data-stu-id="a6052-181"><a name="1.5.5"/>1.5.5</a></span></span>
* <span data-ttu-id="a6052-182">Corrigido hashParitionResolver resolveForRead(): quando nenhuma chave de partição fornecido foi gerar exceção, em vez de devolver uma lista de todas as ligações registadas.</span><span class="sxs-lookup"><span data-stu-id="a6052-182">Fixed hashParitionResolver resolveForRead(): When no partition key supplied was throwing exception, instead of returning a list of all registered links.</span></span>

### <span data-ttu-id="a6052-183"><a name="1.5.4"/>1.5.4</a></span><span class="sxs-lookup"><span data-stu-id="a6052-183"><a name="1.5.4"/>1.5.4</a></span></span>
* <span data-ttu-id="a6052-184">Corrige o problema [#100](https://github.com/Azure/azure-documentdb-node/issues/100) -agente dedicado de HTTPS: evitar modificar agente global de Olá para fins de BD do Cosmos do Azure.</span><span class="sxs-lookup"><span data-stu-id="a6052-184">Fixes issue [#100](https://github.com/Azure/azure-documentdb-node/issues/100) - Dedicated HTTPS Agent: Avoid modifying hello global agent for Azure Cosmos DB purposes.</span></span> <span data-ttu-id="a6052-185">Utilize um agente dedicado para todos os pedidos do lib Olá.</span><span class="sxs-lookup"><span data-stu-id="a6052-185">Use a dedicated agent for all of hello lib’s requests.</span></span>

### <span data-ttu-id="a6052-186"><a name="1.5.3"/>1.5.3</a></span><span class="sxs-lookup"><span data-stu-id="a6052-186"><a name="1.5.3"/>1.5.3</a></span></span>
* <span data-ttu-id="a6052-187">Corrige o problema [#81](https://github.com/Azure/azure-documentdb-node/issues/81) - corretamente processar travessões no ID de suporte de dados.</span><span class="sxs-lookup"><span data-stu-id="a6052-187">Fixes issue [#81](https://github.com/Azure/azure-documentdb-node/issues/81) - Properly handle dashes in media ids.</span></span>

### <span data-ttu-id="a6052-188"><a name="1.5.2"/>1.5.2</a></span><span class="sxs-lookup"><span data-stu-id="a6052-188"><a name="1.5.2"/>1.5.2</a></span></span>
* <span data-ttu-id="a6052-189">Corrige o problema [#95](https://github.com/Azure/azure-documentdb-node/issues/95) -EventEmitter escuta fuga de aviso.</span><span class="sxs-lookup"><span data-stu-id="a6052-189">Fixes issue [#95](https://github.com/Azure/azure-documentdb-node/issues/95) - EventEmitter listener leak warning.</span></span>

### <span data-ttu-id="a6052-190"><a name="1.5.1"/>1.5.1</a></span><span class="sxs-lookup"><span data-stu-id="a6052-190"><a name="1.5.1"/>1.5.1</a></span></span>
* <span data-ttu-id="a6052-191">Corrige o problema [#92](https://github.com/Azure/azure-documentdb-node/issues/90) -mudar o nome de pasta Hash toohash para sistemas de maiúsculas e minúsculas.</span><span class="sxs-lookup"><span data-stu-id="a6052-191">Fixes issue [#92](https://github.com/Azure/azure-documentdb-node/issues/90) - rename folder Hash toohash for case-sensitive systems.</span></span>

### <span data-ttu-id="a6052-192"><a name="1.5.0"/>1.5.0</a></span><span class="sxs-lookup"><span data-stu-id="a6052-192"><a name="1.5.0"/>1.5.0</a></span></span>
* <span data-ttu-id="a6052-193">Suporte de fragmentação de implementar, adicionando as resoluções de hash & ntervalo de datas da partição.</span><span class="sxs-lookup"><span data-stu-id="a6052-193">Implement sharding support by adding hash & range partition resolvers.</span></span>

### <span data-ttu-id="a6052-194"><a name="1.4.0"/>1.4.0</a></span><span class="sxs-lookup"><span data-stu-id="a6052-194"><a name="1.4.0"/>1.4.0</a></span></span>
* <span data-ttu-id="a6052-195">Implemente Upsert.</span><span class="sxs-lookup"><span data-stu-id="a6052-195">Implement Upsert.</span></span> <span data-ttu-id="a6052-196">Novo upsertXXX os métodos no documentClient.</span><span class="sxs-lookup"><span data-stu-id="a6052-196">New upsertXXX methods on documentClient.</span></span>

### <span data-ttu-id="a6052-197"><a name="1.3.0"/>1.3.0</a></span><span class="sxs-lookup"><span data-stu-id="a6052-197"><a name="1.3.0"/>1.3.0</a></span></span>
* <span data-ttu-id="a6052-198">Ignorado toobring números de versão em alinhamento com outros SDKs.</span><span class="sxs-lookup"><span data-stu-id="a6052-198">Skipped toobring version numbers in alignment with other SDKs.</span></span>

### <span data-ttu-id="a6052-199"><a name="1.2.2"/>1.2.2</a></span><span class="sxs-lookup"><span data-stu-id="a6052-199"><a name="1.2.2"/>1.2.2</a></span></span>
* <span data-ttu-id="a6052-200">Divisão Q promete repositório de toonew wrapper.</span><span class="sxs-lookup"><span data-stu-id="a6052-200">Split Q promises wrapper toonew repository.</span></span>
* <span data-ttu-id="a6052-201">Atualize o ficheiro de toopackage para registo de npm.</span><span class="sxs-lookup"><span data-stu-id="a6052-201">Update toopackage file for npm registry.</span></span>

### <span data-ttu-id="a6052-202"><a name="1.2.1"/>1.2.1</a></span><span class="sxs-lookup"><span data-stu-id="a6052-202"><a name="1.2.1"/>1.2.1</a></span></span>
* <span data-ttu-id="a6052-203">Implementa o ID de encaminhamento com base.</span><span class="sxs-lookup"><span data-stu-id="a6052-203">Implements ID Based Routing.</span></span>
* <span data-ttu-id="a6052-204">Corrige o problema [#49](https://github.com/Azure/azure-documentdb-node/issues/49) -propriedade atual está em conflito com current () do método.</span><span class="sxs-lookup"><span data-stu-id="a6052-204">Fixes Issue [#49](https://github.com/Azure/azure-documentdb-node/issues/49) - current property conflicts with method current().</span></span>

### <span data-ttu-id="a6052-205"><a name="1.2.0"/>1.2.0</a></span><span class="sxs-lookup"><span data-stu-id="a6052-205"><a name="1.2.0"/>1.2.0</a></span></span>
* <span data-ttu-id="a6052-206">Suporte adicionado para o índice de Geoespacial.</span><span class="sxs-lookup"><span data-stu-id="a6052-206">Added support for GeoSpatial index.</span></span>
* <span data-ttu-id="a6052-207">Valida a propriedade id de todos os recursos.</span><span class="sxs-lookup"><span data-stu-id="a6052-207">Validates id property for all resources.</span></span> <span data-ttu-id="a6052-208">Os IDs de recursos não podem conter?, /, # &#47; &#47; carateres nem terminar com um espaço.</span><span class="sxs-lookup"><span data-stu-id="a6052-208">Ids for resources cannot contain ?, /, #, &#47;&#47;, characters or end with a space.</span></span>
* <span data-ttu-id="a6052-209">Adiciona tooResourceResponse de "progresso de transformação de índice" do novo cabeçalho.</span><span class="sxs-lookup"><span data-stu-id="a6052-209">Adds new header "index transformation progress" tooResourceResponse.</span></span>

### <span data-ttu-id="a6052-210"><a name="1.1.0"/>1.1.0</a></span><span class="sxs-lookup"><span data-stu-id="a6052-210"><a name="1.1.0"/>1.1.0</a></span></span>
* <span data-ttu-id="a6052-211">Implementa a política de indexação V2.</span><span class="sxs-lookup"><span data-stu-id="a6052-211">Implements V2 indexing policy.</span></span>

### <span data-ttu-id="a6052-212"><a name="1.0.3"/>1.0.3</a></span><span class="sxs-lookup"><span data-stu-id="a6052-212"><a name="1.0.3"/>1.0.3</a></span></span>
* <span data-ttu-id="a6052-213">Problema [#40](https://github.com/Azure/azure-documentdb-node/issues/40) - implementado eslint grunt configurações de núcleos de Olá e promessa SDK.</span><span class="sxs-lookup"><span data-stu-id="a6052-213">Issue [#40](https://github.com/Azure/azure-documentdb-node/issues/40) - Implemented eslint and grunt configurations in hello core and promise SDK.</span></span>

### <span data-ttu-id="a6052-214"><a name="1.0.2"/>1.0.2</a></span><span class="sxs-lookup"><span data-stu-id="a6052-214"><a name="1.0.2"/>1.0.2</a></span></span>
* <span data-ttu-id="a6052-215">Problema [#45](https://github.com/Azure/azure-documentdb-node/issues/45) -Promises wrapper não inclui um cabeçalho com o erro.</span><span class="sxs-lookup"><span data-stu-id="a6052-215">Issue [#45](https://github.com/Azure/azure-documentdb-node/issues/45) - Promises wrapper does not include header with error.</span></span>

### <span data-ttu-id="a6052-216"><a name="1.0.1"/>1.0.1</a></span><span class="sxs-lookup"><span data-stu-id="a6052-216"><a name="1.0.1"/>1.0.1</a></span></span>
* <span data-ttu-id="a6052-217">Implementado tooquery de capacidade para conflitos adicionando readConflicts, readConflictAsync e queryConflicts.</span><span class="sxs-lookup"><span data-stu-id="a6052-217">Implemented ability tooquery for conflicts by adding readConflicts, readConflictAsync, and queryConflicts.</span></span>
* <span data-ttu-id="a6052-218">Documentação da API atualizada.</span><span class="sxs-lookup"><span data-stu-id="a6052-218">Updated API documentation.</span></span>
* <span data-ttu-id="a6052-219">Problema [#41](https://github.com/Azure/azure-documentdb-node/issues/41) -client.createDocumentAsync erro.</span><span class="sxs-lookup"><span data-stu-id="a6052-219">Issue [#41](https://github.com/Azure/azure-documentdb-node/issues/41) - client.createDocumentAsync error.</span></span>

### <span data-ttu-id="a6052-220"><a name="1.0.0"/>1.0.0</a></span><span class="sxs-lookup"><span data-stu-id="a6052-220"><a name="1.0.0"/>1.0.0</a></span></span>
* <span data-ttu-id="a6052-221">GA SDK.</span><span class="sxs-lookup"><span data-stu-id="a6052-221">GA SDK.</span></span>

## <a name="release--retirement-dates"></a><span data-ttu-id="a6052-222">Datas de extinção & versão</span><span class="sxs-lookup"><span data-stu-id="a6052-222">Release & Retirement Dates</span></span>
<span data-ttu-id="a6052-223">A Microsoft disponibiliza notificação, pelo menos, **12 meses** previamente extinguir um SDK na ordem toosmooth Olá transição tooa/suportada mais recente versão.</span><span class="sxs-lookup"><span data-stu-id="a6052-223">Microsoft provides notification at least **12 months** in advance of retiring an SDK in order toosmooth hello transition tooa newer/supported version.</span></span>

<span data-ttu-id="a6052-224">Apenas são adicionadas novas funcionalidades e a funcionalidade e otimizações o atual toohello SDK, como tal, é recomendado que lhe toohello sempre atualização mais recente versão do SDK antecipadamente quanto possível.</span><span class="sxs-lookup"><span data-stu-id="a6052-224">New features and functionality and optimizations are only added toohello current SDK, as such it is  recommended that you always upgrade toohello latest SDK version as early as possible.</span></span>

<span data-ttu-id="a6052-225">Qualquer pedido tooCosmos BD utilizando um SDK extinto é rejeitadas pelo serviço de Olá.</span><span class="sxs-lookup"><span data-stu-id="a6052-225">Any request tooCosmos DB using a retired SDK is be rejected by hello service.</span></span>

<br/>

| <span data-ttu-id="a6052-226">Versão</span><span class="sxs-lookup"><span data-stu-id="a6052-226">Version</span></span> | <span data-ttu-id="a6052-227">Data da versão</span><span class="sxs-lookup"><span data-stu-id="a6052-227">Release Date</span></span> | <span data-ttu-id="a6052-228">Data de retirada</span><span class="sxs-lookup"><span data-stu-id="a6052-228">Retirement Date</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="a6052-229">1.12.2</span><span class="sxs-lookup"><span data-stu-id="a6052-229">1.12.2</span></span>](#1.12.2) |<span data-ttu-id="a6052-230">10 de Agosto de 2017</span><span class="sxs-lookup"><span data-stu-id="a6052-230">August 10, 2017</span></span> |--- |
| [<span data-ttu-id="a6052-231">1.12.1</span><span class="sxs-lookup"><span data-stu-id="a6052-231">1.12.1</span></span>](#1.12.1) |<span data-ttu-id="a6052-232">10 de Agosto de 2017</span><span class="sxs-lookup"><span data-stu-id="a6052-232">August 10, 2017</span></span> |--- |
| [<span data-ttu-id="a6052-233">1.12.0</span><span class="sxs-lookup"><span data-stu-id="a6052-233">1.12.0</span></span>](#1.12.0) |<span data-ttu-id="a6052-234">10 de maio de 2017</span><span class="sxs-lookup"><span data-stu-id="a6052-234">May 10, 2017</span></span> |--- |
| [<span data-ttu-id="a6052-235">1.11.0</span><span class="sxs-lookup"><span data-stu-id="a6052-235">1.11.0</span></span>](#1.11.0) |<span data-ttu-id="a6052-236">16 de Março de 2017</span><span class="sxs-lookup"><span data-stu-id="a6052-236">March 16, 2017</span></span> |--- |
| [<span data-ttu-id="a6052-237">1.10.2</span><span class="sxs-lookup"><span data-stu-id="a6052-237">1.10.2</span></span>](#1.10.2) |<span data-ttu-id="a6052-238">27 de Janeiro de 2017</span><span class="sxs-lookup"><span data-stu-id="a6052-238">January 27, 2017</span></span> |--- |
| [<span data-ttu-id="a6052-239">1.10.1</span><span class="sxs-lookup"><span data-stu-id="a6052-239">1.10.1</span></span>](#1.10.1) |<span data-ttu-id="a6052-240">22 de Dezembro de 2016</span><span class="sxs-lookup"><span data-stu-id="a6052-240">December 22, 2016</span></span> |--- |
| [<span data-ttu-id="a6052-241">1.10.0</span><span class="sxs-lookup"><span data-stu-id="a6052-241">1.10.0</span></span>](#1.10.0) |<span data-ttu-id="a6052-242">03 de Outubro de 2016</span><span class="sxs-lookup"><span data-stu-id="a6052-242">October 03, 2016</span></span> |--- |
| [<span data-ttu-id="a6052-243">1.9.0</span><span class="sxs-lookup"><span data-stu-id="a6052-243">1.9.0</span></span>](#1.9.0) |<span data-ttu-id="a6052-244">07 de Julho de 2016</span><span class="sxs-lookup"><span data-stu-id="a6052-244">July 07, 2016</span></span> |--- |
| [<span data-ttu-id="a6052-245">1.8.0</span><span class="sxs-lookup"><span data-stu-id="a6052-245">1.8.0</span></span>](#1.8.0) |<span data-ttu-id="a6052-246">14 de Junho de 2016</span><span class="sxs-lookup"><span data-stu-id="a6052-246">June 14, 2016</span></span> |--- |
| [<span data-ttu-id="a6052-247">1.7.0</span><span class="sxs-lookup"><span data-stu-id="a6052-247">1.7.0</span></span>](#1.7.0) |<span data-ttu-id="a6052-248">26 de Abril de 2016</span><span class="sxs-lookup"><span data-stu-id="a6052-248">April 26, 2016</span></span> |--- |
| [<span data-ttu-id="a6052-249">1.6.0</span><span class="sxs-lookup"><span data-stu-id="a6052-249">1.6.0</span></span>](#1.6.0) |<span data-ttu-id="a6052-250">29 de Março de 2016</span><span class="sxs-lookup"><span data-stu-id="a6052-250">March 29, 2016</span></span> |--- |
| [<span data-ttu-id="a6052-251">1.5.6</span><span class="sxs-lookup"><span data-stu-id="a6052-251">1.5.6</span></span>](#1.5.6) |<span data-ttu-id="a6052-252">08 de Março de 2016</span><span class="sxs-lookup"><span data-stu-id="a6052-252">March 08, 2016</span></span> |--- |
| [<span data-ttu-id="a6052-253">1.5.5</span><span class="sxs-lookup"><span data-stu-id="a6052-253">1.5.5</span></span>](#1.5.5) |<span data-ttu-id="a6052-254">02 de Fevereiro de 2016</span><span class="sxs-lookup"><span data-stu-id="a6052-254">February 02, 2016</span></span> |--- |
| [<span data-ttu-id="a6052-255">1.5.4</span><span class="sxs-lookup"><span data-stu-id="a6052-255">1.5.4</span></span>](#1.5.4) |<span data-ttu-id="a6052-256">01 de Fevereiro de 2016</span><span class="sxs-lookup"><span data-stu-id="a6052-256">February 01, 2016</span></span> |--- |
| [<span data-ttu-id="a6052-257">1.5.2</span><span class="sxs-lookup"><span data-stu-id="a6052-257">1.5.2</span></span>](#1.5.2) |<span data-ttu-id="a6052-258">26 de Janeiro de 2016</span><span class="sxs-lookup"><span data-stu-id="a6052-258">January 26, 2016</span></span> |--- |
| [<span data-ttu-id="a6052-259">1.5.2</span><span class="sxs-lookup"><span data-stu-id="a6052-259">1.5.2</span></span>](#1.5.2) |<span data-ttu-id="a6052-260">22 de Janeiro de 2016</span><span class="sxs-lookup"><span data-stu-id="a6052-260">January 22, 2016</span></span> |--- |
| [<span data-ttu-id="a6052-261">1.5.1</span><span class="sxs-lookup"><span data-stu-id="a6052-261">1.5.1</span></span>](#1.5.1) |<span data-ttu-id="a6052-262">4 de Janeiro de 2016</span><span class="sxs-lookup"><span data-stu-id="a6052-262">January 4, 2016</span></span> |--- |
| [<span data-ttu-id="a6052-263">1.5.0</span><span class="sxs-lookup"><span data-stu-id="a6052-263">1.5.0</span></span>](#1.5.0) |<span data-ttu-id="a6052-264">31 de Dezembro de 2015</span><span class="sxs-lookup"><span data-stu-id="a6052-264">December 31, 2015</span></span> |--- |
| [<span data-ttu-id="a6052-265">1.4.0</span><span class="sxs-lookup"><span data-stu-id="a6052-265">1.4.0</span></span>](#1.4.0) |<span data-ttu-id="a6052-266">06 de Outubro de 2015</span><span class="sxs-lookup"><span data-stu-id="a6052-266">October 06, 2015</span></span> |--- |
| [<span data-ttu-id="a6052-267">1.3.0</span><span class="sxs-lookup"><span data-stu-id="a6052-267">1.3.0</span></span>](#1.3.0) |<span data-ttu-id="a6052-268">06 de Outubro de 2015</span><span class="sxs-lookup"><span data-stu-id="a6052-268">October 06, 2015</span></span> |--- |
| [<span data-ttu-id="a6052-269">1.2.2</span><span class="sxs-lookup"><span data-stu-id="a6052-269">1.2.2</span></span>](#1.2.2) |<span data-ttu-id="a6052-270">10 de Setembro de 2015</span><span class="sxs-lookup"><span data-stu-id="a6052-270">September 10, 2015</span></span> |--- |
| [<span data-ttu-id="a6052-271">1.2.1</span><span class="sxs-lookup"><span data-stu-id="a6052-271">1.2.1</span></span>](#1.2.1) |<span data-ttu-id="a6052-272">15 de Agosto de 2015</span><span class="sxs-lookup"><span data-stu-id="a6052-272">August 15, 2015</span></span> |--- |
| [<span data-ttu-id="a6052-273">1.2.0</span><span class="sxs-lookup"><span data-stu-id="a6052-273">1.2.0</span></span>](#1.2.0) |<span data-ttu-id="a6052-274">05 de Agosto de 2015</span><span class="sxs-lookup"><span data-stu-id="a6052-274">August 05, 2015</span></span> |--- |
| [<span data-ttu-id="a6052-275">1.1.0</span><span class="sxs-lookup"><span data-stu-id="a6052-275">1.1.0</span></span>](#1.1.0) |<span data-ttu-id="a6052-276">09 de Julho de 2015</span><span class="sxs-lookup"><span data-stu-id="a6052-276">July 09, 2015</span></span> |--- |
| [<span data-ttu-id="a6052-277">1.0.3</span><span class="sxs-lookup"><span data-stu-id="a6052-277">1.0.3</span></span>](#1.0.3) |<span data-ttu-id="a6052-278">04 de Junho de 2015</span><span class="sxs-lookup"><span data-stu-id="a6052-278">June 04, 2015</span></span> |--- |
| [<span data-ttu-id="a6052-279">1.0.2</span><span class="sxs-lookup"><span data-stu-id="a6052-279">1.0.2</span></span>](#1.0.2) |<span data-ttu-id="a6052-280">23 de Maio de 2015</span><span class="sxs-lookup"><span data-stu-id="a6052-280">May 23, 2015</span></span> |--- |
| [<span data-ttu-id="a6052-281">1.0.1</span><span class="sxs-lookup"><span data-stu-id="a6052-281">1.0.1</span></span>](#1.0.1) |<span data-ttu-id="a6052-282">15 de Maio de 2015</span><span class="sxs-lookup"><span data-stu-id="a6052-282">May 15, 2015</span></span> |--- |
| [<span data-ttu-id="a6052-283">1.0.0</span><span class="sxs-lookup"><span data-stu-id="a6052-283">1.0.0</span></span>](#1.0.0) |<span data-ttu-id="a6052-284">08 de Abril de 2015</span><span class="sxs-lookup"><span data-stu-id="a6052-284">April 08, 2015</span></span> |--- |

## <a name="faq"></a><span data-ttu-id="a6052-285">FAQ</span><span class="sxs-lookup"><span data-stu-id="a6052-285">FAQ</span></span>
[!INCLUDE [cosmos-db-sdk-faq](../../includes/cosmos-db-sdk-faq.md)]

## <a name="see-also"></a><span data-ttu-id="a6052-286">Consultar também</span><span class="sxs-lookup"><span data-stu-id="a6052-286">See also</span></span>
<span data-ttu-id="a6052-287">toolearn mais informações sobre a base de dados do Cosmos, consulte [base de dados do Microsoft Azure Cosmos](https://azure.microsoft.com/services/cosmos-db/) página do serviço.</span><span class="sxs-lookup"><span data-stu-id="a6052-287">toolearn more about Cosmos DB, see [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) service page.</span></span>

