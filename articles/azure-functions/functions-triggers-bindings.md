---
title: "aaaWork com acionadores e enlaces de funções do Azure | Microsoft Docs"
description: "Saiba como toouse aciona e os enlaces de funções do Azure tooconnect os eventos de tooonline de execução de código e os serviços baseados na nuvem."
services: functions
documentationcenter: na
author: lindydonna
manager: erikre
editor: 
tags: 
keywords: "funções do azure, funções, processamento de eventos, webhooks, computação dinâmica, arquitetura sem servidor"
ms.assetid: cbc7460a-4d8a-423f-a63e-1cd33fef7252
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/30/2017
ms.author: donnam
ms.openlocfilehash: eb2ebfca172fcc8c0f479adbcfec99e90fc33615
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-triggers-and-bindings-concepts"></a><span data-ttu-id="0e847-104">Conceitos de enlaces e acionadores de funções do Azure</span><span class="sxs-lookup"><span data-stu-id="0e847-104">Azure Functions triggers and bindings concepts</span></span>
<span data-ttu-id="0e847-105">As funções do Azure permite-lhe toowrite código na resposta tooevents no Azure e outros serviços, através de *acionadores* e *enlaces*.</span><span class="sxs-lookup"><span data-stu-id="0e847-105">Azure Functions allows you toowrite code in response tooevents in Azure and other services, through *triggers* and *bindings*.</span></span> <span data-ttu-id="0e847-106">Este artigo é uma descrição geral conceptual dos acionadores e enlaces para todos os suportados linguagens de programação.</span><span class="sxs-lookup"><span data-stu-id="0e847-106">This article is a conceptual overview of triggers and bindings for all supported programming languages.</span></span> <span data-ttu-id="0e847-107">As funcionalidades que são comuns tooall enlaces são descritas aqui.</span><span class="sxs-lookup"><span data-stu-id="0e847-107">Features that are common tooall bindings are described here.</span></span>

## <a name="overview"></a><span data-ttu-id="0e847-108">Descrição geral</span><span class="sxs-lookup"><span data-stu-id="0e847-108">Overview</span></span>

<span data-ttu-id="0e847-109">Acionadores e enlaces são uma forma declarativa toodefine como uma função é invocada e os dados que funciona com.</span><span class="sxs-lookup"><span data-stu-id="0e847-109">Triggers and bindings are a declarative way toodefine how a function is invoked and what data it works with.</span></span> <span data-ttu-id="0e847-110">A *acionador* define a forma como uma função é invocada.</span><span class="sxs-lookup"><span data-stu-id="0e847-110">A *trigger* defines how a function is invoked.</span></span> <span data-ttu-id="0e847-111">Uma função tem de ter exatamente um acionador.</span><span class="sxs-lookup"><span data-stu-id="0e847-111">A function must have exactly one trigger.</span></span> <span data-ttu-id="0e847-112">Acionadores associou dados, o que é normalmente payload Olá que acionou a função de Olá.</span><span class="sxs-lookup"><span data-stu-id="0e847-112">Triggers have associated data, which is usually hello payload that triggered hello function.</span></span> 

<span data-ttu-id="0e847-113">Entrada e saída *enlaces* fornecem uma forma declarativa tooconnect toodata de dentro do seu código.</span><span class="sxs-lookup"><span data-stu-id="0e847-113">Input and output *bindings* provide a declarative way tooconnect toodata from within your code.</span></span> <span data-ttu-id="0e847-114">Tootriggers semelhante, especificar as cadeias de ligação e outras propriedades na configuração da função.</span><span class="sxs-lookup"><span data-stu-id="0e847-114">Similar tootriggers, you specify connection strings and other properties in your function configuration.</span></span> <span data-ttu-id="0e847-115">Enlaces são opcionais e uma função pode ter vários de entrada e saída enlaces.</span><span class="sxs-lookup"><span data-stu-id="0e847-115">Bindings are optional and a function can have multiple input and output bindings.</span></span> 

<span data-ttu-id="0e847-116">Utilizar acionadores e enlaces, pode escrever código que é mais genérico e faz a que codifique os detalhes de Olá dos serviços de Olá com a qual interage.</span><span class="sxs-lookup"><span data-stu-id="0e847-116">Using triggers and bindings, you can write code that is more generic and does not hardcode hello details of hello services with which it interacts.</span></span> <span data-ttu-id="0e847-117">Dados provenientes de valores de entrada de serviços simplesmente tornar-se para o seu código de função.</span><span class="sxs-lookup"><span data-stu-id="0e847-117">Data coming from services simply become input values for your function code.</span></span> <span data-ttu-id="0e847-118">serviço de tooanother toooutput data (como criar uma nova linha no Table Storage do Azure), utilize valor de retorno de Olá do método Olá.</span><span class="sxs-lookup"><span data-stu-id="0e847-118">toooutput data tooanother service (such as creating a new row in Azure Table Storage), use hello return value of hello method.</span></span> <span data-ttu-id="0e847-119">Ou, se precisar de toooutput vários valores, utilize um objeto de programa auxiliar.</span><span class="sxs-lookup"><span data-stu-id="0e847-119">Or, if you need toooutput multiple values, use a helper object.</span></span> <span data-ttu-id="0e847-120">Acionadores e enlaces têm um **nome** propriedade, o que é um identificador que utilize o enlace de Olá tooaccess código.</span><span class="sxs-lookup"><span data-stu-id="0e847-120">Triggers and bindings have a **name** property, which is an identifier you use in your code tooaccess hello binding.</span></span>

