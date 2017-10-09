---
title: "aaaCreate uma função no Azure acionado por um webhook genérico | Microsoft Docs"
description: "Utilize as funções do Azure toocreate uma função sem servidor que é invocada por um webhook no Azure."
services: functions
documentationcenter: na
author: ggailey777
manager: cfowler
editor: 
tags: 
ms.assetid: fafc10c0-84da-4404-b4fa-eea03c7bf2b1
ms.service: functions
ms.devlang: multiple
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 08/12/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 0a4868da91d216c8d20930ce7ec82eaa059c75ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-function-triggered-by-a-generic-webhook"></a><span data-ttu-id="b14c5-103">Criar uma função acionada por um webhook genérico</span><span class="sxs-lookup"><span data-stu-id="b14c5-103">Create a function triggered by a generic webhook</span></span>

<span data-ttu-id="b14c5-104">As funções do Azure permite-lhe executar o seu código num ambiente sem servidor sem ter toofirst criar uma VM ou publicar uma aplicação web.</span><span class="sxs-lookup"><span data-stu-id="b14c5-104">Azure Functions lets you execute your code in a serverless environment without having toofirst create a VM or publish a web application.</span></span> <span data-ttu-id="b14c5-105">Por exemplo, pode configurar toobe uma função acionada por um alerta gerado pelo Monitor do Azure.</span><span class="sxs-lookup"><span data-stu-id="b14c5-105">For example, you can configure a function toobe triggered by an alert raised by Azure Monitor.</span></span> <span data-ttu-id="b14c5-106">Este tópico mostra como tooexecute código c# quando um grupo de recursos é adicionado tooyour subscrição.</span><span class="sxs-lookup"><span data-stu-id="b14c5-106">This topic shows you how tooexecute C# code when a resource group is added tooyour subscription.</span></span>   

![Webhook genérico acionada funcionar em Olá portal do Azure](./media/functions-create-generic-webhook-triggered-function/function-completed.png)

## <a name="prerequisites"></a><span data-ttu-id="b14c5-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="b14c5-108">Prerequisites</span></span> 

<span data-ttu-id="b14c5-109">toocomplete neste tutorial:</span><span class="sxs-lookup"><span data-stu-id="b14c5-109">toocomplete this tutorial:</span></span>

+ <span data-ttu-id="b14c5-110">Se não tiver uma subscrição do Azure, crie uma [conta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) antes de começar.</span><span class="sxs-lookup"><span data-stu-id="b14c5-110">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [functions-portal-favorite-function-apps](../../includes/functions-portal-favorite-function-apps.md)]

## <a name="create-an-azure-function-app"></a><span data-ttu-id="b14c5-111">Criar uma aplicação de Funções do Azure</span><span class="sxs-lookup"><span data-stu-id="b14c5-111">Create an Azure Function app</span></span>

[!INCLUDE [Create function app Azure portal](../../includes/functions-create-function-app-portal.md)]

<span data-ttu-id="b14c5-112">Em seguida, crie uma função na nova aplicação de função Olá.</span><span class="sxs-lookup"><span data-stu-id="b14c5-112">Next, you create a function in hello new function app.</span></span>

## <span data-ttu-id="b14c5-113"><a name="create-function"></a>Criar uma função de webhook genérico acionada</span><span class="sxs-lookup"><span data-stu-id="b14c5-113"><a name="create-function"></a>Create a generic webhook triggered function</span></span>

1. <span data-ttu-id="b14c5-114">Expanda a sua aplicação de função e clique em Olá  **+**  no botão seguinte demasiado**funções**.</span><span class="sxs-lookup"><span data-stu-id="b14c5-114">Expand your function app and click hello **+** button next too**Functions**.</span></span> <span data-ttu-id="b14c5-115">Se esta função é hello um primeiro na sua aplicação de função, selecione **função personalizada**.</span><span class="sxs-lookup"><span data-stu-id="b14c5-115">If this function is hello first one in your function app, select **Custom function**.</span></span> <span data-ttu-id="b14c5-116">Esta ação apresenta o conjunto completo de Olá dos modelos de função.</span><span class="sxs-lookup"><span data-stu-id="b14c5-116">This displays hello complete set of function templates.</span></span>

    ![Página de início rápido de funções no Olá portal do Azure](./media/functions-create-generic-webhook-triggered-function/add-first-function.png)

