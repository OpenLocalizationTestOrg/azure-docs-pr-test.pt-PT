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
# <a name="troubleshooting-bad-gateway-errors-in-application-gateway"></a><span data-ttu-id="24059-103">Resolução de problemas de erros do gateway incorreto no Gateway de aplicação</span><span class="sxs-lookup"><span data-stu-id="24059-103">Troubleshooting bad gateway errors in Application Gateway</span></span>

<span data-ttu-id="24059-104">Saiba como erros (502) do tootroubleshoot gateway incorreto receberam ao utilizar o gateway de aplicação.</span><span class="sxs-lookup"><span data-stu-id="24059-104">Learn how tootroubleshoot bad gateway (502) errors received when using application gateway.</span></span>

## <a name="overview"></a><span data-ttu-id="24059-105">Descrição geral</span><span class="sxs-lookup"><span data-stu-id="24059-105">Overview</span></span>

<span data-ttu-id="24059-106">Depois de configurar um gateway de aplicação, um dos erros de Olá que os utilizadores poderão encontrar é "erro de servidor: 502 - o servidor Web recebeu uma resposta inválida enquanto atuava como servidor de gateway ou proxy".</span><span class="sxs-lookup"><span data-stu-id="24059-106">After configuring an application gateway, one of hello errors that users may encounter is "Server Error: 502 - Web server received an invalid response while acting as a gateway or proxy server".</span></span> <span data-ttu-id="24059-107">Este erro pode acontecer devido a seguinte toohello principais razões:</span><span class="sxs-lookup"><span data-stu-id="24059-107">This error may happen due toohello following main reasons:</span></span>

