---
title: aaaCreate, alterar ou eliminar uma Azure virtual network | Microsoft Docs
description: Saiba como toocreate, alterar ou eliminar uma rede virtual no Azure.
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
ms.openlocfilehash: 7dfe6632753182eae2a13bb0327f03f75e03d057
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-change-or-delete-a-virtual-network"></a>Criar, alterar ou eliminar uma rede virtual

Saiba como toocreate e eliminar definições e alteração de rede virtual, como servidores DNS e endereço IP espaços, para uma rede virtual existente.

Uma rede virtual é uma representação da sua própria rede na nuvem de Olá. Uma rede virtual é um isolamento lógico da Olá em nuvem do Azure que está dedicado tooyour subscrição do Azure. Para cada rede virtual que criou, pode:
- Escolha um tooassign de espaço de endereço. Um espaço de endereços é composta por um ou mais intervalos de endereços que são definidos utilizando a notação de Classless entre domínios encaminhamento CIDR (), como 10.0.0.0/16.
- Escolher o servidor DNS fornecidos pelo Azure toouse Olá ou utilize o seu próprio servidor DNS. Todos os recursos que estão a rede virtual ligado toohello são atribuídos este nomes de tooresolve de servidor DNS na rede virtual Olá.
- Segmento Olá rede virtual em sub-redes, cada um com o seu próprio intervalo de endereços, dentro do espaço de endereço Olá da rede virtual Olá. toolearn como toocreate, alteração e eliminação sub-redes, consulte o artigo [adicionar, alterar ou eliminar sub-redes](virtual-network-manage-subnet.md).

Este artigo explica como toocreate, alterar e eliminar redes virtuais utilizando o modelo de implementação Azure Resource Manager Olá.

## <a name="before"></a>Antes de começar

Antes de iniciar tarefas de Olá que são descritas neste artigo, conclua Olá os seguintes pré-requisitos:

