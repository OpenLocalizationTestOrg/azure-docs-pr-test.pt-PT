---
title: "Segurança de rede de aaaAzure | Microsoft Docs"
description: "Saiba mais sobre serviços informáticos baseada na nuvem que incluem uma seleção grande de instâncias de computação e serviços que podem aumentar verticalmente e horizontalmente automaticamente toomeet Olá às necessidades da sua aplicação ou enterprise."
services: security
documentationcenter: na
author: UnifyCloud
manager: swadhwa
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/24/2017
ms.author: TomSh
ms.openlocfilehash: 7dae83bbe338a2727575447583a7fb773527dd59
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-network-security"></a>Segurança de rede do Azure

Sabemos que a segurança está tarefa um na nuvem de Olá e como importante é que encontrará exatas e atempadas informações sobre a segurança do Azure. Uma das Olá melhor motivos toouse do Azure para as suas aplicações e serviços é tootake partido grande matriz do Azure capacidades e ferramentas de segurança. Estas ferramentas e capacidades de ajudam a torná-lo toocreate possíveis soluções de segura em Olá plataforma Azure.

O Microsoft Azure oferece confidencialidade, integridade e disponibilidade dos dados de cliente, permitindo também accountability transparente. toohelp compreender melhor coleção Olá dos controlos de segurança de rede implementado no Microsoft Azure da perspetiva do cliente Olá, este artigo, "Azure" segurança de rede, é escrito tooprovide ver abrangente segurança de rede Olá controlos disponíveis com o Microsoft Azure.

