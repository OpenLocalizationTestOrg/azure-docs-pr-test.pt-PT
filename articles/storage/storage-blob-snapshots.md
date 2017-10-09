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
ms.openlocfilehash: 9e7af611e885d83df69d3329217f261b3f3f333e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-blob-snapshot"></a>Criar um instantâneo de blob

Um instantâneo é uma versão só de leitura de um blob que é executada num ponto no tempo. Os instantâneos são úteis para criar cópias de segurança blobs. Depois de criar um instantâneo, pode ler, copiar ou eliminá-la, mas não é possível modificá-lo.

Um instantâneo de um blob é blob base tooits idênticos, exceto esse blob Olá URI tem um **DateTime** valor acrescentado as tempo de Olá URI de blob do toohello tooindicate no qual Olá instantâneo foi tirado. Por exemplo, se uma página de URI do blob é `http://storagesample.core.blob.windows.net/mydrives/myvhd`, Olá instantâneo URI é demasiado semelhante`http://storagesample.core.blob.windows.net/mydrives/myvhd?snapshot=2011-03-09T01:42:34.9360000Z`.

> [!NOTE]
> Todos os instantâneos partilham o URI do blob Olá base. Olá apenas distinção entre blob base Olá e instantâneo Olá é Olá anexado **DateTime** valor.
>

Um blob pode ter qualquer número de instantâneos. Mantêm instantâneos até que estes sejam eliminados explicitamente. Um instantâneo não é possível outlive o blob base. Pode enumerar os instantâneos de Olá associados Olá base blob tootrack os instantâneos atuais.

Quando cria um instantâneo de um blob, Olá propriedades do sistema do blob é copiados toohello instantâneo com Olá mesmos valores. metadados do blob Olá base situação também copiado toohello instantâneo, a menos que especifique metadados separado para hello aquando da respetiva criação de instantâneos.

Qualquer concessões associados blob base Olá não afetam os instantâneos de Olá. Não é possível adquirir uma concessão num instantâneo.

É um ficheiro VHD utilizados toostore Olá atual informações e o estado de um disco VM. Pode desligar um disco a partir de Olá VM ou encerrar Olá VM e, em seguida, tirar um instantâneo do respetivo ficheiro VHD. Pode utilizar esse ficheiro de instantâneo posterior tooretrieve Olá VHD ficheiro neste ponto no tempo e recrie Olá VM.

Se a encriptação de serviço de armazenamento (SSE) está ativada para a conta de armazenamento de Olá no qual Olá blob reside e eventuais instantâneos tomados desse blob serão encriptados em descanso.

