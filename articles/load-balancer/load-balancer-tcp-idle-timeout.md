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
# <a name="configure-tcp-idle-timeout-settings-for-azure-load-balancer"></a><span data-ttu-id="6b733-103">Configurar definições de tempo limite de inatividade de TCP para o Balanceador de carga do Azure</span><span class="sxs-lookup"><span data-stu-id="6b733-103">Configure TCP idle timeout settings for Azure Load Balancer</span></span>

<span data-ttu-id="6b733-104">Na sua configuração predefinida, o Balanceador de carga do Azure tem uma definição de tempo limite de inatividade de 4 minutos.</span><span class="sxs-lookup"><span data-stu-id="6b733-104">In its default configuration, Azure Load Balancer has an idle timeout setting of 4 minutes.</span></span> <span data-ttu-id="6b733-105">Se um período de inatividade é maior do que o valor de tempo limite de Olá, não existe nenhuma garantia que Olá TCP ou sessão HTTP é mantida entre Olá cliente e o serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="6b733-105">If a period of inactivity is longer than hello timeout value, there's no guarantee that hello TCP or HTTP session is maintained between hello client and your cloud service.</span></span>

<span data-ttu-id="6b733-106">Quando Olá a ligação foi fechada, a aplicação cliente pode receber Olá seguir a mensagem de erro: "Olá ligação subjacente foi fechada: uma ligação que esperava toobe mantida activa foi fechada pelo servidor de Olá."</span><span class="sxs-lookup"><span data-stu-id="6b733-106">When hello connection is closed, your client application may receive hello following error message: "hello underlying connection was closed: A connection that was expected toobe kept alive was closed by hello server."</span></span>

