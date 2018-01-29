---
title: "Tipos de endereços IP no Azure | Microsoft Docs"
description: "Saiba mais sobre os endereços IP públicos e privados no Azure."
services: virtual-network
documentationcenter: na
author: jimdial
manager: jeconnoc
editor: 
tags: azure-resource-manager
ms.assetid: 610b911c-f358-4cfe-ad82-8b61b87c3b7e
ms.service: virtual-network
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 11/16/2017
ms.author: jdial
ms.openlocfilehash: e3baedba814cf6ac19df72c49e1c95ea2cd5cf73
ms.sourcegitcommit: 7136d06474dd20bb8ef6a821c8d7e31edf3a2820
ms.translationtype: HT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/05/2017
---
# <a name="ip-address-types-and-allocation-methods-in-azure"></a>Tipos de endereços IP e métodos de alocação no Azure

Pode atribuir endereços IP a recursos do Azure para comunicar com outros recursos do Azure, a rede no local e a Internet. Existem dois tipos de endereços IP que pode utilizar no Azure:

* **Endereços IP públicos**: utilizados para comunicação com a Internet, incluindo os serviços do Azure destinados ao público.
* **Endereços IP privados**: utilizados para comunicação dentro de uma rede virtual do Azure (VNet) e da sua rede no local quando utiliza um gateway de VPN ou o circuito do ExpressRoute para expandir a sua rede para o Azure.

> [!NOTE]
> O Azure tem dois modelos de implementação diferentes para criar e trabalhar com os recursos: [Resource Manager e clássico](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json).  Este artigo explica como utilizar o modelo de implementação Resource Manager, o que é recomendado pela Microsoft para a maioria das novas implementações em vez do [modelo de implementação clássica](virtual-network-ip-addresses-overview-classic.md).
> 

