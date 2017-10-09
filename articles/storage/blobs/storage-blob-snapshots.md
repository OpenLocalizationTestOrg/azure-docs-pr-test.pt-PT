---
title: "aaaCreate um instantâneo só de leitura de um blob no Storage do Azure | Microsoft Docs"
description: "Saiba como toocreate um instantâneo de um tooback BLOBs dos dados de blob um determinado momento. Compreender a forma como os instantâneos são faturados e como toouse-los toominimize encargos de capacidade."
services: storage
documentationcenter: 
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 3710705d-e127-4b01-8d0f-29853fb06d0d
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/11/2017
ms.author: marsma
ms.openlocfilehash: 57f2e76b8899b8a513688bf148dd13673141d5bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-blob-snapshot"></a><span data-ttu-id="27bf3-104">Criar um instantâneo de blob</span><span class="sxs-lookup"><span data-stu-id="27bf3-104">Create a blob snapshot</span></span>

<span data-ttu-id="27bf3-105">Um instantâneo é uma versão só de leitura de um blob que é executada num ponto no tempo.</span><span class="sxs-lookup"><span data-stu-id="27bf3-105">A snapshot is a read-only version of a blob that's taken at a point in time.</span></span> <span data-ttu-id="27bf3-106">Os instantâneos são úteis para criar cópias de segurança blobs.</span><span class="sxs-lookup"><span data-stu-id="27bf3-106">Snapshots are useful for backing up blobs.</span></span> <span data-ttu-id="27bf3-107">Depois de criar um instantâneo, pode ler, copiar ou eliminá-la, mas não é possível modificá-lo.</span><span class="sxs-lookup"><span data-stu-id="27bf3-107">After you create a snapshot, you can read, copy, or delete it, but you cannot modify it.</span></span>

<span data-ttu-id="27bf3-108">Um instantâneo de um blob é blob base tooits idênticos, exceto esse blob Olá URI tem um **DateTime** valor acrescentado as tempo de Olá URI de blob do toohello tooindicate no qual Olá instantâneo foi tirado.</span><span class="sxs-lookup"><span data-stu-id="27bf3-108">A snapshot of a blob is identical tooits base blob, except that hello blob URI has a **DateTime** value appended toohello blob URI tooindicate hello time at which hello snapshot was taken.</span></span> <span data-ttu-id="27bf3-109">Por exemplo, se uma página de URI do blob é `http://storagesample.core.blob.windows.net/mydrives/myvhd`, Olá instantâneo URI é demasiado semelhante`http://storagesample.core.blob.windows.net/mydrives/myvhd?snapshot=2011-03-09T01:42:34.9360000Z`.</span><span class="sxs-lookup"><span data-stu-id="27bf3-109">For example, if a page blob URI is `http://storagesample.core.blob.windows.net/mydrives/myvhd`, hello snapshot URI is similar too`http://storagesample.core.blob.windows.net/mydrives/myvhd?snapshot=2011-03-09T01:42:34.9360000Z`.</span></span>

> [!NOTE]
> <span data-ttu-id="27bf3-110">Todos os instantâneos partilham o URI do blob Olá base.</span><span class="sxs-lookup"><span data-stu-id="27bf3-110">All snapshots share hello base blob's URI.</span></span> <span data-ttu-id="27bf3-111">Olá apenas distinção entre blob base Olá e instantâneo Olá é Olá anexado **DateTime** valor.</span><span class="sxs-lookup"><span data-stu-id="27bf3-111">hello only distinction between hello base blob and hello snapshot is hello appended **DateTime** value.</span></span>
>

<span data-ttu-id="27bf3-112">Um blob pode ter qualquer número de instantâneos.</span><span class="sxs-lookup"><span data-stu-id="27bf3-112">A blob can have any number of snapshots.</span></span> <span data-ttu-id="27bf3-113">Mantêm instantâneos até que estes sejam eliminados explicitamente.</span><span class="sxs-lookup"><span data-stu-id="27bf3-113">Snapshots persist until they are explicitly deleted.</span></span> <span data-ttu-id="27bf3-114">Um instantâneo não é possível outlive o blob base.</span><span class="sxs-lookup"><span data-stu-id="27bf3-114">A snapshot cannot outlive its base blob.</span></span> <span data-ttu-id="27bf3-115">Pode enumerar os instantâneos de Olá associados Olá base blob tootrack os instantâneos atuais.</span><span class="sxs-lookup"><span data-stu-id="27bf3-115">You can enumerate hello snapshots associated with hello base blob tootrack your current snapshots.</span></span>

