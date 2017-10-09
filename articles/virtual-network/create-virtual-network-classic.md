---
title: "aaaCreate uma rede virtual do Azure (clássica) com várias sub-redes | Microsoft Docs"
description: "Saiba como toocreate uma rede virtual (clássica) com várias sub-redes no Azure."
services: virtual-network
documentationcenter: 
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-network
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: jdial
ms.custom: 
ms.openlocfilehash: cc7b9ad08d5c26dba09584762bedf614d2847032
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-classic-with-multiple-subnets"></a>Criar uma rede virtual (clássica) com várias sub-redes

> [!IMPORTANT]
> O Azure tem dois [modelos de implementação diferentes](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json) para criar e trabalhar com recursos: Resource Manager e clássico. Este artigo abrange utilizando o modelo de implementação clássica Olá. A Microsoft recomenda a criação de maioria das redes virtuais novo através do Olá [Resource Manager](virtual-networks-create-vnet-arm-pportal.md) modelo de implementação.

Neste tutorial, saiba como toocreate um básico do Azure (virtual network clássica) que tenha separar sub-redes públicas e privadas. Pode criar recursos do Azure, como máquinas virtuais e serviços em nuvem numa sub-rede. Recursos criados no redes virtuais (clássicas) podem comunicar entre si e com os recursos na outra rede virtual do redes tooa ligado.

Saiba mais sobre todos os [rede virtual](virtual-network-manage-network.md) e [sub-rede](virtual-network-manage-subnet.md) definições.

