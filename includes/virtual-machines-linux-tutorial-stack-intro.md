## <a name="create-a-resource-group"></a>Criar um grupo de recursos

Criar um grupo de recursos com Olá [criar grupo az](/cli/azure/group#create) comando. Um grupo de recursos do Azure é um contentor lógico no qual os recursos do Azure são implementados e geridos. 

Olá exemplo seguinte cria um grupo de recursos denominado *myResourceGroup* no Olá *eastus* localização.

```azurecli-interactive 
az group create --name myResourceGroup --location eastus
```

## <a name="create-a-virtual-machine"></a>Criar uma máquina virtual

Criar uma VM com Olá [az vm criar](/cli/azure/vm#create) comando. 

Olá exemplo seguinte cria uma VM chamada *myVM* e cria as chaves SSH se estes ainda não existir numa localização chave predefinido. toouse específicos de um conjunto de chaves, utilize Olá `--ssh-key-value` opção.  

```azurecli-interactive 
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys
```

Quando tiver sido criado Olá VM, Olá CLI do Azure mostra informações toohello semelhante seguinte o exemplo. Tome nota do Olá `publicIpAddress`. Este endereço é utilizado tooaccess Olá VM.

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



## <a name="open-port-80-for-web-traffic"></a>Abrir a porta 80 para o tráfego da Web 

Por predefinição, apenas as ligações de SSH são permitidas para VMs com Linux implementados no Azure. Porque esta VM vai toobe um servidor web, terá de tooopen porta 80 do Olá internet. Olá utilize [az vm open-porta](/cli/azure/vm#open-port) Olá do comando tooopen pretendido porta.  
 
```azurecli-interactive 
az vm open-port --port 80 --resource-group myResourceGroup --name myVM
```
## <a name="ssh-into-your-vm"></a>Aceder através de SSH à VM


Se já não souber Olá endereço IP público da sua VM, execute Olá [lista de ip público de rede az](/cli/azure/network/public-ip#list) comando:


```azurecli-interactive
az network public-ip list --resource-group myResourceGroup --query [].ipAddress
```

Toocreate uma sessão SSH com a máquina virtual de Olá de comando seguinte Olá de utilização. Substitua o endereço IP público correto por Olá da sua máquina virtual. Neste exemplo, endereço IP Olá é *40.68.254.142*.

```bash
ssh azureuser@40.68.254.142
```

