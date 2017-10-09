---
title: erros de Azure Application Gateway incorreto Gateway (502) aaaTroubleshoot | Microsoft Docs
description: "Saiba como erros tootroubleshoot 502 de Gateway de aplicação"
services: application-gateway
documentationcenter: na
author: amitsriva
manager: rossort
editor: 
tags: azure-resource-manager
ms.assetid: 1d431ead-d318-47d8-b3ad-9c69f7e08813
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/09/2017
ms.author: amsriva
ms.openlocfilehash: a50f736ac157256a53f6fbe3a208f0c11dd58f4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-bad-gateway-errors-in-application-gateway"></a>Resolução de problemas de erros do gateway incorreto no Gateway de aplicação

Saiba como erros (502) do tootroubleshoot gateway incorreto receberam ao utilizar o gateway de aplicação.

## <a name="overview"></a>Descrição geral

Depois de configurar um gateway de aplicação, um dos erros de Olá que os utilizadores poderão encontrar é "erro de servidor: 502 - o servidor Web recebeu uma resposta inválida enquanto atuava como servidor de gateway ou proxy". Este erro pode acontecer devido a seguinte toohello principais razões:

* Azure Gateway de aplicação [conjunto back-end não está configurado ou vazio](#empty-backendaddresspool).
* Nenhum dos Olá VMs ou instâncias [conjunto de dimensionamento de VM estão em bom estado](#unhealthy-instances-in-backendaddresspool).
* VMs ou instâncias do conjunto de dimensionamento de VM de back-end são [sonda do Estado de funcionamento não está a responder predefinida de toohello](#problems-with-default-health-probe.md).
* Inválido ou incorrecto [configuração de sondas de estado de funcionamento personalizado](#problems-with-custom-health-probe.md).
* [Pedido de tempo limite ou problemas de conectividade](#request-time-out) com pedidos de utilizador.

## <a name="empty-backendaddresspool"></a>BackendAddressPool vazio

### <a name="cause"></a>Causa

Se Olá Gateway de aplicação tem sem VMs ou conjunto de dimensionamento de VM configurado num conjunto de endereços de back-end de Olá, não é possível encaminhar qualquer pedido de cliente e emite um erro de gateway inválido.

### <a name="solution"></a>Solução

Certifique-se de que o conjunto de endereços de back-end de Olá não está vazio. Isto pode ser feito um através do PowerShell, o CLI ou o portal.

```powershell
Get-AzureRmApplicationGateway -Name "SampleGateway" -ResourceGroupName "ExampleResourceGroup"
```

saída de Olá de Olá precedente cmdlet deve conter o conjunto de endereços de back-end não vazia. Segue-se um exemplo em que dois conjuntos, são devolvidos que estão configurados com endereços IP ou FQDN, para as VMs de back-end. Olá, estado de aprovisionamento de Olá BackendAddressPool tem de ser 'foi concluída com êxito".

BackendAddressPoolsText:

```json
[{
    "BackendAddresses": [{
        "ipAddress": "10.0.0.10",
        "ipAddress": "10.0.0.11"
    }],
    "BackendIpConfigurations": [],
    "ProvisioningState": "Succeeded",
    "Name": "Pool01",
    "Etag": "W/\"00000000-0000-0000-0000-000000000000\"",
    "Id": "/subscriptions/<subscription id>/resourceGroups/<resource group name>/providers/Microsoft.Network/applicationGateways/<application gateway name>/backendAddressPools/pool01"
}, {
    "BackendAddresses": [{
        "Fqdn": "xyx.cloudapp.net",
        "Fqdn": "abc.cloudapp.net"
    }],
    "BackendIpConfigurations": [],
    "ProvisioningState": "Succeeded",
    "Name": "Pool02",
    "Etag": "W/\"00000000-0000-0000-0000-000000000000\"",
    "Id": "/subscriptions/<subscription id>/resourceGroups/<resource group name>/providers/Microsoft.Network/applicationGateways/<application gateway name>/backendAddressPools/pool02"
}]
```

## <a name="unhealthy-instances-in-backendaddresspool"></a>Instâncias de mau estado de funcionamento da BackendAddressPool

### <a name="cause"></a>Causa

Se todas as instâncias Olá BackendAddressPool mau estado de funcionamento, o Gateway de aplicação teria não qualquer pedido de utilizador tooroute de back-end. Isto também pode ser caso Olá quando estão em bom estadas de instâncias de back-end mas não dispõe de aplicação Olá necessário implementada.

### <a name="solution"></a>Solução

Certifique-se de que as instâncias de Olá estão em bom estadas e aplicação Olá está corretamente configurada. Verifique se as instâncias de back-end Olá toorespond capaz de tooa ping de outra VM na mesma VNet Olá. Se configurado com um ponto final público, certifique-se de que uma aplicação web do browser pedido toohello uma.

## <a name="problems-with-default-health-probe"></a>Problemas com a pesquisa de estado de funcionamento predefinida

### <a name="cause"></a>Causa

502 erros também podem ser frequentes indicadores que Olá sonda do Estado de funcionamento predefinida é tooreach não é possível VMs do back-end. Quando uma instância de Gateway de aplicação é aprovisionada, este configura automaticamente a um tooeach de sonda de estado de funcionamento predefinida BackendAddressPool utilizando propriedades de Olá BackendHttpSetting. Não é necessário tooset esta pesquisa de entrada de nenhum utilizador. Especificamente, quando uma regra de balanceamento de carga está configurada, é efetuada uma associação entre um BackendHttpSetting e BackendAddressPool. Uma pesquisa predefinida está configurada para cada uma destas associações e inicia de Gateway de aplicação, uma instância do tooeach de ligação verificação periódicas de integridade no Olá BackendAddressPool na porta Olá especificada no elemento de BackendHttpSetting Olá. Tabela seguinte lista os valores de Olá associados à sonda de estado de funcionamento do Olá predefinido.

| Propriedade de pesquisa | Valor | Descrição |
| --- | --- | --- |
| URL de sonda |http://127.0.0.1/ |Caminho de URL |
| intervalo |30 |Intervalo de pesquisa em segundos |
| Tempo limite |30 |Sonda de tempo limite em segundos |
| Limiar de mau estado de funcionamento |3 |Sonda de contagem de repetições. servidor de back-end Olá está marcado como após número de falhas de sonda consecutivas Olá atinge o limiar de mau estado de funcionamento de Olá. |

### <a name="solution"></a>Solução

* Certifique-se de que um site predefinido está configurado e está à escuta em 127.0.0.1.
* Se BackendHttpSetting Especifica uma porta diferente 80, site predefinido de Olá deve ser configurado toolisten nessa porta.
* Olá toohttp://127.0.0.1:port chamada deve ser devolvido um código de resultado HTTP de 200. Isto deve ser devolvido dentro do período de tempo limite de 30 segundos Olá.
* Certifique-se de que a porta configurada está aberta e que não são regras de firewall ou grupos de segurança do Azure rede, que bloqueia o tráfego de entrada ou de saída na porta Olá configurado.
* Se as VMs clássicas do Azure ou serviço em nuvem é utilizado com o FQDN ou o IP público, certifique-se de que Olá correspondente [endpoint](../virtual-machines/windows/classic/setup-endpoints.md?toc=%2fazure%2fapplication-gateway%2ftoc.json) é aberto.
* Se Olá VM é configurado através do Azure Resource Manager e está fora Olá VNet onde o Gateway de aplicação é implementada, [grupo de segurança de rede](../virtual-network/virtual-networks-nsg.md) tem de ser configurado acesso tooallow Olá pretendido porta.

## <a name="problems-with-custom-health-probe"></a>Problemas com a pesquisa de estado de funcionamento personalizado

### <a name="cause"></a>Causa

Sondas de estado de funcionamento personalizados permitem predefinido de toohello flexibilidade adicional pesquisar comportamento. Quando utilizar das sondas personalizadas, os utilizadores podem configurar intervalo de sonda de Olá, URL de Olá e caminho tootest e quantos tooaccept de respostas de falhas antes de marcar a instância de conjunto back-end Olá como estando danificado. é adicionado Olá seguintes propriedades adicionais.

| Propriedade de pesquisa | Descrição |
| --- | --- |
| Nome |Nome da sonda Olá. Este nome é utilizado toorefer toohello sonda nas definições de HTTP de back-end. |
| Protocolo |O protocolo utilizado sonda de Olá toosend. sonda de Olá utiliza o protocolo de Olá definido nas definições de HTTP de back-end Olá |
| Anfitrião |Sonda de Olá de toosend de nome de anfitrião. Aplicável apenas quando vários sites está configurada no Gateway de aplicação. Isto é diferente do nome de anfitrião VM. |
| Caminho |Caminho relativo de sonda de Olá. inicia a partir do caminho válido de Olá '/'. sonda de Olá é enviada\<protocolo\>://\<anfitrião\>:\<porta\>\<caminho\> |
| intervalo |Intervalo de pesquisa em segundos. Este é o intervalo de tempo de Olá entre duas sondas consecutivos. |
| Tempo limite |Sonda de tempo limite em segundos. Se uma resposta válida não foram recebida durante este período de tempo limite, pesquisa Olá está marcada como falhado. |
| Limiar de mau estado de funcionamento |Sonda de contagem de repetições. servidor de back-end Olá está marcado como após número de falhas de sonda consecutivas Olá atinge o limiar de mau estado de funcionamento de Olá. |

### <a name="solution"></a>Solução

Valide que Olá que sonda de estado de funcionamento personalizado está corretamente configurada como Olá anterior a tabela. Além disso toohello anterior resolução de problemas de passos, certifique-se também seguinte Olá:

* Certifique-se de que sonda Olá foi especificada corretamente de acordo com Olá [guia](application-gateway-create-probe-ps.md).
* Se o Gateway de aplicação está configurada para um único site, por Olá predefinido anfitrião nome deve ser especificado como '127.0.0.1', a menos que caso contrário configurado na sonda personalizada.
* Certifique-se de que uma chamada toohttp: / /\<anfitrião\>:\<porta\>\<caminho\> devolve um código de resultado HTTP de 200.
* Certifique-se de que o intervalo, o tempo limite e UnhealtyThreshold respeitam intervalos aceitável Olá.
* Se utilizar um HTTPS sonda, certifique-se de que o servidor back-end Olá não necessita de SNI ao configurar um certificado fallback no servidor de back-end de Olá próprio. 
* Certifique-se de que o intervalo, o tempo limite e que UnhealtyThreshold estão nos intervalos de Olá aceitável.

## <a name="request-time-out"></a>Limite de tempo do pedido

### <a name="cause"></a>Causa

Quando é recebido um pedido de utilizador, o Gateway de aplicação aplica-se Olá configurado regras toohello pedido e encaminha o mesmo tooa instância de conjunto back-end. Aguarda para um intervalo de tempo para uma resposta de instância de back-end Olá configurável. Por predefinição, este intervalo é **30 segundos**. Se o Gateway de aplicação não recebeu uma resposta de aplicação de back-end este intervalo, a pedido do utilizador é apresentado um erro de 502.

### <a name="solution"></a>Solução

Gateway de aplicação permite que os utilizadores tooconfigure esta definição através de BackendHttpSetting, que pode ser, em seguida, aplicar toodifferent agrupamentos. Diferentes conjuntos de back-end podem ter diferentes BackendHttpSetting e pedido diferentes, por conseguinte, o tempo limite configurado.

```powershell
    New-AzureRmApplicationGatewayBackendHttpSettings -Name 'Setting01' -Port 80 -Protocol Http -CookieBasedAffinity Enabled -RequestTimeout 60
```

## <a name="next-steps"></a>Passos seguintes

Se hello passos anteriores não resolver o problema de Olá, abra uma [suporta permissão](https://azure.microsoft.com/support/options/).

