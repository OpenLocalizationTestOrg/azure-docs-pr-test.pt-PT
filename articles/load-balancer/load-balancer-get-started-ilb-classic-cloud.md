---
title: "Criar um balanceador de carga interno para Serviços Cloud do Azure | Microsoft Docs"
description: "Saiba como criar um balanceador de carga interno com o PowerShell no modelo de implementação clássica"
services: load-balancer
documentationcenter: na
author: KumudD
manager: timlt
tags: azure-service-management
ms.assetid: 57966056-0f46-4f95-a295-483ca1ad135d
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 6616c26ede13919b94a098dc38bdd6e2f0fc0b5b
ms.sourcegitcommit: 68aec76e471d677fd9a6333dc60ed098d1072cfc
ms.translationtype: HT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/18/2017
---
# <a name="get-started-creating-an-internal-load-balancer-classic-for-cloud-services"></a>Introdução à criação de um balanceador de carga interno (modo clássico) para serviços em nuvem

> [!div class="op_single_selector"]
> * [PowerShell](../load-balancer/load-balancer-get-started-ilb-classic-ps.md)
> * [CLI do Azure](../load-balancer/load-balancer-get-started-ilb-classic-cli.md)
> * [Serviços cloud](../load-balancer/load-balancer-get-started-ilb-classic-cloud.md)

> [!IMPORTANT]
> O Azure tem dois modelos de implementação diferentes para criar e trabalhar com os recursos: [Resource Manager e clássico](../azure-resource-manager/resource-manager-deployment-model.md).  Este artigo cobre a utilização do modelo de implementação clássica. A Microsoft recomenda que as implementações mais novas utilizem o modelo Resource Manager. Saiba como [executar estes passos com o modelo do Resource Manager](load-balancer-get-started-ilb-arm-ps.md).

## <a name="configure-internal-load-balancer-for-cloud-services"></a>Configurar o balanceador de carga interno para serviços em nuvem

O balanceador de carga interno é suportado para máquinas virtuais e serviços em nuvem. Um ponto final de balanceador de carga interno criado num serviço em nuvem que esteja fora de uma rede virtual regional estará acessível apenas no serviço em nuvem.

A configuração do balanceador de carga interno tem de ser definida durante a criação da primeira implementação no serviço em nuvem, conforme mostrado no exemplo abaixo.

> [!IMPORTANT]
> Um pré-requisito para executar os passos abaixo consiste em ter uma rede virtual já criada para a implementação em nuvem. É necessário o nome da rede virtual e o nome da sub-rede para criar o Balanceamento de Carga Interno.

### <a name="step-1"></a>Passo 1

Abra o ficheiro de configuração do serviço (.cscfg) para a implementação em nuvem no Visual Studio e adicione a secção seguinte para criar o Balanceamento de Carga Interno no último item "`</Role>`" para a configuração de rede.

```xml
<NetworkConfiguration>
    <LoadBalancers>
    <LoadBalancer name="name of the load balancer">
        <FrontendIPConfiguration type="private" subnet="subnet-name" staticVirtualNetworkIPAddress="static-IP-address"/>
    </LoadBalancer>
    </LoadBalancers>
</NetworkConfiguration>
```

Vamos adicionar os valores do ficheiro de configuração de rede para mostrar o seu aspeto. No exemplo, suponha que criou uma VNet denominada "test_vnet" com uma sub-rede 10.0.0.0/24 denominada test_subnet e um IP estático 10.0.0.4. O balanceador de carga será designado como testLB.

```xml
<NetworkConfiguration>
    <LoadBalancers>
    <LoadBalancer name="testLB">
        <FrontendIPConfiguration type="private" subnet="test_subnet" staticVirtualNetworkIPAddress="10.0.0.4"/>
    </LoadBalancer>
    </LoadBalancers>
</NetworkConfiguration>
```

Para obter mais informações sobre o esquema de balanceador de carga, veja [Adicionar balanceador de carga](https://msdn.microsoft.com/library/azure/dn722411.aspx).

### <a name="step-2"></a>Passo 2

Altere o ficheiro de definição do serviço (.csdef) para adicionar pontos finais ao Balanceamento de Carga Interno. No momento que é criada uma instância de função, o ficheiro de definição do serviço irá adicionar as instâncias de função ao Balanceamento de Carga Interno.

```xml
<WorkerRole name="worker-role-name" vmsize="worker-role-size" enableNativeCodeExecution="[true|false]">
    <Endpoints>
    <InputEndpoint name="input-endpoint-name" protocol="[http|https|tcp|udp]" localPort="local-port-number" port="port-number" certificate="certificate-name" loadBalancerProbe="load-balancer-probe-name" loadBalancer="load-balancer-name" />
    </Endpoints>
</WorkerRole>
```

Ao seguir os mesmos valores do exemplo acima, vamos adicionar os valores ao ficheiro de definição do serviço.

```xml
<WorkerRole name="WorkerRole1" vmsize="A7" enableNativeCodeExecution="[true|false]">
    <Endpoints>
    <InputEndpoint name="endpoint1" protocol="http" localPort="80" port="80" loadBalancer="testLB" />
    </Endpoints>
</WorkerRole>
```

Será efetuado o balanceamento de carga do tráfego de rede com o balanceador de carga testLB através da porta 80 para pedidos de entrada e o envio das instâncias de função de trabalho também será na porta 80.

## <a name="next-steps"></a>Passos seguintes

[Configurar um modo de distribuição de balanceador de carga com a afinidade do IP de origem](load-balancer-distribution-mode.md)

[Configurar definições de tempo limite TCP inativo para o balanceador de carga](load-balancer-tcp-idle-timeout.md)

