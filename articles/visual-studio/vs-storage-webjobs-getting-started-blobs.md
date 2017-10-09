---
title: "aaaGet começar a utilizar o blob storage e o Visual Studio serviços ligados (WebJob projetos) | Microsoft Docs"
description: "Como tooget iniciado utilizando o Blob storage num projeto WebJob depois de se ligar tooan storage do Azure com o Visual Studio ligada a serviços."
services: storage
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: 324c9376-0225-4092-9825-5d1bd5550058
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: kraigb
ms.openlocfilehash: 29f2d5e19426d37d815cdf9a1e00abfb1e07ccf6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-blob-storage-and-visual-studio-connected-services-webjob-projects"></a><span data-ttu-id="6909a-103">Introdução ao Blob do Azure Visual Studio e de armazenamento ligado serviços (projetos de trabalho Web)</span><span class="sxs-lookup"><span data-stu-id="6909a-103">Get started with Azure Blob storage and Visual Studio connected services (WebJob projects)</span></span>
[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="6909a-104">Descrição geral</span><span class="sxs-lookup"><span data-stu-id="6909a-104">Overview</span></span>
<span data-ttu-id="6909a-105">Este artigo fornece c# amostras de código que mostram como tootrigger um processo quando um blob do Azure é criado ou atualizado.</span><span class="sxs-lookup"><span data-stu-id="6909a-105">This article provides C# code samples that show how tootrigger a process when an Azure blob is created or updated.</span></span> <span data-ttu-id="6909a-106">Exemplos de código Olá utilizam Olá [SDK de WebJobs](../app-service-web/websites-dotnet-webjobs-sdk.md) versão 1. x.</span><span class="sxs-lookup"><span data-stu-id="6909a-106">hello code samples use hello [WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk.md) version 1.x.</span></span> <span data-ttu-id="6909a-107">Quando adiciona um projeto de WebJob de tooa de conta de armazenamento utilizando Olá Visual Studio **adicionar serviços ligados** caixa de diálogo, pacote NuGet do armazenamento de Azure adequado do Olá está instalado, referências de .NET adequadas Olá são adicionado toohello projeto e cadeias de ligação para a conta de armazenamento Olá são atualizadas no ficheiro App. config de Olá.</span><span class="sxs-lookup"><span data-stu-id="6909a-107">When you add a storage account tooa WebJob project by using hello Visual Studio **Add Connected Services** dialog, hello appropriate Azure Storage NuGet package is installed, hello appropriate .NET references are added toohello project, and connection strings for hello storage account are updated in hello App.config file.</span></span>

## <a name="how-tootrigger-a-function-when-a-blob-is-created-or-updated"></a><span data-ttu-id="6909a-108">Como tootrigger uma função quando um blob é criado ou atualizado</span><span class="sxs-lookup"><span data-stu-id="6909a-108">How tootrigger a function when a blob is created or updated</span></span>
<span data-ttu-id="6909a-109">Esta secção mostra como toouse Olá **BlobTrigger** atributo.</span><span class="sxs-lookup"><span data-stu-id="6909a-109">This section shows how toouse hello **BlobTrigger** attribute.</span></span>

 <span data-ttu-id="6909a-110">**Nota:** Olá toowatch ficheiros de registo de análises do SDK de WebJobs para blobs novos ou alterados.</span><span class="sxs-lookup"><span data-stu-id="6909a-110">**Note:** hello WebJobs SDK scans log files toowatch for new or changed blobs.</span></span> <span data-ttu-id="6909a-111">Este processo é inerentemente lento; uma função pode não obter uma acionada até vários minutos ou já depois de blob Olá é criado.</span><span class="sxs-lookup"><span data-stu-id="6909a-111">This process is inherently slow; a function might not get triggered until several minutes or longer after hello blob is created.</span></span>  <span data-ttu-id="6909a-112">Se a sua aplicação tiver tooprocess blobs imediatamente, Olá recomendado método é toocreate uma mensagem de fila quando criar Olá blob e utilizar Olá [QueueTrigger](../app-service-web/websites-dotnet-webjobs-sdk-storage-queues-how-to.md#trigger) atributo em vez de Olá **BlobTrigger** atributo na função de Olá que processa BLOBs Olá.</span><span class="sxs-lookup"><span data-stu-id="6909a-112">If your application needs tooprocess blobs immediately, hello recommended method is toocreate a queue message when you create hello blob, and use hello [QueueTrigger](../app-service-web/websites-dotnet-webjobs-sdk-storage-queues-how-to.md#trigger) attribute instead of hello **BlobTrigger** attribute on hello function that processes hello blob.</span></span>

### <a name="single-placeholder-for-blob-name-with-extension"></a><span data-ttu-id="6909a-113">Marcador de posição único para o nome do blob com a extensão</span><span class="sxs-lookup"><span data-stu-id="6909a-113">Single placeholder for blob name with extension</span></span>
<span data-ttu-id="6909a-114">Olá exemplo de código seguinte copia blobs de texto que aparecem no Olá *entrada* contentor toohello *saída* contentor:</span><span class="sxs-lookup"><span data-stu-id="6909a-114">hello following code sample copies text blobs that appear in hello *input* container toohello *output* container:</span></span>

        public static void CopyBlob([BlobTrigger("input/{name}")] TextReader input,
            [Blob("output/{name}")] out string output)
        {
            output = input.ReadToEnd();
        }

<span data-ttu-id="6909a-115">o construtor de atributos de Olá assume um parâmetro de cadeia que especifica o nome do contentor de Olá e um marcador de posição para o nome do blob Olá.</span><span class="sxs-lookup"><span data-stu-id="6909a-115">hello attribute constructor takes a string parameter that specifies hello container name and a placeholder for hello blob name.</span></span> <span data-ttu-id="6909a-116">Neste exemplo, se o nome de um blob *Blob1.txt* é criado na Olá *entrada* contentor, a função de Olá cria um blob com o nome *Blob1.txt* no Olá *saída*  contentor.</span><span class="sxs-lookup"><span data-stu-id="6909a-116">In this example, if a blob named *Blob1.txt* is created in hello *input* container, hello function creates a blob named *Blob1.txt* in hello *output* container.</span></span>

<span data-ttu-id="6909a-117">Pode especificar um padrão de nome com o marcador de posição do nome do blob de Olá, conforme mostrado no seguinte código de exemplo de Olá:</span><span class="sxs-lookup"><span data-stu-id="6909a-117">You can specify a name pattern with hello blob name placeholder, as shown in hello following code sample:</span></span>

        public static void CopyBlob([BlobTrigger("input/original-{name}")] TextReader input,
            [Blob("output/copy-{name}")] out string output)
        {
            output = input.ReadToEnd();
        }

<span data-ttu-id="6909a-118">Este código copia apenas blobs que têm nomes a partir do "original-".</span><span class="sxs-lookup"><span data-stu-id="6909a-118">This code copies only blobs that have names beginning with "original-".</span></span> <span data-ttu-id="6909a-119">Por exemplo, *original Blob1.txt* no Olá *entrada* contentor é copiado demasiado*cópia Blob1.txt* no Olá *saída* contentor.</span><span class="sxs-lookup"><span data-stu-id="6909a-119">For example, *original-Blob1.txt* in hello *input* container is copied too*copy-Blob1.txt* in hello *output* container.</span></span>

<span data-ttu-id="6909a-120">Se precisar de toospecify um padrão de nome para nomes de blob que tenham chavetas no nome de Olá, faça duplo chavetas Olá.</span><span class="sxs-lookup"><span data-stu-id="6909a-120">If you need toospecify a name pattern for blob names that have curly braces in hello name, double hello curly braces.</span></span> <span data-ttu-id="6909a-121">Por exemplo, se pretender que os blobs toofind Olá *imagens* contentor que têm nomes como esta:</span><span class="sxs-lookup"><span data-stu-id="6909a-121">For example, if you want toofind blobs in hello *images* container that have names like this:</span></span>

        {20140101}-soundfile.mp3

<span data-ttu-id="6909a-122">Utilize esta opção para o seu padrão de:</span><span class="sxs-lookup"><span data-stu-id="6909a-122">use this for your pattern:</span></span>

        images/{{20140101}}-{name}

<span data-ttu-id="6909a-123">Exemplo de Olá, Olá *nome* valor do marcador de posição seria *soundfile.mp3*.</span><span class="sxs-lookup"><span data-stu-id="6909a-123">In hello example, hello *name* placeholder value would be *soundfile.mp3*.</span></span>

### <a name="separate-blob-name-and-extension-placeholders"></a><span data-ttu-id="6909a-124">Marcadores de posição de blob separado, nome e extensão</span><span class="sxs-lookup"><span data-stu-id="6909a-124">Separate blob name and extension placeholders</span></span>
<span data-ttu-id="6909a-125">Olá seguintes alterações de exemplo de código Olá extensão de ficheiro como copia blobs que aparecem no Olá *entrada* contentor toohello *saída* contentor.</span><span class="sxs-lookup"><span data-stu-id="6909a-125">hello following code sample changes hello file extension as it copies blobs that appear in hello *input* container toohello *output* container.</span></span> <span data-ttu-id="6909a-126">os registos de código Olá extensão Olá Olá *entrada* blob e define extensão Olá Olá *saída* blob demasiado*. txt*.</span><span class="sxs-lookup"><span data-stu-id="6909a-126">hello code logs hello extension of hello *input* blob and sets hello extension of hello *output* blob too*.txt*.</span></span>

        public static void CopyBlobToTxtFile([BlobTrigger("input/{name}.{ext}")] TextReader input,
            [Blob("output/{name}.txt")] out string output,
            string name,
            string ext,
            TextWriter logger)
        {
            logger.WriteLine("Blob name:" + name);
            logger.WriteLine("Blob extension:" + ext);
            output = input.ReadToEnd();
        }

## <a name="types-that-you-can-bind-tooblobs"></a><span data-ttu-id="6909a-127">Tipos de que é possível vincular tooblobs</span><span class="sxs-lookup"><span data-stu-id="6909a-127">Types that you can bind tooblobs</span></span>
<span data-ttu-id="6909a-128">Pode utilizar Olá **BlobTrigger** atributo em Olá tipos seguintes:</span><span class="sxs-lookup"><span data-stu-id="6909a-128">You can use hello **BlobTrigger** attribute on hello following types:</span></span>

* <span data-ttu-id="6909a-129">**cadeia**</span><span class="sxs-lookup"><span data-stu-id="6909a-129">**string**</span></span>
* <span data-ttu-id="6909a-130">**TextReader**</span><span class="sxs-lookup"><span data-stu-id="6909a-130">**TextReader**</span></span>
* <span data-ttu-id="6909a-131">**Fluxo**</span><span class="sxs-lookup"><span data-stu-id="6909a-131">**Stream**</span></span>
* <span data-ttu-id="6909a-132">**ICloudBlob**</span><span class="sxs-lookup"><span data-stu-id="6909a-132">**ICloudBlob**</span></span>
* <span data-ttu-id="6909a-133">**CloudBlockBlob**</span><span class="sxs-lookup"><span data-stu-id="6909a-133">**CloudBlockBlob**</span></span>
* <span data-ttu-id="6909a-134">**CloudPageBlob**</span><span class="sxs-lookup"><span data-stu-id="6909a-134">**CloudPageBlob**</span></span>
* <span data-ttu-id="6909a-135">Outros tipos de serialização anulados pelo [ICloudBlobStreamBinder](#getting-serialized-blob-content-by-using-icloudblobstreambinder)</span><span class="sxs-lookup"><span data-stu-id="6909a-135">Other types deserialized by [ICloudBlobStreamBinder](#getting-serialized-blob-content-by-using-icloudblobstreambinder)</span></span>

<span data-ttu-id="6909a-136">Se quiser toowork diretamente com Olá conta do storage do Azure, também pode adicionar um **CloudStorageAccount** a assinatura do método toohello parâmetro.</span><span class="sxs-lookup"><span data-stu-id="6909a-136">If you want toowork directly with hello Azure storage account, you can also add a **CloudStorageAccount** parameter toohello method signature.</span></span>

## <a name="getting-text-blob-content-by-binding-toostring"></a><span data-ttu-id="6909a-137">Ao obter conteúdo de blob de texto por toostring de enlace</span><span class="sxs-lookup"><span data-stu-id="6909a-137">Getting text blob content by binding toostring</span></span>
<span data-ttu-id="6909a-138">Se os blobs de texto são esperados, **BlobTrigger** podem ser aplicado tooa **cadeia** parâmetro.</span><span class="sxs-lookup"><span data-stu-id="6909a-138">If text blobs are expected, **BlobTrigger** can be applied tooa **string** parameter.</span></span> <span data-ttu-id="6909a-139">Olá exemplo de código seguinte associa um tooa de blob de texto **cadeia** com o nome de parâmetro **logMessage**.</span><span class="sxs-lookup"><span data-stu-id="6909a-139">hello following code sample binds a text blob tooa **string** parameter named **logMessage**.</span></span> <span data-ttu-id="6909a-140">a função Olá utiliza esse parâmetro toowrite Olá conteúdo Olá blob toohello dashboard do SDK de WebJobs.</span><span class="sxs-lookup"><span data-stu-id="6909a-140">hello function uses that parameter toowrite hello contents of hello blob toohello WebJobs SDK dashboard.</span></span>

        public static void WriteLog([BlobTrigger("input/{name}")] string logMessage,
            string name,
            TextWriter logger)
        {
             logger.WriteLine("Blob name: {0}", name);
             logger.WriteLine("Content:");
             logger.WriteLine(logMessage);
        }

## <a name="getting-serialized-blob-content-by-using-icloudblobstreambinder"></a><span data-ttu-id="6909a-141">Introdução ao serializar o conteúdo de blob utilizando ICloudBlobStreamBinder</span><span class="sxs-lookup"><span data-stu-id="6909a-141">Getting serialized blob content by using ICloudBlobStreamBinder</span></span>
<span data-ttu-id="6909a-142">Olá exemplo de código seguinte utiliza uma classe que implementa **ICloudBlobStreamBinder** tooenable Olá **BlobTrigger** toobind toohello um blob de atributo **WebImage** tipo.</span><span class="sxs-lookup"><span data-stu-id="6909a-142">hello following code sample uses a class that implements **ICloudBlobStreamBinder** tooenable hello **BlobTrigger** attribute toobind a blob toohello **WebImage** type.</span></span>

        public static void WaterMark(
            [BlobTrigger("images3/{name}")] WebImage input,
            [Blob("images3-watermarked/{name}")] out WebImage output)
        {
            output = input.AddTextWatermark("WebJobs SDK",
                horizontalAlign: "Center", verticalAlign: "Middle",
                fontSize: 48, opacity: 50);
        }
        public static void Resize(
            [BlobTrigger("images3-watermarked/{name}")] WebImage input,
            [Blob("images3-resized/{name}")] out WebImage output)
        {
            var width = 180;
            var height = Convert.ToInt32(input.Height * 180 / input.Width);
            output = input.Resize(width, height);
        }

<span data-ttu-id="6909a-143">Olá **WebImage** enlace código é fornecido num **WebImageBinder** classe que deriva de **ICloudBlobStreamBinder**.</span><span class="sxs-lookup"><span data-stu-id="6909a-143">hello **WebImage** binding code is provided in a **WebImageBinder** class that derives from **ICloudBlobStreamBinder**.</span></span>

        public class WebImageBinder : ICloudBlobStreamBinder<WebImage>
        {
            public Task<WebImage> ReadFromStreamAsync(Stream input,
                System.Threading.CancellationToken cancellationToken)
            {
                return Task.FromResult<WebImage>(new WebImage(input));
            }
            public Task WriteToStreamAsync(WebImage value, Stream output,
                System.Threading.CancellationToken cancellationToken)
            {
                var bytes = value.GetBytes();
                return output.WriteAsync(bytes, 0, bytes.Length, cancellationToken);
            }
        }

## <a name="how-toohandle-poison-blobs"></a><span data-ttu-id="6909a-144">Como toohandle poison blobs</span><span class="sxs-lookup"><span data-stu-id="6909a-144">How toohandle poison blobs</span></span>
<span data-ttu-id="6909a-145">Quando um **BlobTrigger** função falhar, Olá SDK denomina-novo, no caso de falha de Olá foi causada por um erro transitório.</span><span class="sxs-lookup"><span data-stu-id="6909a-145">When a **BlobTrigger** function fails, hello SDK calls it again, in case hello failure was caused by a transient error.</span></span> <span data-ttu-id="6909a-146">Se a falha de Olá é causada por conteúdo Olá do blob Olá, função Olá falha sempre que este tenta blob de Olá tooprocess.</span><span class="sxs-lookup"><span data-stu-id="6909a-146">If hello failure is caused by hello content of hello blob, hello function fails every time it tries tooprocess hello blob.</span></span> <span data-ttu-id="6909a-147">Por predefinição, o Olá SDK chama uma função de segurança too5 vezes para um blob especificado.</span><span class="sxs-lookup"><span data-stu-id="6909a-147">By default, hello SDK calls a function up too5 times for a given blob.</span></span> <span data-ttu-id="6909a-148">Se tentar quinta Olá falhar, Olá SDK adiciona uma fila de tooa mensagem com o nome *webjobs-blobtrigger-poison*.</span><span class="sxs-lookup"><span data-stu-id="6909a-148">If hello fifth try fails, hello SDK adds a message tooa queue named *webjobs-blobtrigger-poison*.</span></span>

<span data-ttu-id="6909a-149">Olá número máximo de tentativas é configurável.</span><span class="sxs-lookup"><span data-stu-id="6909a-149">hello maximum number of retries is configurable.</span></span> <span data-ttu-id="6909a-150">Olá mesmo [MaxDequeueCount](../app-service-web/websites-dotnet-webjobs-sdk-storage-queues-how-to.md#configqueue) definição é utilizada para processar de blob nocivas e processamento de mensagens de fila nocivas.</span><span class="sxs-lookup"><span data-stu-id="6909a-150">hello same [MaxDequeueCount](../app-service-web/websites-dotnet-webjobs-sdk-storage-queues-how-to.md#configqueue) setting is used for poison blob handling and poison queue message handling.</span></span>

<span data-ttu-id="6909a-151">mensagem de fila de saudação para blobs nocivas é um objeto JSON que contém Olá seguintes propriedades:</span><span class="sxs-lookup"><span data-stu-id="6909a-151">hello queue message for poison blobs is a JSON object that contains hello following properties:</span></span>

* <span data-ttu-id="6909a-152">FunctionId (no formato de Olá *{nome do WebJob}*. Funções. *{Nome da função}*, por exemplo: WebJob1.Functions.CopyBlob)</span><span class="sxs-lookup"><span data-stu-id="6909a-152">FunctionId (in hello format *{WebJob name}*.Functions.*{Function name}*, for example: WebJob1.Functions.CopyBlob)</span></span>
* <span data-ttu-id="6909a-153">BlobType ("BlockBlob" ou "PageBlob")</span><span class="sxs-lookup"><span data-stu-id="6909a-153">BlobType ("BlockBlob" or "PageBlob")</span></span>
* <span data-ttu-id="6909a-154">ContainerName</span><span class="sxs-lookup"><span data-stu-id="6909a-154">ContainerName</span></span>
* <span data-ttu-id="6909a-155">BlobName</span><span class="sxs-lookup"><span data-stu-id="6909a-155">BlobName</span></span>
* <span data-ttu-id="6909a-156">ETag (um identificador de versão de blob, por exemplo: "0x8D1DC6E70A277EF")</span><span class="sxs-lookup"><span data-stu-id="6909a-156">ETag (a blob version identifier, for example: "0x8D1DC6E70A277EF")</span></span>

<span data-ttu-id="6909a-157">No seguinte Olá código de exemplo, hello **CopyBlob** função tem o código que faz com que esta toofail sempre que é chamado.</span><span class="sxs-lookup"><span data-stu-id="6909a-157">In hello following code sample, hello **CopyBlob** function has code that causes it toofail every time it's called.</span></span> <span data-ttu-id="6909a-158">Depois de Olá SDK denomina-o para o número máximo de Olá de tentativas, é criada uma mensagem na fila de blob nocivas Olá e essa mensagem é processada por Olá **LogPoisonBlob** função.</span><span class="sxs-lookup"><span data-stu-id="6909a-158">After hello SDK calls it for hello maximum number of retries, a message is created on hello poison blob queue, and that message is processed by hello **LogPoisonBlob** function.</span></span>

        public static void CopyBlob([BlobTrigger("input/{name}")] TextReader input,
            [Blob("textblobs/output-{name}")] out string output)
        {
            throw new Exception("Exception for testing poison blob handling");
            output = input.ReadToEnd();
        }

        public static void LogPoisonBlob(
        [QueueTrigger("webjobs-blobtrigger-poison")] PoisonBlobMessage message,
            TextWriter logger)
        {
            logger.WriteLine("FunctionId: {0}", message.FunctionId);
            logger.WriteLine("BlobType: {0}", message.BlobType);
            logger.WriteLine("ContainerName: {0}", message.ContainerName);
            logger.WriteLine("BlobName: {0}", message.BlobName);
            logger.WriteLine("ETag: {0}", message.ETag);
        }

<span data-ttu-id="6909a-159">Olá SDK deserializes automaticamente a mensagem de JSON de saudação.</span><span class="sxs-lookup"><span data-stu-id="6909a-159">hello SDK automatically deserializes hello JSON message.</span></span> <span data-ttu-id="6909a-160">Eis Olá **PoisonBlobMessage** classe:</span><span class="sxs-lookup"><span data-stu-id="6909a-160">Here is hello **PoisonBlobMessage** class:</span></span>

        public class PoisonBlobMessage
        {
            public string FunctionId { get; set; }
            public string BlobType { get; set; }
            public string ContainerName { get; set; }
            public string BlobName { get; set; }
            public string ETag { get; set; }
        }

### <a name="blob-polling-algorithm"></a><span data-ttu-id="6909a-161">Algoritmo de consulta de blob</span><span class="sxs-lookup"><span data-stu-id="6909a-161">Blob polling algorithm</span></span>
<span data-ttu-id="6909a-162">Olá SDK de WebJobs analisa todos os contentores especificados pelo **BlobTrigger** atributos no início da aplicação.</span><span class="sxs-lookup"><span data-stu-id="6909a-162">hello WebJobs SDK scans all containers specified by **BlobTrigger** attributes at application start.</span></span> <span data-ttu-id="6909a-163">Numa conta do storage grande esta análise pode demorar algum tempo, pelo que poderá ser tempo antes de encontram-se os novos blobs e **BlobTrigger** funções são executadas.</span><span class="sxs-lookup"><span data-stu-id="6909a-163">In a large storage account this scan can take some time, so it might be a while before new blobs are found and **BlobTrigger** functions are executed.</span></span>

<span data-ttu-id="6909a-164">Olá que SDK lê periodicamente a partir do armazenamento de BLOBs de Olá toodetect blobs nova ou alterada após o início de aplicações, os registos.</span><span class="sxs-lookup"><span data-stu-id="6909a-164">toodetect new or changed blobs after application start, hello SDK periodically reads from hello blob storage logs.</span></span> <span data-ttu-id="6909a-165">Olá blob registos são colocado na memória intermédia e só fisicamente escrever cada 10 minutos ou por isso, por isso, poderá existir atraso significativo depois de um blob é criado ou atualizado antes de Olá correspondente **BlobTrigger** executa a função.</span><span class="sxs-lookup"><span data-stu-id="6909a-165">hello blob logs are buffered and only get physically written every 10 minutes or so, so there may be significant delay after a blob is created or updated before hello corresponding **BlobTrigger** function executes.</span></span>

<span data-ttu-id="6909a-166">Há uma exceção para blobs que criar utilizando Olá **Blob** atributo.</span><span class="sxs-lookup"><span data-stu-id="6909a-166">There is an exception for blobs that you create by using hello **Blob** attribute.</span></span> <span data-ttu-id="6909a-167">Quando Olá SDK de WebJobs cria um novo blob, estes passam blob novo Olá imediatamente tooany correspondente **BlobTrigger** funções.</span><span class="sxs-lookup"><span data-stu-id="6909a-167">When hello WebJobs SDK creates a new blob, it passes hello new blob immediately tooany matching **BlobTrigger** functions.</span></span> <span data-ttu-id="6909a-168">Por conseguinte, se tiver uma cadeia de blob entradas e saídas, Olá SDK pode processá-los com eficiência.</span><span class="sxs-lookup"><span data-stu-id="6909a-168">Therefore if you have a chain of blob inputs and outputs, hello SDK can process them efficiently.</span></span> <span data-ttu-id="6909a-169">Mas se pretender executar o blob de funções de processamento para blobs que são criados ou atualizados através de outros meios de latência baixa, recomendamos que utilize **QueueTrigger** vez **BlobTrigger**.</span><span class="sxs-lookup"><span data-stu-id="6909a-169">But if you want low latency running your blob processing functions for blobs that are created or updated by other means, we recommend using **QueueTrigger** rather than **BlobTrigger**.</span></span>

### <a name="blob-receipts"></a><span data-ttu-id="6909a-170">Recibos de blob</span><span class="sxs-lookup"><span data-stu-id="6909a-170">Blob receipts</span></span>
<span data-ttu-id="6909a-171">Olá SDK de WebJobs certifica-se de que nenhum **BlobTrigger** função obtém chamada mais do que uma vez para Olá mesmo novas ou atualizadas blob.</span><span class="sxs-lookup"><span data-stu-id="6909a-171">hello WebJobs SDK makes sure that no **BlobTrigger** function gets called more than once for hello same new or updated blob.</span></span> <span data-ttu-id="6909a-172">Fazê-lo, mantendo *blob recibos* na ordem toodetermine se uma versão de blob especificado foi processada.</span><span class="sxs-lookup"><span data-stu-id="6909a-172">It does this by maintaining *blob receipts* in order toodetermine if a given blob version has been processed.</span></span>

<span data-ttu-id="6909a-173">Blob recibos são armazenados num contentor com o nome *anfitriões de webjobs do azure* na conta de armazenamento do Azure Olá especificada pelo Olá AzureWebJobsStorage cadeia de ligação.</span><span class="sxs-lookup"><span data-stu-id="6909a-173">Blob receipts are stored in a container named *azure-webjobs-hosts* in hello Azure storage account specified by hello AzureWebJobsStorage connection string.</span></span> <span data-ttu-id="6909a-174">Um recibo de blob tem Olá seguintes informações:</span><span class="sxs-lookup"><span data-stu-id="6909a-174">A blob receipt has hello following  information:</span></span>

* <span data-ttu-id="6909a-175">Olá, a função que foi chamada para BLOBs Olá ("*{nome do WebJob}*. Funções. *{Nome da função}*", por exemplo:"WebJob1.Functions.CopyBlob")</span><span class="sxs-lookup"><span data-stu-id="6909a-175">hello function that was called for hello blob ("*{WebJob name}*.Functions.*{Function name}*", for example: "WebJob1.Functions.CopyBlob")</span></span>
* <span data-ttu-id="6909a-176">nome do contentor Olá</span><span class="sxs-lookup"><span data-stu-id="6909a-176">hello container name</span></span>
* <span data-ttu-id="6909a-177">tipo de blob Olá ("BlockBlob" ou "PageBlob")</span><span class="sxs-lookup"><span data-stu-id="6909a-177">hello blob type ("BlockBlob" or "PageBlob")</span></span>
* <span data-ttu-id="6909a-178">nome do blob Olá</span><span class="sxs-lookup"><span data-stu-id="6909a-178">hello blob name</span></span>
* <span data-ttu-id="6909a-179">Olá ETag (um identificador de versão de blob, por exemplo: "0x8D1DC6E70A277EF")</span><span class="sxs-lookup"><span data-stu-id="6909a-179">hello ETag (a blob version identifier, for example: "0x8D1DC6E70A277EF")</span></span>

<span data-ttu-id="6909a-180">Se quiser tooforce reprocessamento de um blob, pode eliminar manualmente a receção de blob Olá para esse blob do Olá *anfitriões de webjobs do azure* contentor.</span><span class="sxs-lookup"><span data-stu-id="6909a-180">If you want tooforce reprocessing of a blob, you can manually delete hello blob receipt for that blob from hello *azure-webjobs-hosts* container.</span></span>

## <a name="related-topics-covered-by-hello-queues-article"></a><span data-ttu-id="6909a-181">Tópicos relacionados abrangidos por artigo de filas Olá</span><span class="sxs-lookup"><span data-stu-id="6909a-181">Related topics covered by hello queues article</span></span>
<span data-ttu-id="6909a-182">Para obter informações sobre como processamento de blob toohandle acionado por uma mensagem de fila ou para WebJobs cenários do SDK não tooblob específica de processamento, consulte [como toouse Azure fila de armazenamento com Olá SDK de WebJobs](../app-service-web/websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span><span class="sxs-lookup"><span data-stu-id="6909a-182">For information about how toohandle blob processing triggered by a queue message, or for WebJobs SDK scenarios not specific tooblob processing, see [How toouse Azure queue storage with hello WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span></span>

<span data-ttu-id="6909a-183">Tópicos relacionados abordados esse artigo incluem o seguinte Olá:</span><span class="sxs-lookup"><span data-stu-id="6909a-183">Related topics covered in that article include hello following:</span></span>

* <span data-ttu-id="6909a-184">Async funções</span><span class="sxs-lookup"><span data-stu-id="6909a-184">Async functions</span></span>
* <span data-ttu-id="6909a-185">Várias instâncias</span><span class="sxs-lookup"><span data-stu-id="6909a-185">Multiple instances</span></span>
* <span data-ttu-id="6909a-186">Encerramento correto</span><span class="sxs-lookup"><span data-stu-id="6909a-186">Graceful shutdown</span></span>
* <span data-ttu-id="6909a-187">Utilizar o SDK de WebJobs atributos no corpo de Olá de uma função</span><span class="sxs-lookup"><span data-stu-id="6909a-187">Use WebJobs SDK attributes in hello body of a function</span></span>
* <span data-ttu-id="6909a-188">Conjunto de cadeias de ligação do SDK Olá no código.</span><span class="sxs-lookup"><span data-stu-id="6909a-188">Set hello SDK connection strings in code.</span></span>
* <span data-ttu-id="6909a-189">Definir valores para o SDK de WebJobs os parâmetros do construtor no código</span><span class="sxs-lookup"><span data-stu-id="6909a-189">Set values for WebJobs SDK constructor parameters in code</span></span>
* <span data-ttu-id="6909a-190">Configurar **MaxDequeueCount** para processamento de blob nocivas.</span><span class="sxs-lookup"><span data-stu-id="6909a-190">Configure **MaxDequeueCount** for poison blob handling.</span></span>
* <span data-ttu-id="6909a-191">Acionar manualmente uma função</span><span class="sxs-lookup"><span data-stu-id="6909a-191">Trigger a function manually</span></span>
* <span data-ttu-id="6909a-192">Escrever registos</span><span class="sxs-lookup"><span data-stu-id="6909a-192">Write logs</span></span>

## <a name="next-steps"></a><span data-ttu-id="6909a-193">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="6909a-193">Next steps</span></span>
<span data-ttu-id="6909a-194">Este artigo forneceu exemplos de código que mostram como blobs toohandle cenários comuns para trabalhar com o Azure.</span><span class="sxs-lookup"><span data-stu-id="6909a-194">This article has provided code samples that show how toohandle common scenarios for working with Azure blobs.</span></span> <span data-ttu-id="6909a-195">Para obter mais informações sobre como toouse WebJobs do Azure e Olá SDK de WebJobs, consulte [recursos de documentação de WebJobs do Azure](http://go.microsoft.com/fwlink/?linkid=390226).</span><span class="sxs-lookup"><span data-stu-id="6909a-195">For more information about how toouse Azure WebJobs and hello WebJobs SDK, see [Azure WebJobs documentation resources](http://go.microsoft.com/fwlink/?linkid=390226).</span></span>

