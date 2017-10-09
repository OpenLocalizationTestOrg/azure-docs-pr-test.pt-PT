---
title: aaaConfigure uma rede Virtual para uma Cache de Redis do Azure Premium | Microsoft Docs
description: "Saiba como toocreate e gerir o suporte de rede Virtual para as instâncias de Cache de Redis do Azure do escalão Premium"
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: 8b1e43a0-a70e-41e6-8994-0ac246d8bf7f
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: sdanie
ms.openlocfilehash: fab715f4d9365ee4c2f8b89d2e2e58768c25b671
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-virtual-network-support-for-a-premium-azure-redis-cache"></a>Como tooconfigure suporta a rede Virtual para uma Cache de Redis do Azure Premium
Cache de Redis do Azure tem ofertas de cache diferente, que fornecem flexibilidade na escolha de Olá de tamanho da cache e funcionalidades, incluindo as funcionalidades do escalão Premium, tais como clustering, persistência e suporte de rede virtual. Uma VNet é uma rede privada na nuvem de Olá. Quando uma instância da Cache de Redis do Azure está configurada com uma VNet, não é acessível publicamente e só pode ser acedido a partir de máquinas virtuais e aplicações dentro de Olá VNet. Este artigo descreve como a rede virtual tooconfigure suportam para uma instância de Cache de Redis do Azure premium.

> [!NOTE]
> Cache de Redis do Azure suporta tanto clássico e as VNets do Resource Manager.
> 
> 

Para obter informações sobre outras funcionalidades de cache premium, consulte [introdução toohello Azure Redis escalão Premium da Cache](cache-premium-tier-intro.md).

