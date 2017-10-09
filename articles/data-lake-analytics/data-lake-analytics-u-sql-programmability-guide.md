---
title: "Guia de programação para aaaU-SQL do Azure Data Lake | Microsoft Docs"
description: "Saiba mais sobre o conjunto de Olá de serviços no Azure Data Lake que lhe permitem toocreate uma plataforma de macrodados baseado na nuvem."
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: saveenr
ms.assetid: 63be271e-7c44-4d19-9897-c2913ee9599d
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/30/2017
ms.author: saveenr
ms.openlocfilehash: cc8f126234c6106a0dc633ce85a1d9ab1e634e30
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="u-sql-programmability-guide"></a><span data-ttu-id="654cf-103">Guia de programação para U-SQL</span><span class="sxs-lookup"><span data-stu-id="654cf-103">U-SQL programmability guide</span></span>

<span data-ttu-id="654cf-104">U-SQL é uma linguagem de consulta que foi concebida para o tipo de dados grande de cargas de trabalho.</span><span class="sxs-lookup"><span data-stu-id="654cf-104">U-SQL is a query language that's designed for big data-type of workloads.</span></span> <span data-ttu-id="654cf-105">Uma das funcionalidades de exclusivo Olá do U-SQL é a combinação de Olá de linguagem declarativa de como o SQL Olá com extensibilidade Olá e de programação para fornecida pelo c#.</span><span class="sxs-lookup"><span data-stu-id="654cf-105">One of hello unique features of U-SQL is hello combination of hello SQL-like declarative language with hello extensibility and programmability that's provided by C#.</span></span> <span data-ttu-id="654cf-106">Neste guia, iremos nos podermos concentrar nos extensibilidade Olá e de programação para de linguagem U-SQL Olá que está ativada por c#.</span><span class="sxs-lookup"><span data-stu-id="654cf-106">In this guide, we concentrate on hello extensibility and programmability of hello U-SQL language that's enabled by C#.</span></span>

## <a name="requirements"></a><span data-ttu-id="654cf-107">Requisitos</span><span class="sxs-lookup"><span data-stu-id="654cf-107">Requirements</span></span>