* <span data-ttu-id="24059-108">Azure Gateway de aplicação [conjunto back-end não está configurado ou vazio](#empty-backendaddresspool).</span><span class="sxs-lookup"><span data-stu-id="24059-108">Azure Application Gateway's [back-end pool is not configured or empty](#empty-backendaddresspool).</span></span>
* <span data-ttu-id="24059-109">Nenhum dos Olá VMs ou instâncias [conjunto de dimensionamento de VM estão em bom estado](#unhealthy-instances-in-backendaddresspool).</span><span class="sxs-lookup"><span data-stu-id="24059-109">None of hello VMs or instances in [VM Scale Set are healthy](#unhealthy-instances-in-backendaddresspool).</span></span>
* <span data-ttu-id="24059-110">VMs ou instâncias do conjunto de dimensionamento de VM de back-end são [sonda do Estado de funcionamento não está a responder predefinida de toohello](#problems-with-default-health-probe.md).</span><span class="sxs-lookup"><span data-stu-id="24059-110">Back-end VMs or instances of VM Scale Set are [not responding toohello default health probe](#problems-with-default-health-probe.md).</span></span>
* <span data-ttu-id="24059-111">Inválido ou incorrecto [configuração de sondas de estado de funcionamento personalizado](#problems-with-custom-health-probe.md).</span><span class="sxs-lookup"><span data-stu-id="24059-111">Invalid or improper [configuration of custom health probes](#problems-with-custom-health-probe.md).</span></span>
* <span data-ttu-id="24059-112">[Pedido de tempo limite ou problemas de conectividade](#request-time-out) com pedidos de utilizador.</span><span class="sxs-lookup"><span data-stu-id="24059-112">[Request time out or connectivity issues](#request-time-out) with user requests.</span></span>

## <a name="empty-backendaddresspool"></a><span data-ttu-id="24059-113">BackendAddressPool vazio</span><span class="sxs-lookup"><span data-stu-id="24059-113">Empty BackendAddressPool</span></span>

### <a name="cause"></a><span data-ttu-id="24059-114">Causa</span><span class="sxs-lookup"><span data-stu-id="24059-114">Cause</span></span>

<span data-ttu-id="24059-115">Se Olá Gateway de aplicação tem sem VMs ou conjunto de dimensionamento de VM configurado num conjunto de endereços de back-end de Olá, não é possível encaminhar qualquer pedido de cliente e emite um erro de gateway inválido.</span><span class="sxs-lookup"><span data-stu-id="24059-115">If hello Application Gateway has no VMs or VM Scale Set configured in hello back-end address pool, it cannot route any customer request and throws a bad gateway error.</span></span>

### <a name="solution"></a><span data-ttu-id="24059-116">Solução</span><span class="sxs-lookup"><span data-stu-id="24059-116">Solution</span></span>

<span data-ttu-id="24059-117">Certifique-se de que o conjunto de endereços de back-end de Olá não está vazio.</span><span class="sxs-lookup"><span data-stu-id="24059-117">Ensure that hello back-end address pool is not empty.</span></span> <span data-ttu-id="24059-118">Isto pode ser feito um através do PowerShell, o CLI ou o portal.</span><span class="sxs-lookup"><span data-stu-id="24059-118">This can be done either via PowerShell, CLI, or portal.</span></span>

```powershell
Get-AzureRmApplicationGateway -Name "SampleGateway" -ResourceGroupName "ExampleResourceGroup"
```

<span data-ttu-id="24059-119">saída de Olá de Olá precedente cmdlet deve conter o conjunto de endereços de back-end não vazia.</span><span class="sxs-lookup"><span data-stu-id="24059-119">hello output from hello preceding cmdlet should contain non-empty back-end address pool.</span></span> <span data-ttu-id="24059-120">Segue-se um exemplo em que dois conjuntos, são devolvidos que estão configurados com endereços IP ou FQDN, para as VMs de back-end.</span><span class="sxs-lookup"><span data-stu-id="24059-120">Following is an example where two pools are returned which are configured with FQDN or IP addresses for backend VMs.</span></span> <span data-ttu-id="24059-121">Olá, estado de aprovisionamento de Olá BackendAddressPool tem de ser 'foi concluída com êxito".</span><span class="sxs-lookup"><span data-stu-id="24059-121">hello provisioning state of hello BackendAddressPool must be 'Succeeded'.</span></span>

<span data-ttu-id="24059-122">BackendAddressPoolsText:</span><span class="sxs-lookup"><span data-stu-id="24059-122">BackendAddressPoolsText:</span></span>

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

## <a name="unhealthy-instances-in-backendaddresspool"></a><span data-ttu-id="24059-123">Instâncias de mau estado de funcionamento da BackendAddressPool</span><span class="sxs-lookup"><span data-stu-id="24059-123">Unhealthy instances in BackendAddressPool</span></span>

### <a name="cause"></a><span data-ttu-id="24059-124">Causa</span><span class="sxs-lookup"><span data-stu-id="24059-124">Cause</span></span>

<span data-ttu-id="24059-125">Se todas as instâncias Olá BackendAddressPool mau estado de funcionamento, o Gateway de aplicação teria não qualquer pedido de utilizador tooroute de back-end.</span><span class="sxs-lookup"><span data-stu-id="24059-125">If all hello instances of BackendAddressPool are unhealthy, then Application Gateway would not have any back-end tooroute user request to.</span></span> <span data-ttu-id="24059-126">Isto também pode ser caso Olá quando estão em bom estadas de instâncias de back-end mas não dispõe de aplicação Olá necessário implementada.</span><span class="sxs-lookup"><span data-stu-id="24059-126">This could also be hello case when back-end instances are healthy but do not have hello required application deployed.</span></span>

### <a name="solution"></a><span data-ttu-id="24059-127">Solução</span><span class="sxs-lookup"><span data-stu-id="24059-127">Solution</span></span>

<span data-ttu-id="24059-128">Certifique-se de que as instâncias de Olá estão em bom estadas e aplicação Olá está corretamente configurada.</span><span class="sxs-lookup"><span data-stu-id="24059-128">Ensure that hello instances are healthy and hello application is properly configured.</span></span> <span data-ttu-id="24059-129">Verifique se as instâncias de back-end Olá toorespond capaz de tooa ping de outra VM na mesma VNet Olá.</span><span class="sxs-lookup"><span data-stu-id="24059-129">Check if hello back-end instances are able toorespond tooa ping from another VM in hello same VNet.</span></span> <span data-ttu-id="24059-130">Se configurado com um ponto final público, certifique-se de que uma aplicação web do browser pedido toohello uma.</span><span class="sxs-lookup"><span data-stu-id="24059-130">If configured with a public end point, ensure that a browser request toohello web application is serviceable.</span></span>

## <a name="problems-with-default-health-probe"></a><span data-ttu-id="24059-131">Problemas com a pesquisa de estado de funcionamento predefinida</span><span class="sxs-lookup"><span data-stu-id="24059-131">Problems with default health probe</span></span>

### <a name="cause"></a><span data-ttu-id="24059-132">Causa</span><span class="sxs-lookup"><span data-stu-id="24059-132">Cause</span></span>

<span data-ttu-id="24059-133">502 erros também podem ser frequentes indicadores que Olá sonda do Estado de funcionamento predefinida é tooreach não é possível VMs do back-end.</span><span class="sxs-lookup"><span data-stu-id="24059-133">502 errors can also be frequent indicators that hello default health probe is not able tooreach back-end VMs.</span></span> <span data-ttu-id="24059-134">Quando uma instância de Gateway de aplicação é aprovisionada, este configura automaticamente a um tooeach de sonda de estado de funcionamento predefinida BackendAddressPool utilizando propriedades de Olá BackendHttpSetting.</span><span class="sxs-lookup"><span data-stu-id="24059-134">When an Application Gateway instance is provisioned, it automatically configures a default health probe tooeach BackendAddressPool using properties of hello BackendHttpSetting.</span></span> <span data-ttu-id="24059-135">Não é necessário tooset esta pesquisa de entrada de nenhum utilizador.</span><span class="sxs-lookup"><span data-stu-id="24059-135">No user input is required tooset this probe.</span></span> <span data-ttu-id="24059-136">Especificamente, quando uma regra de balanceamento de carga está configurada, é efetuada uma associação entre um BackendHttpSetting e BackendAddressPool.</span><span class="sxs-lookup"><span data-stu-id="24059-136">Specifically, when a load balancing rule is configured, an association is made between a BackendHttpSetting and BackendAddressPool.</span></span> <span data-ttu-id="24059-137">Uma pesquisa predefinida está configurada para cada uma destas associações e inicia de Gateway de aplicação, uma instância do tooeach de ligação verificação periódicas de integridade no Olá BackendAddressPool na porta Olá especificada no elemento de BackendHttpSetting Olá.</span><span class="sxs-lookup"><span data-stu-id="24059-137">A default probe is configured for each of these associations and Application Gateway initiates a periodic health check connection tooeach instance in hello BackendAddressPool at hello port specified in hello BackendHttpSetting element.</span></span> <span data-ttu-id="24059-138">Tabela seguinte lista os valores de Olá associados à sonda de estado de funcionamento do Olá predefinido.</span><span class="sxs-lookup"><span data-stu-id="24059-138">Following table lists hello values associated with hello default health probe.</span></span>

| <span data-ttu-id="24059-139">Propriedade de pesquisa</span><span class="sxs-lookup"><span data-stu-id="24059-139">Probe property</span></span> | <span data-ttu-id="24059-140">Valor</span><span class="sxs-lookup"><span data-stu-id="24059-140">Value</span></span> | <span data-ttu-id="24059-141">Descrição</span><span class="sxs-lookup"><span data-stu-id="24059-141">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="24059-142">URL de sonda</span><span class="sxs-lookup"><span data-stu-id="24059-142">Probe URL</span></span> |<span data-ttu-id="24059-143">http://127.0.0.1/</span><span class="sxs-lookup"><span data-stu-id="24059-143">http://127.0.0.1/</span></span> |<span data-ttu-id="24059-144">Caminho de URL</span><span class="sxs-lookup"><span data-stu-id="24059-144">URL path</span></span> |
| <span data-ttu-id="24059-145">intervalo</span><span class="sxs-lookup"><span data-stu-id="24059-145">Interval</span></span> |<span data-ttu-id="24059-146">30</span><span class="sxs-lookup"><span data-stu-id="24059-146">30</span></span> |<span data-ttu-id="24059-147">Intervalo de pesquisa em segundos</span><span class="sxs-lookup"><span data-stu-id="24059-147">Probe interval in seconds</span></span> |
| <span data-ttu-id="24059-148">Tempo limite</span><span class="sxs-lookup"><span data-stu-id="24059-148">Time-out</span></span> |<span data-ttu-id="24059-149">30</span><span class="sxs-lookup"><span data-stu-id="24059-149">30</span></span> |<span data-ttu-id="24059-150">Sonda de tempo limite em segundos</span><span class="sxs-lookup"><span data-stu-id="24059-150">Probe time-out in seconds</span></span> |
| <span data-ttu-id="24059-151">Limiar de mau estado de funcionamento</span><span class="sxs-lookup"><span data-stu-id="24059-151">Unhealthy threshold</span></span> |<span data-ttu-id="24059-152">3</span><span class="sxs-lookup"><span data-stu-id="24059-152">3</span></span> |<span data-ttu-id="24059-153">Sonda de contagem de repetições.</span><span class="sxs-lookup"><span data-stu-id="24059-153">Probe retry count.</span></span> <span data-ttu-id="24059-154">servidor de back-end Olá está marcado como após número de falhas de sonda consecutivas Olá atinge o limiar de mau estado de funcionamento de Olá.</span><span class="sxs-lookup"><span data-stu-id="24059-154">hello back-end server is marked down after hello consecutive probe failure count reaches hello unhealthy threshold.</span></span> |

### <a name="solution"></a><span data-ttu-id="24059-155">Solução</span><span class="sxs-lookup"><span data-stu-id="24059-155">Solution</span></span>

* <span data-ttu-id="24059-156">Certifique-se de que um site predefinido está configurado e está à escuta em 127.0.0.1.</span><span class="sxs-lookup"><span data-stu-id="24059-156">Ensure that a default site is configured and is listening at 127.0.0.1.</span></span>
* <span data-ttu-id="24059-157">Se BackendHttpSetting Especifica uma porta diferente 80, site predefinido de Olá deve ser configurado toolisten nessa porta.</span><span class="sxs-lookup"><span data-stu-id="24059-157">If BackendHttpSetting specifies a port other than 80, hello default site should be configured toolisten at that port.</span></span>
* <span data-ttu-id="24059-158">Olá toohttp://127.0.0.1:port chamada deve ser devolvido um código de resultado HTTP de 200.</span><span class="sxs-lookup"><span data-stu-id="24059-158">hello call toohttp://127.0.0.1:port should return an HTTP result code of 200.</span></span> <span data-ttu-id="24059-159">Isto deve ser devolvido dentro do período de tempo limite de 30 segundos Olá.</span><span class="sxs-lookup"><span data-stu-id="24059-159">This should be returned within hello 30 sec time-out period.</span></span>
* <span data-ttu-id="24059-160">Certifique-se de que a porta configurada está aberta e que não são regras de firewall ou grupos de segurança do Azure rede, que bloqueia o tráfego de entrada ou de saída na porta Olá configurado.</span><span class="sxs-lookup"><span data-stu-id="24059-160">Ensure that port configured is open and that there are no firewall rules or Azure Network Security Groups, which block incoming or outgoing traffic on hello port configured.</span></span>
* <span data-ttu-id="24059-161">Se as VMs clássicas do Azure ou serviço em nuvem é utilizado com o FQDN ou o IP público, certifique-se de que Olá correspondente [endpoint](../virtual-machines/windows/classic/setup-endpoints.md?toc=%2fazure%2fapplication-gateway%2ftoc.json) é aberto.</span><span class="sxs-lookup"><span data-stu-id="24059-161">If Azure classic VMs or Cloud Service is used with FQDN or Public IP, ensure that hello corresponding [endpoint](../virtual-machines/windows/classic/setup-endpoints.md?toc=%2fazure%2fapplication-gateway%2ftoc.json) is opened.</span></span>
* <span data-ttu-id="24059-162">Se Olá VM é configurado através do Azure Resource Manager e está fora Olá VNet onde o Gateway de aplicação é implementada, [grupo de segurança de rede](../virtual-network/virtual-networks-nsg.md) tem de ser configurado acesso tooallow Olá pretendido porta.</span><span class="sxs-lookup"><span data-stu-id="24059-162">If hello VM is configured via Azure Resource Manager and is outside hello VNet where Application Gateway is deployed, [Network Security Group](../virtual-network/virtual-networks-nsg.md) must be configured tooallow access on hello desired port.</span></span>

## <a name="problems-with-custom-health-probe"></a><span data-ttu-id="24059-163">Problemas com a pesquisa de estado de funcionamento personalizado</span><span class="sxs-lookup"><span data-stu-id="24059-163">Problems with custom health probe</span></span>

### <a name="cause"></a><span data-ttu-id="24059-164">Causa</span><span class="sxs-lookup"><span data-stu-id="24059-164">Cause</span></span>

<span data-ttu-id="24059-165">Sondas de estado de funcionamento personalizados permitem predefinido de toohello flexibilidade adicional pesquisar comportamento.</span><span class="sxs-lookup"><span data-stu-id="24059-165">Custom health probes allow additional flexibility toohello default probing behavior.</span></span> <span data-ttu-id="24059-166">Quando utilizar das sondas personalizadas, os utilizadores podem configurar intervalo de sonda de Olá, URL de Olá e caminho tootest e quantos tooaccept de respostas de falhas antes de marcar a instância de conjunto back-end Olá como estando danificado.</span><span class="sxs-lookup"><span data-stu-id="24059-166">When using custom probes, users can configure hello probe interval, hello URL, and path tootest, and how many failed responses tooaccept before marking hello back-end pool instance as unhealthy.</span></span> <span data-ttu-id="24059-167">é adicionado Olá seguintes propriedades adicionais.</span><span class="sxs-lookup"><span data-stu-id="24059-167">hello following additional properties are added.</span></span>

| <span data-ttu-id="24059-168">Propriedade de pesquisa</span><span class="sxs-lookup"><span data-stu-id="24059-168">Probe property</span></span> | <span data-ttu-id="24059-169">Descrição</span><span class="sxs-lookup"><span data-stu-id="24059-169">Description</span></span> |
| --- | --- |
| <span data-ttu-id="24059-170">Nome</span><span class="sxs-lookup"><span data-stu-id="24059-170">Name</span></span> |<span data-ttu-id="24059-171">Nome da sonda Olá.</span><span class="sxs-lookup"><span data-stu-id="24059-171">Name of hello probe.</span></span> <span data-ttu-id="24059-172">Este nome é utilizado toorefer toohello sonda nas definições de HTTP de back-end.</span><span class="sxs-lookup"><span data-stu-id="24059-172">This name is used toorefer toohello probe in back-end HTTP settings.</span></span> |
| <span data-ttu-id="24059-173">Protocolo</span><span class="sxs-lookup"><span data-stu-id="24059-173">Protocol</span></span> |<span data-ttu-id="24059-174">O protocolo utilizado sonda de Olá toosend.</span><span class="sxs-lookup"><span data-stu-id="24059-174">Protocol used toosend hello probe.</span></span> <span data-ttu-id="24059-175">sonda de Olá utiliza o protocolo de Olá definido nas definições de HTTP de back-end Olá</span><span class="sxs-lookup"><span data-stu-id="24059-175">hello probe uses hello protocol defined in hello back-end HTTP settings</span></span> |
| <span data-ttu-id="24059-176">Anfitrião</span><span class="sxs-lookup"><span data-stu-id="24059-176">Host</span></span> |<span data-ttu-id="24059-177">Sonda de Olá de toosend de nome de anfitrião.</span><span class="sxs-lookup"><span data-stu-id="24059-177">Host name toosend hello probe.</span></span> <span data-ttu-id="24059-178">Aplicável apenas quando vários sites está configurada no Gateway de aplicação.</span><span class="sxs-lookup"><span data-stu-id="24059-178">Applicable only when multi-site is configured on Application Gateway.</span></span> <span data-ttu-id="24059-179">Isto é diferente do nome de anfitrião VM.</span><span class="sxs-lookup"><span data-stu-id="24059-179">This is different from VM host name.</span></span> |
| <span data-ttu-id="24059-180">Caminho</span><span class="sxs-lookup"><span data-stu-id="24059-180">Path</span></span> |<span data-ttu-id="24059-181">Caminho relativo de sonda de Olá.</span><span class="sxs-lookup"><span data-stu-id="24059-181">Relative path of hello probe.</span></span> <span data-ttu-id="24059-182">inicia a partir do caminho válido de Olá '/'.</span><span class="sxs-lookup"><span data-stu-id="24059-182">hello valid path starts from '/'.</span></span> <span data-ttu-id="24059-183">sonda de Olá é enviada\<protocolo\>://\<anfitrião\>:\<porta\>\<caminho\></span><span class="sxs-lookup"><span data-stu-id="24059-183">hello probe is sent too\<protocol\>://\<host\>:\<port\>\<path\></span></span> |
| <span data-ttu-id="24059-184">intervalo</span><span class="sxs-lookup"><span data-stu-id="24059-184">Interval</span></span> |<span data-ttu-id="24059-185">Intervalo de pesquisa em segundos.</span><span class="sxs-lookup"><span data-stu-id="24059-185">Probe interval in seconds.</span></span> <span data-ttu-id="24059-186">Este é o intervalo de tempo de Olá entre duas sondas consecutivos.</span><span class="sxs-lookup"><span data-stu-id="24059-186">This is hello time interval between two consecutive probes.</span></span> |
| <span data-ttu-id="24059-187">Tempo limite</span><span class="sxs-lookup"><span data-stu-id="24059-187">Time-out</span></span> |<span data-ttu-id="24059-188">Sonda de tempo limite em segundos.</span><span class="sxs-lookup"><span data-stu-id="24059-188">Probe time-out in seconds.</span></span> <span data-ttu-id="24059-189">Se uma resposta válida não foram recebida durante este período de tempo limite, pesquisa Olá está marcada como falhado.</span><span class="sxs-lookup"><span data-stu-id="24059-189">If a valid response is not received within this time-out period, hello probe is marked as failed.</span></span> |
| <span data-ttu-id="24059-190">Limiar de mau estado de funcionamento</span><span class="sxs-lookup"><span data-stu-id="24059-190">Unhealthy threshold</span></span> |<span data-ttu-id="24059-191">Sonda de contagem de repetições.</span><span class="sxs-lookup"><span data-stu-id="24059-191">Probe retry count.</span></span> <span data-ttu-id="24059-192">servidor de back-end Olá está marcado como após número de falhas de sonda consecutivas Olá atinge o limiar de mau estado de funcionamento de Olá.</span><span class="sxs-lookup"><span data-stu-id="24059-192">hello back-end server is marked down after hello consecutive probe failure count reaches hello unhealthy threshold.</span></span> |

### <a name="solution"></a><span data-ttu-id="24059-193">Solução</span><span class="sxs-lookup"><span data-stu-id="24059-193">Solution</span></span>

<span data-ttu-id="24059-194">Valide que Olá que sonda de estado de funcionamento personalizado está corretamente configurada como Olá anterior a tabela.</span><span class="sxs-lookup"><span data-stu-id="24059-194">Validate that hello Custom Health Probe is configured correctly as hello preceding table.</span></span> <span data-ttu-id="24059-195">Além disso toohello anterior resolução de problemas de passos, certifique-se também seguinte Olá:</span><span class="sxs-lookup"><span data-stu-id="24059-195">In addition toohello preceding troubleshooting steps, also ensure hello following:</span></span>

* <span data-ttu-id="24059-196">Certifique-se de que sonda Olá foi especificada corretamente de acordo com Olá [guia](application-gateway-create-probe-ps.md).</span><span class="sxs-lookup"><span data-stu-id="24059-196">Ensure that hello probe is correctly specified as per hello [guide](application-gateway-create-probe-ps.md).</span></span>
* <span data-ttu-id="24059-197">Se o Gateway de aplicação está configurada para um único site, por Olá predefinido anfitrião nome deve ser especificado como '127.0.0.1', a menos que caso contrário configurado na sonda personalizada.</span><span class="sxs-lookup"><span data-stu-id="24059-197">If Application Gateway is configured for a single site, by default hello Host name should be specified as '127.0.0.1', unless otherwise configured in custom probe.</span></span>
* <span data-ttu-id="24059-198">Certifique-se de que uma chamada toohttp: / /\<anfitrião\>:\<porta\>\<caminho\> devolve um código de resultado HTTP de 200.</span><span class="sxs-lookup"><span data-stu-id="24059-198">Ensure that a call toohttp://\<host\>:\<port\>\<path\> returns an HTTP result code of 200.</span></span>
* <span data-ttu-id="24059-199">Certifique-se de que o intervalo, o tempo limite e UnhealtyThreshold respeitam intervalos aceitável Olá.</span><span class="sxs-lookup"><span data-stu-id="24059-199">Ensure that Interval, Time-out and UnhealtyThreshold are within hello acceptable ranges.</span></span>
* <span data-ttu-id="24059-200">Se utilizar um HTTPS sonda, certifique-se de que o servidor back-end Olá não necessita de SNI ao configurar um certificado fallback no servidor de back-end de Olá próprio.</span><span class="sxs-lookup"><span data-stu-id="24059-200">If using an HTTPS probe, make sure that hello backend server doesn't require SNI by configuring a fallback certificate on hello backend server itself.</span></span> 
* <span data-ttu-id="24059-201">Certifique-se de que o intervalo, o tempo limite e que UnhealtyThreshold estão nos intervalos de Olá aceitável.</span><span class="sxs-lookup"><span data-stu-id="24059-201">Ensure that Interval, Time-out, and UnhealtyThreshold are within hello acceptable ranges.</span></span>

## <a name="request-time-out"></a><span data-ttu-id="24059-202">Limite de tempo do pedido</span><span class="sxs-lookup"><span data-stu-id="24059-202">Request time out</span></span>

### <a name="cause"></a><span data-ttu-id="24059-203">Causa</span><span class="sxs-lookup"><span data-stu-id="24059-203">Cause</span></span>

<span data-ttu-id="24059-204">Quando é recebido um pedido de utilizador, o Gateway de aplicação aplica-se Olá configurado regras toohello pedido e encaminha o mesmo tooa instância de conjunto back-end.</span><span class="sxs-lookup"><span data-stu-id="24059-204">When a user request is received, Application Gateway applies hello configured rules toohello request and routes it tooa back-end pool instance.</span></span> <span data-ttu-id="24059-205">Aguarda para um intervalo de tempo para uma resposta de instância de back-end Olá configurável.</span><span class="sxs-lookup"><span data-stu-id="24059-205">It waits for a configurable interval of time for a response from hello back-end instance.</span></span> <span data-ttu-id="24059-206">Por predefinição, este intervalo é **30 segundos**.</span><span class="sxs-lookup"><span data-stu-id="24059-206">By default, this interval is **30 seconds**.</span></span> <span data-ttu-id="24059-207">Se o Gateway de aplicação não recebeu uma resposta de aplicação de back-end este intervalo, a pedido do utilizador é apresentado um erro de 502.</span><span class="sxs-lookup"><span data-stu-id="24059-207">If Application Gateway does not receive a response from back-end application in this interval, user request would see a 502 error.</span></span>

### <a name="solution"></a><span data-ttu-id="24059-208">Solução</span><span class="sxs-lookup"><span data-stu-id="24059-208">Solution</span></span>

<span data-ttu-id="24059-209">Gateway de aplicação permite que os utilizadores tooconfigure esta definição através de BackendHttpSetting, que pode ser, em seguida, aplicar toodifferent agrupamentos.</span><span class="sxs-lookup"><span data-stu-id="24059-209">Application Gateway allows users tooconfigure this setting via BackendHttpSetting, which can be then applied toodifferent pools.</span></span> <span data-ttu-id="24059-210">Diferentes conjuntos de back-end podem ter diferentes BackendHttpSetting e pedido diferentes, por conseguinte, o tempo limite configurado.</span><span class="sxs-lookup"><span data-stu-id="24059-210">Different back-end pools can have different BackendHttpSetting and hence different request time out configured.</span></span>

```powershell
    New-AzureRmApplicationGatewayBackendHttpSettings -Name 'Setting01' -Port 80 -Protocol Http -CookieBasedAffinity Enabled -RequestTimeout 60
```

## <a name="next-steps"></a><span data-ttu-id="24059-211">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="24059-211">Next steps</span></span>

<span data-ttu-id="24059-212">Se hello passos anteriores não resolver o problema de Olá, abra uma [suporta permissão](https://azure.microsoft.com/support/options/).</span><span class="sxs-lookup"><span data-stu-id="24059-212">If hello preceding steps do not resolve hello issue, open a [support ticket](https://azure.microsoft.com/support/options/).</span></span>

