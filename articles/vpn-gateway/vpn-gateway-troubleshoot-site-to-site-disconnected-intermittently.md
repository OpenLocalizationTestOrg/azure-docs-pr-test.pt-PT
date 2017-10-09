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
# <a name="troubleshooting-azure-site-to-site-vpn-disconnects-intermittently"></a>Resolução de problemas: VPN de Site para Site do Azure desliga ligados intermitentemente

Podem ocorrer problemas de Olá que uma ligação de VPN do Microsoft Azure ponto a Site nova ou existente não está estável ou desliga regularmente. Este artigo fornece os passos toohelp identificar e resolver o problema de Olá causa Olá de resolução de problemas. 

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="troubleshooting-steps"></a>Passos de resolução de problemas

### <a name="prerequisite-step"></a>Passo pré-requisitos

Verifique o tipo de Olá do gateway de rede virtual do Azure:

1. Aceda demasiado[portal do Azure](https://portal.azure.com).
2. Verifique Olá **descrição geral** página Olá virtuais do gateway de rede para obter informações de tipo Olá.
    
    ![Descrição geral de Olá do gateway de Olá](media\vpn-gateway-troubleshoot-site-to-site-disconnected-intermittently\gatewayoverview.png)

### <a name="step-1-check-whether-hello-on-premises-vpn-device-is-validated"></a>Passo 1 Verifique se Olá no local o dispositivo VPN é validado

1. Verifique se estão a utilizar um [validar o dispositivo VPN e versão do sistema operativo](vpn-gateway-about-vpn-devices.md#devicetable). Se o dispositivo VPN Olá não é validado, poderá ter toocontact Olá dispositivo fabricante toosee se existir qualquer problema de compatibilidade.
2. Certifique-se de que o dispositivo VPN Olá está configurado corretamente. Para obter mais informações, consulte [editar exemplos de configuração do dispositivo](vpn-gateway-about-vpn-devices.md#editing).

### <a name="step-2-check-hello-security-association-settingsfor-policy-based-azure-virtual-network-gateways"></a>Definições de associação de segurança do passo 2 verificação Olá (para gateways de rede virtual do Azure baseada em políticas)

1. Certifique-se nessa rede virtual Olá, sub-redes e intervalos de na Olá **gateway de rede Local** definição no Microsoft Azure são o mesmo que a configuração de Olá no dispositivo VPN do Olá no local.
2. Certifique-se de que corresponda de definições de associação de segurança de Olá.

### <a name="step-3-check-for-user-defined-routes-or-network-security-groups-on-gateway-subnet"></a>Passo 3 procurar rotas definidas pelo utilizador ou grupos de segurança de rede na sub-rede de Gateway

Uma rota definida pelo utilizador na sub-rede de gateway Olá pode ser restringir algum tráfego e permitindo que o tráfego restante. Isto faz com que são apresentados se a ligação de VPN de Olá está pouco fiáveis para algum tráfego e ideais para outras pessoas. 

### <a name="step-4-check-hello-one-vpn-tunnel-per-subnet-pair-setting-for-policy-based-virtual-network-gateways"></a>Passo 4 verificação Olá "um túnel VPN por par sub-rede" definição (para gateways de rede virtual baseada em políticas)

Certifique-se de que Olá no local VPN está configurado toohave **um túnel VPN por par sub-rede** para gateways de rede virtual baseada em políticas.

### <a name="step-5-check-for-security-association-limitation-for-policy-based-virtual-network-gateways"></a>Passo 5 procurar limitação de associação de segurança (para gateways de rede virtual baseada em políticas)

gateway de rede virtual baseada em políticas Olá tem o limite de 200 pares de associação de segurança de sub-rede. Se o número de Olá de sub-redes de rede virtual do Azure multiplicado vezes por Olá número de sub-redes locais é superior a 200, ver sub-redes esporádicas desligar.

### <a name="step-6-check-on-premises-vpn-device-external-interface-address"></a>Passo 6 verificação no local o endereço de interface externa do dispositivo VPN

- Se hello Internet com o endereço IP do dispositivo VPN Olá está incluída no Olá **gateway de rede Local** definição no Azure, pode deparar-se esporádicas interrupções de ligação.
- Olá interface externa do dispositivo tem de ser diretamente no Olá Internet. Não deverá haver nenhum tradução de endereços de rede (NAT) ou firewall entre Olá Internet e o dispositivo de Olá.
-  Se configurar o Clustering de Firewall toohave um IP virtual, tem de interromper a cluster Olá e expor o dispositivo de VPN Olá diretamente tooa interface pública que Olá gateway pode interagir com.

### <a name="step-7-check-whether-hello-on-premises-vpn-device-has-perfect-forward-secrecy-enabled"></a>Passo 7 de verificação se Olá no local o dispositivo VPN tem Perfect Forward Secrecy ativada

Olá **Perfect Forward Secrecy** funcionalidade pode causar problemas de interrupção de ligação de Olá. Se tiver de dispositivo VPN Olá **perfeita Secrecy reencaminhar** ativada, desative a funcionalidade de Olá. Em seguida, [atualizar a política de IPsec do gateway de rede virtual Olá](vpn-gateway-ipsecikepolicy-rm-powershell.md#managepolicy).

## <a name="next-steps"></a>Passos seguintes

- [Configurar uma rede virtual do Site para Site ligação tooa](vpn-gateway-howto-site-to-site-resource-manager-portal.md)
- [Configurar a política de IPsec/IKE para ligações VPN de Site a Site](vpn-gateway-ipsecikepolicy-rm-powershell.md)

