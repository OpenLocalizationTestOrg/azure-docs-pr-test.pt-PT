---
title: "chaves de substituição de aaaCreate utilizando identidade | Microsoft Docs"
description: "Saiba como chaves de substituição de toocreate toouse identidade no seu tabelas."
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: faa1034d-314c-4f9d-af81-f5a9aedf33e4
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.date: 06/13/2017
ms.author: jrj;barbkess
ms.openlocfilehash: 502cdd2b510b229b2a19c1f78b11862a7386ae3b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-surrogate-keys-by-using-identity"></a>Criar chaves substituto através da utilização de identidade
> [!div class="op_single_selector"]
> * [Descrição geral][Overview]
> * [Tipos de dados][Data Types]
> * [Distribuir][Distribute]
> * [Índice][Index]
> * [Partição][Partition]
> * [Estatísticas][Statistics]
> * [Temporário][Temporary]
> * [Identidade][Identity]
> 
> 

Muitos modelers de dados, como as chaves de substituto toocreate as respetivas tabelas quando estes modelos de armazém de dados de design. Pode utilizar tooachieve de propriedade de identidade Olá este objetivo simples e eficaz sem afetar o desempenho da carga. 

## <a name="get-started-with-identity"></a>Começar com uma identidade
Pode definir uma tabela como ter a propriedade de identidade Olá ao primeiro criar tabela Olá utilizando sintaxe semelhante toohello a seguinte instrução:

```sql
CREATE TABLE dbo.T1
(   C1 INT IDENTITY(1,1) NOT NULL
,   C2 INT NULL
)
WITH
(   DISTRIBUTION = HASH(C2)
,   CLUSTERED COLUMNSTORE INDEX
)
;
```

Em seguida, pode utilizar `INSERT..SELECT` tabela de Olá toopopulate.

## <a name="behavior"></a>Comportamento
Olá propriedade de identidade é concebida tooscale enviados em todas as distribuições de Olá no armazém de dados de Olá sem afetar o desempenho da carga. Por conseguinte, implementação de Olá de identidade é dedicada a alcançar estes objetivos. Esta secção realça nuances Olá de Olá implementação toohelp compreende-las mais detalhadamente.  

### <a name="allocation-of-values"></a>Alocação de valores
Olá propriedade de identidade não garante a ordem de Olá no qual Olá são atribuídos valores de substituição, que reflete o comportamento de Olá do SQL Server e SQL Database do Azure. No entanto, no Azure SQL Data Warehouse, mais pronunciada de ausência de Olá de uma garantia. 

Olá seguinte o exemplo é uma ilustração:

```sql
CREATE TABLE dbo.T1
(   C1 INT IDENTITY(1,1)    NOT NULL
,   C2 VARCHAR(30)              NULL
)
WITH
(   DISTRIBUTION = HASH(C2)
,   CLUSTERED COLUMNSTORE INDEX
)
;

INSERT INTO dbo.T1
VALUES (NULL);

INSERT INTO dbo.T1
VALUES (NULL);

SELECT *
FROM dbo.T1;

DBCC PDW_SHOWSPACEUSED('dbo.T1');
```

No Olá anterior exemplo, duas linhas landed distribuição 1. primeira linha de Olá tem um valor de substituição de 1 Olá na coluna `C1`, e a segunda linha de Olá tem um valor de substituição de 61 Olá. Ambos estes valores foram gerados por Olá propriedade de identidade. No entanto, Olá dos valores de Olá não é contíguo. Este comportamento é propositado.

### <a name="skewed-data"></a>Dados distorcidos 
intervalo de Olá de valores para o tipo de dados de Olá são distribuídos uniformemente por distribuições Olá. Se sofrerá de uma tabela distribuída a partir dos dados distorcidos, Olá, em seguida, intervalo de valores datatype toohello disponível pode ser esgotado prematuramente. Por exemplo, se todos os dados de Olá termina uma distribuição único, em seguida, eficazmente Olá tabela tem acesso tooonly sixtieth um dos valores de Olá Olá do tipo de dados. Por este motivo, Olá propriedade de identidade é limitado demasiado`INT` e `BIGINT` apenas tipos de dados.

### <a name="selectinto"></a>SELECIONAR... PARA
Quando uma coluna de identidade existente é selecionada para uma nova tabela, coluna nova Olá herda propriedade de identidade Olá, a menos que uma das Olá seguintes condições for verdadeira:
- instrução SELECT Olá contém uma associação.
- Múltiplas instruções SELECIONADAS são associadas através da utilização de União.
- a coluna de identidade Olá é listada mais do que uma vez na lista de SELEÇÃO de Olá.
- a coluna de identidade Olá faz parte de uma expressão.
    
Se qualquer um dos seguintes condições for VERDADEIRO, a coluna Olá é criada NOT NULL em vez de a herança de propriedade de identidade Olá.