2. <span data-ttu-id="b14c5-118">Selecione Olá **WebHook genérico - c#** modelo.</span><span class="sxs-lookup"><span data-stu-id="b14c5-118">Select hello **Generic WebHook - C#** template.</span></span> <span data-ttu-id="b14c5-119">Escreva um nome para a função de c#, em seguida, selecione **criar**.</span><span class="sxs-lookup"><span data-stu-id="b14c5-119">Type a name for your C# function, then select **Create**.</span></span>

     ![Criar uma função de webhook genérico acionada no Olá portal do Azure](./media/functions-create-generic-webhook-triggered-function/functions-create-generic-webhook-trigger.png) 

2. <span data-ttu-id="b14c5-121">Na sua nova função, clique em **<> / Get função URL**, em seguida, copie e guarde o valor de Olá.</span><span class="sxs-lookup"><span data-stu-id="b14c5-121">In your new function, click **</> Get function URL**, then copy and save hello value.</span></span> <span data-ttu-id="b14c5-122">Utilize o valor tooconfigure Olá webhook.</span><span class="sxs-lookup"><span data-stu-id="b14c5-122">You use this value tooconfigure hello webhook.</span></span> 

    ![Rever o código de função Olá](./media/functions-create-generic-webhook-triggered-function/functions-copy-function-url.png)
         
<span data-ttu-id="b14c5-124">Em seguida, crie um ponto final de webhook num alerta de registo de atividade no Monitor do Azure.</span><span class="sxs-lookup"><span data-stu-id="b14c5-124">Next, you create a webhook endpoint in an activity log alert in Azure Monitor.</span></span> 

## <a name="create-an-activity-log-alert"></a><span data-ttu-id="b14c5-125">Criar um alerta de registo de atividade</span><span class="sxs-lookup"><span data-stu-id="b14c5-125">Create an activity log alert</span></span>

1. <span data-ttu-id="b14c5-126">No portal do Azure de Olá, navegue toohello **Monitor** serviço, selecione **alertas**e clique em **Adicionar alerta de registo de atividade**.</span><span class="sxs-lookup"><span data-stu-id="b14c5-126">In hello Azure portal, navigate toohello **Monitor** service, select **Alerts**, and click **Add activity log alert**.</span></span>   

    ![Monitorizar](./media/functions-create-generic-webhook-triggered-function/functions-monitor-add-alert.png)

