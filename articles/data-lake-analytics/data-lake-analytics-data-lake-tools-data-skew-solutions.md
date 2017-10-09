---
title: problemas de desfasamento de dados de aaaResolve utilizando ferramentas do Azure Data Lake para Visual Studio | Microsoft Docs
description: "Resolução de problemas possíveis soluções para problemas de desfasamento de dados utilizando ferramentas do Azure Data Lake para Visual Studio."
services: data-lake-analytics
documentationcenter: 
author: yanancai
manager: 
editor: 
ms.assetid: 
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 12/16/2016
ms.author: yanacai
ms.openlocfilehash: 3909fbd89eb40f061268cb7128f7fa84a3c33de7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="resolve-data-skew-problems-by-using-azure-data-lake-tools-for-visual-studio"></a>Resolver problemas de desfasamento de dados utilizando ferramentas do Azure Data Lake para Visual Studio

## <a name="what-is-data-skew"></a>O que é dados desfasamento?

Brevemente indicado, o desfasamento de dados é um valor excessiva representado. Imagine que atribuiu 50 examiners de dedução dos impostos tooaudit dedução dos impostos devolve, um examiner para cada Estado de E.U.A.. examiner de Wyoming Olá, porque não existe a população Olá é pequena, tem pouco toodo. Na Califórnia, no entanto, examiner Olá é mantida muito ocupado devido a população do Estado de Olá de grandes dimensões.
    ![Exemplo de problema de desfasamento de dados](./media/data-lake-analytics-data-lake-tools-data-skew-solutions/data-skew-problem.png)

No nosso cenário, dados de Olá é unevenly distribuídos por todos os examiners de dedução dos impostos, que significa que alguns examiners tem de trabalhar mais do que outras pessoas. No seu próprio trabalho frequentemente experiência situações como Olá exemplo de dedução dos impostos examiner aqui. Em termos mais técnicos, um vértice obtém muito mais dados de elementos da rede, uma situação que faz com que o vértice Olá mais do que Olá outras pessoas e que eventualmente atrasar uma tarefa de toda a funcionar. O que é um, a tarefa de Olá poderá falhar, porque poderão ter vértices, por exemplo, uma limitação de tempo de execução de 5 horas e uma limitação de 6 GB de memória.

## <a name="resolving-data-skew-problems"></a>Resolver problemas de desfasamento de dados

Ferramentas do Azure Data Lake para Visual Studio podem ajudá-lo a detetar se a tarefa tem um problema de desfasamento de dados. Se existir um problema, pode resolver-tentando soluções Olá nesta secção.

## <a name="solution-1-improve-table-partitioning"></a>Solução 1: Melhorar a criação de partições de tabela

### <a name="option-1-filter-hello-skewed-key-value-in-advance"></a>Opção 1: Olá filtro skewed valor da chave antecipadamente

Se não afeta a lógica de negócio, pode filtrar valores de frequência superior Olá antecipadamente. Por exemplo, se existirem muitos 000 000 000 na coluna GUID, não poderá tooaggregate esse valor. Antes de agregação, pode escrever "WHERE GUID! ="000-000 000"" valor de alta frequência toofilter Olá.

### <a name="option-2-pick-a-different-partition-or-distribution-key"></a>Opção 2: Escolher uma chave de partição ou de distribuição diferente

Olá anterior exemplo, se pretender que a carga de trabalho do toocheck apenas Olá dedução dos impostos auditoria Olá todas através de país, pode melhorar a distribuição de dados de Olá selecionando o número de ID de Olá como a chave. Escolha uma partição diferente ou chave de distribuição pode, por vezes, distribuir dados Olá mais uniformemente, mas tem de certificar-se de que esta opção não afeta a lógica de negócio toomake. Por exemplo, toocalculate soma de dedução dos impostos de Olá para cada Estado, poderá pretender toodesignate _estado_ como chave de partição Olá. Se continuar tooexperience este problema, tente utilizar a opção 3.

### <a name="option-3-add-more-partition-or-distribution-keys"></a>Opção 3: Adicionar mais chaves de partição ou de distribuição

Em vez de utilizar apenas _estado_ como uma chave de partição, pode utilizar mais do que uma chave para criação de partições. Por exemplo, considere adicionar _código postal_ como uma partição adicional tooreduce chave dados partição tamanhos e distribuir uniformemente mais dados Olá.

### <a name="option-4-use-round-robin-distribution"></a>Opção 4: Utilizar a distribuição de round robin

