---
title: "endereços de aaaIP utilizados pelo Application Insights | Microsoft Docs"
description: "Exceções de firewall de servidor necessárias para o Application Insights"
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: 44d989f8-bae9-40ff-bfd5-8343d3e59358
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 8/11/2017
ms.author: bwren
ms.openlocfilehash: 2c101b8da2ba9594fbff607f4f7551cda80c3c25
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="ip-addresses-used-by-application-insights"></a><span data-ttu-id="571fb-103">Endereços IP utilizados pelo Application Insights</span><span class="sxs-lookup"><span data-stu-id="571fb-103">IP addresses used by Application Insights</span></span>
<span data-ttu-id="571fb-104">Olá [Azure Application Insights](app-insights-overview.md) serviço utiliza um número de endereços IP.</span><span class="sxs-lookup"><span data-stu-id="571fb-104">hello [Azure Application Insights](app-insights-overview.md) service uses a number of IP addresses.</span></span> <span data-ttu-id="571fb-105">Poderá ser necessário tooknow estes endereços se Olá aplicação que está a monitorizar estiver alojada atrás de uma firewall.</span><span class="sxs-lookup"><span data-stu-id="571fb-105">You might need tooknow these addresses if hello app that you are monitoring is hosted behind a firewall.</span></span>

> [!NOTE]
> <span data-ttu-id="571fb-106">Embora estes endereços são estáticos, é possível que precisamos toochange dos mesmos tootime de tempo.</span><span class="sxs-lookup"><span data-stu-id="571fb-106">Although these addresses are static, it's possible that we will need toochange them from time tootime.</span></span>
> 
> 

## <a name="outgoing-ports"></a><span data-ttu-id="571fb-107">Portas de envio</span><span class="sxs-lookup"><span data-stu-id="571fb-107">Outgoing ports</span></span>
<span data-ttu-id="571fb-108">É necessário tooopen algumas portas de envio no hello de tooallow de firewall do seu servidor Application Insights SDK e/ou o portal do Monitor de estado toosend dados toohello:</span><span class="sxs-lookup"><span data-stu-id="571fb-108">You need tooopen some outgoing ports in your server's firewall tooallow hello Application Insights SDK and/or Status Monitor toosend data toohello portal:</span></span>

