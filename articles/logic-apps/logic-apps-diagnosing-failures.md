---
title: falhas de aaaDiagnose - Azure Logic Apps | Microsoft Docs
description: "Comuns toounderstand de formas em que as logic apps estão a falhar"
services: logic-apps
documentationcenter: .net,nodejs,java
author: jeffhollan
manager: anneta
editor: 
ms.assetid: a6727ebd-39bd-4298-9e68-2ae98738576e
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 10/18/2016
ms.author: LADocs; jehollan
ms.openlocfilehash: 46d318625820034c95e6df3a71ab84c58f076dd7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="diagnose-logic-app-failures"></a><span data-ttu-id="9d4e1-103">Diagnosticar falhas de aplicação lógica</span><span class="sxs-lookup"><span data-stu-id="9d4e1-103">Diagnose logic app failures</span></span>
<span data-ttu-id="9d4e1-104">Se surgirem problemas ou falhas com as logic apps, existem alguns abordagens podem ajudar a compreender melhor onde são feitos falhas Olá.</span><span class="sxs-lookup"><span data-stu-id="9d4e1-104">If you experience issues or failures with your logic apps, there are a few approaches can help you better understand where hello failures are coming from.</span></span>  

## <a name="azure-portal-tools"></a><span data-ttu-id="9d4e1-105">Ferramentas de portais do Azure</span><span class="sxs-lookup"><span data-stu-id="9d4e1-105">Azure portal tools</span></span>
<span data-ttu-id="9d4e1-106">Olá portal do Azure fornece várias ferramentas toodiagnose cada aplicação lógica em cada passo.</span><span class="sxs-lookup"><span data-stu-id="9d4e1-106">hello Azure portal provides many tools toodiagnose each logic app at each step.</span></span>

### <a name="trigger-history"></a><span data-ttu-id="9d4e1-107">Histórico de Acionador</span><span class="sxs-lookup"><span data-stu-id="9d4e1-107">Trigger history</span></span>

<span data-ttu-id="9d4e1-108">Cada aplicação lógica tem pelo menos um acionador.</span><span class="sxs-lookup"><span data-stu-id="9d4e1-108">Each logic app has at least one trigger.</span></span> <span data-ttu-id="9d4e1-109">Se reparar em que as aplicações não são acionando, procure primeiro no histórico de Acionador de Olá para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="9d4e1-109">If you notice that apps aren't firing, look first at hello trigger history for more information.</span></span> <span data-ttu-id="9d4e1-110">Pode aceder ao histórico de Acionador de Olá no painel principal do Olá lógica app'ss.</span><span class="sxs-lookup"><span data-stu-id="9d4e1-110">You can access hello trigger history on hello logic app'ss main blade.</span></span>

![Localizar o histórico de Acionador de Olá][1]

<span data-ttu-id="9d4e1-112">histórico de Acionador de Olá apresenta uma lista de todas as tentativas de Acionador que efetuou a sua aplicação lógica.</span><span class="sxs-lookup"><span data-stu-id="9d4e1-112">hello trigger history lists all trigger attempts that your logic app made.</span></span> <span data-ttu-id="9d4e1-113">Pode clicar em cada toodrill de tentativa de Acionador para detalhes de Olá, especificamente, as entradas ou saídas Olá tentativa de Acionador gerado.</span><span class="sxs-lookup"><span data-stu-id="9d4e1-113">You can click each trigger attempt toodrill into hello details, specifically, any inputs or outputs that hello trigger attempt generated.</span></span> <span data-ttu-id="9d4e1-114">Se encontrar acionadores falhadas, selecione a tentativa de Acionador de Olá e escolha Olá **saídas** ligação tooreview qualquer erro gerado mensagens, por exemplo, as credenciais de FTP que não são válidas.</span><span class="sxs-lookup"><span data-stu-id="9d4e1-114">If you find failed triggers, select hello trigger attempt and choose hello **Outputs** link tooreview any generated error messages, for example, for FTP credentials that aren't valid.</span></span>

<span data-ttu-id="9d4e1-115">Olá Estados diferentes, que poderá ver são:</span><span class="sxs-lookup"><span data-stu-id="9d4e1-115">hello different statuses you might see are:</span></span>

