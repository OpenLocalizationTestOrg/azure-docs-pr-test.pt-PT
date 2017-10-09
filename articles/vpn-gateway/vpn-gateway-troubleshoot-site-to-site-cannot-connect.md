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
# <a name="troubleshooting-an-azure-site-to-site-vpn-connection-cannot-connect-and-stops-working"></a>Resolução de problemas: Uma ligação de VPN de site para site do Azure não é possível ligar e deixa de funcionar

Depois de configurar uma ligação de VPN de site a site entre uma rede no local e uma Azure virtual network, Olá ligação VPN deixa de funcionar e não pode ser novamente ligado. Este artigo fornece a resolução de problemas de passos toohelp resolver este problema. 

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="troubleshooting-steps"></a>Passos de resolução de problemas

problema de Olá tooresolve, tente primeiro demasiado[reposição Olá VPN gateway do Azure](vpn-gateway-resetgw-classic.md) e repor o túnel Olá dispositivo de VPN no local Olá. Se Olá problema persistir, siga estes passos tooidentify Olá causa problema Olá.

### <a name="prerequisite-step"></a>Passo pré-requisitos

Verificação de tipo de Olá do gateway de VPN do Azure Olá.

1. Aceda toohello [portal do Azure](https://portal.azure.com).

2. Verifique Olá **descrição geral** página Olá de gateway de VPN para obter informações de tipo Olá.
    
    ![Descrição geral do gateway de Olá](media\vpn-gateway-troubleshoot-site-to-site-cannot-connect\gatewayoverview.png)

### <a name="step-1-check-whether-hello-on-premises-vpn-device-is-validated"></a>Passo 1. Verifique se o dispositivo VPN no local Olá é validado

1. Verifique se estão a utilizar um [validar o dispositivo VPN e versão do sistema operativo](vpn-gateway-about-vpn-devices.md#devicetable). Se o dispositivo de Olá não é um dispositivo VPN validado, poderá ter toocontact Olá dispositivo fabricante toosee se houver um problema de compatibilidade.

2. Certifique-se de que o dispositivo VPN Olá está configurado corretamente. Para obter mais informações, consulte [editar exemplos de configuração do dispositivo](/vpn-gateway-about-vpn-devices.md#editing).

### <a name="step-2-verify-hello-shared-key"></a>Passo 2. Certifique-se a chave partilhada Olá

Compare a chave partilhada do Olá para Olá no local VPN dispositivo toohello VPN de rede Virtual do Azure toomake certificar-se de que as chaves de Olá correspondem. 

chave partilhada de Olá tooview para Olá ligação de VPN do Azure, utilize um dos seguintes métodos de Olá:

**Portal do Azure**

1. Aceda a ligação site a site de gateway VPN de toohello que criou.

2. No Olá **definições** secção, clique em **chave partilhada**.
    
    ![Chave partilhada](media/vpn-gateway-troubleshoot-site-to-site-cannot-connect/sharedkey.png)

**Azure PowerShell**

Para o modelo de implementação Azure Resource Manager Olá:

    Get-AzureRmVirtualNetworkGatewayConnectionSharedKey -Name <Connection name> -ResourceGroupName <Resource group name>

Para o modelo de implementação clássica Olá:

    Get-AzureVNetGatewayKey -VNetName -LocalNetworkSiteName

### <a name="step-3-verify-hello-vpn-peer-ips"></a>Passo 3. Verificar o elemento de rede VPN Olá IPs

-   Olá, definição de IP no Olá **Gateway de rede Local** objeto no Azure deve corresponder ao IP do dispositivo Olá no local.
-   Olá definição de IP do gateway do Azure que está definida no Olá no local dispositivo deve corresponder ao hello IP de gateway do Azure.

### <a name="step-4-check-udr-and-nsgs-on-hello-gateway-subnet"></a>Passo 4. Certifique-se UDR e NSGs na sub-rede de gateway Olá

Procurar e remover encaminhamento definido pelo utilizador (UDR) ou grupos de segurança de rede (NSGs) na sub-rede de gateway Olá e, em seguida, testar o resultado de Olá. Se o problema de Olá for resolvido, Valide as definições de Olá UDR ou NSG aplicado.

### <a name="step-5-check-hello-on-premises-vpn-device-external-interface-address"></a>Passo 5. Verifique o endereço de interface externa do dispositivo VPN do Olá no local

- Se Olá endereço IP para a Internet do dispositivo VPN de Olá está incluído no Olá **rede Local** definição no Azure, podem ocorrer esporádicas interrupções de ligação.
- Olá interface externa do dispositivo tem de ser diretamente no Olá Internet. Não deverá haver nenhum tradução de endereços de rede ou firewall entre Olá Internet e o dispositivo de Olá.
- tooconfigure toohave clustering um IP virtual de firewall, terá de interromper a cluster Olá e expor o dispositivo de VPN Olá diretamente interface pública tooa desse gateway Olá pode interagir com o.

### <a name="step-6-verify-that-hello-subnets-match-exactly-azure-policy-based-gateways"></a>Passo 6. Certifique-se de que as sub-redes de Olá coincidem (gateways de baseado na política do Azure)

-   Certifique-se de que as sub-redes de Olá correspondem exatamente entre Olá rede virtual do Azure e definições no local para Olá rede virtual do Azure.
-   Certifique-se de que as sub-redes de Olá correspondem exatamente entre Olá **Gateway de rede Local** e definições de rede no local de Olá no local.

### <a name="step-7-verify-hello-azure-gateway-health-probe"></a>Passo 7. Certifique-se de sonda de estado de funcionamento do Olá gateway do Azure

1. Aceda toohello [sonda do Estado de funcionamento](https://&lt;YourVirtualNetworkGatewayIP&gt;:8081/healthprobe).

2. Clique em através de aviso de certificado Olá.
3. Se receber uma resposta, o gateway de VPN Olá é considerado em bom estado. Se não receber uma resposta, gateway Olá poderão não estar em bom estado de funcionamento ou um NSG na sub-rede de gateway Olá está a causar o problema de Olá. Olá seguir o texto é uma resposta de exemplo:

    &lt;? a versão de xml = "1.0"? > <string xmlns="http://schemas.microsoft.com/2003/10/Serialization/">instância primário: GatewayTenantWorker_IN_1 GatewayTenantVersion: 14.7.24.6 < / cadeia&gt;

### <a name="step-8-check-whether-hello-on-premises-vpn-device-has-hello-perfect-forward-secrecy-feature-enabled"></a>Passo 8. Verifique se Olá no local dispositivo VPN tem ativada a funcionalidade Olá perfeita secrecy reencaminhar

funcionalidade de perfeita secrecy reencaminhar Olá pode causar problemas de interrupção de ligação. Se o dispositivo VPN Olá tiver perfeita secrecy reencaminhar ativada, desative a funcionalidade de Olá. Em seguida, atualize a política de IPsec do gateway VPN Olá.

## <a name="next-steps"></a>Passos seguintes

-   [Configurar uma rede virtual de tooa ligação site a site](vpn-gateway-howto-site-to-site-resource-manager-portal.md)
-   [Configurar uma política de IPsec/IKE para ligações de VPN de site a site](vpn-gateway-ipsecikepolicy-rm-powershell.md)