| <span data-ttu-id="571fb-109">Objetivo</span><span class="sxs-lookup"><span data-stu-id="571fb-109">Purpose</span></span> | <span data-ttu-id="571fb-110">URL</span><span class="sxs-lookup"><span data-stu-id="571fb-110">URL</span></span> | <span data-ttu-id="571fb-111">IP</span><span class="sxs-lookup"><span data-stu-id="571fb-111">IP</span></span> | <span data-ttu-id="571fb-112">Portas</span><span class="sxs-lookup"><span data-stu-id="571fb-112">Ports</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="571fb-113">Telemetria</span><span class="sxs-lookup"><span data-stu-id="571fb-113">Telemetry</span></span> |<span data-ttu-id="571fb-114">DC.Services.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="571fb-114">dc.services.visualstudio.com</span></span><br/><span data-ttu-id="571fb-115">DC.applicationinsights.microsoft.com</span><span class="sxs-lookup"><span data-stu-id="571fb-115">dc.applicationinsights.microsoft.com</span></span> |<span data-ttu-id="571fb-116">40.114.241.141</span><span class="sxs-lookup"><span data-stu-id="571fb-116">40.114.241.141</span></span><br/><span data-ttu-id="571fb-117">104.45.136.42</span><span class="sxs-lookup"><span data-stu-id="571fb-117">104.45.136.42</span></span><br/><span data-ttu-id="571fb-118">40.84.189.107</span><span class="sxs-lookup"><span data-stu-id="571fb-118">40.84.189.107</span></span><br/><span data-ttu-id="571fb-119">168.63.242.221</span><span class="sxs-lookup"><span data-stu-id="571fb-119">168.63.242.221</span></span><br/><span data-ttu-id="571fb-120">52.167.221.184</span><span class="sxs-lookup"><span data-stu-id="571fb-120">52.167.221.184</span></span><br/><span data-ttu-id="571fb-121">52.169.64.244</span><span class="sxs-lookup"><span data-stu-id="571fb-121">52.169.64.244</span></span> |<span data-ttu-id="571fb-122">443</span><span class="sxs-lookup"><span data-stu-id="571fb-122">443</span></span> |
| <span data-ttu-id="571fb-123">Transmissão de métricas em direto</span><span class="sxs-lookup"><span data-stu-id="571fb-123">Live Metrics Stream</span></span> |<span data-ttu-id="571fb-124">RT.Services.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="571fb-124">rt.services.visualstudio.com</span></span><br/><span data-ttu-id="571fb-125">RT.applicationinsights.microsoft.com</span><span class="sxs-lookup"><span data-stu-id="571fb-125">rt.applicationinsights.microsoft.com</span></span> |<span data-ttu-id="571fb-126">23.96.28.38</span><span class="sxs-lookup"><span data-stu-id="571fb-126">23.96.28.38</span></span><br/><span data-ttu-id="571fb-127">13.92.40.198</span><span class="sxs-lookup"><span data-stu-id="571fb-127">13.92.40.198</span></span> |<span data-ttu-id="571fb-128">443</span><span class="sxs-lookup"><span data-stu-id="571fb-128">443</span></span> |
| <span data-ttu-id="571fb-129">Telemetria interna</span><span class="sxs-lookup"><span data-stu-id="571fb-129">Internal Telemetry</span></span> |<span data-ttu-id="571fb-130">breeze.aimon.applicationinsights.IO</span><span class="sxs-lookup"><span data-stu-id="571fb-130">breeze.aimon.applicationinsights.io</span></span> |<span data-ttu-id="571fb-131">52.161.11.71</span><span class="sxs-lookup"><span data-stu-id="571fb-131">52.161.11.71</span></span> |<span data-ttu-id="571fb-132">443</span><span class="sxs-lookup"><span data-stu-id="571fb-132">443</span></span> |

## <a name="status-monitor"></a><span data-ttu-id="571fb-133">Monitor de estado</span><span class="sxs-lookup"><span data-stu-id="571fb-133">Status Monitor</span></span>
<span data-ttu-id="571fb-134">Configuração de Monitor do Estado - necessária apenas quando efetuar alterações.</span><span class="sxs-lookup"><span data-stu-id="571fb-134">Status Monitor Configuration - needed only when making changes.</span></span>

| <span data-ttu-id="571fb-135">Objetivo</span><span class="sxs-lookup"><span data-stu-id="571fb-135">Purpose</span></span> | <span data-ttu-id="571fb-136">URL</span><span class="sxs-lookup"><span data-stu-id="571fb-136">URL</span></span> | <span data-ttu-id="571fb-137">IP</span><span class="sxs-lookup"><span data-stu-id="571fb-137">IP</span></span> | <span data-ttu-id="571fb-138">Portas</span><span class="sxs-lookup"><span data-stu-id="571fb-138">Ports</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="571fb-139">Configuração</span><span class="sxs-lookup"><span data-stu-id="571fb-139">Configuration</span></span> |`management.core.windows.net` | |`443` |
| <span data-ttu-id="571fb-140">Configuração</span><span class="sxs-lookup"><span data-stu-id="571fb-140">Configuration</span></span> |`management.azure.com` | |`443` |
| <span data-ttu-id="571fb-141">Configuração</span><span class="sxs-lookup"><span data-stu-id="571fb-141">Configuration</span></span> |`login.windows.net` | |`443` |
| <span data-ttu-id="571fb-142">Configuração</span><span class="sxs-lookup"><span data-stu-id="571fb-142">Configuration</span></span> |`login.microsoftonline.com` | |`443` |
| <span data-ttu-id="571fb-143">Configuração</span><span class="sxs-lookup"><span data-stu-id="571fb-143">Configuration</span></span> |`secure.aadcdn.microsoftonline-p.com` | |`443` |
| <span data-ttu-id="571fb-144">Configuração</span><span class="sxs-lookup"><span data-stu-id="571fb-144">Configuration</span></span> |`auth.gfx.ms` | |`443` |
| <span data-ttu-id="571fb-145">Configuração</span><span class="sxs-lookup"><span data-stu-id="571fb-145">Configuration</span></span> |`login.live.com` | |`443` |
| <span data-ttu-id="571fb-146">Instalação</span><span class="sxs-lookup"><span data-stu-id="571fb-146">Installation</span></span> |`packages.nuget.org` | |`443` |

