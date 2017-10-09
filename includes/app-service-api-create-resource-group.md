<span data-ttu-id="8b4cf-101">Criar um grupo de recursos com Olá [criar grupo az](/cli/azure/group#create) comando.</span><span class="sxs-lookup"><span data-stu-id="8b4cf-101">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span>

[!INCLUDE [resource group intro text](resource-group.md)]

<span data-ttu-id="8b4cf-102">Olá exemplo seguinte cria um grupo de recursos denominado *myResourceGroup* no Olá *westeurope* localização.</span><span class="sxs-lookup"><span data-stu-id="8b4cf-102">hello following example creates a resource group named *myResourceGroup* in hello *westeurope* location.</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location westeurope
```

<span data-ttu-id="8b4cf-103">toosee Olá as localizações disponíveis, executadas Olá `az appservice list-locations` comando.</span><span class="sxs-lookup"><span data-stu-id="8b4cf-103">toosee hello available locations, run hello `az appservice list-locations` command.</span></span> <span data-ttu-id="8b4cf-104">Geralmente, os recursos são criados numa região perto de si.</span><span class="sxs-lookup"><span data-stu-id="8b4cf-104">You generally create resources in a region near you.</span></span>
