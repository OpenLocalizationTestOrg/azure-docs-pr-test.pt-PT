---
title: aaaHow toouse armazenamento de filas do Ruby | Microsoft Docs
description: "Saiba como toouse Olá filas do Azure service toocreate e filas de eliminação e inserção, obterem e eliminar as mensagens. Amostras de escrita em Ruby."
services: storage
documentationcenter: ruby
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 59c2d81b-db9c-46ee-ade2-2f0caae6b1e6
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: ruby
ms.topic: article
ms.date: 12/08/2016
ms.author: robinsh
ms.openlocfilehash: c8eacac058442419cb9e8fe62cb69ad7ef1e2fc4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-queue-storage-from-ruby"></a><span data-ttu-id="9391a-104">Como toouse armazenamento de filas do Ruby</span><span class="sxs-lookup"><span data-stu-id="9391a-104">How toouse Queue storage from Ruby</span></span>
[!INCLUDE [storage-selector-queue-include](../../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a><span data-ttu-id="9391a-105">Descrição geral</span><span class="sxs-lookup"><span data-stu-id="9391a-105">Overview</span></span>
<span data-ttu-id="9391a-106">Este guia mostra como tooperform cenários comuns utilizando Olá o serviço de armazenamento de filas do Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="9391a-106">This guide shows you how tooperform common scenarios using hello Microsoft Azure Queue Storage service.</span></span> <span data-ttu-id="9391a-107">Exemplos de Olá são escritos utilizando Olá Ruby Azure API.</span><span class="sxs-lookup"><span data-stu-id="9391a-107">hello samples are written using hello Ruby Azure API.</span></span>
<span data-ttu-id="9391a-108">Olá os cenários abrangidos incluem **inserir**, **leitura**, **obter**, e **eliminar** fila de mensagens, bem como  **criar e eliminar filas**.</span><span class="sxs-lookup"><span data-stu-id="9391a-108">hello scenarios covered include **inserting**, **peeking**, **getting**, and **deleting** queue messages, as well as **creating and deleting queues**.</span></span>

[!INCLUDE [storage-queue-concepts-include](../../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="create-a-ruby-application"></a><span data-ttu-id="9391a-109">Criar uma aplicação Ruby</span><span class="sxs-lookup"><span data-stu-id="9391a-109">Create a Ruby Application</span></span>
<span data-ttu-id="9391a-110">Crie uma aplicação Ruby.</span><span class="sxs-lookup"><span data-stu-id="9391a-110">Create a Ruby application.</span></span> <span data-ttu-id="9391a-111">Para obter instruções, consulte [Ruby na aplicação Rails Web numa VM do Azure](../../virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md).</span><span class="sxs-lookup"><span data-stu-id="9391a-111">For instructions, see [Ruby on Rails Web application on an Azure VM](../../virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md).</span></span>

## <a name="configure-your-application-tooaccess-storage"></a><span data-ttu-id="9391a-112">Configurar a sua aplicação tooAccess armazenamento</span><span class="sxs-lookup"><span data-stu-id="9391a-112">Configure Your Application tooAccess Storage</span></span>
<span data-ttu-id="9391a-113">toouse storage do Azure, terá de toodownload e utilize Olá Ruby pacote do azure, que inclui um conjunto de bibliotecas de conveniência que comunicam com os serviços de REST de armazenamento Olá.</span><span class="sxs-lookup"><span data-stu-id="9391a-113">toouse Azure storage, you need toodownload and use hello Ruby azure package, which includes a set of convenience libraries that communicate with hello storage REST services.</span></span>

### <a name="use-rubygems-tooobtain-hello-package"></a><span data-ttu-id="9391a-114">Utilize o pacote de Olá RubyGems tooobtain</span><span class="sxs-lookup"><span data-stu-id="9391a-114">Use RubyGems tooobtain hello package</span></span>
1. <span data-ttu-id="9391a-115">Utilize uma interface de linha de comandos, como **PowerShell** (Windows), **Terminal** (Mac), ou **Bash** (Unix).</span><span class="sxs-lookup"><span data-stu-id="9391a-115">Use a command-line interface such as **PowerShell** (Windows), **Terminal** (Mac), or **Bash** (Unix).</span></span>
2. <span data-ttu-id="9391a-116">Escreva "gem instalar azure" gem do Olá comando janela tooinstall Olá e as dependências.</span><span class="sxs-lookup"><span data-stu-id="9391a-116">Type "gem install azure" in hello command window tooinstall hello gem and dependencies.</span></span>

### <a name="import-hello-package"></a><span data-ttu-id="9391a-117">Importar o pacote de Olá</span><span class="sxs-lookup"><span data-stu-id="9391a-117">Import hello package</span></span>
<span data-ttu-id="9391a-118">Utilize o editor de texto favorito, adicione Olá toohello superior de Olá Ruby ficheiro onde pretende toouse armazenamento os seguintes:</span><span class="sxs-lookup"><span data-stu-id="9391a-118">Use your favorite text editor, add hello following toohello top of hello Ruby file where you intend toouse storage:</span></span>

```ruby
require "azure"
```

## <a name="setup-an-azure-storage-connection"></a><span data-ttu-id="9391a-119">Configurar uma ligação de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="9391a-119">Setup an Azure Storage Connection</span></span>
<span data-ttu-id="9391a-120">módulo Olá do azure será lida a variáveis de ambiente de Olá **AZURE\_armazenamento\_conta** e **AZURE\_armazenamento\_ACCESS_KEY** para as informações necessárias tooconnect tooyour conta de armazenamento Azure.</span><span class="sxs-lookup"><span data-stu-id="9391a-120">hello azure module will read hello environment variables **AZURE\_STORAGE\_ACCOUNT** and **AZURE\_STORAGE\_ACCESS_KEY** for information required tooconnect tooyour Azure storage account.</span></span> <span data-ttu-id="9391a-121">Se estas variáveis de ambiente não estiver definidas, tem de especificar as informações de conta de Olá antes de utilizar **Azure::QueueService** com Olá seguinte código:</span><span class="sxs-lookup"><span data-stu-id="9391a-121">If these environment variables are not set, you must specify hello account information before using **Azure::QueueService** with hello following code:</span></span>

```ruby
Azure.config.storage_account_name = "<your azure storage account>"
Azure.config.storage_access_key = "<your Azure storage access key>"
```

<span data-ttu-id="9391a-122">tooobtain estes valores de um clássico ou do armazenamento do Resource Manager conta no Olá portal do Azure:</span><span class="sxs-lookup"><span data-stu-id="9391a-122">tooobtain these values from a classic or Resource Manager storage account in hello Azure portal:</span></span>

1. <span data-ttu-id="9391a-123">Inicie sessão no toohello [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="9391a-123">Log in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="9391a-124">Navegue toohello conta de armazenamento que pretende toouse.</span><span class="sxs-lookup"><span data-stu-id="9391a-124">Navigate toohello storage account you want toouse.</span></span>
3. <span data-ttu-id="9391a-125">No painel de definições de Olá no Olá direito, clique em **chaves de acesso**.</span><span class="sxs-lookup"><span data-stu-id="9391a-125">In hello Settings blade on hello right, click **Access Keys**.</span></span>
4. <span data-ttu-id="9391a-126">Olá acesso painel chaves que aparece, verá a chave de acesso de Olá 1 e 2 a chave de acesso.</span><span class="sxs-lookup"><span data-stu-id="9391a-126">In hello Access keys blade that appears, you'll see hello access key 1 and access key 2.</span></span> <span data-ttu-id="9391a-127">Pode utilizar qualquer um destes.</span><span class="sxs-lookup"><span data-stu-id="9391a-127">You can use either of these.</span></span> 
5. <span data-ttu-id="9391a-128">Clique em Olá cópia ícone toocopy Olá toohello chave da área de transferência.</span><span class="sxs-lookup"><span data-stu-id="9391a-128">Click hello copy icon toocopy hello key toohello clipboard.</span></span> 

## <a name="how-to-create-a-queue"></a><span data-ttu-id="9391a-129">Como: Criar uma fila</span><span class="sxs-lookup"><span data-stu-id="9391a-129">How To: Create a Queue</span></span>
<span data-ttu-id="9391a-130">Olá código seguinte cria um **Azure::QueueService** objeto, que permite-lhe toowork com as filas.</span><span class="sxs-lookup"><span data-stu-id="9391a-130">hello following code creates a **Azure::QueueService** object, which enables you toowork with queues.</span></span>

```ruby
azure_queue_service = Azure::QueueService.new
```

<span data-ttu-id="9391a-131">Olá utilize **create_queue()** método toocreate uma fila com Olá especificado o nome.</span><span class="sxs-lookup"><span data-stu-id="9391a-131">Use hello **create_queue()** method toocreate a queue with hello specified name.</span></span>

```ruby
begin
  azure_queue_service.create_queue("test-queue")
rescue
  puts $!
end
```

## <a name="how-to-insert-a-message-into-a-queue"></a><span data-ttu-id="9391a-132">Como: Introduzir uma mensagem para uma fila</span><span class="sxs-lookup"><span data-stu-id="9391a-132">How To: Insert a Message into a Queue</span></span>
<span data-ttu-id="9391a-133">tooinsert uma mensagem para uma fila, utilize Olá **create_message()** método toocreate uma nova mensagem e adicioná-la toohello fila.</span><span class="sxs-lookup"><span data-stu-id="9391a-133">tooinsert a message into a queue, use hello **create_message()** method toocreate a new message and add it toohello queue.</span></span>

```ruby
azure_queue_service.create_message("test-queue", "test message")
```

## <a name="how-to-peek-at-hello-next-message"></a><span data-ttu-id="9391a-134">Como: Pré-visualizar Olá a mensagem seguinte</span><span class="sxs-lookup"><span data-stu-id="9391a-134">How To: Peek at hello Next Message</span></span>
<span data-ttu-id="9391a-135">Pode pré-visualizar a mensagem de saudação no início de Olá de um fila sem a remover da fila de Olá ao chamar Olá **peek\_messages()** método.</span><span class="sxs-lookup"><span data-stu-id="9391a-135">You can peek at hello message in hello front of a queue without removing it from hello queue by calling hello **peek\_messages()** method.</span></span> <span data-ttu-id="9391a-136">Por predefinição, **peek\_messages()** peeks uma única mensagem.</span><span class="sxs-lookup"><span data-stu-id="9391a-136">By default, **peek\_messages()** peeks at a single message.</span></span> <span data-ttu-id="9391a-137">Também pode especificar mensagens quantos quiser toopeek.</span><span class="sxs-lookup"><span data-stu-id="9391a-137">You can also specify how many messages you want toopeek.</span></span>

```ruby
result = azure_queue_service.peek_messages("test-queue",
  {:number_of_messages => 10})
```

## <a name="how-to-dequeue-hello-next-message"></a><span data-ttu-id="9391a-138">Como: Anular Olá a mensagem seguinte</span><span class="sxs-lookup"><span data-stu-id="9391a-138">How To: Dequeue hello Next Message</span></span>
<span data-ttu-id="9391a-139">Pode remover uma mensagem da fila em dois passos.</span><span class="sxs-lookup"><span data-stu-id="9391a-139">You can remove a message from a queue in two steps.</span></span>

1. <span data-ttu-id="9391a-140">Quando chamar **lista\_messages()**, obterá a mensagem seguinte Olá numa fila por predefinição.</span><span class="sxs-lookup"><span data-stu-id="9391a-140">When you call **list\_messages()**, you get hello next message in a queue by default.</span></span> <span data-ttu-id="9391a-141">Também pode especificar mensagens quantos quiser tooget.</span><span class="sxs-lookup"><span data-stu-id="9391a-141">You can also specify how many messages you want tooget.</span></span> <span data-ttu-id="9391a-142">Olá, as mensagens resultantes da **lista\_messages()** torna-se invisível tooany outro código de leitura de mensagens desta fila.</span><span class="sxs-lookup"><span data-stu-id="9391a-142">hello messages returned from **list\_messages()** becomes invisible tooany other code reading messages from this queue.</span></span> <span data-ttu-id="9391a-143">Passar no tempo limite de visibilidade de Olá em segundos, como um parâmetro.</span><span class="sxs-lookup"><span data-stu-id="9391a-143">You pass in hello visibility timeout in seconds as a parameter.</span></span>
2. <span data-ttu-id="9391a-144">toofinish remover mensagem de saudação da fila de Olá, também tem de chamar **delete_message()**.</span><span class="sxs-lookup"><span data-stu-id="9391a-144">toofinish removing hello message from hello queue, you must also call **delete_message()**.</span></span>

<span data-ttu-id="9391a-145">Este processo de dois passos da remoção de uma mensagem garante que, quando os tooprocess de falha de código pode obter uma mensagem devido a falha de toohardware ou de software, outra instância do seu código Olá mesma mensagem e tente novamente.</span><span class="sxs-lookup"><span data-stu-id="9391a-145">This two-step process of removing a message assures that when your code fails tooprocess a message due toohardware or software failure, another instance of your code can get hello same message and try again.</span></span> <span data-ttu-id="9391a-146">As chamadas de código **eliminar\_message()** imediatamente após a mensagem de saudação foi processada.</span><span class="sxs-lookup"><span data-stu-id="9391a-146">Your code calls **delete\_message()** right after hello message has been processed.</span></span>

```ruby
messages = azure_queue_service.list_messages("test-queue", 30)
azure_queue_service.delete_message("test-queue", 
  messages[0].id, messages[0].pop_receipt)
```

## <a name="how-to-change-hello-contents-of-a-queued-message"></a><span data-ttu-id="9391a-147">Como: Alterar Olá conteúdo de uma mensagem em fila</span><span class="sxs-lookup"><span data-stu-id="9391a-147">How To: Change hello Contents of a Queued Message</span></span>
<span data-ttu-id="9391a-148">Pode alterar o conteúdo de Olá de uma mensagem no local na fila de Olá.</span><span class="sxs-lookup"><span data-stu-id="9391a-148">You can change hello contents of a message in-place in hello queue.</span></span> <span data-ttu-id="9391a-149">código de Olá abaixo utiliza Olá **update_message()** método tooupdate uma mensagem.</span><span class="sxs-lookup"><span data-stu-id="9391a-149">hello code below uses hello **update_message()** method tooupdate a message.</span></span> <span data-ttu-id="9391a-150">método de Olá irá devolver uma cadeia de identificação que contém Olá pop a receção mensagem da fila de saudação e um valor de tempo de data UTC representa quando a mensagem de saudação vai estar visível na fila de Olá.</span><span class="sxs-lookup"><span data-stu-id="9391a-150">hello method will return a tuple which contains hello pop receipt of hello queue message and a UTC date time value that represents when hello message will be visible on hello queue.</span></span>

```ruby
message = azure_queue_service.list_messages("test-queue", 30)
pop_receipt, time_next_visible = azure_queue_service.update_message(
  "test-queue", message.id, message.pop_receipt, "updated test message", 
  30)
```

## <a name="how-to-additional-options-for-dequeuing-messages"></a><span data-ttu-id="9391a-151">Como: Mensagens de opções adicionais para Dequeuing</span><span class="sxs-lookup"><span data-stu-id="9391a-151">How To: Additional Options for Dequeuing Messages</span></span>
<span data-ttu-id="9391a-152">Existem duas formas através das quais pode personalizar a obtenção de mensagens a partir de uma fila.</span><span class="sxs-lookup"><span data-stu-id="9391a-152">There are two ways you can customize message retrieval from a queue.</span></span>

1. <span data-ttu-id="9391a-153">Pode obter um lote de mensagem.</span><span class="sxs-lookup"><span data-stu-id="9391a-153">You can get a batch of message.</span></span>
2. <span data-ttu-id="9391a-154">Pode definir um tempo limite de invisibilidade superiores ou inferiores, permitindo que o código mais ou menos tempo toofully processar cada mensagem.</span><span class="sxs-lookup"><span data-stu-id="9391a-154">You can set a longer or shorter invisibility timeout, allowing your code more or less time toofully process each message.</span></span>

<span data-ttu-id="9391a-155">Olá exemplo de código seguinte utiliza Olá **lista\_messages()** mensagens tooget 15 de método numa chamada.</span><span class="sxs-lookup"><span data-stu-id="9391a-155">hello following code example uses hello **list\_messages()** method tooget 15 messages in one call.</span></span> <span data-ttu-id="9391a-156">Em seguida, imprime e elimina a cada mensagem.</span><span class="sxs-lookup"><span data-stu-id="9391a-156">Then it prints and deletes each message.</span></span> <span data-ttu-id="9391a-157">Também define minutos toofive de tempo limite de invisibilidade do Olá para cada mensagem.</span><span class="sxs-lookup"><span data-stu-id="9391a-157">It also sets hello invisibility timeout toofive minutes for each message.</span></span>

```ruby
azure_queue_service.list_messages("test-queue", 300
  {:number_of_messages => 15}).each do |m|
  puts m.message_text
  azure_queue_service.delete_message("test-queue", m.id, m.pop_receipt)
end
```

## <a name="how-to-get-hello-queue-length"></a><span data-ttu-id="9391a-158">Como: Obter Olá comprimento da fila</span><span class="sxs-lookup"><span data-stu-id="9391a-158">How To: Get hello Queue Length</span></span>
<span data-ttu-id="9391a-159">Pode obter uma estimativa do número de Olá de mensagens em fila Olá.</span><span class="sxs-lookup"><span data-stu-id="9391a-159">You can get an estimation of hello number of messages in hello queue.</span></span> <span data-ttu-id="9391a-160">Olá **obter\_fila\_metadata()** método pede-lhe Olá fila serviço tooreturn Olá mensagem aproximado contagem e metadados sobre fila Olá.</span><span class="sxs-lookup"><span data-stu-id="9391a-160">hello **get\_queue\_metadata()** method asks hello queue service tooreturn hello approximate message count and metadata about hello queue.</span></span>

```ruby
message_count, metadata = azure_queue_service.get_queue_metadata(
  "test-queue")
```

## <a name="how-to-delete-a-queue"></a><span data-ttu-id="9391a-161">Como: Eliminar uma fila</span><span class="sxs-lookup"><span data-stu-id="9391a-161">How To: Delete a Queue</span></span>
<span data-ttu-id="9391a-162">toodelete uma fila e todas as mensagens de Olá nela contidas, chamada Olá **eliminar\_queue()** método no objeto de fila de Olá.</span><span class="sxs-lookup"><span data-stu-id="9391a-162">toodelete a queue and all hello messages contained in it, call hello **delete\_queue()** method on hello queue object.</span></span>

```ruby
azure_queue_service.delete_queue("test-queue")
```

## <a name="next-steps"></a><span data-ttu-id="9391a-163">Passos Seguintes</span><span class="sxs-lookup"><span data-stu-id="9391a-163">Next Steps</span></span>
<span data-ttu-id="9391a-164">Agora que aprendeu as noções básicas de Olá do armazenamento de filas, siga estas toolearn ligações sobre as tarefas de armazenamento mais complexas.</span><span class="sxs-lookup"><span data-stu-id="9391a-164">Now that you've learned hello basics of queue storage, follow these links toolearn about more complex storage tasks.</span></span>

* <span data-ttu-id="9391a-165">Visite Olá [blogue da equipa de armazenamento do Azure](http://blogs.msdn.com/b/windowsazurestorage/)</span><span class="sxs-lookup"><span data-stu-id="9391a-165">Visit hello [Azure Storage Team Blog](http://blogs.msdn.com/b/windowsazurestorage/)</span></span>
* <span data-ttu-id="9391a-166">Visite Olá [Azure SDK para Ruby](https://github.com/WindowsAzure/azure-sdk-for-ruby) repositório no GitHub</span><span class="sxs-lookup"><span data-stu-id="9391a-166">Visit hello [Azure SDK for Ruby](https://github.com/WindowsAzure/azure-sdk-for-ruby) repository on GitHub</span></span>

<span data-ttu-id="9391a-167">Para ver uma comparação entre Olá serviço de fila do Azure abordado neste artigo e filas de barramento de serviço de Azure abordado Olá [como toouse filas do Service Bus](/develop/ruby/how-to-guides/service-bus-queues/) artigo, consulte [filas do Azure e filas do Service Bus - comparados e Contrasted](../../service-bus-messaging/service-bus-azure-and-service-bus-queues-compared-contrasted.md)</span><span class="sxs-lookup"><span data-stu-id="9391a-167">For a comparison between hello Azure Queue Service discussed in this article and Azure Service Bus Queues discussed in hello [How toouse Service Bus Queues](/develop/ruby/how-to-guides/service-bus-queues/) article, see [Azure Queues and Service Bus Queues - Compared and Contrasted](../../service-bus-messaging/service-bus-azure-and-service-bus-queues-compared-contrasted.md)</span></span>