<span data-ttu-id="0e847-121">Pode configurar acionadores e enlaces na Olá **integrar** separador no portal do Olá das funções do Azure.</span><span class="sxs-lookup"><span data-stu-id="0e847-121">You can configure triggers and bindings in hello **Integrate** tab in hello Azure Functions portal.</span></span> <span data-ttu-id="0e847-122">Em bastidores Olá, Olá IU modifica um ficheiro chamado *function.json* ficheiro no diretório de função Olá.</span><span class="sxs-lookup"><span data-stu-id="0e847-122">Under hello covers, hello UI modifies a file called *function.json* file in hello function directory.</span></span> <span data-ttu-id="0e847-123">Pode editar este ficheiro alterando toohello **editor avançada**.</span><span class="sxs-lookup"><span data-stu-id="0e847-123">You can edit this file by changing toohello **Advanced editor**.</span></span>

<span data-ttu-id="0e847-124">Olá tabela seguinte mostra os acionadores de Olá e enlaces que são suportadas as funções do Azure.</span><span class="sxs-lookup"><span data-stu-id="0e847-124">hello following table shows hello triggers and bindings that are supported with Azure Functions.</span></span> 

[!INCLUDE [Full bindings table](../../includes/functions-bindings.md)]

### <a name="example-queue-trigger-and-table-output-binding"></a><span data-ttu-id="0e847-125">Exemplo: acionador de filas e tabela de saída do enlace</span><span class="sxs-lookup"><span data-stu-id="0e847-125">Example: queue trigger and table output binding</span></span>

<span data-ttu-id="0e847-126">Suponha que pretender toowrite um tooAzure linha nova Table Storage sempre que uma nova mensagem é apresentada no armazenamento de filas do Azure.</span><span class="sxs-lookup"><span data-stu-id="0e847-126">Suppose you want toowrite a new row tooAzure Table Storage whenever a new message appears in Azure Queue Storage.</span></span> <span data-ttu-id="0e847-127">Este cenário pode ser implementado através de uma fila do Azure acionador e uma tabela de saída do enlace.</span><span class="sxs-lookup"><span data-stu-id="0e847-127">This scenario can be implemented using an Azure Queue trigger and a Table output binding.</span></span> 

<span data-ttu-id="0e847-128">Necessita de um acionador de fila Olá seguindo as informações no Olá **integrar** separador:</span><span class="sxs-lookup"><span data-stu-id="0e847-128">A queue trigger requires hello following information in hello **Integrate** tab:</span></span>

* <span data-ttu-id="0e847-129">nome de Olá da definição de aplicação Olá que contém a cadeia da ligação de conta de armazenamento de Olá para a fila de Olá</span><span class="sxs-lookup"><span data-stu-id="0e847-129">hello name of hello app setting that contains hello storage account connection string for hello queue</span></span>
* <span data-ttu-id="0e847-130">nome da fila Olá</span><span class="sxs-lookup"><span data-stu-id="0e847-130">hello queue name</span></span>
* <span data-ttu-id="0e847-131">Olá identificador no seu código tooread Olá do conteúdo da mensagem da fila de Olá, tais como `order`.</span><span class="sxs-lookup"><span data-stu-id="0e847-131">hello identifier in your code tooread hello contents of hello queue message, such as `order`.</span></span>

<span data-ttu-id="0e847-132">toowrite tooAzure Table Storage, utilize um enlace de saída com Olá os detalhes:</span><span class="sxs-lookup"><span data-stu-id="0e847-132">toowrite tooAzure Table Storage, use an output binding with hello following details:</span></span>

* <span data-ttu-id="0e847-133">nome de Olá da definição de aplicação Olá que contém a cadeia da ligação de conta de armazenamento de Olá para a tabela de Olá</span><span class="sxs-lookup"><span data-stu-id="0e847-133">hello name of hello app setting that contains hello storage account connection string for hello table</span></span>
* <span data-ttu-id="0e847-134">nome da tabela Olá</span><span class="sxs-lookup"><span data-stu-id="0e847-134">hello table name</span></span>
* <span data-ttu-id="0e847-135">Identificador de Olá no seu toocreate de código de saída itens ou valor de retorno de Olá da função de Olá.</span><span class="sxs-lookup"><span data-stu-id="0e847-135">hello identifier in your code toocreate output items, or hello return value from hello function.</span></span>

