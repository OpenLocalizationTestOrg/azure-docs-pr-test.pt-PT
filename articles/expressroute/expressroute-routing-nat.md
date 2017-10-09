---
title: NAT para Azure ExpressRoute | Microsoft Docs
description: "Esta página apresenta os requisitos detalhados para configurar e gerir o encaminhamento para circuitos do ExpressRoute."
documentationcenter: na
services: expressroute
author: osamazia
manager: ganesr
editor: 
ms.assetid: eaaf0393-d384-4496-9a5c-328e94c262a7
ms.service: expressroute
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/12/2017
ms.author: osamam
ms.openlocfilehash: 7a8b760df90b545b5fbde2f614aef62dd3985bb6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="nat-for-expressroute"></a>NAT para ExpressRoute

tooconnect serviços em nuvem tooMicrosoft com o ExpressRoute, irá precisar de tooset cópias de segurança e gerir o encaminhamento. Alguns fornecedores de conectividade oferecem a configuração e a gestão do encaminhamento como um serviço gerido. Com o seu toosee do fornecedor de conectividade, verifique se oferece este serviço. Caso contrário, terá de cumprir os requisitos de toohello. 

Consulte toohello [circuitos e domínios de encaminhamento](expressroute-circuit-peerings.md) artigo para obter uma descrição de encaminhamento de Olá sessões que necessitam de toobe configurar na toofacilitate conectividade.

> [!NOTE]
> A Microsoft não suporta protocolos de redundância do router (por exemplo, HSRP, VRRP) para configurações de elevada disponibilidade. Precisamos de um par de sessões BGP redundante por peering para elevada disponibilidade.
> 
> 

## <a name="ip-addresses-used-for-peerings"></a>Endereços IP utilizados para peerings

Terá de tooreserve alguns blocos de IP endereços tooconfigure encaminhamento entre a rede e routers de limite (MSEEs) empresarial da Microsoft. Esta secção fornece uma lista dos requisitos e descreve as regras de Olá relativamente a como estes endereços IP tem de ser adquiridos e utilizados.

### <a name="ip-addresses-used-for-azure-private-peering"></a>Endereços IP utilizados para peering privado do Azure

Pode utilizar endereços IP privados ou pública IP endereços tooconfigure Olá peerings. intervalo de endereços de Olá utilizado para configurar as rotas não pode sobrepor com endereço intervalos utilizados toocreate redes virtuais no Azure. 

