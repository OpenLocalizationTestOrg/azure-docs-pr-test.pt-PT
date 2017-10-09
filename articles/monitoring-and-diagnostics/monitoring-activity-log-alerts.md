---
title: alertas de registo de atividade aaaCreate | Microsoft Docs
description: "Seja notificado através de SMS, o webhook e o e-mail quando determinados eventos ocorrem no registo de atividade Olá."
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/03/2017
ms.author: johnkem
ms.openlocfilehash: ba0716cc12a0b3a0024ee5562a025f3f153f8982
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-activity-log-alerts"></a><span data-ttu-id="7ad45-103">Criar alertas de registo de atividade</span><span class="sxs-lookup"><span data-stu-id="7ad45-103">Create activity log alerts</span></span>

## <a name="overview"></a><span data-ttu-id="7ad45-104">Descrição geral</span><span class="sxs-lookup"><span data-stu-id="7ad45-104">Overview</span></span>
<span data-ttu-id="7ad45-105">Alertas de registo de atividade são alertas que ativar quando ocorre a um novo registo de eventos de atividade que corresponde a condições de Olá especificadas no alerta Olá.</span><span class="sxs-lookup"><span data-stu-id="7ad45-105">Activity log alerts are alerts that activate when a new activity log event occurs that matches hello conditions specified in hello alert.</span></span> <span data-ttu-id="7ad45-106">São recursos do Azure, pelo que pode ser criadas utilizando um modelo Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="7ad45-106">They are Azure resources, so they can be created by using an Azure Resource Manager template.</span></span> <span data-ttu-id="7ad45-107">Também podem ser criados, atualizar ou eliminados no Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="7ad45-107">They also can be created, updated, or deleted in hello Azure portal.</span></span> <span data-ttu-id="7ad45-108">Este artigo apresenta alguns conceitos de Olá atrás de alertas de registo de atividade.</span><span class="sxs-lookup"><span data-stu-id="7ad45-108">This article introduces hello concepts behind activity log alerts.</span></span> <span data-ttu-id="7ad45-109">Em seguida, mostra como toouse Olá tooset portal do Azure, um alerta sobre eventos de registo de atividade.</span><span class="sxs-lookup"><span data-stu-id="7ad45-109">It then shows you how toouse hello Azure portal tooset up an alert on activity log events.</span></span>

<span data-ttu-id="7ad45-110">Normalmente, pode cria alertas de registo de atividade tooreceive notificações quando:</span><span class="sxs-lookup"><span data-stu-id="7ad45-110">Typically, you create activity log alerts tooreceive notifications when:</span></span>

* <span data-ttu-id="7ad45-111">Alterações específicas ocorrerem em recursos na sua subscrição do Azure, muitas vezes, âmbito tooparticular grupos de recursos ou recursos.</span><span class="sxs-lookup"><span data-stu-id="7ad45-111">Specific changes occur on resources in your Azure subscription, often scoped tooparticular resource groups or resources.</span></span> <span data-ttu-id="7ad45-112">Por exemplo, poderá pretender toobe notificado quando qualquer máquina virtual na myProductionResourceGroup é eliminada.</span><span class="sxs-lookup"><span data-stu-id="7ad45-112">For example, you might want toobe notified when any virtual machine in myProductionResourceGroup is deleted.</span></span> <span data-ttu-id="7ad45-113">Em alternativa, pode querer toobe notificado se quaisquer novas funções são atribuídas tooa utilizador na sua subscrição.</span><span class="sxs-lookup"><span data-stu-id="7ad45-113">Or, you might want toobe notified if any new roles are assigned tooa user in your subscription.</span></span>
* <span data-ttu-id="7ad45-114">Ocorre um evento de estado de funcionamento do serviço.</span><span class="sxs-lookup"><span data-stu-id="7ad45-114">A service health event occurs.</span></span> <span data-ttu-id="7ad45-115">Eventos de estado de funcionamento de serviço incluem a notificação de incidentes e eventos de manutenção que se aplicam tooresources na sua subscrição.</span><span class="sxs-lookup"><span data-stu-id="7ad45-115">Service health events include notification of incidents and maintenance events that apply tooresources in your subscription.</span></span>

