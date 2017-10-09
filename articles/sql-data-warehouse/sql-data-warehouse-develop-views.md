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
# <a name="views-in-sql-data-warehouse"></a>Vistas do armazém de dados do SQL Server
As vistas são particularmente útil no armazém de dados do SQL Server. Podem ser utilizadas num número de diferentes formas tooimprove Olá da qualidade da sua solução.  Este artigo realça alguns exemplos de como tooenrich sua solução com vistas, bem como limitações Olá que necessitam de toobe considerados.

> [!NOTE]
> Sintaxe para `CREATE VIEW` não é abordada neste artigo. Consulte toohello [Criar vista] [ CREATE VIEW] artigo no MSDN para estas informações de referência.
> 
> 

## <a name="architectural-abstraction"></a>Abstração da arquitetura
Um padrão de aplicação muito comum é toore-criar tabelas criar tabela AS SELECIONE (CTAS) seguido de um objeto mudar o nome padrão enfrenta carregar dados a utilizar.

exemplo de Olá abaixo adiciona a dimensão de data do novo data registos tooa. Tenha em atenção a como um novo tabble, DimDate_New, é criado pela primeira vez e, em seguida, mudar o nome da versão original de Olá tooreplace da tabela de Olá.

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

No entanto, esta abordagem pode resultar em tabelas de apresentação e disappearing da vista de um utilizador, bem como as mensagens de erro de "tabela não existe". Vistas podem ser utilizados tooprovide utilizadores com uma camada de apresentação consistente enfrenta objetos subjacente Olá são mudados. Ao fornecer aos utilizadores acesso toohello dados através das vistas, significa que os utilizadores não têm visibilidade toohave das tabelas subjacente Olá. Isto fornece uma experiência de utilizador consistente garantindo que os estruturadores de armazém de dados de Olá podem evoluir modelo de dados de Olá e maximizar o desempenho utilizando CTAS durante o processo de carregamento de dados de Olá.    

## <a name="performance-optimization"></a>Otimização do desempenho
Vistas também podem ser sobreutilizado tooenforce desempenho otimizado associações entre as tabelas. Por exemplo, uma vista pode incorporar uma chave de distribuição redundante como parte da Olá movimento de dados de toominimize de critérios de associação.  Outra vantagem de uma vista pode ser tooforce uma consulta específica ou sugestão de associação. Utilizar vistas desta forma, garante que associações são sempre executadas de forma ideal, evitando a necessidade de Olá de construção correto do utilizadores tooremember Olá para as respetivas associações.

## <a name="limitations"></a>Limitações
As vistas do armazém de dados do SQL Server são apenas metadados.  Por conseguinte Olá seguintes opções das não está disponível:

* Não há nenhuma opção de enlace de esquema
* Tabelas base não podem ser atualizadas através da vista de Olá
* Não não possível criar vistas através de tabelas temporárias
* Não são suportadas para Olá expansão / sugestões NOEXPAND
* Não existem nenhum vistas indexadas no SQL Data Warehouse

## <a name="next-steps"></a>Passos seguintes
Para obter mais sugestões de desenvolvimento, veja [SQL Data Warehouse development overview (Descrição geral do desenvolvimento no SQL Data Warehouse)][SQL Data Warehouse development overview].
Para `CREATE VIEW` sintaxe Consulte demasiado[Criar vista][CREATE VIEW].

<!--Image references-->

<!--Article references-->
[SQL Data Warehouse development overview]: ./sql-data-warehouse-overview-develop.md

<!--MSDN references-->
[CREATE VIEW]: https://msdn.microsoft.com/en-us/library/ms187956.aspx

<!--Other Web references-->