<span data-ttu-id="654cf-108">Transfira e instale [ferramentas do Azure Data Lake para Visual Studio](https://www.microsoft.com/download/details.aspx?id=49504).</span><span class="sxs-lookup"><span data-stu-id="654cf-108">Download and install [Azure Data Lake Tools for Visual Studio](https://www.microsoft.com/download/details.aspx?id=49504).</span></span>

## <a name="get-started-with-u-sql"></a><span data-ttu-id="654cf-109">Introdução ao U-SQL</span><span class="sxs-lookup"><span data-stu-id="654cf-109">Get started with U-SQL</span></span>  

<span data-ttu-id="654cf-110">Vamos ver Olá seguinte script U-SQL:</span><span class="sxs-lookup"><span data-stu-id="654cf-110">Let’s look at hello following U-SQL script:</span></span>

```
@a  = 
    SELECT * FROM 
        (VALUES
            ("Contoso",   1500.0, "2017-03-39"),
            ("Woodgrove", 2700.0, "2017-04-10")
        ) AS 
              D( customer, amount );
@results =
    SELECT
        customer,
    amount,
    date
    FROM @a;    
```

<span data-ttu-id="654cf-111">Define um conjunto de linhas chamado @a e cria um conjunto de linhas chamado @results de @a.</span><span class="sxs-lookup"><span data-stu-id="654cf-111">It defines a RowSet called @a and creates a RowSet called @results from @a.</span></span>

## <a name="c-types-and-expressions-in-u-sql-script"></a><span data-ttu-id="654cf-112">Tipos de c# e expressões no script U-SQL</span><span class="sxs-lookup"><span data-stu-id="654cf-112">C# types and expressions in U-SQL script</span></span>

<span data-ttu-id="654cf-113">Uma expressão de U-SQL é uma expressão de c# combinada com operações de lógicas de U-SQL, tais `AND`, `OR`, e `NOT`.</span><span class="sxs-lookup"><span data-stu-id="654cf-113">A U-SQL Expression is a C# expression combined with U-SQL logical operations such `AND`, `OR`, and `NOT`.</span></span> <span data-ttu-id="654cf-114">As expressões de U-SQL pode ser utilizadas com SELECIONE, a EXTRAIR, WHERE, tendo, agrupar por e declarar.</span><span class="sxs-lookup"><span data-stu-id="654cf-114">U-SQL Expressions can be used with SELECT, EXTRACT, WHERE, HAVING, GROUP BY and DECLARE.</span></span>

<span data-ttu-id="654cf-115">Por exemplo, Olá seguinte script analisa uma cadeia de um valor de DateTime na cláusula SELECT Olá.</span><span class="sxs-lookup"><span data-stu-id="654cf-115">For example, hello following script parses a string a DateTime value in hello SELECT clause.</span></span>

```
@results =
    SELECT
        customer,
    amount,
    DateTime.Parse(date) AS date
    FROM @a;    
```

<span data-ttu-id="654cf-116">Olá seguinte script analisa uma cadeia de um valor de DateTime numa instrução DECLARE.</span><span class="sxs-lookup"><span data-stu-id="654cf-116">hello following script parses a string a DateTime value in a DECLARE statement.</span></span>

```
DECLARE @d DateTime = ToDateTime.Date("2016/01/01");
```

### <a name="use-c-expressions-for-data-type-conversions"></a><span data-ttu-id="654cf-117">Utilizar c# expressões para conversões de tipo de dados</span><span class="sxs-lookup"><span data-stu-id="654cf-117">Use C# expressions for data type conversions</span></span>
<span data-ttu-id="654cf-118">Olá seguinte o exemplo demonstra como pode efetuar uma conversão de dados datetime através de expressões do c#.</span><span class="sxs-lookup"><span data-stu-id="654cf-118">hello following example demonstrates how you can do a datetime data conversion by using C# expressions.</span></span> <span data-ttu-id="654cf-119">Este cenário em particular, dados de datetime da cadeia são convertida toostandard datetime com notação de tempo de 00:00:00 meia-noite.</span><span class="sxs-lookup"><span data-stu-id="654cf-119">In this particular scenario, string datetime data is converted toostandard datetime with midnight 00:00:00 time notation.</span></span>

```
DECLARE @dt String = "2016-07-06 10:23:15";

@rs1 =
    SELECT 
        Convert.ToDateTime(Convert.ToDateTime(@dt).ToString("yyyy-MM-dd")) AS dt,
        dt AS olddt
    FROM @rs0;
OUTPUT @rs1 too@output_file USING Outputters.Text();
```

### <a name="use-c-expressions-for-todays-date"></a><span data-ttu-id="654cf-120">Utilizar expressões de c# para a data de hoje</span><span class="sxs-lookup"><span data-stu-id="654cf-120">Use C# expressions for today’s date</span></span>
<span data-ttu-id="654cf-121">toopull data de hoje, podemos utilizar Olá seguintes expressão c#:</span><span class="sxs-lookup"><span data-stu-id="654cf-121">toopull today’s date, we can use hello following C# expression:</span></span>

```
DateTime.Now.ToString("M/d/yyyy")
```

<span data-ttu-id="654cf-122">Eis um exemplo de como toouse esta expressão num script:</span><span class="sxs-lookup"><span data-stu-id="654cf-122">Here's an example of how toouse this expression in a script:</span></span>

```
@rs1 =
    SELECT
        MAX(guid) AS start_id,
        MIN(dt) AS start_time,
        MIN(Convert.ToDateTime(Convert.ToDateTime(dt<@default_dt?@default_dt:dt).ToString("yyyy-MM-dd"))) AS start_zero_time,
        MIN(USQL_Programmability.CustomFunctions.GetFiscalPeriod(dt)) AS start_fiscalperiod,
        DateTime.Now.ToString("M/d/yyyy") AS Nowdate,
        user,
        des
    FROM @rs0
    GROUP BY user, des;
```



## <a name="using-net-assemblies"></a><span data-ttu-id="654cf-123">Utilizar as assemblagens .NET</span><span class="sxs-lookup"><span data-stu-id="654cf-123">Using .NET assemblies</span></span>
<span data-ttu-id="654cf-124">Modelo de extensibilidade do U-SQL baseia-se descontos elevados no código personalizado do Olá capacidade tooadd.</span><span class="sxs-lookup"><span data-stu-id="654cf-124">U-SQL’s extensibility model relies heavily on hello ability tooadd custom code.</span></span> <span data-ttu-id="654cf-125">Atualmente, U-SQL proporciona formas fácil tooadd o seus próprios Microsoft. Código baseado na rede (em especial, c#).</span><span class="sxs-lookup"><span data-stu-id="654cf-125">Currently, U-SQL provides you with easy ways tooadd your own Microsoft .NET-based code (in particular, C#).</span></span> <span data-ttu-id="654cf-126">No entanto, também pode adicionar código personalizado escrito na outras linguagens .NET, tais como VB.NET ou F #.</span><span class="sxs-lookup"><span data-stu-id="654cf-126">However, you can also add custom code that's written in other .NET languages, such as VB.NET or F#.</span></span> 

### <a name="register-a-net-assembly"></a><span data-ttu-id="654cf-127">Registar uma assemblagem .NET</span><span class="sxs-lookup"><span data-stu-id="654cf-127">Register a .NET assembly</span></span>

<span data-ttu-id="654cf-128">Utilize Olá CREATE ASSEMBLY instrução tooplace uma assemblagem .NET numa base de dados U-SQL.</span><span class="sxs-lookup"><span data-stu-id="654cf-128">Use hello CREATE ASSEMBLY statement tooplace a .NET assembly into a U-SQL Database.</span></span> <span data-ttu-id="654cf-129">Depois de uma assemblagem numa base de dados, scripts U-SQL podem utilizar esses assemblagens utilizando a instrução da referência de ASSEMBLAGEM de Olá.</span><span class="sxs-lookup"><span data-stu-id="654cf-129">Once an assembly is in a database, U-SQL scripts can use those assemblies by using hello REFERENCE ASSEMBLY statement.</span></span> 

<span data-ttu-id="654cf-130">Olá a seguir mostra código como tooregister uma assemblagem:</span><span class="sxs-lookup"><span data-stu-id="654cf-130">hello following code shows how tooregister an assembly:</span></span>

```
CREATE ASSEMBLY MyDB.[MyAssembly]
    FROM "/myassembly.dll";
```

<span data-ttu-id="654cf-131">Olá a seguir mostra código como tooreference uma assemblagem:</span><span class="sxs-lookup"><span data-stu-id="654cf-131">hello following code shows how tooreference an assembly:</span></span>

```
REFERENCE ASSEMBLY MyDB.[MyAssembly];
```

<span data-ttu-id="654cf-132">Consulte Olá [instruções de registo de assemblagem](https://blogs.msdn.microsoft.com/azuredatalake/2016/08/26/how-to-register-u-sql-assemblies-in-your-u-sql-catalog/) que abrange este tópico em maior detalhe.</span><span class="sxs-lookup"><span data-stu-id="654cf-132">Consult hello [assembly registration instructions](https://blogs.msdn.microsoft.com/azuredatalake/2016/08/26/how-to-register-u-sql-assemblies-in-your-u-sql-catalog/) that covers this topic in greater detail.</span></span>


### <a name="use-assembly-versioning"></a><span data-ttu-id="654cf-133">Utilizar o controlo de versões da assemblagem</span><span class="sxs-lookup"><span data-stu-id="654cf-133">Use assembly versioning</span></span>
<span data-ttu-id="654cf-134">Atualmente, U-SQL utiliza a Olá .NET Framework versão 4.5.</span><span class="sxs-lookup"><span data-stu-id="654cf-134">Currently, U-SQL uses hello .NET Framework version 4.5.</span></span> <span data-ttu-id="654cf-135">Por isso, certifique-se de que os seus próprios assemblagens são compatíveis com que a versão do tempo de execução Olá.</span><span class="sxs-lookup"><span data-stu-id="654cf-135">So ensure that your own assemblies are compatible with that version of hello runtime.</span></span>

<span data-ttu-id="654cf-136">Conforme mencionado anteriormente, código de execuções de U-SQL num formato de 64 bits (x64).</span><span class="sxs-lookup"><span data-stu-id="654cf-136">As mentioned earlier, U-SQL runs code in a 64-bit (x64) format.</span></span> <span data-ttu-id="654cf-137">Por isso certifique-se de que o seu código é toorun compilado em x64.</span><span class="sxs-lookup"><span data-stu-id="654cf-137">So make sure that your code is compiled toorun on x64.</span></span> <span data-ttu-id="654cf-138">Caso contrário, obter o erro de formato incorreto Olá apresentado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="654cf-138">Otherwise you get hello incorrect format error shown earlier.</span></span>

<span data-ttu-id="654cf-139">Cada carregou a assemblagem DLL e ficheiro de recursos, tais como um tempo de execução diferente, uma assemblagem nativa ou um ficheiro de configuração, pode ter um máximo de 400 MB.</span><span class="sxs-lookup"><span data-stu-id="654cf-139">Each uploaded assembly DLL and resource file, such as a different runtime, a native assembly, or a config file, can be at most 400 MB.</span></span> <span data-ttu-id="654cf-140">tamanho total do Olá dos recursos implementados, ou através de implementar recursos através de tooassemblies referências e os ficheiros adicionais, não pode exceder 3 GB.</span><span class="sxs-lookup"><span data-stu-id="654cf-140">hello total size of deployed resources, either via DEPLOY RESOURCE or via references tooassemblies and their additional files, cannot exceed 3 GB.</span></span>

<span data-ttu-id="654cf-141">Por fim, tenha em atenção que cada base de dados do U-SQL só pode conter uma versão de qualquer assemblagem em questão.</span><span class="sxs-lookup"><span data-stu-id="654cf-141">Finally, note that each U-SQL database can only contain one version of any given assembly.</span></span> <span data-ttu-id="654cf-142">Por exemplo, se tiver a versão 7 e versão 8 do Olá biblioteca NewtonSoft Json.Net, terá de tooregistê-las em duas bases de dados diferentes.</span><span class="sxs-lookup"><span data-stu-id="654cf-142">For example, if you need both version 7 and version 8 of hello NewtonSoft Json.Net library, you need tooregister them in two different databases.</span></span> <span data-ttu-id="654cf-143">Além disso, cada script só pode fazer referência tooone versão de uma assemblagem em questão DLL.</span><span class="sxs-lookup"><span data-stu-id="654cf-143">Furthermore, each script can only refer tooone version of a given assembly DLL.</span></span> <span data-ttu-id="654cf-144">No que esta respeita o U-SQL segue Olá c# assemblagem gestão e o controlo de versões de semântica.</span><span class="sxs-lookup"><span data-stu-id="654cf-144">In this respect, U-SQL follows hello C# assembly management and versioning semantics.</span></span>


## <a name="use-user-defined-functions-udf"></a><span data-ttu-id="654cf-145">Utilize as funções definidas pelo utilizador: UDF</span><span class="sxs-lookup"><span data-stu-id="654cf-145">Use user-defined functions: UDF</span></span>
<span data-ttu-id="654cf-146">As funções definidas pelo utilizador do U-SQL ou UDF, são programação rotinas que aceitam parâmetros, execute uma ação (por exemplo, um cálculo complexo) e devolvem Olá resultado da ação como um valor.</span><span class="sxs-lookup"><span data-stu-id="654cf-146">U-SQL user-defined functions, or UDF, are programming routines that accept parameters, perform an action (such as a complex calculation), and return hello result of that action as a value.</span></span> <span data-ttu-id="654cf-147">Olá devolver o valor de UDF só pode ser uma escalar único.</span><span class="sxs-lookup"><span data-stu-id="654cf-147">hello return value of UDF can only be a single scalar.</span></span> <span data-ttu-id="654cf-148">U-SQL UDF pode ser chamado no script de base de U-SQL, como quaisquer outro c# função escalar.</span><span class="sxs-lookup"><span data-stu-id="654cf-148">U-SQL UDF can be called in U-SQL base script like any other C# scalar function.</span></span>

<span data-ttu-id="654cf-149">Recomendamos que inicializar U-SQL definidos pelo utilizador as funções como **pública** e **estático**.</span><span class="sxs-lookup"><span data-stu-id="654cf-149">We recommend that you initialize U-SQL user-defined functions as **public** and **static**.</span></span>

```
public static string MyFunction(string param1)
{
    return "my result";
}
```

<span data-ttu-id="654cf-150">Primeiro vamos ver exemplo simples de Olá de criação de um UDF.</span><span class="sxs-lookup"><span data-stu-id="654cf-150">First let’s look at hello simple example of creating a UDF.</span></span>

<span data-ttu-id="654cf-151">Neste cenário de caso de utilização, precisamos de toodetermine Olá fiscal período, incluindo trimestre fiscal Olá e mês fiscal de Olá primeiro início de sessão de utilizador específico Olá.</span><span class="sxs-lookup"><span data-stu-id="654cf-151">In this use-case scenario, we need toodetermine hello fiscal period, including hello fiscal quarter and fiscal month of hello first sign-in for hello specific user.</span></span> <span data-ttu-id="654cf-152">Olá primeiro mês fiscal do ano Olá no nosso cenário é Junho.</span><span class="sxs-lookup"><span data-stu-id="654cf-152">hello first fiscal month of hello year in our scenario is June.</span></span>

<span data-ttu-id="654cf-153">período de fiscal toocalculate, introduzirmos Olá c# função os seguintes:</span><span class="sxs-lookup"><span data-stu-id="654cf-153">toocalculate fiscal period, we introduce hello following C# function:</span></span>

```
public static string GetFiscalPeriod(DateTime dt)
{
    int FiscalMonth=0;
    if (dt.Month < 7)
    {
    FiscalMonth = dt.Month + 6;
    }
    else
    {
    FiscalMonth = dt.Month - 6;
    }

    int FiscalQuarter=0;
    if (FiscalMonth >=1 && FiscalMonth<=3)
    {
    FiscalQuarter = 1;
    }
    if (FiscalMonth >= 4 && FiscalMonth <= 6)
    {
    FiscalQuarter = 2;
    }
    if (FiscalMonth >= 7 && FiscalMonth <= 9)
    {
    FiscalQuarter = 3;
    }
    if (FiscalMonth >= 10 && FiscalMonth <= 12)
    {
    FiscalQuarter = 4;
    }

    return "Q" + FiscalQuarter.ToString() + ":P" + FiscalMonth.ToString();
}
```

<span data-ttu-id="654cf-154">Basta calcula mês fiscal e trimestre e devolve um valor de cadeia.</span><span class="sxs-lookup"><span data-stu-id="654cf-154">It simply calculates fiscal month and quarter and returns a string value.</span></span> <span data-ttu-id="654cf-155">Para Junho de Olá primeiro mês do Olá trimestre fiscal primeiro, vamos utilizar "Q1:P1".</span><span class="sxs-lookup"><span data-stu-id="654cf-155">For June, hello first month of hello first fiscal quarter, we use "Q1:P1".</span></span> <span data-ttu-id="654cf-156">Para Julho, iremos utilizar "Q1:P2" e assim sucessivamente.</span><span class="sxs-lookup"><span data-stu-id="654cf-156">For July, we use "Q1:P2", and so on.</span></span>

<span data-ttu-id="654cf-157">Este é uma regular função de c# que iremos são curso toouse no nosso projeto U-SQL.</span><span class="sxs-lookup"><span data-stu-id="654cf-157">This is a regular C# function that we are going toouse in our U-SQL project.</span></span>

<span data-ttu-id="654cf-158">Eis o aspeto da secção de code-behind Olá neste cenário:</span><span class="sxs-lookup"><span data-stu-id="654cf-158">Here is how hello code-behind section looks in this scenario:</span></span>

```
using Microsoft.Analytics.Interfaces;
using Microsoft.Analytics.Types.Sql;
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;

namespace USQL_Programmability
{
    public class CustomFunctions
    {
        public static string GetFiscalPeriod(DateTime dt)
        {
            int FiscalMonth=0;
            if (dt.Month < 7)
            {
                FiscalMonth = dt.Month + 6;
            }
            else
            {
                FiscalMonth = dt.Month - 6;
            }

            int FiscalQuarter=0;
            if (FiscalMonth >=1 && FiscalMonth<=3)
            {
                FiscalQuarter = 1;
            }
            if (FiscalMonth >= 4 && FiscalMonth <= 6)
            {
                FiscalQuarter = 2;
            }
            if (FiscalMonth >= 7 && FiscalMonth <= 9)
            {
                FiscalQuarter = 3;
            }
            if (FiscalMonth >= 10 && FiscalMonth <= 12)
            {
                FiscalQuarter = 4;
            }

            return "Q" + FiscalQuarter.ToString() + ":" + FiscalMonth.ToString();
        }

    }

}
```

<span data-ttu-id="654cf-159">Agora, vamos toocall esta função de script de U-SQL base Olá.</span><span class="sxs-lookup"><span data-stu-id="654cf-159">Now we are going toocall this function from hello base U-SQL script.</span></span> <span data-ttu-id="654cf-160">toodo isto, temos tooprovide um nome completamente qualificado para a função de Olá, incluindo o espaço de nomes de Olá, que neste caso é NameSpace.Class.Function(parameter).</span><span class="sxs-lookup"><span data-stu-id="654cf-160">toodo this, we have tooprovide a fully qualified name for hello function, including hello namespace, which in this case is NameSpace.Class.Function(parameter).</span></span>

```
USQL_Programmability.CustomFunctions.GetFiscalPeriod(dt)
```

<span data-ttu-id="654cf-161">Segue-se as real script base de U-SQL de Olá:</span><span class="sxs-lookup"><span data-stu-id="654cf-161">Following is hello actual U-SQL base script:</span></span>

```
DECLARE @input_file string = @"\usql-programmability\input_file.tsv";
DECLARE @output_file string = @"\usql-programmability\output_file.tsv";

@rs0 =
    EXTRACT
            guid Guid,
        dt DateTime,
            user String,
            des String
    FROM @input_file USING Extractors.Tsv();

DECLARE @default_dt DateTime = Convert.ToDateTime("06/01/2016");

@rs1 =
    SELECT
        MAX(guid) AS start_id,
    MIN(dt) AS start_time,
        MIN(Convert.ToDateTime(Convert.ToDateTime(dt<@default_dt?@default_dt:dt).ToString("yyyy-MM-dd"))) AS start_zero_time,
        MIN(USQL_Programmability.CustomFunctions.GetFiscalPeriod(dt)) AS start_fiscalperiod,
        user,
        des
    FROM @rs0
    GROUP BY user, des;

OUTPUT @rs1 
    too@output_file 
    USING Outputters.Text();
```

<span data-ttu-id="654cf-162">Segue-se Olá o ficheiro de saída Olá da execução do script:</span><span class="sxs-lookup"><span data-stu-id="654cf-162">Following is hello output file of hello script execution:</span></span>

```
0d8b9630-d5ca-11e5-8329-251efa3a2941,2016-02-11T07:04:17.2630000-08:00,2016-06-01T00:00:00.0000000,"Q3:8","User1",""

20843640-d771-11e5-b87b-8b7265c75a44,2016-02-11T07:04:17.2630000-08:00,2016-06-01T00:00:00.0000000,"Q3:8","User2",""

301f23d2-d690-11e5-9a98-4b4f60a1836f,2016-02-11T09:01:33.9720000-08:00,2016-06-01T00:00:00.0000000,"Q3:8","User3",""
```

<span data-ttu-id="654cf-163">Este exemplo demonstra a utilização de um simple de inline UDF em U-SQL.</span><span class="sxs-lookup"><span data-stu-id="654cf-163">This example demonstrates a simple usage of inline UDF in U-SQL.</span></span>

### <a name="keep-state-between-udf-invocations"></a><span data-ttu-id="654cf-164">Manter o estado entre invocações de UDF</span><span class="sxs-lookup"><span data-stu-id="654cf-164">Keep state between UDF invocations</span></span>
<span data-ttu-id="654cf-165">Objetos de programação para c# do U-SQL podem ser mais sofisticados, a utilização de interatividade através de variáveis globais do Olá code-behind.</span><span class="sxs-lookup"><span data-stu-id="654cf-165">U-SQL C# programmability objects can be more sophisticated, utilizing interactivity through hello code-behind global variables.</span></span> <span data-ttu-id="654cf-166">Vamos ver Olá seguir o cenário de caso de utilização de negócio.</span><span class="sxs-lookup"><span data-stu-id="654cf-166">Let’s look at hello following business use-case scenario.</span></span>

<span data-ttu-id="654cf-167">Em grandes organizações, os utilizadores podem alternar entre varieties de aplicações internas.</span><span class="sxs-lookup"><span data-stu-id="654cf-167">In large organizations, users can switch between varieties of internal applications.</span></span> <span data-ttu-id="654cf-168">Pode incluir Microsoft Dynamics CRM, PowerBI e assim sucessivamente.</span><span class="sxs-lookup"><span data-stu-id="654cf-168">These can include Microsoft Dynamics CRM, PowerBI, and so on.</span></span> <span data-ttu-id="654cf-169">Os clientes poderão pretendem tooapply uma análise de telemetria do modo como os utilizadores alternar entre aplicações diferentes, tendências de utilização que Olá estão e assim sucessivamente.</span><span class="sxs-lookup"><span data-stu-id="654cf-169">Customers might want tooapply a telemetry analysis of how users switch between different applications, what hello usage trends are, and so on.</span></span> <span data-ttu-id="654cf-170">objetivo de Hello para empresas Olá é toooptimize da utilização da aplicação.</span><span class="sxs-lookup"><span data-stu-id="654cf-170">hello goal for hello business is toooptimize application usage.</span></span> <span data-ttu-id="654cf-171">Também poderá pretendem toocombine diferentes aplicações ou rotinas de início de sessão específicas.</span><span class="sxs-lookup"><span data-stu-id="654cf-171">They also might want toocombine different applications or specific sign-on routines.</span></span>

<span data-ttu-id="654cf-172">tooachieve neste objetivo, temos toodetermine IDs de sessão e do desfasamento de tempo entre Olá última sessão que ocorreram.</span><span class="sxs-lookup"><span data-stu-id="654cf-172">tooachieve this goal, we have toodetermine session IDs and lag time between hello last session that occurred.</span></span>

<span data-ttu-id="654cf-173">Vamos precisar toofind uma anterior início de sessão e, em seguida, atribuir este sessões de início de sessão tooall que estão a ser gerado toohello mesma aplicação.</span><span class="sxs-lookup"><span data-stu-id="654cf-173">We need toofind a previous sign-in and then assign this sign-in tooall sessions that are being generated toohello same application.</span></span> <span data-ttu-id="654cf-174">primeiro desafio de Olá é que script U-SQL de base não permite-nos cálculos tooapply por colunas calculadas já com a função LAG.</span><span class="sxs-lookup"><span data-stu-id="654cf-174">hello first challenge is that U-SQL base script doesn't allow us tooapply calculations over already-calculated columns with LAG function.</span></span> <span data-ttu-id="654cf-175">Olá segundo desafio é que temos tookeep Olá específica de sessão para todas as sessões dentro Olá mesmo período de tempo.</span><span class="sxs-lookup"><span data-stu-id="654cf-175">hello second challenge is that we have tookeep hello specific session for all sessions within hello same time period.</span></span>

<span data-ttu-id="654cf-176">toosolve este problema, vamos utilizar uma variável global dentro de uma secção code-behind: `static public string globalSession;`.</span><span class="sxs-lookup"><span data-stu-id="654cf-176">toosolve this problem, we use a global variable inside a code-behind section: `static public string globalSession;`.</span></span>

<span data-ttu-id="654cf-177">Esta variável global é o conjunto de linhas completa do toohello aplicadas durante a execução do script do nosso.</span><span class="sxs-lookup"><span data-stu-id="654cf-177">This global variable is applied toohello entire rowset during our script execution.</span></span>

<span data-ttu-id="654cf-178">Segue-se a secção do code-behind Olá nosso programa U-SQL:</span><span class="sxs-lookup"><span data-stu-id="654cf-178">Here is hello code-behind section of our U-SQL program:</span></span>

```
using Microsoft.Analytics.Interfaces;
using Microsoft.Analytics.Types.Sql;
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;

namespace USQLApplication21
{
    public class UserSession
    {
        static public string globalSession;
        static public string StampUserSession(string eventTime, string PreviousRow, string Session)
        {

            if (!string.IsNullOrEmpty(PreviousRow))
            {
                double timeGap = Convert.ToDateTime(eventTime).Subtract(Convert.ToDateTime(PreviousRow)).TotalMinutes;
                if (timeGap <= 60) {return Session;}
                else {return Guid.NewGuid().ToString();}
            }
            else {return Guid.NewGuid().ToString();}

        }

        static public string getStampUserSession(string Session)
        {
            if (Session != globalSession && !string.IsNullOrEmpty(Session)) { globalSession = Session; }
            return globalSession;
        }

    }
}
```

<span data-ttu-id="654cf-179">Este exemplo mostra Olá variável global `static public string globalSession;` utilizado dentro de Olá `getStampUserSession` função e a obter reinicializados cada Olá tempo sessão parâmetro é alterado.</span><span class="sxs-lookup"><span data-stu-id="654cf-179">This example shows hello global variable `static public string globalSession;` used inside hello `getStampUserSession` function and getting reinitialized each time hello Session parameter is changed.</span></span>

<span data-ttu-id="654cf-180">Olá script U-SQL de base é o seguinte:</span><span class="sxs-lookup"><span data-stu-id="654cf-180">hello U-SQL base script is as follows:</span></span>

```
DECLARE @in string = @"\UserSession\test1.tsv";
DECLARE @out1 string = @"\UserSession\Out1.csv";
DECLARE @out2 string = @"\UserSession\Out2.csv";
DECLARE @out3 string = @"\UserSession\Out3.csv";

@records =
    EXTRACT DataId string,
            EventDateTime string,           
            UserName string,
            UserSessionTimestamp string

    FROM @in
    USING Extractors.Tsv();

@rs1 =
    SELECT 
        EventDateTime,
        UserName,
    LAG(EventDateTime, 1) 
        OVER(PARTITION BY UserName ORDER BY EventDateTime ASC) AS prevDateTime,          
        string.IsNullOrEmpty(LAG(EventDateTime, 1) 
        OVER(PARTITION BY UserName ORDER BY EventDateTime ASC)) AS Flag,           
        USQLApplication21.UserSession.StampUserSession
           (
            EventDateTime,
            LAG(EventDateTime, 1) OVER(PARTITION BY UserName ORDER BY EventDateTime ASC),
            LAG(UserSessionTimestamp, 1) OVER(PARTITION BY UserName ORDER BY EventDateTime ASC)
           ) AS UserSessionTimestamp
    FROM @records;

@rs2 =
    SELECT 
        EventDateTime,
        UserName,
        LAG(EventDateTime, 1) 
        OVER(PARTITION BY UserName ORDER BY EventDateTime ASC) AS prevDateTime,
        string.IsNullOrEmpty( LAG(EventDateTime, 1) OVER(PARTITION BY UserName ORDER BY EventDateTime ASC)) AS Flag,
        USQLApplication21.UserSession.getStampUserSession(UserSessionTimestamp) AS UserSessionTimestamp
    FROM @rs1
    WHERE UserName != "UserName";

OUTPUT @rs2
    too@out2
    ORDER BY UserName, EventDateTime ASC
    USING Outputters.Csv();
```

<span data-ttu-id="654cf-181">Função `USQLApplication21.UserSession.getStampUserSession(UserSessionTimestamp)` é chamado aqui durante o cálculo de conjunto de linhas de memória Olá segundo.</span><span class="sxs-lookup"><span data-stu-id="654cf-181">Function `USQLApplication21.UserSession.getStampUserSession(UserSessionTimestamp)` is called here during hello second memory rowset calculation.</span></span> <span data-ttu-id="654cf-182">Tenha sido enviado Olá `UserSessionTimestamp` coluna e devolve Olá valor até `UserSessionTimestamp` foi alterada.</span><span class="sxs-lookup"><span data-stu-id="654cf-182">It passes hello `UserSessionTimestamp` column and returns hello value until `UserSessionTimestamp` has changed.</span></span>

<span data-ttu-id="654cf-183">ficheiro de saída Olá é o seguinte:</span><span class="sxs-lookup"><span data-stu-id="654cf-183">hello output file is as follows:</span></span>

```
"2016-02-19T07:32:36.8420000-08:00","User1",,True,"72a0660e-22df-428e-b672-e0977007177f"
"2016-02-17T11:52:43.6350000-08:00","User2",,True,"4a0cd19a-6e67-4d95-a119-4eda590226ba"
"2016-02-17T11:59:08.8320000-08:00","User2","2016-02-17T11:52:43.6350000-08:00",False,"4a0cd19a-6e67-4d95-a119-4eda590226ba"
"2016-02-11T07:04:17.2630000-08:00","User3",,True,"51860a7a-1610-4f74-a9ea-69d5eef7cd9c"
"2016-02-11T07:10:33.9720000-08:00","User3","2016-02-11T07:04:17.2630000-08:00",False,"51860a7a-1610-4f74-a9ea-69d5eef7cd9c"
"2016-02-15T21:27:41.8210000-08:00","User3","2016-02-11T07:10:33.9720000-08:00",False,"4d2bc48d-bdf3-4591-a9c1-7b15ceb8e074"
"2016-02-16T05:48:49.6360000-08:00","User3","2016-02-15T21:27:41.8210000-08:00",False,"dd3006d0-2dcd-42d0-b3a2-bc03dd77c8b9"
"2016-02-16T06:22:43.6390000-08:00","User3","2016-02-16T05:48:49.6360000-08:00",False,"dd3006d0-2dcd-42d0-b3a2-bc03dd77c8b9"
"2016-02-17T16:29:53.2280000-08:00","User3","2016-02-16T06:22:43.6390000-08:00",False,"2fa899c7-eecf-4b1b-a8cd-30c5357b4f3a"
"2016-02-17T16:39:07.2430000-08:00","User3","2016-02-17T16:29:53.2280000-08:00",False,"2fa899c7-eecf-4b1b-a8cd-30c5357b4f3a"
"2016-02-17T17:20:39.3220000-08:00","User3","2016-02-17T16:39:07.2430000-08:00",False,"2fa899c7-eecf-4b1b-a8cd-30c5357b4f3a"
"2016-02-19T05:23:54.5710000-08:00","User3","2016-02-17T17:20:39.3220000-08:00",False,"6ca7ed80-c149-4c22-b24b-94ff5b0d824d"
"2016-02-19T05:48:37.7510000-08:00","User3","2016-02-19T05:23:54.5710000-08:00",False,"6ca7ed80-c149-4c22-b24b-94ff5b0d824d"
"2016-02-19T06:40:27.4830000-08:00","User3","2016-02-19T05:48:37.7510000-08:00",False,"6ca7ed80-c149-4c22-b24b-94ff5b0d824d"
"2016-02-19T07:27:37.7550000-08:00","User3","2016-02-19T06:40:27.4830000-08:00",False,"6ca7ed80-c149-4c22-b24b-94ff5b0d824d"
"2016-02-19T19:35:40.9450000-08:00","User3","2016-02-19T07:27:37.7550000-08:00",False,"3f385f0b-3e68-4456-ac74-ff6cef093674"
"2016-02-20T00:07:37.8250000-08:00","User3","2016-02-19T19:35:40.9450000-08:00",False,"685f76d5-ca48-4c58-b77d-bd3a9ddb33da"
"2016-02-11T09:01:33.9720000-08:00","User4",,True,"9f0cf696-c8ba-449a-8d5f-1ca6ed8f2ee8"
"2016-02-17T06:30:38.6210000-08:00","User4","2016-02-11T09:01:33.9720000-08:00",False,"8b11fd2a-01bf-4a5e-a9af-3c92c4e4382a"
"2016-02-17T22:15:26.4020000-08:00","User4","2016-02-17T06:30:38.6210000-08:00",False,"4e1cb707-3b5f-49c1-90c7-9b33b86ca1f4"
"2016-02-18T14:37:27.6560000-08:00","User4","2016-02-17T22:15:26.4020000-08:00",False,"f4e44400-e837-40ed-8dfd-2ea264d4e338"
"2016-02-19T01:20:31.4800000-08:00","User4","2016-02-18T14:37:27.6560000-08:00",False,"2136f4cf-7c7d-43c1-8ae2-08f4ad6a6e08"
```

<span data-ttu-id="654cf-184">Este exemplo demonstra um cenário de caso de utilização mais complicado que utilizamos uma variável global dentro de uma secção de code-behind que é o conjunto de linhas do toohello aplicados memória completo.</span><span class="sxs-lookup"><span data-stu-id="654cf-184">This example demonstrates a more complicated use-case scenario in which we use a global variable inside a code-behind section that's applied toohello entire memory rowset.</span></span>

## <a name="use-user-defined-types-udt"></a><span data-ttu-id="654cf-185">Utilizar tipos definidos pelo utilizador: UDT</span><span class="sxs-lookup"><span data-stu-id="654cf-185">Use user-defined types: UDT</span></span>
<span data-ttu-id="654cf-186">Os tipos definidos pelo utilizador ou UDT, é outra programação para funcionalidade do U-SQL.</span><span class="sxs-lookup"><span data-stu-id="654cf-186">User-defined types, or UDT, is another programmability feature of U-SQL.</span></span> <span data-ttu-id="654cf-187">U-SQL UDT funciona como um regular c# definido pelo utilizador tipo.</span><span class="sxs-lookup"><span data-stu-id="654cf-187">U-SQL UDT acts like a regular C# user-defined type.</span></span> <span data-ttu-id="654cf-188">C# é uma linguagem com tipo seguro que permita a utilização de Olá dos tipos de incorporadas e personalizadas definidas pelo utilizador.</span><span class="sxs-lookup"><span data-stu-id="654cf-188">C# is a strongly typed language that allows hello use of built-in and custom user-defined types.</span></span>

<span data-ttu-id="654cf-189">U-SQL implicitamente não é possível serializar ou anular a serialização UDTs arbitrários quando Olá UDT é transferida entre vértices em conjuntos de linhas.</span><span class="sxs-lookup"><span data-stu-id="654cf-189">U-SQL cannot implicitly serialize or de-serialize arbitrary UDTs when hello UDT is passed between vertices in rowsets.</span></span> <span data-ttu-id="654cf-190">Isto significa que o utilizador Olá tem tooprovide um formatador explícita utilizando Olá IFormatter interface.</span><span class="sxs-lookup"><span data-stu-id="654cf-190">This means that hello user has tooprovide an explicit formatter by using hello IFormatter interface.</span></span> <span data-ttu-id="654cf-191">Isto fornece o U-SQL com Olá serializar e anular a serialização métodos para Olá UDT.</span><span class="sxs-lookup"><span data-stu-id="654cf-191">This provides U-SQL with hello serialize and de-serialize methods for hello UDT.</span></span>

> [!NOTE]
> <span data-ttu-id="654cf-192">U-SQL extractors incorporadas e outputters atualmente não é possível serializar ou anular a serialização UDT tooor de dados de ficheiros, mesmo com Olá IFormatter conjunto.</span><span class="sxs-lookup"><span data-stu-id="654cf-192">U-SQL’s built-in extractors and outputters currently cannot serialize or de-serialize UDT data tooor from files even with hello IFormatter set.</span></span> <span data-ttu-id="654cf-193">Assim, quando estiver a escrever o ficheiro de tooa de dados UDT com Olá declaração de saída ou lê-lo com um extrator, tiver toopass-o como uma matriz de cadeia ou bytes.</span><span class="sxs-lookup"><span data-stu-id="654cf-193">So when you're writing UDT data tooa file with hello OUTPUT statement, or reading it with an extractor, you have toopass it as a string or byte array.</span></span> <span data-ttu-id="654cf-194">Em seguida, chame serialização Olá e anulação da serialização da código (ou seja, método ToString () do Olá UDT) explicitamente.</span><span class="sxs-lookup"><span data-stu-id="654cf-194">Then you call hello serialization and deserialization code (that is, hello UDT’s ToString() method) explicitly.</span></span> <span data-ttu-id="654cf-195">Definido pelo utilizador extractors e outputters, no Olá outro entregar, podem ler e escrever UDTs.</span><span class="sxs-lookup"><span data-stu-id="654cf-195">User-defined extractors and outputters, on hello other hand, can read and write UDTs.</span></span>

<span data-ttu-id="654cf-196">Se vamos tentar toouse UDT EXTRATOR ou OUTPUTTER (fora SELECIONE anterior), conforme mostrado aqui:</span><span class="sxs-lookup"><span data-stu-id="654cf-196">If we try toouse UDT in EXTRACTOR or OUTPUTTER (out of previous SELECT), as shown here:</span></span>

```
@rs1 =
    SELECT 
        MyNameSpace.Myfunction_Returning_UDT(filed1) AS myfield
    FROM @rs0;

OUTPUT @rs1 
    too@output_file 
    USING Outputters.Text();
```

<span data-ttu-id="654cf-197">Recebemos Olá seguinte erro:</span><span class="sxs-lookup"><span data-stu-id="654cf-197">We receive hello following error:</span></span>

```
Error   1   E_CSC_USER_INVALIDTYPEINOUTPUTTER: Outputters.Text was used toooutput column myfield of type
MyNameSpace.Myfunction_Returning_UDT.

Description:

Outputters.Text only supports built-in types.

Resolution:

Implement a custom outputter that knows how tooserialize this type, or call a serialization method on hello type in
hello preceding SELECT. C:\Users\sergeypu\Documents\Visual Studio 2013\Projects\USQL-Programmability\
USQL-Programmability\Types.usql 52  1   USQL-Programmability
```

<span data-ttu-id="654cf-198">toowork com UDT no outputter, podemos ter tooserialize-toostring com Olá método ToString () ou criar um outputter personalizado.</span><span class="sxs-lookup"><span data-stu-id="654cf-198">toowork with UDT in outputter, we either have tooserialize it toostring with hello ToString() method or create a custom outputter.</span></span>

<span data-ttu-id="654cf-199">UDTs atualmente não é possível utilizar GROUP BY.</span><span class="sxs-lookup"><span data-stu-id="654cf-199">UDTs currently cannot be used in GROUP BY.</span></span> <span data-ttu-id="654cf-200">Se for utilizado UDT no GROUP BY, é emitida Olá seguinte erro:</span><span class="sxs-lookup"><span data-stu-id="654cf-200">If UDT is used in GROUP BY, hello following error is thrown:</span></span>

```
Error   1   E_CSC_USER_INVALIDTYPEINCLAUSE: GROUP BY doesn't support type MyNameSpace.Myfunction_Returning_UDT
for column myfield

Description:

GROUP BY doesn't support UDT or Complex types.

Resolution:

Add a SELECT statement where you can project a scalar column that you want toouse with GROUP BY.
C:\Users\sergeypu\Documents\Visual Studio 2013\Projects\USQL-Programmability\USQL-Programmability\Types.usql
62  5   USQL-Programmability
```

<span data-ttu-id="654cf-201">toodefine um UDT, temos para:</span><span class="sxs-lookup"><span data-stu-id="654cf-201">toodefine a UDT, we have to:</span></span>

* <span data-ttu-id="654cf-202">Adicione Olá seguintes espaços de nomes:</span><span class="sxs-lookup"><span data-stu-id="654cf-202">Add hello following namespaces:</span></span>

```
using Microsoft.Analytics.Interfaces
using System.IO;
```

* <span data-ttu-id="654cf-203">Adicionar `Microsoft.Analytics.Interfaces`, que é necessário para interfaces UDT Olá.</span><span class="sxs-lookup"><span data-stu-id="654cf-203">Add `Microsoft.Analytics.Interfaces`, which is required for hello UDT interfaces.</span></span> <span data-ttu-id="654cf-204">Além disso, `System.IO` poderá estar a interface de IFormatter de Olá toodefine necessários.</span><span class="sxs-lookup"><span data-stu-id="654cf-204">In addition, `System.IO` might be needed toodefine hello IFormatter interface.</span></span>

* <span data-ttu-id="654cf-205">Defina um tipo definido pelo utilizado com o atributo SqlUserDefinedType.</span><span class="sxs-lookup"><span data-stu-id="654cf-205">Define a used-defined type with SqlUserDefinedType attribute.</span></span>

<span data-ttu-id="654cf-206">**SqlUserDefinedType** é utilizado toomark uma definição de tipo numa assemblagem como um tipo definido pelo utilizador (UDT) em U-SQL.</span><span class="sxs-lookup"><span data-stu-id="654cf-206">**SqlUserDefinedType** is used toomark a type definition in an assembly as a user-defined type (UDT) in U-SQL.</span></span> <span data-ttu-id="654cf-207">Propriedades de Olá no atributo Olá refletem as características físicas da Olá de Olá UDT.</span><span class="sxs-lookup"><span data-stu-id="654cf-207">hello properties on hello attribute reflect hello physical characteristics of hello UDT.</span></span> <span data-ttu-id="654cf-208">Esta classe não pode ser herdada.</span><span class="sxs-lookup"><span data-stu-id="654cf-208">This class cannot be inherited.</span></span>

<span data-ttu-id="654cf-209">SqlUserDefinedType é um atributo necessário para a definição de UDT.</span><span class="sxs-lookup"><span data-stu-id="654cf-209">SqlUserDefinedType is a required attribute for UDT definition.</span></span>

<span data-ttu-id="654cf-210">Construtor de classe de Olá Olá:</span><span class="sxs-lookup"><span data-stu-id="654cf-210">hello constructor of hello class:</span></span>  

* <span data-ttu-id="654cf-211">SqlUserDefinedTypeAttribute (formatador de tipo)</span><span class="sxs-lookup"><span data-stu-id="654cf-211">SqlUserDefinedTypeAttribute (type formatter)</span></span>

* <span data-ttu-id="654cf-212">Escreva o formatador: necessário parâmetro toodefine um formatador UDT – especificamente, o tipo de Olá de Olá `IFormatter` interface tem de ser transmitida aqui.</span><span class="sxs-lookup"><span data-stu-id="654cf-212">Type formatter: Required parameter toodefine an UDT formatter--specifically, hello type of hello `IFormatter` interface must be passed here.</span></span>

```
[SqlUserDefinedType(typeof(MyTypeFormatter))]
public class MyType
{ … }
```

* <span data-ttu-id="654cf-213">UDT típico também requer a definição de interface de IFormatter Olá, conforme mostrado no seguinte exemplo de Olá:</span><span class="sxs-lookup"><span data-stu-id="654cf-213">Typical UDT also requires definition of hello IFormatter interface, as shown in hello following example:</span></span>

```
public class MyTypeFormatter : IFormatter<MyType>
{
    public void Serialize(MyType instance, IColumnWriter writer, ISerializationContext context)
    { … }

    public MyType Deserialize(IColumnReader reader, ISerializationContext context)
    { … }
}
```

<span data-ttu-id="654cf-214">Olá `IFormatter` interface serializa e anular serializa um gráfico de objeto com o tipo de raiz de Olá de \<typeparamref name = "T" >.</span><span class="sxs-lookup"><span data-stu-id="654cf-214">hello `IFormatter` interface serializes and de-serializes an object graph with hello root type of \<typeparamref name="T">.</span></span>

<span data-ttu-id="654cf-215">\<typeparam name = "T" > olá o tipo de raiz para tooserialize de gráfico de objeto Olá e anular a serialização.</span><span class="sxs-lookup"><span data-stu-id="654cf-215">\<typeparam name="T">hello root type for hello object graph tooserialize and de-serialize.</span></span>

* <span data-ttu-id="654cf-216">**Anular a serialização**: anular serializa dados Olá no fluxo de Olá fornecida e reconstitutes gráfico Olá de objetos.</span><span class="sxs-lookup"><span data-stu-id="654cf-216">**Deserialize**: De-serializes hello data on hello provided stream and reconstitutes hello graph of objects.</span></span>

* <span data-ttu-id="654cf-217">**Serializar**: Serializa um objeto ou o gráfico de objetos, com Olá fornecido fluxo toohello fornecido de raiz.</span><span class="sxs-lookup"><span data-stu-id="654cf-217">**Serialize**: Serializes an object, or graph of objects, with hello given root toohello provided stream.</span></span>

<span data-ttu-id="654cf-218">`MyType`instância: instância do tipo de Olá.</span><span class="sxs-lookup"><span data-stu-id="654cf-218">`MyType` instance: Instance of hello type.</span></span>  
<span data-ttu-id="654cf-219">`IColumnWriter`escritor / `IColumnReader` leitor: Olá subjacente fluxo da coluna.</span><span class="sxs-lookup"><span data-stu-id="654cf-219">`IColumnWriter` writer / `IColumnReader` reader: hello underlying column stream.</span></span>  
<span data-ttu-id="654cf-220">`ISerializationContext`contexto: enumeração que define um conjunto de sinalizadores que especifica o contexto de origem ou destino de Olá para fluxo Olá durante a serialização.</span><span class="sxs-lookup"><span data-stu-id="654cf-220">`ISerializationContext` context: Enum that defines a set of flags that specifies hello source or destination context for hello stream during serialization.</span></span>

* <span data-ttu-id="654cf-221">**Intermédio**: Especifica nesse contexto Olá de origem ou de destino não é um arquivo persistente.</span><span class="sxs-lookup"><span data-stu-id="654cf-221">**Intermediate**: Specifies that hello source or destination context is not a persisted store.</span></span>

* <span data-ttu-id="654cf-222">**Persistência**: Especifica nesse contexto Olá de origem ou de destino é um arquivo persistente.</span><span class="sxs-lookup"><span data-stu-id="654cf-222">**Persistence**: Specifies that hello source or destination context is a persisted store.</span></span>

<span data-ttu-id="654cf-223">Como um regular c# tipo, uma definição de U-SQL UDT pode incluir substituições para operadores como + /Safari/Chrome = = /! =.</span><span class="sxs-lookup"><span data-stu-id="654cf-223">As a regular C# type, a U-SQL UDT definition can include overrides for operators such as +/==/!=.</span></span> <span data-ttu-id="654cf-224">Também pode incluir métodos estáticos.</span><span class="sxs-lookup"><span data-stu-id="654cf-224">It can also include static methods.</span></span> <span data-ttu-id="654cf-225">Por exemplo, se, vamos toouse este UDT como um parâmetro tooa função de agregação MIN U-SQL, temos toodefine < substituição de operador.</span><span class="sxs-lookup"><span data-stu-id="654cf-225">For example, if we are going toouse this UDT as a parameter tooa U-SQL MIN aggregate function, we have toodefine < operator override.</span></span>

<span data-ttu-id="654cf-226">Anteriormente neste guia, iremos demonstrado um exemplo de identificação de período fiscal de data específica do Olá no formato de Olá Qn:Pn (Q1:P10).</span><span class="sxs-lookup"><span data-stu-id="654cf-226">Earlier in this guide, we demonstrated an example for fiscal period identification from hello specific date in hello format Qn:Pn (Q1:P10).</span></span> <span data-ttu-id="654cf-227">Olá seguinte exemplo mostra como toodefine personalizadas escreva para valores fiscais.</span><span class="sxs-lookup"><span data-stu-id="654cf-227">hello following example shows how toodefine a custom type for fiscal period values.</span></span>

<span data-ttu-id="654cf-228">Segue-se um exemplo de uma secção code-behind com interface UDT e IFormatter personalizada:</span><span class="sxs-lookup"><span data-stu-id="654cf-228">Following is an example of a code-behind section with custom UDT and IFormatter interface:</span></span>

```
[SqlUserDefinedType(typeof(FiscalPeriodFormatter))]
public struct FiscalPeriod
{
    public int Quarter { get; private set; }

    public int Month { get; private set; }

    public FiscalPeriod(int quarter, int month):this()
    {
    this.Quarter = quarter;
    this.Month = month;
    }

    public override bool Equals(object obj)
    {
    if (ReferenceEquals(null, obj))
    {
        return false;
    }

    return obj is FiscalPeriod && Equals((FiscalPeriod)obj);
    }

    public bool Equals(FiscalPeriod other)
    {
return this.Quarter.Equals(other.Quarter) && this.Month.Equals(other.Month);
    }

    public bool GreaterThan(FiscalPeriod other)
    {
return this.Quarter.CompareTo(other.Quarter) > 0 || this.Month.CompareTo(other.Month) > 0;
    }

    public bool LessThan(FiscalPeriod other)
    {
return this.Quarter.CompareTo(other.Quarter) < 0 || this.Month.CompareTo(other.Month) < 0;
    }

    public override int GetHashCode()
    {
    unchecked
    {
        return (this.Quarter.GetHashCode() * 397) ^ this.Month.GetHashCode();
    }
    }

    public static FiscalPeriod operator +(FiscalPeriod c1, FiscalPeriod c2)
    {
return new FiscalPeriod((c1.Quarter + c2.Quarter) > 4 ? (c1.Quarter + c2.Quarter)-4 : (c1.Quarter + c2.Quarter), (c1.Month + c2.Month) > 12 ? (c1.Month + c2.Month) - 12 : (c1.Month + c2.Month));
    }

    public static bool operator ==(FiscalPeriod c1, FiscalPeriod c2)
    {
    return c1.Equals(c2);
    }

    public static bool operator !=(FiscalPeriod c1, FiscalPeriod c2)
    {
    return !c1.Equals(c2);
    }
    public static bool operator >(FiscalPeriod c1, FiscalPeriod c2)
    {
    return c1.GreaterThan(c2);
    }
    public static bool operator <(FiscalPeriod c1, FiscalPeriod c2)
    {
    return c1.LessThan(c2);
    }
    public override string ToString()
    {
    return (String.Format("Q{0}:P{1}", this.Quarter, this.Month));
    }

}

public class FiscalPeriodFormatter : IFormatter<FiscalPeriod>
{
    public void Serialize(FiscalPeriod instance, IColumnWriter writer, ISerializationContext context)
    {
    using (var binaryWriter = new BinaryWriter(writer.BaseStream))
    {
        binaryWriter.Write(instance.Quarter);
        binaryWriter.Write(instance.Month);
        binaryWriter.Flush();
    }
    }

    public FiscalPeriod Deserialize(IColumnReader reader, ISerializationContext context)
    {
    using (var binaryReader = new BinaryReader(reader.BaseStream))
    {
var result = new FiscalPeriod(binaryReader.ReadInt16(), binaryReader.ReadInt16());
        return result;
    }
    }
}
```

<span data-ttu-id="654cf-229">Olá tipo definido inclui dois números: trimestre e mês.</span><span class="sxs-lookup"><span data-stu-id="654cf-229">hello defined type includes two numbers: quarter and month.</span></span> <span data-ttu-id="654cf-230">Os operadores = = /! = / > / < e método estático ToString () são definidas aqui.</span><span class="sxs-lookup"><span data-stu-id="654cf-230">Operators ==/!=/>/< and static method ToString() are defined here.</span></span>

<span data-ttu-id="654cf-231">Conforme mencionado anteriormente, UDT pode ser utilizado em expressões SELECT, mas não é possível utilizar OUTPUTTER/EXTRATOR sem serialização personalizada.</span><span class="sxs-lookup"><span data-stu-id="654cf-231">As mentioned earlier, UDT can be used in SELECT expressions, but cannot be used in OUTPUTTER/EXTRACTOR without custom serialization.</span></span> <span data-ttu-id="654cf-232">-Tem toobe serializado como uma cadeia com ToString () ou utilizado com um OUTPUTTER/EXTRATOR personalizado.</span><span class="sxs-lookup"><span data-stu-id="654cf-232">It either has toobe serialized as a string with ToString() or used with a custom OUTPUTTER/EXTRACTOR.</span></span>

<span data-ttu-id="654cf-233">Agora vamos discutir sobre a utilização de UDT.</span><span class="sxs-lookup"><span data-stu-id="654cf-233">Now let’s discuss usage of UDT.</span></span> <span data-ttu-id="654cf-234">Numa secção por detrás do código, Alterámos o nosso seguinte do GetFiscalPeriod função toohello:</span><span class="sxs-lookup"><span data-stu-id="654cf-234">In a code-behind section, we changed our GetFiscalPeriod function toohello following:</span></span>

```
public static FiscalPeriod GetFiscalPeriodWithCustomType(DateTime dt)
{
    int FiscalMonth = 0;
    if (dt.Month < 7)
    {
    FiscalMonth = dt.Month + 6;
    }
    else
    {
    FiscalMonth = dt.Month - 6;
    }

    int FiscalQuarter = 0;
    if (FiscalMonth >= 1 && FiscalMonth <= 3)
    {
    FiscalQuarter = 1;
    }
    if (FiscalMonth >= 4 && FiscalMonth <= 6)
    {
    FiscalQuarter = 2;
    }
    if (FiscalMonth >= 7 && FiscalMonth <= 9)
    {
    FiscalQuarter = 3;
    }
    if (FiscalMonth >= 10 && FiscalMonth <= 12)
    {
    FiscalQuarter = 4;
    }

    return new FiscalPeriod(FiscalQuarter, FiscalMonth);
}
```

<span data-ttu-id="654cf-235">Como pode ver, devolve valor Olá do nosso tipo FiscalPeriod.</span><span class="sxs-lookup"><span data-stu-id="654cf-235">As you can see, it returns hello value of our FiscalPeriod type.</span></span>

<span data-ttu-id="654cf-236">Aqui fornecemos um exemplo de como toouse-la ainda mais no script U-SQL de base.</span><span class="sxs-lookup"><span data-stu-id="654cf-236">Here we provide an example of how toouse it further in U-SQL base script.</span></span> <span data-ttu-id="654cf-237">Este exemplo demonstra formas diferentes de invocação UDT do script U-SQL.</span><span class="sxs-lookup"><span data-stu-id="654cf-237">This example demonstrates different forms of UDT invocation from U-SQL script.</span></span>

```
DECLARE @input_file string = @"c:\work\cosmos\usql-programmability\input_file.tsv";
DECLARE @output_file string = @"c:\work\cosmos\usql-programmability\output_file.tsv";

@rs0 =
    EXTRACT
        guid string,
        dt DateTime,
        user String,
        des String
    FROM @input_file USING Extractors.Tsv();

@rs1 =
    SELECT 
        guid AS start_id,
        dt,
        DateTime.Now.ToString("M/d/yyyy") AS Nowdate,
        USQL_Programmability.CustomFunctions.GetFiscalPeriodWithCustomType(dt).Quarter AS fiscalquarter,
        USQL_Programmability.CustomFunctions.GetFiscalPeriodWithCustomType(dt).Month AS fiscalmonth,
        USQL_Programmability.CustomFunctions.GetFiscalPeriodWithCustomType(dt) + new USQL_Programmability.CustomFunctions.FiscalPeriod(1,7) AS fiscalperiod_adjusted,
        user,
        des
    FROM @rs0;

@rs2 =
    SELECT 
           start_id,
           dt,
           DateTime.Now.ToString("M/d/yyyy") AS Nowdate,
           fiscalquarter,
           fiscalmonth,
           USQL_Programmability.CustomFunctions.GetFiscalPeriodWithCustomType(dt).ToString() AS fiscalperiod,

       // This user-defined type was created in hello prior SELECT.  Passing hello UDT toothis subsequent SELECT would have failed if hello UDT was not annotated with an IFormatter.
           fiscalperiod_adjusted.ToString() AS fiscalperiod_adjusted,
           user,
           des
    FROM @rs1;

OUTPUT @rs2 
    too@output_file 
    USING Outputters.Text();
```

<span data-ttu-id="654cf-238">Eis um exemplo de uma secção completo por detrás do código:</span><span class="sxs-lookup"><span data-stu-id="654cf-238">Here's an example of a full code-behind section:</span></span>

```
using Microsoft.Analytics.Interfaces;
using Microsoft.Analytics.Types.Sql;
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.IO;

namespace USQL_Programmability
{
    public class CustomFunctions
    {
        static public DateTime? ToDateTime(string dt)
        {
            DateTime dtValue;

            if (!DateTime.TryParse(dt, out dtValue))
                return Convert.ToDateTime(dt);
            else
                return null;
        }

        public static FiscalPeriod GetFiscalPeriodWithCustomType(DateTime dt)
        {
            int FiscalMonth = 0;
            if (dt.Month < 7)
            {
                FiscalMonth = dt.Month + 6;
            }
            else
            {
                FiscalMonth = dt.Month - 6;
            }

            int FiscalQuarter = 0;
            if (FiscalMonth >= 1 && FiscalMonth <= 3)
            {
                FiscalQuarter = 1;
            }
            if (FiscalMonth >= 4 && FiscalMonth <= 6)
            {
                FiscalQuarter = 2;
            }
            if (FiscalMonth >= 7 && FiscalMonth <= 9)
            {
                FiscalQuarter = 3;
            }
            if (FiscalMonth >= 10 && FiscalMonth <= 12)
            {
                FiscalQuarter = 4;
            }

            return new FiscalPeriod(FiscalQuarter, FiscalMonth);
        }



        [SqlUserDefinedType(typeof(FiscalPeriodFormatter))]
        public struct FiscalPeriod
        {
            public int Quarter { get; private set; }

            public int Month { get; private set; }

            public FiscalPeriod(int quarter, int month):this()
            {
                this.Quarter = quarter;
                this.Month = month;
            }

            public override bool Equals(object obj)
            {
                if (ReferenceEquals(null, obj))
                {
                    return false;
                }

                return obj is FiscalPeriod && Equals((FiscalPeriod)obj);
            }

            public bool Equals(FiscalPeriod other)
            {
return this.Quarter.Equals(other.Quarter) &&    this.Month.Equals(other.Month);
            }

            public bool GreaterThan(FiscalPeriod other)
            {
return this.Quarter.CompareTo(other.Quarter) > 0 || this.Month.CompareTo(other.Month) > 0;
            }

            public bool LessThan(FiscalPeriod other)
            {
return this.Quarter.CompareTo(other.Quarter) < 0 || this.Month.CompareTo(other.Month) < 0;
            }

            public override int GetHashCode()
            {
                unchecked
                {
                    return (this.Quarter.GetHashCode() * 397) ^ this.Month.GetHashCode();
                }
            }

            public static FiscalPeriod operator +(FiscalPeriod c1, FiscalPeriod c2)
            {
return new FiscalPeriod((c1.Quarter + c2.Quarter) > 4 ? (c1.Quarter + c2.Quarter)-4 : (c1.Quarter + c2.Quarter), (c1.Month + c2.Month) > 12 ? (c1.Month + c2.Month) - 12 : (c1.Month + c2.Month));
            }

            public static bool operator ==(FiscalPeriod c1, FiscalPeriod c2)
            {
                return c1.Equals(c2);
            }

            public static bool operator !=(FiscalPeriod c1, FiscalPeriod c2)
            {
                return !c1.Equals(c2);
            }
            public static bool operator >(FiscalPeriod c1, FiscalPeriod c2)
            {
                return c1.GreaterThan(c2);
            }
            public static bool operator <(FiscalPeriod c1, FiscalPeriod c2)
            {
                return c1.LessThan(c2);
            }
            public override string ToString()
            {
                return (String.Format("Q{0}:P{1}", this.Quarter, this.Month));
            }

        }

        public class FiscalPeriodFormatter : IFormatter<FiscalPeriod>
        {
public void Serialize(FiscalPeriod instance, IColumnWriter writer, ISerializationContext context)
            {
                using (var binaryWriter = new BinaryWriter(writer.BaseStream))
                {
                    binaryWriter.Write(instance.Quarter);
                    binaryWriter.Write(instance.Month);
                    binaryWriter.Flush();
                }
            }

public FiscalPeriod Deserialize(IColumnReader reader, ISerializationContext context)
            {
                using (var binaryReader = new BinaryReader(reader.BaseStream))
                {
var result = new FiscalPeriod(binaryReader.ReadInt16(), binaryReader.ReadInt16());
                    return result;
                }
            }
        }
    }
}
```

## <a name="use-user-defined-aggregates-udagg"></a><span data-ttu-id="654cf-239">Utilize agregações definidas pelo utilizador: UDAGG</span><span class="sxs-lookup"><span data-stu-id="654cf-239">Use user-defined aggregates: UDAGG</span></span>
<span data-ttu-id="654cf-240">Os agregados definidos pelo utilizador são quaisquer funções relacionadas com a agregação que são fornecidos não out-of-a-box com U-SQL.</span><span class="sxs-lookup"><span data-stu-id="654cf-240">User-defined aggregates are any aggregation-related functions that are not shipped out-of-the-box with U-SQL.</span></span> <span data-ttu-id="654cf-241">exemplo de Olá pode ser um agregado tooperform cálculos de bibliotecas personalizado, concatenations de cadeia, manipulações de cadeias e assim sucessivamente.</span><span class="sxs-lookup"><span data-stu-id="654cf-241">hello example can be an aggregate tooperform custom math calculations, string concatenations, manipulations with strings, and so on.</span></span>

<span data-ttu-id="654cf-242">definição de classe base agregado definido pelo utilizador Olá é o seguinte:</span><span class="sxs-lookup"><span data-stu-id="654cf-242">hello user-defined aggregate base class definition is as follows:</span></span>

```c#
    [SqlUserDefinedAggregate]
    public abstract class IAggregate<T1, T2, TResult> : IAggregate
    {
        protected IAggregate();

        public abstract void Accumulate(T1 t1, T2 t2);
        public abstract void Init();
        public abstract TResult Terminate();
    }
```

<span data-ttu-id="654cf-243">**SqlUserDefinedAggregate** indica que o tipo de Olá deve ser registado como um agregado definido pelo utilizador.</span><span class="sxs-lookup"><span data-stu-id="654cf-243">**SqlUserDefinedAggregate** indicates that hello type should be registered as a user-defined aggregate.</span></span> <span data-ttu-id="654cf-244">Esta classe não pode ser herdada.</span><span class="sxs-lookup"><span data-stu-id="654cf-244">This class cannot be inherited.</span></span>

<span data-ttu-id="654cf-245">Atributo de SqlUserDefinedType **opcional** para definição UDAGG.</span><span class="sxs-lookup"><span data-stu-id="654cf-245">SqlUserDefinedType attribute is **optional** for UDAGG definition.</span></span>


<span data-ttu-id="654cf-246">Olá classe base permite-lhe toopass três parâmetros de abstrato: dois como parâmetros de entrada e um como resultado de Olá.</span><span class="sxs-lookup"><span data-stu-id="654cf-246">hello base class allows you toopass three abstract parameters: two as input parameters and one as hello result.</span></span> <span data-ttu-id="654cf-247">tipos de dados de Olá são variáveis e devem ser definidos durante a herança de classe.</span><span class="sxs-lookup"><span data-stu-id="654cf-247">hello data types are variable and should be defined during class inheritance.</span></span>

```
public class GuidAggregate : IAggregate<string, string, string>
{
    string guid_agg;

    public override void Init()
    { … }

    public override void Accumulate(string guid, string user)
    { … }

    public override string Terminate()
    { … }
}
```

* <span data-ttu-id="654cf-248">**Init** invoca uma vez para cada grupo durante o cálculo.</span><span class="sxs-lookup"><span data-stu-id="654cf-248">**Init** invokes once for each group during computation.</span></span> <span data-ttu-id="654cf-249">Fornece uma rotina de inicialização para cada grupo de agregação.</span><span class="sxs-lookup"><span data-stu-id="654cf-249">It provides an initialization routine for each aggregation group.</span></span>  
* <span data-ttu-id="654cf-250">**Acumular** é executado uma vez para cada valor.</span><span class="sxs-lookup"><span data-stu-id="654cf-250">**Accumulate** is executed once for each value.</span></span> <span data-ttu-id="654cf-251">Fornece uma funcionalidade principal de Olá para o algoritmo de agregação de Olá.</span><span class="sxs-lookup"><span data-stu-id="654cf-251">It provides hello main functionality for hello aggregation algorithm.</span></span> <span data-ttu-id="654cf-252">Pode ser utilizado tooaggregate valores com vários tipos de dados que são definidos durante a herança de classe.</span><span class="sxs-lookup"><span data-stu-id="654cf-252">It can be used tooaggregate values with various data types that are defined during class inheritance.</span></span> <span data-ttu-id="654cf-253">Pode aceitar o dois parâmetros dos tipos de dados da variável.</span><span class="sxs-lookup"><span data-stu-id="654cf-253">It can accept two parameters of variable data types.</span></span>
* <span data-ttu-id="654cf-254">**Terminar** é executado uma vez por grupo de agregação no fim de Olá do processamento toooutput Olá resultado para cada grupo.</span><span class="sxs-lookup"><span data-stu-id="654cf-254">**Terminate** is executed once per aggregation group at hello end of processing toooutput hello result for each group.</span></span>

<span data-ttu-id="654cf-255">entrada correto toodeclare e tipos de dados de saída, utilize de forma a definição de classe de Olá:</span><span class="sxs-lookup"><span data-stu-id="654cf-255">toodeclare correct input and output data types, use hello class definition as follows:</span></span>

```
public abstract class IAggregate<T1, T2, TResult> : IAggregate
```

* <span data-ttu-id="654cf-256">T1: Primeiro parâmetro tooaccumulate</span><span class="sxs-lookup"><span data-stu-id="654cf-256">T1: First parameter tooaccumulate</span></span>
* <span data-ttu-id="654cf-257">T2: Primeiro parâmetro tooaccumulate</span><span class="sxs-lookup"><span data-stu-id="654cf-257">T2: First parameter tooaccumulate</span></span>
* <span data-ttu-id="654cf-258">TResult: Tipo de retorno da terminação</span><span class="sxs-lookup"><span data-stu-id="654cf-258">TResult: Return type of terminate</span></span>

<span data-ttu-id="654cf-259">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="654cf-259">For example:</span></span>

```
public class GuidAggregate : IAggregate<string, int, int>
```

<span data-ttu-id="654cf-260">ou</span><span class="sxs-lookup"><span data-stu-id="654cf-260">or</span></span>

```
public class GuidAggregate : IAggregate<string, string, string>
```

### <a name="use-udagg-in-u-sql"></a><span data-ttu-id="654cf-261">Utilizar UDAGG em U-SQL</span><span class="sxs-lookup"><span data-stu-id="654cf-261">Use UDAGG in U-SQL</span></span>
<span data-ttu-id="654cf-262">toouse UDAGG, primeiro defini-lo no code-behind ou de referência de programação para existente de Olá DLL, conforme debatido anteriormente.</span><span class="sxs-lookup"><span data-stu-id="654cf-262">toouse UDAGG, first define it in code-behind or reference it from hello existent programmability DLL as discussed earlier.</span></span>

<span data-ttu-id="654cf-263">Em seguida, utilize Olá sintaxe:</span><span class="sxs-lookup"><span data-stu-id="654cf-263">Then use hello following syntax:</span></span>

```
AGG<UDAGG_functionname>(param1,param2)
```

<span data-ttu-id="654cf-264">Eis um exemplo de UDAGG:</span><span class="sxs-lookup"><span data-stu-id="654cf-264">Here is an example of UDAGG:</span></span>

```
public class GuidAggregate : IAggregate<string, string, string>
{
    string guid_agg;

    public override void Init()
    {
        guid_agg = "";
    }

    public override void Accumulate(string guid, string user)
    {
        if (user.ToUpper()== "USER1")
        {
        guid_agg += "{" + guid + "}";
        }
    }

    public override string Terminate()
    {
        return guid_agg;
    }

}
```

<span data-ttu-id="654cf-265">E o script de U-SQL base:</span><span class="sxs-lookup"><span data-stu-id="654cf-265">And base U-SQL script:</span></span>

```
DECLARE @input_file string = @"\usql-programmability\input_file.tsv";
DECLARE @output_file string = @" \usql-programmability\output_file.tsv";

@rs0 =
    EXTRACT
            guid string,
        dt DateTime,
            user String,
            des String
    FROM @input_file 
    USING Extractors.Tsv();

@rs1 =
    SELECT
        user,
        AGG<USQL_Programmability.GuidAggregate>(guid,user) AS guid_list
    FROM @rs0
    GROUP BY user;

OUTPUT @rs1 too@output_file USING Outputters.Text();
```

<span data-ttu-id="654cf-266">Neste cenário de caso de utilização, iremos concatenar classe GUIDs para utilizadores específicos Olá.</span><span class="sxs-lookup"><span data-stu-id="654cf-266">In this use-case scenario, we concatenate class GUIDs for hello specific users.</span></span>

## <a name="use-user-defined-objects-udo"></a><span data-ttu-id="654cf-267">Utilizar os objetos definidos pelo utilizador: UDO</span><span class="sxs-lookup"><span data-stu-id="654cf-267">Use user-defined objects: UDO</span></span>
<span data-ttu-id="654cf-268">U-SQL permite objetos de programação para personalizado toodefine, que são chamados objetos definidos pelo utilizador ou UDO.</span><span class="sxs-lookup"><span data-stu-id="654cf-268">U-SQL enables you toodefine custom programmability objects, which are called user-defined objects or UDO.</span></span>

<span data-ttu-id="654cf-269">Olá segue-se uma lista de UDO em U-SQL:</span><span class="sxs-lookup"><span data-stu-id="654cf-269">hello following is a list of UDO in U-SQL:</span></span>

* <span data-ttu-id="654cf-270">Extractors definido pelo utilizador</span><span class="sxs-lookup"><span data-stu-id="654cf-270">User-defined extractors</span></span>
    * <span data-ttu-id="654cf-271">Extrair linha por linha</span><span class="sxs-lookup"><span data-stu-id="654cf-271">Extract row by row</span></span>
    * <span data-ttu-id="654cf-272">Utilizado tooimplement extração de dados de ficheiros estruturados personalizados</span><span class="sxs-lookup"><span data-stu-id="654cf-272">Used tooimplement data extraction from custom structured files</span></span>

* <span data-ttu-id="654cf-273">Outputters definido pelo utilizador</span><span class="sxs-lookup"><span data-stu-id="654cf-273">User-defined outputters</span></span>
    * <span data-ttu-id="654cf-274">Saída linha por linha</span><span class="sxs-lookup"><span data-stu-id="654cf-274">Output row by row</span></span>
    * <span data-ttu-id="654cf-275">Utilizar tipos de dados personalizados toooutput ou formatos de ficheiro personalizadas</span><span class="sxs-lookup"><span data-stu-id="654cf-275">Used toooutput custom data types or custom file formats</span></span>

* <span data-ttu-id="654cf-276">Processadores definidos pelo utilizador</span><span class="sxs-lookup"><span data-stu-id="654cf-276">User-defined processors</span></span>
    * <span data-ttu-id="654cf-277">Obter uma linha e produzir uma linha</span><span class="sxs-lookup"><span data-stu-id="654cf-277">Take one row and produce one row</span></span>
    * <span data-ttu-id="654cf-278">Utilizado tooreduce Olá número de colunas ou produzir novas colunas com valores que são derivadas de um conjunto de coluna existente</span><span class="sxs-lookup"><span data-stu-id="654cf-278">Used tooreduce hello number of columns or produce new columns with values that are derived from an existing column set</span></span>

* <span data-ttu-id="654cf-279">Appliers definido pelo utilizador</span><span class="sxs-lookup"><span data-stu-id="654cf-279">User-defined appliers</span></span>
    * <span data-ttu-id="654cf-280">Obter uma linha e produzir 0 linhas de toon</span><span class="sxs-lookup"><span data-stu-id="654cf-280">Take one row and produce 0 toon rows</span></span>
    * <span data-ttu-id="654cf-281">Utilizado com OUTER/entre aplicar</span><span class="sxs-lookup"><span data-stu-id="654cf-281">Used with OUTER/CROSS APPLY</span></span>

* <span data-ttu-id="654cf-282">Combiners definido pelo utilizador</span><span class="sxs-lookup"><span data-stu-id="654cf-282">User-defined combiners</span></span>
    * <span data-ttu-id="654cf-283">Combina os conjuntos de linhas – associações definidas pelo utilizador</span><span class="sxs-lookup"><span data-stu-id="654cf-283">Combines rowsets--user-defined JOINs</span></span>

* <span data-ttu-id="654cf-284">Reducers definido pelo utilizador</span><span class="sxs-lookup"><span data-stu-id="654cf-284">User-defined reducers</span></span>
    * <span data-ttu-id="654cf-285">Tome n linhas e produzir uma linha</span><span class="sxs-lookup"><span data-stu-id="654cf-285">Take n rows and produce one row</span></span>
    * <span data-ttu-id="654cf-286">Utilizado tooreduce Olá diversas linhas</span><span class="sxs-lookup"><span data-stu-id="654cf-286">Used tooreduce hello number of rows</span></span>

<span data-ttu-id="654cf-287">UDO é normalmente designado explicitamente no script de U-SQL como parte da Olá seguir instruções U-SQL:</span><span class="sxs-lookup"><span data-stu-id="654cf-287">UDO is typically called explicitly in U-SQL script as part of hello following U-SQL statements:</span></span>

* <span data-ttu-id="654cf-288">EXTRAIR</span><span class="sxs-lookup"><span data-stu-id="654cf-288">EXTRACT</span></span>
* <span data-ttu-id="654cf-289">SAÍDA</span><span class="sxs-lookup"><span data-stu-id="654cf-289">OUTPUT</span></span>
* <span data-ttu-id="654cf-290">PROCESSO</span><span class="sxs-lookup"><span data-stu-id="654cf-290">PROCESS</span></span>
* <span data-ttu-id="654cf-291">COMBINAR</span><span class="sxs-lookup"><span data-stu-id="654cf-291">COMBINE</span></span>
* <span data-ttu-id="654cf-292">REDUZIR</span><span class="sxs-lookup"><span data-stu-id="654cf-292">REDUCE</span></span>

> [!NOTE]  
> <span data-ttu-id="654cf-293">UDO é limitadas tooconsume 0.5Gb memória.</span><span class="sxs-lookup"><span data-stu-id="654cf-293">UDO’s are limited tooconsume 0.5Gb memory.</span></span>  <span data-ttu-id="654cf-294">Esta limitação de memória não é aplicável toolocal execuções.</span><span class="sxs-lookup"><span data-stu-id="654cf-294">This memory limitation does not apply toolocal executions.</span></span>

## <a name="use-user-defined-extractors"></a><span data-ttu-id="654cf-295">Utilizar extractors definido pelo utilizador</span><span class="sxs-lookup"><span data-stu-id="654cf-295">Use user-defined extractors</span></span>
<span data-ttu-id="654cf-296">U-SQL permite-lhe dados externos tooimport utilizando uma instrução de EXTRAÇÃO.</span><span class="sxs-lookup"><span data-stu-id="654cf-296">U-SQL allows you tooimport external data by using an EXTRACT statement.</span></span> <span data-ttu-id="654cf-297">Uma instrução de EXTRAÇÃO pode utilizar extractors UDO incorporadas:</span><span class="sxs-lookup"><span data-stu-id="654cf-297">An EXTRACT statement can use built-in UDO extractors:</span></span>  

* <span data-ttu-id="654cf-298">*Extractors.Text()*: fornece a extração dos ficheiros de texto delimitado de codificações diferentes.</span><span class="sxs-lookup"><span data-stu-id="654cf-298">*Extractors.Text()*: Provides extraction from delimited text files of different encodings.</span></span>

* <span data-ttu-id="654cf-299">*Extractors.Csv()*: fornece a extração de valores separados por vírgulas (CSV) os ficheiros do codificações diferentes.</span><span class="sxs-lookup"><span data-stu-id="654cf-299">*Extractors.Csv()*: Provides extraction from comma-separated value (CSV) files of different encodings.</span></span>

* <span data-ttu-id="654cf-300">*Extractors*: fornece a extração de valores separados por separador ficheiros (TSV) de codificações diferentes.</span><span class="sxs-lookup"><span data-stu-id="654cf-300">*Extractors.Tsv()*: Provides extraction from tab-separated value (TSV) files of different encodings.</span></span>

<span data-ttu-id="654cf-301">Pode ser útil toodevelop extrator de personalizado.</span><span class="sxs-lookup"><span data-stu-id="654cf-301">It can be useful toodevelop a custom extractor.</span></span> <span data-ttu-id="654cf-302">Isto pode ser útil durante a importação de dados se quisermos toodo qualquer um dos Olá seguintes tarefas:</span><span class="sxs-lookup"><span data-stu-id="654cf-302">This can be helpful during data import if we want toodo any of hello following tasks:</span></span>

* <span data-ttu-id="654cf-303">Modificar os dados de entrada ao dividir colunas e modificar valores individuais.</span><span class="sxs-lookup"><span data-stu-id="654cf-303">Modify input data by splitting columns and modifying individual values.</span></span> <span data-ttu-id="654cf-304">Olá funcionalidade do processador é melhor para a combinação de colunas.</span><span class="sxs-lookup"><span data-stu-id="654cf-304">hello PROCESSOR functionality is better for combining columns.</span></span>
* <span data-ttu-id="654cf-305">Analisar dados não estruturados, tais como páginas Web e os e-mails ou dados por não estruturados como XML/JSON.</span><span class="sxs-lookup"><span data-stu-id="654cf-305">Parse unstructured data such as Web pages and emails, or semi-unstructured data such as XML/JSON.</span></span>
* <span data-ttu-id="654cf-306">Analisar dados na codificação não suportada.</span><span class="sxs-lookup"><span data-stu-id="654cf-306">Parse data in unsupported encoding.</span></span>

<span data-ttu-id="654cf-307">toodefine um extrator definido pelo utilizador, ou UIR, precisamos toocreate um `IExtractor` interface.</span><span class="sxs-lookup"><span data-stu-id="654cf-307">toodefine a user-defined extractor, or UDE, we need toocreate an `IExtractor` interface.</span></span> <span data-ttu-id="654cf-308">Extrator de toohello de parâmetros, todos os entrada, tais como delimitadores de linha/coluna e codificação, precisam de toobe definido no construtor de Olá da classe de Olá.</span><span class="sxs-lookup"><span data-stu-id="654cf-308">All input parameters toohello extractor, such as column/row delimiters, and encoding, need toobe defined in hello constructor of hello class.</span></span> <span data-ttu-id="654cf-309">Olá `IExtractor` interface deve conter também uma definição para Olá `IEnumerable<IRow>` substituir da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="654cf-309">hello `IExtractor`  interface should also contain a definition for hello `IEnumerable<IRow>` override as follows:</span></span>

```
[SqlUserDefinedExtractor]
public class SampleExtractor : IExtractor
{
     public SampleExtractor(string row_delimiter, char col_delimiter)
     { … }

     public override IEnumerable<IRow> Extract(IUnstructuredReader input, IUpdatableRow output)
     { … }
}
```

<span data-ttu-id="654cf-310">Olá **SqlUserDefinedExtractor** atributo indica que o tipo de Olá deve ser registado como um extrator definido pelo utilizador.</span><span class="sxs-lookup"><span data-stu-id="654cf-310">hello **SqlUserDefinedExtractor** attribute indicates that hello type should be registered as a user-defined extractor.</span></span> <span data-ttu-id="654cf-311">Esta classe não pode ser herdada.</span><span class="sxs-lookup"><span data-stu-id="654cf-311">This class cannot be inherited.</span></span>

<span data-ttu-id="654cf-312">SqlUserDefinedExtractor é um atributo opcional para a definição de UIR.</span><span class="sxs-lookup"><span data-stu-id="654cf-312">SqlUserDefinedExtractor is an optional attribute for UDE definition.</span></span> <span data-ttu-id="654cf-313">Utilizá-la toodefine AtomicFileProcessing propriedade para o objeto de UIR Olá.</span><span class="sxs-lookup"><span data-stu-id="654cf-313">It used toodefine AtomicFileProcessing property for hello UDE object.</span></span>

* <span data-ttu-id="654cf-314">bool AtomicFileProcessing</span><span class="sxs-lookup"><span data-stu-id="654cf-314">bool     AtomicFileProcessing</span></span>   

* <span data-ttu-id="654cf-315">**Verdadeiro** = indica que este extrator requer atómicos os ficheiros de entrada (JSON, XML,...)</span><span class="sxs-lookup"><span data-stu-id="654cf-315">**true** = Indicates that this extractor requires atomic input files (JSON, XML, ...)</span></span>
* <span data-ttu-id="654cf-316">**FALSO** = indica que este extrator pode lidar com ficheiros divididos / distribuídos (CSV, SEQ,...)</span><span class="sxs-lookup"><span data-stu-id="654cf-316">**false** = Indicates that this extractor can deal with split / distributed files (CSV, SEQ, ...)</span></span>

<span data-ttu-id="654cf-317">Olá principal UIR programação para objetos são **entrada** e **saída**.</span><span class="sxs-lookup"><span data-stu-id="654cf-317">hello main UDE programmability objects are **input** and **output**.</span></span> <span data-ttu-id="654cf-318">objeto de entrada Olá é utilizado tooenumerate os dados de entrada como `IUnstructuredReader`.</span><span class="sxs-lookup"><span data-stu-id="654cf-318">hello input object is used tooenumerate input data as `IUnstructuredReader`.</span></span> <span data-ttu-id="654cf-319">o objeto de resultado de Olá é utilizado tooset dados de saída como resultado da atividade de extrator Olá.</span><span class="sxs-lookup"><span data-stu-id="654cf-319">hello output object is used tooset output data as a result of hello extractor activity.</span></span>

<span data-ttu-id="654cf-320">dados de entrada Olá são acedidos através do `System.IO.Stream` e `System.IO.StreamReader`.</span><span class="sxs-lookup"><span data-stu-id="654cf-320">hello input data is accessed through `System.IO.Stream` and `System.IO.StreamReader`.</span></span>

<span data-ttu-id="654cf-321">Para a enumeração de colunas de entrada, vamos primeiro dividir o fluxo de entrada Olá utilizando um delimitador de linha.</span><span class="sxs-lookup"><span data-stu-id="654cf-321">For input columns enumeration, we first split hello input stream by using a row delimiter.</span></span>

```
foreach (Stream current in input.Split(my_row_delimiter))
{
…
}
```

<span data-ttu-id="654cf-322">Em seguida, divida mais linhas de entrada em partes de coluna.</span><span class="sxs-lookup"><span data-stu-id="654cf-322">Then, further split input row into column parts.</span></span>

```
foreach (Stream current in input.Split(my_row_delimiter))
{
…
    string[] parts = line.Split(my_column_delimiter);
    foreach (string part in parts)
    { … }
}
```

<span data-ttu-id="654cf-323">dados de saída tooset, utilizamos Olá `output.Set` método.</span><span class="sxs-lookup"><span data-stu-id="654cf-323">tooset output data, we use hello `output.Set` method.</span></span>

<span data-ttu-id="654cf-324">É importante toounderstand Olá extrator personalizado apenas produz colunas e valores que estão definidos com a saída de Olá.</span><span class="sxs-lookup"><span data-stu-id="654cf-324">It's important toounderstand that hello custom extractor only outputs columns and values that are defined with hello output.</span></span> <span data-ttu-id="654cf-325">Definir a chamada de método.</span><span class="sxs-lookup"><span data-stu-id="654cf-325">Set method call.</span></span>

```
output.Set<string>(count, part);
```

<span data-ttu-id="654cf-326">saída de extrator real Olá é acionada ao chamar `yield return output.AsReadOnly();`.</span><span class="sxs-lookup"><span data-stu-id="654cf-326">hello actual extractor output is triggered by calling `yield return output.AsReadOnly();`.</span></span>

<span data-ttu-id="654cf-327">Segue-se Olá extrator exemplo:</span><span class="sxs-lookup"><span data-stu-id="654cf-327">Following is hello extractor example:</span></span>

```
[SqlUserDefinedExtractor(AtomicFileProcessing = true)]
public class FullDescriptionExtractor : IExtractor
{
     private Encoding _encoding;
     private byte[] _row_delim;
     private char _col_delim;

    public FullDescriptionExtractor(Encoding encoding, string row_delim = "\r\n", char col_delim = '\t')
    {
         this._encoding = ((encoding == null) ? Encoding.UTF8 : encoding);
         this._row_delim = this._encoding.GetBytes(row_delim);
         this._col_delim = col_delim;

    }

    public override IEnumerable<IRow> Extract(IUnstructuredReader input, IUpdatableRow output)
    {
         string line;
         //Read hello input line by line
         foreach (Stream current in input.Split(_encoding.GetBytes("\r\n")))
         {
        using (System.IO.StreamReader streamReader = new StreamReader(current, this._encoding))
         {
             line = streamReader.ReadToEnd().Trim();
             //Split hello input by hello column delimiter
             string[] parts = line.Split(this._col_delim);
             int count = 0; // start with first column
             foreach (string part in parts)
             {
    if (count == 0)
             {  // for column “guid”, re-generated guid
                 Guid new_guid = Guid.NewGuid();
                 output.Set<Guid>(count, new_guid);
             }
             else if (count == 2)
             {
                 // for column “user”, convert tooUPPER case
                 output.Set<string>(count, part.ToUpper());

             }
             else
             {
                 // keep hello rest of hello columns as-is
                 output.Set<string>(count, part);
             }
             count += 1;
             }

         }
         yield return output.AsReadOnly();
         }
         yield break;
     }
}
```

<span data-ttu-id="654cf-328">Neste cenário de caso de utilização, extrator Olá gera de novo Olá GUID para a coluna "guid" e converte valores de Olá do cenário de tooupper de coluna "utilizador".</span><span class="sxs-lookup"><span data-stu-id="654cf-328">In this use-case scenario, hello extractor regenerates hello GUID for “guid” column and converts hello values of “user” column tooupper case.</span></span> <span data-ttu-id="654cf-329">Extractors personalizados podem produzir resultados mais complicados pela análise de dados de entrada e manipulá-lo.</span><span class="sxs-lookup"><span data-stu-id="654cf-329">Custom extractors can produce more complicated results by parsing input data and manipulating it.</span></span>

<span data-ttu-id="654cf-330">Segue-se base script U-SQL que utiliza um extrator personalizado:</span><span class="sxs-lookup"><span data-stu-id="654cf-330">Following is base U-SQL script that uses a custom extractor:</span></span>

```
DECLARE @input_file string = @"\usql-programmability\input_file.tsv";
DECLARE @output_file string = @"\usql-programmability\output_file.tsv";

@rs0 =
    EXTRACT
            guid Guid,
        dt String,
            user String,
            des String
    FROM @input_file
        USING new USQL_Programmability.FullDescriptionExtractor(Encoding.UTF8);

OUTPUT @rs0 too@output_file USING Outputters.Text();
```

## <a name="use-user-defined-outputters"></a><span data-ttu-id="654cf-331">Utilizar outputters definido pelo utilizador</span><span class="sxs-lookup"><span data-stu-id="654cf-331">Use user-defined outputters</span></span>
<span data-ttu-id="654cf-332">Definido pelo utilizador outputter é outra UDO U-SQL que lhe permite uma funcionalidade U-SQL tooextend incorporada.</span><span class="sxs-lookup"><span data-stu-id="654cf-332">User-defined outputter is another U-SQL UDO that allows you tooextend built-in U-SQL functionality.</span></span> <span data-ttu-id="654cf-333">Extrator de toohello semelhante, existem várias outputters incorporadas.</span><span class="sxs-lookup"><span data-stu-id="654cf-333">Similar toohello extractor, there are several built-in outputters.</span></span>

* <span data-ttu-id="654cf-334">*Outputters.Text()*: escreve dados toodelimited ficheiros de texto de codificações diferentes.</span><span class="sxs-lookup"><span data-stu-id="654cf-334">*Outputters.Text()*: Writes data toodelimited text files of different encodings.</span></span>
* <span data-ttu-id="654cf-335">*Outputters*: escreve o valor de valores separados por toocomma dados ficheiros (CSV) de codificações de diferentes.</span><span class="sxs-lookup"><span data-stu-id="654cf-335">*Outputters.Csv()*: Writes data toocomma-separated value (CSV) files of different encodings.</span></span>
* <span data-ttu-id="654cf-336">*Outputters.Tsv()*: escreve o valor de valores separados por tootab dados ficheiros de (TSV) de codificações diferentes.</span><span class="sxs-lookup"><span data-stu-id="654cf-336">*Outputters.Tsv()*: Writes data tootab-separated value (TSV) files of different encodings.</span></span>

<span data-ttu-id="654cf-337">Outputter personalizada permite-lhe toowrite dados num formato personalizado definido.</span><span class="sxs-lookup"><span data-stu-id="654cf-337">Custom outputter allows you toowrite data in a custom defined format.</span></span> <span data-ttu-id="654cf-338">Isto pode ser útil para Olá seguintes tarefas:</span><span class="sxs-lookup"><span data-stu-id="654cf-338">This can be useful for hello following tasks:</span></span>

* <span data-ttu-id="654cf-339">Escrever ficheiros de dados estruturados de toosemi ou não estruturados.</span><span class="sxs-lookup"><span data-stu-id="654cf-339">Writing data toosemi-structured or unstructured files.</span></span>
* <span data-ttu-id="654cf-340">Escrita de dados não suportado codificações.</span><span class="sxs-lookup"><span data-stu-id="654cf-340">Writing data not supported encodings.</span></span>
* <span data-ttu-id="654cf-341">A modificação de dados de saída ou adicionar atributos personalizados.</span><span class="sxs-lookup"><span data-stu-id="654cf-341">Modifying output data or adding custom attributes.</span></span>

<span data-ttu-id="654cf-342">toodefine definido pelo utilizador outputter, precisamos toocreate Olá `IOutputter` interface.</span><span class="sxs-lookup"><span data-stu-id="654cf-342">toodefine user-defined outputter, we need toocreate hello `IOutputter` interface.</span></span>

<span data-ttu-id="654cf-343">Segue-se Olá base `IOutputter` implementação de classe:</span><span class="sxs-lookup"><span data-stu-id="654cf-343">Following is hello base `IOutputter` class implementation:</span></span>

```
public abstract class IOutputter : IUserDefinedOperator
{
    protected IOutputter();

    public virtual void Close();
    public abstract void Output(IRow input, IUnstructuredWriter output);
}
```

<span data-ttu-id="654cf-344">Todos os entrada parâmetros toohello outputter, tais como delimitadores de linha/coluna, codificação e assim sucessivamente, precisam de toobe definido no construtor de Olá da classe de Olá.</span><span class="sxs-lookup"><span data-stu-id="654cf-344">All input parameters toohello outputter, such as column/row delimiters, encoding, and so on, need toobe defined in hello constructor of hello class.</span></span> <span data-ttu-id="654cf-345">Olá `IOutputter` interface deve conter também uma definição para `void Output` substituir.</span><span class="sxs-lookup"><span data-stu-id="654cf-345">hello `IOutputter` interface should also contain a definition for `void Output` override.</span></span> <span data-ttu-id="654cf-346">atributo de Olá `[SqlUserDefinedOutputter(AtomicFileProcessing = true)` , opcionalmente, pode ser definido para o processamento do ficheiro atomic.</span><span class="sxs-lookup"><span data-stu-id="654cf-346">hello attribute `[SqlUserDefinedOutputter(AtomicFileProcessing = true)` can optionally be set for atomic file processing.</span></span> <span data-ttu-id="654cf-347">Para obter mais informações, consulte os detalhes de Olá.</span><span class="sxs-lookup"><span data-stu-id="654cf-347">For more information, see hello following details.</span></span>

```
[SqlUserDefinedOutputter(AtomicFileProcessing = true)]
public class MyOutputter : IOutputter
{

    public MyOutputter(myparam1, myparam2)
    {
      …
    }

    public override void Close()
    {
      …
    }

    public override void Output(IRow row, IUnstructuredWriter output)
    {
      …
    }
}
```

* <span data-ttu-id="654cf-348">`Output`é chamado para cada linha de entrada.</span><span class="sxs-lookup"><span data-stu-id="654cf-348">`Output` is called for each input row.</span></span> <span data-ttu-id="654cf-349">Devolve Olá `IUnstructuredWriter output` conjunto de linhas.</span><span class="sxs-lookup"><span data-stu-id="654cf-349">It returns hello `IUnstructuredWriter output` rowset.</span></span>
* <span data-ttu-id="654cf-350">é utilizado Olá classe construtor outputter toopass parâmetros toohello definido pelo utilizador.</span><span class="sxs-lookup"><span data-stu-id="654cf-350">hello Constructor class is used toopass parameters toohello user-defined outputter.</span></span>
* <span data-ttu-id="654cf-351">`Close`é utilizado toooptionally substituição de estado dispendiosas toorelease ou para determinar quando a última linha de Olá foi escrita.</span><span class="sxs-lookup"><span data-stu-id="654cf-351">`Close` is used toooptionally override toorelease expensive state or determine when hello last row was written.</span></span>

<span data-ttu-id="654cf-352">**SqlUserDefinedOutputter** atributo indica que o tipo de Olá deve ser registado como um outputter definido pelo utilizador.</span><span class="sxs-lookup"><span data-stu-id="654cf-352">**SqlUserDefinedOutputter** attribute indicates that hello type should be registered as a user-defined outputter.</span></span> <span data-ttu-id="654cf-353">Esta classe não pode ser herdada.</span><span class="sxs-lookup"><span data-stu-id="654cf-353">This class cannot be inherited.</span></span>

<span data-ttu-id="654cf-354">SqlUserDefinedOutputter é um atributo opcional para uma definição de outputter definido pelo utilizador.</span><span class="sxs-lookup"><span data-stu-id="654cf-354">SqlUserDefinedOutputter is an optional attribute for a user-defined outputter definition.</span></span> <span data-ttu-id="654cf-355">Utilizou o propriedade do toodefine Olá AtomicFileProcessing.</span><span class="sxs-lookup"><span data-stu-id="654cf-355">It's used toodefine hello AtomicFileProcessing property.</span></span>

* <span data-ttu-id="654cf-356">bool AtomicFileProcessing</span><span class="sxs-lookup"><span data-stu-id="654cf-356">bool     AtomicFileProcessing</span></span>   

* <span data-ttu-id="654cf-357">**Verdadeiro** = indica que este outputter requer ficheiros de saída atómico (JSON, XML,...)</span><span class="sxs-lookup"><span data-stu-id="654cf-357">**true** = Indicates that this outputter requires atomic output files (JSON, XML, ...)</span></span>
* <span data-ttu-id="654cf-358">**FALSO** = indica que este outputter pode lidar com ficheiros divididos / distribuídos (CSV, SEQ,...)</span><span class="sxs-lookup"><span data-stu-id="654cf-358">**false** = Indicates that this outputter can deal with split / distributed files (CSV, SEQ, ...)</span></span>

<span data-ttu-id="654cf-359">objetos de programação para principais Olá são **linha** e **saída**.</span><span class="sxs-lookup"><span data-stu-id="654cf-359">hello main programmability objects are **row** and **output**.</span></span> <span data-ttu-id="654cf-360">Olá **linha** objeto é utilizado tooenumerate dados de saída como `IRow` interface.</span><span class="sxs-lookup"><span data-stu-id="654cf-360">hello **row** object is used tooenumerate output data as `IRow` interface.</span></span> <span data-ttu-id="654cf-361">**Saída** é o ficheiro de destino de toohello de dados de saída de tooset utilizados.</span><span class="sxs-lookup"><span data-stu-id="654cf-361">**Output** is used tooset output data toohello target file.</span></span>

<span data-ttu-id="654cf-362">Olá dados de saída são acedidos através do Olá `IRow` interface.</span><span class="sxs-lookup"><span data-stu-id="654cf-362">hello output data is accessed through hello `IRow` interface.</span></span> <span data-ttu-id="654cf-363">Dados de saída são transmitidos uma linha de cada vez.</span><span class="sxs-lookup"><span data-stu-id="654cf-363">Output data is passed a row at a time.</span></span>

<span data-ttu-id="654cf-364">valores individuais Olá são enumerados ao chamar o método Get Olá interface IRow de Olá:</span><span class="sxs-lookup"><span data-stu-id="654cf-364">hello individual values are enumerated by calling hello Get method of hello IRow interface:</span></span>

```
row.Get<string>("column_name")
```

<span data-ttu-id="654cf-365">É possível determinar os nomes das colunas individuais ao chamar `row.Schema`:</span><span class="sxs-lookup"><span data-stu-id="654cf-365">Individual column names can be determined by calling `row.Schema`:</span></span>

```
ISchema schema = row.Schema;
var col = schema[i];
string val = row.Get<string>(col.Name)
```

<span data-ttu-id="654cf-366">Esta abordagem permite-lhe toobuild um outputter flexível para qualquer esquema metadata.</span><span class="sxs-lookup"><span data-stu-id="654cf-366">This approach enables you toobuild a flexible outputter for any metadata schema.</span></span>

<span data-ttu-id="654cf-367">Olá dados de saída são escritos toofile utilizando `System.IO.StreamWriter`.</span><span class="sxs-lookup"><span data-stu-id="654cf-367">hello output data is written toofile by using `System.IO.StreamWriter`.</span></span> <span data-ttu-id="654cf-368">parâmetro de fluxo de Olá está definido demasiado`output.BaseStrea` como parte da `IUnstructuredWriter output`.</span><span class="sxs-lookup"><span data-stu-id="654cf-368">hello stream parameter is set too`output.BaseStrea` as part of `IUnstructuredWriter output`.</span></span>

<span data-ttu-id="654cf-369">Tenha em atenção que é importante tooflush Olá dados da memória intermédia toohello ficheiro após cada iteração de linha.</span><span class="sxs-lookup"><span data-stu-id="654cf-369">Note that it's important tooflush hello data buffer toohello file after each row iteration.</span></span> <span data-ttu-id="654cf-370">Além disso, Olá `StreamWriter` objeto tem de ser utilizado com Olá Disposable atributo ativada (predefinição) e com Olá **utilizando** palavra-chave:</span><span class="sxs-lookup"><span data-stu-id="654cf-370">In addition, hello `StreamWriter` object must be used with hello Disposable attribute enabled (default) and with hello **using** keyword:</span></span>

```
using (StreamWriter streamWriter = new StreamWriter(output.BaseStream, this._encoding))
{
…
}
```

<span data-ttu-id="654cf-371">Caso contrário, chame o método Flush() explicitamente após cada iteração.</span><span class="sxs-lookup"><span data-stu-id="654cf-371">Otherwise, call Flush() method explicitly after each iteration.</span></span> <span data-ttu-id="654cf-372">Vamos mostrar isto em Olá seguinte exemplo.</span><span class="sxs-lookup"><span data-stu-id="654cf-372">We show this in hello following example.</span></span>

### <a name="set-headers-and-footers-for-user-defined-outputter"></a><span data-ttu-id="654cf-373">Definir cabeçalhos e rodapés de página para outputter definido pelo utilizador</span><span class="sxs-lookup"><span data-stu-id="654cf-373">Set headers and footers for user-defined outputter</span></span>
<span data-ttu-id="654cf-374">tooset cabeçalho, utilize o fluxo de execução única iteração.</span><span class="sxs-lookup"><span data-stu-id="654cf-374">tooset a header, use single iteration execution flow.</span></span>

```
public override void Output(IRow row, IUnstructuredWriter output)
{
 …
if (isHeaderRow)
{
    …                
}

 …
if (isHeaderRow)
{
    isHeaderRow = false;
}
 …
}
}
```

<span data-ttu-id="654cf-375">Olá código Olá primeiro `if (isHeaderRow)` bloco é executado apenas uma vez.</span><span class="sxs-lookup"><span data-stu-id="654cf-375">hello code in hello first `if (isHeaderRow)` block is executed only once.</span></span>

<span data-ttu-id="654cf-376">Para o rodapé Olá, utilize Olá referência toohello instância `System.IO.Stream` objeto (`output.BaseStream`).</span><span class="sxs-lookup"><span data-stu-id="654cf-376">For hello footer, use hello reference toohello instance of `System.IO.Stream` object (`output.BaseStream`).</span></span> <span data-ttu-id="654cf-377">Escrever rodapé Olá em Olá método Close() Olá `IOutputter` interface.</span><span class="sxs-lookup"><span data-stu-id="654cf-377">Write hello footer in hello Close() method of hello `IOutputter` interface.</span></span>  <span data-ttu-id="654cf-378">(Para obter mais informações, consulte o seguinte exemplo de Olá.)</span><span class="sxs-lookup"><span data-stu-id="654cf-378">(For more information, see hello following example.)</span></span>

<span data-ttu-id="654cf-379">Segue-se um exemplo de um outputter definido pelo utilizador:</span><span class="sxs-lookup"><span data-stu-id="654cf-379">Following is an example of a user-defined outputter:</span></span>

```
[SqlUserDefinedOutputter(AtomicFileProcessing = true)]
public class HTMLOutputter : IOutputter
{
    // Local variables initialization
    private string row_delimiter;
    private char col_delimiter;
    private bool isHeaderRow;
    private Encoding encoding;
    private bool IsTableHeader = true;
    private Stream g_writer;

    // Parameters definition            
    public HTMLOutputter(bool isHeader = false, Encoding encoding = null)
    {
    this.isHeaderRow = isHeader;
    this.encoding = ((encoding == null) ? Encoding.UTF8 : encoding);
    }

    // hello Close method is used toowrite hello footer toohello file. It's executed only once, after all rows
    public override void Close().
    {
    //Reference tooIO.Stream object - g_writer
    StreamWriter streamWriter = new StreamWriter(g_writer, this.encoding);
    streamWriter.Write("</table>");
    streamWriter.Flush();
    streamWriter.Close();
    }

    public override void Output(IRow row, IUnstructuredWriter output)
    {
    System.IO.StreamWriter streamWriter = new StreamWriter(output.BaseStream, this.encoding);

    // Metadata schema initialization tooenumerate column names
    ISchema schema = row.Schema;

    // This is a data-independent header--HTML table definition
    if (IsTableHeader)
    {
        streamWriter.Write("<table border=1>");
        IsTableHeader = false;
    }

    // HTML table attributes
    string header_wrapper_on = "<th>";
    string header_wrapper_off = "</th>";
    string data_wrapper_on = "<td>";
    string data_wrapper_off = "</td>";

    // Header row output--runs only once
    if (isHeaderRow)
    {
        streamWriter.Write("<tr>");
        for (int i = 0; i < schema.Count(); i++)
        {
        var col = schema[i];
        streamWriter.Write(header_wrapper_on + col.Name + header_wrapper_off);
        }
        streamWriter.Write("</tr>");
    }

    // Data row output
    streamWriter.Write("<tr>");                
    for (int i = 0; i < schema.Count(); i++)
    {
        var col = schema[i];
        string val = "";
        try
        {
        // Data type enumeration--required toomatch hello distinct list of types from OUTPUT statement
        switch (col.Type.Name.ToString().ToLower())
        {
            case "string": val = row.Get<string>(col.Name).ToString(); break;
            case "guid": val = row.Get<Guid>(col.Name).ToString(); break;
            default: break;
        }
        }
        // Handling NULL values--keeping them empty
        catch (System.NullReferenceException)
        {
        }
        streamWriter.Write(data_wrapper_on + val + data_wrapper_off);
    }
    streamWriter.Write("</tr>");

    if (isHeaderRow)
    {
        isHeaderRow = false;
    }
    // Reference toohello instance of hello IO.Stream object for footer generation
    g_writer = output.BaseStream;
    streamWriter.Flush();
    }
}

// Define hello factory classes
public static class Factory
{
    public static HTMLOutputter HTMLOutputter(bool isHeader = false, Encoding encoding = null)
    {
    return new HTMLOutputter(isHeader, encoding);
    }
}
```

<span data-ttu-id="654cf-380">E o script U-SQL de base:</span><span class="sxs-lookup"><span data-stu-id="654cf-380">And U-SQL base script:</span></span>

```
DECLARE @input_file string = @"\usql-programmability\input_file.tsv";
DECLARE @output_file string = @"\usql-programmability\output_file.html";

@rs0 =
    EXTRACT
            guid Guid,
        dt String,
            user String,
            des String
         FROM @input_file
         USING new USQL_Programmability.FullDescriptionExtractor(Encoding.UTF8);

OUTPUT @rs0 
    too@output_file 
    USING new USQL_Programmability.HTMLOutputter(isHeader: true);
```

<span data-ttu-id="654cf-381">Este é um outputter HTML, que cria um ficheiro HTML com a dados da tabela.</span><span class="sxs-lookup"><span data-stu-id="654cf-381">This is an HTML outputter, which creates an HTML file with table data.</span></span>

### <a name="call-outputter-from-u-sql-base-script"></a><span data-ttu-id="654cf-382">Chamada outputter do script U-SQL de base</span><span class="sxs-lookup"><span data-stu-id="654cf-382">Call outputter from U-SQL base script</span></span>
<span data-ttu-id="654cf-383">toocall um outputter personalizado do script de U-SQL base Olá, nova instância de Olá do objeto de outputter Olá tem toobe criado.</span><span class="sxs-lookup"><span data-stu-id="654cf-383">toocall a custom outputter from hello base U-SQL script, hello new instance of hello outputter object has toobe created.</span></span>

```sql
OUTPUT @rs0 too@output_file USING new USQL_Programmability.HTMLOutputter(isHeader: true);
```

<span data-ttu-id="654cf-384">tooavoid criar uma instância do Olá objeto no base script, podemos criar um dispositivo de moldagem de função, conforme mostrado no nosso exemplo anterior:</span><span class="sxs-lookup"><span data-stu-id="654cf-384">tooavoid creating an instance of hello object in base script, we can create a function wrapper, as shown in our earlier example:</span></span>

```c#
        // Define hello factory classes
        public static class Factory
        {
            public static HTMLOutputter HTMLOutputter(bool isHeader = false, Encoding encoding = null)
            {
                return new HTMLOutputter(isHeader, encoding);
            }
        }
```

<span data-ttu-id="654cf-385">Neste caso, chamada original Olá aspeto Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="654cf-385">In this case, hello original call looks like hello following:</span></span>

```
OUTPUT @rs0 
too@output_file 
USING USQL_Programmability.Factory.HTMLOutputter(isHeader: true);
```

## <a name="use-user-defined-processors"></a><span data-ttu-id="654cf-386">Utilizar processadores definidos pelo utilizador</span><span class="sxs-lookup"><span data-stu-id="654cf-386">Use user-defined processors</span></span>
<span data-ttu-id="654cf-387">Processador definido pelo utilizador ou UDP, é um tipo de UDO U-SQL que lhe permite linhas de entrada de Olá tooprocess aplicando as funcionalidades de programação para.</span><span class="sxs-lookup"><span data-stu-id="654cf-387">User-defined processor, or UDP, is a type of U-SQL UDO that enables you tooprocess hello incoming rows by applying programmability features.</span></span> <span data-ttu-id="654cf-388">UDP permite-lhe toocombine colunas, modificar os valores e adicionar novas colunas, se necessário.</span><span class="sxs-lookup"><span data-stu-id="654cf-388">UDP enables you toocombine columns, modify values, and add new columns if necessary.</span></span> <span data-ttu-id="654cf-389">Basicamente, ajuda a tooprocess elementos de dados de tooproduce necessário um conjunto de linhas.</span><span class="sxs-lookup"><span data-stu-id="654cf-389">Basically, it helps tooprocess a rowset tooproduce required data elements.</span></span>

<span data-ttu-id="654cf-390">toodefine um UDP, precisamos toocreate um `IProcessor` interface com Olá `SqlUserDefinedProcessor` atributo, o que é opcional para UDP.</span><span class="sxs-lookup"><span data-stu-id="654cf-390">toodefine a UDP, we need toocreate an `IProcessor` interface with hello `SqlUserDefinedProcessor` attribute, which is optional for UDP.</span></span>

<span data-ttu-id="654cf-391">Esta interface deve conter a definição de Olá para Olá `IRow` conjunto de linhas de interface substituir, conforme mostrado no seguinte exemplo de Olá:</span><span class="sxs-lookup"><span data-stu-id="654cf-391">This interface should contain hello definition for hello `IRow` interface rowset override, as shown in hello following example:</span></span>

```
[SqlUserDefinedProcessor]
public class MyProcessor: IProcessor
{
public override IRow Process(IRow input, IUpdatableRow output)
 {
        …
 }
}
```

<span data-ttu-id="654cf-392">**SqlUserDefinedProcessor** indica que o tipo de Olá deve ser registado como um processador definido pelo utilizador.</span><span class="sxs-lookup"><span data-stu-id="654cf-392">**SqlUserDefinedProcessor** indicates that hello type should be registered as a user-defined processor.</span></span> <span data-ttu-id="654cf-393">Esta classe não pode ser herdada.</span><span class="sxs-lookup"><span data-stu-id="654cf-393">This class cannot be inherited.</span></span>

<span data-ttu-id="654cf-394">Olá SqlUserDefinedProcessor atributo **opcional** para a definição do UDP.</span><span class="sxs-lookup"><span data-stu-id="654cf-394">hello SqlUserDefinedProcessor attribute is **optional** for UDP definition.</span></span>

<span data-ttu-id="654cf-395">objetos de programação para principais Olá são **entrada** e **saída**.</span><span class="sxs-lookup"><span data-stu-id="654cf-395">hello main programmability objects are **input** and **output**.</span></span> <span data-ttu-id="654cf-396">objeto de entrada Olá é utilizado tooenumerate colunas de entrada e saída e tooset dados de saída como resultado da atividade de processador de Olá.</span><span class="sxs-lookup"><span data-stu-id="654cf-396">hello input object is used tooenumerate input columns and output, and tooset output data as a result of hello processor activity.</span></span>

<span data-ttu-id="654cf-397">Para a enumeração de colunas de entrada, utilizamos Olá `input.Get` método.</span><span class="sxs-lookup"><span data-stu-id="654cf-397">For input columns enumeration, we use hello `input.Get` method.</span></span>

```
string column_name = input.Get<string>("column_name");
```

<span data-ttu-id="654cf-398">Olá parâmetro `input.Get` método é uma coluna que é transmitida como parte da Olá `PRODUCE` cláusula de Olá `PROCESS` declaração do Estado de script base Olá U-SQL.</span><span class="sxs-lookup"><span data-stu-id="654cf-398">hello parameter for `input.Get` method is a column that's passed as part of hello `PRODUCE` clause of hello `PROCESS` statement of hello U-SQL base script.</span></span> <span data-ttu-id="654cf-399">Precisamos toouse do tipo de dados correto de Olá aqui.</span><span class="sxs-lookup"><span data-stu-id="654cf-399">We need toouse hello correct data type here.</span></span>

<span data-ttu-id="654cf-400">Para a saída, utilize Olá `output.Set` método.</span><span class="sxs-lookup"><span data-stu-id="654cf-400">For output, use hello `output.Set` method.</span></span>

<span data-ttu-id="654cf-401">É importante toonote esse produtor personalizado apenas é produz colunas e valores que estão definidos com Olá `output.Set` chamada de método.</span><span class="sxs-lookup"><span data-stu-id="654cf-401">It's important toonote that custom producer only outputs columns and values that are defined with hello `output.Set` method call.</span></span>

```
output.Set<string>("mycolumn", mycolumn);
```

<span data-ttu-id="654cf-402">saída de processador real Olá é acionada ao chamar `return output.AsReadOnly();`.</span><span class="sxs-lookup"><span data-stu-id="654cf-402">hello actual processor output is triggered by calling `return output.AsReadOnly();`.</span></span>

<span data-ttu-id="654cf-403">Segue-se um exemplo de processador:</span><span class="sxs-lookup"><span data-stu-id="654cf-403">Following is a processor example:</span></span>

```
[SqlUserDefinedProcessor]
public class FullDescriptionProcessor : IProcessor
{
public override IRow Process(IRow input, IUpdatableRow output)
 {
     string user = input.Get<string>("user");
     string des = input.Get<string>("des");
     string full_description = user.ToUpper() + "=>" + des;
     output.Set<string>("dt", input.Get<string>("dt"));
     output.Set<string>("full_description", full_description);
     output.Set<Guid>("new_guid", Guid.NewGuid());
     output.Set<Guid>("guid", input.Get<Guid>("guid"));
     return output.AsReadOnly();
 }
}
```

<span data-ttu-id="654cf-404">Neste cenário de caso de utilização, o processador de Olá está a gerar uma nova coluna chamada "full_description" combinando Olá as colunas existentes – neste caso, "utilizador" em maiúsculas e "des".</span><span class="sxs-lookup"><span data-stu-id="654cf-404">In this use-case scenario, hello processor is generating a new column called “full_description” by combining hello existing columns--in this case, “user” in upper case, and “des”.</span></span> <span data-ttu-id="654cf-405">Também gera de novo um GUID e devolve os valores de Olá originais e novo GUID.</span><span class="sxs-lookup"><span data-stu-id="654cf-405">It also regenerates a GUID and returns hello original and new GUID values.</span></span>

<span data-ttu-id="654cf-406">Como pode ver do exemplo anterior Olá, pode chamar métodos c# durante `output.Set` chamada de método.</span><span class="sxs-lookup"><span data-stu-id="654cf-406">As you can see from hello previous example, you can call C# methods during `output.Set` method call.</span></span>

<span data-ttu-id="654cf-407">Segue-se um exemplo de script U-SQL base que utiliza um processador personalizado:</span><span class="sxs-lookup"><span data-stu-id="654cf-407">Following is an example of base U-SQL script that uses a custom processor:</span></span>

```
DECLARE @input_file string = @"\usql-programmability\input_file.tsv";
DECLARE @output_file string = @"\usql-programmability\output_file.tsv";

@rs0 =
    EXTRACT
            guid Guid,
        dt String,
            user String,
            des String
    FROM @input_file USING Extractors.Tsv();

@rs1 =
     PROCESS @rs0
     PRODUCE dt String,
             full_description String,
             guid Guid,
             new_guid Guid
     USING new USQL_Programmability.FullDescriptionProcessor();

OUTPUT @rs1 too@output_file USING Outputters.Text();
```

## <a name="use-user-defined-appliers"></a><span data-ttu-id="654cf-408">Utilizar appliers definido pelo utilizador</span><span class="sxs-lookup"><span data-stu-id="654cf-408">Use user-defined appliers</span></span>
<span data-ttu-id="654cf-409">Um applier do U-SQL definidos pelo utilizador permite-lhe função tooinvoke um personalizado c# para cada linha que é devolvida pela expressão de tabela externa Olá de uma consulta.</span><span class="sxs-lookup"><span data-stu-id="654cf-409">A U-SQL user-defined applier enables you tooinvoke a custom C# function for each row that's returned by hello outer table expression of a query.</span></span> <span data-ttu-id="654cf-410">Olá à direita de entrada é avaliada para cada linha da entrada à esquerda Olá e linhas de Olá que são produzidas são combinadas para o resultado final Olá.</span><span class="sxs-lookup"><span data-stu-id="654cf-410">hello right input is evaluated for each row from hello left input, and hello rows that are produced are combined for hello final output.</span></span> <span data-ttu-id="654cf-411">lista de Olá de colunas que são produzidos pela operadora de rede do Olá aplicar são a combinação de Olá do conjunto de Olá de colunas no lado esquerdo de Olá e Olá de entrada à direita.</span><span class="sxs-lookup"><span data-stu-id="654cf-411">hello list of columns that are produced by hello APPLY operator are hello combination of hello set of columns in hello left and hello right input.</span></span>

<span data-ttu-id="654cf-412">Applier definido pelo utilizador está a ser invocado como parte da Olá USQL SELECIONE expressão.</span><span class="sxs-lookup"><span data-stu-id="654cf-412">User-defined applier is being invoked as part of hello USQL SELECT expression.</span></span>

<span data-ttu-id="654cf-413">Olá chamada típico toohello definido pelo utilizador applier parece Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="654cf-413">hello typical call toohello user-defined applier looks like hello following:</span></span>

```
SELECT …
FROM …
CROSS APPLYis used toopass parameters
new MyScript.MyApplier(param1, param2) AS alias(output_param1 string, …);
```

<span data-ttu-id="654cf-414">Para obter mais informações sobre como utilizar appliers numa expressão SELECT, consulte [U-SQL SELECIONE selecionar de entre aplicar e OUTER APPLY](https://msdn.microsoft.com/library/azure/mt621307.aspx).</span><span class="sxs-lookup"><span data-stu-id="654cf-414">For more information about using appliers in a SELECT expression, see [U-SQL SELECT Selecting from CROSS APPLY and OUTER APPLY](https://msdn.microsoft.com/library/azure/mt621307.aspx).</span></span>

<span data-ttu-id="654cf-415">Olá definido pelo utilizador applier base definição de classe é o seguinte:</span><span class="sxs-lookup"><span data-stu-id="654cf-415">hello user-defined applier base class definition is as follows:</span></span>

```
public abstract class IApplier : IUserDefinedOperator
{
protected IApplier();

public abstract IEnumerable<IRow> Apply(IRow input, IUpdatableRow output);
}
```

<span data-ttu-id="654cf-416">toodefine um applier definido pelo utilizador, precisamos toocreate Olá `IApplier` interface com Olá [`SqlUserDefinedApplier`] atributo, o que é opcional para uma definição applier definido pelo utilizador.</span><span class="sxs-lookup"><span data-stu-id="654cf-416">toodefine a user-defined applier, we need toocreate hello `IApplier` interface with hello [`SqlUserDefinedApplier`] attribute, which is optional for a user-defined applier definition.</span></span>

```
[SqlUserDefinedApplier]
public class ParserApplier : IApplier
{
    public ParserApplier()
    {
        …
    }

    public override IEnumerable<IRow> Apply(IRow input, IUpdatableRow output)
    {
        …
    }
}
```

* <span data-ttu-id="654cf-417">Aplicar é chamado para cada linha da tabela externa Olá.</span><span class="sxs-lookup"><span data-stu-id="654cf-417">Apply is called for each row of hello outer table.</span></span> <span data-ttu-id="654cf-418">Devolve Olá `IUpdatableRow` de saída do conjunto de linhas.</span><span class="sxs-lookup"><span data-stu-id="654cf-418">It returns hello `IUpdatableRow` output rowset.</span></span>
* <span data-ttu-id="654cf-419">a classe de construtor Olá é applier toopass utilizados parâmetros toohello definido pelo utilizador.</span><span class="sxs-lookup"><span data-stu-id="654cf-419">hello Constructor class is used toopass parameters toohello user-defined applier.</span></span>

<span data-ttu-id="654cf-420">**SqlUserDefinedApplier** indica que o tipo de Olá deve ser registado como um applier definido pelo utilizador.</span><span class="sxs-lookup"><span data-stu-id="654cf-420">**SqlUserDefinedApplier** indicates that hello type should be registered as a user-defined applier.</span></span> <span data-ttu-id="654cf-421">Esta classe não pode ser herdada.</span><span class="sxs-lookup"><span data-stu-id="654cf-421">This class cannot be inherited.</span></span>

<span data-ttu-id="654cf-422">**SqlUserDefinedApplier** é **opcional** para uma definição applier definido pelo utilizador.</span><span class="sxs-lookup"><span data-stu-id="654cf-422">**SqlUserDefinedApplier** is **optional** for a user-defined applier definition.</span></span>


<span data-ttu-id="654cf-423">objetos de programação para principais Olá são os seguintes:</span><span class="sxs-lookup"><span data-stu-id="654cf-423">hello main programmability objects are as follows:</span></span>

```
public override IEnumerable<IRow> Apply(IRow input, IUpdatableRow output)
```

<span data-ttu-id="654cf-424">Conjuntos de linhas de entrada são transmitidos como `IRow` entrada.</span><span class="sxs-lookup"><span data-stu-id="654cf-424">Input rowsets are passed as `IRow` input.</span></span> <span data-ttu-id="654cf-425">Olá saída linhas são geradas como `IUpdatableRow` interface de saída.</span><span class="sxs-lookup"><span data-stu-id="654cf-425">hello output rows are generated as `IUpdatableRow` output interface.</span></span>

<span data-ttu-id="654cf-426">Os nomes das colunas individual podem ser determinadas ao chamar Olá `IRow` método de esquema.</span><span class="sxs-lookup"><span data-stu-id="654cf-426">Individual column names can be determined by calling hello `IRow` Schema method.</span></span>

```
ISchema schema = row.Schema;
var col = schema[i];
string val = row.Get<string>(col.Name)
```

<span data-ttu-id="654cf-427">os valores de dados real de Olá tooget da entrada de Olá `IRow`, utilizamos o método Get() Olá `IRow` interface.</span><span class="sxs-lookup"><span data-stu-id="654cf-427">tooget hello actual data values from hello incoming `IRow`, we use hello Get() method of `IRow` interface.</span></span>

```
mycolumn = row.Get<int>("mycolumn")
```

<span data-ttu-id="654cf-428">Ou, utilizamos o nome de coluna de esquema Olá:</span><span class="sxs-lookup"><span data-stu-id="654cf-428">Or we use hello schema column name:</span></span>

```
row.Get<int>(row.Schema[0].Name)
```

<span data-ttu-id="654cf-429">Olá valores de saída tem de ser definidos com `IUpdatableRow` saída:</span><span class="sxs-lookup"><span data-stu-id="654cf-429">hello output values must be set with `IUpdatableRow` output:</span></span>

```
output.Set<int>("mycolumn", mycolumn)
```

<span data-ttu-id="654cf-430">É importante toounderstand que appliers personalizados saída apenas colunas e valores que estão definidos com `output.Set` chamada de método.</span><span class="sxs-lookup"><span data-stu-id="654cf-430">It is important toounderstand that custom appliers only output columns and values that are defined with `output.Set` method call.</span></span>

<span data-ttu-id="654cf-431">saída real Olá é acionada ao chamar `yield return output.AsReadOnly();`.</span><span class="sxs-lookup"><span data-stu-id="654cf-431">hello actual output is triggered by calling `yield return output.AsReadOnly();`.</span></span>

<span data-ttu-id="654cf-432">Olá definido pelo utilizador applier os parâmetros podem ser passados toohello construtor.</span><span class="sxs-lookup"><span data-stu-id="654cf-432">hello user-defined applier parameters can be passed toohello constructor.</span></span> <span data-ttu-id="654cf-433">Applier pode devolver um número de colunas que necessitam de toobe definido durante a chamada de applier Olá no Script de U-SQL base variável.</span><span class="sxs-lookup"><span data-stu-id="654cf-433">Applier can return a variable number of columns that need toobe defined during hello applier call in base U-SQL Script.</span></span>

```
new USQL_Programmability.ParserApplier ("all") AS properties(make string, model string, year string, type string, millage int);
```

<span data-ttu-id="654cf-434">Eis Olá definido pelo utilizador applier exemplo:</span><span class="sxs-lookup"><span data-stu-id="654cf-434">Here is hello user-defined applier example:</span></span>

```
[SqlUserDefinedApplier]
public class ParserApplier : IApplier
{
private string parsingPart;

public ParserApplier(string parsingPart)
{
    if (parsingPart.ToUpper().Contains("ALL")
    || parsingPart.ToUpper().Contains("MAKE")
    || parsingPart.ToUpper().Contains("MODEL")
    || parsingPart.ToUpper().Contains("YEAR")
    || parsingPart.ToUpper().Contains("TYPE")
    || parsingPart.ToUpper().Contains("MILLAGE")
    )
    {
    this.parsingPart = parsingPart;
    }
    else
    {
    throw new ArgumentException("Incorrect parameter. Please use: 'ALL[MAKE|MODEL|TYPE|MILLAGE]'");
    }
}

public override IEnumerable<IRow> Apply(IRow input, IUpdatableRow output)
{

    string[] properties = input.Get<string>("properties").Split(',');

    //  only process with correct number of properties
    if (properties.Count() == 5)
    {

    string make = properties[0];
    string model = properties[1];
    string year = properties[2];
    string type = properties[3];
    int millage = -1;

    // Only return millage if it is number, otherwise, -1
    if (!int.TryParse(properties[4], out millage))
    {
        millage = -1;
    }

    if (parsingPart.ToUpper().Contains("MAKE") || parsingPart.ToUpper().Contains("ALL")) output.Set<string>("make", make);
    if (parsingPart.ToUpper().Contains("MODEL") || parsingPart.ToUpper().Contains("ALL")) output.Set<string>("model", model);
    if (parsingPart.ToUpper().Contains("YEAR") || parsingPart.ToUpper().Contains("ALL")) output.Set<string>("year", year);
    if (parsingPart.ToUpper().Contains("TYPE") || parsingPart.ToUpper().Contains("ALL")) output.Set<string>("type", type);
    if (parsingPart.ToUpper().Contains("MILLAGE") || parsingPart.ToUpper().Contains("ALL")) output.Set<int>("millage", millage);
    }
    yield return output.AsReadOnly();            
}
}
```

<span data-ttu-id="654cf-435">Segue-se script U-SQL base Olá para este applier definido pelo utilizador:</span><span class="sxs-lookup"><span data-stu-id="654cf-435">Following is hello base U-SQL script for this user-defined applier:</span></span>

```
DECLARE @input_file string = @"c:\usql-programmability\car_fleet.tsv";
DECLARE @output_file string = @"c:\usql-programmability\output_file.tsv";

@rs0 =
    EXTRACT
        stocknumber int,
        vin String,
        properties String
    FROM @input_file USING Extractors.Tsv();

@rs1 =
    SELECT
        r.stocknumber,
        r.vin,
        properties.make,
        properties.model,
        properties.year,
        properties.type,
        properties.millage
    FROM @rs0 AS r
    CROSS APPLY
    new USQL_Programmability.ParserApplier ("all") AS properties(make string, model string, year string, type string, millage int);

OUTPUT @rs1 too@output_file USING Outputters.Text();
```

<span data-ttu-id="654cf-436">Neste cenário de cenários de utilização, atos applier definido pelo utilizador como um analisador de valor delimitado por vírgulas para carro Olá fleet propriedades.</span><span class="sxs-lookup"><span data-stu-id="654cf-436">In this use case scenario, user-defined applier acts as a comma-delimited value parser for hello car fleet properties.</span></span> <span data-ttu-id="654cf-437">linhas de ficheiro de entrada Olá aspeto Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="654cf-437">hello input file rows look like hello following:</span></span>

```
103 Z1AB2CD123XY45889   Ford,Explorer,2005,SUV,152345
303 Y0AB2CD34XY458890   Shevrolet,Cruise,2010,4Dr,32455
210 X5AB2CD45XY458893   Nissan,Altima,2011,4Dr,74000
```

<span data-ttu-id="654cf-438">É um ficheiro do TSV típico de ' delimitada por separador ' para com uma coluna de propriedades que contém as propriedades de car como a marca e modelo.</span><span class="sxs-lookup"><span data-stu-id="654cf-438">It is a typical tab-delimited TSV file with a properties column that contains car properties such as make and model.</span></span> <span data-ttu-id="654cf-439">Essas propriedades tem de ser analisados toohello colunas da tabela.</span><span class="sxs-lookup"><span data-stu-id="654cf-439">Those properties must be parsed toohello table columns.</span></span> <span data-ttu-id="654cf-440">applier Olá fornecida também permite-lhe toogenerate dinâmica diversas propriedades no Olá resultam conjunto de linhas, com base no parâmetro Olá que é transmitido.</span><span class="sxs-lookup"><span data-stu-id="654cf-440">hello applier that's provided also enables you toogenerate a dynamic number of properties in hello result rowset, based on hello parameter that's passed.</span></span> <span data-ttu-id="654cf-441">Pode gerar todas as propriedades ou um conjunto específico de propriedades apenas.</span><span class="sxs-lookup"><span data-stu-id="654cf-441">You can generate either all properties or a specific set of properties only.</span></span>

    …USQL_Programmability.ParserApplier ("all")
    …USQL_Programmability.ParserApplier ("make")
    …USQL_Programmability.ParserApplier ("make&model")

<span data-ttu-id="654cf-442">pode ser chamado applier definido pelo utilizador de Olá como uma nova instância do objeto applier:</span><span class="sxs-lookup"><span data-stu-id="654cf-442">hello user-defined applier can be called as a new instance of applier object:</span></span>

```
CROSS APPLY new MyNameSpace.MyApplier (parameter: “value”) AS alias([columns types]…);
```

<span data-ttu-id="654cf-443">Ou com invocação Olá de um método de fábrica do dispositivo de moldagem:</span><span class="sxs-lookup"><span data-stu-id="654cf-443">Or with hello invocation of a wrapper factory method:</span></span>

```c#
    CROSS APPLY MyNameSpace.MyApplier (parameter: “value”) AS alias([columns types]…);
```

## <a name="use-user-defined-combiners"></a><span data-ttu-id="654cf-444">Utilizar combiners definido pelo utilizador</span><span class="sxs-lookup"><span data-stu-id="654cf-444">Use user-defined combiners</span></span>
<span data-ttu-id="654cf-445">Combinação definido pelo utilizador ou UDC, permite-lhe toocombine linhas da esquerda e direita conjuntos de linhas, com base na lógica personalizada.</span><span class="sxs-lookup"><span data-stu-id="654cf-445">User-defined combiner, or UDC, enables you toocombine rows from left and right rowsets, based on custom logic.</span></span> <span data-ttu-id="654cf-446">Combinação definido pelo utilizador é utilizada com a expressão de combinação.</span><span class="sxs-lookup"><span data-stu-id="654cf-446">User-defined combiner is used with COMBINE expression.</span></span>

<span data-ttu-id="654cf-447">Uma combinação está a ser invocada com a expressão de combinação Olá que fornece as informações sobre os dois conjuntos de linhas de entrada Olá necessárias Olá, Olá agrupamento de colunas, hello esperado esquema de resultado e informações adicionais.</span><span class="sxs-lookup"><span data-stu-id="654cf-447">A combiner is being invoked with hello COMBINE expression that provides hello necessary information about both hello input rowsets, hello grouping columns, hello expected result schema, and additional information.</span></span>

<span data-ttu-id="654cf-448">toocall uma combinação num script U-SQL base, podemos utilizar Olá sintaxe:</span><span class="sxs-lookup"><span data-stu-id="654cf-448">toocall a combiner in a base U-SQL script, we use hello following syntax:</span></span>

```
Combine_Expression :=
    'COMBINE' Combine_Input
    'WITH' Combine_Input
    Join_On_Clause
    Produce_Clause
    [Readonly_Clause]
    [Required_Clause]
    USING_Clause.
```

<span data-ttu-id="654cf-449">Para obter mais informações, consulte [COMBINAR expressão (U-SQL)](https://msdn.microsoft.com/library/azure/mt621339.aspx).</span><span class="sxs-lookup"><span data-stu-id="654cf-449">For more information, see [COMBINE Expression (U-SQL)](https://msdn.microsoft.com/library/azure/mt621339.aspx).</span></span>

<span data-ttu-id="654cf-450">toodefine uma combinação de definido pelo utilizador, precisamos toocreate Olá `ICombiner` interface com Olá [`SqlUserDefinedCombiner`] atributo, o que é opcional para uma definição de combinação definido pelo utilizador.</span><span class="sxs-lookup"><span data-stu-id="654cf-450">toodefine a user-defined combiner, we need toocreate hello `ICombiner` interface with hello [`SqlUserDefinedCombiner`] attribute, which is optional for a user-defined Combiner definition.</span></span>

<span data-ttu-id="654cf-451">Base `ICombiner` definição de classe:</span><span class="sxs-lookup"><span data-stu-id="654cf-451">Base `ICombiner` class definition:</span></span>

```
public abstract class ICombiner : IUserDefinedOperator
{
protected ICombiner();
public virtual IEnumerable<IRow> Combine(List<IRowset> inputs,
       IUpdatableRow output);
public abstract IEnumerable<IRow> Combine(IRowset left, IRowset right,
       IUpdatableRow output);
}
```

<span data-ttu-id="654cf-452">Olá implementação personalizada de um `ICombiner` interface deve conter a definição de Olá para um `IEnumerable<IRow>` combinar substituição.</span><span class="sxs-lookup"><span data-stu-id="654cf-452">hello custom implementation of an `ICombiner` interface should contain hello definition for an `IEnumerable<IRow>` Combine override.</span></span>

```
[SqlUserDefinedCombiner]
public class MyCombiner : ICombiner
{

public override IEnumerable<IRow> Combine(IRowset left, IRowset right,
    IUpdatableRow output)
{
    …
}
}
```

<span data-ttu-id="654cf-453">Olá **SqlUserDefinedCombiner** atributo indica que o tipo de Olá deve ser registado como uma combinação de definido pelo utilizador.</span><span class="sxs-lookup"><span data-stu-id="654cf-453">hello **SqlUserDefinedCombiner** attribute indicates that hello type should be registered as a user-defined combiner.</span></span> <span data-ttu-id="654cf-454">Esta classe não pode ser herdada.</span><span class="sxs-lookup"><span data-stu-id="654cf-454">This class cannot be inherited.</span></span>

<span data-ttu-id="654cf-455">**SqlUserDefinedCombiner** é propriedade de modo de combinação de Olá toodefine utilizados.</span><span class="sxs-lookup"><span data-stu-id="654cf-455">**SqlUserDefinedCombiner** is used toodefine hello Combiner mode property.</span></span> <span data-ttu-id="654cf-456">É um atributo opcional para uma definição de combinação definido pelo utilizador.</span><span class="sxs-lookup"><span data-stu-id="654cf-456">It is an optional attribute for a user-defined combiner definition.</span></span>

<span data-ttu-id="654cf-457">Modo de CombinerMode</span><span class="sxs-lookup"><span data-stu-id="654cf-457">CombinerMode     Mode</span></span>

<span data-ttu-id="654cf-458">Enumeração de CombinerMode pode demorar Olá os seguintes valores:</span><span class="sxs-lookup"><span data-stu-id="654cf-458">CombinerMode enum can take hello following values:</span></span>

* <span data-ttu-id="654cf-459">Completo (0), que cada linha de saída depende potencialmente todas as linhas de entrada de Olá da esquerda e à direita com Olá mesmo valor de chave.</span><span class="sxs-lookup"><span data-stu-id="654cf-459">Full  (0) Every output row potentially depends on all hello input rows from left and right       with hello same key value.</span></span>

* <span data-ttu-id="654cf-460">À esquerda (1), cada linha de saída depende de uma única linha de entrada da esquerda Olá (e, potencialmente, todas as linhas da Olá à direita com Olá mesmo valor da chave).</span><span class="sxs-lookup"><span data-stu-id="654cf-460">Left  (1) Every output row depends on a single input row from hello left (and potentially all rows       from hello right with hello same key value).</span></span>

* <span data-ttu-id="654cf-461">À direita (2), cada linha de saída depende de uma única linha de entrada de Olá direito (e, potencialmente, todas as linhas da esquerda Olá com Olá mesmo valor da chave).</span><span class="sxs-lookup"><span data-stu-id="654cf-461">Right (2)     Every output row depends on a single input row from hello right (and potentially all rows       from hello left with hello same key value).</span></span>

* <span data-ttu-id="654cf-462">Linha de cada linha de saída depende de uma única entrada interna (3) da esquerda e direita com Olá mesmo valor.</span><span class="sxs-lookup"><span data-stu-id="654cf-462">Inner (3) Every output row depends on a single input row from left and right with hello same value.</span></span>

<span data-ttu-id="654cf-463">Exemplo: [`SqlUserDefinedCombiner(Mode=CombinerMode.Left)`]</span><span class="sxs-lookup"><span data-stu-id="654cf-463">Example:    [`SqlUserDefinedCombiner(Mode=CombinerMode.Left)`]</span></span>


<span data-ttu-id="654cf-464">objetos de programação para principais Olá são:</span><span class="sxs-lookup"><span data-stu-id="654cf-464">hello main programmability objects are:</span></span>

```c#
    public override IEnumerable<IRow> Combine(IRowset left, IRowset right,
        IUpdatableRow output
```

<span data-ttu-id="654cf-465">Conjuntos de linhas de entrada são transmitidos como **esquerdo** e **direita** `IRowset` tipo de interface.</span><span class="sxs-lookup"><span data-stu-id="654cf-465">Input rowsets are passed as **left** and **right** `IRowset` type of interface.</span></span> <span data-ttu-id="654cf-466">Ambos os conjuntos de linhas tem de ser enumerados para processamento.</span><span class="sxs-lookup"><span data-stu-id="654cf-466">Both rowsets must be enumerated for processing.</span></span> <span data-ttu-id="654cf-467">Apenas pode enumerar cada interface de uma só vez, pelo que estamos a ter tooenumerate e cache-la, se necessário.</span><span class="sxs-lookup"><span data-stu-id="654cf-467">You can only enumerate each interface once, so we have tooenumerate and cache it if necessary.</span></span>

<span data-ttu-id="654cf-468">Para efeitos de colocação em cache, podemos criar uma lista\<T\> tipo de estrutura de memória como resultado de uma LINQ execução da consulta, especificamente lista <`IRow`>.</span><span class="sxs-lookup"><span data-stu-id="654cf-468">For caching purposes, we can create a List\<T\> type of memory structure as a result of a LINQ query execution, specifically List<`IRow`>.</span></span> <span data-ttu-id="654cf-469">tipo de dados anónimos Olá pode ser utilizado durante a enumeração bem.</span><span class="sxs-lookup"><span data-stu-id="654cf-469">hello anonymous data type can be used during enumeration as well.</span></span>

<span data-ttu-id="654cf-470">Consulte [introdução tooLINQ consultas (c#)](https://msdn.microsoft.com/library/bb397906.aspx) para obter mais informações sobre consultas LINQ, e [IEnumerable\<T\> Interface](https://msdn.microsoft.com/library/9eekhta0(v=vs.110).aspx) para obter mais informações sobre IEnumerable\<T\> interface.</span><span class="sxs-lookup"><span data-stu-id="654cf-470">See [Introduction tooLINQ Queries (C#)](https://msdn.microsoft.com/library/bb397906.aspx) for more information about LINQ queries, and [IEnumerable\<T\> Interface](https://msdn.microsoft.com/library/9eekhta0(v=vs.110).aspx) for more information about IEnumerable\<T\> interface.</span></span>

<span data-ttu-id="654cf-471">os valores de dados real de Olá tooget da entrada de Olá `IRowset`, utilizamos o método Get() Olá `IRow` interface.</span><span class="sxs-lookup"><span data-stu-id="654cf-471">tooget hello actual data values from hello incoming `IRowset`, we use hello Get() method of `IRow` interface.</span></span>

```
mycolumn = row.Get<int>("mycolumn")
```

<span data-ttu-id="654cf-472">Os nomes das colunas individual podem ser determinadas ao chamar Olá `IRow` método de esquema.</span><span class="sxs-lookup"><span data-stu-id="654cf-472">Individual column names can be determined by calling hello `IRow` Schema method.</span></span>

```
ISchema schema = row.Schema;
var col = schema[i];
string val = row.Get<string>(col.Name)
```

<span data-ttu-id="654cf-473">Ou utilizando o nome de coluna de esquema Olá:</span><span class="sxs-lookup"><span data-stu-id="654cf-473">Or by using hello schema column name:</span></span>

```
c# row.Get<int>(row.Schema[0].Name)
```

<span data-ttu-id="654cf-474">enumeração de geral Olá com LINQ aspeto Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="654cf-474">hello general enumeration with LINQ looks like hello following:</span></span>

```
var myRowset =
            (from row in left.Rows
                          select new
                          {
                              Mycolumn = row.Get<int>("mycolumn"),
                          }).ToList();
```

<span data-ttu-id="654cf-475">Após a enumerar os dois conjuntos de linhas, vamos tooloop através de todas as linhas.</span><span class="sxs-lookup"><span data-stu-id="654cf-475">After enumerating both rowsets, we are going tooloop through all rows.</span></span> <span data-ttu-id="654cf-476">Para cada linha no conjunto de linhas esquerdo Olá, vamos toofind todas as linhas que satisfaçam a condição de Olá do nosso combinação.</span><span class="sxs-lookup"><span data-stu-id="654cf-476">For each row in hello left rowset, we are going toofind all rows that satisfy hello condition of our combiner.</span></span>

<span data-ttu-id="654cf-477">Olá valores de saída tem de ser definidos com `IUpdatableRow` saída.</span><span class="sxs-lookup"><span data-stu-id="654cf-477">hello output values must be set with `IUpdatableRow` output.</span></span>

```
output.Set<int>("mycolumn", mycolumn)
```

<span data-ttu-id="654cf-478">saída real Olá é acionada ao chamar demasiado`yield return output.AsReadOnly();`.</span><span class="sxs-lookup"><span data-stu-id="654cf-478">hello actual output is triggered by calling too`yield return output.AsReadOnly();`.</span></span>

<span data-ttu-id="654cf-479">Segue-se um exemplo de combinação:</span><span class="sxs-lookup"><span data-stu-id="654cf-479">Following is a combiner example:</span></span>

```
[SqlUserDefinedCombiner]
public class CombineSales : ICombiner
{

public override IEnumerable<IRow> Combine(IRowset left, IRowset right,
    IUpdatableRow output)
{
    var internetSales =
    (from row in left.Rows
          select new
          {
              ProductKey = row.Get<int>("ProductKey"),
              OrderDateKey = row.Get<int>("OrderDateKey"),
              SalesAmount = row.Get<decimal>("SalesAmount"),
              TaxAmt = row.Get<decimal>("TaxAmt")
          }).ToList();

    var resellerSales =
    (from row in right.Rows
     select new
     {
     ProductKey = row.Get<int>("ProductKey"),
     OrderDateKey = row.Get<int>("OrderDateKey"),
     SalesAmount = row.Get<decimal>("SalesAmount"),
     TaxAmt = row.Get<decimal>("TaxAmt")
     }).ToList();

    foreach (var row_i in internetSales)
    {
    foreach (var row_r in resellerSales)
    {

        if (
        row_i.OrderDateKey > 0
        && row_i.OrderDateKey < row_r.OrderDateKey
        && row_i.OrderDateKey == 20010701
        && (row_r.SalesAmount + row_r.TaxAmt) > 20000)
        {
        output.Set<int>("OrderDateKey", row_i.OrderDateKey);
        output.Set<int>("ProductKey", row_i.ProductKey);
        output.Set<decimal>("Internet_Sales_Amount", row_i.SalesAmount + row_i.TaxAmt);
        output.Set<decimal>("Reseller_Sales_Amount", row_r.SalesAmount + row_r.TaxAmt);
        }

    }
    }
    yield return output.AsReadOnly();
}
}
```

<span data-ttu-id="654cf-480">Neste cenário de caso de utilização, iremos está a criar um relatório de análise para revendedor Olá.</span><span class="sxs-lookup"><span data-stu-id="654cf-480">In this use-case scenario, we are building an analytics report for hello retailer.</span></span> <span data-ttu-id="654cf-481">o objetivo de Olá é toofind todos os produtos de custo mais de 20.000 $ e que propor através do Web site Olá mais rápida do que através de revendedor regular de Olá num determinado período de tempo.</span><span class="sxs-lookup"><span data-stu-id="654cf-481">hello goal is toofind all products that cost more than $20,000 and that sell through hello website faster than through hello regular retailer within a certain time frame.</span></span>

<span data-ttu-id="654cf-482">Eis o script de U-SQL base Olá.</span><span class="sxs-lookup"><span data-stu-id="654cf-482">Here is hello base U-SQL script.</span></span> <span data-ttu-id="654cf-483">Pode comparar lógica Olá entre uma associação regular e uma combinação:</span><span class="sxs-lookup"><span data-stu-id="654cf-483">You can compare hello logic between a regular JOIN and a combiner:</span></span>

```sql
DECLARE @LocalURI string = @"\usql-programmability\";

DECLARE @input_file_internet_sales string = @LocalURI+"FactInternetSales.txt";
DECLARE @input_file_reseller_sales string = @LocalURI+"FactResellerSales.txt";
DECLARE @output_file1 string = @LocalURI+"output_file1.tsv";
DECLARE @output_file2 string = @LocalURI+"output_file2.tsv";

@fact_internet_sales =
EXTRACT
    ProductKey int ,
    OrderDateKey int ,
    DueDateKey int ,
    ShipDateKey int ,
    CustomerKey int ,
    PromotionKey int ,
    CurrencyKey int ,
    SalesTerritoryKey int ,
    SalesOrderNumber String ,
    SalesOrderLineNumber  int ,
    RevisionNumber int ,
    OrderQuantity int ,
    UnitPrice decimal ,
    ExtendedAmount decimal,
    UnitPriceDiscountPct float ,
    DiscountAmount float ,
    ProductStandardCost decimal ,
    TotalProductCost decimal ,
    SalesAmount decimal ,
    TaxAmt decimal ,
    Freight decimal ,
    CarrierTrackingNumber String,
    CustomerPONumber String
FROM @input_file_internet_sales
USING Extractors.Text(delimiter:'|', encoding: Encoding.Unicode);

@fact_reseller_sales =
EXTRACT
    ProductKey int ,
    OrderDateKey int ,
    DueDateKey int ,
    ShipDateKey int ,
    ResellerKey int ,
    EmployeeKey int ,
    PromotionKey int ,
    CurrencyKey int ,
    SalesTerritoryKey int ,
    SalesOrderNumber String ,
    SalesOrderLineNumber  int ,
    RevisionNumber int ,
    OrderQuantity int ,
    UnitPrice decimal ,
    ExtendedAmount decimal,
    UnitPriceDiscountPct float ,
    DiscountAmount float ,
    ProductStandardCost decimal ,
    TotalProductCost decimal ,
    SalesAmount decimal ,
    TaxAmt decimal ,
    Freight decimal ,
    CarrierTrackingNumber String,
    CustomerPONumber String
FROM @input_file_reseller_sales
USING Extractors.Text(delimiter:'|', encoding: Encoding.Unicode);

@rs1 =
SELECT
    fis.OrderDateKey,
    fis.ProductKey,
    fis.SalesAmount+fis.TaxAmt AS Internet_Sales_Amount,
    frs.SalesAmount+frs.TaxAmt AS Reseller_Sales_Amount
FROM @fact_internet_sales AS fis
     INNER JOIN @fact_reseller_sales AS frs
     ON fis.ProductKey == frs.ProductKey
WHERE
    fis.OrderDateKey < frs.OrderDateKey
    AND fis.OrderDateKey == 20010701
    AND frs.SalesAmount+frs.TaxAmt > 20000;

@rs2 =
COMBINE @fact_internet_sales AS fis
WITH @fact_reseller_sales AS frs
ON fis.ProductKey == frs.ProductKey
PRODUCE OrderDateKey int,
        ProductKey int,
        Internet_Sales_Amount decimal,
        Reseller_Sales_Amount decimal
USING new USQL_Programmability.CombineSales();

OUTPUT @rs1 too@output_file1 USING Outputters.Tsv();
OUTPUT @rs2 too@output_file2 USING Outputters.Tsv();
```

<span data-ttu-id="654cf-484">Pode ser chamada uma combinação de definido pelo utilizador como uma nova instância do objeto applier Olá:</span><span class="sxs-lookup"><span data-stu-id="654cf-484">A user-defined combiner can be called as a new instance of hello applier object:</span></span>

```
USING new MyNameSpace.MyCombiner();
```


<span data-ttu-id="654cf-485">Ou com invocação Olá de um método de fábrica do dispositivo de moldagem:</span><span class="sxs-lookup"><span data-stu-id="654cf-485">Or with hello invocation of a wrapper factory method:</span></span>

```
USING MyNameSpace.MyCombiner();
```

## <a name="use-user-defined-reducers"></a><span data-ttu-id="654cf-486">Utilizar reducers definido pelo utilizador</span><span class="sxs-lookup"><span data-stu-id="654cf-486">Use user-defined reducers</span></span>

<span data-ttu-id="654cf-487">U-SQL permite-lhe toowrite reducers de conjunto de linhas personalizadas em c# utilizando a estrutura de extensibilidade de operador definido pelo utilizador Olá e implementar uma interface IReducer.</span><span class="sxs-lookup"><span data-stu-id="654cf-487">U-SQL enables you toowrite custom rowset reducers in C# by using hello user-defined operator extensibility framework and implementing an IReducer interface.</span></span>

<span data-ttu-id="654cf-488">Definido pelo utilizador reducer ou UDR, pode ser linhas desnecessários tooeliminate utilizado durante a extração de dados (importar).</span><span class="sxs-lookup"><span data-stu-id="654cf-488">User-defined reducer, or UDR, can be used tooeliminate unnecessary rows during data extraction (import).</span></span> <span data-ttu-id="654cf-489">Também pode ser utilizado toomanipulate e avaliar linhas e colunas.</span><span class="sxs-lookup"><span data-stu-id="654cf-489">It also can be used toomanipulate and evaluate rows and columns.</span></span> <span data-ttu-id="654cf-490">Com base na lógica de programação para, também pode definir que linhas necessário toobe extraído.</span><span class="sxs-lookup"><span data-stu-id="654cf-490">Based on programmability logic, it can also define which rows need toobe extracted.</span></span>

<span data-ttu-id="654cf-491">uma classe UDR toodefine, precisamos toocreate um `IReducer` interface com opcional `SqlUserDefinedReducer` atributo.</span><span class="sxs-lookup"><span data-stu-id="654cf-491">toodefine a UDR class, we need toocreate an `IReducer` interface with an optional `SqlUserDefinedReducer` attribute.</span></span>

<span data-ttu-id="654cf-492">Esta interface de classe deve conter uma definição para Olá `IEnumerable` substituir o conjunto de linhas de interface.</span><span class="sxs-lookup"><span data-stu-id="654cf-492">This class interface should contain a definition for hello `IEnumerable` interface rowset override.</span></span>

```
[SqlUserDefinedReducer]
public class EmptyUserReducer : IReducer
{

    public override IEnumerable<IRow> Reduce(IRowset input, IUpdatableRow output)
    {
        …
    }

}
```

<span data-ttu-id="654cf-493">Olá **SqlUserDefinedReducer** atributo indica que o tipo de Olá deve ser registado como um reducer definido pelo utilizador.</span><span class="sxs-lookup"><span data-stu-id="654cf-493">hello **SqlUserDefinedReducer** attribute indicates that hello type should be registered as a user-defined reducer.</span></span> <span data-ttu-id="654cf-494">Esta classe não pode ser herdada.</span><span class="sxs-lookup"><span data-stu-id="654cf-494">This class cannot be inherited.</span></span>
<span data-ttu-id="654cf-495">**SqlUserDefinedReducer** é um atributo opcional para uma definição de reducer definido pelo utilizador.</span><span class="sxs-lookup"><span data-stu-id="654cf-495">**SqlUserDefinedReducer** is an optional attribute for a user-defined reducer definition.</span></span> <span data-ttu-id="654cf-496">Utilizou o toodefine IsRecursive propriedade.</span><span class="sxs-lookup"><span data-stu-id="654cf-496">It's used toodefine IsRecursive property.</span></span>

* <span data-ttu-id="654cf-497">bool IsRecursive</span><span class="sxs-lookup"><span data-stu-id="654cf-497">bool     IsRecursive</span></span>    
* <span data-ttu-id="654cf-498">**Verdadeiro** = indica se esta Reducer é idempotent</span><span class="sxs-lookup"><span data-stu-id="654cf-498">**true**  = Indicates whether this Reducer is idempotent</span></span>

<span data-ttu-id="654cf-499">objetos de programação para principais Olá são **entrada** e **saída**.</span><span class="sxs-lookup"><span data-stu-id="654cf-499">hello main programmability objects are **input** and **output**.</span></span> <span data-ttu-id="654cf-500">objeto de entrada Olá é utilizado tooenumerate linhas de entrada.</span><span class="sxs-lookup"><span data-stu-id="654cf-500">hello input object is used tooenumerate input rows.</span></span> <span data-ttu-id="654cf-501">O resultado é utilizado tooset linhas de saída como resultado de reduzir a atividade.</span><span class="sxs-lookup"><span data-stu-id="654cf-501">Output is used tooset output rows as a result of reducing activity.</span></span>

<span data-ttu-id="654cf-502">Para a enumeração de linhas de entrada, utilizamos Olá `Row.Get` método.</span><span class="sxs-lookup"><span data-stu-id="654cf-502">For input rows enumeration, we use hello `Row.Get` method.</span></span>

```
foreach (IRow row in input.Rows)
{
    row.Get<string>("mycolumn");
}
```

<span data-ttu-id="654cf-503">Olá parâmetro Olá `Row.Get` método é uma coluna que é transmitida como parte da Olá `PRODUCE` classe de Olá `REDUCE` declaração do Estado de script base Olá U-SQL.</span><span class="sxs-lookup"><span data-stu-id="654cf-503">hello parameter for hello `Row.Get` method is a column that's passed as part of hello `PRODUCE` class of hello `REDUCE` statement of hello U-SQL base script.</span></span> <span data-ttu-id="654cf-504">Precisamos toouse Olá correto do tipo de dados aqui bem.</span><span class="sxs-lookup"><span data-stu-id="654cf-504">We need toouse hello correct data type here as well.</span></span>

<span data-ttu-id="654cf-505">Para a saída, utilize Olá `output.Set` método.</span><span class="sxs-lookup"><span data-stu-id="654cf-505">For output, use hello `output.Set` method.</span></span>

<span data-ttu-id="654cf-506">É importante toounderstand que reducer personalizado únicos saídas valores que estão definidos com Olá `output.Set` chamada de método.</span><span class="sxs-lookup"><span data-stu-id="654cf-506">It is important toounderstand that custom reducer only outputs values that are defined with hello `output.Set` method call.</span></span>

```
output.Set<string>("mycolumn", guid);
```

<span data-ttu-id="654cf-507">saída de reducer real Olá é acionada ao chamar `yield return output.AsReadOnly();`.</span><span class="sxs-lookup"><span data-stu-id="654cf-507">hello actual reducer output is triggered by calling `yield return output.AsReadOnly();`.</span></span>

<span data-ttu-id="654cf-508">Segue-se um exemplo de reducer:</span><span class="sxs-lookup"><span data-stu-id="654cf-508">Following is a reducer example:</span></span>

```
[SqlUserDefinedReducer]
public class EmptyUserReducer : IReducer
{

    public override IEnumerable<IRow> Reduce(IRowset input, IUpdatableRow output)
    {
    string guid;
    DateTime dt;
    string user;
    string des;

    foreach (IRow row in input.Rows)
    {
        guid = row.Get<string>("guid");
        dt = row.Get<DateTime>("dt");
        user = row.Get<string>("user");
        des = row.Get<string>("des");

        if (user.Length > 0)
        {
        output.Set<string>("guid", guid);
        output.Set<DateTime>("dt", dt);
        output.Set<string>("user", user);
        output.Set<string>("des", des);

        yield return output.AsReadOnly();
        }
    }
    }

}
```

<span data-ttu-id="654cf-509">Neste cenário de caso de utilização, reducer Olá está a ignorar as linhas com um nome de utilizador vazio.</span><span class="sxs-lookup"><span data-stu-id="654cf-509">In this use-case scenario, hello reducer is skipping rows with an empty user name.</span></span> <span data-ttu-id="654cf-510">Para cada linha no conjunto de linhas, lê de cada coluna necessária, em seguida, avalia o comprimento do nome de utilizador Olá Olá.</span><span class="sxs-lookup"><span data-stu-id="654cf-510">For each row in rowset, it reads each required column, then evaluates hello length of hello user name.</span></span> <span data-ttu-id="654cf-511">Linha real Olá-produz apenas se o comprimento do valor de nome de utilizador é superior a 0.</span><span class="sxs-lookup"><span data-stu-id="654cf-511">It outputs hello actual row only if user name value length is more than 0.</span></span>

<span data-ttu-id="654cf-512">Segue-se base script U-SQL que utiliza um reducer personalizado:</span><span class="sxs-lookup"><span data-stu-id="654cf-512">Following is base U-SQL script that uses a custom reducer:</span></span>

```
DECLARE @input_file string = @"\usql-programmability\input_file_reducer.tsv";
DECLARE @output_file string = @"\usql-programmability\output_file.tsv";

@rs0 =
    EXTRACT
            guid string,
        dt DateTime,
            user String,
            des String
    FROM @input_file 
    USING Extractors.Tsv();

@rs1 =
    REDUCE @rs0 PRESORT guid
    ON guid  
    PRODUCE guid string, dt DateTime, user String, des String
    USING new USQL_Programmability.EmptyUserReducer();

@rs2 =
    SELECT guid AS start_id,
           dt AS start_time,
           DateTime.Now.ToString("M/d/yyyy") AS Nowdate,
           USQL_Programmability.CustomFunctions.GetFiscalPeriodWithCustomType(dt).ToString() AS start_fiscalperiod,
           user,
           des
    FROM @rs1;

OUTPUT @rs2 
    too@output_file 
    USING Outputters.Text();
```