## <a name="hockeyapp"></a><span data-ttu-id="571fb-147">HockeyApp</span><span class="sxs-lookup"><span data-stu-id="571fb-147">HockeyApp</span></span>
| <span data-ttu-id="571fb-148">Objetivo</span><span class="sxs-lookup"><span data-stu-id="571fb-148">Purpose</span></span> | <span data-ttu-id="571fb-149">URL</span><span class="sxs-lookup"><span data-stu-id="571fb-149">URL</span></span> | <span data-ttu-id="571fb-150">IP</span><span class="sxs-lookup"><span data-stu-id="571fb-150">IP</span></span> | <span data-ttu-id="571fb-151">Portas</span><span class="sxs-lookup"><span data-stu-id="571fb-151">Ports</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="571fb-152">Dados de falhas</span><span class="sxs-lookup"><span data-stu-id="571fb-152">Crash data</span></span> |<span data-ttu-id="571fb-153">Gate.hockeyapp.NET</span><span class="sxs-lookup"><span data-stu-id="571fb-153">gate.hockeyapp.net</span></span> |<span data-ttu-id="571fb-154">104.45.136.42</span><span class="sxs-lookup"><span data-stu-id="571fb-154">104.45.136.42</span></span> |<span data-ttu-id="571fb-155">80, 443</span><span class="sxs-lookup"><span data-stu-id="571fb-155">80, 443</span></span> |

## <a name="availability-tests"></a><span data-ttu-id="571fb-156">Testes de disponibilidade</span><span class="sxs-lookup"><span data-stu-id="571fb-156">Availability tests</span></span>
<span data-ttu-id="571fb-157">Esta é Olá lista de endereços a partir da qual [testes web de disponibilidade](app-insights-monitor-web-app-availability.md) são executados.</span><span class="sxs-lookup"><span data-stu-id="571fb-157">This is hello list of addresses from which [availability web tests](app-insights-monitor-web-app-availability.md) are run.</span></span> <span data-ttu-id="571fb-158">Se pretende que os testes web toorun na sua aplicação, mas o servidor web tooserving restrito de clientes específico, em seguida, terá de tráfego de entrada toopermit dos nossos servidores de teste de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="571fb-158">If you want toorun web tests on your app, but your web server is restricted tooserving specific clients, then you will have toopermit incoming traffic from our availability test servers.</span></span>

<span data-ttu-id="571fb-159">Abra as portas 80 (http) e 443 (https) para o tráfego de entrada nestes endereços (endereços IP são agrupados por localização):</span><span class="sxs-lookup"><span data-stu-id="571fb-159">Open ports 80 (http) and 443 (https) for incoming traffic from these addresses (IP addresses are grouped by location):</span></span>

