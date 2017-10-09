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
# <a name="how-toouse-queue-storage-from-ruby"></a>Como toouse armazenamento de filas do Ruby
[!INCLUDE [storage-selector-queue-include](../../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a>Descrição geral
Este guia mostra como tooperform cenários comuns utilizando Olá o serviço de armazenamento de filas do Microsoft Azure. Exemplos de Olá são escritos utilizando Olá Ruby Azure API.
Olá os cenários abrangidos incluem **inserir**, **leitura**, **obter**, e **eliminar** fila de mensagens, bem como  **criar e eliminar filas**.

[!INCLUDE [storage-queue-concepts-include](../../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="create-a-ruby-application"></a>Criar uma aplicação Ruby
Crie uma aplicação Ruby. Para obter instruções, consulte [Ruby na aplicação Rails Web numa VM do Azure](../../virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md).

## <a name="configure-your-application-tooaccess-storage"></a>Configurar a sua aplicação tooAccess armazenamento
toouse storage do Azure, terá de toodownload e utilize Olá Ruby pacote do azure, que inclui um conjunto de bibliotecas de conveniência que comunicam com os serviços de REST de armazenamento Olá.

### <a name="use-rubygems-tooobtain-hello-package"></a>Utilize o pacote de Olá RubyGems tooobtain
1. Utilize uma interface de linha de comandos, como **PowerShell** (Windows), **Terminal** (Mac), ou **Bash** (Unix).
2. Escreva "gem instalar azure" gem do Olá comando janela tooinstall Olá e as dependências.

### <a name="import-hello-package"></a>Importar o pacote de Olá
Utilize o editor de texto favorito, adicione Olá toohello superior de Olá Ruby ficheiro onde pretende toouse armazenamento os seguintes:

```ruby
require "azure"
```

## <a name="setup-an-azure-storage-connection"></a>Configurar uma ligação de armazenamento do Azure
módulo Olá do azure será lida a variáveis de ambiente de Olá **AZURE\_armazenamento\_conta** e **AZURE\_armazenamento\_ACCESS_KEY** para as informações necessárias tooconnect tooyour conta de armazenamento Azure. Se estas variáveis de ambiente não estiver definidas, tem de especificar as informações de conta de Olá antes de utilizar **Azure::QueueService** com Olá seguinte código:

```ruby
Azure.config.storage_account_name = "<your azure storage account>"
Azure.config.storage_access_key = "<your Azure storage access key>"
```

tooobtain estes valores de um clássico ou do armazenamento do Resource Manager conta no Olá portal do Azure:

1. Inicie sessão no toohello [portal do Azure](https://portal.azure.com).
2. Navegue toohello conta de armazenamento que pretende toouse.
3. No painel de definições de Olá no Olá direito, clique em **chaves de acesso**.
4. Olá acesso painel chaves que aparece, verá a chave de acesso de Olá 1 e 2 a chave de acesso. Pode utilizar qualquer um destes. 
5. Clique em Olá cópia ícone toocopy Olá toohello chave da área de transferência. 

## <a name="how-to-create-a-queue"></a>Como: Criar uma fila
Olá código seguinte cria um **Azure::QueueService** objeto, que permite-lhe toowork com as filas.

```ruby
azure_queue_service = Azure::QueueService.new
```

Olá utilize **create_queue()** método toocreate uma fila com Olá especificado o nome.

```ruby
begin
  azure_queue_service.create_queue("test-queue")
rescue
  puts $!
end
```

## <a name="how-to-insert-a-message-into-a-queue"></a>Como: Introduzir uma mensagem para uma fila
tooinsert uma mensagem para uma fila, utilize Olá **create_message()** método toocreate uma nova mensagem e adicioná-la toohello fila.

```ruby
azure_queue_service.create_message("test-queue", "test message")
```

## <a name="how-to-peek-at-hello-next-message"></a>Como: Pré-visualizar Olá a mensagem seguinte
Pode pré-visualizar a mensagem de saudação no início de Olá de um fila sem a remover da fila de Olá ao chamar Olá **peek\_messages()** método. Por predefinição, **peek\_messages()** peeks uma única mensagem. Também pode especificar mensagens quantos quiser toopeek.

```ruby
result = azure_queue_service.peek_messages("test-queue",
  {:number_of_messages => 10})
```

## <a name="how-to-dequeue-hello-next-message"></a>Como: Anular Olá a mensagem seguinte
Pode remover uma mensagem da fila em dois passos.

1. Quando chamar **lista\_messages()**, obterá a mensagem seguinte Olá numa fila por predefinição. Também pode especificar mensagens quantos quiser tooget. Olá, as mensagens resultantes da **lista\_messages()** torna-se invisível tooany outro código de leitura de mensagens desta fila. Passar no tempo limite de visibilidade de Olá em segundos, como um parâmetro.
2. toofinish remover mensagem de saudação da fila de Olá, também tem de chamar **delete_message()**.

Este processo de dois passos da remoção de uma mensagem garante que, quando os tooprocess de falha de código pode obter uma mensagem devido a falha de toohardware ou de software, outra instância do seu código Olá mesma mensagem e tente novamente. As chamadas de código **eliminar\_message()** imediatamente após a mensagem de saudação foi processada.

```ruby
messages = azure_queue_service.list_messages("test-queue", 30)
azure_queue_service.delete_message("test-queue", 
  messages[0].id, messages[0].pop_receipt)
```

## <a name="how-to-change-hello-contents-of-a-queued-message"></a>Como: Alterar Olá conteúdo de uma mensagem em fila
Pode alterar o conteúdo de Olá de uma mensagem no local na fila de Olá. código de Olá abaixo utiliza Olá **update_message()** método tooupdate uma mensagem. método de Olá irá devolver uma cadeia de identificação que contém Olá pop a receção mensagem da fila de saudação e um valor de tempo de data UTC representa quando a mensagem de saudação vai estar visível na fila de Olá.

```ruby
message = azure_queue_service.list_messages("test-queue", 30)
pop_receipt, time_next_visible = azure_queue_service.update_message(
  "test-queue", message.id, message.pop_receipt, "updated test message", 
  30)
```

## <a name="how-to-additional-options-for-dequeuing-messages"></a>Como: Mensagens de opções adicionais para Dequeuing
Existem duas formas através das quais pode personalizar a obtenção de mensagens a partir de uma fila.

1. Pode obter um lote de mensagem.
2. Pode definir um tempo limite de invisibilidade superiores ou inferiores, permitindo que o código mais ou menos tempo toofully processar cada mensagem.

Olá exemplo de código seguinte utiliza Olá **lista\_messages()** mensagens tooget 15 de método numa chamada. Em seguida, imprime e elimina a cada mensagem. Também define minutos toofive de tempo limite de invisibilidade do Olá para cada mensagem.

```ruby
azure_queue_service.list_messages("test-queue", 300
  {:number_of_messages => 15}).each do |m|
  puts m.message_text
  azure_queue_service.delete_message("test-queue", m.id, m.pop_receipt)
end
```

## <a name="how-to-get-hello-queue-length"></a>Como: Obter Olá comprimento da fila
Pode obter uma estimativa do número de Olá de mensagens em fila Olá. Olá **obter\_fila\_metadata()** método pede-lhe Olá fila serviço tooreturn Olá mensagem aproximado contagem e metadados sobre fila Olá.

```ruby
message_count, metadata = azure_queue_service.get_queue_metadata(
  "test-queue")
```

## <a name="how-to-delete-a-queue"></a>Como: Eliminar uma fila
toodelete uma fila e todas as mensagens de Olá nela contidas, chamada Olá **eliminar\_queue()** método no objeto de fila de Olá.

```ruby
azure_queue_service.delete_queue("test-queue")
```

## <a name="next-steps"></a>Passos Seguintes
Agora que aprendeu as noções básicas de Olá do armazenamento de filas, siga estas toolearn ligações sobre as tarefas de armazenamento mais complexas.

* Visite Olá [blogue da equipa de armazenamento do Azure](http://blogs.msdn.com/b/windowsazurestorage/)
* Visite Olá [Azure SDK para Ruby](https://github.com/WindowsAzure/azure-sdk-for-ruby) repositório no GitHub

Para ver uma comparação entre Olá serviço de fila do Azure abordado neste artigo e filas de barramento de serviço de Azure abordado Olá [como toouse filas do Service Bus](/develop/ruby/how-to-guides/service-bus-queues/) artigo, consulte [filas do Azure e filas do Service Bus - comparados e Contrasted](../../service-bus-messaging/service-bus-azure-and-service-bus-queues-compared-contrasted.md)