2. <span data-ttu-id="b14c5-128">Utilize as definições de Olá conforme especificado na tabela de Olá:</span><span class="sxs-lookup"><span data-stu-id="b14c5-128">Use hello settings as specified in hello table:</span></span>

    ![Criar um alerta de registo de atividade](./media/functions-create-generic-webhook-triggered-function/functions-monitor-add-alert-settings.png)

    | <span data-ttu-id="b14c5-130">Definição</span><span class="sxs-lookup"><span data-stu-id="b14c5-130">Setting</span></span>      |  <span data-ttu-id="b14c5-131">Valor sugerido</span><span class="sxs-lookup"><span data-stu-id="b14c5-131">Suggested value</span></span>   | <span data-ttu-id="b14c5-132">Descrição</span><span class="sxs-lookup"><span data-stu-id="b14c5-132">Description</span></span>                              |
    | ------------ |  ------- | -------------------------------------------------- |
    | <span data-ttu-id="b14c5-133">**Nome de alerta de registo de atividade**</span><span class="sxs-lookup"><span data-stu-id="b14c5-133">**Activity log alert name**</span></span> | <span data-ttu-id="b14c5-134">recursos-grupo-criar-alerta</span><span class="sxs-lookup"><span data-stu-id="b14c5-134">resource-group-create-alert</span></span> | <span data-ttu-id="b14c5-135">Nome do alerta de registo de atividade Olá.</span><span class="sxs-lookup"><span data-stu-id="b14c5-135">Name of hello activity log alert.</span></span> |
    | <span data-ttu-id="b14c5-136">**Subscrição**</span><span class="sxs-lookup"><span data-stu-id="b14c5-136">**Subscription**</span></span> | <span data-ttu-id="b14c5-137">A sua subscrição</span><span class="sxs-lookup"><span data-stu-id="b14c5-137">Your subscription</span></span> | <span data-ttu-id="b14c5-138">subscrição Olá que estiver a utilizar para este tutorial.</span><span class="sxs-lookup"><span data-stu-id="b14c5-138">hello subscription you are using for this tutorial.</span></span> | 
    |  <span data-ttu-id="b14c5-139">**Grupo de Recursos**</span><span class="sxs-lookup"><span data-stu-id="b14c5-139">**Resource Group**</span></span> | <span data-ttu-id="b14c5-140">myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="b14c5-140">myResourceGroup</span></span> | <span data-ttu-id="b14c5-141">grupo de recursos de Olá recursos alerta Olá implementadas.</span><span class="sxs-lookup"><span data-stu-id="b14c5-141">hello resource group that hello alert resources are deployed to.</span></span> <span data-ttu-id="b14c5-142">Utilizar Olá mesmo grupo de recursos, como a sua aplicação de função torna mais fácil tooclean cópias de segurança depois de concluir o tutorial Olá.</span><span class="sxs-lookup"><span data-stu-id="b14c5-142">Using hello same resource group as your function app makes it easier tooclean up after you complete hello tutorial.</span></span> |
    | <span data-ttu-id="b14c5-143">**Categoria de evento**</span><span class="sxs-lookup"><span data-stu-id="b14c5-143">**Event category**</span></span> | <span data-ttu-id="b14c5-144">Administrativos</span><span class="sxs-lookup"><span data-stu-id="b14c5-144">Administrative</span></span> | <span data-ttu-id="b14c5-145">Esta categoria inclui as alterações efetuadas tooAzure recursos.</span><span class="sxs-lookup"><span data-stu-id="b14c5-145">This category includes changes made tooAzure resources.</span></span>  |
    | <span data-ttu-id="b14c5-146">**Tipo de recurso**</span><span class="sxs-lookup"><span data-stu-id="b14c5-146">**Resource type**</span></span> | <span data-ttu-id="b14c5-147">Grupos de recursos</span><span class="sxs-lookup"><span data-stu-id="b14c5-147">Resource groups</span></span> | <span data-ttu-id="b14c5-148">Filtra a agrupar atividades tooresource alertas.</span><span class="sxs-lookup"><span data-stu-id="b14c5-148">Filters alerts tooresource group activities.</span></span> |
    | <span data-ttu-id="b14c5-149">**Grupo de Recursos**</span><span class="sxs-lookup"><span data-stu-id="b14c5-149">**Resource Group**</span></span><br/><span data-ttu-id="b14c5-150">e **recursos**</span><span class="sxs-lookup"><span data-stu-id="b14c5-150">and **Resource**</span></span> | <span data-ttu-id="b14c5-151">Todos</span><span class="sxs-lookup"><span data-stu-id="b14c5-151">All</span></span> | <span data-ttu-id="b14c5-152">Monitorize todos os recursos.</span><span class="sxs-lookup"><span data-stu-id="b14c5-152">Monitor all resources.</span></span> |
    | <span data-ttu-id="b14c5-153">**Nome da operação**</span><span class="sxs-lookup"><span data-stu-id="b14c5-153">**Operation name**</span></span> | <span data-ttu-id="b14c5-154">Criar Grupo de Recursos</span><span class="sxs-lookup"><span data-stu-id="b14c5-154">Create Resource Group</span></span> | <span data-ttu-id="b14c5-155">Filtros de operações de toocreate de alertas.</span><span class="sxs-lookup"><span data-stu-id="b14c5-155">Filters alerts toocreate operations.</span></span> |
    | <span data-ttu-id="b14c5-156">**Nível**</span><span class="sxs-lookup"><span data-stu-id="b14c5-156">**Level**</span></span> | <span data-ttu-id="b14c5-157">Informativo</span><span class="sxs-lookup"><span data-stu-id="b14c5-157">Informational</span></span> | <span data-ttu-id="b14c5-158">Inclua alertas informativos de nível.</span><span class="sxs-lookup"><span data-stu-id="b14c5-158">Include informational level alerts.</span></span> | 
    | <span data-ttu-id="b14c5-159">**Estado**</span><span class="sxs-lookup"><span data-stu-id="b14c5-159">**Status**</span></span> | <span data-ttu-id="b14c5-160">Bem-sucedido</span><span class="sxs-lookup"><span data-stu-id="b14c5-160">Succeeded</span></span> | <span data-ttu-id="b14c5-161">Filtros tooactions de alertas que foram concluídos com êxito.</span><span class="sxs-lookup"><span data-stu-id="b14c5-161">Filters alerts tooactions that have completed successfully.</span></span> |
    | <span data-ttu-id="b14c5-162">**Grupo de ação**</span><span class="sxs-lookup"><span data-stu-id="b14c5-162">**Action group**</span></span> | <span data-ttu-id="b14c5-163">novo</span><span class="sxs-lookup"><span data-stu-id="b14c5-163">New</span></span> | <span data-ttu-id="b14c5-164">Crie um novo grupo de ação, que define Olá ação demora quando for gerado um alerta.</span><span class="sxs-lookup"><span data-stu-id="b14c5-164">Create a new action group, which defines hello action takes when an alert is raised.</span></span> |
    | <span data-ttu-id="b14c5-165">**Nome do grupo de ação**</span><span class="sxs-lookup"><span data-stu-id="b14c5-165">**Action group name**</span></span> | <span data-ttu-id="b14c5-166">função de webhook</span><span class="sxs-lookup"><span data-stu-id="b14c5-166">function-webhook</span></span> | <span data-ttu-id="b14c5-167">Um grupo de ação do nome tooidentify Olá.</span><span class="sxs-lookup"><span data-stu-id="b14c5-167">A name tooidentify hello action group.</span></span>  | 
    | <span data-ttu-id="b14c5-168">**Nome abreviado**</span><span class="sxs-lookup"><span data-stu-id="b14c5-168">**Short name**</span></span> | <span data-ttu-id="b14c5-169">funcwebhook</span><span class="sxs-lookup"><span data-stu-id="b14c5-169">funcwebhook</span></span> | <span data-ttu-id="b14c5-170">Um nome abreviado do grupo de ação de Olá.</span><span class="sxs-lookup"><span data-stu-id="b14c5-170">A short name for hello action group.</span></span> |  

