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
# <a name="how-toouse-azure-redis-cache"></a>Como tooUse do Azure da Cache de Redis
> [!div class="op_single_selector"]
> * [.NET](cache-dotnet-how-to-use-azure-redis-cache.md)
> * [ASP.NET](cache-web-app-howto.md)
> * [Node.js](cache-nodejs-get-started.md)
> * [Java](cache-java-get-started.md)
> * [python](cache-python-get-started.md)
> 
> 

Este guia mostra como tooget iniciado utilizando **a Cache de Redis do Azure**. Cache de Redis do Microsoft Azure baseia Olá populares open source para a Cache de Redis. Dá-lhe aceder tooa segura, dedicada cache de Redis e gerida pela Microsoft. Pode aceder a uma cache criada com a Cache de Redis do Azure a partir de qualquer aplicação dentro do Microsoft Azure.

Cache de Redis do Microsoft Azure está disponível no Olá seguintes escalões:

* **Básico** – Único nó. Vários tamanhos segurança too53 GB.
* **Standard** – Dois nós Primário/Réplica. Vários tamanhos segurança too53 GB. SLA de 99,9%.
* **Premium** – dois nós primário/réplica com segurança too10 shards. Vários tamanhos entre 6 GB too530 GB. Todas as funcionalidades do escalão Standard e mais, incluindo o suporte para o [Cluster de Redis](cache-how-to-premium-clustering.md), a [Persistência de Redis](cache-how-to-premium-persistence.md) e a [Azure Virtual Network](cache-how-to-premium-vnet.md). SLA de 99,9%.

Cada escalão difere em termos de funcionalidades e preços. Para obter informações sobre os preços, veja [Cache Pricing Details (Detalhes dos Preços da Cache)][Cache Pricing Details].

Este guia mostra como toouse Olá [stackexchange. redis] [ StackExchange.Redis] cliente utilizando C\# código. Olá os cenários abrangidos incluem **criar e configurar uma cache**, **configurar clientes de cache**, e **adição e remoção de objetos da cache de Olá**. Para obter mais informações sobre como utilizar a Cache de Redis do Azure, veja [Next Steps (Passos Seguintes)][Next Steps]. Para um tutorial passo a passo para criar uma ASP.NET MVC aplicação web com a Cache de Redis, consulte [como toocreate uma aplicação Web com a Cache de Redis](cache-web-app-howto.md).

<a name="getting-started-cache-service"></a>

## <a name="get-started-with-azure-redis-cache"></a>Introdução à Cache de Redis do Azure 
É fácil começar a trabalhar com a Cache de Redis do Azure. tooget iniciado, pode aprovisionar e configurar uma cache. Em seguida, configure os clientes de cache Olá para que podem aceder a cache de Olá. Assim que os clientes de cache Olá estiverem configurados, pode começar a trabalhar com eles.

* [Criar cache Olá][Create hello cache]
* [Configurar clientes de cache de Olá][Configure hello cache clients]

<a name="create-cache"></a>

## <a name="create-a-cache"></a>Criar uma cache
[!INCLUDE [redis-cache-create](../../includes/redis-cache-create.md)]

### <a name="tooaccess-your-cache-after-its-created"></a>tooaccess seja criada a sua cache depois
[!INCLUDE [redis-cache-create](../../includes/redis-cache-browse.md)]

Para obter mais informações sobre como configurar a cache, consulte [como tooconfigure a Cache de Redis do Azure](cache-configure.md).

<a name="NuGet"></a>

## <a name="configure-hello-cache-clients"></a>Configurar clientes de cache de Olá
[!INCLUDE [redis-cache-configure](../../includes/redis-cache-configure-stackexchange-redis-nuget.md)]

Depois do projeto de cliente é configurado para a colocação em cache, pode utilizar as técnicas de Olá descritas nas seguintes secções para trabalhar com a cache de Olá.

<a name="working-with-caches"></a>

## <a name="working-with-caches"></a>Trabalhar com Caches
passos de Olá nesta secção descrevem como tooperform comuns tarefas com a Cache.

