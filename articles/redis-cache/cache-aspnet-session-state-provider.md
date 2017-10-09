---
title: "aaaCache fornecedor de estado de sessão do ASP.NET | Microsoft Docs"
description: "Saiba como o estado de sessão do ASP.NET de toostore utilizando a Cache de Redis do Azure"
services: redis-cache
documentationcenter: na
author: steved0x
manager: douge
editor: tysonn
ms.assetid: 192f384c-836a-479a-bb65-8c3e6d6522bb
ms.service: cache
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: cache-redis
ms.workload: tbd
ms.date: 05/01/2017
ms.author: sdanie
ms.openlocfilehash: 9ea84cf67b9314b15dce696f596d399921194510
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="aspnet-session-state-provider-for-azure-redis-cache"></a>Fornecedor de Estado da Sessão ASP.NET para a Cache de Redis do Azure
Cache de Redis do Azure fornece um fornecedor de estado de sessão que pode utilizar toostore o estado da sessão num cache em vez de memória ou num servidor SQL da base de dados. toouse Olá colocação em cache no fornecedor de estado de sessão, primeiro de configurar a cache e, em seguida, configure a sua aplicação ASP.NET para cache com o pacote de Redis NuGet de estado de sessão de Cache de Olá.

Muitas vezes, não é prático num tooavoid de aplicação de nuvem do mundo real armazenar alguma forma de estado para uma sessão de utilizador, mas alguns abordagens impacto no desempenho e escalabilidade mais do que outras pessoas. Se tiver estado toostore, melhor solução de Olá tookeep Olá quantidade de estado pequeno e armazene-o em cookies. Se que não é exequível, Olá seguinte melhor solução é toouse ASP.NET o estado da sessão com um fornecedor de cache distribuída, dentro da memória. Olá pior de um ponto de vista de desempenho e a escalabilidade é toouse um fornecedor de estado de sessão de segurança da base de dados. Este tópico fornece orientações sobre como utilizar Olá fornecedor de estado de sessão do ASP.NET para a Cache de Redis do Azure. Para obter informações sobre outras opções de estado de sessão, consulte [opções de estado da sessão ASP.NET](#aspnet-session-state-options).

## <a name="store-aspnet-session-state-in-hello-cache"></a>Armazenar o estado da sessão ASP.NET na cache de Olá
tooconfigure uma aplicação de cliente no Visual Studio com o pacote de Redis NuGet de estado de sessão de Cache de Olá, clique em **Gestor de pacotes NuGet**, **consola do Gestor de pacotes** de Olá **ferramentas** menu.

Execute hello os seguintes comandos do Olá `Package Manager Console` janela.
    
```
Install-Package Microsoft.Web.RedisSessionStateProvider
```

> [!IMPORTANT]
> Se estiver a utilizar Olá funcionalidade de clustering do escalão premium de Olá, tem de utilizar [RedisSessionStateProvider](https://www.nuget.org/packages/Microsoft.Web.RedisSessionStateProvider) 2.0.1 ou superior ou de uma exceção é emitida. Mover too2.0.1 ou superior, é uma alteração inovadora; Para obter mais informações, consulte [v2.0.0 interrompendo detalhes de alteração](https://github.com/Azure/aspnet-redis-providers/wiki/v2.0.0-Breaking-Change-Details). No momento de Olá desta atualização de artigo, a versão atual do Olá deste pacote é 2.2.3.
> 
> 

pacote de Redis NuGet de fornecedor de estado de sessão de Olá tem uma dependência no pacote de StrongName Olá. Se o pacote de StrongName Olá não está presente no projeto, está instalado.

>[!NOTE]
>Adição toohello com nome seguro StrongName pacote, há também Olá stackexchange. redis não-com nome seguro versão. Caso contrário, se o projeto está a utilizar Olá não-com nome seguro stackexchange. redis versão que tem de o desinstalar, obter nomenclatura conflitos no seu projeto. Para obter mais informações sobre estes pacotes, consulte [clientes de cache de .NET configurar](cache-dotnet-how-to-use-azure-redis-cache.md#configure-the-cache-clients).
>
>

Olá NuGet pacote transfere e adiciona Olá necessário assemblagem referencia e adiciona Olá secção a seguir no seu ficheiro Web. config. Esta secção contém configuração necessários de Olá para sua Olá de toouse de aplicação de ASP.NET fornecedor de estado de sessão de Cache de Redis.

```xml
<sessionState mode="Custom" customProvider="MySessionStateStore">
    <providers>
    <!--
    <add name="MySessionStateStore"
           host = "127.0.0.1" [String]
        port = "" [number]
        accessKey = "" [String]
        ssl = "false" [true|false]
        throwOnError = "true" [true|false]
        retryTimeoutInMilliseconds = "0" [number]
        databaseId = "0" [number]
        applicationName = "" [String]
        connectionTimeoutInMilliseconds = "5000" [number]
        operationTimeoutInMilliseconds = "5000" [number]
    />
    -->
    <add name="MySessionStateStore" type="Microsoft.Web.Redis.RedisSessionStateProvider" host="127.0.0.1" accessKey="" ssl="false"/>
    </providers>
</sessionState>
```

Olá comentado secção fornece um exemplo de atributos de Olá e as definições de exemplo para cada atributo.

Configurar atributos Olá com valores de Olá do painel da cache no portal do Microsoft Azure Olá e configure Olá outros valores conforme pretendido. Para obter instruções sobre como aceder as propriedades da cache, consulte [Configure Redis cache as definições](cache-configure.md#configure-redis-cache-settings).

* **anfitrião** – especifique o ponto final da cache.
* **porta** – utilizar a porta não SSL ou a porta SSL, dependendo das definições de ssl Olá.
* **accessKey** – utilizar a chave primária ou secundária de Olá para a sua cache.
* **SSL** – VERDADEIRO se quiser comunicações de cliente de cache/toosecure com ssl; caso contrário FALSO. Ser se Olá toospecify da porta do correto.
  * porta do Olá não SSL está desativada por predefinição para novas caches. Especifica verdadeiro para esta Olá toouse de definição porta SSL. Para obter mais informações sobre como ativar a porta não SSL de Olá, consulte Olá [portas de acesso](cache-configure.md#access-ports) secção Olá [configurar uma cache](cache-configure.md) tópico.
* **throwOnError** – VERDADEIRO se quiser toobe uma exceção emitida se houver uma falha, ou FALSO se pretende Olá operação toofail silenciosamente. Pode verificar a existência de uma falha ao verificar a propriedade de Microsoft.Web.Redis.RedisSessionStateProvider.LastException estática Olá. Olá predefinição é verdadeiro.
* **retryTimeoutInMilliseconds** – operações que não são repetidas durante este intervalo, especificado em milissegundos. Volte a tentar primeiro Olá ocorre após 20 milissegundos e, em seguida, as repetições ocorrem a cada segundo até que o intervalo de retryTimeoutInMilliseconds Olá expira. Imediatamente após este intervalo, operação Olá é repetida uma vez final. Se continuar a operação de Olá falhar, Olá é emitida exceção novamente chamador toohello, dependendo da definição de throwOnError Olá. valor predefinido de Olá for 0, o que não significa nenhuma tentativas.
* **databaseId** – Especifica que toouse de base de dados para a cache de saída de dados. Se não for especificado, é utilizado o valor predefinido de Olá 0.
* **applicationName** – chaves são armazenadas no redis como `{<Application Name>_<Session ID>}_Data`. Este esquema de nomenclatura permite que várias aplicações tooshare Olá a mesma instância de Redis. Este parâmetro é opcional e se não o a fornecer um valor predefinido é utilizado.
* **connectionTimeoutInMilliseconds** – esta definição permite-lhe toooverride Olá connectTimeout no cliente do Olá stackexchange. redis. Se não for especificado, Olá connectTimeout predefinição 5000 é utilizada. Para obter mais informações, consulte [modelo de configuração stackexchange. redis](http://go.microsoft.com/fwlink/?LinkId=398705).
* **operationTimeoutInMilliseconds** – esta definição permite-lhe toooverride Olá syncTimeout no cliente do Olá stackexchange. redis. Se não for especificado, é utilizada Olá syncTimeout predefinição 1000. Para obter mais informações, consulte [modelo de configuração stackexchange. redis](http://go.microsoft.com/fwlink/?LinkId=398705).

Para obter mais informações sobre estas propriedades, consulte Olá original blogue anúncio de mensagem em [anunciar ASP.NET sessão fornecedor de estado para Redis](http://blogs.msdn.com/b/webdev/archive/2014/05/12/announcing-asp-net-session-state-provider-for-redis-preview-release.aspx).

Não se esqueça toocomment saída Olá padrão InProc sessão Estado fornecedor secção no seu Web. config.

```xml
<!-- <sessionState mode="InProc"
     customProvider="DefaultSessionProvider">
     <providers>
        <add name="DefaultSessionProvider"
              type="System.Web.Providers.DefaultSessionStateProvider,
                    System.Web.Providers, Version=1.0.0.0, Culture=neutral,
                    PublicKeyToken=31bf3856ad364e35"
              connectionStringName="DefaultConnection" />
      </providers>
</sessionState> -->
```

Depois destes passos são efetuados, a aplicação é configurada toouse Olá fornecedor de estado de sessão de Cache de Redis. Quando utilizar o estado da sessão na sua aplicação, é armazenada numa instância da Cache de Redis do Azure.

> [!IMPORTANT]
> Os dados armazenados na cache de Olá tem de ser serializável, ao contrário dos dados de Olá que podem ser armazenados no Olá predefinido fornecedor de estado de sessão de ASP.NET dentro da memória. Quando é utilizado Olá fornecedor de estado de sessão de Redis, lembre-se de que tipos de dados de Olá que estão a ser armazenados no estado da sessão são serializáveis.
> 
> 

## <a name="aspnet-session-state-options"></a>Opções de estado de sessão do ASP.NET
* No fornecedor de estado da sessão de memória - este fornecedor armazena o estado da sessão Olá na memória. benefício de Olá de utilizar este fornecedor é é simples e rápida. No entanto não pode dimensionar as suas aplicações Web se estiver a utilizar no fornecedor de memória, uma vez que não é distribuída.
* Fornecedor de estado da sessão do SQL Server - este fornecedor armazena Olá estado da sessão no Sql Server. Utilize este fornecedor, se pretender o estado da sessão toostore Olá no armazenamento persistente. Pode dimensionar a sua aplicação Web, mas utilizar o Sql Server para a sessão tem um impacto no desempenho na sua aplicação Web.
* Distribuída na memória sessão fornecedor de estado como Redis Cache sessão fornecedor de estado - oferece este fornecedor Olá melhor de dois mundos. A aplicação Web pode ter um fornecedor de estado de sessão simples, rápidas e dimensionáveis. Porque esta Olá de arquivos de fornecedor estado da sessão cache, a aplicação tem tootake em consideração todas Olá características associadas quando se fala tooa distribuídas na Cache de memória, tais como falhas de rede transitórios. Para melhores práticas em Cache a utilizar, consulte [orientações sobre a colocação em cache](../best-practices-caching.md) da Microsoft Patterns & práticas [Design da aplicação em nuvem do Azure e as diretrizes de implementação](https://github.com/mspnp/azure-guidance).

Para obter mais informações sobre o estado da sessão e outras melhores práticas, consulte [Web desenvolvimento melhores práticas (compilar aplicações de nuvem de mundo Real com o Azure)](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices).

## <a name="next-steps"></a>Passos seguintes
Veja Olá [fornecedor de Cache de saída do ASP.NET para a Cache de Redis do Azure](cache-aspnet-output-cache-provider.md).

