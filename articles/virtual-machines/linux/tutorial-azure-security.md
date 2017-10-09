---
title: "aaaAzure Centro de segurança e Linux as máquinas virtuais no Azure | Microsoft Docs"
description: "Saiba mais sobre a segurança para a máquina virtual do Linux do Azure com o Centro de segurança do Azure."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/07/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 7aa0de35fb311457e769f152c8575ec43e41c39c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-virtual-machine-security-by-using-azure-security-center"></a><span data-ttu-id="db077-103">Monitorizar a segurança da máquina virtual utilizando o Centro de segurança do Azure</span><span class="sxs-lookup"><span data-stu-id="db077-103">Monitor virtual machine security by using Azure Security Center</span></span>

<span data-ttu-id="db077-104">Centro de segurança do Azure pode ajudar a obter visibilidade para o recurso do Azure práticas de segurança.</span><span class="sxs-lookup"><span data-stu-id="db077-104">Azure Security Center can help you gain visibility into your Azure resource security practices.</span></span> <span data-ttu-id="db077-105">Centro de segurança oferece monitorização de segurança integrada.</span><span class="sxs-lookup"><span data-stu-id="db077-105">Security Center offers integrated security monitoring.</span></span> <span data-ttu-id="db077-106">-Pode detetar ameaças que caso contrário podem passar despercebidas.</span><span class="sxs-lookup"><span data-stu-id="db077-106">It can detect threats that otherwise might go unnoticed.</span></span> <span data-ttu-id="db077-107">Neste tutorial, pode obter informações sobre o Centro de segurança do Azure e como:</span><span class="sxs-lookup"><span data-stu-id="db077-107">In this tutorial, you learn about Azure Security Center, and how to:</span></span>
 
> [!div class="checklist"]
> * <span data-ttu-id="db077-108">Configurar a recolha de dados</span><span class="sxs-lookup"><span data-stu-id="db077-108">Set up data collection</span></span>
> * <span data-ttu-id="db077-109">Configurar políticas de segurança</span><span class="sxs-lookup"><span data-stu-id="db077-109">Set up security policies</span></span>
> * <span data-ttu-id="db077-110">Ver e corrigir problemas de estado de funcionamento de configuração</span><span class="sxs-lookup"><span data-stu-id="db077-110">View and fix configuration health issues</span></span>
> * <span data-ttu-id="db077-111">Reveja as ameaças detetadas</span><span class="sxs-lookup"><span data-stu-id="db077-111">Review detected threats</span></span>  

## <a name="security-center-overview"></a><span data-ttu-id="db077-112">Descrição geral do Centro de segurança</span><span class="sxs-lookup"><span data-stu-id="db077-112">Security Center overview</span></span>

<span data-ttu-id="db077-113">Centro de segurança identifica potenciais problemas de configuração de máquina virtual (VM) e direcionados ameaças de segurança.</span><span class="sxs-lookup"><span data-stu-id="db077-113">Security Center identifies potential virtual machine (VM) configuration issues and targeted security threats.</span></span> <span data-ttu-id="db077-114">Estes podem incluir as VMs que estão em falta grupos de segurança de rede, os discos não encriptados e ataques de protocolo RDP (Remote Desktop Protocol) de força bruta.</span><span class="sxs-lookup"><span data-stu-id="db077-114">These might include VMs that are missing network security groups, unencrypted disks, and brute-force Remote Desktop Protocol (RDP) attacks.</span></span> <span data-ttu-id="db077-115">informações de Olá são mostradas no dashboard do Centro de segurança de Olá em gráficos de fácil leitura.</span><span class="sxs-lookup"><span data-stu-id="db077-115">hello information is shown on hello Security Center dashboard in easy-to-read graphs.</span></span>

