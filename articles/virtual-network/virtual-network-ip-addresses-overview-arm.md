---
title: "tipos de endereço aaaIP no Azure | Microsoft Docs"
description: "Saiba mais sobre os endereços IP públicos e privados no Azure."
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
tags: azure-resource-manager
ms.assetid: 610b911c-f358-4cfe-ad82-8b61b87c3b7e
ms.service: virtual-network
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/27/2016
ms.author: jdial
ms.openlocfilehash: 402d3707c00f0b3bf3ef1febd5ade66223da74bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="ip-address-types-and-allocation-methods-in-azure"></a>Tipos de endereços IP e métodos de alocação no Azure
Pode atribuir IP endereços tooAzure recursos toocommunicate com outros recursos do Azure, a sua rede no local e Olá Internet. Existem dois tipos de endereços IP que pode utilizar no Azure:

* **Endereços IP públicos**: utilizado para comunicação com Olá Internet, incluindo os serviços de destinado ao público do Azure
* **Endereços IP privados**: utilizado para comunicação dentro de uma rede virtual do Azure (VNet) e no local de rede quando utiliza o gateway VPN ou tooextend de circuito de ExpressRoute tooAzure sua rede.

> [!NOTE]
> O Azure tem dois modelos de implementação diferentes para criar e trabalhar com os recursos: [Resource Manager e clássico](../resource-manager-deployment-model.md).  Este artigo abrange utilizando o modelo de implementação Resource Manager de Olá, que a Microsoft recomenda-se para a maioria das implementações de novo em vez de Olá [modelo de implementação clássica](virtual-network-ip-addresses-overview-classic.md).
> 

