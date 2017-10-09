---
title: "aaaCache fornecedor de Cache de saída do ASP.NET"
description: "Saiba como saída de página do ASP.NET de toocache utilizando a Cache de Redis do Azure"
services: redis-cache
documentationcenter: na
author: steved0x
manager: douge
editor: tysonn
ms.assetid: 78469a66-0829-484f-8660-b2598ec60fbf
ms.service: cache
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: cache-redis
ms.workload: tbd
ms.date: 02/14/2017
ms.author: sdanie
ms.openlocfilehash: fc38cc657604b351f55ad8febac383783ac29700
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="aspnet-output-cache-provider-for-azure-redis-cache"></a><span data-ttu-id="5b530-103">Fornecedor de Cache de saída do ASP.NET para o Azure Redis Cache</span><span class="sxs-lookup"><span data-stu-id="5b530-103">ASP.NET Output Cache Provider for Azure Redis Cache</span></span>
<span data-ttu-id="5b530-104">Olá Redis fornecedor de Cache de saída é um mecanismo de armazenamento de fora do processo para dados da cache de saída.</span><span class="sxs-lookup"><span data-stu-id="5b530-104">hello Redis Output Cache Provider is an out-of-process storage mechanism for output cache data.</span></span> <span data-ttu-id="5b530-105">Estes dados são especificamente para as respostas HTTP completas (página a cache de saída).</span><span class="sxs-lookup"><span data-stu-id="5b530-105">This data is specifically for full HTTP responses (page output caching).</span></span> <span data-ttu-id="5b530-106">fornecedor de Olá plugs para Olá nova saída cache fornecedor ponto de extensibilidade que foi introduzido no ASP.NET 4.</span><span class="sxs-lookup"><span data-stu-id="5b530-106">hello provider plugs into hello new output cache provider extensibility point that was introduced in ASP.NET 4.</span></span>