## <a name="why-vnet"></a>Por que motivo VNet?
[Rede Virtual do Azure (VNet)](https://azure.microsoft.com/services/virtual-network/) implementação proporciona maior segurança e isolamento para a Cache de Redis do Azure, bem como sub-redes, políticas de controlo de acesso e outra funcionalidades toofurther restringir o acesso.

## <a name="virtual-network-support"></a>Suporte de rede virtual
Suporte da virtual Network (VNet) é configurado no Olá **nova Cache de Redis** painel durante a criação da cache. 

[!INCLUDE [redis-cache-create](../../includes/redis-cache-premium-create.md)]

Assim que tiver selecionado um escalão de preços premium, pode configurar a integração de Redis VNet selecionando uma VNet que está a ser Olá mesma subscrição e localização da cache. toouse uma nova VNet, criá-la primeiro ao seguir os passos de Olá em [criar uma rede virtual com o portal do Azure de Olá](../virtual-network/virtual-networks-create-vnet-arm-pportal.md) ou [criar uma rede virtual (clássica) utilizando o portal do Azure de Olá](../virtual-network/virtual-networks-create-vnet-classic-pportal.md) e, em seguida, devolver toohello **Nova Cache de Redis** toocreate de painel e configurar a cache de premium.

tooconfigure Olá VNet para a nova cache, clique em **rede Virtual** no Olá **nova Cache de Redis** painel e selecione Olá pretendido VNet de Olá na lista pendente.

![Rede virtual][redis-cache-vnet]

Selecione Olá sub-rede pretendido de Olá **sub-rede** pendente lista e especifique Olá pretendido **endereço IP estático**. Se estiver a utilizar um Olá VNet clássica **endereço IP estático** campo é opcional e, se for especificado nenhum, um é escolhido de sub-rede Olá selecionado.

> [!IMPORTANT]
> Quando implementar um tooa a Cache de Redis do Azure VNet do Resource Manager, tem de ser cache Olá numa sub-rede dedicada que contém outros recursos de exceto instâncias de Cache de Redis do Azure. Se for feita uma tentativa de toodeploy tooa uma Cache de Redis do Azure VNet do Resource Manager tooa sub-rede que contém outros recursos, a implementação de Olá falha.
> 
> 

![Rede virtual][redis-cache-vnet-ip]

> [!IMPORTANT]
> Azure reserva-se alguns endereços IP dentro de cada sub-rede e estes endereços não podem ser utilizados. Olá primeiro e últimos endereços IP de sub-redes de Olá estão reservados para compatibilidade com o protocolo, juntamente com três endereços mais utilizados para serviços do Azure. Para obter mais informações, consulte [existem restrições sobre como utilizar estas sub-redes de endereços IP?](../virtual-network/virtual-networks-faq.md#are-there-any-restrictions-on-using-ip-addresses-within-these-subnets)
> 
> Adição de endereços IP toohello utilizado pela infraestrutura de VNET do Azure Olá, cada Redis instância Olá sub-rede utiliza dois endereços IP por ID de partição horizontal e um endereço IP adicional Olá Balanceador de carga. Uma cache agrupado é considerada um de toohave partições horizontais.
> 
> 

Depois de criar a cache de Olá, pode ver configuração Olá Olá VNet clicando **rede Virtual** de Olá **menu recursos**.

![Rede virtual][redis-cache-vnet-info]

tooconnect tooyour Azure Redis cache instância quando utilizar uma VNet, especifique o nome de anfitrião de Olá da cache na cadeia de ligação de Olá conforme mostrado no seguinte exemplo de Olá:

    private static Lazy<ConnectionMultiplexer> lazyConnection = new Lazy<ConnectionMultiplexer>(() =>
    {
        return ConnectionMultiplexer.Connect("contoso5premium.redis.cache.windows.net,abortConnect=false,ssl=true,password=password");
    });

    public static ConnectionMultiplexer Connection
    {
        get
        {
            return lazyConnection.Value;
        }
    }

## <a name="azure-redis-cache-vnet-faq"></a>Cache de Redis do Azure VNet FAQ
Olá seguinte lista contém toocommonly respostas perguntas mais sobre o dimensionamento do Olá a Cache de Redis do Azure.

* [Quais são alguns problemas de configuração incorreta comum com a Cache de Redis do Azure e as VNets?](#what-are-some-common-misconfiguration-issues-with-azure-redis-cache-and-vnets)
* [Como verificar se a minha cache está a funcionar numa VNET?](#how-can-i-verify-that-my-cache-is-working-in-a-vnet)
* [Pode utilizar as VNets com uma cache básica ou padrão?](#can-i-use-vnets-with-a-standard-or-basic-cache)
* [Por que motivo criar uma cache de Redis falha na algumas sub-redes, mas não a outros utilizadores?](#why-does-creating-a-redis-cache-fail-in-some-subnets-but-not-others)
* [Quais são os requisitos de espaço de endereço de sub-rede Olá?](#what-are-the-subnet-address-space-requirements)
* [Todas as funcionalidades de cache funcionam quando alojam uma cache numa VNET?](#do-all-cache-features-work-when-hosting-a-cache-in-a-vnet)

## <a name="what-are-some-common-misconfiguration-issues-with-azure-redis-cache-and-vnets"></a>Quais são alguns problemas de configuração incorreta comum com a Cache de Redis do Azure e as VNets?
Quando a Cache de Redis do Azure está alojada numa VNet, portas de Olá no Olá tabelas a seguir são utilizadas. 

>[!IMPORTANT]
>Se estiverem bloqueadas portas Olá Olá tabelas a seguir, a cache de Olá poderá não funcionar corretamente. Um ou mais destas portas bloqueadas é ter problema de configuração incorreta mais comuns Olá ao utilizar a Cache de Redis do Azure numa VNet.
> 
> 

- [Requisitos de porta de saída](#outbound-port-requirements)
- [Requisitos de porta de entrada](#inbound-port-requirements)

### <a name="outbound-port-requirements"></a>Requisitos de porta de saída

Existem sete requisitos de porta de saída.

- Se assim o desejar, todas as ligações de saída toohello, internet pode ser efetuadas através de um cliente no local auditoria do dispositivo.
- Três portas Olá encaminhar pontos finais de tooAzure de tráfego de manutenção do armazenamento do Azure e o DNS do Azure.
- Olá restantes intervalos de portas e para comunicações de sub-rede internas do Redis. Não existem regras NSG de sub-rede são necessárias para comunicações de sub-rede internas do Redis.

| Portas | Direção | Protocolo de transporte | Objetivo | Local IP | IP remoto |
| --- | --- | --- | --- | --- | --- |
| 80, 443 |Saída |TCP |Redis dependências no Azure armazenamento/PKI (Internet) | (Redis sub-rede) |* |
| 53 |Saída |TCP/UDP |Redis dependências no DNS (Internet/VNet) | (Redis sub-rede) |* |
| 8443 |Saída |TCP |Comunicações internas para Redis | (Redis sub-rede) | (Redis sub-rede) |
| 10221-10231 |Saída |TCP |Comunicações internas para Redis | (Redis sub-rede) | (Redis sub-rede) |
| 20226 |Saída |TCP |Comunicações internas para Redis | (Redis sub-rede) |(Redis sub-rede) |
| 13000-13999 |Saída |TCP |Comunicações internas para Redis | (Redis sub-rede) |(Redis sub-rede) |
| 15000-15999 |Saída |TCP |Comunicações internas para Redis | (Redis sub-rede) |(Redis sub-rede) |


### <a name="inbound-port-requirements"></a>Requisitos de porta de entrada

Existem oito requisitos de intervalo de portas de entrada. Pedidos de entrada nestes intervalos são uma entrada de outros serviços alojados no Olá mesma VNET ou toohello interno comunicações de sub-rede de Redis.

| Portas | Direção | Protocolo de transporte | Objetivo | Local IP | IP remoto |
| --- | --- | --- | --- | --- | --- |
| 6379, 6380 |Entrada |TCP |TooRedis de comunicação de cliente, Azure balanceamento de carga | (Redis sub-rede) |Rede virtual, o Balanceador de carga do Azure |
| 8443 |Entrada |TCP |Comunicações internas para Redis | (Redis sub-rede) |(Redis sub-rede) |
| 8500 |Entrada |TCP/UDP |Balanceamento de carga do Azure | (Redis sub-rede) |Azure Load Balancer |
| 10221-10231 |Entrada |TCP |Comunicações internas para Redis | (Redis sub-rede) |(Redis sub-rede), o Balanceador de carga do Azure |
| 13000-13999 |Entrada |TCP |Comunicação de cliente tooRedis Clusters de balanceamento de carga do Azure | (Redis sub-rede) |Rede virtual, o Balanceador de carga do Azure |
| 15000-15999 |Entrada |TCP |TooRedis de comunicação de cliente do Azure, Clusters de balanceamento de carga | (Redis sub-rede) |Rede virtual, o Balanceador de carga do Azure |
| 16001 |Entrada |TCP/UDP |Balanceamento de carga do Azure | (Redis sub-rede) |Azure Load Balancer |
| 20226 |Entrada |TCP |Comunicações internas para Redis | (Redis sub-rede) |(Redis sub-rede) |

### <a name="additional-vnet-network-connectivity-requirements"></a>Requisitos de conectividade de rede VNET adicionais

Existem requisitos de conectividade de rede do Azure Redis Cache que não pode ser cumprido inicialmente numa rede virtual. Cache de Redis do Azure requer que todos os Olá os seguintes itens toofunction corretamente quando utilizada dentro de uma rede virtual.

* Rede de saída conectividade tooAzure pontos finais do Storage em todo o mundo. Isto inclui pontos finais localizados em Olá mesma região que a instância da Cache de Redis do Azure de Olá, bem como pontos finais de armazenamento localizados na **outros** regiões do Azure. Pontos finais de armazenamento do Azure resolver em Olá seguintes domínios DNS: *w*, *w*, *q*e *w*. 
* Saída conectividade de rede demasiado*ocsp.msocsp.com*, *mscrl.microsoft.com*, e *crl.microsoft.com*. Este conectividade é a funcionalidade SSL toosupport necessários.
* configuração de DNS de Olá de rede virtual Olá deve ser capaz de resolver todos os pontos finais de Olá e domínios mencionados Olá pontos anteriores. Podem ser cumpridos estes requisitos de DNS, assegurando que configurada e mantida na rede virtual Olá uma infraestrutura de DNS válida.
* Toohello de conectividade de rede de saída seguindo Azure pontos finais de monitorização, que resolver em Olá seguintes domínios DNS: shoebox2 black.shoebox2.metrics.nsatc.net, Norte-prod2.prod2.metrics.nsatc.net azglobal-black.azglobal.metrics.nsatc.net, shoebox2-red.shoebox2.metrics.nsatc.net, Leste-prod2.prod2.metrics.nsatc.net azglobal-red.azglobal.metrics.nsatc.net.

### <a name="how-can-i-verify-that-my-cache-is-working-in-a-vnet"></a>Como verificar se a minha cache está a funcionar numa VNET?

>[!IMPORTANT]
>Ao ligar a instância de Cache de Redis do Azure tooan que está alojada numa VNET, cache, os clientes têm de estar em Olá mesma VNET, incluindo aplicações de teste ou ferramentas de diagnóstico efetuando o ping.
>
>

Depois dos requisitos de portas de Olá estiverem configurados, conforme descrito na secção anterior Olá, pode verificar a sua cache está a funcionar, efetuando Olá os seguintes passos.

- [Reiniciar](cache-administration.md#reboot) todas Olá nós em cache. Se todos os Olá necessário dependências de cache não não possível aceder (conforme documentado no [requisitos de portas de entrada](cache-how-to-premium-vnet.md#inbound-port-requirements) e [requisitos de porta de saída](cache-how-to-premium-vnet.md#outbound-port-requirements)), cache Olá não será capaz de toorestart com êxito.
- Depois de nós de cache de Olá reiniciaram (conforme comunicado pelo Estado da cache Olá Olá portal do Azure), pode efetuar Olá seguintes testes:
  - enviar um ping Olá ponto final da cache (utilizando a porta 6380) de uma máquina que esteja dentro do Olá mesma VNET, como Olá colocar em cache, utilizando [tcping](https://www.elifulkerson.com/projects/tcping.php). Por exemplo:
    
    `tcping.exe contosocache.redis.cache.windows.net 6380`
    
    Se hello `tcping` ferramenta relatórios que Olá porta está aberta, a cache de Olá está disponível para a ligação de clientes no Olá VNET.

  - Outra forma tootest é toocreate um cliente de cache de teste (que pode ser uma simples aplicação de consola com stackexchange. redis) que liga toohello cache e adiciona e obtém alguns itens da cache de Olá. Instalar a aplicação de cliente de exemplo de Olá para uma VM que está a ser Olá mesma VNET, como cache de Olá e execute-a cache de toohello tooverify conectividade.


### <a name="can-i-use-vnets-with-a-standard-or-basic-cache"></a>Pode utilizar as VNets com uma cache básica ou padrão?
As VNets só pode ser utilizadas com premium caches.

### <a name="why-does-creating-a-redis-cache-fail-in-some-subnets-but-not-others"></a>Por que motivo criar uma cache de Redis falha na algumas sub-redes, mas não a outros utilizadores?
Se estiver a implementar um tooa a Cache de Redis do Azure VNet do Resource Manager, tem de ser cache Olá numa sub-rede dedicada com nenhum outro tipo de recurso. Se for feita uma tentativa de toodeploy tooa uma Cache de Redis do Azure sub-rede da VNet do Resource Manager que contém outros recursos, a implementação de Olá falha. Tem de eliminar recursos existentes de Olá dentro de sub-rede Olá antes de poder criar uma nova cache de Redis.

Pode implementar vários tipos de recursos tooa VNet clássica, desde que tem suficiente IP endereços disponíveis.

### <a name="what-are-hello-subnet-address-space-requirements"></a>Quais são os requisitos de espaço de endereço de sub-rede Olá?
Azure reserva-se alguns endereços IP dentro de cada sub-rede e estes endereços não podem ser utilizados. Olá primeiro e últimos endereços IP de sub-redes de Olá estão reservados para compatibilidade com o protocolo, juntamente com três endereços mais utilizados para serviços do Azure. Para obter mais informações, consulte [existem restrições sobre como utilizar estas sub-redes de endereços IP?](../virtual-network/virtual-networks-faq.md#are-there-any-restrictions-on-using-ip-addresses-within-these-subnets)

Adição de endereços IP toohello utilizado pela infraestrutura de VNET do Azure Olá, cada Redis instância Olá sub-rede utiliza dois endereços IP por ID de partição horizontal e um endereço IP adicional Olá Balanceador de carga. Uma cache agrupado é considerada um de toohave partições horizontais.

### <a name="do-all-cache-features-work-when-hosting-a-cache-in-a-vnet"></a>Todas as funcionalidades de cache funcionam quando alojam uma cache numa VNET?
Quando a cache faz parte de uma VNET, apenas os clientes Olá VNET podem aceder à cache de Olá. Como resultado, hello seguintes funcionalidades de gestão de cache não funcionam neste momento.

* Consola de redis - porque consola Redis é executado no seu browser local, o que está fora Olá VNET, não é possível ligar tooyour cache.

## <a name="use-expressroute-with-azure-redis-cache"></a>Utilizar o ExpressRoute com a Cache de Redis do Azure
Os clientes podem ligar-se um [Azure ExpressRoute](https://azure.microsoft.com/services/expressroute/) infraestrutura de rede virtual tootheir de circuito, deste modo, expandir os respetivos tooAzure de rede no local. 

Por predefinição, um circuito ExpressRoute criado recentemente não pratica a imposição do túnel (anúncio de uma rota predefinida, 0.0.0.0/0) na VNET. Como resultado, conectividade de Internet de saída é permitida diretamente a partir de Olá VNET e aplicações de cliente são tooother tooconnect capaz de Azure pontos finais, incluindo a Cache de Redis do Azure.

No entanto uma configuração de cliente comum é toouse imposição do túnel (anunciar uma rota predefinida) que força a saída Internet tráfego tooinstead fluxo no local. Este fluxo de tráfego de quebras de conectividade com a Cache de Redis do Azure se o tráfego de saída Olá, em seguida, bloqueado no local que hello instância da Cache de Redis do Azure não é possível toocommunicate com as respetivas dependências.

solução de Olá é toodefine um (ou mais) definido pelo utilizador rotas (UDRs) na sub-rede Olá que contém Olá a Cache de Redis do Azure. Um UDR define as rotas de sub-rede específicos que serão cumpridas em vez de rota predefinida de Olá.

Se for possível, recomenda-se Olá toouse seguinte configuração:

* configuração do ExpressRoute Olá anuncia 0.0.0.0/0 e por predefinição, force túneis todos os tráfego de saída no local.
* Olá UDR aplicada toohello sub-rede que contém Olá a Cache de Redis do Azure define 0.0.0.0/0 com uma rota de trabalho para TCP/IP tráfego toohello internet pública; Por exemplo pela definição Olá próximo salto too'Internet de tipo '.

Olá efeito combinado destes passos é que o nível de sub-rede Olá UDR tem precedência sobre Olá ExpressRoute imposição do túnel, que garante a saída acesso à Internet de Olá a Cache de Redis do Azure.

Instância de Cache de Redis do Azure tooan ao ligar a uma aplicação no local com o ExpressRoute não é um cenário de utilização normal devido a razões tooperformance (para um melhor desempenho a Cache de Redis do Azure, os clientes devem estar em Olá mesma região que Olá a Cache de Redis do Azure).

>[!IMPORTANT] 
>Olá rotas definidas num UDR **tem** ser específico o suficiente tootake precedência sobre qualquer rotas anunciadas pela configuração do ExpressRoute Olá. Olá exemplo seguinte utiliza o intervalo de endereços Olá 0.0.0.0/0 abrangente e como tal, pode potencialmente ser acidentalmente substituído pelo anúncios de rota utilizando intervalos de endereços mais específicos.

>[!WARNING]  
>Cache de Redis do Azure não é suportado com configurações de ExpressRoute que **incorretamente cross-anunciar rotas de Olá caminho toohello privada peering caminho de peering público**. Configurações de ExpressRoute que tenham o peering público configurado, receber anúncios de rota da Microsoft para um grande conjunto de intervalos de endereços IP do Microsoft Azure. Se estes intervalos de endereços são incorretamente cross-anunciados no caminho de peering privado Olá, o resultado de Olá é que todos os pacotes de rede de saída da sub-rede de instância Cache de Redis do Azure Olá são rede no local de tooa incorretamente force-em túnel do cliente infraestrutura. Este fluxo de rede de quebras de Cache de Redis do Azure. problema de toothis Olá solução é rotas de publicidade entre toostop de Olá caminho toohello privada peering caminho de peering público.


Informações de fundo sobre rotas definidas pelo utilizador estão disponíveis neste [descrição geral](../virtual-network/virtual-networks-udr-overview.md).

Para obter mais informações sobre o ExpressRoute, consulte [descrição geral técnica do ExpressRoute](../expressroute/expressroute-introduction.md).

## <a name="next-steps"></a>Passos seguintes
Saiba como toouse mais premium cache funcionalidades.

* [Introdução toohello Azure Redis escalão Premium da Cache](cache-premium-tier-intro.md)

<!-- IMAGES -->

[redis-cache-vnet]: ./media/cache-how-to-premium-vnet/redis-cache-vnet.png

[redis-cache-vnet-ip]: ./media/cache-how-to-premium-vnet/redis-cache-vnet-ip.png

[redis-cache-vnet-info]: ./media/cache-how-to-premium-vnet/redis-cache-vnet-info.png

