---
title: "aaaAzure práticas recomendadas de segurança de rede | Microsoft Docs"
description: "Este artigo fornece um conjunto de melhores práticas para utilizar de segurança de rede incorporada capacidades do Azure."
services: security
documentationcenter: na
author: TomShinder
manager: swadhwa
editor: TomShinder
ms.assetid: 7f6aa45f-138f-4fde-a611-aaf7e8fe56d1
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/09/2017
ms.author: TomSh
ms.openlocfilehash: 5867dea358b4da65c65b3e52fcab7e687e981642
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-network-security-best-practices"></a>Práticas recomendadas de segurança de rede do Azure
Microsoft Azure permite-lhe dispositivos de tooother está ligado em rede de máquinas virtuais e aplicações tooconnect colocando-los em redes virtuais do Azure. Uma rede Virtual do Azure é uma construção de rede virtual que permite-lhe tooconnect rede virtual interface cartões tooa virtual tooallow baseada em TCP/IP comunicações de rede entre dispositivos de rede ativada. Máquinas virtuais do Azure ligado tooan rede Virtual do Azure são tooconnect capaz de toodevices no Olá a mesma rede Virtual do Azure, diferentes redes de virtuais do Azure, no Olá Internet ou mesmo nas suas próprias redes no local.

Neste artigo, vamos abordar uma coleção de práticas recomendadas de segurança de rede do Azure. Estas melhores práticas são derivadas da nossa experiência com redes do Azure e experiências Olá dos clientes, como por si.

Para cada melhor prática, vamos explicar:

* Que Olá melhor prática é
* Motivo pelo qual pretende tooenable que melhor prática
* Se falhar tooenable Olá prática recomendada, que poderá ser resultado de Olá
* Possíveis alternativas toohello prática recomendada
* Como pode saber tooenable Olá prática recomendada

Este artigo de melhores práticas de segurança do Azure rede baseia-se no opinião um consenso e capacidades da plataforma do Azure e conjuntos de funcionalidades, tal como existem momento Olá que este artigo foi escrito. As tecnologias e opinions alteram ao longo do tempo e este artigo será atualizado num tooreflect regularmente essas alterações.

Azure rede melhores práticas de segurança abordadas neste artigo incluem:

* Logicamente as sub-redes de segmento
* Controlar o comportamento de encaminhamento
* Ativar a imposição do túnel
* Utilizar dispositivos de rede Virtual
* Implementar o DMZ para zonas de segurança
* Evitar a exposição toohello Internet com ligações WAN dedicadas
* Otimizar o desempenho e disponibilidade
* Utilizar o balanceamento de carga global
* Desativar tooAzure acesso RDP a máquinas virtuais
* Centro de segurança do Azure de ativação
* Expandir o seu centro de dados no Azure

