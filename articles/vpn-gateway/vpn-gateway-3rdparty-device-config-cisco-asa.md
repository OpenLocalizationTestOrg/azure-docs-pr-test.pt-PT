---
title: "a configuração do aaaSample – ligar os gateways de VPN tooAzure de dispositivo de Cisco ASA | Microsoft Docs"
description: "Este artigo fornece uma configuração de exemplo para o dispositivo de Cisco ASA tooAzure gateways de VPN a ligar."
services: vpn-gateway
documentationcenter: na
author: yushwang
manager: rossort
editor: 
tags: 
ms.assetid: a8bfc955-de49-4172-95ac-5257e262d7ea
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/20/2017
ms.author: yushwang
ms.openlocfilehash: dad13e02afe8dad2379db750eb09602e08e8ea99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="sample-configuration-cisco-asa-device-ikev2no-bgp"></a><span data-ttu-id="84f50-103">Configuração de exemplo: Cisco ASA dispositivo (IKEv2/não BGP)</span><span class="sxs-lookup"><span data-stu-id="84f50-103">Sample configuration: Cisco ASA device (IKEv2/no BGP)</span></span>
<span data-ttu-id="84f50-104">Este artigo fornece configurações de exemplo para dispositivos de Cisco ASA tooAzure gateways de VPN a ligar.</span><span class="sxs-lookup"><span data-stu-id="84f50-104">This article provides sample configurations for Cisco ASA devices connecting tooAzure VPN gateways.</span></span>

## <a name="device-at-a-glance"></a><span data-ttu-id="84f50-105">Dispositivo de forma rápida</span><span class="sxs-lookup"><span data-stu-id="84f50-105">Device at a glance</span></span>

|                        |                                   |
| ---                    | ---                               |
| <span data-ttu-id="84f50-106">Fabricante do dispositivo</span><span class="sxs-lookup"><span data-stu-id="84f50-106">Device vendor</span></span>          | <span data-ttu-id="84f50-107">Cisco</span><span class="sxs-lookup"><span data-stu-id="84f50-107">Cisco</span></span>                             |
| <span data-ttu-id="84f50-108">Modelo do dispositivo</span><span class="sxs-lookup"><span data-stu-id="84f50-108">Device model</span></span>           | <span data-ttu-id="84f50-109">ASA (aplicação de segurança adaptável)</span><span class="sxs-lookup"><span data-stu-id="84f50-109">ASA (Adaptive Security Appliance)</span></span> |
| <span data-ttu-id="84f50-110">Versão de destino</span><span class="sxs-lookup"><span data-stu-id="84f50-110">Target version</span></span>         | <span data-ttu-id="84f50-111">8.4+</span><span class="sxs-lookup"><span data-stu-id="84f50-111">8.4+</span></span>                              |
| <span data-ttu-id="84f50-112">Modelo testado</span><span class="sxs-lookup"><span data-stu-id="84f50-112">Tested model</span></span>           | <span data-ttu-id="84f50-113">ASA 5505</span><span class="sxs-lookup"><span data-stu-id="84f50-113">ASA 5505</span></span>                          |
| <span data-ttu-id="84f50-114">Versão testada</span><span class="sxs-lookup"><span data-stu-id="84f50-114">Tested version</span></span>         | <span data-ttu-id="84f50-115">9.2</span><span class="sxs-lookup"><span data-stu-id="84f50-115">9.2</span></span>                               |
| <span data-ttu-id="84f50-116">Versão do IKE</span><span class="sxs-lookup"><span data-stu-id="84f50-116">IKE version</span></span>            | <span data-ttu-id="84f50-117">**IKEv2**</span><span class="sxs-lookup"><span data-stu-id="84f50-117">**IKEv2**</span></span>                         |
| <span data-ttu-id="84f50-118">BGP</span><span class="sxs-lookup"><span data-stu-id="84f50-118">BGP</span></span>                    | <span data-ttu-id="84f50-119">**Não**</span><span class="sxs-lookup"><span data-stu-id="84f50-119">**No**</span></span>                            |
| <span data-ttu-id="84f50-120">Tipo de gateway VPN do Azure</span><span class="sxs-lookup"><span data-stu-id="84f50-120">Azure VPN gateway type</span></span> | <span data-ttu-id="84f50-121">**Baseado na rota** gateway de VPN</span><span class="sxs-lookup"><span data-stu-id="84f50-121">**Route-based** VPN gateway</span></span>       |
|                        |                                   |