<span data-ttu-id="0e847-136">Enlaces de utilizam as definições de aplicação para Olá de tooenforce de cadeias de ligação melhores práticas que *function.json* não contém segredos do serviço.</span><span class="sxs-lookup"><span data-stu-id="0e847-136">Bindings use app settings for connection strings tooenforce hello best practice that *function.json* does not contain service secrets.</span></span>

<span data-ttu-id="0e847-137">Em seguida, utilize identificadores de Olá fornecido toointegrate com armazenamento do Azure no seu código.</span><span class="sxs-lookup"><span data-stu-id="0e847-137">Then, use hello identifiers you provided toointegrate with Azure Storage in your code.</span></span>

```cs
#r "Newtonsoft.Json"

using Newtonsoft.Json.Linq;

// From an incoming queue message that is a JSON object, add fields and write tooTable Storage
// hello method return value creates a new row in Table Storage
public static Person Run(JObject order, TraceWriter log)
{
    return new Person() { 
            PartitionKey = "Orders", 
            RowKey = Guid.NewGuid().ToString(),  
            Name = order["Name"].ToString(),
            MobileNumber = order["MobileNumber"].ToString() };  
}
 
public class Person
{
    public string PartitionKey { get; set; }
    public string RowKey { get; set; }
    public string Name { get; set; }
    public string MobileNumber { get; set; }
}
```

```javascript
// From an incoming queue message that is a JSON object, add fields and write tooTable Storage
// hello second parameter toocontext.done is used as hello value for hello new row
module.exports = function (context, order) {
    order.PartitionKey = "Orders";
    order.RowKey = generateRandomId(); 

    context.done(null, order);
};

function generateRandomId() {
    return Math.random().toString(36).substring(2, 15) +
        Math.random().toString(36).substring(2, 15);
}
```

<span data-ttu-id="0e847-138">Eis Olá *function.json* que corresponde toohello precedente código.</span><span class="sxs-lookup"><span data-stu-id="0e847-138">Here is hello *function.json* that corresponds toohello preceding code.</span></span> <span data-ttu-id="0e847-139">Tenha em atenção que Olá a mesma configuração pode ser utilizada, independentemente do idioma Olá de implementação da função de Olá.</span><span class="sxs-lookup"><span data-stu-id="0e847-139">Note that hello same configuration can be used, regardless of hello language of hello function implementation.</span></span>

```json
{
  "bindings": [
    {
      "name": "order",
      "type": "queueTrigger",
      "direction": "in",
      "queueName": "myqueue-items",
      "connection": "MY_STORAGE_ACCT_APP_SETTING"
    },
    {
      "name": "$return",
      "type": "table",
      "direction": "out",
      "tableName": "outTable",
      "connection": "MY_TABLE_STORAGE_ACCT_APP_SETTING"
    }
  ]
}
```
<span data-ttu-id="0e847-140">tooview e editar Olá conteúdo *function.json* no portal do Azure Olá, clique em Olá **editor avançada** opção no Olá **integrar** separador da sua função.</span><span class="sxs-lookup"><span data-stu-id="0e847-140">tooview and edit hello contents of *function.json* in hello Azure portal, click hello **Advanced editor** option on hello **Integrate** tab of your function.</span></span>

<span data-ttu-id="0e847-141">Para obter mais exemplos de código e detalhes sobre a integração com o Storage do Azure, consulte [acionadores de funções do Azure e vínculos para armazenamento do Azure](functions-bindings-storage.md).</span><span class="sxs-lookup"><span data-stu-id="0e847-141">For more code examples and details on integrating with Azure Storage, see [Azure Functions triggers and bindings for Azure Storage](functions-bindings-storage.md).</span></span>

### <a name="binding-direction"></a><span data-ttu-id="0e847-142">Direção de enlace</span><span class="sxs-lookup"><span data-stu-id="0e847-142">Binding direction</span></span>

<span data-ttu-id="0e847-143">Todos os acionadores e enlaces de tem um `direction` propriedade:</span><span class="sxs-lookup"><span data-stu-id="0e847-143">All triggers and bindings have a `direction` property:</span></span>

- <span data-ttu-id="0e847-144">Para acionadores, a direção de Olá é sempre`in`</span><span class="sxs-lookup"><span data-stu-id="0e847-144">For triggers, hello direction is always `in`</span></span>
- <span data-ttu-id="0e847-145">Utilizam enlaces de entrada e de saída `in` e`out`</span><span class="sxs-lookup"><span data-stu-id="0e847-145">Input and output bindings use `in` and `out`</span></span>
- <span data-ttu-id="0e847-146">Alguns enlaces suportam uma direção especial `inout`.</span><span class="sxs-lookup"><span data-stu-id="0e847-146">Some bindings support a special direction `inout`.</span></span> <span data-ttu-id="0e847-147">Se utilizar `inout`, apenas Olá **editor avançada** está disponível no Olá **integrar** separador.</span><span class="sxs-lookup"><span data-stu-id="0e847-147">If you use `inout`, only hello **Advanced editor** is available in hello **Integrate** tab.</span></span>

