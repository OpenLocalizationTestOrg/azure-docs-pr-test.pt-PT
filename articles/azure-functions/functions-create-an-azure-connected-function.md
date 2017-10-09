---
title: "aaaCreate uma função que estabelece ligação a serviços tooAzure | Microsoft Docs"
description: "Utilize as funções do Azure toocreate uma aplicação sem servidor que liga tooother Azure serviços."
services: functions
documentationcenter: dev-center-name
author: yochay
manager: manager-alias
editor: 
tags: 
keywords: "funções do azure, funções, processamento de eventos, webhooks, computação dinâmica, arquitetura sem servidor"
ms.assetid: ab86065d-6050-46c9-a336-1bfc1fa4b5a1
ms.service: functions
ms.devlang: multiple
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 03/01/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 9d1f7d3b236f8d2c1a404c76aee410f6d458fb7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-functions-toocreate-a-function-that-connects-tooother-azure-services"></a><span data-ttu-id="a5c0e-104">Utilize as funções do Azure toocreate uma função que estabelece ligação tooother Azure serviços</span><span class="sxs-lookup"><span data-stu-id="a5c0e-104">Use Azure Functions toocreate a function that connects tooother Azure services</span></span>

<span data-ttu-id="a5c0e-105">Este tópico mostra como toocreate uma função nas funções do Azure que escuta toomessages no Olá de fila e as cópias de um armazenamento do Azure mensagens toorows uma tabela de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="a5c0e-105">This topic shows you how toocreate a function in Azure Functions that listens toomessages on an Azure Storage queue and copies hello messages toorows in an Azure Storage table.</span></span> <span data-ttu-id="a5c0e-106">Uma função de temporizador acionada é utilizado tooload mensagens na fila de Olá.</span><span class="sxs-lookup"><span data-stu-id="a5c0e-106">A timer triggered function is used tooload messages into hello queue.</span></span> <span data-ttu-id="a5c0e-107">Uma segunda função lê a partir da fila de Olá e escreve tabela toohello de mensagens.</span><span class="sxs-lookup"><span data-stu-id="a5c0e-107">A second function reads from hello queue and writes messages toohello table.</span></span> <span data-ttu-id="a5c0e-108">Fila Olá e tabela de Olá são criados pelas funções do Azure com base nas definições de enlace Olá.</span><span class="sxs-lookup"><span data-stu-id="a5c0e-108">Both hello queue and hello table are created for you by Azure Functions based on hello binding definitions.</span></span> 

<span data-ttu-id="a5c0e-109">ações de toomake mais interessantes, uma função é escrita em JavaScript e Olá outro é escrito em c# script.</span><span class="sxs-lookup"><span data-stu-id="a5c0e-109">toomake things more interesting, one function is written in JavaScript and hello other is written in C# script.</span></span> <span data-ttu-id="a5c0e-110">Isto demonstra como uma aplicação de função pode ter funções em várias linguagens.</span><span class="sxs-lookup"><span data-stu-id="a5c0e-110">This demonstrates how a function app can have functions in various languages.</span></span> 

