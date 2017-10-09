---
title: "conectividade do On-Premises aaaDiagnose através do gateway VPN com o observador de rede do Azure | Microsoft Docs"
description: "Este artigo descreve como toodiagnose no conetividade em vários locais através do gateway VPN com a resolução de problemas de recursos do observador de rede do Azure."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: aeffbf3d-fd19-4d61-831d-a7114f7534f9
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 9941c5d1b49bec29062210684dae8653cbdb84b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="diagnose-on-premises-connectivity-via-vpn-gateways"></a>Diagnosticar conectividade no local através de gateways de VPN

Gateway de VPN do Azure permite-lhe solução híbrida toocreate que resolvem Olá necessidade de uma ligação segura entre a sua rede no local e a sua rede virtual do Azure. Como os requisitos são exclusivos, por isso é escolha Olá do dispositivo VPN no local. Azure suporta atualmente [vários dispositivos VPN](../vpn-gateway/vpn-gateway-about-vpn-devices.md#devicetable) que constantemente são validadas em parceria com fornecedores de dispositivos de Olá. Reveja as definições de configuração específicos do dispositivo Olá antes de configurar o dispositivo VPN no local. Da mesma forma, o Gateway de VPN do Azure está configurado com um conjunto de [IPsec parâmetros suportados](../vpn-gateway/vpn-gateway-about-vpn-devices.md#ipsec) que são utilizadas para estabelecer ligações. Atualmente não há nenhuma forma de toospecify ou selecione uma combinação de parâmetros de IPsec do Gateway de VPN do Azure de Olá específica. Para estabelecer uma ligação com êxito entre no local e o Azure, Olá no local as definições do dispositivo de VPN tem de estar em conformidade com os parâmetros de IPsec de Olá prescritos pelo Gateway de VPN do Azure. Se hello são as definições estão corretas, não existe uma perda de conectividade e até agora estes problemas de resolução de problemas não trivial e normalmente demorou horas tooidentify e corrija problema Olá.

Com Olá observador de rede de Azure funcionalidade de resolução de problemas, são toodiagnose capaz de quaisquer problemas com o seu Gateway e ligações e dentro de minutos tem suficiente toomake informações problema de Olá uma decisão informada toorectify.

## <a name="scenario"></a>Cenário

Pretender tooconfigure um site para site ligação entre o Azure e no local utilizando FortiGate conforme Olá no local do VPN Gateway. tooachieve neste cenário, seriam necessários Olá a seguinte configuração:

1. Gateway de rede virtual - Olá Gateway de VPN no Azure
1. Gateway de rede local - Olá [no local (FortiGate) VPN Gateway](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md#LocalNetworkGateway) representação na nuvem do Azure
1. Ligação de site a site (baseado em política) - [ligação entre Olá Gateway de VPN e Olá no local router](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md#createconnection)
1. [Configurar FortiGate](https://github.com/Azure/Azure-vpn-config-samples/blob/master/Fortinet/Current/Site-to-Site_VPN_using_FortiGate.md)

Pode encontrar orientação passo a passo detalhada para configurar uma configuração Site a Site, visitando: [criar uma VNet com uma ligação Site a Site utilizando o portal do Azure de Olá](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md).

Um dos passos de configuração críticas Olá está a configurar os parâmetros de comunicação de IPsec Olá, qualquer configuração incorreta que servem como tooloss de conectividade entre a rede no local de Olá e o Azure. Atualmente, os Gateways de VPN do Azure são Olá toosupport configurado os seguintes parâmetros IPsec para a fase 1. Tenha em atenção, tal como mencionado anteriormente, que estas definições não podem ser modificadas.  Como pode ver na tabela de Olá abaixo, algoritmos de encriptação de Olá suportados pelo Gateway de VPN do Azure são AES256, 3DES e AES-128.

### <a name="ike-phase-1-setup"></a>Configuração de fase 1 do IKE

| **Propriedade** | **PolicyBased** | **Gateway RouteBased e Standard ou VPN de elevado desempenho** |
| --- | --- | --- |
| Versão do IKE |IKEv1 |IKEv2 |
| Grupo Diffie-Hellman |Grupo 2 (1024 bits) |Grupo 2 (1024 bits) |
| Método de Autenticação |Chave Pré-partilhada |Chave Pré-partilhada |
| Algoritmos de Encriptação |AES256 AES128 3DES |AES256 3DES |
| Algoritmo Hash |SHA1(SHA128) |SHA1(SHA128), SHA2(SHA256) |
| Duração (Tempo) da Associação de Segurança (SA) da Fase 1 |28 800 segundos |10 800 segundos |

Como um utilizador, seria necessário tooconfigure sua FortiGate, uma configuração de exemplo pode ser encontrada no [GitHub](https://github.com/Azure/Azure-vpn-config-samples/blob/master/Fortinet/Current/fortigate_show%20full-configuration.txt). Inadvertidamente tiver configurado o toouse FortiGate SHA-512 como Olá algoritmo hash. Como este algoritmo não é um algoritmo suportado para ligações baseadas em políticas, funciona a ligação VPN.

Estes problemas são tootroubleshoot disco rígido e causas raiz são, muitas vezes, não intuitivos. Neste caso, pode abrir uma ajuda de tooget de pedido de suporte sobre como resolver o problema de Olá. Mas com o observador de rede de Azure API de resolução de problemas, pode identificar estes problemas no seu próprio.

## <a name="troubleshooting-using-azure-network-watcher"></a>Resolução de problemas com o observador de rede do Azure

toodiagnose a ligação, tooAzure PowerShell de ligar e iniciar Olá `Start-AzureRmNetworkWatcherResourceTroubleshooting` cmdlet. Pode encontrar detalhes Olá utilizando este cmdlet em [resolver problemas de Gateway de rede Virtual e ligações - PowerShell](network-watcher-troubleshoot-manage-powershell.md). Este cmdlet pode demorar até toofew minutos toocomplete.

Após a conclusão do cmdlet Olá, pode navegar toohello localização de armazenamento especificada no cmdlet Olá tooget informações detalhadas sobre sobre o problema de Olá e registos. Observador de rede do Azure cria uma pasta de zip que contém Olá os seguintes ficheiros de registo:

![1][1]

Ficheiro de Olá aberta denominado IKEErrors.txt e apresenta a seguinte Olá erro, que indica um problema com no local configuração incorreta de definição do IKE.

```
Error: On-premises device rejected Quick Mode settings. Check values.
     based on log : Peer sent NO_PROPOSAL_CHOSEN notify
```

Pode obter informações detalhadas do Olá Scrubbed wfpdiag.txt sobre o erro de Olá, tal como neste caso menciona que foi `ERROR_IPSEC_IKE_POLICY_MATCH` esse tooconnection de oportunidades potenciais não está a funcionar corretamente.

Configuração incorreta comum outra é Olá especificando incorretas chaves partilhadas. Em caso de Olá anterior exemplo tivesse especificado diferentes chaves partilhadas, Olá IKEErrors.txt mostra Olá seguinte erro: `Error: Authentication failed. Check shared key`.

Funcionalidade de resolução de problemas do observador de rede do Azure permite-lhe toodiagnose e resolver problemas do seu Gateway de VPN e a ligação com facilidade de Olá de um cmdlet do PowerShell simple. Atualmente, suportam Olá diagnosticar seguintes condições e estiver a trabalhar para adicionar mais condição.

### <a name="gateway"></a>Gateway

| Tipo de índice de falhas | Razão | Registar|
|---|---|---|
| NoFault | Quando não é detetado nenhum erro. |Sim|
| GatewayNotFound | Não é possível encontrar o Gateway ou Gateway não está aprovisionada. |Não|
| PlannedMaintenance |  Uma instância de gateway está em manutenção.  |Não|
| UserDrivenUpdate | Quando uma atualização de utilizador está em curso. Isto pode ser uma operação de redimensionamento. | Não |
| VipUnResponsive | Não é possível contactar a instância principal de Olá do Olá Gateway. Isto acontece quando ocorre uma falha de pesquisa de estado de funcionamento de Olá. | Não |
| PlatformInActive | Não há um problema com a plataforma de Olá. | Não|
| ServiceNotRunning | serviço subjacente Olá não está em execução. | Não|
| NoConnectionsFoundForGateway | Não existem ligações existe no gateway de Olá. Esta é apenas um aviso.| Não|
| ConnectionsNotConnected | Nenhuma das ligações de Olá estão ligadas. Esta é apenas um aviso.| Sim|
| GatewayCPUUsageExceeded | Olá Gateway a utilização atual de utilização da CPU é > 95%. | Sim |

### <a name="connection"></a>Ligação

| Tipo de índice de falhas | Razão | Registar|
|---|---|---|
| NoFault | Quando não é detetado nenhum erro. |Sim|
| GatewayNotFound | Não é possível encontrar o Gateway ou Gateway não está aprovisionada. |Não|
| PlannedMaintenance | Uma instância de gateway está em manutenção.  |Não|
| UserDrivenUpdate | Quando uma atualização de utilizador está em curso. Isto pode ser uma operação de redimensionamento.  | Não |
| VipUnResponsive | Não é possível contactar a instância principal de Olá do Olá Gateway. Ocorre quando ocorre uma falha de pesquisa de estado de funcionamento de Olá. | Não |
| ConnectionEntityNotFound | Configuração da ligação está em falta. | Não |
| ConnectionIsMarkedDisconnected | Olá ligação está marcada como "desligada". |Não|
| ConnectionNotConfiguredOnGateway | o serviço subjacente Olá não tem Olá que ligação configurada. | Sim |
| ConnectionMarkedStandy | Olá subjacente do serviço está marcada como modo de espera.| Sim|
| Autenticação | Erro de correspondência de chave pré-partilhada. | Sim|
| PeerReachability | gateway de ponto a ponto Olá não está acessível. | Sim|
| IkePolicyMismatch | gateway de ponto a ponto Olá tem políticas IKE que não são suportadas pelo Azure. | Sim|
| Erro de WfpParse | Erro ao registo WFP Olá análise. |Sim|

## <a name="next-steps"></a>Passos seguintes

Saiba toocheck conectividade de Gateway de VPN com o PowerShell e automatização do Azure, visitando [gateways de VPN do Monitor com a resolução de problemas do observador de rede do Azure](network-watcher-monitor-with-azure-automation.md)

[1]: ./media/network-watcher-diagnose-on-premises-connectivity/figure1.png
