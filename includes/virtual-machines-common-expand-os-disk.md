## <a name="overview"></a>Descrição geral
Quando cria uma nova máquina virtual (VM) num grupo de recursos ao implementar uma imagem de [Azure Marketplace](https://azure.microsoft.com/marketplace/), disco de SO Olá predefinido é de 127 GB. Mesmo que é possível tooadd dados discos toohello VM (quantos consoante Olá SKU que escolheu) e além é recomendada tooinstall aplicações e cargas de trabalho que consomem muita CPU nestes discos adenda, frequentemente que os clientes precisam tooexpand Olá SO unidade toosupport determinados cenários, como o seguinte:

1. Suportar aplicações antigas que instalam componentes na unidade do SO.
2. Migrar uma máquina virtual ou PC físicos no local com uma unidade de SO maior.

> [!IMPORTANT]
> O Azure tem dois modelos de implementação diferentes para criar e trabalhar com recursos: Resource Manager e Clássico. Este artigo abrange utilizando o modelo do Resource Manager Olá. A Microsoft recomenda que as implementações mais novas utilizem o modelo de Gestor de recursos de Olá.
> 
> 

## <a name="resize-hello-os-drive"></a>Redimensionar disco Olá SO
Neste artigo, irá realizar tarefas Olá de redimensionamento unidade Olá SO utilizar módulos do Gestor de recursos de [Azure Powershell](/powershell/azureps-cmdlets-docs). Abra o ISE do Powershell ou a janela do Powershell no modo administrativo e siga os passos de Olá abaixo:

1. Início de sessão tooyour Microsoft Azure conta no modo de gestão de recursos e selecione a sua subscrição da seguinte forma:
   
   ```Powershell
   Login-AzureRmAccount
   Select-AzureRmSubscription –SubscriptionName 'my-subscription-name'
   ```
2. Defina o nome do grupo de recursos e o nome VM da seguinte forma:
   
   ```Powershell
   $rgName = 'my-resource-group-name'
   $vmName = 'my-vm-name'
   ```
3. Obter uma referência tooyour VM da seguinte forma:
   
   ```Powershell
   $vm = Get-AzureRmVM -ResourceGroupName $rgName -Name $vmName
   ```
4. Pare Olá VM antes de o redimensionamento de disco Olá da seguinte forma:
   
    ```Powershell
    Stop-AzureRmVM -ResourceGroupName $rgName -Name $vmName
    ```
5. E provém aqui momento Olá que tiver sido a aguardar! Definir o tamanho de Olá de valor de toohello pretendido de disco de SO de Olá e atualizar Olá VM da seguinte forma:
   
   ```Powershell
   $vm.StorageProfile.OSDisk.DiskSizeGB = 1023
   Update-AzureRmVM -ResourceGroupName $rgName -VM $vm
   ```
   
   > [!WARNING]
   > tamanho do novo Olá deve ser superior ao tamanho do disco existente Olá. Olá máximo permitido é de 1023 GB.
   > 
   > 
6. Atualização Olá VM pode demorar alguns segundos. Depois de comando de Olá terminar em execução, reinicie Olá VM da seguinte forma:
   
   ```Powershell
   Start-AzureRmVM -ResourceGroupName $rgName -Name $vmName
   ```

E já está! Agora RDP nas Olá VM, abra a gestão de computadores (ou gestão de discos) e expanda a unidade de Olá Olá recentemente atribuído espaço a utilizar.

## <a name="summary"></a>Resumo
Neste artigo, utilizámos o Azure Resource Manager módulos do Powershell tooexpand Olá disco do SO da máquina virtual IaaS. Reproduzido abaixo é o script de conclusão de Olá para sua referência:

```Powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionName 'my-subscription-name'
$rgName = 'my-resource-group-name'
$vmName = 'my-vm-name'
$vm = Get-AzureRmVM -ResourceGroupName $rgName -Name $vmName
Stop-AzureRmVM -ResourceGroupName $rgName -Name $vmName
$vm.StorageProfile.OSDisk.DiskSizeGB = 1023
Update-AzureRmVM -ResourceGroupName $rgName -VM $vm
Start-AzureRmVM -ResourceGroupName $rgName -Name $vmName
```

## <a name="next-steps"></a>Passos Seguintes
Embora este artigo, vamos concentra-se principalmente em expandir disco Olá SO de VM de Olá, hello programada script também pode ser utilizada para expandir Olá dados discos anexados toohello VM alterando uma única linha de código. Por exemplo, dados de primeiro tooexpand Olá disco ligado toohello VM, substitua Olá ```OSDisk``` objeto do ```StorageProfile``` com ```DataDisks``` matriz e utilizar tooobtain um índice numérico um disco de dados anexados de toofirst de referência, conforme mostrado abaixo:

```Powershell
$vm.StorageProfile.DataDisks[0].DiskSizeGB = 1023
```
Do mesmo modo pode fazer referência a VM, utilizando um índice, conforme mostrado acima outro dados discos anexados toohello ou Olá ```Name``` propriedade dos discos de Olá conforme ilustrado abaixo:

```Powershell
($vm.StorageProfile.DataDisks | Where {$_.Name -eq 'my-second-data-disk'})[0].DiskSizeGB = 1023
```

Se quiser toofind enviados como tooattach discos tooan VM do Azure Resource Manager, selecionar esta opção [artigo](../articles/virtual-machines/windows/attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

