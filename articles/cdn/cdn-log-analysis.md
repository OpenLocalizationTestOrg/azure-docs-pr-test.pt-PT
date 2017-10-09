---
title: "análise de aaaLog para o Azure CDN | Microsoft Docs"
description: "Cliente pode ativar a análise de registos para a CDN do Azure."
services: cdn
documentationcenter: 
author: smcevoy
manager: erikre
editor: 
ms.assetid: 95e18b3c-b987-46c2-baa8-a27a029e3076
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/03/2017
ms.author: v-semcev
ms.openlocfilehash: 56e5a4fec46fd156cf38252732afb4522741d009
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="diagnostics-logs-for-azure-cdn"></a><span data-ttu-id="7eef5-103">Registos de diagnóstico para a CDN do Azure</span><span class="sxs-lookup"><span data-stu-id="7eef5-103">Diagnostics Logs for Azure CDN</span></span>

<span data-ttu-id="7eef5-104">Depois de ativar a CDN para a sua aplicação, irá provavelmente pretender a utilização CDN toomonitor Olá, verifique o estado de funcionamento de Olá do seu entrega e resolver problemas potenciais problemas.</span><span class="sxs-lookup"><span data-stu-id="7eef5-104">After enabling CDN for your application, you will likely want toomonitor hello CDN usage, check hello health of your delivery, and troubleshoot potential issues.</span></span> <span data-ttu-id="7eef5-105">CDN do Azure fornece mais capacidades com [análise de núcleo de CDN](cdn-analyze-usage-patterns.md) e [os registos de diagnóstico](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs)</span><span class="sxs-lookup"><span data-stu-id="7eef5-105">Azure CDN provides these capabilities with [CDN Core Analytics](cdn-analyze-usage-patterns.md) and [Diagnostic Logs](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs)</span></span>

## <a name="cdn-core-analytics"></a><span data-ttu-id="7eef5-106">Análise de núcleo CDN</span><span class="sxs-lookup"><span data-stu-id="7eef5-106">CDN Core Analytics</span></span>
<span data-ttu-id="7eef5-107">Como um utilizador CDN do Azure atual com o perfil de premium ou standard da Verizon, já estiver tooview capaz de análise de núcleo no portal suplementar Olá acessível através da opção de "Gerir" Olá da Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="7eef5-107">As a current Azure CDN user with Verizon standard or premium profile, you are already able tooview core analytics in hello supplemental portal accessible via hello "Manage" option from hello Azure portal.</span></span> 

## <a name="azure-diagnostic-logs"></a><span data-ttu-id="7eef5-108">Registos de diagnóstico do Azure</span><span class="sxs-lookup"><span data-stu-id="7eef5-108">Azure Diagnostic Logs</span></span>

