---
title: conector de aaaSMTP no Azure Logic Apps | Microsoft Docs
description: "Crie aplicações lógicas com o App service do Azure. Ligar tooSMTP toosend e-mail."
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: d4141c08-88d7-4e59-a757-c06d0dc74300
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 07/15/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 36bb836851014d24f2e069fda8376ad7a08c943b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-smtp-connector"></a><span data-ttu-id="8b8f5-104">Começar a utilizar o conector de SMTP Olá</span><span class="sxs-lookup"><span data-stu-id="8b8f5-104">Get started with hello SMTP connector</span></span>
<span data-ttu-id="8b8f5-105">Ligar tooSMTP toosend e-mail.</span><span class="sxs-lookup"><span data-stu-id="8b8f5-105">Connect tooSMTP toosend email.</span></span>

<span data-ttu-id="8b8f5-106">toouse [qualquer conector](apis-list.md), terá primeiro de toocreate uma aplicação lógica.</span><span class="sxs-lookup"><span data-stu-id="8b8f5-106">toouse [any connector](apis-list.md), you first need toocreate a logic app.</span></span> <span data-ttu-id="8b8f5-107">Pode começar a utilizar pelo [criar uma aplicação lógica agora](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="8b8f5-107">You can get started by [creating a logic app now](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-toosmtp"></a><span data-ttu-id="8b8f5-108">Ligar tooSMTP</span><span class="sxs-lookup"><span data-stu-id="8b8f5-108">Connect tooSMTP</span></span>
<span data-ttu-id="8b8f5-109">Antes da aplicação lógica pode aceder a qualquer serviço, terá primeiro de toocreate um *ligação* toohello serviço.</span><span class="sxs-lookup"><span data-stu-id="8b8f5-109">Before your logic app can access any service, you first need toocreate a *connection* toohello service.</span></span> <span data-ttu-id="8b8f5-110">A [ligação](connectors-overview.md) fornece conectividade entre uma aplicação lógica e outro serviço.</span><span class="sxs-lookup"><span data-stu-id="8b8f5-110">A [connection](connectors-overview.md) provides connectivity between a logic app and another service.</span></span> <span data-ttu-id="8b8f5-111">Por exemplo, tooconnect tooSMTP, primeiro precisa de um SMTP *ligação*.</span><span class="sxs-lookup"><span data-stu-id="8b8f5-111">For example, tooconnect tooSMTP, you first need an SMTP *connection*.</span></span> <span data-ttu-id="8b8f5-112">toocreate uma ligação, introduza as credenciais de Olá que normalmente utiliza o serviço de Olá tooaccess ligar.</span><span class="sxs-lookup"><span data-stu-id="8b8f5-112">toocreate a connection, enter hello credentials you normally use tooaccess hello service you connect to.</span></span> <span data-ttu-id="8b8f5-113">Por isso, no exemplo de Olá SMTP, introduza nome da ligação Olá credenciais tooyour, o endereço do servidor SMTP e o utilizador início de sessão informações toocreate Olá ligação tooSMTP.</span><span class="sxs-lookup"><span data-stu-id="8b8f5-113">So, in hello SMTP example, enter hello credentials tooyour connection name, SMTP server address, and user login information toocreate hello connection tooSMTP.</span></span>  

### <a name="create-a-connection-toosmtp"></a><span data-ttu-id="8b8f5-114">Criar uma ligação tooSMTP</span><span class="sxs-lookup"><span data-stu-id="8b8f5-114">Create a connection tooSMTP</span></span>
> [!INCLUDE [Steps toocreate a connection tooSMTP](../../includes/connectors-create-api-smtp.md)]
> 
> 

## <a name="use-an-smtp-trigger"></a><span data-ttu-id="8b8f5-115">Utilizar um acionador de SMTP</span><span class="sxs-lookup"><span data-stu-id="8b8f5-115">Use an SMTP trigger</span></span>
<span data-ttu-id="8b8f5-116">Um acionador é um evento que pode ser o fluxo de trabalho do Olá toostart utilizados definido numa aplicação lógica.</span><span class="sxs-lookup"><span data-stu-id="8b8f5-116">A trigger is an event that can be used toostart hello workflow defined in a logic app.</span></span> <span data-ttu-id="8b8f5-117">[Saiba mais sobre acionadores](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="8b8f5-117">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

<span data-ttu-id="8b8f5-118">Neste exemplo, porque SMTP não tem um acionador próprios, iremos utilizar Olá **Salesforce - quando é criado um objecto** acionador.</span><span class="sxs-lookup"><span data-stu-id="8b8f5-118">In this example, because SMTP does not have a trigger of its own, we'll use hello **Salesforce - When an object is created** trigger.</span></span> <span data-ttu-id="8b8f5-119">Este acionador ativa quando é criado um novo objeto no Salesforce.</span><span class="sxs-lookup"><span data-stu-id="8b8f5-119">This trigger activates when a new object is created in Salesforce.</span></span> <span data-ttu-id="8b8f5-120">Para o nosso exemplo, iremos definir-forma a que sempre que é criado um novo fabrico no Salesforce, um *enviar correio eletrónico* ação ocorre através do conector de Olá SMTP com uma notificação de Olá novas oportunidades potenciais a ser criada.</span><span class="sxs-lookup"><span data-stu-id="8b8f5-120">For our example, we'll set it up such that every time a new lead is created in Salesforce, a *send email* action occurs via hello SMTP connector with a notification of hello new lead being created.</span></span>

1. <span data-ttu-id="8b8f5-121">Introduza *salesforce* na caixa de pesquisa de Olá no designer de aplicações de lógica de Olá, em seguida, selecione Olá **Salesforce - quando é criado um objecto** acionador.</span><span class="sxs-lookup"><span data-stu-id="8b8f5-121">Enter *salesforce* in hello search box on hello logic apps designer then select hello **Salesforce - When an object is created** trigger.</span></span>  
   ![](../../includes/media/connectors-create-api-salesforce/trigger-1.png)  
2. <span data-ttu-id="8b8f5-122">Olá **quando é criado um objecto** controlo é apresentado.</span><span class="sxs-lookup"><span data-stu-id="8b8f5-122">hello **When an object is created** control is displayed.</span></span>
   ![](../../includes/media/connectors-create-api-salesforce/trigger-2.png)  
3. <span data-ttu-id="8b8f5-123">Selecione Olá **tipo de objeto** , em seguida, selecione *levar* da lista de Olá de objetos.</span><span class="sxs-lookup"><span data-stu-id="8b8f5-123">Select hello **Object Type** then select *Lead* from hello list of objects.</span></span> <span data-ttu-id="8b8f5-124">Neste passo, é com a indicação de que está a criar um acionador que irá notificar a sua aplicação lógica sempre que é criado um novo fabrico no Salesforce.</span><span class="sxs-lookup"><span data-stu-id="8b8f5-124">In this step you are indicating that you are creating a trigger that will notify your logic app whenever a new lead is created in Salesforce.</span></span>  
   ![](../../includes/media/connectors-create-api-salesforce/trigger3.png)  
4. <span data-ttu-id="8b8f5-125">acionador Olá foi criado.</span><span class="sxs-lookup"><span data-stu-id="8b8f5-125">hello trigger has been created.</span></span>  
   ![](../../includes/media/connectors-create-api-salesforce/trigger-4.png)  

## <a name="use-an-smtp-action"></a><span data-ttu-id="8b8f5-126">Utilizar uma ação de SMTP</span><span class="sxs-lookup"><span data-stu-id="8b8f5-126">Use an SMTP action</span></span>
<span data-ttu-id="8b8f5-127">Uma ação é uma operação levada a cabo pelo fluxo de trabalho Olá definido numa aplicação lógica.</span><span class="sxs-lookup"><span data-stu-id="8b8f5-127">An action is an operation carried out by hello workflow defined in a logic app.</span></span> <span data-ttu-id="8b8f5-128">[Saiba mais sobre as ações](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="8b8f5-128">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

<span data-ttu-id="8b8f5-129">Agora que hello acionador foi adicionado, siga estas ação tooadd um SMTP passos que irá ocorrer quando é criado um novo fabrico no Salesforce.</span><span class="sxs-lookup"><span data-stu-id="8b8f5-129">Now that hello trigger has been added, follow these steps tooadd an SMTP action that will occur when a new lead is created in Salesforce.</span></span>

1. <span data-ttu-id="8b8f5-130">Selecione **+ novo passo** ação de Olá tooadd gostaria tootake quando é criada uma antecedência de novo.</span><span class="sxs-lookup"><span data-stu-id="8b8f5-130">Select **+ New Step** tooadd hello action you would like tootake when a new lead is created.</span></span>  
   ![](../../includes/media/connectors-create-api-salesforce/trigger4.png)  
2. <span data-ttu-id="8b8f5-131">Selecione **adicionar uma ação**.</span><span class="sxs-lookup"><span data-stu-id="8b8f5-131">Select **Add an action**.</span></span> <span data-ttu-id="8b8f5-132">Esta caixa de pesquisa de Olá abre onde pode procurar qualquer ação gostaria de tootake.</span><span class="sxs-lookup"><span data-stu-id="8b8f5-132">This opens hello search box where you can search for any action you would like tootake.</span></span>  
   ![](../../includes/media/connectors-create-api-smtp/using-smtp-action-2.png)  
3. <span data-ttu-id="8b8f5-133">Introduza *smtp* toosearch para ações de tooSMTP relacionados.</span><span class="sxs-lookup"><span data-stu-id="8b8f5-133">Enter *smtp* toosearch for actions related tooSMTP.</span></span>  
4. <span data-ttu-id="8b8f5-134">Selecione **SMTP - enviar correio eletrónico** como Olá ação tootake quando antecedência novo Olá é criada.</span><span class="sxs-lookup"><span data-stu-id="8b8f5-134">Select **SMTP - Send Email** as hello action tootake when hello new lead is created.</span></span> <span data-ttu-id="8b8f5-135">Bloco de controlo de ação de Olá abre.</span><span class="sxs-lookup"><span data-stu-id="8b8f5-135">hello action control block opens.</span></span> <span data-ttu-id="8b8f5-136">Terá tooestablish a ligação de smtp no bloco de estruturador Olá se não o fez, anteriormente.</span><span class="sxs-lookup"><span data-stu-id="8b8f5-136">You will have tooestablish your smtp connection in hello designer block if you have not done so previously.</span></span>  
   ![](../../includes/media/connectors-create-api-smtp/smtp-2.png)    
5. <span data-ttu-id="8b8f5-137">Introduza as informações do e-mail pretendido no Olá **SMTP - enviar correio eletrónico** bloco.</span><span class="sxs-lookup"><span data-stu-id="8b8f5-137">Input your desired email information in hello **SMTP - Send Email** block.</span></span>  
   ![](../../includes/media/connectors-create-api-smtp/using-smtp-action-4.PNG)  
6. <span data-ttu-id="8b8f5-138">Guarde o trabalho na ordem tooactivate o fluxo de trabalho.</span><span class="sxs-lookup"><span data-stu-id="8b8f5-138">Save your work in order tooactivate your workflow.</span></span>  

## <a name="connector-specific-details"></a><span data-ttu-id="8b8f5-139">Detalhes específicos do conector</span><span class="sxs-lookup"><span data-stu-id="8b8f5-139">Connector-specific details</span></span>

<span data-ttu-id="8b8f5-140">Ver todos os acionadores e ações definidas no swagger Olá e consulte também os limites de Olá [detalhes do conector](/connectors/smtpconnector/).</span><span class="sxs-lookup"><span data-stu-id="8b8f5-140">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/smtpconnector/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="8b8f5-141">Mais conectores</span><span class="sxs-lookup"><span data-stu-id="8b8f5-141">More connectors</span></span>
<span data-ttu-id="8b8f5-142">Voltar atrás toohello [lista APIs](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="8b8f5-142">Go back toohello [APIs list](apis-list.md).</span></span>
