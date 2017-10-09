---
title: 'Configurar filtros de rota para peering de ExpressRoute ao Microsoft Azure: Portal | Microsoft Docs'
description: "Este artigo descreve como tooconfigure filtros de rota para Peering da Microsoft utilizando Olá portal do Azure"
documentationcenter: na
services: expressroute
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/25/2017
ms.author: ganesr;cherylmc
ms.openlocfilehash: 2a47d465ec5f175d9510cef94606f70f036f0862
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-route-filters-for-microsoft-peering"></a>Configurar filtros de rota para o peering da Microsoft

Filtros de rota são uma forma tooconsume um subconjunto de serviços suportados através do peering da Microsoft. passos seguintes Olá nesta ajuda de artigo, configurar e gerir filtros de rota para circuitos do ExpressRoute.

Serviços de Dynamics 365 e serviços do Office 365, como o Exchange Online, SharePoint Online e Skype para empresas, estão acessíveis através do peering da Microsoft hello. Ao peering da Microsoft está configurado num circuito do ExpressRoute, todos os serviços de toothese relacionados prefixos estão anunciados através de sessões de BGP de Olá que são estabelecidas. Um valor das Comunidades de BGP é anexado tooevery prefixo tooidentify Olá serviço é fornecido através de prefixo de Olá. Para obter uma lista de valores das Comunidades BGP Olá e mapeiam para os serviços de Olá, consulte [Comunidades BGP](expressroute-routing.md#bgp).

Se necessitar de serviços de tooall de conectividade, um grande número de prefixos está anunciado através da BGP. Isto aumenta significativamente tamanho Olá Olá de tabelas de rotas mantida por routers na sua rede. Se planear tooconsume apenas um subconjunto de serviços fornecido via peering da Microsoft, pode reduzir o tamanho de Olá das suas tabelas de rota de duas formas. Pode:

- Filtre prefixos indesejáveis aplicando filtros de rota no Comunidades BGP. Esta é uma prática padrão de rede e é utilizada frequentemente no diversas redes.

- Definir os filtros de rota e aplicá-las tooyour circuito do ExpressRoute. Um filtro de rota é um novo recurso, que permite selecionar lista Olá de serviços planeie tooconsume através do peering da Microsoft. Routers de ExpressRoute enviam apenas lista de Olá de prefixos que pertencem os serviços de toohello identificados no filtro de rota Olá.

### <a name="about"></a>Sobre os filtros de rotas

Quando o peering da Microsoft está configurado no seu circuito do ExpressRoute, routers de limite de Microsoft Olá estabelecer um par de sessões de BGP com routers de limite de Olá (seu ou o fornecedor de conectividade). Não existem rotas são rede tooyour anunciado. rede de tooyour de anúncios de rota tooenable, tem de associar um filtro de rota.

Um filtro de rota permite-lhe identificar os serviços que pretende tooconsume através do peering da Microsoft do circuito do ExpressRoute. É, essencialmente, uma lista de técnico de todos os valores das Comunidades BGP de Olá. Depois de um recurso de filtro de rota é definido e anexado tooan circuito do ExpressRoute, todos os prefixos que mapeiam os valores das Comunidades BGP toohello são rede tooyour anunciado.

toobe tooattach capaz de filtros de rotas com os serviços do Office 365 nos mesmos, tem de ter serviços do Office 365 de tooconsume de autorização através do ExpressRoute. Se não tiver serviços autorizados tooconsume do Office 365 através do ExpressRoute, filtros de rota Olá operação tooattach falhar. Para obter mais informações sobre o processo de autorização de Olá, consulte [Azure ExpressRoute para o Office 365](https://support.office.com/article/Azure-ExpressRoute-for-Office-365-6d2534a2-c19c-4a99-be5e-33a0cee5d3bd). Serviços de 365 conectividade tooDynamics não requer qualquer autorização anterior.

> [!IMPORTANT]
> Peering da Microsoft dos circuitos ExpressRoute que foram configuradas tooAugust anterior 1, 2017 terá todos os serviço prefixos anunciados através do peering da Microsoft, mesmo se os filtros de rota não estão definidos. Peering da Microsoft dos circuitos ExpressRoute que estão configurados em ou após 1 de Agosto de 2017 não terão qualquer prefixos anunciados até que está ligado um filtro de rota toohello circuito.
> 
> 

### <a name="workflow"></a>Fluxo de trabalho

toobe toosuccessfully de capaz de ligar tooservices através do peering da Microsoft, tem de concluir os seguintes passos de configuração de Olá:

- Tem de ter um circuito ExpressRoute ativo que tenha aprovisionado de peering da Microsoft. Pode utilizar Olá seguir instruções tooaccomplish estas tarefas:
  - [Criar um circuito ExpressRoute](expressroute-howto-circuit-portal-resource-manager.md) e ter circuito Olá ativado pelo seu fornecedor de conectividade antes de continuar. Olá circuito ExpressRoute tem de estar num Estado aprovisionado e ativado.
  - [Criar peering da Microsoft](expressroute-howto-routing-portal-resource-manager.md) se gerir sessões BGP de Olá diretamente. Ou, solicite ao seu fornecedor de conectividade aprovisionar o peering da Microsoft para o seu circuito.

-  Tem de criar e configurar um filtro de rota.
    - Identificar Olá serviços com tooconsume através do peering da Microsoft
    - Identifique Olá lista dos valores das Comunidades BGP associados Olá serviços
    - Criar uma regra tooallow Olá prefixo lista correspondente Olá valores das Comunidades BGP

-  Tem de anexar o circuito do ExpressRoute toohello Olá rota filtro.

## <a name="before-you-begin"></a>Antes de começar

Antes de iniciar a configuração, certifique-se de que cumpre os seguintes critérios de Olá:

 - Olá revisão [pré-requisitos](expressroute-prerequisites.md) e [fluxos de trabalho](expressroute-workflows.md) antes de iniciar a configuração.

 - Deve ter um circuito ExpressRoute ativo. Siga as instruções de Olá demasiado[criar um circuito ExpressRoute](expressroute-howto-circuit-portal-resource-manager.md) e ter circuito Olá ativado pelo seu fornecedor de conectividade antes de continuar. Olá circuito ExpressRoute tem de estar num Estado aprovisionado e ativado.

 - Tem de ter um peering da Microsoft Active Directory. Siga as instruções apresentadas em [criar e modificar a configuração do peering](expressroute-howto-routing-portal-resource-manager.md)


## <a name="prefixes"></a>Passo 1. Obter uma lista de prefixos e os valores das Comunidades BGP

### <a name="1-get-a-list-of-bgp-community-values"></a>1. Obter uma lista de valores das Comunidades BGP

Valores das Comunidades BGP associados a serviços acessíveis através do peering da Microsoft está disponível no Olá [requisitos de encaminhamento do ExpressRoute](expressroute-routing.md) página.

### <a name="2-make-a-list-of-hello-values-that-you-want-toouse"></a>2. Se uma lista de valores de Olá que pretende que o toouse

Se uma lista dos valores das Comunidades BGP que pretende toouse num filtro de rota Olá. Por exemplo, Olá valor das Comunidades de BGP para os serviços de Dynamics 365 é 12076:5040.

## <a name="filter"></a>Passo 2. Criar um filtro de rota e uma regra de filtro

Um filtro de rota pode ter apenas uma regra e Olá regra tem de ser do tipo 'Permitir'. Esta regra pode ter uma lista dos valores das Comunidades BGP associados à mesma.

### <a name="1-create-a-route-filter"></a>1. Criar um filtro de rota
Pode criar um filtro de rota selecionando Olá opção toocreate um novo recurso. Clique em **novo** > **redes** > **RouteFilter**, conforme apresentado na Olá seguinte imagem:

![Criar um filtro de rota](.\media\how-to-routefilter-portal\CreateRouteFilter1.png)

Tem de colocar o filtro de rota Olá num grupo de recursos. 

![Criar um filtro de rota](.\media\how-to-routefilter-portal\CreateRouteFilter.png)

### <a name="2-create-a-filter-rule"></a>2. Criar uma regra de filtro

Pode adicionar e regras de atualização selecionando Olá gerir separador de regra para o filtro de rota.

![Criar um filtro de rota](.\media\how-to-routefilter-portal\ManageRouteFilter.png)


Pode selecionar Olá serviços pretende tooconnect toofrom Olá na lista pendente e guardar a regra de Olá quando terminar.

![Criar um filtro de rota](.\media\how-to-routefilter-portal\AddRouteFilterRule.png)


## <a name="attach"></a>Passo 3. Anexar o circuito do ExpressRoute tooan Olá rota filtro

Pode anexar o circuito de tooa de filtro de rota Olá selecionando o botão "adicionar o circuito" de Olá e selecionando circuito de ExpressRoute Olá Olá na lista pendente.

![Criar um filtro de rota](.\media\how-to-routefilter-portal\AddCktToRouteFilter.png)

## <a name="getproperties"></a>Propriedades de Olá tooget de um filtro de rota

Pode ver as propriedades de um filtro de rota quando abrir o recurso de Olá no portal de Olá.

![Criar um filtro de rota](.\media\how-to-routefilter-portal\ViewRouteFilter.png)


## <a name="updateproperties"></a>Propriedades de Olá tooupdate de um filtro de rota

Pode atualizar a lista de Olá do BGP Comunidade valores tooa anexado circuito selecionando o botão de Olá "Gerir regra".


![Criar um filtro de rota](.\media\how-to-routefilter-portal\ManageRouteFilter.png)

![Criar um filtro de rota](.\media\how-to-routefilter-portal\AddRouteFilterRule.png) 


## <a name="detach"></a>toodetach um filtro de rota de um circuito do ExpressRoute

toodetach um circuito do filtro de rota Olá, clique em circuito Olá e clique em "desassocie".

![Criar um filtro de rota](.\media\how-to-routefilter-portal\DetachRouteFilter.png) 


## <a name="delete"></a>toodelete um filtro de rota

Pode eliminar um filtro de rota, selecionando o botão para eliminar Olá. 

![Criar um filtro de rota](.\media\how-to-routefilter-portal\DeleteRouteFilter.png) 

## <a name="next-steps"></a>Passos seguintes

Para obter mais informações sobre o ExpressRoute, consulte Olá [FAQ do ExpressRoute](expressroute-faqs.md).