> [!WARNING]
> Redes virtuais (clássicas) são imediatamente eliminados pelo Azure quando um [a subscrição está desativada](../billing/billing-subscription-become-disable.md?toc=%2fazure%2fvirtual-network%2ftoc.json#you-reached-your-spending-limit). Redes virtuais (clássica) são eliminados independentemente se recursos existem na rede virtual Olá. Se mais tarde voltar a ativar a subscrição de Olá, os recursos que existiam na rede virtual Olá devem ser recriados.

Pode criar uma rede virtual (clássica) utilizando Olá [portal do Azure](#portal), Olá [interface de linha de comandos do Azure (CLI) 1.0](#azure-cli), ou [PowerShell](#powershell).

## <a name="portal"></a>Portal

1. Num browser da Internet, aceda toohello [portal do Azure](https://portal.azure.com). Inicie sessão com a sua [conta do Azure](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account). Se não tiver uma conta do Azure, pode inscrever-se para obter um [avaliação gratuita](https://azure.microsoft.com/offers/ms-azr-0044p).
2. Clique em **+ novo** no portal de Olá.
3. Introduza *rede Virtual* no Olá **Olá pesquisa Marketplace** caixa, Olá parte superior do Olá **novo** painel que aparece.  Clique em **rede Virtual** quando for apresentada nos resultados de pesquisa de Olá.
4. Selecione **clássico** no Olá **selecionar um modelo de implementação** caixa Olá **rede Virtual** painel apresentado, clique em **criar**. 
5. Introduza Olá os seguintes valores no Olá **criar rede virtual (clássica)** painel e clique em **criar**:

    |Definição|Valor|
    |---|---|
    |Nome|myVnet|
    |Espaço de endereços|10.0.0.0/16|
    |Nome da sub-rede|Público|
    |Intervalo de endereços da sub-rede|10.0.0.0/24|
    |Grupo de recursos|Deixe **criar nova** selecionada e, em seguida, introduza **myResourceGroup**.|
    |Subscrição e localização|Selecione a sua subscrição e localização.

    Se tiver tooAzure novo, saiba mais sobre [grupos de recursos](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#resource-group), [subscrições](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#subscription), e [localizações](https://azure.microsoft.com/regions) (também referida tooas *regiões*).
4. No portal de Olá, pode criar apenas uma sub-rede quando criar uma rede virtual. Neste tutorial, crie uma sub-rede do segundo depois de criar rede virtual Olá. Mais tarde poderá criar recursos acessível através da Internet no Olá **pública** sub-rede. Também poderá criar recursos que não estão acessíveis a partir do Olá Internet no Olá **privada** sub-rede. toocreate Olá segunda sub-rede, introduza **myVnet** no Olá **procurar recursos** caixa na Olá parte superior da página Olá. Clique em **myVnet** quando for apresentada nos resultados de pesquisa de Olá.
5. Clique em **sub-redes** (no Olá **definições** secção) no Olá **criar rede virtual (clássica)** painel que aparece.
6. Clique em **+ adicionar** no Olá **myVnet - sub-redes** painel que aparece.
7. Introduza **privada** para **nome** no Olá **adicionar sub-rede** painel. Introduza **10.0.1.0/24** para **intervalo de endereços**.  Clique em **OK**.
8. No Olá **myVnet - sub-redes** painel, pode ver Olá **pública** e **privada** sub-redes que criou.
9. **Opcional**: Quando concluir este tutorial, é aconselhável recursos de Olá toodelete que criou, para que não implicar custos de utilização:
    - Clique em **descrição geral** no Olá **myVnet** painel.
    - Clique em Olá **eliminar** ícone na Olá **myVnet** painel.
    - eliminação de Olá tooconfirm, clique em **Sim** no Olá **Delete de rede virtual** caixa.

## <a name="azure-cli"></a>CLI do Azure

1. Pode [instalar e configurar a CLI do Azure de Olá](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json), ou utilize Olá CLI dentro Olá Shell de nuvem do Azure. Olá Shell de nuvem do Azure é uma shell de deteção livre que podem ser executados diretamente no Olá portal do Azure. Tem Olá CLI do Azure pré-instalado e configurado toouse com a sua conta. tooget ajuda para comandos da CLI, escreva `azure <command> --help`. 
2. Numa sessão CLI, inicie sessão no tooAzure com o comando de Olá que se segue. Se clicar em **experimente** na caixa de Olá abaixo, uma Shell de nuvem abre. Pode iniciar sessão tooyour subscrição do Azure, sem introduzir Olá os seguintes comandos:

    ```azurecli-interactive
    azure login
    ```

3. Olá tooensure CLI está no modo de gestão de serviço, introduza Olá os seguintes comandos:

    ```azurecli-interactive
    azure config mode asm
    ```

4. Crie uma rede virtual com uma sub-rede privada:

    ```azurecli-interactive
    azure network vnet create --vnet myVnet --address-space 10.0.0.0 --cidr 16  --subnet-name Private --subnet-start-ip 10.0.0.0 --subnet-cidr 24 --location "East US"
    ```

5. Crie uma sub-rede pública dentro da rede virtual Olá:

    ```azurecli-interactive
    azure network vnet subnet create --name Public --vnet-name myVnet --address-prefix 10.0.1.0/24
    ```    
    
6. Reveja a rede virtual Olá e sub-redes:

    ```azurecli-interactive
    azure network vnet show --vnet myVnet
    ```

7. **Opcional**: É aconselhável a recursos de Olá toodelete que criou quando concluir este tutorial, pelo que não implicar custos de utilização:

    ```azurecli-interactive
    azure network vnet delete --vnet myVnet --quiet
    ```

> [!NOTE]
> Apesar de não é possível especificar um toocreate do grupo de recursos uma rede virtual (clássica) utilizando a CLI de Olá, Azure cria a rede virtual Olá num grupo de recursos com o nome *predefinido redes*.

## <a name="powershell"></a>PowerShell

1. Instale a versão mais recente do Olá do Olá PowerShell [Azure](https://www.powershellgallery.com/packages/Azure) módulo. Se estiver tooAzure nova do PowerShell, consulte [descrição geral do Azure PowerShell](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json).
2. Inicie uma sessão do PowerShell.
3. No PowerShell, inicie sessão no tooAzure introduzindo Olá `Add-AzureAccount` comando.
4. Alterar seguinte Olá caminho e nome de ficheiro, conforme adequado, em seguida, Exportar ficheiro de configuração de rede existente:

    ```powershell
    Get-AzureVNetConfig -ExportToFile c:\azure\NetworkConfig.xml
    ```

5. toocreate uma rede virtual com a sub-redes públicas e privadas, utilize qualquer Olá de tooadd do editor de texto **VirtualNetworkSite** elemento que se segue toohello ficheiro de configuração de rede.

    ```xml
    <VirtualNetworkSite name="myVnet" Location="East US">
        <AddressSpace>
          <AddressPrefix>10.0.0.0/16</AddressPrefix>
        </AddressSpace>
        <Subnets>
          <Subnet name="Private">
            <AddressPrefix>10.0.0.0/24</AddressPrefix>
          </Subnet>
          <Subnet name="Public">
            <AddressPrefix>10.0.1.0/24</AddressPrefix>
          </Subnet>
        </Subnets>
      </VirtualNetworkSite>
    ```

    Olá revisão completa [esquema do ficheiro de configuração de rede](https://msdn.microsoft.com/library/azure/jj157100.aspx).

6. Importe o ficheiro de configuração de rede Olá:

    ```powershell
    Set-AzureVNetConfig -ConfigurationPath c:\azure\NetworkConfig.xml
    ```

    > [!WARNING]
    > Importar um ficheiro de configuração foi alterada de rede pode fazer com que as alterações tooexisting redes virtuais (clássica) na sua subscrição. Certifique-se apenas a adicionar rede virtual anterior de Olá e que não alterar ou remover quaisquer redes virtuais existentes da sua subscrição. 

7. Reveja a rede virtual Olá e sub-redes:

    ```powershell
    Get-AzureVNetSite -VNetName "myVnet"
    ```

8. **Opcional**: É aconselhável a recursos de Olá toodelete que criou quando concluir este tutorial, pelo que não implicar custos de utilização. toodelete Olá rede virtual, concluir os passos 4 a 6 novamente, Olá de remover este tempo **VirtualNetworkSite** elemento adicionado no passo 5.
 
> [!NOTE]
> Apesar de não é possível especificar um toocreate do grupo de recursos uma rede virtual (clássica) utilizando o PowerShell, o Azure cria rede virtual Olá num grupo de recursos com o nome *predefinido redes*.

---

## <a name="next-steps"></a>Passos seguintes

- Consulte toolearn sobre todas as definições da sub-rede e a rede virtual [gerir redes virtuais](virtual-network-manage-network.md) e [gerir sub-redes da rede virtual](virtual-network-manage-subnet.md). Tem várias opções para utilizar redes virtuais e sub-redes um requisitos diferentes do ambiente toomeet de produção.
- toofilter entrada e saída tráfego de sub-rede, criar e aplicar [grupos de segurança de rede](virtual-networks-nsg.md) toosubnets.
- Criar um [Windows](../virtual-machines/windows/classic/createportal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) ou um [Linux](../virtual-machines/linux/classic/createportal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) máquina virtual e, em seguida, ligue-o tooan de rede virtual existente.
- redes virtuais tooconnect dois na mesma localização do Azure de Olá, crie um [peering de rede virtual](create-peering-different-deployment-models.md) entre redes virtuais Olá. Pode elemento uma rede virtual (Resource Manager) tooa (virtual network clássica), mas não é possível criar um peering entre duas redes virtuais (clássicas).
- Ligar a rede no local do Olá rede virtual tooan utilizando um [Gateway de VPN](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) ou [Azure ExpressRoute](../expressroute/expressroute-howto-linkvnet-portal-resource-manager.md?toc=%2fazure%2fvirtual-network%2ftoc.json) circuito.
