---
title: 'Criar e modificar um circuito ExpressRoute: portal do Azure | Microsoft Docs'
description: Este artigo descreve como toocreate, aprovisionar, certifique-se, atualizar, eliminar e retirar o aprovisionamento um circuito ExpressRoute.
documentationcenter: na
services: expressroute
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 68d59d59-ed4d-482f-9cbc-534ebb090613
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/07/2017
ms.author: cherylmc;ganesr
ms.openlocfilehash: 200418aed6bdebace43a2f57cf532d1c8d13cb83
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-modify-an-expressroute-circuit"></a>Criar e modificar um circuito do ExpressRoute
> [!div class="op_single_selector"]
> * [Portal do Azure](expressroute-howto-circuit-portal-resource-manager.md)
> * [PowerShell](expressroute-howto-circuit-arm.md)
> * [CLI do Azure](howto-circuit-cli.md)
> * [Vídeo - portal do Azure](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-an-expressroute-circuit)
> * [PowerShell (clássico)](expressroute-howto-circuit-classic.md)
>

Este artigo descreve como toocreate um circuito ExpressRoute do Azure utilizando Olá Azure modelo de implementação de Gestor de recursos do Azure de portal e Olá. Olá também os seguintes passos mostra como toocheck Olá estado do circuito Olá, a atualização, ou eliminar e retirar o aprovisionamento do mesmo.


