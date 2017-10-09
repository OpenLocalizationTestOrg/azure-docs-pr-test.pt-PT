---
title: aaaMonitor Surface Hubs com Log Analytics do Azure | Microsoft Docs
description: "Utilize Olá Surface Hub solução tootrack Olá estado de funcionamento do seu Surface Hubs e compreender como estão a ser utilizados."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: 8b4e56bc-2d4f-4648-a236-16e9e732ebef
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/07/2017
ms.author: banders
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 623d30e749cafdd4a34ba0c5b3408164f1b4a95b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-surface-hubs-with-log-analytics-tootrack-their-health"></a><span data-ttu-id="4bdfa-103">Monitorizar Surface Hubs tootrack de análise de registos com o respetivo estado de funcionamento</span><span class="sxs-lookup"><span data-stu-id="4bdfa-103">Monitor Surface Hubs with Log Analytics tootrack their health</span></span>

![Símbolo de Hub de superfície](./media/log-analytics-surface-hubs/surface-hub-symbol.png)

<span data-ttu-id="4bdfa-105">Este artigo descreve como pode utilizar Olá solução Surface Hub na análise de registos toomonitor Microsoft Surface Hub dispositivos Olá Microsoft Operations Management Suite (OMS).</span><span class="sxs-lookup"><span data-stu-id="4bdfa-105">This article describes how you can use hello Surface Hub solution in Log Analytics toomonitor Microsoft Surface Hub devices with hello Microsoft Operations Management Suite (OMS).</span></span> <span data-ttu-id="4bdfa-106">Inicie sessão ajuda a análise que controlar o estado de funcionamento de Olá do seu Surface Hubs, bem como a compreender como estão a ser utilizados.</span><span class="sxs-lookup"><span data-stu-id="4bdfa-106">Log Analytics helps you track hello health of your Surface Hubs as well as understand how they are being used.</span></span>

<span data-ttu-id="4bdfa-107">Cada Surface Hub tem Olá que Microsoft Monitoring Agent instalado.</span><span class="sxs-lookup"><span data-stu-id="4bdfa-107">Each Surface Hub has hello Microsoft Monitoring Agent installed.</span></span> <span data-ttu-id="4bdfa-108">O através do agente de Olá que pode enviar dados a partir do seu tooOMS Surface Hub.</span><span class="sxs-lookup"><span data-stu-id="4bdfa-108">Its through hello agent that you can send data from your Surface Hub tooOMS.</span></span> <span data-ttu-id="4bdfa-109">Ficheiros de registo são lidos a partir do seu Surface Hubs e estão, em seguida, são enviados o serviço do toohello OMS.</span><span class="sxs-lookup"><span data-stu-id="4bdfa-109">Log files are read from your Surface Hubs and are then are sent toohello OMS service.</span></span> <span data-ttu-id="4bdfa-110">Problemas, como servidores estar offline, Olá calendário não sincronizar ou se a conta de dispositivo Olá é toolog não é possível para o Skype são apresentados na OMS no dashboard do Olá Surface Hub.</span><span class="sxs-lookup"><span data-stu-id="4bdfa-110">Issues like servers being offline, hello calendar not syncing, or if hello device account is unable toolog into Skype are shown in OMS in hello Surface Hub dashboard.</span></span> <span data-ttu-id="4bdfa-111">Ao utilizar dados Olá no dashboard de Olá, pode identificar dispositivos que não estão em execução, ou que estão a ter outros problemas e potencialmente aplicar correções para problemas de Olá detetado.</span><span class="sxs-lookup"><span data-stu-id="4bdfa-111">By using hello data in hello dashboard, you can identify devices that are not running, or that are having other problems, and potentially apply fixes for hello detected issues.</span></span>

## <a name="installing-and-configuring-hello-solution"></a><span data-ttu-id="4bdfa-112">Instalar e configurar a solução de Olá</span><span class="sxs-lookup"><span data-stu-id="4bdfa-112">Installing and configuring hello solution</span></span>
<span data-ttu-id="4bdfa-113">Utilize Olá tooinstall informações a seguir e configurar a solução de Olá.</span><span class="sxs-lookup"><span data-stu-id="4bdfa-113">Use hello following information tooinstall and configure hello solution.</span></span> <span data-ttu-id="4bdfa-114">Na ordem toomanage o Surface Hubs de Olá Microsoft Operations Management Suite (OMS), terá de Olá seguintes:</span><span class="sxs-lookup"><span data-stu-id="4bdfa-114">In order toomanage your Surface Hubs from hello Microsoft Operations Management Suite (OMS), you'll need hello following:</span></span>

