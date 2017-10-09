---
title: "enlaces de funções de HTTP e webhook aaaAzure | Microsoft Docs"
description: "Compreender a forma como toouse HTTP e webhook aciona e os enlaces de funções do Azure."
services: functions
documentationcenter: na
author: mattchenderson
manager: erikre
editor: 
tags: 
keywords: "das funções do Azure, funções, eventos de processamento, webhooks, dinâmicos de computação, arquitetura sem servidor, HTTP, API, REST"
ms.assetid: 2b12200d-63d8-4ec1-9da8-39831d5a51b1
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 11/18/2016
ms.author: mahender
ms.openlocfilehash: c23b7a1443d492ed78c595e97d1d778a7ab12416
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-http-and-webhook-bindings"></a>Enlaces de funções de HTTP e webhook do Azure
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

Este artigo explica como aciona tooconfigure e trabalhar com HTTP e os enlaces de funções do Azure.
Com estas, pode utilizar as funções do Azure toobuild sem servidor APIs e respondeu toowebhooks.

As funções do Azure fornece Olá enlaces a seguir:
- Um [acionador HTTP](#httptrigger) permite invocar uma função com um pedido de HTTP. Isto pode ser personalizado toorespond[webhooks](#hooktrigger).
- Um [vínculo de saída HTTP](#output) permite-lhe toorespond toohello pedido.

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

[!INCLUDE [HTTP client best practices](../../includes/functions-http-client-best-practices.md)]

<a name="httptrigger"></a>

## <a name="http-trigger"></a>Acionador HTTP
acionador HTTP Olá executará a função no pedido HTTP de tooan de resposta. Pode personalizar toorespond tooa determinado URL ou um conjunto de métodos de HTTP. Um acionador HTTP, também pode ser configurado toorespond toowebhooks. 

Se utilizar o portal de funções de Olá, pode também começar a utilizar imediato utilizando um modelo de pré-efetuado. Selecione **nova função** e escolher "API e Webhooks" Olá **cenário** pendente. Selecione um dos modelos de Olá e clique em **criar**.

Por predefinição, um acionador HTTP responderá toohello pedido com um código de estado HTTP 200 OK e um corpo vazio. toomodify Olá resposta, configure um [enlace HTTP de saída](#output)

### <a name="configuring-an-http-trigger"></a>Configurar um acionador HTTP
Um acionador HTTP está definido, incluindo um toohello semelhante de objeto JSON a seguir no Olá `bindings` matriz de function.json:

```json
{
    "name": "req",
    "type": "httpTrigger",
    "direction": "in",
    "authLevel": "function",
    "methods": [ "get" ],
    "route": "values/{id}"
},
```
enlace de Olá suporta Olá seguintes propriedades:

* **nome** : necessária - o nome da variável Olá utilizado no código de função para o pedido de Olá ou corpo do pedido. Consulte [trabalhar com um acionador HTTP a partir do código](#httptriggerusage).
* **tipo** : obrigatória - tem de ser definido demasiado "httpTrigger".
* **direção** : obrigatória - tem de ser definido demasiado "em".
* _authLevel_ : Isto determina as chaves, se existirem, precisam de toobe presente no pedido de Olá na função de Olá tooinvoke de ordem. Consulte [trabalhar com as chaves](#keys) abaixo. valor de Olá pode ser um dos seguintes Olá:
    * _anónimo_: a chave de API não é necessária.
    * _função_: é necessária uma chave de API específicas. Este é o valor predefinido de Olá se não for fornecido nenhum.
    * _administração_ : Olá mestre chave é necessária.
* **métodos** : Esta é uma matriz dos métodos de Olá HTTP a função de Olá toowhich responderá. Se não for especificado, a função de Olá responderá métodos tooall HTTP. Consulte [personalizar o ponto final de Olá HTTP](#url).
* **rota** : Isto define o modelo de rota Olá, controlar toowhich URLs responderá a função do pedido. Olá valor predefinido se não for fornecido nenhum é `<functionname>`. Consulte [personalizar o ponto final de Olá HTTP](#url).
* **webHookType** : Esta ação configura Olá HTTP acionador tooact como reciever um webhook de fornecedor especificado Olá. Olá _métodos_ propriedade não deve ser definida se isto for escolhido. Consulte [responder toowebhooks](#hooktrigger). valor de Olá pode ser um dos seguintes Olá:
    * _genericJson_ : um ponto final de webhook fins gerais sem lógica para um fornecedor específico.
    * _github_ : função Olá responderá tooGitHub webhooks. Olá _authLevel_ propriedade não deve ser definida se isto for escolhido.
    * _slack_ : função Olá responderá tooSlack webhooks. Olá _authLevel_ propriedade não deve ser definida se isto for escolhido.

<a name="httptriggerusage"></a>
### <a name="working-with-an-http-trigger-from-code"></a>Trabalhar com um acionador HTTP a partir do código
Para as funções de c# e F #, podem declarar tipo Olá do seu toobe de entrada de Acionador ou `HttpRequestMessage` ou um tipo personalizado. Se optar por `HttpRequestMessage`, em seguida, irá obter o objeto de pedido de toohello acesso total. Para um tipo personalizado (por exemplo, um POCO), funções tentará corpo do pedido tooparse Olá como as propriedades do objeto JSON toopopulate Olá.

Para funções de Node.js, tempo de execução do Olá funções fornece o corpo do pedido Olá em vez de objecto de pedido de Olá.

Consulte [amostras de Acionador HTTP](#httptriggersample) utilizações por exemplo.


<a name="output"></a>
## <a name="http-response-output-binding"></a>Enlace de saída de resposta de HTTP
Utilize Olá HTTP saída enlace toorespond toohello HTTP pedido remetente. Este enlace necessita de um acionador HTTP e permite-lhe resposta de Olá toocustomize associada pedido trigger Olá. Se o enlace de saída de um HTTP não for fornecido, um acionador HTTP irá devolver HTTP 200 OK com uma mensagem vazia. 

### <a name="configuring-an-http-output-binding"></a>Configurar um HTTP de saída do enlace
Olá HTTP de saída do enlace está definido, incluindo um toohello semelhante de objeto JSON a seguir no Olá `bindings` matriz de function.json:

```json
{
    "name": "res",
    "type": "http",
    "direction": "out"
}
```
o enlace de Olá contém Olá seguintes propriedades:

* **nome** : obrigatória - Olá utilizado no código de função para resposta Olá o nome da variável. Consulte [enlace a partir do código de saída de trabalhar com um HTTP](#outputusage).
* **tipo** : obrigatória - tem de ser definido demasiado "http".
* **direção** : obrigatória - tem de ser definido demasiado "out".

<a name="outputusage"></a>
### <a name="working-with-an-http-output-binding-from-code"></a>Trabalhar com um HTTP enlace a partir do código de saída
Pode utilizar Olá saída parâmetro (por exemplo, "res") toorespond toohello http ou webhook autor da chamada. Em alternativa, pode utilizar o padrão `Request.CreateResponse()` (c#) ou `context.res` (Node.JS) padrão tooreturn sua resposta. Para obter exemplos sobre como toouse Olá método última, consulte [amostras de Acionador HTTP](#httptriggersample) e [amostras de Acionador de Webhook](#hooktriggersample).


<a name="hooktrigger"></a>
## <a name="responding-toowebhooks"></a>Responder toowebhooks
Um acionador HTTP com Olá _webHookType_ propriedade será configurado toorespond demasiado[webhooks](https://en.wikipedia.org/wiki/Webhook). configuração básica Olá utiliza a definição de "genericJson" Olá. Restringe esta pedidos tooonly as utilizando o HTTP POST e com Olá `application/json` tipo de conteúdo.

Olá acionador pode ser tooa personalizáveis fornecedor de webhook específico (por exemplo, [GitHub](https://developer.github.com/webhooks/) e [Slack](https://api.slack.com/outgoing-webhooks)). Se não for especificado um fornecedor, o tempo de execução do Olá funções pode asseguramos lógica de validação do fornecedor de Olá por si.  

### <a name="configuring-github-as-a-webhook-provider"></a>Configuração de GitHub como um fornecedor de webhook
toorespond tooGitHub webhooks, primeiro criar a sua função com um acionador de HTTP e defina Olá _webHookType_ propriedade demasiado "github". Em seguida, copie o [URL](#url) e [chave de API](#keys) no seu repositório GitHub **adicionar webhook** página. Consulte o artigo do GitHub [criar Webhooks](http://go.microsoft.com/fwlink/?LinkID=761099&clcid=0x409) documentação para obter mais informações.

![](./media/functions-bindings-http-webhook/github-add-webhook.png)

### <a name="configuring-slack-as-a-webhook-provider"></a>Configurar Slack como um fornecedor de webhook
webhook Slack Olá gera um token para si em vez de permitindo-lhe especificar, pelo que tem de configurar uma chave de específicas com token Olá de Slack. Consulte [trabalhar com as chaves](#keys).

<a name="url"></a>
## <a name="customizing-hello-http-endpoint"></a>Personalizar o ponto final de HTTP Olá
Por predefinição quando cria uma função de um acionador HTTP ou o WebHook, função Olá é endereçável com uma rota de formulário Olá:

    http://<yourapp>.azurewebsites.net/api/<funcname> 

Pode personalizar esta rota utilizando Olá opcional `route` propriedade no acionador Olá HTTP de entrada de enlace. Por exemplo, Olá seguir *function.json* ficheiro define um `route` propriedade para um acionador HTTP:

```json
    {
      "bindings": [
        {
          "type": "httpTrigger",
          "name": "req",
          "direction": "in",
          "methods": [ "get" ],
          "route": "products/{category:alpha}/{id:int?}"
        },
        {
          "type": "http",
          "name": "res",
          "direction": "out"
        }
      ]
    }
```

Utilizando esta configuração, Olá função é agora endereçável com Olá rota em vez de rota original Olá a seguir.

    http://<yourapp>.azurewebsites.net/api/products/electronics/357

Isto permite que o código de função Olá toosupport dois parâmetros no endereço Olá, "categoria" e "id". Pode utilizar qualquer [Web API rota restrição](https://www.asp.net/web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2#constraints) com os parâmetros. Olá o seguinte código à função c# utilizam ambos os parâmetros.

```csharp
    public static Task<HttpResponseMessage> Run(HttpRequestMessage req, string category, int? id, 
                                                    TraceWriter log)
    {
        if (id == null)
           return  req.CreateResponse(HttpStatusCode.OK, $"All {category} items were requested.");
        else
           return  req.CreateResponse(HttpStatusCode.OK, $"{category} item with id = {id} has been requested.");
    }
```

Eis Olá do Node.js função código toouse mesmos parâmetros de rota.

```javascript
    module.exports = function (context, req) {

        var category = context.bindingData.category;
        var id = context.bindingData.id;

        if (!id) {
            context.res = {
                // status: 200, /* Defaults too200 */
                body: "All " + category + " items were requested."
            };
        }
        else {
            context.res = {
                // status: 200, /* Defaults too200 */
                body: category + " item with id = " + id + " was requested."
            };
        }

        context.done();
    } 
```

Por predefinição, todas as rotas de função são adicionado o prefixo *api*. Também pode personalizar ou remover o prefixo de Olá utilizando Olá `http.routePrefix` propriedade no seu *host.json* ficheiro. Olá exemplo a seguir remove Olá *api* prefixo de rota através da utilização de uma cadeia vazia para o prefixo de Olá no Olá *host.json* ficheiro.

```json
    {
      "http": {
        "routePrefix": ""
      }
    }
```

Para obter informações detalhadas sobre como tooupdate Olá *host.json* ficheiro para a função, consulte [como ficheiros de aplicação de função tooupdate](functions-reference.md#fileupdate). 

Para obter informações sobre outras propriedades que pode configurar na sua *host.json* de ficheiros, consulte [host.json referência](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json).


<a name="keys"></a>
## <a name="working-with-keys"></a>Trabalhar com as chaves
HttpTriggers pode tirar partido das chaves de segurança adicional. Um padrão HttpTrigger pode utilizá-las como uma chave de API, exigindo Olá toobe chave presente no pedido de Olá. Webhooks pode utilizar os pedidos de tooauthorize de chaves de diversas formas, consoante o fornecedor de Olá suporta.

As chaves são armazenadas como parte da sua aplicação de função no Azure e são encriptadas em pausa. tooview as chaves, criar novos ou toonew valores de chaves de agregação, navegue tooone das suas funções no portal de Olá e selecione "Gerir". 

Existem dois tipos de chaves:
- **Das chaves de anfitrião**: estas chaves são partilhadas por todas as funções dentro da aplicação de função Olá. Quando utilizado como uma chave de API, estes cmdlets permitem a função de tooany de acesso à aplicação de função Olá.
- **As chaves de função**: estas chaves aplicam-se apenas toohello funções específicas em que estão definidos. Quando utilizado como uma chave de API, estes apenas permitem o acesso toothat função.

Cada chave com o nome de referência e existe uma chave de predefinição (denominada "predefinido") ao nível de função e o anfitrião de Olá. Olá **chave mestra** uma chave de anfitrião predefinido com o nome "_master" que está definido para cada aplicação de função e não pode ser revogado. Fornece acesso administrativo toohello runtime APIs. Utilizar `"authLevel": "admin"` na Olá enlace JSON irá exigir esta chave toobe apresentada no pedido de Olá; qualquer outra chave ocorrerá uma falha de autorização.

> [!NOTE]
> Devida toohello elevados permissões concedidas pela chave mestra de Olá, não deve partilhar esta chave com terceiros nem distribui-lo em aplicações de cliente nativo. Tenha cuidado quando escolher o nível de autorização de administrador Olá.
> 
> 

### <a name="api-key-authorization"></a>Autorização da chave de API
Por predefinição, um HttpTrigger requer uma chave de API no pedido HTTP Olá. Por isso, o pedido HTTP normalmente este aspeto:

    https://<yourapp>.azurewebsites.net/api/<function>?code=<ApiKey>

chave de Olá pode ser incluído numa variável de cadeia de consulta com o nome `code`, como acima, ou pode ser incluído num `x-functions-key` cabeçalho de HTTP. valor de Olá da chave de Olá pode ser qualquer tecla de função definido para a função de Olá ou qualquer chave de anfitrião.

Pode escolher tooallow pedidos sem chaves ou especificar essa chave mestra de Olá tem de ser utilizado pela alteração Olá `authLevel` propriedade no Olá enlace JSON (consulte [acionador HTTP](#httptrigger)).

### <a name="keys-and-webhooks"></a>As chaves e webhooks
Autorização de Webhook é processada pelo componente de reciever de webhook Olá, parte Olá HttpTrigger e o mecanismo de Olá varia com base no tipo de webhook Olá. Cada mecanismo, o Contudo dependem de uma chave. Por predefinição, será utilizada a tecla de função de Olá com o nome "predefinida". Se desejar toouse uma chave diferente, terá de tooconfigure Olá webhook fornecedor toosend Olá nome da chave com o pedido de Olá dos Olá seguintes formas:

- **Cadeia de consulta**: fornecedor de Olá transmite o nome da chave Olá no Olá `clientid` parâmetro de cadeia de consulta (por exemplo, `https://<yourapp>.azurewebsites.net/api/<funcname>?clientid=<keyname>`).
- **Cabeçalho de pedido**: fornecedor de Olá transmite o nome da chave Olá no Olá `x-functions-clientid` cabeçalho.

> [!NOTE]
> Teclas de função têm precedência sobre as chaves de anfitrião. Se duas chaves são definidas com o mesmo nome, hello de Olá função chave será utilizada.
> 
> 


<a name="httptriggersample"></a>
## <a name="http-trigger-samples"></a>Exemplos de Acionador HTTP
Suponhamos tiver Olá seguir acionador HTTP de Olá `bindings` matriz de function.json:

```json
{
    "name": "req",
    "type": "httpTrigger",
    "direction": "in",
    "authLevel": "function"
},
```

Consulte o exemplo de específicas do idioma Olá que procura um `name` parâmetro ou na cadeia de consulta Olá ou no corpo de Olá do pedido de Olá HTTP.

* [C#](#httptriggercsharp)
* [F#](#httptriggerfsharp)
* [Node.js](#httptriggernodejs)


<a name="httptriggercsharp"></a>
### <a name="http-trigger-sample-in-c"></a>Exemplo de Acionador HTTP em c# #
```csharp
using System.Net;
using System.Threading.Tasks;

public static async Task<HttpResponseMessage> Run(HttpRequestMessage req, TraceWriter log)
{
    log.Info($"C# HTTP trigger function processed a request. RequestUri={req.RequestUri}");

    // parse query parameter
    string name = req.GetQueryNameValuePairs()
        .FirstOrDefault(q => string.Compare(q.Key, "name", true) == 0)
        .Value;

    // Get request body
    dynamic data = await req.Content.ReadAsAsync<object>();

    // Set name tooquery string or body data
    name = name ?? data?.name;

    return name == null
        ? req.CreateResponse(HttpStatusCode.BadRequest, "Please pass a name on hello query string or in hello request body")
        : req.CreateResponse(HttpStatusCode.OK, "Hello " + name);
}
```

Também é possível vincular tooa POCO em vez de `HttpRequestMessage`. Isto irá ser hydrated do corpo de Olá de pedido de Olá, analisado como JSON. Da mesma forma, um tipo pode ser transmitido a saída de resposta HTTP de toohello enlace e este será devolvido como corpo da resposta Olá, com um código de 200 estado.
```csharp
using System.Net;
using System.Threading.Tasks;

public static string Run(CustomObject req, TraceWriter log)
{
    return "Hello " + req?.name;
}

public class CustomObject {
     public String name {get; set;}
}
}
```

<a name="httptriggerfsharp"></a>
### <a name="http-trigger-sample-in-f"></a>Exemplo de Acionador HTTP no F # #
```fsharp
open System.Net
open System.Net.Http
open FSharp.Interop.Dynamic

let Run(req: HttpRequestMessage) =
    async {
        let q =
            req.GetQueryNameValuePairs()
                |> Seq.tryFind (fun kv -> kv.Key = "name")
        match q with
        | Some kv ->
            return req.CreateResponse(HttpStatusCode.OK, "Hello " + kv.Value)
        | None ->
            let! data = Async.AwaitTask(req.Content.ReadAsAsync<obj>())
            try
                return req.CreateResponse(HttpStatusCode.OK, "Hello " + data?name)
            with e ->
                return req.CreateErrorResponse(HttpStatusCode.BadRequest, "Please pass a name on hello query string or in hello request body")
    } |> Async.StartAsTask
```

É necessário um `project.json` ficheiros que utilize NuGet tooreference Olá `FSharp.Interop.Dynamic` e `Dynamitey` assemblagens, como esta:

```json
{
  "frameworks": {
    "net46": {
      "dependencies": {
        "Dynamitey": "1.0.2",
        "FSharp.Interop.Dynamic": "3.0.0"
      }
    }
  }
}
```

Isto irá utilizar as suas dependências NuGet toofetch e fará referência na seu script.

<a name="httptriggernodejs"></a>
### <a name="http-trigger-sample-in-nodejs"></a>Exemplo de Acionador HTTP no Node.JS
```javascript
module.exports = function(context, req) {
    context.log('Node.js HTTP trigger function processed a request. RequestUri=%s', req.originalUrl);

    if (req.query.name || (req.body && req.body.name)) {
        context.res = {
            // status: 200, /* Defaults too200 */
            body: "Hello " + (req.query.name || req.body.name)
        };
    }
    else {
        context.res = {
            status: 400,
            body: "Please pass a name on hello query string or in hello request body"
        };
    }
    context.done();
};
```



<a name="hooktriggersample"></a>
## <a name="webhook-samples"></a>Amostras do Webhook
Suponhamos tiver Olá seguir acionador de webhook no Olá `bindings` matriz de function.json:

```json
{
    "webHookType": "github",
    "name": "req",
    "type": "httpTrigger",
    "direction": "in",
},
```

Consulte o exemplo do Olá específicas do idioma que os registos de comentários de problema do GitHub.

* [C#](#hooktriggercsharp)
* [F#](#hooktriggerfsharp)
* [Node.js](#hooktriggernodejs)

<a name="hooktriggercsharp"></a>

### <a name="webhook-sample-in-c"></a>Exemplo de Webhook em c# #
```csharp
#r "Newtonsoft.Json"

using System;
using System.Net;
using System.Threading.Tasks;
using Newtonsoft.Json;

public static async Task<object> Run(HttpRequestMessage req, TraceWriter log)
{
    string jsonContent = await req.Content.ReadAsStringAsync();
    dynamic data = JsonConvert.DeserializeObject(jsonContent);

    log.Info($"WebHook was triggered! Comment: {data.comment.body}");

    return req.CreateResponse(HttpStatusCode.OK, new {
        body = $"New GitHub comment: {data.comment.body}"
    });
}
```

<a name="hooktriggerfsharp"></a>

### <a name="webhook-sample-in-f"></a>Exemplo de Webhook no F # #
```fsharp
open System.Net
open System.Net.Http
open FSharp.Interop.Dynamic
open Newtonsoft.Json

type Response = {
    body: string
}

let Run(req: HttpRequestMessage, log: TraceWriter) =
    async {
        let! content = req.Content.ReadAsStringAsync() |> Async.AwaitTask
        let data = content |> JsonConvert.DeserializeObject
        log.Info(sprintf "GitHub WebHook triggered! %s" data?comment?body)
        return req.CreateResponse(
            HttpStatusCode.OK,
            { body = sprintf "New GitHub comment: %s" data?comment?body })
    } |> Async.StartAsTask
```

<a name="hooktriggernodejs"></a>

### <a name="webhook-sample-in-nodejs"></a>Exemplo de Webhook no Node.JS
```javascript
module.exports = function (context, data) {
    context.log('GitHub WebHook triggered!', data.comment.body);
    context.res = { body: 'New GitHub comment: ' + data.comment.body };
    context.done();
};
```


## <a name="next-steps"></a>Passos seguintes
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

