---
title: aaaAzure arquitetura de conectividade da base de dados SQL | Microsoft Docs
description: "Este documento explica Olá Azure SQLDB conectividade arquitetura no Azure ou a partir de fora do Azure."
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: monicar
ms.assetid: 
ms.service: sql-database
ms.custom: DBs & servers
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 06/05/2017
ms.author: carlrab
ms.openlocfilehash: 917df6d88a16f1b841b617fb2a53025b4d14d034
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sql-database-connectivity-architecture"></a><span data-ttu-id="d8cce-103">Arquitetura de conectividade de base de dados SQL do Azure</span><span class="sxs-lookup"><span data-stu-id="d8cce-103">Azure SQL Database Connectivity Architecture</span></span> 

<span data-ttu-id="d8cce-104">Este artigo explica a arquitetura de conectividade de base de dados do Azure SQL Olá e explica a forma como os diferentes componentes Olá funcionarem toodirect tráfego tooyour instância SQL Database do Azure.</span><span class="sxs-lookup"><span data-stu-id="d8cce-104">This article explains hello Azure SQL Database connectivity architecture and explains how hello different components function toodirect traffic tooyour instance of Azure SQL Database.</span></span> <span data-ttu-id="d8cce-105">Estes componentes de conectividade da SQL Database do Azure funcionarem toohello de tráfego de rede toodirect da base de dados do Azure com os clientes ligar a partir de dentro do Azure e com os clientes ligar a partir de fora do Azure.</span><span class="sxs-lookup"><span data-stu-id="d8cce-105">These Azure SQL Database connectivity components function toodirect network traffic toohello Azure database with clients connecting from within Azure and with clients connecting from outside of Azure.</span></span> <span data-ttu-id="d8cce-106">Este artigo fornece também toochange de amostras de script como ocorre a conectividade e considerações de Olá relacionadas com definições de conetividade do toochanging Olá predefinido.</span><span class="sxs-lookup"><span data-stu-id="d8cce-106">This article also provides script samples toochange how connectivity occurs, and hello considerations related toochanging hello default connectivity settings.</span></span> <span data-ttu-id="d8cce-107">Se existirem quaisquer perguntas depois de ler este artigo, entre em contacto com Dhruv em dmalik@microsoft.com.</span><span class="sxs-lookup"><span data-stu-id="d8cce-107">If there are any questions after reading this article, please contact Dhruv at dmalik@microsoft.com.</span></span> 

## <a name="connectivity-architecture"></a><span data-ttu-id="d8cce-108">Arquitetura de conectividade</span><span class="sxs-lookup"><span data-stu-id="d8cce-108">Connectivity architecture</span></span>

<span data-ttu-id="d8cce-109">Olá diagrama a seguir fornece uma descrição geral de alto nível de Olá arquitetura de conectividade da SQL Database do Azure.</span><span class="sxs-lookup"><span data-stu-id="d8cce-109">hello following diagram provides a high-level overview of hello Azure SQL Database connectivity architecture.</span></span> 

![Descrição geral da arquitetura](./media/sql-database-connectivity-architecture/architecture-overview.png)


<span data-ttu-id="d8cce-111">Olá passos seguintes descrevem como uma ligação é estabelecida tooan SQL database do Azure através de Olá SQL Database do Azure software Balanceador de carga (SLB) e o gateway do Olá SQL Database do Azure.</span><span class="sxs-lookup"><span data-stu-id="d8cce-111">hello following steps describe how a connection is established tooan Azure SQL database through hello Azure SQL Database software load-balancer (SLB) and hello Azure SQL Database gateway.</span></span>

