---
title: "o nível de compatibilidade de aaaDatabase 130 - SQL Database do Azure | Microsoft Docs"
description: "Neste artigo, vamos explorar as vantagens de Olá da SQL Database do Azure a executar ao nível de compatibilidade 130 e tirar partido dos benefícios de Olá do novo otimizador de consultas Olá e consultar as funcionalidades do processador. Podemos também endereços Olá possíveis-efeitos secundários no desempenho das consultas Olá para aplicações de SQL Olá existentes."
services: sql-database
documentationcenter: 
author: alainlissoir
manager: jhubbard
editor: 
ms.assetid: 8619f90b-7516-46dc-9885-98429add0053
ms.service: sql-database
ms.custom: monitor & tune
ms.workload: data-management
ms.devlang: NA
ms.tgt_pltfrm: NA
ms.topic: article
ms.date: 08/08/2016
ms.author: alainl
ms.openlocfilehash: 25693c5f7b01405b7073fa7d4cc2833fbe125e2f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="improved-query-performance-with-compatibility-level-130-in-azure-sql-database"></a>Melhorada desempenho das consultas com 130 de nível de compatibilidade na SQL Database do Azure
Base de dados SQL do Azure está em execução transparente centenas de milhares de bases de dados em vários níveis de compatibilidade diferentes, preservando e guaranteeing versão correspondente do toohello de compatibilidade com versões anteriores de Olá do Microsoft SQL Server para todos os seus clientes!

Neste artigo, vamos explorar as vantagens de Olá da sua Databse de SQL do Azure a executar ao nível de compatibilidade 130 e tirar partido dos benefícios de Olá do novo otimizador de consultas Olá e consultar as funcionalidades do processador. Podemos também endereços Olá possíveis-efeitos secundários no desempenho das consultas Olá para aplicações de SQL Olá existentes.

Como um lembrete do histórico, alinhamento Olá dos níveis de compatibilidade do SQL Server versões toodefault são:

* 100: no SQL Server 2008 e o Azure SQL da base de dados V11.
* 110: no SQL Server 2012 e SQL do Azure da base de dados V11.
* 120: no SQL Server 2014 e SQL do Azure da base de dados V12.
* 130: no SQL Server 2016 e o Azure SQL da base de dados V12.

> [!IMPORTANT]
> A partir de **mid Junho de 2016**, na base de dados SQL do Azure, o nível de compatibilidade predefinido Olá será 130 em vez de 120 para **recém-criado** bases de dados.
> 
> Bases de dados criadas antes mid Junho de 2016 serão *não* afetadas e irão manter o respetivo nível de compatibilidade atual (100, 110 ou 120). As bases de dados migrados de SQL Database do Azure versão V11 tooV12 terão um nível de compatibilidade 110 ou 100. 
> 

## <a name="about-compatibility-level-130"></a>Sobre o nível de compatibilidade 130
Em primeiro lugar, se quiser tooknow Olá atual nível de compatibilidade da base de dados, execute Olá a seguinte instrução Transact-SQL.

```
SELECT compatibility_level
    FROM sys.databases
    WHERE name = '<YOUR DATABASE_NAME>’;
```


Antes desta alteração toolevel 130 acontece para **recentemente** criar bases de dados, vamos rever o que esta alteração é tudo através de alguns exemplos de consultas muito básica e ver como a qualquer pessoa pode beneficiar do mesmo.

O processamento da consulta em bases de dados relacionais pode ser muito complexo e pode levar toolots de computador ciência e mathematics toounderstand Olá inerente opções de design e comportamentos. Neste documento, o conteúdo de Olá foi intencionalmente simplificada tooensure que qualquer pessoa com algum conhecimento técnico mínimo compreender Olá impacto da alteração de nível de compatibilidade de Olá e determinar como beneficiar aplicações.

