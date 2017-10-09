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
# <a name="get-started-with-u-sql"></a><span data-ttu-id="8f82e-103">Introdução ao U-SQL</span><span class="sxs-lookup"><span data-stu-id="8f82e-103">Get started with U-SQL</span></span>
<span data-ttu-id="8f82e-104">U-SQL é uma linguagem que combina SQL declarativa com imperativo c# toolet a processa os dados em qualquer escala.</span><span class="sxs-lookup"><span data-stu-id="8f82e-104">U-SQL is a language that combines declarative SQL with imperative C# toolet you process data at any scale.</span></span> <span data-ttu-id="8f82e-105">Através de Olá dimensionável, consulta distribuída a capacidade de U-SQL, pode de analisar eficazmente os dados em arquivos relacionais, tais como SQL Database do Azure.</span><span class="sxs-lookup"><span data-stu-id="8f82e-105">Through hello scalable, distributed-query capability of U-SQL, you can efficiently analyze data across relational stores such as Azure SQL Database.</span></span> <span data-ttu-id="8f82e-106">Com o U-SQL, pode processar dados não estruturados ao aplicar o esquema na leitura e a inserção lógica personalizada e UDFs.</span><span class="sxs-lookup"><span data-stu-id="8f82e-106">With U-SQL, you can process unstructured data by applying schema on read and inserting custom logic and UDFs.</span></span> <span data-ttu-id="8f82e-107">Além disso, o U-SQL inclui extensibilidade dá-lhe controlo detalhado sobre como tooexecute à escala.</span><span class="sxs-lookup"><span data-stu-id="8f82e-107">Additionally, U-SQL includes extensibility that gives you fine-grained control over how tooexecute at scale.</span></span> 

## <a name="learning-resources"></a><span data-ttu-id="8f82e-108">Recursos de aprendizagem</span><span class="sxs-lookup"><span data-stu-id="8f82e-108">Learning resources</span></span>