<span data-ttu-id="27bf3-116">Quando cria um instantâneo de um blob, Olá propriedades do sistema do blob é copiados toohello instantâneo com Olá mesmos valores.</span><span class="sxs-lookup"><span data-stu-id="27bf3-116">When you create a snapshot of a blob, hello blob's system properties are copied toohello snapshot with hello same values.</span></span> <span data-ttu-id="27bf3-117">metadados do blob Olá base situação também copiado toohello instantâneo, a menos que especifique metadados separado para hello aquando da respetiva criação de instantâneos.</span><span class="sxs-lookup"><span data-stu-id="27bf3-117">hello base blob's metadata is also copied toohello snapshot, unless you specify separate metadata for hello snapshot when you create it.</span></span>

<span data-ttu-id="27bf3-118">Qualquer concessões associados blob base Olá não afetam os instantâneos de Olá.</span><span class="sxs-lookup"><span data-stu-id="27bf3-118">Any leases associated with hello base blob do not affect hello snapshot.</span></span> <span data-ttu-id="27bf3-119">Não é possível adquirir uma concessão num instantâneo.</span><span class="sxs-lookup"><span data-stu-id="27bf3-119">You cannot acquire a lease on a snapshot.</span></span>

<span data-ttu-id="27bf3-120">É um ficheiro VHD utilizados toostore Olá atual informações e o estado de um disco VM.</span><span class="sxs-lookup"><span data-stu-id="27bf3-120">A VHD file is used toostore hello current information and status for a VM disk.</span></span> <span data-ttu-id="27bf3-121">Pode desligar um disco a partir de Olá VM ou encerrar Olá VM e, em seguida, tirar um instantâneo do respetivo ficheiro VHD.</span><span class="sxs-lookup"><span data-stu-id="27bf3-121">You can detach a disk from within hello VM or shut down hello VM, and then take a snapshot of its VHD file.</span></span> <span data-ttu-id="27bf3-122">Pode utilizar esse ficheiro de instantâneo posterior tooretrieve Olá VHD ficheiro neste ponto no tempo e recrie Olá VM.</span><span class="sxs-lookup"><span data-stu-id="27bf3-122">You can use that snapshot file later tooretrieve hello VHD file at that point in time and recreate hello VM.</span></span>

<span data-ttu-id="27bf3-123">Se a encriptação de serviço de armazenamento (SSE) está ativada para a conta de armazenamento de Olá no qual Olá blob reside e eventuais instantâneos tomados desse blob serão encriptados em descanso.</span><span class="sxs-lookup"><span data-stu-id="27bf3-123">If Storage Service Encryption (SSE) is enabled for hello storage account in which hello blob resides, then any snapshots taken of that blob will be encrypted at rest.</span></span>

