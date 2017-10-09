---
title: aaaCannot eliminar uma rede virtual no Azure | Microsoft Docs
description: "Saiba como tootroubleshoot Olá problema em que não é possível eliminar uma rede virtual no Azure."
services: virtual-network
documentationcenter: na
author: chadmath
manager: cshepard
editor: 
tags: azure-resource-manager
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/17/2017
ms.author: genli
ms.openlocfilehash: a9050ab238ccb0380fd46130430222efb8f42388
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-failed-toodelete-a-virtual-network-in-azure"></a>Resolução de problemas: Falha toodelete uma rede virtual no Azure

Poderá receber erros quando tenta toodelete uma rede virtual no Microsoft Azure. Este artigo fornece a resolução de problemas de passos toohelp resolver este problema. 

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="troubleshooting-guidance"></a>Orientação na resolução de problemas 

1. [Verifique se um gateway de rede virtual está em execução na rede virtual Olá](#check-whether-a-virtual-network-gateway-is-running-in-the-virtual-network).
2. [Verifique se um gateway de aplicação está em execução na rede virtual Olá](#check-whether-an-application-gateway-is-running-in-the-virtual-network).
3. [Verifique se o serviço de domínio do Active Directory do Azure está ativado na rede virtual Olá](#check-whether-azure-active-directory-domain-service-is-enabled-in-the-virtual-network).
4. [Verifique se a rede virtual Olá está ligado tooother recursos](#check-whether-the-virtual-network-is-connected-to-other-resource).
5. [Verifique se uma máquina virtual ainda está em execução na rede virtual Olá](#check-whether-a-virtual-machine-is-still-running-in-the-virtual-network).
6. [Verifique se a rede virtual Olá está encravada no migração](#check-whether-the-virtual-network-is-stuck-in-migration).

## <a name="troubleshooting-steps"></a>Passos de resolução de problemas

### <a name="check-whether-a-virtual-network-gateway-is-running-in-hello-virtual-network"></a>Verifique se um gateway de rede virtual está em execução na rede virtual Olá

rede virtual do Olá tooremove, deverá remover primeiro o gateway de rede virtual Olá.

Para redes virtuais clássicas, visite toohello **descrição geral** página de rede virtual clássica Olá no Olá portal do Azure. No Olá **ligações VPN** secção, se o gateway de Olá está em execução na rede virtual Olá, verá Olá IP endereço de gateway Olá. 

![Verifique se o gateway está em execução](media/virtual-network-troubleshoot-cannot-delete-vnet/classic-gateway.png)

Para as redes virtuais, aceda toohello **descrição geral** página de rede virtual Olá. Verifique **dispositivos ligados** Olá virtual gateway de rede.

![Verifique o dispositivo ligado Olá](media/virtual-network-troubleshoot-cannot-delete-vnet/vnet-gateway.png)

Antes de poder remover gateway Olá, remova primeiro qualquer **ligação** objetos no gateway de Olá. 

### <a name="check-whether-an-application-gateway-is-running-in-hello-virtual-network"></a>Verifique se um gateway de aplicação está em execução na rede virtual Olá

Aceda toohello **descrição geral** página de rede virtual Olá. Verifique Olá **dispositivos ligados** Olá gateway de aplicação.

![Verifique o dispositivo ligado Olá](media/virtual-network-troubleshoot-cannot-delete-vnet/app-gateway.png)

Se existir um gateway de aplicação, tem de removê-lo antes de poder eliminar a rede virtual Olá.

### <a name="check-whether-azure-active-directory-domain-service-is-enabled-in-hello-virtual-network"></a>Verifique se o serviço de domínio do Active Directory do Azure está ativado na rede virtual Olá

Se Olá os serviços de domínio do Active Directory é ativado e ligado toohello rede virtual, não é possível eliminar esta rede virtual. 

![Verifique o dispositivo ligado Olá](media/virtual-network-troubleshoot-cannot-delete-vnet/enable-domain-services.png)

toodisable Olá serviço, siga estes passos:

1. Aceda toohello [portal clássico do Azure](https://manage.windowsazure.com).
2. No painel esquerdo Olá, selecione **do Active Directory**.
3. Selecione o diretório do Azure Active Directory (Azure AD) de Olá que tenha o serviço de domínio do Active Directory ativada.
4. Selecione Olá **configurar** separador.
5. Em **dos serviços de domínio**, alterar Olá **ativar os serviços de domínio para este diretório** opção demasiado**não**.  

### <a name="check-whether-hello-virtual-network-is-connected-tooother-resource"></a>Verifique se a rede virtual Olá está ligado tooother recursos

Verifique a existência de ligações de circuito, ligações e peerings de rede virtual. Qualquer uma destas unidades podem provocar um toofail de eliminação de rede virtual. 

Olá ordem de eliminação recomendada é o seguinte:

1. Ligações de gateway
2. Gateways
3. IPs
4. Peerings de rede virtual
5. Ambiente de serviço de aplicações (ASE)

### <a name="check-whether-a-virtual-machine-is-still-running-in-hello-virtual-network"></a>Verifique se uma máquina virtual ainda está em execução na rede virtual Olá

Certifique-se de que nenhuma máquina virtual na rede virtual Olá.

### <a name="check-whether-hello-virtual-network-is-stuck-in-migration"></a>Verifique se a rede virtual Olá está encravada no migração

Se a rede virtual Olá está encravada no estado de migração, não pode ser eliminada. Execute Olá migração de Olá tooabort de comando a seguir e, em seguida, elimine a rede virtual Olá.

    Move-AzureVirtualNetwork -VirtualNetworkName "Name" -Abort

## <a name="next-steps"></a>Passos seguintes

- [Rede Virtual do Azure](virtual-networks-overview.md)
- [Perguntas mais frequentes (FAQ) da Rede Virtual do Azure](virtual-networks-faq.md)