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
# <a name="about-cryptographic-requirements-and-azure-vpn-gateways"></a><span data-ttu-id="70f0d-103">Sobre os requisitos de criptografia e gateways de VPN do Azure</span><span class="sxs-lookup"><span data-stu-id="70f0d-103">About cryptographic requirements and Azure VPN gateways</span></span>

<span data-ttu-id="70f0d-104">Este artigo descreve como configurar toosatisfy de gateways de VPN do Azure os requisitos de criptografia para túneis S2S VPN de vários locais e ligações VNet a VNet no Azure.</span><span class="sxs-lookup"><span data-stu-id="70f0d-104">This article discusses how you can configure Azure VPN gateways toosatisfy your cryptographic requirements for both cross-premises S2S VPN tunnels and VNet-to-VNet connections within Azure.</span></span> 

## <a name="about-ipsec-and-ike-policy-parameters-for-azure-vpn-gateways"></a><span data-ttu-id="70f0d-105">Acerca dos parâmetros de política IPsec e IKE para gateways de VPN do Azure</span><span class="sxs-lookup"><span data-stu-id="70f0d-105">About IPsec and IKE policy parameters for Azure VPN gateways</span></span>
<span data-ttu-id="70f0d-106">Protocolo IPsec e IKE padrão suporta uma vasta gama de algoritmos criptográficos várias combinações.</span><span class="sxs-lookup"><span data-stu-id="70f0d-106">IPsec and IKE protocol standard supports a wide range of cryptographic algorithms in various combinations.</span></span> <span data-ttu-id="70f0d-107">Se os clientes pedem uma combinação específica de algoritmos criptográficos e parâmetros, os gateways de VPN do Azure utilizam um conjunto de propostas de predefinição.</span><span class="sxs-lookup"><span data-stu-id="70f0d-107">If customers do not request a specific combination of cryptographic algorithms and parameters, Azure VPN gateways use a set of default proposals.</span></span> <span data-ttu-id="70f0d-108">conjuntos de política predefinida de Olá foram escolhidos toomaximize interoperabilidade com uma vasta gama de dispositivos VPN de terceiros em configurações predefinidas.</span><span class="sxs-lookup"><span data-stu-id="70f0d-108">hello default policy sets were chosen toomaximize interoperability with a wide range of third-party VPN devices in default configurations.</span></span> <span data-ttu-id="70f0d-109">Como resultado, as políticas de Olá e número de Olá de propostas não podem abranger todas as possíveis combinações de algoritmos criptográficos disponíveis e força da codificação chave.</span><span class="sxs-lookup"><span data-stu-id="70f0d-109">As a result, hello policies and hello number of proposals cannot cover all possible combinations of available cryptographic algorithms and key strengths.</span></span>

<span data-ttu-id="70f0d-110">Olá política predefinida definida para o gateway de VPN do Azure está listado no documento de Olá: [acerca dos dispositivos VPN e parâmetros IPsec/IKE para ligações de Gateway de VPN de Site para Site](vpn-gateway-about-vpn-devices.md).</span><span class="sxs-lookup"><span data-stu-id="70f0d-110">hello default policy set for Azure VPN gateway is listed in hello document: [About VPN devices and IPsec/IKE parameters for Site-to-Site VPN Gateway connections](vpn-gateway-about-vpn-devices.md).</span></span>

## <a name="cryptographic-requirements"></a><span data-ttu-id="70f0d-111">Requisitos de criptografia</span><span class="sxs-lookup"><span data-stu-id="70f0d-111">Cryptographic requirements</span></span>
<span data-ttu-id="70f0d-112">Para comunicações que necessitam de algoritmos criptográficos específicos ou parâmetros, normalmente devido a requisitos de segurança ou toocompliance, os clientes agora podem configurar os respetivos toouse de gateways de VPN do Azure uma política personalizada do IPsec/IKE com específicos de criptografia algoritmos e chave força da codificação, em vez de conjuntos de política do Olá predefinido do Azure.</span><span class="sxs-lookup"><span data-stu-id="70f0d-112">For communications that require specific cryptographic algorithms or parameters, typically due toocompliance or security requirements, customers can now configure their Azure VPN gateways toouse a custom IPsec/IKE policy with specific cryptographic algorithms and key strengths, rather than hello Azure default policy sets.</span></span>

<span data-ttu-id="70f0d-113">Por exemplo, políticas de modo principal Olá IKEv2 para gateways de VPN do Azure utilizam apenas Diffie-Hellman Grupo 2 (1024 bits), enquanto que os clientes poderão ter toospecify mais forte grupos toobe utilizado no IKE, tais como 14 de grupo (2048 bits), grupo 24 (grupo MODP de 2048 bits) ou ECP (elíptica curva grupos) 384 ou 256 bits (e de grupo 19 20 de grupo, respetivamente).</span><span class="sxs-lookup"><span data-stu-id="70f0d-113">For example, hello IKEv2 main mode policies for Azure VPN gateways utilize only Diffie-Hellman Group 2 (1024 bits), whereas customers may need toospecify stronger groups toobe used in IKE, such as Group 14 (2048-bit), Group 24 (2048-bit MODP Group), or ECP (elliptic curve groups) 256 or 384 bit (Group 19 and Group 20, respectively).</span></span> <span data-ttu-id="70f0d-114">Requisitos de semelhantes aplicam políticas de modo rápido de tooIPsec bem.</span><span class="sxs-lookup"><span data-stu-id="70f0d-114">Similar requirements apply tooIPsec quick mode policies as well.</span></span>

