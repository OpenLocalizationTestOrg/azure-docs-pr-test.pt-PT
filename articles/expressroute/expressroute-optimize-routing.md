---
title: 'Otimizar o encaminhamento do ExpressRoute: Azure | Microsoft Docs'
description: "Esta página fornece detalhes sobre como toooptimize encaminhamento quando tem mais do que uma ExpressRoute circuitos que estabelecer ligação entre a Microsoft e a sua rede empresarial."
documentationcenter: na
services: expressroute
author: charwen
manager: carmonm
editor: 
ms.assetid: fca53249-d9c3-4cff-8916-f8749386a4dd
ms.service: expressroute
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/06/2017
ms.author: charwen
ms.openlocfilehash: ebcfb638f67a9ac78c3e476668bfd0bb0ffb9985
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-expressroute-routing"></a>Otimizar o Encaminhamento do ExpressRoute
Quando tiver vários circuitos ExpressRoute, terá de tooMicrosoft de tooconnect mais do que um caminho. Como resultado, o encaminhamento inferior ao ideal – pode acontecer - ou seja, o tráfego pode demorar um tooreach de caminho mais longo Microsoft e Microsoft tooyour rede. Olá mais Olá caminho de rede, latência de Olá superior Olá. A latência tem um impacto direto no desempenho das aplicações e na experiência do utilizador. Este artigo ilustra este problema e explica como toooptimize encaminhamento utilizando Olá tecnologias de encaminhamento padrão.

## <a name="suboptimal-routing-from-customer-toomicrosoft"></a>Inferior ao ideal de encaminhamento de tooMicrosoft de cliente
Vamos analisar problema de encaminhamento Olá por um exemplo. Imagine que tem dois escritórios no Olá E.U.A., um em Los Angeles e outro em Nova Iorque. Os escritórios estão ligados através de uma Rede Alargada (WAN), que pode ser a sua própria rede principal ou a VPN de IP do seu fornecedor de serviços. Tem dois circuitos do ExpressRoute, um nos EUA oeste e o outro nos EUA leste, que também estão ligados Olá WAN. Obviamente, tem dois caminhos tooconnect toohello Microsoft network. Imagine agora que tem a implementação do Azure (por exemplo, o Serviço de Aplicações do Azure) nos E.U.A. Oeste e nos E.U.A. Leste. A intenção é tooconnect os utilizadores em Los Angeles tooAzure dos EUA oeste e os utilizadores em Nova Iorque tooAzure dos EUA leste, porque o seu administrador de serviços anuncia que os utilizadores em cada acesso office Olá próximas serviços do Azure para uma experiência ideal. Infelizmente, Olá plano funciona bem para utilizadores da costa leste de Olá, mas não para os utilizadores da costa oeste do Olá. causa Olá problema Olá é seguinte Olá. Em cada circuito do ExpressRoute, estamos a anunciar tooyou ambos prefixo Olá no Azure dos EUA Leste (23.100.0.0/16) e o prefixo de Olá no Azure dos EUA oeste (13.100.0.0/16). Se não souber que prefixo corresponde a que região, não é tootreat capaz de forma diferente. A rede WAN poderá achar que ambos os prefixos de Olá são próximo Leste tooUS que dos EUA oeste e, por conseguinte, encaminhar ambos os toohello de utilizadores do office circuito do ExpressRoute nos EUA Leste. No final de Olá, terá muitos utilizadores insatisfeitos no Olá escritório em Los Angeles.

![Problema de ExpressRoute caso 1 - inferior ao ideal de encaminhamento de tooMicrosoft de cliente](./media/expressroute-optimize-routing/expressroute-case1-problem.png)