```
AU : Sydney
13.70.83.252
13.75.150.96
13.75.153.9
13.75.158.185
BR : Sao Paulo
191.232.32.122
191.232.172.45
191.232.176.218
191.232.191.225
CH : Zurich
94.245.66.43
94.245.66.44
94.245.66.45
94.245.66.48
FR : Paris
94.245.72.44
94.245.72.45
94.245.72.46
94.245.72.49
94.245.72.52
94.245.72.53
HK : Hong Kong
13.75.121.122
23.99.115.153
23.99.123.38
23.102.232.186
52.175.38.49
52.175.39.103
IE : Dublin
13.74.184.101
13.74.185.160
40.69.200.198
52.164.224.46
52.169.12.203
52.169.14.11
52.169.237.149
52.178.183.105
JP : Kawaguchi
52.243.33.33
52.243.33.141
52.243.35.253
52.243.41.117
NL : Amsterdam
52.174.166.113
52.174.178.96
52.174.31.140
52.174.35.14
52.178.104.23
52.178.109.190
52.178.111.139
52.233.166.221
RU : Moscow
94.245.82.32
94.245.82.33
94.245.82.37
94.245.82.38
SE : Stockholm
94.245.78.40
94.245.78.41
94.245.78.42
94.245.78.45
SG : Singapore
52.187.29.7
52.187.179.17
52.187.76.248
52.187.43.24
52.163.57.91
52.187.30.120
US : CA-San Jose
104.45.228.236
104.45.237.251
13.64.152.110
13.64.156.54
13.64.232.251
13.64.236.105
13.91.94.59
40.118.131.182
40.83.189.192
40.83.215.122
US : FL-Miami
65.54.78.49
65.54.78.50
65.54.78.51
65.54.78.54
65.54.78.57
65.54.78.58
65.54.78.59
65.54.78.60
US : IL-Chicago
23.96.247.139
23.96.249.113
52.162.124.242
52.162.126.139
52.162.241.147
52.162.246.222
52.162.247.136
52.237.153.231
52.237.154.216
52.237.156.14
52.237.157.218
52.237.157.37
US : TX-San Antonio
104.210.145.106
13.84.176.24
13.84.49.16
13.85.11.137
13.85.26.248
13.85.69.145
52.171.136.162
52.171.141.253
52.171.57.172
52.171.58.140
US : VA-Ashburn
13.82.218.95
13.90.96.71
13.90.98.52
13.92.137.70
40.85.187.235
40.87.61.61
52.168.8.247
52.170.38.79
52.170.80.61
52.179.9.26

```  