3. <span data-ttu-id="b14c5-171">No **ações**, adicionar uma ação com as definições de Olá conforme especificado na tabela de Olá:</span><span class="sxs-lookup"><span data-stu-id="b14c5-171">In **Actions**, add an action using hello settings as specified in hello table:</span></span> 

    ![Adicionar um grupo de ação](./media/functions-create-generic-webhook-triggered-function/functions-monitor-add-alert-settings-2.png)

    | <span data-ttu-id="b14c5-173">Definição</span><span class="sxs-lookup"><span data-stu-id="b14c5-173">Setting</span></span>      |  <span data-ttu-id="b14c5-174">Valor sugerido</span><span class="sxs-lookup"><span data-stu-id="b14c5-174">Suggested value</span></span>   | <span data-ttu-id="b14c5-175">Descrição</span><span class="sxs-lookup"><span data-stu-id="b14c5-175">Description</span></span>                              |
    | ------------ |  ------- | -------------------------------------------------- |
    | <span data-ttu-id="b14c5-176">**Nome**</span><span class="sxs-lookup"><span data-stu-id="b14c5-176">**Name**</span></span> | <span data-ttu-id="b14c5-177">CallFunctionWebhook</span><span class="sxs-lookup"><span data-stu-id="b14c5-177">CallFunctionWebhook</span></span> | <span data-ttu-id="b14c5-178">Um nome para a ação de Olá.</span><span class="sxs-lookup"><span data-stu-id="b14c5-178">A name for hello action.</span></span> |
    | <span data-ttu-id="b14c5-179">**Tipo de ação**</span><span class="sxs-lookup"><span data-stu-id="b14c5-179">**Action type**</span></span> | <span data-ttu-id="b14c5-180">Webhook</span><span class="sxs-lookup"><span data-stu-id="b14c5-180">Webhook</span></span> | <span data-ttu-id="b14c5-181">alerta de toohello Olá resposta é que é chamado um URL do Webhook.</span><span class="sxs-lookup"><span data-stu-id="b14c5-181">hello response toohello alert is that a Webhook URL is called.</span></span> |
    | <span data-ttu-id="b14c5-182">**Detalhes**</span><span class="sxs-lookup"><span data-stu-id="b14c5-182">**Details**</span></span> | <span data-ttu-id="b14c5-183">URL de função</span><span class="sxs-lookup"><span data-stu-id="b14c5-183">Function URL</span></span> | <span data-ttu-id="b14c5-184">Cole no URL do webhook Olá da função de Olá que copiou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="b14c5-184">Paste in hello webhook URL of hello function that you copied earlier.</span></span> |<span data-ttu-id="b14c5-185">v</span><span class="sxs-lookup"><span data-stu-id="b14c5-185">v</span></span>

