---
title: "aaaCreate uma Máquina Virtual do SQL Server no Azure PowerShell (Resource Manager) | Microsoft Docs"
description: "Fornece os passos e scripts do PowerShell para criar uma VM do Azure com imagens de Galeria de máquina virtual do SQL Server."
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
editor: 
tags: azure-resource-manager
ms.assetid: 98d50dd8-48ad-444f-9031-5378d8270d7b
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 01/17/2017
ms.author: jroth
ms.openlocfilehash: 2b8cb8f69ff9894a95eab617816a60c8674eeefa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="provision-a-sql-server-virtual-machine-using-azure-powershell-resource-manager"></a>Aprovisionar uma máquina virtual de SQL Server com o Azure PowerShell (Resource Manager)
> [!div class="op_single_selector"]
> * [Portal](virtual-machines-windows-portal-sql-server-provision.md)
> * [PowerShell](virtual-machines-windows-ps-sql-create.md)
>
>

## <a name="overview"></a>Descrição geral
Este tutorial mostra como toocreate utilizando uma única máquina virtual do Azure Olá **do Azure Resource Manager** modelo de implementação utilizando cmdlets do PowerShell do Azure. Neste tutorial, iremos criar uma máquina virtual utilizando uma única unidade de disco a partir de uma imagem no Olá galeria do SQL Server. Iremos criar novos fornecedores de armazenamento de Olá, rede e recursos de computação que serão utilizados pela máquina virtual de Olá. Se tiver fornecedores existentes para qualquer um destes recursos, pode utilizar em vez disso, os fornecedores.

Se precisar de hello versão clássica deste tópico, consulte o artigo [aprovisionar uma máquina virtual de SQL Server utilizando o Azure PowerShell clássico](../classic/ps-sql-create.md).

## <a name="prerequisites"></a>Pré-requisitos
Para este tutorial precisa de:

* Uma conta do Azure e subscrição antes de começar. Se não tiver uma, inscreva-se um [avaliação gratuita](https://azure.microsoft.com/pricing/free-trial/).
* [O Azure PowerShell)](/powershell/azure/overview), versão mínima do 1.4.0 ou posterior (Este tutorial escrita utilizando a versão 1.5.0).
  * tooretrieve a versão, o tipo **Azure Get-Module - ListAvailable**.

## <a name="configure-your-subscription"></a>Configurar a sua subscrição
Abra o Windows PowerShell e estabelecer acesso tooyour conta do Azure executando o seguinte cmdlet de Olá. Será apresentada com um início de sessão no ecrã tooenter as suas credenciais. Utilize Olá mesmo correio eletrónico e palavra-passe que utilizam toosign no toohello portal do Azure.

    Add-AzureRmAccount

Após iniciar sessão com êxito a Verão algumas informações no ecrã que incluem o SubscriptionId Olá com a qual tem sessão iniciada. Esta é a subscrição de Olá na qual serão criados recursos Olá para este tutorial, a menos que altere tooa outra subscrição. Se tiver vários SubscriptionIds, execute uma lista de todos os seus SubscriptionIds Olá cmdlet tooreturn os seguintes:

    Get-AzureRmSubscription

toochange tooanother SubscriptionID, execute Olá seguintes cmdlet com o SubscriptionId pretendido.

    Select-AzureRmSubscription -SubscriptionId xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx

## <a name="define-image-variables"></a>Definir as variáveis de imagem
toosimplify facilidade de utilização e a compreensão de script de Olá concluída este tutorial, iremos será iniciada, definindo um número de variáveis. Alterar os valores de parâmetros de Olá como julgar, mas cuidado com de nomenclatura comprimentos de tooname relacionados restrições e os carateres especiais ao modificar os valores de Olá fornecidos.

### <a name="location-and-resource-group"></a>Localização e grupo de recursos
Utilize duas variáveis toodefine Olá dados região e Olá grupo de recursos no qual vai criar Olá outros recursos para a máquina virtual de Olá.