* <span data-ttu-id="9d4e1-116">**Ignorado**.</span><span class="sxs-lookup"><span data-stu-id="9d4e1-116">**Skipped**.</span></span> <span data-ttu-id="9d4e1-117">ponto final de Olá foi consultado toocheck para dados e recebeu uma resposta que não estavam disponíveis dados.</span><span class="sxs-lookup"><span data-stu-id="9d4e1-117">hello endpoint was polled toocheck for data and received a response that no data was available.</span></span>
* <span data-ttu-id="9d4e1-118">**Foi concluída com êxito**.</span><span class="sxs-lookup"><span data-stu-id="9d4e1-118">**Succeeded**.</span></span> <span data-ttu-id="9d4e1-119">acionador Olá recebeu uma resposta que estavam disponíveis dados.</span><span class="sxs-lookup"><span data-stu-id="9d4e1-119">hello trigger received a response that data was available.</span></span> <span data-ttu-id="9d4e1-120">Este estado poderá resultar de um acionador manual, um acionador de recorrência ou um acionador de consulta.</span><span class="sxs-lookup"><span data-stu-id="9d4e1-120">This status might result from a manual trigger, a recurrence trigger, or a polling trigger.</span></span> <span data-ttu-id="9d4e1-121">Este estado é normalmente acompanhado Olá **Fired** Estado, mas poderá não ser se tiver uma condição ou o comando SplitOn na vista de código que não foi satisfeita.</span><span class="sxs-lookup"><span data-stu-id="9d4e1-121">This status is usually accompanied by hello **Fired** status, but might not be if you have a condition or SplitOn command in code view that wasn't satisfied.</span></span>
* <span data-ttu-id="9d4e1-122">**Não foi possível**.</span><span class="sxs-lookup"><span data-stu-id="9d4e1-122">**Failed**.</span></span> <span data-ttu-id="9d4e1-123">Foi gerado um erro.</span><span class="sxs-lookup"><span data-stu-id="9d4e1-123">An error was generated.</span></span>

#### <a name="start-a-trigger-manually"></a><span data-ttu-id="9d4e1-124">Inicie manualmente um acionador</span><span class="sxs-lookup"><span data-stu-id="9d4e1-124">Start a trigger manually</span></span>

<span data-ttu-id="9d4e1-125">Se pretender toocheck de aplicação de lógica de Olá para um acionador disponível imediatamente sem aguardar a próxima periodicidade de Olá, clique em **selecione acionador** no painel principal de Olá tooforce uma verificação.</span><span class="sxs-lookup"><span data-stu-id="9d4e1-125">If you want hello logic app toocheck for an available trigger immediately without waiting for hello next recurrence, click **Select Trigger** on hello main blade tooforce a check.</span></span> <span data-ttu-id="9d4e1-126">Por exemplo, ao clicar nesta ligação com um acionador Dropbox faz com que Olá fluxo de trabalho tooimmediately consulta Dropbox para novos ficheiros.</span><span class="sxs-lookup"><span data-stu-id="9d4e1-126">For example, clicking this link with a Dropbox trigger causes hello workflow tooimmediately poll Dropbox for new files.</span></span>

### <a name="run-history"></a><span data-ttu-id="9d4e1-127">histórico de execução</span><span class="sxs-lookup"><span data-stu-id="9d4e1-127">Run history</span></span>

<span data-ttu-id="9d4e1-128">Cada acionador fired resulta numa execução.</span><span class="sxs-lookup"><span data-stu-id="9d4e1-128">Every fired trigger results in a run.</span></span> <span data-ttu-id="9d4e1-129">Pode aceder a informações de execução a partir do painel principal Olá, que contém vários detalhes que podem ajudar a compreender o que aconteceu durante o fluxo de trabalho Olá.</span><span class="sxs-lookup"><span data-stu-id="9d4e1-129">You can access run information from hello main blade, which contains many details that can help you understand what happened during hello workflow.</span></span>

![Localizar Olá histórico de execução][2]

<span data-ttu-id="9d4e1-131">Uma execução apresentará um dos seguintes Estados de Olá:</span><span class="sxs-lookup"><span data-stu-id="9d4e1-131">A run displays one of hello following statuses:</span></span>

