---
title: "aaaScenario - logic apps do acionador com as funções do Azure e Azure Service Bus | Microsoft Docs"
description: "Criar uma aplicação lógica de uma função tootrigger através da utilização das funções do Azure e o Service Bus do Azure"
services: logic-apps,functions
documentationcenter: .net,nodejs,java
author: jeffhollan
manager: anneta
editor: 
ms.assetid: 19cbd921-7071-4221-ab86-b44d0fc0ecef
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 05/23/2016
ms.author: LADocs; jehollan
ms.openlocfilehash: a7b78ebcfe492eee2e08ceeae6b9c5f8ed4717bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="scenario-trigger-a-logic-app-with-azure-functions-and-azure-service-bus"></a><span data-ttu-id="1439c-103">Cenário: Acionar uma aplicação lógica com as funções do Azure e o Service Bus do Azure</span><span class="sxs-lookup"><span data-stu-id="1439c-103">Scenario: Trigger a logic app with Azure Functions and Azure Service Bus</span></span>

<span data-ttu-id="1439c-104">Pode utilizar as funções do Azure toocreate um acionador para uma aplicação lógica quando precisar de toodeploy uma execução longa escuta ou tarefas.</span><span class="sxs-lookup"><span data-stu-id="1439c-104">You can use Azure Functions toocreate a trigger for a logic app when you need toodeploy a long-running listener or task.</span></span> <span data-ttu-id="1439c-105">Por exemplo, pode criar uma função que escuta uma fila e, em seguida, acionados imediatamente uma aplicação lógica como um acionador de push.</span><span class="sxs-lookup"><span data-stu-id="1439c-105">For example, you can create a function that listens in on a queue and then immediately fire a logic app as a push trigger.</span></span>

## <a name="build-hello-logic-app"></a><span data-ttu-id="1439c-106">Criar aplicação de lógica de Olá</span><span class="sxs-lookup"><span data-stu-id="1439c-106">Build hello logic app</span></span>
<span data-ttu-id="1439c-107">Neste exemplo, poderá ter uma função em execução para cada aplicação lógica que necessita de toobe acionado.</span><span class="sxs-lookup"><span data-stu-id="1439c-107">In this example, you have a function running for each logic app that needs toobe triggered.</span></span> <span data-ttu-id="1439c-108">Em primeiro lugar, crie uma aplicação lógica que tem um acionador de pedido HTTP.</span><span class="sxs-lookup"><span data-stu-id="1439c-108">First, create a logic app that has an HTTP request trigger.</span></span> <span data-ttu-id="1439c-109">esse ponto final de chamadas de função de Olá sempre que é recebida uma mensagem de fila.</span><span class="sxs-lookup"><span data-stu-id="1439c-109">hello function calls that endpoint whenever a queue message is received.</span></span>  