### <a name="create-table-as-select"></a>CRIAR TABLE AS SELECT
Criar tabela AS SELECIONE (CTAS) forma Olá mesmo comportamento SQL Server que é descrito selecione... PARA. No entanto, não é possível especificar uma propriedade de identidade na definição de coluna Olá de Olá `CREATE TABLE` fazem parte da instrução Olá. É também não é possível utilizar a função de identidade Olá no Olá `SELECT` fazem parte da Olá CTAS. toopopulate uma tabela, terá de toouse `CREATE TABLE` seguido de tabela de Olá toodefine `INSERT..SELECT` toopopulate-lo.

## <a name="explicitly-insert-values-into-an-identity-column"></a>Inserir explicitamente valores numa coluna de identidade 
Suporta o SQL Data Warehouse `SET IDENTITY_INSERT <your table> ON|OFF` sintaxe. Pode utilizar valores de inserção de tooexplicitly esta sintaxe na coluna de identidade Olá.

Muitos modelers de dados como negativo predefinidas toouse para determinados valores de linhas na respetiva dimensões. Um exemplo é Olá -1 ou linha "membro desconhecido". 

script seguinte Olá mostra como tooexplicitly adicionar esta linha utilizando IDENTITY_INSERT definir:

```sql
SET IDENTITY_INSERT dbo.T1 ON;

INSERT INTO dbo.T1
(   C1
,   C2
)
VALUES (-1,'UNKNOWN')
;

SET IDENTITY_INSERT dbo.T1 OFF;

SELECT  *
FROM    dbo.T1
;
```    

## <a name="load-data-into-a-table-with-identity"></a>Carregar dados para uma tabela com uma identidade

presença Olá Olá propriedade de identidade tem alguns códigos de carregamento de dados de tooyour implicações. Esta secção realça alguns padrões básicos para carregar dados para tabelas através da utilização de identidade. 

### <a name="load-data-with-polybase"></a>Carregar dados com o PolyBase
dados de tooload numa tabela e gerar uma chave de substituição, utilizando a identidade, criar a tabela de Olá e, em seguida, utilizar INSERT... SELECIONE ou INSIRA... VALORES tooperform Olá carga.

Olá exemplo seguinte realça padrão básico Olá:
 
```sql
--CREATE TABLE with IDENTITY
CREATE TABLE dbo.T1
(   C1 INT IDENTITY(1,1)
,   C2 VARCHAR(30)
)
WITH
(   DISTRIBUTION = HASH(C2)
,   CLUSTERED COLUMNSTORE INDEX
)
;

--Use INSERT..SELECT toopopulate hello table from an external table
INSERT INTO dbo.T1
(C2)
SELECT  C2
FROM    ext.T1
;

SELECT  *
FROM    dbo.T1
;

DBCC PDW_SHOWSPACEUSED('dbo.T1');
```

> [!NOTE] 
> Não é possível toouse `CREATE TABLE AS SELECT` atualmente ao carregar dados para uma tabela com uma coluna de identidade.
> 

Para mais informações sobre como carregar dados utilizando a ferramenta do programa (BCP) de cópia em massa Olá, consulte Olá seguintes artigos:

- [Carregar com o PolyBase][]
- [O PolyBase melhores práticas][]

### <a name="load-data-with-bcp"></a>Carregar dados com o BCP
BCP é uma ferramenta da linha de comandos que pode utilizar dados tooload para o SQL Data Warehouse. Um dos respetivos parâmetros (-I) controlos Olá comportamento do BCP ao carregar dados para uma tabela com uma coluna de identidade. 

Quando é especificado -I, valores Olá contidos no ficheiro de entrada Olá para a coluna de Olá com a identidade são retidos. Se for -I *não* especificado, em seguida, são ignorados valores Olá nesta coluna. Se a coluna de identidade Olá não estiver incluída, em seguida, Olá os dados são carregados como normal. valores de Olá são gerados de acordo com a política incremento e seed toohello da propriedade Olá.

Para mais informações sobre como carregar dados utilizando o BCP, consulte Olá seguintes artigos:

- [Carregar com o BCP][]
- [BCP no MSDN][]

## <a name="catalog-views"></a>Vistas de catálogo
Armazém de dados SQL suporta Olá `sys.identity_columns` vista de catálogo. Esta vista pode ser utilizado tooidentify uma coluna que tem a propriedade de identidade Olá.

toohelp compreender melhor o esquema de base de dados de Olá, este exemplo mostra como toointegrate `sys.identity_columns` com outras vistas de catálogo de sistema:

