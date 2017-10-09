<span data-ttu-id="b2556-101">Criar um grupo de recursos com Olá [criar grupo az](/cli/azure/group#create) comando.</span><span class="sxs-lookup"><span data-stu-id="b2556-101">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span>

[!INCLUDE [resource group intro text](resource-group.md)]

<span data-ttu-id="b2556-102">Olá exemplo seguinte cria um grupo de recursos denominado *myResourceGroup* no Olá *westeurope* localização.</span><span class="sxs-lookup"><span data-stu-id="b2556-102">hello following example creates a resource group named *myResourceGroup* in hello *westeurope* location.</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location westeurope
```

<span data-ttu-id="b2556-103">Geralmente criar o recurso do grupo e Olá recursos numa região perto de si.</span><span class="sxs-lookup"><span data-stu-id="b2556-103">You generally create your resource group and hello resources in a region near you.</span></span> <span data-ttu-id="b2556-104">as localizações de todos os toosee suportado para Web Apps do Azure, execute Olá `az appservice list-locations` comando.</span><span class="sxs-lookup"><span data-stu-id="b2556-104">toosee all supported locations for Azure Web Apps, run hello `az appservice list-locations` command.</span></span> 
