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
# <a name="aspnet-output-cache-provider-for-azure-redis-cache"></a>Fornecedor de Cache de saída do ASP.NET para o Azure Redis Cache
Olá Redis fornecedor de Cache de saída é um mecanismo de armazenamento de fora do processo para dados da cache de saída. Estes dados são especificamente para as respostas HTTP completas (página a cache de saída). fornecedor de Olá plugs para Olá nova saída cache fornecedor ponto de extensibilidade que foi introduzido no ASP.NET 4.

Olá toouse Redis fornecedor de Cache de saída, primeiro de configurar a cache e, em seguida, configure a sua aplicação ASP.NET, utilizando o pacote de Redis NuGet de fornecedor de Cache de saída Olá. Este tópico fornece orientações sobre como configurar a sua Olá toouse de aplicação Redis fornecedor de Cache de saída. Para obter mais informações sobre como criar e configurar uma instância da Cache de Redis do Azure, consulte [criar uma cache](cache-dotnet-how-to-use-azure-redis-cache.md#create-a-cache).

## <a name="store-aspnet-page-output-in-hello-cache"></a>Armazenar a saída de páginas do ASP.NET na cache de Olá
tooconfigure uma aplicação de cliente no Visual Studio com o pacote de Redis NuGet de estado de sessão de Cache de Olá, clique em **Gestor de pacotes NuGet**, **consola do Gestor de pacotes** de Olá **ferramentas** menu.

Execute hello os seguintes comandos do Olá `Package Manager Console` janela.
    
```
Install-Package Microsoft.Web.RedisOutputCacheProvider
```

pacote de Redis NuGet de fornecedor de Cache de saída Olá tem uma dependência no pacote de StrongName Olá. Se o pacote de StrongName Olá não está presente no projeto, está instalado. Para obter mais informações sobre o pacote de Redis NuGet de fornecedor de Cache de saída Olá, consulte Olá [RedisOutputCacheProvider](https://www.nuget.org/packages/Microsoft.Web.RedisOutputCacheProvider/) página NuGet.

>[!NOTE]
>Adição toohello com nome seguro StrongName pacote, há também Olá stackexchange. redis não-com nome seguro versão. Caso contrário, se o projeto está a utilizar Olá não-com nome seguro stackexchange. redis versão que tem de o desinstalar, obter nomenclatura conflitos no seu projeto. Para obter mais informações sobre estes pacotes, consulte [clientes de cache de .NET configurar](cache-dotnet-how-to-use-azure-redis-cache.md#configure-the-cache-clients).
>
>

Olá NuGet pacote transfere e adiciona Olá necessário assemblagem referencia e adiciona Olá secção a seguir no seu ficheiro Web. config. Esta secção contém configuração necessários de Olá para sua Olá de toouse de aplicação de ASP.NET Redis fornecedor de Cache de saída.

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

Olá comentado secção fornece um exemplo de atributos de Olá e as definições de exemplo para cada atributo.

Configurar atributos Olá com valores de Olá do painel da cache no portal do Microsoft Azure Olá e configure Olá outros valores conforme pretendido. Para obter instruções sobre como aceder as propriedades da cache, consulte [Configure Redis cache as definições](cache-configure.md#configure-redis-cache-settings).

* **anfitrião** – especifique o ponto final da cache.
* **porta** – utilizar a porta não SSL ou a porta SSL, dependendo das definições de ssl Olá.
* **accessKey** – utilizar a chave primária ou secundária de Olá para a sua cache.
* **SSL** – VERDADEIRO se quiser comunicações de cliente de cache/toosecure com ssl; caso contrário FALSO. Ser se Olá toospecify da porta do correto.
  * porta do Olá não SSL está desativada por predefinição para novas caches. Especifica verdadeiro para esta Olá toouse de definição porta SSL. Para obter mais informações sobre como ativar a porta não SSL de Olá, consulte Olá [portas de acesso](cache-configure.md#access-ports) secção Olá [configurar uma cache](cache-configure.md) tópico.
* **databaseId** – especificado que toouse de base de dados para a cache de saída de dados. Se não for especificado, é utilizado o valor predefinido de Olá 0.
* **applicationName** – chaves são armazenadas no redis como `<AppName>_<SessionId>_Data`. Este esquema de nomenclatura permite vários Olá de tooshare aplicações mesma chave. Este parâmetro é opcional e se não o a fornecer um valor predefinido é utilizado.
* **connectionTimeoutInMilliseconds** – esta definição permite-lhe toooverride Olá connectTimeout no cliente do Olá stackexchange. redis. Se não for especificado, Olá connectTimeout predefinição 5000 é utilizada. Para obter mais informações, consulte [modelo de configuração stackexchange. redis](http://go.microsoft.com/fwlink/?LinkId=398705).
* **operationTimeoutInMilliseconds** – esta definição permite-lhe toooverride Olá syncTimeout no cliente do Olá stackexchange. redis. Se não for especificado, é utilizada Olá syncTimeout predefinição 1000. Para obter mais informações, consulte [modelo de configuração stackexchange. redis](http://go.microsoft.com/fwlink/?LinkId=398705).

Adicione uma página de tooeach diretiva OutputCache para o qual pretende a saída de Olá toocache.

```
<%@ OutputCache Duration="60" VaryByParam="*" %>
```

No exemplo anterior Olá, Olá página dados permanecem na cache de Olá em cache durante 60 segundos e uma versão diferente da página Olá é colocado em cache para cada combinação de parâmetro. Para mais informações sobre a diretiva OutputCache Olá, consulte [ @OutputCache ](http://go.microsoft.com/fwlink/?linkid=320837).

Depois destes passos são efetuados, a aplicação é configurada toouse Olá Redis fornecedor de Cache de saída.

## <a name="next-steps"></a>Passos seguintes
Veja Olá [fornecedor de estado de sessão do ASP.NET para a Cache de Redis do Azure](cache-aspnet-session-state-provider.md).

