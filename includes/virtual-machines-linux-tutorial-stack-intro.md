## <a name="create-a-resource-group"></a>Criar um grupo de recursos

Crie um grupo de recursos com o comando [az group create](/cli/azure/group#az_group_create). Um grupo de recursos do Azure é um contentor lógico no qual os recursos do Azure são implementados e geridos. 

O exemplo seguinte cria um grupo de recursos com o nome *myResourceGroup* na localização *eastus*.

```azurecli-interactive 
az group create --name myResourceGroup --location eastus
```

## <a name="create-a-virtual-machine"></a>Criar uma máquina virtual

Crie uma VM com o comando [z vm create](/cli/azure/vm#az_vm_create). 

O exemplo seguinte cria uma VM com o nome *myVM* e cria chaves SSH caso estas ainda não existam numa localização chave predefinida. Para utilizar um conjunto específico de chaves, utilize a opção `--ssh-key-value`. O comando também define *azureuser* como um nome de utilizador administrador. Utilizar este nome mais tarde para ligar à VM. 

```azurecli-interactive 
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys
```

Quando a VM tiver sido criada, a CLI do Azure mostra informações semelhantes ao seguinte exemplo. Tome nota do `publicIpAddress`. Este endereço é utilizado para aceder a VM em passos posteriores.

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

Por predefinição, apenas as ligações de SSH são permitidas para VMs com Linux implementados no Azure. Porque esta VM vai ser um servidor web, terá de abrir a porta 80 da internet. Utilize o comando [az vm open-port](/cli/azure/vm#az_vm_open_port) para abrir a porta pretendida.  
 
```azurecli-interactive 
az vm open-port --port 80 --resource-group myResourceGroup --name myVM
```
## <a name="ssh-into-your-vm"></a>Aceder através de SSH à VM


Se já não souber o endereço IP público da sua VM, execute o [lista de ip público de rede az](/cli/azure/network/public-ip#list) comando. Precisa este endereço IP para vários passos posteriores.


```azurecli-interactive
az network public-ip list --resource-group myResourceGroup --query [].ipAddress
```

Utilize o seguinte comando para criar uma sessão SSH com a máquina virtual. Substitua o endereço IP público correto da sua máquina virtual. Neste exemplo, o endereço IP é *40.68.254.142*. *azureuser* é o nome de utilizador administrador definiu quando criou a VM.

```bash
ssh azureuser@40.68.254.142
```