## <a name="custom-ipsecike-policy-with-azure-vpn-gateways"></a><span data-ttu-id="70f0d-115">Política personalizada do IPsec/IKE com gateways de VPN do Azure</span><span class="sxs-lookup"><span data-stu-id="70f0d-115">Custom IPsec/IKE policy with Azure VPN gateways</span></span>
<span data-ttu-id="70f0d-116">Gateways de VPN do Azure suportam agora por ligação, a política personalizada do IPsec/IKE.</span><span class="sxs-lookup"><span data-stu-id="70f0d-116">Azure VPN gateways now support per-connection, custom IPsec/IKE policy.</span></span> <span data-ttu-id="70f0d-117">Para um Site para Site ou a ligação VNet a VNet, pode escolher uma combinação específica de algoritmos criptográficos para IPsec e IKE força de chave Olá assim o desejar, conforme mostrado no seguinte exemplo de Olá:</span><span class="sxs-lookup"><span data-stu-id="70f0d-117">For a Site-to-Site or VNet-to-VNet connection, you can choose a specific combination of cryptographic algorithms for IPsec and IKE with hello desired key strength, as shown in hello following example:</span></span>

![política de ike IPSec](./media/vpn-gateway-about-compliance-crypto/ipsecikepolicy.png)

<span data-ttu-id="70f0d-119">Pode criar uma política de IPsec/IKE e aplicar tooa a ligação de novo ou existente.</span><span class="sxs-lookup"><span data-stu-id="70f0d-119">You can create an IPsec/IKE policy and apply tooa new or existing connection.</span></span> 

### <a name="workflow"></a><span data-ttu-id="70f0d-120">Fluxo de trabalho</span><span class="sxs-lookup"><span data-stu-id="70f0d-120">Workflow</span></span>

1. <span data-ttu-id="70f0d-121">Criar redes virtuais Olá, gateways de VPN ou gateways de rede local para a topologia de conectividade, conforme descrito em outros toodocuments como</span><span class="sxs-lookup"><span data-stu-id="70f0d-121">Create hello virtual networks, VPN gateways, or local network gateways for your connectivity topology as described in other how-toodocuments</span></span>
2. <span data-ttu-id="70f0d-122">Criar uma política de IPsec/IKE</span><span class="sxs-lookup"><span data-stu-id="70f0d-122">Create an IPsec/IKE policy</span></span>
3. <span data-ttu-id="70f0d-123">Pode aplicar a política de Olá quando cria uma ligação S2S ou VNet a VNet</span><span class="sxs-lookup"><span data-stu-id="70f0d-123">You can apply hello policy when you create a S2S or VNet-to-VNet connection</span></span>
4. <span data-ttu-id="70f0d-124">Se a ligação de Olá já está a ser criada, pode aplicar ou atualizar a ligação do Olá política tooan existente</span><span class="sxs-lookup"><span data-stu-id="70f0d-124">If hello connection is already created, you can apply or update hello policy tooan existing connection</span></span>


## <a name="ipsecike-policy-faq"></a><span data-ttu-id="70f0d-125">FAQ da política de IPsec/IKE</span><span class="sxs-lookup"><span data-stu-id="70f0d-125">IPsec/IKE policy FAQ</span></span>

[!INCLUDE [vpn-gateway-ipsecikepolicy-faq-include](../../includes/vpn-gateway-ipsecikepolicy-faq-include.md)]


## <a name="next-steps"></a><span data-ttu-id="70f0d-126">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="70f0d-126">Next steps</span></span>
<span data-ttu-id="70f0d-127">Consulte [política IPsec/IKE configurar](vpn-gateway-ipsecikepolicy-rm-powershell.md) para obter instruções passo a passo sobre como configurar a política personalizada do IPsec/IKE numa ligação.</span><span class="sxs-lookup"><span data-stu-id="70f0d-127">See [Configure IPsec/IKE policy](vpn-gateway-ipsecikepolicy-rm-powershell.md) for step-by-step instructions on configuring custom IPsec/IKE policy on a connection.</span></span>

<span data-ttu-id="70f0d-128">Consulte também [ligar vários dispositivos VPN baseado na política](vpn-gateway-connect-multiple-policybased-rm-ps.md) toolearn mais informações sobre Olá UsePolicyBasedTrafficSelectors opção.</span><span class="sxs-lookup"><span data-stu-id="70f0d-128">See also [Connect multiple policy-based VPN devices](vpn-gateway-connect-multiple-policybased-rm-ps.md) toolearn more about hello UsePolicyBasedTrafficSelectors option.</span></span>
