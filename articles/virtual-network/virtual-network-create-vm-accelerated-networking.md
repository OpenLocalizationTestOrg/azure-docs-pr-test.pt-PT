---
title: "aaaCreate uma máquina virtual do Azure com acelerados rede | Microsoft Docs"
description: "Saiba como toocreate uma máquina virtual com acelerados da rede."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/10/2017
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 241362891bfe083ab32c2f558be54f63f87c0693
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-machine-with-accelerated-networking"></a>Criar uma máquina virtual com acelerados da rede

Neste tutorial, saiba como toocreate uma Máquina Virtual do Azure (VM) a com acelerados da rede. Redes na melhoria são GA para Windows e numa pré-visualização pública para as distribuições do Linux específicas. Redes na melhoria permite tooa de Virtualização (SR-IOV) de e/s de raiz única VM, melhorando em grande medida o desempenho de rede. Este caminho de elevado desempenho ignora o anfitrião Olá datapath Olá, reduzindo a latência, interferência e utilização da CPU, para utilização com Olá mais pedir o seu trabalho rede cargas de trabalho em tipos VM suportados. Olá seguinte imagem mostra comunicação entre duas máquinas virtuais (VM), com e sem redes na melhoria:

![Comparação](./media/virtual-network-create-vm-accelerated-networking/image1.png)

