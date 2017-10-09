---
title: "aaaHow toouse armazenamento de filas do Azure com Olá SDK de WebJobs"
description: "Saiba como toouse Azure fila de armazenamento com Olá SDK de WebJobs. Criar e eliminar filas; Inserir, observar, obter e eliminar a fila de mensagens e muito mais."
services: app-service\web, storage
documentationcenter: .net
author: ggailey777
manager: erikre
editor: jimbe
ms.assetid: dbfac5d9-f4a0-4e3e-9ecc-af3d7bf80463
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 06/01/2016
ms.author: glenga
ms.openlocfilehash: 49f844436b0453489800b2762a5c7dc30b9db805
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-queue-storage-with-hello-webjobs-sdk"></a><span data-ttu-id="8b794-104">Como toouse Azure fila de armazenamento com Olá SDK de WebJobs</span><span class="sxs-lookup"><span data-stu-id="8b794-104">How toouse Azure queue storage with hello WebJobs SDK</span></span>
## <a name="overview"></a><span data-ttu-id="8b794-105">Descrição geral</span><span class="sxs-lookup"><span data-stu-id="8b794-105">Overview</span></span>
<span data-ttu-id="8b794-106">Este guia fornece c# exemplos de código que mostram como toouse Olá versão do SDK de WebJobs do Azure 1. x com Olá serviço de armazenamento de filas do Azure.</span><span class="sxs-lookup"><span data-stu-id="8b794-106">This guide provides C# code samples that show how toouse hello Azure WebJobs SDK version 1.x with hello Azure queue storage service.</span></span>

<span data-ttu-id="8b794-107">Guia de Olá parte do princípio de que sabe [como toocreate um projeto do trabalho Web no Visual Studio com ligação cadeias essa conta do storage ponto tooyour](websites-dotnet-webjobs-sdk-get-started.md) ou demasiado[várias contas do storage](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs).</span><span class="sxs-lookup"><span data-stu-id="8b794-107">hello guide assumes you know [how toocreate a WebJob project in Visual Studio with connection strings that point tooyour storage account](websites-dotnet-webjobs-sdk-get-started.md) or too[multiple storage accounts](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs).</span></span>

<span data-ttu-id="8b794-108">Na maioria das fragmentos de código Olá mostra apenas as funções, não Olá código que cria Olá `JobHost` objeto tal como neste exemplo:</span><span class="sxs-lookup"><span data-stu-id="8b794-108">Most of hello code snippets only show functions, not hello code that creates hello `JobHost` object as in this example:</span></span>

        static void Main(string[] args)
        {
            JobHost host = new JobHost();
            host.RunAndBlock();
        }

<span data-ttu-id="8b794-109">Guia de Olá inclui Olá os seguintes tópicos:</span><span class="sxs-lookup"><span data-stu-id="8b794-109">hello guide includes hello following topics:</span></span>

