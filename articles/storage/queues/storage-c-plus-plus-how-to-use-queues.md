---
title: armazenamento de filas aaaHow toouse (C++) | Microsoft Docs
description: "Saiba como toouse Olá o serviço de fila de armazenamento no Azure. Exemplos são escritos em C++."
services: storage
documentationcenter: .net
author: cbrooksmsft
manager: jahogg
editor: tysonn
ms.assetid: c8a36365-29f6-404d-8fd1-858a7f33b50a
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: cpp
ms.topic: article
ms.date: 05/11/2017
ms.author: cbrooksmsft
ms.openlocfilehash: b0cddf017878e9fab87f47d24b2906e40c9f4ad5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-queue-storage-from-c"></a><span data-ttu-id="36fc7-104">Como toouse armazenamento de filas do C++</span><span class="sxs-lookup"><span data-stu-id="36fc7-104">How toouse Queue Storage from C++</span></span>
[!INCLUDE [storage-selector-queue-include](../../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a><span data-ttu-id="36fc7-105">Descrição geral</span><span class="sxs-lookup"><span data-stu-id="36fc7-105">Overview</span></span>
<span data-ttu-id="36fc7-106">Este guia irá mostrar como tooperform cenários comuns utilizando Olá o serviço de armazenamento de filas do Azure.</span><span class="sxs-lookup"><span data-stu-id="36fc7-106">This guide will show you how tooperform common scenarios using hello Azure Queue storage service.</span></span> <span data-ttu-id="36fc7-107">Exemplos de Olá são escritos em C++ e utilizar Olá [biblioteca de clientes do Storage do Azure para C++](http://github.com/Azure/azure-storage-cpp/blob/master/README.md).</span><span class="sxs-lookup"><span data-stu-id="36fc7-107">hello samples are written in C++ and use hello [Azure Storage Client Library for C++](http://github.com/Azure/azure-storage-cpp/blob/master/README.md).</span></span> <span data-ttu-id="36fc7-108">Olá os cenários abrangidos incluem **inserir**, **leitura**, **obter**, e **eliminar** fila de mensagens, bem como  **criar e eliminar filas**.</span><span class="sxs-lookup"><span data-stu-id="36fc7-108">hello scenarios covered include **inserting**, **peeking**, **getting**, and **deleting** queue messages, as well as **creating and deleting queues**.</span></span>

> [!NOTE]
> <span data-ttu-id="36fc7-109">Destinos neste guia Olá biblioteca de clientes do Storage do Azure para C++ versão 1.0.0 e acima.</span><span class="sxs-lookup"><span data-stu-id="36fc7-109">This guide targets hello Azure Storage Client Library for C++ version 1.0.0 and above.</span></span> <span data-ttu-id="36fc7-110">Olá recomendada de versão é biblioteca de clientes de armazenamento 2.2.0, que está disponível através de [NuGet](http://www.nuget.org/packages/wastorage) ou [GitHub](http://github.com/Azure/azure-storage-cpp/).</span><span class="sxs-lookup"><span data-stu-id="36fc7-110">hello recommended version is Storage Client Library 2.2.0, which is available via [NuGet](http://www.nuget.org/packages/wastorage) or [GitHub](http://github.com/Azure/azure-storage-cpp/).</span></span>
> 
> 

[!INCLUDE [storage-queue-concepts-include](../../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="create-a-c-application"></a><span data-ttu-id="36fc7-111">Criar uma aplicação do C++</span><span class="sxs-lookup"><span data-stu-id="36fc7-111">Create a C++ application</span></span>
<span data-ttu-id="36fc7-112">Neste guia, irá utilizar as funcionalidades de armazenamento que podem ser executadas dentro de uma aplicação de C++.</span><span class="sxs-lookup"><span data-stu-id="36fc7-112">In this guide, you will use storage features which can be run within a C++ application.</span></span>

<span data-ttu-id="36fc7-113">toodo por isso, terá de tooinstall hello biblioteca de clientes do Storage do Azure para C++ e criar uma conta de armazenamento do Azure na sua subscrição do Azure.</span><span class="sxs-lookup"><span data-stu-id="36fc7-113">toodo so, you will need tooinstall hello Azure Storage Client Library for C++ and create an Azure storage account in your Azure subscription.</span></span>

<span data-ttu-id="36fc7-114">Olá tooinstall biblioteca de clientes do Storage do Azure para C++, pode utilizar Olá seguintes métodos:</span><span class="sxs-lookup"><span data-stu-id="36fc7-114">tooinstall hello Azure Storage Client Library for C++, you can use hello following methods:</span></span>

* <span data-ttu-id="36fc7-115">**Linux:** siga as instruções de Olá indicadas na Olá [biblioteca de clientes do Storage do Azure para o ficheiro Leia-me do C++](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) página.</span><span class="sxs-lookup"><span data-stu-id="36fc7-115">**Linux:** Follow hello instructions given in hello [Azure Storage Client Library for C++ README](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) page.</span></span>
* <span data-ttu-id="36fc7-116">**Windows:** no Visual Studio, clique em **ferramentas > Gestor de pacotes NuGet > consola do Gestor de pacotes**.</span><span class="sxs-lookup"><span data-stu-id="36fc7-116">**Windows:** In Visual Studio, click **Tools > NuGet Package Manager > Package Manager Console**.</span></span> <span data-ttu-id="36fc7-117">Seguinte Olá de tipo de comando para Olá [consola do Gestor de pacotes NuGet](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) e prima **ENTER**.</span><span class="sxs-lookup"><span data-stu-id="36fc7-117">Type hello following command into hello [NuGet Package Manager console](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) and press **ENTER**.</span></span>

```  
Install-Package wastorage
```

## <a name="configure-your-application-tooaccess-queue-storage"></a><span data-ttu-id="36fc7-118">Configurar o seu tooaccess aplicações o armazenamento de filas</span><span class="sxs-lookup"><span data-stu-id="36fc7-118">Configure your application tooaccess Queue Storage</span></span>
<span data-ttu-id="36fc7-119">Adicione a seguinte Olá incluem parte superior do toohello de declarações do ficheiro de C++ de olá onde pretende toouse Olá Azure APIs tooaccess as filas de armazenamento:</span><span class="sxs-lookup"><span data-stu-id="36fc7-119">Add hello following include statements toohello top of hello C++ file where you want toouse hello Azure storage APIs tooaccess queues:</span></span>  

```cpp
#include <was/storage_account.h>
#include <was/queue.h>
```

## <a name="set-up-an-azure-storage-connection-string"></a><span data-ttu-id="36fc7-120">Configurar uma cadeia de ligação de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="36fc7-120">Set up an Azure storage connection string</span></span>
<span data-ttu-id="36fc7-121">Um cliente de armazenamento do Azure utiliza um armazenamento cadeia toostore pontos finais da ligação e as credenciais para aceder aos serviços de gestão de dados.</span><span class="sxs-lookup"><span data-stu-id="36fc7-121">An Azure storage client uses a storage connection string toostore endpoints and credentials for accessing data management services.</span></span> <span data-ttu-id="36fc7-122">Quando em execução numa aplicação de cliente, tem de fornecer cadeia de ligação de armazenamento de Olá Olá seguir o formato, utilizando o nome de Olá do seu armazenamento conta e Olá armazenamento chave de acesso da conta de armazenamento de Olá listada no Olá [Portal do Azure](https://portal.azure.com)para Olá *AccountName* e *AccountKey* valores.</span><span class="sxs-lookup"><span data-stu-id="36fc7-122">When running in a client application, you must provide hello storage connection string in hello following format, using hello name of your storage account and hello storage access key for hello storage account listed in hello [Azure Portal](https://portal.azure.com) for hello *AccountName* and *AccountKey* values.</span></span> <span data-ttu-id="36fc7-123">Para obter informações sobre as contas do storage e chaves de acesso, consulte [sobre contas de armazenamento do Azure](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="36fc7-123">For information on storage accounts and access keys, see [About Azure Storage Accounts](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json).</span></span> <span data-ttu-id="36fc7-124">Este exemplo mostra como podem declarar uma cadeia de ligação do campo estático toohold Olá:</span><span class="sxs-lookup"><span data-stu-id="36fc7-124">This example shows how you can declare a static field toohold hello connection string:</span></span>  

```cpp
// Define hello connection-string with your values.
const utility::string_t storage_connection_string(U("DefaultEndpointsProtocol=https;AccountName=your_storage_account;AccountKey=your_storage_account_key"));
```

<span data-ttu-id="36fc7-125">tootest a aplicação no seu computador local do Windows, pode utilizar Olá Microsoft Azure [emulador do storage](../common/storage-use-emulator.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json) que é instalado com Olá [Azure SDK](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="36fc7-125">tootest your application in your local Windows computer, you can use hello Microsoft Azure [storage emulator](../common/storage-use-emulator.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json) that is installed with hello [Azure SDK](https://azure.microsoft.com/downloads/).</span></span> <span data-ttu-id="36fc7-126">emulador do storage Olá é um utilitário que simula Olá tabela, fila e Blob serviços disponíveis no Azure no seu computador de desenvolvimento local.</span><span class="sxs-lookup"><span data-stu-id="36fc7-126">hello storage emulator is a utility that simulates hello Blob, Queue, and Table services available in Azure on your local development machine.</span></span> <span data-ttu-id="36fc7-127">Olá exemplo seguinte mostra como podem declarar um campo estático toohold Olá ligação cadeia tooyour local emulador do storage:</span><span class="sxs-lookup"><span data-stu-id="36fc7-127">hello following example shows how you can declare a static field toohold hello connection string tooyour local storage emulator:</span></span>  

```cpp
// Define hello connection-string with Azure Storage Emulator.
const utility::string_t storage_connection_string(U("UseDevelopmentStorage=true;"));  
```

<span data-ttu-id="36fc7-128">emulador do storage do Azure de toostart Olá, selecione Olá **iniciar** Olá botão ou prima **Windows** chave.</span><span class="sxs-lookup"><span data-stu-id="36fc7-128">toostart hello Azure storage emulator, select hello **Start** button or press hello **Windows** key.</span></span> <span data-ttu-id="36fc7-129">Começa a escrever **emulador do Storage do Azure**e selecione **emulador do Storage do Microsoft Azure** da lista de Olá das aplicações.</span><span class="sxs-lookup"><span data-stu-id="36fc7-129">Begin typing **Azure Storage Emulator**, and select **Microsoft Azure Storage Emulator** from hello list of applications.</span></span>

<span data-ttu-id="36fc7-130">Olá exemplos seguintes partem do princípio que utiliza um destes dois métodos tooget Olá armazenamento da cadeia de ligação.</span><span class="sxs-lookup"><span data-stu-id="36fc7-130">hello following samples assume that you have used one of these two methods tooget hello storage connection string.</span></span>

## <a name="retrieve-your-connection-string"></a><span data-ttu-id="36fc7-131">Obter a cadeia de ligação</span><span class="sxs-lookup"><span data-stu-id="36fc7-131">Retrieve your connection string</span></span>
<span data-ttu-id="36fc7-132">Pode utilizar Olá **cloud_storage_account** classe toorepresent informações da sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="36fc7-132">You can use hello **cloud_storage_account** class toorepresent your Storage Account information.</span></span> <span data-ttu-id="36fc7-133">tooretrieve informações da cadeia de ligação de armazenamento Olá de conta de armazenamento, pode utilizar Olá **analisar** método.</span><span class="sxs-lookup"><span data-stu-id="36fc7-133">tooretrieve your storage account information from hello storage connection string, you can use hello **parse** method.</span></span>

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);
```

## <a name="how-to-create-a-queue"></a><span data-ttu-id="36fc7-134">Como: criar uma fila</span><span class="sxs-lookup"><span data-stu-id="36fc7-134">How to: Create a queue</span></span>
<span data-ttu-id="36fc7-135">A **cloud_queue_client** objeto permite-lhe obter objetos de referência para as filas.</span><span class="sxs-lookup"><span data-stu-id="36fc7-135">A **cloud_queue_client** object lets you get reference objects for queues.</span></span> <span data-ttu-id="36fc7-136">Olá código seguinte cria um **cloud_queue_client** objeto.</span><span class="sxs-lookup"><span data-stu-id="36fc7-136">hello following code creates a **cloud_queue_client** object.</span></span>

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create a queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();
```

<span data-ttu-id="36fc7-137">Olá utilize **cloud_queue_client** tooget uma fila de toohello referência pretende toouse de objeto.</span><span class="sxs-lookup"><span data-stu-id="36fc7-137">Use hello **cloud_queue_client** object tooget a reference toohello queue you want toouse.</span></span> <span data-ttu-id="36fc7-138">Pode criar fila Olá se não existir.</span><span class="sxs-lookup"><span data-stu-id="36fc7-138">You can create hello queue if it doesn't exist.</span></span>

```cpp
// Retrieve a reference tooa queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Create hello queue if it doesn't already exist.
 queue.create_if_not_exists();  
```

## <a name="how-to-insert-a-message-into-a-queue"></a><span data-ttu-id="36fc7-139">Como: introduzir uma mensagem para uma fila</span><span class="sxs-lookup"><span data-stu-id="36fc7-139">How to: Insert a message into a queue</span></span>
<span data-ttu-id="36fc7-140">tooinsert uma mensagem numa fila existente, primeiro crie um novo **cloud_queue_message**.</span><span class="sxs-lookup"><span data-stu-id="36fc7-140">tooinsert a message into an existing queue, first create a new **cloud_queue_message**.</span></span> <span data-ttu-id="36fc7-141">Em seguida, chame Olá **add_message** método.</span><span class="sxs-lookup"><span data-stu-id="36fc7-141">Next, call hello **add_message** method.</span></span> <span data-ttu-id="36fc7-142">A **cloud_queue_message** pode ser criada a partir de qualquer uma cadeia ou um **byte** matriz.</span><span class="sxs-lookup"><span data-stu-id="36fc7-142">A **cloud_queue_message** can be created from either a string or a **byte** array.</span></span> <span data-ttu-id="36fc7-143">Eis o código que cria uma fila (se não existir) e a mensagem de saudação inserções "Olá, mundo":</span><span class="sxs-lookup"><span data-stu-id="36fc7-143">Here is code which creates a queue (if it doesn't exist) and inserts hello message 'Hello, World':</span></span>

```cpp
// Retrieve storage account from connection-string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();

// Retrieve a reference tooa queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Create hello queue if it doesn't already exist.
queue.create_if_not_exists();

// Create a message and add it toohello queue.
azure::storage::cloud_queue_message message1(U("Hello, World"));
queue.add_message(message1);  
```

## <a name="how-to-peek-at-hello-next-message"></a><span data-ttu-id="36fc7-144">Como: pré-visualizar a mensagem seguinte Olá</span><span class="sxs-lookup"><span data-stu-id="36fc7-144">How to: Peek at hello next message</span></span>
<span data-ttu-id="36fc7-145">Pode pré-visualizar a mensagem de saudação no início de Olá de um fila sem a remover da fila de Olá ao chamar Olá **peek_message** método.</span><span class="sxs-lookup"><span data-stu-id="36fc7-145">You can peek at hello message in hello front of a queue without removing it from hello queue by calling hello **peek_message** method.</span></span>

```cpp
// Retrieve storage account from connection-string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();

// Retrieve a reference tooa queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Peek at hello next message.
azure::storage::cloud_queue_message peeked_message = queue.peek_message();

// Output hello message content.
std::wcout << U("Peeked message content: ") << peeked_message.content_as_string() << std::endl;
```

## <a name="how-to-change-hello-contents-of-a-queued-message"></a><span data-ttu-id="36fc7-146">Como: alterar Olá conteúdo de uma mensagem em fila</span><span class="sxs-lookup"><span data-stu-id="36fc7-146">How to: Change hello contents of a queued message</span></span>
<span data-ttu-id="36fc7-147">Pode alterar o conteúdo de Olá de uma mensagem no local na fila de Olá.</span><span class="sxs-lookup"><span data-stu-id="36fc7-147">You can change hello contents of a message in-place in hello queue.</span></span> <span data-ttu-id="36fc7-148">Se a mensagem de saudação representa uma tarefa de trabalho, pode utilizar este estado da funcionalidade tooupdate Olá da tarefa de trabalho de Olá.</span><span class="sxs-lookup"><span data-stu-id="36fc7-148">If hello message represents a work task, you could use this feature tooupdate hello status of hello work task.</span></span> <span data-ttu-id="36fc7-149">Olá seguinte código atualiza a mensagem da fila de saudação com novos conteúdos e conjuntos Olá tooextend de tempo limite de visibilidade 60 segundos.</span><span class="sxs-lookup"><span data-stu-id="36fc7-149">hello following code updates hello queue message with new contents, and sets hello visibility timeout tooextend another 60 seconds.</span></span> <span data-ttu-id="36fc7-150">Isto guarda Olá estado do trabalho associado à mensagem de saudação e atribui o cliente de Olá toocontinue minuto outra mensagem de saudação a trabalhar.</span><span class="sxs-lookup"><span data-stu-id="36fc7-150">This saves hello state of work associated with hello message, and gives hello client another minute toocontinue working on hello message.</span></span> <span data-ttu-id="36fc7-151">Pode utilizar esta técnica tootrack com vários passos os fluxos de trabalho na fila de mensagens, sem ter toostart através de Olá início se falhar um passo de processamento devido a falha de toohardware ou software.</span><span class="sxs-lookup"><span data-stu-id="36fc7-151">You could use this technique tootrack multi-step workflows on queue messages, without having toostart over from hello beginning if a processing step fails due toohardware or software failure.</span></span> <span data-ttu-id="36fc7-152">Normalmente, também manteria uma contagem de tentativas e se a mensagem de saudação for repetida mais do que n vezes, deveria eliminá-la.</span><span class="sxs-lookup"><span data-stu-id="36fc7-152">Typically, you would keep a retry count as well, and if hello message is retried more than n times, you would delete it.</span></span> <span data-ttu-id="36fc7-153">Esta ação protege contra uma mensagem que aciona um erro da aplicação sempre que é processada.</span><span class="sxs-lookup"><span data-stu-id="36fc7-153">This protects against a message that triggers an application error each time it is processed.</span></span>

```cpp
// Retrieve storage account from connection-string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_conection_string);

// Create hello queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();

// Retrieve a reference tooa queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Get hello message from hello queue and update hello message contents.
// hello visibility timeout "0" means make it visible immediately.
// hello visibility timeout "60" means hello client can get another minute toocontinue
// working on hello message.
azure::storage::cloud_queue_message changed_message = queue.get_message();

changed_message.set_content(U("Changed message"));
queue.update_message(changed_message, std::chrono::seconds(60), true);

// Output hello message content.
std::wcout << U("Changed message content: ") << changed_message.content_as_string() << std::endl;  
```

## <a name="how-to-de-queue-hello-next-message"></a><span data-ttu-id="36fc7-154">Como: anular fila a mensagem seguinte Olá</span><span class="sxs-lookup"><span data-stu-id="36fc7-154">How to: De-queue hello next message</span></span>
<span data-ttu-id="36fc7-155">O código remove uma mensagem da fila em dois passos.</span><span class="sxs-lookup"><span data-stu-id="36fc7-155">Your code de-queues a message from a queue in two steps.</span></span> <span data-ttu-id="36fc7-156">Quando chamar **get_message**, obterá a mensagem seguinte Olá numa fila.</span><span class="sxs-lookup"><span data-stu-id="36fc7-156">When you call **get_message**, you get hello next message in a queue.</span></span> <span data-ttu-id="36fc7-157">Uma mensagem devolvida por **get_message** torna-se invisível tooany outro código de leitura de mensagens desta fila.</span><span class="sxs-lookup"><span data-stu-id="36fc7-157">A message returned from **get_message** becomes invisible tooany other code reading messages from this queue.</span></span> <span data-ttu-id="36fc7-158">toofinish remover mensagem de saudação da fila de Olá, também tem de chamar **delete_message**.</span><span class="sxs-lookup"><span data-stu-id="36fc7-158">toofinish removing hello message from hello queue, you must also call **delete_message**.</span></span> <span data-ttu-id="36fc7-159">Este processo de dois passos da remoção de uma mensagem garante que se o código de falha tooprocess que pode obter uma mensagem devido a falha de toohardware ou de software, outra instância do seu código Olá a mesma mensagem e tente novamente.</span><span class="sxs-lookup"><span data-stu-id="36fc7-159">This two-step process of removing a message assures that if your code fails tooprocess a message due toohardware or software failure, another instance of your code can get hello same message and try again.</span></span> <span data-ttu-id="36fc7-160">As chamadas de código **delete_message** imediatamente após a mensagem de saudação foi processada.</span><span class="sxs-lookup"><span data-stu-id="36fc7-160">Your code calls **delete_message** right after hello message has been processed.</span></span>

```cpp
// Retrieve storage account from connection-string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();

// Retrieve a reference tooa queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Get hello next message.
azure::storage::cloud_queue_message dequeued_message = queue.get_message();
std::wcout << U("Dequeued message: ") << dequeued_message.content_as_string() << std::endl;

// Delete hello message.
queue.delete_message(dequeued_message);
```

## <a name="how-to-leverage-additional-options-for-de-queuing-messages"></a><span data-ttu-id="36fc7-161">Como: tirar partido das opções adicionais para anular a colocação de mensagens</span><span class="sxs-lookup"><span data-stu-id="36fc7-161">How to: Leverage additional options for de-queuing messages</span></span>
<span data-ttu-id="36fc7-162">Existem duas formas através das quais pode personalizar a obtenção de mensagens a partir de uma fila.</span><span class="sxs-lookup"><span data-stu-id="36fc7-162">There are two ways you can customize message retrieval from a queue.</span></span> <span data-ttu-id="36fc7-163">Em primeiro lugar, pode obter um lote de mensagens em fila (cópia de segurança too32).</span><span class="sxs-lookup"><span data-stu-id="36fc7-163">First, you can get a batch of messages (up too32).</span></span> <span data-ttu-id="36fc7-164">Segundo, pode definir um tempo limite de invisibilidade superiores ou inferiores, permitindo que o código mais ou menos tempo toofully processar cada mensagem.</span><span class="sxs-lookup"><span data-stu-id="36fc7-164">Second, you can set a longer or shorter invisibility timeout, allowing your code more or less time toofully process each message.</span></span> <span data-ttu-id="36fc7-165">Olá exemplo de código seguinte utiliza Olá **get_messages** mensagens de tooget 20 método numa chamada.</span><span class="sxs-lookup"><span data-stu-id="36fc7-165">hello following code example uses hello **get_messages** method tooget 20 messages in one call.</span></span> <span data-ttu-id="36fc7-166">Em seguida, processa cada mensagem utilizando um **para** ciclo.</span><span class="sxs-lookup"><span data-stu-id="36fc7-166">Then it processes each message using a **for** loop.</span></span> <span data-ttu-id="36fc7-167">Também define minutos toofive de tempo limite de invisibilidade do Olá para cada mensagem.</span><span class="sxs-lookup"><span data-stu-id="36fc7-167">It also sets hello invisibility timeout toofive minutes for each message.</span></span> <span data-ttu-id="36fc7-168">Tenha em atenção que Olá 5 minutos inicia para todas as mensagens com Olá mesmo tempo, pelo que, depois de 5 minutos passaram desde a chamada de Olá demasiado**get_messages**, as mensagens que não tenham sido eliminadas ficarão visíveis novamente.</span><span class="sxs-lookup"><span data-stu-id="36fc7-168">Note that hello 5 minutes starts for all messages at hello same time, so after 5 minutes have passed since hello call too**get_messages**, any messages which have not been deleted will become visible again.</span></span>

```cpp
// Retrieve storage account from connection-string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();

// Retrieve a reference tooa queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Dequeue some queue messages (maximum 32 at a time) and set their visibility timeout to
// 5 minutes (300 seconds).
azure::storage::queue_request_options options;
azure::storage::operation_context context;

// Retrieve 20 messages from hello queue with a visibility timeout of 300 seconds.
std::vector<azure::storage::cloud_queue_message> messages = queue.get_messages(20, std::chrono::seconds(300), options, context);

for (auto it = messages.cbegin(); it != messages.cend(); ++it)
{
    // Display hello contents of hello message.
    std::wcout << U("Get: ") << it->content_as_string() << std::endl;
}
```

## <a name="how-to-get-hello-queue-length"></a><span data-ttu-id="36fc7-169">Como: obter o comprimento da fila Olá</span><span class="sxs-lookup"><span data-stu-id="36fc7-169">How to: Get hello queue length</span></span>
<span data-ttu-id="36fc7-170">Pode obter uma estimativa do número de Olá de mensagens numa fila.</span><span class="sxs-lookup"><span data-stu-id="36fc7-170">You can get an estimate of hello number of messages in a queue.</span></span> <span data-ttu-id="36fc7-171">Olá **download_attributes** método pede-lhe Olá fila serviço tooretrieve atributos de fila de Olá, incluindo a contagem de mensagens hello.</span><span class="sxs-lookup"><span data-stu-id="36fc7-171">hello **download_attributes** method asks hello Queue service tooretrieve hello queue attributes, including hello message count.</span></span> <span data-ttu-id="36fc7-172">Olá **approximate_message_count** método obtém Olá aproximado número de mensagens em fila Olá.</span><span class="sxs-lookup"><span data-stu-id="36fc7-172">hello **approximate_message_count** method gets hello approximate number of messages in hello queue.</span></span>

```cpp
// Retrieve storage account from connection-string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();

// Retrieve a reference tooa queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Fetch hello queue attributes.
queue.download_attributes();

// Retrieve hello cached approximate message count.
int cachedMessageCount = queue.approximate_message_count();

// Display number of messages.
std::wcout << U("Number of messages in queue: ") << cachedMessageCount << std::endl;  
```

## <a name="how-to-delete-a-queue"></a><span data-ttu-id="36fc7-173">Como: eliminar uma fila</span><span class="sxs-lookup"><span data-stu-id="36fc7-173">How to: Delete a queue</span></span>
<span data-ttu-id="36fc7-174">toodelete uma fila e todas as mensagens de Olá nela contidas, chamada Olá **delete_queue_if_exists** método no objeto de fila de Olá.</span><span class="sxs-lookup"><span data-stu-id="36fc7-174">toodelete a queue and all hello messages contained in it, call hello **delete_queue_if_exists** method on hello queue object.</span></span>

```cpp
// Retrieve storage account from connection-string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();

// Retrieve a reference tooa queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// If hello queue exists and delete it.
queue.delete_queue_if_exists();  
```

## <a name="next-steps"></a><span data-ttu-id="36fc7-175">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="36fc7-175">Next steps</span></span>
<span data-ttu-id="36fc7-176">Agora que aprendeu as noções básicas de Olá do armazenamento de filas, siga estas toolearn ligações mais sobre o Storage do Azure.</span><span class="sxs-lookup"><span data-stu-id="36fc7-176">Now that you've learned hello basics of Queue storage, follow these links toolearn more about Azure Storage.</span></span>

* [<span data-ttu-id="36fc7-177">Como toouse Blob Storage do C++</span><span class="sxs-lookup"><span data-stu-id="36fc7-177">How toouse Blob Storage from C++</span></span>](../blobs/storage-c-plus-plus-how-to-use-blobs.md)
* [<span data-ttu-id="36fc7-178">Como toouse Table Storage do C++</span><span class="sxs-lookup"><span data-stu-id="36fc7-178">How toouse Table Storage from C++</span></span>](../../cosmos-db/table-storage-how-to-use-c-plus.md)
* [<span data-ttu-id="36fc7-179">Recursos de armazenamento do Azure de lista em C++</span><span class="sxs-lookup"><span data-stu-id="36fc7-179">List Azure Storage Resources in C++</span></span>](../common/storage-c-plus-plus-enumeration.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json)
* [<span data-ttu-id="36fc7-180">Biblioteca de clientes do Storage para referência do C++</span><span class="sxs-lookup"><span data-stu-id="36fc7-180">Storage Client Library for C++ Reference</span></span>](http://azure.github.io/azure-storage-cpp)
* [<span data-ttu-id="36fc7-181">Documentação do Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="36fc7-181">Azure Storage Documentation</span></span>](https://azure.microsoft.com/documentation/services/storage/)