---
title: "desempenho de base de dados SQL aaaAzure otimização orientações | Microsoft Docs"
description: "Este artigo pode ajudá-lo a determinar qual toochoose de camada de serviço para a sua aplicação. Também recomenda formas tootune Olá de tooget a aplicação mais da SQL Database do Azure."
services: sql-database
documentationcenter: na
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: dd8d95fa-24b2-4233-b3f1-8e8952a7a22b
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 02/09/2017
ms.author: carlrab
ms.openlocfilehash: 2699f755391e94ab488ac1e6acedd30f8aec4488
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tuning-performance-in-azure-sql-database"></a>Otimização de desempenho na SQL Database do Azure

Base de dados SQL do Azure fornece [recomendações](sql-database-advisor.md) que pode utilizar tooimprove desempenho da base de dados, ou pode deixar a base de dados do Azure SQL [automaticamente adaptar tooyour aplicação](sql-database-automatic-tuning.md) e aplicar as alterações que irá melhorar o desempenho da sua carga de trabalho.

Em não tem recomendações aplicáveis e continuará a ter problemas de desempenho, poderá utilizar Olá seguir os desempenhos de tooimprove métodos:
1. Aumentar [escalões de serviço](sql-database-service-tiers.md) e fornecer mais recursos tooyour da base de dados.
2. Otimizar a sua aplicação e aplicam-se algumas melhores práticas que podem melhorar o desempenho. 
3. Otimize a base de dados de Olá alterando índices e consultas toomore eficientemente trabalhar com dados.

Estes são os métodos manuais porque necessita de toodecide que [escalões de serviço](sql-database-service-tiers.md) deverá escolher ou seria necessário toorewrite aplicação ou código base de dados e deply alterações Olá.

## <a name="increasing-performance-tier-of-your-database"></a>Aumentar a camada de desempenho da base de dados