## <a name="logically-segment-subnets"></a>Logicamente as sub-redes de segmento
[Redes virtuais do Azure](https://azure.microsoft.com/documentation/services/virtual-network/) são semelhantes LAN tooa na sua rede no local. Olá ideia atrás de uma rede Virtual do Azure é a criação de uma único IP endereço com base no espaço rede privada em que pode colocar todos os seus [Virtual Machines do Azure](https://azure.microsoft.com/services/virtual-machines/). Olá privados espaços de endereços IP disponíveis estão a ser Olá A classe (10.0.0.0/8), classe B (172.16.0.0/12) e de classe C intervalos (192.168.0.0/16).

Toowhat semelhantes no local, poderá ser útil toosegment Olá maior o espaço de endereços em sub-redes. Pode utilizar [CIDR](https://en.wikipedia.org/wiki/Classless_Inter-Domain_Routing) com base subnetting princípios toocreate as sub-redes.

Encaminhamento entre sub-redes acontecerá automaticamente e não precisa de toomanually configurar tabelas de encaminhamento. No entanto, a predefinição de Olá é que não existem sem controlos de acesso de rede entre sub-redes Olá que criar no Olá rede Virtual do Azure. Na ordem toocreate rede controlos de acesso entre sub-redes, terá de tooput algo entre sub-redes Olá.

Uma das ações de Olá pode utilizar tooaccomplish esta tarefa é um [grupo de segurança de rede](../virtual-network/virtual-networks-nsg.md) (NSG). Os NSGs são inspeção de pacotes de monitorização de estado simples toocreate permitir/recusar as regras de tráfego de rede de abordar a dispositivos que utilizam Olá 5 cadeias de identificação (IP de origem Olá, porta de origem, IP de destino, porta de destino e protocolo de camada 4). Pode permitir ou negar o tráfego tooand do endereço IP único, tooand de vários endereços IP ou até mesmo tooand de sub-redes de todos.

Utilizar os NSGs para controlo de acesso de rede entre sub-redes permite-lhe tooput recursos que pertencem toohello mesmo zona de segurança ou função nas suas próprias sub-redes. Por exemplo, considere uma simples aplicação de 3 camadas que tem uma camada web, uma camada de lógica de aplicação e uma camada de base de dados. Colocar as máquinas virtuais que pertencem tooeach estas camadas nas suas próprias sub-redes. Em seguida, utilizar NSGs toocontrol tráfego entre sub-redes Olá:

* Máquinas de virtuais de camada Web podem apenas iniciar máquinas de lógica de aplicação de toohello ligações e só pode aceitar ligações a partir de Olá Internet
* Máquinas de virtuais de lógica de aplicação apenas podem iniciar ligações com camadas de base de dados e só pode aceitar ligações a partir da camada de web de Olá
* Máquinas de virtuais de camada de base de dados não é possível iniciar a ligação com qualquer coisa fora da sua própria sub-rede e só pode aceitar ligações a partir da camada de lógica de aplicação Olá

toolearn mais sobre os grupos de segurança de rede e como pode utilizá-los toologically segmento redes virtuais do Azure, leia o artigo de Olá [que é um grupo de segurança de rede](../virtual-network/virtual-networks-nsg.md) (NSG).

## <a name="control-routing-behavior"></a>Controlar o comportamento de encaminhamento
Quando coloca uma máquina virtual numa rede Virtual do Azure, irá notar que Olá a máquina virtual pode ligar-se tooany outra máquina virtual no Olá a mesma rede Virtual do Azure, mesmo se hello outras máquinas virtuais estiverem em sub-redes diferentes. motivo Olá por que motivo é possível é que haja uma coleção de rotas de sistema que estão ativadas por predefinição que permita este tipo de comunicação. Estas rotas predefinidas permitem máquinas virtuais no Olá mesmas rede Virtual do Azure tooinitiate as ligações entre si e com Olá Internet (para comunicações de saída toohello Internet apenas).

Enquanto as rotas de sistema do Olá predefinidas são úteis para vários cenários de implementação, há horas em que pretende configuração de encaminhamento de Olá toocustomize para as implementações. Estas personalizações permitirá tooconfigure Olá próximos salto endereço tooreach determinados destinos.

Recomendamos que configure rotas definidas pelo utilizador ao implementar uma aplicação de segurança de rede virtual, que iremos falar sobre no posterior melhor prática.

> [!NOTE]
> Rotas definidas pelo utilizador não são necessárias e rotas de sistema predefinido Olá irão funcionar na maioria das instâncias.
>
>

Pode saber mais sobre rotas definidas pelo utilizador e como tooconfigure-las ao ler o artigo Olá [que são rotas definidas pelo utilizador e reencaminhamento IP](../virtual-network/virtual-networks-udr-overview.md).

## <a name="enable-forced-tunneling"></a>Ativar a imposição do túnel
toobetter compreender a imposição do túnel, é útil toounderstand é que "divisão de túnel".
exemplo de mais comuns de Olá de divisão de túnel é utilizado com ligações VPN. Imagine que estabeleça uma ligação VPN da sua rede empresarial do átrios sala tooyour. Esta ligação permite tooconnect tooresources na sua rede empresarial e aceda todas as comunicações tooresources na sua rede empresarial através do túnel VPN de Olá.

O que acontece quando quiser tooconnect tooresources no Olá Internet? Quando a divisão do túnel estiver ativada, as ligações aceda diretamente toohello Internet e não através de Olá VPN túnel. Alguns especialistas de segurança, considere este toobe um risco potencial e, por conseguinte, recomendamos que divisão de túnel desativada e todas as ligações, os destinado Olá Internet e os destinado a recursos da empresa, aceda através do túnel VPN de Olá. Olá vantagem fazê-lo é essa toohello ligações à Internet, em seguida, são forçadas através de dispositivos de segurança do Olá rede empresarial, que não conseguiriam caso Olá se o cliente VPN de Olá ligado toohello Internet fora do túnel VPN de Olá.

Agora vamos colocar esta cópia toovirtual máquinas numa rede Virtual do Azure. as rotas predefinidas de Olá para uma rede Virtual do Azure permitem que as máquinas virtuais tooinitiate tráfego toohello Internet. Isto demasiado pode representar um risco de segurança, como estas ligações de saída foi possível aumentar a superfície de ataque de Olá de uma máquina virtual e ser aproveitadas pelas atacantes.
Por este motivo, recomendamos que ative a imposição do túnel nas suas máquinas virtuais quando tiver uma conectividade entre instalações entre a rede Virtual do Azure e a sua rede no local. Serão abordadas cruzada conetividade mais tarde neste documento de práticas de melhor de rede do Azure.

Se não tiver uma ligação entre locais, certifique-se, tirar partido de grupos de segurança de rede (debatidas anteriormente) ou do Azure rede virtual segurança aparelhos (referido seguinte) tooprevent ligações de saída toohello Internet a partir de Virtual do Azure Máquinas.

mais informações sobre como toolearn imposição do túnel e como tooenable, leia o artigo de Olá [configurar a imposição do túnel com o PowerShell e do Azure Resource Manager](../vpn-gateway/vpn-gateway-forced-tunneling-rm.md).

## <a name="use-virtual-network-appliances"></a>Utilizar dispositivos de rede virtual
Enquanto os grupos de segurança de rede e o encaminhamento de definido pelo utilizador podem fornecer medidas de segurança de rede em Olá camadas de rede e o transporte de Olá [modelo OSI](https://en.wikipedia.org/wiki/OSI_model), vão toobe situações onde irá pretende ou precisa tooenable segurança alta níveis da pilha de Olá. Estas situações, recomendamos que implemente aplicações de segurança de rede virtual fornecidas pelo Azure parceiros.

Aplicações de segurança de rede do Azure podem proporcionar significativamente melhorados níveis de segurança ao longo do que é fornecido por controlos de nível de rede. Algumas das funcionalidades de segurança de rede de Olá fornecidas por aplicações de segurança de rede virtual incluem:

* Firewalling
* Deteção de intrusões/intrusões prevenção
* Gestão de vulnerabilidade
* Controlo de aplicação
* Deteção de anomalias com base na rede
* A filtragem da Web
* Antivírus
* Proteção de Botnet

Se necessitar de um nível mais elevado de segurança de rede que pode obter com controlos de nível de acesso de rede, em seguida, recomendamos que analise e implementar aplicações de segurança de rede virtual do Azure.

toolearn sobre as aplicações de segurança de rede virtual do Azure estão disponíveis e sobre as respetivas capacidades, visite Olá [Azure Marketplace](https://azure.microsoft.com/marketplace/) e procure "segurança" e "segurança de rede".

## <a name="deploy-dmzs-for-security-zoning"></a>Implementar o DMZ para zonas de segurança
Uma rede de Perímetro ou "rede de perímetro" é uma física ou segmento de rede lógica que esteja concebida tooprovide uma camada adicional de segurança entre os recursos e Olá Internet. objetivo Olá Olá DMZ é tooplace especializada dispositivos de controlo de acesso de rede no limite de Olá da rede de Olá DMZ para que apenas pretendido o tráfego é permitido passado Olá dispositivo de segurança de rede e na rede Virtual do Azure.

DMZ é úteis porque lhe pode concentrar-se a gestão de controlo de acesso de rede, monitorização, registo e relatórios sobre dispositivos Olá na periferia Olá da sua rede Virtual do Azure. Aqui, normalmente, seria ativar DDoS prevenção, sistemas de prevenção de intrusões/deteção de intrusões (IDS/IPS), as regras de firewall e políticas, web filtragem, antimalware de rede e muito mais. dispositivos de segurança de rede Olá manter-se entre Olá Internet e a rede Virtual do Azure e tem uma interface em ambas as redes.

Embora seja estrutura básica do Olá de uma rede de Perímetro, existem muitas estruturas diferentes de rede de Perímetro, tal como back, duplamente, o tri, multihomed e outros.

Recomenda-se para todas as implementações de alta segurança que considerar implementar um nível de Olá tooenhance DMZ de segurança de rede para os seus recursos do Azure.

mais informações sobre o DMZ e como toodeploy-las no Azure, leia o artigo de Olá toolearn [Cloud Services da Microsoft e de segurança de rede](../best-practices-network-security.md).

## <a name="avoid-exposure-toohello-internet-with-dedicated-wan-links"></a>Evitar a exposição toohello Internet com ligações WAN dedicadas
Muitas organizações tem optado por rota de TI híbridos Olá. TI híbridos, alguns dos recursos de informações da empresa Olá estão no Azure, enquanto outros permanecem no local. Em muitos casos alguns componentes de um serviço irão ser em execução no Azure enquanto outros componentes permanecem no local.

No híbrida Olá cenário IT, existe é normalmente algum tipo de conectividade em vários locais. Isto em vários locais conectividade permite Olá empresa tooconnect os respetivos tooAzure de redes no local redes virtuais. Existem duas soluções de conectividade em vários locais disponíveis:

* VPN de site a site
* ExpressRoute

[VPN de site para site](../vpn-gateway/vpn-gateway-site-to-site-create.md) representa uma ligação privada virtual entre a rede no local e uma rede Virtual do Azure. Esta ligação demora mais Olá Internet e permite-lhe demasiado "Criar um túnel entre" informações no interior de uma ligação encriptada entre a rede e do Azure. VPN de site a site é uma tecnologia de segura, madura que tenha sido implementada por empresas de todos os tamanhos de decades. Encriptação de túnel é executada com [modo de túnel IPsec](https://technet.microsoft.com/library/cc786385.aspx).

Enquanto VPN site a site é uma tecnologia de fidedigna, fiável e estabelecida, o tráfego de túnel Olá atravessar Olá Internet. Além disso, a largura de banda é relativamente restrita tooa máximo sobre 200 Mbps.

Se necessitar de um nível excecional de segurança ou de desempenho para as suas ligações entre locais, recomendamos que utilize o Azure ExpressRoute para a conectividade em vários locais. O ExpressRoute é uma WAN dedicada ligação entre a sua localização no local ou num fornecedor de alojamento do Exchange. Porque se trata de uma ligação de telco, os dados não percorram Olá Internet e, por conseguinte, é toohello não exposta potenciais riscos inerentes em comunicações da Internet.

mais informações sobre como funciona o Azure ExpressRoute toolearn e como toodeploy, leia o artigo de Olá [descrição geral técnica do ExpressRoute](../expressroute/expressroute-introduction.md).

## <a name="optimize-uptime-and-performance"></a>Otimizar o desempenho e disponibilidade
Confidencialidade, integridade e disponibilidade (CIA) compõem triad Olá do modelo de segurança mais influential hoje. Confidencialidade sobre privacidade e encriptação, integridade é sobre certificando-se de que dados não são alterados por parte do pessoal não autorizada, não sendo disponibilidade sobre certificando-se de que as pessoas autorizadas são tooaccess capaz de informações de Olá que estiverem autorizadas tooaccess. Falha em qualquer uma das seguintes áreas representa uma potencial violação em segurança.

Disponibilidade pode considerar como sendo sobre desempenho e disponibilidade. Se um serviço estiver desativado, não não possível aceder a informações. Se o desempenho é por isso, fraco como dados de Olá toomake inutilizáveis, em seguida, iremos pode considerar Olá dados toobe inacessível. Por conseguinte, numa perspetiva de segurança, precisamos toodo qualquer podemos toomake se nossos serviços tem o desempenho e disponibilidade ideal.
Um método popular e mais eficaz utilizado tooenhance disponibilidade e desempenho é toouse balanceamento de carga. Balanceamento de carga é um método de distribuição de tráfego de rede nos servidores que fazem parte de um serviço. Por exemplo, se tiver servidores web front-end como parte do seu serviço, pode utilizar o balanceamento de carga tráfego de Olá toodistribute entre os vários servidores web front-end.

Esta distribuição de tráfego aumenta a disponibilidade dos porque se um dos servidores de web de Olá ficar indisponível, o Balanceador de carga Olá irá parar de enviar tráfego toothat servidor e redirecionamento tráfego toohello os servidores que ainda estão online. Balanceamento de carga também ajuda-o desempenho, porque hello processador, rede e memória sobrecarga para servir pedidos é distribuído por todos os servidores de balanceamento de carga Olá.

Recomendamos que utilize o balanceamento de carga sempre que pode e, conforme adequado para os serviços. Iremos irá endereços appropriateness no Olá secções a seguir.
No nível de rede Virtual do Azure Olá, Azure fornece-lhe primário três as opções de balanceamento de carga:

* Balanceamento de carga baseado em HTTP
* Balanceamento de carga externa
* Balanceamento de carga interno

## <a name="http-based-load-balancing"></a>Balanceamento de carga baseado em HTTP
Balanceamento de carga baseado em HTTP bases decisões sobre que ligações de toosend de servidor utilizando as características de protocolo de Olá HTTP. O Azure tem um balanceador de carga HTTP passa por nome de Olá do Gateway de aplicação.

Recomendamos que, Gateway de aplicação do Azure dos EUA quando:

* Aplicações que necessitam de pedidos de Olá mesmo tooreach de sessão de utilizador/cliente Windows hello mesma máquina virtual de back-end. Exemplos de isto iriam ser compras carrinho aplicações e servidores de correio eletrónico de web.
* As aplicações que pretende toofree farms de servidores web de terminação de SSL sobrecarga, tirando partido de Gateway de aplicação [descarga de SSL](https://f5.com/glossary/ssl-offloading) funcionalidade.
* As aplicações, como uma rede de entrega de conteúdos, que necessitam de vários pedidos HTTP na Olá toobe de ligação de TCP de longa execução mesmo encaminhados ou servidores de back-end toodifferent com balanceamento de carga.

toolearn mais informações sobre como funciona o Gateway de aplicação do Azure e como pode utilizá-lo das implementações, leia o artigo Olá [descrição geral do Gateway de aplicação](../application-gateway/application-gateway-introduction.md).

## <a name="external-load-balancing"></a>Balanceamento de carga externa
Balanceamento de carga externo ocorre quando as ligações recebidas da Internet de Olá com entre os servidores localizados numa rede Virtual do Azure de balanceamento de carga. Balanceador de carga externo Azure Olá pode fornecer esta capacidade e recomendamos que o utilize quando não precisa de sessões temporária Olá ou descarga de SSL.

Em contraste com base em tooHTTP balanceamento de carga, Olá Balanceador de carga externo utiliza informações em camadas de rede e o transporte de Olá de Olá OSI modelo toomake decisões de rede em que servidor tooload saldo ligação.

Recomendamos que utilize o balanceamento de carga externo, sempre que tiver [as aplicações sem estado](http://whatis.techtarget.com/definition/stateless-app) aceitando pedidos recebidos de Olá Internet.

toolearn mais informações sobre como funciona o Olá Balanceador de carga externos do Azure e como implementá-la, leia o artigo Olá [introdução à criação de um balanceador de carga com acesso à Internet no Gestor de recursos com o PowerShell](../load-balancer/load-balancer-get-started-internet-arm-ps.md).

## <a name="internal-load-balancing"></a>Balanceamento de carga interna
Balanceamento de carga interna é semelhante tooexternal balanceamento de carga e utiliza Olá mesmo mecanismo tooload saldo ligações toohello servidores atrás-los. Olá apenas diferença é que Balanceador de carga Olá neste caso, está a aceitar ligações a partir de máquinas virtuais que não estão no Olá Internet. Na maioria dos casos, as ligações de Olá que são considerados aceites para balanceamento de carga são iniciadas por dispositivos numa rede Virtual do Azure.

Recomendamos que utilize para cenários que irão beneficiar esta capacidade, tal como quando precisa de tooload saldo ligações tooSQL servidores ou servidores web interna de balanceamento de carga interna.

toolearn mais informações sobre como funciona o Azure interno balanceamento de carga e como implementá-la, leia o artigo Olá [introdução à criação de um balanceador de carga internos através do PowerShell](../load-balancer/load-balancer-get-started-internet-arm-ps.md#update-an-existing-load-balancer).

## <a name="use-global-load-balancing"></a>Utilizar o balanceamento de carga global
Possibilita de informática em nuvem pública toodeploy globalmente distribuídas as aplicações que têm componentes localizados nos centros de dados em todo o mundo Olá. Isto é possível no Microsoft Azure devido a presença de centro de dados global do tooAzure. Em contrapartida tecnologias de balanceamento de carga de toohello mencionado anteriormente, balanceamento de carga global torna possível toomake serviços disponíveis, mesmo quando centros de dados completos podem ficar indisponíveis.

Pode obter este tipo global de balanceamento de carga no Azure, tirando partido de [Traffic Manager do Azure](https://azure.microsoft.com/documentation/services/traffic-manager/). Gestor de tráfego torna é saldo tooload possíveis dos serviços de tooyour ligações com base na localização de Olá do utilizador Olá.

Por exemplo, se o utilizador Olá é efetuar um serviço pedido tooyour Olá EU, ligação Olá é serviços tooyour direcionados localizados no Centro de dados EU. Esta parte do Traffic Manager global de balanceamento de carga ajuda tooimprove desempenho porque a ligação toohello mais próximo do Centro de dados é mais rápida do que a ligação toodatacenters que estão agora ausente.

No lado de disponibilidade de Olá, balanceamento de carga global certifica-se de que o serviço está disponível, mesmo se todo o datacenter deve ficar disponível.

Por exemplo, se um datacenter Azure deve ficar indisponível devido a razões tooenvironmental ou atraso toooutages (como falhas de rede regional), ligações de serviço tooyour seria é redirecionada toohello mais próximo do Centro de dados online. Este tipo de balanceamento de carga global é conseguido ao tirar partido das políticas DNS que pode criar no Traffic Manager.

Recomendamos que utilize o Gestor de tráfego para qualquer solução de nuvem desenvolver que tem um âmbito amplamente distribuído em várias regiões e requer o nível mais elevado de Olá de tempo de atividade possíveis.

toolearn mais sobre o Gestor de tráfego do Azure e como toodeploy, leia o artigo de Olá [que é o Gestor de tráfego](../traffic-manager/traffic-manager-overview.md).

## <a name="disable-rdpssh-access-tooazure-virtual-machines"></a>Desativar o acesso RDP/SSH tooAzure máquinas virtuais
É possível tooreach Virtual Machines do Azure utilizando Olá [protocolo de ambiente de trabalho remoto](https://en.wikipedia.org/wiki/Remote_Desktop_Protocol) (RDP) e Olá [Secure Shell](https://en.wikipedia.org/wiki/Secure_Shell) protocolos (SSH). Estes protocolos tornam possível toomanage máquinas de localizações remotas e são padrão da informática do Centro de dados.

Olá problema de segurança potencial com utilizando estes protocolos através de Olá Internet é que os atacantes podem utilizar vários [força bruta](https://en.wikipedia.org/wiki/Brute-force_attack) técnicas toogain acesso tooAzure máquinas virtuais. Depois dos atacantes de Olá obterem acesso, pode utilizar a máquina virtual como um ponto de iniciação para comprometer a outras máquinas na sua rede Virtual do Azure ou mesmo ataques dispositivos de rede fora do Azure.

Por este motivo, recomendamos que desative direta RDP e SSH acesso tooyour Virtual Machines do Azure de Olá Internet. Depois de direto RDP e SSH o acesso dos Olá que Internet está desativada, tiver outras opções que pode utilizar tooaccess estas máquinas virtuais para a gestão remota:

* VPN ponto a site
* VPN de site a site
* ExpressRoute

[VPN ponto a site](../vpn-gateway/vpn-gateway-point-to-site-create.md) é outro termo para uma ligação de cliente/servidor VPN de acesso remoto. Uma VPN ponto a site permite que um único utilizador tooan de tooconnect rede Virtual do Azure através de Olá Internet. Depois de estabelecer a ligação de ponto a site Olá, utilizador de Olá será capaz de toouse RDP ou SSH tooconnect tooany máquinas virtuais localizadas nesse Olá Azure Virtual Network que Olá utilizador ligado toovia ponto a site VPN. Esta parte do princípio de que o utilizador Olá é tooreach autorizado dessas máquinas virtuais.

VPN ponto a site é mais segura do que as ligações RDP ou SSH diretas porque o utilizador Olá tem tooauthenticate duas vezes antes de máquina de virtual tooa ligação. Em primeiro lugar, Olá tooauthenticate necessidades de utilizador (e ser autorizado) tooestablish ligação de VPN de ponto a site Olá; segundo, Olá tooauthenticate necessidades de utilizador (e ser autorizado) as sessão tooestablish Olá RDP ou SSH.

A [VPN site a site](../vpn-gateway/vpn-gateway-site-to-site-create.md) se liga uma rede de tooanother toda a rede através do Olá Internet. Pode utilizar um tooconnect VPN de site para site seu tooan de rede local Virtual Network do Azure. Se implementar uma VPN de site a site, os utilizadores na sua rede no local será capaz de tooconnect toovirtual máquinas na sua rede Virtual do Azure utilizando Olá RDP ou o protocolo SSH mais Olá ligação de VPN de site a site e não necessita que tooallow direta RDP ou SSH aceder ao longo de Olá Internet.

Também pode utilizar uma funcionalidade de tooprovide de ligação WAN dedicado semelhante toohello VPN de site para site. diferenças principais Olá são 1. ligação WAN dedicado Olá não atravessar Olá Internet e 2. as ligações WAN dedicadas são, normalmente, mais estável e performant. O Azure oferece uma solução de ligação WAN dedicado no formato Olá [ExpressRoute](https://azure.microsoft.com/documentation/services/expressroute/).

## <a name="enable-azure-security-center"></a>Centro de segurança do Azure de ativação
Centro de segurança do Azure ajuda-o a evitar, detetar e responder toothreats e fornece que maior visibilidade e controlo sobre, segurança Olá dos seus recursos Azure. Fornece gestão de políticas e monitorização de segurança integrada nas suas subscrições do Azure, ajuda a detetar ameaças que caso contrário podem passar despercebidas e funciona com um ecossistema abrangente de soluções de segurança.

Centro de segurança do Azure ajuda-o a otimizar e monitorizar a segurança de rede por:

* Fornecer recomendações de segurança de rede
* Monitorização de estado de Olá da sua configuração de segurança de rede
* Alertar toonetwork com base ameaças de ambos os níveis Olá endpoint e da rede

Recomendamos vivamente que ative o Centro de segurança do Azure para todas as implementações do Azure.

mais informações sobre o Centro de segurança do Azure e como tooenable-lo para as implementações, leia o artigo de Olá toolearn [tooAzure de introdução do Centro de segurança](../security-center/security-center-intro.md).

## <a name="securely-extend-your-datacenter-into-azure"></a>Expandir o seu centro de dados em segurança no Azure
TI empresariais de muitas organizações procura tooexpand numa nuvem Olá em vez dos respetivos centros de dados no local a crescer. Esta expansão representa uma extensão da infraestrutura de TI existente numa nuvem pública Olá. Ao tirar partido em vários locais Opções de conectividade, é possível tootreat as redes virtuais do Azure como apenas outra sub-rede no seu local infraestrutura de rede.

No entanto, há uma grande quantidade de planeamento e questões de design que ter toobe resolvido primeiro. Isto é especialmente importante na área de Olá de segurança de rede. Uma das formas toounderstand de melhor Olá como abordar a essa uma estrutura é toosee um exemplo.

Microsoft criou Olá [diagrama de arquitetura de referência de extensão de Datacenter](https://gallery.technet.microsoft.com/Datacenter-extension-687b1d84#content) e suporte toohelp colaterais perceber uma extensão de centro de dados iria aspeto. Isto fornece uma implementação de referência de exemplo que pode utilizar tooplan e estruturar uma nuvem de toohello de extensão de centro de dados empresariais seguros. Recomendamos que reveja tooget este documento uma ideia dos componentes de chave Olá de uma solução segura.

toolearn mais informações sobre como toosecurely expandir o seu centro de dados no Azure, veja o vídeo de Olá [tooMicrosoft de expandir o Datacenter do Azure](https://www.youtube.com/watch?v=Th1oQQCb2KA).
