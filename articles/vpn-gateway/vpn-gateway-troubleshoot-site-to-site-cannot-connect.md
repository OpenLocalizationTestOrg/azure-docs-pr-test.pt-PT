---
title: "aaaTroubleshoot uma ligação de VPN de site para site do Azure que não é possível ligar | Microsoft Docs"
description: "Saiba como tootroubleshoot uma ligação de VPN de site a site que subitamente deixa de funcionar e não pode ser novamente ligado."
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
ms.openlocfilehash: 632c75bfcfb93a532eeead2855d43e6614569a99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-an-azure-site-to-site-vpn-connection-cannot-connect-and-stops-working"></a><span data-ttu-id="c92f9-103">Resolução de problemas: Uma ligação de VPN de site para site do Azure não é possível ligar e deixa de funcionar</span><span class="sxs-lookup"><span data-stu-id="c92f9-103">Troubleshooting: An Azure site-to-site VPN connection cannot connect and stops working</span></span>

<span data-ttu-id="c92f9-104">Depois de configurar uma ligação de VPN de site a site entre uma rede no local e uma Azure virtual network, Olá ligação VPN deixa de funcionar e não pode ser novamente ligado.</span><span class="sxs-lookup"><span data-stu-id="c92f9-104">After you configure a site-to-site VPN connection between an on-premises network and an Azure virtual network, hello VPN connection suddenly stops working and cannot be reconnected.</span></span> <span data-ttu-id="c92f9-105">Este artigo fornece a resolução de problemas de passos toohelp resolver este problema.</span><span class="sxs-lookup"><span data-stu-id="c92f9-105">This article provides troubleshooting steps toohelp you resolve this problem.</span></span> 

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="troubleshooting-steps"></a><span data-ttu-id="c92f9-106">Passos de resolução de problemas</span><span class="sxs-lookup"><span data-stu-id="c92f9-106">Troubleshooting steps</span></span>

<span data-ttu-id="c92f9-107">problema de Olá tooresolve, tente primeiro demasiado[reposição Olá VPN gateway do Azure](vpn-gateway-resetgw-classic.md) e repor o túnel Olá dispositivo de VPN no local Olá.</span><span class="sxs-lookup"><span data-stu-id="c92f9-107">tooresolve hello problem, first try too[reset hello Azure VPN gateway](vpn-gateway-resetgw-classic.md) and reset hello tunnel from hello on-premises VPN device.</span></span> <span data-ttu-id="c92f9-108">Se Olá problema persistir, siga estes passos tooidentify Olá causa problema Olá.</span><span class="sxs-lookup"><span data-stu-id="c92f9-108">If hello problem persists, follow these steps tooidentify hello cause of hello problem.</span></span>

### <a name="prerequisite-step"></a><span data-ttu-id="c92f9-109">Passo pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="c92f9-109">Prerequisite step</span></span>

<span data-ttu-id="c92f9-110">Verificação de tipo de Olá do gateway de VPN do Azure Olá.</span><span class="sxs-lookup"><span data-stu-id="c92f9-110">Check hello type of hello Azure VPN gateway.</span></span>

