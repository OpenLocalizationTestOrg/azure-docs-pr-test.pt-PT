---
title: aaaHow toouse Azure Table Storage do Ruby | Microsoft Docs
description: "Armazene dados estruturados na nuvem de Olá utilizando o Table storage do Azure, um arquivo de dados NoSQL."
services: cosmos-db
documentationcenter: ruby
author: mimig1
manager: jhubbard
editor: 
ms.assetid: 047cd9ff-17d3-4c15-9284-1b5cc61a3224
ms.service: cosmos-db
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: ruby
ms.topic: article
ms.date: 12/08/2016
ms.author: mimig
ms.openlocfilehash: 2f9eb5a9160b551d6d1d198869787070c402b1d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-table-storage-from-ruby"></a>Como toouse Azure Table Storage do Ruby
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

## <a name="overview"></a>Descrição geral
Este guia mostra como tooperform cenários comuns utilizando Olá o serviço de Azure Table. Exemplos de Olá são escritos utilizando Olá Ruby API. Olá os cenários abrangidos incluem **criar e eliminar uma tabela, a inserir e consultar entidades numa tabela**.

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-ruby-application"></a>Criar uma aplicação Ruby
Para obter instruções sobre como toocreate uma aplicação Ruby, consulte [Ruby na aplicação Rails Web numa VM do Azure](../virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md).

## <a name="configure-your-application-tooaccess-storage"></a>Configurar o armazenamento de tooaccess de aplicação
toouse Storage do Azure, terá de toodownload e utilize Olá Ruby pacote do azure que inclui um conjunto de bibliotecas de conveniência que comunicam com os serviços de armazenamento REST Olá.

### <a name="use-rubygems-tooobtain-hello-package"></a>Utilize o pacote de Olá RubyGems tooobtain
1. Utilize uma interface de linha de comandos, como **PowerShell** (Windows), **Terminal** (Mac), ou **Bash** (Unix).
2. Tipo **azure de instalação gem** gem do Olá comando janela tooinstall Olá e dependências.

### <a name="import-hello-package"></a>Importar o pacote de Olá
Utilize o editor de texto favorito, adicione Olá toohello superior de Olá Ruby ficheiro onde pretende toouse armazenamento os seguintes:

```ruby
require "azure"
```

## <a name="set-up-an-azure-storage-connection"></a>Configurar uma ligação de armazenamento do Azure
Olá módulo do azure será lida a variáveis de ambiente de Olá **AZURE\_armazenamento\_conta** e **AZURE\_armazenamento\_acesso\_chave**para obter informações de conta de armazenamento do Azure tooconnect tooyour necessário. Se estas variáveis de ambiente não estiver definidas, tem de especificar as informações de conta de Olá antes de utilizar **Azure::TableService** com Olá seguinte código:

```ruby
Azure.config.storage_account_name = "<your azure storage account>"
Azure.config.storage_access_key = "<your azure storage access key>"
```

tooobtain estes valores de um clássico ou do armazenamento do Resource Manager conta no Olá portal do Azure:

