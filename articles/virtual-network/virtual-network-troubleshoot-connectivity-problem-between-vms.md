---
title: problemas de conectividade aaaTroubleshooting entre as VMs do Azure | Microsoft Docs
description: "Saiba como tooTroubleshoot Olá problemas de conectividade entre as VMs do Azure."
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
ms.date: 08/25/2017
ms.author: genli
ms.openlocfilehash: ee0819178dcbee2bf529a495758e6c33f49e085e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-connectivity-problems-between-azure-vms"></a>Resolução de problemas de conectividade entre as VMs do Azure

Podem ocorrer problemas de conectividade entre as VMs do Azure. Este artigo fornece a resolução de problemas de passos toohelp resolver este problema. 

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="symptom"></a>Sintoma

VM do Azure não consegue ligar tooanother VM do Azure.

## <a name="troubleshooting-guidance"></a>Orientação na resolução de problemas 

1. [Verifique se a NIC está configurada incorretamente](#step-1-check-if-nic-is-misconfigured)
2. [Verifique se o tráfego de rede é bloqueado por NSG ou UDR](#step-2-check-if-network-traffic-is-blocked-by-nsg-or-udr)
3. [Verifique se o tráfego de rede é bloqueado pela firewall da VM](#step-3-check-if-network-traffic-is-blocked-by-vm-firewall)
4. [Verifique se VM aplicação ou serviço está a escutar na porta Olá](#step-4-check-whether-vm-app-or-service-is-listening-on-the-port)
5. [Verifique se o problema de Olá é causado por realizar o SNAT](#step-5-check-whether-the-problem-is-caused-by-snat)
6. [Verifique se o tráfego está bloqueado por ACLs para Olá VMS clássicas](#step-6-check-whether-traffic-is-blocked-by-acls-for-the-classic-vm)
7. [Verifique se o ponto final de Olá é criado para Olá VMS clássicas](#step-7-check-whether-the-endpoint-is-created-for-the-classic-vm)
8. [Não é possível tooconnect tooa partilha de rede VM](#step-8-unable-to-connect-to-a-vm-network-share)
9. [Conectividade inter-Vnet](#step-9-inter-vnet-connectivity)

## <a name="troubleshooting-steps"></a>Passos de resolução de problemas

Siga estes problema de Olá tootroubleshoot passos. Verifique se o problema de Olá resolvido depois de cada passo. 

### <a name="step-1-check-if-nic-is-misconfigured"></a>Passo 1: Verificar se a NIC está configurada incorretamente

Siga [como tooreset interface de rede para a VM do Windows Azure](../virtual-machines/windows/reset-network-interface.md). 

Se o problema de Olá ocorrer depois de modificar a interface de rede Olá (NIC), siga estes passos:

**VMs de Mulit NIC**

1. Adicionar uma NIC.
2. Corrigir problemas de Olá no Olá incorreto NIC ou remover incorreto NIC.  Em seguida, readd Olá NIC.

Para obter mais informações, consulte [tooor de interfaces de rede de adicionar, remover máquinas virtuais](virtual-network-network-interface-vm.md).

**VM NIC único** 

- [Reimplementar a VM do Windows](../virtual-machines/windows/redeploy-to-new-node.md)
- [Reimplementar a VM com Linux](../virtual-machines/linux/redeploy-to-new-node.md)

### <a name="step-2-check-if-network-traffic-is-blocked-by-nsg-or-udr"></a>Passo 2: Verificar se o tráfego de rede é bloqueado por NSG ou UDR

Utilizar [verificar do fluxo de rede do observador do IP](../network-watcher/network-watcher-ip-flow-verify-overview.md) e [NSG fluxo registo](../network-watcher/network-watcher-nsg-flow-logging-overview.md) tooidentify se existir um grupo de segurança de rede ou as rotas definidas pelo utilizador que está a interferir com o fluxo de tráfego.

### <a name="step-3-check-if-network-traffic-is-blocked-by-vm-firewall"></a>Passo 3: Verificar se o tráfego de rede é bloqueado pela firewall da VM

Desative a firewall Olá e, em seguida, testar o resultado de Olá. Se o problema de Olá for resolvido, validar as definições de Olá na firewall de Olá e volte a ativar.

### <a name="step-4-check-whether-vm-app-or-service-is-listening-on-hello-port"></a>Passo 4: Verificar se VM aplicação ou serviço está a escutar na porta Olá

Pode utilizar um Olá os seguintes métodos toocheck se VM aplicação ou serviço está a escutar na porta Olá

- Olá execute os seguintes comandos toocheck se Olá servidor está a escutar nessa porta.

**VM do Windows**

    netstat –ano

**VM do Linux**

    netstat -l

- Executar Olá **Telnet** comando no Olá porta do VM tooitself tootest Olá. Se Olá teste falhar, aplicação ou serviço não é toolisten configurado na porta Olá.

### <a name="step-5-check-whether-hello-problem-is-caused-by-snat"></a>Passo 5: Verificar se o problema de Olá é causado por realizar o SNAT

Em alguns cenários, hello VM é colocada atrás de uma solução de balanceamento de carga que tem uma dependência de recursos fora do Azure. Nestes cenários, se surgirem problemas de ligação intermitente, Olá problema poderá ser causado pelo [esgotamento de porta de realizar o SNAT](../load-balancer/load-balancer-outbound-connections.md). problema de Olá tooresolve, criar um VIP (ou ILPIP para clássico) para cada VM que está por trás do Balanceador de carga Olá e proteger com o NSG ou ACL. 

### <a name="step-6-check-whether-traffic-is-blocked-by-acls-for-hello-classic-vm"></a>Passo 6: Verifique se o tráfego está bloqueado por ACLs para Olá VMS clássicas

Uma ACL fornece Olá capacidade tooselectively permitir ou negar o tráfego para um ponto final da máquina virtual. Para obter mais informações, consulte [gerir Olá ACL num ponto final](../virtual-machines/windows/classic/setup-endpoints.md#manage-the-acl-on-an-endpoint).

### <a name="step-7-check-whether-hello-endpoint-is-created-for-hello-classic-vm"></a>Passo 7: Verifique se o ponto final de Olá é criado para Olá VMS clássicas

Todas as VMs que criar no Azure utilizando o modelo de implementação clássica Olá automaticamente comunicar através de um canal de rede privada com outras máquinas virtuais na Olá que mesma rede virtual ou serviço da nuvem. No entanto, os computadores em outras redes virtuais requerem pontos finais toodirect Olá rede entrada tráfego tooa máquina virtual. Para obter mais informações, consulte [como tooset dos pontos finais](../virtual-machines/windows/classic/setup-endpoints.md).

### <a name="step-8-unable-tooconnect-tooa-vm-network-share"></a>Passo 8: Partilha de rede VM não é possível tooconnect tooa

Se não é possível tooconnect tooa partilha de rede VM, problema Olá pode dever-se indisponível NICs em Olá VM. toodelete Olá NICs indisponíveis, consulte [como toodelete Olá NICs indisponíveis](../virtual-machines/windows/reset-network-interface.md#delete-the-unavailable-nics)

### <a name="step-9-inter-vnet-connectivity"></a>Passo 9: Inter-vnet conectividade

Utilizar [verificar do fluxo de rede do observador do IP](../network-watcher/network-watcher-ip-flow-verify-overview.md) e [NSG fluxo registo](../network-watcher/network-watcher-nsg-flow-logging-overview.md) tooidentify se existir um grupo de segurança de rede ou as rotas definidas pelo utilizador que está a interferir com o fluxo de tráfego. Também pode validar a configuração do Inter-Vnet [aqui](https://support.microsoft.com/en-us/help/4032151/configuring-and-validating-vnet-or-vpn-connections).

### <a name="need-help-contact-support"></a>Precisa de ajuda? Contacte o suporte.
Se ainda precisar de ajuda, [contacte o suporte](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget seu problema resolvido rapidamente.