Modifique conforme pretendido e, em seguida, executar Olá os seguintes cmdlets tooinitialize estas variáveis.

    $Location = "SouthCentralUS"
    $ResourceGroupName = "sqlvm1"

### <a name="storage-properties"></a>Propriedades de armazenamento
Utilize Olá variáveis toodefine Olá conta e Olá tipo de armazenamento de toobe de armazenamento utilizado pela máquina virtual de Olá a seguir.

Modifique conforme pretendido e, em seguida, executar Olá seguintes cmdlet tooinitialize estas variáveis. Tenha em atenção que neste exemplo, estamos a utilizar [armazenamento Premium](../../../storage/common/storage-premium-storage.md), que é recomendada para cargas de trabalho de produção. Para obter detalhes sobre esta orientação e outras recomendações, consulte [práticas recomendadas do SQL Server em Azure Virtual Machines](virtual-machines-windows-sql-performance.md).

    $StorageName = $ResourceGroupName + "storage"
    $StorageSku = "Premium_LRS"

### <a name="network-properties"></a>Propriedades da rede
Utilizar Olá seguir a interface de rede variáveis toodefine Olá, método de alocação de TCP/IP Olá, nome da rede virtual Olá, nome de sub-rede virtual Olá, Olá intervalo de endereços IP para a rede virtual Olá, Olá intervalo de endereços IP de sub-rede Olá e Olá toobe de etiqueta do nome de domínio público utilizada pela rede Olá na máquina virtual de Olá.

Modifique conforme pretendido e, em seguida, executar Olá seguintes cmdlet tooinitialize estas variáveis.

    $InterfaceName = $ResourceGroupName + "ServerInterface"
    $TCPIPAllocationMethod = "Dynamic"
    $VNetName = $ResourceGroupName + "VNet"
    $SubnetName = "Default"
    $VNetAddressPrefix = "10.0.0.0/16"
    $VNetSubnetAddressPrefix = "10.0.0.0/24"
    $DomainName = "sqlvm1"

### <a name="virtual-machine-properties"></a>Propriedades da máquina virtual
Utilize Olá seguir o nome da máquina virtual variáveis toodefine Olá, o nome do computador Olá, o tamanho da máquina virtual Olá e o nome do disco de sistema operativo Olá para a máquina virtual de Olá.

Modifique conforme pretendido e, em seguida, executar Olá seguintes cmdlet tooinitialize estas variáveis.

    $VMName = $ResourceGroupName + "VM"
    $ComputerName = $ResourceGroupName + "Server"
    $VMSize = "Standard_DS13"
    $OSDiskName = $VMName + "OSDisk"

### <a name="image-properties"></a>Propriedades da imagem
Utilize Olá variáveis toodefine Olá imagem toouse para a máquina virtual de Olá a seguir. Neste exemplo, a imagem do SQL Server 2016 Enterprise Olá é utilizada.

Modifique conforme pretendido e, em seguida, executar Olá seguintes cmdlet tooinitialize estas variáveis.

    $PublisherName = "MicrosoftSQLServer"
    $OfferName = "SQL2016-WS2016"
    $Sku = "Enterprise"
    $Version = "latest"

Tenha em atenção que pode obter uma lista completa das ofertas de imagem do SQL Server com o comando Get-AzureRmVMImageOffer de Olá:

    Get-AzureRmVMImageOffer -Location 'East US' -Publisher 'MicrosoftSQLServer'

E pode ver Olá Skus disponíveis para uma oferta com comando Olá Get AzureRmVMImageSku. Olá comando seguinte apresenta todos os Skus disponíveis para Olá **SQL2014SP1 WS2012R2** oferecem.

    Get-AzureRmVMImageSku -Location 'East US' -Publisher 'MicrosoftSQLServer' -Offer 'SQL2014SP1-WS2012R2' | Select Skus

## <a name="create-a-resource-group"></a>Criar um grupo de recursos
Com o modelo de implementação do Resource Manager Olá, Olá o objeto primeiro que criou é o grupo de recursos de Olá. Utilizaremos Olá [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) cmdlet toocreate um grupo de recursos do Azure e os respetivos recursos com recurso de Olá grupo nome e localização definido pelo variáveis de Olá anteriormente inicializado.