* <span data-ttu-id="4bdfa-115">Uma subscrição válida demasiado[OMS](http://www.microsoft.com/oms).</span><span class="sxs-lookup"><span data-stu-id="4bdfa-115">A valid subscription too[OMS](http://www.microsoft.com/oms).</span></span>
* <span data-ttu-id="4bdfa-116">Um [subscrição OMS](https://azure.microsoft.com/pricing/details/log-analytics/) nível que irão suportar o número de Olá de dispositivos que pretende toomonitor.</span><span class="sxs-lookup"><span data-stu-id="4bdfa-116">An [OMS subscription](https://azure.microsoft.com/pricing/details/log-analytics/) level that will support hello number of devices you want toomonitor.</span></span> <span data-ttu-id="4bdfa-117">Preços do OMS variam consoante o número de dispositivos inscritos e a quantidade de dados-processos.</span><span class="sxs-lookup"><span data-stu-id="4bdfa-117">OMS pricing varies depending on how many devices are enrolled, and how much data it processes.</span></span> <span data-ttu-id="4bdfa-118">Poderá ser útil tootake isto em consideração ao planear a sua implementação Surface Hub.</span><span class="sxs-lookup"><span data-stu-id="4bdfa-118">You'll want tootake this into consideration when planning your Surface Hub rollout.</span></span>

<span data-ttu-id="4bdfa-119">Em seguida, irá adicionar uma subscrição de Microsoft Azure existente do OMS subscrição tooyour ou criar uma nova área de trabalho diretamente através do portal do OMS Olá.</span><span class="sxs-lookup"><span data-stu-id="4bdfa-119">Next, you will either add an OMS subscription tooyour existing Microsoft Azure subscription or create a new workspace directly through hello OMS portal.</span></span> <span data-ttu-id="4bdfa-120">Instruções detalhadas para utilizando um dos métodos é [introdução à análise de registos](log-analytics-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="4bdfa-120">Detailed instructions for using either method is at [Get started with Log Analytics](log-analytics-get-started.md).</span></span> <span data-ttu-id="4bdfa-121">Depois de configurada Olá subscrição OMS, existem duas formas tooenroll os seus dispositivos Surface Hub:</span><span class="sxs-lookup"><span data-stu-id="4bdfa-121">Once hello OMS subscription is set up, there are two ways tooenroll your Surface Hub devices:</span></span>

* <span data-ttu-id="4bdfa-122">Automaticamente através do Intune</span><span class="sxs-lookup"><span data-stu-id="4bdfa-122">Automatically through Intune</span></span>
* <span data-ttu-id="4bdfa-123">Manualmente através de **definições** no seu dispositivo Surface Hub.</span><span class="sxs-lookup"><span data-stu-id="4bdfa-123">Manually through **Settings** on your Surface Hub device.</span></span>

## <a name="set-up-monitoring"></a><span data-ttu-id="4bdfa-124">Configurar a monitorização</span><span class="sxs-lookup"><span data-stu-id="4bdfa-124">Set up monitoring</span></span>
<span data-ttu-id="4bdfa-125">Pode monitorizar o estado de funcionamento de Olá e a atividade dos seus Surface Hub através da análise do registo no OMS.</span><span class="sxs-lookup"><span data-stu-id="4bdfa-125">You can monitor hello health and activity of your Surface Hub using Log Analytics in OMS.</span></span> <span data-ttu-id="4bdfa-126">Pode inscrever Olá Surface Hub no OMS através do Intune ou localmente utilizando **definições** no Olá Surface Hub.</span><span class="sxs-lookup"><span data-stu-id="4bdfa-126">You can enroll hello Surface Hub in OMS by using Intune, or locally by using **Settings** on hello Surface Hub.</span></span>

## <a name="connect-surface-hubs-toooms-through-intune"></a><span data-ttu-id="4bdfa-127">Ligar tooOMS Surface Hubs através do Intune</span><span class="sxs-lookup"><span data-stu-id="4bdfa-127">Connect Surface Hubs tooOMS through Intune</span></span>
<span data-ttu-id="4bdfa-128">Irá precisar de a Olá ID e a chave da área de trabalho para a área de trabalho do OMS Olá que irão gerir a sua Surface Hubs.</span><span class="sxs-lookup"><span data-stu-id="4bdfa-128">You'll need hello workspace ID and workspace key for hello OMS workspace that will manage your Surface Hubs.</span></span> <span data-ttu-id="4bdfa-129">Pode obter as do portal do OMS Olá.</span><span class="sxs-lookup"><span data-stu-id="4bdfa-129">You can get those from hello OMS portal.</span></span>

<span data-ttu-id="4bdfa-130">O Intune é um produto Microsoft permite-lhe toocentrally gerir Olá OMS as definições de configuração que são aplicado tooone ou mais dos seus dispositivos.</span><span class="sxs-lookup"><span data-stu-id="4bdfa-130">Intune is a Microsoft product that allows you toocentrally manage hello OMS configuration settings that are applied tooone or more of your devices.</span></span> <span data-ttu-id="4bdfa-131">Siga estes passos tooconfigure os seus dispositivos através do Intune:</span><span class="sxs-lookup"><span data-stu-id="4bdfa-131">Follow these steps tooconfigure your devices through Intune:</span></span>

1. <span data-ttu-id="4bdfa-132">Inicie sessão no tooIntune.</span><span class="sxs-lookup"><span data-stu-id="4bdfa-132">Sign in tooIntune.</span></span>
2. <span data-ttu-id="4bdfa-133">Navegue demasiado**definições** > **origens ligadas**.</span><span class="sxs-lookup"><span data-stu-id="4bdfa-133">Navigate too**Settings** > **Connected Sources**.</span></span>
3. <span data-ttu-id="4bdfa-134">Criar ou editar uma política baseada no modelo do Olá Surface Hub.</span><span class="sxs-lookup"><span data-stu-id="4bdfa-134">Create or edit a policy based on hello Surface Hub template.</span></span>
4. <span data-ttu-id="4bdfa-135">Navegue toohello secção OMS (informações operacionais do Azure) da política de Olá e adicionar Olá *ID da área de trabalho* e *chave da área de trabalho* toohello política.</span><span class="sxs-lookup"><span data-stu-id="4bdfa-135">Navigate toohello OMS (Azure Operational Insights) section of hello policy, and add hello *Workspace ID* and *Workspace Key* toohello policy.</span></span>
5. <span data-ttu-id="4bdfa-136">Guarde política de Olá.</span><span class="sxs-lookup"><span data-stu-id="4bdfa-136">Save hello policy.</span></span>
6. <span data-ttu-id="4bdfa-137">Associe política Olá grupo adequado do Olá dos dispositivos.</span><span class="sxs-lookup"><span data-stu-id="4bdfa-137">Associate hello policy with hello appropriate group of devices.</span></span>

   ![Política do Intune](./media/log-analytics-surface-hubs/intune.png)

<span data-ttu-id="4bdfa-139">Intune, em seguida, sincroniza-se as definições de OMS Olá com dispositivos Olá no grupo de destino Olá, inscrevendo-os na sua área de trabalho do OMS.</span><span class="sxs-lookup"><span data-stu-id="4bdfa-139">Intune then syncs hello OMS settings with hello devices in hello target group, enrolling them in your OMS workspace.</span></span>

## <a name="connect-surface-hubs-toooms-using-hello-settings-app"></a><span data-ttu-id="4bdfa-140">Ligar tooOMS Surface Hubs utilizando a aplicação de definições de Olá</span><span class="sxs-lookup"><span data-stu-id="4bdfa-140">Connect Surface Hubs tooOMS using hello Settings app</span></span>
<span data-ttu-id="4bdfa-141">Irá precisar de a Olá ID e a chave da área de trabalho para a área de trabalho do OMS Olá que irão gerir a sua Surface Hubs.</span><span class="sxs-lookup"><span data-stu-id="4bdfa-141">You'll need hello workspace ID and workspace key for hello OMS workspace that will manage your Surface Hubs.</span></span> <span data-ttu-id="4bdfa-142">Pode obter as do portal do OMS Olá.</span><span class="sxs-lookup"><span data-stu-id="4bdfa-142">You can get those from hello OMS portal.</span></span>

<span data-ttu-id="4bdfa-143">Se não utilizar o Intune toomanage seu ambiente, pode inscrever dispositivos manualmente através de **definições** em cada Surface Hub:</span><span class="sxs-lookup"><span data-stu-id="4bdfa-143">If you don't use Intune toomanage your environment, you can enroll devices manually through **Settings** on each Surface Hub:</span></span>

1. <span data-ttu-id="4bdfa-144">A partir do seu Surface Hub, abra **definições**.</span><span class="sxs-lookup"><span data-stu-id="4bdfa-144">From your Surface Hub, open **Settings**.</span></span>
2. <span data-ttu-id="4bdfa-145">Introduza as credenciais de administrador do dispositivo Olá quando lhe for pedido.</span><span class="sxs-lookup"><span data-stu-id="4bdfa-145">Enter hello device admin credentials when prompted.</span></span>
3. <span data-ttu-id="4bdfa-146">Clique em **este dispositivo**e Olá em **monitorização**, clique em **configurar definições do OMS**.</span><span class="sxs-lookup"><span data-stu-id="4bdfa-146">Click **This device**, and hello under **Monitoring**, click **Configure OMS Settings**.</span></span>
4. <span data-ttu-id="4bdfa-147">Selecione **Ativar monitorização**.</span><span class="sxs-lookup"><span data-stu-id="4bdfa-147">Select **Enable monitoring**.</span></span>
5. <span data-ttu-id="4bdfa-148">Na caixa de diálogo do definições do OMS de Olá, escreva Olá **ID da área de trabalho** e Olá tipo **chave da área de trabalho**.</span><span class="sxs-lookup"><span data-stu-id="4bdfa-148">In hello OMS settings dialog, type hello **Workspace ID** and type hello **Workspace Key**.</span></span>  
   <span data-ttu-id="4bdfa-149">![definições](./media/log-analytics-surface-hubs/settings.png)</span><span class="sxs-lookup"><span data-stu-id="4bdfa-149">![settings](./media/log-analytics-surface-hubs/settings.png)</span></span>
6. <span data-ttu-id="4bdfa-150">Clique em **OK** configuração de Olá toocomplete.</span><span class="sxs-lookup"><span data-stu-id="4bdfa-150">Click **OK** toocomplete hello configuration.</span></span>

<span data-ttu-id="4bdfa-151">Uma confirmação é apresentado a informar se pretende ou não Olá configuração OMS com êxito foi aplicada toohello dispositivo.</span><span class="sxs-lookup"><span data-stu-id="4bdfa-151">A confirmation appears telling you whether or not hello OMS configuration was successfully applied toohello device.</span></span> <span data-ttu-id="4bdfa-152">Se tiver sido, é apresentada uma mensagem a indicar que o agente Olá ligado com êxito o serviço do toohello OMS.</span><span class="sxs-lookup"><span data-stu-id="4bdfa-152">If it was, a message appears stating that hello agent successfully connected toohello OMS service.</span></span> <span data-ttu-id="4bdfa-153">dispositivo Olá, em seguida, começa a enviar dados tooOMS onde pode ver e atuar no mesmo.</span><span class="sxs-lookup"><span data-stu-id="4bdfa-153">hello device then starts sending data tooOMS where you can view and act on it.</span></span>

## <a name="monitor-surface-hubs"></a><span data-ttu-id="4bdfa-154">Monitor de Surface Hubs</span><span class="sxs-lookup"><span data-stu-id="4bdfa-154">Monitor Surface Hubs</span></span>
<span data-ttu-id="4bdfa-155">Monitorização do seu Surface Hubs utilizar OMS é muito como monitorizar todos os outros dispositivos inscritos.</span><span class="sxs-lookup"><span data-stu-id="4bdfa-155">Monitoring your Surface Hubs using OMS is much like monitoring any other enrolled devices.</span></span>

1. <span data-ttu-id="4bdfa-156">Inicie sessão no toohello portal do OMS.</span><span class="sxs-lookup"><span data-stu-id="4bdfa-156">Sign in toohello OMS portal.</span></span>
2. <span data-ttu-id="4bdfa-157">Navegue até o dashboard de pacote de solução do toohello Surface Hub.</span><span class="sxs-lookup"><span data-stu-id="4bdfa-157">Navigate toohello Surface Hub solution pack dashboard.</span></span>
3. <span data-ttu-id="4bdfa-158">É apresentado o estado de funcionamento do seu dispositivo.</span><span class="sxs-lookup"><span data-stu-id="4bdfa-158">Your device's health is displayed.</span></span>

   ![Dashboard de Hub de superfície](./media/log-analytics-surface-hubs/surface-hub-dashboard.png)

<span data-ttu-id="4bdfa-160">Pode criar [alertas](log-analytics-alerts.md) com base na procura de registo existentes ou personalizados.</span><span class="sxs-lookup"><span data-stu-id="4bdfa-160">You can create [alerts](log-analytics-alerts.md) based on existing or custom log searches.</span></span> <span data-ttu-id="4bdfa-161">Utilizar Olá de dados de Olá que OMS recolhe do seu Surface Hubs, pode procurar problemas e alerta em condições de Olá por si para os seus dispositivos.</span><span class="sxs-lookup"><span data-stu-id="4bdfa-161">Using hello data hello OMS collects from your Surface Hubs, you can search for issues and alert on hello conditions that you define for your devices.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4bdfa-162">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="4bdfa-162">Next steps</span></span>
* <span data-ttu-id="4bdfa-163">Utilize [pesquisas de registo na análise de registos](log-analytics-log-searches.md) tooview detalhadas dados Surface Hub.</span><span class="sxs-lookup"><span data-stu-id="4bdfa-163">Use [Log searches in Log Analytics](log-analytics-log-searches.md) tooview detailed Surface Hub data.</span></span>
* <span data-ttu-id="4bdfa-164">Criar [alertas](log-analytics-alerts.md) toonotify-o quando ocorrem problemas com o Surface Hubs.</span><span class="sxs-lookup"><span data-stu-id="4bdfa-164">Create [alerts](log-analytics-alerts.md) toonotify you when issues occur with your Surface Hubs.</span></span>