## <a name="data-access-api"></a><span data-ttu-id="571fb-160">API de acesso a dados</span><span class="sxs-lookup"><span data-stu-id="571fb-160">Data access API</span></span>
| <span data-ttu-id="571fb-161">Objetivo</span><span class="sxs-lookup"><span data-stu-id="571fb-161">Purpose</span></span> | <span data-ttu-id="571fb-162">URI</span><span class="sxs-lookup"><span data-stu-id="571fb-162">URI</span></span> | <span data-ttu-id="571fb-163">IP</span><span class="sxs-lookup"><span data-stu-id="571fb-163">IP</span></span> | <span data-ttu-id="571fb-164">Portas</span><span class="sxs-lookup"><span data-stu-id="571fb-164">Ports</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="571fb-165">API</span><span class="sxs-lookup"><span data-stu-id="571fb-165">API</span></span> |<span data-ttu-id="571fb-166">API.applicationinsights.IO</span><span class="sxs-lookup"><span data-stu-id="571fb-166">api.applicationinsights.io</span></span><br/><span data-ttu-id="571fb-167">api1.applicationinsights.IO</span><span class="sxs-lookup"><span data-stu-id="571fb-167">api1.applicationinsights.io</span></span><br/><span data-ttu-id="571fb-168">api2.applicationinsights.IO</span><span class="sxs-lookup"><span data-stu-id="571fb-168">api2.applicationinsights.io</span></span><br/><span data-ttu-id="571fb-169">api3.applicationinsights.IO</span><span class="sxs-lookup"><span data-stu-id="571fb-169">api3.applicationinsights.io</span></span><br/><span data-ttu-id="571fb-170">api4.applicationinsights.IO</span><span class="sxs-lookup"><span data-stu-id="571fb-170">api4.applicationinsights.io</span></span><br/><span data-ttu-id="571fb-171">api5.applicationinsights.IO</span><span class="sxs-lookup"><span data-stu-id="571fb-171">api5.applicationinsights.io</span></span> |<span data-ttu-id="571fb-172">13.82.26.252</span><span class="sxs-lookup"><span data-stu-id="571fb-172">13.82.26.252</span></span><br/><span data-ttu-id="571fb-173">40.76.213.73</span><span class="sxs-lookup"><span data-stu-id="571fb-173">40.76.213.73</span></span> |<span data-ttu-id="571fb-174">80,443</span><span class="sxs-lookup"><span data-stu-id="571fb-174">80,443</span></span> |
| <span data-ttu-id="571fb-175">Documentos de API</span><span class="sxs-lookup"><span data-stu-id="571fb-175">API docs</span></span> |<span data-ttu-id="571fb-176">Dev.applicationinsights.IO</span><span class="sxs-lookup"><span data-stu-id="571fb-176">dev.applicationinsights.io</span></span><br/><span data-ttu-id="571fb-177">Dev.applicationinsights.microsoft.com</span><span class="sxs-lookup"><span data-stu-id="571fb-177">dev.applicationinsights.microsoft.com</span></span><br/><span data-ttu-id="571fb-178">Dev.aisvc.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="571fb-178">dev.aisvc.visualstudio.com</span></span><br/><span data-ttu-id="571fb-179">www.applicationinsights.IO</span><span class="sxs-lookup"><span data-stu-id="571fb-179">www.applicationinsights.io</span></span><br/><span data-ttu-id="571fb-180">www.applicationinsights.microsoft.com</span><span class="sxs-lookup"><span data-stu-id="571fb-180">www.applicationinsights.microsoft.com</span></span><br/><span data-ttu-id="571fb-181">www.aisvc.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="571fb-181">www.aisvc.visualstudio.com</span></span> |<span data-ttu-id="571fb-182">13.82.24.149</span><span class="sxs-lookup"><span data-stu-id="571fb-182">13.82.24.149</span></span><br/><span data-ttu-id="571fb-183">40.114.82.10</span><span class="sxs-lookup"><span data-stu-id="571fb-183">40.114.82.10</span></span> |<span data-ttu-id="571fb-184">80,443</span><span class="sxs-lookup"><span data-stu-id="571fb-184">80,443</span></span> |
| <span data-ttu-id="571fb-185">API interno</span><span class="sxs-lookup"><span data-stu-id="571fb-185">Internal API</span></span> |<span data-ttu-id="571fb-186">aigs.aisvc.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="571fb-186">aigs.aisvc.visualstudio.com</span></span><br/><span data-ttu-id="571fb-187">aigs1.aisvc.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="571fb-187">aigs1.aisvc.visualstudio.com</span></span><br/><span data-ttu-id="571fb-188">aigs2.aisvc.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="571fb-188">aigs2.aisvc.visualstudio.com</span></span><br/><span data-ttu-id="571fb-189">aigs3.aisvc.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="571fb-189">aigs3.aisvc.visualstudio.com</span></span><br/><span data-ttu-id="571fb-190">aigs4.aisvc.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="571fb-190">aigs4.aisvc.visualstudio.com</span></span><br/><span data-ttu-id="571fb-191">aigs5.aisvc.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="571fb-191">aigs5.aisvc.visualstudio.com</span></span><br/><span data-ttu-id="571fb-192">aigs6.aisvc.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="571fb-192">aigs6.aisvc.visualstudio.com</span></span> |<span data-ttu-id="571fb-193">dinâmica</span><span class="sxs-lookup"><span data-stu-id="571fb-193">dynamic</span></span>|<span data-ttu-id="571fb-194">443</span><span class="sxs-lookup"><span data-stu-id="571fb-194">443</span></span> |

## <a name="application-insights-analytics"></a><span data-ttu-id="571fb-195">Application Insights Analytics</span><span class="sxs-lookup"><span data-stu-id="571fb-195">Application Insights Analytics</span></span>

