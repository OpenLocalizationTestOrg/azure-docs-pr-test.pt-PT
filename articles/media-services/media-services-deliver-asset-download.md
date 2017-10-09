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
# <a name="how-to-deliver-an-asset-by-download"></a><span data-ttu-id="7df10-104">Como: fornecer um recurso por transferência</span><span class="sxs-lookup"><span data-stu-id="7df10-104">How to: Deliver an Asset by Download</span></span>
<span data-ttu-id="7df10-105">Este tópico descreve as opções de entrega de recursos de suporte de dados carregados tooMedia serviços.</span><span class="sxs-lookup"><span data-stu-id="7df10-105">This topic discusses options for delivering media assets uploaded tooMedia Services.</span></span> <span data-ttu-id="7df10-106">Pode fornecer conteúdo de serviços de suporte de dados em vários cenários de aplicação.</span><span class="sxs-lookup"><span data-stu-id="7df10-106">You can deliver Media Services content in numerous application scenarios.</span></span> <span data-ttu-id="7df10-107">Pode transferir os recursos de suporte de dados ou aceder às mesmas através da utilização de um localizador.</span><span class="sxs-lookup"><span data-stu-id="7df10-107">You can download media assets, or access them by using a locator.</span></span> <span data-ttu-id="7df10-108">Pode enviar aplicações de tooanother conteúdo do suporte de dados ou tooanother fornecedor de conteúdos.</span><span class="sxs-lookup"><span data-stu-id="7df10-108">You can send media content tooanother application or tooanother content provider.</span></span> <span data-ttu-id="7df10-109">Para um melhor desempenho e escalabilidade, pode também de fornecer conteúdo utilizando uma rede de entrega de conteúdos (CDN).</span><span class="sxs-lookup"><span data-stu-id="7df10-109">For improved performance and scalability, you can also deliver content by using a Content Delivery Network (CDN).</span></span>

<span data-ttu-id="7df10-110">Este exemplo mostra como recursos de suporte de dados de toodownload partir do computador local do tooyour dos Media Services.</span><span class="sxs-lookup"><span data-stu-id="7df10-110">This example shows how toodownload media assets from Media Services tooyour local computer.</span></span> <span data-ttu-id="7df10-111">Olá consultas de código Olá tarefas associadas a conta de Media Services Olá por ID de tarefa e acede a **OutputMediaAssets** coleção (que é o conjunto de Olá de um ou mais recursos de suporte de dados de saída que resulta da executar uma tarefa).</span><span class="sxs-lookup"><span data-stu-id="7df10-111">hello code queries hello jobs associated with hello Media Services account by job ID and accesses its **OutputMediaAssets** collection (which is hello set of one or more output media assets that results from running a job).</span></span> <span data-ttu-id="7df10-112">Este exemplo mostra como suporte de dados de saída toodownload ativos de uma tarefa, mas podem aplicar Olá toodownload do mesmo abordagem outros elementos.</span><span class="sxs-lookup"><span data-stu-id="7df10-112">This  example shows how toodownload output media assets from a job, but you can apply hello same approach toodownload other assets.</span></span>

>[!NOTE]
><span data-ttu-id="7df10-113">Existe um limite de 1,000,000 políticas para diferentes políticas do AMS (por exemplo, para a política Locator ou ContentKeyAuthorizationPolicy).</span><span class="sxs-lookup"><span data-stu-id="7df10-113">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="7df10-114">Deve utilizar Olá mesmo ID de política, se estiver a utilizar sempre Olá mesmo dias / permissões, por exemplo, políticas para os localizadores são tooremain pretendido no local durante muito tempo (políticas não carregamento) de acesso.</span><span class="sxs-lookup"><span data-stu-id="7df10-114">You should use hello same policy ID if you are always using hello same days / access permissions, for example, policies for locators that are intended tooremain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="7df10-115">Para obter mais informações, veja [este](media-services-dotnet-manage-entities.md#limit-access-policies) tópico.</span><span class="sxs-lookup"><span data-stu-id="7df10-115">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>

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



## <a name="media-services-learning-paths"></a><span data-ttu-id="7df10-116">Percursos de aprendizagem dos Media Services</span><span class="sxs-lookup"><span data-stu-id="7df10-116">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="7df10-117">Enviar comentários</span><span class="sxs-lookup"><span data-stu-id="7df10-117">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="7df10-118">Veja Também</span><span class="sxs-lookup"><span data-stu-id="7df10-118">See Also</span></span>
[<span data-ttu-id="7df10-119">Distribuir os conteúdos de transmissão em fluxo</span><span class="sxs-lookup"><span data-stu-id="7df10-119">Deliver streaming content</span></span>](media-services-deliver-streaming-content.md)