<span data-ttu-id="db077-116">tooaccess Olá dashboard do Centro de segurança, no portal do Azure, no menu de Olá, selecione de Olá **Centro de segurança**.</span><span class="sxs-lookup"><span data-stu-id="db077-116">tooaccess hello Security Center dashboard, in hello Azure portal, on hello menu, select  **Security Center**.</span></span> <span data-ttu-id="db077-117">No dashboard de Olá, pode ver o estado de funcionamento de segurança de Olá do seu ambiente do Azure, encontrar uma contagem de recomendações atuais e ver Olá estado atual de alertas de ameaça.</span><span class="sxs-lookup"><span data-stu-id="db077-117">On hello dashboard, you can see hello security health of your Azure environment, find a count of current recommendations, and view hello current state of threat alerts.</span></span> <span data-ttu-id="db077-118">Pode expandir cada toosee de alto nível gráfico mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="db077-118">You can expand each high-level chart toosee more detail.</span></span>

![Dashboard do Centro de segurança](./media/tutorial-azure-security/asc-dash.png)

<span data-ttu-id="db077-120">Centro de segurança vai mais além recomendações tooprovide de deteção de dados para problemas que Deteta.</span><span class="sxs-lookup"><span data-stu-id="db077-120">Security Center goes beyond data discovery tooprovide recommendations for issues that it detects.</span></span> <span data-ttu-id="db077-121">Por exemplo, se uma VM foi implementada sem um grupo de segurança de rede ligado, o Centro de segurança apresenta uma recomendação, com passos de remediação que pode efetuar.</span><span class="sxs-lookup"><span data-stu-id="db077-121">For example, if a VM was deployed without an attached network security group, Security Center displays a recommendation, with remediation steps you can take.</span></span> <span data-ttu-id="db077-122">Obter a remediação automática sem sair contexto Olá do Centro de segurança.</span><span class="sxs-lookup"><span data-stu-id="db077-122">You get automated remediation without leaving hello context of Security Center.</span></span>  

![Recomendações](./media/tutorial-azure-security/recommendations.png)

## <a name="set-up-data-collection"></a><span data-ttu-id="db077-124">Configurar a recolha de dados</span><span class="sxs-lookup"><span data-stu-id="db077-124">Set up data collection</span></span>

<span data-ttu-id="db077-125">Antes de poder obter visibilidade para configurações de segurança VM, terá de tooset configurar recolha de dados do Centro de segurança.</span><span class="sxs-lookup"><span data-stu-id="db077-125">Before you can get visibility into VM security configurations, you need tooset up Security Center data collection.</span></span> <span data-ttu-id="db077-126">Isto envolve a ativação da recolha de dados e criar toohold recolhido dados de conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="db077-126">This involves turning on data collection and creating an Azure storage account toohold collected data.</span></span> 

1. <span data-ttu-id="db077-127">No dashboard do Centro de segurança de Olá, clique em **política de segurança**e, em seguida, selecione a sua subscrição.</span><span class="sxs-lookup"><span data-stu-id="db077-127">On hello Security Center dashboard, click **Security policy**, and then select your subscription.</span></span> 
2. <span data-ttu-id="db077-128">Para **recolha de dados**, selecione **no**.</span><span class="sxs-lookup"><span data-stu-id="db077-128">For **Data collection**, select **On**.</span></span>
3. <span data-ttu-id="db077-129">Selecione uma conta de armazenamento, de toocreate **escolher uma conta de armazenamento**.</span><span class="sxs-lookup"><span data-stu-id="db077-129">toocreate a storage account, select **Choose a storage account**.</span></span> <span data-ttu-id="db077-130">Em seguida, selecione **OK**.</span><span class="sxs-lookup"><span data-stu-id="db077-130">Then, select **OK**.</span></span>
4. <span data-ttu-id="db077-131">No Olá **política de segurança** painel, selecione **guardar**.</span><span class="sxs-lookup"><span data-stu-id="db077-131">On hello **Security Policy** blade, select **Save**.</span></span> 

<span data-ttu-id="db077-132">agente de recolha de dados de centro de segurança de Olá é instalado em todas as VMs e começa a recolha de dados.</span><span class="sxs-lookup"><span data-stu-id="db077-132">hello Security Center data collection agent is then installed on all VMs, and data collection begins.</span></span> 

