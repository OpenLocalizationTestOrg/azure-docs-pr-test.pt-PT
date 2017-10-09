---
title: "subscrição aaaAzure limites e quotas | Microsoft Docs"
description: "Fornece uma lista de subscrição do Azure comuns e limites de serviço, quotas e restrições. Isto inclui informações sobre como tooincrease limita juntamente com os valores máximos."
services: 
documentationcenter: 
author: rothja
manager: jeffreyg
editor: 
tags: billing
ms.assetid: 60d848f9-ff26-496e-a5ec-ccf92ad7d125
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: byvinyal
ms.openlocfilehash: a754d56124520791254ab8f1729808f0750ff222
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-subscription-and-service-limits-quotas-and-constraints"></a><span data-ttu-id="062b6-104">Subscrição do Azure e limites de serviço, quotas e restrições</span><span class="sxs-lookup"><span data-stu-id="062b6-104">Azure subscription and service limits, quotas, and constraints</span></span>
<span data-ttu-id="062b6-105">Este documento apresenta alguns dos limites de Microsoft Azure mais comuns Olá, que também por vezes, são chamados quotas.</span><span class="sxs-lookup"><span data-stu-id="062b6-105">This document lists some of hello most common Microsoft Azure limits, which are also sometimes called quotas.</span></span> <span data-ttu-id="062b6-106">Este documento atualmente não abrange todos os serviços do Azure.</span><span class="sxs-lookup"><span data-stu-id="062b6-106">This document doesn't currently cover all Azure services.</span></span> <span data-ttu-id="062b6-107">Ao longo do tempo, a lista de Olá será expandida e atualizado toocover mais da plataforma de Olá.</span><span class="sxs-lookup"><span data-stu-id="062b6-107">Over time, hello list will be expanded and updated toocover more of hello platform.</span></span>