* <span data-ttu-id="9d4e1-132">**Foi concluída com êxito**.</span><span class="sxs-lookup"><span data-stu-id="9d4e1-132">**Succeeded**.</span></span> <span data-ttu-id="9d4e1-133">Todas as ações com êxito.</span><span class="sxs-lookup"><span data-stu-id="9d4e1-133">All actions succeeded.</span></span> <span data-ttu-id="9d4e1-134">Se Ocorreu uma falha, falha de que foi processada por uma ação que ocorreram mais tarde no fluxo de trabalho Olá.</span><span class="sxs-lookup"><span data-stu-id="9d4e1-134">If a failure happened, that failure was handled by an action that occurred later in hello workflow.</span></span> <span data-ttu-id="9d4e1-135">Ou seja, falha de Olá foi processada por uma ação que foi definida toorun após uma falha na ação.</span><span class="sxs-lookup"><span data-stu-id="9d4e1-135">That is, hello failure was handled by an action that was set toorun after a failed action.</span></span>
* <span data-ttu-id="9d4e1-136">**Não foi possível**.</span><span class="sxs-lookup"><span data-stu-id="9d4e1-136">**Failed**.</span></span> <span data-ttu-id="9d4e1-137">Pelo menos uma ação tido uma falha que não foi processada por uma ação mais tarde no Olá fluxo de trabalho.</span><span class="sxs-lookup"><span data-stu-id="9d4e1-137">At least one action had a failure that was not handled by an action later in hello workflow.</span></span>
* <span data-ttu-id="9d4e1-138">**Cancelada**.</span><span class="sxs-lookup"><span data-stu-id="9d4e1-138">**Cancelled**.</span></span> <span data-ttu-id="9d4e1-139">fluxo de trabalho Olá estava a ser executado, mas foi recebido um pedido de cancelamento.</span><span class="sxs-lookup"><span data-stu-id="9d4e1-139">hello workflow was running but received a cancel request.</span></span>
* <span data-ttu-id="9d4e1-140">**Executar**.</span><span class="sxs-lookup"><span data-stu-id="9d4e1-140">**Running**.</span></span> <span data-ttu-id="9d4e1-141">fluxo de trabalho Olá está atualmente em execução.</span><span class="sxs-lookup"><span data-stu-id="9d4e1-141">hello workflow is currently running.</span></span> <span data-ttu-id="9d4e1-142">Este estado pode ocorrer para fluxos de trabalho otimizados ou devido a Olá atual plano de preços.</span><span class="sxs-lookup"><span data-stu-id="9d4e1-142">This status might occur for throttled workflows, or because of hello current pricing plan.</span></span> <span data-ttu-id="9d4e1-143">Para obter mais informações, consulte [limites de ação na página de preços de Olá](https://azure.microsoft.com/pricing/details/app-service/plans/).</span><span class="sxs-lookup"><span data-stu-id="9d4e1-143">For details, see [action limits on hello pricing page](https://azure.microsoft.com/pricing/details/app-service/plans/).</span></span> <span data-ttu-id="9d4e1-144">Configurar o diagnóstico (gráficos de Olá que são apresentados em Olá histórico de execução) também pode fornecer informações sobre quaisquer eventos de limitação que ocorrem.</span><span class="sxs-lookup"><span data-stu-id="9d4e1-144">Configuring diagnostics (hello charts that appear under hello run history) also can provide information about any throttle events that happen.</span></span>

<span data-ttu-id="9d4e1-145">Quando está a visualizar um histórico de execução, pode desagregar para obter mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="9d4e1-145">When you are looking at a run history, you can drill in for more details.</span></span>  

#### <a name="trigger-outputs"></a><span data-ttu-id="9d4e1-146">Saídas de Acionador</span><span class="sxs-lookup"><span data-stu-id="9d4e1-146">Trigger outputs</span></span>

<span data-ttu-id="9d4e1-147">Acionador produz Mostrar dados de Olá que provém de Acionador de Olá.</span><span class="sxs-lookup"><span data-stu-id="9d4e1-147">Trigger outputs show hello data that came from hello trigger.</span></span> <span data-ttu-id="9d4e1-148">Estes saídas podem ajudá-lo a determinar se todas as propriedades devolvidas conforme esperado.</span><span class="sxs-lookup"><span data-stu-id="9d4e1-148">These outputs can help you determine whether all properties returned as expected.</span></span>

> [!NOTE]
> <span data-ttu-id="9d4e1-149">Se vir qualquer conteúdo que não compreender, saiba como Azure Logic Apps [processa diferentes tipos de conteúdo](../logic-apps/logic-apps-content-type.md).</span><span class="sxs-lookup"><span data-stu-id="9d4e1-149">If you see any content that you don't understand, learn how Azure Logic Apps [handles different content types](../logic-apps/logic-apps-content-type.md).</span></span>
> 

![Exemplos de saída do acionador][3]

#### <a name="action-inputs-and-outputs"></a><span data-ttu-id="9d4e1-151">Ação de entradas e saídas</span><span class="sxs-lookup"><span data-stu-id="9d4e1-151">Action inputs and outputs</span></span>

<span data-ttu-id="9d4e1-152">Pode explorar entradas de Olá e saídas que receberam uma ação.</span><span class="sxs-lookup"><span data-stu-id="9d4e1-152">You can drill into hello inputs and outputs that an action received.</span></span> <span data-ttu-id="9d4e1-153">Estes dados são útil para compreender o tamanho de Olá e a forma da área de Olá saídas e também para localizar as mensagens de erro poderão ter sido geradas.</span><span class="sxs-lookup"><span data-stu-id="9d4e1-153">This data is useful for understanding hello size and shape of hello outputs, and also for finding any error messages that might have been generated.</span></span>

![Ação de entradas e saídas][4]

## <a name="debug-workflow-runtime"></a><span data-ttu-id="9d4e1-155">Tempo de execução do fluxo de trabalho de depuração</span><span class="sxs-lookup"><span data-stu-id="9d4e1-155">Debug workflow runtime</span></span>

<span data-ttu-id="9d4e1-156">Juntamente com a monitorização entradas Olá, saídas e acionadores de execução, pode adicionar alguns fluxo de trabalho de tooa passos que ajudam na depuração.</span><span class="sxs-lookup"><span data-stu-id="9d4e1-156">Along with monitoring hello inputs, outputs, and triggers of a run, you could add some steps tooa workflow that help with debugging.</span></span> 
<span data-ttu-id="9d4e1-157">[RequestBin](http://requestb.in) é uma ferramenta poderosa, que pode adicionar como um passo num fluxo de trabalho.</span><span class="sxs-lookup"><span data-stu-id="9d4e1-157">[RequestBin](http://requestb.in) is a powerful tool that you can add as a step in a workflow.</span></span> <span data-ttu-id="9d4e1-158">Ao utilizar RequestBin, pode configurar um HTTP inspector toodetermine Olá exato tamanho do pedido, a forma e o formato de um pedido HTTP.</span><span class="sxs-lookup"><span data-stu-id="9d4e1-158">By using RequestBin, you can set up an HTTP request inspector toodetermine hello exact size, shape, and format of an HTTP request.</span></span> <span data-ttu-id="9d4e1-159">Pode criar um RequestBin e cole o URL de Olá numa aplicação lógica ação de HTTP POST com conteúdo do corpo que pretende que tootest, por exemplo, uma expressão ou outro resultado de passo.</span><span class="sxs-lookup"><span data-stu-id="9d4e1-159">You can create a RequestBin and paste hello URL in a logic app HTTP POST action with body content that you want tootest, for example, an expression or another step output.</span></span> <span data-ttu-id="9d4e1-160">Depois de executar a aplicação de lógica de Olá, pode atualizar o seu toosee RequestBin como pedido Olá foi incorretamente quando gerados a partir do motor do Olá Logic Apps.</span><span class="sxs-lookup"><span data-stu-id="9d4e1-160">After you run hello logic app, you can refresh your RequestBin toosee how hello request was formed when generated from hello Logic Apps engine.</span></span>

<!-- image references -->
[1]: ./media/logic-apps-diagnosing-failures/triggerhistory.png
[2]: ./media/logic-apps-diagnosing-failures/runhistory.png
[3]: ./media/logic-apps-diagnosing-failures/triggeroutputslink.png
[4]: ./media/logic-apps-diagnosing-failures/actionoutputs.png
