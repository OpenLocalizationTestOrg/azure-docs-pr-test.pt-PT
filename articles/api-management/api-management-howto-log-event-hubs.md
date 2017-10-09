---
title: aaaHow toolog eventos tooAzure Event Hubs na API Management do Azure | Microsoft Docs
description: Saiba como toolog eventos tooAzure Event Hubs na API Management do Azure.
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 88f6507d-7460-4eb2-bffd-76025b73f8c4
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 09ca65fc48a874467c6662858f7594e9b19fcdb9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toolog-events-tooazure-event-hubs-in-azure-api-management"></a><span data-ttu-id="e1743-103">Como toolog eventos tooAzure Event Hubs na API Management do Azure</span><span class="sxs-lookup"><span data-stu-id="e1743-103">How toolog events tooAzure Event Hubs in Azure API Management</span></span>
<span data-ttu-id="e1743-104">Os Hubs de eventos do Azure é um serviço de entrada de dados altamente dimensionável que pode ingerir milhões de eventos por segundo para que possa processar e analisar Olá quantidades enormes de dados produzidos pelos seus dispositivos e aplicações ligados.</span><span class="sxs-lookup"><span data-stu-id="e1743-104">Azure Event Hubs is a highly scalable data ingress service that can ingest millions of events per second so that you can process and analyze hello massive amounts of data produced by your connected devices and applications.</span></span> <span data-ttu-id="e1743-105">Os Event Hubs atuam como Olá "porta da frente" para um pipeline de eventos e, depois dos dados são recolhidos para um hub de eventos, podem ser transformado e armazenados através de qualquer fornecedor de análise em tempo real ou adaptadores de criação de batches/armazenamento.</span><span class="sxs-lookup"><span data-stu-id="e1743-105">Event Hubs acts as hello "front door" for an event pipeline, and once data is collected into an event hub, it can be transformed and stored using any real-time analytics provider or batching/storage adapters.</span></span> <span data-ttu-id="e1743-106">Os Event Hubs desacoplam a produção de Olá de um fluxo de eventos do consumo desses eventos, Olá para que os consumidores de eventos possam aceder eventos Olá na sua própria agenda.</span><span class="sxs-lookup"><span data-stu-id="e1743-106">Event Hubs decouples hello production of a stream of events from hello consumption of those events, so that event consumers can access hello events on their own schedule.</span></span>

