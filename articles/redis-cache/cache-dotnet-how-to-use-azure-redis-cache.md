---
title: aaaHow tooUse a Cache de Redis do Azure | Microsoft Docs
description: "Saiba como tooimprove Olá desempenho das aplicações do Azure com a Cache de Redis do Azure"
services: redis-cache,app-service
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: c502f74c-44de-4087-8303-1b1f43da12d5
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 07/27/2017
ms.author: sdanie
ms.openlocfilehash: 763d70c10972eec9a1885969e8da5bf1c4084727
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-redis-cache"></a><span data-ttu-id="bb150-103">Como tooUse do Azure da Cache de Redis</span><span class="sxs-lookup"><span data-stu-id="bb150-103">How tooUse Azure Redis Cache</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="bb150-104">.NET</span><span class="sxs-lookup"><span data-stu-id="bb150-104">.NET</span></span>](cache-dotnet-how-to-use-azure-redis-cache.md)
> * [<span data-ttu-id="bb150-105">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="bb150-105">ASP.NET</span></span>](cache-web-app-howto.md)
> * [<span data-ttu-id="bb150-106">Node.js</span><span class="sxs-lookup"><span data-stu-id="bb150-106">Node.js</span></span>](cache-nodejs-get-started.md)
> * [<span data-ttu-id="bb150-107">Java</span><span class="sxs-lookup"><span data-stu-id="bb150-107">Java</span></span>](cache-java-get-started.md)
> * [<span data-ttu-id="bb150-108">python</span><span class="sxs-lookup"><span data-stu-id="bb150-108">Python</span></span>](cache-python-get-started.md)
> 
> 

<span data-ttu-id="bb150-109">Este guia mostra como tooget iniciado utilizando **a Cache de Redis do Azure**.</span><span class="sxs-lookup"><span data-stu-id="bb150-109">This guide shows you how tooget started using **Azure Redis Cache**.</span></span> <span data-ttu-id="bb150-110">Cache de Redis do Microsoft Azure baseia Olá populares open source para a Cache de Redis.</span><span class="sxs-lookup"><span data-stu-id="bb150-110">Microsoft Azure Redis Cache is based on hello popular open source Redis Cache.</span></span> <span data-ttu-id="bb150-111">Dá-lhe aceder tooa segura, dedicada cache de Redis e gerida pela Microsoft.</span><span class="sxs-lookup"><span data-stu-id="bb150-111">It gives you access tooa secure, dedicated Redis cache, managed by Microsoft.</span></span> <span data-ttu-id="bb150-112">Pode aceder a uma cache criada com a Cache de Redis do Azure a partir de qualquer aplicação dentro do Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="bb150-112">A cache created using Azure Redis Cache is accessible from any application within Microsoft Azure.</span></span>

<span data-ttu-id="bb150-113">Cache de Redis do Microsoft Azure está disponível no Olá seguintes escalões:</span><span class="sxs-lookup"><span data-stu-id="bb150-113">Microsoft Azure Redis Cache is available in hello following tiers:</span></span>

* <span data-ttu-id="bb150-114">**Básico** – Único nó.</span><span class="sxs-lookup"><span data-stu-id="bb150-114">**Basic** – Single node.</span></span> <span data-ttu-id="bb150-115">Vários tamanhos segurança too53 GB.</span><span class="sxs-lookup"><span data-stu-id="bb150-115">Multiple sizes up too53 GB.</span></span>
* <span data-ttu-id="bb150-116">**Standard** – Dois nós Primário/Réplica.</span><span class="sxs-lookup"><span data-stu-id="bb150-116">**Standard** – Two-node Primary/Replica.</span></span> <span data-ttu-id="bb150-117">Vários tamanhos segurança too53 GB.</span><span class="sxs-lookup"><span data-stu-id="bb150-117">Multiple sizes up too53 GB.</span></span> <span data-ttu-id="bb150-118">SLA de 99,9%.</span><span class="sxs-lookup"><span data-stu-id="bb150-118">99.9% SLA.</span></span>
* <span data-ttu-id="bb150-119">**Premium** – dois nós primário/réplica com segurança too10 shards.</span><span class="sxs-lookup"><span data-stu-id="bb150-119">**Premium** – Two-node Primary/Replica with up too10 shards.</span></span> <span data-ttu-id="bb150-120">Vários tamanhos entre 6 GB too530 GB.</span><span class="sxs-lookup"><span data-stu-id="bb150-120">Multiple sizes from 6 GB too530 GB.</span></span> <span data-ttu-id="bb150-121">Todas as funcionalidades do escalão Standard e mais, incluindo o suporte para o [Cluster de Redis](cache-how-to-premium-clustering.md), a [Persistência de Redis](cache-how-to-premium-persistence.md) e a [Azure Virtual Network](cache-how-to-premium-vnet.md).</span><span class="sxs-lookup"><span data-stu-id="bb150-121">All Standard tier features and more including support for [Redis cluster](cache-how-to-premium-clustering.md), [Redis persistence](cache-how-to-premium-persistence.md), and [Azure Virtual Network](cache-how-to-premium-vnet.md).</span></span> <span data-ttu-id="bb150-122">SLA de 99,9%.</span><span class="sxs-lookup"><span data-stu-id="bb150-122">99.9% SLA.</span></span>

