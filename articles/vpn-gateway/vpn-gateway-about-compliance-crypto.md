---
title: aaaAbout requisitos de criptografia e gateways de VPN do Azure | Microsoft Docs
description: Este artigo descreve os requisitos de criptografia e gateways de VPN do Azure
services: vpn-gateway
documentationcenter: na
author: yushwang
manager: rossort
editor: 
tags: azure-resource-manager
ms.assetid: 238cd9b3-f1ce-4341-b18e-7390935604fa
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/22/2017
ms.author: yushwang
ms.openlocfilehash: af5f14d66beeea5316218f9788c4ad7876826162
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="about-cryptographic-requirements-and-azure-vpn-gateways"></a>Sobre os requisitos de criptografia e gateways de VPN do Azure

Este artigo descreve como configurar toosatisfy de gateways de VPN do Azure os requisitos de criptografia para túneis S2S VPN de vários locais e ligações VNet a VNet no Azure. 

## <a name="about-ipsec-and-ike-policy-parameters-for-azure-vpn-gateways"></a>Acerca dos parâmetros de política IPsec e IKE para gateways de VPN do Azure
Protocolo IPsec e IKE padrão suporta uma vasta gama de algoritmos criptográficos várias combinações. Se os clientes pedem uma combinação específica de algoritmos criptográficos e parâmetros, os gateways de VPN do Azure utilizam um conjunto de propostas de predefinição. conjuntos de política predefinida de Olá foram escolhidos toomaximize interoperabilidade com uma vasta gama de dispositivos VPN de terceiros em configurações predefinidas. Como resultado, as políticas de Olá e número de Olá de propostas não podem abranger todas as possíveis combinações de algoritmos criptográficos disponíveis e força da codificação chave.

Olá política predefinida definida para o gateway de VPN do Azure está listado no documento de Olá: [acerca dos dispositivos VPN e parâmetros IPsec/IKE para ligações de Gateway de VPN de Site para Site](vpn-gateway-about-vpn-devices.md).

## <a name="cryptographic-requirements"></a>Requisitos de criptografia
Para comunicações que necessitam de algoritmos criptográficos específicos ou parâmetros, normalmente devido a requisitos de segurança ou toocompliance, os clientes agora podem configurar os respetivos toouse de gateways de VPN do Azure uma política personalizada do IPsec/IKE com específicos de criptografia algoritmos e chave força da codificação, em vez de conjuntos de política do Olá predefinido do Azure.

Por exemplo, políticas de modo principal Olá IKEv2 para gateways de VPN do Azure utilizam apenas Diffie-Hellman Grupo 2 (1024 bits), enquanto que os clientes poderão ter toospecify mais forte grupos toobe utilizado no IKE, tais como 14 de grupo (2048 bits), grupo 24 (grupo MODP de 2048 bits) ou ECP (elíptica curva grupos) 384 ou 256 bits (e de grupo 19 20 de grupo, respetivamente). Requisitos de semelhantes aplicam políticas de modo rápido de tooIPsec bem.

## <a name="custom-ipsecike-policy-with-azure-vpn-gateways"></a>Política personalizada do IPsec/IKE com gateways de VPN do Azure
Gateways de VPN do Azure suportam agora por ligação, a política personalizada do IPsec/IKE. Para um Site para Site ou a ligação VNet a VNet, pode escolher uma combinação específica de algoritmos criptográficos para IPsec e IKE força de chave Olá assim o desejar, conforme mostrado no seguinte exemplo de Olá:

![política de ike IPSec](./media/vpn-gateway-about-compliance-crypto/ipsecikepolicy.png)

Pode criar uma política de IPsec/IKE e aplicar tooa a ligação de novo ou existente. 

### <a name="workflow"></a>Fluxo de trabalho

1. Criar redes virtuais Olá, gateways de VPN ou gateways de rede local para a topologia de conectividade, conforme descrito em outros toodocuments como
2. Criar uma política de IPsec/IKE
3. Pode aplicar a política de Olá quando cria uma ligação S2S ou VNet a VNet
4. Se a ligação de Olá já está a ser criada, pode aplicar ou atualizar a ligação do Olá política tooan existente


## <a name="ipsecike-policy-faq"></a>FAQ da política de IPsec/IKE

[!INCLUDE [vpn-gateway-ipsecikepolicy-faq-include](../../includes/vpn-gateway-ipsecikepolicy-faq-include.md)]


## <a name="next-steps"></a>Passos seguintes
Consulte [política IPsec/IKE configurar](vpn-gateway-ipsecikepolicy-rm-powershell.md) para obter instruções passo a passo sobre como configurar a política personalizada do IPsec/IKE numa ligação.

Consulte também [ligar vários dispositivos VPN baseado na política](vpn-gateway-connect-multiple-policybased-rm-ps.md) toolearn mais informações sobre Olá UsePolicyBasedTrafficSelectors opção.
