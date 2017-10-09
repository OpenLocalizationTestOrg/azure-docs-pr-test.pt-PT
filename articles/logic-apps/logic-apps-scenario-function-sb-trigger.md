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
# <a name="scenario-trigger-a-logic-app-with-azure-functions-and-azure-service-bus"></a>Cenário: Acionar uma aplicação lógica com as funções do Azure e o Service Bus do Azure

Pode utilizar as funções do Azure toocreate um acionador para uma aplicação lógica quando precisar de toodeploy uma execução longa escuta ou tarefas. Por exemplo, pode criar uma função que escuta uma fila e, em seguida, acionados imediatamente uma aplicação lógica como um acionador de push.

## <a name="build-hello-logic-app"></a>Criar aplicação de lógica de Olá
Neste exemplo, poderá ter uma função em execução para cada aplicação lógica que necessita de toobe acionado. Em primeiro lugar, crie uma aplicação lógica que tem um acionador de pedido HTTP. esse ponto final de chamadas de função de Olá sempre que é recebida uma mensagem de fila.  

1. Crie uma aplicação lógica.
2. Selecione Olá **Manual - quando é recebido um pedido HTTP** acionador.
   Opcionalmente, pode especificar um toouse de esquema JSON com a mensagem da fila de Olá utilizando uma ferramenta como o [jsonschema.net](http://jsonschema.net). Cole o esquema de Olá no acionador Olá. Esquemas ajudam designer Olá compreender a forma de Olá das propriedades de dados e fluem no sentido de Olá mais facilmente através de Olá fluxo de trabalho.
2. Adiciona quaisquer passos adicionais que pretenda toooccur depois é recebida uma mensagem de fila. Por exemplo, envie uma mensagem de e-mail através do Office 365.  
3. Guarde Olá lógica toogenerate Olá chamada de retorno URL da aplicação para a aplicação de lógica de toothis de Acionador de Olá. URL de Olá é apresentado no cartão de Acionador de Olá.

![chamada de retorno Olá URL aparece no cartão de Acionador de Olá][1]

## <a name="build-hello-function"></a>Criar função Olá
Em seguida, tem de criar uma função que age como acionador Olá e escuta toohello fila.

1. No Olá [portal das funções do Azure](https://functions.azure.com/signin), selecione **nova função**e, em seguida, selecione Olá **ServiceBusQueueTrigger - c#** modelo.
   
    ![Portal de funções do Azure][2]
2. Configurar Olá ligação toohello fila do Service Bus, que utiliza Olá SDK do Service Bus `OnMessageReceive()` serviço de escuta.
3. Gravar um função básico toocall Olá logic app ponto final (criado anteriormente) utilizando a mensagem da fila de saudação como um acionador. Eis um exemplo completo de uma função. exemplo de Olá utiliza um `application/json` tipo de conteúdo de mensagem, mas pode alterar este tipo conforme necessário.
   
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

tootest, adicione uma mensagem da fila através de uma ferramenta como o [Explorador do Service Bus](https://github.com/paolosalvatori/ServiceBusExplorer). Consulte a aplicação de lógica de Olá acionados imediatamente após a função de Olá recebe a mensagem de saudação.

<!-- Image References -->
[1]: ./media/logic-apps-scenario-function-sb-trigger/manualtrigger.png
[2]: ./media/logic-apps-scenario-function-sb-trigger/newqueuetriggerfunction.png
