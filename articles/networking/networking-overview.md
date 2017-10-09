---
title: redes aaaAzure | Microsoft Docs
description: "Saiba mais sobre os serviços de rede do Azure e capacidades."
services: networking
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
ms.date: 04/19/2017
ms.author: jdial
ms.openlocfilehash: 18945d139427f2e65138c0fd223e663fa46e9211
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-networking"></a>Redes do Azure

O Azure oferece uma variedade de capacidades de rede que podem ser utilizadas em conjunto ou separadamente. Clique em qualquer um dos Olá toolearn principais capacidades mais sobre os mesmos os seguintes:
- [Conectividade entre os recursos do Azure](#connectivity): recursos Azure ligar em conjunto numa rede virtual privada, segura na nuvem de Olá.
- [Conectividade Internet](#internet-connectivity): comunicar tooand a partir dos recursos do Azure através de Olá Internet.
- [No local conectividade](#on-premises-connectivity): ligar um recursos de tooAzure de rede no local através de uma rede privada virtual (VPN) através de Olá Internet ou através de uma ligação dedicada tooAzure.
- [Direção do tráfego e balanceamento de carga](#load-balancing): Olá, tooservers de tráfego de balanceamento de carga na mesma localização e o tráfego direta tooservers em diferentes localizações.
- [Segurança](#security): filtrar o tráfego de rede entre sub-redes da rede ou de máquinas virtuais individuais (VM).
- [Encaminhamento](#routing): utilizar o encaminhamento predefinido ou controlar totalmente o encaminhamento entre os recursos do Azure e no local.
- [Capacidade de gestão](#manageability): monitorizar e gerir os recursos de rede do Azure.
- [Ferramentas de implementação e configuração](#tools): utilizar um portal baseado na web ou ferramentas de linha de comandos entre plataformas toodeploy e configurar recursos de rede.

## <a name="Connectivity"></a>Conectividade entre os recursos do Azure

Recursos do Azure como máquinas virtuais, Cloud Services, conjuntos de dimensionamento de máquinas virtuais e ambientes do App Service do Azure podem comunicar em privado entre si através de uma rede Virtual do Azure (VNet). Uma VNet é um isolamento lógico da Olá em nuvem do Azure dedicada tooyour [subscrição](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fnetworking%2ftoc.json). Pode implementar várias VNets dentro de cada subscrição do Azure e Azure [região](https://azure.microsoft.com/regions). Cada VNet está isolado de outras VNets. Para cada VNet pode:

- Especifique um espaço de endereços IP privado personalizado utilizando endereços (RFC 1918) públicos e privados. Azure atribui um endereço IP privado recursos ligados toohello VNet do espaço de endereços de Olá que atribuir.
- Segmentar Olá VNet num ou mais sub-redes e atribuir uma parte da sub-rede de tooeach de espaço de endereços VNet Olá.
- Utilize a resolução de nome fornecidos pelo Azure ou especificar que o próprio servidor DNS para utilização pelos recursos ligados tooa VNet.

mais informações sobre o serviço de rede Virtual do Azure Olá, leia Olá toolearn [descrição geral de rede Virtual](../virtual-network/virtual-networks-overview.md?toc=%2fazure%2fnetworking%2ftoc.json) artigo. Pode ligar VNets tooeach outros, ativar recursos ligados tooeither VNet toocommunicate entre si entre VNets. Pode utilizar um ou ambos Olá opções tooconnect VNets tooeach outros os seguintes:

- **Peering:** ativa recursos ligados toodifferent as VNets do Azure dentro Olá mesma região do Azure toocommunicate entre si. Olá largura de banda e latência em Olá VNets é Olá mesmo como se recursos Olá foram toohello ligada mesma VNet. toolearn mais informações sobre peering, leia Olá [descrição geral de peering da rede Virtual](../virtual-network/virtual-network-peering-overview.md?toc=%2fazure%2fnetworking%2ftoc.json) artigo.
- **Gateway de VPN:** ativa recursos ligados toodifferent as VNets do Azure dentro de diferentes regiões Azure toocommunicate entre si. Fluxos de tráfego entre as VNets através de um Gateway de VPN do Azure. Largura de banda entre as VNets é limitado toohello largura de banda do gateway de Olá. mais sobre como ligar VNets com um Gateway de VPN, leia Olá toolearn [configurar uma ligação VNet a VNet em regiões](../vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal.md?toc=%2fazure%2fnetworking%2ftoc.json) artigo.

## <a name="internet-connectivity"></a>Conectividade Internet

Todos os recursos do Azure ligado tooa VNet tem conectividade de saída toohello Internet por predefinição. endereço IP privado Olá do recurso de Olá é o endereço de rede de origem traduzido endereço IP público tooa (realizar o SNAT) por Olá infraestrutura do Azure. mais informações sobre a ligação à Internet de saída, leia Olá toolearn [Noções sobre ligações de saída no Azure](../load-balancer/load-balancer-outbound-connections.md?toc=%2fazure%2fnetworking%2ftoc.json) artigo.

toocommunicate tooAzure recursos da Internet sem realizar o SNAT, um recurso deve ser atribuída um endereço IP público Olá Internet ou toocommunicate toohello saída de entrada. mais informações sobre os endereços IP públicos, leia Olá toolearn [endereços IP públicos](../virtual-network/virtual-network-public-ip-address.md?toc=%2fazure%2fnetworking%2ftoc.json) artigo.

## <a name="on-premises-connectivity"></a>Conectividade no local

Pode aceder a recursos na sua VNet em segurança através de uma ligação VPN ou uma ligação privada direta. toosend tráfego de rede entre a rede virtual do Azure e a sua rede no local, tem de criar um gateway de rede virtual. Configurar as definições de Olá gateway toocreate Olá tipo de ligação que pretende, VPN ou ExpressRoute.

Pode ligar-se a sua tooa de rede no local VNet utilizando qualquer combinação dos Olá seguintes opções:

**Ponto a site (VPN através de SSTP)**

Olá seguinte imagem mostra toosite separado do ponto de ligações entre vários computadores e uma VNet:

![Ponto a site](./media/networking-overview/point-to-site.png)

Esta ligação é estabelecida entre um computador único e uma VNet. Este tipo de ligação é excelente se de que está a começar com o Azure ou para os programadores, porque necessita de rede do tooyour de alterações existente do pouco ou nenhum. Também é conveniente quando estiverem a ligar a partir de uma localização remota, como numa conferência ou doméstica. As ligações ponto a site são, muitas vezes, conjugadas com uma ligação site a site através de Olá mesmo gateway de rede virtual. ligação de Olá utiliza a comunicação de tooprovide encriptado de protocolo SSTP Olá Olá Internet entre o computador de Olá e Olá VNet. Latência de Olá para uma VPN ponto a site é imprevisível, uma vez que o tráfego de Olá atravessa Olá Internet.

**Site a site (túnel VPN IPsec/IKE)**

![Site a Site](./media/networking-overview/site-to-site.png)

Esta ligação é estabelecida entre o dispositivo VPN no local e um Gateway de VPN do Azure. Este tipo de ligação permite qualquer recurso no local que está a autorizar a tooaccess Olá VNet. ligação de Olá é uma VPN IPSec/IKE que fornece comunicações encriptadas através de Olá Internet entre o dispositivo no local e o gateway de VPN do Azure Olá. Pode ligar vários toohello de sites no local mesmo gateway de VPN. Olá no local dispositivo VPN em cada site tem de ter um com acesso exterior endereço IP público que não estiver protegido por um NAT. Latência de Olá para uma ligação site a site é imprevisível, uma vez que o tráfego de Olá atravessa Olá Internet.

**ExpressRoute (ligação privada dedicada)**

![ExpressRoute](./media/networking-overview/expressroute.png)

Este tipo de ligação é estabelecido entre a rede e o Azure, através de um parceiro do ExpressRoute. Esta ligação é privada. Tráfego atravessar não Olá Internet. Latência de Olá para uma ligação ExpressRoute é previsível, uma vez que o tráfego não atravessar Olá Internet. ExpressRoute pode ser combinado com uma ligação site a site.

mais informações sobre todos os Olá ligação opções anteriores, leia Olá toolearn [diagramas de topologia de ligação](../vpn-gateway/vpn-gateway-about-vpngateways.md?toc=%2fazure%2fnetworking%2ftoc.json) artigo.

## <a name="load-balancing"></a>Direção do tráfego e balanceamento de carga

O Microsoft Azure oferece vários serviços para gerir a forma como o tráfego de rede é distribuído e balanceamento de carga. Pode utilizar qualquer uma das seguintes capacidades em separado ou em conjunto de Olá:

**Balanceamento de carga de DNS**

Olá serviço Gestor de tráfego do Azure fornece balanceamento de carga DNS global. Gestor de tráfego responde tooclients com o endereço IP Olá de um ponto final em bom estado, com base dos seguintes métodos de encaminhamento de Olá:
- **Geográfica:** os clientes são direcionados toospecific pontos finais (Azure externo ou aninhado) com base no que localização geográfica as respetivas consultas DNS tem origem. Este método permite cenários onde saberem a região geográfica do cliente e o encaminhamento-los com base no mesmo, são importante. Os exemplos incluem complying com indica a soberania dos dados, localização de experiência de utilizador e de conteúdo e medir o tráfego de regiões diferentes.
- **Desempenho:** endereço IP Olá devolvido toohello cliente é o cliente de toohello "mais próximo" Olá. ponto final de 'mais próximo' Olá não é necessariamente mais próximo, medido pela distância geográfica. Em vez disso, este método determina endpoint mais próximo Olá, medindo a latência de rede. Gestor de tráfego mantém um Internet latência tabela tootrack Olá reportadas round-trip tempo entre a intervalos de endereços IP e cada datacenter do Azure.
- **Prioridade:** tráfego é toohello direcionados ponto final do principal (mais alta prioridade). Se o ponto final de primário Olá não estiver disponível, o Gestor de tráfego de rotas Olá segundo ponto de final do tráfego toohello. Se ambos os pontos finais da primária e secundária Olá não estiverem disponíveis, o tráfego de Olá fica toohello terceira, e assim sucessivamente. Disponibilidade do ponto final de Olá é com base no estado de Olá configurado (ativado ou desativado) e Olá a monitorização de pontos finais em curso.
- **Round robin ponderado:** para cada pedido, o Gestor de tráfego escolhe aleatoriamente um ponto de final disponível. probabilidade Olá de escolher um ponto final é baseada em ponderações Olá atribuídas tooall os pontos finais disponíveis. Utilizar Olá mesma importância em todos os resultados de pontos finais uma distribuição de tráfego, mesmo. Utilizar ponderações superiores ou inferiores em pontos finais específicos, faz com que toobe esses pontos finais devolveu mais ou menos frequência nas respostas DNS Olá.

Olá imagem a seguir mostra um pedido para tooa de aplicações direcionadas para um web ponto final da aplicação Web. Pontos finais também podem ser outros serviços do Azure, tais como VMs e serviços em nuvem.

![Gestor de Tráfego](./media/networking-overview/traffic-manager.png)

Olá cliente liga-se diretamente toothat endpoint. Traffic Manager do Azure Deteta quando um ponto final está danificado e, em seguida, redireciona os clientes tooa diferentes, bom ponto final. mais sobre o Gestor de tráfego, leia Olá toolearn [descrição geral do Gestor de tráfego do Azure](../traffic-manager/traffic-manager-overview.md?toc=%2fazure%2fnetworking%2ftoc.json) artigo.

**Balanceamento de carga de aplicação**

Olá serviço de Gateway de aplicação do Azure fornece o controlador de entrega de aplicações (ADC) como um serviço. Gateway de aplicação oferece tooprotect de firewall de vários grupos de capacidades de balanceamento de carga de camada 7 (HTTP/HTTPS) para as suas aplicações, incluindo uma aplicação web, as aplicações web de vulnerabilidades e explorações. Gateway de aplicação também permite-lhe produtividade do toooptimize web farm ao descarregar o gateway de aplicação de toohello de terminação de SSL intensivas em CPU. 

Outras funcionalidades de encaminhamento de 7 camadas incluem a distribuição de round robin de tráfego de entrada, afinidade com base no cookie de sessão, URL com base no caminho de encaminhamento e Olá capacidade toohost vários sites por trás de um gateway de aplicação único. Gateway de aplicação pode ser configurado como um gateway de acesso à Internet, um gateway meramente internos ou uma combinação de ambos. Gateway de aplicação é Azure totalmente gerido, escalável e altamente disponível. Proporciona um conjunto avançado de capacidades de registo e diagnóstico, para uma melhor capacidade de gestão. mais sobre o Gateway de aplicação, leia Olá toolearn [descrição geral do Gateway de aplicação](../application-gateway/application-gateway-introduction.md?toc=%2fazure%2fnetworking%2ftoc.json) artigo.

Olá imagem seguinte mostra URL de encaminhamento com o Gateway de aplicação com base no caminho:

![Gateway de Aplicação](./media/networking-overview/application-gateway.png)

**Balanceamento de carga de rede**

Olá Balanceador de carga do Azure fornece elevado desempenho, baixa latência camada 4 balanceamento de carga para todos os protocolos UDP e TCP. Gere ligações de entrada e saídas. Pode configurar públicos e internos com balanceamento de carga pontos finais. Pode definir regras toomap destinos de conjunto de tooback-end de ligações de entrada através de TCP e HTTP pesquisa de estado de funcionamento opções toomanage disponibilidade do serviço. mais informações sobre o Balanceador de carga, leia Olá toolearn [descrição geral do Balanceador de carga](../load-balancer/load-balancer-overview.md?toc=%2fazure%2fnetworking%2ftoc.json) artigo.

Olá imagem a seguir mostra uma aplicação de várias camada de acesso à Internet que utiliza ambos os balanceadores de carga internos e externos:

![Load balancer](./media/networking-overview/load-balancer.png)

## <a name="security"></a>Segurança

Pode filtrar o tráfego tooand de recursos do Azure utilizando Olá seguintes opções:

- **Rede:** pode implementar toofilter de grupos (NSGs) para segurança de rede do Azure entrada e saída tooAzure recursos de tráfego. Cada NSG contém uma ou mais regras de entrada e saídas. Cada regra especifica os endereços IP de origem Olá, endereços IP de destino, porta e protocolo a que o tráfego é filtrado com. Os NSGs podem ser aplicados tooindividual sub-redes e VMs individuais. mais sobre NSGs, leia Olá toolearn [descrição geral de grupos de segurança de rede](../virtual-network/virtual-networks-nsg.md?toc=%2fazure%2fnetworking%2ftoc.json) artigo.
- **Aplicação:** utilizando um Gateway de aplicação com firewall de aplicação web pode proteger as suas aplicações web de vulnerabilidades e explorações. Exemplos comuns são ataques de injeção SQL, processamento de scripts entre sites e cabeçalhos com formato incorreto. Gateway de aplicação filtra este tráfego e deixa de chegar aos seus servidores web. São tooconfigure capaz de regras de que pretende ativado. políticas de negociação de SSL de tooconfigure capacidade Olá é fornecido tooallow determinada políticas toobe desativada. mais informações sobre firewall de aplicação web de Olá, leia Olá toolearn [firewall de aplicações Web](../application-gateway/application-gateway-web-application-firewall-overview.md?toc=%2fazure%2fnetworking%2ftoc.json) artigo.

Se precisar de capacidade de rede Azure não fornecer ou pretender toouse aplicações de rede que utiliza no local, pode implementar produtos Olá em VMs e ligue-tooyour VNet. Olá [Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/category/networking?page=1&subcategories=appliances) contém várias VMs diferentes pré-configurados com aplicações de rede poderá a utilizam atualmente. Estas VMs previamente configuradas são normalmente referidos tooas virtual os dispositivos de rede (NVA). NVAs estão disponíveis com aplicações, tais como a firewall e a otimização de WAN.

## <a name="routing"></a>Encaminhamento

O Azure cria predefinido tabelas de rota que permitem recursos ligados tooany sub-rede qualquer toocommunicate VNet entre si. Pode implementar um ou ambos Olá os seguintes tipos de rotas toooverride Olá rotas predefinidas que Azure cria:
- **Definido pelo utilizador:** pode criar as tabelas de rotas personalizadas com rotas controlam em que o tráfego é encaminhado toofor cada sub-rede. mais sobre as rotas definidas pelo utilizador, ler Olá toolearn [rotas definidas pelo utilizador](../virtual-network/virtual-networks-udr-overview.md?toc=%2fazure%2fnetworking%2ftoc.json) artigo.
- **Protocolo de gateway Protocol (BGP):** se ligar a sua rede no local do VNet tooyour através de uma ligação ExpressRoute ou de Gateway de VPN do Azure, pode propagar rotas BGP tooyour VNets. BGP é Olá protocolo de encaminhamento padrão utilizado normalmente na Olá tooexchange encaminhamento e acessibilidade informação de Internet entre duas ou mais redes. Elementos BGP chamado quando utilizados no contexto de Olá das redes virtuais do Azure, BGP permite Olá Gateways de VPN do Azure e os seus dispositivos VPN no local, ou vizinhos, tooexchange "rotas" que o informam ambas as gateways em disponibilidade Olá e acessibilidade para esses prefixos toogo através de gateways de Olá ou routers envolvidos. BGP também pode ativar o encaminhamento de tráfego entre várias redes ao propagar rotas um gateway BGP aprende de um tooall de elemento de rede BGP outros elementos de rede BGP. toolearn mais informações sobre o BGP, consulte Olá [BGP descrição geral de Gateways de VPN do Azure](../vpn-gateway/vpn-gateway-bgp-overview.md?toc=%2fazure%2fnetworking%2ftoc.json) artigo.

## <a name="manageability"></a>Capacidade de gestão

O Azure oferece seguinte Olá ferramentas toomonitor e gerir redes:
- **Registos de atividade:** tem de recursos do Azure todos os registos de atividade que fornecem informações sobre as operações executadas colocar, estado de operações e quem iniciou a operação de Olá. mais sobre os registos de atividade, leia Olá toolearn [descrição geral de registos de atividade](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md?toc=%2fazure%2fnetworking%2ftoc.json) artigo.
- **Os registos de diagnóstico:** Periodic e spontaneous eventos são criados pelos recursos de rede e registados em contas do storage do Azure, enviados tooan Hub de eventos do Azure ou enviados tooAzure análise de registos. Os registos de diagnóstico fornecem o estado de funcionamento do conhecimentos aprofundados toohello de um recurso. Os registos de diagnóstico são fornecidos para o Balanceador de carga (através da Internet), os grupos de segurança de rede, as rotas e Gateway de aplicação. mais informações sobre os registos de diagnóstico, leia Olá toolearn [descrição geral de registos de diagnóstico](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md?toc=%2fazure%2fnetworking%2ftoc.json) artigo.
- **Métricas:** métricas são medidas de desempenho e contadores recolhidos durante um período de tempo nos recursos. Métricas podem ser com base nos limiares de alertas de tootrigger utilizados. Atualmente as métricas estão disponíveis no Gateway de aplicação. mais informações sobre as métricas, leia Olá toolearn [descrição geral de métricas](../monitoring-and-diagnostics/monitoring-overview-metrics.md?toc=%2fazure%2fnetworking%2ftoc.json) artigo.
- **Resolução de problemas:** informações de resolução de problemas pode ser acedida diretamente Olá portal do Azure. informações de Olá ajudam a diagnosticar problemas comuns com o ExpressRoute, Gateway de VPN, Gateway de aplicação, registos de segurança de rede, rotas, DNS, Balanceador de carga e do Traffic Manager.
- **O controlo de acesso baseado em funções (RBAC):** controlar quem pode criar e gerir recursos de rede com controlo de acesso baseado em funções (RBAC). Saiba mais sobre o RBAC o lendo Olá [começar a utilizar o RBAC](../active-directory/role-based-access-control-what-is.md?toc=%2fazure%2fnetworking%2ftoc.json) artigo. 
- **Captura de pacotes:** Olá observador de rede de Azure serviço fornece Olá toorun capacidade capturar um pacote numa VM através de uma extensão no Olá VM. Esta capacidade está disponível para Linux e VMs do Windows. mais informações sobre a captura de pacotes, leia Olá toolearn [descrição geral de captura de pacotes](../network-watcher/network-watcher-packet-capture-overview.md?toc=%2fazure%2fnetworking%2ftoc.json) artigo.
- **Certifique-se de fluxos IP:** observador de rede permite-lhe tooverify IP fluxos entre uma VM do Azure e um toodetermine recurso remoto se os pacotes são permitidos ou negados. Esta capacidade permite aos administradores Olá tooquickly diagnosticar problemas de conectividade. toolearn mais informações sobre como flui tooverify IP, leia Olá [fluxo IP verificar descrição geral](../network-watcher/network-watcher-ip-flow-verify-overview.md?toc=%2fazure%2fnetworking%2ftoc.json) artigo.
- **Resolver problemas de conectividade VPN:** Olá capacidade de troubleshooter VPN do observador de rede fornece Olá capacidade tooquery uma ligação ou o gateway e verificar Olá estado de funcionamento dos recursos de Olá. mais informações sobre resolução de problemas de ligações de VPN, leia Olá toolearn [descrição geral de resolução de problemas de conectividade VPN](../network-watcher/network-watcher-troubleshoot-overview.md?toc=%2fazure%2fnetworking%2ftoc.json) artigo.
- **Visualizar a topologia de rede:** ver uma representação gráfica Olá de recursos de rede numa VNet com o observador de rede. mais sobre a visualização de topologia de rede, leia Olá toolearn [descrição geral da topologia](../network-watcher/network-watcher-topology-overview.md?toc=%2fazure%2fnetworking%2ftoc.json) artigo.

## <a name="tools"></a>Ferramentas de configuração e implementação

Pode implementar e configurar recursos de rede do Azure com qualquer uma das seguintes ferramentas de Olá:

- **Portal do Azure:** uma interface gráfica do utilizador que é executado num browser. Abra Olá [portal do Azure](http://portal.azure.com).
- **O Azure PowerShell:** ferramentas da linha de comandos para gerir o Azure a partir de computadores Windows. Saiba mais sobre o Azure PowerShell por ler Olá [descrição geral do Azure PowerShell](/powershell/azure/overview?view=azurermps-3.8.0?toc=%2fazure%2fnetworking%2ftoc.json) artigo.
- **Interface de linha de comandos (CLI) do Azure:** ferramentas da linha de comandos para gerir o Azure a partir de computadores Linux, macOS ou do Windows. Saiba mais sobre Olá CLI do Azure por ler Olá [descrição geral da CLI do Azure](/cli/azure/get-started-with-azure-cli?toc=%2fazure%2fnetworking%2ftoc.json) artigo.
- **Modelos Azure Resource Manager:** um ficheiro (no formato JSON) que define a infraestrutura de Olá e a configuração de uma solução do Azure. Ao utilizar um modelo, pode implementar repetidamente a solução durante o ciclo de vida da mesma e ter a confiança de que os recursos são implementados num estado consistente. mais sobre a criação de modelos, leia Olá toolearn [melhores práticas para a criação de modelos](../azure-resource-manager/resource-manager-template-best-practices.md?toc=%2fazure%2fnetworking%2ftoc.json) artigo. Modelos podem ser implementados Olá portal do Azure, CLI ou PowerShell. tooget os primeiros com modelos, implemente uma das Olá vários modelos previamente configurados no Olá [modelos de início rápido do Azure](https://azure.microsoft.com/resources/templates/?term=network) biblioteca. 

## <a name="pricing"></a>Preços

Alguns dos Olá Azure serviços de rede têm um encargos, enquanto outras são gratuitas. Olá vista [rede Virtual](https://azure.microsoft.com/pricing/details/virtual-network), [Gateway de VPN](https://azure.microsoft.com/pricing/details/vpn-gateway), [Gateway de aplicação](https://azure.microsoft.com/en-us/pricing/details/application-gateway/), [Balanceador de carga](https://azure.microsoft.com/pricing/details/load-balancer), [doobservadorderede](https://azure.microsoft.com/pricing/details/network-watcher), [DNS](https://azure.microsoft.com/pricing/details/dns), [Gestor de tráfego](https://azure.microsoft.com/pricing/details/traffic-manager) e [ExpressRoute](https://azure.microsoft.com/pricing/details/expressroute) preços páginas para obter mais informações.

## <a name="next-steps"></a>Passos seguintes

- Criar a primeira VNet e ligue-se algumas VMs tooit, seguindo os passos de Olá no Olá [criar a primeira rede virtual](../virtual-network/virtual-network-get-started-vnet-subnet.md?toc=%2fazure%2fnetworking%2ftoc.json) artigo.
- Ligar o computador tooa VNet, efetuando os passos de Olá Olá [configurar uma ligação ponto a site](../vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal.md?toc=%2fazure%2fnetworking%2ftoc.json) artigo.
- Balanceamento de carga de servidores de toopublic de tráfego de Internet, efetuando os passos de Olá Olá [criar um balanceador de carga para a Internet](../load-balancer/load-balancer-get-started-internet-portal.md?toc=%2fazure%2fnetworking%2ftoc.json) artigo.
