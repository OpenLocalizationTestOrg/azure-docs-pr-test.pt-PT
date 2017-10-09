---
title: "endereços IP aaaConfigure para uma interface de rede do Azure | Microsoft Docs"
description: "Saiba como tooadd, alterar e remova endereços IP públicos e privados para uma interface de rede."
services: virtual-network
documentationcenter: na
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
ms.date: 07/24/2017
ms.author: jdial
ms.openlocfilehash: 1e5ea6c65d93be9b1fda5d807500a0823c94c89c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="add-change-or-remove-ip-addresses-for-an-azure-network-interface"></a>Adicionar, alterar ou remover os endereços IP para uma interface de rede do Azure

Saiba como tooadd, alterar e remova endereços IP públicos e privados para uma interface de rede. Endereços de IP privado atribuídos a interface de rede tooa ativar toocommunicate uma máquina virtual com outros recursos numa Azure virtual network e redes ligadas. Um endereço IP privado também permite a comunicação de saída toohello Internet utilizando um endereço IP imprevisível. A [endereço IP público](virtual-network-public-ip-address.md) atribuído tooa interface de rede permite que a máquina virtual de tooa de comunicação de entrada de Olá Internet. endereço de Olá também permite a comunicação de saída da máquina virtual de Olá toohello Internet utilizando um endereço IP previsível. Para obter mais informações, consulte [Noções sobre ligações de saída no Azure](../load-balancer/load-balancer-outbound-connections.md?toc=%2fazure%2fvirtual-network%2ftoc.json). 

Se precisar de toocreate, alterar ou eliminar uma interface de rede, leia Olá [gerir uma interface de rede](virtual-network-network-interface.md) artigo. Se precisar de interfaces de rede tooadd tooor remover interfaces de rede de uma máquina virtual, leia Olá [interfaces de rede de adicionar ou remover](virtual-network-network-interface-vm.md) artigo. 


## <a name="before-you-begin"></a>Antes de começar

Conclua Olá seguintes tarefas antes de concluir os passos em qualquer secção deste artigo:

