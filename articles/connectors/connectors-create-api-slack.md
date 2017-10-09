---
title: "aaaUse Olá Slack conector nas suas Azure logic apps | Microsoft Docs"
description: Ligar tooSlack nas suas logic apps
services: logic-apps
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: 234cad64-b13d-4494-ae78-18b17119ba24
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 6599d7b69d2147425c9fab978c5d0f93e5605f19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-slack-connector"></a><span data-ttu-id="7cf5a-103">Introdução ao conector Slack Olá</span><span class="sxs-lookup"><span data-stu-id="7cf5a-103">Get started with hello Slack connector</span></span>
<span data-ttu-id="7cf5a-104">Slack é uma ferramenta de comunicação de equipa, que reúne todas as suas comunicações equipa num colocar, de forma instantânea pesquisáveis e disponível onde quer que esteja.</span><span class="sxs-lookup"><span data-stu-id="7cf5a-104">Slack is a team communication tool, that brings together all of your team communications in one place, instantly searchable and available wherever you go.</span></span> 

<span data-ttu-id="7cf5a-105">Começar através da criação de uma aplicação lógica agora; consulte [criar uma aplicação lógica](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="7cf5a-105">Get started by creating a logic app now; see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="create-a-connection-tooslack"></a><span data-ttu-id="7cf5a-106">Criar uma ligação tooSlack</span><span class="sxs-lookup"><span data-stu-id="7cf5a-106">Create a connection tooSlack</span></span>
<span data-ttu-id="7cf5a-107">conector de Slack Olá toouse, crie primeiro um **ligação** , em seguida, fornecer detalhes de Olá estas propriedades:</span><span class="sxs-lookup"><span data-stu-id="7cf5a-107">toouse hello Slack connector, you first create a **connection** then provide hello details for these properties:</span></span> 

| <span data-ttu-id="7cf5a-108">Propriedade</span><span class="sxs-lookup"><span data-stu-id="7cf5a-108">Property</span></span> | <span data-ttu-id="7cf5a-109">Necessário</span><span class="sxs-lookup"><span data-stu-id="7cf5a-109">Required</span></span> | <span data-ttu-id="7cf5a-110">Descrição</span><span class="sxs-lookup"><span data-stu-id="7cf5a-110">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="7cf5a-111">Token</span><span class="sxs-lookup"><span data-stu-id="7cf5a-111">Token</span></span> |<span data-ttu-id="7cf5a-112">Sim</span><span class="sxs-lookup"><span data-stu-id="7cf5a-112">Yes</span></span> |<span data-ttu-id="7cf5a-113">Forneça credenciais Slack</span><span class="sxs-lookup"><span data-stu-id="7cf5a-113">Provide Slack Credentials</span></span> |

<span data-ttu-id="7cf5a-114">Siga estes passos toosign ao Slack e configuração de Olá completa de Olá Slack **ligação** na sua aplicação lógica:</span><span class="sxs-lookup"><span data-stu-id="7cf5a-114">Follow these steps toosign into Slack, and complete hello configuration of hello Slack **connection** in your logic app:</span></span>

1. <span data-ttu-id="7cf5a-115">Selecione **periodicidade**</span><span class="sxs-lookup"><span data-stu-id="7cf5a-115">Select **Recurrence**</span></span>
2. <span data-ttu-id="7cf5a-116">Selecione um **frequência** e introduza um **intervalo**</span><span class="sxs-lookup"><span data-stu-id="7cf5a-116">Select a **Frequency** and enter an **Interval**</span></span>
3. <span data-ttu-id="7cf5a-117">Selecione **adicionar uma ação**</span><span class="sxs-lookup"><span data-stu-id="7cf5a-117">Select **Add an action**</span></span>  
   <span data-ttu-id="7cf5a-118">![Configurar Slack][1]</span><span class="sxs-lookup"><span data-stu-id="7cf5a-118">![Configure Slack][1]</span></span>  
4. <span data-ttu-id="7cf5a-119">Introduza Slack na caixa de pesquisa de Olá e aguarde Olá pesquisa tooreturn todas as entradas com Slack no nome de Olá</span><span class="sxs-lookup"><span data-stu-id="7cf5a-119">Enter Slack in hello search box and wait for hello search tooreturn all entries with Slack in hello name</span></span>
5. <span data-ttu-id="7cf5a-120">Selecione **Slack - mensagem Post**</span><span class="sxs-lookup"><span data-stu-id="7cf5a-120">Select **Slack - Post message**</span></span>
6. <span data-ttu-id="7cf5a-121">Selecione **sessão tooSlack**:</span><span class="sxs-lookup"><span data-stu-id="7cf5a-121">Select **Sign in tooSlack**:</span></span>  
   <span data-ttu-id="7cf5a-122">![Configurar Slack][2]</span><span class="sxs-lookup"><span data-stu-id="7cf5a-122">![Configure Slack][2]</span></span>
7. <span data-ttu-id="7cf5a-123">Forneça o toosign credenciais Slack na aplicação de Olá tooauthorize</span><span class="sxs-lookup"><span data-stu-id="7cf5a-123">Provide your Slack credentials toosign in tooauthorize hello  application</span></span>    
   ![Configurar Slack][3]  
8. <span data-ttu-id="7cf5a-125">Será página de início de sessão redirecionado tooyour organização.</span><span class="sxs-lookup"><span data-stu-id="7cf5a-125">You'll be redirected tooyour organization's Log in page.</span></span> <span data-ttu-id="7cf5a-126">**Autorizar** toointeract Slack com a sua aplicação lógica:</span><span class="sxs-lookup"><span data-stu-id="7cf5a-126">**Authorize** Slack toointeract with your logic app:</span></span>      
   <span data-ttu-id="7cf5a-127">![Configurar Slack][5]</span><span class="sxs-lookup"><span data-stu-id="7cf5a-127">![Configure Slack][5]</span></span> 
9. <span data-ttu-id="7cf5a-128">Após a conclusão da autorização de Olá será redirecionado tooyour logic app toocomplete-configurando Olá **Slack - obter todas as mensagens** secção.</span><span class="sxs-lookup"><span data-stu-id="7cf5a-128">After hello authorization completes you'll be redirected tooyour logic app toocomplete it by configuring hello **Slack - Get all messages** section.</span></span> <span data-ttu-id="7cf5a-129">Adicione outros acionadores e ações que precisa.</span><span class="sxs-lookup"><span data-stu-id="7cf5a-129">Add other triggers and actions that you need.</span></span>  
   <span data-ttu-id="7cf5a-130">![Configurar Slack][6]</span><span class="sxs-lookup"><span data-stu-id="7cf5a-130">![Configure Slack][6]</span></span>
10. <span data-ttu-id="7cf5a-131">Guarde o trabalho selecionando **guardar** na barra de menus Olá acima.</span><span class="sxs-lookup"><span data-stu-id="7cf5a-131">Save your work by selecting **Save** on hello menu bar above.</span></span>

## <a name="connector-specific-details"></a><span data-ttu-id="7cf5a-132">Detalhes específicos do conector</span><span class="sxs-lookup"><span data-stu-id="7cf5a-132">Connector-specific details</span></span>

<span data-ttu-id="7cf5a-133">Ver todos os acionadores e ações definidas no swagger Olá e consulte também os limites de Olá [detalhes do conector](/connectors/slack/).</span><span class="sxs-lookup"><span data-stu-id="7cf5a-133">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/slack/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="7cf5a-134">Mais conectores</span><span class="sxs-lookup"><span data-stu-id="7cf5a-134">More connectors</span></span>
<span data-ttu-id="7cf5a-135">Voltar atrás toohello [lista APIs](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="7cf5a-135">Go back toohello [APIs list](apis-list.md).</span></span>

[1]: ./media/connectors-create-api-slack/connectionconfig1.png
[2]: ./media/connectors-create-api-slack/connectionconfig2.png 
[3]: ./media/connectors-create-api-slack/connectionconfig3.png
[4]: ./media/connectors-create-api-slack/connectionconfig4.png
[5]: ./media/connectors-create-api-slack/connectionconfig5.png
[6]: ./media/connectors-create-api-slack/connectionconfig6.png
