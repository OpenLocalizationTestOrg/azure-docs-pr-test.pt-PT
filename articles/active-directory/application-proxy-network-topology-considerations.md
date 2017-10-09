---
title: "considerações de topologia aaaNetwork quando utilizar o Proxy de aplicações do Azure Active Directory | Microsoft Docs"
description: "Abrange as considerações de topologia de rede ao utilizar o Proxy de aplicações do Azure AD."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/28/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 9b8cdd2196efeb92a74e44dde6511f7d3091a968
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="network-topology-considerations-when-using-azure-active-directory-application-proxy"></a>Considerações de topologia de rede ao utilizar o Proxy de aplicações do Azure Active Directory

Este artigo explica as considerações de topologia de rede ao utilizar o Proxy de aplicações do Azure Active Directory (Azure AD) para a publicar e aceder remotamente as suas aplicações.

## <a name="traffic-flow"></a>Fluxo de tráfego

Quando uma aplicação publicada através do Azure AD para o Proxy de aplicações, o tráfego de aplicações do Olá utilizadores toohello flui através de ligações de três:

1. utilizador de Olá liga toohello Proxy de aplicações do Azure AD pública ponto final de serviço no Azure
2. Olá serviço Proxy de aplicações liga toohello conector de Proxy de aplicações
3. conector do Proxy da aplicação Olá liga-se a aplicação de destino toohello

![Diagrama que mostra o fluxo de tráfego da aplicação de tootarget do utilizador](./media/application-proxy-network-topologies/application-proxy-three-hops.png)

## <a name="tenant-location-and-application-proxy-service"></a>Localização de inquilino e o serviço Proxy de aplicações

Quando se inscreve para um inquilino do Azure AD, região Olá do seu inquilino é determinado pelo país de Olá que especificar. Quando ativar o Proxy da aplicação, instâncias de serviço de Proxy da aplicação Olá para o seu inquilino são escolhidas ou criadas no Olá mesma região que o seu inquilino do Azure AD ou Olá tooit de região mais próxima.

Por exemplo, se a região do seu inquilino do Azure AD é Olá União Europeia (EU), todos os conectores de Proxy de aplicações a utilizam instâncias de serviço nos centros de dados do Azure no Olá EU. Quando o acesso de utilizadores a aplicações publicadas, o tráfego atravessa instâncias de serviço de Proxy da aplicação Olá nesta localização.

## <a name="considerations-for-reducing-latency"></a>Considerações para reduzir a latência

Todas as soluções de proxy introduzem latência na sua ligação de rede. Independentemente do que na solução de VPN ou de proxy escolher como solução de acesso remoto, sempre inclui um conjunto de servidores, permitindo Olá ligação tooinside a sua rede empresarial.

As organizações incluem, geralmente, os pontos finais do servidor na sua rede de perímetro. Com o Proxy de aplicações do Azure AD, no entanto, o tráfego flui através do serviço de proxy de Olá na nuvem de Olá enquanto conectores Olá residirem na sua rede empresarial. Não é necessária nenhuma rede de perímetro.

secções Olá contenham toohelp sugestões adicionais reduzir a latência de ainda mais. 

### <a name="connector-placement"></a>Posicionamento de conector

Proxy de aplicações escolhe localização Olá de instâncias para si, com base na sua localização de inquilino. No entanto, pode obter toodecide onde o conector de Olá tooinstall, dando-lhe Olá energia toodefine Olá latência as características de tráfego de rede.

Quando configurar Olá serviço Proxy de aplicações, peça ao hello seguintes perguntas:

* Onde está localizada a aplicação Olá?
* Onde estão a maioria dos utilizadores que acedem a aplicação Olá localizada?
* Onde está localizada a instância de Proxy da aplicação Olá?
* Já tem uma rede dedicada ligação tooAzure dos centros de dados configurados, como o Azure ExpressRoute ou uma VPN semelhante?

conector Olá tem toocommunicate com o Azure e as suas aplicações (os passos 2 e 3 no diagrama de fluxo de tráfego de Olá), por isso, Olá colocação de Olá conector afeta Olá latência dessas duas ligações. Ao avaliar a colocação de Olá do conector de Olá, tenha em Olá atenção os seguintes pontos:

* Se quiser toouse a delegação restrita de Kerberos (KCD) para o início de sessão único, conector Olá necessita de um centro de dados de tooa de linha de visão. Além disso, o servidor do conector Olá é associado a um domínio de toobe.  
* Quando em dúvida, instale a aplicação de toohello próximo do Olá conector.

### <a name="general-approach-toominimize-latency"></a>Latência de toominimize abordagem geral

Pode minimizar a latência de Olá de tráfego de ponto a ponto Olá por otimizar cada ligação de rede. Cada ligação pode ser otimizada por:

* Reduzir a distância Olá entre dois ends de Olá do salto de Olá.
* Escolher Olá tootraverse de rede à direita. Por exemplo, uma rede privada em vez de Olá a atravessar Internet pública pode ser mais rápida, que devem estar toodedicated ligações.