* <span data-ttu-id="8f82e-109">Olá [U-SQL Tutorial](http://aka.ms/usqltutorial) fornece instruções orientadas da maioria dos idiomas Olá U-SQL.</span><span class="sxs-lookup"><span data-stu-id="8f82e-109">hello [U-SQL Tutorial](http://aka.ms/usqltutorial) provides a guided walkthrough of most of hello U-SQL language.</span></span> <span data-ttu-id="8f82e-110">Este documento é recomendado ler para todos os programadores que toolearn U-SQL.</span><span class="sxs-lookup"><span data-stu-id="8f82e-110">This document is recommended reading for all developers wanting toolearn U-SQL.</span></span>
* <span data-ttu-id="8f82e-111">Para obter informações detalhadas sobre Olá **sintaxe de linguagem U-SQL**, consulte Olá [referência de linguagem U-SQL](http://go.microsoft.com/fwlink/p/?LinkId=691348).</span><span class="sxs-lookup"><span data-stu-id="8f82e-111">For detailed information about hello **U-SQL language syntax**, see hello [U-SQL Language Reference](http://go.microsoft.com/fwlink/p/?LinkId=691348).</span></span>
* <span data-ttu-id="8f82e-112">Olá toounderstand **philosophy de design do U-SQL**, consulte a mensagem de blogue do Visual Studio Olá [introdução de U-SQL – uma linguagem que facilita grande processamento de dados](https://blogs.msdn.microsoft.com/visualstudio/2015/09/28/introducing-u-sql-a-language-that-makes-big-data-processing-easy/).</span><span class="sxs-lookup"><span data-stu-id="8f82e-112">toounderstand hello **U-SQL design philosophy**, see hello Visual Studio blog post [Introducing U-SQL – A Language that makes Big Data Processing Easy](https://blogs.msdn.microsoft.com/visualstudio/2015/09/28/introducing-u-sql-a-language-that-makes-big-data-processing-easy/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8f82e-113">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="8f82e-113">Prerequisites</span></span>

<span data-ttu-id="8f82e-114">Antes de seguir exemplos de Olá U-SQL neste documento, leia e concluir [Tutorial: desenvolver scripts SQL-U utilizando ferramentas do Data Lake para Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="8f82e-114">Before you go through hello U-SQL samples in this document, read and complete [Tutorial: Develop U-SQL scripts using Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span></span> <span data-ttu-id="8f82e-115">Este tutorial explica mechanics Olá de utilizando U-SQL com o Azure Data Lake Tools para Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="8f82e-115">That tutorial explains hello mechanics of using U-SQL with Azure Data Lake Tools for Visual Studio.</span></span>

## <a name="your-first-u-sql-script"></a><span data-ttu-id="8f82e-116">O seu primeiro script U-SQL</span><span class="sxs-lookup"><span data-stu-id="8f82e-116">Your first U-SQL script</span></span>

<span data-ttu-id="8f82e-117">Olá seguinte script U-SQL é simple e permite-nos analisar o idioma de Olá U-SQL muitos aspetos.</span><span class="sxs-lookup"><span data-stu-id="8f82e-117">hello following U-SQL script is simple and lets us explore many aspects hello U-SQL language.</span></span>

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

<span data-ttu-id="8f82e-118">Este script não tem quaisquer passos de transformação.</span><span class="sxs-lookup"><span data-stu-id="8f82e-118">This script doesn't have any transformation steps.</span></span> <span data-ttu-id="8f82e-119">Também lê a partir do ficheiro de origem Olá chamado `SearchLog.tsv`, schematizes-lo e escreve Olá conjunto de linhas de volta para um ficheiro denominado SearchLog-first-u-sql.csv.</span><span class="sxs-lookup"><span data-stu-id="8f82e-119">It reads from hello source file called `SearchLog.tsv`, schematizes it, and writes hello rowset back into a file called SearchLog-first-u-sql.csv.</span></span>

<span data-ttu-id="8f82e-120">Tenha em atenção Olá ponto de interrogação seguinte toohello tipo de dados no Olá `Duration` campo.</span><span class="sxs-lookup"><span data-stu-id="8f82e-120">Notice hello question mark next toohello data type in hello `Duration` field.</span></span> <span data-ttu-id="8f82e-121">Significa que Olá `Duration` campo pode ser nulo.</span><span class="sxs-lookup"><span data-stu-id="8f82e-121">It means that hello `Duration` field could be null.</span></span>

### <a name="key-concepts"></a><span data-ttu-id="8f82e-122">Conceitos-chave</span><span class="sxs-lookup"><span data-stu-id="8f82e-122">Key concepts</span></span>
* <span data-ttu-id="8f82e-123">**Variáveis de conjunto de linhas**: cada expressão de consulta que produz um conjunto de linhas pode ser atribuído tooa variável.</span><span class="sxs-lookup"><span data-stu-id="8f82e-123">**Rowset variables**: Each query expression that produces a rowset can be assigned tooa variable.</span></span> <span data-ttu-id="8f82e-124">U-SQL segue o padrão de nomenclatura variável Olá T-SQL (`@searchlog`, por exemplo) no script de Olá.</span><span class="sxs-lookup"><span data-stu-id="8f82e-124">U-SQL follows hello T-SQL variable naming pattern (`@searchlog`, for example) in hello script.</span></span>
* <span data-ttu-id="8f82e-125">Olá **EXTRAIR** lê dados a partir de um ficheiro de palavra-chave e define o esquema de Olá na leitura.</span><span class="sxs-lookup"><span data-stu-id="8f82e-125">hello **EXTRACT** keyword reads data from a file and defines hello schema on read.</span></span> <span data-ttu-id="8f82e-126">`Extractors.Tsv`é um incorporada extrator de U-SQL para os ficheiros de separador separados-valor.</span><span class="sxs-lookup"><span data-stu-id="8f82e-126">`Extractors.Tsv` is a built-in U-SQL extractor for tab-separated-value files.</span></span> <span data-ttu-id="8f82e-127">Pode desenvolver extractors personalizados.</span><span class="sxs-lookup"><span data-stu-id="8f82e-127">You can develop custom extractors.</span></span>
* <span data-ttu-id="8f82e-128">Olá **saída** escreve dados a partir de um ficheiro de tooa do conjunto de linhas.</span><span class="sxs-lookup"><span data-stu-id="8f82e-128">hello **OUTPUT** writes data from a rowset tooa file.</span></span> <span data-ttu-id="8f82e-129">`Outputters.Csv()`é um outputter toocreate incorporada do U-SQL com um ficheiro de valores separados por vírgulas.</span><span class="sxs-lookup"><span data-stu-id="8f82e-129">`Outputters.Csv()` is a built-in U-SQL outputter toocreate a comma-separated-value file.</span></span> <span data-ttu-id="8f82e-130">Pode desenvolver outputters personalizados.</span><span class="sxs-lookup"><span data-stu-id="8f82e-130">You can develop custom outputters.</span></span>

### <a name="file-paths"></a><span data-ttu-id="8f82e-131">Caminhos de ficheiro</span><span class="sxs-lookup"><span data-stu-id="8f82e-131">File paths</span></span>

<span data-ttu-id="8f82e-132">Olá EXTRAIR e instruções de saída utilizam caminhos de ficheiro.</span><span class="sxs-lookup"><span data-stu-id="8f82e-132">hello EXTRACT and OUTPUT statements use file paths.</span></span> <span data-ttu-id="8f82e-133">Caminhos de ficheiro podem ser absoluto ou relativo:</span><span class="sxs-lookup"><span data-stu-id="8f82e-133">File paths can be absolute or relative:</span></span>

<span data-ttu-id="8f82e-134">Este caminho absoluto do ficheiro seguinte refere-se o ficheiro tooa num com o nome do Data Lake Store `mystore`:</span><span class="sxs-lookup"><span data-stu-id="8f82e-134">This following absolute file path refers tooa file in a Data Lake Store named `mystore`:</span></span>

    adl://mystore.azuredatalakestore.net/Samples/Data/SearchLog.tsv

<span data-ttu-id="8f82e-135">Este caminho de ficheiro seguintes começa com `"/"`.</span><span class="sxs-lookup"><span data-stu-id="8f82e-135">This following file path starts with `"/"`.</span></span> <span data-ttu-id="8f82e-136">Refere-se tooa ficheiro na conta de Data Lake Store predefinida Olá:</span><span class="sxs-lookup"><span data-stu-id="8f82e-136">It refers tooa file in hello default Data Lake Store account:</span></span>

    /output/SearchLog-first-u-sql.csv

## <a name="use-scalar-variables"></a><span data-ttu-id="8f82e-137">Utilizar variáveis escalares</span><span class="sxs-lookup"><span data-stu-id="8f82e-137">Use scalar variables</span></span>

<span data-ttu-id="8f82e-138">Pode utilizar variáveis escalares como toomake bem a manutenção de script mais fácil.</span><span class="sxs-lookup"><span data-stu-id="8f82e-138">You can use scalar variables as well toomake your script maintenance easier.</span></span> <span data-ttu-id="8f82e-139">script de U-SQL anterior Olá também pode ser escrito como:</span><span class="sxs-lookup"><span data-stu-id="8f82e-139">hello previous U-SQL script can also be written as:</span></span>

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

## <a name="transform-rowsets"></a><span data-ttu-id="8f82e-140">Conjuntos de linhas de transformação</span><span class="sxs-lookup"><span data-stu-id="8f82e-140">Transform rowsets</span></span>

<span data-ttu-id="8f82e-141">Utilize **SELECIONE** tootransform conjuntos de linhas:</span><span class="sxs-lookup"><span data-stu-id="8f82e-141">Use **SELECT** tootransform rowsets:</span></span>

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

<span data-ttu-id="8f82e-142">Olá a cláusula WHERE utiliza um [expressão c# booleana](https://msdn.microsoft.com/library/6a71f45d.aspx).</span><span class="sxs-lookup"><span data-stu-id="8f82e-142">hello WHERE clause uses a [C# Boolean expression](https://msdn.microsoft.com/library/6a71f45d.aspx).</span></span> <span data-ttu-id="8f82e-143">Pode utilizar Olá c# expressão idioma toodo as suas próprias expressões e funções.</span><span class="sxs-lookup"><span data-stu-id="8f82e-143">You can use hello C# expression language toodo your own expressions and functions.</span></span> <span data-ttu-id="8f82e-144">Mesmo pode efetuar uma filtragem mais complexas de excelência combinando-los com conjunctions lógicas (ANDs) e disjunctions (ORs).</span><span class="sxs-lookup"><span data-stu-id="8f82e-144">You can even perform more complex filtering by combining them with logical conjunctions (ANDs) and disjunctions (ORs).</span></span>

<span data-ttu-id="8f82e-145">Olá seguinte script utiliza o método de DateTime.Parse() Olá e um conjunto.</span><span class="sxs-lookup"><span data-stu-id="8f82e-145">hello following script uses hello DateTime.Parse() method and a conjunction.</span></span>

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
 ><span data-ttu-id="8f82e-146">consulta segundo Olá está a funcionar no resultado de Olá do Olá primeiro conjunto de linhas, que cria um compostos de Olá dois filtros.</span><span class="sxs-lookup"><span data-stu-id="8f82e-146">hello second query is operating on hello result of hello first rowset, which creates a composite of hello two filters.</span></span> <span data-ttu-id="8f82e-147">Também pode reutilizar um nome de variável e nomes de Olá passam lexically.</span><span class="sxs-lookup"><span data-stu-id="8f82e-147">You can also reuse a variable name, and hello names are scoped lexically.</span></span>

## <a name="aggregate-rowsets"></a><span data-ttu-id="8f82e-148">Conjuntos de linhas agregados</span><span class="sxs-lookup"><span data-stu-id="8f82e-148">Aggregate rowsets</span></span>
<span data-ttu-id="8f82e-149">Oferece de U-SQL Olá familiar ORDER BY, GROUP BY e agregações.</span><span class="sxs-lookup"><span data-stu-id="8f82e-149">U-SQL gives you hello familiar ORDER BY, GROUP BY, and aggregations.</span></span>

<span data-ttu-id="8f82e-150">Olá seguinte consulta localiza duração total Olá por região e, em seguida, apresenta superior Olá durações de cinco por ordem.</span><span class="sxs-lookup"><span data-stu-id="8f82e-150">hello following query finds hello total duration per region, and then displays hello top five durations in order.</span></span>

<span data-ttu-id="8f82e-151">Conjuntos de linhas do U-SQL não conservar a sua ordem para a consulta seguinte Olá.</span><span class="sxs-lookup"><span data-stu-id="8f82e-151">U-SQL rowsets do not preserve their order for hello next query.</span></span> <span data-ttu-id="8f82e-152">Assim, tooorder uma saída, terá de tooadd ORDER BY toohello saída instrução:</span><span class="sxs-lookup"><span data-stu-id="8f82e-152">Thus, tooorder an output, you need tooadd ORDER BY toohello OUTPUT statement:</span></span>

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

<span data-ttu-id="8f82e-153">Olá U-SQL ORDER BY cláusula necessita de utilizar a cláusula de obtenção de Olá numa expressão SELECT.</span><span class="sxs-lookup"><span data-stu-id="8f82e-153">hello U-SQL ORDER BY clause requires using hello FETCH clause in a SELECT expression.</span></span>

<span data-ttu-id="8f82e-154">a cláusula de U-SQL ter Olá pode ser utilizado toorestrict Olá saída toogroups que satisfaçam a condição HAVING de Olá:</span><span class="sxs-lookup"><span data-stu-id="8f82e-154">hello U-SQL HAVING clause can be used toorestrict hello output toogroups that satisfy hello HAVING condition:</span></span>

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

<span data-ttu-id="8f82e-155">Para cenários avançados de agregação, consulte a documentação de referência Olá Olá U-SQL para [agregar, análise e as funções de referência](https://msdn.microsoft.com/en-us/library/azure/mt621335.aspx)</span><span class="sxs-lookup"><span data-stu-id="8f82e-155">For advanced aggregation scenarios, see hello hello U-SQL reference documentation for [aggregate, analytic, and reference functions](https://msdn.microsoft.com/en-us/library/azure/mt621335.aspx)</span></span>

## <a name="next-steps"></a><span data-ttu-id="8f82e-156">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="8f82e-156">Next steps</span></span>
* [<span data-ttu-id="8f82e-157">Descrição geral do Microsoft Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="8f82e-157">Overview of Microsoft Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
* [<span data-ttu-id="8f82e-158">Desenvolver scripts U-SQL com as Ferramentas do Data Lake para Visual Studio</span><span class="sxs-lookup"><span data-stu-id="8f82e-158">Develop U-SQL scripts using Data Lake Tools for Visual Studio</span></span>](data-lake-analytics-data-lake-tools-get-started.md)