1. <span data-ttu-id="c92f9-111">Aceda toohello [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="c92f9-111">Go toohello [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="c92f9-112">Verifique Olá **descrição geral** página Olá de gateway de VPN para obter informações de tipo Olá.</span><span class="sxs-lookup"><span data-stu-id="c92f9-112">Check hello **Overview** page of hello VPN gateway for hello type information.</span></span>
    
    ![Descrição geral do gateway de Olá](media\vpn-gateway-troubleshoot-site-to-site-cannot-connect\gatewayoverview.png)

### <a name="step-1-check-whether-hello-on-premises-vpn-device-is-validated"></a><span data-ttu-id="c92f9-114">Passo 1.</span><span class="sxs-lookup"><span data-stu-id="c92f9-114">Step 1.</span></span> <span data-ttu-id="c92f9-115">Verifique se o dispositivo VPN no local Olá é validado</span><span class="sxs-lookup"><span data-stu-id="c92f9-115">Check whether hello on-premises VPN device is validated</span></span>

1. <span data-ttu-id="c92f9-116">Verifique se estão a utilizar um [validar o dispositivo VPN e versão do sistema operativo](vpn-gateway-about-vpn-devices.md#devicetable).</span><span class="sxs-lookup"><span data-stu-id="c92f9-116">Check whether you are using a [validated VPN device and operating system version](vpn-gateway-about-vpn-devices.md#devicetable).</span></span> <span data-ttu-id="c92f9-117">Se o dispositivo de Olá não é um dispositivo VPN validado, poderá ter toocontact Olá dispositivo fabricante toosee se houver um problema de compatibilidade.</span><span class="sxs-lookup"><span data-stu-id="c92f9-117">If hello device is not a validated VPN device, you might have toocontact hello device manufacturer toosee if there is a compatibility issue.</span></span>

2. <span data-ttu-id="c92f9-118">Certifique-se de que o dispositivo VPN Olá está configurado corretamente.</span><span class="sxs-lookup"><span data-stu-id="c92f9-118">Make sure that hello VPN device is correctly configured.</span></span> <span data-ttu-id="c92f9-119">Para obter mais informações, consulte [editar exemplos de configuração do dispositivo](/vpn-gateway-about-vpn-devices.md#editing).</span><span class="sxs-lookup"><span data-stu-id="c92f9-119">For more information, see [Edit device configuration samples](/vpn-gateway-about-vpn-devices.md#editing).</span></span>

### <a name="step-2-verify-hello-shared-key"></a><span data-ttu-id="c92f9-120">Passo 2.</span><span class="sxs-lookup"><span data-stu-id="c92f9-120">Step 2.</span></span> <span data-ttu-id="c92f9-121">Certifique-se a chave partilhada Olá</span><span class="sxs-lookup"><span data-stu-id="c92f9-121">Verify hello shared key</span></span>

<span data-ttu-id="c92f9-122">Compare a chave partilhada do Olá para Olá no local VPN dispositivo toohello VPN de rede Virtual do Azure toomake certificar-se de que as chaves de Olá correspondem.</span><span class="sxs-lookup"><span data-stu-id="c92f9-122">Compare hello shared key for hello on-premises VPN device toohello Azure Virtual Network VPN toomake sure that hello keys match.</span></span> 

<span data-ttu-id="c92f9-123">chave partilhada de Olá tooview para Olá ligação de VPN do Azure, utilize um dos seguintes métodos de Olá:</span><span class="sxs-lookup"><span data-stu-id="c92f9-123">tooview hello shared key for hello Azure VPN connection, use one of hello following methods:</span></span>

<span data-ttu-id="c92f9-124">**Portal do Azure**</span><span class="sxs-lookup"><span data-stu-id="c92f9-124">**Azure portal**</span></span>

1. <span data-ttu-id="c92f9-125">Aceda a ligação site a site de gateway VPN de toohello que criou.</span><span class="sxs-lookup"><span data-stu-id="c92f9-125">Go toohello VPN gateway site-to-site connection that you created.</span></span>

2. <span data-ttu-id="c92f9-126">No Olá **definições** secção, clique em **chave partilhada**.</span><span class="sxs-lookup"><span data-stu-id="c92f9-126">In hello **Settings** section, click **Shared key**.</span></span>
    
    ![Chave partilhada](media/vpn-gateway-troubleshoot-site-to-site-cannot-connect/sharedkey.png)

<span data-ttu-id="c92f9-128">**Azure PowerShell**</span><span class="sxs-lookup"><span data-stu-id="c92f9-128">**Azure PowerShell**</span></span>

<span data-ttu-id="c92f9-129">Para o modelo de implementação Azure Resource Manager Olá:</span><span class="sxs-lookup"><span data-stu-id="c92f9-129">For hello Azure Resource Manager deployment model:</span></span>

    Get-AzureRmVirtualNetworkGatewayConnectionSharedKey -Name <Connection name> -ResourceGroupName <Resource group name>

<span data-ttu-id="c92f9-130">Para o modelo de implementação clássica Olá:</span><span class="sxs-lookup"><span data-stu-id="c92f9-130">For hello classic deployment model:</span></span>

    Get-AzureVNetGatewayKey -VNetName -LocalNetworkSiteName

### <a name="step-3-verify-hello-vpn-peer-ips"></a><span data-ttu-id="c92f9-131">Passo 3.</span><span class="sxs-lookup"><span data-stu-id="c92f9-131">Step 3.</span></span> <span data-ttu-id="c92f9-132">Verificar o elemento de rede VPN Olá IPs</span><span class="sxs-lookup"><span data-stu-id="c92f9-132">Verify hello VPN peer IPs</span></span>

-   <span data-ttu-id="c92f9-133">Olá, definição de IP no Olá **Gateway de rede Local** objeto no Azure deve corresponder ao IP do dispositivo Olá no local.</span><span class="sxs-lookup"><span data-stu-id="c92f9-133">hello IP definition in hello **Local Network Gateway** object in Azure should match hello on-premises device IP.</span></span>
-   <span data-ttu-id="c92f9-134">Olá definição de IP do gateway do Azure que está definida no Olá no local dispositivo deve corresponder ao hello IP de gateway do Azure.</span><span class="sxs-lookup"><span data-stu-id="c92f9-134">hello Azure gateway IP definition that is set on hello on-premises device should match hello Azure gateway IP.</span></span>

### <a name="step-4-check-udr-and-nsgs-on-hello-gateway-subnet"></a><span data-ttu-id="c92f9-135">Passo 4.</span><span class="sxs-lookup"><span data-stu-id="c92f9-135">Step 4.</span></span> <span data-ttu-id="c92f9-136">Certifique-se UDR e NSGs na sub-rede de gateway Olá</span><span class="sxs-lookup"><span data-stu-id="c92f9-136">Check UDR and NSGs on hello gateway subnet</span></span>

<span data-ttu-id="c92f9-137">Procurar e remover encaminhamento definido pelo utilizador (UDR) ou grupos de segurança de rede (NSGs) na sub-rede de gateway Olá e, em seguida, testar o resultado de Olá.</span><span class="sxs-lookup"><span data-stu-id="c92f9-137">Check for and remove user-defined routing (UDR) or Network Security Groups (NSGs) on hello gateway subnet, and then test hello result.</span></span> <span data-ttu-id="c92f9-138">Se o problema de Olá for resolvido, Valide as definições de Olá UDR ou NSG aplicado.</span><span class="sxs-lookup"><span data-stu-id="c92f9-138">If hello problem is resolved, validate hello settings that UDR or NSG applied.</span></span>

### <a name="step-5-check-hello-on-premises-vpn-device-external-interface-address"></a><span data-ttu-id="c92f9-139">Passo 5.</span><span class="sxs-lookup"><span data-stu-id="c92f9-139">Step 5.</span></span> <span data-ttu-id="c92f9-140">Verifique o endereço de interface externa do dispositivo VPN do Olá no local</span><span class="sxs-lookup"><span data-stu-id="c92f9-140">Check hello on-premises VPN device external interface address</span></span>

- <span data-ttu-id="c92f9-141">Se Olá endereço IP para a Internet do dispositivo VPN de Olá está incluído no Olá **rede Local** definição no Azure, podem ocorrer esporádicas interrupções de ligação.</span><span class="sxs-lookup"><span data-stu-id="c92f9-141">If hello Internet-facing IP address of hello VPN device is included in hello **Local network** definition in Azure, you might experience sporadic disconnections.</span></span>
- <span data-ttu-id="c92f9-142">Olá interface externa do dispositivo tem de ser diretamente no Olá Internet.</span><span class="sxs-lookup"><span data-stu-id="c92f9-142">hello device's external interface must be directly on hello Internet.</span></span> <span data-ttu-id="c92f9-143">Não deverá haver nenhum tradução de endereços de rede ou firewall entre Olá Internet e o dispositivo de Olá.</span><span class="sxs-lookup"><span data-stu-id="c92f9-143">There should be no network address translation or firewall between hello Internet and hello device.</span></span>
- <span data-ttu-id="c92f9-144">tooconfigure toohave clustering um IP virtual de firewall, terá de interromper a cluster Olá e expor o dispositivo de VPN Olá diretamente interface pública tooa desse gateway Olá pode interagir com o.</span><span class="sxs-lookup"><span data-stu-id="c92f9-144">tooconfigure firewall clustering toohave a virtual IP, you must break hello cluster and expose hello VPN appliance directly tooa public interface that hello gateway can interface with.</span></span>

### <a name="step-6-verify-that-hello-subnets-match-exactly-azure-policy-based-gateways"></a><span data-ttu-id="c92f9-145">Passo 6.</span><span class="sxs-lookup"><span data-stu-id="c92f9-145">Step 6.</span></span> <span data-ttu-id="c92f9-146">Certifique-se de que as sub-redes de Olá coincidem (gateways de baseado na política do Azure)</span><span class="sxs-lookup"><span data-stu-id="c92f9-146">Verify that hello subnets match exactly (Azure policy-based gateways)</span></span>

-   <span data-ttu-id="c92f9-147">Certifique-se de que as sub-redes de Olá correspondem exatamente entre Olá rede virtual do Azure e definições no local para Olá rede virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="c92f9-147">Verify that hello subnets match exactly between hello Azure virtual network and on-premises definitions for hello Azure virtual network.</span></span>
-   <span data-ttu-id="c92f9-148">Certifique-se de que as sub-redes de Olá correspondem exatamente entre Olá **Gateway de rede Local** e definições de rede no local de Olá no local.</span><span class="sxs-lookup"><span data-stu-id="c92f9-148">Verify that hello subnets match exactly between hello **Local Network Gateway** and on-premises definitions for hello on-premises network.</span></span>

### <a name="step-7-verify-hello-azure-gateway-health-probe"></a><span data-ttu-id="c92f9-149">Passo 7.</span><span class="sxs-lookup"><span data-stu-id="c92f9-149">Step 7.</span></span> <span data-ttu-id="c92f9-150">Certifique-se de sonda de estado de funcionamento do Olá gateway do Azure</span><span class="sxs-lookup"><span data-stu-id="c92f9-150">Verify hello Azure gateway health probe</span></span>

1. <span data-ttu-id="c92f9-151">Aceda toohello [sonda do Estado de funcionamento](https://&lt;YourVirtualNetworkGatewayIP&gt;:8081/healthprobe).</span><span class="sxs-lookup"><span data-stu-id="c92f9-151">Go toohello [health probe](https://&lt;YourVirtualNetworkGatewayIP&gt;:8081/healthprobe).</span></span>

2. <span data-ttu-id="c92f9-152">Clique em através de aviso de certificado Olá.</span><span class="sxs-lookup"><span data-stu-id="c92f9-152">Click through hello certificate warning.</span></span>
3. <span data-ttu-id="c92f9-153">Se receber uma resposta, o gateway de VPN Olá é considerado em bom estado.</span><span class="sxs-lookup"><span data-stu-id="c92f9-153">If you receive a response, hello VPN gateway is considered healthy.</span></span> <span data-ttu-id="c92f9-154">Se não receber uma resposta, gateway Olá poderão não estar em bom estado de funcionamento ou um NSG na sub-rede de gateway Olá está a causar o problema de Olá.</span><span class="sxs-lookup"><span data-stu-id="c92f9-154">If you don't receive a response, hello gateway might not be healthy or an NSG on hello gateway subnet is causing hello problem.</span></span> <span data-ttu-id="c92f9-155">Olá seguir o texto é uma resposta de exemplo:</span><span class="sxs-lookup"><span data-stu-id="c92f9-155">hello following text is a sample response:</span></span>

    <span data-ttu-id="c92f9-156">&lt;? a versão de xml = "1.0"? > <string xmlns="http://schemas.microsoft.com/2003/10/Serialization/">instância primário: GatewayTenantWorker_IN_1 GatewayTenantVersion: 14.7.24.6 < / cadeia&gt;</span><span class="sxs-lookup"><span data-stu-id="c92f9-156">&lt;?xml version="1.0"?>  <string xmlns="http://schemas.microsoft.com/2003/10/Serialization/">Primary Instance: GatewayTenantWorker_IN_1 GatewayTenantVersion: 14.7.24.6</string&gt;</span></span>

### <a name="step-8-check-whether-hello-on-premises-vpn-device-has-hello-perfect-forward-secrecy-feature-enabled"></a><span data-ttu-id="c92f9-157">Passo 8.</span><span class="sxs-lookup"><span data-stu-id="c92f9-157">Step 8.</span></span> <span data-ttu-id="c92f9-158">Verifique se Olá no local dispositivo VPN tem ativada a funcionalidade Olá perfeita secrecy reencaminhar</span><span class="sxs-lookup"><span data-stu-id="c92f9-158">Check whether hello on-premises VPN device has hello perfect forward secrecy feature enabled</span></span>

<span data-ttu-id="c92f9-159">funcionalidade de perfeita secrecy reencaminhar Olá pode causar problemas de interrupção de ligação.</span><span class="sxs-lookup"><span data-stu-id="c92f9-159">hello perfect forward secrecy feature can cause disconnection problems.</span></span> <span data-ttu-id="c92f9-160">Se o dispositivo VPN Olá tiver perfeita secrecy reencaminhar ativada, desative a funcionalidade de Olá.</span><span class="sxs-lookup"><span data-stu-id="c92f9-160">If hello VPN device has perfect forward secrecy enabled, disable hello feature.</span></span> <span data-ttu-id="c92f9-161">Em seguida, atualize a política de IPsec do gateway VPN Olá.</span><span class="sxs-lookup"><span data-stu-id="c92f9-161">Then update hello VPN gateway IPsec policy.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c92f9-162">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="c92f9-162">Next steps</span></span>

-   [<span data-ttu-id="c92f9-163">Configurar uma rede virtual de tooa ligação site a site</span><span class="sxs-lookup"><span data-stu-id="c92f9-163">Configure a site-to-site connection tooa virtual network</span></span>](vpn-gateway-howto-site-to-site-resource-manager-portal.md)
-   [<span data-ttu-id="c92f9-164">Configurar uma política de IPsec/IKE para ligações de VPN de site a site</span><span class="sxs-lookup"><span data-stu-id="c92f9-164">Configure an IPsec/IKE policy for site-to-site VPN connections</span></span>](vpn-gateway-ipsecikepolicy-rm-powershell.md)