<span data-ttu-id="bb150-123">Cada escalão difere em termos de funcionalidades e preços.</span><span class="sxs-lookup"><span data-stu-id="bb150-123">Each tier differs in terms of features and pricing.</span></span> <span data-ttu-id="bb150-124">Para obter informações sobre os preços, veja [Cache Pricing Details (Detalhes dos Preços da Cache)][Cache Pricing Details].</span><span class="sxs-lookup"><span data-stu-id="bb150-124">For information on pricing, see [Cache Pricing Details][Cache Pricing Details].</span></span>

<span data-ttu-id="bb150-125">Este guia mostra como toouse Olá [stackexchange. redis] [ StackExchange.Redis] cliente utilizando C\# código.</span><span class="sxs-lookup"><span data-stu-id="bb150-125">This guide shows you how toouse hello [StackExchange.Redis][StackExchange.Redis] client using C\# code.</span></span> <span data-ttu-id="bb150-126">Olá os cenários abrangidos incluem **criar e configurar uma cache**, **configurar clientes de cache**, e **adição e remoção de objetos da cache de Olá**.</span><span class="sxs-lookup"><span data-stu-id="bb150-126">hello scenarios covered include **creating and configuring a cache**, **configuring cache clients**, and **adding and removing objects from hello cache**.</span></span> <span data-ttu-id="bb150-127">Para obter mais informações sobre como utilizar a Cache de Redis do Azure, veja [Next Steps (Passos Seguintes)][Next Steps].</span><span class="sxs-lookup"><span data-stu-id="bb150-127">For more information on using Azure Redis Cache, see [Next Steps][Next Steps].</span></span> <span data-ttu-id="bb150-128">Para um tutorial passo a passo para criar uma ASP.NET MVC aplicação web com a Cache de Redis, consulte [como toocreate uma aplicação Web com a Cache de Redis](cache-web-app-howto.md).</span><span class="sxs-lookup"><span data-stu-id="bb150-128">For a step-by-step tutorial of building an ASP.NET MVC web app with Redis Cache, see [How toocreate a Web App with Redis Cache](cache-web-app-howto.md).</span></span>

<a name="getting-started-cache-service"></a>

## <a name="get-started-with-azure-redis-cache"></a><span data-ttu-id="bb150-129">Introdução à Cache de Redis do Azure </span><span class="sxs-lookup"><span data-stu-id="bb150-129">Get Started with Azure Redis Cache</span></span>
<span data-ttu-id="bb150-130">É fácil começar a trabalhar com a Cache de Redis do Azure.</span><span class="sxs-lookup"><span data-stu-id="bb150-130">Getting started with Azure Redis Cache is easy.</span></span> <span data-ttu-id="bb150-131">tooget iniciado, pode aprovisionar e configurar uma cache.</span><span class="sxs-lookup"><span data-stu-id="bb150-131">tooget started, you provision and configure a cache.</span></span> <span data-ttu-id="bb150-132">Em seguida, configure os clientes de cache Olá para que podem aceder a cache de Olá.</span><span class="sxs-lookup"><span data-stu-id="bb150-132">Next, you configure hello cache clients so they can access hello cache.</span></span> <span data-ttu-id="bb150-133">Assim que os clientes de cache Olá estiverem configurados, pode começar a trabalhar com eles.</span><span class="sxs-lookup"><span data-stu-id="bb150-133">Once hello cache clients are configured, you can begin working with them.</span></span>

* <span data-ttu-id="bb150-134">[Criar cache Olá][Create hello cache]</span><span class="sxs-lookup"><span data-stu-id="bb150-134">[Create hello cache][Create hello cache]</span></span>
* <span data-ttu-id="bb150-135">[Configurar clientes de cache de Olá][Configure hello cache clients]</span><span class="sxs-lookup"><span data-stu-id="bb150-135">[Configure hello cache clients][Configure hello cache clients]</span></span>

<a name="create-cache"></a>

## <a name="create-a-cache"></a><span data-ttu-id="bb150-136">Criar uma cache</span><span class="sxs-lookup"><span data-stu-id="bb150-136">Create a cache</span></span>
[!INCLUDE [redis-cache-create](../../includes/redis-cache-create.md)]

### <a name="tooaccess-your-cache-after-its-created"></a><span data-ttu-id="bb150-137">tooaccess seja criada a sua cache depois</span><span class="sxs-lookup"><span data-stu-id="bb150-137">tooaccess your cache after it's created</span></span>
[!INCLUDE [redis-cache-create](../../includes/redis-cache-browse.md)]

