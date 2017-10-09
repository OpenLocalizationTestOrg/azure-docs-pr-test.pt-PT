---
title: "aaaCreate, alterar ou eliminar um endereço IP público do Azure | Microsoft Docs"
description: "Saiba como toocreate, alterar ou eliminar um endereço IP público."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: bb71abaf-b2d9-4147-b607-38067a10caf6
ms.service: virtual-network
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/24/2017
ms.author: jdial
ms.openlocfilehash: 0f2578e8661c8f33419b896debcfa0ba1b41fc5c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-change-or-delete-a-public-ip-address"></a>Criar, alterar ou eliminar um endereço IP público

Saiba mais sobre um IP público de endereço e como toocreate, alterar e eliminar um. Um endereço IP público é um recurso com as suas próprias definições configuráveis. Permite a atribuição de recursos do Azure de um tooother de endereço IP público:
- Entrada tooresources de conectividade da Internet, tais como máquinas virtuais do Azure (VM), conjuntos de dimensionamento de Máquina Virtual do Azure, o Gateway de VPN do Azure, gateways de aplicação e Balanceadores de carga do Azure para a Internet. Recursos do Azure não é possível receber a comunicação de entrada de Olá Internet sem um endereço IP público atribuído. Embora alguns recursos do Azure são inerentemente acessíveis através de endereços IP públicos, outros recursos tem de ter atribuídos toothem toobe acessível a partir da Internet de Olá os endereços IP públicos.
- Conectividade de saída toohello Internet utilizando um endereço IP previsível. Por exemplo, uma máquina virtual podem comunicar toohello saída à Internet sem um endereço atribuído tooit público do IP, mas o respetivo endereço é o endereço de rede traduzido por Azure tooan imprevisíveis, endereço público. Atribuir um recurso de tooa de endereço IP público permite-lhe tooknow qual o endereço IP é utilizado para ligação Olá de saída. Embora previsível, endereço Olá pode alterar, dependendo do método de atribuição de Olá escolhido. Para obter mais informações, consulte [criar um endereço IP público](#create-a-public-ip-address). mais informações sobre ligações de saída a partir dos recursos do Azure, leia Olá toolearn [compreender ligações de saída](../load-balancer/load-balancer-outbound-connections.md?toc=%2fazure%2fvirtual-network%2ftoc.json) artigo.

## <a name="before-you-begin"></a>Antes de começar

Conclua Olá seguintes tarefas antes de concluir os passos em qualquer secção deste artigo:

- Olá revisão [Azure limita](../azure-subscription-service-limits.md?toc=%2fazure%2fvirtual-network%2ftoc.json#azure-resource-manager-virtual-networking-limits) toolearn artigo sobre os limites de endereços IP públicos.
- Inicie sessão no toohello Azure [portal](https://portal.azure.com), interface de linha de comandos (CLI) do Azure ou o Azure PowerShell com uma conta do Azure. Se ainda não tiver uma conta do Azure, inscreva-se um [conta de avaliação gratuita](https://azure.microsoft.com/free).
- Se utilizar o PowerShell comandos toocomplete tarefas neste artigo, [instalar e configurar o Azure PowerShell](/powershell/azureps-cmdlets-docs?toc=%2fazure%2fvirtual-network%2ftoc.json). Certifique-se de que tem a versão mais recente do Olá dos mini-comandos de Azure PowerShell Olá instalados. tooget ajuda para comandos do PowerShell, com exemplos, digite `get-help <command> -full`.
- Se utilizar a interface de linha de comandos do Azure (CLI) comandos toocomplete tarefas neste artigo, [instalar e configurar a CLI do Azure de Olá](/cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json). Certifique-se de que tem a versão mais recente do Olá de Olá CLI do Azure instalados. tooget ajuda para comandos da CLI, escreva `az <command> --help`. Em vez de instalar Olá CLI e respetivos pré-requisitos, pode utilizar Olá Shell de nuvem do Azure. Olá Shell de nuvem do Azure é uma shell de deteção livre que podem ser executados diretamente no Olá portal do Azure. Tem Olá CLI do Azure pré-instalado e configurado toouse com a sua conta. Olá toouse Shell de nuvem, clique em Olá nuvem Shell **> _** botão, Olá parte superior do Olá [portal](https://portal.azure.com).

Endereços IP públicos têm uma cobrança nominal. os preços tooview Olá, leia Olá [preços de endereço IP](https://azure.microsoft.com/pricing/details/ip-addresses) página. 

## <a name="create-a-public-ip-address"></a>Crie um endereço IP público

1. Inicie sessão no toohello [portal do Azure](https://portal.azure.com) com uma conta que seja atribuídas (no mínimo) permissões para a função de contribuinte de rede Olá para a sua subscrição. Olá leitura [funções incorporadas para controlo de acesso baseado em funções do Azure](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) artigo toolearn mais informações sobre a atribuição de funções e permissões tooaccounts.
2. Na caixa de Olá que contém texto Olá *procurar recursos* Olá parte superior do portal do Azure de Olá, escreva *endereço ip público*. Quando **endereços IP públicos** é apresentado nos resultados de pesquisa de Olá, clique no mesmo.
3. Clique em **+ adicionar** no Olá **endereço IP público** painel que aparece.
4. Introduza ou selecione os valores de Olá seguintes definições no Olá **Criar endereço IP público** painel apresentado, clique em **criar**:

    |Definição|Necessário?|Detalhes|
    |---|---|---|
    |Nome|Sim|nome de Olá têm de ser exclusivo dentro do grupo de recursos de Olá que selecionar.|
    |Versão do IP|Sim| Selecione IPv4 ou IPv6. Enquanto IPv4 público endereços podem ser atribuídos tooseveral recursos do Azure, um endereço IP público IPv6 só pode ser atribuído Balanceador de carga tooan para a Internet. Balanceador de carga Olá pode carregar saldo IPv6 tráfego tooAzure máquinas. Saiba mais sobre [máquinas de toovirtual de tráfego IPv6 de balanceamento de carga](../load-balancer/load-balancer-ipv6-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json).
    |Atribuição de endereços IP|Sim|**Dynamic:** endereços dinâmicos são atribuídos apenas depois de endereço IP público do Olá está associado tooa NIC anexado tooa VM e hello VM for iniciada pela Olá pela primeira vez. Endereços dinâmicos podem alterar se Olá VM Olá NIC anexado toois parado (desalocado). Olá endereço permanece Olá, mesmo se hello VM é reiniciada ou parada (mas não desalocada). **Estática:** endereços estáticos são atribuídos quando for criado o endereço IP público Olá. Endereços estáticos fazê-lo não alteração mesmo que se hello VM é colocada numa Olá parado (desalocado) de estado. endereço de Olá apenas é libertado quando Olá NIC é eliminado. Para poder alterar método de atribuição de Olá depois Olá NIC é criado. Se selecionar o IPv6 para Olá **versão do IP**, o método de atribuição apenas disponível Olá é **dinâmica**.|
    |Tempo limite de inatividade (minutos)|Não|Minutos tookeep uma ligação TCP ou HTTP aberta sem depender de mensagens keep-alive de toosend de clientes. Se selecionar IPv6 para **IP versão**, este valor não pode ser alterado. |
    |Etiqueta de nome DNS|Não|Tem de ser exclusivos num Olá localização do Azure, criar o nome de Olá no (em todas as subscrições e todos os clientes). Olá serviço DNS público do Azure regista automaticamente Olá nome e endereço IP para que possa ligar tooa recursos com o nome de Olá. Azure acrescenta *location.cloudapp.azure.com* (em que a localização é a localização de Olá selecionar) o nome de toohello fornecer toocreate Olá completamente qualificado nome DNS. Se optar por toocreate ambas as versões de endereço, hello mesmo nome DNS é atribuído tooboth Olá IPv4 e os endereços IPv6. Olá serviço DNS do Azure contém registos de nome de um de IPv4 e IPv6 AAAA e responde com ambos os registos quando o nome DNS Olá é consultado. cliente de Olá escolhe que toocommunicate endereço (IPv4 ou IPv6) com.|
    |Criar um endereço IPv6 (ou IPv4)|Não| Indica se é apresentado o IPv6 ou IPv4 está dependente aquilo que selecionar para **IP versão**. Por exemplo, se selecionar **IPv4** para **IP versão**, **IPv6** é apresentado aqui.
    |Nome (apenas visível se tiver selecionado Olá **criar um endereço IPv6 (ou IPv4)** caixa de verificação)|Sim, se selecionar Olá **criar IPv6** (ou IPv4) caixa de verificação.|Olá nome tem de ser diferente do nome de Olá introduzido pela primeira vez para Olá **nome** nesta lista. Se escolher toocreate IPv4 e um endereço IPv6, o portal Olá cria dois separados endereço recursos do IP público, uma com cada versão do endereço IP atribuído tooit.|
    |Atribuição de endereços IP (apenas visível se tiver selecionado Olá **criar um endereço IPv6 (ou IPv4)** caixa de verificação)|Sim, se selecionar Olá **criar IPv6** (ou IPv4) caixa de verificação.|Se a caixa de verificação Olá indica **criar um endereço IPv4**, pode selecionar um método de atribuição. Se a caixa de verificação Olá indica **criar um endereço IPv6**, não é possível selecionar um método de atribuição, como deve ser **dinâmica**.|
    |Subscrição|Sim|Tem de existir na Olá mesmo [subscrição](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#subscription) como recurso Olá pretende tooassociate Olá público endereço IP.|
    |Grupo de recursos|Sim|Pode existir no Olá idêntica ou diferente, [grupo de recursos](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#resource-group) como recurso Olá pretende tooassociate Olá público endereço IP.|
    |Localização|Sim|Tem de existir na Olá mesmo [localização](https://azure.microsoft.com/regions), também denominados tooas região, como o recurso de Olá pretende tooassociate Olá público endereço IP.|

**Comandos**

Apesar do portal de Olá fornece Olá opção toocreate dois endereços recursos do IP público (IPv4 e um IPv6), Olá os seguintes comandos do PowerShell e CLI criar um recurso com um endereço para uma versão IP ou Olá outros. Se pretender que os dois endereços recursos do IP público, uma para cada versão do IP, tem de executar o comando de Olá duas vezes, especificando diferentes nomes e versões para recursos Olá do endereço IP público. 

|Ferramenta|Comando|
|---|---|
|CLI|[Criar AZ público-ip da rede](/cli/azure/network/public-ip?toc=%2fazure%2fvirtual-network%2ftoc.json#create)|
|PowerShell|[Novo AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress)|

## <a name="view-change-settings-for-or-delete-a-public-ip-address"></a>Ver, alterar as definições ou eliminar um endereço IP público

1. Inicie sessão no toohello [portal do Azure](https://portal.azure.com) com uma conta que seja atribuídas (no mínimo) permissões para a função de contribuinte de rede Olá para a sua subscrição. Olá leitura [funções incorporadas para controlo de acesso baseado em funções do Azure](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) artigo toolearn mais informações sobre a atribuição de funções e permissões tooaccounts.
2. Na caixa de Olá que contém texto Olá *procurar recursos* Olá parte superior do portal do Azure de Olá, escreva *endereço ip público*. Quando **endereços IP públicos** é apresentado nos resultados de pesquisa de Olá, clique no mesmo.
3. No Olá **endereços IP públicos** painel apresentado, clique em nome de Olá do Olá endereço IP público que pretende tooview, alterar as definições ou elimina.
4. No painel de Olá que aparece para o endereço IP público Olá, um completado dos Olá seguintes opções consoante pretenda tooview, eliminar ou alterar o endereço IP público Olá.
    - **Vista**: Olá **descrição geral** seção do painel de Olá mostra definições da chave do endereço IP público do Olá, tais como a interface de rede Olá está demasiado associado (se o endereço de Olá interface de rede tooa associado). portal de Olá não apresenta a versão de Olá do endereço Olá (IPv4 ou IPv6). informações de versão de Olá tooview, utilize Olá PowerShell ou o CLI comando tooview Olá endereço IP público. Se a versão do endereço IP Olá for IPv6, Olá atribuído endereço não é apresentada pelo portal Olá, PowerShell ou Olá CLI. 
    - **Eliminar**: toodelete Olá endereço IP público, clique em **eliminar** no Olá **descrição geral** secção do painel de Olá. Se o endereço de Olá for configuração de IP tooan atualmente associados, não pode ser eliminada. Se o endereço de Olá está atualmente associado uma configuração, clique em **desassocie** endereço de Olá toodissociate da configuração de IP Olá.
    - **Alteração**: clique em **configuração**. Alterar as definições através de informações de Olá no passo 4 do Olá [criar um endereço IP público](#create-a-public-ip-address) secção deste artigo. atribuição de Olá toochange para um endereço IPv4 de toodynamic estático, tem primeiro de dissociá endereço IPv4 público Olá da configuração de IP Olá que está associado. Em seguida, pode alterar toodynamic de método de atribuição de Olá e clique em **associar** toohello de endereço IP do tooassociate Olá mesmo IP configuração, uma configuração diferente ou pode deixá-lo-desassociada. toodissociate um endereço IP público, em Olá **descrição geral** secção, clique em **desassocie**.

>[!WARNING]
>Quando alterar o método de atribuição de Olá de toodynamic estático, perderá endereço IP de Olá que foi atribuído toohello endereço IP público. Ao hello do Azure servidores DNS públicos manter um mapeamento entre os endereços estáticos ou dinâmicos e qualquer etiqueta de nome DNS (se for definido um), um endereço IP dinâmico pode ser alteradas quando Olá VM é iniciado depois de ser no Olá parada (desalocado) de estado. endereço de Olá tooprevent de alteração, atribua um endereço IP estático.

**Comandos**

|Ferramenta|Comando|
|---|---|
|CLI|[lista de ip público de rede AZ](/cli/azure/network/public-ip?toc=%2fazure%2fvirtual-network%2ftoc.json#list) toolist os endereços IP públicos, [az rede pública-ip-mostrar](/cli/azure/network/public-ip?toc=%2fazure%2fvirtual-network%2ftoc.json#show) definições tooshow; [atualização de ip público de rede az](/cli/azure/network/public-ip?toc=%2fazure%2fvirtual-network%2ftoc.json#update) tooupdate; [az público-ip da rede eliminar](/cli/azure/network/public-ip?toc=%2fazure%2fvirtual-network%2ftoc.json#delete) toodelete|
|PowerShell|[Get-AzureRmPublicIpAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress?toc=%2fazure%2fvirtual-network%2ftoc.json) tooretrieve um IP público objeto de endereço e ver as respetivas definições, [conjunto AzureRmPublicIpAddress](/powershell/resourcemanager/azurerm.network/set-azurermpublicipaddress?toc=%2fazure%2fvirtual-network%2ftoc.json) definições tooupdate; [Remover AzureRmPublicIpAddress](/powershell/module/azurerm.network/remove-azurermpublicipaddress) toodelete|

## <a name="next-steps"></a>Passos seguintes
Atribua endereços IP públicos durante a criação de Olá os seguintes recursos do Azure:

- [Windows](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-network%2ftoc.json) ou [Linux](../virtual-machines/linux/quick-create-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) máquinas virtuais
- [Balanceador de carga do Azure para a Internet](../load-balancer/load-balancer-get-started-internet-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json)
- [Gateway de aplicação do Azure](../application-gateway/application-gateway-create-gateway-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json)
- [Ligação site a site utilizando um Gateway de VPN do Azure](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json)
- [Conjunto de dimensionamento da Máquina Virtual do Azure](../virtual-machine-scale-sets/virtual-machine-scale-sets-portal-create.md?toc=%2fazure%2fvirtual-network%2ftoc.json)
