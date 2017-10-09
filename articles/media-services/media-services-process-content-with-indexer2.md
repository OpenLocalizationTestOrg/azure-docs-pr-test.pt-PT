---
title: "aaaIndexing ficheiros de suporte de dados pré-visualização do Azure Media indexador 2 | Microsoft Docs"
description: "Indexador de suporte de dados do Azure permite-lhe toomake conteúdo dos seus ficheiros de suporte de dados pesquisáveis e toogenerate um transcript de texto completo para fechado captioning e palavras-chave. Este tópico mostra como toouse indexador de multimédia 2 de pré-visualização."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 85d25525-a498-44eb-ae3a-2ca5ceb8e53d
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/31/2017
ms.author: adsolank;juliako;
ms.openlocfilehash: f83fa0db58b828ffa29933d68ce108b4906dcd78
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="indexing-media-files-with-azure-media-indexer-2-preview"></a>A indexação de ficheiros de suporte de dados pré-visualização do indexador 2 Media Services do Azure
## <a name="overview"></a>Descrição geral
Olá **pré-visualização do Azure Media indexador 2** processador de multimédia (MP) permite-lhe toomake ficheiros de suporte de dados e conteúdo pesquisável, bem como gerar controla captioning fechada. Toohello em comparação com a versão anterior do [indexador de suporte de dados do Azure](media-services-index-content.md), **pré-visualização do Azure Media indexador 2** efetua a indexação mais rápido e oferece mais amplo suporte de idiomas. Idiomas suportados incluem o inglês, espanhol, francês, alemão, italiano, chinês (simplificado, de Mandarim), português, árabes e japonês.

Olá **pré-visualização do Azure Media indexador 2** MP está atualmente em pré-visualização.

Este tópico mostra como toocreate indexação as tarefas com **pré-visualização do Azure Media indexador 2**.

> [!NOTE]
> aplicar Olá seguintes considerações:
> 
> Indexador 2 não é suportada na China do Azure e Azure Government.
> 
> Quando o conteúdo de indexação, certifique-se toouse os ficheiros de suporte de dados que tenham o reconhecimento de voz muito simples (sem leitores de música em segundo plano, ruído, efeitos ou hiss microfone). Alguns exemplos de conteúdo apropriado: registadas reuniões, lectures ou apresentações. Olá seguinte conteúdo poderá não ser adequado para indexação: filmes, mostra TV, qualquer caráter com áudio misto e efeitos de som, mal registadas conteúdo com o ruído de fundo (hiss).
> 
> 

Este tópico fornece detalhes sobre **pré-visualização do Azure Media indexador 2** e mostra como toouse-lo com o SDK de Media Services para .NET

## <a name="input-and-output-files"></a>Ficheiros de entrada e de saída
### <a name="input-files"></a>Ficheiros de entrada
Ficheiros de vídeos ou áudio

### <a name="output-files"></a>Ficheiros de saída
Uma tarefa de indexação pode gerar ficheiros de legendas no Olá seguintes formatos:  

* **SAMI**
* **TTML**
* **WebVTT**

Fechado ficheiros de legenda (CC) nestes formatos podem ser utilizados toomake áudio e vídeo ficheiros toopeople acessível com hearing disability.

## <a name="task-configuration-preset"></a>Configuração da tarefa (predefinição)
Quando criar um indexação tarefas com **pré-visualização do Azure Media indexador 2**, tem de especificar uma predefinição de configuração.

Olá seguinte JSON define os parâmetros disponíveis.

    {
      "version":"1.0",
      "Features":
        [
           {
           "Options": {
                "Formats":["WebVtt","ttml"],
                "Language":"enUs",
                "Type":"RecoOptions"
           },
           "Type":"SpReco"
        }]
    }

## <a name="supported-languages"></a>Linguagens suportadas
Pré-visualização de 2 do indexador de suporte de dados do Azure suporta reconhecimento de voz para texto de Olá (ao especificar nome de idioma Olá na configuração da tarefa Olá, utilize o código de 4 carateres entre parênteses Retos, conforme mostrado abaixo) os seguintes idiomas:

* Inglês [EnUs]
* Espanhol [EsEs]
* Chinês (Mandarim, simplificada) [ZhCn]
* Francês [FrFr]
* Alemão [DeDe]
* Italiano [ItIt]
* Português [PtBr]
* Árabe (Egyptian) [ArEg]
* Japonês [JaJp]
* Russo [RuRu]
* Território inglês [EnGb]
* Espanhol Mexican [EsMx] 

## <a name="supported-file-types"></a>Tipos de ficheiro suportados

