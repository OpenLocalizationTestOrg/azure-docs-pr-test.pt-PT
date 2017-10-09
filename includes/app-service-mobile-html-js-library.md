## <a name="create-client"></a>Criar uma ligação de cliente
Criar uma ligação de cliente através da criação de um objeto `WindowsAzure.MobileServiceClient`.  Substitua `appUrl` com o tooyour URL de aplicação móvel.

```
var client = WindowsAzure.MobileServiceClient(appUrl);
```

## <a name="table-reference"></a>Trabalhar com tabelas
tooaccess ou atualização de dados, criar uma tabela de back-end de toohello de referência. Substitua `tableName` com o nome de Olá da sua tabela

```
var table = client.getTable(tableName);
```

Assim que tiver uma referência da tabela, pode trabalhar mais com a mesma:

* [Consultar uma Tabela](#querying)
  * [Filtrar Dados](#table-filter)
  * [Paginar através de Dados](#table-paging)
  * [Ordenar Dados](#sorting-data)
* [Inserir Dados](#inserting)
* [Modificar dados](#modifying)
* [Eliminar Dados](#deleting)

### <a name="querying"></a>Como: consultar uma referência de tabela
Depois de ter uma referência de tabela, pode utilizar este tooquery dados no servidor de Olá.  As consultas são efetuadas num idioma "tipo LINQ".
código do tooreturn todos os dados da tabela de Olá, Olá utilize os seguintes:

```
/**
 * Process hello results that are received by a call tootable.read()
 *
 * @param {Object} results hello results as a pseudo-array
 * @param {int} results.length hello length of hello results array
 * @param {Object} results[] hello individual results
 */
function success(results) {
   var numItemsRead = results.length;

   for (var i = 0 ; i < results.length ; i++) {
       var row = results[i];
       // Each row is an object - hello properties are hello columns
   }
}

function failure(error) {
    throw new Error('Error loading data: ', error);
}

table
    .read()
    .then(success, failure);
```

a função de êxito Olá denomina-se com os resultados de Olá.  Não utilize `for (var i in results)` no êxito Olá funcionar como que será iterar informações que estão incluídas nos resultados de Olá quando outras funções de consulta (tais como `.includeTotalCount()`) são utilizados.

Para obter mais informações sobre Olá sintaxe de consulta, consulte Olá [consultar a documentação do objeto].

#### <a name="table-filter"></a>Filtragem de dados no servidor de Olá
Pode utilizar um `where` cláusula na referência de tabela Olá:

```
table
    .where({ userId: user.userId, complete: false })
    .read()
    .then(success, failure);
```

Também pode utilizar uma função que filtra o objeto de Olá.  Neste caso, Olá `this` variável atribuída toothe o objeto atual a ser filtrado.  Olá seguinte código é funcionalmente equivalente toohello exemplo anterior:

```
function filterByUserId(currentUserId) {
    return this.userId === currentUserId && this.complete === false;
}

table
    .where(filterByUserId, user.userId)
    .read()
    .then(success, failure);
```

#### <a name="table-paging"></a>Paginar através de dados
Utilizar Olá `take()` e `skip()` métodos.  Por exemplo, se desejar tabela de Olá toosplit numa linha de 100 registos:

```
var totalCount = 0, pages = 0;

// Step 1 - get hello total number of records
table.includeTotalCount().take(0).read(function (results) {
    totalCount = results.totalCount;
    pages = Math.floor(totalCount/100) + 1;
    loadPage(0);
}, failure);

function loadPage(pageNum) {
    let skip = pageNum * 100;
    table.skip(skip).take(100).read(function (results) {
        for (var i = 0 ; i < results.length ; i++) {
            var row = results[i];
            // Process each row
        }
    }
}
```

Olá `.includeTotalCount()` método é utilizado tooadd um objeto de resultados do totalCount campo toohello.  O campo de totalCount é preenchido com o número total de Olá de registos que teria de ser devolvido se a paginação não é utilizada.

Em seguida, pode utilizar a variável de páginas de Olá e algumas tooprovide de botões de IU uma lista de página; utilizar `loadPage()` carregar novos registos de Olá para cada página.  Implementar a colocação em cache toospeed acesso toorecords que já foram carregadas.

#### <a name="sorting-data"></a>Como: devolver dados ordenados
Olá utilize `.orderBy()` ou `.orderByDescending()` consultar métodos:

```
table
    .orderBy('name')
    .read()
    .then(success, failure);
```

Para obter mais informações sobre o objeto da consulta Olá, consulte Olá [consultar a documentação do objeto].

### <a name="inserting"></a>Como: inserir dados
Criar um objeto de JavaScript com data adequada Olá e chamada `table.insert()` no modo assíncrono:

```javascript
var newItem = {
    name: 'My Name',
    signupDate: new Date()
};

table
    .insert(newItem)
    .done(function (insertedItem) {
        var id = insertedItem.id;
    }, failure);
```

No inserção com êxito, item Olá inserido é devolvido com os campos adicionais Olá que são necessários para operações de sincronização.  Atualize a sua própria cache com estas informações para atualizações posteriores.

Olá, Azure Mobile Apps Node.js servidor SDK suporta esquema dinâmica para fins de desenvolvimento.  Esquema dinâmica permite-lhe tabela do tooadd colunas toohello especificando-los numa operação insert ou update.  Recomendamos que desative dinâmica esquema antes de mover o tooproduction de aplicação.

### <a name="modifying"></a>Como: modificar dados
Toohello semelhante `.insert()` método, deve criar um objeto de atualização e, em seguida, chame `.update()`.  Olá objetos de atualização tem de conter ID Olá toobe registos Olá atualizada - Olá ID é obtido ao ler o registo de Olá ou ao chamar `.insert()`.

```javascript
var updateItem = {
    id: '7163bc7a-70b2-4dde-98e9-8818969611bd',
    name: 'My New Name'
};

table
    .update(updateItem)
    .done(function (updatedItem) {
        // You can now update your cached copy
    }, failure);
```

### <a name="deleting"></a>Como: eliminar dados
toodelete um registo, chamada Olá `.del()` método.  Transmita o ID de Olá uma referência de objeto:

```
table
    .del({ id: '7163bc7a-70b2-4dde-98e9-8818969611bd' })
    .done(function () {
        // Record is now deleted - update your cache
    }, failure);
```
