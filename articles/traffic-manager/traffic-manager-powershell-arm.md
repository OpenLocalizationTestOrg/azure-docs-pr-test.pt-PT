---
title: aaaUsing PowerShell toomanage Traffic Manager no Azure | Microsoft Docs
description: "Com o PowerShell para o Gestor de tráfego com o Azure Resource Manager"
services: traffic-manager
documentationcenter: na
author: kumudd
manager: timlt
ms.assetid: bc247448-1d2e-4104-ac03-42b59ebde065
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/16/2017
ms.author: kumud
ms.openlocfilehash: 018c37db63beb82fdad54cfd7e13ab3cb645723a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="using-powershell-toomanage-traffic-manager"></a><span data-ttu-id="acc5e-103">Utilizar o PowerShell toomanage Gestor de tráfego</span><span class="sxs-lookup"><span data-stu-id="acc5e-103">Using PowerShell toomanage Traffic Manager</span></span>

<span data-ttu-id="acc5e-104">O Azure Resource Manager é Olá a interface de gestão preferenciais para serviços no Azure.</span><span class="sxs-lookup"><span data-stu-id="acc5e-104">Azure Resource Manager is hello preferred management interface for services in Azure.</span></span> <span data-ttu-id="acc5e-105">Perfis do Traffic Manager do Azure podem ser geridos através de APIs do Azure Resource Manager e as ferramentas.</span><span class="sxs-lookup"><span data-stu-id="acc5e-105">Azure Traffic Manager profiles can be managed using Azure Resource Manager-based APIs and tools.</span></span>

## <a name="resource-model"></a><span data-ttu-id="acc5e-106">Modelo de recursos</span><span class="sxs-lookup"><span data-stu-id="acc5e-106">Resource model</span></span>

<span data-ttu-id="acc5e-107">Traffic Manager do Azure está configurado com uma coleção de definições denominado um perfil do Traffic Manager.</span><span class="sxs-lookup"><span data-stu-id="acc5e-107">Azure Traffic Manager is configured using a collection of settings called a Traffic Manager profile.</span></span> <span data-ttu-id="acc5e-108">Este perfil contém as definições de DNS, as definições de encaminhamento de tráfego, ponto final de definições de monitorização e uma lista de tráfego de toowhich pontos finais do serviço é encaminhada.</span><span class="sxs-lookup"><span data-stu-id="acc5e-108">This profile contains DNS settings, traffic routing settings, endpoint monitoring settings, and a list of service endpoints toowhich traffic is routed.</span></span>

<span data-ttu-id="acc5e-109">Cada perfil de Gestor de tráfego é representada por um recurso do tipo 'TrafficManagerProfiles'.</span><span class="sxs-lookup"><span data-stu-id="acc5e-109">Each Traffic Manager profile is represented by a resource of type 'TrafficManagerProfiles'.</span></span> <span data-ttu-id="acc5e-110">Ao nível da API de REST Olá, Olá URI para cada perfil é:</span><span class="sxs-lookup"><span data-stu-id="acc5e-110">At hello REST API level, hello URI for each profile is as follows:</span></span>

    https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Network/trafficManagerProfiles/{profile-name}?api-version={api-version}

## <a name="setting-up-azure-powershell"></a><span data-ttu-id="acc5e-111">Configurar o Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="acc5e-111">Setting up Azure PowerShell</span></span>

<span data-ttu-id="acc5e-112">Estas instruções utilizam o Microsoft Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="acc5e-112">These instructions use Microsoft Azure PowerShell.</span></span> <span data-ttu-id="acc5e-113">Olá seguinte artigo explica como tooinstall e configurar o Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="acc5e-113">hello following article explains how tooinstall and configure Azure PowerShell.</span></span>

* [<span data-ttu-id="acc5e-114">Como tooinstall e configurar o Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="acc5e-114">How tooinstall and configure Azure PowerShell</span></span>](/powershell/azure/overview)

<span data-ttu-id="acc5e-115">Exemplos de Olá deste artigo partem do princípio de que tem um grupo de recursos existente.</span><span class="sxs-lookup"><span data-stu-id="acc5e-115">hello examples in this article assume that you have an existing resource group.</span></span> <span data-ttu-id="acc5e-116">Pode criar um grupo de recursos com Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="acc5e-116">You can create a resource group using hello following command:</span></span>

```powershell
New-AzureRmResourceGroup -Name MyRG -Location "West US"
```

> [!NOTE]
> <span data-ttu-id="acc5e-117">O Azure Resource Manager requer que todos os grupos de recursos tem uma localização.</span><span class="sxs-lookup"><span data-stu-id="acc5e-117">Azure Resource Manager requires that all resource groups have a location.</span></span> <span data-ttu-id="acc5e-118">Esta localização é utilizada como predefinição de Olá de recursos criados nesse grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="acc5e-118">This location is used as hello default for resources created in that resource group.</span></span> <span data-ttu-id="acc5e-119">No entanto, uma vez que os recursos de perfil do Gestor de tráfego são globais, não regionais, escolha de Olá de localização do grupo de recursos não tem impacto no Gestor de tráfego do Azure.</span><span class="sxs-lookup"><span data-stu-id="acc5e-119">However, since Traffic Manager profile resources are global, not regional, hello choice of resource group location has no impact on Azure Traffic Manager.</span></span>

## <a name="create-a-traffic-manager-profile"></a><span data-ttu-id="acc5e-120">Criar um perfil de Gestor de tráfego</span><span class="sxs-lookup"><span data-stu-id="acc5e-120">Create a Traffic Manager Profile</span></span>

<span data-ttu-id="acc5e-121">toocreate um perfil do Traffic Manager, utilize Olá `New-AzureRmTrafficManagerProfile` cmdlet:</span><span class="sxs-lookup"><span data-stu-id="acc5e-121">toocreate a Traffic Manager profile, use hello `New-AzureRmTrafficManagerProfile` cmdlet:</span></span>

```powershell
$profile = New-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyRG -TrafficRoutingMethod Performance -RelativeDnsName contoso -Ttl 30 -MonitorProtocol HTTP -MonitorPort 80 -MonitorPath "/"
```

<span data-ttu-id="acc5e-122">Olá, a tabela seguinte descreve os parâmetros de Olá:</span><span class="sxs-lookup"><span data-stu-id="acc5e-122">hello following table describes hello parameters:</span></span>