1. Inicie sessão no toohello [portal do Azure](https://portal.azure.com).
2. Navegue toohello conta de armazenamento que pretende toouse.
3. No painel de definições de Olá no Olá direito, clique em **chaves de acesso**.
4. Olá acesso painel chaves que aparece, verá a chave de acesso de Olá 1 e 2 a chave de acesso. Pode utilizar qualquer um destes.
5. Clique em Olá cópia ícone toocopy Olá toohello chave da área de transferência.

## <a name="create-a-table"></a>Criar uma tabela
Olá **Azure::TableService** objeto permite-lhe trabalhar com tabelas e entidades. toocreate uma tabela, utilize Olá **criar\_table()** método. Olá exemplo seguinte cria uma tabela ou impressões Olá erro se existir alguma.

```ruby
azure_table_service = Azure::TableService.new
begin
    azure_table_service.create_table("testtable")
rescue
    puts $!
end
```

## <a name="add-an-entity-tooa-table"></a>Adicionar uma tabela de tooa entidade
tooadd uma entidade, primeiro crie um objeto de hash, que define as propriedades de entidade. Tenha em atenção que para cada entidade tem de especificar um **PartitionKey** e **RowKey**. Estas são Olá identificadores exclusivos da sua entidades e são valores que podem ser consultados muito mais rapidamente do que as outras propriedades. Storage do Azure utiliza **PartitionKey** tooautomatically distribuir entidades da tabela de Olá através de vários nós de armazenamento. Entidades com Olá mesmo **PartitionKey** são armazenadas no Olá mesmo nó. Olá **RowKey** é Olá da entidade de Olá dentro de partição Olá pertence a um ID exclusivo.

```ruby
entity = { "content" => "test entity",
    :PartitionKey => "test-partition-key", :RowKey => "1" }
azure_table_service.insert_entity("testtable", entity)
```

## <a name="update-an-entity"></a>Atualizar uma entidade
Existem vários métodos tooupdate de disponível uma entidade existente:

* **Atualizar\_entity():** atualizar uma entidade existente, substituindo-lo.
* **intercalação\_entity():** atualiza uma entidade existente, a intercalação novos valores de propriedade na entidade existente Olá.
* **Inserir\_ou\_intercalação\_entity():** atualiza uma entidade existente, substituindo-lo. Se nenhuma entidade de existir, será inserido um novo:
* **Inserir\_ou\_substituir\_entity():** atualiza uma entidade existente, a intercalação novos valores de propriedade na entidade existente Olá. Se nenhuma entidade de existir, será inserido um novo.

Olá exemplo seguinte demonstra a atualizar uma entidade utilizando **atualizar\_entity()**:

```ruby
entity = { "content" => "test entity with updated content",
    :PartitionKey => "test-partition-key", :RowKey => "1" }
azure_table_service.update_entity("testtable", entity)
```

Com **atualizar\_entity()** e **intercalação\_entity()**, se a entidade de Olá que estão a atualizar não existir, a operação de atualização de Olá irá falhar. Por conseguinte, se desejar toostore uma entidade, independentemente de já existir, deve em vez disso, utilizar **inserir\_ou\_substituir\_entity()** ou **inserir\_ou \_intercalação\_entity()**.

## <a name="work-with-groups-of-entities"></a>Trabalhar com grupos de entidades
Por vezes, faz sentido toosubmit várias operações em conjunto no tooensure batch atomic processados pelo servidor Olá. tooaccomplish que, primeiro crie um **Batch** de objeto e, em seguida, utilizar Olá **executar\_batch()** método no **TableService**. Olá exemplo seguinte demonstra submeter duas entidades com RowKey 2 e 3 num batch. Tenha em atenção que só funciona para entidades com Olá PartitionKey mesmo.

```ruby
azure_table_service = Azure::TableService.new
batch = Azure::Storage::Table::Batch.new("testtable",
    "test-partition-key") do
    insert "2", { "content" => "new content 2" }
    insert "3", { "content" => "new content 3" }
end
results = azure_table_service.execute_batch(batch)
```

## <a name="query-for-an-entity"></a>Consulta de uma entidade
tooquery uma entidade numa tabela, utilize Olá **obter\_entity()** método, transferindo o nome da tabela Olá, **PartitionKey** e **RowKey**.

```ruby
result = azure_table_service.get_entity("testtable", "test-partition-key",
    "1")
```

## <a name="query-a-set-of-entities"></a>Consulta de um conjunto de entidades
tooquery um conjunto de entidades numa tabela, crie um objeto de hash de consulta e utilize Olá **consulta\_entities()** método. Olá exemplo seguinte demonstra obter todas as entidades de Olá com Olá mesmo **PartitionKey**:

```ruby
query = { :filter => "PartitionKey eq 'test-partition-key'" }
result, token = azure_table_service.query_entities("testtable", query)
```

> [!NOTE]
> Se o conjunto de resultados de Olá é demasiado grande para uma única consulta tooreturn, um token de continuação será devolvido que pode utilizar as páginas subsequentes tooretrieve.
>
>

## <a name="query-a-subset-of-entity-properties"></a>Consultar um subconjunto de propriedades de entidade
Uma tabela de tooa de consulta pode obter apenas algumas propriedades de uma entidade. Esta técnica, denominada "projeção", reduz a largura de banda e pode melhorar o desempenho de consulta, especialmente para entidades grandes. Cláusula de seleção de Olá de utilização e os nomes de Olá de passagem de Olá propriedades gostaria toobring através de toohello cliente.

```ruby
query = { :filter => "PartitionKey eq 'test-partition-key'",
    :select => ["content"] }
result, token = azure_table_service.query_entities("testtable", query)
```

## <a name="delete-an-entity"></a>Eliminar uma entidade
toodelete uma entidade, utilize Olá **eliminar\_entity()** método. É necessário toopass no nome de Olá da tabela de Olá que contém a entidade de Olá, Olá PartitionKey e RowKey da entidade de Olá.

```ruby
azure_table_service.delete_entity("testtable", "test-partition-key", "1")
```

## <a name="delete-a-table"></a>Eliminar uma tabela
toodelete uma tabela, utilize Olá **eliminar\_table()** método e passar no nome de Olá da Olá pretende toodelete de tabela.

```ruby
azure_table_service.delete_table("testtable")
```

## <a name="next-steps"></a>Passos seguintes

* [Explorador de armazenamento do Microsoft Azure](../vs-azure-tools-storage-manage-with-storage-explorer.md) é uma aplicação autónoma e gratuita da Microsoft permite-lhe toowork visualmente com dados de armazenamento do Azure no Windows, macOS e Linux.
* [Azure SDK para Ruby](http://github.com/WindowsAzure/azure-sdk-for-ruby) repositório no GitHub