Se tiver uma ligação VPN ou ExpressRoute dedicada entre o Azure e a sua rede empresarial, poderá ser útil toouse que.

## <a name="focus-your-optimization-strategy"></a>Concentre-se a sua estratégia de otimização

Não há pouca que pode efetuar a ligação de Olá toocontrol entre os utilizadores e Olá serviço Proxy de aplicações. Os utilizadores podem aceder às suas aplicações de uma rede doméstica, num café ou noutro país. Em vez disso, pode otimizar a ligações de Olá de Olá Proxy da aplicação do serviço toohello Proxy de aplicações conectores toohello de aplicações. Considere a incorporar Olá seguintes padrões no seu ambiente.

### <a name="pattern-1-put-hello-connector-close-toohello-application"></a>Padrão de 1: Colocar Olá conector toohello fechar aplicação

Local Olá conector toohello fechar aplicação de destino na rede de cliente Olá. Esta configuração minimiza o passo 3 no diagrama de topografia Olá, porque o conector de Olá e aplicação fechar. 

Se o conector tem de um controlador de domínio de toohello de linha de visão, é vantajoso este padrão. A maioria dos nossos clientes utiliza este padrão, porque funciona bem para a maioria dos cenários. Este padrão também pode ser conjugado com o tráfego de 2 toooptimize padrão entre o serviço de Olá e conector Olá.

### <a name="pattern-2-take-advantage-of-expressroute-with-public-peering"></a>Padrão de 2: Tirar partido do ExpressRoute com o peering público

Se tiver configurado com um peering público do ExpressRoute, pode utilizar a ligação do ExpressRoute mais rápida Olá para o tráfego entre o Proxy de aplicações e conector Olá. o conector de Olá é ainda na sua rede, toohello fechar aplicação.

### <a name="pattern-3-take-advantage-of-expressroute-with-private-peering"></a>Padrão de 3: Tirar partido do ExpressRoute com o peering privado

Se tiver uma VPN dedicada ou ExpressRoute configurar com o peering privado entre o Azure e a sua rede empresarial, tem outra opção. Nesta configuração, a rede virtual do Olá no Azure, normalmente, é considerado como uma extensão de rede empresarial Olá. Por isso, pode instalar o conector de Olá no Olá datacenter do Azure e, ainda satisfazer requisitos de latência baixa Olá da ligação de conector para aplicação Olá.

Latência não fiquem comprometida porque o tráfego é que fluem através de uma ligação dedicada. Também obter a latência de conector do serviço de Proxy de aplicações melhorada porque o conector de Olá está instalado no tooyour de fechar datacenter do Azure a localização de inquilino do Azure AD.

![Diagrama que mostra o conector instalado dentro de um datacenter do Azure](./media/application-proxy-network-topologies/application-proxy-expressroute-private.png)

### <a name="other-approaches"></a>Outras abordagens

Embora este artigo aborda Olá colocação do conector, também pode alterar colocação Olá das características de latência Olá aplicação tooget melhor.

Cada vez mais, as organizações estiver a mover as respetivas redes em ambientes alojados. Isto permite-lhes tooplace as suas aplicações num ambiente alojado que também faz parte da sua rede empresarial e continuarão a estar dentro do domínio Olá. Neste caso, os padrões de Olá abordados Olá precedente secções podem ser aplicados toohello nova localização da aplicação. Se estiver a considerar esta opção, consulte o artigo [serviços de domínio do Azure AD](../active-directory-domain-services/active-directory-ds-overview.md).

Além disso, considere a organizar os conectores com [grupos conector](active-directory-application-proxy-connectors.md) tootarget aplicações que estão em diferentes localizações e as redes. 

## <a name="common-use-cases"></a>Casos de utilização comuns

Nesta secção, iremos guiá-lo através de alguns cenários comuns. Partem do princípio de que Olá inquilino do Azure AD (e, por conseguinte, o ponto final de serviço de proxy) está localizado na Olá dos Estados Unidos (EUA). Olá considerações abordadas estes casos de utilização também se aplicam tooother regiões à volta de globo Olá.

Nestes cenários, podemos chamar cada ligação de um "salto" e numbê-los para debate mais fácil:

- **Salto 1**: utilizador toohello serviço Proxy de aplicações
- **Salto 2**: o conector do Proxy de aplicações de toohello de serviço Proxy de aplicações
- **Salto 3**: aplicação de destino de toohello de conector de Proxy de aplicações 

### <a name="use-case-1"></a>Caso de utilização 1

**Cenário:** aplicação Olá estiver numa rede de uma organização no Olá US, com os utilizadores Olá mesma região. Existe a entre Olá datacenter do Azure e a rede empresarial Olá não ExpressRoute ou VPN.

**Recomendação:** siga padrão 1, explicado na secção anterior Olá. Para latência melhorada, considere utilizar o ExpressRoute, se necessário.