4. <span data-ttu-id="b14c5-186">Clique em **OK** toocreate Olá alerta e ação de grupo.</span><span class="sxs-lookup"><span data-stu-id="b14c5-186">Click **OK** toocreate hello alert and action group.</span></span>  

<span data-ttu-id="b14c5-187">chama-se agora Olá webhook quando é criado um grupo de recursos na sua subscrição.</span><span class="sxs-lookup"><span data-stu-id="b14c5-187">hello webhook is now called when a resource group is created in your subscription.</span></span> <span data-ttu-id="b14c5-188">Em seguida, atualize o código de Olá no seu Olá toohandle de função dados de registo JSON no corpo de Olá de pedido de Olá.</span><span class="sxs-lookup"><span data-stu-id="b14c5-188">Next, you update hello code in your function toohandle hello JSON log data in hello body of hello request.</span></span>   

## <a name="update-hello-function-code"></a><span data-ttu-id="b14c5-189">Atualizar o código de função Olá</span><span class="sxs-lookup"><span data-stu-id="b14c5-189">Update hello function code</span></span>

1. <span data-ttu-id="b14c5-190">Navegue tooyour back-a aplicação de função no portal de Olá e expandir a sua função.</span><span class="sxs-lookup"><span data-stu-id="b14c5-190">Navigate back tooyour function app in hello portal, and expand your function.</span></span> 

2. <span data-ttu-id="b14c5-191">Substitua o código de script de Olá c# na função de Olá no portal de Olá com Olá seguinte código:</span><span class="sxs-lookup"><span data-stu-id="b14c5-191">Replace hello C# script code in hello function in hello portal with hello following code:</span></span>

    ```csharp
    #r "Newtonsoft.Json"
    
    using System;
    using System.Net;
    using Newtonsoft.Json;
    using Newtonsoft.Json.Linq;
    
    public static async Task<object> Run(HttpRequestMessage req, TraceWriter log)
    {
        log.Info($"Webhook was triggered!");
    
        // Get hello activityLog object from hello JSON in hello message body.
        string jsonContent = await req.Content.ReadAsStringAsync();
        JToken activityLog = JObject.Parse(jsonContent.ToString())
            .SelectToken("data.context.activityLog");
    
        // Return an error if hello resource in hello activity log isn't a resource group. 
        if (activityLog == null || !string.Equals((string)activityLog["resourceType"], 
            "Microsoft.Resources/subscriptions/resourcegroups"))
        {
            log.Error("An error occured");
            return req.CreateResponse(HttpStatusCode.BadRequest, new
            {
                error = "Unexpected message payload or wrong alert received."
            });
        }
    
        // Write information about hello created resource group toohello streaming log.
        log.Info(string.Format("Resource group '{0}' was {1} on {2}.",
            (string)activityLog["resourceGroupName"],
            ((string)activityLog["subStatus"]).ToLower(), 
            (DateTime)activityLog["submissionTimestamp"]));
    
        return req.CreateResponse(HttpStatusCode.OK);    
    }
    ```

