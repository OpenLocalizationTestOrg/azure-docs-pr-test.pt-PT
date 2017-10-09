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
# <a name="how-toolog-events-tooazure-event-hubs-in-azure-api-management"></a>Como toolog eventos tooAzure Event Hubs na API Management do Azure
Os Hubs de eventos do Azure é um serviço de entrada de dados altamente dimensionável que pode ingerir milhões de eventos por segundo para que possa processar e analisar Olá quantidades enormes de dados produzidos pelos seus dispositivos e aplicações ligados. Os Event Hubs atuam como Olá "porta da frente" para um pipeline de eventos e, depois dos dados são recolhidos para um hub de eventos, podem ser transformado e armazenados através de qualquer fornecedor de análise em tempo real ou adaptadores de criação de batches/armazenamento. Os Event Hubs desacoplam a produção de Olá de um fluxo de eventos do consumo desses eventos, Olá para que os consumidores de eventos possam aceder eventos Olá na sua própria agenda.

Este artigo é um complemento toohello [integrar a gestão de API do Azure com os Event Hubs](https://azure.microsoft.com/documentation/videos/integrate-azure-api-management-with-event-hubs/) vídeo e descreve como eventos de API Management toolog utilizar Event Hubs do Azure.

## <a name="create-an-azure-event-hub"></a>Criar um Hub de eventos do Azure
toocreate um novo Hub de eventos, o início de sessão toohello [portal clássico do Azure](https://manage.windowsazure.com) e clique em **novo**->**serviços aplicacionais**->**Service Bus**  -> **Hub de eventos**->**criação rápida**. Introduza um nome de Hub de eventos, região, selecione uma subscrição e selecione um espaço de nomes. Se ainda não criou anteriormente um espaço de nomes pode criar um, escrevendo um nome na Olá **espaço de nomes** caixa de texto. Depois de todas as propriedades estiverem configuradas, clique em **criar um novo Hub de eventos** toocreate Olá Hub de eventos.

![Criar o hub de eventos][create-event-hub]

Em seguida, navegue até toohello **configurar** separador para o seu novo Hub de eventos e criar dois **partilhado políticas de acesso**. Nome Olá primeiro **Sending** e atribua-lhe **enviar** permissões.

![Política de envio][sending-policy]

Nome Olá segunda **receber**, atribua-lhe **escutar** permissões e clique em **guardar**.

![Receber a política][receiving-policy]

Cada política de acesso partilhado permite que aplicações toosend e receber eventos tooand Olá Hub de eventos. cadeias de ligação de Olá tooaccess para estas políticas, navegue toohello **Dashboard** separador de Olá Hub de eventos e clique em **informações de ligação**.

![Cadeia de ligação][event-hub-dashboard]

Olá **Sending** cadeia de ligação é utilizada quando o registo de eventos e Olá **receber** cadeia de ligação é utilizada ao transferir eventos a partir de Olá Hub de eventos.

![Cadeia de ligação][event-hub-connection-string]

## <a name="create-an-api-management-logger"></a>Criar um registo de API Management
Agora que tem um Hub de eventos, o passo seguinte Olá é tooconfigure um [registador](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-logger-entity) na gestão de API do serviço para que possa registar eventos toohello Hub de eventos.

Registadores de API Management são configurados utilizando Olá [API de REST de gestão de API](http://aka.ms/smapi). Antes de utilizar Olá REST API para Olá pela primeira vez, reveja Olá [pré-requisitos](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/api-management-rest#Prerequisites) e certifique-se de que tem [ativada acesso toohello REST API](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/api-management-rest#EnableRESTAPI).

toocreate um registo, se um pedido HTTP PUT Olá seguir o modelo de URL a utilizar.

`https://{your service}.management.azure-api.net/loggers/{new logger name}?api-version=2014-02-14-preview`

* Substitua `{your service}` com o nome de Olá da sua instância do serviço de API Management.
* Substitua `{new logger name}` com o nome pretendido Olá para o novo registo. Irá referenciar este nome quando configurar Olá [registo-eventhub](https://msdn.microsoft.com/library/azure/dn894085.aspx#log-to-eventhub) política

Adicione Olá seguintes cabeçalhos toohello pedido.

* Tipo de conteúdo: application/json
* Autorização: SharedAccessSignature 58...
  * Para obter instruções sobre como gerar Olá `SharedAccessSignature` consulte [autenticação de API do REST de gestão do Azure API](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-authentication).

Especifique o corpo do pedido Olá Olá seguir o modelo a utilizar.

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

* `type`tem de ser definido demasiado`AzureEventHub`.
* `description`Fornece uma descrição opcional do registador de Olá e pode ser uma cadeia de comprimento zero se assim o desejar.
* `credentials`contém Olá `name` e `connectionString` do seu Hub de eventos do Azure.

Quando efetuar o pedido de Olá, se o registo de Olá é criado um código de estado de `201 Created` é devolvido.

> [!NOTE]
> Para outros códigos de retorno possíveis e os respetivos motivos, consulte [criar um registo](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-logger-entity#PUT). toosee como executar outras operações, tais como a lista, update e delete, consulte Olá [registador](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-logger-entity) documentação de entidade.
>
>

## <a name="configure-log-to-eventhubs-policies"></a>Configurar políticas de registo-eventhubs
Depois de ter configurado o registo na API Management, pode configurar os eventos do registo para eventhubs políticas toolog Olá assim o desejar. Olá registo-eventhubs política pode ser utilizada em qualquer um dos Olá secção de política de saída Olá ou secção de entrada de política.

políticas de tooconfigure, início de sessão toohello [portal do Azure](https://portal.azure.com), navegue até o serviço de API Management tooyour e, em **portal do publicador** tooaccess Olá portal do publicador.

![Portal do publicador][publisher-portal]

Clique em **políticas** no menu de API Management Olá Olá esquerda, selecione de produto pretendido Olá e API e clique em **Adicionar política**. Neste exemplo, estamos a adicionar uma política toohello **API eco** no Olá **ilimitada** produto.

![Adicionar política][add-policy]

Posicione o cursor no Olá `inbound` política secção e clique em Olá **registo tooEventHub** Olá de tooinsert política `log-to-eventhub` modelo de política de instrução.

![Editor de políticas][event-hub-policy]

```xml
<log-to-eventhub logger-id ='logger-id'>
  @( string.Join(",", DateTime.UtcNow, context.Deployment.ServiceName, context.RequestId, context.Request.IpAddress, context.Operation.Name))
</log-to-eventhub>
```

Substitua `logger-id` com o nome de Olá do registador de API Management Olá que configurou no passo anterior Olá.

Pode utilizar uma expressão que devolve uma cadeia como valor de Olá para Olá `log-to-eventhub` elemento. Neste exemplo, uma cadeia contendo Olá data e hora, nome do serviço, id do pedido, endereço de ip do pedido e o nome da operação é registada.

Clique em **guardar** toosave Olá atualizar a configuração da política. Assim que é guardado Olá política estar ativa e os eventos são registado toohello designado Hub de eventos.

## <a name="next-steps"></a>Passos seguintes
* Saiba mais sobre os Event Hubs do Azure
  * [Introdução ao Event Hubs do Azure](../event-hubs/event-hubs-c-getstarted-send.md)
  * [Receber mensagens com o EventProcessorHost](../event-hubs/event-hubs-dotnet-standard-getstarted-receive-eph.md)
  * [Guia de programação dos Event Hubs](../event-hubs/event-hubs-programming-guide.md)
* Saiba mais sobre a integração de API Management e do Event Hubs
  * [Referência de entidade de registo](https://docs.microsoft.com/rest/api/apimanagement/loggers)
  * [referência de política de registo para eventhub](https://docs.microsoft.com/azure/api-management/api-management-advanced-policies#log-to-eventhub)
  * [Monitorizar as suas APIs com API Management do Azure, os Event Hubs e Runscope](api-management-log-to-eventhub-sample.md)    

## <a name="watch-a-video-walkthrough"></a>Veja um vídeo com instruções
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