| <span data-ttu-id="571fb-196">Objetivo</span><span class="sxs-lookup"><span data-stu-id="571fb-196">Purpose</span></span> | <span data-ttu-id="571fb-197">URI</span><span class="sxs-lookup"><span data-stu-id="571fb-197">URI</span></span> | <span data-ttu-id="571fb-198">IP</span><span class="sxs-lookup"><span data-stu-id="571fb-198">IP</span></span> | <span data-ttu-id="571fb-199">Portas</span><span class="sxs-lookup"><span data-stu-id="571fb-199">Ports</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="571fb-200">Portal da análise</span><span class="sxs-lookup"><span data-stu-id="571fb-200">Analytics Portal</span></span> | <span data-ttu-id="571fb-201">Analytics.applicationinsights.IO</span><span class="sxs-lookup"><span data-stu-id="571fb-201">analytics.applicationinsights.io</span></span> | <span data-ttu-id="571fb-202">dinâmica</span><span class="sxs-lookup"><span data-stu-id="571fb-202">dynamic</span></span> | <span data-ttu-id="571fb-203">80,443</span><span class="sxs-lookup"><span data-stu-id="571fb-203">80,443</span></span> |
| <span data-ttu-id="571fb-204">CDN</span><span class="sxs-lookup"><span data-stu-id="571fb-204">CDN</span></span> | <span data-ttu-id="571fb-205">applicationanalytics.azureedge.NET</span><span class="sxs-lookup"><span data-stu-id="571fb-205">applicationanalytics.azureedge.net</span></span> | <span data-ttu-id="571fb-206">dinâmica</span><span class="sxs-lookup"><span data-stu-id="571fb-206">dynamic</span></span> | <span data-ttu-id="571fb-207">80,443</span><span class="sxs-lookup"><span data-stu-id="571fb-207">80,443</span></span> |
| <span data-ttu-id="571fb-208">Suporte de dados CDN</span><span class="sxs-lookup"><span data-stu-id="571fb-208">Media CDN</span></span> | <span data-ttu-id="571fb-209">applicationanalyticsmedia.azureedge.NET</span><span class="sxs-lookup"><span data-stu-id="571fb-209">applicationanalyticsmedia.azureedge.net</span></span> | <span data-ttu-id="571fb-210">dinâmica</span><span class="sxs-lookup"><span data-stu-id="571fb-210">dynamic</span></span> | <span data-ttu-id="571fb-211">80,443</span><span class="sxs-lookup"><span data-stu-id="571fb-211">80,443</span></span> |

<span data-ttu-id="571fb-212">Nota: *. applicationinsights.io domínio pertence a equipa do Application Insights.</span><span class="sxs-lookup"><span data-stu-id="571fb-212">Note: *.applicationinsights.io domain is owned by Application Insights team.</span></span>

## <a name="application-insights-azure-portal-extension"></a><span data-ttu-id="571fb-213">Application Insights extensão de Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="571fb-213">Application Insights Azure Portal Extension</span></span>

| <span data-ttu-id="571fb-214">Objetivo</span><span class="sxs-lookup"><span data-stu-id="571fb-214">Purpose</span></span> | <span data-ttu-id="571fb-215">URI</span><span class="sxs-lookup"><span data-stu-id="571fb-215">URI</span></span> | <span data-ttu-id="571fb-216">IP</span><span class="sxs-lookup"><span data-stu-id="571fb-216">IP</span></span> | <span data-ttu-id="571fb-217">Portas</span><span class="sxs-lookup"><span data-stu-id="571fb-217">Ports</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="571fb-218">Extensão do Application Insights</span><span class="sxs-lookup"><span data-stu-id="571fb-218">Application Insights Extension</span></span> | <span data-ttu-id="571fb-219">stamp2.App.insightsportal.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="571fb-219">stamp2.app.insightsportal.visualstudio.com</span></span> | <span data-ttu-id="571fb-220">dinâmica</span><span class="sxs-lookup"><span data-stu-id="571fb-220">dynamic</span></span> | <span data-ttu-id="571fb-221">80,443</span><span class="sxs-lookup"><span data-stu-id="571fb-221">80,443</span></span> |
| <span data-ttu-id="571fb-222">Extensão do Application Insights CDN</span><span class="sxs-lookup"><span data-stu-id="571fb-222">Application Insights Extension CDN</span></span> | <span data-ttu-id="571fb-223">insightsportal-prod2-cdn.aisvc.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="571fb-223">insightsportal-prod2-cdn.aisvc.visualstudio.com</span></span><br/><span data-ttu-id="571fb-224">insightsportal-prod2 asiae cdn.aisvc.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="571fb-224">insightsportal-prod2-asiae-cdn.aisvc.visualstudio.com</span></span><br/><span data-ttu-id="571fb-225">insightsportal-cdn-aimon.applicationinsights.io</span><span class="sxs-lookup"><span data-stu-id="571fb-225">insightsportal-cdn-aimon.applicationinsights.io</span></span> | <span data-ttu-id="571fb-226">dinâmica</span><span class="sxs-lookup"><span data-stu-id="571fb-226">dynamic</span></span> | <span data-ttu-id="571fb-227">80,443</span><span class="sxs-lookup"><span data-stu-id="571fb-227">80,443</span></span> |

