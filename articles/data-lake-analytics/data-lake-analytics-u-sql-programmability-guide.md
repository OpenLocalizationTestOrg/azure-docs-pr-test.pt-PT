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
# <a name="u-sql-programmability-guide"></a>Guia de programação para U-SQL

U-SQL é uma linguagem de consulta que foi concebida para o tipo de dados grande de cargas de trabalho. Uma das funcionalidades de exclusivo Olá do U-SQL é a combinação de Olá de linguagem declarativa de como o SQL Olá com extensibilidade Olá e de programação para fornecida pelo c#. Neste guia, iremos nos podermos concentrar nos extensibilidade Olá e de programação para de linguagem U-SQL Olá que está ativada por c#.

## <a name="requirements"></a>Requisitos

Transfira e instale [ferramentas do Azure Data Lake para Visual Studio](https://www.microsoft.com/download/details.aspx?id=49504).

## <a name="get-started-with-u-sql"></a>Introdução ao U-SQL  

Vamos ver Olá seguinte script U-SQL:

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

Define um conjunto de linhas chamado @a e cria um conjunto de linhas chamado @results de @a.

## <a name="c-types-and-expressions-in-u-sql-script"></a>Tipos de c# e expressões no script U-SQL

Uma expressão de U-SQL é uma expressão de c# combinada com operações de lógicas de U-SQL, tais `AND`, `OR`, e `NOT`. As expressões de U-SQL pode ser utilizadas com SELECIONE, a EXTRAIR, WHERE, tendo, agrupar por e declarar.

Por exemplo, Olá seguinte script analisa uma cadeia de um valor de DateTime na cláusula SELECT Olá.

```
@results =
    SELECT
        customer,
    amount,
    DateTime.Parse(date) AS date
    FROM @a;    
```

Olá seguinte script analisa uma cadeia de um valor de DateTime numa instrução DECLARE.

```
DECLARE @d DateTime = ToDateTime.Date("2016/01/01");
```

### <a name="use-c-expressions-for-data-type-conversions"></a>Utilizar c# expressões para conversões de tipo de dados
Olá seguinte o exemplo demonstra como pode efetuar uma conversão de dados datetime através de expressões do c#. Este cenário em particular, dados de datetime da cadeia são convertida toostandard datetime com notação de tempo de 00:00:00 meia-noite.

```
DECLARE @dt String = "2016-07-06 10:23:15";

@rs1 =
    SELECT 
        Convert.ToDateTime(Convert.ToDateTime(@dt).ToString("yyyy-MM-dd")) AS dt,
        dt AS olddt
    FROM @rs0;
OUTPUT @rs1 too@output_file USING Outputters.Text();
```

### <a name="use-c-expressions-for-todays-date"></a>Utilizar expressões de c# para a data de hoje
toopull data de hoje, podemos utilizar Olá seguintes expressão c#:

```
DateTime.Now.ToString("M/d/yyyy")
```

Eis um exemplo de como toouse esta expressão num script:

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



## <a name="using-net-assemblies"></a>Utilizar as assemblagens .NET
Modelo de extensibilidade do U-SQL baseia-se descontos elevados no código personalizado do Olá capacidade tooadd. Atualmente, U-SQL proporciona formas fácil tooadd o seus próprios Microsoft. Código baseado na rede (em especial, c#). No entanto, também pode adicionar código personalizado escrito na outras linguagens .NET, tais como VB.NET ou F #. 

### <a name="register-a-net-assembly"></a>Registar uma assemblagem .NET

Utilize Olá CREATE ASSEMBLY instrução tooplace uma assemblagem .NET numa base de dados U-SQL. Depois de uma assemblagem numa base de dados, scripts U-SQL podem utilizar esses assemblagens utilizando a instrução da referência de ASSEMBLAGEM de Olá. 

Olá a seguir mostra código como tooregister uma assemblagem:

```
CREATE ASSEMBLY MyDB.[MyAssembly]
    FROM "/myassembly.dll";
```

Olá a seguir mostra código como tooreference uma assemblagem:

```
REFERENCE ASSEMBLY MyDB.[MyAssembly];
```

Consulte Olá [instruções de registo de assemblagem](https://blogs.msdn.microsoft.com/azuredatalake/2016/08/26/how-to-register-u-sql-assemblies-in-your-u-sql-catalog/) que abrange este tópico em maior detalhe.


### <a name="use-assembly-versioning"></a>Utilizar o controlo de versões da assemblagem
Atualmente, U-SQL utiliza a Olá .NET Framework versão 4.5. Por isso, certifique-se de que os seus próprios assemblagens são compatíveis com que a versão do tempo de execução Olá.

Conforme mencionado anteriormente, código de execuções de U-SQL num formato de 64 bits (x64). Por isso certifique-se de que o seu código é toorun compilado em x64. Caso contrário, obter o erro de formato incorreto Olá apresentado anteriormente.

Cada carregou a assemblagem DLL e ficheiro de recursos, tais como um tempo de execução diferente, uma assemblagem nativa ou um ficheiro de configuração, pode ter um máximo de 400 MB. tamanho total do Olá dos recursos implementados, ou através de implementar recursos através de tooassemblies referências e os ficheiros adicionais, não pode exceder 3 GB.

Por fim, tenha em atenção que cada base de dados do U-SQL só pode conter uma versão de qualquer assemblagem em questão. Por exemplo, se tiver a versão 7 e versão 8 do Olá biblioteca NewtonSoft Json.Net, terá de tooregistê-las em duas bases de dados diferentes. Além disso, cada script só pode fazer referência tooone versão de uma assemblagem em questão DLL. No que esta respeita o U-SQL segue Olá c# assemblagem gestão e o controlo de versões de semântica.


## <a name="use-user-defined-functions-udf"></a>Utilize as funções definidas pelo utilizador: UDF
As funções definidas pelo utilizador do U-SQL ou UDF, são programação rotinas que aceitam parâmetros, execute uma ação (por exemplo, um cálculo complexo) e devolvem Olá resultado da ação como um valor. Olá devolver o valor de UDF só pode ser uma escalar único. U-SQL UDF pode ser chamado no script de base de U-SQL, como quaisquer outro c# função escalar.

Recomendamos que inicializar U-SQL definidos pelo utilizador as funções como **pública** e **estático**.

```
public static string MyFunction(string param1)
{
    return "my result";
}
```

Primeiro vamos ver exemplo simples de Olá de criação de um UDF.

Neste cenário de caso de utilização, precisamos de toodetermine Olá fiscal período, incluindo trimestre fiscal Olá e mês fiscal de Olá primeiro início de sessão de utilizador específico Olá. Olá primeiro mês fiscal do ano Olá no nosso cenário é Junho.

período de fiscal toocalculate, introduzirmos Olá c# função os seguintes:

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

Basta calcula mês fiscal e trimestre e devolve um valor de cadeia. Para Junho de Olá primeiro mês do Olá trimestre fiscal primeiro, vamos utilizar "Q1:P1". Para Julho, iremos utilizar "Q1:P2" e assim sucessivamente.

Este é uma regular função de c# que iremos são curso toouse no nosso projeto U-SQL.

Eis o aspeto da secção de code-behind Olá neste cenário:

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

Agora, vamos toocall esta função de script de U-SQL base Olá. toodo isto, temos tooprovide um nome completamente qualificado para a função de Olá, incluindo o espaço de nomes de Olá, que neste caso é NameSpace.Class.Function(parameter).

```
USQL_Programmability.CustomFunctions.GetFiscalPeriod(dt)
```

Segue-se as real script base de U-SQL de Olá:

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

Segue-se Olá o ficheiro de saída Olá da execução do script:

```
0d8b9630-d5ca-11e5-8329-251efa3a2941,2016-02-11T07:04:17.2630000-08:00,2016-06-01T00:00:00.0000000,"Q3:8","User1",""

20843640-d771-11e5-b87b-8b7265c75a44,2016-02-11T07:04:17.2630000-08:00,2016-06-01T00:00:00.0000000,"Q3:8","User2",""

301f23d2-d690-11e5-9a98-4b4f60a1836f,2016-02-11T09:01:33.9720000-08:00,2016-06-01T00:00:00.0000000,"Q3:8","User3",""
```

Este exemplo demonstra a utilização de um simple de inline UDF em U-SQL.

### <a name="keep-state-between-udf-invocations"></a>Manter o estado entre invocações de UDF
Objetos de programação para c# do U-SQL podem ser mais sofisticados, a utilização de interatividade através de variáveis globais do Olá code-behind. Vamos ver Olá seguir o cenário de caso de utilização de negócio.

Em grandes organizações, os utilizadores podem alternar entre varieties de aplicações internas. Pode incluir Microsoft Dynamics CRM, PowerBI e assim sucessivamente. Os clientes poderão pretendem tooapply uma análise de telemetria do modo como os utilizadores alternar entre aplicações diferentes, tendências de utilização que Olá estão e assim sucessivamente. objetivo de Hello para empresas Olá é toooptimize da utilização da aplicação. Também poderá pretendem toocombine diferentes aplicações ou rotinas de início de sessão específicas.

tooachieve neste objetivo, temos toodetermine IDs de sessão e do desfasamento de tempo entre Olá última sessão que ocorreram.

Vamos precisar toofind uma anterior início de sessão e, em seguida, atribuir este sessões de início de sessão tooall que estão a ser gerado toohello mesma aplicação. primeiro desafio de Olá é que script U-SQL de base não permite-nos cálculos tooapply por colunas calculadas já com a função LAG. Olá segundo desafio é que temos tookeep Olá específica de sessão para todas as sessões dentro Olá mesmo período de tempo.

toosolve este problema, vamos utilizar uma variável global dentro de uma secção code-behind: `static public string globalSession;`.

Esta variável global é o conjunto de linhas completa do toohello aplicadas durante a execução do script do nosso.

Segue-se a secção do code-behind Olá nosso programa U-SQL:

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

Este exemplo mostra Olá variável global `static public string globalSession;` utilizado dentro de Olá `getStampUserSession` função e a obter reinicializados cada Olá tempo sessão parâmetro é alterado.

Olá script U-SQL de base é o seguinte:

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

Função `USQLApplication21.UserSession.getStampUserSession(UserSessionTimestamp)` é chamado aqui durante o cálculo de conjunto de linhas de memória Olá segundo. Tenha sido enviado Olá `UserSessionTimestamp` coluna e devolve Olá valor até `UserSessionTimestamp` foi alterada.

ficheiro de saída Olá é o seguinte:

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

Este exemplo demonstra um cenário de caso de utilização mais complicado que utilizamos uma variável global dentro de uma secção de code-behind que é o conjunto de linhas do toohello aplicados memória completo.

## <a name="use-user-defined-types-udt"></a>Utilizar tipos definidos pelo utilizador: UDT
Os tipos definidos pelo utilizador ou UDT, é outra programação para funcionalidade do U-SQL. U-SQL UDT funciona como um regular c# definido pelo utilizador tipo. C# é uma linguagem com tipo seguro que permita a utilização de Olá dos tipos de incorporadas e personalizadas definidas pelo utilizador.

U-SQL implicitamente não é possível serializar ou anular a serialização UDTs arbitrários quando Olá UDT é transferida entre vértices em conjuntos de linhas. Isto significa que o utilizador Olá tem tooprovide um formatador explícita utilizando Olá IFormatter interface. Isto fornece o U-SQL com Olá serializar e anular a serialização métodos para Olá UDT.

> [!NOTE]
> U-SQL extractors incorporadas e outputters atualmente não é possível serializar ou anular a serialização UDT tooor de dados de ficheiros, mesmo com Olá IFormatter conjunto. Assim, quando estiver a escrever o ficheiro de tooa de dados UDT com Olá declaração de saída ou lê-lo com um extrator, tiver toopass-o como uma matriz de cadeia ou bytes. Em seguida, chame serialização Olá e anulação da serialização da código (ou seja, método ToString () do Olá UDT) explicitamente. Definido pelo utilizador extractors e outputters, no Olá outro entregar, podem ler e escrever UDTs.

Se vamos tentar toouse UDT EXTRATOR ou OUTPUTTER (fora SELECIONE anterior), conforme mostrado aqui:

```
@rs1 =
    SELECT 
        MyNameSpace.Myfunction_Returning_UDT(filed1) AS myfield
    FROM @rs0;

OUTPUT @rs1 
    too@output_file 
    USING Outputters.Text();
```

Recebemos Olá seguinte erro:

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

toowork com UDT no outputter, podemos ter tooserialize-toostring com Olá método ToString () ou criar um outputter personalizado.

UDTs atualmente não é possível utilizar GROUP BY. Se for utilizado UDT no GROUP BY, é emitida Olá seguinte erro:

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

toodefine um UDT, temos para:

* Adicione Olá seguintes espaços de nomes:

```
using Microsoft.Analytics.Interfaces
using System.IO;
```

* Adicionar `Microsoft.Analytics.Interfaces`, que é necessário para interfaces UDT Olá. Além disso, `System.IO` poderá estar a interface de IFormatter de Olá toodefine necessários.

* Defina um tipo definido pelo utilizado com o atributo SqlUserDefinedType.

**SqlUserDefinedType** é utilizado toomark uma definição de tipo numa assemblagem como um tipo definido pelo utilizador (UDT) em U-SQL. Propriedades de Olá no atributo Olá refletem as características físicas da Olá de Olá UDT. Esta classe não pode ser herdada.

SqlUserDefinedType é um atributo necessário para a definição de UDT.

Construtor de classe de Olá Olá:  

* SqlUserDefinedTypeAttribute (formatador de tipo)

* Escreva o formatador: necessário parâmetro toodefine um formatador UDT – especificamente, o tipo de Olá de Olá `IFormatter` interface tem de ser transmitida aqui.

```
[SqlUserDefinedType(typeof(MyTypeFormatter))]
public class MyType
{ … }
```

* UDT típico também requer a definição de interface de IFormatter Olá, conforme mostrado no seguinte exemplo de Olá:

```
public class MyTypeFormatter : IFormatter<MyType>
{
    public void Serialize(MyType instance, IColumnWriter writer, ISerializationContext context)
    { … }

    public MyType Deserialize(IColumnReader reader, ISerializationContext context)
    { … }
}
```

Olá `IFormatter` interface serializa e anular serializa um gráfico de objeto com o tipo de raiz de Olá de \<typeparamref name = "T" >.

\<typeparam name = "T" > olá o tipo de raiz para tooserialize de gráfico de objeto Olá e anular a serialização.

* **Anular a serialização**: anular serializa dados Olá no fluxo de Olá fornecida e reconstitutes gráfico Olá de objetos.

* **Serializar**: Serializa um objeto ou o gráfico de objetos, com Olá fornecido fluxo toohello fornecido de raiz.

`MyType`instância: instância do tipo de Olá.  
`IColumnWriter`escritor / `IColumnReader` leitor: Olá subjacente fluxo da coluna.  
`ISerializationContext`contexto: enumeração que define um conjunto de sinalizadores que especifica o contexto de origem ou destino de Olá para fluxo Olá durante a serialização.

* **Intermédio**: Especifica nesse contexto Olá de origem ou de destino não é um arquivo persistente.

* **Persistência**: Especifica nesse contexto Olá de origem ou de destino é um arquivo persistente.

Como um regular c# tipo, uma definição de U-SQL UDT pode incluir substituições para operadores como + /Safari/Chrome = = /! =. Também pode incluir métodos estáticos. Por exemplo, se, vamos toouse este UDT como um parâmetro tooa função de agregação MIN U-SQL, temos toodefine < substituição de operador.

Anteriormente neste guia, iremos demonstrado um exemplo de identificação de período fiscal de data específica do Olá no formato de Olá Qn:Pn (Q1:P10). Olá seguinte exemplo mostra como toodefine personalizadas escreva para valores fiscais.

Segue-se um exemplo de uma secção code-behind com interface UDT e IFormatter personalizada:

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

Olá tipo definido inclui dois números: trimestre e mês. Os operadores = = /! = / > / < e método estático ToString () são definidas aqui.

Conforme mencionado anteriormente, UDT pode ser utilizado em expressões SELECT, mas não é possível utilizar OUTPUTTER/EXTRATOR sem serialização personalizada. -Tem toobe serializado como uma cadeia com ToString () ou utilizado com um OUTPUTTER/EXTRATOR personalizado.

Agora vamos discutir sobre a utilização de UDT. Numa secção por detrás do código, Alterámos o nosso seguinte do GetFiscalPeriod função toohello:

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

Como pode ver, devolve valor Olá do nosso tipo FiscalPeriod.

Aqui fornecemos um exemplo de como toouse-la ainda mais no script U-SQL de base. Este exemplo demonstra formas diferentes de invocação UDT do script U-SQL.

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

Eis um exemplo de uma secção completo por detrás do código:

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

## <a name="use-user-defined-aggregates-udagg"></a>Utilize agregações definidas pelo utilizador: UDAGG
Os agregados definidos pelo utilizador são quaisquer funções relacionadas com a agregação que são fornecidos não out-of-a-box com U-SQL. exemplo de Olá pode ser um agregado tooperform cálculos de bibliotecas personalizado, concatenations de cadeia, manipulações de cadeias e assim sucessivamente.

definição de classe base agregado definido pelo utilizador Olá é o seguinte:

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

**SqlUserDefinedAggregate** indica que o tipo de Olá deve ser registado como um agregado definido pelo utilizador. Esta classe não pode ser herdada.

Atributo de SqlUserDefinedType **opcional** para definição UDAGG.


Olá classe base permite-lhe toopass três parâmetros de abstrato: dois como parâmetros de entrada e um como resultado de Olá. tipos de dados de Olá são variáveis e devem ser definidos durante a herança de classe.

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

* **Init** invoca uma vez para cada grupo durante o cálculo. Fornece uma rotina de inicialização para cada grupo de agregação.  
* **Acumular** é executado uma vez para cada valor. Fornece uma funcionalidade principal de Olá para o algoritmo de agregação de Olá. Pode ser utilizado tooaggregate valores com vários tipos de dados que são definidos durante a herança de classe. Pode aceitar o dois parâmetros dos tipos de dados da variável.
* **Terminar** é executado uma vez por grupo de agregação no fim de Olá do processamento toooutput Olá resultado para cada grupo.

entrada correto toodeclare e tipos de dados de saída, utilize de forma a definição de classe de Olá:

```
public abstract class IAggregate<T1, T2, TResult> : IAggregate
```

* T1: Primeiro parâmetro tooaccumulate
* T2: Primeiro parâmetro tooaccumulate
* TResult: Tipo de retorno da terminação

Por exemplo:

```
public class GuidAggregate : IAggregate<string, int, int>
```

ou

```
public class GuidAggregate : IAggregate<string, string, string>
```

### <a name="use-udagg-in-u-sql"></a>Utilizar UDAGG em U-SQL
toouse UDAGG, primeiro defini-lo no code-behind ou de referência de programação para existente de Olá DLL, conforme debatido anteriormente.

Em seguida, utilize Olá sintaxe:

```
AGG<UDAGG_functionname>(param1,param2)
```

Eis um exemplo de UDAGG:

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

E o script de U-SQL base:

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

Neste cenário de caso de utilização, iremos concatenar classe GUIDs para utilizadores específicos Olá.

## <a name="use-user-defined-objects-udo"></a>Utilizar os objetos definidos pelo utilizador: UDO
U-SQL permite objetos de programação para personalizado toodefine, que são chamados objetos definidos pelo utilizador ou UDO.

Olá segue-se uma lista de UDO em U-SQL:

* Extractors definido pelo utilizador
    * Extrair linha por linha
    * Utilizado tooimplement extração de dados de ficheiros estruturados personalizados

* Outputters definido pelo utilizador
    * Saída linha por linha
    * Utilizar tipos de dados personalizados toooutput ou formatos de ficheiro personalizadas

* Processadores definidos pelo utilizador
    * Obter uma linha e produzir uma linha
    * Utilizado tooreduce Olá número de colunas ou produzir novas colunas com valores que são derivadas de um conjunto de coluna existente

* Appliers definido pelo utilizador
    * Obter uma linha e produzir 0 linhas de toon
    * Utilizado com OUTER/entre aplicar

* Combiners definido pelo utilizador
    * Combina os conjuntos de linhas – associações definidas pelo utilizador

* Reducers definido pelo utilizador
    * Tome n linhas e produzir uma linha
    * Utilizado tooreduce Olá diversas linhas

UDO é normalmente designado explicitamente no script de U-SQL como parte da Olá seguir instruções U-SQL:

* EXTRAIR
* SAÍDA
* PROCESSO
* COMBINAR
* REDUZIR

> [!NOTE]  
> UDO é limitadas tooconsume 0.5Gb memória.  Esta limitação de memória não é aplicável toolocal execuções.

## <a name="use-user-defined-extractors"></a>Utilizar extractors definido pelo utilizador
U-SQL permite-lhe dados externos tooimport utilizando uma instrução de EXTRAÇÃO. Uma instrução de EXTRAÇÃO pode utilizar extractors UDO incorporadas:  

* *Extractors.Text()*: fornece a extração dos ficheiros de texto delimitado de codificações diferentes.

* *Extractors.Csv()*: fornece a extração de valores separados por vírgulas (CSV) os ficheiros do codificações diferentes.

* *Extractors*: fornece a extração de valores separados por separador ficheiros (TSV) de codificações diferentes.

Pode ser útil toodevelop extrator de personalizado. Isto pode ser útil durante a importação de dados se quisermos toodo qualquer um dos Olá seguintes tarefas:

* Modificar os dados de entrada ao dividir colunas e modificar valores individuais. Olá funcionalidade do processador é melhor para a combinação de colunas.
* Analisar dados não estruturados, tais como páginas Web e os e-mails ou dados por não estruturados como XML/JSON.
* Analisar dados na codificação não suportada.

toodefine um extrator definido pelo utilizador, ou UIR, precisamos toocreate um `IExtractor` interface. Extrator de toohello de parâmetros, todos os entrada, tais como delimitadores de linha/coluna e codificação, precisam de toobe definido no construtor de Olá da classe de Olá. Olá `IExtractor` interface deve conter também uma definição para Olá `IEnumerable<IRow>` substituir da seguinte forma:

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

Olá **SqlUserDefinedExtractor** atributo indica que o tipo de Olá deve ser registado como um extrator definido pelo utilizador. Esta classe não pode ser herdada.

SqlUserDefinedExtractor é um atributo opcional para a definição de UIR. Utilizá-la toodefine AtomicFileProcessing propriedade para o objeto de UIR Olá.

* bool AtomicFileProcessing   

* **Verdadeiro** = indica que este extrator requer atómicos os ficheiros de entrada (JSON, XML,...)
* **FALSO** = indica que este extrator pode lidar com ficheiros divididos / distribuídos (CSV, SEQ,...)

Olá principal UIR programação para objetos são **entrada** e **saída**. objeto de entrada Olá é utilizado tooenumerate os dados de entrada como `IUnstructuredReader`. o objeto de resultado de Olá é utilizado tooset dados de saída como resultado da atividade de extrator Olá.

dados de entrada Olá são acedidos através do `System.IO.Stream` e `System.IO.StreamReader`.

Para a enumeração de colunas de entrada, vamos primeiro dividir o fluxo de entrada Olá utilizando um delimitador de linha.

```
foreach (Stream current in input.Split(my_row_delimiter))
{
…
}
```

Em seguida, divida mais linhas de entrada em partes de coluna.

```
foreach (Stream current in input.Split(my_row_delimiter))
{
…
    string[] parts = line.Split(my_column_delimiter);
    foreach (string part in parts)
    { … }
}
```

dados de saída tooset, utilizamos Olá `output.Set` método.

É importante toounderstand Olá extrator personalizado apenas produz colunas e valores que estão definidos com a saída de Olá. Definir a chamada de método.

```
output.Set<string>(count, part);
```

saída de extrator real Olá é acionada ao chamar `yield return output.AsReadOnly();`.

Segue-se Olá extrator exemplo:

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

Neste cenário de caso de utilização, extrator Olá gera de novo Olá GUID para a coluna "guid" e converte valores de Olá do cenário de tooupper de coluna "utilizador". Extractors personalizados podem produzir resultados mais complicados pela análise de dados de entrada e manipulá-lo.

Segue-se base script U-SQL que utiliza um extrator personalizado:

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

## <a name="use-user-defined-outputters"></a>Utilizar outputters definido pelo utilizador
Definido pelo utilizador outputter é outra UDO U-SQL que lhe permite uma funcionalidade U-SQL tooextend incorporada. Extrator de toohello semelhante, existem várias outputters incorporadas.

* *Outputters.Text()*: escreve dados toodelimited ficheiros de texto de codificações diferentes.
* *Outputters*: escreve o valor de valores separados por toocomma dados ficheiros (CSV) de codificações de diferentes.
* *Outputters.Tsv()*: escreve o valor de valores separados por tootab dados ficheiros de (TSV) de codificações diferentes.

Outputter personalizada permite-lhe toowrite dados num formato personalizado definido. Isto pode ser útil para Olá seguintes tarefas:

* Escrever ficheiros de dados estruturados de toosemi ou não estruturados.
* Escrita de dados não suportado codificações.
* A modificação de dados de saída ou adicionar atributos personalizados.

toodefine definido pelo utilizador outputter, precisamos toocreate Olá `IOutputter` interface.

Segue-se Olá base `IOutputter` implementação de classe:

```
public abstract class IOutputter : IUserDefinedOperator
{
    protected IOutputter();

    public virtual void Close();
    public abstract void Output(IRow input, IUnstructuredWriter output);
}
```

Todos os entrada parâmetros toohello outputter, tais como delimitadores de linha/coluna, codificação e assim sucessivamente, precisam de toobe definido no construtor de Olá da classe de Olá. Olá `IOutputter` interface deve conter também uma definição para `void Output` substituir. atributo de Olá `[SqlUserDefinedOutputter(AtomicFileProcessing = true)` , opcionalmente, pode ser definido para o processamento do ficheiro atomic. Para obter mais informações, consulte os detalhes de Olá.

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

* `Output`é chamado para cada linha de entrada. Devolve Olá `IUnstructuredWriter output` conjunto de linhas.
* é utilizado Olá classe construtor outputter toopass parâmetros toohello definido pelo utilizador.
* `Close`é utilizado toooptionally substituição de estado dispendiosas toorelease ou para determinar quando a última linha de Olá foi escrita.

**SqlUserDefinedOutputter** atributo indica que o tipo de Olá deve ser registado como um outputter definido pelo utilizador. Esta classe não pode ser herdada.

SqlUserDefinedOutputter é um atributo opcional para uma definição de outputter definido pelo utilizador. Utilizou o propriedade do toodefine Olá AtomicFileProcessing.

* bool AtomicFileProcessing   

* **Verdadeiro** = indica que este outputter requer ficheiros de saída atómico (JSON, XML,...)
* **FALSO** = indica que este outputter pode lidar com ficheiros divididos / distribuídos (CSV, SEQ,...)

objetos de programação para principais Olá são **linha** e **saída**. Olá **linha** objeto é utilizado tooenumerate dados de saída como `IRow` interface. **Saída** é o ficheiro de destino de toohello de dados de saída de tooset utilizados.

Olá dados de saída são acedidos através do Olá `IRow` interface. Dados de saída são transmitidos uma linha de cada vez.

valores individuais Olá são enumerados ao chamar o método Get Olá interface IRow de Olá:

```
row.Get<string>("column_name")
```

É possível determinar os nomes das colunas individuais ao chamar `row.Schema`:

```
ISchema schema = row.Schema;
var col = schema[i];
string val = row.Get<string>(col.Name)
```

Esta abordagem permite-lhe toobuild um outputter flexível para qualquer esquema metadata.

Olá dados de saída são escritos toofile utilizando `System.IO.StreamWriter`. parâmetro de fluxo de Olá está definido demasiado`output.BaseStrea` como parte da `IUnstructuredWriter output`.

Tenha em atenção que é importante tooflush Olá dados da memória intermédia toohello ficheiro após cada iteração de linha. Além disso, Olá `StreamWriter` objeto tem de ser utilizado com Olá Disposable atributo ativada (predefinição) e com Olá **utilizando** palavra-chave:

```
using (StreamWriter streamWriter = new StreamWriter(output.BaseStream, this._encoding))
{
…
}
```

Caso contrário, chame o método Flush() explicitamente após cada iteração. Vamos mostrar isto em Olá seguinte exemplo.

### <a name="set-headers-and-footers-for-user-defined-outputter"></a>Definir cabeçalhos e rodapés de página para outputter definido pelo utilizador
tooset cabeçalho, utilize o fluxo de execução única iteração.

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

Olá código Olá primeiro `if (isHeaderRow)` bloco é executado apenas uma vez.

Para o rodapé Olá, utilize Olá referência toohello instância `System.IO.Stream` objeto (`output.BaseStream`). Escrever rodapé Olá em Olá método Close() Olá `IOutputter` interface.  (Para obter mais informações, consulte o seguinte exemplo de Olá.)

Segue-se um exemplo de um outputter definido pelo utilizador:

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

E o script U-SQL de base:

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

Este é um outputter HTML, que cria um ficheiro HTML com a dados da tabela.

### <a name="call-outputter-from-u-sql-base-script"></a>Chamada outputter do script U-SQL de base
toocall um outputter personalizado do script de U-SQL base Olá, nova instância de Olá do objeto de outputter Olá tem toobe criado.

```sql
OUTPUT @rs0 too@output_file USING new USQL_Programmability.HTMLOutputter(isHeader: true);
```

tooavoid criar uma instância do Olá objeto no base script, podemos criar um dispositivo de moldagem de função, conforme mostrado no nosso exemplo anterior:

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

Neste caso, chamada original Olá aspeto Olá seguinte:

```
OUTPUT @rs0 
too@output_file 
USING USQL_Programmability.Factory.HTMLOutputter(isHeader: true);
```

## <a name="use-user-defined-processors"></a>Utilizar processadores definidos pelo utilizador
Processador definido pelo utilizador ou UDP, é um tipo de UDO U-SQL que lhe permite linhas de entrada de Olá tooprocess aplicando as funcionalidades de programação para. UDP permite-lhe toocombine colunas, modificar os valores e adicionar novas colunas, se necessário. Basicamente, ajuda a tooprocess elementos de dados de tooproduce necessário um conjunto de linhas.

toodefine um UDP, precisamos toocreate um `IProcessor` interface com Olá `SqlUserDefinedProcessor` atributo, o que é opcional para UDP.

Esta interface deve conter a definição de Olá para Olá `IRow` conjunto de linhas de interface substituir, conforme mostrado no seguinte exemplo de Olá:

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

**SqlUserDefinedProcessor** indica que o tipo de Olá deve ser registado como um processador definido pelo utilizador. Esta classe não pode ser herdada.

Olá SqlUserDefinedProcessor atributo **opcional** para a definição do UDP.

objetos de programação para principais Olá são **entrada** e **saída**. objeto de entrada Olá é utilizado tooenumerate colunas de entrada e saída e tooset dados de saída como resultado da atividade de processador de Olá.

Para a enumeração de colunas de entrada, utilizamos Olá `input.Get` método.

```
string column_name = input.Get<string>("column_name");
```

Olá parâmetro `input.Get` método é uma coluna que é transmitida como parte da Olá `PRODUCE` cláusula de Olá `PROCESS` declaração do Estado de script base Olá U-SQL. Precisamos toouse do tipo de dados correto de Olá aqui.

Para a saída, utilize Olá `output.Set` método.

É importante toonote esse produtor personalizado apenas é produz colunas e valores que estão definidos com Olá `output.Set` chamada de método.

```
output.Set<string>("mycolumn", mycolumn);
```

saída de processador real Olá é acionada ao chamar `return output.AsReadOnly();`.

Segue-se um exemplo de processador:

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

Neste cenário de caso de utilização, o processador de Olá está a gerar uma nova coluna chamada "full_description" combinando Olá as colunas existentes – neste caso, "utilizador" em maiúsculas e "des". Também gera de novo um GUID e devolve os valores de Olá originais e novo GUID.

Como pode ver do exemplo anterior Olá, pode chamar métodos c# durante `output.Set` chamada de método.

Segue-se um exemplo de script U-SQL base que utiliza um processador personalizado:

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

## <a name="use-user-defined-appliers"></a>Utilizar appliers definido pelo utilizador
Um applier do U-SQL definidos pelo utilizador permite-lhe função tooinvoke um personalizado c# para cada linha que é devolvida pela expressão de tabela externa Olá de uma consulta. Olá à direita de entrada é avaliada para cada linha da entrada à esquerda Olá e linhas de Olá que são produzidas são combinadas para o resultado final Olá. lista de Olá de colunas que são produzidos pela operadora de rede do Olá aplicar são a combinação de Olá do conjunto de Olá de colunas no lado esquerdo de Olá e Olá de entrada à direita.

Applier definido pelo utilizador está a ser invocado como parte da Olá USQL SELECIONE expressão.

Olá chamada típico toohello definido pelo utilizador applier parece Olá seguinte:

```
SELECT …
FROM …
CROSS APPLYis used toopass parameters
new MyScript.MyApplier(param1, param2) AS alias(output_param1 string, …);
```

Para obter mais informações sobre como utilizar appliers numa expressão SELECT, consulte [U-SQL SELECIONE selecionar de entre aplicar e OUTER APPLY](https://msdn.microsoft.com/library/azure/mt621307.aspx).

Olá definido pelo utilizador applier base definição de classe é o seguinte:

```
public abstract class IApplier : IUserDefinedOperator
{
protected IApplier();

public abstract IEnumerable<IRow> Apply(IRow input, IUpdatableRow output);
}
```

toodefine um applier definido pelo utilizador, precisamos toocreate Olá `IApplier` interface com Olá [`SqlUserDefinedApplier`] atributo, o que é opcional para uma definição applier definido pelo utilizador.

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

* Aplicar é chamado para cada linha da tabela externa Olá. Devolve Olá `IUpdatableRow` de saída do conjunto de linhas.
* a classe de construtor Olá é applier toopass utilizados parâmetros toohello definido pelo utilizador.

**SqlUserDefinedApplier** indica que o tipo de Olá deve ser registado como um applier definido pelo utilizador. Esta classe não pode ser herdada.

**SqlUserDefinedApplier** é **opcional** para uma definição applier definido pelo utilizador.


objetos de programação para principais Olá são os seguintes:

```
public override IEnumerable<IRow> Apply(IRow input, IUpdatableRow output)
```

Conjuntos de linhas de entrada são transmitidos como `IRow` entrada. Olá saída linhas são geradas como `IUpdatableRow` interface de saída.

Os nomes das colunas individual podem ser determinadas ao chamar Olá `IRow` método de esquema.

```
ISchema schema = row.Schema;
var col = schema[i];
string val = row.Get<string>(col.Name)
```

os valores de dados real de Olá tooget da entrada de Olá `IRow`, utilizamos o método Get() Olá `IRow` interface.

```
mycolumn = row.Get<int>("mycolumn")
```

Ou, utilizamos o nome de coluna de esquema Olá:

```
row.Get<int>(row.Schema[0].Name)
```

Olá valores de saída tem de ser definidos com `IUpdatableRow` saída:

```
output.Set<int>("mycolumn", mycolumn)
```

É importante toounderstand que appliers personalizados saída apenas colunas e valores que estão definidos com `output.Set` chamada de método.

saída real Olá é acionada ao chamar `yield return output.AsReadOnly();`.

Olá definido pelo utilizador applier os parâmetros podem ser passados toohello construtor. Applier pode devolver um número de colunas que necessitam de toobe definido durante a chamada de applier Olá no Script de U-SQL base variável.

```
new USQL_Programmability.ParserApplier ("all") AS properties(make string, model string, year string, type string, millage int);
```

Eis Olá definido pelo utilizador applier exemplo:

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

Segue-se script U-SQL base Olá para este applier definido pelo utilizador:

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

Neste cenário de cenários de utilização, atos applier definido pelo utilizador como um analisador de valor delimitado por vírgulas para carro Olá fleet propriedades. linhas de ficheiro de entrada Olá aspeto Olá seguinte:

```
103 Z1AB2CD123XY45889   Ford,Explorer,2005,SUV,152345
303 Y0AB2CD34XY458890   Shevrolet,Cruise,2010,4Dr,32455
210 X5AB2CD45XY458893   Nissan,Altima,2011,4Dr,74000
```

É um ficheiro do TSV típico de ' delimitada por separador ' para com uma coluna de propriedades que contém as propriedades de car como a marca e modelo. Essas propriedades tem de ser analisados toohello colunas da tabela. applier Olá fornecida também permite-lhe toogenerate dinâmica diversas propriedades no Olá resultam conjunto de linhas, com base no parâmetro Olá que é transmitido. Pode gerar todas as propriedades ou um conjunto específico de propriedades apenas.

    …USQL_Programmability.ParserApplier ("all")
    …USQL_Programmability.ParserApplier ("make")
    …USQL_Programmability.ParserApplier ("make&model")

pode ser chamado applier definido pelo utilizador de Olá como uma nova instância do objeto applier:

```
CROSS APPLY new MyNameSpace.MyApplier (parameter: “value”) AS alias([columns types]…);
```

Ou com invocação Olá de um método de fábrica do dispositivo de moldagem:

```c#
    CROSS APPLY MyNameSpace.MyApplier (parameter: “value”) AS alias([columns types]…);
```

## <a name="use-user-defined-combiners"></a>Utilizar combiners definido pelo utilizador
Combinação definido pelo utilizador ou UDC, permite-lhe toocombine linhas da esquerda e direita conjuntos de linhas, com base na lógica personalizada. Combinação definido pelo utilizador é utilizada com a expressão de combinação.

Uma combinação está a ser invocada com a expressão de combinação Olá que fornece as informações sobre os dois conjuntos de linhas de entrada Olá necessárias Olá, Olá agrupamento de colunas, hello esperado esquema de resultado e informações adicionais.

toocall uma combinação num script U-SQL base, podemos utilizar Olá sintaxe:

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

Para obter mais informações, consulte [COMBINAR expressão (U-SQL)](https://msdn.microsoft.com/library/azure/mt621339.aspx).

toodefine uma combinação de definido pelo utilizador, precisamos toocreate Olá `ICombiner` interface com Olá [`SqlUserDefinedCombiner`] atributo, o que é opcional para uma definição de combinação definido pelo utilizador.

Base `ICombiner` definição de classe:

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

Olá implementação personalizada de um `ICombiner` interface deve conter a definição de Olá para um `IEnumerable<IRow>` combinar substituição.

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

Olá **SqlUserDefinedCombiner** atributo indica que o tipo de Olá deve ser registado como uma combinação de definido pelo utilizador. Esta classe não pode ser herdada.

**SqlUserDefinedCombiner** é propriedade de modo de combinação de Olá toodefine utilizados. É um atributo opcional para uma definição de combinação definido pelo utilizador.

Modo de CombinerMode

Enumeração de CombinerMode pode demorar Olá os seguintes valores:

* Completo (0), que cada linha de saída depende potencialmente todas as linhas de entrada de Olá da esquerda e à direita com Olá mesmo valor de chave.

* À esquerda (1), cada linha de saída depende de uma única linha de entrada da esquerda Olá (e, potencialmente, todas as linhas da Olá à direita com Olá mesmo valor da chave).

* À direita (2), cada linha de saída depende de uma única linha de entrada de Olá direito (e, potencialmente, todas as linhas da esquerda Olá com Olá mesmo valor da chave).

* Linha de cada linha de saída depende de uma única entrada interna (3) da esquerda e direita com Olá mesmo valor.

Exemplo: [`SqlUserDefinedCombiner(Mode=CombinerMode.Left)`]


objetos de programação para principais Olá são:

```c#
    public override IEnumerable<IRow> Combine(IRowset left, IRowset right,
        IUpdatableRow output
```

Conjuntos de linhas de entrada são transmitidos como **esquerdo** e **direita** `IRowset` tipo de interface. Ambos os conjuntos de linhas tem de ser enumerados para processamento. Apenas pode enumerar cada interface de uma só vez, pelo que estamos a ter tooenumerate e cache-la, se necessário.

Para efeitos de colocação em cache, podemos criar uma lista\<T\> tipo de estrutura de memória como resultado de uma LINQ execução da consulta, especificamente lista <`IRow`>. tipo de dados anónimos Olá pode ser utilizado durante a enumeração bem.

Consulte [introdução tooLINQ consultas (c#)](https://msdn.microsoft.com/library/bb397906.aspx) para obter mais informações sobre consultas LINQ, e [IEnumerable\<T\> Interface](https://msdn.microsoft.com/library/9eekhta0(v=vs.110).aspx) para obter mais informações sobre IEnumerable\<T\> interface.

os valores de dados real de Olá tooget da entrada de Olá `IRowset`, utilizamos o método Get() Olá `IRow` interface.

```
mycolumn = row.Get<int>("mycolumn")
```

Os nomes das colunas individual podem ser determinadas ao chamar Olá `IRow` método de esquema.

```
ISchema schema = row.Schema;
var col = schema[i];
string val = row.Get<string>(col.Name)
```

Ou utilizando o nome de coluna de esquema Olá:

```
c# row.Get<int>(row.Schema[0].Name)
```

enumeração de geral Olá com LINQ aspeto Olá seguinte:

```
var myRowset =
            (from row in left.Rows
                          select new
                          {
                              Mycolumn = row.Get<int>("mycolumn"),
                          }).ToList();
```

Após a enumerar os dois conjuntos de linhas, vamos tooloop através de todas as linhas. Para cada linha no conjunto de linhas esquerdo Olá, vamos toofind todas as linhas que satisfaçam a condição de Olá do nosso combinação.

Olá valores de saída tem de ser definidos com `IUpdatableRow` saída.

```
output.Set<int>("mycolumn", mycolumn)
```

saída real Olá é acionada ao chamar demasiado`yield return output.AsReadOnly();`.

Segue-se um exemplo de combinação:

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

Neste cenário de caso de utilização, iremos está a criar um relatório de análise para revendedor Olá. o objetivo de Olá é toofind todos os produtos de custo mais de 20.000 $ e que propor através do Web site Olá mais rápida do que através de revendedor regular de Olá num determinado período de tempo.

Eis o script de U-SQL base Olá. Pode comparar lógica Olá entre uma associação regular e uma combinação:

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

Pode ser chamada uma combinação de definido pelo utilizador como uma nova instância do objeto applier Olá:

```
USING new MyNameSpace.MyCombiner();
```


Ou com invocação Olá de um método de fábrica do dispositivo de moldagem:

```
USING MyNameSpace.MyCombiner();
```

## <a name="use-user-defined-reducers"></a>Utilizar reducers definido pelo utilizador

U-SQL permite-lhe toowrite reducers de conjunto de linhas personalizadas em c# utilizando a estrutura de extensibilidade de operador definido pelo utilizador Olá e implementar uma interface IReducer.

Definido pelo utilizador reducer ou UDR, pode ser linhas desnecessários tooeliminate utilizado durante a extração de dados (importar). Também pode ser utilizado toomanipulate e avaliar linhas e colunas. Com base na lógica de programação para, também pode definir que linhas necessário toobe extraído.

uma classe UDR toodefine, precisamos toocreate um `IReducer` interface com opcional `SqlUserDefinedReducer` atributo.

Esta interface de classe deve conter uma definição para Olá `IEnumerable` substituir o conjunto de linhas de interface.

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

Olá **SqlUserDefinedReducer** atributo indica que o tipo de Olá deve ser registado como um reducer definido pelo utilizador. Esta classe não pode ser herdada.
**SqlUserDefinedReducer** é um atributo opcional para uma definição de reducer definido pelo utilizador. Utilizou o toodefine IsRecursive propriedade.

* bool IsRecursive    
* **Verdadeiro** = indica se esta Reducer é idempotent

objetos de programação para principais Olá são **entrada** e **saída**. objeto de entrada Olá é utilizado tooenumerate linhas de entrada. O resultado é utilizado tooset linhas de saída como resultado de reduzir a atividade.

Para a enumeração de linhas de entrada, utilizamos Olá `Row.Get` método.

```
foreach (IRow row in input.Rows)
{
    row.Get<string>("mycolumn");
}
```

Olá parâmetro Olá `Row.Get` método é uma coluna que é transmitida como parte da Olá `PRODUCE` classe de Olá `REDUCE` declaração do Estado de script base Olá U-SQL. Precisamos toouse Olá correto do tipo de dados aqui bem.

Para a saída, utilize Olá `output.Set` método.

É importante toounderstand que reducer personalizado únicos saídas valores que estão definidos com Olá `output.Set` chamada de método.

```
output.Set<string>("mycolumn", guid);
```

saída de reducer real Olá é acionada ao chamar `yield return output.AsReadOnly();`.

Segue-se um exemplo de reducer:

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

Neste cenário de caso de utilização, reducer Olá está a ignorar as linhas com um nome de utilizador vazio. Para cada linha no conjunto de linhas, lê de cada coluna necessária, em seguida, avalia o comprimento do nome de utilizador Olá Olá. Linha real Olá-produz apenas se o comprimento do valor de nome de utilizador é superior a 0.

Segue-se base script U-SQL que utiliza um reducer personalizado:

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
