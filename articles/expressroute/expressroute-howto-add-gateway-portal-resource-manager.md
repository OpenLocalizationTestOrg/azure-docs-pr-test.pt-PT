---
title: 'Adicionar um tooa de gateway de rede virtual VNet para o ExpressRoute: Portal: Azure | Microsoft Docs'
description: "Este artigo explica como adicionar um tooan de gateway de rede virtual já criado a VNet do Resource Manager para o ExpressRoute."
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
ms.date: 04/17/2017
ms.author: cherylmc
ms.openlocfilehash: 9e922af1f3676eeebc569b57c3ae3a22d4e0b395
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-virtual-network-gateway-for-expressroute-using-hello-azure-portal"></a>Configurar um gateway de rede virtual para o ExpressRoute utilizando Olá portal do Azure
> [!div class="op_single_selector"]
> * [Resource Manager - portal do Azure](expressroute-howto-add-gateway-portal-resource-manager.md)
> * [Resource Manager – PowerShell](expressroute-howto-add-gateway-resource-manager.md)
> * [Clássico - PowerShell](expressroute-howto-add-gateway-classic.md)
> * [Vídeo - portal do Azure](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-vpn-gateway-for-your-virtual-network)
> 
> 

Este artigo explica os passos de Olá tooadd um gateway de rede virtual para uma VNet já existente. Este artigo explica como Olá passos tooadd, redimensionar e remover um gateway de rede virtual (VNet) para uma VNet já existente. passos de Olá para esta configuração estão especificamente para VNets que foram criadas utilizando o modelo de implementação Resource Manager do Olá que será utilizado uma configuração do ExpressRoute. Para obter mais informações sobre gateways de rede virtual e definições de configuração do gateway do ExpressRoute, consulte [sobre gateways de rede virtual para o ExpressRoute](expressroute-about-virtual-network-gateways.md). 


## <a name="before-beginning"></a>Antes de começar

Olá os passos para utilizar esta tarefa uma VNet com base nos valores de Olá no Olá seguinte lista de referência de configuração. Podemos utilizar esta lista no nosso passos de exemplo. Pode copiar Olá lista toouse como uma referência, substituindo os valores de Olá com os seus próprios.

**Lista de referência de configuração**

* Nome da rede virtual = "TestVNet"
* Espaço de endereços de rede virtuais = 192.168.0.0/16
* Nome da sub-rede = "FrontEnd" 
    * Espaço de endereços da sub-rede = "192.168.1.0/24"
* Grupo de recursos = "TestRG"
* Localização = "EUA Leste"
* Nome de sub-rede de gateway: "GatewaySubnet" tem de nome sempre uma sub-rede de gateway *GatewaySubnet*.
    * Espaço de endereços de sub-rede de gateway = "192.168.200.0/26"
* O nome do gateway = "ERGW"
* O nome IP do gateway = "MyERGWVIP"
* Tipo de gateway = "ExpressRoute" deste tipo é necessário para uma configuração do ExpressRoute.
* O nome IP público do gateway = "MyERGWVIP"

Pode ver um [vídeo](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-vpn-gateway-for-your-virtual-network) destes passos antes de iniciar a configuração.

## <a name="create-hello-gateway-subnet"></a>Criar a sub-rede do gateway Olá

1. No Olá [portal](http://portal.azure.com), navegue até toohello Resource Manager rede virtual para o qual pretende toocreate um gateway de rede virtual.
2. No Olá **definições** secção do painel da VNet, clique em **sub-redes** painel de sub-redes de Olá tooexpand.
3. No Olá **sub-redes** painel, clique em **+ sub-rede do Gateway** tooopen Olá **adicionar sub-rede** painel. 
   
    ![Adicionar sub-rede do gateway Olá](./media/expressroute-howto-add-gateway-portal-resource-manager/addgwsubnet.png "adicionar sub-rede do gateway Olá")


4. Olá **nome** para a sub-rede é automaticamente preenchida com Olá valor "GatewaySubnet". Este valor é necessário para sub-rede do Azure toorecognize Olá como a sub-rede do gateway Olá. Ajustar Olá preenchida automaticamente **intervalo de endereços** valores toomatch os requisitos de configuração. Recomendamos que crie uma sub-rede de gateway com/27 ou superior (/ 26, / 25, etc.). Em seguida, clique em **OK** toosave Olá valores e criar a sub-rede do gateway Olá.

    ![Adicionar a sub-rede de Olá](./media/expressroute-howto-add-gateway-portal-resource-manager/addsubnetgw.png "adicionar a sub-rede de Olá")

## <a name="create-hello-virtual-network-gateway"></a>Criar gateway de rede virtual Olá

1. No portal de Olá, no lado esquerdo Olá, clique em  **+**  e escreva "Gateway de rede Virtual" na pesquisa. Localizar **gateway de rede Virtual** na pesquisa de Olá devolver e clique Olá entrada. No Olá **gateway de rede Virtual** painel, clique em **criar** em Olá parte inferior do painel de Olá. Esta ação abre Olá **criar gateway de rede virtual** painel.
2. No Olá **criar gateway de rede virtual** painel, preencha os valores de Olá para o gateway de rede virtual.

    ![Create virtual network gateway blade fields](./media/expressroute-howto-add-gateway-portal-resource-manager/gw.png "Create virtual network gateway blade fields")
3. **Nome**: dê um nome ao gateway. Isto é não Olá, mesmo que atribuir nome a uma sub-rede de gateway. -'S nome Olá do objeto do gateway Olá que estiver a criar.
4. **Tipo de gateway**: selecione **ExpressRoute**.
5. **SKU**: SKU de gateway Olá selecione na lista pendente de Olá.
6. **Localização**: ajustar Olá **localização** campo toopoint toohello localização onde está localizada a sua rede virtual. Se a localização de Olá não está a apontar região toohello onde reside a sua rede virtual, rede virtual Olá não aparece na lista pendente do Olá 'Escolha uma rede virtual'.
7. Escolha Olá toowhich de rede virtual pretende tooadd este gateway. Clique em **rede Virtual** tooopen Olá **escolha uma rede virtual** painel. Selecione Olá VNet. Se não vir a VNet, certifique-se de que Olá **localização** campo está a apontar toohello região na qual está localizada a sua rede virtual.
9. Escolha um endereço IP público. Clique em **endereço IP público** tooopen Olá **escolher endereço IP público** painel. Clique em **+ criar novos** tooopen Olá **painel de endereço IP público criar**. Introduza um nome para o seu endereço IP público. Este painel cria um toowhich de objeto do endereço IP público que um endereço IP público será atribuído dinamicamente. Clique em **OK** toosave o painel de toothis alterações.
10. **Subscrição**: Certifique-se de que Olá correta está selecionada a subscrição.
11. **Grupo de recursos**: esta definição é determinada pelo Olá rede Virtual que selecionou.
12. Não ajustar Olá **localização** depois especificadas definições anteriores Olá.
13. Verifique as definições de Olá. Se pretender que o seu tooappear de gateway no dashboard de Olá, pode selecionar **Pin toodashboard** em Olá parte inferior do painel de Olá.
14. Clique em **criar** toobegin criar Olá gateway. definições de Olá são validadas e gateway Olá implementa. Criar gateway de rede virtual pode demorar até too45 minutos toocomplete.

## <a name="next-steps"></a>Passos seguintes
Depois de ter criado o gateway de VNet Olá, pode associar o seu tooan VNet circuito ExpressRoute. Consulte [ligar uma rede Virtual de tooan circuito ExpressRoute](expressroute-howto-linkvnet-portal-resource-manager.md).