```sql
SELECT  sm.name
,       tb.name
,       co.name
,       CASE WHEN ic.column_id IS NOT NULL
             THEN 1
        ELSE 0
        END AS is_identity 
FROM        sys.schemas AS sm
JOIN        sys.tables  AS tb           ON  sm.schema_id = tb.schema_id
JOIN        sys.columns AS co           ON  tb.object_id = co.object_id
LEFT JOIN   sys.identity_columns AS ic  ON  co.object_id = ic.object_id
                                        AND co.column_id = ic.column_id
WHERE   sm.name = 'dbo'
AND     tb.name = 'T1'
;
```

## <a name="limitations"></a>Limitações
Não é possível utilizar Olá propriedade de identidade Olá os seguintes cenários:
- Em que tipo de dados da coluna de Olá não é INT ou BIGINT
- Em que a coluna de Olá também é Olá de distribuição de chaves
- Em que a tabela de Olá é uma tabela externa 

Olá funções relacionadas com os seguintes não é suportado no armazém de dados do SQL Server:

- [IDENTITY()][]
- [@@IDENTITY][]
- [SCOPE_IDENTITY][]
- [IDENT_CURRENT][]
- [IDENT_INCR][]
- [IDENT_SEED][]
- [DBCC CHECK_IDENT()][]

## <a name="tasks"></a>Tarefas

Esta secção fornece algum código de exemplo pode utilizar tarefas comuns tooperform quando trabalha com colunas de identidade.

> [!NOTE] 
> C1 de coluna é Olá identidade no Olá todas as seguintes tarefas.
> 
 
### <a name="find-hello-highest-allocated-value-for-a-table"></a>Localizar o valor mais elevado de Olá alocado para uma tabela
Olá utilize `MAX()` função de valor de mais alto de toodetermine Olá atribuído a uma tabela distribuída:

```sql
SELECT  MAX(C1)
FROM    dbo.T1
``` 

### <a name="find-hello-seed-and-increment-for-hello-identity-property"></a>Localizar Olá seed e incrementação maiores para Olá propriedade de identidade
Pode utilizar Olá catálogo vistas toodiscover Olá identidade incremento e seed valores de configuração para uma tabela utilizando Olá seguinte consulta: 

```sql
SELECT  sm.name
,       tb.name
,       co.name
,       ic.seed_value
,       ic.increment_value 
FROM        sys.schemas AS sm
JOIN        sys.tables  AS tb           ON  sm.schema_id = tb.schema_id
JOIN        sys.columns AS co           ON  tb.object_id = co.object_id
JOIN        sys.identity_columns AS ic  ON  co.object_id = ic.object_id
                                        AND co.column_id = ic.column_id
WHERE   sm.name = 'dbo'
AND     tb.name = 'T1'
;
```

## <a name="next-steps"></a>Passos seguintes

* toolearn mais informações sobre desenvolver as tabelas, consulte [descrição geral da tabela][Overview], [tipos de dados de tabela][Data Types], [distribuir uma tabela] [ Distribute], [Uma tabela de índice][Index], [uma tabela de partição][Partition], e [ Tabelas temporárias][Temporary]. 
* Para obter mais informações sobre as melhores práticas, consulte [melhores práticas do SQL Data Warehouse][SQL Data Warehouse Best Practices].  

<!--Image references-->

<!--Article references-->
[Overview]: ./sql-data-warehouse-tables-overview.md
[Data Types]: ./sql-data-warehouse-tables-data-types.md
[Distribute]: ./sql-data-warehouse-tables-distribute.md
[Index]: ./sql-data-warehouse-tables-index.md
[Partition]: ./sql-data-warehouse-tables-partition.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md
[Temporary]: ./sql-data-warehouse-tables-temporary.md
[Identity]: ./sql-data-warehouse-tables-identity.md
[SQL Data Warehouse Best Practices]: ./sql-data-warehouse-best-practices.md

[Carregar com o bcp]: https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-load-with-bcp/
[Carregar com o PolyBase]: https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-load-from-azure-blob-storage-with-polybase/
[O PolyBase melhores práticas]: https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-load-polybase-guide/


<!--MSDN references-->
[Identity property]: https://msdn.microsoft.com/library/ms186775.aspx
[sys.identity_columns]: https://msdn.microsoft.com/library/ms187334.aspx
[IDENTITY()]: https://msdn.microsoft.com/library/ms189838.aspx
[@@IDENTITY]: https://msdn.microsoft.com/library/ms187342.aspx
[SCOPE_IDENTITY]: https://msdn.microsoft.com/library/ms190315.aspx
[IDENT_CURRENT]: https://msdn.microsoft.com/library/ms175098.aspx
[IDENT_INCR]: https://msdn.microsoft.com/library/ms189795.aspx
[IDENT_SEED]: https://msdn.microsoft.com/library/ms189834.aspx
[DBCC CHECK_IDENT()]: https://msdn.microsoft.com/library/ms176057.aspx

[BCP no MSDN]: https://msdn.microsoft.com/library/ms162802.aspx
  

<!--Other Web references-->  
