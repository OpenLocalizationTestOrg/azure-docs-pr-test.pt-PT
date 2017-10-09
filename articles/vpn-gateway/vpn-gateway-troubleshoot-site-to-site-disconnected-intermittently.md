---
title: aaaTroubleshoot VPN de Site para Site do Azure desliga ligados intermitentemente | Microsoft Docs
description: "Saiba como tootroubleshoot Olá problema na ligação de VPN de Site a Site que Olá desligado regularmente."
services: vpn-gateway
documentationcenter: na
author: chadmath
manager: cshepard
editor: 
tags: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/21/2017
ms.author: genli
ms.openlocfilehash: 1ce3c4ff9d8f650312e45f33b760ebcc6597fc13
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-azure-site-to-site-vpn-disconnects-intermittently"></a><span data-ttu-id="00b7c-103">Resolução de problemas: VPN de Site para Site do Azure desliga ligados intermitentemente</span><span class="sxs-lookup"><span data-stu-id="00b7c-103">Troubleshooting: Azure Site-to-Site VPN disconnects intermittently</span></span>

<span data-ttu-id="00b7c-104">Podem ocorrer problemas de Olá que uma ligação de VPN do Microsoft Azure ponto a Site nova ou existente não está estável ou desliga regularmente.</span><span class="sxs-lookup"><span data-stu-id="00b7c-104">You might experience hello problem that a new or existing Microsoft Azure Point-to-Site VPN connection is not stable or disconnects regularly.</span></span> <span data-ttu-id="00b7c-105">Este artigo fornece os passos toohelp identificar e resolver o problema de Olá causa Olá de resolução de problemas.</span><span class="sxs-lookup"><span data-stu-id="00b7c-105">This article provides troubleshoot steps toohelp you identify and resolve hello cause of hello problem.</span></span> 

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="troubleshooting-steps"></a><span data-ttu-id="00b7c-106">Passos de resolução de problemas</span><span class="sxs-lookup"><span data-stu-id="00b7c-106">Troubleshooting steps</span></span>

### <a name="prerequisite-step"></a><span data-ttu-id="00b7c-107">Passo pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="00b7c-107">Prerequisite step</span></span>

<span data-ttu-id="00b7c-108">Verifique o tipo de Olá do gateway de rede virtual do Azure:</span><span class="sxs-lookup"><span data-stu-id="00b7c-108">Check hello type of Azure  virtual network gateway:</span></span>

