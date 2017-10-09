---
title: 'Tutorial: Encriptar e desencriptar blobs no armazenamento do Azure com o Cofre de chaves do Azure | Microsoft Docs'
description: "Como tooencrypt e desencriptar um blob a utilizar a encriptação do lado do cliente para armazenamento do Microsoft Azure com o Cofre de chaves do Azure."
services: storage
documentationcenter: 
author: adhurwit
manager: jasonsav
editor: tysonn
ms.assetid: 027e8631-c1bf-48c1-9d9b-f6843e88b583
ms.service: storage
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 01/23/2017
ms.author: adhurwit
ms.openlocfilehash: 3eb64f104f378dd09ef295c94e03167655883391
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-encrypt-and-decrypt-blobs-in-microsoft-azure-storage-using-azure-key-vault"></a><span data-ttu-id="019ad-103">Tutorial: Encriptar e desencriptar blobs no armazenamento do Microsoft Azure com o Cofre de chaves do Azure</span><span class="sxs-lookup"><span data-stu-id="019ad-103">Tutorial: Encrypt and decrypt blobs in Microsoft Azure Storage using Azure Key Vault</span></span>
## <a name="introduction"></a><span data-ttu-id="019ad-104">Introdução</span><span class="sxs-lookup"><span data-stu-id="019ad-104">Introduction</span></span>
<span data-ttu-id="019ad-105">Este tutorial abrange como utilizar o toomake de encriptação de armazenamento do lado do cliente com o Cofre de chaves do Azure.</span><span class="sxs-lookup"><span data-stu-id="019ad-105">This tutorial covers how toomake use of client-side storage encryption with Azure Key Vault.</span></span> <span data-ttu-id="019ad-106">Explica como tooencrypt e desencriptar um blob numa aplicação de consola utilização destas tecnologias.</span><span class="sxs-lookup"><span data-stu-id="019ad-106">It walks you through how tooencrypt and decrypt a blob in a console application using these technologies.</span></span>

<span data-ttu-id="019ad-107">**Estimado tempo toocomplete:** 20 minutos</span><span class="sxs-lookup"><span data-stu-id="019ad-107">**Estimated time toocomplete:** 20 minutes</span></span>

