---
title: "aaaLog API do Recoletor de dados de HTTP de análise | Microsoft Docs"
description: "Pode utilizar Olá API de Recoletor de dados do registo análise HTTP tooadd POST JSON dados toohello Log Analytics repositório partir de qualquer cliente que pode chamar Olá REST API. Este artigo descreve como toouse Olá API e tem exemplos de como toopublish dados através da utilização de linguagens de programação diferentes."
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: 
ms.assetid: a831fd90-3f55-423b-8b20-ccbaaac2ca75
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: bwren
ms.openlocfilehash: c2921082831c49da764d946ac9c4fab975a38185
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="send-data-toolog-analytics-with-hello-http-data-collector-api"></a>Enviar dados tooLog análise com Olá API de Recoletor de dados de HTTP
Este artigo mostra como toouse Olá API de Recoletor de dados de HTTP toosend dados tooLog análise de um cliente de REST API.  Descreve como tooformat quaisquer dados recolhidos pelo seu script ou aplicação, inclua-o num pedido e tem esse pedido autorizado através da análise de registos.  São fornecidos exemplos do PowerShell, c# e Python.

## <a name="concepts"></a>Conceitos
Pode utilizar Olá API de Recoletor de dados de HTTP toosend dados tooLog Analytics a partir de qualquer cliente que possa chamar uma API REST.  Esta situação pode ter um runbook na automatização do Azure que recolhe a gestão de dados do Azure ou outra nuvem ou poderão ser um sistema de gestão alternativo que utiliza a análise de registos tooconsolidate e analisar dados.

Todos os dados no repositório de análise de registos de Olá é armazenado como um registo com um tipo de registo específica.  Formatar o seu toohello de toosend dados API de Recoletor de dados de HTTP como vários registos em JSON.  Ao submeter dados Olá, será criado um registo individual no repositório de Olá para cada registo no payload de pedido de Olá.


![Descrição geral de Recoletores de dados HTTP](media/log-analytics-data-collector-api/overview.png)



## <a name="create-a-request"></a>Criar um pedido
API de Recoletores de dados do toouse Olá HTTP, criar um pedido POST inclui Olá dados toosend em JavaScript Object Notation (JSON).  Olá três tabelas lista Olá atributos que são necessários para cada pedido. Iremos descrevem cada atributo em mais detalhe posteriormente no artigo Olá.

### <a name="request-uri"></a>URI do pedido
| Atributo | Propriedade |
|:--- |:--- |
| Método |POST |
| URI |https://\<CustomerId\>.ods.opinsights.azure.com/api/logs?api-version=2016-04-01 |
| Tipo de conteúdo |application/json |

### <a name="request-uri-parameters"></a>Parâmetros URI do pedido
| Parâmetro | Descrição |
|:--- |:--- |
| CustomerID |Olá Identificador exclusivo para a área de trabalho do Olá Microsoft Operations Management Suite. |
| Recurso |nome do recurso Olá API: / api/logs. |
| Versão de API |versão de Olá do toouse Olá API com este pedido. Atualmente, é 2016-04-01. |

### <a name="request-headers"></a>Cabeçalhos de pedido
| Cabeçalho | Descrição |
|:--- |:--- |
| Autorização |assinatura de autorização de Olá. Artigo de Olá, pode ler sobre como cabeçalho toocreate um SHA256 HMAC. |
| Tipo de registo |Especifique o tipo de registo de Olá Olá de dados de que estão a ser submetidos. Atualmente, o tipo de registo de Olá suporta apenas carateres alfanuméricos. Não suporta números ou carateres especiais. |
| x-ms-data |data de Olá esse pedido de Olá foi processado, no formato RFC 1123. |
| campo Hora gerado |nome de Olá de um campo de dados de Olá que contém Olá timestamp Olá do item de dados. Se especificar um campo, em seguida, o respetivo conteúdo é utilizado para **TimeGenerated**. Se este campo não está especificado, Olá predefinido para **TimeGenerated** está na altura de Olá esse Olá é ingerida mensagem. conteúdo de Olá do campo de mensagem de Olá deve seguir o formato de Olá ISO 8601 aaaa-MM-Aaaathh. |

