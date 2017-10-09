---
title: "aaaCreate e gerir grupos de ação na Olá portal do Azure | Microsoft Docs"
description: "Saiba como toocreate e gerir grupos de ação na Olá portal do Azure."
author: anirudhcavale
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
ms.date: 05/15/2017
ms.author: ancav
ms.openlocfilehash: 97e0b22bea7787fff6856f895a7e6256c177efd9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-action-groups-in-hello-azure-portal"></a><span data-ttu-id="1f0a3-103">Criar e gerir grupos de ação na Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="1f0a3-103">Create and manage action groups in hello Azure portal</span></span>
## <a name="overview"></a><span data-ttu-id="1f0a3-104">Descrição geral</span><span class="sxs-lookup"><span data-stu-id="1f0a3-104">Overview</span></span> ##
<span data-ttu-id="1f0a3-105">Este artigo mostra como toocreate e gerir grupos de ação na Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="1f0a3-105">This article shows you how toocreate and manage action groups in hello Azure portal.</span></span>

<span data-ttu-id="1f0a3-106">Pode configurar uma lista de ações com grupos de ação.</span><span class="sxs-lookup"><span data-stu-id="1f0a3-106">You can configure a list of actions with action groups.</span></span> <span data-ttu-id="1f0a3-107">Estes grupos, em seguida, podem ser utilizados quando definir alertas do registo de atividade.</span><span class="sxs-lookup"><span data-stu-id="1f0a3-107">These groups then can be used when you define activity log alerts.</span></span> <span data-ttu-id="1f0a3-108">Estes grupos, em seguida, podem ser reutilizados por cada alerta de registo de atividade que definir, garantindo que Olá mesmas ações efetuadas sempre que é acionada o alerta de registo de atividade Olá.</span><span class="sxs-lookup"><span data-stu-id="1f0a3-108">These groups can then be reused by each activity log alert you define, ensuring that hello same actions are taken each time hello activity log alert is triggered.</span></span>

<span data-ttu-id="1f0a3-109">Um grupo de ação pode ter segurança too10 de cada tipo de ação.</span><span class="sxs-lookup"><span data-stu-id="1f0a3-109">An action group can have up too10 of each action type.</span></span> <span data-ttu-id="1f0a3-110">Cada ação é constituída por Olá seguintes propriedades:</span><span class="sxs-lookup"><span data-stu-id="1f0a3-110">Each action is made up of hello following properties:</span></span>

* <span data-ttu-id="1f0a3-111">**Nome**: um identificador exclusivo dentro do grupo de ação de Olá.</span><span class="sxs-lookup"><span data-stu-id="1f0a3-111">**Name**: A unique identifier within hello action group.</span></span>  
* <span data-ttu-id="1f0a3-112">**Tipo de ação**: enviar um SMS, envie um e-mail ou chamar um webhook.</span><span class="sxs-lookup"><span data-stu-id="1f0a3-112">**Action type**: Send an SMS, send an email, or call a webhook.</span></span>  
* <span data-ttu-id="1f0a3-113">**Detalhes**: Olá correspondente número de telefone, o endereço de e-mail ou o webhook URI.</span><span class="sxs-lookup"><span data-stu-id="1f0a3-113">**Details**: hello corresponding phone number, email address, or webhook URI.</span></span>

<span data-ttu-id="1f0a3-114">Para obter informações sobre como toouse do Azure Resource Manager modelos tooconfigure ação grupos, consulte [modelos de Gestor de recursos do grupo de ação](monitoring-create-action-group-with-resource-manager-template.md).</span><span class="sxs-lookup"><span data-stu-id="1f0a3-114">For information on how toouse Azure Resource Manager templates tooconfigure action groups, see [Action group Resource Manager templates](monitoring-create-action-group-with-resource-manager-template.md).</span></span>

