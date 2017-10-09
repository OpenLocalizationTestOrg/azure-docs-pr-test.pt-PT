---
title: "Olá aaaUnderstand idioma de consulta do IoT Hub do Azure | Microsoft Docs"
description: "Guia para programadores - descrição do idioma de consulta de SQL Server como o IoT Hub Olá utilizado tooretrieve informações sobre dispositivos duplos e tarefas a partir do seu IoT hub."
services: iot-hub
documentationcenter: .net
author: fsautomata
manager: timlt
editor: 
ms.assetid: 851a9ed3-b69e-422e-8a5d-1d79f91ddf15
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/25/17
ms.author: elioda
ms.openlocfilehash: 01a7c8ffdf44c6c27b834739d02c8fef1dd3d3fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="reference---iot-hub-query-language-for-device-twins-jobs-and-message-routing"></a>Referência - idioma de consulta do IoT Hub para dispositivos duplos, tarefas e o encaminhamento de mensagens

IoT Hub fornece informações de tooretrieve um poderosa linguagem semelhante a SQL relativos à [dispositivos duplos] [ lnk-twins] e [tarefas][lnk-jobs]e [mensagem encaminhamento][lnk-devguide-messaging-routes]. Este artigo apresenta:

* Uma introdução toohello principais funcionalidades de Olá idioma de consulta do IoT Hub, e
* Olá detalhadas descrição de idioma de Olá.

## <a name="get-started-with-device-twin-queries"></a>Começar a utilizar consultas do dispositivo duplo
[Dispositivos duplos] [ lnk-twins] pode conter objetos JSON arbitrários, como as etiquetas e propriedades. IoT Hub permite-lhe tooquery dispositivos duplos como um único documento JSON que contém todas as informações do dispositivo duplo.
Partem do princípio de, por exemplo, que os dispositivos duplos do IoT hub tem Olá seguir a estrutura:

```json
{
    "deviceId": "myDeviceId",
    "etag": "AAAAAAAAAAc=",
    "tags": {
        "location": {
            "region": "US",
            "plant": "Redmond43"
        }
    },
    "properties": {
        "desired": {
            "telemetryConfig": {
                "configId": "db00ebf5-eeeb-42be-86a1-458cccb69e57",
                "sendFrequencyInSecs": 300
            },
            "$metadata": {
            ...
            },
            "$version": 4
        },
        "reported": {
            "connectivity": {
                "type": "cellular"
            },
            "telemetryConfig": {
                "configId": "db00ebf5-eeeb-42be-86a1-458cccb69e57",
                "sendFrequencyInSecs": 300,
                "status": "Success"
            },
            "$metadata": {
            ...
            },
            "$version": 7
        }
    }
}
```

IoT Hub expõe dispositivos duplos da Olá como uma coleção de documentos chamada **dispositivos**.
Por isso, Olá seguinte consulta obtém o conjunto completo de Olá de dispositivos duplos:

```sql
SELECT * FROM devices
```

> [!NOTE]
> [Os SDKs IoT do Azure] [ lnk-hub-sdks] suporta paginação dos resultados grande.

IoT Hub permite-lhe tooretrieve dispositivos duplos filtragem com condições arbitrários. Por exemplo,

```sql
SELECT * FROM devices
WHERE tags.location.region = 'US'
```

obtém Olá dispositivos duplos com Olá **location.region** etiquetas definido demasiado**E.U.A.**.
Operadores booleanos e comparações aritméticas suportadas, bem como, por exemplo

```sql
SELECT * FROM devices
WHERE tags.location.region = 'US'
    AND properties.reported.telemetryConfig.sendFrequencyInSecs >= 60
```

obtém todos os dispositivos duplos, localizados na Olá nos configurado toosend telemetria inferior, muitas vezes, a cada minuto. Para efeitos práticos, também é possível toouse constantes de matriz com Olá **IN** e **NIN** operadores (não nos). Por exemplo,

```sql
SELECT * FROM devices
WHERE properties.reported.connectivity IN ['wired', 'wifi']
```

