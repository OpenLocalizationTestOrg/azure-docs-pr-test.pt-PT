Criar um grupo de recursos com Olá [criar grupo az](/cli/azure/group#create) comando.

[!INCLUDE [resource group intro text](resource-group.md)]

Olá exemplo seguinte cria um grupo de recursos denominado *myResourceGroup* no Olá *westeurope* localização.

```azurecli-interactive
az group create --name myResourceGroup --location westeurope
```

toosee Olá as localizações disponíveis, executadas Olá `az appservice list-locations` comando. Geralmente, os recursos são criados numa região perto de si.