| <span data-ttu-id="acc5e-123">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="acc5e-123">Parameter</span></span> | <span data-ttu-id="acc5e-124">Descrição</span><span class="sxs-lookup"><span data-stu-id="acc5e-124">Description</span></span> |
| --- | --- |
| <span data-ttu-id="acc5e-125">Nome</span><span class="sxs-lookup"><span data-stu-id="acc5e-125">Name</span></span> |<span data-ttu-id="acc5e-126">nome do recurso de Olá para Olá recursos de perfil do Gestor de tráfego.</span><span class="sxs-lookup"><span data-stu-id="acc5e-126">hello resource name for hello Traffic Manager profile resource.</span></span> <span data-ttu-id="acc5e-127">Os perfis do Olá mesmo grupo de recursos tem de ter nomes exclusivos.</span><span class="sxs-lookup"><span data-stu-id="acc5e-127">Profiles in hello same resource group must have unique names.</span></span> <span data-ttu-id="acc5e-128">Este nome está separado do nome DNS Olá utilizada para consultas DNS.</span><span class="sxs-lookup"><span data-stu-id="acc5e-128">This name is separate from hello DNS name used for DNS queries.</span></span> |
| <span data-ttu-id="acc5e-129">resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="acc5e-129">ResourceGroupName</span></span> |<span data-ttu-id="acc5e-130">nome de Olá do Olá recursos que contém Olá perfil recurso do grupo.</span><span class="sxs-lookup"><span data-stu-id="acc5e-130">hello name of hello resource group containing hello profile resource.</span></span> |
| <span data-ttu-id="acc5e-131">TrafficRoutingMethod</span><span class="sxs-lookup"><span data-stu-id="acc5e-131">TrafficRoutingMethod</span></span> |<span data-ttu-id="acc5e-132">Especifica Olá encaminhamento de tráfego método utilizado toodetermine o ponto final é devolvido em resposta uma consulta DNS.</span><span class="sxs-lookup"><span data-stu-id="acc5e-132">Specifies hello traffic-routing method used toodetermine which endpoint is returned in response a DNS query.</span></span> <span data-ttu-id="acc5e-133">Os valores possíveis são 'Desempenho', 'Weighted' ou 'Priority'.</span><span class="sxs-lookup"><span data-stu-id="acc5e-133">Possible values are 'Performance', 'Weighted' or 'Priority'.</span></span> |
| <span data-ttu-id="acc5e-134">RelativeDnsName</span><span class="sxs-lookup"><span data-stu-id="acc5e-134">RelativeDnsName</span></span> |<span data-ttu-id="acc5e-135">Especifica a parte do nome de anfitrião Olá Olá DNS do nome de fornecido por este perfil do Traffic Manager.</span><span class="sxs-lookup"><span data-stu-id="acc5e-135">Specifies hello hostname portion of hello DNS name provided by this Traffic Manager profile.</span></span> <span data-ttu-id="acc5e-136">Este valor é combinado com o nome de domínio DNS de Olá utilizada pelo Gestor de tráfego do Azure tooform Olá nome domínio completamente qualificado (FQDN) do perfil de Olá.</span><span class="sxs-lookup"><span data-stu-id="acc5e-136">This value is combined with hello DNS domain name used by Azure Traffic Manager tooform hello fully qualified domain name (FQDN) of hello profile.</span></span> <span data-ttu-id="acc5e-137">Por exemplo, definir o valor de Olá da "contoso" fica 'contoso.trafficmanager.net'.</span><span class="sxs-lookup"><span data-stu-id="acc5e-137">For example, setting hello value of 'contoso' becomes 'contoso.trafficmanager.net.'</span></span> |
| <span data-ttu-id="acc5e-138">VALOR DE TTL</span><span class="sxs-lookup"><span data-stu-id="acc5e-138">TTL</span></span> |<span data-ttu-id="acc5e-139">Especifica Olá DNS Time-to-Live (TTL), em segundos.</span><span class="sxs-lookup"><span data-stu-id="acc5e-139">Specifies hello DNS Time-to-Live (TTL), in seconds.</span></span> <span data-ttu-id="acc5e-140">Este valor de TTL informa as resoluções Local DNS Olá e clientes DNS quanto toocache, as respostas DNS, para este perfil do Traffic Manager.</span><span class="sxs-lookup"><span data-stu-id="acc5e-140">This TTL informs hello Local DNS resolvers and DNS clients how long toocache DNS responses for this Traffic Manager profile.</span></span> |
| <span data-ttu-id="acc5e-141">MonitorProtocol</span><span class="sxs-lookup"><span data-stu-id="acc5e-141">MonitorProtocol</span></span> |<span data-ttu-id="acc5e-142">Especifica o estado de funcionamento do Olá protocolo toouse toomonitor ponto final.</span><span class="sxs-lookup"><span data-stu-id="acc5e-142">Specifies hello protocol toouse toomonitor endpoint health.</span></span> <span data-ttu-id="acc5e-143">Os valores possíveis são 'HTTP' e 'HTTPS'.</span><span class="sxs-lookup"><span data-stu-id="acc5e-143">Possible values are 'HTTP' and 'HTTPS'.</span></span> |
| <span data-ttu-id="acc5e-144">MonitorPort</span><span class="sxs-lookup"><span data-stu-id="acc5e-144">MonitorPort</span></span> |<span data-ttu-id="acc5e-145">Especifica Olá a porta TCP utilizada toomonitor estado de funcionamento do ponto final.</span><span class="sxs-lookup"><span data-stu-id="acc5e-145">Specifies hello TCP port used toomonitor endpoint health.</span></span> |
| <span data-ttu-id="acc5e-146">MonitorPath</span><span class="sxs-lookup"><span data-stu-id="acc5e-146">MonitorPath</span></span> |<span data-ttu-id="acc5e-147">Especifica o nome de domínio de ponto final do Olá caminho relativo toohello utilizado tooprobe para Estado de funcionamento do ponto final.</span><span class="sxs-lookup"><span data-stu-id="acc5e-147">Specifies hello path relative toohello endpoint domain name used tooprobe for endpoint health.</span></span> |

