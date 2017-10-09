instância do tooconnect tooan a Cache de Redis do Azure, os clientes de cache tem de nome de anfitrião Olá, portas e as chaves da cache de Olá. Alguns clientes podem mencionar itens toothese por nomes ligeiramente diferentes. Pode obter estas informações no Olá portal do Azure ou através de ferramentas da linha de comandos, como o CLI do Azure.

### <a name="retrieve-host-name-ports-and-access-keys-using-hello-azure-portal"></a>Obter nome de anfitrião, portas e as chaves de acesso utilizando Olá Portal do Azure
tooretrieve alojar nome, portas e as chaves de acesso utilizando Olá Portal do Azure, [procurar](../articles/redis-cache/cache-configure.md#configure-redis-cache-settings) tooyour cache no Olá [portal do Azure](https://portal.azure.com) e clique em **chaves de acesso** e  **Propriedades** no Olá **menu recursos**. 

![Definições da cache de Redis](media/redis-cache-access-keys/redis-cache-hostname-ports-keys.png)

### <a name="retrieve-host-name-ports-and-access-keys-using-azure-cli"></a>Obtenha o nome do anfitrião, as portas e as chaves de acesso através da CLI do Azure
nome de anfitrião de Olá tooretrieve e portas a utilizar o Azure CLI 2.0 pode chamar [mostrar de redis az](https://docs.microsoft.com/cli/azure/redis#show)e as chaves de Olá tooretrieve pode chamar [az redis lista chaves](https://docs.microsoft.com/cli/azure/redis#list-keys). Olá seguinte script chama estes dois comandos e echos Olá hostname, portas e consola de toohello de chaves.

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

Para obter mais informações sobre este script, consulte [obter hostname Olá, portas e as chaves para a Cache de Redis do Azure](../articles/redis-cache/scripts/cache-keys-ports.md). Para obter mais informações sobre a CLI 2.0 do Azure, consulte [Install Azure CLI 2.0 (Instalar a CLI 2.0 do Azure)](https://docs.microsoft.com/cli/azure/install-azure-cli) e [Get started with Azure CLI 2.0 (Introdução à CLI 2.0 do Azure)](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli).
