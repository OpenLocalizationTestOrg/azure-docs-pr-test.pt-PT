---
title: computador de tooyour de ativos de Media Services aaaDownload - Azure | Microsoft Docs
description: "Saiba mais sobre o computador de tooyour toodownload ativos. Exemplos de código são escritos em c# e utilizam Olá SDK de Media Services para .NET."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 8908a1dd-3ffb-4f18-955d-4c8e2d82fc5d
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: juliako
ms.openlocfilehash: 6c6e764720caa59d8371178a2682700345f7bc57
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-to-deliver-an-asset-by-download"></a>Como: fornecer um recurso por transferência
Este tópico descreve as opções de entrega de recursos de suporte de dados carregados tooMedia serviços. Pode fornecer conteúdo de serviços de suporte de dados em vários cenários de aplicação. Pode transferir os recursos de suporte de dados ou aceder às mesmas através da utilização de um localizador. Pode enviar aplicações de tooanother conteúdo do suporte de dados ou tooanother fornecedor de conteúdos. Para um melhor desempenho e escalabilidade, pode também de fornecer conteúdo utilizando uma rede de entrega de conteúdos (CDN).

Este exemplo mostra como recursos de suporte de dados de toodownload partir do computador local do tooyour dos Media Services. Olá consultas de código Olá tarefas associadas a conta de Media Services Olá por ID de tarefa e acede a **OutputMediaAssets** coleção (que é o conjunto de Olá de um ou mais recursos de suporte de dados de saída que resulta da executar uma tarefa). Este exemplo mostra como suporte de dados de saída toodownload ativos de uma tarefa, mas podem aplicar Olá toodownload do mesmo abordagem outros elementos.

>[!NOTE]
>Existe um limite de 1,000,000 políticas para diferentes políticas do AMS (por exemplo, para a política Locator ou ContentKeyAuthorizationPolicy). Deve utilizar Olá mesmo ID de política, se estiver a utilizar sempre Olá mesmo dias / permissões, por exemplo, políticas para os localizadores são tooremain pretendido no local durante muito tempo (políticas não carregamento) de acesso. Para obter mais informações, veja [este](media-services-dotnet-manage-entities.md#limit-access-policies) tópico.

    // Download hello output asset of hello specified job tooa local folder.
    static IAsset DownloadAssetToLocal( string jobId, string outputFolder)
    {
        // This method illustrates how toodownload a single asset. 
        // However, you can iterate through hello OutputAssets
        // collection, and download all assets if there are many. 

        // Get a reference toohello job. 
        IJob job = GetJob(jobId);

        // Get a reference toohello first output asset. If there were multiple 
        // output media assets you could iterate and handle each one.
        IAsset outputAsset = job.OutputMediaAssets[0];

        // Create a SAS locator toodownload hello asset
        IAccessPolicy accessPolicy = _context.AccessPolicies.Create("File Download Policy", TimeSpan.FromDays(30), AccessPermissions.Read);
        ILocator locator = _context.Locators.CreateLocator(LocatorType.Sas, outputAsset, accessPolicy);

        BlobTransferClient blobTransfer = new BlobTransferClient
        {
            NumberOfConcurrentTransfers = 20,
            ParallelTransferThreadCount = 20
        };

        var downloadTasks = new List<Task>();
        foreach (IAssetFile outputFile in outputAsset.AssetFiles)
        {
            // Use hello following event handler toocheck download progress.
            outputFile.DownloadProgressChanged += DownloadProgress;

            string localDownloadPath = Path.Combine(outputFolder, outputFile.Name);

            Console.WriteLine("File download path:  " + localDownloadPath);

            downloadTasks.Add(outputFile.DownloadAsync(Path.GetFullPath(localDownloadPath), blobTransfer, locator, CancellationToken.None));

            outputFile.DownloadProgressChanged -= DownloadProgress;
        }

        Task.WaitAll(downloadTasks.ToArray());

        return outputAsset;
    }

    static void DownloadProgress(object sender, DownloadProgressChangedEventArgs e)
    {
        Console.WriteLine(string.Format("{0} % download progress. ", e.Progress));
    }



## <a name="media-services-learning-paths"></a>Percursos de aprendizagem dos Media Services
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Enviar comentários
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a>Veja Também
[Distribuir os conteúdos de transmissão em fluxo](media-services-deliver-streaming-content.md)

