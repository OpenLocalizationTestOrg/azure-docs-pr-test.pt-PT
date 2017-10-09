---
title: aaaQoS requisitos para o ExpressRoute | Microsoft Docs
description: "Esta página fornece os requisitos detalhados para configurar e gerir o QoS para circuitos do ExpressRoute."
documentationcenter: na
services: expressroute
author: cherylmc
manager: carmonm
editor: 
ms.assetid: db1c1447-0283-4a09-907b-ae481adc40c7
ms.service: expressroute
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/25/2017
ms.author: cherylmc
ms.openlocfilehash: 46cc81bd38ff50dd9e7a1bfdd0faa457ff7b2fa1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="expressroute-qos-requirements"></a>Requisitos do QoS do ExpressRoute
O Skype para Empresas tem várias cargas de trabalho que exigem um tratamento do QoS diferenciado. Se planear serviços de voz tooconsume através do ExpressRoute, deve cumprir os requisitos de toohello descritos abaixo.

![](./media/expressroute-qos/expressroute-qos.png)

> [!NOTE]
> Os requisitos do QoS aplicam-se toohello peering da Microsoft apenas. valores DSCP Olá no seu tráfego de rede recebidos no peering público do Azure e peering privado do Azure será too0 de reposição. 
> 
> 

Olá tabela seguinte fornece uma lista de marcações DSCP utilizadas pelo Skype para empresas. Consulte demasiado[gerir QoS para Skype para empresas](https://technet.microsoft.com/library/gg405409.aspx) para obter mais informações.

| **Classe de Tráfego** | **Tratamento (Marcação DSCP)** | **Cargas de trabalho do Skype para Empresas** |
| --- | --- | --- |
| **Voz** |EF (46) |Voz do Skype/Lync |
| **Interativo** |AF41 (34) |Video, VBSS |
| AF21 (18) |Partilha de aplicações | |
| **Predefinição** |AF11 (10) |Transferência de ficheiros |
| CS0 (0) |Tudo o resto | |

* Deve classificar as cargas de trabalho Olá e marcar os valores DSCP corretos do Olá. Siga as orientações de Olá fornecida [aqui](https://technet.microsoft.com/library/gg405409.aspx) sobre marcações DSCP de tooset na sua rede.
* Deve configurar e suportar várias filas do QoS na rede. Voz tem de ser uma classe autónoma e receber o tratamento EF de Olá especificado no RFC 3246. 
* Pode decidir Olá colocação mecanismo, a política de deteção de congestionamento e a alocação de largura de banda por classe de tráfego. No entanto, hello marcação DSCP para o Skype para cargas de trabalho do negócio têm de ser preservado. Se estiver a utilizar marcações DSCP não listadas acima, por exemplo, AF31 (26), terá de reescrever este too0 de valor DSCP antes de enviar Olá tooMicrosoft de pacote. A Microsoft só envia pacotes marcados com Olá valor DSCP mostrado na Olá acima tabela. 

## <a name="next-steps"></a>Passos seguintes
* Consulte os requisitos de toohello para [encaminhamento](expressroute-routing.md) e [NAT](expressroute-nat.md).
* Consulte a seguinte Olá liga tooconfigure a ligação do ExpressRoute.
  
  * [Crie um circuito do ExpressRoute](expressroute-howto-circuit-classic.md)
  * [Configure o encaminhamento](expressroute-howto-routing-classic.md)
  * [Associar um tooan VNet circuito do ExpressRoute](expressroute-howto-linkvnet-classic.md)

