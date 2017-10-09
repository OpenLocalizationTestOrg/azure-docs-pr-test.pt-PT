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
# <a name="shared-access-signatures-part-2-create-and-use-a-sas-with-blob-storage"></a><span data-ttu-id="7c2b6-103">Partilhado assinaturas de acesso, parte 2: Criar e utilizar um SAS com o Blob storage</span><span class="sxs-lookup"><span data-stu-id="7c2b6-103">Shared Access Signatures, Part 2: Create and use a SAS with Blob storage</span></span>

<span data-ttu-id="7c2b6-104">[Parte 1](storage-dotnet-shared-access-signature-part-1.md) deste tutorial, explorou partilhada assinaturas de acesso (SAS) e explicado melhores práticas para utilizá-los.</span><span class="sxs-lookup"><span data-stu-id="7c2b6-104">[Part 1](storage-dotnet-shared-access-signature-part-1.md) of this tutorial explored shared access signatures (SAS) and explained best practices for using them.</span></span> <span data-ttu-id="7c2b6-105">Parte 2 mostra-lhe como toogenerate e, em seguida, de acesso partilhado assinaturas com o Blob storage.</span><span class="sxs-lookup"><span data-stu-id="7c2b6-105">Part 2 shows you how toogenerate and then use shared access signatures with Blob storage.</span></span> <span data-ttu-id="7c2b6-106">Exemplos de Olá são escritos em c# e utilizam Olá biblioteca de clientes do Storage do Azure para .NET.</span><span class="sxs-lookup"><span data-stu-id="7c2b6-106">hello examples are written in C# and use hello Azure Storage Client Library for .NET.</span></span> <span data-ttu-id="7c2b6-107">Exemplos de Olá neste tutorial:</span><span class="sxs-lookup"><span data-stu-id="7c2b6-107">hello examples in this tutorial:</span></span>

* <span data-ttu-id="7c2b6-108">Gerar uma assinatura de acesso partilhado num contentor</span><span class="sxs-lookup"><span data-stu-id="7c2b6-108">Generate a shared access signature on a container</span></span>
* <span data-ttu-id="7c2b6-109">Gerar uma assinatura de acesso partilhado no blob</span><span class="sxs-lookup"><span data-stu-id="7c2b6-109">Generate a shared access signature on a blob</span></span>
* <span data-ttu-id="7c2b6-110">Criar um acesso armazenado assinaturas de toomanage política nos recursos de um contentor</span><span class="sxs-lookup"><span data-stu-id="7c2b6-110">Create a stored access policy toomanage signatures on a container's resources</span></span>
* <span data-ttu-id="7c2b6-111">Testar assinaturas de acesso de Olá partilhado numa aplicação de cliente</span><span class="sxs-lookup"><span data-stu-id="7c2b6-111">Test hello shared access signatures in a client application</span></span>

## <a name="about-this-tutorial"></a><span data-ttu-id="7c2b6-112">Acerca deste tutorial</span><span class="sxs-lookup"><span data-stu-id="7c2b6-112">About this tutorial</span></span>
<span data-ttu-id="7c2b6-113">Neste tutorial, vamos criar duas aplicações de consola que demonstram criar e utilizar assinaturas de acesso partilhado para contentores e blobs:</span><span class="sxs-lookup"><span data-stu-id="7c2b6-113">In this tutorial, we create two console applications that demonstrate creating and using shared access signatures for containers and blobs:</span></span>

<span data-ttu-id="7c2b6-114">**Aplicação 1**: Olá a aplicação de gestão.</span><span class="sxs-lookup"><span data-stu-id="7c2b6-114">**Application 1**: hello management application.</span></span> <span data-ttu-id="7c2b6-115">Gera uma assinatura de acesso partilhado para um contentor e um blob.</span><span class="sxs-lookup"><span data-stu-id="7c2b6-115">Generates a shared access signature for a container and a blob.</span></span> <span data-ttu-id="7c2b6-116">Inclui a chave de acesso da conta de armazenamento de Olá no código fonte.</span><span class="sxs-lookup"><span data-stu-id="7c2b6-116">Includes hello storage account access key in source code.</span></span>

<span data-ttu-id="7c2b6-117">**Aplicação 2**: Olá aplicação cliente.</span><span class="sxs-lookup"><span data-stu-id="7c2b6-117">**Application 2**: hello client application.</span></span> <span data-ttu-id="7c2b6-118">Acede contentor de blob recursos e utilizar assinaturas de acesso de Olá partilhado criadas com a aplicação primeiro Olá.</span><span class="sxs-lookup"><span data-stu-id="7c2b6-118">Accesses container and blob resources using hello shared access signatures created with hello first application.</span></span> <span data-ttu-id="7c2b6-119">Utiliza apenas Olá acesso partilhado assinaturas tooaccess contentor e de recursos do blob – faz *não* incluem a chave de acesso da conta de armazenamento de Olá.</span><span class="sxs-lookup"><span data-stu-id="7c2b6-119">Uses only hello shared access signatures tooaccess container and blob resources--it does *not* include hello storage account access key.</span></span>