## <a name="set-up-a-security-policy"></a><span data-ttu-id="db077-133">Configurar uma política de segurança</span><span class="sxs-lookup"><span data-stu-id="db077-133">Set up a security policy</span></span>

<span data-ttu-id="db077-134">As políticas de segurança são itens de Olá toodefine utilizado para o qual o Centro de segurança recolhe dados e faz recomendações.</span><span class="sxs-lookup"><span data-stu-id="db077-134">Security policies are used toodefine hello items for which Security Center collects data and makes recommendations.</span></span> <span data-ttu-id="db077-135">Pode aplicar conjuntos toodifferent de políticas de segurança diferentes dos recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="db077-135">You can apply different security policies toodifferent sets of Azure resources.</span></span> <span data-ttu-id="db077-136">Embora por predefinição os recursos do Azure são avaliados em relação a todos os itens de política, pode desativar os itens de política individuais para todos os recursos do Azure ou para um grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="db077-136">Although by default Azure resources are evaluated against all policy items, you can turn off individual policy items for all Azure resources or for a resource group.</span></span> <span data-ttu-id="db077-137">Para obter informações aprofundadas sobre as políticas de segurança do Centro de segurança, consulte [definir políticas de segurança no Centro de segurança do Azure](../../security-center/security-center-policies.md).</span><span class="sxs-lookup"><span data-stu-id="db077-137">For in-depth information about Security Center security policies, see [Set security policies in Azure Security Center](../../security-center/security-center-policies.md).</span></span> 

<span data-ttu-id="db077-138">tooset configurar uma política de segurança para todos os recursos do Azure:</span><span class="sxs-lookup"><span data-stu-id="db077-138">tooset up a security policy for all Azure resources:</span></span>

1. <span data-ttu-id="db077-139">No dashboard do Centro de segurança de Olá, selecione **política de segurança**e, em seguida, selecione a sua subscrição.</span><span class="sxs-lookup"><span data-stu-id="db077-139">On hello Security Center dashboard, select **Security policy**, and then select your subscription.</span></span>
2. <span data-ttu-id="db077-140">Selecione **política de prevenção**.</span><span class="sxs-lookup"><span data-stu-id="db077-140">Select **Prevention policy**.</span></span>
3. <span data-ttu-id="db077-141">Ativar ou desativar os itens de política que pretende que o tooapply tooall recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="db077-141">Turn on or turn off policy items that you want tooapply tooall Azure resources.</span></span>
4. <span data-ttu-id="db077-142">Quando tiver terminado de selecionar as definições, selecione **OK**.</span><span class="sxs-lookup"><span data-stu-id="db077-142">When you're finished selecting your settings, select **OK**.</span></span>
5. <span data-ttu-id="db077-143">No Olá **política de segurança** painel, selecione **guardar**.</span><span class="sxs-lookup"><span data-stu-id="db077-143">On hello **Security policy** blade, select **Save**.</span></span> 

<span data-ttu-id="db077-144">tooset configurar uma política para um grupo de recursos específico:</span><span class="sxs-lookup"><span data-stu-id="db077-144">tooset up a policy for a specific resource group:</span></span>