Este documento destina-se tooinform-lo sobre vasta gama de Olá da rede controla que pode configurar a segurança de Olá tooenhance das soluções de Olá que implementar no Azure. Se estiver interessado em que Microsoft does toosecure Olá rede dos recursos de infraestrutura de Olá própria plataforma do Azure, consulte a secção de segurança do Azure Olá Olá [Microsoft Trust Center](https://www.microsoft.com/trustcenter/security/azure-security).

## <a name="azure-platform"></a>Plataforma Azure

Azure é uma plataforma de serviço de nuvem pública que suporta uma seleção abrangente dos sistemas operativos, programação idiomas, estruturas, ferramentas, bases de dados e dispositivos.  Pode ser executado contentores de Linux com a integração do Docker; criar aplicações com JavaScript, Python, .NET, PHP, Java e Node.js; compilação back-ends para iOS, Android e Windows dispositivos. Serviços cloud do Azure suportam Olá mesmas tecnologias milhões de programadores e profissionais de TI já dependem e fidedignidade.

Quando criar ou migrar os recursos de IT para um fornecedor de serviços de nuvem pública, é depender tooprotect de capacidades da organização as suas aplicações e dados com Olá controlos de serviços e Olá fornecem toomanage Olá segurança da sua conta baseado na nuvem ativos.

Infraestrutura do Azure foi concebida de Olá instalações tooapplications para alojar milhões de clientes em simultâneo, e fornece uma base de confiança no qual as empresas podem cumprir os seus requisitos de segurança. Além disso, Azure fornece uma coleção de um vasto conjunto de toocontrol de capacidade de segurança configuráveis opções e Olá-las de modo a que pode personalizar toomeet Olá exclusivo os requisitos de segurança de implementações da sua organização.

## <a name="abstract"></a>Abstrato

Serviços de nuvem pública da Microsoft fornecem serviços de hiper escala e infraestrutura, as capacidades de nível empresarial e muitas opções para conectividade híbrida. Pode escolher tooaccess estes serviços através de Olá Internet ou com o ExpressRoute do Azure, que fornece a conectividade de rede privada. plataforma do Microsoft Azure de Olá permite-lhe tooseamlessly alargar a infraestrutura para nuvem Olá e criar arquiteturas de várias camadas. Além disso, terceiros pode ativar avançadas de capacidades por oferta de serviços de segurança e de aplicações virtuais.

Serviços de rede do Azure maximizem flexibilidade, disponibilidade, resiliência, segurança e integridade por predefinição. Este documento técnico fornece detalhes sobre as funções de rede Olá do Azure e obter informações sobre como os clientes podem utilizar toohelp de funcionalidades de segurança nativa do Azure proteger recursos de informações.

Olá pretendido público para este documento inclui:

- Gestores de técnicos, os administradores de rede e os programadores que estão a procurar soluções de segurança disponíveis e suportadas no Azure.

-   SMEs ou os executivos de processo de empresas que pretendem tooget uma descrição geral de alto nível Olá tecnologias de rede do Azure e serviços que são relevantes em discussões em torno da segurança de rede no Olá nuvem pública do Azure.

## <a name="azure-networking-big-picture"></a>Visão geral de redes do Azure
Microsoft Azure inclui um toosupport de infraestrutura de rede robusta a sua aplicação e os requisitos de conectividade do serviço. Conectividade de rede é possível entre os recursos localizados no Azure, no local e Azure alojadas recursos e tooand de Olá Internet e o Azure.

![Visão geral de redes do Azure](media/azure-network-security/azure-network-security-fig-1.png)

Olá [infraestrutura de rede do Azure](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-networking-guidelines) permite toosecurely ligar recursos do Azure tooeach outros com redes virtuais (VNets). Uma VNet é uma representação da sua própria rede na nuvem de Olá. Uma VNet é um isolamento lógico da Olá em nuvem do Azure rede dedicada tooyour subscrição. Pode ligar redes do VNets tooyour no local.

Suporte do Azure dedicado rede no local do ligação WAN conectividade tooyour e uma rede Virtual do Azure com [ExpressRoute](https://docs.microsoft.com/azure/expressroute/expressroute-introduction). Olá ligação entre o Azure e o seu site utiliza uma ligação dedicada que passam para Olá Internet pública. Se a aplicação do Azure está em execução em vários datacenters, pode utilizar [Traffic Manager do Azure](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-overview) tooroute pedidos de utilizadores inteligentemente entre instâncias da aplicação Olá. Também pode encaminhar tooservices tráfego não em execução no Azure que estejam acessíveis a partir do Olá Internet.

## <a name="enterprise-view-of-azure-networking-components"></a>Vista de Enterprise dos componentes de rede do Azure
O Azure tem muitos componentes de rede que são relevantes toonetwork debates de segurança. Vamos descrever estes componentes de rede e foco segurança Olá emite toothem relacionado.

> [!Note]
> Nem todos os aspetos do funcionamento em rede do Azure são descritos – Vamos discutir apenas os considerado toobe pivotal planear e conceber uma infraestrutura de rede segura em torno dos seus serviços e aplicações que implementar no Azure.

Neste documento, será possível Olá abrange seguir Azure redes capacidades empresariais:

-   Conectividade de rede básica

-   Conectividade híbrida

-   Controlos de segurança

-   Validar a rede

### <a name="basic-network-connectivity"></a>Conectividade de rede básica

Olá [Azure Virtual Network](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview) ativa de serviço toosecurely ligar recursos do Azure tooeach outros com redes virtuais (VNet). Uma VNet é uma representação da sua própria rede na nuvem de Olá. Uma VNet é um isolamento lógico da Olá rede Azure infraestrutura dedicada tooyour subscrição. Também pode ligar VNets tooeach outros e tooyour redes de VPNs de site para site a utilizar no local e dedicado [ligações WAN](https://docs.microsoft.com/azure/expressroute/expressroute-introduction).

![Conectividade de rede básica](media/azure-network-security/azure-network-security-fig-2.png)

Com Olá compreender que utilize servidores de toohost de VMs no Azure, pergunta Olá é como dessas VMs ligam tooa rede. Olá resposta é que as VMs ligam tooan [Azure Virtual Network](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview).

Redes virtuais do Azure são como Olá virtual redes utilizam no local com as suas próprias soluções de plataforma de virtualização, como o Microsoft Hyper-V ou VMware.

#### <a name="intra-vnet-connectivity"></a>Conectividade intra VNet

Pode ligar VNets tooeach outros, ativar recursos ligados tooeither VNet toocommunicate entre si entre VNets. Pode utilizar um ou ambos Olá opções tooconnect VNets tooeach outros os seguintes:

- **Peering:** ativa recursos ligados toodifferent as VNets do Azure dentro Olá mesma localização do Azure toocommunicate entre si. Olá largura de banda e latência em Olá VNet é Olá mesmo como se recursos Olá foram toohello ligada mesma VNet. ler toolearn mais informações sobre peering, [peering de rede Virtual](https://docs.microsoft.com/azure/virtual-network/virtual-network-peering-overview).

 ![Peering](media/azure-network-security/azure-network-security-fig-3.png)

- **Ligação VNet a VNet:** ativa recursos ligados toodifferent VNet do Azure dentro Olá idêntica ou diferentes localizações do Azure. Ao contrário de peering, largura de banda é limitada entre VNets porque o tráfego tem de fluir através de um Gateway de VPN do Azure.

![Ligação VNet a VNet](media/azure-network-security/azure-network-security-fig-4.png)


mais sobre como ligar VNets com uma ligação VNet a VNet, leia Olá toolearn [configurar um artigo de ligação de VNet a VNet](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal?toc=%2fazure%2fvirtual-network%2ftoc.json).

#### <a name="azure-virtual-network-capabilities"></a>Capacidades de rede virtual do Azure:

Como pode ver, uma rede Virtual do Azure fornece as máquinas virtuais tooconnect toohello rede para que estes possam ligar a recursos de rede tooother de forma segura. No entanto, a conectividade básica é início Olá apenas. Olá seguintes capacidades de Olá serviço de rede Virtual do Azure expõem as características de segurança de Olá rede Virtual do Azure:

-   Isolamento

-   Conectividade Internet

-   Conectividade de recursos do Azure

-   Conectividade de VNet

-   Conectividade no local

-   Filtragem de tráfego

-   Encaminhamento

**Isolamento**

As VNets estão [isolado](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview) entre si. Pode criar VNets separadas para o desenvolvimento, teste e produção que utilize Olá mesmo [CIDR](https://en.wikipedia.org/wiki/Classless_Inter-Domain_Routing) blocos de endereços. Por outro lado, pode criar várias VNets que utilizam diferentes blocos de endereços CIDR e ligar redes em conjunto. Pode segmentar uma VNet em várias sub-redes.

O Azure oferece resolução dos nomes internos para VMs e [serviços em nuvem](https://azure.microsoft.com/services/cloud-services/) instâncias de função ligado tooa VNet. Opcionalmente, pode configurar uma VNet toouse os seus próprios servidores DNS, em vez de utilizar a resolução do nome interno do Azure.

Pode implementar várias VNets dentro de cada Azure [subscrição](https://docs.microsoft.com/azure/azure-glossary-cloud-terminology?toc=%2fazure%2fvirtual-network%2ftoc.json) e o Azure [região](https://docs.microsoft.com/azure/azure-glossary-cloud-terminology?toc=%2fazure%2fvirtual-network%2ftoc.json). Cada VNet está isolado de outras VNets. Para cada VNet pode:

-   Especifique um espaço de endereços IP privado personalizado utilizando endereços (RFC 1918) públicos e privados. Azure atribui recursos ligados toohello VNet um endereço IP privado do espaço de endereços de Olá, atribuir.

-   Segmentar Olá VNet num ou mais sub-redes e atribuir uma parte da sub-rede de tooeach de espaço de endereços VNet Olá.

-   Utilize a resolução de nome fornecidos pelo Azure ou especificar que o próprio servidor DNS para utilização pelos recursos ligados tooa VNet. mais informações sobre resolução de nomes em VNets, leia Olá toolearn [a resolução de nomes para VMs e serviços em nuvem](https://docs.microsoft.com/azure/virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances).

**Ligação à Internet**

Todos os [máquinas virtuais do Azure (VM)](https://docs.microsoft.com/azure/virtual-machines/windows/) e instâncias de função de serviços em nuvem tooa ligado VNet ter acesso toohello Internet, por predefinição. Também pode ativar a entrada de aceder a recursos de toospecific, conforme necessário. (VM) e instâncias de função de serviços em nuvem tooa ligado VNet ter acesso toohello Internet, por predefinição. Também pode ativar a entrada de aceder a recursos de toospecific, conforme necessário.

Todos os recursos ligados tooa VNet tem conectividade de saída toohello Internet por predefinição. endereço IP privado Olá do recurso de Olá é o endereço de rede de origem traduzido endereço IP público tooa (realizar o SNAT) por Olá infraestrutura do Azure. Pode alterar a conectividade de predefinição Olá implementando encaminhamento personalizado e filtragem de tráfego. mais informações sobre a ligação à Internet de saída, leia Olá toolearn [Noções sobre ligações de saída no Azure](https://docs.microsoft.com/azure/load-balancer/load-balancer-outbound-connections?toc=%2fazure%2fvirtual-network%2ftoc.json).

toocommunicate tooAzure recursos da Internet sem realizar o SNAT, um recurso deve ser atribuída um endereço IP público Olá Internet ou toocommunicate toohello saída de entrada. mais informações sobre os endereços IP públicos, leia Olá toolearn [endereços IP públicos](https://docs.microsoft.com/azure/virtual-network/virtual-network-public-ip-address).

**Conectividade de recursos do Azure**

[Recursos do Azure](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview) , tais como serviços em nuvem e as VMs podem ser ligado toohello mesma VNet. recursos de Olá podem ligar outro tooeach privada endereços IP, mesmo que se encontrem em sub-redes diferentes. O Azure oferece encaminhamento predefinido entre sub-redes, VNets e redes no local, pelo que não tem tooconfigure e gerir as rotas.

Pode ligar a vários recursos do Azure tooa VNet, tais como máquinas virtuais (VM), Cloud Services, ambientes do App Service e conjuntos de dimensionamento de Máquina Virtual. VMs ligam sub-rede tooa numa VNet através de uma interface de rede (NIC). mais informações sobre NICs, lidos Olá toolearn [interfaces de rede](https://docs.microsoft.com/azure/virtual-network/virtual-network-network-interface).

**Conectividade de VNet**

[As VNets](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview) pode ser ligado tooeach outros, permitir recursos ligados tooany VNet toocommunicate com qualquer recurso no qualquer outra VNet.

Pode ligar VNets tooeach outros, ativar recursos ligados tooeither VNet toocommunicate entre si entre VNets. Pode utilizar um ou ambos Olá opções tooconnect VNets tooeach outros os seguintes:

- **Peering:** ativa recursos ligados toodifferent as VNets do Azure dentro Olá mesma localização do Azure toocommunicate entre si. Olá largura de banda e latência em Olá VNets é Olá, mesmo que se recursos Olá foram toohello ligado VNet.toolearn mesmo mais informações sobre peering, leia Olá [peering de rede Virtual](https://docs.microsoft.com/azure/virtual-network/virtual-network-peering-overview).

- **Ligação VNet a VNet:** ativa recursos ligados toodifferent VNet do Azure dentro Olá idêntica ou diferentes localizações do Azure. Ao contrário de peering, largura de banda é limitada entre VNets porque o tráfego tem de fluir através de um Gateway de VPN do Azure. toolearn mais sobre como ligar VNets com uma ligação VNet a VNet. toolearn ler mais, Olá [configurar uma ligação VNet a VNet](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal?toc=%2fazure%2fvirtual-network%2ftoc.json) .

**Conectividade no local**

As VNets podem ser ligadas demasiado[no local](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview) redes através de ligações de rede privada entre a rede e o Azure ou através de uma ligação de VPN de site a site através de Olá Internet.

Pode ligar-se a sua tooa de rede no local VNet utilizando qualquer combinação dos Olá seguintes opções:

- **Ponto a site rede privada virtual (VPN):** estabelecida entre uma única rede ligada tooyour de PC e Olá VNet. Este tipo de ligação é excelente se de que está a começar com o Azure ou para os programadores, porque necessita de rede do tooyour de alterações existente do pouco ou nenhum. ligação de Olá utiliza a comunicação de tooprovide encriptado de protocolo SSTP Olá Olá Internet entre Olá PC e Olá VNet. a latência de Olá para uma VPN ponto a site é imprevisível, uma vez que o tráfego de Olá atravessa Olá Internet.

- **VPN de site para site:** estabelecida entre o dispositivo VPN e um Gateway de VPN do Azure. Este tipo de ligação permite qualquer recurso no local autorizar tooaccess uma VNet. ligação de Olá é uma VPN IPsec/IKE que fornece comunicações encriptadas através de Olá Internet entre o dispositivo no local e o gateway de VPN do Azure Olá. Latência de Olá para uma ligação site a site é imprevisível, uma vez que o tráfego de Olá atravessa Olá Internet.

- **O ExpressRoute do Azure:** estabelecida entre a rede e o Azure, através de um parceiro do ExpressRoute. Esta ligação é privada. Tráfego atravessar não Olá Internet. Latência de Olá para uma ligação ExpressRoute é previsível, uma vez que o tráfego não atravessar Olá Internet. mais informações sobre todos os Olá ligação opções anteriores, leia Olá toolearn [diagramas de topologia de ligação](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-vpngateways?toc=%2fazure%2fvirtual-network%2ftoc.json).

**Filtragem do tráfego**

Instâncias de função da VM e serviços em nuvem [tráfego de rede](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview) pode ser filtrada entrada e saída por endereço IP de origem e porta, endereço IP de destino e porta e protocolo.

Pode filtrar o tráfego de rede entre as sub-redes utilizando um ou ambos Olá seguintes opções:

- **Rede (NSG) de grupos de segurança:** cada NSG pode conter várias regras de segurança de entrada e saída que lhe permitem tráfego toofilter por endereço IP de origem e de destino, porta e protocolo. Pode aplicar um tooeach NSG NIC numa VM. Também pode aplicar uma sub-rede de toohello NSG um NIC ou outros recursos do Azure, está ligado. mais sobre NSGs, leia Olá toolearn [grupos de segurança de rede](https://docs.microsoft.com/azure/virtual-network/virtual-networks-nsg).

- **Os dispositivos de rede virtuais:** um dispositivo de rede virtual está numa VM a executar o software que executa uma função de rede, como uma firewall. Ver uma lista de NVAs disponíveis no Olá Azure Marketplace. NVAs estão também disponíveis, que fornecem a otimização de WAN e outra rede funções de tráfego. NVAs são normalmente utilizadas com definido pelo utilizador ou as rotas BGP. Também pode utilizar um tráfego de toofilter NVA entre VNets.

**Encaminhamento**

Opcionalmente, pode substituir predefinição do Azure encaminhamento por configurar as seus próprios rotas ou utilizar rotas BGP através de um gateway de rede.

O Azure cria as tabelas de rotas ativar recursos ligados tooany sub-rede qualquer toocommunicate VNet entre si, por predefinição. Pode implementar um ou ambos Olá toooverride opções a seguir Olá rotas predefinidas que Azure cria:

- **Rotas definidas pelo utilizador:** pode criar as tabelas de rotas personalizadas com rotas controlam em que o tráfego é encaminhado toofor cada sub-rede. mais sobre as rotas definidas pelo utilizador, ler Olá toolearn [rotas definidas pelo utilizador](https://docs.microsoft.com/azure/virtual-network/virtual-networks-udr-overview).

- **Rotas BGP:** se ligar a sua rede no local do VNet tooyour através de uma ligação ExpressRoute ou de Gateway de VPN do Azure, pode propagar rotas BGP tooyour VNets.

### <a name="hybrid-internet-connectivity-connect-tooan-on-premises-network"></a>Conectividade de internet híbrida: ligar a rede no local de tooan
Pode ligar-se a sua tooa de rede no local VNet utilizando qualquer combinação dos Olá seguintes opções:

-   Conectividade Internet

-   VPN ponto a site (P2S VPN)

-   VPN de site para Site (S2S VPN)

-   ExpressRoute

#### <a name="internet-connectivity"></a>Conectividade Internet

Como sugere o respetivo nome, a conectividade à Internet faz com que as cargas de trabalho acessível a partir do Olá Internet, fazendo com que expõe tooworkloads pontos finais públicos diferentes que em direto no interior da rede virtual Olá. Estas cargas de trabalho podem ser expostas através de [Balanceador de carga para a Internet](https://docs.microsoft.com/azure/load-balancer/load-balancer-internet-overview) ou simplesmente a atribuir um IP público de endereços toohello VM. Desta forma, torna possível para qualquer caráter no Olá toobe de Internet tooreach capaz de que a máquina virtual, fornecidas uma firewall de anfitrião, [de rede (NSG) de grupos de segurança](https://docs.microsoft.com/azure/virtual-network/virtual-networks-nsg), e [rotas definidas pelo utilizador](https://docs.microsoft.com/azure/virtual-network/virtual-networks-udr-overview) de permitir que toohappen.

Neste cenário, pode expor uma aplicação que necessita de toobe pública toohello Internet e ser capaz de tooconnect tooit de qualquer local, ou a partir de localizações específicas consoante a configuração de Olá das cargas de trabalho.

#### <a name="point-to-site-vpn-or-site-to-site-vpn"></a>VPN ponto a Site ou VPN Site a Site
Estes dois recai num Olá mesma categoria. Ambos os precisam toohave sua VNet um Gateway de VPN e pode ligar tooit utilizando um cliente de VPN para a estação de trabalho como parte da Olá [configuraçãoponto a Site](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal) ou pode configurar no local [dedispositivoVPN](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-vpn-devices) toobe capaz de tooterminate uma VPN de site para site. Desta forma, os dispositivos no local podem ligar tooresources dentro Olá VNet.

Uma configuração ponto a Site (P2S) permite-lhe criar uma ligação segura a partir de uma rede virtual do computador tooa de cliente individuais. Uma P2S é uma ligação VPN através de SSTP (Secure Socket Tunneling Protocol).

![VPN ponto a Site](media/azure-network-security/azure-network-security-fig-5.png)

As ligações ponto a Site são úteis quando pretende tooconnect tooyour VNet a partir de uma localização remota, tal como casa ou de um centro de conferência ou quando tem apenas alguns clientes que necessitam de rede virtual do tooconnect tooa.

As ligações P2S não precisam de nenhum dispositivo VPN ou endereço IP destinado ao público. Estabelecer uma ligação de VPN Olá do computador de cliente Olá. Por conseguinte, P2S não é recomendado forma tooconnect tooAzure caso precisa de uma ligação persistente de vários dispositivos no local e computadores tooyour rede do Azure.

![VPN de Site a site](media/azure-network-security/azure-network-security-fig-6.png)

> [!Note]
> Para obter mais informações sobre ligações ponto a Site, consulte Olá [ponto a Site FA v Q](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-point-to-site-classic-azure-portal).

Uma ligação de gateway VPN de Site a Site é utilizado tooconnect tooan rede virtual do Azure de rede no local através de um túnel VPN IPsec/IKE (IKEv1 ou IKEv2).

Este tipo de ligação requer uma VPN dispositivos localizado no local que tenha um tooit de atribuída de endereço IP público com acesso exterior. Esta ligação demora mais Olá Internet e permite-lhe demasiado "Criar um túnel entre" informações no interior de uma ligação encriptada entre a rede e do Azure. VPN de site a site é uma tecnologia de segura, madura que tenha sido implementada por empresas de todos os tamanhos de decades. Encriptação de túnel é executada com [modo de túnel IPsec](https://technet.microsoft.com/library/cc786385.aspx).

Enquanto VPN site a site é uma tecnologia de fidedigna, fiável e estabelecida, o tráfego de túnel Olá atravessar Olá Internet. Além disso, a largura de banda é relativamente restrita tooa máximo de cerca de 200 Mbps.

Se necessitar de um nível excecional de segurança ou de desempenho para as suas ligações entre locais, recomendamos que utilize o Azure ExpressRoute para a conectividade em vários locais. O ExpressRoute é uma WAN dedicada ligação entre a sua localização no local ou num fornecedor de alojamento do Exchange. Porque se trata de uma ligação de telco, os dados não percorram Olá Internet e, por conseguinte, é toohello não exposta potenciais riscos inerentes em comunicações da Internet.

> [!Note]
> Para obter mais informações sobre gateways de VPN, consulte o artigo [gateway de VPN](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-vpngateways).

#### <a name="dedicated-wan-link"></a>Ligação WAN dedicada
O Microsoft Azure ExpressRoute permite-lhe expandir as suas redes no local para Olá do Azure através de uma ligação privada dedicada facilitada por um fornecedor de conectividade.

As ligações do ExpressRoute não passam Olá Internet pública. Isto permite a toooffer de ligações ExpressRoute mais fiabilidade, velocidades mais rápidas, latências inferiores e uma maior segurança ligações típicas através de Olá Internet.

![ Ligação WAN dedicada](media/azure-network-security/azure-network-security-fig-7.png)

> [!Note]
> Para obter informações sobre como tooconnect sua tooMicrosoft de rede com o ExpressRoute, consulte [modelos de conectividade do ExpressRoute](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-vpngateways) e [descrição geral técnica do ExpressRoute](https://docs.microsoft.com/azure/expressroute/expressroute-introduction).

Como com opções de VPN de site para site Olá, ExpressRoute também permite-lhe tooresources tooconnect que não são necessariamente na VNet apenas um. Na verdade, consoante Olá SKU, pode ligar too10 VNets. Se tiver Olá [suplemento premium](https://docs.microsoft.com/azure/expressroute/expressroute-faqs), ligações tooup too100 VNets são possíveis, dependendo da largura de banda. mais informações sobre quais estes tipos de aspeto de ligações, como, leia toolearn [diagramas de topologia de ligação](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-vpngateways?toc=%2fazure%2fvirtual-network%2ftoc.json).

### <a name="security-controls"></a>Controlos de segurança
Uma rede Virtual do Azure fornece uma rede lógica e segura que está isolada de outras redes virtuais e suporta vários controlos de segurança que utilizam nas redes no local. Os clientes criem as seus próprios estrutura utilizando: sub-redes — poderem utilizar os seus próprios intervalo de endereços IP privado, configurar tabelas de rota, grupos de segurança de rede do controlo de acesso (ACLs) de listas, gateways e aplicações virtuais toorun as respetivas cargas de trabalho na nuvem de Olá.

Olá, são os controlos de segurança que pode utilizar nas suas redes virtuais do Azure:

-   Controlos de acesso de rede

-   Rotas definidas pelo utilizador

-   Dispositivo de segurança de rede

-   Gateway de Aplicação

-   Firewall de aplicação Web do Azure

-   Controlo de disponibilidade de rede

#### <a name="network-access-controls"></a>Controlos de acesso de rede
Enquanto Olá rede Virtual do Azure (VNet) é fundamental para Olá modelo de rede do Azure e fornece isolamento e proteção, Olá [grupos de segurança de rede (NSG)](https://blogs.msdn.microsoft.com/igorpag/2016/05/14/azure-network-security-groups-nsg-best-practices-and-lessons-learned/) são ferramenta principal Olá utilizar tooenforce e controlo de tráfego de rede regras de nível de rede de Olá.

![ Controlos de acesso de rede](media/azure-network-security/azure-network-security-fig-8.png)


Pode controlar o acesso ao que permite ou nega comunicação entre as cargas de trabalho de Olá dentro de uma rede virtual, de sistemas na redes do cliente através de uma conectividade entre instalações, ou direcionar comunicação da Internet.

Diagrama de Olá, VNets e NSGs residirem numa camada específica na pilha de segurança geral do Azure Olá, onde os NSGs, UDR e os dispositivos de rede virtual podem ser utilizado toocreate segurança limites tooprotect Olá implementações de aplicações numa rede de Olá protegido.

Os NSGs utilizam um tráfego de tooevaluate 5 cadeias de identificação (e são utilizados nas regras de Olá que configurar para Olá NSG):

-   [Endereço IP de origem e de destino](https://support.microsoft.com/help/969029/the-functionality-for-source-ip-address-selection-in-windows-server-2008-and-in-windows-vista-differs-from-the-corresponding-functionality-in-earlier-versions-of-windows)

-   [Porta de origem e de destino](https://technet.microsoft.com/library/dd197515)

-   Protocolo: [protocolo de controlo de transmissão (TCP)](https://technet.microsoft.com/library/cc940037.aspx) ou [protocolo de datagrama de utilizador (UDP)](https://technet.microsoft.com/library/cc940034.aspx)

Isto significa que pode controlar o acesso entre uma única VM e um grupo de VMs, ou um único tooanother VM única VM, ou entre sub-redes completos. Novamente, tenha em atenção que este é o pacote de monitorização de estado simple filtragem, inspeção de pacotes não completa. Não há nenhuma validação de protocolo ou IDS de nível de rede ou capacidade IPS de um grupo de segurança de rede.

Um NSG é fornecido com algumas regras incorporadas que deve ter em consideração. Nomeadamente:

-   **Permitir todo o tráfego dentro de uma rede virtual específico:** todas as VMs no Olá a mesma rede Virtual do Azure podem comunicar entre si.

-   **Permitir tooinbound de balanceamento de carga do Azure:** esta regra permite que o tráfego de qualquer endereço de destino de tooany de endereço de origem para o Balanceador de carga do Azure de Olá.

-   **Negar toda a entrada:** esta regra bloqueia todo o tráfego sourcing de Olá Internet que ativou explicitamente.

-   **Permitir que todos os toohello saída tráfego à Internet:** esta regra permite que as VMs tooinitiate ligações toohello Internet. Se não pretender que estas ligações iniciadas, é necessário toocreate tooblock uma regra essas ligações ou impor a imposição do túnel.

#### <a name="system-routes-and-user-defined-routes"></a>Rotas de sistema e as rotas definidas pelo utilizador

Quando adiciona tooa do máquinas virtuais (VMs) de rede virtual (VNet) no Azure, tenha em atenção que Olá VMs são capaz toocommunicate entre si através de rede de Olá, automaticamente. Não é necessário toospecify um gateway, apesar de estarem Olá VMs em sub-redes diferentes.

Olá mesmo se aplica a comunicação de Olá VMs toohello Internet pública e a rede no local de tooyour mesmo quando o proprietário de uma ligação híbrida do Azure tooyour Centro de dados está presente.

![Rotas de sistema](media/azure-network-security/azure-network-security-fig-9.png)

Este fluxo de comunicação é possível porque o Azure utiliza uma série de toodefine de rotas de sistema como flui o tráfego IP. Rotas de sistema controlam o fluxo de Olá de comunicação no Olá os seguintes cenários:

-   A partir do Olá mesma sub-rede.

-   A partir de um tooanother sub-rede numa VNet.

-   A partir de VMs toohello Internet.

-   A partir de um tooanother VNet VNet através de um gateway VPN.

-   A partir de um tooanother de VNet a VNet através de VNet Peering ([encadeamento de serviços](https://docs.microsoft.com/azure/virtual-network/virtual-network-peering-overview)).

-   A partir da rede de local de tooyour VNet através de um gateway VPN.

Muitas empresas têm segurança estrita e as políticas de requisitos de conformidade que exigem a inspeção no local de todos os tooenforce de pacotes de rede específico. O Azure oferece um mecanismo chamado [imposição do túnel](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-forced-tunneling) que encaminha o tráfego de Olá VMs tooon local ao criar uma rota personalizada ou [Border Gateway Protocol (BGP)](https://docs.microsoft.com/windows-server/remote/remote-access/bgp/border-gateway-protocol-bgp) anúncios através do ExpressRoute ou VPN.

Imposição do túnel no Azure está configurado através de rotas definidas pelo utilizador da rede virtual (UDR). Redirecionar o tráfego tooan no local site é expresso como um gateway de VPN do Azure de toohello de rota predefinida.

Olá secção seguinte apresenta uma lista de limitação atual Olá de rotas e tabela de encaminhamento de Olá para uma rede Virtual do Azure:

-   Cada sub-rede da rede virtual tem uma tabela de encaminhamento incorporada, do sistema. tabela de encaminhamento de sistema de Olá tem Olá seguintes três grupos de rotas:

 -  **Rotas de VNet locais:** diretamente toohello destino VMs no Olá mesma rede virtual

 - **Nas rotas local:** toohello VPN gateway do Azure

 -  **Rota predefinida:** toohello diretamente à Internet. Pacotes destinados a toohello endereços IP privados não abrangidos por rotas Olá dois anteriores são ignorados.

-   Com a versão de Olá de rotas definidas pelo utilizador, pode criar um encaminhamento tooadd de tabela uma rota predefinida e, em seguida, associar Olá encaminhamento tabela tooyour VNet sub-rede tooenable forçado túnel nessas sub-redes.

-   É necessário tooset "site predefinido" entre a rede virtual do Olá em vários locais sites locais toohello ligado.

-   Imposição do túnel tem de ser associado a uma VNet com um gateway VPN encaminhamento dinâmico (não um gateway estático).

- ExpressRoute imposição do túnel não está configurada através desta mecanismo, mas em vez disso, é ativado por uma rota predefinida através de Olá BGP de ExpressRoute de publicidade sessões de peering.

> [!Note]
> Para obter mais informações, consulte Olá [documentação do ExpressRoute](https://azure.microsoft.com/documentation/services/expressroute/) para obter mais informações.

#### <a name="network-security-appliances"></a>Aplicações de segurança de rede
Enquanto os grupos de segurança de rede e rotas definidas pelo utilizador podem fornecer medidas de segurança de rede em Olá camadas de rede e o transporte de Olá [modelo OSI](https://en.wikipedia.org/wiki/OSI_model), vão toobe situações em que pretende ou precisa tooenable segurança de níveis superiores de pilha de rede Olá. Estas situações, recomendamos que implemente aplicações de segurança de rede virtual fornecidas pelo Azure parceiros.

![Aplicações de segurança de rede](./media/azure-network-security/azure-network-security-fig-10.png)

Aplicações de segurança de rede do Azure melhorar a segurança de VNet e funções de rede e estão disponível de vários fornecedores através de Olá [Azure Marketplace](https://azuremarketplace.microsoft.com). Estas aparelhos virtuais segurança podem ser implementado tooprovide:

-   Firewalls elevadas

-   Prevenção de intrusões

-   Deteção de intrusão

-   Firewalls de aplicação Web (WAFs)

-   Otimização de WAN

-   Encaminhamento

-   Balanceamento de carga

-   VPN

-   Gestão de certificados

-   Active Directory

-   Autenticação multifator

#### <a name="application-gateway"></a>Gateway de aplicação

[Gateway de aplicação do Microsoft Azure](https://docs.microsoft.com/azure/application-gateway/application-gateway-introduction) é uma aplicação virtual dedicada que fornece um controlador de entrega de aplicações (ADC) como um serviço.

 ![Gateway de Aplicação](./media/azure-network-security/azure-network-security-fig-11.png)

Gateway de aplicação permite-lhe toooptimize web farm desempenho e disponibilidade ao descarregar da CPU que consomem muita SSL terminação toohello gateway de aplicação (-descarga de SSL). Também fornece outras funcionalidades de encaminhamento de camada 7, incluindo:

-   Round robin distribuição de tráfego de entrada

-   Afinidade com base no cookie de sessão

-   URL com base no caminho de encaminhamento

-   Capacidade toohost vários sites por trás de um único Gateway de aplicação


A [firewall de aplicações web (WAF)](https://docs.microsoft.com/azure/application-gateway/application-gateway-web-application-firewall-overview) também é fornecido como parte do gateway de aplicação Olá. Isto fornece proteção tooweb aplicações comuns vulnerabilidades web e exploits. Gateway de aplicação pode ser configurado como um Internet com o gateway, interna apenas gateway ou uma combinação de ambos.

Gateway de aplicação WAF pode ser executado no modo de deteção ou prevenção. É um caso de utilização comuns para os administradores toorun no tráfego tooobserve de modo de deteção para padrões maliciosos. Depois de exploits potenciais são detetadas, ativar o modo de tooprevention bloqueia o tráfego de entrada suspeito.

 ![Gateway de Aplicação](./media/azure-network-security/azure-network-security-fig-12.png)

Além disso, Gateway de aplicação WAF ajuda-o a monitorizar aplicações web contra ataques em cadeia utilizando um registo de WAF em tempo real que estão integrados [Azure Monitor](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview) e [Centro de segurança do Azure](https://azure.microsoft.com/services/security-center/) tootrack WAF alertas e monitorizar facilmente as tendências.

Olá JSON formatado registo passa diretamente a conta de armazenamento do cliente de toohello. Tem controlo total sobre estes registos e pode aplicar as suas políticas de retenção.

Também pode incorporar estes registos no seu sistema de análise utilizando [a integração de registo do Azure](https://aka.ms/AzLog). Registos de WAF também são integrados com [Operations Management Suite (OMS)](https://www.microsoft.com/cloud-platform/operations-management-suite) pelo que pode utilizar a análise de registos do OMS tooexecute sofisticados consultas detalhadas.

#### <a name="azure-web-application-firewall-waf"></a>Firewall de aplicação web do Azure (WAF)

As aplicações Web são cada vez mais destinos de ataques maliciosos que explora vulnerabilidades conhecidas comuns, tais como a injeção de SQL, ataques de scripts entre sites e outros ataques que aparecem no Olá [10 de principais OWASP](https://www.owasp.org/index.php/Category:OWASP_Top_Ten_Project). Impedir essas exploits na aplicação Olá requer manutenção rigorosas, monitorização em várias camadas de topologia de aplicação Olá e aplicação de patches.

 ![Firewall de aplicação Web do Azure (WAF)](./media/azure-network-security/azure-network-security-fig-13.png)

Um centralizada [firewall de aplicações web (WAF)](https://docs.microsoft.com/azure/application-gateway/application-gateway-web-application-firewall-overview) pode proteger contra ataques da web e simplifica a gestão de segurança sem necessidade de alterações de aplicação.

Uma solução de WAF também possam reagir a ameaça de segurança de tooa mais rápida por uma vulnerabilidade conhecida numa localização central versus proteger cada uma das aplicações web individuais de aplicação de patches. Gateways de aplicação existentes podem ser facilmente gateway de aplicação de firewall ativada de aplicação web tooa convertido.

#### <a name="network-availability-controls"></a>Controlos de disponibilidade de rede

Existem tráfego de rede diferentes opções toodistribute utilizar o Microsoft Azure. Estas opções funcionam de forma diferente entre si, tendo um conjunto de funcionalidades diferente e suportando diferentes cenários. Podem todos ser utilizados em isolamento ou em conjunto.

Seguintes são Olá controlos de disponibilidade de rede:

-   Azure Load Balancer

-   Gateway de Aplicação

-   Gestor de Tráfego

**Balanceador de carga do Azure**

Fornece tooyour aplicações de elevado desempenho de disponibilidade e rede. É um balanceador de carga de camada 4 (TCP, UDP) que distribui o tráfego de entrada entre instâncias de bom estado de funcionamento dos serviços definidos um conjunto com balanceamento de carga.

 ![Azure Load Balancer](media/azure-network-security/azure-network-security-fig-14.png)


Balanceador de carga do Azure pode ser configurado para:

-   Carregar saldo entradas Internet tráfego toovirtual máquinas. Esta configuração é conhecida como [balanceamento de carga para a Internet](https://docs.microsoft.com/azure/load-balancer/load-balancer-internet-overview).

-   Tráfego de balanceamento de carga entre máquinas virtuais numa rede virtual, entre as máquinas virtuais nos serviços em nuvem ou entre computadores no local e as máquinas virtuais numa rede virtual em vários locais. Esta configuração é conhecida como [balanceamento de carga interna](https://docs.microsoft.com/azure/load-balancer/load-balancer-internal-overview).

-   Reencaminhar tráfego externo tooa máquina virtual específica.

Todos os recursos na nuvem de Olá tem um toobe de endereço IP público acessível a partir do Olá Internet. Olá a infraestrutura de nuvem no Azure utiliza endereços não encaminháveis internos de IP para os respetivos recursos. Azure utiliza a tradução de endereços de rede (NAT) com pública IP endereços toocommunicate toohello Internet.

 **Gateway de aplicação**

 Gateway de aplicação funciona na camada de aplicação Olá (camada 7 na pilha de referência do Olá OSI rede). Atua como um serviço de proxy inverso, terminar a ligação de cliente Olá e pedidos de reencaminhamento pontos finais de tooback-end.

 **Gestor de tráfego**

Gestor de tráfego do Microsoft Azure permite-lhe distribuição de Olá toocontrol tráfego do utilizador para pontos finais do serviço em datacenters diferentes. Pontos finais de serviço suportados pelo Gestor de tráfego incluem as VMs do Azure, as aplicações Web e serviços em nuvem. Também pode utilizar o Gestor de Tráfego com pontos finais externos, não pertencentes ao Azure.

Gestor de tráfego utiliza Olá sistema de nome de domínio (DNS) pedidos de cliente toodirect toohello endpoint mais adequado, com base num [método de encaminhamento de tráfego](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-routing-methods) e Olá estado de funcionamento dos pontos finais de Olá. Gestor de tráfego fornece um período de encaminhamento de tráfego métodos toosuit diferente da aplicação necessidades, o estado de funcionamento do ponto final [monitorização](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-monitoring)e ativação pós-falha automática. Gestor de tráfego é resiliente toofailure, incluindo a falha de Olá de uma região do Azure completa.

Traffic Manager do Azure permite-lhe toocontrol distribuição Olá tráfego entre pontos finais da sua aplicação. Um ponto final é qualquer serviço de acesso à Internet alojada dentro ou fora do Azure.

Gestor de tráfego proporciona duas vantagens chave:

-   Distribuição de tráfego de acordo com tooone de vários [métodos de encaminhamento de tráfego](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-routing-methods).

-   [Monitorização contínua de estado de funcionamento do ponto final](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-monitoring) e ativação pós-falha automática quando não conseguem pontos finais.

Quando um cliente tenta tooconnect tooa serviço, deve resolver primeiro o nome DNS de Olá do endereço IP do Olá serviço tooan. Olá estabelece ligação, em seguida, serviço de Olá de tooaccess de endereço IP toothat. Pontos finais com base nas regras de Olá do método de encaminhamento de tráfego de Olá de serviço do Gestor de tráfego utiliza DNS toodirect clientes toospecific. Os clientes ligam diretamente endpoint toohello selecionado. Gestor de tráfego não é um proxy ou de um gateway. Gestor de tráfego não consegue ver o tráfego de Olá passar entre Olá cliente e o serviço de Olá.

### <a name="azure-network-validation"></a>Validação de rede do Azure

Validação de rede do Azure é tooensure Olá rede do Azure está a funcionar conforme está configurado e pode ser efetuada a validação Olá serviços e funcionalidades disponíveis toomonitor Olá rede a utilizar. Com o observador de rede do Azure, pode aceder a um plethora de registo e diagnóstico capacidades que permitem com insights toounderstand o estado de funcionamento e desempenho da rede. Estas funcionalidades estão acessíveis através do Portal, Power Shell, CLI, Rest API e SDK.

Segurança operacionais do Azure refere-se os serviços de toohello, controlos e toousers disponíveis funcionalidades para proteger os seus dados, aplicações e outros recursos no Microsoft Azure. Segurança operacionais do Azure é construída numa estrutura que incorpora o conhecimento de Olá adquirido através de uma várias funcionalidades que são exclusivo tooMicrosoft, incluindo Olá Microsoft Security Development Lifecycle (SDL), Olá Centre de resposta de segurança do Microsoft programa e deteção profunda de Olá informático segurança das ameaças.

-   [Azure Operations Management Suite](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview)

-   [Centro de Segurança do Azure](https://docs.microsoft.com/azure/security-center/security-center-intro)

-   [Azure Monitor](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview)

-   [Observador de rede do Azure](https://docs.microsoft.com/azure/network-watcher/network-watcher-monitoring-overview)

-   [Análise de armazenamento do Azure](https://docs.microsoft.com/rest/api/storageservices/fileservices/storage-analytics)

-   Azure Resource Manager

#### <a name="azure-resource-manager"></a>Gestor de recursos do Azure

pessoas Olá e processos que operam o Microsoft Azure são talvez Olá funcionalidade de segurança mais importante da plataforma de Olá. Esta secção descreve as funcionalidades de infraestrutura do global datacenter da Microsoft que ajudam a melhorar e manter a segurança, continuidade e privacidade.

infraestrutura de Olá para a sua aplicação, normalmente, é composta por vários componentes, como uma máquina virtual, conta de armazenamento e rede virtual, ou uma aplicação web, base de dados, servidor de base de dados e serviços de terceiros. Não vê estes componentes como entidades separadas. Em vez disso, vê-os como partes relacionadas e interdependentes de uma única entidade. Pretende toodeploy, gerir e monitorizá-los como um grupo. O Azure Resource Manager permite-lhe toowork com recursos de Olá na sua solução como um grupo.

Pode implementar, atualizar ou eliminar todos os recursos de Olá para a sua solução numa operação única e coordenada. Utiliza um modelo para a implementação e esse modelo pode funcionar para ambientes diferentes, como de teste e produção. O Resource Manager fornece segurança, auditoria e etiquetagem funcionalidades toohelp gerir os recursos após a implementação.

**vantagens de Olá da utilização do Resource Manager**

O Resource Manager oferece várias vantagens:

-   Pode implementar, gerir e monitorizar todos os recursos de Olá para a sua solução como um grupo, em vez de os processar individualmente.

-   Pode implementar a solução durante todo o ciclo de vida de desenvolvimento de Olá repetidamente e tem confiança em como os recursos são implementados num estado consistente.

-   Pode gerir a sua infraestrutura através de modelos declarativos em vez de scripts.

-   Pode definir as dependências de Olá entre os recursos, para que sejam implementados na ordem correta Olá.

-   Pode aplicar serviços de tooall de controlo de acesso no seu grupo de recursos porque o controlo de acesso baseado em funções (RBAC) está integrado de forma nativa na plataforma de gestão de Olá.

-   Pode aplicar etiquetas tooresources toologically organizar todos os recursos de Olá na sua subscrição.

-   Pode clarificar a faturação da sua organização ao visualizar os custos de um grupo de recursos que partilha a etiqueta.

> [!Note]
> O Resource Manager fornece uma nova toodeploy de forma e gerir as suas soluções. Se utilizou Olá modelo de implementação anterior e pretende toolearn sobre as alterações de Olá, consulte [Gestor de recursos de compreender implementação clássica e](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-deployment-model).

## <a name="azure-network-logging-and-monitoring"></a>Monitorização e de registo de rede do Azure

Azure oferece muitas ferramentas toomonitor, evitar, detetar e responder a eventos de segurança toonetwork. Alguns dos Olá mais poderosa ferramentas disponíveis tooyou nesta área incluem:

-   Observador de Rede

-   Monitorização ao nível da rede recursos

-   Log Analytics

### <a name="network-watcher"></a>Observador de rede

[Observador de rede](https://docs.microsoft.com/azure/network-watcher/network-watcher-monitoring-overview) -baseada em cenários de monitorização é fornecido com funcionalidades de Olá do observador de rede. Este serviço inclui a captura de pacotes, o salto seguinte, o fluxo IP verificar, a vista de grupo de segurança, os registos de fluxo NSG. A monitorização ao nível do cenário fornece uma vista de tooend final dos recursos de rede em contraste tooindividual recursos a monitorização da rede.

 ![Observador de Rede](./media/azure-network-security/azure-network-security-fig-15.png)

Observador de rede é um serviço regional que permite toomonitor e diagnosticar condições a um nível de cenário rede, para e do Azure. Diagnóstico de rede e ferramentas de visualização disponíveis com o observador de rede ajudam-na compreender, diagnosticar e obter a rede de tooyour insights no Azure.

Observador de rede tem atualmente Olá seguintes capacidades:

#### <a name="topology"></a>Topologia

[Topologia](https://docs.microsoft.com/azure/network-watcher/network-watcher-topology-overview) devolve um gráfico dos recursos de rede numa rede virtual. gráfico de Olá ilustra interconnection Olá entre Olá recursos toorepresent Olá final tooend conectividade da rede. No portal de Olá, topologia devolve os objetos de recurso de Olá de acordo com a base de rede virtual. relações de Olá estão representadas por linhas entre os recursos de Olá fora da região de observador de rede Olá, mesmo que no recurso de Olá grupo não será apresentado. recursos de Olá devolvidos na vista de portal Olá são um subconjunto dos componentes de rede Olá são graphed. toosee Olá obter uma lista completa dos recursos de rede, pode utilizar [PowerShell](https://docs.microsoft.com/azure/network-watcher/network-watcher-topology-powershell) ou [REST](https://docs.microsoft.com/azure/network-watcher/network-watcher-topology-rest).

Como são devolvidos recursos ligação Olá entre eles são modelados em duas relações.

- **Contenção** -rede Virtual contém uma sub-rede que contém uma NIC.

- **Associados** -A NIC está associado uma VM.

#### <a name="variable-packet-capture"></a>Captura de pacotes variável

Observador de rede [captura de pacotes variável](https://docs.microsoft.com/azure/network-watcher/network-watcher-packet-capture-overview) permite-lhe toocreate pacote captura sessões tootrack tráfego tooand de uma máquina virtual. Captura de pacotes ajuda anomalias de rede toodiagnose ambas de forma reativa e proactivity. Outras utilizações incluem a recolha de estatísticas de rede, obtenha informações sobre intrusions de rede, o servidor de cliente toodebug comunicações e muito mais.

Captura de pacotes é uma extensão de máquina virtual que esteja iniciada remotamente através do observador de rede. Esta capacidade facilita o fardo de Olá da execução de uma captura de pacotes manualmente na máquina virtual Olá assim o desejar, que poupa tempo importante. Captura de pacotes pode ser acionada através do portal de Olá, do PowerShell, CLI ou REST API. Um exemplo de como pode ser acionada captura de pacotes é com alertas de Máquina Virtual.

#### <a name="ip-flow-verify"></a>Certifique-se de fluxo IP

[Certifique-se de fluxos IP](https://docs.microsoft.com/azure/network-watcher/network-watcher-ip-flow-verify-overview) verifica se um pacote é permitido ou negado tooor de uma máquina virtual com base nas informações de 5 cadeias de identificação. Esta informação é constituído por direção, protocolo, local IP, remoto IP, porta local e porta remota. Se pacotes hello é negado por um grupo de segurança, é devolvido o nome de Olá da regra Olá negado pacotes hello de. Enquanto qualquer IP de origem ou de destino pode ser selecionado, esta funcionalidade ajuda os administradores Diagnostique rapidamente problemas de conectividade do ou toohello internet e da ou toohello num ambiente no local.

IP fluxos verificar destina-se uma interface de rede de uma máquina virtual. Fluxo de tráfego, em seguida, é verificado com base nas definições de Olá configurado tooor dessa interface de rede. Esta funcionalidade é útil para confirmar se uma regra num grupo de segurança de rede está a bloquear tooor de tráfego de entrada ou saída de uma máquina virtual.

#### <a name="next-hop"></a>Próximo salto

Determina Olá [próximo salto](https://docs.microsoft.com/azure/network-watcher/network-watcher-next-hop-overview) para os pacotes que está a ser encaminhados no Olá recursos de infraestrutura de rede de Azure, permitir toodiagnose qualquer configurada incorretamente rotas definidas pelo utilizador. Tráfego de uma VM é enviado destino tooa com base nas rotas efetivas Olá associadas um NIC. Salto seguinte obtém o tipo de salto seguinte Olá e endereço IP de um pacote de uma máquina virtual específica e a NIC. Isto ajuda a toodetermine se hello pacotes está a ser toohello direcionados destino ou está a ser preto de tráfego de Olá holed.

Também o salto seguinte devolve tabela de rotas Olá associada de salto seguinte Olá. Ao consultar um salto seguinte se rota Olá está definida como uma rota definida pelo utilizador, será devolvida esse rota. Caso contrário, o próximo salto devolve "Rota de sistema".

#### <a name="security-group-view"></a>vista do grupo de segurança

Obtém as regras de segurança eficaz e aplicados Olá que são aplicadas numa VM. Grupos de segurança de rede estão associados a um nível de sub-rede ou um nível de NIC. Quando associados a um nível de sub-rede, aplica-se as instâncias VM de Olá tooall na sub-rede Olá. Rede [vista do grupo de segurança](https://docs.microsoft.com/azure/network-watcher/network-watcher-security-group-view-overview) devolve todos os NSGs Olá configurado e regras que estão associadas a um nível NIC e a sub-rede para uma máquina virtual que fornecem informações sobre a configuração de Olá. Além disso, as regras de segurança eficaz Olá são devolvidas para cada um dos Olá NICs numa VM. Vista de grupo de segurança de rede a utilizar, pode avaliar uma VM para vulnerabilidades de rede, tais como portas abertas. Também pode validar se o grupo de segurança de rede está a funcionar conforme esperado com base num [comparação entre Olá configurado e Olá regras de segurança eficaz](https://docs.microsoft.com/azure/network-watcher/network-watcher-nsg-auditing-powershell).

#### <a name="nsg-flow-logging"></a>Registo de fluxo do NSG

 Registos de fluxo para grupos de segurança de rede permitem-lhe toocapture registos tootraffic relacionados que é permitido ou negado por regras de segurança de Olá no grupo de Olá. fluxo de Olá é definido por uma informação de 5 cadeias de identificação – IP de origem, IP de destino, porta de origem, porta de destino e protocolo.

[Os registos de fluxo do grupo de segurança de rede](https://docs.microsoft.com/azure/network-watcher/network-watcher-nsg-flow-logging-overview) são uma funcionalidade do observador de rede que permite-lhe tooview informações sobre o tráfego IP de entrada e de saída através de um grupo de segurança de rede.

#### <a name="virtual-network-gateway-and-connection-troubleshooting"></a>Gateway de rede virtual e a resolução de problemas de ligação

Observador de rede oferece muitas funcionalidades no que respeita toounderstanding os recursos de rede no Azure. Uma dessas funcionalidades é recursos de resolução de problemas. [Resolução de problemas de recursos](https://docs.microsoft.com/azure/network-watcher/network-watcher-troubleshoot-manage-rest) pode ser chamada por PowerShell, a CLI ou a REST API. Quando chamado, o observador de rede inspeciona o estado de funcionamento de Olá de um gateway de rede Virtual ou uma ligação e devolve conclusões.

Esta secção leva-o através de tarefas de gestão diferentes Olá que estão atualmente disponíveis para a resolução de problemas de recursos.

-   [Resolver problemas relacionados com um gateway de rede Virtual](https://docs.microsoft.com/azure/network-watcher/network-watcher-troubleshoot-manage-rest)

-   [Resolver problemas de uma ligação](https://docs.microsoft.com/azure/network-watcher/network-watcher-troubleshoot-manage-rest)

#### <a name="network-subscription-limits"></a>Limites de subscrição de rede

[Limites de subscrição de rede](https://docs.microsoft.com/azure/network-watcher/network-watcher-monitoring-overview) lhe fornecer os detalhes de utilização de Olá de cada um dos recursos de rede Olá numa subscrição numa região contra o número máximo de Olá de recursos disponíveis.

#### <a name="configuring-diagnostics-log"></a>Configuração de diagnósticos de registo

Observador de rede fornece um [os registos de diagnóstico](https://docs.microsoft.com/azure/network-watcher/network-watcher-monitoring-overview) vista. Esta vista contém todos os recursos de rede que suportam o registo de diagnóstico. Desta vista, pode ativar e desativar os recursos de rede rápida e convenientemente.

### <a name="network-resource-level-monitoring"></a>Monitorização ao nível da rede recursos

Olá seguintes funcionalidades está disponível para monitorização de nível de recursos:

#### <a name="audit-log"></a>Registo de auditoria

Operações efetuadas como parte da configuração de Olá de redes são registadas. Estes registos de auditoria é essencial tooestablish compliances vários. Estes registos podem ser visualizados no Olá portal do Azure ou obtidos através de ferramentas da Microsoft, tais como o Power BI ou ferramentas de terceiros. Os registos de auditoria estão disponíveis através do portal de Olá, do PowerShell, CLI e Rest API.

> [!Note]
> Para obter mais informações sobre os registos de auditoria, consulte [auditar operações com o Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-audit).
Os registos de auditoria estão disponíveis para operações efetuadas em todos os recursos de rede.


#### <a name="metrics"></a>Métricas

As métricas são medidas de desempenho e contadores recolhidos durante um período. Métricas estão atualmente disponíveis para o Gateway de aplicação. Métricas podem ser alertas tootrigger utilizados com base num limiar. Gateway de aplicação do Azure por predefinição monitoriza Olá estado de funcionamento de todos os recursos no seu conjunto de back-end e remove automaticamente qualquer recurso considerado em mau estado de funcionamento do conjunto de Olá. Gateway de aplicação continua instâncias mau estado de funcionamento do toomonitor Olá e adiciona-fazer uma cópia toohello bom conjunto de back-end assim que ficarem disponíveis e as sondas toohealth de responder. Gateway de aplicação envia Olá sondas de estado de funcionamento com Olá mesma porta que está definida nas definições de HTTP de back-end Olá. Esta configuração assegura que sonda Olá consiste em testar Olá a mesma porta que os clientes estariam a utilizar back-end do tooconnect toohello.

> [!Note]
> Consulte [diagnóstico do Gateway de aplicação](https://docs.microsoft.com/azure/application-gateway/application-gateway-probe-overview) tooview como métricas podem ser utilizados toocreate alertas.

#### <a name="diagnostic-logs"></a>Registos de diagnósticos

Eventos periódicos e spontaneous são criados pelos recursos de rede e registados em contas do storage, enviadas tooan Hub de eventos ou análise de registos. Estes registos fornecem informações de estado de funcionamento de Olá de um recurso. Estes registos podem ser visualizados no ferramentas como o Power BI e análise de registos. toolearn como registos de diagnóstico tooview, visite [Log Analytics](https://docs.microsoft.com/azure/log-analytics/log-analytics-azure-networking-analytics).

Os registos de diagnóstico estão disponíveis para [Balanceador de carga](https://docs.microsoft.com/azure/load-balancer/load-balancer-monitor-log), [grupos de segurança de rede](https://docs.microsoft.com/azure/virtual-network/virtual-network-nsg-manage-log), rotas, e [Gateway de aplicação](https://docs.microsoft.com/azure/application-gateway/application-gateway-diagnostics).

Observador de rede fornece que um diagnóstico os registos de vista. Esta vista contém todos os recursos de rede que suportam o registo de diagnóstico. Desta vista, pode ativar e desativar os recursos de rede rápida e convenientemente.

### <a name="log-analytics"></a>Log analytics

[Análise de registo](https://docs.microsoft.com/azure/log-analytics/log-analytics-overview) é um serviço no [Operations Management Suite (OMS)](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview) que monitoriza o toomaintain de ambientes de nuvem e no local, disponibilidade e o desempenho. Recolhe dados gerados pelos recursos nos seus ambientes de nuvem e no local e de outro análise de tooprovide ferramentas monitorização em várias origens.

Análise de registos oferece Olá seguintes soluções para monitorização as redes:

-   Monitor de desempenho de rede (NPM)

-   Análise de Gateway de aplicação do Azure

-   Análise de grupo de segurança de rede do Azure

#### <a name="network-performance-monitor-npm"></a>Monitor de desempenho de rede (NPM)
Olá [Monitor de desempenho de rede](https://docs.microsoft.com/azure/log-analytics/log-analytics-network-performance-monitor) solução de gestão é uma solução que monitoriza o estado de funcionamento de Olá, disponibilidade e acessibilidade de redes de monitorização de rede.

É utilizado toomonitor conectividade entre:

-   Nuvem pública e no local

-   Os centros de dados e localizações de utilizador (sucursais)

-   Sub-redes alojar várias camadas de uma aplicação de várias camadas.


#### <a name="azure-application-gateway-analytics-in-log-analytics"></a>Análise de gateway de aplicação do Azure na análise de registos

Olá seguintes os registos é suportada para Gateways de aplicação:

-   ApplicationGatewayAccessLog

-   ApplicationGatewayPerformanceLog

-   ApplicationGatewayFirewallLog

Olá métricas a seguir é suportada para Gateways de aplicação:

-   débito de 5 minutos

#### <a name="azure-network-security-group-analytics-in-log-analytics"></a>Análise de grupo de segurança de rede do Azure na análise de registos

Olá seguintes registos são suportados para [grupos de segurança de rede](https://docs.microsoft.com/azure/virtual-network/virtual-network-nsg-manage-log):

- **NetworkSecurityGroupEvent:** contém entradas para o NSG, as regras são aplicadas tooVMs e funções de instância com base no endereço MAC. Estado Olá para estas regras é recolhido a cada 60 segundos.

- **NetworkSecurityGroupRuleCounter:** contém entradas quantas vezes cada NSG regra é aplicada toodeny ou permitir o tráfego.

## <a name="next-steps"></a>Passos seguintes
Saber mais sobre a segurança ao ler alguns dos nossos tópicos de segurança aprofundados:

-   [Análise de registos para grupos de segurança de rede (NSGs)](https://docs.microsoft.com/azure/virtual-network/virtual-network-nsg-manage-log)

-   [Rede inovações interrupção de nuvem de Olá essa unidade](https://azure.microsoft.com/blog/networking-innovations-that-drive-the-cloud-disruption/)

-   [SONiC: Olá redes de software de comutador que for ligado Olá nuvem Global da Microsoft](https://azure.microsoft.com/blog/sonic-the-networking-switch-software-that-powers-the-microsoft-global-cloud/)

-   [Como Microsoft baseia-se a rede rápida e fiável global](https://azure.microsoft.com/blog/how-microsoft-builds-its-fast-and-reliable-global-network/)

-   [Iluminação da cópia de segurança inovação de rede](https://azure.microsoft.com/blog/lighting-up-network-innovation/)