<span data-ttu-id="b14c5-192">Agora pode testar a função de Olá ao criar um novo grupo de recursos na sua subscrição.</span><span class="sxs-lookup"><span data-stu-id="b14c5-192">Now you can test hello function by creating a new resource group in your subscription.</span></span>

## <a name="test-hello-function"></a><span data-ttu-id="b14c5-193">Testar a função de Olá</span><span class="sxs-lookup"><span data-stu-id="b14c5-193">Test hello function</span></span>

1. <span data-ttu-id="b14c5-194">Clique em ícone de grupo de recursos de Olá no lado esquerdo de Olá do portal do Azure, selecione de Olá **+ adicionar**, escreva um **nome do grupo de recursos**e selecione **criar** toocreate um grupo de recursos em branco.</span><span class="sxs-lookup"><span data-stu-id="b14c5-194">Click hello resource group icon in hello left of hello Azure portal, select **+ Add**, type a **Resource group name**, and select **Create** toocreate an empty resource group.</span></span>
    
    ![Crie um grupo de recursos.](./media/functions-create-generic-webhook-triggered-function/functions-create-resource-group.png)

2. <span data-ttu-id="b14c5-196">Volte a função tooyour e expanda Olá **registos** janela.</span><span class="sxs-lookup"><span data-stu-id="b14c5-196">Go back tooyour function and expand hello **Logs** window.</span></span> <span data-ttu-id="b14c5-197">Depois de criar o grupo de recursos de Olá, hello acionadores de alerta de registo de atividade Olá webhook e executa a função de Olá.</span><span class="sxs-lookup"><span data-stu-id="b14c5-197">After hello resource group is created, hello activity log alert triggers hello webhook and hello function executes.</span></span> <span data-ttu-id="b14c5-198">Pode ver o nome Olá Olá novo grupo de recursos escrito toohello registos.</span><span class="sxs-lookup"><span data-stu-id="b14c5-198">You see hello name of hello new resource group written toohello logs.</span></span>  

    ![Adicione uma definição de aplicação de teste.](./media/functions-create-generic-webhook-triggered-function/function-view-logs.png)

3. <span data-ttu-id="b14c5-200">(Opcional) Voltar atrás e elimine o grupo de recursos de Olá que criou.</span><span class="sxs-lookup"><span data-stu-id="b14c5-200">(Optional) Go back and delete hello resource group that you created.</span></span> <span data-ttu-id="b14c5-201">Tenha em atenção que esta actividade não acionar a função de Olá.</span><span class="sxs-lookup"><span data-stu-id="b14c5-201">Note that this activity doesn't trigger hello function.</span></span> <span data-ttu-id="b14c5-202">Isto acontece porque eliminar operações são filtradas por alerta Olá.</span><span class="sxs-lookup"><span data-stu-id="b14c5-202">This is because delete operations are filtered out by hello alert.</span></span> 

## <a name="clean-up-resources"></a><span data-ttu-id="b14c5-203">Limpar recursos</span><span class="sxs-lookup"><span data-stu-id="b14c5-203">Clean up resources</span></span>

[!INCLUDE [Next steps note](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a><span data-ttu-id="b14c5-204">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="b14c5-204">Next steps</span></span>

<span data-ttu-id="b14c5-205">Foi criada com uma função que é executado quando é recebido um pedido de um webhook genérico.</span><span class="sxs-lookup"><span data-stu-id="b14c5-205">You have created a function that runs when a request is received from a generic webhook.</span></span> 

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

<span data-ttu-id="b14c5-206">Para obter mais informações sobre os acionadores de webhook, veja [Enlaces de HTTP e webhook das Funções do Azure](functions-bindings-http-webhook.md).</span><span class="sxs-lookup"><span data-stu-id="b14c5-206">For more information about webhook triggers, see [Azure Functions HTTP and webhook bindings](functions-bindings-http-webhook.md).</span></span> <span data-ttu-id="b14c5-207">toolearn mais informações sobre desenvolver as funções em c#, consulte [referência para programadores script Azure funções c#](functions-reference-csharp.md).</span><span class="sxs-lookup"><span data-stu-id="b14c5-207">toolearn more about developing functions in C#, see [Azure Functions C# script developer reference](functions-reference-csharp.md).</span></span>

