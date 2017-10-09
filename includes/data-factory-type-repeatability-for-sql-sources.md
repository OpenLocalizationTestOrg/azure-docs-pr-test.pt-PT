## <a name="repeatability-during-copy"></a><span data-ttu-id="5604a-101">Repetibilidade durante a cópia</span><span class="sxs-lookup"><span data-stu-id="5604a-101">Repeatability during Copy</span></span>
<span data-ttu-id="5604a-102">Quando copiar tooAzure de dados do SQL Server/SQL Server a partir de outros dados armazena um repetibilidade de tookeep necessidades em mente tooavoid resultados inesperados.</span><span class="sxs-lookup"><span data-stu-id="5604a-102">When copying data tooAzure SQL/SQL Server from other data stores one needs tookeep repeatability in mind tooavoid unintended outcomes.</span></span> 

<span data-ttu-id="5604a-103">Quando copiar dados tooAzure base de dados do SQL Server/SQL Server, atividade de cópia irá pela tabela de receptores de toohello Olá conjunto de dados predefinido ACRESCENTAR por predefinição.</span><span class="sxs-lookup"><span data-stu-id="5604a-103">When copying data tooAzure SQL/SQL Server Database, copy activity will by default APPEND hello data set toohello sink table by default.</span></span> <span data-ttu-id="5604a-104">Por exemplo, quando copiar dados a partir de uma origem de ficheiro CSV (dados de valores separados por vírgulas) que contém dois regista tooAzure base de dados do SQL Server/SQL Server, isto é que tabela Olá parece ser:</span><span class="sxs-lookup"><span data-stu-id="5604a-104">For example, when copying data from a CSV (comma separated values data) file source containing two records tooAzure SQL/SQL Server Database, this is what hello table looks like:</span></span>

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    2            2015-05-01 00:00:00
```

<span data-ttu-id="5604a-105">Suponha que encontrou erros no ficheiro de origem e a quantidade de Olá atualizada de baixo Tube de 2 too4 no ficheiro de origem Olá.</span><span class="sxs-lookup"><span data-stu-id="5604a-105">Suppose you found errors in source file and updated hello quantity of Down Tube from 2 too4 in hello source file.</span></span> <span data-ttu-id="5604a-106">Se executar novamente o setor de dados de Olá durante esse período, encontrará dois novos registos anexado tooAzure base de dados do SQL Server/SQL Server.</span><span class="sxs-lookup"><span data-stu-id="5604a-106">If you re-run hello data slice for that period, you’ll find two new records appended tooAzure SQL/SQL Server Database.</span></span> <span data-ttu-id="5604a-107">Olá abaixo parte do princípio de que nenhuma das colunas de Olá na tabela de Olá tem restrição de chave primária Olá.</span><span class="sxs-lookup"><span data-stu-id="5604a-107">hello below assumes none of hello columns in hello table have hello primary key constraint.</span></span>

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    2            2015-05-01 00:00:00
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    4            2015-05-01 00:00:00
```

<span data-ttu-id="5604a-108">tooavoid isto, terá de semântica UPSERT toospecify tirando partido de uma das Olá abaixo 2 mecanismos indicado abaixo.</span><span class="sxs-lookup"><span data-stu-id="5604a-108">tooavoid this, you will need toospecify UPSERT semantics by leveraging one of hello below 2 mechanisms stated below.</span></span>

> [!NOTE]
> <span data-ttu-id="5604a-109">Um setor pode ser novamente executado automaticamente no Azure Data Factory de acordo com a política de repetição de Olá especificada.</span><span class="sxs-lookup"><span data-stu-id="5604a-109">A slice can be re-run automatically in Azure Data Factory as per hello retry policy specified.</span></span>
> 
> 

### <a name="mechanism-1"></a><span data-ttu-id="5604a-110">Mecanismo de 1</span><span class="sxs-lookup"><span data-stu-id="5604a-110">Mechanism 1</span></span>
<span data-ttu-id="5604a-111">Pode tirar partido **sqlWriterCleanupScript** propriedade toofirst efetuar a ação de limpeza quando um setor é executado.</span><span class="sxs-lookup"><span data-stu-id="5604a-111">You can leverage **sqlWriterCleanupScript** property toofirst perform cleanup action when a slice is run.</span></span> 

```json
"sink":  
{ 
  "type": "SqlSink", 
  "sqlWriterCleanupScript": "$$Text.Format('DELETE FROM table WHERE ModifiedDate >= \\'{0:yyyy-MM-dd HH:mm}\\' AND ModifiedDate < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
}
```

<span data-ttu-id="5604a-112">Olá script de limpeza iria ser executado primeiro durante a cópia de um setor dado que iria a eliminar dados de Olá do setor de toothat correspondente do Olá tabela SQL.</span><span class="sxs-lookup"><span data-stu-id="5604a-112">hello cleanup script would be executed first during copy for a given slice which would delete hello data from hello SQL Table corresponding toothat slice.</span></span> <span data-ttu-id="5604a-113">atividade de Olá subsequentemente irá inserir dados Olá na Olá tabela SQL.</span><span class="sxs-lookup"><span data-stu-id="5604a-113">hello activity will subsequently insert hello data into hello SQL Table.</span></span> 