obtém todos os dispositivos duplos, que comunicou Wi-Fi ou com fios conectividade. Este é frequentemente necessário tooidentify todos os dispositivos duplos, que contém uma propriedade específica. IoT Hub suporta função Olá `is_defined()` para esta finalidade. Por exemplo,

```SQL
SELECT * FROM devices
WHERE is_defined(properties.reported.connectivity)
```

obter todos os dispositivos duplos que definem Olá `connectivity` comunicadas propriedade. Consulte toohello [cláusula WHERE] [ lnk-query-where] secção para referência completa Olá Olá capacidades de filtragem.

Agrupamento e agregações também são suportadas. Por exemplo,

```sql
SELECT properties.reported.telemetryConfig.status AS status,
    COUNT() AS numberOfDevices
FROM devices
GROUP BY properties.reported.telemetryConfig.status
```

Devolve a contagem de Olá de dispositivos de Olá em cada Estado de configuração de telemetria.

```json
[
    {
        "numberOfDevices": 3,
        "status": "Success"
    },
    {
        "numberOfDevices": 2,
        "status": "Pending"
    },
    {
        "numberOfDevices": 1,
        "status": "Error"
    }
]
```

Olá anterior exemplo ilustra uma situação em que três dispositivos comunicados configuração com êxito, dois ainda a aplicar a configuração de Olá e um comunicou um erro.

