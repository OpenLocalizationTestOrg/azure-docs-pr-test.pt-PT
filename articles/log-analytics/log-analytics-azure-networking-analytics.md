---
title: "aaaAzure solução de análise de redes no Log Analytics | Microsoft Docs"
description: "Pode utilizar Olá solução de análise de redes do Azure nos registos de grupo de segurança de rede do Azure tooreview análise de registos e registos do Gateway de aplicação do Azure."
services: log-analytics
documentationcenter: 
author: richrundmsft
manager: ewinner
editor: 
ms.assetid: 66a3b8a1-6c55-4533-9538-cad60c18f28b
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/09/2017
ms.author: richrund
ms.openlocfilehash: 3674189786bacccc82e6708e78f14c92178e6676
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-networking-monitoring-solutions-in-log-analytics"></a><span data-ttu-id="5d5f4-103">Soluções de análise de registos de monitorização da rede do Azure</span><span class="sxs-lookup"><span data-stu-id="5d5f4-103">Azure networking monitoring solutions in Log Analytics</span></span>

<span data-ttu-id="5d5f4-104">Análise de registos oferece Olá seguintes soluções para monitorização as redes:</span><span class="sxs-lookup"><span data-stu-id="5d5f4-104">Log Analytics offers hello following solutions for monitoring your networks:</span></span>
* <span data-ttu-id="5d5f4-105">Monitor de desempenho de rede (NPM) para</span><span class="sxs-lookup"><span data-stu-id="5d5f4-105">Network Performance Monitor (NPM) to</span></span>
 * <span data-ttu-id="5d5f4-106">Estado de funcionamento do monitor Olá da sua rede</span><span class="sxs-lookup"><span data-stu-id="5d5f4-106">Monitor hello health of your network</span></span>
* <span data-ttu-id="5d5f4-107">Tooreview de análise de Gateway de aplicação do Azure</span><span class="sxs-lookup"><span data-stu-id="5d5f4-107">Azure Application Gateway analytics tooreview</span></span>
 * <span data-ttu-id="5d5f4-108">Registos de Gateway de aplicação do Azure</span><span class="sxs-lookup"><span data-stu-id="5d5f4-108">Azure Application Gateway logs</span></span>
 * <span data-ttu-id="5d5f4-109">Métricas de Gateway de aplicação do Azure</span><span class="sxs-lookup"><span data-stu-id="5d5f4-109">Azure Application Gateway metrics</span></span>
* <span data-ttu-id="5d5f4-110">Tooreview de análise do grupo de segurança de rede do Azure</span><span class="sxs-lookup"><span data-stu-id="5d5f4-110">Azure Network Security Group analytics tooreview</span></span>
 * <span data-ttu-id="5d5f4-111">Registos do grupo de segurança de rede do Azure</span><span class="sxs-lookup"><span data-stu-id="5d5f4-111">Azure Network Security Group logs</span></span>

## <a name="network-performance-monitor-npm"></a><span data-ttu-id="5d5f4-112">Monitor de desempenho de rede (NPM)</span><span class="sxs-lookup"><span data-stu-id="5d5f4-112">Network Performance Monitor (NPM)</span></span>

<span data-ttu-id="5d5f4-113">Olá [Monitor de desempenho de rede](log-analytics-network-performance-monitor.md) solução de gestão é uma solução, que monitoriza o estado de funcionamento de Olá, disponibilidade e acessibilidade de redes de monitorização de rede.</span><span class="sxs-lookup"><span data-stu-id="5d5f4-113">hello [Network Performance Monitor](log-analytics-network-performance-monitor.md) management solution is a network monitoring solution, that monitors hello health, availability and reachability of networks.</span></span>  <span data-ttu-id="5d5f4-114">É utilizado toomonitor conectividade entre:</span><span class="sxs-lookup"><span data-stu-id="5d5f4-114">It is used toomonitor connectivity between:</span></span>

* <span data-ttu-id="5d5f4-115">Nuvem pública e no local</span><span class="sxs-lookup"><span data-stu-id="5d5f4-115">Public cloud and on-premises</span></span>
* <span data-ttu-id="5d5f4-116">Os centros de dados e localizações de utilizador (sucursais)</span><span class="sxs-lookup"><span data-stu-id="5d5f4-116">Data centers and user locations (branch offices)</span></span>
* <span data-ttu-id="5d5f4-117">Sub-redes alojar várias camadas de uma aplicação de várias camadas.</span><span class="sxs-lookup"><span data-stu-id="5d5f4-117">Subnets hosting various tiers of a multi-tiered application.</span></span>

<span data-ttu-id="5d5f4-118">Para obter mais informações, consulte [Monitor de desempenho de rede](log-analytics-network-performance-monitor.md).</span><span class="sxs-lookup"><span data-stu-id="5d5f4-118">For more information, see [Network Performance Monitor](log-analytics-network-performance-monitor.md).</span></span>