1. <span data-ttu-id="db077-145">No dashboard do Centro de segurança de Olá, selecione **política de segurança**e, em seguida, selecione um grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="db077-145">On hello Security Center dashboard, select **Security policy**, and then select a resource group.</span></span>
2. <span data-ttu-id="db077-146">Selecione **política de prevenção**.</span><span class="sxs-lookup"><span data-stu-id="db077-146">Select **Prevention policy**.</span></span>
3. <span data-ttu-id="db077-147">Ativar ou desativar os itens de política que pretende que o grupo de recursos de toohello tooapply.</span><span class="sxs-lookup"><span data-stu-id="db077-147">Turn on or turn off policy items that you want tooapply toohello resource group.</span></span>
4. <span data-ttu-id="db077-148">Em **HERANÇA**, selecione **Unique**.</span><span class="sxs-lookup"><span data-stu-id="db077-148">Under **INHERITANCE**, select **Unique**.</span></span>
5. <span data-ttu-id="db077-149">Quando tiver terminado de selecionar as definições, selecione **OK**.</span><span class="sxs-lookup"><span data-stu-id="db077-149">When you're finished selecting your settings, select **OK**.</span></span>
6. <span data-ttu-id="db077-150">No Olá **política de segurança** painel, selecione **guardar**.</span><span class="sxs-lookup"><span data-stu-id="db077-150">On hello **Security policy** blade, select **Save**.</span></span>  

<span data-ttu-id="db077-151">Também pode desativar a recolha de dados para um grupo de recursos específico nesta página.</span><span class="sxs-lookup"><span data-stu-id="db077-151">You also can turn off data collection for a specific resource group on this page.</span></span>

<span data-ttu-id="db077-152">No seguinte exemplo de Olá, foi criada uma política exclusiva para um grupo de recursos denominado *myResoureGroup*.</span><span class="sxs-lookup"><span data-stu-id="db077-152">In hello following example, a unique policy has been created for a resource group named *myResoureGroup*.</span></span> <span data-ttu-id="db077-153">Nesta política, o disco de encriptação e web aplicação firewall recomendações estão desativadas.</span><span class="sxs-lookup"><span data-stu-id="db077-153">In this policy, disk encryption and web application firewall recommendations are turned off.</span></span>

![Exclusivo da política](./media/tutorial-azure-security/unique-policy.png)

## <a name="view-vm-configuration-health"></a><span data-ttu-id="db077-155">Ver estado de funcionamento de configuração de VM</span><span class="sxs-lookup"><span data-stu-id="db077-155">View VM configuration health</span></span>

<span data-ttu-id="db077-156">Depois de ter ativada a recolha de dados e definir uma política de segurança, o Centro de segurança começa tooprovide alertas e as recomendações.</span><span class="sxs-lookup"><span data-stu-id="db077-156">After you've turned on data collection and set a security policy, Security Center begins tooprovide alerts and recommendations.</span></span> <span data-ttu-id="db077-157">Como VMs implementadas, o agente de recolha de dados de Olá está instalado.</span><span class="sxs-lookup"><span data-stu-id="db077-157">As VMs are deployed, hello data collection agent is installed.</span></span> <span data-ttu-id="db077-158">Centro de segurança, em seguida, é preenchido com dados de Olá novas VMs.</span><span class="sxs-lookup"><span data-stu-id="db077-158">Security Center is then populated with data for hello new VMs.</span></span> <span data-ttu-id="db077-159">Para obter informações aprofundadas sobre o estado de funcionamento de configuração de VM, consulte [proteger as suas VMs no Centro de segurança](../../security-center/security-center-virtual-machine-recommendations.md).</span><span class="sxs-lookup"><span data-stu-id="db077-159">For in-depth information about VM configuration health, see [Protect your VMs in Security Center](../../security-center/security-center-virtual-machine-recommendations.md).</span></span> 

<span data-ttu-id="db077-160">Como os dados são recolhidos, estado de funcionamento de recursos de Olá para cada VM e os recursos do Azure relacionados é agregado.</span><span class="sxs-lookup"><span data-stu-id="db077-160">As data is collected, hello resource health for each VM and related Azure resource is aggregated.</span></span> <span data-ttu-id="db077-161">informações de Olá são apresentadas um gráfico de fácil leitura.</span><span class="sxs-lookup"><span data-stu-id="db077-161">hello information is shown in an easy-to-read chart.</span></span> 

<span data-ttu-id="db077-162">Estado de funcionamento de recursos tooview:</span><span class="sxs-lookup"><span data-stu-id="db077-162">tooview resource health:</span></span>

