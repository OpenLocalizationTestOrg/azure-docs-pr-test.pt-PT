---
title: "aaaRepeatable cópia no Azure Data Factory | Microsoft Docs"
description: "Saiba como tooavoid duplicados, apesar de um setor que copia dados é executado mais do que uma vez."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: 
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jingwang
ms.openlocfilehash: 79a3fde2b700bf0a0e167479d6a86c5bee1bf7ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="repeatable-copy-in-azure-data-factory"></a><span data-ttu-id="4a5e8-103">Repetíveis cópia no Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="4a5e8-103">Repeatable copy in Azure Data Factory</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="4a5e8-104">Repetíveis leitura a partir de origens relacionais</span><span class="sxs-lookup"><span data-stu-id="4a5e8-104">Repeatable read from relational sources</span></span>
<span data-ttu-id="4a5e8-105">Quando copiar dados de arquivos de dados relacional, manter a repetibilidade em mente tooavoid resultados inesperados.</span><span class="sxs-lookup"><span data-stu-id="4a5e8-105">When copying data from relational data stores, keep repeatability in mind tooavoid unintended outcomes.</span></span> <span data-ttu-id="4a5e8-106">No Azure Data Factory, pode voltar a executar um setor manualmente.</span><span class="sxs-lookup"><span data-stu-id="4a5e8-106">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="4a5e8-107">Também pode configurar a política de repetição para um conjunto de dados para que um setor será novamente executado quando ocorre uma falha.</span><span class="sxs-lookup"><span data-stu-id="4a5e8-107">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="4a5e8-108">Quando um setor é voltar a executar qualquer forma, terá de toomake certificar-se de que Olá mesmos dados é de leitura como não independentemente do número de vezes que um setor é executado.</span><span class="sxs-lookup"><span data-stu-id="4a5e8-108">When a slice is rerun in either way, you need toomake sure that hello same data is read no matter how many times a slice is run.</span></span>  
 
> [!NOTE]
> <span data-ttu-id="4a5e8-109">Olá exemplos seguintes são para o Azure SQL, mas são aplicáveis tooany arquivo de dados que suporta conjuntos de dados retangular.</span><span class="sxs-lookup"><span data-stu-id="4a5e8-109">hello following samples are for Azure SQL but are applicable tooany data store that supports rectangular datasets.</span></span> <span data-ttu-id="4a5e8-110">Poderá ter tooadjust Olá **tipo** de origem e Olá **consulta** propriedade (por exemplo: consulta em vez de sqlReaderQuery) para dados de Olá armazenar.</span><span class="sxs-lookup"><span data-stu-id="4a5e8-110">You may have tooadjust hello **type** of source and hello **query** property (for example: query instead of sqlReaderQuery) for hello data store.</span></span>   