Se estiver familiarizado com o modelo de implementação clássica, veja as [diferenças dos endereços IP entre a implementação Clássica e Resource Manager](virtual-network-ip-addresses-overview-classic.md#differences-between-resource-manager-and-classic-deployments).

## <a name="public-ip-addresses"></a>Endereços IP públicos

Os endereços IP públicos permitem que os recursos da Internet comuniquem com os recursos do Azure à entrada. Os endereços IP públicos também permitem que os recursos do Azure comuniquem com a Internet à saída, bem como com serviços do Azure destinados ao público com um endereço IP atribuído ao recurso. O endereço está dedicado ao recurso, até que a atribuição do mesmo seja anulada por si. Se um recurso não tiver um endereço IP público atribuído, continua a poder comunicar com a Internet à saída, mas o Azure atribui de forma dinâmica um endereço IP disponível que não se encontre dedicado ao recurso. Para obter mais informações sobre ligações de saída no Azure, veja [Noções sobre ligações de saída](../load-balancer/load-balancer-outbound-connections.md?toc=%2fazure%2fvirtual-network%2ftoc.json).

No Azure Resource Manager, os endereços [IP públicos](virtual-network-public-ip-address.md) são recursos que tem as suas próprias propriedades. Alguns dos recursos aos quais pode associar um recurso de endereço IP público são:

* Interfaces de rede de máquina virtual
* Balanceadores de carga com acesso à Internet
* Gateways de VPN
* Gateways de aplicação

### <a name="ip-address-version"></a>Versão do endereço IP

Os endereços IP públicos são criados com um endereço IPv4 ou IPv6. Os endereços IPv6 públicos só podem ser atribuídos a balanceadores de carga com acesso à Internet.

### <a name="sku"></a>SKU

Os endereços IP públicos são criados com um dos SKUs seguintes:

#### <a name="basic"></a>Básica

Todos os endereços IP públicos criados antes da introdução de SKUs são endereços IP públicos de SKU Básico. Com a introdução de SKUs, tem a opção de especificar que SKU pretende que o endereço IP público seja. Os endereços de SKU Básico:

- São atribuídos com o método de alocação estático ou dinâmico.
- São atribuídos a qualquer recurso do Azure ao qual possa ser atribuído um endereço IP público, como interfaces de rede, Gateways de VPN, Gateways de Aplicação e Balanceadores de carga com acesso à Internet.
- Podem ser atribuídos a uma zona específica.
- Não têm redundância de zona. Para saber mais sobre as zonas de disponibilidade, veja [Descrição geral das zonas de disponibilidade](../availability-zones/az-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json).

#### <a name="standard"></a>Standard

Os endereços IP de SKU Standard:

- São atribuídos apenas com o método de alocação estático.
- São atribuídos a interfaces de rede ou balanceadores de carga com acesso à Internet Standard. Para obter mais informações sobre os SKUs de balanceador de carga do Azure, veja [SKU standard de balanceador de carga do Azure](../load-balancer/load-balancer-standard-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json).
- Têm redundância de zona por predefinição. Podem ser criados zonais e garantidos numa zona de disponibilidade específica.  Para saber mais sobre as zonas de disponibilidade, veja [Descrição geral das zonas de disponibilidade](../availability-zones/az-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json).
 
> [!NOTE]
> Quando atribui um endereço IP público de SKU standard a uma interface de rede de máquina virtual, tem de permitir explicitamente o tráfego pretendido com um [grupo de segurança de rede](security-overview.md#network-security-groups).  A comunicação com o recurso falha até criar e associar um grupo de segurança de rede e permitir explicitamente o tráfego pretendido.

O SKU standard encontra-se em versão de pré-visualização. Antes de criar um endereço IP público de SKU Standard, primeiro tem de se registar na pré-visualização e criar o endereço numa localização suportada. Para se registar na pré-visualização, veja [Registar-se na pré-visualização do SKU standard](virtual-network-public-ip-address.md#register-for-the-standard-sku-preview). Para obter uma lista de localizações (regiões) suportadas, veja [Disponibilidade de região](../load-balancer/load-balancer-standard-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json#region-availability) e monitorize a página [Atualizações de Rede Virtual do Azure](https://azure.microsoft.com/updates/?product=virtual-network) para obter suporte de região adicional.


### <a name="allocation-method"></a>Método de alocação

Os endereços IP podem ser alocados a um recurso de endereço IP público de duas formas - *dinâmica* ou *estática*. O método de alocação predefinido é o *dinâmico*, no qual o endereço IP **não** é alocado no momento da criação. Em vez disso, o endereço IP público é alocado quando inicia (ou cria) o recurso associado (como uma VM ou um balanceador de carga). O endereço IP é libertado quando para (ou elimina) o recurso. Após ser libertado do recurso A, por exemplo, o endereço IP pode ser atribuído a um recurso diferente. Se o endereço IP for atribuído a um recurso diferente enquanto o recurso A está parado, quando reiniciar o recurso A, é atribuído um endereço IP diferente.

Para garantir que o endereço IP do recurso associado fica o mesmo, pode definir o método de alocação explicitamente como *estático*. É atribuído imediatamente um endereço IP estático. O endereço só é libertado quando elimina o recurso ou altera o método de alocação para *dinâmico*.

> [!NOTE]
> Mesmo se definir o método de alocação como *estático*, não pode especificar o endereço IP real atribuído ao recurso de endereço IP público. O Azure atribui o endereço IP a partir de um conjunto de endereços IP disponíveis na localização do Azure na qual o recurso é criado.
>

Normalmente, os endereços IP públicos são utilizados nos cenários seguintes:

* Quando o utilizador tem de atualizar as regras de firewall para comunicar com os seus recursos do Azure.
* Resolução de nomes DNS, em que a alteração de um endereço IP exigiria que os registos A fossem atualizados.
* Os seus recursos do Azure comunicam com outros serviços ou aplicações que utilizam um modelo de segurança baseado no endereço IP.
* Utiliza certificados SSL associados a um endereço IP.

> [!NOTE]
> O Azure aloca endereços IP públicos a partir de um intervalo exclusivo a cada região do Azure. Para obter detalhes, veja [Intervalos de IP do Azure Datacenter](https://www.microsoft.com/download/details.aspx?id=41653).
>

### <a name="dns-hostname-resolution"></a>Resolução de nomes de anfitrião DNS
Pode especificar uma etiqueta de nome de domínio DNS par um recurso IP público, que cria um mapeamento para *domainnamelabel*.*location*.cloudapp.azure.com para o endereço IP público nos servidores DNS geridos pelo Azure. Por exemplo, se criar um recurso de IP público com **contoso** como *domainnamelabel* na **localização** *E.U.A. Oeste* do Azure, o nome de domínio completamente qualificado (FQDN) **contoso.westus.cloudapp.azure.com** é resolvido para o endereço IP público do recurso. Pode utilizar o FQDN para criar um registo CNAME de domínio personalizado que aponte para o endereço IP público no Azure. Em vez de, ou além de, utilizar a etiqueta de nome DNS com o sufixo predefinido, pode utilizar o serviço DNS do Azure para configurar um nome DNS com um sufixo personalizado que é resolvido para o endereço IP público. Para obter mais informações, veja [Utilizar o DNS do Azure com um endereço IP público do Azure](../dns/dns-custom-domain.md?toc=%2fazure%2fvirtual-network%2ftoc.json#public-ip-address).

> [!IMPORTANT]
> Cada etiqueta de nome de domínio criada tem de ser exclusiva no âmbito da respetiva localização do Azure.  
>

### <a name="virtual-machines"></a>Máquinas virtuais

Pode associar um endereço IP público a uma máquina virtual do [Windows](../virtual-machines/windows/overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json) ou do [Linux](../virtual-machines/linux/overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json) ao atribuí-lo à respetiva **interface de rede**. Pode atribuir um endereço IP público dinâmico ou estático a uma máquina virtual. Saiba mais sobre como [atribuir endereços IP a interfaces de rede](virtual-network-network-interface-addresses.md).

### <a name="internet-facing-load-balancers"></a>Balanceadores de carga com acesso à Internet

Pode associar um endereço IP público criado com qualquer [SKU](#SKU) a um [Balanceador de Carga do Azure](../load-balancer/load-balancer-overview.md) ao atribuí-lo à configuração do **front-end** do balanceador de carga. O endereço IP público serve como endereço IP virtual (VIP) com balanceamento de carga. Pode atribuir um endereço IP público dinâmico ou estático a um front-end de balanceador de carga. Também pode atribuir múltiplos endereços IP públicos a um front-end de balanceador de carga, que permite cenários de [vários VIPs](../load-balancer/load-balancer-multivip-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json), como um ambiente multi-inquilinos com Web sites baseados em SSL. Para obter mais informações sobre os SKUs de balanceador de carga do Azure, veja [SKU standard de balanceador de carga do Azure](../load-balancer/load-balancer-standard-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json).

### <a name="vpn-gateways"></a>Gateways de VPN

Um [Gateway de VPN do Azure](../vpn-gateway/vpn-gateway-about-vpngateways.md?toc=%2fazure%2fvirtual-network%2ftoc.json) liga uma rede virtual do Azure a outras redes virtuais do Azure ou a uma rede no local. Um endereço IP público é atribuído ao Gateway de VPN para que possa comunicar com a rede remota. Só pode atribuir um endereço IP público *dinâmico* a um gateway de VPN.

### <a name="application-gateways"></a>Gateways de aplicação

Pode associar um endereço IP público a um [Gateway de Aplicação](../application-gateway/application-gateway-introduction.md?toc=%2fazure%2fvirtual-network%2ftoc.json) do Azure, ao atribuí-lo à configuração do **front-end** do gateway. Este endereço IP público funciona como um VIP com balanceamento de carga. Só pode atribuir um endereço IP público *dinâmico* à configuração de front-end de um gateway de aplicação.

### <a name="at-a-glance"></a>De relance
A tabela seguinte mostra a propriedade específica através da qual os endereços IP públicos podem ser associados a recursos de nível superior e os métodos de alocação possíveis (dinâmico ou estático) que podem ser utilizados.

| Recurso de nível superior | Associação de endereço IP | Dinâmica | Estático |
| --- | --- | --- | --- |
| Máquina virtual |Interface de rede |Sim |Sim |
| Balanceador de carga com acesso à Internet |Configuração de front-end |Sim |Sim |
| Gateway de VPN |Configuração de IP do gateway |Sim |Não |
| Gateway de aplicação |Configuração de front-end |Sim |Não |

## <a name="private-ip-addresses"></a>Endereços IP Privados
Os endereços IP privados permitem aos recursos do Azure comunicar com outros recursos numa [rede virtual](virtual-networks-overview.md) ou numa rede no local através de um gateway de VPN ou de um circuito do ExpressRoute, sem utilizar um endereço IP acessível pela Interne.

No modelo de implementação Azure Resource Manager, os endereços IP privados são associados aos tipos de recursos do Azure seguintes:

* Interfaces de rede de máquina virtual
* Balanceadores de carga internos (ILBs)
* Gateways de aplicação

### <a name="ip-address-version"></a>Versão do endereço IP

Os endereços IP privados são criados com um endereço IPv4 ou IPv6. Os endereços IPv6 privados só podem ser atribuídos com o método alocação dinâmico. Não é possível comunicar entre endereços IPv6 privados numa rede virtual. Pode comunicar internamente com um endereço IPv6 privado a partir da Internet, através de um balanceador de carga com acesso à Internet. Veja [Criar um balanceador de carga com acesso à Internet com IPv6](../load-balancer/load-balancer-ipv6-internet-ps.md?toc=%2fazure%2fvirtual-network%2ftoc.json) para obter detalhes.

### <a name="allocation-method"></a>Método de alocação

Os endereços IP privados são alocados a partir do intervalo de endereços da sub-rede da rede virtual em que um recurso está implementado. O Azure reserva os primeiros quatro endereços em cada intervalo de endereços da sub-rede, de modo a que os endereços não possam ser atribuídos aos recursos. Por exemplo, se o intervalo de endereços da sub-rede for 10.0.0.0/16, não é possível atribuir os endereços 10.0.0.0 a 10.0.0.3 aos recursos. Os endereços IP dentro do intervalo de endereços da sub-rede só podem ser atribuídos a um recurso de cada vez. 

Os endereços IP privados podem ser alocados de duas formas:

- **Dinâmica**: o Azure atribui o endereço IP não atribuído ou não reservado seguinte disponível no intervalo de endereços da sub-rede. Por exemplo, o Azure atribui o endereço 10.0.0.10 a um novo recurso caso os endereços 10.0.0.4 a 10.0.0.9 já estejam atribuídos a outros recursos. Dinâmico é o método de alocação predefinido. Após a atribuição, os endereços IP dinâmicos só são lançados se uma interface de rede for eliminada, atribuída a uma sub-rede diferente dentro da mesma rede virtual, ou se o método de alocação for alterado para estático e for especificado um endereço IP diferente. Por predefinição, o Azure atribui o endereço atribuído de forma dinâmica anterior como endereço estático quando o utilizador altera o método de alocação de dinâmico para estático.
- **Estática**: o utilizador seleciona e atribui um endereço IP não atribuído ou não reservado qualquer do intervalo de endereços da sub-rede. Por exemplo, se o intervalo de endereços de uma sub-rede for 10.0.0.0/16 e os endereços 10.0.0.4 a 10.0.0.9 já estiverem atribuídos a outros recursos, o utilizador pode atribuir qualquer endereço entre 10.0.0.10 e 10.0.255.254. Os endereços estáticos só são lançados se uma interface de rede for eliminada. Se o utilizador alterar o método de alocação para dinâmico, o Azure atribui de forma dinâmica o endereço IP estático atribuído anteriormente como endereço dinâmico, mesmo que o endereço não seja o endereço seguinte disponível do intervalo de endereços da sub-rede. O endereço também muda se a interface de rede for atribuída a uma sub-rede diferente dentro da mesma rede virtual, mas, para atribuir a interface de rede a uma sub-rede diferente, tem, primeiro, de alterar o método de alocação de estático para dinâmico. Assim que tiver atribuído a interface de rede a uma sub-rede diferente, pode alterar o método de alocação novamente para estático e atribuir um endereço IP do intervalo de endereços da nova sub-rede.

### <a name="virtual-machines"></a>Máquinas virtuais

Um ou mais endereços IP privados são atribuídos a uma ou mais **interfaces de rede** de uma máquina virtual do [Windows](../virtual-machines/windows/overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json) ou do [Linux](../virtual-machines/linux/overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json). Pode especificar o método de alocação como dinâmico ou estático para cada endereço IP privado.

#### <a name="internal-dns-hostname-resolution-for-virtual-machines"></a>Resolução de nomes de anfitrião DNS interna (para máquinas virtuais)

Todas as máquinas virtuais do Azure são configuradas com [servidores DNS geridos pelo Azure](virtual-networks-name-resolution-for-vms-and-role-instances.md#azure-provided-name-resolution) por predefinição, a não ser que configure explicitamente servidores DNS personalizados. Estes servidores DNS fornecem resolução de nomes interna para as máquinas virtuais que residam na mesma rede virtual.

Quando cria uma máquina virtual, é adicionado aos servidores DNS geridos pelo Azure um mapeamento do nome do anfitrião para o respetivo endereço IP privado. Se uma máquina virtual tiver várias interfaces de rede, ou várias configurações de IP para uma interface de rede, o nome de anfitrião é mapeado para o endereço IP privado da configuração de IP principal da interface de rede principal.

As máquinas virtuais configuradas com servidores DNS geridos pelo Azure conseguem resolver os nomes de anfitrião de todas as máquinas virtuais dentro da mesma rede virtual para os respetivos endereços IP privados. Para resolver os nomes de anfitrião de máquinas virtuais em redes virtuais ligadas, tem de utilizar um servidor DNS personalizado.

### <a name="internal-load-balancers-ilb--application-gateways"></a>Balanceadores de carga internos (ILBs) e gateways de aplicação

Pode atribuir um endereço IP privado à configuração de **front-end** de um [Balanceador de Carga Interno do Azure](../load-balancer/load-balancer-internal-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json) (ILB) ou de um [Gateway de Aplicação do Azure](../application-gateway/application-gateway-introduction.md?toc=%2fazure%2fvirtual-network%2ftoc.json). Este endereço IP privado funciona como um ponto final interno, que só é acessível pelos recursos dentro da respetiva rede virtual e pelas redes remotas ligadas à rede virtual. Pode atribuir um endereço IP privado dinâmico ou estático à configuração do front-end.

### <a name="at-a-glance"></a>De relance
A tabela seguinte mostra a propriedade específica através da qual os endereços IP privados podem ser associados a recursos de nível superior e os métodos de alocação possíveis (dinâmico ou estático) que podem ser utilizados.

| Recurso de nível superior | Associação de endereço IP | Dinâmica | Estático |
| --- | --- | --- | --- |
| Máquina virtual |Interface de rede |Sim |Sim |
| Load balancer |Configuração de front-end |Sim |Sim |
| Gateway de aplicação |Configuração de front-end |Sim |Sim |

## <a name="limits"></a>Limites
Os limites impostos no endereçamento IP estão indicados no conjunto completo de [limites para redes](../azure-subscription-service-limits.md?toc=%2fazure%2fvirtual-network%2ftoc.json#networking-limits) no Azure. Os limites são por região e por subscrição. Pode [contactar o suporte](https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade) para aumentar os limites predefinidos até aos limites máximos, com base nas necessidades da sua atividade.

## <a name="pricing"></a>Preços
Os endereços IP públicos podem ter custos nominais. Para saber mais sobre os preços dos endereços IP no Azure, reveja a página [Preços de Endereços IP](https://azure.microsoft.com/pricing/details/ip-addresses).

## <a name="next-steps"></a>Passos seguintes
* [Deploy a VM with a static public IP using the Azure portal (Implementar uma VM com IP público estático através do portal do Azure)](virtual-network-deploy-static-pip-arm-portal.md)
* [Deploy a VM with a static public IP using a template (Implementar uma VM com um IP estático público através de um modelo)](virtual-network-deploy-static-pip-arm-template.md)
* [Deploy a VM with a static private IP address using the Azure portal (Implementar uma VM com um endereço IP privado estático através do portal do Azure)](virtual-networks-static-private-ip-arm-pportal.md)