- <span data-ttu-id="d8cce-112">Os clientes no Azure ou fora do Azure ligam toohello SLB, que tem um endereço IP público e escuta na porta 1433.</span><span class="sxs-lookup"><span data-stu-id="d8cce-112">Clients within Azure or outside of Azure connect toohello SLB, which has a public IP address and listens on port 1433.</span></span>
- <span data-ttu-id="d8cce-113">Olá SLB direciona o gateway do tráfego toohello SQL Database do Azure.</span><span class="sxs-lookup"><span data-stu-id="d8cce-113">hello SLB directs traffic toohello Azure SQL Database gateway.</span></span>
- <span data-ttu-id="d8cce-114">gateway de Olá redireciona o tráfego de Olá toohello middleware de proxy correta.</span><span class="sxs-lookup"><span data-stu-id="d8cce-114">hello gateway redirects hello traffic toohello correct proxy middleware.</span></span>
- <span data-ttu-id="d8cce-115">Olá proxy middleware redireciona Olá tráfego toohello adequado SQL database do Azure.</span><span class="sxs-lookup"><span data-stu-id="d8cce-115">hello proxy middleware redirects hello traffic toohello appropriate Azure SQL database.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d8cce-116">Cada um destes componentes tem ataques denial of protection service (DDoS distribuídos) incorporada na rede de Olá e a camada de aplicação de Olá.</span><span class="sxs-lookup"><span data-stu-id="d8cce-116">Each of these components has distributed denial of service (DDoS) protection built-in at hello network and hello app layer.</span></span>
>

## <a name="connectivity-from-within-azure"></a><span data-ttu-id="d8cce-117">Conectividade no Azure</span><span class="sxs-lookup"><span data-stu-id="d8cce-117">Connectivity from within Azure</span></span>

<span data-ttu-id="d8cce-118">Se estiver a ligar no Azure, as suas ligações tem uma política de ligação do **redirecionar** por predefinição.</span><span class="sxs-lookup"><span data-stu-id="d8cce-118">If you are connecting from within Azure, your connections have a connection policy of **Redirect** by default.</span></span> <span data-ttu-id="d8cce-119">Uma política do **redirecionar** significa que as ligações após a conclusão da sessão TCP Olá toohello estabelecida SQL database do Azure, sessão de cliente Olá, em seguida, redirecionado toohello proxy middleware com um alteração toohello destino IP virtual do que um Olá SQL Database do Azure gateway toothat de Olá middleware de proxy.</span><span class="sxs-lookup"><span data-stu-id="d8cce-119">A policy of **Redirect** means that connections after hello TCP session is established toohello Azure SQL database, hello client session is then redirected toohello proxy middleware with a change toohello destination virtual IP from that of hello Azure SQL Database gateway toothat of hello proxy middleware.</span></span> <span data-ttu-id="d8cce-120">Depois disso, todos os pacotes subsequentes fluir diretamente através do middleware de proxy Olá, ignorando o gateway do Olá SQL Database do Azure.</span><span class="sxs-lookup"><span data-stu-id="d8cce-120">Thereafter, all subsequent packets flow directly via hello proxy middleware, bypassing hello Azure SQL Database gateway.</span></span> <span data-ttu-id="d8cce-121">Olá seguinte diagrama ilustra o fluxo de tráfego.</span><span class="sxs-lookup"><span data-stu-id="d8cce-121">hello following diagram illustrates this traffic flow.</span></span>

![Descrição geral da arquitetura](./media/sql-database-connectivity-architecture/connectivity-from-within-azure.png)

## <a name="connectivity-from-outside-of-azure"></a><span data-ttu-id="d8cce-123">Conectividade de fora do Azure</span><span class="sxs-lookup"><span data-stu-id="d8cce-123">Connectivity from outside of Azure</span></span>

<span data-ttu-id="d8cce-124">Se estiver a ligar a partir de fora do Azure, as suas ligações tem uma política de ligação do **Proxy** por predefinição.</span><span class="sxs-lookup"><span data-stu-id="d8cce-124">If you are connecting from outside Azure, your connections have a connection policy of **Proxy** by default.</span></span> <span data-ttu-id="d8cce-125">Uma política do **Proxy** Olá, significa que sessão TCP Olá é estabelecida através do gateway da SQL Database do Azure de Olá e todos os pacotes subsequentes fluxo através do gateway.</span><span class="sxs-lookup"><span data-stu-id="d8cce-125">A policy of **Proxy** means that hello TCP session is established via hello Azure SQL Database gateway and all subsequent packets flow via hello gateway.</span></span> <span data-ttu-id="d8cce-126">Olá seguinte diagrama ilustra o fluxo de tráfego.</span><span class="sxs-lookup"><span data-stu-id="d8cce-126">hello following diagram illustrates this traffic flow.</span></span>

![Descrição geral da arquitetura](./media/sql-database-connectivity-architecture/connectivity-from-outside-azure.png)

## <a name="azure-sql-database-gateway-ip-addresses"></a><span data-ttu-id="d8cce-128">Endereços de IP do gateway de base de dados SQL do Azure</span><span class="sxs-lookup"><span data-stu-id="d8cce-128">Azure SQL Database gateway IP addresses</span></span>

