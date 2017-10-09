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
# <a name="how-toouse-azure-queue-storage-with-hello-webjobs-sdk"></a>Como toouse Azure fila de armazenamento com Olá SDK de WebJobs
## <a name="overview"></a>Descrição geral
Este guia fornece c# exemplos de código que mostram como toouse Olá versão do SDK de WebJobs do Azure 1. x com Olá serviço de armazenamento de filas do Azure.

Guia de Olá parte do princípio de que sabe [como toocreate um projeto do trabalho Web no Visual Studio com ligação cadeias essa conta do storage ponto tooyour](websites-dotnet-webjobs-sdk-get-started.md) ou demasiado[várias contas do storage](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs).

Na maioria das fragmentos de código Olá mostra apenas as funções, não Olá código que cria Olá `JobHost` objeto tal como neste exemplo:

        static void Main(string[] args)
        {
            JobHost host = new JobHost();
            host.RunAndBlock();
        }

Guia de Olá inclui Olá os seguintes tópicos:

* [Como tootrigger uma função quando é recebida uma mensagem de fila](#trigger)
  * Mensagens de filas de cadeia
  * Mensagens de filas POCO
  * Async funções
  * Atributo de QueueTrigger tipos Olá funciona com o
  * Algoritmo de consulta
  * Várias instâncias
  * Execução paralela
  * Obter a fila ou metadados de mensagem de fila
  * Encerramento correto
* [Como toocreate uma fila de mensagens ao processar uma mensagem de fila](#createqueue)
  * Mensagens de filas de cadeia
  * Mensagens de filas POCO
  * Criar várias mensagens ou nas funções de assíncrona
  * Atributo de fila de Olá tipos funciona com o
  * Utilizar o SDK de WebJobs atributos no corpo de Olá de uma função
* [Como tooread e de escrita de blobs ao processar uma mensagem de fila](#blobs)
  * Mensagens de filas de cadeia
  * Mensagens de filas POCO
  * Atributo de Blob tipos Olá funciona com o
* [Como toohandle poison mensagens](#poison)
  * Processamento de mensagens nocivas automática
  * Processamento de mensagens nocivas manual
* [Como tooset opções de configuração](#config)
  * Definir cadeias de ligação do SDK no código
  * Configurar definições de QueueTrigger
  * Definir valores para o SDK de WebJobs os parâmetros do construtor no código
* [Como uma função de tootrigger manualmente](#manual)
* [Modo de registo de toowrite](#logs)
* [Como toohandle erros e configurar os tempos limite](#errors)
* [Passos seguintes?](#nextsteps)

## <a id="trigger"></a>Como tootrigger uma função quando é recebida uma mensagem de fila
chamadas de uma função que Olá SDK de WebJobs toowrite quando é recebida uma mensagem de fila, utilize Olá `QueueTrigger` atributo. o construtor de atributos de Olá assume um parâmetro de cadeia que especifica o nome de Olá de Olá toopoll de fila. Também pode [definir o nome da fila Olá dinamicamente](#config).

### <a name="string-queue-messages"></a>Mensagens de filas de cadeia
No seguinte exemplo de Olá, Olá fila contém uma mensagem de cadeia, por isso, `QueueTrigger` é aplicado tooa parâmetro de cadeia com o nome `logMessage` que contém conteúdo Olá de mensagem de fila de saudação. Olá função [escreve um toohello de mensagem do registo Dashboard](#logs).

        public static void ProcessQueueMessage([QueueTrigger("logqueue")] string logMessage, TextWriter logger)
        {
            logger.WriteLine(logMessage);
        }

Besides `string`, parâmetro de Olá pode ser uma matriz de bytes, um `CloudQueueMessage` objeto ou um POCO por si.

### <a name="poco-plain-old-clr-objecthttpenwikipediaorgwikiplainoldclrobject-queue-messages"></a>POCO [(simples objeto antigo de CLR](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) mensagens da fila
No seguinte exemplo de Olá, mensagem de fila de saudação contém um JSON para um `BlobInformation` objeto que inclui um `BlobName` propriedade. Olá SDK automaticamente deserializes objeto Olá.

        public static void WriteLogPOCO([QueueTrigger("logqueue")] BlobInformation blobInfo, TextWriter logger)
        {
            logger.WriteLine("Queue message refers tooblob: " + blobInfo.BlobName);
        }

Olá SDK utiliza Olá [pacote NuGet newtonsoft](http://www.nuget.org/packages/Newtonsoft.Json) tooserialize e anular a serialização de mensagens. Se criar a fila de mensagens num programa que não utiliza o SDK de WebJobs do Olá, pode escrever o código como Olá seguinte exemplo toocreate uma mensagem de fila POCO esse Olá que SDK pode analisar.

        BlobInformation blobInfo = new BlobInformation() { BlobName = "log.txt" };
        var queueMessage = new CloudQueueMessage(JsonConvert.SerializeObject(blobInfo));
        logQueue.AddMessage(queueMessage);

### <a name="async-functions"></a>Async funções
Olá seguinte função async [escreve um toohello registo Dashboard](#logs).

        public async static Task ProcessQueueMessageAsync([QueueTrigger("logqueue")] string logMessage, TextWriter logger)
        {
            await logger.WriteLineAsync(logMessage);
        }

Funções de assíncrona poderão demorar um [token de cancelamento](http://www.asp.net/mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4#CancelToken), conforme mostrado no seguinte exemplo de que copia um blob de Olá. (Para obter uma explicação sobre Olá `queueTrigger` marcador de posição, consulte Olá [Blobs](#blobs) secção.)

        public async static Task ProcessQueueMessageAsyncCancellationToken(
            [QueueTrigger("blobcopyqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}",FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{queueTrigger}-new",FileAccess.Write)] Stream blobOutput,
            CancellationToken token)
        {
            await blobInput.CopyToAsync(blobOutput, 4096, token);
        }

### <a id="qtattributetypes"></a>Atributo de QueueTrigger tipos Olá funciona com o
Pode utilizar `QueueTrigger` com Olá tipos seguintes:

* `string`
* Um tipo POCO serializado como JSON
* `byte[]`
* `CloudQueueMessage`

### <a id="polling"></a>Algoritmo de consulta
Olá SDK implementa um efeito de Olá tooreduce aleatório exponencial término algoritmo da fila de inatividade de consulta em custos de transação de armazenamento.  Quando é encontrada uma mensagem, Olá SDK tem de aguardar dois segundos e, em seguida, verifica a existência de outra mensagem; Quando não é encontrada nenhuma mensagem aguarda cerca de quatro segundos antes de tentar novamente. Depois de tentativas falhadas subsequentes tooget uma mensagem de fila, tempo de espera de Olá continua tooincrease até atingir o tempo de espera máximo de Olá, os minutos de tooone predefinições. [Olá tempo de espera máximo é configurável](#config).

### <a id="instances"></a>Várias instâncias
Se a sua aplicação web é executada em várias instâncias, executa um WebJob contínuo em cada máquina, cada máquina irão e aguarde acionadores tentativa toorun funções. Olá acionador de fila do SDK de WebJobs automaticamente impede que uma função de processar uma mensagem de fila várias vezes; as funções não dispõe de toobe escrito toobe idempotent. No entanto, se quiser tooensure que apenas uma instância de uma função é executado mesmo quando existem múltiplas instâncias da aplicação de web do anfitrião de Olá, pode utilizar Olá `Singleton` atributo.

### <a id="parallel"></a>Execução paralela
Se tiver várias funções que está a escutar filas diferentes, Olá SDK chamam-los em paralelo quando as mensagens são recebidas em simultâneo.

Olá mesmo acontece quando várias mensagens são recebidas para uma fila única. Por predefinição, o SDK de Olá obtém um lote de 16 mensagens de fila de cada vez e executa a função Olá que processa-os em paralelo. [tamanho do lote Olá é configurável](#config). Quando o número de Olá a ser processado obtém-se para baixo toohalf do tamanho do lote Olá, Olá SDK obtém outro lote e começa a processar as mensagens. Por conseguinte Olá máximo número em simultâneo de mensagens processados por função é um e um meio vezes Olá de tamanho de lote. Este limite aplica-se em separado tooeach função que tenha um `QueueTrigger` atributo.

Se não quiser execução paralela de mensagens recebidas uma fila, pode definir too1 de tamanho de lote Olá. Consulte também **mais controlo sobre o processamento de fila** no [RTM do SDK de WebJobs do Azure 1.1.0](https://azure.microsoft.com/blog/azure-webjobs-sdk-1-1-0-rtm/).

### <a id="queuemetadata"></a>Obter a fila ou metadados de mensagem de fila
Pode obter Olá seguintes propriedades de mensagem, adicionando a assinatura do método toohello parâmetros:

* `DateTimeOffset`expirationTime
* `DateTimeOffset`insertionTime
* `DateTimeOffset`nextVisibleTime
* `string`queueTrigger (contém o texto da mensagem)
* `string`ID
* `string`popReceipt
* `int`dequeueCount

Se quiser toowork diretamente com Olá API do armazenamento do Azure, também pode adicionar um `CloudStorageAccount` parâmetro.

Olá exemplo seguinte escreve todas este registo de aplicação de informações de tooan de metadados. Exemplo de Olá, logMessage e queueTrigger contêm conteúdo de Olá de mensagem de fila de saudação.

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

Segue-se um registo de exemplo escrito pelo código de exemplo de Olá:

        logMessage=Hello world!
        expirationTime=10/14/2014 10:31:04 PM +00:00
        insertionTime=10/7/2014 10:31:04 PM +00:00
        nextVisibleTime=10/7/2014 10:41:23 PM +00:00
        id=262e49cd-26d3-4303-ae88-33baf8796d91
        popReceipt=AgAAAAMAAAAAAAAAfc9H0n/izwE=
        dequeueCount=1
        queue endpoint=https://contosoads.queue.core.windows.net/
        queueTrigger=Hello world!

### <a id="graceful"></a>Encerramento correto
Uma função que é executado num WebJob contínuo pode aceitar um `CancellationToken` parâmetro que lhe permite Olá sistema operativo toonotify Olá a função ao hello WebJob é sobre toobe terminada. Pode utilizar toomake esta notificação se a função de Olá não terminar inesperadamente de uma forma que mantém os dados num estado inconsistente.

Olá seguinte exemplo mostra como toocheck para iminente WebJob terminação de uma função.

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

**Nota:** Olá Dashboard não poderá mostrar corretamente o estado de Olá e de saída de funções que foi encerrado.

Para obter mais informações, consulte [encerramento correto WebJobs](http://blog.amitapple.com/post/2014/05/webjobs-graceful-shutdown/#.VCt1GXl0wpR).   

## <a id="createqueue"></a>Como toocreate uma fila de mensagens ao processar uma mensagem de fila
toowrite uma função que cria uma nova mensagem da fila, utilize Olá `Queue` atributo. Como `QueueTrigger`, passa no nome da fila Olá como uma cadeia ou pode [definir o nome da fila Olá dinamicamente](#config).

### <a name="string-queue-messages"></a>Mensagens de filas de cadeia
Olá seguinte exemplo de código async não cria uma nova mensagem da fila na fila de Olá com o nome "outputqueue" com Olá mesmo conteúdo como mensagem de fila de saudação recebido na fila de Olá com o nome "inputqueue". (Assíncrona utilizam funções `IAsyncCollector<T>` conforme mostrado posteriormente nesta secção.)

        public static void CreateQueueMessage(
            [QueueTrigger("inputqueue")] string queueMessage,
            [Queue("outputqueue")] out string outputQueueMessage )
        {
            outputQueueMessage = queueMessage;
        }

### <a name="poco-plain-old-clr-objecthttpenwikipediaorgwikiplainoldclrobject-queue-messages"></a>POCO [(simples objeto antigo de CLR](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) mensagens da fila
tipo de uma mensagem de fila que contém um POCO em vez de uma cadeia, passagem Olá POCO toocreate como um toohello de parâmetro de saída `Queue` construtor de atributos.

        public static void CreateQueueMessage(
            [QueueTrigger("inputqueue")] BlobInformation blobInfoInput,
            [Queue("outputqueue")] out BlobInformation blobInfoOutput )
        {
            blobInfoOutput = blobInfoInput;
        }

Olá SDK automaticamente serializa Olá tooJSON de objeto. Uma mensagem de fila é criada sempre, mesmo que o objeto Olá é nulo.

### <a name="create-multiple-messages-or-in-async-functions"></a>Criar várias mensagens ou nas funções de assíncrona
toocreate várias mensagens, se o tipo de parâmetro de Olá para a fila de saída Olá `ICollector<T>` ou `IAsyncCollector<T>`, conforme mostrado no seguinte exemplo de Olá.

        public static void CreateQueueMessages(
            [QueueTrigger("inputqueue")] string queueMessage,
            [Queue("outputqueue")] ICollector<string> outputQueueMessage,
            TextWriter logger)
        {
            logger.WriteLine("Creating 2 messages in outputqueue");
            outputQueueMessage.Add(queueMessage + "1");
            outputQueueMessage.Add(queueMessage + "2");
        }

Cada mensagem de fila é criada imediatamente quando hello `Add` método é chamado.

### <a name="types-that-hello-queue-attribute-works-with"></a>Tipos de atributo de fila que Olá funciona com o
Pode utilizar Olá `Queue` atributo em Olá os seguintes tipos de parâmetro:

* `out string`(cria a mensagem da fila se o valor do parâmetro for não nulo quando a função de Olá termina)
* `out byte[]`(funciona como `string`)
* `out CloudQueueMessage`(funciona como `string`)
* `out POCO`(um tipo serializável, cria uma mensagem com um objeto nulo se Olá parâmetro é nulo quando a função de Olá termina)
* `ICollector`
* `IAsyncCollector`
* `CloudQueue`(para criar mensagens manualmente utilizando diretamente o Olá API Storage do Azure)

### <a id="ibinder"></a>Utilizar o SDK de WebJobs atributos no corpo de Olá de uma função
Se precisar de toodo algumas funcionam na sua função antes de o utilizar como um atributo do SDK de WebJobs `Queue`, `Blob`, ou `Table`, pode utilizar Olá `IBinder` interface.

Olá seguinte o exemplo assume uma mensagem de fila de entrada e cria uma nova mensagem com Olá mesmo conteúdo na fila de saída. o nome de fila de saída de Olá está definido por código no corpo de Olá da função de Olá.

        public static void CreateQueueMessage(
            [QueueTrigger("inputqueue")] string queueMessage,
            IBinder binder)
        {
            string outputQueueName = "outputqueue" + DateTime.Now.Month.ToString();
            QueueAttribute queueAttribute = new QueueAttribute(outputQueueName);
            CloudQueue outputQueue = binder.Bind<CloudQueue>(queueAttribute);
            outputQueue.AddMessage(new CloudQueueMessage(queueMessage));
        }

Olá `IBinder` interface também pode ser utilizada com Olá `Table` e `Blob` atributos.

## <a id="blobs"></a>Como tooread e de escrita de blobs e tabelas ao processar uma mensagem de fila
Olá `Blob` e `Table` atributos permitem-lhe tooread e escrever os blobs e tabelas. Exemplos de Olá nesta secção aplicam-se tooblobs. Para exemplos de código que mostram como tootrigger processa quando blobs são criados ou atualizados, consulte [como toouse Azure blob storage com o SDK de WebJobs do Olá](websites-dotnet-webjobs-sdk-storage-blobs-how-to.md)e para exemplos de código de leitura e escrita de tabelas, consulte [como toouse tabela do Azure armazenamento com Olá SDK de WebJobs](websites-dotnet-webjobs-sdk-storage-tables-how-to.md).

### <a name="string-queue-messages-triggering-blob-operations"></a>Mensagens de filas de cadeia acionar operações de BLOBs
Para uma mensagem de fila que contém uma cadeia, `queueTrigger` é um marcador de posição pode utilizar Olá `Blob` do atributo `blobPath` parâmetro contém o conteúdo de Olá da mensagem de saudação.

Olá exemplo seguinte utiliza `Stream` objetos tooread e de escrita de blobs. mensagem de fila de saudação é o nome de Olá de um blob localizado num contentor de textblobs Olá. Uma cópia do blob Olá com "-novo" toohello anexado nome é criada Olá mesmo contentor.

        public static void ProcessQueueMessage(
            [QueueTrigger("blobcopyqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}",FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{queueTrigger}-new",FileAccess.Write)] Stream blobOutput)
        {
            blobInput.CopyTo(blobOutput, 4096);
        }

Olá `Blob` demora de construtor de atributos um `blobPath` parâmetro que especifica o contentor de Olá e nome do blob. Para mais informações sobre esta marcador de posição, consulte [como toouse Azure blob storage com o SDK de WebJobs do Olá](websites-dotnet-webjobs-sdk-storage-blobs-how-to.md),

Quando o atributo de Olá decorates um `Stream` objeto, de outro construtor parâmetro Olá `FileAccess` modo como a leitura, escrita ou leitura/escrita.

Olá exemplo seguinte utiliza uma `CloudBlockBlob` toodelete um blob de objeto. mensagem de fila de saudação é o nome de Olá do blob Olá.

        public static void DeleteBlob(
            [QueueTrigger("deleteblobqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}")] CloudBlockBlob blobToDelete)
        {
            blobToDelete.Delete();
        }

### <a id="pocoblobs"></a>POCO [(simples objeto antigo de CLR](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) mensagens da fila
Para um POCO armazenado como JSON na mensagem de fila de Olá, pode utilizar os marcadores de posição pelo nome propriedades do objeto de Olá na Olá `Queue` do atributo `blobPath` parâmetro. Também pode utilizar [fila os nomes de propriedade de metadados](#queuemetadata) como marcadores de posição.

Olá exemplo seguinte copia um blob tooa novo de blob com uma extensão diferente. mensagem de fila de saudação é um `BlobInformation` objeto inclui `BlobName` e `BlobNameWithoutExtension` propriedades. os nomes de propriedade Olá são utilizados como marcadores de posição no caminho do blob Olá Olá `Blob` atributos.

        public static void CopyBlobPOCO(
            [QueueTrigger("copyblobqueue")] BlobInformation blobInfo,
            [Blob("textblobs/{BlobName}", FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{BlobNameWithoutExtension}.txt", FileAccess.Write)] Stream blobOutput)
        {
            blobInput.CopyTo(blobOutput, 4096);
        }

Olá SDK utiliza Olá [pacote NuGet newtonsoft](http://www.nuget.org/packages/Newtonsoft.Json) tooserialize e anular a serialização de mensagens. Se criar a fila de mensagens num programa que não utiliza o SDK de WebJobs do Olá, pode escrever o código como Olá seguinte exemplo toocreate uma mensagem de fila POCO esse Olá que SDK pode analisar.

        BlobInformation blobInfo = new BlobInformation() { BlobName = "boot.log", BlobNameWithoutExtension = "boot" };
        var queueMessage = new CloudQueueMessage(JsonConvert.SerializeObject(blobInfo));
        logQueue.AddMessage(queueMessage);

Se precisar de toodo algumas funcionam na sua função antes de enlace um objeto de tooan blob, pode utilizar o atributo de Olá no corpo de Olá da função de Olá, [conforme mostrado anteriormente para o atributo de fila de Olá](#ibinder).

### <a id="blobattributetypes"></a>Tipos que pode utilizar Olá Blob de atributo com o
Olá `Blob` atributo pode ser utilizado com Olá tipos seguintes:

* `Stream`(ler ou escrever, utilizando o parâmetro de construtor de FileAccess Olá)
* `TextReader`
* `TextWriter`
* `string`(leitura)
* `out string`(escrever; cria um blob apenas se o parâmetro de cadeia Olá for não nulo quando a função de Olá devolve)
* POCO (leitura)
* saída POCO (escrever; sempre cria um blob, cria como um objeto nulo se POCO parâmetro é nulo quando a função de Olá devolve)
* `CloudBlobStream`(escrita)
* `ICloudBlob`(ler ou escrever)
* `CloudBlockBlob`(ler ou escrever)
* `CloudPageBlob`(ler ou escrever)

## <a id="poison"></a>Como toohandle poison mensagens
Mensagens cujo conteúdo faz com que uma função toofail são denominadas *poison mensagens*. Quando a função de Olá falha, a mensagem da fila de saudação não é eliminada e, eventualmente, é captada novamente, que provocou toobe de ciclo de Olá repetido. Olá SDK automaticamente pode interromper o ciclo de Olá após um número limitado de iterações ou pode fazê-lo manualmente.

### <a name="automatic-poison-message-handling"></a>Processamento de mensagens nocivas automática
Olá SDK irá chamar uma função de segurança too5 vezes tooprocess uma mensagem de fila. Se tentar quinta Olá falhar, mensagem de saudação é fila corrompida foi movida tooa. [Olá número máximo de tentativas é configurável](#config).

nome da fila nocivas Olá *{originalqueuename}*-nocivas. Pode escrever um tooprocess função mensagens da fila nocivas Olá por registá-los ou enviar uma notificação que é necessária atenção manual.

No seguinte Olá de exemplo de Olá `CopyBlob` função irão falhar quando uma mensagem de fila contém o nome de Olá de um blob que não existe. Quando isso acontece, mensagem de saudação é movida da fila de copyblobqueue poison Olá copyblobqueue fila toohello. Olá `ProcessPoisonMessage` , em seguida, os registos Olá a mensagem corrompida foi.

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

Olá ilustração seguinte mostra resultado destas funções consola quando uma mensagem corrompida foi for processada.

![Resultado da consola para processamento de mensagens nocivas](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/poison.png)

### <a name="manual-poison-message-handling"></a>Processamento de mensagens nocivas manual
Pode obter Olá diversas vezes uma mensagem foi captada para processamento através da adição de um `int` com o nome de parâmetro `dequeueCount` tooyour função. Pode, em seguida, verifique Olá anular a contagem no código de função e executar a sua própria mensagem corrompida foi processamento quando o número de Olá excede um limiar, conforme mostrado no seguinte exemplo de Olá.

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

## <a id="config"></a>Como tooset opções de configuração
Pode utilizar Olá `JobHostConfiguration` Olá do tipo tooset seguintes opções de configuração:

* Conjunto de cadeias de ligação do SDK Olá no código.
* Configurar `QueueTrigger` definições, tais como o máximo anular contagem.
* Obter os nomes de fila de configuração.

### <a id="setconnstr"></a>Definir cadeias de ligação do SDK no código
Definir cadeias de ligação do SDK de Olá no código permite-lhe toouse os seus próprios nomes de cadeia de ligação em ficheiros de configuração ou variáveis de ambiente, conforme mostrado no seguinte exemplo de Olá.

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

### <a id="configqueue"></a>Configurar definições de QueueTrigger
Pode configurar Olá definições que se aplicam processamento de mensagens de fila toohello os seguintes:

* Olá número máximo de fila de mensagens que são captado em simultâneo toobe executado em paralelo (a predefinição é 16).
* Olá número máximo de tentativas antes do envio de uma mensagem de fila fila nocivas tooa (a predefinição é 5).
* tempo de espera máximo de Olá antes de consulta novamente quando uma fila está vazia (a predefinição é 1 minuto).

Olá seguinte exemplo mostra como tooconfigure estas definições:

        static void Main(string[] args)
        {
            JobHostConfiguration config = new JobHostConfiguration();
            config.Queues.BatchSize = 8;
            config.Queues.MaxDequeueCount = 4;
            config.Queues.MaxPollingInterval = TimeSpan.FromSeconds(15);
            JobHost host = new JobHost(config);
            host.RunAndBlock();
        }

### <a id="setnamesincode"></a>Definir valores para o SDK de WebJobs os parâmetros do construtor no código
Por vezes, pretende toospecify um nome de fila, um nome de blob ou contentor ou nome de uma tabela no código em vez de codificá-lo. Por exemplo, poderá pretender que nome da fila Olá toospecify para `QueueTrigger` numa variável de ambiente ou ficheiro de configuração.

Pode fazê-lo mediante a transmissão num `NameResolver` objeto toohello `JobHostConfiguration` tipo. Incluir marcadores de posição especiais rodeados por sinais de sinal de percentagem () nos parâmetros de construtor de atributo do SDK de WebJobs e os seus `NameResolver` código especifica Olá valores reais toobe utilizado em vez dos marcadores de posição.

Por exemplo, suponha que pretende toouse uma fila com o nome logqueuetest no ambiente de teste de Olá e um logqueueprod nomeado em produção. Em vez de um nome de fila hard-coded, pretende que o nome de Olá toospecify de uma entrada na Olá `appSettings` coleção que teria o nome de fila real Olá. Se hello `appSettings` chave é logqueue, a função foi aspeto Olá seguinte exemplo.

        public static void WriteLog([QueueTrigger("%logqueue%")] string logMessage)
        {
            Console.WriteLine(logMessage);
        }

O `NameResolver` classe, em seguida, foi possível obter o nome da fila de Olá `appSettings` conforme mostrado no seguinte exemplo de Olá:

        public class QueueNameResolver : INameResolver
        {
            public string Resolve(string name)
            {
                return ConfigurationManager.AppSettings[name].ToString();
            }
        }

Passar Olá `NameResolver` a classe toohello `JobHost` conforme mostrado no seguinte exemplo de Olá de objeto.

        static void Main(string[] args)
        {
            JobHostConfiguration config = new JobHostConfiguration();
            config.NameResolver = new QueueNameResolver();
            JobHost host = new JobHost(config);
            host.RunAndBlock();
        }

**Nota:** fila, tabela e dos nomes blob são resolvidos sempre que uma função é chamada, mas os nomes de contentor do blob são resolvidos apenas quando inicia a aplicação Olá. Não é possível alterar o nome do contentor de blob enquanto Olá tarefa está em execução.

## <a id="manual"></a>Como uma função de tootrigger manualmente
uma função de tootrigger manualmente, utilize Olá `Call` ou `CallAsync` método no Olá `JobHost` objeto e Olá `NoAutomaticTrigger` atributo na função Olá, conforme mostrado no seguinte exemplo de Olá.

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

## <a id="logs"></a>Modo de registo de toowrite
Olá Dashboard mostra os registos em dois locais: página Olá Olá WebJob e página Olá para uma invocação de WebJob específica.

![Registos na página do trabalho Web](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/dashboardapplogs.png)

![Registos na página de invocação de função](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/dashboardlogs.png)

Saída de métodos de consola que tem de chamar uma função ou Olá `Main()` método é apresentado na página do Dashboard Olá para Olá WebJob e não na página Olá para um determinado método de invocação. Saída do objeto de TextWriter Olá que obtém a partir de um parâmetro na sua assinatura do método é apresentado na página do Dashboard Olá para um método de invocação.

Resultado da consola não pode ser ligado tooa determinado método invocação porque Olá consola single-threaded, enquanto muitas funções de tarefas poderão estar em execução em Olá mesmo tempo. É por esse motivo Olá SDK fornece cada invocação de função com o seu próprio objeto de escritor do registo exclusivo.

toowrite [registos de rastreio de aplicação](web-sites-dotnet-troubleshoot-visual-studio.md#logsoverview), utilize `Console.Out` (cria registos marcados como informação) e `Console.Error` (cria registos marcados como erro). Uma alternativa é toouse [rastreio ou TraceSource](http://blogs.msdn.com/b/mcsuksoldev/archive/2014/09/04/adding-trace-to-azure-web-sites-and-web-jobs.aspx), que fornece verboso, aviso, e os níveis de crítico na adição tooInfo e o erro. Os registos de rastreio de aplicações são apresentados nos ficheiros de registo de aplicação web Olá, as tabelas do Azure, ou de blobs do Azure, dependendo de como configurar a sua aplicação web do Azure. Como é verdadeiro de todos os resultados da consola, os registos de aplicações 100 mais recentes Olá também são apresentados na página do Dashboard de Olá para Olá WebJob, não Olá página uma invocação de função.

Resultado da consola é apresentado no Olá Dashboard apenas se o programa de Olá está em execução num trabalho Web do Azure, não se o programa de Olá é executada localmente ou alguns outros ambiente.

Desative o registo de dashboard para cenários de débito elevado. Por predefinição, Olá SDK escreve registos toostorage e esta atividade pode degradar o desempenho quando está a processar muitas mensagens. toodisable registo, defina toonull de cadeia de ligação de dashboard Olá, conforme mostrado no seguinte exemplo de Olá.

        JobHostConfiguration config = new JobHostConfiguration();       
        config.DashboardConnectionString = "";        
        JobHost host = new JobHost(config);
        host.RunAndBlock();

Olá exemplo seguinte mostra várias formas toowrite registos:

        public static void WriteLog(
            [QueueTrigger("logqueue")] string logMessage,
            TextWriter logger)
        {
            Console.WriteLine("Console.Write - " + logMessage);
            Console.Out.WriteLine("Console.Out - " + logMessage);
            Console.Error.WriteLine("Console.Error - " + logMessage);
            logger.WriteLine("TextWriter - " + logMessage);
        }

No Dashboard do SDK de WebJobs Olá, Olá saída de Olá `TextWriter` objeto mostra cópias de segurança quando acede toohello página para um determinado invocação de função e clique em **alternar saída**:

![Clique em ligação de invocação de função](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/dashboardinvocations.png)

![Registos na página de invocação de função](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/dashboardlogs.png)

No Dashboard do SDK de WebJobs Olá, linhas de Olá 100 mais recente da consola de saída Mostrar cópias de segurança quando aceda toohello página Olá WebJob (não para a invocação de função Olá) e clique em **alternar saída**.

![Clique em Ativar/desativar de saída](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/dashboardapplogs.png)

Num WebJob contínuo, os registos de aplicações apresentada na/dados/tarefas/contínua/*{webjobname}*/job_log.txt no sistema de ficheiros de aplicação de web de Olá.

        [09/26/2014 21:01:13 > 491e54: INFO] Console.Write - Hello world!
        [09/26/2014 21:01:13 > 491e54: ERR ] Console.Error - Hello world!
        [09/26/2014 21:01:13 > 491e54: INFO] Console.Out - Hello world!

Numa aplicação Olá BLOBs do Azure registos este aspeto: 2014-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738373502,0,17404,17,Console.Write - Olá, mundo!, 2014-09-26T21:01:13, erro, contosoadsnew, 491e54, 635473620738373502,0,17404,19,Console.Error - Olá, mundo!, 2014-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738529920,0,17404,17,Console.Out - Olá, mundo!,

E no Olá tabela do Azure `Console.Out` e `Console.Error` registos tem o seguinte aspeto:

![Registo de informações na tabela](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/tableinfo.png)

![Registo de erros na tabela](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/tableerror.png)

Se quiser tooplug no seu próprio registo, consulte [neste exemplo](http://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/MiscOperations/Program.cs).

## <a id="errors"></a>Como toohandle erros e configurar os tempos limite
Olá SDK de WebJobs também inclui um [tempo limite](http://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/MiscOperations/Functions.cs) atributo que pode utilizar toocause toobe uma função cancelada se não concluir dentro de um período de tempo especificado. Se pretender tooraise um alerta quando existem demasiados erros ocorrem dentro de um período de tempo especificado, pode utilizar Olá `ErrorTrigger` atributo. Eis um [ErrorTrigger exemplo](https://github.com/Azure/azure-webjobs-sdk-extensions/wiki/Error-Monitoring).

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

Pode também dinamicamente desativar e ativar funções toocontrol se de que podem ser acionadas, utilizando um parâmetro de configuração que pode ser uma definição de aplicação ou o nome de variável de ambiente. Para o código de exemplo, consulte Olá `Disable` atributo em [Olá SDK de WebJobs amostras repositório](https://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/MiscOperations/Functions.cs).

## <a id="nextsteps"></a> Passos seguintes
Este guia forneceu o código de exemplo que mostram como toohandle cenários comuns para trabalhar com as filas do Azure. Para obter mais informações sobre como toouse WebJobs do Azure e Olá SDK de WebJobs, consulte [recursos de recomendada de WebJobs do Azure](http://go.microsoft.com/fwlink/?linkid=390226).
