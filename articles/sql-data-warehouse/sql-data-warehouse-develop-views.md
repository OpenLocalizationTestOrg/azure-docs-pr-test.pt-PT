---
title: vistas de aaaUsing T-SQL no Azure SQL Data Warehouse | Microsoft Docs
description: "Sugestões para utilizar as vistas de Transact-SQL no Azure SQL Data Warehouse para desenvolver soluções."
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: b5208f32-8f4a-4056-8788-2adbb253d9fd
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: t-sql
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: 3990b133946621691bdfa4b09523d21867470c74
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="views-in-sql-data-warehouse"></a><span data-ttu-id="83104-103">Vistas do armazém de dados do SQL Server</span><span class="sxs-lookup"><span data-stu-id="83104-103">Views in SQL Data Warehouse</span></span>
<span data-ttu-id="83104-104">As vistas são particularmente útil no armazém de dados do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="83104-104">Views are particularly useful in SQL Data Warehouse.</span></span> <span data-ttu-id="83104-105">Podem ser utilizadas num número de diferentes formas tooimprove Olá da qualidade da sua solução.</span><span class="sxs-lookup"><span data-stu-id="83104-105">They can be used in a number of different ways tooimprove hello quality of your solution.</span></span>  <span data-ttu-id="83104-106">Este artigo realça alguns exemplos de como tooenrich sua solução com vistas, bem como limitações Olá que necessitam de toobe considerados.</span><span class="sxs-lookup"><span data-stu-id="83104-106">This article highlights a few examples of how tooenrich your solution with views, as well as hello limitations that need toobe considered.</span></span>

> [!NOTE]
> <span data-ttu-id="83104-107">Sintaxe para `CREATE VIEW` não é abordada neste artigo.</span><span class="sxs-lookup"><span data-stu-id="83104-107">Syntax for `CREATE VIEW` is not discussed in this article.</span></span> <span data-ttu-id="83104-108">Consulte toohello [Criar vista] [ CREATE VIEW] artigo no MSDN para estas informações de referência.</span><span class="sxs-lookup"><span data-stu-id="83104-108">Please refer toohello [CREATE VIEW][CREATE VIEW] article on MSDN for this reference information.</span></span>
> 
> 

## <a name="architectural-abstraction"></a><span data-ttu-id="83104-109">Abstração da arquitetura</span><span class="sxs-lookup"><span data-stu-id="83104-109">Architectural abstraction</span></span>
<span data-ttu-id="83104-110">Um padrão de aplicação muito comum é toore-criar tabelas criar tabela AS SELECIONE (CTAS) seguido de um objeto mudar o nome padrão enfrenta carregar dados a utilizar.</span><span class="sxs-lookup"><span data-stu-id="83104-110">A very common application pattern is toore-create tables using CREATE TABLE AS SELECT (CTAS) followed by an object renaming pattern whilst loading data.</span></span>

<span data-ttu-id="83104-111">exemplo de Olá abaixo adiciona a dimensão de data do novo data registos tooa.</span><span class="sxs-lookup"><span data-stu-id="83104-111">hello example below adds new date records tooa date dimension.</span></span> <span data-ttu-id="83104-112">Tenha em atenção a como um novo tabble, DimDate_New, é criado pela primeira vez e, em seguida, mudar o nome da versão original de Olá tooreplace da tabela de Olá.</span><span class="sxs-lookup"><span data-stu-id="83104-112">Note how a new tabble, DimDate_New, is first created and then renamed tooreplace hello original version of hello table.</span></span>

```sql
CREATE TABLE dbo.DimDate_New
WITH (DISTRIBUTION = ROUND_ROBIN
, CLUSTERED INDEX (DateKey ASC)
)
AS
SELECT *
FROM   dbo.DimDate  AS prod
UNION ALL
SELECT *
FROM   dbo.DimDate_stg AS stg
;

RENAME OBJECT DimDate tooDimDate_Old;
RENAME OBJECT DimDate_New tooDimDate;

```

<span data-ttu-id="83104-113">No entanto, esta abordagem pode resultar em tabelas de apresentação e disappearing da vista de um utilizador, bem como as mensagens de erro de "tabela não existe".</span><span class="sxs-lookup"><span data-stu-id="83104-113">However, this approach can result in tables appearing and disappearing from a user's view as well as "table does not exist" error messages.</span></span> <span data-ttu-id="83104-114">Vistas podem ser utilizados tooprovide utilizadores com uma camada de apresentação consistente enfrenta objetos subjacente Olá são mudados.</span><span class="sxs-lookup"><span data-stu-id="83104-114">Views can be used tooprovide users with a consistent presentation layer whilst hello underlying objects are renamed.</span></span> <span data-ttu-id="83104-115">Ao fornecer aos utilizadores acesso toohello dados através das vistas, significa que os utilizadores não têm visibilidade toohave das tabelas subjacente Olá.</span><span class="sxs-lookup"><span data-stu-id="83104-115">By providing users access toohello data through a views, means users don't need toohave visibility of hello underlying tables.</span></span> <span data-ttu-id="83104-116">Isto fornece uma experiência de utilizador consistente garantindo que os estruturadores de armazém de dados de Olá podem evoluir modelo de dados de Olá e maximizar o desempenho utilizando CTAS durante o processo de carregamento de dados de Olá.</span><span class="sxs-lookup"><span data-stu-id="83104-116">This provides a consistent user experience while ensuring that hello data warehouse designers can evolve hello data model and maximize performance by using CTAS during hello data loading process.</span></span>    

