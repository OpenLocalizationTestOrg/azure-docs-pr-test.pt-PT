---
title: "aaaCreate um Azure virtual rede peering - modelos de implementação diferentes - subscrição mesmo | Microsoft Docs"
description: "Saiba como toocreate um peering de rede virtual entre redes virtuais criados através de modelos de implementação do Azure diferentes que existem no Olá mesma subscrição do Azure."
services: virtual-network
documentationcenter: 
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
ms.date: 07/17/2017
ms.author: jdial;narayan;annahar
ms.openlocfilehash: 365156d651c9042ed52baeb15bf629fcc5329af8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-peering---different-deployment-models-same-subscription"></a>Criar um peering de rede virtual - diferentes modelos de implementação, a mesma subscrição 

Neste tutorial, aprende toocreate uma rede virtual peering entre redes virtuais criadas através de modelos de implementação diferentes. Ambas as redes virtuais existem no Olá mesma subscrição. Peering duas redes virtuais ativa recursos toocommunicate de redes virtuais diferentes entre si com Olá mesmo largura de banda e latência dado a entender, os recursos de Olá foram no Olá mesma rede virtual. Saiba mais sobre [peering de rede Virtual](virtual-network-peering-overview.md). 

Olá passos toocreate um peering de rede virtual são diferentes, dependendo se as redes virtuais Olá são Olá idêntica ou diferente, subscrições e que [modelo de implementação do Azure](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json) redes virtuais Olá são criados através do. Saiba como toocreate a virtual rede peering noutros cenários, clicando em cenário Olá de Olá a tabela seguinte:

|Modelo de implementação do Azure  | Subscrição do Azure  |
|--------- |---------|
|[O Gestor de recursos](virtual-network-create-peering.md) |mesmo|
|[O Gestor de recursos](create-peering-different-subscriptions.md) |Diferentes|
|[Um Gestor de recursos, um clássico](create-peering-different-deployment-models-subscriptions.md) |Diferentes|

Não é possível criar uma rede virtual peering entre duas redes virtuais implementadas através do modelo de implementação clássica Olá. Um peering de rede virtual só é possível criar entre duas redes virtuais que existem no Olá mesma região do Azure. Se precisar de tooconnect redes virtuais que foram criados através do modelo de implementação clássica hello, ou que existe em diferentes regiões do Azure, pode utilizar um Azure [Gateway de VPN](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) tooconnect Olá redes virtuais. 

