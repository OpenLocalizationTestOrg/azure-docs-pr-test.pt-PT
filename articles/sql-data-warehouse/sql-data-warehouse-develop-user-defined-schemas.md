---
title: definido pelo aaaUser esquemas no SQL Data Warehouse | Microsoft Docs
description: "Sugestões para utilizar os esquemas de Transact-SQL no Azure SQL Data Warehouse para desenvolver soluções."
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: 52af5bd5-d5d3-4f9b-8704-06829fb924e3
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: t-sql
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: c411d6fed68e67c444a5871eab06182eaeb6dbf5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="user-defined-schemas-in-sql-data-warehouse"></a><span data-ttu-id="654ef-103">Esquemas definido pelo utilizador no SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="654ef-103">User-defined schemas in SQL Data Warehouse</span></span>
<span data-ttu-id="654ef-104">Armazéns de dados tradicionais, muitas vezes, utilize bases de dados separada toocreate aplicação limites com base na carga de trabalho, o domínio ou segurança.</span><span class="sxs-lookup"><span data-stu-id="654ef-104">Traditional data warehouses often use separate databases toocreate application boundaries based on either workload, domain or security.</span></span> <span data-ttu-id="654ef-105">Por exemplo, um armazém de dados do SQL Server tradicional pode incluir uma base de dados de teste, uma base de dados do armazém de dados e algumas bases de dados do data mart.</span><span class="sxs-lookup"><span data-stu-id="654ef-105">For example, a traditional SQL Server data warehouse might include a staging database, a data warehouse database, and some data mart databases.</span></span> <span data-ttu-id="654ef-106">Nesta topologia, cada base de dados funciona como uma carga de trabalho e o limite de segurança na arquitetura de Olá.</span><span class="sxs-lookup"><span data-stu-id="654ef-106">In this topology each database operates as a workload and security boundary in hello architecture.</span></span>

<span data-ttu-id="654ef-107">Por outro lado, o SQL Data Warehouse executa carga de trabalho do Olá completo de dados do armazém dentro de uma base de dados.</span><span class="sxs-lookup"><span data-stu-id="654ef-107">By contrast, SQL Data Warehouse runs hello entire data warehouse workload within one database.</span></span> <span data-ttu-id="654ef-108">Cruzada da base de dados não são permitidas associações.</span><span class="sxs-lookup"><span data-stu-id="654ef-108">Cross database joins are not permitted.</span></span> <span data-ttu-id="654ef-109">Por conseguinte, o SQL Data Warehouse espera todas as tabelas utilizadas ao hello do armazém toobe armazenado dentro de uma base de dados Olá.</span><span class="sxs-lookup"><span data-stu-id="654ef-109">Therefore SQL Data Warehouse expects all tables used by hello warehouse toobe stored within hello one database.</span></span>

> [!NOTE]
> <span data-ttu-id="654ef-110">Armazém de dados do SQL Server não suporta consultas de base de dados cruzada de qualquer tipo.</span><span class="sxs-lookup"><span data-stu-id="654ef-110">SQL Data Warehouse does not support cross database queries of any kind.</span></span> <span data-ttu-id="654ef-111">Por conseguinte, as implementações de armazém de dados que tiram partido deste padrão de terá toobe revisto.</span><span class="sxs-lookup"><span data-stu-id="654ef-111">Consequently, data warehouse implementations that leverage this pattern will need toobe revised.</span></span>
> 
> 

## <a name="recommendations"></a><span data-ttu-id="654ef-112">Recomendações</span><span class="sxs-lookup"><span data-stu-id="654ef-112">Recommendations</span></span>
<span data-ttu-id="654ef-113">Estes são recomendações para consolidar as cargas de trabalho, segurança, domínio e limites funcionais utilizando esquemas definidas pelo utilizador</span><span class="sxs-lookup"><span data-stu-id="654ef-113">These are recommendations for consolidating workloads, security, domain and functional boundaries by using user defined schemas</span></span>

