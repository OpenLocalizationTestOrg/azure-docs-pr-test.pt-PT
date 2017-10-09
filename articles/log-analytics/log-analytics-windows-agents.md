---
title: aaaConnect Windows computadores tooAzure Log Analytics | Microsoft Docs
description: "Este artigo mostra computadores com Windows hello passos tooconnect Olá no seu toohello de infraestrutura no local serviço análise de registos ao utilizar uma versão personalizada da Olá Microsoft Monitoring Agent (MMA)."
services: log-analytics
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: 
ms.assetid: 932f7b8c-485c-40c1-98e3-7d4c560876d2
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/03/2017
ms.author: magoedte
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 7e15f9eeb0440bd2f6557d7215df701526e4f9aa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="connect-windows-computers-toohello-log-analytics-service-in-azure"></a><span data-ttu-id="8f92c-103">Ligar o serviço de análise de registos do Windows computadores toohello no Azure</span><span class="sxs-lookup"><span data-stu-id="8f92c-103">Connect Windows computers toohello Log Analytics service in Azure</span></span>

<span data-ttu-id="8f92c-104">Este artigo mostra Olá passos tooconnect computadores com Windows no seu áreas de trabalho de tooOMS de infraestrutura no local utilizando uma versão personalizada da Olá Microsoft Monitoring Agent (MMA).</span><span class="sxs-lookup"><span data-stu-id="8f92c-104">This article shows hello steps tooconnect Windows computers in your on-premises infrastructure tooOMS workspaces by using a customized version of hello Microsoft Monitoring Agent (MMA).</span></span> <span data-ttu-id="8f92c-105">Tem de tooinstall e ligar agentes para todos os computadores de Olá que pretende que tooonboard serem no serviço de análise de registos do toosend dados toohello e tooview e act nesses dados.</span><span class="sxs-lookup"><span data-stu-id="8f92c-105">You need tooinstall and connect agents for all of hello computers that you want tooonboard in order for them toosend data toohello Log Analytics service and tooview and act on that data.</span></span> <span data-ttu-id="8f92c-106">Cada agente pode reportar toomultiple áreas de trabalho.</span><span class="sxs-lookup"><span data-stu-id="8f92c-106">Each agent can report toomultiple workspaces.</span></span>

<span data-ttu-id="8f92c-107">Pode instalar agentes utilizando a configuração, a linha de comandos, ou com pretendido Estado Configuration (DSC) na automatização do Azure.</span><span class="sxs-lookup"><span data-stu-id="8f92c-107">You can install agents using Setup, command line, or with Desired State Configuration (DSC) in Azure Automation.</span></span>  

>[!NOTE]
<span data-ttu-id="8f92c-108">Para máquinas virtuais em execução no Azure, pode simplificar a instalação utilizando Olá [extensão da máquina virtual](log-analytics-azure-vm-extension.md).</span><span class="sxs-lookup"><span data-stu-id="8f92c-108">For virtual machines running in Azure, you can simplify installation by using hello [virtual machine extension](log-analytics-azure-vm-extension.md).</span></span>