<span data-ttu-id="d8cce-129">tooconnect tooan SQL database do Azure a partir dos recursos no local, terá de gateway de SQL Database do Azure de toohello de tráfego de rede de saída de tooallow para sua região do Azure.</span><span class="sxs-lookup"><span data-stu-id="d8cce-129">tooconnect tooan Azure SQL database from on-premises resources, you need tooallow outbound network traffic toohello Azure SQL Database gateway for your Azure region.</span></span> <span data-ttu-id="d8cce-130">As suas ligações aceda apenas através do gateway de Olá ao ligar-se no modo de Proxy, que é a predefinição de Olá quando ligar a partir de recursos no local.</span><span class="sxs-lookup"><span data-stu-id="d8cce-130">Your connections only go via hello gateway when connecting in Proxy mode, which is hello default when connecting from on-premises resources.</span></span>

<span data-ttu-id="d8cce-131">Olá listas de tabela a seguir Olá IPs primária e secundária do gateway de base de dados do Azure SQL Olá para todas as regiões de dados.</span><span class="sxs-lookup"><span data-stu-id="d8cce-131">hello following table lists hello primary and secondary IPs of hello Azure SQL Database gateway for all data regions.</span></span> <span data-ttu-id="d8cce-132">Para algumas regiões, existem dois endereços IP.</span><span class="sxs-lookup"><span data-stu-id="d8cce-132">For some regions, there are two IP addresses.</span></span> <span data-ttu-id="d8cce-133">Estas regiões, endereço IP primário Olá é o endereço IP atual Olá do gateway de Olá e segundo endereço IP Olá é um endereço IP de ativação pós-falha.</span><span class="sxs-lookup"><span data-stu-id="d8cce-133">In these regions, hello primary IP address is hello current IP address of hello gateway and hello second IP address is a failover IP address.</span></span> <span data-ttu-id="d8cce-134">o endereço de ativação pós-falha de Olá é Olá endereço toowhich pode mover a servidor tookeep Olá serviço disponibilidade elevada.</span><span class="sxs-lookup"><span data-stu-id="d8cce-134">hello failover address is hello address toowhich we might move your server tookeep hello service availability high.</span></span> <span data-ttu-id="d8cce-135">Para estas regiões, recomendamos que permitem a saída tooboth endereços IP Olá.</span><span class="sxs-lookup"><span data-stu-id="d8cce-135">For these regions, we recommend that you allow outbound tooboth hello IP addresses.</span></span> <span data-ttu-id="d8cce-136">endereço IP segundo Olá pertencente à Microsoft e não escutar todos os serviços até ser ativado através de ligações de tooaccept da SQL Database do Azure.</span><span class="sxs-lookup"><span data-stu-id="d8cce-136">hello second IP address is owned by Microsoft and does not listen in on any services until it is activated by Azure SQL Database tooaccept connections.</span></span>