### <a name="solution-use-bgp-communities"></a>Solução: utilizar Comunidades do BGP
toooptimize encaminhamento para ambos os utilizadores do office, terá de tooknow que prefixo corresponde a partir do Azure dos EUA oeste e qual a Azure dos EUA Leste. Codificamos estas informações com os [Valores das Comunidades do BGP](expressroute-routing.md). Atribuímos um tooeach de valor das Comunidades do BGP exclusivo região do Azure, por exemplo “12076:51004” para EUA Leste e “12076:51006” para EUA Oeste. Agora que sabe que prefixo corresponde a que região do Azure, já pode configurar que circuito do ExpressRoute deve ser o preferencial. Uma vez que utilizamos informações de encaminhamento do tooexchange Olá BGP, pode utilizar o encaminhamento de BGP preferência Local tooinfluence. No nosso exemplo, pode atribuir um maior preferência local valor too13.100.0.0/16 nos EUA oeste que nos EUA leste e da mesma forma, um maior preferência local valor too23.100.0.0/16 nos EUA Leste que nos EUA oeste. Esta configuração permitirá garantir que, quando os dois caminhos tooMicrosoft estão disponíveis, os utilizadores em Los Angeles demorará circuito do ExpressRoute Olá nos EUA oeste tooconnect tooAzure dos EUA oeste, ao passo que os utilizadores em Nova Iorque demorar Olá ExpressRoute nos EUA Leste tooAzure dos EUA leste . O encaminhamento fica otimizado em ambos os lados. 

![Solução do Caso 1 do ExpressRoute - utilizar Comunidades do BGP](./media/expressroute-optimize-routing/expressroute-case1-solution.png)

> [!NOTE]
> Olá técnica mesma, utilizando a preferência Local, pode ser aplicado toorouting do cliente tooAzure rede Virtual. Iremos não etiquetar os prefixos toohello de valor das Comunidades do BGP anunciados a partir da rede tooyour do Azure. No entanto, uma vez que já sabe que a implementação de rede Virtual está a fechar toowhich do seu escritório, pode configurar os routers em conformidade tooprefer um tooanother de circuito de ExpressRoute.
>
>

