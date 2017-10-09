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
# <a name="get-started-with-service-bus-topics"></a><span data-ttu-id="dcfe2-103">Introdução aos tópicos do Service Bus</span><span class="sxs-lookup"><span data-stu-id="dcfe2-103">Get started with Service Bus topics</span></span>

[!INCLUDE [service-bus-selector-topics](../../includes/service-bus-selector-topics.md)]

## <a name="what-will-be-accomplished"></a><span data-ttu-id="dcfe2-104">O que será efetuado</span><span class="sxs-lookup"><span data-stu-id="dcfe2-104">What will be accomplished</span></span>

<span data-ttu-id="dcfe2-105">Este tutorial abrange Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="dcfe2-105">This tutorial covers hello following steps:</span></span>

1. <span data-ttu-id="dcfe2-106">Crie um espaço de nomes do Service Bus, utilizando Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="dcfe2-106">Create a Service Bus namespace, using hello Azure portal.</span></span>
2. <span data-ttu-id="dcfe2-107">Crie um tópico do Service Bus, utilizando Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="dcfe2-107">Create a Service Bus topic, using hello Azure portal.</span></span>
3. <span data-ttu-id="dcfe2-108">Crie um tópico de toothat da subscrição Service Bus, utilizando Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="dcfe2-108">Create a Service Bus subscription toothat topic, using hello Azure portal.</span></span>
4. <span data-ttu-id="dcfe2-109">Escreva um toosend de aplicação de consola um tópico de toohello da mensagem.</span><span class="sxs-lookup"><span data-stu-id="dcfe2-109">Write a console application toosend a message toohello topic.</span></span>
5. <span data-ttu-id="dcfe2-110">Escreva um tooreceive de aplicação de consola essa mensagem da subscrição Olá.</span><span class="sxs-lookup"><span data-stu-id="dcfe2-110">Write a console application tooreceive that message from hello subscription.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dcfe2-111">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="dcfe2-111">Prerequisites</span></span>