<span data-ttu-id="4a5e8-111">Normalmente, ao ler do relacionais arquivos, quer tooread únicos Olá dados correspondente toothat setor.</span><span class="sxs-lookup"><span data-stu-id="4a5e8-111">Usually, when reading from relational stores, you want tooread only hello data corresponding toothat slice.</span></span> <span data-ttu-id="4a5e8-112">Uma forma toodo, por isso, seria utilizando Olá WindowStart e WindowEnd sistema variáveis disponíveis no Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="4a5e8-112">A way toodo so would be by using hello WindowStart and WindowEnd system variables available in Azure Data Factory.</span></span> <span data-ttu-id="4a5e8-113">Leia sobre as variáveis de Olá e funções no Azure Data Factory aqui no Olá [do Azure Data Factory - as funções e variáveis do sistema](data-factory-functions-variables.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="4a5e8-113">Read about hello variables and functions in Azure Data Factory here in hello [Azure Data Factory - Functions and System Variables](data-factory-functions-variables.md) article.</span></span> <span data-ttu-id="4a5e8-114">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="4a5e8-114">Example:</span></span> 

```json
"source": {
    "type": "SqlSource",
    "sqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm\\'', WindowStart, WindowEnd)"
},
```
<span data-ttu-id="4a5e8-115">Esta consulta lê os dados que se situe no intervalo de duração de setor de Olá (WindowStart -> WindowEnd) da tabela de Olá MyTable.</span><span class="sxs-lookup"><span data-stu-id="4a5e8-115">This query reads data that falls in hello slice duration range (WindowStart -> WindowEnd) from hello table MyTable.</span></span> <span data-ttu-id="4a5e8-116">Volte a executar este setor seria também Certifique-se sempre que Olá mesmos dados é de leitura.</span><span class="sxs-lookup"><span data-stu-id="4a5e8-116">Rerun of this slice would also always ensure that hello same data is read.</span></span> 

<span data-ttu-id="4a5e8-117">Noutros casos, poderá desejar tabela inteira de Olá tooread e podem definir Olá sqlReaderQuery da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="4a5e8-117">In other cases, you may wish tooread hello entire table and may define hello sqlReaderQuery as follows:</span></span>

```json
"source": 
{            
    "type": "SqlSource",
    "sqlReaderQuery": "select * from MyTable"
},
```

## <a name="repeatable-write-toosqlsink"></a><span data-ttu-id="4a5e8-118">Escrita repetíveis tooSqlSink</span><span class="sxs-lookup"><span data-stu-id="4a5e8-118">Repeatable write tooSqlSink</span></span>
<span data-ttu-id="4a5e8-119">Quando copiar dados demasiado**Azure SQL/SQL Server** de outros arquivos de dados, terá de tookeep repetibilidade em mente tooavoid resultados inesperados.</span><span class="sxs-lookup"><span data-stu-id="4a5e8-119">When copying data too**Azure SQL/SQL Server** from other data stores, you need tookeep repeatability in mind tooavoid unintended outcomes.</span></span> 

<span data-ttu-id="4a5e8-120">Quando copiar dados tooAzure base de dados do SQL Server/SQL Server, a atividade de cópia de Olá acrescenta tabela do sink de toohello de dados por predefinição.</span><span class="sxs-lookup"><span data-stu-id="4a5e8-120">When copying data tooAzure SQL/SQL Server Database, hello copy activity appends data toohello sink table by default.</span></span> <span data-ttu-id="4a5e8-121">Diga, está a copiar dados de um CSV (valores separados por vírgulas) ficheiros que contêm dois registos toohello uma base de dados do servidor SQL/SQL do Azure a tabela seguinte.</span><span class="sxs-lookup"><span data-stu-id="4a5e8-121">Say, you are copying data from a CSV (comma-separated values) file containing two records toohello following table in an Azure SQL/SQL Server Database.</span></span> <span data-ttu-id="4a5e8-122">Quando um setor é executado, os registos de duas de Olá são copiados toohello tabela SQL.</span><span class="sxs-lookup"><span data-stu-id="4a5e8-122">When a slice runs, hello two records are copied toohello SQL table.</span></span> 

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    2            2015-05-01 00:00:00
```

<span data-ttu-id="4a5e8-123">Suponha que encontrou erros no ficheiro de origem e atualizar a quantidade de Olá de baixo Tube de 2 too4.</span><span class="sxs-lookup"><span data-stu-id="4a5e8-123">Suppose you found errors in source file and updated hello quantity of Down Tube from 2 too4.</span></span> <span data-ttu-id="4a5e8-124">Se voltar a executar o setor de dados de Olá durante esse período manualmente, encontrará dois novos registos anexado tooAzure base de dados do SQL Server/SQL Server.</span><span class="sxs-lookup"><span data-stu-id="4a5e8-124">If you rerun hello data slice for that period manually, you’ll find two new records appended tooAzure SQL/SQL Server Database.</span></span> <span data-ttu-id="4a5e8-125">Este exemplo parte do princípio de que nenhuma das colunas de Olá na tabela de Olá tem restrição de chave primária Olá.</span><span class="sxs-lookup"><span data-stu-id="4a5e8-125">This example assumes that none of hello columns in hello table has hello primary key constraint.</span></span>

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    2            2015-05-01 00:00:00
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    4            2015-05-01 00:00:00
```

<span data-ttu-id="4a5e8-126">tooavoid este comportamento, terá de semântica UPSERT toospecify utilizando um dos seguintes dois mecanismos de Olá:</span><span class="sxs-lookup"><span data-stu-id="4a5e8-126">tooavoid this behavior, you need toospecify UPSERT semantics by using one of hello following two mechanisms:</span></span>

### <a name="mechanism-1-using-sqlwritercleanupscript"></a><span data-ttu-id="4a5e8-127">Mecanismo de 1: sqlWriterCleanupScript utilizando o</span><span class="sxs-lookup"><span data-stu-id="4a5e8-127">Mechanism 1: using sqlWriterCleanupScript</span></span>
<span data-ttu-id="4a5e8-128">Pode utilizar Olá **sqlWriterCleanupScript** tooclean de propriedade dos dados da tabela do sink Olá antes de inserir dados Olá quando um setor é executado.</span><span class="sxs-lookup"><span data-stu-id="4a5e8-128">You can use hello **sqlWriterCleanupScript** property tooclean up data from hello sink table before inserting hello data when a slice is run.</span></span> 

```json
"sink":  
{ 
  "type": "SqlSink", 
  "sqlWriterCleanupScript": "$$Text.Format('DELETE FROM table WHERE ModifiedDate >= \\'{0:yyyy-MM-dd HH:mm}\\' AND ModifiedDate < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
}
```

<span data-ttu-id="4a5e8-129">Quando um setor é executado, o script de limpeza Olá é executado primeiro dados toodelete que corresponde ao toohello setor da tabela SQL Olá.</span><span class="sxs-lookup"><span data-stu-id="4a5e8-129">When a slice runs, hello cleanup script is run first toodelete data that corresponds toohello slice from hello SQL table.</span></span> <span data-ttu-id="4a5e8-130">atividade de cópia de Olá, em seguida, insere dados no Olá tabela SQL.</span><span class="sxs-lookup"><span data-stu-id="4a5e8-130">hello copy activity then inserts data into hello SQL Table.</span></span> <span data-ttu-id="4a5e8-131">Se o setor de Olá será novamente executada, a quantidade de Olá é atualizada conforme pretendido.</span><span class="sxs-lookup"><span data-stu-id="4a5e8-131">If hello slice is rerun, hello quantity is updated as desired.</span></span>

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    4            2015-05-01 00:00:00
```

<span data-ttu-id="4a5e8-132">Suponha que Olá registo Washer simples é removido do csv original Olá.</span><span class="sxs-lookup"><span data-stu-id="4a5e8-132">Suppose hello Flat Washer record is removed from hello original csv.</span></span> <span data-ttu-id="4a5e8-133">Em seguida, volte a executar o setor de Olá produziria Olá seguinte resultado:</span><span class="sxs-lookup"><span data-stu-id="4a5e8-133">Then rerunning hello slice would produce hello following result:</span></span> 

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
7     Down Tube    4            2015-05-01 00:00:00
```

<span data-ttu-id="4a5e8-134">atividade de cópia de Olá ficou Olá limpeza toodelete Olá correspondente dados de script para esse setor.</span><span class="sxs-lookup"><span data-stu-id="4a5e8-134">hello copy activity ran hello cleanup script toodelete hello corresponding data for that slice.</span></span> <span data-ttu-id="4a5e8-135">Em seguida, lê-lo entrada Olá do ficheiro csv de Olá (que contidas, em seguida, apenas um registo) e inseridas-Olá tabela.</span><span class="sxs-lookup"><span data-stu-id="4a5e8-135">Then it read hello input from hello csv (which then contained only one record) and inserted it into hello Table.</span></span> 

### <a name="mechanism-2-using-sliceidentifiercolumnname"></a><span data-ttu-id="4a5e8-136">Mecanismo de 2: sliceIdentifierColumnName utilizando o</span><span class="sxs-lookup"><span data-stu-id="4a5e8-136">Mechanism 2: using sliceIdentifierColumnName</span></span>
> [!IMPORTANT]
> <span data-ttu-id="4a5e8-137">Atualmente, sliceIdentifierColumnName não é suportada para o Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="4a5e8-137">Currently, sliceIdentifierColumnName is not supported for Azure SQL Data Warehouse.</span></span> 

<span data-ttu-id="4a5e8-138">repetibilidade do Olá segundo mecanismo tooachieve é ter uma coluna dedicada (sliceIdentifierColumnName) na tabela de destino de Olá.</span><span class="sxs-lookup"><span data-stu-id="4a5e8-138">hello second mechanism tooachieve repeatability is by having a dedicated column (sliceIdentifierColumnName) in hello target Table.</span></span> <span data-ttu-id="4a5e8-139">Esta coluna seria utilizada pelo Azure Data Factory tooensure Olá origem e destino mantenha-se sincronizados.</span><span class="sxs-lookup"><span data-stu-id="4a5e8-139">This column would be used by Azure Data Factory tooensure hello source and destination stay synchronized.</span></span> <span data-ttu-id="4a5e8-140">Esta abordagem funciona quando existe flexibilidade na alterar ou a definição de esquema de tabela de SQL de destino Olá.</span><span class="sxs-lookup"><span data-stu-id="4a5e8-140">This approach works when there is flexibility in changing or defining hello destination SQL Table schema.</span></span> 

<span data-ttu-id="4a5e8-141">Esta coluna é utilizada pelo Azure Data Factory para fins de repetibilidade e processo de Olá do Azure Data Factory não fazer qualquer esquema toohello tabela é alterado.</span><span class="sxs-lookup"><span data-stu-id="4a5e8-141">This column is used by Azure Data Factory for repeatability purposes and in hello process Azure Data Factory does not make any schema changes toohello Table.</span></span> <span data-ttu-id="4a5e8-142">Forma toouse esta abordagem:</span><span class="sxs-lookup"><span data-stu-id="4a5e8-142">Way toouse this approach:</span></span>

1. <span data-ttu-id="4a5e8-143">Definir uma coluna do tipo **binário (32)** no destino Olá tabela SQL.</span><span class="sxs-lookup"><span data-stu-id="4a5e8-143">Define a column of type **binary (32)** in hello destination SQL Table.</span></span> <span data-ttu-id="4a5e8-144">Não deverá haver nenhum restrições nesta coluna.</span><span class="sxs-lookup"><span data-stu-id="4a5e8-144">There should be no constraints on this column.</span></span> <span data-ttu-id="4a5e8-145">Vamos nome desta coluna como AdfSliceIdentifier para este exemplo.</span><span class="sxs-lookup"><span data-stu-id="4a5e8-145">Let's name this column as AdfSliceIdentifier for this example.</span></span>


    <span data-ttu-id="4a5e8-146">Tabela de origem:</span><span class="sxs-lookup"><span data-stu-id="4a5e8-146">Source table:</span></span>

    ```sql
    CREATE TABLE [dbo].[Student](
       [Id] [varchar](32) NOT NULL,
       [Name] [nvarchar](256) NOT NULL
    )
    ```

    <span data-ttu-id="4a5e8-147">Tabela de destino:</span><span class="sxs-lookup"><span data-stu-id="4a5e8-147">Destination table:</span></span> 

    ```sql
    CREATE TABLE [dbo].[Student](
       [Id] [varchar](32) NOT NULL,
       [Name] [nvarchar](256) NOT NULL,
       [AdfSliceIdentifier] [binary](32) NULL
    )
    ```

2. <span data-ttu-id="4a5e8-148">Utilizá-lo na atividade de cópia de Olá da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="4a5e8-148">Use it in hello copy activity as follows:</span></span>
   
    ```json
    "sink":  
    { 
   
        "type": "SqlSink", 
        "sliceIdentifierColumnName": "AdfSliceIdentifier"
    }
    ```

<span data-ttu-id="4a5e8-149">O Azure Data Factory preenche esta coluna de acordo com a respetiva necessidade tooensure Olá origem e de destino permanecem sincronizadas.</span><span class="sxs-lookup"><span data-stu-id="4a5e8-149">Azure Data Factory populates this column as per its need tooensure hello source and destination stay synchronized.</span></span> <span data-ttu-id="4a5e8-150">valores Olá esta coluna não devem ser utilizados fora neste contexto.</span><span class="sxs-lookup"><span data-stu-id="4a5e8-150">hello values of this column should not be used outside of this context.</span></span> 

<span data-ttu-id="4a5e8-151">Semelhante toomechanism 1, a atividade de cópia limpa automaticamente dados de Olá para Olá fornecido setor do destino de Olá tabela SQL.</span><span class="sxs-lookup"><span data-stu-id="4a5e8-151">Similar toomechanism 1, Copy Activity automatically cleans up hello data for hello given slice from hello destination SQL Table.</span></span> <span data-ttu-id="4a5e8-152">Em seguida, inserem dados de origem na tabela de destino toohello.</span><span class="sxs-lookup"><span data-stu-id="4a5e8-152">It then inserts data from source in toohello destination table.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="4a5e8-153">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="4a5e8-153">Next steps</span></span>
<span data-ttu-id="4a5e8-154">Reveja Olá seguintes artigos do conector que, para concluir os exemplos JSON:</span><span class="sxs-lookup"><span data-stu-id="4a5e8-154">Review hello following connector articles that for complete JSON examples:</span></span> 

- [<span data-ttu-id="4a5e8-155">Base de Dados SQL do Azure</span><span class="sxs-lookup"><span data-stu-id="4a5e8-155">Azure SQL Database</span></span>](data-factory-azure-sql-connector.md)
- [<span data-ttu-id="4a5e8-156">Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="4a5e8-156">Azure SQL Data Warehouse</span></span>](data-factory-azure-sql-data-warehouse-connector.md)
- [<span data-ttu-id="4a5e8-157">SQL Server</span><span class="sxs-lookup"><span data-stu-id="4a5e8-157">SQL Server</span></span>](data-factory-sqlserver-connector.md)