| <span data-ttu-id="d8cce-137">Nome da Região</span><span class="sxs-lookup"><span data-stu-id="d8cce-137">Region Name</span></span> | <span data-ttu-id="d8cce-138">Endereço IP primário</span><span class="sxs-lookup"><span data-stu-id="d8cce-138">Primary IP address</span></span> | <span data-ttu-id="d8cce-139">Endereço IP secundário</span><span class="sxs-lookup"><span data-stu-id="d8cce-139">Secondary IP address</span></span> |
| --- | --- |--- |
| <span data-ttu-id="d8cce-140">Leste da Austrália</span><span class="sxs-lookup"><span data-stu-id="d8cce-140">Australia East</span></span> | <span data-ttu-id="d8cce-141">191.238.66.109</span><span class="sxs-lookup"><span data-stu-id="d8cce-141">191.238.66.109</span></span> | <span data-ttu-id="d8cce-142">13.75.149.87</span><span class="sxs-lookup"><span data-stu-id="d8cce-142">13.75.149.87</span></span> |
| <span data-ttu-id="d8cce-143">Sudeste da Austrália</span><span class="sxs-lookup"><span data-stu-id="d8cce-143">Australia South East</span></span> | <span data-ttu-id="d8cce-144">191.239.192.109</span><span class="sxs-lookup"><span data-stu-id="d8cce-144">191.239.192.109</span></span> | <span data-ttu-id="d8cce-145">13.73.109.251</span><span class="sxs-lookup"><span data-stu-id="d8cce-145">13.73.109.251</span></span> |
| <span data-ttu-id="d8cce-146">Sul do Brasil</span><span class="sxs-lookup"><span data-stu-id="d8cce-146">Brazil South</span></span> | <span data-ttu-id="d8cce-147">104.41.11.5</span><span class="sxs-lookup"><span data-stu-id="d8cce-147">104.41.11.5</span></span> | |    
| <span data-ttu-id="d8cce-148">Canadá Central</span><span class="sxs-lookup"><span data-stu-id="d8cce-148">Canada Central</span></span> | <span data-ttu-id="d8cce-149">40.85.224.249</span><span class="sxs-lookup"><span data-stu-id="d8cce-149">40.85.224.249</span></span> | |    
| <span data-ttu-id="d8cce-150">Leste do Canadá</span><span class="sxs-lookup"><span data-stu-id="d8cce-150">Canada East</span></span> | <span data-ttu-id="d8cce-151">40.86.226.166</span><span class="sxs-lookup"><span data-stu-id="d8cce-151">40.86.226.166</span></span> | |
| <span data-ttu-id="d8cce-152">EUA Central</span><span class="sxs-lookup"><span data-stu-id="d8cce-152">Central US</span></span> | <span data-ttu-id="d8cce-153">23.99.160.139</span><span class="sxs-lookup"><span data-stu-id="d8cce-153">23.99.160.139</span></span> | <span data-ttu-id="d8cce-154">13.67.215.62</span><span class="sxs-lookup"><span data-stu-id="d8cce-154">13.67.215.62</span></span> |
| <span data-ttu-id="d8cce-155">Ásia Oriental</span><span class="sxs-lookup"><span data-stu-id="d8cce-155">East Asia</span></span> | <span data-ttu-id="d8cce-156">191.234.2.139</span><span class="sxs-lookup"><span data-stu-id="d8cce-156">191.234.2.139</span></span> | <span data-ttu-id="d8cce-157">52.175.33.150</span><span class="sxs-lookup"><span data-stu-id="d8cce-157">52.175.33.150</span></span> |
| <span data-ttu-id="d8cce-158">EUA Leste 1</span><span class="sxs-lookup"><span data-stu-id="d8cce-158">East US 1</span></span> | <span data-ttu-id="d8cce-159">191.238.6.43</span><span class="sxs-lookup"><span data-stu-id="d8cce-159">191.238.6.43</span></span> | <span data-ttu-id="d8cce-160">40.121.158.30</span><span class="sxs-lookup"><span data-stu-id="d8cce-160">40.121.158.30</span></span> |
| <span data-ttu-id="d8cce-161">EUA Leste 2</span><span class="sxs-lookup"><span data-stu-id="d8cce-161">East US 2</span></span> | <span data-ttu-id="d8cce-162">191.239.224.107</span><span class="sxs-lookup"><span data-stu-id="d8cce-162">191.239.224.107</span></span> | <span data-ttu-id="d8cce-163">40.79.84.180</span><span class="sxs-lookup"><span data-stu-id="d8cce-163">40.79.84.180</span></span> |
| <span data-ttu-id="d8cce-164">Índia Central</span><span class="sxs-lookup"><span data-stu-id="d8cce-164">India Central</span></span> | <span data-ttu-id="d8cce-165">104.211.96.159</span><span class="sxs-lookup"><span data-stu-id="d8cce-165">104.211.96.159</span></span>  | |   
| <span data-ttu-id="d8cce-166">Índia do Sul</span><span class="sxs-lookup"><span data-stu-id="d8cce-166">India South</span></span> | <span data-ttu-id="d8cce-167">104.211.224.146</span><span class="sxs-lookup"><span data-stu-id="d8cce-167">104.211.224.146</span></span>  | |
| <span data-ttu-id="d8cce-168">Índia Ocidental</span><span class="sxs-lookup"><span data-stu-id="d8cce-168">India West</span></span> | <span data-ttu-id="d8cce-169">104.211.160.80</span><span class="sxs-lookup"><span data-stu-id="d8cce-169">104.211.160.80</span></span> | |
| <span data-ttu-id="d8cce-170">Leste do Japão</span><span class="sxs-lookup"><span data-stu-id="d8cce-170">Japan East</span></span> | <span data-ttu-id="d8cce-171">191.237.240.43</span><span class="sxs-lookup"><span data-stu-id="d8cce-171">191.237.240.43</span></span> | <span data-ttu-id="d8cce-172">13.78.61.196</span><span class="sxs-lookup"><span data-stu-id="d8cce-172">13.78.61.196</span></span> |
| <span data-ttu-id="d8cce-173">Oeste do Japão</span><span class="sxs-lookup"><span data-stu-id="d8cce-173">Japan West</span></span> | <span data-ttu-id="d8cce-174">191.238.68.11</span><span class="sxs-lookup"><span data-stu-id="d8cce-174">191.238.68.11</span></span> | <span data-ttu-id="d8cce-175">104.214.148.156</span><span class="sxs-lookup"><span data-stu-id="d8cce-175">104.214.148.156</span></span> |
| <span data-ttu-id="d8cce-176">Coreia Central</span><span class="sxs-lookup"><span data-stu-id="d8cce-176">Korea Central</span></span> | <span data-ttu-id="d8cce-177">52.231.32.42</span><span class="sxs-lookup"><span data-stu-id="d8cce-177">52.231.32.42</span></span> | |
| <span data-ttu-id="d8cce-178">Coreia do Sul</span><span class="sxs-lookup"><span data-stu-id="d8cce-178">Korea South</span></span> | <span data-ttu-id="d8cce-179">52.231.200.86</span><span class="sxs-lookup"><span data-stu-id="d8cce-179">52.231.200.86</span></span> |  |
| <span data-ttu-id="d8cce-180">EUA Centro-Norte</span><span class="sxs-lookup"><span data-stu-id="d8cce-180">North Central US</span></span> | <span data-ttu-id="d8cce-181">23.98.55.75</span><span class="sxs-lookup"><span data-stu-id="d8cce-181">23.98.55.75</span></span> | <span data-ttu-id="d8cce-182">23.96.178.199</span><span class="sxs-lookup"><span data-stu-id="d8cce-182">23.96.178.199</span></span> |
| <span data-ttu-id="d8cce-183">Europa do Norte</span><span class="sxs-lookup"><span data-stu-id="d8cce-183">North Europe</span></span> | <span data-ttu-id="d8cce-184">191.235.193.75</span><span class="sxs-lookup"><span data-stu-id="d8cce-184">191.235.193.75</span></span> | <span data-ttu-id="d8cce-185">40.113.93.91</span><span class="sxs-lookup"><span data-stu-id="d8cce-185">40.113.93.91</span></span> |
| <span data-ttu-id="d8cce-186">EUA Centro-Sul</span><span class="sxs-lookup"><span data-stu-id="d8cce-186">South Central US</span></span> | <span data-ttu-id="d8cce-187">23.98.162.75</span><span class="sxs-lookup"><span data-stu-id="d8cce-187">23.98.162.75</span></span> | <span data-ttu-id="d8cce-188">13.66.62.124</span><span class="sxs-lookup"><span data-stu-id="d8cce-188">13.66.62.124</span></span> |
| <span data-ttu-id="d8cce-189">Sudeste Asiático</span><span class="sxs-lookup"><span data-stu-id="d8cce-189">South East Asia</span></span> | <span data-ttu-id="d8cce-190">23.100.117.95</span><span class="sxs-lookup"><span data-stu-id="d8cce-190">23.100.117.95</span></span> | <span data-ttu-id="d8cce-191">104.43.15.0</span><span class="sxs-lookup"><span data-stu-id="d8cce-191">104.43.15.0</span></span> |
| <span data-ttu-id="d8cce-192">Norte do Reino Unido</span><span class="sxs-lookup"><span data-stu-id="d8cce-192">UK North</span></span> | <span data-ttu-id="d8cce-193">13.87.97.210</span><span class="sxs-lookup"><span data-stu-id="d8cce-193">13.87.97.210</span></span> | |
| <span data-ttu-id="d8cce-194">Sul do RU 1</span><span class="sxs-lookup"><span data-stu-id="d8cce-194">UK South 1</span></span> | <span data-ttu-id="d8cce-195">51.140.184.11</span><span class="sxs-lookup"><span data-stu-id="d8cce-195">51.140.184.11</span></span> | |    
| <span data-ttu-id="d8cce-196">Sul do Reino Unido 2</span><span class="sxs-lookup"><span data-stu-id="d8cce-196">UK South 2</span></span> | <span data-ttu-id="d8cce-197">13.87.34.7</span><span class="sxs-lookup"><span data-stu-id="d8cce-197">13.87.34.7</span></span> | |
| <span data-ttu-id="d8cce-198">Reino Unido Oeste</span><span class="sxs-lookup"><span data-stu-id="d8cce-198">UK West</span></span> | <span data-ttu-id="d8cce-199">51.141.8.11</span><span class="sxs-lookup"><span data-stu-id="d8cce-199">51.141.8.11</span></span>  | |
| <span data-ttu-id="d8cce-200">EUA Centro-Oeste</span><span class="sxs-lookup"><span data-stu-id="d8cce-200">West Central US</span></span> | <span data-ttu-id="d8cce-201">13.78.145.25</span><span class="sxs-lookup"><span data-stu-id="d8cce-201">13.78.145.25</span></span> | |
| <span data-ttu-id="d8cce-202">Europa Ocidental</span><span class="sxs-lookup"><span data-stu-id="d8cce-202">West Europe</span></span> | <span data-ttu-id="d8cce-203">191.237.232.75</span><span class="sxs-lookup"><span data-stu-id="d8cce-203">191.237.232.75</span></span> | <span data-ttu-id="d8cce-204">40.68.37.158</span><span class="sxs-lookup"><span data-stu-id="d8cce-204">40.68.37.158</span></span> |
| <span data-ttu-id="d8cce-205">EUA oeste 1</span><span class="sxs-lookup"><span data-stu-id="d8cce-205">West US 1</span></span> | <span data-ttu-id="d8cce-206">23.99.34.75</span><span class="sxs-lookup"><span data-stu-id="d8cce-206">23.99.34.75</span></span> | <span data-ttu-id="d8cce-207">104.42.238.205</span><span class="sxs-lookup"><span data-stu-id="d8cce-207">104.42.238.205</span></span> |
| <span data-ttu-id="d8cce-208">EUA Oeste 2</span><span class="sxs-lookup"><span data-stu-id="d8cce-208">West US 2</span></span> | <span data-ttu-id="d8cce-209">13.66.226.202</span><span class="sxs-lookup"><span data-stu-id="d8cce-209">13.66.226.202</span></span>  | |
||||

