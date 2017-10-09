---
title: aaaGet ao agendador do Azure no portal do Azure | Microsoft Docs
description: "Introdução ao Agendador do Azure no portal do Azure"
services: scheduler
documentationcenter: .NET
author: derek1ee
manager: kevinlam1
editor: 
ms.assetid: e69542ec-d10f-4f17-9b7a-2ee441ee7d68
ms.service: scheduler
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 08/10/2016
ms.author: deli
ms.openlocfilehash: 58255c0ad19da65932f8b1d36cb8fef1ff6e651b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-scheduler-in-azure-portal"></a><span data-ttu-id="748f5-103">Introdução ao Agendador do Azure no portal do Azure</span><span class="sxs-lookup"><span data-stu-id="748f5-103">Get started with Azure Scheduler in Azure portal</span></span>
<span data-ttu-id="748f5-104">É fácil toocreate agendada tarefas do agendador do Azure.</span><span class="sxs-lookup"><span data-stu-id="748f5-104">It's easy toocreate scheduled jobs in Azure Scheduler.</span></span> <span data-ttu-id="748f5-105">Neste tutorial, irá aprender como toocreate uma tarefa.</span><span class="sxs-lookup"><span data-stu-id="748f5-105">In this tutorial, you'll learn how toocreate a job.</span></span> <span data-ttu-id="748f5-106">Também irá aprender capacidades de monitorização e gestão do Agendador.</span><span class="sxs-lookup"><span data-stu-id="748f5-106">You'll also learn Scheduler's monitoring and management capabilities.</span></span>