1.  <span data-ttu-id="db077-163">No dashboard do Centro de segurança de Olá, sob **estado de funcionamento de segurança de recursos**, selecione **computação**.</span><span class="sxs-lookup"><span data-stu-id="db077-163">On hello Security Center dashboard, under **Resource security health**, select **Compute**.</span></span> 
2.  <span data-ttu-id="db077-164">No Olá **computação** painel, selecione **máquinas virtuais**.</span><span class="sxs-lookup"><span data-stu-id="db077-164">On hello **Compute** blade, select **Virtual machines**.</span></span> <span data-ttu-id="db077-165">Esta vista fornece um resumo do Estado de configuração de Olá para todas as suas VMs.</span><span class="sxs-lookup"><span data-stu-id="db077-165">This view provides a summary of hello configuration status for all your VMs.</span></span>

![Estado de funcionamento de computação](./media/tutorial-azure-security/compute-health.png)

<span data-ttu-id="db077-167">toosee todas as recomendações para uma VM, selecione Olá VM.</span><span class="sxs-lookup"><span data-stu-id="db077-167">toosee all recommendations for a VM, select hello VM.</span></span> <span data-ttu-id="db077-168">Recomendações e remediação são abordadas mais detalhadamente na secção seguinte, Olá deste tutorial.</span><span class="sxs-lookup"><span data-stu-id="db077-168">Recommendations and remediation are covered in more detail in hello next section of this tutorial.</span></span>

## <a name="remediate-configuration-issues"></a><span data-ttu-id="db077-169">Resolver problemas de configuração</span><span class="sxs-lookup"><span data-stu-id="db077-169">Remediate configuration issues</span></span>

<span data-ttu-id="db077-170">Depois de centro de segurança começa toopopulate com dados de configuração, as recomendações são efetuadas com base na política de segurança de Olá que configurou.</span><span class="sxs-lookup"><span data-stu-id="db077-170">After Security Center begins toopopulate with configuration data, recommendations are made based on hello security policy you set up.</span></span> <span data-ttu-id="db077-171">Por exemplo, se uma VM foi configurado sem um grupo de segurança de rede associados, uma recomendação é feita toocreate um.</span><span class="sxs-lookup"><span data-stu-id="db077-171">For instance, if a VM was set up without an associated network security group, a recommendation is made toocreate one.</span></span> 

<span data-ttu-id="db077-172">toosee uma lista de todas as recomendações:</span><span class="sxs-lookup"><span data-stu-id="db077-172">toosee a list of all recommendations:</span></span> 

1. <span data-ttu-id="db077-173">No dashboard do Centro de segurança de Olá, selecione **recomendações**.</span><span class="sxs-lookup"><span data-stu-id="db077-173">On hello Security Center dashboard, select **Recommendations**.</span></span>
2. <span data-ttu-id="db077-174">Selecione uma recomendação específica.</span><span class="sxs-lookup"><span data-stu-id="db077-174">Select a specific recommendation.</span></span> <span data-ttu-id="db077-175">É apresentada uma lista de todos os recursos para o qual se aplica a recomendação de Olá.</span><span class="sxs-lookup"><span data-stu-id="db077-175">A list of all resources for which hello recommendation applies appears.</span></span>
3. <span data-ttu-id="db077-176">tooapply uma recomendação, selecione um recurso específico.</span><span class="sxs-lookup"><span data-stu-id="db077-176">tooapply a recommendation, select a specific resource.</span></span> 
4. <span data-ttu-id="db077-177">Siga as instruções de Olá para passos de remediação.</span><span class="sxs-lookup"><span data-stu-id="db077-177">Follow hello instructions for remediation steps.</span></span> 