## <a name="change-azure-sql-database-connection-policy"></a><span data-ttu-id="d8cce-210">Alterar a política de ligação de SQL Database do Azure</span><span class="sxs-lookup"><span data-stu-id="d8cce-210">Change Azure SQL Database connection policy</span></span>

<span data-ttu-id="d8cce-211">Olá toochange política de ligação de SQL Database do Azure para um servidor de base de dados do Azure SQL, utilize Olá [REST API](https://msdn.microsoft.com/library/azure/mt604439.aspx).</span><span class="sxs-lookup"><span data-stu-id="d8cce-211">toochange hello Azure SQL Database connection policy for an Azure SQL Database server, use hello [REST API](https://msdn.microsoft.com/library/azure/mt604439.aspx).</span></span> 

- <span data-ttu-id="d8cce-212">Se a política de ligação for definida demasiado**Proxy**, todos os pacotes de fluxo através do gateway da SQL Database do Azure de Olá de rede.</span><span class="sxs-lookup"><span data-stu-id="d8cce-212">If your connection policy is set too**Proxy**, all network packets flow via hello Azure SQL Database gateway.</span></span> <span data-ttu-id="d8cce-213">Para esta definição, terá de IP do gateway tooallow tooonly saída Olá SQL Database do Azure.</span><span class="sxs-lookup"><span data-stu-id="d8cce-213">For this setting, you need tooallow outbound tooonly hello Azure SQL Database gateway IP.</span></span> <span data-ttu-id="d8cce-214">Utilizar uma definição de **Proxy** tem a latência mais que uma definição de **redirecionar**.</span><span class="sxs-lookup"><span data-stu-id="d8cce-214">Using a setting of **Proxy** has more latency than a setting of **Redirect**.</span></span> 
- <span data-ttu-id="d8cce-215">Se a política de ligação é **redirecionar**, todos os pacotes de rede diretamente fluxo toohello middleware proxy.</span><span class="sxs-lookup"><span data-stu-id="d8cce-215">If your connection policy is setting **Redirect**, all network packets flow directly toohello middleware proxy.</span></span> <span data-ttu-id="d8cce-216">Para esta definição, terá de tooallow saída toomultiple IPs.</span><span class="sxs-lookup"><span data-stu-id="d8cce-216">For this setting, you need tooallow outbound toomultiple IPs.</span></span> 

## <a name="script-toochange-connection-settings"></a><span data-ttu-id="d8cce-217">Definições de ligação do script toochange</span><span class="sxs-lookup"><span data-stu-id="d8cce-217">Script toochange connection settings</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d8cce-218">Este script requer Olá [módulo Azure PowerShell](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="d8cce-218">This script requires hello [Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>
>

<span data-ttu-id="d8cce-219">Olá script do PowerShell a seguir mostra como toochange Olá política de ligação.</span><span class="sxs-lookup"><span data-stu-id="d8cce-219">hello following PowerShell script shows how toochange hello connection policy.</span></span>

```powershell
import-module azureRm
Login-AzureRmAccount

$tenantId =  #your AAD tenant ID
$subscriptionId = #Azure SubscriptionID
$uri = #AAD uri
$authUrl = "https://login.microsoftonline.com/$tenantId"
$serverName = #sqldb server name 
$resourceGroupName=#sqldb resource group
$AuthContext = [Microsoft.IdentityModel.Clients.ActiveDirectory.AuthenticationContext]$authUrl

$result = $AuthContext.AcquireToken("https://management.core.windows.net/",
$clientId,
[Uri]$uri, 
[Microsoft.IdentityModel.Clients.ActiveDirectory.PromptBehavior]::Auto)

$authHeader = @{
'Content-Type'='application\json; '
'Authorization'=$result.CreateAuthorizationHeader()
}

#getting hello current connection property
Invoke-RestMethod -Uri "https://management.azure.com/subscriptions/$subscriptionId/resourceGroups/$resourceGroupName/providers/Microsoft.Sql/servers/$serverName/connectionPolicies/Default?api-version=2014-04-01-preview" -Method GET -Headers $authHeader

#setting hello property too‘Proxy’
$connectionType=”Proxy” <#Redirect / Default are other options#>
$body = @{properties=@{connectionType=$connectionType}} | ConvertTo-Json

Invoke-RestMethod -Uri "https://management.azure.com/subscriptions/$subscriptionId/resourceGroups/$resourceGroupName/providers/Microsoft.Sql/servers/$serverName/connectionPolicies/Default?api-version=2014-04-01-preview" -Method PUT -Headers $authHeader -Body $body -ContentType "application/json"
```

## <a name="next-steps"></a><span data-ttu-id="d8cce-220">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="d8cce-220">Next steps</span></span>

- <span data-ttu-id="d8cce-221">Para obter informações sobre como toochange Olá política de ligação de SQL Database do Azure para um servidor de base de dados do Azure SQL, consulte [Create ou política de ligação do servidor de atualização utilizando Olá REST API](https://msdn.microsoft.com/library/azure/mt604439.aspx).</span><span class="sxs-lookup"><span data-stu-id="d8cce-221">For information on how toochange hello Azure SQL Database connection policy for an Azure SQL Database server, see [Create or Update Server Connection Policy using hello REST API](https://msdn.microsoft.com/library/azure/mt604439.aspx).</span></span>
- <span data-ttu-id="d8cce-222">Para informações sobre o comportamento de ligação de SQL Database do Azure para clientes que utilizam ADO.NET 4.5 ou uma versão posterior, consulte [portas para além de 1433 para ADO.NET 4.5](sql-database-develop-direct-route-ports-adonet-v12.md).</span><span class="sxs-lookup"><span data-stu-id="d8cce-222">For information about Azure SQL Database connection behavior for clients that use ADO.NET 4.5 or a later version, see [Ports beyond 1433 for ADO.NET 4.5](sql-database-develop-direct-route-ports-adonet-v12.md).</span></span>
- <span data-ttu-id="d8cce-223">Para informações de descrição geral do desenvolvimento de aplicações gerais, consulte [descrição geral do desenvolvimento de aplicações de base de dados do SQL Server](sql-database-develop-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d8cce-223">For general application development overview information, see [SQL Database Application Development Overview](sql-database-develop-overview.md).</span></span>