1. <span data-ttu-id="00b7c-109">Aceda demasiado[portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="00b7c-109">Go too[Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="00b7c-110">Verifique Olá **descrição geral** página Olá virtuais do gateway de rede para obter informações de tipo Olá.</span><span class="sxs-lookup"><span data-stu-id="00b7c-110">Check hello **Overview** page of hello virtual network gateway for hello type information.</span></span>
    
    ![Descrição geral de Olá do gateway de Olá](media\vpn-gateway-troubleshoot-site-to-site-disconnected-intermittently\gatewayoverview.png)

### <a name="step-1-check-whether-hello-on-premises-vpn-device-is-validated"></a><span data-ttu-id="00b7c-112">Passo 1 Verifique se Olá no local o dispositivo VPN é validado</span><span class="sxs-lookup"><span data-stu-id="00b7c-112">Step 1 Check whether hello on-premises VPN device is validated</span></span>

1. <span data-ttu-id="00b7c-113">Verifique se estão a utilizar um [validar o dispositivo VPN e versão do sistema operativo](vpn-gateway-about-vpn-devices.md#devicetable).</span><span class="sxs-lookup"><span data-stu-id="00b7c-113">Check whether you are using a [validated VPN device and operating system version](vpn-gateway-about-vpn-devices.md#devicetable).</span></span> <span data-ttu-id="00b7c-114">Se o dispositivo VPN Olá não é validado, poderá ter toocontact Olá dispositivo fabricante toosee se existir qualquer problema de compatibilidade.</span><span class="sxs-lookup"><span data-stu-id="00b7c-114">If hello VPN device is not validated, you may have toocontact hello device manufacturer toosee if there is any compatibility issue.</span></span>
2. <span data-ttu-id="00b7c-115">Certifique-se de que o dispositivo VPN Olá está configurado corretamente.</span><span class="sxs-lookup"><span data-stu-id="00b7c-115">Make sure that hello VPN device is correctly configured.</span></span> <span data-ttu-id="00b7c-116">Para obter mais informações, consulte [editar exemplos de configuração do dispositivo](vpn-gateway-about-vpn-devices.md#editing).</span><span class="sxs-lookup"><span data-stu-id="00b7c-116">For more information, see [Editing device configuration samples](vpn-gateway-about-vpn-devices.md#editing).</span></span>

### <a name="step-2-check-hello-security-association-settingsfor-policy-based-azure-virtual-network-gateways"></a><span data-ttu-id="00b7c-117">Definições de associação de segurança do passo 2 verificação Olá (para gateways de rede virtual do Azure baseada em políticas)</span><span class="sxs-lookup"><span data-stu-id="00b7c-117">Step 2 Check hello Security Association settings(for policy-based Azure virtual network gateways)</span></span>

1. <span data-ttu-id="00b7c-118">Certifique-se nessa rede virtual Olá, sub-redes e intervalos de na Olá **gateway de rede Local** definição no Microsoft Azure são o mesmo que a configuração de Olá no dispositivo VPN do Olá no local.</span><span class="sxs-lookup"><span data-stu-id="00b7c-118">Make sure that hello virtual network, subnets and, ranges in hello **Local network gateway** definition in Microsoft Azure are same as hello configuration on hello on-premises VPN device.</span></span>
2. <span data-ttu-id="00b7c-119">Certifique-se de que corresponda de definições de associação de segurança de Olá.</span><span class="sxs-lookup"><span data-stu-id="00b7c-119">Verify that hello Security Association settings match.</span></span>

### <a name="step-3-check-for-user-defined-routes-or-network-security-groups-on-gateway-subnet"></a><span data-ttu-id="00b7c-120">Passo 3 procurar rotas definidas pelo utilizador ou grupos de segurança de rede na sub-rede de Gateway</span><span class="sxs-lookup"><span data-stu-id="00b7c-120">Step 3 Check for User-Defined Routes or Network Security Groups on Gateway Subnet</span></span>

<span data-ttu-id="00b7c-121">Uma rota definida pelo utilizador na sub-rede de gateway Olá pode ser restringir algum tráfego e permitindo que o tráfego restante.</span><span class="sxs-lookup"><span data-stu-id="00b7c-121">A user-defined route on hello gateway subnet may be restricting some traffic and allowing other traffic.</span></span> <span data-ttu-id="00b7c-122">Isto faz com que são apresentados se a ligação de VPN de Olá está pouco fiáveis para algum tráfego e ideais para outras pessoas.</span><span class="sxs-lookup"><span data-stu-id="00b7c-122">This makes it appear that hello VPN connection is unreliable for some traffic and good for others.</span></span> 

### <a name="step-4-check-hello-one-vpn-tunnel-per-subnet-pair-setting-for-policy-based-virtual-network-gateways"></a><span data-ttu-id="00b7c-123">Passo 4 verificação Olá "um túnel VPN por par sub-rede" definição (para gateways de rede virtual baseada em políticas)</span><span class="sxs-lookup"><span data-stu-id="00b7c-123">Step 4 Check hello "one VPN Tunnel per Subnet Pair" setting (for policy-based virtual network gateways)</span></span>

<span data-ttu-id="00b7c-124">Certifique-se de que Olá no local VPN está configurado toohave **um túnel VPN por par sub-rede** para gateways de rede virtual baseada em políticas.</span><span class="sxs-lookup"><span data-stu-id="00b7c-124">Make sure that hello on-premises VPN device is set toohave **one VPN tunnel per subnet pair** for policy-based virtual network gateways.</span></span>

### <a name="step-5-check-for-security-association-limitation-for-policy-based-virtual-network-gateways"></a><span data-ttu-id="00b7c-125">Passo 5 procurar limitação de associação de segurança (para gateways de rede virtual baseada em políticas)</span><span class="sxs-lookup"><span data-stu-id="00b7c-125">Step 5 Check for Security Association Limitation (for policy-based virtual network gateways)</span></span>

<span data-ttu-id="00b7c-126">gateway de rede virtual baseada em políticas Olá tem o limite de 200 pares de associação de segurança de sub-rede.</span><span class="sxs-lookup"><span data-stu-id="00b7c-126">hello Policy-based virtual network gateway has limit of 200 subnet Security Association pairs.</span></span> <span data-ttu-id="00b7c-127">Se o número de Olá de sub-redes de rede virtual do Azure multiplicado vezes por Olá número de sub-redes locais é superior a 200, ver sub-redes esporádicas desligar.</span><span class="sxs-lookup"><span data-stu-id="00b7c-127">If hello number of Azure virtual network subnets multiplied times by hello number of local subnets is greater than 200, you see sporadic subnets disconnecting.</span></span>

### <a name="step-6-check-on-premises-vpn-device-external-interface-address"></a><span data-ttu-id="00b7c-128">Passo 6 verificação no local o endereço de interface externa do dispositivo VPN</span><span class="sxs-lookup"><span data-stu-id="00b7c-128">Step 6 Check on-premises VPN device external interface address</span></span>

- <span data-ttu-id="00b7c-129">Se hello Internet com o endereço IP do dispositivo VPN Olá está incluída no Olá **gateway de rede Local** definição no Azure, pode deparar-se esporádicas interrupções de ligação.</span><span class="sxs-lookup"><span data-stu-id="00b7c-129">If hello Internet facing IP address of hello VPN device is included in hello **Local network gateway** definition in Azure, you may experience sporadic disconnections.</span></span>
- <span data-ttu-id="00b7c-130">Olá interface externa do dispositivo tem de ser diretamente no Olá Internet.</span><span class="sxs-lookup"><span data-stu-id="00b7c-130">hello device's external interface must be directly on hello Internet.</span></span> <span data-ttu-id="00b7c-131">Não deverá haver nenhum tradução de endereços de rede (NAT) ou firewall entre Olá Internet e o dispositivo de Olá.</span><span class="sxs-lookup"><span data-stu-id="00b7c-131">There should be no Network Address Translation (NAT) or firewall between hello Internet and hello device.</span></span>
-  <span data-ttu-id="00b7c-132">Se configurar o Clustering de Firewall toohave um IP virtual, tem de interromper a cluster Olá e expor o dispositivo de VPN Olá diretamente tooa interface pública que Olá gateway pode interagir com.</span><span class="sxs-lookup"><span data-stu-id="00b7c-132">If you configure Firewall Clustering toohave a virtual IP, you must break hello cluster and expose hello VPN appliance directly tooa public interface that hello gateway can interface with.</span></span>

### <a name="step-7-check-whether-hello-on-premises-vpn-device-has-perfect-forward-secrecy-enabled"></a><span data-ttu-id="00b7c-133">Passo 7 de verificação se Olá no local o dispositivo VPN tem Perfect Forward Secrecy ativada</span><span class="sxs-lookup"><span data-stu-id="00b7c-133">Step 7 Check whether hello on-premises VPN device has Perfect Forward Secrecy enabled</span></span>

<span data-ttu-id="00b7c-134">Olá **Perfect Forward Secrecy** funcionalidade pode causar problemas de interrupção de ligação de Olá.</span><span class="sxs-lookup"><span data-stu-id="00b7c-134">hello **Perfect Forward Secrecy** feature can cause hello disconnection problems.</span></span> <span data-ttu-id="00b7c-135">Se tiver de dispositivo VPN Olá **perfeita Secrecy reencaminhar** ativada, desative a funcionalidade de Olá.</span><span class="sxs-lookup"><span data-stu-id="00b7c-135">If hello VPN device has **Perfect forward Secrecy** enabled, disable hello feature.</span></span> <span data-ttu-id="00b7c-136">Em seguida, [atualizar a política de IPsec do gateway de rede virtual Olá](vpn-gateway-ipsecikepolicy-rm-powershell.md#managepolicy).</span><span class="sxs-lookup"><span data-stu-id="00b7c-136">Then [update hello virtual network gateway IPsec policy](vpn-gateway-ipsecikepolicy-rm-powershell.md#managepolicy).</span></span>

## <a name="next-steps"></a><span data-ttu-id="00b7c-137">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="00b7c-137">Next steps</span></span>

- [<span data-ttu-id="00b7c-138">Configurar uma rede virtual do Site para Site ligação tooa</span><span class="sxs-lookup"><span data-stu-id="00b7c-138">Configure a Site-to-Site connection tooa virtual network</span></span>](vpn-gateway-howto-site-to-site-resource-manager-portal.md)
- [<span data-ttu-id="00b7c-139">Configurar a política de IPsec/IKE para ligações VPN de Site a Site</span><span class="sxs-lookup"><span data-stu-id="00b7c-139">Configure IPsec/IKE policy for Site-to-Site VPN connections</span></span>](vpn-gateway-ipsecikepolicy-rm-powershell.md)

