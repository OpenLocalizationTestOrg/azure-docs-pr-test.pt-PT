---
title: aaaCreate e utilizar uma assinatura de acesso partilhado (SAS) com o Blob storage do Azure | Microsoft Docs
description: "Este tutorial mostra como toocreate partilhado assinaturas de acesso para utilização com o Blob storage e como tooconsume-las nas suas aplicações de cliente."
services: storage
documentationcenter: 
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 491e0b3c-76d4-4149-9a80-bbbd683b1f3e
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 05/15/2017
ms.author: marsma
ms.openlocfilehash: 629f5c0aee3f41115a0d514a2010d8cc0187126d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="shared-access-signatures-part-2-create-and-use-a-sas-with-blob-storage"></a>Partilhado assinaturas de acesso, parte 2: Criar e utilizar um SAS com o Blob storage

[Parte 1](storage-dotnet-shared-access-signature-part-1.md) deste tutorial, explorou partilhada assinaturas de acesso (SAS) e explicado melhores práticas para utilizá-los. Parte 2 mostra-lhe como toogenerate e, em seguida, de acesso partilhado assinaturas com o Blob storage. Exemplos de Olá são escritos em c# e utilizam Olá biblioteca de clientes do Storage do Azure para .NET. Exemplos de Olá neste tutorial:

* Gerar uma assinatura de acesso partilhado num contentor
* Gerar uma assinatura de acesso partilhado no blob
* Criar um acesso armazenado assinaturas de toomanage política nos recursos de um contentor
* Testar assinaturas de acesso de Olá partilhado numa aplicação de cliente

## <a name="about-this-tutorial"></a>Acerca deste tutorial
Neste tutorial, vamos criar duas aplicações de consola que demonstram criar e utilizar assinaturas de acesso partilhado para contentores e blobs:

**Aplicação 1**: Olá a aplicação de gestão. Gera uma assinatura de acesso partilhado para um contentor e um blob. Inclui a chave de acesso da conta de armazenamento de Olá no código fonte.

**Aplicação 2**: Olá aplicação cliente. Acede contentor de blob recursos e utilizar assinaturas de acesso de Olá partilhado criadas com a aplicação primeiro Olá. Utiliza apenas Olá acesso partilhado assinaturas tooaccess contentor e de recursos do blob – faz *não* incluem a chave de acesso da conta de armazenamento de Olá.

