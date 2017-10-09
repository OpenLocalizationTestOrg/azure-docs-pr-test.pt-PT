---
title: aaaHow toouse armazenamento de filas do Python | Microsoft Docs
description: "Saiba como toouse Olá serviço fila do Azure do Python toocreate e eliminar filas, inserir, obter e eliminar as mensagens."
services: storage
documentationcenter: python
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: cc0d2da2-379a-4b58-a234-8852b4e3d99d
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 12/08/2016
ms.author: robinsh
ms.openlocfilehash: ce8d999d9fafaef0dab48442560d004c034c0804
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-queue-storage-from-python"></a><span data-ttu-id="03d81-103">Como toouse armazenamento de filas do Python</span><span class="sxs-lookup"><span data-stu-id="03d81-103">How toouse Queue storage from Python</span></span>
[!INCLUDE [storage-selector-queue-include](../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a><span data-ttu-id="03d81-104">Descrição geral</span><span class="sxs-lookup"><span data-stu-id="03d81-104">Overview</span></span>
<span data-ttu-id="03d81-105">Este guia mostra como tooperform cenários comuns utilizando Olá o serviço de armazenamento de filas do Azure.</span><span class="sxs-lookup"><span data-stu-id="03d81-105">This guide shows you how tooperform common scenarios using hello Azure Queue storage service.</span></span> <span data-ttu-id="03d81-106">Exemplos de Olá são escritos no Python e utilizam Olá [SDK de armazenamento do Microsoft Azure para Python].</span><span class="sxs-lookup"><span data-stu-id="03d81-106">hello samples are written in Python and use hello [Microsoft Azure Storage SDK for Python].</span></span> <span data-ttu-id="03d81-107">Olá os cenários abrangidos incluem **inserir**, **leitura**, **obter**, e **eliminar** fila de mensagens, bem como  **criar e eliminar filas**.</span><span class="sxs-lookup"><span data-stu-id="03d81-107">hello scenarios covered include **inserting**, **peeking**, **getting**, and **deleting** queue messages, as well as **creating and deleting queues**.</span></span> <span data-ttu-id="03d81-108">Para obter mais informações sobre as filas, consulte a secção toohello [passos].</span><span class="sxs-lookup"><span data-stu-id="03d81-108">For more information on queues, refer toohello [Next Steps] section.</span></span>

[!INCLUDE [storage-queue-concepts-include](../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="how-to-create-a-queue"></a><span data-ttu-id="03d81-109">Como: Criar uma fila</span><span class="sxs-lookup"><span data-stu-id="03d81-109">How To: Create a Queue</span></span>
<span data-ttu-id="03d81-110">Olá **QueueService** objeto permite-lhe trabalhar com as filas.</span><span class="sxs-lookup"><span data-stu-id="03d81-110">hello **QueueService** object lets you work with queues.</span></span> <span data-ttu-id="03d81-111">Olá código seguinte cria um **QueueService** objeto.</span><span class="sxs-lookup"><span data-stu-id="03d81-111">hello following code creates a **QueueService** object.</span></span> <span data-ttu-id="03d81-112">Adicione o seguinte Olá perto do topo Olá de qualquer ficheiro de Python no qual pretende tooprogrammatically acesso Storage do Azure:</span><span class="sxs-lookup"><span data-stu-id="03d81-112">Add hello following near hello top of any Python file in which you wish tooprogrammatically access Azure Storage:</span></span>

```python
from azure.storage.queue import QueueService
```

<span data-ttu-id="03d81-113">Olá código seguinte cria um **QueueService** utilizando Olá chave conta do storage conta e o nome do objeto.</span><span class="sxs-lookup"><span data-stu-id="03d81-113">hello following code creates a **QueueService** object using hello storage account name and account key.</span></span> <span data-ttu-id="03d81-114">Substitua 'myaccount' e 'mykey' com o nome da conta e a chave.</span><span class="sxs-lookup"><span data-stu-id="03d81-114">Replace 'myaccount' and 'mykey' with your account name and key.</span></span>

```python
queue_service = QueueService(account_name='myaccount', account_key='mykey')

queue_service.create_queue('taskqueue')
```

## <a name="how-to-insert-a-message-into-a-queue"></a><span data-ttu-id="03d81-115">Como: Introduzir uma mensagem para uma fila</span><span class="sxs-lookup"><span data-stu-id="03d81-115">How To: Insert a Message into a Queue</span></span>
<span data-ttu-id="03d81-116">tooinsert uma mensagem para uma fila, utilize Olá **colocar\_mensagem** método para criar uma nova mensagem e adicioná-lo toohello fila.</span><span class="sxs-lookup"><span data-stu-id="03d81-116">tooinsert a message into a queue, use hello **put\_message** method to create a new message and add it toohello queue.</span></span>

```python
queue_service.put_message('taskqueue', u'Hello World')
```

## <a name="how-to-peek-at-hello-next-message"></a><span data-ttu-id="03d81-117">Como: Pré-visualizar Olá a mensagem seguinte</span><span class="sxs-lookup"><span data-stu-id="03d81-117">How To: Peek at hello Next Message</span></span>
<span data-ttu-id="03d81-118">Pode pré-visualizar a mensagem de saudação no início de Olá de um fila sem a remover da fila de Olá ao chamar Olá **peek\_mensagens** método.</span><span class="sxs-lookup"><span data-stu-id="03d81-118">You can peek at hello message in hello front of a queue without removing it from hello queue by calling hello **peek\_messages** method.</span></span> <span data-ttu-id="03d81-119">Por predefinição, **peek\_mensagens** peeks uma única mensagem.</span><span class="sxs-lookup"><span data-stu-id="03d81-119">By default, **peek\_messages** peeks at a single message.</span></span>

```python
messages = queue_service.peek_messages('taskqueue')
for message in messages:
    print(message.content)
```

## <a name="how-to-dequeue-messages"></a><span data-ttu-id="03d81-120">Como: Anular mensagens</span><span class="sxs-lookup"><span data-stu-id="03d81-120">How To: Dequeue Messages</span></span>
<span data-ttu-id="03d81-121">O código remove uma mensagem da fila em dois passos.</span><span class="sxs-lookup"><span data-stu-id="03d81-121">Your code removes a message from a queue in two steps.</span></span> <span data-ttu-id="03d81-122">Quando chamar **obter\_mensagens**, obterá a mensagem seguinte Olá numa fila por predefinição.</span><span class="sxs-lookup"><span data-stu-id="03d81-122">When you call **get\_messages**, you get hello next message in a queue by default.</span></span> <span data-ttu-id="03d81-123">Uma mensagem devolvida por **obter\_mensagens** torna-se invisível tooany outro código de leitura de mensagens desta fila.</span><span class="sxs-lookup"><span data-stu-id="03d81-123">A message returned from **get\_messages** becomes invisible tooany other code reading messages from this queue.</span></span> <span data-ttu-id="03d81-124">Por predefinição, esta mensagem permanece invisível durante 30 segundos.</span><span class="sxs-lookup"><span data-stu-id="03d81-124">By default, this message stays invisible for 30 seconds.</span></span> <span data-ttu-id="03d81-125">toofinish remover mensagem de saudação da fila de Olá, também tem de chamar **eliminar\_mensagem**.</span><span class="sxs-lookup"><span data-stu-id="03d81-125">toofinish removing hello message from hello queue, you must also call **delete\_message**.</span></span> <span data-ttu-id="03d81-126">Este processo de dois passos da remoção de uma mensagem garante que quando o código de falha tooprocess uma mensagem devido a falha de hardware ou software, outra instância do seu código pode obter a mesma mensagem e tente novamente.</span><span class="sxs-lookup"><span data-stu-id="03d81-126">This two-step process of removing a message assures that when your code fails tooprocess a message due to hardware or software failure, another instance of your code can get the same message and try again.</span></span> <span data-ttu-id="03d81-127">As chamadas de código **eliminar\_mensagem** imediatamente após a mensagem de saudação foi processada.</span><span class="sxs-lookup"><span data-stu-id="03d81-127">Your code calls **delete\_message** right after hello message has been processed.</span></span>

```python
messages = queue_service.get_messages('taskqueue')
for message in messages:
    print(message.content)
    queue_service.delete_message('taskqueue', message.id, message.pop_receipt)
```

<span data-ttu-id="03d81-128">Existem duas formas através das quais pode personalizar a obtenção de mensagens a partir de uma fila.</span><span class="sxs-lookup"><span data-stu-id="03d81-128">There are two ways you can customize message retrieval from a queue.</span></span>
<span data-ttu-id="03d81-129">Em primeiro lugar, pode obter um lote de mensagens em fila (cópia de segurança too32).</span><span class="sxs-lookup"><span data-stu-id="03d81-129">First, you can get a batch of messages (up too32).</span></span> <span data-ttu-id="03d81-130">Segundo, pode definir um tempo limite de invisibilidade superiores ou inferiores, permitindo que o código mais ou menos tempo toofully processar cada mensagem.</span><span class="sxs-lookup"><span data-stu-id="03d81-130">Second, you can set a longer or shorter invisibility timeout, allowing your code more or less time toofully process each message.</span></span> <span data-ttu-id="03d81-131">seguinte Olá código de exemplo utiliza o **obter\_mensagens** mensagens de tooget 16 método numa chamada.</span><span class="sxs-lookup"><span data-stu-id="03d81-131">hello following code example uses the **get\_messages** method tooget 16 messages in one call.</span></span> <span data-ttu-id="03d81-132">Em seguida, processa cada mensagem utilizando um ciclo for.</span><span class="sxs-lookup"><span data-stu-id="03d81-132">Then it processes each message using a for loop.</span></span> <span data-ttu-id="03d81-133">Também define Olá tempo limite de invisibilidade para cinco minutos para cada mensagem.</span><span class="sxs-lookup"><span data-stu-id="03d81-133">It also sets hello invisibility timeout to five minutes for each message.</span></span>

```python
messages = queue_service.get_messages('taskqueue', num_messages=16, visibility_timeout=5*60)
for message in messages:
    print(message.content)
    queue_service.delete_message('taskqueue', message.id, message.pop_receipt)        
```

## <a name="how-to-change-hello-contents-of-a-queued-message"></a><span data-ttu-id="03d81-134">Como: Alterar Olá conteúdo de uma mensagem em fila</span><span class="sxs-lookup"><span data-stu-id="03d81-134">How To: Change hello Contents of a Queued Message</span></span>
<span data-ttu-id="03d81-135">Pode alterar o conteúdo de Olá de uma mensagem no local na fila de Olá.</span><span class="sxs-lookup"><span data-stu-id="03d81-135">You can change hello contents of a message in-place in hello queue.</span></span> <span data-ttu-id="03d81-136">Se a mensagem representa uma tarefa de trabalho, pode utilizar esta funcionalidade tooupdate o estado de tarefa de trabalho de Olá.</span><span class="sxs-lookup"><span data-stu-id="03d81-136">If the message represents a work task, you could use this feature tooupdate the status of hello work task.</span></span> <span data-ttu-id="03d81-137">código de Olá abaixo utiliza Olá **atualizar\_mensagem** método tooupdate uma mensagem.</span><span class="sxs-lookup"><span data-stu-id="03d81-137">hello code below uses hello **update\_message** method tooupdate a message.</span></span> <span data-ttu-id="03d81-138">tempo limite de visibilidade de Olá está definido too0, que significa a mensagem é apresentada imediatamente e Olá conteúdo for atualizado.</span><span class="sxs-lookup"><span data-stu-id="03d81-138">hello visibility timeout is set too0, meaning the message appears immediately and hello content is updated.</span></span>

```python
messages = queue_service.get_messages('taskqueue')
for message in messages:
    queue_service.update_message('taskqueue', message.id, message.pop_receipt, 0, u'Hello World Again')
```

## <a name="how-to-get-hello-queue-length"></a><span data-ttu-id="03d81-139">Como: Obter Olá comprimento da fila</span><span class="sxs-lookup"><span data-stu-id="03d81-139">How To: Get hello Queue Length</span></span>
<span data-ttu-id="03d81-140">Pode obter uma estimativa do número de Olá de mensagens numa fila.</span><span class="sxs-lookup"><span data-stu-id="03d81-140">You can get an estimate of hello number of messages in a queue.</span></span> <span data-ttu-id="03d81-141">O **obter\_fila\_metadados** método pede-lhe Olá metadados sobre fila Olá tooreturn do serviço de fila e Olá **approximate_message_count**.</span><span class="sxs-lookup"><span data-stu-id="03d81-141">The **get\_queue\_metadata** method asks hello queue service tooreturn metadata about hello queue, and hello **approximate_message_count**.</span></span> <span data-ttu-id="03d81-142">resultado de Olá apenas é aproximado porque as mensagens podem ser adicionadas ou removidas depois de ter o serviço fila responde tooyour pedido.</span><span class="sxs-lookup"><span data-stu-id="03d81-142">hello result is only approximate because messages can be added or removed after the queue service responds tooyour request.</span></span>

```python
metadata = queue_service.get_queue_metadata('taskqueue')
count = metadata.approximate_message_count
```

## <a name="how-to-delete-a-queue"></a><span data-ttu-id="03d81-143">Como: Eliminar uma fila</span><span class="sxs-lookup"><span data-stu-id="03d81-143">How To: Delete a Queue</span></span>
<span data-ttu-id="03d81-144">toodelete uma fila e todas as mensagens de Olá nela contidas, chame o **eliminar\_fila** método.</span><span class="sxs-lookup"><span data-stu-id="03d81-144">toodelete a queue and all hello messages contained in it, call the **delete\_queue** method.</span></span>

```python
queue_service.delete_queue('taskqueue')
```

## <a name="next-steps"></a><span data-ttu-id="03d81-145">Passos Seguintes</span><span class="sxs-lookup"><span data-stu-id="03d81-145">Next Steps</span></span>
<span data-ttu-id="03d81-146">Agora que aprendeu as noções básicas de Olá do armazenamento de filas, siga estas toolearn ligações mais.</span><span class="sxs-lookup"><span data-stu-id="03d81-146">Now that you've learned hello basics of Queue storage, follow these links toolearn more.</span></span>

* [<span data-ttu-id="03d81-147">Centro para Programadores do Python</span><span class="sxs-lookup"><span data-stu-id="03d81-147">Python Developer Center</span></span>](/develop/python/)
* [<span data-ttu-id="03d81-148">API REST dos Serviços do Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="03d81-148">Azure Storage Services REST API</span></span>](http://msdn.microsoft.com/library/azure/dd179355)
* <span data-ttu-id="03d81-149">[Blogue da Equipa de Armazenamento do Azure]</span><span class="sxs-lookup"><span data-stu-id="03d81-149">[Azure Storage Team Blog]</span></span>
* <span data-ttu-id="03d81-150">[SDK de armazenamento do Microsoft Azure para Python]</span><span class="sxs-lookup"><span data-stu-id="03d81-150">[Microsoft Azure Storage SDK for Python]</span></span>

[Blogue da Equipa de Armazenamento do Azure]: http://blogs.msdn.com/b/windowsazurestorage/
[SDK de armazenamento do Microsoft Azure para Python]: https://github.com/Azure/azure-storage-python