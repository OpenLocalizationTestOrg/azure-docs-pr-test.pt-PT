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
# <a name="how-toouse-queue-storage-from-python"></a>Como toouse armazenamento de filas do Python
[!INCLUDE [storage-selector-queue-include](../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a>Descrição geral
Este guia mostra como tooperform cenários comuns utilizando Olá o serviço de armazenamento de filas do Azure. Exemplos de Olá são escritos no Python e utilizam Olá [SDK de armazenamento do Microsoft Azure para Python]. Olá os cenários abrangidos incluem **inserir**, **leitura**, **obter**, e **eliminar** fila de mensagens, bem como  **criar e eliminar filas**. Para obter mais informações sobre as filas, consulte a secção toohello [passos].

[!INCLUDE [storage-queue-concepts-include](../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="how-to-create-a-queue"></a>Como: Criar uma fila
Olá **QueueService** objeto permite-lhe trabalhar com as filas. Olá código seguinte cria um **QueueService** objeto. Adicione o seguinte Olá perto do topo Olá de qualquer ficheiro de Python no qual pretende tooprogrammatically acesso Storage do Azure:

```python
from azure.storage.queue import QueueService
```

Olá código seguinte cria um **QueueService** utilizando Olá chave conta do storage conta e o nome do objeto. Substitua 'myaccount' e 'mykey' com o nome da conta e a chave.

```python
queue_service = QueueService(account_name='myaccount', account_key='mykey')

queue_service.create_queue('taskqueue')
```

## <a name="how-to-insert-a-message-into-a-queue"></a>Como: Introduzir uma mensagem para uma fila
tooinsert uma mensagem para uma fila, utilize Olá **colocar\_mensagem** método para criar uma nova mensagem e adicioná-lo toohello fila.

```python
queue_service.put_message('taskqueue', u'Hello World')
```

## <a name="how-to-peek-at-hello-next-message"></a>Como: Pré-visualizar Olá a mensagem seguinte
Pode pré-visualizar a mensagem de saudação no início de Olá de um fila sem a remover da fila de Olá ao chamar Olá **peek\_mensagens** método. Por predefinição, **peek\_mensagens** peeks uma única mensagem.

```python
messages = queue_service.peek_messages('taskqueue')
for message in messages:
    print(message.content)
```

## <a name="how-to-dequeue-messages"></a>Como: Anular mensagens
O código remove uma mensagem da fila em dois passos. Quando chamar **obter\_mensagens**, obterá a mensagem seguinte Olá numa fila por predefinição. Uma mensagem devolvida por **obter\_mensagens** torna-se invisível tooany outro código de leitura de mensagens desta fila. Por predefinição, esta mensagem permanece invisível durante 30 segundos. toofinish remover mensagem de saudação da fila de Olá, também tem de chamar **eliminar\_mensagem**. Este processo de dois passos da remoção de uma mensagem garante que quando o código de falha tooprocess uma mensagem devido a falha de hardware ou software, outra instância do seu código pode obter a mesma mensagem e tente novamente. As chamadas de código **eliminar\_mensagem** imediatamente após a mensagem de saudação foi processada.

```python
messages = queue_service.get_messages('taskqueue')
for message in messages:
    print(message.content)
    queue_service.delete_message('taskqueue', message.id, message.pop_receipt)
```

Existem duas formas através das quais pode personalizar a obtenção de mensagens a partir de uma fila.
Em primeiro lugar, pode obter um lote de mensagens em fila (cópia de segurança too32). Segundo, pode definir um tempo limite de invisibilidade superiores ou inferiores, permitindo que o código mais ou menos tempo toofully processar cada mensagem. seguinte Olá código de exemplo utiliza o **obter\_mensagens** mensagens de tooget 16 método numa chamada. Em seguida, processa cada mensagem utilizando um ciclo for. Também define Olá tempo limite de invisibilidade para cinco minutos para cada mensagem.

```python
messages = queue_service.get_messages('taskqueue', num_messages=16, visibility_timeout=5*60)
for message in messages:
    print(message.content)
    queue_service.delete_message('taskqueue', message.id, message.pop_receipt)        
```

## <a name="how-to-change-hello-contents-of-a-queued-message"></a>Como: Alterar Olá conteúdo de uma mensagem em fila
Pode alterar o conteúdo de Olá de uma mensagem no local na fila de Olá. Se a mensagem representa uma tarefa de trabalho, pode utilizar esta funcionalidade tooupdate o estado de tarefa de trabalho de Olá. código de Olá abaixo utiliza Olá **atualizar\_mensagem** método tooupdate uma mensagem. tempo limite de visibilidade de Olá está definido too0, que significa a mensagem é apresentada imediatamente e Olá conteúdo for atualizado.

```python
messages = queue_service.get_messages('taskqueue')
for message in messages:
    queue_service.update_message('taskqueue', message.id, message.pop_receipt, 0, u'Hello World Again')
```

## <a name="how-to-get-hello-queue-length"></a>Como: Obter Olá comprimento da fila
Pode obter uma estimativa do número de Olá de mensagens numa fila. O **obter\_fila\_metadados** método pede-lhe Olá metadados sobre fila Olá tooreturn do serviço de fila e Olá **approximate_message_count**. resultado de Olá apenas é aproximado porque as mensagens podem ser adicionadas ou removidas depois de ter o serviço fila responde tooyour pedido.

```python
metadata = queue_service.get_queue_metadata('taskqueue')
count = metadata.approximate_message_count
```

## <a name="how-to-delete-a-queue"></a>Como: Eliminar uma fila
toodelete uma fila e todas as mensagens de Olá nela contidas, chame o **eliminar\_fila** método.

```python
queue_service.delete_queue('taskqueue')
```

## <a name="next-steps"></a>Passos Seguintes
Agora que aprendeu as noções básicas de Olá do armazenamento de filas, siga estas toolearn ligações mais.

* [Centro para Programadores do Python](/develop/python/)
* [API REST dos Serviços do Armazenamento do Azure](http://msdn.microsoft.com/library/azure/dd179355)
* [Blogue da Equipa de Armazenamento do Azure]
* [SDK de armazenamento do Microsoft Azure para Python]

[Blogue da Equipa de Armazenamento do Azure]: http://blogs.msdn.com/b/windowsazurestorage/
[SDK de armazenamento do Microsoft Azure para Python]: https://github.com/Azure/azure-storage-python