Sem redes na melhoria, todo o tráfego de rede que entra e sai Olá VM tem atravessar anfitrião Olá e do comutador virtual de Olá. comutador virtual Olá fornece a imposição de políticas de todos os, tais como grupos de segurança de rede acedam listas de controlo, isolamento e outro tráfego de toonetwork de serviços de rede virtualizado. mais informações sobre comutadores virtuais, leia Olá toolearn [Virtualização de rede do Hyper-V e do comutador virtual](https://technet.microsoft.com/library/jj945275.aspx) artigo.

Com redes na melhoria, o tráfego de rede chega à interface de rede da VM Olá (NIC) e, em seguida, é reencaminhado toohello VM. Aplica-se todas as políticas de rede que Olá comutador virtual sem redes na melhoria são descarregadas sendo aplicada no hardware. Aplicar a política de hardware permite Olá NIC tooforward tráfego de rede diretamente toohello VM, ignorando anfitrião Olá e do comutador virtual de Olá, enquanto mantém todos os Olá política-aplicada no anfitrião de Olá.

Olá vantagens do funcionamento em rede na melhoria só se aplicam toohello VM que está ativada no. Para obter melhores resultados Olá, é ideal tooenable esta funcionalidade em, pelo menos, duas VMs ligado toohello mesma rede Virtual do Azure (VNet). Quando a comunicação entre VNets ou ligação no local, esta funcionalidade tem a latência de toooverall um impacto mínimo.

> [!WARNING]
> Este Linux pré-visualização pública pode não ter Olá mesmo nível de disponibilidade e fiabilidade, tal como as funcionalidades que estão em geral lançamento de disponibilidade. funcionalidade de Olá não é suportada, pode ter restrita capacidades e poderão não estar disponível em todas as localizações do Azure. Para notificações mais atualizadas à sua Olá, disponibilidade e o estado desta funcionalidade, verificar atualizações Olá de rede Virtual do Azure.

## <a name="benefits"></a>Benefícios
* **Reduzir a latência / superiores pacotes por segundo (pps):** remover comutador virtual de Olá de Olá datapath remove tempo Olá gastam de pacotes no anfitrião de Olá para processamento da política e aumenta Olá número de pacotes que podem ser processados no interior Olá VM.
* **Reduzido interferência:** comutador Virtual de processamento depende da quantidade de Olá de política que tem toobe aplicada e Olá carga de trabalho de Olá da CPU que está a fazer o processamento de Olá. A descarga de hardware de toohello de imposição de política de Olá remove esse variabilidade fornecendo pacotes diretamente toohello VM, a remoção de comunicação de tooVM Olá anfitrião e todas as interrupções de software e contexto muda.
* **Diminuir a utilização da CPU:** Bypassing Olá virtual comutador do anfitrião de Olá leva a utilização da CPU tooless para processar o tráfego de rede.

## <a name="Limitations"></a>Limitações
Quando utilizar esta capacidade de existir Olá seguintes limitações:

* **Criação de interface de rede:** Accelerated redes só podem ser ativada para uma NIC de novo. Não pode ser ativada para uma NIC que existente.
* **A criação de VM:** A NIC com redes na melhoria ativada pode apenas ser anexada tooa VM ao hello é criada a VM. Olá NIC não pode ser anexado tooan existente VM.
* **Regiões:** VMs do Windows com redes na melhoria são disponibilizadas em regiões mais do Azure. VMs com Linux com redes na melhoria são disponibilizadas em várias regiões. está a expandir as regiões de Olá esta capacidade está disponível. Consulte o blogue de atualizações de rede Virtual do Azure Olá abaixo para obter informações mais recentes do Olá.   
* **Sistemas operativos suportados:** Windows: Centro de dados do Microsoft Windows Server 2012 R2 e Windows Server 2016. Linux: Ubuntu Server 16.04 LTS com 4.4.0-77 de kernel ou superior, SLES 12 SP2, RHEL 7.3 e CentOS 7.3 (publicado por "Não autorizado Wave Software").
* **Tamanho da VM:** fins gerais e os tamanhos de instância com otimização de computação com oito ou vários núcleos. Para obter mais informações, consulte Olá [Windows](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) e [Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) artigos de tamanhos de VM. Olá conjunto de tamanhos de instância VM suportados irá expandir no Olá futura.
* **Apenas a implementação através do Azure Resource Manager (ARM):** acelerados redes não está disponível para implementação através da ASM/RDFE.

Limitações de toothese as alterações sejam anunciadas através de Olá [a rede Virtual do Azure atualiza](https://azure.microsoft.com/updates/accelerated-networking-in-preview) página.

## <a name="create-a-windows-vm"></a>Criar uma VM do Windows
Pode utilizar Olá portal do Azure ou para o Azure [PowerShell](#windows-powershell) toocreate Olá VM.

### <a name="windows-portal"></a>Portal

1. A partir do browser da Internet, abra Olá Azure [portal](https://portal.azure.com) e inicie sessão com o Azure [conta](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account). Se ainda não tiver uma conta, pode inscrever-se para obter um [avaliação gratuita](https://azure.microsoft.com/offers/ms-azr-0044p).
2. No portal de Olá, clique em **+ novo** > **computação** > **Datacenter do Windows Server 2016**. 
3. No Olá **Datacenter do Windows Server 2016** painel que aparece, deixe *Resource Manager* selecionado em **selecionar um modelo de implementação**e clique em **criar** .
4. No Olá **Noções básicas** painel apresentado, introduza os seguintes valores de Olá, deixe as restantes opções predefinidas de Olá ou selecione ou introduza os seus próprios valores e clique em Olá **OK** botão:

    |Definição|Valor|
    |---|---|
    |Nome|MyVm|
    |Grupo de recursos|Deixe **criar nova** selecionada e introduza *MyResourceGroup*|
    |Localização|EUA Oeste 2|

    Se tiver tooAzure novo, saiba mais sobre [grupos de recursos](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#resource-group), [subscrições](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#subscription), e [localizações](https://azure.microsoft.com/regions) (que também são denominados tooas regiões).
5. No Olá **escolher um tamanho** painel apresentado, introduza *8* no Olá **núcleos mínimo** caixa, em seguida, clique em **ver todos os**.
6. Clique em **DS4_V2 padrão**, ou suportada qualquer uma VM, em seguida, clique em Olá **selecione** botão.
7. No Olá **definições** painel que aparece, deixe todas as definições como-é, exceto clique **ativado** em **acelerados redes**, em seguida, clique em Olá **OK** botão. **Nota:** se, nos passos anteriores, selecionou os valores de tamanho VM, sistema operativo ou localização que não estão listados no Olá [limitações](#Limitations) secção deste artigo, **Accelerated redes**não está visível.
8. No Olá **resumo** painel apresentado, clique em Olá **OK** botão. Azure inicia a criação de Olá VM. Criação de VM demora alguns minutos.
9. Olá tooinstall acelerados controlador de rede para o Windows, Olá concluir os passos em Olá [configurar Windows](#configure-windows) secção deste artigo.

### <a name="windows-powershell"></a>PowerShell
1. Instale a versão mais recente do Olá do Olá Azure PowerShell [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) módulo. Se tiver tooAzure nova do PowerShell, leia Olá [descrição geral do Azure PowerShell](/powershell/azure/get-started-azureps?toc=%2fazure%2fvirtual-network%2ftoc.json) artigo.
2. Inicie uma sessão do PowerShell, clicando em botão Iniciar do Windows hello, escrevendo **powershell**, em seguida, clicar em **PowerShell** de resultados da pesquisa Olá.
3. Na janela do PowerShell, introduza Olá `login-azurermaccount` toosign de comando com o Azure [conta](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account). Se ainda não tiver uma conta, pode inscrever-se para obter um [avaliação gratuita](https://azure.microsoft.com/offers/ms-azr-0044p).
4. No seu browser, copie Olá seguintes script:
    ```powershell
    $RgName="MyResourceGroup"
    $Location="westus2"
    
    # Create a resource group
    New-AzureRmResourceGroup `
      -Name $RgName `
      -Location $Location
    
    # Create a subnet
    $Subnet = New-AzureRmVirtualNetworkSubnetConfig `
      -Name MySubnet `
      -AddressPrefix 10.0.0.0/24
    
    # Create a virtual network
    $Vnet=New-AzureRmVirtualNetwork `
      -ResourceGroupName $RgName `
      -Location $Location `
      -Name MyVnet `
      -AddressPrefix 10.0.0.0/16 `
      -Subnet $Subnet

    # Create a public IP address
    $Pip = New-AzureRmPublicIpAddress `
      -Name MyPublicIp `
      -ResourceGroupName $RgName `
      -Location $Location `
      -AllocationMethod Static

    # Create a virtual network interface and associate hello public IP address tooit
    $Nic = New-AzureRmNetworkInterface `
      -Name MyNic `
      -ResourceGroupName $RgName `
      -Location $Location `
      -SubnetId $Vnet.Subnets[0].Id `
      -PublicIpAddressId $Pip.Id `
      -EnableAcceleratedNetworking
     
    # Define a credential object for hello VM. PowerShell prompts you for a username and password.
    $Cred = Get-Credential

    # Create a virtual machine configuration
    $VmConfig = New-AzureRmVMConfig `
      -VMName MyVM -VMSize Standard_DS4_v2 | `
      Set-AzureRmVMOperatingSystem `
      -Windows `
      -ComputerName myVM `
      -Credential $Cred | `
    Set-AzureRmVMSourceImage `
      -PublisherName MicrosoftWindowsServer `
      -Offer WindowsServer `
      -Skus 2016-Datacenter `
      -Version latest | `
    Add-AzureRmVMNetworkInterface -Id $Nic.Id 

    # Create hello virtual machine.    
    New-AzureRmVM `
      -ResourceGroupName $RgName `
      -Location $Location `
      -VM $VmConfig
    #
    ```
5. Na janela do PowerShell, faça duplo clique script de Olá toopaste e iniciar a execução-lo. Lhe for pedido um nome de utilizador e palavra-passe. Utilize estas credenciais toolog toohello VM ao ligar tooit no passo seguinte Olá. Se o script de Olá falha e alterar os valores no script de Olá antes de executar este, confirme valores Olá que utilizou para o tamanho da VM, sistema operativo, e localização estão listadas no Olá [limitações](#Limitations) secção deste artigo.
6. Olá tooinstall acelerados controlador de rede para o Windows, Olá concluir os passos em Olá [configurar Windows](#configure-windows) secção deste artigo.

### <a name="configure-windows"></a>Configurar o Windows
Depois de criar Olá VM no Azure, tem de instalar o controlador de rede na melhoria de Olá para Windows. Antes de concluir os seguintes passos de Olá, tem de ter criado uma VM do Windows com redes na melhoria utilizando qualquer um dos Olá [portal](#windows-portal) ou [PowerShell](#windows-powershell) passos neste artigo. 

1. A partir do browser da Internet, abra Olá Azure [portal](https://portal.azure.com) e inicie sessão com o Azure [conta](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account). Se ainda não tiver uma conta, pode inscrever-se para obter um [avaliação gratuita](https://azure.microsoft.com/offers/ms-azr-0044p).
2. Na caixa de Olá que contém texto Olá *procurar recursos* Olá parte superior do portal do Azure de Olá, escreva *MyVm*. Quando **MyVm** é apresentado nos resultados de pesquisa de Olá, clique no mesmo.
3. No Olá **MyVm** painel apresentado, clique em Olá **Connect** botão no canto esquerdo superior do painel de Olá Olá. **Nota:** se **criar** é visível em Olá **Connect** botão, Azure não ainda acabou de criar Olá VM. Clique em **Connect** apenas depois de já não vê **criar** em Olá **Connect** botão.
4. Permitir o Olá toodownload do browser **MyVm.rdp** ficheiro.  Depois de transferido, clique em Olá ficheiro tooopen-lo. 
5. Clique em Olá **Connect** botão no Olá **ligação ao ambiente de trabalho remoto** caixa que aparece, notificam que Olá não seja possível identificar o publicador da ligação remota Olá.
6. No Olá **segurança do Windows** caixa apresentada, clique em **mais opções**, em seguida, clique em **utilizar uma conta diferente**. Introduza Olá nome de utilizador e palavra-passe que introduziu no passo 4, em seguida, clique em Olá **OK** botão.
7. Clique em Olá **Sim** botão na caixa de ligação de ambiente de trabalho remoto Olá que aparece, notificam que não é possível verificar a identidade de Olá do computador remoto Olá.
8. Clique no botão de iniciar o Windows hello e clique em **Gestor de dispositivos**. Expanda Olá **adaptadores de rede** nós. Confirme que Olá **adaptador de Ethernet de função Virtual Mellanox ConnectX 3** for apresentada, conforme mostrado na Olá seguinte imagem:
   
    ![Gestor de dispositivos](./media/virtual-network-create-vm-accelerated-networking/image2.png)

9. Na melhoria de redes está agora ativada para a VM.

## <a name="create-a-linux-vm"></a>Criar uma VM do Linux
Pode utilizar Olá portal do Azure ou para o Azure [PowerShell](#linux-powershell) toocreate um Ubuntu ou SLES VM. Para RHEL e CentOS VMs é um fluxo de trabalho diferentes.  Consulte as instruções de Olá abaixo.

### <a name="linux-portal"></a>Portal
1. Registar-se Olá acelerado redes para pré-visualização do Linux, efetuando os passos 1 a 5 para Olá [criar uma VM com Linux - PowerShell](#linux-powershell) secção deste artigo.  Não é possível registar para a pré-visualização de Olá no portal de Olá.
2. Concluir os passos 1-8 de Olá em [criar uma VM do Windows - portal](#windows-portal) secção deste artigo. No passo 2, clique em **Ubuntu Server 16.04 LTS** em vez de **Datacenter do Windows Server 2016**. Para este tutorial, escolha toouse uma palavra-passe, em vez de uma chave SSH, embora para implementações de produção, pode utilizar. Se **acelerados redes** não aparecer quando concluir o passo 7 Olá [criar uma VM do Windows - portal](#windows-portal) secção deste artigo, é provável para uma das Olá seguintes motivos:
    - Ainda não está registado para a pré-visualização de Olá. Confirme que o seu estado de registo é **registada**, conforme explicado no passo 4 do Olá [criar uma VM com Linux - Powershell](#linux-powershell) secção deste artigo. **Nota:** se participaram no Olá Accelerated de rede para a pré-visualização de VMs do Windows (respetivo não toouse tooregister necessários mais acelerado redes para VMs do Windows), não está automaticamente registados para Olá Accelerated redes para Pré-visualização de VMs com Linux. Tem de registar para Olá Accelerated redes para VMs com Linux pré-visualizar tooparticipate no mesmo.
    - Não selecionou um tamanho de VM, o sistema operativo ou a localização indicada na Olá [limitações](#limitations) secção deste artigo.
3. Olá tooinstall acelerados controlador de rede para o Linux, Olá concluir os passos em Olá [configurar Linux](#configure-linux) secção deste artigo.

### <a name="linux-powershell"></a>PowerShell

>[!WARNING]
>Se criar VMs com Linux com redes na melhoria numa subscrição e, em seguida, tente toocreate uma VM do Windows com redes na melhoria no Olá mesma subscrição, Olá a criação de Windows VM-la poderá falhar. Durante esta pré-visualização, recomenda-se que teste o Linux e VMs do Windows com redes na melhoria em subscrições diferentes.
>

1. Instale a versão mais recente do Olá do Olá Azure PowerShell [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) módulo. Se tiver tooAzure nova do PowerShell, leia Olá [descrição geral do Azure PowerShell](/powershell/azure/get-started-azureps?toc=%2fazure%2fvirtual-network%2ftoc.json) artigo.
2. Inicie uma sessão do PowerShell, clicando em botão Iniciar do Windows hello, escrevendo **powershell**, em seguida, clicar em **PowerShell** de resultados da pesquisa Olá.
3. Na janela do PowerShell, introduza Olá `login-azurermaccount` toosign de comando com o Azure [conta](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account). Se ainda não tiver uma conta, pode inscrever-se para obter um [avaliação gratuita](https://azure.microsoft.com/offers/ms-azr-0044p).
4. Registar-se Olá acelerado redes para o Azure pré-visualização concluindo Olá os seguintes passos:
    - Enviar um e-mail demasiado[ axnpreview@microsoft.com ](mailto:axnpreview@microsoft.com?subject=Request%20to%20enable%20subscription%20%3csubscription%20id%3e) com o ID de subscrição do Azure e a utilização pretendida. Aguarde um e-mail de confirmação da Microsoft sobre a sua subscrição que está a ser ativada.
    - Introduza Olá tooconfirm comandos que estão registados para pré-visualização Olá os seguintes:
    
        ```powershell
        Get-AzureRmProviderFeature -FeatureName AllowAcceleratedNetworkingForLinux -ProviderNamespace Microsoft.Network
        ```

        Não continue com o passo 5 até **registada** aparece no Olá depois de introduzir o comando anterior Olá de saída. O resultado tem aspeto seguinte Olá saída antes de continuar:
    
        ```powershell
        FeatureName                        ProviderName      RegistrationState
        -----------                        ------------      -----------------
        AllowAcceleratedNetworkingForLinux Microsoft.Network Registered
        ```
        
      >[!NOTE]
      >Se participaram no Olá Accelerated de rede para a pré-visualização de VMs do Windows (respetivo não toouse tooregister necessários mais acelerado redes para VMs do Windows), não está automaticamente registados para Olá Accelerated de rede para a pré-visualização de VMs com Linux. Tem de registar para Olá Accelerated redes para VMs com Linux pré-visualizar tooparticipate no mesmo.
      >
5. No seu browser, copie Olá seguinte script substituindo Ubuntu ou SLES conforme pretendido.  Novamente, VM de Redhat e CentOS têm um fluxo de trabalho diferentes descrito abaixo:

    ```powershell
    $RgName="MyResourceGroup"
    $Location="westus2"
    
    # Create a resource group
    New-AzureRmResourceGroup `
      -Name $RgName `
      -Location $Location
    
    # Create a subnet
    $Subnet = New-AzureRmVirtualNetworkSubnetConfig `
      -Name MySubnet `
      -AddressPrefix 10.0.0.0/24
    
    # Create a virtual network
    $Vnet=New-AzureRmVirtualNetwork `
      -ResourceGroupName $RgName `
      -Location $Location `
      -Name MyVnet `
      -AddressPrefix 10.0.0.0/16 `
      -Subnet $Subnet

    # Create a public IP address
    $Pip = New-AzureRmPublicIpAddress `
      -Name MyPublicIp `
      -ResourceGroupName $RgName `
      -Location $Location `
      -AllocationMethod Static

    # Create a virtual network interface and associate hello public IP address tooit
    $Nic = New-AzureRmNetworkInterface `
      -Name MyNic `
      -ResourceGroupName $RgName `
      -Location $Location `
      -SubnetId $Vnet.Subnets[0].Id `
      -PublicIpAddressId $Pip.Id `
      -EnableAcceleratedNetworking
     
    # Create a new Storage account and define hello new VM’s OSDisk name and its URI
    # Must end with ".vhd" extension
    $OSDiskName = "MyOsDiskName.vhd"
    # Storage account name must be between 3 and 24 characters in length and use numbers and lower-case letters only.
    $OSDiskSAName = "thestorageaccountname"  
    $StorageAccount = New-AzureRmStorageAccount -ResourceGroupName $RgName -Name $OSDiskSAName -Type "Standard_GRS" -Location $Location
    $OSDiskUri = $StorageAccount.PrimaryEndpoints.Blob.ToString() + "vhds/" + $OSDiskName
 
    # Define a credential object for hello VM. PowerShell prompts you for a username and password.
    $Cred = Get-Credential

    # Create a virtual machine configuration
    $VmConfig = New-AzureRmVMConfig `
      -VMName MyVM -VMSize Standard_DS4_v2 | `
      Set-AzureRmVMOperatingSystem `
      -Linux `
      -ComputerName myVM `
      -Credential $Cred | `
    Set-AzureRmVMSourceImage `
      -PublisherName Canonical `
      -Offer UbuntuServer `
      -Skus 16.04-LTS `
      -Version latest | `
    Add-AzureRmVMNetworkInterface -Id $Nic.Id | `
    Set-AzureRmVMOSDisk -Name $OSDiskName `
      -VhdUri $OSDiskUri `
      -CreateOption FromImage 

    # Create hello virtual machine.    
    New-AzureRmVM `
      -ResourceGroupName $RgName `
      -Location $Location `
      -VM $VmConfig
    ```
    
6. Na janela do PowerShell, faça duplo clique script de Olá toopaste e iniciar a execução-lo. Lhe for pedido um nome de utilizador e palavra-passe. Utilize estas credenciais toolog toohello VM ao ligar tooit no passo seguinte Olá. Se o script de Olá falhar, confirme se a:
    - Estão registados para pré-visualização Olá, conforme explicado no passo 4
    - Se alterar o tamanho da VM, tipo de sistema operativo ou valores da localização do script Olá antes de executar este, que os valores de Olá estão listados na Olá [limitações](#Limitations) secção deste artigo.
7. Olá tooinstall acelerados controlador de rede para o Linux, Olá concluir os passos em Olá [configurar Linux](#configure-linux) secção deste artigo.

### <a name="configure-linux"></a>Configurar Linux

Depois de criar Olá VM no Azure, tem de instalar o controlador de rede na melhoria de Olá para Linux. Antes de concluir os seguintes passos de Olá, tem de ter criado uma VM com Linux com redes na melhoria utilizando qualquer um dos Olá [portal](#linux-portal) ou [PowerShell](#linux-powershell) passos neste artigo. 

1. A partir do browser da Internet, abra Olá Azure [portal](https://portal.azure.com) e inicie sessão com o Azure [conta](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account). Se ainda não tiver uma conta, pode inscrever-se para obter um [avaliação gratuita](https://azure.microsoft.com/offers/ms-azr-0044p).
2. Olá parte superior do portal, toohello direito Olá de Olá *procurar recursos* barra, clique em Olá **> _** ícone toostart numa shell de nuvem de deteção (pré-visualização). Olá painel de shell de nuvem de Bash aparece na parte inferior de Olá do portal de Olá e após alguns segundos, apresenta um  **username@Azure:~ $** linha. Embora pode SSH toohello VM do seu computador, em vez de shell de nuvem Olá, instruções Olá deste tutorial partem do princípio de que está a utilizar a shell de nuvem Olá.
3. Olá parte superior do portal de Olá, na caixa de Olá que contém texto Olá *procurar recursos*, tipo *MyVm*. Quando **MyVm** é apresentado nos resultados de pesquisa de Olá, clique no mesmo.
4. No Olá **MyVm** painel apresentado, clique em Olá **Connect** botão no canto esquerdo superior do painel de Olá Olá. **Nota:** se **criar** é visível em Olá **Connect** botão, Azure não ainda acabou de criar Olá VM. Clique em **Connect** apenas depois de já não vê **criar** em Olá **Connect** botão.
5. Azure abre uma caixa informá-lo tooenter Olá `ssh adminuser@<ipaddress>`. Introduza este comando Olá nuvem shell (ou cópia a partir da caixa de Olá que antes eram no passo 4 e colá-lo na shell de nuvem toohello), em seguida, prima Enter.
6. Introduza **Sim** pergunta toohello solicitar que se pretender ligar toocontinue, em seguida, prima Enter.
7. Introduza a palavra-passe de Olá que introduziu durante a criação de Olá VM. Uma vez iniciado sessão com êxito toohello VM, verá um adminuser@MyVm:~ linha$. Agora são registados no toohello VM através de sessão de shell Olá na nuvem. **Nota:** nuvem shell tempo limite de sessões após 10 minutos de inatividade.

Neste momento, as instruções de Olá variam com base na distribuição Olá que estiver a utilizar. 

#### <a name="ubuntusles"></a>Ubuntu/SLES

1. Na linha de Olá, introduza `uname -r` e confirmar a versão de Olá para:

    * Ubuntu é "4.4.0-77-generic", ou superior
    * SLES é "4.4.59-92.20-default" ou superior

2. Crie um bond entre Olá vNIC de rede padrão e Olá acelerado vNIC de rede ao executar comandos de Olá que se seguem. Tráfego de rede utiliza Olá superior efetuar vNIC na melhoria de rede, enquanto bond Olá garante que o tráfego de rede não é interrompido em determinadas alterações de configuração.
          
     ```bash
     wget https://raw.githubusercontent.com/LIS/lis-next/master/tools/sriov/configure_hv_sriov.sh
     chmod +x ./configure_hv_sriov.sh
     sudo ./configure_hv_sriov.sh
     ```
3. Depois de executar o script Olá Olá VM será reiniciado depois de um segundo 60 colocar em pausa.
4. Uma vez Olá VM é reiniciada, restabeleça a ligação tooit, efetuando os passos 5 a 7 novamente.
5. Executar Olá `ifconfig` comando e confirme que tem pensar bond0 e interface Olá está a ser mostrada como cópia de segurança. 
 
 >[!NOTE]
      >As aplicações que utilizam redes na melhoria têm de comunicar através de Olá *bond0* interface, não *eth0*.  Pode alterar o nome da interface Olá antes de rede na melhoria atinge disponibilidade geral.

#### <a name="rhelcentos"></a>RHEL/CentOS

Criar um Red Hat Enterprise Linux ou VM do CentOS 7.3 requer alguns extra os controladores de mais recentes de tooload Olá necessárias para a SR-IOV e Olá Virtual função (vf) para a placa de rede Olá passos. Olá primeira fase de instruções de Olá prepara uma imagem que pode ser utilizado toomake um ou mais máquinas virtuais que tenham controladores de Olá previamente carregadas.

##### <a name="phase-one-prepare-a-red-hat-enterprise-linux-or-centos-73-base-image"></a>A primeira fase: preparar uma imagem de base do Red Hat Enterprise Linux ou CentOS 7.3. 

1.  Aprovisionar um não - SRIOV CentOS 7.3 VM no Azure

2.  Instale o LIS 4.2.2:
    
    ```bash
    wget http://download.microsoft.com/download/6/8/F/68FE11B8-FAA4-4F8D-8C7D-74DA7F2CFC8C/lis-rpms-4.2.2-2.tar.gz
    tar -xvf lis-rpms-4.2.2-2.tar.gz
    cd LISISO && sudo ./install.sh
    ```

3.  Transferir ficheiros de configuração
    
    ```bash
    cd /etc/udev/rules.d/  
    sudo wget https://raw.githubusercontent.com/LIS/lis-next/master/tools/sriov/60-hyperv-vf-name.rules 
    cd /usr/sbin/
    sudo wget https://raw.githubusercontent.com/LIS/lis-next/master/tools/sriov/hv_vf_name 
    sudo chmod +x hv_vf_name
    cd /etc/sysconfig/network-scripts/
    sudo wget https://raw.githubusercontent.com/LIS/lis-next/master/tools/sriov/ifcfg-vf1   
    ```

4.  Desaprovisionar esta VM

    ```bash
    sudo waagent -deprovision+user 
    ```

5.  No portal do Azure, parar esta VM; e aceda "Discos" do tooVM, o URI do VHD do Olá OSDisk de captura. Este URI contém o nome do VHD da imagem base Olá e a respetiva conta de armazenamento. 
 
##### <a name="phase-two-provision-new-vms-on-azure"></a>Fase dois: aprovisionar novas VMs no Azure

1.  Aprovisionar novas VMs com base com o New-AzureRMVMConfig utilizando Olá imagem base do VHD capturado na primeira fase, com AcceleratedNetworking ativada em vNIC Olá:

    ```powershell
    $RgName="MyResourceGroup"
    $Location="westus2"
    
    # Create a resource group
    New-AzureRmResourceGroup `
     -Name $RgName `
     -Location $Location

    # Create a subnet
    $Subnet = New-AzureRmVirtualNetworkSubnetConfig `
     -Name MySubnet `
     -AddressPrefix 10.0.0.0/24

    # Create a virtual network
    $Vnet=New-AzureRmVirtualNetwork `
     -ResourceGroupName $RgName `
     -Location $Location `
     -Name MyVnet `
     -AddressPrefix 10.0.0.0/16 `
     -Subnet $Subnet
    
    # Create a public IP address
    $Pip = New-AzureRmPublicIpAddress `
     -Name MyPublicIp `
     -ResourceGroupName $RgName `
     -Location $Location `
     -AllocationMethod Static
    
    # Create a virtual network interface and associate hello public IP address tooit
    $Nic = New-AzureRmNetworkInterface `
     -Name MyNic `
     -ResourceGroupName $RgName `
     -Location $Location `
     -SubnetId $Vnet.Subnets[0].Id `
     -PublicIpAddressId $Pip.Id `
     -EnableAcceleratedNetworking
    
    # Specify hello base image's VHD URI (from phase one step 5). 
    # Note: hello storage account of this base image vhd should have "Storage service encryption" disabled
    # See more from here: https://docs.microsoft.com/en-us/azure/storage/storage-service-encryption
    # This is just an example URI, you will need tooreplace this when running this script
    $sourceUri="https://myexamplesa.blob.core.windows.net/vhds/CentOS73-Base-Test120170629111341.vhd" 

    # Specify a URI for hello location from which hello new image binary large object (BLOB) is copied toostart hello virtual machine. 
    # Must end with ".vhd" extension
    $OsDiskName = "MyOsDiskName.vhd" 
    $destOsDiskUri = "https://myexamplesa.blob.core.windows.net/vhds/" + $OsDiskName
    
    # Define a credential object for hello VM. PowerShell prompts you for a username and password.
    $Cred = Get-Credential
    
    # Create a custom virtual machine configuration
    $VmConfig = New-AzureRmVMConfig `
     -VMName MyVM -VMSize Standard_DS4_v2 | `
    Set-AzureRmVMOperatingSystem `
     -Linux `
     -ComputerName myVM `
     -Credential $Cred | `
    Add-AzureRmVMNetworkInterface -Id $Nic.Id | `
    Set-AzureRmVMOSDisk `
     -Name $OsDiskName `
     -SourceImageUri $sourceUri `
     -VhdUri $destOsDiskUri `
     -CreateOption FromImage `
     -Linux
    
    # Create hello virtual machine.    
    New-AzureRmVM `
     -ResourceGroupName $RgName `
     -Location $Location `
     -VM $VmConfig
    ```

2.  Depois de VMs efetuar o arranque, verifique o dispositivo de VF Olá por "lspci" e verifique Olá Mellanox entrada. Por exemplo, deveremos ver este item de saída de lspci Olá:
    
    ```
    0001:00:02.0 Ethernet controller: Mellanox Technologies MT27500/MT27520 Family [ConnectX-3/ConnectX-3 Pro Virtual Function]
    ```
    
3.  Execute o script bonding Olá:

    ```bash
    sudo bondvf.sh
    ```

4.  Reiniciar Olá novas VMs:

    ```bash
    sudo reboot
    ```

Olá VM deverá começar com bond0 configurado e Olá caminho acelerados rede ativado.  Executar `ifconfig` tooconfirm.