1. <span data-ttu-id="654ef-114">Utilize um toorun de base de dados do armazém de dados do SQL Server a carga de trabalho do armazém de dados completo</span><span class="sxs-lookup"><span data-stu-id="654ef-114">Use one SQL Data Warehouse database toorun your entire data warehouse workload</span></span>
2. <span data-ttu-id="654ef-115">Consolidar os seus dados do armazém ambiente toouse um SQL Data Warehouse base de dados existente</span><span class="sxs-lookup"><span data-stu-id="654ef-115">Consolidate your existing data warehouse environment toouse one SQL Data Warehouse database</span></span>
3. <span data-ttu-id="654ef-116">Tire partido **definido pelo utilizador esquemas** limites de Olá tooprovide anteriormente implementada utilizando bases de dados.</span><span class="sxs-lookup"><span data-stu-id="654ef-116">Leverage **user-defined schemas** tooprovide hello boundary previously implemented using databases.</span></span>

<span data-ttu-id="654ef-117">Se definido pelo utilizador esquemas não foram utilizadas anteriormente, em seguida, terá uma ardósia limpa.</span><span class="sxs-lookup"><span data-stu-id="654ef-117">If user-defined schemas have not been used previously then you have a clean slate.</span></span> <span data-ttu-id="654ef-118">Basta utilize o nome de base de dados antigo Olá como base Olá para as esquemas definido pelo utilizador na base de dados do Olá SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="654ef-118">Simply use hello old database name as hello basis for your user-defined schemas in hello SQL Data Warehouse database.</span></span>

<span data-ttu-id="654ef-119">Se já tem sido utilizadas esquemas, em seguida, tem algumas opções:</span><span class="sxs-lookup"><span data-stu-id="654ef-119">If schemas have already been used then you have a few options:</span></span>

1. <span data-ttu-id="654ef-120">Remova os nomes de esquema legado Olá e começar do início</span><span class="sxs-lookup"><span data-stu-id="654ef-120">Remove hello legacy schema names and start fresh</span></span>
2. <span data-ttu-id="654ef-121">Manter os nomes de esquema legado Olá por Olá previamente pendente esquema legado toohello tabela Nome</span><span class="sxs-lookup"><span data-stu-id="654ef-121">Retain hello legacy schema names by pre-pending hello legacy schema name toohello table name</span></span>
3. <span data-ttu-id="654ef-122">Manter os nomes de esquema legado Olá implementando vistas através de tabela Olá toore um esquema extra-criar Olá antigo esquema estrutura.</span><span class="sxs-lookup"><span data-stu-id="654ef-122">Retain hello legacy schema names by implementing views over hello table in an extra schema toore-create hello old schema structure.</span></span>

> [!NOTE]
> <span data-ttu-id="654ef-123">No primeiro inspeção opção 3 pode parecer como opção mais apelativos para resolver Olá.</span><span class="sxs-lookup"><span data-stu-id="654ef-123">On first inspection option 3 may seem like hello most appealing option.</span></span> <span data-ttu-id="654ef-124">No entanto, devil Olá é detalhadamente Olá.</span><span class="sxs-lookup"><span data-stu-id="654ef-124">However, hello devil is in hello detail.</span></span> <span data-ttu-id="654ef-125">As vistas são só de leitura em SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="654ef-125">Views are read only in SQL Data Warehouse.</span></span> <span data-ttu-id="654ef-126">Qualquer modificação de dados ou tabela teria toobe efetuada relativamente à tabela base Olá.</span><span class="sxs-lookup"><span data-stu-id="654ef-126">Any data or table modification would need toobe performed against hello base table.</span></span> <span data-ttu-id="654ef-127">Opção 3 apresenta também uma camada de vistas no seu sistema.</span><span class="sxs-lookup"><span data-stu-id="654ef-127">Option 3 also introduces a layer of views into your system.</span></span> <span data-ttu-id="654ef-128">Pode querer toogive este algumas profundamente adicional se estiver a utilizar vistas na sua arquitetura já.</span><span class="sxs-lookup"><span data-stu-id="654ef-128">You might want toogive this some additional thought if you are using views in your architecture already.</span></span>
> 
> 