* [<span data-ttu-id="8b794-110">Como tootrigger uma função quando é recebida uma mensagem de fila</span><span class="sxs-lookup"><span data-stu-id="8b794-110">How tootrigger a function when a queue message is received</span></span>](#trigger)
  * <span data-ttu-id="8b794-111">Mensagens de filas de cadeia</span><span class="sxs-lookup"><span data-stu-id="8b794-111">String queue messages</span></span>
  * <span data-ttu-id="8b794-112">Mensagens de filas POCO</span><span class="sxs-lookup"><span data-stu-id="8b794-112">POCO queue messages</span></span>
  * <span data-ttu-id="8b794-113">Async funções</span><span class="sxs-lookup"><span data-stu-id="8b794-113">Async functions</span></span>
  * <span data-ttu-id="8b794-114">Atributo de QueueTrigger tipos Olá funciona com o</span><span class="sxs-lookup"><span data-stu-id="8b794-114">Types hello QueueTrigger attribute works with</span></span>
  * <span data-ttu-id="8b794-115">Algoritmo de consulta</span><span class="sxs-lookup"><span data-stu-id="8b794-115">Polling algorithm</span></span>
  * <span data-ttu-id="8b794-116">Várias instâncias</span><span class="sxs-lookup"><span data-stu-id="8b794-116">Multiple instances</span></span>
  * <span data-ttu-id="8b794-117">Execução paralela</span><span class="sxs-lookup"><span data-stu-id="8b794-117">Parallel execution</span></span>
  * <span data-ttu-id="8b794-118">Obter a fila ou metadados de mensagem de fila</span><span class="sxs-lookup"><span data-stu-id="8b794-118">Get queue or queue message metadata</span></span>
  * <span data-ttu-id="8b794-119">Encerramento correto</span><span class="sxs-lookup"><span data-stu-id="8b794-119">Graceful shutdown</span></span>
* [<span data-ttu-id="8b794-120">Como toocreate uma fila de mensagens ao processar uma mensagem de fila</span><span class="sxs-lookup"><span data-stu-id="8b794-120">How toocreate a queue message while processing a queue message</span></span>](#createqueue)
  * <span data-ttu-id="8b794-121">Mensagens de filas de cadeia</span><span class="sxs-lookup"><span data-stu-id="8b794-121">String queue messages</span></span>
  * <span data-ttu-id="8b794-122">Mensagens de filas POCO</span><span class="sxs-lookup"><span data-stu-id="8b794-122">POCO queue messages</span></span>
  * <span data-ttu-id="8b794-123">Criar várias mensagens ou nas funções de assíncrona</span><span class="sxs-lookup"><span data-stu-id="8b794-123">Create multiple messages or in async functions</span></span>
  * <span data-ttu-id="8b794-124">Atributo de fila de Olá tipos funciona com o</span><span class="sxs-lookup"><span data-stu-id="8b794-124">Types hello Queue attribute works with</span></span>
  * <span data-ttu-id="8b794-125">Utilizar o SDK de WebJobs atributos no corpo de Olá de uma função</span><span class="sxs-lookup"><span data-stu-id="8b794-125">Use WebJobs SDK attributes in hello body of a function</span></span>
* [<span data-ttu-id="8b794-126">Como tooread e de escrita de blobs ao processar uma mensagem de fila</span><span class="sxs-lookup"><span data-stu-id="8b794-126">How tooread and write blobs while processing a queue message</span></span>](#blobs)
  * <span data-ttu-id="8b794-127">Mensagens de filas de cadeia</span><span class="sxs-lookup"><span data-stu-id="8b794-127">String queue messages</span></span>
  * <span data-ttu-id="8b794-128">Mensagens de filas POCO</span><span class="sxs-lookup"><span data-stu-id="8b794-128">POCO queue messages</span></span>
  * <span data-ttu-id="8b794-129">Atributo de Blob tipos Olá funciona com o</span><span class="sxs-lookup"><span data-stu-id="8b794-129">Types hello Blob attribute works with</span></span>
* [<span data-ttu-id="8b794-130">Como toohandle poison mensagens</span><span class="sxs-lookup"><span data-stu-id="8b794-130">How toohandle poison messages</span></span>](#poison)
  * <span data-ttu-id="8b794-131">Processamento de mensagens nocivas automática</span><span class="sxs-lookup"><span data-stu-id="8b794-131">Automatic poison message handling</span></span>
  * <span data-ttu-id="8b794-132">Processamento de mensagens nocivas manual</span><span class="sxs-lookup"><span data-stu-id="8b794-132">Manual poison message handling</span></span>
* [<span data-ttu-id="8b794-133">Como tooset opções de configuração</span><span class="sxs-lookup"><span data-stu-id="8b794-133">How tooset configuration options</span></span>](#config)
  * <span data-ttu-id="8b794-134">Definir cadeias de ligação do SDK no código</span><span class="sxs-lookup"><span data-stu-id="8b794-134">Set SDK connection strings in code</span></span>
  * <span data-ttu-id="8b794-135">Configurar definições de QueueTrigger</span><span class="sxs-lookup"><span data-stu-id="8b794-135">Configure QueueTrigger settings</span></span>
  * <span data-ttu-id="8b794-136">Definir valores para o SDK de WebJobs os parâmetros do construtor no código</span><span class="sxs-lookup"><span data-stu-id="8b794-136">Set values for WebJobs SDK constructor parameters in code</span></span>
* [<span data-ttu-id="8b794-137">Como uma função de tootrigger manualmente</span><span class="sxs-lookup"><span data-stu-id="8b794-137">How tootrigger a function manually</span></span>](#manual)
* [<span data-ttu-id="8b794-138">Modo de registo de toowrite</span><span class="sxs-lookup"><span data-stu-id="8b794-138">How toowrite logs</span></span>](#logs)
* [<span data-ttu-id="8b794-139">Como toohandle erros e configurar os tempos limite</span><span class="sxs-lookup"><span data-stu-id="8b794-139">How toohandle errors and configure timeouts</span></span>](#errors)
* [<span data-ttu-id="8b794-140">Passos seguintes?</span><span class="sxs-lookup"><span data-stu-id="8b794-140">Next steps</span></span>](#nextsteps)

## <span data-ttu-id="8b794-141"><a id="trigger"></a>Como tootrigger uma função quando é recebida uma mensagem de fila</span><span class="sxs-lookup"><span data-stu-id="8b794-141"><a id="trigger"></a> How tootrigger a function when a queue message is received</span></span>
<span data-ttu-id="8b794-142">chamadas de uma função que Olá SDK de WebJobs toowrite quando é recebida uma mensagem de fila, utilize Olá `QueueTrigger` atributo.</span><span class="sxs-lookup"><span data-stu-id="8b794-142">toowrite a function that hello WebJobs SDK calls when a queue message is received, use hello `QueueTrigger` attribute.</span></span> <span data-ttu-id="8b794-143">o construtor de atributos de Olá assume um parâmetro de cadeia que especifica o nome de Olá de Olá toopoll de fila.</span><span class="sxs-lookup"><span data-stu-id="8b794-143">hello attribute constructor takes a string parameter that specifies hello name of hello queue toopoll.</span></span> <span data-ttu-id="8b794-144">Também pode [definir o nome da fila Olá dinamicamente](#config).</span><span class="sxs-lookup"><span data-stu-id="8b794-144">You can also [set hello queue name dynamically](#config).</span></span>

### <a name="string-queue-messages"></a><span data-ttu-id="8b794-145">Mensagens de filas de cadeia</span><span class="sxs-lookup"><span data-stu-id="8b794-145">String queue messages</span></span>
<span data-ttu-id="8b794-146">No seguinte exemplo de Olá, Olá fila contém uma mensagem de cadeia, por isso, `QueueTrigger` é aplicado tooa parâmetro de cadeia com o nome `logMessage` que contém conteúdo Olá de mensagem de fila de saudação.</span><span class="sxs-lookup"><span data-stu-id="8b794-146">In hello following example, hello queue contains a string message, so `QueueTrigger` is applied tooa string parameter named `logMessage` which contains hello content of hello queue message.</span></span> <span data-ttu-id="8b794-147">Olá função [escreve um toohello de mensagem do registo Dashboard](#logs).</span><span class="sxs-lookup"><span data-stu-id="8b794-147">hello function [writes a log message toohello Dashboard](#logs).</span></span>

        public static void ProcessQueueMessage([QueueTrigger("logqueue")] string logMessage, TextWriter logger)
        {
            logger.WriteLine(logMessage);
        }

<span data-ttu-id="8b794-148">Besides `string`, parâmetro de Olá pode ser uma matriz de bytes, um `CloudQueueMessage` objeto ou um POCO por si.</span><span class="sxs-lookup"><span data-stu-id="8b794-148">Besides `string`, hello parameter may be a byte array, a `CloudQueueMessage` object, or a POCO  that you define.</span></span>

### <a name="poco-plain-old-clr-objecthttpenwikipediaorgwikiplainoldclrobject-queue-messages"></a><span data-ttu-id="8b794-149">POCO [(simples objeto antigo de CLR](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) mensagens da fila</span><span class="sxs-lookup"><span data-stu-id="8b794-149">POCO [(Plain Old CLR Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) queue messages</span></span>
<span data-ttu-id="8b794-150">No seguinte exemplo de Olá, mensagem de fila de saudação contém um JSON para um `BlobInformation` objeto que inclui um `BlobName` propriedade.</span><span class="sxs-lookup"><span data-stu-id="8b794-150">In hello following example, hello queue message contains JSON for a `BlobInformation` object which includes a `BlobName` property.</span></span> <span data-ttu-id="8b794-151">Olá SDK automaticamente deserializes objeto Olá.</span><span class="sxs-lookup"><span data-stu-id="8b794-151">hello SDK automatically deserializes hello object.</span></span>

        public static void WriteLogPOCO([QueueTrigger("logqueue")] BlobInformation blobInfo, TextWriter logger)
        {
            logger.WriteLine("Queue message refers tooblob: " + blobInfo.BlobName);
        }

<span data-ttu-id="8b794-152">Olá SDK utiliza Olá [pacote NuGet newtonsoft](http://www.nuget.org/packages/Newtonsoft.Json) tooserialize e anular a serialização de mensagens.</span><span class="sxs-lookup"><span data-stu-id="8b794-152">hello SDK uses hello [Newtonsoft.Json NuGet package](http://www.nuget.org/packages/Newtonsoft.Json) tooserialize and deserialize messages.</span></span> <span data-ttu-id="8b794-153">Se criar a fila de mensagens num programa que não utiliza o SDK de WebJobs do Olá, pode escrever o código como Olá seguinte exemplo toocreate uma mensagem de fila POCO esse Olá que SDK pode analisar.</span><span class="sxs-lookup"><span data-stu-id="8b794-153">If you create queue messages in a program that doesn't use hello WebJobs SDK, you can write code like hello following example toocreate a POCO queue message that hello SDK can parse.</span></span>

        BlobInformation blobInfo = new BlobInformation() { BlobName = "log.txt" };
        var queueMessage = new CloudQueueMessage(JsonConvert.SerializeObject(blobInfo));
        logQueue.AddMessage(queueMessage);

### <a name="async-functions"></a><span data-ttu-id="8b794-154">Async funções</span><span class="sxs-lookup"><span data-stu-id="8b794-154">Async functions</span></span>
<span data-ttu-id="8b794-155">Olá seguinte função async [escreve um toohello registo Dashboard](#logs).</span><span class="sxs-lookup"><span data-stu-id="8b794-155">hello following async function [writes a log toohello Dashboard](#logs).</span></span>

        public async static Task ProcessQueueMessageAsync([QueueTrigger("logqueue")] string logMessage, TextWriter logger)
        {
            await logger.WriteLineAsync(logMessage);
        }

<span data-ttu-id="8b794-156">Funções de assíncrona poderão demorar um [token de cancelamento](http://www.asp.net/mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4#CancelToken), conforme mostrado no seguinte exemplo de que copia um blob de Olá.</span><span class="sxs-lookup"><span data-stu-id="8b794-156">Async functions may take a [cancellation token](http://www.asp.net/mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4#CancelToken), as shown in hello following example which copies a blob.</span></span> <span data-ttu-id="8b794-157">(Para obter uma explicação sobre Olá `queueTrigger` marcador de posição, consulte Olá [Blobs](#blobs) secção.)</span><span class="sxs-lookup"><span data-stu-id="8b794-157">(For an explanation of hello `queueTrigger` placeholder, see hello [Blobs](#blobs) section.)</span></span>

        public async static Task ProcessQueueMessageAsyncCancellationToken(
            [QueueTrigger("blobcopyqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}",FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{queueTrigger}-new",FileAccess.Write)] Stream blobOutput,
            CancellationToken token)
        {
            await blobInput.CopyToAsync(blobOutput, 4096, token);
        }

### <span data-ttu-id="8b794-158"><a id="qtattributetypes"></a>Atributo de QueueTrigger tipos Olá funciona com o</span><span class="sxs-lookup"><span data-stu-id="8b794-158"><a id="qtattributetypes"></a> Types hello QueueTrigger attribute works with</span></span>
<span data-ttu-id="8b794-159">Pode utilizar `QueueTrigger` com Olá tipos seguintes:</span><span class="sxs-lookup"><span data-stu-id="8b794-159">You can use `QueueTrigger` with hello following types:</span></span>

* `string`
* <span data-ttu-id="8b794-160">Um tipo POCO serializado como JSON</span><span class="sxs-lookup"><span data-stu-id="8b794-160">A POCO type serialized as JSON</span></span>
* `byte[]`
* `CloudQueueMessage`

### <span data-ttu-id="8b794-161"><a id="polling"></a>Algoritmo de consulta</span><span class="sxs-lookup"><span data-stu-id="8b794-161"><a id="polling"></a> Polling algorithm</span></span>
<span data-ttu-id="8b794-162">Olá SDK implementa um efeito de Olá tooreduce aleatório exponencial término algoritmo da fila de inatividade de consulta em custos de transação de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="8b794-162">hello SDK implements a random exponential back-off algorithm tooreduce hello effect of idle-queue polling on storage transaction costs.</span></span>  <span data-ttu-id="8b794-163">Quando é encontrada uma mensagem, Olá SDK tem de aguardar dois segundos e, em seguida, verifica a existência de outra mensagem; Quando não é encontrada nenhuma mensagem aguarda cerca de quatro segundos antes de tentar novamente.</span><span class="sxs-lookup"><span data-stu-id="8b794-163">When a message is found, hello SDK waits two seconds and then checks for another message; when no message is found it waits about four seconds before trying again.</span></span> <span data-ttu-id="8b794-164">Depois de tentativas falhadas subsequentes tooget uma mensagem de fila, tempo de espera de Olá continua tooincrease até atingir o tempo de espera máximo de Olá, os minutos de tooone predefinições.</span><span class="sxs-lookup"><span data-stu-id="8b794-164">After subsequent failed attempts tooget a queue message, hello wait time continues tooincrease until it reaches hello maximum wait time, which defaults tooone minute.</span></span> <span data-ttu-id="8b794-165">[Olá tempo de espera máximo é configurável](#config).</span><span class="sxs-lookup"><span data-stu-id="8b794-165">[hello maximum wait time is configurable](#config).</span></span>

### <span data-ttu-id="8b794-166"><a id="instances"></a>Várias instâncias</span><span class="sxs-lookup"><span data-stu-id="8b794-166"><a id="instances"></a> Multiple instances</span></span>
<span data-ttu-id="8b794-167">Se a sua aplicação web é executada em várias instâncias, executa um WebJob contínuo em cada máquina, cada máquina irão e aguarde acionadores tentativa toorun funções.</span><span class="sxs-lookup"><span data-stu-id="8b794-167">If your web app runs on multiple instances, a continuous WebJob runs on each machine, and each machine will wait for triggers and attempt toorun functions.</span></span> <span data-ttu-id="8b794-168">Olá acionador de fila do SDK de WebJobs automaticamente impede que uma função de processar uma mensagem de fila várias vezes; as funções não dispõe de toobe escrito toobe idempotent.</span><span class="sxs-lookup"><span data-stu-id="8b794-168">hello WebJobs SDK queue trigger automatically prevents a function from processing a queue message multiple times; functions do not have toobe written toobe idempotent.</span></span> <span data-ttu-id="8b794-169">No entanto, se quiser tooensure que apenas uma instância de uma função é executado mesmo quando existem múltiplas instâncias da aplicação de web do anfitrião de Olá, pode utilizar Olá `Singleton` atributo.</span><span class="sxs-lookup"><span data-stu-id="8b794-169">However, if you want tooensure that only one instance of a function runs even when there are multiple instances of hello host web app, you can use hello `Singleton` attribute.</span></span>

### <span data-ttu-id="8b794-170"><a id="parallel"></a>Execução paralela</span><span class="sxs-lookup"><span data-stu-id="8b794-170"><a id="parallel"></a> Parallel execution</span></span>
<span data-ttu-id="8b794-171">Se tiver várias funções que está a escutar filas diferentes, Olá SDK chamam-los em paralelo quando as mensagens são recebidas em simultâneo.</span><span class="sxs-lookup"><span data-stu-id="8b794-171">If you have multiple functions listening on different queues, hello SDK will call them in parallel when messages are received simultaneously.</span></span>

<span data-ttu-id="8b794-172">Olá mesmo acontece quando várias mensagens são recebidas para uma fila única.</span><span class="sxs-lookup"><span data-stu-id="8b794-172">hello same is true when multiple messages are received for a single queue.</span></span> <span data-ttu-id="8b794-173">Por predefinição, o SDK de Olá obtém um lote de 16 mensagens de fila de cada vez e executa a função Olá que processa-os em paralelo.</span><span class="sxs-lookup"><span data-stu-id="8b794-173">By default, hello SDK gets a batch of 16 queue messages at a time and executes hello function that processes them in parallel.</span></span> <span data-ttu-id="8b794-174">[tamanho do lote Olá é configurável](#config).</span><span class="sxs-lookup"><span data-stu-id="8b794-174">[hello batch size is configurable](#config).</span></span> <span data-ttu-id="8b794-175">Quando o número de Olá a ser processado obtém-se para baixo toohalf do tamanho do lote Olá, Olá SDK obtém outro lote e começa a processar as mensagens.</span><span class="sxs-lookup"><span data-stu-id="8b794-175">When hello number being processed gets down toohalf of hello batch size, hello SDK gets another batch and starts processing those messages.</span></span> <span data-ttu-id="8b794-176">Por conseguinte Olá máximo número em simultâneo de mensagens processados por função é um e um meio vezes Olá de tamanho de lote.</span><span class="sxs-lookup"><span data-stu-id="8b794-176">Therefore hello maximum number of concurrent messages being processed per function is one and a half times hello batch size.</span></span> <span data-ttu-id="8b794-177">Este limite aplica-se em separado tooeach função que tenha um `QueueTrigger` atributo.</span><span class="sxs-lookup"><span data-stu-id="8b794-177">This limit applies separately tooeach function that has a `QueueTrigger` attribute.</span></span>

<span data-ttu-id="8b794-178">Se não quiser execução paralela de mensagens recebidas uma fila, pode definir too1 de tamanho de lote Olá.</span><span class="sxs-lookup"><span data-stu-id="8b794-178">If you don't want parallel execution for messages received on one queue, you can set hello batch size too1.</span></span> <span data-ttu-id="8b794-179">Consulte também **mais controlo sobre o processamento de fila** no [RTM do SDK de WebJobs do Azure 1.1.0](https://azure.microsoft.com/blog/azure-webjobs-sdk-1-1-0-rtm/).</span><span class="sxs-lookup"><span data-stu-id="8b794-179">See also **More control over Queue processing** in [Azure WebJobs SDK 1.1.0 RTM](https://azure.microsoft.com/blog/azure-webjobs-sdk-1-1-0-rtm/).</span></span>

### <span data-ttu-id="8b794-180"><a id="queuemetadata"></a>Obter a fila ou metadados de mensagem de fila</span><span class="sxs-lookup"><span data-stu-id="8b794-180"><a id="queuemetadata"></a>Get queue or queue message metadata</span></span>
<span data-ttu-id="8b794-181">Pode obter Olá seguintes propriedades de mensagem, adicionando a assinatura do método toohello parâmetros:</span><span class="sxs-lookup"><span data-stu-id="8b794-181">You can get hello following message properties by adding parameters toohello method signature:</span></span>

* <span data-ttu-id="8b794-182">`DateTimeOffset`expirationTime</span><span class="sxs-lookup"><span data-stu-id="8b794-182">`DateTimeOffset` expirationTime</span></span>
* <span data-ttu-id="8b794-183">`DateTimeOffset`insertionTime</span><span class="sxs-lookup"><span data-stu-id="8b794-183">`DateTimeOffset` insertionTime</span></span>
* <span data-ttu-id="8b794-184">`DateTimeOffset`nextVisibleTime</span><span class="sxs-lookup"><span data-stu-id="8b794-184">`DateTimeOffset` nextVisibleTime</span></span>
* <span data-ttu-id="8b794-185">`string`queueTrigger (contém o texto da mensagem)</span><span class="sxs-lookup"><span data-stu-id="8b794-185">`string` queueTrigger (contains message text)</span></span>
* <span data-ttu-id="8b794-186">`string`ID</span><span class="sxs-lookup"><span data-stu-id="8b794-186">`string` id</span></span>
* <span data-ttu-id="8b794-187">`string`popReceipt</span><span class="sxs-lookup"><span data-stu-id="8b794-187">`string` popReceipt</span></span>
* <span data-ttu-id="8b794-188">`int`dequeueCount</span><span class="sxs-lookup"><span data-stu-id="8b794-188">`int` dequeueCount</span></span>

<span data-ttu-id="8b794-189">Se quiser toowork diretamente com Olá API do armazenamento do Azure, também pode adicionar um `CloudStorageAccount` parâmetro.</span><span class="sxs-lookup"><span data-stu-id="8b794-189">If you want toowork directly with hello Azure storage API, you can also add a `CloudStorageAccount` parameter.</span></span>

<span data-ttu-id="8b794-190">Olá exemplo seguinte escreve todas este registo de aplicação de informações de tooan de metadados.</span><span class="sxs-lookup"><span data-stu-id="8b794-190">hello following example writes all of this metadata tooan INFO application log.</span></span> <span data-ttu-id="8b794-191">Exemplo de Olá, logMessage e queueTrigger contêm conteúdo de Olá de mensagem de fila de saudação.</span><span class="sxs-lookup"><span data-stu-id="8b794-191">In hello example, both logMessage and queueTrigger contain hello content of hello queue message.</span></span>

        public static void WriteLog([QueueTrigger("logqueue")] string logMessage,
            DateTimeOffset expirationTime,
            DateTimeOffset insertionTime,
            DateTimeOffset nextVisibleTime,
            string id,
            string popReceipt,
            int dequeueCount,
            string queueTrigger,
            CloudStorageAccount cloudStorageAccount,
            TextWriter logger)
        {
            logger.WriteLine(
                "logMessage={0}\n" +
            "expirationTime={1}\ninsertionTime={2}\n" +
                "nextVisibleTime={3}\n" +
                "id={4}\npopReceipt={5}\ndequeueCount={6}\n" +
                "queue endpoint={7} queueTrigger={8}",
                logMessage, expirationTime,
                insertionTime,
                nextVisibleTime, id,
                popReceipt, dequeueCount,
                cloudStorageAccount.QueueEndpoint,
                queueTrigger);
        }

<span data-ttu-id="8b794-192">Segue-se um registo de exemplo escrito pelo código de exemplo de Olá:</span><span class="sxs-lookup"><span data-stu-id="8b794-192">Here is a sample log written by hello sample code:</span></span>

        logMessage=Hello world!
        expirationTime=10/14/2014 10:31:04 PM +00:00
        insertionTime=10/7/2014 10:31:04 PM +00:00
        nextVisibleTime=10/7/2014 10:41:23 PM +00:00
        id=262e49cd-26d3-4303-ae88-33baf8796d91
        popReceipt=AgAAAAMAAAAAAAAAfc9H0n/izwE=
        dequeueCount=1
        queue endpoint=https://contosoads.queue.core.windows.net/
        queueTrigger=Hello world!

### <span data-ttu-id="8b794-193"><a id="graceful"></a>Encerramento correto</span><span class="sxs-lookup"><span data-stu-id="8b794-193"><a id="graceful"></a>Graceful shutdown</span></span>
<span data-ttu-id="8b794-194">Uma função que é executado num WebJob contínuo pode aceitar um `CancellationToken` parâmetro que lhe permite Olá sistema operativo toonotify Olá a função ao hello WebJob é sobre toobe terminada.</span><span class="sxs-lookup"><span data-stu-id="8b794-194">A function that runs in a continuous WebJob can accept a `CancellationToken` parameter which enables hello operating system toonotify hello function when hello WebJob is about toobe terminated.</span></span> <span data-ttu-id="8b794-195">Pode utilizar toomake esta notificação se a função de Olá não terminar inesperadamente de uma forma que mantém os dados num estado inconsistente.</span><span class="sxs-lookup"><span data-stu-id="8b794-195">You can use this notification toomake sure hello function doesn't terminate unexpectedly in a way that leaves data in an inconsistent state.</span></span>

<span data-ttu-id="8b794-196">Olá seguinte exemplo mostra como toocheck para iminente WebJob terminação de uma função.</span><span class="sxs-lookup"><span data-stu-id="8b794-196">hello following example shows how toocheck for impending WebJob termination in a function.</span></span>

    public static void GracefulShutdownDemo(
                [QueueTrigger("inputqueue")] string inputText,
                TextWriter logger,
                CancellationToken token)
    {
        for (int i = 0; i < 100; i++)
        {
            if (token.IsCancellationRequested)
            {
                logger.WriteLine("Function was cancelled at iteration {0}", i);
                break;
            }
            Thread.Sleep(1000);
            logger.WriteLine("Normal processing for queue message={0}", inputText);
        }
    }

<span data-ttu-id="8b794-197">**Nota:** Olá Dashboard não poderá mostrar corretamente o estado de Olá e de saída de funções que foi encerrado.</span><span class="sxs-lookup"><span data-stu-id="8b794-197">**Note:** hello Dashboard might not correctly show hello status and output of functions that have been shut down.</span></span>

<span data-ttu-id="8b794-198">Para obter mais informações, consulte [encerramento correto WebJobs](http://blog.amitapple.com/post/2014/05/webjobs-graceful-shutdown/#.VCt1GXl0wpR).</span><span class="sxs-lookup"><span data-stu-id="8b794-198">For more information, see [WebJobs Graceful Shutdown](http://blog.amitapple.com/post/2014/05/webjobs-graceful-shutdown/#.VCt1GXl0wpR).</span></span>   

## <span data-ttu-id="8b794-199"><a id="createqueue"></a>Como toocreate uma fila de mensagens ao processar uma mensagem de fila</span><span class="sxs-lookup"><span data-stu-id="8b794-199"><a id="createqueue"></a> How toocreate a queue message while processing a queue message</span></span>
<span data-ttu-id="8b794-200">toowrite uma função que cria uma nova mensagem da fila, utilize Olá `Queue` atributo.</span><span class="sxs-lookup"><span data-stu-id="8b794-200">toowrite a function that creates a new queue message, use hello `Queue` attribute.</span></span> <span data-ttu-id="8b794-201">Como `QueueTrigger`, passa no nome da fila Olá como uma cadeia ou pode [definir o nome da fila Olá dinamicamente](#config).</span><span class="sxs-lookup"><span data-stu-id="8b794-201">Like `QueueTrigger`, you pass in hello queue name as a string or you can [set hello queue name dynamically](#config).</span></span>

### <a name="string-queue-messages"></a><span data-ttu-id="8b794-202">Mensagens de filas de cadeia</span><span class="sxs-lookup"><span data-stu-id="8b794-202">String queue messages</span></span>
<span data-ttu-id="8b794-203">Olá seguinte exemplo de código async não cria uma nova mensagem da fila na fila de Olá com o nome "outputqueue" com Olá mesmo conteúdo como mensagem de fila de saudação recebido na fila de Olá com o nome "inputqueue".</span><span class="sxs-lookup"><span data-stu-id="8b794-203">hello following non-async code sample creates a new queue message in hello queue named "outputqueue" with hello same content as hello queue message received in hello queue named "inputqueue".</span></span> <span data-ttu-id="8b794-204">(Assíncrona utilizam funções `IAsyncCollector<T>` conforme mostrado posteriormente nesta secção.)</span><span class="sxs-lookup"><span data-stu-id="8b794-204">(For async functions use `IAsyncCollector<T>` as shown later in this section.)</span></span>

        public static void CreateQueueMessage(
            [QueueTrigger("inputqueue")] string queueMessage,
            [Queue("outputqueue")] out string outputQueueMessage )
        {
            outputQueueMessage = queueMessage;
        }

### <a name="poco-plain-old-clr-objecthttpenwikipediaorgwikiplainoldclrobject-queue-messages"></a><span data-ttu-id="8b794-205">POCO [(simples objeto antigo de CLR](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) mensagens da fila</span><span class="sxs-lookup"><span data-stu-id="8b794-205">POCO [(Plain Old CLR Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) queue messages</span></span>
<span data-ttu-id="8b794-206">tipo de uma mensagem de fila que contém um POCO em vez de uma cadeia, passagem Olá POCO toocreate como um toohello de parâmetro de saída `Queue` construtor de atributos.</span><span class="sxs-lookup"><span data-stu-id="8b794-206">toocreate a queue message that contains a POCO rather than a string, pass hello POCO type as an output parameter toohello `Queue` attribute constructor.</span></span>

        public static void CreateQueueMessage(
            [QueueTrigger("inputqueue")] BlobInformation blobInfoInput,
            [Queue("outputqueue")] out BlobInformation blobInfoOutput )
        {
            blobInfoOutput = blobInfoInput;
        }

<span data-ttu-id="8b794-207">Olá SDK automaticamente serializa Olá tooJSON de objeto.</span><span class="sxs-lookup"><span data-stu-id="8b794-207">hello SDK automatically serializes hello object tooJSON.</span></span> <span data-ttu-id="8b794-208">Uma mensagem de fila é criada sempre, mesmo que o objeto Olá é nulo.</span><span class="sxs-lookup"><span data-stu-id="8b794-208">A queue message is always created, even if hello object is null.</span></span>

### <a name="create-multiple-messages-or-in-async-functions"></a><span data-ttu-id="8b794-209">Criar várias mensagens ou nas funções de assíncrona</span><span class="sxs-lookup"><span data-stu-id="8b794-209">Create multiple messages or in async functions</span></span>
<span data-ttu-id="8b794-210">toocreate várias mensagens, se o tipo de parâmetro de Olá para a fila de saída Olá `ICollector<T>` ou `IAsyncCollector<T>`, conforme mostrado no seguinte exemplo de Olá.</span><span class="sxs-lookup"><span data-stu-id="8b794-210">toocreate multiple messages, make hello parameter type for hello output queue `ICollector<T>` or `IAsyncCollector<T>`, as shown in hello following example.</span></span>

        public static void CreateQueueMessages(
            [QueueTrigger("inputqueue")] string queueMessage,
            [Queue("outputqueue")] ICollector<string> outputQueueMessage,
            TextWriter logger)
        {
            logger.WriteLine("Creating 2 messages in outputqueue");
            outputQueueMessage.Add(queueMessage + "1");
            outputQueueMessage.Add(queueMessage + "2");
        }

<span data-ttu-id="8b794-211">Cada mensagem de fila é criada imediatamente quando hello `Add` método é chamado.</span><span class="sxs-lookup"><span data-stu-id="8b794-211">Each queue message is created immediately when hello `Add` method is called.</span></span>

### <a name="types-that-hello-queue-attribute-works-with"></a><span data-ttu-id="8b794-212">Tipos de atributo de fila que Olá funciona com o</span><span class="sxs-lookup"><span data-stu-id="8b794-212">Types that hello Queue attribute works with</span></span>
<span data-ttu-id="8b794-213">Pode utilizar Olá `Queue` atributo em Olá os seguintes tipos de parâmetro:</span><span class="sxs-lookup"><span data-stu-id="8b794-213">You can use hello `Queue` attribute on hello following parameter types:</span></span>

* <span data-ttu-id="8b794-214">`out string`(cria a mensagem da fila se o valor do parâmetro for não nulo quando a função de Olá termina)</span><span class="sxs-lookup"><span data-stu-id="8b794-214">`out string` (creates queue message if parameter value is non-null when hello function ends)</span></span>
* <span data-ttu-id="8b794-215">`out byte[]`(funciona como `string`)</span><span class="sxs-lookup"><span data-stu-id="8b794-215">`out byte[]` (works like `string`)</span></span>
* <span data-ttu-id="8b794-216">`out CloudQueueMessage`(funciona como `string`)</span><span class="sxs-lookup"><span data-stu-id="8b794-216">`out CloudQueueMessage` (works like `string`)</span></span>
* <span data-ttu-id="8b794-217">`out POCO`(um tipo serializável, cria uma mensagem com um objeto nulo se Olá parâmetro é nulo quando a função de Olá termina)</span><span class="sxs-lookup"><span data-stu-id="8b794-217">`out POCO` (a serializable type, creates a message with a null object if hello paramter is null when hello function ends)</span></span>
* `ICollector`
* `IAsyncCollector`
* <span data-ttu-id="8b794-218">`CloudQueue`(para criar mensagens manualmente utilizando diretamente o Olá API Storage do Azure)</span><span class="sxs-lookup"><span data-stu-id="8b794-218">`CloudQueue` (for creating messages manually using hello Azure Storage API directly)</span></span>

### <span data-ttu-id="8b794-219"><a id="ibinder"></a>Utilizar o SDK de WebJobs atributos no corpo de Olá de uma função</span><span class="sxs-lookup"><span data-stu-id="8b794-219"><a id="ibinder"></a>Use WebJobs SDK attributes in hello body of a function</span></span>
<span data-ttu-id="8b794-220">Se precisar de toodo algumas funcionam na sua função antes de o utilizar como um atributo do SDK de WebJobs `Queue`, `Blob`, ou `Table`, pode utilizar Olá `IBinder` interface.</span><span class="sxs-lookup"><span data-stu-id="8b794-220">If you need toodo some work in your function before using a WebJobs SDK attribute such as `Queue`, `Blob`, or `Table`, you can use hello `IBinder` interface.</span></span>

<span data-ttu-id="8b794-221">Olá seguinte o exemplo assume uma mensagem de fila de entrada e cria uma nova mensagem com Olá mesmo conteúdo na fila de saída.</span><span class="sxs-lookup"><span data-stu-id="8b794-221">hello following example takes an input queue message and creates a new message with hello same content in an output queue.</span></span> <span data-ttu-id="8b794-222">o nome de fila de saída de Olá está definido por código no corpo de Olá da função de Olá.</span><span class="sxs-lookup"><span data-stu-id="8b794-222">hello output queue name is set by code in hello body of hello function.</span></span>

        public static void CreateQueueMessage(
            [QueueTrigger("inputqueue")] string queueMessage,
            IBinder binder)
        {
            string outputQueueName = "outputqueue" + DateTime.Now.Month.ToString();
            QueueAttribute queueAttribute = new QueueAttribute(outputQueueName);
            CloudQueue outputQueue = binder.Bind<CloudQueue>(queueAttribute);
            outputQueue.AddMessage(new CloudQueueMessage(queueMessage));
        }

<span data-ttu-id="8b794-223">Olá `IBinder` interface também pode ser utilizada com Olá `Table` e `Blob` atributos.</span><span class="sxs-lookup"><span data-stu-id="8b794-223">hello `IBinder` interface can also be used with hello `Table` and `Blob` attributes.</span></span>

## <span data-ttu-id="8b794-224"><a id="blobs"></a>Como tooread e de escrita de blobs e tabelas ao processar uma mensagem de fila</span><span class="sxs-lookup"><span data-stu-id="8b794-224"><a id="blobs"></a> How tooread and write blobs and tables while processing a queue message</span></span>
<span data-ttu-id="8b794-225">Olá `Blob` e `Table` atributos permitem-lhe tooread e escrever os blobs e tabelas.</span><span class="sxs-lookup"><span data-stu-id="8b794-225">hello `Blob` and `Table` attributes enable you tooread and write blobs and tables.</span></span> <span data-ttu-id="8b794-226">Exemplos de Olá nesta secção aplicam-se tooblobs.</span><span class="sxs-lookup"><span data-stu-id="8b794-226">hello samples in this section apply tooblobs.</span></span> <span data-ttu-id="8b794-227">Para exemplos de código que mostram como tootrigger processa quando blobs são criados ou atualizados, consulte [como toouse Azure blob storage com o SDK de WebJobs do Olá](websites-dotnet-webjobs-sdk-storage-blobs-how-to.md)e para exemplos de código de leitura e escrita de tabelas, consulte [como toouse tabela do Azure armazenamento com Olá SDK de WebJobs](websites-dotnet-webjobs-sdk-storage-tables-how-to.md).</span><span class="sxs-lookup"><span data-stu-id="8b794-227">For code samples that show how tootrigger processes when blobs are created or updated, see [How toouse Azure blob storage with hello WebJobs SDK](websites-dotnet-webjobs-sdk-storage-blobs-how-to.md), and for code samples that read and write tables, see [How toouse Azure table storage with hello WebJobs SDK](websites-dotnet-webjobs-sdk-storage-tables-how-to.md).</span></span>

### <a name="string-queue-messages-triggering-blob-operations"></a><span data-ttu-id="8b794-228">Mensagens de filas de cadeia acionar operações de BLOBs</span><span class="sxs-lookup"><span data-stu-id="8b794-228">String queue messages triggering blob operations</span></span>
<span data-ttu-id="8b794-229">Para uma mensagem de fila que contém uma cadeia, `queueTrigger` é um marcador de posição pode utilizar Olá `Blob` do atributo `blobPath` parâmetro contém o conteúdo de Olá da mensagem de saudação.</span><span class="sxs-lookup"><span data-stu-id="8b794-229">For a queue message that contains a string, `queueTrigger` is a placeholder you can use in hello `Blob` attribute's `blobPath` parameter that contains hello contents of hello message.</span></span>

<span data-ttu-id="8b794-230">Olá exemplo seguinte utiliza `Stream` objetos tooread e de escrita de blobs.</span><span class="sxs-lookup"><span data-stu-id="8b794-230">hello following example uses `Stream` objects tooread and write blobs.</span></span> <span data-ttu-id="8b794-231">mensagem de fila de saudação é o nome de Olá de um blob localizado num contentor de textblobs Olá.</span><span class="sxs-lookup"><span data-stu-id="8b794-231">hello queue message is hello name of a blob located in hello textblobs container.</span></span> <span data-ttu-id="8b794-232">Uma cópia do blob Olá com "-novo" toohello anexado nome é criada Olá mesmo contentor.</span><span class="sxs-lookup"><span data-stu-id="8b794-232">A copy of hello blob with "-new" appended toohello name is created in hello same container.</span></span>

        public static void ProcessQueueMessage(
            [QueueTrigger("blobcopyqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}",FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{queueTrigger}-new",FileAccess.Write)] Stream blobOutput)
        {
            blobInput.CopyTo(blobOutput, 4096);
        }

<span data-ttu-id="8b794-233">Olá `Blob` demora de construtor de atributos um `blobPath` parâmetro que especifica o contentor de Olá e nome do blob.</span><span class="sxs-lookup"><span data-stu-id="8b794-233">hello `Blob` attribute constructor takes a `blobPath` parameter that specifies hello container and blob name.</span></span> <span data-ttu-id="8b794-234">Para mais informações sobre esta marcador de posição, consulte [como toouse Azure blob storage com o SDK de WebJobs do Olá](websites-dotnet-webjobs-sdk-storage-blobs-how-to.md),</span><span class="sxs-lookup"><span data-stu-id="8b794-234">For more information about this placeholder, see [How toouse Azure blob storage with hello WebJobs SDK](websites-dotnet-webjobs-sdk-storage-blobs-how-to.md),</span></span>

<span data-ttu-id="8b794-235">Quando o atributo de Olá decorates um `Stream` objeto, de outro construtor parâmetro Olá `FileAccess` modo como a leitura, escrita ou leitura/escrita.</span><span class="sxs-lookup"><span data-stu-id="8b794-235">When hello attribute decorates a `Stream` object, another constructor parameter specifies hello `FileAccess` mode as read, write, or read/write.</span></span>

<span data-ttu-id="8b794-236">Olá exemplo seguinte utiliza uma `CloudBlockBlob` toodelete um blob de objeto.</span><span class="sxs-lookup"><span data-stu-id="8b794-236">hello following example uses a `CloudBlockBlob` object toodelete a blob.</span></span> <span data-ttu-id="8b794-237">mensagem de fila de saudação é o nome de Olá do blob Olá.</span><span class="sxs-lookup"><span data-stu-id="8b794-237">hello queue message is hello name of hello blob.</span></span>

        public static void DeleteBlob(
            [QueueTrigger("deleteblobqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}")] CloudBlockBlob blobToDelete)
        {
            blobToDelete.Delete();
        }

### <span data-ttu-id="8b794-238"><a id="pocoblobs"></a>POCO [(simples objeto antigo de CLR](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) mensagens da fila</span><span class="sxs-lookup"><span data-stu-id="8b794-238"><a id="pocoblobs"></a> POCO [(Plain Old CLR Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) queue messages</span></span>
<span data-ttu-id="8b794-239">Para um POCO armazenado como JSON na mensagem de fila de Olá, pode utilizar os marcadores de posição pelo nome propriedades do objeto de Olá na Olá `Queue` do atributo `blobPath` parâmetro.</span><span class="sxs-lookup"><span data-stu-id="8b794-239">For a POCO stored as JSON in hello queue message, you can use placeholders that name properties of hello object in hello `Queue` attribute's `blobPath` parameter.</span></span> <span data-ttu-id="8b794-240">Também pode utilizar [fila os nomes de propriedade de metadados](#queuemetadata) como marcadores de posição.</span><span class="sxs-lookup"><span data-stu-id="8b794-240">You can also use [queue metadata property names](#queuemetadata) as placeholders.</span></span>

<span data-ttu-id="8b794-241">Olá exemplo seguinte copia um blob tooa novo de blob com uma extensão diferente.</span><span class="sxs-lookup"><span data-stu-id="8b794-241">hello following example copies a blob tooa new blob with a different extension.</span></span> <span data-ttu-id="8b794-242">mensagem de fila de saudação é um `BlobInformation` objeto inclui `BlobName` e `BlobNameWithoutExtension` propriedades.</span><span class="sxs-lookup"><span data-stu-id="8b794-242">hello queue message is a `BlobInformation` object that includes `BlobName` and `BlobNameWithoutExtension` properties.</span></span> <span data-ttu-id="8b794-243">os nomes de propriedade Olá são utilizados como marcadores de posição no caminho do blob Olá Olá `Blob` atributos.</span><span class="sxs-lookup"><span data-stu-id="8b794-243">hello property names are used as placeholders in hello blob path for hello `Blob` attributes.</span></span>

        public static void CopyBlobPOCO(
            [QueueTrigger("copyblobqueue")] BlobInformation blobInfo,
            [Blob("textblobs/{BlobName}", FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{BlobNameWithoutExtension}.txt", FileAccess.Write)] Stream blobOutput)
        {
            blobInput.CopyTo(blobOutput, 4096);
        }

<span data-ttu-id="8b794-244">Olá SDK utiliza Olá [pacote NuGet newtonsoft](http://www.nuget.org/packages/Newtonsoft.Json) tooserialize e anular a serialização de mensagens.</span><span class="sxs-lookup"><span data-stu-id="8b794-244">hello SDK uses hello [Newtonsoft.Json NuGet package](http://www.nuget.org/packages/Newtonsoft.Json) tooserialize and deserialize messages.</span></span> <span data-ttu-id="8b794-245">Se criar a fila de mensagens num programa que não utiliza o SDK de WebJobs do Olá, pode escrever o código como Olá seguinte exemplo toocreate uma mensagem de fila POCO esse Olá que SDK pode analisar.</span><span class="sxs-lookup"><span data-stu-id="8b794-245">If you create queue messages in a program that doesn't use hello WebJobs SDK, you can write code like hello following example toocreate a POCO queue message that hello SDK can parse.</span></span>

        BlobInformation blobInfo = new BlobInformation() { BlobName = "boot.log", BlobNameWithoutExtension = "boot" };
        var queueMessage = new CloudQueueMessage(JsonConvert.SerializeObject(blobInfo));
        logQueue.AddMessage(queueMessage);

<span data-ttu-id="8b794-246">Se precisar de toodo algumas funcionam na sua função antes de enlace um objeto de tooan blob, pode utilizar o atributo de Olá no corpo de Olá da função de Olá, [conforme mostrado anteriormente para o atributo de fila de Olá](#ibinder).</span><span class="sxs-lookup"><span data-stu-id="8b794-246">If you need toodo some work in your function before binding a blob tooan object, you can use hello attribute in hello body of hello function, [as shown earlier for hello Queue attribute](#ibinder).</span></span>

### <span data-ttu-id="8b794-247"><a id="blobattributetypes"></a>Tipos que pode utilizar Olá Blob de atributo com o</span><span class="sxs-lookup"><span data-stu-id="8b794-247"><a id="blobattributetypes"></a> Types you can use hello Blob attribute with</span></span>
<span data-ttu-id="8b794-248">Olá `Blob` atributo pode ser utilizado com Olá tipos seguintes:</span><span class="sxs-lookup"><span data-stu-id="8b794-248">hello `Blob` attribute can be used with hello following types:</span></span>

* <span data-ttu-id="8b794-249">`Stream`(ler ou escrever, utilizando o parâmetro de construtor de FileAccess Olá)</span><span class="sxs-lookup"><span data-stu-id="8b794-249">`Stream` (read or write, specified by using hello FileAccess constructor parameter)</span></span>
* `TextReader`
* `TextWriter`
* <span data-ttu-id="8b794-250">`string`(leitura)</span><span class="sxs-lookup"><span data-stu-id="8b794-250">`string` (read)</span></span>
* <span data-ttu-id="8b794-251">`out string`(escrever; cria um blob apenas se o parâmetro de cadeia Olá for não nulo quando a função de Olá devolve)</span><span class="sxs-lookup"><span data-stu-id="8b794-251">`out string` (write; creates a blob only if hello string parameter is non-null when hello function returns)</span></span>
* <span data-ttu-id="8b794-252">POCO (leitura)</span><span class="sxs-lookup"><span data-stu-id="8b794-252">POCO (read)</span></span>
* <span data-ttu-id="8b794-253">saída POCO (escrever; sempre cria um blob, cria como um objeto nulo se POCO parâmetro é nulo quando a função de Olá devolve)</span><span class="sxs-lookup"><span data-stu-id="8b794-253">out POCO (write; always creates a blob, creates as null object if POCO parameter is null when hello function returns)</span></span>
* <span data-ttu-id="8b794-254">`CloudBlobStream`(escrita)</span><span class="sxs-lookup"><span data-stu-id="8b794-254">`CloudBlobStream` (write)</span></span>
* <span data-ttu-id="8b794-255">`ICloudBlob`(ler ou escrever)</span><span class="sxs-lookup"><span data-stu-id="8b794-255">`ICloudBlob` (read or write)</span></span>
* <span data-ttu-id="8b794-256">`CloudBlockBlob`(ler ou escrever)</span><span class="sxs-lookup"><span data-stu-id="8b794-256">`CloudBlockBlob` (read or write)</span></span>
* <span data-ttu-id="8b794-257">`CloudPageBlob`(ler ou escrever)</span><span class="sxs-lookup"><span data-stu-id="8b794-257">`CloudPageBlob` (read or write)</span></span>

## <span data-ttu-id="8b794-258"><a id="poison"></a>Como toohandle poison mensagens</span><span class="sxs-lookup"><span data-stu-id="8b794-258"><a id="poison"></a> How toohandle poison messages</span></span>
<span data-ttu-id="8b794-259">Mensagens cujo conteúdo faz com que uma função toofail são denominadas *poison mensagens*.</span><span class="sxs-lookup"><span data-stu-id="8b794-259">Messages whose content causes a function toofail are called *poison messages*.</span></span> <span data-ttu-id="8b794-260">Quando a função de Olá falha, a mensagem da fila de saudação não é eliminada e, eventualmente, é captada novamente, que provocou toobe de ciclo de Olá repetido.</span><span class="sxs-lookup"><span data-stu-id="8b794-260">When hello function fails, hello queue message is not deleted and eventually is picked up again, causing hello cycle toobe repeated.</span></span> <span data-ttu-id="8b794-261">Olá SDK automaticamente pode interromper o ciclo de Olá após um número limitado de iterações ou pode fazê-lo manualmente.</span><span class="sxs-lookup"><span data-stu-id="8b794-261">hello SDK can automatically interrupt hello cycle after a limited number of iterations, or you can do it manually.</span></span>

### <a name="automatic-poison-message-handling"></a><span data-ttu-id="8b794-262">Processamento de mensagens nocivas automática</span><span class="sxs-lookup"><span data-stu-id="8b794-262">Automatic poison message handling</span></span>
<span data-ttu-id="8b794-263">Olá SDK irá chamar uma função de segurança too5 vezes tooprocess uma mensagem de fila.</span><span class="sxs-lookup"><span data-stu-id="8b794-263">hello SDK will call a function up too5 times tooprocess a queue message.</span></span> <span data-ttu-id="8b794-264">Se tentar quinta Olá falhar, mensagem de saudação é fila corrompida foi movida tooa.</span><span class="sxs-lookup"><span data-stu-id="8b794-264">If hello fifth try fails, hello message is moved tooa poison queue.</span></span> <span data-ttu-id="8b794-265">[Olá número máximo de tentativas é configurável](#config).</span><span class="sxs-lookup"><span data-stu-id="8b794-265">[hello maximum number of retries is configurable](#config).</span></span>

<span data-ttu-id="8b794-266">nome da fila nocivas Olá *{originalqueuename}*-nocivas.</span><span class="sxs-lookup"><span data-stu-id="8b794-266">hello poison queue is named *{originalqueuename}*-poison.</span></span> <span data-ttu-id="8b794-267">Pode escrever um tooprocess função mensagens da fila nocivas Olá por registá-los ou enviar uma notificação que é necessária atenção manual.</span><span class="sxs-lookup"><span data-stu-id="8b794-267">You can write a function tooprocess messages from hello poison queue by logging them or sending a notification that manual attention is needed.</span></span>

<span data-ttu-id="8b794-268">No seguinte Olá de exemplo de Olá `CopyBlob` função irão falhar quando uma mensagem de fila contém o nome de Olá de um blob que não existe.</span><span class="sxs-lookup"><span data-stu-id="8b794-268">In hello following example hello `CopyBlob` function will fail when a queue message contains hello name of a blob that doesn't exist.</span></span> <span data-ttu-id="8b794-269">Quando isso acontece, mensagem de saudação é movida da fila de copyblobqueue poison Olá copyblobqueue fila toohello.</span><span class="sxs-lookup"><span data-stu-id="8b794-269">When that happens, hello message is moved from hello copyblobqueue queue toohello copyblobqueue-poison queue.</span></span> <span data-ttu-id="8b794-270">Olá `ProcessPoisonMessage` , em seguida, os registos Olá a mensagem corrompida foi.</span><span class="sxs-lookup"><span data-stu-id="8b794-270">hello `ProcessPoisonMessage` then logs hello poison message.</span></span>

        public static void CopyBlob(
            [QueueTrigger("copyblobqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}", FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{queueTrigger}-new", FileAccess.Write)] Stream blobOutput)
        {
            blobInput.CopyTo(blobOutput, 4096);
        }

        public static void ProcessPoisonMessage(
            [QueueTrigger("copyblobqueue-poison")] string blobName, TextWriter logger)
        {
            logger.WriteLine("Failed toocopy blob, name=" + blobName);
        }

<span data-ttu-id="8b794-271">Olá ilustração seguinte mostra resultado destas funções consola quando uma mensagem corrompida foi for processada.</span><span class="sxs-lookup"><span data-stu-id="8b794-271">hello following illustration shows console output from these functions when a poison message is processed.</span></span>

![Resultado da consola para processamento de mensagens nocivas](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/poison.png)

### <a name="manual-poison-message-handling"></a><span data-ttu-id="8b794-273">Processamento de mensagens nocivas manual</span><span class="sxs-lookup"><span data-stu-id="8b794-273">Manual poison message handling</span></span>
<span data-ttu-id="8b794-274">Pode obter Olá diversas vezes uma mensagem foi captada para processamento através da adição de um `int` com o nome de parâmetro `dequeueCount` tooyour função.</span><span class="sxs-lookup"><span data-stu-id="8b794-274">You can get hello number of times a message has been picked up for processing by adding an `int` parameter named `dequeueCount` tooyour function.</span></span> <span data-ttu-id="8b794-275">Pode, em seguida, verifique Olá anular a contagem no código de função e executar a sua própria mensagem corrompida foi processamento quando o número de Olá excede um limiar, conforme mostrado no seguinte exemplo de Olá.</span><span class="sxs-lookup"><span data-stu-id="8b794-275">You can then check hello dequeue count in function code and perform your own poison message handling when hello number exceeds a threshold, as shown in hello following example.</span></span>

        public static void CopyBlob(
            [QueueTrigger("copyblobqueue")] string blobName, int dequeueCount,
            [Blob("textblobs/{queueTrigger}", FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{queueTrigger}-new", FileAccess.Write)] Stream blobOutput,
            TextWriter logger)
        {
            if (dequeueCount > 3)
            {
                logger.WriteLine("Failed toocopy blob, name=" + blobName);
            }
            else
            {
            blobInput.CopyTo(blobOutput, 4096);
            }
        }

## <span data-ttu-id="8b794-276"><a id="config"></a>Como tooset opções de configuração</span><span class="sxs-lookup"><span data-stu-id="8b794-276"><a id="config"></a> How tooset configuration options</span></span>
<span data-ttu-id="8b794-277">Pode utilizar Olá `JobHostConfiguration` Olá do tipo tooset seguintes opções de configuração:</span><span class="sxs-lookup"><span data-stu-id="8b794-277">You can use hello `JobHostConfiguration` type tooset hello following configuration options:</span></span>

* <span data-ttu-id="8b794-278">Conjunto de cadeias de ligação do SDK Olá no código.</span><span class="sxs-lookup"><span data-stu-id="8b794-278">Set hello SDK connection strings in code.</span></span>
* <span data-ttu-id="8b794-279">Configurar `QueueTrigger` definições, tais como o máximo anular contagem.</span><span class="sxs-lookup"><span data-stu-id="8b794-279">Configure `QueueTrigger` settings such as maximum dequeue count.</span></span>
* <span data-ttu-id="8b794-280">Obter os nomes de fila de configuração.</span><span class="sxs-lookup"><span data-stu-id="8b794-280">Get queue names from configuration.</span></span>

### <span data-ttu-id="8b794-281"><a id="setconnstr"></a>Definir cadeias de ligação do SDK no código</span><span class="sxs-lookup"><span data-stu-id="8b794-281"><a id="setconnstr"></a>Set SDK connection strings in code</span></span>
<span data-ttu-id="8b794-282">Definir cadeias de ligação do SDK de Olá no código permite-lhe toouse os seus próprios nomes de cadeia de ligação em ficheiros de configuração ou variáveis de ambiente, conforme mostrado no seguinte exemplo de Olá.</span><span class="sxs-lookup"><span data-stu-id="8b794-282">Setting hello SDK connection strings in code enables you toouse your own connection string names in configuration files or environment variables, as shown in hello following example.</span></span>

        static void Main(string[] args)
        {
            var _storageConn = ConfigurationManager
                .ConnectionStrings["MyStorageConnection"].ConnectionString;

            var _dashboardConn = ConfigurationManager
                .ConnectionStrings["MyDashboardConnection"].ConnectionString;

            var _serviceBusConn = ConfigurationManager
                .ConnectionStrings["MyServiceBusConnection"].ConnectionString;

            JobHostConfiguration config = new JobHostConfiguration();
            config.StorageConnectionString = _storageConn;
            config.DashboardConnectionString = _dashboardConn;
            config.ServiceBusConnectionString = _serviceBusConn;
            JobHost host = new JobHost(config);
            host.RunAndBlock();
        }

### <span data-ttu-id="8b794-283"><a id="configqueue"></a>Configurar definições de QueueTrigger</span><span class="sxs-lookup"><span data-stu-id="8b794-283"><a id="configqueue"></a>Configure QueueTrigger  settings</span></span>
<span data-ttu-id="8b794-284">Pode configurar Olá definições que se aplicam processamento de mensagens de fila toohello os seguintes:</span><span class="sxs-lookup"><span data-stu-id="8b794-284">You can configure hello following settings that apply toohello queue message processing:</span></span>

* <span data-ttu-id="8b794-285">Olá número máximo de fila de mensagens que são captado em simultâneo toobe executado em paralelo (a predefinição é 16).</span><span class="sxs-lookup"><span data-stu-id="8b794-285">hello maximum number of queue messages that are picked up simultaneously toobe executed in parallel (default is 16).</span></span>
* <span data-ttu-id="8b794-286">Olá número máximo de tentativas antes do envio de uma mensagem de fila fila nocivas tooa (a predefinição é 5).</span><span class="sxs-lookup"><span data-stu-id="8b794-286">hello maximum number of retries before a queue message is sent tooa poison queue (default is 5).</span></span>
* <span data-ttu-id="8b794-287">tempo de espera máximo de Olá antes de consulta novamente quando uma fila está vazia (a predefinição é 1 minuto).</span><span class="sxs-lookup"><span data-stu-id="8b794-287">hello maximum wait time before polling again when a queue is empty (default is 1 minute).</span></span>

<span data-ttu-id="8b794-288">Olá seguinte exemplo mostra como tooconfigure estas definições:</span><span class="sxs-lookup"><span data-stu-id="8b794-288">hello following example shows how tooconfigure these settings:</span></span>

        static void Main(string[] args)
        {
            JobHostConfiguration config = new JobHostConfiguration();
            config.Queues.BatchSize = 8;
            config.Queues.MaxDequeueCount = 4;
            config.Queues.MaxPollingInterval = TimeSpan.FromSeconds(15);
            JobHost host = new JobHost(config);
            host.RunAndBlock();
        }

### <span data-ttu-id="8b794-289"><a id="setnamesincode"></a>Definir valores para o SDK de WebJobs os parâmetros do construtor no código</span><span class="sxs-lookup"><span data-stu-id="8b794-289"><a id="setnamesincode"></a>Set values for WebJobs SDK constructor parameters in code</span></span>
<span data-ttu-id="8b794-290">Por vezes, pretende toospecify um nome de fila, um nome de blob ou contentor ou nome de uma tabela no código em vez de codificá-lo.</span><span class="sxs-lookup"><span data-stu-id="8b794-290">Sometimes you want toospecify a queue name, a blob name or container, or a table name in code rather than hard-code it.</span></span> <span data-ttu-id="8b794-291">Por exemplo, poderá pretender que nome da fila Olá toospecify para `QueueTrigger` numa variável de ambiente ou ficheiro de configuração.</span><span class="sxs-lookup"><span data-stu-id="8b794-291">For example, you might want toospecify hello queue name for `QueueTrigger` in a configuration file or environment variable.</span></span>

<span data-ttu-id="8b794-292">Pode fazê-lo mediante a transmissão num `NameResolver` objeto toohello `JobHostConfiguration` tipo.</span><span class="sxs-lookup"><span data-stu-id="8b794-292">You can do that by passing in a `NameResolver` object toohello `JobHostConfiguration` type.</span></span> <span data-ttu-id="8b794-293">Incluir marcadores de posição especiais rodeados por sinais de sinal de percentagem () nos parâmetros de construtor de atributo do SDK de WebJobs e os seus `NameResolver` código especifica Olá valores reais toobe utilizado em vez dos marcadores de posição.</span><span class="sxs-lookup"><span data-stu-id="8b794-293">You include special placeholders surrounded by percent (%) signs in WebJobs SDK attribute constructor parameters, and your `NameResolver` code specifies hello actual values toobe used in place of those placeholders.</span></span>

<span data-ttu-id="8b794-294">Por exemplo, suponha que pretende toouse uma fila com o nome logqueuetest no ambiente de teste de Olá e um logqueueprod nomeado em produção.</span><span class="sxs-lookup"><span data-stu-id="8b794-294">For example, suppose you want toouse a queue named logqueuetest in hello test environment and one named logqueueprod in production.</span></span> <span data-ttu-id="8b794-295">Em vez de um nome de fila hard-coded, pretende que o nome de Olá toospecify de uma entrada na Olá `appSettings` coleção que teria o nome de fila real Olá.</span><span class="sxs-lookup"><span data-stu-id="8b794-295">Instead of a hard-coded queue name, you want toospecify hello name of an entry in hello `appSettings` collection that would have hello actual queue name.</span></span> <span data-ttu-id="8b794-296">Se hello `appSettings` chave é logqueue, a função foi aspeto Olá seguinte exemplo.</span><span class="sxs-lookup"><span data-stu-id="8b794-296">If hello `appSettings` key is logqueue, your function could look like hello following example.</span></span>

        public static void WriteLog([QueueTrigger("%logqueue%")] string logMessage)
        {
            Console.WriteLine(logMessage);
        }

<span data-ttu-id="8b794-297">O `NameResolver` classe, em seguida, foi possível obter o nome da fila de Olá `appSettings` conforme mostrado no seguinte exemplo de Olá:</span><span class="sxs-lookup"><span data-stu-id="8b794-297">Your `NameResolver` class could then get hello queue name from `appSettings` as shown in hello following example:</span></span>

        public class QueueNameResolver : INameResolver
        {
            public string Resolve(string name)
            {
                return ConfigurationManager.AppSettings[name].ToString();
            }
        }

<span data-ttu-id="8b794-298">Passar Olá `NameResolver` a classe toohello `JobHost` conforme mostrado no seguinte exemplo de Olá de objeto.</span><span class="sxs-lookup"><span data-stu-id="8b794-298">You pass hello `NameResolver` class in toohello `JobHost` object as shown in hello following example.</span></span>

        static void Main(string[] args)
        {
            JobHostConfiguration config = new JobHostConfiguration();
            config.NameResolver = new QueueNameResolver();
            JobHost host = new JobHost(config);
            host.RunAndBlock();
        }

<span data-ttu-id="8b794-299">**Nota:** fila, tabela e dos nomes blob são resolvidos sempre que uma função é chamada, mas os nomes de contentor do blob são resolvidos apenas quando inicia a aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="8b794-299">**Note:** Queue, table, and blob names are resolved each time a function is called, but blob container names are resolved only when hello application starts.</span></span> <span data-ttu-id="8b794-300">Não é possível alterar o nome do contentor de blob enquanto Olá tarefa está em execução.</span><span class="sxs-lookup"><span data-stu-id="8b794-300">You can't change blob container name while hello job is running.</span></span>

## <span data-ttu-id="8b794-301"><a id="manual"></a>Como uma função de tootrigger manualmente</span><span class="sxs-lookup"><span data-stu-id="8b794-301"><a id="manual"></a>How tootrigger a function manually</span></span>
<span data-ttu-id="8b794-302">uma função de tootrigger manualmente, utilize Olá `Call` ou `CallAsync` método no Olá `JobHost` objeto e Olá `NoAutomaticTrigger` atributo na função Olá, conforme mostrado no seguinte exemplo de Olá.</span><span class="sxs-lookup"><span data-stu-id="8b794-302">tootrigger a function manually, use hello `Call` or `CallAsync` method on hello `JobHost` object and hello `NoAutomaticTrigger` attribute on hello function, as shown in hello following example.</span></span>

        public class Program
        {
            static void Main(string[] args)
            {
                JobHost host = new JobHost();
                host.Call(typeof(Program).GetMethod("CreateQueueMessage"), new { value = "Hello world!" });
            }

            [NoAutomaticTrigger]
            public static void CreateQueueMessage(
                TextWriter logger,
                string value,
                [Queue("outputqueue")] out string message)
            {
                message = value;
                logger.WriteLine("Creating queue message: ", message);
            }
        }

## <span data-ttu-id="8b794-303"><a id="logs"></a>Modo de registo de toowrite</span><span class="sxs-lookup"><span data-stu-id="8b794-303"><a id="logs"></a>How toowrite logs</span></span>
<span data-ttu-id="8b794-304">Olá Dashboard mostra os registos em dois locais: página Olá Olá WebJob e página Olá para uma invocação de WebJob específica.</span><span class="sxs-lookup"><span data-stu-id="8b794-304">hello Dashboard shows logs in two places: hello page for hello WebJob, and hello page for a particular WebJob invocation.</span></span>

![Registos na página do trabalho Web](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/dashboardapplogs.png)

![Registos na página de invocação de função](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/dashboardlogs.png)

<span data-ttu-id="8b794-307">Saída de métodos de consola que tem de chamar uma função ou Olá `Main()` método é apresentado na página do Dashboard Olá para Olá WebJob e não na página Olá para um determinado método de invocação.</span><span class="sxs-lookup"><span data-stu-id="8b794-307">Output from Console methods that you call in a function or in hello `Main()` method appears in hello Dashboard page for hello WebJob, not in hello page for a particular method invocation.</span></span> <span data-ttu-id="8b794-308">Saída do objeto de TextWriter Olá que obtém a partir de um parâmetro na sua assinatura do método é apresentado na página do Dashboard Olá para um método de invocação.</span><span class="sxs-lookup"><span data-stu-id="8b794-308">Output from hello TextWriter object that you get from a parameter in your method signature appears in hello Dashboard page for a method invocation.</span></span>

<span data-ttu-id="8b794-309">Resultado da consola não pode ser ligado tooa determinado método invocação porque Olá consola single-threaded, enquanto muitas funções de tarefas poderão estar em execução em Olá mesmo tempo.</span><span class="sxs-lookup"><span data-stu-id="8b794-309">Console output can't be linked tooa particular method invocation because hello Console is single-threaded, while many job functions may be running at hello same time.</span></span> <span data-ttu-id="8b794-310">É por esse motivo Olá SDK fornece cada invocação de função com o seu próprio objeto de escritor do registo exclusivo.</span><span class="sxs-lookup"><span data-stu-id="8b794-310">That's why hello  SDK provides each function invocation with its own unique log writer object.</span></span>

<span data-ttu-id="8b794-311">toowrite [registos de rastreio de aplicação](web-sites-dotnet-troubleshoot-visual-studio.md#logsoverview), utilize `Console.Out` (cria registos marcados como informação) e `Console.Error` (cria registos marcados como erro).</span><span class="sxs-lookup"><span data-stu-id="8b794-311">toowrite [application tracing logs](web-sites-dotnet-troubleshoot-visual-studio.md#logsoverview), use `Console.Out` (creates logs marked as INFO) and `Console.Error` (creates logs marked as ERROR).</span></span> <span data-ttu-id="8b794-312">Uma alternativa é toouse [rastreio ou TraceSource](http://blogs.msdn.com/b/mcsuksoldev/archive/2014/09/04/adding-trace-to-azure-web-sites-and-web-jobs.aspx), que fornece verboso, aviso, e os níveis de crítico na adição tooInfo e o erro.</span><span class="sxs-lookup"><span data-stu-id="8b794-312">An alternative is toouse [Trace or TraceSource](http://blogs.msdn.com/b/mcsuksoldev/archive/2014/09/04/adding-trace-to-azure-web-sites-and-web-jobs.aspx), which provides Verbose, Warning, and Critical levels in addition tooInfo and Error.</span></span> <span data-ttu-id="8b794-313">Os registos de rastreio de aplicações são apresentados nos ficheiros de registo de aplicação web Olá, as tabelas do Azure, ou de blobs do Azure, dependendo de como configurar a sua aplicação web do Azure.</span><span class="sxs-lookup"><span data-stu-id="8b794-313">Application tracing logs appear in hello web app log files, Azure tables, or Azure blobs depending on how you configure your Azure web app.</span></span> <span data-ttu-id="8b794-314">Como é verdadeiro de todos os resultados da consola, os registos de aplicações 100 mais recentes Olá também são apresentados na página do Dashboard de Olá para Olá WebJob, não Olá página uma invocação de função.</span><span class="sxs-lookup"><span data-stu-id="8b794-314">As is true of all Console output, hello most recent 100 application logs also appear in hello Dashboard page for hello WebJob, not hello page for a function invocation.</span></span>

<span data-ttu-id="8b794-315">Resultado da consola é apresentado no Olá Dashboard apenas se o programa de Olá está em execução num trabalho Web do Azure, não se o programa de Olá é executada localmente ou alguns outros ambiente.</span><span class="sxs-lookup"><span data-stu-id="8b794-315">Console output appears in hello Dashboard only if hello program is running in an Azure WebJob, not if hello program is running locally or in some other environment.</span></span>

<span data-ttu-id="8b794-316">Desative o registo de dashboard para cenários de débito elevado.</span><span class="sxs-lookup"><span data-stu-id="8b794-316">Disable dashboard logging for high throughput scenarios.</span></span> <span data-ttu-id="8b794-317">Por predefinição, Olá SDK escreve registos toostorage e esta atividade pode degradar o desempenho quando está a processar muitas mensagens.</span><span class="sxs-lookup"><span data-stu-id="8b794-317">By default, hello SDK writes logs toostorage, and this activity could degrade performance when you are processing many messages.</span></span> <span data-ttu-id="8b794-318">toodisable registo, defina toonull de cadeia de ligação de dashboard Olá, conforme mostrado no seguinte exemplo de Olá.</span><span class="sxs-lookup"><span data-stu-id="8b794-318">toodisable logging, set hello dashboard connection string toonull as shown in hello following example.</span></span>

        JobHostConfiguration config = new JobHostConfiguration();       
        config.DashboardConnectionString = "";        
        JobHost host = new JobHost(config);
        host.RunAndBlock();

<span data-ttu-id="8b794-319">Olá exemplo seguinte mostra várias formas toowrite registos:</span><span class="sxs-lookup"><span data-stu-id="8b794-319">hello following example shows several ways toowrite logs:</span></span>

        public static void WriteLog(
            [QueueTrigger("logqueue")] string logMessage,
            TextWriter logger)
        {
            Console.WriteLine("Console.Write - " + logMessage);
            Console.Out.WriteLine("Console.Out - " + logMessage);
            Console.Error.WriteLine("Console.Error - " + logMessage);
            logger.WriteLine("TextWriter - " + logMessage);
        }

<span data-ttu-id="8b794-320">No Dashboard do SDK de WebJobs Olá, Olá saída de Olá `TextWriter` objeto mostra cópias de segurança quando acede toohello página para um determinado invocação de função e clique em **alternar saída**:</span><span class="sxs-lookup"><span data-stu-id="8b794-320">In hello WebJobs SDK Dashboard, hello output from hello `TextWriter` object shows up when you go toohello page for a particular function invocation and click **Toggle Output**:</span></span>

![Clique em ligação de invocação de função](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/dashboardinvocations.png)

![Registos na página de invocação de função](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/dashboardlogs.png)

<span data-ttu-id="8b794-323">No Dashboard do SDK de WebJobs Olá, linhas de Olá 100 mais recente da consola de saída Mostrar cópias de segurança quando aceda toohello página Olá WebJob (não para a invocação de função Olá) e clique em **alternar saída**.</span><span class="sxs-lookup"><span data-stu-id="8b794-323">In hello WebJobs SDK Dashboard, hello most recent 100 lines of Console output show up when you go toohello page for hello WebJob (not for hello function invocation) and click **Toggle Output**.</span></span>

![Clique em Ativar/desativar de saída](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/dashboardapplogs.png)

<span data-ttu-id="8b794-325">Num WebJob contínuo, os registos de aplicações apresentada na/dados/tarefas/contínua/*{webjobname}*/job_log.txt no sistema de ficheiros de aplicação de web de Olá.</span><span class="sxs-lookup"><span data-stu-id="8b794-325">In a continuous WebJob, application logs show up in /data/jobs/continuous/*{webjobname}*/job_log.txt in hello web app file system.</span></span>

        [09/26/2014 21:01:13 > 491e54: INFO] Console.Write - Hello world!
        [09/26/2014 21:01:13 > 491e54: ERR ] Console.Error - Hello world!
        [09/26/2014 21:01:13 > 491e54: INFO] Console.Out - Hello world!

<span data-ttu-id="8b794-326">Numa aplicação Olá BLOBs do Azure registos este aspeto: 2014-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738373502,0,17404,17,Console.Write - Olá, mundo!, 2014-09-26T21:01:13, erro, contosoadsnew, 491e54, 635473620738373502,0,17404,19,Console.Error - Olá, mundo!, 2014-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738529920,0,17404,17,Console.Out - Olá, mundo!,</span><span class="sxs-lookup"><span data-stu-id="8b794-326">In an Azure blob hello application logs look like this: 2014-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738373502,0,17404,17,Console.Write - Hello world!, 2014-09-26T21:01:13,Error,contosoadsnew,491e54,635473620738373502,0,17404,19,Console.Error - Hello world!, 2014-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738529920,0,17404,17,Console.Out - Hello world!,</span></span>

<span data-ttu-id="8b794-327">E no Olá tabela do Azure `Console.Out` e `Console.Error` registos tem o seguinte aspeto:</span><span class="sxs-lookup"><span data-stu-id="8b794-327">And in an Azure table hello `Console.Out` and `Console.Error` logs look like this:</span></span>

![Registo de informações na tabela](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/tableinfo.png)

![Registo de erros na tabela](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/tableerror.png)

<span data-ttu-id="8b794-330">Se quiser tooplug no seu próprio registo, consulte [neste exemplo](http://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/MiscOperations/Program.cs).</span><span class="sxs-lookup"><span data-stu-id="8b794-330">If you want tooplug in your own logger, see [this example](http://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/MiscOperations/Program.cs).</span></span>

## <span data-ttu-id="8b794-331"><a id="errors"></a>Como toohandle erros e configurar os tempos limite</span><span class="sxs-lookup"><span data-stu-id="8b794-331"><a id="errors"></a>How toohandle errors and configure timeouts</span></span>
<span data-ttu-id="8b794-332">Olá SDK de WebJobs também inclui um [tempo limite](http://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/MiscOperations/Functions.cs) atributo que pode utilizar toocause toobe uma função cancelada se não concluir dentro de um período de tempo especificado.</span><span class="sxs-lookup"><span data-stu-id="8b794-332">hello WebJobs SDK also includes a [Timeout](http://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/MiscOperations/Functions.cs) attribute that you can use toocause a function toobe canceled if doesn't complete within a specified amount of time.</span></span> <span data-ttu-id="8b794-333">Se pretender tooraise um alerta quando existem demasiados erros ocorrem dentro de um período de tempo especificado, pode utilizar Olá `ErrorTrigger` atributo.</span><span class="sxs-lookup"><span data-stu-id="8b794-333">And if you want tooraise an alert when too many errors happen within a specified period of time, you can use hello `ErrorTrigger` attribute.</span></span> <span data-ttu-id="8b794-334">Eis um [ErrorTrigger exemplo](https://github.com/Azure/azure-webjobs-sdk-extensions/wiki/Error-Monitoring).</span><span class="sxs-lookup"><span data-stu-id="8b794-334">Here is an [ErrorTrigger example](https://github.com/Azure/azure-webjobs-sdk-extensions/wiki/Error-Monitoring).</span></span>

```
public static void ErrorMonitor(
[ErrorTrigger("00:01:00", 1)] TraceFilter filter, TextWriter log,
[SendGrid(
    too= "admin@emailaddress.com",
    Subject = "Error!")]
 SendGridMessage message)
{
    // log last 5 detailed errors toohello Dashboard
   log.WriteLine(filter.GetDetailedMessage(5));
   message.Text = filter.GetDetailedMessage(1);
}
```

<span data-ttu-id="8b794-335">Pode também dinamicamente desativar e ativar funções toocontrol se de que podem ser acionadas, utilizando um parâmetro de configuração que pode ser uma definição de aplicação ou o nome de variável de ambiente.</span><span class="sxs-lookup"><span data-stu-id="8b794-335">You can also dynamically disable and enable functions toocontrol whether they can be triggered, by using a configuration switch that could be an app setting or environment variable name.</span></span> <span data-ttu-id="8b794-336">Para o código de exemplo, consulte Olá `Disable` atributo em [Olá SDK de WebJobs amostras repositório](https://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/MiscOperations/Functions.cs).</span><span class="sxs-lookup"><span data-stu-id="8b794-336">For sample code, see hello `Disable` attribute in [hello WebJobs SDK samples repository](https://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/MiscOperations/Functions.cs).</span></span>

## <span data-ttu-id="8b794-337"><a id="nextsteps"></a> Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="8b794-337"><a id="nextsteps"></a> Next steps</span></span>
<span data-ttu-id="8b794-338">Este guia forneceu o código de exemplo que mostram como toohandle cenários comuns para trabalhar com as filas do Azure.</span><span class="sxs-lookup"><span data-stu-id="8b794-338">This guide has provided code samples that show how toohandle common scenarios for working with Azure queues.</span></span> <span data-ttu-id="8b794-339">Para obter mais informações sobre como toouse WebJobs do Azure e Olá SDK de WebJobs, consulte [recursos de recomendada de WebJobs do Azure](http://go.microsoft.com/fwlink/?linkid=390226).</span><span class="sxs-lookup"><span data-stu-id="8b794-339">For more information about how toouse Azure WebJobs and hello WebJobs SDK, see [Azure WebJobs Recommended Resources](http://go.microsoft.com/fwlink/?linkid=390226).</span></span>