<span data-ttu-id="5604a-114">Se o setor de Olá está agora volte a executar, em seguida, pode encontrar a quantidade de Olá é atualizada como pretendido.</span><span class="sxs-lookup"><span data-stu-id="5604a-114">If hello slice is now re-run, then you will find hello quantity is updated as desired.</span></span>

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    4            2015-05-01 00:00:00
```

<span data-ttu-id="5604a-115">Suponha que Olá registo Washer simples é removido do csv original Olá.</span><span class="sxs-lookup"><span data-stu-id="5604a-115">Suppose hello Flat Washer record is removed from hello original csv.</span></span> <span data-ttu-id="5604a-116">Em seguida, volte em execução setor de Olá produziria Olá seguinte resultado:</span><span class="sxs-lookup"><span data-stu-id="5604a-116">Then re-running hello slice would produce hello following result:</span></span> 

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
7     Down Tube    4            2015-05-01 00:00:00
```
<span data-ttu-id="5604a-117">Nada de novo tinha toobe concluído.</span><span class="sxs-lookup"><span data-stu-id="5604a-117">Nothing new had toobe done.</span></span> <span data-ttu-id="5604a-118">atividade de cópia de Olá ficou Olá limpeza toodelete Olá correspondente dados de script para esse setor.</span><span class="sxs-lookup"><span data-stu-id="5604a-118">hello copy activity ran hello cleanup script toodelete hello corresponding data for that slice.</span></span> <span data-ttu-id="5604a-119">Em seguida, lê-lo entrada Olá do ficheiro csv de Olá (que, em seguida, contidos apenas 1 registo) e inseridas-Olá tabela.</span><span class="sxs-lookup"><span data-stu-id="5604a-119">Then it read hello input from hello csv (which then contained only 1 record) and inserted it into hello Table.</span></span> 

### <a name="mechanism-2"></a><span data-ttu-id="5604a-120">Mecanismo de 2</span><span class="sxs-lookup"><span data-stu-id="5604a-120">Mechanism 2</span></span>
> [!IMPORTANT]
> <span data-ttu-id="5604a-121">sliceIdentifierColumnName não é suportada para o Azure SQL Data Warehouse neste momento.</span><span class="sxs-lookup"><span data-stu-id="5604a-121">sliceIdentifierColumnName is not supported for Azure SQL Data Warehouse at this time.</span></span> 

<span data-ttu-id="5604a-122">Repetibilidade de tooachieve outro mecanismo é ter uma coluna dedicada (**sliceIdentifierColumnName**) no Olá tabela de destino.</span><span class="sxs-lookup"><span data-stu-id="5604a-122">Another mechanism tooachieve repeatability is by having a dedicated column (**sliceIdentifierColumnName**) in hello target Table.</span></span> <span data-ttu-id="5604a-123">Esta coluna seria utilizada pelo Azure Data Factory tooensure Olá origem e destino mantenha-se sincronizados.</span><span class="sxs-lookup"><span data-stu-id="5604a-123">This column would be used by Azure Data Factory tooensure hello source and destination stay synchronized.</span></span> <span data-ttu-id="5604a-124">Esta abordagem funciona quando existe flexibilidade na alterar ou a definição de esquema de tabela de SQL de destino Olá.</span><span class="sxs-lookup"><span data-stu-id="5604a-124">This approach works when there is flexibility in changing or defining hello destination SQL Table schema.</span></span> 

<span data-ttu-id="5604a-125">Esta coluna seria utilizada pelo Azure Data Factory para fins de repetibilidade e no processo de Olá do Azure Data Factory não efetuará quaisquer esquema toohello tabela é alterado.</span><span class="sxs-lookup"><span data-stu-id="5604a-125">This column would be used by Azure Data Factory for repeatability purposes and in hello process Azure Data Factory will not make any schema changes toohello Table.</span></span> <span data-ttu-id="5604a-126">Forma toouse esta abordagem:</span><span class="sxs-lookup"><span data-stu-id="5604a-126">Way toouse this approach:</span></span>

1. <span data-ttu-id="5604a-127">Defina uma coluna do tipo binário (32) no destino Olá tabela SQL.</span><span class="sxs-lookup"><span data-stu-id="5604a-127">Define a column of type binary (32) in hello destination SQL Table.</span></span> <span data-ttu-id="5604a-128">Não deverá haver nenhum restrições nesta coluna.</span><span class="sxs-lookup"><span data-stu-id="5604a-128">There should be no constraints on this column.</span></span> <span data-ttu-id="5604a-129">Vamos nome desta coluna como 'ColumnForADFuseOnly' para este exemplo.</span><span class="sxs-lookup"><span data-stu-id="5604a-129">Let's name this column as ‘ColumnForADFuseOnly’ for this example.</span></span>
2. <span data-ttu-id="5604a-130">Utilizá-lo na atividade de cópia de Olá da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="5604a-130">Use it in hello copy activity as follows:</span></span>
   
    ```json
    "sink":  
    { 
   
        "type": "SqlSink", 
        "sliceIdentifierColumnName": "ColumnForADFuseOnly"
    }
    ```

<span data-ttu-id="5604a-131">O Azure Data Factory preencherá esta coluna de acordo com a respetiva necessidade tooensure Olá origem e de destino permanecem sincronizadas.</span><span class="sxs-lookup"><span data-stu-id="5604a-131">Azure Data Factory will populate this column as per its need tooensure hello source and destination stay synchronized.</span></span> <span data-ttu-id="5604a-132">valores Olá esta coluna não devem ser utilizados fora neste contexto por utilizador Olá.</span><span class="sxs-lookup"><span data-stu-id="5604a-132">hello values of this column should not be used outside of this context by hello user.</span></span> 

<span data-ttu-id="5604a-133">Semelhante toomechanism 1, será de atividade de cópia automaticamente primeiro limpar dados de Olá para Olá dado o setor do destino de Olá tabela SQL e, em seguida, executar a atividade de cópia de Olá normalmente tooinsert dados Olá toodestination de origem para essa setor.</span><span class="sxs-lookup"><span data-stu-id="5604a-133">Similar toomechanism 1, Copy Activity will automatically first clean up hello data for hello given slice from hello destination SQL Table and then run hello copy activity normally tooinsert hello data from source toodestination for that slice.</span></span> 