<span data-ttu-id="bb150-138">Para obter mais informações sobre como configurar a cache, consulte [como tooconfigure a Cache de Redis do Azure](cache-configure.md).</span><span class="sxs-lookup"><span data-stu-id="bb150-138">For more information about configuring your cache, see [How tooconfigure Azure Redis Cache](cache-configure.md).</span></span>

<a name="NuGet"></a>

## <a name="configure-hello-cache-clients"></a><span data-ttu-id="bb150-139">Configurar clientes de cache de Olá</span><span class="sxs-lookup"><span data-stu-id="bb150-139">Configure hello cache clients</span></span>
[!INCLUDE [redis-cache-configure](../../includes/redis-cache-configure-stackexchange-redis-nuget.md)]

<span data-ttu-id="bb150-140">Depois do projeto de cliente é configurado para a colocação em cache, pode utilizar as técnicas de Olá descritas nas seguintes secções para trabalhar com a cache de Olá.</span><span class="sxs-lookup"><span data-stu-id="bb150-140">Once your client project is configured for caching, you can use hello techniques described in hello following sections for working with your cache.</span></span>

<a name="working-with-caches"></a>

## <a name="working-with-caches"></a><span data-ttu-id="bb150-141">Trabalhar com Caches</span><span class="sxs-lookup"><span data-stu-id="bb150-141">Working with Caches</span></span>
<span data-ttu-id="bb150-142">passos de Olá nesta secção descrevem como tooperform comuns tarefas com a Cache.</span><span class="sxs-lookup"><span data-stu-id="bb150-142">hello steps in this section describe how tooperform common tasks with Cache.</span></span>