* [Ligar toohello cache][Connect toohello cache]
* [Adicionar e obter objetos da cache de Olá][Add and retrieve objects from hello cache]
* [Trabalhar com objetos .NET na cache de Olá](#work-with-net-objects-in-the-cache)

<a name="connect-to-cache"></a>

## <a name="connect-toohello-cache"></a>Ligar toohello cache
trabalho tooprogrammatically com uma cache, precisa de uma cache de toohello de referência. Adicione Olá seguir superior toohello de qualquer ficheiro a partir do qual pretende toouse Olá stackexchange. redis cliente tooaccess uma Cache de Redis do Azure.

    using StackExchange.Redis;

> [!NOTE]
> cliente do Olá stackexchange. redis requer o .NET Framework 4 ou superior.
> 
> 

Olá toohello de ligação, a Cache de Redis do Azure é gerida pelo Olá `ConnectionMultiplexer` classe. Esta classe deve ser partilhada e reutilizada em toda a aplicação cliente e não precisa de toobe criado numa base por operação. 

tooconnect tooan a Cache de Redis do Azure e ser devolvida uma instância de um ligado `ConnectionMultiplexer`, chamada Olá estático `Connect` método e passar no Olá colocar em cache ponto final e a chave. Utilize chave Olá gerado a partir de Olá portal do Azure como parâmetro de palavra-passe Olá.

    ConnectionMultiplexer connection = ConnectionMultiplexer.Connect("contoso5.redis.cache.windows.net,abortConnect=false,ssl=true,password=...");

> [!IMPORTANT]
> Aviso: nunca guarde as credenciais no código fonte. tookeep simples este exemplo, as credenciais são apresentadas no código de origem Olá. Consulte [como cadeias de aplicação e de trabalho de cadeias de ligação] [ How Application Strings and Connection Strings Work] para obter informações sobre como toostore credenciais.
> 
> 

Se não quiser toouse SSL, defina `ssl=false` ou omita Olá `ssl` parâmetro.

> [!NOTE]
> porta do Olá não SSL está desativada por predefinição para novas caches. Para obter instruções sobre como ativar a porta não SSL de Olá, consulte [portas de acesso](cache-configure.md#access-ports).
> 
> 

Uma abordagem toosharing um `ConnectionMultiplexer` instância na sua aplicação é toohave uma propriedade estática que devolva uma instância ligada, semelhante toohello seguinte exemplo. Esta abordagem fornece uma forma segura para threads tooinitialize apenas um único ligado `ConnectionMultiplexer` instância. Nestes exemplos `abortConnect` é toofalse conjunto, o que significa que a chamada de Olá tem êxito mesmo se não for estabelecida uma ligação toohello a Cache de Redis do Azure. Uma funcionalidade-chave de `ConnectionMultiplexer` é que este restaura automaticamente cache de toohello conectividade depois do problema de rede Olá ou outras causas são resolvidas.

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

Para obter mais informações sobre as opções avançadas de configuração de ligação, veja o [Modelo de configuração StackExchange.Redis][StackExchange.Redis configuration model].

[!INCLUDE [redis-cache-create](../../includes/redis-cache-access-keys.md)]

Depois de Olá ligação for estabelecida, é devolvida uma referência toohello redis cache da base de dados, chamar Olá `ConnectionMultiplexer.GetDatabase` método. objeto de Olá devolvido pelo Olá `GetDatabase` método é um objeto pass-through simples e não precisa de toobe armazenado.

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

Caches de Redis do Azure têm um número configurável de bases de dados (predefinição de 16) que podem ser utilizados toologically Olá separado dados dentro de uma cache de Redis. Para obter mais informações, veja [O que são as bases de dados Redis?](cache-faq.md#what-are-redis-databases) e [Configuração do servidor predefinido Redis](cache-configure.md#default-redis-server-configuration).

Agora que já sabe como instância de Cache de Redis do Azure tooconnect tooan e devolver um toohello referência colocar em cache da base de dados, vamos ver trabalhar com a cache de Olá.

<a name="add-object"></a>

## <a name="add-and-retrieve-objects-from-hello-cache"></a>Adicionar e obter objetos da cache de Olá
Podem armazenar e obtidos a partir de uma cache utilizando Olá itens `StringSet` e `StringGet` métodos.

    // If key1 exists, it is overwritten.
    cache.StringSet("key1", "value1");

    string value = cache.StringGet("key1");

O redis armazena mais dados como cadeias de Redis, mas estas cadeias podem conter vários tipos de dados, incluindo dados binários serializados, que podem ser utilizados ao armazenar objetos .NET na cache de Olá grande.

Quando chamar `StringGet`, Olá objeto existir, será devolvido, se não, `null` é devolvido. Se `null` é devolvida, pode obter o valor de Olá Olá pretendido da origem de dados e guarde-o na cache de Olá para uma utilização posterior. Este padrão de utilização é conhecido como padrão do lado da cache de Olá.

    string value = cache.StringGet("key1");
    if (value == null)
    {
        // hello item keyed by "key1" is not in hello cache. Obtain
        // it from hello desired data source and add it toohello cache.
        value = GetValueFromDataSource();

        cache.StringSet("key1", value);
    }

Também pode utilizar `RedisValue`, conforme mostrado no seguinte exemplo de Olá. `RedisValue` tem operadores implícitos para trabalhar com tipos de dados integrais e pode ser útil se `null` for um valor esperado para um item em cache.


    RedisValue value = cache.StringGet("key1");
    if (!value.HasValue)
    {
        value = GetValueFromDataSource();
        cache.StringSet("key1", value);
    }


expiração de Olá toospecify de um item na cache de Olá, utilize Olá `TimeSpan` parâmetro `StringSet`.

    cache.StringSet("key1", "value1", TimeSpan.FromMinutes(90));

## <a name="work-with-net-objects-in-hello-cache"></a>Trabalhar com objetos .NET na cache de Olá
A Cache de Redis do Azure pode colocar em cache objetos .NET e tipos de dados primitivos, mas para ser colocado em cache, o objeto .NET tem de ser serializado. Esta serialização do objeto .NET Olá responsabilidade do programador da aplicação Olá e proporciona flexibilidade de programador Olá na escolha de Olá de serializador Olá.

Objetos de uma forma simples tooserialize é toouse Olá `JsonConvert` métodos de serialização no [Newtonsoft.Json.NET](https://www.nuget.org/packages/Newtonsoft.Json/8.0.1-beta1) e serializar tooand JSON. Olá exemplo seguinte mostra um obter e definir utilizando uma `Employee` a instância do objeto.

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

## <a name="next-steps"></a>Passos Seguintes
Agora que aprendeu as noções básicas de Olá, siga estas toolearn ligações mais informações sobre a Cache de Redis do Azure.

* Consulte Olá fornecedores do ASP.NET para a Cache de Redis do Azure.
  * [Fornecedor de Estado da Sessão de Redis do Azure](cache-aspnet-session-state-provider.md)
  * [Fornecedor de Cache de Saída do ASP.NET da Cache de Redis do Azure](cache-aspnet-output-cache-provider.md)
* [Ativar o diagnóstico da cache](cache-how-to-monitor.md#enable-cache-diagnostics) para poder [monitor](cache-how-to-monitor.md) Olá estado de funcionamento da cache. Pode ver Olá métricas na Olá portal do Azure e podem também [transferir e reveja](https://github.com/rustd/RedisSamples/tree/master/CustomMonitoring) -los utilizando as ferramentas de Olá à sua escolha.
* Veja Olá [documentação do cliente de cache stackexchange. redis][StackExchange.Redis cache client documentation].
  * Pode aceder à Cache de Redis do Azure a partir de muitos clientes de Redis e linguagens de desenvolvimento. Para obter mais informações, veja [http://redis.io/clients][http://redis.io/clients].
* A Cache de Redis do Azure também pode ser utilizada com serviços e ferramentas de terceiros, tais como Redsmin e Redis Desktop Manager.
  * Para mais informações sobre Redsmin, consulte [como tooretrieve uma ligação de Redis do Azure cadeia e utilizá-lo com o Redsmin][How tooretrieve an Azure Redis connection string and use it with Redsmin].
  * Aceda e inspecione os seus dados na Cache de Redis do Azure através de uma GUI com o [RedisDesktopManager](https://github.com/uglide/RedisDesktopManager).
* Consulte Olá [redis] [ redis] documentação e ler sobre [tipos de dados de redis] [ redis data types] e [uma introdução de quinze minutos tipos de dados de tooRedis][a fifteen minute introduction tooRedis data types].

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


