

As extensões de VM podem ajudá-lo a:

* Modificar as funcionalidades de segurança e identidade, como repor valores de conta e utilizar antimalware
* Iniciar, parar ou configurar a monitorização e o diagnóstico
* Repor ou instalar as funcionalidades de conectividade, como RDP e SSH
* Diagnosticar, monitorizar e gerir as suas VMs

Existem também muitas outras funcionalidades. Novas funcionalidades de extensão de VM são lançadas regularmente. Este artigo descreve Olá Azure VM agentes para o Windows e Linux, e como o suportam a funcionalidade de extensão da VM. Para obter uma lista de extensões de VM por categoria de funcionalidades, veja [Extensões e Funcionalidades de VM do Azure](../articles/virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

## <a name="azure-vm-agents-for-windows-and-linux"></a>Agentes VM do Azure para Windows e Linux
Olá o agente de máquinas virtuais do Azure (agente da VM) é um processo de seguro, leve-peso que instala, configura e remove as extensões VM em instâncias de Virtual Machines do Azure. Olá agente da VM atua como o serviço de controlo local seguro Olá para a VM do Azure. as extensões de Olá que Olá agente cargas fornecem tooincrease funcionalidades específicas a produtividade utilizando Olá instância.

Existem dois Agentes VM do Azure, um para VMs do Windows e outro para VMs do Linux.

Se pretender um toouse de instância de máquina virtual com uma ou mais extensões VM, Olá instância tem de ter um agente de VM instalado. Uma imagem de máquina virtual criada utilizando Olá portal do Azure e uma imagem de Olá **Marketplace** automaticamente instala um agente de VM no processo de criação de Olá. Se uma instância de máquina virtual não possui um agente de VM, pode instalar Olá agente da VM após a instância de máquina virtual de Olá é criada. Em alternativa, pode instalar o agente de Olá numa imagem de VM personalizada que, em seguida, carregar.

> [!IMPORTANT]
> Estes Agentes VM são serviços muito leves que permitem a administração protegida de instâncias de máquina virtual. Poderão existir casos em que não pretende Olá agente da VM. Se assim for, ser VMs toocreate se de que não tenham Olá agente da VM instalado utilizando Olá Azure CLI ou PowerShell. Embora Olá agente da VM pode ser removido fisicamente, comportamento Olá das extensões de VM na instância de Olá não está definido. Como resultado, a remoção de um Agente VM instalado não é suportada.
>

Olá agente VM está ativado no Olá seguintes situações:

* Olá, quando criar uma instância de uma VM utilizando o portal do Azure e selecionar uma imagem de Olá **Marketplace**,
* Quando cria uma instância de uma VM utilizando Olá [New-AzureVM](https://msdn.microsoft.com/library/azure/dn495254.aspx) ou Olá [New-AzureQuickVM](https://msdn.microsoft.com/library/azure/dn495183.aspx) cmdlet. Pode criar uma VM sem um agente de VM adicionando Olá **– DisableGuestAgent** parâmetro toohello [adicionar AzureProvisioningConfig](https://msdn.microsoft.com/library/azure/dn495299.aspx) cmdlet,

* Quando manualmente transferir e instalar Olá agente VM a uma instância VM existente e defina Olá **ProvisionGuestAgent** valor demasiado**verdadeiro**. Pode utilizar esta técnica para agentes do Windows e Linux, com um comando do PowerShell ou uma chamada REST. (Se não definir Olá **ProvisionGuestAgent** valor depois de instalar manualmente Olá agente da VM, adição de Olá de Olá agente da VM não está corretamente detetado.) Olá seguinte como exemplo de código mostra toodo este através do PowerShell onde hello `$svc` e `$name` já terem sido determinados os argumentos:

      $vm = Get-AzureVM –ServiceName $svc –Name $name
      $vm.VM.ProvisionGuestAgent = $TRUE
      Update-AzureVM –Name $name –VM $vm.VM –ServiceName $svc

* Quando cria uma imagem de VM que inclui um agente VM instalado. Assim que existe a imagem de Olá com Olá agente da VM, pode carregar esse tooAzure de imagem. Para uma VM do Windows, transfira Olá [ficheiro. msi do agente de VM Windows](http://go.microsoft.com/fwlink/?LinkID=394789) e instalar Olá agente da VM. Para uma VM com Linux, instale Olá agente VM a partir do repositório do GitHub Olá localizado em <https://github.com/Azure/WALinuxAgent>. Para obter mais informações sobre como tooinstall Olá agente da VM no Linux, consulte Olá [guia de utilizador do agente de VM do Azure Linux](../articles/virtual-machines/linux/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

> [!NOTE]
> PaaS, hello agente da VM é designado **WindowsAzureGuestAgent**e está sempre disponível no Web e as VMs de função de trabalho. (Para obter mais informações, consulte [arquitetura de função do Azure](http://blogs.msdn.com/b/kwill/archive/2011/05/05/windows-azure-role-architecture.aspx).) Olá agente da VM para VMs de função agora pode adicionar o serviço de nuvem extensões toohello VMs no Olá mesma forma que realiza computadores virtuais persistentes. diferença maior de Olá entre as extensões de VM na função VMs e VMs persistentes é quando são adicionadas as extensões VM Olá. Com as VMs de função, as extensões são adicionadas primeiro toohello o serviço em nuvem, em seguida, toohello implementações no serviço em nuvem.
>
> Utilize o [Get-AzureServiceAvailableExtension](https://msdn.microsoft.com/library/azure/dn722498.aspx) cmdlet toolist todas as extensões VM de função disponíveis.
>
>

## <a name="find-add-update-and-remove-vm-extensions"></a>Localizar, Adicionar, Atualizar e Remover Extensões de VM
Para obter detalhes sobre estas tarefas, veja [Adicionar, Localizar, Atualizar e Remover Extensões de VM do Azure](../articles/virtual-machines/windows/classic/manage-extensions.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).