## <a name="part-1-create-a-console-application-toogenerate-shared-access-signatures"></a><span data-ttu-id="7c2b6-120">Parte 1: Criar um aplicação toogenerate partilhado o acesso à consola assinaturas</span><span class="sxs-lookup"><span data-stu-id="7c2b6-120">Part 1: Create a console application toogenerate shared access signatures</span></span>
<span data-ttu-id="7c2b6-121">Em primeiro lugar, certifique-se de que tem Olá biblioteca de clientes do Storage do Azure para .NET instalado.</span><span class="sxs-lookup"><span data-stu-id="7c2b6-121">First, ensure that you have hello Azure Storage Client Library for .NET installed.</span></span> <span data-ttu-id="7c2b6-122">Pode instalar Olá [pacote NuGet](http://nuget.org/packages/WindowsAzure.Storage/ "pacote NuGet") que contém as assemblagens de mais atualizadas à sua Olá da biblioteca de cliente Olá.</span><span class="sxs-lookup"><span data-stu-id="7c2b6-122">You can install hello [NuGet package](http://nuget.org/packages/WindowsAzure.Storage/ "NuGet package") containing hello most up-to-date assemblies for hello client library.</span></span> <span data-ttu-id="7c2b6-123">Este é Olá recomendado método para se certificar de que tem correções mais recentes Olá.</span><span class="sxs-lookup"><span data-stu-id="7c2b6-123">This is hello recommended method for ensuring that you have hello most recent fixes.</span></span> <span data-ttu-id="7c2b6-124">Também pode transferir a biblioteca de clientes Olá como parte da versão mais recente do Olá do Olá [Azure SDK para .NET](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="7c2b6-124">You can also download hello client library as part of hello most recent version of hello [Azure SDK for .NET](https://azure.microsoft.com/downloads/).</span></span>

<span data-ttu-id="7c2b6-125">No Visual Studio, crie uma nova aplicação de consola do Windows e dê-lhe nome **GenerateSharedAccessSignatures**.</span><span class="sxs-lookup"><span data-stu-id="7c2b6-125">In Visual Studio, create a new Windows console application and name it **GenerateSharedAccessSignatures**.</span></span> <span data-ttu-id="7c2b6-126">Adicione referências demasiado[configurationmanager](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager) e [Windowsazure](https://www.nuget.org/packages/WindowsAzure.Storage/) utilizando uma das seguintes abordagens de Olá:</span><span class="sxs-lookup"><span data-stu-id="7c2b6-126">Add references too[Microsoft.WindowsAzure.ConfigurationManager](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager) and [WindowsAzure.Storage](https://www.nuget.org/packages/WindowsAzure.Storage/) by using one of hello following approaches:</span></span>

* <span data-ttu-id="7c2b6-127">Olá utilize [Gestor de pacotes NuGet](https://docs.nuget.org/consume/installing-nuget) no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7c2b6-127">Use hello [NuGet package manager](https://docs.nuget.org/consume/installing-nuget) in Visual Studio.</span></span> <span data-ttu-id="7c2b6-128">Selecione **projeto** > **gerir pacotes NuGet**, procure online por cada pacote (configurationmanager e Windowsazure) e instalá-los.</span><span class="sxs-lookup"><span data-stu-id="7c2b6-128">Select **Project** > **Manage NuGet Packages**, search online for each package (Microsoft.WindowsAzure.ConfigurationManager and WindowsAzure.Storage) and install them.</span></span>
* <span data-ttu-id="7c2b6-129">Em alternativa, localize estas assemblagens na instalação do Olá SDK do Azure e adicionar referências toothem:</span><span class="sxs-lookup"><span data-stu-id="7c2b6-129">Alternatively, locate these assemblies in your installation of hello Azure SDK and add references toothem:</span></span>
  * <span data-ttu-id="7c2b6-130">Microsoft.WindowsAzure.Configuration.dll</span><span class="sxs-lookup"><span data-stu-id="7c2b6-130">Microsoft.WindowsAzure.Configuration.dll</span></span>
  * <span data-ttu-id="7c2b6-131">Microsoft.WindowsAzure.Storage.dll</span><span class="sxs-lookup"><span data-stu-id="7c2b6-131">Microsoft.WindowsAzure.Storage.dll</span></span>

<span data-ttu-id="7c2b6-132">Olá parte superior do ficheiro Program.cs de Olá, adicione o seguinte de Olá **utilizando** diretivas:</span><span class="sxs-lookup"><span data-stu-id="7c2b6-132">At hello top of hello Program.cs file, add hello following **using** directives:</span></span>

```csharp
using System.IO;
using Microsoft.Azure;
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Blob;
```

<span data-ttu-id="7c2b6-133">Edite o ficheiro App. config de Olá para que contém uma definição de configuração com uma cadeia de ligação que aponta tooyour conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="7c2b6-133">Edit hello app.config file so that it contains a configuration setting with a connection string that points tooyour storage account.</span></span> <span data-ttu-id="7c2b6-134">O ficheiro App. config deve ter um aspeto semelhante toothis uma:</span><span class="sxs-lookup"><span data-stu-id="7c2b6-134">Your app.config file should look similar toothis one:</span></span>

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

### <a name="generate-a-shared-access-signature-uri-for-a-container"></a><span data-ttu-id="7c2b6-135">Gerar uma assinatura de acesso partilhado URI para um contentor</span><span class="sxs-lookup"><span data-stu-id="7c2b6-135">Generate a shared access signature URI for a container</span></span>
<span data-ttu-id="7c2b6-136">toobegin com, iremos adicionar um método toogenerate uma assinatura de acesso partilhado num novo contentor.</span><span class="sxs-lookup"><span data-stu-id="7c2b6-136">toobegin with, we add a method toogenerate a shared access signature on a new container.</span></span> <span data-ttu-id="7c2b6-137">Neste caso, assinatura de Olá não está associada uma política de acesso armazenada, para que acarreta no Olá informações de Olá URI que indica que as respetivas expiração tempo e Olá permissões concede.</span><span class="sxs-lookup"><span data-stu-id="7c2b6-137">In this case, hello signature is not associated with a stored access policy, so it carries on hello URI hello information indicating its expiry time and hello permissions it grants.</span></span>

<span data-ttu-id="7c2b6-138">Primeiro, adicione o código toohello **main ()** método tooauthenticate aceder à conta de armazenamento tooyour e criar um novo contentor:</span><span class="sxs-lookup"><span data-stu-id="7c2b6-138">First, add code toohello **Main()** method tooauthenticate access tooyour storage account and create a new container:</span></span>

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

<span data-ttu-id="7c2b6-139">Em seguida, adicione um método que gera a assinatura de acesso partilhado Olá para o contentor de Olá e devolve a assinatura de Olá URI:</span><span class="sxs-lookup"><span data-stu-id="7c2b6-139">Next, add a method that generates hello shared access signature for hello container and returns hello signature URI:</span></span>

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

<span data-ttu-id="7c2b6-140">Adicionar Olá seguintes linhas na parte inferior de Olá de Olá **main ()** método, antes de chamar o Olá demasiado**Console.ReadLine()**, toocall **GetContainerSasUri()** e escrever Olá janela de consola de toohello URI de assinatura:</span><span class="sxs-lookup"><span data-stu-id="7c2b6-140">Add hello following lines at hello bottom of hello **Main()** method, before hello call too**Console.ReadLine()**, toocall **GetContainerSasUri()** and write hello signature URI toohello console window:</span></span>

```csharp
//Generate a SAS URI for hello container, without a stored access policy.
Console.WriteLine("Container SAS URI: " + GetContainerSasUri(container));
Console.WriteLine();
```

<span data-ttu-id="7c2b6-141">Compilar e executar toooutput Olá assinatura de acesso partilhado URI para o novo contentor de Olá.</span><span class="sxs-lookup"><span data-stu-id="7c2b6-141">Compile and run toooutput hello shared access signature URI for hello new container.</span></span> <span data-ttu-id="7c2b6-142">Olá URI será semelhante toohello seguinte:</span><span class="sxs-lookup"><span data-stu-id="7c2b6-142">hello URI will be similar toohello following:</span></span>

```
https://storageaccount.blob.core.windows.net/sascontainer?sv=2012-02-12&se=2013-04-13T00%3A12%3A08Z&sr=c&sp=wl&sig=t%2BbzU9%2B7ry4okULN9S0wst%2F8MCUhTjrHyV9rDNLSe8g%3D
```

<span data-ttu-id="7c2b6-143">Depois de ter a executar o código de Olá, assinatura de acesso partilhado Olá que criou para o contentor de Olá será válida para Olá próximas 24 horas.</span><span class="sxs-lookup"><span data-stu-id="7c2b6-143">Once you have run hello code, hello shared access signature you created for hello container will be valid for hello next 24 hours.</span></span> <span data-ttu-id="7c2b6-144">assinatura de Olá atribui um cliente permissão toolist blobs contentor Olá e toowrite novo contentor de toohello de blobs.</span><span class="sxs-lookup"><span data-stu-id="7c2b6-144">hello signature grants a client permission toolist blobs in hello container and toowrite new blobs toohello container.</span></span>

### <a name="generate-a-shared-access-signature-uri-for-a-blob"></a><span data-ttu-id="7c2b6-145">Gerar uma assinatura de acesso partilhado URI para um blob</span><span class="sxs-lookup"><span data-stu-id="7c2b6-145">Generate a shared access signature URI for a blob</span></span>
<span data-ttu-id="7c2b6-146">Em seguida, iremos escrever toocreate de código semelhante um novo blob dentro do contentor de Olá e gerar uma assinatura de acesso partilhado para o mesmo.</span><span class="sxs-lookup"><span data-stu-id="7c2b6-146">Next, we write similar code toocreate a new blob within hello container and generate a shared access signature for it.</span></span> <span data-ttu-id="7c2b6-147">Esta assinatura de acesso partilhado não está associada uma política de acesso armazenada, pelo que inclui informações de permissão, hora de expiração e hora de início de Olá Olá URI.</span><span class="sxs-lookup"><span data-stu-id="7c2b6-147">This shared access signature is not associated with a stored access policy, so it includes hello start time, expiry time, and permission information in hello URI.</span></span>

<span data-ttu-id="7c2b6-148">Adicione um novo método que cria um novo blob e escreve tooit algum texto, em seguida, gera uma assinatura de acesso partilhado e devolve a assinatura de Olá URI:</span><span class="sxs-lookup"><span data-stu-id="7c2b6-148">Add a new method that creates a new blob and writes some text tooit, then generates a shared access signature and returns hello signature URI:</span></span>

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

<span data-ttu-id="7c2b6-149">Na parte inferior de Olá de Olá **main ()** método, adicione Olá seguintes linhas toocall **GetBlobSasUri()**, antes de chamar o Olá demasiado**Console.ReadLine()**e escrever Olá partilhado janela de consola do acesso assinatura URI toohello:</span><span class="sxs-lookup"><span data-stu-id="7c2b6-149">At hello bottom of hello **Main()** method, add hello following lines toocall **GetBlobSasUri()**, before hello call too**Console.ReadLine()**, and write hello shared access signature URI toohello console window:</span></span>

```csharp
//Generate a SAS URI for a blob within hello container, without a stored access policy.
Console.WriteLine("Blob SAS URI: " + GetBlobSasUri(container));
Console.WriteLine();
```

<span data-ttu-id="7c2b6-150">Compilar e executar toooutput Olá assinatura de acesso partilhado URI de blob Olá de novo.</span><span class="sxs-lookup"><span data-stu-id="7c2b6-150">Compile and run toooutput hello shared access signature URI for hello new blob.</span></span> <span data-ttu-id="7c2b6-151">Olá URI será semelhante toohello seguinte:</span><span class="sxs-lookup"><span data-stu-id="7c2b6-151">hello URI will be similar toohello following:</span></span>

```
https://storageaccount.blob.core.windows.net/sascontainer/sasblob.txt?sv=2012-02-12&st=2013-04-12T23%3A37%3A08Z&se=2013-04-13T00%3A12%3A08Z&sr=b&sp=rw&sig=dF2064yHtc8RusQLvkQFPItYdeOz3zR8zHsDMBi4S30%3D
```

### <a name="create-a-stored-access-policy-on-hello-container"></a><span data-ttu-id="7c2b6-152">Criar uma política de acesso armazenada no contentor de Olá</span><span class="sxs-lookup"><span data-stu-id="7c2b6-152">Create a stored access policy on hello container</span></span>
<span data-ttu-id="7c2b6-153">Agora vamos criar uma política de acesso armazenada no contentor de Olá, que irá definir restrições Olá qualquer assinaturas de acesso partilhado que estão associados ao mesmo.</span><span class="sxs-lookup"><span data-stu-id="7c2b6-153">Now let's create a stored access policy on hello container, which will define hello constraints for any shared access signatures that are associated with it.</span></span>

<span data-ttu-id="7c2b6-154">Nos exemplos anteriores Olá, especificamos hora de início de Olá (implícita ou explicitamente), tempo de expiração de Olá e permissões para Olá Olá partilhado URI próprio de assinatura de acesso.</span><span class="sxs-lookup"><span data-stu-id="7c2b6-154">In hello previous examples, we specified hello start time (implicitly or explicitly), hello expiry time, and hello permissions on hello shared access signature URI itself.</span></span> <span data-ttu-id="7c2b6-155">No Olá exemplos a seguir, iremos especificá-los na política de acesso de Olá armazenado, não na assinatura de acesso partilhado Olá.</span><span class="sxs-lookup"><span data-stu-id="7c2b6-155">In hello following examples, we specify these on hello stored access policy, not on hello shared access signature.</span></span> <span data-ttu-id="7c2b6-156">Se o fizer por isso, permite-nos toochange destas restrições sem emitir novamente Olá partilhadas aceder a assinatura.</span><span class="sxs-lookup"><span data-stu-id="7c2b6-156">Doing so enables us toochange these constraints without reissuing hello shared access signature.</span></span>

<span data-ttu-id="7c2b6-157">É possível toohave uma ou várias das restrições de Olá na assinatura de acesso partilhado Olá e resto Olá na política de acesso de Olá armazenado.</span><span class="sxs-lookup"><span data-stu-id="7c2b6-157">It's possible toohave one or more of hello constraints on hello shared access signature, and hello remainder on hello stored access policy.</span></span> <span data-ttu-id="7c2b6-158">No entanto, apenas pode especificar a hora de início Olá, hora de expiração e as permissões num local ou Olá outro.</span><span class="sxs-lookup"><span data-stu-id="7c2b6-158">However, you can only specify hello start time, expiry time, and permissions in one place or hello other.</span></span> <span data-ttu-id="7c2b6-159">Por exemplo, não é possível especificar permissões numa assinatura de acesso partilhado Olá e também especifique-os na política de acesso de Olá armazenado.</span><span class="sxs-lookup"><span data-stu-id="7c2b6-159">For example, you can't specify permissions on hello shared access signature and also specify them on hello stored access policy.</span></span>

<span data-ttu-id="7c2b6-160">Quando adiciona um contentor de tooa de política de acesso armazenada, tem de obter permissões existentes do contentor de Olá, adicionar a nova política de acesso Olá e, em seguida, definir as permissões de um contentor Olá.</span><span class="sxs-lookup"><span data-stu-id="7c2b6-160">When you add a stored access policy tooa container, you must get hello container's existing permissions, add hello new access policy, and then set hello container's permissions.</span></span>

<span data-ttu-id="7c2b6-161">Adicione um novo método que cria uma nova política de acesso armazenado num contentor e devolve o nome de Olá da política de Olá:</span><span class="sxs-lookup"><span data-stu-id="7c2b6-161">Add a new method that creates a new stored access policy on a container and returns hello name of hello policy:</span></span>

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

<span data-ttu-id="7c2b6-162">Na parte inferior de Olá de Olá **main ()** método, antes de chamar o Olá demasiado**Console.ReadLine()**, adicionar Olá seguir de linhas toofirst Limpe quaisquer políticas de acesso existentes e, em seguida, chame Olá  **CreateSharedAccessPolicy()** método:</span><span class="sxs-lookup"><span data-stu-id="7c2b6-162">At hello bottom of hello **Main()** method, before hello call too**Console.ReadLine()**, add hello following lines toofirst clear any existing access policies, and then call hello **CreateSharedAccessPolicy()** method:</span></span>

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

<span data-ttu-id="7c2b6-163">Quando desmarcar as políticas de acesso de Olá num contentor, primeiro deve obter um contentor Olá permissões existentes, em seguida, permissões de limpar Olá e definir permissões de Olá novamente.</span><span class="sxs-lookup"><span data-stu-id="7c2b6-163">When you clear hello access policies on a container, you must first get hello container's existing permissions, then clear hello permissions, then set hello permissions again.</span></span>

### <a name="generate-a-shared-access-signature-uri-on-hello-container-that-uses-an-access-policy"></a><span data-ttu-id="7c2b6-164">Gerar uma assinatura de acesso partilhado URI no contentor de Olá que utiliza uma política de acesso</span><span class="sxs-lookup"><span data-stu-id="7c2b6-164">Generate a shared access signature URI on hello container that uses an access policy</span></span>
<span data-ttu-id="7c2b6-165">Em seguida, iremos criar outro assinatura de acesso partilhado do contentor de Olá que criámos anteriormente, mas neste momento, associar assinatura Olá política de acesso de Olá armazenado que no exemplo anterior Olá foi criada.</span><span class="sxs-lookup"><span data-stu-id="7c2b6-165">Next, we create another shared access signature for hello container that we created earlier, but this time we associate hello signature with hello stored access policy we created in hello previous example.</span></span>

<span data-ttu-id="7c2b6-166">Adicione um novo toogenerate de método outro assinatura de acesso partilhado do contentor de Olá:</span><span class="sxs-lookup"><span data-stu-id="7c2b6-166">Add a new method toogenerate another shared access signature for hello container:</span></span>

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

<span data-ttu-id="7c2b6-167">Na parte inferior de Olá de Olá **main ()** método, antes de chamar o Olá demasiado**Console.ReadLine()**, adicionar Olá seguir Olá de toocall linhas **GetContainerSasUriWithPolicy** método :</span><span class="sxs-lookup"><span data-stu-id="7c2b6-167">At hello bottom of hello **Main()** method, before hello call too**Console.ReadLine()**, add hello following lines toocall hello **GetContainerSasUriWithPolicy** method:</span></span>

```csharp
//Generate a SAS URI for hello container, using a stored access policy tooset constraints on hello SAS.
Console.WriteLine("Container SAS URI using stored access policy: " + GetContainerSasUriWithPolicy(container, sharedAccessPolicyName));
Console.WriteLine();
```

### <a name="generate-a-shared-access-signature-uri-on-hello-blob-that-uses-an-access-policy"></a><span data-ttu-id="7c2b6-168">Gerar um URI de assinatura de acesso partilhado no Olá Blob que utiliza uma política de acesso</span><span class="sxs-lookup"><span data-stu-id="7c2b6-168">Generate a Shared Access Signature URI on hello Blob That Uses an Access Policy</span></span>
<span data-ttu-id="7c2b6-169">Por fim, vamos adicionar um toocreate método semelhante outro blob e gerar uma assinatura de acesso partilhado que está associada a uma política de acesso armazenada.</span><span class="sxs-lookup"><span data-stu-id="7c2b6-169">Finally, we add a similar method toocreate another blob and generate a shared access signature that's associated with a stored access policy.</span></span>

<span data-ttu-id="7c2b6-170">Adicione um novo toocreate de método um blob e gerar uma assinatura de acesso partilhado:</span><span class="sxs-lookup"><span data-stu-id="7c2b6-170">Add a new method toocreate a blob and generate a shared access signature:</span></span>

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

<span data-ttu-id="7c2b6-171">Na parte inferior de Olá de Olá **main ()** método, antes de chamar o Olá demasiado**Console.ReadLine()**, adicionar Olá seguir Olá de toocall linhas **GetBlobSasUriWithPolicy** método:</span><span class="sxs-lookup"><span data-stu-id="7c2b6-171">At hello bottom of hello **Main()** method, before hello call too**Console.ReadLine()**, add hello following lines toocall hello **GetBlobSasUriWithPolicy** method:</span></span>

```csharp
//Generate a SAS URI for a blob within hello container, using a stored access policy tooset constraints on hello SAS.
Console.WriteLine("Blob SAS URI using stored access policy: " + GetBlobSasUriWithPolicy(container, sharedAccessPolicyName));
Console.WriteLine();
```

<span data-ttu-id="7c2b6-172">Olá **main ()** método deve agora ter este aspeto na íntegra.</span><span class="sxs-lookup"><span data-stu-id="7c2b6-172">hello **Main()** method should now look like this in its entirety.</span></span> <span data-ttu-id="7c2b6-173">Execute-a assinatura de acesso partilhado do toowrite Olá janela de consola toohello de URIs, em seguida, copie e cole-los para um ficheiro de texto para utilização num Olá segunda parte deste tutorial.</span><span class="sxs-lookup"><span data-stu-id="7c2b6-173">Run it toowrite hello shared access signature URIs toohello console window, then copy and paste them into a text file for use in hello second part of this tutorial.</span></span>

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

<span data-ttu-id="7c2b6-174">Quando executar a aplicação de consola GenerateSharedAccessSignatures Olá, verá a seguinte de toohello semelhante de saída.</span><span class="sxs-lookup"><span data-stu-id="7c2b6-174">When you run hello GenerateSharedAccessSignatures console application, you'll see output similar toohello following.</span></span> <span data-ttu-id="7c2b6-175">Estes são utilizados na parte 2 do tutorial Olá assinaturas de acesso de Olá partilhado.</span><span class="sxs-lookup"><span data-stu-id="7c2b6-175">These are hello shared access signatures you use in Part 2 of hello tutorial.</span></span>

```
Container SAS URI: https://storagesample.blob.core.windows.net/sascontainer?sv=2016-05-31&sr=c&sig=pFlEZD%2F6sJTNLxD%2FQ26Hh85j%2FzYPxZav6mP1KJwnvJE%3D&se=2017-05-16T16%3A16%3A47Z&sp=wl

Blob SAS URI: https://storagesample.blob.core.windows.net/sascontainer/sasblob.txt?sv=2016-05-31&sr=b&sig=%2FiBWAZbXESzCMvRcm7JwJBK0gT0BtPSWEq4pRwmlBRI%3D&st=2017-05-15T16%3A11%3A48Z&se=2017-05-16T16%3A16%3A48Z&sp=rw

Container SAS URI using stored access policy: https://storagesample.blob.core.windows.net/sascontainer?sv=2016-05-31&sr=c&si=tutorialpolicy&sig=aMb6rKDvvpfiGVsZI2rCmyUra6ZPpq%2BZ%2FLyTgAeec%2Bk%3D

Blob SAS URI using stored access policy: https://storagesample.blob.core.windows.net/sascontainer/sasblobpolicy.txt?sv=2016-05-31&sr=b&si=tutorialpolicy&sig=%2FkTWkT23SS45%2FoF4bK2mqXkN%2BPKs%2FyHuzkfQ4GFoZVU%3D
```

## <a name="part-2-create-a-console-application-tootest-hello-shared-access-signatures"></a><span data-ttu-id="7c2b6-176">Parte 2: Criar um aplicação tootest Olá partilhado o acesso à consola assinaturas</span><span class="sxs-lookup"><span data-stu-id="7c2b6-176">Part 2: Create a console application tootest hello shared access signatures</span></span>
<span data-ttu-id="7c2b6-177">Olá tootest partilhadas assinaturas de acesso que criou nos exemplos anteriores Olá, iremos criar uma segunda aplicação de consola que utiliza as operações de tooperform de assinaturas hello no contentor de Olá e um blob.</span><span class="sxs-lookup"><span data-stu-id="7c2b6-177">tootest hello shared access signatures created in hello previous examples, we create a second console application that uses hello signatures tooperform operations on hello container and on a blob.</span></span>

> [!NOTE]
> <span data-ttu-id="7c2b6-178">Se mais de 24 horas passaram, uma vez que concluir a primeira parte de Olá tutorial Olá, assinaturas hello gerou já não será válidas.</span><span class="sxs-lookup"><span data-stu-id="7c2b6-178">If more than 24 hours have passed since you completed hello first part of hello tutorial, hello signatures you generated will no longer be valid.</span></span> <span data-ttu-id="7c2b6-179">Neste caso, deve executar o código de Olá na toogenerate de aplicação de consola primeiro Olá assinaturas de acesso partilhado raiz para utilização num Olá segunda parte tutorial Olá.</span><span class="sxs-lookup"><span data-stu-id="7c2b6-179">In this case, you should run hello code in hello first console application toogenerate fresh shared access signatures for use in hello second part of hello tutorial.</span></span>
>

<span data-ttu-id="7c2b6-180">No Visual Studio, crie uma nova aplicação de consola do Windows e dê-lhe nome **ConsumeSharedAccessSignatures**.</span><span class="sxs-lookup"><span data-stu-id="7c2b6-180">In Visual Studio, create a new Windows console application and name it **ConsumeSharedAccessSignatures**.</span></span> <span data-ttu-id="7c2b6-181">Adicione referências demasiado[configurationmanager](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager) e [Windowsazure](https://www.nuget.org/packages/WindowsAzure.Storage/), tal como fez anteriormente.</span><span class="sxs-lookup"><span data-stu-id="7c2b6-181">Add references too[Microsoft.WindowsAzure.ConfigurationManager](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager) and [WindowsAzure.Storage](https://www.nuget.org/packages/WindowsAzure.Storage/), as you did previously.</span></span>

<span data-ttu-id="7c2b6-182">Olá parte superior do ficheiro Program.cs de Olá, adicione o seguinte de Olá **utilizando** diretivas:</span><span class="sxs-lookup"><span data-stu-id="7c2b6-182">At hello top of hello Program.cs file, add hello following **using** directives:</span></span>

```csharp
using System.IO;
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Blob;
```

<span data-ttu-id="7c2b6-183">No corpo de Olá de Olá **main ()** método, adicione Olá seguir as constantes string, alterar as assinaturas de acesso de toohello partilhado valores gerado na parte 1 do tutorial Olá.</span><span class="sxs-lookup"><span data-stu-id="7c2b6-183">In hello body of hello **Main()** method, add hello following string constants, changing their values toohello shared access signatures you generated in part 1 of hello tutorial.</span></span>

```csharp
static void Main(string[] args)
{
    const string containerSAS = "<your container SAS>";
    const string blobSAS = "<your blob SAS>";
    const string containerSASWithAccessPolicy = "<your container SAS with access policy>";
    const string blobSASWithAccessPolicy = "<your blob SAS with access policy>";
}
```

### <a name="add-a-method-tootry-container-operations-using-a-shared-access-signature"></a><span data-ttu-id="7c2b6-184">Adicione um método tootry contentor de operações com uma assinatura de acesso partilhado</span><span class="sxs-lookup"><span data-stu-id="7c2b6-184">Add a method tootry container operations using a shared access signature</span></span>
<span data-ttu-id="7c2b6-185">Em seguida, iremos adicionar um método que os testes de algumas operações de contentor com uma assinatura de acesso partilhado do contentor de Olá.</span><span class="sxs-lookup"><span data-stu-id="7c2b6-185">Next, we add a method that tests some container operations using a shared access signature for hello container.</span></span> <span data-ttu-id="7c2b6-186">assinatura de acesso partilhado Olá é tooreturn utilizado um contentor de toohello referência, autenticar o contentor de toohello de acesso com base na assinatura Olá individualmente.</span><span class="sxs-lookup"><span data-stu-id="7c2b6-186">hello shared access signature is used tooreturn a reference toohello container, authenticating access toohello container based on hello signature alone.</span></span>

<span data-ttu-id="7c2b6-187">Adicione Olá método tooProgram.cs os seguintes:</span><span class="sxs-lookup"><span data-stu-id="7c2b6-187">Add hello following method tooProgram.cs:</span></span>

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

<span data-ttu-id="7c2b6-188">Olá atualização **main ()** método toocall **UseContainerSAS()** com ambos Olá de assinaturas de acesso que criou no contentor de Olá partilhado:</span><span class="sxs-lookup"><span data-stu-id="7c2b6-188">Update hello **Main()** method toocall **UseContainerSAS()** with both of hello shared access signatures you created on hello container:</span></span>

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

### <a name="add-a-method-tootry-blob-operations-using-a-shared-access-signature"></a><span data-ttu-id="7c2b6-189">Adicione um método tootry blob de operações com uma assinatura de acesso partilhado</span><span class="sxs-lookup"><span data-stu-id="7c2b6-189">Add a method tootry blob operations using a shared access signature</span></span>
<span data-ttu-id="7c2b6-190">Por último, iremos adicionar um método que os testes de algumas operações de blob a utilizar uma assinatura de acesso partilhado no blob Olá.</span><span class="sxs-lookup"><span data-stu-id="7c2b6-190">Finally, we add a method that tests some blob operations using a shared access signature on hello blob.</span></span> <span data-ttu-id="7c2b6-191">Neste caso, utilizamos o construtor de Olá **CloudBlockBlob(String)**, passando na assinatura de acesso partilhado Olá, tooreturn um blob de toohello de referência.</span><span class="sxs-lookup"><span data-stu-id="7c2b6-191">In this case, we use hello constructor **CloudBlockBlob(String)**, passing in hello shared access signature, tooreturn a reference toohello blob.</span></span> <span data-ttu-id="7c2b6-192">Não outra é necessária autenticação; baseia-se na assinatura Olá individualmente.</span><span class="sxs-lookup"><span data-stu-id="7c2b6-192">No other authentication is required; it's based on hello signature alone.</span></span>

<span data-ttu-id="7c2b6-193">Adicione Olá método tooProgram.cs os seguintes:</span><span class="sxs-lookup"><span data-stu-id="7c2b6-193">Add hello following method tooProgram.cs:</span></span>

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

<span data-ttu-id="7c2b6-194">Olá atualização **main ()** método toocall **UseBlobSAS()** com ambos Olá de assinaturas de acesso que criou no blob Olá partilhado:</span><span class="sxs-lookup"><span data-stu-id="7c2b6-194">Update hello **Main()** method toocall **UseBlobSAS()** with both of hello shared access signatures that you created on hello blob:</span></span>

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

<span data-ttu-id="7c2b6-195">Executar a aplicação de consola Olá e observe Olá saída toosee as operações são permitidas para as assinaturas.</span><span class="sxs-lookup"><span data-stu-id="7c2b6-195">Run hello console application and observe hello output toosee which operations are permitted for which signatures.</span></span> <span data-ttu-id="7c2b6-196">saída de Olá na janela de consola Olá terá um aspeto semelhante toohello seguinte:</span><span class="sxs-lookup"><span data-stu-id="7c2b6-196">hello output in hello console window will look similar toohello following:</span></span>

```
Write operation succeeded for SAS https://storagesample.blob.core.windows.net/sascontainer?sv=2016-05-31&sr=c&sig=32EaQGuFyDMb3yOAey3wq%2B%2FLwgPQxAgSo7UhzLdyIDU%3D&se=2017-05-16T15%3A41%3A20Z&sp=wl

List operation succeeded for SAS https://storagesample.blob.core.windows.net/sascontainer?sv=2016-05-31&sr=c&sig=32EaQGuFyDMb3yOAey3wq%2B%2FLwgPQxAgSo7UhzLdyIDU%3D&se=2017-05-16T15%3A41%3A20Z&sp=wl

Read operation failed for SAS https://storagesample.blob.core.windows.net/sascontainer?sv=2016-05-31&sr=c&sig=32EaQGuFyDMb3yOAey3wq%2B%2FLwgPQxAgSo7UhzLdyIDU%3D&se=2017-05-16T15%3A41%3A20Z&sp=wl
Additional error information: hello remote server returned an error: (403) Forbidden.

Delete operation failed for SAS https://storagesample.blob.core.windows.net/sascontainer?sv=2016-05-31&sr=c&sig=32EaQGuFyDMb3yOAey3wq%2B%2FLwgPQxAgSo7UhzLdyIDU%3D&se=2017-05-16T15%3A41%3A20Z&sp=wl
Additional error information: hello remote server returned an error: (403) Forbidden.

...
```

## <a name="next-steps"></a><span data-ttu-id="7c2b6-197">Passos Seguintes</span><span class="sxs-lookup"><span data-stu-id="7c2b6-197">Next Steps</span></span>

* [<span data-ttu-id="7c2b6-198">Assinaturas de acesso partilhado, parte 1: Olá de compreensão modelo SAS</span><span class="sxs-lookup"><span data-stu-id="7c2b6-198">Shared Access Signatures, Part 1: Understanding hello SAS Model</span></span>](storage-dotnet-shared-access-signature-part-1.md)
* [<span data-ttu-id="7c2b6-199">Gerir o acesso de leitura anónimo toocontainers e blobs</span><span class="sxs-lookup"><span data-stu-id="7c2b6-199">Manage anonymous read access toocontainers and blobs</span></span>](storage-manage-access-to-resources.md)
* [<span data-ttu-id="7c2b6-200">Delegar o acesso com uma assinatura de acesso partilhado (REST API)</span><span class="sxs-lookup"><span data-stu-id="7c2b6-200">Delegating access with a shared access signature (REST API)</span></span>](http://msdn.microsoft.com/library/azure/ee395415.aspx)
* [<span data-ttu-id="7c2b6-201">Introduzir tabela e fila SAS</span><span class="sxs-lookup"><span data-stu-id="7c2b6-201">Introducing Table and Queue SAS</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-table-sas-shared-access-signature-queue-sas-and-update-to-blob-sas.aspx)