- Olá revisão [Azure limita](../azure-subscription-service-limits.md?toc=%2fazure%2fvirtual-network%2ftoc.json#azure-resource-manager-virtual-networking-limits) toolearn artigo sobre os limites de endereços IP públicos e privados.
- Inicie sessão no toohello Azure [portal](https://portal.azure.com), interface de linha de comandos (CLI) do Azure ou o Azure PowerShell com uma conta do Azure. Se ainda não tiver uma conta do Azure, inscreva-se um [conta de avaliação gratuita](https://azure.microsoft.com/free).
- Se utilizar o PowerShell comandos toocomplete tarefas neste artigo, [instalar e configurar o Azure PowerShell](/powershell/azureps-cmdlets-docs?toc=%2fazure%2fvirtual-network%2ftoc.json). Certifique-se de que tem a versão mais recente do Olá dos mini-comandos de Azure PowerShell Olá instalados. tooget ajuda para comandos do PowerShell, com exemplos, digite `get-help <command> -full`.
- Se utilizar a interface de linha de comandos do Azure (CLI) comandos toocomplete tarefas neste artigo, [instalar e configurar a CLI do Azure de Olá](/cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json). Certifique-se de que tem a versão mais recente do Olá de Olá CLI do Azure instalados. tooget ajuda para comandos da CLI, escreva `az <command> --help`. Em vez de instalar Olá CLI e respetivos pré-requisitos, pode utilizar Olá Shell de nuvem do Azure. Olá Shell de nuvem do Azure é uma shell de deteção livre que podem ser executados diretamente no Olá portal do Azure. Tem Olá CLI do Azure pré-instalado e configurado toouse com a sua conta. Olá toouse Shell de nuvem, clique em Olá nuvem Shell **> _** botão, Olá parte superior do Olá [portal](https://portal.azure.com).

## <a name="add-ip-addresses"></a>Adicionar endereços IP

Pode adicionar como muitas [privada](#private) e [pública](#public) [IPv4](#ipv4) endereços como a interface de rede necessário tooa, dentro dos limites de Olá listado no Olá [limites do Azure ](../azure-subscription-service-limits.md?toc=%2fazure%2fvirtual-network%2ftoc.json#azure-resource-manager-virtual-networking-limits) artigo. Não é possível utilizar Olá portal tooadd uma interface de rede existente do IPv6 endereço tooan (embora, pode utilizar Olá portal tooadd uma interface de rede do tooa de endereço IPv6 privada ao criar a interface de rede Olá). Pode utilizar o PowerShell ou Olá CLI tooadd um IPv6 privada endereço tooone [configuração de IP secundária](#secondary) (desde que não existem nenhum configurações de IP secundárias existentes), para uma rede existente, interface que não é ligado tooa virtual máquina. Não é possível utilizar qualquer tooadd ferramenta uma interface de rede do tooa de endereço IPv6 pública. Consulte [IPv6](#ipv6) para obter detalhes sobre a utilização de endereços IPv6. 

1. Inicie sessão no toohello [portal do Azure](https://portal.azure.com) com uma conta que seja atribuídas (no mínimo) permissões para a função de contribuinte de rede Olá para a sua subscrição. Olá leitura [funções incorporadas para controlo de acesso baseado em funções do Azure](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) artigo toolearn mais informações sobre a atribuição de funções e permissões tooaccounts.
2. Na caixa de Olá que contém texto Olá *procurar recursos* Olá parte superior do portal do Azure de Olá, escreva *interfaces de rede*. Quando **interfaces de rede** é apresentado nos resultados de pesquisa de Olá, clique no mesmo.
3. No Olá **interfaces de rede** painel apresentado, clique em que pretende que o endereço IPv4 de tooadd para interface de rede de Olá.
4. Clique em **configurações de IP** no Olá **definições** secção do painel de Olá Olá interface de rede que selecionou.
5. Clique em **+ adicionar** no Olá painel que abre as configurações de IP.
6. Especifique Olá seguinte, em seguida, clique em **OK** tooclose Olá **configuração de IP adicionar** painel:

    |Definição|Necessário?|Detalhes|
    |---|---|---|
    |Nome|Sim|Tem de ser exclusivo Olá interface de rede|
    |Tipo|Sim|Uma vez que estiver a adicionar uma interface de rede existente do IP configuração tooan e cada interface de rede tem de ter um [primário](#primary) é a única opção de configuração de IP, **secundário**.|
    |Método de atribuição de endereço IP privado|Sim|[**Dinâmica** ](#dynamic) endereços podem alterar se a máquina virtual de Olá é reiniciada depois de ter sido Olá parada (desalocado) de estado. Azure atribui um endereço disponível do espaço de endereços de Olá Olá sub-rede Olá da interface de rede está ligado a. [**Estático** ](#static) endereços não são lançados até que a interface de rede Olá é eliminado. Especifique um endereço IP do intervalo espaço de endereços de sub-rede de Olá que não está atualmente a ser utilizada por outra configuração de IP.|
    |Endereço IP público|Não|**Desativado:** nenhum recurso de endereço IP público é uma configuração de IP toohello atualmente associados. **Ativado:** selecione um endereço IPv4 de IP público existente ou crie um novo. toolearn como ler toocreate um endereço IP público, Olá [endereços IP públicos](virtual-network-public-ip-address.md#create-a-public-ip-address) artigo.|
7. Adicionar manualmente secundário privado IP endereços toohello sistema operativo máquina virtual, concluindo instruções Olá Olá [atribuir vários endereços IP de sistemas de operativos toovirtual máquina](virtual-network-multiple-ip-addresses-portal.md#os-config) artigo. Consulte [privada](#private) endereços IP para considerações especiais antes de adicionar manualmente o sistema de operativo da máquina virtual de tooa a endereços IP. Não adicione quaisquer público IP endereços toohello sistema operativo máquina virtual.

**Comandos**

|Ferramenta|Comando|
|---|---|
|CLI|[Criar nic de rede AZ ip-config](/cli/azure/network/nic/ip-config?toc=%2fazure%2fvirtual-network%2ftoc.json#create)|
|PowerShell|[AzureRmNetworkInterfaceIpConfig adicionar](/powershell/module/azurerm.network/add-azurermnetworkinterfaceipconfig?toc=%2fazure%2fvirtual-network%2ftoc.json)|

## <a name="change-ip-address-settings"></a>Alterar definições do endereço IP

Poderá ter o método de atribuição de Olá toochange de um endereço IPv4, alteração Olá endereço IPv4 estático, ou endereço IP público Olá alteração atribuídos tooa interface de rede. Se estiver a alterar o endereço IPv4 privado Olá de uma configuração de IP secundária associada uma interface de rede secundárias numa máquina virtual (Saiba mais sobre [interfaces de rede principal e secundário](virtual-network-network-interface-vm.md#about)), Olá local virtual máquina em Olá parada (desalocado) de estado antes de concluir Olá os seguintes passos: 

1. Inicie sessão no toohello [portal do Azure](https://portal.azure.com) com uma conta que seja atribuídas (no mínimo) permissões para a função de contribuinte de rede Olá para a sua subscrição. Olá leitura [funções incorporadas para controlo de acesso baseado em funções do Azure](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) artigo toolearn mais informações sobre a atribuição de funções e permissões tooaccounts.
2. Na caixa de Olá que contém texto Olá *procurar recursos* Olá parte superior do portal do Azure de Olá, escreva *interfaces de rede*. Quando **interfaces de rede** é apresentado nos resultados de pesquisa de Olá, clique no mesmo.
3. No Olá **interfaces de rede** painel apresentado, clique em interface de rede Olá pretende tooview ou alterar as definições de endereço IP para.
4. Clique em **configurações de IP** no Olá **definições** secção do painel de Olá Olá interface de rede que selecionou.
5. Clique em configuração de IP Olá que pretende toomodify na lista de Olá na Olá painel que abre as configurações de IP.
6. Alterar definições do Olá, conforme pretendido, utilizando Olá obter informações sobre definições de Olá no passo 6 do Olá [adicionar uma configuração de IP](#create-ip-config) secção deste artigo. Clique em **guardar** painel de Olá tooclose para a configuração de IP Olá é alterado.

>[!NOTE]
>Se a interface de rede primária Olá tem várias configurações de IP e altere o endereço IP privado Olá Olá principal da configuração de IP, tem de reatribuir manualmente Olá primária e secundária IP endereços toohello interface de rede no Windows (não necessário para Linux). interface de rede do IP endereços tooa dentro de um sistema operativo, de atribuir toomanually ler Olá [atribuir vários endereços IP toovirtual máquinas](virtual-network-multiple-ip-addresses-portal.md#os-config) artigo. Consulte [privada](#private) endereços IP para considerações especiais antes de adicionar manualmente o sistema de operativo da máquina virtual de tooa a endereços IP. Não adicione quaisquer público IP endereços toohello sistema operativo máquina virtual.

**Comandos**

|Ferramenta|Comando|
|---|---|
|CLI|[atualização de configuração de ip da nic de rede de AZ](/cli/azure/network/nic/ip-config?toc=%2fazure%2fvirtual-network%2ftoc.json#update)|
|PowerShell|[Conjunto AzureRMNetworkInterfaceIpConfig](/powershell/module/azurerm.network/set-azurermnetworkinterfaceipconfig?toc=%2fazure%2fvirtual-network%2ftoc.json)|

## <a name="remove-ip-addresses"></a>Remova endereços IP

Pode remover [privada](#private) e [pública](#public) endereços IP da interface de rede, mas uma interface de rede tem sempre de ter pelo menos um tooit de endereço atribuído IPv4 privado.

1. Inicie sessão no toohello [portal do Azure](https://portal.azure.com) com uma conta que seja atribuídas (no mínimo) permissões para a função de contribuinte de rede Olá para a sua subscrição. Olá leitura [funções incorporadas para controlo de acesso baseado em funções do Azure](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) artigo toolearn mais informações sobre a atribuição de funções e permissões tooaccounts.
2. Na caixa de Olá que contém texto Olá *procurar recursos* Olá parte superior do portal do Azure de Olá, escreva *interfaces de rede*. Quando **interfaces de rede** é apresentado nos resultados de pesquisa de Olá, clique no mesmo.
3. No Olá **interfaces de rede** painel apresentado, clique em que pretende tooremove endereços IP da interface de rede de Olá.
4. Clique em **configurações de IP** no Olá **definições** secção do painel de Olá Olá interface de rede que selecionou.
5. Com o botão direito um [secundário](#secondary) configuração de IP (não é possível eliminar Olá [primário](#primary) configuração) pretende toodelete, clique em **eliminar**, em seguida, clique em **Sim**  eliminação de Olá tooconfirm. Se a configuração de Olá possui tooit associados a um recurso de endereço IP público, recurso Olá é desassociado da configuração de IP Olá, mas recursos Olá não é eliminado.
6. Fechar Olá **configurações de IP** painel.

**Comandos**

|Ferramenta|Comando|
|---|---|
|CLI|[eliminação de configuração de ip do AZ rede nic](/cli/azure/network/nic/ip-config?toc=%2fazure%2fvirtual-network%2ftoc.json#delete)|
|PowerShell|[Remover AzureRmNetworkInterfaceIpConfig](/powershell/module/azurerm.network/remove-azurermnetworkinterfaceipconfig?toc=%2fazure%2fvirtual-network%2ftoc.json)|

## <a name="ip-configurations"></a>Configurações de IP

[Privada](#private) e (opcionalmente) [pública](#public) endereços IP são atribuídos tooone ou mais configurações de IP atribuídos tooa interface de rede. Existem dois tipos de configurações de IP:

### <a name="primary"></a>Primária

Cada interface de rede é atribuído uma configuração de IP primária. Uma configuração de IP primária:

- Tem um [privada](#private) [IPv4](#ipv4) tooit endereço atribuído. Não é possível atribuir uma privada [IPv6](#ipv6) configuração de IP primária tooa endereço.
- Também pode ter um [pública](#public) tooit de endereço atribuído IPv4. Não é possível atribuir uma pública tooa primária ou secundária IP configuração de endereços IPv6. Pode, contudo, atribuir um IPv6 pública endereço de Balanceador de carga do Azure de tooan, pode carregar equilibrar o endereço de IPv6 privado tráfego tooa virtual da máquina. Para obter mais informações, consulte [detalhes e limitações do IPv6](../load-balancer/load-balancer-ipv6-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json#details-and-limitations).

### <a name="secondary"></a>Secundária

Além disso tooa a configuração de IP primária, uma interface de rede pode ter zero ou mais secundárias configurações de IP atribuídas tooit. Uma configuração de IP secundária:

- Tem de ter um tooit de endereço atribuído privada IPv4 ou IPv6. Se o endereço de Olá for IPv6, a interface de rede Olá só pode ter uma configuração de IP secundária. Se o endereço de Olá for IPv4, o interface de rede Olá pode ter várias configurações de IP secundárias atribuídas tooit. toolearn mais informações sobre quantas endereços de IPv4 privados e públicos podem ser atribuídos a interface de rede tooa, consulte Olá [Azure limita](../azure-subscription-service-limits.md?toc=%2fazure%2fvirtual-network%2ftoc.json#azure-resource-manager-virtual-networking-limits) artigo.  
- Também poderá ter um tooit atribuído de endereço IPv4 público, se o endereço IP privado Olá IPv4. Se o endereço IP privado Olá IPv6, não é possível atribuir um pública IPv4 ou IPv6 endereço toohello configuração de IP. Atribuir vários interface de rede do tooa endereços IP é útil em cenários tais como:
    - Alojar vários Web Sites ou serviços com diferentes endereços IP e certificados SSL num único servidor.
    - Uma máquina virtual que servem como uma aplicação virtual de rede, tais como uma firewall ou Balanceador de carga.
    - Olá capacidade tooadd qualquer um dos Olá endereços IPv4 privado para qualquer conjunto de tooan back-end de Balanceador de carga do Azure de interfaces de rede Olá. No passado, Olá, apenas Olá primário endereço IPv4 de interface de rede primária Olá foi possível adicionar o conjunto de back-end tooa. toolearn mais informações sobre como tooload equilibrar configurações com várias IPv4, consulte Olá [várias configurações de IP de balanceamento de carga](../load-balancer/load-balancer-multiple-ip.md?toc=%2fazure%2fvirtual-network%2ftoc.json) artigo. 
    - Olá capacidade tooload saldo uma IPv6 endereço atribuído tooa interface de rede. toolearn mais informações sobre como tooload equilibrar tooa privado endereço de IPv6, consulte Olá [equilibrar os endereços IPv6](../load-balancer/load-balancer-ipv6-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json) artigo.


## <a name="address-types"></a>Tipos de endereço

Pode atribuir Olá os seguintes tipos de tooan de endereços IP [configuração de IP](#ip-configurations):

### <a name="private"></a>Privado

Privada [IPv4](#ipv4) endereços ativar toocommunicate uma máquina virtual com outros recursos numa rede virtual ou outras redes ligadas. Uma máquina virtual não é possível comunicar entrada para, nem pode a máquina virtual de Olá comunicar saída com privado [IPv6](#ipv6) endereço, com uma exceção. Uma máquina virtual podem comunicar com o Balanceador de carga do Azure de Olá utilizando um endereço IPv6. Para obter mais informações, consulte [detalhes e limitações do IPv6](../load-balancer/load-balancer-ipv6-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json#details-and-limitations). 

Por predefinição, os servidores de DHCP do Azure de Olá atribuir endereço IPv4 privado Olá para Olá [configuração de IP primária](#primary) Olá interface toohello rede da interface de rede no sistema de operativo Olá máquina virtual. Se necessário, manualmente nunca deverá definir endereço IP Olá de uma interface de rede dentro do sistema operativo da máquina virtual Olá. 

> [!WARNING]
> Se o endereço de IPv4 Olá definido como Olá endereço IP primário de uma interface de rede no sistema de operativo de uma máquina virtual é alguma vez diferente de endereço IPv4 privado Olá atribuído toohello configuração de IP primária Olá primário da interface de rede ligado tooa máquina virtual no Azure, perderá conectividade toohello máquina.

Existem cenários onde é necessário toomanually conjunto Olá endereço IP de uma interface de rede dentro do sistema operativo da máquina virtual Olá. Por exemplo, tem de definir manualmente Olá primários e secundários endereços IP de um sistema operativo Windows quando adicionar vários tooan de endereços IP máquina virtual do Azure. Para uma máquina virtual do Linux, só poderá ser necessário endereços IP toomanually conjunto Olá secundários. Consulte [IP adicionar endereços de sistema de operativo tooa VM](virtual-network-multiple-ip-addresses-portal.md#os-config) para obter mais detalhes. Quando definir o endereço IP Olá no sistema de operativo Olá manualmente, é recomendado que atribua sempre Olá endereços toohello configuração de IP utilizando o método de atribuição de estático (em vez de dinâmico) Olá uma interface de rede. Atribuir o endereço de Olá utilizando o método estático Olá assegura que o endereço Olá não é alterado no Azure. Se alguma vez precisar de endereço de Olá toochange atribuído a configuração de IP tooan, é recomendado que tem:

1. tooensure Olá máquina está a receber um endereço de servidores de DHCP do Azure de Olá, altere a atribuição de Olá de Olá IP endereços back-tooDHCP dentro do sistema de operativo Olá e reinício Olá máquina.
2. Parar (desalocar) Olá máquina.
3. Alterar o endereço IP Olá para a configuração de IP Olá no Azure.
4. Inicie máquina virtual de Olá.
5. [Configurar manualmente](virtual-network-multiple-ip-addresses-portal.md#os-config) Olá toomatch de endereços num sistema de operativo Olá (e também Olá endereço IP primário no Windows) de IP secundária definida no Azure.
 
Ao seguir os passos anteriores Olá, Olá privada IP endereço atribuído toohello interface de rede no Azure e no sistema de operativo de uma máquina virtual, permanecem Olá mesmo. controlar tookeep que as máquinas virtuais na sua subscrição que definiu manualmente endereços IP dentro de um sistema operativo, considere adicionar um Azure [tag](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json#tags) toohello máquinas de virtuais. Poderá utilizar "atribuição de endereços IP: estático", por exemplo. Desta forma, pode localizar facilmente máquinas de virtuais Olá na sua subscrição que definiu manualmente Olá do endereço IP no sistema de operativo Olá.

Além disso tooenabling toocommunicate uma máquina virtual com outros recursos no Olá mesmos, ou ligados redes virtuais, um IP privado de endereços também permite Internet uma máquina virtual toocommunicate saída toohello. Ligações de saída são endereço de rede de origem traduzido por endereço IP de público imprevisível de tooan do Azure. mais acerca do Azure à saída de Internet, leia Olá toolearn [conectividade de Internet de saída do Azure](../load-balancer/load-balancer-outbound-connections.md?toc=%2fazure%2fvirtual-network%2ftoc.json) artigo. Não é possível comunicar o endereço IP privado da máquina virtual tooa entrada de Olá Internet.

### <a name="public"></a>Público

Endereços IP públicos permitem a máquina virtual a conectividade de entrada tooa partir Olá Internet. Ligações de saída toohello Internet utilizar um endereço IP previsível. Consulte [Noções sobre ligações de saída no Azure](../load-balancer/load-balancer-outbound-connections.md?toc=%2fazure%2fvirtual-network%2ftoc.json) para obter mais detalhes. Pode atribuir uma configuração de IP do tooan de endereço IP pública, mas não são necessários para. Se não atribuir uma máquina de virtual do tooa de endereço IP pública, ainda consegue comunicar toohello saída Internet com o respetivo endereço IP privado. mais informações sobre os endereços IP públicos, leia Olá toolearn [endereço IP público](virtual-network-public-ip-address.md) artigo.

Existem limites toohello diversas privada e interface de rede de endereços IP públicos que pode atribuir tooa. Para obter mais informações, leia o artigo Olá [Azure limita](../azure-subscription-service-limits.md?toc=%2fazure%2fvirtual-network%2ftoc.json#azure-resource-manager-virtual-networking-limits) artigo.

> [!NOTE]
> Azure traduz-se privado IP endereço tooa endereço IP público uma máquina virtual. Como resultado, o sistema de operativo Olá não tem conhecimento do quaisquer endereços IP públicos atribuídos tooit, pelo que não existe nenhum tooever necessidade manualmente atribuir um endereço IP público no sistema de operativo Olá.

## <a name="assignment-methods"></a>Métodos de atribuição

Endereços IP públicos e privados atribuídos, utilizando os seguintes métodos de atribuição de Olá:

### <a name="dynamic"></a>Dinâmica

IPv4 privada dinâmico e IPv6 (opcionalmente) endereços são atribuídos por predefinição. Endereços dinâmicos podem alterar se a máquina virtual de Olá é colocada em Olá parada (desalocado) de estado, em seguida, iniciado. Se não quiser toochange de endereços IPv4 para vida Olá da máquina virtual de Olá, atribua os endereços de Olá utilizando o método estático Olá. Só é possível atribuir um endereço IPv6 privado utilizando o método de atribuição dinâmica Olá. Não é possível atribuir uma pública tooan IP configuração de endereços IPv6 utilizando um dos métodos.

### <a name="static"></a>Estático

Endereços atribuídos utilizando o método estático Olá não alterar até que uma máquina virtual é eliminada. Atribuir manualmente uma privada IPv4 endereço tooan configuração de IP estático do espaço de endereços de Olá para a interface de rede do Olá sub-rede Olá está em. (Opcionalmente), pode atribuir uma pública ou privada IPv4 endereço tooan configuração de IP estático. Não é possível atribuir uma pública ou privada IPv6 endereço tooan configuração de IP estático. toolearn mais informações sobre como o Azure atribui os endereços IPv4 públicos estáticos, consulte Olá [endereço IP público](virtual-network-public-ip-address.md) artigo.

## <a name="ip-address-versions"></a>Versões de endereços IP

Pode especificar Olá seguintes versões ao atribuir endereços:

### <a name="ipv4"></a>IPv4

Cada interface de rede tem de ter um [primário](#primary) configuração de IP com um atribuído [privada](#private) [IPv4](#ipv4) endereço. Pode adicionar um ou mais [secundário](#secondary) configurações de IP com IPv4 privado e (opcionalmente) IPv4 [pública](#public) endereço IP.

### <a name="ipv6"></a>IPv6

Pode atribuir privada zero ou um [IPv6](#ipv6) endereço tooone secundária configuração do IP de uma interface de rede. interface de rede Olá não pode ter quaisquer configurações de IP secundárias existentes. Não é possível adicionar uma configuração de IP com um endereço IPv6 através do portal Olá. Utilize o PowerShell ou Olá CLI tooadd uma configuração de IP com uma privada IPv6 endereço tooan existente interface de rede. interface de rede Olá não pode ser anexado tooan existente VM.

> [!NOTE]
> Apesar de poder criar uma interface de rede com um endereço IPv6 através do portal Olá, não é possível adicionar uma rede interface tooa novo ou existente máquina virtual existente, através do portal Olá. Utilizar o PowerShell ou Olá Azure CLI 2.0 toocreate uma interface de rede com um endereço IPv6 privado, em seguida, anexar a interface de rede de Olá quando criar uma máquina virtual. Não é possível anexar uma interface de rede com um endereço IPv6 privado atribuído tooit tooan existente a máquina virtual. Não é possível adicionar uma privada IPv6 endereço tooan configuração de IP para qualquer máquina virtual de rede interface ligado tooa utilizar quaisquer ferramentas (portal, CLI ou PowerShell).

Não é possível atribuir uma pública tooa primária ou secundária IP configuração de endereços IPv6.

## <a name="next-steps"></a>Passos seguintes
toocreate uma máquina virtual com diferentes configurações de IP, leia Olá seguintes artigos:

|Tarefa|Ferramenta|
|---|---|
|Criar uma VM com vários NICs|[CLI](../virtual-machines/linux/multiple-nics.md?toc=%2fazure%2fvirtual-network%2ftoc.json), [PowerShell](../virtual-machines/windows/multiple-nics.md?toc=%2fazure%2fvirtual-network%2ftoc.json)|
|Criar uma VM de NIC único com vários endereços de IPv4|[CLI](virtual-network-multiple-ip-addresses-cli.md), [PowerShell](virtual-network-multiple-ip-addresses-powershell.md)|
|Criar uma VM de NIC único com um endereço IPv6 privado (atrás de um balanceador de carga do Azure)|[CLI](../load-balancer/load-balancer-ipv6-internet-cli.md?toc=%2fazure%2fvirtual-network%2ftoc.json), [PowerShell](../load-balancer/load-balancer-ipv6-internet-ps.md?toc=%2fazure%2fvirtual-network%2ftoc.json), [modelo Azure Resource Manager](../load-balancer/load-balancer-ipv6-internet-template.md?toc=%2fazure%2fvirtual-network%2ftoc.json)|