<span data-ttu-id="7eef5-109">O Azure com esta nova funcionalidade, pode agora ver análise de núcleo e guardá-las para um ou mais destinos, incluindo:</span><span class="sxs-lookup"><span data-stu-id="7eef5-109">Azure With this new feature, you can now view core analytics and save them into one or more destinations including:</span></span>

 - <span data-ttu-id="7eef5-110">Conta de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="7eef5-110">Azure Storage account</span></span>
 - <span data-ttu-id="7eef5-111">Azure Event Hubs</span><span class="sxs-lookup"><span data-stu-id="7eef5-111">Azure Event Hubs</span></span>
 - [<span data-ttu-id="7eef5-112">Repositório de análise de registos do OMS</span><span class="sxs-lookup"><span data-stu-id="7eef5-112">OMS Log Analytics repository</span></span>](https://docs.microsoft.com/azure/log-analytics/log-analytics-get-started)
 
 <span data-ttu-id="7eef5-113">Esta funcionalidade está disponível para todos os pontos finais da CDN que pertencem tooVerizon (Standard e Premium) e perfis da CDN Akamai (Standard).</span><span class="sxs-lookup"><span data-stu-id="7eef5-113">This feature is available for all CDN endpoints belonging tooVerizon (Standard & Premium) and Akamai (Standard) CDN Profiles.</span></span>

<span data-ttu-id="7eef5-114">Registos de diagnóstico permitem-lhe tooexport métricas de utilização básica da sua variedade de tooa de ponto final CDN de origens de modo a que pode aceder aos mesmos de forma personalizada.</span><span class="sxs-lookup"><span data-stu-id="7eef5-114">Diagnostics logs allow you tooexport basic usage metrics from your CDN endpoint tooa variety of sources so that you can consume them in a customized way.</span></span> <span data-ttu-id="7eef5-115">Por exemplo, pode fazê-lo Olá os seguintes tipos de exportação de dados:</span><span class="sxs-lookup"><span data-stu-id="7eef5-115">For example, you can do hello following types of data export:</span></span>

- <span data-ttu-id="7eef5-116">Exportar o armazenamento de dados tooblob, exportar tooCSV e gerar gráficos no excel.</span><span class="sxs-lookup"><span data-stu-id="7eef5-116">Export data tooblob storage, export tooCSV, and generate graphs in excel.</span></span>
- <span data-ttu-id="7eef5-117">Exporte os hubs de tooevent de dados e estar relacionados com a dados a partir de outros serviços do azure.</span><span class="sxs-lookup"><span data-stu-id="7eef5-117">Export data tooevent hubs and correlate with data from other azure services.</span></span>
- <span data-ttu-id="7eef5-118">Exportar dados toolog análise e ver dados no seu próprio espaço de trabalho do OMS</span><span class="sxs-lookup"><span data-stu-id="7eef5-118">Export data toolog analytics and view data in your own OMS work space</span></span>

<span data-ttu-id="7eef5-119">Olá figura seguinte mostra uma vista de análise de núcleo de CDN típica de dados.</span><span class="sxs-lookup"><span data-stu-id="7eef5-119">hello following figure shows a typical CDN Core Analytics view into data.</span></span>

![Portal – registos de diagnóstico](./media/cdn-diagnostics-log/01_OMS-workspace.png)

<span data-ttu-id="7eef5-121">*Figura 1 - vista de análise de núcleo de CDN*</span><span class="sxs-lookup"><span data-stu-id="7eef5-121">*Figure 1 - CDN Core Analytics view*</span></span>

<span data-ttu-id="7eef5-122">Olá seguir instruções passa pelo esquema Olá de dados de análise de núcleo Olá, os passos envolvidos na ativar a funcionalidade de Olá, entrega-los toovarious destinos e consumir nestes destinos.</span><span class="sxs-lookup"><span data-stu-id="7eef5-122">hello following walkthrough goes through hello schema of hello core analytics data, steps involved in enabling hello feature and delivering them toovarious destinations, and consuming from these destinations.</span></span>

## <a name="enable-logging-with-azure-portal"></a><span data-ttu-id="7eef5-123">Ativar o registo com o portal do Azure</span><span class="sxs-lookup"><span data-stu-id="7eef5-123">Enable logging with Azure portal</span></span>

> [!NOTE]
> <span data-ttu-id="7eef5-124">Olá registos de diagnóstico são ativados **desativar** por predefinição.</span><span class="sxs-lookup"><span data-stu-id="7eef5-124">hello diagnostics logs are turned **off** by default.</span></span> 

<span data-ttu-id="7eef5-125">Siga os passos de Olá abaixo tooenable registo CDN Core Analytics:</span><span class="sxs-lookup"><span data-stu-id="7eef5-125">Follow hello steps below tooenable logging with CDN Core Analytics:</span></span>

<span data-ttu-id="7eef5-126">Inicie sessão no toohello [portal do Azure](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="7eef5-126">Sign in toohello [Azure portal](http://portal.azure.com).</span></span> <span data-ttu-id="7eef5-127">Se ainda não tiver ativado para o fluxo de trabalho CDN [ativar a CDN do Azure](cdn-create-new-endpoint.md) antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="7eef5-127">If you don't already have CDN enabled for your workflow, [Enable Azure CDN](cdn-create-new-endpoint.md) before you continue.</span></span>

1. <span data-ttu-id="7eef5-128">No portal de Olá, navegue até demasiado**perfil da CDN**.</span><span class="sxs-lookup"><span data-stu-id="7eef5-128">In hello portal, navigate too**CDN profile**.</span></span>
2. <span data-ttu-id="7eef5-129">Selecione um perfil CDN, em seguida, selecione o ponto final de CDN Olá que pretende que o tooenable **registos de diagnóstico**.</span><span class="sxs-lookup"><span data-stu-id="7eef5-129">Select a CDN profile, then select hello CDN endpoint that you want tooenable **Diagnostics Logs**.</span></span>

    ![Portal – registos de diagnóstico](./media/cdn-diagnostics-log/02_Browse-to-Diagnostics-logs.png)

3. <span data-ttu-id="7eef5-131">Aceda demasiado**registos de diagnóstico** painel em **monitorização** secção, em seguida, alterar o estado de Olá demasiado**no**.</span><span class="sxs-lookup"><span data-stu-id="7eef5-131">Go too**Diagnostics Logs** blade Under **Monitoring** section, then change hello status too**On**.</span></span>

    ![Portal – registos de diagnóstico](./media/cdn-diagnostics-log/03_Diagnostics-logs-options.png)

### <a name="enable-logging-with-azure-storage"></a><span data-ttu-id="7eef5-133">Ativar o registo com o Storage do Azure</span><span class="sxs-lookup"><span data-stu-id="7eef5-133">Enable logging with Azure Storage</span></span>
    
<span data-ttu-id="7eef5-134">Selecione toouse Storage do Azure toostore Olá registos **arquivar a conta de armazenamento tooa**, selecione os dias de retenção e, em **CoreAnalytics** em **registo**.</span><span class="sxs-lookup"><span data-stu-id="7eef5-134">toouse Azure Storage toostore hello logs, select **Archive tooa storage account**, select retention days, and click **CoreAnalytics** under **Log**.</span></span>

![Portal – registos de diagnóstico](./media/cdn-diagnostics-log/04_Diagnostics-logs-storage.png)

<span data-ttu-id="7eef5-136">*Figura 2 - registo com o Storage do Azure*</span><span class="sxs-lookup"><span data-stu-id="7eef5-136">*Figure 2 - Logging with Azure Storage*</span></span>

### <a name="logging-with-oms-log-analytics"></a><span data-ttu-id="7eef5-137">Registo de análise de registos do OMS</span><span class="sxs-lookup"><span data-stu-id="7eef5-137">Logging with OMS Log Analytics</span></span>

<span data-ttu-id="7eef5-138">toouse OMS registo toostore Olá pelos registos de análise, siga estes passos:</span><span class="sxs-lookup"><span data-stu-id="7eef5-138">toouse OMS Log Analytics toostore hello logs, follow these steps:</span></span>

1. <span data-ttu-id="7eef5-139">De Olá **registos de diagnóstico** painel em **monitorização**, selecione **enviar tooLog análise** do</span><span class="sxs-lookup"><span data-stu-id="7eef5-139">From hello **Diagnostics Logs** blade Under **Monitoring**, select **Send tooLog Analytics** from</span></span> 

    ![Portal – registos de diagnóstico](./media/cdn-diagnostics-log/05_Ready-to-Configure.png)    

2. <span data-ttu-id="7eef5-141">Configure o registo de análise de registos de Olá ao clicar em configurar.</span><span class="sxs-lookup"><span data-stu-id="7eef5-141">Configure hello Log Analytics logging by clicking on Configure.</span></span> <span data-ttu-id="7eef5-142">Isto leva-o diálogo tooa onde pode selecionar uma área de trabalho anterior ou crie um novo.</span><span class="sxs-lookup"><span data-stu-id="7eef5-142">This takes you tooa dialog where you can select a previous workspace or create a new one.</span></span>

    ![Portal – registos de diagnóstico](./media/cdn-diagnostics-log/06_Choose-workspace.png)

3. <span data-ttu-id="7eef5-144">Clique em **criar nova área de trabalho**.</span><span class="sxs-lookup"><span data-stu-id="7eef5-144">Click **Create New Workspace**.</span></span>

    ![Portal – registos de diagnóstico](./media/cdn-diagnostics-log/07_Create-new.png)

4. <span data-ttu-id="7eef5-146">Em seguida, tem de selecionar um novo nome de área de trabalho, a subscrição existente, a grupo de recursos (novo ou existente), a localização e o escalão de preço.</span><span class="sxs-lookup"><span data-stu-id="7eef5-146">Next you must select a new workspace name, existing subscription, resource group (new or existing), location, and pricing tier.</span></span> <span data-ttu-id="7eef5-147">Tem de opção de Olá de afixação este dashboard de tooyour de configuração.</span><span class="sxs-lookup"><span data-stu-id="7eef5-147">You have hello option of pinning this configuration tooyour dashboard.</span></span> <span data-ttu-id="7eef5-148">Clique em OK toocomplete Olá configuração.</span><span class="sxs-lookup"><span data-stu-id="7eef5-148">Click OK toocomplete hello configuration.</span></span>

    <span data-ttu-id="7eef5-149">Em seguida, deverá ver a sua área de trabalho com os nomes de grupo do OMS área de trabalho e recursos.</span><span class="sxs-lookup"><span data-stu-id="7eef5-149">Next you should see your workspace with your OMS Workspace and Resource group names.</span></span> <span data-ttu-id="7eef5-150">Os nomes têm de ser exclusivos e só podem utilizar letras, números e hífenes.</span><span class="sxs-lookup"><span data-stu-id="7eef5-150">Names must be unique and can only use letters, numbers, and hyphens.</span></span> <span data-ttu-id="7eef5-151">Não são permitidos espaços e carateres de sublinhado.</span><span class="sxs-lookup"><span data-stu-id="7eef5-151">Spaces and underscores are not allowed.</span></span> 

    ![Portal – registos de diagnóstico](./media/cdn-diagnostics-log/08_Workspace-resource.png)

5. <span data-ttu-id="7eef5-153">Junto a obter uma mensagem curta indicar que a sua área de trabalho foi criada e são devolvidos tooyour ecrã de configuração de registo.</span><span class="sxs-lookup"><span data-stu-id="7eef5-153">You next get a short message saying that your workspace has been created and you are returned tooyour logging configuration screen.</span></span> <span data-ttu-id="7eef5-154">Pode confirmar o nome de Olá da sua área de trabalho de análise de registos.</span><span class="sxs-lookup"><span data-stu-id="7eef5-154">You can confirm hello name of your Log Analytics workspace.</span></span>

    ![Portal – registos de diagnóstico](./media/cdn-diagnostics-log/09_Return-to-logging.png)

    <span data-ttu-id="7eef5-156">Assim que tiver configurado a configuração de análise de registos de Olá, certifique-se de que Olá CoreAnalytics caixa para o registo de CDN também de verificação.</span><span class="sxs-lookup"><span data-stu-id="7eef5-156">Once you have set up hello Log Analytics configuration, make sure you also check hello CoreAnalytics box for CDN logging.</span></span>

6. <span data-ttu-id="7eef5-157">Se tudo está tooyour liking, clique em Olá **guardar** botão na Olá parte superior da caixa de diálogo de configuração de Olá.</span><span class="sxs-lookup"><span data-stu-id="7eef5-157">If everything is tooyour liking, click hello **Save** button at hello top of hello configuration dialog.</span></span>

    ![Portal – registos de diagnóstico](./media/cdn-diagnostics-log/10_Save-me.png)

    <span data-ttu-id="7eef5-159">Olá **guardar** botão já não está ativa e esse Olá no/DESATIVAR botão está ON, mas blue em vez de roxa.</span><span class="sxs-lookup"><span data-stu-id="7eef5-159">hello **Save** button is no longer active and that hello ON/OFF button is now ON, but blue instead of purple.</span></span>

7. <span data-ttu-id="7eef5-160">Se quiser toosee a nova área de trabalho do OMS, aceda tooyour portal do Azure Dashboard, clique no nome de Olá da sua área de trabalho de análise de registos.</span><span class="sxs-lookup"><span data-stu-id="7eef5-160">If you want toosee your new OMS workspace, go tooyour Azure portal Dashboard, click hello name of your Log Analytics workspace.</span></span> <span data-ttu-id="7eef5-161">Em seguida, verá a área de trabalho (Certifique-se de que a área de trabalho OMS é realçada Olá esquerda).</span><span class="sxs-lookup"><span data-stu-id="7eef5-161">Next you will see your workspace (make sure that OMS Workspace is highlighted on hello left).</span></span> <span data-ttu-id="7eef5-162">Clique em toosee de mosaico do Portal do OMS Olá sua área de trabalho no repositório do Olá OMS.</span><span class="sxs-lookup"><span data-stu-id="7eef5-162">Click on hello OMS Portal tile toosee your workspace in hello OMS repository.</span></span> 

    ![Portal – registos de diagnóstico](./media/cdn-diagnostics-log/11_OMS-dashboard.png) 

    <span data-ttu-id="7eef5-164">O repositório do OMS está agora pronto toolog dados.</span><span class="sxs-lookup"><span data-stu-id="7eef5-164">Your OMS repository is now ready toolog data.</span></span> <span data-ttu-id="7eef5-165">Na ordem tooconsume esses dados, tem de utilizar um [OMS solução](#consuming-oms-log-analytics-data), abrangidas neste artigo.</span><span class="sxs-lookup"><span data-stu-id="7eef5-165">In order tooconsume that data, you must use an [OMS Solution](#consuming-oms-log-analytics-data), covered later in this article.</span></span>

<span data-ttu-id="7eef5-166">Para mais informações sobre os atrasos de dados de registo, visite [aqui](#log-data-delays).</span><span class="sxs-lookup"><span data-stu-id="7eef5-166">For more information about log data delays, go [here](#log-data-delays).</span></span>

## <a name="enable-logging-with-powershell"></a><span data-ttu-id="7eef5-167">Ativar o registo com o PowerShell</span><span class="sxs-lookup"><span data-stu-id="7eef5-167">Enable logging with PowerShell</span></span>

<span data-ttu-id="7eef5-168">Segue-se um exemplo de como tooenable e obter os registos de diagnóstico através de Olá Cmdlets do PowerShell do Azure.</span><span class="sxs-lookup"><span data-stu-id="7eef5-168">Below is an example on how tooenable and get Diagnostic Logs via hello Azure PowerShell Cmdlets.</span></span>

###<a name="enabling-diagnostic-logs-in-a-storage-account"></a><span data-ttu-id="7eef5-169">Ativar o diagnóstico inicia sessão numa conta do Storage</span><span class="sxs-lookup"><span data-stu-id="7eef5-169">Enabling Diagnostic Logs in a Storage Account</span></span>

<span data-ttu-id="7eef5-170">Primeiro início de sessão e selecionar uma subscrição:</span><span class="sxs-lookup"><span data-stu-id="7eef5-170">First log in and select a subscription:</span></span>

    Login-AzureRmAccount 

    Select-AzureSubscription -SubscriptionId 


<span data-ttu-id="7eef5-171">tooEnable registos de diagnóstico numa conta do Storage, utilize este comando:</span><span class="sxs-lookup"><span data-stu-id="7eef5-171">tooEnable Diagnostic Logs in a Storage Account, use this command:</span></span>

```powershell
    Set-AzureRmDiagnosticSetting -ResourceId "/subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.Cdn/profiles/{profileName}/endpoints/{endpointName}" -StorageAccountId "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ClassicStorage/storageAccounts/{storageAccountName}" -Enabled $true -Categories CoreAnalytics
```
<span data-ttu-id="7eef5-172">tooEnable registos de diagnóstico na área de trabalho do OMS, utilize este comando:</span><span class="sxs-lookup"><span data-stu-id="7eef5-172">tooEnable Diagnostics Logs in an OMS workspace, use this command:</span></span>

```powershell
    Set-AzureRmDiagnosticSetting -ResourceId "/subscriptions/`{subscriptionId}<subscriptionId>
    .<subscriptionName>" -WorkspaceId "/subscriptions/<workspaceId>.<workspaceName>" -Enabled $true -Categories CoreAnalytics 
```



## <a name="consuming-diagnostics-logs-from-azure-storage"></a><span data-ttu-id="7eef5-173">Consumir os registos de diagnóstico do armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="7eef5-173">Consuming diagnostics logs from Azure Storage</span></span>
<span data-ttu-id="7eef5-174">Esta secção descreve o esquema de Olá da análise de núcleo CDN Olá, a forma como estas estão organizados dentro de uma conta de armazenamento do Azure e fornece Olá de toodownload de código de exemplo regista no ficheiro CSV de tooa.</span><span class="sxs-lookup"><span data-stu-id="7eef5-174">This section describes hello schema of hello CDN core analytics, how these are organized inside of an Azure Storage Account and provides sample code toodownload hello logs in tooa CSV file.</span></span>

### <a name="using-microsoft-azure-storage-explorer"></a><span data-ttu-id="7eef5-175">Utilizar o Explorador de armazenamento do Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="7eef5-175">Using Microsoft Azure Storage Explorer</span></span>
<span data-ttu-id="7eef5-176">Antes de poder aceder a dados de análise de núcleo de Olá Olá conta do Storage do Azure, primeiro precisa de uma ferramenta tooaccess Olá do conteúdo numa conta do storage.</span><span class="sxs-lookup"><span data-stu-id="7eef5-176">Before you can access hello core analytics data from hello Azure Storage Account, you first need a tool tooaccess hello contents in a storage account.</span></span> <span data-ttu-id="7eef5-177">Apesar de existirem várias ferramentas disponíveis no mercado Olá, Olá que recomendamos é Olá Explorador de armazenamento do Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="7eef5-177">While there are several tools available in hello market, hello one that we recommend is hello Microsoft Azure Storage Explorer.</span></span> <span data-ttu-id="7eef5-178">Pode transferir a ferramenta de Olá do [aqui](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="7eef5-178">You can download hello tool from [here](http://storageexplorer.com/).</span></span> <span data-ttu-id="7eef5-179">Depois de transferir e instalar software Olá, configurá-lo toouse Olá a mesma conta do Storage do Azure que foi configurado como um destino toohello registos de diagnóstico da CDN.</span><span class="sxs-lookup"><span data-stu-id="7eef5-179">After downloading and installing hello software, configure it toouse hello same Azure Storage Account that was configured as a destination toohello CDN Diagnostics Logs.</span></span>

1.  <span data-ttu-id="7eef5-180">Abra **Explorador de armazenamento do Microsoft Azure**</span><span class="sxs-lookup"><span data-stu-id="7eef5-180">Open **Microsoft Azure Storage Explorer**</span></span>
2.  <span data-ttu-id="7eef5-181">Localize a conta de armazenamento Olá</span><span class="sxs-lookup"><span data-stu-id="7eef5-181">Locate hello storage account</span></span>
3.  <span data-ttu-id="7eef5-182">Aceda toohello **"Contentores de BLOBs"** nós sob este armazenamento conta e expanda o nó de Olá</span><span class="sxs-lookup"><span data-stu-id="7eef5-182">Go toohello **“Blob Containers”** node under this storage account and expand hello node</span></span>
4.  <span data-ttu-id="7eef5-183">Com o nome de contentor de Olá selecione **"insights-registos-coreanalytics"** e faça duplo clique</span><span class="sxs-lookup"><span data-stu-id="7eef5-183">Select hello container named **“insights-logs-coreanalytics”** and double-click it</span></span>
5.  <span data-ttu-id="7eef5-184">Resulta Mostrar cópias de segurança no Olá painel direita começadas Olá primeiro nível, que se parece com **"resourceId ="**.</span><span class="sxs-lookup"><span data-stu-id="7eef5-184">Results show up on hello right-hand pane starting with hello first level, which looks like **“resourceId=”**.</span></span> <span data-ttu-id="7eef5-185">Continuar a clicar em todas as forma de Olá até ver ficheiros de Olá **PT1H.json**.</span><span class="sxs-lookup"><span data-stu-id="7eef5-185">Continue clicking all hello way until you see hello file **PT1H.json**.</span></span> <span data-ttu-id="7eef5-186">Consulte Olá nota para obter explicações caminho Olá a seguir.</span><span class="sxs-lookup"><span data-stu-id="7eef5-186">See hello following note for explanation of hello path.</span></span>
6.  <span data-ttu-id="7eef5-187">Cada blob **PT1H.json** representa hello registos de análise para uma hora para um ponto final de CDN específico ou o domínio personalizado.</span><span class="sxs-lookup"><span data-stu-id="7eef5-187">Each blob **PT1H.json** represents hello analytics logs for one hour for a specific CDN endpoint or its custom domain.</span></span>
7.  <span data-ttu-id="7eef5-188">esquema de Olá do conteúdo Olá deste ficheiro JSON está descrita na secção Olá esquema Olá registos de análise de núcleo</span><span class="sxs-lookup"><span data-stu-id="7eef5-188">hello schema of hello contents of this JSON file is described in hello section Schema of hello Core Analytics Logs</span></span>


> [!NOTE]
> <span data-ttu-id="7eef5-189">**Formato de caminho do blob**</span><span class="sxs-lookup"><span data-stu-id="7eef5-189">**Blob path format**</span></span>
> 
> <span data-ttu-id="7eef5-190">Registos de análise do Core são gerados a cada hora.</span><span class="sxs-lookup"><span data-stu-id="7eef5-190">Core Analytics logs are generated every hour.</span></span> <span data-ttu-id="7eef5-191">Todos os dados para uma hora são recolhidos e armazenados no interior de um único Blob do Azure como um payload JSON.</span><span class="sxs-lookup"><span data-stu-id="7eef5-191">All data for an hour are collected and stored inside a single Azure Blob as a JSON payload.</span></span> <span data-ttu-id="7eef5-192">Olá caminho toothis Blob do Azure é apresentado como se houver uma estrutura hierárquica.</span><span class="sxs-lookup"><span data-stu-id="7eef5-192">hello path toothis Azure Blob appears as if there is a hierarchical structure.</span></span> <span data-ttu-id="7eef5-193">Isto acontece porque a ferramenta de Explorador de armazenamento Olá interpreta '/' como um separador de diretório e mostra hierarquia Olá para sua comodidade.</span><span class="sxs-lookup"><span data-stu-id="7eef5-193">This is because hello Storage explorer tool interprets '/' as a directory separator and shows hello hierarchy for convenience.</span></span> <span data-ttu-id="7eef5-194">Na realidade, caminho todo Olá apenas representa o nome do blob Olá.</span><span class="sxs-lookup"><span data-stu-id="7eef5-194">Actually, hello whole path just represents hello blob name.</span></span> <span data-ttu-id="7eef5-195">Este nome de blob Olá segue Olá seguinte convenção de nomenclatura</span><span class="sxs-lookup"><span data-stu-id="7eef5-195">This name of hello blob follows hello following naming convention</span></span> 
    
    resourceId=/SUBSCRIPTIONS/{Subscription Id}/RESOURCEGROUPS/{Resource Group Name}/PROVIDERS/MICROSOFT.CDN/PROFILES/{Profile Name}/ENDPOINTS/{Endpoint Name}/ y={Year}/m={Month}/d={Day}/h={Hour}/m={Minutes}/PT1H.json

<span data-ttu-id="7eef5-196">**Descrição de campos:**</span><span class="sxs-lookup"><span data-stu-id="7eef5-196">**Description of fields:**</span></span>

|<span data-ttu-id="7eef5-197">valor</span><span class="sxs-lookup"><span data-stu-id="7eef5-197">value</span></span>|<span data-ttu-id="7eef5-198">descrição</span><span class="sxs-lookup"><span data-stu-id="7eef5-198">description</span></span>|
|-------|---------|
|<span data-ttu-id="7eef5-199">ID da subscrição</span><span class="sxs-lookup"><span data-stu-id="7eef5-199">Subscription ID</span></span>    |<span data-ttu-id="7eef5-200">ID do Olá subscrição do Azure.</span><span class="sxs-lookup"><span data-stu-id="7eef5-200">ID of hello Azure Subscription.</span></span> <span data-ttu-id="7eef5-201">Trata-se no formato de Guid Olá.</span><span class="sxs-lookup"><span data-stu-id="7eef5-201">This is in hello Guid format.</span></span>|
|<span data-ttu-id="7eef5-202">Recurso</span><span class="sxs-lookup"><span data-stu-id="7eef5-202">Resource</span></span> |<span data-ttu-id="7eef5-203">Nome do grupo de recursos CDN de Olá grupo toowhich Olá recurso pertence.</span><span class="sxs-lookup"><span data-stu-id="7eef5-203">Group Name   Name of hello resource group toowhich hello CDN resources belong.</span></span>|
|<span data-ttu-id="7eef5-204">Nome do perfil</span><span class="sxs-lookup"><span data-stu-id="7eef5-204">Profile Name</span></span> |<span data-ttu-id="7eef5-205">Nome do Olá perfil da CDN</span><span class="sxs-lookup"><span data-stu-id="7eef5-205">Name of hello CDN Profile</span></span>|
|<span data-ttu-id="7eef5-206">Nome do ponto final</span><span class="sxs-lookup"><span data-stu-id="7eef5-206">Endpoint Name</span></span> |<span data-ttu-id="7eef5-207">Nome do Olá ponto final de CDN</span><span class="sxs-lookup"><span data-stu-id="7eef5-207">Name of hello CDN Endpoint</span></span>|
|<span data-ttu-id="7eef5-208">ano</span><span class="sxs-lookup"><span data-stu-id="7eef5-208">Year</span></span>|  <span data-ttu-id="7eef5-209">representação de 4 dígitos do ano Olá 2017 por exemplo,</span><span class="sxs-lookup"><span data-stu-id="7eef5-209">4-digit representation of hello year for example, 2017</span></span>|
|<span data-ttu-id="7eef5-210">Mês</span><span class="sxs-lookup"><span data-stu-id="7eef5-210">Month</span></span>| <span data-ttu-id="7eef5-211">representação de 2-dígitos do número de meses Olá.</span><span class="sxs-lookup"><span data-stu-id="7eef5-211">2-digit representation of hello month number.</span></span> <span data-ttu-id="7eef5-212">01 = Janeiro... 12 = Dezembro</span><span class="sxs-lookup"><span data-stu-id="7eef5-212">01=January ... 12=December</span></span>|
|<span data-ttu-id="7eef5-213">Dia</span><span class="sxs-lookup"><span data-stu-id="7eef5-213">Day</span></span>|   <span data-ttu-id="7eef5-214">representação de dígitos 2 do dia de Olá do mês de Olá</span><span class="sxs-lookup"><span data-stu-id="7eef5-214">2 digit representation of hello day of hello month</span></span>|
|<span data-ttu-id="7eef5-215">PT1H.JSON</span><span class="sxs-lookup"><span data-stu-id="7eef5-215">PT1H.json</span></span>| <span data-ttu-id="7eef5-216">Armazenar dados de análise Olá real do ficheiro JSON</span><span class="sxs-lookup"><span data-stu-id="7eef5-216">Actual JSON file where hello analytics data is stored</span></span>|

### <a name="exporting-hello-core-analytics-data-tooa-csv-file"></a><span data-ttu-id="7eef5-217">Exportar dados de análise de núcleo de Olá tooa ficheiro CSV</span><span class="sxs-lookup"><span data-stu-id="7eef5-217">Exporting hello Core Analytics Data tooa CSV File</span></span>

<span data-ttu-id="7eef5-218">toomake it tooaccess fácil Olá análise de núcleo, iremos fornecer um código de exemplo para uma ferramenta que permite a transferência de ficheiros de JSON de Olá para um formato de ficheiro flat separados por vírgulas, que pode ser utilizado tooeasily criar gráficos ou outras agregações.</span><span class="sxs-lookup"><span data-stu-id="7eef5-218">toomake it easy tooaccess hello Core Analytics, we provide a sample code for a tool, which allows downloading hello JSON files into a flat comma-separated file format, which can be used tooeasily create charts or other aggregations.</span></span>

<span data-ttu-id="7eef5-219">Eis como pode utilizar a ferramenta de Olá:</span><span class="sxs-lookup"><span data-stu-id="7eef5-219">Here is how you can use hello tool:</span></span>

1.  <span data-ttu-id="7eef5-220">Visite Olá github ligação: [https://github.com/Azure-Samples/azure-cdn-samples/tree/master/CoreAnalytics-ExportToCsv](https://github.com/Azure-Samples/azure-cdn-samples/tree/master/CoreAnalytics-ExportToCsv )</span><span class="sxs-lookup"><span data-stu-id="7eef5-220">Visit hello github link: [https://github.com/Azure-Samples/azure-cdn-samples/tree/master/CoreAnalytics-ExportToCsv ](https://github.com/Azure-Samples/azure-cdn-samples/tree/master/CoreAnalytics-ExportToCsv )</span></span>
2.  <span data-ttu-id="7eef5-221">Transferir o código de Olá</span><span class="sxs-lookup"><span data-stu-id="7eef5-221">Download hello code</span></span>
3.  <span data-ttu-id="7eef5-222">Siga as instruções toocompile e configurar</span><span class="sxs-lookup"><span data-stu-id="7eef5-222">Follow instructions toocompile and configure</span></span>
4.  <span data-ttu-id="7eef5-223">Execute a ferramenta de Olá</span><span class="sxs-lookup"><span data-stu-id="7eef5-223">Run hello tool</span></span>
5.  <span data-ttu-id="7eef5-224">Um ficheiro CSV resultante mostra os dados de análise de Olá numa hierarquia simples simple.</span><span class="sxs-lookup"><span data-stu-id="7eef5-224">Resulting CSV file shows hello analytics data in a simple flat hierarchy.</span></span>

## <a name="consuming-diagnostics-logs-from-an-oms-log-analytics-repository"></a><span data-ttu-id="7eef5-225">Consumir os registos de diagnóstico de um repositório de análise de registos do OMS</span><span class="sxs-lookup"><span data-stu-id="7eef5-225">Consuming diagnostics logs from an OMS Log Analytics repository</span></span>
<span data-ttu-id="7eef5-226">Análise de registos é um serviço no Operations Management Suite (OMS) que monitoriza o toomaintain de ambientes de nuvem e no local, disponibilidade e o desempenho.</span><span class="sxs-lookup"><span data-stu-id="7eef5-226">Log Analytics is a service in Operations Management Suite (OMS) that monitors your cloud and on-premises environments toomaintain their availability and performance.</span></span> <span data-ttu-id="7eef5-227">Recolhe dados gerados pelos recursos nos seus ambientes de nuvem e no local e de outro análise de tooprovide ferramentas monitorização em várias origens.</span><span class="sxs-lookup"><span data-stu-id="7eef5-227">It collects data generated by resources in your cloud and on-premises environments and from other monitoring tools tooprovide analysis across multiple sources.</span></span> 

<span data-ttu-id="7eef5-228">Análise de registos toouse, tem de [ativar o registo](#enable-logging-with-azure-storage) repositório de análise de registos do Azure OMS toohello, que é abordado anteriores no artigo.</span><span class="sxs-lookup"><span data-stu-id="7eef5-228">toouse Log Analytics, you must [enable logging](#enable-logging-with-azure-storage) toohello Azure OMS Log Analytics repository, which is discussed earlier in this article.</span></span>

### <a name="using-hello-oms-repository"></a><span data-ttu-id="7eef5-229">Utilizar Olá repositório do OMS</span><span class="sxs-lookup"><span data-stu-id="7eef5-229">Using hello OMS Repository</span></span>

 <span data-ttu-id="7eef5-230">Olá diagrama a seguir mostra a arquitetura de Olá de entradas de Olá e saídas do repositório de Olá:</span><span class="sxs-lookup"><span data-stu-id="7eef5-230">hello following diagram shows hello architecture of hello inputs and outputs of hello repository:</span></span>

![Repositório de análise de registo do OMS](./media/cdn-diagnostics-log/12_Repo-overview.png)

<span data-ttu-id="7eef5-232">*Figura 3 - repositório de análise do registo*</span><span class="sxs-lookup"><span data-stu-id="7eef5-232">*Figure 3 - Log Analytics Repository*</span></span>

<span data-ttu-id="7eef5-233">Pode apresentar dados Olá numa variedade de formas utilizando soluções de gestão.</span><span class="sxs-lookup"><span data-stu-id="7eef5-233">You can display hello data in a variety of ways by using Management Solutions.</span></span> <span data-ttu-id="7eef5-234">Pode obter as soluções de gestão de Olá [Azure Marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/category/monitoring-management?page=1&subcategories=management-solutions).</span><span class="sxs-lookup"><span data-stu-id="7eef5-234">You can obtain Management Solutions from hello [Azure Marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/category/monitoring-management?page=1&subcategories=management-solutions).</span></span>

<span data-ttu-id="7eef5-235">Pode instalar as soluções de gestão do Azure marketplace, clicando em Olá **obtê-lo agora** ligação na parte inferior de Olá de cada solução.</span><span class="sxs-lookup"><span data-stu-id="7eef5-235">You can install management solutions from Azure marketplace by clicking hello **Get it now** link at hello bottom of each solution.</span></span>

### <a name="adding-an-oms-cdn-management-solution"></a><span data-ttu-id="7eef5-236">Adicionar uma solução de gestão da CDN do OMS</span><span class="sxs-lookup"><span data-stu-id="7eef5-236">Adding an OMS CDN Management Solution</span></span>

<span data-ttu-id="7eef5-237">Siga estes passos tooadd uma solução de gestão:</span><span class="sxs-lookup"><span data-stu-id="7eef5-237">Follow these steps tooadd a Management Solution:</span></span>

1.   <span data-ttu-id="7eef5-238">Se ainda não o fez, inicie sessão toohello portal do Azure através da sua subscrição do Azure e aceda tooyour Dashboard.</span><span class="sxs-lookup"><span data-stu-id="7eef5-238">If you haven't already done so, sign in toohello Azure portal using your Azure subscription and go tooyour Dashboard.</span></span>
    <span data-ttu-id="7eef5-239">![Dashboard do Azure](./media/cdn-diagnostics-log/13_Azure-dashboard.png)</span><span class="sxs-lookup"><span data-stu-id="7eef5-239">![Azure Dashboard](./media/cdn-diagnostics-log/13_Azure-dashboard.png)</span></span>

2. <span data-ttu-id="7eef5-240">No Olá **novo** painel em **Marketplace**, selecione **monitorização + gestão**.</span><span class="sxs-lookup"><span data-stu-id="7eef5-240">In hello **New** blade under **Marketplace**, select **Monitoring + management**.</span></span>

    ![Marketplace](./media/cdn-diagnostics-log/14_Marketplace.png)

3. <span data-ttu-id="7eef5-242">No Olá **monitorização + gestão** painel, clique em **ver todos os**.</span><span class="sxs-lookup"><span data-stu-id="7eef5-242">In hello **Monitoring + management** blade, click **See all**.</span></span>

    ![Ver tudo](./media/cdn-diagnostics-log/15_See-all.png)

4.  <span data-ttu-id="7eef5-244">Procure CDN na caixa de pesquisa de Olá.</span><span class="sxs-lookup"><span data-stu-id="7eef5-244">Search for CDN in hello search box.</span></span>

    ![Ver tudo](./media/cdn-diagnostics-log/16_Search-for.png)

5.  <span data-ttu-id="7eef5-246">Selecione **análise de núcleo da CDN do Azure**.</span><span class="sxs-lookup"><span data-stu-id="7eef5-246">Select **Azure CDN Core Analytics**.</span></span> 

    ![Ver tudo](./media/cdn-diagnostics-log/17_Core-analytics.png)

6.  <span data-ttu-id="7eef5-248">Depois de clicar em **criar**, será pedido toocreate uma área de trabalho do OMS nova ou utilize uma já existente.</span><span class="sxs-lookup"><span data-stu-id="7eef5-248">After clicking **Create**, you will be asked toocreate a new OMS workspace or use an existing one.</span></span> 

    ![Ver tudo](./media/cdn-diagnostics-log/18_Adding-solution.png)

7.  <span data-ttu-id="7eef5-250">Selecione a área de trabalho Olá criado antes de.</span><span class="sxs-lookup"><span data-stu-id="7eef5-250">Select hello workspace you created before.</span></span> <span data-ttu-id="7eef5-251">Em seguida, terá de tooadd uma conta de automatização.</span><span class="sxs-lookup"><span data-stu-id="7eef5-251">You then need tooadd an automation account.</span></span>

    ![Ver tudo](./media/cdn-diagnostics-log/19_Add-automation.png)

8. <span data-ttu-id="7eef5-253">Olá ecrã seguinte mostra formulário de conta de automatização de Olá, terá de preencher enviados.</span><span class="sxs-lookup"><span data-stu-id="7eef5-253">hello following screen shows hello automation account form you must fill out.</span></span> 

    ![Ver tudo](./media/cdn-diagnostics-log/20_Automation.png)

9. <span data-ttu-id="7eef5-255">Assim que tiver criado a conta de automatização Olá, está pronto tooadd sua solução.</span><span class="sxs-lookup"><span data-stu-id="7eef5-255">Once you have created hello automation account, you are ready tooadd your solution.</span></span> <span data-ttu-id="7eef5-256">Clique em Olá **criar** botão.</span><span class="sxs-lookup"><span data-stu-id="7eef5-256">Click hello **Create** button.</span></span>

    ![Ver tudo](./media/cdn-diagnostics-log/21_Ready.png)

10. <span data-ttu-id="7eef5-258">A solução foi agora adicionada tooyour área de trabalho.</span><span class="sxs-lookup"><span data-stu-id="7eef5-258">Your solution has now been added tooyour workspace.</span></span> <span data-ttu-id="7eef5-259">Volte tooyour Dashboard de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="7eef5-259">Go back tooyour Azure portal Dashboard.</span></span>

    ![Ver tudo](./media/cdn-diagnostics-log/22_Dashboard.png)

    <span data-ttu-id="7eef5-261">Clique em área de trabalho do Log Analytics Olá criou toogo tooyour área.</span><span class="sxs-lookup"><span data-stu-id="7eef5-261">Click hello Log Analytics workspace you created toogo tooyour workspace.</span></span> 

11. <span data-ttu-id="7eef5-262">Clique em Olá **Portal do OMS** mosaico toosee solução nova no portal do OMS Olá.</span><span class="sxs-lookup"><span data-stu-id="7eef5-262">Click hello **OMS Portal** tile toosee your new solution in hello OMS portal.</span></span>

    ![Ver tudo](./media/cdn-diagnostics-log/23_workspace.png)

12. <span data-ttu-id="7eef5-264">O portal do OMS deve agora ter o seguinte aspeto Olá ecrã a seguir:</span><span class="sxs-lookup"><span data-stu-id="7eef5-264">Your OMS portal should now look like hello following screen:</span></span>

    ![Ver tudo](./media/cdn-diagnostics-log/24_OMS-solution.png)

    <span data-ttu-id="7eef5-266">Clique das Olá mosaicos toosee várias vistas sobre os seus dados.</span><span class="sxs-lookup"><span data-stu-id="7eef5-266">Click one of hello tiles toosee several views into your data.</span></span>

    ![Ver tudo](./media/cdn-diagnostics-log/25_Interior-view.png)

    <span data-ttu-id="7eef5-268">Pode se deslocar para a esquerda ou direita toosee ainda mais os mosaicos que representa vistas individuais em dados de Olá.</span><span class="sxs-lookup"><span data-stu-id="7eef5-268">You can scroll left or right toosee further tiles representing individual views into hello data.</span></span> 

    <span data-ttu-id="7eef5-269">Clicar dos mosaicos Olá dá-lhe obter mais detalhes sobre os dados.</span><span class="sxs-lookup"><span data-stu-id="7eef5-269">Clicking one of hello tiles gives you more details about your data.</span></span>

     ![Ver tudo](./media/cdn-diagnostics-log/26_Further-detail.png)

### <a name="offers-and-pricing-tiers"></a><span data-ttu-id="7eef5-271">Ofertas e escalões de preços</span><span class="sxs-lookup"><span data-stu-id="7eef5-271">Offers and pricing tiers</span></span>

<span data-ttu-id="7eef5-272">Pode ver ofertas e escalões de preços para soluções de gestão do OMS [aqui](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-add-solutions#offers-and-pricing-tiers).</span><span class="sxs-lookup"><span data-stu-id="7eef5-272">You can see offers and pricing tiers for OMS management solutions [here](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-add-solutions#offers-and-pricing-tiers).</span></span>

### <a name="customizing-views"></a><span data-ttu-id="7eef5-273">Personalizar vistas</span><span class="sxs-lookup"><span data-stu-id="7eef5-273">Customizing views</span></span>

<span data-ttu-id="7eef5-274">Pode personalizar vista Olá sobre os seus dados através da utilização de Olá **estruturador de vistas**.</span><span class="sxs-lookup"><span data-stu-id="7eef5-274">You can customize hello view into your data by using hello **View Designer**.</span></span> <span data-ttu-id="7eef5-275">Aceda a área de trabalho do tooyour OMS e começar a estruturar clicando Olá **estruturador de vistas** mosaico.</span><span class="sxs-lookup"><span data-stu-id="7eef5-275">Go tooyour OMS workspace and begin designing by clicking hello **View Designer** tile.</span></span>

![Estruturador de Vista](./media/cdn-diagnostics-log/27_Designer.png)

<span data-ttu-id="7eef5-277">Pode arrastar e largar tipos de gráficos da esquerda Olá e preencha os detalhes de dados de Olá que pretende tooanalyze no Olá à esquerda.</span><span class="sxs-lookup"><span data-stu-id="7eef5-277">You can drag and drop types of charts from hello left and fill in hello data details you want tooanalyze on hello left.</span></span>

![Estruturador de Vista](./media/cdn-diagnostics-log/28_Designer.png)

    
## <a name="log-data-delays"></a><span data-ttu-id="7eef5-279">Atrasos de dados de registo</span><span class="sxs-lookup"><span data-stu-id="7eef5-279">Log data delays</span></span>

<span data-ttu-id="7eef5-280">Atrasos de dados de registo da Verizon</span><span class="sxs-lookup"><span data-stu-id="7eef5-280">Verizon log data delays</span></span> | <span data-ttu-id="7eef5-281">Atrasos de dados de registo Akamai</span><span class="sxs-lookup"><span data-stu-id="7eef5-281">Akamai log data delays</span></span>
--- | ---
<span data-ttu-id="7eef5-282">Dados de registo da Verizon estão atrasados 1 hora em demorar too2 horas toostart apresentação após a conclusão da propagação de ponto final.</span><span class="sxs-lookup"><span data-stu-id="7eef5-282">Verizon log data is 1 hour delayed, and take up too2 hours toostart appearing after endpoint propagation completion.</span></span> | <span data-ttu-id="7eef5-283">Dados de registo da Akamai é de 24 horas atrasadas e ocupa too2 horas toostart apresentação se tiver sido criado há mais de 24 horas.</span><span class="sxs-lookup"><span data-stu-id="7eef5-283">Akamai log data is 24 hours delayed, and takes up too2 hours toostart appearing if it was created more than 24 hours ago.</span></span> <span data-ttu-id="7eef5-284">Se tiver sido recentemente criado, pode demorar até too25 horas para Olá registos toostart volte a aparecer.</span><span class="sxs-lookup"><span data-stu-id="7eef5-284">If it was recently created, it can take up too25 hours for hello logs toostart appearing.</span></span>

## <a name="diagnostic-log-types-for-cdn-core-analytics"></a><span data-ttu-id="7eef5-285">Tipos de registo de diagnóstico para análise de núcleo de CDN</span><span class="sxs-lookup"><span data-stu-id="7eef5-285">Diagnostic log types for CDN Core Analytics</span></span>

<span data-ttu-id="7eef5-286">Estamos atualmente oferecem apenas os registos de análise de núcleo, que contêm as métricas que mostra as estatísticas de resposta HTTP e estatísticas de saída, conforme visto a partir de Olá CDN POPs/contornos.</span><span class="sxs-lookup"><span data-stu-id="7eef5-286">We currently offer only Core Analytics logs, which contain metrics showing HTTP response statistics and egress statistics as seen from hello CDN POPs/edges.</span></span>

### <a name="core-analytics-metrics-details"></a><span data-ttu-id="7eef5-287">Detalhes de métricas de análise de núcleo</span><span class="sxs-lookup"><span data-stu-id="7eef5-287">Core Analytics Metrics Details</span></span>
<span data-ttu-id="7eef5-288">Olá, a tabela seguinte mostra uma lista das métricas disponíveis no Olá que os registos de análise de núcleo.</span><span class="sxs-lookup"><span data-stu-id="7eef5-288">hello following table shows a list of metrics available in hello Core Analytics logs.</span></span> <span data-ttu-id="7eef5-289">Nem todas as métricas estão disponíveis de todos os fornecedores, apesar destas diferenças são mínimas.</span><span class="sxs-lookup"><span data-stu-id="7eef5-289">Not all metrics are available from all providers, although such differences are minimal.</span></span> <span data-ttu-id="7eef5-290">Olá, a tabela seguinte também mostra uma métrica de determinado estiver disponível a partir de um fornecedor.</span><span class="sxs-lookup"><span data-stu-id="7eef5-290">hello following table also shows if a given metric is available from a provider.</span></span> <span data-ttu-id="7eef5-291">Tenha em atenção que as métricas de Olá estão disponíveis para apenas esses pontos finais da CDN que tenham tráfego nos mesmos.</span><span class="sxs-lookup"><span data-stu-id="7eef5-291">Please note that hello metrics are available for only those CDN endpoints that have traffic on them.</span></span>


|<span data-ttu-id="7eef5-292">Métrica</span><span class="sxs-lookup"><span data-stu-id="7eef5-292">Metric</span></span>                     | <span data-ttu-id="7eef5-293">Descrição</span><span class="sxs-lookup"><span data-stu-id="7eef5-293">Description</span></span>   | <span data-ttu-id="7eef5-294">Verizon</span><span class="sxs-lookup"><span data-stu-id="7eef5-294">Verizon</span></span>  | <span data-ttu-id="7eef5-295">Akamai</span><span class="sxs-lookup"><span data-stu-id="7eef5-295">Akamai</span></span> 
|---------------------------|---------------|---|---|
| <span data-ttu-id="7eef5-296">RequestCountTotal</span><span class="sxs-lookup"><span data-stu-id="7eef5-296">RequestCountTotal</span></span>         |<span data-ttu-id="7eef5-297">Número total de pedidos de pedido durante este período</span><span class="sxs-lookup"><span data-stu-id="7eef5-297">Total number of request hits during this period</span></span>| <span data-ttu-id="7eef5-298">Sim</span><span class="sxs-lookup"><span data-stu-id="7eef5-298">Yes</span></span>  |<span data-ttu-id="7eef5-299">Sim</span><span class="sxs-lookup"><span data-stu-id="7eef5-299">Yes</span></span>   |
| <span data-ttu-id="7eef5-300">RequestCountHttpStatus2xx</span><span class="sxs-lookup"><span data-stu-id="7eef5-300">RequestCountHttpStatus2xx</span></span> |<span data-ttu-id="7eef5-301">Contagem de todos os pedidos que resultaram num código de HTTP 2xx (por exemplo, 200, 202)</span><span class="sxs-lookup"><span data-stu-id="7eef5-301">Count of all requests that resulted in a 2xx HTTP code (e.g. 200, 202)</span></span>              | <span data-ttu-id="7eef5-302">Sim</span><span class="sxs-lookup"><span data-stu-id="7eef5-302">Yes</span></span>  |<span data-ttu-id="7eef5-303">Sim</span><span class="sxs-lookup"><span data-stu-id="7eef5-303">Yes</span></span>   |
| <span data-ttu-id="7eef5-304">RequestCountHttpStatus3xx</span><span class="sxs-lookup"><span data-stu-id="7eef5-304">RequestCountHttpStatus3xx</span></span> | <span data-ttu-id="7eef5-305">Contagem de todos os pedidos que resultaram num código de HTTP 3xx (por exemplo, 300, 302)</span><span class="sxs-lookup"><span data-stu-id="7eef5-305">Count of all requests that resulted in a 3xx HTTP code (e.g. 300, 302)</span></span>              | <span data-ttu-id="7eef5-306">Sim</span><span class="sxs-lookup"><span data-stu-id="7eef5-306">Yes</span></span>  |<span data-ttu-id="7eef5-307">Sim</span><span class="sxs-lookup"><span data-stu-id="7eef5-307">Yes</span></span>   |
| <span data-ttu-id="7eef5-308">RequestCountHttpStatus4xx</span><span class="sxs-lookup"><span data-stu-id="7eef5-308">RequestCountHttpStatus4xx</span></span> |<span data-ttu-id="7eef5-309">Contagem de todos os pedidos que resultaram num código de HTTP 4xx (por exemplo, 400, 404)</span><span class="sxs-lookup"><span data-stu-id="7eef5-309">Count of all requests that resulted in a 4xx HTTP code (e.g. 400, 404)</span></span>               | <span data-ttu-id="7eef5-310">Sim</span><span class="sxs-lookup"><span data-stu-id="7eef5-310">Yes</span></span>   |<span data-ttu-id="7eef5-311">Sim</span><span class="sxs-lookup"><span data-stu-id="7eef5-311">Yes</span></span>   |
| <span data-ttu-id="7eef5-312">RequestCountHttpStatus5xx</span><span class="sxs-lookup"><span data-stu-id="7eef5-312">RequestCountHttpStatus5xx</span></span> | <span data-ttu-id="7eef5-313">Contagem de todos os pedidos que resultaram num código de HTTP 5xx (por exemplo, 500, 504)</span><span class="sxs-lookup"><span data-stu-id="7eef5-313">Count of all requests that resulted in a 5xx HTTP code (e.g. 500, 504)</span></span>              | <span data-ttu-id="7eef5-314">Sim</span><span class="sxs-lookup"><span data-stu-id="7eef5-314">Yes</span></span>  |<span data-ttu-id="7eef5-315">Sim</span><span class="sxs-lookup"><span data-stu-id="7eef5-315">Yes</span></span>   |
| <span data-ttu-id="7eef5-316">RequestCountHttpStatusOthers</span><span class="sxs-lookup"><span data-stu-id="7eef5-316">RequestCountHttpStatusOthers</span></span> |  <span data-ttu-id="7eef5-317">Contagem de todos os outros códigos HTTP (fora 2xx-5xx)</span><span class="sxs-lookup"><span data-stu-id="7eef5-317">Count of all other HTTP codes (outside of 2xx-5xx)</span></span> | <span data-ttu-id="7eef5-318">Sim</span><span class="sxs-lookup"><span data-stu-id="7eef5-318">Yes</span></span>  |<span data-ttu-id="7eef5-319">Sim</span><span class="sxs-lookup"><span data-stu-id="7eef5-319">Yes</span></span>   |
| <span data-ttu-id="7eef5-320">RequestCountHttpStatus200</span><span class="sxs-lookup"><span data-stu-id="7eef5-320">RequestCountHttpStatus200</span></span> | <span data-ttu-id="7eef5-321">Contagem de todos os pedidos que resultaram numa resposta de código HTTP 200</span><span class="sxs-lookup"><span data-stu-id="7eef5-321">Count of all requests that resulted in a 200 HTTP code response</span></span>              |<span data-ttu-id="7eef5-322">Não</span><span class="sxs-lookup"><span data-stu-id="7eef5-322">No</span></span>   |<span data-ttu-id="7eef5-323">Sim</span><span class="sxs-lookup"><span data-stu-id="7eef5-323">Yes</span></span>   |
| <span data-ttu-id="7eef5-324">RequestCountHttpStatus206</span><span class="sxs-lookup"><span data-stu-id="7eef5-324">RequestCountHttpStatus206</span></span> | <span data-ttu-id="7eef5-325">Contagem de todos os pedidos que resultaram numa resposta código 206 HTTP</span><span class="sxs-lookup"><span data-stu-id="7eef5-325">Count of all requests that resulted in a 206 HTTP code response</span></span>              |<span data-ttu-id="7eef5-326">Não</span><span class="sxs-lookup"><span data-stu-id="7eef5-326">No</span></span>   |<span data-ttu-id="7eef5-327">Sim</span><span class="sxs-lookup"><span data-stu-id="7eef5-327">Yes</span></span>   |
| <span data-ttu-id="7eef5-328">RequestCountHttpStatus302</span><span class="sxs-lookup"><span data-stu-id="7eef5-328">RequestCountHttpStatus302</span></span> | <span data-ttu-id="7eef5-329">Contagem de todos os pedidos que resultaram numa resposta de código HTTP 302</span><span class="sxs-lookup"><span data-stu-id="7eef5-329">Count of all requests that resulted in a 302 HTTP code response</span></span>              |<span data-ttu-id="7eef5-330">Não</span><span class="sxs-lookup"><span data-stu-id="7eef5-330">No</span></span>   |<span data-ttu-id="7eef5-331">Sim</span><span class="sxs-lookup"><span data-stu-id="7eef5-331">Yes</span></span>   |
| <span data-ttu-id="7eef5-332">RequestCountHttpStatus304</span><span class="sxs-lookup"><span data-stu-id="7eef5-332">RequestCountHttpStatus304</span></span> |  <span data-ttu-id="7eef5-333">Contagem de todos os pedidos que resultaram numa resposta código 304 HTTP</span><span class="sxs-lookup"><span data-stu-id="7eef5-333">Count of all requests that resulted in a 304 HTTP code response</span></span>             |<span data-ttu-id="7eef5-334">Não</span><span class="sxs-lookup"><span data-stu-id="7eef5-334">No</span></span>   |<span data-ttu-id="7eef5-335">Sim</span><span class="sxs-lookup"><span data-stu-id="7eef5-335">Yes</span></span>   |
| <span data-ttu-id="7eef5-336">RequestCountHttpStatus404</span><span class="sxs-lookup"><span data-stu-id="7eef5-336">RequestCountHttpStatus404</span></span> | <span data-ttu-id="7eef5-337">Contagem de todos os pedidos que resultaram numa resposta de código HTTP 404</span><span class="sxs-lookup"><span data-stu-id="7eef5-337">Count of all requests that resulted in a 404 HTTP code response</span></span>              |<span data-ttu-id="7eef5-338">Não</span><span class="sxs-lookup"><span data-stu-id="7eef5-338">No</span></span>   |<span data-ttu-id="7eef5-339">Sim</span><span class="sxs-lookup"><span data-stu-id="7eef5-339">Yes</span></span>   |
| <span data-ttu-id="7eef5-340">RequestCountCacheHit</span><span class="sxs-lookup"><span data-stu-id="7eef5-340">RequestCountCacheHit</span></span> |<span data-ttu-id="7eef5-341">Contagem de todos os pedidos que resultaram num de acertos na Cache.</span><span class="sxs-lookup"><span data-stu-id="7eef5-341">Count of all requests that resulted in a Cache Hit.</span></span> <span data-ttu-id="7eef5-342">Isto significa que o recurso de Olá servido diretamente a partir de Olá POP toohello cliente.</span><span class="sxs-lookup"><span data-stu-id="7eef5-342">This means hello asset was served directly from hello POP toohello Client.</span></span>               | <span data-ttu-id="7eef5-343">Sim</span><span class="sxs-lookup"><span data-stu-id="7eef5-343">Yes</span></span>  |<span data-ttu-id="7eef5-344">Não</span><span class="sxs-lookup"><span data-stu-id="7eef5-344">No</span></span>   |
| <span data-ttu-id="7eef5-345">RequestCountCacheMiss</span><span class="sxs-lookup"><span data-stu-id="7eef5-345">RequestCountCacheMiss</span></span> | <span data-ttu-id="7eef5-346">Contagem de todos os pedidos que resultaram numa Cache de falha de acerto na.</span><span class="sxs-lookup"><span data-stu-id="7eef5-346">Count of all requests that resulted in a Cache Miss.</span></span> <span data-ttu-id="7eef5-347">Isto significa que não foi encontrado no cliente de toohello mais próximo do Olá POP asset Olá e, por conseguinte, foi obtido do Olá origem.</span><span class="sxs-lookup"><span data-stu-id="7eef5-347">This means hello asset was not found on hello POP closest toohello client, and therefore was retrieved from hello Origin.</span></span>              |<span data-ttu-id="7eef5-348">Sim</span><span class="sxs-lookup"><span data-stu-id="7eef5-348">Yes</span></span>   | <span data-ttu-id="7eef5-349">Não</span><span class="sxs-lookup"><span data-stu-id="7eef5-349">No</span></span>  |
| <span data-ttu-id="7eef5-350">RequestCountCacheNoCache</span><span class="sxs-lookup"><span data-stu-id="7eef5-350">RequestCountCacheNoCache</span></span> | <span data-ttu-id="7eef5-351">Contagem de todos os pedidos de recurso de tooan impedido de ser colocadas em cache devido a configuração do utilizador tooa no limite de Olá.</span><span class="sxs-lookup"><span data-stu-id="7eef5-351">Count of all requests tooan asset that are prevented from being cached due tooa user configuration on hello edge.</span></span>              |<span data-ttu-id="7eef5-352">Sim</span><span class="sxs-lookup"><span data-stu-id="7eef5-352">Yes</span></span>   | <span data-ttu-id="7eef5-353">Não</span><span class="sxs-lookup"><span data-stu-id="7eef5-353">No</span></span>  |
| <span data-ttu-id="7eef5-354">RequestCountCacheUncacheable</span><span class="sxs-lookup"><span data-stu-id="7eef5-354">RequestCountCacheUncacheable</span></span> | <span data-ttu-id="7eef5-355">Contagem de todos os pedidos tooassets impedido de ser colocadas em cache por Cache-Control do elemento de Olá e expira cabeçalhos, o que indicam que este deve não ser colocadas em cache num POP ou pelo cliente de Olá HTTP</span><span class="sxs-lookup"><span data-stu-id="7eef5-355">Count of all requests tooassets that are prevented from being cached by hello asset's Cache-Control and Expires headers, which indicate that it should not be cached on a POP or by hello HTTP client</span></span>                |<span data-ttu-id="7eef5-356">Sim</span><span class="sxs-lookup"><span data-stu-id="7eef5-356">Yes</span></span>   |<span data-ttu-id="7eef5-357">Não</span><span class="sxs-lookup"><span data-stu-id="7eef5-357">No</span></span>   |
| <span data-ttu-id="7eef5-358">RequestCountCacheOthers</span><span class="sxs-lookup"><span data-stu-id="7eef5-358">RequestCountCacheOthers</span></span> | <span data-ttu-id="7eef5-359">Contagem de todos os pedidos com o estado de cache não abrangido por acima.</span><span class="sxs-lookup"><span data-stu-id="7eef5-359">Count of all requests with cache status not covered by above.</span></span>              |<span data-ttu-id="7eef5-360">Sim</span><span class="sxs-lookup"><span data-stu-id="7eef5-360">Yes</span></span>   | <span data-ttu-id="7eef5-361">Não</span><span class="sxs-lookup"><span data-stu-id="7eef5-361">No</span></span>  |
| <span data-ttu-id="7eef5-362">EgressTotal</span><span class="sxs-lookup"><span data-stu-id="7eef5-362">EgressTotal</span></span> | <span data-ttu-id="7eef5-363">Transferência de dados de saída em GB</span><span class="sxs-lookup"><span data-stu-id="7eef5-363">Outbound data transfer in GB</span></span>              |<span data-ttu-id="7eef5-364">Sim</span><span class="sxs-lookup"><span data-stu-id="7eef5-364">Yes</span></span>   |<span data-ttu-id="7eef5-365">Sim</span><span class="sxs-lookup"><span data-stu-id="7eef5-365">Yes</span></span>   |
| <span data-ttu-id="7eef5-366">EgressHttpStatus2xx</span><span class="sxs-lookup"><span data-stu-id="7eef5-366">EgressHttpStatus2xx</span></span> | <span data-ttu-id="7eef5-367">Dados de saída transferência * para respostas com códigos de estado HTTP 2xx em GB</span><span class="sxs-lookup"><span data-stu-id="7eef5-367">Outbound data transfer* for responses with 2xx HTTP status codes in GB</span></span>            |<span data-ttu-id="7eef5-368">Sim</span><span class="sxs-lookup"><span data-stu-id="7eef5-368">Yes</span></span>   |<span data-ttu-id="7eef5-369">Não</span><span class="sxs-lookup"><span data-stu-id="7eef5-369">No</span></span>   |
| <span data-ttu-id="7eef5-370">EgressHttpStatus3xx</span><span class="sxs-lookup"><span data-stu-id="7eef5-370">EgressHttpStatus3xx</span></span> | <span data-ttu-id="7eef5-371">Transferência de dados de saída para as respostas com códigos de estado HTTP 3xx em GB</span><span class="sxs-lookup"><span data-stu-id="7eef5-371">Outbound data transfer for responses with 3xx HTTP status codes in GB</span></span>              |<span data-ttu-id="7eef5-372">Sim</span><span class="sxs-lookup"><span data-stu-id="7eef5-372">Yes</span></span>   |<span data-ttu-id="7eef5-373">Não</span><span class="sxs-lookup"><span data-stu-id="7eef5-373">No</span></span>   |
| <span data-ttu-id="7eef5-374">EgressHttpStatus4xx</span><span class="sxs-lookup"><span data-stu-id="7eef5-374">EgressHttpStatus4xx</span></span> | <span data-ttu-id="7eef5-375">Transferência de dados de saída para as respostas com códigos de estado HTTP 4xx em GB</span><span class="sxs-lookup"><span data-stu-id="7eef5-375">Outbound data transfer for responses with 4xx HTTP status codes in GB</span></span>               |<span data-ttu-id="7eef5-376">Sim</span><span class="sxs-lookup"><span data-stu-id="7eef5-376">Yes</span></span>   | <span data-ttu-id="7eef5-377">Não</span><span class="sxs-lookup"><span data-stu-id="7eef5-377">No</span></span>  |
| <span data-ttu-id="7eef5-378">EgressHttpStatus5xx</span><span class="sxs-lookup"><span data-stu-id="7eef5-378">EgressHttpStatus5xx</span></span> | <span data-ttu-id="7eef5-379">Transferência de dados de saída para as respostas com códigos de estado HTTP 5xx em GB</span><span class="sxs-lookup"><span data-stu-id="7eef5-379">Outbound data transfer for responses with 5xx HTTP status codes in GB</span></span>               |<span data-ttu-id="7eef5-380">Sim</span><span class="sxs-lookup"><span data-stu-id="7eef5-380">Yes</span></span>   |  <span data-ttu-id="7eef5-381">Não</span><span class="sxs-lookup"><span data-stu-id="7eef5-381">No</span></span> |
| <span data-ttu-id="7eef5-382">EgressHttpStatusOthers</span><span class="sxs-lookup"><span data-stu-id="7eef5-382">EgressHttpStatusOthers</span></span> | <span data-ttu-id="7eef5-383">Transferência de dados de saída para as respostas com outros códigos de estado HTTP em GB</span><span class="sxs-lookup"><span data-stu-id="7eef5-383">Outbound data transfer for responses with other HTTP status codes in GB</span></span>                |<span data-ttu-id="7eef5-384">Sim</span><span class="sxs-lookup"><span data-stu-id="7eef5-384">Yes</span></span>   |<span data-ttu-id="7eef5-385">Não</span><span class="sxs-lookup"><span data-stu-id="7eef5-385">No</span></span>   |
| <span data-ttu-id="7eef5-386">EgressCacheHit</span><span class="sxs-lookup"><span data-stu-id="7eef5-386">EgressCacheHit</span></span> |  <span data-ttu-id="7eef5-387">Saída transferência de dados para as respostas que foram fornecidas diretamente a partir da cache CDN Olá no Olá POPs/contornos de CDN</span><span class="sxs-lookup"><span data-stu-id="7eef5-387">Outbound data transfer for responses that were delivered directly from hello CDN cache on hello CDN POPs/Edges</span></span>  |<span data-ttu-id="7eef5-388">Sim</span><span class="sxs-lookup"><span data-stu-id="7eef5-388">Yes</span></span>   |  <span data-ttu-id="7eef5-389">Não</span><span class="sxs-lookup"><span data-stu-id="7eef5-389">No</span></span> |
| <span data-ttu-id="7eef5-390">EgressCacheMiss</span><span class="sxs-lookup"><span data-stu-id="7eef5-390">EgressCacheMiss</span></span> | <span data-ttu-id="7eef5-391">Transferência de dados de saída para as respostas que não foram encontradas no Olá mais próximo do servidor POP e obtidas a partir do servidor de origem Olá</span><span class="sxs-lookup"><span data-stu-id="7eef5-391">Outbound data transfer for responses that were not found on hello nearest POP server, and retrieved from hello origin server</span></span>              |<span data-ttu-id="7eef5-392">Sim</span><span class="sxs-lookup"><span data-stu-id="7eef5-392">Yes</span></span>   |  <span data-ttu-id="7eef5-393">Não</span><span class="sxs-lookup"><span data-stu-id="7eef5-393">No</span></span> |
| <span data-ttu-id="7eef5-394">EgressCacheNoCache</span><span class="sxs-lookup"><span data-stu-id="7eef5-394">EgressCacheNoCache</span></span> | <span data-ttu-id="7eef5-395">Transferem de dados de saída para recursos que são impedidos de ser colocadas em cache devido a configuração do utilizador tooa no limite de Olá.</span><span class="sxs-lookup"><span data-stu-id="7eef5-395">Outbound data transfer for assets that are prevented from being cached due tooa user configuration on hello edge.</span></span>                |<span data-ttu-id="7eef5-396">Sim</span><span class="sxs-lookup"><span data-stu-id="7eef5-396">Yes</span></span>   |<span data-ttu-id="7eef5-397">Não</span><span class="sxs-lookup"><span data-stu-id="7eef5-397">No</span></span>   |
| <span data-ttu-id="7eef5-398">EgressCacheUncacheable</span><span class="sxs-lookup"><span data-stu-id="7eef5-398">EgressCacheUncacheable</span></span> | <span data-ttu-id="7eef5-399">Transferência de dados de saída para recursos que são impedidos de ser colocadas em cache por Cache-Control e/ou Expires cabeçalhos, o que indicam que este deve não ser colocadas em cache num POP ou pelo cliente de Olá HTTP do elemento de Olá</span><span class="sxs-lookup"><span data-stu-id="7eef5-399">Outbound data transfer for assets that are prevented from being cached by hello asset's Cache-Control and/or Expires headers, which indicate that it should not be cached on a POP or by hello HTTP client</span></span>                    |<span data-ttu-id="7eef5-400">Sim</span><span class="sxs-lookup"><span data-stu-id="7eef5-400">Yes</span></span>   | <span data-ttu-id="7eef5-401">Não</span><span class="sxs-lookup"><span data-stu-id="7eef5-401">No</span></span>  |
| <span data-ttu-id="7eef5-402">EgressCacheOthers</span><span class="sxs-lookup"><span data-stu-id="7eef5-402">EgressCacheOthers</span></span> |  <span data-ttu-id="7eef5-403">Transferências de dados de saída para obter outros cenários de cache.</span><span class="sxs-lookup"><span data-stu-id="7eef5-403">Outbound data transfers for other cache scenarios.</span></span>             |<span data-ttu-id="7eef5-404">Sim</span><span class="sxs-lookup"><span data-stu-id="7eef5-404">Yes</span></span>   | <span data-ttu-id="7eef5-405">Não</span><span class="sxs-lookup"><span data-stu-id="7eef5-405">No</span></span>  |

<span data-ttu-id="7eef5-406">* Transferência de dados saída refere-se tootraffic entregar do cliente de toohello de servidores POP do CDN.</span><span class="sxs-lookup"><span data-stu-id="7eef5-406">*Outbound data transfer refers tootraffic delivered from CDN POP servers toohello client.</span></span>


### <a name="schema-of-hello-core-analytics-logs"></a><span data-ttu-id="7eef5-407">Esquema de Olá registos de análise de núcleo</span><span class="sxs-lookup"><span data-stu-id="7eef5-407">Schema of hello Core Analytics Logs</span></span> 

<span data-ttu-id="7eef5-408">Todos os registos são armazenados no formato JSON e cada entrada tem campos de cadeia Olá abaixo esquema os seguintes:</span><span class="sxs-lookup"><span data-stu-id="7eef5-408">All logs are stored in JSON format and each entry has string fields following hello below schema:</span></span>

```json
    "records": [
        {
            "time": "2017-04-27T01:00:00",
            "resourceId": "<ARM Resource Id of hello CDN Endpoint>",
            "operationName": "Microsoft.Cdn/profiles/endpoints/contentDelivery",
            "category": "CoreAnalytics",
            "properties": {
                "DomainName": "<Name of hello domain for which hello statistics is reported>",
                "RequestCountTotal": integer value,
                "RequestCountHttpStatus2xx": integer value,
                "RequestCountHttpStatus3xx": integer value,
                "RequestCountHttpStatus4xx": integer value,
                "RequestCountHttpStatus5xx": integer value,
                "RequestCountHttpStatusOthers": integer value,
                "RequestCountHttpStatus200": integer value,
                "RequestCountHttpStatus206": integer value,
                "RequestCountHttpStatus302": integer value,
                "RequestCountHttpStatus304": integer value,
                "RequestCountHttpStatus404": integer value,
                "RequestCountCacheHit": integer value,
                "RequestCountCacheMiss": integer value,
                "RequestCountCacheNoCache": integer value,
                "RequestCountCacheUncacheable": integer value,
                "RequestCountCacheOthers": integer value,
                "EgressTotal": double value,
                "EgressHttpStatus2xx": double value,
                "EgressHttpStatus3xx": double value,
                "EgressHttpStatus4xx": double value,
                "EgressHttpStatus5xx": double value,
                "EgressHttpStatusOthers": double value,
                "EgressCacheHit": double value,
                "EgressCacheMiss": double value,
                "EgressCacheNoCache": double value,
                "EgressCacheUncacheable": double value,
                "EgressCacheOthers": double value,
            }
        }

    ]
}
```

<span data-ttu-id="7eef5-409">Onde Olá 'time' representa a hora de início de Olá de limite de hora Olá para o qual é reportadas a estatísticas de Olá.</span><span class="sxs-lookup"><span data-stu-id="7eef5-409">Where hello ‘time’ represents hello start time of hello hour boundary for which hello statistics is reported.</span></span> <span data-ttu-id="7eef5-410">Quando uma métrica não é suportada por um fornecedor CDN, em vez de um valor de duplo ou número inteiro, será um valor nulo.</span><span class="sxs-lookup"><span data-stu-id="7eef5-410">When a metric is not supported by a CDN provider, instead of a double or integer value, there will be a null value.</span></span> <span data-ttu-id="7eef5-411">Este valor nulo indica ausência Olá uma métrica e isto é diferente do valor de 0.</span><span class="sxs-lookup"><span data-stu-id="7eef5-411">This null value indicates hello absence of a metric, and this is different from a 0 value.</span></span> <span data-ttu-id="7eef5-412">Note também que vai haver um conjunto destas métricas por domínio configurado no ponto final de Olá.</span><span class="sxs-lookup"><span data-stu-id="7eef5-412">Also note that there will be one set of these metrics per domain configured on hello endpoint.</span></span>

<span data-ttu-id="7eef5-413">Propriedades de exemplo abaixo:</span><span class="sxs-lookup"><span data-stu-id="7eef5-413">Example properties below:</span></span>

```json
{
     "DomainName": "manlingakamaitest2.azureedge.net",
     "RequestCountTotal": 480,
     "RequestCountHttpStatus2xx": 480,
     "RequestCountHttpStatus3xx": 0,
     "RequestCountHttpStatus4xx": 0,
     "RequestCountHttpStatus5xx": 0,
     "RequestCountHttpStatusOthers": 0,
     "RequestCountHttpStatus200": 480,
     "RequestCountHttpStatus206": 0,
     "RequestCountHttpStatus302": 0,
     "RequestCountHttpStatus304": 0,
     "RequestCountHttpStatus404": 0,
     "RequestCountCacheHit": null,
     "RequestCountCacheMiss": null,
     "RequestCountCacheNoCache": null,
     "RequestCountCacheUncacheable": null,
     "RequestCountCacheOthers": null,
     "EgressTotal": 0.09,
     "EgressHttpStatus2xx": null,
     "EgressHttpStatus3xx": null,
     "EgressHttpStatus4xx": null,
     "EgressHttpStatus5xx": null,
     "EgressHttpStatusOthers": null,
     "EgressCacheHit": null,
     "EgressCacheMiss": null,
     "EgressCacheNoCache": null,
     "EgressCacheUncacheable": null,
     "EgressCacheOthers": null
}

```

## <a name="additional-resources"></a><span data-ttu-id="7eef5-414">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="7eef5-414">Additional resources</span></span>

* [<span data-ttu-id="7eef5-415">Registos de diagnóstico do Azure</span><span class="sxs-lookup"><span data-stu-id="7eef5-415">Azure Diagnostic logs</span></span>](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs)
* [<span data-ttu-id="7eef5-416">Análise de núcleo através do portal suplementar CDN do Azure</span><span class="sxs-lookup"><span data-stu-id="7eef5-416">Core analytics via Azure CDN supplemental portal</span></span>](https://docs.microsoft.com/azure/cdn/cdn-analyze-usage-patterns)
* [<span data-ttu-id="7eef5-417">Análise de registos do OMS do Azure</span><span class="sxs-lookup"><span data-stu-id="7eef5-417">Azure OMS Log Analytics</span></span>](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-overview)
* [<span data-ttu-id="7eef5-418">Análise de registos do Azure REST API</span><span class="sxs-lookup"><span data-stu-id="7eef5-418">Azure Log Analytics REST API</span></span>](https://docs.microsoft.com/en-us/rest/api/loganalytics)