* <span data-ttu-id="bb150-143">[Ligar toohello cache][Connect toohello cache]</span><span class="sxs-lookup"><span data-stu-id="bb150-143">[Connect toohello cache][Connect toohello cache]</span></span>
* <span data-ttu-id="bb150-144">[Adicionar e obter objetos da cache de Olá][Add and retrieve objects from hello cache]</span><span class="sxs-lookup"><span data-stu-id="bb150-144">[Add and retrieve objects from hello cache][Add and retrieve objects from hello cache]</span></span>
* [<span data-ttu-id="bb150-145">Trabalhar com objetos .NET na cache de Olá</span><span class="sxs-lookup"><span data-stu-id="bb150-145">Work with .NET objects in hello cache</span></span>](#work-with-net-objects-in-the-cache)

<a name="connect-to-cache"></a>

## <a name="connect-toohello-cache"></a><span data-ttu-id="bb150-146">Ligar toohello cache</span><span class="sxs-lookup"><span data-stu-id="bb150-146">Connect toohello cache</span></span>
<span data-ttu-id="bb150-147">trabalho tooprogrammatically com uma cache, precisa de uma cache de toohello de referência.</span><span class="sxs-lookup"><span data-stu-id="bb150-147">tooprogrammatically work with a cache, you need a reference toohello cache.</span></span> <span data-ttu-id="bb150-148">Adicione Olá seguir superior toohello de qualquer ficheiro a partir do qual pretende toouse Olá stackexchange. redis cliente tooaccess uma Cache de Redis do Azure.</span><span class="sxs-lookup"><span data-stu-id="bb150-148">Add hello following toohello top of any file from which you want toouse hello StackExchange.Redis client tooaccess an Azure Redis Cache.</span></span>

    using StackExchange.Redis;

> [!NOTE]
> <span data-ttu-id="bb150-149">cliente do Olá stackexchange. redis requer o .NET Framework 4 ou superior.</span><span class="sxs-lookup"><span data-stu-id="bb150-149">hello StackExchange.Redis client requires .NET Framework 4 or higher.</span></span>
> 
> 

<span data-ttu-id="bb150-150">Olá toohello de ligação, a Cache de Redis do Azure é gerida pelo Olá `ConnectionMultiplexer` classe.</span><span class="sxs-lookup"><span data-stu-id="bb150-150">hello connection toohello Azure Redis Cache is managed by hello `ConnectionMultiplexer` class.</span></span> <span data-ttu-id="bb150-151">Esta classe deve ser partilhada e reutilizada em toda a aplicação cliente e não precisa de toobe criado numa base por operação.</span><span class="sxs-lookup"><span data-stu-id="bb150-151">This class should be shared and reused throughout your client application, and does not need toobe created on a per operation basis.</span></span> 

<span data-ttu-id="bb150-152">tooconnect tooan a Cache de Redis do Azure e ser devolvida uma instância de um ligado `ConnectionMultiplexer`, chamada Olá estático `Connect` método e passar no Olá colocar em cache ponto final e a chave.</span><span class="sxs-lookup"><span data-stu-id="bb150-152">tooconnect tooan Azure Redis Cache and be returned an instance of a connected `ConnectionMultiplexer`, call hello static `Connect` method and pass in hello cache endpoint and key.</span></span> <span data-ttu-id="bb150-153">Utilize chave Olá gerado a partir de Olá portal do Azure como parâmetro de palavra-passe Olá.</span><span class="sxs-lookup"><span data-stu-id="bb150-153">Use hello key generated from hello Azure portal as hello password parameter.</span></span>

    ConnectionMultiplexer connection = ConnectionMultiplexer.Connect("contoso5.redis.cache.windows.net,abortConnect=false,ssl=true,password=...");

> [!IMPORTANT]
> <span data-ttu-id="bb150-154">Aviso: nunca guarde as credenciais no código fonte.</span><span class="sxs-lookup"><span data-stu-id="bb150-154">Warning: Never store credentials in source code.</span></span> <span data-ttu-id="bb150-155">tookeep simples este exemplo, as credenciais são apresentadas no código de origem Olá.</span><span class="sxs-lookup"><span data-stu-id="bb150-155">tookeep this sample simple, I’m showing them in hello source code.</span></span> <span data-ttu-id="bb150-156">Consulte [como cadeias de aplicação e de trabalho de cadeias de ligação] [ How Application Strings and Connection Strings Work] para obter informações sobre como toostore credenciais.</span><span class="sxs-lookup"><span data-stu-id="bb150-156">See [How Application Strings and Connection Strings Work][How Application Strings and Connection Strings Work] for information on how toostore credentials.</span></span>
> 
> 

<span data-ttu-id="bb150-157">Se não quiser toouse SSL, defina `ssl=false` ou omita Olá `ssl` parâmetro.</span><span class="sxs-lookup"><span data-stu-id="bb150-157">If you don't want toouse SSL, either set `ssl=false` or omit hello `ssl` parameter.</span></span>

> [!NOTE]
> <span data-ttu-id="bb150-158">porta do Olá não SSL está desativada por predefinição para novas caches.</span><span class="sxs-lookup"><span data-stu-id="bb150-158">hello non-SSL port is disabled by default for new caches.</span></span> <span data-ttu-id="bb150-159">Para obter instruções sobre como ativar a porta não SSL de Olá, consulte [portas de acesso](cache-configure.md#access-ports).</span><span class="sxs-lookup"><span data-stu-id="bb150-159">For instructions on enabling hello non-SSL port, see [Access Ports](cache-configure.md#access-ports).</span></span>
> 
> 

<span data-ttu-id="bb150-160">Uma abordagem toosharing um `ConnectionMultiplexer` instância na sua aplicação é toohave uma propriedade estática que devolva uma instância ligada, semelhante toohello seguinte exemplo.</span><span class="sxs-lookup"><span data-stu-id="bb150-160">One approach toosharing a `ConnectionMultiplexer` instance in your application is toohave a static property that returns a connected instance, similar toohello following example.</span></span> <span data-ttu-id="bb150-161">Esta abordagem fornece uma forma segura para threads tooinitialize apenas um único ligado `ConnectionMultiplexer` instância.</span><span class="sxs-lookup"><span data-stu-id="bb150-161">This approach provides a thread-safe way tooinitialize only a single connected `ConnectionMultiplexer` instance.</span></span> <span data-ttu-id="bb150-162">Nestes exemplos `abortConnect` é toofalse conjunto, o que significa que a chamada de Olá tem êxito mesmo se não for estabelecida uma ligação toohello a Cache de Redis do Azure.</span><span class="sxs-lookup"><span data-stu-id="bb150-162">In these examples `abortConnect` is set toofalse, which means that hello call succeeds even if a connection toohello Azure Redis Cache is not established.</span></span> <span data-ttu-id="bb150-163">Uma funcionalidade-chave de `ConnectionMultiplexer` é que este restaura automaticamente cache de toohello conectividade depois do problema de rede Olá ou outras causas são resolvidas.</span><span class="sxs-lookup"><span data-stu-id="bb150-163">One key feature of `ConnectionMultiplexer` is that it automatically restores connectivity toohello cache once hello network issue or other causes are resolved.</span></span>

    private static Lazy<ConnectionMultiplexer> lazyConnection = new Lazy<ConnectionMultiplexer>(() =>
    {
        return ConnectionMultiplexer.Connect("contoso5.redis.cache.windows.net,abortConnect=false,ssl=true,password=...");
    });

    public static ConnectionMultiplexer Connection
    {
        get
        {
            return lazyConnection.Value;
        }
    }

<span data-ttu-id="bb150-164">Para obter mais informações sobre as opções avançadas de configuração de ligação, veja o [Modelo de configuração StackExchange.Redis][StackExchange.Redis configuration model].</span><span class="sxs-lookup"><span data-stu-id="bb150-164">For more information on advanced connection configuration options, see [StackExchange.Redis configuration model][StackExchange.Redis configuration model].</span></span>

[!INCLUDE [redis-cache-create](../../includes/redis-cache-access-keys.md)]

<span data-ttu-id="bb150-165">Depois de Olá ligação for estabelecida, é devolvida uma referência toohello redis cache da base de dados, chamar Olá `ConnectionMultiplexer.GetDatabase` método.</span><span class="sxs-lookup"><span data-stu-id="bb150-165">Once hello connection is established, return a reference toohello redis cache database by calling hello `ConnectionMultiplexer.GetDatabase` method.</span></span> <span data-ttu-id="bb150-166">objeto de Olá devolvido pelo Olá `GetDatabase` método é um objeto pass-through simples e não precisa de toobe armazenado.</span><span class="sxs-lookup"><span data-stu-id="bb150-166">hello object returned from hello `GetDatabase` method is a lightweight pass-through object and does not need toobe stored.</span></span>

    // Connection refers tooa property that returns a ConnectionMultiplexer
    // as shown in hello previous example.
    IDatabase cache = Connection.GetDatabase();

    // Perform cache operations using hello cache object...
    // Simple put of integral data types into hello cache
    cache.StringSet("key1", "value");
    cache.StringSet("key2", 25);

    // Simple get of data types from hello cache
    string key1 = cache.StringGet("key1");
    int key2 = (int)cache.StringGet("key2");

<span data-ttu-id="bb150-167">Caches de Redis do Azure têm um número configurável de bases de dados (predefinição de 16) que podem ser utilizados toologically Olá separado dados dentro de uma cache de Redis.</span><span class="sxs-lookup"><span data-stu-id="bb150-167">Azure Redis caches have a configurable number of databases (default of 16) that can be used toologically separate hello data within a Redis cache.</span></span> <span data-ttu-id="bb150-168">Para obter mais informações, veja [O que são as bases de dados Redis?](cache-faq.md#what-are-redis-databases) e [Configuração do servidor predefinido Redis](cache-configure.md#default-redis-server-configuration).</span><span class="sxs-lookup"><span data-stu-id="bb150-168">For more information, see [What are Redis databases?](cache-faq.md#what-are-redis-databases) and [Default Redis server configuration](cache-configure.md#default-redis-server-configuration).</span></span>

<span data-ttu-id="bb150-169">Agora que já sabe como instância de Cache de Redis do Azure tooconnect tooan e devolver um toohello referência colocar em cache da base de dados, vamos ver trabalhar com a cache de Olá.</span><span class="sxs-lookup"><span data-stu-id="bb150-169">Now that you know how tooconnect tooan Azure Redis Cache instance and return a reference toohello cache database, let's look at working with hello cache.</span></span>

<a name="add-object"></a>

## <a name="add-and-retrieve-objects-from-hello-cache"></a><span data-ttu-id="bb150-170">Adicionar e obter objetos da cache de Olá</span><span class="sxs-lookup"><span data-stu-id="bb150-170">Add and retrieve objects from hello cache</span></span>
<span data-ttu-id="bb150-171">Podem armazenar e obtidos a partir de uma cache utilizando Olá itens `StringSet` e `StringGet` métodos.</span><span class="sxs-lookup"><span data-stu-id="bb150-171">Items can be stored in and retrieved from a cache by using hello `StringSet` and `StringGet` methods.</span></span>

    // If key1 exists, it is overwritten.
    cache.StringSet("key1", "value1");

    string value = cache.StringGet("key1");

<span data-ttu-id="bb150-172">O redis armazena mais dados como cadeias de Redis, mas estas cadeias podem conter vários tipos de dados, incluindo dados binários serializados, que podem ser utilizados ao armazenar objetos .NET na cache de Olá grande.</span><span class="sxs-lookup"><span data-stu-id="bb150-172">Redis stores most data as Redis strings, but these strings can contain many types of data, including serialized binary data, which can be used when storing .NET objects in hello cache.</span></span>

<span data-ttu-id="bb150-173">Quando chamar `StringGet`, Olá objeto existir, será devolvido, se não, `null` é devolvido.</span><span class="sxs-lookup"><span data-stu-id="bb150-173">When calling `StringGet`, if hello object exists, it is returned, and if it does not, `null` is returned.</span></span> <span data-ttu-id="bb150-174">Se `null` é devolvida, pode obter o valor de Olá Olá pretendido da origem de dados e guarde-o na cache de Olá para uma utilização posterior.</span><span class="sxs-lookup"><span data-stu-id="bb150-174">If `null` is returned, you can retrieve hello value from hello desired data source and store it in hello cache for subsequent use.</span></span> <span data-ttu-id="bb150-175">Este padrão de utilização é conhecido como padrão do lado da cache de Olá.</span><span class="sxs-lookup"><span data-stu-id="bb150-175">This usage pattern is known as hello cache-aside pattern.</span></span>

    string value = cache.StringGet("key1");
    if (value == null)
    {
        // hello item keyed by "key1" is not in hello cache. Obtain
        // it from hello desired data source and add it toohello cache.
        value = GetValueFromDataSource();

        cache.StringSet("key1", value);
    }

<span data-ttu-id="bb150-176">Também pode utilizar `RedisValue`, conforme mostrado no seguinte exemplo de Olá.</span><span class="sxs-lookup"><span data-stu-id="bb150-176">You can also use `RedisValue`, as shown in hello following example.</span></span> <span data-ttu-id="bb150-177">`RedisValue` tem operadores implícitos para trabalhar com tipos de dados integrais e pode ser útil se `null` for um valor esperado para um item em cache.</span><span class="sxs-lookup"><span data-stu-id="bb150-177">`RedisValue` has implicit operators for working with integral data types, and can be useful if `null` is an expected value for a cached item.</span></span>


    RedisValue value = cache.StringGet("key1");
    if (!value.HasValue)
    {
        value = GetValueFromDataSource();
        cache.StringSet("key1", value);
    }


<span data-ttu-id="bb150-178">expiração de Olá toospecify de um item na cache de Olá, utilize Olá `TimeSpan` parâmetro `StringSet`.</span><span class="sxs-lookup"><span data-stu-id="bb150-178">toospecify hello expiration of an item in hello cache, use hello `TimeSpan` parameter of `StringSet`.</span></span>

    cache.StringSet("key1", "value1", TimeSpan.FromMinutes(90));

## <a name="work-with-net-objects-in-hello-cache"></a><span data-ttu-id="bb150-179">Trabalhar com objetos .NET na cache de Olá</span><span class="sxs-lookup"><span data-stu-id="bb150-179">Work with .NET objects in hello cache</span></span>
<span data-ttu-id="bb150-180">A Cache de Redis do Azure pode colocar em cache objetos .NET e tipos de dados primitivos, mas para ser colocado em cache, o objeto .NET tem de ser serializado.</span><span class="sxs-lookup"><span data-stu-id="bb150-180">Azure Redis Cache can cache both .NET objects and primitive data types, but before a .NET object can be cached it must be serialized.</span></span> <span data-ttu-id="bb150-181">Esta serialização do objeto .NET Olá responsabilidade do programador da aplicação Olá e proporciona flexibilidade de programador Olá na escolha de Olá de serializador Olá.</span><span class="sxs-lookup"><span data-stu-id="bb150-181">This .NET object serialization is hello responsibility of hello application developer, and gives hello developer flexibility in hello choice of hello serializer.</span></span>

<span data-ttu-id="bb150-182">Objetos de uma forma simples tooserialize é toouse Olá `JsonConvert` métodos de serialização no [Newtonsoft.Json.NET](https://www.nuget.org/packages/Newtonsoft.Json/8.0.1-beta1) e serializar tooand JSON.</span><span class="sxs-lookup"><span data-stu-id="bb150-182">One simple way tooserialize objects is toouse hello `JsonConvert` serialization methods in [Newtonsoft.Json.NET](https://www.nuget.org/packages/Newtonsoft.Json/8.0.1-beta1) and serialize tooand from JSON.</span></span> <span data-ttu-id="bb150-183">Olá exemplo seguinte mostra um obter e definir utilizando uma `Employee` a instância do objeto.</span><span class="sxs-lookup"><span data-stu-id="bb150-183">hello following example shows a get and set using an `Employee` object instance.</span></span>

    class Employee
    {
        public int Id { get; set; }
        public string Name { get; set; }

        public Employee(int EmployeeId, string Name)
        {
            this.Id = EmployeeId;
            this.Name = Name;
        }
    }

    // Store toocache
    cache.StringSet("e25", JsonConvert.SerializeObject(new Employee(25, "Clayton Gragg")));

    // Retrieve from cache
    Employee e25 = JsonConvert.DeserializeObject<Employee>(cache.StringGet("e25"));

<a name="next-steps"></a>

## <a name="next-steps"></a><span data-ttu-id="bb150-184">Passos Seguintes</span><span class="sxs-lookup"><span data-stu-id="bb150-184">Next Steps</span></span>
<span data-ttu-id="bb150-185">Agora que aprendeu as noções básicas de Olá, siga estas toolearn ligações mais informações sobre a Cache de Redis do Azure.</span><span class="sxs-lookup"><span data-stu-id="bb150-185">Now that you've learned hello basics, follow these links toolearn more about Azure Redis Cache.</span></span>

* <span data-ttu-id="bb150-186">Consulte Olá fornecedores do ASP.NET para a Cache de Redis do Azure.</span><span class="sxs-lookup"><span data-stu-id="bb150-186">Check out hello ASP.NET providers for Azure Redis Cache.</span></span>
  * [<span data-ttu-id="bb150-187">Fornecedor de Estado da Sessão de Redis do Azure</span><span class="sxs-lookup"><span data-stu-id="bb150-187">Azure Redis Session State Provider</span></span>](cache-aspnet-session-state-provider.md)
  * [<span data-ttu-id="bb150-188">Fornecedor de Cache de Saída do ASP.NET da Cache de Redis do Azure</span><span class="sxs-lookup"><span data-stu-id="bb150-188">Azure Redis Cache ASP.NET Output Cache Provider</span></span>](cache-aspnet-output-cache-provider.md)
* <span data-ttu-id="bb150-189">[Ativar o diagnóstico da cache](cache-how-to-monitor.md#enable-cache-diagnostics) para poder [monitor](cache-how-to-monitor.md) Olá estado de funcionamento da cache.</span><span class="sxs-lookup"><span data-stu-id="bb150-189">[Enable cache diagnostics](cache-how-to-monitor.md#enable-cache-diagnostics) so you can [monitor](cache-how-to-monitor.md) hello health of your cache.</span></span> <span data-ttu-id="bb150-190">Pode ver Olá métricas na Olá portal do Azure e podem também [transferir e reveja](https://github.com/rustd/RedisSamples/tree/master/CustomMonitoring) -los utilizando as ferramentas de Olá à sua escolha.</span><span class="sxs-lookup"><span data-stu-id="bb150-190">You can view hello metrics in hello Azure portal and you can also [download and review](https://github.com/rustd/RedisSamples/tree/master/CustomMonitoring) them using hello tools of your choice.</span></span>
* <span data-ttu-id="bb150-191">Veja Olá [documentação do cliente de cache stackexchange. redis][StackExchange.Redis cache client documentation].</span><span class="sxs-lookup"><span data-stu-id="bb150-191">Check out hello [StackExchange.Redis cache client documentation][StackExchange.Redis cache client documentation].</span></span>
  * <span data-ttu-id="bb150-192">Pode aceder à Cache de Redis do Azure a partir de muitos clientes de Redis e linguagens de desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="bb150-192">Azure Redis Cache can be accessed from many Redis clients and development languages.</span></span> <span data-ttu-id="bb150-193">Para obter mais informações, veja [http://redis.io/clients][http://redis.io/clients].</span><span class="sxs-lookup"><span data-stu-id="bb150-193">For more information, see [http://redis.io/clients][http://redis.io/clients].</span></span>
* <span data-ttu-id="bb150-194">A Cache de Redis do Azure também pode ser utilizada com serviços e ferramentas de terceiros, tais como Redsmin e Redis Desktop Manager.</span><span class="sxs-lookup"><span data-stu-id="bb150-194">Azure Redis Cache can also be used with third-party services and tools such as Redsmin and Redis Desktop Manager.</span></span>
  * <span data-ttu-id="bb150-195">Para mais informações sobre Redsmin, consulte [como tooretrieve uma ligação de Redis do Azure cadeia e utilizá-lo com o Redsmin][How tooretrieve an Azure Redis connection string and use it with Redsmin].</span><span class="sxs-lookup"><span data-stu-id="bb150-195">For more information about Redsmin, see [How tooretrieve an Azure Redis connection string and use it with Redsmin][How tooretrieve an Azure Redis connection string and use it with Redsmin].</span></span>
  * <span data-ttu-id="bb150-196">Aceda e inspecione os seus dados na Cache de Redis do Azure através de uma GUI com o [RedisDesktopManager](https://github.com/uglide/RedisDesktopManager).</span><span class="sxs-lookup"><span data-stu-id="bb150-196">Access and inspect your data in Azure Redis Cache with a GUI using [RedisDesktopManager](https://github.com/uglide/RedisDesktopManager).</span></span>
* <span data-ttu-id="bb150-197">Consulte Olá [redis] [ redis] documentação e ler sobre [tipos de dados de redis] [ redis data types] e [uma introdução de quinze minutos tipos de dados de tooRedis][a fifteen minute introduction tooRedis data types].</span><span class="sxs-lookup"><span data-stu-id="bb150-197">See hello [redis][redis] documentation and read about [redis data types][redis data types] and [a fifteen minute introduction tooRedis data types][a fifteen minute introduction tooRedis data types].</span></span>

<!-- INTRA-TOPIC LINKS -->
[Next Steps]: #next-steps
[Introduction tooAzure Redis Cache (Video)]: #video
[What is Azure Redis Cache?]: #what-is
[Create an Azure Cache]: #create-cache
[Which type of caching is right for me?]: #choosing-cache
[Prepare Your Visual Studio Project tooUse Azure Caching]: #prepare-vs
[Configure Your Application tooUse Caching]: #configure-app
[Get Started with Azure Redis Cache]: #getting-started-cache-service
[Create hello cache]: #create-cache
[Configure hello cache]: #enable-caching
[Configure hello cache clients]: #NuGet
[Working with Caches]: #working-with-caches
[Connect toohello cache]: #connect-to-cache
[Add and retrieve objects from hello cache]: #add-object
[Specify hello expiration of an object in hello cache]: #specify-expiration
[Store ASP.NET session state in hello cache]: #store-session


<!-- IMAGES -->


[StackExchangeNuget]: ./media/cache-dotnet-how-to-use-azure-redis-cache/redis-cache-stackexchange-redis.png

[NuGetMenu]: ./media/cache-dotnet-how-to-use-azure-redis-cache/redis-cache-manage-nuget-menu.png

[CacheProperties]: ./media/cache-dotnet-how-to-use-azure-redis-cache/redis-cache-properties.png

[ManageKeys]: ./media/cache-dotnet-how-to-use-azure-redis-cache/redis-cache-manage-keys.png

[SessionStateNuGet]: ./media/cache-dotnet-how-to-use-azure-redis-cache/redis-cache-session-state-provider.png

[BrowseCaches]: ./media/cache-dotnet-how-to-use-azure-redis-cache/redis-cache-browse-caches.png

[Caches]: ./media/cache-dotnet-how-to-use-azure-redis-cache/redis-cache-caches.png







<!-- LINKS -->
[http://redis.io/clients]: http://redis.io/clients
[Develop in other languages for Azure Redis Cache]: http://msdn.microsoft.com/library/azure/dn690470.aspx
[How tooretrieve an Azure Redis connection string and use it with Redsmin]: https://redsmin.uservoice.com/knowledgebase/articles/485711-how-to-connect-redsmin-to-azure-redis-cache
[Azure Redis Session State Provider]: http://go.microsoft.com/fwlink/?LinkId=398249
[How to: Configure a Cache Client Programmatically]: http://msdn.microsoft.com/library/windowsazure/gg618003.aspx
[Session State Provider for Azure Cache]: http://go.microsoft.com/fwlink/?LinkId=320835
[Azure AppFabric Cache: Caching Session State]: http://www.microsoft.com/showcase/details.aspx?uuid=87c833e9-97a9-42b2-8bb1-7601f9b5ca20
[Output Cache Provider for Azure Cache]: http://go.microsoft.com/fwlink/?LinkId=320837
[Azure Shared Caching]: http://msdn.microsoft.com/library/windowsazure/gg278356.aspx
[Team Blog]: http://blogs.msdn.com/b/windowsazure/
[Azure Caching]: http://www.microsoft.com/showcase/Search.aspx?phrase=azure+caching
[How tooConfigure Virtual Machine Sizes]: http://go.microsoft.com/fwlink/?LinkId=164387
[Azure Caching Capacity Planning Considerations]: http://go.microsoft.com/fwlink/?LinkId=320167
[Azure Caching]: http://go.microsoft.com/fwlink/?LinkId=252658
[How to: Set hello Cacheability of an ASP.NET Page Declaratively]: http://msdn.microsoft.com/library/zd1ysf1y.aspx
[How to: Set a Page's Cacheability Programmatically]: http://msdn.microsoft.com/library/z852zf6b.aspx
[Configure a cache in Azure Redis Cache]: http://msdn.microsoft.com/library/azure/dn793612.aspx

[StackExchange.Redis configuration model]: https://stackexchange.github.io/StackExchange.Redis/Configuration

[Work with .NET objects in hello cache]: http://msdn.microsoft.com/library/dn690521.aspx#Objects


[NuGet Package Manager Installation]: http://go.microsoft.com/fwlink/?LinkId=240311
[Cache Pricing Details]: http://www.windowsazure.com/pricing/details/cache/
[Azure portal]: https://portal.azure.com/

[Overview of Azure Redis Cache]: http://go.microsoft.com/fwlink/?LinkId=320830
[Azure Redis Cache]: http://go.microsoft.com/fwlink/?LinkId=398247

[Migrate tooAzure Redis Cache]: http://go.microsoft.com/fwlink/?LinkId=317347
[Azure Redis Cache Samples]: http://go.microsoft.com/fwlink/?LinkId=320840
[Using Resource groups toomanage your Azure resources]: ../azure-resource-manager/resource-group-overview.md

[StackExchange.Redis]: http://github.com/StackExchange/StackExchange.Redis
[StackExchange.Redis cache client documentation]: http://github.com/StackExchange/StackExchange.Redis#documentation

[Redis]: http://redis.io/documentation
[Redis data types]: http://redis.io/topics/data-types
[a fifteen minute introduction tooRedis data types]: http://redis.io/topics/data-types-intro

[How Application Strings and Connection Strings Work]: http://azure.microsoft.com/blog/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work/