Se não é possível localizar uma chave adequada para a partição e a distribuição, pode experimentar toouse distribuição de round robin. Distribuição de round robin processa todas as linhas igualmente e aleatoriamente coloca-os no registos correspondentes. dados de Olá obtém distribuídos uniformemente, mas perder informações localidade, uma desvantagem que também pode reduzir o desempenho de tarefa para algumas operações. Além disso, se estão a fazer a agregação para a chave distorcidos Olá mesmo assim, o problema de desfasamento de dados de Olá serão mantidas. toolearn mais informações sobre distribuição de round robin, consulte as distribuições de tabela do U-SQL Olá secção [CREATE TABLE (U-SQL): criar uma tabela com o esquema](https://msdn.microsoft.com/en-us/library/mt706196.aspx#dis_sch).

## <a name="solution-2-improve-hello-query-plan"></a>Solução 2: Melhorar o plano de consulta Olá

### <a name="option-1-use-hello-create-statistics-statement"></a>Opção 1: Utilizar a instrução CREATE STATISTICS de Olá

U-SQL fornece da instrução CREATE STATISTICS Olá em tabelas. Esta declaração fornece mais informações toohello o otimizador de consultas sobre Olá características dos dados, como a distribuição de valor, que estão armazenados numa tabela. Para a maior parte das consultas, otimizador de consultas Olá já gera as estatísticas de necessário Olá para um plano de consulta de alta qualidade. Ocasionalmente, poderá ser necessário tooimprove desempenho das consultas, criar estatísticas adicionais com CREATE STATISTICS ou ao modificar a estrutura da consulta Olá. Para obter mais informações, consulte Olá [CREATE STATISTICS (U-SQL)](https://msdn.microsoft.com/en-us/library/azure/mt771898.aspx) página.

Exemplo de código:

    CREATE STATISTICS IF NOT EXISTS stats_SampleTable_date ON SampleDB.dbo.SampleTable(date) WITH FULLSCAN;

>[!NOTE]
>Informações de estatísticas não são atualizadas automaticamente. Se atualizar dados Olá numa tabela sem voltar a criar estatísticas Olá, o desempenho das consultas Olá poderá diminui.

### <a name="option-2-use-skewfactor"></a>Opção 2: Utilizar SKEWFACTOR

Se quiser dedução dos impostos Olá de toosum para cada Estado, tem de utilizar o grupo por Estado, uma abordagem que não a evitar o problema do Olá desfasamento de dados. No entanto, pode fornecer uma sugestão de dados no seu tooidentify consulta dados desfasamento nas chaves de modo a que o otimizador de Olá pode preparar um plano de execução.

Normalmente, pode definir o parâmetro Olá como 0,5 e 1, com 0,5 que significa que não desfasamento de pesada significado dissimetrias e 1. Porque a sugestão Olá afeta a otimização de plano de execução para a instrução atual Olá e todas as instruções a jusante, ser sugestão de Olá tooadd se antes de Olá potencial skewed key-wise agregação.

    SKEWFACTOR (columns) = x

    Provides a hint that hello given columns have a skew factor x from 0 (no skew) through 1 (very heavy skew).

Exemplo de código:

    //Add a SKEWFACTOR hint.
    @Impressions =
        SELECT * FROM
        searchDM.SML.PageView(@start, @end) AS PageView
        OPTION(SKEWFACTOR(Query)=0.5)
        ;

    //Query 1 for key: Query, ClientId
    @Sessions =
        SELECT
            ClientId,
            Query,
            SUM(PageClicks) AS Clicks
        FROM
            @Impressions
        GROUP BY
            Query, ClientId
        ;

    //Query 2 for Key: Query
    @Display =
        SELECT * FROM @Sessions
            INNER JOIN @Campaigns
                ON @Sessions.Query == @Campaigns.Query
        ;   

### <a name="option-3-use-rowcount"></a>Opção 3: Utilizar contagem de linhas  
Além disso tooSKEWFACTOR, para skewed-chave específica associar casos, se souber que Olá outro conjunto de linhas do associado é pequeno, pode dizer otimizador de Olá adicionando uma sugestão de contagem de linhas na instrução U-SQL de Olá antes de associação. Desta forma, otimizador pode escolher um toohelp de estratégia de associação de difusão melhorar o desempenho. Lembre-se de que a contagem de linhas não resolver o problema de desfasamento de dados de Olá, mas pode oferecer ajuda adicional.

    OPTION(ROWCOUNT = n)

    Identify a small row set before JOIN by providing an estimated integer row count.

Exemplo de código:

    //Unstructured (24-hour daily log impressions)
    @Huge   = EXTRACT ClientId int, ...
                FROM @"wasb://ads@wcentralus/2015/10/30/{*}.nif"
                ;

    //Small subset (that is, ForgetMe opt out)
    @Small  = SELECT * FROM @Huge
                WHERE Bing.ForgetMe(x,y,z)
                OPTION(ROWCOUNT=500)
                ;

    //Result (not enough information toodetermine simple broadcast JOIN)
    @Remove = SELECT * FROM Bing.Sessions
                INNER JOIN @Small ON Sessions.Client == @Small.Client
                ;

## <a name="solution-3-improve-hello-user-defined-reducer-and-combiner"></a>Solução 3: Melhorar reducer definido pelo utilizador de Olá e combinação

Por vezes, pode escrever um toodeal de operador definido pelo utilizador com lógica mais complicada processo e um reducer bem escrito e a combinação podem mitigar um problema de desfasamento de dados em alguns casos.

### <a name="option-1-use-a-recursive-reducer-if-possible"></a>Opção 1: Utilizar um reducer recursiva, se possível

Por predefinição, um reducer definido pelo utilizador é executado no modo não recursivo, que significa que reduzem o trabalho para uma chave é distribuída para um único vértice. Mas, se os seus dados é skewed, conjuntos de dados enormes Olá possam ser processados no vértice único e execute durante muito tempo.

desempenho tooimprove, pode adicionar um atributo no seu toorun de reducer toodefine código no modo recursivo. Em seguida, Olá grandes conjuntos de dados podem ser distribuídas toomultiple vértices e executadas em paralelo, que acelera a tarefa.

toochange um toorecursive de reducer não recursiva, terá de se de que o algoritmo associative toomake. Por exemplo, soma Olá é associative e mediana Olá não é. Terá também de certificar-se de que Olá de entrada e saída para reducer manter Olá toomake mesmo esquema.

Atributo de recursiva reducer:

    [SqlUserDefinedReducer(IsRecursive = true)]

Exemplo de código:

    [SqlUserDefinedReducer(IsRecursive = true)]
    public class TopNReducer : IReducer
    {
        public override IEnumerable<IRow>
            Reduce(IRowset input, IUpdatableRow output)
        {
            //Your reducer code goes here.
        }
    }

### <a name="option-2-use-row-level-combiner-mode-if-possible"></a>Opção 2: Utilizar o modo de combinação ao nível da linha, se possível

Sugestão de contagem de linhas de toohello semelhante para casos de associação de chave skewed específico, o modo de combinação tenta toodistribute grande valor de chave skewed conjuntos toomultiple vértices para que o trabalho Olá pode ser executado em simultâneo. Modo de combinação não é possível resolver problemas de desfasamento de dados, mas pode oferecer ajuda adicional para conjuntos de valores de chave skewed grande.

Por predefinição, o modo de combinação Olá é completo, o que significa que Olá deixado conjunto de linhas e conjunto de linhas à direita não pode ser separado. Definição de modo de Olá como direito/esquerda/interna permite que a associação ao nível da linha. sistema de Olá separa conjuntos de linha correspondente Olá e distribui-las em vários vértices que são executadas em paralelo. No entanto, antes de configurar o modo de combinação de Olá, tenha cuidado tooensure Olá conjuntos de linhas correspondentes pode ser separado.

exemplo de Olá que se segue mostra um conjunto de linhas esquerdo separados. Cada linha de saída depende de uma única linha de entrada da esquerda Olá e potencialmente depende todas as linhas da Olá à direita com Olá mesmo valor da chave. Se definir o modo de combinação Olá como à esquerda, o sistema Olá separa Olá grande esquerda linha definida para as pequenas e atribui-las toomultiple vértices.

![Ilustração do modo de combinação](./media/data-lake-analytics-data-lake-tools-data-skew-solutions/combiner-mode-illustration.png)

>[!NOTE]
>Se definir o modo de combinação errado Olá, combinação Olá é menos eficiente e resultados de Olá poderão estar incorreto.

Atributos do modo de combinação de:

- [SqlUserDefinedCombiner(Mode=CombinerMode.Full)]: Every output row potentially depends on all hello input rows from left and right with hello same key value.

- SqlUserDefinedCombiner(Mode=CombinerMode.Left): Cada linha de saída depende de uma única linha de entrada da esquerda Olá (e, potencialmente, todas as linhas da Olá à direita com Olá mesmo valor da chave).

- qlUserDefinedCombiner(Mode=CombinerMode.Right): cada linha de saída depende de uma única linha de entrada de Olá direito (e, potencialmente, todas as linhas da esquerda Olá com Olá mesmo valor da chave).

- SqlUserDefinedCombiner(Mode=CombinerMode.Inner): Cada linha de saída depende de uma única linha de entrada de Olá à esquerda e Olá à direita com Olá mesmo valor.

Exemplo de código:

    [SqlUserDefinedCombiner(Mode = CombinerMode.Right)]
    public class WatsonDedupCombiner : ICombiner
    {
        public override IEnumerable<IRow>
            Combine(IRowset left, IRowset right, IUpdatableRow output)
        {
        //Your combiner code goes here.
        }
    }
