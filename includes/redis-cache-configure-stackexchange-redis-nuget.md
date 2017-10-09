<span data-ttu-id="f898e-101">As aplicações de .NET podem utilizar Olá **stackexchange. redis** cliente de cache, o que pode ser configurado no Visual Studio com um pacote NuGet que simplifica a configuração de Olá das aplicações de cliente de cache.</span><span class="sxs-lookup"><span data-stu-id="f898e-101">.NET applications can use hello **StackExchange.Redis** cache client, which can be configured in Visual Studio using a NuGet package that simplifies hello configuration of cache client applications.</span></span> 

> [!NOTE]
> <span data-ttu-id="f898e-102">Para obter mais informações, consulte Olá [stackexchange. redis](http://github.com/StackExchange/StackExchange.Redis) github página e Olá [documentação do cliente de cache stackexchange. redis](http://github.com/StackExchange/StackExchange.Redis#documentation).</span><span class="sxs-lookup"><span data-stu-id="f898e-102">For more information, see hello [StackExchange.Redis](http://github.com/StackExchange/StackExchange.Redis) github page and  hello [StackExchange.Redis cache client documentation](http://github.com/StackExchange/StackExchange.Redis#documentation).</span></span>
> 
> 

<span data-ttu-id="f898e-103">tooconfigure uma aplicação de cliente no Visual Studio com Olá pacote NuGet stackexchange. redis, clique no projeto Olá no **Explorador de soluções** e escolha **gerir pacotes NuGet**.</span><span class="sxs-lookup"><span data-stu-id="f898e-103">tooconfigure a client application in Visual Studio using hello StackExchange.Redis NuGet package, right-click hello project in **Solution Explorer** and choose **Manage NuGet Packages**.</span></span> 

![Gerir pacotes NuGet](media/redis-cache-configure-stackexchange-redis-nuget/redis-cache-manage-nuget-menu.png)

<span data-ttu-id="f898e-105">Tipo **stackexchange. redis** ou **StrongName** na caixa de texto de pesquisa de Olá, selecione a versão pretendida do Olá partir dos resultados de Olá e clique em **instalar**.</span><span class="sxs-lookup"><span data-stu-id="f898e-105">Type **StackExchange.Redis** or **StackExchange.Redis.StrongName** into hello search text box, select hello desired version from hello results, and click **Install**.</span></span>

> [!NOTE]
> <span data-ttu-id="f898e-106">Se preferir toouse uma versão com nome seguro do Olá **stackexchange. redis** biblioteca de clientes, escolha **StrongName**; caso contrário, escolha **stackexchange. redis**.</span><span class="sxs-lookup"><span data-stu-id="f898e-106">If you prefer toouse a strong-named version of hello **StackExchange.Redis** client library, choose **StackExchange.Redis.StrongName**; otherwise choose **StackExchange.Redis**.</span></span>
> 
> 

![Pacote NuGet StackExchange.Redis](media/redis-cache-configure-stackexchange-redis-nuget/redis-cache-stackexchange-redis.png)

<span data-ttu-id="f898e-108">Olá NuGet pacote transfere e adiciona Olá necessário referências de assemblagem para a sua tooaccess de aplicação de cliente a Cache de Redis do Azure com o cliente de cache stackexchange. redis Olá.</span><span class="sxs-lookup"><span data-stu-id="f898e-108">hello NuGet package downloads and adds hello required assembly references for your client application tooaccess Azure Redis Cache with hello StackExchange.Redis cache client.</span></span>

> [!NOTE]
> <span data-ttu-id="f898e-109">Se anteriormente tiver configurado o projeto toouse stackexchange. redis, pode procurar o pacote de toohello de atualizações de Olá **Gestor de pacotes NuGet**.</span><span class="sxs-lookup"><span data-stu-id="f898e-109">If you have previously configured your project toouse StackExchange.Redis, you can check for updates toohello package from hello **NuGet Package Manager**.</span></span> <span data-ttu-id="f898e-110">toocheck para e versões de instalação atualizada do Olá pacote NuGet stackexchange. redis, clique em **atualizações** no Olá Olá **Gestor de pacotes NuGet** janela.</span><span class="sxs-lookup"><span data-stu-id="f898e-110">toocheck for and install updated versions of hello StackExchange.Redis NuGet package, click **Updates** in hello hello **NuGet Package Manager** window.</span></span> <span data-ttu-id="f898e-111">Se estiver disponível uma atualização toohello pacote NuGet stackexchange. redis, pode atualizar a versão do projeto toouse Olá atualizado.</span><span class="sxs-lookup"><span data-stu-id="f898e-111">If an update toohello StackExchange.Redis NuGet package is available, you can update your project toouse hello updated version.</span></span>
> 
> 

<span data-ttu-id="f898e-112">Também pode instalar Olá pacote NuGet stackexchange. redis, clicando em **Gestor de pacotes NuGet**, **consola do Gestor de pacotes** de Olá **ferramentas** e, em execução Olá os seguintes comandos do Olá **consola do Gestor de pacotes** janela.</span><span class="sxs-lookup"><span data-stu-id="f898e-112">You can also install hello StackExchange.Redis NuGet package by clicking **NuGet Package Manager**, **Package Manager Console** from hello **Tools** menu, and running hello following command from hello **Package Manager Console** window.</span></span>
    
```
Install-Package StackExchange.Redis
```