<span data-ttu-id="7ad45-116">Em ambos os casos, um alerta de registo de atividade monitoriza apenas eventos na subscrição Olá no qual Olá é criado um alerta.</span><span class="sxs-lookup"><span data-stu-id="7ad45-116">In either case, an activity log alert monitors only for events in hello subscription in which hello alert is created.</span></span>

<span data-ttu-id="7ad45-117">Pode configurar um alerta de registo de atividade com base em qualquer propriedade de nível superior do objeto JSON Olá para um registo de eventos de atividade.</span><span class="sxs-lookup"><span data-stu-id="7ad45-117">You can configure an activity log alert based on any top-level property in hello JSON object for an activity log event.</span></span> <span data-ttu-id="7ad45-118">No entanto, o portal de Olá mostra as opções mais comuns de Olá:</span><span class="sxs-lookup"><span data-stu-id="7ad45-118">However, hello portal shows hello most common options:</span></span>

- <span data-ttu-id="7ad45-119">**Categoria**: administrativo, serviço de estado de funcionamento, dimensionamento automático e recomendação.</span><span class="sxs-lookup"><span data-stu-id="7ad45-119">**Category**: Administrative, Service Health, Autoscale, and Recommendation.</span></span> <span data-ttu-id="7ad45-120">Para obter mais informações, consulte [descrição geral do registo de atividade do Azure de Olá](./monitoring-overview-activity-logs.md#categories-in-the-activity-log).</span><span class="sxs-lookup"><span data-stu-id="7ad45-120">For more information, see [Overview of hello Azure activity log](./monitoring-overview-activity-logs.md#categories-in-the-activity-log).</span></span> <span data-ttu-id="7ad45-121">toolearn mais informações sobre eventos de estado de funcionamento do serviço, consulte [receber alertas de registo de atividade em notificações de serviço](./monitoring-activity-log-alerts-on-service-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="7ad45-121">toolearn more about service health events, see [Receive activity log alerts on service notifications](./monitoring-activity-log-alerts-on-service-notifications.md).</span></span>
- <span data-ttu-id="7ad45-122">**Grupo de recursos**</span><span class="sxs-lookup"><span data-stu-id="7ad45-122">**Resource group**</span></span>
- <span data-ttu-id="7ad45-123">**Recurso**</span><span class="sxs-lookup"><span data-stu-id="7ad45-123">**Resource**</span></span>
- <span data-ttu-id="7ad45-124">**Tipo de recurso**</span><span class="sxs-lookup"><span data-stu-id="7ad45-124">**Resource type**</span></span>
- <span data-ttu-id="7ad45-125">**Nome da operação**: nome de operação de controlo de acesso baseado em funções do Resource Manager Olá.</span><span class="sxs-lookup"><span data-stu-id="7ad45-125">**Operation name**: hello Resource Manager Role-Based Access Control operation name.</span></span>
- <span data-ttu-id="7ad45-126">**Nível**: Olá nível de gravidade do evento de Olá (verboso, informativo, aviso, erro ou crítico).</span><span class="sxs-lookup"><span data-stu-id="7ad45-126">**Level**: hello severity level of hello event (Verbose, Informational, Warning, Error, or Critical).</span></span>
- <span data-ttu-id="7ad45-127">**Estado**: Estado Olá do evento de Olá, normalmente iniciada, falhou ou foi concluída com êxito.</span><span class="sxs-lookup"><span data-stu-id="7ad45-127">**Status**: hello status of hello event, typically Started, Failed, or Succeeded.</span></span>
- <span data-ttu-id="7ad45-128">**Evento iniciadas pelo**: também conhecido como Olá "autor da chamada."</span><span class="sxs-lookup"><span data-stu-id="7ad45-128">**Event initiated by**: Also known as hello "caller."</span></span> <span data-ttu-id="7ad45-129">endereço de correio eletrónico hello ou do Azure Active Directory identificador de Olá utilizador que executou a operação de Olá.</span><span class="sxs-lookup"><span data-stu-id="7ad45-129">hello email address or Azure Active Directory identifier of hello user who performed hello operation.</span></span>

>[!NOTE]
><span data-ttu-id="7ad45-130">Tem de especificar pelo menos, duas Olá precedente critérios do alerta, com a ser uma categoria de Olá.</span><span class="sxs-lookup"><span data-stu-id="7ad45-130">You must specify at least two of hello preceding criteria in your alert, with one being hello category.</span></span> <span data-ttu-id="7ad45-131">Não pode criar um alerta que activa sempre que é criado um evento nos registos de atividade Olá.</span><span class="sxs-lookup"><span data-stu-id="7ad45-131">You may not create an alert that activates every time an event is created in hello activity logs.</span></span>
>
>

<span data-ttu-id="7ad45-132">Quando um alerta de registo de atividade é ativado, utiliza uma ação de grupo toogenerate ações ou notificações.</span><span class="sxs-lookup"><span data-stu-id="7ad45-132">When an activity log alert is activated, it uses an action group toogenerate actions or notifications.</span></span> <span data-ttu-id="7ad45-133">Um grupo de ação é um conjunto reutilizável de recetores de notificação, tais como endereços de correio eletrónico, números de telefone de URLs de webhook ou SMS.</span><span class="sxs-lookup"><span data-stu-id="7ad45-133">An action group is a reusable set of notification receivers, such as email addresses, webhook URLs, or SMS phone numbers.</span></span> <span data-ttu-id="7ad45-134">recetores Olá podem ser referenciadas a partir de vários alertas toocentralize e os canais de notificação de grupo.</span><span class="sxs-lookup"><span data-stu-id="7ad45-134">hello receivers can be referenced from multiple alerts toocentralize and group your notification channels.</span></span> <span data-ttu-id="7ad45-135">Quando definir o alerta de registo de atividade, tem duas opções.</span><span class="sxs-lookup"><span data-stu-id="7ad45-135">When you define your activity log alert, you have two options.</span></span> <span data-ttu-id="7ad45-136">Pode:</span><span class="sxs-lookup"><span data-stu-id="7ad45-136">You can:</span></span>

* <span data-ttu-id="7ad45-137">Utilize um grupo de ação existente no seu alerta de registo de atividade.</span><span class="sxs-lookup"><span data-stu-id="7ad45-137">Use an existing action group in your activity log alert.</span></span> 
* <span data-ttu-id="7ad45-138">Crie um novo grupo de ação.</span><span class="sxs-lookup"><span data-stu-id="7ad45-138">Create a new action group.</span></span> 

<span data-ttu-id="7ad45-139">toolearn mais informações sobre grupos de ação, consulte [criar e gerir grupos de ação no portal do Azure de Olá](monitoring-action-groups.md).</span><span class="sxs-lookup"><span data-stu-id="7ad45-139">toolearn more about action groups, see [Create and manage action groups in hello Azure portal](monitoring-action-groups.md).</span></span>

<span data-ttu-id="7ad45-140">toolearn mais informações sobre notificações de estado de funcionamento do serviço, consulte [receber alertas de registo de atividade em notificações do Estado de funcionamento do serviço](monitoring-activity-log-alerts-on-service-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="7ad45-140">toolearn more about service health notifications, see [Receive activity log alerts on service health notifications](monitoring-activity-log-alerts-on-service-notifications.md).</span></span>

## <a name="create-an-alert-on-an-activity-log-event-with-a-new-action-group-by-using-hello-azure-portal"></a><span data-ttu-id="7ad45-141">Criar um alerta um evento de registo de atividade com um novo grupo de ação utilizando Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="7ad45-141">Create an alert on an activity log event with a new action group by using hello Azure portal</span></span>
1. <span data-ttu-id="7ad45-142">No Olá [portal](https://portal.azure.com), selecione **Monitor**.</span><span class="sxs-lookup"><span data-stu-id="7ad45-142">In hello [portal](https://portal.azure.com), select **Monitor**.</span></span>

    ![Olá serviço "Monitor de"](./media/monitoring-activity-log-alerts/home-monitor.png)
2. <span data-ttu-id="7ad45-144">No Olá **registo de atividade** secção, selecione **alertas**.</span><span class="sxs-lookup"><span data-stu-id="7ad45-144">In hello **Activity log** section, select **Alerts**.</span></span>

    ![separador de "Alertas" Olá](./media/monitoring-activity-log-alerts/alerts-blades.png)
3. <span data-ttu-id="7ad45-146">Selecione **Adicionar alerta de registo de atividade**e preencha os campos de Olá.</span><span class="sxs-lookup"><span data-stu-id="7ad45-146">Select **Add activity log alert**, and fill in hello fields.</span></span>

4. <span data-ttu-id="7ad45-147">Introduza um nome na Olá **nome de alerta de registo de atividade** caixa e selecione um **Descrição**.</span><span class="sxs-lookup"><span data-stu-id="7ad45-147">Enter a name in hello **Activity log alert name** box, and select a **Description**.</span></span>

    ![Olá comando "Adicionar o alerta de registo de atividade"](./media/monitoring-activity-log-alerts/add-activity-log-alert.png)

5. <span data-ttu-id="7ad45-149">Olá **subscrição** caixa autofills com a sua subscrição atual.</span><span class="sxs-lookup"><span data-stu-id="7ad45-149">hello **Subscription** box autofills with your current subscription.</span></span> <span data-ttu-id="7ad45-150">Esta subscrição está Olá um no qual o grupo ação Olá é guardado.</span><span class="sxs-lookup"><span data-stu-id="7ad45-150">This subscription is hello one in which hello action group is saved.</span></span> <span data-ttu-id="7ad45-151">recurso de alerta de Olá está implementado toothis subscrição e monitores atividade eventos de registo do mesmo.</span><span class="sxs-lookup"><span data-stu-id="7ad45-151">hello alert resource is deployed toothis subscription and monitors activity log events from it.</span></span>

    ![caixa de diálogo de "Adicionar o alerta de registo de atividade" Olá](./media/monitoring-activity-log-alerts/activity-log-alert-new-action-group.png)

6. <span data-ttu-id="7ad45-153">Selecione Olá **grupo de recursos** no qual Olá alerta recurso é criado.</span><span class="sxs-lookup"><span data-stu-id="7ad45-153">Select hello **Resource group** in which hello alert resource is created.</span></span> <span data-ttu-id="7ad45-154">Não se trata de grupo de recursos de Olá que é monitorizado por alerta Olá.</span><span class="sxs-lookup"><span data-stu-id="7ad45-154">This is not hello resource group that's monitored by hello alert.</span></span> <span data-ttu-id="7ad45-155">Em vez disso, é grupo de recursos de olá onde está localizado o recurso de alerta de Olá.</span><span class="sxs-lookup"><span data-stu-id="7ad45-155">Instead, it's hello resource group where hello alert resource is located.</span></span>

7. <span data-ttu-id="7ad45-156">Opcionalmente, selecione um **categoria de evento** toomodify Olá filtros adicionais que são apresentados.</span><span class="sxs-lookup"><span data-stu-id="7ad45-156">Optionally, select an **Event category** toomodify hello additional filters that are shown.</span></span> <span data-ttu-id="7ad45-157">Para eventos administrativos, filtros de Olá incluem **grupo de recursos**, **recursos**, **tipo de recurso**, **nome da operação**, **Nível**, **estado**, e **eventos iniciadas pelo**.</span><span class="sxs-lookup"><span data-stu-id="7ad45-157">For Administrative events, hello filters include **Resource group**, **Resource**, **Resource type**, **Operation name**, **Level**, **Status**, and **Event initiated by**.</span></span> <span data-ttu-id="7ad45-158">Estes valores identificam os eventos este alerta deve monitorizar.</span><span class="sxs-lookup"><span data-stu-id="7ad45-158">These values identify which events this alert should monitor.</span></span>

    >[!NOTE]
    ><span data-ttu-id="7ad45-159">Tem de especificar pelo menos uma das Olá precedente critérios do alerta.</span><span class="sxs-lookup"><span data-stu-id="7ad45-159">You must specify at least one of hello preceding criteria in your alert.</span></span> <span data-ttu-id="7ad45-160">Não pode criar um alerta que activa sempre que é criado um evento nos registos de atividade Olá.</span><span class="sxs-lookup"><span data-stu-id="7ad45-160">You may not create an alert that activates every time an event is created in hello activity logs.</span></span>
    >
    >

8. <span data-ttu-id="7ad45-161">Introduza um nome na Olá **nome do grupo de ação** caixa e introduza um nome na Olá **nome abreviado** caixa.</span><span class="sxs-lookup"><span data-stu-id="7ad45-161">Enter a name in hello **Action group name** box, and enter a name in hello **Short name** box.</span></span> <span data-ttu-id="7ad45-162">nome abreviado Olá é utilizado em vez de um nome de grupo ação completa, quando as notificações são enviadas através deste grupo.</span><span class="sxs-lookup"><span data-stu-id="7ad45-162">hello short name is used in place of a full action group name when notifications are sent using this group.</span></span>

9.  <span data-ttu-id="7ad45-163">Defina uma lista de ações, fornecendo a ação de Olá:</span><span class="sxs-lookup"><span data-stu-id="7ad45-163">Define a list of actions by providing hello action’s:</span></span>

    <span data-ttu-id="7ad45-164">a.</span><span class="sxs-lookup"><span data-stu-id="7ad45-164">a.</span></span> <span data-ttu-id="7ad45-165">**Nome**: introduza o nome da ação de Olá, alias ou identificador.</span><span class="sxs-lookup"><span data-stu-id="7ad45-165">**Name**: Enter hello action’s name, alias, or identifier.</span></span>

    <span data-ttu-id="7ad45-166">b.</span><span class="sxs-lookup"><span data-stu-id="7ad45-166">b.</span></span> <span data-ttu-id="7ad45-167">**Tipo de ação**: selecione SMS, o e-mail ou o webhook.</span><span class="sxs-lookup"><span data-stu-id="7ad45-167">**Action Type**: Select SMS, email, or webhook.</span></span>

    <span data-ttu-id="7ad45-168">c.</span><span class="sxs-lookup"><span data-stu-id="7ad45-168">c.</span></span> <span data-ttu-id="7ad45-169">**Detalhes**: com base no tipo de ação de Olá, introduza um número de telefone, o endereço de e-mail ou o webhook URI.</span><span class="sxs-lookup"><span data-stu-id="7ad45-169">**Details**: Based on hello action type, enter a phone number, email address, or webhook URI.</span></span>

10. <span data-ttu-id="7ad45-170">Selecione **OK** alerta de Olá toocreate.</span><span class="sxs-lookup"><span data-stu-id="7ad45-170">Select **OK** toocreate hello alert.</span></span>

<span data-ttu-id="7ad45-171">alerta de Olá demora alguns minutos toofully se propague e, em seguida, ficar ativo.</span><span class="sxs-lookup"><span data-stu-id="7ad45-171">hello alert takes a few minutes toofully propagate and then become active.</span></span> <span data-ttu-id="7ad45-172">Este é acionado quando novos eventos correspondem aos critérios de alerta de Olá.</span><span class="sxs-lookup"><span data-stu-id="7ad45-172">It triggers when new events match hello alert's criteria.</span></span>

<span data-ttu-id="7ad45-173">Para obter mais informações, consulte [esquema de webhook compreender Olá utilizada nos alertas do registo de atividade](monitoring-activity-log-alerts-webhook.md).</span><span class="sxs-lookup"><span data-stu-id="7ad45-173">For more information, see [Understand hello webhook schema used in activity log alerts](monitoring-activity-log-alerts-webhook.md).</span></span>

>[!NOTE]
><span data-ttu-id="7ad45-174">grupo definido nestes passos em ação Olá é reutilizável como um grupo de ação existente para todas as definições de alerta futuras.</span><span class="sxs-lookup"><span data-stu-id="7ad45-174">hello action group defined in these steps is reusable as an existing action group for all future alert definitions.</span></span>
>
>

## <a name="create-an-alert-on-an-activity-log-event-for-an-existing-action-group-by-using-hello-azure-portal"></a><span data-ttu-id="7ad45-175">Criar um alerta um evento de registo de atividade para um grupo de ação existente utilizando Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="7ad45-175">Create an alert on an activity log event for an existing action group by using hello Azure portal</span></span>
1. <span data-ttu-id="7ad45-176">Siga os passos 1 a 7 no Olá anterior secção toocreate o alerta de registo de atividade.</span><span class="sxs-lookup"><span data-stu-id="7ad45-176">Follow steps 1 through 7 in hello previous section toocreate your activity log alert.</span></span>

2. <span data-ttu-id="7ad45-177">Em **notificar através de**, selecione Olá **existentes** botão do grupo de ação.</span><span class="sxs-lookup"><span data-stu-id="7ad45-177">Under **Notify via**, select hello **Existing** action group button.</span></span> <span data-ttu-id="7ad45-178">Selecione um grupo de ação existente na lista de Olá.</span><span class="sxs-lookup"><span data-stu-id="7ad45-178">Select an existing action group from hello list.</span></span>

3. <span data-ttu-id="7ad45-179">Selecione **OK** alerta de Olá toocreate.</span><span class="sxs-lookup"><span data-stu-id="7ad45-179">Select **OK** toocreate hello alert.</span></span>

<span data-ttu-id="7ad45-180">alerta de Olá demora alguns minutos toofully se propague e, em seguida, ficar ativo.</span><span class="sxs-lookup"><span data-stu-id="7ad45-180">hello alert takes a few minutes toofully propagate and then become active.</span></span> <span data-ttu-id="7ad45-181">Este é acionado quando novos eventos correspondem aos critérios de alerta de Olá.</span><span class="sxs-lookup"><span data-stu-id="7ad45-181">It triggers when new events match hello alert's criteria.</span></span>

## <a name="manage-your-alerts"></a><span data-ttu-id="7ad45-182">Gerir os alertas</span><span class="sxs-lookup"><span data-stu-id="7ad45-182">Manage your alerts</span></span>

<span data-ttu-id="7ad45-183">Depois de criar um alerta, é visível na secção de alertas de Olá do painel de Monitor de Olá.</span><span class="sxs-lookup"><span data-stu-id="7ad45-183">After you create an alert, it's visible in hello Alerts section of hello Monitor blade.</span></span> <span data-ttu-id="7ad45-184">Selecione o alerta de Olá que pretende toomanage para:</span><span class="sxs-lookup"><span data-stu-id="7ad45-184">Select hello alert you want toomanage to:</span></span>

* <span data-ttu-id="7ad45-185">Editá-lo.</span><span class="sxs-lookup"><span data-stu-id="7ad45-185">Edit it.</span></span>
* <span data-ttu-id="7ad45-186">Elimine-o.</span><span class="sxs-lookup"><span data-stu-id="7ad45-186">Delete it.</span></span>
* <span data-ttu-id="7ad45-187">Desactivar ou activar, se pretender parar de tootemporarily ou retomar a receção de notificações de alerta de Olá.</span><span class="sxs-lookup"><span data-stu-id="7ad45-187">Disable or enable it, if you want tootemporarily stop or resume receiving notifications for hello alert.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7ad45-188">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="7ad45-188">Next steps</span></span>
- <span data-ttu-id="7ad45-189">Obter um [descrição geral dos alertas](monitoring-overview-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="7ad45-189">Get an [overview of alerts](monitoring-overview-alerts.md).</span></span>
- <span data-ttu-id="7ad45-190">Saiba mais sobre [limitação de taxa de notificação](monitoring-alerts-rate-limiting.md).</span><span class="sxs-lookup"><span data-stu-id="7ad45-190">Learn about [notification rate limiting](monitoring-alerts-rate-limiting.md).</span></span>
- <span data-ttu-id="7ad45-191">Olá revisão [esquema de webhook alerta de registo de atividade](monitoring-activity-log-alerts-webhook.md).</span><span class="sxs-lookup"><span data-stu-id="7ad45-191">Review hello [activity log alert webhook schema](monitoring-activity-log-alerts-webhook.md).</span></span>
- <span data-ttu-id="7ad45-192">Saiba mais sobre [grupos ação](monitoring-action-groups.md).</span><span class="sxs-lookup"><span data-stu-id="7ad45-192">Learn more about [action groups](monitoring-action-groups.md).</span></span>  
- <span data-ttu-id="7ad45-193">Saiba mais sobre [notificações de estado de funcionamento do serviço](monitoring-service-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="7ad45-193">Learn about [service health notifications](monitoring-service-notifications.md).</span></span>
- <span data-ttu-id="7ad45-194">Criar um [toomonitor alerta de registo de atividade, todas as operações de motor de dimensionamento automático na sua subscrição](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-alert).</span><span class="sxs-lookup"><span data-stu-id="7ad45-194">Create an [activity log alert toomonitor all autoscale engine operations on your subscription](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-alert).</span></span>
- <span data-ttu-id="7ad45-195">Criar um [toomonitor alerta de registo de atividade, todas as operações de escala-na/escalável de dimensionamento automático falhou na sua subscrição](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-failed-alert).</span><span class="sxs-lookup"><span data-stu-id="7ad45-195">Create an [activity log alert toomonitor all failed autoscale scale-in/scale-out operations on your subscription](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-failed-alert).</span></span>
