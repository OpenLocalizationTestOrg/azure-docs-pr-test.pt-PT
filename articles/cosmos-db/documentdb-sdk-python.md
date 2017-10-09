---
title: API de Python do Cosmos DB, aaaAzure SDK & recursos | Microsoft Docs
description: "Saiba tudo sobre Olá Python API e SDK, incluindo as datas de versão, datas de extinção e as alterações efetuadas entre cada versão do Olá SDK Python do Azure Cosmos DB."
services: cosmos-db
documentationcenter: python
author: rnagpal
manager: jhubbard
editor: cgronlun
ms.assetid: 3ac344a9-b2fa-4a3f-a4cc-02d287e05469
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 05/24/2017
ms.author: rnagpal
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 1a164b72d2bd819de87df0229357b82e2177af2f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-python-sdk-release-notes-and-resources"></a><span data-ttu-id="a6e3b-103">SDK de Python Cosmos BD do Azure: Notas de versão e recursos</span><span class="sxs-lookup"><span data-stu-id="a6e3b-103">Azure Cosmos DB Python SDK: Release notes and resources</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a6e3b-104">.NET</span><span class="sxs-lookup"><span data-stu-id="a6e3b-104">.NET</span></span>](documentdb-sdk-dotnet.md)
> * [<span data-ttu-id="a6e3b-105">Feed de alteração de .NET</span><span class="sxs-lookup"><span data-stu-id="a6e3b-105">.NET Change Feed</span></span>](documentdb-sdk-dotnet-changefeed.md)
> * [<span data-ttu-id="a6e3b-106">.NET Core</span><span class="sxs-lookup"><span data-stu-id="a6e3b-106">.NET Core</span></span>](documentdb-sdk-dotnet-core.md)
> * [<span data-ttu-id="a6e3b-107">Node.js</span><span class="sxs-lookup"><span data-stu-id="a6e3b-107">Node.js</span></span>](documentdb-sdk-node.md)
> * [<span data-ttu-id="a6e3b-108">Java</span><span class="sxs-lookup"><span data-stu-id="a6e3b-108">Java</span></span>](documentdb-sdk-java.md)
> * [<span data-ttu-id="a6e3b-109">Python</span><span class="sxs-lookup"><span data-stu-id="a6e3b-109">Python</span></span>](documentdb-sdk-python.md)
> * [<span data-ttu-id="a6e3b-110">REST</span><span class="sxs-lookup"><span data-stu-id="a6e3b-110">REST</span></span>](https://docs.microsoft.com/rest/api/documentdb/)
> * [<span data-ttu-id="a6e3b-111">Fornecedor de Recursos REST</span><span class="sxs-lookup"><span data-stu-id="a6e3b-111">REST Resource Provider</span></span>](https://docs.microsoft.com/rest/api/documentdbresourceprovider/)
> * [<span data-ttu-id="a6e3b-112">SQL</span><span class="sxs-lookup"><span data-stu-id="a6e3b-112">SQL</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx)
> 
> 

<table>

<tr><td><span data-ttu-id="a6e3b-113">**Transferir o SDK**</span><span class="sxs-lookup"><span data-stu-id="a6e3b-113">**Download SDK**</span></span></td><td>[<span data-ttu-id="a6e3b-114">PyPI</span><span class="sxs-lookup"><span data-stu-id="a6e3b-114">PyPI</span></span>](https://pypi.python.org/pypi/pydocumentdb)</td></tr>

<tr><td><span data-ttu-id="a6e3b-115">**Documentação da API**</span><span class="sxs-lookup"><span data-stu-id="a6e3b-115">**API documentation**</span></span></td><td>[<span data-ttu-id="a6e3b-116">Documentação de referência da API de Python</span><span class="sxs-lookup"><span data-stu-id="a6e3b-116">Python API reference documentation</span></span>](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.html)</td></tr>

<tr><td><span data-ttu-id="a6e3b-117">**Instruções de instalação do SDK**</span><span class="sxs-lookup"><span data-stu-id="a6e3b-117">**SDK installation instructions**</span></span></td><td>[<span data-ttu-id="a6e3b-118">Instruções de instalação do Python SDK</span><span class="sxs-lookup"><span data-stu-id="a6e3b-118">Python SDK installation instructions</span></span>](http://azure.github.io/azure-documentdb-python/)</td></tr>

<tr><td><span data-ttu-id="a6e3b-119">**Contribuir tooSDK**</span><span class="sxs-lookup"><span data-stu-id="a6e3b-119">**Contribute tooSDK**</span></span></td><td>[<span data-ttu-id="a6e3b-120">GitHub</span><span class="sxs-lookup"><span data-stu-id="a6e3b-120">GitHub</span></span>](https://github.com/Azure/azure-documentdb-python)</td></tr>

<tr><td><span data-ttu-id="a6e3b-121">**Introdução**</span><span class="sxs-lookup"><span data-stu-id="a6e3b-121">**Get started**</span></span></td><td>[<span data-ttu-id="a6e3b-122">Introdução ao hello Python SDK</span><span class="sxs-lookup"><span data-stu-id="a6e3b-122">Get started with hello Python SDK</span></span>](documentdb-python-application.md)</td></tr>

<tr><td><span data-ttu-id="a6e3b-123">**Plataforma suportada atual**</span><span class="sxs-lookup"><span data-stu-id="a6e3b-123">**Current supported platform**</span></span></td><td><span data-ttu-id="a6e3b-124">[Python 2.7](https://www.python.org/downloads/) e [Python 3.5](https://www.python.org/downloads/)</span><span class="sxs-lookup"><span data-stu-id="a6e3b-124">[Python 2.7](https://www.python.org/downloads/) and [Python 3.5](https://www.python.org/downloads/)</span></span></td></tr>
</table></br>

## <a name="release-notes"></a><span data-ttu-id="a6e3b-125">Notas de versão</span><span class="sxs-lookup"><span data-stu-id="a6e3b-125">Release notes</span></span>
### <a name="a-name220220"></a><span data-ttu-id="a6e3b-126"><a name="2.2.0"/>2.2.0</span><span class="sxs-lookup"><span data-stu-id="a6e3b-126"><a name="2.2.0"/>2.2.0</span></span>
* <span data-ttu-id="a6e3b-127">Suporte adicionado para um novo nível de consistência chamado ConsistentPrefix.</span><span class="sxs-lookup"><span data-stu-id="a6e3b-127">Added support for a new consistency level called ConsistentPrefix.</span></span>


### <a name="a-name210210"></a><span data-ttu-id="a6e3b-128"><a name="2.1.0"/>2.1.0</span><span class="sxs-lookup"><span data-stu-id="a6e3b-128"><a name="2.1.0"/>2.1.0</span></span>
* <span data-ttu-id="a6e3b-129">Suporte adicionado para consultas de agregação (CONTAGEM, MIN, MAX, soma e média).</span><span class="sxs-lookup"><span data-stu-id="a6e3b-129">Added support for aggregation queries (COUNT, MIN, MAX, SUM, and AVG).</span></span>
* <span data-ttu-id="a6e3b-130">Adicionar uma opção para desativar a verificação de SSL quando em execução contra o emulador de BD do Cosmos.</span><span class="sxs-lookup"><span data-stu-id="a6e3b-130">Added an option for disabling SSL verification when running against Cosmos DB Emulator.</span></span>
* <span data-ttu-id="a6e3b-131">Remover a restrição de Olá do módulo de pedidos dependentes toobe 2.10.0 exatamente.</span><span class="sxs-lookup"><span data-stu-id="a6e3b-131">Removed hello restriction of dependent requests module toobe exactly 2.10.0.</span></span>
* <span data-ttu-id="a6e3b-132">Lowered débito mínimo em coleções particionadas de 10,100 RU/s too2500 RU/s.</span><span class="sxs-lookup"><span data-stu-id="a6e3b-132">Lowered minimum throughput on partitioned collections from 10,100 RU/s too2500 RU/s.</span></span>
* <span data-ttu-id="a6e3b-133">Suporte adicionado para ativar o registo de script durante a execução do procedimento armazenado.</span><span class="sxs-lookup"><span data-stu-id="a6e3b-133">Added support for enabling script logging during stored procedure execution.</span></span>
* <span data-ttu-id="a6e3b-134">Versão de REST API demasiado bumped'2017-01-19' com esta versão.</span><span class="sxs-lookup"><span data-stu-id="a6e3b-134">REST API version bumped too'2017-01-19' with this release.</span></span>

### <a name="a-name201201"></a><span data-ttu-id="a6e3b-135"><a name="2.0.1"/>2.0.1</span><span class="sxs-lookup"><span data-stu-id="a6e3b-135"><a name="2.0.1"/>2.0.1</span></span>
* <span data-ttu-id="a6e3b-136">Efetuou alterações editoriais toodocumentation comentários.</span><span class="sxs-lookup"><span data-stu-id="a6e3b-136">Made editorial changes toodocumentation comments.</span></span>

### <a name="a-name200200"></a><span data-ttu-id="a6e3b-137"><a name="2.0.0"/>2.0.0</span><span class="sxs-lookup"><span data-stu-id="a6e3b-137"><a name="2.0.0"/>2.0.0</span></span>
* <span data-ttu-id="a6e3b-138">Suporte adicionado para o Python 3.5.</span><span class="sxs-lookup"><span data-stu-id="a6e3b-138">Added support for Python 3.5.</span></span>
* <span data-ttu-id="a6e3b-139">Suporte adicionado para utilizar um módulo de pedidos de agrupamento de ligações.</span><span class="sxs-lookup"><span data-stu-id="a6e3b-139">Added support for connection pooling using a requests module.</span></span>
* <span data-ttu-id="a6e3b-140">Adicionado suporte para a consistência de sessão.</span><span class="sxs-lookup"><span data-stu-id="a6e3b-140">Added support for session consistency.</span></span>
* <span data-ttu-id="a6e3b-141">Suporte adicionado para consultas de parte superior/ORDERBY para coleções particionadas.</span><span class="sxs-lookup"><span data-stu-id="a6e3b-141">Added support for TOP/ORDERBY queries for partitioned collections.</span></span>

### <a name="a-name190190"></a><span data-ttu-id="a6e3b-142"><a name="1.9.0"/>1.9.0</span><span class="sxs-lookup"><span data-stu-id="a6e3b-142"><a name="1.9.0"/>1.9.0</span></span>
* <span data-ttu-id="a6e3b-143">Suporte de política de repetição adicionado para pedidos otimizados.</span><span class="sxs-lookup"><span data-stu-id="a6e3b-143">Added retry policy support for throttled requests.</span></span> <span data-ttu-id="a6e3b-144">(Pedidos otimizados recebem uma pedido taxa demasiado grande exceção, o código de erro 429.) Por predefinição, base de dados do Azure Cosmos repete nove vezes para cada pedido quando for detetado o código de erro 429, para respeitar o tempo de retryAfter Olá no cabeçalho de resposta de Olá.</span><span class="sxs-lookup"><span data-stu-id="a6e3b-144">(Throttled requests receive a request rate too large exception, error code 429.) By default, Azure Cosmos DB retries nine times for each request when error code 429 is encountered, honoring hello retryAfter time in hello response header.</span></span> <span data-ttu-id="a6e3b-145">Um período de tempo do intervalo de repetição fixo pode agora ser definido como parte da Olá RetryOptions propriedade no objecto de ConnectionPolicy Olá se pretender que o tempo de retryAfter tooignore Olá devolvido pelo servidor entre repetições Olá.</span><span class="sxs-lookup"><span data-stu-id="a6e3b-145">A fixed retry interval time can now be set as part of hello RetryOptions property on hello ConnectionPolicy object if you want tooignore hello retryAfter time returned by server between hello retries.</span></span> <span data-ttu-id="a6e3b-146">BD do Azure do Cosmos aguarda agora um máximo de 30 segundos para cada pedido que está a ser limitado (independentemente da contagem de repetições) e devolve a resposta de Olá com o código de erro 429.</span><span class="sxs-lookup"><span data-stu-id="a6e3b-146">Azure Cosmos DB now waits for a maximum of 30 seconds for each request that is being throttled (irrespective of retry count) and returns hello response with error code 429.</span></span> <span data-ttu-id="a6e3b-147">Neste momento também pode ser substituída no Olá RetryOptions propriedade ConnectionPolicy objeto.</span><span class="sxs-lookup"><span data-stu-id="a6e3b-147">This time can also be overriden in hello RetryOptions property on ConnectionPolicy object.</span></span>
* <span data-ttu-id="a6e3b-148">BD do cosmos devolve agora x-ms-limitação--contagem de repetições e x-ms-throttle-retry-wait-time-ms como cabeçalhos de resposta de Olá em cada limitação do pedido toodenote Olá Repetir contagem e Olá cummulative tempo do pedido Olá aguardaram entre repetições Olá.</span><span class="sxs-lookup"><span data-stu-id="a6e3b-148">Cosmos DB now returns x-ms-throttle-retry-count and x-ms-throttle-retry-wait-time-ms as hello response headers in every request toodenote hello throttle retry count and hello cummulative time hello request waited between hello retries.</span></span>
* <span data-ttu-id="a6e3b-149">Classe de RetryPolicy Olá removido propriedade correspondente da Olá (retry_policy) exposta na classe de document_client Olá e introduzidas em vez disso, uma classe de RetryOptions exposição de propriedade de RetryOptions Olá na classe ConnectionPolicy que pode ser utilizado toooverride Alguns dos predefinido Olá as opções de repetição.</span><span class="sxs-lookup"><span data-stu-id="a6e3b-149">Removed hello RetryPolicy class and hello corresponding property (retry_policy) exposed on hello document_client class and instead introduced a RetryOptions class exposing hello RetryOptions property on ConnectionPolicy class that can be used toooverride some of hello default retry options.</span></span>

### <a name="a-name180180"></a><span data-ttu-id="a6e3b-150"><a name="1.8.0"/>1.8.0</span><span class="sxs-lookup"><span data-stu-id="a6e3b-150"><a name="1.8.0"/>1.8.0</span></span>
* <span data-ttu-id="a6e3b-151">Suporte adicionado Olá para contas de multirregião base de dados.</span><span class="sxs-lookup"><span data-stu-id="a6e3b-151">Added hello support for multi-region database accounts.</span></span>

### <a name="a-name170170"></a><span data-ttu-id="a6e3b-152"><a name="1.7.0"/>1.7.0</span><span class="sxs-lookup"><span data-stu-id="a6e3b-152"><a name="1.7.0"/>1.7.0</span></span>
* <span data-ttu-id="a6e3b-153">Olá adicionado suporte para a funcionalidade de tooLive(TTL) de tempo para documentos.</span><span class="sxs-lookup"><span data-stu-id="a6e3b-153">Added hello support for Time tooLive(TTL) feature for documents.</span></span>

### <a name="a-name161161"></a><span data-ttu-id="a6e3b-154"><a name="1.6.1"/>1.6.1</span><span class="sxs-lookup"><span data-stu-id="a6e3b-154"><a name="1.6.1"/>1.6.1</span></span>
* <span data-ttu-id="a6e3b-155">Correções de erros relacionados com o lado tooserver tooallow carateres especiais no caminho de partitionkey de criação de partições.</span><span class="sxs-lookup"><span data-stu-id="a6e3b-155">Bug fixes related tooserver side partitioning tooallow special characters in partitionkey path.</span></span>

### <a name="a-name160160"></a><span data-ttu-id="a6e3b-156"><a name="1.6.0"/>1.6.0</span><span class="sxs-lookup"><span data-stu-id="a6e3b-156"><a name="1.6.0"/>1.6.0</span></span>
* <span data-ttu-id="a6e3b-157">Implementado [particionada coleções](partition-data.md) e [níveis de desempenho definido pelo utilizador](performance-levels.md).</span><span class="sxs-lookup"><span data-stu-id="a6e3b-157">Implemented [partitioned collections](partition-data.md) and [user-defined performance levels](performance-levels.md).</span></span> 

### <a name="a-name150150"></a><span data-ttu-id="a6e3b-158"><a name="1.5.0"/>1.5.0</span><span class="sxs-lookup"><span data-stu-id="a6e3b-158"><a name="1.5.0"/>1.5.0</span></span>
* <span data-ttu-id="a6e3b-159">Adicionar Hash & intervalo de partição resoluções tooassist com as aplicações de fragmentação através de várias partições.</span><span class="sxs-lookup"><span data-stu-id="a6e3b-159">Add Hash & Range partition resolvers tooassist with sharding applications across multiple partitions.</span></span>

### <a name="a-name142142"></a><span data-ttu-id="a6e3b-160"><a name="1.4.2"/>1.4.2</span><span class="sxs-lookup"><span data-stu-id="a6e3b-160"><a name="1.4.2"/>1.4.2</span></span>
* <span data-ttu-id="a6e3b-161">Implemente Upsert.</span><span class="sxs-lookup"><span data-stu-id="a6e3b-161">Implement Upsert.</span></span> <span data-ttu-id="a6e3b-162">Novos métodos de UpsertXXX adicionado toosupport Upsert funcionalidade.</span><span class="sxs-lookup"><span data-stu-id="a6e3b-162">New UpsertXXX methods added toosupport Upsert feature.</span></span>
* <span data-ttu-id="a6e3b-163">ID de implementar baseado Routing.</span><span class="sxs-lookup"><span data-stu-id="a6e3b-163">Implement ID Based Routing.</span></span> <span data-ttu-id="a6e3b-164">Sem alterações de API públicas, todas as alterações internas.</span><span class="sxs-lookup"><span data-stu-id="a6e3b-164">No public API changes, all changes internal.</span></span>

### <a name="a-name120120"></a><span data-ttu-id="a6e3b-165"><a name="1.2.0"/>1.2.0</span><span class="sxs-lookup"><span data-stu-id="a6e3b-165"><a name="1.2.0"/>1.2.0</span></span>
* <span data-ttu-id="a6e3b-166">Índice de Geoespacial suporta.</span><span class="sxs-lookup"><span data-stu-id="a6e3b-166">Supports GeoSpatial index.</span></span>
* <span data-ttu-id="a6e3b-167">Valida a propriedade id de todos os recursos.</span><span class="sxs-lookup"><span data-stu-id="a6e3b-167">Validates id property for all resources.</span></span> <span data-ttu-id="a6e3b-168">Os IDs de recursos não podem conter?, /, #, \, carateres nem terminar com um espaço.</span><span class="sxs-lookup"><span data-stu-id="a6e3b-168">Ids for resources cannot contain ?, /, #, \, characters or end with a space.</span></span>
* <span data-ttu-id="a6e3b-169">Adiciona tooResourceResponse de "progresso de transformação de índice" do novo cabeçalho.</span><span class="sxs-lookup"><span data-stu-id="a6e3b-169">Adds new header "index transformation progress" tooResourceResponse.</span></span>

### <a name="a-name110110"></a><span data-ttu-id="a6e3b-170"><a name="1.1.0"/>1.1.0</span><span class="sxs-lookup"><span data-stu-id="a6e3b-170"><a name="1.1.0"/>1.1.0</span></span>
* <span data-ttu-id="a6e3b-171">Implementa a política de indexação V2.</span><span class="sxs-lookup"><span data-stu-id="a6e3b-171">Implements V2 indexing policy.</span></span>

### <a name="a-name101101"></a><span data-ttu-id="a6e3b-172"><a name="1.0.1"/>1.0.1</span><span class="sxs-lookup"><span data-stu-id="a6e3b-172"><a name="1.0.1"/>1.0.1</span></span>
* <span data-ttu-id="a6e3b-173">Suporta a ligação de proxy.</span><span class="sxs-lookup"><span data-stu-id="a6e3b-173">Supports proxy connection.</span></span>

### <a name="a-name100100"></a><span data-ttu-id="a6e3b-174"><a name="1.0.0"/>1.0.0</span><span class="sxs-lookup"><span data-stu-id="a6e3b-174"><a name="1.0.0"/>1.0.0</span></span>
* <span data-ttu-id="a6e3b-175">GA SDK.</span><span class="sxs-lookup"><span data-stu-id="a6e3b-175">GA SDK.</span></span>

## <a name="release--retirement-dates"></a><span data-ttu-id="a6e3b-176">Versão & extinção datas</span><span class="sxs-lookup"><span data-stu-id="a6e3b-176">Release & retirement dates</span></span>
<span data-ttu-id="a6e3b-177">A Microsoft vai fornecer pelo menos notificação **12 meses** previamente extinguir um SDK na ordem toosmooth Olá transição tooa/suportada mais recente versão.</span><span class="sxs-lookup"><span data-stu-id="a6e3b-177">Microsoft will provide notification at least **12 months** in advance of retiring an SDK in order toosmooth hello transition tooa newer/supported version.</span></span>

<span data-ttu-id="a6e3b-178">Apenas são adicionadas novas funcionalidades e a funcionalidade e otimizações o atual toohello SDK, como tal, é recomendado que lhe toohello sempre atualização mais recente versão do SDK antecipadamente quanto possível.</span><span class="sxs-lookup"><span data-stu-id="a6e3b-178">New features and functionality and optimizations are only added toohello current SDK, as such it is  recommend that you always upgrade toohello latest SDK version as early as possible.</span></span> 

<span data-ttu-id="a6e3b-179">Qualquer tooCosmos pedido BD utilizando um SDK extinto serão rejeitadas pelo serviço de Olá.</span><span class="sxs-lookup"><span data-stu-id="a6e3b-179">Any request tooCosmos DB using a retired SDK will be rejected by hello service.</span></span>

> [!WARNING]
> <span data-ttu-id="a6e3b-180">Todas as versões do Olá SDK do Azure DocumentDB para tooversion anterior Python **1.0.0** serão descontinuados no **29 de Fevereiro de 2016**.</span><span class="sxs-lookup"><span data-stu-id="a6e3b-180">All versions of hello Azure DocumentDB SDK for Python prior tooversion **1.0.0** will be retired on **February 29, 2016**.</span></span> 
> 
> 

<br/>

| <span data-ttu-id="a6e3b-181">Versão</span><span class="sxs-lookup"><span data-stu-id="a6e3b-181">Version</span></span> | <span data-ttu-id="a6e3b-182">Data da versão</span><span class="sxs-lookup"><span data-stu-id="a6e3b-182">Release Date</span></span> | <span data-ttu-id="a6e3b-183">Data de retirada</span><span class="sxs-lookup"><span data-stu-id="a6e3b-183">Retirement Date</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="a6e3b-184">2.2.0</span><span class="sxs-lookup"><span data-stu-id="a6e3b-184">2.2.0</span></span>](#2.2.0) |<span data-ttu-id="a6e3b-185">10 de maio de 2017</span><span class="sxs-lookup"><span data-stu-id="a6e3b-185">May 10, 2017</span></span> |--- |
| [<span data-ttu-id="a6e3b-186">2.1.0</span><span class="sxs-lookup"><span data-stu-id="a6e3b-186">2.1.0</span></span>](#2.1.0) |<span data-ttu-id="a6e3b-187">01 de Maio de 2017</span><span class="sxs-lookup"><span data-stu-id="a6e3b-187">May 01, 2017</span></span> |--- |
| [<span data-ttu-id="a6e3b-188">2.0.1</span><span class="sxs-lookup"><span data-stu-id="a6e3b-188">2.0.1</span></span>](#2.0.1) |<span data-ttu-id="a6e3b-189">30 de Outubro de 2016</span><span class="sxs-lookup"><span data-stu-id="a6e3b-189">October 30, 2016</span></span> |--- |
| [<span data-ttu-id="a6e3b-190">2.0.0</span><span class="sxs-lookup"><span data-stu-id="a6e3b-190">2.0.0</span></span>](#2.0.0) |<span data-ttu-id="a6e3b-191">29 de Setembro de 2016</span><span class="sxs-lookup"><span data-stu-id="a6e3b-191">September 29, 2016</span></span> |--- |
| [<span data-ttu-id="a6e3b-192">1.9.0</span><span class="sxs-lookup"><span data-stu-id="a6e3b-192">1.9.0</span></span>](#1.9.0) |<span data-ttu-id="a6e3b-193">07 de Julho de 2016</span><span class="sxs-lookup"><span data-stu-id="a6e3b-193">July 07, 2016</span></span> |--- |
| [<span data-ttu-id="a6e3b-194">1.8.0</span><span class="sxs-lookup"><span data-stu-id="a6e3b-194">1.8.0</span></span>](#1.8.0) |<span data-ttu-id="a6e3b-195">14 de Junho de 2016</span><span class="sxs-lookup"><span data-stu-id="a6e3b-195">June 14, 2016</span></span> |--- |
| [<span data-ttu-id="a6e3b-196">1.7.0</span><span class="sxs-lookup"><span data-stu-id="a6e3b-196">1.7.0</span></span>](#1.7.0) |<span data-ttu-id="a6e3b-197">26 de Abril de 2016</span><span class="sxs-lookup"><span data-stu-id="a6e3b-197">April 26, 2016</span></span> |--- |
| [<span data-ttu-id="a6e3b-198">1.6.1</span><span class="sxs-lookup"><span data-stu-id="a6e3b-198">1.6.1</span></span>](#1.6.1) |<span data-ttu-id="a6e3b-199">08 de Abril de 2016</span><span class="sxs-lookup"><span data-stu-id="a6e3b-199">April 08, 2016</span></span> |--- |
| [<span data-ttu-id="a6e3b-200">1.6.0</span><span class="sxs-lookup"><span data-stu-id="a6e3b-200">1.6.0</span></span>](#1.6.0) |<span data-ttu-id="a6e3b-201">29 de Março de 2016</span><span class="sxs-lookup"><span data-stu-id="a6e3b-201">March 29, 2016</span></span> |--- |
| [<span data-ttu-id="a6e3b-202">1.5.0</span><span class="sxs-lookup"><span data-stu-id="a6e3b-202">1.5.0</span></span>](#1.5.0) |<span data-ttu-id="a6e3b-203">03 de Janeiro de 2016</span><span class="sxs-lookup"><span data-stu-id="a6e3b-203">January 03, 2016</span></span> |--- |
| [<span data-ttu-id="a6e3b-204">1.4.2</span><span class="sxs-lookup"><span data-stu-id="a6e3b-204">1.4.2</span></span>](#1.4.2) |<span data-ttu-id="a6e3b-205">06 de Outubro de 2015</span><span class="sxs-lookup"><span data-stu-id="a6e3b-205">October 06, 2015</span></span> |--- |
| [<span data-ttu-id="a6e3b-206">1.4.1</span><span class="sxs-lookup"><span data-stu-id="a6e3b-206">1.4.1</span></span>](#1.4.1) |<span data-ttu-id="a6e3b-207">06 de Outubro de 2015</span><span class="sxs-lookup"><span data-stu-id="a6e3b-207">October 06, 2015</span></span> |--- |
| [<span data-ttu-id="a6e3b-208">1.2.0</span><span class="sxs-lookup"><span data-stu-id="a6e3b-208">1.2.0</span></span>](#1.2.0) |<span data-ttu-id="a6e3b-209">06 de Agosto de 2015</span><span class="sxs-lookup"><span data-stu-id="a6e3b-209">August 06, 2015</span></span> |--- |
| [<span data-ttu-id="a6e3b-210">1.1.0</span><span class="sxs-lookup"><span data-stu-id="a6e3b-210">1.1.0</span></span>](#1.1.0) |<span data-ttu-id="a6e3b-211">09 de Julho de 2015</span><span class="sxs-lookup"><span data-stu-id="a6e3b-211">July 09, 2015</span></span> |--- |
| [<span data-ttu-id="a6e3b-212">1.0.1</span><span class="sxs-lookup"><span data-stu-id="a6e3b-212">1.0.1</span></span>](#1.0.1) |<span data-ttu-id="a6e3b-213">25 de Maio de 2015</span><span class="sxs-lookup"><span data-stu-id="a6e3b-213">May 25, 2015</span></span> |--- |
| [<span data-ttu-id="a6e3b-214">1.0.0</span><span class="sxs-lookup"><span data-stu-id="a6e3b-214">1.0.0</span></span>](#1.0.0) |<span data-ttu-id="a6e3b-215">07 de Abril de 2015</span><span class="sxs-lookup"><span data-stu-id="a6e3b-215">April 07, 2015</span></span> |--- |
| <span data-ttu-id="a6e3b-216">0.9.4-prelease</span><span class="sxs-lookup"><span data-stu-id="a6e3b-216">0.9.4-prelease</span></span> |<span data-ttu-id="a6e3b-217">14 de Janeiro de 2015</span><span class="sxs-lookup"><span data-stu-id="a6e3b-217">January 14, 2015</span></span> |<span data-ttu-id="a6e3b-218">29 de Fevereiro de 2016</span><span class="sxs-lookup"><span data-stu-id="a6e3b-218">February 29, 2016</span></span> |
| <span data-ttu-id="a6e3b-219">0.9.3-prelease</span><span class="sxs-lookup"><span data-stu-id="a6e3b-219">0.9.3-prelease</span></span> |<span data-ttu-id="a6e3b-220">09 de Dezembro de 2014</span><span class="sxs-lookup"><span data-stu-id="a6e3b-220">December 09, 2014</span></span> |<span data-ttu-id="a6e3b-221">29 de Fevereiro de 2016</span><span class="sxs-lookup"><span data-stu-id="a6e3b-221">February 29, 2016</span></span> |
| <span data-ttu-id="a6e3b-222">0.9.2-prelease</span><span class="sxs-lookup"><span data-stu-id="a6e3b-222">0.9.2-prelease</span></span> |<span data-ttu-id="a6e3b-223">25 de Novembro de 2014</span><span class="sxs-lookup"><span data-stu-id="a6e3b-223">November 25, 2014</span></span> |<span data-ttu-id="a6e3b-224">29 de Fevereiro de 2016</span><span class="sxs-lookup"><span data-stu-id="a6e3b-224">February 29, 2016</span></span> |
| <span data-ttu-id="a6e3b-225">0.9.1-prelease</span><span class="sxs-lookup"><span data-stu-id="a6e3b-225">0.9.1-prelease</span></span> |<span data-ttu-id="a6e3b-226">23 de Setembro de 2014</span><span class="sxs-lookup"><span data-stu-id="a6e3b-226">September 23, 2014</span></span> |<span data-ttu-id="a6e3b-227">29 de Fevereiro de 2016</span><span class="sxs-lookup"><span data-stu-id="a6e3b-227">February 29, 2016</span></span> |
| <span data-ttu-id="a6e3b-228">0.9.0-prelease</span><span class="sxs-lookup"><span data-stu-id="a6e3b-228">0.9.0-prelease</span></span> |<span data-ttu-id="a6e3b-229">21 de Agosto de 2014</span><span class="sxs-lookup"><span data-stu-id="a6e3b-229">August 21, 2014</span></span> |<span data-ttu-id="a6e3b-230">29 de Fevereiro de 2016</span><span class="sxs-lookup"><span data-stu-id="a6e3b-230">February 29, 2016</span></span> |

## <a name="faq"></a><span data-ttu-id="a6e3b-231">FAQ</span><span class="sxs-lookup"><span data-stu-id="a6e3b-231">FAQ</span></span>
[!INCLUDE [cosmos-db-sdk-faq](../../includes/cosmos-db-sdk-faq.md)]

## <a name="see-also"></a><span data-ttu-id="a6e3b-232">Consultar também</span><span class="sxs-lookup"><span data-stu-id="a6e3b-232">See also</span></span>
<span data-ttu-id="a6e3b-233">toolearn mais informações sobre a base de dados do Cosmos, consulte [base de dados do Microsoft Azure Cosmos](https://azure.microsoft.com/services/cosmos-db/) página do serviço.</span><span class="sxs-lookup"><span data-stu-id="a6e3b-233">toolearn more about Cosmos DB, see [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) service page.</span></span> 