### <a name="examples"></a><span data-ttu-id="654ef-129">Exemplos:</span><span class="sxs-lookup"><span data-stu-id="654ef-129">Examples:</span></span>
<span data-ttu-id="654ef-130">Implementar esquemas definido pelo utilizador com base nos nomes de base de dados</span><span class="sxs-lookup"><span data-stu-id="654ef-130">Implement user-defined schemas based on database names</span></span>

```sql
CREATE SCHEMA [stg]; -- stg previously database name for staging database
GO
CREATE SCHEMA [edw]; -- edw previously database name for hello data warehouse
GO
CREATE TABLE [stg].[customer] -- create staging tables in hello stg schema
(       CustKey BIGINT NOT NULL
,       ...
);
GO
CREATE TABLE [edw].[customer] -- create data warehouse tables in hello edw schema
(       CustKey BIGINT NOT NULL
,       ...
);
```

<span data-ttu-id="654ef-131">Manter esquema legada nomes por previamente pendente-los toohello nome da tabela.</span><span class="sxs-lookup"><span data-stu-id="654ef-131">Retain legacy schema names by pre-pending them toohello table name.</span></span> <span data-ttu-id="654ef-132">Utilize esquemas Olá limite de carga de trabalho.</span><span class="sxs-lookup"><span data-stu-id="654ef-132">Use schemas for hello workload boundary.</span></span>

```sql
CREATE SCHEMA [stg]; -- stg defines hello staging boundary
GO
CREATE SCHEMA [edw]; -- edw defines hello data warehouse boundary
GO
CREATE TABLE [stg].[dim_customer] --pre-pend hello old schema name toohello table and create in hello staging boundary
(       CustKey BIGINT NOT NULL
,       ...
);
GO
CREATE TABLE [edw].[dim_customer] --pre-pend hello old schema name toohello table and create in hello data warehouse boundary
(       CustKey BIGINT NOT NULL
,       ...
);
```

<span data-ttu-id="654ef-133">Manter os nomes de esquema legado utilizar as vistas</span><span class="sxs-lookup"><span data-stu-id="654ef-133">Retain legacy schema names using views</span></span>

```sql
CREATE SCHEMA [stg]; -- stg defines hello staging boundary
GO
CREATE SCHEMA [edw]; -- stg defines hello data warehouse boundary
GO
CREATE SCHEMA [dim]; -- edw defines hello legacy schema name boundary
GO
CREATE TABLE [stg].[customer] -- create hello base staging tables in hello staging boundary
(       CustKey    BIGINT NOT NULL
,       ...
)
GO
CREATE TABLE [edw].[customer] -- create hello base data warehouse tables in hello data warehouse boundary
(       CustKey    BIGINT NOT NULL
,       ...
)
GO
CREATE VIEW [dim].[customer] -- create a view in hello legacy schema name boundary for presentation consistency purposes only
AS
SELECT  CustKey
,       ...
FROM    [edw].customer
;
```

> [!NOTE]
> <span data-ttu-id="654ef-134">Qualquer alteração na estratégia de esquema tem uma revisão do modelo de segurança de Olá da base de dados de Olá.</span><span class="sxs-lookup"><span data-stu-id="654ef-134">Any change in schema strategy needs a review of hello security model for hello database.</span></span> <span data-ttu-id="654ef-135">Em muitos casos poderá ser toosimplify capaz de modelo de segurança de Olá ao atribuir permissões ao nível do esquema de Olá.</span><span class="sxs-lookup"><span data-stu-id="654ef-135">In many cases you might be able toosimplify hello security model by assigning permissions at hello schema level.</span></span> <span data-ttu-id="654ef-136">Se são necessárias permissões mais granulares, em seguida, pode utilizar funções de base de dados.</span><span class="sxs-lookup"><span data-stu-id="654ef-136">If more granular permissions are required then you can use database roles.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="654ef-137">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="654ef-137">Next steps</span></span>
<span data-ttu-id="654ef-138">Para mais sugestões de desenvolvimento, consulte [descrição geral do desenvolvimento][development overview].</span><span class="sxs-lookup"><span data-stu-id="654ef-138">For more development tips, see [development overview][development overview].</span></span>

<!--Image references-->

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md

<!--MSDN references-->

<!--Other Web references-->