<span data-ttu-id="6b733-107">Uma prática comum é toouse uma ligação keep-alive de TCP.</span><span class="sxs-lookup"><span data-stu-id="6b733-107">A common practice is toouse a TCP keep-alive.</span></span> <span data-ttu-id="6b733-108">Esta prática mantém a ligação de Olá Active Directory durante um período de tempo.</span><span class="sxs-lookup"><span data-stu-id="6b733-108">This practice keeps hello connection active for a longer period.</span></span> <span data-ttu-id="6b733-109">Para obter mais informações, consulte estes [exemplos de .NET](https://msdn.microsoft.com/library/system.net.servicepoint.settcpkeepalive.aspx).</span><span class="sxs-lookup"><span data-stu-id="6b733-109">For more information, see these [.NET examples](https://msdn.microsoft.com/library/system.net.servicepoint.settcpkeepalive.aspx).</span></span> <span data-ttu-id="6b733-110">Com ligação keep-alive ativada, os pacotes são enviados durante períodos de inatividade na ligação de Olá.</span><span class="sxs-lookup"><span data-stu-id="6b733-110">With keep-alive enabled, packets are sent during periods of inactivity on hello connection.</span></span> <span data-ttu-id="6b733-111">Estes pacotes ligação keep-alive Certifique-se de que o valor de tempo limite de inatividade Olá nunca seja atingido e ligação Olá é mantida durante um longo período.</span><span class="sxs-lookup"><span data-stu-id="6b733-111">These keep-alive packets ensure that hello idle timeout value is never reached and hello connection is maintained for a long period.</span></span>

<span data-ttu-id="6b733-112">Esta definição funciona em ligações de entrada apenas.</span><span class="sxs-lookup"><span data-stu-id="6b733-112">This setting works for inbound connections only.</span></span> <span data-ttu-id="6b733-113">ligação de perda de tooavoid Olá, tem de configurar Olá TCP ligação keep-alive com um intervalo menor que Olá tempo limite de inatividade definição ou aumente Olá tempo limite de inatividade valor.</span><span class="sxs-lookup"><span data-stu-id="6b733-113">tooavoid losing hello connection, you must configure hello TCP keep-alive with an interval less than hello idle timeout setting or increase hello idle timeout value.</span></span> <span data-ttu-id="6b733-114">toosupport tais cenários, adicionámos suporte para um tempo limite de inatividade configurável.</span><span class="sxs-lookup"><span data-stu-id="6b733-114">toosupport such scenarios, we've added support for a configurable idle timeout.</span></span> <span data-ttu-id="6b733-115">Agora pode defini-lo para uma duração de 4 too30 minutos.</span><span class="sxs-lookup"><span data-stu-id="6b733-115">You can now set it for a duration of 4 too30 minutes.</span></span>

<span data-ttu-id="6b733-116">TCP ligação keep-alive funciona bem para cenários em que a vida bateria não é uma restrição.</span><span class="sxs-lookup"><span data-stu-id="6b733-116">TCP keep-alive works well for scenarios where battery life is not a constraint.</span></span> <span data-ttu-id="6b733-117">Não é recomendado para aplicações móveis.</span><span class="sxs-lookup"><span data-stu-id="6b733-117">It is not recommended for mobile applications.</span></span> <span data-ttu-id="6b733-118">Utilizar uma ligação keep-alive na aplicação móvel de TCP pode drenar bateria do dispositivo de Olá mais rapidamente.</span><span class="sxs-lookup"><span data-stu-id="6b733-118">Using a TCP keep-alive in a mobile application can drain hello device battery faster.</span></span>

![Tempo limite TCP](./media/load-balancer-tcp-idle-timeout/image1.png)

<span data-ttu-id="6b733-120">Olá seguintes secções descreve como toochange inativo definições de tempo limite em máquinas virtuais e serviços em nuvem.</span><span class="sxs-lookup"><span data-stu-id="6b733-120">hello following sections describe how toochange idle timeout settings in virtual machines and cloud services.</span></span>

## <a name="configure-hello-tcp-timeout-for-your-instance-level-public-ip-too15-minutes"></a><span data-ttu-id="6b733-121">Configurar o tempo limite TCP de Olá para os minutos de too15 IP públicos do nível de instância</span><span class="sxs-lookup"><span data-stu-id="6b733-121">Configure hello TCP timeout for your instance-level public IP too15 minutes</span></span>

```powershell
Set-AzurePublicIP -PublicIPName webip -VM MyVM -IdleTimeoutInMinutes 15
```

<span data-ttu-id="6b733-122">`IdleTimeoutInMinutes` é opcional.</span><span class="sxs-lookup"><span data-stu-id="6b733-122">`IdleTimeoutInMinutes` is optional.</span></span> <span data-ttu-id="6b733-123">Se não for definido, o tempo limite predefinido de Olá é 4 minutos.</span><span class="sxs-lookup"><span data-stu-id="6b733-123">If it is not set, hello default timeout is 4 minutes.</span></span> <span data-ttu-id="6b733-124">intervalo de tempo limite aceitável Olá é 4 too30 minutos.</span><span class="sxs-lookup"><span data-stu-id="6b733-124">hello acceptable timeout range is 4 too30 minutes.</span></span>

## <a name="set-hello-idle-timeout-when-creating-an-azure-endpoint-on-a-virtual-machine"></a><span data-ttu-id="6b733-125">Definir o tempo limite de inatividade Olá ao criar um ponto final do Azure numa máquina virtual</span><span class="sxs-lookup"><span data-stu-id="6b733-125">Set hello idle timeout when creating an Azure endpoint on a virtual machine</span></span>

<span data-ttu-id="6b733-126">toochange Olá a definição de um ponto final de limite de tempo, utilize Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="6b733-126">toochange hello timeout setting for an endpoint, use hello following:</span></span>

```powershell
Get-AzureVM -ServiceName "mySvc" -Name "MyVM1" | Add-AzureEndpoint -Name "HttpIn" -Protocol "tcp" -PublicPort 80 -LocalPort 8080 -IdleTimeoutInMinutes 15| Update-AzureVM
```

<span data-ttu-id="6b733-127">tooretrieve a configuração de tempo limite de inatividade, Olá utilize os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="6b733-127">tooretrieve your idle timeout configuration, use hello following command:</span></span>

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

## <a name="set-hello-tcp-timeout-on-a-load-balanced-endpoint-set"></a><span data-ttu-id="6b733-128">Definir um tempo limite TCP de Olá num conjunto de ponto final com balanceamento de carga</span><span class="sxs-lookup"><span data-stu-id="6b733-128">Set hello TCP timeout on a load-balanced endpoint set</span></span>

<span data-ttu-id="6b733-129">Se os pontos finais fizerem parte de um conjunto de ponto final com balanceamento de carga, tem de definir o tempo limite TCP de Olá no conjunto de ponto final com balanceamento de carga Olá.</span><span class="sxs-lookup"><span data-stu-id="6b733-129">If endpoints are part of a load-balanced endpoint set, hello TCP timeout must be set on hello load-balanced endpoint set.</span></span> <span data-ttu-id="6b733-130">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="6b733-130">For example:</span></span>

```powershell
Set-AzureLoadBalancedEndpoint -ServiceName "MyService" -LBSetName "LBSet1" -Protocol tcp -LocalPort 80 -ProbeProtocolTCP -ProbePort 8080 -IdleTimeoutInMinutes 15
```

## <a name="change-timeout-settings-for-cloud-services"></a><span data-ttu-id="6b733-131">Alterar as definições de tempo limite para serviços cloud</span><span class="sxs-lookup"><span data-stu-id="6b733-131">Change timeout settings for cloud services</span></span>

<span data-ttu-id="6b733-132">Pode utilizar Olá Azure SDK tooupdate seu serviço em nuvem.</span><span class="sxs-lookup"><span data-stu-id="6b733-132">You can use hello Azure SDK tooupdate your cloud service.</span></span> <span data-ttu-id="6b733-133">Se as definições de endpoint para serviços em nuvem no ficheiro. csdef Olá.</span><span class="sxs-lookup"><span data-stu-id="6b733-133">You make endpoint settings for cloud services in hello .csdef file.</span></span> <span data-ttu-id="6b733-134">Atualizar o tempo limite TCP de Olá para a implementação de um serviço em nuvem exige uma atualização da implementação.</span><span class="sxs-lookup"><span data-stu-id="6b733-134">Updating hello TCP timeout for deployment of a cloud service requires a deployment upgrade.</span></span> <span data-ttu-id="6b733-135">Uma exceção é se o tempo limite TCP de Olá é especificado apenas para um IP público.</span><span class="sxs-lookup"><span data-stu-id="6b733-135">An exception is if hello TCP timeout is specified only for a public IP.</span></span> <span data-ttu-id="6b733-136">Definições de IP público estão no ficheiro. cscfg Olá e pode atualizá-las através da atualização da implementação e atualização.</span><span class="sxs-lookup"><span data-stu-id="6b733-136">Public IP settings are in hello .cscfg file, and you can update them through deployment update and upgrade.</span></span>

<span data-ttu-id="6b733-137">alterações. csdef Olá para definições de ponto final são:</span><span class="sxs-lookup"><span data-stu-id="6b733-137">hello .csdef changes for endpoint settings are:</span></span>

```xml
<WorkerRole name="worker-role-name" vmsize="worker-role-size" enableNativeCodeExecution="[true|false]">
    <Endpoints>
    <InputEndpoint name="input-endpoint-name" protocol="[http|https|tcp|udp]" localPort="local-port-number" port="port-number" certificate="certificate-name" loadBalancerProbe="load-balancer-probe-name" idleTimeoutInMinutes="tcp-timeout" />
    </Endpoints>
</WorkerRole>
```

<span data-ttu-id="6b733-138">alterações. cscfg Olá para a definição de tempo limite de Olá em IPs públicos são:</span><span class="sxs-lookup"><span data-stu-id="6b733-138">hello .cscfg changes for hello timeout setting on public IPs are:</span></span>

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

## <a name="rest-api-example"></a><span data-ttu-id="6b733-139">Exemplo de REST API</span><span class="sxs-lookup"><span data-stu-id="6b733-139">REST API example</span></span>

<span data-ttu-id="6b733-140">Pode configurar o tempo limite de inatividade do Olá TCP utilizando a API de gestão do serviço de Olá.</span><span class="sxs-lookup"><span data-stu-id="6b733-140">You can configure hello TCP idle timeout by using hello service management API.</span></span> <span data-ttu-id="6b733-141">Certifique-se de que Olá `x-ms-version` cabeçalho está definido tooversion `2014-06-01` ou posterior.</span><span class="sxs-lookup"><span data-stu-id="6b733-141">Make sure that hello `x-ms-version` header is set tooversion `2014-06-01` or later.</span></span> <span data-ttu-id="6b733-142">Olá configuração de Olá especificado com balanceamento de carga pontos finais de entrada em todas as máquinas virtuais numa implementação de atualização.</span><span class="sxs-lookup"><span data-stu-id="6b733-142">Update hello configuration of hello specified load-balanced input endpoints on all virtual machines in a deployment.</span></span>

### <a name="request"></a><span data-ttu-id="6b733-143">Pedir</span><span class="sxs-lookup"><span data-stu-id="6b733-143">Request</span></span>

    POST https://management.core.windows.net/<subscription-id>/services/hostedservices/<cloudservice-name>/deployments/<deployment-name>

### <a name="response"></a><span data-ttu-id="6b733-144">Resposta</span><span class="sxs-lookup"><span data-stu-id="6b733-144">Response</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="6b733-145">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="6b733-145">Next steps</span></span>

[<span data-ttu-id="6b733-146">Descrição geral do Balanceador de carga interno</span><span class="sxs-lookup"><span data-stu-id="6b733-146">Internal load balancer overview</span></span>](load-balancer-internal-overview.md)

[<span data-ttu-id="6b733-147">Começar a configurar um balanceador de carga para a Internet</span><span class="sxs-lookup"><span data-stu-id="6b733-147">Get started configuring an Internet-facing load balancer</span></span>](load-balancer-get-started-internet-arm-ps.md)

[<span data-ttu-id="6b733-148">Configurar um modo de distribuição de balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="6b733-148">Configure a load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)
