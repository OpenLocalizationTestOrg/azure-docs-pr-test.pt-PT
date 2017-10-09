## <a name="create-a-resource-group"></a><span data-ttu-id="00603-101">Criar um grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="00603-101">Create a resource group</span></span>

<span data-ttu-id="00603-102">Criar um grupo de recursos com Olá [criar grupo az](/cli/azure/group#create) comando.</span><span class="sxs-lookup"><span data-stu-id="00603-102">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="00603-103">Um grupo de recursos do Azure é um contentor lógico no qual os recursos do Azure são implementados e geridos.</span><span class="sxs-lookup"><span data-stu-id="00603-103">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="00603-104">Olá exemplo seguinte cria um grupo de recursos denominado *myResourceGroup* no Olá *eastus* localização.</span><span class="sxs-lookup"><span data-stu-id="00603-104">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location.</span></span>

```azurecli-interactive 
az group create --name myResourceGroup --location eastus
```

## <a name="create-a-virtual-machine"></a><span data-ttu-id="00603-105">Criar uma máquina virtual</span><span class="sxs-lookup"><span data-stu-id="00603-105">Create a virtual machine</span></span>

<span data-ttu-id="00603-106">Criar uma VM com Olá [az vm criar](/cli/azure/vm#create) comando.</span><span class="sxs-lookup"><span data-stu-id="00603-106">Create a VM with hello [az vm create](/cli/azure/vm#create) command.</span></span> 

<span data-ttu-id="00603-107">Olá exemplo seguinte cria uma VM chamada *myVM* e cria as chaves SSH se estes ainda não existir numa localização chave predefinido.</span><span class="sxs-lookup"><span data-stu-id="00603-107">hello following example creates a VM named *myVM* and creates SSH keys if they do not already exist in a default key location.</span></span> <span data-ttu-id="00603-108">toouse específicos de um conjunto de chaves, utilize Olá `--ssh-key-value` opção.</span><span class="sxs-lookup"><span data-stu-id="00603-108">toouse a specific set of keys, use hello `--ssh-key-value` option.</span></span>  

```azurecli-interactive 
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys
```

<span data-ttu-id="00603-109">Quando tiver sido criado Olá VM, Olá CLI do Azure mostra informações toohello semelhante seguinte o exemplo.</span><span class="sxs-lookup"><span data-stu-id="00603-109">When hello VM has been created, hello Azure CLI shows information similar toohello following example.</span></span> <span data-ttu-id="00603-110">Tome nota do Olá `publicIpAddress`.</span><span class="sxs-lookup"><span data-stu-id="00603-110">Take note of hello `publicIpAddress`.</span></span> <span data-ttu-id="00603-111">Este endereço é utilizado tooaccess Olá VM.</span><span class="sxs-lookup"><span data-stu-id="00603-111">This address is used tooaccess hello VM.</span></span>

```azurecli-interactive 
{
  "fqdns": "",
  "id": "/subscriptions/<subscription ID>/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM",
  "location": "eastus",
  "macAddress": "00-0D-3A-23-9A-49",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.4",
  "publicIpAddress": "40.68.254.142",
  "resourceGroup": "myResourceGroup"
}
```



## <a name="open-port-80-for-web-traffic"></a><span data-ttu-id="00603-112">Abrir a porta 80 para o tráfego da Web</span><span class="sxs-lookup"><span data-stu-id="00603-112">Open port 80 for web traffic</span></span> 

<span data-ttu-id="00603-113">Por predefinição, apenas as ligações de SSH são permitidas para VMs com Linux implementados no Azure.</span><span class="sxs-lookup"><span data-stu-id="00603-113">By default, only SSH connections are allowed into Linux VMs deployed in Azure.</span></span> <span data-ttu-id="00603-114">Porque esta VM vai toobe um servidor web, terá de tooopen porta 80 do Olá internet.</span><span class="sxs-lookup"><span data-stu-id="00603-114">Because this VM is going toobe a web server, you need tooopen port 80 from hello internet.</span></span> <span data-ttu-id="00603-115">Olá utilize [az vm open-porta](/cli/azure/vm#open-port) Olá do comando tooopen pretendido porta.</span><span class="sxs-lookup"><span data-stu-id="00603-115">Use hello [az vm open-port](/cli/azure/vm#open-port) command tooopen hello desired port.</span></span>  
 
```azurecli-interactive 
az vm open-port --port 80 --resource-group myResourceGroup --name myVM
```
## <a name="ssh-into-your-vm"></a><span data-ttu-id="00603-116">Aceder através de SSH à VM</span><span class="sxs-lookup"><span data-stu-id="00603-116">SSH into your VM</span></span>


<span data-ttu-id="00603-117">Se já não souber Olá endereço IP público da sua VM, execute Olá [lista de ip público de rede az](/cli/azure/network/public-ip#list) comando:</span><span class="sxs-lookup"><span data-stu-id="00603-117">If you don't already know hello public IP address of your VM, run hello [az network public-ip list](/cli/azure/network/public-ip#list) command:</span></span>


```azurecli-interactive
az network public-ip list --resource-group myResourceGroup --query [].ipAddress
```

<span data-ttu-id="00603-118">Toocreate uma sessão SSH com a máquina virtual de Olá de comando seguinte Olá de utilização.</span><span class="sxs-lookup"><span data-stu-id="00603-118">Use hello following command toocreate an SSH session with hello virtual machine.</span></span> <span data-ttu-id="00603-119">Substitua o endereço IP público correto por Olá da sua máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="00603-119">Substitute hello correct public IP address of your virtual machine.</span></span> <span data-ttu-id="00603-120">Neste exemplo, endereço IP Olá é *40.68.254.142*.</span><span class="sxs-lookup"><span data-stu-id="00603-120">In this example, hello IP address is *40.68.254.142*.</span></span>

```bash
ssh azureuser@40.68.254.142
```