<span data-ttu-id="a5c0e-111">Pode ver este cenário demonstrado num [vídeo no Canal 9](https://channel9.msdn.com/Series/Windows-Azure-Web-Sites-Tutorials/Create-an-Azure-Function-which-binds-to-an-Azure-service/player).</span><span class="sxs-lookup"><span data-stu-id="a5c0e-111">You can see this scenario demonstrated in a [video on Channel 9](https://channel9.msdn.com/Series/Windows-Azure-Web-Sites-Tutorials/Create-an-Azure-Function-which-binds-to-an-Azure-service/player).</span></span>

## <a name="create-a-function-that-writes-toohello-queue"></a><span data-ttu-id="a5c0e-112">Criar uma função que escreve toohello fila</span><span class="sxs-lookup"><span data-stu-id="a5c0e-112">Create a function that writes toohello queue</span></span>

<span data-ttu-id="a5c0e-113">Antes de poder ligar tooa fila de armazenamento, terá de toocreate uma função que carrega a fila de mensagens hello.</span><span class="sxs-lookup"><span data-stu-id="a5c0e-113">Before you can connect tooa storage queue, you need toocreate a function that loads hello message queue.</span></span> <span data-ttu-id="a5c0e-114">Esta função de JavaScript utiliza um acionador de temporizador escreve uma fila de toohello mensagens cada 10 segundos.</span><span class="sxs-lookup"><span data-stu-id="a5c0e-114">This JavaScript function uses a timer trigger that writes a message toohello queue every 10 seconds.</span></span> <span data-ttu-id="a5c0e-115">Se ainda não tiver uma conta do Azure, veja Olá [das funções do Azure de tente](https://functions.azure.com/try) experiência, ou [criar a sua conta do Azure gratuita](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="a5c0e-115">If you don't already have an Azure account, check out hello [Try Azure Functions](https://functions.azure.com/try) experience, or [create your free Azure account](https://azure.microsoft.com/free/).</span></span>

1. <span data-ttu-id="a5c0e-116">Aceda toohello portal do Azure e localize a aplicação de função.</span><span class="sxs-lookup"><span data-stu-id="a5c0e-116">Go toohello Azure portal and locate your function app.</span></span>

2. <span data-ttu-id="a5c0e-117">Clique em **Nova Função** > **TimerTrigger JavaScript**.</span><span class="sxs-lookup"><span data-stu-id="a5c0e-117">Click **New Function** > **TimerTrigger-JavaScript**.</span></span> 

3. <span data-ttu-id="a5c0e-118">Nome de função Olá **FunctionsBindingsDemo1**, introduza um valor de expressão de cron de `0/10 * * * * *` para **agenda**e, em seguida, clique em **criar**.</span><span class="sxs-lookup"><span data-stu-id="a5c0e-118">Name hello function **FunctionsBindingsDemo1**, enter a cron expression value of `0/10 * * * * *` for **Schedule**, and then click **Create**.</span></span>
   
    ![Adicionar uma função acionada por temporizador](./media/functions-create-an-azure-connected-function/new-trigger-timer-function.png)

    <span data-ttu-id="a5c0e-120">Criou uma função acionada por temporizador que é executada a cada 10 segundos.</span><span class="sxs-lookup"><span data-stu-id="a5c0e-120">You have now created a timer triggered function that runs every 10 seconds.</span></span>

5. <span data-ttu-id="a5c0e-121">No Olá **desenvolver** separador, clique em **registos** e ver a atividade de Olá no registo de Olá.</span><span class="sxs-lookup"><span data-stu-id="a5c0e-121">On hello **Develop** tab, click **Logs** and view hello activity in hello log.</span></span> <span data-ttu-id="a5c0e-122">Verá uma entrada de registo escrita a cada 10 segundos.</span><span class="sxs-lookup"><span data-stu-id="a5c0e-122">You see a log entry written every 10 seconds.</span></span>
   
    ![Ver Olá registo tooverify Olá função funciona](./media/functions-create-an-azure-connected-function/functionsbindingsdemo1-view-log.png)

## <a name="add-a-message-queue-output-binding"></a><span data-ttu-id="a5c0e-124">Adicionar um enlace de saída da fila de mensagens</span><span class="sxs-lookup"><span data-stu-id="a5c0e-124">Add a message queue output binding</span></span>

1. <span data-ttu-id="a5c0e-125">No Olá **integrar** separador, escolha **nova saída** > **armazenamento de filas do Azure** > **selecione**.</span><span class="sxs-lookup"><span data-stu-id="a5c0e-125">On hello **Integrate** tab, choose **New Output** > **Azure Queue Storage** > **Select**.</span></span>

    ![Adicionar uma função de temporizador de acionador](./media/functions-create-an-azure-connected-function/functionsbindingsdemo1-integrate-tab.png)

2. <span data-ttu-id="a5c0e-127">Introduza `myQueueItem` para **nome do parâmetro mensagem** e `functions-bindings` para **nome da fila**, selecione um existente **ligação de conta de armazenamento** ou clique em **novo** toocreate um armazenamento de ligação de conta e, em seguida, clique em **guardar**.</span><span class="sxs-lookup"><span data-stu-id="a5c0e-127">Enter `myQueueItem` for **Message parameter name** and `functions-bindings` for **Queue name**, select an existing **Storage account connection** or click **new** toocreate a storage account connection, and then click **Save**.</span></span>  

    ![Criar a fila de armazenamento de toohello de enlace de saída de Olá](./media/functions-create-an-azure-connected-function/functionsbindingsdemo1-integrate-tab2.png)

1. <span data-ttu-id="a5c0e-129">Novamente no Olá **desenvolver** separador, acrescentar Olá função toohello de código a seguir:</span><span class="sxs-lookup"><span data-stu-id="a5c0e-129">Back in hello **Develop** tab, append hello following code toohello function:</span></span>
   
    ```javascript
   
    function myQueueItem() 
    {
        return {
            msg: "some message goes here",
            time: "time goes here"
        }
    }
   
    ```
2. <span data-ttu-id="a5c0e-130">Localizar Olá *se* instrução cerca de linha 9 da função de Olá e seguinte de Olá de inserção código após essa instrução.</span><span class="sxs-lookup"><span data-stu-id="a5c0e-130">Locate hello *if* statement around line 9 of hello function, and insert hello following code after that statement.</span></span>
   
    ```javascript
   
    var toBeQed = myQueueItem();
    toBeQed.time = timeStamp;
    context.bindings.myQueueItem = toBeQed;
   
    ```  
   
    <span data-ttu-id="a5c0e-131">Este código cria um **myQueueItem** e define o **tempo** propriedade toohello atual timeStamp.</span><span class="sxs-lookup"><span data-stu-id="a5c0e-131">This code creates a **myQueueItem** and sets its **time** property toohello current timeStamp.</span></span> <span data-ttu-id="a5c0e-132">Em seguida, adiciona Olá nova fila item toohello contexto **myQueueItem** enlace.</span><span class="sxs-lookup"><span data-stu-id="a5c0e-132">It then adds hello new queue item toohello context's **myQueueItem** binding.</span></span>

3. <span data-ttu-id="a5c0e-133">Clique em **Guardar e executar**.</span><span class="sxs-lookup"><span data-stu-id="a5c0e-133">Click **Save and Run**.</span></span>

## <a name="view-storage-updates-by-using-storage-explorer"></a><span data-ttu-id="a5c0e-134">Ver atualizações de armazenamento através do Explorador de Armazenamento</span><span class="sxs-lookup"><span data-stu-id="a5c0e-134">View storage updates by using Storage Explorer</span></span>
<span data-ttu-id="a5c0e-135">Pode verificar se a função está a funcionar visualizando as mensagens na fila de Olá que criou.</span><span class="sxs-lookup"><span data-stu-id="a5c0e-135">You can verify that your function is working by viewing messages in hello queue you created.</span></span>  <span data-ttu-id="a5c0e-136">Pode ligar a fila de armazenamento tooyour utilizando Cloud Explorer no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a5c0e-136">You can connect tooyour storage queue by using Cloud Explorer in Visual Studio.</span></span> <span data-ttu-id="a5c0e-137">No entanto, o portal de Olá torna conta de armazenamento de tooyour tooconnect fácil utilizando o Explorador de armazenamento do Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="a5c0e-137">However, hello portal makes it easy tooconnect tooyour storage account by using Microsoft Azure Storage Explorer.</span></span>

1. <span data-ttu-id="a5c0e-138">No Olá **integrar** separador, clique numa fila de saída do enlace > **documentação**, em seguida, Mostrar Olá cadeia de ligação para a sua conta de armazenamento e copie o valor de Olá.</span><span class="sxs-lookup"><span data-stu-id="a5c0e-138">In hello **Integrate** tab, click your queue output binding > **Documentation**, then unhide hello Connection String for your storage account and copy hello value.</span></span> <span data-ttu-id="a5c0e-139">Utilize esta conta de armazenamento do valor tooconnect tooyour.</span><span class="sxs-lookup"><span data-stu-id="a5c0e-139">You use this value tooconnect tooyour storage account.</span></span>

    ![Transferir o Explorador de Armazenamento do Azure](./media/functions-create-an-azure-connected-function/functionsbindingsdemo1-integrate-tab3.png)


2. <span data-ttu-id="a5c0e-141">Se ainda não o fez, transfira e instale o [Explorador de Armazenamento do Microsoft Azure](http://storageexplorer.com).</span><span class="sxs-lookup"><span data-stu-id="a5c0e-141">If you haven't already done so, download and install [Microsoft Azure Storage Explorer](http://storageexplorer.com).</span></span> 
 
3. <span data-ttu-id="a5c0e-142">No Explorador de armazenamento, clique em Olá ligar tooAzure ícone de armazenamento, cole a cadeia de ligação de Olá no campo Olá e conclua o Assistente de Olá.</span><span class="sxs-lookup"><span data-stu-id="a5c0e-142">In Storage Explorer, click hello connect tooAzure Storage icon, paste hello connection string in hello field, and complete hello wizard.</span></span>

    ![Explorador de Armazenamento adicionar uma ligação](./media/functions-create-an-azure-connected-function/functionsbindingsdemo1-storage-explorer.png)

4. <span data-ttu-id="a5c0e-144">Em **Local e anexado**, expanda **contas do Storage** > a conta do storage > **filas** > **enlaces de funções**e certifique-se de que as mensagens são escritas toohello fila.</span><span class="sxs-lookup"><span data-stu-id="a5c0e-144">Under **Local and attached**, expand **Storage Accounts** > your storage account > **Queues** > **functions-bindings** and verify that messages are written toohello queue.</span></span>

    ![Vista de mensagens em fila Olá](./media/functions-create-an-azure-connected-function/functionsbindings-azure-storage-explorer.png)

    <span data-ttu-id="a5c0e-146">Se a fila de Olá não existe ou está vazia, não há provavelmente um problema com o enlace de função ou o código.</span><span class="sxs-lookup"><span data-stu-id="a5c0e-146">If hello queue does not exist or is empty, there is most likely a problem with your function binding or code.</span></span>

## <a name="create-a-function-that-reads-from-hello-queue"></a><span data-ttu-id="a5c0e-147">Criar uma função que lê a partir da fila de Olá</span><span class="sxs-lookup"><span data-stu-id="a5c0e-147">Create a function that reads from hello queue</span></span>

<span data-ttu-id="a5c0e-148">Agora que configurou a serem adicionadas toohello fila de mensagens, pode criar outra função que lê a partir da fila de Olá e escritas de paginações hello permanentemente mensagens tooan tabela de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="a5c0e-148">Now that you have messages being added toohello queue, you can create another function that reads from hello queue and writes hello messages permanently tooan Azure Storage table.</span></span>

1. <span data-ttu-id="a5c0e-149">Clique em **Nova Função** > **QueueTrigger CSharp**.</span><span class="sxs-lookup"><span data-stu-id="a5c0e-149">Click **New Function** > **QueueTrigger-CSharp**.</span></span> 
 
2. <span data-ttu-id="a5c0e-150">Nome de função Olá `FunctionsBindingsDemo2`, introduza **enlaces de funções** no Olá **nome da fila** campo, selecione uma conta de armazenamento existente ou criar um e, em seguida, clique em **criar**.</span><span class="sxs-lookup"><span data-stu-id="a5c0e-150">Name hello function `FunctionsBindingsDemo2`, enter **functions-bindings** in hello **Queue name** field, select an existing storage account or create one, and then click **Create**.</span></span>

    ![Adicionar uma função de temporizador de fila de saída](./media/functions-create-an-azure-connected-function/function-demo2-new-function.png) 

3. <span data-ttu-id="a5c0e-152">(Opcional) Pode verificar que a nova função de Olá funciona através da visualização nova fila de Olá no Explorador de armazenamento como antes.</span><span class="sxs-lookup"><span data-stu-id="a5c0e-152">(Optional) You can verify that hello new function works by viewing hello new queue in Storage Explorer as before.</span></span> <span data-ttu-id="a5c0e-153">Também pode utilizar o Cloud Explorer no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a5c0e-153">You can also use Cloud Explorer in Visual Studio.</span></span>  

4. <span data-ttu-id="a5c0e-154">(Opcional) Atualizar Olá **enlaces de funções** fila e repare que itens foram removidos da fila de Olá.</span><span class="sxs-lookup"><span data-stu-id="a5c0e-154">(Optional) Refresh hello **functions-bindings** queue and notice that items have been removed from hello queue.</span></span> <span data-ttu-id="a5c0e-155">Olá remoção ocorre porque a função Olá está vinculada toohello **enlaces de funções** como uma entrada da função da acionador e Olá lê fila Olá da fila.</span><span class="sxs-lookup"><span data-stu-id="a5c0e-155">hello removal occurs because hello function is bound toohello **functions-bindings** queue as an input trigger and hello function reads hello queue.</span></span> 
 
## <a name="add-a-table-output-binding"></a><span data-ttu-id="a5c0e-156">Adicionar um enlace de saída de tabela</span><span class="sxs-lookup"><span data-stu-id="a5c0e-156">Add a table output binding</span></span>

1. <span data-ttu-id="a5c0e-157">Em FunctionsBindingsDemo2, clique em **Integrar** > **Nova Saída** > **Armazenamento de Tabelas do Azure** > **Selecionar**.</span><span class="sxs-lookup"><span data-stu-id="a5c0e-157">In FunctionsBindingsDemo2, click **Integrate** > **New Output** > **Azure Table Storage** > **Select**.</span></span>

    ![Adicionar uma tabela de armazenamento do Azure do enlace tooan](./media/functions-create-an-azure-connected-function/functionsbindingsdemo2-integrate-tab.png) 

2. <span data-ttu-id="a5c0e-159">Introduza `functionbindings` para **Nome da tabela** e `myTable` para **Nome do parâmetro de tabela**, escolha um **Ligação da conta de armazenamento** ou crie uma nova e, em seguida, clique em **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="a5c0e-159">Enter `functionbindings` for **Table name** and `myTable` for **Table parameter name**, choose a **Storage account connection** or create a new one, and then click **Save**.</span></span>

    ![Configurar o vínculo de tabela de armazenamento Olá](./media/functions-create-an-azure-connected-function/functionsbindingsdemo2-integrate-tab2.png)
   
3. <span data-ttu-id="a5c0e-161">No Olá **desenvolver** separador, substitua o código de função existente Olá seguinte Olá:</span><span class="sxs-lookup"><span data-stu-id="a5c0e-161">In hello **Develop** tab, replace hello existing function code with hello following:</span></span>
   
    ```cs
    
    using System;
    
    public static void Run(QItem myQueueItem, ICollector<TableItem> myTable, TraceWriter log)
    {    
        TableItem myItem = new TableItem
        {
            PartitionKey = "key",
            RowKey = Guid.NewGuid().ToString(),
            Time = DateTime.Now.ToString("hh.mm.ss.ffffff"),
            Msg = myQueueItem.Msg,
            OriginalTime = myQueueItem.Time    
        };
        
        // Add hello item toohello table binding collection.
        myTable.Add(myItem);
    
        log.Verbose($"C# Queue trigger function processed: {myItem.RowKey} | {myItem.Msg} | {myItem.Time}");
    }
    
    public class TableItem
    {
        public string PartitionKey {get; set;}
        public string RowKey {get; set;}
        public string Time {get; set;}
        public string Msg {get; set;}
        public string OriginalTime {get; set;}
    }
    
    public class QItem
    {
        public string Msg { get; set;}
        public string Time { get; set;}
    }
    ```
    <span data-ttu-id="a5c0e-162">Olá **TableItem** classe representa uma linha na tabela de armazenamento Olá e adicionar Olá item toohello `myTable` coleção de **TableItem** objetos.</span><span class="sxs-lookup"><span data-stu-id="a5c0e-162">hello **TableItem** class represents a row in hello storage table, and you add hello item toohello `myTable` collection of **TableItem** objects.</span></span> <span data-ttu-id="a5c0e-163">Tem de definir Olá **PartitionKey** e **RowKey** propriedades toobe tooinsert possível na tabela de Olá.</span><span class="sxs-lookup"><span data-stu-id="a5c0e-163">You must set hello **PartitionKey** and **RowKey** properties toobe able tooinsert into hello table.</span></span>

4. <span data-ttu-id="a5c0e-164">Clique em **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="a5c0e-164">Click **Save**.</span></span>  <span data-ttu-id="a5c0e-165">Por fim, pode verificar Olá função funciona através da visualização de tabela Olá no Explorador de armazenamento ou Visual Studio Cloud Explorer.</span><span class="sxs-lookup"><span data-stu-id="a5c0e-165">Finally, you can verify hello function works by viewing hello table in Storage explorer or Visual Studio Cloud Explorer.</span></span>

5. <span data-ttu-id="a5c0e-166">(Opcional) Na sua conta do storage no Explorador de armazenamento, expanda **tabelas** > **functionsbindings** e certifique-se de que as linhas são adicionadas toohello tabela.</span><span class="sxs-lookup"><span data-stu-id="a5c0e-166">(Optional) In your storage account in Storage Explorer, expand **Tables** > **functionsbindings** and verify that rows are added toohello table.</span></span> <span data-ttu-id="a5c0e-167">Pode fazê-lo Olá mesmo no Cloud Explorer no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a5c0e-167">You can do hello same in Cloud Explorer in Visual Studio.</span></span>

    ![Vista de linhas na tabela de Olá](./media/functions-create-an-azure-connected-function/functionsbindings-azure-storage-explorer2.png)

    <span data-ttu-id="a5c0e-169">Se a tabela de Olá não existe ou está vazia, não há provavelmente um problema com o enlace de função ou o código.</span><span class="sxs-lookup"><span data-stu-id="a5c0e-169">If hello table does not exist or is empty, there is most likely a problem with your function binding or code.</span></span> 
 
[!INCLUDE [More binding information](../../includes/functions-bindings-next-steps.md)]

## <a name="next-steps"></a><span data-ttu-id="a5c0e-170">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="a5c0e-170">Next steps</span></span>
<span data-ttu-id="a5c0e-171">Para obter mais informações sobre as funções do Azure, consulte Olá os seguintes tópicos:</span><span class="sxs-lookup"><span data-stu-id="a5c0e-171">For more information about Azure Functions, see hello following topics:</span></span>

* [<span data-ttu-id="a5c0e-172">Referência para programadores das Funções do Azure</span><span class="sxs-lookup"><span data-stu-id="a5c0e-172">Azure Functions developer reference</span></span>](functions-reference.md)  
  <span data-ttu-id="a5c0e-173">Referência para programadores para codificar funções e definir acionadores e enlaces.</span><span class="sxs-lookup"><span data-stu-id="a5c0e-173">Programmer reference for coding functions and defining triggers and bindings.</span></span>
* [<span data-ttu-id="a5c0e-174">Testar as Funções do Azure</span><span class="sxs-lookup"><span data-stu-id="a5c0e-174">Testing Azure Functions</span></span>](functions-test-a-function.md)  
  <span data-ttu-id="a5c0e-175">Descreve várias ferramentas e técnicas para testar as suas funções.</span><span class="sxs-lookup"><span data-stu-id="a5c0e-175">Describes various tools and techniques for testing your functions.</span></span>
* [<span data-ttu-id="a5c0e-176">Como tooscale das funções do Azure</span><span class="sxs-lookup"><span data-stu-id="a5c0e-176">How tooscale Azure Functions</span></span>](functions-scale.md)  
  <span data-ttu-id="a5c0e-177">Aborda os planos de serviço disponíveis com as funções do Azure, incluindo o plano de alojamento de consumo de Olá e como toochoose Olá plano adequado.</span><span class="sxs-lookup"><span data-stu-id="a5c0e-177">Discusses service plans available with Azure Functions, including hello Consumption hosting plan, and how toochoose hello right plan.</span></span> 

[!INCLUDE [Getting help note](../../includes/functions-get-help.md)]