## <a name="create-an-action-group-by-using-hello-azure-portal"></a><span data-ttu-id="1f0a3-115">Criar um grupo de ação utilizando Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="1f0a3-115">Create an action group by using hello Azure portal</span></span> ##
1. <span data-ttu-id="1f0a3-116">No Olá [portal](https://portal.azure.com), selecione **Monitor**.</span><span class="sxs-lookup"><span data-stu-id="1f0a3-116">In hello [portal](https://portal.azure.com), select **Monitor**.</span></span> <span data-ttu-id="1f0a3-117">Olá **Monitor** painel consolida todas as suas monitorização definições e dados de uma vista.</span><span class="sxs-lookup"><span data-stu-id="1f0a3-117">hello **Monitor** blade consolidates all your monitoring settings and data in one view.</span></span>

    ![Olá serviço "Monitor de"](./media/monitoring-action-groups/home-monitor.png)
2. <span data-ttu-id="1f0a3-119">No Olá **registo de atividade** secção, selecione **grupos ação**.</span><span class="sxs-lookup"><span data-stu-id="1f0a3-119">In hello **Activity log** section, select **Action groups**.</span></span>

    ![separador de "Grupos de ação" Olá](./media/monitoring-action-groups/action-groups-blade.png)
3. <span data-ttu-id="1f0a3-121">Selecione **adicionar grupo de ação**e preencha os campos de Olá.</span><span class="sxs-lookup"><span data-stu-id="1f0a3-121">Select **Add action group**, and fill in hello fields.</span></span>

    ![Olá comando "Adicionar grupo de ação"](./media/monitoring-action-groups/add-action-group.png)
4. <span data-ttu-id="1f0a3-123">Introduza um nome na Olá **nome do grupo de ação** caixa e introduza um nome na Olá **nome abreviado** caixa.</span><span class="sxs-lookup"><span data-stu-id="1f0a3-123">Enter a name in hello **Action group name** box, and enter a name in hello **Short name** box.</span></span> <span data-ttu-id="1f0a3-124">nome abreviado Olá é utilizado em vez de um nome de grupo ação completa, quando as notificações são enviadas através deste grupo.</span><span class="sxs-lookup"><span data-stu-id="1f0a3-124">hello short name is used in place of a full action group name when notifications are sent using this group.</span></span>

      ![caixa de diálogo Olá adicionar ação grupo"](./media/monitoring-action-groups/action-group-define.png)

5. <span data-ttu-id="1f0a3-126">Olá **subscrição** caixa autofills com a sua subscrição atual.</span><span class="sxs-lookup"><span data-stu-id="1f0a3-126">hello **Subscription** box autofills with your current subscription.</span></span> <span data-ttu-id="1f0a3-127">Esta subscrição está Olá um no qual o grupo ação Olá é guardado.</span><span class="sxs-lookup"><span data-stu-id="1f0a3-127">This subscription is hello one in which hello action group is saved.</span></span>

6. <span data-ttu-id="1f0a3-128">Selecione Olá **grupo de recursos** a ação de Olá grupo é guardado.</span><span class="sxs-lookup"><span data-stu-id="1f0a3-128">Select hello **Resource group** in which hello action group is saved.</span></span>

7. <span data-ttu-id="1f0a3-129">Defina uma lista de ações, fornecendo cada ação:</span><span class="sxs-lookup"><span data-stu-id="1f0a3-129">Define a list of actions by providing each action's:</span></span>

    <span data-ttu-id="1f0a3-130">a.</span><span class="sxs-lookup"><span data-stu-id="1f0a3-130">a.</span></span> <span data-ttu-id="1f0a3-131">**Nome**: introduza um identificador exclusivo para esta ação.</span><span class="sxs-lookup"><span data-stu-id="1f0a3-131">**Name**: Enter a unique identifier for this action.</span></span>

    <span data-ttu-id="1f0a3-132">b.</span><span class="sxs-lookup"><span data-stu-id="1f0a3-132">b.</span></span> <span data-ttu-id="1f0a3-133">**Tipo de ação**: selecione SMS, o e-mail ou o webhook.</span><span class="sxs-lookup"><span data-stu-id="1f0a3-133">**Action Type**: Select SMS, email, or webhook.</span></span>

    <span data-ttu-id="1f0a3-134">c.</span><span class="sxs-lookup"><span data-stu-id="1f0a3-134">c.</span></span> <span data-ttu-id="1f0a3-135">**Detalhes**: com base no tipo de ação de Olá, introduza um número de telefone, o endereço de e-mail ou o webhook URI.</span><span class="sxs-lookup"><span data-stu-id="1f0a3-135">**Details**: Based on hello action type, enter a phone number, email address, or webhook URI.</span></span>

8. <span data-ttu-id="1f0a3-136">Selecione **OK** grupo de ação de Olá toocreate.</span><span class="sxs-lookup"><span data-stu-id="1f0a3-136">Select **OK** toocreate hello action group.</span></span>

## <a name="manage-your-action-groups"></a><span data-ttu-id="1f0a3-137">Gerir os grupos de ação</span><span class="sxs-lookup"><span data-stu-id="1f0a3-137">Manage your action groups</span></span> ##
<span data-ttu-id="1f0a3-138">Depois de criar um grupo de ação, é visível na Olá **grupos ação** secção Olá **Monitor** painel.</span><span class="sxs-lookup"><span data-stu-id="1f0a3-138">After you create an action group, it's visible in hello **Action groups** section of hello **Monitor** blade.</span></span> <span data-ttu-id="1f0a3-139">Selecione o grupo de ação de Olá que pretende toomanage para:</span><span class="sxs-lookup"><span data-stu-id="1f0a3-139">Select hello action group you want toomanage to:</span></span>

* <span data-ttu-id="1f0a3-140">Adicionar, editar ou remover as ações.</span><span class="sxs-lookup"><span data-stu-id="1f0a3-140">Add, edit, or remove actions.</span></span>
* <span data-ttu-id="1f0a3-141">Elimine grupo de ação de Olá.</span><span class="sxs-lookup"><span data-stu-id="1f0a3-141">Delete hello action group.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1f0a3-142">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="1f0a3-142">Next steps</span></span> ##
* <span data-ttu-id="1f0a3-143">Saiba mais sobre [SMS alerta comportamento](monitoring-sms-alert-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="1f0a3-143">Learn more about [SMS alert behavior](monitoring-sms-alert-behavior.md).</span></span>  
* <span data-ttu-id="1f0a3-144">Obter um [compreensão do esquema de webhook alerta de registo de atividade Olá](monitoring-activity-log-alerts-webhook.md).</span><span class="sxs-lookup"><span data-stu-id="1f0a3-144">Gain an [understanding of hello activity log alert webhook schema](monitoring-activity-log-alerts-webhook.md).</span></span>  
* <span data-ttu-id="1f0a3-145">Saiba mais sobre [limitação de taxa](monitoring-alerts-rate-limiting.md) em alertas.</span><span class="sxs-lookup"><span data-stu-id="1f0a3-145">Learn more about [rate limiting](monitoring-alerts-rate-limiting.md) on alerts.</span></span> 
* <span data-ttu-id="1f0a3-146">Obter um [descrição geral dos alertas de registo de atividade](monitoring-overview-alerts.md)e saber como tooreceive alertas.</span><span class="sxs-lookup"><span data-stu-id="1f0a3-146">Get an [overview of activity log alerts](monitoring-overview-alerts.md), and learn how tooreceive alerts.</span></span>  
* <span data-ttu-id="1f0a3-147">Saiba como demasiado[configurar alertas sempre que uma notificação de estado de funcionamento do serviço é publicada](monitoring-activity-log-alerts-on-service-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="1f0a3-147">Learn how too[configure alerts whenever a service health notification is posted](monitoring-activity-log-alerts-on-service-notifications.md).</span></span>
