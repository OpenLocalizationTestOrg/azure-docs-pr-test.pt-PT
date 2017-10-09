---
title: tempo limite de inatividade de TCP de Balanceador de carga do aaaConfigure | Microsoft Docs
description: Configurar o tempo limite de inatividade de TCP de Balanceador de carga
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
ms.assetid: 4625c6a8-5725-47ce-81db-4fa3bd055891
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/24/2016
ms.author: kumud
ms.openlocfilehash: 2bf0704b891f708e0a5bd7aa827441930f51cfaf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-tcp-idle-timeout-settings-for-azure-load-balancer"></a>Configurar definições de tempo limite de inatividade de TCP para o Balanceador de carga do Azure

Na sua configuração predefinida, o Balanceador de carga do Azure tem uma definição de tempo limite de inatividade de 4 minutos. Se um período de inatividade é maior do que o valor de tempo limite de Olá, não existe nenhuma garantia que Olá TCP ou sessão HTTP é mantida entre Olá cliente e o serviço de nuvem.

Quando Olá a ligação foi fechada, a aplicação cliente pode receber Olá seguir a mensagem de erro: "Olá ligação subjacente foi fechada: uma ligação que esperava toobe mantida activa foi fechada pelo servidor de Olá."

Uma prática comum é toouse uma ligação keep-alive de TCP. Esta prática mantém a ligação de Olá Active Directory durante um período de tempo. Para obter mais informações, consulte estes [exemplos de .NET](https://msdn.microsoft.com/library/system.net.servicepoint.settcpkeepalive.aspx). Com ligação keep-alive ativada, os pacotes são enviados durante períodos de inatividade na ligação de Olá. Estes pacotes ligação keep-alive Certifique-se de que o valor de tempo limite de inatividade Olá nunca seja atingido e ligação Olá é mantida durante um longo período.

Esta definição funciona em ligações de entrada apenas. ligação de perda de tooavoid Olá, tem de configurar Olá TCP ligação keep-alive com um intervalo menor que Olá tempo limite de inatividade definição ou aumente Olá tempo limite de inatividade valor. toosupport tais cenários, adicionámos suporte para um tempo limite de inatividade configurável. Agora pode defini-lo para uma duração de 4 too30 minutos.

TCP ligação keep-alive funciona bem para cenários em que a vida bateria não é uma restrição. Não é recomendado para aplicações móveis. Utilizar uma ligação keep-alive na aplicação móvel de TCP pode drenar bateria do dispositivo de Olá mais rapidamente.

![Tempo limite TCP](./media/load-balancer-tcp-idle-timeout/image1.png)

Olá seguintes secções descreve como toochange inativo definições de tempo limite em máquinas virtuais e serviços em nuvem.

## <a name="configure-hello-tcp-timeout-for-your-instance-level-public-ip-too15-minutes"></a>Configurar o tempo limite TCP de Olá para os minutos de too15 IP públicos do nível de instância

```powershell
Set-AzurePublicIP -PublicIPName webip -VM MyVM -IdleTimeoutInMinutes 15
```

`IdleTimeoutInMinutes` é opcional. Se não for definido, o tempo limite predefinido de Olá é 4 minutos. intervalo de tempo limite aceitável Olá é 4 too30 minutos.

## <a name="set-hello-idle-timeout-when-creating-an-azure-endpoint-on-a-virtual-machine"></a>Definir o tempo limite de inatividade Olá ao criar um ponto final do Azure numa máquina virtual

toochange Olá a definição de um ponto final de limite de tempo, utilize Olá seguinte:

```powershell
Get-AzureVM -ServiceName "mySvc" -Name "MyVM1" | Add-AzureEndpoint -Name "HttpIn" -Protocol "tcp" -PublicPort 80 -LocalPort 8080 -IdleTimeoutInMinutes 15| Update-AzureVM
```

tooretrieve a configuração de tempo limite de inatividade, Olá utilize os seguintes comandos:

    PS C:\> Get-AzureVM -ServiceName "MyService" -Name "MyVM" | Get-AzureEndpoint
    VERBOSE: 6:43:50 PM - Completed Operation: Get Deployment
    LBSetName : MyLoadBalancedSet
    LocalPort : 80
    Name : HTTP
    Port : 80
    Protocol : tcp
    Vip : 65.52.xxx.xxx
    ProbePath :
    ProbePort : 80
    ProbeProtocol : tcp
    ProbeIntervalInSeconds : 15
    ProbeTimeoutInSeconds : 31
    EnableDirectServerReturn : False
    Acl : {}
    InternalLoadBalancerName :
    IdleTimeoutInMinutes : 15

## <a name="set-hello-tcp-timeout-on-a-load-balanced-endpoint-set"></a>Definir um tempo limite TCP de Olá num conjunto de ponto final com balanceamento de carga

Se os pontos finais fizerem parte de um conjunto de ponto final com balanceamento de carga, tem de definir o tempo limite TCP de Olá no conjunto de ponto final com balanceamento de carga Olá. Por exemplo:

```powershell
Set-AzureLoadBalancedEndpoint -ServiceName "MyService" -LBSetName "LBSet1" -Protocol tcp -LocalPort 80 -ProbeProtocolTCP -ProbePort 8080 -IdleTimeoutInMinutes 15
```

## <a name="change-timeout-settings-for-cloud-services"></a>Alterar as definições de tempo limite para serviços cloud

Pode utilizar Olá Azure SDK tooupdate seu serviço em nuvem. Se as definições de endpoint para serviços em nuvem no ficheiro. csdef Olá. Atualizar o tempo limite TCP de Olá para a implementação de um serviço em nuvem exige uma atualização da implementação. Uma exceção é se o tempo limite TCP de Olá é especificado apenas para um IP público. Definições de IP público estão no ficheiro. cscfg Olá e pode atualizá-las através da atualização da implementação e atualização.

alterações. csdef Olá para definições de ponto final são:

```xml
<WorkerRole name="worker-role-name" vmsize="worker-role-size" enableNativeCodeExecution="[true|false]">
    <Endpoints>
    <InputEndpoint name="input-endpoint-name" protocol="[http|https|tcp|udp]" localPort="local-port-number" port="port-number" certificate="certificate-name" loadBalancerProbe="load-balancer-probe-name" idleTimeoutInMinutes="tcp-timeout" />
    </Endpoints>
</WorkerRole>
```

alterações. cscfg Olá para a definição de tempo limite de Olá em IPs públicos são:

```xml
<NetworkConfiguration>
    <VirtualNetworkSite name="VNet"/>
    <AddressAssignments>
    <InstanceAddress roleName="VMRolePersisted">
    <PublicIPs>
        <PublicIP name="public-ip-name" idleTimeoutInMinutes="timeout-in-minutes"/>
    </PublicIPs>
    </InstanceAddress>
    </AddressAssignments>
</NetworkConfiguration>
```

## <a name="rest-api-example"></a>Exemplo de REST API

Pode configurar o tempo limite de inatividade do Olá TCP utilizando a API de gestão do serviço de Olá. Certifique-se de que Olá `x-ms-version` cabeçalho está definido tooversion `2014-06-01` ou posterior. Olá configuração de Olá especificado com balanceamento de carga pontos finais de entrada em todas as máquinas virtuais numa implementação de atualização.

### <a name="request"></a>Pedir

    POST https://management.core.windows.net/<subscription-id>/services/hostedservices/<cloudservice-name>/deployments/<deployment-name>

### <a name="response"></a>Resposta

```xml
<LoadBalancedEndpointList xmlns="http://schemas.microsoft.com/windowsazure" xmlns:i="http://www.w3.org/2001/XMLSchema-instance">
    <InputEndpoint>
    <LoadBalancedEndpointSetName>endpoint-set-name</LoadBalancedEndpointSetName>
    <LocalPort>local-port-number</LocalPort>
    <Port>external-port-number</Port>
    <LoadBalancerProbe>
        <Path>path-of-probe</Path>
        <Port>port-assigned-to-probe</Port>
        <Protocol>probe-protocol</Protocol>
        <IntervalInSeconds>interval-of-probe</IntervalInSeconds>
        <TimeoutInSeconds>timeout-for-probe</TimeoutInSeconds>
    </LoadBalancerProbe>
    <LoadBalancerName>name-of-internal-loadbalancer</LoadBalancerName>
    <Protocol>endpoint-protocol</Protocol>
    <IdleTimeoutInMinutes>15</IdleTimeoutInMinutes>
    <EnableDirectServerReturn>enable-direct-server-return</EnableDirectServerReturn>
    <EndpointACL>
        <Rules>
        <Rule>
            <Order>priority-of-the-rule</Order>
            <Action>permit-rule</Action>
            <RemoteSubnet>subnet-of-the-rule</RemoteSubnet>
            <Description>description-of-the-rule</Description>
        </Rule>
        </Rules>
    </EndpointACL>
    </InputEndpoint>
</LoadBalancedEndpointList>
```

## <a name="next-steps"></a>Passos seguintes

[Descrição geral do Balanceador de carga interno](load-balancer-internal-overview.md)

[Começar a configurar um balanceador de carga para a Internet](load-balancer-get-started-internet-arm-ps.md)

[Configurar um modo de distribuição de balanceador de carga](load-balancer-distribution-mode.md)
