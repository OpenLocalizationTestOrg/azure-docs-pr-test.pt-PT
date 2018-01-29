---
title: Como utilizar o Table storage do Azure com o Python | Microsoft Docs
description: "Armazene dados estruturados na nuvem através do Table Storage do Azure, um arquivo de dados NoSQL."
services: cosmos-db
documentationcenter: python
author: mimig1
manager: jhubbard
editor: tysonn
ms.assetid: 7ddb9f3e-4e6d-4103-96e6-f0351d69a17b
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 11/03/2017
ms.author: mimig
ms.openlocfilehash: a786f82d94a1a0039ed65a618670f872ffa3e3c2
ms.sourcegitcommit: f1c1789f2f2502d683afaf5a2f46cc548c0dea50
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 01/18/2018
---
# <a name="how-to-use-azure-table-storage-with-python"></a>Como utilizar o Table storage do Azure com o Python

[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

Este guia mostra como efetuar cenários comuns do armazenamento de tabelas do Azure no Python utilizando o [SDK de armazenamento do Microsoft Azure para Python](https://github.com/Azure/azure-storage-python). Os cenários abrangidos incluem criar e eliminar uma tabela e a inserção e consultar entidades.

Ao trabalhar com os cenários neste tutorial, pode ser útil designar o [SDK de armazenamento do Azure para referência da API de Python](https://azure-storage.readthedocs.io/en/latest/index.html).

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="install-the-azure-storage-sdk-for-python"></a>Instalar o armazenamento do Azure SDK para Python

Assim que tiver criado uma conta de armazenamento, o próximo passo é instalar o [SDK de armazenamento do Microsoft Azure para Python](https://github.com/Azure/azure-storage-python). Para obter detalhes sobre como instalar o SDK, consulte o [README.rst](https://github.com/Azure/azure-storage-python/blob/master/README.rst) ficheiro o SDK de armazenamento para o repositório de Python no GitHub.

## <a name="create-a-table"></a>Criar uma tabela

Para trabalhar com o serviço de Azure Table do Python, tem de importar o [TableService] [ py_TableService] módulo. Uma vez que irá funcionar com as entidades da tabela, também terá do [entidade] [ py_Entity] classe. Adicione este código perto da parte superior do ficheiro de Python para importar ambas:

```python
from azure.storage.table import TableService, Entity
```

Criar um [TableService] [ py_TableService] objeto, passando na sua chave de conta e o nome da conta de armazenamento. Substitua `myaccount` e `mykey` com o nome da conta e chave e chamada [create_table] [ py_create_table] para criar a tabela no armazenamento do Azure.

```python
table_service = TableService(account_name='myaccount', account_key='mykey')

table_service.create_table('tasktable')
```

## <a name="add-an-entity-to-a-table"></a>Adicionar uma entidade a uma tabela

Para adicionar uma entidade, tem primeiro de criar um objeto que representa a entidade, em seguida, passa o objeto para o [TableService][py_TableService].[ insert_entity] [ py_insert_entity] método. O objeto de entidade pode ser um dicionário ou um objeto do tipo [entidade][py_Entity]e define os valores e nomes de propriedade da entidade. Cada entidade tem de incluir necessários [PartitionKey e RowKey](#partitionkey-and-rowkey) propriedades, para além de quaisquer outras propriedades a definir para a entidade.

Este exemplo cria um objeto de dicionário que representa uma entidade, em seguida, transmite-as para o [insert_entity] [ py_insert_entity] método para adicioná-lo para a tabela:

```python
task = {'PartitionKey': 'tasksSeattle', 'RowKey': '001', 'description' : 'Take out the trash', 'priority' : 200}
table_service.insert_entity('tasktable', task)
```

Este exemplo cria um [entidade] [ py_Entity] objeto, em seguida, passa-o para o [insert_entity] [ py_insert_entity] método para adicioná-lo para a tabela:

```python
task = Entity()
task.PartitionKey = 'tasksSeattle'
task.RowKey = '002'
task.description = 'Wash the car'
task.priority = 100
table_service.insert_entity('tasktable', task)
```

### <a name="partitionkey-and-rowkey"></a>PartitionKey e RowKey

Tem de especificar um **PartitionKey** e um **RowKey** propriedade para cada entidade. Estes são os identificadores exclusivos da sua entidades, como em conjunto constituem a chave primária de uma entidade. Pode consultar ao utilizar estes valores muito mais rápidos do que pode consultar as propriedades de entidade porque estas propriedades só são indexadas.

As utilizações de serviço tabela **PartitionKey** inteligentemente distribuir as entidades da tabela em nós de armazenamento. Entidades que tenham o mesmo **PartitionKey** são armazenados no mesmo nó. **RowKey** é o ID exclusivo da entidade na partição pertence.

## <a name="update-an-entity"></a>Atualizar uma entidade

Para atualizar todos os valores de propriedade de uma entidade, chame o [update_entity] [ py_update_entity] método. Este exemplo mostra como substituir uma entidade existente com uma versão atualizada:

```python
task = {'PartitionKey': 'tasksSeattle', 'RowKey': '001', 'description' : 'Take out the garbage', 'priority' : 250}
table_service.update_entity('tasktable', task)
```

Se a entidade que está a ser atualizada já não existir, a operação de atualização irá falhar. Se pretende armazenar uma entidade se existe ou não, utilizar [insert_or_replace_entity][py_insert_or_replace_entity]. No exemplo seguinte, a primeira chamada substituirá a entidade existente. A segunda chamada inserir uma nova entidade, dado que nenhuma entidade com o PartitionKey especificado e RowKey não existe na tabela.

```python
# Replace the entity created earlier
task = {'PartitionKey': 'tasksSeattle', 'RowKey': '001', 'description' : 'Take out the garbage again', 'priority' : 250}
table_service.insert_or_replace_entity('tasktable', task)

# Insert a new entity
task = {'PartitionKey': 'tasksSeattle', 'RowKey': '003', 'description' : 'Buy detergent', 'priority' : 300}
table_service.insert_or_replace_entity('tasktable', task)
```

> [!TIP]
> O [update_entity] [ py_update_entity] método substitui todas as propriedades e valores de uma entidade existente, também pode utilizar para remover propriedades de uma entidade existente. Pode utilizar o [merge_entity] [ py_merge_entity] método para atualizar uma entidade existente com os valores de propriedade novas ou modificada sem completamente substituir a entidade.

## <a name="modify-multiple-entities"></a>Modificar várias entidades

Para garantir o processamento de um pedido atómico pelo serviço tabela, pode submeter várias operações em conjunto num batch. Em primeiro lugar, utilize o [TableBatch] [ py_TableBatch] classe para adicionar várias operações para um único lote. Em seguida, chame [TableService][py_TableService].[ commit_batch] [ py_commit_batch] para submeter as operações de uma operação atómica. Todas as entidades de ser modificados no batch tem de ser a mesma partição.

Este exemplo adiciona duas entidades em conjunto num batch:

```python
from azure.storage.table import TableBatch
batch = TableBatch()
task004 = {'PartitionKey': 'tasksSeattle', 'RowKey': '004', 'description' : 'Go grocery shopping', 'priority' : 400}
task005 = {'PartitionKey': 'tasksSeattle', 'RowKey': '005', 'description' : 'Clean the bathroom', 'priority' : 100}
batch.insert_entity(task004)
batch.insert_entity(task005)
table_service.commit_batch('tasktable', batch)
```

Lotes também podem ser utilizados com a sintaxe do Gestor de contexto:

```python
task006 = {'PartitionKey': 'tasksSeattle', 'RowKey': '006', 'description' : 'Go grocery shopping', 'priority' : 400}
task007 = {'PartitionKey': 'tasksSeattle', 'RowKey': '007', 'description' : 'Clean the bathroom', 'priority' : 100}

with table_service.batch('tasktable') as batch:
    batch.insert_entity(task006)
    batch.insert_entity(task007)
```

## <a name="query-for-an-entity"></a>Consulta de uma entidade

Para consultar uma entidade numa tabela, passar o respetivo PartitionKey e RowKey para o [TableService][py_TableService].[ get_entity] [ py_get_entity] método.

```python
task = table_service.get_entity('tasktable', 'tasksSeattle', '001')
print(task.description)
print(task.priority)
```

## <a name="query-a-set-of-entities"></a>Consulta de um conjunto de entidades

Pode consultar um conjunto de entidades, fornecendo uma cadeia de filtro com o **filtro** parâmetro. Neste exemplo localiza todas as tarefas em Seattle aplicando um filtro em PartitionKey:

```python
tasks = table_service.query_entities('tasktable', filter="PartitionKey eq 'tasksSeattle'")
for task in tasks:
    print(task.description)
    print(task.priority)
```

## <a name="query-a-subset-of-entity-properties"></a>Consultar um subconjunto de propriedades de entidade

Também pode restringir as propriedades que são devolvidas para cada entidade numa consulta. Esta técnica, denominada *projecção*, reduz a largura de banda e pode melhorar o desempenho de consulta, especialmente para entidades grandes ou conjuntos de resultados. Utilize o **selecione** parâmetro e pass, os nomes das propriedades que pretende devolvidos ao cliente.

A consulta no seguinte código devolve apenas as descrições de entidades na tabela.

> [!NOTE]
> O fragmento seguinte funciona apenas com o Storage do Azure. Não é suportada pelo emulador de armazenamento.

```python
tasks = table_service.query_entities('tasktable', filter="PartitionKey eq 'tasksSeattle'", select='description')
for task in tasks:
    print(task.description)
```

## <a name="delete-an-entity"></a>Eliminar uma entidade

Eliminar uma entidade transferindo o respetivo PartitionKey e RowKey para o [delete_entity] [ py_delete_entity] método.

```python
table_service.delete_entity('tasktable', 'tasksSeattle', '001')
```

## <a name="delete-a-table"></a>Eliminar uma tabela

Se já não necessita de uma tabela ou qualquer uma das entidades dentro da mesma, chame o [delete_table] [ py_delete_table] método para eliminar permanentemente a tabela do Storage do Azure.

```python
table_service.delete_table('tasktable')
```

## <a name="next-steps"></a>Passos Seguintes

* [SDK de armazenamento do Azure para referência da API de Python](https://azure-storage.readthedocs.io/en/latest/index.html)
* [Armazenamento do Azure SDK para Python](https://github.com/Azure/azure-storage-python)
* [Centro para Programadores do Python](https://azure.microsoft.com/develop/python/)
* [Explorador de armazenamento do Microsoft Azure](../vs-azure-tools-storage-manage-with-storage-explorer.md): uma aplicação gratuita de várias plataformas para trabalhar visualmente com dados de armazenamento do Azure no Windows, macOS e Linux.

[py_commit_batch]: https://azure-storage.readthedocs.io/en/latest/ref/azure.storage.table.tableservice.html#azure.storage.table.tableservice.TableService.commit_batch
[py_create_table]: https://azure-storage.readthedocs.io/en/latest/ref/azure.storage.table.tableservice.html#azure.storage.table.tableservice.TableService.create_table
[py_delete_entity]: https://azure-storage.readthedocs.io/en/latest/ref/azure.storage.table.tableservice.html#azure.storage.table.tableservice.TableService.delete_entity
[py_delete_table]: https://azure-storage.readthedocs.io/en/latest/ref/azure.storage.table.tableservice.html#azure.storage.table.tableservice.TableService.delete_table
[py_Entity]: https://azure-storage.readthedocs.io/en/latest/ref/azure.storage.table.models.html#azure.storage.table.models.Entity
[py_get_entity]: https://azure-storage.readthedocs.io/en/latest/ref/azure.storage.table.tableservice.html#azure.storage.table.tableservice.TableService.get_entity
[py_insert_entity]: https://azure-storage.readthedocs.io/en/latest/ref/azure.storage.table.tableservice.html#azure.storage.table.tableservice.TableService.insert_entity
[py_insert_or_replace_entity]: https://azure-storage.readthedocs.io/en/latest/ref/azure.storage.table.tableservice.html#azure.storage.table.tableservice.TableService.insert_or_replace_entity
[py_merge_entity]: https://azure-storage.readthedocs.io/en/latest/ref/azure.storage.table.tableservice.html#azure.storage.table.tableservice.TableService.merge_entity
[py_update_entity]: https://azure-storage.readthedocs.io/en/latest/ref/azure.storage.table.tableservice.html#azure.storage.table.tableservice.TableService.update_entity
[py_TableService]: https://azure-storage.readthedocs.io/en/latest/ref/azure.storage.table.tableservice.html
[py_TableBatch]: https://azure-storage.readthedocs.io/en/latest/ref/azure.storage.table.tablebatch.html#azure.storage.table.tablebatch.TableBatch