## <a name="using-hello-function-return-type-tooreturn-a-single-output"></a><span data-ttu-id="0e847-148">Utilizar Olá função tipo de retorno tooreturn de saída única</span><span class="sxs-lookup"><span data-stu-id="0e847-148">Using hello function return type tooreturn a single output</span></span>

<span data-ttu-id="0e847-149">Olá anterior exemplo mostra como toouse Olá função valor de retorno tooprovide saída tooa enlace, o que é conseguido utilizando o parâmetro de nome especial Olá `$return`.</span><span class="sxs-lookup"><span data-stu-id="0e847-149">hello preceding example shows how toouse hello function return value tooprovide output tooa binding, which is achieved by using hello special name parameter `$return`.</span></span> <span data-ttu-id="0e847-150">(Esta é apenas suportada em idiomas de que tem um valor de retorno, como c#, JavaScript e F #.) Se uma função tem múltiplos enlaces de resultados, utilize `$return` para apenas um dos enlaces de saída Olá.</span><span class="sxs-lookup"><span data-stu-id="0e847-150">(This is only supported in languages that have a return value, such as C#, JavaScript, and F#.) If a function has multiple output bindings, use `$return` for only one of hello output bindings.</span></span> 

```json
// excerpt of function.json
{
    "name": "$return",
    "type": "blob",
    "direction": "out",
    "path": "output-container/{id}"
}
```

<span data-ttu-id="0e847-151">Exemplos de Olá abaixo mostra como devolvem tipos são utilizados com enlaces de saída em c#, JavaScript e F #.</span><span class="sxs-lookup"><span data-stu-id="0e847-151">hello examples below show how return types are used with output bindings in C#, JavaScript, and F#.</span></span>

```cs
// C# example: use method return value for output binding
public static string Run(WorkItem input, TraceWriter log)
{
    string json = string.Format("{{ \"id\": \"{0}\" }}", input.Id);
    log.Info($"C# script processed queue message. Item={json}");
    return json;
}
```

```cs
// C# example: async method, using return value for output binding
public static Task<string> Run(WorkItem input, TraceWriter log)
{
    string json = string.Format("{{ \"id\": \"{0}\" }}", input.Id);
    log.Info($"C# script processed queue message. Item={json}");
    return json;
}
```

```javascript
// JavaScript: return a value in hello second parameter toocontext.done
module.exports = function (context, input) {
    var json = JSON.stringify(input);
    context.log('Node.js script processed queue message', json);
    context.done(null, json);
}
```

```fsharp
// F# example: use return value for output binding
let Run(input: WorkItem, log: TraceWriter) =
    let json = String.Format("{{ \"id\": \"{0}\" }}", input.Id)   
    log.Info(sprintf "F# script processed queue message '%s'" json)
    json
```

## <a name="binding-datatype-property"></a><span data-ttu-id="0e847-152">Propriedade de tipo de dados de enlace</span><span class="sxs-lookup"><span data-stu-id="0e847-152">Binding dataType property</span></span>

<span data-ttu-id="0e847-153">No .NET, utilize o tipo de dados do Olá tipos toodefine Olá para dados de entrada.</span><span class="sxs-lookup"><span data-stu-id="0e847-153">In .NET, use hello types toodefine hello data type for input data.</span></span> <span data-ttu-id="0e847-154">Por exemplo, utilize `string` toobind toohello texto de um acionador de fila e um tooread de matriz de bytes como binário.</span><span class="sxs-lookup"><span data-stu-id="0e847-154">For instance, use `string` toobind toohello text of a queue trigger and a byte array tooread as binary.</span></span>

<span data-ttu-id="0e847-155">Para os idiomas que são escritos dinamicamente, como JavaScript, utilize Olá `dataType` propriedade na definição de enlace Olá.</span><span class="sxs-lookup"><span data-stu-id="0e847-155">For languages that are dynamically typed such as JavaScript, use hello `dataType` property in hello binding definition.</span></span> <span data-ttu-id="0e847-156">Por exemplo, tooread Olá conteúdo de um pedido HTTP no formato binário, utilize o tipo de Olá `binary`:</span><span class="sxs-lookup"><span data-stu-id="0e847-156">For example, tooread hello content of an HTTP request in binary format, use hello type `binary`:</span></span>

```json
{
    "type": "httpTrigger",
    "name": "req",
    "direction": "in",
    "dataType": "binary"
}
```

<span data-ttu-id="0e847-157">Outras opções para `dataType` são `stream` e `string`.</span><span class="sxs-lookup"><span data-stu-id="0e847-157">Other options for `dataType` are `stream` and `string`.</span></span>

## <a name="resolving-app-settings"></a><span data-ttu-id="0e847-158">Resolver as definições de aplicação</span><span class="sxs-lookup"><span data-stu-id="0e847-158">Resolving app settings</span></span>
<span data-ttu-id="0e847-159">Como melhor prática, os segredos e cadeias de ligação devem ser geridas utilizando as definições de aplicação, em vez de ficheiros de configuração.</span><span class="sxs-lookup"><span data-stu-id="0e847-159">As a best practice, secrets and connection strings should be managed using app settings, rather than configuration files.</span></span> <span data-ttu-id="0e847-160">Isto limita o acesso toothese segredos e torna toostore seguro *function.json* num repositório de controlo de origem público.</span><span class="sxs-lookup"><span data-stu-id="0e847-160">This limits access toothese secrets and makes it safe toostore *function.json* in a public source control repository.</span></span>

<span data-ttu-id="0e847-161">As definições de aplicações também são úteis sempre que pretender configuração toochange com base no ambiente de Olá.</span><span class="sxs-lookup"><span data-stu-id="0e847-161">App settings are also useful whenever you want toochange configuration based on hello environment.</span></span> <span data-ttu-id="0e847-162">Por exemplo, num ambiente de teste, poderá ser útil toomonitor um contentor de armazenamento de fila ou blob diferente.</span><span class="sxs-lookup"><span data-stu-id="0e847-162">For example, in a test environment, you may want toomonitor a different queue or blob storage container.</span></span>

<span data-ttu-id="0e847-163">São resolvidas as definições de aplicação sempre que um valor está entre símbolos de percentagem inicia, tais como `%MyAppSetting%`.</span><span class="sxs-lookup"><span data-stu-id="0e847-163">App settings are resolved whenever a value is enclosed in percent signs, such as `%MyAppSetting%`.</span></span> <span data-ttu-id="0e847-164">Tenha em atenção que Olá `connection` propriedade de acionadores e enlaces é num caso especial e resolve automaticamente os valores das definições de aplicação.</span><span class="sxs-lookup"><span data-stu-id="0e847-164">Note that hello `connection` property of triggers and bindings is a special case and automatically resolves values as app settings.</span></span> 

<span data-ttu-id="0e847-165">Olá exemplo seguinte é um acionador de fila que utiliza uma definição de aplicação `%input-queue-name%` toodefine Olá fila tootrigger no.</span><span class="sxs-lookup"><span data-stu-id="0e847-165">hello following example is a queue trigger that uses an app setting `%input-queue-name%` toodefine hello queue tootrigger on.</span></span>

```json
{
  "bindings": [
    {
      "name": "order",
      "type": "queueTrigger",
      "direction": "in",
      "queueName": "%input-queue-name%",
      "connection": "MY_STORAGE_ACCT_APP_SETTING"
    }
  ]
}
```

## <a name="trigger-metadata-properties"></a><span data-ttu-id="0e847-166">Propriedades de metadados do acionador</span><span class="sxs-lookup"><span data-stu-id="0e847-166">Trigger metadata properties</span></span>

<span data-ttu-id="0e847-167">Payload de dados do toohello de adição fornecido por um acionador (por exemplo, a mensagem da fila de saudação que acionou uma função), acionadores muitos fornecem valores de metadados adicionais.</span><span class="sxs-lookup"><span data-stu-id="0e847-167">In addition toohello data payload provided by a trigger (such as hello queue message that triggered a function), many triggers provide additional metadata values.</span></span> <span data-ttu-id="0e847-168">Estes valores podem ser utilizados como parâmetros de entrada em c# e F # ou as propriedades de Olá `context.bindings` objeto em JavaScript.</span><span class="sxs-lookup"><span data-stu-id="0e847-168">These values can be used as input parameters in C# and F# or properties on hello `context.bindings` object in JavaScript.</span></span> 

<span data-ttu-id="0e847-169">Por exemplo, um acionador de fila suporta Olá seguintes propriedades:</span><span class="sxs-lookup"><span data-stu-id="0e847-169">For example, a queue trigger supports hello following properties:</span></span>

* <span data-ttu-id="0e847-170">QueueTrigger - acionar o conteúdo da mensagem se uma cadeia válida</span><span class="sxs-lookup"><span data-stu-id="0e847-170">QueueTrigger - triggering message content if a valid string</span></span>
* <span data-ttu-id="0e847-171">DequeueCount</span><span class="sxs-lookup"><span data-stu-id="0e847-171">DequeueCount</span></span>
* <span data-ttu-id="0e847-172">expirationTime</span><span class="sxs-lookup"><span data-stu-id="0e847-172">ExpirationTime</span></span>
* <span data-ttu-id="0e847-173">Id</span><span class="sxs-lookup"><span data-stu-id="0e847-173">Id</span></span>
* <span data-ttu-id="0e847-174">InsertionTime</span><span class="sxs-lookup"><span data-stu-id="0e847-174">InsertionTime</span></span>
* <span data-ttu-id="0e847-175">NextVisibleTime</span><span class="sxs-lookup"><span data-stu-id="0e847-175">NextVisibleTime</span></span>
* <span data-ttu-id="0e847-176">PopReceipt</span><span class="sxs-lookup"><span data-stu-id="0e847-176">PopReceipt</span></span>

<span data-ttu-id="0e847-177">Detalhes das propriedades de metadados para cada acionador são descritos no tópico de referência Olá correspondente.</span><span class="sxs-lookup"><span data-stu-id="0e847-177">Details of metadata properties for each trigger are described in hello corresponding reference topic.</span></span> <span data-ttu-id="0e847-178">Documentação também está disponível no Olá **integrar** separador do portal de Olá, no Olá **documentação** secção abaixo área de configuração de enlace Olá.</span><span class="sxs-lookup"><span data-stu-id="0e847-178">Documentation is also available in hello **Integrate** tab of hello portal, in hello **Documentation** section below hello binding configuration area.</span></span>  

<span data-ttu-id="0e847-179">Por exemplo, uma vez que os acionadores de blob têm alguns atrasos, pode utilizar um toorun de Acionador de fila a função (consulte [acionador de armazenamento de BLOBs](functions-bindings-storage-blob.md#storage-blob-trigger).</span><span class="sxs-lookup"><span data-stu-id="0e847-179">For example, since blob triggers have some delays, you can use a queue trigger toorun your function (see [Blob Storage Trigger](functions-bindings-storage-blob.md#storage-blob-trigger).</span></span> <span data-ttu-id="0e847-180">mensagem de fila de saudação iria conter Olá blob filename tootrigger no.</span><span class="sxs-lookup"><span data-stu-id="0e847-180">hello queue message would contain hello blob filename tootrigger on.</span></span> <span data-ttu-id="0e847-181">Utilizar Olá `queueTrigger` propriedade de metadados, pode especificar este comportamento todos na sua configuração, em vez de código.</span><span class="sxs-lookup"><span data-stu-id="0e847-181">Using hello `queueTrigger` metadata property, you can specify this behavior all in your configuration, rather than your code.</span></span>

```json
  "bindings": [
    {
      "name": "myQueueItem",
      "type": "queueTrigger",
      "queueName": "myqueue-items",
      "connection": "MyStorageConnection",
    },
    {
      "name": "myInputBlob",
      "type": "blob",
      "path": "samples-workitems/{queueTrigger}",
      "direction": "in",
      "connection": "MyStorageConnection"
    }
  ]
```

<span data-ttu-id="0e847-182">Propriedades de metadados de um acionador também podem ser utilizadas num *expressão de enlace* para outro enlace, como Olá descrito na secção a seguir.</span><span class="sxs-lookup"><span data-stu-id="0e847-182">Metadata properties from a trigger can also be used in a *binding expression* for another binding, as described in hello following section.</span></span>

## <a name="binding-expressions-and-patterns"></a><span data-ttu-id="0e847-183">Expressões de enlace e padrões</span><span class="sxs-lookup"><span data-stu-id="0e847-183">Binding expressions and patterns</span></span>

<span data-ttu-id="0e847-184">Uma das funcionalidades mais poderosas do Olá de acionadores e enlaces é *expressões de enlace*.</span><span class="sxs-lookup"><span data-stu-id="0e847-184">One of hello most powerful features of triggers and bindings is *binding expressions*.</span></span> <span data-ttu-id="0e847-185">No seu enlace, pode definir as expressões de padrão que, em seguida, podem ser utilizadas noutros enlaces ou o seu código.</span><span class="sxs-lookup"><span data-stu-id="0e847-185">Within your binding, you can define pattern expressions which can then be used in other bindings or your code.</span></span> <span data-ttu-id="0e847-186">Também podem ser utilizado o acionador metadados no enlace expressões, como a mostrar no exemplo de Olá no Olá anterior a secção.</span><span class="sxs-lookup"><span data-stu-id="0e847-186">Trigger metadata can also be used in binding expressions, as show in hello sample in hello preceding section.</span></span>

<span data-ttu-id="0e847-187">Por exemplo, suponha que pretende tooresize imagens no contentor de armazenamento de blob específico, toohello semelhante **imagem Resizer** modelo no Olá **nova função** página.</span><span class="sxs-lookup"><span data-stu-id="0e847-187">For example, suppose you want tooresize images in particular blob storage container, similar toohello **Image Resizer** template in hello **New Function** page.</span></span> <span data-ttu-id="0e847-188">Aceda demasiado**nova função** -> idioma **c#** -> cenário **amostras** -> **ImageResizer CSharp**.</span><span class="sxs-lookup"><span data-stu-id="0e847-188">Go too**New Function** -> Language **C#** -> Scenario **Samples** -> **ImageResizer-CSharp**.</span></span> 

<span data-ttu-id="0e847-189">Eis Olá *function.json* definição:</span><span class="sxs-lookup"><span data-stu-id="0e847-189">Here is hello *function.json* definition:</span></span>

```json
{
  "bindings": [
    {
      "name": "image",
      "type": "blobTrigger",
      "path": "sample-images/{filename}",
      "direction": "in",
      "connection": "MyStorageConnection"
    },
    {
      "name": "imageSmall",
      "type": "blob",
      "path": "sample-images-sm/{filename}",
      "direction": "out",
      "connection": "MyStorageConnection"
    }
  ],
}
```

<span data-ttu-id="0e847-190">Tenha em atenção que Olá `filename` parâmetro é utilizado de definição do acionador de blob Olá, bem como blob Olá vínculo de saída.</span><span class="sxs-lookup"><span data-stu-id="0e847-190">Notice that hello `filename` parameter is used in both hello blob trigger definition as well as hello blob output binding.</span></span> <span data-ttu-id="0e847-191">Este parâmetro também pode ser utilizado no código da função.</span><span class="sxs-lookup"><span data-stu-id="0e847-191">This parameter can also be used in function code.</span></span>

```csharp
// C# example of binding too{filename}
public static void Run(Stream image, string filename, Stream imageSmall, TraceWriter log)  
{
    log.Info($"Blob trigger processing: {filename}");
    // ...
} 
```

<!--TODO: add JavaScript example -->
<!-- Blocked by bug https://github.com/Azure/Azure-Functions/issues/248 -->


### <a name="random-guids"></a><span data-ttu-id="0e847-192">GUIDs aleatórios</span><span class="sxs-lookup"><span data-stu-id="0e847-192">Random GUIDs</span></span>
<span data-ttu-id="0e847-193">As funções do Azure fornece uma sintaxe de conveniência para gerar GUIDs dos enlaces, através de Olá `{rand-guid}` expressão de enlace.</span><span class="sxs-lookup"><span data-stu-id="0e847-193">Azure Functions provides a convenience syntax for generating GUIDs in your bindings, through hello `{rand-guid}` binding expression.</span></span> <span data-ttu-id="0e847-194">Olá exemplo seguinte utiliza este toogenerate um nome exclusivo de blob:</span><span class="sxs-lookup"><span data-stu-id="0e847-194">hello following example uses this toogenerate a unique blob name:</span></span> 

```json
{
  "type": "blob",
  "name": "blobOutput",
  "direction": "out",
  "path": "my-output-container/{rand-guid}"
}
```

### <a name="current-time"></a><span data-ttu-id="0e847-195">Hora atual</span><span class="sxs-lookup"><span data-stu-id="0e847-195">Current time</span></span>

<span data-ttu-id="0e847-196">Pode utilizar a expressão de enlace Olá `DateTime`, que resolve demasiado`DateTime.UtcNow`.</span><span class="sxs-lookup"><span data-stu-id="0e847-196">You can use hello binding expression `DateTime`, which resolves too`DateTime.UtcNow`.</span></span>

```json
{
  "type": "blob",
  "name": "blobOutput",
  "direction": "out",
  "path": "my-output-container/{DateTime}"
}
```

## <a name="bind-toocustom-input-properties-in-a-binding-expression"></a><span data-ttu-id="0e847-197">Vincular as propriedades de entrada de toocustom numa expressão de enlace</span><span class="sxs-lookup"><span data-stu-id="0e847-197">Bind toocustom input properties in a binding expression</span></span>

<span data-ttu-id="0e847-198">Expressões de enlace também podem referenciar propriedades que são definidas no payload de Acionador de Olá próprio.</span><span class="sxs-lookup"><span data-stu-id="0e847-198">Binding expressions can also reference properties that are defined in hello trigger payload itself.</span></span> <span data-ttu-id="0e847-199">Por exemplo, poderá ser útil o ficheiro de armazenamento do BLOBs do toodynamically enlace tooa de um nome de ficheiro fornecido num webhook.</span><span class="sxs-lookup"><span data-stu-id="0e847-199">For example, you may want toodynamically bind tooa blob storage file from a filename provided in a webhook.</span></span>

<span data-ttu-id="0e847-200">Por exemplo, Olá seguir *function.json* utiliza uma propriedade denominada `BlobName` do payload de Acionador de Olá:</span><span class="sxs-lookup"><span data-stu-id="0e847-200">For example, hello following *function.json* uses a property called `BlobName` from hello trigger payload:</span></span>

```json
{
  "bindings": [
    {
      "name": "info",
      "type": "httpTrigger",
      "direction": "in",
      "webHookType": "genericJson",
    },
    {
      "name": "blobContents",
      "type": "blob",
      "direction": "in",
      "path": "strings/{BlobName}",
      "connection": "AzureWebJobsStorage"
    },
    {
      "name": "res",
      "type": "http",
      "direction": "out"
    }
  ]
}
```

<span data-ttu-id="0e847-201">tooaccomplish este em c# e F #, tem de definir um POCO que define os campos de Olá cuja serialização irão ser anulados no payload de Acionador de Olá.</span><span class="sxs-lookup"><span data-stu-id="0e847-201">tooaccomplish this in C# and F#, you must define a POCO that defines hello fields that will be deserialized in hello trigger payload.</span></span>

```csharp
using System.Net;

public class BlobInfo
{
    public string BlobName { get; set; }
}
  
public static HttpResponseMessage Run(HttpRequestMessage req, BlobInfo info, string blobContents)
{
    if (blobContents == null) {
        return req.CreateResponse(HttpStatusCode.NotFound);
    } 

    return req.CreateResponse(HttpStatusCode.OK, new {
        data = $"{blobContents}"
    });
}
```

<span data-ttu-id="0e847-202">Em JavaScript, a desserialização de JSON é automaticamente executada e pode utilizar propriedades de Olá diretamente.</span><span class="sxs-lookup"><span data-stu-id="0e847-202">In JavaScript, JSON deserialization is automatically performed and you can use hello properties directly.</span></span>

```javascript
module.exports = function (context, info) {
    if ('BlobName' in info) {
        context.res = {
            body: { 'data': context.bindings.blobContents }
        }
    }
    else {
        context.res = {
            status: 404
        };
    }
    context.done();
}
```

## <a name="configuring-binding-data-at-runtime"></a><span data-ttu-id="0e847-203">Configuração de enlace de dados em tempo de execução</span><span class="sxs-lookup"><span data-stu-id="0e847-203">Configuring binding data at runtime</span></span>

<span data-ttu-id="0e847-204">Em c# e outras linguagens .NET, pode utilizar um padrão de enlace imperativo, como toohello oposição ao enlaces declarativa no *function.json*.</span><span class="sxs-lookup"><span data-stu-id="0e847-204">In C# and other .NET languages, you can use an imperative binding pattern, as opposed toohello declarative bindings in *function.json*.</span></span> <span data-ttu-id="0e847-205">Enlace imperativo é útil se precisam de parâmetros de enlace toobe calculada ao tempo de tempo de execução, em vez de design.</span><span class="sxs-lookup"><span data-stu-id="0e847-205">Imperative binding is useful when binding parameters need toobe computed at runtime rather than design time.</span></span> <span data-ttu-id="0e847-206">toolearn mais, consulte [enlace no tempo de execução através dos enlaces imperativo](functions-reference-csharp.md#imperative-bindings) numa referência de programador Olá c#.</span><span class="sxs-lookup"><span data-stu-id="0e847-206">toolearn more, see [Binding at runtime via imperative bindings](functions-reference-csharp.md#imperative-bindings) in hello C# developer reference.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0e847-207">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="0e847-207">Next steps</span></span>
<span data-ttu-id="0e847-208">Para obter mais informações sobre um enlace específico, consulte Olá seguintes artigos:</span><span class="sxs-lookup"><span data-stu-id="0e847-208">For more information on a specific binding, see hello following articles:</span></span>

- [<span data-ttu-id="0e847-209">HTTP e webhooks</span><span class="sxs-lookup"><span data-stu-id="0e847-209">HTTP and webhooks</span></span>](functions-bindings-http-webhook.md)
- [<span data-ttu-id="0e847-210">Temporizador</span><span class="sxs-lookup"><span data-stu-id="0e847-210">Timer</span></span>](functions-bindings-timer.md)
- [<span data-ttu-id="0e847-211">Armazenamento de filas</span><span class="sxs-lookup"><span data-stu-id="0e847-211">Queue storage</span></span>](functions-bindings-storage-queue.md)
- [<span data-ttu-id="0e847-212">Armazenamento de blobs</span><span class="sxs-lookup"><span data-stu-id="0e847-212">Blob storage</span></span>](functions-bindings-storage-blob.md)
- [<span data-ttu-id="0e847-213">Armazenamento de tabelas</span><span class="sxs-lookup"><span data-stu-id="0e847-213">Table storage</span></span>](functions-bindings-storage-table.md)
- [<span data-ttu-id="0e847-214">Hub de Eventos</span><span class="sxs-lookup"><span data-stu-id="0e847-214">Event Hub</span></span>](functions-bindings-event-hubs.md)
- [<span data-ttu-id="0e847-215">Service Bus</span><span class="sxs-lookup"><span data-stu-id="0e847-215">Service Bus</span></span>](functions-bindings-service-bus.md)
- [<span data-ttu-id="0e847-216">BD do Cosmos</span><span class="sxs-lookup"><span data-stu-id="0e847-216">Cosmos DB</span></span>](functions-bindings-documentdb.md)
- [<span data-ttu-id="0e847-217">SendGrid</span><span class="sxs-lookup"><span data-stu-id="0e847-217">SendGrid</span></span>](functions-bindings-sendgrid.md)
- [<span data-ttu-id="0e847-218">Twilio</span><span class="sxs-lookup"><span data-stu-id="0e847-218">Twilio</span></span>](functions-bindings-twilio.md)
- [<span data-ttu-id="0e847-219">Hubs de Notificação</span><span class="sxs-lookup"><span data-stu-id="0e847-219">Notification Hubs</span></span>](functions-bindings-notification-hubs.md)
- [<span data-ttu-id="0e847-220">Aplicações Móveis</span><span class="sxs-lookup"><span data-stu-id="0e847-220">Mobile Apps</span></span>](functions-bindings-mobile-apps.md)
- [<span data-ttu-id="0e847-221">Ficheiro externo</span><span class="sxs-lookup"><span data-stu-id="0e847-221">External file</span></span>](functions-bindings-external-file.md)