1. <span data-ttu-id="dcfe2-112">[Visual Studio 2015 ou superior](http://www.visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="dcfe2-112">[Visual Studio 2015 or higher](http://www.visualstudio.com).</span></span> <span data-ttu-id="dcfe2-113">Exemplos de Olá neste tutorial utilizam o Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="dcfe2-113">hello examples in this tutorial use Visual Studio 2017.</span></span>
2. <span data-ttu-id="dcfe2-114">Uma subscrição do Azure.</span><span class="sxs-lookup"><span data-stu-id="dcfe2-114">An Azure subscription.</span></span>

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="1-create-a-namespace-using-hello-azure-portal"></a><span data-ttu-id="dcfe2-115">1. Criar um espaço de nomes utilizando Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="dcfe2-115">1. Create a namespace using hello Azure portal</span></span>

<span data-ttu-id="dcfe2-116">Se já criou um espaço de nomes de mensagens do Service Bus, avance toohello [criar um tópico com Olá portal do Azure](#2-create-a-topic-using-the-azure-portal) secção.</span><span class="sxs-lookup"><span data-stu-id="dcfe2-116">If you have already created a Service Bus Messaging namespace, jump toohello [Create a topic using hello Azure portal](#2-create-a-topic-using-the-azure-portal) section.</span></span>

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="2-create-a-topic-using-hello-azure-portal"></a><span data-ttu-id="dcfe2-117">2. Criar um tópico com Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="dcfe2-117">2. Create a topic using hello Azure portal</span></span>

1. <span data-ttu-id="dcfe2-118">Inicie sessão no toohello [portal do Azure][azure-portal].</span><span class="sxs-lookup"><span data-stu-id="dcfe2-118">Log on toohello [Azure portal][azure-portal].</span></span>
2. <span data-ttu-id="dcfe2-119">No painel de navegação esquerdo Olá do portal de Olá, clique em **Service Bus** (se não vir **Service Bus**, clique em **mais serviços**).</span><span class="sxs-lookup"><span data-stu-id="dcfe2-119">In hello left navigation pane of hello portal, click **Service Bus** (if you don't see **Service Bus**, click **More services**).</span></span>
3. <span data-ttu-id="dcfe2-120">Clique em Olá espaço de nomes no qual gostaria de tópico de Olá toocreate.</span><span class="sxs-lookup"><span data-stu-id="dcfe2-120">Click hello namespace in which you would like toocreate hello topic.</span></span> <span data-ttu-id="dcfe2-121">é apresentado o painel de descrição geral do espaço de nomes de Olá:</span><span class="sxs-lookup"><span data-stu-id="dcfe2-121">hello namespace overview blade appears:</span></span>
   
    ![Criar um tópico][createtopic1]
4. <span data-ttu-id="dcfe2-123">No Olá **espaço de nomes do Service Bus** painel, clique em **tópicos**, em seguida, clique em **Adicionar tópico**.</span><span class="sxs-lookup"><span data-stu-id="dcfe2-123">In hello **Service Bus namespace** blade, click **Topics**, then click **Add topic**.</span></span>
   
    ![Selecionar tópicos][createtopic2]
5. <span data-ttu-id="dcfe2-125">Introduza um nome para o tópico Olá e desmarque Olá **ativar a criação de partições** opção.</span><span class="sxs-lookup"><span data-stu-id="dcfe2-125">Enter a name for hello topic, and uncheck hello **Enable partitioning** option.</span></span> <span data-ttu-id="dcfe2-126">Deixe Olá outras opções com os respetivos valores predefinidos.</span><span class="sxs-lookup"><span data-stu-id="dcfe2-126">Leave hello other options with their default values.</span></span>
   
    ![Selecionar Novo][createtopic3]
6. <span data-ttu-id="dcfe2-128">Na Olá parte inferior do painel de Olá, clique em **criar**.</span><span class="sxs-lookup"><span data-stu-id="dcfe2-128">At hello bottom of hello blade, click **Create**.</span></span>

## <a name="3-create-a-subscription-toohello-topic"></a><span data-ttu-id="dcfe2-129">3. Criar um tópico de toohello de subscrição</span><span class="sxs-lookup"><span data-stu-id="dcfe2-129">3. Create a subscription toohello topic</span></span>

1. <span data-ttu-id="dcfe2-130">No painel de recursos portal Olá, clique Olá espaço de nomes que criou no passo 1, em seguida, clique no nome do tópico Olá que criou no passo 2.</span><span class="sxs-lookup"><span data-stu-id="dcfe2-130">In hello portal resources pane, click hello namespace you created in step 1, then click name of hello topic you created in step 2.</span></span>
2. <span data-ttu-id="dcfe2-131">Top Olá do painel de descrição geral de Olá, clique em Olá plus assinar junto demasiado**subscrição** tooadd um tópico de toothis de subscrição.</span><span class="sxs-lookup"><span data-stu-id="dcfe2-131">A hello top of hello overview pane, click hello plus sign next too**Subscription** tooadd a subscription toothis topic.</span></span>

    ![Criar subscrição][createtopic4]

3. <span data-ttu-id="dcfe2-133">Introduza um nome para a subscrição de Olá.</span><span class="sxs-lookup"><span data-stu-id="dcfe2-133">Enter a name for hello subscription.</span></span> <span data-ttu-id="dcfe2-134">Deixe Olá outras opções com os respetivos valores predefinidos.</span><span class="sxs-lookup"><span data-stu-id="dcfe2-134">Leave hello other options with their default values.</span></span>

## <a name="4-send-messages-toohello-topic"></a><span data-ttu-id="dcfe2-135">4. Enviar tópico toohello de mensagens</span><span class="sxs-lookup"><span data-stu-id="dcfe2-135">4. Send messages toohello topic</span></span>

<span data-ttu-id="dcfe2-136">tópico de toohello de mensagens toosend, vamos escrever uma aplicação de consola c# com o Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="dcfe2-136">toosend messages toohello topic, we write a C# console application using Visual Studio.</span></span>

### <a name="create-a-console-application"></a><span data-ttu-id="dcfe2-137">Criar uma aplicação de consola</span><span class="sxs-lookup"><span data-stu-id="dcfe2-137">Create a console application</span></span>

<span data-ttu-id="dcfe2-138">Abra o Visual Studio e crie um novo projeto de **Aplicação de consola (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="dcfe2-138">Launch Visual Studio and create a new **Console app (.NET Framework)** project.</span></span>

### <a name="add-hello-service-bus-nuget-package"></a><span data-ttu-id="dcfe2-139">Adicionar o pacote NuGet do Service Bus de Olá</span><span class="sxs-lookup"><span data-stu-id="dcfe2-139">Add hello Service Bus NuGet package</span></span>

1. <span data-ttu-id="dcfe2-140">Clique no projeto Olá recém-criado e selecione **gerir pacotes NuGet**.</span><span class="sxs-lookup"><span data-stu-id="dcfe2-140">Right-click hello newly created project and select **Manage NuGet Packages**.</span></span>
2. <span data-ttu-id="dcfe2-141">Clique em Olá **procurar** separador, procure **Microsoft Azure Service Bus**e, em seguida, selecione Olá **Windowsazure** item.</span><span class="sxs-lookup"><span data-stu-id="dcfe2-141">Click hello **Browse** tab, search for **Microsoft Azure Service Bus**, and then select hello **WindowsAzure.ServiceBus** item.</span></span> <span data-ttu-id="dcfe2-142">Clique em **instalar** toocomplete Olá instalação, em seguida, feche esta caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="dcfe2-142">Click **Install** toocomplete hello installation, then close this dialog box.</span></span>
   
    ![Selecionar um pacote NuGet][nuget-pkg]

### <a name="write-some-code-toosend-a-message-toohello-topic"></a><span data-ttu-id="dcfe2-144">Escrever algum código toosend um tópico de toohello mensagem</span><span class="sxs-lookup"><span data-stu-id="dcfe2-144">Write some code toosend a message toohello topic</span></span>

1. <span data-ttu-id="dcfe2-145">Adicione Olá seguinte `using` topo de toohello declaração do ficheiro Program.cs de Olá.</span><span class="sxs-lookup"><span data-stu-id="dcfe2-145">Add hello following `using` statement toohello top of hello Program.cs file.</span></span>
   
    ```csharp
    using Microsoft.ServiceBus.Messaging;
    ```
2. <span data-ttu-id="dcfe2-146">Adicionar Olá seguinte código toohello `Main` método.</span><span class="sxs-lookup"><span data-stu-id="dcfe2-146">Add hello following code toohello `Main` method.</span></span> <span data-ttu-id="dcfe2-147">Conjunto Olá `connectionString` obtida ao criar o espaço de nomes de Olá e definir da cadeia de ligação de variável toohello `topicName` toohello nome que utilizou durante a criação de tópico Olá.</span><span class="sxs-lookup"><span data-stu-id="dcfe2-147">Set hello `connectionString` variable toohello connection string that you obtained when creating hello namespace, and set `topicName` toohello name that you used when creating hello topic.</span></span>
   
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
   
    <span data-ttu-id="dcfe2-148">O ficheiro Program.cs deve ter o seguinte aspeto.</span><span class="sxs-lookup"><span data-stu-id="dcfe2-148">Here is what your Program.cs file should look like.</span></span>
   
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
3. <span data-ttu-id="dcfe2-149">Execute o programa Olá e consulte Olá portal do Azure: clique no nome de Olá o tópico no espaço de nomes de Olá **descrição geral** painel.</span><span class="sxs-lookup"><span data-stu-id="dcfe2-149">Run hello program, and check hello Azure portal: click hello name of your topic in hello namespace **Overview** blade.</span></span> <span data-ttu-id="dcfe2-150">tópico de Olá **Essentials** é apresentado o painel.</span><span class="sxs-lookup"><span data-stu-id="dcfe2-150">hello topic **Essentials** blade is displayed.</span></span> <span data-ttu-id="dcfe2-151">Em subscrições de Olá listadas quase Olá parte inferior do painel de Olá, tenha em atenção que Olá **contagem de mensagens** valor para cada subscrição deve ser 1.</span><span class="sxs-lookup"><span data-stu-id="dcfe2-151">In hello subscription(s) listed near hello bottom of hello blade, notice that hello **Message Count** value for each subscription should now be 1.</span></span> <span data-ttu-id="dcfe2-152">Cada vez que executar a aplicação de remetente Olá sem obter mensagens hello (conforme descrito na secção seguinte Olá), este valor aumenta por 1.</span><span class="sxs-lookup"><span data-stu-id="dcfe2-152">Each time you run hello sender application without retrieving hello messages (as described in hello next section), this value increases by 1.</span></span> <span data-ttu-id="dcfe2-153">Tenha também em atenção que tamanho atual de Olá de Olá de incrementos do tópico Olá **atual** valor no Olá **Essentials** painel sempre que a aplicação Olá adiciona uma mensagem toohello tópico/subscrição.</span><span class="sxs-lookup"><span data-stu-id="dcfe2-153">Also note that hello current size of hello topic increments hello **Current** value on hello **Essentials** blade each time hello app adds a message toohello topic/subscription.</span></span>
   
      ![Tamanho da mensagem][topic-message]

## <a name="5-receive-messages-from-hello-subscription"></a><span data-ttu-id="dcfe2-155">5. Receber mensagens de subscrição de Olá</span><span class="sxs-lookup"><span data-stu-id="dcfe2-155">5. Receive messages from hello subscription</span></span>

1. <span data-ttu-id="dcfe2-156">mensagem de saudação tooreceive ou mensagens que acabámos de enviar, crie uma nova aplicação de consola e adicione um pacote NuGet do Service Bus do referência toohello, semelhante aplicação remetente anterior toohello.</span><span class="sxs-lookup"><span data-stu-id="dcfe2-156">tooreceive hello message or messages you just sent, create a new console application and add a reference toohello Service Bus NuGet package, similar toohello previous sender application.</span></span>
2. <span data-ttu-id="dcfe2-157">Adicione Olá seguinte `using` topo de toohello declaração do ficheiro Program.cs de Olá.</span><span class="sxs-lookup"><span data-stu-id="dcfe2-157">Add hello following `using` statement toohello top of hello Program.cs file.</span></span>
   
    ```csharp
    using Microsoft.ServiceBus.Messaging;
    ```
3. <span data-ttu-id="dcfe2-158">Adicionar Olá seguinte código toohello `Main` método.</span><span class="sxs-lookup"><span data-stu-id="dcfe2-158">Add hello following code toohello `Main` method.</span></span> <span data-ttu-id="dcfe2-159">Conjunto Olá `connectionString` obtida ao criar o espaço de nomes de Olá e definir da cadeia de ligação de variável toohello `topicName` toohello nome que utilizou durante a criação de tópico Olá.</span><span class="sxs-lookup"><span data-stu-id="dcfe2-159">Set hello `connectionString` variable toohello connection string you obtained when creating hello namespace, and set `topicName` toohello name that you used when creating hello topic.</span></span>
   
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
   
    <span data-ttu-id="dcfe2-160">O ficheiro Program.cs deve ter o seguinte aspeto:</span><span class="sxs-lookup"><span data-stu-id="dcfe2-160">Here is what your Program.cs file should look like:</span></span>
   
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
4. <span data-ttu-id="dcfe2-161">Executar Olá programa e consulte o portal de Olá novamente.</span><span class="sxs-lookup"><span data-stu-id="dcfe2-161">Run hello program, and check hello portal again.</span></span> <span data-ttu-id="dcfe2-162">Tenha em atenção que Olá **contagem de mensagens** e **atual** os valores são agora 0.</span><span class="sxs-lookup"><span data-stu-id="dcfe2-162">Notice that hello **Message Count** and **Current** values are now 0.</span></span>
   
    ![Comprimento do tópico][topic-message-receive]

<span data-ttu-id="dcfe2-164">Parabéns!</span><span class="sxs-lookup"><span data-stu-id="dcfe2-164">Congratulations!</span></span> <span data-ttu-id="dcfe2-165">Criou agora um tópico e uma subscrição, enviou uma mensagem e recebeu essa mensagem.</span><span class="sxs-lookup"><span data-stu-id="dcfe2-165">You have now created a topic and subscription, sent a message, and received that message.</span></span>

## <a name="next-steps"></a><span data-ttu-id="dcfe2-166">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="dcfe2-166">Next steps</span></span>

<span data-ttu-id="dcfe2-167">Consulte a nossa [repositório do GitHub com exemplos](https://github.com/Azure/azure-service-bus/tree/master/samples) que demonstra Algumas das Olá funcionalidades de mensagens do Service Bus mais avançadas.</span><span class="sxs-lookup"><span data-stu-id="dcfe2-167">Check out our [GitHub repository with samples](https://github.com/Azure/azure-service-bus/tree/master/samples) that demonstrate some of hello more advanced features of Service Bus messaging.</span></span>

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
