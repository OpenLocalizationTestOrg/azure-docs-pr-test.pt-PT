---
title: "problemas de aaaConnectivity e redes de FAQ de serviços do Microsoft Azure nuvem | Microsoft Docs"
description: "Este artigo apresenta uma lista de Olá perguntas mais frequentes sobre a conectividade e de rede para serviços de nuvem do Microsoft Azure."
services: cloud-services
documentationcenter: 
author: genlin
manager: cshepard
editor: 
tags: top-support-issue
ms.assetid: 84985660-2cfd-483a-8378-50eef6a0151d
ms.service: cloud-services
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/10/2017
ms.author: genli
ms.openlocfilehash: e725dbbf585a76807362c59299d0a31f511afd3d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="connectivity-and-networking-issues-for-azure-cloud-services-frequently-asked-questions-faqs"></a>Problemas de conectividade e de rede do Cloud Services do Azure: Perguntas mais frequentes sobre (FAQ)

Este artigo inclui perguntas mais frequentes sobre problemas de conectividade e de rede para [dos serviços de nuvem do Microsoft Azure](https://azure.microsoft.com/services/cloud-services). Também pode consultar Olá [página de tamanho de VM de serviços em nuvem](cloud-services-sizes-specs.md) para obter informações de tamanho.

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="i-cant-reserve-an-ip-in-a-multi-vip-cloud-service"></a>Posso não é possível reservar um IP num serviço de nuvem a várias VIP
Em primeiro lugar, certifique-se de que instância de máquina virtual de Olá que está a tentar tooreserve Olá IP está ativada. Segundo, certifique-se de que está a utilizar IPs reservados para ambos Olá implementações de teste e produção. **Não** alterar as definições de Olá, ao atualizar de implementação de Olá.

## <a name="how-do-i-remote-desktop-when-i-have-an-nsg"></a>Como posso ambiente de trabalho remoto quando tiver um NSG?
Adicionar toohello de regras NSG que permitam o tráfego em portas **3389** e **20000**.  Ambiente de trabalho remoto utiliza a porta **3389**.  Instâncias de serviço de nuvem são carga balanceada, pelo diretamente não é possível controlar qual tooconnect de instância para.  Olá *RemoteForwarder* e *RemoteAccess* agentes gerir o tráfego RDP e permitir Olá cliente toosend um cookie RDP e tooconnect uma instância individual para.  Olá *RemoteForwarder* e *RemoteAccess* agentes requerem essa porta **20000** ser aberto, que pode ser bloqueado se tiver um NSG.

## <a name="can-i-ping-a-cloud-service"></a>Posso ping um serviço em nuvem?

Não, não através da utilização normal Olá "ping" / protocolo ICMP. Olá protocolo ICMP não é permitido através do Balanceador de carga do Azure de Olá.

conectividade tootest, recomendamos que efetue um ping de porta. Enquanto Ping.exe utiliza o ICMP, outras ferramentas, como o PSPing, Nmap e telnet permitem-lhe tootest conectividade tooa específica a porta TCP.

Para obter mais informações, consulte [utilizar pings porta em vez de ICMP tootest conectividade de VM do Azure](https://blogs.msdn.microsoft.com/mast/2014/06/22/use-port-pings-instead-of-icmp-to-test-azure-vm-connectivity/).

## <a name="how-do-i-prevent-receiving-thousands-of-hits-from-unknown-ip-addresses-that-indicate-some-sort-of-malicious-attack-toohello-cloud-service"></a>Como impedir a receção milhares de pedidos de endereços IP desconhecidos que indiquem algum tipo de ataque malicioso toohello serviço em nuvem?
Azure implementa um tooprotect de segurança de rede multicamada respetivos serviços de plataforma contra ataques em distribuída denial of service (DDoS distribuídos). Olá sistema de defesa Azure DDoS faz parte monitorização processo contínuo do Azure, que é continuamente melhorado através de penetração de teste. Este sistema de defesa DDoS foi concebido toowithstand não só a ataques de Olá fora, mas também a partir de outros inquilinos do Azure. Para obter mais detalhes, consulte [segurança de rede do Microsoft Azure](http://download.microsoft.com/download/C/A/3/CA3FC5C0-ECE0-4F87-BF4B-D74064A00846/AzureNetworkSecurity_v3_Feb2015.pdf).

Também pode criar um bloco de tooselectively de tarefa de arranque alguns endereços IP específicos. Para obter mais informações, consulte [bloquear um endereço IP específico](cloud-services-startup-tasks-common.md#block-a-specific-ip-address).

## <a name="when-i-try-toordp-toomy-cloud-service-instance-i-get-hello-message-hello-user-account-has-expired"></a>Ao tentar tooRDP toomy instância de serviço em nuvem, é apresentada a mensagem de Olá, "conta de utilizador Olá expirou."
Pode obter a mensagem de erro de Olá "Esta conta de utilizador expirou" quando a ignorar a data de expiração de Olá que está configurada nas definições do RDP. Pode alterar data de expiração de Olá a partir do portal de Olá seguindo estes passos:
1. Inicie sessão no toohello consola de gestão do Azure (https://manage.windowsazure.com), navegue até o serviço em nuvem tooyour e selecione Olá **configurar** separador.
2. Selecione **remoto**.
3. Alterar Olá "Expira em" data e, em seguida, guarde a configuração de Olá.

Agora deve ser capaz de tooRDP tooyour máquina.

## <a name="why-is-loadbalancer-not-balancing-traffic-equally"></a>Por que motivo é LoadBalancer não balanceamento tráfego equitativamente?
Para obter informações sobre como interna funciona de Balanceador de carga, consulte [novo modo de distribuição do Balanceador de carga do Azure](https://azure.microsoft.com/blog/azure-load-balancer-new-distribution-mode/).

algoritmo de distribuição de Olá utilizado é uma 5 cadeias de identificação (IP, porta de origem, de origem destino IP, porta de destino, protocolo tipo) servidores de tooavailable toomap tráfego de hash. Fornece retenções apenas dentro de uma sessão de transporte. Pacotes hello a sessão TCP ou UDP mesmo será direcionado toohello instância mesmo datacenter IP (DIP) por trás do ponto final do Olá com balanceamento de carga. Quando o cliente Olá fecha e abra novamente a ligação de Olá ou inicia uma nova sessão de Olá mesmo IP de origem, porta de origem Olá alterações e faz com que Olá tráfego toogo tooa DIP pontos finais diferentes.