> [!NOTE]
> 1. <span data-ttu-id="84f50-122">configuração de Olá abaixo liga um tooan de dispositivo de Cisco ASA Azure **baseado na rota** VPN gateway com a política personalizada do IPsec/IKE com a opção "UserPolicyBasedTrafficSelectors", conforme descrito em [neste artigo](vpn-gateway-connect-multiple-policybased-rm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="84f50-122">hello configuration below connects a Cisco ASA device tooan Azure **route-based** VPN gateway using custom IPsec/IKE policy with "UserPolicyBasedTrafficSelectors" option, as described in [this article](vpn-gateway-connect-multiple-policybased-rm-ps.md).</span></span>
> 2. <span data-ttu-id="84f50-123">Requer ASA dispositivos toouse **IKEv2** com configurações de lista-baseada no acesso, não VTI com base em.</span><span class="sxs-lookup"><span data-stu-id="84f50-123">It requires ASA devices toouse **IKEv2** with access-list-based configurations, not VTI-based.</span></span>
> 3. <span data-ttu-id="84f50-124">Consulte com as especificações de fornecedor de dispositivo VPN política de Olá tooensure é suportada nos seus dispositivos VPN no local.</span><span class="sxs-lookup"><span data-stu-id="84f50-124">Please consult with your VPN device vendor specifications tooensure hello policy is supported on your on-premises VPN devices.</span></span>

## <a name="vpn-device-requirements"></a><span data-ttu-id="84f50-125">Requisitos de dispositivos VPN</span><span class="sxs-lookup"><span data-stu-id="84f50-125">VPN device requirements</span></span>
<span data-ttu-id="84f50-126">Gateways de VPN do Azure utilizam padrão IPsec/IKE protocolo conjuntos tooestablish túneis S2S VPN.</span><span class="sxs-lookup"><span data-stu-id="84f50-126">Azure VPN gateways use standard IPsec/IKE protocol suites tooestablish S2S VPN tunnels.</span></span> <span data-ttu-id="84f50-127">Consulte demasiado[acerca dos dispositivos VPN](vpn-gateway-about-vpn-devices.md) para Olá detalhadas os parâmetros de protocolo de IPsec/IKE e algoritmos de criptografia predefinido para gateways de VPN do Azure.</span><span class="sxs-lookup"><span data-stu-id="84f50-127">Refer too[About VPN devices](vpn-gateway-about-vpn-devices.md) for hello detailed IPsec/IKE protocol parameters and default cryptographic algorithms for Azure VPN gateways.</span></span> <span data-ttu-id="84f50-128">Opcionalmente, pode especificar combinação exato de Olá de algoritmos criptográficos e força da codificação chave para uma ligação específica, tal como descrito no [sobre os requisitos de criptografia](vpn-gateway-about-compliance-crypto.md).</span><span class="sxs-lookup"><span data-stu-id="84f50-128">You can optionally specify hello exact combination of cryptographic algorithms and key strengths for a specific connection as described in [About cryptographic requirements](vpn-gateway-about-compliance-crypto.md).</span></span> <span data-ttu-id="84f50-129">Se selecionar uma combinação específica de algoritmos criptográficos e chave força da codificação, certifique-se que utilizar especificações correspondente Olá nos seus dispositivos VPN.</span><span class="sxs-lookup"><span data-stu-id="84f50-129">If you select a specific combination of cryptographic algorithms and key strengths, please make sure you use hello corresponding specifications on your VPN devices.</span></span>

## <a name="single-vpn-tunnel"></a><span data-ttu-id="84f50-130">Túnel VPN único</span><span class="sxs-lookup"><span data-stu-id="84f50-130">Single VPN tunnel</span></span>
<span data-ttu-id="84f50-131">Esta topologia é composta por um único túnel de S2S VPN entre um gateway de VPN do Azure e o dispositivo VPN no local.</span><span class="sxs-lookup"><span data-stu-id="84f50-131">This topology consists of a single S2S VPN tunnel between an Azure VPN gateway and your on-premises VPN device.</span></span> <span data-ttu-id="84f50-132">Opcionalmente, pode configurar o BGP em túnel do Olá VPN.</span><span class="sxs-lookup"><span data-stu-id="84f50-132">You can optionally configure BGP across hello VPN tunnel.</span></span>

![túnel único](./media/vpn-gateway-3rdparty-device-config-cisco-asa/singletunnel.png)

<span data-ttu-id="84f50-134">Consulte demasiado[configuração de túnel único](vpn-gateway-3rdparty-device-config-overview.md#singletunnel) para detalhadas, instruções passo a passo toobuild Olá configurações do Azure.</span><span class="sxs-lookup"><span data-stu-id="84f50-134">Refer too[Single tunnel setup](vpn-gateway-3rdparty-device-config-overview.md#singletunnel) for detailed, step-by-step instructions toobuild hello Azure configurations.</span></span>

### <a name="network-and-vpn-gateway-information"></a><span data-ttu-id="84f50-135">Informações do gateway de rede e da VPN</span><span class="sxs-lookup"><span data-stu-id="84f50-135">Network and VPN gateway information</span></span>
<span data-ttu-id="84f50-136">Esta secção lista os parâmetros de Olá para Olá este exemplo.</span><span class="sxs-lookup"><span data-stu-id="84f50-136">This section list hello parameters for hello this sample.</span></span>

| <span data-ttu-id="84f50-137">**Parâmetro**</span><span class="sxs-lookup"><span data-stu-id="84f50-137">**Parameter**</span></span>                | <span data-ttu-id="84f50-138">**Valor**</span><span class="sxs-lookup"><span data-stu-id="84f50-138">**Value**</span></span>                    |
| ---                          | ---                          |
| <span data-ttu-id="84f50-139">Prefixos de endereço VNet</span><span class="sxs-lookup"><span data-stu-id="84f50-139">VNet address prefixes</span></span>        | <span data-ttu-id="84f50-140">10.11.0.0/16</span><span class="sxs-lookup"><span data-stu-id="84f50-140">10.11.0.0/16</span></span><br><span data-ttu-id="84f50-141">10.12.0.0/16</span><span class="sxs-lookup"><span data-stu-id="84f50-141">10.12.0.0/16</span></span> |
| <span data-ttu-id="84f50-142">IP do gateway VPN do Azure</span><span class="sxs-lookup"><span data-stu-id="84f50-142">Azure VPN gateway IP</span></span>         | <span data-ttu-id="84f50-143">Azure_Gateway_Public_IP</span><span class="sxs-lookup"><span data-stu-id="84f50-143">Azure_Gateway_Public_IP</span></span>      |
| <span data-ttu-id="84f50-144">Prefixos de endereço no local</span><span class="sxs-lookup"><span data-stu-id="84f50-144">On-premises address prefixes</span></span> | <span data-ttu-id="84f50-145">10.51.0.0/16</span><span class="sxs-lookup"><span data-stu-id="84f50-145">10.51.0.0/16</span></span><br><span data-ttu-id="84f50-146">10.52.0.0/16</span><span class="sxs-lookup"><span data-stu-id="84f50-146">10.52.0.0/16</span></span> |
| <span data-ttu-id="84f50-147">IP do dispositivo VPN no local</span><span class="sxs-lookup"><span data-stu-id="84f50-147">On-premises VPN device IP</span></span>    | <span data-ttu-id="84f50-148">OnPrem_Device_Public_IP</span><span class="sxs-lookup"><span data-stu-id="84f50-148">OnPrem_Device_Public_IP</span></span>     |
| <span data-ttu-id="84f50-149">* VNet ASN de BGP</span><span class="sxs-lookup"><span data-stu-id="84f50-149">*VNet BGP ASN</span></span>                | <span data-ttu-id="84f50-150">65010</span><span class="sxs-lookup"><span data-stu-id="84f50-150">65010</span></span>                        |
| <span data-ttu-id="84f50-151">* IP do elemento BGP do azure</span><span class="sxs-lookup"><span data-stu-id="84f50-151">*Azure BGP peer IP</span></span>           | <span data-ttu-id="84f50-152">10.12.255.30</span><span class="sxs-lookup"><span data-stu-id="84f50-152">10.12.255.30</span></span>                 |
| <span data-ttu-id="84f50-153">* No local ASN de BGP</span><span class="sxs-lookup"><span data-stu-id="84f50-153">*On-premises BGP ASN</span></span>         | <span data-ttu-id="84f50-154">65050</span><span class="sxs-lookup"><span data-stu-id="84f50-154">65050</span></span>                        |
| <span data-ttu-id="84f50-155">* IP do elemento BGP no local</span><span class="sxs-lookup"><span data-stu-id="84f50-155">*On-premises BGP peer IP</span></span>     | <span data-ttu-id="84f50-156">10.52.255.254</span><span class="sxs-lookup"><span data-stu-id="84f50-156">10.52.255.254</span></span>                |
|                              |                              |

* <span data-ttu-id="84f50-157">(*) Parâmetros opcionais para BGP apenas.</span><span class="sxs-lookup"><span data-stu-id="84f50-157">(*) Optional parameters for BGP only.</span></span>

### <a name="ipsecike-policy--parameters"></a><span data-ttu-id="84f50-158">Política do IPsec/IKE & parâmetros</span><span class="sxs-lookup"><span data-stu-id="84f50-158">IPsec/IKE policy & parameters</span></span>

<span data-ttu-id="84f50-159">tabela de Olá abaixo apresenta uma lista de algoritmos de IPsec/IKE Olá e parâmetros utilizados no exemplo de Olá.</span><span class="sxs-lookup"><span data-stu-id="84f50-159">hello table below lists hello IPsec/IKE algorithms and parameters used in hello sample.</span></span> <span data-ttu-id="84f50-160">Consulte o toomake de especificações de dispositivo VPN se de que todos os algoritmos listados acima são suportados pelo seu modelos de dispositivos VPN e as versões de firmware.</span><span class="sxs-lookup"><span data-stu-id="84f50-160">Please consult your VPN device specifications toomake sure all algorithms listed above are supported by your VPN device models and firmware versions.</span></span>

| <span data-ttu-id="84f50-161">**IPsec/IKEv2**</span><span class="sxs-lookup"><span data-stu-id="84f50-161">**IPsec/IKEv2**</span></span>  | <span data-ttu-id="84f50-162">**Valor**</span><span class="sxs-lookup"><span data-stu-id="84f50-162">**Value**</span></span>                            |
| ---              | ---                                  |
| <span data-ttu-id="84f50-163">Encriptação IKEv2</span><span class="sxs-lookup"><span data-stu-id="84f50-163">IKEv2 Encryption</span></span> | <span data-ttu-id="84f50-164">AES256</span><span class="sxs-lookup"><span data-stu-id="84f50-164">AES256</span></span>                               |
| <span data-ttu-id="84f50-165">Integridade do IKEv2</span><span class="sxs-lookup"><span data-stu-id="84f50-165">IKEv2 Integrity</span></span>  | <span data-ttu-id="84f50-166">SHA384</span><span class="sxs-lookup"><span data-stu-id="84f50-166">SHA384</span></span>                               |
| <span data-ttu-id="84f50-167">Grupo DH</span><span class="sxs-lookup"><span data-stu-id="84f50-167">DH Group</span></span>         | <span data-ttu-id="84f50-168">DHGroup24</span><span class="sxs-lookup"><span data-stu-id="84f50-168">DHGroup24</span></span>                            |
| <span data-ttu-id="84f50-169">Encriptação do IPsec</span><span class="sxs-lookup"><span data-stu-id="84f50-169">IPsec Encryption</span></span> | <span data-ttu-id="84f50-170">AES256</span><span class="sxs-lookup"><span data-stu-id="84f50-170">AES256</span></span>                               |
| <span data-ttu-id="84f50-171">Integridade do IPsec</span><span class="sxs-lookup"><span data-stu-id="84f50-171">IPsec Integrity</span></span>  | <span data-ttu-id="84f50-172">SHA1</span><span class="sxs-lookup"><span data-stu-id="84f50-172">SHA1</span></span>                                 |
| <span data-ttu-id="84f50-173">Grupo PFS</span><span class="sxs-lookup"><span data-stu-id="84f50-173">PFS Group</span></span>        | <span data-ttu-id="84f50-174">PFS24</span><span class="sxs-lookup"><span data-stu-id="84f50-174">PFS24</span></span>                                |
| <span data-ttu-id="84f50-175">Duração de SA QM</span><span class="sxs-lookup"><span data-stu-id="84f50-175">QM SA Lifetime</span></span>   | <span data-ttu-id="84f50-176">segundos de 7200</span><span class="sxs-lookup"><span data-stu-id="84f50-176">7200 seconds</span></span>                         |
| <span data-ttu-id="84f50-177">Seletor de tráfego</span><span class="sxs-lookup"><span data-stu-id="84f50-177">Traffic Selector</span></span> | <span data-ttu-id="84f50-178">UsePolicyBasedTrafficSelectors $True</span><span class="sxs-lookup"><span data-stu-id="84f50-178">UsePolicyBasedTrafficSelectors $True</span></span> |
| <span data-ttu-id="84f50-179">Chave Pré-partilhada</span><span class="sxs-lookup"><span data-stu-id="84f50-179">Pre-Shared Key</span></span>   | <span data-ttu-id="84f50-180">PreSharedKey</span><span class="sxs-lookup"><span data-stu-id="84f50-180">PreSharedKey</span></span>                         |
|                  |                                      |

- <span data-ttu-id="84f50-181">(*) Em alguns dispositivos, IPsec integridade tem de ser "null" se GCM AES é utilizado como o algoritmo de encriptação de IPsec.</span><span class="sxs-lookup"><span data-stu-id="84f50-181">(*) On some device, IPsec integrity must be "null" if GCM-AES is used as IPsec encryption algorithm.</span></span>

### <a name="device-notes"></a><span data-ttu-id="84f50-182">Notas de dispositivo</span><span class="sxs-lookup"><span data-stu-id="84f50-182">Device notes</span></span>

>[!NOTE]
>
> 1. <span data-ttu-id="84f50-183">Suporte do IKEv2 requer ASA versão 8.4 e superior.</span><span class="sxs-lookup"><span data-stu-id="84f50-183">IKEv2 support requires ASA version 8.4 and above.</span></span>
> 2. <span data-ttu-id="84f50-184">Suporte de grupo DH superior e PFS (além do grupo de 5) requer a versão do ASA 9.x.</span><span class="sxs-lookup"><span data-stu-id="84f50-184">Higher DH and PFS group support (beyond Group 5) requires ASA version 9.x.</span></span>
> 3. <span data-ttu-id="84f50-185">Encriptação de IPsec com AES-GCM e IPsec integridade com o SHA-256, SHA-384, suporte de SHA-512 requer a versão do ASA 9.x no hardware mais recente do ASA; 5505 ASA, 5510, 5520, 5540, 5550, são 5580 **não** suportado.</span><span class="sxs-lookup"><span data-stu-id="84f50-185">IPsec encryption with AES-GCM and IPsec integrity with SHA-256, SHA-384, SHA-512 support requires ASA version 9.x on newer ASA hardware; ASA 5505, 5510, 5520, 5540, 5550, 5580 are **not** supported.</span></span> <span data-ttu-id="84f50-186">(Verifique Olá fornecedor especificações tooconfirm.)</span><span class="sxs-lookup"><span data-stu-id="84f50-186">(Please check hello vendor specifications tooconfirm.)</span></span>
>


### <a name="sample-device-configurations"></a><span data-ttu-id="84f50-187">Configurações de dispositivos de exemplo</span><span class="sxs-lookup"><span data-stu-id="84f50-187">Sample device configurations</span></span>
<span data-ttu-id="84f50-188">script de Olá abaixo fornece uma configuração de exemplo com base na topologia de Olá e os parâmetros indicados acima.</span><span class="sxs-lookup"><span data-stu-id="84f50-188">hello script below provides a sample configuration based on hello topology and parameters listed above.</span></span> <span data-ttu-id="84f50-189">configuração de túnel S2S VPN Olá consiste Olá seguintes partes:</span><span class="sxs-lookup"><span data-stu-id="84f50-189">hello S2S VPN tunnel configuration consists of hello following parts:</span></span>

1. <span data-ttu-id="84f50-190">Interfaces & rotas</span><span class="sxs-lookup"><span data-stu-id="84f50-190">Interfaces & routes</span></span>
2. <span data-ttu-id="84f50-191">Apresenta uma lista de acesso</span><span class="sxs-lookup"><span data-stu-id="84f50-191">Access lists</span></span>
3. <span data-ttu-id="84f50-192">Política de IKE e parâmetros (a fase 1 ou modo principal)</span><span class="sxs-lookup"><span data-stu-id="84f50-192">IKE policy and parameters (Phase 1 or Main Mode)</span></span>
4. <span data-ttu-id="84f50-193">Política de IPsec e parâmetros (a fase 2 ou modo rápido)</span><span class="sxs-lookup"><span data-stu-id="84f50-193">IPsec policy and parameters (Phase 2 or Quick Mode)</span></span>
5. <span data-ttu-id="84f50-194">Outros parâmetros (TCP MSS clamping, etc.)</span><span class="sxs-lookup"><span data-stu-id="84f50-194">Other parameters (TCP MSS clamping, etc.)</span></span>

>[!IMPORTANT] 
><span data-ttu-id="84f50-195">Certifique-se que conclua a configuração adicional Olá listada abaixo e substitui os marcadores de Olá com valores reais Olá:</span><span class="sxs-lookup"><span data-stu-id="84f50-195">Please make sure you complete hello additional configuration listed below and replace hello placeholders with hello actual values:</span></span>
> 
> - <span data-ttu-id="84f50-196">Configuração para dentro e fora de interfaces de interface</span><span class="sxs-lookup"><span data-stu-id="84f50-196">Interface configuration for both inside and outside interfaces</span></span>
> - <span data-ttu-id="84f50-197">Rotas para as redes privadas/dentro e fora/público</span><span class="sxs-lookup"><span data-stu-id="84f50-197">Routes for your inside/private and outside/public networks</span></span>
> - <span data-ttu-id="84f50-198">Certifique-se de que todos os nomes e números de política são exclusivos num dispositivo Olá</span><span class="sxs-lookup"><span data-stu-id="84f50-198">Ensure all names and policy numbers are unique on hello device</span></span>
> - <span data-ttu-id="84f50-199">Certifique-se de que são suportados os algoritmos de criptografia Olá no seu dispositivo</span><span class="sxs-lookup"><span data-stu-id="84f50-199">Ensure hello cryptographic algorithms are supported on your device</span></span>
> - <span data-ttu-id="84f50-200">Substitua Olá seguir proprietários do local com os valores reais Olá</span><span class="sxs-lookup"><span data-stu-id="84f50-200">Replace hello following place holders with hello actual values</span></span>
>   - <span data-ttu-id="84f50-201">Fora do nome de interface: "fora"</span><span class="sxs-lookup"><span data-stu-id="84f50-201">Outside interface name: "outside"</span></span>
>   - <span data-ttu-id="84f50-202">Azure_Gateway_Public_IP</span><span class="sxs-lookup"><span data-stu-id="84f50-202">Azure_Gateway_Public_IP</span></span>
>   - <span data-ttu-id="84f50-203">OnPrem_Device_Public_IP</span><span class="sxs-lookup"><span data-stu-id="84f50-203">OnPrem_Device_Public_IP</span></span>
>   - <span data-ttu-id="84f50-204">Pre_Shared_Key do IKE</span><span class="sxs-lookup"><span data-stu-id="84f50-204">IKE Pre_Shared_Key</span></span>
>   - <span data-ttu-id="84f50-205">VNet e nomes de gateway de rede local (VNetName, LNGName)</span><span class="sxs-lookup"><span data-stu-id="84f50-205">VNet and local network gateway names (VNetName, LNGName)</span></span>
>   - <span data-ttu-id="84f50-206">Os prefixos de endereços de rede de VNet e no local</span><span class="sxs-lookup"><span data-stu-id="84f50-206">VNet and on-premises network address prefixes</span></span>
>   - <span data-ttu-id="84f50-207">Netmasks adequada</span><span class="sxs-lookup"><span data-stu-id="84f50-207">Proper netmasks</span></span>

#### <a name="sample-configuration"></a><span data-ttu-id="84f50-208">Configuração de exemplo</span><span class="sxs-lookup"><span data-stu-id="84f50-208">Sample configuration</span></span>

```
! Sample ASA configuration for connecting tooAzure VPN gateway
!
! Tested hardware: ASA 5505
! Tested version:  ASA version 9.2(4)
!
! Replace hello following place holders with your actual values:
!   - Interface names - default are "outside" and "inside"
!   - <Azure_Gateway_Public_IP>
!   - <OnPrem_Device_Public_IP>
!   - <Pre_Shared_Key>
!   - <VNetName>*
!   - <LNGName>* ==> LocalNetworkGateway - hello Azure resource that represents the
!     on-premises network, specifies network prefixes, device public IP, BGP info, etc.
!   - <PrivateIPAddress> ==> Replace it with a private IP address if applicable
!   - <Netmask> ==> Replace it with appropriate netmasks
!   - <Nexthop> ==> Replace it with hello actual nexthop IP address
!
! (*) Must be unique names in hello device configuration
!
! ==> Interface & route configurations
!
!     > <OnPrem_Device_Public_IP> address on hello outside interface or vlan
!     > <PrivateIPAddress> on hello inside interface or vlan; e.g., 10.51.0.1/24
!     > Route tooconnect too<Azure_Gateway_Public_IP> address
!
!     > Example:
!
!       interface Ethernet0/0
!        switchport access vlan 2
!       exit
!
!       interface vlan 1
!        nameif inside
!        security-level 100
!        ip address <PrivateIPAddress> <Netmask>
!       exit
!
!       interface vlan 2
!        nameif outside
!        security-level 0
!        ip address <OnPrem_Device_Public_IP> <Netmask>
!       exit
!
!       route outside 0.0.0.0 0.0.0.0 <NextHop IP> 1
!
! ==> Access lists
!
!     > Most firewall devices deny all traffic by default. Create access lists to
!       (1) Allow S2S VPN tunnels between hello ASA and hello Azure gateway public IP address
!       (2) Construct traffic selectors as part of IPsec policy or proposal
!
access-list outside_access_in extended permit ip host <Azure_Gateway_Public_IP> host <OnPrem_Device_Public_IP>
!
!     > Object group that consists of all VNet prefixes (e.g., 10.11.0.0/16 &
!       10.12.0.0/16)
!
object-group network Azure-<VNetName>
 description Azure virtual network <VNetName> prefixes
 network-object 10.11.0.0 255.255.0.0
 network-object 10.12.0.0 255.255.0.0
exit
!
!     > Object group that corresponding toohello <LNGName> prefixes.
!       E.g., 10.51.0.0/16 and 10.52.0.0/16. Note that LNG = "local network gateway".
!       In Azure network resource, a local network gateway defines hello on-premises
!       network properties (address prefixes, VPN device IP, BGP ASN, etc.)
!
object-group network <LNGName>
 description On-Premises network <LNGName> prefixes
 network-object 10.51.0.0 255.255.0.0
 network-object 10.52.0.0 255.255.0.0
exit
!
!     > Specify hello access-list between hello Azure VNet and your on-premises network.
!       This access list defines hello IPsec SA traffic selectors.
!
access-list Azure-<VNetName>-acl extended permit ip object-group <LNGName> object-group Azure-<VNetName>
!
!     > No NAT required between hello on-premises network and Azure VNet
!
nat (inside,outside) source static <LNGName> <LNGName> destination static Azure-<VNetName> Azure-<VNetName>
!
! ==> IKEv2 configuration
!
!     > General IKEv2 configuration - enable IKEv2 for VPN
!
group-policy DfltGrpPolicy attributes
 vpn-tunnel-protocol ikev1 ikev2
exit
!
crypto isakmp identity address
crypto ikev2 enable outside
!
!     > Define IKEv2 Phase 1/Main Mode policy
!       - Make sure hello policy number is not used
!       - integrity and prf must be hello same
!       - DH group 14 and above require ASA version 9.x.
!
crypto ikev2 policy 1
 encryption       aes-256
 integrity        sha384
 prf              sha384
 group            24
 lifetime seconds 86400
exit
!
!     > Set connection type and pre-shared key
!
tunnel-group <Azure_Gateway_Public_IP> type ipsec-l2l
tunnel-group <Azure_Gateway_Public_IP> ipsec-attributes
 ikev2 remote-authentication pre-shared-key <Pre_Shared_Key> 
 ikev2 local-authentication  pre-shared-key <Pre_Shared_Key> 
exit
!
! ==> IPsec configuration
!
!     > IKEv2 Phase 2/Quick Mode proposal
!       - AES-GCM and SHA-2 requires ASA version 9.x on newer ASA models. ASA
!         5505, 5510, 5520, 5540, 5550, 5580 are not supported.
!       - ESP integrity must be null if AES-GCM is configured as ESP encryption
!
crypto ipsec ikev2 ipsec-proposal AES-256
 protocol esp encryption aes-256
 protocol esp integrity  sha-1
exit
!
!     > Set access list & traffic selectors, PFS, IPsec protposal, SA lifetime
!       - This sample uses "Azure-<VNetName>-map" as hello crypto map name
!       - ASA supports only one crypto map per interface, if you already have
!         an existing crypto map assigned tooyour outside interface, you must use
!         hello same crypto map name, but with a different sequence number for
!         this policy
!       - "match address" policy uses hello access-list "Azure-<VNetName>-acl" defined 
!         previously
!       - "ipsec-proposal" uses hello proposal "AES-256" defined previously 
!       - PFS groups 14 and beyond requires ASA version 9.x.
!
crypto map Azure-<VNetName>-map 1 match address Azure-<VNetName>-acl
crypto map Azure-<VNetName>-map 1 set pfs group24
crypto map Azure-<VNetName>-map 1 set peer <Azure_Gateway_Public_IP>
crypto map Azure-<VNetName>-map 1 set ikev2 ipsec-proposal AES-256
crypto map Azure-<VNetName>-map 1 set security-association lifetime seconds 7200
crypto map Azure-<VNetName>-map interface outside
!
! ==> Set TCP MSS too1350
!
sysopt connection tcpmss 1350
!
```

## <a name="simple-debugging-commands"></a><span data-ttu-id="84f50-209">Comandos de depuração simples</span><span class="sxs-lookup"><span data-stu-id="84f50-209">Simple debugging commands</span></span>

<span data-ttu-id="84f50-210">Eis alguns comandos do ASA para fins de depuração:</span><span class="sxs-lookup"><span data-stu-id="84f50-210">Here are some ASA commands for debugging purposes:</span></span>

1. <span data-ttu-id="84f50-211">Mostrar Olá IPsec e do IKE SA</span><span class="sxs-lookup"><span data-stu-id="84f50-211">Show hello IPsec and IKE SA's</span></span>
    - <span data-ttu-id="84f50-212">"Mostrar ipsec criptografia sa"</span><span class="sxs-lookup"><span data-stu-id="84f50-212">"show crypto ipsec sa"</span></span>
    - <span data-ttu-id="84f50-213">"Mostrar crypto ikev2 sa"</span><span class="sxs-lookup"><span data-stu-id="84f50-213">"show crypto ikev2 sa"</span></span>
2. <span data-ttu-id="84f50-214">Modo de depuração entrar - Isto pode obter muito desnecessárias, na consola de Olá</span><span class="sxs-lookup"><span data-stu-id="84f50-214">Entering debug mode - this can get very noisy on hello console</span></span>
    - <span data-ttu-id="84f50-215">"depuração ikev2 criptografia plataforma <level>"</span><span class="sxs-lookup"><span data-stu-id="84f50-215">"debug crypto ikev2 platform <level>"</span></span>
    - <span data-ttu-id="84f50-216">"protocolo ikev2 criptografia de depuração <level>"</span><span class="sxs-lookup"><span data-stu-id="84f50-216">"debug crypto ikev2 protocol <level>"</span></span>
3. <span data-ttu-id="84f50-217">Lista de configurações atuais</span><span class="sxs-lookup"><span data-stu-id="84f50-217">List current configurations</span></span>
    - <span data-ttu-id="84f50-218">"Mostrar execução" - mostra Olá configurações atuais num dispositivo Olá; Pode utilizar Olá vários comandos secundárias toolist partes específicas da configuração de Olá.</span><span class="sxs-lookup"><span data-stu-id="84f50-218">"show run" - shows hello current configurations on hello device; you can use hello various sub-commands toolist specific parts of hello configuration.</span></span> <span data-ttu-id="84f50-219">Por exemplo, "Mostrar executar criptografia", "Mostrar executar a lista de acesso", "Mostrar executar o grupo de túnel", etc.</span><span class="sxs-lookup"><span data-stu-id="84f50-219">E.g., "show run crypto", "show run access-list", "show run tunnel-group", etc.</span></span>


## <a name="next-steps"></a><span data-ttu-id="84f50-220">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="84f50-220">Next steps</span></span>
<span data-ttu-id="84f50-221">Consulte [configurar Gateways de VPN de ativo-ativo em vários locais e ligações VNet a VNet](vpn-gateway-activeactive-rm-powershell.md) para passos tooconfigure ativo-ativo em vários locais e ligações VNet a VNet.</span><span class="sxs-lookup"><span data-stu-id="84f50-221">See [Configuring Active-Active VPN Gateways for Cross-Premises and VNet-to-VNet Connections](vpn-gateway-activeactive-rm-powershell.md) for steps tooconfigure active-active cross-premises and VNet-to-VNet connections.</span></span>