## <a name="authorization"></a>Autorização
Qualquer API de Recoletor de dados do registo de análise de HTTP de toohello do pedido tem de incluir um cabeçalho de autorização. tooauthenticate um pedido, tem de iniciar sessão pedido Olá com Olá primário ou de chave secundária do Olá da área de trabalho de Olá que está a efetuar o pedido de Olá. Em seguida, passe esse assinatura como parte do pedido de Olá.   

Eis o formato de Olá para o cabeçalho de autorização de Olá:

```
Authorization: SharedKey <WorkspaceID>:<Signature>
```

*WorkspaceID* é Olá Identificador exclusivo para a área de trabalho do Olá Operations Management Suite. *Assinatura* é um [Message Authentication Code (HMAC) com base em Hash](https://msdn.microsoft.com/library/system.security.cryptography.hmacsha256.aspx) que é criada a partir do pedido de Olá e, em seguida, calculada utilizando Olá [algoritmo SHA256](https://msdn.microsoft.com/library/system.security.cryptography.sha256.aspx). Em seguida, codificá-lo utilizando a codificação Base64.

Utilize este Olá de tooencode formato **SharedKey** cadeia da assinatura:

```
StringToSign = VERB + "\n" +
                  Content-Length + "\n" +
               Content-Type + "\n" +
                  x-ms-date + "\n" +
                  "/api/logs";
```

Eis um exemplo de uma cadeia de assinatura:

```
POST\n1024\napplication/json\nx-ms-date:Mon, 04 Apr 2016 08:00:00 GMT\n/api/logs
```

Quando tiver a cadeia de assinatura de Olá, codificá-lo utilizando Olá Algoritmo HMAC SHA256 no Olá cadeia com codificação UTF-8 e, em seguida, codificar resultado Olá como Base64. Utilize este formato:

```
Signature=Base64(HMAC-SHA256(UTF8(StringToSign)))
```

Exemplos de Olá nas secções seguintes Olá tem toohelp de código de exemplo cria um cabeçalho de autorização.

## <a name="request-body"></a>Corpo do pedido
Olá corpo de mensagem de saudação tem de ser no JSON. Tem de incluir um ou mais registos com Olá propriedade pares nome / valor neste formato:

```
{
"property1": "value1",
" property 2": "value2"
" property 3": "value3",
" property 4": "value4"
}
```

Pode batch vários registos num único pedido utilizando Olá seguir o formato. Todos os registos de Olá tem de ser Olá mesmo tipo de registo.

```
{
"property1": "value1",
" property 2": "value2"
" property 3": "value3",
" property 4": "value4"
},
{
"property1": "value1",
" property 2": "value2"
" property 3": "value3",
" property 4": "value4"
}
```

## <a name="record-type-and-properties"></a>Tipo de registo e as propriedades
Definir um tipo de registo personalizado ao submeter dados através de Olá API de Recoletor de dados do registo de análise de HTTP. Atualmente, não é possível escrever dados tooexisting tipos de registo que foram criados por outros tipos de dados e soluções. Análise de registos lê dados de entrada Olá e, em seguida, cria propriedades que correspondem aos tipos de dados de Olá dos valores de Olá que introduzir.

Cada toohello pedido API de análise do registo tem de incluir um **tipo de registo** cabeçalho com o nome de Olá para o tipo de registo Olá. sufixo Olá **_CL** é nome toohello automaticamente anexado introduza toodistinguish-lo a partir do registo de outro tipos de como um registo personalizado. Por exemplo, se introduzir o nome de Olá **MyNewRecordType**, análise de registos cria um registo com o tipo de Olá **MyNewRecordType_CL**. Isto ajuda a garantir que não existem não existem conflitos entre os nomes de tipo criados pelo utilizador e os que são fornecidos na atuais ou futuras soluções da Microsoft.

tipo de dados de uma propriedade de tooidentify, análise de registos adiciona um nome de propriedade de toohello sufixo. Se uma propriedade contiver um valor nulo, a propriedade Olá não está incluída desse registo. Esta tabela lista o tipo de dados de propriedade Olá e sufixo correspondente:

| Tipo de dados de propriedade | Sufixo |
|:--- |:--- |
| Cadeia |_s |
| Valor booleano |_b |
| duplo |_d |
| Data/hora |_t |
| GUID |_g |

tipo de dados de Olá que utiliza a análise de registos para cada propriedade depende se Olá o tipo de registo para o novo registo de Olá já existe.

* Se o tipo de registo Olá não existir, a análise de registos cria um novo. Análise de registos utiliza o tipo de dados ao hello do toodetermine de inferência Olá JSON tipo para cada propriedade para o novo registo de Olá.
* Se existir o tipo de registo Olá, análise de registos tenta toocreate um novo registo com base nas propriedades existentes. Se Olá tipo de dados para uma propriedade no registo novo Olá não corresponde ao e não pode ser convertida toohello existente tipo ou se hello registo inclui uma propriedade que não existe, análise de registos cria uma nova propriedade que tem o sufixo relevantes Olá.

Por exemplo, esta entrada de submissão criaria um registo com três propriedades, **number_d**, **boolean_b**, e **string_s**:

![Registo de exemplo 1](media/log-analytics-data-collector-api/record-01.png)

Se tiver submetido, em seguida, esta entrada seguinte, com todos os valores a formatados como cadeias, propriedades Olá não ser alterado. Estes valores podem ser convertida tooexisting tipos de dados:

![Registo de exemplo 2](media/log-analytics-data-collector-api/record-02.png)

No entanto, se tiver efetuado, em seguida, este submissão seguinte, análise de registos criaria Olá novas propriedades **boolean_d** e **string_d**. Não não possível converter estes valores:

![Registo de exemplo 3](media/log-analytics-data-collector-api/record-03.png)

Se, em seguida, submetido Olá entrada, a seguir antes da criação do tipo de registo Olá, análise de registos criaria um registo com três propriedades, **number_s**, **boolean_s**, e **string_s**. Esta entrada, cada um dos valores iniciais Olá está formatada como uma cadeia:

![Registo de exemplo 4](media/log-analytics-data-collector-api/record-04.png)

## <a name="data-limits"></a>Limites de dados
Existem algumas restrições à volta de dados de Olá publicados toohello recolha de dados do Log Analytics API.

* Máximo de 30 MB por post tooLog API de Recoletor de dados de análise. Este é um limite de tamanho para um único pedido de post. Se os dados de um pedido de post único que exceda 30 MB Olá, deve dividir Olá dados de cópia de segurança toosmaller tamanho segmentos e enviá-las em simultâneo.
* Máximo de limite de 32 KB para os valores de campo. Se o valor do campo Olá for superior a 32 KB, dados de Olá serão truncados.
* Recomendada número máximo de campos para um determinado tipo é 50. Este é um limite prático de uma perspetiva de experiência de pesquisa e facilidade de utilização.  

## <a name="return-codes"></a>Códigos de retorno
Olá, código de estado HTTP 200 significa que esse pedido Olá foi recebido para processamento. Isto indica dessa operação Olá foi concluída com êxito.

Esta tabela lista o conjunto completo de Olá de códigos de estado que poderá devolver serviço Olá:

| Código | Estado | Código de erro | Descrição |
|:--- |:--- |:--- |:--- |
| 200 |OK | |pedido de Olá foi aceite com êxito. |
| 400 |Pedido incorreto |InactiveCustomer |área de trabalho Olá foi fechada. |
| 400 |Pedido incorreto |InvalidApiVersion |versão de API de Olá que especificou não foi reconhecido pelo serviço de Olá. |
| 400 |Pedido incorreto |InvalidCustomerId |ID da área de trabalho de Olá especificado é inválido. |
| 400 |Pedido incorreto |InvalidDataFormat |Foi submetida JSON inválido. corpo da resposta Olá pode conter mais informações sobre como tooresolve Olá erro. |
| 400 |Pedido incorreto |InvalidLogType |o tipo de registo de Olá especificado continha carateres especiais ou números. |
| 400 |Pedido incorreto |MissingApiVersion |Não foi especificada a versão da API Olá. |
| 400 |Pedido incorreto |MissingContentType |Não foi especificado o tipo de conteúdo de Olá. |
| 400 |Pedido incorreto |MissingLogType |Olá necessário não foi especificado o tipo de valor de registo. |
| 400 |Pedido incorreto |UnsupportedContentType |tipo de conteúdo de Olá não foi definido demasiado**application/json**. |
| 403 |Proibido |InvalidAuthorization |pedido de Olá tooauthenticate do serviço de Olá falhou. Certifique-se de que essa chave de ID e a ligação de área de trabalho do Olá são válidos. |
| 404 |Não foi encontrado | | O URL de Olá fornecido está incorreto ou Olá do pedido é demasiado grande. |
| 429 |Demasiados pedidos | | serviço de Olá está com um elevado volume de dados da sua conta. Repita o pedido de Olá mais tarde. |
| 500 |Erro interno do servidor |UnspecifiedError |serviço de Olá encontrou um erro interno. Repita o pedido de Olá. |
| 503 |Serviço indisponível |ServiceUnavailable |o serviço de Olá está atualmente indisponível tooreceive pedidos. Repita o pedido. |

## <a name="query-data"></a>Consultar dados
dados de tooquery submetidos por Olá API de Recoletor de dados de HTTP de análise de registo, procure registos com **tipo** que seja igual toohello **LogType** valor que especificou, acrescentar **_CL**. Por exemplo, se tiver utilizado **MyCustomLog**, em seguida, iria devolver todos os registos com **tipo = MyCustomLog_CL**.

>[!NOTE]
> Se a sua área de trabalho tiver sido atualizado toohello [idioma de consulta de análise de registos nova](log-analytics-log-search-upgrade.md), em seguida, Olá acima consulta alteraria toohello seguinte.

> `MyCustomLog_CL`

## <a name="sample-requests"></a>Pedidos de exemplo
Olá secções seguintes, irá encontrar exemplos de como toosubmit dados toohello API de Recoletor de dados do registo de análise de HTTP utilizando diferentes linguagens de programação.

Para cada amostra, execute estes passos variáveis de Olá tooset para o cabeçalho de autorização de Olá:

1. No portal do Operations Management Suite Olá, selecione Olá **definições** mosaico e, em seguida, selecione Olá **origens ligadas** separador.
2. toohello à direita dos **ID da área de trabalho**, selecione o ícone de cópia de Olá e, em seguida, cole Olá ID como valor Olá Olá **ID de cliente** variável.
3. toohello à direita dos **chave primária**, selecione o ícone de cópia de Olá e, em seguida, cole Olá ID como valor Olá Olá **chave partilhada** variável.

Em alternativa, pode alterar as variáveis de Olá para o tipo de registo de Olá e dados JSON.

### <a name="powershell-sample"></a>Exemplo do PowerShell
```
# Replace with your Workspace ID
$CustomerId = "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"  

# Replace with your Primary Key
$SharedKey = "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"

# Specify hello name of hello record type that you'll be creating
$LogType = "MyRecordType"

# Specify a field with hello created time for hello records
$TimeStampField = "DateValue"


# Create two records with hello same set of properties toocreate
$json = @"
[{  "StringValue": "MyString1",
    "NumberValue": 42,
    "BooleanValue": true,
    "DateValue": "2016-05-12T20:00:00.625Z",
    "GUIDValue": "9909ED01-A74C-4874-8ABF-D2678E3AE23D"
},
{   "StringValue": "MyString2",
    "NumberValue": 43,
    "BooleanValue": false,
    "DateValue": "2016-05-12T20:00:00.625Z",
    "GUIDValue": "8809ED01-A74C-4874-8ABF-D2678E3AE23D"
}]
"@

# Create hello function toocreate hello authorization signature
Function Build-Signature ($customerId, $sharedKey, $date, $contentLength, $method, $contentType, $resource)
{
    $xHeaders = "x-ms-date:" + $date
    $stringToHash = $method + "`n" + $contentLength + "`n" + $contentType + "`n" + $xHeaders + "`n" + $resource

    $bytesToHash = [Text.Encoding]::UTF8.GetBytes($stringToHash)
    $keyBytes = [Convert]::FromBase64String($sharedKey)

    $sha256 = New-Object System.Security.Cryptography.HMACSHA256
    $sha256.Key = $keyBytes
    $calculatedHash = $sha256.ComputeHash($bytesToHash)
    $encodedHash = [Convert]::ToBase64String($calculatedHash)
    $authorization = 'SharedKey {0}:{1}' -f $customerId,$encodedHash
    return $authorization
}


# Create hello function toocreate and post hello request
Function Post-OMSData($customerId, $sharedKey, $body, $logType)
{
    $method = "POST"
    $contentType = "application/json"
    $resource = "/api/logs"
    $rfc1123date = [DateTime]::UtcNow.ToString("r")
    $contentLength = $body.Length
    $signature = Build-Signature `
        -customerId $customerId `
        -sharedKey $sharedKey `
        -date $rfc1123date `
        -contentLength $contentLength `
        -fileName $fileName `
        -method $method `
        -contentType $contentType `
        -resource $resource
    $uri = "https://" + $customerId + ".ods.opinsights.azure.com" + $resource + "?api-version=2016-04-01"

    $headers = @{
        "Authorization" = $signature;
        "Log-Type" = $logType;
        "x-ms-date" = $rfc1123date;
        "time-generated-field" = $TimeStampField;
    }

    $response = Invoke-WebRequest -Uri $uri -Method $method -ContentType $contentType -Headers $headers -Body $body -UseBasicParsing
    return $response.StatusCode

}

# Submit hello data toohello API endpoint
Post-OMSData -customerId $customerId -sharedKey $sharedKey -body ([System.Text.Encoding]::UTF8.GetBytes($json)) -logType $logType  
```

### <a name="c-sample"></a>Exemplo C#
```
using System;
using System.Net;
using System.Net.Http;
using System.Net.Http.Headers;
using System.Security.Cryptography;
using System.Text;
using System.Threading.Tasks;

namespace OIAPIExample
{
    class ApiExample
    {
        // An example JSON object, with key/value pairs
        static string json = @"[{""DemoField1"":""DemoValue1"",""DemoField2"":""DemoValue2""},{""DemoField3"":""DemoValue3"",""DemoField4"":""DemoValue4""}]";

        // Update customerId tooyour Operations Management Suite workspace ID
        static string customerId = "xxxxxxxx-xxx-xxx-xxx-xxxxxxxxxxxx";

        // For sharedKey, use either hello primary or hello secondary Connected Sources client authentication key   
        static string sharedKey = "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxx";

        // LogName is name of hello event type that is being submitted tooLog Analytics
        static string LogName = "DemoExample";

        // You can use an optional field toospecify hello timestamp from hello data. If hello time field is not specified, Log Analytics assumes hello time is hello message ingestion time
        static string TimeStampField = "";

        static void Main()
        {
            // Create a hash for hello API signature
            var datestring = DateTime.UtcNow.ToString("r");
            string stringToHash = "POST\n" + json.Length + "\napplication/json\n" + "x-ms-date:" + datestring + "\n/api/logs";
            string hashedString = BuildSignature(stringToHash, sharedKey);
            string signature = "SharedKey " + customerId + ":" + hashedString;

            PostData(signature, datestring, json);
        }

        // Build hello API signature
        public static string BuildSignature(string message, string secret)
        {
            var encoding = new System.Text.ASCIIEncoding();
            byte[] keyByte = Convert.FromBase64String(secret);
            byte[] messageBytes = encoding.GetBytes(message);
            using (var hmacsha256 = new HMACSHA256(keyByte))
            {
                byte[] hash = hmacsha256.ComputeHash(messageBytes);
                return Convert.ToBase64String(hash);
            }
        }

        // Send a request toohello POST API endpoint
        public static void PostData(string signature, string date, string json)
        {
            try
            {
                string url = "https://" + customerId + ".ods.opinsights.azure.com/api/logs?api-version=2016-04-01";

                System.Net.Http.HttpClient client = new System.Net.Http.HttpClient();
                client.DefaultRequestHeaders.Add("Accept", "application/json");
                client.DefaultRequestHeaders.Add("Log-Type", LogName);
                client.DefaultRequestHeaders.Add("Authorization", signature);
                client.DefaultRequestHeaders.Add("x-ms-date", date);
                client.DefaultRequestHeaders.Add("time-generated-field", TimeStampField);

                System.Net.Http.HttpContent httpContent = new StringContent(json, Encoding.UTF8);
                httpContent.Headers.ContentType = new MediaTypeHeaderValue("application/json");
                Task<System.Net.Http.HttpResponseMessage> response = client.PostAsync(new Uri(url), httpContent);

                System.Net.Http.HttpContent responseContent = response.Result.Content;
                string result = responseContent.ReadAsStringAsync().Result;
                Console.WriteLine("Return Result: " + result);
            }
            catch (Exception excep)
            {
                Console.WriteLine("API Post Exception: " + excep.Message);
            }
        }
    }
}

```

### <a name="python-sample"></a>Exemplo de Python
```
import json
import requests
import datetime
import hashlib
import hmac
import base64

# Update hello customer ID tooyour Operations Management Suite workspace ID
customer_id = 'xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx'

# For hello shared key, use either hello primary or hello secondary Connected Sources client authentication key   
shared_key = "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"

# hello log type is hello name of hello event that is being submitted
log_type = 'WebMonitorTest'

# An example JSON web monitor object
json_data = [{
   "slot_ID": 12345,
    "ID": "5cdad72f-c848-4df0-8aaa-ffe033e75d57",
    "availability_Value": 100,
    "performance_Value": 6.954,
    "measurement_Name": "last_one_hour",
    "duration": 3600,
    "warning_Threshold": 0,
    "critical_Threshold": 0,
    "IsActive": "true"
},
{   
    "slot_ID": 67890,
    "ID": "b6bee458-fb65-492e-996d-61c4d7fbb942",
    "availability_Value": 100,
    "performance_Value": 3.379,
    "measurement_Name": "last_one_hour",
    "duration": 3600,
    "warning_Threshold": 0,
    "critical_Threshold": 0,
    "IsActive": "false"
}]
body = json.dumps(json_data)

#####################
######Functions######  
#####################

# Build hello API signature
def build_signature(customer_id, shared_key, date, content_length, method, content_type, resource):
    x_headers = 'x-ms-date:' + date
    string_to_hash = method + "\n" + str(content_length) + "\n" + content_type + "\n" + x_headers + "\n" + resource
    bytes_to_hash = bytes(string_to_hash).encode('utf-8')  
    decoded_key = base64.b64decode(shared_key)
    encoded_hash = base64.b64encode(hmac.new(decoded_key, bytes_to_hash, digestmod=hashlib.sha256).digest())
    authorization = "SharedKey {}:{}".format(customer_id,encoded_hash)
    return authorization

# Build and send a request toohello POST API
def post_data(customer_id, shared_key, body, log_type):
    method = 'POST'
    content_type = 'application/json'
    resource = '/api/logs'
    rfc1123date = datetime.datetime.utcnow().strftime('%a, %d %b %Y %H:%M:%S GMT')
    content_length = len(body)
    signature = build_signature(customer_id, shared_key, rfc1123date, content_length, method, content_type, resource)
    uri = 'https://' + customer_id + '.ods.opinsights.azure.com' + resource + '?api-version=2016-04-01'

    headers = {
        'content-type': content_type,
        'Authorization': signature,
        'Log-Type': log_type,
        'x-ms-date': rfc1123date
    }

    response = requests.post(uri,data=body, headers=headers)
    if (response.status_code >= 200 and response.status_code <= 299):
        print 'Accepted'
    else:
        print "Response code: {}".format(response.status_code)

post_data(customer_id, shared_key, body, log_type)
```

## <a name="next-steps"></a>Passos seguintes
- Olá utilize [API de pesquisa de registo](log-analytics-log-search-api.md) tooretrieve dados do repositório de análise de registos de Olá.
