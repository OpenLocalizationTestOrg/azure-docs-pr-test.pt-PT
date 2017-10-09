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
# <a name="how-toouse-queue-storage-from-c"></a>Como toouse armazenamento de filas do C++
[!INCLUDE [storage-selector-queue-include](../../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a>Descrição geral
Este guia irá mostrar como tooperform cenários comuns utilizando Olá o serviço de armazenamento de filas do Azure. Exemplos de Olá são escritos em C++ e utilizar Olá [biblioteca de clientes do Storage do Azure para C++](http://github.com/Azure/azure-storage-cpp/blob/master/README.md). Olá os cenários abrangidos incluem **inserir**, **leitura**, **obter**, e **eliminar** fila de mensagens, bem como  **criar e eliminar filas**.

> [!NOTE]
> Destinos neste guia Olá biblioteca de clientes do Storage do Azure para C++ versão 1.0.0 e acima. Olá recomendada de versão é biblioteca de clientes de armazenamento 2.2.0, que está disponível através de [NuGet](http://www.nuget.org/packages/wastorage) ou [GitHub](http://github.com/Azure/azure-storage-cpp/).
> 
> 

[!INCLUDE [storage-queue-concepts-include](../../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="create-a-c-application"></a>Criar uma aplicação do C++
Neste guia, irá utilizar as funcionalidades de armazenamento que podem ser executadas dentro de uma aplicação de C++.

toodo por isso, terá de tooinstall hello biblioteca de clientes do Storage do Azure para C++ e criar uma conta de armazenamento do Azure na sua subscrição do Azure.

Olá tooinstall biblioteca de clientes do Storage do Azure para C++, pode utilizar Olá seguintes métodos:

* **Linux:** siga as instruções de Olá indicadas na Olá [biblioteca de clientes do Storage do Azure para o ficheiro Leia-me do C++](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) página.
* **Windows:** no Visual Studio, clique em **ferramentas > Gestor de pacotes NuGet > consola do Gestor de pacotes**. Seguinte Olá de tipo de comando para Olá [consola do Gestor de pacotes NuGet](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) e prima **ENTER**.

```  
Install-Package wastorage
```

## <a name="configure-your-application-tooaccess-queue-storage"></a>Configurar o seu tooaccess aplicações o armazenamento de filas
Adicione a seguinte Olá incluem parte superior do toohello de declarações do ficheiro de C++ de olá onde pretende toouse Olá Azure APIs tooaccess as filas de armazenamento:  

```cpp
#include <was/storage_account.h>
#include <was/queue.h>
```

## <a name="set-up-an-azure-storage-connection-string"></a>Configurar uma cadeia de ligação de armazenamento do Azure
Um cliente de armazenamento do Azure utiliza um armazenamento cadeia toostore pontos finais da ligação e as credenciais para aceder aos serviços de gestão de dados. Quando em execução numa aplicação de cliente, tem de fornecer cadeia de ligação de armazenamento de Olá Olá seguir o formato, utilizando o nome de Olá do seu armazenamento conta e Olá armazenamento chave de acesso da conta de armazenamento de Olá listada no Olá [Portal do Azure](https://portal.azure.com)para Olá *AccountName* e *AccountKey* valores. Para obter informações sobre as contas do storage e chaves de acesso, consulte [sobre contas de armazenamento do Azure](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json). Este exemplo mostra como podem declarar uma cadeia de ligação do campo estático toohold Olá:  

```cpp
// Define hello connection-string with your values.
const utility::string_t storage_connection_string(U("DefaultEndpointsProtocol=https;AccountName=your_storage_account;AccountKey=your_storage_account_key"));
```

tootest a aplicação no seu computador local do Windows, pode utilizar Olá Microsoft Azure [emulador do storage](../common/storage-use-emulator.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json) que é instalado com Olá [Azure SDK](https://azure.microsoft.com/downloads/). emulador do storage Olá é um utilitário que simula Olá tabela, fila e Blob serviços disponíveis no Azure no seu computador de desenvolvimento local. Olá exemplo seguinte mostra como podem declarar um campo estático toohold Olá ligação cadeia tooyour local emulador do storage:  

```cpp
// Define hello connection-string with Azure Storage Emulator.
const utility::string_t storage_connection_string(U("UseDevelopmentStorage=true;"));  
```

emulador do storage do Azure de toostart Olá, selecione Olá **iniciar** Olá botão ou prima **Windows** chave. Começa a escrever **emulador do Storage do Azure**e selecione **emulador do Storage do Microsoft Azure** da lista de Olá das aplicações.

Olá exemplos seguintes partem do princípio que utiliza um destes dois métodos tooget Olá armazenamento da cadeia de ligação.

## <a name="retrieve-your-connection-string"></a>Obter a cadeia de ligação
Pode utilizar Olá **cloud_storage_account** classe toorepresent informações da sua conta de armazenamento. tooretrieve informações da cadeia de ligação de armazenamento Olá de conta de armazenamento, pode utilizar Olá **analisar** método.

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);
```

## <a name="how-to-create-a-queue"></a>Como: criar uma fila
A **cloud_queue_client** objeto permite-lhe obter objetos de referência para as filas. Olá código seguinte cria um **cloud_queue_client** objeto.

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create a queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();
```

Olá utilize **cloud_queue_client** tooget uma fila de toohello referência pretende toouse de objeto. Pode criar fila Olá se não existir.

```cpp
// Retrieve a reference tooa queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Create hello queue if it doesn't already exist.
 queue.create_if_not_exists();  
```

## <a name="how-to-insert-a-message-into-a-queue"></a>Como: introduzir uma mensagem para uma fila
tooinsert uma mensagem numa fila existente, primeiro crie um novo **cloud_queue_message**. Em seguida, chame Olá **add_message** método. A **cloud_queue_message** pode ser criada a partir de qualquer uma cadeia ou um **byte** matriz. Eis o código que cria uma fila (se não existir) e a mensagem de saudação inserções "Olá, mundo":

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

## <a name="how-to-peek-at-hello-next-message"></a>Como: pré-visualizar a mensagem seguinte Olá
Pode pré-visualizar a mensagem de saudação no início de Olá de um fila sem a remover da fila de Olá ao chamar Olá **peek_message** método.

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

## <a name="how-to-change-hello-contents-of-a-queued-message"></a>Como: alterar Olá conteúdo de uma mensagem em fila
Pode alterar o conteúdo de Olá de uma mensagem no local na fila de Olá. Se a mensagem de saudação representa uma tarefa de trabalho, pode utilizar este estado da funcionalidade tooupdate Olá da tarefa de trabalho de Olá. Olá seguinte código atualiza a mensagem da fila de saudação com novos conteúdos e conjuntos Olá tooextend de tempo limite de visibilidade 60 segundos. Isto guarda Olá estado do trabalho associado à mensagem de saudação e atribui o cliente de Olá toocontinue minuto outra mensagem de saudação a trabalhar. Pode utilizar esta técnica tootrack com vários passos os fluxos de trabalho na fila de mensagens, sem ter toostart através de Olá início se falhar um passo de processamento devido a falha de toohardware ou software. Normalmente, também manteria uma contagem de tentativas e se a mensagem de saudação for repetida mais do que n vezes, deveria eliminá-la. Esta ação protege contra uma mensagem que aciona um erro da aplicação sempre que é processada.

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

## <a name="how-to-de-queue-hello-next-message"></a>Como: anular fila a mensagem seguinte Olá
O código remove uma mensagem da fila em dois passos. Quando chamar **get_message**, obterá a mensagem seguinte Olá numa fila. Uma mensagem devolvida por **get_message** torna-se invisível tooany outro código de leitura de mensagens desta fila. toofinish remover mensagem de saudação da fila de Olá, também tem de chamar **delete_message**. Este processo de dois passos da remoção de uma mensagem garante que se o código de falha tooprocess que pode obter uma mensagem devido a falha de toohardware ou de software, outra instância do seu código Olá a mesma mensagem e tente novamente. As chamadas de código **delete_message** imediatamente após a mensagem de saudação foi processada.

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

## <a name="how-to-leverage-additional-options-for-de-queuing-messages"></a>Como: tirar partido das opções adicionais para anular a colocação de mensagens
Existem duas formas através das quais pode personalizar a obtenção de mensagens a partir de uma fila. Em primeiro lugar, pode obter um lote de mensagens em fila (cópia de segurança too32). Segundo, pode definir um tempo limite de invisibilidade superiores ou inferiores, permitindo que o código mais ou menos tempo toofully processar cada mensagem. Olá exemplo de código seguinte utiliza Olá **get_messages** mensagens de tooget 20 método numa chamada. Em seguida, processa cada mensagem utilizando um **para** ciclo. Também define minutos toofive de tempo limite de invisibilidade do Olá para cada mensagem. Tenha em atenção que Olá 5 minutos inicia para todas as mensagens com Olá mesmo tempo, pelo que, depois de 5 minutos passaram desde a chamada de Olá demasiado**get_messages**, as mensagens que não tenham sido eliminadas ficarão visíveis novamente.

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

## <a name="how-to-get-hello-queue-length"></a>Como: obter o comprimento da fila Olá
Pode obter uma estimativa do número de Olá de mensagens numa fila. Olá **download_attributes** método pede-lhe Olá fila serviço tooretrieve atributos de fila de Olá, incluindo a contagem de mensagens hello. Olá **approximate_message_count** método obtém Olá aproximado número de mensagens em fila Olá.

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

## <a name="how-to-delete-a-queue"></a>Como: eliminar uma fila
toodelete uma fila e todas as mensagens de Olá nela contidas, chamada Olá **delete_queue_if_exists** método no objeto de fila de Olá.

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

## <a name="next-steps"></a>Passos seguintes
Agora que aprendeu as noções básicas de Olá do armazenamento de filas, siga estas toolearn ligações mais sobre o Storage do Azure.

* [Como toouse Blob Storage do C++](../blobs/storage-c-plus-plus-how-to-use-blobs.md)
* [Como toouse Table Storage do C++](../../cosmos-db/table-storage-how-to-use-c-plus.md)
* [Recursos de armazenamento do Azure de lista em C++](../common/storage-c-plus-plus-enumeration.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json)
* [Biblioteca de clientes do Storage para referência do C++](http://azure.github.io/azure-storage-cpp)
* [Documentação do Armazenamento do Azure](https://azure.microsoft.com/documentation/services/storage/)