Este é um padrão simple. Otimizar o salto 3 colocando conector Olá junto da aplicação Olá. Também é uma escolha natural, porque o conector Olá normalmente é instalado com linha de visão toohello aplicação e toohello datacenter tooperform KCD operações.

![Diagrama que mostra que os utilizadores, proxy, conector e aplicações estão todos em Olá-nos](./media/application-proxy-network-topologies/application-proxy-pattern1.png)

### <a name="use-case-2"></a>Caso de utilização 2

**Cenário:** aplicação Olá estiver numa rede de uma organização no Olá US, com utilizadores distribuídos global. Existe a entre Olá datacenter do Azure e a rede empresarial Olá não ExpressRoute ou VPN.

**Recomendação:** siga padrão 1, explicado na secção anterior Olá. 

Novamente, Olá comuns padrão, é toooptimize salto 3, onde colocar o conector de Olá junto da aplicação Olá. Não é normalmente dispendioso, se for Olá todos no mesmo salto 3 região. No entanto, salto 1 pode ser mais dispendioso, dependendo de onde está o utilizador Olá, porque os utilizadores em Olá mundo tem aceder à instância de Proxy da aplicação Olá no Olá E.U.A.. É importante salientar que qualquer solução de proxy tem caraterísticas semelhantes sobre utilizadores que está a ser distribuídos globalmente.

![Diagrama que mostra que os utilizadores encontram-se distribuídas globalmente, mas Olá proxy, conector e aplicações estão numa Olá-nos](./media/application-proxy-network-topologies/application-proxy-pattern2.png)

### <a name="use-case-3"></a>Caso utilize 3

**Cenário:** aplicação Olá estiver numa rede de uma organização no Olá-nos. ExpressRoute com o peering público existe entre a rede empresarial do Azure e Olá.

**Recomendação:** siga padrões 1 e 2, explicado na secção anterior Olá.

Em primeiro lugar, coloque o conector Olá como fechar como aplicação toohello possíveis. Em seguida, sistema Olá utiliza automaticamente o ExpressRoute para o salto 2. 

Se a ligação de ExpressRoute Olá utilizar peering público, o tráfego de Olá entre proxy Olá e conector Olá flui através dessa ligação. Salto 2 otimizou latência.

![Diagrama que mostra o ExpressRoute entre Olá proxy e de conector](./media/application-proxy-network-topologies/application-proxy-pattern3.png)

### <a name="use-case-4"></a>Caso de utilização 4

**Cenário:** aplicação Olá estiver numa rede de uma organização no Olá-nos. ExpressRoute com o peering privado existe entre a rede empresarial do Azure e Olá.

**Recomendação:** siga padrão 3, explicado na secção anterior Olá.

Colocar conector Olá Olá datacenter do Azure que está ligado toohello rede empresarial através do peering privado do ExpressRoute. 

conector Olá pode ser colocado em Olá datacenter do Azure. Uma vez que o conector de Olá ainda tem uma linha de visão toohello aplicação e Olá Centro de dados através da rede privada Olá, salto 3 permanece otimizado. Além disso, salto 2 está otimizado adicional.

![Diagrama que mostra o conector Olá um datacenter do Azure e ExpressRoute entre conector Olá e aplicação](./media/application-proxy-network-topologies/application-proxy-pattern4.png)

### <a name="use-case-5"></a>Caso de utilização 5

**Cenário:** aplicação Olá estiver numa rede de uma organização no Olá EU, com a instância de Proxy da aplicação Olá e a maioria dos utilizadores no Olá-nos.

**Recomendação:** conector de Olá local junto da aplicação Olá. Porque os utilizadores de E.U.A. estão a aceder a uma instância de Proxy de aplicações que ocorre toobe no Olá mesma região, salto 1 não é demasiado caro. Salto 3 está otimizado. Considere utilizar o ExpressRoute toooptimize salto 2. 

![Diagrama que mostra os utilizadores e o proxy no Olá E.U.A., com o conector Olá e a aplicação no Olá EU](./media/application-proxy-network-topologies/application-proxy-pattern5b.png)

Também pode considerar a utilizar um outro variante nesta situação. Se a maioria dos utilizadores na organização de Olá estiverem em Olá dos EUA, possibilidades são que a rede expande toohello nos bem. Coloque o conector Olá no Olá E.U.A. e utilizar a aplicação de toohello de linha de rede empresarial interna Olá dedicado no Olá EU. Este saltos de forma 2 e 3 são otimizados.

![Diagrama que mostra os utilizadores, o proxy e o conector em Olá E.U.A., a aplicação no Olá EU](./media/application-proxy-network-topologies/application-proxy-pattern5c.png)

## <a name="next-steps"></a>Passos seguintes

- [Ativar o Proxy da aplicação](active-directory-application-proxy-enable.md)
- [Ativar o início de sessão único](active-directory-application-proxy-sso-using-kcd.md)
- [Ativar o acesso condicional](active-directory-application-proxy-conditional-access.md)
- [Resolver problemas com o Proxy da aplicação](active-directory-application-proxy-troubleshoot.md)