## <a name="application-insights-sdks"></a><span data-ttu-id="571fb-228">SDKs do Application Insights</span><span class="sxs-lookup"><span data-stu-id="571fb-228">Application Insights SDKs</span></span>

| <span data-ttu-id="571fb-229">Objetivo</span><span class="sxs-lookup"><span data-stu-id="571fb-229">Purpose</span></span> | <span data-ttu-id="571fb-230">URI</span><span class="sxs-lookup"><span data-stu-id="571fb-230">URI</span></span> | <span data-ttu-id="571fb-231">IP</span><span class="sxs-lookup"><span data-stu-id="571fb-231">IP</span></span> | <span data-ttu-id="571fb-232">Portas</span><span class="sxs-lookup"><span data-stu-id="571fb-232">Ports</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="571fb-233">SDK JS CDN do Application Insights</span><span class="sxs-lookup"><span data-stu-id="571fb-233">Application Insights JS SDK CDN</span></span> | <span data-ttu-id="571fb-234">az416426.vo.msecnd.NET</span><span class="sxs-lookup"><span data-stu-id="571fb-234">az416426.vo.msecnd.net</span></span> | <span data-ttu-id="571fb-235">dinâmica</span><span class="sxs-lookup"><span data-stu-id="571fb-235">dynamic</span></span> | <span data-ttu-id="571fb-236">80,443</span><span class="sxs-lookup"><span data-stu-id="571fb-236">80,443</span></span> |
| <span data-ttu-id="571fb-237">Application Insights Java SDK</span><span class="sxs-lookup"><span data-stu-id="571fb-237">Application Insights Java SDK</span></span> | <span data-ttu-id="571fb-238">aijavasdk.blob.Core.Windows.NET</span><span class="sxs-lookup"><span data-stu-id="571fb-238">aijavasdk.blob.core.windows.net</span></span> | <span data-ttu-id="571fb-239">dinâmica</span><span class="sxs-lookup"><span data-stu-id="571fb-239">dynamic</span></span> | <span data-ttu-id="571fb-240">80,443</span><span class="sxs-lookup"><span data-stu-id="571fb-240">80,443</span></span> |

## <a name="profiler"></a><span data-ttu-id="571fb-241">Gerador de perfis</span><span class="sxs-lookup"><span data-stu-id="571fb-241">Profiler</span></span>

| <span data-ttu-id="571fb-242">Objetivo</span><span class="sxs-lookup"><span data-stu-id="571fb-242">Purpose</span></span> | <span data-ttu-id="571fb-243">URI</span><span class="sxs-lookup"><span data-stu-id="571fb-243">URI</span></span> | <span data-ttu-id="571fb-244">IP</span><span class="sxs-lookup"><span data-stu-id="571fb-244">IP</span></span> | <span data-ttu-id="571fb-245">Portas</span><span class="sxs-lookup"><span data-stu-id="571fb-245">Ports</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="571fb-246">Agente</span><span class="sxs-lookup"><span data-stu-id="571fb-246">Agent</span></span> | <span data-ttu-id="571fb-247">Agent.azureserviceprofiler.NET</span><span class="sxs-lookup"><span data-stu-id="571fb-247">agent.azureserviceprofiler.net</span></span><br/><span data-ttu-id="571fb-248">*. agent.azureserviceprofiler.net</span><span class="sxs-lookup"><span data-stu-id="571fb-248">*.agent.azureserviceprofiler.net</span></span> | <span data-ttu-id="571fb-249">dinâmica</span><span class="sxs-lookup"><span data-stu-id="571fb-249">dynamic</span></span> | <span data-ttu-id="571fb-250">443</span><span class="sxs-lookup"><span data-stu-id="571fb-250">443</span></span>
| <span data-ttu-id="571fb-251">Portal</span><span class="sxs-lookup"><span data-stu-id="571fb-251">Portal</span></span> | <span data-ttu-id="571fb-252">gateway.azureserviceprofiler.NET</span><span class="sxs-lookup"><span data-stu-id="571fb-252">gateway.azureserviceprofiler.net</span></span> | <span data-ttu-id="571fb-253">dinâmica</span><span class="sxs-lookup"><span data-stu-id="571fb-253">dynamic</span></span> | <span data-ttu-id="571fb-254">443</span><span class="sxs-lookup"><span data-stu-id="571fb-254">443</span></span>
| <span data-ttu-id="571fb-255">Armazenamento</span><span class="sxs-lookup"><span data-stu-id="571fb-255">Storage</span></span> | <span data-ttu-id="571fb-256">*. core.windows.net</span><span class="sxs-lookup"><span data-stu-id="571fb-256">*.core.windows.net</span></span> | <span data-ttu-id="571fb-257">dinâmica</span><span class="sxs-lookup"><span data-stu-id="571fb-257">dynamic</span></span> | <span data-ttu-id="571fb-258">443</span><span class="sxs-lookup"><span data-stu-id="571fb-258">443</span></span>