<span data-ttu-id="db077-178">Em muitos casos, o Centro de segurança fornece passos passíveis de ação pode demorar tooaddress uma recomendação sem sair do Centro de segurança.</span><span class="sxs-lookup"><span data-stu-id="db077-178">In many cases, Security Center provides actionable steps you can take tooaddress a recommendation without leaving Security Center.</span></span> <span data-ttu-id="db077-179">No seguinte exemplo de Olá, o Centro de segurança Deteta um grupo de segurança de rede que tenha uma regra de entrada sem restrições.</span><span class="sxs-lookup"><span data-stu-id="db077-179">In hello following example, Security Center detects a network security group that has an unrestricted inbound rule.</span></span> <span data-ttu-id="db077-180">Na página de recomendação Olá, pode selecionar Olá **editar regras de entrada** botão.</span><span class="sxs-lookup"><span data-stu-id="db077-180">On hello recommendation page, you can select hello **Edit inbound rules** button.</span></span> <span data-ttu-id="db077-181">Olá IU que é necessário toomodify Olá regra é apresentada.</span><span class="sxs-lookup"><span data-stu-id="db077-181">hello UI that is needed toomodify hello rule appears.</span></span> 

![Recomendações](./media/tutorial-azure-security/remediation.png)

<span data-ttu-id="db077-183">Como são resolvidas as recomendações, são marcados como resolvido.</span><span class="sxs-lookup"><span data-stu-id="db077-183">As recommendations are remediated, they are marked as resolved.</span></span> 

## <a name="view-detected-threats"></a><span data-ttu-id="db077-184">Ver ameaças detetadas</span><span class="sxs-lookup"><span data-stu-id="db077-184">View detected threats</span></span>

<span data-ttu-id="db077-185">Além disso tooresource recomendações de configuração, o Centro de segurança apresenta os alertas de deteção de ameaças.</span><span class="sxs-lookup"><span data-stu-id="db077-185">In addition tooresource configuration recommendations, Security Center displays threat detection alerts.</span></span> <span data-ttu-id="db077-186">funcionalidade de alertas de segurança de Olá agrega os dados recolhidos a partir de cada VM, registos de rede do Azure e soluções de parceiros ligadas toodetect ameaças de segurança relativamente aos recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="db077-186">hello security alerts feature aggregates data collected from each VM, Azure networking logs, and connected partner solutions toodetect security threats against Azure resources.</span></span> <span data-ttu-id="db077-187">Para obter informações aprofundadas sobre as capacidades de deteção de ameaças do Centro de segurança, consulte [as capacidades de deteção do Centro de segurança do Azure](../../security-center/security-center-detection-capabilities.md).</span><span class="sxs-lookup"><span data-stu-id="db077-187">For in-depth information about Security Center threat detection capabilities, see [Azure Security Center detection capabilities](../../security-center/security-center-detection-capabilities.md).</span></span>

<span data-ttu-id="db077-188">funcionalidade de alertas de segurança de Olá requer o Centro de segurança de Olá preços toobe camada aumentada de *livres* demasiado*padrão*.</span><span class="sxs-lookup"><span data-stu-id="db077-188">hello security alerts feature requires hello Security Center pricing tier toobe increased from *Free* too*Standard*.</span></span> <span data-ttu-id="db077-189">30 dias **avaliação gratuita** está disponível quando mover toothis escalão de preço superior.</span><span class="sxs-lookup"><span data-stu-id="db077-189">A 30-day **free trial** is available when you move toothis higher pricing tier.</span></span> 

<span data-ttu-id="db077-190">escalão de preço Olá toochange:</span><span class="sxs-lookup"><span data-stu-id="db077-190">toochange hello pricing tier:</span></span>  

1. <span data-ttu-id="db077-191">No dashboard do Centro de segurança de Olá, clique em **política de segurança**e, em seguida, selecione a sua subscrição.</span><span class="sxs-lookup"><span data-stu-id="db077-191">On hello Security Center dashboard, click **Security policy**, and then select your subscription.</span></span>
2. <span data-ttu-id="db077-192">Selecione **escalão de preço**.</span><span class="sxs-lookup"><span data-stu-id="db077-192">Select **Pricing tier**.</span></span>
3. <span data-ttu-id="db077-193">Selecione a camada novo Olá e, em seguida, selecione **selecione**.</span><span class="sxs-lookup"><span data-stu-id="db077-193">Select hello new tier, and then select **Select**.</span></span>
4. <span data-ttu-id="db077-194">No Olá **política de segurança** painel, selecione **guardar**.</span><span class="sxs-lookup"><span data-stu-id="db077-194">On hello **Security policy** blade, select **Save**.</span></span> 