Se estiver familiarizado com o modelo de implementação clássica Olá, verifique Olá [diferenças entre clássico de endereçamento de IP e o Resource Manager](virtual-network-ip-addresses-overview-classic.md#differences-between-resource-manager-and-classic-deployments).

## <a name="public-ip-addresses"></a>Endereços IP públicos
Endereços IP públicos permitem toocommunicate de recursos do Azure com os serviços de destinado ao público de Internet e o Azure, tal como [a Cache de Redis do Azure](https://azure.microsoft.com/services/cache/), [Event Hubs do Azure](https://azure.microsoft.com/services/event-hubs/), [bases de dados do SQL](../sql-database/sql-database-technical-overview.md), e [storage do Azure](../storage/common/storage-introduction.md).

No Azure Resource Manager, os endereços [IP públicos](resource-groups-networking.md#public-ip-address) são recursos que tem as suas próprias propriedades. Pode associar um recurso de endereço IP público com qualquer um dos Olá os seguintes recursos:

* Máquinas virtuais (VM)
* Balanceadores de carga com acesso à Internet
* Gateways de VPN
* Gateways de aplicação

### <a name="allocation-method"></a>Método de alocação
Existem dois métodos em que um endereço IP está alocado tooa *pública* recurso de IP - *dinâmica* ou *estático*. método de alocação Olá predefinido é *dinâmica*, em que é um endereço IP **não** alocada Olá que da respetiva criação. Em vez disso, o endereço IP público Olá é atribuído quando iniciar (ou crie) recursos de Olá associado (como uma VM ou Balanceador de carga). endereço IP Olá é libertado ao parar (ou eliminar) recursos de Olá. Isto faz com que toochange de endereço IP de Olá quando parar e iniciar um recurso.

endereço IP de Olá tooensure para hello recursos associados permanecem Olá mesmo, pode definir o método de alocação de Olá explicitamente demasiado*estático*. Neste caso, é atribuído imediatamente um endereço IP. Lançado apenas ao eliminar o recurso de Olá ou alterar o método de alocação de demasiado*dinâmica*.

> [!NOTE]
> Mesmo quando configurar o método de alocação de Olá demasiado*estático*, não é possível especificar Olá real IP endereço atribuído toohello *recurso de IP público*. Em vez disso, obtém atribuído partir de um conjunto de endereços IP disponíveis na localização do Azure de Olá recursos Olá é criado na.
>

Endereços IP públicos estáticos são frequentemente utilizados no Olá os seguintes cenários:

* Os utilizadores finais necessitam tooupdate toocommunicate de regras de firewall com os recursos do Azure.
* Resolução de nomes DNS, em que a alteração de um endereço IP exigiria que os registos A fossem atualizados.
* Os seus recursos do Azure comunicam com outros serviços ou aplicações que utilizam um modelo de segurança baseado no endereço IP.
* Utilize o endereço IP do SSL certificados tooan ligado.

> [!NOTE]
> lista de Olá de intervalos de IP a partir da qual os endereços IP públicos (dinâmico/estático) são atribuídos recursos tooAzure está publicada no [intervalos de IP de Datacenter do Azure](https://www.microsoft.com/download/details.aspx?id=41653).
>

### <a name="dns-hostname-resolution"></a>Resolução de nomes de anfitrião DNS
Pode especificar uma etiqueta de nome de domínio DNS para um recurso IP público, que cria um mapeamento para *domainnamelabel*. *localização*. cloudapp.azure.com toohello público endereço IP em servidores de DNS do Azure gerida pelo Olá. Por exemplo, se criar um recurso IP público com **contoso** como um *domainnamelabel* no Olá **EUA oeste** Azure *localização*, Olá o nome de domínio completamente qualificado (FQDN) **contoso.westus.cloudapp.azure.com** irá resolver o endereço IP público toohello do recurso de Olá. Pode utilizar este FQDN toocreate um registo CNAME de domínio personalizado que aponta de endereço IP público do toohello no Azure.

> [!IMPORTANT]
> Cada etiqueta de nome de domínio criada tem de ser exclusiva no âmbito da respetiva localização do Azure.  
>

### <a name="virtual-machines"></a>Máquinas virtuais
Pode associar um endereço IP público com um [Windows](../virtual-machines/windows/overview.md) ou [Linux](../virtual-machines/virtual-machines-linux-about.md) VM atribuindo-tooits **interface de rede**. No caso de Olá de uma VM com várias interfaces de rede, pode atribuir-toohello *primário* apenas a interface de rede. Pode atribuir uma dinâmica ou um estático público IP endereço tooa VM.

### <a name="internet-facing-load-balancers"></a>Balanceadores de carga com acesso à Internet
Pode associar um endereço IP público com um [Azure Load Balancer](../load-balancer/load-balancer-overview.md), atribuindo-toohello Balanceador de carga **front-end** configuração. Este endereço IP serve como um endereço IP virtual (VIP) com balanceamento de carga. Pode atribuir um dinâmico ou estático público IP endereço tooa Balanceador de carga front-end. Também pode atribuir várias pública IP endereços tooa Balanceador de carga front-end, permitindo [várias VIP](../load-balancer/load-balancer-multivip.md) cenários, como num ambiente multi-inquilino com Web sites baseados em SSL.

### <a name="vpn-gateways"></a>Gateways de VPN
[Gateway de VPN do Azure](../vpn-gateway/vpn-gateway-about-vpngateways.md) é utilizado tooconnect uma rede virtual do Azure (VNet) tooother as VNets do Azure ou tooan rede no local. Terá de tooassign um tooits de endereço IP público **configuração de IP** tooenable-toocommunicate com rede remota Olá. Atualmente, só é possível atribuir um *dinâmica* público gateway de VPN do tooa endereço IP.

### <a name="application-gateways"></a>Gateways de aplicação
Pode associar um endereço IP público com um Azure [Gateway de aplicação](../application-gateway/application-gateway-introduction.md), atribuindo-lo do gateway toohello **front-end** configuração. Este endereço IP público funciona como um VIP com balanceamento de carga. Atualmente, só é possível atribuir um *dinâmica* pública tooan application gateway front-end configuração do endereço IP.

### <a name="at-a-glance"></a>De relance
tabela de Olá abaixo mostra a propriedade específica Olá através do qual pode ser um endereço IP público recurso mais superior tooa associados e Olá alocação possíveis métodos (dinâmicos ou estáticos) que podem ser utilizados.

| Recurso de nível superior | Associação de endereço IP | Dinâmica | Estático |
| --- | --- | --- | --- |
| Máquina virtual |Interface de rede |Sim |Sim |
| Load balancer |Configuração de front-end |Sim |Sim |
| Gateway de VPN |Configuração de IP do gateway |Sim |Não |
| Gateway de aplicação |Configuração de front-end |Sim |Não |

## <a name="private-ip-addresses"></a>Endereços IP Privados
Endereços IP privados permitem toocommunicate de recursos do Azure com outros recursos num [rede virtual](virtual-networks-overview.md) ou a uma rede no local através de um gateway de VPN ou o circuito do ExpressRoute, sem utilizar um endereço IP acessível para a Internet.

No modelo de implementação Azure Resource Manager Olá, um endereço IP privado é associado toohello os seguintes tipos de recursos do Azure:

* VMs
* Balanceadores de carga internos (ILBs)
* Gateways de aplicação

### <a name="allocation-method"></a>Método de alocação
Foi atribuído um endereço IP privado de endereço Olá intervalo de Olá sub-rede toowhich Olá recurso está ligado. intervalo de endereços de Olá da própria sub-rede de Olá faz parte do intervalo de endereços da VNet Olá.

Os endereços IP privados podem ser alocados de duas formas - *dinâmica* ou *estática*. método de alocação Olá predefinido é *dinâmica*, em que o endereço IP Olá é automaticamente atribuído a partir de sub-rede do recurso Olá (utilizando DHCP). Este endereço IP pode ser alteradas quando parar e iniciar o recurso de Olá.

Pode definir o método de alocação de Olá demasiado*estático* permanece de endereço IP do tooensure Olá Olá mesmo. Neste caso, terá também tooprovide um endereço IP válido que faz parte da sub-rede do recurso Olá.

Geralmente, os endereços IP privados estáticos são utilizados para:

* VMs que funcionam como controladores de domínio ou servidores DNS.
* Recursos que precisam de regras de firewall que utilizem endereços IP.
* Recursos acedidos por outros recursos/aplicações através de um endereço IP.

### <a name="virtual-machines"></a>Máquinas virtuais
Um endereço IP privado é atribuído toohello **interface de rede** de um [Windows](../virtual-machines/windows/overview.md) ou [Linux](../virtual-machines/virtual-machines-linux-about.md) VM. No caso de VMs de várias interfaces de rede, é atribuído um endereço IP privado a cada interface. Pode especificar o método de alocação de Olá como dinâmico ou estático para uma interface de rede.

#### <a name="internal-dns-hostname-resolution-for-vms"></a>Resolução de nomes de anfitrião DNS interna (para VMs)
Todas as VMs do Azure são configuradas com [servidores DNS geridos pelo Azure](virtual-networks-name-resolution-for-vms-and-role-instances.md#azure-provided-name-resolution) por predefinição, a não ser que configure explicitamente servidores DNS personalizados. Estes servidores DNS fornecem a resolução dos nomes internos para VMs que residem no Olá mesmo VNet.

Quando cria uma VM, um mapeamento para o endereço IP Olá hostname tooits privado é adicionado a servidores DNS do Azure gerida pelo toohello. Em caso de uma interface de rede multi VM, Olá hostname está mapeado toohello endereço IP privado Olá primário da interface de rede.

VMs configuradas com os servidores DNS geridos pelo Azure será capaz de tooresolve Olá hostnames de todas as VMs dentro dos respetivos endereços IP privados do VNet tootheir.

### <a name="internal-load-balancers-ilb--application-gateways"></a>Balanceadores de carga internos (ILBs) e gateways de aplicação
Pode atribuir um toohello de endereço IP privado **front-end** configuração de um [Balanceador de carga interno Azure](../load-balancer/load-balancer-internal-overview.md) (ILB) ou um [Gateway de aplicação do Azure](../application-gateway/application-gateway-introduction.md). Este endereço IP privado funciona como um ponto final interno, acessível recursos toohello apenas dentro da sua rede virtual (VNet) e a redes remotas Olá ligado toohello VNet. Pode atribuir a uma dinâmica ou estática privada toohello front-end configuração do endereço IP.

### <a name="at-a-glance"></a>De relance
tabela de Olá abaixo mostra a propriedade específica Olá através do qual pode ser um endereço IP privado recurso mais superior tooa associados e Olá alocação possíveis métodos (dinâmicos ou estáticos) que podem ser utilizados.

| Recurso de nível superior | Associação de endereço IP | Dinâmica | Estático |
| --- | --- | --- | --- |
| Máquina virtual |Interface de rede |Sim |Sim |
| Load balancer |Configuração de front-end |Sim |Sim |
| Gateway de aplicação |Configuração de front-end |Sim |Sim |

## <a name="limits"></a>Limites
Olá limites impostos no endereçamento IP são indicados em conjunto completo de Olá de [limita para funcionamento em rede](../azure-subscription-service-limits.md#networking-limits) no Azure. Estes limites são por região e por subscrição. Pode [contacte o suporte](https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade) limites de predefinição Olá tooincrease segurança toohello os limites máximos com base nas necessidades de negócio.

## <a name="pricing"></a>Preços
Os endereços IP públicos podem ter custos nominais. toolearn mais informações sobre o IP de endereços de preço no Azure, reveja Olá [preços de endereço IP](https://azure.microsoft.com/pricing/details/ip-addresses) página.

## <a name="next-steps"></a>Passos seguintes
* [Implementar uma VM com um IP público estático utilizando Olá portal do Azure](virtual-network-deploy-static-pip-arm-portal.md)
* [Deploy a VM with a static public IP using a template (Implementar uma VM com um IP estático público através de um modelo)](virtual-network-deploy-static-pip-arm-template.md)
* [Implementar uma VM com um endereço IP privado estático utilizando Olá portal do Azure](virtual-networks-static-private-ip-arm-pportal.md)