Base de dados SQL do Azure oferece quatro [escalões de serviço](sql-database-service-tiers.md) que pode escolher entre: básicas, Standard, Premium e Premium RS (desempenho é medido em unidades de débito de base de dados, ou [DTUs](sql-database-what-is-a-dtu.md). Cada escalão de serviço estritamente isola recursos Olá que pode utilizar a base de dados do SQL Server e garante o desempenho previsível que nível de serviço. Neste artigo, vamos oferecem orientações que podem ajudar a escolher a camada de serviço Olá para a sua aplicação. Vamos discutir também formas que pode otimizar o seu Olá tooget de aplicação mais da SQL Database do Azure.

> [!NOTE]
> Este artigo incida no guia de desempenho das bases de dados na base de dados do Azure SQL. Para obter orientações de desempenho relacionados tooelastic agrupamentos, consulte [considerações sobre preço e desempenho para conjuntos elásticos](sql-database-elastic-pool-guidance.md). Tenha em atenção, no entanto, pode aplicar muitas das recomendações toodatabases este artigo num agrupamento elástico de otimização de Olá e obter os benefícios de desempenho semelhante.
> 

* **Básico**: Olá serviço básico camada oferece um bom desempenho à previsibilidade para cada base de dados, de hora mais de hora. Numa base de dados básica, recursos suficientes suportam um bom desempenho na base de dados pequena que não tem vários pedidos em simultâneo. Casos de utilização típica quando deverá utilizar o escalão de serviço básico são:
  * **Apenas começar a utilizar com a SQL Database do Azure**. As aplicações que estão em desenvolvimento, muitas vezes, não precisam de níveis de elevado desempenho. Bases de dados básicas são um ambiente ideal para o desenvolvimento de base de dados ou de teste, num ponto de preços baixa.
  * **Tiver uma base de dados com um único utilizador**. As aplicações que associa um utilizador único uma base de dados, normalmente, não tem requisitos de concorrência e desempenho elevados. Estas aplicações são candidatos para a camada de serviço básico Olá.
* **Standard**: camada de serviço Standard Olá oferece desempenho melhorado previsão e fornece um bom desempenho para bases de dados que tenham vários pedidos simultâneos, como o grupo de trabalho e aplicações web. Ao escolher uma base de dados de camada de serviço Standard, tamanho da aplicação de base de dados com base no desempenho previsível, minuto minutos.
  * **A base de dados tem vários pedidos simultâneos**. Aplicações de serviço mais do que um utilizador num momento normalmente têm níveis de desempenho superiores. Por exemplo, aplicações web ou de grupo de trabalho que têm requisitos de tráfego de e/s de toomedium baixa suportando várias consultas em simultâneo são bons candidatos para a camada de serviço Standard Olá.
* **Premium**: camada de serviço Premium Olá disponibiliza desempenho previsível, segundo por segundo, para cada base de dados Premium. Quando escolher o escalão de serviço Premium Olá, pode dimensione a sua aplicação de base de dados com base no Olá pico de carga para a base de dados. plano de Olá remove casos em que a variância de desempenho pode causar tootake consultas pequeno maior do que esperado nas operações de sensíveis à latência. Este modelo pode simplificar bastante a ciclos de validação de desenvolvimento e produto Olá para aplicações que precisem toomake instruções forte sobre necessidades de recursos de pico, a variância de desempenho ou a latência de consulta. A maioria dos casos de utilização do escalão de serviço de Premium têm um ou mais destas características:
  * **Elevada pico de carga**. Uma aplicação que requer substancial CPU, memória ou entrada/saída (e/s) toocomplete as suas operações requer um nível dedicado e de elevado desempenho. Por exemplo, uma operação de base de dados conhecido tooconsume vários núcleos de CPU para um período de tempo alargado é uma candidata para a camada de serviço Premium Olá.
  * **Demasiados pedidos simultâneos**. Algumas aplicações de base de dados serviço demasiados pedidos simultâneos, por exemplo, quando a servir um Web site que tem um volume de tráfego elevado. Básico e padrão escalões de serviço limitam o número de Olá de pedidos em simultâneo por base de dados. Aplicações que necessitam de mais ligações teria toochoose um reserva adequado tamanho toohandle Olá número máximo de pedidos necessários.
  * **Baixa latência**. Algumas aplicações precisam de tooguarantee uma resposta da base de dados de Olá no tempo mínimo. Se um procedimento armazenado específico denomina-se como parte de uma operação de cliente mais vasto, poderá ser necessário um requisito toohave partir desse chamada de retorno em mais do que 20 milissegundos, 99 por cento do tempo de Olá. Este tipo de beneficia de aplicação de camada de serviço Premium Olá, se que essa Olá necessárias informática energia toomake está disponível.
* **Premium RS**: Olá escalão Premium RS foi concebido para cargas de trabalho de e/s intensivas que não necessitam de Olá garantias de disponibilidade mais elevadas. Os exemplos incluem o teste de cargas de trabalho de elevado desempenho ou uma carga de trabalho analítica em que a base de dados de Olá não é sistema Olá de registo.

nível de serviço Olá que necessita para a base de dados do SQL Server depende de requisitos de carregamento de pico Olá para a dimensão de cada recurso. Algumas aplicações utilizam uma quantidade trivial de um único recurso, mas têm requisitos significativos para outros recursos.

### <a name="service-tier-capabilities-and-limits"></a>Capacidades de camada de serviço e limites

Em cada camada de serviço, definir nível de desempenho de Olá, pelo que terá de Olá flexibilidade toopay apenas para a capacidade de Olá que precisa. Pode [ajustar capacidade](sql-database-service-tiers.md), ou reduzir vertical, como as alterações de carga de trabalho. Por exemplo, se a carga de trabalho de base de dados se elevada durante a época de compras de back-escola Olá, pode aumentar o nível de desempenho de Olá da base de dados de Olá durante um período de tempo definido, Julho através de Setembro. Pode reduzir quando termina a época de pico. Pode minimizar paga por otimizar o seu sazonalidade de toohello de ambiente de nuvem da sua empresa. Este modelo também funciona bem para ciclos de versão de produto de software. Um agrupamento de teste poderá atribuir capacidade enquanto teste é executado e, em seguida, liberte essa capacidade quando terminarem de teste. Um modelo de pedido de capacidade, paga pelos capacidade à medida que precisa dele e evitar despesas em recursos dedicados que raramente poderá utilizar.

### <a name="why-service-tiers"></a>Por que motivo escalões de serviço?
Apesar de cada carga de trabalho de base de dados pode ser diferente, o objetivo Olá escalões de serviço é a previsão de desempenho de tooprovide em vários níveis de desempenho. Clientes com os requisitos de recursos de base de dados em grande escala, podem trabalhar num ambiente informático mais dedicado.

## <a name="tune-your-application"></a>Otimizar a sua aplicação
No tradicional no SQL Server local, processo de Olá de planeamento de capacidade inicial, muitas vezes, é separado do processo de Olá da execução de uma aplicação na produção. Produto de hardware e licenças adquiridas pela primeira vez, e a otimização de desempenho é efetuada posteriormente. Quando utilizar a SQL Database do Azure, é um processo de Olá toointerweave boa ideia de execução de uma aplicação e otimização-lo. Com o modelo de Olá de pagar capacidade a pedido, pode otimizar a sua aplicação toouse Olá mínimo recursos necessários agora, em vez de provocam um aprovisionamento no hardware baseiam guesses dos planos de crescimento futuro para uma aplicação, que frequentemente estão incorretos. Alguns clientes podem escolher não tootune uma aplicação e, em vez disso, escolha toooverprovision recursos de hardware. Esta abordagem poderá ser aconselhável se não quiser toochange uma aplicação chave durante um período ocupado. No entanto, a otimização de uma aplicação pode minimizar os requisitos de recursos e faturas mensais inferiores ao utilizar camadas de serviços de Olá na SQL Database do Azure.

### <a name="application-characteristics"></a>Características de aplicação
Embora os escalões de serviço do SQL Database do Azure são tooimprove concebida desempenho estabilidade e à previsibilidade para uma aplicação, algumas melhores práticas podem ajudá-lo a otimizar o tirar partido do aplicação toobetter dos recursos de Olá um nível de desempenho. Embora muitas aplicações tenham ganhos de desempenho significativas simplesmente por mudar tooa mais elevado nível de desempenho ou serviço da camada, alguns necessidade de aplicações adicionais otimização toobenefit de um nível mais elevado de serviço. Para um melhor desempenho, considere a otimização de aplicação adicional para aplicações que têm estas características:

* **As aplicações que têm um desempenho lento devido a "chatty" comportamento**. Aplicações chatty efetuar operações de acesso de dados excessivo destinadas a latência de toonetwork confidenciais. Poderá ser necessário toomodify estes tipos de aplicações tooreduce Olá diversas dados acesso operações toohello SQL da base de dados. Por exemplo, pode melhorar o desempenho da aplicação através da utilização de técnicas, como a criação de batches de consultas ad-hoc ou movendo Olá consulta toostored procedimentos. Para obter mais informações, consulte [Batch consultas](#batch-queries).
* **Bases de dados com uma carga de trabalho que consomem muita que não pode ser suportado por uma única máquina toda**. Bases de dados que excedam recursos Olá de nível de desempenho de Premium Olá mais elevado poderão beneficiar aumentar horizontalmente a carga de trabalho Olá. Para obter mais informações, consulte [fragmentação entre bases de dados](#cross-database-sharding) e [criação de partições funcionais](#functional-partitioning).
* **As aplicações que têm consultas inferior ao ideal –**. Aplicações, especialmente na camada de acesso de dados de Olá, mal ter otimizados consultas não poderão beneficiar de um nível de desempenho superior. Isto inclui consultas que não dispõem de uma cláusula WHERE, tem em falta índices ou tem desatualizada estatísticas. Estas aplicações beneficiam técnicas de otimização de desempenho de consulta padrão. Para obter mais informações, consulte [em falta índices](#identifying-and-adding-missing-indexes) e [consultar Otimização e hinting](#query-tuning-and-hinting).
* **Design de acesso a aplicações que tenham dados inferior ao ideal –**. As aplicações com problemas de simultaneidade de acesso de dados inerente, deadlocking por exemplo, não poderão beneficiar de um nível de desempenho superior. Considere a redução de ida e volta contra Olá SQL Database do Azure por dados de colocação em cache do lado do cliente de Olá com Olá serviço de colocação em cache do Azure ou outra tecnologia de colocação em cache. Consulte [colocação em cache de camada de aplicação](#application-tier-caching).

## <a name="tune-your-database"></a>Otimizar a base de dados
Nesta secção, vamos ver alguns técnicas que pode utilizar tootune SQL Database do Azure toogain Olá melhor desempenho para a sua aplicação e executá-lo ao nível de desempenho possíveis mais baixo Olá. Algumas destas técnicas correspondem tradicionais do SQL Server de otimização de melhores práticas, mas outros estão tooAzure específica da base de dados do SQL Server. Em alguns casos, pode examinar os recursos de Olá consumido para uma base de dados toofind áreas toofurther otimizar e expandir tradicional toowork de técnicas de SQL Server na SQL Database do Azure.

### <a name="identify-performance-issues-using-azure-portal"></a>Identificar problemas de desempenho através do portal do Azure
Olá ferramentas no portal do Azure de Olá os seguintes pode ajudar a analisar e corrigir problemas de desempenho com a base de dados do SQL Server:

* [Query Performance Insight](sql-database-query-performance.md)
* [Assistente da Base de Dados SQL](sql-database-advisor.md)

Olá portal do Azure tem mais informações sobre ambas estas ferramentas e como toouse-los. diagnosticar tooefficiently e problemas corretos, recomendamos que primeiro tente Olá as ferramentas do Olá portal do Azure. Recomendamos que utilize manual Olá otimização abordagens que discutimos a em seguida, em falta índices e otimizar a consulta, em casos especiais.

Encontrar mais informações sobre como identificar problemas na SQL Database do Azure no [monitorização do desempenho](sql-database-single-database-monitor.md) artigo.

### <a name="identifying-and-adding-missing-indexes"></a>Identificar e adicionar os índices em falta
Um problema comum no desempenho da base de dados OLTP relacionada com a estrutura de base de dados física toohello. Muitas vezes, esquemas de base de dados são concebidas e fornecidas sem as testar à escala (a carga ou no volume de dados). Infelizmente, desempenho Olá de um plano de consulta poderá ser aceitável em pequena escala, mas diminuir substancialmente em volumes de dados de nível de produção. origem mais comuns de Olá deste problema é a falta de Olá de filtros de toosatisfy índices adequado ou outras restrições numa consulta. Muitas vezes, falta de índices de manifestos como uma tabela de análise quando uma procura do índice foi suffice.

Neste exemplo, o plano de consulta selecionada Olá utiliza uma análise quando uma procura seria suffice:

    DROP TABLE dbo.missingindex;
    CREATE TABLE dbo.missingindex (col1 INT IDENTITY PRIMARY KEY, col2 INT);
    DECLARE @a int = 0;
    SET NOCOUNT ON;
    BEGIN TRANSACTION
    WHILE @a < 20000
    BEGIN
        INSERT INTO dbo.missingindex(col2) VALUES (@a);
        SET @a += 1;
    END
    COMMIT TRANSACTION;
    GO
    SELECT m1.col1
    FROM dbo.missingindex m1 INNER JOIN dbo.missingindex m2 ON(m1.col1=m2.col1)
    WHERE m1.col2 = 4;

![Um plano de consulta com índices em falta](./media/sql-database-performance-guidance/query_plan_missing_indexes.png)

Base de dados SQL do Azure pode ajudar a localizar e corrigir comuns em falta condições de índice. DMVs incorporadas em SQL Database do Azure observe compilações de consulta em que um índice seria reduzir significativamente Olá estimado custo toorun uma consulta. Durante a execução de consulta, base de dados SQL controla a frequência cada plano de consulta é executado e Olá controla estimado intervalo entre Olá ao executar o plano de consulta e Olá imagined um onde existia nesse índice. Pode utilizar estes estimado de tooquickly DMVs estrutura de base de dados física de tooyour que alterações poderá melhorar o custo de carga de trabalho geral para uma base de dados e a carga de trabalho real.

Pode utilizar este potencial problema tooevaluate de consulta em falta índices:

    SELECT CONVERT (varchar, getdate(), 126) AS runtime,
        mig.index_group_handle, mid.index_handle,
        CONVERT (decimal (28,1), migs.avg_total_user_cost * migs.avg_user_impact *
                (migs.user_seeks + migs.user_scans)) AS improvement_measure,
        'CREATE INDEX missing_index_' + CONVERT (varchar, mig.index_group_handle) + '_' +
                  CONVERT (varchar, mid.index_handle) + ' ON ' + mid.statement + '
                  (' + ISNULL (mid.equality_columns,'')
                  + CASE WHEN mid.equality_columns IS NOT NULL
                              AND mid.inequality_columns IS NOT NULL
                         THEN ',' ELSE '' END + ISNULL (mid.inequality_columns, '')
                  + ')'
                  + ISNULL (' INCLUDE (' + mid.included_columns + ')', '') AS create_index_statement,
        migs.*,
        mid.database_id,
        mid.[object_id]
    FROM sys.dm_db_missing_index_groups AS mig
    INNER JOIN sys.dm_db_missing_index_group_stats AS migs
        ON migs.group_handle = mig.index_group_handle
    INNER JOIN sys.dm_db_missing_index_details AS mid
        ON mig.index_handle = mid.index_handle
    ORDER BY migs.avg_total_user_cost * migs.avg_user_impact * (migs.user_seeks + migs.user_scans) DESC

Neste exemplo, a consulta de Olá resultou neste Sugestão:

    CREATE INDEX missing_index_5006_5005 ON [dbo].[missingindex] ([col2])  

Depois de criado, essa mesma instrução SELECT escolhe um plano diferente, que utiliza uma procura em vez de uma análise e, em seguida, executa a forma mais eficiente plano Olá:

![Um plano de consulta com índices corrigidos](./media/sql-database-performance-guidance/query_plan_corrected_indexes.png)

informações de chave Olá é essa Olá capacidade de e/s de um partilhado, sistema de mercadoria é mais limitado do que uma máquina de servidor dedicado. Há um premium na minimizando desnecessário e/s tootake máximo partido do sistema Olá no Olá DTU cada nível de desempenho das camadas de serviços Olá SQL Database do Azure. Opções de design de base de dados físico adequado podem significativamente melhorar a latência de Olá para consultas individuais, melhorar o débito de Olá de pedidos simultâneos processadas por unidade de escala e minimizar a consulta de Olá Olá custos toosatisfy necessária. Para mais informações sobre Olá em falta DMVs de índice, consulte [sys.dm_db_missing_index_details](https://msdn.microsoft.com/library/ms345434.aspx).

### <a name="query-tuning-and-hinting"></a>Otimização da consulta e hinting
o otimizador de consultas Olá na SQL Database do Azure é semelhante toohello tradicional do SQL Server otimizador de consultas. Na maioria das melhores práticas de Olá para otimizar as consultas e Olá compreender reasoning limitações de modelo para o otimizador de consultas Olá também se aplicam tooAzure base de dados SQL. Se a otimizar as consultas na base de dados do Azure SQL, poderá obter benefício adicional de Olá de reduzir as exigências do recurso agregado. A aplicação poderá ser capaz de toorun um custo mais baixo que equivalente untuned porque pode ser executado num nível de desempenho inferior.

Um exemplo comum no SQL Server e que também se aplica a tooAzure base de dados SQL é como o otimizador "interceta" parâmetros de consulta de Olá. Durante a compilação, otimizador de consultas Olá avalia o valor atual Olá toodetermine um parâmetro, se pode gerar um plano de consulta mais ideal. Embora muitas vezes, esta estratégia pode levar tooa o plano de consulta que é significativamente mais rápido do que um plano compilado sem os valores de parâmetros conhecido, atualmente funciona imperfectly ambos no SQL Server e no SQL Database do Azure. Por vezes, parâmetro Olá é intercetados não na e, por vezes, parâmetro Olá é intercetados na mas plano gerado Olá é inferior ao ideal para o conjunto completo de Olá de valores de parâmetros numa carga de trabalho. Microsoft inclui sugestões de consulta (diretivas) para que possa especificar intenção mais deliberadamente e substituir o comportamento predefinido de Olá de parâmetro de interceção. Muitas vezes, se utilizar sugestões, pode corrigir casos em que as comportamento Olá predefinido do SQL Server ou SQL Database do Azure é imperfect para uma carga de trabalho do cliente específico.

Exemplo Olá de seguinte demonstra como o processador de consultas Olá pode gerar um plano que é inferior ao ideal para desempenho e requisitos de recursos. Este exemplo mostra também a que se utilizar uma sugestão de consulta, pode reduzir os requisitos de recursos e tempo de execução da consulta da base de dados do SQL Server:

    DROP TABLE psptest1;
    CREATE TABLE psptest1(col1 int primary key identity, col2 int, col3 binary(200));

    DECLARE @a int = 0;
    SET NOCOUNT ON;
    BEGIN TRANSACTION
    WHILE @a < 20000
    BEGIN
        INSERT INTO psptest1(col2) values (1);
        INSERT INTO psptest1(col2) values (@a);
        SET @a += 1;
    END
    COMMIT TRANSACTION
    CREATE INDEX i1 on psptest1(col2);
    GO

    CREATE PROCEDURE psp1 (@param1 int)
    AS
    BEGIN
        INSERT INTO t1 SELECT * FROM psptest1
        WHERE col2 = @param1
        ORDER BY col2;
    END
    GO

    CREATE PROCEDURE psp2 (@param2 int)
    AS
    BEGIN
        INSERT INTO t1 SELECT * FROM psptest1 WHERE col2 = @param2
        ORDER BY col2
        OPTION (OPTIMIZE FOR (@param2 UNKNOWN))
    END
    GO

    CREATE TABLE t1 (col1 int primary key, col2 int, col3 binary(200));
    GO

código de configuração de Olá cria uma tabela que tem skewed a distribuição de dados. Olá consultas difere do plano com base na qual parâmetro está selecionado. Infelizmente, plano Olá comportamento de colocação em cache não sempre recompilar consulta Olá com base no valor de parâmetro Olá mais comuns. Por isso, é possível um toobe inferior ao ideal – plano em cache e utilizado para vários valores, mesmo quando um plano diferente pode ser uma melhor opção de plano em média. Em seguida, o plano de consulta Olá cria dois procedimentos armazenados que sejam idênticos, à exceção de um tem uma sugestão de consulta especiais.

**Exemplo, parte 1**

    -- Prime Procedure Cache with scan plan
    EXEC psp1 @param1=1;
    TRUNCATE TABLE t1;

    -- Iterate multiple times tooshow hello performance difference
    DECLARE @i int = 0;
    WHILE @i < 1000
    BEGIN
        EXEC psp1 @param1=2;
        TRUNCATE TABLE t1;
        SET @i += 1;
    END

**Exemplo, parte 2**

(Recomendamos que aguarde pelo menos 10 minutos antes de começar a parte 2 de exemplo de Olá, para que os resultados de Olá forem distintos em Olá resultante dados de telemetria.)

    EXEC psp2 @param2=1;
    TRUNCATE TABLE t1;

    DECLARE @i int = 0;
    WHILE @i < 1000
    BEGIN
        EXEC psp2 @param2=2;
        TRUNCATE TABLE t1;
        SET @i += 1;
    END

Cada parte deste exemplo tenta toorun uma instrução insert parametrizada 1.000 vezes (toogenerate um suficientes toouse de carga como um conjunto de dados de teste). Quando executa a procedimentos armazenados, o processador de consultas Olá examina o valor do parâmetro Olá que é transmitido toohello procedimento durante a respetiva compilação primeiro (parâmetro "de interceção"). processador Olá coloca em cache plano resultante Olá e utiliza-o para invocações posteriores, mesmo que o valor do parâmetro Olá é diferente. plano de ideal Olá não pode ser utilizado em todos os casos. Por vezes, precisa de tooguide Olá otimizador toopick um plano que é melhor para caso médio Olá em vez de caso específico Olá do quando Olá foi primeiro compilar a consulta. Neste exemplo, o plano inicial Olá gera um plano de "verificação", que lê todas as linhas toofind cada valor que corresponde ao parâmetro Olá:

![Consulta de otimização através da utilização de um plano de análise](./media/sql-database-performance-guidance/query_tuning_1.png)

Porque o procedimento de Olá é executada através da utilização de valor de Olá 1, o plano resultante Olá foi ideal para o valor de Olá 1 mas não foi inferior ao ideal para todos os outros valores na tabela de Olá. resultado de Olá provavelmente não é o que seria aconselhável se foram toopick cada planear aleatoriamente, porque o plano de Olá efetua mais lentamente e utiliza mais recursos.

Se executar o teste de Olá com `SET STATISTICS IO` definido demasiado`ON`, trabalho de análise lógica Olá neste exemplo é efetuado em segundo plano de Olá. Pode ver que existem 1,148 leituras efetuadas pelo plano de Olá (que é ineficaz se caso médio Olá tooreturn apenas linha):

![Consulta de otimização, utilizando uma análise lógica](./media/sql-database-performance-guidance/query_tuning_2.png)

Olá segunda parte exemplo Olá utiliza uma consulta sugestão tootell Olá otimizador toouse um valor específico durante o processo de compilação de Olá. Neste caso, força-Olá processador tooignore Olá valor de consulta que é transmitido como parâmetro Olá, e, em vez disso, tooassume `UNKNOWN`. Isto refere-se o valor de tooa com frequência médio Olá na tabela de Olá (ignorando o desfasamento). plano de Olá resultante é um plano de com base na procura de mensagens em fila que é mais rápido e utiliza menos recursos, em média, Olá plano na parte 1 deste exemplo:

![Consulta de otimização, utilizando uma sugestão de consulta](./media/sql-database-performance-guidance/query_tuning_3.png)

Pode ver o efeito de Olá no Olá **resource_stats** tabela (há um atraso de tempo de Olá que executar o teste de Olá e quando os dados de Olá preenche tabela Olá). Para este exemplo, parte 1 executada durante a janela de tempo Olá 25:22:00 e a parte 2 executada às 22:35:00. Olá anterior janela de tempo utilizada mais recursos nessa janela de tempo que Olá posteriormente, um (devido a melhorias de eficiência de plano).

    SELECT TOP 1000 *
    FROM sys.resource_stats
    WHERE database_name = 'resource1'
    ORDER BY start_time DESC

![Consulta de otimização de resultados de exemplo](./media/sql-database-performance-guidance/query_tuning_4.png)

> [!NOTE]
> Embora seja intencionalmente pequeno volume Olá neste exemplo, efeito Olá dos parâmetros inferior ao ideal – pode ser significativo, especialmente nas bases de dados maiores. diferença Olá, em casos extremos, pode estar entre segundos para casos rápidos e horas para os casos lentas.
> 
> 

Pode examinar **resource_stats** toodetermine se recursos Olá para um teste utiliza mais ou menos recursos do que outro teste. Quando se comparam os dados, separe temporização Olá de testes para que não estão a ser Olá mesma janela de 5 minutos Olá **resource_stats** vista. Olá objetivo exercício Olá é toominimize quantidade total de Olá dos recursos utilizados e não toominimize Olá das horas de ponta aos recursos. Geralmente, otimizar um fragmento de código para latência também reduz o consumo de recursos. Certifique-se de que são necessárias alterações de Olá efetuadas tooan aplicação e que as alterações de Olá negativamente não afetam a experiência do cliente Olá para alguém que possam estar a utilizar sugestões de consulta na aplicação Olá.

Se uma carga de trabalho tem um conjunto de repetir consultas, muitas vezes, faz sentido toocapture e validar optimality Olá das opções do plano porque unidades de Olá mínima de recursos tamanho unidade toohost necessário Olá da base de dados. Depois de validá-lo, ocasionalmente reexamine planos Olá que toohelp, certificar-se que não tenham degradado. Pode saber mais sobre [consultar sugestões (Transact-SQL)](https://msdn.microsoft.com/library/ms181714.aspx).

### <a name="cross-database-sharding"></a>Fragmentação entre bases de dados
Porque a SQL Database do Azure é executado no hardware do produto, os limites de capacidade de Olá para uma base de dados são inferiores para uma instalação do SQL Server tradicional no local. Alguns clientes utilizam operações de base de dados de toospread de técnicas de fragmentação através de várias bases de dados quando as operações de Olá não cabem Olá limites de uma base de dados na base de dados do Azure SQL. A maioria dos clientes que utilizam técnicas de fragmentação na SQL Database do Azure dividir os seus dados numa única dimensão por várias bases de dados. Para que esta abordagem tem toounderstand que aplicações OLTP frequentemente efetuar transações que se aplicam tooonly uma linha ou tooa pequeno grupo de linhas do esquema de Olá.

> [!NOTE]
> Base de dados do SQL Server fornece agora tooassist uma biblioteca com fragmentação. Para obter mais informações, consulte [descrição geral da biblioteca de cliente da linha de base de dados elástica](sql-database-elastic-database-client-library.md).
> 
> 

Por exemplo, se uma base de dados tiver o nome de cliente, a ordem e detalhes da encomenda (como Olá tradicionais de exemplo Northwind da base de dados que é fornecido com o SQL Server), foi dividir dados em várias bases de dados através do agrupamento de um cliente com Olá relacionadas com a ordem e os detalhes de ordem informações. Pode garantir que dados desse cliente Olá permanecem na base de dados individual. aplicação Olá seria dividir diferentes clientes por bases de dados, de forma eficaz propagando-se Olá carga em várias bases de dados. Com fragmentação, os clientes não só podem evitar limite de tamanho máximo da base de dados de Olá, mas a SQL Database do Azure também pode processar as cargas de trabalho significativamente maiores do que os limites de Olá dos níveis de desempenho diferentes Olá, desde que cada base de dados individuais se ajusta à sua DTU.

Apesar de fragmentação de base de dados não reduzir a capacidade do recurso agregado Olá para uma solução, é altamente eficaz em soluções muito grande que são distribuídas por várias bases de dados de suporte. Cada base de dados pode executar um desempenho diferentes nível toosupport muito grande, bases de dados "Efetivo" com requisitos de recursos elevados.

### <a name="functional-partitioning"></a>Criação de partições funcionais
Utilizadores do SQL Server, muitas vezes, combinam muitas funções de uma base de dados. Por exemplo, se uma aplicação tiver inventário de toomanage lógica para um arquivo, essa base de dados pode ter lógica associada inventário, controlar as ordens de compra, procedimentos armazenados e vistas indexadas ou materializadas que gerir relatórios do fim do mês. Esta técnica torna mais fácil tooadminister Olá base de dados de operações como a cópia de segurança, mas também requer toosize Olá hardware toohandle Olá pico de carga em todas as funções de uma aplicação.

Se utilizar uma arquitetura de escalamento horizontal na SQL Database do Azure, é uma boa ideia toosplit diferentes funções de uma aplicação em bases de dados diferentes. Ao utilizar esta técnica, cada aplicação dimensiona de forma independente. Como uma aplicação fica busier (e Olá a carga aumenta de base de dados de Olá), o administrador de Olá pode escolher níveis de desempenho independente para cada função na aplicação Olá. No limite Olá, com esta arquitetura, uma aplicação pode ser maior do que uma máquina de mercadoria único pode processar, porque a carga de Olá é distribuída por várias máquinas.

### <a name="batch-queries"></a>Consultas de batch
Para aplicações que acedam aos dados através da utilização de volume elevado, frequentes, consultar o ad hoc, uma quantidade substancial de tempo de resposta é gasto em comunicações de rede entre a camada da aplicação Olá e a camada de base de dados do Azure SQL Olá. Mesmo quando ambas Olá aplicação e a SQL Database do Azure estão em Olá mesmo centro de dados, latência de rede Olá entre Olá dois poderá ser magnified por um grande número de operações de acesso de dados. rede de Olá tooreduce arredondar viagens para dados de Olá operações de acesso, considere utilizar Olá opção tooeither batch Olá consultas ad hoc ou toocompile-las como procedimentos armazenados. Se o batch consultas ad hoc Olá, pode enviar várias consultas como um lote grande num tooAzure viagem única base de dados SQL. Se compilar consultas ad hoc num procedimento armazenado, pode conseguir Olá que mesmo resultar como se o lote de-los. Utilizar um procedimento armazenado também oferece Olá vantagem de aumentar as possibilidades de Olá de colocação em cache de planos de consulta Olá na SQL Database do Azure para poder utilizar Olá procedimento armazenado novamente.

Algumas aplicações são escrita intensivas. Por vezes, pode reduzir o Olá total e/s de carga numa base de dados, considerar como toobatch escreve em conjunto. Muitas vezes, isto é tão simple quanto utilizar transações explícitas em vez de transações de consolidação automática em lotes ad hoc e procedimentos armazenados. Para uma edição de avaliação de diferentes técnicas que pode utilizar, consulte [técnicas para aplicações de base de dados SQL do Azure de criação de batches](https://msdn.microsoft.com/library/windowsazure/dn132615.aspx). Testar o suas próprias carga de trabalho toofind Olá direita modelo para a criação de batches. Toounderstand se de que um modelo poderá ter de ser ligeiramente garante a consistência transacional diferentes. Localizar Olá direita carga de trabalho que minimiza a utilização de recursos requer localizar combinação certa de Olá de compromissos consistência e o desempenho.

### <a name="application-tier-caching"></a>Colocação em cache de camada de aplicação
Algumas aplicações de base de dados têm cargas de trabalho pesado de leitura. Colocação em cache camadas pode reduzir a carga de Olá na base de dados de Olá e, possivelmente, poderá reduzir toosupport necessário ao nível de Olá desempenho uma base de dados ao utilizar a SQL Database do Azure. Com [a Cache de Redis do Azure](https://azure.microsoft.com/services/cache/), se tiver uma carga de trabalho pesado de leitura, pode ler dados Olá uma vez (ou, talvez, uma vez por máquina de camada de aplicação, dependendo de como estiver configurado) e, em seguida, armazenar esses dados fora da sua base de dados do SQL Server. Esta é uma forma tooreduce da base de dados de carga (CPU e e/s de leitura), mas não existe um efeito em consistência transacional porque os dados de Olá a ser lidos a partir da cache de Olá poderão ser sincronizados com os dados de Olá na base de dados de Olá. Embora muitas aplicações algum nível de inconsistência é aceitável, que não é true para todas as cargas de trabalho. Deve compreender os requisitos da aplicação antes de implementar uma estratégia de colocação em cache de camada de aplicação.

## <a name="next-steps"></a>Passos seguintes
* Para obter mais informações sobre os escalões de serviço, consulte [opções de base de dados SQL e o desempenho](sql-database-service-tiers.md)
* Para obter mais informações sobre conjuntos elásticos, consulte [o que é um conjunto elástico do Azure?](sql-database-elastic-pool.md)
* Para obter informações sobre agrupamentos de desempenho e elásticos, consulte [quando tooconsider agrupamento elástico](sql-database-elastic-pool-guidance.md)