* Tem de reservar uma sub-rede /29 ou duas sub-redes /30 para as interfaces de encaminhamento.
* as sub-redes de Olá utilizadas para encaminhamento podem ser endereços IP privados ou endereços IP públicos.
* sub-redes Olá tem não estão em conflito com o intervalo de Olá reservado pelo cliente de Olá para utilização na nuvem da Microsoft hello.
* Se for utilizada uma sub-rede /29, será dividida em duas sub-redes /30. 
  * Olá primeiro/sub-rede 30 será utilizada para ligação primária Olá e Olá /30 segunda sub-rede será utilizada para a ligação secundária Olá.
  * Para cada uma das sub-redes Olá /30, tem de utilizar Olá primeiro endereço IP da sub-rede Olá /30 do router. Microsoft utilizará Olá segundo endereço IP da sub-rede de Olá /30 tooset se uma sessão BGP.
  * Tem de configurar ambas as sessões de BGP para o nosso [SLA de disponibilidade](https://azure.microsoft.com/support/legal/sla/) toobe válido.  

#### <a name="example-for-private-peering"></a>Exemplo de peering privado

Se escolher toouse a.b.c.d/29 tooset segurança Olá peering, este será dividido em duas sub-redes/30. Exemplo de Olá abaixo, iremos abordar como a sub-rede de a.b.c.d/29 Olá é utilizada. 

a.b.c.d/29 será dividido tooa.b.c.d/30 e a.b.c.d+4/30 e transmitidos para baixo tooMicrosoft através de Olá APIs de aprovisionamento. Irá utilizar + 1 como VRF IP do Olá para Olá PE primário e a Microsoft irão consumir + 2 como VRF IP de Olá Olá MSEE primário. Irá utilizar + 5 como hello VRF IP para hello PE secundário e a Microsoft utilizará + 6 como VRF IP de Olá Olá MSEE secundário.

Considere o caso onde poderá selecionar 192.168.100.128/29 tooset segurança peering privado. 192.168.100.128/29 inclui os endereços de 192.168.100.128 too192.168.100.135, dos quais:

* 192.168.100.128/30 será atribuído toolink1, com o fornecedor a utilizar o 192.168.100.129 e a Microsoft a utilizar o 192.168.100.130.
* 192.168.100.132/30 será atribuído toolink2, com o fornecedor a utilizar o 192.168.100.133 e a Microsoft a utilizar o 192.168.100.134.

### <a name="ip-addresses-used-for-azure-public-and-microsoft-peering"></a>Endereços IP utilizados para o peering público do Azure e da Microsoft

Tem de utilizar endereços IP públicos que é proprietário para configurar sessões de BGP Olá. Microsoft tem de ser propriedade de Olá tooverify capaz de endereços IP Olá através de registos de Internet de encaminhamento e registos de encaminhamento de Internet. 

* Tem de utilizar um único/29 ou duas sub-redes/30 tooset segurança Olá BGP de sub-rede peering para cada peering por circuito ExpressRoute (se tiver mais do que um). 
* Se for utilizada uma sub-rede /29, será dividida em duas sub-redes /30. 
  * Olá primeiro/sub-rede 30 será utilizada para ligação primária Olá e Olá /30 segunda sub-rede será utilizada para a ligação secundária Olá.
  * Para cada uma das sub-redes Olá /30, tem de utilizar Olá primeiro endereço IP da sub-rede Olá /30 do router. Microsoft utilizará Olá segundo endereço IP da sub-rede de Olá /30 tooset se uma sessão BGP.
  * Tem de configurar ambas as sessões de BGP para o nosso [SLA de disponibilidade](https://azure.microsoft.com/support/legal/sla/) toobe válido.

## <a name="public-ip-address-requirement"></a>Requisito de endereço IP público

### <a name="private-peering"></a>Peering Privado

Pode escolher toouse endereços de IPv4 públicos ou privados para peering privado. Fornecemos um isolamento do tráfego ponto-a-ponto, de modo a que a sobreposição de endereços com outros clientes não seja possível em caso de peering privado. Estes endereços não são tooInternet anunciado. 

### <a name="public-peering"></a>Peering Público

Olá caminho de peering público Azure permite-lhe tooconnect tooall serviços alojados no Azure ao longo dos respetivos endereços IP públicos. Estes incluem os serviços listados na Olá [ExpessRoute FAQ](expressroute-faqs.md) e quaisquer serviços alojados pelos ISVs no Microsoft Azure. Serviços de conectividade tooMicrosoft do Azure na público peering é sempre iniciado a partir da rede na rede da Microsoft hello. Tem de utilizar endereços IP públicos para a rede do Olá tráfego destinado tooMicrosoft.

### <a name="microsoft-peering"></a>Peering da Microsoft

caminho de peering da Microsoft Olá permite-lhe ligar serviços de cloud tooMicrosoft que não são suportados através de Olá caminho de peering público do Azure. lista de Olá de serviços inclui serviços do Office 365, como o Exchange Online, SharePoint Online, Skype para empresas e Dynamics 365. Microsoft suporta a conectividade bidirecional no peering da Microsoft hello. O tráfego destinado tooMicrosoft cloud services tem de utilizar endereços IPv4 públicos válidos antes de serem introduzidos na rede da Microsoft hello.

Certifique-se de que o endereço IP e o número as estão registado tooyou dos registos de Olá listados abaixo.

* [ARIN](https://www.arin.net/)
* [APNIC](https://www.apnic.net/)
* [AFRINIC](https://www.afrinic.net/)
* [LACNIC](http://www.lacnic.net/)
* [RIPENCC](https://www.ripe.net/)
* [RADB](http://www.radb.net/)
* [ALTDB](http://altdb.net/)

> [!IMPORTANT]
> IP público endereços anunciados tooMicrosoft através do ExpressRoute não pode ser toohello anunciado à Internet. Isto poderá interromper serviços da Microsoft tooother conectividade. No entanto, os endereços IP Públicos utilizados pelos servidores da rede que comunicam com pontos finais do O365 dentro da Microsoft poderão ser anunciados através do ExpressRoute. 
> 
> 

## <a name="dynamic-route-exchange"></a>Troca de rotas dinâmicas

A troca do encaminhamento será feita através do protocolo eBGP. São estabelecidas sessões de EBGP entre Olá MSEEs e os routers. A autenticação das sessões de BGP não é um requisito. Se necessário, pode ser configurado um hash MD5. Consulte Olá [configurar encaminhamento](expressroute-howto-routing-classic.md) e [circuito Aprovisiona fluxos de trabalho e Estados de circuitos](expressroute-workflows.md) para obter informações sobre como configurar sessões de BGP.

## <a name="autonomous-system-numbers"></a>Números de Sistema Autónomos

A Microsoft utilizará AS 12076 para o peering público do Azure, o peering privado do Azure e o peering da Microsoft. Reservamos os ASNs do 65515 too65520 para utilização interna. São suportados números AS de 16 e de 32 bits.

Não há requisitos quanto à simetria da transferência de dados. caminhos de Olá reencaminhamento e do remetente podem atravessar pares de routers diferentes. As rotas idênticas têm de ser anunciadas nos dois lados nos vários pares de circuito que lhe pertençam. Métricas de rota não são necessária toobe idêntico.

## <a name="route-aggregation-and-prefix-limits"></a>Agregação de rotas e limites de prefixo

Fornecemos suporte de cópia de segurança too4000 prefixos anunciados toous através de Olá peering privado do Azure. Isto pode ser aumentado segurança too10, 000 prefixos se o suplemento premium do ExpressRoute de Olá estiver ativado. Podemos aceitar too200 prefixos por sessão BGP para o Azure público e peering da Microsoft. 

sessão de BGP Olá será ignorada se o número de Olá de prefixos exceder o limite de Olá. Aceitamos rotas predefinidas na Olá privada ligação peering apenas. Fornecedor tem de filtrar rota predefinida e endereços IP privados (RFC 1918) de Olá público do Azure e caminhos de peering da Microsoft. 

## <a name="transit-routing-and-cross-region-routing"></a>Encaminhamento de trânsito e encaminhamento por várias regiões

Não é possível encaminhar o ExpressRoute como router de trânsito. Irá ter toorely no seu fornecedor de conectividade para serviços de encaminhamento de trânsito.

## <a name="advertising-default-routes"></a>Anunciar rotas predefinidas

As rotas predefinidas só são permitidas em sessões do peering privado do Azure. Nesse caso, encaminharemos todo o tráfego de rede de tooyour Olá redes virtuais associadas. Anúncio de rotas predefinidas no peering privado resultará no caminho de internet Olá a partir do Azure que está a ser bloqueado. Dependem do tráfego de tooroute periferia empresarial do e toohello internet para serviços alojados no Azure. 

 tooenable conectividade tooother Azure serviços e serviços de infraestrutura, deve certificar-se um dos seguintes itens de Olá no local:

* Peering público do Azure está ativada tooroute tráfego toopublic os pontos finais
* Utilize definido pelo utilizador encaminhamento tooallow a conectividade à internet para cada sub-rede que exigem que a conectividade à Internet.

> [!NOTE]
> O anúncio de rotas predefinidas interrompe a ativação de licenças do Windows e de outras licenças de VMs. Siga as instruções [aqui](http://blogs.msdn.com/b/mast/archive/2015/05/20/use-azure-custom-routes-to-enable-kms-activation-with-forced-tunneling.aspx) toowork contornar esta situação.
> 
> 

## <a name="support-for-bgp-communities-preview"></a>Suporte para comunidades de BGP (pré-visualização)

Esta secção apresenta uma descrição geral de como as comunidades de BGP serão utilizadas com o ExpressRoute. A Microsoft anuncia as rotas de Olá público e caminhos de peering da Microsoft com rotas etiquetadas com valores de Comunidade apropriados. Olá lógica por detrás disto e Olá detalhes sobre a Comunidade valores são descritos abaixo. Microsoft, no entanto, não irão honrar qualquer Comunidade tooroutes marcado valores anunciados tooMicrosoft.

Se estiver a ligar tooMicrosoft através do ExpressRoute numa localização de peering numa região geopolítica, terá acesso tooall Microsoft cloud services em todas as regiões dentro dos limites geopolíticos OLÁ. 

Por exemplo, se ligado tooMicrosoft em Amesterdão através do ExpressRoute, terá acesso tooall cloud services da Microsoft alojados na Europa do Norte e Europa Ocidental. 

Consulte toohello [ExpressRoute parceiros e localizações de peering](expressroute-locations.md) página para uma lista detalhada das regiões geopolíticas, regiões do Azure associadas e das localizações de peering do ExpressRoute correspondentes.

Pode comprar mais do que um circuito do ExpressRoute por região geopolítica. Ter várias ligações oferece vantagens significativas de elevada disponibilidade devida toogeo-redundância. Nos casos em que tenha vários circuitos ExpressRoute, receberá Olá mesmo conjunto de prefixos anunciado da Microsoft em peering público do Olá e caminhos de peering da Microsoft. o que significa que terá vários caminhos da sua rede para a Microsoft. Isto pode provocar, potencialmente, toobe de decisões de encaminhamento inferiores às ideais na sua rede. Como resultado, pode deparar-serviços de toodifferent de experiências de conectividade inferiores às ideais. 

A Microsoft irá marcar prefixos anunciados através do peering público e peering da Microsoft com valores de Comunidade BGP adequados, com a indicação de prefixos de Olá Olá região está alojada no. Também pode utilizar Olá Comunidade valores toomake adequado encaminhamento decisões toooffer [toocustomers encaminhamento ideal](expressroute-optimize-routing.md).

| **Região Geopolítica** | **Região do Microsoft Azure** | **Valor da comunidade BGP** |
| --- | --- | --- |
| **América do Norte** | | |
| EUA Leste |12076:51004 | |
| EUA Leste 2 |12076:51005 | |
| EUA Oeste |12076:51006 | |
| EUA Oeste 2 |12076:51026 | |
| EUA Centro-Oeste |12076:51027 | |
| EUA Centro-Norte |12076:51007 | |
| EUA Centro-Sul |12076:51008 | |
| EUA Central |12076:51009 | |
| Canadá Central |12076:51020 | |
| Leste do Canadá |12076:51021 | |
| **América do Sul** | | |
| Sul do Brasil |12076:51014 | |
| **Europa** | | |
| Europa do Norte |12076:51003 | |
| Europa Ocidental |12076:51002 | |
| **Ásia-Pacífico** | | |
| Ásia Oriental |12076:51010 | |
| Sudeste Asiático |12076:51011 | |
| **Japão** | | |
| Leste do Japão |12076:51012 | |
| Oeste do Japão |12076:51013 | |
| **Austrália** | | |
| Leste da Austrália |12076:51015 | |
| Sudeste da Austrália |12076:51016 | |
| **Índia** | | |
| Índia do Sul |12076:51019 | |
| Índia Ocidental |12076:51018 | |
| Índia Central |12076:51017 | |

Todas as rotas anunciadas a partir da Microsoft serão etiquetadas com o valor do Olá da Comunidade adequado. 

> [!IMPORTANT]
> Os prefixos globais serão etiquetados com um valor da comunidade adequado e serão anunciados apenas quando o suplemento premium do ExpressRoute estiver ativado.
> 
> 

Além disso toohello acima, a Microsoft irá também marcar marcará prefixos baseados no serviço de Olá pertencem a. Isto aplica-se apenas toohello Microsoft peering. tabela de Olá abaixo fornece um mapeamento de valor de Comunidade do serviço tooBGP.

| **Serviço** | **Valor da comunidade BGP** |
| --- | --- |
| **Exchange** |12076:5010 |
| **SharePoint** |12076:5020 |
| **Skype para Empresas** |12076:5030 |
| **Dynamics 365** |12076:5040 |
| **Outros Serviços do Office 365** |12076:5100 |

> [!NOTE]
> A Microsoft não honra os valores das Comunidades BGP que definiu no Olá rotas anunciado tooMicrosoft.
> 
> 

## <a name="next-steps"></a>Passos seguintes

* Configurar a ligação do ExpressRoute.
  
  * [Criar um circuito de ExpressRoute para o modelo de implementação clássica Olá](expressroute-howto-circuit-classic.md) ou [criar e modificar um circuito ExpressRoute com o Azure Resource Manager](expressroute-howto-circuit-arm.md)
  * [Configurar o encaminhamento para o modelo de implementação clássica Olá](expressroute-howto-routing-classic.md) ou [configurar o encaminhamento para o modelo de implementação do Resource Manager Olá](expressroute-howto-routing-arm.md)
  * [Associar um tooan de VNet circuito de ExpressRoute clássico](expressroute-howto-linkvnet-classic.md) ou [ligação tooan uma VNet do Resource Manager circuito do ExpressRoute](expressroute-howto-linkvnet-arm.md)