## <a name="performance-optimization"></a><span data-ttu-id="83104-117">Otimização do desempenho</span><span class="sxs-lookup"><span data-stu-id="83104-117">Performance optimization</span></span>
<span data-ttu-id="83104-118">Vistas também podem ser sobreutilizado tooenforce desempenho otimizado associações entre as tabelas.</span><span class="sxs-lookup"><span data-stu-id="83104-118">Views can also be utilized tooenforce performance optimized joins between tables.</span></span> <span data-ttu-id="83104-119">Por exemplo, uma vista pode incorporar uma chave de distribuição redundante como parte da Olá movimento de dados de toominimize de critérios de associação.</span><span class="sxs-lookup"><span data-stu-id="83104-119">For example, a view can incorporate a redundant distribution key as part of hello joining criteria toominimize data movement.</span></span>  <span data-ttu-id="83104-120">Outra vantagem de uma vista pode ser tooforce uma consulta específica ou sugestão de associação.</span><span class="sxs-lookup"><span data-stu-id="83104-120">Another benefit of a view could be tooforce a specific query or joining hint.</span></span> <span data-ttu-id="83104-121">Utilizar vistas desta forma, garante que associações são sempre executadas de forma ideal, evitando a necessidade de Olá de construção correto do utilizadores tooremember Olá para as respetivas associações.</span><span class="sxs-lookup"><span data-stu-id="83104-121">Using views in this manner guarantees that joins are always performed in an optimal fashion avoiding hello need for users tooremember hello correct construct for their joins.</span></span>

## <a name="limitations"></a><span data-ttu-id="83104-122">Limitações</span><span class="sxs-lookup"><span data-stu-id="83104-122">Limitations</span></span>
<span data-ttu-id="83104-123">As vistas do armazém de dados do SQL Server são apenas metadados.</span><span class="sxs-lookup"><span data-stu-id="83104-123">Views in SQL Data Warehouse are metadata only.</span></span>  <span data-ttu-id="83104-124">Por conseguinte Olá seguintes opções das não está disponível:</span><span class="sxs-lookup"><span data-stu-id="83104-124">Consequently hello following options are not available:</span></span>

* <span data-ttu-id="83104-125">Não há nenhuma opção de enlace de esquema</span><span class="sxs-lookup"><span data-stu-id="83104-125">There is no schema binding option</span></span>
* <span data-ttu-id="83104-126">Tabelas base não podem ser atualizadas através da vista de Olá</span><span class="sxs-lookup"><span data-stu-id="83104-126">Base tables cannot be updated through hello view</span></span>
* <span data-ttu-id="83104-127">Não não possível criar vistas através de tabelas temporárias</span><span class="sxs-lookup"><span data-stu-id="83104-127">Views cannot be created over temporary tables</span></span>
* <span data-ttu-id="83104-128">Não são suportadas para Olá expansão / sugestões NOEXPAND</span><span class="sxs-lookup"><span data-stu-id="83104-128">There is no support for hello EXPAND / NOEXPAND hints</span></span>
* <span data-ttu-id="83104-129">Não existem nenhum vistas indexadas no SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="83104-129">There are no indexed views in SQL Data Warehouse</span></span>

## <a name="next-steps"></a><span data-ttu-id="83104-130">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="83104-130">Next steps</span></span>
<span data-ttu-id="83104-131">Para obter mais sugestões de desenvolvimento, veja [SQL Data Warehouse development overview (Descrição geral do desenvolvimento no SQL Data Warehouse)][SQL Data Warehouse development overview].</span><span class="sxs-lookup"><span data-stu-id="83104-131">For more development tips, see [SQL Data Warehouse development overview][SQL Data Warehouse development overview].</span></span>
<span data-ttu-id="83104-132">Para `CREATE VIEW` sintaxe Consulte demasiado[Criar vista][CREATE VIEW].</span><span class="sxs-lookup"><span data-stu-id="83104-132">For `CREATE VIEW` syntax please refer too[CREATE VIEW][CREATE VIEW].</span></span>

<!--Image references-->

<!--Article references-->
[SQL Data Warehouse development overview]: ./sql-data-warehouse-overview-develop.md

<!--MSDN references-->
[CREATE VIEW]: https://msdn.microsoft.com/en-us/library/ms187956.aspx

<!--Other Web references-->
