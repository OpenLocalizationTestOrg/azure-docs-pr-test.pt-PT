---
title: "ação de consulta de Olá aaaAdd nas logic apps | Microsoft Docs"
description: "Descrição geral da ação de consulta Olá para efetuar ações como filtro matriz."
services: 
documentationcenter: 
author: jeffhollan
manager: erikre
editor: 
tags: connectors
ms.assetid: 34e702c7-f9e5-4885-9266-fc7404adecfe
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/20/2016
ms.author: jehollan
ms.openlocfilehash: 3d4be901e7e6bf1b644057648930667ab34f2124
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-query-action"></a><span data-ttu-id="0c513-103">Introdução à ação de consulta Olá</span><span class="sxs-lookup"><span data-stu-id="0c513-103">Get started with hello query action</span></span>
<span data-ttu-id="0c513-104">Utilizando a ação de consulta Olá, pode trabalhar com lotes e matrizes tooaccomplish fluxos de trabalho para:</span><span class="sxs-lookup"><span data-stu-id="0c513-104">By using hello query action, you can work with batches and arrays tooaccomplish workflows to:</span></span>

* <span data-ttu-id="0c513-105">Crie uma tarefa para todos os registos de alta prioridade a partir de uma base de dados.</span><span class="sxs-lookup"><span data-stu-id="0c513-105">Create a task for all high-priority records from a database.</span></span>
* <span data-ttu-id="0c513-106">Guarde anexos de PDF todas as mensagens de correio eletrónico para um blob do Azure.</span><span class="sxs-lookup"><span data-stu-id="0c513-106">Save all PDF attachments for emails into an Azure blob.</span></span>