## <a name="suboptimal-routing-from-microsoft-toocustomer"></a>Inferior ao ideal de encaminhamento de toocustomer da Microsoft
Aqui é o outro exemplo em que as ligações da Microsoft demorar um tooreach de caminho mais longo sua rede. Neste caso, está a utilizar servidores do Exchange no local e o Exchange Online num [ambiente híbrido](https://technet.microsoft.com/library/jj200581%28v=exchg.150%29.aspx). Os escritórios estão ligado tooa WAN. Anunciar prefixos Olá dos seus servidores no local em ambos os seus tooMicrosoft escritórios através de circuitos do ExpressRoute Olá dois. Exchange Online irá iniciar servidores no local de toohello de ligações em casos como a migração de caixa de correio. Infelizmente, Olá ligação tooyour escritório em Los Angeles é encaminhada toohello circuito do ExpressRoute nos EUA Leste atravessando da costa oeste do Olá todo toohello back continente antes. Olá causa do problema Olá é semelhante toohello primeiro um. Sem sugestões, a rede da Microsoft Olá não é possível dizer que prefixos do cliente está a fechar Leste tooUS e qual delas é fechar tooUS oeste. Ocorre office do toopick Olá caminho incorreto tooyour em Los Angeles.

![ExpressRoute caso 2 - inferior ao ideal de encaminhamento de toocustomer da Microsoft](./media/expressroute-optimize-routing/expressroute-case2-problem.png)

### <a name="solution-use-as-path-prepending"></a>Solução: utilizar prefixação COMO CAMINHO
Existem dois problema de toohello soluções. Olá primeiro um é simplesmente anunciar o prefixo no local para o seu escritório em Los Angeles, 177.2.0.0/31, no circuito de ExpressRoute Olá nos EUA oeste e o prefixo no local para o seu escritório de Nova Iorque, 177.2.0.2/31, no circuito de ExpressRoute Olá nos EUA Leste. Como resultado, é apenas um caminho para a Microsoft tooconnect tooeach dos seus escritórios. Não há ambiguidade e o encaminhamento é otimizado. Com esta conceção, terá de toothink sobre a sua estratégia de ativação pós-falha. No Olá eventos Olá tooMicrosoft caminho através do ExpressRoute for interrompido, tem de certificar-se de que Exchange Online ainda conseguir ligar servidores no local de tooyour toomake. 

solução segundo Olá é que continuar tooadvertise dos prefixos Olá em ambos os circuitos ExpressRoute e, além disso, dar-numa sugestão de qual prefixo é toowhich fechar um dos seus escritórios. Porque suportamos a prefixação como caminho do BGP, pode configurar Olá como caminho para o encaminhamento de tooinfluence de prefixo. Neste exemplo, pode aumentar a prefixação como caminho de Olá para 172.2.0.0/31 nos EUA leste, para que preferirmos circuito de ExpressRoute Olá nos EUA oeste para o tráfego destinado a este prefixo (uma vez que a nossa rede irá considerar Olá caminho toothis prefixo é constituído pelos mais curto no Oeste Olá). Da mesma forma pode aumentar a prefixação como caminho de Olá para 172.2.0.2/31 nos EUA oeste para que a preferirmos o circuito de ExpressRoute Olá nos EUA Leste. O encaminhamento fica otimizado para ambos os escritórios. Com esta estrutura, se um circuito do ExpressRoute for interrompido, o Exchange Online ainda consegue contactá-lo através de outro circuito do ExpressRoute e da sua WAN. 

> [!IMPORTANT]
> Removemos privada como números existentes na Olá como caminho para os prefixos de Olá receberam no Peering da Microsoft. Terá de tooappend números públicos como no Olá como caminho tooinfluence encaminhamento para Peering da Microsoft.
> 
> 

![Solução do Caso 2 do ExpressRoute - utilizar prefixação COMO CAMINHO](./media/expressroute-optimize-routing/expressroute-case2-solution.png)

> [!NOTE]
> Enquanto são exemplos de Olá fornecidos aqui para peerings público e da Microsoft, suportamos Olá as mesmas capacidades para peering privado do Olá. Além disso, prefixação como caminho de Olá funciona dentro de um único circuito do ExpressRoute, seleção de Olá tooinfluence dos caminhos de Olá primária e secundária.
> 
> 

## <a name="suboptimal-routing-between-virtual-networks"></a>Encaminhamento inferior ao ideal entre redes virtuais
Com o ExpressRoute, pode ativar a rede Virtual tooVirtual rede (que também é conhecido como "VNet") comunicação associando-los tooan circuito do ExpressRoute. Encaminhamento inferior ao ideal – pode acontecer quando a ligá-las toomultiple circuitos do ExpressRoute, entre Olá VNets. Vamos considerar um exemplo. Tem dois circuitos do ExpressRoute, um nos E.U.A. Oeste e outro nos E.U.A. Leste. Em cada região, tem duas VNets. Os servidores web são implementados numa VNet e servidores de aplicações em Olá outros. Para a redundância, a ligação Olá duas VNets em cada região tooboth Olá local circuito do ExpressRoute e Olá remoto circuito do ExpressRoute. Como é apresentada abaixo, a partir de cada VNet existem dois caminhos toohello outra VNet. Olá VNets não souber que circuito do ExpressRoute é local e que é remoto. Por conseguinte como fazem igual-custo várias-Path (ECMP) encaminhamento tooload-equilibrar inter-VNet o tráfego, alguns fluxos de tráfego irão demorar caminho mais longo Olá e obterem encaminhados no circuito de ExpressRoute remoto Olá.

![Caso 3 do ExpressRoute - encaminhamento inferior ao ideal entre redes virtuais](./media/expressroute-optimize-routing/expressroute-case3-problem.png)

### <a name="solution-assign-a-high-weight-toolocal-connection"></a>Solução: atribuir uma ligação de toolocal importância elevada
solução Olá é simple. Uma vez que já sabe onde estão os circuitos VNets e Olá Olá, pode diga-nos de caminho no qual deve preferir cada VNet. Especificamente para este exemplo, pode designar uma maior ponderação toohello ligação de local de ligação remota toohello (consulte exemplo de configuração de Olá [aqui](expressroute-howto-linkvnet-arm.md#modify-a-virtual-network-connection)). Quando uma VNet recebe prefixo Olá Olá outra VNet em várias ligações preferirão ligação Olá com Olá maior ponderação toosend tráfego destinado a esse prefixo.

![Solução do ExpressRoute cenário 3 - atribuir importância elevada toolocal ligação](./media/expressroute-optimize-routing/expressroute-case3-solution.png)

> [!NOTE]
> Também pode influenciar o encaminhamento de rede do VNet tooyour no local, se tiver vários circuitos do ExpressRoute, configurando o peso Olá de uma ligação em vez de aplicar como caminho prefixação uma técnica descrita Olá segundo cenário acima. Para cada prefixo sempre veremos peso de ligação de Olá antes Olá comprimento como caminho ao decidir como toosend tráfego.
>
>