<span data-ttu-id="acc5e-148">Olá cmdlet cria um perfil do Traffic Manager no Azure e devolve um objeto tooPowerShell correspondente do perfil.</span><span class="sxs-lookup"><span data-stu-id="acc5e-148">hello cmdlet creates a Traffic Manager profile in Azure and returns a corresponding profile object tooPowerShell.</span></span> <span data-ttu-id="acc5e-149">Neste momento, o perfil de Olá não contém quaisquer pontos finais.</span><span class="sxs-lookup"><span data-stu-id="acc5e-149">At this point, hello profile does not contain any endpoints.</span></span> <span data-ttu-id="acc5e-150">Para obter mais informações sobre como adicionar o perfil do Gestor de tráfego de tooa de pontos finais, consulte [adicionar pontos finais de Gestor de tráfego](#adding-traffic-manager-endpoints).</span><span class="sxs-lookup"><span data-stu-id="acc5e-150">For more information about adding endpoints tooa Traffic Manager profile, see [Adding Traffic Manager Endpoints](#adding-traffic-manager-endpoints).</span></span>

## <a name="get-a-traffic-manager-profile"></a><span data-ttu-id="acc5e-151">Obter um perfil do Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="acc5e-151">Get a Traffic Manager Profile</span></span>

<span data-ttu-id="acc5e-152">tooretrieve um objeto de perfil do Traffic Manager existente, utilize Olá `Get-AzureRmTrafficManagerProfle` cmdlet:</span><span class="sxs-lookup"><span data-stu-id="acc5e-152">tooretrieve an existing Traffic Manager profile object, use hello `Get-AzureRmTrafficManagerProfle` cmdlet:</span></span>

```powershell
$profile = Get-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyRG
```

<span data-ttu-id="acc5e-153">Este cmdlet devolve um objeto de perfil do Traffic Manager.</span><span class="sxs-lookup"><span data-stu-id="acc5e-153">This cmdlet returns a Traffic Manager profile object.</span></span>

## <a name="update-a-traffic-manager-profile"></a><span data-ttu-id="acc5e-154">Atualizar um perfil do Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="acc5e-154">Update a Traffic Manager Profile</span></span>

<span data-ttu-id="acc5e-155">Modificar perfis do Traffic Manager segue um processo do passo 3:</span><span class="sxs-lookup"><span data-stu-id="acc5e-155">Modifying Traffic Manager profiles follows a 3-step process:</span></span>

1. <span data-ttu-id="acc5e-156">Obter Olá perfil utilizar `Get-AzureRmTrafficManagerProfile` ou utilizar o perfil de Olá devolvido pelo `New-AzureRmTrafficManagerProfile`.</span><span class="sxs-lookup"><span data-stu-id="acc5e-156">Retrieve hello profile using `Get-AzureRmTrafficManagerProfile` or use hello profile returned by `New-AzureRmTrafficManagerProfile`.</span></span>
2. <span data-ttu-id="acc5e-157">Modificar o perfil de Olá.</span><span class="sxs-lookup"><span data-stu-id="acc5e-157">Modify hello profile.</span></span> <span data-ttu-id="acc5e-158">Pode adicionar e remover pontos finais ou altere os parâmetros do ponto final ou o perfil.</span><span class="sxs-lookup"><span data-stu-id="acc5e-158">You can add and remove endpoints or change endpoint or profile parameters.</span></span> <span data-ttu-id="acc5e-159">Estas alterações são operações offline.</span><span class="sxs-lookup"><span data-stu-id="acc5e-159">These changes are off-line operations.</span></span> <span data-ttu-id="acc5e-160">Só está a alterar o objeto local do Olá na memória que representa o perfil de Olá.</span><span class="sxs-lookup"><span data-stu-id="acc5e-160">You are only changing hello local object in memory that represents hello profile.</span></span>
3. <span data-ttu-id="acc5e-161">Consolidar as alterações utilizando Olá `Set-AzureRmTrafficManagerProfile` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="acc5e-161">Commit your changes using hello `Set-AzureRmTrafficManagerProfile` cmdlet.</span></span>

<span data-ttu-id="acc5e-162">Todas as propriedades de perfil podem ser alteradas, exceto RelativeDnsName do perfil de Olá.</span><span class="sxs-lookup"><span data-stu-id="acc5e-162">All profile properties can be changed except hello profile's RelativeDnsName.</span></span> <span data-ttu-id="acc5e-163">toochange Olá RelativeDnsName, tem de eliminar o perfil e um novo perfil com um novo nome.</span><span class="sxs-lookup"><span data-stu-id="acc5e-163">toochange hello RelativeDnsName, you must delete profile and a new profile with a new name.</span></span>

<span data-ttu-id="acc5e-164">Olá seguinte o exemplo demonstra como toochange Olá TTL do perfil:</span><span class="sxs-lookup"><span data-stu-id="acc5e-164">hello following example demonstrates how toochange hello profile's TTL:</span></span>

```powershell
$profile = Get-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyRG
$profile.Ttl = 300
Set-AzureRmTrafficManagerProfile -TrafficManagerProfile $profile
```

<span data-ttu-id="acc5e-165">Existem três tipos de pontos finais do Gestor de tráfego:</span><span class="sxs-lookup"><span data-stu-id="acc5e-165">There are three types of Traffic Manager endpoints:</span></span>

1. <span data-ttu-id="acc5e-166">**Pontos finais Azure** são serviços alojados no Azure</span><span class="sxs-lookup"><span data-stu-id="acc5e-166">**Azure endpoints** are services hosted in Azure</span></span>
2. <span data-ttu-id="acc5e-167">**Pontos finais externos** são serviços alojados fora do Azure</span><span class="sxs-lookup"><span data-stu-id="acc5e-167">**External endpoints** are services hosted outside of Azure</span></span>
3. <span data-ttu-id="acc5e-168">**Pontos finais de aninhada** são utilizados tooconstruct aninhada hierarquias de perfis do Traffic Manager.</span><span class="sxs-lookup"><span data-stu-id="acc5e-168">**Nested endpoints** are used tooconstruct nested hierarchies of Traffic Manager profiles.</span></span> <span data-ttu-id="acc5e-169">Pontos finais aninhados ativar o encaminhamento de tráfego configurações avançadas para aplicações complexas.</span><span class="sxs-lookup"><span data-stu-id="acc5e-169">Nested endpoints enable advanced traffic-routing configurations for complex applications.</span></span>

<span data-ttu-id="acc5e-170">Em três casos, é possível adicionar pontos finais de duas formas:</span><span class="sxs-lookup"><span data-stu-id="acc5e-170">In all three cases, endpoints can be added in two ways:</span></span>

1. <span data-ttu-id="acc5e-171">Através de um processo de passo 3 descrito anteriormente.</span><span class="sxs-lookup"><span data-stu-id="acc5e-171">Using a 3-step process described previously.</span></span> <span data-ttu-id="acc5e-172">Olá vantagem este método é que várias alterações de ponto final podem ser efetuadas numa única atualização.</span><span class="sxs-lookup"><span data-stu-id="acc5e-172">hello advantage of this method is that several endpoint changes can be made in a single update.</span></span>
2. <span data-ttu-id="acc5e-173">Utilizando o cmdlet New-AzureRmTrafficManagerEndpoint de Olá.</span><span class="sxs-lookup"><span data-stu-id="acc5e-173">Using hello New-AzureRmTrafficManagerEndpoint cmdlet.</span></span> <span data-ttu-id="acc5e-174">Este cmdlet adiciona um perfil de Gestor de tráfego existente do ponto final tooan numa única operação.</span><span class="sxs-lookup"><span data-stu-id="acc5e-174">This cmdlet adds an endpoint tooan existing Traffic Manager profile in a single operation.</span></span>

## <a name="adding-azure-endpoints"></a><span data-ttu-id="acc5e-175">Adicionar pontos finais Azure</span><span class="sxs-lookup"><span data-stu-id="acc5e-175">Adding Azure Endpoints</span></span>

<span data-ttu-id="acc5e-176">Pontos finais Azure referenciam serviços alojados no Azure.</span><span class="sxs-lookup"><span data-stu-id="acc5e-176">Azure endpoints reference services hosted in Azure.</span></span> <span data-ttu-id="acc5e-177">São suportados dois tipos de pontos finais do Azure:</span><span class="sxs-lookup"><span data-stu-id="acc5e-177">Two types of Azure endpoints are supported:</span></span>

1. <span data-ttu-id="acc5e-178">Aplicações Web do Azure</span><span class="sxs-lookup"><span data-stu-id="acc5e-178">Azure Web Apps</span></span>
2. <span data-ttu-id="acc5e-179">Recursos PublicIpAddress do Azure (o que podem ser anexado tooa-Balanceador de carga ou uma máquina virtual NIC).</span><span class="sxs-lookup"><span data-stu-id="acc5e-179">Azure PublicIpAddress resources (which can be attached tooa load-balancer or a virtual machine NIC).</span></span> <span data-ttu-id="acc5e-180">Olá PublicIpAddress tem de ter um nome DNS atribuído toobe utilizado no Traffic Manager.</span><span class="sxs-lookup"><span data-stu-id="acc5e-180">hello PublicIpAddress must have a DNS name assigned toobe used in Traffic Manager.</span></span>

<span data-ttu-id="acc5e-181">Em cada caso:</span><span class="sxs-lookup"><span data-stu-id="acc5e-181">In each case:</span></span>

* <span data-ttu-id="acc5e-182">o serviço de Olá é especificado utilizando o parâmetro de 'targetResourceId' Olá de `Add-AzureRmTrafficManagerEndpointConfig` ou `New-AzureRmTrafficManagerEndpoint`.</span><span class="sxs-lookup"><span data-stu-id="acc5e-182">hello service is specified using hello 'targetResourceId' parameter of `Add-AzureRmTrafficManagerEndpointConfig` or `New-AzureRmTrafficManagerEndpoint`.</span></span>
* <span data-ttu-id="acc5e-183">Olá 'Target' e 'EndpointLocation' são implícito por Olá TargetResourceId.</span><span class="sxs-lookup"><span data-stu-id="acc5e-183">hello 'Target' and 'EndpointLocation' are implied by hello TargetResourceId.</span></span>
* <span data-ttu-id="acc5e-184">A especificação de Olá 'Peso' é opcional.</span><span class="sxs-lookup"><span data-stu-id="acc5e-184">Specifying hello 'Weight' is optional.</span></span> <span data-ttu-id="acc5e-185">Ponderações só são utilizadas se o perfil de Olá é o método de encaminhamento de tráfego do toouse configurado Olá 'Weighted'.</span><span class="sxs-lookup"><span data-stu-id="acc5e-185">Weights are only used if hello profile is configured toouse hello 'Weighted' traffic-routing method.</span></span> <span data-ttu-id="acc5e-186">Caso contrário, são ignorados.</span><span class="sxs-lookup"><span data-stu-id="acc5e-186">Otherwise, they are ignored.</span></span> <span data-ttu-id="acc5e-187">Se for especificado, o valor de Olá tem de ser um número entre 1 e 1000.</span><span class="sxs-lookup"><span data-stu-id="acc5e-187">If specified, hello value must be a number between 1 and 1000.</span></span> <span data-ttu-id="acc5e-188">valor predefinido de Olá é '1'.</span><span class="sxs-lookup"><span data-stu-id="acc5e-188">hello default value is '1'.</span></span>
* <span data-ttu-id="acc5e-189">Olá especificando 'Priority' é opcional.</span><span class="sxs-lookup"><span data-stu-id="acc5e-189">Specifying hello 'Priority' is optional.</span></span> <span data-ttu-id="acc5e-190">Prioridades só são utilizadas se o perfil de Olá é o método de encaminhamento de tráfego do toouse configurado Olá 'Priority'.</span><span class="sxs-lookup"><span data-stu-id="acc5e-190">Priorities are only used if hello profile is configured toouse hello 'Priority' traffic-routing method.</span></span> <span data-ttu-id="acc5e-191">Caso contrário, são ignorados.</span><span class="sxs-lookup"><span data-stu-id="acc5e-191">Otherwise, they are ignored.</span></span> <span data-ttu-id="acc5e-192">Os valores válidos são de 1 too1000 com valores mais baixos que indica uma prioridade mais alta.</span><span class="sxs-lookup"><span data-stu-id="acc5e-192">Valid values are from 1 too1000 with lower values indicating a higher priority.</span></span> <span data-ttu-id="acc5e-193">Se for especificado para um ponto final, tem de ser especificados para todos os pontos finais.</span><span class="sxs-lookup"><span data-stu-id="acc5e-193">If specified for one endpoint, they must be specified for all endpoints.</span></span> <span data-ttu-id="acc5e-194">Se for omitido, os valores predefinidos a partir de '1' são aplicados por ordem de Olá que estão listados pontos finais de Olá.</span><span class="sxs-lookup"><span data-stu-id="acc5e-194">If omitted, default values starting from '1' are applied in hello order that hello endpoints are listed.</span></span>

### <a name="example-1-adding-web-app-endpoints-using-add-azurermtrafficmanagerendpointconfig"></a><span data-ttu-id="acc5e-195">Exemplo 1: Adicionar pontos finais de aplicação Web utilizando`Add-AzureRmTrafficManagerEndpointConfig`</span><span class="sxs-lookup"><span data-stu-id="acc5e-195">Example 1: Adding Web App endpoints using `Add-AzureRmTrafficManagerEndpointConfig`</span></span>

<span data-ttu-id="acc5e-196">Neste exemplo, vamos criar um perfil de Gestor de tráfego e adicionar dois pontos finais de aplicação Web utilizando Olá `Add-AzureRmTrafficManagerEndpointConfig` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="acc5e-196">In this example, we create a Traffic Manager profile and add two Web App endpoints using hello `Add-AzureRmTrafficManagerEndpointConfig` cmdlet.</span></span>

```powershell
$profile = New-AzureRmTrafficManagerProfile -Name myprofile -ResourceGroupName MyRG -TrafficRoutingMethod Performance -RelativeDnsName myapp -Ttl 30 -MonitorProtocol HTTP -MonitorPort 80 -MonitorPath "/"
$webapp1 = Get-AzureRMWebApp -Name webapp1
Add-AzureRmTrafficManagerEndpointConfig -EndpointName webapp1ep -TrafficManagerProfile $profile -Type AzureEndpoints -TargetResourceId $webapp1.Id -EndpointStatus Enabled
$webapp2 = Get-AzureRMWebApp -Name webapp2
Add-AzureRmTrafficManagerEndpointConfig -EndpointName webapp2ep -TrafficManagerProfile $profile -Type AzureEndpoints -TargetResourceId $webapp2.Id -EndpointStatus Enabled
Set-AzureRmTrafficManagerProfile -TrafficManagerProfile $profile
```
### <a name="example-2-adding-a-publicipaddress-endpoint-using-new-azurermtrafficmanagerendpoint"></a><span data-ttu-id="acc5e-197">Exemplo 2: Adicionar um publicIpAddress utilizando o ponto final`New-AzureRmTrafficManagerEndpoint`</span><span class="sxs-lookup"><span data-stu-id="acc5e-197">Example 2: Adding a publicIpAddress endpoint using `New-AzureRmTrafficManagerEndpoint`</span></span>

<span data-ttu-id="acc5e-198">Neste exemplo, um recurso de endereço IP público é adicionado o perfil do Traffic Manager toohello.</span><span class="sxs-lookup"><span data-stu-id="acc5e-198">In this example, a public IP address resource is added toohello Traffic Manager profile.</span></span> <span data-ttu-id="acc5e-199">endereço IP público Olá tem de ter um nome DNS configurado e pode ser vinculado a qualquer um dos toohello NIC um VM ou tooa de Balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="acc5e-199">hello public IP address must have a DNS name configured, and can be bound either toohello NIC of a VM or tooa load balancer.</span></span>

```powershell
$ip = Get-AzureRmPublicIpAddress -Name MyPublicIP -ResourceGroupName MyRG
New-AzureRmTrafficManagerEndpoint -Name MyIpEndpoint -ProfileName MyProfile -ResourceGroupName MyRG -Type AzureEndpoints -TargetResourceId $ip.Id -EndpointStatus Enabled
```

## <a name="adding-external-endpoints"></a><span data-ttu-id="acc5e-200">Adicionar pontos finais externos</span><span class="sxs-lookup"><span data-stu-id="acc5e-200">Adding External Endpoints</span></span>

<span data-ttu-id="acc5e-201">O tráfego Manager utiliza pontos finais externos toodirect tráfego tooservices alojados fora do Azure.</span><span class="sxs-lookup"><span data-stu-id="acc5e-201">Traffic Manager uses external endpoints toodirect traffic tooservices hosted outside of Azure.</span></span> <span data-ttu-id="acc5e-202">Como com pontos finais do Azure, pontos finais externos podem ser adicionados a utilizar `Add-AzureRmTrafficManagerEndpointConfig` seguido `Set-AzureRmTrafficManagerProfile`, ou `New-AzureRMTrafficManagerEndpoint`.</span><span class="sxs-lookup"><span data-stu-id="acc5e-202">As with Azure endpoints, external endpoints can be added either using `Add-AzureRmTrafficManagerEndpointConfig` followed by `Set-AzureRmTrafficManagerProfile`, or `New-AzureRMTrafficManagerEndpoint`.</span></span>

<span data-ttu-id="acc5e-203">Quando especificar pontos finais externos:</span><span class="sxs-lookup"><span data-stu-id="acc5e-203">When specifying external endpoints:</span></span>

* <span data-ttu-id="acc5e-204">nome de domínio de ponto final de Olá tem de ser especificado utilizando o parâmetro de 'Target' Olá</span><span class="sxs-lookup"><span data-stu-id="acc5e-204">hello endpoint domain name must be specified using hello 'Target' parameter</span></span>
* <span data-ttu-id="acc5e-205">Se for utilizado Olá método de encaminhamento de tráfego 'Desempenho', é necessário o Olá 'EndpointLocation'.</span><span class="sxs-lookup"><span data-stu-id="acc5e-205">If hello 'Performance' traffic-routing method is used, hello 'EndpointLocation' is required.</span></span> <span data-ttu-id="acc5e-206">Caso contrário, é opcional.</span><span class="sxs-lookup"><span data-stu-id="acc5e-206">Otherwise it is optional.</span></span> <span data-ttu-id="acc5e-207">valor de Olá tem de ser um [nome da região do Azure válido](https://azure.microsoft.com/regions/).</span><span class="sxs-lookup"><span data-stu-id="acc5e-207">hello value must be a [valid Azure region name](https://azure.microsoft.com/regions/).</span></span>
* <span data-ttu-id="acc5e-208">Olá 'Importância' e 'Priority' é opcional.</span><span class="sxs-lookup"><span data-stu-id="acc5e-208">hello 'Weight' and 'Priority' are optional.</span></span>

### <a name="example-1-adding-external-endpoints-using-add-azurermtrafficmanagerendpointconfig-and-set-azurermtrafficmanagerprofile"></a><span data-ttu-id="acc5e-209">Exemplo 1: Adicionar pontos finais externos utilizando `Add-AzureRmTrafficManagerEndpointConfig` e`Set-AzureRmTrafficManagerProfile`</span><span class="sxs-lookup"><span data-stu-id="acc5e-209">Example 1: Adding external endpoints using `Add-AzureRmTrafficManagerEndpointConfig` and `Set-AzureRmTrafficManagerProfile`</span></span>

<span data-ttu-id="acc5e-210">Neste exemplo, vamos criar um perfil de Gestor de tráfego, adicionar dois pontos finais externos e consolidar as alterações de Olá.</span><span class="sxs-lookup"><span data-stu-id="acc5e-210">In this example, we create a Traffic Manager profile, add two external endpoints, and commit hello changes.</span></span>

```powershell
$profile = New-AzureRmTrafficManagerProfile -Name myprofile -ResourceGroupName MyRG -TrafficRoutingMethod Performance -RelativeDnsName myapp -Ttl 30 -MonitorProtocol HTTP -MonitorPort 80 -MonitorPath "/"
Add-AzureRmTrafficManagerEndpointConfig -EndpointName eu-endpoint -TrafficManagerProfile $profile -Type ExternalEndpoints -Target app-eu.contoso.com -EndpointLocation "North Europe" -EndpointStatus Enabled
Add-AzureRmTrafficManagerEndpointConfig -EndpointName us-endpoint -TrafficManagerProfile $profile -Type ExternalEndpoints -Target app-us.contoso.com -EndpointLocation "Central US" -EndpointStatus Enabled
Set-AzureRmTrafficManagerProfile -TrafficManagerProfile $profile
```

### <a name="example-2-adding-external-endpoints-using-new-azurermtrafficmanagerendpoint"></a><span data-ttu-id="acc5e-211">Exemplo 2: Adicionar pontos finais externos utilizando`New-AzureRmTrafficManagerEndpoint`</span><span class="sxs-lookup"><span data-stu-id="acc5e-211">Example 2: Adding external endpoints using `New-AzureRmTrafficManagerEndpoint`</span></span>

<span data-ttu-id="acc5e-212">Neste exemplo, vamos adicionar um perfil existente de tooan de ponto final externo.</span><span class="sxs-lookup"><span data-stu-id="acc5e-212">In this example, we add an external endpoint tooan existing profile.</span></span> <span data-ttu-id="acc5e-213">perfil de Olá for especificado utilizando nomes de grupos de recursos e perfil Olá.</span><span class="sxs-lookup"><span data-stu-id="acc5e-213">hello profile is specified using hello profile and resource group names.</span></span>

```powershell
New-AzureRmTrafficManagerEndpoint -Name eu-endpoint -ProfileName MyProfile -ResourceGroupName MyRG -Type ExternalEndpoints -Target app-eu.contoso.com -EndpointStatus Enabled
```

## <a name="adding-nested-endpoints"></a><span data-ttu-id="acc5e-214">Adicionar pontos finais de 'Nested'</span><span class="sxs-lookup"><span data-stu-id="acc5e-214">Adding 'Nested' endpoints</span></span>

<span data-ttu-id="acc5e-215">Cada perfil do Traffic Manager Especifica um único método de encaminhamento de tráfego.</span><span class="sxs-lookup"><span data-stu-id="acc5e-215">Each Traffic Manager profile specifies a single traffic-routing method.</span></span> <span data-ttu-id="acc5e-216">No entanto, existem cenários que necessitam de mais sofisticadas encaminhamento do tráfego de encaminhamento de Olá fornecido por um único perfil do Gestor de tráfego.</span><span class="sxs-lookup"><span data-stu-id="acc5e-216">However, there are scenarios that require more sophisticated traffic routing than hello routing provided by a single Traffic Manager profile.</span></span> <span data-ttu-id="acc5e-217">Podem aninhar vantagens Olá de toocombine de perfis do Gestor de tráfego de mais do que um método de encaminhamento de tráfego.</span><span class="sxs-lookup"><span data-stu-id="acc5e-217">You can nest Traffic Manager profiles toocombine hello benefits of more than one traffic-routing method.</span></span> <span data-ttu-id="acc5e-218">Perfis aninhados permitem-lhe toooverride Olá predefinido do Traffic Manager comportamento toosupport maior e mais complexas implementações de aplicações.</span><span class="sxs-lookup"><span data-stu-id="acc5e-218">Nested profiles allow you toooverride hello default Traffic Manager behavior toosupport larger and more complex application deployments.</span></span> <span data-ttu-id="acc5e-219">Para obter mais exemplos, consulte [perfis do Gestor de tráfego aninhada](traffic-manager-nested-profiles.md).</span><span class="sxs-lookup"><span data-stu-id="acc5e-219">For more detailed examples, see [Nested Traffic Manager profiles](traffic-manager-nested-profiles.md).</span></span>

<span data-ttu-id="acc5e-220">Pontos finais aninhados estão configurados no perfil de principal de Olá, com um tipo de ponto final específico, 'NestedEndpoints'.</span><span class="sxs-lookup"><span data-stu-id="acc5e-220">Nested endpoints are configured at hello parent profile, using a specific endpoint type, 'NestedEndpoints'.</span></span> <span data-ttu-id="acc5e-221">Quando especificar pontos finais aninhados:</span><span class="sxs-lookup"><span data-stu-id="acc5e-221">When specifying nested endpoints:</span></span>

* <span data-ttu-id="acc5e-222">ponto final de Olá tem de ser especificado utilizando o parâmetro de 'targetResourceId' Olá</span><span class="sxs-lookup"><span data-stu-id="acc5e-222">hello endpoint must be specified using hello 'targetResourceId' parameter</span></span>
* <span data-ttu-id="acc5e-223">Se for utilizado Olá método de encaminhamento de tráfego 'Desempenho', é necessário o Olá 'EndpointLocation'.</span><span class="sxs-lookup"><span data-stu-id="acc5e-223">If hello 'Performance' traffic-routing method is used, hello 'EndpointLocation' is required.</span></span> <span data-ttu-id="acc5e-224">Caso contrário, é opcional.</span><span class="sxs-lookup"><span data-stu-id="acc5e-224">Otherwise it is optional.</span></span> <span data-ttu-id="acc5e-225">valor de Olá tem de ser um [nome da região do Azure válido](http://azure.microsoft.com/regions/).</span><span class="sxs-lookup"><span data-stu-id="acc5e-225">hello value must be a [valid Azure region name](http://azure.microsoft.com/regions/).</span></span>
* <span data-ttu-id="acc5e-226">Olá 'Importância' e 'Priority' é opcional, como pontos finais do Azure.</span><span class="sxs-lookup"><span data-stu-id="acc5e-226">hello 'Weight' and 'Priority' are optional, as for Azure endpoints.</span></span>
* <span data-ttu-id="acc5e-227">parâmetro de 'MinChildEndpoints' Olá é opcional.</span><span class="sxs-lookup"><span data-stu-id="acc5e-227">hello 'MinChildEndpoints' parameter is optional.</span></span> <span data-ttu-id="acc5e-228">valor predefinido de Olá é '1'.</span><span class="sxs-lookup"><span data-stu-id="acc5e-228">hello default value is '1'.</span></span> <span data-ttu-id="acc5e-229">Se o número de Olá de pontos finais disponíveis está abaixo deste limiar, o perfil de principal de Olá considera perfil subordinado de Olá 'degradado' e diverts tráfego toohello outros pontos finais no perfil do Olá principal.</span><span class="sxs-lookup"><span data-stu-id="acc5e-229">If hello number of available endpoints falls below this threshold, hello parent profile considers hello child profile 'degraded' and diverts traffic toohello other endpoints in hello parent profile.</span></span>

### <a name="example-1-adding-nested-endpoints-using-add-azurermtrafficmanagerendpointconfig-and-set-azurermtrafficmanagerprofile"></a><span data-ttu-id="acc5e-230">Exemplo 1: Adicionar pontos finais aninhados utilizando `Add-AzureRmTrafficManagerEndpointConfig` e`Set-AzureRmTrafficManagerProfile`</span><span class="sxs-lookup"><span data-stu-id="acc5e-230">Example 1: Adding nested endpoints using `Add-AzureRmTrafficManagerEndpointConfig` and `Set-AzureRmTrafficManagerProfile`</span></span>

<span data-ttu-id="acc5e-231">Neste exemplo, vamos perfis principais e subordinados do novo Gestor de tráfego, adicionar subordinado Olá como um principal de toohello aninhada endpoint e consolidar alterações de Olá.</span><span class="sxs-lookup"><span data-stu-id="acc5e-231">In this example, we create new Traffic Manager child and parent profiles, add hello child as a nested endpoint toohello parent, and commit hello changes.</span></span>

```powershell
$child = New-AzureRmTrafficManagerProfile -Name child -ResourceGroupName MyRG -TrafficRoutingMethod Priority -RelativeDnsName child -Ttl 30 -MonitorProtocol HTTP -MonitorPort 80 -MonitorPath "/"
$parent = New-AzureRmTrafficManagerProfile -Name parent -ResourceGroupName MyRG -TrafficRoutingMethod Performance -RelativeDnsName parent -Ttl 30 -MonitorProtocol HTTP -MonitorPort 80 -MonitorPath "/"
Add-AzureRmTrafficManagerEndpointConfig -EndpointName child-endpoint -TrafficManagerProfile $parent -Type NestedEndpoints -TargetResourceId $child.Id -EndpointStatus Enabled -EndpointLocation "North Europe" -MinChildEndpoints 2
Set-AzureRmTrafficManagerProfile -TrafficManagerProfile $profile
```

<span data-ttu-id="acc5e-232">De uma forma abreviada neste exemplo, não foi possível adicionar não quaisquer outros pontos finais toohello subordinado ou principal perfis.</span><span class="sxs-lookup"><span data-stu-id="acc5e-232">For brevity in this example, we did not add any other endpoints toohello child or parent profiles.</span></span>

### <a name="example-2-adding-nested-endpoints-using-new-azurermtrafficmanagerendpoint"></a><span data-ttu-id="acc5e-233">Exemplo 2: Adicionar pontos finais aninhados utilizando`New-AzureRmTrafficManagerEndpoint`</span><span class="sxs-lookup"><span data-stu-id="acc5e-233">Example 2: Adding nested endpoints using `New-AzureRmTrafficManagerEndpoint`</span></span>

<span data-ttu-id="acc5e-234">Neste exemplo, vamos adicionar um perfil subordinado existente como um perfil existente de principal do ponto final aninhada tooan.</span><span class="sxs-lookup"><span data-stu-id="acc5e-234">In this example, we add an existing child profile as a nested endpoint tooan existing parent profile.</span></span> <span data-ttu-id="acc5e-235">perfil de Olá for especificado utilizando nomes de grupos de recursos e perfil Olá.</span><span class="sxs-lookup"><span data-stu-id="acc5e-235">hello profile is specified using hello profile and resource group names.</span></span>

```powershell
$child = Get-AzureRmTrafficManagerEndpoint -Name child -ResourceGroupName MyRG
New-AzureRmTrafficManagerEndpoint -Name child-endpoint -ProfileName parent -ResourceGroupName MyRG -Type NestedEndpoints -TargetResourceId $child.Id -EndpointStatus Enabled -EndpointLocation "North Europe" -MinChildEndpoints 2
```

## <a name="update-a-traffic-manager-endpoint"></a><span data-ttu-id="acc5e-236">Atualizar um ponto final do Gestor de tráfego</span><span class="sxs-lookup"><span data-stu-id="acc5e-236">Update a Traffic Manager Endpoint</span></span>

<span data-ttu-id="acc5e-237">Existem duas formas tooupdate um ponto final do Traffic Manager existente:</span><span class="sxs-lookup"><span data-stu-id="acc5e-237">There are two ways tooupdate an existing Traffic Manager endpoint:</span></span>

1. <span data-ttu-id="acc5e-238">Obter a utilização de perfil de Gestor de tráfego de Olá `Get-AzureRmTrafficManagerProfile`, atualizar as propriedades do ponto final de Olá no perfil de Olá e confirmar as alterações de Olá utilizando `Set-AzureRmTrafficManagerProfile`.</span><span class="sxs-lookup"><span data-stu-id="acc5e-238">Get hello Traffic Manager profile using `Get-AzureRmTrafficManagerProfile`, update hello endpoint properties within hello profile, and commit hello changes using `Set-AzureRmTrafficManagerProfile`.</span></span> <span data-ttu-id="acc5e-239">Este método tem a vantagem de Olá de que está a ser capaz de tooupdate mais do que um ponto final numa única operação.</span><span class="sxs-lookup"><span data-stu-id="acc5e-239">This method has hello advantage of being able tooupdate more than one endpoint in a single operation.</span></span>
2. <span data-ttu-id="acc5e-240">Obter através de ponto final de Gestor de tráfego de Olá `Get-AzureRmTrafficManagerEndpoint`, atualizar propriedades do ponto final de Olá e confirmar as alterações de Olá utilizando `Set-AzureRmTrafficManagerEndpoint`.</span><span class="sxs-lookup"><span data-stu-id="acc5e-240">Get hello Traffic Manager endpoint using `Get-AzureRmTrafficManagerEndpoint`, update hello endpoint properties, and commit hello changes using `Set-AzureRmTrafficManagerEndpoint`.</span></span> <span data-ttu-id="acc5e-241">Este método é mais simples, uma vez que não requer a indexação numa matriz de pontos finais de Olá no perfil de Olá.</span><span class="sxs-lookup"><span data-stu-id="acc5e-241">This method is simpler, since it does not require indexing into hello Endpoints array in hello profile.</span></span>

### <a name="example-1-updating-endpoints-using-get-azurermtrafficmanagerprofile-and-set-azurermtrafficmanagerprofile"></a><span data-ttu-id="acc5e-242">Exemplo 1: Atualizar pontos finais utilizando `Get-AzureRmTrafficManagerProfile` e`Set-AzureRmTrafficManagerProfile`</span><span class="sxs-lookup"><span data-stu-id="acc5e-242">Example 1: Updating endpoints using `Get-AzureRmTrafficManagerProfile` and `Set-AzureRmTrafficManagerProfile`</span></span>

<span data-ttu-id="acc5e-243">Neste exemplo, vamos modificar prioridade Olá em dois pontos finais dentro de um perfil existente.</span><span class="sxs-lookup"><span data-stu-id="acc5e-243">In this example, we modify hello priority on two endpoints within an existing profile.</span></span>

```powershell
$profile = Get-AzureRmTrafficManagerProfile -Name myprofile -ResourceGroupName MyRG
$profile.Endpoints[0].Priority = 2
$profile.Endpoints[1].Priority = 1
Set-AzureRmTrafficManagerProfile -TrafficManagerProfile $profile
```

### <a name="example-2-updating-an-endpoint-using-get-azurermtrafficmanagerendpoint-and-set-azurermtrafficmanagerendpoint"></a><span data-ttu-id="acc5e-244">Exemplo 2: Atualizar um ponto final utilizando `Get-AzureRmTrafficManagerEndpoint` e`Set-AzureRmTrafficManagerEndpoint`</span><span class="sxs-lookup"><span data-stu-id="acc5e-244">Example 2: Updating an endpoint using `Get-AzureRmTrafficManagerEndpoint` and `Set-AzureRmTrafficManagerEndpoint`</span></span>

<span data-ttu-id="acc5e-245">Neste exemplo, vamos modificar ponderação Olá de um único ponto final num perfil existente.</span><span class="sxs-lookup"><span data-stu-id="acc5e-245">In this example, we modify hello weight of a single endpoint in an existing profile.</span></span>

```powershell
$endpoint = Get-AzureRmTrafficManagerEndpoint -Name myendpoint -ProfileName myprofile -ResourceGroupName MyRG -Type ExternalEndpoints
$endpoint.Weight = 20
Set-AzureRmTrafficManagerEndpoint -TrafficManagerEndpoint $endpoint
```

## <a name="enabling-and-disabling-endpoints-and-profiles"></a><span data-ttu-id="acc5e-246">Ativar e desativar pontos finais e perfis</span><span class="sxs-lookup"><span data-stu-id="acc5e-246">Enabling and Disabling Endpoints and Profiles</span></span>

<span data-ttu-id="acc5e-247">Gestor de tráfego permite que os pontos finais individuais toobe ativados e desativados, bem como permitir que a ativação e a desativação dos perfis de todos.</span><span class="sxs-lookup"><span data-stu-id="acc5e-247">Traffic Manager allows individual endpoints toobe enabled and disabled, as well as allowing enabling and disabling of entire profiles.</span></span>
<span data-ttu-id="acc5e-248">Estas alterações podem ser efetuadas pelos recursos de ponto final ou o perfil de Olá obter/atualizar/definição.</span><span class="sxs-lookup"><span data-stu-id="acc5e-248">These changes can be made by getting/updating/setting hello endpoint or profile resources.</span></span> <span data-ttu-id="acc5e-249">toostreamline estas operações comuns, são também suportadas através de cmdlets dedicados.</span><span class="sxs-lookup"><span data-stu-id="acc5e-249">toostreamline these common operations, they are also supported via dedicated cmdlets.</span></span>

### <a name="example-1-enabling-and-disabling-a-traffic-manager-profile"></a><span data-ttu-id="acc5e-250">Exemplo 1: Ativar e desativar um perfil do Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="acc5e-250">Example 1: Enabling and disabling a Traffic Manager profile</span></span>

<span data-ttu-id="acc5e-251">tooenable um perfil do Traffic Manager, utilize `Enable-AzureRmTrafficManagerProfile`.</span><span class="sxs-lookup"><span data-stu-id="acc5e-251">tooenable a Traffic Manager profile, use `Enable-AzureRmTrafficManagerProfile`.</span></span> <span data-ttu-id="acc5e-252">perfil de Olá pode ser especificada utilizando um objeto de perfil.</span><span class="sxs-lookup"><span data-stu-id="acc5e-252">hello profile can be specified using a profile object.</span></span> <span data-ttu-id="acc5e-253">Olá perfil pode ser transmitido um objeto através do pipeline de Olá ou utilizando Olá '-TrafficManagerProfile' parâmetro.</span><span class="sxs-lookup"><span data-stu-id="acc5e-253">hello profile object can be passed via hello pipeline or by using hello '-TrafficManagerProfile' parameter.</span></span> <span data-ttu-id="acc5e-254">Neste exemplo, especificamos perfil Olá pelo nome do grupo de recursos e perfil Olá.</span><span class="sxs-lookup"><span data-stu-id="acc5e-254">In this example, we specify hello profile by hello profile and resource group name.</span></span>

```powershell
Enable-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyResourceGroup
```

<span data-ttu-id="acc5e-255">toodisable um perfil de Gestor de tráfego:</span><span class="sxs-lookup"><span data-stu-id="acc5e-255">toodisable a Traffic Manager profile:</span></span>

```powershell
Disable-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyResourceGroup
```

<span data-ttu-id="acc5e-256">Olá desativar AzureRmTrafficManagerProfile cmdlet solicita a confirmação.</span><span class="sxs-lookup"><span data-stu-id="acc5e-256">hello Disable-AzureRmTrafficManagerProfile cmdlet prompts for confirmation.</span></span> <span data-ttu-id="acc5e-257">Esta linha de comandos pode ser suprimida utilizando Olá '-Force' parâmetro.</span><span class="sxs-lookup"><span data-stu-id="acc5e-257">This prompt can be suppressed using hello '-Force' parameter.</span></span>

### <a name="example-2-enabling-and-disabling-a-traffic-manager-endpoint"></a><span data-ttu-id="acc5e-258">Exemplo 2: Ativar e desativar um ponto final do Gestor de tráfego</span><span class="sxs-lookup"><span data-stu-id="acc5e-258">Example 2: Enabling and disabling a Traffic Manager endpoint</span></span>

<span data-ttu-id="acc5e-259">utilizar um ponto final do Gestor de tráfego, de tooenable `Enable-AzureRmTrafficManagerEndpoint`.</span><span class="sxs-lookup"><span data-stu-id="acc5e-259">tooenable a Traffic Manager endpoint, use `Enable-AzureRmTrafficManagerEndpoint`.</span></span> <span data-ttu-id="acc5e-260">Existem dois ponto final do Olá de toospecify formas</span><span class="sxs-lookup"><span data-stu-id="acc5e-260">There are two ways toospecify hello endpoint</span></span>

1. <span data-ttu-id="acc5e-261">Utilizando um objeto de TrafficManagerEndpoint transmitido através do pipeline de Olá ou Olá '-TrafficManagerEndpoint' parâmetro</span><span class="sxs-lookup"><span data-stu-id="acc5e-261">Using a TrafficManagerEndpoint object passed via hello pipeline or using hello '-TrafficManagerEndpoint' parameter</span></span>
2. <span data-ttu-id="acc5e-262">Utilizar o nome do ponto final Olá, tipo de ponto final, o nome de perfil e nome do grupo de recursos:</span><span class="sxs-lookup"><span data-stu-id="acc5e-262">Using hello endpoint name, endpoint type, profile name, and resource group name:</span></span>

```powershell
Enable-AzureRmTrafficManagerEndpoint -Name MyEndpoint -Type AzureEndpoints -ProfileName MyProfile -ResourceGroupName MyRG
```

<span data-ttu-id="acc5e-263">Da mesma forma, toodisable um ponto final do Gestor de tráfego:</span><span class="sxs-lookup"><span data-stu-id="acc5e-263">Similarly, toodisable a Traffic Manager endpoint:</span></span>

```powershell
Disable-AzureRmTrafficManagerEndpoint -Name MyEndpoint -Type AzureEndpoints -ProfileName MyProfile -ResourceGroupName MyRG -Force
```

<span data-ttu-id="acc5e-264">Tal como com `Disable-AzureRmTrafficManagerProfile`, Olá `Disable-AzureRmTrafficManagerEndpoint` cmdlet solicita a confirmação.</span><span class="sxs-lookup"><span data-stu-id="acc5e-264">As with `Disable-AzureRmTrafficManagerProfile`, hello `Disable-AzureRmTrafficManagerEndpoint` cmdlet prompts for confirmation.</span></span> <span data-ttu-id="acc5e-265">Esta linha de comandos pode ser suprimida utilizando Olá '-Force' parâmetro.</span><span class="sxs-lookup"><span data-stu-id="acc5e-265">This prompt can be suppressed using hello '-Force' parameter.</span></span>

## <a name="delete-a-traffic-manager-endpoint"></a><span data-ttu-id="acc5e-266">Eliminar um ponto final do Gestor de tráfego</span><span class="sxs-lookup"><span data-stu-id="acc5e-266">Delete a Traffic Manager Endpoint</span></span>

<span data-ttu-id="acc5e-267">pontos finais individuais tooremove, utilize Olá `Remove-AzureRmTrafficManagerEndpoint` cmdlet:</span><span class="sxs-lookup"><span data-stu-id="acc5e-267">tooremove individual endpoints, use hello `Remove-AzureRmTrafficManagerEndpoint` cmdlet:</span></span>

```powershell
Remove-AzureRmTrafficManagerEndpoint -Name MyEndpoint -Type AzureEndpoints -ProfileName MyProfile -ResourceGroupName MyRG
```

<span data-ttu-id="acc5e-268">Este cmdlet solicita a confirmação.</span><span class="sxs-lookup"><span data-stu-id="acc5e-268">This cmdlet prompts for confirmation.</span></span> <span data-ttu-id="acc5e-269">Esta linha de comandos pode ser suprimida utilizando Olá '-Force' parâmetro.</span><span class="sxs-lookup"><span data-stu-id="acc5e-269">This prompt can be suppressed using hello '-Force' parameter.</span></span>

## <a name="delete-a-traffic-manager-profile"></a><span data-ttu-id="acc5e-270">Eliminar um perfil do Gestor de tráfego</span><span class="sxs-lookup"><span data-stu-id="acc5e-270">Delete a Traffic Manager Profile</span></span>

<span data-ttu-id="acc5e-271">toodelete um perfil do Traffic Manager, utilize Olá `Remove-AzureRmTrafficManagerProfile` cmdlet, especificando os nomes de grupos de recursos e perfil Olá:</span><span class="sxs-lookup"><span data-stu-id="acc5e-271">toodelete a Traffic Manager profile, use hello `Remove-AzureRmTrafficManagerProfile` cmdlet, specifying hello profile and resource group names:</span></span>

```powershell
Remove-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyRG [-Force]
```

<span data-ttu-id="acc5e-272">Este cmdlet solicita a confirmação.</span><span class="sxs-lookup"><span data-stu-id="acc5e-272">This cmdlet prompts for confirmation.</span></span> <span data-ttu-id="acc5e-273">Esta linha de comandos pode ser suprimida utilizando Olá '-Force' parâmetro.</span><span class="sxs-lookup"><span data-stu-id="acc5e-273">This prompt can be suppressed using hello '-Force' parameter.</span></span>

<span data-ttu-id="acc5e-274">Olá perfil toobe eliminado também pode ser especificada utilizando um objeto de perfil:</span><span class="sxs-lookup"><span data-stu-id="acc5e-274">hello profile toobe deleted can also be specified using a profile object:</span></span>

```powershell
$profile = Get-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyRG
Remove-AzureRmTrafficManagerProfile -TrafficManagerProfile $profile [-Force]
```

<span data-ttu-id="acc5e-275">Também pode ser ligada esta sequência:</span><span class="sxs-lookup"><span data-stu-id="acc5e-275">This sequence can also be piped:</span></span>

```powershell
Get-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyRG | Remove-AzureRmTrafficManagerProfile [-Force]
```

## <a name="next-steps"></a><span data-ttu-id="acc5e-276">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="acc5e-276">Next steps</span></span>

[<span data-ttu-id="acc5e-277">Gestor de tráfego de monitorização</span><span class="sxs-lookup"><span data-stu-id="acc5e-277">Traffic Manager monitoring</span></span>](traffic-manager-monitoring.md)

[<span data-ttu-id="acc5e-278">Considerações de desempenho para o Gestor de Tráfego</span><span class="sxs-lookup"><span data-stu-id="acc5e-278">Traffic Manager performance considerations</span></span>](traffic-manager-performance-considerations.md)
