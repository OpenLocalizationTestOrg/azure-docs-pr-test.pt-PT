---
title: "aaaGet começar a utilizar os tópicos de Service Bus do Azure e as subscrições | Microsoft Docs"
description: "Grave uma aplicação da consola C# que utilize tópicos e subscrições das mensagens do Service Bus."
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: service-bus-messaging
ms.devlang: tbd
ms.topic: hero-article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 06/30/2017
ms.author: sethm
ms.openlocfilehash: 619d602599d97ecff2ded0681a383b19f1a8b7ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-service-bus-topics"></a>Introdução aos tópicos do Service Bus

[!INCLUDE [service-bus-selector-topics](../../includes/service-bus-selector-topics.md)]

## <a name="what-will-be-accomplished"></a>O que será efetuado

Este tutorial abrange Olá os seguintes passos:

1. Crie um espaço de nomes do Service Bus, utilizando Olá portal do Azure.
2. Crie um tópico do Service Bus, utilizando Olá portal do Azure.
3. Crie um tópico de toothat da subscrição Service Bus, utilizando Olá portal do Azure.
4. Escreva um toosend de aplicação de consola um tópico de toohello da mensagem.
5. Escreva um tooreceive de aplicação de consola essa mensagem da subscrição Olá.

## <a name="prerequisites"></a>Pré-requisitos