Pode utilizar Olá [portal do Azure](#portal), Olá Azure [interface de linha de comandos](#cli) (CLI), ou do Azure [PowerShell](#powershell) toocreate um peering de rede virtual. Clique em qualquer um dos Olá anterior ferramenta ligações toogo diretamente toohello passos para criar um peering de rede virtual com a ferramenta de escolha.

## <a name="cli"></a>Criar peering - Portal

1. Inicie sessão no toohello [portal do Azure](https://portal.azure.com). conta de Olá, que inicie sessão com tem de ter Olá as permissões necessárias toocreate um peering de rede virtual. Consulte Olá [permissões](#permissions) secção deste artigo para obter mais detalhes.
2. Clique em **+ novo**, clique em **redes**, em seguida, clique em **rede Virtual**.
3. No Olá **criar rede virtual** painel, introduza, ou selecione os valores de Olá seguintes definições, em seguida, clique em **criar**:
    - **Nome**: *myVnet1*
    - **Espaço de endereços**: *10.0.0.0/16*
    - **Nome da sub-rede**: *predefinido*
    - **Intervalo de endereços da sub-rede**: *10.0.0.0/24*
    - **Subscrição**: selecione a sua subscrição
    - **Grupo de recursos**: selecione **criar nova** e introduza *myResourceGroup*
    - **Localização**: *EUA leste*
4. Clique em **+ nova**. No Olá **Olá pesquisa Marketplace** caixa, escreva *rede Virtual*. Clique em **rede Virtual** quando for apresentada nos resultados de pesquisa de Olá. 
5. No Olá **rede Virtual** painel, selecione **clássico** no Olá **selecionar um modelo de implementação** caixa e, em seguida, clique em **criar**.
6. No Olá **criar rede virtual** painel, introduza, ou selecione os valores de Olá seguintes definições, em seguida, clique em **criar**:
    - **Nome**: *myVnet2*
    - **Espaço de endereços**: *10.1.0.0/16*
    - **Nome da sub-rede**: *predefinido*
    - **Intervalo de endereços da sub-rede**: *10.1.0.0/24*
    - **Subscrição**: selecione a sua subscrição
    - **Grupo de recursos**: selecione **utilizar existente** e selecione *myResourceGroup*
    - **Localização**: *EUA leste*
7. No Olá **procurar recursos** caixa, Olá parte superior do portal de Olá, tipo *myResourceGroup*. Clique em **myResourceGroup** quando for apresentada nos resultados de pesquisa de Olá. É apresentado um painel para Olá **myresourcegroup** grupo de recursos. grupo de recursos de Olá contém Olá duas redes virtuais criados nos passos anteriores.
8. Clique em **myVNet1**.
9. No Olá **myVnet1** painel apresentado, clique em **Peerings** da lista de vertical Olá das opções em Olá à esquerda do lado do painel de Olá.
10. No Olá **myVnet1 - Peerings** painel que antes eram, clique em **+ adicionar**
11. No Olá **adicionar peering** painel apresentado, introduza, ou selecione Olá seguintes opções e clique em **OK**:
     - **Nome**: *myVnet1ToMyVnet2*
     - **Modelo de implementação de rede virtual**: selecione **clássico**. 
     - **Subscrição**: selecione a sua subscrição
     - **Rede virtual**: clique em **escolha uma rede virtual**, em seguida, clique em **myVnet2**.
     - **Permitir o acesso de rede virtual:** Certifique-se de que **ativado** está selecionada.
    Não existem outras definições são utilizadas neste tutorial. ler toolearn sobre todas as definições de peering, [gerir peerings de rede virtual](virtual-network-manage-peering.md#create-a-peering).
12. Depois de clicar em **OK** no passo anterior Olá, Olá **adicionar peering** painel fecha e vir Olá **myVnet1 - Peerings** painel novamente. Após alguns segundos, Olá peering que criou aparece no painel de Olá. **Ligado** está listado no Olá **PEERING estado** coluna Olá **myVnet1ToMyVnet2** peering é criado.

    Olá peering agora é estabelecida. Quaisquer recursos do Azure, que criar a rede virtual estão agora toocommunicate consegue entre si através dos respetivos endereços IP. Se estiver a utilizar a resolução do nome do Azure de predefinido para as redes virtuais Olá, Olá recursos em redes virtuais Olá não estão nomes tooresolve capaz de várias redes virtuais Olá. Se pretender que os nomes de tooresolve várias redes virtuais num peering, terá de criar o seu próprio servidor DNS. Saiba como tooset segurança [resolução de nomes utilizando o seu próprio servidor DNS](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).
13. **Opcional**: Apesar de criação de máquinas virtuais não é abrangido neste tutorial, pode criar uma máquina virtual em cada rede virtual e ligar a partir de uma máquina virtual toohello outras toovalidate conectividade.
14. **Opcional**: toodelete Olá recursos que criar neste tutorial, a Olá concluir os passos em Olá [eliminar recursos](#delete-portal) secção deste artigo.

## <a name="cli"></a>Criar peering - CLI do Azure

1. [Instalar](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json) Olá CLI do Azure 1.0 toocreate Olá (virtual network clássica).
2. Abra uma sessão de comando e inicie sessão tooAzure utilizando Olá `azure login` comando.
3. Executar Olá CLI no modo de gestão do serviço introduzindo Olá `azure config mode asm` comando.
4. Introduza Olá os seguintes comandos toocreate Olá (virtual network clássica):
 
    ```azurecli
    azure network vnet create --vnet myVnet2 --address-space 10.1.0.0 --cidr 16 --location "East US"
    ```

5. Crie um grupo de recursos e uma rede virtual (Resource Manager). Pode utilizar Olá CLI 1.0 ou 2.0 ([instalar](/cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json)). Neste tutorial, Olá CLI 2.0 é rede virtual de Olá toocreate utilizados (Resource Manager), uma vez que 2.0 tem de ser utilizado toocreate Olá peering. Execute Olá seguinte bash script da CLI do seu computador local com Olá CLI 2.0.4 ou posterior instalado. Para obter as opções de execução bash scripts CLI num cliente Windows, consulte [Olá CLI do Azure a executar no Windows](../virtual-machines/windows/cli-options.md?toc=%2fazure%2fvirtual-network%2ftoc.json). Também pode executar o script de Olá utilizando Olá Shell de nuvem do Azure. Olá Shell de nuvem do Azure é uma shell de deteção livre que podem ser executados diretamente no Olá portal do Azure. Tem Olá CLI do Azure pré-instalado e configurado toouse com a sua conta. Clique em Olá **experimente** clique no botão no script de Olá que se segue, que invoca uma Shell de nuvem que os registos pode iniciar sessão tooyour conta do Azure com. tooexecute Olá script, clique em Olá **cópia** botão e colar, conteúdo de Olá para a Shell de nuvem, em seguida, prima `Enter`.

    ```azurecli-interactive
    #!/bin/bash

    # Create a resource group.
    az group create \
      --name myResourceGroup \
      --location eastus

    # Create hello virtual network (Resource Manager).
    az network vnet create \
      --name myVnet1 \
      --resource-group myResourceGroup \
      --location eastus \
      --address-prefix 10.0.0.0/16
    ```

6. Crie uma peering entre Olá duas redes virtuais criadas através de modelos de implementação diferentes Olá de rede virtual. Copie Olá seguindo o editor de texto do script tooa do seu PC. Substitua `<subscription id>` com o ID de subscrição Se não souber o Id de subscrição, introduza Olá `az account show` comando. Olá valor para **id** Olá saída é o ID de subscrição Cole o script de Olá modificada na sessão CLI tooyour e, em seguida, prima `Enter`.

    ```azurecli-interactive
    # Get hello id for VNet1.
    vnet1Id=$(az network vnet show \
      --resource-group myResourceGroup \
      --name myVnet1 \
      --query id --out tsv)

    # Peer VNet1 tooVNet2.
    az network vnet peering create \
      --name myVnet1ToMyVnet2 \
      --resource-group myResourceGroup \
      --vnet-name myVnet1 \
      --remote-vnet-id /subscriptions/<subscription id>/resourceGroups/Default-Networking/providers/Microsoft.ClassicNetwork/virtualNetworks/myVnet2 \
      --allow-vnet-access
    ```
7. Após a execução do script Olá, reveja Olá peering para a rede virtual de Olá (Resource Manager). Cópia Olá a seguir comando, cole-o na sua sessão do CLI e, em seguida, prima `Enter`:

    ```azurecli-interactive
    az network vnet peering list \
      --resource-group myResourceGroup \
      --vnet-name myVnet1 \
      --output table
    ```
    
    Olá saída apresenta **ligado** no Olá **PeeringState** coluna. 

    Quaisquer recursos do Azure, que criar a rede virtual estão agora toocommunicate consegue entre si através dos respetivos endereços IP. Se estiver a utilizar a resolução do nome do Azure de predefinido para as redes virtuais Olá, Olá recursos em redes virtuais Olá não estão nomes tooresolve capaz de várias redes virtuais Olá. Se pretender que os nomes de tooresolve várias redes virtuais num peering, terá de criar o seu próprio servidor DNS. Saiba como tooset segurança [resolução de nomes utilizando o seu próprio servidor DNS](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).
8. **Opcional**: Apesar de criação de máquinas virtuais não é abrangido neste tutorial, pode criar uma máquina virtual em cada rede virtual e ligar a partir de uma máquina virtual toohello outras toovalidate conectividade.
9. **Opcional**: toodelete Olá recursos que criar neste tutorial, Olá concluir os passos em [eliminar recursos](#delete-cli) neste artigo.

## <a name="powershell"></a>Criar peering - PowerShell

1. Instale a versão mais recente do Olá do Olá PowerShell [Azure](https://www.powershellgallery.com/packages/Azure) e [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) módulos. Se estiver tooAzure nova do PowerShell, consulte [descrição geral do Azure PowerShell](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json).
2. Inicie uma sessão do PowerShell.
3. No PowerShell, inicie sessão no tooAzure introduzindo Olá `Add-AzureAccount` comando.
4. toocreate uma rede virtual (clássica) com o PowerShell, tem de criar um novo, ou modifique um existente, o ficheiro de configuração de rede. Saiba como demasiado[exportar, atualizar e importar ficheiros de configuração de rede](virtual-networks-using-network-configuration-file.md). Olá ficheiro deve incluir seguinte Olá **VirtualNetworkSite** elemento de rede virtual Olá utilizado neste tutorial:

    ```xml
    <VirtualNetworkSite name="myVnet2" Location="East US">
      <AddressSpace>
        <AddressPrefix>10.1.0.0/16</AddressPrefix>
      </AddressSpace>
      <Subnets>
        <Subnet name="default">
          <AddressPrefix>10.1.0.0/24</AddressPrefix>
        </Subnet>
      </Subnets>
    </VirtualNetworkSite>
    ```

    > [!WARNING]
    > Importar um ficheiro de configuração foi alterada de rede pode fazer com que as alterações tooexisting redes virtuais (clássica) na sua subscrição. Certifique-se apenas a adicionar rede virtual anterior de Olá e que não alterar ou remover quaisquer redes virtuais existentes da sua subscrição. 
5. Inicie sessão na rede virtual do tooAzure toocreate Olá (Resource Manager), introduzindo Olá `login-azurermaccount` comando. conta de Olá, que inicie sessão com tem de ter Olá as permissões necessárias toocreate um peering de rede virtual. Consulte Olá [permissões](#permissions) secção deste artigo para obter mais detalhes.
6. Crie um grupo de recursos e uma rede virtual (Resource Manager). Copie o script de Olá, cole-o PowerShell e, em seguida, prima `Enter`.

    ```powershell
    # Create a resource group.
      New-AzureRmResourceGroup -Name myResourceGroup -Location eastus

    # Create hello virtual network (Resource Manager).
      $vnet1 = New-AzureRmVirtualNetwork `
      -ResourceGroupName myResourceGroup `
      -Name 'myVnet1' `
      -AddressPrefix '10.0.0.0/16' `
      -Location eastus
    ```

7. Crie uma peering entre Olá duas redes virtuais criadas através de modelos de implementação diferentes Olá de rede virtual. Copie Olá seguindo o editor de texto do script tooa do seu PC. Substitua `<subscription id>` com o ID de subscrição Se não souber o Id de subscrição, introduza Olá `Get-AzureRmSubscription` comando tooview-lo. Olá valor para **Id** Olá devolveu o resultado é o ID de subscrição. script do tooexecute Olá, Olá de cópia modificado script no seu editor de texto, em seguida, clique com botão direito na sessão do PowerShell e, em seguida, prima `Enter`.

    ```powershell
    # Peer VNet1 tooVNet2.
    Add-AzureRmVirtualNetworkPeering `
      -Name myVnet1ToMyVnet2 `
      -VirtualNetwork $vnet1 `
      -RemoteVirtualNetworkId /subscriptions/<subscription Id>/resourceGroups/Default-Networking/providers/Microsoft.ClassicNetwork/virtualNetworks/myVnet2
    ```

8. Após a execução do script Olá, reveja Olá peering para a rede virtual de Olá (Resource Manager). Cópia Olá a seguir comando, colá-lo na sua sessão do PowerShell e, em seguida, prima `Enter`:

    ```powershell
    Get-AzureRmVirtualNetworkPeering `
      -ResourceGroupName myResourceGroup `
      -VirtualNetworkName myVnet1 `
      | Format-Table VirtualNetworkName, PeeringState
    ```

    Olá saída apresenta **ligado** no Olá **PeeringState** coluna.

    Quaisquer recursos do Azure, que criar a rede virtual estão agora toocommunicate consegue entre si através dos respetivos endereços IP. Se estiver a utilizar a resolução do nome do Azure de predefinido para as redes virtuais Olá, Olá recursos em redes virtuais Olá não estão nomes tooresolve capaz de várias redes virtuais Olá. Se pretender que os nomes de tooresolve várias redes virtuais num peering, terá de criar o seu próprio servidor DNS. Saiba como tooset segurança [resolução de nomes utilizando o seu próprio servidor DNS](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).

9. **Opcional**: Apesar de criação de máquinas virtuais não é abrangido neste tutorial, pode criar uma máquina virtual em cada rede virtual e ligar a partir de uma máquina virtual toohello outras toovalidate conectividade.
10. **Opcional**: toodelete Olá recursos que criar neste tutorial, Olá concluir os passos em [eliminar recursos](#delete-powershell) neste artigo.
 
## <a name="permissions"></a>Permissões

contas de Olá que utilizar toocreate um peering de rede virtual tem de ter permissões de função necessários Olá ou. Por exemplo, se foram peering duas redes virtuais com o nome myVnet1 e myVnet2, deve ser atribuída à conta Olá seguinte função mínima ou as permissões para cada rede virtual:
    
|Rede virtual|Modelo de implementação|Função|Permissões|
|---|---|---|---|
|myVnet1|Resource Manager|[Contribuidor de Rede](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)|Microsoft.Network/virtualNetworks/virtualNetworkPeerings/write|
| |Clássica|[Contribuidor de Rede Clássica](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#classic-network-contributor)|N/D|
|myVnet2|Resource Manager|[Contribuidor de Rede](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)|Microsoft.Network/virtualNetworks/peer|
||Clássica|[Contribuidor de Rede Clássica](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#classic-network-contributor)|Microsoft.ClassicNetwork/virtualNetworks/peer|

Saiba mais sobre [funções incorporadas](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) e atribuir permissões específicas demasiado[funções personalizadas](../active-directory/role-based-access-control-custom-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json) (apenas para o Resource Manager).

## <a name="delete"></a>Eliminar recursos
Quando tiver terminado neste tutorial, pode querer recursos de Olá toodelete que criou no tutorial Olá, pelo que não implicar custos de utilização. Também eliminar um grupo de recursos elimina todos os recursos que estão no grupo de recursos de Olá.

### <a name="delete-portal"></a>Portal do Azure

1. Na caixa de pesquisa de portal Olá, introduza **myResourceGroup**. Nos resultados de pesquisa de Olá, clique em **myResourceGroup**.
2. No Olá **myResourceGroup** painel, clique em Olá **eliminar** ícone.
3. a eliminação de Olá tooconfirm, no Olá **Olá tipo nome do grupo de recursos** box, introduza **myResourceGroup**e, em seguida, clique em **eliminar**.

### <a name="delete-cli"></a>CLI do Azure

1. Utilize a rede virtual do Azure CLI 2.0 de Olá toodelete Olá (Resource Manager) com Olá os seguintes comandos:

    ```azurecli-interactive
    az group delete --name myResourceGroup --yes
    ```

2. Utilize Olá CLI do Azure 1.0 toodelete Olá (virtual network clássica) com Olá os seguintes comandos:

    ```azurecli
    azure config mode asm

    azure network vnet delete --vnet myVnet2 --quiet
    ```

### <a name="delete-powershell"></a>PowerShell

1. Introduza Olá os seguintes comandos toodelete Olá rede virtual (Resource Manager):

    ```powershell
    Remove-AzureRmResourceGroup -Name myResourceGroup -Force
    ```

2. toodelete Olá rede virtual (clássica) com o PowerShell, tem de modificar um ficheiro de configuração de rede existente. Saiba como demasiado[exportar, atualizar e importar ficheiros de configuração de rede](virtual-networks-using-network-configuration-file.md). Remova Olá seguir VirtualNetworkSite elemento de rede virtual Olá utilizado neste tutorial:

    ```xml
    <VirtualNetworkSite name="myVnet2" Location="East US">
      <AddressSpace>
        <AddressPrefix>10.1.0.0/16</AddressPrefix>
      </AddressSpace>
      <Subnets>
        <Subnet name="default">
          <AddressPrefix>10.1.0.0/24</AddressPrefix>
        </Subnet>
      </Subnets>
    </VirtualNetworkSite>
    ```

    > [!WARNING]
    > Importar um ficheiro de configuração foi alterada de rede pode fazer com que as alterações tooexisting redes virtuais (clássica) na sua subscrição. Certifique-se de que apenas remove rede virtual anterior de Olá e que não alterar ou remover quaisquer outras redes virtuais existentes da sua subscrição. 

## <a name="next-steps"></a>Passos seguintes

- Exaustivamente familiarizar-se com importante [restrições de peering de rede virtual e comportamentos](virtual-network-manage-peering.md#requirements-and-constraints) antes de criar uma rede virtual para a produção de peering utilize.
- Saiba mais sobre todos os [definições de rede virtual peering](virtual-network-manage-peering.md#create-a-peering).
- Saiba como demasiado[criar um hub- and -spoke topologia de rede](/azure/architecture/reference-architectures/hybrid-networking/hub-spoke?toc=%2fazure%2fvirtual-network%2ftoc.json#vnet-peering) com peering de rede virtual.