## <a name="snapshot-debugger"></a><span data-ttu-id="571fb-259">Depurador de Instantâneos</span><span class="sxs-lookup"><span data-stu-id="571fb-259">Snapshot Debugger</span></span>

| <span data-ttu-id="571fb-260">Objetivo</span><span class="sxs-lookup"><span data-stu-id="571fb-260">Purpose</span></span> | <span data-ttu-id="571fb-261">URI</span><span class="sxs-lookup"><span data-stu-id="571fb-261">URI</span></span> | <span data-ttu-id="571fb-262">IP</span><span class="sxs-lookup"><span data-stu-id="571fb-262">IP</span></span> | <span data-ttu-id="571fb-263">Portas</span><span class="sxs-lookup"><span data-stu-id="571fb-263">Ports</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="571fb-264">Agente</span><span class="sxs-lookup"><span data-stu-id="571fb-264">Agent</span></span> | <span data-ttu-id="571fb-265">ppe.azureserviceprofiler.NET</span><span class="sxs-lookup"><span data-stu-id="571fb-265">ppe.azureserviceprofiler.net</span></span><br/><span data-ttu-id="571fb-266">*. ppe.azureserviceprofiler.net</span><span class="sxs-lookup"><span data-stu-id="571fb-266">*.ppe.azureserviceprofiler.net</span></span> | <span data-ttu-id="571fb-267">dinâmica</span><span class="sxs-lookup"><span data-stu-id="571fb-267">dynamic</span></span> | <span data-ttu-id="571fb-268">443</span><span class="sxs-lookup"><span data-stu-id="571fb-268">443</span></span>
| <span data-ttu-id="571fb-269">Portal</span><span class="sxs-lookup"><span data-stu-id="571fb-269">Portal</span></span> | <span data-ttu-id="571fb-270">ppe.gateway.azureserviceprofiler.NET</span><span class="sxs-lookup"><span data-stu-id="571fb-270">ppe.gateway.azureserviceprofiler.net</span></span> | <span data-ttu-id="571fb-271">dinâmica</span><span class="sxs-lookup"><span data-stu-id="571fb-271">dynamic</span></span> | <span data-ttu-id="571fb-272">443</span><span class="sxs-lookup"><span data-stu-id="571fb-272">443</span></span>
| <span data-ttu-id="571fb-273">Armazenamento</span><span class="sxs-lookup"><span data-stu-id="571fb-273">Storage</span></span> | <span data-ttu-id="571fb-274">*. core.windows.net</span><span class="sxs-lookup"><span data-stu-id="571fb-274">*.core.windows.net</span></span> | <span data-ttu-id="571fb-275">dinâmica</span><span class="sxs-lookup"><span data-stu-id="571fb-275">dynamic</span></span> | <span data-ttu-id="571fb-276">443</span><span class="sxs-lookup"><span data-stu-id="571fb-276">443</span></span>