Vamos ter ver rapidamente o nível de compatibilidade de Olá 130 coloca na tabela de Olá.  Pode encontrar mais detalhes em [ALTER a nível de compatibilidade da base de dados (Transact-SQL)](https://msdn.microsoft.com/library/bb510680.aspx), mas Eis um breve resumo:

* Olá a operação de inserção de uma instrução Insert select pode ser multi-thread ou pode ter um plano paralelo, enquanto que antes desta operação foi single-threaded.
* Memória Optimized tabela e consultas de variáveis de tabela podem agora tem planos paralelos, enquanto que antes desta operação foi também single-threaded.
* Estatísticas para a tabela com otimização de memória agora podem ser convertidas e são atualizados automaticamente. Consulte [Novidades no motor de base de dados: OLTP na memória](https://msdn.microsoft.com/library/bb510411.aspx#InMemory) para obter mais detalhes.
* Modo de batch v/s modo linha alterações com os índices de arquivo de colunas
  * Ordena numa tabela com um índice de arquivo de coluna está agora em modo batch.
  * Os agregados de modos de janela agora operam em modo de lote, tais como as declarações de desfasamento de TSQL/oportunidades potenciais.
  * As consultas em tabelas de arquivo de colunas com múltiplas cláusulas distintas operam em modo de Batch.
  * As consultas em execução em DOP = 1 ou com um plano de série também de ser executado no modo de Batch.
* Melhoramentos de estimativa de cardinalidade realmente vêm com o nível de compatibilidade 120, mas os de que a ser executado numa compatibilidade inferior ao nível (ou seja, 100, ou 110), hello mover toocompatibility nível 130 será também apresentada estas melhorias e estes também podem pela última vez, beneficiar desempenho das consultas Olá das suas aplicações.

## <a name="practicing-compatibility-level-130"></a>Nível de compatibilidade practicing 130
Primeiro vamos obter algumas tabelas, índices e dados aleatórios criados toopractice algumas destas novas capacidades. Exemplos de script TSQL Olá podem ser executados com o SQL Server 2016 ou na SQL Database do Azure. No entanto, quando criar uma base de dados SQL do Azure, certifique-se que escolha no Olá mínimo um P2 da base de dados porque necessita de, pelo menos, duas núcleos tooallow vários segmentos e beneficiar, por conseguinte, estas funcionalidades.

```
-- Create a Premium P2 Database in Azure SQL Database

CREATE DATABASE MyTestDB
    (EDITION=’Premium’, SERVICE_OBJECTIVE=’P2′);
GO

-- Create 2 tables with a column store index on
-- hello second one (only available on Premium databases)

CREATE TABLE T_source
    (Color varchar(10), c1 bigint, c2 bigint);

CREATE TABLE T_target
    (c1 bigint, c2 bigint);

CREATE CLUSTERED COLUMNSTORE INDEX CCI ON T_target;
GO

-- Insert few rows.

INSERT T_source VALUES
    (‘Blue’, RAND() * 100000, RAND() * 100000),
    (‘Yellow’, RAND() * 100000, RAND() * 100000),
    (‘Red’, RAND() * 100000, RAND() * 100000),
    (‘Green’, RAND() * 100000, RAND() * 100000),
    (‘Black’, RAND() * 100000, RAND() * 100000);

GO 200

INSERT T_source SELECT * FROM T_source;

GO 10
```


Agora, vamos tem um toosome aspeto das funcionalidades de consulta de processamento de Olá vem com um nível de compatibilidade 130.

## <a name="parallel-insert"></a>INSERT paralela
Executar Olá TSQL as instruções abaixo executa Olá a operação de inserção em nível de compatibilidade 120 e 130, que executa respetivamente Olá a operação de inserção de um modelo de threading único (120) e de um modelo com vários threads (130).

```
-- Parallel INSERT … SELECT … in heap or CCI
-- is available under 130 only

SET STATISTICS XML ON;

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 120;
GO 

-- hello INSERT part is in serial

INSERT t_target WITH (tablock)
    SELECT C1, COUNT(C2) * 10 * RAND()
        FROM T_source
        GROUP BY C1
    OPTION (RECOMPILE);

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 130
GO

-- hello INSERT part is in parallel

INSERT t_target WITH (tablock)
    SELECT C1, COUNT(C2) * 10 * RAND()
        FROM T_source
        GROUP BY C1
    OPTION (RECOMPILE);

SET STATISTICS XML OFF;
```


Ao solicitar o plano de consulta de Olá real Olá, observar a representação gráfica ou o respetivo conteúdo XML, pode determinar que estimativa de cardinalidade função é na play. Observar Olá planos do lado do lado a lado na figura 1, pode claramente, Vemos que Olá inserir do arquivo de colunas execução fica da série em 120 tooparallel no 130. Além disso, tenha em atenção que alteração Olá do ícone de iterator Olá no plano 130 Olá dois setas paralelas, que mostra que ilustra o facto de Olá agora Olá execução iterator é realmente paralela. Se tiver um grande toocomplete de operações de inserção, execução paralela de Olá, toohello ligado número de núcleos que tem na sua disposal da base de dados de Olá, terão um desempenho superior; cópia de segurança tooa 100 vezes mais rápida consoante a sua situação!

*Figura 1: Inserir alterações de operação de série tooparallel com um nível de compatibilidade 130.*

![Figura 1](./media/sql-database-compatibility-level-query-performance-130/figure-1.jpg)

## <a name="serial-batch-mode"></a>Modo de Batch de série
Da mesma forma, mover toocompatibility nível 130 durante o processamento de linhas de dados permite o processamento de modo de batch. Em primeiro lugar, as operações de modo de lote só estão disponíveis quando tem um índice de arquivo de colunas no local. Segundo, um lote normalmente representa ~ 900 linhas e utiliza uma lógica de código otimizada para a CPU especializada, débito de memória superior e diretamente tira partido Olá dados comprimidos de Olá coluna arquivo sempre que possível. Nas seguintes condições, SQL Server 2016 pode processar ~ 900 linhas de uma só vez, em vez de 1 linha momento Olá, e como consequence, hello custo global gerais da operação de Olá é agora partilhado por lote inteiro Olá, reduzindo Olá geral custo por linha. Esta quantidade partilhada operações combinado com compressão de arquivo de colunas de Olá basicamente reduz a latência de Olá envolvida numa operação batch SELECIONE modo. Pode encontrar mais detalhes acerca do arquivo de colunas de Olá e lote modo em [guia de índices Columnstore](https://msdn.microsoft.com/library/gg492088.aspx).

```
-- Serial batch mode execution

SET STATISTICS XML ON;

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 120;
GO

-- hello scan and aggregate are in row mode

SELECT C1, COUNT (C2)
    FROM T_target
    GROUP BY C1
    OPTION (MAXDOP 1, RECOMPILE);
GO

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 130;
GO 

-- hello scan and aggregate are in batch mode,
-- and force MAXDOP too1 tooshow that batch mode
-- also now works in serial mode.

SELECT C1, COUNT(C2)
    FROM T_target
    GROUP BY C1
    OPTION (MAXDOP 1, RECOMPILE);
GO

SET STATISTICS XML OFF;
```


Como visível abaixo, ao observar Olá consulta planos do lado do lado a lado na figura 2, é possível ver que o modo de processamento de Olá foi alterada com um nível de compatibilidade de Olá, e como consequence, quando executar consultas Olá completamente em ambos os nível de compatibilidade, é possível ver que a maioria do tempo de processamento de Olá é despendido no modo de (86%) em comparação com toohello batch modo linha (14%), onde 2 lotes foram processados. Aumentar o conjunto de dados de Olá, hello benefício irá aumentar.

*Figura 2: SELECIONE as alterações de operação do modo de toobatch série com o nível de compatibilidade 130.*

![Figura 2](./media/sql-database-compatibility-level-query-performance-130/figure-2.jpg)

## <a name="batch-mode-on-sort-execution"></a>Modo de batch na execução de ordenação
Transição de Olá toohello semelhante acima, mas a operação de ordenação tooa aplicados, do modo de toobatch linha modo (nível de compatibilidade 120) (nível de compatibilidade 130) melhora o desempenho de Olá de Olá operação de ordenação para Olá as mesmas razões.

```
-- Batch mode on sort execution

SET STATISTICS XML ON;

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 120;
GO

-- hello scan and aggregate are in row mode

SELECT C1, COUNT(C2)
    FROM T_target
    GROUP BY C1
    ORDER BY C1
    OPTION (MAXDOP 1, RECOMPILE);
GO

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 130;
GO

-- hello scan and aggregate are in batch mode,
-- and force MAXDOP too1 tooshow that batch mode
-- also now works in serial mode.

SELECT C1, COUNT(C2)
    FROM T_target
    GROUP BY C1
    ORDER BY C1
    OPTION (MAXDOP 1, RECOMPILE);
GO

SET STATISTICS XML OFF;
```


Visível do lado do lado a lado na figura 3, é possível ver que a operação de ordenação Olá no modo linha representa 81% de Olá custo, enquanto o modo de batch de Olá representa apenas % 19 de custo de Olá (respetivamente 81% e % de 56 na ordenação Olá próprio).

*Figura 3: A operação de ordenação alterações do modo de toobatch linha com o nível de compatibilidade 130.*

![Figura 3](./media/sql-database-compatibility-level-query-performance-130/figure-3.png)

Obviamente, estes exemplos só contenham dezenas de milhares de linhas, que é nothing quando observar os dados de Olá disponíveis na maioria dos SQL Servers estes dias. Apenas projeto estes contra milhões de linhas em vez disso, e isto pode traduzir em vários minutos de execução spared diariamente pendentes natureza Olá a carga de trabalho.

## <a name="cardinality-estimation-ce-improvements"></a>Melhoramentos de estimativa (CE) de cardinalidade
Introduzida com o SQL Server 2014, qualquer base de dados com um nível de compatibilidade 120 ou acima fará com que utilize das novas funcionalidades de estimativa de cardinalidade Olá. Essencialmente, estimativa de cardinalidade é lógica Olá utilizado toodetermine como o SQL server irá executar uma consulta com base na respetivo custo estimado. estimativa de Olá é calculada utilizando a entrada de estatísticas associadas a objetos envolvidos nessa consulta. Praticamente, um nível elevado, as funções de estimativa de cardinalidade são estimativas de contagem de linha, juntamente com informações sobre a distribuição de Olá dos valores de Olá, contagens de valor distintos, e contagens duplicadas contidas no Olá tabelas e os objetos referenciados na consulta de Olá. Obter estas estimativas incorreto, pode levar a e/s de disco de toounnecessary devido tooinsufficient concede de memória (ou seja, TempDB spills) ou tooa seleção de uma execução de série de plano através de um paralelo planear execução, tooname algumas. Conclusão, estimativas incorretas podem levar tooan degradação do desempenho global de execução da consulta Olá. No Olá outro lado, melhor calcula, estimativas mais exatas, execuções de consulta de toobetter de clientes potenciais clientes potenciais!

Tal como mencionado anteriormente, otimizações de consulta e calcula é um fim complexa, mas se pretender toolearn mais sobre os planos de consulta e o avaliador de cardinalidade herdado, pode consultar toohello documento no [otimizar o seu planos de consulta com Olá SQL Server 2014 Avaliador de cardinalidade herdado](https://msdn.microsoft.com/library/dn673537.aspx) para uma descrição mais aprofundada.

## <a name="which-cardinality-estimation-do-you-currently-use"></a>Que estimativa de cardinalidade atualmente utiliza?
toodetermine em que estimativa de cardinalidade as suas consultas estão em execução, vamos apenas utilizar consulta de Olá exemplos abaixo. Tenha em atenção que este primeiro exemplo serão executados com nível de compatibilidade 110, implying utilize Olá de funções de estimativa de cardinalidade antigas Olá.

```
-- Old CE

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 110;
GO

SET STATISTICS XML ON;

SELECT [c1]
    FROM [dbo].[T_target]
    WHERE [c1] > 20000;
GO

SET STATISTICS XML OFF;
```


Após a conclusão da execução, clique na ligação XML Olá e observe Olá as propriedades da iterator primeiro Olá, conforme mostrado abaixo. Tenha em atenção o nome da propriedade Olá chamado CardinalityEstimationModelVersion atualmente definido na 70. Não significa que o nível de compatibilidade de base de dados de Olá está definido a versão do SQL Server 7.0 toohello (está definido no 110 como visíveis nas instruções de TSQL Olá acima), mas o valor de Olá 70 simplesmente representa Olá legada estimativa de cardinalidade funcionalidade disponível desde o SQL Server Servidor 7.0, que não tinha nenhum revisões principais até que o SQL Server 2014 (vem com um nível de compatibilidade de 120).

*Figura 4: Olá CardinalityEstimationModelVersion é definir too70 quando um nível de compatibilidade 110 ou abaixo.*

![Figura 4](./media/sql-database-compatibility-level-query-performance-130/figure-4.png)

Em alternativa, pode alterar too130 de nível de compatibilidade de Olá e desativar a utilização de Olá da nova função de estimativa de cardinalidade Olá utilizando Olá LEGACY_CARDINALITY_ESTIMATION definir tooON com [ALTER configuração base de dados no âmbito](https://msdn.microsoft.com/library/mt629158.aspx). Isto irá ser exatamente Olá igual ao utilizar 110 uma estimativa de cardinalidade função ponto de vista de durante a utilização de consulta mais recente Olá processar o nível de compatibilidade. Ao fazê-lo, pode beneficiar da nova consulta de Olá processamento funcionalidades futuras com um nível de compatibilidade mais recente do hello (ou seja, modo de lote), mas ainda dependem da funcionalidade de estimativa de cardinalidade antiga Olá se necessário.

```
-- Old CE

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 130;
GO

ALTER DATABASE
    SCOPED CONFIGURATION
    SET LEGACY_CARDINALITY_ESTIMATION = ON;
GO

SET STATISTICS XML ON;

SELECT [c1]
    FROM [dbo].[T_target]
    WHERE [c1] > 20000;
GO

SET STATISTICS XML OFF;
```


Mover apenas o nível de compatibilidade de toohello 120 ou 130 ativa a funcionalidade de estimativa de cardinalidade novo Olá. Nesse caso, a predefinição de Olá CardinalityEstimationModelVersion será definida em conformidade too120 ou 130 visível como abaixo.

```
-- New CE

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 130;
GO

ALTER DATABASE
    SCOPED CONFIGURATION
    SET LEGACY_CARDINALITY_ESTIMATION = OFF;
GO

SET STATISTICS XML ON;

SELECT [c1]
    FROM [dbo].[T_target]
    WHERE [c1] > 20000;
GO

SET STATISTICS XML OFF;
```


*Figura 5: Olá CardinalityEstimationModelVersion é definir too130 quando um nível de compatibilidade de 130.*

![figura 5](./media/sql-database-compatibility-level-query-performance-130/figure-5.jpg)

## <a name="witnessing-hello-cardinality-estimation-differences"></a>Diferenças de estimativa de cardinalidade Olá witnessing
Agora, vamos executar ligeiramente mais complexo que envolvem um INNER JOIN com uma cláusula WHERE com algumas predicados de consulta e vamos ver estimativa de contagem de linhas Olá da função de estimativa de cardinalidade antiga Olá primeiro.

```
-- Old CE row estimate with INNER JOIN and WHERE clause

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 130;
GO

ALTER DATABASE
    SCOPED CONFIGURATION
    SET LEGACY_CARDINALITY_ESTIMATION = ON;
GO

SET STATISTICS XML ON;

SELECT T.[c2]
    FROM
                   [dbo].[T_source] S
        INNER JOIN [dbo].[T_target] T  ON T.c1=S.c1
    WHERE
        S.[Color] = ‘Red’  AND
        S.[c2] > 2000  AND
        T.[c2] > 2000
    OPTION (RECOMPILE);
GO

SET STATISTICS XML OFF;
```


Executar esta consulta eficazmente devolve 200,704 linhas, enquanto Olá estimativa de linha com a funcionalidade de estimativa de cardinalidade antiga Olá afirmações 194,284 linhas. Obviamente, como consiga aceder tal antes, esses resultados de contagem de linhas também dependerá frequência executou Olá exemplos anteriores, que preenche as tabelas de exemplo de Olá repetidas em cada execução. Obviamente, predicados Olá na sua consulta também irão ter uma influência no estimativa real de Olá além de forma de tabela Olá, conteúdo de dados e como estes dados, na verdade, correlacionar entre si.

*Figura 6: estimativa de contagem de linhas Olá está 194,284 ou 6.000 linhas desativada de Olá 200,704 as linhas esperadas.*

![figura 6](./media/sql-database-compatibility-level-query-performance-130/figure-6.jpg)

No Olá mesma forma, vamos executar agora Olá mesmo consultar com a nova funcionalidade de estimativa de cardinalidade Olá.

```
-- New CE row estimate with INNER JOIN and WHERE clause

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 130;
GO

ALTER DATABASE
    SCOPED CONFIGURATION
    SET LEGACY_CARDINALITY_ESTIMATION = OFF;
GO

SET STATISTICS XML ON;

SELECT T.[c2]
    FROM
                   [dbo].[T_source] S
        INNER JOIN [dbo].[T_target] T  ON T.c1=S.c1
    WHERE
        S.[Color] = ‘Red’  AND
        S.[c2] > 2000  AND
        T.[c2] > 2000
    OPTION (RECOMPILE);
GO

SET STATISTICS XML OFF;
```


Observar Olá abaixo, agora, Vemos que estimativa de linha de Olá é 202,877, ou muito próximo e superior ao hello estimativa de cardinalidade antigo.

*A figura 7: estimativa de contagem de linhas Olá está agora 202,877, em vez de 194,284.*

![figura 7](./media/sql-database-compatibility-level-query-performance-130/figure-7.jpg)

Na realidade, o conjunto de resultados de Olá é 200,704 linhas (mas todos depende da frequência executou consultas Olá de Olá exemplos anteriores, mas mais importante ainda, porque Olá TSQL utiliza a instrução de RAND() Olá, Olá real os valores devolvidos podem diferir dos de um toohello execução seguinte). Por conseguinte, neste exemplo específico, hello nova estimativa de cardinalidade efetua uma melhor tarefa ao fazer uma estimativa do número de Olá de linhas porque 202,877 é muito próximo too200, 704, que 194,284! Último, se alterar Olá cláusula WHERE predicados tooequality (vez ">" para a instância), isto foi possível efetuar a Olá calcula entre Olá antiga e nova função de cardinalidade ainda mais diferentes, consoante o número de correspondências pode obter.

Obviamente, neste caso, que está a ser ~ 6000 linhas fora da contagem real não representa uma grande quantidade de dados em algumas situações. Agora, transpor esta toomillions de linhas em várias tabelas e consultas mais complexas, e a estimativa de Olá por vezes pode estar desligada por milhões de linhas, Olá por conseguinte, o risco de segurança diretriz Olá errado plano de execução, ou quando solicitar memória insuficiente concede à esquerda tooTempDB spills e e/s mais por isso, são muito superior.

Se tiver oportunidade de Olá, restaure esta comparação com as suas consultas mais comuns e conjuntos de dados e ver para si por quanto alguns estimativas de Olá antiga e nova são afetados, embora alguns pode ficar mais off na realidade Olá ou alguns outros apenas apenas simplesmente Quanto mais próximo linha real de toohello conta, na verdade, é devolvido em conjuntos de resultados de Olá. Todos dependerá da forma de Olá da sua consultas, características de base de dados SQL do Azure de Olá, natureza Olá e tamanho de Olá dos seus conjuntos de dados e estatísticas de Olá disponíveis sobre os mesmos. Se acabou de criar a instância de SQL Database do Azure, Olá consulta otimizador será toobuild o conhecimento do zero em vez de estatísticas de reutilizar compostas consulta anterior Olá é executado. Por isso, Olá estimativas são situação de servidor e aplicação tooevery muito contextuais e quase específico. É tookeep um aspeto importante lembrar!

## <a name="some-considerations-tootake-into-account"></a>Tootake algumas considerações para a conta
Embora a maioria das cargas de trabalho seriam beneficiar do nível de compatibilidade de Olá 130, antes de adotar o nível de compatibilidade de Olá para o seu ambiente de produção, basicamente tem 3 opções:

1. Mover o nível de toocompatibility 130 e ver como efetuar ações. Caso tenha em atenção algumas regressões ', apenas simplesmente definir Olá compatibilidade nível tooits back-nível original, ou manter 130 e apenas inverso modo Legado do Olá estimativa de cardinalidade back toohello (tal como explicado anteriormente, isto sozinho foi resolver Olá problema).
2. Testar cuidadosamente as suas aplicações existentes em carga semelhante de produção, ajustar e validar desempenho Olá antes tooproduction contínuo. Em caso de problemas, mesmo que acima, pode sempre voltar atrás toohello original nível de compatibilidade, ou simplesmente inverso modo Legado do Olá estimativa de cardinalidade toohello back.
3. Como uma opção final e Olá tooaddress de forma mais recente estas questões, é o arquivo de consultas de Olá tooleverage. Que é a opção recomendada de hoje! análise de Olá tooassist das suas consultas em compatibilidade nível 120 ou abaixo versus 130, não é possível Aconselhamo-lo suficiente toouse arquivo de consultas. O arquivo de consultas está disponível com a versão mais recente do Olá do Azure SQL Database V12 e foi concebido toohelp, com a resolução de problemas de desempenho de consulta. Considere Olá arquivo de consultas como um gravador de dados para a base de dados a recolher e apresentar informações detalhadas de históricos sobre todas as consultas. Isto significativamente simplifica forenses de desempenho ao reduzir Olá tempo toodiagnose e resolver problemas. Pode encontrar mais informações em [arquivo de consultas: um gravador de dados para a base de dados](https://azure.microsoft.com/blog/query-store-a-flight-data-recorder-for-your-database/).

Num alto nível, se já tiver um conjunto de bases de dados com o nível de compatibilidade 120 ou abaixo e planear toomove Olá algumas delas too130, ou porque a carga de trabalho aprovisionar automaticamente novas bases de dados que serão em breve definido por predefinição too130, considere. seguinte Olá:

* Antes de alterar toohello novo nível de compatibilidade de produção, ative o arquivo de consultas. Pode consultar demasiado[alterar Olá modo de compatibilidade de base de dados e a utilização Olá arquivo de consultas](https://msdn.microsoft.com/library/bb895281.aspx) para obter mais informações.
* Em seguida, teste críticas todas as cargas de trabalho com dados representativos e consultas de um ambiente de produção como e o desempenho de Olá comparar teve e conforme comunicado pelo arquivo de consultas. Se ocorrer algum regressões, pode identificar Olá regressed consultas com Olá arquivo de consultas e utilizar o plano de Olá forçar do arquivo de consultas opção (também conhecido como planear a afixação). Nesse caso, pode definitively permaneça com um nível de compatibilidade de Olá 130 e utiliza o plano de consulta anteriores Olá como sugerido pelo Olá arquivo de consultas.
* Se pretender tooleverage novas funcionalidades e capacidades da base de dados do SQL do Azure (que está a executar o SQL Server 2016), mas são sensíveis toochanges pelo nível de compatibilidade de Olá 130, como último recurso, pode considerar forçar o nível de compatibilidade de Olá novamente nível de toohello que se adapta às sua carga de trabalho, utilizando uma instrução ALTER DATABASE. Mas, em primeiro lugar, tenha em atenção que plano do arquivo de consultas de Olá afixação opção é a melhor opção porque não utilizar 130 é basicamente permanecendo no nível de funcionalidade Olá de uma versão mais antiga do SQL Server.
* Se tiver aplicações multi-inquilino expansão várias bases de dados, poderá ser Olá tooupdate necessário aprovisionar lógica do seu tooensure bases de dados de um nível de compatibilidade consistente em todas as bases de dados; aqueles antigos e recentemente aprovisionadas. O desempenho da carga de trabalho de aplicação pode ser facto toohello confidenciais que algumas bases de dados estão em execução em níveis de compatibilidade diferentes e, por conseguinte, a consistência de nível de compatibilidade em qualquer base de dados pode ser necessária na ordem tooprovide Olá mesmo experiência tooyour clientes tudo em quadro Olá. Tenha em atenção que não é um mandato, realmente depende de como a aplicação é afetada por nível de compatibilidade de Olá.
* Última, sobre Olá estimativa de cardinalidade e tal como alterar o nível de compatibilidade de Olá, antes de continuar na produção, é recomendado tootest a carga de trabalho de produção em Olá novo condições toodetermine se a aplicação é vantajosa do melhoramentos de estimativa de cardinalidade Olá.

## <a name="conclusion"></a>Conclusão
Utilizar a SQL Database do Azure toobenefit de todos os melhoramentos do SQL Server 2016 claramente melhorar as execuções de consulta. Tal como-é! Obviamente, tal como qualquer nova funcionalidade, uma avaliação adequada tem de ser efetuada toodetermine Olá exato as condições sob as quais a carga de trabalho de base de dados funciona Olá melhor. Experiência mostra que a maioria das cargas de trabalho são tooat esperado pelo menos, executado transparente com nível de compatibilidade 130, tirando partido de nova consulta de processamento funções e nova estimativa de cardinalidade. Que consiga aceder tal, verdade, existem sempre algumas exceções e fazer atraso adequado diligence toodetermine uma avaliação importante quanto pode beneficiar estes melhoramentos. E novamente, o arquivo de consultas Olá pode ser uma ajuda excelente fazer este trabalho!

À medida que o SQL Azure evolui, que pode esperar um nível de compatibilidade 140 no Olá futuras. Quando a hora é adequada, iremos será iniciado se fala sobre o que será apresentada neste nível de compatibilidade futuros 140, tal como brevemente discutimos aqui o nível de compatibilidade 130 é colocar hoje.

Por agora, vamos não se esqueça, a partir de Junho de 2016, SQL Database do Azure deixará nível de compatibilidade do Olá predefinição de 120 too130 para bases de dados recentemente criados. Tenha em atenção!

## <a name="references"></a>Referências
* [Novidades no motor de base de dados](https://msdn.microsoft.com/library/bb510411.aspx#InMemory)
* [Blogue: O arquivo de consultas: um gravador de dados para a base de dados, por Borko Novakovic, 8 de Junho de 2016](https://azure.microsoft.com/blog/query-store-a-flight-data-recorder-for-your-database/)
* [Nível de compatibilidade de base de dados ALTER (Transact-SQL)](https://msdn.microsoft.com/library/bb510680.aspx)
* [ALTERAR A CONFIGURAÇÃO DE ÂMBITO DE BASE DE DADOS](https://msdn.microsoft.com/library/mt629158.aspx)
* [Nível de compatibilidade 130 para V12 de base de dados SQL do Azure](https://azure.microsoft.com/updates/compatibility-level-130-for-azure-sql-database-v12/)
* [Otimizar o seu planos de consulta com Olá avaliador de SQL Server 2014 cardinalidade herdado](https://msdn.microsoft.com/library/dn673537.aspx)
* [Guia de índices Columnstore](https://msdn.microsoft.com/library/gg492088.aspx)
* [Blogue: Melhor desempenho das consultas com um nível de compatibilidade 130 na base de dados SQL do Azure, por Alain Lissoir, 6 de Maio de 2016](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/05/06/improved-query-performance-with-compatibility-level-130-in-azure-sql-database/)

<!--
Improved Query Performance with Compatibility Level 130 in Azure SQL Database

May 6, 2016 by Alain Lissoir (AlainL), on GitHub 'alainlissoir'.

https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/05/06/improved-query-performance-with-compatibility-level-130-in-azure-sql-database/

..... Now, above.
....................
..... Soon, below?

CAPS / MSDN ideally, but instead on ACom:
.. # Assess effects of latest compatibility level on query performance, how to

sql-database-compatibility-level-query-performance-130.md

genemi = MightyPen , 2016-05-20  Friday  17:00pm
-->
