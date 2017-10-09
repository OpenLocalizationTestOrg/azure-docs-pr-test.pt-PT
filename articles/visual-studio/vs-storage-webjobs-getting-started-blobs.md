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
# <a name="get-started-with-azure-blob-storage-and-visual-studio-connected-services-webjob-projects"></a>Introdução ao Blob do Azure Visual Studio e de armazenamento ligado serviços (projetos de trabalho Web)
[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a>Descrição geral
Este artigo fornece c# amostras de código que mostram como tootrigger um processo quando um blob do Azure é criado ou atualizado. Exemplos de código Olá utilizam Olá [SDK de WebJobs](../app-service-web/websites-dotnet-webjobs-sdk.md) versão 1. x. Quando adiciona um projeto de WebJob de tooa de conta de armazenamento utilizando Olá Visual Studio **adicionar serviços ligados** caixa de diálogo, pacote NuGet do armazenamento de Azure adequado do Olá está instalado, referências de .NET adequadas Olá são adicionado toohello projeto e cadeias de ligação para a conta de armazenamento Olá são atualizadas no ficheiro App. config de Olá.

## <a name="how-tootrigger-a-function-when-a-blob-is-created-or-updated"></a>Como tootrigger uma função quando um blob é criado ou atualizado
Esta secção mostra como toouse Olá **BlobTrigger** atributo.

 **Nota:** Olá toowatch ficheiros de registo de análises do SDK de WebJobs para blobs novos ou alterados. Este processo é inerentemente lento; uma função pode não obter uma acionada até vários minutos ou já depois de blob Olá é criado.  Se a sua aplicação tiver tooprocess blobs imediatamente, Olá recomendado método é toocreate uma mensagem de fila quando criar Olá blob e utilizar Olá [QueueTrigger](../app-service-web/websites-dotnet-webjobs-sdk-storage-queues-how-to.md#trigger) atributo em vez de Olá **BlobTrigger** atributo na função de Olá que processa BLOBs Olá.

### <a name="single-placeholder-for-blob-name-with-extension"></a>Marcador de posição único para o nome do blob com a extensão
Olá exemplo de código seguinte copia blobs de texto que aparecem no Olá *entrada* contentor toohello *saída* contentor:

        public static void CopyBlob([BlobTrigger("input/{name}")] TextReader input,
            [Blob("output/{name}")] out string output)
        {
            output = input.ReadToEnd();
        }

o construtor de atributos de Olá assume um parâmetro de cadeia que especifica o nome do contentor de Olá e um marcador de posição para o nome do blob Olá. Neste exemplo, se o nome de um blob *Blob1.txt* é criado na Olá *entrada* contentor, a função de Olá cria um blob com o nome *Blob1.txt* no Olá *saída*  contentor.

Pode especificar um padrão de nome com o marcador de posição do nome do blob de Olá, conforme mostrado no seguinte código de exemplo de Olá:

        public static void CopyBlob([BlobTrigger("input/original-{name}")] TextReader input,
            [Blob("output/copy-{name}")] out string output)
        {
            output = input.ReadToEnd();
        }

Este código copia apenas blobs que têm nomes a partir do "original-". Por exemplo, *original Blob1.txt* no Olá *entrada* contentor é copiado demasiado*cópia Blob1.txt* no Olá *saída* contentor.

Se precisar de toospecify um padrão de nome para nomes de blob que tenham chavetas no nome de Olá, faça duplo chavetas Olá. Por exemplo, se pretender que os blobs toofind Olá *imagens* contentor que têm nomes como esta:

        {20140101}-soundfile.mp3

Utilize esta opção para o seu padrão de:

        images/{{20140101}}-{name}

Exemplo de Olá, Olá *nome* valor do marcador de posição seria *soundfile.mp3*.

### <a name="separate-blob-name-and-extension-placeholders"></a>Marcadores de posição de blob separado, nome e extensão
Olá seguintes alterações de exemplo de código Olá extensão de ficheiro como copia blobs que aparecem no Olá *entrada* contentor toohello *saída* contentor. os registos de código Olá extensão Olá Olá *entrada* blob e define extensão Olá Olá *saída* blob demasiado*. txt*.

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

## <a name="types-that-you-can-bind-tooblobs"></a>Tipos de que é possível vincular tooblobs
Pode utilizar Olá **BlobTrigger** atributo em Olá tipos seguintes:

* **cadeia**
* **TextReader**
* **Fluxo**
* **ICloudBlob**
* **CloudBlockBlob**
* **CloudPageBlob**
* Outros tipos de serialização anulados pelo [ICloudBlobStreamBinder](#getting-serialized-blob-content-by-using-icloudblobstreambinder)

Se quiser toowork diretamente com Olá conta do storage do Azure, também pode adicionar um **CloudStorageAccount** a assinatura do método toohello parâmetro.

## <a name="getting-text-blob-content-by-binding-toostring"></a>Ao obter conteúdo de blob de texto por toostring de enlace
Se os blobs de texto são esperados, **BlobTrigger** podem ser aplicado tooa **cadeia** parâmetro. Olá exemplo de código seguinte associa um tooa de blob de texto **cadeia** com o nome de parâmetro **logMessage**. a função Olá utiliza esse parâmetro toowrite Olá conteúdo Olá blob toohello dashboard do SDK de WebJobs.

        public static void WriteLog([BlobTrigger("input/{name}")] string logMessage,
            string name,
            TextWriter logger)
        {
             logger.WriteLine("Blob name: {0}", name);
             logger.WriteLine("Content:");
             logger.WriteLine(logMessage);
        }

## <a name="getting-serialized-blob-content-by-using-icloudblobstreambinder"></a>Introdução ao serializar o conteúdo de blob utilizando ICloudBlobStreamBinder
Olá exemplo de código seguinte utiliza uma classe que implementa **ICloudBlobStreamBinder** tooenable Olá **BlobTrigger** toobind toohello um blob de atributo **WebImage** tipo.

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

Olá **WebImage** enlace código é fornecido num **WebImageBinder** classe que deriva de **ICloudBlobStreamBinder**.

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

## <a name="how-toohandle-poison-blobs"></a>Como toohandle poison blobs
Quando um **BlobTrigger** função falhar, Olá SDK denomina-novo, no caso de falha de Olá foi causada por um erro transitório. Se a falha de Olá é causada por conteúdo Olá do blob Olá, função Olá falha sempre que este tenta blob de Olá tooprocess. Por predefinição, o Olá SDK chama uma função de segurança too5 vezes para um blob especificado. Se tentar quinta Olá falhar, Olá SDK adiciona uma fila de tooa mensagem com o nome *webjobs-blobtrigger-poison*.

Olá número máximo de tentativas é configurável. Olá mesmo [MaxDequeueCount](../app-service-web/websites-dotnet-webjobs-sdk-storage-queues-how-to.md#configqueue) definição é utilizada para processar de blob nocivas e processamento de mensagens de fila nocivas.

mensagem de fila de saudação para blobs nocivas é um objeto JSON que contém Olá seguintes propriedades:

* FunctionId (no formato de Olá *{nome do WebJob}*. Funções. *{Nome da função}*, por exemplo: WebJob1.Functions.CopyBlob)
* BlobType ("BlockBlob" ou "PageBlob")
* ContainerName
* BlobName
* ETag (um identificador de versão de blob, por exemplo: "0x8D1DC6E70A277EF")

No seguinte Olá código de exemplo, hello **CopyBlob** função tem o código que faz com que esta toofail sempre que é chamado. Depois de Olá SDK denomina-o para o número máximo de Olá de tentativas, é criada uma mensagem na fila de blob nocivas Olá e essa mensagem é processada por Olá **LogPoisonBlob** função.

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

Olá SDK deserializes automaticamente a mensagem de JSON de saudação. Eis Olá **PoisonBlobMessage** classe:

        public class PoisonBlobMessage
        {
            public string FunctionId { get; set; }
            public string BlobType { get; set; }
            public string ContainerName { get; set; }
            public string BlobName { get; set; }
            public string ETag { get; set; }
        }

### <a name="blob-polling-algorithm"></a>Algoritmo de consulta de blob
Olá SDK de WebJobs analisa todos os contentores especificados pelo **BlobTrigger** atributos no início da aplicação. Numa conta do storage grande esta análise pode demorar algum tempo, pelo que poderá ser tempo antes de encontram-se os novos blobs e **BlobTrigger** funções são executadas.

Olá que SDK lê periodicamente a partir do armazenamento de BLOBs de Olá toodetect blobs nova ou alterada após o início de aplicações, os registos. Olá blob registos são colocado na memória intermédia e só fisicamente escrever cada 10 minutos ou por isso, por isso, poderá existir atraso significativo depois de um blob é criado ou atualizado antes de Olá correspondente **BlobTrigger** executa a função.

Há uma exceção para blobs que criar utilizando Olá **Blob** atributo. Quando Olá SDK de WebJobs cria um novo blob, estes passam blob novo Olá imediatamente tooany correspondente **BlobTrigger** funções. Por conseguinte, se tiver uma cadeia de blob entradas e saídas, Olá SDK pode processá-los com eficiência. Mas se pretender executar o blob de funções de processamento para blobs que são criados ou atualizados através de outros meios de latência baixa, recomendamos que utilize **QueueTrigger** vez **BlobTrigger**.

### <a name="blob-receipts"></a>Recibos de blob
Olá SDK de WebJobs certifica-se de que nenhum **BlobTrigger** função obtém chamada mais do que uma vez para Olá mesmo novas ou atualizadas blob. Fazê-lo, mantendo *blob recibos* na ordem toodetermine se uma versão de blob especificado foi processada.

Blob recibos são armazenados num contentor com o nome *anfitriões de webjobs do azure* na conta de armazenamento do Azure Olá especificada pelo Olá AzureWebJobsStorage cadeia de ligação. Um recibo de blob tem Olá seguintes informações:

* Olá, a função que foi chamada para BLOBs Olá ("*{nome do WebJob}*. Funções. *{Nome da função}*", por exemplo:"WebJob1.Functions.CopyBlob")
* nome do contentor Olá
* tipo de blob Olá ("BlockBlob" ou "PageBlob")
* nome do blob Olá
* Olá ETag (um identificador de versão de blob, por exemplo: "0x8D1DC6E70A277EF")

Se quiser tooforce reprocessamento de um blob, pode eliminar manualmente a receção de blob Olá para esse blob do Olá *anfitriões de webjobs do azure* contentor.

## <a name="related-topics-covered-by-hello-queues-article"></a>Tópicos relacionados abrangidos por artigo de filas Olá
Para obter informações sobre como processamento de blob toohandle acionado por uma mensagem de fila ou para WebJobs cenários do SDK não tooblob específica de processamento, consulte [como toouse Azure fila de armazenamento com Olá SDK de WebJobs](../app-service-web/websites-dotnet-webjobs-sdk-storage-queues-how-to.md).

Tópicos relacionados abordados esse artigo incluem o seguinte Olá:

* Async funções
* Várias instâncias
* Encerramento correto
* Utilizar o SDK de WebJobs atributos no corpo de Olá de uma função
* Conjunto de cadeias de ligação do SDK Olá no código.
* Definir valores para o SDK de WebJobs os parâmetros do construtor no código
* Configurar **MaxDequeueCount** para processamento de blob nocivas.
* Acionar manualmente uma função
* Escrever registos

## <a name="next-steps"></a>Passos seguintes
Este artigo forneceu exemplos de código que mostram como blobs toohandle cenários comuns para trabalhar com o Azure. Para obter mais informações sobre como toouse WebJobs do Azure e Olá SDK de WebJobs, consulte [recursos de documentação de WebJobs do Azure](http://go.microsoft.com/fwlink/?linkid=390226).

