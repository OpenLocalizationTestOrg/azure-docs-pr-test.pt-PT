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
# <a name="user-defined-schemas-in-sql-data-warehouse"></a>Esquemas definido pelo utilizador no SQL Data Warehouse
Armazéns de dados tradicionais, muitas vezes, utilize bases de dados separada toocreate aplicação limites com base na carga de trabalho, o domínio ou segurança. Por exemplo, um armazém de dados do SQL Server tradicional pode incluir uma base de dados de teste, uma base de dados do armazém de dados e algumas bases de dados do data mart. Nesta topologia, cada base de dados funciona como uma carga de trabalho e o limite de segurança na arquitetura de Olá.

Por outro lado, o SQL Data Warehouse executa carga de trabalho do Olá completo de dados do armazém dentro de uma base de dados. Cruzada da base de dados não são permitidas associações. Por conseguinte, o SQL Data Warehouse espera todas as tabelas utilizadas ao hello do armazém toobe armazenado dentro de uma base de dados Olá.

> [!NOTE]
> Armazém de dados do SQL Server não suporta consultas de base de dados cruzada de qualquer tipo. Por conseguinte, as implementações de armazém de dados que tiram partido deste padrão de terá toobe revisto.
> 
> 

## <a name="recommendations"></a>Recomendações
Estes são recomendações para consolidar as cargas de trabalho, segurança, domínio e limites funcionais utilizando esquemas definidas pelo utilizador

1. Utilize um toorun de base de dados do armazém de dados do SQL Server a carga de trabalho do armazém de dados completo
2. Consolidar os seus dados do armazém ambiente toouse um SQL Data Warehouse base de dados existente
3. Tire partido **definido pelo utilizador esquemas** limites de Olá tooprovide anteriormente implementada utilizando bases de dados.

Se definido pelo utilizador esquemas não foram utilizadas anteriormente, em seguida, terá uma ardósia limpa. Basta utilize o nome de base de dados antigo Olá como base Olá para as esquemas definido pelo utilizador na base de dados do Olá SQL Data Warehouse.

Se já tem sido utilizadas esquemas, em seguida, tem algumas opções:

1. Remova os nomes de esquema legado Olá e começar do início
2. Manter os nomes de esquema legado Olá por Olá previamente pendente esquema legado toohello tabela Nome
3. Manter os nomes de esquema legado Olá implementando vistas através de tabela Olá toore um esquema extra-criar Olá antigo esquema estrutura.

> [!NOTE]
> No primeiro inspeção opção 3 pode parecer como opção mais apelativos para resolver Olá. No entanto, devil Olá é detalhadamente Olá. As vistas são só de leitura em SQL Data Warehouse. Qualquer modificação de dados ou tabela teria toobe efetuada relativamente à tabela base Olá. Opção 3 apresenta também uma camada de vistas no seu sistema. Pode querer toogive este algumas profundamente adicional se estiver a utilizar vistas na sua arquitetura já.
> 
> 

### <a name="examples"></a>Exemplos:
Implementar esquemas definido pelo utilizador com base nos nomes de base de dados

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

Manter esquema legada nomes por previamente pendente-los toohello nome da tabela. Utilize esquemas Olá limite de carga de trabalho.

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

Manter os nomes de esquema legado utilizar as vistas

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
> Qualquer alteração na estratégia de esquema tem uma revisão do modelo de segurança de Olá da base de dados de Olá. Em muitos casos poderá ser toosimplify capaz de modelo de segurança de Olá ao atribuir permissões ao nível do esquema de Olá. Se são necessárias permissões mais granulares, em seguida, pode utilizar funções de base de dados.
> 
> 

## <a name="next-steps"></a>Passos seguintes
Para mais sugestões de desenvolvimento, consulte [descrição geral do desenvolvimento][development overview].

<!--Image references-->

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md

<!--MSDN references-->

<!--Other Web references-->