<span data-ttu-id="e1743-107">Este artigo é um complemento toohello [integrar a gestão de API do Azure com os Event Hubs](https://azure.microsoft.com/documentation/videos/integrate-azure-api-management-with-event-hubs/) vídeo e descreve como eventos de API Management toolog utilizar Event Hubs do Azure.</span><span class="sxs-lookup"><span data-stu-id="e1743-107">This article is a companion toohello [Integrate Azure API Management with Event Hubs](https://azure.microsoft.com/documentation/videos/integrate-azure-api-management-with-event-hubs/) video and describes how toolog API Management events using Azure Event Hubs.</span></span>

## <a name="create-an-azure-event-hub"></a><span data-ttu-id="e1743-108">Criar um Hub de eventos do Azure</span><span class="sxs-lookup"><span data-stu-id="e1743-108">Create an Azure Event Hub</span></span>
<span data-ttu-id="e1743-109">toocreate um novo Hub de eventos, o início de sessão toohello [portal clássico do Azure](https://manage.windowsazure.com) e clique em **novo**->**serviços aplicacionais**->**Service Bus**  -> **Hub de eventos**->**criação rápida**.</span><span class="sxs-lookup"><span data-stu-id="e1743-109">toocreate a new Event Hub, sign-in toohello [Azure classic portal](https://manage.windowsazure.com) and click **New**->**App Services**->**Service Bus**->**Event Hub**->**Quick Create**.</span></span> <span data-ttu-id="e1743-110">Introduza um nome de Hub de eventos, região, selecione uma subscrição e selecione um espaço de nomes.</span><span class="sxs-lookup"><span data-stu-id="e1743-110">Enter an Event Hub name, region, select a subscription, and select a namespace.</span></span> <span data-ttu-id="e1743-111">Se ainda não criou anteriormente um espaço de nomes pode criar um, escrevendo um nome na Olá **espaço de nomes** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="e1743-111">If you haven't previously created a namespace you can create one by typing a name in hello **Namespace** textbox.</span></span> <span data-ttu-id="e1743-112">Depois de todas as propriedades estiverem configuradas, clique em **criar um novo Hub de eventos** toocreate Olá Hub de eventos.</span><span class="sxs-lookup"><span data-stu-id="e1743-112">Once all properties are configured, click **Create a new Event Hub** toocreate hello Event Hub.</span></span>

![Criar o hub de eventos][create-event-hub]

<span data-ttu-id="e1743-114">Em seguida, navegue até toohello **configurar** separador para o seu novo Hub de eventos e criar dois **partilhado políticas de acesso**.</span><span class="sxs-lookup"><span data-stu-id="e1743-114">Next, navigate toohello **Configure** tab for your new Event Hub and create two **shared access policies**.</span></span> <span data-ttu-id="e1743-115">Nome Olá primeiro **Sending** e atribua-lhe **enviar** permissões.</span><span class="sxs-lookup"><span data-stu-id="e1743-115">Name hello first one **Sending** and give it **Send** permissions.</span></span>

![Política de envio][sending-policy]

<span data-ttu-id="e1743-117">Nome Olá segunda **receber**, atribua-lhe **escutar** permissões e clique em **guardar**.</span><span class="sxs-lookup"><span data-stu-id="e1743-117">Name hello second one **Receiving**, give it **Listen** permissions, and click **Save**.</span></span>

![Receber a política][receiving-policy]

<span data-ttu-id="e1743-119">Cada política de acesso partilhado permite que aplicações toosend e receber eventos tooand Olá Hub de eventos.</span><span class="sxs-lookup"><span data-stu-id="e1743-119">Each shared access policy allows applications toosend and receive events tooand from hello Event Hub.</span></span> <span data-ttu-id="e1743-120">cadeias de ligação de Olá tooaccess para estas políticas, navegue toohello **Dashboard** separador de Olá Hub de eventos e clique em **informações de ligação**.</span><span class="sxs-lookup"><span data-stu-id="e1743-120">tooaccess hello connection strings for these policies, navigate toohello **Dashboard** tab of hello Event Hub and click **Connection information**.</span></span>

![Cadeia de ligação][event-hub-dashboard]

<span data-ttu-id="e1743-122">Olá **Sending** cadeia de ligação é utilizada quando o registo de eventos e Olá **receber** cadeia de ligação é utilizada ao transferir eventos a partir de Olá Hub de eventos.</span><span class="sxs-lookup"><span data-stu-id="e1743-122">hello **Sending** connection string is used when logging events, and hello **Receiving** connection string is used when downloading events from hello Event Hub.</span></span>

![Cadeia de ligação][event-hub-connection-string]

## <a name="create-an-api-management-logger"></a><span data-ttu-id="e1743-124">Criar um registo de API Management</span><span class="sxs-lookup"><span data-stu-id="e1743-124">Create an API Management logger</span></span>
<span data-ttu-id="e1743-125">Agora que tem um Hub de eventos, o passo seguinte Olá é tooconfigure um [registador](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-logger-entity) na gestão de API do serviço para que possa registar eventos toohello Hub de eventos.</span><span class="sxs-lookup"><span data-stu-id="e1743-125">Now that you have an Event Hub, hello next step is tooconfigure a [Logger](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-logger-entity) in your API Management service so that it can log events toohello Event Hub.</span></span>

<span data-ttu-id="e1743-126">Registadores de API Management são configurados utilizando Olá [API de REST de gestão de API](http://aka.ms/smapi).</span><span class="sxs-lookup"><span data-stu-id="e1743-126">API Management loggers are configured using hello [API Management REST API](http://aka.ms/smapi).</span></span> <span data-ttu-id="e1743-127">Antes de utilizar Olá REST API para Olá pela primeira vez, reveja Olá [pré-requisitos](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/api-management-rest#Prerequisites) e certifique-se de que tem [ativada acesso toohello REST API](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/api-management-rest#EnableRESTAPI).</span><span class="sxs-lookup"><span data-stu-id="e1743-127">Before using hello REST API for hello first time, review hello [prerequisites](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/api-management-rest#Prerequisites) and ensure that you have [enabled access toohello REST API](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/api-management-rest#EnableRESTAPI).</span></span>

<span data-ttu-id="e1743-128">toocreate um registo, se um pedido HTTP PUT Olá seguir o modelo de URL a utilizar.</span><span class="sxs-lookup"><span data-stu-id="e1743-128">toocreate a logger, make an HTTP PUT request using hello following URL template.</span></span>

`https://{your service}.management.azure-api.net/loggers/{new logger name}?api-version=2014-02-14-preview`

* <span data-ttu-id="e1743-129">Substitua `{your service}` com o nome de Olá da sua instância do serviço de API Management.</span><span class="sxs-lookup"><span data-stu-id="e1743-129">Replace `{your service}` with hello name of your API Management service instance.</span></span>
* <span data-ttu-id="e1743-130">Substitua `{new logger name}` com o nome pretendido Olá para o novo registo.</span><span class="sxs-lookup"><span data-stu-id="e1743-130">Replace `{new logger name}` with hello desired name for your new logger.</span></span> <span data-ttu-id="e1743-131">Irá referenciar este nome quando configurar Olá [registo-eventhub](https://msdn.microsoft.com/library/azure/dn894085.aspx#log-to-eventhub) política</span><span class="sxs-lookup"><span data-stu-id="e1743-131">You will reference this name when you configure hello [log-to-eventhub](https://msdn.microsoft.com/library/azure/dn894085.aspx#log-to-eventhub) policy</span></span>

<span data-ttu-id="e1743-132">Adicione Olá seguintes cabeçalhos toohello pedido.</span><span class="sxs-lookup"><span data-stu-id="e1743-132">Add hello following headers toohello request.</span></span>

* <span data-ttu-id="e1743-133">Tipo de conteúdo: application/json</span><span class="sxs-lookup"><span data-stu-id="e1743-133">Content-Type : application/json</span></span>
* <span data-ttu-id="e1743-134">Autorização: SharedAccessSignature 58...</span><span class="sxs-lookup"><span data-stu-id="e1743-134">Authorization : SharedAccessSignature 58...</span></span>
  * <span data-ttu-id="e1743-135">Para obter instruções sobre como gerar Olá `SharedAccessSignature` consulte [autenticação de API do REST de gestão do Azure API](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-authentication).</span><span class="sxs-lookup"><span data-stu-id="e1743-135">For instructions on generating hello `SharedAccessSignature` see [Azure API Management REST API Authentication](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-authentication).</span></span>

<span data-ttu-id="e1743-136">Especifique o corpo do pedido Olá Olá seguir o modelo a utilizar.</span><span class="sxs-lookup"><span data-stu-id="e1743-136">Specify hello request body using hello following template.</span></span>

```json
{
  "type" : "AzureEventHub",
  "description" : "Sample logger description",
  "credentials" : {
    "name" : "Name of hello Event Hub from hello Azure Classic Portal",
    "connectionString" : "Endpoint=Event Hub Sender connection string"
    }
}
```

* <span data-ttu-id="e1743-137">`type`tem de ser definido demasiado`AzureEventHub`.</span><span class="sxs-lookup"><span data-stu-id="e1743-137">`type` must be set too`AzureEventHub`.</span></span>
* <span data-ttu-id="e1743-138">`description`Fornece uma descrição opcional do registador de Olá e pode ser uma cadeia de comprimento zero se assim o desejar.</span><span class="sxs-lookup"><span data-stu-id="e1743-138">`description` provides an optional description of hello logger and can be a zero length string if desired.</span></span>
* <span data-ttu-id="e1743-139">`credentials`contém Olá `name` e `connectionString` do seu Hub de eventos do Azure.</span><span class="sxs-lookup"><span data-stu-id="e1743-139">`credentials` contains hello `name` and `connectionString` of your Azure Event Hub.</span></span>

<span data-ttu-id="e1743-140">Quando efetuar o pedido de Olá, se o registo de Olá é criado um código de estado de `201 Created` é devolvido.</span><span class="sxs-lookup"><span data-stu-id="e1743-140">When you make hello request, if hello logger is created a status code of `201 Created` is returned.</span></span>

> [!NOTE]
> <span data-ttu-id="e1743-141">Para outros códigos de retorno possíveis e os respetivos motivos, consulte [criar um registo](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-logger-entity#PUT).</span><span class="sxs-lookup"><span data-stu-id="e1743-141">For other possible return codes and their reasons, see [Create a Logger](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-logger-entity#PUT).</span></span> <span data-ttu-id="e1743-142">toosee como executar outras operações, tais como a lista, update e delete, consulte Olá [registador](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-logger-entity) documentação de entidade.</span><span class="sxs-lookup"><span data-stu-id="e1743-142">toosee how perform other operations such as list, update, and delete, see hello [Logger](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-logger-entity) entity documentation.</span></span>
>
>

## <a name="configure-log-to-eventhubs-policies"></a><span data-ttu-id="e1743-143">Configurar políticas de registo-eventhubs</span><span class="sxs-lookup"><span data-stu-id="e1743-143">Configure log-to-eventhubs policies</span></span>
<span data-ttu-id="e1743-144">Depois de ter configurado o registo na API Management, pode configurar os eventos do registo para eventhubs políticas toolog Olá assim o desejar.</span><span class="sxs-lookup"><span data-stu-id="e1743-144">Once your logger is configured in API Management, you can configure your log-to-eventhubs policies toolog hello desired events.</span></span> <span data-ttu-id="e1743-145">Olá registo-eventhubs política pode ser utilizada em qualquer um dos Olá secção de política de saída Olá ou secção de entrada de política.</span><span class="sxs-lookup"><span data-stu-id="e1743-145">hello log-to-eventhubs policy can be used in either hello inbound policy section or hello outbound policy section.</span></span>

<span data-ttu-id="e1743-146">políticas de tooconfigure, início de sessão toohello [portal do Azure](https://portal.azure.com), navegue até o serviço de API Management tooyour e, em **portal do publicador** tooaccess Olá portal do publicador.</span><span class="sxs-lookup"><span data-stu-id="e1743-146">tooconfigure policies, sign-in toohello [Azure portal](https://portal.azure.com), navigate tooyour API Management service, and click **Publisher portal** tooaccess hello publisher portal.</span></span>

![Portal do publicador][publisher-portal]

<span data-ttu-id="e1743-148">Clique em **políticas** no menu de API Management Olá Olá esquerda, selecione de produto pretendido Olá e API e clique em **Adicionar política**.</span><span class="sxs-lookup"><span data-stu-id="e1743-148">Click **Policies** in hello API Management menu on hello left, select hello desired product and API, and click **Add policy**.</span></span> <span data-ttu-id="e1743-149">Neste exemplo, estamos a adicionar uma política toohello **API eco** no Olá **ilimitada** produto.</span><span class="sxs-lookup"><span data-stu-id="e1743-149">In this example we're adding a policy toohello **Echo API** in hello **Unlimited** product.</span></span>

![Adicionar política][add-policy]

<span data-ttu-id="e1743-151">Posicione o cursor no Olá `inbound` política secção e clique em Olá **registo tooEventHub** Olá de tooinsert política `log-to-eventhub` modelo de política de instrução.</span><span class="sxs-lookup"><span data-stu-id="e1743-151">Position your cursor in hello `inbound` policy section and click hello **Log tooEventHub** policy tooinsert hello `log-to-eventhub` policy statement template.</span></span>

![Editor de políticas][event-hub-policy]

```xml
<log-to-eventhub logger-id ='logger-id'>
  @( string.Join(",", DateTime.UtcNow, context.Deployment.ServiceName, context.RequestId, context.Request.IpAddress, context.Operation.Name))
</log-to-eventhub>
```

<span data-ttu-id="e1743-153">Substitua `logger-id` com o nome de Olá do registador de API Management Olá que configurou no passo anterior Olá.</span><span class="sxs-lookup"><span data-stu-id="e1743-153">Replace `logger-id` with hello name of hello API Management logger you configured in hello previous step.</span></span>

<span data-ttu-id="e1743-154">Pode utilizar uma expressão que devolve uma cadeia como valor de Olá para Olá `log-to-eventhub` elemento.</span><span class="sxs-lookup"><span data-stu-id="e1743-154">You can use any expression that returns a string as hello value for hello `log-to-eventhub` element.</span></span> <span data-ttu-id="e1743-155">Neste exemplo, uma cadeia contendo Olá data e hora, nome do serviço, id do pedido, endereço de ip do pedido e o nome da operação é registada.</span><span class="sxs-lookup"><span data-stu-id="e1743-155">In this example a string containing hello date and time, service name, request id, request ip address, and operation name is logged.</span></span>

<span data-ttu-id="e1743-156">Clique em **guardar** toosave Olá atualizar a configuração da política.</span><span class="sxs-lookup"><span data-stu-id="e1743-156">Click **Save** toosave hello updated policy configuration.</span></span> <span data-ttu-id="e1743-157">Assim que é guardado Olá política estar ativa e os eventos são registado toohello designado Hub de eventos.</span><span class="sxs-lookup"><span data-stu-id="e1743-157">As soon as it is saved hello policy is active and events are logged toohello designated Event Hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e1743-158">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="e1743-158">Next steps</span></span>
* <span data-ttu-id="e1743-159">Saiba mais sobre os Event Hubs do Azure</span><span class="sxs-lookup"><span data-stu-id="e1743-159">Learn more about Azure Event Hubs</span></span>
  * [<span data-ttu-id="e1743-160">Introdução ao Event Hubs do Azure</span><span class="sxs-lookup"><span data-stu-id="e1743-160">Get started with Azure Event Hubs</span></span>](../event-hubs/event-hubs-c-getstarted-send.md)
  * [<span data-ttu-id="e1743-161">Receber mensagens com o EventProcessorHost</span><span class="sxs-lookup"><span data-stu-id="e1743-161">Receive messages with EventProcessorHost</span></span>](../event-hubs/event-hubs-dotnet-standard-getstarted-receive-eph.md)
  * [<span data-ttu-id="e1743-162">Guia de programação dos Event Hubs</span><span class="sxs-lookup"><span data-stu-id="e1743-162">Event Hubs programming guide</span></span>](../event-hubs/event-hubs-programming-guide.md)
* <span data-ttu-id="e1743-163">Saiba mais sobre a integração de API Management e do Event Hubs</span><span class="sxs-lookup"><span data-stu-id="e1743-163">Learn more about API Management and Event Hubs integration</span></span>
  * [<span data-ttu-id="e1743-164">Referência de entidade de registo</span><span class="sxs-lookup"><span data-stu-id="e1743-164">Logger entity reference</span></span>](https://docs.microsoft.com/rest/api/apimanagement/loggers)
  * [<span data-ttu-id="e1743-165">referência de política de registo para eventhub</span><span class="sxs-lookup"><span data-stu-id="e1743-165">log-to-eventhub policy reference</span></span>](https://docs.microsoft.com/azure/api-management/api-management-advanced-policies#log-to-eventhub)
  * [<span data-ttu-id="e1743-166">Monitorizar as suas APIs com API Management do Azure, os Event Hubs e Runscope</span><span class="sxs-lookup"><span data-stu-id="e1743-166">Monitor your APIs with Azure API Management, Event Hubs and Runscope</span></span>](api-management-log-to-eventhub-sample.md)    

## <a name="watch-a-video-walkthrough"></a><span data-ttu-id="e1743-167">Veja um vídeo com instruções</span><span class="sxs-lookup"><span data-stu-id="e1743-167">Watch a video walkthrough</span></span>
> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Integrate-Azure-API-Management-with-Event-Hubs/player]
>
>

[publisher-portal]: ./media/api-management-howto-log-event-hubs/publisher-portal.png
[create-event-hub]: ./media/api-management-howto-log-event-hubs/create-event-hub.png
[event-hub-connection-string]: ./media/api-management-howto-log-event-hubs/event-hub-connection-string.png
[event-hub-dashboard]: ./media/api-management-howto-log-event-hubs/event-hub-dashboard.png
[receiving-policy]: ./media/api-management-howto-log-event-hubs/receiving-policy.png
[sending-policy]: ./media/api-management-howto-log-event-hubs/sending-policy.png
[event-hub-policy]: ./media/api-management-howto-log-event-hubs/event-hub-policy.png
[add-policy]: ./media/api-management-howto-log-event-hubs/add-policy.png
