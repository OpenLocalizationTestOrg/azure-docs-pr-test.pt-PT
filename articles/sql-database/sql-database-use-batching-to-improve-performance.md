---
title: "toouse aaaHow criação de batches de desempenho da aplicação tooimprove SQL Database do Azure"
description: "Olá tópico fornece uma prova que criação de batches de base de dados operações significativamente imroves Olá velocidade e escalabilidade das suas aplicações de base de dados do Azure SQL. Embora estas técnicas de lotes de trabalho para qualquer base de dados do SQL Server, o foco Olá artigo Olá é no Azure."
services: sql-database
documentationcenter: na
author: stevestein
manager: jhubbard
editor: 
ms.assetid: 563862ca-c65a-46f6-975d-10df7ff6aa9c
ms.service: sql-database
ms.custom: develop apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 07/12/2016
ms.author: sstein
ms.openlocfilehash: 124b203ee69c595f0813852ff09ef9ec6841233a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-batching-tooimprove-sql-database-application-performance"></a>Como toouse tooimprove de desempenho de aplicações de base de dados SQL de criação de batches
Criação de batches de operações tooAzure base de dados SQL significativamente melhora o desempenho de Olá e a escalabilidade das suas aplicações. Na ordem toounderstand Olá vantagens, indicadas Olá primeira parte deste artigo abrange alguns resultados do teste de exemplo que comparam os pedidos de batches e sequenciais tooa base de dados SQL. Olá resto Olá artigo mostra técnicas Olá, cenários e considerações toohelp toouse de criação de batches com êxito nas suas aplicações do Azure.

## <a name="why-is-batching-important-for-sql-database"></a>Por isso é criação de batches importante para a base de dados SQL?
Serviço remoto de tooa chamadas de criação de batches é uma estratégia para aumentar o desempenho e escalabilidade bem conhecida. Não existe corrigidas interações de tooany os custos com um serviço remoto, como serialização, a transferência de rede e a anulação da serialização de processamento. Empacotamento transações separadas muitos para um único lote minimiza estes custos.

Neste documento, queremos tooexamine várias estratégias de lotes de base de dados SQL e cenários. Embora estas estratégias também são importantes para aplicações no local que utilizam o SQL Server, existem várias razões para Realce a utilização de Olá de criação de batches para a base de dados SQL:

* Não há potencialmente maior latência de rede no acesso à base de dados do SQL Server, especialmente se estão a aceder à base de dados SQL a partir de fora Olá mesmo centro de dados do Microsoft Azure.
* características de multi-inquilino de Olá de meios de base de dados SQL que Olá eficiência de dados de Olá toohello correlaciona de camada de acesso global escalabilidade da base de dados de Olá. Base de dados do SQL Server tem a impedir que qualquer utilizador/inquilino único monopolizing detrimento toohello de recursos de base de dados de outros inquilinos. Em resposta toousage que excedam quotas predefinidas, base de dados SQL pode reduzir o débito ou responder com exceções de limitação. Resulta numa eficiência, tais como a criação de batches, permitem toodo trabalhar mais na base de dados do SQL Server antes de atingir estes limites. 
* Criação de batches também é rentável para arquiteturas que utilizem várias bases de dados (fragmentação). eficiência de Olá da sua interação com cada unidade de base de dados ainda é um fator chave a escalabilidade geral. 

Uma das vantagens de Olá da utilização da base de dados do SQL Server é se não tiver toomanage Olá servidores desse anfitrião Olá da base de dados. No entanto, esta infraestrutura gerida também significa que tem toothink diferente sobre otimizações de base de dados. Já não pode ser tooimprove Olá da base de dados hardware ou na rede de infraestrutura. Microsoft Azure controla os ambientes. área de principais de Olá que pode controlar é como a sua aplicação interage com base de dados SQL. Criação de batches é uma destas otimizações de. 

Olá primeira parte documento Olá examina várias técnicas de lotes para aplicações de .NET que utilizam a base de dados SQL. Olá últimas duas secções abrangem cenários e as diretrizes de lotes.

## <a name="batching-strategies"></a>Estratégias de criação de batches
### <a name="note-about-timing-results-in-this-topic"></a>Tenha em atenção sobre os resultados de temporização neste tópico
> [!NOTE]
> Resultados não são benchmarks mas destinam tooshow **desempenho relativo**. As temporizações baseiam-se uma média de, pelo menos, 10 execuções do teste. As operações são inserções para uma tabela vazia. Estes testes foram medidos pre-V12 e não necessariamente correspondem toothroughput que podem ocorrer numa base de dados V12 utilizando Olá novo [escalões de serviço](sql-database-service-tiers.md). benefício de relativo Olá de Olá técnica de criação de batches deve ser semelhante.
> 
> 

### <a name="transactions"></a>Transações
Parece um toobegin uma revisão de criação de batches por debater transações. Mas utilize Olá de transações do lado do cliente tem um efeito de lotes do lado do servidor subtis que melhora o desempenho. Transações podem ser adicionadas e com apenas algumas linhas de código, para que fornecem um desempenho de tooimprove de forma rápida de operações sequenciais.

Considere o seguinte código c# que contém uma sequência de inserção de Olá e operações numa tabela simple de atualização.

    List<string> dbOperations = new List<string>();
    dbOperations.Add("update MyTable set mytext = 'updated text' where id = 1");
    dbOperations.Add("update MyTable set mytext = 'updated text' where id = 2");
    dbOperations.Add("update MyTable set mytext = 'updated text' where id = 3");
    dbOperations.Add("insert MyTable values ('new value',1)");
    dbOperations.Add("insert MyTable values ('new value',2)");
    dbOperations.Add("insert MyTable values ('new value',3)");

Olá seguir ADO.NET código sequencialmente executa estas operações.

    using (SqlConnection connection = new SqlConnection(CloudConfigurationManager.GetSetting("Sql.ConnectionString")))
    {
        conn.Open();

        foreach(string commandString in dbOperations)
        {
            SqlCommand cmd = new SqlCommand(commandString, conn);
            cmd.ExecuteNonQuery();                   
        }
    }

