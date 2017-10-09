<span data-ttu-id="18b2b-101">instância do tooconnect tooan a Cache de Redis do Azure, os clientes de cache tem de nome de anfitrião Olá, portas e as chaves da cache de Olá.</span><span class="sxs-lookup"><span data-stu-id="18b2b-101">tooconnect tooan Azure Redis Cache instance, cache clients need hello host name, ports, and keys of hello cache.</span></span> <span data-ttu-id="18b2b-102">Alguns clientes podem mencionar itens toothese por nomes ligeiramente diferentes.</span><span class="sxs-lookup"><span data-stu-id="18b2b-102">Some clients may refer toothese items by slightly different names.</span></span> <span data-ttu-id="18b2b-103">Pode obter estas informações no Olá portal do Azure ou através de ferramentas da linha de comandos, como o CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="18b2b-103">You can retrieve this information in hello Azure portal or by using command-line tools such as Azure CLI.</span></span>

### <a name="retrieve-host-name-ports-and-access-keys-using-hello-azure-portal"></a><span data-ttu-id="18b2b-104">Obter nome de anfitrião, portas e as chaves de acesso utilizando Olá Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="18b2b-104">Retrieve host name, ports, and access keys using hello Azure Portal</span></span>
<span data-ttu-id="18b2b-105">tooretrieve alojar nome, portas e as chaves de acesso utilizando Olá Portal do Azure, [procurar](../articles/redis-cache/cache-configure.md#configure-redis-cache-settings) tooyour cache no Olá [portal do Azure](https://portal.azure.com) e clique em **chaves de acesso** e  **Propriedades** no Olá **menu recursos**.</span><span class="sxs-lookup"><span data-stu-id="18b2b-105">tooretrieve host name, ports, and access keys using hello Azure Portal, [browse](../articles/redis-cache/cache-configure.md#configure-redis-cache-settings) tooyour cache in hello [Azure portal](https://portal.azure.com) and click **Access keys** and **Properties** in hello **Resource menu**.</span></span> 

![Definições da cache de Redis](media/redis-cache-access-keys/redis-cache-hostname-ports-keys.png)

### <a name="retrieve-host-name-ports-and-access-keys-using-azure-cli"></a><span data-ttu-id="18b2b-107">Obtenha o nome do anfitrião, as portas e as chaves de acesso através da CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="18b2b-107">Retrieve host name, ports, and access keys using Azure CLI</span></span>
<span data-ttu-id="18b2b-108">nome de anfitrião de Olá tooretrieve e portas a utilizar o Azure CLI 2.0 pode chamar [mostrar de redis az](https://docs.microsoft.com/cli/azure/redis#show)e as chaves de Olá tooretrieve pode chamar [az redis lista chaves](https://docs.microsoft.com/cli/azure/redis#list-keys).</span><span class="sxs-lookup"><span data-stu-id="18b2b-108">tooretrieve hello host name and ports using Azure CLI 2.0 you can call [az redis show](https://docs.microsoft.com/cli/azure/redis#show), and tooretrieve hello keys you can call [az redis list-keys](https://docs.microsoft.com/cli/azure/redis#list-keys).</span></span> <span data-ttu-id="18b2b-109">Olá seguinte script chama estes dois comandos e echos Olá hostname, portas e consola de toohello de chaves.</span><span class="sxs-lookup"><span data-stu-id="18b2b-109">hello following script calls these two commands and echos hello hostname, ports, and keys toohello console.</span></span>

```azurecli
#/bin/bash

# Retrieve hello hostname, ports, and keys for contosoCache located in contosoGroup

# Retrieve hello hostname and ports for an Azure Redis Cache instance
redis=($(az redis show --name contosoCache --resource-group contosoGroup --query [hostName,enableNonSslPort,port,sslPort] --output tsv))

# Retrieve hello keys for an Azure Redis Cache instance
keys=($(az redis list-keys --name contosoCache --resource-group contosoGroup --query [primaryKey,secondaryKey] --output tsv))

# Display hello retrieved hostname, keys, and ports
echo "Hostname:" ${redis[0]}
echo "Non SSL Port:" ${redis[2]}
echo "Non SSL Port Enabled:" ${redis[1]}
echo "SSL Port:" ${redis[3]}
echo "Primary Key:" ${keys[0]}
echo "Secondary Key:" ${keys[1]}
```

<span data-ttu-id="18b2b-110">Para obter mais informações sobre este script, consulte [obter hostname Olá, portas e as chaves para a Cache de Redis do Azure](../articles/redis-cache/scripts/cache-keys-ports.md).</span><span class="sxs-lookup"><span data-stu-id="18b2b-110">For more information about this script, see [Get hello hostname, ports, and keys for Azure Redis Cache](../articles/redis-cache/scripts/cache-keys-ports.md).</span></span> <span data-ttu-id="18b2b-111">Para obter mais informações sobre a CLI 2.0 do Azure, consulte [Install Azure CLI 2.0 (Instalar a CLI 2.0 do Azure)](https://docs.microsoft.com/cli/azure/install-azure-cli) e [Get started with Azure CLI 2.0 (Introdução à CLI 2.0 do Azure)](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="18b2b-111">For more information on Azure CLI 2.0, see [Install Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli) and [Get started with Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli).</span></span>
