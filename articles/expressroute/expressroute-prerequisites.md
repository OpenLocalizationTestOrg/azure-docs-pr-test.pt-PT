---
title: "aaaPrerequisites para adoção do ExpressRoute do Azure | Microsoft Docs"
description: "Esta página fornece uma lista de toobe requisitos cumprida para que possa ordenar um circuito ExpressRoute do Azure."
documentationcenter: na
services: expressroute
author: cherylmc
manager: timlt
editor: 
ms.assetid: f872d25e-acfd-405d-9d1b-dcb9f323a2ff
ms.service: expressroute
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/30/2017
ms.author: cherylmc
ms.openlocfilehash: 524c86f6570dc6e6505fe55323b8508e8eeff791
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="expressroute-prerequisites--checklist"></a>Pré-requisitos e lista de verificação do ExpressRoute
tooconnect tooMicrosoft cloud services com o ExpressRoute, terá de tooverify esse Olá os seguintes requisitos listados em Olá secções a seguir foram cumpridos.

[!INCLUDE [expressroute-office365-include](../../includes/expressroute-office365-include.md)]

## <a name="azure-account"></a>Conta do Azure
* Uma conta ativa do Microsoft Azure. Esta conta é necessária tooset segurança Olá circuito ExpressRoute. Os circuitos do ExpressRoute são recursos incluídos nas subscrições do Azure. Uma subscrição do Azure é um requisito, mesmo se a conectividade estiver limitadas toonon-Microsoft cloud services do Azure, tais como serviços do Office 365 e Dynamics 365.
* Uma subscrição ativa do Office 365 (se utilizar os serviços do Office 365). Para obter mais informações, consulte Olá [requisitos específicos do Office 365](#office-365-specific-requirements) secção deste artigo.

## <a name="connectivity-provider"></a>Fornecedor de conectividade

* Pode trabalhar com um [parceiro de conectividade do ExpressRoute](expressroute-locations.md#partners) tooconnect toohello nuvem da Microsoft. Pode configurar uma ligação entre a sua rede no local e a Microsoft de [três modos](expressroute-introduction.md).
* Se o seu fornecedor não é um parceiro de conectividade do ExpressRoute, ainda pode ligar toohello nuvem da Microsoft através de um [fornecedor do exchange de nuvem](expressroute-locations.md#connectivity-through-exchange-providers).

## <a name="network-requirements"></a>Requisitos da rede
* **Conectividade redundante**: não é necessário haver redundância na conectividade física entre o utilizador e o fornecedor. Microsoft requerem toobe de sessões BGP redundante entre routers da Microsoft e os routers de peering Olá, configurar, mesmo se tiver apenas [uma troca de nuvem de ligação física tooa](expressroute-faqs.md#onep2plink).
* **Encaminhamento**: consoante a forma de ligar toohello Microsoft Cloud, utilizador ou o fornecedor necessário tooset configurar e gerir sessões de BGP de Olá para [domínios de encaminhamento](expressroute-circuit-peerings.md). Alguns fornecedores de conectividade Ethernet ou fornecedores do Exchange na nuvem poderão oferecer gestão de BGP como um serviço de valor acrescentado.
* **NAT**: a Microsoft só aceita endereços IP públicos através do peering da Microsoft. Se estiver a utilizar endereços IP privados na sua rede no local, o utilizador ou o fornecedor necessário tootranslate Olá IP privado endereços os endereços IP públicos toohello [utilizando Olá NAT](expressroute-nat.md).
* **QoS**: o Skype para Empresas tem vários serviços (por exemplo, voz, vídeo, texto) que exigem um tratamento QoS diferenciado. Utilizador e o fornecedor devem seguir Olá [os requisitos do QoS](expressroute-qos.md).
* **Segurança de rede**: considere [segurança de rede](../best-practices-network-security.md) ao ligar toohello Microsoft Cloud através do ExpressRoute.

## <a name="office-365"></a>Office 365
Se planear tooenable do Office 365 no ExpressRoute, reveja Olá seguintes documentos para obter mais informações sobre os requisitos do Office 365.

* [Descrição geral do ExpressRoute para o Office 365](https://support.office.com/en-us/article/Azure-ExpressRoute-for-Office-365-6d2534a2-c19c-4a99-be5e-33a0cee5d3bd)
* [Encaminhamento com o ExpressRoute para o Office 365](https://support.office.com/en-us/article/Routing-with-ExpressRoute-for-Office-365-e1da26c6-2d39-4379-af6f-4da213218408)
* [Intervalos de endereços IP e URLs do Office 365](https://support.office.com/en-us/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2)
* [Planeamento de rede e otimização de desempenho para o Office 365](https://support.office.com/en-us/article/Network-planning-and-performance-tuning-for-Office-365-e5f1228c-da3c-4654-bf16-d163daee8848)
* [Calculadoras e ferramentas de largura de banda de rede](https://support.office.com/en-us/article/Network-and-migration-planning-for-Office-365-f5ee6c33-bcd7-4b0b-b0f8-dc1d9fb8d132)
* [Integração do Office 365 com ambientes no local](https://support.office.com/en-us/article/Office-365-integration-with-on-premises-environments-263faf8d-aa21-428b-aed3-2021837a4b65)
* [Vídeos de formação de avançada do ExpressRoute no Office 365](https://channel9.msdn.com/series/aer/)

## <a name="dynamics-365"></a>Dynamics 365
Se planear tooenable Dynamics 365 no ExpressRoute, reveja Olá seguintes documentos para obter mais informações acerca de Dynamics 365

* [Documento técnico do Dynamics 365 e ExpressRoute](http://download.microsoft.com/download/B/2/8/B2896B38-9832-417B-9836-9EF240C0A212/Microsoft%20Dynamics%20365%20and%20ExpressRoute.pdf)
* [URL](https://support.microsoft.com/kb/2655102) e [intervalos de endereços de IP do Dynamics 365](https://support.microsoft.com/kb/2728473)

## <a name="next-steps"></a>Passos seguintes
* Para obter mais informações sobre o ExpressRoute, consulte Olá [FAQ do ExpressRoute](expressroute-faqs.md).
* Localizar um fornecedor de conectividade do ExpressRoute. Veja [Parceiros e localizações de peering do ExpressRoute ](expressroute-locations.md).
* Consulte toorequirements para [encaminhamento](expressroute-routing.md), [NAT](expressroute-nat.md), e [QoS](expressroute-qos.md).
* Configurar a ligação do ExpressRoute.
  * [Crie um circuito do ExpressRoute](expressroute-howto-circuit-classic.md)
  * [Configure o encaminhamento](expressroute-howto-routing-classic.md)
  * [Associar um tooan VNet circuito do ExpressRoute](expressroute-howto-linkvnet-classic.md)