Para informações sobre os tipos de ficheiros suportados, consulte Olá [codecs/formatos suportados](media-services-media-encoder-standard-formats.md#input-containerfile-formats) secção.

## <a name="net-sample-code"></a>Código de exemplo do .NET

seguinte Olá programa mostra como:

1. Criar um elemento e carregar um ficheiro de suporte de dados para o elemento de Olá.
2. Crie uma tarefa com uma tarefa de indexação com base num ficheiro de configuração que contenha Olá predefinição json a seguir.
   
        {
          "version":"1.0",
          "Features":
            [
               {
               "Options": {
                    "Formats":["WebVtt","ttml"],
                    "Language":"enUs",
                    "Type":"RecoOptions"
               },
               "Type":"SpReco"
            }]
        }
3. Transfira os ficheiros de saída Olá. 
   
#### <a name="create-and-configure-a-visual-studio-project"></a>Criar e configurar um projeto de Visual Studio

Configurar o ambiente de desenvolvimento e preencher o ficheiro de App. config Olá com as informações de ligação, conforme descrito em [desenvolvimento de Media Services com .NET](media-services-dotnet-how-to-use.md). 

#### <a name="example"></a>Exemplo

    using System;
    using System.Configuration;
    using System.IO;
    using System.Linq;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using System.Threading;
    using System.Threading.Tasks;

    namespace IndexContent
    {
        class Program
        {
            // Read values from hello App.config file.
            private static readonly string _AADTenantDomain =
                ConfigurationManager.AppSettings["AADTenantDomain"];
            private static readonly string _RESTAPIEndpoint =
                ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];

            // Field for service context.
            private static CloudMediaContext _context = null;

            static void Main(string[] args)
            {
                var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
                var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

                _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);

                // Run indexing job.
                var asset = RunIndexingJob(@"C:\supportFiles\Indexer\BigBuckBunny.mp4",
                                            @"C:\supportFiles\Indexer\config.json");

                // Download hello job output asset.
                DownloadAsset(asset, @"C:\supportFiles\Indexer\Output");
            }

            static IAsset RunIndexingJob(string inputMediaFilePath, string configurationFile)
            {
                // Create an asset and upload hello input media file toostorage.
                IAsset asset = CreateAssetAndUploadSingleFile(inputMediaFilePath,
                    "My Indexing Input Asset",
                    AssetCreationOptions.None);

                // Declare a new job.
                IJob job = _context.Jobs.Create("My Indexing Job");

                // Get a reference tooAzure Media Indexer 2 Preview.
                string MediaProcessorName = "Azure Media Indexer 2 Preview";

                var processor = GetLatestMediaProcessorByName(MediaProcessorName);

                // Read configuration from hello specified file.
                string configuration = File.ReadAllText(configurationFile);

                // Create a task with hello encoding details, using a string preset.
                ITask task = job.Tasks.AddNew("My Indexing Task",
                    processor,
                    configuration,
                    TaskOptions.None);

                // Specify hello input asset toobe indexed.
                task.InputAssets.Add(asset);

                // Add an output asset toocontain hello results of hello job.
                task.OutputAssets.AddNew("My Indexing Output Asset", AssetCreationOptions.None);

                // Use hello following event handler toocheck job progress.  
                job.StateChanged += new EventHandler<JobStateChangedEventArgs>(StateChanged);

                // Launch hello job.
                job.Submit();

                // Check job execution and wait for job toofinish.
                Task progressJobTask = job.GetExecutionProgressTask(CancellationToken.None);

                progressJobTask.Wait();

                // If job state is Error, hello event handling
                // method for job progress should log errors.  Here we check
                // for error state and exit if needed.
                if (job.State == JobState.Error)
                {
                    ErrorDetail error = job.Tasks.First().ErrorDetails.First();
                    Console.WriteLine(string.Format("Error: {0}. {1}",
                                                    error.Code,
                                                    error.Message));
                    return null;
                }

                return job.OutputMediaAssets[0];
            }

            static IAsset CreateAssetAndUploadSingleFile(string filePath, string assetName, AssetCreationOptions options)
            {
                IAsset asset = _context.Assets.Create(assetName, options);

                var assetFile = asset.AssetFiles.Create(Path.GetFileName(filePath));
                assetFile.Upload(filePath);

                return asset;
            }

            static void DownloadAsset(IAsset asset, string outputDirectory)
            {
                foreach (IAssetFile file in asset.AssetFiles)
                {
                    file.Download(Path.Combine(outputDirectory, file.Name));
                }
            }

            static IMediaProcessor GetLatestMediaProcessorByName(string mediaProcessorName)
            {
                var processor = _context.MediaProcessors
                    .Where(p => p.Name == mediaProcessorName)
                    .ToList()
                    .OrderBy(p => new Version(p.Version))
                    .LastOrDefault();

                if (processor == null)
                    throw new ArgumentException(string.Format("Unknown media processor",
                                                               mediaProcessorName));

                return processor;
            }

            static private void StateChanged(object sender, JobStateChangedEventArgs e)
            {
                Console.WriteLine("Job state changed event:");
                Console.WriteLine("  Previous state: " + e.PreviousState);
                Console.WriteLine("  Current state: " + e.CurrentState);

                switch (e.CurrentState)
                {
                    case JobState.Finished:
                        Console.WriteLine();
                        Console.WriteLine("Job is finished.");
                        Console.WriteLine();
                        break;
                    case JobState.Canceling:
                    case JobState.Queued:
                    case JobState.Scheduled:
                    case JobState.Processing:
                        Console.WriteLine("Please wait...\n");
                        break;
                    case JobState.Canceled:
                    case JobState.Error:
                        // Cast sender as a job.
                        IJob job = (IJob)sender;
                        // Display or log error details as needed.
                        // LogJobStop(job.Id);
                        break;
                    default:
                        break;
                }
            }
        }
    }

## <a name="media-services-learning-paths"></a>Percursos de aprendizagem dos Media Services
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Enviar comentários
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a>Ligações relacionadas
[Descrição geral da análise de serviços de multimédia do Azure](media-services-analytics-overview.md)

[Demonstrações de análise de multimédia do Azure](http://azuremedialabs.azurewebsites.net/demos/Analytics.html)

