---
title: "verificação de tooconnectivity aaaIntroduction no observador de rede do Azure | Microsoft Docs"
description: "Esta página fornece uma descrição geral de Olá capacidade de conectividade do observador de rede"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/11/2017
ms.author: gwallace
ms.openlocfilehash: 52fc4547f167cea2992a046859dc0550d136e80d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooconnectivity-check-in-azure-network-watcher"></a>Introdução tooconnectivity registar observador de rede do Azure

Olá funcionalidade de conectividade do observador de rede fornece Olá capacidade toocheck uma ligação de TCP direta de uma máquina virtual tooa máquina virtual (VM), o nome de domínio completamente qualificado (FQDN), URI, ou o endereço IPv4. Cenários de rede são complexos, estão implementados utilizando grupos de segurança de rede, firewalls, rotas definidas pelo utilizador e de recursos fornecidos pelo Azure. Configurações complexas efetua a resolução de problemas de conectividade um desafio. Observador de rede ajuda a reduzir a quantidade de Olá de tempo toofind e detetar problemas de conectividade. resultados de Olá devolvidos podem fornecer informações se um problema de conectividade é devido a plataforma de tooa ou um problema de configuração do utilizador. Conectividade pode ser verificada com [PowerShell](network-watcher-connectivity-powershell.md), [CLI do Azure](network-watcher-connectivity-cli.md), e [REST API](network-watcher-connectivity-rest.md).

> [!IMPORTANT]
> Verificação da conectividade requer uma extensão da máquina virtual `AzureNetworkWatcherExtension`. Para instalar a extensão de Olá numa Windows VM visite [extensão da máquina virtual de agente de observador de rede do Azure para Windows](../virtual-machines/windows/extensions-nwa.md) e para, visite VM com Linux [extensão da máquina virtual de agente de observador de rede do Azure para Linux](../virtual-machines/linux/extensions-nwa.md).

## <a name="response"></a>Resposta

Olá, a tabela seguinte apresenta as propriedades de Olá devolvidas quando uma verificação de conectividade concluiu a execução.

|Propriedade  |Descrição  |
|---------|---------|
|ConnectionStatus     | Estado de Olá da verificação da conectividade Olá. São possíveis resultados **Reachable** e **Unreachable**.        |
|AvgLatencyInMs     | Latência média de durante a verificação da conectividade Olá em milissegundos. (Apenas apresentar se verifique o estado é acessível)        |
|MinLatencyInMs     | Verifique mínimos de latência durante a conectividade de Olá em milissegundos. (Apenas apresentar se verifique o estado é acessível)        |
|MaxLatencyInMs     | Latência máxima durante a conectividade de Olá verifique em milissegundos. (Apenas apresentar se verifique o estado é acessível)        |
|ProbesSent     | Número de sondas enviada durante a verificação de Olá. O valor máximo é 100.        |
|ProbesFailed     | Número de sondas que falhou durante a verificação de Olá. O valor máximo é 100.        |
|Saltos     | Salto pelo caminho do salto de toodestination de origem.        |
|Saltos []. Tipo     | Tipo de recurso. Os valores possíveis são **origem**, **VirtualAppliance**, **VnetLocal**, e **Internet**.        |
|Saltos []. ID | Identificador exclusivo do salto de Olá.|
|Saltos []. Endereço | Endereço IP do salto de Olá.|
|Saltos []. ResourceId | ResourceID do salto de Olá se salto Olá é um recurso do Azure. Se se tratar de um recurso de internet, ResourceID é **Internet**. |
|Saltos []. NextHopIds | Olá Identificador exclusivo de salto seguinte Olá executado.|
|Saltos []. Problemas | Uma coleção de problemas encontrados durante a verificação de Olá nesse hop. Se ocorreram sem problemas, o valor de Olá está em branco.|
|Saltos []. Problemas []. Origem | Em salto atual de Olá, onde ocorreu o problema. Os valores possíveis são:<br/> **Entrada** -problema é a ligação de Olá de Olá anterior salto toohello atual salto<br/>**Saída** -problema é a ligação de Olá de Olá atual salto toohello salto seguinte<br/>**Local** -problema está na salto atual Olá.|
|Saltos []. Problemas []. Gravidade | gravidade de Olá de Olá problema detetado. Os valores possíveis são **erro** e **aviso**. |
|Saltos []. Problemas []. Tipo |tipo de Olá do problema encontrado. Os valores possíveis são: <br/>**CPU**<br/>**Memória**<br/>**GuestFirewall**<br/>**DnsResolution**<br/>**NetworkSecurityRule**<br/>**UserDefinedRoute** |
|Saltos []. Problemas []. Contexto |Detalhes sobre o problema de Olá encontrado.|
|Saltos []. Problemas []. Contexto [] .key |Chave de Olá par chave-valor devolvido.|
|Saltos []. Problemas []. Contexto [] .value |Valor de Olá par chave-valor devolvido.|

Olá segue-se um exemplo de um problema encontrado um salto.

```json
"Issues": [
    {
        "Origin": "Outbound",
        "Severity": "Error",
        "Type": "NetworkSecurityRule",
        "Context": [
            {
                "key": "RuleName",
                "value": "UserRule_Port80"
            }
        ]
    }
]
```
## <a name="fault-types"></a>Tipos de falhas

verificação da conectividade Olá devolve tipos de falhas sobre a ligação de Olá. Olá tabela seguinte fornece uma lista de tipos de falhas atual Olá devolvido.

|Tipo  |Descrição  |
|---------|---------|
|CPU     | Elevada utilização da CPU.       |
|Memória     | Utilização elevada da memória.       |
|GuestFirewall     | O tráfego está bloqueado devido a configuração da firewall tooa máquina virtual.        |
|DNSResolution     | Falha na resolução DNS para endereço de destino Olá.        |
|NetworkSecurityRule    | O tráfego está bloqueado por uma regra de NSG (regra será devolvida)        |
|UserDefinedRoute|O tráfego é ignorado por definidas pelo utilizador de tooa ou rotas de sistema. |

### <a name="next-steps"></a>Passos seguintes

Saiba como recursos de tooa tooverify conectividade, visitando: [Verifique a conectividade com o observador de rede de Azure](network-watcher-connectivity-powershell.md).

<!--Image references-->
[1]: ./media/network-watcher-next-hop-overview/figure1.png