## <a name="part-1-create-a-console-application-toogenerate-shared-access-signatures"></a>Parte 1: Criar um aplicação toogenerate partilhado o acesso à consola assinaturas
Em primeiro lugar, certifique-se de que tem Olá biblioteca de clientes do Storage do Azure para .NET instalado. Pode instalar Olá [pacote NuGet](http://nuget.org/packages/WindowsAzure.Storage/ "pacote NuGet") que contém as assemblagens de mais atualizadas à sua Olá da biblioteca de cliente Olá. Este é Olá recomendado método para se certificar de que tem correções mais recentes Olá. Também pode transferir a biblioteca de clientes Olá como parte da versão mais recente do Olá do Olá [Azure SDK para .NET](https://azure.microsoft.com/downloads/).

No Visual Studio, crie uma nova aplicação de consola do Windows e dê-lhe nome **GenerateSharedAccessSignatures**. Adicione referências demasiado[configurationmanager](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager) e [Windowsazure](https://www.nuget.org/packages/WindowsAzure.Storage/) utilizando uma das seguintes abordagens de Olá:

* Olá utilize [Gestor de pacotes NuGet](https://docs.nuget.org/consume/installing-nuget) no Visual Studio. Selecione **projeto** > **gerir pacotes NuGet**, procure online por cada pacote (configurationmanager e Windowsazure) e instalá-los.
* Em alternativa, localize estas assemblagens na instalação do Olá SDK do Azure e adicionar referências toothem:
  * Microsoft.WindowsAzure.Configuration.dll
  * Microsoft.WindowsAzure.Storage.dll

Olá parte superior do ficheiro Program.cs de Olá, adicione o seguinte de Olá **utilizando** diretivas:

```csharp
using System.IO;
using Microsoft.Azure;
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Blob;
```

Edite o ficheiro App. config de Olá para que contém uma definição de configuração com uma cadeia de ligação que aponta tooyour conta de armazenamento. O ficheiro App. config deve ter um aspeto semelhante toothis uma:

```xml
<configuration>
  <startup>
    <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.5.2" />
  </startup>
  <appSettings>
    <add key="StorageConnectionString" value="DefaultEndpointsProtocol=https;AccountName=myaccount;AccountKey=mykey"/>
  </appSettings>
</configuration>
```

### <a name="generate-a-shared-access-signature-uri-for-a-container"></a>Gerar uma assinatura de acesso partilhado URI para um contentor
toobegin com, iremos adicionar um método toogenerate uma assinatura de acesso partilhado num novo contentor. Neste caso, assinatura de Olá não está associada uma política de acesso armazenada, para que acarreta no Olá informações de Olá URI que indica que as respetivas expiração tempo e Olá permissões concede.

Primeiro, adicione o código toohello **main ()** método tooauthenticate aceder à conta de armazenamento tooyour e criar um novo contentor:

```csharp
static void Main(string[] args)
{
    //Parse hello connection string and return a reference toohello storage account.
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(CloudConfigurationManager.GetSetting("StorageConnectionString"));

    //Create hello blob client object.
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

    //Get a reference tooa container toouse for hello sample code, and create it if it does not exist.
    CloudBlobContainer container = blobClient.GetContainerReference("sascontainer");
    container.CreateIfNotExists();

    //Insert calls toohello methods created below here...

    //Require user input before closing hello console window.
    Console.ReadLine();
}
```

Em seguida, adicione um método que gera a assinatura de acesso partilhado Olá para o contentor de Olá e devolve a assinatura de Olá URI:

```csharp
static string GetContainerSasUri(CloudBlobContainer container)
{
    //Set hello expiry time and permissions for hello container.
    //In this case no start time is specified, so hello shared access signature becomes valid immediately.
    SharedAccessBlobPolicy sasConstraints = new SharedAccessBlobPolicy();
    sasConstraints.SharedAccessExpiryTime = DateTimeOffset.UtcNow.AddHours(24);
    sasConstraints.Permissions = SharedAccessBlobPermissions.List | SharedAccessBlobPermissions.Write;

    //Generate hello shared access signature on hello container, setting hello constraints directly on hello signature.
    string sasContainerToken = container.GetSharedAccessSignature(sasConstraints);

    //Return hello URI string for hello container, including hello SAS token.
    return container.Uri + sasContainerToken;
}
```

Adicionar Olá seguintes linhas na parte inferior de Olá de Olá **main ()** método, antes de chamar o Olá demasiado**Console.ReadLine()**, toocall **GetContainerSasUri()** e escrever Olá janela de consola de toohello URI de assinatura:

```csharp
//Generate a SAS URI for hello container, without a stored access policy.
Console.WriteLine("Container SAS URI: " + GetContainerSasUri(container));
Console.WriteLine();
```

Compilar e executar toooutput Olá assinatura de acesso partilhado URI para o novo contentor de Olá. Olá URI será semelhante toohello seguinte:

```
https://storageaccount.blob.core.windows.net/sascontainer?sv=2012-02-12&se=2013-04-13T00%3A12%3A08Z&sr=c&sp=wl&sig=t%2BbzU9%2B7ry4okULN9S0wst%2F8MCUhTjrHyV9rDNLSe8g%3D
```

Depois de ter a executar o código de Olá, assinatura de acesso partilhado Olá que criou para o contentor de Olá será válida para Olá próximas 24 horas. assinatura de Olá atribui um cliente permissão toolist blobs contentor Olá e toowrite novo contentor de toohello de blobs.

### <a name="generate-a-shared-access-signature-uri-for-a-blob"></a>Gerar uma assinatura de acesso partilhado URI para um blob
Em seguida, iremos escrever toocreate de código semelhante um novo blob dentro do contentor de Olá e gerar uma assinatura de acesso partilhado para o mesmo. Esta assinatura de acesso partilhado não está associada uma política de acesso armazenada, pelo que inclui informações de permissão, hora de expiração e hora de início de Olá Olá URI.

Adicione um novo método que cria um novo blob e escreve tooit algum texto, em seguida, gera uma assinatura de acesso partilhado e devolve a assinatura de Olá URI:

```csharp
static string GetBlobSasUri(CloudBlobContainer container)
{
    //Get a reference tooa blob within hello container.
    CloudBlockBlob blob = container.GetBlockBlobReference("sasblob.txt");

    //Upload text toohello blob. If hello blob does not yet exist, it will be created.
    //If hello blob does exist, its existing content will be overwritten.
    string blobContent = "This blob will be accessible tooclients via a shared access signature (SAS).";
    blob.UploadText(blobContent);

    //Set hello expiry time and permissions for hello blob.
    //In this case, hello start time is specified as a few minutes in hello past, toomitigate clock skew.
    //hello shared access signature will be valid immediately.
    SharedAccessBlobPolicy sasConstraints = new SharedAccessBlobPolicy();
    sasConstraints.SharedAccessStartTime = DateTimeOffset.UtcNow.AddMinutes(-5);
    sasConstraints.SharedAccessExpiryTime = DateTimeOffset.UtcNow.AddHours(24);
    sasConstraints.Permissions = SharedAccessBlobPermissions.Read | SharedAccessBlobPermissions.Write;

    //Generate hello shared access signature on hello blob, setting hello constraints directly on hello signature.
    string sasBlobToken = blob.GetSharedAccessSignature(sasConstraints);

    //Return hello URI string for hello container, including hello SAS token.
    return blob.Uri + sasBlobToken;
}
```

Na parte inferior de Olá de Olá **main ()** método, adicione Olá seguintes linhas toocall **GetBlobSasUri()**, antes de chamar o Olá demasiado**Console.ReadLine()**e escrever Olá partilhado janela de consola do acesso assinatura URI toohello:

```csharp
//Generate a SAS URI for a blob within hello container, without a stored access policy.
Console.WriteLine("Blob SAS URI: " + GetBlobSasUri(container));
Console.WriteLine();
```

Compilar e executar toooutput Olá assinatura de acesso partilhado URI de blob Olá de novo. Olá URI será semelhante toohello seguinte:

```
https://storageaccount.blob.core.windows.net/sascontainer/sasblob.txt?sv=2012-02-12&st=2013-04-12T23%3A37%3A08Z&se=2013-04-13T00%3A12%3A08Z&sr=b&sp=rw&sig=dF2064yHtc8RusQLvkQFPItYdeOz3zR8zHsDMBi4S30%3D
```

### <a name="create-a-stored-access-policy-on-hello-container"></a>Criar uma política de acesso armazenada no contentor de Olá
Agora vamos criar uma política de acesso armazenada no contentor de Olá, que irá definir restrições Olá qualquer assinaturas de acesso partilhado que estão associados ao mesmo.

Nos exemplos anteriores Olá, especificamos hora de início de Olá (implícita ou explicitamente), tempo de expiração de Olá e permissões para Olá Olá partilhado URI próprio de assinatura de acesso. No Olá exemplos a seguir, iremos especificá-los na política de acesso de Olá armazenado, não na assinatura de acesso partilhado Olá. Se o fizer por isso, permite-nos toochange destas restrições sem emitir novamente Olá partilhadas aceder a assinatura.

É possível toohave uma ou várias das restrições de Olá na assinatura de acesso partilhado Olá e resto Olá na política de acesso de Olá armazenado. No entanto, apenas pode especificar a hora de início Olá, hora de expiração e as permissões num local ou Olá outro. Por exemplo, não é possível especificar permissões numa assinatura de acesso partilhado Olá e também especifique-os na política de acesso de Olá armazenado.

Quando adiciona um contentor de tooa de política de acesso armazenada, tem de obter permissões existentes do contentor de Olá, adicionar a nova política de acesso Olá e, em seguida, definir as permissões de um contentor Olá.

Adicione um novo método que cria uma nova política de acesso armazenado num contentor e devolve o nome de Olá da política de Olá:

```csharp
static void CreateSharedAccessPolicy(CloudBlobClient blobClient, CloudBlobContainer container,
    string policyName)
{
    //Get hello container's existing permissions.
    BlobContainerPermissions permissions = container.GetPermissions();

    //Create a new shared access policy and define its constraints.
    SharedAccessBlobPolicy sharedPolicy = new SharedAccessBlobPolicy()
    {
        SharedAccessExpiryTime = DateTimeOffset.UtcNow.AddHours(24),
        Permissions = SharedAccessBlobPermissions.Write | SharedAccessBlobPermissions.List | SharedAccessBlobPermissions.Read
    };

    //Add hello new policy toohello container's permissions, and set hello container's permissions.
    permissions.SharedAccessPolicies.Add(policyName, sharedPolicy);
    container.SetPermissions(permissions);
}
```

Na parte inferior de Olá de Olá **main ()** método, antes de chamar o Olá demasiado**Console.ReadLine()**, adicionar Olá seguir de linhas toofirst Limpe quaisquer políticas de acesso existentes e, em seguida, chame Olá  **CreateSharedAccessPolicy()** método:

```csharp
//Clear any existing access policies on container.
BlobContainerPermissions perms = container.GetPermissions();
perms.SharedAccessPolicies.Clear();
container.SetPermissions(perms);

//Create a new access policy on hello container, which may be optionally used tooprovide constraints for
//shared access signatures on hello container and hello blob.
string sharedAccessPolicyName = "tutorialpolicy";
CreateSharedAccessPolicy(blobClient, container, sharedAccessPolicyName);
```

Quando desmarcar as políticas de acesso de Olá num contentor, primeiro deve obter um contentor Olá permissões existentes, em seguida, permissões de limpar Olá e definir permissões de Olá novamente.

### <a name="generate-a-shared-access-signature-uri-on-hello-container-that-uses-an-access-policy"></a>Gerar uma assinatura de acesso partilhado URI no contentor de Olá que utiliza uma política de acesso
Em seguida, iremos criar outro assinatura de acesso partilhado do contentor de Olá que criámos anteriormente, mas neste momento, associar assinatura Olá política de acesso de Olá armazenado que no exemplo anterior Olá foi criada.

Adicione um novo toogenerate de método outro assinatura de acesso partilhado do contentor de Olá:

```csharp
static string GetContainerSasUriWithPolicy(CloudBlobContainer container, string policyName)
{
    //Generate hello shared access signature on hello container. In this case, all of hello constraints for the
    //shared access signature are specified on hello stored access policy.
    string sasContainerToken = container.GetSharedAccessSignature(null, policyName);

    //Return hello URI string for hello container, including hello SAS token.
    return container.Uri + sasContainerToken;
}
```

Na parte inferior de Olá de Olá **main ()** método, antes de chamar o Olá demasiado**Console.ReadLine()**, adicionar Olá seguir Olá de toocall linhas **GetContainerSasUriWithPolicy** método :

```csharp
//Generate a SAS URI for hello container, using a stored access policy tooset constraints on hello SAS.
Console.WriteLine("Container SAS URI using stored access policy: " + GetContainerSasUriWithPolicy(container, sharedAccessPolicyName));
Console.WriteLine();
```

### <a name="generate-a-shared-access-signature-uri-on-hello-blob-that-uses-an-access-policy"></a>Gerar um URI de assinatura de acesso partilhado no Olá Blob que utiliza uma política de acesso
Por fim, vamos adicionar um toocreate método semelhante outro blob e gerar uma assinatura de acesso partilhado que está associada a uma política de acesso armazenada.

Adicione um novo toocreate de método um blob e gerar uma assinatura de acesso partilhado:

```csharp
static string GetBlobSasUriWithPolicy(CloudBlobContainer container, string policyName)
{
    //Get a reference tooa blob within hello container.
    CloudBlockBlob blob = container.GetBlockBlobReference("sasblobpolicy.txt");

    //Upload text toohello blob. If hello blob does not yet exist, it will be created.
    //If hello blob does exist, its existing content will be overwritten.
    string blobContent = "This blob will be accessible tooclients via a shared access signature. " +
    "A stored access policy defines hello constraints for hello signature.";
    MemoryStream ms = new MemoryStream(Encoding.UTF8.GetBytes(blobContent));
    ms.Position = 0;
    using (ms)
    {
        blob.UploadFromStream(ms);
    }

    //Generate hello shared access signature on hello blob.
    string sasBlobToken = blob.GetSharedAccessSignature(null, policyName);

    //Return hello URI string for hello container, including hello SAS token.
    return blob.Uri + sasBlobToken;
}
```

Na parte inferior de Olá de Olá **main ()** método, antes de chamar o Olá demasiado**Console.ReadLine()**, adicionar Olá seguir Olá de toocall linhas **GetBlobSasUriWithPolicy** método:

```csharp
//Generate a SAS URI for a blob within hello container, using a stored access policy tooset constraints on hello SAS.
Console.WriteLine("Blob SAS URI using stored access policy: " + GetBlobSasUriWithPolicy(container, sharedAccessPolicyName));
Console.WriteLine();
```

Olá **main ()** método deve agora ter este aspeto na íntegra. Execute-a assinatura de acesso partilhado do toowrite Olá janela de consola toohello de URIs, em seguida, copie e cole-los para um ficheiro de texto para utilização num Olá segunda parte deste tutorial.

```csharp
static void Main(string[] args)
{
    //Parse hello connection string and return a reference toohello storage account.
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(CloudConfigurationManager.GetSetting("StorageConnectionString"));

    //Create hello blob client object.
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

    //Get a reference tooa container toouse for hello sample code, and create it if it does not exist.
    CloudBlobContainer container = blobClient.GetContainerReference("sascontainer");
    container.CreateIfNotExists();

    //Generate a SAS URI for hello container, without a stored access policy.
    Console.WriteLine("Container SAS URI: " + GetContainerSasUri(container));
    Console.WriteLine();

    //Generate a SAS URI for a blob within hello container, without a stored access policy.
    Console.WriteLine("Blob SAS URI: " + GetBlobSasUri(container));
    Console.WriteLine();

    //Clear any existing access policies on container.
    BlobContainerPermissions perms = container.GetPermissions();
    perms.SharedAccessPolicies.Clear();
    container.SetPermissions(perms);

    //Create a new access policy on hello container, which may be optionally used tooprovide constraints for
    //shared access signatures on hello container and hello blob.
    string sharedAccessPolicyName = "tutorialpolicy";
    CreateSharedAccessPolicy(blobClient, container, sharedAccessPolicyName);

    //Generate a SAS URI for hello container, using a stored access policy tooset constraints on hello SAS.
    Console.WriteLine("Container SAS URI using stored access policy: " + GetContainerSasUriWithPolicy(container, sharedAccessPolicyName));
    Console.WriteLine();

    //Generate a SAS URI for a blob within hello container, using a stored access policy tooset constraints on hello SAS.
    Console.WriteLine("Blob SAS URI using stored access policy: " + GetBlobSasUriWithPolicy(container, sharedAccessPolicyName));
    Console.WriteLine();

    Console.ReadLine();
}
```

Quando executar a aplicação de consola GenerateSharedAccessSignatures Olá, verá a seguinte de toohello semelhante de saída. Estes são utilizados na parte 2 do tutorial Olá assinaturas de acesso de Olá partilhado.

```
Container SAS URI: https://storagesample.blob.core.windows.net/sascontainer?sv=2016-05-31&sr=c&sig=pFlEZD%2F6sJTNLxD%2FQ26Hh85j%2FzYPxZav6mP1KJwnvJE%3D&se=2017-05-16T16%3A16%3A47Z&sp=wl

Blob SAS URI: https://storagesample.blob.core.windows.net/sascontainer/sasblob.txt?sv=2016-05-31&sr=b&sig=%2FiBWAZbXESzCMvRcm7JwJBK0gT0BtPSWEq4pRwmlBRI%3D&st=2017-05-15T16%3A11%3A48Z&se=2017-05-16T16%3A16%3A48Z&sp=rw

Container SAS URI using stored access policy: https://storagesample.blob.core.windows.net/sascontainer?sv=2016-05-31&sr=c&si=tutorialpolicy&sig=aMb6rKDvvpfiGVsZI2rCmyUra6ZPpq%2BZ%2FLyTgAeec%2Bk%3D

Blob SAS URI using stored access policy: https://storagesample.blob.core.windows.net/sascontainer/sasblobpolicy.txt?sv=2016-05-31&sr=b&si=tutorialpolicy&sig=%2FkTWkT23SS45%2FoF4bK2mqXkN%2BPKs%2FyHuzkfQ4GFoZVU%3D
```

## <a name="part-2-create-a-console-application-tootest-hello-shared-access-signatures"></a>Parte 2: Criar um aplicação tootest Olá partilhado o acesso à consola assinaturas
Olá tootest partilhadas assinaturas de acesso que criou nos exemplos anteriores Olá, iremos criar uma segunda aplicação de consola que utiliza as operações de tooperform de assinaturas hello no contentor de Olá e um blob.

> [!NOTE]
> Se mais de 24 horas passaram, uma vez que concluir a primeira parte de Olá tutorial Olá, assinaturas hello gerou já não será válidas. Neste caso, deve executar o código de Olá na toogenerate de aplicação de consola primeiro Olá assinaturas de acesso partilhado raiz para utilização num Olá segunda parte tutorial Olá.
>

No Visual Studio, crie uma nova aplicação de consola do Windows e dê-lhe nome **ConsumeSharedAccessSignatures**. Adicione referências demasiado[configurationmanager](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager) e [Windowsazure](https://www.nuget.org/packages/WindowsAzure.Storage/), tal como fez anteriormente.

Olá parte superior do ficheiro Program.cs de Olá, adicione o seguinte de Olá **utilizando** diretivas:

```csharp
using System.IO;
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Blob;
```

No corpo de Olá de Olá **main ()** método, adicione Olá seguir as constantes string, alterar as assinaturas de acesso de toohello partilhado valores gerado na parte 1 do tutorial Olá.

```csharp
static void Main(string[] args)
{
    const string containerSAS = "<your container SAS>";
    const string blobSAS = "<your blob SAS>";
    const string containerSASWithAccessPolicy = "<your container SAS with access policy>";
    const string blobSASWithAccessPolicy = "<your blob SAS with access policy>";
}
```

### <a name="add-a-method-tootry-container-operations-using-a-shared-access-signature"></a>Adicione um método tootry contentor de operações com uma assinatura de acesso partilhado
Em seguida, iremos adicionar um método que os testes de algumas operações de contentor com uma assinatura de acesso partilhado do contentor de Olá. assinatura de acesso partilhado Olá é tooreturn utilizado um contentor de toohello referência, autenticar o contentor de toohello de acesso com base na assinatura Olá individualmente.

Adicione Olá método tooProgram.cs os seguintes:

```csharp
static void UseContainerSAS(string sas)
{
    //Try performing container operations with hello SAS provided.

    //Return a reference toohello container using hello SAS URI.
    CloudBlobContainer container = new CloudBlobContainer(new Uri(sas));

    //Create a list toostore blob URIs returned by a listing operation on hello container.
    List<ICloudBlob> blobList = new List<ICloudBlob>();

    //Write operation: write a new blob toohello container.
    try
    {
        CloudBlockBlob blob = container.GetBlockBlobReference("blobCreatedViaSAS.txt");
        string blobContent = "This blob was created with a shared access signature granting write permissions toohello container. ";
        blob.UploadText(blobContent);

        Console.WriteLine("Write operation succeeded for SAS " + sas);
        Console.WriteLine();
    }
    catch (StorageException e)
    {
        Console.WriteLine("Write operation failed for SAS " + sas);
        Console.WriteLine("Additional error information: " + e.Message);
        Console.WriteLine();
    }

    //List operation: List hello blobs in hello container.
    try
    {
        foreach (ICloudBlob blob in container.ListBlobs())
        {
            blobList.Add(blob);
        }
        Console.WriteLine("List operation succeeded for SAS " + sas);
        Console.WriteLine();
    }
    catch (StorageException e)
    {
        Console.WriteLine("List operation failed for SAS " + sas);
        Console.WriteLine("Additional error information: " + e.Message);
        Console.WriteLine();
    }

    //Read operation: Get a reference tooone of hello blobs in hello container and read it.
    try
    {
        CloudBlockBlob blob = container.GetBlockBlobReference(blobList[0].Name);
        MemoryStream msRead = new MemoryStream();
        msRead.Position = 0;
        using (msRead)
        {
            blob.DownloadToStream(msRead);
            Console.WriteLine(msRead.Length);
        }
        Console.WriteLine("Read operation succeeded for SAS " + sas);
        Console.WriteLine();
    }
    catch (StorageException e)
    {
        Console.WriteLine("Read operation failed for SAS " + sas);
        Console.WriteLine("Additional error information: " + e.Message);
        Console.WriteLine();
    }
    Console.WriteLine();

    //Delete operation: Delete a blob in hello container.
    try
    {
        CloudBlockBlob blob = container.GetBlockBlobReference(blobList[0].Name);
        blob.Delete();
        Console.WriteLine("Delete operation succeeded for SAS " + sas);
        Console.WriteLine();
    }
    catch (StorageException e)
    {
        Console.WriteLine("Delete operation failed for SAS " + sas);
        Console.WriteLine("Additional error information: " + e.Message);
        Console.WriteLine();
    }
}
```

Olá atualização **main ()** método toocall **UseContainerSAS()** com ambos Olá de assinaturas de acesso que criou no contentor de Olá partilhado:

```csharp
static void Main(string[] args)
{
    string containerSAS = "<your container SAS>";
    string blobSAS = "<your blob SAS>";
    string containerSASWithAccessPolicy = "<your container SAS with access policy>";
    string blobSASWithAccessPolicy = "<your blob SAS with access policy>";

    //Call hello test methods with hello shared access signatures created on hello container, with and without hello access policy.
    UseContainerSAS(containerSAS);
    UseContainerSAS(containerSASWithAccessPolicy);

    Console.ReadLine();
}
```

### <a name="add-a-method-tootry-blob-operations-using-a-shared-access-signature"></a>Adicione um método tootry blob de operações com uma assinatura de acesso partilhado
Por último, iremos adicionar um método que os testes de algumas operações de blob a utilizar uma assinatura de acesso partilhado no blob Olá. Neste caso, utilizamos o construtor de Olá **CloudBlockBlob(String)**, passando na assinatura de acesso partilhado Olá, tooreturn um blob de toohello de referência. Não outra é necessária autenticação; baseia-se na assinatura Olá individualmente.

Adicione Olá método tooProgram.cs os seguintes:

```csharp
static void UseBlobSAS(string sas)
{
    //Try performing blob operations using hello SAS provided.

    //Return a reference toohello blob using hello SAS URI.
    CloudBlockBlob blob = new CloudBlockBlob(new Uri(sas));

    //Write operation: Write a new blob toohello container.
    try
    {
        string blobContent = "This blob was created with a shared access signature granting write permissions toohello blob. ";
        MemoryStream msWrite = new MemoryStream(Encoding.UTF8.GetBytes(blobContent));
        msWrite.Position = 0;
        using (msWrite)
        {
            blob.UploadFromStream(msWrite);
        }
        Console.WriteLine("Write operation succeeded for SAS " + sas);
        Console.WriteLine();
    }
    catch (StorageException e)
    {
        Console.WriteLine("Write operation failed for SAS " + sas);
        Console.WriteLine("Additional error information: " + e.Message);
        Console.WriteLine();
    }

    //Read operation: Read hello contents of hello blob.
    try
    {
        MemoryStream msRead = new MemoryStream();
        using (msRead)
        {
            blob.DownloadToStream(msRead);
            msRead.Position = 0;
            using (StreamReader reader = new StreamReader(msRead, true))
            {
                string line;
                while ((line = reader.ReadLine()) != null)
                {
                    Console.WriteLine(line);
                }
            }
        }
        Console.WriteLine("Read operation succeeded for SAS " + sas);
        Console.WriteLine();
    }
    catch (StorageException e)
    {
        Console.WriteLine("Read operation failed for SAS " + sas);
        Console.WriteLine("Additional error information: " + e.Message);
        Console.WriteLine();
    }

    //Delete operation: Delete hello blob.
    try
    {
        blob.Delete();
        Console.WriteLine("Delete operation succeeded for SAS " + sas);
        Console.WriteLine();
    }
    catch (StorageException e)
    {
        Console.WriteLine("Delete operation failed for SAS " + sas);
        Console.WriteLine("Additional error information: " + e.Message);
        Console.WriteLine();
    }
}
```

Olá atualização **main ()** método toocall **UseBlobSAS()** com ambos Olá de assinaturas de acesso que criou no blob Olá partilhado:

```csharp
static void Main(string[] args)
{
    string containerSAS = "<your container SAS>";
    string blobSAS = "<your blob SAS>";
    string containerSASWithAccessPolicy = "<your container SAS with access policy>";
    string blobSASWithAccessPolicy = "<your blob SAS with access policy>";

    //Call hello test methods with hello shared access signatures created on hello container, with and without hello access policy.
    UseContainerSAS(containerSAS);
    UseContainerSAS(containerSASWithAccessPolicy);

    //Call hello test methods with hello shared access signatures created on hello blob, with and without hello access policy.
    UseBlobSAS(blobSAS);
    UseBlobSAS(blobSASWithAccessPolicy);

    Console.ReadLine();
}
```

Executar a aplicação de consola Olá e observe Olá saída toosee as operações são permitidas para as assinaturas. saída de Olá na janela de consola Olá terá um aspeto semelhante toohello seguinte:

```
Write operation succeeded for SAS https://storagesample.blob.core.windows.net/sascontainer?sv=2016-05-31&sr=c&sig=32EaQGuFyDMb3yOAey3wq%2B%2FLwgPQxAgSo7UhzLdyIDU%3D&se=2017-05-16T15%3A41%3A20Z&sp=wl

List operation succeeded for SAS https://storagesample.blob.core.windows.net/sascontainer?sv=2016-05-31&sr=c&sig=32EaQGuFyDMb3yOAey3wq%2B%2FLwgPQxAgSo7UhzLdyIDU%3D&se=2017-05-16T15%3A41%3A20Z&sp=wl

Read operation failed for SAS https://storagesample.blob.core.windows.net/sascontainer?sv=2016-05-31&sr=c&sig=32EaQGuFyDMb3yOAey3wq%2B%2FLwgPQxAgSo7UhzLdyIDU%3D&se=2017-05-16T15%3A41%3A20Z&sp=wl
Additional error information: hello remote server returned an error: (403) Forbidden.

Delete operation failed for SAS https://storagesample.blob.core.windows.net/sascontainer?sv=2016-05-31&sr=c&sig=32EaQGuFyDMb3yOAey3wq%2B%2FLwgPQxAgSo7UhzLdyIDU%3D&se=2017-05-16T15%3A41%3A20Z&sp=wl
Additional error information: hello remote server returned an error: (403) Forbidden.

...
```

## <a name="next-steps"></a>Passos Seguintes

* [Assinaturas de acesso partilhado, parte 1: Olá de compreensão modelo SAS](storage-dotnet-shared-access-signature-part-1.md)
* [Gerir o acesso de leitura anónimo toocontainers e blobs](storage-manage-access-to-resources.md)
* [Delegar o acesso com uma assinatura de acesso partilhado (REST API)](http://msdn.microsoft.com/library/azure/ee395415.aspx)
* [Introduzir tabela e fila SAS](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-table-sas-shared-access-signature-queue-sas-and-update-to-blob-sas.aspx)