<span data-ttu-id="019ad-108">Para obter informações gerais sobre o Cofre de chaves do Azure, consulte [que é o Cofre de chaves do Azure?](../key-vault/key-vault-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="019ad-108">For overview information about Azure Key Vault, see [What is Azure Key Vault?](../key-vault/key-vault-whatis.md).</span></span>

<span data-ttu-id="019ad-109">Para obter informações gerais sobre a encriptação do lado do cliente para o Storage do Azure, consulte [encriptação do lado do cliente e o Cofre de chaves do Azure para armazenamento do Microsoft Azure](storage-client-side-encryption.md).</span><span class="sxs-lookup"><span data-stu-id="019ad-109">For overview information about client-side encryption for Azure Storage, see [Client-Side Encryption and Azure Key Vault for Microsoft Azure Storage](storage-client-side-encryption.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="019ad-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="019ad-110">Prerequisites</span></span>
<span data-ttu-id="019ad-111">toocomplete neste tutorial, tem de ter Olá seguintes:</span><span class="sxs-lookup"><span data-stu-id="019ad-111">toocomplete this tutorial, you must have hello following:</span></span>

* <span data-ttu-id="019ad-112">Uma conta de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="019ad-112">An Azure Storage account</span></span>
* <span data-ttu-id="019ad-113">Visual Studio 2013 ou posterior</span><span class="sxs-lookup"><span data-stu-id="019ad-113">Visual Studio 2013 or later</span></span>
* <span data-ttu-id="019ad-114">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="019ad-114">Azure PowerShell</span></span>

## <a name="overview-of-client-side-encryption"></a><span data-ttu-id="019ad-115">Descrição geral de encriptação do lado do cliente</span><span class="sxs-lookup"><span data-stu-id="019ad-115">Overview of client-side encryption</span></span>
<span data-ttu-id="019ad-116">Para obter uma descrição geral de encriptação do lado do cliente para o Storage do Azure, consulte [encriptação do lado do cliente e o Cofre de chaves do Azure para armazenamento do Microsoft Azure](storage-client-side-encryption.md)</span><span class="sxs-lookup"><span data-stu-id="019ad-116">For an overview of client-side encryption for Azure Storage, see [Client-Side Encryption and Azure Key Vault for Microsoft Azure Storage](storage-client-side-encryption.md)</span></span>

<span data-ttu-id="019ad-117">Eis uma breve descrição como funciona a encriptação do lado do cliente:</span><span class="sxs-lookup"><span data-stu-id="019ad-117">Here is a brief description of how client side encryption works:</span></span>

1. <span data-ttu-id="019ad-118">SDK do cliente de armazenamento do Azure Olá gera uma chave de encriptação de conteúdo (CEK), que é uma chave simétrica one time utilização.</span><span class="sxs-lookup"><span data-stu-id="019ad-118">hello Azure Storage client SDK generates a content encryption key (CEK), which is a one-time-use symmetric key.</span></span>
2. <span data-ttu-id="019ad-119">Dados de cliente são encriptados utilizando este CEK.</span><span class="sxs-lookup"><span data-stu-id="019ad-119">Customer data is encrypted using this CEK.</span></span>
3. <span data-ttu-id="019ad-120">Olá CEK, em seguida, da aplicação (encriptadas) utilizando a chave de encriptação de chaves Olá (de chaves KEK).</span><span class="sxs-lookup"><span data-stu-id="019ad-120">hello CEK is then wrapped (encrypted) using hello key encryption key (KEK).</span></span> <span data-ttu-id="019ad-121">Olá KEK é identificada por um identificador de chave e pode ser um par de chaves assimétricas ou uma chave simétrica e pode ser gerido localmente ou armazenado no Cofre de chaves do Azure.</span><span class="sxs-lookup"><span data-stu-id="019ad-121">hello KEK is identified by a key identifier and can be an asymmetric key pair or a symmetric key and can be managed locally or stored in Azure Key Vault.</span></span> <span data-ttu-id="019ad-122">cliente de armazenamento de Olá próprio nunca tem acesso toohello KEK.</span><span class="sxs-lookup"><span data-stu-id="019ad-122">hello Storage client itself never has access toohello KEK.</span></span> <span data-ttu-id="019ad-123">Apenas ele invoca o algoritmo de chave de moldagem de Olá fornecida pelo Cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="019ad-123">It just invokes hello key wrapping algorithm that is provided by Key Vault.</span></span> <span data-ttu-id="019ad-124">Os clientes podem optar toouse fornecedores personalizados para a chave de encapsulamento de aplicações/abertura se pretenderem.</span><span class="sxs-lookup"><span data-stu-id="019ad-124">Customers can choose toouse custom providers for key wrapping/unwrapping if they want.</span></span>
4. <span data-ttu-id="019ad-125">Olá dados encriptados em seguida, são carregado toohello serviço de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="019ad-125">hello encrypted data is then uploaded toohello Azure Storage service.</span></span>

## <a name="set-up-your-azure-key-vault"></a><span data-ttu-id="019ad-126">Configurar o seu Cofre de chaves do Azure</span><span class="sxs-lookup"><span data-stu-id="019ad-126">Set up your Azure Key Vault</span></span>
<span data-ttu-id="019ad-127">Ordem tooproceed com este tutorial, terá de Olá toodo os seguintes passos, que são descritos no tutorial Olá [introdução ao Cofre de chaves do Azure](../key-vault/key-vault-get-started.md):</span><span class="sxs-lookup"><span data-stu-id="019ad-127">In order tooproceed with this tutorial, you need toodo hello following steps, which are outlined in hello tutorial  [Get started with Azure Key Vault](../key-vault/key-vault-get-started.md):</span></span>

* <span data-ttu-id="019ad-128">Crie um cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="019ad-128">Create a key vault.</span></span>
* <span data-ttu-id="019ad-129">Adicione uma chave ou segredo toohello Cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="019ad-129">Add a key or secret toohello key vault.</span></span>
* <span data-ttu-id="019ad-130">Registe uma aplicação no Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="019ad-130">Register an application with Azure Active Directory.</span></span>
* <span data-ttu-id="019ad-131">Autorize Olá aplicação toouse Olá chave ou segredo.</span><span class="sxs-lookup"><span data-stu-id="019ad-131">Authorize hello application toouse hello key or secret.</span></span>

<span data-ttu-id="019ad-132">Certifique-nota do Olá ClientID e ClientSecret que foram gerados ao registar uma aplicação no Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="019ad-132">Make note of hello ClientID and ClientSecret that were generated when registering an application with Azure Active Directory.</span></span>

<span data-ttu-id="019ad-133">Crie ambas as chaves no Cofre de chaves Olá.</span><span class="sxs-lookup"><span data-stu-id="019ad-133">Create both keys in hello key vault.</span></span> <span data-ttu-id="019ad-134">Partimos do princípio de rest de Olá tutorial Olá que utiliza os seguintes nomes de Olá: ContosoKeyVault e TestRSAKey1.</span><span class="sxs-lookup"><span data-stu-id="019ad-134">We assume for hello rest of hello tutorial that you have used hello following names: ContosoKeyVault and TestRSAKey1.</span></span>

## <a name="create-a-console-application-with-packages-and-appsettings"></a><span data-ttu-id="019ad-135">Criar uma aplicação de consola com pacotes e AppSettings</span><span class="sxs-lookup"><span data-stu-id="019ad-135">Create a console application with packages and AppSettings</span></span>
<span data-ttu-id="019ad-136">No Visual Studio, crie uma nova aplicação de consola.</span><span class="sxs-lookup"><span data-stu-id="019ad-136">In Visual Studio, create a new console application.</span></span>

<span data-ttu-id="019ad-137">Adicione pacotes nuget necessário Olá consola do Gestor de pacotes.</span><span class="sxs-lookup"><span data-stu-id="019ad-137">Add necessary nuget packages in hello Package Manager Console.</span></span>

```
Install-Package WindowsAzure.Storage

// This is hello latest stable release for ADAL.
Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 2.16.204221202

Install-Package Microsoft.Azure.KeyVault
Install-Package Microsoft.Azure.KeyVault.Extensions
```

<span data-ttu-id="019ad-138">Adicione AppSettings toohello App. config.</span><span class="sxs-lookup"><span data-stu-id="019ad-138">Add AppSettings toohello App.Config.</span></span>

```xml
<appSettings>
    <add key="accountName" value="myaccount"/>
    <add key="accountKey" value="theaccountkey"/>
    <add key="clientId" value="theclientid"/>
    <add key="clientSecret" value="theclientsecret"/>
    <add key="container" value="stuff"/>
</appSettings>
```

<span data-ttu-id="019ad-139">Adicione Olá seguinte `using` instruções e disponibilizar se tooadd um projeto de toohello tooSystem.Configuration referência.</span><span class="sxs-lookup"><span data-stu-id="019ad-139">Add hello following `using` statements and make sure tooadd a reference tooSystem.Configuration toohello project.</span></span>

```csharp
using Microsoft.IdentityModel.Clients.ActiveDirectory;
using System.Configuration;
using Microsoft.WindowsAzure.Storage.Auth;
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Blob;
using Microsoft.Azure.KeyVault;
using System.Threading;        
using System.IO;
```

## <a name="add-a-method-tooget-a-token-tooyour-console-application"></a><span data-ttu-id="019ad-140">Adicione um método tooget uma aplicação de consola token tooyour</span><span class="sxs-lookup"><span data-stu-id="019ad-140">Add a method tooget a token tooyour console application</span></span>
<span data-ttu-id="019ad-141">Olá seguinte método é utilizado pelas classes do Cofre de chaves que necessitam de tooauthenticate para o Cofre de chaves de tooyour de acesso.</span><span class="sxs-lookup"><span data-stu-id="019ad-141">hello following method is used by Key Vault classes that need tooauthenticate for access tooyour key vault.</span></span>

```csharp
private async static Task<string> GetToken(string authority, string resource, string scope)
{
    var authContext = new AuthenticationContext(authority);
    ClientCredential clientCred = new ClientCredential(
        ConfigurationManager.AppSettings["clientId"],
        ConfigurationManager.AppSettings["clientSecret"]);
    AuthenticationResult result = await authContext.AcquireTokenAsync(resource, clientCred);

    if (result == null)
        throw new InvalidOperationException("Failed tooobtain hello JWT token");

    return result.AccessToken;
}
```

## <a name="access-storage-and-key-vault-in-your-program"></a><span data-ttu-id="019ad-142">Armazenamento de acesso e o Cofre de chaves no seu programa</span><span class="sxs-lookup"><span data-stu-id="019ad-142">Access Storage and Key Vault in your program</span></span>
<span data-ttu-id="019ad-143">Olá função principal, adicione Olá seguinte código.</span><span class="sxs-lookup"><span data-stu-id="019ad-143">In hello Main function, add hello following code.</span></span>

```csharp
// This is standard code toointeract with Blob storage.
StorageCredentials creds = new StorageCredentials(
    ConfigurationManager.AppSettings["accountName"],
       ConfigurationManager.AppSettings["accountKey"]);
CloudStorageAccount account = new CloudStorageAccount(creds, useHttps: true);
CloudBlobClient client = account.CreateCloudBlobClient();
CloudBlobContainer contain = client.GetContainerReference(ConfigurationManager.AppSettings["container"]);
contain.CreateIfNotExists();

// hello Resolver object is used toointeract with Key Vault for Azure Storage.
// This is where hello GetToken method from above is used.
KeyVaultKeyResolver cloudResolver = new KeyVaultKeyResolver(GetToken);
```

> [!NOTE]
> <span data-ttu-id="019ad-144">Modelos de objetos do Cofre de chaves</span><span class="sxs-lookup"><span data-stu-id="019ad-144">Key Vault Object Models</span></span>
> 
> <span data-ttu-id="019ad-145">É importante toounderstand que existem objetos de Cofre de chaves, na verdade, dois modelos toobe em consideração: um baseia-se no Olá API de REST (espaço de nomes do KeyVault) e outro Olá é uma extensão para a encriptação do lado do cliente.</span><span class="sxs-lookup"><span data-stu-id="019ad-145">It is important toounderstand that there are actually two Key Vault object models toobe aware of: one is based on hello REST API (KeyVault namespace) and hello other is an extension for client-side encryption.</span></span>
> 
> <span data-ttu-id="019ad-146">Olá chave de cofre cliente interage com Olá REST API e compreende JSON Web chaves e segredos para dois tipos de Olá das ações que estão incluídas no Cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="019ad-146">hello Key Vault Client interacts with hello REST API and understands JSON Web Keys and secrets for hello two kinds of things that are contained in Key Vault.</span></span>
> 
> <span data-ttu-id="019ad-147">as extensões do Cofre de chave Olá são as classes que parecem criadas especificamente para a encriptação do lado do cliente no armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="019ad-147">hello Key Vault Extensions are classes that seem specifically created for client-side encryption in Azure Storage.</span></span> <span data-ttu-id="019ad-148">Contêm uma interface de chaves (IKey) e classes com base no conceito Olá de uma resolução de chave.</span><span class="sxs-lookup"><span data-stu-id="019ad-148">They contain an interface for keys (IKey) and classes based on hello concept of a Key Resolver.</span></span> <span data-ttu-id="019ad-149">Existem duas implementações do IKey terá tooknow: RSAKey e SymmetricKey.</span><span class="sxs-lookup"><span data-stu-id="019ad-149">There are two implementations of IKey that you need tooknow: RSAKey and SymmetricKey.</span></span> <span data-ttu-id="019ad-150">Agora acontecer toocoincide com coisas Olá que estão incluídas no Cofre de chaves, mas neste momento estão classes independentes (para que Olá chave e o segredo obtido ao hello do cliente do Cofre de chave não implementam IKey).</span><span class="sxs-lookup"><span data-stu-id="019ad-150">Now they happen toocoincide with hello things that are contained in a Key Vault, but at this point they are independent classes (so hello Key and Secret retrieved by hello Key Vault Client do not implement IKey).</span></span>
> 
> 

## <a name="encrypt-blob-and-upload"></a><span data-ttu-id="019ad-151">Encriptar blob e carregue</span><span class="sxs-lookup"><span data-stu-id="019ad-151">Encrypt blob and upload</span></span>
<span data-ttu-id="019ad-152">Adicione o seguinte Olá code tooencrypt um blob e carregue-o tooyour conta de armazenamento Azure.</span><span class="sxs-lookup"><span data-stu-id="019ad-152">Add hello following code tooencrypt a blob and upload it tooyour Azure storage account.</span></span> <span data-ttu-id="019ad-153">Olá **ResolveKeyAsync** método que é utilizado devolve um IKey.</span><span class="sxs-lookup"><span data-stu-id="019ad-153">hello **ResolveKeyAsync** method that is used returns an IKey.</span></span>

```csharp
// Retrieve hello key that you created previously.
// hello IKey that is returned here is an RsaKey.
// Remember that we used hello names contosokeyvault and testrsakey1.
var rsa = cloudResolver.ResolveKeyAsync("https://contosokeyvault.vault.azure.net/keys/TestRSAKey1", CancellationToken.None).GetAwaiter().GetResult();

// Now you simply use hello RSA key tooencrypt by setting it in hello BlobEncryptionPolicy.
BlobEncryptionPolicy policy = new BlobEncryptionPolicy(rsa, null);
BlobRequestOptions options = new BlobRequestOptions() { EncryptionPolicy = policy };

// Reference a block blob.
CloudBlockBlob blob = contain.GetBlockBlobReference("MyFile.txt");

// Upload using hello UploadFromStream method.
using (var stream = System.IO.File.OpenRead(@"C:\data\MyFile.txt"))
    blob.UploadFromStream(stream, stream.Length, null, options, null);
```

<span data-ttu-id="019ad-154">Segue-se uma captura de ecrã do Olá [Portal clássico do Azure](https://manage.windowsazure.com) para um blob que foram encriptado através de encriptação do lado do cliente com uma chave armazenada num cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="019ad-154">Following is a screenshot from hello [Azure Classic Portal](https://manage.windowsazure.com) for a blob that has been encrypted by using client-side encryption with a key stored in Key Vault.</span></span> <span data-ttu-id="019ad-155">Olá **KeyId** propriedade é Olá URI para a chave de Olá no Cofre de chaves que age como Olá KEK.</span><span class="sxs-lookup"><span data-stu-id="019ad-155">hello **KeyId** property is hello URI for hello key in Key Vault that acts as hello KEK.</span></span> <span data-ttu-id="019ad-156">Olá **EncryptedKey** propriedade contém a versão encriptada Olá de Olá CEK.</span><span class="sxs-lookup"><span data-stu-id="019ad-156">hello **EncryptedKey** property contains hello encrypted version of hello CEK.</span></span>

![Captura de ecrã que mostra os metadados do Blob que inclui os metadados de encriptação](./media/storage-encrypt-decrypt-blobs-key-vault/blobmetadata.png)

> [!NOTE]
> <span data-ttu-id="019ad-158">Se observar o construtor de BlobEncryptionPolicy Olá, verá que possa aceitar uma chave de e/ou de uma resolução.</span><span class="sxs-lookup"><span data-stu-id="019ad-158">If you look at hello BlobEncryptionPolicy constructor, you will see that it can accept a key and/or a resolver.</span></span> <span data-ttu-id="019ad-159">Tenha em atenção que agora não é possível utilizar uma resolução para a encriptação porque faz atualmente não suportam uma chave de predefinição.</span><span class="sxs-lookup"><span data-stu-id="019ad-159">Be aware that right now you cannot use a resolver for encryption because it does not currently support a default key.</span></span>
> 
> 

## <a name="decrypt-blob-and-download"></a><span data-ttu-id="019ad-160">Desencriptar BLOBs e transferir</span><span class="sxs-lookup"><span data-stu-id="019ad-160">Decrypt blob and download</span></span>
<span data-ttu-id="019ad-161">Desencriptação é realmente o utilizador quando utilizar Olá resolução classes fazem sentido.</span><span class="sxs-lookup"><span data-stu-id="019ad-161">Decryption is really when using hello Resolver classes make sense.</span></span> <span data-ttu-id="019ad-162">Olá ID da chave de Olá utilizada para encriptação associado blob Olá nos respetivos metadados, pelo que não existe nenhuma razão para a tooretrieve Olá chave e lembre-se a associação de Olá entre chave e BLOBs.</span><span class="sxs-lookup"><span data-stu-id="019ad-162">hello ID of hello key used for encryption is associated with hello blob in its metadata, so there is no reason for you tooretrieve hello key and remember hello association between key and blob.</span></span> <span data-ttu-id="019ad-163">Basta ter toomake se que essa chave Olá permanece no Cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="019ad-163">You just have toomake sure that hello key remains in Key Vault.</span></span>   

<span data-ttu-id="019ad-164">chave privada do Olá de permaneça uma chave RSA no Cofre de chaves, por isso, para desencriptação toooccur, Olá chave encriptados da Olá metadados do blob que contém Olá CEK é enviado tooKey cofre para a desencriptação.</span><span class="sxs-lookup"><span data-stu-id="019ad-164">hello private key of an RSA Key remains in Key Vault, so for decryption toooccur, hello Encrypted Key from hello blob metadata that contains hello CEK is sent tooKey Vault for decryption.</span></span>

<span data-ttu-id="019ad-165">Adicione Olá seguir o blob de Olá toodecrypt que acabou de carregar.</span><span class="sxs-lookup"><span data-stu-id="019ad-165">Add hello following toodecrypt hello blob that you just uploaded.</span></span>

```csharp
// In this case, we will not pass a key and only pass hello resolver because
// this policy will only be used for downloading / decrypting.
BlobEncryptionPolicy policy = new BlobEncryptionPolicy(null, cloudResolver);
BlobRequestOptions options = new BlobRequestOptions() { EncryptionPolicy = policy };

using (var np = File.Open(@"C:\data\MyFileDecrypted.txt", FileMode.Create))
    blob.DownloadToStream(np, null, options, null);
```

> [!NOTE]
> <span data-ttu-id="019ad-166">Existem alguns dos outros tipos de gestão de chaves resoluções toomake mais fácil, incluindo: AggregateKeyResolver e CachingKeyResolver.</span><span class="sxs-lookup"><span data-stu-id="019ad-166">There are a couple of other kinds of resolvers toomake key management easier, including: AggregateKeyResolver and CachingKeyResolver.</span></span>
> 
> 

## <a name="use-key-vault-secrets"></a><span data-ttu-id="019ad-167">Utilize os segredos do Cofre de chaves</span><span class="sxs-lookup"><span data-stu-id="019ad-167">Use Key Vault secrets</span></span>
<span data-ttu-id="019ad-168">Olá forma toouse um segredo com a encriptação do lado do cliente é através de Olá SymmetricKey classe porque um segredo é, essencialmente, uma chave simétrica.</span><span class="sxs-lookup"><span data-stu-id="019ad-168">hello way toouse a secret with client-side encryption is via hello SymmetricKey class because a secret is essentially a symmetric key.</span></span> <span data-ttu-id="019ad-169">No entanto, conforme indicado acima, um segredo no Cofre de chaves não está mapeado exatamente tooa SymmetricKey.</span><span class="sxs-lookup"><span data-stu-id="019ad-169">But, as noted above, a secret in Key Vault does not map exactly tooa SymmetricKey.</span></span> <span data-ttu-id="019ad-170">Existem alguns aspetos toounderstand:</span><span class="sxs-lookup"><span data-stu-id="019ad-170">There are a few things toounderstand:</span></span>

* <span data-ttu-id="019ad-171">chave de Olá num SymmetricKey tem toobe um comprimento fixo: 128, 192, 256, 384 ou 512 bits.</span><span class="sxs-lookup"><span data-stu-id="019ad-171">hello key in a SymmetricKey has toobe a fixed length: 128, 192, 256, 384, or 512 bits.</span></span>
* <span data-ttu-id="019ad-172">chave de Olá num SymmetricKey deve ser codificado em Base64.</span><span class="sxs-lookup"><span data-stu-id="019ad-172">hello key in a SymmetricKey should be Base64 encoded.</span></span>
* <span data-ttu-id="019ad-173">Um segredo do Cofre de chaves que será utilizado como um SymmetricKey tem toohave um tipo de conteúdo de "application/octet-stream" no Cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="019ad-173">A Key Vault secret that will be used as a SymmetricKey needs toohave a Content Type of "application/octet-stream" in Key Vault.</span></span>

<span data-ttu-id="019ad-174">Eis um exemplo do PowerShell de criar um segredo no Cofre de chaves que podem ser utilizados como uma SymmetricKey.</span><span class="sxs-lookup"><span data-stu-id="019ad-174">Here is an example in PowerShell of creating a secret in Key Vault that can be used as a SymmetricKey.</span></span>
<span data-ttu-id="019ad-175">Tenha em atenção que valor Olá rígido codificada, $key, destina-se apenas a fins de demonstração.</span><span class="sxs-lookup"><span data-stu-id="019ad-175">Please note that hello hard coded value, $key, is for demonstration purpose only.</span></span> <span data-ttu-id="019ad-176">No seu próprio código deverá toogenerate esta chave.</span><span class="sxs-lookup"><span data-stu-id="019ad-176">In your own code you'll want toogenerate this key.</span></span>

```csharp
// Here we are making a 128-bit key so we have 16 characters.
//     hello characters are in hello ASCII range of UTF8 so they are
//    each 1 byte. 16 x 8 = 128.
$key = "qwertyuiopasdfgh"
$b = [System.Text.Encoding]::UTF8.GetBytes($key)
$enc = [System.Convert]::ToBase64String($b)
$secretvalue = ConvertTo-SecureString $enc -AsPlainText -Force

// Substitute hello VaultName and Name in this command.
$secret = Set-AzureKeyVaultSecret -VaultName 'ContoseKeyVault' -Name 'TestSecret2' -SecretValue $secretvalue -ContentType "application/octet-stream"
```

<span data-ttu-id="019ad-177">Na sua aplicação de consola, pode utilizar Olá mesmo chamar como antes tooretrieve neste secreto como um SymmetricKey.</span><span class="sxs-lookup"><span data-stu-id="019ad-177">In your console application, you can use hello same call as before tooretrieve this secret as a SymmetricKey.</span></span>

```csharp
SymmetricKey sec = (SymmetricKey) cloudResolver.ResolveKeyAsync(
    "https://contosokeyvault.vault.azure.net/secrets/TestSecret2/",
    CancellationToken.None).GetAwaiter().GetResult();
```
<span data-ttu-id="019ad-178">E já está.</span><span class="sxs-lookup"><span data-stu-id="019ad-178">That's it.</span></span> <span data-ttu-id="019ad-179">Divirta-se!</span><span class="sxs-lookup"><span data-stu-id="019ad-179">Enjoy!</span></span>

## <a name="next-steps"></a><span data-ttu-id="019ad-180">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="019ad-180">Next steps</span></span>
<span data-ttu-id="019ad-181">Para obter mais informações sobre como utilizar o armazenamento do Microsoft Azure com c#, consulte [biblioteca do cliente de armazenamento do Microsoft Azure para .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx).</span><span class="sxs-lookup"><span data-stu-id="019ad-181">For more information about using Microsoft Azure Storage with C#, see [Microsoft Azure Storage Client Library for .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx).</span></span>

<span data-ttu-id="019ad-182">Para obter mais informações sobre Olá API de REST do Blob, consulte [API de REST do serviço Blob](https://msdn.microsoft.com/library/azure/dd135733.aspx).</span><span class="sxs-lookup"><span data-stu-id="019ad-182">For more information about hello Blob REST API, see [Blob Service REST API](https://msdn.microsoft.com/library/azure/dd135733.aspx).</span></span>

<span data-ttu-id="019ad-183">Para informações mais recentes de Olá no armazenamento do Microsoft Azure, visite toohello [blogue de equipa de armazenamento do Microsoft Azure](http://blogs.msdn.com/b/windowsazurestorage/).</span><span class="sxs-lookup"><span data-stu-id="019ad-183">For hello latest information on Microsoft Azure Storage, go toohello [Microsoft Azure Storage Team Blog](http://blogs.msdn.com/b/windowsazurestorage/).</span></span>
