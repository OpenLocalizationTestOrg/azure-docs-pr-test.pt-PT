---
title: "Exemplos de aaaQuery de padrões de utilização comuns no Stream Analytics | Microsoft Docs"
description: "Padrões de consulta comuns do Azure Stream Analytics"
keywords: Exemplos de consulta
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jenniehubbard
editor: cgronlun
ms.assetid: 6b9a7d00-fbcc-42f6-9cbb-8bbf0bbd3d0e
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/08/2017
ms.author: jenniehubbard
ms.openlocfilehash: c8f7a8ac661eaf0281f4140b02c42141b73040fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="query-examples-for-common-stream-analytics-usage-patterns"></a>Exemplos de padrões de utilização comuns do Stream Analytics de consulta
## <a name="introduction"></a>Introdução
As consultas no Azure Stream Analytics são expressas num idioma de consulta como o SQL Server. Estas consultas estão documentadas na Olá [referência de linguagem de consulta do Stream Analytics](https://msdn.microsoft.com/library/azure/dn834998.aspx) guia. Este artigo destaca soluções tooseveral padrões de consulta comuns, com base nos cenários no mundo real. Este é um trabalho em curso e continua toobe atualizada com novos padrões numa base contínua.

## <a name="query-example-convert-data-types"></a>Exemplo de consulta: converter os tipos de dados
**Descrição**: definir os tipos de Olá das propriedades no fluxo de entrada Olá.
Por exemplo, o peso de carro Olá futuras no fluxo de entrada Olá como cadeias e tem de toobe convertido demasiado**INT** tooperform **soma** -cópia de segurança.

**Entrada**:

| Certifique- | Hora | Peso |
| --- | --- | --- |
| Honda |2015-01-01T00:00:01.0000000Z |"1000" |
| Honda |2015-01-01T00:00:02.0000000Z |"2000" |

**Saída**:

| Certifique- | Peso |
| --- | --- |
| Honda |3000 |

**Solução**:

    SELECT
        Make,
        SUM(CAST(Weight AS BIGINT)) AS Weight
    FROM
        Input TIMESTAMP BY Time
    GROUP BY
        Make,
        TumblingWindow(second, 10)

**EXPLICAÇÃO**: Utilize um **CAST** instrução no Olá **ponderação** campo toospecify respetivo tipo de dados. Ver lista de Olá dos tipos de dados suportados no [tipos de dados (Azure Stream Analytics)](https://msdn.microsoft.com/library/azure/dn835065.aspx).

## <a name="query-example-use-likenot-like-toodo-pattern-matching"></a>Exemplo de consulta: Utilize como/não, como a correspondência de padrões toodo
**Descrição**: verificar se um valor de campo em eventos de Olá corresponde a um determinado padrão.
Por exemplo, verifique que o resultado de Olá devolve plates de licença que começam com um e terminar com 9.

**Entrada**:

| Certifique- | LicensePlate | Hora |
| --- | --- | --- |
| Honda |ABC 123 |2015-01-01T00:00:01.0000000Z |
| Toyota |AAA 999 |2015-01-01T00:00:02.0000000Z |
| Nissan |ABC 369 |2015-01-01T00:00:03.0000000Z |

**Saída**:

| Certifique- | LicensePlate | Hora |
| --- | --- | --- |
| Toyota |AAA 999 |2015-01-01T00:00:02.0000000Z |
| Nissan |ABC 369 |2015-01-01T00:00:03.0000000Z |

**Solução**:

    SELECT
        *
    FROM
        Input TIMESTAMP BY Time
    WHERE
        LicensePlate LIKE 'A%9'

**EXPLICAÇÃO**: Olá utilize **como** Olá toocheck de instrução **LicensePlate** campo valor. Deve começar com um um, em seguida, ter qualquer cadeia de zero ou mais carateres e, em seguida, terminar com um 9. 

## <a name="query-example-specify-logic-for-different-casesvalues-case-statements"></a>Exemplo de consulta: especificar lógica para casos/valores diferentes (instruções maiúsculas)
**Descrição**: forneça um cálculo diferente de um campo, com base num critério específico.
Por exemplo, indique uma descrição de cadeia para automóveis quantos de Olá, mesmo se passaram, com um caso especial para 1.

**Entrada**:

| Certifique- | Hora |
| --- | --- |
| Honda |2015-01-01T00:00:01.0000000Z |
| Toyota |2015-01-01T00:00:02.0000000Z |
| Toyota |2015-01-01T00:00:03.0000000Z |

**Saída**:

| CarsPassed | Hora |
| --- | --- | --- |
| 1 Honda |2015-01-01T00:00:10.0000000Z |
| 2 Toyotas |2015-01-01T00:00:10.0000000Z |

**Solução**:

    SELECT
        CASE
            WHEN COUNT(*) = 1 THEN CONCAT('1 ', Make)
            ELSE CONCAT(CAST(COUNT(*) AS NVARCHAR(MAX)), ' ', Make, 's')
        END AS CarsPassed,
        System.TimeStamp AS Time
    FROM
        Input TIMESTAMP BY Time
    GROUP BY
        Make,
        TumblingWindow(second, 10)

**EXPLICAÇÃO**: Olá **caso** cláusula nos permite tooprovide cálculo diferentes, com base em algumas critérios (no nosso caso, a contagem de Olá de automóveis Olá na janela de agregação Olá).

## <a name="query-example-send-data-toomultiple-outputs"></a>Exemplo de consulta: enviar dados toomultiple produz
**Descrição**: enviar dados toomultiple saída destinos de uma única tarefa.
Por exemplo, analisar os dados para um alerta baseadas em limiares e todo o armazenamento tooblob eventos de arquivo.

**Entrada**:

| Certifique- | Hora |
| --- | --- |
| Honda |2015-01-01T00:00:01.0000000Z |
| Honda |2015-01-01T00:00:02.0000000Z |
| Toyota |2015-01-01T00:00:01.0000000Z |
| Toyota |2015-01-01T00:00:02.0000000Z |
| Toyota |2015-01-01T00:00:03.0000000Z |

**Output1**:

| Certifique- | Hora |
| --- | --- |
| Honda |2015-01-01T00:00:01.0000000Z |
| Honda |2015-01-01T00:00:02.0000000Z |
| Toyota |2015-01-01T00:00:01.0000000Z |
| Toyota |2015-01-01T00:00:02.0000000Z |
| Toyota |2015-01-01T00:00:03.0000000Z |

**Output2**:

| Certifique- | Hora | Contagem |
| --- | --- | --- |
| Toyota |2015-01-01T00:00:10.0000000Z |3 |

**Solução**:

    SELECT
        *
    INTO
        ArchiveOutput
    FROM
        Input TIMESTAMP BY Time

    SELECT
        Make,
        System.TimeStamp AS Time,
        COUNT(*) AS [Count]
    INTO
        AlertOutput
    FROM
        Input TIMESTAMP BY Time
    GROUP BY
        Make,
        TumblingWindow(second, 10)
    HAVING
        [Count] >= 3

**EXPLICAÇÃO**: Olá **INTO** cláusula indica Stream Analytics que Olá produz toowrite Olá dados toofrom esta instrução.
consulta primeiro Olá é um pass-through de dados de Olá recebemos tooan saída que são denominados **ArchiveOutput**.
consulta segundo Olá efetua algumas agregação simple e filtragem e envia resultados Olá tooa sistema de alerta a jusante.

Tenha em atenção que também pode reutilizar resultados Olá de expressões de tabela comuns (ctes recursivos) do Olá (tais como **WITH** instruções) em várias instruções de saída. Esta opção tem Olá benefício adicional de abrir a origem de entrada menos leitores toohello.
Por exemplo: 

    WITH AllRedCars AS (
        SELECT
            *
        FROM
            Input TIMESTAMP BY Time
        WHERE
            Color = 'red'
    )
    SELECT * INTO HondaOutput FROM AllRedCars WHERE Make = 'Honda'
    SELECT * INTO ToyotaOutput FROM AllRedCars WHERE Make = 'Toyota'

## <a name="query-example-count-unique-values"></a>Exemplo de consulta: contagem de valores exclusivos
**Descrição**: Olá número exclusivo de valores de campos que são apresentados no fluxo de Olá dentro de uma janela de tempo da contagem.
Por exemplo, quantas exclusivo faz com que o de automóveis passadas booth de utilização de Olá numa janela segundo 2?

**Entrada**:

| Certifique- | Hora |
| --- | --- |
| Honda |2015-01-01T00:00:01.0000000Z |
| Honda |2015-01-01T00:00:02.0000000Z |
| Toyota |2015-01-01T00:00:01.0000000Z |
| Toyota |2015-01-01T00:00:02.0000000Z |
| Toyota |2015-01-01T00:00:03.0000000Z |

**Saída:**

| Contagem | Hora |
| --- | --- |
| 2 |2015-01-01T00:00:02.000Z |
| 1 |2015-01-01T00:00:04.000Z |

**Solução:**

````
SELECT
     COUNT(DISTINCT Make) AS CountMake,
     System.TIMESTAMP AS TIME
FROM Input TIMESTAMP BY TIME
GROUP BY 
     TumblingWindow(second, 2)
````


**Explicação:**
**CONTAGEM (tornar distintos)** devolve Olá número de valores distintos numa Olá **tornar** coluna dentro de uma janela de tempo.

## <a name="query-example-determine-if-a-value-has-changed"></a>Exemplo de consulta: determinar se um valor foi alterada
**Descrição**: observar um toodetermine valor anterior, se for diferente do valor atual de Olá.
Por exemplo, é carro anterior Olá no Olá de viagem de utilização de Olá que mesmo tornar mais carro atual Olá?

**Entrada**:

| Certifique- | Hora |
| --- | --- |
| Honda |2015-01-01T00:00:01.0000000Z |
| Toyota |2015-01-01T00:00:02.0000000Z |

**Saída**:

| Certifique- | Hora |
| --- | --- |
| Toyota |2015-01-01T00:00:02.0000000Z |

**Solução**:

    SELECT
        Make,
        Time
    FROM
        Input TIMESTAMP BY Time
    WHERE
        LAG(Make, 1) OVER (LIMIT DURATION(minute, 1)) <> Make

**EXPLICAÇÃO**: Utilize **desfasamento** toopeek para Olá fluxo um evento volta de entrada e obter Olá **tornar** valor. Em seguida, compare toohello **tornar** valor num evento Olá de saída e de evento atual de Olá se forem diferentes.

## <a name="query-example-find-hello-first-event-in-a-window"></a>Exemplo de consulta: o primeiro evento a localizar Olá numa janela
**Descrição**: localizar carro primeiro de Olá em cada intervalo de 10 minutos.

**Entrada**:

| LicensePlate | Certifique- | Hora |
| --- | --- | --- |
| DXE 5291 |Honda |2015-07-27T00:00:05.0000000Z |
| YZK 5704 |Ford |2015-07-27T00:02:17.0000000Z |
| RMV 8282 |Honda |2015-07-27T00:05:01.0000000Z |
| YHN 6970 |Toyota |2015-07-27T00:06:00.0000000Z |
| VFE 1616 |Toyota |2015-07-27T00:09:31.0000000Z |
| QYF 9358 |Honda |2015-07-27T00:12:02.0000000Z |
| MDR 6128 |BMW |2015-07-27T00:13:45.0000000Z |

**Saída**:

| LicensePlate | Certifique- | Hora |
| --- | --- | --- |
| DXE 5291 |Honda |2015-07-27T00:00:05.0000000Z |
| QYF 9358 |Honda |2015-07-27T00:12:02.0000000Z |

**Solução**:

    SELECT 
        LicensePlate,
        Make,
        Time
    FROM 
        Input TIMESTAMP BY Time
    WHERE 
        IsFirst(minute, 10) = 1

Agora vamos alterar Olá problema e localizar Olá primeiro carro de uma determinada efetuar em cada intervalo de 10 minutos.

| LicensePlate | Certifique- | Hora |
| --- | --- | --- |
| DXE 5291 |Honda |2015-07-27T00:00:05.0000000Z |
| YZK 5704 |Ford |2015-07-27T00:02:17.0000000Z |
| YHN 6970 |Toyota |2015-07-27T00:06:00.0000000Z |
| QYF 9358 |Honda |2015-07-27T00:12:02.0000000Z |
| MDR 6128 |BMW |2015-07-27T00:13:45.0000000Z |

**Solução**:

    SELECT 
        LicensePlate,
        Make,
        Time
    FROM 
        Input TIMESTAMP BY Time
    WHERE 
        IsFirst(minute, 10) OVER (PARTITION BY Make) = 1

## <a name="query-example-find-hello-last-event-in-a-window"></a>Exemplo de consulta: último evento de localizar Olá numa janela
**Descrição**: carro de último Olá localizar em cada intervalo de 10 minutos.

**Entrada**:

| LicensePlate | Certifique- | Hora |
| --- | --- | --- |
| DXE 5291 |Honda |2015-07-27T00:00:05.0000000Z |
| YZK 5704 |Ford |2015-07-27T00:02:17.0000000Z |
| RMV 8282 |Honda |2015-07-27T00:05:01.0000000Z |
| YHN 6970 |Toyota |2015-07-27T00:06:00.0000000Z |
| VFE 1616 |Toyota |2015-07-27T00:09:31.0000000Z |
| QYF 9358 |Honda |2015-07-27T00:12:02.0000000Z |
| MDR 6128 |BMW |2015-07-27T00:13:45.0000000Z |

**Saída**:

| LicensePlate | Certifique- | Hora |
| --- | --- | --- |
| VFE 1616 |Toyota |2015-07-27T00:09:31.0000000Z |
| MDR 6128 |BMW |2015-07-27T00:13:45.0000000Z |

**Solução**:

    WITH LastInWindow AS
    (
        SELECT 
            MAX(Time) AS LastEventTime
        FROM 
            Input TIMESTAMP BY Time
        GROUP BY 
            TumblingWindow(minute, 10)
    )
    SELECT 
        Input.LicensePlate,
        Input.Make,
        Input.Time
    FROM
        Input TIMESTAMP BY Time 
        INNER JOIN LastInWindow
        ON DATEDIFF(minute, Input, LastInWindow) BETWEEN 0 AND 10
        AND Input.Time = LastInWindow.LastEventTime

**EXPLICAÇÃO**: Existem dois passos numa consulta Olá. Olá primeiro encontra um Olá mais recente carimbo de hora do windows 10 minutos. associações de passo segundo Olá Olá resultados de consulta de primeiro Olá com Olá original fluxo toofind Olá eventos que correspondem ao hello último tempo carimbos de cada janela. 

## <a name="query-example-detect-hello-absence-of-events"></a>Exemplo de consulta: detetar ausência de Olá de eventos
**Descrição**: verificar se uma sequência não tem um valor que corresponde a um determinado critério.
Por exemplo, 2 carros consecutivos de Olá, que mesmo se introduziu viagem de utilização de Olá dentro Olá últimos 90 segundos?

**Entrada**:

| Certifique- | LicensePlate | Hora |
| --- | --- | --- |
| Honda |ABC 123 |2015-01-01T00:00:01.0000000Z |
| Honda |AAA 999 |2015-01-01T00:00:02.0000000Z |
| Toyota |DEF 987 |2015-01-01T00:00:03.0000000Z |
| Honda |GHI 345 |2015-01-01T00:00:04.0000000Z |

**Saída**:

| Certifique- | Hora | CurrentCarLicensePlate | FirstCarLicensePlate | FirstCarTime |
| --- | --- | --- | --- | --- |
| Honda |2015-01-01T00:00:02.0000000Z |AAA 999 |ABC 123 |2015-01-01T00:00:01.0000000Z |

**Solução**:

    SELECT
        Make,
        Time,
        LicensePlate AS CurrentCarLicensePlate,
        LAG(LicensePlate, 1) OVER (LIMIT DURATION(second, 90)) AS FirstCarLicensePlate,
        LAG(Time, 1) OVER (LIMIT DURATION(second, 90)) AS FirstCarTime
    FROM
        Input TIMESTAMP BY Time
    WHERE
        LAG(Make, 1) OVER (LIMIT DURATION(second, 90)) = Make

**EXPLICAÇÃO**: Utilize **desfasamento** toopeek para Olá fluxo um evento volta de entrada e obter Olá **tornar** valor. Compare-toohello **tornar** valor Olá atual de eventos e, em seguida, eventos de Olá de saída se estes estão Olá mesmo. Também pode utilizar **desfasamento** tooget dados sobre carro anterior Olá.

## <a name="query-example-detect-hello-duration-between-events"></a>Exemplo de consulta: detetar duração Olá entre eventos
**Descrição**: localizar duração Olá de um evento específico. Por exemplo, tendo em conta um clickstream da web, determine o tempo de Olá gasto numa funcionalidade.

**Entrada**:  

| Utilizador | Funcionalidade | Evento | Hora |
| --- | --- | --- | --- |
| user@location.com |RightMenu |Iniciar |2015-01-01T00:00:01.0000000Z |
| user@location.com |RightMenu |Fim |2015-01-01T00:00:08.0000000Z |

**Saída**:  

| Utilizador | Funcionalidade | Duração |
| --- | --- | --- |
| user@location.com |RightMenu |7 |

**Solução**:

````
    SELECT
        [user], feature, DATEDIFF(second, LAST(Time) OVER (PARTITION BY [user], feature LIMIT DURATION(hour, 1) WHEN Event = 'start'), Time) as duration
    FROM input TIMESTAMP BY Time
    WHERE
        Event = 'end'
````

**EXPLICAÇÃO**: Olá utilize **último** funcionar tooretrieve Olá pela última vez **tempo** valor quando o tipo de evento Olá foi **iniciar**. Olá **último** funcionar utiliza **PARTITION BY [user]** tooindicate Olá resultado é calculada por utilizador exclusivo. consulta de Olá tem um limiar máximo de 1 hora de diferença de tempo de Olá entre **iniciar** e **parar** eventos, mas é configurável conforme necessário **(limite DURATION(hour, 1)**.

## <a name="query-example-detect-hello-duration-of-a-condition"></a>Exemplo de consulta: detetar duração Olá de uma condição
**Descrição**: localizar fora quanto Ocorreu uma condição.
Por exemplo, suponha que um erro resultou em todos os carros ter uma ponderação incorreta (acima pounds 20.000). Queremos toocompute duração Olá erros Olá.

**Entrada**:

| Certifique- | Hora | Peso |
| --- | --- | --- |
| Honda |2015-01-01T00:00:01.0000000Z |2000 |
| Toyota |2015-01-01T00:00:02.0000000Z |25000 |
| Honda |2015-01-01T00:00:03.0000000Z |26000 |
| Toyota |2015-01-01T00:00:04.0000000Z |25000 |
| Honda |2015-01-01T00:00:05.0000000Z |26000 |
| Toyota |2015-01-01T00:00:06.0000000Z |25000 |
| Honda |2015-01-01T00:00:07.0000000Z |26000 |
| Toyota |2015-01-01T00:00:08.0000000Z |2000 |

**Saída**:

| StartFault | EndFault |
| --- | --- |
| 2015-01-01T00:00:02.000Z |2015-01-01T00:00:07.000Z |

**Solução**:

````
    WITH SelectPreviousEvent AS
    (
    SELECT
    *,
        LAG([time]) OVER (LIMIT DURATION(hour, 24)) as previousTime,
        LAG([weight]) OVER (LIMIT DURATION(hour, 24)) as previousWeight
    FROM input TIMESTAMP BY [time]
    )

    SELECT 
        LAG(time) OVER (LIMIT DURATION(hour, 24) WHEN previousWeight < 20000 ) [StartFault],
        previousTime [EndFault]
    FROM SelectPreviousEvent
    WHERE
        [weight] < 20000
        AND previousWeight > 20000
````

**EXPLICAÇÃO**: Utilize **desfasamento** tooview Olá o fluxo de entrada para 24 horas e procure instâncias onde **StartFault** e **StopFault** são abrangido pelo Olá < 20000 de importância.

## <a name="query-example-fill-missing-values"></a>Exemplo de consulta: preencher os valores em falta
**Descrição**: para o fluxo de Olá dos eventos que têm valores em falta, produzir um fluxo de eventos com intervalos regulares.
Por exemplo, gere um evento a cada cinco segundos, que comunica o ponto de dados de Olá visto mais recentemente.

**Entrada**:

| T | valor |
| --- | --- |
| "2014-01-01T06:01:00" |1 |
| "2014-01-01T06:01:05" |2 |
| "2014-01-01T06:01:10" |3 |
| "2014-01-01T06:01:15" |4 |
| "2014-01-01T06:01:30" |5 |
| "2014-01-01T06:01:35" |6 |

**Saída (primeiras 10 linhas)**:

| windowend | lastevent.t | lastevent.Value |
| --- | --- | --- |
| 2014-01-01T14:01:00.000Z |2014-01-01T14:01:00.000Z |1 |
| 2014-01-01T14:01:05.000Z |2014-01-01T14:01:05.000Z |2 |
| 2014-01-01T14:01:10.000Z |2014-01-01T14:01:10.000Z |3 |
| 2014-01-01T14:01:15.000Z |2014-01-01T14:01:15.000Z |4 |
| 2014-01-01T14:01:20.000Z |2014-01-01T14:01:15.000Z |4 |
| 2014-01-01T14:01:25.000Z |2014-01-01T14:01:15.000Z |4 |
| 2014-01-01T14:01:30.000Z |2014-01-01T14:01:30.000Z |5 |
| 2014-01-01T14:01:35.000Z |2014-01-01T14:01:35.000Z |6 |
| 2014-01-01T14:01:40.000Z |2014-01-01T14:01:35.000Z |6 |
| 2014-01-01T14:01:45.000Z |2014-01-01T14:01:35.000Z |6 |

**Solução**:

    SELECT
        System.Timestamp AS windowEnd,
        TopOne() OVER (ORDER BY t DESC) AS lastEvent
    FROM
        input TIMESTAMP BY t
    GROUP BY HOPPINGWINDOW(second, 300, 5)


**EXPLICAÇÃO**: esta consulta gera eventos a cada cinco segundos e saídas Olá último evento que foi recebido anteriormente. Olá [Hopping janela](https://msdn.microsoft.com/library/dn835041.aspx "Hopping janela – Azure Stream Analytics") duração determina até que ponto a consulta de back-Olá procura eventos mais recentes do toofind Olá (300 segundos neste exemplo).

## <a name="get-help"></a>Obter ajuda
Para obter mais assistência, experimente a nossa [fórum do Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).

## <a name="next-steps"></a>Passos seguintes
* [Introdução tooAzure Stream Analytics](stream-analytics-introduction.md)
* [Começar a utilizar o Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [Tarefas de escala do Azure Stream Analytics](stream-analytics-scale-jobs.md)
* [Referência do idioma de consulta do Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Referência de API do REST de gestão do Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn835031.aspx)

