


Um conjunto de disponibilidade ajuda a manter as máquinas virtuais disponíveis durante o período de inatividade, tal como durante a manutenção. Colocar duas ou mais máquinas virtuais da mesma forma configuradas num conjunto de disponibilidade cria Olá redundância necessária toomaintain disponibilidade dos serviços ou aplicações de Olá que executa a máquina virtual. Para obter mais informações sobre como isto funciona, consulte [gerir a disponibilidade de Olá das máquinas virtuais][Manage hello availability of virtual machines].

É uma melhor toouse de prática conjuntos de disponibilidade e balanceamento de carga toohelp de pontos finais Certifique-se de que a aplicação está sempre disponível e em execução com eficiência. Para obter detalhes sobre os pontos finais com balanceamento de carga, consulte [para serviços de infraestrutura do Azure de balanceamento de carga][Load balancing for Azure infrastructure services].

Pode adicionar as máquinas virtuais clássicas para um conjunto, utilizando uma das duas opções de disponibilidade:

* [Opção 1: Criar uma máquina virtual e um conjunto de disponibilidade em Olá mesmo tempo][Option 1: Create a virtual machine and an availability set at hello same time]. Em seguida, adicione novas máquinas virtuais toohello, definido ao criar essas máquinas virtuais.
* [Opção 2: Adicionar um conjunto de disponibilidade de tooan de máquina virtual existente][Option 2: Add an existing virtual machine tooan availability set].

> [!NOTE]
> No modelo clássico de Olá Olá máquinas virtuais que pretende tooput no mesmo conjunto de disponibilidade tem de pertencer toohello mesmo serviço em nuvem.
> 
> 

## <a id="createset"></a>Opção 1: criar uma máquina virtual e um conjunto de disponibilidade em Olá mesmo tempo
Pode utilizar qualquer um dos Olá portal do Azure ou do Azure PowerShell comandos toodo isto.

Olá toouse portal do Azure:

1. Se ainda não o fez, inicie sessão no toohello [portal do Azure](https://portal.azure.com).
2. No menu do hub de Olá, clique em **+ novo**e, em seguida, clique em **Máquina Virtual**.
   
    ![Texto alternativo da imagem](./media/virtual-machines-common-classic-configure-availability/ChooseVMImage.png)
3. Selecione a imagem de máquina virtual de Marketplace Olá desejar toouse. Pode escolher toocreate uma máquina virtual Linux ou do Windows.
4. Para Olá selecionado máquina virtual, certifique-se de que modelo de implementação Olá estiver definido demasiado**clássico** e, em seguida, clique em **criar**
   
    ![Texto alternativo da imagem](./media/virtual-machines-common-classic-configure-availability/ChooseClassicModel.png)
5. Introduza um nome da máquina virtual, o nome de utilizador e a palavra-passe (para máquinas do Windows) ou a chave pública SSH (para computadores Linux). 
6. Escolha o tamanho da VM Olá e, em seguida, clique em **selecione** toocontinue.
7. Escolha **configuração opcional > do conjunto de disponibilidade**e selecione o conjunto de disponibilidade de Olá desejar tooadd Olá máquina virtual.
   
    ![Texto alternativo da imagem](./media/virtual-machines-common-classic-configure-availability/ChooseAvailabilitySet.png) 
8. Reveja as definições de configuração. Quando tiver terminado, clique em **criar**.
9. Enquanto o Azure cria a máquina virtual, pode controlar o progresso de Olá em **máquinas virtuais** no menu do hub de Olá.

toouse Azure PowerShell comandos toocreate uma máquina virtual do Azure e adicione-o conjunto de disponibilidade novo ou existente tooa, consulte [toocreate de utilização do Azure PowerShell e pré-configurar máquinas virtuais baseadas no Windows](../articles/virtual-machines/windows/classic/create-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

## <a id="addmachine"></a>Opção 2: adicionar um conjunto de disponibilidade de tooan de máquina virtual existente
No portal do Azure Olá, pode adicionar existente as máquinas virtuais clássicas tooan, conjunto de disponibilidade de existente ou crie um novo para os mesmos. (Tenha em atenção que as máquinas virtuais Olá Olá mesmo conjunto de disponibilidade tem de pertencer toohello mesmo serviço em nuvem.) passos de Olá são quase Olá mesmo. Com o Azure PowerShell, pode adicionar o conjunto de disponibilidade Olá máquina virtual tooan existente.

1. Se ainda não o fez, inicie sessão no toohello [portal do Azure](https://portal.azure.com).
2. No menu do Hub de Olá, clique em **máquinas virtuais (clássicas)**.
   
    ![Texto alternativo da imagem](./media/virtual-machines-common-classic-configure-availability/ChooseClassicVM.png)
3. Na lista de Olá de máquinas virtuais, selecione o nome de Olá da máquina virtual de Olá que pretende que o conjunto de toohello tooadd.
4. Escolha **do conjunto de disponibilidade** da máquina virtual de Olá **definições**.
   
    ![Texto alternativo da imagem](./media/virtual-machines-common-classic-configure-availability/AvailabilitySetSettings.png)
5. Selecione o conjunto de disponibilidade de Olá que desejar tooadd Olá máquina virtual. máquina virtual de Olá têm de pertencer toohello mesmo serviço em nuvem como conjunto de disponibilidade de Olá.
   
    ![Texto alternativo da imagem](./media/virtual-machines-common-classic-configure-availability/AvailabilitySetPicker.png)
6. Clique em **Guardar**.

comandos do Azure PowerShell toouse, abra uma sessão do PowerShell do Azure de nível de administrador e execute Olá os seguintes comandos. Para os marcadores de posição de Olá (tais como &lt;VmCloudServiceName&gt;), substituir tudo dentro de aspas Olá, incluindo Olá < e > carateres, com Olá corrigir nomes.

    Get-AzureVM -ServiceName "<VmCloudServiceName>" -Name "<VmName>" | Set-AzureAvailabilitySet -AvailabilitySetName "<AvSetName>" | Update-AzureVM

> [!NOTE]
> Olá poderá ter toofinish toobe reiniciado adicioná-lo toohello conjunto de disponibilidade.
> 
> 

<!-- LINKS -->
[Option 1: Create a virtual machine and an availability set at hello same time]: #createset
[Option 2: Add an existing virtual machine tooan availability set]: #addmachine

[Load balancing for Azure infrastructure services]: ../articles/virtual-machines/virtual-machines-linux-load-balance.md
[Manage hello availability of virtual machines]:../articles/virtual-machines/linux/manage-availability.md

[Create a virtual machine running Windows]: ../articles/virtual-machines/virtual-machines-windows-hero-tutorial.md
[Virtual Network overview]: ../articles/virtual-network/virtual-networks-overview.md