## <a name="create-a-job"></a><span data-ttu-id="748f5-107">Criar uma tarefa</span><span class="sxs-lookup"><span data-stu-id="748f5-107">Create a job</span></span>
1. <span data-ttu-id="748f5-108">A iniciar sessão demasiado[portal do Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="748f5-108">Sign in too[Azure portal](https://portal.azure.com/).</span></span>  
2. <span data-ttu-id="748f5-109">Clique em **+ novo** > tipo *programador* na caixa de pesquisa de Olá > selecione **programador** nos resultados > clique **criar**.</span><span class="sxs-lookup"><span data-stu-id="748f5-109">Click **+New** > type *Scheduler* in hello search box >  select **Scheduler** in results > click **Create**.</span></span>
   
    ![][marketplace-create]
3. <span data-ttu-id="748f5-110">Vamos criar uma tarefa que simplesmente chegue a http://www.microsoft.com/ com um pedido GET.</span><span class="sxs-lookup"><span data-stu-id="748f5-110">Let’s create a job that simply hits http://www.microsoft.com/ with a GET request.</span></span> <span data-ttu-id="748f5-111">No Olá **tarefa do agendador** ecrã, introduza Olá seguintes informações:</span><span class="sxs-lookup"><span data-stu-id="748f5-111">In hello **Scheduler Job** screen, enter hello following information:</span></span>
   
   1. <span data-ttu-id="748f5-112">**Nome:** `getmicrosoft`</span><span class="sxs-lookup"><span data-stu-id="748f5-112">**Name:** `getmicrosoft`</span></span>  
   2. <span data-ttu-id="748f5-113">**Subscrição:** a sua subscrição do Azure</span><span class="sxs-lookup"><span data-stu-id="748f5-113">**Subscription:** Your Azure subscription</span></span>   
   3. <span data-ttu-id="748f5-114">**Coleção de Tarefas:** selecione uma coleção de tarefas existente ou clique em **Criar novo** > introduza um nome.</span><span class="sxs-lookup"><span data-stu-id="748f5-114">**Job Collection:** Select an existing job collection, or click **Create New** > enter a name.</span></span>
4. <span data-ttu-id="748f5-115">Em seguida, no **definições de ação**, definir Olá os seguintes valores:</span><span class="sxs-lookup"><span data-stu-id="748f5-115">Next, in **Action Settings**, define hello following values:</span></span>
   
   1. <span data-ttu-id="748f5-116">**Tipo de Ação:** ` HTTP`</span><span class="sxs-lookup"><span data-stu-id="748f5-116">**Action Type:** ` HTTP`</span></span>  
   2. <span data-ttu-id="748f5-117">**Método:** `GET`</span><span class="sxs-lookup"><span data-stu-id="748f5-117">**Method:** `GET`</span></span>  
   3. <span data-ttu-id="748f5-118">**URL:** ` http://www.microsoft.com`</span><span class="sxs-lookup"><span data-stu-id="748f5-118">**URL:** ` http://www.microsoft.com`</span></span>  
      
      ![][action-settings]
5. <span data-ttu-id="748f5-119">Por fim, vamos definir uma agenda.</span><span class="sxs-lookup"><span data-stu-id="748f5-119">Finally, let's define a schedule.</span></span> <span data-ttu-id="748f5-120">tarefa de Olá pode ser definido como uma única tarefa, mas vamos escolher uma agenda de periodicidade:</span><span class="sxs-lookup"><span data-stu-id="748f5-120">hello job could be defined as a one-time job, but let’s pick a recurrence schedule:</span></span>
   
   1. <span data-ttu-id="748f5-121">**Periodicidade**: `Recurring`</span><span class="sxs-lookup"><span data-stu-id="748f5-121">**Recurrence**: `Recurring`</span></span>
   2. <span data-ttu-id="748f5-122">**Iniciar**: data de hoje</span><span class="sxs-lookup"><span data-stu-id="748f5-122">**Start**: Today's date</span></span>
   3. <span data-ttu-id="748f5-123">**Recorrer a cada**: `12 Hours`</span><span class="sxs-lookup"><span data-stu-id="748f5-123">**Recur every**: `12 Hours`</span></span>
   4. <span data-ttu-id="748f5-124">**Terminar a**: dois dias a partir da data de hoje</span><span class="sxs-lookup"><span data-stu-id="748f5-124">**End by**: Two days from today's date</span></span>  
      
      ![][recurrence-schedule]
6. <span data-ttu-id="748f5-125">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="748f5-125">Click **Create**</span></span>

## <a name="manage-and-monitor-jobs"></a><span data-ttu-id="748f5-126">Gerir e monitorizar tarefas</span><span class="sxs-lookup"><span data-stu-id="748f5-126">Manage and monitor jobs</span></span>
<span data-ttu-id="748f5-127">Quando é criada uma tarefa, aparecerá no dashboard do Olá principal do Azure.</span><span class="sxs-lookup"><span data-stu-id="748f5-127">Once a job is created, it appears in hello main Azure dashboard.</span></span> <span data-ttu-id="748f5-128">Clique em tarefa Olá e uma nova janela abre-se com Olá seguintes separadores:</span><span class="sxs-lookup"><span data-stu-id="748f5-128">Click hello job and a new window opens with hello following tabs:</span></span>

1. <span data-ttu-id="748f5-129">Propriedades</span><span class="sxs-lookup"><span data-stu-id="748f5-129">Properties</span></span>  
2. <span data-ttu-id="748f5-130">Definições de Ação</span><span class="sxs-lookup"><span data-stu-id="748f5-130">Action Settings</span></span>  
3. <span data-ttu-id="748f5-131">Agenda</span><span class="sxs-lookup"><span data-stu-id="748f5-131">Schedule</span></span>  
4. <span data-ttu-id="748f5-132">Histórico</span><span class="sxs-lookup"><span data-stu-id="748f5-132">History</span></span>
5. <span data-ttu-id="748f5-133">Utilizadores</span><span class="sxs-lookup"><span data-stu-id="748f5-133">Users</span></span>
   
   ![][job-overview]

### <a name="properties"></a><span data-ttu-id="748f5-134">Propriedades</span><span class="sxs-lookup"><span data-stu-id="748f5-134">Properties</span></span>
<span data-ttu-id="748f5-135">Estas propriedades só de leitura descrevem Olá gestão metadados de tarefa do agendador de Olá.</span><span class="sxs-lookup"><span data-stu-id="748f5-135">These read-only properties describe hello management metadata for hello Scheduler job.</span></span>

   ![][job-properties]

### <a name="action-settings"></a><span data-ttu-id="748f5-136">Definições de ação</span><span class="sxs-lookup"><span data-stu-id="748f5-136">Action settings</span></span>
<span data-ttu-id="748f5-137">Clicar numa tarefa no Olá **tarefas** ecrã permite-lhe tooconfigure da tarefa.</span><span class="sxs-lookup"><span data-stu-id="748f5-137">Clicking on a job in hello **Jobs** screen allows you tooconfigure that job.</span></span> <span data-ttu-id="748f5-138">Isto permite-lhe configurar as definições avançadas, se não as tenha feito no Olá criação rápida assistente.</span><span class="sxs-lookup"><span data-stu-id="748f5-138">This lets you configure advanced settings, if you didn't configure them in hello quick-create wizard.</span></span>

<span data-ttu-id="748f5-139">Para todos os tipos de ação, pode alterar a política de repetição Olá e ação de erro Olá.</span><span class="sxs-lookup"><span data-stu-id="748f5-139">For all action types, you may change hello retry policy and hello error action.</span></span>

<span data-ttu-id="748f5-140">Para os tipos de ação de tarefa HTTP e HTTPS, pode alterar Olá método tooany permitido verbo HTTP.</span><span class="sxs-lookup"><span data-stu-id="748f5-140">For HTTP and HTTPS job action types, you may change hello method tooany allowed HTTP verb.</span></span> <span data-ttu-id="748f5-141">Também pode adicionar, eliminar ou alterar cabeçalhos Olá e informações de autenticação básica.</span><span class="sxs-lookup"><span data-stu-id="748f5-141">You may also add, delete, or change hello headers and basic authentication information.</span></span>

<span data-ttu-id="748f5-142">Para tipos de ação de fila de armazenamento, pode alterar a conta de armazenamento Olá, nome da fila, SAS token e corpo.</span><span class="sxs-lookup"><span data-stu-id="748f5-142">For storage queue action types, you may change hello storage account, queue name, SAS token, and body.</span></span>

<span data-ttu-id="748f5-143">Para os tipos de ação de barramento de serviço, pode alterar Olá espaço de nomes, caminho do tópico/fila, definições de autenticação, tipo de transporte, propriedades da mensagem e corpo da mensagem.</span><span class="sxs-lookup"><span data-stu-id="748f5-143">For service bus action types, you may change hello namespace, topic/queue path, authentication settings, transport type, message properties, and message body.</span></span>

   ![][job-action-settings]

### <a name="schedule"></a><span data-ttu-id="748f5-144">Agenda</span><span class="sxs-lookup"><span data-stu-id="748f5-144">Schedule</span></span>
<span data-ttu-id="748f5-145">Isto permite-lhe reconfigurar a agenda de Olá, se pretender que o agendamento de Olá toochange que criou no Olá criação rápida assistente.</span><span class="sxs-lookup"><span data-stu-id="748f5-145">This lets you reconfigure hello schedule, if you'd like toochange hello schedule you created in hello quick-create wizard.</span></span>

<span data-ttu-id="748f5-146">Esta é uma oportunidade toobuild [agendas complexas e periodicidade avançada na sua tarefa](scheduler-advanced-complexity.md)</span><span class="sxs-lookup"><span data-stu-id="748f5-146">This is an opportunity toobuild [complex schedules and advanced recurrence in your job](scheduler-advanced-complexity.md)</span></span>

<span data-ttu-id="748f5-147">Pode alterar a data de início Olá e tempo, a agenda de periodicidade e Olá terminar a data e hora (se a tarefa de Olá seja recorrente).</span><span class="sxs-lookup"><span data-stu-id="748f5-147">You may change hello start date and time, recurrence schedule, and hello end date and time (if hello job is recurring.)</span></span>

   ![][job-schedule]

### <a name="history"></a><span data-ttu-id="748f5-148">Histórico</span><span class="sxs-lookup"><span data-stu-id="748f5-148">History</span></span>
<span data-ttu-id="748f5-149">Olá **histórico** separador mostra as métricas selecionadas para cada execução da tarefa no sistema de Olá para a tarefa selecionada Olá.</span><span class="sxs-lookup"><span data-stu-id="748f5-149">hello **History** tab displays selected metrics for every job execution in hello system for hello selected job.</span></span> <span data-ttu-id="748f5-150">Estas métricas fornecem valores em tempo real sobre o estado de funcionamento de Olá do seu agendador:</span><span class="sxs-lookup"><span data-stu-id="748f5-150">These metrics provide real-time values regarding hello health of your Scheduler:</span></span>

1. <span data-ttu-id="748f5-151">Estado</span><span class="sxs-lookup"><span data-stu-id="748f5-151">Status</span></span>  
2. <span data-ttu-id="748f5-152">Detalhes</span><span class="sxs-lookup"><span data-stu-id="748f5-152">Details</span></span>  
3. <span data-ttu-id="748f5-153">Tentativas de repetição</span><span class="sxs-lookup"><span data-stu-id="748f5-153">Retry attempts</span></span>
4. <span data-ttu-id="748f5-154">Ocorrência: 1ª, 2ª, 3ª, etc.</span><span class="sxs-lookup"><span data-stu-id="748f5-154">Occurrence: 1st, 2nd, 3rd, etc.</span></span>
5. <span data-ttu-id="748f5-155">Hora de início de execução</span><span class="sxs-lookup"><span data-stu-id="748f5-155">Start time of execution</span></span>  
6. <span data-ttu-id="748f5-156">Hora de fim de execução</span><span class="sxs-lookup"><span data-stu-id="748f5-156">End time of execution</span></span>
   
   ![][job-history]

<span data-ttu-id="748f5-157">Pode clicar numa execução tooview respetivo **detalhes de histórico**, incluindo a resposta completa do Olá para cada execução.</span><span class="sxs-lookup"><span data-stu-id="748f5-157">You can click on a run tooview its **History Details**, including hello whole response for every execution.</span></span> <span data-ttu-id="748f5-158">Esta caixa de diálogo também lhe permite área de transferência do toocopy Olá resposta toohello.</span><span class="sxs-lookup"><span data-stu-id="748f5-158">This dialog box also allows you toocopy hello response toohello clipboard.</span></span>

   ![][job-history-details]

### <a name="users"></a><span data-ttu-id="748f5-159">Utilizadores</span><span class="sxs-lookup"><span data-stu-id="748f5-159">Users</span></span>
<span data-ttu-id="748f5-160">O Controlo de Acesso Baseado em Funções (RBAC) do Azure permite uma gestão pormenorizada de acesso ao Agendador do Azure.</span><span class="sxs-lookup"><span data-stu-id="748f5-160">Azure Role-Based Access Control (RBAC) enables fine-grained access management for Azure Scheduler.</span></span> <span data-ttu-id="748f5-161">toolearn como toouse Olá separador de utilizadores, consulte demasiado[controlo de acesso em funções do Azure](../active-directory/role-based-access-control-configure.md)</span><span class="sxs-lookup"><span data-stu-id="748f5-161">toolearn how toouse hello Users tab, refer too[Azure Role-Based Access Control](../active-directory/role-based-access-control-configure.md)</span></span>

## <a name="see-also"></a><span data-ttu-id="748f5-162">Consultar também</span><span class="sxs-lookup"><span data-stu-id="748f5-162">See also</span></span>
 [<span data-ttu-id="748f5-163">O que é o Scheduler?</span><span class="sxs-lookup"><span data-stu-id="748f5-163">What is Scheduler?</span></span>](scheduler-intro.md)

 [<span data-ttu-id="748f5-164">Conceitos, terminologia e hierarquia de entidades do Scheduler</span><span class="sxs-lookup"><span data-stu-id="748f5-164">Scheduler concepts, terminology, and entity hierarchy</span></span>](scheduler-concepts-terms.md)

 [<span data-ttu-id="748f5-165">Planos e faturação no Azure Scheduler</span><span class="sxs-lookup"><span data-stu-id="748f5-165">Plans and billing in Azure Scheduler</span></span>](scheduler-plans-billing.md)

 [<span data-ttu-id="748f5-166">Como as agendas de toobuild complexas e periodicidade avançada com o agendador do Azure</span><span class="sxs-lookup"><span data-stu-id="748f5-166">How toobuild complex schedules and advanced recurrence with Azure Scheduler</span></span>](scheduler-advanced-complexity.md)

 [<span data-ttu-id="748f5-167">Referência da API REST do Scheduler</span><span class="sxs-lookup"><span data-stu-id="748f5-167">Scheduler REST API reference</span></span>](https://msdn.microsoft.com/library/mt629143)

 [<span data-ttu-id="748f5-168">Referência de cmdlets do PowerShell do Scheduler</span><span class="sxs-lookup"><span data-stu-id="748f5-168">Scheduler PowerShell cmdlets reference</span></span>](scheduler-powershell-reference.md)

 [<span data-ttu-id="748f5-169">Elevada disponibilidade e fiabilidade do Scheduler</span><span class="sxs-lookup"><span data-stu-id="748f5-169">Scheduler high-availability and reliability</span></span>](scheduler-high-availability-reliability.md)

 [<span data-ttu-id="748f5-170">Limites, predefinições e códigos de erro do Scheduler</span><span class="sxs-lookup"><span data-stu-id="748f5-170">Scheduler limits, defaults, and error codes</span></span>](scheduler-limits-defaults-errors.md)

 [<span data-ttu-id="748f5-171">Autenticação de saída do Scheduler</span><span class="sxs-lookup"><span data-stu-id="748f5-171">Scheduler outbound authentication</span></span>](scheduler-outbound-authentication.md)

[marketplace-create]: ./media/scheduler-get-started-portal/scheduler-v2-portal-marketplace-create.png
[action-settings]: ./media/scheduler-get-started-portal/scheduler-v2-portal-action-settings.png
[recurrence-schedule]: ./media/scheduler-get-started-portal/scheduler-v2-portal-recurrence-schedule.png
[job-properties]: ./media/scheduler-get-started-portal/scheduler-v2-portal-job-properties.png
[job-overview]: ./media/scheduler-get-started-portal/scheduler-v2-portal-job-overview-1.png
[job-action-settings]: ./media/scheduler-get-started-portal/scheduler-v2-portal-job-action-settings.png
[job-schedule]: ./media/scheduler-get-started-portal/scheduler-v2-portal-job-schedule.png
[job-history]: ./media/scheduler-get-started-portal/scheduler-v2-portal-job-history.png
[job-history-details]: ./media/scheduler-get-started-portal/scheduler-v2-portal-job-history-details.png


[1]: ./media/scheduler-get-started-portal/scheduler-get-started-portal001.png
[2]: ./media/scheduler-get-started-portal/scheduler-get-started-portal002.png
[3]: ./media/scheduler-get-started-portal/scheduler-get-started-portal003.png
[4]: ./media/scheduler-get-started-portal/scheduler-get-started-portal004.png
[5]: ./media/scheduler-get-started-portal/scheduler-get-started-portal005.png
[6]: ./media/scheduler-get-started-portal/scheduler-get-started-portal006.png
[7]: ./media/scheduler-get-started-portal/scheduler-get-started-portal007.png
[8]: ./media/scheduler-get-started-portal/scheduler-get-started-portal008.png
[9]: ./media/scheduler-get-started-portal/scheduler-get-started-portal009.png
[10]: ./media/scheduler-get-started-portal/scheduler-get-started-portal010.png
[11]: ./media/scheduler-get-started-portal/scheduler-get-started-portal011.png
[12]: ./media/scheduler-get-started-portal/scheduler-get-started-portal012.png
[13]: ./media/scheduler-get-started-portal/scheduler-get-started-portal013.png
[14]: ./media/scheduler-get-started-portal/scheduler-get-started-portal014.png
[15]: ./media/scheduler-get-started-portal/scheduler-get-started-portal015.png