Execute Olá seguintes cmdlet toocreate o novo grupo de recursos.

    New-AzureRmResourceGroup -Name $ResourceGroupName -Location $Location

## <a name="create-a-storage-account"></a>Criar uma conta de armazenamento
máquina virtual de Olá requer recursos de armazenamento para o disco do sistema operativo Olá e para Olá dados do SQL Server e os ficheiros de registo. De simplicidade, iremos criar um único disco para ambos. Pode anexar mais discos posteriormente utilizando Olá [Azure adicionar disco](/powershell/module/azure/add-azuredisk) cmdlet na ordem tooplace os dados do SQL Server e os ficheiros de registo no discos dedicados. Utilizaremos Olá [New-AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet toocreate um padrão de armazenamento e de contas no seu novo grupo de recursos com o nome de conta do storage Olá, nome de Sku de armazenamento e localização definidos utilizando variáveis de Olá que inicializar anteriormente.

Execute Olá seguintes cmdlet toocreate a sua nova conta de armazenamento.

    $StorageAccount = New-AzureRmStorageAccount -ResourceGroupName $ResourceGroupName -Name $StorageName -SkuName $StorageSku -Kind "Storage" -Location $Location

## <a name="create-network-resources"></a>Criar recursos de rede
máquina virtual de Olá requer um número de recursos de rede para conectividade de rede.

* Cada máquina virtual necessita de uma rede virtual.
* Uma rede virtual tem de ter pelo menos uma subrede definida.
* Uma interface de rede tem de ser definida com um público ou um endereço IP privado.

### <a name="create-a-virtual-network-subnet-configuration"></a>Criar uma configuração de sub-rede de rede virtual
Iremos irá começar por criar uma configuração de sub-rede para a nossa rede virtual. Para o nosso tutorial, iremos criar uma sub-rede predefinida utilizando Olá [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) cmdlet. Iremos criar a configuração de sub-rede de rede virtual com Olá nome e endereço prefixo de sub-rede definido utilizando variáveis de Olá anteriormente inicializado.

> [!NOTE]
> Pode definir propriedades adicionais de configuração de sub-rede de rede virtual Olá utilizar este cmdlet, mas que ultrapassa o âmbito de Olá deste tutorial.
>
>

Execute Olá seguintes cmdlet toocreate a configuração de sub-rede virtual.

    $SubnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name $SubnetName -AddressPrefix $VNetSubnetAddressPrefix

### <a name="create-a-virtual-network"></a>Criar uma rede virtual
Em seguida, iremos criar nossa rede virtual com o Olá [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork) cmdlet. Iremos criar nossa rede virtual no seu novo grupo de recursos, com o nome de Olá, a localização e o prefixo de endereço definidos utilizando variáveis de Olá anteriormente inicializado e utilizando a configuração de sub-rede Olá que definiu no passo anterior Olá.

Execute Olá seguintes cmdlet toocreate a rede virtual.

    $VNet = New-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $ResourceGroupName -Location $Location -AddressPrefix $VNetAddressPrefix -Subnet $SubnetConfig

### <a name="create-hello-public-ip-address"></a>Criar endereço IP público do Olá
Agora que temos nossa rede virtual definido, é necessário tooconfigure um endereço IP para a máquina de virtual toohello de conectividade. Para este tutorial, iremos criar um endereço IP público utilizando toosupport conectividade à Internet de endereçamento de IP dinâmico. Utilizaremos Olá [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress) cmdlet toocreate Olá endereço IP público na Olá recursos grupo criado prevously e com o nome de Olá, localização, método de alocação e etiqueta de nome de domínio DNS definidos utilizando Olá variáveis que anteriormente inicializado.

> [!NOTE]
> Pode definir propriedades adicionais do endereço IP público Olá utilizar este cmdlet, mas que ultrapassa o âmbito de Olá deste tutorial inicial. Pode também criar um endereço privado ou um endereço com um endereço estático, mas também que ultrapassa Olá âmbito deste tutorial.
>
>

Execute Olá seguintes cmdlet toocreate o seu endereço IP público.

    $PublicIp = New-AzureRmPublicIpAddress -Name $InterfaceName -ResourceGroupName $ResourceGroupName -Location $Location -AllocationMethod $TCPIPAllocationMethod -DomainNameLabel $DomainName

### <a name="create-hello-network-interface"></a>Criar a interface de rede Olá
Estamos agora interface de rede de Olá toocreate pronto que irá utilizar o nosso máquina virtual. Utilizaremos Olá [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) cmdlet toocreate nossa interface de rede no grupo de recursos de Olá criada anteriormente e com o nome de Olá, localização, sub-rede e o endereço IP público definido anteriormente.

Execute Olá seguintes cmdlet toocreate sua interface de rede.

    $Interface = New-AzureRmNetworkInterface -Name $InterfaceName -ResourceGroupName $ResourceGroupName -Location $Location -SubnetId $VNet.Subnets[0].Id -PublicIpAddressId $PublicIp.Id

## <a name="configure-a-vm-object"></a>Configurar um objeto VM
Agora que temos de recursos de armazenamento e rede definidos, estamos prontos toodefine recursos de computação para a máquina virtual de Olá. Para o nosso tutorial, iremos irá especificar várias propriedades do sistema operativo e o tamanho da máquina virtual Olá, especificar Olá interface de rede que criámos anteriormente, definir o armazenamento de BLOBs e, em seguida, especifique o disco do sistema operativo Olá.

### <a name="create-hello-vm-object"></a>Criar o objeto da VM Olá
Iremos será iniciada, especificando o tamanho da máquina virtual Olá. Para este tutorial, estamos a especificar um DS13. Utilizaremos Olá [New-AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig) cmdlet toocreate um objeto de configuráveis máquina virtual com o nome de Olá e tamanho definidos utilizando variáveis de Olá anteriormente inicializado.

Execute Olá seguinte objeto de máquina virtual do cmdlet toocreate Olá.

    $VirtualMachine = New-AzureRmVMConfig -VMName $VMName -VMSize $VMSize

### <a name="create-a-credential-object-toohold-hello-name-and-password-for-hello-local-administrator-credentials"></a>Criar uma credencial do objeto toohold Olá e palavra-passe para as credenciais de administrador local Olá
Antes, pode definir propriedades do sistema operativo Olá para a máquina virtual de Olá, precisamos toosupply Olá das credenciais da conta de administrador local Olá como uma cadeia segura. tooaccomplish isto, iremos utilizar Olá [Get-Credential](https://technet.microsoft.com/library/hh849815.aspx) cmdlet.

Executar o seguinte cmdlet de Olá e, na janela de pedido da credencial do Windows PowerShell Olá, escreva toouse de nome e palavra-passe de Olá Olá conta de administrador local na máquina de virtual do Windows hello.

    $Credential = Get-Credential -Message "Type hello name and password of hello local administrator account."

### <a name="set-hello-operating-system-properties-for-hello-virtual-machine"></a>Definir as propriedades do sistema operativo Olá para a máquina virtual de Olá
Agora vamos são propriedades do sistema operativo tooset pronto Olá máquina virtual. Utilizaremos Olá [conjunto AzureRmVMOperatingSystem](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem) tipo Olá de tooset de cmdlet do sistema operativo como Windows, necessita de Olá [agente da máquina virtual](../classic/agents-and-extensions.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) toobe instalado, especifique esse cmdlet Olá permite automática Atualizar e definir o nome da máquina virtual Olá, nome do computador Olá e as credenciais de Olá utilizando variáveis de Olá anteriormente inicializado.

Execute Olá seguintes cmdlet tooset Olá propriedades de sistema operativo para a máquina virtual.

    $VirtualMachine = Set-AzureRmVMOperatingSystem -VM $VirtualMachine -Windows -ComputerName $ComputerName -Credential $Credential -ProvisionVMAgent -EnableAutoUpdate

### <a name="add-hello-network-interface-toohello-virtual-machine"></a>Adicionar Olá rede interface toohello máquina
Em seguida, iremos adicionar a interface de rede de Olá que foi criada anteriormente toohello máquina. Utilizaremos Olá [adicionar AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface) cmdlet tooadd Olá rede interface utilizando variável de interface de rede Olá definido anteriormente.

Execute Olá seguir a interface de rede do cmdlet tooset Olá para a máquina virtual.

    $VirtualMachine = Add-AzureRmVMNetworkInterface -VM $VirtualMachine -Id $Interface.Id

### <a name="set-hello-blob-storage-location-for-hello-disk-toobe-used-by-hello-virtual-machine"></a>Definir localização de armazenamento de BLOBs de Olá para Olá toobe de disco utilizado pela máquina virtual de Olá
Em seguida, iremos irá definir localização de armazenamento de BLOBs de Olá para Olá toobe de disco utilizado pela máquina virtual de Olá utilizando variáveis de Olá definido anteriormente.

Execute Olá seguinte localização de armazenamento de Blobs do cmdlet tooset Olá.

    $OSDiskUri = $StorageAccount.PrimaryEndpoints.Blob.ToString() + "vhds/" + $OSDiskName + ".vhd"

### <a name="set-hello-operating-system-disk-properties-for-hello-virtual-machine"></a>Definir o sistema de operativo Olá propriedades de disco para a máquina virtual de Olá
Em seguida, iremos irá definir sistema de operativo Olá propriedades do disco para a máquina virtual de Olá. Utilizaremos Olá [conjunto AzureRmVMOSDisk](/powershell/module/azurerm.compute/set-azurermvmosdisk) toospecify cmdlet que Olá o sistema operativo da máquina virtual de Olá serão provenientes de uma imagem, tooset tooread apenas a colocação em cache (porque o SQL Server está a ser instalado no Olá mesmo disco) e defina nome da máquina virtual Olá e o disco do sistema operativo Olá definidos utilizando variáveis de Olá definido anteriormente.

Execute Olá seguintes propriedades de disco do sistema operativo do cmdlet tooset Olá para a máquina virtual.

    $VirtualMachine = Set-AzureRmVMOSDisk -VM $VirtualMachine -Name $OSDiskName -VhdUri $OSDiskUri -Caching ReadOnly -CreateOption FromImage

### <a name="specify-hello-platform-image-for-hello-virtual-machine"></a>Especifique a imagem de plataforma Olá para a máquina virtual de Olá
A nossa último passo da configuração é imagem de plataforma Olá toospecify nosso máquina virtual. Para o nosso tutorial, estamos a utilizar imagem do SQL Server 2016 CTP mais recente Olá. Utilizaremos Olá [conjunto AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage) cmdlet toouse esta imagem, conforme definido pelo variáveis de Olá definido anteriormente.

Execute Olá seguinte imagem de plataforma do cmdlet toospecify Olá para a máquina virtual.

    $VirtualMachine = Set-AzureRmVMSourceImage -VM $VirtualMachine -PublisherName $PublisherName -Offer $OfferName -Skus $Sku -Version $Version

## <a name="create-hello-sql-vm"></a>Criar Olá VM do SQL Server
Agora que tiver concluído os passos de configuração de Olá, está pronto toocreate Olá máquina. Utilizaremos Olá [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm) máquina virtual cmdlet toocreate Olá utilizando variáveis de Olá que definiu.

Execute Olá seguintes cmdlet toocreate a máquina virtual.

    New-AzureRmVM -ResourceGroupName $ResourceGroupName -Location $Location -VM $VirtualMachine

máquina virtual de Olá é criada. Tenha em atenção que é criada uma conta de armazenamento standard para diagnóstico de arranque porque Olá especificada a conta de armazenamento de disco da máquina virtual Olá é uma conta de armazenamento premium.

Agora, pode ver esta máquina Olá Portal do Azure toosee [respetivo endereço IP público e o respetivo nome de domínio completamente qualificado](virtual-machines-windows-portal-sql-server-provision.md).

## <a name="example-script"></a>Script de exemplo
Olá seguinte script contém Olá concluída script do PowerShell para este tutorial. Pressupõe que já tem a configuração Olá subscrição do Azure toouse com Olá **Add-AzureRmAccount** e **Select-AzureRmSubscription** comandos.

    # Variables
    ## Global
    $Location = "SouthCentralUS"
    $ResourceGroupName = "sqlvm1"
    ## Storage
    $StorageName = $ResourceGroupName + "storage"
    $StorageSku = "Premium_LRS"

    ## Network
    $InterfaceName = $ResourceGroupName + "ServerInterface"
    $VNetName = $ResourceGroupName + "VNet"
    $SubnetName = "Default"
    $VNetAddressPrefix = "10.0.0.0/16"
    $VNetSubnetAddressPrefix = "10.0.0.0/24"
    $TCPIPAllocationMethod = "Dynamic"
    $DomainName = "sqlvm1"

    ##Compute
    $VMName = $ResourceGroupName + "VM"
    $ComputerName = $ResourceGroupName + "Server"
    $VMSize = "Standard_DS13"
    $OSDiskName = $VMName + "OSDisk"

    ##Image
    $PublisherName = "MicrosoftSQLServer"
    $OfferName = "SQL2016-WS2016"
    $Sku = "Enterprise"
    $Version = "latest"

    # Resource Group
    New-AzureRmResourceGroup -Name $ResourceGroupName -Location $Location

    # Storage
    $StorageAccount = New-AzureRmStorageAccount -ResourceGroupName $ResourceGroupName -Name $StorageName -SkuName $StorageSku -Kind "Storage" -Location $Location

    # Network
    $SubnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name $SubnetName -AddressPrefix $VNetSubnetAddressPrefix
    $VNet = New-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $ResourceGroupName -Location $Location -AddressPrefix $VNetAddressPrefix -Subnet $SubnetConfig
    $PublicIp = New-AzureRmPublicIpAddress -Name $InterfaceName -ResourceGroupName $ResourceGroupName -Location $Location -AllocationMethod $TCPIPAllocationMethod -DomainNameLabel $DomainName
    $Interface = New-AzureRmNetworkInterface -Name $InterfaceName -ResourceGroupName $ResourceGroupName -Location $Location -SubnetId $VNet.Subnets[0].Id -PublicIpAddressId $PublicIp.Id

    # Compute
    $VirtualMachine = New-AzureRmVMConfig -VMName $VMName -VMSize $VMSize
    $Credential = Get-Credential -Message "Type hello name and password of hello local administrator account."
    $VirtualMachine = Set-AzureRmVMOperatingSystem -VM $VirtualMachine -Windows -ComputerName $ComputerName -Credential $Credential -ProvisionVMAgent -EnableAutoUpdate #-TimeZone = $TimeZone
    $VirtualMachine = Add-AzureRmVMNetworkInterface -VM $VirtualMachine -Id $Interface.Id
    $OSDiskUri = $StorageAccount.PrimaryEndpoints.Blob.ToString() + "vhds/" + $OSDiskName + ".vhd"
    $VirtualMachine = Set-AzureRmVMOSDisk -VM $VirtualMachine -Name $OSDiskName -VhdUri $OSDiskUri -Caching ReadOnly -CreateOption FromImage

    # Image
    $VirtualMachine = Set-AzureRmVMSourceImage -VM $VirtualMachine -PublisherName $PublisherName -Offer $OfferName -Skus $Sku -Version $Version

    ## Create hello VM in Azure
    New-AzureRmVM -ResourceGroupName $ResourceGroupName -Location $Location -VM $VirtualMachine

## <a name="next-steps"></a>Passos seguintes
Depois de criar a máquina virtual de Olá, está pronto tooconnect toohello máquinas com conectividade RDP e o programa de configuração. Para obter mais informações, consulte [ligar tooa Máquina Virtual do servidor SQL no Azure (Resource Manager)](virtual-machines-windows-sql-connect.md).