## <a name="azure-application-gateway-and-network-security-group-analytics"></a><span data-ttu-id="5d5f4-119">Análise de Gateway de aplicação e o grupo de segurança de rede do Azure</span><span class="sxs-lookup"><span data-stu-id="5d5f4-119">Azure Application Gateway and Network Security Group analytics</span></span>
<span data-ttu-id="5d5f4-120">soluções de Olá toouse:</span><span class="sxs-lookup"><span data-stu-id="5d5f4-120">toouse hello solutions:</span></span>
1. <span data-ttu-id="5d5f4-121">Adicionar tooLog de solução de gestão de Olá, a análise e</span><span class="sxs-lookup"><span data-stu-id="5d5f4-121">Add hello management solution tooLog Analytics, and</span></span>
2. <span data-ttu-id="5d5f4-122">Ative o diagnóstico toodirect Olá diagnóstico tooa Log Analytics área de trabalho.</span><span class="sxs-lookup"><span data-stu-id="5d5f4-122">Enable diagnostics toodirect hello diagnostics tooa Log Analytics workspace.</span></span> <span data-ttu-id="5d5f4-123">Não é necessário toowrite Olá registos tooAzure o Blob storage.</span><span class="sxs-lookup"><span data-stu-id="5d5f4-123">It is not necessary toowrite hello logs tooAzure Blob storage.</span></span>

<span data-ttu-id="5d5f4-124">Pode ativar os diagnósticos e solução correspondente Olá para uma ou ambas Gateway de aplicação e grupos de segurança de rede.</span><span class="sxs-lookup"><span data-stu-id="5d5f4-124">You can enable diagnostics and hello corresponding solution for either one or both of Application Gateway and Networking Security Groups.</span></span>

<span data-ttu-id="5d5f4-125">Se não ativar o registo de diagnóstico para um tipo de recurso específico, mas instalar solução Olá, painéis de dashboard Olá para esse recurso em branco e apresentam uma mensagem de erro.</span><span class="sxs-lookup"><span data-stu-id="5d5f4-125">If you do not enable diagnostic logging for a particular resource type, but install hello solution, hello dashboard blades for that resource are blank and display an error message.</span></span>