<span data-ttu-id="062b6-108">Visite [descrição geral de preços do Azure](https://azure.microsoft.com/pricing/) toolearn mais informações sobre preços do Azure.</span><span class="sxs-lookup"><span data-stu-id="062b6-108">Please visit [Azure Pricing Overview](https://azure.microsoft.com/pricing/) toolearn more about Azure pricing.</span></span> <span data-ttu-id="062b6-109">Aqui, pode estimar os custos com Olá [Calculadora de preços](https://azure.microsoft.com/pricing/calculator/) ou, visitando Olá preços da página de detalhes para um serviço (por exemplo, [VMs do Windows](https://azure.microsoft.com/pricing/details/virtual-machines/#Windows)).</span><span class="sxs-lookup"><span data-stu-id="062b6-109">There, you can estimate your costs using hello [Pricing Calculator](https://azure.microsoft.com/pricing/calculator/) or by visiting hello pricing details page for a service (for example, [Windows VMs](https://azure.microsoft.com/pricing/details/virtual-machines/#Windows)).</span></span> <span data-ttu-id="062b6-110">Para sugestões toohelp gerir os custos, consulte [evitar custos inesperados com faturação do Azure e custos de gestão](billing/billing-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="062b6-110">For tips toohelp manage your costs, see [Prevent unexpected costs with Azure billing and cost management](billing/billing-getting-started.md).</span></span>

> [!NOTE]
> <span data-ttu-id="062b6-111">Se quiser limite de Olá tooraise ou quota acima Olá **limite predefinido**, [abrir um pedido de suporte online do cliente, sem encargos](azure-supportability/resource-manager-core-quotas-request.md).</span><span class="sxs-lookup"><span data-stu-id="062b6-111">If you want tooraise hello limit or quota above hello **Default Limit**, [open an online customer support request at no charge](azure-supportability/resource-manager-core-quotas-request.md).</span></span> <span data-ttu-id="062b6-112">Olá limites não podem ser gerados acima Olá **limite máximo** valor mostrado no Olá tabelas a seguir.</span><span class="sxs-lookup"><span data-stu-id="062b6-112">hello limits can't be raised above hello **Maximum Limit** value shown in hello following tables.</span></span> <span data-ttu-id="062b6-113">Se não houver nenhuma **limite máximo** coluna, em seguida, recursos de Olá não tem limites ajustável.</span><span class="sxs-lookup"><span data-stu-id="062b6-113">If there is no **Maximum Limit** column, then hello resource doesn't have adjustable limits.</span></span> 
> 
> <span data-ttu-id="062b6-114">As subscrições de avaliação gratuitas não são elegíveis para o limite ou aumenta a quota.</span><span class="sxs-lookup"><span data-stu-id="062b6-114">Free Trial subscriptions are not eligible for limit or quota increases.</span></span> <span data-ttu-id="062b6-115">Se tiver uma versão de avaliação gratuita, pode atualizar tooa [pay as you go](https://azure.microsoft.com/offers/ms-azr-0003p/) subscrição.</span><span class="sxs-lookup"><span data-stu-id="062b6-115">If you have a Free Trial, you can upgrade tooa [Pay-As-You-Go](https://azure.microsoft.com/offers/ms-azr-0003p/) subscription.</span></span> <span data-ttu-id="062b6-116">Para obter mais informações, consulte [atualizar avaliação gratuita do Azure tooPay-como-,-ir](billing/billing-upgrade-azure-subscription.md).</span><span class="sxs-lookup"><span data-stu-id="062b6-116">For more information, see [Upgrade Azure Free Trial tooPay-As-You-Go](billing/billing-upgrade-azure-subscription.md).</span></span>
> 

## <a name="limits-and-hello-azure-resource-manager"></a><span data-ttu-id="062b6-117">Limites e Olá do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="062b6-117">Limits and hello Azure Resource Manager</span></span>
<span data-ttu-id="062b6-118">É agora possível toocombine vários recursos do Azure no tooa único grupo de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="062b6-118">It is now possible toocombine multiple Azure resources in tooa single Azure Resource Group.</span></span> <span data-ttu-id="062b6-119">Quando utilizar grupos de recursos, os limites que uma vez foram global passará a ser geridos a um nível regional com Olá do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="062b6-119">When using Resource Groups, limits that once were global become managed at a regional level with hello Azure Resource Manager.</span></span> <span data-ttu-id="062b6-120">Para obter mais informações sobre grupos de recursos do Azure, consulte [descrição geral do Azure Resource Manager](azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="062b6-120">For more information about Azure Resource Groups, see [Azure Resource Manager overview](azure-resource-manager/resource-group-overview.md).</span></span>

<span data-ttu-id="062b6-121">Nos limites de Olá abaixo, uma nova tabela foi adicionado tooreflect quaisquer diferenças nos limites ao utilizar Olá do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="062b6-121">In hello limits below, a new table has been added tooreflect any differences in limits when using hello Azure Resource Manager.</span></span> <span data-ttu-id="062b6-122">Por exemplo, não há um **limites de subscrição** tabela e um **limites de subscrição - Azure Resource Manager** tabela.</span><span class="sxs-lookup"><span data-stu-id="062b6-122">For example, there is a **Subscription Limits** table and a **Subscription Limits - Azure Resource Manager** table.</span></span> <span data-ttu-id="062b6-123">Quando um limite aplica-se cenários tooboth, só é apresentada na primeira tabela de Olá.</span><span class="sxs-lookup"><span data-stu-id="062b6-123">When a limit applies tooboth scenarios, it is only shown in hello first table.</span></span> <span data-ttu-id="062b6-124">A menos que indicado em contrário, os limites são globais em todas as regiões.</span><span class="sxs-lookup"><span data-stu-id="062b6-124">Unless otherwise indicated, limits are global across all regions.</span></span>

> [!NOTE]
> <span data-ttu-id="062b6-125">É importante tooemphasize que quotas para os recursos em grupos de recursos do Azure estão por regiões acessível através da sua subscrição e não estão por subscrição, as quotas de gestão do serviço de Olá.</span><span class="sxs-lookup"><span data-stu-id="062b6-125">It is important tooemphasize that quotas for resources in Azure Resource Groups are per-region accessible by your subscription, and are not per-subscription, as hello service management quotas are.</span></span> <span data-ttu-id="062b6-126">Vamos utilizar quotas de núcleos como exemplo.</span><span class="sxs-lookup"><span data-stu-id="062b6-126">Let's use core quotas as an example.</span></span> <span data-ttu-id="062b6-127">Se precisar de toorequest aumentar uma quota com suporte para núcleos, terá toodecide como vários núcleos pretende toouse em que regiões e, em seguida, efetue um pedido específico para o grupo de recursos do Azure principal quotas para quantidades de Olá e regiões que pretende.</span><span class="sxs-lookup"><span data-stu-id="062b6-127">If you need toorequest a quota increase with support for cores, you need toodecide how many cores you want toouse in which regions, and then make a specific request for Azure Resource Group core quotas for hello amounts and regions that you want.</span></span> <span data-ttu-id="062b6-128">Por conseguinte, se precisar de toouse 30 núcleos na Europa Ocidental toorun existe; a sua aplicação especificamente o utilizador deve pedir 30 núcleos na Europa Ocidental.</span><span class="sxs-lookup"><span data-stu-id="062b6-128">Therefore, if you need toouse 30 cores in West Europe toorun your application there; you should specifically request 30 cores in West Europe.</span></span> <span data-ttu-id="062b6-129">Mas não terá uma quota de núcleos aumentam a qualquer outra região – apenas Europa Ocidental terão a quota de núcleos de 30 de Olá.</span><span class="sxs-lookup"><span data-stu-id="062b6-129">But you will not have a core quota increase in any other region -- only West Europe will have hello 30-core quota.</span></span>
> <!-- -->
> <span data-ttu-id="062b6-130">Como resultado, pode encontrá-lo útil tooconsider decidir o seu quotas do grupo de recursos do Azure necessita toobe para a carga de trabalho em qualquer uma região e pedido que culmina em cada região na qual estiver a considerar implementação.</span><span class="sxs-lookup"><span data-stu-id="062b6-130">As a result, you may find it useful tooconsider deciding what your Azure Resource Group quotas need toobe for your workload in any one region, and request that amount in each region into which you are considering deployment.</span></span> <span data-ttu-id="062b6-131">Consulte [resolução de problemas de implementação](resource-manager-common-deployment-errors.md) para obter mais ajuda a detetar as quotas atuais para regiões específicas.</span><span class="sxs-lookup"><span data-stu-id="062b6-131">See [troubleshooting deployment issues](resource-manager-common-deployment-errors.md) for more help discovering your current quotas for specific regions.</span></span>
> 
> 

## <a name="service-specific-limits"></a><span data-ttu-id="062b6-132">Limites de serviço específicos</span><span class="sxs-lookup"><span data-stu-id="062b6-132">Service-specific limits</span></span>
* [<span data-ttu-id="062b6-133">Active Directory</span><span class="sxs-lookup"><span data-stu-id="062b6-133">Active Directory</span></span>](#active-directory-limits)
* [<span data-ttu-id="062b6-134">Gestão de API</span><span class="sxs-lookup"><span data-stu-id="062b6-134">API Management</span></span>](#api-management-limits)
* [<span data-ttu-id="062b6-135">Serviço de Aplicações</span><span class="sxs-lookup"><span data-stu-id="062b6-135">App Service</span></span>](#app-service-limits)
* [<span data-ttu-id="062b6-136">Gateway de Aplicação</span><span class="sxs-lookup"><span data-stu-id="062b6-136">Application Gateway</span></span>](#application-gateway-limits)
* [<span data-ttu-id="062b6-137">Application Insights</span><span class="sxs-lookup"><span data-stu-id="062b6-137">Application Insights</span></span>](#application-insights-limits)
* [<span data-ttu-id="062b6-138">Automatização</span><span class="sxs-lookup"><span data-stu-id="062b6-138">Automation</span></span>](#automation-limits)
* [<span data-ttu-id="062b6-139">BD do Cosmos para o Azure</span><span class="sxs-lookup"><span data-stu-id="062b6-139">Azure Cosmos DB</span></span>](#azure-cosmos-db-limits)
* [<span data-ttu-id="062b6-140">Grelha de eventos do Azure</span><span class="sxs-lookup"><span data-stu-id="062b6-140">Azure Event Grid</span></span>](#azure-event-grid-limits)
* [<span data-ttu-id="062b6-141">Cache de Redis do Azure</span><span class="sxs-lookup"><span data-stu-id="062b6-141">Azure Redis Cache</span></span>](#azure-redis-cache-limits)
* [<span data-ttu-id="062b6-142">Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="062b6-142">Azure RemoteApp</span></span>](#azure-remoteapp-limits)
* [<span data-ttu-id="062b6-143">Cópia de segurança</span><span class="sxs-lookup"><span data-stu-id="062b6-143">Backup</span></span>](#backup-limits)
* [<span data-ttu-id="062b6-144">Batch</span><span class="sxs-lookup"><span data-stu-id="062b6-144">Batch</span></span>](#batch-limits)
* [<span data-ttu-id="062b6-145">Serviços BizTalk</span><span class="sxs-lookup"><span data-stu-id="062b6-145">BizTalk Services</span></span>](#biztalk-services-limits)
* [<span data-ttu-id="062b6-146">CDN</span><span class="sxs-lookup"><span data-stu-id="062b6-146">CDN</span></span>](#cdn-limits)
* [<span data-ttu-id="062b6-147">Serviços Cloud</span><span class="sxs-lookup"><span data-stu-id="062b6-147">Cloud Services</span></span>](#cloud-services-limits)
* [<span data-ttu-id="062b6-148">Container Instances</span><span class="sxs-lookup"><span data-stu-id="062b6-148">Container Instances</span></span>](#container-instances-limits)
* [<span data-ttu-id="062b6-149">Data Factory</span><span class="sxs-lookup"><span data-stu-id="062b6-149">Data Factory</span></span>](#data-factory-limits)
* [<span data-ttu-id="062b6-150">Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="062b6-150">Data Lake Analytics</span></span>](#data-lake-analytics-limits)
* [<span data-ttu-id="062b6-151">Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="062b6-151">Data Lake Store</span></span>](#data-lake-store-limits)
* [<span data-ttu-id="062b6-152">DNS</span><span class="sxs-lookup"><span data-stu-id="062b6-152">DNS</span></span>](#dns-limits)
* [<span data-ttu-id="062b6-153">Hubs de Eventos</span><span class="sxs-lookup"><span data-stu-id="062b6-153">Event Hubs</span></span>](#event-hubs-limits)
* [<span data-ttu-id="062b6-154">Hub IoT</span><span class="sxs-lookup"><span data-stu-id="062b6-154">IoT Hub</span></span>](#iot-hub-limits)
* [<span data-ttu-id="062b6-155">Cofre de Chaves</span><span class="sxs-lookup"><span data-stu-id="062b6-155">Key Vault</span></span>](#key-vault-limits)
* [<span data-ttu-id="062b6-156">Análise de registo / Operational Insights</span><span class="sxs-lookup"><span data-stu-id="062b6-156">Log Analytics / Operational Insights</span></span>](#log-analytics-limits)
* [<span data-ttu-id="062b6-157">Serviços de Multimédia</span><span class="sxs-lookup"><span data-stu-id="062b6-157">Media Services</span></span>](#media-services-limits)
* [<span data-ttu-id="062b6-158">Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="062b6-158">Mobile Engagement</span></span>](#mobile-engagement-limits)
* [<span data-ttu-id="062b6-159">Serviços móveis</span><span class="sxs-lookup"><span data-stu-id="062b6-159">Mobile Services</span></span>](#mobile-services-limits)
* [<span data-ttu-id="062b6-160">Monitorizar</span><span class="sxs-lookup"><span data-stu-id="062b6-160">Monitor</span></span>](#monitor-limits)
* [<span data-ttu-id="062b6-161">Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="062b6-161">Multi-Factor Authentication</span></span>](#multi-factor-authentication)
* [<span data-ttu-id="062b6-162">Redes</span><span class="sxs-lookup"><span data-stu-id="062b6-162">Networking</span></span>](#networking-limits)
* [<span data-ttu-id="062b6-163">Observador de rede</span><span class="sxs-lookup"><span data-stu-id="062b6-163">Network Watcher</span></span>](#network-watcher-limits)
* [<span data-ttu-id="062b6-164">Serviço de Hub de notificação</span><span class="sxs-lookup"><span data-stu-id="062b6-164">Notification Hub Service</span></span>](#notification-hub-service-limits)
* [<span data-ttu-id="062b6-165">Grupo de Recursos</span><span class="sxs-lookup"><span data-stu-id="062b6-165">Resource Group</span></span>](#resource-group-limits)
* [<span data-ttu-id="062b6-166">Scheduler</span><span class="sxs-lookup"><span data-stu-id="062b6-166">Scheduler</span></span>](#scheduler-limits)
* [<span data-ttu-id="062b6-167">Pesquisa</span><span class="sxs-lookup"><span data-stu-id="062b6-167">Search</span></span>](#search-limits)
* [<span data-ttu-id="062b6-168">Service Bus</span><span class="sxs-lookup"><span data-stu-id="062b6-168">Service Bus</span></span>](#service-bus-limits)
* [<span data-ttu-id="062b6-169">Site Recovery</span><span class="sxs-lookup"><span data-stu-id="062b6-169">Site Recovery</span></span>](#site-recovery-limits)
* [<span data-ttu-id="062b6-170">Base de Dados SQL</span><span class="sxs-lookup"><span data-stu-id="062b6-170">SQL Database</span></span>](#sql-database-limits)
* [<span data-ttu-id="062b6-171">Armazenamento</span><span class="sxs-lookup"><span data-stu-id="062b6-171">Storage</span></span>](#storage-limits)
* [<span data-ttu-id="062b6-172">Sistema StorSimple</span><span class="sxs-lookup"><span data-stu-id="062b6-172">StorSimple System</span></span>](#storsimple-system-limits)
* [<span data-ttu-id="062b6-173">Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="062b6-173">Stream Analytics</span></span>](#stream-analytics-limits)
* [<span data-ttu-id="062b6-174">Subscrição</span><span class="sxs-lookup"><span data-stu-id="062b6-174">Subscription</span></span>](#subscription-limits)
* [<span data-ttu-id="062b6-175">Gestor de Tráfego</span><span class="sxs-lookup"><span data-stu-id="062b6-175">Traffic Manager</span></span>](#traffic-manager-limits)
* [<span data-ttu-id="062b6-176">Máquinas Virtuais</span><span class="sxs-lookup"><span data-stu-id="062b6-176">Virtual Machines</span></span>](#virtual-machines-limits)
* [<span data-ttu-id="062b6-177">Conjuntos de Dimensionamento de Máquinas Virtuais</span><span class="sxs-lookup"><span data-stu-id="062b6-177">Virtual Machine Scale Sets</span></span>](#virtual-machine-scale-sets-limits)

### <a name="subscription-limits"></a><span data-ttu-id="062b6-178">Limites de subscrição</span><span class="sxs-lookup"><span data-stu-id="062b6-178">Subscription limits</span></span>
#### <a name="subscription-limits"></a><span data-ttu-id="062b6-179">Limites de subscrição</span><span class="sxs-lookup"><span data-stu-id="062b6-179">Subscription limits</span></span>
[!INCLUDE [azure-subscription-limits](../includes/azure-subscription-limits.md)]

#### <a name="subscription-limits---azure-resource-manager"></a><span data-ttu-id="062b6-180">Limites de subscrição - Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="062b6-180">Subscription limits - Azure Resource Manager</span></span>
<span data-ttu-id="062b6-181">Olá limites a seguir aplicam-se ao utilizar Olá do Azure Resource Manager e grupos de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="062b6-181">hello following limits apply when using hello Azure Resource Manager and Azure Resource Groups.</span></span> <span data-ttu-id="062b6-182">Limites de utilização não mudaram com Olá do Azure Resource Manager não estão listados abaixo.</span><span class="sxs-lookup"><span data-stu-id="062b6-182">Limits that have not changed with hello Azure Resource Manager are not listed below.</span></span> <span data-ttu-id="062b6-183">Consulte a tabela anterior toohello esses limites de.</span><span class="sxs-lookup"><span data-stu-id="062b6-183">Please refer toohello previous table for those limits.</span></span>

<span data-ttu-id="062b6-184">Para obter informações sobre como lidar com limites de pedidos de Gestor de recursos, consulte [limitação Gestor de recursos pedidos](resource-manager-request-limits.md).</span><span class="sxs-lookup"><span data-stu-id="062b6-184">For information about handling limits on Resource Manager requests, see [Throttling Resource Manager requests](resource-manager-request-limits.md).</span></span>

[!INCLUDE [azure-subscription-limits-azure-resource-manager](../includes/azure-subscription-limits-azure-resource-manager.md)]

### <a name="resource-group-limits"></a><span data-ttu-id="062b6-185">Limites do grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="062b6-185">Resource Group limits</span></span>
[!INCLUDE [azure-resource-groups-limits](../includes/azure-resource-groups-limits.md)]

### <a name="virtual-machines-limits"></a><span data-ttu-id="062b6-186">Limites de máquinas virtuais</span><span class="sxs-lookup"><span data-stu-id="062b6-186">Virtual Machines limits</span></span>
#### <a name="virtual-machine-limits"></a><span data-ttu-id="062b6-187">Limites de máquinas virtuais</span><span class="sxs-lookup"><span data-stu-id="062b6-187">Virtual Machine limits</span></span>
[!INCLUDE [azure-virtual-machines-limits](../includes/azure-virtual-machines-limits.md)]

#### <a name="virtual-machines-limits---azure-resource-manager"></a><span data-ttu-id="062b6-188">Limites de máquinas virtuais - Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="062b6-188">Virtual Machines limits - Azure Resource Manager</span></span>
<span data-ttu-id="062b6-189">Olá limites a seguir aplicam-se ao utilizar Olá do Azure Resource Manager e grupos de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="062b6-189">hello following limits apply when using hello Azure Resource Manager and Azure Resource Groups.</span></span> <span data-ttu-id="062b6-190">Limites de utilização não mudaram com Olá do Azure Resource Manager não estão listados abaixo.</span><span class="sxs-lookup"><span data-stu-id="062b6-190">Limits that have not changed with hello Azure Resource Manager are not listed below.</span></span> <span data-ttu-id="062b6-191">Consulte a tabela anterior toohello esses limites de.</span><span class="sxs-lookup"><span data-stu-id="062b6-191">Please refer toohello previous table for those limits.</span></span>

[!INCLUDE [azure-virtual-machines-limits-azure-resource-manager](../includes/azure-virtual-machines-limits-azure-resource-manager.md)]

### <a name="virtual-machine-scale-sets-limits"></a><span data-ttu-id="062b6-192">Limites de conjuntos de dimensionamento de máquina virtual</span><span class="sxs-lookup"><span data-stu-id="062b6-192">Virtual Machine Scale Sets limits</span></span>
[!INCLUDE [virtual-machine-scale-sets-limits](../includes/azure-virtual-machine-scale-sets-limits.md)]

### <a name="container-instances-limits"></a><span data-ttu-id="062b6-193">Os limites de instâncias de contentor</span><span class="sxs-lookup"><span data-stu-id="062b6-193">Container Instances Limits</span></span>
[!INCLUDE [container-instances-limits](../includes/container-instances-limits.md)]

### <a name="networking-limits"></a><span data-ttu-id="062b6-194">Limites de rede</span><span class="sxs-lookup"><span data-stu-id="062b6-194">Networking limits</span></span>
[!INCLUDE [expressroute-limits](../includes/expressroute-limits.md)]

#### <a name="networking-limits"></a><span data-ttu-id="062b6-195">Limites de rede</span><span class="sxs-lookup"><span data-stu-id="062b6-195">Networking limits</span></span>
[!INCLUDE [azure-virtual-network-limits](../includes/azure-virtual-network-limits.md)]

#### <a name="application-gateway-limits"></a><span data-ttu-id="062b6-196">Limites de Gateway de aplicação</span><span class="sxs-lookup"><span data-stu-id="062b6-196">Application Gateway limits</span></span>
[!INCLUDE [application-gateway-limits](../includes/application-gateway-limits.md)]

#### <a name="network-watcher-limits"></a><span data-ttu-id="062b6-197">Limites de observador de rede</span><span class="sxs-lookup"><span data-stu-id="062b6-197">Network Watcher limits</span></span>
[!INCLUDE [network-watcher-limits](../includes/network-watcher-limits.md)]

#### <a name="traffic-manager-limits"></a><span data-ttu-id="062b6-198">Limites do Gestor de tráfego</span><span class="sxs-lookup"><span data-stu-id="062b6-198">Traffic Manager limits</span></span>
[!INCLUDE [traffic-manager-limits](../includes/traffic-manager-limits.md)]

#### <a name="dns-limits"></a><span data-ttu-id="062b6-199">Limites DNS</span><span class="sxs-lookup"><span data-stu-id="062b6-199">DNS limits</span></span>
[!INCLUDE [dns-limits](../includes/dns-limits.md)]

### <a name="storage-limits"></a><span data-ttu-id="062b6-200">Limites de armazenamento</span><span class="sxs-lookup"><span data-stu-id="062b6-200">Storage limits</span></span>
<span data-ttu-id="062b6-201">Para obter detalhes adicionais sobre os limites de conta de armazenamento, consulte [metas de desempenho e escalabilidade do Storage do Azure](storage/common/storage-scalability-targets.md).</span><span class="sxs-lookup"><span data-stu-id="062b6-201">For additional details on storage account limits, see [Azure Storage Scalability and Performance Targets](storage/common/storage-scalability-targets.md).</span></span>
<!--like # storage accts --> 
#### <a name="storage-service-limits"></a><span data-ttu-id="062b6-202">Limites de serviço de armazenamento</span><span class="sxs-lookup"><span data-stu-id="062b6-202">Storage Service limits</span></span>
[!INCLUDE [azure-storage-limits](../includes/azure-storage-limits.md)]

<!-- conceptual info about disk limits -- applies toounmanaged and managed -->
#### <a name="virtual-machine-disk-limits"></a><span data-ttu-id="062b6-203">Limites de disco de máquina virtual</span><span class="sxs-lookup"><span data-stu-id="062b6-203">Virtual machine disk limits</span></span> 
[!INCLUDE [azure-storage-limits-vm-disks](../includes/azure-storage-limits-vm-disks.md)]

<span data-ttu-id="062b6-204">Consulte [tamanhos de Máquina Virtual](virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) para obter detalhes adicionais.</span><span class="sxs-lookup"><span data-stu-id="062b6-204">See [Virtual machine sizes](virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for additional details.</span></span>

#### <a name="managed-virtual-machine-disks"></a><span data-ttu-id="062b6-205">Discos de máquinas de virtuais gerido</span><span class="sxs-lookup"><span data-stu-id="062b6-205">Managed virtual machine disks</span></span>

[!INCLUDE [azure-storage-limits-vm-disks-managed](../includes/azure-storage-limits-vm-disks-managed.md)]

#### <a name="unmanaged-virtual-machine-disks"></a><span data-ttu-id="062b6-206">Discos de máquinas de virtuais não geridos</span><span class="sxs-lookup"><span data-stu-id="062b6-206">Unmanaged virtual machine disks</span></span>

[!INCLUDE [azure-storage-limits-vm-disks-standard](../includes/azure-storage-limits-vm-disks-standard.md)]

[!INCLUDE [azure-storage-limits-vm-disks-premium](../includes/azure-storage-limits-vm-disks-premium.md)]

#### <a name="storage-resource-provider-limits"></a><span data-ttu-id="062b6-207">Limites de fornecedor de recursos de armazenamento</span><span class="sxs-lookup"><span data-stu-id="062b6-207">Storage Resource Provider limits</span></span>
[!INCLUDE [azure-storage-limits-azure-resource-manager](../includes/azure-storage-limits-azure-resource-manager.md)]

### <a name="cloud-services-limits"></a><span data-ttu-id="062b6-208">Limites de serviços cloud</span><span class="sxs-lookup"><span data-stu-id="062b6-208">Cloud Services limits</span></span>
[!INCLUDE [azure-cloud-services-limits](../includes/azure-cloud-services-limits.md)]

### <a name="app-service-limits"></a><span data-ttu-id="062b6-209">Limites de serviço de aplicações</span><span class="sxs-lookup"><span data-stu-id="062b6-209">App Service limits</span></span>
<span data-ttu-id="062b6-210">seguinte Olá que limites do App Service incluem os limites de Web Apps, Mobile Apps, API Apps e Logic Apps.</span><span class="sxs-lookup"><span data-stu-id="062b6-210">hello following App Service limits include limits for Web Apps, Mobile Apps, API Apps, and Logic Apps.</span></span>

[!INCLUDE [azure-websites-limits](../includes/azure-websites-limits.md)]

### <a name="scheduler-limits"></a><span data-ttu-id="062b6-211">Limites de programador</span><span class="sxs-lookup"><span data-stu-id="062b6-211">Scheduler limits</span></span>
[!INCLUDE [scheduler-limits-table](../includes/scheduler-limits-table.md)]

### <a name="batch-limits"></a><span data-ttu-id="062b6-212">Limites do batch</span><span class="sxs-lookup"><span data-stu-id="062b6-212">Batch limits</span></span>
[!INCLUDE [azure-batch-limits](../includes/azure-batch-limits.md)]

### <a name="biztalk-services-limits"></a><span data-ttu-id="062b6-213">Limites de serviços BizTalk</span><span class="sxs-lookup"><span data-stu-id="062b6-213">BizTalk Services limits</span></span>
<span data-ttu-id="062b6-214">Olá tabela seguinte mostra os limites de Olá dos Biztalk Services do Azure.</span><span class="sxs-lookup"><span data-stu-id="062b6-214">hello following table shows hello limits for Azure Biztalk Services.</span></span>

[!INCLUDE [biztalk-services-service-limits](../includes/biztalk-services-service-limits.md)]

### <a name="azure-cosmos-db-limits"></a><span data-ttu-id="062b6-215">Limites de Cosmos BD do Azure</span><span class="sxs-lookup"><span data-stu-id="062b6-215">Azure Cosmos DB limits</span></span>
<span data-ttu-id="062b6-216">BD do Cosmos do Azure é uma base de dados de escala global em que débito e o armazenamento pode ser expandido toohandle que requer a sua aplicação.</span><span class="sxs-lookup"><span data-stu-id="062b6-216">Azure Cosmos DB is a global scale database in which throughput and storage can be scaled toohandle whatever your application requires.</span></span> <span data-ttu-id="062b6-217">Se tiver alguma questão sobre dimensionamento Olá fornece a base de dados do Azure Cosmos, envie um e-mail tooaskcosmosdb@microsoft.com.</span><span class="sxs-lookup"><span data-stu-id="062b6-217">If you have any questions about hello scale Azure Cosmos DB provides, please send email tooaskcosmosdb@microsoft.com.</span></span>

### <a name="mobile-engagement-limits"></a><span data-ttu-id="062b6-218">Limites de Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="062b6-218">Mobile Engagement limits</span></span>
[!INCLUDE [azure-mobile-engagement-limits](../includes/azure-mobile-engagement-limits.md)]

### <a name="search-limits"></a><span data-ttu-id="062b6-219">Limites de pesquisa</span><span class="sxs-lookup"><span data-stu-id="062b6-219">Search limits</span></span>
<span data-ttu-id="062b6-220">Escalões de preços determinam a capacidade de Olá e limites do seu serviço de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="062b6-220">Pricing tiers determine hello capacity and limits of your search service.</span></span> <span data-ttu-id="062b6-221">As camadas incluem:</span><span class="sxs-lookup"><span data-stu-id="062b6-221">Tiers include:</span></span>

* <span data-ttu-id="062b6-222">*Livre* serviço multi-inquilino, partilhado com outros subscritores do Azure, concebida para avaliação e de desenvolvimento pequeno projetos.</span><span class="sxs-lookup"><span data-stu-id="062b6-222">*Free* multi-tenant service, shared with other Azure subscribers, intended for evaluation and small development projects.</span></span>
* <span data-ttu-id="062b6-223">*Básico* disponibiliza recursos informáticos dedicados para cargas de trabalho de produção em escala mais pequena, segurança de réplicas toothree para cargas de trabalho de consulta altamente disponível.</span><span class="sxs-lookup"><span data-stu-id="062b6-223">*Basic* provides dedicated computing resources for production workloads at a smaller scale, with up toothree replicas for highly available query workloads.</span></span>
* <span data-ttu-id="062b6-224">*Padrão (S1, S2, S3, S3 alta densidade)* é para cargas de trabalho de produção maior.</span><span class="sxs-lookup"><span data-stu-id="062b6-224">*Standard (S1, S2, S3, S3 High Density)* is for larger production workloads.</span></span> <span data-ttu-id="062b6-225">Vários níveis existem no escalão standard Olá para que possa escolher uma configuração de recursos que melhor de adeque ao seu perfil de carga de trabalho.</span><span class="sxs-lookup"><span data-stu-id="062b6-225">Multiple levels exist within hello standard tier so that you can choose a resource configuration that best matches your workload profile.</span></span>

<span data-ttu-id="062b6-226">**Limites por subscrição**</span><span class="sxs-lookup"><span data-stu-id="062b6-226">**Limits per subscription**</span></span>

[!INCLUDE [azure-search-limits-per-subscription](../includes/azure-search-limits-per-subscription.md)]

<span data-ttu-id="062b6-227">**Limites por serviço de pesquisa**</span><span class="sxs-lookup"><span data-stu-id="062b6-227">**Limits per search service**</span></span>

[!INCLUDE [azure-search-limits-per-service](../includes/azure-search-limits-per-service.md)]

<span data-ttu-id="062b6-228">toolearn mais informações sobre limites de um nível mais granular, tais como o tamanho do documento, consultas por segundo, chaves, pedidos e respostas, consulte [Service limites na Azure Search](search/search-limits-quotas-capacity.md).</span><span class="sxs-lookup"><span data-stu-id="062b6-228">toolearn more about limits on a more granular level, such as document size, queries per second, keys, requests, and responses, see [Service limits in Azure Search](search/search-limits-quotas-capacity.md).</span></span>

### <a name="media-services-limits"></a><span data-ttu-id="062b6-229">Limites de Media Services</span><span class="sxs-lookup"><span data-stu-id="062b6-229">Media Services limits</span></span>
[!INCLUDE [azure-mediaservices-limits](../includes/azure-mediaservices-limits.md)]

### <a name="cdn-limits"></a><span data-ttu-id="062b6-230">Limites CDN</span><span class="sxs-lookup"><span data-stu-id="062b6-230">CDN limits</span></span>
[!INCLUDE [cdn-limits](../includes/cdn-limits.md)]

### <a name="mobile-services-limits"></a><span data-ttu-id="062b6-231">Limites de Mobile Services</span><span class="sxs-lookup"><span data-stu-id="062b6-231">Mobile Services limits</span></span>
[!INCLUDE [mobile-services-limits](../includes/mobile-services-limits.md)]

### <a name="monitor-limits"></a><span data-ttu-id="062b6-232">Limites de monitor</span><span class="sxs-lookup"><span data-stu-id="062b6-232">Monitor limits</span></span>
[!INCLUDE [monitoring-limits](../includes/monitoring-limits.md)]

### <a name="notification-hub-service-limits"></a><span data-ttu-id="062b6-233">Limites de serviço de Hub de notificação</span><span class="sxs-lookup"><span data-stu-id="062b6-233">Notification Hub Service limits</span></span>
[!INCLUDE [notification-hub-limits](../includes/notification-hub-limits.md)]

### <a name="event-hubs-limits"></a><span data-ttu-id="062b6-234">Limites de Hubs de eventos</span><span class="sxs-lookup"><span data-stu-id="062b6-234">Event Hubs limits</span></span>
[!INCLUDE [azure-servicebus-limits](../includes/event-hubs-limits.md)]

### <a name="service-bus-limits"></a><span data-ttu-id="062b6-235">Limites de Service Bus</span><span class="sxs-lookup"><span data-stu-id="062b6-235">Service Bus limits</span></span>
[!INCLUDE [azure-servicebus-limits](../includes/service-bus-quotas-table.md)]

### <a name="iot-hub-limits"></a><span data-ttu-id="062b6-236">Limites do IoT Hub</span><span class="sxs-lookup"><span data-stu-id="062b6-236">IoT Hub limits</span></span>
[!INCLUDE [azure-iothub-limits](../includes/iot-hub-limits.md)]

### <a name="data-factory-limits"></a><span data-ttu-id="062b6-237">Limites de fábrica de dados</span><span class="sxs-lookup"><span data-stu-id="062b6-237">Data Factory limits</span></span>
[!INCLUDE [azure-data-factory-limits](../includes/azure-data-factory-limits.md)]

### <a name="data-lake-analytics-limits"></a><span data-ttu-id="062b6-238">Limites de análise do Data Lake</span><span class="sxs-lookup"><span data-stu-id="062b6-238">Data Lake Analytics limits</span></span>
[!INCLUDE [azure-data-lake-analytics-limits](../includes/azure-data-lake-analytics-limits.md)]

### <a name="data-lake-store-limits"></a><span data-ttu-id="062b6-239">Limites de data Lake Store</span><span class="sxs-lookup"><span data-stu-id="062b6-239">Data Lake Store limits</span></span>
[!INCLUDE [azure-data-lake-store-limits](../includes/azure-data-lake-store-limits.md)]

### <a name="stream-analytics-limits"></a><span data-ttu-id="062b6-240">Limita o do Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="062b6-240">Stream Analytics limits</span></span>
[!INCLUDE [stream-analytics-limits-table](../includes/stream-analytics-limits-table.md)]

### <a name="active-directory-limits"></a><span data-ttu-id="062b6-241">Limita do Active Directory</span><span class="sxs-lookup"><span data-stu-id="062b6-241">Active Directory limits</span></span>
[!INCLUDE [AAD-service-limits](../includes/active-directory-service-limits-include.md)]

### <a name="azure-event-grid-limits"></a><span data-ttu-id="062b6-242">Limites de grelha de eventos do Azure</span><span class="sxs-lookup"><span data-stu-id="062b6-242">Azure Event Grid limits</span></span>
[!INCLUDE [event-grid-limits](../includes/event-grid-limits.md)]

### <a name="azure-remoteapp-limits"></a><span data-ttu-id="062b6-243">Limita o Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="062b6-243">Azure RemoteApp limits</span></span>
[!INCLUDE [azure-remoteapp-limits](../includes/azure-remoteapp-limits.md)]

### <a name="storsimple-system-limits"></a><span data-ttu-id="062b6-244">Limites de sistema do StorSimple</span><span class="sxs-lookup"><span data-stu-id="062b6-244">StorSimple System limits</span></span>
[!INCLUDE [storsimple-limits-table](../includes/storsimple-limits-table.md)]

### <a name="log-analytics-limits"></a><span data-ttu-id="062b6-245">Limita a análise de registos</span><span class="sxs-lookup"><span data-stu-id="062b6-245">Log Analytics limits</span></span>
[!INCLUDE [operational-insights-limits](../includes/operational-insights-limits.md)]

### <a name="backup-limits"></a><span data-ttu-id="062b6-246">Limites de cópia de segurança</span><span class="sxs-lookup"><span data-stu-id="062b6-246">Backup limits</span></span>
[!INCLUDE [azure-backup-limits](../includes/azure-backup-limits.md)]

### <a name="site-recovery-limits"></a><span data-ttu-id="062b6-247">Limites do Site Recovery</span><span class="sxs-lookup"><span data-stu-id="062b6-247">Site Recovery limits</span></span>
[!INCLUDE [site-recovery-limits](../includes/site-recovery-limits.md)]

### <a name="application-insights-limits"></a><span data-ttu-id="062b6-248">Limites do Application Insights</span><span class="sxs-lookup"><span data-stu-id="062b6-248">Application Insights limits</span></span>
[!INCLUDE [application-insights-limits](../includes/application-insights-limits.md)]

### <a name="api-management-limits"></a><span data-ttu-id="062b6-249">Limites de API Management</span><span class="sxs-lookup"><span data-stu-id="062b6-249">API Management limits</span></span>
[!INCLUDE [api-management-service-limits](../includes/api-management-service-limits.md)]

### <a name="azure-redis-cache-limits"></a><span data-ttu-id="062b6-250">Limites de Cache de Redis do Azure</span><span class="sxs-lookup"><span data-stu-id="062b6-250">Azure Redis Cache limits</span></span>
[!INCLUDE [redis-cache-service-limits](../includes/redis-cache-service-limits.md)]

### <a name="key-vault-limits"></a><span data-ttu-id="062b6-251">Limites do Cofre de chaves</span><span class="sxs-lookup"><span data-stu-id="062b6-251">Key Vault limits</span></span>
[!INCLUDE [key-vault-limits](../includes/key-vault-limits.md)]

### <a name="multi-factor-authentication"></a><span data-ttu-id="062b6-252">Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="062b6-252">Multi-Factor Authentication</span></span>
[!INCLUDE [azure-mfa-service-limits](../includes/azure-mfa-service-limits.md)]

### <a name="automation-limits"></a><span data-ttu-id="062b6-253">Limites de automatização</span><span class="sxs-lookup"><span data-stu-id="062b6-253">Automation limits</span></span>
[!INCLUDE [automation-limits](../includes/azure-automation-service-limits.md)]

### <a name="sql-database-limits"></a><span data-ttu-id="062b6-254">Limites de base de dados SQL</span><span class="sxs-lookup"><span data-stu-id="062b6-254">SQL Database limits</span></span>
<span data-ttu-id="062b6-255">Para os limites de base de dados SQL, consulte [dos limites de recursos de base de dados do SQL Server](sql-database/sql-database-resource-limits.md).</span><span class="sxs-lookup"><span data-stu-id="062b6-255">For SQL Database limits, see [SQL Database Resource Limits](sql-database/sql-database-resource-limits.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="062b6-256">Consultar também</span><span class="sxs-lookup"><span data-stu-id="062b6-256">See also</span></span>
[<span data-ttu-id="062b6-257">Compreender os limites do Azure e aumenta</span><span class="sxs-lookup"><span data-stu-id="062b6-257">Understanding Azure Limits and Increases</span></span>](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/)

[<span data-ttu-id="062b6-258">Máquina virtual e tamanhos do serviço em nuvem do Azure</span><span class="sxs-lookup"><span data-stu-id="062b6-258">Virtual Machine and Cloud Service Sizes for Azure</span></span>](virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[<span data-ttu-id="062b6-259">Tamanhos de serviços Cloud</span><span class="sxs-lookup"><span data-stu-id="062b6-259">Sizes for Cloud Services</span></span>](cloud-services/cloud-services-sizes-specs.md)

