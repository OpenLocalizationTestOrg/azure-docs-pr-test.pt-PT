---
title: "aplicação de contentor do DC/OS do aaaEnable acesso tooAzure | Microsoft Docs"
description: "Como público tooenable acedam a contentores de SO/tooDC no serviço de contentor do Azure."
services: container-service
documentationcenter: 
author: sauryadas
manager: madhana
editor: 
tags: acs, azure-container-service
keywords: "Docker, Contentores, Microserviços, Mesos, Azure"
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/26/2016
ms.author: saudas
ms.custom: mvc
ms.openlocfilehash: 1ba251ba5a176a6a5e1c7831655164e380a62b27
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="enable-public-access-tooan-azure-container-service-application"></a><span data-ttu-id="41ede-104">Ativar a aplicação de serviço de contentor do Azure de tooan acesso público</span><span class="sxs-lookup"><span data-stu-id="41ede-104">Enable public access tooan Azure Container Service application</span></span>
<span data-ttu-id="41ede-105">Qualquer contentor de DC/OS em Olá ACS [agrupamento de agentes públicos](container-service-mesos-marathon-ui.md#deploy-a-docker-formatted-container) é toohello automaticamente exposto à internet.</span><span class="sxs-lookup"><span data-stu-id="41ede-105">Any DC/OS container in hello ACS [public agent pool](container-service-mesos-marathon-ui.md#deploy-a-docker-formatted-container) is automatically exposed toohello internet.</span></span> <span data-ttu-id="41ede-106">Por predefinição, as portas **80**, **443**, **8080** estão abertas e qualquer contentor (público) está a escutar as portas estão acessíveis.</span><span class="sxs-lookup"><span data-stu-id="41ede-106">By default, ports **80**, **443**, **8080** are opened, and any (public) container listening on those ports are accessible.</span></span> <span data-ttu-id="41ede-107">Este artigo mostra como tooopen mais portas para as suas aplicações no serviço de contentor do Azure.</span><span class="sxs-lookup"><span data-stu-id="41ede-107">This article shows you how tooopen more ports for your applications in Azure Container Service.</span></span>

## <a name="open-a-port-portal"></a><span data-ttu-id="41ede-108">Abrir uma porta (portal)</span><span class="sxs-lookup"><span data-stu-id="41ede-108">Open a port (portal)</span></span>
<span data-ttu-id="41ede-109">Em primeiro lugar, temos de porta de Olá tooopen que queremos.</span><span class="sxs-lookup"><span data-stu-id="41ede-109">First, we need tooopen hello port we want.</span></span>

1. <span data-ttu-id="41ede-110">Inicie sessão no portal de toohello.</span><span class="sxs-lookup"><span data-stu-id="41ede-110">Log in toohello portal.</span></span>
2. <span data-ttu-id="41ede-111">Grupo de recursos de Olá localizar que implementou Olá serviço de contentor do Azure para.</span><span class="sxs-lookup"><span data-stu-id="41ede-111">Find hello resource group that you deployed hello Azure Container Service to.</span></span>
3. <span data-ttu-id="41ede-112">Selecione o Balanceador de carga do agente de Olá (que é denominado semelhante demasiado**XXXX-agente-lb-XXXX**).</span><span class="sxs-lookup"><span data-stu-id="41ede-112">Select hello agent load balancer (which is named similar too**XXXX-agent-lb-XXXX**).</span></span>
   
    ![Balanceador de carga do serviço de contentor do Azure](./media/container-service-enable-public-access/agent-load-balancer.png)
4. <span data-ttu-id="41ede-114">Clique em **sondas** e, em seguida, **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="41ede-114">Click **Probes** and then **Add**.</span></span>
   
    ![Pesquisas de Balanceador de carga do serviço de contentor do Azure](./media/container-service-enable-public-access/add-probe.png)
5. <span data-ttu-id="41ede-116">Preencha o formulário de pesquisa de Olá e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="41ede-116">Fill out hello probe form and click **OK**.</span></span>
   
   | <span data-ttu-id="41ede-117">Campo</span><span class="sxs-lookup"><span data-stu-id="41ede-117">Field</span></span> | <span data-ttu-id="41ede-118">Descrição</span><span class="sxs-lookup"><span data-stu-id="41ede-118">Description</span></span> |
   | --- | --- |
   | <span data-ttu-id="41ede-119">Nome</span><span class="sxs-lookup"><span data-stu-id="41ede-119">Name</span></span> |<span data-ttu-id="41ede-120">Um nome descritivo da sonda Olá.</span><span class="sxs-lookup"><span data-stu-id="41ede-120">A descriptive name of hello probe.</span></span> |
   | <span data-ttu-id="41ede-121">Porta</span><span class="sxs-lookup"><span data-stu-id="41ede-121">Port</span></span> |<span data-ttu-id="41ede-122">porta de Olá de Olá tootest de contentor.</span><span class="sxs-lookup"><span data-stu-id="41ede-122">hello port of hello container tootest.</span></span> |
   | <span data-ttu-id="41ede-123">Caminho</span><span class="sxs-lookup"><span data-stu-id="41ede-123">Path</span></span> |<span data-ttu-id="41ede-124">(Quando no modo HTTP) Olá tooprobe de caminho relativo Web site.</span><span class="sxs-lookup"><span data-stu-id="41ede-124">(When in HTTP mode) hello relative website path tooprobe.</span></span> <span data-ttu-id="41ede-125">HTTPS não suportado.</span><span class="sxs-lookup"><span data-stu-id="41ede-125">HTTPS not supported.</span></span> |
   | <span data-ttu-id="41ede-126">intervalo</span><span class="sxs-lookup"><span data-stu-id="41ede-126">Interval</span></span> |<span data-ttu-id="41ede-127">Olá período de tempo entre sonda tenta, em segundos.</span><span class="sxs-lookup"><span data-stu-id="41ede-127">hello amount of time between probe attempts, in seconds.</span></span> |
   | <span data-ttu-id="41ede-128">Limiar de mau estado de funcionamento</span><span class="sxs-lookup"><span data-stu-id="41ede-128">Unhealthy threshold</span></span> |<span data-ttu-id="41ede-129">Número de sonda consecutivas tentativas antes de considerar o contentor de Olá mau estado de funcionamento.</span><span class="sxs-lookup"><span data-stu-id="41ede-129">Number of consecutive probe attempts before considering hello container unhealthy.</span></span> |
6. <span data-ttu-id="41ede-130">Novamente na propriedades Olá Olá agente de Balanceador de carga, clique em **as regras de balanceamento de carga** e, em seguida, **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="41ede-130">Back at hello properties of hello agent load balancer, click **Load balancing rules** and then **Add**.</span></span>
   
    ![Regras de Balanceador de carga de serviço de contentor do Azure](./media/container-service-enable-public-access/add-balancer-rule.png)
7. <span data-ttu-id="41ede-132">Preencha o formulário de Balanceador de carga Olá e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="41ede-132">Fill out hello load balancer form and click **OK**.</span></span>
   
   | <span data-ttu-id="41ede-133">Campo</span><span class="sxs-lookup"><span data-stu-id="41ede-133">Field</span></span> | <span data-ttu-id="41ede-134">Descrição</span><span class="sxs-lookup"><span data-stu-id="41ede-134">Description</span></span> |
   | --- | --- |
   | <span data-ttu-id="41ede-135">Nome</span><span class="sxs-lookup"><span data-stu-id="41ede-135">Name</span></span> |<span data-ttu-id="41ede-136">Um nome descritivo Olá de Balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="41ede-136">A descriptive name of hello load balancer.</span></span> |
   | <span data-ttu-id="41ede-137">Porta</span><span class="sxs-lookup"><span data-stu-id="41ede-137">Port</span></span> |<span data-ttu-id="41ede-138">porta de entrada pública de Olá.</span><span class="sxs-lookup"><span data-stu-id="41ede-138">hello public incoming port.</span></span> |
   | <span data-ttu-id="41ede-139">Porta de back-end</span><span class="sxs-lookup"><span data-stu-id="41ede-139">Backend port</span></span> |<span data-ttu-id="41ede-140">Olá interno público a porta da Olá contentor tooroute tráfego.</span><span class="sxs-lookup"><span data-stu-id="41ede-140">hello internal-public port of hello container tooroute traffic to.</span></span> |
   | <span data-ttu-id="41ede-141">Conjunto back-end</span><span class="sxs-lookup"><span data-stu-id="41ede-141">Backend pool</span></span> |<span data-ttu-id="41ede-142">contentores Olá neste conjunto estará destino Olá para este Balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="41ede-142">hello containers in this pool will be hello target for this load balancer.</span></span> |
   | <span data-ttu-id="41ede-143">Sonda</span><span class="sxs-lookup"><span data-stu-id="41ede-143">Probe</span></span> |<span data-ttu-id="41ede-144">Olá toodetermine sonda utilizada se um destino na Olá **conjunto back-end** está em bom estado.</span><span class="sxs-lookup"><span data-stu-id="41ede-144">hello probe used toodetermine if a target in hello **Backend pool** is healthy.</span></span> |
   | <span data-ttu-id="41ede-145">Persistência da sessão</span><span class="sxs-lookup"><span data-stu-id="41ede-145">Session persistence</span></span> |<span data-ttu-id="41ede-146">Determina como o tráfego de um cliente deve ser processado Olá enquanto estiver em curso sessão Olá.</span><span class="sxs-lookup"><span data-stu-id="41ede-146">Determines how traffic from a client should be handled for hello duration of hello session.</span></span><br><br><span data-ttu-id="41ede-147">**Nenhum**: os pedidos sucessivos de Olá mesmo cliente pode ser processado por qualquer contentor.</span><span class="sxs-lookup"><span data-stu-id="41ede-147">**None**: Successive requests from hello same client can be handled by any container.</span></span><br><span data-ttu-id="41ede-148">**Cliente IP**: Olá, os pedidos sucessivos de Olá mesmo IP de cliente são processadas pelo mesmo contentor.</span><span class="sxs-lookup"><span data-stu-id="41ede-148">**Client IP**: Successive requests from hello same client IP are handled by hello same container.</span></span><br><span data-ttu-id="41ede-149">**Cliente IP e protocolo**: Olá, os pedidos sucessivos de Olá mesma combinação de IP e protocolo de cliente são processadas pelo mesmo contentor.</span><span class="sxs-lookup"><span data-stu-id="41ede-149">**Client IP and protocol**: Successive requests from hello same client IP and protocol combination are handled by hello same container.</span></span> |
   | <span data-ttu-id="41ede-150">Tempo limite de inatividade</span><span class="sxs-lookup"><span data-stu-id="41ede-150">Idle timeout</span></span> |<span data-ttu-id="41ede-151">(Apenas TCP) Em minutos, Olá tookeep de tempo que um cliente TCP/HTTP abrir sem depender *ligação keep-alive* mensagens.</span><span class="sxs-lookup"><span data-stu-id="41ede-151">(TCP only) In minutes, hello time tookeep a TCP/HTTP client open without relying on *keep-alive* messages.</span></span> |

## <a name="add-a-security-rule-portal"></a><span data-ttu-id="41ede-152">Adicionar uma regra de segurança (portal)</span><span class="sxs-lookup"><span data-stu-id="41ede-152">Add a security rule (portal)</span></span>
<span data-ttu-id="41ede-153">Em seguida, temos tooadd uma regra de segurança que encaminha o tráfego da nossa porta aberta através da firewall Olá.</span><span class="sxs-lookup"><span data-stu-id="41ede-153">Next, we need tooadd a security rule that routes traffic from our opened port through hello firewall.</span></span>

1. <span data-ttu-id="41ede-154">Inicie sessão no portal de toohello.</span><span class="sxs-lookup"><span data-stu-id="41ede-154">Log in toohello portal.</span></span>
2. <span data-ttu-id="41ede-155">Grupo de recursos de Olá localizar que implementou Olá serviço de contentor do Azure para.</span><span class="sxs-lookup"><span data-stu-id="41ede-155">Find hello resource group that you deployed hello Azure Container Service to.</span></span>
3. <span data-ttu-id="41ede-156">Selecione Olá **pública** grupo de segurança de rede do agente (que é denominado semelhante demasiado**XXXX-agente-público-nsg-XXXX**).</span><span class="sxs-lookup"><span data-stu-id="41ede-156">Select hello **public** agent network security group (which is named similar too**XXXX-agent-public-nsg-XXXX**).</span></span>
   
    ![Grupo de segurança de rede de serviço de contentor do Azure](./media/container-service-enable-public-access/agent-nsg.png)
4. <span data-ttu-id="41ede-158">Selecione **regras de segurança de entrada** e, em seguida, **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="41ede-158">Select **Inbound security rules** and then **Add**.</span></span>
   
    ![Regras de grupo de segurança de rede de serviço de contentor do Azure](./media/container-service-enable-public-access/add-firewall-rule.png)
5. <span data-ttu-id="41ede-160">Preencha tooallow de regra de firewall de Olá a porta pública e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="41ede-160">Fill out hello firewall rule tooallow your public port and click **OK**.</span></span>
   
   | <span data-ttu-id="41ede-161">Campo</span><span class="sxs-lookup"><span data-stu-id="41ede-161">Field</span></span> | <span data-ttu-id="41ede-162">Descrição</span><span class="sxs-lookup"><span data-stu-id="41ede-162">Description</span></span> |
   | --- | --- |
   | <span data-ttu-id="41ede-163">Nome</span><span class="sxs-lookup"><span data-stu-id="41ede-163">Name</span></span> |<span data-ttu-id="41ede-164">Um nome descritivo Olá da regra da firewall.</span><span class="sxs-lookup"><span data-stu-id="41ede-164">A descriptive name of hello firewall rule.</span></span> |
   | <span data-ttu-id="41ede-165">Prioridade</span><span class="sxs-lookup"><span data-stu-id="41ede-165">Priority</span></span> |<span data-ttu-id="41ede-166">Classificação de prioridade da regra de Olá.</span><span class="sxs-lookup"><span data-stu-id="41ede-166">Priority rank for hello rule.</span></span> <span data-ttu-id="41ede-167">Olá Olá número Olá superior Olá prioridade inferior.</span><span class="sxs-lookup"><span data-stu-id="41ede-167">hello lower hello number hello higher hello priority.</span></span> |
   | <span data-ttu-id="41ede-168">Origem</span><span class="sxs-lookup"><span data-stu-id="41ede-168">Source</span></span> |<span data-ttu-id="41ede-169">Restringir Olá entrada IP endereço intervalo toobe permitido ou negado por esta regra.</span><span class="sxs-lookup"><span data-stu-id="41ede-169">Restrict hello incoming IP address range toobe allowed or denied by this rule.</span></span> <span data-ttu-id="41ede-170">Utilize **qualquer** toonot especificar uma restrição.</span><span class="sxs-lookup"><span data-stu-id="41ede-170">Use **Any** toonot specify a restriction.</span></span> |
   | <span data-ttu-id="41ede-171">Serviço</span><span class="sxs-lookup"><span data-stu-id="41ede-171">Service</span></span> |<span data-ttu-id="41ede-172">Selecione um conjunto de serviços predefinidos que destina-se a esta regra de segurança.</span><span class="sxs-lookup"><span data-stu-id="41ede-172">Select a set of predefined services this security rule is for.</span></span> <span data-ttu-id="41ede-173">Caso contrário, utilize **personalizada** toocreate os seus próprios.</span><span class="sxs-lookup"><span data-stu-id="41ede-173">Otherwise use **Custom** toocreate your own.</span></span> |
   | <span data-ttu-id="41ede-174">Protocolo</span><span class="sxs-lookup"><span data-stu-id="41ede-174">Protocol</span></span> |<span data-ttu-id="41ede-175">Restringir o tráfego com base no **TCP** ou **UDP**.</span><span class="sxs-lookup"><span data-stu-id="41ede-175">Restrict traffic based on **TCP** or **UDP**.</span></span> <span data-ttu-id="41ede-176">Utilize **qualquer** toonot especificar uma restrição.</span><span class="sxs-lookup"><span data-stu-id="41ede-176">Use **Any** toonot specify a restriction.</span></span> |
   | <span data-ttu-id="41ede-177">Intervalo de portas</span><span class="sxs-lookup"><span data-stu-id="41ede-177">Port range</span></span> |<span data-ttu-id="41ede-178">Quando **serviço** é **personalizada**, especifica Olá intervalo de portas que esta regra afeta.</span><span class="sxs-lookup"><span data-stu-id="41ede-178">When **Service** is **Custom**, specifies hello range of ports that this rule affects.</span></span> <span data-ttu-id="41ede-179">Pode utilizar uma porta única, tal como **80**, ou como um intervalo **1024-1500**.</span><span class="sxs-lookup"><span data-stu-id="41ede-179">You can use a single port, such as **80**, or a range like **1024-1500**.</span></span> |
   | <span data-ttu-id="41ede-180">Ação</span><span class="sxs-lookup"><span data-stu-id="41ede-180">Action</span></span> |<span data-ttu-id="41ede-181">Permitir ou negar o tráfego que cumpra os critérios de Olá.</span><span class="sxs-lookup"><span data-stu-id="41ede-181">Allow or deny traffic that meets hello criteria.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="41ede-182">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="41ede-182">Next steps</span></span>
<span data-ttu-id="41ede-183">Saiba mais sobre a diferença de Olá entre [públicos e privados agentes DC/OS](container-service-dcos-agents.md).</span><span class="sxs-lookup"><span data-stu-id="41ede-183">Learn about hello difference between [public and private DC/OS agents](container-service-dcos-agents.md).</span></span>

<span data-ttu-id="41ede-184">Leia mais informações sobre [gerir os contentores de DC/SO](container-service-mesos-marathon-ui.md).</span><span class="sxs-lookup"><span data-stu-id="41ede-184">Read more information about [managing your DC/OS containers](container-service-mesos-marathon-ui.md).</span></span>