> [!NOTE]
> <span data-ttu-id="5d5f4-126">Em Janeiro de 2017, Olá suportados forma de envio de registos de grupos de segurança de rede e Gateways de aplicação tooLog que Analytics foi alterado.</span><span class="sxs-lookup"><span data-stu-id="5d5f4-126">In January 2017, hello supported way of sending logs from Application Gateways and Network Security Groups tooLog Analytics changed.</span></span> <span data-ttu-id="5d5f4-127">Se vir Olá **análise de rede do Azure (preterido)** solução, consulte demasiado[migrar de solução de análise de redes de antiga Olá](#migrating-from-the-old-networking-analytics-solution) para obter os passos precisa de toofollow.</span><span class="sxs-lookup"><span data-stu-id="5d5f4-127">If you see hello **Azure Networking Analytics (deprecated)** solution, refer too[migrating from hello old Networking Analytics solution](#migrating-from-the-old-networking-analytics-solution) for steps you need toofollow.</span></span>
>
>

## <a name="review-azure-networking-data-collection-details"></a><span data-ttu-id="5d5f4-128">Reveja os detalhes de recolha de dados de rede do Azure</span><span class="sxs-lookup"><span data-stu-id="5d5f4-128">Review Azure networking data collection details</span></span>
<span data-ttu-id="5d5f4-129">análise de Gateway de aplicação do Azure Olá e soluções de gestão de análise de grupo de segurança de rede Olá recolher registos de diagnóstico diretamente a partir de grupos de segurança de rede e Gateways de aplicação do Azure.</span><span class="sxs-lookup"><span data-stu-id="5d5f4-129">hello Azure Application Gateway analytics and hello Network Security Group analytics management solutions collect diagnostics logs directly from Azure Application Gateways and Network Security Groups.</span></span> <span data-ttu-id="5d5f4-130">Não é necessário toowrite Olá registos tooAzure o Blob storage e sem agente é necessário para a recolha de dados.</span><span class="sxs-lookup"><span data-stu-id="5d5f4-130">It is not necessary toowrite hello logs tooAzure Blob storage and no agent is required for data collection.</span></span>

<span data-ttu-id="5d5f4-131">Olá tabela seguinte mostra os métodos de recolha de dados e outros detalhes sobre como os dados são recolhidos para análise do grupo de segurança de rede de Olá e de análise de Gateway de aplicação do Azure.</span><span class="sxs-lookup"><span data-stu-id="5d5f4-131">hello following table shows data collection methods and other details about how data is collected for Azure Application Gateway analytics and hello Network Security Group analytics.</span></span>

| <span data-ttu-id="5d5f4-132">Plataforma</span><span class="sxs-lookup"><span data-stu-id="5d5f4-132">Platform</span></span> | <span data-ttu-id="5d5f4-133">Direcionar o agente</span><span class="sxs-lookup"><span data-stu-id="5d5f4-133">Direct agent</span></span> | <span data-ttu-id="5d5f4-134">Agente do System Center Operations Manager de sistemas</span><span class="sxs-lookup"><span data-stu-id="5d5f4-134">Systems Center Operations Manager agent</span></span> | <span data-ttu-id="5d5f4-135">Azure</span><span class="sxs-lookup"><span data-stu-id="5d5f4-135">Azure</span></span> | <span data-ttu-id="5d5f4-136">O Operations Manager necessárias?</span><span class="sxs-lookup"><span data-stu-id="5d5f4-136">Operations Manager required?</span></span> | <span data-ttu-id="5d5f4-137">Dados de agente do Operations Manager enviados através do grupo de gestão</span><span class="sxs-lookup"><span data-stu-id="5d5f4-137">Operations Manager agent data sent via management group</span></span> | <span data-ttu-id="5d5f4-138">Frequência da recolha</span><span class="sxs-lookup"><span data-stu-id="5d5f4-138">Collection frequency</span></span> |
| --- | --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="5d5f4-139">Azure</span><span class="sxs-lookup"><span data-stu-id="5d5f4-139">Azure</span></span> |  |  |<span data-ttu-id="5d5f4-140">&#8226;</span><span class="sxs-lookup"><span data-stu-id="5d5f4-140">&#8226;</span></span> |  |  |<span data-ttu-id="5d5f4-141">Quando tem sessão iniciada</span><span class="sxs-lookup"><span data-stu-id="5d5f4-141">when logged</span></span> |


## <a name="azure-application-gateway-analytics-solution-in-log-analytics"></a><span data-ttu-id="5d5f4-142">Solução de análise do Gateway de aplicação do Azure na análise de registos</span><span class="sxs-lookup"><span data-stu-id="5d5f4-142">Azure Application Gateway analytics solution in Log Analytics</span></span>

![Símbolo de análise de Gateway de aplicação do Azure](./media/log-analytics-azure-networking/azure-analytics-symbol.png)

<span data-ttu-id="5d5f4-144">Olá seguintes os registos é suportada para Gateways de aplicação:</span><span class="sxs-lookup"><span data-stu-id="5d5f4-144">hello following logs are supported for Application Gateways:</span></span>

* <span data-ttu-id="5d5f4-145">ApplicationGatewayAccessLog</span><span class="sxs-lookup"><span data-stu-id="5d5f4-145">ApplicationGatewayAccessLog</span></span>
* <span data-ttu-id="5d5f4-146">ApplicationGatewayPerformanceLog</span><span class="sxs-lookup"><span data-stu-id="5d5f4-146">ApplicationGatewayPerformanceLog</span></span>
* <span data-ttu-id="5d5f4-147">ApplicationGatewayFirewallLog</span><span class="sxs-lookup"><span data-stu-id="5d5f4-147">ApplicationGatewayFirewallLog</span></span>

<span data-ttu-id="5d5f4-148">Olá métricas a seguir é suportada para Gateways de aplicação:</span><span class="sxs-lookup"><span data-stu-id="5d5f4-148">hello following metrics are supported for Application Gateways:</span></span>

* <span data-ttu-id="5d5f4-149">débito de 5 minutos</span><span class="sxs-lookup"><span data-stu-id="5d5f4-149">5 minute throughput</span></span>

### <a name="install-and-configure-hello-solution"></a><span data-ttu-id="5d5f4-150">Instalar e configurar a solução de Olá</span><span class="sxs-lookup"><span data-stu-id="5d5f4-150">Install and configure hello solution</span></span>
<span data-ttu-id="5d5f4-151">Utilizar Olá seguir instruções tooinstall e configure a solução de análise do Gateway de aplicação do Azure Olá:</span><span class="sxs-lookup"><span data-stu-id="5d5f4-151">Use hello following instructions tooinstall and configure hello Azure Application Gateway analytics solution:</span></span>

1. <span data-ttu-id="5d5f4-152">Ativar a solução de análise do Gateway de aplicação do Azure Olá de [do Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.AzureAppGatewayAnalyticsOMS?tab=Overview) ou utilizando o processo de Olá descrito em [soluções de análise de registos de adicionar de Olá soluções galeria](log-analytics-add-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="5d5f4-152">Enable hello Azure Application Gateway analytics solution from [Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.AzureAppGatewayAnalyticsOMS?tab=Overview) or by using hello process described in [Add Log Analytics solutions from hello Solutions Gallery](log-analytics-add-solutions.md).</span></span>
2. <span data-ttu-id="5d5f4-153">Ativar o registo de diagnóstico de Olá [Gateways de aplicação](../application-gateway/application-gateway-diagnostics.md) pretende toomonitor.</span><span class="sxs-lookup"><span data-stu-id="5d5f4-153">Enable diagnostics logging for hello [Application Gateways](../application-gateway/application-gateway-diagnostics.md) you want toomonitor.</span></span>

#### <a name="enable-azure-application-gateway-diagnostics-in-hello-portal"></a><span data-ttu-id="5d5f4-154">Ativar o diagnóstico do Gateway de aplicação do Azure no portal de Olá</span><span class="sxs-lookup"><span data-stu-id="5d5f4-154">Enable Azure Application Gateway diagnostics in hello portal</span></span>

1. <span data-ttu-id="5d5f4-155">No portal do Azure Olá, navegue toomonitor de recurso do Gateway de aplicação toohello</span><span class="sxs-lookup"><span data-stu-id="5d5f4-155">In hello Azure portal, navigate toohello Application Gateway resource toomonitor</span></span>
2. <span data-ttu-id="5d5f4-156">Selecione *registos de diagnóstico* Olá tooopen seguir página</span><span class="sxs-lookup"><span data-stu-id="5d5f4-156">Select *Diagnostics logs* tooopen hello following page</span></span>

   ![imagem de recurso de Gateway de aplicação do Azure](./media/log-analytics-azure-networking/log-analytics-appgateway-enable-diagnostics01.png)
3. <span data-ttu-id="5d5f4-158">Clique em *ative os diagnósticos* Olá tooopen seguir página</span><span class="sxs-lookup"><span data-stu-id="5d5f4-158">Click *Turn on diagnostics* tooopen hello following page</span></span>

   ![imagem de recurso de Gateway de aplicação do Azure](./media/log-analytics-azure-networking/log-analytics-appgateway-enable-diagnostics02.png)
4. <span data-ttu-id="5d5f4-160">Clique em tooturn diagnósticos, *no* em *Estado*</span><span class="sxs-lookup"><span data-stu-id="5d5f4-160">tooturn on diagnostics, click *On* under *Status*</span></span>
5. <span data-ttu-id="5d5f4-161">Clique em Olá caixa de verificação *enviar tooLog análise*</span><span class="sxs-lookup"><span data-stu-id="5d5f4-161">Click hello checkbox for *Send tooLog Analytics*</span></span>
6. <span data-ttu-id="5d5f4-162">Selecione uma área de trabalho de análise de registos existente ou crie uma área de trabalho</span><span class="sxs-lookup"><span data-stu-id="5d5f4-162">Select an existing Log Analytics workspace, or create a workspace</span></span>
7. <span data-ttu-id="5d5f4-163">Clique em Olá caixa de verificação em **registo** para cada um dos Olá registo tipos toocollect</span><span class="sxs-lookup"><span data-stu-id="5d5f4-163">Click hello checkbox under **Log** for each of hello log types toocollect</span></span>
8. <span data-ttu-id="5d5f4-164">Clique em *guardar* tooenable o registo de Olá de diagnóstico tooLog análise</span><span class="sxs-lookup"><span data-stu-id="5d5f4-164">Click *Save* tooenable hello logging of diagnostics tooLog Analytics</span></span>

#### <a name="enable-azure-network-diagnostics-using-powershell"></a><span data-ttu-id="5d5f4-165">Ativar o diagnóstico de rede do Azure com o PowerShell</span><span class="sxs-lookup"><span data-stu-id="5d5f4-165">Enable Azure network diagnostics using PowerShell</span></span>

<span data-ttu-id="5d5f4-166">Olá seguinte script do PowerShell fornece um exemplo de como tooenable diagnóstico de registo para gateways de aplicação.</span><span class="sxs-lookup"><span data-stu-id="5d5f4-166">hello following PowerShell script provides an example of how tooenable diagnostic logging for application gateways.</span></span>

```powershell
$workspaceId = "/subscriptions/d2e37fee-1234-40b2-5678-0b2199de3b50/resourcegroups/oi-default-east-us/providers/microsoft.operationalinsights/workspaces/rollingbaskets"

$gateway = Get-AzureRmApplicationGateway -Name 'ContosoGateway'

Set-AzureRmDiagnosticSetting -ResourceId $gateway.ResourceId  -WorkspaceId $workspaceId -Enabled $true
```

### <a name="use-azure-application-gateway-analytics"></a><span data-ttu-id="5d5f4-167">Utilize a análise de Gateway de aplicação do Azure</span><span class="sxs-lookup"><span data-stu-id="5d5f4-167">Use Azure Application Gateway analytics</span></span>
![imagem do Gateway de aplicação do Azure mosaico de análise](./media/log-analytics-azure-networking/log-analytics-appgateway-tile.png)

<span data-ttu-id="5d5f4-169">Depois de clicar em Olá **análise de Gateway de aplicação do Azure** mosaico Olá descrição geral, pode ver resumos dos seus registos e depois pormenorize em toodetails para Olá seguintes categorias:</span><span class="sxs-lookup"><span data-stu-id="5d5f4-169">After you click hello **Azure Application Gateway analytics** tile on hello Overview, you can view summaries of your logs and then drill in toodetails for hello following categories:</span></span>

* <span data-ttu-id="5d5f4-170">Os registos de acesso de Gateway de aplicação</span><span class="sxs-lookup"><span data-stu-id="5d5f4-170">Application Gateway Access logs</span></span>
  * <span data-ttu-id="5d5f4-171">Erros de cliente e servidor para os registos de acesso do Gateway de aplicação</span><span class="sxs-lookup"><span data-stu-id="5d5f4-171">Client and server errors for Application Gateway access logs</span></span>
  * <span data-ttu-id="5d5f4-172">Pedidos por hora para cada Gateway de aplicação</span><span class="sxs-lookup"><span data-stu-id="5d5f4-172">Requests per hour for each Application Gateway</span></span>
  * <span data-ttu-id="5d5f4-173">Falha de pedidos por hora para cada Gateway de aplicação</span><span class="sxs-lookup"><span data-stu-id="5d5f4-173">Failed requests per hour for each Application Gateway</span></span>
  * <span data-ttu-id="5d5f4-174">Erros pelo agente de utilizador para Gateways de aplicação</span><span class="sxs-lookup"><span data-stu-id="5d5f4-174">Errors by user agent for Application Gateways</span></span>
* <span data-ttu-id="5d5f4-175">Desempenho do Gateway de aplicação</span><span class="sxs-lookup"><span data-stu-id="5d5f4-175">Application Gateway performance</span></span>
  * <span data-ttu-id="5d5f4-176">Estado de funcionamento do anfitrião para o Gateway de aplicação</span><span class="sxs-lookup"><span data-stu-id="5d5f4-176">Host health for Application Gateway</span></span>
  * <span data-ttu-id="5d5f4-177">Pedidos falhados de percentil máximo e 95th para Gateway de aplicação</span><span class="sxs-lookup"><span data-stu-id="5d5f4-177">Maximum and 95th percentile for Application Gateway failed requests</span></span>

![imagem do dashboard de análise do Gateway de aplicação do Azure](./media/log-analytics-azure-networking/log-analytics-appgateway01.png)

![imagem do dashboard de análise do Gateway de aplicação do Azure](./media/log-analytics-azure-networking/log-analytics-appgateway02.png)

<span data-ttu-id="5d5f4-180">No Olá **análise de Gateway de aplicação do Azure** dashboard, reveja as informações de resumo de Olá dos painéis de Olá e, em seguida, clique numa tooview informações detalhadas sobre a página de pesquisa de registo de Olá.</span><span class="sxs-lookup"><span data-stu-id="5d5f4-180">On hello **Azure Application Gateway analytics** dashboard, review hello summary information in one of hello blades, and then click one tooview detailed information on hello log search page.</span></span>

<span data-ttu-id="5d5f4-181">Em qualquer uma das páginas de pesquisa de registo Olá, pode ver os resultados por tempo, os resultados detalhados e o histórico de pesquisa de registo.</span><span class="sxs-lookup"><span data-stu-id="5d5f4-181">On any of hello log search pages, you can view results by time, detailed results, and your log search history.</span></span> <span data-ttu-id="5d5f4-182">Também pode filtrar por resultados de Olá facetas toonarrow.</span><span class="sxs-lookup"><span data-stu-id="5d5f4-182">You can also filter by facets toonarrow hello results.</span></span>


## <a name="azure-network-security-group-analytics-solution-in-log-analytics"></a><span data-ttu-id="5d5f4-183">Solução de análise do grupo de segurança de rede do Azure na análise de registos</span><span class="sxs-lookup"><span data-stu-id="5d5f4-183">Azure Network Security Group analytics solution in Log Analytics</span></span>

![Símbolo de análise do grupo de segurança de rede do Azure](./media/log-analytics-azure-networking/azure-analytics-symbol.png)

<span data-ttu-id="5d5f4-185">Olá seguintes os registos é suportada para grupos de segurança de rede:</span><span class="sxs-lookup"><span data-stu-id="5d5f4-185">hello following logs are supported for network security groups:</span></span>

* <span data-ttu-id="5d5f4-186">NetworkSecurityGroupEvent</span><span class="sxs-lookup"><span data-stu-id="5d5f4-186">NetworkSecurityGroupEvent</span></span>
* <span data-ttu-id="5d5f4-187">NetworkSecurityGroupRuleCounter</span><span class="sxs-lookup"><span data-stu-id="5d5f4-187">NetworkSecurityGroupRuleCounter</span></span>

### <a name="install-and-configure-hello-solution"></a><span data-ttu-id="5d5f4-188">Instalar e configurar a solução de Olá</span><span class="sxs-lookup"><span data-stu-id="5d5f4-188">Install and configure hello solution</span></span>
<span data-ttu-id="5d5f4-189">Utilizar Olá seguir instruções tooinstall e configure a solução de análise de redes do Azure Olá:</span><span class="sxs-lookup"><span data-stu-id="5d5f4-189">Use hello following instructions tooinstall and configure hello Azure Networking Analytics solution:</span></span>

1. <span data-ttu-id="5d5f4-190">Ativar a solução de análise do grupo de segurança de rede de Azure Olá de [do Azure marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.AzureNSGAnalyticsOMS?tab=Overview) ou utilizando o processo de Olá descrito em [soluções de análise de registos de adicionar de Olá soluções galeria](log-analytics-add-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="5d5f4-190">Enable hello Azure Network Security Group analytics solution from [Azure marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.AzureNSGAnalyticsOMS?tab=Overview) or by using hello process described in [Add Log Analytics solutions from hello Solutions Gallery](log-analytics-add-solutions.md).</span></span>
2. <span data-ttu-id="5d5f4-191">Ativar o registo de diagnóstico de Olá [grupo de segurança de rede](../virtual-network/virtual-network-nsg-manage-log.md) recursos que pretende toomonitor.</span><span class="sxs-lookup"><span data-stu-id="5d5f4-191">Enable diagnostics logging for hello [Network Security Group](../virtual-network/virtual-network-nsg-manage-log.md) resources you want toomonitor.</span></span>

### <a name="enable-azure-network-security-group-diagnostics-in-hello-portal"></a><span data-ttu-id="5d5f4-192">Ativar o diagnóstico de grupo de segurança de rede do Azure no portal de Olá</span><span class="sxs-lookup"><span data-stu-id="5d5f4-192">Enable Azure network security group diagnostics in hello portal</span></span>

1. <span data-ttu-id="5d5f4-193">No portal do Azure Olá, navegue toomonitor de recursos do grupo de segurança de rede toohello</span><span class="sxs-lookup"><span data-stu-id="5d5f4-193">In hello Azure portal, navigate toohello Network Security Group resource toomonitor</span></span>
2. <span data-ttu-id="5d5f4-194">Selecione *registos de diagnóstico* Olá tooopen seguir página</span><span class="sxs-lookup"><span data-stu-id="5d5f4-194">Select *Diagnostics logs* tooopen hello following page</span></span>

   ![imagem de recurso do grupo de segurança de rede do Azure](./media/log-analytics-azure-networking/log-analytics-nsg-enable-diagnostics01.png)
3. <span data-ttu-id="5d5f4-196">Clique em *ative os diagnósticos* Olá tooopen seguir página</span><span class="sxs-lookup"><span data-stu-id="5d5f4-196">Click *Turn on diagnostics* tooopen hello following page</span></span>

   ![imagem de recurso do grupo de segurança de rede do Azure](./media/log-analytics-azure-networking/log-analytics-nsg-enable-diagnostics02.png)
4. <span data-ttu-id="5d5f4-198">Clique em tooturn diagnósticos, *no* em *Estado*</span><span class="sxs-lookup"><span data-stu-id="5d5f4-198">tooturn on diagnostics, click *On* under *Status*</span></span>
5. <span data-ttu-id="5d5f4-199">Clique em Olá caixa de verificação *enviar tooLog análise*</span><span class="sxs-lookup"><span data-stu-id="5d5f4-199">Click hello checkbox for *Send tooLog Analytics*</span></span>
6. <span data-ttu-id="5d5f4-200">Selecione uma área de trabalho de análise de registos existente ou crie uma área de trabalho</span><span class="sxs-lookup"><span data-stu-id="5d5f4-200">Select an existing Log Analytics workspace, or create a workspace</span></span>
7. <span data-ttu-id="5d5f4-201">Clique em Olá caixa de verificação em **registo** para cada um dos Olá registo tipos toocollect</span><span class="sxs-lookup"><span data-stu-id="5d5f4-201">Click hello checkbox under **Log** for each of hello log types toocollect</span></span>
8. <span data-ttu-id="5d5f4-202">Clique em *guardar* tooenable o registo de Olá de diagnóstico tooLog análise</span><span class="sxs-lookup"><span data-stu-id="5d5f4-202">Click *Save* tooenable hello logging of diagnostics tooLog Analytics</span></span>

### <a name="enable-azure-network-diagnostics-using-powershell"></a><span data-ttu-id="5d5f4-203">Ativar o diagnóstico de rede do Azure com o PowerShell</span><span class="sxs-lookup"><span data-stu-id="5d5f4-203">Enable Azure network diagnostics using PowerShell</span></span>

<span data-ttu-id="5d5f4-204">Olá seguinte script do PowerShell fornece um exemplo de como tooenable diagnóstico de registo para grupos de segurança de rede</span><span class="sxs-lookup"><span data-stu-id="5d5f4-204">hello following PowerShell script provides an example of how tooenable diagnostic logging for network security groups</span></span>
```powershell
$workspaceId = "/subscriptions/d2e37fee-1234-40b2-5678-0b2199de3b50/resourcegroups/oi-default-east-us/providers/microsoft.operationalinsights/workspaces/rollingbaskets"

$nsg = Get-AzureRmNetworkSecurityGroup -Name 'ContosoNSG'

Set-AzureRmDiagnosticSetting -ResourceId $nsg.ResourceId  -WorkspaceId $workspaceId -Enabled $true
```

### <a name="use-azure-network-security-group-analytics"></a><span data-ttu-id="5d5f4-205">Análise de grupo de segurança de rede de Azure de utilização</span><span class="sxs-lookup"><span data-stu-id="5d5f4-205">Use Azure Network Security Group analytics</span></span>
<span data-ttu-id="5d5f4-206">Depois de clicar em Olá **análise do grupo de segurança de rede de Azure** mosaico Olá descrição geral, pode ver resumos dos seus registos e depois pormenorize em toodetails para Olá seguintes categorias:</span><span class="sxs-lookup"><span data-stu-id="5d5f4-206">After you click hello **Azure Network Security Group analytics** tile on hello Overview, you can view summaries of your logs and then drill in toodetails for hello following categories:</span></span>

* <span data-ttu-id="5d5f4-207">Grupo de segurança de rede bloqueado fluxos</span><span class="sxs-lookup"><span data-stu-id="5d5f4-207">Network security group blocked flows</span></span>
  * <span data-ttu-id="5d5f4-208">Regras de grupo de segurança de rede com fluxos de bloqueados</span><span class="sxs-lookup"><span data-stu-id="5d5f4-208">Network security group rules with blocked flows</span></span>
  * <span data-ttu-id="5d5f4-209">Endereços MAC com fluxos bloqueados</span><span class="sxs-lookup"><span data-stu-id="5d5f4-209">MAC addresses with blocked flows</span></span>
* <span data-ttu-id="5d5f4-210">Grupo de segurança de rede permitido fluxos</span><span class="sxs-lookup"><span data-stu-id="5d5f4-210">Network security group allowed flows</span></span>
  * <span data-ttu-id="5d5f4-211">Regras de grupo de segurança de rede com fluxos permitidos</span><span class="sxs-lookup"><span data-stu-id="5d5f4-211">Network security group rules with allowed flows</span></span>
  * <span data-ttu-id="5d5f4-212">Endereços MAC com fluxos permitidos</span><span class="sxs-lookup"><span data-stu-id="5d5f4-212">MAC addresses with allowed flows</span></span>

![imagem do dashboard de análise do grupo de segurança de rede do Azure](./media/log-analytics-azure-networking/log-analytics-nsg01.png)

![imagem do dashboard de análise do grupo de segurança de rede do Azure](./media/log-analytics-azure-networking/log-analytics-nsg02.png)

<span data-ttu-id="5d5f4-215">No Olá **análise do grupo de segurança de rede de Azure** dashboard, reveja as informações de resumo de Olá dos painéis de Olá e, em seguida, clique numa tooview informações detalhadas sobre a página de pesquisa de registo de Olá.</span><span class="sxs-lookup"><span data-stu-id="5d5f4-215">On hello **Azure Network Security Group analytics** dashboard, review hello summary information in one of hello blades, and then click one tooview detailed information on hello log search page.</span></span>

<span data-ttu-id="5d5f4-216">Em qualquer uma das páginas de pesquisa de registo Olá, pode ver os resultados por tempo, os resultados detalhados e o histórico de pesquisa de registo.</span><span class="sxs-lookup"><span data-stu-id="5d5f4-216">On any of hello log search pages, you can view results by time, detailed results, and your log search history.</span></span> <span data-ttu-id="5d5f4-217">Também pode filtrar por resultados de Olá facetas toonarrow.</span><span class="sxs-lookup"><span data-stu-id="5d5f4-217">You can also filter by facets toonarrow hello results.</span></span>

## <a name="migrating-from-hello-old-networking-analytics-solution"></a><span data-ttu-id="5d5f4-218">Migrar a partir de solução de análise de redes de antiga Olá</span><span class="sxs-lookup"><span data-stu-id="5d5f4-218">Migrating from hello old Networking Analytics solution</span></span>
<span data-ttu-id="5d5f4-219">Em Janeiro de 2017, Olá suportados forma de envio de registos de Gateways de aplicação do Azure e os grupos de segurança de rede do Azure tooLog que Analytics foi alterado.</span><span class="sxs-lookup"><span data-stu-id="5d5f4-219">In January 2017, hello supported way of sending logs from Azure Application Gateways and Azure Network Security Groups tooLog Analytics changed.</span></span> <span data-ttu-id="5d5f4-220">Estas alterações fornecem Olá seguintes vantagens:</span><span class="sxs-lookup"><span data-stu-id="5d5f4-220">These changes provide hello following advantages:</span></span>
+ <span data-ttu-id="5d5f4-221">Os registos são escritos diretamente tooLog análise sem Olá necessário toouse uma conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="5d5f4-221">Logs are written directly tooLog Analytics without hello need toouse a storage account</span></span>
+ <span data-ttu-id="5d5f4-222">A menor latência de tempo de Olá quando os registos são gerados toothem estejam disponíveis no Log Analytics</span><span class="sxs-lookup"><span data-stu-id="5d5f4-222">Less latency from hello time when logs are generated toothem being available in Log Analytics</span></span>
+ <span data-ttu-id="5d5f4-223">Menos passos de configuração</span><span class="sxs-lookup"><span data-stu-id="5d5f4-223">Fewer configuration steps</span></span>
+ <span data-ttu-id="5d5f4-224">Um formato comum para todos os tipos de diagnóstico do Azure</span><span class="sxs-lookup"><span data-stu-id="5d5f4-224">A common format for all types of Azure diagnostics</span></span>

<span data-ttu-id="5d5f4-225">Olá toouse atualizado soluções:</span><span class="sxs-lookup"><span data-stu-id="5d5f4-225">toouse hello updated solutions:</span></span>

1. [<span data-ttu-id="5d5f4-226">Configurar toobe de diagnóstico enviado diretamente tooLog análise dos Gateways de aplicação do Azure</span><span class="sxs-lookup"><span data-stu-id="5d5f4-226">Configure diagnostics toobe sent directly tooLog Analytics from Azure Application Gateways</span></span>](#enable-azure-application-gateway-diagnostics-in-the-portal)
2. [<span data-ttu-id="5d5f4-227">Configurar toobe de diagnóstico enviado tooLog análise diretamente a partir de grupos de segurança de rede do Azure</span><span class="sxs-lookup"><span data-stu-id="5d5f4-227">Configure diagnostics toobe sent directly tooLog Analytics from Azure Network Security Groups</span></span>](#enable-azure-network-security-group-diagnostics-in-the-portal)
2. <span data-ttu-id="5d5f4-228">Ativar Olá *análise de Gateway de aplicação do Azure* e Olá *análises de grupo de segurança de rede de Azure* solução utilizando Olá processo descrito no [soluções de análise de registos de adicionar de Olá Galeria de soluções](log-analytics-add-solutions.md)</span><span class="sxs-lookup"><span data-stu-id="5d5f4-228">Enable hello *Azure Application Gateway Analytics* and hello *Azure Network Security Group Analytics* solution by using hello process described in [Add Log Analytics solutions from hello Solutions Gallery](log-analytics-add-solutions.md)</span></span>
3. <span data-ttu-id="5d5f4-229">Atualizar qualquer consultas guardadas, dashboards ou alertas toouse Olá novo tipo de dados</span><span class="sxs-lookup"><span data-stu-id="5d5f4-229">Update any saved queries, dashboards, or alerts toouse hello new data type</span></span>
  + <span data-ttu-id="5d5f4-230">O tipo é tooAzureDiagnostics.</span><span class="sxs-lookup"><span data-stu-id="5d5f4-230">Type is tooAzureDiagnostics.</span></span> <span data-ttu-id="5d5f4-231">Pode utilizar Olá ResourceType toofilter tooAzure rede os registos de.</span><span class="sxs-lookup"><span data-stu-id="5d5f4-231">You can use hello ResourceType toofilter tooAzure networking logs.</span></span>

    | <span data-ttu-id="5d5f4-232">Em vez de:</span><span class="sxs-lookup"><span data-stu-id="5d5f4-232">Instead of:</span></span> | <span data-ttu-id="5d5f4-233">Utilização:</span><span class="sxs-lookup"><span data-stu-id="5d5f4-233">Use:</span></span> |
    | --- | --- |
    |`Type=NetworkApplicationgateways OperationName=ApplicationGatewayAccess`| `Type=AzureDiagnostics ResourceType=APPLICATIONGATEWAYS OperationName=ApplicationGatewayAccess` |
    |`Type=NetworkApplicationgateways OperationName=ApplicationGatewayPerformance` | `Type=AzureDiagnostics ResourceType=APPLICATIONGATEWAYS OperationName=ApplicationGatewayPerformance` |
    | `Type=NetworkSecuritygroups` | `Type=AzureDiagnostics ResourceType=NETWORKSECURITYGROUPS` |

   + <span data-ttu-id="5d5f4-234">Para qualquer campo que têm um sufixo de \_s, \_d, ou \_g no nome de Olá, alteração Olá primeiro caráter toolower maiúsculas e minúsculas</span><span class="sxs-lookup"><span data-stu-id="5d5f4-234">For any field that has a suffix of \_s, \_d, or \_g in hello name, change hello first character toolower case</span></span>
   + <span data-ttu-id="5d5f4-235">Para qualquer campo que têm um sufixo de \_Nã no nome, dados de Olá é dividido em campos individuais com base nos nomes de campo Olá aninhado.</span><span class="sxs-lookup"><span data-stu-id="5d5f4-235">For any field that has a suffix of \_o in name, hello data is split into individual fields based on hello nested field names.</span></span>
4. <span data-ttu-id="5d5f4-236">Remover Olá *redes a análise do Azure (preterido)* solução.</span><span class="sxs-lookup"><span data-stu-id="5d5f4-236">Remove hello *Azure Networking Analytics (Deprecated)* solution.</span></span>
  + <span data-ttu-id="5d5f4-237">Se estiver a utilizar o PowerShell, utilize`Set-AzureOperationalInsightsIntelligencePack -ResourceGroupName <resource group that hello workspace is in> -WorkspaceName <name of hello log analytics workspace> -IntelligencePackName "AzureNetwork" -Enabled $false`</span><span class="sxs-lookup"><span data-stu-id="5d5f4-237">If you are using PowerShell, use `Set-AzureOperationalInsightsIntelligencePack -ResourceGroupName <resource group that hello workspace is in> -WorkspaceName <name of hello log analytics workspace> -IntelligencePackName "AzureNetwork" -Enabled $false`</span></span>

<span data-ttu-id="5d5f4-238">Recolher os dados antes de alteração de Olá não estiver visível na solução nova Olá.</span><span class="sxs-lookup"><span data-stu-id="5d5f4-238">Data collected before hello change is not visible in hello new solution.</span></span> <span data-ttu-id="5d5f4-239">Pode continuar tooquery para esta utilizando dados Olá tipo antigo e nomes de campo.</span><span class="sxs-lookup"><span data-stu-id="5d5f4-239">You can continue tooquery for this data using hello old Type and field names.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="5d5f4-240">Resolução de problemas</span><span class="sxs-lookup"><span data-stu-id="5d5f4-240">Troubleshooting</span></span>
[!INCLUDE [log-analytics-troubleshoot-azure-diagnostics](../../includes/log-analytics-troubleshoot-azure-diagnostics.md)]

## <a name="next-steps"></a><span data-ttu-id="5d5f4-241">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="5d5f4-241">Next steps</span></span>
* <span data-ttu-id="5d5f4-242">Utilize [pesquisas de registo na análise de registos](log-analytics-log-searches.md) tooview detalhadas dados de diagnóstico do Azure.</span><span class="sxs-lookup"><span data-stu-id="5d5f4-242">Use [Log searches in Log Analytics](log-analytics-log-searches.md) tooview detailed Azure diagnostics data.</span></span>