1. <span data-ttu-id="1439c-110">Crie uma aplicação lógica.</span><span class="sxs-lookup"><span data-stu-id="1439c-110">Create a logic app.</span></span>
2. <span data-ttu-id="1439c-111">Selecione Olá **Manual - quando é recebido um pedido HTTP** acionador.</span><span class="sxs-lookup"><span data-stu-id="1439c-111">Select hello **Manual - When an HTTP Request is Received** trigger.</span></span>
   <span data-ttu-id="1439c-112">Opcionalmente, pode especificar um toouse de esquema JSON com a mensagem da fila de Olá utilizando uma ferramenta como o [jsonschema.net](http://jsonschema.net).</span><span class="sxs-lookup"><span data-stu-id="1439c-112">Optionally, you can specify a JSON schema toouse with hello queue message by using a tool like [jsonschema.net](http://jsonschema.net).</span></span> <span data-ttu-id="1439c-113">Cole o esquema de Olá no acionador Olá.</span><span class="sxs-lookup"><span data-stu-id="1439c-113">Paste hello schema in hello trigger.</span></span> <span data-ttu-id="1439c-114">Esquemas ajudam designer Olá compreender a forma de Olá das propriedades de dados e fluem no sentido de Olá mais facilmente através de Olá fluxo de trabalho.</span><span class="sxs-lookup"><span data-stu-id="1439c-114">Schemas help hello designer understand hello shape of hello data and flow properties more easily through hello workflow.</span></span>
2. <span data-ttu-id="1439c-115">Adiciona quaisquer passos adicionais que pretenda toooccur depois é recebida uma mensagem de fila.</span><span class="sxs-lookup"><span data-stu-id="1439c-115">Add any additional steps that you want toooccur after a queue message is received.</span></span> <span data-ttu-id="1439c-116">Por exemplo, envie uma mensagem de e-mail através do Office 365.</span><span class="sxs-lookup"><span data-stu-id="1439c-116">For example, send an email via Office 365.</span></span>  
3. <span data-ttu-id="1439c-117">Guarde Olá lógica toogenerate Olá chamada de retorno URL da aplicação para a aplicação de lógica de toothis de Acionador de Olá.</span><span class="sxs-lookup"><span data-stu-id="1439c-117">Save hello logic app toogenerate hello callback URL for hello trigger toothis logic app.</span></span> <span data-ttu-id="1439c-118">URL de Olá é apresentado no cartão de Acionador de Olá.</span><span class="sxs-lookup"><span data-stu-id="1439c-118">hello URL appears on hello trigger card.</span></span>

![chamada de retorno Olá URL aparece no cartão de Acionador de Olá][1]

## <a name="build-hello-function"></a><span data-ttu-id="1439c-120">Criar função Olá</span><span class="sxs-lookup"><span data-stu-id="1439c-120">Build hello function</span></span>
<span data-ttu-id="1439c-121">Em seguida, tem de criar uma função que age como acionador Olá e escuta toohello fila.</span><span class="sxs-lookup"><span data-stu-id="1439c-121">Next, you must create a function that acts as hello trigger and listens toohello queue.</span></span>

1. <span data-ttu-id="1439c-122">No Olá [portal das funções do Azure](https://functions.azure.com/signin), selecione **nova função**e, em seguida, selecione Olá **ServiceBusQueueTrigger - c#** modelo.</span><span class="sxs-lookup"><span data-stu-id="1439c-122">In hello [Azure Functions portal](https://functions.azure.com/signin), select **New Function**, and then select hello **ServiceBusQueueTrigger - C#** template.</span></span>
   
    ![Portal de funções do Azure][2]
2. <span data-ttu-id="1439c-124">Configurar Olá ligação toohello fila do Service Bus, que utiliza Olá SDK do Service Bus `OnMessageReceive()` serviço de escuta.</span><span class="sxs-lookup"><span data-stu-id="1439c-124">Configure hello connection toohello Service Bus queue, which uses hello Azure Service Bus SDK `OnMessageReceive()` listener.</span></span>
3. <span data-ttu-id="1439c-125">Gravar um função básico toocall Olá logic app ponto final (criado anteriormente) utilizando a mensagem da fila de saudação como um acionador.</span><span class="sxs-lookup"><span data-stu-id="1439c-125">Write a basic function toocall hello logic app endpoint (created earlier) by using hello queue message as a trigger.</span></span> <span data-ttu-id="1439c-126">Eis um exemplo completo de uma função.</span><span class="sxs-lookup"><span data-stu-id="1439c-126">Here's a full example of a function.</span></span> <span data-ttu-id="1439c-127">exemplo de Olá utiliza um `application/json` tipo de conteúdo de mensagem, mas pode alterar este tipo conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="1439c-127">hello example uses an `application/json` message content type, but you can change this type as necessary.</span></span>
   
   ```
   using System;
   using System.Threading.Tasks;
   using System.Net.Http;
   using System.Text;
   
   private static string logicAppUri = @"https://prod-05.westus.logic.azure.com:443/.........";
   
   public static void Run(string myQueueItem, TraceWriter log)
   {
   
       log.Info($"C# ServiceBus queue trigger function processed message: {myQueueItem}");
       using (var client = new HttpClient())
       {
           var response = client.PostAsync(logicAppUri, new StringContent(myQueueItem, Encoding.UTF8, "application/json")).Result;
       }
   }
   ```

<span data-ttu-id="1439c-128">tootest, adicione uma mensagem da fila através de uma ferramenta como o [Explorador do Service Bus](https://github.com/paolosalvatori/ServiceBusExplorer).</span><span class="sxs-lookup"><span data-stu-id="1439c-128">tootest, add a queue message via a tool like [Service Bus Explorer](https://github.com/paolosalvatori/ServiceBusExplorer).</span></span> <span data-ttu-id="1439c-129">Consulte a aplicação de lógica de Olá acionados imediatamente após a função de Olá recebe a mensagem de saudação.</span><span class="sxs-lookup"><span data-stu-id="1439c-129">See hello logic app fire immediately after hello function receives hello message.</span></span>

<!-- Image References -->
[1]: ./media/logic-apps-scenario-function-sb-trigger/manualtrigger.png
[2]: ./media/logic-apps-scenario-function-sb-trigger/newqueuetriggerfunction.png