<span data-ttu-id="8f92c-109">Em computadores com a conectividade à Internet, o agente de Olá utiliza Olá ligação toohello Internet toosend dados tooOMS.</span><span class="sxs-lookup"><span data-stu-id="8f92c-109">On computers with Internet connectivity, hello agent uses hello connection toohello Internet toosend data tooOMS.</span></span> <span data-ttu-id="8f92c-110">Para computadores que não têm acesso à Internet, pode utilizar um proxy ou Olá [OMS Gateway](log-analytics-oms-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="8f92c-110">For computers that do not have Internet connectivity, you can use a proxy or hello [OMS Gateway](log-analytics-oms-gateway.md).</span></span>

<span data-ttu-id="8f92c-111">Ligar o seu tooOMS de computadores do Windows é simples utilizar três passos simples:</span><span class="sxs-lookup"><span data-stu-id="8f92c-111">Connecting your Windows computers tooOMS is straightforward using three simple steps:</span></span>

1. <span data-ttu-id="8f92c-112">Transferir o ficheiro de configuração do agente de Olá a partir do portal do OMS Olá</span><span class="sxs-lookup"><span data-stu-id="8f92c-112">Download hello agent setup file from hello OMS portal</span></span>
2. <span data-ttu-id="8f92c-113">Instalar o agente de Olá utilizando o método de Olá que escolher</span><span class="sxs-lookup"><span data-stu-id="8f92c-113">Install hello agent using hello method you choose</span></span>
3. <span data-ttu-id="8f92c-114">Configure o agente de Olá ou adicione áreas de trabalho adicionais, se necessário</span><span class="sxs-lookup"><span data-stu-id="8f92c-114">Configure hello agent or add additional workspaces, if necessary</span></span>

<span data-ttu-id="8f92c-115">Olá seguinte diagrama mostra Olá relação entre os computadores com o Windows e o OMS depois de ter instalado e configurado os agentes.</span><span class="sxs-lookup"><span data-stu-id="8f92c-115">hello following diagram shows hello relationship between your Windows computers and OMS after you’ve installed and configured agents.</span></span>

![OMS-direta-agente-diagrama](./media/log-analytics-windows-agents/oms-direct-agent-diagram.png)

<span data-ttu-id="8f92c-117">Se as políticas de segurança de TI não permitir que os computadores no seu toohello tooconnect de rede à Internet, pode configurar o seu toohello de tooconnect computadores OMS Gateway.</span><span class="sxs-lookup"><span data-stu-id="8f92c-117">If your IT security policies do not allow computers on your network tooconnect toohello Internet, you can configure your computers tooconnect toohello OMS Gateway.</span></span> <span data-ttu-id="8f92c-118">Para obter mais informações e passos sobre como tooconfigure sua toocommunicate servidores através do serviço OMS toohello um Gateway do OMS, consulte o artigo [ligar tooOMS de computadores utilizando Olá OMS Gateway](log-analytics-oms-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="8f92c-118">For more information and steps on how tooconfigure your servers toocommunicate through an OMS Gateway toohello OMS service, see [Connect computers tooOMS using hello OMS Gateway](log-analytics-oms-gateway.md).</span></span>

## <a name="system-requirements-and-required-configuration"></a><span data-ttu-id="8f92c-119">Requisitos de sistema e a configuração necessária</span><span class="sxs-lookup"><span data-stu-id="8f92c-119">System requirements and required configuration</span></span>
<span data-ttu-id="8f92c-120">Antes de instalar ou implementar agentes, reveja Olá tooensure detalhes que cumpre os requisitos de Olá a seguir.</span><span class="sxs-lookup"><span data-stu-id="8f92c-120">Before you install or deploy agents, review hello following details tooensure you meet hello requirements.</span></span>

- <span data-ttu-id="8f92c-121">Só pode instalar Olá OMS MMA em computadores com o Windows Server 2008 SP 1 ou posterior ou Windows 7 SP1 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="8f92c-121">You can only install hello OMS MMA on computers running Windows Server 2008 SP 1 or later or Windows 7 SP1 or later.</span></span>
- <span data-ttu-id="8f92c-122">Necessita de uma subscrição do Azure.</span><span class="sxs-lookup"><span data-stu-id="8f92c-122">You need an Azure subscription.</span></span>  <span data-ttu-id="8f92c-123">Para obter mais informações, consulte [introdução à análise de registos](log-analytics-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="8f92c-123">For more information, see [Get started with Log Analytics](log-analytics-get-started.md).</span></span>
- <span data-ttu-id="8f92c-124">Cada computador com o Windows tem de ser capaz de tooconnect toohello Internet através de HTTPS ou toohello OMS Gateway.</span><span class="sxs-lookup"><span data-stu-id="8f92c-124">Each Windows computer must be able tooconnect toohello Internet using HTTPS or toohello OMS Gateway.</span></span> <span data-ttu-id="8f92c-125">Esta ligação pode ser direta, através de um proxy ou através de Olá OMS Gateway.</span><span class="sxs-lookup"><span data-stu-id="8f92c-125">This connection can be direct, via a proxy, or through hello OMS Gateway.</span></span>
- <span data-ttu-id="8f92c-126">Pode instalar Olá OMS MMA em computadores autónomos, servidores e máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="8f92c-126">You can install hello OMS MMA on stand-alone computers, servers, and virtual machines.</span></span> <span data-ttu-id="8f92c-127">Se pretender tooconnect tooOMS de máquinas de virtuais alojado no Azure, veja [tooLog de máquinas virtuais do Azure ligar análise](log-analytics-azure-vm-extension.md).</span><span class="sxs-lookup"><span data-stu-id="8f92c-127">If you want tooconnect Azure-hosted virtual machines tooOMS, see [Connect Azure virtual machines tooLog Analytics](log-analytics-azure-vm-extension.md).</span></span>
- <span data-ttu-id="8f92c-128">agente de Olá tem toouse a porta TCP 443 para vários recursos.</span><span class="sxs-lookup"><span data-stu-id="8f92c-128">hello agent needs toouse TCP port 443 for various resources.</span></span>

### <a name="network"></a><span data-ttu-id="8f92c-129">Rede</span><span class="sxs-lookup"><span data-stu-id="8f92c-129">Network</span></span>

<span data-ttu-id="8f92c-130">Para Windows agentes tooconnect tooand registar com o serviço OMS Olá, têm de ter acesso toonetwork recursos, incluindo URLs de domínio e de números de porta de Olá.</span><span class="sxs-lookup"><span data-stu-id="8f92c-130">For Windows agents tooconnect tooand register with hello OMS service, they must have access toonetwork resources, including hello port numbers and domain URLs.</span></span>

- <span data-ttu-id="8f92c-131">Para servidores proxy, tem de tooensure Olá recursos estão configurados nas definições do agente de servidor de proxy adequado.</span><span class="sxs-lookup"><span data-stu-id="8f92c-131">For proxy servers, you need tooensure that hello appropriate proxy server resources are configured in agent settings.</span></span>
- <span data-ttu-id="8f92c-132">Para firewalls que restringem o acesso toohello Internet, ou os engenheiros de rede necessário tooconfigure tooOMS de acesso de toopermit sua firewall.</span><span class="sxs-lookup"><span data-stu-id="8f92c-132">For firewalls that restrict access toohello Internet, you or your networking engineers need tooconfigure your firewall toopermit access tooOMS.</span></span> <span data-ttu-id="8f92c-133">Não é necessária nenhuma ação nas definições do agente.</span><span class="sxs-lookup"><span data-stu-id="8f92c-133">No action is needed in agent settings.</span></span>

<span data-ttu-id="8f92c-134">Olá, a tabela seguinte mostra os recursos necessários para a comunicação.</span><span class="sxs-lookup"><span data-stu-id="8f92c-134">hello following table shows resources needed for communication.</span></span>

>[!NOTE]
><span data-ttu-id="8f92c-135">Alguns dos Olá os seguintes recursos mencionar das informações operacionais, que era um nome anterior para análise de registos.</span><span class="sxs-lookup"><span data-stu-id="8f92c-135">Some of hello following resources mention Operational Insights, which was a previous name for Log Analytics.</span></span>

| <span data-ttu-id="8f92c-136">Recursos do Agente</span><span class="sxs-lookup"><span data-stu-id="8f92c-136">Agent Resource</span></span> | <span data-ttu-id="8f92c-137">Portas</span><span class="sxs-lookup"><span data-stu-id="8f92c-137">Ports</span></span> | <span data-ttu-id="8f92c-138">Inspeção de HTTPS direto</span><span class="sxs-lookup"><span data-stu-id="8f92c-138">Bypass HTTPS inspection</span></span> |
|---|---|---|
| <span data-ttu-id="8f92c-139">*.ods.opinsights.azure.com</span><span class="sxs-lookup"><span data-stu-id="8f92c-139">*.ods.opinsights.azure.com</span></span> | <span data-ttu-id="8f92c-140">443</span><span class="sxs-lookup"><span data-stu-id="8f92c-140">443</span></span> | <span data-ttu-id="8f92c-141">Sim</span><span class="sxs-lookup"><span data-stu-id="8f92c-141">Yes</span></span> |
| <span data-ttu-id="8f92c-142">*.oms.opinsights.azure.com</span><span class="sxs-lookup"><span data-stu-id="8f92c-142">*.oms.opinsights.azure.com</span></span> | <span data-ttu-id="8f92c-143">443</span><span class="sxs-lookup"><span data-stu-id="8f92c-143">443</span></span> | <span data-ttu-id="8f92c-144">Sim</span><span class="sxs-lookup"><span data-stu-id="8f92c-144">Yes</span></span> |
| <span data-ttu-id="8f92c-145">*.blob.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="8f92c-145">*.blob.core.windows.net</span></span> | <span data-ttu-id="8f92c-146">443</span><span class="sxs-lookup"><span data-stu-id="8f92c-146">443</span></span> | <span data-ttu-id="8f92c-147">Sim</span><span class="sxs-lookup"><span data-stu-id="8f92c-147">Yes</span></span> |
| <span data-ttu-id="8f92c-148">*.azure-automation.net</span><span class="sxs-lookup"><span data-stu-id="8f92c-148">*.azure-automation.net</span></span> | <span data-ttu-id="8f92c-149">443</span><span class="sxs-lookup"><span data-stu-id="8f92c-149">443</span></span> | <span data-ttu-id="8f92c-150">Sim</span><span class="sxs-lookup"><span data-stu-id="8f92c-150">Yes</span></span> |



## <a name="download-hello-agent-setup-file-from-oms"></a><span data-ttu-id="8f92c-151">Transferir o ficheiro de configuração do agente de Olá do OMS</span><span class="sxs-lookup"><span data-stu-id="8f92c-151">Download hello agent setup file from OMS</span></span>
1. <span data-ttu-id="8f92c-152">No portal do OMS Olá, no Olá **descrição geral** página, clique em Olá **definições** mosaico.</span><span class="sxs-lookup"><span data-stu-id="8f92c-152">In hello OMS portal, on hello **Overview** page, click hello **Settings** tile.</span></span>  <span data-ttu-id="8f92c-153">Clique em Olá **origens ligadas** separador na parte superior do Olá.</span><span class="sxs-lookup"><span data-stu-id="8f92c-153">Click hello **Connected Sources** tab at hello top.</span></span>  
    <span data-ttu-id="8f92c-154">![Separador de origens ligada](./media/log-analytics-windows-agents/oms-direct-agent-connected-sources.png)</span><span class="sxs-lookup"><span data-stu-id="8f92c-154">![Connected Sources tab](./media/log-analytics-windows-agents/oms-direct-agent-connected-sources.png)</span></span>
2. <span data-ttu-id="8f92c-155">Clique em **servidores Windows** e, em seguida, clique em **transferir o agente do Windows** tooyour aplicável computador processador tipo toodownload Olá ficheiro da configuração.</span><span class="sxs-lookup"><span data-stu-id="8f92c-155">Click **Windows Servers** and then click **Download Windows Agent** applicable tooyour computer processor type toodownload hello setup file.</span></span>
3. <span data-ttu-id="8f92c-156">No Olá à direita dos **ID da área de trabalho**, clique Olá ícone de cópia e colagem Olá ID no bloco de notas.</span><span class="sxs-lookup"><span data-stu-id="8f92c-156">On hello right of **Workspace ID**, click hello copy icon and paste hello ID into Notepad.</span></span>
4. <span data-ttu-id="8f92c-157">No Olá à direita dos **chave primária**, clique Olá ícone de cópia e colagem chave Olá no bloco de notas.</span><span class="sxs-lookup"><span data-stu-id="8f92c-157">On hello right of **Primary Key**, click hello copy icon and paste hello key into Notepad.</span></span>     

## <a name="install-hello-agent-using-setup"></a><span data-ttu-id="8f92c-158">Instalar o agente de Olá utilizando o programa de configuração</span><span class="sxs-lookup"><span data-stu-id="8f92c-158">Install hello agent using setup</span></span>
1. <span data-ttu-id="8f92c-159">Execute o agente de Olá de tooinstall de configuração num computador que pretende que o toomanage.</span><span class="sxs-lookup"><span data-stu-id="8f92c-159">Run Setup tooinstall hello agent on a computer that you want toomanage.</span></span>
2. <span data-ttu-id="8f92c-160">Na página de boas-vindas Olá, clique em **seguinte**.</span><span class="sxs-lookup"><span data-stu-id="8f92c-160">On hello Welcome page, click **Next**.</span></span>
3. <span data-ttu-id="8f92c-161">Na página de termos de licenciamento de Olá, leia Olá de licenciamento e, em seguida, clique em **concordo**.</span><span class="sxs-lookup"><span data-stu-id="8f92c-161">On hello License Terms page, read hello license and then click **I Agree**.</span></span>
4. <span data-ttu-id="8f92c-162">Na página de pasta de destino Olá, altere ou mantenha a pasta de instalação predefinida de Olá e, em seguida, clique em **seguinte**.</span><span class="sxs-lookup"><span data-stu-id="8f92c-162">On hello Destination Folder page, change or keep hello default installation folder and then click **Next**.</span></span>
5. <span data-ttu-id="8f92c-163">Na página de opções de configuração do agente de Olá, pode escolher tooconnect Olá agente tooAzure análise de registos (OMS), Operations Manager, ou pode deixar as escolhas de Olá em branco se pretende que o agente de Olá tooconfigure mais tarde.</span><span class="sxs-lookup"><span data-stu-id="8f92c-163">On hello Agent Setup Options page, you can choose tooconnect hello agent tooAzure Log Analytics (OMS), Operations Manager, or you can leave hello choices blank if you want tooconfigure hello agent later.</span></span> <span data-ttu-id="8f92c-164">Clique em **Seguinte**.</span><span class="sxs-lookup"><span data-stu-id="8f92c-164">Click **Next**.</span></span>   
    - <span data-ttu-id="8f92c-165">Se tiver escolhido tooconnect tooAzure análise de registos (OMS), cole Olá **ID da área de trabalho** e **chave da área de trabalho (chave primária)** copiado no bloco de notas no procedimento anterior Olá e, em seguida, clique em  **Seguinte**.</span><span class="sxs-lookup"><span data-stu-id="8f92c-165">If you chose tooconnect tooAzure Log Analytics (OMS), paste hello **Workspace ID** and **Workspace Key (Primary Key)** that you copied into Notepad in hello previous procedure and then click **Next**.</span></span>  
        <span data-ttu-id="8f92c-166">![Cole o ID da área de trabalho e a chave primária](./media/log-analytics-windows-agents/connect-workspace.png)</span><span class="sxs-lookup"><span data-stu-id="8f92c-166">![paste Workspace ID and Primary Key](./media/log-analytics-windows-agents/connect-workspace.png)</span></span>
    - <span data-ttu-id="8f92c-167">Se tiver escolhido tooconnect tooOperations Manager, escreva Olá **Management Group Name**, **servidor de gestão** nome, e **porta do servidor de gestão**e, em seguida, clique em **Seguinte**.</span><span class="sxs-lookup"><span data-stu-id="8f92c-167">If you chose tooconnect tooOperations Manager, type hello **Management Group Name**, **Management Server** name, and **Management Server Port**, and then click **Next**.</span></span> <span data-ttu-id="8f92c-168">Na página de conta de ação do agente de Olá, escolha a conta do sistema Local Olá ou uma conta de domínio local e, em seguida, clique em **seguinte**.</span><span class="sxs-lookup"><span data-stu-id="8f92c-168">On hello Agent Action Account page, choose either hello Local System account or a local domain account and then click **Next**.</span></span>  
        <span data-ttu-id="8f92c-169">![configuração do grupo de gestão](./media/log-analytics-windows-agents/oms-mma-om-setup01.png)![conta de ação do agente](./media/log-analytics-windows-agents/oms-mma-om-setup02.png)</span><span class="sxs-lookup"><span data-stu-id="8f92c-169">![management group configuration](./media/log-analytics-windows-agents/oms-mma-om-setup01.png)![agent action account](./media/log-analytics-windows-agents/oms-mma-om-setup02.png)</span></span>

6. <span data-ttu-id="8f92c-170">Na página de tooInstall pronto Olá, reveja as suas opções e, em seguida, clique em **instalar**.</span><span class="sxs-lookup"><span data-stu-id="8f92c-170">On hello Ready tooInstall page, review your choices and then click **Install**.</span></span>
7. <span data-ttu-id="8f92c-171">No Olá concluir com êxito a configuração da página, clique em **concluir**.</span><span class="sxs-lookup"><span data-stu-id="8f92c-171">On hello Configuration completed successfully page, click **Finish**.</span></span>
8. <span data-ttu-id="8f92c-172">Quando terminar, Olá **Microsoft Monitoring Agent** aparece no **painel de controlo**.</span><span class="sxs-lookup"><span data-stu-id="8f92c-172">When complete, hello **Microsoft Monitoring Agent** appears in **Control Panel**.</span></span> <span data-ttu-id="8f92c-173">Pode rever a configuração não existe e certifique-se de que o agente Olá tooOperational ligado Insights (OMS).</span><span class="sxs-lookup"><span data-stu-id="8f92c-173">You can review your configuration there and verify that hello agent is connected tooOperational Insights (OMS).</span></span> <span data-ttu-id="8f92c-174">Quando Olá tooOMS ligados, o agente apresenta uma mensagem a indicar: **Olá Microsoft Monitoring Agent foi ligado com êxito o serviço do Microsoft Operations Management Suite toohello.**</span><span class="sxs-lookup"><span data-stu-id="8f92c-174">When connected tooOMS, hello agent displays a message stating: **hello Microsoft Monitoring Agent has successfully connected toohello Microsoft Operations Management Suite service.**</span></span>

## <a name="configure-proxy-settings"></a><span data-ttu-id="8f92c-175">Configurar definições de proxy</span><span class="sxs-lookup"><span data-stu-id="8f92c-175">Configure proxy settings</span></span>

<span data-ttu-id="8f92c-176">Pode utilizar Olá seguir o procedimento tooconfigure as definições de proxy Olá Microsoft Monitoring Agent utilizando o painel de controlo.</span><span class="sxs-lookup"><span data-stu-id="8f92c-176">You can use hello following procedure tooconfigure proxy settings for hello Microsoft Monitoring Agent using Control Panel.</span></span> <span data-ttu-id="8f92c-177">É necessário toouse este procedimento para cada servidor.</span><span class="sxs-lookup"><span data-stu-id="8f92c-177">You need toouse this procedure for each server.</span></span> <span data-ttu-id="8f92c-178">Se tiver vários servidores que precisa de tooconfigure, poderá considerar mais fácil toouse tooautomate um script este processo.</span><span class="sxs-lookup"><span data-stu-id="8f92c-178">If you have many servers that you need tooconfigure, you might find it easier toouse a script tooautomate this process.</span></span> <span data-ttu-id="8f92c-179">Se Sim, consulte o procedimento seguinte Olá [tooconfigure as definições de proxy para o Microsoft Monitoring Agent utilizando um script de Olá](#to-configure-proxy-settings-for-the-microsoft-monitoring-agent-using-a-script).</span><span class="sxs-lookup"><span data-stu-id="8f92c-179">If so, see hello next procedure [tooconfigure proxy settings for hello Microsoft Monitoring Agent using a script](#to-configure-proxy-settings-for-the-microsoft-monitoring-agent-using-a-script).</span></span>

### <a name="tooconfigure-proxy-settings-for-hello-microsoft-monitoring-agent-using-control-panel"></a><span data-ttu-id="8f92c-180">definições de proxy tooconfigure Olá Microsoft Monitoring Agent utilizando o painel de controlo</span><span class="sxs-lookup"><span data-stu-id="8f92c-180">tooconfigure proxy settings for hello Microsoft Monitoring Agent using Control Panel</span></span>
1. <span data-ttu-id="8f92c-181">Abra o **Painel de Controlo**.</span><span class="sxs-lookup"><span data-stu-id="8f92c-181">Open **Control Panel**.</span></span>
2. <span data-ttu-id="8f92c-182">Abra o **Agente de Monitorização da Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="8f92c-182">Open **Microsoft Monitoring Agent**.</span></span>
3. <span data-ttu-id="8f92c-183">Clique em Olá **as definições de Proxy** separador.</span><span class="sxs-lookup"><span data-stu-id="8f92c-183">Click hello **Proxy Settings** tab.</span></span>  
    <span data-ttu-id="8f92c-184">![separador de definições de proxy](./media/log-analytics-windows-agents/proxy-direct-agent-proxy.png)</span><span class="sxs-lookup"><span data-stu-id="8f92c-184">![proxy settings tab](./media/log-analytics-windows-agents/proxy-direct-agent-proxy.png)</span></span>
4. <span data-ttu-id="8f92c-185">Selecione **utilizar um servidor proxy** e escreva o URL de Olá e número de porta, se um exemplo de toohello necessários, semelhante mostrado.</span><span class="sxs-lookup"><span data-stu-id="8f92c-185">Select **Use a proxy server** and type hello URL and port number, if one is needed, similar toohello example shown.</span></span> <span data-ttu-id="8f92c-186">Se o servidor proxy requer autenticação, escreva Olá nome de utilizador e palavra-passe tooaccess Olá servidor proxy.</span><span class="sxs-lookup"><span data-stu-id="8f92c-186">If your proxy server requires authentication, type hello username and password tooaccess hello proxy server.</span></span>


### <a name="verify-agent-connectivity-toooms"></a><span data-ttu-id="8f92c-187">Certifique-se tooOMS de conectividade de agente</span><span class="sxs-lookup"><span data-stu-id="8f92c-187">Verify agent connectivity tooOMS</span></span>

<span data-ttu-id="8f92c-188">Pode facilmente verificar se os agentes estão a comunicar com o OMS Olá seguir o procedimento a utilizar:</span><span class="sxs-lookup"><span data-stu-id="8f92c-188">You can easily verify whether your agents are communicating with OMS using hello following procedure:</span></span>

1.  <span data-ttu-id="8f92c-189">No computador de Olá com o agente do Windows hello, abra o painel de controlo.</span><span class="sxs-lookup"><span data-stu-id="8f92c-189">On hello computer with hello Windows agent, open Control Panel.</span></span>
2.  <span data-ttu-id="8f92c-190">Abra o Microsoft Monitoring Agent.</span><span class="sxs-lookup"><span data-stu-id="8f92c-190">Open Microsoft Monitoring Agent.</span></span>
3.  <span data-ttu-id="8f92c-191">Clique Olá separador de análise de registos do Azure (OMS).</span><span class="sxs-lookup"><span data-stu-id="8f92c-191">Click hello Azure Log Analytics (OMS) tab.</span></span>
4.  <span data-ttu-id="8f92c-192">Na coluna de estado de Olá, deverá ver que o agente Olá ligado com êxito toohello o serviço do Operations Management Suite.</span><span class="sxs-lookup"><span data-stu-id="8f92c-192">In hello Status column, you should see that hello agent connected successfully toohello Operations Management Suite service.</span></span>

![agente ligado](./media/log-analytics-windows-agents/mma-connected.png)


### <a name="tooconfigure-proxy-settings-for-hello-microsoft-monitoring-agent-using-a-script"></a><span data-ttu-id="8f92c-194">definições de proxy tooconfigure Olá Microsoft Monitoring Agent utilizando um script</span><span class="sxs-lookup"><span data-stu-id="8f92c-194">tooconfigure proxy settings for hello Microsoft Monitoring Agent using a script</span></span>
<span data-ttu-id="8f92c-195">Copie Olá seguinte exemplo, atualizá-lo com o ambiente de tooyour específicos de informação, guarde-o com uma extensão de nome de ficheiro PS1 e, em seguida, execute o script de Olá em cada computador que estabelece diretamente ligação de serviço do toohello OMS.</span><span class="sxs-lookup"><span data-stu-id="8f92c-195">Copy hello following sample, update it with information specific tooyour environment, save it with a PS1 file name extension, and then run hello script on each computer that connects directly toohello OMS service.</span></span>

    param($ProxyDomainName="http://proxy.contoso.com:80", $cred=(Get-Credential))

    # First we get hello Health Service configuration object.  We need toodetermine if we
    #have hello right update rollup with hello API we need.  If not, no need toorun hello rest of hello script.
    $healthServiceSettings = New-Object -ComObject 'AgentConfigManager.MgmtSvcCfg'

    $proxyMethod = $healthServiceSettings | Get-Member -Name 'SetProxyInfo'

    if (!$proxyMethod)
    {
         Write-Output 'Health Service proxy API not present, will not update settings.'
         return
    }

    Write-Output "Clearing proxy settings."
    $healthServiceSettings.SetProxyInfo('', '', '')

    $ProxyUserName = $cred.username

    Write-Output "Setting proxy too$ProxyDomainName with proxy username $ProxyUserName."
    $healthServiceSettings.SetProxyInfo($ProxyDomainName, $ProxyUserName, $cred.GetNetworkCredential().password)



## <a name="install-hello-agent-using-hello-command-line"></a><span data-ttu-id="8f92c-196">Instalar o agente de Olá utilizando a linha de comandos Olá</span><span class="sxs-lookup"><span data-stu-id="8f92c-196">Install hello agent using hello command line</span></span>
- <span data-ttu-id="8f92c-197">Modificar e, em seguida, utilize Olá seguinte agente Olá tooinstall de exemplo utilizando Olá linha de comandos.</span><span class="sxs-lookup"><span data-stu-id="8f92c-197">Modify and then use hello following example tooinstall hello agent using hello command line.</span></span> <span data-ttu-id="8f92c-198">exemplo de Olá executa uma instalação totalmente automática.</span><span class="sxs-lookup"><span data-stu-id="8f92c-198">hello example performs a fully silent installation.</span></span>

    >[!NOTE]
    <span data-ttu-id="8f92c-199">Se quiser tooupgrade um agente, terá de toouse Olá Log Analytics API de scripting.</span><span class="sxs-lookup"><span data-stu-id="8f92c-199">If you want tooupgrade an agent, you need toouse hello Log Analytics scripting API.</span></span> <span data-ttu-id="8f92c-200">Consulte Olá seguinte secção tooupgrade um agente.</span><span class="sxs-lookup"><span data-stu-id="8f92c-200">See hello next section tooupgrade an agent.</span></span>

    ```dos
    MMASetup-AMD64.exe /Q:A /R:N /C:"setup.exe /qn ADD_OPINSIGHTS_WORKSPACE=1 OPINSIGHTS_WORKSPACE_ID=<your workspace id> OPINSIGHTS_WORKSPACE_KEY=<your workspace key> AcceptEndUserLicenseAgreement=1"
    ```

<span data-ttu-id="8f92c-201">agente de Olá utiliza IExpress como respetivo Self-extractor utilizando Olá `/c` comando.</span><span class="sxs-lookup"><span data-stu-id="8f92c-201">hello agent uses IExpress as its self-extractor using hello `/c` command.</span></span> <span data-ttu-id="8f92c-202">Pode ver os parâmetros da linha de comandos do Olá em [comutadores da linha de comandos para IExpress](https://support.microsoft.com/help/197147/command-line-switches-for-iexpress-software-update-packages) e, em seguida, atualização Olá exemplo toosuit às suas necessidades.</span><span class="sxs-lookup"><span data-stu-id="8f92c-202">You can see hello command-line switches at [Command-line switches for IExpress](https://support.microsoft.com/help/197147/command-line-switches-for-iexpress-software-update-packages) and then update hello example toosuit your needs.</span></span>

|<span data-ttu-id="8f92c-203">Opções de MMA específico</span><span class="sxs-lookup"><span data-stu-id="8f92c-203">MMA-specific options</span></span>                   |<span data-ttu-id="8f92c-204">Notas</span><span class="sxs-lookup"><span data-stu-id="8f92c-204">Notes</span></span>         |
|---------------------------------------|--------------|
|<span data-ttu-id="8f92c-205">ADD_OPINSIGHTS_WORKSPACE</span><span class="sxs-lookup"><span data-stu-id="8f92c-205">ADD_OPINSIGHTS_WORKSPACE</span></span>               | <span data-ttu-id="8f92c-206">1 = área de trabalho do configurar Olá agente tooreport tooa</span><span class="sxs-lookup"><span data-stu-id="8f92c-206">1 = Configure hello agent tooreport tooa workspace</span></span>                |
|<span data-ttu-id="8f92c-207">OPINSIGHTS_WORKSPACE_ID</span><span class="sxs-lookup"><span data-stu-id="8f92c-207">OPINSIGHTS_WORKSPACE_ID</span></span>                | <span data-ttu-id="8f92c-208">Id da área de trabalho (guid) para Olá tooadd de área de trabalho</span><span class="sxs-lookup"><span data-stu-id="8f92c-208">Workspace Id (guid) for hello workspace tooadd</span></span>                    |
|<span data-ttu-id="8f92c-209">OPINSIGHTS_WORKSPACE_KEY</span><span class="sxs-lookup"><span data-stu-id="8f92c-209">OPINSIGHTS_WORKSPACE_KEY</span></span>               | <span data-ttu-id="8f92c-210">Autenticar tooinitially utilizada chave de área de trabalho com área de trabalho Olá</span><span class="sxs-lookup"><span data-stu-id="8f92c-210">Workspace key used tooinitially authenticate with hello workspace</span></span> |
|<span data-ttu-id="8f92c-211">OPINSIGHTS_WORKSPACE_AZURE_CLOUD_TYPE</span><span class="sxs-lookup"><span data-stu-id="8f92c-211">OPINSIGHTS_WORKSPACE_AZURE_CLOUD_TYPE</span></span>  | <span data-ttu-id="8f92c-212">Especifique o ambiente de nuvem olá onde está localizada a área de trabalho Olá</span><span class="sxs-lookup"><span data-stu-id="8f92c-212">Specify hello cloud environment where hello workspace is located</span></span> <br> <span data-ttu-id="8f92c-213">0 = em nuvem comerciais do azure (predefinição)</span><span class="sxs-lookup"><span data-stu-id="8f92c-213">0 = Azure commercial cloud (default)</span></span> <br> <span data-ttu-id="8f92c-214">1 = azure Government</span><span class="sxs-lookup"><span data-stu-id="8f92c-214">1 = Azure Government</span></span> |
|<span data-ttu-id="8f92c-215">OPINSIGHTS_PROXY_URL</span><span class="sxs-lookup"><span data-stu-id="8f92c-215">OPINSIGHTS_PROXY_URL</span></span>               | <span data-ttu-id="8f92c-216">URI para Olá proxy toouse</span><span class="sxs-lookup"><span data-stu-id="8f92c-216">URI for hello proxy toouse</span></span> |
|<span data-ttu-id="8f92c-217">OPINSIGHTS_PROXY_USERNAME</span><span class="sxs-lookup"><span data-stu-id="8f92c-217">OPINSIGHTS_PROXY_USERNAME</span></span>               | <span data-ttu-id="8f92c-218">Nome de utilizador tooaccess um proxy autenticado</span><span class="sxs-lookup"><span data-stu-id="8f92c-218">Username tooaccess an authenticated proxy</span></span> |
|<span data-ttu-id="8f92c-219">OPINSIGHTS_PROXY_PASSWORD</span><span class="sxs-lookup"><span data-stu-id="8f92c-219">OPINSIGHTS_PROXY_PASSWORD</span></span>               | <span data-ttu-id="8f92c-220">Palavra-passe tooaccess um proxy autenticado</span><span class="sxs-lookup"><span data-stu-id="8f92c-220">Password tooaccess an authenticated proxy</span></span> |

>[!NOTE]
<span data-ttu-id="8f92c-221">limite de comprimento de linha de comandos atingir de Olá do tooavoid de IExpress, instale o agente de Olá com nenhuma área de trabalho configurada e, em seguida, utilizar uma configuração de tooset de script para a área de trabalho de Olá.</span><span class="sxs-lookup"><span data-stu-id="8f92c-221">tooavoid hitting hello command-line length limit of IExpress, install hello agent with no workspace configured and then use a script tooset configuration for hello workspace.</span></span>

>[!NOTE]
<span data-ttu-id="8f92c-222">Se obtiver um `Command line option syntax error.` quando utilizar Olá `OPINSIGHTS_WORKSPACE_AZURE_CLOUD_TYPE` parâmetro, pode utilizar Olá solução os seguintes:</span><span class="sxs-lookup"><span data-stu-id="8f92c-222">If you get a `Command line option syntax error.` when using hello `OPINSIGHTS_WORKSPACE_AZURE_CLOUD_TYPE` parameter, you can use hello following workaround:</span></span>
```dos
MMASetup-AMD64.exe /C /T:.\MMAExtract
cd .\MMAExtract
setup.exe /qn ADD_OPINSIGHTS_WORKSPACE=1 OPINSIGHTS_WORKSPACE_AZURE_CLOUD_TYPE=1 OPINSIGHTS_WORKSPACE_ID=<your workspace id> OPINSIGHTS_WORKSPACE_KEY=<your workspace key> AcceptEndUserLicenseAgreement=1
```

## <a name="add-a-workspace-using-a-script"></a><span data-ttu-id="8f92c-223">Adicionar uma área de trabalho através de um script</span><span class="sxs-lookup"><span data-stu-id="8f92c-223">Add a workspace using a script</span></span>
<span data-ttu-id="8f92c-224">Adicione uma área de trabalho utilizando a API de scripting de agente do Olá análise de registos com o seguinte exemplo de Olá:</span><span class="sxs-lookup"><span data-stu-id="8f92c-224">Add a workspace using hello Log Analytics agent scripting API with hello following example:</span></span>

```PowerShell
$mma = New-Object -ComObject 'AgentConfigManager.MgmtSvcCfg'
$mma.AddCloudWorkspace($workspaceId, $workspaceKey)
$mma.ReloadConfiguration()
```

<span data-ttu-id="8f92c-225">tooadd uma área de trabalho do Azure para US Government, Olá utilizar script de exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="8f92c-225">tooadd a workspace in Azure for US Government, use hello following script sample:</span></span>
```PowerShell
$mma = New-Object -ComObject 'AgentConfigManager.MgmtSvcCfg'
$mma.AddCloudWorkspace($workspaceId, $workspaceKey, 1)
$mma.ReloadConfiguration()
```

>[!NOTE]
<span data-ttu-id="8f92c-226">Se tiver utilizado a linha de comandos Olá ou script anteriormente tooinstall ou configurar o agente de Olá, `EnableAzureOperationalInsights` foi substituído por `AddCloudWorkspace`.</span><span class="sxs-lookup"><span data-stu-id="8f92c-226">If you've used hello command line or script previously tooinstall or configure hello agent, `EnableAzureOperationalInsights` was replaced by `AddCloudWorkspace`.</span></span>

## <a name="install-hello-agent-using-dsc-in-azure-automation"></a><span data-ttu-id="8f92c-227">Instalar o agente de Olá utilizando DSC na automatização do Azure</span><span class="sxs-lookup"><span data-stu-id="8f92c-227">Install hello agent using DSC in Azure Automation</span></span>

<span data-ttu-id="8f92c-228">Pode utilizar Olá seguinte script exemplo tooinstall Olá agente utilizando DSC na automatização do Azure.</span><span class="sxs-lookup"><span data-stu-id="8f92c-228">You can use hello following script example tooinstall hello agent using DSC in Azure Automation.</span></span> <span data-ttu-id="8f92c-229">exemplo de Olá instala Olá agente de 64 bits, identificado por Olá `URI` valor.</span><span class="sxs-lookup"><span data-stu-id="8f92c-229">hello example installs hello 64-bit agent, identified by hello `URI` value.</span></span> <span data-ttu-id="8f92c-230">Também pode utilizar a versão de 32 bits Olá, substituindo o valor do URI Olá.</span><span class="sxs-lookup"><span data-stu-id="8f92c-230">You can also use hello 32-bit version by replacing hello URI value.</span></span> <span data-ttu-id="8f92c-231">Olá URIs para ambas as versões são:</span><span class="sxs-lookup"><span data-stu-id="8f92c-231">hello URIs for both versions are:</span></span>

- <span data-ttu-id="8f92c-232">O agente de 64 bits do Windows - https://go.microsoft.com/fwlink/?LinkId=828603</span><span class="sxs-lookup"><span data-stu-id="8f92c-232">Windows 64-bit agent - https://go.microsoft.com/fwlink/?LinkId=828603</span></span>
- <span data-ttu-id="8f92c-233">O agente de 32 bits do Windows - https://go.microsoft.com/fwlink/?LinkId=828604</span><span class="sxs-lookup"><span data-stu-id="8f92c-233">Windows 32-bit agent - https://go.microsoft.com/fwlink/?LinkId=828604</span></span>


>[!NOTE]
<span data-ttu-id="8f92c-234">Este procedimento e o script de exemplo não irá atualizar um agente existente.</span><span class="sxs-lookup"><span data-stu-id="8f92c-234">This procedure and script example will not upgrade an existing agent.</span></span>

1. <span data-ttu-id="8f92c-235">Importar Olá xPSDesiredStateConfiguration módulo DSC de [http://www.powershellgallery.com/packages/xPSDesiredStateConfiguration](http://www.powershellgallery.com/packages/xPSDesiredStateConfiguration) na automatização do Azure.</span><span class="sxs-lookup"><span data-stu-id="8f92c-235">Import hello xPSDesiredStateConfiguration DSC Module from [http://www.powershellgallery.com/packages/xPSDesiredStateConfiguration](http://www.powershellgallery.com/packages/xPSDesiredStateConfiguration) into Azure Automation.</span></span>  
2.  <span data-ttu-id="8f92c-236">Criar recursos de variável de automatização do Azure para *OPSINSIGHTS_WS_ID* e *OPSINSIGHTS_WS_KEY*.</span><span class="sxs-lookup"><span data-stu-id="8f92c-236">Create Azure Automation variable assets for *OPSINSIGHTS_WS_ID* and *OPSINSIGHTS_WS_KEY*.</span></span> <span data-ttu-id="8f92c-237">Definir *OPSINSIGHTS_WS_ID* tooyour ID da área de trabalho de análise de registos do OMS e defina *OPSINSIGHTS_WS_KEY* toohello chave primária da sua área de trabalho.</span><span class="sxs-lookup"><span data-stu-id="8f92c-237">Set *OPSINSIGHTS_WS_ID* tooyour OMS Log Analytics workspace ID and set *OPSINSIGHTS_WS_KEY* toohello primary key of your workspace.</span></span>
3.  <span data-ttu-id="8f92c-238">Utilizar Olá script a seguir e guarde-o como MMAgent.ps1</span><span class="sxs-lookup"><span data-stu-id="8f92c-238">Use hello following script and save it as MMAgent.ps1</span></span>
4.  <span data-ttu-id="8f92c-239">Modificar e, em seguida, utilize Olá seguinte agente Olá tooinstall de exemplo utilizando DSC na automatização do Azure.</span><span class="sxs-lookup"><span data-stu-id="8f92c-239">Modify and then use hello following example tooinstall hello agent using DSC in Azure Automation.</span></span> <span data-ttu-id="8f92c-240">Importe MMAgent.ps1 para automatização do Azure utilizando a interface de automatização do Azure Olá ou o cmdlet.</span><span class="sxs-lookup"><span data-stu-id="8f92c-240">Import MMAgent.ps1 into Azure Automation by using hello Azure Automation interface or cmdlet.</span></span>
5.  <span data-ttu-id="8f92c-241">Atribua uma configuração de toohello de nó.</span><span class="sxs-lookup"><span data-stu-id="8f92c-241">Assign a node toohello configuration.</span></span> <span data-ttu-id="8f92c-242">Em 15 minutos, o nó de Olá verifica a respetiva configuração e Olá MMA é feito o Push de nó toohello.</span><span class="sxs-lookup"><span data-stu-id="8f92c-242">Within 15 minutes, hello node checks its configuration and hello MMA is pushed toohello node.</span></span>

```PowerShell
Configuration MMAgent
{
    $OIPackageLocalPath = "C:\MMASetup-AMD64.exe"
    $OPSINSIGHTS_WS_ID = Get-AutomationVariable -Name "OPSINSIGHTS_WS_ID"
    $OPSINSIGHTS_WS_KEY = Get-AutomationVariable -Name "OPSINSIGHTS_WS_KEY"


    Import-DscResource -ModuleName xPSDesiredStateConfiguration

    Node OMSnode {
        Service OIService
        {
            Name = "HealthService"
            State = "Running"
            DependsOn = "[Package]OI"
        }

        xRemoteFile OIPackage {
            Uri = "https://go.microsoft.com/fwlink/?LinkId=828603"
            DestinationPath = $OIPackageLocalPath
        }

        Package OI {
            Ensure = "Present"
            Path  = $OIPackageLocalPath
            Name = "Microsoft Monitoring Agent"
            ProductId = "8A7F2C51-4C7D-4BFD-9014-91D11F24AAE2"
            Arguments = '/C:"setup.exe /qn ADD_OPINSIGHTS_WORKSPACE=1 OPINSIGHTS_WORKSPACE_ID=' + $OPSINSIGHTS_WS_ID + ' OPINSIGHTS_WORKSPACE_KEY=' + $OPSINSIGHTS_WS_KEY + ' AcceptEndUserLicenseAgreement=1"'
            DependsOn = "[xRemoteFile]OIPackage"
        }
    }
}


```

### <a name="get-hello-latest-productid-value"></a><span data-ttu-id="8f92c-243">Obter o valor de ProductId Olá mais recente</span><span class="sxs-lookup"><span data-stu-id="8f92c-243">Get hello latest ProductId value</span></span>

<span data-ttu-id="8f92c-244">Olá `ProductId value` Olá MMAgent.ps1 script é a versão do agente tooeach exclusivo.</span><span class="sxs-lookup"><span data-stu-id="8f92c-244">hello `ProductId value` in hello MMAgent.ps1 script is unique tooeach agent version.</span></span> <span data-ttu-id="8f92c-245">Quando uma versão atualizada de cada agente for publicada, alterações Olá ProductId valor.</span><span class="sxs-lookup"><span data-stu-id="8f92c-245">When an updated version of each agent is published, hello ProductId value changes.</span></span> <span data-ttu-id="8f92c-246">Por isso, quando Olá ProductId for alterada no futuro Olá, pode encontrar a versão do agente Olá através de um script simple.</span><span class="sxs-lookup"><span data-stu-id="8f92c-246">So, when hello ProductId changes in hello future, you can find hello agent version using a simple script.</span></span> <span data-ttu-id="8f92c-247">Depois de ter Olá mais recente versão do agente instalado no servidor de teste, pode utilizar Olá seguinte script tooget Olá instalado ProductId valor.</span><span class="sxs-lookup"><span data-stu-id="8f92c-247">After you have hello latest agent version installed on a test server, you can use hello following script tooget hello installed ProductId value.</span></span> <span data-ttu-id="8f92c-248">Utilizar o valor de ProductId mais recente Olá, pode atualizar o valor Olá Olá MMAgent.ps1 script.</span><span class="sxs-lookup"><span data-stu-id="8f92c-248">Using hello latest ProductId value, you can update hello value in hello MMAgent.ps1 script.</span></span>

```PowerShell
$InstalledApplications  = Get-ChildItem hklm:\SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall


foreach ($Application in $InstalledApplications)

{

     $Key = Get-ItemProperty $Application.PSPath

     if ($Key.DisplayName -eq "Microsoft Monitoring Agent")

     {

        $Key.DisplayName

        Write-Output ("Product ID is: " + $Key.PSChildName.Substring(1,$Key.PSChildName.Length -2))

     }

}  
```

## <a name="configure-an-agent-manually-or-add-additional-workspaces"></a><span data-ttu-id="8f92c-249">Configure manualmente um agente ou adicione áreas de trabalho adicionais</span><span class="sxs-lookup"><span data-stu-id="8f92c-249">Configure an agent manually or add additional workspaces</span></span>
<span data-ttu-id="8f92c-250">Se instalou agentes, mas não foi possível configurá-las ou se quiser áreas de trabalho do Olá agente tooreport toomultiple, pode utilizar Olá seguir informações tooenable um agente ou reconfigurá-lo.</span><span class="sxs-lookup"><span data-stu-id="8f92c-250">If you've installed agents but did not configure them or if you want hello agent tooreport toomultiple workspaces, you can use hello following information tooenable an agent or reconfigure it.</span></span> <span data-ttu-id="8f92c-251">Depois de configurar o agente de Olá, vai registar com o serviço de agente Olá e irá obter as informações de configuração necessário e pacotes de gestão que contêm informações de soluções.</span><span class="sxs-lookup"><span data-stu-id="8f92c-251">After you've configured hello agent, it will register with hello agent service and will get necessary configuration information and management packs that contain solution information.</span></span>

1. <span data-ttu-id="8f92c-252">Depois de instalar o Microsoft Monitoring Agent de Olá, abra **painel de controlo**.</span><span class="sxs-lookup"><span data-stu-id="8f92c-252">After you've installed hello Microsoft Monitoring Agent, open **Control Panel**.</span></span>
2. <span data-ttu-id="8f92c-253">Abra **Microsoft Monitoring Agent** e, em seguida, clique em Olá **análise de registos do Azure (OMS)** separador.</span><span class="sxs-lookup"><span data-stu-id="8f92c-253">Open **Microsoft Monitoring Agent** and then click hello **Azure Log Analytics (OMS)** tab.</span></span>   
3. <span data-ttu-id="8f92c-254">Clique em **adicionar** tooopen Olá **adicionar uma área de trabalho de análise do registo** caixa.</span><span class="sxs-lookup"><span data-stu-id="8f92c-254">Click **Add** tooopen hello **Add a Log Analytics Workspace** box.</span></span>
4. <span data-ttu-id="8f92c-255">Olá colar **ID da área de trabalho** e **chave da área de trabalho (chave primária)** copiado no bloco de notas num procedimento anterior para a área de trabalho de Olá que pretende tooadd e, em seguida, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="8f92c-255">Paste hello **Workspace ID** and **Workspace Key (Primary Key)** that you copied into Notepad in a previous procedure for hello workspace that you want tooadd and then click **OK**.</span></span>  
    <span data-ttu-id="8f92c-256">![configurar as informações operacionais](./media/log-analytics-windows-agents/add-workspace.png)</span><span class="sxs-lookup"><span data-stu-id="8f92c-256">![configure Operational Insights](./media/log-analytics-windows-agents/add-workspace.png)</span></span>

<span data-ttu-id="8f92c-257">Depois dos dados são recolhidos a partir de computadores monitorizados por agente Olá, número de Olá dos computadores monitorizados pelo OMS irão aparecer no portal do OMS Olá no Olá **origens ligadas** separador **definições** como  **Servidores ligados**.</span><span class="sxs-lookup"><span data-stu-id="8f92c-257">After data is collected from computers monitored by hello agent, hello number of computers monitored by OMS will appear in hello OMS portal on hello **Connected Sources** tab in **Settings** as **Servers Connected**.</span></span>


## <a name="toodisable-an-agent"></a><span data-ttu-id="8f92c-258">toodisable um agente</span><span class="sxs-lookup"><span data-stu-id="8f92c-258">toodisable an agent</span></span>
1. <span data-ttu-id="8f92c-259">Depois de instalar o agente de Olá, abra **painel de controlo**.</span><span class="sxs-lookup"><span data-stu-id="8f92c-259">After installing hello agent, open **Control Panel**.</span></span>
2. <span data-ttu-id="8f92c-260">Abra o Microsoft Monitoring Agent e, em seguida, clique em Olá **análise de registos do Azure (OMS)** separador.</span><span class="sxs-lookup"><span data-stu-id="8f92c-260">Open Microsoft Monitoring Agent and then click hello **Azure Log Analytics (OMS)** tab.</span></span>
3. <span data-ttu-id="8f92c-261">Selecione uma área de trabalho e, em seguida, clique em **remover**.</span><span class="sxs-lookup"><span data-stu-id="8f92c-261">Select a workspace and then click **Remove**.</span></span> <span data-ttu-id="8f92c-262">Repita este passo para todas as outras áreas de trabalho.</span><span class="sxs-lookup"><span data-stu-id="8f92c-262">Repeat this step for all other workspaces.</span></span>


## <a name="optionally-configure-agents-tooreport-tooan-operations-manager-management-group"></a><span data-ttu-id="8f92c-263">Opcionalmente, configure o grupo de gestão do agentes tooreport tooan do Operations Manager</span><span class="sxs-lookup"><span data-stu-id="8f92c-263">Optionally, configure agents tooreport tooan Operations Manager management group</span></span>

<span data-ttu-id="8f92c-264">Se utilizar o Operations Manager na sua infraestrutura de TI, também pode utilizar o agente MMA Olá como um agente do Operations Manager.</span><span class="sxs-lookup"><span data-stu-id="8f92c-264">If you use Operations Manager in your IT infrastructure, you can also use hello MMA agent as an Operations Manager agent.</span></span>

### <a name="tooconfigure-mma-agents-tooreport-tooan-operations-manager-management-group"></a><span data-ttu-id="8f92c-265">grupo de gestão ao Operations Manager do tooan de tooreport tooconfigure MMA agentes</span><span class="sxs-lookup"><span data-stu-id="8f92c-265">tooconfigure MMA agents tooreport tooan Operations Manager management group</span></span>
1.  <span data-ttu-id="8f92c-266">Olá onde está instalado o agente de Olá, abra no computador **painel de controlo**.</span><span class="sxs-lookup"><span data-stu-id="8f92c-266">On hello computer where hello agent is installed, open **Control Panel**.</span></span>  
2.  <span data-ttu-id="8f92c-267">Abra **Microsoft Monitoring Agent** e, em seguida, clique em Olá **do Operations Manager** separador.</span><span class="sxs-lookup"><span data-stu-id="8f92c-267">Open **Microsoft Monitoring Agent** and then click hello **Operations Manager** tab.</span></span>  
    <span data-ttu-id="8f92c-268">![Separador do Microsoft Monitoring Agent do Operations Manager](./media/log-analytics-windows-agents/om-mg01.png)</span><span class="sxs-lookup"><span data-stu-id="8f92c-268">![Microsoft Monitoring Agent Operations Manager tab](./media/log-analytics-windows-agents/om-mg01.png)</span></span>
3.  <span data-ttu-id="8f92c-269">Se os servidores do Operations Manager tem integração com o Active Directory, clique em **atualizar automaticamente atribuições de grupo de gestão do AD DS**.</span><span class="sxs-lookup"><span data-stu-id="8f92c-269">If your Operations Manager servers have integration with Active Directory, click **Automatically update management group assignments from AD DS**.</span></span>
4.  <span data-ttu-id="8f92c-270">Clique em **adicionar** tooopen Olá **adicionar um grupo de gestão** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="8f92c-270">Click **Add** tooopen hello **Add a Management Group** dialog box.</span></span>  
    <span data-ttu-id="8f92c-271">![O Microsoft Monitoring Agent adicionar um grupo de gestão](./media/log-analytics-windows-agents/oms-mma-om02.png)</span><span class="sxs-lookup"><span data-stu-id="8f92c-271">![Microsoft Monitoring Agent Add a Management Group](./media/log-analytics-windows-agents/oms-mma-om02.png)</span></span>
5.  <span data-ttu-id="8f92c-272">No **nome do grupo de gestão** caixa, o nome do tipo Olá do seu grupo de gestão.</span><span class="sxs-lookup"><span data-stu-id="8f92c-272">In **Management group name** box, type hello name of your management group.</span></span>
6.  <span data-ttu-id="8f92c-273">No Olá **servidor de gestão principal** caixa, nome de computador do tipo Olá Olá principal do servidor de gestão.</span><span class="sxs-lookup"><span data-stu-id="8f92c-273">In hello **Primary management server** box, type hello computer name of hello primary management server.</span></span>
7.  <span data-ttu-id="8f92c-274">No Olá **porta do servidor de gestão** caixa, número de porta TCP de Olá de tipo.</span><span class="sxs-lookup"><span data-stu-id="8f92c-274">In hello **Management server port** box, type hello TCP port number.</span></span>
8.  <span data-ttu-id="8f92c-275">Em **conta de ação do agente**, escolha a conta do sistema Local Olá ou uma conta de domínio local.</span><span class="sxs-lookup"><span data-stu-id="8f92c-275">Under **Agent Action Account**, choose either hello Local System account or a local domain account.</span></span>
9.  <span data-ttu-id="8f92c-276">Clique em **OK** tooclose Olá **adicionar um grupo de gestão** caixa de diálogo e, em seguida, clique em **OK** tooclose Olá **propriedades de agente de monitorização da Microsoft**caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="8f92c-276">Click **OK** tooclose hello **Add a Management Group** dialog box and then click **OK** tooclose hello **Microsoft Monitoring Agent Properties** dialog box.</span></span>


## <a name="next-steps"></a><span data-ttu-id="8f92c-277">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="8f92c-277">Next steps</span></span>

- <span data-ttu-id="8f92c-278">[Adicionar soluções de análise de registos de Olá soluções galeria](log-analytics-add-solutions.md) tooadd funcionalidade e a recolha de dados.</span><span class="sxs-lookup"><span data-stu-id="8f92c-278">[Add Log Analytics solutions from hello Solutions Gallery](log-analytics-add-solutions.md) tooadd functionality and gather data.</span></span>