## <a name="create-a-snapshot"></a><span data-ttu-id="27bf3-124">Criar um instantâneo</span><span class="sxs-lookup"><span data-stu-id="27bf3-124">Create a snapshot</span></span>
<span data-ttu-id="27bf3-125">Olá exemplo de código seguinte mostra como toocreate um instantâneo, utilizando Olá [biblioteca de clientes do Storage do Azure para .NET](https://www.nuget.org/packages/WindowsAzure.Storage/).</span><span class="sxs-lookup"><span data-stu-id="27bf3-125">hello following code example shows how toocreate a snapshot by using hello [Azure Storage Client Library for .NET](https://www.nuget.org/packages/WindowsAzure.Storage/).</span></span> <span data-ttu-id="27bf3-126">Este exemplo Especifica metadados adicionais para instantâneo Olá quando é criado.</span><span class="sxs-lookup"><span data-stu-id="27bf3-126">This example specifies additional metadata for hello snapshot when it is created.</span></span>

```csharp
private static async Task CreateBlockBlobSnapshot(CloudBlobContainer container)
{
    // Create a new block blob in hello container.
    CloudBlockBlob baseBlob = container.GetBlockBlobReference("sample-base-blob.txt");

    // Add blob metadata.
    baseBlob.Metadata.Add("ApproxBlobCreatedDate", DateTime.UtcNow.ToString());

    try
    {
        // Upload hello blob toocreate it, with its metadata.
        await baseBlob.UploadTextAsync(string.Format("Base blob: {0}", baseBlob.Uri.ToString()));

        // Sleep 5 seconds.
        System.Threading.Thread.Sleep(5000);

        // Create a snapshot of hello base blob.
        // Specify metadata at hello time that hello snapshot is created toospecify unique metadata for hello snapshot.
        // If no metadata is specified when hello snapshot is created, hello base blob's metadata is copied toohello snapshot.
        Dictionary<string, string> metadata = new Dictionary<string, string>();
        metadata.Add("ApproxSnapshotCreatedDate", DateTime.UtcNow.ToString());
        await baseBlob.CreateSnapshotAsync(metadata, null, null, null);
    }
    catch (StorageException e)
    {
        Console.WriteLine(e.Message);
        Console.ReadLine();
        throw;
    }
}
```

## <a name="copy-snapshots"></a><span data-ttu-id="27bf3-127">Instantâneos de cópia</span><span class="sxs-lookup"><span data-stu-id="27bf3-127">Copy snapshots</span></span>
<span data-ttu-id="27bf3-128">Operações de cópia que envolvem os blobs e instantâneos, siga estas regras:</span><span class="sxs-lookup"><span data-stu-id="27bf3-128">Copy operations involving blobs and snapshots follow these rules:</span></span>

* <span data-ttu-id="27bf3-129">Pode copiar um instantâneo ao longo do respetivo blob base.</span><span class="sxs-lookup"><span data-stu-id="27bf3-129">You can copy a snapshot over its base blob.</span></span> <span data-ttu-id="27bf3-130">Ao promover uma posição de toohello instantâneos do blob base Olá, pode restaurar uma versão anterior de um blob.</span><span class="sxs-lookup"><span data-stu-id="27bf3-130">By promoting a snapshot toohello position of hello base blob, you can restore an earlier version of a blob.</span></span> <span data-ttu-id="27bf3-131">Olá permanece de instantâneo, mas o blob base Olá é substituído por uma cópia do instantâneo Olá gravável.</span><span class="sxs-lookup"><span data-stu-id="27bf3-131">hello snapshot remains, but hello base blob is overwritten with a writable copy of hello snapshot.</span></span>
* <span data-ttu-id="27bf3-132">Pode copiar um blob de destino do instantâneo tooa com um nome diferente.</span><span class="sxs-lookup"><span data-stu-id="27bf3-132">You can copy a snapshot tooa destination blob with a different name.</span></span> <span data-ttu-id="27bf3-133">blob de destino Olá resultante é um blob gravável e não um instantâneo.</span><span class="sxs-lookup"><span data-stu-id="27bf3-133">hello resulting destination blob is a writable blob and not a snapshot.</span></span>
* <span data-ttu-id="27bf3-134">Quando um blob de origem é copiado, todos os instantâneos do blob de origem Olá não são copiados toohello destino.</span><span class="sxs-lookup"><span data-stu-id="27bf3-134">When a source blob is copied, any snapshots of hello source blob are not copied toohello destination.</span></span> <span data-ttu-id="27bf3-135">Quando um blob de destino é substituído por uma cópia, todos os instantâneos associados com o blob de destino original Olá permaneçam intactos.</span><span class="sxs-lookup"><span data-stu-id="27bf3-135">When a destination blob is overwritten with a copy, any snapshots associated with hello original destination blob remain intact.</span></span>
* <span data-ttu-id="27bf3-136">Quando cria um instantâneo de um blob de bloco, lista de bloqueios consolidada de blob Olá é também copiado toohello instantâneo.</span><span class="sxs-lookup"><span data-stu-id="27bf3-136">When you create a snapshot of a block blob, hello blob's committed block list is also copied toohello snapshot.</span></span> <span data-ttu-id="27bf3-137">Quaisquer não consolidados blocos não são copiados.</span><span class="sxs-lookup"><span data-stu-id="27bf3-137">Any uncommitted blocks are not copied.</span></span>

## <a name="specify-an-access-condition"></a><span data-ttu-id="27bf3-138">Especifique uma condição de acesso</span><span class="sxs-lookup"><span data-stu-id="27bf3-138">Specify an access condition</span></span>
<span data-ttu-id="27bf3-139">Quando chamar [CreateSnapshotAsync][dotnet_CreateSnapshotAsync], pode especificar uma condição de acesso para que hello instantâneo apenas se a condição é cumprida.</span><span class="sxs-lookup"><span data-stu-id="27bf3-139">When you call [CreateSnapshotAsync][dotnet_CreateSnapshotAsync], you can specify an access condition so that hello snapshot is created only if a condition is met.</span></span> <span data-ttu-id="27bf3-140">toospecify uma condição de acesso, utilize Olá [AccessCondition] [ dotnet_AccessCondition] parâmetro.</span><span class="sxs-lookup"><span data-stu-id="27bf3-140">toospecify an access condition, use hello [AccessCondition][dotnet_AccessCondition] parameter.</span></span> <span data-ttu-id="27bf3-141">Se Olá especificado não é cumprida a condição, não é possível criar instantâneo de Olá e Olá serviço Blob devolve o código de estado [HTTPStatusCode][dotnet_HTTPStatusCode]. PreconditionFailed.</span><span class="sxs-lookup"><span data-stu-id="27bf3-141">If hello specified condition is not met, hello snapshot is not created, and hello Blob service returns status code [HTTPStatusCode][dotnet_HTTPStatusCode].PreconditionFailed.</span></span>

## <a name="delete-snapshots"></a><span data-ttu-id="27bf3-142">Elimine os instantâneos</span><span class="sxs-lookup"><span data-stu-id="27bf3-142">Delete snapshots</span></span>
<span data-ttu-id="27bf3-143">Não é possível eliminar um blob com instantâneos, exceto se os instantâneos de Olá também são eliminados.</span><span class="sxs-lookup"><span data-stu-id="27bf3-143">You can't delete a blob with snapshots unless hello snapshots are also deleted.</span></span> <span data-ttu-id="27bf3-144">Pode eliminar um instantâneo individualmente ou especificar que todos os instantâneos eliminado quando o blob de origem Olá é eliminado.</span><span class="sxs-lookup"><span data-stu-id="27bf3-144">You can delete a snapshot individually, or specify that all snapshots be deleted when hello source blob is deleted.</span></span> <span data-ttu-id="27bf3-145">Se tentar toodelete um blob que ainda tem instantâneos, resulta um erro.</span><span class="sxs-lookup"><span data-stu-id="27bf3-145">If you attempt toodelete a blob that still has snapshots, an error results.</span></span>

<span data-ttu-id="27bf3-146">Olá seguinte como exemplo de código mostra toodelete um blob e o respetivos instantâneos no .NET, onde `blockBlob` é um objeto do tipo [CloudBlockBlob][dotnet_CloudBlockBlob]:</span><span class="sxs-lookup"><span data-stu-id="27bf3-146">hello following code example shows how toodelete a blob and its snapshots in .NET, where `blockBlob` is an object of type [CloudBlockBlob][dotnet_CloudBlockBlob]:</span></span>

```csharp
await blockBlob.DeleteIfExistsAsync(DeleteSnapshotsOption.IncludeSnapshots, null, null, null);
```

## <a name="snapshots-with-azure-premium-storage"></a><span data-ttu-id="27bf3-147">Instantâneos com armazenamento do Azure Premium</span><span class="sxs-lookup"><span data-stu-id="27bf3-147">Snapshots with Azure Premium Storage</span></span>
<span data-ttu-id="27bf3-148">Quando utilizar instantâneos de Premium Storage, aplicam-se Olá seguintes regras:</span><span class="sxs-lookup"><span data-stu-id="27bf3-148">When using snapshots with Premium Storage, hello following rules apply:</span></span>

* <span data-ttu-id="27bf3-149">número máximo de Olá de instantâneos por BLOBs de páginas numa conta de armazenamento premium é 100.</span><span class="sxs-lookup"><span data-stu-id="27bf3-149">hello maximum number of snapshots per page blob in a premium storage account is 100.</span></span> <span data-ttu-id="27bf3-150">Se esse limite for excedido, Olá operação instantâneo Blob devolve o código de erro 409 (`SnapshotCountExceeded`).</span><span class="sxs-lookup"><span data-stu-id="27bf3-150">If that limit is exceeded, hello Snapshot Blob operation returns error code 409 (`SnapshotCountExceeded`).</span></span>
* <span data-ttu-id="27bf3-151">Pode tirar um instantâneo de um blob de página numa conta de armazenamento premium uma vez a cada 10 minutos.</span><span class="sxs-lookup"><span data-stu-id="27bf3-151">You can take a snapshot of a page blob in a premium storage account once every 10 minutes.</span></span> <span data-ttu-id="27bf3-152">Se a velocidade a que for excedida, Olá operação instantâneo Blob devolve o código de erro 409 (`SnapshotOperationRateExceeded`).</span><span class="sxs-lookup"><span data-stu-id="27bf3-152">If that rate is exceeded, hello Snapshot Blob operation returns error code 409 (`SnapshotOperationRateExceeded`).</span></span>
* <span data-ttu-id="27bf3-153">tooread um instantâneo, pode utilizar Olá copiar Blob operação toocopy um blob de página do instantâneo tooanother na conta de Olá.</span><span class="sxs-lookup"><span data-stu-id="27bf3-153">tooread a snapshot, you can use hello Copy Blob operation toocopy a snapshot tooanother page blob in hello account.</span></span> <span data-ttu-id="27bf3-154">blob de destino Olá da operação de cópia de Olá não pode ter todos os instantâneos existentes.</span><span class="sxs-lookup"><span data-stu-id="27bf3-154">hello destination blob for hello copy operation must not have any existing snapshots.</span></span> <span data-ttu-id="27bf3-155">Se o blob de destino Olá possui instantâneos, em seguida, Olá operação de cópia Blob devolve o código de erro 409 (`SnapshotsPresent`).</span><span class="sxs-lookup"><span data-stu-id="27bf3-155">If hello destination blob does have snapshots, then hello Copy Blob operation returns error code 409 (`SnapshotsPresent`).</span></span>

## <a name="return-hello-absolute-uri-tooa-snapshot"></a><span data-ttu-id="27bf3-156">Devolver o instantâneo de tooa URI absoluto Olá</span><span class="sxs-lookup"><span data-stu-id="27bf3-156">Return hello absolute URI tooa snapshot</span></span>
<span data-ttu-id="27bf3-157">Este exemplo de código c# cria um instantâneo e escreve saída Olá URI absoluto para a localização principal Olá.</span><span class="sxs-lookup"><span data-stu-id="27bf3-157">This C# code example creates a snapshot and writes out hello absolute URI for hello primary location.</span></span>

```csharp
//Create hello blob service client object.
const string ConnectionString = "DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key";

CloudStorageAccount storageAccount = CloudStorageAccount.Parse(ConnectionString);
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

//Get a reference tooa container.
CloudBlobContainer container = blobClient.GetContainerReference("sample-container");
container.CreateIfNotExists();

//Get a reference tooa blob.
CloudBlockBlob blob = container.GetBlockBlobReference("sampleblob.txt");
blob.UploadText("This is a blob.");

//Create a snapshot of hello blob and write out its primary URI.
CloudBlockBlob blobSnapshot = blob.CreateSnapshot();
Console.WriteLine(blobSnapshot.SnapshotQualifiedStorageUri.PrimaryUri);
```

## <a name="understand-how-snapshots-accrue-charges"></a><span data-ttu-id="27bf3-158">Compreender a forma como instantâneos acumular custos</span><span class="sxs-lookup"><span data-stu-id="27bf3-158">Understand how snapshots accrue charges</span></span>
<span data-ttu-id="27bf3-159">Criar um instantâneo, o que é uma cópia só de leitura de um blob, pode resultar na conta de tooyour de encargos de armazenamento de dados adicionais.</span><span class="sxs-lookup"><span data-stu-id="27bf3-159">Creating a snapshot, which is a read-only copy of a blob, can result in additional data storage charges tooyour account.</span></span> <span data-ttu-id="27bf3-160">Ao conceber a sua aplicação, é importante toobe ciente de como estes custos podem acumular, de modo a que pode minimizar os custos.</span><span class="sxs-lookup"><span data-stu-id="27bf3-160">When designing your application, it is important toobe aware of how these charges might accrue so that you can minimize costs.</span></span>

### <a name="important-billing-considerations"></a><span data-ttu-id="27bf3-161">Considerações importantes sobre faturação</span><span class="sxs-lookup"><span data-stu-id="27bf3-161">Important billing considerations</span></span>
<span data-ttu-id="27bf3-162">Olá lista a seguir inclui pontos chave tooconsider ao criar um instantâneo.</span><span class="sxs-lookup"><span data-stu-id="27bf3-162">hello following list includes key points tooconsider when creating a snapshot.</span></span>

* <span data-ttu-id="27bf3-163">A conta do storage incorreu custos de blocos exclusivos ou páginas, quer sejam no blob Olá ou num instantâneo Olá.</span><span class="sxs-lookup"><span data-stu-id="27bf3-163">Your storage account incurs charges for unique blocks or pages, whether they are in hello blob or in hello snapshot.</span></span> <span data-ttu-id="27bf3-164">A conta não implicar custos adicionais de instantâneos associados um blob até que Atualize blob Olá em que têm como base.</span><span class="sxs-lookup"><span data-stu-id="27bf3-164">Your account does not incur additional charges for snapshots associated with a blob until you update hello blob on which they are based.</span></span> <span data-ttu-id="27bf3-165">Depois de atualizar blob base Olá, diverges dos respetivos instantâneos.</span><span class="sxs-lookup"><span data-stu-id="27bf3-165">After you update hello base blob, it diverges from its snapshots.</span></span> <span data-ttu-id="27bf3-166">Quando isto acontecer, são-lhe cobrados para blocos exclusivo Olá ou páginas em cada blob ou um instantâneo.</span><span class="sxs-lookup"><span data-stu-id="27bf3-166">When this happens, you are charged for hello unique blocks or pages in each blob or snapshot.</span></span>
* <span data-ttu-id="27bf3-167">Se substituir um bloco dentro de um blob de bloco, o bloco subsequentemente é cobrado como um bloqueio exclusivo.</span><span class="sxs-lookup"><span data-stu-id="27bf3-167">When you replace a block within a block blob, that block is subsequently charged as a unique block.</span></span> <span data-ttu-id="27bf3-168">Isto acontece mesmo se tiver de bloco de Olá Olá mesmo bloquear o ID e Olá mesmo dados dado que tem no instantâneo Olá.</span><span class="sxs-lookup"><span data-stu-id="27bf3-168">This is true even if hello block has hello same block ID and hello same data as it has in hello snapshot.</span></span> <span data-ttu-id="27bf3-169">Depois de confirmadas bloco Olá novamente,-diverges do respetivo homólogo em qualquer instantâneo e será cobrada para os respetivos dados.</span><span class="sxs-lookup"><span data-stu-id="27bf3-169">After hello block is committed again, it diverges from its counterpart in any snapshot, and you will be charged for its data.</span></span> <span data-ttu-id="27bf3-170">Olá que mesmo se aplica para uma página num blob de página que é atualizado com dados idênticos.</span><span class="sxs-lookup"><span data-stu-id="27bf3-170">hello same holds true for a page in a page blob that's updated with identical data.</span></span>
* <span data-ttu-id="27bf3-171">Substituir um blob de blocos ao chamar Olá [UploadFromFile][dotnet_UploadFromFile], [UploadText][dotnet_UploadText], [UploadFromStream] [ dotnet_UploadFromStream], ou [UploadFromByteArray] [ dotnet_UploadFromByteArray] método substitui todos os blocos num blob Olá.</span><span class="sxs-lookup"><span data-stu-id="27bf3-171">Replacing a block blob by calling hello [UploadFromFile][dotnet_UploadFromFile], [UploadText][dotnet_UploadText], [UploadFromStream][dotnet_UploadFromStream], or [UploadFromByteArray][dotnet_UploadFromByteArray] method replaces all blocks in hello blob.</span></span> <span data-ttu-id="27bf3-172">Se tiver um instantâneo associado a esse blob, todos os blocos no blob base Olá e instantâneo agora diverge e será cobrada para todos os blocos de Olá em ambos os blobs.</span><span class="sxs-lookup"><span data-stu-id="27bf3-172">If you have a snapshot associated with that blob, all blocks in hello base blob and snapshot now diverge, and you will be charged for all hello blocks in both blobs.</span></span> <span data-ttu-id="27bf3-173">Isto acontece mesmo se os dados de Olá no blob base Olá e instantâneo Olá permanecem idênticos.</span><span class="sxs-lookup"><span data-stu-id="27bf3-173">This is true even if hello data in hello base blob and hello snapshot remain identical.</span></span>
* <span data-ttu-id="27bf3-174">Olá serviço Blob do Azure não tem um toodetermine significa que, se dois blocos contiverem dados idênticos.</span><span class="sxs-lookup"><span data-stu-id="27bf3-174">hello Azure Blob service does not have a means toodetermine whether two blocks contain identical data.</span></span> <span data-ttu-id="27bf3-175">Cada bloco que está carregado e consolidado é tratado como exclusivos, mesmo que tenha Olá mesmos dados e Olá bloquear o mesmo ID.</span><span class="sxs-lookup"><span data-stu-id="27bf3-175">Each block that is uploaded and committed is treated as unique, even if it has hello same data and hello same block ID.</span></span> <span data-ttu-id="27bf3-176">Uma vez que acumular custos de blocos exclusivos, é importante tooconsider que atualizar um blob que tenha um instantâneo resulta em blocos exclusivos adicionais e encargos adicionais.</span><span class="sxs-lookup"><span data-stu-id="27bf3-176">Because charges accrue for unique blocks, it's important tooconsider that updating a blob that has a snapshot results in additional unique blocks and additional charges.</span></span>

### <a name="minimize-cost-with-snapshot-management"></a><span data-ttu-id="27bf3-177">Minimizar os custos com gestão de instantâneos</span><span class="sxs-lookup"><span data-stu-id="27bf3-177">Minimize cost with snapshot management</span></span>

<span data-ttu-id="27bf3-178">É recomendado gerir os instantâneos cuidadosamente tooavoid encargos adicionais.</span><span class="sxs-lookup"><span data-stu-id="27bf3-178">We recommend managing your snapshots carefully tooavoid extra charges.</span></span> <span data-ttu-id="27bf3-179">Pode seguir estes procedimentos recomendados toohelp minimizar os custos de Olá tarifas de armazenamento de Olá do seu instantâneos:</span><span class="sxs-lookup"><span data-stu-id="27bf3-179">You can follow these best practices toohelp minimize hello costs incurred by hello storage of your snapshots:</span></span>

* <span data-ttu-id="27bf3-180">Eliminar e voltar a criar instantâneos associados a um blob sempre que atualizar blob Olá, mesmo que estão a atualizar com dados idênticos, a menos que a estrutura da aplicação requer que manter instantâneos.</span><span class="sxs-lookup"><span data-stu-id="27bf3-180">Delete and re-create snapshots associated with a blob whenever you update hello blob, even if you are updating with identical data, unless your application design requires that you maintain snapshots.</span></span> <span data-ttu-id="27bf3-181">Ao eliminar e voltar a criar instantâneos do blob Olá, pode certificar-se de que não se diverge blob Olá e instantâneos.</span><span class="sxs-lookup"><span data-stu-id="27bf3-181">By deleting and re-creating hello blob's snapshots, you can ensure that hello blob and snapshots do not diverge.</span></span>
* <span data-ttu-id="27bf3-182">Se estiver a manter instantâneos para um blob, evite chamar [UploadFromFile][dotnet_UploadFromFile], [UploadText][dotnet_UploadText], [ UploadFromStream][dotnet_UploadFromStream], ou [UploadFromByteArray] [ dotnet_UploadFromByteArray] blob de Olá tooupdate.</span><span class="sxs-lookup"><span data-stu-id="27bf3-182">If you are maintaining snapshots for a blob, avoid calling [UploadFromFile][dotnet_UploadFromFile], [UploadText][dotnet_UploadText], [UploadFromStream][dotnet_UploadFromStream], or [UploadFromByteArray][dotnet_UploadFromByteArray] tooupdate hello blob.</span></span> <span data-ttu-id="27bf3-183">Estes métodos substituem todos os blocos de Olá num blob Olá, fazendo com que o blob de base e respetiva toodiverge instantâneos significativamente.</span><span class="sxs-lookup"><span data-stu-id="27bf3-183">These methods replace all of hello blocks in hello blob, causing your base blob and its snapshots toodiverge significantly.</span></span> <span data-ttu-id="27bf3-184">Em vez disso, atualização Olá menor número possível de blocos através de Olá [PutBlock] [ dotnet_PutBlock] e [PutBlockList] [ dotnet_PutBlockList] métodos.</span><span class="sxs-lookup"><span data-stu-id="27bf3-184">Instead, update hello fewest possible number of blocks by using hello [PutBlock][dotnet_PutBlock] and [PutBlockList][dotnet_PutBlockList] methods.</span></span>

### <a name="snapshot-billing-scenarios"></a><span data-ttu-id="27bf3-185">Instantâneo de cenários de faturação</span><span class="sxs-lookup"><span data-stu-id="27bf3-185">Snapshot billing scenarios</span></span>
<span data-ttu-id="27bf3-186">os seguintes cenários de Olá demonstram como encargos acumular para um blob de bloco e respetivos instantâneos.</span><span class="sxs-lookup"><span data-stu-id="27bf3-186">hello following scenarios demonstrate how charges accrue for a block blob and its snapshots.</span></span>

<span data-ttu-id="27bf3-187">**Cenário 1**</span><span class="sxs-lookup"><span data-stu-id="27bf3-187">**Scenario 1**</span></span>

<span data-ttu-id="27bf3-188">Cenário 1, blob base Olá não tiver sido atualizado após Olá instantâneo foi captado, pelo que são cobradas taxas apenas para blocos exclusivos 1, 2 e 3.</span><span class="sxs-lookup"><span data-stu-id="27bf3-188">In scenario 1, hello base blob has not been updated after hello snapshot was taken, so charges are incurred only for unique blocks 1, 2, and 3.</span></span>

![Recursos de armazenamento do Azure](./media/storage-blob-snapshots/storage-blob-snapshots-billing-scenario-1.png)

<span data-ttu-id="27bf3-190">**Cenário 2**</span><span class="sxs-lookup"><span data-stu-id="27bf3-190">**Scenario 2**</span></span>

<span data-ttu-id="27bf3-191">Cenário 2, blob base Olá foi atualizada, mas o instantâneo de Olá tem não.</span><span class="sxs-lookup"><span data-stu-id="27bf3-191">In scenario 2, hello base blob has been updated, but hello snapshot has not.</span></span> <span data-ttu-id="27bf3-192">Bloco 3 foi atualizada e, apesar de contém Olá mesmos dados e Olá o mesmo ID, é não Olá igual ao bloquear 3 no instantâneo Olá.</span><span class="sxs-lookup"><span data-stu-id="27bf3-192">Block 3 was updated, and even though it contains hello same data and hello same ID, it is not hello same as block 3 in hello snapshot.</span></span> <span data-ttu-id="27bf3-193">Como resultado, a conta Olá é cobrada de quatro blocos.</span><span class="sxs-lookup"><span data-stu-id="27bf3-193">As a result, hello account is charged for four blocks.</span></span>

![Recursos de armazenamento do Azure](./media/storage-blob-snapshots/storage-blob-snapshots-billing-scenario-2.png)

<span data-ttu-id="27bf3-195">**Cenário 3**</span><span class="sxs-lookup"><span data-stu-id="27bf3-195">**Scenario 3**</span></span>

<span data-ttu-id="27bf3-196">No cenário 3, blob base Olá foi atualizada, mas o instantâneo de Olá tem não.</span><span class="sxs-lookup"><span data-stu-id="27bf3-196">In scenario 3, hello base blob has been updated, but hello snapshot has not.</span></span> <span data-ttu-id="27bf3-197">Bloco 3 foi substituído por blocos 4 num blob base Olá, mas o instantâneo de Olá ainda reflete bloco 3.</span><span class="sxs-lookup"><span data-stu-id="27bf3-197">Block 3 was replaced with block 4 in hello base blob, but hello snapshot still reflects block 3.</span></span> <span data-ttu-id="27bf3-198">Como resultado, a conta Olá é cobrada de quatro blocos.</span><span class="sxs-lookup"><span data-stu-id="27bf3-198">As a result, hello account is charged for four blocks.</span></span>

![Recursos de armazenamento do Azure](./media/storage-blob-snapshots/storage-blob-snapshots-billing-scenario-3.png)

<span data-ttu-id="27bf3-200">**Cenário 4**</span><span class="sxs-lookup"><span data-stu-id="27bf3-200">**Scenario 4**</span></span>

<span data-ttu-id="27bf3-201">Cenário 4, blob base Olá foi totalmente atualizado e contém nenhum dos seus blocos de originais.</span><span class="sxs-lookup"><span data-stu-id="27bf3-201">In scenario 4, hello base blob has been completely updated and contains none of its original blocks.</span></span> <span data-ttu-id="27bf3-202">Como resultado, a conta de Olá é cobrada para todos os blocos exclusivos oito.</span><span class="sxs-lookup"><span data-stu-id="27bf3-202">As a result, hello account is charged for all eight unique blocks.</span></span> <span data-ttu-id="27bf3-203">Este cenário pode ocorrer se estiver a utilizar um método de atualização, tais como [UploadFromFile][dotnet_UploadFromFile], [UploadText][dotnet_UploadText], [ UploadFromStream][dotnet_UploadFromStream], ou [UploadFromByteArray][dotnet_UploadFromByteArray], porque estes métodos substituem todos os conteúdos de Olá de um blob.</span><span class="sxs-lookup"><span data-stu-id="27bf3-203">This scenario can occur if you are using an update method such as [UploadFromFile][dotnet_UploadFromFile], [UploadText][dotnet_UploadText], [UploadFromStream][dotnet_UploadFromStream], or [UploadFromByteArray][dotnet_UploadFromByteArray], because these methods replace all of hello contents of a blob.</span></span>

![Recursos de armazenamento do Azure](./media/storage-blob-snapshots/storage-blob-snapshots-billing-scenario-4.png)

## <a name="next-steps"></a><span data-ttu-id="27bf3-205">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="27bf3-205">Next steps</span></span>

* <span data-ttu-id="27bf3-206">Pode encontrar mais informações sobre como trabalhar com instantâneos de disco de máquina virtual (VM) no [cópia de segurança do Azure discos VM não geridos com instantâneos incrementais](../../virtual-machines/windows/incremental-snapshots.md)</span><span class="sxs-lookup"><span data-stu-id="27bf3-206">You can find more information about working with virtual machine (VM) disk snapshots in [Back up Azure unmanaged VM disks with incremental snapshots](../../virtual-machines/windows/incremental-snapshots.md)</span></span>

* <span data-ttu-id="27bf3-207">Para obter exemplos de códigos adicionais utilizando o Blob storage, consulte [exemplos de código do Azure](https://azure.microsoft.com/documentation/samples/?service=storage&term=blob).</span><span class="sxs-lookup"><span data-stu-id="27bf3-207">For additional code examples using Blob storage, see [Azure Code Samples](https://azure.microsoft.com/documentation/samples/?service=storage&term=blob).</span></span> <span data-ttu-id="27bf3-208">Pode transferir uma aplicação de exemplo e executá-la ou procurar Olá código no GitHub.</span><span class="sxs-lookup"><span data-stu-id="27bf3-208">You can download a sample application and run it, or browse hello code on GitHub.</span></span>

[dotnet_AccessCondition]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.accesscondition.aspx
[dotnet_CloudBlockBlob]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.cloudblockblob.aspx
[dotnet_CreateSnapshotAsync]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.cloudblockblob.createsnapshotasync.aspx
[dotnet_HTTPStatusCode]: https://msdn.microsoft.com/library/system.net.httpstatuscode(v=vs.110).aspx
[dotnet_PutBlockList]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.cloudblockblob.putblocklist.aspx
[dotnet_PutBlock]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.cloudblockblob.putblock.aspx
[dotnet_UploadFromByteArray]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.cloudblockblob.uploadfrombytearray.aspx
[dotnet_UploadFromFile]: https://msdn.microsoft.com/library/azure/mt705654.aspx
[dotnet_UploadFromStream]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.cloudblockblob.uploadfromstream.aspx
[dotnet_UploadText]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.cloudblockblob.uploadtext.aspx