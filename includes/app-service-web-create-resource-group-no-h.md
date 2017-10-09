Criar um grupo de recursos com Olá [criar grupo az](/cli/azure/group#create) comando.

[!INCLUDE [resource group intro text](resource-group.md)]

Olá exemplo seguinte cria um grupo de recursos denominado *myResourceGroup* no Olá *westeurope* localização.

```azurecli-interactive
az group create --name myResourceGroup --location westeurope
```

Geralmente criar o recurso do grupo e Olá recursos numa região perto de si. as localizações de todos os toosee suportado para Web Apps do Azure, execute Olá `az appservice list-locations` comando. 
