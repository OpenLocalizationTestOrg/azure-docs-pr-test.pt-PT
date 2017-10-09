## <span data-ttu-id="f0b95-101"><a name="create-client"></a>Criar uma ligação de cliente</span><span class="sxs-lookup"><span data-stu-id="f0b95-101"><a name="create-client"></a>Create a client connection</span></span>
<span data-ttu-id="f0b95-102">Criar uma ligação de cliente através da criação de um objeto `WindowsAzure.MobileServiceClient`.</span><span class="sxs-lookup"><span data-stu-id="f0b95-102">Create a client connection by creating a `WindowsAzure.MobileServiceClient` object.</span></span>  <span data-ttu-id="f0b95-103">Substitua `appUrl` com o tooyour URL de aplicação móvel.</span><span class="sxs-lookup"><span data-stu-id="f0b95-103">Replace `appUrl` with the URL tooyour Mobile App.</span></span>

```
var client = WindowsAzure.MobileServiceClient(appUrl);
```

## <span data-ttu-id="f0b95-104"><a name="table-reference"></a>Trabalhar com tabelas</span><span class="sxs-lookup"><span data-stu-id="f0b95-104"><a name="table-reference"></a>Work with tables</span></span>
<span data-ttu-id="f0b95-105">tooaccess ou atualização de dados, criar uma tabela de back-end de toohello de referência.</span><span class="sxs-lookup"><span data-stu-id="f0b95-105">tooaccess or update data, create a reference toohello backend table.</span></span> <span data-ttu-id="f0b95-106">Substitua `tableName` com o nome de Olá da sua tabela</span><span class="sxs-lookup"><span data-stu-id="f0b95-106">Replace `tableName` with hello name of your table</span></span>

```
var table = client.getTable(tableName);
```

<span data-ttu-id="f0b95-107">Assim que tiver uma referência da tabela, pode trabalhar mais com a mesma:</span><span class="sxs-lookup"><span data-stu-id="f0b95-107">Once you have a table reference, you can work further with your table:</span></span>