### <a name="c-example"></a>Exemplo do c#
funcionalidade de consulta Olá é exposta pelo Olá [c# SDK do serviço] [ lnk-hub-sdks] no Olá **RegistryManager** classe.
Eis um exemplo de uma consulta simples:

```csharp
var query = registryManager.CreateQuery("SELECT * FROM devices", 100);
while (query.HasMoreResults)
{
    var page = await query.GetNextAsTwinAsync();
    foreach (var twin in page)
    {
        // do work on twin object
    }
}
```

Tenha em atenção como Olá **consulta** é criar instâncias do objecto com um tamanho de página (cópia de segurança too1000) e, em seguida, várias páginas podem ser obtidas pelos Olá chamar **GetNextAsTwinAsync** métodos várias vezes.
Tenha em atenção que objeto da consulta Olá expõe vários **seguinte\***, dependendo da opção de anulação da serialização de Olá exigido pela consulta Olá, por exemplo, o dispositivo duplo ou tarefa de objetos, ou simples toobe JSON utilizados quando usar projeções.

### <a name="nodejs-example"></a>Exemplo de node.js
funcionalidade de consulta Olá é exposta pelo Olá [o serviço de IoT do Azure SDK para Node.js] [ lnk-hub-sdks] no Olá **registo** objeto.
Eis um exemplo de uma consulta simples:

```nodejs
var query = registry.createQuery('SELECT * FROM devices', 100);
var onResults = function(err, results) {
    if (err) {
        console.error('Failed toofetch hello results: ' + err.message);
    } else {
        // Do something with hello results
        results.forEach(function(twin) {
            console.log(twin.deviceId);
        });

        if (query.hasMoreResults) {
            query.nextAsTwin(onResults);
        }
    }
};
query.nextAsTwin(onResults);
```

Tenha em atenção como Olá **consulta** é criar instâncias do objecto com um tamanho de página (cópia de segurança too1000) e, em seguida, várias páginas podem ser obtidas pelos Olá chamar **nextAsTwin** métodos várias vezes.
Tenha em atenção que objeto da consulta Olá expõe vários **seguinte\***, dependendo da opção de anulação da serialização de Olá exigido pela consulta Olá, por exemplo, o dispositivo duplo ou tarefa de objetos, ou simples toobe JSON utilizados quando usar projeções.

### <a name="limitations"></a>Limitações
> [!IMPORTANT]
> Os resultados da consulta podem ter alguns minutos de atraso com valores mais recentes do relativamente toohello dispositivos duplos. Se a consultar os dispositivos individuais duplos por id, é sempre preferível toouse Olá obter a API do dispositivo duplo, que sempre contém valores mais recentes Olá e tem os limites de limitação superior.

Atualmente, em que comparações são suportadas para a instância apenas entre tipos primitivos (não existem objetos), `... WHERE properties.desired.config = properties.reported.config` só é suportada se essas propriedades têm valores primitivos.

## <a name="get-started-with-jobs-queries"></a>Começar a utilizar consultas de tarefas
[As tarefas] [ lnk-jobs] fornecem uma forma tooexecute operações em conjuntos de dispositivos. Cada dispositivo duplo contém informações de Olá das tarefas de Olá do qual faz parte de uma coleção chamada **tarefas**.
Logicamente,

```json
{
    "deviceId": "myDeviceId",
    "etag": "AAAAAAAAAAc=",
    "tags": {
        ...
    },
    "properties": {
        ...
    },
    "jobs": [
        {
            "deviceId": "myDeviceId",
            "jobId": "myJobId",
            "jobType": "scheduleTwinUpdate",
            "status": "completed",
            "startTimeUtc": "2016-09-29T18:18:52.7418462",
            "endTimeUtc": "2016-09-29T18:20:52.7418462",
            "createdDateTimeUtc": "2016-09-29T18:18:56.7787107Z",
            "lastUpdatedDateTimeUtc": "2016-09-29T18:18:56.8894408Z",
            "outcome": {
                "deviceMethodResponse": null
            }
        },
        ...
    ]
}
```

Atualmente, esta coleção está consultável como **devices.jobs** no Olá idioma de consulta do IoT Hub.

> [!IMPORTANT]
> Atualmente, a propriedade de tarefas Olá nunca é devolvida ao consultar dispositivos duplos (ou seja, as consultas que contém 'a partir de dispositivos'). Só pode ser acedido diretamente com consultas através de `FROM devices.jobs`.
>
>

Por exemplo, tooget todas as tarefas (últimos e agendadas) que afetam um único dispositivo, pode utilizar Olá seguinte consulta:

```sql
SELECT * FROM devices.jobs
WHERE devices.jobs.deviceId = 'myDeviceId'
```

Tenha em atenção a como esta consulta fornece o estado de específicos do dispositivo Olá (e possivelmente resposta de método direto Olá) de cada tarefa devolvida.
Também é possível toofilter com condições booleanos arbitrários em todas as propriedades do objeto no Olá **devices.jobs** coleção.
Por exemplo, Olá seguinte consulta:

```sql
SELECT * FROM devices.jobs
WHERE devices.jobs.deviceId = 'myDeviceId'
    AND devices.jobs.jobType = 'scheduleTwinUpdate'
    AND devices.jobs.status = 'completed'
    AND devices.jobs.createdTimeUtc > '2016-09-01'
```

tarefas de atualização do obtém todos os concluída dispositivo duplo para dispositivo **myDeviceId** que foram criados depois de Setembro de 2016.

Também é possível tooretrieve resultados de por dispositivo Olá de uma única tarefa.

```sql
SELECT * FROM devices.jobs
WHERE devices.jobs.jobId = 'myJobId'
```

### <a name="limitations"></a>Limitações
Atualmente, a consulta do **devices.jobs** não suportam:

* Projeções, por conseguinte, apenas `SELECT *` é possível.
* Condições que fazem referência toohello dispositivo duplo nas propriedades de toojob de adição (consulte Olá anterior a secção).
* Efetuar agregações, tais como contagem, avg, agrupar por.

## <a name="get-started-with-device-to-cloud-message-routes-query-expressions"></a>Começar a utilizar expressões de consulta de rotas de mensagens do dispositivo-nuvem

Utilizar [rotas de dispositivo para nuvem][lnk-devguide-messaging-routes], pode configurar pontos finais toodifferent com base em expressões avaliadas em comparação com as mensagens individuais de mensagens de toodispatch dispositivo para a nuvem do IoT Hub.

rota de Olá [condição] [ lnk-query-expressions] utiliza Olá mesmo idioma de consulta de IoT Hub como condições de consultas duplo e a tarefa. Rota condições são avaliadas no cabeçalhos de mensagens hello e corpo. A expressão de consulta encaminhamento poderá envolver o método apenas cabeçalhos de mensagens, apenas corpo da mensagem hello, ou ambos os cabeçalhos de mensagens e corpo da mensagem. IoT Hub assume um esquema específico para cabeçalhos de Olá e corpo da mensagem em mensagens de tooroute ordem e Olá seguintes secções descreve o que é necessário para a rota de tooproperly do IoT Hub:

### <a name="routing-on-message-headers"></a>Encaminhamento nos cabeçalhos de mensagens

IoT Hub assume Olá após a representação JSON de cabeçalhos de mensagens para o encaminhamento de mensagem:

```json
{
    "$messageId": "",
    "$enqueuedTime": "",
    "$to": "",
    "$expiryTimeUtc": "",
    "$correlationId": "",
    "$userId": "",
    "$ack": "",
    "$connectionDeviceId": "",
    "$connectionDeviceGenerationId": "",
    "$connectionAuthMethod": "",
    "$content-type": "",
    "$content-encoding": "",

    "userProperty1": "",
    "userProperty2": ""
}
```

Propriedades do sistema de mensagens têm o prefixo Olá `'$'` símbolo.
Propriedades do utilizador são sempre acedidas com os respetivos nomes. Se um nome de propriedade de utilizador acontece toocoincide com uma propriedade de sistema (tais como `$to`), será possível obter a propriedade de utilizador Olá com Olá `$to` expressão.
Pode sempre aceder à propriedade de sistema de Olá utilizando parênteses Retos `{}`: por exemplo, pode utilizar expressão Olá `{$to}` tooaccess Olá propriedade de sistema `to`. Os nomes de propriedade entre parênteses obtêm sempre a propriedade de sistema Olá correspondente.

Lembre-se de que os nomes de propriedades são sensível a maiúsculas e minúsculas.

> [!NOTE]
> Todas as propriedades de mensagem são cadeias. Propriedades do sistema, conforme descrito em Olá [guia para programadores][lnk-devguide-messaging-format], atualmente não estão disponível toouse nas consultas.
>

Por exemplo, se utilizar um `messageType` propriedade, poderá pretender tooroute todos os ponto final tooone de telemetria e ponto final de tooanother do todos os alertas. Pode escrever Olá telemetria de Olá expressão tooroute os seguintes:

```sql
messageType = 'telemetry'
```

E Olá seguintes mensagens de alerta por Olá tooroute de expressão:

```sql
messageType = 'alert'
```

Expressões e funções também são suportadas. Esta funcionalidade permite-lhe toodistinguish entre o nível de gravidade, por exemplo:

```sql
messageType = 'alerts' AND as_number(severity) <= 2
```

Consulte toohello [expressão e condições] [ lnk-query-expressions] secção para obter uma lista completa Olá operadores suportados e as funções.

### <a name="routing-on-message-bodies"></a>Encaminhamento corpos de mensagens

IoT Hub apenas pode encaminhar com base no corpo da mensagem conteúdos se o corpo da mensagem Olá está corretamente formado JSON com codificação UTF-8, UTF-16 ou UTF-32. Tem de definir o tipo de mensagem de saudação conteúdo Olá demasiado`application/json` e Olá conteúdo tooone codificação de Olá suportado UTF codificações tooallow de cabeçalhos de mensagem de Olá mensagem de saudação do IoT Hub tooroute com base nos conteúdos do corpo de Olá. Se qualquer um dos cabeçalhos de Olá não for especificado, o IoT Hub não tentará tooevaluate uma expressão de consulta que envolvem corpo Olá contra a mensagem de saudação. Se a mensagem não é uma mensagem JSON ou se a mensagem de saudação não especifica o tipo de conteúdo de Olá e codificação de conteúdo, pode continuar a utilizar a mensagem de saudação tooroute com base nos cabeçalhos de mensagens hello de encaminhamento de mensagens.

Pode utilizar `$body` na mensagem de saudação do Olá consulta expressão tooroute. Pode utilizar uma referência de corpo simples, de referência de matriz de corpo ou várias referências de corpo numa expressão de consulta Olá. A expressão de consulta também pode combinar uma referência de corpo com uma referência de cabeçalho da mensagem. Por exemplo, Olá são todas as expressões de consulta válida:

```sql
$body.message.Weather.Location.State = 'WA'
$body.Weather.HistoricalData[0].Month = 'Feb'
$body.Weather.Temperature = 50 AND $body.message.Weather.IsEnabled
length($body.Weather.Location.State) = 2
$body.Weather.Temperature = 50 AND Status = 'Active'
```

## <a name="basics-of-an-iot-hub-query"></a>Noções básicas de uma consulta do IoT Hub
Cada consulta de IoT Hub é composta por de um, SELECIONE e cláusulas FROM e onde opcional e GROUP BY cláusulas. Cada consulta é executada numa coleção de documentos JSON, por exemplo, dispositivos duplos. cláusula FROM de Olá indica Olá documento coleção toobe iterated no (**dispositivos** ou **devices.jobs**). Olá, em seguida, o filtro em olá onde é aplicada a cláusula. Com agregações, de resultados de Olá deste passo são agrupados como Olá especificado na cláusula GROUP BY e, para cada grupo, é gerada uma linha conforme especificado na cláusula SELECT Olá.

```sql
SELECT <select_list>
FROM <from_specification>
[WHERE <filter_condition>]
[GROUP BY <group_specification>]
```

## <a name="from-clause"></a>A cláusula FROM
Olá **do < from_specification >** cláusula pode assumir apenas dois valores: **dos dispositivos**, tooquery dispositivos duplos, ou **de devices.jobs**, tooquery tarefa por do dispositivo detalhes.

## <a name="where-clause"></a>Cláusula WHERE
Olá **onde < filter_condition >** cláusula é opcional. Especifica uma ou mais condições que os documentos JSON de Olá na coleção de FROM Olá devem satisfazer toobe incluída como parte do resultado de Olá. De qualquer documento JSON tem de avaliar Olá especificado condições demasiado "true" toobe incluída no resultado de Olá.

Olá permitido condições são descritas na secção [expressões e condições][lnk-query-expressions].

## <a name="select-clause"></a>Cláusula SELECT
cláusula SELECT Olá (**SELECIONE < select_list >**) é obrigatória e especifica quais os valores são obtidos a partir de consulta Olá. Especifica Olá JSON valores toobe utilizado toogenerate novos objetos JSON.
Para cada elemento da Olá subconjunto filtrado (e opcionalmente agrupado) da coleção de FROM Olá, a fase de projeção Olá gera um novo objeto JSON, construído com valores de Olá especificados na cláusula SELECT Olá.

Segue-se a gramática Olá da cláusula SELECT Olá:

```
SELECT [TOP <max number>] <projection list>

<projection_list> ::=
    '*'
    | <projection_element> AS alias [, <projection_element> AS alias]+

<projection_element> :==
    attribute_name
    | <projection_element> '.' attribute_name
    | <aggregate>

<aggregate> :==
    count()
    | avg(<projection_element>)
    | sum(<projection_element>)
    | min(<projection_element>)
    | max(<projection_element>)
```

onde **attribute_name** refere-se a propriedade tooany do documento JSON de Olá na coleção de FROM Olá. Alguns exemplos de cláusulas SELECT podem ser encontrados na Olá [introdução às consultas do dispositivo duplo] [ lnk-query-getstarted] secção.

Atualmente, seleção cláusulas diferentes **SELECIONE \***  só são suportados em consultas de agregação em dispositivos duplos.

## <a name="group-by-clause"></a>Cláusula GROUP BY
Olá **GROUP BY < group_specification >** cláusula passo é opcional que pode ser executado após o filtro de Olá especificado no Olá cláusula WHERE e antes de projeção de Olá especificada no Olá SELECIONE. Grupos de documentos com base no valor de Olá de um atributo. Estes grupos são utilizados toogenerate agregado valores conforme especificado na cláusula SELECT Olá.

Um exemplo de uma consulta com GROUP BY é:

```sql
SELECT properties.reported.telemetryConfig.status AS status,
    COUNT() AS numberOfDevices
FROM devices
GROUP BY properties.reported.telemetryConfig.status
```

Olá formal sintaxe GROUP BY está:

```
GROUP BY <group_by_element>
<group_by_element> :==
    attribute_name
    | < group_by_element > '.' attribute_name
```

onde **attribute_name** refere-se a propriedade tooany do documento JSON de Olá na coleção de FROM Olá.

Atualmente, a cláusula GROUP BY Olá só é suportada ao consultar dispositivos duplos.

## <a name="expressions-and-conditions"></a>As expressões e condições
Um nível elevado, um *expressão*:

* Avalia a instância de tooan de um tipo JSON (por exemplo, booleano, número, cadeia, matriz ou objeto), e
* É definido pela manipulação de dados provenientes de documento JSON do dispositivo Olá e constantes utilizando operadores incorporados e funções.

*Condições* são expressões avaliar tooa booleano. Qualquer constante diferente booleano **verdadeiro** são considerados como estando **falso** (incluindo **nulo**, **indefinido**, qualquer instância de objeto ou a matriz qualquer cadeia e claramente Olá booleano **falso**).

Olá sintaxe para expressões é:

```
<expression> ::=
    <constant> |
    attribute_name |
    <function_call> |
    <expression> binary_operator <expression> |
    <create_array_expression> |
    '(' <expression> ')'

<function_call> ::=
    <function_name> '(' expression ')'

<constant> ::=
    <undefined_constant>
    | <null_constant>
    | <number_constant>
    | <string_constant>
    | <array_constant>

<undefined_constant> ::= undefined
<null_constant> ::= null
<number_constant> ::= decimal_literal | hexadecimal_literal
<string_constant> ::= string_literal
<array_constant> ::= '[' <constant> [, <constant>]+ ']'
```

Em que:

| Símbolo | Definição |
| --- | --- |
| attribute_name | Uma propriedade de documento JSON Olá no Olá **FROM** coleção. |
| binary_operator | Nenhum operador binário listado no Olá [operadores](#operators) secção. |
| function_name| Qualquer função listado no Olá [funções](#functions) secção. |
| decimal_literal |Um número de vírgula flutuante expressado na notação decimal. |
| hexadecimal_literal |Um número expresso por cadeia Olá '0x' seguido de uma cadeia de dígitos hexadecimais. |
| string_literal |As literais de cadeia são cadeias Unicode representadas por uma sequência de zero ou mais carateres Unicode ou sequências de escape. As literais de cadeia estão incluídas no plicas (apóstrofo: ') ou de aspas (aspas: "). Permitido escapes: `\'`, `\"`, `\\`, `\uXXXX` caracteres Unicode definido pelo 4 dígitos hexadecimais. |

### <a name="operators"></a>Operadores
é suportado Olá seguintes operadores:

| Família | Operadores |
| --- | --- |
| Aritmética |+,-,*,/,% |
| Lógica |E, EM ALTERNATIVA, NÃO |
| Comparação |=, !=, <, >, <=, >=, <> |

### <a name="functions"></a>Funções
Ao consultar Olá duplos e tarefas, apenas é suportada a função é:

| Função | Descrição |
| -------- | ----------- |
| IS_DEFINED(Property) | Devolve um valor boleano que indica se foi atribuída um valor de propriedade de Olá (incluindo `null`). |

Em condições de rotas, Olá seguintes funções de bibliotecas é suportado:

| Função | Descrição |
| -------- | ----------- |
| Abs(x) | Devolve Olá absoluto () especificado um valor positivo de Olá expressão numérica. |
| Exp(x) | Devolve Olá valor exponencial Olá especificada a expressão numérica (i ^ x). |
| Power(x,y) | Devolve o valor de Olá especificado de Olá toohello de expressão especificado power (x ^ y).|
| SQUARE(x) | Olá devolve quadrado de Olá especificado valor numérico. |
| CEILING(x) | Devolve Olá menor número inteiro maior que ou igual ao hello especificado expressão numérica. |
| FLOOR(x) | Devolve um número inteiro maior de Olá inferior ou igual toohello especificada a expressão numérica. |
| Sign(x) | Devolve Olá positivo (+ 1), zero (0), negativo (-1) sinal de Olá foi especificado ou expressão numérica.|
| SQRT(x) | Olá devolve quadrado de Olá especificado valor numérico. |

Em condições de rotas, é suportado Olá seguinte tipo de verificação e conversão de funções:

| Função | Descrição |
| -------- | ----------- |
| AS_NUMBER | Converte o número de tooa Olá cadeia de entrada. `noop`Se a entrada é um número; `Undefined` se a cadeia não representa um número.|
| IS_ARRAY | Devolve um valor de Booleano indicando se Olá de Olá especificado expressão é uma matriz. |
| IS_BOOL | Devolve um valor de Booleano indicando se Olá de Olá especificado expressão é um valor booleano. |
| IS_DEFINED | Devolve um valor boleano que indica se foi atribuída um valor de propriedade de Olá. |
| IS_NULL | Devolve um valor de Booleano indicando se Olá de Olá especificado expressão é nulo. |
| IS_NUMBER | Devolve um valor de Booleano indicando se Olá de Olá especificado expressão for um número. |
| IS_OBJECT | Devolve um valor de Booleano indicando se Olá de Olá especificado expressão é um objeto JSON. |
| IS_PRIMITIVE | Devolve um valor de Booleano indicando se Olá de Olá especificado expressão é uma primitiva (string, Boolean, numéricos ou `null`). |
| IS_STRING | Devolve um valor de Booleano indicando se Olá de Olá especificado expressão é uma cadeia. |

Em condições de rotas, é suportado Olá seguintes funções de cadeia:

| Função | Descrição |
| -------- | ----------- |
| CONCAT(x,...) | Devolve uma cadeia que é o resultado Olá concatenar duas ou mais valores de cadeia. |
| LENGTH(x) | Devolve Olá número de carateres de Olá especificada a expressão de cadeia.|
| LOWER(x) | Devolve uma expressão de cadeia após a conversão toolowercase de dados do caráter em maiúsculas. |
| UPPER(x) | Devolve uma expressão de cadeia após a conversão toouppercase de dados do caráter em minúsculas. |
| SUBCADEIA (cadeia, início [, comprimento]) | Devolve parte de uma expressão de cadeia começando Olá especificado posição de caráter baseado em zero e continua a toohello especificado comprimento ou toohello fim da cadeia de Olá. |
| INDEX_OF (cadeia, fragmento) | Devolve Olá iniciar a posição da primeira ocorrência de Olá de Olá segunda cadeia expressão numa expressão de cadeia especificada primeiro Olá ou -1 se não é possível encontrar a cadeia de Olá.|
| STARTS_WITH (x, y) | Devolve um valor boleano que indica se primeira expressão de cadeia Olá começa com Olá segundo. |
| ENDS_WITH (x, y) | Devolve um valor boleano que indica se primeira expressão de cadeia Olá termina com Olá segundo. |
| CONTAINS(x,y) | Devolve um valor boleano que indica se primeira expressão de cadeia Olá contém Olá segundo. |

## <a name="next-steps"></a>Passos seguintes
Saiba como tooexecute consulta nas suas aplicações utilizando [SDKs IoT do Azure][lnk-hub-sdks].

[lnk-query-where]: iot-hub-devguide-query-language.md#where-clause
[lnk-query-expressions]: iot-hub-devguide-query-language.md#expressions-and-conditions
[lnk-query-getstarted]: iot-hub-devguide-query-language.md#get-started-with-device-twin-queries

[lnk-twins]: iot-hub-devguide-device-twins.md
[lnk-jobs]: iot-hub-devguide-jobs.md
[lnk-devguide-endpoints]: iot-hub-devguide-endpoints.md
[lnk-devguide-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md
[lnk-devguide-messaging-routes]: iot-hub-devguide-messages-read-custom.md
[lnk-devguide-messaging-format]: iot-hub-devguide-messages-construct.md
[lnk-devguide-messaging-routes]: ./iot-hub-devguide-messages-read-custom.md

[lnk-hub-sdks]: iot-hub-devguide-sdks.md