<span data-ttu-id="db077-195">Depois de alterar o escalão de preço de Olá, o gráfico de alertas de segurança de Olá começa toopopulate como são detetadas ameaças de segurança.</span><span class="sxs-lookup"><span data-stu-id="db077-195">After you've changed hello pricing tier, hello security alerts graph begins toopopulate as security threats are detected.</span></span>

![Alertas de segurança](./media/tutorial-azure-security/security-alerts.png)

<span data-ttu-id="db077-197">Selecione uma alerta tooview informações.</span><span class="sxs-lookup"><span data-stu-id="db077-197">Select an alert tooview information.</span></span> <span data-ttu-id="db077-198">Por exemplo, pode ver uma descrição de ameaça Olá, hora da deteção Olá, todas as tentativas de ameaças e Olá remediação recomendada.</span><span class="sxs-lookup"><span data-stu-id="db077-198">For example, you can see a description of hello threat, hello detection time, all threat attempts, and hello recommended remediation.</span></span> <span data-ttu-id="db077-199">No seguinte exemplo de Olá, foi detetado um ataque de força bruta RDP, com 294 tentativas falhadas de RDP.</span><span class="sxs-lookup"><span data-stu-id="db077-199">In hello following example, an RDP brute-force attack was detected, with 294 failed RDP attempts.</span></span> <span data-ttu-id="db077-200">É fornecida uma resolução recomendada.</span><span class="sxs-lookup"><span data-stu-id="db077-200">A recommended resolution is provided.</span></span>

![Ataque RDP](./media/tutorial-azure-security/rdp-attack.png)

## <a name="next-steps"></a><span data-ttu-id="db077-202">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="db077-202">Next steps</span></span>
<span data-ttu-id="db077-203">Neste tutorial, pode configurar o Centro de segurança do Azure e, em seguida, revisto VMs no Centro de segurança.</span><span class="sxs-lookup"><span data-stu-id="db077-203">In this tutorial, you set up Azure Security Center, and then reviewed VMs in Security Center.</span></span> <span data-ttu-id="db077-204">Aprendeu a:</span><span class="sxs-lookup"><span data-stu-id="db077-204">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="db077-205">Configurar a recolha de dados</span><span class="sxs-lookup"><span data-stu-id="db077-205">Set up data collection</span></span>
> * <span data-ttu-id="db077-206">Configurar políticas de segurança</span><span class="sxs-lookup"><span data-stu-id="db077-206">Set up security policies</span></span>
> * <span data-ttu-id="db077-207">Ver e corrigir problemas de estado de funcionamento de configuração</span><span class="sxs-lookup"><span data-stu-id="db077-207">View and fix configuration health issues</span></span>
> * <span data-ttu-id="db077-208">Reveja as ameaças detetadas</span><span class="sxs-lookup"><span data-stu-id="db077-208">Review detected threats</span></span>

<span data-ttu-id="db077-209">Produzir toolearn tutorial seguinte de toohello mais informações sobre como criar um pipeline de CI/CD com Jenkins, GitHub e Docker.</span><span class="sxs-lookup"><span data-stu-id="db077-209">Advance toohello next tutorial toolearn more about creating a CI/CD pipeline with Jenkins, GitHub, and Docker.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="db077-210">Criar a infraestrutura de CI/CD com Jenkins, GitHub e Docker</span><span class="sxs-lookup"><span data-stu-id="db077-210">Create CI/CD infrastructure with Jenkins, GitHub, and Docker</span></span>](tutorial-jenkins-github-docker-cicd.md)