* [<span data-ttu-id="f0b95-108">Consultar uma Tabela</span><span class="sxs-lookup"><span data-stu-id="f0b95-108">Query a Table</span></span>](#querying)
  * [<span data-ttu-id="f0b95-109">Filtrar Dados</span><span class="sxs-lookup"><span data-stu-id="f0b95-109">Filtering Data</span></span>](#table-filter)
  * [<span data-ttu-id="f0b95-110">Paginar através de Dados</span><span class="sxs-lookup"><span data-stu-id="f0b95-110">Paging through Data</span></span>](#table-paging)
  * [<span data-ttu-id="f0b95-111">Ordenar Dados</span><span class="sxs-lookup"><span data-stu-id="f0b95-111">Sorting Data</span></span>](#sorting-data)
* [<span data-ttu-id="f0b95-112">Inserir Dados</span><span class="sxs-lookup"><span data-stu-id="f0b95-112">Inserting Data</span></span>](#inserting)
* [<span data-ttu-id="f0b95-113">Modificar dados</span><span class="sxs-lookup"><span data-stu-id="f0b95-113">Modifying Data</span></span>](#modifying)
* [<span data-ttu-id="f0b95-114">Eliminar Dados</span><span class="sxs-lookup"><span data-stu-id="f0b95-114">Deleting Data</span></span>](#deleting)

### <span data-ttu-id="f0b95-115"><a name="querying"></a>Como: consultar uma referência de tabela</span><span class="sxs-lookup"><span data-stu-id="f0b95-115"><a name="querying"></a>How to: Query a table reference</span></span>
<span data-ttu-id="f0b95-116">Depois de ter uma referência de tabela, pode utilizar este tooquery dados no servidor de Olá.</span><span class="sxs-lookup"><span data-stu-id="f0b95-116">Once you have a table reference, you can use it tooquery for data on hello server.</span></span>  <span data-ttu-id="f0b95-117">As consultas são efetuadas num idioma "tipo LINQ".</span><span class="sxs-lookup"><span data-stu-id="f0b95-117">Queries are made in a "LINQ-like" language.</span></span>
<span data-ttu-id="f0b95-118">código do tooreturn todos os dados da tabela de Olá, Olá utilize os seguintes:</span><span class="sxs-lookup"><span data-stu-id="f0b95-118">tooreturn all data from hello table, use hello following code:</span></span>

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

<span data-ttu-id="f0b95-119">a função de êxito Olá denomina-se com os resultados de Olá.</span><span class="sxs-lookup"><span data-stu-id="f0b95-119">hello success function is called with hello results.</span></span>  <span data-ttu-id="f0b95-120">Não utilize `for (var i in results)` no êxito Olá funcionar como que será iterar informações que estão incluídas nos resultados de Olá quando outras funções de consulta (tais como `.includeTotalCount()`) são utilizados.</span><span class="sxs-lookup"><span data-stu-id="f0b95-120">Do not use `for (var i in results)` in hello success function as that will iterate over information that is included in hello results when other query functions (such as `.includeTotalCount()`) are used.</span></span>

<span data-ttu-id="f0b95-121">Para obter mais informações sobre Olá sintaxe de consulta, consulte Olá [consultar a documentação do objeto].</span><span class="sxs-lookup"><span data-stu-id="f0b95-121">For more information on hello Query syntax, see hello [Query object documentation].</span></span>

#### <span data-ttu-id="f0b95-122"><a name="table-filter"></a>Filtragem de dados no servidor de Olá</span><span class="sxs-lookup"><span data-stu-id="f0b95-122"><a name="table-filter"></a>Filtering data on hello server</span></span>
<span data-ttu-id="f0b95-123">Pode utilizar um `where` cláusula na referência de tabela Olá:</span><span class="sxs-lookup"><span data-stu-id="f0b95-123">You can use a `where` clause on hello table reference:</span></span>

```
table
    .where({ userId: user.userId, complete: false })
    .read()
    .then(success, failure);
```

<span data-ttu-id="f0b95-124">Também pode utilizar uma função que filtra o objeto de Olá.</span><span class="sxs-lookup"><span data-stu-id="f0b95-124">You can also use a function that filters hello object.</span></span>  <span data-ttu-id="f0b95-125">Neste caso, Olá `this` variável atribuída toothe o objeto atual a ser filtrado.</span><span class="sxs-lookup"><span data-stu-id="f0b95-125">In this case, hello `this` variable is assigned toothe current object being filtered.</span></span>  <span data-ttu-id="f0b95-126">Olá seguinte código é funcionalmente equivalente toohello exemplo anterior:</span><span class="sxs-lookup"><span data-stu-id="f0b95-126">hello following code is functionally equivalent toohello prior example:</span></span>

```
function filterByUserId(currentUserId) {
    return this.userId === currentUserId && this.complete === false;
}

table
    .where(filterByUserId, user.userId)
    .read()
    .then(success, failure);
```

#### <span data-ttu-id="f0b95-127"><a name="table-paging"></a>Paginar através de dados</span><span class="sxs-lookup"><span data-stu-id="f0b95-127"><a name="table-paging"></a>Paging through data</span></span>
<span data-ttu-id="f0b95-128">Utilizar Olá `take()` e `skip()` métodos.</span><span class="sxs-lookup"><span data-stu-id="f0b95-128">Utilize hello `take()` and `skip()` methods.</span></span>  <span data-ttu-id="f0b95-129">Por exemplo, se desejar tabela de Olá toosplit numa linha de 100 registos:</span><span class="sxs-lookup"><span data-stu-id="f0b95-129">For example, if you wish toosplit hello table into 100-row records:</span></span>

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

<span data-ttu-id="f0b95-130">Olá `.includeTotalCount()` método é utilizado tooadd um objeto de resultados do totalCount campo toohello.</span><span class="sxs-lookup"><span data-stu-id="f0b95-130">hello `.includeTotalCount()` method is used tooadd a totalCount field toohello results object.</span></span>  <span data-ttu-id="f0b95-131">O campo de totalCount é preenchido com o número total de Olá de registos que teria de ser devolvido se a paginação não é utilizada.</span><span class="sxs-lookup"><span data-stu-id="f0b95-131">The totalCount field is filled with hello total number of records that would be returned if no paging is used.</span></span>

<span data-ttu-id="f0b95-132">Em seguida, pode utilizar a variável de páginas de Olá e algumas tooprovide de botões de IU uma lista de página; utilizar `loadPage()` carregar novos registos de Olá para cada página.</span><span class="sxs-lookup"><span data-stu-id="f0b95-132">You can then use hello pages variable and some UI buttons tooprovide a page list; use `loadPage()` to load hello new records for each page.</span></span>  <span data-ttu-id="f0b95-133">Implementar a colocação em cache toospeed acesso toorecords que já foram carregadas.</span><span class="sxs-lookup"><span data-stu-id="f0b95-133">Implement caching toospeed access toorecords that have already been loaded.</span></span>

#### <span data-ttu-id="f0b95-134"><a name="sorting-data"></a>Como: devolver dados ordenados</span><span class="sxs-lookup"><span data-stu-id="f0b95-134"><a name="sorting-data"></a>How to: Return sorted data</span></span>
<span data-ttu-id="f0b95-135">Olá utilize `.orderBy()` ou `.orderByDescending()` consultar métodos:</span><span class="sxs-lookup"><span data-stu-id="f0b95-135">Use hello `.orderBy()` or `.orderByDescending()` query methods:</span></span>

```
table
    .orderBy('name')
    .read()
    .then(success, failure);
```

<span data-ttu-id="f0b95-136">Para obter mais informações sobre o objeto da consulta Olá, consulte Olá [consultar a documentação do objeto].</span><span class="sxs-lookup"><span data-stu-id="f0b95-136">For more information on hello Query object, see hello [Query object documentation].</span></span>

### <span data-ttu-id="f0b95-137"><a name="inserting"></a>Como: inserir dados</span><span class="sxs-lookup"><span data-stu-id="f0b95-137"><a name="inserting"></a>How to: Insert data</span></span>
<span data-ttu-id="f0b95-138">Criar um objeto de JavaScript com data adequada Olá e chamada `table.insert()` no modo assíncrono:</span><span class="sxs-lookup"><span data-stu-id="f0b95-138">Create a JavaScript object with hello appropriate date and call `table.insert()` asynchronously:</span></span>

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

<span data-ttu-id="f0b95-139">No inserção com êxito, item Olá inserido é devolvido com os campos adicionais Olá que são necessários para operações de sincronização.</span><span class="sxs-lookup"><span data-stu-id="f0b95-139">On successful insertion, hello inserted item is returned with hello additional fields that are required for sync operations.</span></span>  <span data-ttu-id="f0b95-140">Atualize a sua própria cache com estas informações para atualizações posteriores.</span><span class="sxs-lookup"><span data-stu-id="f0b95-140">Update your own cache with this information for later updates.</span></span>

<span data-ttu-id="f0b95-141">Olá, Azure Mobile Apps Node.js servidor SDK suporta esquema dinâmica para fins de desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="f0b95-141">hello Azure Mobile Apps Node.js Server SDK supports dynamic schema for development purposes.</span></span>  <span data-ttu-id="f0b95-142">Esquema dinâmica permite-lhe tabela do tooadd colunas toohello especificando-los numa operação insert ou update.</span><span class="sxs-lookup"><span data-stu-id="f0b95-142">Dynamic Schema allows you tooadd columns toohello table by specifying them in an insert or update operation.</span></span>  <span data-ttu-id="f0b95-143">Recomendamos que desative dinâmica esquema antes de mover o tooproduction de aplicação.</span><span class="sxs-lookup"><span data-stu-id="f0b95-143">We recommend that you turn off dynamic schema before moving your application tooproduction.</span></span>

### <span data-ttu-id="f0b95-144"><a name="modifying"></a>Como: modificar dados</span><span class="sxs-lookup"><span data-stu-id="f0b95-144"><a name="modifying"></a>How to: Modify data</span></span>
<span data-ttu-id="f0b95-145">Toohello semelhante `.insert()` método, deve criar um objeto de atualização e, em seguida, chame `.update()`.</span><span class="sxs-lookup"><span data-stu-id="f0b95-145">Similar toohello `.insert()` method, you should create an Update object and then call `.update()`.</span></span>  <span data-ttu-id="f0b95-146">Olá objetos de atualização tem de conter ID Olá toobe registos Olá atualizada - Olá ID é obtido ao ler o registo de Olá ou ao chamar `.insert()`.</span><span class="sxs-lookup"><span data-stu-id="f0b95-146">hello update object must contain hello ID of hello record toobe updated - hello ID is obtained when reading hello record or when calling `.insert()`.</span></span>

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

### <span data-ttu-id="f0b95-147"><a name="deleting"></a>Como: eliminar dados</span><span class="sxs-lookup"><span data-stu-id="f0b95-147"><a name="deleting"></a>How to: Delete data</span></span>
<span data-ttu-id="f0b95-148">toodelete um registo, chamada Olá `.del()` método.</span><span class="sxs-lookup"><span data-stu-id="f0b95-148">toodelete a record, call hello `.del()` method.</span></span>  <span data-ttu-id="f0b95-149">Transmita o ID de Olá uma referência de objeto:</span><span class="sxs-lookup"><span data-stu-id="f0b95-149">Pass hello ID in an object reference:</span></span>

```
table
    .del({ id: '7163bc7a-70b2-4dde-98e9-8818969611bd' })
    .done(function () {
        // Record is now deleted - update your cache
    }, failure);
```
