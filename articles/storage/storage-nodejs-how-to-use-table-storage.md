---
title: aaaHow toouse Table storage do Azure do Node.js | Microsoft Docs
description: "Armazene dados estruturados na nuvem de Olá utilizando o Table storage do Azure, um arquivo de dados NoSQL."
services: storage
documentationcenter: nodejs
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: fc2e33d2-c5da-4861-8503-53fdc25750de
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 12/08/2016
ms.author: marsma
ms.openlocfilehash: 990a71337b806d759d0277a7691712346db7b355
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-table-storage-from-nodejs"></a>Como toouse Table storage do Azure do Node.js
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

## <a name="overview"></a>Descrição geral
Este tópico mostra como tooperform cenários comuns utilizando Olá tabelas do Azure service numa aplicação Node.js.

Exemplos de código Olá neste tópico partem do princípio de que já tem uma aplicação Node.js. Para obter informações sobre como toocreate uma aplicação Node.js no Azure, consulte qualquer um dos seguintes tópicos:

* [Criar uma aplicação web Node.js no App Service do Azure](../app-service-web/app-service-web-get-started-nodejs.md)
* [Criar e implementar uma aplicação de web Node.js tooAzure com o WebMatrix](../app-service-web/web-sites-nodejs-use-webmatrix.md)
* [Criar e implementar uma tooan de aplicação Node.js o serviço em nuvem do Azure](../cloud-services/cloud-services-nodejs-develop-deploy-app.md) (através do Windows PowerShell)

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="configure-your-application-tooaccess-azure-storage"></a>Configurar a sua aplicação tooaccess Storage do Azure
toouse Storage do Azure, terá de Olá SDK de armazenamento do Azure para Node.js, que inclui um conjunto de bibliotecas de conveniência que comunicam com os serviços de REST de armazenamento Olá.

### <a name="use-node-package-manager-npm-tooinstall-hello-package"></a>Utilizar o Gestor de pacote de nó (NPM) tooinstall Olá pacote
1. Utilize uma interface de linha de comandos, como **PowerShell** (Windows), **Terminal** (Mac), ou **Bash** (Unix) e navegue pasta toohello onde criou a aplicação.
2. Tipo **npm instalar storage do azure** na janela de comandos Olá. O resultado do comando de Olá é semelhante toohello seguinte o exemplo.

       azure-storage@0.5.0 node_modules\azure-storage
       +-- extend@1.2.1
       +-- xmlbuilder@0.4.3
       +-- mime@1.2.11
       +-- node-uuid@1.4.3
       +-- validator@3.22.2
       +-- underscore@1.4.4
       +-- readable-stream@1.0.33 (string_decoder@0.10.31, isarray@0.0.1, inherits@2.0.1, core-util-is@1.0.1)
       +-- xml2js@0.2.7 (sax@0.5.2)
       +-- request@2.57.0 (caseless@0.10.0, aws-sign2@0.5.0, forever-agent@0.6.1, stringstream@0.0.4, oauth-sign@0.8.0, tunnel-agent@0.4.1, isstream@0.1.2, json-stringify-safe@5.0.1, bl@0.9.4, combined-stream@1.0.5, qs@3.1.0, mime-types@2.0.14, form-data@0.2.0, http-signature@0.11.0, tough-cookie@2.0.0, hawk@2.3.1, har-validator@1.8.0)
3. Pode executar manualmente Olá **ls** tooverify de comando que um **nó\_módulos** pasta foi criada. Dentro dessa pasta encontrará Olá **storage do azure** pacote, que contém as bibliotecas de Olá necessita de armazenamento tooaccess.

### <a name="import-hello-package"></a>Importar o pacote de Olá
Adicionar Olá seguinte código toohello parte superior Olá **server.js** ficheiros na sua aplicação:

```nodejs
var azure = require('azure-storage');
```

