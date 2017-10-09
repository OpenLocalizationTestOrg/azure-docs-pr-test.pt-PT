---
title: "Introdução à linguagem U-SQL | Microsoft Docs"
description: "Saiba Olá Noções básicas do Olá linguagem U-SQL."
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: saveenr
editor: cgronlun
ms.assetid: 57143396-ab86-47dd-b6f8-613ba28c28d2
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/23/2017
ms.author: saveenr
ms.openlocfilehash: 5edee0e0d85211e84b3d47895c53d71f0a19f083
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-u-sql"></a>Introdução ao U-SQL
U-SQL é uma linguagem que combina SQL declarativa com imperativo c# toolet a processa os dados em qualquer escala. Através de Olá dimensionável, consulta distribuída a capacidade de U-SQL, pode de analisar eficazmente os dados em arquivos relacionais, tais como SQL Database do Azure. Com o U-SQL, pode processar dados não estruturados ao aplicar o esquema na leitura e a inserção lógica personalizada e UDFs. Além disso, o U-SQL inclui extensibilidade dá-lhe controlo detalhado sobre como tooexecute à escala. 

## <a name="learning-resources"></a>Recursos de aprendizagem

* Olá [U-SQL Tutorial](http://aka.ms/usqltutorial) fornece instruções orientadas da maioria dos idiomas Olá U-SQL. Este documento é recomendado ler para todos os programadores que toolearn U-SQL.
* Para obter informações detalhadas sobre Olá **sintaxe de linguagem U-SQL**, consulte Olá [referência de linguagem U-SQL](http://go.microsoft.com/fwlink/p/?LinkId=691348).
* Olá toounderstand **philosophy de design do U-SQL**, consulte a mensagem de blogue do Visual Studio Olá [introdução de U-SQL – uma linguagem que facilita grande processamento de dados](https://blogs.msdn.microsoft.com/visualstudio/2015/09/28/introducing-u-sql-a-language-that-makes-big-data-processing-easy/).

## <a name="prerequisites"></a>Pré-requisitos

Antes de seguir exemplos de Olá U-SQL neste documento, leia e concluir [Tutorial: desenvolver scripts SQL-U utilizando ferramentas do Data Lake para Visual Studio](data-lake-analytics-data-lake-tools-get-started.md). Este tutorial explica mechanics Olá de utilizando U-SQL com o Azure Data Lake Tools para Visual Studio.

## <a name="your-first-u-sql-script"></a>O seu primeiro script U-SQL

Olá seguinte script U-SQL é simple e permite-nos analisar o idioma de Olá U-SQL muitos aspetos.

```
@searchlog =
    EXTRACT UserId          int,
            Start           DateTime,
            Region          string,
            Query           string,
            Duration        int?,
            Urls            string,
            ClickedUrls     string
    FROM "/Samples/Data/SearchLog.tsv"
    USING Extractors.Tsv();

OUTPUT @searchlog   
    too"/output/SearchLog-first-u-sql.csv"
    USING Outputters.Csv();
```

Este script não tem quaisquer passos de transformação. Também lê a partir do ficheiro de origem Olá chamado `SearchLog.tsv`, schematizes-lo e escreve Olá conjunto de linhas de volta para um ficheiro denominado SearchLog-first-u-sql.csv.

Tenha em atenção Olá ponto de interrogação seguinte toohello tipo de dados no Olá `Duration` campo. Significa que Olá `Duration` campo pode ser nulo.

### <a name="key-concepts"></a>Conceitos-chave
* **Variáveis de conjunto de linhas**: cada expressão de consulta que produz um conjunto de linhas pode ser atribuído tooa variável. U-SQL segue o padrão de nomenclatura variável Olá T-SQL (`@searchlog`, por exemplo) no script de Olá.
* Olá **EXTRAIR** lê dados a partir de um ficheiro de palavra-chave e define o esquema de Olá na leitura. `Extractors.Tsv`é um incorporada extrator de U-SQL para os ficheiros de separador separados-valor. Pode desenvolver extractors personalizados.
* Olá **saída** escreve dados a partir de um ficheiro de tooa do conjunto de linhas. `Outputters.Csv()`é um outputter toocreate incorporada do U-SQL com um ficheiro de valores separados por vírgulas. Pode desenvolver outputters personalizados.

### <a name="file-paths"></a>Caminhos de ficheiro

Olá EXTRAIR e instruções de saída utilizam caminhos de ficheiro. Caminhos de ficheiro podem ser absoluto ou relativo:

Este caminho absoluto do ficheiro seguinte refere-se o ficheiro tooa num com o nome do Data Lake Store `mystore`:

    adl://mystore.azuredatalakestore.net/Samples/Data/SearchLog.tsv

Este caminho de ficheiro seguintes começa com `"/"`. Refere-se tooa ficheiro na conta de Data Lake Store predefinida Olá:

    /output/SearchLog-first-u-sql.csv

## <a name="use-scalar-variables"></a>Utilizar variáveis escalares

Pode utilizar variáveis escalares como toomake bem a manutenção de script mais fácil. script de U-SQL anterior Olá também pode ser escrito como:

    DECLARE @in  string = "/Samples/Data/SearchLog.tsv";
    DECLARE @out string = "/output/SearchLog-scalar-variables.csv";

    @searchlog =
        EXTRACT UserId          int,
                Start           DateTime,
                Region          string,
                Query           string,
                Duration        int?,
                Urls            string,
                ClickedUrls     string
        FROM @in
        USING Extractors.Tsv();

    OUTPUT @searchlog   
        too@out
        USING Outputters.Csv();

## <a name="transform-rowsets"></a>Conjuntos de linhas de transformação

Utilize **SELECIONE** tootransform conjuntos de linhas:

    @searchlog =
        EXTRACT UserId          int,
                Start           DateTime,
                Region          string,
                Query           string,
                Duration        int?,
                Urls            string,
                ClickedUrls     string
        FROM "/Samples/Data/SearchLog.tsv"
        USING Extractors.Tsv();

    @rs1 =
        SELECT Start, Region, Duration
        FROM @searchlog
    WHERE Region == "en-gb";

    OUTPUT @rs1   
        too"/output/SearchLog-transform-rowsets.csv"
        USING Outputters.Csv();

Olá a cláusula WHERE utiliza um [expressão c# booleana](https://msdn.microsoft.com/library/6a71f45d.aspx). Pode utilizar Olá c# expressão idioma toodo as suas próprias expressões e funções. Mesmo pode efetuar uma filtragem mais complexas de excelência combinando-los com conjunctions lógicas (ANDs) e disjunctions (ORs).

Olá seguinte script utiliza o método de DateTime.Parse() Olá e um conjunto.

    @searchlog =
        EXTRACT UserId          int,
                Start           DateTime,
                Region          string,
                Query           string,
                Duration        int?,
                Urls            string,
                ClickedUrls     string
        FROM "/Samples/Data/SearchLog.tsv"
        USING Extractors.Tsv();

    @rs1 =
        SELECT Start, Region, Duration
        FROM @searchlog
    WHERE Region == "en-gb";

    @rs1 =
        SELECT Start, Region, Duration
        FROM @rs1
        WHERE Start >= DateTime.Parse("2012/02/16") AND Start <= DateTime.Parse("2012/02/17");

    OUTPUT @rs1   
        too"/output/SearchLog-transform-datetime.csv"
        USING Outputters.Csv();

 >[!NOTE]
 >consulta segundo Olá está a funcionar no resultado de Olá do Olá primeiro conjunto de linhas, que cria um compostos de Olá dois filtros. Também pode reutilizar um nome de variável e nomes de Olá passam lexically.

## <a name="aggregate-rowsets"></a>Conjuntos de linhas agregados
Oferece de U-SQL Olá familiar ORDER BY, GROUP BY e agregações.

Olá seguinte consulta localiza duração total Olá por região e, em seguida, apresenta superior Olá durações de cinco por ordem.

Conjuntos de linhas do U-SQL não conservar a sua ordem para a consulta seguinte Olá. Assim, tooorder uma saída, terá de tooadd ORDER BY toohello saída instrução:

    DECLARE @outpref string = "/output/Searchlog-aggregation";
    DECLARE @out1    string = @outpref+"_agg.csv";
    DECLARE @out2    string = @outpref+"_top5agg.csv";

    @searchlog =
        EXTRACT UserId          int,
                Start           DateTime,
                Region          string,
                Query           string,
                Duration        int?,
                Urls            string,
                ClickedUrls     string
        FROM "/Samples/Data/SearchLog.tsv"
        USING Extractors.Tsv();

    @rs1 =
        SELECT
            Region,
            SUM(Duration) AS TotalDuration
        FROM @searchlog
    GROUP BY Region;

    @res =
        SELECT *
        FROM @rs1
        ORDER BY TotalDuration DESC
        FETCH 5 ROWS;

    OUTPUT @rs1
        too@out1
        ORDER BY TotalDuration DESC
        USING Outputters.Csv();

    OUTPUT @res
        too@out2
        ORDER BY TotalDuration DESC
        USING Outputters.Csv();

Olá U-SQL ORDER BY cláusula necessita de utilizar a cláusula de obtenção de Olá numa expressão SELECT.

a cláusula de U-SQL ter Olá pode ser utilizado toorestrict Olá saída toogroups que satisfaçam a condição HAVING de Olá:

    @searchlog =
        EXTRACT UserId          int,
                Start           DateTime,
                Region          string,
                Query           string,
                Duration        int?,
                Urls            string,
                ClickedUrls     string
        FROM "/Samples/Data/SearchLog.tsv"
        USING Extractors.Tsv();

    @res =
        SELECT
            Region,
            SUM(Duration) AS TotalDuration
        FROM @searchlog
        GROUP BY Region
        HAVING SUM(Duration) > 200;

    OUTPUT @res
        too"/output/Searchlog-having.csv"
        ORDER BY TotalDuration DESC
        USING Outputters.Csv();

Para cenários avançados de agregação, consulte a documentação de referência Olá Olá U-SQL para [agregar, análise e as funções de referência](https://msdn.microsoft.com/en-us/library/azure/mt621335.aspx)

## <a name="next-steps"></a>Passos seguintes
* [Descrição geral do Microsoft Azure Data Lake Analytics](data-lake-analytics-overview.md)
* [Desenvolver scripts U-SQL com as Ferramentas do Data Lake para Visual Studio](data-lake-analytics-data-lake-tools-get-started.md)
