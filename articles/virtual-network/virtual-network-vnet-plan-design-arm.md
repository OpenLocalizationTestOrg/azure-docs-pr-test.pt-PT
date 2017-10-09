---
title: "aaaAzure rede Virtual (VNet) plano e do guia de conceção | Microsoft Docs"
description: "Saiba como tooplan e design de redes virtuais no Azure com base nos seus requisitos de isolamento, conectividade e localização."
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
ms.assetid: 3a4a9aea-7608-4d2e-bb3c-40de2e537200
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/08/2016
ms.author: jdial
ms.openlocfilehash: f3ffadf8cf254f64b1f86b44f90315d2bc679f63
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="plan-and-design-azure-virtual-networks"></a>Planear e estruturar as redes virtuais do Azure
Criar um tooexperiment VNet com o fácil suficiente, mas possibilidades são, irá implementar várias VNets ao longo do tempo toosupport Olá produção às necessidades da sua organização. Com algum planeamento e conceção, irá ser capaz de toodeploy VNets e ligar recursos Olá, que terá de forma mais eficaz. Se não estiver familiarizado com as VNets, é recomendado que lhe [Saiba mais sobre as VNets](virtual-networks-overview.md) e [como toodeploy](virtual-networks-create-vnet-arm-pportal.md) um antes de continuar.

## <a name="plan"></a>Planear
Uma compreensão profunda sobre as subscrições do Azure, regiões e recursos de rede é essencial para êxito. Pode utilizar a lista de Olá considerações abaixo como um ponto de partida. Assim que compreender as considerações, poderá definir requisitos de Olá para o design de rede.

### <a name="considerations"></a>Considerações
Antes de atender Olá abaixo de perguntas de planeamento, considere o seguinte Olá:

* Tudo o que cria no Azure é composto por um ou mais recursos. Uma máquina virtual (VM) é um recurso, Olá adaptador interface de rede (NIC) utilizado por uma VM é um recurso, endereço IP público Olá utilizado por um NIC é um recurso, Olá de VNet Olá NIC está ligado toois um recurso.
* Criar recursos dentro de um [região do Azure](https://azure.microsoft.com/regions/#services) e subscrição. Recursos só podem ser ligado tooa rede virtual que existe na Olá mesmo recurso de subscrição e região da Olá.
* Pode ligar redes virtuais tooeach outros utilizando:
    * **[Peering de rede virtual](virtual-network-peering-overview.md)**: redes virtuais Olá tem de existir na Olá mesma região do Azure. Largura de banda entre os recursos na redes virtuais em modo de peering é Olá mesmo como se recursos Olá foram toohello ligada mesma rede virtual.
    * **Um Azure [Gateway de VPN](../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md)**: redes virtuais Olá podem existir no Olá mesmo, ou em diferentes regiões do Azure. Largura de banda entre os recursos na redes virtuais ligadas através de um Gateway de VPN é limitada pela largura de banda de Olá de Olá Gateway de VPN.
* Pode ligar a rede do VNets tooyour no local utilizando um dos Olá [opções de conectividade](../vpn-gateway/vpn-gateway-about-vpngateways.md#s2smulti) disponíveis no Azure.
* Recursos diferentes podem ser agrupados num [grupos de recursos](../azure-resource-manager/resource-group-overview.md#resource-groups), tornando mais fácil recursos de Olá toomanage como uma unidade. Um grupo de recursos pode conter recursos a partir de várias regiões, desde que os recursos de Olá pertencer toohello mesma subscrição.

### <a name="define-requirements"></a>Definir os requisitos
Utilize perguntas de Olá abaixo como um ponto de partida para o design de rede do Azure.    

1. O que localizações do Azure irão efetuar a utilizar toohost VNets?
2. Necessita de comunicação de tooprovide entre estas localizações do Azure?
3. Necessita de tooprovide comunicação entre o VNet(s) do Azure e o datacenter(s) no local?
4. Quantos infraestrutura como VMs de serviço (IaaS), cloud e dos serviços de funções, efetue de aplicações web que precisa para a sua solução?
5. Precisa que o tráfego de tooisolate com base nos grupos de VMs (servidores de web ou seja, front-end e servidores de base de dados de back-end)?
6. Precisa que o fluxo de tráfego de toocontrol utilizar aplicações virtuais?
7. Fazer a necessidade dos utilizadores diferentes conjuntos de permissões toodifferent recursos do Azure?

### <a name="understand-vnet-and-subnet-properties"></a>Compreender as propriedades de VNet e sub-rede
Recursos de VNet e sub-redes ajudam a definir um limite de segurança para cargas de trabalho em execução no Azure. Uma VNet é caracterizada por uma coleção de espaços de endereços, definida como blocos CIDR.

> [!NOTE]
> Os administradores de rede estiver familiarizados com notação CIDR. Se não estiver familiarizado com CIDR, [saber mais acerca do mesmo](http://whatismyipaddress.com/cidr).
>
>

As VNets conter Olá seguintes propriedades.

| Propriedade | Descrição | Restrições |
| --- | --- | --- |
| **nome** |Nome da VNet |Cadeia de cópia de segurança too80 carateres. Pode conter letras, números, caráter de sublinhado, pontos ou hífenes. Tem de começar com uma letra ou um número. Tem de terminar com uma letra, um número ou um caráter de sublinhado. Pode contém em maiúsculas ou letras minúsculas. |
| **localização** |Localização do Azure (também referida tooas região). |Tem de ser um dos Olá localizações do Azure válidas. |
| **addressSpace** |Coleção de prefixos de endereços que compõem Olá VNet em notação CIDR. |Tem de ser uma matriz de blocos de endereços CIDR válidos, incluindo intervalos de endereços IP públicos. |
| **sub-redes** |Coleção de sub-redes que compõem Olá VNet |consulte a tabela de propriedades de sub-rede Olá abaixo. |
| **dhcpOptions** |Objeto que contém uma propriedade necessária único com o nome **dnsServers**. | |
| **dnsServers** |Matriz de servidores DNS utilizados por Olá VNet. Não se for especificado nenhum servidor, é utilizada a resolução do nome interno do Azure. |Tem de ser uma matriz de segurança de servidores DNS too10, por endereço IP. |

Uma sub-rede é um recurso de subordinados de uma VNet e ajuda a definir segmentos dos espaços de endereços dentro de um bloco CIDR utilizar prefixos de endereços IP. NICs podem ser adicionados toosubnets e tooVMs ligado, fornecer conectividade de várias cargas de trabalho.

Sub-redes contenham Olá seguintes propriedades.

| Propriedade | Descrição | Restrições |
| --- | --- | --- |
| **nome** |Nome da sub-rede |Cadeia de cópia de segurança too80 carateres. Pode conter letras, números, caráter de sublinhado, pontos ou hífenes. Tem de começar com uma letra ou um número. Tem de terminar com uma letra, um número ou um caráter de sublinhado. Pode contém em maiúsculas ou letras minúsculas. |
| **localização** |Localização do Azure (também referida tooas região). |Tem de ser um dos Olá localizações do Azure válidas. |
| **addressPrefix** |Prefixo de endereço único que compõem a sub-rede de Olá em notação CIDR |Tem de ser um bloco CIDR único que faz parte de um dos espaços de endereços da VNet Olá. |
| **networkSecurityGroup** |NSG aplicado toohello sub-rede | |
| **routeTable** |Tabela de rotas aplicadas toohello sub-rede | |
| **ipConfigurations** |Coleção de objetos de configuração de IP utilizados pelo NICs toohello ligado sub-rede | |

### <a name="name-resolution"></a>Resolução de nomes
Por predefinição, utiliza a sua VNet [resolução de nome fornecidos pelo Azure](virtual-networks-name-resolution-for-vms-and-role-instances.md) Olá, nomes de tooresolve dentro Olá VNet e na Internet pública. No entanto, se ligar os seus centros de dados das VNets tooyour no local, terá de tooprovide [o próprio servidor DNS](virtual-networks-name-resolution-for-vms-and-role-instances.md) tooresolve nomes entre as redes.  

### <a name="limits"></a>Limites
Reveja os limites de rede Olá no Olá [Azure limita](../azure-subscription-service-limits.md#networking-limits) tooensure artigo que a estrutura não entra em conflito com qualquer um dos limites de Olá. Alguns limites podem ser aumentados ao abrir um pedido de suporte.

### <a name="role-based-access-control-rbac"></a>Controlo de Acesso Baseado em Funções (RBAC)
Pode utilizar [Azure RBAC](../active-directory/role-based-access-built-in-roles.md) nível de Olá toocontrol de acesso diferentes, os utilizadores pode ter toodifferent recursos no Azure. Dessa forma, que pode segregar trabalho Olá pela sua equipa com base nas suas necessidades.

Preocupações como para as redes virtuais, os utilizadores Olá **contribuinte de rede** função tem controlo total sobre recursos de rede virtual do Azure Resource Manager. Da mesma forma, os utilizadores Olá **clássico contribuinte de rede** função tem controlo total sobre recursos de rede virtual clássica.

> [!NOTE]
> Também pode [criar as suas próprias funções](../active-directory/role-based-access-control-configure.md) tooseparate às suas necessidades administrativas.
>
>

## <a name="design"></a>Design
Quando souber as respostas de Olá toohello perguntas no Olá [planear](#Plan) secção, consulte Olá seguintes antes de definir as suas VNets.

### <a name="number-of-subscriptions-and-vnets"></a>Número de subscrições e as VNets
Deve considerar a criação de várias VNets no Olá os seguintes cenários:

* **As VMs que necessitam de toobe colocada em diferentes localizações do Azure**. As VNets no Azure são regionais. Estes não podem abranger localizações. Motivo precisa de, pelo menos, uma VNet para cada localização do Azure que pretende incluir toohost VMs.
* **Cargas de trabalho que necessitam de toobe completamente isolada entre si**. Pode criar VNets separadas, esse mesmo Olá de utilizar espaços de endereços IP mesmos, tooisolate diferentes cargas de trabalho entre si.

Tenha em atenção que os limites de Olá que consulte acima são por região por subscrição. Isto significa que pode utilizar vários de limite de Olá do tooincrease subscrições de recursos que pode manter no Azure. Pode utilizar uma VPN de site para site ou um circuito do ExpressRoute, tooconnect VNets em subscrições diferentes.

### <a name="subscription-and-vnet-design-patterns"></a>Subscrição e padrões de conceção de VNet
tabela de Olá abaixo mostra alguns padrões de conceção comuns para a utilização de subscrições e as VNets.

| Cenário | Diagrama | Profissionais de TI | Contras |
| --- | --- | --- | --- |
| Subscrição único, duas VNets por aplicação |![Subscrição único](./media/virtual-network-vnet-plan-design-arm/figure1.png) |Toomanage apenas uma subscrição. |Número máximo de VNets por região do Azure. Precisa de mais subscrições depois disso. Olá revisão [Azure limita](../azure-subscription-service-limits.md#networking-limits) artigo para obter detalhes. |
| Uma subscrição por aplicação, duas VNets por aplicação |![Subscrição único](./media/virtual-network-vnet-plan-design-arm/figure2.png) |Utiliza apenas duas VNets por subscrição. |Mais difícil toomanage quando existem demasiadas aplicações. |
| Uma subscrição por unidade de negócio, duas VNets por aplicação. |![Subscrição único](./media/virtual-network-vnet-plan-design-arm/figure3.png) |Balancear entre o número de subscrições e as VNets. |Número máximo de VNets por unidade de negócio (subscrição). Olá revisão [Azure limita](../azure-subscription-service-limits.md#networking-limits) artigo para obter detalhes. |
| Uma subscrição por unidade de negócio, duas VNets por grupo de aplicações. |![Subscrição único](./media/virtual-network-vnet-plan-design-arm/figure4.png) |Balancear entre o número de subscrições e as VNets. |Aplicações tem de ser isoladas através da utilização de sub-redes e NSGs. |

### <a name="number-of-subnets"></a>Número de sub-redes
Deve considerar a várias sub-redes na VNet em Olá os seguintes cenários:

* **Insuficiente endereços IP privados para todas as NICs numa sub-rede**. Se o espaço de endereços da sub-rede não contém endereços IP suficientes para o número de Olá de NICs na sub-rede Olá, terá de toocreate várias sub-redes. Tenha em atenção que o Azure reserva 5 de cada sub-rede que não é possível utilizar a endereços IP privados: Olá primeiro e último endereços dos toobe 3 endereços utilizado internamente (para fins DHCP e DNS) e espaços de endereços de Olá (para o endereço de sub-rede Olá e multicast).
* **Segurança**. Pode utilizar grupos de tooseparate de sub-redes de VMs entre si para cargas de trabalho que têm uma camada multi estrutura e aplicar diferentes [(NSGs) de grupos de segurança de rede](virtual-networks-nsg.md#subnets) para essas sub-redes.
* **Conectividade híbrida**. Pode utilizar gateways de VPN e circuitos ExpressRoute demasiado[ligar](../vpn-gateway/vpn-gateway-about-vpngateways.md#s2smulti) tooone as VNets outro, e tooyour no local center(s) de dados. Gateways de VPN e circuitos ExpressRoute necessitam de uma sub-rede dos seus próprios toobe criado.
* **Aplicações virtuais**. Pode utilizar uma aplicação virtual, tal como uma firewall, o acelerador WAN ou o gateway de VPN uma VNet do Azure. Se o fizer, terá de demasiado[encaminhar o tráfego](virtual-networks-udr-overview.md) toothose aparelhos e isolá-los na sua própria sub-rede.

### <a name="subnet-and-nsg-design-patterns"></a>Sub-rede e padrões de conceção do NSG
tabela de Olá abaixo mostra alguns padrões de conceção comuns para a utilização de sub-redes.

| Cenário | Diagrama | Profissionais de TI | Contras |
| --- | --- | --- | --- |
| Sub-rede única, NSGs por camada de aplicação, por aplicação |![Sub-rede única](./media/virtual-network-vnet-plan-design-arm/figure5.png) |Apenas uma sub-rede toomanage. |Vários NSGs tooisolate de necessário cada aplicação. |
| Uma sub-rede por aplicação, os NSGs por camada da aplicação |![Sub-rede por aplicação](./media/virtual-network-vnet-plan-design-arm/figure6.png) |Menos NSGs toomanage. |Várias sub-redes toomanage. |
| Uma sub-rede por camada de aplicação, os NSGs por aplicação. |![Sub-rede por camada](./media/virtual-network-vnet-plan-design-arm/figure7.png) |Balancear entre o número de sub-redes e NSGs. |Número máximo de NSGs por subscrição. Olá revisão [Azure limita](../azure-subscription-service-limits.md#networking-limits) artigo para obter detalhes. |
| Uma sub-rede por camada de aplicação, por aplicação, os NSGs por sub-rede |![Sub-rede por camada por aplicação](./media/virtual-network-vnet-plan-design-arm/figure8.png) |Possivelmente menor número de NSGs. |Várias sub-redes toomanage. |

## <a name="sample-design"></a>Estrutura de exemplo
aplicação de Olá tooillustrate das informações de Olá neste artigo, considere Olá cenário a seguir.

Funciona para uma empresa que tenha 2 centros de dados na América do Norte e Europa de centros de dados de dois. Identificou 6 cliente diferentes aplicações mantida por 2 unidades empresariais diferentes que pretende que o toomigrate tooAzure como um piloto. arquitetura de básico Olá para aplicações de Olá são os seguintes:

* App1, App2, App3 e App4 são aplicações web alojadas em servidores Linux em execução Ubuntu. Cada aplicação estabelece ligação a servidor de aplicação separado tooa que aloja serviços RESTful em servidores Linux. serviços RESTful Olá ligar a base de dados MySQL de back-end tooa.
* App5 e App6 são aplicações web alojadas em servidores Windows com o Windows Server 2012 R2. Cada aplicação estabelece ligação tooa back-end do SQL Server da base de dados.
* Todas as aplicações estão alojadas atualmente dos centros de dados da empresa Olá na América do Norte.
* os centros de dados no local Olá utilizam espaço de endereços de 10.0.0.0/8 Olá.

É necessário toodesign uma solução de rede virtual que cumpra os requisitos de Olá:

* Cada unidade de negócio não deve ser afetada por consumo de recursos de outras unidades de negócio.
* Deve minimizar o período de Olá de VNets e sub-redes toomake a gestão mais fácil.
* Cada unidade de negócio deve ter um teste/desenvolvimento único VNet utilizado para todas as aplicações.
* Cada aplicação estiver alojada num 2 do Azure data centers diferentes por continente (América do Norte e Europa).
* Cada aplicação é completamente isolada umas das outras.
* Cada aplicação pode ser acedida pelos clientes através de Olá Internet através de HTTP.
* Cada aplicação pode ser acedida por utilizadores toohello ligado centros de dados no local utilizando um túnel encriptado.
* Centros de dados de tooon local de ligação devem utilizar dispositivos VPN existentes.
* Olá grupo de rede da empresa deve ter controlo total sobre a configuração de VNet Olá.
* Os programadores em cada unidade de negócio só devem ser capaz de toodeploy VMs tooexisting sub-redes.
* Todas as aplicações serão migradas conforme forem tooAzure (comparação de precisão e shift).
* as bases de dados de Olá em cada localização devem replicar tooother Azure localizações uma vez por dia.
* Cada aplicação deve utilizar 5 servidores de web de front-end, 2 servidores de aplicações (quando for necessário) e 2 servidores de base de dados.

### <a name="plan"></a>Planear
Deve começar a sua estrutura, planeamento respondendo perguntas Olá Olá [definir requisitos](#Define-requirements) secção conforme mostrado abaixo.

1. O que localizações do Azure irão efetuar a utilizar toohost VNets?

    2 localizações na América do Norte, 2 localizações e na Europa. Escolha os com base na localização física do Olá dos seus centros de dados no local existente. Dessa forma, a ligação a partir do seu tooAzure localizações físicas terá uma melhor latência.
2. Necessita de comunicação de tooprovide entre estas localizações do Azure?

    Sim. Uma vez que as bases de dados de Olá tem de ser replicada tooall localizações.
3. Necessita de tooprovide comunicação entre o VNet(s) do Azure e o center(s) de dados no local?

    Sim. Uma vez que os utilizadores ligados toohello os centros de dados no local tem de ser tooaccess capaz de aplicações de Olá através de um túnel encriptado.
4. Quantas VMs de IaaS necessita para a sua solução?

    200 VMs de IaaS. App1, App2, App3 e App4 requerem 5 servidores web cada, 2 servidores aplicacionais cada e 2 servidores de base de dados. Este é um total de 9 VMs de IaaS por aplicação ou 36 VMs de IaaS. App5 e App6 necessitam de 5 servidores web e 2 servidores de base de dados. Este é um total de 7 VMs de IaaS por aplicação ou 14 VMs de IaaS. Por conseguinte, terá de 50 VMs de IaaS para todas as aplicações em cada região do Azure. Uma vez que precisamos toouse 4 regiões, será 200 VMs de IaaS.

    Também terá de tooprovide servidores DNS em cada VNet ou em seu nome de tooresolve de centros de dados no local entre as VMs de IaaS do Azure e a sua rede no local.
5. Precisa que o tráfego de tooisolate com base nos grupos de VMs (servidores de web ou seja, front-end e servidores de base de dados de back-end)?

    Sim. Cada aplicação deve ser completamente isolada umas das outras e cada camada de aplicações também deve ser isolada.
6. Precisa que o fluxo de tráfego de toocontrol utilizar aplicações virtuais?

    Não. Aplicações virtuais podem ser utilizado tooprovide mais controlam sobre o fluxo de tráfego, incluindo registo mais detalhado de plane de dados.
7. Fazer a necessidade dos utilizadores diferentes conjuntos de permissões toodifferent recursos do Azure?

    Sim. equipa de rede Olá tem controlo total nas definições de rede virtual de Olá, enquanto os programadores só devem ser capaz de toodeploy as respetivas sub-redes de toopre existente para as VMs.

### <a name="design"></a>Design
Deve seguir a estrutura de Olá especificando subscrições, VNets, sub-redes e NSGs. Vamos abordar os NSGs aqui, mas deve Saiba mais sobre [NSGs](virtual-networks-nsg.md) antes de concluir a estrutura.

**Número de subscrições e as VNets**

Olá, os requisitos é toosubscriptions relacionados e as VNets:

* Cada unidade de negócio não deve ser afetada por consumo de recursos de outras unidades de negócio.
* Deve minimizar o período de Olá de VNets e sub-redes.
* Cada unidade de negócio deve ter um teste/desenvolvimento único VNet utilizado para todas as aplicações.
* Cada aplicação estiver alojada num 2 do Azure data centers diferentes por continente (América do Norte e Europa).

Com base nesses requisitos, precisa de uma subscrição para cada unidade de negócio. Dessa forma, consumo de recursos a partir de uma unidade de negócio não contabilizará limites para outras unidades de negócio. E, uma vez que pretende que o número de Olá toominimize de VNets, deve considerar a utilização Olá **uma subscrição por unidade de negócio, duas VNets por grupo de aplicações** padrão, como mostrado abaixo.

![Subscrição único](./media/virtual-network-vnet-plan-design-arm/figure9.png)

Também precisa de espaço de endereços de Olá toospecify para cada VNet. Uma vez que precisa de conectividade entre Olá no local centros de dados e hello regiões do Azure, espaço de endereços de Olá utilizado para as VNets do Azure não é possível clash com a rede no local de Olá e espaço de endereços de Olá utilizado por cada VNet não deve clash com outras VNets existentes. Pode utilizar espaços de endereços de Olá na tabela de Olá abaixo toosatisfy estes requisitos.  

| **Subscrição** | **VNet** | **Região do Azure** | **Espaço de endereços** |
| --- | --- | --- | --- |
| BU1 |ProdBU1US1 |EUA Oeste |172.16.0.0/16 |
| BU1 |ProdBU1US2 |EUA Leste |172.17.0.0/16 |
| BU1 |ProdBU1EU1 |Europa do Norte |172.18.0.0/16 |
| BU1 |ProdBU1EU2 |Europa Ocidental |172.19.0.0/16 |
| BU1 |TestDevBU1 |EUA Oeste |172.20.0.0/16 |
| BU2 |TestDevBU2 |EUA Oeste |172.21.0.0/16 |
| BU2 |ProdBU2US1 |EUA Oeste |172.22.0.0/16 |
| BU2 |ProdBU2US2 |EUA Leste |172.23.0.0/16 |
| BU2 |ProdBU2EU1 |Europa do Norte |172.24.0.0/16 |
| BU2 |ProdBU2EU2 |Europa Ocidental |172.25.0.0/16 |

**Número de sub-redes e NSGs**

Olá, os requisitos é toosubnets relacionados e NSGs:

* Deve minimizar o período de Olá de VNets e sub-redes.
* Cada aplicação é completamente isolada umas das outras.
* Cada aplicação pode ser acedida pelos clientes através de Olá Internet através de HTTP.
* Cada aplicação pode ser acedida por utilizadores toohello ligado centros de dados no local utilizando um túnel encriptado.
* Centros de dados de tooon local de ligação devem utilizar dispositivos VPN existentes.
* as bases de dados de Olá em cada localização devem replicar tooother Azure localizações uma vez por dia.

Com base nesses requisitos, pode utilizar uma sub-rede por camada da aplicação e utilizar NSGs toofilter tráfego por aplicação. Dessa forma, só tem de 3 sub-redes em cada VNet (front-end, a camada de aplicação e a camada de dados) e um NSG por aplicação por sub-rede. Neste caso, deve considerar a utilização Olá **uma sub-rede por camada de aplicação, os NSGs por aplicação** padrão de conceção. figura Olá abaixo mostra a utilização de Olá do padrão de conceção de Olá que representa Olá **ProdBU1US1** VNet.

![Uma sub-rede por camada, um NSG por aplicação por camada](./media/virtual-network-vnet-plan-design-arm/figure11.png)

No entanto, também terá toocreate uma sub-rede adicional para conectividade a VPN Olá entre Olá VNets e seus centros de dados no local. E precisa de espaço de endereços de Olá toospecify para cada sub-rede. figura Olá abaixo mostra uma solução de exemplo para **ProdBU1US1** VNet. Iriam replicar neste cenário para cada VNet. Cada cor representa uma aplicação diferente.

![Exemplo VNet](./media/virtual-network-vnet-plan-design-arm/figure10.png)

**Controlo de acesso**

Olá requisitos seguintes são tooaccess relacionados controlo:

* Olá grupo de rede da empresa deve ter controlo total sobre a configuração de VNet Olá.
* Os programadores em cada unidade de negócio só devem ser capaz de toodeploy VMs tooexisting sub-redes.

Com base nesses requisitos, pode adicionar utilizadores de Olá redes equipa toohello incorporada **contribuinte de rede** função em cada subscrição; e criar uma função personalizada para Olá os programadores de aplicações em cada subscrição dá ao direitos-las tooadd VMs tooexisting sub-redes.

## <a name="next-steps"></a>Passos seguintes
* [Implementar uma rede virtual](virtual-networks-create-vnet-arm-template-click.md) com base no cenário.
* Compreender como demasiado[o balanceamento de carga](../load-balancer/load-balancer-overview.md) VMs de IaaS e [Gerir encaminhamento por várias regiões do Azure](../traffic-manager/traffic-manager-overview.md).
* Saiba mais sobre [NSGs e como tooplan e design](virtual-networks-nsg.md) uma solução NSG.
* Saiba mais sobre o [em vários locais e opções de conectividade de VNet](../vpn-gateway/vpn-gateway-about-vpngateways.md#s2smulti).
