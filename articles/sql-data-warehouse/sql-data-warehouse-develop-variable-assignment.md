---
title: "variáveis de aaaAssign no SQL Data Warehouse | Microsoft Docs"
description: "Sugestões para atribuição de variáveis de Transact-SQL no Azure SQL Data Warehouse para desenvolver soluções."
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: 81ddc7cf-a6ba-4585-91a3-b6ea50f49227
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: t-sql
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: 9de48739bb0af80ff2a117704b31512c680f78d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="assign-variables-in-sql-data-warehouse"></a><span data-ttu-id="7318d-103">Atribuir variáveis no SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="7318d-103">Assign variables in SQL Data Warehouse</span></span>
<span data-ttu-id="7318d-104">As variáveis no armazém de dados do SQL Server são definidas utilizando um Olá `DECLARE` instrução ou Olá `SET` instrução.</span><span class="sxs-lookup"><span data-stu-id="7318d-104">Variables in SQL Data Warehouse are set using hello `DECLARE` statement or hello `SET` statement.</span></span>

<span data-ttu-id="7318d-105">Todos os seguintes Olá são formas válidas perfeitamente tooset um valor da variável:</span><span class="sxs-lookup"><span data-stu-id="7318d-105">All of hello following are perfectly valid ways tooset a variable value:</span></span>

## <a name="setting-variables-with-declare"></a><span data-ttu-id="7318d-106">Definir variáveis com DECLARE</span><span class="sxs-lookup"><span data-stu-id="7318d-106">Setting variables with DECLARE</span></span>
<span data-ttu-id="7318d-107">A inicializar variáveis com DECLARE é uma das Olá mais flexível formas tooset um valor da variável no armazém de dados do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="7318d-107">Initializing variables with DECLARE is one of hello most flexible ways tooset a variable value in SQL Data Warehouse.</span></span>

```sql
DECLARE @v  int = 0
;
```

<span data-ttu-id="7318d-108">Também pode utilizar DECLARE tooset mais de uma variável num momento.</span><span class="sxs-lookup"><span data-stu-id="7318d-108">You can also use DECLARE tooset more than one variable at a time.</span></span> <span data-ttu-id="7318d-109">Não é possível utilizar `SELECT` ou `UPDATE` toodo isto:</span><span class="sxs-lookup"><span data-stu-id="7318d-109">You cannot use `SELECT` or `UPDATE` toodo this:</span></span>

```sql
DECLARE @v  INT = (SELECT TOP 1 c_customer_sk FROM Customer where c_last_name = 'Smith')
,       @v1 INT = (SELECT TOP 1 c_customer_sk FROM Customer where c_last_name = 'Jones')
;
```

<span data-ttu-id="7318d-110">Não é possível inicializar o e utilizar uma variável num Olá mesma instrução DECLARE.</span><span class="sxs-lookup"><span data-stu-id="7318d-110">You cannot initialise and use a variable in hello same DECLARE statement.</span></span> <span data-ttu-id="7318d-111">tooillustrate Olá ponto Olá exemplo abaixo é **não** permitido como @p1 é inicializado tanto utilizado no Olá mesma instrução DECLARE.</span><span class="sxs-lookup"><span data-stu-id="7318d-111">tooillustrate hello point hello example below is **not** allowed as @p1 is both initialized and used in hello same DECLARE statement.</span></span> <span data-ttu-id="7318d-112">Este procedimento resultará num erro.</span><span class="sxs-lookup"><span data-stu-id="7318d-112">This will result in an error.</span></span>

```sql
DECLARE @p1 int = 0
,       @p2 int = (SELECT COUNT (*) FROM sys.types where is_user_defined = @p1 )
;
```

## <a name="setting-values-with-set"></a><span data-ttu-id="7318d-113">Valores de definição com conjunto</span><span class="sxs-lookup"><span data-stu-id="7318d-113">Setting values with SET</span></span>
<span data-ttu-id="7318d-114">Conjunto é um método muito comum para definir uma única variável.</span><span class="sxs-lookup"><span data-stu-id="7318d-114">Set is a very common method for setting a single variable.</span></span>

<span data-ttu-id="7318d-115">Todos os exemplos de Olá abaixo são formas válidas de definir uma variável com o conjunto de:</span><span class="sxs-lookup"><span data-stu-id="7318d-115">All of hello examples below are valid ways of setting a variable with SET:</span></span>

```sql
SET     @v = (Select max(database_id) from sys.databases);
SET     @v = 1;
SET     @v = @v+1;
SET     @v +=1;
```

<span data-ttu-id="7318d-116">Só é possível definir uma variável num momento com conjunto.</span><span class="sxs-lookup"><span data-stu-id="7318d-116">You can only set one variable at a time with SET.</span></span> <span data-ttu-id="7318d-117">No entanto, como podem ser vistos acima operadores compostos são permissable.</span><span class="sxs-lookup"><span data-stu-id="7318d-117">However, as can be seen above compound operators are permissable.</span></span>

## <a name="limitations"></a><span data-ttu-id="7318d-118">Limitações</span><span class="sxs-lookup"><span data-stu-id="7318d-118">Limitations</span></span>
<span data-ttu-id="7318d-119">Não é possível utilizar SELECIONE ou a ATUALIZAÇÃO para atribuição de variáveis.</span><span class="sxs-lookup"><span data-stu-id="7318d-119">You cannot use SELECT or UPDATE for variable assignment.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7318d-120">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="7318d-120">Next steps</span></span>
<span data-ttu-id="7318d-121">Para mais sugestões de desenvolvimento, consulte [descrição geral do desenvolvimento][development overview].</span><span class="sxs-lookup"><span data-stu-id="7318d-121">For more development tips, see [development overview][development overview].</span></span>

<!--Image references-->

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md

<!--MSDN references-->

<!--Other Web references-->