## <a name="set-up-an-azure-storage-connection"></a>Configurar uma ligação de armazenamento do Azure
módulo Olá do azure será lida a variáveis de ambiente de Olá AZURE\_armazenamento\_conta e o AZURE\_armazenamento\_acesso\_chave ou o AZURE\_armazenamento\_ligação \_Cadeia de informações necessárias tooconnect tooyour conta do storage do Azure. Se estas variáveis de ambiente não estiver definidas, tem de especificar as informações da conta Olá ao chamar **TableService**.

Para obter um exemplo de definir variáveis de ambiente de Olá na Olá [portal do Azure](https://portal.azure.com) para um Web site do Azure, consulte [através da aplicação de web de Node.js Olá o serviço de tabela do Azure](../app-service-web/storage-nodejs-use-table-storage-web-site.md).

## <a name="create-a-table"></a>Criar uma tabela
Olá código seguinte cria um **TableService** objeto e utiliza-toocreate uma nova tabela. Adicione Olá seguinte perto da parte superior Olá **server.js**.

```nodejs
var tableSvc = azure.createTableService();
```

Olá chamada demasiado**createTableIfNotExists** criará uma nova tabela com o nome especificado Olá se já existir. Olá exemplo seguinte cria uma nova tabela com o nome 'mytable' se já existir:

```nodejs
tableSvc.createTableIfNotExists('mytable', function(error, result, response){
  if(!error){
    // Table exists or created
  }
});
```

Olá `result.created` será `true` se for criada uma nova tabela, e `false` se Olá tabela já existe. Olá `response` contêm informações sobre o pedido de Olá.

### <a name="filters"></a>Filtros
As operações de filtragem opcionais podem ser aplicados toooperations efetuada utilizando **TableService**. Operações de filtragem pode incluir registo automaticamente repetir, etc. Os filtros são objetos que implementam um método com assinatura de Olá:

```nodejs
function handle (requestOptions, next)
```

Depois de efetuar a respetiva pré-processamentos nas opções de pedido de Olá, Olá método necessita toocall "seguinte", transmitir uma chamada de retorno com Olá assinatura os seguintes:

```nodejs
function (returnObject, finalCallback, next)
```

Esta chamada de retorno e após o processamento Olá returnObject (resposta de hello do servidor de toohello Olá pedido), a chamada de retorno de Olá tem tooeither invocar em seguida, se existir toocontinue outros filtros de processamento ou simplesmente invocar finalCallback; caso contrário, tooend Olá invocação de serviço.

Dois filtros que implementa lógica de repetição são incluídos com Olá Azure SDK para Node.js, **ExponentialRetryPolicyFilter** e **LinearRetryPolicyFilter**. seguinte Olá cria um **TableService** objeto que utiliza Olá **ExponentialRetryPolicyFilter**:

```nodejs
var retryOperations = new azure.ExponentialRetryPolicyFilter();
var tableSvc = azure.createTableService().withFilter(retryOperations);
```

## <a name="add-an-entity-tooa-table"></a>Adicionar uma tabela de tooa entidade
tooadd uma entidade, primeiro crie um objeto que define as propriedades de entidade. Todas as entidades tem de conter um **PartitionKey** e **RowKey**, que são identificadores exclusivos para a entidade de Olá.

* **PartitionKey** -determina partição Olá entidade Olá armazenados no
* **RowKey** - exclusivamente identifica entidade Olá dentro de partição Olá

Ambos **PartitionKey** e **RowKey** tem de ser valores de cadeia. Para obter mais informações, consulte [Olá compreender o modelo de dados do serviço tabela](http://msdn.microsoft.com/library/azure/dd179338.aspx).

Olá segue-se um exemplo de definir uma entidade. Tenha em atenção que **dueDate** está definido como um tipo de **Edm.DateTime**. Tipo de Olá especificação é opcional e tipos irão ser inferidos se não for especificados.

```nodejs
var task = {
  PartitionKey: {'_':'hometasks'},
  RowKey: {'_': '1'},
  description: {'_':'take out hello trash'},
  dueDate: {'_':new Date(2015, 6, 20), '$':'Edm.DateTime'}
};
```

> [!NOTE]
> Há também um **Timestamp** campo para cada registo, o que é definido pelo Azure quando uma entidade é inserida ou atualizada.
>
>

Também pode utilizar Olá **entityGenerator** toocreate entidades. Olá exemplo seguinte cria Olá mesma entidade de tarefas utilizando Olá **entityGenerator**.

```nodejs
var entGen = azure.TableUtilities.entityGenerator;
var task = {
  PartitionKey: entGen.String('hometasks'),
  RowKey: entGen.String('1'),
  description: entGen.String('take out hello trash'),
  dueDate: entGen.DateTime(new Date(Date.UTC(2015, 6, 20))),
};
```

tooadd uma tabela de tooyour de entidade, transmitir toohello de objeto de entidade Olá **insertEntity** método.

```nodejs
tableSvc.insertEntity('mytable',task, function (error, result, response) {
  if(!error){
    // Entity inserted
  }
});
```

Se a operação de Olá for bem-sucedida, `result` irá conter Olá [ETag](http://en.wikipedia.org/wiki/HTTP_ETag) de Olá inserir o registo e `response` contêm informações sobre a operação de Olá.

Exemplo de resposta:

```nodejs
{ '.metadata': { etag: 'W/"datetime\'2015-02-25T01%3A22%3A22.5Z\'"' } }
```

> [!NOTE]
> Por predefinição, **insertEntity** não devolve entidades Olá inserido como parte da Olá `response` informações. Se planear efetuar outras operações nesta entidade ou informações de Olá toocache assim o desejar, pode ser útil toohave devolvido como parte da Olá `result`. Pode fazê-lo ao ativar **echoContent** da seguinte forma:
>
> `tableSvc.insertEntity('mytable', task, {echoContent: true}, function (error, result, response) {...}`
>
>

## <a name="update-an-entity"></a>Atualizar uma entidade
Existem vários métodos tooupdate de disponível uma entidade existente:

* **replaceEntity** -atualizações de uma entidade existente, substituindo-la
* **mergeEntity** -atualiza uma entidade existente, a intercalação novos valores de propriedade na entidade existente Olá
* **insertOrReplaceEntity** -atualizações de uma entidade existente, substituindo-lo. Se nenhuma entidade de existir, será inserido um novo
* **insertOrMergeEntity** -atualiza uma entidade existente, a intercalação novos valores de propriedade para Olá existente. Se nenhuma entidade de existir, será inserido um novo

Olá exemplo seguinte demonstra a atualizar uma entidade utilizando **replaceEntity**:

```nodejs
tableSvc.replaceEntity('mytable', updatedTask, function(error, result, response){
  if(!error) {
    // Entity updated
  }
});
```

> [!NOTE]
> Por predefinição, ao atualizar uma entidade não verifica toosee se dados Olá a ser atualizados anteriormente foi modificados por outro processo. atualizações em simultâneo toosupport:
>
> 1. Obter Olá ETag do objeto de Olá a ser atualizado. Este é devolvido como parte da Olá `response` em nenhuma operação relacionada com entidade e podem ser recuperadas por meio `response['.metadata'].etag`.
> 2. Quando efetuar uma operação de atualização numa entidade, adicionar Olá ETag obter as informações anteriormente toohello nova entidade. Por exemplo:
>
>       entity2 .etag ['.metadata'] = currentEtag;
> 3. Efetue a operação de atualização de Olá. Se a entidade de Olá foi modificada desde que obtida valor ETag de Olá, tais como outra instância da sua aplicação, um `error` vai ser devolvido a indicar que a condição de atualização de Olá especificada num pedido de Olá não foi cumprida.
>
>

Com **replaceEntity** e **mergeEntity**, se não existir entidade Olá que está a ser atualizada, em seguida, a operação de atualização de Olá irá falhar. Por conseguinte, se desejar toostore uma entidade, independentemente de já existir, utilize **insertOrReplaceEntity** ou **insertOrMergeEntity**.

Olá `result` para atualização bem sucedida operações irão conter Olá **Etag** de Olá atualizado entidade.

## <a name="work-with-groups-of-entities"></a>Trabalhar com grupos de entidades
Por vezes, faz sentido toosubmit várias operações em conjunto no tooensure batch atomic processados pelo servidor Olá. tooaccomplish que, utilize Olá **TableBatch** toocreate um lote de classe e, em seguida, utilize Olá **executeBatch** método **TableService** tooperform Olá em lotes operações.

 Olá seguinte exemplo mostra como submeter duas entidades no batch:

```nodejs
var task1 = {
  PartitionKey: {'_':'hometasks'},
  RowKey: {'_': '1'},
  description: {'_':'Take out hello trash'},
  dueDate: {'_':new Date(2015, 6, 20)}
};
var task2 = {
  PartitionKey: {'_':'hometasks'},
  RowKey: {'_': '2'},
  description: {'_':'Wash hello dishes'},
  dueDate: {'_':new Date(2015, 6, 20)}
};

var batch = new azure.TableBatch();

batch.insertEntity(task1, {echoContent: true});
batch.insertEntity(task2, {echoContent: true});

tableSvc.executeBatch('mytable', batch, function (error, result, response) {
  if(!error) {
    // Batch completed
  }
});
```

Para operações de lote com êxito, `result` irá conter informações para cada operação no lote de Olá.

### <a name="work-with-batched-operations"></a>Trabalhar com operações em lote
Operações adicionado tooa batch pode ser inspecionado visualizando Olá `operations` propriedade. Também pode utilizar Olá toowork de métodos com operações os seguintes:

* **Limpar** -limpa todas as operações do batch
* **getOperations** -obtém uma operação do batch Olá
* **hasOperations** -devolve true se o batch Olá contém operações
* **removeOperations** -remove uma operação
* **tamanho** -devolve Olá número de operações em lote de Olá

## <a name="retrieve-an-entity-by-key"></a>Obter uma entidade pela chave
tooreturn uma entidade específica com base no Olá **PartitionKey** e **RowKey**, utilize Olá **retrieveEntity** método.

```nodejs
tableSvc.retrieveEntity('mytable', 'hometasks', '1', function(error, result, response){
  if(!error){
    // result contains hello entity
  }
});
```

Assim que esta operação for concluída, `result` irá conter a entidade de Olá.

## <a name="query-a-set-of-entities"></a>Consulta de um conjunto de entidades
tooquery uma tabela, utilize Olá **TableQuery** objeto toobuild se uma expressão de consulta utilizando Olá cláusulas os seguintes:

* **Selecione** -Olá campos toobe devolvidas da consulta de Olá
* **onde** - hello onde cláusula

  * **e** - um `and` onde condição
  * **ou** - um `or` onde condição
* **parte superior** -Olá número de itens toofetch

Olá exemplo seguinte cria uma consulta que irá devolver Olá superiores cinco itens com uma PartitionKey 'hometasks'.

```nodejs
var query = new azure.TableQuery()
  .top(5)
  .where('PartitionKey eq ?', 'hometasks');
```

Uma vez que **selecione** não for utilizado, serão devolvidos todos os campos. consulta de Olá tooperform contra uma tabela, utilize **queryEntities**. Olá exemplo seguinte utiliza este entidades tooreturn de consulta de 'mytable'.

```nodejs
tableSvc.queryEntities('mytable',query, null, function(error, result, response) {
  if(!error) {
    // query was successful
  }
});
```

Se tiver êxito, `result.entries` irá conter uma matriz de entidades que correspondem à consulta de Olá. Se a consulta de Olá foi tooreturn não é possível todas as entidades, `result.continuationToken` será não -*nulo* e pode ser utilizado como Olá terceiro parâmetro de **queryEntities** tooretrieve mais resultados. Para consulta inicial Olá, utilize *nulo* para o terceiro parâmetro de Olá.

### <a name="query-a-subset-of-entity-properties"></a>Consultar um subconjunto de propriedades de entidade
Uma tabela de tooa de consulta pode obter alguns campos de uma entidade.
Isto reduz a largura de banda e pode melhorar o desempenho de consulta, especialmente para entidades grandes. Olá utilize **selecione** cláusula e passar nomes Olá de Olá campos toobe devolvido. Por exemplo, hello seguinte consulta devolverá apenas Olá **Descrição** e **dueDate** campos.

```nodejs
var query = new azure.TableQuery()
  .select(['description', 'dueDate'])
  .top(5)
  .where('PartitionKey eq ?', 'hometasks');
```

## <a name="delete-an-entity"></a>Eliminar uma entidade
Pode eliminar uma entidade com as chaves de partição e linha. Neste exemplo, Olá **task1** objeto contém Olá **RowKey** e **PartitionKey** valores de Olá toobe de entidade eliminada. Em seguida, é transmitido um objeto de Olá toohello **deleteEntity** método.

```nodejs
var task = {
  PartitionKey: {'_':'hometasks'},
  RowKey: {'_': '1'}
};

tableSvc.deleteEntity('mytable', task, function(error, response){
  if(!error) {
    // Entity deleted
  }
});
```

> [!NOTE]
> Considere utilizar ETags quando a eliminação de itens, tooensure Olá item não foi modificada por outro processo. Consulte [atualizar uma entidade](#update-an-entity) para obter informações sobre como utilizar ETags.
>
>

## <a name="delete-a-table"></a>Eliminar uma tabela
Olá seguinte código elimina uma tabela a partir de uma conta de armazenamento.

```nodejs
tableSvc.deleteTable('mytable', function(error, response){
    if(!error){
        // Table deleted
    }
});
```

Se não tiver a certeza se existe a tabela de Olá, utilize **deleteTableIfExists**.

## <a name="use-continuation-tokens"></a>Utilize tokens de continuação
Quando estiver a consultar tabelas para grandes quantidades de resultados, procure os tokens de continuação. Poderão estar disponíveis para a consulta que poderá Note que o se não criar toorecognize quando existe um token de continuação grandes quantidades de dados.

resultados de Olá objeto devolvido durante a consulta de conjuntos de entidades um `continuationToken` propriedade quando tal um token está presente. Em seguida, pode utilizar este quando efetuar uma toomove toocontinue de consulta em entidades de partição e a tabela de Olá.

Ao consultar, poderá ser fornecido um parâmetro de continuationToken entre a instância de objeto da consulta de Olá e função de chamada de retorno de Olá:

```nodejs
var nextContinuationToken = null;
dc.table.queryEntities(tableName,
    query,
    nextContinuationToken,
    function (error, results) {
        if (error) throw error;

        // iterate through results.entries with results

        if (results.continuationToken) {
            nextContinuationToken = results.continuationToken;
        }

    });
```

Se inspecionar Olá `continuationToken` objeto, encontrará propriedades, tais como `nextPartitionKey`, `nextRowKey` e `targetLocation`, que pode ser utilizado tooiterate através de todos os resultados de Olá.

Também é um exemplo de continuação no repositório de Node.js de armazenamento do Azure Olá no GitHub. Procure `examples/samples/continuationsample.js`.

## <a name="work-with-shared-access-signatures"></a>Trabalhar com assinaturas de acesso partilhado
Assinaturas de acesso partilhado (SAS) são uma tootables de acesso granulares tooprovide de forma segura sem fornecer o nome da conta de armazenamento ou chaves. SAS são frequentemente utilizados tooprovide limitada para aceder a dados tooyour, tais como permitir que uma aplicação móvel tooquery registos.

Uma aplicação como um serviço baseado na nuvem fidedigna gera uma SAS utilizando Olá **generateSharedAccessSignature** de Olá **TableService**e fornece-tooan fidedigna ou fidedigna por aplicação Por exemplo, uma aplicação móvel. Olá SAS é gerado utilizando uma política, que descreve o início de Olá e datas final durante o qual Olá SAS é válido, bem como Olá marcador de posição SAS de toohello concedida ao nível de acesso.

Olá exemplo seguinte gera uma nova política de acesso partilhado, o que permitirá Olá tabela Olá do SAS marcador de posição tooquery ('r') e expira 100 minutos após a hora de Olá que é criado.

```nodejs
var startDate = new Date();
var expiryDate = new Date(startDate);
expiryDate.setMinutes(startDate.getMinutes() + 100);
startDate.setMinutes(startDate.getMinutes() - 100);

var sharedAccessPolicy = {
  AccessPolicy: {
    Permissions: azure.TableUtilities.SharedAccessPermissions.QUERY,
    Start: startDate,
    Expiry: expiryDate
  },
};

var tableSAS = tableSvc.generateSharedAccessSignature('mytable', sharedAccessPolicy);
var host = tableSvc.host;
```

Tenha em atenção que as informações do anfitrião Olá têm de ser fornecidos também, conforme necessário, quando o marcador de posição do Olá SAS tenta tabela de Olá tooaccess.

Olá aplicação cliente, em seguida, utiliza Olá SAS com **TableServiceWithSAS** tooperform operações relativamente à tabela de Olá. seguinte o exemplo de Olá liga toohello tabela e executa uma consulta.

```nodejs
var sharedTableService = azure.createTableServiceWithSas(host, tableSAS);
var query = azure.TableQuery()
  .where('PartitionKey eq ?', 'hometasks');

sharedTableService.queryEntities(query, null, function(error, result, response) {
  if(!error) {
    // result contains hello entities
  }
});
```

Uma vez que hello SAS foi gerado com acesso de consulta apenas, se foi efetuada uma tentativa tooinsert, atualizar ou eliminar entidades, será devolvido um erro.

### <a name="access-control-lists"></a>Listas de controlo de acesso
Também pode utilizar uma política de acesso de Olá de tooset de lista de controlo de acesso (ACL) para um SAS. Isto é útil se desejar tooallow tabela do Olá vários tooaccess de clientes, mas fornecem as políticas de acesso diferentes para cada cliente.

Uma ACL é implementada com uma matriz de políticas de acesso, com um ID associado a cada política. Olá seguinte o exemplo define duas políticas, uma para 'user1' e outra para 'Utilizador2':

```nodejs
var sharedAccessPolicy = {
  user1: {
    Permissions: azure.TableUtilities.SharedAccessPermissions.QUERY,
    Start: startDate,
    Expiry: expiryDate
  },
  user2: {
    Permissions: azure.TableUtilities.SharedAccessPermissions.ADD,
    Start: startDate,
    Expiry: expiryDate
  }
};
```

Olá seguinte obtém do exemplo Olá ACL atual para Olá **hometasks** tabela e, em seguida, adiciona novas políticas de Olá utilizando **setTableAcl**. Esta abordagem permite:

```nodejs
var extend = require('extend');
tableSvc.getTableAcl('hometasks', function(error, result, response) {
if(!error){
    var newSignedIdentifiers = extend(true, result.signedIdentifiers, sharedAccessPolicy);
    tableSvc.setTableAcl('hometasks', newSignedIdentifiers, function(error, result, response){
      if(!error){
        // ACL set
      }
    });
  }
});
```

Uma vez Olá que ACL foi definida, pode, em seguida, crie um SAS com base no ID de Olá para uma política. Olá seguinte exemplo cria um novo SAS para 'Utilizador2':

```nodejs
tableSAS = tableSvc.generateSharedAccessSignature('hometasks', { Id: 'user2' });
```

## <a name="next-steps"></a>Passos seguintes
Para obter mais informações, consulte Olá os seguintes recursos.

* [Explorador de armazenamento do Microsoft Azure](../vs-azure-tools-storage-manage-with-storage-explorer.md) é uma aplicação autónoma e gratuita da Microsoft permite-lhe toowork visualmente com dados de armazenamento do Azure no Windows, macOS e Linux.
* [SDK de armazenamento do Azure para o nó](https://github.com/Azure/azure-storage-node) repositório no GitHub.
* [Centro para Programadores do Node.js](/develop/nodejs/)
* [Criar e implementar uma tooan de aplicação Node.js Web site do Azure](../app-service-web/app-service-web-get-started-nodejs.md)