<span data-ttu-id="5b530-107">Olá toouse Redis fornecedor de Cache de saída, primeiro de configurar a cache e, em seguida, configure a sua aplicação ASP.NET, utilizando o pacote de Redis NuGet de fornecedor de Cache de saída Olá.</span><span class="sxs-lookup"><span data-stu-id="5b530-107">toouse hello Redis Output Cache Provider, first configure your cache, and then configure your ASP.NET application using hello Redis Output Cache Provider NuGet package.</span></span> <span data-ttu-id="5b530-108">Este tópico fornece orientações sobre como configurar a sua Olá toouse de aplicação Redis fornecedor de Cache de saída.</span><span class="sxs-lookup"><span data-stu-id="5b530-108">This topic provides guidance on configuring your application toouse hello Redis Output Cache Provider.</span></span> <span data-ttu-id="5b530-109">Para obter mais informações sobre como criar e configurar uma instância da Cache de Redis do Azure, consulte [criar uma cache](cache-dotnet-how-to-use-azure-redis-cache.md#create-a-cache).</span><span class="sxs-lookup"><span data-stu-id="5b530-109">For more information about creating and configuring an Azure Redis Cache instance, see [Create a cache](cache-dotnet-how-to-use-azure-redis-cache.md#create-a-cache).</span></span>

## <a name="store-aspnet-page-output-in-hello-cache"></a><span data-ttu-id="5b530-110">Armazenar a saída de páginas do ASP.NET na cache de Olá</span><span class="sxs-lookup"><span data-stu-id="5b530-110">Store ASP.NET page output in hello cache</span></span>
<span data-ttu-id="5b530-111">tooconfigure uma aplicação de cliente no Visual Studio com o pacote de Redis NuGet de estado de sessão de Cache de Olá, clique em **Gestor de pacotes NuGet**, **consola do Gestor de pacotes** de Olá **ferramentas** menu.</span><span class="sxs-lookup"><span data-stu-id="5b530-111">tooconfigure a client application in Visual Studio using hello Redis Cache Session State NuGet package, click **NuGet Package Manager**, **Package Manager Console** from hello **Tools** menu.</span></span>

<span data-ttu-id="5b530-112">Execute hello os seguintes comandos do Olá `Package Manager Console` janela.</span><span class="sxs-lookup"><span data-stu-id="5b530-112">Run hello following command from hello `Package Manager Console` window.</span></span>
    
```
Install-Package Microsoft.Web.RedisOutputCacheProvider
```

<span data-ttu-id="5b530-113">pacote de Redis NuGet de fornecedor de Cache de saída Olá tem uma dependência no pacote de StrongName Olá.</span><span class="sxs-lookup"><span data-stu-id="5b530-113">hello Redis Output Cache Provider NuGet package has a dependency on hello StackExchange.Redis.StrongName package.</span></span> <span data-ttu-id="5b530-114">Se o pacote de StrongName Olá não está presente no projeto, está instalado.</span><span class="sxs-lookup"><span data-stu-id="5b530-114">If hello StackExchange.Redis.StrongName package is not present in your project, it is installed.</span></span> <span data-ttu-id="5b530-115">Para obter mais informações sobre o pacote de Redis NuGet de fornecedor de Cache de saída Olá, consulte Olá [RedisOutputCacheProvider](https://www.nuget.org/packages/Microsoft.Web.RedisOutputCacheProvider/) página NuGet.</span><span class="sxs-lookup"><span data-stu-id="5b530-115">For more information about hello Redis Output Cache Provider NuGet package, see hello [RedisOutputCacheProvider](https://www.nuget.org/packages/Microsoft.Web.RedisOutputCacheProvider/) NuGet page.</span></span>

>[!NOTE]
><span data-ttu-id="5b530-116">Adição toohello com nome seguro StrongName pacote, há também Olá stackexchange. redis não-com nome seguro versão.</span><span class="sxs-lookup"><span data-stu-id="5b530-116">In addition toohello strong-named StackExchange.Redis.StrongName package, there is also hello StackExchange.Redis non-strong-named version.</span></span> <span data-ttu-id="5b530-117">Caso contrário, se o projeto está a utilizar Olá não-com nome seguro stackexchange. redis versão que tem de o desinstalar, obter nomenclatura conflitos no seu projeto.</span><span class="sxs-lookup"><span data-stu-id="5b530-117">If your project is using hello non-strong-named StackExchange.Redis version you must uninstall it, otherwise you get naming conflicts in your project.</span></span> <span data-ttu-id="5b530-118">Para obter mais informações sobre estes pacotes, consulte [clientes de cache de .NET configurar](cache-dotnet-how-to-use-azure-redis-cache.md#configure-the-cache-clients).</span><span class="sxs-lookup"><span data-stu-id="5b530-118">For more information about these packages, see [Configure .NET cache clients](cache-dotnet-how-to-use-azure-redis-cache.md#configure-the-cache-clients).</span></span>
>
>

<span data-ttu-id="5b530-119">Olá NuGet pacote transfere e adiciona Olá necessário assemblagem referencia e adiciona Olá secção a seguir no seu ficheiro Web. config.</span><span class="sxs-lookup"><span data-stu-id="5b530-119">hello NuGet package downloads and adds hello required assembly references and adds hello following section into your web.config file.</span></span> <span data-ttu-id="5b530-120">Esta secção contém configuração necessários de Olá para sua Olá de toouse de aplicação de ASP.NET Redis fornecedor de Cache de saída.</span><span class="sxs-lookup"><span data-stu-id="5b530-120">This section contains hello required configuration for your ASP.NET application toouse hello Redis Output Cache Provider.</span></span>

```xml
<caching>
  <outputCachedefault Provider="MyRedisOutputCache">
    <providers>
      <!--
      <add name="MyRedisOutputCache"
        host = "127.0.0.1" [String]
        port = "" [number]
        accessKey = "" [String]
        ssl = "false" [true|false]
        databaseId = "0" [number]
        applicationName = "" [String]
        connectionTimeoutInMilliseconds = "5000" [number]
        operationTimeoutInMilliseconds = "5000" [number]
      />
      -->
      <add name="MyRedisOutputCache" type="Microsoft.Web.Redis.RedisOutputCacheProvider" host="127.0.0.1" accessKey="" ssl="false"/>
    </providers>
  </outputCache>
</caching>
```

<span data-ttu-id="5b530-121">Olá comentado secção fornece um exemplo de atributos de Olá e as definições de exemplo para cada atributo.</span><span class="sxs-lookup"><span data-stu-id="5b530-121">hello commented section provides an example of hello attributes and sample settings for each attribute.</span></span>

<span data-ttu-id="5b530-122">Configurar atributos Olá com valores de Olá do painel da cache no portal do Microsoft Azure Olá e configure Olá outros valores conforme pretendido.</span><span class="sxs-lookup"><span data-stu-id="5b530-122">Configure hello attributes with hello values from your cache blade in hello Microsoft Azure portal, and configure hello other values as desired.</span></span> <span data-ttu-id="5b530-123">Para obter instruções sobre como aceder as propriedades da cache, consulte [Configure Redis cache as definições](cache-configure.md#configure-redis-cache-settings).</span><span class="sxs-lookup"><span data-stu-id="5b530-123">For instructions on accessing your cache properties, see [Configure Redis cache settings](cache-configure.md#configure-redis-cache-settings).</span></span>

* <span data-ttu-id="5b530-124">**anfitrião** – especifique o ponto final da cache.</span><span class="sxs-lookup"><span data-stu-id="5b530-124">**host** – specify your cache endpoint.</span></span>
* <span data-ttu-id="5b530-125">**porta** – utilizar a porta não SSL ou a porta SSL, dependendo das definições de ssl Olá.</span><span class="sxs-lookup"><span data-stu-id="5b530-125">**port** – use either your non-SSL port or your SSL port, depending on hello ssl settings.</span></span>
* <span data-ttu-id="5b530-126">**accessKey** – utilizar a chave primária ou secundária de Olá para a sua cache.</span><span class="sxs-lookup"><span data-stu-id="5b530-126">**accessKey** – use either hello primary or secondary key for your cache.</span></span>
* <span data-ttu-id="5b530-127">**SSL** – VERDADEIRO se quiser comunicações de cliente de cache/toosecure com ssl; caso contrário FALSO.</span><span class="sxs-lookup"><span data-stu-id="5b530-127">**ssl** – true if you want toosecure cache/client communications with ssl; otherwise false.</span></span> <span data-ttu-id="5b530-128">Ser se Olá toospecify da porta do correto.</span><span class="sxs-lookup"><span data-stu-id="5b530-128">Be sure toospecify hello correct port.</span></span>
  * <span data-ttu-id="5b530-129">porta do Olá não SSL está desativada por predefinição para novas caches.</span><span class="sxs-lookup"><span data-stu-id="5b530-129">hello non-SSL port is disabled by default for new caches.</span></span> <span data-ttu-id="5b530-130">Especifica verdadeiro para esta Olá toouse de definição porta SSL.</span><span class="sxs-lookup"><span data-stu-id="5b530-130">Specify true for this setting toouse hello SSL port.</span></span> <span data-ttu-id="5b530-131">Para obter mais informações sobre como ativar a porta não SSL de Olá, consulte Olá [portas de acesso](cache-configure.md#access-ports) secção Olá [configurar uma cache](cache-configure.md) tópico.</span><span class="sxs-lookup"><span data-stu-id="5b530-131">For more information about enabling hello non-SSL port, see hello [Access Ports](cache-configure.md#access-ports) section in hello [Configure a cache](cache-configure.md) topic.</span></span>
* <span data-ttu-id="5b530-132">**databaseId** – especificado que toouse de base de dados para a cache de saída de dados.</span><span class="sxs-lookup"><span data-stu-id="5b530-132">**databaseId** – Specified which database toouse for cache output data.</span></span> <span data-ttu-id="5b530-133">Se não for especificado, é utilizado o valor predefinido de Olá 0.</span><span class="sxs-lookup"><span data-stu-id="5b530-133">If not specified, hello default value of 0 is used.</span></span>
* <span data-ttu-id="5b530-134">**applicationName** – chaves são armazenadas no redis como `<AppName>_<SessionId>_Data`.</span><span class="sxs-lookup"><span data-stu-id="5b530-134">**applicationName** – Keys are stored in redis as `<AppName>_<SessionId>_Data`.</span></span> <span data-ttu-id="5b530-135">Este esquema de nomenclatura permite vários Olá de tooshare aplicações mesma chave.</span><span class="sxs-lookup"><span data-stu-id="5b530-135">This naming scheme enables multiple applications tooshare hello same key.</span></span> <span data-ttu-id="5b530-136">Este parâmetro é opcional e se não o a fornecer um valor predefinido é utilizado.</span><span class="sxs-lookup"><span data-stu-id="5b530-136">This parameter is optional and if you do not provide it a default value is used.</span></span>
* <span data-ttu-id="5b530-137">**connectionTimeoutInMilliseconds** – esta definição permite-lhe toooverride Olá connectTimeout no cliente do Olá stackexchange. redis.</span><span class="sxs-lookup"><span data-stu-id="5b530-137">**connectionTimeoutInMilliseconds** – This setting allows you toooverride hello connectTimeout setting in hello StackExchange.Redis client.</span></span> <span data-ttu-id="5b530-138">Se não for especificado, Olá connectTimeout predefinição 5000 é utilizada.</span><span class="sxs-lookup"><span data-stu-id="5b530-138">If not specified, hello default connectTimeout setting of 5000 is used.</span></span> <span data-ttu-id="5b530-139">Para obter mais informações, consulte [modelo de configuração stackexchange. redis](http://go.microsoft.com/fwlink/?LinkId=398705).</span><span class="sxs-lookup"><span data-stu-id="5b530-139">For more information, see [StackExchange.Redis configuration model](http://go.microsoft.com/fwlink/?LinkId=398705).</span></span>
* <span data-ttu-id="5b530-140">**operationTimeoutInMilliseconds** – esta definição permite-lhe toooverride Olá syncTimeout no cliente do Olá stackexchange. redis.</span><span class="sxs-lookup"><span data-stu-id="5b530-140">**operationTimeoutInMilliseconds** – This setting allows you toooverride hello syncTimeout setting in hello StackExchange.Redis client.</span></span> <span data-ttu-id="5b530-141">Se não for especificado, é utilizada Olá syncTimeout predefinição 1000.</span><span class="sxs-lookup"><span data-stu-id="5b530-141">If not specified, hello default syncTimeout setting of 1000 is used.</span></span> <span data-ttu-id="5b530-142">Para obter mais informações, consulte [modelo de configuração stackexchange. redis](http://go.microsoft.com/fwlink/?LinkId=398705).</span><span class="sxs-lookup"><span data-stu-id="5b530-142">For more information, see [StackExchange.Redis configuration model](http://go.microsoft.com/fwlink/?LinkId=398705).</span></span>

<span data-ttu-id="5b530-143">Adicione uma página de tooeach diretiva OutputCache para o qual pretende a saída de Olá toocache.</span><span class="sxs-lookup"><span data-stu-id="5b530-143">Add an OutputCache directive tooeach page for which you wish toocache hello output.</span></span>

```
<%@ OutputCache Duration="60" VaryByParam="*" %>
```

<span data-ttu-id="5b530-144">No exemplo anterior Olá, Olá página dados permanecem na cache de Olá em cache durante 60 segundos e uma versão diferente da página Olá é colocado em cache para cada combinação de parâmetro.</span><span class="sxs-lookup"><span data-stu-id="5b530-144">In hello previous example, hello cached page data remains in hello cache for 60 seconds, and a different version of hello page is cached for each parameter combination.</span></span> <span data-ttu-id="5b530-145">Para mais informações sobre a diretiva OutputCache Olá, consulte [ @OutputCache ](http://go.microsoft.com/fwlink/?linkid=320837).</span><span class="sxs-lookup"><span data-stu-id="5b530-145">For more information about hello OutputCache directive, see [@OutputCache](http://go.microsoft.com/fwlink/?linkid=320837).</span></span>

<span data-ttu-id="5b530-146">Depois destes passos são efetuados, a aplicação é configurada toouse Olá Redis fornecedor de Cache de saída.</span><span class="sxs-lookup"><span data-stu-id="5b530-146">Once these steps are performed, your application is configured toouse hello Redis Output Cache Provider.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5b530-147">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="5b530-147">Next steps</span></span>
<span data-ttu-id="5b530-148">Veja Olá [fornecedor de estado de sessão do ASP.NET para a Cache de Redis do Azure](cache-aspnet-session-state-provider.md).</span><span class="sxs-lookup"><span data-stu-id="5b530-148">Check out hello [ASP.NET Session State Provider for Azure Redis Cache](cache-aspnet-session-state-provider.md).</span></span>