<span data-ttu-id="0c513-107">tooget iniciado utilizando a ação de consulta Olá numa aplicação lógica, consulte [criar uma aplicação lógica](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="0c513-107">tooget started using hello query action in a logic app, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="use-hello-query-action"></a><span data-ttu-id="0c513-108">Utilize a ação de consulta Olá</span><span class="sxs-lookup"><span data-stu-id="0c513-108">Use hello query action</span></span>
<span data-ttu-id="0c513-109">Uma ação é uma operação que é efetuada pelo fluxo de trabalho de Olá que está definido uma aplicação lógica.</span><span class="sxs-lookup"><span data-stu-id="0c513-109">An action is an operation that is carried out by hello workflow that is defined in a logic app.</span></span> <span data-ttu-id="0c513-110">[Saiba mais sobre as ações](connectors-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0c513-110">[Learn more about actions](connectors-overview.md).</span></span>  

<span data-ttu-id="0c513-111">ação de consulta Olá tem atualmente uma operação, denominada matriz de filtro de Olá, que é exposto no estruturador de Olá.</span><span class="sxs-lookup"><span data-stu-id="0c513-111">hello query action currently has one operation, called hello filter array, that is exposed in hello designer.</span></span> <span data-ttu-id="0c513-112">Isto permite-lhe tooquery uma matriz e devolver um conjunto de resultados filtrados.</span><span class="sxs-lookup"><span data-stu-id="0c513-112">This allows you tooquery an array and return a set of filtered results.</span></span>

<span data-ttu-id="0c513-113">Eis como pode adicioná-lo numa aplicação lógica:</span><span class="sxs-lookup"><span data-stu-id="0c513-113">Here's how you can add it in a logic app:</span></span>

1. <span data-ttu-id="0c513-114">Selecione Olá **novo passo** botão.</span><span class="sxs-lookup"><span data-stu-id="0c513-114">Select hello **New Step** button.</span></span>
2. <span data-ttu-id="0c513-115">Escolha **adicionar uma ação**.</span><span class="sxs-lookup"><span data-stu-id="0c513-115">Choose **Add an action**.</span></span>
3. <span data-ttu-id="0c513-116">Na caixa de pesquisa de ação de Olá, escreva **filtro** Olá toolist **matriz de filtro** ação.</span><span class="sxs-lookup"><span data-stu-id="0c513-116">In hello action search box, type **filter** toolist hello **Filter array** action.</span></span>
   
    ![Selecione a ação de consulta Olá](./media/connectors-native-query/using-action-1.png)
4. <span data-ttu-id="0c513-118">Selecione um toofilter de matriz.</span><span class="sxs-lookup"><span data-stu-id="0c513-118">Select an array toofilter.</span></span> <span data-ttu-id="0c513-119">(hello seguinte captura de ecrã mostra matriz Olá de resultados a partir de uma pesquisa do Twitter.)</span><span class="sxs-lookup"><span data-stu-id="0c513-119">(hello following screenshot shows hello array of results from a Twitter search.)</span></span>
5. <span data-ttu-id="0c513-120">Crie uma condição tooevaluate em cada item.</span><span class="sxs-lookup"><span data-stu-id="0c513-120">Create a condition tooevaluate on each item.</span></span> <span data-ttu-id="0c513-121">(Olá seguinte captura de ecrã filtra tweets dos utilizadores que tenham mais do que 100 followers.)</span><span class="sxs-lookup"><span data-stu-id="0c513-121">(hello following screenshot filters tweets from users who have more than 100 followers.)</span></span>
   
    ![Ação de consulta Olá concluída](./media/connectors-native-query/using-action-2.png)
   
    <span data-ttu-id="0c513-123">ação de Olá será saída uma matriz nova que contém apenas os resultados que são cumpridos os requisitos de filtro de Olá.</span><span class="sxs-lookup"><span data-stu-id="0c513-123">hello action will output a new array that contains only results that met hello filter requirements.</span></span>
6. <span data-ttu-id="0c513-124">Clique em canto superior esquerdo de Olá de Olá toosave de barra de ferramentas e a lógica aplicação será ambos os guardar e publicar (ativar).</span><span class="sxs-lookup"><span data-stu-id="0c513-124">Click hello upper-left corner of hello toolbar toosave, and your logic app will both save and publish (activate).</span></span>

## <a name="query-action"></a><span data-ttu-id="0c513-125">Ação de consulta</span><span class="sxs-lookup"><span data-stu-id="0c513-125">Query action</span></span>
<span data-ttu-id="0c513-126">Seguem-se detalhes Olá para a ação de Olá que suporte este conector.</span><span class="sxs-lookup"><span data-stu-id="0c513-126">Here are hello details for hello action that this connector supports.</span></span> <span data-ttu-id="0c513-127">conector de Olá tem uma ação possíveis.</span><span class="sxs-lookup"><span data-stu-id="0c513-127">hello connector has one possible action.</span></span>

| <span data-ttu-id="0c513-128">Ação</span><span class="sxs-lookup"><span data-stu-id="0c513-128">Action</span></span> | <span data-ttu-id="0c513-129">Descrição</span><span class="sxs-lookup"><span data-stu-id="0c513-129">Description</span></span> |
| --- | --- |
| <span data-ttu-id="0c513-130">Matriz de filtro</span><span class="sxs-lookup"><span data-stu-id="0c513-130">Filter array</span></span> |<span data-ttu-id="0c513-131">Avalia uma condição para cada item numa matriz e devolve resultados Olá</span><span class="sxs-lookup"><span data-stu-id="0c513-131">Evaluates a condition for each item in an array and returns hello results</span></span> |

## <a name="action-details"></a><span data-ttu-id="0c513-132">Detalhes de ação</span><span class="sxs-lookup"><span data-stu-id="0c513-132">Action details</span></span>
<span data-ttu-id="0c513-133">ação de consulta Olá vem com uma ação possíveis.</span><span class="sxs-lookup"><span data-stu-id="0c513-133">hello query action comes with one possible action.</span></span> <span data-ttu-id="0c513-134">Olá tabelas seguintes descrevem Olá necessários e opcionais campos de entrada para a ação de Olá e detalhes saída correspondente Olá associadas através da ação de Olá.</span><span class="sxs-lookup"><span data-stu-id="0c513-134">hello following tables describe hello required and optional input fields for hello action and hello corresponding output details that are associated with using hello action.</span></span>

### <a name="filter-array"></a><span data-ttu-id="0c513-135">Matriz de filtro</span><span class="sxs-lookup"><span data-stu-id="0c513-135">Filter array</span></span>
<span data-ttu-id="0c513-136">Olá seguem-se os campos de entrada para a ação de Olá, o que faz um pedido de saída de HTTP.</span><span class="sxs-lookup"><span data-stu-id="0c513-136">hello following are input fields for hello action, which makes an HTTP outbound request.</span></span>
<span data-ttu-id="0c513-137">A * significa que é um campo obrigatório.</span><span class="sxs-lookup"><span data-stu-id="0c513-137">A * means that it is a required field.</span></span>

| <span data-ttu-id="0c513-138">Nome a apresentar</span><span class="sxs-lookup"><span data-stu-id="0c513-138">Display name</span></span> | <span data-ttu-id="0c513-139">Nome da propriedade</span><span class="sxs-lookup"><span data-stu-id="0c513-139">Property name</span></span> | <span data-ttu-id="0c513-140">Descrição</span><span class="sxs-lookup"><span data-stu-id="0c513-140">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0c513-141">De *</span><span class="sxs-lookup"><span data-stu-id="0c513-141">From*</span></span> |<span data-ttu-id="0c513-142">Do</span><span class="sxs-lookup"><span data-stu-id="0c513-142">from</span></span> |<span data-ttu-id="0c513-143">Olá matriz toofilter</span><span class="sxs-lookup"><span data-stu-id="0c513-143">hello array toofilter</span></span> |
| <span data-ttu-id="0c513-144">Condição *</span><span class="sxs-lookup"><span data-stu-id="0c513-144">Condition*</span></span> |<span data-ttu-id="0c513-145">onde</span><span class="sxs-lookup"><span data-stu-id="0c513-145">where</span></span> |<span data-ttu-id="0c513-146">Olá condição tooevaluate para cada item</span><span class="sxs-lookup"><span data-stu-id="0c513-146">hello condition tooevaluate for each item</span></span> |

<br>

### <a name="output-details"></a><span data-ttu-id="0c513-147">Detalhes de saída</span><span class="sxs-lookup"><span data-stu-id="0c513-147">Output details</span></span>
<span data-ttu-id="0c513-148">Olá seguem-se detalhes de saída para Olá resposta de HTTP.</span><span class="sxs-lookup"><span data-stu-id="0c513-148">hello following are output details for hello HTTP response.</span></span>

| <span data-ttu-id="0c513-149">Nome da propriedade</span><span class="sxs-lookup"><span data-stu-id="0c513-149">Property name</span></span> | <span data-ttu-id="0c513-150">Tipo de dados</span><span class="sxs-lookup"><span data-stu-id="0c513-150">Data type</span></span> | <span data-ttu-id="0c513-151">Descrição</span><span class="sxs-lookup"><span data-stu-id="0c513-151">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0c513-152">Matriz filtrado</span><span class="sxs-lookup"><span data-stu-id="0c513-152">Filtered array</span></span> |<span data-ttu-id="0c513-153">Matriz</span><span class="sxs-lookup"><span data-stu-id="0c513-153">array</span></span> |<span data-ttu-id="0c513-154">Uma matriz que contenha um objeto para cada resultado filtrado</span><span class="sxs-lookup"><span data-stu-id="0c513-154">An array that contains an object for each filtered result</span></span> |

## <a name="next-steps"></a><span data-ttu-id="0c513-155">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="0c513-155">Next steps</span></span>
<span data-ttu-id="0c513-156">Agora, experimente a plataforma de Olá e [criar uma aplicação lógica](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="0c513-156">Now, try out hello platform and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="0c513-157">Pode explorar Olá outros conectores disponíveis em aplicações lógicas observando nosso [lista APIs](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="0c513-157">You can explore hello other available connectors in logic apps by looking at our [APIs list](apis-list.md).</span></span>

