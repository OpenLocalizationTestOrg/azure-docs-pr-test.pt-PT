---
title: aaaHow toouse armazenamento de tabelas (C++) | Microsoft Docs
description: "Armazene dados estruturados na nuvem de Olá utilizando o Table storage do Azure, um arquivo de dados NoSQL."
services: storage
documentationcenter: .net
author: seguler
manager: jahogg
editor: tysonn
ms.assetid: f191f308-e4b2-4de9-85cb-551b82b1ea7c
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/28/2017
ms.author: seguler
ms.openlocfilehash: 8eee0031350ab6ff3f76fb288b2f896687aa17a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-table-storage-from-c"></a>Como toouse Table storage do C++
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

## <a name="overview"></a>Descrição geral
Este guia irá mostrar como tooperform cenários comuns utilizando Olá o serviço de armazenamento de tabelas do Azure. Exemplos de Olá são escritos em C++ e utilizar Olá [biblioteca de clientes do Storage do Azure para C++](https://github.com/Azure/azure-storage-cpp/blob/master/README.md). Olá os cenários abrangidos incluem **criar e eliminar uma tabela** e **trabalhar com as entidades da tabela**.

> [!NOTE]
> Destinos neste guia Olá biblioteca de clientes do Storage do Azure para C++ versão 1.0.0 e acima. Olá recomendada de versão é biblioteca de clientes de armazenamento 2.2.0, que está disponível através de [NuGet](http://www.nuget.org/packages/wastorage) ou [GitHub](https://github.com/Azure/azure-storage-cpp/).
> 
> 

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-c-application"></a>Criar uma aplicação do C++
Neste guia, irá utilizar as funcionalidades de armazenamento que podem ser executadas dentro de uma aplicação de C++. toodo por isso, terá de tooinstall hello biblioteca de clientes do Storage do Azure para C++ e criar uma conta de armazenamento do Azure na sua subscrição do Azure.  

Olá tooinstall biblioteca de clientes do Storage do Azure para C++, pode utilizar Olá seguintes métodos:

* **Linux:** siga as instruções de Olá fornecidas no Olá [biblioteca de clientes do Storage do Azure para o ficheiro Leia-me do C++](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) página.  
* **Windows:** no Visual Studio, clique em **ferramentas > Gestor de pacotes NuGet > consola do Gestor de pacotes**. Seguinte Olá de tipo de comando para Olá [consola do Gestor de pacotes NuGet](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) e prima Enter.  
  
     Pacote de instalação wastorage

## <a name="configure-your-application-tooaccess-table-storage"></a>Configurar a aplicação tooaccess o Table storage
Adicione a seguinte Olá incluem parte superior do toohello de declarações do ficheiro de C++ de olá onde pretende que as tabelas de tooaccess APIs de armazenamento do Azure Olá toouse:  

```cpp
#include <was/storage_account.h>
#include <was/table.h>
```

## <a name="set-up-an-azure-storage-connection-string"></a>Configurar uma cadeia de ligação de armazenamento do Azure
Um cliente de armazenamento do Azure utiliza um armazenamento cadeia toostore pontos finais da ligação e as credenciais para aceder aos serviços de gestão de dados. Quando executar uma aplicação de cliente, tem de fornecer cadeia de ligação de armazenamento de Olá Olá seguir o formato. Utilize o nome de Olá do seu armazenamento conta e Olá armazenamento chave de acesso de conta de armazenamento Olá listado no Olá [Portal do Azure](https://portal.azure.com) para Olá *AccountName* e *AccountKey* valores. Para obter informações sobre as contas do storage e chaves de acesso, consulte [contas do storage do Azure sobre](storage-create-storage-account.md). Este exemplo mostra como podem declarar uma cadeia de ligação do campo estático toohold Olá:  

```cpp
// Define hello connection string with your values.
const utility::string_t storage_connection_string(U("DefaultEndpointsProtocol=https;AccountName=your_storage_account;AccountKey=your_storage_account_key"));
```

tootest a aplicação no seu computador baseado em Windows local, pode utilizar Olá Azure [emulador do storage](storage-use-emulator.md) que é instalado com Olá [Azure SDK](https://azure.microsoft.com/downloads/). emulador do storage Olá é um utilitário que simula Olá tabela, fila e Blob do Azure serviços disponíveis no computador de desenvolvimento local. Olá exemplo seguinte mostra como podem declarar um campo estático toohold Olá ligação cadeia tooyour local emulador do storage:  

```cpp
// Define hello connection string with Azure storage emulator.
const utility::string_t storage_connection_string(U("UseDevelopmentStorage=true;"));  
```

toostart Olá emulador do storage do Azure, clique em Olá **iniciar** botão ou prima tecla de Windows hello. Começa a escrever **emulador do Storage do Azure**e, em seguida, selecione **emulador do Storage do Microsoft Azure** da lista de Olá das aplicações.  

Olá exemplos seguintes partem do princípio que utiliza um destes dois métodos tooget Olá armazenamento da cadeia de ligação.  

## <a name="retrieve-your-connection-string"></a>Obter a cadeia de ligação
Pode utilizar Olá **cloud_storage_account** classe toorepresent as informações da conta de armazenamento. tooretrieve informações da cadeia de ligação de armazenamento Olá de conta de armazenamento, pode utilizar o método de análise Olá.

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);
```

Em seguida, obter uma referência tooa **cloud_table_client** classe, que permite-lhe obter objetos de referência para as tabelas e entidades armazenadas no Olá serviço de armazenamento de tabela. Olá código seguinte cria um **cloud_table_client** objeto através da utilização de objeto de conta de armazenamento de Olá vamos obter acima:  

```cpp
// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();
```

## <a name="create-a-table"></a>Criar uma tabela
A **cloud_table_client** objeto permite-lhe obter objetos de referência para as tabelas e entidades. Olá código seguinte cria um **cloud_table_client** objeto e utiliza-toocreate uma nova tabela.

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);  

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Retrieve a reference tooa table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Create hello table if it doesn't exist.
table.create_if_not_exists();  
```

## <a name="add-an-entity-tooa-table"></a>Adicionar uma tabela de tooa entidade
tooadd uma tabela de tooa de entidade, crie um novo **table_entity** objeto e transmita-demasiado**table_operation::insert_entity**. Olá seguinte código utiliza nome próprio do cliente Olá como chave de linha de Olá e o apelido como chave de partição Olá. Em conjunto, a partição de uma entidade e a chave de linha de identificar exclusivamente entidade Olá na tabela de Olá. As chaves de partição de entidades com Olá a mesma chave de partição pode ser consultada mais rapidamente do que aqueles com diferentes, mas utilizar várias chaves de partição permite maior escalabilidade da operação paralela. Para obter mais informações, consulte [Microsoft Azure armazenamento desempenho e escalabilidade lista de verificação](storage-performance-checklist.md).

Olá código seguinte cria uma nova instância do **table_entity** com algumas toobe de dados de cliente armazenado. Olá código seguinte chama **table_operation::insert_entity** toocreate um **table_operation** tooinsert uma entidade de objeto para uma tabela e associa Olá nova entidade de tabela com o mesmo. Por fim, Olá código chama Olá executar o método num Olá **cloud_table** objeto. E Olá novo **table_operation** envia um pedido toohello tabela serviço tooinsert Olá nova entidade de cliente na tabela de "pessoas" Olá.  

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Retrieve a reference tooa table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Create hello table if it doesn't exist.
table.create_if_not_exists();

// Create a new customer entity.
azure::storage::table_entity customer1(U("Harp"), U("Walter"));

azure::storage::table_entity::properties_type& properties = customer1.properties();
properties.reserve(2);
properties[U("Email")] = azure::storage::entity_property(U("Walter@contoso.com"));

properties[U("Phone")] = azure::storage::entity_property(U("425-555-0101"));

// Create hello table operation that inserts hello customer entity.
azure::storage::table_operation insert_operation = azure::storage::table_operation::insert_entity(customer1);

// Execute hello insert operation.
azure::storage::table_result insert_result = table.execute(insert_operation);
```

## <a name="insert-a-batch-of-entities"></a>Inserir um lote de entidades
Pode inserir um lote de entidades toohello serviço tabela numa operação de escrita. Olá código seguinte cria um **table_batch_operation** de objeto e, em seguida, adiciona três inserir tooit de operações. Cada operação de inserção é adicionada ao criar um novo objeto de entidade, os respetivos valores, a definição e, em seguida, ao chamar Olá inserir método no Olá **table_batch_operation** operação de inserção de entidade de Olá tooassociate objeto com um novo. Em seguida, **cloud_table.execute** é designado por operação de Olá tooexecute.  

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for hello table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Define a batch operation.
azure::storage::table_batch_operation batch_operation;

// Create a customer entity and add it toohello table.
azure::storage::table_entity customer1(U("Smith"), U("Jeff"));

azure::storage::table_entity::properties_type& properties1 = customer1.properties();
properties1.reserve(2);
properties1[U("Email")] = azure::storage::entity_property(U("Jeff@contoso.com"));
properties1[U("Phone")] = azure::storage::entity_property(U("425-555-0104"));

// Create another customer entity and add it toohello table.
azure::storage::table_entity customer2(U("Smith"), U("Ben"));

azure::storage::table_entity::properties_type& properties2 = customer2.properties();
properties2.reserve(2);
properties2[U("Email")] = azure::storage::entity_property(U("Ben@contoso.com"));
properties2[U("Phone")] = azure::storage::entity_property(U("425-555-0102"));

// Create a third customer entity tooadd toohello table.
azure::storage::table_entity customer3(U("Smith"), U("Denise"));

azure::storage::table_entity::properties_type& properties3 = customer3.properties();
properties3.reserve(2);
properties3[U("Email")] = azure::storage::entity_property(U("Denise@contoso.com"));
properties3[U("Phone")] = azure::storage::entity_property(U("425-555-0103"));

// Add customer entities toohello batch insert operation.
batch_operation.insert_or_replace_entity(customer1);
batch_operation.insert_or_replace_entity(customer2);
batch_operation.insert_or_replace_entity(customer3);

// Execute hello batch operation.
std::vector<azure::storage::table_result> results = table.execute_batch(batch_operation);
```

Toonote algumas coisas nas operações de lote:  

* Pode efetuar cópias de segurança too100 insert, eliminar, intercalação, substituir, as operações de inserção ou intercalação e inserir ou substituir em qualquer combinação num batch único.  
* Uma operação em lote pode ter uma operação de obter, se esta é uma operação em lote de Olá apenas Olá.  
* Todas as entidades numa operação batch único tem de ter Olá mesma chave de partição.  
* Uma operação em lote é limitado tooa payload de dados de 4 MB.  

## <a name="retrieve-all-entities-in-a-partition"></a>Obter todas as entidades numa partição
tooquery uma tabela para todas as entidades numa partição, utilize um **table_query** objeto. Olá exemplo de código seguinte especifica um filtro para entidades em que "Santos" é a chave de partição Olá. Este exemplo imprime os campos de Olá de cada entidade na consola de toohello de resultados de consulta Olá.  

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for hello table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Construct hello query operation for all customer entities where PartitionKey="Smith".
azure::storage::table_query query;

query.set_filter_string(azure::storage::table_query::generate_filter_condition(U("PartitionKey"), azure::storage::query_comparison_operator::equal, U("Smith")));

// Execute hello query.
azure::storage::table_query_iterator it = table.execute_query(query);

// Print hello fields for each customer.
azure::storage::table_query_iterator end_of_results;
for (; it != end_of_results; ++it)
{
    const azure::storage::table_entity::properties_type& properties = it->properties();

    std::wcout << U("PartitionKey: ") << it->partition_key() << U(", RowKey: ") << it->row_key()
        << U(", Property1: ") << properties.at(U("Email")).string_value()
        << U(", Property2: ") << properties.at(U("Phone")).string_value() << std::endl;
}  
```

consulta de Olá neste exemplo inclui todas as entidades de Olá que correspondem aos critérios de filtro de Olá. Se tiver tabelas grandes e precisa, muitas vezes, as entidades da tabela toodownload Olá, recomendamos que armazene os dados em blobs de armazenamento do Azure em vez disso.

## <a name="retrieve-a-range-of-entities-in-a-partition"></a>Obter um intervalo de entidades numa partição
Se não quiser tooquery todas as entidades de Olá numa partição, pode especificar um intervalo através da combinação de filtro de chave de partição de Olá com um filtro de chave de linha. Olá exemplo de código seguinte utiliza dois filtros tooget todas as entidades na partição "Santos", em que a chave de linha de Olá (nome próprio) começa com uma letra anterior ao "E" Olá por letras do alfabeto e, em seguida, imprime os resultados da consulta Olá.  

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for hello table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Create hello table query.
azure::storage::table_query query;

query.set_filter_string(azure::storage::table_query::combine_filter_conditions(
    azure::storage::table_query::generate_filter_condition(U("PartitionKey"),
    azure::storage::query_comparison_operator::equal, U("Smith")),
    azure::storage::query_logical_operator::op_and,
    azure::storage::table_query::generate_filter_condition(U("RowKey"), azure::storage::query_comparison_operator::less_than, U("E"))));

// Execute hello query.
azure::storage::table_query_iterator it = table.execute_query(query);

// Loop through hello results, displaying information about hello entity.
azure::storage::table_query_iterator end_of_results;
for (; it != end_of_results; ++it)
{
    const azure::storage::table_entity::properties_type& properties = it->properties();

    std::wcout << U("PartitionKey: ") << it->partition_key() << U(", RowKey: ") << it->row_key()
        << U(", Property1: ") << properties.at(U("Email")).string_value()
        << U(", Property2: ") << properties.at(U("Phone")).string_value() << std::endl;
}  
```

## <a name="retrieve-a-single-entity"></a>Obter uma única entidade
Pode escrever uma consulta tooretrieve uma entidade única e específica. Olá seguinte código utiliza **table_operation::retrieve_entity** cliente de Olá toospecify "Jorge Santos". Este método devolve apenas uma entidade em vez de uma coleção, não sendo hello valor devolvido em **table_result**. A especificação de chaves de partição e da fila numa consulta é Olá tooretrieve da forma mais rápida do serviço de tabela Olá, uma única entidade.  

```cpp
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for hello table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Retrieve hello entity with partition key of "Smith" and row key of "Jeff".
azure::storage::table_operation retrieve_operation = azure::storage::table_operation::retrieve_entity(U("Smith"), U("Jeff"));
azure::storage::table_result retrieve_result = table.execute(retrieve_operation);

// Output hello entity.
azure::storage::table_entity entity = retrieve_result.entity();
const azure::storage::table_entity::properties_type& properties = entity.properties();

std::wcout << U("PartitionKey: ") << entity.partition_key() << U(", RowKey: ") << entity.row_key()
    << U(", Property1: ") << properties.at(U("Email")).string_value()
    << U(", Property2: ") << properties.at(U("Phone")).string_value() << std::endl;
```

## <a name="replace-an-entity"></a>Substituir uma entidade
tooreplace uma entidade, obtê-lo a partir do serviço de tabela Olá, modificar o objecto entidade de Olá e, em seguida, guarde as alterações de Olá fazer uma cópia de serviço de tabela toohello. Olá código seguinte altera o endereço de e-mail e o número de telefone de um cliente existente. Em vez de chamar **table_operation::insert_entity**, este código utiliza **table_operation::replace_entity**. Isto faz com que Olá entidade toobe totalmente substituída no servidor de Olá, a menos que a entidade de Olá no servidor de Olá foi alterada desde que foi obtida, caso em que a operação de Olá irá falhar. Esta falha é tooprevent a aplicação inadvertidamente uma alteração efetuada entre Olá obtenção e atualização por outro componente da aplicação. Olá processamento adequado desta falha é tooretrieve Olá entidade novamente, efetuar as alterações (se ainda forem válidas) e, em seguida, executar outra **table_operation::replace_entity** operação. secção seguinte Olá irá mostrar como toooverride este comportamento.  

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for hello table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Replace an entity.
azure::storage::table_entity entity_to_replace(U("Smith"), U("Jeff"));
azure::storage::table_entity::properties_type& properties_to_replace = entity_to_replace.properties();
properties_to_replace.reserve(2);

// Specify a new phone number.
properties_to_replace[U("Phone")] = azure::storage::entity_property(U("425-555-0106"));

// Specify a new email address.
properties_to_replace[U("Email")] = azure::storage::entity_property(U("JeffS@contoso.com"));

// Create an operation tooreplace hello entity.
azure::storage::table_operation replace_operation = azure::storage::table_operation::replace_entity(entity_to_replace);

// Submit hello operation toohello Table service.
azure::storage::table_result replace_result = table.execute(replace_operation);
```

## <a name="insert-or-replace-an-entity"></a>Inserir ou substituir uma entidade
**table_operation::replace_entity** operações falharão se a entidade de Olá tiver sido alterada desde que foi obtida do servidor de Olá. Além disso, tem de obter Olá entidade do servidor de Olá primeiro por ordem para **table_operation::replace_entity** toobe com êxito. Por vezes, no entanto, não sabe se a entidade de Olá existe no servidor de Olá e Olá os valores atuais armazenados na mesma são irrelevantes — a atualização deve substituí todos eles. tooaccomplish, teria de utilizar um **table_operation::insert_or_replace_entity** operação. Esta operação insere a entidade de Olá se não existir ou substitui-lo se existir, independentemente de quando foi feita a última atualização da Olá. No seguinte exemplo de código de Olá, a entidade de cliente Olá para Jorge Santos ainda é obtida, mas é guardada, em seguida, servidor de back-toohello via **table_operation::insert_or_replace_entity**. As atualizações efetuadas toohello entidade entre a operação de obtenção e atualização Olá serão substituídas.  

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for hello table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Insert-or-replace an entity.
azure::storage::table_entity entity_to_insert_or_replace(U("Smith"), U("Jeff"));
azure::storage::table_entity::properties_type& properties_to_insert_or_replace = entity_to_insert_or_replace.properties();

properties_to_insert_or_replace.reserve(2);

// Specify a phone number.
properties_to_insert_or_replace[U("Phone")] = azure::storage::entity_property(U("425-555-0107"));

// Specify an email address.
properties_to_insert_or_replace[U("Email")] = azure::storage::entity_property(U("Jeffsm@contoso.com"));

// Create an operation tooinsert-or-replace hello entity.
azure::storage::table_operation insert_or_replace_operation = azure::storage::table_operation::insert_or_replace_entity(entity_to_insert_or_replace);

// Submit hello operation toohello Table service.
azure::storage::table_result insert_or_replace_result = table.execute(insert_or_replace_operation);
```

## <a name="query-a-subset-of-entity-properties"></a>Consultar um subconjunto de propriedades de entidade
Uma tabela de tooa de consulta pode obter apenas algumas propriedades de uma entidade. Olá consulta Olá seguinte código utiliza Olá **table_query::set_select_columns** método tooreturn apenas Olá endereços de e-mail de entidades na tabela de Olá.  

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for hello table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Define hello query, and select only hello Email property.
azure::storage::table_query query;
std::vector<utility::string_t> columns;

columns.push_back(U("Email"));
query.set_select_columns(columns);

// Execute hello query.
azure::storage::table_query_iterator it = table.execute_query(query);

// Display hello results.
azure::storage::table_query_iterator end_of_results;
for (; it != end_of_results; ++it)
{
    std::wcout << U("PartitionKey: ") << it->partition_key() << U(", RowKey: ") << it->row_key();

    const azure::storage::table_entity::properties_type& properties = it->properties();
    for (auto prop_it = properties.begin(); prop_it != properties.end(); ++prop_it)
    {
        std::wcout << ", " << prop_it->first << ": " << prop_it->second.str();
    }

    std::wcout << std::endl;
}
```

> [!NOTE]
> Consultar algumas propriedades de uma entidade é uma operação mais eficiente do que todas as propriedades a obter.
> 
> 

## <a name="delete-an-entity"></a>Eliminar uma entidade
Pode facilmente eliminar uma entidade depois de a ter obtido. Assim que a entidade de Olá é obtida, chamar **table_operation::delete_entity** com Olá toodelete de entidade. Em seguida, chame Olá **cloud_table.execute** método. Olá código seguinte obtém e elimina uma entidade com uma chave de partição de "Santos" e uma chave de linha de "Jorge".  

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for hello table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Create an operation tooretrieve hello entity with partition key of "Smith" and row key of "Jeff".
azure::storage::table_operation retrieve_operation = azure::storage::table_operation::retrieve_entity(U("Smith"), U("Jeff"));
azure::storage::table_result retrieve_result = table.execute(retrieve_operation);

// Create an operation toodelete hello entity.
azure::storage::table_operation delete_operation = azure::storage::table_operation::delete_entity(retrieve_result.entity());

// Submit hello delete operation toohello Table service.
azure::storage::table_result delete_result = table.execute(delete_operation);  
```

## <a name="delete-a-table"></a>Eliminar uma tabela
Por fim, Olá seguinte exemplo de código elimina uma tabela a partir de uma conta de armazenamento. Uma tabela que foi eliminada estará indisponível toobe recriada durante um período de tempo após a eliminação de Olá.  

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for hello table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Create an operation tooretrieve hello entity with partition key of "Smith" and row key of "Jeff".
azure::storage::table_operation retrieve_operation = azure::storage::table_operation::retrieve_entity(U("Smith"), U("Jeff"));
azure::storage::table_result retrieve_result = table.execute(retrieve_operation);

// Create an operation toodelete hello entity.
azure::storage::table_operation delete_operation = azure::storage::table_operation::delete_entity(retrieve_result.entity());

// Submit hello delete operation toohello Table service.
azure::storage::table_result delete_result = table.execute(delete_operation);
```

## <a name="next-steps"></a>Passos seguintes
Agora que aprendeu as noções básicas de Olá do table storage, siga estas toolearn ligações mais sobre o Storage do Azure:  

* [Explorador de armazenamento do Microsoft Azure](../vs-azure-tools-storage-manage-with-storage-explorer.md) é uma aplicação autónoma e gratuita da Microsoft permite-lhe toowork visualmente com dados de armazenamento do Azure no Windows, macOS e Linux.
* [Como toouse Blob storage do C++](storage-c-plus-plus-how-to-use-blobs.md)
* [Como toouse armazenamento de filas do C++](storage-c-plus-plus-how-to-use-queues.md)
* [Lista de recursos de armazenamento do Azure em C++](storage-c-plus-plus-enumeration.md)
* [Biblioteca de clientes do Storage para referência do C++](http://azure.github.io/azure-storage-cpp)
* [Documentação do Storage do Azure](https://azure.microsoft.com/documentation/services/storage/)