## <a name="before-you-begin"></a>Antes de começar
* Olá revisão [pré-requisitos](expressroute-prerequisites.md) e [fluxos de trabalho](expressroute-workflows.md) antes de iniciar a configuração.
* Certifique-se de que tem acesso toohello [portal do Azure](https://portal.azure.com).
* Certifique-se de que dispõe de permissões toocreate novos recursos de rede. Se não tiver permissões corretas Olá, contacte o administrador de conta.
* Pode [ver um vídeo](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-an-expressroute-circuit) antes de começar por ordem toobetter compreender os passos de Olá.

## <a name="create-and-provision-an-expressroute-circuit"></a>Criar e aprovisionar um circuito do ExpressRoute
### <a name="1-sign-in-toohello-azure-portal"></a>1. A iniciar sessão toohello portal do Azure
Num browser, navegue toohello [portal do Azure](http://portal.azure.com) e inicie sessão com a sua conta do Azure.

### <a name="2-create-a-new-expressroute-circuit"></a>2. Criar um novo circuito do ExpressRoute
> [!IMPORTANT]
> O circuito de ExpressRoute será cobrado a partir do momento em que Olá uma chave de serviço é emitida. Certifique-se de que efetuar esta operação quando o fornecedor de conectividade de Olá circuito de Olá tooprovision pronto.
> 
> 

1. Pode criar um circuito ExpressRoute selecionando Olá opção toocreate um novo recurso. Clique em **novo** > **redes** > **ExpressRoute**, conforme apresentado na Olá seguinte imagem:
   
    ![Criar um circuito do ExpressRoute](./media/expressroute-howto-circuit-portal-resource-manager/createcircuit1.png)
2. Depois de clicar em **ExpressRoute**, verá Olá **circuito ExpressRoute criar** painel. Quando estiver a preencher valores de Olá neste painel, certifique-se de que especifica a camada SKU correta Olá e medição de dados.
   
   * **Camada** determina se a um padrão de ExpressRoute ou de um suplemento ExpressRoute premium está ativado. Pode especificar **padrão** tooget Olá standard SKU ou **Premium** para o suplemento do Olá premium.
   * **Medição de dados** determina o tipo de faturação Olá. Pode especificar **Metered** para um plano de dados limitados e **ilimitada** para um plano de dados ilimitados. Tenha em atenção que pode alterar o tipo de faturação Olá de **Metered** demasiado**ilimitada**, mas não é possível alterar o tipo de Olá da **ilimitada** demasiado**Metered**.
     
     ![Configurar a camada SKU Olá e medição de dados](./media/expressroute-howto-circuit-portal-resource-manager/createcircuit2.png)

> [!IMPORTANT]
> . Lembre-se de que a localização de Peering de Olá indica Olá [localização física](expressroute-locations.md) onde são peering com a Microsoft. Este é **não** ligado demasiado propriedade de "Localização", que se refere geografia toohello onde está localizada a Olá fornecedor de recursos de rede do Azure. Apesar de não estão relacionadas, é uma boa prática toochoose um toohello geograficamente fechar o fornecedor de recursos de rede de localização de Peering do circuito Olá. 
> 
> 

### <a name="3-view-hello-circuits-and-properties"></a>3. Vista Olá circuitos e propriedades
**Ver todos os circuitos de Olá**

Pode ver todos os circuitos Olá que criou, selecionando **todos os recursos** no menu do lado esquerdo de Olá.

![Circuitos de vista](./media/expressroute-howto-circuit-portal-resource-manager/listresource.png)

**Ver propriedades de Olá**

    You can view hello properties of hello circuit by selecting it. On this blade, note hello service key for hello circuit. You must copy hello circuit key for your circuit and pass it down toohello service provider toocomplete hello provisioning process. hello circuit key is specific tooyour circuit.

![Ver propriedades](./media/expressroute-howto-circuit-portal-resource-manager/listproperties1.png)

### <a name="4-send-hello-service-key-tooyour-connectivity-provider-for-provisioning"></a>4. Enviar o fornecedor de conectividade do Olá serviço tooyour chave para o aprovisionamento
Neste painel, **Estado fornecedor** fornece informações sobre o estado atual do Olá de aprovisionamento no lado do fornecedor de serviços de Olá. **Estado de circuitos** fornece o estado de Olá Olá do lado da Microsoft. Para obter mais informações sobre os Estados de aprovisionamento do circuito, consulte Olá [fluxos de trabalho](expressroute-workflows.md#expressroute-circuit-provisioning-states) artigo.

Quando cria um novo circuito do ExpressRoute, circuito Olá estarão disponíveis na Olá seguinte estado:

Estado do fornecedor: não aprovisionado<BR>
Estado de circuitos: ativado

![Iniciar o processo de aprovisionamento](./media/expressroute-howto-circuit-portal-resource-manager/viewstatus.png)

o circuito de Olá mudará toohello seguinte estado quando o fornecedor de conectividade Olá está no processo de Olá de ativação-lo por si:

Estado do fornecedor: aprovisionamento<BR>
Estado de circuitos: ativado

Para toobe capaz de toouse um circuito do ExpressRoute, tem de ter Olá seguinte estado:

Estado do fornecedor: aprovisionado<BR>
Estado de circuitos: ativado

### <a name="5-periodically-check-hello-status-and-hello-state-of-hello-circuit-key"></a>5. Verificar periodicamente o estado de Olá e estado de Olá da chave de circuito Olá
Pode ver as propriedades de Olá do circuito Olá que está a interessados ao selecioná-la. Verifique Olá **Estado fornecedor** e certifique-se de que foi movida demasiado**aprovisionado** antes de continuar.

![Estado do circuito e fornecedor](./media/expressroute-howto-circuit-portal-resource-manager/viewstatusprovisioned.png)

### <a name="6-create-your-routing-configuration"></a>6. Criar a configuração de encaminhamento
Para obter instruções passo a passo, consulte toohello [configuração de encaminhamento de circuito de ExpressRoute](expressroute-howto-routing-portal-resource-manager.md) artigo toocreate e modificar peerings do circuito.

> [!IMPORTANT]
> Estas instruções aplicam-se apenas toocircuits que são criados com fornecedores de serviços que oferecem serviços de 2 conectividade de camada. Se estiver a utilizar um fornecedor de serviço que oferece gerido layer 3 serviços (normalmente, uma VPN de IP, como MPLS), o seu fornecedor de conectividade irá configurar e gerir encaminhamento por si.
> 
> 

### <a name="7-link-a-virtual-network-tooan-expressroute-circuit"></a>7. Ligar uma rede virtual de tooan circuito do ExpressRoute
Em seguida, associe um tooyour de rede virtual circuito ExpressRoute. Olá utilize [ligação virtual redes tooExpressRoute circuitos](expressroute-howto-linkvnet-arm.md) artigo quando trabalha com o modelo de implementação do Resource Manager Olá.

## <a name="getting-hello-status-of-an-expressroute-circuit"></a>Ao obter o estado de Olá de um circuito ExpressRoute
Pode ver o estado de Olá de um circuito ao selecioná-la. 

![Estado de um circuito ExpressRoute](./media/expressroute-howto-circuit-portal-resource-manager/listproperties1.png)

## <a name="modifying-an-expressroute-circuit"></a>Modificar um circuito do ExpressRoute
Pode modificar algumas propriedades de um circuito ExpressRoute sem afetar a conectividade.

Pode fazê-lo Olá sem período de indisponibilidade os seguintes:

* Ativar ou desativar um suplemento ExpressRoute premium para o seu circuito do ExpressRoute.
* Aumento Olá largura de banda do circuito de ExpressRoute fornecido está capacidade disponível na porta Olá. Tenha em atenção que a largura de banda de Olá de um circuito de desatualização não é suportado. 
* Alterar Olá plano do tooUnlimited dados limitados de dados de medição. Tenha em atenção que a alteração plano medição Olá de tooMetered dados ilimitados de dados não é suportada.
* Pode ativar e desativar *permitir operações clássicas*.

Para obter mais informações sobre limites e limitações, consulte toohello [FAQ do ExpressRoute](expressroute-faqs.md).

toomodify um circuito do ExpressRoute, clique em Olá **configuração** conforme mostrado na figura Olá abaixo.

![Modificar o circuito](./media/expressroute-howto-circuit-portal-resource-manager/modifycircuit.png)

Pode modificar Olá da largura de banda, SKU e modelo de faturação e permitir operações clássicas dentro do painel de configuração de Olá.

> [!IMPORTANT]
> Pode ter o circuito de ExpressRoute toorecreate Olá se existir capacidade inadequada na porta existente Olá. Não é possível atualizar o circuito Olá se não houver nenhuma capacidade adicional nessa localização.
>
> Não é possível reduzir a largura de banda de Olá de um circuito de ExpressRoute sem interrupção. Desatualização de largura de banda requer que o circuito de ExpressRoute toodeprovision Olá e, em seguida, reaprovisionar um circuito de ExpressRoute novo.
> 
> Desativar o suplemento premium operação pode falhar se estiver a utilizar recursos que são maiores que o que é permitido para o circuito standard Olá.
> 
> 

## <a name="deprovisioning-and-deleting-an-expressroute-circuit"></a>Desaprovisionamento e eliminar um circuito do ExpressRoute
Pode eliminar o circuito de ExpressRoute selecionando Olá **eliminar** ícone. Tenha em atenção o seguinte Olá:

* Tem de desassociar todas as redes virtuais do Olá circuito ExpressRoute. Se esta operação falhar, verifique se as redes virtuais ligadas toohello circuito.
* Se for Olá ExpressRoute circuito fornecedor do serviço de estado de aprovisionamento **aprovisionamento** ou **aprovisionado** tem de trabalhar com o seu circuito de Olá de toodeprovision de fornecedor de serviço no seu lado. Iremos continuar tooreserve recursos e faturar-lhe até que o fornecedor de serviços de Olá conclui o circuito de Olá desaprovisionamento e notifica-nos.
* Se o fornecedor de serviços de Olá tem desaprovisionada circuito Olá (fornecedor de serviços de Olá estado de aprovisionamento está definido demasiado**não aprovisionado**), em seguida, pode eliminar o circuito Olá. Isto irá parar faturação para o circuito Olá

## <a name="next-steps"></a>Passos seguintes
Depois de criar o seu circuito, certifique-se de que Olá a seguir:

* [Criar e modificar o encaminhamento para o seu circuito do ExpressRoute](expressroute-howto-routing-portal-resource-manager.md)
* [Ligar o seu tooyour de rede virtual circuito do ExpressRoute](expressroute-howto-linkvnet-arm.md)

