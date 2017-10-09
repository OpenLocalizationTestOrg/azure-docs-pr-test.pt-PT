As aplicações de .NET podem utilizar Olá **stackexchange. redis** cliente de cache, o que pode ser configurado no Visual Studio com um pacote NuGet que simplifica a configuração de Olá das aplicações de cliente de cache. 

> [!NOTE]
> Para obter mais informações, consulte Olá [stackexchange. redis](http://github.com/StackExchange/StackExchange.Redis) github página e Olá [documentação do cliente de cache stackexchange. redis](http://github.com/StackExchange/StackExchange.Redis#documentation).
> 
> 

tooconfigure uma aplicação de cliente no Visual Studio com Olá pacote NuGet stackexchange. redis, clique no projeto Olá no **Explorador de soluções** e escolha **gerir pacotes NuGet**. 

![Gerir pacotes NuGet](media/redis-cache-configure-stackexchange-redis-nuget/redis-cache-manage-nuget-menu.png)

Tipo **stackexchange. redis** ou **StrongName** na caixa de texto de pesquisa de Olá, selecione a versão pretendida do Olá partir dos resultados de Olá e clique em **instalar**.

> [!NOTE]
> Se preferir toouse uma versão com nome seguro do Olá **stackexchange. redis** biblioteca de clientes, escolha **StrongName**; caso contrário, escolha **stackexchange. redis**.
> 
> 

![Pacote NuGet StackExchange.Redis](media/redis-cache-configure-stackexchange-redis-nuget/redis-cache-stackexchange-redis.png)

Olá NuGet pacote transfere e adiciona Olá necessário referências de assemblagem para a sua tooaccess de aplicação de cliente a Cache de Redis do Azure com o cliente de cache stackexchange. redis Olá.

> [!NOTE]
> Se anteriormente tiver configurado o projeto toouse stackexchange. redis, pode procurar o pacote de toohello de atualizações de Olá **Gestor de pacotes NuGet**. toocheck para e versões de instalação atualizada do Olá pacote NuGet stackexchange. redis, clique em **atualizações** no Olá Olá **Gestor de pacotes NuGet** janela. Se estiver disponível uma atualização toohello pacote NuGet stackexchange. redis, pode atualizar a versão do projeto toouse Olá atualizado.
> 
> 

Também pode instalar Olá pacote NuGet stackexchange. redis, clicando em **Gestor de pacotes NuGet**, **consola do Gestor de pacotes** de Olá **ferramentas** e, em execução Olá os seguintes comandos do Olá **consola do Gestor de pacotes** janela.
    
```
Install-Package StackExchange.Redis
```