## <a name="create-a-snapshot"></a>Criar um instantâneo
Olá exemplo de código seguinte mostra como toocreate um instantâneo, utilizando Olá [biblioteca de clientes do Storage do Azure para .NET](https://www.nuget.org/packages/WindowsAzure.Storage/). Este exemplo Especifica metadados adicionais para instantâneo Olá quando é criado.

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

## <a name="copy-snapshots"></a>Instantâneos de cópia
Operações de cópia que envolvem os blobs e instantâneos, siga estas regras:

* Pode copiar um instantâneo ao longo do respetivo blob base. Ao promover uma posição de toohello instantâneos do blob base Olá, pode restaurar uma versão anterior de um blob. Olá permanece de instantâneo, mas o blob base Olá é substituído por uma cópia do instantâneo Olá gravável.
* Pode copiar um blob de destino do instantâneo tooa com um nome diferente. blob de destino Olá resultante é um blob gravável e não um instantâneo.
* Quando um blob de origem é copiado, todos os instantâneos do blob de origem Olá não são copiados toohello destino. Quando um blob de destino é substituído por uma cópia, todos os instantâneos associados com o blob de destino original Olá permaneçam intactos.
* Quando cria um instantâneo de um blob de bloco, lista de bloqueios consolidada de blob Olá é também copiado toohello instantâneo. Quaisquer não consolidados blocos não são copiados.

## <a name="specify-an-access-condition"></a>Especifique uma condição de acesso
Quando chamar [CreateSnapshotAsync][dotnet_CreateSnapshotAsync], pode especificar uma condição de acesso para que hello instantâneo apenas se a condição é cumprida. toospecify uma condição de acesso, utilize Olá [AccessCondition] [ dotnet_AccessCondition] parâmetro. Se Olá especificado não é cumprida a condição, não é possível criar instantâneo de Olá e Olá serviço Blob devolve o código de estado [HTTPStatusCode][dotnet_HTTPStatusCode]. PreconditionFailed.

## <a name="delete-snapshots"></a>Elimine os instantâneos
Não é possível eliminar um blob com instantâneos, exceto se os instantâneos de Olá também são eliminados. Pode eliminar um instantâneo individualmente ou especificar que todos os instantâneos eliminado quando o blob de origem Olá é eliminado. Se tentar toodelete um blob que ainda tem instantâneos, resulta um erro.

Olá seguinte como exemplo de código mostra toodelete um blob e o respetivos instantâneos no .NET, onde `blockBlob` é um objeto do tipo [CloudBlockBlob][dotnet_CloudBlockBlob]:

```csharp
await blockBlob.DeleteIfExistsAsync(DeleteSnapshotsOption.IncludeSnapshots, null, null, null);
```

## <a name="snapshots-with-azure-premium-storage"></a>Instantâneos com armazenamento do Azure Premium
Quando utilizar instantâneos de Premium Storage, aplicam-se Olá seguintes regras:

* número máximo de Olá de instantâneos por BLOBs de páginas numa conta de armazenamento premium é 100. Se esse limite for excedido, Olá operação instantâneo Blob devolve o código de erro 409 (`SnapshotCountExceeded`).
* Pode tirar um instantâneo de um blob de página numa conta de armazenamento premium uma vez a cada 10 minutos. Se a velocidade a que for excedida, Olá operação instantâneo Blob devolve o código de erro 409 (`SnapshotOperationRateExceeded`).
* tooread um instantâneo, pode utilizar Olá copiar Blob operação toocopy um blob de página do instantâneo tooanother na conta de Olá. blob de destino Olá da operação de cópia de Olá não pode ter todos os instantâneos existentes. Se o blob de destino Olá possui instantâneos, em seguida, Olá operação de cópia Blob devolve o código de erro 409 (`SnapshotsPresent`).

## <a name="return-hello-absolute-uri-tooa-snapshot"></a>Devolver o instantâneo de tooa URI absoluto Olá
Este exemplo de código c# cria um instantâneo e escreve saída Olá URI absoluto para a localização principal Olá.

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

## <a name="understand-how-snapshots-accrue-charges"></a>Compreender a forma como instantâneos acumular custos
Criar um instantâneo, o que é uma cópia só de leitura de um blob, pode resultar na conta de tooyour de encargos de armazenamento de dados adicionais. Ao conceber a sua aplicação, é importante toobe ciente de como estes custos podem acumular, de modo a que pode minimizar os custos.

### <a name="important-billing-considerations"></a>Considerações importantes sobre faturação
Olá lista a seguir inclui pontos chave tooconsider ao criar um instantâneo.

* A conta do storage incorreu custos de blocos exclusivos ou páginas, quer sejam no blob Olá ou num instantâneo Olá. A conta não implicar custos adicionais de instantâneos associados um blob até que Atualize blob Olá em que têm como base. Depois de atualizar blob base Olá, diverges dos respetivos instantâneos. Quando isto acontecer, são-lhe cobrados para blocos exclusivo Olá ou páginas em cada blob ou um instantâneo.
* Se substituir um bloco dentro de um blob de bloco, o bloco subsequentemente é cobrado como um bloqueio exclusivo. Isto acontece mesmo se tiver de bloco de Olá Olá mesmo bloquear o ID e Olá mesmo dados dado que tem no instantâneo Olá. Depois de confirmadas bloco Olá novamente,-diverges do respetivo homólogo em qualquer instantâneo e será cobrada para os respetivos dados. Olá que mesmo se aplica para uma página num blob de página que é atualizado com dados idênticos.
* Substituir um blob de blocos ao chamar Olá [UploadFromFile][dotnet_UploadFromFile], [UploadText][dotnet_UploadText], [UploadFromStream] [ dotnet_UploadFromStream], ou [UploadFromByteArray] [ dotnet_UploadFromByteArray] método substitui todos os blocos num blob Olá. Se tiver um instantâneo associado a esse blob, todos os blocos no blob base Olá e instantâneo agora diverge e será cobrada para todos os blocos de Olá em ambos os blobs. Isto acontece mesmo se os dados de Olá no blob base Olá e instantâneo Olá permanecem idênticos.
* Olá serviço Blob do Azure não tem um toodetermine significa que, se dois blocos contiverem dados idênticos. Cada bloco que está carregado e consolidado é tratado como exclusivos, mesmo que tenha Olá mesmos dados e Olá bloquear o mesmo ID. Uma vez que acumular custos de blocos exclusivos, é importante tooconsider que atualizar um blob que tenha um instantâneo resulta em blocos exclusivos adicionais e encargos adicionais.

### <a name="minimize-cost-with-snapshot-management"></a>Minimizar os custos com gestão de instantâneos

É recomendado gerir os instantâneos cuidadosamente tooavoid encargos adicionais. Pode seguir estes procedimentos recomendados toohelp minimizar os custos de Olá tarifas de armazenamento de Olá do seu instantâneos:

* Eliminar e voltar a criar instantâneos associados a um blob sempre que atualizar blob Olá, mesmo que estão a atualizar com dados idênticos, a menos que a estrutura da aplicação requer que manter instantâneos. Ao eliminar e voltar a criar instantâneos do blob Olá, pode certificar-se de que não se diverge blob Olá e instantâneos.
* Se estiver a manter instantâneos para um blob, evite chamar [UploadFromFile][dotnet_UploadFromFile], [UploadText][dotnet_UploadText], [ UploadFromStream][dotnet_UploadFromStream], ou [UploadFromByteArray] [ dotnet_UploadFromByteArray] blob de Olá tooupdate. Estes métodos substituem todos os blocos de Olá num blob Olá, fazendo com que o blob de base e respetiva toodiverge instantâneos significativamente. Em vez disso, atualização Olá menor número possível de blocos através de Olá [PutBlock] [ dotnet_PutBlock] e [PutBlockList] [ dotnet_PutBlockList] métodos.

### <a name="snapshot-billing-scenarios"></a>Instantâneo de cenários de faturação
os seguintes cenários de Olá demonstram como encargos acumular para um blob de bloco e respetivos instantâneos.

**Cenário 1**

Cenário 1, blob base Olá não tiver sido atualizado após Olá instantâneo foi captado, pelo que são cobradas taxas apenas para blocos exclusivos 1, 2 e 3.

![Recursos de armazenamento do Azure](./media/storage-blob-snapshots/storage-blob-snapshots-billing-scenario-1.png)

**Cenário 2**

Cenário 2, blob base Olá foi atualizada, mas o instantâneo de Olá tem não. Bloco 3 foi atualizada e, apesar de contém Olá mesmos dados e Olá o mesmo ID, é não Olá igual ao bloquear 3 no instantâneo Olá. Como resultado, a conta Olá é cobrada de quatro blocos.

![Recursos de armazenamento do Azure](./media/storage-blob-snapshots/storage-blob-snapshots-billing-scenario-2.png)

**Cenário 3**

No cenário 3, blob base Olá foi atualizada, mas o instantâneo de Olá tem não. Bloco 3 foi substituído por blocos 4 num blob base Olá, mas o instantâneo de Olá ainda reflete bloco 3. Como resultado, a conta Olá é cobrada de quatro blocos.

![Recursos de armazenamento do Azure](./media/storage-blob-snapshots/storage-blob-snapshots-billing-scenario-3.png)

**Cenário 4**

Cenário 4, blob base Olá foi totalmente atualizado e contém nenhum dos seus blocos de originais. Como resultado, a conta de Olá é cobrada para todos os blocos exclusivos oito. Este cenário pode ocorrer se estiver a utilizar um método de atualização, tais como [UploadFromFile][dotnet_UploadFromFile], [UploadText][dotnet_UploadText], [ UploadFromStream][dotnet_UploadFromStream], ou [UploadFromByteArray][dotnet_UploadFromByteArray], porque estes métodos substituem todos os conteúdos de Olá de um blob.

![Recursos de armazenamento do Azure](./media/storage-blob-snapshots/storage-blob-snapshots-billing-scenario-4.png)

## <a name="next-steps"></a>Passos seguintes

* Pode encontrar mais informações sobre como trabalhar com instantâneos de disco de máquina virtual (VM) no [cópia de segurança do Azure discos VM não geridos com instantâneos incrementais](storage-incremental-snapshots.md)

* Para obter exemplos de códigos adicionais utilizando o Blob storage, consulte [exemplos de código do Azure](https://azure.microsoft.com/documentation/samples/?service=storage&term=blob). Pode transferir uma aplicação de exemplo e executá-la ou procurar Olá código no GitHub.

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