- Se a nova tooworking com redes virtuais, recomendamos que reveja Olá exercício no [criar a sua primeira rede virtual do Azure](virtual-network-get-started-vnet-subnet.md). Neste exercício pode ajudar a tornar-se mais familiar com redes virtuais.
- toolearn sobre os limites de redes virtuais, reveja [limites do Azure](../azure-subscription-service-limits.md?toc=%2fazure%2fvirtual-network%2ftoc.json#azure-resource-manager-virtual-networking-limits).
- Inicie sessão no portal do Azure de toohello, Olá ferramenta da linha de comandos do Azure (CLI do Azure) ou o Azure PowerShell, utilizando a sua conta do Azure. Se não tiver uma conta do Azure, inscreva-se um [conta de avaliação gratuita](https://azure.microsoft.com/free).
- Se planear toouse PowerShell comandos tarefas de Olá toocomplete descritas neste artigo, deve primeiro [instalar e configurar o Azure PowerShell](/powershell/azureps-cmdlets-docs?toc=%2fazure%2fvirtual-network%2ftoc.json). Certifique-se de que tem a versão mais recente do Olá de Olá cmdlets Azure PowerShell instalados. Introduza tooget ajuda para comandos do PowerShell nos exemplos de Olá, `get-help <command> -full`.
- Se planear toouse CLI do Azure comandos tarefas de Olá toocomplete descritas neste artigo, deve primeiro [instalar e configurar a CLI do Azure](/cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json). Certifique-se de que tem a versão mais recente do Olá da CLI do Azure instalados. ajuda para tooget comandos da CLI do Azure, introduza `az <command> --help`.


## <a name="create-vnet"></a>Criar uma rede virtual

toocreate uma rede virtual:

1. Inicie sessão no toohello [portal](https://portal.azure.com) com uma conta que está a atribuir permissões para a função de contribuinte de rede Olá (no mínimo) para a sua subscrição. toolearn mais informações sobre a atribuição de funções e permissões tooaccounts, consulte [funções incorporadas para controlo de acesso baseado em funções do Azure](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor).
2. Clique em **novo** > **redes** > **rede Virtual**.
3. No Olá **rede Virtual** painel, no Olá **selecionar um modelo de implementação** caixa, deixe **Resource Manager** selecionada e, em seguida, clique em **criar**.
4. No Olá **criar rede virtual** painel, introduza ou selecione os valores de Olá seguintes definições, em seguida, clique em **criar**:
    - **Nome**: Olá nome tem de ser exclusivo no Olá [grupo de recursos](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#resource-group) que selecione a rede virtual de Olá toocreate no. Não é possível alterar o nome de Olá depois da criação Olá de rede virtual. Pode criar várias redes virtuais ao longo do tempo. Para sugestões de atribuição de nomes, consulte [convenções de nomenclatura](/azure/architecture/best-practices/naming-conventions.md?toc=%2fazure%2fvirtual-network%2ftoc.json#naming-rules-and-restrictions). Seguir uma convenção de nomenclatura pode ajudar a torná-lo mais fácil toomanage várias redes virtuais.
    - **Espaço de endereços**: Especifique o espaço de endereços de Olá em notação CIDR. definir o espaço de endereços Olá pode ser public ou private (RFC 1918). Se definir o espaço de endereços de Olá como público ou privado, o espaço de endereços de Olá é acessível apenas a partir de dentro da rede virtual Olá, interligados redes virtuais e redes no local que ligou toohello de rede virtual. Não é possível adicionar Olá seguintes espaços de endereços:
        - 224.0.0.0/4 (Multicast)
        - 255.255.255.255/32 (difusão)
        - 127.0.0.0/8 (Loopback)
        - 169.254.0.0/16 (locais)
        - 168.63.129.16/32 (DNS interno)

      Embora, pode definir apenas um espaço de endereços quando criar rede virtual Olá, pode adicionar mais espaços de endereços depois da criação Olá de rede virtual. toolearn como tooadd um endereço espaço tooan rede virtual existente, consulte [adicionar ou remover um espaço de endereço](#add-address-spaces) neste artigo.

      >[!WARNING]
      >Se uma rede virtual tem espaços de endereços que se sobrepõe a outra rede no local ou de rede virtual, não não possível ligar a redes de Olá dois. Antes de definir um espaço de endereços, considere se é aconselhável redes virtuais do tooconnect Olá rede virtual tooother ou redes no local no Olá futuras.
      >
      >

    - **Nome da sub-rede**: nome de sub-rede Olá têm de ser exclusivo dentro da rede virtual Olá. Não é possível alterar o nome da sub-rede Olá depois Olá sub-rede é criada. portal de Olá necessita que define uma sub-rede quando cria uma rede virtual, apesar de uma rede virtual não é necessário toohave quaisquer sub-redes. No portal de Olá, pode definir apenas uma sub-rede quando criar uma rede virtual. Pode adicionar mais toohello sub-redes da rede do virtual mais tarde, depois da criação Olá de rede virtual. tooadd sub-rede tooa rede virtual, consulte [criar uma sub-rede](virtual-network-manage-subnet.md#create-subnet) no [criar, alterar ou eliminar sub-redes](virtual-network-manage-subnet.md). Pode criar uma rede virtual que tem várias sub-redes utilizando a CLI do Azure ou o PowerShell.

      >[!TIP]
      >Por vezes, administradores criar sub-redes diferentes toofilter ou controlo de tráfego de encaminhamento entre sub-redes de Olá. Antes de definir sub-redes, considere como poderá pretender toofilter e encaminhar tráfego entre as sub-redes. toolearn mais sobre a filtragem de tráfego entre sub-redes, consulte [grupos de segurança de rede](virtual-networks-nsg.md). Azure automaticamente tráfego de rotas entre sub-redes, mas pode substituir as rotas predefinidas do Azure. toolearn como toooverride Azure predefinido o encaminhamento de tráfego de sub-rede, consulte [rotas definidas pelo utilizador](virtual-networks-udr-overview.md).
      >

    - **Intervalo de endereços da sub-rede**: intervalo de Olá tem de estar no espaço de endereços de Olá que introduziu para a rede virtual Olá. o intervalo de menor Olá que pode especificar é /29, que fornece oito endereços IP para a sub-rede de Olá. As reservas de Azure Olá pela primeira vez e pela última vez em cada sub-rede para a conformidade de protocolo de endereços. Três endereços adicionais estão reservados para utilização do serviço do Azure. Como resultado, uma rede virtual com um intervalo de endereços de sub-rede de /29 tem três apenas endereços IP utilizáveis. Se planear tooconnect um gateway de VPN de tooa de rede virtual, terá de criar uma sub-rede de gateway. Saiba mais sobre [considerações de intervalo de endereço específico para sub-redes de gateway](../vpn-gateway/vpn-gateway-about-vpn-gateway-settings.md?toc=%2fazure%2fvirtual-network%2ftoc.json#gwsub). Pode alterar o intervalo de endereços de Olá depois de criar a sub-rede de Olá, sob condições específicas. toolearn como toochange um intervalo de endereços da sub-rede, consulte [alterar definições da sub-rede](#change-subnet) no [adicionar, alterar ou eliminar sub-redes](virtual-network-manage-subnet.md).
    - **Subscrição**: selecione uma [subscrição](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#subscription). Não é possível utilizar Olá mesma rede virtual em mais do que uma subscrição do Azure. No entanto, pode ligar uma rede virtual em redes de toovirtual subscrição um nas outras subscrições. tooconnect redes virtuais em diferentes subscrições, utilize o peering de rede virtual ou de Gateway de VPN do Azure. Qualquer recurso do Azure que se ligar a rede virtual toohello tem de constar Olá mesma subscrição que a rede virtual Olá.
    - **Grupo de recursos**: selecione um existente [grupo de recursos](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json#resource-groups) ou crie um novo. Um recurso do Azure que se ligar a rede virtual toohello pode estar em Olá mesmo grupo de recursos, como a rede virtual Olá ou num grupo de recursos diferentes.
    - **Localização**: selecione um Azure [localização](https://azure.microsoft.com/regions/), também conhecido como uma região. Uma rede virtual pode ter apenas uma localização do Azure. No entanto, pode ligar uma rede virtual numa localização tooa virtual rede noutra localização, utilizando um gateway de VPN. Qualquer recurso do Azure que se ligar a rede virtual toohello tem de constar Olá mesma localização da rede virtual Olá.

**Comandos**

|Ferramenta|Comando|
|---|---|
|CLI do Azure|[Criar AZ rede vnet](/cli/azure/network/vnet?toc=%2fazure%2fvirtual-network%2ftoc.json#create)|
|PowerShell|[Novo-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork?toc=%2fazure%2fvirtual-network%2ftoc.json)|

## <a name = "view-vnet"></a>Ver redes virtuais e definições

redes virtuais tooview e definições:

1. Inicie sessão no toohello [portal](https://portal.azure.com) com uma conta que está a atribuir permissões para a função de contribuinte de rede Olá (no mínimo) para a sua subscrição. toolearn mais informações sobre a atribuição de funções e permissões tooaccounts, consulte [funções incorporadas para controlo de acesso baseado em funções do Azure](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor).
2. Na caixa de pesquisa de portal Olá, introduza **redes virtuais**. Nos resultados de pesquisa de Olá, clique em **redes virtuais**.
3. No Olá **redes virtuais** painel, clique Olá rede virtual que pretende que as definições de tooview para.
4. Olá seguintes definições estão listadas no painel de Olá para a rede virtual Olá que selecionou:
    - **Descrição geral**: fornece informações sobre a rede virtual Olá, incluindo o espaço de endereços e servidores DNS. Olá seguinte captura de ecrã mostra as definições de descrição geral de Olá para uma rede virtual denominada **MyVNet**:

        ![Descrição geral da interface de rede](./media/virtual-network-manage-network/vnet-overview.png)

      No Olá **descrição geral** painel, pode mover um rede virtual tooa outro subscrição ou grupo de recursos. toolearn como toomove uma rede virtual, consulte [mover recursos tooa noutro grupo de recursos ou subscrição](../azure-resource-manager/resource-group-move-resources.md?toc=%2fazure%2fvirtual-network%2ftoc.json). artigo de Olá apresenta uma lista de pré-requisitos e como recursos toomove utilizando Olá portal do Azure, PowerShell e CLI do Azure. Tem de mover todos os recursos que estão ligados toohello rede virtual com a rede virtual Olá.
    - **Espaço de endereços**: espaços de endereços de Olá que estão atribuídos a rede virtual toohello estão listados. Olá, toolearn como tooadd e remover um espaço de endereços, conclua os passos no [adicionar ou remover um espaço de endereço](#address-spaces) neste artigo.
    - **Dispositivos ligados**: são listados todos os recursos que estão ligados toohello rede virtual. No Olá anterior a captura de ecrã, três interfaces de rede e um balanceador de carga são ligados toohello rede virtual. Quaisquer recursos novos que criar e ligar a rede virtual toohello estão listados. Se eliminar um recurso que foi ligado toohello rede virtual, já não aparece na lista de Olá.
    - **Sub-redes**: uma lista de sub-redes existentes na rede virtual Olá é apresentada. toolearn como tooadd e remover uma sub-rede, consulte [criar uma sub-rede](virtual-network-manage-subnet.md#create-subnet) e [eliminar uma sub-rede](virtual-network-manage-subnet.md#delete-subnet) no [adicionar, alterar ou eliminar sub-redes](virtual-network-manage-subnet.md).
    - **Servidores DNS**: pode especificar se hello servidor DNS interno do Azure ou um servidor DNS personalizado fornece resolução de nomes para dispositivos que estão ligados toohello rede virtual. Quando cria uma rede virtual, utilizando Olá portal do Azure, servidores DNS do Azure são utilizadas para a resolução do nome dentro de uma rede virtual, por predefinição. servidores DNS do toomodify Olá, Olá concluir os passos em [adicionar, alterar ou remover um servidor DNS](#dns-servers) neste artigo.
    - **Peerings**: se existirem peerings existente na subscrição Olá, estes são apresentados aqui. Pode ver as definições para peerings existente, ou criar, alterar ou eliminar peerings. toolearn mais informações sobre peerings, consulte [peering de rede Virtual](virtual-network-peering-overview.md).
    - **Propriedades**: definições de apresenta sobre Olá rede virtual, incluindo o ID de recurso da rede virtual Olá e Olá subscrição do Azure está a ser.
    - **Diagrama**: diagrama Olá fornece uma representação visual de todos os dispositivos que estão ligados toohello rede virtual. Diagrama de Olá tem algumas informações chaves sobre os dispositivos de Olá. toomanage um dispositivo nesta vista, no diagrama de Olá, clique em dispositivo Olá.
    - **Definições comuns de Azure**: toolearn mais informações sobre as definições do Azure comuns, consulte Olá seguintes informações:
        *   [Registo de atividades](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json#activity-logs)
        *   [Controlo de acesso (IAM)](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json#access-control)
        *   [Etiquetas](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json#tags)
        *   [Bloqueia](../azure-resource-manager/resource-group-lock-resources.md?toc=%2fazure%2fvirtual-network%2ftoc.json)
        *   [Script de automatização](../azure-resource-manager/resource-manager-export-template.md?toc=%2fazure%2fvirtual-network%2ftoc.json#export-the-template-from-resource-group)

**Comandos**

|Ferramenta|Comando|
|---|---|
|CLI do Azure|[Mostrar de vnet AZ rede](/cli/azure/network/vnet?toc=%2fazure%2fvirtual-network%2ftoc.json#show)|
|PowerShell|[Get-AzureRmVirtualNetwork](/powershell/module/azurerm.network/get-azurermvirtualnetwork/?toc=%2fazure%2fvirtual-network%2ftoc.json)|


## <a name="add-address-spaces"></a>Adicionar ou remover um espaço de endereço

Pode adicionar e remover espaços de endereços de rede virtual. Um espaço de endereços tem de ser especificado em notação CIDR e não se podem sobrepor com outros espaços de endereços dentro Olá mesma rede virtual. espaços de endereços de Olá que definir podem ser public ou private (RFC 1918). Se definir o espaço de endereços de Olá como público ou privado, o espaço de endereços de Olá é acessível apenas a partir de dentro da rede virtual Olá, interligados redes virtuais e redes no local que ligou toohello de rede virtual. Não é possível adicionar Olá seguintes espaços de endereços:

- 224.0.0.0/4 (Multicast)
- 255.255.255.255/32 (difusão)
- 127.0.0.0/8 (Loopback)
- 169.254.0.0/16 (locais)
- 168.63.129.16/32 (DNS interno)

tooadd ou remover um espaço de endereço:

1. Inicie sessão no toohello [portal](https://portal.azure.com) com uma conta que está a atribuir permissões para a função de contribuinte de rede Olá (no mínimo) para a sua subscrição. toolearn mais informações sobre a atribuição de funções e permissões tooaccounts, consulte [funções incorporadas para controlo de acesso baseado em funções do Azure](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor).
2. Na caixa de pesquisa de portal Olá, introduza **redes virtuais**. Nos resultados de pesquisa de Olá, selecione **redes virtuais**.
3. No Olá **redes virtuais** painel, clique Olá rede virtual para o qual pretende tooadd ou remover um espaço de endereços.
4. No Olá virtual de rede painel, em **definições**, clique em **espaço de endereços**.
5. No painel Olá espaço de endereços de Olá, execute um dos Olá seguintes opções:
    - **Adicionar um espaço de endereço**: introduza o espaço de endereços novo Olá. espaço de endereços de Olá não pode sobrepor-se com um espaço de endereço existente que está definido para a rede virtual Olá.
    - **Remover um espaço de endereço**: faça duplo clique um espaço de endereços e, em seguida, clique em **remover**. Se existir uma sub-rede no espaço de endereços de Olá, não é possível remover o espaço de endereços de Olá. tooremove um espaço de endereços, tem primeiro de eliminar quaisquer sub-redes (e quaisquer recursos que estão ligados toohello sub-redes) que existe no espaço de endereços de Olá.
6. Clique em **Guardar**.

**Comandos**

|Ferramenta|Comando|
|---|---|
|CLI do Azure|Apenas o Gestor de recursos|[atualização do AZ rede vnet](/cli/azure/network/vnet?toc=%2fazure%2fvirtual-network%2ftoc.json#update)|
|PowerShell|[Set-AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork?toc=%2fazure%2fvirtual-network%2ftoc.json)|

## <a name="dns-servers"></a>Adicionar, alterar ou remover um servidor DNS

Registar todas as VMs que estão ligados toohello rede virtual com os servidores DNS Olá que especificar para a rede virtual Olá. Também utilizam Olá especificado servidor DNS para resolução de nomes. Cada interface de rede (NIC) numa VM pode ter as suas próprias definições de servidor DNS. Se um NIC tem as suas próprias definições de servidor DNS, elas substituirão as definições do servidor DNS Olá para a rede virtual Olá. toolearn mais informações sobre as definições de DNS de NIC, consulte [interface tarefas e definições de rede](virtual-network-network-interface.md#change-dns-servers). toolearn mais informações sobre resolução de nomes para VMs e instâncias de função nos serviços de nuvem do Azure, consulte [a resolução de nomes para VMs e instâncias de função](virtual-networks-name-resolution-for-vms-and-role-instances.md). tooadd, alterar ou remover um servidor DNS:

1. Inicie sessão no toohello [portal](https://portal.azure.com) com uma conta que está a atribuir permissões para a função de contribuinte de rede Olá (no mínimo) para a sua subscrição. toolearn mais informações sobre a atribuição de funções e permissões tooaccounts, consulte [funções incorporadas para controlo de acesso baseado em funções do Azure](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor).
2. Na caixa de pesquisa de portal Olá, escreva **redes virtuais**. Nos resultados de pesquisa de Olá, selecione **redes virtuais**.
3. No Olá **redes virtuais** painel, clique em rede virtual Olá pretende toochange definições de DNS para.
4. No Olá virtual de rede painel, em **definições**, clique em **servidores DNS**.
5. Selecione uma das seguintes opções no painel de Olá apresenta uma lista de servidores DNS de Olá:
    - **Predefinição (fornecidos pelo Azure)**: todos os nomes de recursos e endereços IP privados são toohello registado automaticamente servidores de DNS do Azure. Pode resolver nomes entre todos os recursos que estão ligado toohello mesma rede virtual. Não é possível utilizar nomes de tooresolve esta opção várias redes virtuais. os nomes de tooresolve várias redes virtuais, tem de utilizar um servidor DNS personalizado.
    - **Personalizada**: pode adicionar um ou mais servidores, limitar a cópia de segurança toohello do Azure para uma rede virtual. toolearn mais informações sobre os limites do servidor DNS, consulte [limites do Azure](../azure-subscription-service-limits.md?toc=%2fazure%2fvirtual-network%2ftoc.json#virtual-networking-limits-classic). Tem Olá seguintes opções:
        - **Adicionar um endereço**: Adiciona a lista de servidores DNS de rede virtual tooyour servidor Olá. Esta opção também regista o servidor DNS de Olá com o Azure. Se já registou um servidor DNS com o Azure, pode selecionar esse servidor DNS na lista de Olá.
        - **Remover um endereço**: servidor toohello seguinte que pretende que o tooremove, clique em **X**. Servidor de Olá eliminar remove o servidor de Olá apenas a partir desta lista de rede virtual. servidor DNS Olá permanece registado no Azure para a sua toouse de redes virtuais.
        - **Reordenar os endereços do servidor DNS**: é importante tooverify que lista os servidores DNS no Olá corrigir ordem para o seu ambiente. Listas de servidor DNS são utilizadas por ordem de Olá que são especificados. Não funcionam como uma configuração round robin. Se o servidor DNS primeiro Olá na lista de Olá pode ser acedido, o cliente de Olá utiliza esse servidor DNS, independentemente se servidor DNS de Olá está a funcionar corretamente. Remova todos os servidores DNS Olá estão listados e, em seguida, adicioná-las novamente ordem Olá que pretende.
        - **Alterar um endereço**: servidor DNS Olá na lista de Olá de realce e, em seguida, introduza o nome do novo Olá.
6. Clique em **Guardar**.
7. Reinicie Olá VMs que são ligados toohello rede virtual, pelo que são atribuídas Olá novo servidor as definições de DNS. VMs continuam toouse as atuais definições de DNS quando estes forem reiniciados.

**Comandos**

|Ferramenta|Comando|
|---|---|
|CLI do Azure|[atualização do AZ rede vnet](/cli/azure/network/vnet?toc=%2fazure%2fvirtual-network%2ftoc.json#update)|
|PowerShell|[Set-AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork?toc=%2fazure%2fvirtual-network%2ftoc.json)|

## <a name="delete-vnet"></a>Eliminar uma rede virtual

Pode eliminar uma rede virtual apenas se não houver nenhuma tooit ligados de recursos. Se existirem recursos ligados tooany sub-rede numa rede virtual Olá, primeiro tem de eliminar os recursos de Olá que estão ligados tooall sub-redes na rede virtual Olá. passos de Olá demorar toodelete um recurso variam consoante o recurso Olá. documentação de Olá toolearn como ler toodelete recursos que estão ligados toosubnets, para cada tipo de recurso que pretende toodelete. toodelete uma rede virtual:

1. Inicie sessão no toohello [portal](https://portal.azure.com) com uma conta que seja atribuídas (no mínimo) permissões para a função de contribuinte de rede Olá para a sua subscrição. toolearn mais informações sobre a atribuição de funções e permissões tooaccounts, consulte [funções incorporadas para controlo de acesso baseado em funções do Azure](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor).
2. Na caixa de pesquisa de portal Olá, introduza **redes virtuais**. Nos resultados de pesquisa de Olá, clique em **redes virtuais**.
3. No Olá **redes virtuais** painel, rede virtual Olá selecione pretende toodelete.
4. No painel de rede virtual Olá, tooconfirm que não existem nenhum dispositivo ligado toohello de rede virtual, em **definições**, clique em **dispositivos ligados**. Se existirem dispositivos ligados, tem de as eliminar antes de poder eliminar a rede virtual Olá. Se não houver nenhuma dispositivos ligados, clique em **descrição geral**.
5. Olá parte superior do painel de Olá, clique em Olá **eliminar** ícone.
6. eliminação de Olá tooconfirm da rede virtual Olá, clique em **Sim**.


**Comandos**

|Ferramenta|Comando|
|---|---|
|CLI do Azure|[rede Azure vnet eliminar](/cli/azure/network/vnet?toc=%2fazure%2fvirtual-network%2ftoc.json#delete)|
|PowerShell|[Remove-AzureRmVirtualNetwork](/powershell/module/azurerm.network/remove-azurermvirtualnetwork?toc=%2fazure%2fvirtual-network%2ftoc.json)|


## <a name="next-steps"></a>Passos seguintes

- toocreate uma VM e, em seguida, ligue-a rede virtual tooa, consulte [criar uma rede virtual e ligar as VMs](virtual-network-get-started-vnet-subnet.md#create-vms).
- tráfego de rede toofilter entre sub-redes na rede virtual, consulte [criar grupos de segurança de rede](virtual-networks-create-nsg-arm-pportal.md).
- toopeer uma rede virtual tooanother rede virtual, consulte [criar um peering de rede virtual](virtual-network-create-peering.md#portal).
- toolearn sobre as opções para ligar uma rede no local do tooan de rede virtual, consulte [sobre o Gateway de VPN](../vpn-gateway/vpn-gateway-about-vpngateways.md?toc=%2fazure%2fvirtual-network%2ftoc.json#diagrams).