Olá melhor forma toooptimize este código é tooimplement alguma forma de criação de batches de lado do cliente destas chamadas. Mas há um desempenho de Olá tooincrease de forma simples deste código simplesmente envolvendo sequência Olá de chamadas de uma transação. Eis Olá código mesmo que utiliza uma transação.

    using (SqlConnection connection = new SqlConnection(CloudConfigurationManager.GetSetting("Sql.ConnectionString")))
    {
        conn.Open();
        SqlTransaction transaction = conn.BeginTransaction();

        foreach (string commandString in dbOperations)
        {
            SqlCommand cmd = new SqlCommand(commandString, conn, transaction);
            cmd.ExecuteNonQuery();
        }

        transaction.Commit();
    }

Transações, na verdade, estão a ser utilizadas em ambos estes exemplos. No primeiro exemplo Olá, cada chamada individuais é uma transação implícita. No segundo exemplo Olá, uma transação explícita encapsula num wrapper todas as chamadas de Olá. Por documentação Olá Olá [registo de transações de escrita antecipada](https://msdn.microsoft.com/library/ms186259.aspx), registos são libertados toohello disco quando consolida a transação de Olá. Por isso, incluindo chamadas mais de uma transação, hello registo de transações de escrita toohello pode atrasar até Olá transação está consolidada. Em vigor, pretende ativar a criação de batches para registo de transações do servidor de Olá, escritas toohello.

Olá, a tabela seguinte mostra alguns resultados do teste ad-hoc. testes de Olá realizados Olá que mesmo sequenciais insere com e sem transações. Para obter mais perspetiva, primeiro conjunto de Olá de testes executou remotamente a partir de uma base de dados do computador portátil toohello no Microsoft Azure. Olá segundo conjunto de testes executou de um serviço em nuvem e a base de dados que ambos resided dentro Olá mesmo centro de dados do Microsoft Azure (EUA oeste). Olá tabela seguinte mostra a duração de Olá em milissegundos do inserções sequenciais com e sem transações.

**No local tooAzure**:

| Operações | Nenhuma transação (ms) | Transações (ms) |
| --- | --- | --- |
| 1 |130 |402 |
| 10 |1208 |1226 |
| 100 |12662 |10395 |
| 1000 |128852 |102917 |

**TooAzure do Azure (mesmo centro de dados)**:

| Operações | Nenhuma transação (ms) | Transações (ms) |
| --- | --- | --- |
| 1 |21 |26 |
| 10 |220 |56 |
| 100 |2145 |341 |
| 1000 |21479 |2756 |

> [!NOTE]
> Resultados não são testes de desempenho. Consulte Olá [nota sobre os resultados de temporização neste tópico](#note-about-timing-results-in-this-topic).
> 
> 

Com base nos resultados do teste anterior Olá, uma única operação de moldagem de uma transação diminui, na verdade, o desempenho. Mas como aumentar o número de Olá de operações dentro de uma transação única, melhoramento de desempenho de Olá torna-se mais marcado. diferença de desempenho de Olá também é mais evidente quando todas as operações de ocorrerem num centro de dados do Olá Microsoft Azure. Olá uma maior latência da utilização de base de dados SQL do datacenter do Microsoft Azure de Olá exteriores overshadows ganhos de desempenho de Olá da utilização de transações.

Embora a utilização de Olá de transações pode aumentar o desempenho, continuar demasiado[observar as melhores práticas para ligações de transações e](https://msdn.microsoft.com/library/ms187484.aspx). Manter transação Olá o mais curta como ligação de base de dados possíveis e fechar Olá após a conclusão do trabalho Olá. Olá, utilizando a instrução no exemplo anterior Olá garante que Olá a ligação foi fechada quando blocos de código subsequentes Olá estiver concluída.

exemplo anterior Olá demonstra que pode adicionar um código ADO.NET tooany transações locais com duas linhas. Transações oferecem uma forma rápida de desempenho de Olá tooimprove de código que torna sequencial inserir, atualizar e eliminar operações. No entanto, para um desempenho mais rápido Olá, considere alterar Olá código adicional tootake partido do lado do cliente de criação de batches, tais como parâmetros de valor de tabela.

Para obter mais informações sobre transações por ADO.NET, consulte [transações locais em ADO.NET](https://docs.microsoft.com/dotnet/framework/data/adonet/local-transactions).

### <a name="table-valued-parameters"></a>parâmetros de valor de tabela
Parâmetros de valor de tabela suportam tipos de tabela definido pelo utilizador como parâmetros instruções Transact-SQL, funções e procedimentos armazenados. Esta técnica de lotes do lado do cliente permite-lhe toosend várias linhas de dados dentro do parâmetro de valor de tabela Olá. parâmetros de valor de tabela de toouse, defina primeiro um tipo de tabela. Olá a seguinte instrução Transact-SQL cria um tipo de tabela com o nome **MyTableType**.

    CREATE TYPE MyTableType AS TABLE 
    ( mytext TEXT,
      num INT );


No código, crie um **DataTable** com Olá exacta mesmo nomes e tipos de tipo de tabela Olá. Passar esta **DataTable** num parâmetro de uma consulta de texto ou o procedimento armazenado chamada. Olá exemplo seguinte mostra esta técnica:

    using (SqlConnection connection = new SqlConnection(CloudConfigurationManager.GetSetting("Sql.ConnectionString")))
    {
        connection.Open();

        DataTable table = new DataTable();
        // Add columns and rows. hello following is a simple example.
        table.Columns.Add("mytext", typeof(string));
        table.Columns.Add("num", typeof(int));    
        for (var i = 0; i < 10; i++)
        {
            table.Rows.Add(DateTime.Now.ToString(), DateTime.Now.Millisecond);
        }

        SqlCommand cmd = new SqlCommand(
            "INSERT INTO MyTable(mytext, num) SELECT mytext, num FROM @TestTvp",
            connection);

        cmd.Parameters.Add(
            new SqlParameter()
            {
                ParameterName = "@TestTvp",
                SqlDbType = SqlDbType.Structured,
                TypeName = "MyTableType",
                Value = table,
            });

        cmd.ExecuteNonQuery();
    }

No exemplo anterior Olá, Olá **SqlCommand** objeto insere linhas de um parâmetro de valor de tabela,  **@TestTvp** . Olá criado anteriormente **DataTable** objeto está atribuído parâmetro toothis com Olá **SqlCommand.Parameters.Add** método. Inserções de Olá lotes de uma chamada significativamente aumenta desempenho Olá através de inserções sequenciais.

tooimprove Olá anterior exemplo além disso, utilize um procedimento armazenado em vez de um comando baseado em texto. Olá comando Transact-SQL a seguir cria um procedimento armazenado que aceita Olá **SimpleTestTableType** parâmetro de valor de tabela.

    CREATE PROCEDURE [dbo].[sp_InsertRows] 
    @TestTvp as MyTableType READONLY
    AS
    BEGIN
    INSERT INTO MyTable(mytext, num) 
    SELECT mytext, num FROM @TestTvp
    END
    GO

Em seguida, altere Olá **SqlCommand** declaração no seguinte de toohello de exemplo Olá anterior código de objeto.

    SqlCommand cmd = new SqlCommand("sp_InsertRows", connection);
    cmd.CommandType = CommandType.StoredProcedure;

Na maioria dos casos, os parâmetros de valor de tabela ter equivalente ou um melhor desempenho do que outras técnicas de lotes. Parâmetros de valor de tabela são, muitas vezes, preferível, mais flexíveis do que outras opções. Por exemplo, outras técnicas, tais como a cópia em massa SQL, apenas permitem a inserção de Olá de linhas novas. Mas com parâmetros de valor de tabela, pode utilizar lógica Olá armazenado procedimento toodetermine que linhas são atualizações e que são insere. tipo de tabela Olá também pode ser modificado toocontain uma coluna de "Operação" que indica se Olá especificadas linha deve ser inserida, atualizada ou eliminada.

Olá, a tabela seguinte mostra os resultados do teste de ad-hoc para utilização de Olá dos parâmetros de valor de tabela em milissegundos.

| Operações | No local tooAzure (ms) | Azure mesmo centro de dados (ms) |
| --- | --- | --- |
| 1 |124 |32 |
| 10 |131 |25 |
| 100 |338 |51 |
| 1000 |2615 |382 |
| 10000 |23830 |3586 |

> [!NOTE]
> Resultados não são testes de desempenho. Consulte Olá [nota sobre os resultados de temporização neste tópico](#note-about-timing-results-in-this-topic).
> 
> 

Olá ganhos de desempenho da criação de batches é imediatamente aparente. No teste sequenciais anterior Olá, 1000 demorou segundos 129 Olá exteriores datacenter e segundos 21 num Olá Centro de dados. Mas com parâmetros de valor de tabela, 1000 operações demorar apenas segundos 2.6 fora do datacenter Olá e 0.4 segundos num Olá Centro de dados.

Para obter mais informações sobre os parâmetros de valor de tabela, consulte [Table-Valued parâmetros](https://msdn.microsoft.com/library/bb510489.aspx).

### <a name="sql-bulk-copy"></a>Cópia em massa SQL
Cópia em massa SQL é outra forma tooinsert grandes quantidades de dados para uma base de dados de destino. As aplicações de .NET podem utilizar Olá **SqlBulkCopy** operações de inserção em massa tooperform de classe. **SqlBulkCopy** é semelhante na ferramenta de linha de comandos toohello função, **Bcp.exe**, ou Olá instrução de Transact-SQL, **inserção em massa**. Olá exemplo de código seguinte mostra como toobulk Olá de copiar as linhas da origem de Olá **DataTable**, tabela, a tabela de destino toohello no SQL Server, MyTable.

    using (SqlConnection connection = new SqlConnection(CloudConfigurationManager.GetSetting("Sql.ConnectionString")))
    {
        connection.Open();

        using (SqlBulkCopy bulkCopy = new SqlBulkCopy(connection))
        {
            bulkCopy.DestinationTableName = "MyTable";
            bulkCopy.ColumnMappings.Add("mytext", "mytext");
            bulkCopy.ColumnMappings.Add("num", "num");
            bulkCopy.WriteToServer(table);
        }
    }

Existem alguns casos onde cópia em massa é preferencial através de parâmetros de valor de tabela. Consulte a tabela de comparação de Olá de Table-Valued parameters versus operações de inserção em massa tópico Olá [Table-Valued parâmetros](https://msdn.microsoft.com/library/bb510489.aspx).

Olá seguintes resultados de teste do ad-hoc mostram desempenho Olá de criação de batches com **SqlBulkCopy** em milissegundos.

| Operações | No local tooAzure (ms) | Azure mesmo centro de dados (ms) |
| --- | --- | --- |
| 1 |433 |57 |
| 10 |441 |32 |
| 100 |636 |53 |
| 1000 |2535 |341 |
| 10000 |21605 |2737 |

> [!NOTE]
> Resultados não são testes de desempenho. Consulte Olá [nota sobre os resultados de temporização neste tópico](#note-about-timing-results-in-this-topic).
> 
> 

Em tamanhos de lote mais pequenos, parâmetros de valor de tabela de utilização de Olá outperformed Olá **SqlBulkCopy** classe. No entanto, **SqlBulkCopy** efetuada 12-31% mais rapidamente do que os parâmetros de valor de tabela de testes de Olá de linhas de 1000 e 10 000. Como parâmetros de valor de tabela, **SqlBulkCopy** é uma boa opção para inserções em lote, especialmente quando comparado com desempenho toohello das operações não em lotes.

Para obter mais informações sobre a cópia em massa no ADO.NET, consulte [operações de cópia em massa no SQL Server](https://msdn.microsoft.com/library/7ek5da1a.aspx).

### <a name="multiple-row-parameterized-insert-statements"></a>Instruções parametrizadas inserir várias linhas
Uma alternativa para lotes pequenos é tooconstruct uma grande parametrizadas instrução INSERT que insere várias linhas. Olá seguinte exemplo de código demonstra esta técnica.

    using (SqlConnection connection = new SqlConnection(CloudConfigurationManager.GetSetting("Sql.ConnectionString")))
    {
        connection.Open();

        string insertCommand = "INSERT INTO [MyTable] ( mytext, num ) " +
            "VALUES (@p1, @p2), (@p3, @p4), (@p5, @p6), (@p7, @p8), (@p9, @p10)";

        SqlCommand cmd = new SqlCommand(insertCommand, connection);

        for (int i = 1; i <= 10; i += 2)
        {
            cmd.Parameters.Add(new SqlParameter("@p" + i.ToString(), "test"));
            cmd.Parameters.Add(new SqlParameter("@p" + (i+1).ToString(), i));
        }

        cmd.ExecuteNonQuery();
    }


Neste exemplo destina o conceito básico de Olá tooshow. Um cenário mais realista seria percorrer cadeia de consulta do Olá necessário entidades tooconstruct Olá e parâmetros de comando Olá em simultâneo. Está limitado tooa total dos parâmetros de consulta de 2100, pelo que isto limita o número total de Olá de linhas que podem ser processados desta forma.

Olá seguir desempenho Olá mostrar de resultados de teste de ad-hoc deste tipo de instrução insert em milissegundos.

| Operações | Parâmetros de valor de tabela (ms) | INSERÇÃO de instrução única (ms) |
| --- | --- | --- |
| 1 |32 |20 |
| 10 |30 |25 |
| 100 |33 |51 |

> [!NOTE]
> Resultados não são testes de desempenho. Consulte Olá [nota sobre os resultados de temporização neste tópico](#note-about-timing-results-in-this-topic).
> 
> 

Esta abordagem pode ser ligeiramente mais rápida para lotes são menos de 100 linhas. Embora seja pequena melhoria Olá, esta técnica é outra opção que poderá funcionar corretamente no seu cenário de aplicação específica.

### <a name="dataadapter"></a>DataAdapter
Olá **DataAdapter** classe permite-lhe toomodify um **DataSet** objeto e, em seguida, submeter as alterações de Olá como operações INSERT, UPDATE e DELETE. Se estiver a utilizar Olá **DataAdapter** desta forma, é importante toonote que separam as chamadas são efetuados para cada operação distinct. tooimprove desempenho, utilize Olá **UpdateBatchSize** propriedade toohello diversas operações que deve ser em lotes num momento. Para obter mais informações, consulte [efetuar Batch operações utilizando DataAdapters](https://msdn.microsoft.com/library/aadf8fk2.aspx).

### <a name="entity-framework"></a>Do Entity framework
Do Entity Framework não suporta atualmente a criação de batches. Os programadores diferentes na Comunidade Olá foi efetuada uma tentativa soluções toodemonstrate, como ignorar Olá **SaveChanges** método. Mas soluções Olá são normalmente toohello complexa e personalizadas aplicação e o modelo de dados. projeto de codeplex Olá do Entity Framework tem atualmente uma página de debate sobre este pedido de funcionalidade. tooview este debate, consulte [Design reunião notas - 2 de Agosto de 2012](http://entityframework.codeplex.com/wikipage?title=Design%20Meeting%20Notes%20-%20August%202%2c%202012).

### <a name="xml"></a>XML
Por questões de exaustividade, iremos sentir que é importante tootalk sobre XML como uma estratégia de lotes. No entanto, a utilização de Olá de XML não tem nenhum vantagens através de outros métodos e as desvantagens várias. abordagem de Olá é parâmetros tootable valor semelhantes, mas um ficheiro XML ou cadeia é transferida um procedimento tooa armazenado em vez de uma tabela definida pelo utilizador. procedimento armazenado de Olá analisa comandos Olá no procedimento de Olá armazenado.

Existem várias desvantagens toothis abordagem:

* Trabalhar com XML pode ser complicada e propensas ao erro.
* Análise Olá XML na base de dados de Olá pode ser intensivas em CPU.
* Na maioria dos casos, este método é mais lento do que os parâmetros de valor de tabela.

Por esta razão, não se recomenda utilizar Olá de XML para consultas de batch.

## <a name="batching-considerations"></a>Considerações sobre a criação de batches
Olá seguintes secções fornece mais orientação para a utilização de Olá de criação de batches em aplicações de base de dados SQL.

### <a name="tradeoffs"></a>Fala
Consoante a arquitetura, a criação de batches pode envolver uma variação entre o desempenho e resiliência. Por exemplo, considere o cenário de olá onde a função inesperadamente fica inativo. Se perder a uma linha de dados, o impacto de Olá é inferior ao impacto Olá de perda de um lote de linhas unsubmitted grande. Não há um maior risco quando a memória intermédia linhas antes de lhes enviar toohello base de dados numa janela de tempo especificado.

Devido a esta compromisso, avalie o tipo de Olá de operações que o batch. Batch de forma mais agressiva (lotes maiores e mais intervalos de tempo) com dados seja menos críticos.

### <a name="batch-size"></a>Tamanho do lote
No nossos testes, normalmente, não havia não lotes de grandes dimensões de toobreaking partido para segmentos mais pequenos. Na verdade, muitas vezes, esta subdivision resultou no desempenho mais lento ao submeter um único lote grande. Por exemplo, considere um cenário onde pretende tooinsert 1000 linhas. Olá tabela seguinte mostra quanto tempo os parâmetros de valor de tabela toouse tooinsert 1000 linhas quando dividido em lotes mais pequenos.

| Tamanho do lote | Iterações | Parâmetros de valor de tabela (ms) |
| --- | --- | --- |
| 1000 |1 |347 |
| 500 |2 |355 |
| 100 |10 |465 |
| 50 |20 |630 |

> [!NOTE]
> Resultados não são testes de desempenho. Consulte Olá [nota sobre os resultados de temporização neste tópico](#note-about-timing-results-in-this-topic).
> 
> 

Pode ver que Olá obter o melhor desempenho para 1000 linhas é toosubmit-los ao mesmo tempo. Outros testes (não apresentados aqui) surgiu um toobreak ganhos de desempenho pequeno um lote de 10000 linhas em dois lotes de 5000. Mas o esquema da tabela Olá para estes testes é relativamente simple, pelo que deverá efetuar os testes no seu dados específicos e batch tamanhos tooverify estes findings.

Outro fator tooconsider é que, se ficar demasiado grande batch total Olá, base de dados do SQL Server poderá limitar e refuse batch de Olá toocommit. Para obter melhores resultados Olá, teste toodetermine seu cenário específico se houver um tamanho de lote ideal. Certifique-tamanho de lote Olá configuráveis em tempo de execução tooenable ajustes rápida com base no desempenho ou erros.

Por fim, equilibrar o tamanho do lote de Olá Olá com riscos de Olá associados à criação de batches. Se existem erros transitórios ou função Olá falha, considere consequências Olá repetir a operação de Olá ou perda de dados de Olá no lote de Olá.

### <a name="parallel-processing"></a>Processamento paralelo
E se demorou abordagem Olá de reduzir o tamanho do lote Olá mas utilizados vários threads o tooexecute Olá trabalho? Novamente, os nossos testes mostrou que vários lotes multithread mais pequeno normalmente a efetuadas worse um único lote maior. Olá teste seguinte tenta tooinsert 1000 linhas num ou mais lotes paralelas. Este teste mostra como mais lotes em simultâneo, na verdade, diminuir o desempenho.

| Tamanho do lote [iterações] | Dois threads (ms) | Quatro threads (ms) | Seis threads (ms) |
| --- | --- | --- | --- |
| 1000 [1] |277 |315 |266 |
| 500 [2] |548 |278 |256 |
| 250 [4] |405 |329 |265 |
| 100 [10] |488 |439 |391 |

> [!NOTE]
> Resultados não são testes de desempenho. Consulte Olá [nota sobre os resultados de temporização neste tópico](#note-about-timing-results-in-this-topic).
> 
> 

Existem várias razões possíveis para degradação do desempenho do Olá tooparallelism devida:

* Existem várias chamadas de rede em simultâneo em vez de um.
* Várias operações em relação a uma única tabela podem resultar em contenção e a bloquear.
* Existem sobrecargas associadas multithreading.
* despesa Olá abrir várias ligações prevalece sobre o benefício de Olá de processamento paralelo.

Se destinar a tabelas diferentes ou bases de dados, é possível toosee algumas desempenho obter com esta estratégia. Fragmentação de base de dados ou federações seria um cenário para esta abordagem. Fragmentação utiliza várias bases de dados e base de dados de tooeach de dados diferente de rotas. Se cada lote pequeno for tooa base de dados diferente, em seguida, efetuar operações de Olá em paralelo pode ser mais eficiente. No entanto, Olá ganhos de desempenho não é suficientemente significativa toouse como base Olá de fragmentação de base de dados de toouse uma decisão na sua solução.

Em algumas estruturas, execução paralela de lotes de menores pode resultar na melhor débito de pedidos num sistema com carga. Neste caso, mesmo que se tooprocess mais rápida, um único lote maior, processamento de lotes de vários em paralelo poderá ser mais eficiente.

Se utilizar a execução paralela, considere controlar Olá de número máximo de threads de trabalho. Um número mais pequeno poderá resultar em menos contenção e um tempo de execução mais rápido. Além disso, considere a carga adicional Olá que isto coloca na base de dados Olá destino nas ligações e transações.

### <a name="related-performance-factors"></a>Fatores de desempenho relacionados
Documentação de orientação típica no desempenho da base de dados também afeta a criação de batches. Por exemplo, inserir desempenho é reduzido para tabelas com uma chave primária grande ou vários índices não em cluster.

Se os parâmetros de valor de tabela utilizam um procedimento armazenado, pode utilizar o comando de Olá **SET NOCOUNT ON** início Olá procedimento Olá. Esta declaração suprime retorno Olá de contagem de Olá de linhas de Olá afetado no procedimento de Olá. No entanto, nos nossos testes, Olá utilização de **SET NOCOUNT ON** tinha sem qualquer efeito ou diminuir o desempenho. Olá procedimento armazenado de teste foi simple com um único **inserir** comando a partir do parâmetro de valor de tabela Olá. É possível que mais complexos procedimentos armazenados seriam beneficiar esta instrução. Mas não parta do princípio que adicionar **SET NOCOUNT ON** tooyour armazenado procedimento automaticamente melhora o desempenho. toounderstand Olá efeito, testar o procedimento armazenado com e sem Olá **SET NOCOUNT ON** instrução.

## <a name="batching-scenarios"></a>Cenários de criação de batches
Olá secções seguintes descrevem como parâmetros de valor de tabela toouse em três cenários de aplicação. cenário primeiro Olá mostra como colocação em memória intermédia e criação de batches podem trabalhar em conjunto. cenário segundo Olá melhora o desempenho efetuando o detalhe do mestre de operações numa chamada de procedimento armazenado único. Olá final cenário mostra como toouse parâmetros de valor de tabela numa operação "UPSERT".

### <a name="buffering"></a>Colocação em memória intermédia
Apesar de existirem alguns cenários que são candidatos óbvios de criação de batches, há muitos cenários que podem tirar partido da criação de batches pelo processamento atrasado. No entanto, também processar atrasada acarreta um maior risco que há perdidos de dados de Olá no evento Olá de uma falha inesperada. É importante toounderstand este risco e considere consequências Olá.

Por exemplo, considere uma aplicação web que controla o histórico de navegação de Olá de cada utilizador. Em cada pedido de página aplicação Olá foi possível efetuar a vista de página de base de dados chamada toorecord Olá do utilizador. Mas, mais elevado desempenho e escalabilidade podem ser conseguidos através da memória intermédia de atividades de navegação dos utilizadores Olá e, em seguida, enviar esta base de dados de toohello dados em lotes. Pode acionar a atualização de base de dados de Olá por tempo decorrido e/ou tamanho da memória intermédia. Por exemplo, uma regra de especificar que esse batch Olá deve ser processada após 20 segundos ou quando a memória intermédia de Olá atinge 1000 itens.

seguinte Olá código de exemplo utiliza [extensões reativa - Rx](https://msdn.microsoft.com/data/gg577609) tooprocess colocado na memória intermédia eventos gerados por uma classe de monitorização. Olá quando a memória intermédia preenche ou um tempo limite for atingido, lote de Olá dos dados de utilizador é enviado toohello base de dados com um parâmetro de valor de tabela.

Olá os detalhes de navegação de utilizador modelos Olá NavHistoryData classe. Contém informações básicas, tais como o identificador de utilizador Olá, Olá URL acedidos e Olá tempo de acesso.

    public class NavHistoryData
    {
        public NavHistoryData(int userId, string url, DateTime accessTime)
        { UserId = userId; URL = url; AccessTime = accessTime; }
        public int UserId { get; set; }
        public string URL { get; set; }
        public DateTime AccessTime { get; set; }
    }

Olá NavHistoryDataMonitor classe é responsável pela base de dados do Olá utilizador navegação dados toohello da memória intermédia. Contém um método, RecordUserNavigationEntry, que responde ao gerar uma **OnAdded** eventos. Olá código seguinte mostra lógica de construtor de Olá que utiliza Rx toocreate uma coleção observable com base em eventos de Olá. Em seguida, subscreve coleção observable toothis com o método de memória intermédia de Olá. sobrecarga Olá Especifica que memória intermédia Olá deve ser enviada cada 20 segundos ou entradas de 1000.

    public NavHistoryDataMonitor()
    {
        var observableData =
            Observable.FromEventPattern<NavHistoryDataEventArgs>(this, "OnAdded");

        observableData.Buffer(TimeSpan.FromSeconds(20), 1000).Subscribe(Handler);           
    }

processador Olá converte todos os itens de Olá colocado na memória intermédia de um tipo de valor de tabela e, em seguida, passa este procedimento tooa armazenado do tipo que batch Olá de processos. Olá código seguinte mostra Olá concluir definição Olá NavHistoryDataEventArgs e classes de NavHistoryDataMonitor Olá.

    public class NavHistoryDataEventArgs : System.EventArgs
    {
        public NavHistoryDataEventArgs(NavHistoryData data) { Data = data; }
        public NavHistoryData Data { get; set; }
    }

    public class NavHistoryDataMonitor
    {
        public event EventHandler<NavHistoryDataEventArgs> OnAdded;

        public NavHistoryDataMonitor()
        {
            var observableData =
                Observable.FromEventPattern<NavHistoryDataEventArgs>(this, "OnAdded");

            observableData.Buffer(TimeSpan.FromSeconds(20), 1000).Subscribe(Handler);           
        }

        public void RecordUserNavigationEntry(NavHistoryData data)
        {    
            if (OnAdded != null)
                OnAdded(this, new NavHistoryDataEventArgs(data));
        }

        protected void Handler(IList<EventPattern<NavHistoryDataEventArgs>> items)
        {
            DataTable navHistoryBatch = new DataTable("NavigationHistoryBatch");
            navHistoryBatch.Columns.Add("UserId", typeof(int));
            navHistoryBatch.Columns.Add("URL", typeof(string));
            navHistoryBatch.Columns.Add("AccessTime", typeof(DateTime));
            foreach (EventPattern<NavHistoryDataEventArgs> item in items)
            {
                NavHistoryData data = item.EventArgs.Data;
                navHistoryBatch.Rows.Add(data.UserId, data.URL, data.AccessTime);
            }

            using (SqlConnection connection = new SqlConnection(CloudConfigurationManager.GetSetting("Sql.ConnectionString")))
            {
                connection.Open();

                SqlCommand cmd = new SqlCommand("sp_RecordUserNavigation", connection);
                cmd.CommandType = CommandType.StoredProcedure;

                cmd.Parameters.Add(
                    new SqlParameter()
                    {
                        ParameterName = "@NavHistoryBatch",
                        SqlDbType = SqlDbType.Structured,
                        TypeName = "NavigationHistoryTableType",
                        Value = navHistoryBatch,
                    });

                cmd.ExecuteNonQuery();
            }
        }
    }

toouse esta classe buffering, aplicação Olá cria um objeto de NavHistoryDataMonitor estático. Sempre que um utilizador acede a uma página aplicação Olá chama o método de NavHistoryDataMonitor.RecordUserNavigationEntry Olá. Olá, colocação em memória intermédia lógica prossegue tootake care of a enviar de base de dados de toohello estas entradas em lotes.

### <a name="master-detail"></a>Detalhe de principal
Parâmetros de valor de tabela são úteis para cenários de inserção simples. No entanto, pode ser mais difícil inserções toobatch que envolvem mais do que uma tabela. cenário de "mestre/Detalhes" Olá é um bom exemplo. tabela principal Olá identifica entidade principal Olá. Uma ou mais tabelas de detalhe armazenam mais dados sobre a entidade de Olá. Neste cenário, as relações de chave externas Impor relação Olá da entidade principal do detalhes tooa exclusivo. Considere uma versão simplificada da tabela PurchaseOrder e a respetiva tabela de OrderDetail associada. Olá Transact-SQL a seguir cria tabela de PurchaseOrder Olá com quatro colunas: OrderID, OrderDate, CustomerID e estado.

    CREATE TABLE [dbo].[PurchaseOrder](
    [OrderID] [int] IDENTITY(1,1) NOT NULL,
    [OrderDate] [datetime] NOT NULL,
    [CustomerID] [int] NOT NULL,
    [Status] [nvarchar](50) NOT NULL,
     CONSTRAINT [PrimaryKey_PurchaseOrder] 
    PRIMARY KEY CLUSTERED ( [OrderID] ASC ))

Cada ordem contém um ou mais compras de produto. Esta informação é capturada na tabela de PurchaseOrderDetail Olá. Olá seguir Transact-SQL cria tabela de PurchaseOrderDetail Olá com cinco colunas: OrderID, OrderDetailID, ProductID, UnitPrice e OrderQty.

    CREATE TABLE [dbo].[PurchaseOrderDetail](
    [OrderID] [int] NOT NULL,
    [OrderDetailID] [int] IDENTITY(1,1) NOT NULL,
    [ProductID] [int] NOT NULL,
    [UnitPrice] [money] NULL,
    [OrderQty] [smallint] NULL,
     CONSTRAINT [PrimaryKey_PurchaseOrderDetail] PRIMARY KEY CLUSTERED 
    ( [OrderID] ASC, [OrderDetailID] ASC ))

coluna de OrderID Olá na tabela de PurchaseOrderDetail Olá tem de referenciar uma ordem da tabela de PurchaseOrder Olá. Olá seguinte definição de uma chave externa impõe esta restrição.

    ALTER TABLE [dbo].[PurchaseOrderDetail]  WITH CHECK ADD 
    CONSTRAINT [FK_OrderID_PurchaseOrder] FOREIGN KEY([OrderID])
    REFERENCES [dbo].[PurchaseOrder] ([OrderID])

Nos parâmetros de valor de tabela de toouse de ordem, tem de ter um tipo de tabela definido pelo utilizador para cada tabela de destino.

    CREATE TYPE PurchaseOrderTableType AS TABLE 
    ( OrderID INT,
      OrderDate DATETIME,
      CustomerID INT,
      Status NVARCHAR(50) );
    GO

    CREATE TYPE PurchaseOrderDetailTableType AS TABLE 
    ( OrderID INT,
      ProductID INT,
      UnitPrice MONEY,
      OrderQty SMALLINT );
    GO

Em seguida, defina um procedimento armazenado que aceita tabelas destes tipos. Este procedimento permite que um lote de toolocally aplicação um conjunto de encomendas pendentes e detalhes da encomenda numa única chamada. Olá Transact-SQL seguinte fornece Olá declaração de procedimento armazenado concluído para este exemplo de ordem de compra.

    CREATE PROCEDURE sp_InsertOrdersBatch (
    @orders as PurchaseOrderTableType READONLY,
    @details as PurchaseOrderDetailTableType READONLY )
    AS
    SET NOCOUNT ON;

    -- Table that connects hello order identifiers in hello @orders
    -- table with hello actual order identifiers in hello PurchaseOrder table
    DECLARE @IdentityLink AS TABLE ( 
    SubmittedKey int, 
    ActualKey int, 
    RowNumber int identity(1,1)
    );

          -- Add new orders toohello PurchaseOrder table, storing hello actual
    -- order identifiers in hello @IdentityLink table   
    INSERT INTO PurchaseOrder ([OrderDate], [CustomerID], [Status])
    OUTPUT inserted.OrderID INTO @IdentityLink (ActualKey)
    SELECT [OrderDate], [CustomerID], [Status] FROM @orders ORDER BY OrderID;

    -- Match hello passed-in order identifiers with hello actual identifiers
    -- and complete hello @IdentityLink table for use with inserting hello details
    WITH OrderedRows As (
    SELECT OrderID, ROW_NUMBER () OVER (ORDER BY OrderID) As RowNumber 
    FROM @orders
    )
    UPDATE @IdentityLink SET SubmittedKey = M.OrderID
    FROM @IdentityLink L JOIN OrderedRows M ON L.RowNumber = M.RowNumber;

    -- Insert hello order details into hello PurchaseOrderDetail table, 
          -- using hello actual order identifiers of hello master table, PurchaseOrder
    INSERT INTO PurchaseOrderDetail (
    [OrderID],
    [ProductID],
    [UnitPrice],
    [OrderQty] )
    SELECT L.ActualKey, D.ProductID, D.UnitPrice, D.OrderQty
    FROM @details D
    JOIN @IdentityLink L ON L.SubmittedKey = D.OrderID;
    GO

Neste exemplo, Olá definida localmente @IdentityLink tabela armazena Olá OrderID os valores reais de linhas de Olá recentemente inserida. Estes identificadores de ordem são diferentes das Olá temporários OrderID valores Olá @orders e @details parâmetros de valor de tabela. Por este motivo, Olá @IdentityLink tabela, em seguida, liga-se os valores de OrderID Olá de Olá @orders toohello reais OrderID os valores de parâmetros para novas linhas de Olá na tabela de PurchaseOrder Olá. Após este passo, Olá @IdentityLink tabela pode facilitar inserir detalhes da encomenda Olá com Olá OrderID real que satisfaz a restrição de chave externa Olá.

Este procedimento armazenado pode ser utilizado a partir do código ou a partir de outras chamadas de Transact-SQL. Consulte a secção de parâmetros de valor de tabela de Olá deste documento para obter um exemplo de código. Olá Transact-SQL a seguir mostra como toocall Olá sp_InsertOrdersBatch.

    declare @orders as PurchaseOrderTableType
    declare @details as PurchaseOrderDetailTableType

    INSERT @orders 
    ([OrderID], [OrderDate], [CustomerID], [Status])
    VALUES(1, '1/1/2013', 1125, 'Complete'),
    (2, '1/13/2013', 348, 'Processing'),
    (3, '1/12/2013', 2504, 'Shipped')

    INSERT @details
    ([OrderID], [ProductID], [UnitPrice], [OrderQty])
    VALUES(1, 10, $11.50, 1),
    (1, 12, $1.58, 1),
    (2, 23, $2.57, 2),
    (3, 4, $10.00, 1)

    exec sp_InsertOrdersBatch @orders, @details

Esta solução permite toouse cada lote de um conjunto de valores de OrderID que começam em 1. Estes valores OrderID temporários descrevem as relações de Olá no lote de Olá, mas são determinados valores de OrderID reais Olá momento Olá da operação de inserção de Olá. Pode executar Olá instruções mesmas no exemplo anterior Olá repetidamente e gerar as ordens exclusivas na base de dados de Olá. Por este motivo, considere adicionar mais lógica código ou a base de dados, que impede as ordens duplicadas quando utilizar esta técnica de criação de batches.

Este exemplo demonstra que podem ser em ainda mais complexas operações de base de dados, tais como de detalhe do mestre de operações, de lotes utilizando os parâmetros de valor de tabela.

### <a name="upsert"></a>UPSERT
Outro cenário lotes envolve em simultâneo atualizar linhas existentes e inserir novas linhas. Esta operação é por vezes, referidos tooas uma operação de "UPSERT" (atualização + insert). Em vez de efetuar chamadas separado tooINSERT e a ATUALIZAÇÃO, a instrução de intercalação de Olá é melhor se adequam toothis tarefas. Olá instrução MERGE pode executar ambos os insert e operações numa única chamada de atualização.

Parâmetros de valor de tabela podem ser utilizados com Olá intercalação instrução tooperform atualiza e inserções. Por exemplo, considere uma tabela de empregado simplificada que contém Olá seguintes colunas: campo IDdeEmpregado, nome próprio, apelido, SocialSecurityNumber:

    CREATE TABLE [dbo].[Employee](
    [EmployeeID] [int] IDENTITY(1,1) NOT NULL,
    [FirstName] [nvarchar](50) NOT NULL,
    [LastName] [nvarchar](50) NOT NULL,
    [SocialSecurityNumber] [nvarchar](50) NOT NULL,
     CONSTRAINT [PrimaryKey_Employee] PRIMARY KEY CLUSTERED 
    ([EmployeeID] ASC ))

Neste exemplo, pode utilizar o facto de Olá que esse Olá SocialSecurityNumber é exclusivo tooperform uma intercalação das várias empregados. Em primeiro lugar, crie o tipo de tabela definido pelo utilizador Olá:

    CREATE TYPE EmployeeTableType AS TABLE 
    ( Employee_ID INT,
      FirstName NVARCHAR(50),
      LastName NVARCHAR(50),
      SocialSecurityNumber NVARCHAR(50) );
    GO

Em seguida, crie um procedimento armazenado ou escrever código que utiliza Olá atualização de Olá de tooperform de instrução de intercalação e insere. Olá exemplo seguinte utiliza instrução MERGE de Olá num parâmetro de valor de tabela, @employees, do tipo EmployeeTableType. Olá conteúdo Olá @employees tabela não são mostrados aqui.

    MERGE Employee AS target
    USING (SELECT [FirstName], [LastName], [SocialSecurityNumber] FROM @employees) 
    AS source ([FirstName], [LastName], [SocialSecurityNumber])
    ON (target.[SocialSecurityNumber] = source.[SocialSecurityNumber])
    WHEN MATCHED THEN 
    UPDATE SET
    target.FirstName = source.FirstName, 
    target.LastName = source.LastName
    WHEN NOT MATCHED THEN
       INSERT ([FirstName], [LastName], [SocialSecurityNumber])
       VALUES (source.[FirstName], source.[LastName], source.[SocialSecurityNumber]);

Para obter mais informações, consulte a documentação de Olá e exemplos de instrução de intercalação Olá. Embora Olá trabalho mesmo pode ser efetuado num passo vários armazenadas chamada de procedimento com as operações INSERT e ATUALIZAÇÃO separadas, Olá instrução MERGE é mais eficiente. Código de base de dados também pode construir chamadas de Transact-SQL que utilizem a instrução de intercalação de Olá diretamente, sem necessidade de dois chamadas de base de dados para inserir e a ATUALIZAÇÃO.

## <a name="recommendation-summary"></a>Recomendação resumo
Olá lista seguinte fornece um resumo das Olá criação de batches recomendações apresentadas neste tópico:

* Utilize a colocação em memória intermédia e criação de batches de desempenho de Olá tooincrease e a escalabilidade das aplicações de base de dados SQL.
* Compreenda fala Olá entre a criação de batches/colocação em memória intermédia e resiliência. Durante uma falha de função, o risco de Olá de perda de um lote não processado de dados críticos da empresa poderá compensar vantagem de desempenho de Olá de criação de batches.
* Tentativa de tookeep todas as chamadas toohello da base de dados dentro de uma latência de tooreduce único centro de dados.
* Se optar por uma única técnica de lotes, parâmetros de valor de tabela oferecem o melhor desempenho possível Olá e flexibilidade.
* Para mais rápido Olá inserir o desempenho, siga estas Diretrizes gerais, mas testar o cenário:
  * Para < 100 linhas, utilize um único comando INSERT parametrizado.
  * Para < 1000 linhas, utilize parâmetros de valor de tabela.
  * Para > = 1000 linhas, utilize SqlBulkCopy.
* Para atualizar e eliminar operações, utilize parâmetros de valor de tabela com a lógica de procedimento armazenado que determina a operação de correto Olá em cada linha no parâmetro de tabela Olá.
* Diretrizes de tamanho de lote:
  * Utilize Olá maiores batch tamanhos que façam sentido para a sua aplicação e os requisitos comerciais.
  * Obter saldo Olá desempenho de lotes grande com riscos de Olá de falhas temporárias ou catastrófica. O que é consequence Olá de novas tentativas ou perda de dados de Olá no lote de Olá? 
  * Teste Olá maior batch tamanho tooverify que a base de dados do SQL Server não rejeitá-lo.
  * Crie definições de configuração esse controlo de criação de batches, tais como o tamanho do lote Olá ou janela de tempo de colocação em memória intermédia Olá. Estas definições fornecem flexibilidade. Pode alterar Olá criação de batches de comportamento em produção sem voltar a implementar o serviço em nuvem Olá.
* Evite a execução paralela de lotes funcionar numa tabela na base de dados de um único. Se optar por toodivide um único lote em vários threads de trabalho, execute testes toodetermine Olá número ideal de threads. Depois de um limiar não especificado, mais threads irão diminuir o desempenho em vez de o aumente demasiado.
* Considere a memória intermédia de tamanho e a hora como uma forma de implementar a criação de batches para cenários mais.

## <a name="next-steps"></a>Passos seguintes
Este artigo concentra-se em como técnicas de programação e de design de base de dados relacionados toobatching pode melhorar o desempenho da aplicação e a escalabilidade. Mas este é um fator na sua estratégia geral. Para obter mais maneiras tooimprove desempenho e a escalabilidade, consulte [orientações de desempenho de SQL Database do Azure para bases de dados individuais](sql-database-performance-guidance.md) e [considerações sobre preço e desempenho de um conjunto elástico](sql-database-elastic-pool-guidance.md).

