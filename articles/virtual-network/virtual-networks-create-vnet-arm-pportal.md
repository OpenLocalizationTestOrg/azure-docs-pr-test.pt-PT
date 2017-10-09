---
title: "aaaCreate uma Azure virtual network com várias sub-redes | Microsoft Docs"
description: "Saiba como toocreate uma rede virtual com várias sub-redes no Azure."
services: virtual-network
documentationcenter: 
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 4ad679a4-a959-4e48-a317-d9f5655a442b
ms.service: virtual-network
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/26/2017
ms.author: jdial
ms.custom: 
ms.openlocfilehash: 0f56fa6ac24537d33b8e217f5b03f387826ab487
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-with-multiple-subnets"></a>Criar uma rede virtual com várias sub-redes

Neste tutorial, saiba como toocreate básica do Azure rede virtual que tenha separar sub-redes públicas e privadas. Pode criar recursos do Azure, como máquinas virtuais, ambientes do App Service, conjuntos de dimensionamento de Máquina Virtual, do Azure HDInsight e serviços em nuvem numa sub-rede. Recursos na redes virtuais podem comunicar entre si e com os recursos na outra rede virtual do redes tooa ligado.

Olá secções seguintes incluem passos que pode efetuar toocreate uma rede virtual, utilizando Olá [portal do Azure](#portal), Olá interface de linha de comandos do Azure ([CLI do Azure](#azure-cli)), [Azure PowerShell ](#powershell)e um [modelo Azure Resource Manager](#resource-manager-template). resultado de Olá é Olá mesmo, independentemente da ferramenta de que utiliza a rede virtual do toocreate Olá. Clique na ferramenta ligação toogo toothat secção do tutorial Olá. Saiba mais sobre todos os [rede virtual](virtual-network-manage-network.md) e [sub-rede](virtual-network-manage-subnet.md) definições.

Este artigo fornece os passos toocreate uma rede virtual através do modelo de implementação Resource Manager de Olá, que é o modelo de implementação de Olá que recomendamos a utilização quando criar novas redes virtuais. Se precisar de toocreate uma rede virtual (clássica), consulte [criar uma rede virtual (clássica)](create-virtual-network-classic.md). Se não estiver familiarizado com os modelos de implementação do Azure, consulte [modelos de implementação do Azure compreender](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json).

## <a name="portal"></a>Portal do Azure

1. Num browser da Internet, aceda toohello [portal do Azure](https://portal.azure.com). Inicie sessão com a sua [conta do Azure](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account). Se não tiver uma conta do Azure, pode inscrever-se para obter um [avaliação gratuita](https://azure.microsoft.com/offers/ms-azr-0044p).
2. No portal de Olá, clique em **+ novo** > **redes** > **rede Virtual**.
3. No Olá **criar rede virtual** painel, introduza Olá os seguintes valores e, em seguida, clique em **criar**:

    |Definição|Valor|
    |---|---|
    |Nome|myVnet|
    |Espaço de endereços|10.0.0.0/16|
    |Nome da sub-rede|Público|
    |Intervalo de endereços da sub-rede|10.0.0.0/24|
    |Grupo de recursos|Deixe **criar nova** selecionada e, em seguida, introduza **myResourceGroup**.|
    |Subscrição e localização|Selecione a sua subscrição e localização.

    Se tiver tooAzure novo, saiba mais sobre [grupos de recursos](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#resource-group), [subscrições](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#subscription), e [localizações](https://azure.microsoft.com/regions) (também referida tooas *regiões*).
4. No portal de Olá, pode criar apenas uma sub-rede quando criar uma rede virtual. Neste tutorial, crie uma sub-rede do segundo depois de criar rede virtual Olá. Mais tarde poderá criar recursos acessível através da Internet no Olá **pública** sub-rede. Também poderá criar recursos que não estão acessíveis a partir do Olá Internet no Olá **privada** sub-rede. toocreate Olá segunda sub-rede, Olá **procurar recursos** em Olá parte superior da página Olá, introduza **myVnet**. Nos resultados de pesquisa de Olá, clique em **myVnet**. Se tiver várias redes virtuais com o mesmo nome na sua subscrição de Olá, verifique os grupos de recursos Olá que estão listados em cada rede virtual. Certifique-se de que clica Olá **myVnet** procurar resultado que tenha o grupo de recursos de Olá **myResourceGroup**.
5. No Olá **myVnet** painel, em **definições**, clique em **sub-redes**.
6. No Olá **myVnet - sub-redes** painel, clique em **+ sub-rede**.
7. No Olá **adicionar sub-rede** painel, para **nome**, introduza **privada**. Para **intervalo de endereços**, introduza **10.0.1.0/24**.  Clique em **OK**.
8. No Olá **myVnet - sub-redes** painel, reveja Olá sub-redes. Pode ver Olá **pública** e **privada** sub-redes que criou.
9. **Opcional:** toodelete Olá recursos que criar neste tutorial, Olá concluir os passos em [eliminar recursos](#delete-portal) neste artigo.

## <a name="azure-cli"></a>CLI do Azure

Comandos da CLI do Azure são hello iguais, se executar comandos Olá do Windows, Linux ou macOS. No entanto, existem diferenças scripts shells de sistema operativo. script de Olá no Olá passos a seguir executa na shell de deteção. 

1. [Instalar e configurar a CLI do Azure de Olá](/cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json). Certifique-se de que tem a versão mais recente do Olá de Olá CLI do Azure instalados. tooget ajuda para comandos da CLI, escreva `az <command> --help`. Em vez de instalar Olá CLI e respetivos pré-requisitos, pode utilizar Olá Shell de nuvem do Azure. Olá Shell de nuvem do Azure é uma shell de deteção livre que podem ser executados diretamente no Olá portal do Azure. Olá Shell de nuvem tem Olá CLI do Azure pré-instalado e configurado toouse com a sua conta. Olá toouse Shell de nuvem, clique em Olá Shell de nuvem (**> _**) botão, Olá parte superior do Olá [portal](https://portal.azure.com) ou basta clicar Olá *experimente* botão nos passos de Olá que se seguem. 
2. Se executar Olá CLI localmente, inicie sessão no tooAzure com Olá `az login` comando. Se utilizar Olá nuvem Shell, já está registado no.
3. Olá revisão seguinte script e os seus comentários. No seu browser, copie o script Olá e cole-o para a sua sessão CLI:

    ```azurecli-interactive
    #!/bin/bash
    
    # Create a resource group.
    az group create \
      --name myResourceGroup \
      --location eastus
    
    # Create a virtual network with one subnet named Public.
    az network vnet create \
      --name myVnet \
      --resource-group myResourceGroup \
      --subnet-name Public
    
    # Create an additional subnet named Private in hello virtual network.
    az network vnet subnet create \
      --name Private \
      --address-prefix 10.0.1.0/24 \
      --vnet-name myVnet \
      --resource-group myResourceGroup
    ```
    
4. Quando o script de Olá é terminado em execução, reveja as sub-redes de Olá para a rede virtual Olá. Copie Olá seguinte comando e, em seguida, cole-o para a sua sessão CLI:

    ```azurecli
    az network vnet subnet list --resource-group myResourceGroup --vnet-name myVnet --output table
    ```

5. **Opcional**: toodelete Olá recursos que criar neste tutorial, Olá concluir os passos em [eliminar recursos](#delete-cli) neste artigo.

## <a name="powershell"></a>PowerShell

1. Instale a versão mais recente do Olá do Olá PowerShell [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) módulo. Se estiver tooAzure nova do PowerShell, consulte [descrição geral do Azure PowerShell](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json).
2. Numa sessão do PowerShell, inicie sessão no tooAzure com seu [conta do Azure](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account) utilizando Olá `login-azurermaccount` comando.

3. Olá revisão seguinte script e os seus comentários. No seu browser, copie o script de Olá e cole-o sua sessão do PowerShell:

    ```powershell
    # Create a resource group.
    New-AzureRmResourceGroup `
      -Name myResourceGroup `
      -Location eastus
    
    # Create hello public and private subnets.
    $Subnet1 = New-AzureRmVirtualNetworkSubnetConfig `
      -Name Public `
      -AddressPrefix 10.0.0.0/24
    $Subnet2 = New-AzureRmVirtualNetworkSubnetConfig `
      -Name Private `
      -AddressPrefix 10.0.1.0/24
    
    # Create a virtual network.
    $Vnet=New-AzureRmVirtualNetwork `
      -ResourceGroupName myResourceGroup `
      -Location eastus `
      -Name myVnet `
      -AddressPrefix 10.0.0.0/16 `
      -Subnet $Subnet1,$Subnet2
    ```

4. tooreview Olá sub-redes para a rede virtual Olá, copie Olá seguinte comando e, em seguida, cole-o a sessão do PowerShell:

    ```powershell
    $Vnet.subnets | Format-Table Name, AddressPrefix
    ```

5. **Opcional**: toodelete Olá recursos que criar neste tutorial, Olá concluir os passos em [eliminar recursos](#delete-powershell) neste artigo.

## <a name="resource-manager-template"></a>Modelo do Resource Manager

Pode implementar uma rede virtual, utilizando um modelo Azure Resource Manager. toolearn mais informações sobre modelos, consulte [que é o Gestor de recursos](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json#template-deployment). modelo de Olá tooaccess e toolearn sobre os respetivos parâmetros, consulte Olá [criar uma rede virtual com duas sub-redes](https://azure.microsoft.com/resources/templates/101-vnet-two-subnets/) modelo. Pode implementar a modelo Olá utilizando Olá [portal](#template-portal), [CLI do Azure](#template-cli), ou [PowerShell](#template-powershell).

**Opcional:** toodelete Olá recursos que criar neste tutorial, a Olá concluir os passos em qualquer subsecções de [eliminar recursos](#delete) neste artigo.

### <a name="template-portal"></a>Portal do Azure

1. No seu browser, abra Olá [página modelo](https://azure.microsoft.com/resources/templates/101-vnet-two-subnets).
2. Clique em Olá **implementar tooAzure** botão. Se ainda não tiver sessão iniciada no tooAzure, inicie sessão no ecrã de início de sessão portal do Azure Olá que aparece.
3. Inicie sessão no portal de toohello utilizando o [conta do Azure](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account). Se não tiver uma conta do Azure, pode inscrever-se para obter um [avaliação gratuita](https://azure.microsoft.com/offers/ms-azr-0044p).
4. Introduza Olá valores para parâmetros de Olá os seguintes:

    |Parâmetro|Valor|
    |---|---|
    |Subscrição|Selecione a sua subscrição|
    |Grupo de recursos|myResourceGroup|
    |Localização|Selecione uma localização|
    |Nome da Vnet|myVnet|
    |Prefixo de endereço Vnet|10.0.0.0/16|
    |Subnet1Prefix|10.0.0.0/24|
    |Subnet1Name|Público|
    |Subnet2Prefix|10.0.1.0/24|
    |Subnet2Name|Privado|

5. Concordo toohello termos e condições e, em seguida, clique em **Compra** rede virtual do toodeploy Olá.

### <a name="template-cli"></a>CLI do Azure

1. [Instalar e configurar a CLI do Azure de Olá](/cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json). Certifique-se de que tem a versão mais recente do Olá de Olá CLI do Azure instalados. tooget ajuda para comandos da CLI, escreva `az <command> --help`. Em vez de instalar Olá CLI e respetivos pré-requisitos, pode utilizar Olá Shell de nuvem do Azure. Olá Shell de nuvem do Azure é uma shell de deteção livre que podem ser executados diretamente no Olá portal do Azure. Olá Shell de nuvem tem Olá CLI do Azure pré-instalado e configurado toouse com a sua conta. Olá toouse Shell de nuvem, clique em Olá nuvem Shell **> _** botão, Olá parte superior do Olá [portal](https://portal.azure.com), ou basta clicar Olá **experimente** botão nos passos de Olá que se seguem. 
2. Se executar Olá CLI localmente, inicie sessão no tooAzure com Olá `az login` comando. Se utilizar Olá nuvem Shell, já está registado no.
3. um grupo de recursos de rede virtual Olá toocreate, cópia Olá apresentado a seguir comando e cole-o sua sessão CLI:

    ```azurecli-interactive
    az group create --name myResourceGroup --location eastus
    ```
    
4. Pode implementar a modelo Olá utilizando uma das seguintes opções de parâmetros de Olá:
    - **Valores de parâmetro predefinidos**. Introduza Olá os seguintes comandos:
    
        ```azurecli-interactive
        az group deployment create --resource-group myResourceGroup --name VnetTutorial --template-uri https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vnet-two-subnets/azuredeploy.json`
        ```
    - **Valores de parâmetro personalizado**. Transferir e modificar o modelo de Olá antes de implementar o modelo de Olá. Também pode implementar a modelo de Olá utilizando parâmetros na linha de comandos Olá ou implementar a modelo de Olá com um ficheiro de parâmetros separado. toodownload Olá parâmetros de modelo e os ficheiros, clique em Olá **procurar no GitHub** botão Olá [criar uma rede virtual com duas sub-redes](https://azure.microsoft.com/resources/templates/101-vnet-two-subnets/) página do modelo. No GitHub, clique em Olá **azuredeploy.parameters.json** ou **azuredeploy. JSON** ficheiro. Em seguida, clique em Olá **Raw** ficheiro do botão toodisplay Olá. No seu browser, copie o conteúdo de Olá do ficheiro de Olá. Guarde Olá conteúdo tooa ficheiro no seu computador. Pode modificar os valores de parâmetros de Olá no modelo de Olá ou implementar a modelo de Olá com um ficheiro de parâmetros separado.  

    mais informações sobre como toolearn como toodeploy modelos através destes métodos, escreva `az group deployment create --help`.

### <a name="template-powershell"></a>PowerShell

1. Instale a versão mais recente do Olá do Olá PowerShell [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) módulo. Se estiver tooAzure nova do PowerShell, consulte [descrição geral do Azure PowerShell](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json).
2. Numa sessão do PowerShell, toosign no seu [conta do Azure](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account), introduza `login-azurermaccount`.
3. toocreate um grupo de recursos de rede virtual Olá, introduza Olá os seguintes comandos:

    ```powershell
    New-AzureRmResourceGroup -Name myResourceGroup -Location eastus
    ```
    
4. Pode implementar a modelo Olá utilizando uma das seguintes opções de parâmetros de Olá:
    - **Valores de parâmetro predefinidos**. Introduza Olá os seguintes comandos:
    
        ```powershell
        New-AzureRmResourceGroupDeployment -Name VnetTutorial -ResourceGroupName myResourceGroup -TemplateUri https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vnet-two-subnets/azuredeploy.json
        ```
        
    - **Valores de parâmetro personalizado**. Transferir e modificar o modelo de Olá antes de implementá-lo. Também pode implementar a modelo de Olá utilizando parâmetros na linha de comandos Olá ou implementar a modelo de Olá com um ficheiro de parâmetros separado. toodownload Olá parâmetros de modelo e os ficheiros, clique em Olá **procurar no GitHub** botão Olá [criar uma rede virtual com duas sub-redes](https://azure.microsoft.com/resources/templates/101-vnet-two-subnets/) página do modelo. No GitHub, clique em Olá **azuredeploy.parameters.json** ou **azuredeploy. JSON** ficheiro. Em seguida, clique em Olá **Raw** ficheiro do botão toodisplay Olá. No seu browser, copie o conteúdo de Olá do ficheiro de Olá. Guarde Olá conteúdo tooa ficheiro no seu computador. Pode modificar os valores de parâmetros de Olá no modelo de Olá ou implementar a modelo de Olá com um ficheiro de parâmetros separado.  

    mais informações sobre como toolearn como toodeploy modelos através destes métodos, escreva `Get-Help New-AzureRmResourceGroupDeployment`. 

## <a name="delete"></a>Eliminar recursos

Quando concluir este tutorial, pode querer recursos de Olá toodelete que criou, para que não implicar custos de utilização. Também eliminar um grupo de recursos elimina todos os recursos que estão no grupo de recursos de Olá.

### <a name="delete-portal"></a>Portal do Azure

1. Na caixa de pesquisa de portal Olá, introduza **myResourceGroup**. Nos resultados de pesquisa de Olá, clique em **myResourceGroup**.
2. No Olá **myResourceGroup** painel, clique em Olá **eliminar** ícone.
3. a eliminação de Olá tooconfirm, no Olá **Olá tipo nome do grupo de recursos** box, introduza **myResourceGroup**e, em seguida, clique em **eliminar**.

### <a name="delete-cli"></a>CLI do Azure

Numa sessão CLI, introduza Olá os seguintes comandos:

```azurecli-interactive
az group delete --name myResourceGroup --yes
```

### <a name="delete-powershell"></a>PowerShell

Numa sessão do PowerShell, introduza Olá os seguintes comandos:

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="next-steps"></a>Passos seguintes

- Consulte toolearn sobre todas as definições da sub-rede e a rede virtual [gerir redes virtuais](virtual-network-manage-network.md#view-vnet) e [gerir sub-redes da rede virtual](virtual-network-manage-subnet.md#create-subnet). Tem várias opções para utilizar redes virtuais e sub-redes um requisitos diferentes do ambiente toomeet de produção.
- toofilter entrada e saída tráfego de sub-rede, criar e aplicar [grupos de segurança de rede](virtual-networks-nsg.md) toosubnets.
- Criar um [Windows](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-network%2ftoc.json) ou um [Linux](../virtual-machines/linux/quick-create-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) máquina virtual e, em seguida, ligue-o tooan de rede virtual existente.
- redes virtuais tooconnect dois na mesma localização do Azure de Olá, crie um [peering de rede virtual](virtual-network-peering-overview.md) entre redes virtuais Olá.
- Ligar a rede no local do Olá rede virtual tooan utilizando um [Gateway de VPN](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) ou [Azure ExpressRoute](../expressroute/expressroute-howto-linkvnet-portal-resource-manager.md?toc=%2fazure%2fvirtual-network%2ftoc.json) circuito.
