toocreate uma cache, sessão pela primeira vez no toohello [portal do Azure](https://portal.azure.com)e clique em **novo** > **bases de dados** > **a Cache de Redis**.

> [!NOTE]
> Se não tiver uma conta do Azure, pode [Criar uma conta do Azure gratuita](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=redis_cache_hero) em apenas alguns minutos.
> 
> 

![Nova cache](media/redis-cache-create/redis-cache-new-cache-menu.png)

> [!NOTE]
> Além disso toocreating coloca em cache no Olá portal do Azure, pode também criar com o Resource Manager modelos, o PowerShell ou o CLI do Azure.
> 
> * toocreate uma cache com modelos do Resource Manager, consulte [criar uma cache de Redis através de um modelo](../articles/redis-cache/cache-redis-cache-arm-provision.md).
> * toocreate uma cache com o Azure PowerShell, consulte [gerir Cache de Redis do Azure com o Azure PowerShell](../articles/redis-cache/cache-howto-manage-redis-cache-powershell.md).
> * toocreate uma cache com a CLI do Azure, consulte [como toocreate e gerir Olá Interface de linha de comandos do Azure (CLI do Azure) a utilizar a Cache de Redis do Azure](../articles/redis-cache/cache-manage-cli.md).
> 
> 

No Olá **nova Cache de Redis** painel, especifique Olá configuração pretendida para a cache de Olá.

![Criar cache](media/redis-cache-create/redis-cache-cache-create.png) 

* No **nome Dns**, introduza um toouse de nome de cache exclusivo para o ponto final de cache Olá. nome da cache Olá tem de ser uma cadeia entre 1 e 63 carateres e conter apenas números, letras e Olá `-` caráter. Olá nome da cache não pode começar nem terminar com Olá `-` caráter e consecutivos `-` carateres não são válidos.
* Para **subscrição**, selecione Olá subscrição do Azure que pretende que toouse para a cache de Olá. Se a sua conta tiver apenas uma subscrição, será selecionada automaticamente e Olá **subscrição** pendente não será apresentado.
* Em **Grupo de recursos**, selecione ou crie um grupo de recursos para a sua cache. Para obter mais informações, consulte [toomanage de grupos de utilização de recursos, os recursos do Azure](../articles/azure-resource-manager/resource-group-overview.md). 
* Utilize **localização** toospecify Olá localização geográfica na qual a sua cache será alojada. Para melhor desempenho Olá, a Microsoft recomenda vivamente que crie cache Olá no Olá mesma região que a aplicação de cliente de cache de Olá.
* Utilize **escalão de preço** tooselect Olá pretendido tamanho da cache e funcionalidades.
* **Cluster de redis** permite-lhe toocreate caches superiores a 53 GB e tooshard dados em vários nós de Redis. Para obter mais informações, consulte [como tooconfigure clustering para uma Cache de Redis do Azure Premium](../articles/redis-cache/cache-how-to-premium-clustering.md).
* **Persistência de redis** oferece Olá capacidade toopersist tooan sua cache conta de armazenamento do Azure. Para obter instruções sobre como configurar a persistência, consulte [como tooconfigure persistência para uma Cache de Redis do Azure Premium](../articles/redis-cache/cache-how-to-premium-persistence.md).
* **Rede virtual** fornece segurança e isolamento melhorados ao restringir o acesso tooyour cache tooonly aos clientes dentro Olá especificado rede Virtual do Azure. Pode utilizar todas as funcionalidades de Olá da VNet, tais como sub-redes, políticas de controlo de acesso e outra funcionalidades toofurther restringir acesso tooRedis. Para obter mais informações, consulte [como suportam o tooconfigure rede Virtual para uma Cache de Redis do Azure Premium](../articles/redis-cache/cache-how-to-premium-vnet.md).
* Por predefinição, o acesso não SSL está desativado para as novas caches. porta não SSL do tooenable Olá, verificação **desbloquear a porta (não SSL encriptado) de 6379**.

Depois de novas opções de cache Olá estiverem configuradas, clique em **criar**. Pode demorar alguns minutos para Olá cache toobe criado. Estado de Olá toocheck, pode monitorizar o progresso de Olá no startboard Olá. Depois de ter sido criado a cache de Olá, a nova cache tem um **executar** estado e está pronto para ser utilizado com [predefinições](../articles/redis-cache/cache-configure.md#default-redis-server-configuration).

![Cache criada](media/redis-cache-create/redis-cache-cache-created.png)