1. [Visual Studio 2015 ou superior](http://www.visualstudio.com). Exemplos de Olá neste tutorial utilizam o Visual Studio 2017.
2. Uma subscrição do Azure.

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="1-create-a-namespace-using-hello-azure-portal"></a>1. Criar um espaço de nomes utilizando Olá portal do Azure

Se já criou um espaço de nomes de mensagens do Service Bus, avance toohello [criar um tópico com Olá portal do Azure](#2-create-a-topic-using-the-azure-portal) secção.

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="2-create-a-topic-using-hello-azure-portal"></a>2. Criar um tópico com Olá portal do Azure

1. Inicie sessão no toohello [portal do Azure][azure-portal].
2. No painel de navegação esquerdo Olá do portal de Olá, clique em **Service Bus** (se não vir **Service Bus**, clique em **mais serviços**).
3. Clique em Olá espaço de nomes no qual gostaria de tópico de Olá toocreate. é apresentado o painel de descrição geral do espaço de nomes de Olá:
   
    ![Criar um tópico][createtopic1]
4. No Olá **espaço de nomes do Service Bus** painel, clique em **tópicos**, em seguida, clique em **Adicionar tópico**.
   
    ![Selecionar tópicos][createtopic2]
5. Introduza um nome para o tópico Olá e desmarque Olá **ativar a criação de partições** opção. Deixe Olá outras opções com os respetivos valores predefinidos.
   
    ![Selecionar Novo][createtopic3]
6. Na Olá parte inferior do painel de Olá, clique em **criar**.

## <a name="3-create-a-subscription-toohello-topic"></a>3. Criar um tópico de toohello de subscrição

1. No painel de recursos portal Olá, clique Olá espaço de nomes que criou no passo 1, em seguida, clique no nome do tópico Olá que criou no passo 2.
2. Top Olá do painel de descrição geral de Olá, clique em Olá plus assinar junto demasiado**subscrição** tooadd um tópico de toothis de subscrição.

    ![Criar subscrição][createtopic4]

3. Introduza um nome para a subscrição de Olá. Deixe Olá outras opções com os respetivos valores predefinidos.

## <a name="4-send-messages-toohello-topic"></a>4. Enviar tópico toohello de mensagens

tópico de toohello de mensagens toosend, vamos escrever uma aplicação de consola c# com o Visual Studio.

### <a name="create-a-console-application"></a>Criar uma aplicação de consola

Abra o Visual Studio e crie um novo projeto de **Aplicação de consola (.NET Framework)**.

### <a name="add-hello-service-bus-nuget-package"></a>Adicionar o pacote NuGet do Service Bus de Olá

1. Clique no projeto Olá recém-criado e selecione **gerir pacotes NuGet**.
2. Clique em Olá **procurar** separador, procure **Microsoft Azure Service Bus**e, em seguida, selecione Olá **Windowsazure** item. Clique em **instalar** toocomplete Olá instalação, em seguida, feche esta caixa de diálogo.
   
    ![Selecionar um pacote NuGet][nuget-pkg]

### <a name="write-some-code-toosend-a-message-toohello-topic"></a>Escrever algum código toosend um tópico de toohello mensagem

1. Adicione Olá seguinte `using` topo de toohello declaração do ficheiro Program.cs de Olá.
   
    ```csharp
    using Microsoft.ServiceBus.Messaging;
    ```
2. Adicionar Olá seguinte código toohello `Main` método. Conjunto Olá `connectionString` obtida ao criar o espaço de nomes de Olá e definir da cadeia de ligação de variável toohello `topicName` toohello nome que utilizou durante a criação de tópico Olá.
   
    ```csharp
    var connectionString = "<your connection string>";
    var topicName = "<your topic name>";
   
    var client = TopicClient.CreateFromConnectionString(connectionString, topicName);
    var message = new BrokeredMessage("This is a test message!");

    Console.WriteLine(String.Format("Message body: {0}", message.GetBody<String>()));
    Console.WriteLine(String.Format("Message id: {0}", message.MessageId));

    client.Send(message);

    Console.WriteLine("Message successfully sent! Press ENTER tooexit program");
    Console.ReadLine();
    ```
   
    O ficheiro Program.cs deve ter o seguinte aspeto.
   
    ```csharp
    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Text;
    using System.Threading.Tasks;
    using Microsoft.ServiceBus.Messaging;

    namespace tsend
    {
        class Program
        {
            static void Main(string[] args)
            {
                var connectionString = "Endpoint=sb://<your namespace>.servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=<your key>";
                var topicName = "<your topic name>";

                var client = TopicClient.CreateFromConnectionString(connectionString, topicName);
                var message = new BrokeredMessage("This is a test message!");

                Console.WriteLine(String.Format("Message body: {0}", message.GetBody<String>()));
                Console.WriteLine(String.Format("Message id: {0}", message.MessageId));

                client.Send(message);

                Console.WriteLine("Message successfully sent! Press ENTER tooexit program");
                Console.ReadLine();
            }
        }
    }
    ```
3. Execute o programa Olá e consulte Olá portal do Azure: clique no nome de Olá o tópico no espaço de nomes de Olá **descrição geral** painel. tópico de Olá **Essentials** é apresentado o painel. Em subscrições de Olá listadas quase Olá parte inferior do painel de Olá, tenha em atenção que Olá **contagem de mensagens** valor para cada subscrição deve ser 1. Cada vez que executar a aplicação de remetente Olá sem obter mensagens hello (conforme descrito na secção seguinte Olá), este valor aumenta por 1. Tenha também em atenção que tamanho atual de Olá de Olá de incrementos do tópico Olá **atual** valor no Olá **Essentials** painel sempre que a aplicação Olá adiciona uma mensagem toohello tópico/subscrição.
   
      ![Tamanho da mensagem][topic-message]

## <a name="5-receive-messages-from-hello-subscription"></a>5. Receber mensagens de subscrição de Olá

1. mensagem de saudação tooreceive ou mensagens que acabámos de enviar, crie uma nova aplicação de consola e adicione um pacote NuGet do Service Bus do referência toohello, semelhante aplicação remetente anterior toohello.
2. Adicione Olá seguinte `using` topo de toohello declaração do ficheiro Program.cs de Olá.
   
    ```csharp
    using Microsoft.ServiceBus.Messaging;
    ```
3. Adicionar Olá seguinte código toohello `Main` método. Conjunto Olá `connectionString` obtida ao criar o espaço de nomes de Olá e definir da cadeia de ligação de variável toohello `topicName` toohello nome que utilizou durante a criação de tópico Olá.
   
    ```csharp
    var connectionString = "<your connection string>";
    var topicName = "<your topic name>";
   
    var client = SubscriptionClient.CreateFromConnectionString(connectionString, topicName, "<your subscription name>");
   
    client.OnMessage(message =>
    {
      Console.WriteLine(String.Format("Message body: {0}", message.GetBody<String>()));
      Console.WriteLine(String.Format("Message id: {0}", message.MessageId));
    });
   
    Console.WriteLine("Press ENTER tooexit program");
    Console.ReadLine();
    ```
   
    O ficheiro Program.cs deve ter o seguinte aspeto:
   
    ```csharp
    using System;
    using Microsoft.ServiceBus.Messaging;
   
    namespace GettingStartedWithTopics
    {
      class Program
      {
        static void Main(string[] args)
        {
          var connectionString = "Endpoint=sb://<your namespace>.servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=<your key>";;
          var topicName = "<your topic name>";
   
          var client = SubscriptionClient.CreateFromConnectionString(connectionString, topicName, "<your subscription name>");
   
          client.OnMessage(message =>
          {
            Console.WriteLine(String.Format("Message body: {0}", message.GetBody<String>()));
            Console.WriteLine(String.Format("Message id: {0}", message.MessageId));
          });

          Console.WriteLine("Press ENTER tooexit program");   
          Console.ReadLine();
        }
      }
    }
    ```
4. Executar Olá programa e consulte o portal de Olá novamente. Tenha em atenção que Olá **contagem de mensagens** e **atual** os valores são agora 0.
   
    ![Comprimento do tópico][topic-message-receive]

Parabéns! Criou agora um tópico e uma subscrição, enviou uma mensagem e recebeu essa mensagem.

## <a name="next-steps"></a>Passos seguintes

Consulte a nossa [repositório do GitHub com exemplos](https://github.com/Azure/azure-service-bus/tree/master/samples) que demonstra Algumas das Olá funcionalidades de mensagens do Service Bus mais avançadas.

<!--Image references-->

[nuget-pkg]: ./media/service-bus-dotnet-how-to-use-topics-subscriptions/nuget-package.png
[topic-message]: ./media/service-bus-dotnet-how-to-use-topics-subscriptions/topic-message.png
[topic-message-receive]: ./media/service-bus-dotnet-how-to-use-topics-subscriptions/topic-message-receive.png
[createtopic1]: ./media/service-bus-dotnet-how-to-use-topics-subscriptions/create-topic1.png
[createtopic2]: ./media/service-bus-dotnet-how-to-use-topics-subscriptions/create-topic2.png
[createtopic3]: ./media/service-bus-dotnet-how-to-use-topics-subscriptions/create-topic3.png
[createtopic4]: ./media/service-bus-dotnet-how-to-use-topics-subscriptions/create-topic4.png
[github-samples]: https://github.com/Azure-Samples/azure-servicebus-messaging-samples
[azure-portal]: https://portal.azure.com
